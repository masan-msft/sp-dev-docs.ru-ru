---
title: "Учебник: переход с UserCustomAction на расширения SharePoint Framework"
description: "Переход от старых (\"классических\") настроек к новой модели на основе расширений SharePoint Framework."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 69e2268b01b0bc42959991d15d7f8d90aaa86b5c
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="migrating-from-usercustomaction-to-sharepoint-framework-extensions"></a>Переход с дополнительных действий пользователя на расширения SharePoint Framework

За последние несколько лет в большинстве корпоративных решений на основе Office 365 и SharePoint Online для расширения пользовательского интерфейса страниц использовалась возможность _CustomAction_ для сайтов на платформе функций SharePoint. Однако в "современном" интерфейсе SharePoint Online большинство таких настроек больше не доступно. Реализовать схожие функции в "современном" интерфейсе можно с помощью новых расширений SharePoint Framework.

Из данного руководства вы узнаете, как перейти от старых ("классических") настроек к новой модели на основе расширений SharePoint Framework.

> [!NOTE]
> Дополнительные сведения о создании расширений SharePoint Framework см. в статье [Обзор расширений SharePoint Framework](../overview-extensions.md).

Сначала рассмотрим доступные разработчикам варианты для создания расширений SharePoint Framework.

* **Настройщик заполнителей**. Расширьте встроенный "современный" пользовательский интерфейс SharePoint Online, добавив собственные элементы HTML и клиентский код к стандартным заполнителям "современных" страниц. На момент написания этой статьи заполнители доступны в верхнем и нижнем колонтитулах каждой "современной" страницы.
* **Набор команд**. Добавьте собственные элементы меню ECB или кнопки на панель команд списка или библиотеки. С этими командами можно связать любое действие JavaScript (TypeScript).
* **Настройщик полей**. Настройте отображение поля в списке, используя собственные элементы HTML и клиентский код.

Наиболее полезное в нашем контексте расширение — настройщик заполнителей.

Предположим, вы добавили в SharePoint Online элемент _CustomAction_ для отображения собственного нижнего колонтитула на всех страницах сайта.

Ниже представлен XML-код этого элемента _CustomAction_ на платформе SharePoint Feature Framework.

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="jQueryCDN"
                Title="jQueryCDN"
                Description="Loads jQuery from the public CDN"
                ScriptSrc="https://code.jquery.com/jquery-3.2.1.slim.min.js"
                Location="ScriptLink"
                Sequence="100" />
  <CustomAction Id="spoCustomBar"
                Title="spoCustomBar"
                Description="Loads a script to rendere a custom footer"
                Location="ScriptLink"
                ScriptSrc="SiteAssets/SPOCustomUI.js"
                Sequence="200" />
</Elements>
```

Как видите, в файле определено несколько элементов типа _CustomAction_, которые необходимо включить на страницы целевого сайта: код jQuery, загружаемый через общедоступную сеть CDN, и пользовательский файл JavaScript.

Для полноты картины ниже показан код JavaScript, который отрисовывает специальный нижний колонтитул с предопределенными элементами меню.

```JavaScript
var SPOCustomUI = SPOCustomUI || {};

SPOCustomUI.setUpCustomFooter = function () {
    if ($("#SPOCustomFooter").length)
        return;

    var footerContainer = $("<div>");
    footerContainer.attr("id", "SPOCustomFooter");

    footerContainer.append("<ul>");

    $("#s4-workspace").append(footerContainer);
}

SPOCustomUI.addCustomFooterText = function (id, text) {
    if ($("#" + id).length)
        return;

    var customElement = $("<div>");
    customElement.attr("id", id);
    customElement.html(text);

    $("#SPOCustomFooter > ul").before(customElement);

    return customElement;
}

SPOCustomUI.addCustomFooterLink = function (id, text, url) {
    if ($("#" + id).length)
        return;

    var customElement = $("<a>");
    customElement.attr("id", id);
    customElement.attr("href", url);
    customElement.html(text);

    $("#SPOCustomFooter > ul").append($("<li>").append(customElement));

    return customElement;
}

SPOCustomUI.loadCSS = function (url) {
    var head = document.getElementsByTagName('head')[0];
    var style = document.createElement('link');
    style.type = 'text/css';
    style.rel = 'stylesheet';
    style.href = url;
    head.appendChild(style);
}

