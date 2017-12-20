---
title: "Перенос решения с jQuery и DataTables, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 4a7092759ceb458b5f3036a627dd3e4411bec147
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="migrate-jquery-and-datatables-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a>Перенос решения с jQuery и DataTables, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework

Один из часто используемых подключаемых модулей jQuery — [DataTables](https://datatables.net/). С помощью таблиц данных вы можете легко создавать функциональные представления данных, поступающих из SharePoint и внешних API. В этой статье показано, как перенести модификацию SharePoint с использованием модуля DataTables, созданную с помощью веб-части редактора скриптов, на платформу SharePoint Framework.

## <a name="list-of-it-requests-built-using-the-script-editor-web-part"></a>Список запросов в службу поддержки, созданный с помощью веб-части редактора скриптов

Чтобы проиллюстрировать перенос модификации SharePoint с использованием модуля DataTables на платформу SharePoint Framework, мы будем использовать представленное ниже решение, которое показывает обзор запросов в службу поддержки, полученных из списка SharePoint.

![Обзор запросов в службу поддержки на странице SharePoint](../../../images/datatables-sewp.png)

Решение создано с помощью стандартной веб-части редактора скриптов SharePoint. Ниже представлен код, используемый модификацией.

```html
<script src="https://code.jquery.com/jquery-1.12.4.js"></script>
<script src="https://cdn.datatables.net/1.10.15/js/jquery.dataTables.js"></script>
<script src="https://momentjs.com/downloads/moment.min.js"></script>
<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
<table id="requests" class="display" cellspacing="0" width="100%">
    <thead>
        <tr>
            <th>ID</th>
            <th>Business unit</th>
            <th>Category</th>
            <th>Status</th>
            <th>Due date</th>
            <th>Assigned to</th>
        </tr>
    </thead>
</table>
<script>
// UMD
(function(factory) {
    "use strict";

    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], function ($) {
            return factory( $, window, document );
        });
    }
    else if (typeof exports === 'object') {
        // CommonJS
        module.exports = function (root, $) {
            if (!root) {
                root = window;
            }

            if (!$) {
                $ = typeof window !== 'undefined' ?
                    require('jquery') :
                    require('jquery')( root );
            }

            return factory($, root, root.document);
        };
    }
    else {
        // Browser
        factory(jQuery, window, document);
    }
}
(function($, window, document) {
    $.fn.dataTable.render.moment = function (from, to, locale) {
        // Argument shifting
        if (arguments.length === 1) {
            locale = 'en';
            to = from;
            from = 'YYYY-MM-DD';
        }
        else if (arguments.length === 2) {
            locale = 'en';
        }

        return function (d, type, row) {
            var m = window.moment(d, from, locale, true);

            // Order and type get a number value from Moment, everything else
            // sees the rendered value
            return m.format(type === 'sort' || type === 'type' ? 'x' : to);
        };
    };
}));
</script>
<script>
$(document).ready(function() {
    $('#requests').DataTable({
        'ajax': {
        'url': "../_api/web/lists/getbytitle('IT Requests')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title",
        'headers': { 'Accept': 'application/json;odata=nometadata' },
        'dataSrc': function(data) {
            return data.value.map(function(item) {
                return [
                    item.ID,
                    item.BusinessUnit,
                    item.Category,
                    item.Status,
                    new Date(item.DueDate),
                    item.AssignedTo.Title
                ];
            });
        }
    },
    columnDefs: [{
        targets: 4,
        render: $.fn.dataTable.render.moment('YYYY/MM/DD')
    }]
    });
});
</script>
```

Сначала модификация загружает используемые ею библиотеки: jQuery, DataTables и Moment.js (строки 1–4). Затем она задает структуру таблицы, используемой для представления данных (строки 5–16). После создания таблицы она помещает Moment.js в подключаемый модуль DataTables, чтобы отображаемые в таблице даты можно было форматировать (первый блок скрипта в строках 17–70). В завершение модификация загружает и представляет список запросов в службу поддержки с помощью модуля DataTables. Данные загружаются с помощью AJAX из списка SharePoint (строки 71–96).

Благодаря модулю DataTables пользователи получают функциональное решение, в котором легко фильтровать, сортировать и перелистывать результаты, не прилагая дополнительных усилий.

![Список запросов в службу поддержки, отображаемый с помощью таблиц данных, который отфильтрован по запросам, назначенным пользователю Lidia и отсортирован по дате выполнения](../../../images/datatables-sewp-filter.png)

## <a name="migrate-the-it-requests-overview-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a>Перенос решения для просмотра запросов в службу поддержки из веб-части редактора скриптов на платформу SharePoint Framework

> [!NOTE] 
> Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment.md) для создания решений на платформе SharePoint Framework.

