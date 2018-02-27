---
title: "Перенос решения с jQuery и FullCalendar, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework"
description: "Узнайте, как перенести модификацию SharePoint с использованием модуля FullCalendar, созданную в веб-части редактора скриптов, на платформу SharePoint Framework."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 313fd63a223d0fb2d7913f18bafab70b2159ab9f
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="migrate-jquery-and-fullcalendar-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a>Перенос решения с jQuery и FullCalendar, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework

При создании решений SharePoint разработчики часто используют подключаемый модуль [FullCalendar](https://fullcalendar.io) для jQuery, чтобы отображать данные в представлении календаря. FullCalendar — отличная альтернатива стандартному представлению календаря SharePoint, так как с помощью этого модуля можно отображать данные из нескольких списков календарей, из других списков и даже из расположений за пределами SharePoint. В этой статье показано, как перенести модификацию SharePoint с FullCalendar, созданную в веб-части редактора скриптов, на платформу SharePoint Framework.

## <a name="list-of-tasks-displayed-as-a-calendar-built-using-the-script-editor-web-part"></a>Список задач, отображаемый в виде календаря, созданного с помощью веб-части редактора скриптов

Чтобы проиллюстрировать перенос модификации SharePoint с использованием FullCalendar на платформу SharePoint Framework, мы будем использовать приведенное ниже решение, которое показывает представление календаря с задачами, полученными из списка SharePoint.

![Представление календаря с задачами, отображаемое на странице SharePoint](../../../images/fullcalendar-sewp.png)

Решение создано с помощью стандартной веб-части редактора скриптов SharePoint. Ниже представлен код, используемый модификацией.

```html
<script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/moment.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.js"></script>
<link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
<div id="calendar"></div>

<script>
  var PATH_TO_DISPFORM = _spPageContextInfo.webAbsoluteUrl + "/Lists/Tasks/DispForm.aspx";
  var TASK_LIST = "Tasks";
  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];

  displayTasks();

  function displayTasks() {
    $('#calendar').fullCalendar('destroy');
    $('#calendar').fullCalendar({
      weekends: false,
      header: {
        left: 'prev,next today',
        center: 'title',
        right: 'month,basicWeek,basicDay'
      },
      displayEventTime: false,
      // open up the display form when a user clicks on an event
      eventClick: function (calEvent, jsEvent, view) {
        window.location = PATH_TO_DISPFORM + "?ID=" + calEvent.id;
      },
      editable: true,
      timezone: "UTC",
      droppable: true, // this allows things to be dropped onto the calendar
      // update the end date when a user drags and drops an event 
      eventDrop: function (event, delta, revertFunc) {
        updateTask(event.id, event.start, event.end);
      },
      // put the events on the calendar 
      events: function (start, end, timezone, callback) {
        var startDate = start.format('YYYY-MM-DD');
        var endDate = end.format('YYYY-MM-DD');

        var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
$filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";

        $.ajax({
          url: _spPageContextInfo.webAbsoluteUrl + restQuery,
          type: "GET",
          dataType: "json",
          headers: {
            Accept: "application/json;odata=nometadata"
          }
        })
          .done(function (data, textStatus, jqXHR) {
            var personColors = {};
            var colorNo = 0;

            var events = data.value.map(function (task) {
              var assignedTo = task.AssignedTo.map(function (person) {
                return person.Title;
              }).join(', ');

              var color = personColors[assignedTo];
              if (!color) {
                color = COLORS[colorNo++];
                personColors[assignedTo] = color;
              }
              if (colorNo >= COLORS.length) {
                colorNo = 0;
              }

              return {
                title: task.Title + " - " + assignedTo,
                id: task.ID,
                color: color, // specify the background color and border color can also create a class and use className parameter. 
                start: moment.utc(task.StartDate).add("1", "days"),
                end: moment.utc(task.DueDate).add("1", "days") // add one day to end date so that calendar properly shows event ending on that day
              };
            });

            callback(events);
          });
      }
    });
  }

  function updateTask(id, startDate, dueDate) {
    // subtract the previously added day to the date to store correct date
    var sDate = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      startDate.format("hh:mm") + ":00Z";
    if (!dueDate) {
      dueDate = startDate;
    }
    var dDate = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      dueDate.format("hh:mm") + ":00Z";

    $.ajax({
      url: _spPageContextInfo.webAbsoluteUrl + '/_api/contextinfo',
      type: 'POST',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    })
      .then(function (data, textStatus, jqXHR) {
        return $.ajax({
          url: _spPageContextInfo.webAbsoluteUrl +
          "/_api/Web/Lists/getByTitle('" + TASK_LIST + "')/Items(" + id + ")",
          type: 'POST',
          data: JSON.stringify({
            StartDate: sDate,
            DueDate: dDate,
          }),
          headers: {
            Accept: "application/json;odata=nometadata",
            "Content-Type": "application/json;odata=nometadata",
            "X-RequestDigest": data.FormDigestValue,
            "IF-MATCH": "*",
            "X-Http-Method": "PATCH"
          }
        });
      })
      .done(function (data, textStatus, jqXHR) {
        alert("Update Successful");
      })
      .fail(function (jqXHR, textStatus, errorThrown) {
        alert("Update Failed");
      })
      .always(function () {
        displayTasks();
      });
  }
</script>
```

> [!NOTE] 
> Это решение основано на работе Mark Rackley, специалиста MVP по серверам и службам Office, а также директора по стратегическим вопросам в компании PAIT Group. Дополнительные сведения об исходном решении см. в статье [Создание пользовательских календарей в SharePoint с помощью FullCalendar.io](http://www.markrackley.net/2017/06/07/using-fullcalendar-io-to-create-custom-calendars-in-sharepoint/).

Для начала модификация загружает свои библиотеки: jQuery, Moment.js и FullCalendar (строки 1–4). 

Затем задается тег div для добавления создаваемого представления календаря (строка 5). 

После этого определяются две функции: **displayTasks** (отображает задачи в представлении календаря) и **updateTask** (вызывается при перетаскивании задачи для переноса ее на другую дату и обновляет даты в соответствующем элементе списка). В каждой функции определяется собственный запрос REST, который затем используется для связи с REST API списков SharePoint, чтобы получать или обновлять элементы списков.

Используя подключаемый модуль FullCalendar для jQuery, можно с минимальными усилиями создавать функциональные решения, предоставляющие пользователям такие возможности, как пометка событий разными цветами и упорядочивание событий путем перетаскивания.

![Перетаскивание событий в модуле FullCalendar для перепланировки задач](../../../images/fullcalendar-sewp-draganddrop.png)

## <a name="migrate-the-tasks-calendar-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a>Перенос решения для просмотра календаря задач из веб-части редактора скриптов на платформу SharePoint Framework

> [!NOTE] 
> Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment.md) для создания решений на платформе SharePoint Framework.

Преобразование модификации на основе веб-части редактора скриптов для SharePoint Framework обеспечивает ряд преимуществ, таких как повышенное удобство настройки и централизованное управление решением. Ниже представлено пошаговое описание переноса решения на платформу SharePoint Framework. 

Для начала необходимо перенести решение на платформу SharePoint Framework, внеся как можно меньше изменений в первоначальный код. Затем следует преобразовать код решения в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов во время разработки, и заменить часть кода на API SharePoint Framework, чтобы в полной мере воспользоваться возможностями платформы и еще больше упростить решение.

> [!NOTE] 
> Исходный код проекта на разных этапах миграции представлен в статье [Руководство. Перенос решения с jQuery и FullCalendar, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-fullcalendar).

### <a name="create-new-sharepoint-framework-project"></a>Создание проекта SharePoint Framework

1. Для начала создайте папку проекта:

  ```sh
  md fullcalendar-taskscalendar
  ```

2. Перейдите в папку проекта:

  ```sh
  cd fullcalendar-taskscalendar
  ```

3. В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы выполнить скаффолдинг нового проекта на платформе SharePoint Framework:

  ```sh
  yo @microsoft/sharepoint
  ```

4. Определите значения следующим образом:
  - имя решения — **fullcalendar-taskscalendar**;
  - расположение файлов — **Use the current folder** (Использовать текущую папку);
  - создаваемый клиентский компонент — **WebPart**;
  - имя веб-части — **Tasks calendar**;
  - описание веб-части **Shows tasks in the calendar view** (Показывает задачи в представлении календаря);
  - отправная точка создания веб-части — **No javaScript web framework** (Без платформы JavaScript).

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/fullcalendar-yeoman.png)