SPOCustomUI.init = function (whenReadyDoFunc) {
    // avoid executing inside iframes (used by Sharepoint for dialogs)
    if (self !== top) return;

    if (!window.jQuery) {
        // jQuery is needed for Custom Bar to run
        setTimeout(function () { SPOCustomUI.init(whenReadyDoFunc); }, 50);
    } else {
        $(function () {
            SPOCustomUI.setUpCustomFooter();
            whenReadyDoFunc();
        });
    }
}

// The following initializes the custom footer with some fake links
SPOCustomUI.init(function () {

    var currentScriptUrl;

    var currentScript = document.querySelectorAll("script[src*='SPOCustomUI']");
    if (currentScript.length > 0) {
        currentScriptUrl = currentScript[0].src;
    }
    if (currentScriptUrl != undefined) {
        var currentScriptBaseUrl = currentScriptUrl.substring(0, currentScriptUrl.lastIndexOf('/') + 1);
        SPOCustomUI.loadCSS(currentScriptBaseUrl + 'SPOCustomUI.css');
    }

    SPOCustomUI.addCustomFooterText('SPOFooterCopyright', '&copy; 2017, Contoso Inc.');
    SPOCustomUI.addCustomFooterLink('SPOFooterCRMLink', 'CRM', 'CRM.aspx');
    SPOCustomUI.addCustomFooterLink('SPOFooterSearchLink', 'Search Center', 'SearchCenter.aspx');
    SPOCustomUI.addCustomFooterLink('SPOFooterPrivacyLink', 'Privacy Policy', 'Privacy.aspx');
});
```

<br/>

На следующем рисунке показан результат предыдущего дополнительного действия на домашней странице классического сайта.

![Специальный нижний колонтитул на классической странице](../../../images/user-custom-action-footer-sample.png)

<br/>

Ниже описано, как перенести старое решение в "современный" пользовательский интерфейс.

> [!NOTE]
> Прежде чем выполнять действия, описанные в этой статье, обязательно [настройте среду разработки](../../set-up-your-development-environment.md).

## <a name="create-a-new-sharepoint-framework-solution"></a>Создание решения SharePoint Framework

1. Откройте любую командную строку (например, PowerShell, CMD.EXE или Cmder). Создайте папку для решения под названием **spfx-react-custom-footer** и создайте решение SharePoint Framework, запустив генератор Yeoman с помощью следующей команды:

    ```
    yo @microsoft/sharepoint
    ```

2. При появлении запроса:

    * Оставьте имя решения по умолчанию (**spfx-react-custom-footer**) и нажмите клавишу ВВОД.
    * Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.
    * Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу ВВОД.
    * Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании.
    * Выберите **Extension** (Расширение) в качестве типа создаваемого клиентского компонента.
    * Выберите для создаваемого расширения тип **Настройщик заполнителей**.
    * Укажите для настройщика заполнителей имя **CustomFooter**.

    ![Пользовательский интерфейс генератора Yeoman при создании специального нижнего колонтитула](../../../images/spfx-react-custom-footer-yeoman.png)

    На этом этапе Yeoman устанавливает необходимые зависимости и формирует шаблон файлов и папок решения вместе с расширением **CustomFooter**. Это может занять несколько минут.

    После успешного формирования шаблона должно появиться следующее сообщение:

    ![Формирование шаблона завершено](../../../images/spfx-react-custom-footer-yeoman-completed.png)

3. Чтобы заблокировать версию зависимостей проекта, выполните следующую команду:

    ```
    npm shrinkwrap
    ```

4. Запустите Visual Studio Code (или другой редактор кода) и начните разработку решения. Чтобы запустить Visual Studio Code, можно выполнить следующий оператор:

    ```
    code .
    ```

## <a name="define-the-new-ui-elements"></a>Определение новых элементов пользовательского интерфейса

Элементы специального нижнего колонтитула отрисовываются с помощью React и пользовательского компонента React. Конечно, вы можете создать элементы нижнего колонтитула с помощью любой технологии. В этом руководстве мы используем React, чтобы получить доступ к компонентам Office UI Fabric для React.

> [!NOTE]
> Дополнительные сведения о разработке решений с помощью React см. в [этом руководстве](https://reactjs.org/tutorial/tutorial.html).

1. Откройте файл **CustomFooterApplicationCustomizer.manifest.json** в папке **src/extensions/customFooter**. Скопируйте значение свойства `id` и сохраните его в надежном месте, так как оно понадобится вам позже.

2. Откройте файл **CustomFooterApplicationCustomizer.ts** в папке **src/расширения/customFooter** и импортируйте типы `PlaceholderContent` и `PlaceholderName` из пакета `'@microsoft/sp-application-base'`. В самом начале файла добавьте директивы импорта для React.

    В приведенном ниже фрагменте кода показан раздел импорта в файле **CustomFooterApplicationCustomizer.ts**.

    ``` TypeScript
    import * as React from 'react';
    import * as ReactDom from 'react-dom';

    import { override } from '@microsoft/decorators';
    import { Log } from '@microsoft/sp-core-library';
    import {
    BaseApplicationCustomizer,
    PlaceholderContent,
    PlaceholderName
    } from '@microsoft/sp-application-base';
    import { Dialog } from '@microsoft/sp-dialog';

    import * as strings from 'CustomFooterApplicationCustomizerStrings';
    import CustomFooter from './components/CustomFooter';
    ```

3. Найдите определение класса `CustomFooterApplicationCustomizer` и объявите новый частный элемент `bottomPlaceholder` типа `PlaceholderContent | undefined`. 

4. В переопределении метода `onInit` вызовите пользовательскую функцию `renderPlaceHolders` и определите эту функцию.

    В приведенном ниже фрагменте кода показана реализация класса CustomFooterApplicationCustomizer.

    ``` TypeScript
    /** A Custom Action which can be run during execution of a Client Side Application */
    export default class CustomFooterApplicationCustomizer
    extends BaseApplicationCustomizer<ICustomFooterApplicationCustomizerProperties> {

    // This private member holds a reference to the page's footer
    private _bottomPlaceholder: PlaceholderContent | undefined;

    @override
    public onInit(): Promise<void> {
        Log.info(LOG_SOURCE, `Initialized ${strings.Title}`);

        let message: string = this.properties.testMessage;
        if (!message) {
        message = '(No properties were provided.)';
        }

        // Call render method for rendering the needed html elements
        this._renderPlaceHolders();

        return Promise.resolve();
    }

    private _renderPlaceHolders(): void {

        // Handling the bottom placeholder
        if (!this._bottomPlaceholder) {
        this._bottomPlaceholder =
            this.context.placeholderProvider.tryCreateContent(
            PlaceholderName.Bottom);

        // The extension should not assume that the expected placeholder is available.
        if (!this._bottomPlaceholder) {
            console.error('The expected placeholder (Bottom) was not found.');
            return;
        }

        const element: React.ReactElement<{}> = React.createElement(CustomFooter);
        
        ReactDom.render(element, this._bottomPlaceholder.domElement);
        }
    }
    }
    ```

    Метод `renderPlaceHolders` ищет заполнитель типа `Bottom` и (если он найден) отрисовывает его содержимое. В самом конце метода `renderPlaceHolders` код создает новый экземпляр компонента React `CustomFooter` и отрисовывает его в заполнителе в нижней части страницы (т. е. на месте нижнего колонтитула).

    > [!NOTE]
    > В "современной" модели компонент React заменяет файл JavaScript из "классической" модели. Конечно, вы можете по-прежнему отрисовывать нижний колонтитул, используя по большей части имеющийся чистый код JavaScript. Однако рекомендуется обновить реализацию. Это целесообразно с методологической, и с практической точки зрения.

5. Добавьте новую папку под названием **components** в папку **src/extensions/customFooter**. Создайте в новой папке файл и назовите его **CustomFooter.tsx**.

    В приведенном ниже фрагменте кода показан исходный файл компонента.

    ```TypeScript
    import * as React from 'react';

    import { CommandButton } from 'office-ui-fabric-react/lib/Button';

    export default class CustomFooter extends React.Component<{}, {}> {

    public render(): React.ReactElement<{}> {

        return (
        <div className={`ms-bgColor-neutralLighter ms-fontColor-white`}>
            <div className={`ms-bgColor-neutralLighter ms-fontColor-white`}>
                <div className={`ms-Grid`}>
                    <div className="ms-Grid-row">
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                            <CommandButton 
                                data-automation="CopyRight"
                                href={`CRM.aspx`}>&copy; 2017, Contoso Inc.</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                        <CommandButton 
                                data-automation="CRM"
                                iconProps={ { iconName: 'People' } }
                                href={`CRM.aspx`}>CRM</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                        <CommandButton 
                                data-automation="SearchCenter"
                                iconProps={ { iconName: 'Search' } }
                                href={`SearchCenter.aspx`}>Search Center</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm2 ms-md2 ms-lg2">
                            <CommandButton 
                                data-automation="Privacy"
                                iconProps={ { iconName: 'Lock' } }
                                href={`Privacy.aspx`}>Privacy Policy</CommandButton>
                        </div>
                        <div className="ms-Grid-col ms-sm4 ms-md4 ms-lg4">
                        </div>
                    </div>
                </div>
            </div>
        </div>
        );
    }
    }
    ```

    В данном документе не рассматривается создание компонента React. В любом случае обратите внимание на операторы `import` в начале файла, где компонент импортирует React и компонент React `CommandButton` из библиотеки компонентов Office UI Fabric.
    
    Вывод компонента `CustomFooter` определен в методе `render` с несколькими экземплярами компонента `CommandButton`, представляющими собой ссылки в нижнем колонтитуле. Все выходные данные HTML заключены в макет сетки из Office UI Fabric.
    
    > [!NOTE]
    > Дополнительные сведения о макете сетки Office UI Fabric см. в разделе [Гибкий макет](https://developer.microsoft.com/ru-RU/fabric#/styles/layout).

    На приведенном ниже рисунке показан результат.

    ![Специальный нижний колонтитул на "современном" сайте](../../../images/spfx-react-custom-footer-output.png)

## <a name="test-the-solution-in-debug-mode"></a>Тестирование решения в режиме отладки

1. Вернитесь в окно консоль и выполните следующую команду, чтобы выполнить сборку и запустить локальный сервер Node.js для размещения решения.

    ```
    gulp serve --nobrowser
    ```

2. Теперь откройте любой браузер и перейдите на "современную" страницу любого "современного" сайта группы. Добавьте приведенные ниже параметры строки запроса в URL-адрес страницы.

    ```
    ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"82242bbb-f951-4c71-a978-80eb8f35e4c1":{"location":"ClientSideExtension.ApplicationCustomizer"}}
    ```

    В этой строке запроса замените GUID сохраненным значением `id` из файла **CustomFooterApplicationCustomizer.manifest.json**. 
    
    При выполнении запроса страницы появится запрос разрешения на запуск кода с localhost (окно с заголовком "Разрешить скрипты отладки?"). Конечно, если вы хотите отладить и протестировать решение локально, необходимо разрешить загрузку скриптов отладки.

## <a name="package-and-host-the-solution"></a>Упаковка и размещение решения

Если вы довольны результатом, теперь можно упаковать решение и разместить его в настоящей инфраструктуре.
Прежде чем собирать пакет, необходимо объявить XML-файл Feature Framework для подготовки расширения.

### <a name="review-feature-framework-elements"></a>Обзор элементов Feature Framework

1. В редакторе кода откройте вложенную папку **/sharepoint/assets** в папке решения и измените файл **elements.xml**. В приведенном ниже фрагменте кода показано, как должен выглядеть файл.

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
        <CustomAction
            Title="CustomFooter"
            Location="ClientSideExtension.ApplicationCustomizer"
            ClientSideComponentId="82242bbb-f951-4c71-a978-80eb8f35e4c1">
        </CustomAction>
    </Elements>
    ```

    Как видите, он напоминает файл SharePoint Feature Framework из "классической" модели, но использует атрибут `ClientSideComponentId`, чтобы ссылаться на свойство `id` специального расширения. Вы также можете добавить атрибут `ClientSideComponentProperties`, если нужно предоставить расширению пользовательские параметры (в данном руководстве это не требуется).