Преобразование этой модификации для платформы SharePoint Framework предоставляет ряд преимуществ, таких как удобство настройки и централизованное управление решением. Ниже представлено пошаговое руководство по переносу решения на платформу SharePoint Framework. Для начала мы перенесем решение на платформу SharePoint Framework, внося как можно меньше изменений в исходный код. Затем мы преобразуем код решения в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов во время разработки.

> Исходный код проекта на разных этапах миграции доступен на странице [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-datatables](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-datatables).

### <a name="create-new-sharepoint-framework-project"></a>Создание проекта SharePoint Framework

Для начала создайте папку проекта.

```sh
md datatables-itrequests
```

Перейдите в папку проекта:

```sh
cd datatables-itrequests
```

В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:

```sh
yo @microsoft/sharepoint
```

Определите значения следующим образом:
- имя решения — **datatables-itrequests**;
- расположение файлов — **Use the current folder** (Использовать текущую папку);
- отправная точка создания веб-части — **No javaScript web framework** (Без платформы JavaScript);
- имя веб-части — **IT requests** (Запросы в службу поддержки);
- описание веб-части — **Shows overview of IT support requests** (Показывает обзор запросов в службу поддержки).

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/datatables-yeoman.png)

После завершения скаффолдинга блокируйте версию зависимостей проекта, выполнив следующую команду:

```sh
npm shrinkwrap
```

Далее откройте папку проекта в редакторе кода. В этом руководстве используется Visual Studio Code.

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/datatables-vscode.png)

### <a name="load-javascript-libraries"></a>Загрузка библиотек JavaScript

Как и в исходном решении, созданном с помощью веб-части редактора скриптов, сначала следует загрузить библиотеки JavaScript, необходимые решению. В SharePoint Framework эта операция обычно делится на два этапа: указание URL-адреса, с которого будет загружена библиотека, и обращение к библиотеке в коде.

Для начала укажите URL-адрес, с которого следует загружать библиотеки. В редакторе кода откройте файл **./config/config.json** и замените раздел **externals** на следующий код:

```json
{
  "externals": {
    "jquery": "https://code.jquery.com/jquery-1.12.4.min.js",
    "datatables.net": "https://cdn.datatables.net/1.10.15/js/jquery.dataTables.min.js",
    "moment": "https://momentjs.com/downloads/moment.min.js"
  }
}
```

Затем откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и после последнего оператора **import** добавьте следующий код:

```ts
import 'jquery';
import 'datatables.net';
import 'moment';
```

### <a name="define-data-table"></a>Определение таблицы данных

