---
title: "Перенос решения с jQuery и FullCalendar, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework"
description: "Узнайте, как перенести модификацию SharePoint с использованием модуля FullCalendar, созданную в веб-части редактора скриптов, на платформу SharePoint Framework."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 5127e9f8598ff087bdbc34f9f1e678226bd127da
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="migrate-jquery-and-fullcalendar-solution-built-using-script-editor-web-part-to-sharepoint-framework"></a><span data-ttu-id="43f8e-103">Перенос решения с jQuery и FullCalendar, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="43f8e-103">Migrate jQuery and FullCalendar solution built using Script Editor Web Part to SharePoint Framework</span></span>

<span data-ttu-id="43f8e-104">При создании решений SharePoint разработчики часто используют подключаемый модуль [FullCalendar](https://fullcalendar.io) для jQuery, чтобы отображать данные в представлении календаря.</span><span class="sxs-lookup"><span data-stu-id="43f8e-104">When building SharePoint solutions, SharePoint developers often use the [FullCalendar](https://fullcalendar.io) jQuery plug-in to display data in calendar view.</span></span> <span data-ttu-id="43f8e-105">FullCalendar — отличная альтернатива стандартному представлению календаря SharePoint, так как с помощью этого модуля можно отображать данные из нескольких списков календарей, из других списков и даже из расположений за пределами SharePoint.</span><span class="sxs-lookup"><span data-stu-id="43f8e-105">When building SharePoint solutions, SharePoint developers often use the FullCalendar jQuery plugin to display data in calendar view. FullCalendar is a great alternative to the standard SharePoint calendar view, as it allows you to render as calendar data from multiple calendar lists, data from non-calendar lists or even data from outside of SharePoint. This article illustrates how you would migrate a SharePoint customization using FullCalendar built with the Script Editor Web Part to the SharePoint Framework.</span></span> <span data-ttu-id="43f8e-106">В этой статье показано, как перенести модификацию SharePoint с FullCalendar, созданную в веб-части редактора скриптов, на платформу SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43f8e-106">This article illustrates how you would migrate a SharePoint customization by using FullCalendar built with the Script Editor Web Part to the SharePoint Framework.</span></span>

## <a name="list-of-tasks-displayed-as-a-calendar-built-using-the-script-editor-web-part"></a><span data-ttu-id="43f8e-107">Список задач, отображаемый в виде календаря, созданного с помощью веб-части редактора скриптов</span><span class="sxs-lookup"><span data-stu-id="43f8e-107">List of tasks displayed as a calendar built using the Script Editor Web Part</span></span>

<span data-ttu-id="43f8e-108">Чтобы проиллюстрировать перенос модификации SharePoint с использованием FullCalendar на платформу SharePoint Framework, мы будем использовать приведенное ниже решение, которое показывает представление календаря с задачами, полученными из списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="43f8e-108">To illustrate the process of migrating a SharePoint customization using FullCalendar to the SharePoint Framework you will use the following solution that shows a calendar view of tasks retrieved from a SharePoint list.</span></span>

![Представление календаря с задачами, отображаемое на странице SharePoint](../../../images/fullcalendar-sewp.png)

<span data-ttu-id="43f8e-p102">Решение создано с помощью стандартной веб-части редактора скриптов SharePoint. Ниже представлен код, используемый модификацией.</span><span class="sxs-lookup"><span data-stu-id="43f8e-p102">The solution is built using the standard SharePoint Script Editor Web Part. Following is the code used by the customization.</span></span>

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
> <span data-ttu-id="43f8e-112">Это решение основано на работе Mark Rackley, специалиста MVP по серверам и службам Office, а также директора по стратегическим вопросам в компании PAIT Group.</span><span class="sxs-lookup"><span data-stu-id="43f8e-112">This solution is based on the work of Mark Rackley, Office Servers and Services MVP and Chief Strategy Officer at PAIT Group. For more information about the original solution visit http://www.markrackley.net/2017/06/07/using-fullcalendar-io-to-create-custom-calendars-in-sharepoint/.</span></span> <span data-ttu-id="43f8e-113">Дополнительные сведения об исходном решении см. в статье [Создание пользовательских календарей в SharePoint с помощью FullCalendar.io](http://www.markrackley.net/2017/06/07/using-fullcalendar-io-to-create-custom-calendars-in-sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="43f8e-113">For more information about the original solution, see [Using FullCalendar.io to Create Custom Calendars in SharePoint](http://www.markrackley.net/2017/06/07/using-fullcalendar-io-to-create-custom-calendars-in-sharepoint/).</span></span>

<span data-ttu-id="43f8e-114">Для начала модификация загружает свои библиотеки: jQuery, Moment.js и FullCalendar (строки 1–4).</span><span class="sxs-lookup"><span data-stu-id="43f8e-114">First, the customization loads the libraries it uses: jQuery, Moment.js, and FullCalendar (lines 1-4).</span></span> 

<span data-ttu-id="43f8e-115">Затем задается тег div для добавления создаваемого представления календаря (строка 5).</span><span class="sxs-lookup"><span data-stu-id="43f8e-115">Next, it defines the div into which the generated calendar view is injected (line 5).</span></span> 

<span data-ttu-id="43f8e-116">После этого определяются две функции: **displayTasks** (отображает задачи в представлении календаря) и **updateTask** (вызывается при перетаскивании задачи для переноса ее на другую дату и обновляет даты в соответствующем элементе списка).</span><span class="sxs-lookup"><span data-stu-id="43f8e-116">It then defines two functions: **displayTasks**, used to display tasks in the calendar view, and **updateTask**, which is triggered after dragging and dropping a task to a different date and which updates the dates on the underlying list item.</span></span> <span data-ttu-id="43f8e-117">В каждой функции определяется собственный запрос REST, который затем используется для связи с REST API списков SharePoint, чтобы получать или обновлять элементы списков.</span><span class="sxs-lookup"><span data-stu-id="43f8e-117">Each function defines its own REST query, which is then used to communicate with the SharePoint List REST API to retrieve or update list items.</span></span>

<span data-ttu-id="43f8e-118">Используя подключаемый модуль FullCalendar для jQuery, можно с минимальными усилиями создавать функциональные решения, предоставляющие пользователям такие возможности, как пометка событий разными цветами и упорядочивание событий путем перетаскивания.</span><span class="sxs-lookup"><span data-stu-id="43f8e-118">Using the FullCalendar jQuery plugin, with little effort users get rich solutions capable of things such as using different colors to mark different events or using drag and drop to reorganize events.</span></span>

![Перетаскивание событий в модуле FullCalendar для перепланировки задач](../../../images/fullcalendar-sewp-draganddrop.png)

## <a name="migrate-the-tasks-calendar-solution-from-the-script-editor-web-part-to-the-sharepoint-framework"></a><span data-ttu-id="43f8e-120">Перенос решения для просмотра календаря задач из веб-части редактора скриптов на платформу SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="43f8e-120">Migrate the Tasks calendar solution from the Script Editor Web Part to the SharePoint Framework</span></span>

> [!NOTE] 
> <span data-ttu-id="43f8e-121">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment.md) для создания решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43f8e-121">Before following the steps in this article, be sure to [set up your development environment](../../set-up-your-development-environment.md) for building SharePoint Framework solutions.</span></span>

