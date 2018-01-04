---
title: "Учебник: переход с JSLink на расширения SharePoint Framework"
ms.date: 12/19/2017
ms.prod: sharepoint
ms.openlocfilehash: 85e6801645da5cc1de0d49505a35b5fa8b68b820
ms.sourcegitcommit: bf4bc1e80c6ef1a0ff479039ef9ae0ee84d5f6b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="migrating-from-jslink-to-sharepoint-framework-extensions"></a>Переход с JSLink на расширения SharePoint Framework

После выпуска Microsoft SharePoint 2013 в большинстве корпоративных решений, основанных на Office 365 и SharePoint Online, для настройки полей использовалось свойство _JSLink_ полей и представлений списков. Однако на данный момент, с появлением "современного" пользовательского интерфейса SharePoint Online, большинство таких модификаций недоступно. К счастью, с помощью новых расширений SharePoint Framework вы можете реализовать практически идентичные функции в "современном" пользовательском интерфейсе. Из данного руководства вы узнаете, как перейти от старых ("классических") модификаций к новой модели, основанной на расширениях SharePoint Framework.

## <a name="understanding-sharepoint-framework-extensions"></a>Общие сведения о расширениях SharePoint Framework

Для начала рассмотрим доступные разработчикам варианты расширений SharePoint Framework:

* **Настройщик приложений**. Расширьте встроенный "современный" пользовательский интерфейс SharePoint Online, добавив пользовательские элементы HTML и клиентский код в заранее определенные заполнители на "современных" страницах. На момент написания этой статьи заполнители доступны в верхнем и нижнем колонтитулах каждой "современной" страницы.
* **Набор команд**. Позволяет добавлять пользовательские пункты меню ECB и настраиваемые кнопки на панель команд или в представление списка или библиотеки. С этими командами можно связать любое действие JavaScript (TypeScript).
* **Настройщик полей**. Настройте отображение поля в представлении списка, используя настраиваемые элементы HTML и клиентский код.

Как вы могли понять из приведенных выше описаний, в нашем случае наиболее удобным вариантом будет расширение "Настройщик полей".

> [!NOTE]
> Дополнительные сведения о расширениях SharePoint Framework см. в статье ["Обзор расширений SharePoint Framework"]((https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/extensions/overview-extensions)).

## <a name="migrating-a-jslink-to-an-spfx-field-customizer"></a>Переход с JSLink на настройщик полей SPFx

Предположим, используется среда SharePoint Online, в которой есть настраиваемый список с настраиваемым полем Color, относящимся к типу _Choice_ и принимающим следующие значения: _Red_, _Green_, _Blue_, _Yellow_. Допустим, что у вас есть пользовательское значение для свойства _JSLink_ веб-части, отображающей представление настраиваемого списка. Ниже представлен фрагмент кода JavaScript, на который ссылается свойство _JSLink_ (_customColorRendering.js_).

```JavaScript
// Define a namespace for the custom rendering code
var customJSLinkRendering = customJSLinkRendering || {}; 

// Define a function that declare the custom rendering rules for the target list view
customJSLinkRendering.CustomizeFieldRendering = function () {  

    // Define a custom object to configure the rendering template overrides
    var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = 
    { 
        // Declare the custom rendering function for the 'View' of field 'Color'
        'Color': 
        { 
            'View': customJSLinkRendering.RenderColorField 
        } 
    }; 

    // Register the custom rendering template
    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride); 
}; 

// Declare the custom rendering function for the 'View' of field 'Color'
customJSLinkRendering.RenderColorField = function (context)  
{ 
    var colorField = context.CurrentItem.Color; 

    // Declare a local variable to hold the output color
    var color = '';

    // Evaluate the values of the 'Color' field and render it accordingly
    switch (colorField)
    {
        case 'Red':
            color = 'red';
            break;
        case 'Green':
            color = 'green';
            break;
        case 'Blue':
            color = 'blue';
            break;
        case 'Yellow':
            color = 'yellow';
            break;
        default:
            color = 'white';
            break;
    }

    // Render the output for the 'Color' field
    return "<div style='float: left; width: 20px; height: 20px; margin: 5px; border: 1px solid rgba(0,0,0,.2);background:" + color + "' />"; 
}; 

// Invoke the custom rendering function
customJSLinkRendering.CustomizeFieldRendering();
```

Кроме того, на приведенном ниже снимке экрана показано, как настраивается JSLink в веб-части представления списка.