Как и в исходном решении, дальше следует определить структуру таблицы, используемой для отображения данных. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените метод **render** на следующий код:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table id="requests" class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;
  }
  // ...
}
```

### <a name="register-momentjs-plugin-for-datatables"></a>Регистрация подключаемого модуля Moment.js для DataTables

Теперь необходимо определить подключаемый модуль Moment.js для модуля DataTables, чтобы даты в таблице можно было форматировать. В папке **./src/webparts/itRequests** создайте файл с именем **moment-plugin.js** и вставьте следующий код:

```js
// UMD
(function (factory) {
    "use strict";

    if (typeof define === 'function' && define.amd) {
        // AMD
        define(['jquery'], function ($) {
            return factory($, window, document);
        });
    }
    else if (typeof exports === 'object') {
        // CommonJS
        module.exports = function (root, $) {
            if (!root) {
                root = window;
            }

            if (!$) {
                $ = typeof window !== 'undefined' ?
                    require('jquery') :
                    require('jquery')(root);
            }

            return factory($, root, root.document);
        };
    }
    else {
        // Browser
        factory(jQuery, window, document);
    }
}

(function ($, window, document) {
    $.fn.dataTable.render.moment = function (from, to, locale) {
        // Argument shifting
        if (arguments.length === 1) {
            locale = 'en';
            to = from;
            from = 'YYYY-MM-DD';
        }
        else if (arguments.length === 2) {
            locale = 'en';
        }

        return function (d, type, row) {
            var moment = require('moment');
            var m = moment(d, from, locale, true);

            // Order and type get a number value from Moment, everything else
            // sees the rendered value
            return m.format(type === 'sort' || type === 'type' ? 'x' : to);
        };
    };
}));
```

Чтобы веб-часть загрузила подключаемый модуль, она должна ссылаться на новый файл **moment-plugin.js**. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и после последнего оператора **import** добавьте следующий код:

```ts
import './moment-plugin';
```

> [!NOTE] 
> Ссылаясь на другие файлы, не нужно включать расширение **.js**. SharePoint Framework автоматически определит расширение.

### <a name="initiate-datatables-and-load-data"></a>Инициализация модуля DataTables и загрузка данных

Последний этап — добавление кода, инициализирующего таблицу данных и загружающего данные из SharePoint. В папке **./src/webparts/itRequests** создайте файл с именем **script.js** и вставьте следующий код:

```js
$(document).ready(function () {
    $('#requests').DataTable({
        'ajax': {
            'url': "../../_api/web/lists/getbytitle('IT Requests')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title",
            'headers': { 'Accept': 'application/json;odata=nometadata' },
            'dataSrc': function (data) {
                return data.value.map(function (item) {
                    return [
                        item.ID,
                        item.BusinessUnit,
                        item.Category,
                        item.Status,
                        new Date(item.DueDate),
                        item.AssignedTo.Title
                    ];
                });
            }
        },
        columnDefs: [{
            targets: 4,
            render: $.fn.dataTable.render.moment('YYYY/MM/DD')
        }]
    });
});
```

Чтобы сослаться на этот файл в веб-части, откройте в редакторе кода файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и измените метод **render** на следующий код:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table id="requests" class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;

      require('./script');
  }
  // ...
}
```

Убедитесь, что веб-часть работает надлежащим образом, выполнив в командной строке следующую команду:

```sh
gulp serve --nobrowser
```

Так как веб-часть загружает свои данные из SharePoint, необходимо протестировать ее с помощью размещенного рабочего места SharePoint Framework. Перейдите на страницу **https://yourtenant.sharepoint.com/_layouts/workbench.aspx** и добавьте веб-часть на холст. Должны появиться запросы в службу поддержки, отображаемые с помощью подключаемого модуля DataTables для jQuery.