5. По завершении скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:

  ```sh
  npm shrinkwrap
  ```

6. Откройте папку проекта в редакторе кода. В этом руководстве используется Visual Studio Code.

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/fullcalendar-vscode.png)

### <a name="load-javascript-libraries"></a>Загрузка библиотек JavaScript

Как и в исходном решении, созданном с помощью веб-части редактора скриптов, сначала необходимо загрузить библиотеки JavaScript, необходимые решению. Как правило, в SharePoint Framework этот процесс состоит из двух этапов: указания URL-адреса, с которого загружаются библиотеки, и обращения к библиотеке в коде.

1. Укажите URL-адрес, с которого следует загружать библиотеки. В редакторе кода откройте файл **./config/config.json** и замените раздел **externals** на следующий код:

  ```json
  {
    "externals": {
      "jquery": "https://code.jquery.com/jquery-1.11.1.min.js",
      "moment": "https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/moment.min.js",
      "fullcalendar": "https://cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.js"
    }
  }
  ```

2. Откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и после последнего оператора **import** добавьте следующий код:

  ```typescript
  import 'jquery';
  import 'moment';
  import 'fullcalendar';
  ```

### <a name="define-container-div"></a>Определение div контейнера

Как и в исходном решении, далее необходимо определить, где будет отображаться календарь. 

В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените код метода **render** на следующий:

```typescript
  export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.tasksCalendar}">
          <link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
          <div id="calendar"></div>
        </div>`;
    }
    // ...
  }