<span data-ttu-id="43f8e-122">Преобразование модификации на основе веб-части редактора скриптов для SharePoint Framework обеспечивает ряд преимуществ, таких как повышенное удобство настройки и централизованное управление решением.</span><span class="sxs-lookup"><span data-stu-id="43f8e-122">Transforming a Script Editor Web Part-based customization to the SharePoint Framework offers a number of benefits such as more user-friendly configuration and centralized management of the solution.</span></span> <span data-ttu-id="43f8e-123">Ниже представлено пошаговое описание переноса решения на платформу SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43f8e-123">Following is a step-by-step description of how you would migrate the solution to the SharePoint Framework.</span></span> 

<span data-ttu-id="43f8e-124">Для начала необходимо перенести решение на платформу SharePoint Framework, внеся как можно меньше изменений в первоначальный код.</span><span class="sxs-lookup"><span data-stu-id="43f8e-124">First, you migrate the solution to the SharePoint Framework with as few changes to the original code as possible.</span></span> <span data-ttu-id="43f8e-125">Затем следует преобразовать код решения в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов во время разработки, и заменить часть кода на API SharePoint Framework, чтобы в полной мере воспользоваться возможностями платформы и еще больше упростить решение.</span><span class="sxs-lookup"><span data-stu-id="43f8e-125">Later, you transform the solution's code to TypeScript to benefit from its development-time type safety features, and replace some of the code with the SharePoint Framework API to fully benefit from its capabilities and simplify the solution even further.</span></span>

> [!NOTE] 
> <span data-ttu-id="43f8e-126">Исходный код проекта на разных этапах миграции представлен в статье [Руководство. Перенос решения с jQuery и FullCalendar, созданного с помощью веб-части редактора скриптов, на платформу SharePoint Framework](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-fullcalendar).</span><span class="sxs-lookup"><span data-stu-id="43f8e-126">The source code of the project in the different stages of migration is available at [Tutorial: Migrate jQuery and FullCalendar solution built using Script Editor Web Part to SharePoint Framework](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/tutorial-migrate-fullcalendar).</span></span>

### <a name="create-new-sharepoint-framework-project"></a><span data-ttu-id="43f8e-127">Создание проекта SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="43f8e-127">Create new SharePoint Framework project</span></span>

1. <span data-ttu-id="43f8e-128">Для начала создайте папку проекта:</span><span class="sxs-lookup"><span data-stu-id="43f8e-128">Start by creating a new folder for your project</span></span>

  ```sh
  md fullcalendar-taskscalendar
  ```

2. <span data-ttu-id="43f8e-129">Перейдите в папку проекта:</span><span class="sxs-lookup"><span data-stu-id="43f8e-129">Navigate to the project folder:</span></span>

  ```sh
  cd fullcalendar-taskscalendar
  ```

3. <span data-ttu-id="43f8e-130">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы выполнить скаффолдинг нового проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="43f8e-130">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="43f8e-131">Определите значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="43f8e-131">When prompted, define values as follows:</span></span>
  - <span data-ttu-id="43f8e-132">имя решения — **fullcalendar-taskscalendar**;</span><span class="sxs-lookup"><span data-stu-id="43f8e-132">**fullcalendar-taskscalendar** as your solution name</span></span>
  - <span data-ttu-id="43f8e-133">расположение файлов — **Use the current folder** (Использовать текущую папку);</span><span class="sxs-lookup"><span data-stu-id="43f8e-133">**Use the current folder** for the location to place the files</span></span>
  - <span data-ttu-id="43f8e-134">создаваемый клиентский компонент — **WebPart**;</span><span class="sxs-lookup"><span data-stu-id="43f8e-134">**WebPart** as the client-side component to create</span></span>
  - <span data-ttu-id="43f8e-135">имя веб-части — **Tasks calendar**;</span><span class="sxs-lookup"><span data-stu-id="43f8e-135">**Tasks calendar** as your web part name</span></span>
  - <span data-ttu-id="43f8e-136">описание веб-части **Shows tasks in the calendar view** (Показывает задачи в представлении календаря);</span><span class="sxs-lookup"><span data-stu-id="43f8e-136">**Shows tasks in the calendar view** as your web part description</span></span>
  - <span data-ttu-id="43f8e-137">отправная точка создания веб-части — **No javaScript web framework** (Без платформы JavaScript).</span><span class="sxs-lookup"><span data-stu-id="43f8e-137">**No javaScript web framework** as the starting point to build the web part</span></span>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/fullcalendar-yeoman.png)

5. <span data-ttu-id="43f8e-139">По завершении скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-139">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="43f8e-140">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="43f8e-140">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="43f8e-141">В этом руководстве используется Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="43f8e-141">In this tutorial, you will use Visual Studio Code.</span></span>

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/fullcalendar-vscode.png)

### <a name="load-javascript-libraries"></a><span data-ttu-id="43f8e-143">Загрузка библиотек JavaScript</span><span class="sxs-lookup"><span data-stu-id="43f8e-143">Load JavaScript libraries</span></span>