2. Откройте файл **package-solution.json** в папке **/config** решения. В файле вы увидите ссылку на файл **elements.xml** в разделе `assets`.

    ```JSON
    {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
        "name": "spfx-react-custom-footer-client-side-solution",
        "id": "911728a5-7bde-4453-97b2-2eba59277ed3",
        "version": "1.0.0.0",
        "features": [
        {
            "title": "Application Extension - Deployment of custom action.",
            "description": "Deploys a custom action with ClientSideComponentId association",
            "id": "f16a2612-3163-46ad-9664-3d3daac68cff",
            "version": "1.0.0.0",
            "assets": {
            "elementManifests": [
                "elements.xml"
            ]
            }
        }
        ]
    },
    "paths": {
        "zippedPackage": "solution/spfx-react-custom-footer.sppkg"
    }
    }
    ```

### <a name="enable-the-cdn-in-your-office-365-tenant"></a>Включение сети доставки содержимого (CDN) в клиенте Office 365

Теперь необходимо разместить расширение в среде внешнего размещения. Сеть доставки содержимого Office 365 — самый простой способ размещать решения SharePoint непосредственно из их клиента, пользуясь при этом преимуществами службы сетей доставки содержимого (CDN) для сокращения времени загрузки ресурсов.

1. Скачайте [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588), чтобы убедиться, что у вас установлена последняя версия.