![Запросы в службу поддержки, отображаемые в клиентской веб-части SharePoint Framework](../../../images/datatables-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a>Добавление поддержки настройки веб-части с помощью ее свойств

На предыдущих этапах мы перенесли решения для просмотра запросов в службу поддержки из веб-части редактора скриптов на платформу SharePoint Framework. Решение уже работает надлежащим образом, но не использует преимущества SharePoint Framework. Имя списка, из которого загружаются запросы в службу поддержки, включено в код, представляющий собой обычный код JavaScript, который сложнее оптимизировать, чем TypeScript. Ниже показано, как расширить имеющееся решение, чтобы пользователь мог указывать имя списка, из которого будут загружаться данные. Позже мы преобразуем код в TypeScript, чтобы воспользоваться функциями безопасности типов.

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a>Определение свойства веб-части для хранения имени списка

Для начала определите свойство веб-части для хранения имени списка, из которого загружаются запросы в службу поддержки. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.manifest.json**, измените имя заданного по умолчанию свойства **description** на **listName** и удалите его значение.

![Свойство listName манифеста веб-части, выделенное в Visual Studio Code](../../../images/datatables-spfx-listname-property.png)

Затем обновите интерфейс свойств веб-части, чтобы увидеть изменения в манифесте. В редакторе кода откройте файл **./src/webparts/itRequests/IItRequestsWebPartProps.ts** и измените его содержимое на следующее:

```ts
export interface IItRequestsWebPartProps {
  listName: string;
}
```

Затем обновите метки отображения свойства **listName**. Откройте файл **./src/webparts/itRequests/loc/mystrings.d.ts** и измените его содержимое на следующее:

```ts
declare interface IItRequestsStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListNameFieldLabel: string;
}

declare module 'itRequestsStrings' {
  const strings: IItRequestsStrings;
  export = strings;
}
```

Затем откройте файл **./src/webparts/itRequests/loc/en-us.js** и измените его содержимое на следующее:

```js
define([], function() {
  return {
    "PropertyPaneDescription": "IT Requests settings",
    "BasicGroupName": "Data",
    "ListNameFieldLabel": "List name"
  }
});
```

Напоследок обновите веб-часть, чтобы она использовала новое свойство. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените метод **getPropertyPaneConfiguration** на следующий код:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  // ...
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
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }

  protected get disableReactivePropertyChanges(): boolean {
    return true;
  }
}
```

Чтобы веб-часть не перезагружалась, когда пользователь вводит имя списка, она также должна использовать нереактивную область свойств. Для этого добавьте метод **disableReactivePropertyChanges** и задайте для него возвращаемое значение **true**.

### <a name="use-the-configured-name-of-the-list-to-load-the-data-from"></a>Использование заданного имени списка для загрузки данных

Изначально имя списка, из которого загружаются данные, было встроено в запрос REST. Теперь, когда пользователи могут настраивать это имя, указанное значение должно отправляться в запрос REST перед загрузкой данных. Это проще всего сделать, переместив содержимое файла **script.js** в основной файл веб-части.

В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените метод **render** на следующий код:

```ts
var $: any = (window as any).$;