<span data-ttu-id="43f8e-144">Как и в исходном решении, созданном с помощью веб-части редактора скриптов, сначала необходимо загрузить библиотеки JavaScript, необходимые решению.</span><span class="sxs-lookup"><span data-stu-id="43f8e-144">Similar to the original solution built by using the Script Editor Web Part, you first need to load the JavaScript libraries required by the solution.</span></span> <span data-ttu-id="43f8e-145">Как правило, в SharePoint Framework этот процесс состоит из двух этапов: указания URL-адреса, с которого загружаются библиотеки, и обращения к библиотеке в коде.</span><span class="sxs-lookup"><span data-stu-id="43f8e-145">Similarly to the original solution built using the Script Editor Web Part, first you need to load the JavaScript libraries required by the solution. In SharePoint Framework this usually consists of two steps: specifying the URL from which the library should be loaded, and referencing the library in the code.</span></span>

1. <span data-ttu-id="43f8e-146">Укажите URL-адреса, с которых следует загружать библиотеки.</span><span class="sxs-lookup"><span data-stu-id="43f8e-146">Specify the URLs from which libraries should be loaded.</span></span> <span data-ttu-id="43f8e-147">Откройте в редакторе кода файл **./config/config.json** и замените код в разделе **externals** на следующий:</span><span class="sxs-lookup"><span data-stu-id="43f8e-147">Start, with specifying the URLs from which libraries should be loaded. In the code editor, open the **./config/config.json** file and change the **externals** section to:</span></span>

  ```json
  {
    "externals": {
      "jquery": "https://code.jquery.com/jquery-1.11.1.min.js",
      "moment": "https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.10.6/moment.min.js",
      "fullcalendar": "https://cdnjs.cloudflare.com/ajax/libs/fullcalendar/3.4.0/fullcalendar.min.js"
    }
  }
  ```

2. <span data-ttu-id="43f8e-148">Откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и после последнего оператора **import** добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-148">Next, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file, and after the last **import** statement add:</span></span>

  ```ts
  import 'jquery';
  import 'moment';
  import 'fullcalendar';
  ```

### <a name="define-container-div"></a><span data-ttu-id="43f8e-149">Определение div контейнера</span><span class="sxs-lookup"><span data-stu-id="43f8e-149">Define container div</span></span>

<span data-ttu-id="43f8e-150">Как и в исходном решении, далее необходимо определить, где будет отображаться календарь.</span><span class="sxs-lookup"><span data-stu-id="43f8e-150">Just as in the original solution, the next step is to define the location where the calendar should be rendered. In the code editor, open the ./src/webparts/tasksCalendar/TasksCalendarWebPart.ts file and change the render method to:</span></span> 

<span data-ttu-id="43f8e-151">В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените код метода **render** на следующий:</span><span class="sxs-lookup"><span data-stu-id="43f8e-151">In order to reference this file in the web part, in the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file and change the **render** method to:</span></span>

```ts
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

### <a name="initiate-fullcalendar-and-load-data"></a><span data-ttu-id="43f8e-152">Инициализация модуля FullCalendar и загрузка данных</span><span class="sxs-lookup"><span data-stu-id="43f8e-152">Initiate FullCalendar and load data</span></span>

<span data-ttu-id="43f8e-153">Последний этап — добавление кода, инициализирующего подключаемый модуль FullCalendar для jQuery и загружающего данные из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="43f8e-153">The last step is to include the code that initiates the FullCalendar jQuery plugin and loads the data from SharePoint. In the ./src/webparts/tasksCalendar folder, create a new file named script.js and paste the following code:</span></span> 

1.  <span data-ttu-id="43f8e-154">В папке **./src/webparts/tasksCalendar** создайте файл с именем **script.js** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-154">In the **./src/webparts/tasksCalendar** folder, create a new file named **script.js**, and paste in the following code:</span></span>

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

  <span data-ttu-id="43f8e-155">Он практически идентичен первоначальному коду модификации на основе веб-части редактора скриптов.</span><span class="sxs-lookup"><span data-stu-id="43f8e-155">This code is almost identical to the original code of the Script Editor Web Part customization.</span></span> <span data-ttu-id="43f8e-156">Единственное отличие заключается в том, что первоначальный код получал URL-адрес текущего сайта из глобальной переменной **\_spPageContextInfo**, которую задает SharePoint (строки 8, 45, 96 и 104), а на платформе SharePoint Framework используется пользовательская переменная, которую необходимо задать в веб-части.</span><span class="sxs-lookup"><span data-stu-id="43f8e-156">This code is almost identical with the original code of the Script Editor Web Part customization. The only difference is that where the original code retrieved the URL of the current web from the global **\_spPageContextInfo** variable set by SharePoint (lines 8, 45, 96 and 104), the code in the SharePoint Framework uses a custom variable that you will have to set in the web part. SharePoint Framework client-side web parts can be used both on classic and modern pages. While the _spPageContextInfo variable is present on classic pages, it's not available on modern pages which is why you can't rely on it and need a custom property that you can control yourself instead.</span></span> 
  
  <span data-ttu-id="43f8e-157">Клиентские веб-части SharePoint Framework можно использовать как на классических, так и на современных страницах.</span><span class="sxs-lookup"><span data-stu-id="43f8e-157">SharePoint Framework client-side web parts can be used both on classic and modern pages.</span></span> <span data-ttu-id="43f8e-158">Переменная **_spPageContextInfo** используется на классических страницах, но недоступна на современных, поэтому не следует рассчитывать на нее. Рекомендуем использовать настраиваемое свойство, которым можно управлять самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="43f8e-158">While the **_spPageContextInfo** variable is present on classic pages, it's not available on modern pages, which is why you can't rely on it and need a custom property that you can control yourself instead.</span></span>

2. <span data-ttu-id="43f8e-159">Чтобы сослаться на этот файл в веб-части, откройте в редакторе кода файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените метод **render** на следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-159">In order to reference this file in the web part, in the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file and change the **render** method to:</span></span>

  ```ts
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

