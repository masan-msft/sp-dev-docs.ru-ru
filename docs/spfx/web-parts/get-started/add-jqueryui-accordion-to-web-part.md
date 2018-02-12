---
title: "Добавление элемента Accordion jQueryUI в клиентскую веб-часть SharePoint"
description: "Чтобы добавить в проект веб-части элемент \"аккордеон\" jQueryUI, требуется создать новую веб-часть."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 3c692687133db378dd23842d1ef28ad202e733eb
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="add-jqueryui-accordion-to-your-sharepoint-client-side-web-part"></a>Добавление элемента "аккордеон" jQueryUI в клиентскую веб-часть SharePoint

Чтобы добавить в проект веб-части элемент "аккордеон" jQueryUI, требуется создать новую веб-часть, как показано на следующем изображении. 

![Снимок экрана: веб-часть, включающая элемент "аккордеон" jQuery](../../../images/jquery-accordion-wb.png)

Прежде чем начинать, выполните следующие действия:

* [Создайте свою первую веб-часть](build-a-hello-world-web-part.md).
* [Подключите веб-часть к SharePoint](connect-to-sharepoint.md).

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=7UOxTbMMPrQ&index=6&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq). 

<a href="https://www.youtube.com/watch?v=7UOxTbMMPrQ&index=6&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../images/spfx-youtube-tutorial5.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

Цепочка инструментов разработчика для добавления веб-частей в пакет использует Webpack, SystemJS и CommonJS. При этом загружаются возможные внешние зависимости, такие как jQuery и jQueryUI. Для загрузки внешних зависимостей на более высоком уровне:

* Получите внешнюю библиотеку с помощью npm или скачайте ее на сайте поставщика.
* Установите [определения типов TypeScript](http://definitelytyped.org/) для соответствующей платформы (при наличии).
* При необходимости обновите конфигурацию решения, чтобы в пакет веб-части не добавлялась по умолчанию внешняя зависимость.

## <a name="create-a-new-web-part-project"></a>Создание проекта веб-части

1. Создайте каталог проекта в любом расположении:

  ```
  md jquery-webpart
  ```
      
  > [!WARNING] 
  > Создайте этот каталог в новой папке, а не в папке, вложенной в `helloworld-webpart`.

2. Перейдите к каталогу проекта:

  ```
  cd jquery-webpart
  ```
    
3. Создайте веб-часть jQuery, запустив генератор Yeoman для SharePoint:

  ```
  yo @microsoft/sharepoint
  ```

4. Когда появится запрос:

  * Оставьте имя по умолчанию (**jquery-webpart**) для своего решения и нажмите клавишу ВВОД.
  * Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.
  * Выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.
  * Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании. 
  * Выберите **WebPart** в качестве типа создаваемого клиентского компонента. 

5. Ниже требуется указать информацию о веб-части:

  * Введите **jQuery** в качестве имени веб-части и нажмите клавишу ВВОД.
  * Введите описание **jQuery Web Part** (Веб-часть jQuery) и нажмите клавишу ВВОД. 
  * Оставьте параметр **No JavaScript framework** (Не использовать платформу JavaScript), задаваемый по умолчанию, и нажмите клавишу ВВОД, чтобы продолжить.

  После этого Yeoman установит необходимые зависимости и выполнит скаффолдинг файлов решения. Это может занять несколько минут. При этом Yeoman также включит в проект веб-часть **jQueryWebPart**.

6. После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:

  ```sh
  npm shrinkwrap
  ```

7. Введите следующую команду, чтобы открыть проект веб-части в Visual Studio Code:

  ```
  code .
  ```


## <a name="install-jquery-and-jquery-ui-npm-packages"></a>Установка пакетов NPM jQuery и jQuery UI

1. Введите в консоли следующий код, чтобы установить пакет npm jQuery:

  ```
  npm install --save jquery@2
  ```

2. Теперь введите следующий код, чтобы установить пакет npm jQueryUI:

  ```
  npm install --save jqueryui
  ```

  Далее необходимо установить определения типов для проекта. Начиная с TypeScript 2.0, определения типов можно устанавливать с помощью npm.

3. Откройте консоль и установите необходимые типы:

  ```
  npm install --save @types/jquery@2
  npm install --save @types/jqueryui
  ```

### <a name="to-unbundle-external-dependencies-from-web-part-bundle"></a>Извлечение внешних зависимостей из пакета веб-части

По умолчанию все добавляемые зависимости включаются в пакет веб-части. Это не всегда удобно. Вы можете извлечь эти зависимости из пакета веб-части.

1. В Visual Studio Code откройте файл **config\config.json**.

  Этот файл содержит сведения о пакетах и возможных внешних зависимостях. 

  Область `bundles` содержит сведения о пакете по умолчанию (в данном случае — пакете веб-части jQuery). Каждой веб-части, добавленной в решение, соответствует одна запись.

  ```json
    "bundles": {
      "j-query-web-part": {
        "components": [
          {
            "entrypoint": "./lib/webparts/jQuery/JQueryWebPart.js",
            "manifest": "./src/webparts/jQuery/JQueryWebPart.manifest.json"
          }
        ]
      }
    },
  ```

2. Раздел `externals` содержит библиотеки, не добавленные в пакет по умолчанию. 

  ```json
    "externals": {},
  ```

3. Чтобы исключить `jQuery` и `jQueryUI` из пакета по умолчанию, добавьте модули в раздел `externals`:

  ```json
  "jquery":"node_modules/jquery/dist/jquery.min.js",
  "jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
  ```

Теперь при создании проекта `jQuery` и `jQueryUI` не будут добавляться в пакет веб-части по умолчанию.

Ниже приведено полное содержимое файла config.json на настоящий момент.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/config.2.0.schema.json",
  "version": "2.0",
  "bundles": {
    "j-query-web-part": {
      "components": [
        {
          "entrypoint": "./lib/webparts/jQuery/JQueryWebPart.js",
          "manifest": "./src/webparts/jQuery/JQueryWebPart.manifest.json"
        }
      ]
    }
  },
  "externals": {
    "jquery":"node_modules/jquery/dist/jquery.min.js",
    "jqueryui":"node_modules/jqueryui/jquery-ui.min.js"
  },
  "localizedResources": {
    "JQueryWebPartStrings": "lib/webparts/jQuery/loc/{locale}.js"
  }
}
```


## <a name="build-the-accordion"></a>Создание элемента Accordion

Откройте папку проекта **jquery-webpart** в Visual Studio Code. Проект должен содержать веб-часть jQuery, добавленную ранее в папку `/src/webparts/jQuery`.

### <a name="to-add-the-accordion-html"></a>Добавление HTML-кода элемента "аккордеон"

1. Добавьте в папку `src/webparts/jQuery` новый файл **MyAccordionTemplate.ts**.

2. Создайте и экспортируйте (как модуль) класс `MyAccordionTemplate`, содержащий HTML-код элемента Accordion.

  ```HTML
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