export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;

    $(document).ready(() => {
      $('table', this.domElement).DataTable({
        'ajax': {
          'url': `../../_api/web/lists/getbytitle('${escape(this.properties.listName)}')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title`,
          'headers': { 'Accept': 'application/json;odata=nometadata' },
          'dataSrc': function (data) {
            return data.value.map(function (item) {
              return [
                item.ID,
                item.BusinessUnit,
                item.Category,
                item.Status,
                new Date(item.DueDate),
                item.AssignedTo.Title
              ];
            });
          }
        },
        columnDefs: [{
          targets: 4,
          render: $.fn.dataTable.render.moment('YYYY/MM/DD')
        }]
      });
    });
  }

  // ...
}
```

Вместо того чтобы ссылаться на код из файла **script.js**, мы включаем все содержимое в метод **render** веб-части. Теперь вы можете заменить фиксированное имя списка в запросе REST (строка 40) на значение свойства **listName**, в котором хранится указанное пользователем имя списка. Прежде чем использовать это значение, мы применим функцию lodash **escape**, чтобы запретить внедрение сценариев.

На этом этапе большая часть кода по-прежнему написана на обычном JavaScript. Во избежание проблем с переменной jQuery **$** при сборке мы определили для нее тип **any** в строке 18. Позже, когда мы будем преобразовывать код в TypeScript, мы заменим его на подходящее определение типа.

Так как мы только что переместили содержимое файла **script.js** в основной файл веб-части, файл **script.js** больше не требуется и его можно удалить из проекта.

Чтобы убедиться, что веб-часть работает надлежащим образом, выполните в командной строке следующую команду:

```sh
gulp serve --nobrowser
```

Перейдите к размещенному рабочему месту и добавьте веб-часть на холст. Откройте область свойств веб-части, укажите имя списка запросов в службу поддержки и нажмите кнопку **Применить**, чтобы подтвердить изменения. Теперь в веб-части должны отображаться запросы в службу поддержки.

![Запросы в службу поддержки, загруженные из указанного списка и отображаемые в клиентской веб-части SharePoint Framework](../../../images/datatables-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a>Преобразование обычного кода JavaScript в TypeScript

Использование TypeScript вместо обычного JavaScript предоставляет ряд преимуществ. TypeScript не только упрощает поддержку и оптимизацию, но и позволяет раньше обнаруживать ошибки. Ниже описано, как преобразовать первоначальный код JavaScript в TypeScript.

### <a name="add-type-definitions-for-used-libraries"></a>Добавление определений типов для используемых библиотек

Для надлежащей работы TypeScript необходимы определения типов для различных библиотек, используемых в проекте. Определения типов часто распространяются в виде пакетов npm в пространстве имен @types.

Для начала установите определения типов для jQuery и DataTables, выполнив в командной строке следующую команду:

```sh
npm install --save-dev @types/jquery @types/jquery.datatables
```

Определения типов для пакета Moment.js распространяются вместе с ним. Несмотря на то что мы загружаем Moment.js с URL-адреса, для использования его типов все равно нужно установить в проекте пакет Moment.js.

Установите пакет Moment.js, выполнив в командной строке следующую команду:

```sh
npm install --save moment
```

### <a name="update-package-references"></a>Обновление ссылок на пакеты

Чтобы использовать типы из установленных определений, необходимо изменить ссылки на библиотеки. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените оператор `import 'jquery';` на следующий:

```ts
import * as $ from 'jquery';
```

Определив **$** как jQuery, вы можете удалить добавленное ранее локальное определение **$**:

```ts
var $: any = (window as any).$;
```

DataTables — это подключаемый модуль для jQuery, который присоединяется к jQuery, поэтому определение его типа невозможно загрузить напрямую. Вместо этого необходимо добавить его в список глобально загружаемых типов. В редакторе кода откройте файл **./tsconfig.json** и добавьте **jquery.datatables** в массив **types**:

```json
{
  "compilerOptions": {
    "target": "es5",
    "forceConsistentCasingInFileNames": true,
    "module": "commonjs",
    "jsx": "react",
    "declaration": true,
    "sourceMap": true,
    "types": [
      "es6-promise",
      "es6-collections",
      "jquery.datatables",
      "webpack-env"
    ]
  }
}
```

### <a name="update-main-web-part-files-to-typescript"></a>Преобразование основных файлов веб-части в TypeScript

Теперь, когда у нас есть определения типов для всех библиотек, установленных в проекте, можно приступить к преобразованию обычного кода JavaScript в TypeScript.

Для начала определите интерфейс для сведений о запросах в службу поддержки, полученных из списка SharePoint. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и сразу над классом веб-части добавьте следующий фрагмент кода:

```ts
interface IRequestItem {
  ID: number;
  BusinessUnit: string;
  Category: string;
  Status: string;
  DueDate: string;
  AssignedTo: { Title: string; };
}
```

Затем в классе веб-части замените метод **render** на следующий код:

```ts
export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
  public render(): void {
    this.domElement.innerHTML = `
      <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.15/css/jquery.dataTables.min.css" />
      <table class="display ${styles.helloWorld}" cellspacing="0" width="100%">
        <thead>
            <tr>
                <th>ID</th>
                <th>Business unit</th>
                <th>Category</th>
                <th>Status</th>
                <th>Due date</th>
                <th>Assigned to</th>
            </tr>
        </thead>
      </table>`;

    $('table', this.domElement).DataTable({
      'ajax': {
        'url': `../../_api/web/lists/getbytitle('${escape(this.properties.listName)}')/items?$select=ID,BusinessUnit,Category,Status,DueDate,AssignedTo/Title&$expand=AssignedTo/Title`,
        'headers': { 'Accept': 'application/json;odata=nometadata' },
        'dataSrc': (data: { value: IRequestItem[] }): any[][] => {
          return data.value.map((item: IRequestItem): any[] => {
            return [
              item.ID,
              item.BusinessUnit,
              item.Category,
              item.Status,
              new Date(item.DueDate),
              item.AssignedTo.Title
            ];
          });
        }
      },
      columnDefs: [{
        targets: 4,
        render: $.fn.dataTable.render.moment('YYYY/MM/DD')
      }]
    });
  }

  // ...
}
```

Обратите внимание, что запрос AJAX для получения данных из списка SharePoint теперь типизирован и помогает гарантировать, что вы ссылаетесь на правильные свойства, передавая их в массив в модуле DataTables. Структура данных, используемая модулем DataTables для представления строки в таблице, — это массив смешанных типов, поэтому для простоты она была определена как **any[]**. Использование типа **any** в этом контексте допустимо, так как данные, возвращаемые в свойстве **dataSrc**, используются внутри модуля DataTables.

Обновляя метод **render**, мы внесли еще два изменения. Во-первых, мы удалили из таблицы атрибут **id**. Это позволяет размещать на странице несколько экземпляров одной веб-части. Кроме того, удалена ссылка на функцию `$(document).ready()`, в которой нет необходимости, так как модель DOM элемента, где отрисовывается таблица данных, задается перед кодом инициализации DataTables.

### <a name="update-the-momentjs-datatables-plugin-to-typescript"></a>Преобразование подключаемого модуля Moment.js для DataTables в TypeScript

Последний компонент решения, который необходимо преобразовать в TypeScript, — это подключаемый модуль Moment.js для DataTables. Для начала измените имя файла **./src/webparts/itRequests/moment-plugin.js** на **./src/webparts/itRequests/moment-plugin.ts**, чтобы его обрабатывал компилятор TypeScript. Затем откройте файл **moment-plugin.ts** в редакторе кода и замените его содержимое на следующее:

```ts
import * as $ from 'jquery';
import * as moment from 'moment';