3. <span data-ttu-id="43f8e-160">Проверьте работу веб-части, выполнив в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-160">Verify, that the web part is working as expected by in the command line executing:</span></span>

  ```sh
  gulp serve --nobrowser
  ```

  <span data-ttu-id="43f8e-161">Так как веб-часть загружает свои данные из SharePoint, ее необходимо тестировать с помощью размещенной рабочей области SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43f8e-161">Because the web part loads its data from SharePoint, you have to test the web part by using the hosted SharePoint Framework workbench.</span></span> 
  
4. <span data-ttu-id="43f8e-162">Перейдите по адресу `https://yourtenant.sharepoint.com/_layouts/workbench.aspx` и добавьте веб-часть на холст.</span><span class="sxs-lookup"><span data-stu-id="43f8e-162">Navigate to `https://yourtenant.sharepoint.com/_layouts/workbench.aspx` and add the web part to the canvas.</span></span> <span data-ttu-id="43f8e-163">Теперь задачи должны отображаться в представлении календаря с помощью подключаемого модуля FullCalendar для jQuery.</span><span class="sxs-lookup"><span data-stu-id="43f8e-163">You should now see the tasks displayed in a calendar view by using the FullCalendar jQuery plug-in.</span></span>

  ![Задачи, отображаемые в представлении календаря в клиентской веб-части SharePoint Framework](../../../images/fullcalendar-spfx.png)

## <a name="add-support-for-configuring-the-web-part-through-web-part-properties"></a><span data-ttu-id="43f8e-165">Добавление возможности настраивать веб-часть с помощью ее свойств</span><span class="sxs-lookup"><span data-stu-id="43f8e-165">Add support for configuring the web part through web part properties</span></span>

<span data-ttu-id="43f8e-166">На предыдущих этапах мы перенесли решение для просмотра календаря задач из веб-части редактора скриптов на платформу SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43f8e-166">In the previous steps, you migrated the Tasks calendar solutions from the Script Editor Web Part to the SharePoint Framework.</span></span> <span data-ttu-id="43f8e-167">Решение уже работает надлежащим образом, но не использует преимущества платформы SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43f8e-167">While the solution already works as expected, it doesn't use any of the SharePoint Framework benefits.</span></span> <span data-ttu-id="43f8e-168">Имя списка, из которого загружаются задачи, включено в код, представляющий собой обычный JavaScript, который хуже поддается рефакторингу, чем TypeScript.</span><span class="sxs-lookup"><span data-stu-id="43f8e-168">The name of the list from which tasks are loaded is included in the code, and the code itself is plain JavaScript, which is harder to refactor than TypeScript.</span></span> 

<span data-ttu-id="43f8e-169">В приведенных ниже разделах описано, как расширить имеющееся решение, чтобы пользователи могли указывать имя списка, из которого будут загружаться данные.</span><span class="sxs-lookup"><span data-stu-id="43f8e-169">The following steps illustrate how to extend the existing solution to allow users to specify the name of the list to load the data from.</span></span> <span data-ttu-id="43f8e-170">Позже мы преобразуем код в TypeScript, чтобы воспользоваться функциями обеспечения безопасности типов.</span><span class="sxs-lookup"><span data-stu-id="43f8e-170">Later, you transform the code to TypeScript to benefit from its type safety features.</span></span>

### <a name="define-web-part-property-for-storing-the-name-of-the-list"></a><span data-ttu-id="43f8e-171">Определение свойства веб-части для хранения имени списка</span><span class="sxs-lookup"><span data-stu-id="43f8e-171">Define web part property for storing the name of the list</span></span>

1. <span data-ttu-id="43f8e-172">Определите свойство веб-части для хранения имени списка, из которого будут загружаться задачи.</span><span class="sxs-lookup"><span data-stu-id="43f8e-172">Define a web part property to store the name of the list from which tasks should be loaded.</span></span> <span data-ttu-id="43f8e-173">В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.manifest.json**, замените имя заданного по умолчанию свойства **description** на **listName** и удалите его значение.</span><span class="sxs-lookup"><span data-stu-id="43f8e-173">Start with defining a web part property to store the name of the list from which tasks should be loaded. In the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.manifest.json** file and rename the default **description** property to **listName** and clear its value.</span></span>

  ![Свойство listName манифеста веб-части, выделенное в Visual Studio Code](../../../images/fullcalendar-spfx-listname-property.png)

2. <span data-ttu-id="43f8e-175">Обновите интерфейс свойств веб-части, чтобы применить изменения манифеста.</span><span class="sxs-lookup"><span data-stu-id="43f8e-175">Update the web part properties interface to reflect the changes in the manifest.</span></span> <span data-ttu-id="43f8e-176">В редакторе кода откройте файл **./src/webparts/tasksCalendar/ITasksCalendarWebPartProps.ts** и замените его содержимое на следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-176">In the code editor open the **./src/webparts/toDo/app/DataService.ts** file and change its contents to:</span></span>

  ```ts
  export interface ITasksCalendarWebPartProps {
    listName: string;
  }
  ```

3. <span data-ttu-id="43f8e-177">Обновите метки отображения для свойства **listName**.</span><span class="sxs-lookup"><span data-stu-id="43f8e-177">Update the display labels for the **listName** property.</span></span> <span data-ttu-id="43f8e-178">Откройте файл **./src/webparts/tasksCalendar/loc/mystrings.d.ts** и замените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="43f8e-178">Then, update the display labels for the listName property. Open the **./src/webparts/tasksCalendar/loc/mystrings.d.ts** file and change its contents to:</span></span>

  ```ts
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

4. <span data-ttu-id="43f8e-179">Откройте файл **./src/webparts/tasksCalendar/loc/en-us.js** и замените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="43f8e-179">Next, open the **./src/webparts/tasksCalendar/loc/en-us.js** file and change its contents to:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Tasks calendar settings",
      "BasicGroupName": "Data",
      "ListNameFieldLabel": "List name"
    }
  });
  ```