```

### <a name="initiate-fullcalendar-and-load-data"></a>Инициализация модуля FullCalendar и загрузка данных

Последний этап — добавление кода, инициализирующего подключаемый модуль FullCalendar для jQuery и загружающего данные из SharePoint. 

1.  В папке **./src/webparts/tasksCalendar** создайте файл с именем **script.js** и вставьте следующий код:

  ```js
  var moment = require('moment');

  var PATH_TO_DISPFORM = window.webAbsoluteUrl + "/Lists/Tasks/DispForm.aspx";
  var TASK_LIST = "Tasks";
  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];

  displayTasks();

  function displayTasks() {
    $('#calendar').fullCalendar('destroy');
    $('#calendar').fullCalendar({
      weekends: false,
      header: {
        left: 'prev,next today',
        center: 'title',
        right: 'month,basicWeek,basicDay'
      },
      displayEventTime: false,
      // open up the display form when a user clicks on an event
      eventClick: function (calEvent, jsEvent, view) {
        window.location = PATH_TO_DISPFORM + "?ID=" + calEvent.id;
      },
      editable: true,
      timezone: "UTC",
      droppable: true, // this allows things to be dropped onto the calendar
      // update the end date when a user drags and drops an event 
      eventDrop: function (event, delta, revertFunc) {
        updateTask(event.id, event.start, event.end);
      },
      // put the events on the calendar 
      events: function (start, end, timezone, callback) {
        var startDate = start.format('YYYY-MM-DD');
        var endDate = end.format('YYYY-MM-DD');

        var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";

        $.ajax({
          url: window.webAbsoluteUrl + restQuery,
          type: "GET",
          dataType: "json",
          headers: {
            Accept: "application/json;odata=nometadata"
          }
        })
          .done(function (data, textStatus, jqXHR) {
            var personColors = {};
            var colorNo = 0;

            var events = data.value.map(function (task) {
              var assignedTo = task.AssignedTo.map(function (person) {
                return person.Title;
              }).join(', ');

              var color = personColors[assignedTo];
              if (!color) {
                color = COLORS[colorNo++];
                personColors[assignedTo] = color;
              }
              if (colorNo >= COLORS.length) {
                colorNo = 0;
              }

              return {
                title: task.Title + " - " + assignedTo,
                id: task.ID,
                color: color, // specify the background color and border color can also create a class and use className parameter. 
                start: moment.utc(task.StartDate).add("1", "days"),
                end: moment.utc(task.DueDate).add("1", "days") // add one day to end date so that calendar properly shows event ending on that day
              };
            });

            callback(events);
          });
      }
    });
  }

  function updateTask(id, startDate, dueDate) {
    // subtract the previously added day to the date to store correct date
    var sDate = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      startDate.format("hh:mm") + ":00Z";
    if (!dueDate) {
      dueDate = startDate;
    }
    var dDate = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
      dueDate.format("hh:mm") + ":00Z";

    $.ajax({
      url: window.webAbsoluteUrl + '/_api/contextinfo',
      type: 'POST',
      headers: {
        'Accept': 'application/json;odata=nometadata'
      }
    })
      .then(function (data, textStatus, jqXHR) {
        return $.ajax({
          url: window.webAbsoluteUrl +
          "/_api/Web/Lists/getByTitle('" + TASK_LIST + "')/Items(" + id + ")",
          type: 'POST',
          data: JSON.stringify({
            StartDate: sDate,
            DueDate: dDate,
          }),
          headers: {
            Accept: "application/json;odata=nometadata",
            "Content-Type": "application/json;odata=nometadata",
            "X-RequestDigest": data.FormDigestValue,
            "IF-MATCH": "*",
            "X-Http-Method": "PATCH"
          }
        });
      })
      .done(function (data, textStatus, jqXHR) {
        alert("Update Successful");
      })
      .fail(function (jqXHR, textStatus, errorThrown) {
        alert("Update Failed");
      })
      .always(function () {
        displayTasks();
      });
  }
  ```

  Он практически идентичен первоначальному коду модификации на основе веб-части редактора скриптов. Единственное отличие заключается в том, что первоначальный код получал URL-адрес текущего сайта из глобальной переменной **\_spPageContextInfo**, которую задает SharePoint (строки 8, 45, 96 и 104), а на платформе SharePoint Framework используется пользовательская переменная, которую необходимо задать в веб-части. 
  
  Клиентские веб-части SharePoint Framework можно использовать как на классических, так и на современных страницах. Переменная **_spPageContextInfo** используется на классических страницах, но недоступна на современных, поэтому не следует рассчитывать на нее. Рекомендуем использовать настраиваемое свойство, которым можно управлять самостоятельно.

2. Чтобы сослаться на этот файл в веб-части, откройте в редакторе кода файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените метод **render** на следующий код:

  ```typescript
  export default class ItRequestsWebPart extends BaseClientSideWebPart<IItRequestsWebPartProps> {
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.tasksCalendar}">
          <link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
          <div id="calendar"></div>
        </div>`;

      (window as any).webAbsoluteUrl = this.context.pageContext.web.absoluteUrl;
      require('./script');
    }
    // ...
  }
  ```