/* tslint:disable:no-function-expression */
$.fn.dataTable.render.moment = function (from: string, to: string, locale: string): (d: any, type: string, row: any) => string {
/* tslint:enable */
    // Argument shifting
    if (arguments.length === 1) {
        locale = 'en';
        to = from;
        from = 'YYYY-MM-DD';
    }
    else if (arguments.length === 2) {
        locale = 'en';
    }

    return (d: any, type: string, row: any): string => {
        let m: moment.Moment = moment(d, from, locale, true);

        // Order and type get a number value from Moment, everything else
        // sees the rendered value
        return m.format(type === 'sort' || type === 'type' ? 'x' : to);
    };
};
```

Для начала мы загрузим ссылки на jQuery и Moment.js, чтобы сообщить TypeScript, на что ссылаются соответствующие переменные. Затем мы определим функцию подключаемого модуля. Как правило, в TypeScript для функций используется стрелочная нотация (`=>`). Однако в данном случае, так как нам требуется доступ к свойству **arguments**, необходимо использовать обычное определение функции. Чтобы tslint не выводил предупреждение о том, что не используется стрелочная нотация, вы можете в явной форме отключить правило **no-function-expression** для определения функции.

Чтобы убедиться, что все работает должным образом, в командной строке выполните следующую команду:

```sh
gulp serve --nobrowser
```

Перейдите к размещенному рабочему месту и добавьте веб-часть на холст. Визуально ничего не изменилось, но новая кодовая база использует TypeScript и соответствующие определения типов, упрощая поддержку решения.