5. <span data-ttu-id="43f8e-180">Обновите веб-часть, чтобы использовалось новое свойство.</span><span class="sxs-lookup"><span data-stu-id="43f8e-180">Update the web part to use the newly defined property.</span></span> <span data-ttu-id="43f8e-181">В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените код метода **getPropertyPaneConfiguration** на следующий:</span><span class="sxs-lookup"><span data-stu-id="43f8e-181">Finally, update the web part to use the newly defined property. In the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file and change the **getPropertyPaneConfiguration** method to:</span></span>

  ```ts
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

<span data-ttu-id="43f8e-182">Чтобы веб-часть не перезагружалась, когда пользователь вводит имя списка, она также должна использовать нереактивную область свойств. Для этого добавьте метод **disableReactivePropertyChanges** и задайте для него возвращаемое значение **true**.</span><span class="sxs-lookup"><span data-stu-id="43f8e-182">To prevent the web part from reloading as users type the name of the list, you've also configured the web part to use the non-reactive property pane by adding the **disableReactivePropertyChanges** method and settings its return value to **true**.</span></span>

### <a name="use-the-configured-name-of-the-list-to-load-the-data-from"></a><span data-ttu-id="43f8e-183">Использование заданного имени списка для загрузки данных</span><span class="sxs-lookup"><span data-stu-id="43f8e-183">Use the configured name of the list to load the data from</span></span>

<span data-ttu-id="43f8e-184">Изначально имя списка, из которого загружаются данные, внедрялось в запросы REST.</span><span class="sxs-lookup"><span data-stu-id="43f8e-184">Initially, the name of the list from which the data should be loaded was embedded in the REST queries.</span></span> <span data-ttu-id="43f8e-185">Теперь, когда пользователи могут настраивать это имя, указанное значение следует внедрять в запросы REST перед их выполнением.</span><span class="sxs-lookup"><span data-stu-id="43f8e-185">Now that users can configure this name, the configured value should be injected into the REST queries before executing them.</span></span> <span data-ttu-id="43f8e-186">Это проще всего сделать, переместив содержимое файла **script.js** в основной файл веб-части.</span><span class="sxs-lookup"><span data-stu-id="43f8e-186">The easiest way to do that is by moving the contents of the **script.js** file to the main web part file.</span></span>

1. <span data-ttu-id="43f8e-187">В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="43f8e-187">In the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file.</span></span>

2. <span data-ttu-id="43f8e-188">Измените оператор импорта для загрузки необходимых библиотек:</span><span class="sxs-lookup"><span data-stu-id="43f8e-188">Start, by changing the import statement to load the required libraries to:</span></span>

  ```ts
  var $: any = require('jquery');
  var moment: any = require('moment');

  import 'fullcalendar';

  var COLORS = ['#466365', '#B49A67', '#93B7BE', '#E07A5F', '#849483', '#084C61', '#DB3A34'];
  ```

  <span data-ttu-id="43f8e-189">В коде, который мы будем использовать позже, есть ссылка на библиотеку Moment.js, поэтому коду TypeScript должно быть известно ее имя, иначе сборка проекта завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="43f8e-189">Because Moment.js is referenced in the code that you will be using later, its name must be known to TypeScript or building the project will fail.</span></span> <span data-ttu-id="43f8e-190">То же относится и к jQuery.</span><span class="sxs-lookup"><span data-stu-id="43f8e-190">The same applies to jQuery.</span></span> <span data-ttu-id="43f8e-191">Так как FullCalendar представляет собой подключаемый модуль для jQuery, присоединяющийся к объекту jQuery, его можно импортировать так же, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="43f8e-191">Because FullCalendar is a jQuery plug-in that attaches itself to the jQuery object, it can be imported the same way as previously.</span></span>

  <span data-ttu-id="43f8e-192">Последняя часть включает копирование списка цветов для пометки различных событий.</span><span class="sxs-lookup"><span data-stu-id="43f8e-192">The last part includes copying the list of colors to use for marking the different events.</span></span>

3. <span data-ttu-id="43f8e-193">Скопируйте функции **displayTasks** и **updateTask** из файла **script.js** и вставьте их в класс **TasksCalendarWebPart**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="43f8e-193">Next, copy the **displayTasks** and **updateTask** functions from the **script.js** file and paste them as follows inside the **TasksCalendarWebPart** class:</span></span>

  ```ts
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

  <span data-ttu-id="43f8e-194">По сравнению с предыдущим случаем в код вносится меньше изменений.</span><span class="sxs-lookup"><span data-stu-id="43f8e-194">There are a few changes in the code compared to the previous situation.</span></span> <span data-ttu-id="43f8e-195">Теперь обычные функции JavaScript преобразуются в методы TypeScript путем замены ключевого слова **function** на модификатор **private**.</span><span class="sxs-lookup"><span data-stu-id="43f8e-195">Plain JavaScript functions are now changed into TypeScript methods by replacing the **function** keyword with the **private** modifier.</span></span> <span data-ttu-id="43f8e-196">Это необходимо, чтобы можно было добавить их в класс **TaskCalendarWebPart**.</span><span class="sxs-lookup"><span data-stu-id="43f8e-196">This is required to be able to add them to the **TaskCalendarWebPart** class.</span></span> <span data-ttu-id="43f8e-197">Так как теперь оба метода находятся в том же файле, что и веб-часть, вы можете не определять глобальную переменную для хранения URL-адреса текущего сайта, а обращаться к нему непосредственно из контекста веб-части с помощью свойства `this.context.pageContext.web.absoluteUrl`.</span><span class="sxs-lookup"><span data-stu-id="43f8e-197">Because both methods are now in the same file as the web part, instead of defining a global variable to hold the URL of the current site, you can access it directly from the web part context by using the `this.context.pageContext.web.absoluteUrl` property.</span></span> <span data-ttu-id="43f8e-198">Кроме того, во всех запросах REST фиксированное имя списка заменяется на значение свойства **listName**, в котором хранится имя списка, заданное пользователем.</span><span class="sxs-lookup"><span data-stu-id="43f8e-198">Additionally, in all REST queries, the fixed list name is replaced with the value of the **listName** property, which holds the name of the list as configured by the user.</span></span> <span data-ttu-id="43f8e-199">Прежде чем использовать это значение, необходимо применить к нему функцию **escape** из lodash, чтобы запретить внедрение скриптов.</span><span class="sxs-lookup"><span data-stu-id="43f8e-199">Before using the value, it's being escaped by using the lodash's **escape** function to disallow script injection.</span></span>