3. Проверьте работу веб-части, выполнив в командной строке следующую команду:

  ```sh
  gulp serve --nobrowser
  ```

  Так как веб-часть загружает свои данные из SharePoint, ее необходимо тестировать с помощью размещенной рабочей области SharePoint Framework. 
  
4. Перейдите по адресу `https://yourtenant.sharepoint.com/_layouts/workbench.aspx` и добавьте веб-часть на холст. Теперь задачи должны отображаться в представлении календаря с помощью подключаемого модуля FullCalendar для jQuery.

  ![Задачи, отображаемые в представлении календаря в клиентской веб-части SharePoint Framework](../../../images/fullcalendar-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a>Добавление возможности настраивать веб-часть с помощью ее свойств

На предыдущих этапах мы перенесли решение для просмотра календаря задач из веб-части редактора скриптов на платформу SharePoint Framework. Решение уже работает надлежащим образом, но не использует преимущества платформы SharePoint Framework. Имя списка, из которого загружаются задачи, включено в код, представляющий собой обычный JavaScript, который хуже поддается рефакторингу, чем TypeScript. 

В приведенных ниже разделах описано, как расширить имеющееся решение, чтобы пользователи могли указывать имя списка, из которого будут загружаться данные. Позже мы преобразуем код в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов.

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a>Определение свойства веб-части для хранения имени списка

1. Определите свойство веб-части для хранения имени списка, из которого будут загружаться задачи. В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.manifest.json**, замените имя заданного по умолчанию свойства **description** на **listName** и удалите его значение.

  ![Свойство listName манифеста веб-части, выделенное в Visual Studio Code](../../../images/fullcalendar-spfx-listname-property.png)

2. Обновите интерфейс свойств веб-части, чтобы применить изменения манифеста. В редакторе кода откройте файл **./src/webparts/tasksCalendar/ITasksCalendarWebPartProps.ts** и замените его содержимое на следующий код:

  ```typescript
  export interface ITasksCalendarWebPartProps {
    listName: string;
  }
  ```

3. Обновите метки отображения для свойства **listName**. Откройте файл **./src/webparts/tasksCalendar/loc/mystrings.d.ts** и замените его содержимое на следующее:

  ```typescript
  declare interface ITasksCalendarStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListNameFieldLabel: string;
  }

  declare module 'tasksCalendarStrings' {
    const strings: ITasksCalendarStrings;
    export = strings;
  }
  ```

4. Откройте файл **./src/webparts/tasksCalendar/loc/en-us.js** и замените его содержимое на следующее:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Tasks calendar settings",
      "BasicGroupName": "Data",
      "ListNameFieldLabel": "List name"
    }
  });
  ```

5. Обновите веб-часть, чтобы использовалось новое свойство. В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените код метода **getPropertyPaneConfiguration** на следующий:

  ```typescript
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
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

Изначально имя списка, из которого загружаются данные, внедрялось в запросы REST. Теперь, когда пользователи могут настраивать это имя, указанное значение следует внедрять в запросы REST перед их выполнением. Это проще всего сделать, переместив содержимое файла **script.js** в основной файл веб-части.

1. В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**.

2. Измените оператор импорта для загрузки необходимых библиотек:

  ```typescript
  var $: any = require('jquery');
  var moment: any = require('moment');

  import 'fullcalendar';

  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];
  ```

  В коде, который мы будем использовать позже, есть ссылка на библиотеку Moment.js, поэтому коду TypeScript должно быть известно ее имя, иначе сборка проекта завершится ошибкой. То же относится и к jQuery. Так как FullCalendar представляет собой подключаемый модуль для jQuery, присоединяющийся к объекту jQuery, его можно импортировать так же, как и раньше.

  Последняя часть включает копирование списка цветов для пометки различных событий.