2. Подключитесь к клиенту SharePoint Online с помощью PowerShell:
    
    ```powershell
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. Чтобы узнать текущее состояние настроек общедоступной сети CDN для клиента, поочередно выполните указанные ниже команды. 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. Включите общедоступную сеть доставки содержимого в клиенте:
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    Теперь в клиенте включена общедоступная сеть доставки содержимого с использованием разрешенной конфигурации типов файлов по умолчанию. Это означает, что поддерживаются такие расширения: CSS, EOT, CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF.

5. Откройте браузер и перейдите к семейству веб-сайтов, в котором вы хотите разместить свою библиотеку CDN. Это может быть любое семейство веб-сайтов в клиенте. Это руководство описывает создание библиотеки CDN, но вы также можете использовать отдельную папку в любой существующей библиотеке документов как конечную точку CDN.

6. В семействе веб-сайтов создайте библиотеку документов **CDN** и добавьте в нее папку **customfooter**.
    
7. В консоли PowerShell добавьте новый источник сети доставки содержимого. В этом случае мы задаем источник `*/cdn`, то есть в качестве источника сети доставки содержимого будет выступать любая относительная папка с именем **cdn**.
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. Выполните указанную ниже команду, чтобы получить список источников сети доставки содержимого клиента:
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
    Обратите внимание, что новый источник указан как допустимый источник сети доставки содержимого. Окончательная настройка источника занимает приблизительно 15 минут, поэтому мы можем продолжить подготовку расширения, которое будет размещено в источнике после развертывания. 

    ![Список общедоступных источников в клиенте](../../../images/ext-app-cdn-origins-pending.png)

    Если рядом с названием источника нет уведомления `(configuration pending)`, он готов к использованию в клиенте. Это указывает на выполняющуюся настройку SharePoint Online и системы CDN. 

### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a>Обновление параметров решения и его публикация в сети доставки содержимого

Теперь необходимо обновить решение для использования только что созданной сети CDN в качестве среды внешнего размещения и опубликовать в ней пакет решения. Для этого выполните указанные ниже действия.

1. Вернитесь к ранее созданному решению, чтобы внести необходимые изменения в URL-адреса.
    
2. Обновите файл _write-manifestests.json_ (в папке _config_), как показано ниже, чтобы он указывал на конечную точку CDN. Используйте `publiccdn.sharepointonline.com` в качестве префикса, а затем дополните URL-адрес фактическим путем к вашему клиенту. Формат URL-адреса для сети доставки содержимого:
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Путь к конечной точке CDN в манифесте записи](../../../images/spfx-react-custom-footer-write-manifest.png)

3. Сохраните изменения.

4. Выполните описанную ниже задачу для упаковки решения. При этом будет выполнена сборка конечной версии проекта с использованием URL-адреса сети доставки содержимого, указанного в файле **writer-manifest.json**. Результат будет помещен в папку **./temp/deploy**. Эти файлы вам нужно будет добавить в папку SharePoint, представляющую собой конечную точку CDN. 
    
    ```
    gulp bundle --ship
    ```
    
5. Выполните указанную ниже команду, чтобы упаковать решение. Эта команда создает пакет **spfx-react-custom-footer.sppkg** в папке **sharepoint/solution** и подготавливает ресурсы в папке **temp/deploy** к развертыванию в CDN.
    
    ```
    gulp package-solution --ship
    ```
    
6. Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте, а затем нажмите кнопку _Развернуть_.

    ![Диалоговое окно подтверждения доверия в каталоге приложений со ссылкой на конечную точку CDN](../../../images/spfx-react-custom-footer-cdn-address.png)

7. Отправьте или перетащите файлы из папки **temp/deploy** в созданную ранее папку **CDN/customfooter**.

### <a name="install-and-run-the-solution"></a>Установка и запуск решения

1. Откройте браузер и перейдите на любой "современный" сайт.

2. Перейдите на страницу **Контент сайта** и добавьте новое **приложение**.

3. Выберите **Из вашей организации**, чтобы просмотреть решения, доступные в каталоге приложений.

4. Выберите решение **spfx-react-custom-footer-client-side-solution** и установите его на целевом сайте.

    ![Добавление пользовательского интерфейса для добавления решения на сайт](../../../images/spfx-react-custom-footer-add-app.png)

5. После установки приложения обновите страницу или перейдите на домашнюю страницу сайта. Внизу страницы должен отображаться специальный нижний колонтитул.

Поздравляем! Вы создали специальный нижний колонтитул, используя расширения SharePoint Framework.

## <a name="see-also"></a>См. также

- [Обзор расширений SharePoint Framework](../overview-extensions.md)