3. Сохраните файл.

### <a name="to-import-the-accordion-html"></a>Импорт HTML-кода элемента "аккордеон"

1. В Visual Studio Code откройте **src\webparts\jQuery\JQueryWebPart.ts**.

2. В верхней части файла, где указаны другие операции импорта, добавьте следующий код:

  ```typescript
  import MyAccordionTemplate from './MyAccordionTemplate';
  ```

### <a name="to-import-jquery-and-jqueryui"></a>Импорт jQuery и jQueryUI

1. Вы можете импортировать jQuery в свою веб-часть так же, как импортировали MyAccordionTemplate. В верхней части файла, где указаны другие операции импорта, добавьте следующий код:

  ```typescript
  import * as jQuery from 'jquery';
  import 'jqueryui';
  ```

2. Загрузите внешние CSS-файлы, используя загрузчик модулей. Добавьте следующую операцию импорта:

  ```typescript
  import { SPComponentLoader } from '@microsoft/sp-loader';
  ```

3. Загрузите стили jQueryUI в классе `JQueryWebPart` веб-части, добавив конструктор и используя импортированный ранее SPComponentLoader. Добавьте в веб-часть следующий конструктор: 

  ```typescript
    public constructor() {
      super();

      SPComponentLoader.loadCss('//code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css');
    }
  ```

  Этот код выполняет следующие действия:

  * Вызывает родительский конструктор с контекстом для инициализации веб-части.
  * Асинхронно загружает стили элемента "аккордеон" из CDN.


### <a name="to-render-accordion"></a>Отрисовка элемента "аккордеон"

1. В `jQueryWebPart.ts` перейдите к методу `render`.

2. Укажите отрисовку HTML-кода элемента "аккордеон" во внутреннем HTML-коде веб-части:

  ```typescript
  this.domElement.innerHTML = MyAccordionTemplate.templateHtml;
  ```

3. Настроить элемент "аккордеон" jQueryUI можно несколькими способами. Задайте несколько параметров для элемента "аккордеон" прямо под оператором `this.domElement.innerHTML = MyAccordionTemplate.templateHtml;`:

  ```typescript
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

4. Инициализируйте элемент "аккордеон":

  ```typescript
  jQuery('.accordion', this.domElement).accordion(accordionOptions);
  ```

  Как видите, применяется переменная `jQuery`, которую вы использовали для импорта модуля `jquery`. Затем инициализируется элемент Accordion.

  Метод `render` полностью выглядит так:

  ```typescript
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

5. Сохраните файл.


## <a name="preview-the-web-part"></a>Просмотр веб-части

1. В консоли откройте папку jquery-webpart и введите следующую строку для сборки и просмотра веб-части:

  ```
  gulp serve
  ```

  > [!NOTE]
  > Visual Studio Code поддерживает gulp и другие средства запуска задач. Нажмите клавиши CTRL+SHIFT+B в Windows или CMD+SHIFT+B на Mac для отладки и просмотра веб-части.

  Средство gulp выполнит задачи и откроет локальную версию SharePoint Workbench.

2. Выберите значок **+** на холсте страницы, чтобы отобразить список веб-частей, и добавьте веб-часть jQuery. Теперь должен появиться элемент "аккордеон" jQueryUI!

  ![Снимок экрана: веб-часть, включающая элемент "аккордеон" jQuery](../../../images/jquery-accordion-wb.png)

3. В консоли, в которой запущена команда `gulp serve`, нажмите клавиши CTRL+C, чтобы завершить задачу.

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!