![Настройка свойства JSLink в веб-части представления списка](../../../images/jslink-field-configuration.png)

Если вы отправили файл JavaScript в библиотеку _"Активы сайта"_, то для свойства _JSLink_ может быть задано значение _"~site/SiteAssets/customColorRendering.js"_.
А здесь, для полноты картины, показано, как работает настраиваемая отрисовка списка.

![Настраиваемая отрисовка поля Color настраиваемого списка](../../../images/jslink-field-output.png)

Как видите, в полях Color отображается квадрат, заполненный цветом, выбранным на уровне элемента.

> [!NOTE]
> Чтобы подготовить такое решение на "классическом сайте", можно воспользоваться шаблоном подготовки PnP, который может одновременно подготовить список с настраиваемым полем и JSLink.

Чтобы перенести представленное выше решение на платформу SharePoint Framework, необходимо выполнить указанные ниже действия.

### <a name="create-a-new-sharepoint-framework-solution"></a>Создание решения SharePoint Framework

 Подготовив среду разработки к созданию решений SharePoint Framework, вы можете приступить к созданию расширения SharePoint Framework, выполнив действия, описанные в статье ["Как настроить среду разработки клиентских веб-частей SharePoint"]((https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/set-up-your-development-environment)).

1. Откройте любое средство командной строки (PowerShell, CMD.EXE, Cmder и т. д.), создайте папку для решения (назовите ее _spfx-custom-field-extension_) и создайте решение SharePoint Framework, запустив генератор Yeoman с помощью следующей команды:

```
yo @microsoft/sharepoint
```

