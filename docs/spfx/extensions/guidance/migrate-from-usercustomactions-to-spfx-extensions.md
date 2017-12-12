# <a name="migrating-from-usercustomaction-to-sharepoint-framework-extensions"></a>Переход с UserCustomAction на расширения SharePoint Framework

За последние несколько лет в большинстве корпоративных решений на основе Office 365 и SharePoint Online для расширения пользовательского интерфейса страниц использовалась возможность _CustomAction_ для сайтов на платформе функций SharePoint. Однако на данный момент, с появлением "современного" пользовательского интерфейса SharePoint Online, большинство таких модификаций недоступно. К счастью, с помощью новых расширений SharePoint Framework вы можете реализовать практически идентичные функции в "современном" пользовательском интерфейсе. Из данного руководства вы узнаете, как перейти от старых ("классических") модификаций к новой модели, основанной на расширениях SharePoint Framework.

> [!IMPORTANT]
> "Классический" интерфейс не объявляется устаревшим — он будет сосуществовать с "современным".

_**Область применения:** SharePoint Online_

## <a name="understanding-sharepoint-framework-extensions"></a>Общие сведения о расширениях SharePoint Framework
<a name="spfxExtensions"> </a> Для начала рассмотрим доступные разработчикам варианты расширений SharePoint Framework:

* **Настройщик приложений**. Расширьте встроенный "современный" пользовательский интерфейс SharePoint Online, добавив пользовательские элементы HTML и клиентский код в заранее определенные заполнители на "современных" страницах. На момент написания этой статьи заполнители доступны в верхнем и нижнем колонтитулах каждой "современной" страницы.
* **Набор команд**. Позволяет добавлять пользовательские пункты меню ECB и настраиваемые кнопки на панель команд или в представление списка или библиотеки. С этими командами можно связать любое действие JavaScript (TypeScript).
* **Настройщик полей**. Настройте отображение поля в представлении списка, используя настраиваемые элементы HTML и клиентский код.

Как вы могли понять из приведенных выше описаний, в нашем случае наиболее удобным вариантом будет расширение "Настройщик приложений".

> [!NOTE]
> Дополнительные сведения о расширениях SharePoint Framework см. в статье ["Обзор расширений SharePoint Framework"](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/extensions/overview-extensions).

## <a name="migrating-a-usercustomaction-to-an-spfx-application-customizer"></a>Перенос элемента UserCustomAction в настройщик приложений SPFx
<a name="FromUserCustomActionToApplicationCustomizer"> </a> Предположим, у вас есть элемент _CustomAction_ в SharePoint Online, необходимый для создания настраиваемого нижнего колонтитула на всех страницах сайта.
Ниже представлен фрагмент кода XML, в котором определяется этот элемент _CustomAction_ на платформе функций SharePoint.

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

Как видите, в файле элементов функции определяется пара элементов типа _CustomAction_, чтобы включить в страницы целевого сайта как код jQuery, загружаемый через общедоступную сеть CDN, так и пользовательский файл JavaScript, который отображает настраиваемый нижний колонтитул.

Кроме того, для полноты здесь представлен код JavaScript, который отображает настраиваемый нижний колонтитул, где для простоты пункты меню заранее определены в коде.

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

На приведенном ниже рисунке представлены выходные данные вышеописанного дополнительного действия на домашней странице классического сайта.

![Пользовательский нижний колонтитул на классической странице](../../../images/user-custom-action-footer-sample.png)

Чтобы перенести представленное выше решение в "современный" пользовательский интерфейс, необходимо выполнить указанные ниже действия.

### <a name="create-a-new-sharepoint-framework-solution"></a>Создание решения SharePoint Framework
<a name="CreateApplicationCustomizer"> </a> Подготовив среду разработки к созданию решений SharePoint Framework, вы можете приступить к созданию расширения SharePoint Framework, выполнив действия, описанные в статье ["Как настроить среду разработки клиентских веб-частей SharePoint"](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/set-up-your-development-environment).

1. Откройте любое средство командной строки (PowerShell, CMD.EXE, Cmder и т. д.), создайте папку для решения (назовите ее _spfx-react-custom-footer_) и создайте решение SharePoint Framework, запустив генератор Yeoman с помощью следующей команды:

```
yo @microsoft/sharepoint
```

При появлении соответствующих запросов укажите следующие параметры:
* Оставьте имя решения по умолчанию (_spfx-react-custom-footer_) и нажмите клавишу ВВОД.
* Выберите SharePoint Online only (latest) (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.
* Выберите Use the current folder (Использовать текущую папку) и нажмите клавишу ВВОД.
* Выберите N, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.
* Выберите Extension (Расширение) в качестве типа создаваемого клиентского компонента.
* Выберите для создаваемого расширения тип "Настройщик приложений".
* Укажите для настройщика приложений имя CustomFooter.

![Пользовательский интерфейс генератора Yeoman при создании решения для пользовательского нижнего колонтитула](../../../images/spfx-react-custom-footer-yeoman.png)

На этом этапе Yeoman установит необходимые зависимости и сформирует шаблон файлов и папок решения вместе с расширением _CustomFooter_. Это может занять несколько минут.

После успешного формирования шаблона должно появиться следующее сообщение:

![Формирование шаблона завершено](../../../images/spfx-react-custom-footer-yeoman-completed.png)

2. Чтобы заблокировать версию зависимостей проекта, выполните следующую команду:

```
npm shrinkwrap
```

3. Теперь запустите Visual Studio Code (или другой редактор кода) и начните разработку решения. Чтобы запустить Visual Studio Code, можно выполнить приведенный ниже оператор.

```
code .
```

### <a name="define-the-new-ui-elements"></a>Определение новых элементов пользовательского интерфейса
<a name="DefineApplicationCustomizerUI"> </a> Элементы пользовательского интерфейса в нижнем колонтитуле будут отрисовываться с помощью React и пользовательского компонента React. Конечно, вы можете создать элементы пользовательского интерфейса в нижнем колонтитуле с помощью любой технологии. В этом руководстве мы используем React, чтобы получить доступ к компонентам Office UI Fabric для React.

> [!NOTE]
> Дополнительные сведения о разработке решений с помощью React см. в [этом руководстве по React](https://reactjs.org/tutorial/tutorial.html).

1. Для начала откройте файл _CustomFooterApplicationCustomizer.manifest.json_ в папке _src/extensions/customFooter_. Скопируйте значение свойства _id_ и сохраните его в надежном месте, так как оно потребуется позже.

2. Теперь откройте файл _CustomFooterApplicationCustomizer.ts_ в той же папке и импортируйте типы _PlaceholderContent_ и _PlaceholderName_ из пакета _@microsoft/sp-application-base_.
Кроме того, в самом начале файла добавьте директивы импорта для React.

В приведенном ниже фрагменте кода показан раздел импорта в файле _CustomFooterApplicationCustomizer.ts_.

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

3. Найдите определение класса _CustomFooterApplicationCustomizer_ и объявите новый частный элемент __bottomPlaceholder_ типа _PlaceholderContent | undefined_.
Теперь в переопределении метода _onInit_ вызовите пользовательскую функцию __renderPlaceHolders_ и определите эту функцию.

В приведенном ниже фрагменте кода показана реализация класса настройщика приложений в нижнем колонтитуле.

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

Для начала метод __renderPlaceHolders_ ищет заполнитель типа _Bottom_ и (если он найден) отображает его содержимое.
На самом деле в самом конце метода __renderPlaceHolders_ код создает экземпляр компонента React _CustomFooter_ и отображает его в заполнителе в нижней части страницы (т. е. на месте нижнего колонтитула).

> [!NOTE]
> В "современной" модели компонент React заменит файл JavaScript из "классической" модели. Конечно, вы можете по-прежнему отображать весь нижний колонтитул с помощью чистого кода JavaScript и использовать большую часть имеющегося кода. Тем не менее обновление реализации обосновано не только с точки зрения технологий, но и с точки зрения кода.

4. Добавьте новую папку с именем components в папку _src/extensions/customFooter_. Создайте в новой папке файл и назовите его _CustomFooter.tsx_.
В приведенном ниже фрагменте кода показан файл исходного кода компонента.

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

В данном документе не рассматривается создание компонента React. В любом случае обратите внимание на операторы _import_ в начале файла, где компонент импортирует React, и на компонент React _CommandButton_ из библиотеки компонентов Office UI Fabric.
Кроме того, в методе _render_ для компонента определяются выходные данные элемента _CustomFooter_ с несколькими экземплярами компонента _CommandButton_ для ссылок в нижнем колонтитуле.
Все выходные данные HTML заключены в макет сетки из Office UI Fabric.
> [!NOTE]
> Дополнительные сведения о макете сетки Office UI Fabric см. в документе [Адаптивная разметка](https://developer.microsoft.com/ru-RU/fabric#/styles/layout).

На приведенном ниже рисунке показаны выходные данные.

![Пользовательский нижний колонтитул на "современном" сайте](../../../images/spfx-react-custom-footer-output.png)

### <a name="test-the-solution-in-debug-mode"></a>Тестирование решения в режиме отладки
<a name="DebugApplicationCustomizer"> </a> Теперь все готово к тестированию решения в режиме отладки. 

1. Вернитесь к окну консоли и выполните следующую команду:

```
gulp serve --nobrowser
```

Приведенная выше команда выполняет сборку решения и запускает локальный сервер Node.js для его размещения.

2. Теперь откройте любой браузер и перейдите к "современной" странице на любом "современном" сайте группы. Затем добавьте приведенные ниже параметры строки запроса к URL-адресу страницы.

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"82242bbb-f951-4c71-a978-80eb8f35e4c1":{"location":"ClientSideExtension.ApplicationCustomizer"}}
```

В приведенной выше строке запроса необходимо заменить GUID на сохраненное ранее значение _id_ из файла _CustomFooterApplicationCustomizer.manifest.json_. Обратите внимание, что при выполнении запроса страницы появится окно с предупреждающим сообщением "Разрешить скрипты отладки?", где из соображений безопасности спрашивается ваше согласие на запуск кода с localhost. Конечно, если вы хотите отладить и протестировать решение локально, потребуется разрешить загрузку скриптов отладки.

### <a name="package-and-host-the-solution"></a>Упаковка и размещение решения
<a name="PackageAndHostApplicationCustomizer"> </a> Если вы довольны результатом, теперь можно упаковать решение и разместить его в настоящей инфраструктуре.
Прежде чем собирать пакет, необходимо объявить XML-файл платформы функций для подготовки расширения.

#### <a name="review-feature-framework-elements"></a>Обзор элементов платформы функций
В редакторе кода откройте вложенную папку _/sharepoint/assets_ в папке решения и измените файл _elements.xml_.
В приведенном ниже фрагменте кода показано, как должен выглядеть файл.

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

Как видите, он напоминает файл платформы функций SharePoint из "классической" модели, но использует атрибут _ClientSideComponentId_, чтобы ссылаться на свойство _id_ настраиваемого расширения. Вы также можете добавить атрибут _ClientSideComponentProperties_, если нужно предоставить расширению пользовательские параметры (в данном руководстве это не требуется).

Теперь откройте файл _package-solution.json_ в папке _/config_ решения. В файле вы увидите ссылку на файл _elements.xml_ в разделе _assets_.

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

#### <a name="enable-the-cdn-in-your-office-365-tenant"></a>Включение сети доставки содержимого (CDN) в клиенте Office 365
Теперь необходимо разместить расширение в среде внешнего размещения. Сеть доставки содержимого Office 365 — самый простой способ размещать решения SharePoint непосредственно из их клиента, пользуясь при этом преимуществами службы сетей доставки содержимого (CDN) для сокращения времени загрузки ресурсов.

1. Скачайте [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588), чтобы убедиться, что у вас установлена последняя версия.

2. Подключитесь к клиенту SharePoint Online с помощью PowerShell:
    
    ```
    Connect-SPOService -Url https://[tenant]-admin.sharepoint.com
    ```
    
3. Чтобы узнать текущее состояние настроек общедоступной сети CDN для клиента, поочередно выполните указанные ниже команды. 
    
    ```
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. Включите общедоступную сеть доставки содержимого в клиенте:
    
    ```
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    Теперь в клиенте включена общедоступная сеть доставки содержимого с использованием разрешенной конфигурации типов файлов по умолчанию. Это означает, что поддерживаются такие расширения: CSS, EOT, CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF.

5. Откройте браузер и перейдите к семейству веб-сайтов, в котором вы хотите разместить свою библиотеку CDN. Это может быть любое семейство веб-сайтов в клиенте. Это руководство описывает создание библиотеки CDN, но вы также можете использовать отдельную папку в любой существующей библиотеке документов как конечную точку CDN.

6. В семействе веб-сайтов создайте библиотеку документов _CDN_ и добавьте в нее папку _customfooter_.
    
7. В консоли PowerShell добавьте новый источник сети доставки содержимого. В этом случае мы задаем источник `*/cdn`, то есть в качестве источника сети доставки содержимого (CDN) будет выступать любая относительная папка с именем _cdn_.
    
    ```
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. Выполните следующую команду, чтобы получить список источников сетей CDN из клиента:
    
    ```
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
Обратите внимание, что новый источник указан как допустимый источник сети доставки содержимого. Настройка источника займет некоторое время (приблизительно 15 минут), поэтому мы пока можем подготовить к работе расширение, которое будет размещено в источнике по завершении развертывания. 

![Список общедоступных источников в клиенте](../../../images/ext-app-cdn-origins-pending.png)

Если рядом с названием источника нет уведомления `(configuration pending)`, он готов к использованию в клиенте. Это указывает на выполняющуюся настройку SharePoint Online и системы CDN. 

#### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a>Обновление параметров решения и его публикация в сети доставки содержимого
Теперь необходимо обновить решение для использования только что созданной сети CDN в качестве среды внешнего размещения и опубликовать в ней пакет решения. Чтобы выполнить эту задачу, выполните указанные ниже действия.

1. Вернитесь к ранее созданному решению, чтобы внести необходимые изменения в URL-адреса.
    
2. Обновите файл _write-manifestests.json_ (в папке _config_), как показано ниже, чтобы он указывал на конечную точку CDN. Используйте префикс `publiccdn.sharepointonline.com`, а затем дополните URL-адрес фактическим путем к вашему клиенту. Формат URL-адреса для сети доставки содержимого:
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Обновленный манифест записи с путем к конечной точке CDN](../../../images/spfx-react-custom-footer-write-manifest.png)

3. Сохраните изменения.

4. Выполните описанную ниже задачу для упаковки решения. При этом будет выполнена сборка конечной версии проекта с использованием URL-адреса CDN, указанного в файле _writer-manifest.json_. Результат будет помещен в папку _./temp/deploy_. Эти файлы вам нужно будет добавить в папку SharePoint, представляющую собой конечную точку CDN. 
    
    ```
    gulp bundle --ship
    ```
    
5. Выполните приведенную ниже задачу, чтобы упаковать решение. Эта команда создаст пакет _spfx-react-custom-footer.sppkg_ в папке _sharepoint/solution_, а также подготовит ресурсы в папке _temp/deploy_ к развертыванию в CDN.
    
    ```
    gulp package-solution --ship
    ```
    
6. Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте, а затем нажмите кнопку _Развернуть_.

    ![Диалоговое окно доверия в каталоге приложений с путем к конечной точке CDN](../../../images/spfx-react-custom-footer-cdn-address.png)

7. Отправьте или перетащите файлы из папки _temp/deploy_ в созданную ранее папку _CDN/customfooter_.

### <a name="install-and-run-the-solution"></a>Установка и запуск решения
<a name="InstallApplicationCustomizer"> </a> Теперь вы можете установить решения на любом целевом "современном" сайте.

1. Откройте браузер и перейдите на любой "современный" сайт.

2. Перейдите на страницу _Контент сайта_ и добавьте новое _приложение_.

3. Установите новое приложение _из вашей организации_, чтобы просмотреть решения, доступные в _каталоге приложений_.

4. Выберите решение _spfx-react-custom-footer-client-side-solution_ и установите его на целевом сайте.

    ![Добавление пользовательского интерфейса приложения для добавления решения на сайт](../../../images/spfx-react-custom-footer-add-app.png)

5. По завершении установки приложения обновите страницу или перейдите на домашнюю страницу сайта. Вы сможете увидеть пользовательский нижний колонтитул в действии.

Поздравляем! Вы создали пользовательский нижний колонтитул с помощью расширений SharePoint Framework.