4. <span data-ttu-id="43f8e-200">Напоследок измените метод **render**, чтобы он вызывал новый метод **displayTasks**:</span><span class="sxs-lookup"><span data-stu-id="43f8e-200">As the last step, change the **render** method to call the newly added **displayTasks** method:</span></span>

  ```ts
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

5. <span data-ttu-id="43f8e-201">Так как мы только что переместили содержимое файла **script.js** в основной файл веб-части, файл **script.js** больше не требуется. Его можно удалить из проекта.</span><span class="sxs-lookup"><span data-stu-id="43f8e-201">As you have just moved the contents of the **script.js** file into the main web part file, the **script.js** is no longer necessary and you can delete it from the project.</span></span>

6. <span data-ttu-id="43f8e-202">Чтобы проверить работу веб-части, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-202">To verify that the web part is working as expected, run in the command line:</span></span>

  ```sh
  gulp serve --nobrowser
  ```

7. <span data-ttu-id="43f8e-203">Перейдите к размещенной рабочей области и добавьте веб-часть на холст.</span><span class="sxs-lookup"><span data-stu-id="43f8e-203">Navigate to the hosted Workbench and add the web part to the canvas.</span></span> <span data-ttu-id="43f8e-204">Откройте область свойств веб-части, укажите имя списка задач и нажмите кнопку **Apply** (Применить), чтобы подтвердить изменения.</span><span class="sxs-lookup"><span data-stu-id="43f8e-204">Open the web part property pane, specify the name of the list with tasks, and select the **Apply** button to confirm the changes.</span></span> <span data-ttu-id="43f8e-205">Задачи должны появиться в представлении календаря в веб-части.</span><span class="sxs-lookup"><span data-stu-id="43f8e-205">You should now see tasks displayed in a calendar view in the web part.</span></span>

  ![Задачи, загруженные из указанного списка и отображаемые в клиентской веб-части SharePoint Framework](../../../images/fullcalendar-spfx-list-configured.png)

## <a name="transform-the-plain-javascript-code-to-typescript"></a><span data-ttu-id="43f8e-207">Преобразование обычного кода JavaScript в TypeScript</span><span class="sxs-lookup"><span data-stu-id="43f8e-207">Transform the plain JavaScript code to TypeScript</span></span>

<span data-ttu-id="43f8e-208">Использование TypeScript вместо обычного JavaScript обеспечивает ряд преимуществ.</span><span class="sxs-lookup"><span data-stu-id="43f8e-208">Using TypeScript over plain JavaScript offers a number of benefits.</span></span> <span data-ttu-id="43f8e-209">Обслуживание и рефакторинг кода выполнять удобнее, если используется TypeScript. Кроме того, в таком коде можно раньше обнаруживать ошибки.</span><span class="sxs-lookup"><span data-stu-id="43f8e-209">Using TypeScript over plain JavaScript offers a number of benefits. Not only is TypeScript easier to maintain and refactor but it also allows you to catch errors earlier. Following steps describe how you would transform the original JavaScript code to TypeScript.</span></span> <span data-ttu-id="43f8e-210">Ниже описано, как преобразовать первоначальный код JavaScript в TypeScript.</span><span class="sxs-lookup"><span data-stu-id="43f8e-210">The following steps describe how you would transform the original JavaScript code to TypeScript.</span></span>

### <a name="add-type-definitions-for-used-libraries"></a><span data-ttu-id="43f8e-211">Добавление определений типов для используемых библиотек</span><span class="sxs-lookup"><span data-stu-id="43f8e-211">Add type definitions for used libraries</span></span>

<span data-ttu-id="43f8e-p124">Для надлежащей работы TypeScript необходимы определения типов для различных библиотек, используемых в проекте. Определения типов часто распространяются в виде пакетов npm в пространстве имен @types.</span><span class="sxs-lookup"><span data-stu-id="43f8e-p124">To function properly, TypeScript requires type definitions for the different libraries used in the project. Type definitions are often distributed as npm packages in the @types namespace.</span></span>

1. <span data-ttu-id="43f8e-214">Установите определения типов для jQuery и FullCalendar, выполнив в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-214">Start by installing type definitions for jQuery and FullCalendar by executing in the command line:</span></span>

  ```sh
  npm install --save-dev @types/jquery@1 @types/fullcalendar
  ```

  <span data-ttu-id="43f8e-215">Определения типов для Moment.js доступны в пакете Moment.js.</span><span class="sxs-lookup"><span data-stu-id="43f8e-215">Type definitions for Moment.js are distributed together with the Moment.js package.</span></span> <span data-ttu-id="43f8e-216">Мы загружаем библиотеку Moment.js с URL-адреса, но для использования ее определений типов все равно необходимо установить пакет Moment.js в проекте.</span><span class="sxs-lookup"><span data-stu-id="43f8e-216">Type definitions for Moment.js are distributed together with the Moment.js package. Even though, you're loading Moment.js from a URL, in order to use its typings, you still need to install the Moment.js package in the project.</span></span>

2. <span data-ttu-id="43f8e-217">Установите пакет Moment.js, выполнив в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-217">Install the Moment.js package by executing in the command line:</span></span>

  ```sh
  npm install --save moment
  ```

### <a name="update-package-references"></a><span data-ttu-id="43f8e-218">Обновление ссылок на пакеты</span><span class="sxs-lookup"><span data-stu-id="43f8e-218">Update package references</span></span>

<span data-ttu-id="43f8e-219">Чтобы использовать типы из установленных определений, необходимо изменить ссылки на библиотеки.</span><span class="sxs-lookup"><span data-stu-id="43f8e-219">In order to use types from the installed type definitions, you have to change how you reference libraries. In the code editor, open the ./src/webparts/itRequests/ItRequestsWebPart.ts file and change  statement to:</span></span> 

<span data-ttu-id="43f8e-220">В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и замените операторы импорта на следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-220">In order to use types from the installed type definitions, you have to change how you reference libraries. In the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file and change the import statements to:</span></span>

```ts
import * as $ from 'jquery';
import 'fullcalendar';
import * as moment from 'moment';
```

### <a name="update-main-web-part-files-to-typescript"></a><span data-ttu-id="43f8e-221">Преобразование основных файлов веб-части в TypeScript</span><span class="sxs-lookup"><span data-stu-id="43f8e-221">Update main web part files to TypeScript</span></span>

<span data-ttu-id="43f8e-222">Теперь, когда у нас есть определения типов для всех библиотек, установленных в проекте, можно приступить к преобразованию обычного кода JavaScript в TypeScript.</span><span class="sxs-lookup"><span data-stu-id="43f8e-222">Now that you have type definitions for all libraries installed in the project, you can start transforming the plain JavaScript code to TypeScript.</span></span>

1. <span data-ttu-id="43f8e-223">Определите интерфейс для задачи, получаемой из списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="43f8e-223">Define an interface for a task that you retrieve from the SharePoint list.</span></span> <span data-ttu-id="43f8e-224">В редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** и непосредственно над классом веб-части добавьте следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="43f8e-224">Start, with defining an interface for a task that you retrieve from the SharePoint list. In the code editor, open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file and just above the web part class, add the following code snippet:</span></span>

  ```ts
  interface ITask {
    ID: number;
    Title: string;
    StartDate: string;
    DueDate: string;
    AssignedTo: [{ Title: string }];
  }
  ```

2. <span data-ttu-id="43f8e-225">В классе веб-части замените методы **displayTasks** и **updateTask** на следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-225">Next, in the web part class, change the **displayTasks** and **updateTask** methods to:</span></span>

  ```ts
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

  <span data-ttu-id="43f8e-226">Первое и самое очевидное изменение при преобразовании обычного кода JavaScript в TypeScript — это явные типы.</span><span class="sxs-lookup"><span data-stu-id="43f8e-226">The first and most obvious change when transforming plain JavaScript to TypeScript are explicit types.</span></span> <span data-ttu-id="43f8e-227">Использовать их не обязательно, но они четко дают понять, данные какого типа ожидаются в тех или иных полях.</span><span class="sxs-lookup"><span data-stu-id="43f8e-227">While they are not required, they make it clear which type of data is expected where.</span></span> <span data-ttu-id="43f8e-228">TypeScript мгновенно определяет любое отклонение от заданного соглашения, помогая вам находить возможные проблемы как можно раньше в процессе разработки.</span><span class="sxs-lookup"><span data-stu-id="43f8e-228">Any deviation from the specified contract is immediately caught by TypeScript, helping you find possible issues as soon as possible during the development process.</span></span> <span data-ttu-id="43f8e-229">Это особенно полезно при работе с откликами AJAX и их данными.</span><span class="sxs-lookup"><span data-stu-id="43f8e-229">This is particularly useful when working with AJAX responses and their data.</span></span>

  <span data-ttu-id="43f8e-230">Еще одно изменение, которое вы уже могли заметить, — строковая интерполяция TypeScript.</span><span class="sxs-lookup"><span data-stu-id="43f8e-230">Another change that you might have noticed already is the TypeScript string interpolation.</span></span> <span data-ttu-id="43f8e-231">Она упрощает динамическое составление строк и делает код более удобочитаемым.</span><span class="sxs-lookup"><span data-stu-id="43f8e-231">Another change, that you might have noticed already, is TypeScript string interpolation. Using string interpolation simplifies dynamic string composition and increases the readability of your code. Compare plain JavaScript:</span></span> 
  
  <span data-ttu-id="43f8e-232">Обычный код JavaScript:</span><span class="sxs-lookup"><span data-stu-id="43f8e-232">Compare plain JavaScript:</span></span>

  ```js
  var restQuery = "/_api/Web/Lists/GetByTitle('" + TASK_LIST + "')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '" + startDate + "' and DueDate le '" + endDate + "')or(StartDate ge '" + startDate + "' and StartDate le '" + endDate + "'))";
  ```

  <span data-ttu-id="43f8e-233">Сравните его со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="43f8e-233">to:</span></span>

  ```ts
  const restQuery: string = `/_api/Web/Lists/GetByTitle('${escape(this.properties.listName)}')/items?$select=ID,Title,\
  Status,StartDate,DueDate,AssignedTo/Title&$expand=AssignedTo&\
  $filter=((DueDate ge '${startDate}' and DueDate le '${endDate}')or(StartDate ge '${startDate}' and StartDate le '${endDate}'))`;
  ```

  <span data-ttu-id="43f8e-234">Еще одно преимущество строковой интерполяции TypeScript — отсутствие необходимости отменять кавычки, что также упрощает запросы REST.</span><span class="sxs-lookup"><span data-stu-id="43f8e-234">Additional benefit of using TypeScript string interpolation is, that you don't need to escape quotes, which also simplifies composing REST queries.</span></span>

