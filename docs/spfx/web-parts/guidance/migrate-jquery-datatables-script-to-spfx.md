---
title: "Перенос решения с jQuery и DataTables, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework"
description: "Узнайте, как перенести модификацию SharePoint с DataTables для создания подробных обзоров данных, поступающих из SharePoint и внешних API."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: eae130d79f29e1bf29cd309895d0ebddd41ffc9b
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="migrate-jquery-and-datatables-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a>Перенос решения с jQuery или DataTables, созданного при помощи веб-части редактора скриптов, в SharePoint Framework

Один из часто используемых подключаемых модулей jQuery — [DataTables](https://datatables.net/). С помощью DataTables можно легко создавать подробные обзоры данных, поступающих из SharePoint и внешних API.

## <a name="list-of-it-requests-built-using-the-script-editor-web-part"></a>Список запросов в службу поддержки, созданный с помощью веб-части редактора скриптов

Чтобы проиллюстрировать перенос модификации SharePoint, для которой применяется DataTables, в SharePoint Framework, мы будем использовать представленное ниже решение, которое показывает обзор запросов о технической поддержке, полученных из списка SharePoint.

![Обзор запросов в службу поддержки на странице SharePoint](../../../images/datatables-sewp.png)

<br/>

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

Для начала модификация загружает свои библиотеки: jQuery, DataTables и Moment.js (строки 1–4). 

Затем она задает структуру таблицы, используемой для представления данных (строки 5–16). 

После создания таблицы она включает библиотеку Moment.js в подключаемый модуль DataTables, чтобы отображаемые в таблице даты можно было форматировать (первый блок скрипта в строках 17–70). 

Наконец, модификация использует модуль DataTables для загрузки и показа списка запросов о технической поддержке. Данные загружаются с помощью AJAX из списка SharePoint (строки 71–96).

Благодаря модулю DataTables пользователи получают функциональное решение, в котором легко фильтровать, сортировать и перелистывать результаты, не прилагая дополнительных усилий.

![Список запросов в службу поддержки, отображаемый с помощью таблиц данных, который отфильтрован по запросам, назначенным пользователю Lidia и отсортирован по дате выполнения](../../../images/datatables-sewp-filter.png)

## <a name="migrate-the-it-requests-overview-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a>Перенос решения для просмотра запросов в службу поддержки из веб-части редактора скриптов на платформу SharePoint Framework

> [!NOTE] 
> Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment.md) для создания решений на платформе SharePoint Framework.

Преобразование этой модификации для платформы SharePoint Framework обеспечивает ряд преимуществ, таких как удобство настройки и централизованное управление решением. Ниже представлено пошаговое руководство по переносу решения на платформу SharePoint Framework. Для начала мы перенесем решение на платформу SharePoint Framework, внося как можно меньше изменений в первоначальный код. Затем преобразуем код решения в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов во время разработки.

> [!NOTE] 
> Исходный код проекта на разных этапах миграции представлен в статье [Руководство. Перенос решения jQuery или DataTables, созданного с помощью веб-части редактора скриптов, в SharePoint Framework](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-datatables).

### <a name="create-new-sharepoint-framework-project"></a>Создание проекта SharePoint Framework

1. Для начала создайте папку проекта:

    ```sh
    md datatables-itrequests
    ```

2. Перейдите в папку проекта:

    ```sh
    cd datatables-itrequests
    ```

3. В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы выполнить скаффолдинг нового проекта на платформе SharePoint Framework:

    ```sh
    yo @microsoft/sharepoint
    ```

4. Определите значения следующим образом:

    - имя решения — **datatables-itrequests**;
    - расположение файлов — **Use the current folder** (Использовать текущую папку);
    - отправная точка создания веб-части — **No javaScript web framework** (Без платформы JavaScript);
    - имя веб-части — **IT requests** (Запросы в службу поддержки);
    - описание веб-части — **Shows overview of IT support requests** (Показывает обзор запросов в службу поддержки).

    ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/datatables-yeoman.png)