3. Скопируйте функции **displayTasks** и **updateTask** из файла **script.js** и вставьте их в класс **TasksCalendarWebPart**, как показано ниже.

  ```typescript
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    // ...

    private displayTasks() {
      $('#calendar').fullCalendar('destroy');
      $('#calendar').fullCalendar({
        weekends: false,
        header: {
          left: 'prev,next today',
          center: 'title',
          right: 'month,basicWeek,basicDay'
        },
        displayEventTime: false,
        // open up the display form when a user clicks on an event
        eventClick: (calEvent, jsEvent, view) => {
          (window as any).location = this.context.pageContext.web.absoluteUrl +
            "/Lists/" + escape(this.properties.listName) + "/DispForm.aspx?ID=" + calEvent.id;
        },
        editable: true,
        timezone: "UTC",
        droppable: true, // this allows things to be dropped onto the calendar
        // update the end date when a user drags and drops an event 
        eventDrop: (event, delta, revertFunc) => {
          this.updateTask(event.id, event.start, event.end);
        },
        // put the events on the calendar 
        events: (start, end, timezone, callback) => {
          var startDate = start.format('YYYY-MM-DD');
          var endDate = end.format('YYYY-MM-DD');

          var restQuery = "/_api/Web/Lists/GetByTitle('" + escape(this.properties.listName) + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";

          $.ajax({
            url: this.context.pageContext.web.absoluteUrl + restQuery,
            type: "GET",
            dataType: "json",
            headers: {
              Accept: "application/json;odata=nometadata"
            }
          })
            .done((data, textStatus, jqXHR) => {
              var personColors = {};
              var colorNo = 0;

              var events = data.value.map((task) => {
                var assignedTo = task.AssignedTo.map((person) => {
                  return person.Title;
                }).join(', ');

                var color = personColors[assignedTo];
                if (!color) {
                  color = COLORS[colorNo++];
                  personColors[assignedTo] = color;
                }
                if (colorNo >= COLORS.length) {
                  colorNo = 0;
                }

                return {
                  title: task.Title + " - " + assignedTo,
                  id: task.ID,
                  color: color, // specify the background color and border color can also create a class and use className parameter. 
                  start: moment.utc(task.StartDate).add("1", "days"),
                  end: moment.utc(task.DueDate).add("1", "days") // add one day to end date so that calendar properly shows event ending on that day
                };
              });

              callback(events);
            });
        }
      });
    }

    private updateTask(id, startDate, dueDate) {
      // subtract the previously added day to the date to store correct date
      var sDate = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        startDate.format("hh:mm") + ":00Z";
      if (!dueDate) {
        dueDate = startDate;
      }
      var dDate = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        dueDate.format("hh:mm") + ":00Z";

      $.ajax({
        url: this.context.pageContext.web.absoluteUrl + '/_api/contextinfo',
        type: 'POST',
        headers: {
          'Accept': 'application/json;odata=nometadata'
        }
      })
        .then((data, textStatus, jqXHR) => {
          return $.ajax({
            url: this.context.pageContext.web.absoluteUrl +
            "/_api/Web/Lists/getByTitle('" + escape(this.properties.listName) + "')/Items(" + id + ")",
            type: 'POST',
            data: JSON.stringify({
              StartDate: sDate,
              DueDate: dDate,
            }),
            headers: {
              Accept: "application/json;odata=nometadata",
              "Content-Type": "application/json;odata=nometadata",
              "X-RequestDigest": data.FormDigestValue,
              "IF-MATCH": "*",
              "X-Http-Method": "PATCH"
            }
          });
        })
        .done((data, textStatus, jqXHR) => {
          alert("Update Successful");
        })
        .fail((jqXHR, textStatus, errorThrown) => {
          alert("Update Failed");
        })
        .always(() => {
          this.displayTasks();
        });
    }

    // ...
  }
  ```

  <br/>

  По сравнению с предыдущим случаем в код вносится меньше изменений. Теперь обычные функции JavaScript преобразуются в методы TypeScript путем замены ключевого слова **function** на модификатор **private**. Это необходимо, чтобы можно было добавить их в класс **TaskCalendarWebPart**. Так как теперь оба метода находятся в том же файле, что и веб-часть, вы можете не определять глобальную переменную для хранения URL-адреса текущего сайта, а обращаться к нему непосредственно из контекста веб-части с помощью свойства `this.context.pageContext.web.absoluteUrl`. Кроме того, во всех запросах REST фиксированное имя списка заменяется на значение свойства **listName**, в котором хранится имя списка, заданное пользователем. Прежде чем использовать это значение, необходимо применить к нему функцию **escape** из lodash, чтобы запретить внедрение скриптов.

4. Напоследок измените метод **render**, чтобы он вызывал новый метод **displayTasks**:

  ```typescript
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    public render(): void {
      this.domElement.innerHTML = `
        <div class="${styles.tasksCalendar}">
          <link type="text/css" rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.css" />
          <div id="calendar"></div>
        </div>`;

      this.displayTasks();
    }
    // ...
  }
  ```

5. Так как мы только что переместили содержимое файла **script.js** в основной файл веб-части, файл **script.js** больше не требуется. Его можно удалить из проекта.

6. Чтобы проверить работу веб-части, выполните в командной строке следующую команду:

  ```sh
  gulp serve --nobrowser
  ```