3. <span data-ttu-id="43f8e-235">Чтобы убедиться, что все работает должным образом, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-235">To confirm that everything is working as expected, in the command line execute:</span></span>

  ```sh
  gulp serve --nobrowser
  ```

4. <span data-ttu-id="43f8e-236">Перейдите к размещенной рабочей области и добавьте веб-часть на холст.</span><span class="sxs-lookup"><span data-stu-id="43f8e-236">Go to the hosted Workbench and add the web part to the canvas.</span></span> <span data-ttu-id="43f8e-237">Визуально ничего не изменилось, но новая кодовая база использует TypeScript и соответствующие определения типов, что упрощает обслуживание решения.</span><span class="sxs-lookup"><span data-stu-id="43f8e-237">Navigate to the hosted workbench and add the web part to the canvas. Although visually nothing has changed, the new code base uses TypeScript and its type definitions to help you maintain the solution.</span></span>

### <a name="replace-jquery-ajax-calls-with-sharepoint-framework-api"></a><span data-ttu-id="43f8e-238">Замена вызовов AJAX jQuery на API SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="43f8e-238">Replace jQuery AJAX calls with SharePoint Framework API</span></span>

<span data-ttu-id="43f8e-p130">В данный момент решение использует вызовы AJAX jQuery для связи с REST API SharePoint. Для обычных запросов GET так же удобно использовать API AJAX jQuery, как и SPHttpClient на платформе SharePoint Framework. Разница становится заметна при выполнении запросов POST, таких как следующий запрос на обновление события:</span><span class="sxs-lookup"><span data-stu-id="43f8e-p130">At this moment, the solution uses jQuery AJAX calls to communicate with the SharePoint REST API. For regular GET requests, the jQuery AJAX API is just as convenient as using the SharePoint Framework SPHttpClient. The real difference is when performing POST requests such as the one for updating the event:</span></span>