5. По завершении скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:

    ```sh
    npm shrinkwrap
    ```

6. Откройте папку проекта в редакторе кода. В этом руководстве используется Visual Studio Code.

    ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/datatables-vscode.png)

### <a name="load-javascript-libraries"></a>Загрузка библиотек JavaScript

Как и в исходном решении, созданном с помощью веб-части редактора скриптов, сначала следует загрузить библиотеки JavaScript, необходимые решению. В SharePoint Framework эта операция обычно делится на два этапа: указание URL-адреса, с которого будет загружена библиотека, и обращение к библиотеке в коде.

1. Укажите URL-адрес, с которого следует загружать библиотеки. В редакторе кода откройте файл **./config/config.json** и замените раздел **externals** на следующий код:

    ```json
    {
    "externals": {
        "jquery": "https://code.jquery.com/jquery-1.12.4.min.js",
        "datatables.net": "https://cdn.datatables.net/1.10.15/js/jquery.dataTables.min.js",
        "moment": "https://momentjs.com/downloads/moment.min.js"
    }
    }
    ```

2. Откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и после последнего оператора **import** добавьте следующий код:

    ```typescript
    import 'jquery';
    import 'datatables.net';
    import 'moment';
    ```

### <a name="define-data-table"></a>Определение таблицы данных

Как и в исходном решении, далее необходимо определить структуру таблицы, используемой для отображения данных. 

Откройте в редакторе кода файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените метод **render** на следующий код:

```typescript
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

Далее необходимо определить подключаемый модуль Moment.js для DataTables, чтобы можно было форматировать даты в таблице. 

1. В папке **./src/webparts/itRequests** создайте файл с именем **moment-plugin.js** и вставьте следующий код:

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

2. Чтобы загрузить подключаемый модуль, веб-часть должна ссылаться на новый файл **moment-plugin.js**. Откройте в редакторе кода файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и после последнего оператора **import** добавьте следующий код:

    ```typescript
    import './moment-plugin';
    ```

> [!NOTE] 
> Ссылаясь на другие файлы, не требуется включать расширение **JS**. SharePoint Framework автоматически распознает расширение.

### <a name="initiate-datatables-and-load-data"></a>Инициализация модуля DataTables и загрузка данных

Последний этап — добавление кода, инициализирующего таблицу данных и загружающего данные из SharePoint. 

1. В папке **./src/webparts/itRequests** создайте файл с именем **script.js** и вставьте следующий код:

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

2. Чтобы сослаться на этот файл в веб-части, откройте в редакторе кода файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените метод **render** на следующий код:

    ```typescript
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

3. Убедитесь, что веб-часть работает надлежащим образом, выполнив в командной строке следующую команду:

    ```sh
    gulp serve --nobrowser
    ```

Так как веб-часть загружает свои данные из SharePoint, ее необходимо тестировать с помощью размещенной рабочей области SharePoint Framework. Перейдите по адресу `https://yourtenant.sharepoint.com/_layouts/workbench.aspx` и добавьте веб-часть на холст. Теперь запросы о технической поддержке должны отображаться с помощью подключаемого модуля DataTables для jQuery.