7. Перейдите к размещенной рабочей области и добавьте веб-часть на холст. Откройте область свойств веб-части, укажите имя списка задач и нажмите кнопку **Apply** (Применить), чтобы подтвердить изменения. Задачи должны появиться в представлении календаря в веб-части.

  ![Задачи, загруженные из указанного списка и отображаемые в клиентской веб-части SharePoint Framework](../../../images/fullcalendar-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a>Преобразование обычного кода JavaScript в TypeScript

Использование TypeScript вместо обычного JavaScript обеспечивает ряд преимуществ. Обслуживание и рефакторинг кода выполнять удобнее, если используется TypeScript. Кроме того, в таком коде можно раньше обнаруживать ошибки. Ниже описано, как преобразовать первоначальный код JavaScript в TypeScript.

### <a name="add-type-definitions-for-used-libraries"></a>Добавление определений типов для используемых библиотек

Для надлежащей работы TypeScript необходимы определения типов для различных библиотек, используемых в проекте. Определения типов часто распространяются в виде пакетов npm в пространстве имен @types.

1. Установите определения типов для jQuery и FullCalendar, выполнив в командной строке следующую команду:

  ```sh
  npm install --save-dev @types/jquery@1 @types/fullcalendar
  ```

  Определения типов для Moment.js доступны в пакете Moment.js. Мы загружаем библиотеку Moment.js с URL-адреса, но для использования ее определений типов все равно необходимо установить пакет Moment.js в проекте.

2. Установите пакет Moment.js, выполнив в командной строке следующую команду:

  ```sh
  npm install --save moment
  ```

### <a name="update-package-references"></a>Обновление ссылок на пакеты

Чтобы использовать типы из установленных определений, необходимо изменить ссылки на библиотеки. 

В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените операторы импорта на следующий код:

```typescript
import * as $ from 'jquery';
import 'fullcalendar';
import * as moment from 'moment';
```

### <a name="update-main-web-part-files-to-typescript"></a>Преобразование основных файлов веб-части в TypeScript

Теперь, когда у нас есть определения типов для всех библиотек, установленных в проекте, можно приступить к преобразованию обычного кода JavaScript в TypeScript.

1. Определите интерфейс для задачи, получаемой из списка SharePoint. В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и непосредственно над классом веб-части добавьте следующий фрагмент кода:

  ```typescript
  interface ITask {
    ID: number;
    Title: string;
    StartDate: string;
    DueDate: string;
    AssignedTo: [{ Title: string }];
  }
  ```

2. В классе веб-части замените методы **displayTasks** и **updateTask** на следующий код:

  ```typescript
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    private readonly colors: string[] = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];

    // ...

    private displayTasks(): void {
      $('#calendar').fullCalendar('destroy');
      $('#calendar').fullCalendar({
        weekends: false,
        header: {
          left: 'prev,next today',
          center: 'title',
          right: 'month,basicWeek,basicDay'
        },
        displayEventTime: false,
        // open up the display form when a user clicks on an event
        eventClick: (calEvent: FC.EventObject, jsEvent: MouseEvent, view: FC.ViewObject): void => {
          (window as any).location = `${this.context.pageContext.web.absoluteUrl}\
  /Lists/${escape(this.properties.listName)}/DispForm.aspx?ID=${calEvent.id}`;
        },
        editable: true,
        timezone: "UTC",
        droppable: true, // this allows things to be dropped onto the calendar
        // update the end date when a user drags and drops an event 
        eventDrop: (event: FC.EventObject, delta: moment.Duration, revertFunc: Function): void => {
          this.updateTask(event.id, <moment.Moment>event.start, <moment.Moment>event.end);
        },
        // put the events on the calendar 
        events: (start: moment.Moment, end: moment.Moment, timezone: string, callback: Function): void => {
          const startDate: string = start.format('YYYY-MM-DD');
          const endDate: string = end.format('YYYY-MM-DD');

          const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;

          $.ajax({
            url: this.context.pageContext.web.absoluteUrl + restQuery,
            type: "GET",
            dataType: "json",
            headers: {
              Accept: "application/json;odata=nometadata"
            }
          })
            .done((data: { value: ITask[] }, textStatus: string, jqXHR: JQueryXHR): void => {
              let personColors: { [person: string]: string; } = {};
              let colorNo: number = 0;

              const events: FC.EventObject[] = data.value.map((task: ITask): FC.EventObject => {
                const assignedTo: string = task.AssignedTo.map((person: { Title: string }): string => {
                  return person.Title;
                }).join(', ');

                let color: string = personColors[assignedTo];
                if (!color) {
                  color = this.colors[colorNo++];
                  personColors[assignedTo] = color;
                }
                if (colorNo >= this.colors.length) {
                  colorNo = 0;
                }

                return {
                  title: `${task.Title} - ${assignedTo}`,
                  id: task.ID,
                  // specify the background color and border color can also create a class and use className parameter
                  color: color,
                  start: moment.utc(task.StartDate).add("1", "days"),
                  // add one day to end date so that calendar properly shows event ending on that day
                  end: moment.utc(task.DueDate).add("1", "days")
                };
              });

              callback(events);
            });
        }
      });
    }

    private updateTask(id: number, startDate: moment.Moment, dueDate: moment.Moment): void {
      // subtract the previously added day to the date to store correct date
      const sDate: string = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        startDate.format("hh:mm") + ":00Z";
      if (!dueDate) {
        dueDate = startDate;
      }
      const dDate: string = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        dueDate.format("hh:mm") + ":00Z";

      $.ajax({
        url: this.context.pageContext.web.absoluteUrl + '/_api/contextinfo',
        type: 'POST',
        headers: {
          'Accept': 'application/json;odata=nometadata'
        }
      })
        .then((data: { FormDigestValue: string }, textStatus: string, jqXHR: JQueryXHR): JQueryXHR => {
          return $.ajax({
            url: `${this.context.pageContext.web.absoluteUrl}\
  /_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`,
            type: 'POST',
            data: JSON.stringify({
              StartDate: sDate,
              DueDate: dDate,
            }),
            headers: {
              Accept: "application/json;odata=nometadata",
              "Content-Type": "application/json;odata=nometadata",
              "X-RequestDigest": data.FormDigestValue,
              "IF-MATCH": "*",
              "X-Http-Method": "PATCH"
            }
          });
        })
        .done((data: {}, textStatus: string, jqXHR: JQueryXHR): void => {
          alert("Update Successful");
        })
        .fail((jqXHR: JQueryXHR, textStatus: string, errorThrown: string): void => {
          alert("Update Failed");
        })
        .always((): void => {
          this.displayTasks();
        });
    }

    // ...
  }
  ```

  <br/>

  Первое и самое очевидное изменение при преобразовании обычного кода JavaScript в TypeScript — это явные типы. Использовать их не обязательно, но они четко дают понять, данные какого типа ожидаются в тех или иных полях. TypeScript мгновенно определяет любое отклонение от заданного соглашения, помогая вам находить возможные проблемы как можно раньше в процессе разработки. Это особенно полезно при работе с откликами AJAX и их данными.

  Еще одно изменение, которое вы уже могли заметить, — строковая интерполяция TypeScript. Она упрощает динамическое составление строк и делает код более удобочитаемым. 
  
  Обычный код JavaScript:

  ```js
  var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";
  ```

  Сравните его со следующим кодом:

  ```typescript
  const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;
  ```

  Еще одно преимущество строковой интерполяции TypeScript — отсутствие необходимости отменять кавычки, что также упрощает запросы REST.

3. Чтобы убедиться, что все работает должным образом, выполните в командной строке следующую команду:

  ```sh
  gulp serve --nobrowser
  ```

4. Перейдите к размещенной рабочей области и добавьте веб-часть на холст. Визуально ничего не изменилось, но новая кодовая база использует TypeScript и соответствующие определения типов, что упрощает обслуживание решения.

### <a name="replace-jquery-ajax-calls-with-sharepoint-framework-api"></a>Замена вызовов AJAX jQuery на API SharePoint Framework

В данный момент решение использует вызовы AJAX jQuery для связи с REST API SharePoint. Для обычных запросов GET так же удобно использовать API AJAX jQuery, как и SPHttpClient на платформе SharePoint Framework. Разница становится заметна при выполнении запросов POST, таких как следующий запрос на обновление события:

```typescript
$.ajax({
  url: this.context.pageContext.web.absoluteUrl + '/_api/contextinfo',
  type: 'POST',
  headers: {
    'Accept': 'application/json;odata=nometadata'
  }
})
  .then((data: { FormDigestValue: string }, textStatus: string, jqXHR: JQueryXHR): JQueryXHR => {
    return $.ajax({
      url: `${this.context.pageContext.web.absoluteUrl}\
/_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`,
      type: 'POST',
      data: JSON.stringify({
        StartDate: sDate,
        DueDate: dDate,
      }),
      headers: {
        Accept: "application/json;odata=nometadata",
        "Content-Type": "application/json;odata=nometadata",
        "X-RequestDigest": data.FormDigestValue,
        "IF-MATCH": "*",
        "X-Http-Method": "PATCH"
      }
    });
  })
  .done((data: {}, textStatus: string, jqXHR: JQueryXHR): void => {
    alert("Update Successful");
  })
  // ...
```

Так как нам требуется обновить элемент списка, необходимо предоставить среде SharePoint действительный токен дайджеста запроса. Он доступен на классических страницах, но действителен в течение 3 минут, поэтому всегда предпочтительнее получить действительный токен самостоятельно, прежде чем выполнять обновление. Получив дайджест запроса, следует добавить его к заголовкам запроса на обновление. В противном случае запрос не будет выполнен.

Класс SPHttpClient платформы SharePoint Framework упрощает связь с SharePoint, автоматически определяя запросы POST, которым требуется действительный токен дайджеста. Для таких запросов SPHttpClient автоматически получает токен из SharePoint и добавляет его к запросу. Для сравнения, аналогичный запрос, отправленный с использованием SPHttpClient, будет выглядеть так:

```typescript
this.context.spHttpClient.post(`${this.context.pageContext.web.absoluteUrl}\
/_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`, SPHttpClient.configurations.v1, {
  body: JSON.stringify({
    StartDate: sDate,
    DueDate: dDate,
  }),
  headers: {
    Accept: "application/json;odata=nometadata",
    "Content-Type": "application/json;odata=nometadata",
    "IF-MATCH": "*",
    "X-Http-Method": "PATCH"
  }
})
.then((response: SPHttpClientResponse): void => {
  // ...
});
```

<br/>

1. Чтобы заменить исходные вызовы AJAX jQuery на API SPHttpClient платформы SharePoint Framework, в редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**. В список импорта добавьте следующее:

  ```typescript
  import { SPHttpClient, SPHttpClientResponse } from '@microsoft/sp-http';
  ```

2. В классе **TasksCalendarWebPart** замените методы **displayTasks** и **updateTask** на следующий код:

  ```typescript
  export default class TasksCalendarWebPart extends BaseClientSideWebPart<ITasksCalendarWebPartProps> {
    // ...

    private displayTasks(): void {
      $('#calendar').fullCalendar('destroy');
      $('#calendar').fullCalendar({
        weekends: false,
        header: {
          left: 'prev,next today',
          center: 'title',
          right: 'month,basicWeek,basicDay'
        },
        displayEventTime: false,
        // open up the display form when a user clicks on an event
        eventClick: (calEvent: FC.EventObject, jsEvent: MouseEvent, view: FC.ViewObject): void => {
          (window as any).location = `${this.context.pageContext.web.absoluteUrl}\
  /Lists/${escape(this.properties.listName)}/DispForm.aspx?ID=${calEvent.id}`;
        },
        editable: true,
        timezone: "UTC",
        droppable: true, // this allows things to be dropped onto the calendar
        // update the end date when a user drags and drops an event 
        eventDrop: (event: FC.EventObject, delta: moment.Duration, revertFunc: Function): void => {
          this.updateTask(event.id, <moment.Moment>event.start, <moment.Moment>event.end);
        },
        // put the events on the calendar 
        events: (start: moment.Moment, end: moment.Moment, timezone: string, callback: Function): void => {
          const startDate: string = start.format('YYYY-MM-DD');
          const endDate: string = end.format('YYYY-MM-DD');

          const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;

          this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + restQuery, SPHttpClient.configurations.v1, {
            headers: {
              'Accept': "application/json;odata.metadata=none"
            }
          })
            .then((response: SPHttpClientResponse): Promise<{ value: ITask[] }> => {
              return response.json();
            })
            .then((data: { value: ITask[] }): void => {
              let personColors: { [person: string]: string; } = {};
              let colorNo: number = 0;

              const events: FC.EventObject[] = data.value.map((task: ITask): FC.EventObject => {
                const assignedTo: string = task.AssignedTo.map((person: { Title: string }): string => {
                  return person.Title;
                }).join(', ');

                let color: string = personColors[assignedTo];
                if (!color) {
                  color = this.colors[colorNo++];
                  personColors[assignedTo] = color;
                }
                if (colorNo >= this.colors.length) {
                  colorNo = 0;
                }

                return {
                  title: `${task.Title} - ${assignedTo}`,
                  id: task.ID,
                  // specify the background color and border color can also create a class and use className paramter
                  color: color,
                  start: moment.utc(task.StartDate).add("1", "days"),
                  // add one day to end date so that calendar properly shows event ending on that day
                  end: moment.utc(task.DueDate).add("1", "days")
                };
              });

              callback(events);
            });
        }
      });
    }

    private updateTask(id: number, startDate: moment.Moment, dueDate: moment.Moment): void {
      // subtract the previously added day to the date to store correct date
      const sDate: string = moment.utc(startDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        startDate.format("hh:mm") + ":00Z";
      if (!dueDate) {
        dueDate = startDate;
      }
      const dDate: string = moment.utc(dueDate).add("-1", "days").format('YYYY-MM-DD') + "T" +
        dueDate.format("hh:mm") + ":00Z";

      this.context.spHttpClient.post(`${this.context.pageContext.web.absoluteUrl}\
  /_api/Web/Lists/getByTitle('${escape(this.properties.listName)}')/Items(${id})`, SPHttpClient.configurations.v1, {
          body: JSON.stringify({
            StartDate: sDate,
            DueDate: dDate,
          }),
          headers: {
            Accept: "application/json;odata=nometadata",
            "Content-Type": "application/json;odata=nometadata",
            "IF-MATCH": "*",
            "X-Http-Method": "PATCH"
          }
        })
        .then((response: SPHttpClientResponse): void => {
          if (response.ok) {
            alert("Update Successful");
          }
          else {
            alert("Update Failed");
          }

          this.displayTasks();
        });
    }

    // ...
  }
  ```

  <br/>

  > [!IMPORTANT] 
  > Если в откликах от REST API SharePoint запрещены метаданные, то при использовании класса SPHttpClient платформы SharePoint Framework необходимо убедиться, что для заголовка **Accept** используется значение `application/json;odata.metadata=none`, а не `application/json;odata=nometadata`. SPHttpClient использует OData 4.0, поэтому необходимо задать первое значение. Если использовать другое, при выполнении запроса будет возвращена ошибка **406 Not Acceptable**.

3. Чтобы убедиться, что все работает должным образом, выполните в командной строке следующую команду:

  ```sh
  gulp serve --nobrowser
  ```

4. Перейдите к размещенной рабочей области и добавьте веб-часть на холст. Внешне ничего не изменилось, но в новом коде используется SPHttpClient на платформе SharePoint Framework, что упрощает код и поддержку решения.
