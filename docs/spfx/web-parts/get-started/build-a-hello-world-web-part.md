---
title: "Создание первой клиентской веб-части SharePoint (Hello World, часть 1)"
ms.date: 12/05/2017
ms.prod: sharepoint
ms.openlocfilehash: 9a5fefeb0e5dac79958534dd4819a905ff608635
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="build-your-first-sharepoint-client-side-web-part-hello-world-part-1"></a>Создание первой клиентской веб-части SharePoint (Hello World, часть 1)

Клиентские веб-части — это клиентские компоненты, которые запускаются в контексте страницы SharePoint. Клиентские веб-части можно развертывать в SharePoint Online, а для их создания также можно использовать современные инструменты и библиотеки JavaScript.

Поддержка клиентских веб-частей:

* Создание при помощи HTML и JavaScript.
* Как SharePoint Online, так и локальные среды.

> [!NOTE]
> Прежде чем выполнять действия, описанные в этой статье, обязательно [настройте среду разработки](../../set-up-your-development-environment.md).

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=YqUIX2pMUzg&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=2). 

<a href="https://www.youtube.com/watch?v=YqUIX2pMUzg&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=2">
<img src="../../../images/spfx-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a>Создание проекта веб-части
Создайте каталог проекта в любом расположении.
    
```
md helloworld-webpart
```

Перейдите к каталогу проекта.

```
cd helloworld-webpart
```

Создайте веб-часть HelloWorld, запустив генератор Yeoman для SharePoint.

```
yo @microsoft/sharepoint
```
    
Когда появится запрос:

* Оставьте имя по умолчанию (**helloworld-webpart**) для своего решения и нажмите клавишу **ВВОД**.
* Выберите **Только SharePoint Online (новая версия)** и нажмите клавишу **ВВОД**.
* Выберите вариант **Использовать текущую папку** для размещения файлов.
* Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании. 
* Выберите **WebPart** в качестве типа создаваемого клиентского компонента. 

Далее вам потребуется указать определенные сведения о веб-части:

* Оставьте имя по умолчанию (**HelloWorld**) для своей веб-части и нажмите клавишу **ВВОД**.
* Оставьте **описание HelloWorld** по умолчанию для своей веб-части и нажмите клавишу **ВВОД**.
* Оставьте выбранным параметр **No javascript web framework** (Не использовать платформу веб-решений на базе JavaScript) по умолчанию и нажмите клавишу **ВВОД**.

![Генератор Yeoman для SharePoint предлагает создать клиентскую веб-часть](../../../images/yeoman-sp-prompts.png)

После этого Yeoman установит необходимые зависимости и выполнит скаффолдинг файлов решения, а также веб-части **HelloWorld**. Это может занять несколько минут.

Когда скаффолдинг успешно закончится, появится следующее сообщение:

!["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../images/yeoman-sp-complete.png)

Сведения об устранении неполадок см. в статье [Известные проблемы](../../known-issues-and-common-questions.md).

### <a name="using-your-favorite-code-editor"></a>Использование удобного редактора кода
Так как клиентские решения SharePoint созданы с помощью HTML и TypeScript, для разработки веб-части можно использовать любой редактор кода, который поддерживает клиентское программирование, например:

* [Visual Studio Code](https://code.visualstudio.com/);
* [Atom](https://atom.io);
* [Webstorm](https://www.jetbrains.com/webstorm).

В примерах и инструкциях, приведенных в документации по SharePoint Framework, указывается Visual Studio Code. Visual Studio Code — мощный редактор исходного кода, предложенный корпорацией Майкрософт, который занимает мало места на диске и работает на компьютерах с Windows, Mac OS или Linux. Он изначально поддерживает JavaScript, TypeScript и Node.js, а также предусматривает использование богатой экосистемы расширений для других языков (например, C++, C#, Python, PHP) и сред выполнения.
   
## <a name="preview-the-web-part"></a>Просмотр веб-части
Чтобы просмотреть веб-часть, выполните сборку и запустите ее на локальном веб-сервере. В клиентской цепочке инструментов по умолчанию используется конечная точка HTTPS. Но так как сертификат по умолчанию не настроен для локальной среды разработки, браузер сообщит об ошибке сертификата. Цепочка инструментов SPFx включает сертификат разработчика, который можно установить для создания веб-частей.

Чтобы установить сертификат разработчика для использования SPFx, перейдите в консоль, откройте каталог **helloworld-webpart** и введите следующую команду:

```
gulp trust-dev-cert
```

Теперь, когда вы установили сертификат разработчика, введите в консоли следующую команду для сборки и просмотра веб-части:

```
gulp serve
```

Эта команда выполнит ряд задач Gulp, чтобы создать локальный HTTPS-сервер на основе Node по адресу localhost:4321, и запустит браузер по умолчанию для просмотра веб-частей в локальной среде разработки.

![Проект веб-части gulp serve](../../../images/helloworld-wp-gulp-serve.png)

Инструменты клиентской разработки SharePoint используют [Gulp](http://gulpjs.com/) как средство запуска задач для таких задач по сборке, как:

* добавление в пакет и минификация файлов JavaScript и CSS;
* запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;
* компиляция файлов SASS в CSS;
* компиляция файлов TypeScript в JavaScript.

Visual Studio Code поддерживает Gulp и другие средства запуска задач. Нажмите клавиши **CTRL+SHIFT+B** в Windows или **CMD+SHIFT+B** в Mac OS для отладки и просмотра веб-части. 

### <a name="sharepoint-workbench"></a>SharePoint Workbench
SharePoint Workbench — это рабочая область конструирования для разработчиков, которая позволяет быстро просматривать и проверять веб-части, не развертывая их в SharePoint. SharePoint Workbench включает клиентскую страницу и клиентский холст, на которых можно добавлять, удалять и проверять веб-части, которые находятся в разработке.

![Рабочая область SharePoint Workbench, запущенная локально](../../../images/sp-workbench.png)

Чтобы добавить веб-часть HelloWorld, нажмите кнопку **Добавить**. Эта кнопка открывает панель элементов со списком веб-частей, которые можно добавить. Список будет включать веб-часть **HelloWorld**, а также другие веб-части, доступные локально в среде разработки.
   
![Панель элементов SharePoint Workbench на localhost](../../../images/sp-workbench-toolbox.png)
   
Выберите пункт **HelloWorld**, чтобы добавить эту веб-часть на страницу:
   
![Веб-часть HelloWorld в SharePoint Workbench](../../../images/sp-workbench-helloworld-wp.png)

**Поздравляем!** Вы только что добавили свою первую клиентскую веб-часть на клиентскую страницу.
   
Теперь выберите значок карандаша в крайнем левом углу веб-части, чтобы открыть панель свойств веб-части.
   
![Панель свойств веб-части HelloWorld](../../../images/sp-workbench-helloworld-pp.png)

На панели свойств можно задавать свойства для настройки веб-части. Панель свойств запускается на стороне клиента и имеет одинаковый дизайн для всех веб-частей SharePoint.
   
Измените текст в поле **Описание** на текст **Клиентские веб-части — это великолепно!**

Обратите внимание, что при вводе текст в веб-части также меняется. 

Теперь вы можете настроить режим обновления для панели свойств, выбрав реактивный или нереактивный вариант. В режиме по умолчанию (реактивном) изменения становятся видны по мере редактирования свойств и сохраняются мгновенно.  

## <a name="web-part-project-structure"></a>Структура проекта веб-части
С помощью Visual Studio Code можно просмотреть структуру проекта веб-части. 

* Перейдите на консоль и остановите обработку, нажав клавиши CTRL+C (в Windows). 
* Введите указанную ниже команду, чтобы открыть проект веб-части в Visual Studio Code (или используйте другой редактор):

```
code .
```

![Структура проекта HelloWorld](../../../images/helloworld-wp-vscode-project-structure.png)

Если возникла ошибка, [задайте команду code в PATH](https://code.visualstudio.com/docs/editor/setup).

TypeScript — это основной язык для создания клиентских веб-частей SharePoint. TypeScript — это типизированная расширенная версия языка JavaScript. Код TypeScript компилируется в обычный JavaScript. Клиентские средства разработки SharePoint основаны на классах, модулях и интерфейсах TypeScript, что позволяет разработчикам создавать надежные клиентские веб-части. 

Ниже приведены некоторые ключевые файлы в проекте.

### <a name="web-part-class"></a>Класс веб-части
**HelloWorldWebPart.ts** в папке **src\webparts\helloworld** определяет основную точку входа для веб-части. Класс веб-части **HelloWorldWebPart** расширяет класс **BaseClientSideWebPart**. Чтобы клиентская веб-часть была допустимой, она должна расширять класс **BaseClientSideWebPart**.

Этот класс обеспечивает минимальную функциональность, необходимую для создания веб-части. Он также предоставляет много параметров для проверки и доступа к свойствам только для чтения, например **displayMode**, другим свойствам веб-частей, контексту веб-частей, а также **instanceId** и **domElement**.

Обратите внимание на то, что класс веб-части определяется как принимающий тип свойства **IHelloWorldWebPartProps**.

Тип свойства определяется как интерфейс перед классом **HelloWorldWebPart** в файле **HelloWorldWebPart.ts**.

```ts
export interface IHelloWorldWebPartProps {
    description: string;
}
```

Это определение свойства используется для определения типов настраиваемых свойств для веб-части. Дополнительные сведения см. в разделе, посвященном области свойств, ниже. 

#### <a name="web-part-render-method"></a>Метод отрисовки веб-части
Элемент DOM, в котором должна отрисовываться веб-часть, доступен в методе **render**. Этот метод используется для отрисовки веб-части в этом элементе DOM. В веб-части **HelloWorld** элемент DOM присвоен переменной DIV. Параметры метода включают режим отображения (чтение или редактирование) и настроенные свойства веб-части, если они есть: 

```ts
  public render(): void {
    this.domElement.innerHTML = `
      <div class="${ styles.helloWorld }">
        <div class="${ styles.container }">
          <div class="${ styles.row }">
            <div class="${ styles.column }">
              <span class="${ styles.title }">Welcome to SharePoint!</span>
              <p class="${ styles.subTitle }">Customize SharePoint experiences using Web Parts.</p>
              <p class="${ styles.description }">${escape(this.properties.description)}</p>
              <a href="https://aka.ms/spfx" class="${ styles.button }">
                <span class="${ styles.label }">Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>`;
  }
```

Эта модель достаточно гибкая — в элемент DOM можно загружать веб-части, созданные на любой платформе JavaScript. 

#### <a name="configure-the-web-part-property-pane"></a>Настройка области свойств веб-части
Область свойств определяется в классе **HelloWorldWebPart**. Панель свойств нужно настраивать в свойстве **propertyPaneSettings**.

Когда свойства заданы, вы можете получить к ним доступ в веб-части, используя `this.properties.<property-value>`, как показано в примере с методом **render**:

```ts
<p class="${styles.description}">${escape(this.properties.description)}</p>
```

Обратите внимание, что мы выполняем управляющий код HTML для значения свойства, чтобы убедиться, что строка является допустимой.

Просмотрите статью об [интеграции панели свойств с веб-частью](../basics/integrate-with-property-pane.md), чтобы узнать больше о работе с панелью свойств и типами полей в ней.

Давайте добавим в область свойств еще флажок, раскрывающийся список и переключатель. Для этого сначала импортируйте из платформы соответствующие поля области свойств.

Перейдите к верхней части файла и добавьте приведенный ниже код в раздел импорта из `@microsoft/sp-webpart-base`.

```ts
PropertyPaneCheckbox,
PropertyPaneDropdown,
PropertyPaneToggle
```

Полный раздел импорта будет выглядеть так:

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField,
  PropertyPaneCheckbox,
  PropertyPaneDropdown,
  PropertyPaneToggle
} from '@microsoft/sp-webpart-base';
```

Далее обновите свойства веб-части, включив новые. При этом будут сопоставлены соответствующие поля и типизированные объекты.

Замените интерфейс **IHelloWorldWebPartProps** приведенным ниже кодом.

```ts
export interface IHelloWorldWebPartProps {
    description: string;
    test: string;
    test1: boolean;
    test2: string;
    test3: boolean;
}
```

Сохраните файл.

Замените метод **getPropertyPaneConfiguration** приведенным ниже кодом, который добавляет новые поля области свойств и сопоставляет их с соответствующими типизированными объектами.

```ts
protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
  return {
    pages: [
      {
        header: {
          description: strings.PropertyPaneDescription
        },
        groups: [
          {
            groupName: strings.BasicGroupName,
            groupFields: [
            PropertyPaneTextField('description', {
              label: 'Description'
            }),
            PropertyPaneTextField('test', {
              label: 'Multi-line Text Field',
              multiline: true
            }),
            PropertyPaneCheckbox('test1', {
              text: 'Checkbox'
            }),
            PropertyPaneDropdown('test2', {
              label: 'Dropdown',
              options: [
                { key: '1', text: 'One' },
                { key: '2', text: 'Two' },
                { key: '3', text: 'Three' },
                { key: '4', text: 'Four' }
              ]}),
            PropertyPaneToggle('test3', {
              label: 'Toggle',
              onText: 'On',
              offText: 'Off'
            })
          ]
          }
        ]
      }
    ]
  };
}
```


После добавления свойств веб-части к ним можно получить доступ так же, как к свойству **description**:

```ts
<p class="${ styles.description }">${escape(this.properties.test)}</p>
```

Чтобы задать значение по умолчанию для этих свойств, необходимо обновить контейнер свойств **properties** манифеста веб-части.

Откройте `HelloWorldWebPart.manifest.json` и измените `properties` так:

```ts
"properties": {
  "description": "HelloWorld",
  "test": "Multi-line text field",
  "test1": true,
  "test2": "2",
  "test3": true
}
```

Область свойств веб-части будет содержать данные значения по умолчанию для указанных свойств.

### <a name="web-part-manifest"></a>Манифест веб-части
Файл **HelloWorldWebPart.manifest.json** определяет метаданные веб-части, такие как версия, идентификатор, отображаемое имя, значок и описание. Все веб-части должны содержать этот манифест.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "7d5437ee-afc2-4e66-914b-80be5ace4056",
  "alias": "HelloWorldWebPart",
  "componentType": "WebPart",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "preconfiguredEntries": [{
    "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
    "group": { "default": "Other" },
    "title": { "default": "HelloWorld" },
    "description": { "default": "HelloWorld description" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "HelloWorld",
      "test": "Multi-line text field",
      "test1": true,
      "test2": "2",
      "test3": true
    }
  }]
}

```

Теперь, когда мы добавили новые свойства, опять запустите веб-часть из локальной среды разработки, выполнив приведенную ниже команду. Это также обеспечит правильное применение указанных выше изменений.

```
gulp serve
```

### <a name="preview-the-web-part-in-sharepoint"></a>Просмотр веб-части в SharePoint

В SharePoint размещается рабочая область SharePoint Workbench, чтобы вы могли просматривать и проверять локальные веб-части, которые находятся в разработке. Ее основное преимущество состоит в том, что веб-части запускаются в контексте SharePoint, и вы можете работать с данными SharePoint.

Перейдите по такому URL-адресу: "https://your-sharepoint-tenant.sharepoint.com/_layouts/workbench.aspx".

> [!NOTE]
> Если у вас не установлен сертификат разработчика SPFx, рабочая область сообщит вам, что она не загружает сценарии из localhost. Остановите процесс, выполняющийся в данный момент в окне консоли, выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика, а затем запустите команду `gulp serve` еще раз.

![Рабочая область SharePoint Workbench, запущенная на сайте SharePoint Online](../../../images/sp-workbench-o365.png)

Обратите внимание, что рабочая область SharePoint теперь включает панель навигации Office 365. 

Выберите **значок добавления** на холсте, чтобы открыть панель элементов. В панели элементов теперь отображаются веб-части, доступные на сайте с рабочей областью SharePoint, а также веб-часть **HelloWorldWebPart**.

![Панель элементов в рабочей области SharePoint, запущенной на сайте SharePoint Online](../../../images/sp-workbench-o365-toolbox.png)

Добавьте **HelloWorld** из панели элементов. Теперь ваша веб-часть работает на странице в SharePoint.

![Веб-часть HelloWorld в рабочей области SharePoint, запущенной на сайте SharePoint Online](../../../images/sp-workbench-o365-helloworld-wp.png)

> [!NOTE]
> Цвет веб-части зависит от цвета сайта. По умолчанию веб-часть наследует основные цвета с сайта, на котором она размещена, с помощью динамических ссылок на используемые там стили Office UI Fabric Core.

Так как ваша веб-часть по-прежнему находится на этапе разработки и тестирования, ее не нужно упаковывать и развертывать в SharePoint. 

## <a name="next-steps"></a>Дальнейшие действия
Поздравляем с запуском вашей первой веб-части Hello World! Теперь стоит ознакомиться со статьей [Подключение к SharePoint](./connect-to-sharepoint.md). В ней описано, как расширить возможности Hello World, обеспечив взаимодействие с REST API списков SharePoint. Обратите внимание на то, что команда `gulp serve` по-прежнему запущена в окне консоли (или в Visual Studio Code, если вы используете этот редактор). Можете переходить к следующей статье, не останавливая ее.

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!