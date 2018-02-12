---
title: "Создание первой клиентской веб-части SharePoint (Hello World, часть 1)"
description: "Создание и предварительный просмотр проекта веб-части."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 259689c87365b6e1c70686b1cd1108549318f9b0
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
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

### <a name="to-create-a-new-web-part-project"></a>Создание проекта веб-части

1. Создайте каталог проекта в любом расположении.
    
  ```
  md helloworld-webpart
  ```

2. Перейдите к каталогу проекта.

  ```
  cd helloworld-webpart
  ```

3. Создайте веб-часть HelloWorld, запустив генератор Yeoman для SharePoint.

  ```
  yo @microsoft/sharepoint
  ```
    
4. Когда появится запрос, сделайте следующее:

  - Оставьте имя по умолчанию (**helloworld-webpart**) для своего решения и нажмите клавишу ВВОД.
  - Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.
  - Выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.
  - Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании. 
  - Выберите **WebPart** в качестве типа создаваемого клиентского компонента. 

5. Ниже требуется указать информацию о веб-части:

  - Оставьте имя по умолчанию (**HelloWorld**) для своей веб-части и нажмите клавишу ВВОД.
  - Оставьте **описание HelloWorld** по умолчанию для своей веб-части и нажмите клавишу ВВОД.
  - Оставьте выбранным параметр **No javascript web framework** (Не использовать платформу веб-решений на базе JavaScript) и нажмите клавишу ВВОД.

  ![Генератор Yeoman для SharePoint предлагает создать клиентскую веб-часть](../../../images/yeoman-sp-prompts.png)

После этого Yeoman установит необходимые зависимости и сформирует шаблоны файлов решения, а также веб-части **HelloWorld**. Это может занять несколько минут.

После успешного формирования шаблона должно появиться следующее сообщение:

!["Формирование шаблона клиентского решения SharePoint успешно выполнено".](../../../images/yeoman-sp-complete.png)

Сведения об устранении неполадок см. в статье [Известные проблемы](../../known-issues-and-common-questions.md).

### <a name="using-your-favorite-code-editor"></a>Использование удобного редактора кода
Так как клиентские решения SharePoint созданы с помощью HTML и TypeScript, для разработки веб-части можно использовать любой редактор кода, который поддерживает клиентское программирование, например:

- [Visual Studio Code](https://code.visualstudio.com/);
- [Atom](https://atom.io);
- [Webstorm](https://www.jetbrains.com/webstorm).

В примерах и инструкциях, приведенных в документации по SharePoint Framework, используется Visual Studio Code. Visual Studio Code — мощный редактор исходного кода от корпорации Майкрософт, который занимает мало места на диске и работает на компьютерах с Windows, Mac OS и Linux. Он изначально поддерживает JavaScript, TypeScript и Node.js, а также предусматривает использование богатой экосистемы расширений для других языков (например, C++, C#, Python, PHP) и сред выполнения.
   
## <a name="preview-the-web-part"></a>Предварительный просмотр веб-части

Чтобы просмотреть веб-часть, выполните сборку и запустите ее на локальном веб-сервере. В клиентской цепочке инструментов по умолчанию используется конечная точка HTTPS. Но так как сертификат по умолчанию не настроен для локальной среды разработки, браузер сообщит об ошибке сертификата. Цепочка инструментов SPFx включает сертификат разработчика, который можно установить для создания веб-частей.

### <a name="to-install-the-developer-certificate-and-preview-your-web-part"></a>Установка сертификата разработчика и предварительный просмотр веб-части

1. Перейдите в консоль, убедитесь, что по-прежнему выбран каталог **helloworld-webpart**, и введите следующую команду:

  ```
  gulp trust-dev-cert
  ```

2. Теперь, когда вы установили сертификат разработчика, введите в консоли следующую команду для сборки и предварительного просмотра веб-части:

  ```
  gulp serve
  ```

Эта команда выполняет ряд задач Gulp, чтобы создать локальный HTTPS-сервер на основе узлов по адресу `localhost:4321`, и запускает браузер по умолчанию для просмотра веб-частей в локальной среде разработки.

![Проект веб-части gulp serve](../../../images/helloworld-wp-gulp-serve.png)

Инструменты клиентской разработки SharePoint используют [Gulp](http://gulpjs.com/) как средство запуска таких задач по сборке, как:

- объединение и минификация файлов JavaScript и CSS;
- запуск инструментов для вызова задач по объединению и минификации перед каждой сборкой;
- компиляция файлов SASS в CSS;
- компиляция файлов TypeScript в JavaScript.

Visual Studio Code поддерживает Gulp и другие средства запуска задач. Нажмите клавиши CTRL+SHIFT+B в Windows или CMD+SHIFT+B в Mac OS для отладки и просмотра веб-части. 

SharePoint Workbench — это рабочая область конструирования для разработчиков, которая позволяет быстро просматривать и проверять веб-части, не развертывая их в SharePoint. SharePoint Workbench включает клиентскую страницу и клиентский холст, на которых можно добавлять, удалять и проверять веб-части, которые находятся в разработке.

![Рабочая область SharePoint Workbench, запущенная локально](../../../images/sp-workbench.png)

### <a name="to-use-sharepoint-workbench-to-preview-and-test-your-web-part"></a>Предварительный просмотр и тестирование веб-части с помощью SharePoint Workbench

1. Чтобы добавить веб-часть HelloWorld, нажмите значок **Добавить**. Откроется панель элементов со списком веб-частей, которые можно добавить. Список включает веб-часть **HelloWorld**, а также другие веб-части, доступные локально в среде разработки.
   
  ![Панель элементов SharePoint Workbench по адресу localhost](../../../images/sp-workbench-toolbox.png)
   
2. Выберите пункт **HelloWorld**, чтобы добавить эту веб-часть на страницу.
   
  ![Веб-часть HelloWorld в SharePoint Workbench](../../../images/sp-workbench-helloworld-wp.png)

  Поздравляем! Вы только что добавили свою первую клиентскую веб-часть на клиентскую страницу.
   
3. Выберите значок карандаша в крайнем левом углу веб-части, чтобы открыть панель свойств веб-части.
   
  ![Панель свойств веб-части HelloWorld](../../../images/sp-workbench-helloworld-pp.png)

  На панели свойств можно задавать свойства для настройки веб-части. Панель свойств запускается на стороне клиента и имеет одинаковый дизайн для всех веб-частей SharePoint.
   
4. Измените текст в поле **Описание** на текст **Клиентские веб-части — это великолепно!**

  Обратите внимание, что при вводе текст в веб-части также меняется. 

Теперь вы можете настроить режим обновления для панели свойств, выбрав реактивный или нереактивный вариант. В режиме по умолчанию (реактивном) изменения становятся видны по мере редактирования свойств и сохраняются мгновенно.  

## <a name="web-part-project-structure"></a>Структура проекта веб-части

### <a name="to-use-visual-studio-code-to-explore-the-web-part-project-structure"></a>Анализ структуры проекта веб-части с помощью Visual Studio Code 

1. Откройте консоль и остановите обработку, нажав клавиши CTRL+C (в Windows).

2. Введите следующую команду, чтобы открыть проект веб-части в Visual Studio Code (или используйте другой редактор):

  ```
  code .
  ```

  ![Структура проекта HelloWorld](../../../images/helloworld-wp-vscode-project-structure.png)

Если возникла ошибка, [задайте команду code в PATH](https://code.visualstudio.com/docs/editor/setup).

TypeScript — это основной язык для создания клиентских веб-частей SharePoint. TypeScript — это типизированная расширенная версия языка JavaScript. Код TypeScript компилируется в обычный JavaScript. Клиентские средства разработки SharePoint основаны на классах, модулях и интерфейсах TypeScript, что позволяет разработчикам создавать надежные клиентские веб-части. 

Ниже приведены некоторые ключевые файлы в проекте.

### <a name="web-part-class"></a>Класс веб-части

**HelloWorldWebPart.ts** в папке **src\webparts\helloworld** определяет основную точку входа для веб-части. Класс веб-части **HelloWorldWebPart** расширяет класс **BaseClientSideWebPart**. Чтобы клиентская веб-часть была допустимой, она должна расширять класс **BaseClientSideWebPart**.

Класс **BaseClientSideWebPart** обеспечивает минимальную функциональность, необходимую для создания веб-части. Он также предоставляет много параметров для проверки и доступа к свойствам, доступным только для чтения (например, **displayMode**), другим свойствам веб-частей, контексту веб-частей, а также свойствам **instanceId** и **domElement**.

Обратите внимание, что класс веб-части определяется как принимающий свойство типа **IHelloWorldWebPartProps**.

Тип свойства определяется как интерфейс перед классом **HelloWorldWebPart** в файле **HelloWorldWebPart.ts**.

```typescript
export interface IHelloWorldWebPartProps {
    description: string;
}
```

С помощью этого определения свойства задаются типы настраиваемых свойств для веб-части. Дополнительные сведения см. в разделе, посвященном области свойств, ниже. 

#### <a name="web-part-render-method"></a>Метод отрисовки веб-части
Элемент DOM, в котором должна отрисовываться веб-часть, доступен в методе **render**. Этот метод используется для отрисовки веб-части в этом элементе DOM. В веб-части **HelloWorld** элемент DOM присвоен переменной DIV. Параметры метода включают режим отображения (чтение или редактирование) и настроенные свойства веб-части, если они есть: 

```typescript
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

Когда свойства заданы, вы можете получить к ним доступ в веб-части, используя строку `this.properties.<property-value>`, как показано в примере с методом **render**:

```typescript
<p class="${styles.description}">${escape(this.properties.description)}</p>
```

Обратите внимание, что мы выполняем управляющий код HTML для значения свойства, чтобы убедиться, что строка является допустимой. Дополнительные сведения о работе с областью свойств и типами ее полей см. в статье [Сделайте клиентскую веб-часть SharePoint настраиваемой](../basics/integrate-with-property-pane.md). 

Теперь добавим в область еще несколько свойств: флажок, раскрывающийся список и переключатель. Для этого сначала импортируйте из платформы соответствующие поля области свойств.

1. Перейдите к верхней части файла и добавьте приведенный ниже код в раздел импорта из `@microsoft/sp-webpart-base`.

  ```typescript
  PropertyPaneCheckbox,
  PropertyPaneDropdown,
  PropertyPaneToggle
  ```

  Полный раздел импорта выглядит следующим образом:

  ```typescript
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneTextField,
    PropertyPaneCheckbox,
    PropertyPaneDropdown,
    PropertyPaneToggle
  } from '@microsoft/sp-webpart-base';
  ```

2. Обновите свойства веб-части, включив новые. При этом будут сопоставлены соответствующие поля и типизированные объекты.

3. Замените интерфейс **IHelloWorldWebPartProps** на приведенный ниже код.

  ```typescript
  export interface IHelloWorldWebPartProps {
      description: string;
      test: string;
      test1: boolean;
      test2: string;
      test3: boolean;
  }
  ```

4. Сохраните файл.

5. Замените метод **getPropertyPaneConfiguration** указанным ниже кодом, который добавляет новые поля области свойств и сопоставляет их с соответствующими типизированными объектами.

  ```typescript
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

6. После добавления свойств веб-части к ним можно получить доступ так же, как к свойству **description**:

  ```typescript
  <p class="${ styles.description }">${escape(this.properties.test)}</p>
  ```

  Чтобы задать значение по умолчанию для этих свойств, необходимо обновить контейнер свойств **properties** манифеста веб-части.

7. Откройте файл `HelloWorldWebPart.manifest.json` и замените `properties` следующим кодом:

  ```typescript
  "properties": {
    "description": "HelloWorld",
    "test": "Multi-line text field",
    "test1": true,
    "test2": "2",
    "test3": true
  }
  ```

Теперь для указанных свойств области свойств веб-части заданы эти значения по умолчанию.

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

<br/>

Теперь, когда мы добавили новые свойства, убедитесь, что веб-часть размещена в локальной среде разработки, выполнив приведенную ниже команду. Она также проверяет, правильно ли применены указанные выше изменения.

```
gulp serve
```

### <a name="preview-the-web-part-in-sharepoint"></a>Просмотр веб-части в SharePoint

В SharePoint размещается рабочая область SharePoint Workbench, чтобы вы могли просматривать и проверять локальные веб-части, которые находятся в разработке. Ее основное преимущество состоит в том, что веб-части запускаются в контексте SharePoint, и вы можете работать с данными SharePoint.

1. Перейдите по следующему URL-адресу: `https://your-sharepoint-tenant.sharepoint.com/_layouts/workbench.aspx`

  > [!NOTE]
  > Если у вас не установлен сертификат разработчика SPFx, Workbench сообщит вам, что он не загружает сценарии из localhost. Остановите процесс, выполняющийся в данный момент в окне консоли, выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика, а затем выполните команду `gulp serve` еще раз.

  ![Версия SharePoint Workbench, запущенная на сайте SharePoint Online](../../../images/sp-workbench-o365.png)

2. Обратите внимание, что SharePoint Workbench теперь включает панель навигации Office 365. 

3. Нажмите **значок добавления** на холсте, чтобы открыть панель элементов. В панели элементов теперь отображаются веб-части, доступные на сайте с SharePoint Workbench, а также веб-часть **HelloWorldWebPart**.

  ![Панель элементов в версии SharePoint Workbench, запущенной на сайте SharePoint Online](../../../images/sp-workbench-o365-toolbox.png)

4. Добавьте **HelloWorld** из панели элементов. Теперь ваша веб-часть работает на странице в SharePoint.

  ![Веб-часть HelloWorld в версии SharePoint Workbench, запущенной на сайте SharePoint Online](../../../images/sp-workbench-o365-helloworld-wp.png)

> [!NOTE]
> Цвет веб-части зависит от цвета сайта. По умолчанию веб-часть наследует основные цвета с сайта, на котором она размещена, с помощью динамических ссылок на используемые там стили Office UI Fabric Core.

Так как ваша веб-часть по-прежнему находится на этапе разработки и тестирования, ее не нужно упаковывать и развертывать в SharePoint. 

## <a name="next-steps"></a>Дальнейшие действия

Поздравляем с запуском вашей первой веб-части Hello World! 

Теперь, когда веб-часть работает, вы можете продолжить ее разработку, ознакомившись со статьей [Подключение веб-части к SharePoint](./connect-to-sharepoint.md). В ней рассказывается, как добавить в веб-часть Hello World возможность взаимодействия с REST API для списков SharePoint. Обратите внимание, что команда `gulp serve` по-прежнему запущена в окне консоли (или в Visual Studio Code, если вы используете этот редактор). Можете переходить к следующей статье, не останавливая ее.

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!