![Запросы о технической поддержке, отображаемые в клиентской веб-части SharePoint Framework](../../../images/datatables-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a>Добавление возможности настраивать веб-часть с помощью ее свойств

На предыдущих этапах мы перенесли решение для просмотра запросов о технической поддержке из веб-части редактора скриптов на платформу SharePoint Framework. Решение уже работает надлежащим образом, но не использует преимущества платформы SharePoint Framework. Имя списка, из которого загружаются запросы о технической поддержке, включено в код, представляющий собой обычный JavaScript, который хуже поддается рефакторингу, чем TypeScript. 

В приведенных ниже разделах описано, как расширить имеющееся решение, чтобы пользователи могли указывать имя списка, из которого будут загружаться данные. Позже мы преобразуем код в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов.

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a>Определение свойства веб-части для хранения имени списка

1. Определите свойство веб-части для хранения имени списка, из которого будут загружаться запросы о технической поддержке. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.manifest.json**, замените имя заданного по умолчанию свойства **description** на **listName** и удалите его значение.

    ![Свойство listName манифеста веб-части, выделенное в Visual Studio Code](../../../images/datatables-spfx-listname-property.png)

2. Обновите интерфейс свойств веб-части, чтобы применить изменения манифеста. В редакторе кода откройте файл **./src/webparts/itRequests/IItRequestsWebPartProps.ts** и замените его содержимое на следующий код:

    ```typescript
    export interface IItRequestsWebPartProps {
    listName: string;
    }
    ```

3. Обновите метки отображения для свойства **listName**. Откройте файл **./src/webparts/itRequests/loc/mystrings.d.ts** и замените его содержимое на следующее:

    ```typescript
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

4. Откройте файл **./src/webparts/itRequests/loc/en-us.js** и измените его содержимое на следующее:

    ```js
    define([], function() {
    return {
        "PropertyPaneDescription": "IT Requests settings",
        "BasicGroupName": "Data",
        "ListNameFieldLabel": "List name"
    }
    });
    ```

5. Обновите веб-часть, чтобы использовалось новое свойство. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените код метода **getPropertyPaneConfiguration** на следующий:

    ```typescript
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

Изначально имя списка, из которого загружаются данные, внедрялось в запрос REST. Теперь, когда пользователи могут настраивать это имя, указанное значение следует внедрять в запрос REST перед загрузкой данных. Это проще всего сделать, переместив содержимое файла **script.js** в основной файл веб-части.

1. Откройте в редакторе кода файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените метод **render** на следующий код:

    ```typescript
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

2. Вместо того чтобы ссылаться на код из файла **script.js**, мы поместим все его содержимое в метод **render** веб-части. Теперь в строке 40 запроса REST можно заменить фиксированное имя списка на значение свойства **listName**, в котором хранится заданное пользователем имя списка. Прежде чем использовать это значение, необходимо применить к нему функцию **escape** из lodash, чтобы запретить внедрение скриптов.

    На этом этапе значительная часть кода все еще написана на обычном JavaScript. Чтобы во время сборки не возникали проблемы с переменной jQuery **$**, необходимо указать для нее тип **any** в строке 18. Позже, при преобразовании кода в TypeScript, следует заменить ее на подходящее определение типа.

    Так как мы только что переместили содержимое файла **script.js** в основной файл веб-части, файл **script.js** больше не требуется. Его можно удалить из проекта.

3. Чтобы проверить работу веб-части, выполните в командной строке следующую команду:

    ```sh
    gulp serve --nobrowser
    ```

4. Перейдите к размещенной рабочей области и добавьте веб-часть на холст. Откройте область свойств веб-части, укажите имя списка запросов о технической поддержке и нажмите кнопку **Apply** (Применить), чтобы подтвердить изменения. 

    Теперь в веб-части должны отображаться запросы о технической поддержке.

    ![Запросы о технической поддержке, загруженные из указанного списка и отображаемые в клиентской веб-части SharePoint Framework](../../../images/datatables-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a>Преобразование обычного кода JavaScript в TypeScript

Использование TypeScript вместо обычного JavaScript обеспечивает ряд преимуществ. Обслуживание и рефакторинг кода выполнять удобнее, если используется TypeScript. Кроме того, в таком коде можно раньше обнаруживать ошибки. Ниже описано, как преобразовать первоначальный код JavaScript в TypeScript.

### <a name="add-type-definitions-for-used-libraries"></a>Добавление определений типов для используемых библиотек

Для надлежащей работы TypeScript необходимы определения типов для различных библиотек, используемых в проекте. Определения типов часто распространяются в виде пакетов npm в пространстве имен @types.

1. Чтобы установить определения типов для jQuery и DataTables, выполните в командной строке следующую команду:

    ```sh
    npm install --save-dev @types/jquery @types/jquery.datatables
    ```

    Определения типов для Moment.js доступны в пакете Moment.js. Мы загружаем библиотеку Moment.js с URL-адреса, но для использования ее определений типов все равно необходимо установить пакет Moment.js в проекте.

2. Установите пакет Moment.js, выполнив в командной строке следующую команду:

    ```sh
    npm install --save moment
    ```

### <a name="update-package-references"></a>Обновление ссылок на пакеты

Чтобы использовать типы из установленных определений, необходимо изменить ссылки на библиотеки. 

1. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и замените оператор `import 'jquery';` на следующий код:

    ```typescript
    import * as $ from 'jquery';
    ```

2. Определив **$** как jQuery, вы можете удалить добавленное ранее локальное определение **$**:

    ```typescript
    var $: any = (window as any).$;
    ```

3. Так как DataTables представляет собой подключаемый модуль jQuery, присоединяющийся к jQuery, определение его типа невозможно загрузить напрямую. Вместо это необходимо добавить его в список глобально загружаемых типов. Откройте в редакторе кода файл **./tsconfig.json** и добавьте в массив **types** элемент **jquery.datatables**:

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

1. Определите интерфейс для сведений, касающихся запросов о технической поддержке, получаемых из списка SharePoint. В редакторе кода откройте файл **./src/webparts/itRequests/ItRequestsWebPart.ts** и непосредственно над классом веб-части добавьте следующий фрагмент кода:

    ```typescript
    interface IRequestItem {
    ID: number;
    BusinessUnit: string;
    Category: string;
    Status: string;
    DueDate: string;
    AssignedTo: { Title: string; };
    }
    ```

2. Затем в классе веб-части замените метод **render** на следующий код:

    ```typescript
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

3. Обратите внимание на то, что теперь запрос AJAX на получение данных из списка SharePoint является типизированным и позволяет ссылаться на правильные свойства при передаче их в массив в модуле DataTables. Структура данных, используемая модулем DataTables для представления строки в таблице, является массивом смешанных типов, поэтому для простоты она была определена как **any[]**. Использовать тип **any** в этом контексте допустимо, так как данные, возвращаемые в свойстве **dataSrc**, используются только в модуле DataTables.

    Обновляя метод **render**, мы также внесли еще два изменения. По-первых, мы удалили из таблицы атрибут **id**. Это позволяет добавить на страницу несколько экземпляров одной и той же веб-части. Кроме того, мы удалили ссылку на функцию `$(document).ready()`. Это не обязательно, так как модель DOM элемента, в котором отображается таблица данных, задается до кода инициализации модуля DataTables.

### <a name="update-the-momentjs-datatables-plugin-to-typescript"></a>Преобразование подключаемого модуля Moment.js для DataTables в TypeScript

Последний фрагмент решения, который необходимо преобразовать в TypeScript, — подключаемый модуль Moment.js для DataTables. 

1. Замените имя файла **./src/webparts/itRequests/moment-plugin.js** на **./src/webparts/itRequests/moment-plugin.ts**, чтобы его обрабатывал компилятор TypeScript. 

2. Откройте файл **moment-plugin.ts** в редакторе кода и замените его содержимое на следующий код:

    ```typescript
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

3. Для начала мы загружаем ссылки на jQuery и Moment.js, чтобы сообщить коду TypeScript, на что указывают соответствующие переменные. Затем мы определяем функцию подключаемого модуля. Как правило, в TypeScript для функций используется стрелочная нотация (`=>`). Однако в данном случае, так как требуется доступ к свойству **arguments**, необходимо использовать обычное определение функции. Чтобы tslint не выдавал предупреждение о том, что стрелочная нотация не используется, вы можете явно отключить правило **no-function-expression** для определения функции.

4. Чтобы убедиться, что все работает должным образом, выполните в командной строке следующую команду:

    ```sh
    gulp serve --nobrowser
```

5. Перейдите к размещенной рабочей области и добавьте веб-часть на холст. Визуально ничего не изменилось, но новая кодовая база использует TypeScript и соответствующие определения типов, что упрощает обслуживание решения.
