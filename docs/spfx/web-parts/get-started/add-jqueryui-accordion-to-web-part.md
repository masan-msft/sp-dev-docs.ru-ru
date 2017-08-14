# <a name="add-jqueryui-accordion-to-your-sharepoint-client-side-web-part"></a>Добавление элемента Accordion jQueryUI в клиентскую веб-часть SharePoint

В этой статье описано, как добавить элемент Accordion jQueryUI в проект веб-части. Для этого нужно создать новую веб-часть, как показано на приведенном ниже изображении. 

![Снимок экрана: веб-часть, включающая элемент Accordion jQuery](../../../../images/jquery-accordion-wb.png)

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq). 

<a href="https://www.youtube.com/watch?v=-3m__hRQxEI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../../images/spfx-youtube-tutorial5.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="prerequisites"></a>Обязательные условия
Прежде чем начать, выполните следующие действия:

* [Создайте свою первую веб-часть](build-a-hello-world-web-part.md).
* [Подключитесь к SharePoint](connect-to-sharepoint.md).

Цепочка инструментов разработчика для добавления веб-частей в пакет использует Webpack, SystemJS и CommonJS. При этом загружаются возможные внешние зависимости, такие как jQuery и jQueryUI. Для загрузки внешних зависимостей на более высоком уровне:

* Получите внешнюю библиотеку с помощью npm или скачайте ее на сайте поставщика.
* Установите [определения типов TypeScript](http://definitelytyped.org/) для соответствующей платформы (при наличии).
* При необходимости обновите конфигурацию решения, чтобы в пакет веб-части не добавлялась по умолчанию внешняя зависимость.

## <a name="create-a-new-web-part-project"></a>Создание проекта веб-части

Создайте каталог проекта в любом расположении:

```
md jquery-webpart
```
    
> **Предупреждение.** Создайте этот каталог в новой папке, а не в папке, вложенной в `helloworld-webpart`.

Перейдите к каталогу проекта:

```
cd jquery-webpart
```
    
Создайте веб-часть jQuery, запустив генератор Yeoman для SharePoint:

```
yo @microsoft/sharepoint
```

Когда появится запрос:

* Оставьте имя по умолчанию (**jquery-webpart**) для своего решения и нажмите клавишу **ВВОД**.
* Выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.

Далее вам потребуется указать определенные сведения о веб-части:

* Оставьте выбранным параметр **No javascript web framework** (Не использовать платформу веб-решений на базе JavaScript) по умолчанию и нажмите клавишу **ВВОД**, чтобы продолжить.
* Введите имя **jQuery** для веб-части и нажмите клавишу **ВВОД**.
* Введите описание веб-части **jQuery Web Part** и нажмите клавишу **ВВОД**. 

После этого Yeoman установит необходимые зависимости и выполнит скаффолдинг файлов решения. Это может занять несколько минут. При этом Yeoman также включит в проект веб-часть **jQueryWebPart**.

Введите в консоли следующий код, чтобы открыть проект веб-части в Visual Studio Code:

```
code .
```

## <a name="install-jquery-and-jquery-ui-npm-packages"></a>Установка пакетов npm jQuery и jQuery UI

Введите в консоли следующий код, чтобы установить пакет npm jQuery:

```
npm install --save jquery@2
```

 Теперь введите следующий код, чтобы установить пакет npm jQueryUI:

```
npm install --save jqueryui
```

Далее необходимо установить определения типов для проекта. Начиная с TypeScript 2.0 определения типов можно устанавливать с помощью npm.

Откройте консоль и установите необходимые типы:

```
npm install --save @types/jquery@2
npm install --save @types/jqueryui
```

### <a name="unbundle-external-dependencies-from-web-part-bundle"></a>Извлечение внешних зависимостей из пакета веб-части
По умолчанию все добавляемые зависимости включаются в пакет веб-части. Это не всегда удобно. Вы можете извлечь эти зависимости из пакета веб-части.

Откройте файл config\config.json в Visual Studio Code.

Этот файл содержит сведения о пакетах и возможных внешних зависимостях. 

Область `entries` содержит сведения о пакете по умолчанию (в данном случае — пакете веб-части jQuery). Каждой добавленной веб-части, добавленной в решение, соответствует одна запись.

```json
"entries": [
  {
    "entry": "./lib/webparts/jQuery/jQueryWebPart.js",
    "manifest": "./src/webparts/jQuery/jQueryWebPart.manifest.json",
    "outputPath": "./dist/j-query.bundle.js",
  }
]
```

Раздел `externals` содержит библиотеки, не включенные в пакет по умолчанию. 

```json
  "externals": {},
```

Чтобы исключить `jQuery` и `jQueryUI` из пакета по умолчанию, добавьте модули в раздел `externals`:

```json
"jquery":"node_modules/jquery/dist/jquery.min.js",
"jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
```

Теперь при создании проекта `jQuery` и `jQueryUI` не будут добавляться в пакет веб-части по умолчанию.

Ниже приведено полное содержимое файла config.json на настоящий момент.

```json
{
  "entries": [
    {
      "entry": "./lib/webparts/jQuery/JQueryWebPart.js",
      "manifest": "./src/webparts/jQuery/JQueryWebPart.manifest.json",
      "outputPath": "./dist/j-query.bundle.js"
    }
  ],
  "externals": {
    "jquery":"node_modules/jquery/dist/jquery.min.js",
    "jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
  },
  "localizedResources": {
    "jQueryStrings": "webparts/jQuery/loc/{locale}.js"
  }
}
```


## <a name="build-the-accordion"></a>Создание элемента Accordion

Откройте папку проекта **jquery-webpart** в Visual Studio Code. Проект должен содержать веб-часть jQuery, добавленную ранее в папку /src/webparts/jQuery.

### <a name="add-accordion-html"></a>Добавление HTML-кода Accordion
Добавьте в папку `src/webparts/jQuery` новый файл **MyAccordionTemplate.ts**.

Создайте и экспортируйте (как модуль) класс `MyAccordionTemplate`, содержащий HTML-код элемента Accordion.

```ts
export default class MyAccordionTemplate {
    public static templateHtml: string =  `
      <div class="accordion">
        <h3>Section 1</h3>
        <div>
            <p>
            Mauris mauris ante, blandit et, ultrices a, suscipit eget, quam. Integer
            ut neque. Vivamus nisi metus, molestie vel, gravida in, condimentum sit
            amet, nunc. Nam a nibh. Donec suscipit eros. Nam mi. Proin viverra leo ut
            odio. Curabitur malesuada. Vestibulum a velit eu ante scelerisque vulputate.
            </p>
        </div>
        <h3>Section 2</h3>
        <div>
            <p>
            Sed non urna. Donec et ante. Phasellus eu ligula. Vestibulum sit amet
            purus. Vivamus hendrerit, dolor at aliquet laoreet, mauris turpis porttitor
            velit, faucibus interdum tellus libero ac justo. Vivamus non quam. In
            suscipit faucibus urna.
            </p>
        </div>
        <h3>Section 3</h3>
        <div>
            <p>
            Nam enim risus, molestie et, porta ac, aliquam ac, risus. Quisque lobortis.
            Phasellus pellentesque purus in massa. Aenean in pede. Phasellus ac libero
            ac tellus pellentesque semper. Sed ac felis. Sed commodo, magna quis
            lacinia ornare, quam ante aliquam nisi, eu iaculis leo purus venenatis dui.
            </p>
            <ul>
            <li>List item one</li>
            <li>List item two</li>
            <li>List item three</li>
            </ul>
        </div>
        <h3>Section 4</h3>
        <div>
            <p>
            Cras dictum. Pellentesque habitant morbi tristique senectus et netus
            et malesuada fames ac turpis egestas. Vestibulum ante ipsum primis in
            faucibus orci luctus et ultrices posuere cubilia Curae; Aenean lacinia
            mauris vel est.
            </p>
            <p>
            Suspendisse eu nisl. Nullam ut libero. Integer dignissim consequat lectus.
            Class aptent taciti sociosqu ad litora torquent per conubia nostra, per
            inceptos himenaeos.
            </p>
        </div>
     </div>`;
}
```

Сохраните файл.

### <a name="import-accordion-html"></a>Импорт HTML-кода Accordion

В Visual Studio Code откройте **src\webparts\jQuery\JQueryWebPart.ts**.

В верхней части файла, где указаны другие операции импорта, добавьте следующий код:

```ts
import MyAccordionTemplate from './MyAccordionTemplate';
```

### <a name="import-jquery-and-jqueryui"></a>Импорт jQuery и jQueryUI
Вы можете импортировать jQuery в свою веб-часть так же, как импортировали MyAccordionTemplate.

В верхней части файла, где указаны другие операции импорта, добавьте следующий код:

```ts
import * as jQuery from 'jquery';
import 'jqueryui';
```

После этого необходимо загрузить внешние CSS-файлы. Для этого используйте загрузчик модулей. Добавьте следующую операцию импорта:

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';
```

Чтобы загрузить стили jQueryUI, в классе `JQueryWebPart` веб-части необходимо добавить конструктор и использовать импортированный ранее SPComponentLoader. Добавьте представленный ниже конструктор в веб-часть. 

```ts
  public constructor() {
    super();

    SPComponentLoader.loadCss('//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css');
  }
```

Этот код выполняет следующие действия:

* Вызывает родительский конструктор с контекстом для инициализации веб-части.
* Асинхронно загружает стили accordion из CDN.

### <a name="render-accordion"></a>Отрисовка Accordion

В `jQueryWebPart.ts` перейдите к методу `render`.

Укажите отрисовку HTML-кода accordion во внутреннем HTML-коде веб-части:

```ts
this.domElement.innerHTML = MyAccordionTemplate.templateHtml;
```

Настроить элемент Accordion jQueryUI можно несколькими способами. Задайте несколько параметров для элемента accordion прямо под строкой `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:

```ts
const accordionOptions: JQueryUI.AccordionOptions = {
  animate: true,
  collapsible: false,
  icons: {
    header: 'ui-icon-circle-arrow-e',
    activeHeader: 'ui-icon-circle-arrow-s'
  }
};
```

Как видите, типизированное определение jQueryUI позволяет создать типизированную переменную `JQueryUI.AccordionOptions` и указать поддерживаемые свойства. 

Поэкспериментировав с IntelliSense, вы заметите, что поддерживаются все доступные методы в `JQueryUI.`, а также параметры методов.

Инициализируйте элемент accordion:

```ts
jQuery('.accordion', this.domElement).accordion(accordionOptions);
```

Как видите, применяется переменная `jQuery`, которую вы использовали для импорта модуля `jquery`. Затем инициализируется элемент Accordion.

Метод `render` полностью выглядит так:

```ts
public render(): void {
  this.domElement.innerHTML = MyAccordionTemplate.templateHtml;

  const accordionOptions: JQueryUI.AccordionOptions = {
    animate: true,
    collapsible: false,
    icons: {
      header: 'ui-icon-circle-arrow-e',
      activeHeader: 'ui-icon-circle-arrow-s'
    }
  };

  jQuery('.accordion', this.domElement).accordion(accordionOptions);
}
```

Сохраните файл.

## <a name="preview-the-web-part"></a>Просмотр веб-части

В консоли откройте папку jquery-webpart и введите следующую строку для сборки и просмотра веб-части:

```
gulp serve
```

> **Примечание.** Visual Studio Code поддерживает Gulp и другие средства запуска задач. Нажмите клавиши **CTRL+SHIFT+B** в Windows или **CMD+SHIFT+B** в Mac OS для отладки и просмотра веб-части.

Gulp выполнит задачи и откроет локальную рабочую область веб-частей SharePoint.

Выберите значок **+** на холсте страницы, чтобы отобразить список веб-частей, и добавьте веб-часть jQuery. Теперь должен появиться элемент Accordion jQueryUI!

![Снимок экрана: веб-часть, включающая элемент Accordion jQuery](../../../../images/jquery-accordion-wb.png)

В консоли, в которой запущена команда `gulp serve`, нажмите клавиши **CTRL+C**, чтобы завершить задачу.