При появлении соответствующих запросов укажите следующие параметры:
* Оставьте имя решения по умолчанию (_spfx-custom-field-extension_) и нажмите клавишу ВВОД.
* Выберите SharePoint Online only (latest) (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.
* Выберите Use the current folder (Использовать текущую папку) и нажмите клавишу ВВОД.
* Выберите N, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.
* Выберите Extension (Расширение) в качестве типа создаваемого клиентского компонента.
* Выберите для создаваемого расширения тип _"Настройщик полей"_.
* Укажите для настройщика полей имя "CustomColorField".
* Чтобы не использовать конкретную платформу JavaScript, выберите параметр _No JavaScript framework_ (Без платформы JavaScript).

![Пользовательский интерфейс генератора Yeoman при создании решения для пользовательского нижнего колонтитула](../../../images/spfx-custom-field-extension-yeoman.png)

На этом этапе Yeoman установит необходимые зависимости и сформирует шаблон файлов и папок решения вместе с расширением _CustomColorField_. Это может занять несколько минут.

После успешного формирования шаблона должно появиться следующее сообщение:

![Формирование шаблона завершено](../../../images/spfx-custom-field-extension-yeoman-completed.png)

2. Чтобы заблокировать версию зависимостей проекта, выполните следующую команду:

```
npm shrinkwrap
```

3. Теперь запустите Visual Studio Code (или другой редактор кода) и начните разработку решения. Чтобы запустить Visual Studio Code, можно выполнить приведенный ниже оператор.

```
code .
```

### <a name="define-the-new-field-customizer-with-javascript"></a>Определение нового настройщика полей с помощью JavaScript

 Чтобы воспроизвести такое поведение отрисовки настраиваемого поля _JSLink_, достаточно реализовать такую же логику с помощью клиентского кода в новом решении SharePoint Framework. Чтобы выполнить эту задачу, сделайте следующее:

1. Для начала откройте файл _CustomColorFieldFieldCustomizer.manifest.json_ в папке _src/extensions/customColorField_. Скопируйте значение свойства _id_ и сохраните его в надежном месте, так как оно потребуется позже.

2. Теперь откройте файл _CustomColorFieldFieldCustomizer.ts_ в той же папке и измените его содержимое в соответствии с приведенным ниже фрагментом кода.

``` TypeScript
import { Log } from '@microsoft/sp-core-library';
import { override } from '@microsoft/decorators';
import {
  BaseFieldCustomizer,
  IFieldCustomizerCellEventParameters
} from '@microsoft/sp-listview-extensibility';

import * as strings from 'CustomColorFieldFieldCustomizerStrings';
import styles from './CustomColorFieldFieldCustomizer.module.scss';

/**
 * If your field customizer uses the ClientSideComponentProperties JSON input,
 * it will be deserialized into the BaseExtension.properties object.
 * You can define an interface to describe it.
 */
export interface ICustomColorFieldFieldCustomizerProperties {
  // This is an example; replace with your own property
  sampleText?: string;
}

const LOG_SOURCE: string = 'CustomColorFieldFieldCustomizer';

export default class CustomColorFieldFieldCustomizer
  extends BaseFieldCustomizer<ICustomColorFieldFieldCustomizerProperties> {

  @override
  public onInit(): Promise<void> {
    // Add your custom initialization to this method.  The framework will wait
    // for the returned promise to resolve before firing any BaseFieldCustomizer events.
    Log.info(LOG_SOURCE, 'Activated CustomColorFieldFieldCustomizer with properties:');
    Log.info(LOG_SOURCE, JSON.stringify(this.properties, undefined, 2));
    Log.info(LOG_SOURCE, `The following string should be equal: "CustomColorFieldFieldCustomizer" and "${strings.Title}"`);
    return Promise.resolve();
  }

  @override
  public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

    var colorField = event.fieldValue; 
    
    // Declare a local variable to hold the output color
    var color = '';

    // Evaluate the values of the 'Color' field and render it accordingly
    switch (colorField)
    {
        case 'Red':
            color = 'red';
            break;
        case 'Green':
            color = 'green';
            break;
        case 'Blue':
            color = 'blue';
            break;
        case 'Yellow':
            color = 'yellow';
            break;
        default:
            color = 'white';
            break;
    }
    
    // Render the output for the 'Color' field
    event.domElement.innerHTML = "<div style='float: left; width: 20px; height: 20px; margin: 5px; border: 1px solid rgba(0,0,0,.2);background:" + color + "' />"; 
  }

  @override
  public onDisposeCell(event: IFieldCustomizerCellEventParameters): void {
    // This method should be used to free any resources that were allocated during rendering.
    // For example, if your onRenderCell() called ReactDOM.render(), then you should
    // call ReactDOM.unmountComponentAtNode() here.
    super.onDisposeCell(event);
  }
}
```

Как видите, содержимое метода _onRenderCell_ практически такое же, как у метода _RenderColorField_ в реализации _JSLink_.
Единственные отличия:
- чтобы получить текущее значение поля, необходимо считать свойство _event.fieldValue_ входного аргумента метода _onRenderCell_;
- чтобы вернуть настраиваемый HTML-код для отрисовки поля, необходимо назначить значение свойству _innerHTML_ объекта _event.domElement_, представляющему выходной контейнер HTML для отрисовки поля.

Если не считать этих незначительных изменений, вы можете использовать практически такой же код JavaScript, как прежде.

На приведенном ниже рисунке показаны выходные данные.

![Настройщик полей в "современном" списке](../../../images/spfx-custom-field-extension-output.png)

### <a name="test-the-solution-in-debug-mode"></a>Тестирование решения в режиме отладки

Теперь все готово к тестированию решения в режиме отладки. 

1. Вернитесь к окну консоли и выполните следующую команду:

```
gulp serve --nobrowser
```

Приведенная выше команда выполняет сборку решения и запускает локальный сервер Node.js для его размещения.

2. Теперь откройте любой браузер и перейдите к "современному" списку, содержащему настраиваемое поле с именем _Color_, и введите _Choice_ с теми же вариантами значений, что и раньше (Red, Green, Blue, Yellow). Впоследствии вы можете использовать список, созданный на "классическом" сайте, просматривая его в "современном" интерфейсе. Затем добавьте приведенные ниже параметры строки запроса к URL-адресу страницы _AllItems.aspx_.

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Color":{"id":"c3070978-d85e-4298-8758-70b5b5933076"}}
```

В приведенной ниже строке запроса потребуется заменить GUID на сохраненное ранее значение _id_ из файла _CustomColorFieldFieldCustomizer.manifest.json_. Имя объекта _Color_ указывает на поле, которое требуется настроить. При желании вы также можете передать настраиваемый объект конфигурации, сериализованный в формате JSON, в качестве дополнительного параметра при конструировании настройщика полей.

Обратите внимание, что при выполнении запроса страницы появится окно с предупреждающим сообщением "Разрешить скрипты отладки?", где из соображений безопасности спрашивается ваше согласие на запуск кода с localhost. Конечно, если вы хотите отладить и протестировать решение локально, потребуется разрешить загрузку скриптов отладки.

### <a name="define-the-new-field-customizer-with-typescript"></a>Определение нового настройщика полей с помощью TypeScript

Теперь вы можете заменить код JavaScript на TypeScript, чтобы воспользоваться преимуществами полностью типизированного подхода, реализованного в TypeScript.

1. Откройте файл _CustomColorFieldFieldCustomizer.module.scss_ в папке _src/extensions/customColorField_. Это файл Sassy CSS, представляющий стиль пользовательского интерфейса настройщика полей. Замените содержимое файла SCSS на приведенный ниже код.

``` SCSS
.CustomColorField {
  .cell {
    float: left;
    width: 20px; 
    height: 20px; 
    margin: 5px; 
    border: 1px solid rgba(0,0,0,.2);
  }

  .cellRed {
    background: red;
  }

  .cellGreen {
    background: green;
  }

  .cellBlue {
    background: blue;
  }

  .cellYellow {
    background: yellow;
  }

  .cellWhite {
    background: white;
  }
}
```

2. Замените реализацию метода _onRenderCell_ на приведенный ниже фрагмент кода.

``` TypeScript
@override
public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

// Read the current field value
let colorField: String = event.fieldValue; 

// Add the main style to the field container element
event.domElement.classList.add(styles.CustomColorField);

// Get a reference to the output HTML
let fieldHtml: HTMLDivElement = event.domElement.firstChild as HTMLDivElement;

// Add the standard style
fieldHtml.classList.add(styles.cell);

// Add the colored style
switch(colorField)
{
    case "Red":
    fieldHtml.classList.add(styles.cellRed);
    break;
    case "Green":
    fieldHtml.classList.add(styles.cellGreen);
    break;
    case "Blue":
    fieldHtml.classList.add(styles.cellBlue);
    break;
    case "Yellow":
    fieldHtml.classList.add(styles.cellYellow);
    break;
    default:
    fieldHtml.classList.add(styles.cellWhite);
    break;
}
}
```

Обратите внимание, что в новой реализации метода используется полностью типизированный подход, а класс CSS _cell_ назначается дочернему элементу _DIV_ текущего элемента поля вместе с другим пользовательским классом CSS, чтобы определить целевой цвет элемента _DIV_ в соответствии с выбранным значением поля.

3. Еще раз запустите настройщик полей в режиме отладки и ознакомьтесь с результатом.

### <a name="package-and-host-the-solution"></a>Упаковка и размещение решения

Если вы довольны результатом, теперь можно упаковать решение и разместить его в настоящей инфраструктуре.
Прежде чем собирать пакет, необходимо объявить XML-файл платформы функций для подготовки расширения.

#### <a name="review-feature-framework-elements"></a>Обзор элементов платформы функций
В редакторе кода откройте вложенную папку _/sharepoint/assets_ в папке решения и измените файл _elements.xml_.
В приведенном ниже фрагменте кода показано, как должен выглядеть файл.

```XML
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Field ID="{40475661-efaf-447a-a220-c992b20ec1c3}"
            Name="SPFxColor"
            DisplayName="Color"
            Title="Color"
            Type="Choice"
            Required="FALSE"
            Group="SPFx Columns"
            ClientSideComponentId="c3070978-d85e-4298-8758-70b5b5933076">
    </Field>