```ts
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

<span data-ttu-id="43f8e-242">Так как нам требуется обновить элемент списка, необходимо предоставить среде SharePoint действительный токен дайджеста запроса.</span><span class="sxs-lookup"><span data-stu-id="43f8e-242">Because you want to update a list item, you need to provide SharePoint with a valid request digest token.</span></span> <span data-ttu-id="43f8e-243">Он доступен на классических страницах, но действителен в течение 3 минут, поэтому всегда предпочтительнее получить действительный токен самостоятельно, прежде чем выполнять обновление.</span><span class="sxs-lookup"><span data-stu-id="43f8e-243">While it's available on classic pages, it's valid for 3 minutes, so it's always the safest to retrieve a valid token yourself before performing an update operation.</span></span> <span data-ttu-id="43f8e-244">Получив дайджест запроса, следует добавить его к заголовкам запроса на обновление.</span><span class="sxs-lookup"><span data-stu-id="43f8e-244">After you obtain the request digest, you have to add it to request headers of the update request.</span></span> <span data-ttu-id="43f8e-245">В противном случае запрос не будет выполнен.</span><span class="sxs-lookup"><span data-stu-id="43f8e-245">If you don't, the request fails.</span></span>

<span data-ttu-id="43f8e-246">Класс SPHttpClient платформы SharePoint Framework упрощает связь с SharePoint, автоматически определяя запросы POST, которым требуется действительный токен дайджеста.</span><span class="sxs-lookup"><span data-stu-id="43f8e-246">SharePoint Framework SPHttpClient simplifies communicating with SharePoint because it automatically detects if the request is a POST request and needs a valid request digest.</span></span> <span data-ttu-id="43f8e-247">Для таких запросов SPHttpClient автоматически получает токен из SharePoint и добавляет его к запросу.</span><span class="sxs-lookup"><span data-stu-id="43f8e-247">If it does, the SPHttpClient automatically retrieves it from SharePoint and adds it to the request.</span></span> <span data-ttu-id="43f8e-248">Для сравнения, аналогичный запрос, отправленный с использованием SPHttpClient, будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="43f8e-248">By comparison, the same request issued using the SPHttpClient would look like this:</span></span>

```ts
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

1. <span data-ttu-id="43f8e-p133">Чтобы заменить исходные вызовы AJAX jQuery на API SPHttpClient платформы SharePoint Framework, в редакторе кода откройте файл **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts**. В список импорта добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="43f8e-p133">To replace the original jQuery AJAX calls with the SharePoint Framework SPHttpClient API, in the code editor open the **./src/webparts/tasksCalendar/TasksCalendarWebPart.ts** file. To the list of imports add:</span></span>

  ```ts
  import { SPHttpClient, SPHttpClientResponse } from '@microsoft/sp-http';
  ```

2. <span data-ttu-id="43f8e-251">В классе **TasksCalendarWebPart** замените методы **displayTasks** и **updateTask** на следующий код:</span><span class="sxs-lookup"><span data-stu-id="43f8e-251">In the **TasksCalendarWebPart** class replace the **displayTasks** and **updateTask** methods with the following code:</span></span>

  ```ts
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
  > <span data-ttu-id="43f8e-252">Если в откликах от REST API SharePoint запрещены метаданные, то при использовании класса SPHttpClient платформы SharePoint Framework необходимо убедиться, что для заголовка **Accept** используется значение `application/json;odata.metadata=none`, а не `application/json;odata=nometadata`.</span><span class="sxs-lookup"><span data-stu-id="43f8e-252">Important: If you're suppressing metadata in the responses of the SharePoint REST API, when using the SharePoint Framework SPHttpClient you have to ensure that you're using `application/json;odata.metadata=none` and not `application/json;odata=nometadata` as the value of the **Accept** header. SPHttpClient uses OData 4.0 and requires the first value. If you use the latter instead, the request will fail with a 406 Not Acceptable response.</span></span> <span data-ttu-id="43f8e-253">SPHttpClient использует OData 4.0, поэтому необходимо задать первое значение.</span><span class="sxs-lookup"><span data-stu-id="43f8e-253">SPHttpClient uses OData 4.0 and requires the first value.</span></span> <span data-ttu-id="43f8e-254">Если использовать другое, при выполнении запроса будет возвращена ошибка **406 Not Acceptable**.</span><span class="sxs-lookup"><span data-stu-id="43f8e-254">If you use the latter instead, the request fails with a **406 Not Acceptable** response.</span></span>

3. <span data-ttu-id="43f8e-255">Чтобы убедиться, что все работает должным образом, выполните в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="43f8e-255">To confirm that everything is working as expected, in the command line execute:</span></span>

  ```sh
  gulp serve --nobrowser
  ```

4. <span data-ttu-id="43f8e-256">Перейдите к размещенной рабочей области и добавьте веб-часть на холст.</span><span class="sxs-lookup"><span data-stu-id="43f8e-256">Go to the hosted Workbench and add the web part to the canvas.</span></span> <span data-ttu-id="43f8e-257">Внешне ничего не изменилось, но в новом коде используется SPHttpClient на платформе SharePoint Framework, что упрощает код и поддержку решения.</span><span class="sxs-lookup"><span data-stu-id="43f8e-257">Navigate to the hosted workbench and add the web part to the canvas. Although there are still no visual changes, the new code uses the SharePoint Framework SPHttpClient which simplifies your code and maintaining your solution.</span></span>