</Elements>
```

Как видите, он напоминает файл платформы функций SharePoint. В нем определяется настраиваемый элемент _Field_ типа _Choice_, с помощью атрибута _ClientSideComponentId_ ссылающийся на свойство _id_ настройщика полей. Кроме того, может быть задан атрибут _ClientSideComponentProperties_ для установки настраиваемых свойств конфигурации, необходимых расширению.

Теперь откройте файл _package-solution.json_ в папке _/config_ решения. В файле вы увидите ссылку на файл _elements.xml_ в разделе _assets_.

```JSON
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "spfx-custom-field-extension-client-side-solution",
    "id": "ab0fbbf8-01ba-4633-8498-46cfd5652619",
    "version": "1.0.0.0",
    "features": [
      {
        "title": "Application Extension - Deployment of custom action.",
        "description": "Deploys a custom action with ClientSideComponentId association",
        "id": "090dc976-878d-44fe-8f8e-ac603d094aa1",
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
    "zippedPackage": "solution/spfx-custom-field-extension.sppkg"
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

6. В семействе веб-сайтов создайте библиотеку документов _CDN_ и добавьте в нее папку _customcolorfield_.
    
7. В консоли PowerShell добавьте новый источник сети доставки содержимого. В этом случае мы задаем источник `*/cdn`, то есть в качестве источника сети доставки содержимого (CDN) будет выступать любая относительная папка с именем _cdn_.
    
    ```
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. Выполните указанную ниже команду, чтобы получить список источников сети доставки содержимого клиента:
    
    ```
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
Обратите внимание, что новый источник указан как допустимый источник сети доставки содержимого. Настройка источника займет некоторое время (приблизительно 15 минут), поэтому мы пока можем подготовить к работе расширение, которое будет размещено в источнике по завершении развертывания. 

![Список общедоступных источников в клиенте](../../../images/ext-app-cdn-origins-pending.png)

Если рядом с названием источника нет уведомления `(configuration pending)`, он готов к использованию в клиенте. Это указывает на выполняющуюся настройку SharePoint Online и системы CDN. 

#### <a name="update-the-solution-settings-and-publish-it-on-the-cdn"></a>Обновление параметров решения и его публикация в сети доставки содержимого

Теперь необходимо обновить решение для использования только что созданной сети CDN в качестве среды внешнего размещения и опубликовать в ней пакет решения. Чтобы выполнить эту задачу, выполните указанные ниже действия.

1. Вернитесь к ранее созданному решению, чтобы внести необходимые изменения в URL-адреса.
    
2. Обновите файл _write-manifestests.json_ (в папке _config_), как показано ниже, чтобы он указывал на конечную точку CDN. Используйте `publiccdn.sharepointonline.com` в качестве префикса, а затем дополните URL-адрес фактическим путем к вашему клиенту. Формат URL-адреса для сети доставки содержимого:
    
    ```
    https://publiccdn.sharepointonline.com/[tenant host name]/sites/[site]/[library]/[folder]
    ```
    
    ![Путь к конечной точке CDN в манифесте записи](../../../images/spfx-custom-field-extension-manifest.png)

3. Сохраните изменения.

4. Выполните описанную ниже задачу для упаковки решения. При этом будет выполнена сборка конечной версии проекта с использованием URL-адреса CDN, указанного в файле _writer-manifest.json_. Результат будет помещен в папку _./temp/deploy_. Эти файлы вам нужно будет добавить в папку SharePoint, представляющую собой конечную точку CDN. 
    
    ```
    gulp bundle --ship
    ```
    
5. Выполните приведенную ниже задачу, чтобы упаковать решение. Эта команда создаст пакет _spfx-custom-field-extension.sppkg_ в папке _sharepoint/solution_, а также подготовит ресурсы в папке _temp/deploy_ к развертыванию в CDN.
    
    ```
    gulp package-solution --ship
    ```
    
6. Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте, а затем нажмите кнопку _Развернуть_.

    ![Диалоговое окно доверия в каталоге приложений с путем к конечной точке CDN](../../../images/spfx-custom-field-extension-address.png)

7. Отправьте или перетащите файлы из папки _temp/deploy_ в созданную ранее папку _CDN/customcolorfield_.

### <a name="install-and-run-the-solution"></a>Установка и запуск решения

Теперь вы можете установить решения на любом целевом "современном" сайте.

1. Откройте браузер и перейдите на любой "современный" сайт.

2. Перейдите на страницу _Контент сайта_ и добавьте новое _приложение_.

3. Установите новое приложение _из вашей организации_, чтобы просмотреть решения, доступные в _каталоге приложений_.

4. Выберите решение _spfx-custom-field-extension-client-side-solution_ и установите его на целевом сайте.

    ![Добавление пользовательского интерфейса приложения для добавления решения на сайт](../../../images/spfx-custom-field-extension-add-app.png)

5. По завершении установки приложения создайте настраиваемый список, измените его свойства и добавьте новый столбец на основе имеющихся столбцов. Выберите группу столбцов под названием _"Столбцы SPFx"_ и добавьте поле _Color_.

![Настройщик полей в действии](../../../images/spfx-custom-field-extension-add-field.png)

6. Измените добавленное поле и настройте значения цветов (например, "Красный", "Зеленый", "Синий", "Желтый"), а затем сохраните параметры поля.

7. Добавьте в список элементы и просмотрите выходные данные в представлении списка. Они должны выглядеть так, как на приведенном ниже снимке экрана.

![Настройщик полей в действии](../../../images/spfx-custom-field-extension-final-output.png)

Поздравляем! Вы создали настройщик полей с помощью расширений SharePoint Framework.
