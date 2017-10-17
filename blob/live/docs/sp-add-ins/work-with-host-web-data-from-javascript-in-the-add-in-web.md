---
title: "Работа с данными хост-сайта из JavaScript на сайте надстройки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 5690868499a39cb0c9b448e7a16a8cf0be1290ec
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="work-with-host-web-data-from-javascript-in-the-add-in-web"></a><span data-ttu-id="9581e-102">Работа с данными хост-сайта из JavaScript на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="9581e-102">Work with host web data from JavaScript in the add-in web</span></span>
<span data-ttu-id="9581e-103">Узнайте, как использовать объектную модель JavaScript (JSOM) в SharePoint для работы с данными SharePoint на хост-сайте в коде JavaScript на страницах сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="9581e-103">Use the SharePoint JavaScript object model (JSOM) to work with SharePoint data in the host web from JavaScript on pages in the add-in web.</span></span>
 

 <span data-ttu-id="9581e-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9581e-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="9581e-107">Это 11-я часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="9581e-107">This is the 11th in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="9581e-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="9581e-109">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-110">Добавление настраиваемых столбцов в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-111">Добавление настраиваемого типа контента в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-112">Добавление веб-части на страницу в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-113">Добавление рабочего процесса в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-113">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-114">Добавление настраиваемой страницы и стиля для надстройки с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-114">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-115">Добавление настраиваемой функции отрисовки в клиенте в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-115">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-116">Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-116">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="9581e-117">Работа с данными SharePoint с помощью API JavaScript для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-117">Use the SharePoint JavaScript APIs to work with SharePoint data</span></span>](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md)
    
 

 <span data-ttu-id="9581e-p102">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение Visual Studio, которое можно использовать для продолжения работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeHostWebData.sln.</span><span class="sxs-lookup"><span data-stu-id="9581e-p102">**Note**  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeHostWebData.sln file.</span></span>
 

<span data-ttu-id="9581e-p103">По умолчанию SharePoint запрещает JavaScript в надстройке получать доступ к данным на других сайтах SharePoint в ферме. Это позволяет предотвратить доступ сценариев во вредоносных надстройках к конфиденциальным данным. Но зачастую надстройке необходимо иметь доступ к хост-сайту или другим веб-сайтам в том же семействе сайтов, в котором находится хост-сайт. В этом случае можно воспользоваться двумя указанными ниже способами.</span><span class="sxs-lookup"><span data-stu-id="9581e-p103">By default, SharePoint is designed to prevent JavaScript in an add-in from getting access to data in other SharePoint websites on the farm. This prevents script in a rogue add-in from getting access to sensitive data. But often an add-in needs to have access to the host web, or to other websites within the same site collection as the host web. There are two parts to enabling this scenario in your add-in:</span></span>
 

- <span data-ttu-id="9581e-p104">Запросить разрешение на доступ к хост-сайту в файле манифеста надстройки. При установке надстройки пользователю будет предложено предоставить ей это разрешение. Если пользователь не даст разрешения, то ему не удастся установить надстройку.</span><span class="sxs-lookup"><span data-stu-id="9581e-p104">You request permission to the host web in the add-in manifest file of your add-in. The user who installs the add-in is prompted to grant this permission, and the add-in cannot be installed if user does not.</span></span>
    
 
- <span data-ttu-id="9581e-p105">Отправлять вызовы JSOM на хост-сайт с помощью объекта **SP.AppContextSite**, а не **SP.ClientContext**. Этот объект позволяет надстройке получать объекты контекста для веб-сайтов, отличных от сайта надстройки, но входящих в то же семейство веб-сайтов. Существует еще один способ доступа к любому веб-сайту в подписке SharePoint Online (или локальном веб-приложении SharePoint), но это более сложная тема.</span><span class="sxs-lookup"><span data-stu-id="9581e-p105">Instead of using an  **SP.ClientContext** object to make JSOM calls to the host web, you use a **SP.AppContextSite** object. This object enables the add-in to get a context objects for websites other than the add-in web, but only for websites within the same site collection. (There is also a way to get access to any website in the SharePoint Online subscription [or on-premise SharePoint Web Application], but that is an advanced subject.)</span></span>
    
 
 <span data-ttu-id="9581e-129">В данной статье вы будете использовать JSOM для поиска еще не запущенных процессов вводного обучения и проверки того, что они запланированы в календаре на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="9581e-129">In this article you use the JSOM to find the orientations that are not yet started and ensure that they are scheduled on a calendar in the host web.</span></span>
 

## <a name="prepare-the-host-web-calendar"></a><span data-ttu-id="9581e-130">Подготовка календаря хост-сайта</span><span class="sxs-lookup"><span data-stu-id="9581e-130">Prepare the host web calendar</span></span>

<span data-ttu-id="9581e-p106">Откройте хост-сайт (ваш тестовый веб-сайт разработчика) и убедитесь, что на нем есть календарь Employee Orientation Schedule (Расписание вводного обучения для сотрудников) с одним событием Orient Cassie Hicks (Вводное обучение для Cassie Hicks). Если его нет, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9581e-p106">Open the host web -- your developer test website -- and verify that there is a calendar on it named "Employee Orientation Schedule" and it has a single event on it: "Orient Cassie Hicks". If there isn't, take the following steps:</span></span>
 

 

1. <span data-ttu-id="9581e-133">На домашней странице сайта выберите пункты **Содержимое сайта** > **Добавить надстройку** > **Calendar** (Календарь).</span><span class="sxs-lookup"><span data-stu-id="9581e-133">From the home page of the site, choose  **Site Contents** > **add an add-in** > **Calendar**.</span></span>
    
 
2. <span data-ttu-id="9581e-134">В диалоговом окне **Adding Calendar** (Добавление календаря) введите "Employee Orientation Schedule" (Расписание вводного обучения для сотрудников) в поле **Name** (Имя), а затем нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="9581e-134">On the  **Adding Calendar** dialog, typeEmployee Orientation Schedule for the **Name**, and then choose  **Create**.</span></span>
    
 
3. <span data-ttu-id="9581e-135">Когда откроется календарь, наведите указатель на любую дату, чтобы на ней появилась ссылка **Add** (Добавить), и перейдите по этой ссылке.</span><span class="sxs-lookup"><span data-stu-id="9581e-135">When the calendar opens, put the cursor on any date until the  **Add** link appears on the date, and then click **Add**.</span></span> 
    
 
4. <span data-ttu-id="9581e-p107">В диалоговом окне **Employee Orientation Schedule - New Item** (Расписание вводного обучения для сотрудников: новый элемент) введите "Orient Cassi Hicks" (Вводное обучение Cassi Hicks) в поле **Title** (Название). В остальных полях оставьте значения, заданные по умолчанию, а затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="9581e-p107">On the  **Employee Orientation Schedule - New Item** dialog, typeOrient Cassi Hicks for the **Title**. Leave the other fields at their defaults and click  **Save**.</span></span>
    
    <span data-ttu-id="9581e-138">Календарь должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="9581e-138">The calendar should look similar to the following:</span></span>
    

    <span data-ttu-id="9581e-139">**Настраиваемый календарь**</span><span class="sxs-lookup"><span data-stu-id="9581e-139">**Custom calendar**</span></span>

 

  ![Календарь под названием "Employee Orientation Schedule" (Расписание вводного обучения для сотрудников), где в пункте "June 1st" (1 июня) указано "Orient Cassie Hicks" (Вводное обучение Cassie Hicks)](../images/d2066862-41c1-424d-9bfb-b6c5342bcf2c.PNG)
 

 

 

## <a name="create-the-javascript-and-a-button-to-invoke-it"></a><span data-ttu-id="9581e-141">Создание кода JavaScript и кнопки для его вызова</span><span class="sxs-lookup"><span data-stu-id="9581e-141">Create the JavaScript and a button to invoke it</span></span>


1. <span data-ttu-id="9581e-142">В **обозревателе решений** откройте файл Add-in.js в узле **Скрипты**.</span><span class="sxs-lookup"><span data-stu-id="9581e-142">Open the Add-in.js file in the  **Scripts** node in **Solution Explorer**.</span></span> 
    
 
2. <span data-ttu-id="9581e-143">Добавьте приведенные ниже объявления под объявлением `completedItems`.</span><span class="sxs-lookup"><span data-stu-id="9581e-143">Add the following declarations below the declaration for  `completedItems`.</span></span> 
    
      - <span data-ttu-id="9581e-144">`notStartedItems` ссылается на элементы списка **New Employees in Seattle** (Новые сотрудники в Сиэтле), для которых в столбце **Orientation Stage** (Этап обучения) задано значение **Not Started** (Не начато).</span><span class="sxs-lookup"><span data-stu-id="9581e-144">The  `notStartedItems` references the items on the **New Employees in Seattle** list whose **Orientation Stage** is **Not Started**.</span></span>
    
 
  - <span data-ttu-id="9581e-145">`calendarList` ссылается на календарь, созданный на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="9581e-145">The  `calendarList` references the calendar you created on the host web.</span></span>
    
 
  - <span data-ttu-id="9581e-146">`scheduledItems` ссылается на коллекцию элементов календаря.</span><span class="sxs-lookup"><span data-stu-id="9581e-146">The  `scheduledItems` references a collection of items on the calendar.</span></span>
    
 

```
  var notStartedItems;
var calendarList;
var scheduledItems;
```

3. <span data-ttu-id="9581e-p108">Когда Надстройка SharePoint запущена, SharePoint вызывает ее начальную страницу и добавляет в URL-адрес страницы несколько параметров запроса. Один из этих параметров  `SPHostUrl`, который представляет собой URL-адрес хост-сайта. Надстройке необходима эта информация, чтобы совершать вызовы к данным хост-сайта, поэтому в начале файла Add-in.js сразу же после объявления переменных для  `scheduledItems` добавьте указанную ниже строку. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="9581e-p108">When a SharePoint Add-in is run, SharePoint calls its start page and adds some query parameters to the start page URL. One of these is  `SPHostUrl` which is, of course, the URL of the host web. The add-in needs this information in order to make calls to host web data, so near the top of the Add-in.js file, just under the variable declaration for `scheduledItems`, add the following line. Note the following about this code:</span></span>
    
      - <span data-ttu-id="9581e-151">`getQueryStringParameter` — это служебная функция, которую мы создадим на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="9581e-151">The  `getQueryStringParameter` is a utility function that you create in the next step.</span></span>
    
 
  - <span data-ttu-id="9581e-152">`decodeUriComponent` это стандартная функция JavaScript, выполняющая обратное преобразование кодировки универсального кода ресурса (URI), которое SharePoint совершает для параметров запроса. Например, код %2F для косой черты будет преобразован обратно в символ /.</span><span class="sxs-lookup"><span data-stu-id="9581e-152">The  `decodeUriComponent` is a standard JavaScript function that reverses the URI-encoding that SharePoint does on the query parameters; for example, an encoded forward slash, "%2F", is changed back to a "/".</span></span>
    
 

```
  var hostWebURL = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
```

4. <span data-ttu-id="9581e-p109">Добавьте приведенный ниже код в конце файла. С помощью этой функции можно считывать параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="9581e-p109">Add the following code to the bottom of the file. This function can be used to read the query parameters.</span></span> 
    
```
  // Utility functions

function getQueryStringParameter(paramToRetrieve) {
     var params = document.URL.split("?")[1].split("&amp;");
     var strParams = "";
     for (var i = 0; i < params.length; i = i + 1) {
         var singleParam = params[i].split("=");
         if (singleParam[0] == paramToRetrieve) {
             return singleParam[1];
        }
     }
 }
```

5. <span data-ttu-id="9581e-p110">Добавьте приведенную ниже функцию в файл Add-in.js перед разделом с функциями обратного вызова для обработки сбоев. Вот что нужно знать об этом коде:</span><span class="sxs-lookup"><span data-stu-id="9581e-p110">Add the following function to the Add-in.js file somewhere above the failure callbacks section. Note the following about this code:</span></span>
    
      - <span data-ttu-id="9581e-p111">Этот код практически идентичен методу для запросов к спискам, который получает элементы с состоянием **Completed** (Завершено), за тем исключением, что он получает элементы с состоянием **Not Started** (Не начато), а не **Completed** (Завершено). Нас интересуют только элементы с состоянием **Not Started** (Не начато), так как для простоты в этом скрипте предполагается, что если процесс вводного обучения прошел этап **Not Started** (Не начато), то обучение должно уже быть запланировано.</span><span class="sxs-lookup"><span data-stu-id="9581e-p111">This is nearly identical to the list query method that gets the  **Completed** items, except that it gets items that are **Not Started** instead of those that are **Completed**. We are interested in only the  **Not Started** items because the script makes the simplifying assumption that if an orientation is past the **Not Started** stage, then it must already be scheduled.</span></span>
    
 
  -  <span data-ttu-id="9581e-159">Мы создадим два метода обратного вызова в методе **executeQueryAsync** на последующих этапах.</span><span class="sxs-lookup"><span data-stu-id="9581e-159">You create the two callback methods in the **executeQueryAsync** call in later steps.</span></span>
    
 

```
  function ensureOrientationScheduling() {

    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml(
        '<View><Query><Where><Eq>' +
            '<FieldRef Name=\'OrientationStage\'/><Value Type=\'Choice\'>Not started</Value>' +
        '</Eq></Where></Query></View>');
    notStartedItems = employeeList.getItems(camlQuery);
  
    clientContext.load(notStartedItems);
    clientContext.executeQueryAsync(getScheduledOrientations, onGetNotStartedItemsFail);
    return false;
}
```

6. <span data-ttu-id="9581e-p112">Добавьте указанную ниже функцию в файл Add-in.js сразу же после предыдущей функции. Обратите внимание, что она использует объект  `hostWebContext` для идентификации списка, к которому выполняется запрос.</span><span class="sxs-lookup"><span data-stu-id="9581e-p112">Add the following function to the Add-in.js file just below the preceding function. Notice that it uses the  `hostWebContext` object to identify the list that is queried.</span></span>
    
     <span data-ttu-id="9581e-p113">**Примечание.** Обратите внимание, что в запрос CAML не добавляется никакой части кода для запроса. В результате отсутствия фактического запроса в объекте запроса будут получены *все* значения времени из списка. Если список слишком большой, то запрос к серверу может выполняться неприемлемо долго. В этом случае нам понадобится другой способ достижения цели. Однако в этом примере с очень маленьким списком (списки календарей почти всегда небольшие) мы получаем весь список, поэтому можем просмотреть его полностью, сводя к минимуму количество вызовов к серверу, то есть вызовов метода **executeQueryAsync**.</span><span class="sxs-lookup"><span data-stu-id="9581e-p113">**Note**  Notice that no query markup is added to the CAML query. The effect of having no actual query in the query object is to ensure that  *all*  of the list times will be retrieved. If the list was very large this might cause the request to the server to be unacceptably long-running. In that case, we'd want to find some other way of accomplishing our goal. But in this sample situation with a very small list (and calendar lists are almost always small), getting the whole list, so that we can iterate through it on the client will actually help us minimize the number of calls to the server; that is, calls of **executeQueryAsync**.</span></span>

```
  function getScheduledOrientations() {

    var hostWebContext = new SP.AppContextSite(clientContext, hostWebURL);
    calendarList = hostWebContext.get_web().get_lists().getByTitle('Employee Orientation Schedule');

    var camlQuery = new SP.CamlQuery();
    scheduledItems = calendarList.getItems(camlQuery);

    clientContext.load(scheduledItems);
    clientContext.executeQueryAsync(scheduleAsNeeded, onGetScheduledItemsFail);
}
```

7. <span data-ttu-id="9581e-p114">Добавьте приведенную ниже функцию в файл. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="9581e-p114">Add the following function to the file. Note the following about this code:</span></span>
    
      - <span data-ttu-id="9581e-p115">Этот метод проверяет, содержится ли название элемента с состоянием **Not Started** (Не начато) в списке **New Employees In Seattle** (Новые сотрудники в Сиэтле), то есть имя сотрудника, в названии события из календаря **Employee Orientation Schedule** (Расписание вводного обучения для сотрудников). При этом для простоты предполагается, что при создании всех записей в календаре в названиях событий используются полные имена сотрудников.</span><span class="sxs-lookup"><span data-stu-id="9581e-p115">The method checks to see if the title of a  **Not Started** item in the **New Employees In Seattle** list, which is the name of an employee, is contained in the title of an event in the **Employee Orientation Schedule** calendar. So there is a simplifying assumption that all entries in the calendar are created with the full employee name in the event title.</span></span>
    
 
  - <span data-ttu-id="9581e-171">Если ни одно из уже имеющихся в календаре событий не совпадает с элементом с состоянием **Not Started** (Не начато), то сценарий создает элемент календаря для элемента с состоянием **Not Started** (Не начато).</span><span class="sxs-lookup"><span data-stu-id="9581e-171">If none of the events that are already on the calendar matches a  **Not Started** item, the script creates a calendar item for the **Not Started** item.</span></span>
    
 
  - <span data-ttu-id="9581e-172">JSOM использует простой объект **ListItemCreationInformation** вместо объекта **SPListItem**, чтобы свести к минимуму объем полезных данных, отправляемых на сервер SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9581e-172">JSOM uses a light weight  **ListItemCreationInformation** object instead of a **SPListItem** object to minimize the size of the payload that is sent to the SharePoint server.</span></span>
    
 
  - <span data-ttu-id="9581e-p116">Двум полям типа DateTime нового события календаря присвоены даты месяца, в котором была написана эта статья:  `2015-06`.  *Измените эти даты на день текущих месяца и года, чтобы не нужно было прокручивать календарь для поиска этих элементов.*</span><span class="sxs-lookup"><span data-stu-id="9581e-p116">The two DateTime fields of the new calendar event are set to days in the month when this article was written:  `2015-06`.  *Change these dates to a day in the current month and year, so you don't have to scroll back in your calendar to find the items.*</span></span> 
    
 
  - <span data-ttu-id="9581e-p117">Если в расписании не будет обнаружено элементов с состоянием **Not Started** (Не начато), то первый элемент будет внесен в расписание на 10-е число месяца. Каждый последующий элемент, которого нет в расписании, будет вноситься в расписание со сдвигом на один день. Для простоты в примере предполагается, что элементов не так много и они не будут запланированы на несуществующие дни месяца, например на 32-е число.</span><span class="sxs-lookup"><span data-stu-id="9581e-p117">If any  **Not Started** items are found to be unscheduled, the first one will be scheduled for the 10th of the month. Each additional unscheduled item will be scheduled for a day later. The simplifying assumption is that there won't be so many that some are scheduled for impossible days of the month, such as "32".</span></span>
    
 
  - <span data-ttu-id="9581e-p118">Большая часть этого кода представляет собой стандартный JavaScript. Строки с использованием модели JSOM SharePoint прокомментированы.</span><span class="sxs-lookup"><span data-stu-id="9581e-p118">Most of this code is standard JavaScript. There are comments for the lines that use SharePoint JSOM.</span></span>
    
 

```
  function scheduleAsNeeded() {

    var unscheduledItems = false;
    var dayOfMonth = '10';

    var listItemEnumerator = notStartedItems.getEnumerator();

    while (listItemEnumerator.moveNext()) {
        var alreadyScheduled = false;
        var notStartedItem = listItemEnumerator.get_current();

        var calendarEventEnumerator = scheduledItems.getEnumerator();
        while (calendarEventEnumerator.moveNext()) {
            var scheduledEvent = calendarEventEnumerator.get_current();

             // The SP.ListItem.get_item('field_name ') method gets the value of the specified field.
            if (scheduledEvent.get_item('Title').indexOf(notStartedItem.get_item('Title')) > -1) {
                alreadyScheduled = true;
                break;
            }
        }
        if (alreadyScheduled === false) {

             // SP.ListItemCreationInformation holds the information the SharePoint server needs to
             // create a list item
            var calendarItem = new SP.ListItemCreationInformation();

             // The some_list .additem method tells the server which list to add 
             // the item to.
            var itemToCreate = calendarList.addItem(calendarItem);

             // The some_item .set_item method sets the value of the specified field.
            itemToCreate.set_item('Title', 'Orient ' + notStartedItem.get_item('Title'));

             // The EventDate and EndDate are the start and stop times of an event.
            itemToCreate.set_item('EventDate', '2015-06-' + dayOfMonth + 'T21:00:00Z');
            itemToCreate.set_item('EndDate', '2015-06-' + dayOfMonth + 'T23:00:00Z');
            dayOfMonth++;

             // The update method tells the server to commit the changes to the SharePoint database.
            itemToCreate.update();
            unscheduledItems = true;
        }
    }
    if (unscheduledItems) {
        calendarList.update();
        clientContext.executeQueryAsync(onScheduleItemsSuccess, onScheduleItemsFail);
    }
}
```

8. <span data-ttu-id="9581e-180">Добавьте указанный ниже обработчик успешного выполнения, который вызывается при добавлении элементов, которых ранее не было в расписании, в календарь.</span><span class="sxs-lookup"><span data-stu-id="9581e-180">Add the following success handler that is called when the previously unscheduled items are added to the calendar.</span></span>
    
```
  function onScheduleItemsSuccess() {
    alert('There was one or more unscheduled orientations and they have been added to the '
              + 'Employee Orientation Schedule calendar.');
}
```

9. <span data-ttu-id="9581e-181">Добавьте приведенные ниже функции в раздел файла с функциями обратного вызова для обработки неудачного выполнения.</span><span class="sxs-lookup"><span data-stu-id="9581e-181">Add the following failure functions to the Failure callbacks section of the file.</span></span>
    
```
  function onGetNotStartedItemsFail(sender, args) {
    alert('Unable to get the not-started items. Error:' 
        + args.get_message() + '\n' + args.get_stackTrace());
}

function onGetScheduledItemsFail(sender, args) {
    alert('Unable to get scheduled items from host web. Error:' 
        + args.get_message() + '\n' + args.get_stackTrace());
}

function onScheduleItemsFail(sender, args) {
    alert('Unable to schedule items on host web calendar. Error:' 
        + args.get_message() + '\n' + args.get_stackTrace());
}
```

10. <span data-ttu-id="9581e-182">Откройте файл default.aspx и найдите элемент **asp:Content** с идентификатором **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="9581e-182">Open the default.aspx file and find the  **asp:Content** element with the ID **PlaceHolderMain**.</span></span>
    
 
11. <span data-ttu-id="9581e-183">Добавьте приведенную ниже часть кода непосредственно под кнопкой `purgeCompletedItems`.</span><span class="sxs-lookup"><span data-stu-id="9581e-183">Add the following markup just below the  `purgeCompletedItems` button.</span></span>
    
```HTML
  <p><asp:Button runat="server" OnClientClick="return ensureOrientationScheduling()" 
  ID="ensureorientationschedulingbutton" Text="Ensure all items are on the Calendar" /></p>
```

12. <span data-ttu-id="9581e-184">Заново выполните сборку проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9581e-184">Rebuild the project in Visual Studio.</span></span>
    
 
13. <span data-ttu-id="9581e-p119">Чтобы при тестировании надстройки вам не приходилось вручную задавать значение "Not Started" (Не начато) для всех полей **Orientation Stage** (Этап обучения), откройте файл elements.xml для экземпляра списка **NewEmployeesInSeattle** (не для шаблона списка **NewEmployeeOrientation**) и убедитесь, что для параметра "Orientation Stage" трех последних элементов **Row**, *включая строку для Cassie Hicks*, задано значение "Not Started" (Не начато). Это значение используется по умолчанию, поэтому самый простой способ сделать это — убедиться в отсутствии элементов **Field** для столбца `OrientationStage` этих трех (или более) строк.</span><span class="sxs-lookup"><span data-stu-id="9581e-p119">To minimize the need to manually set the  **Orientation Stage** of list items toNot Started while testing the add-in, open the elements.xml file for the list instance **NewEmployeesInSeattle** (not the elements.xml for the list template **NewEmployeeOrientation**) and ensure that the Orientation Stage value for at least three of the  **Row** elements, *including the row for Cassie Hicks*  will have the valueNot Started. Since that is the default value, the simplest way to do this is to ensure that there is no  **Field** element for `OrientationStage` for the three (or more) rows.</span></span>
    
    <span data-ttu-id="9581e-187">Ниже показано, как должен выглядеть элемент **Rows**.</span><span class="sxs-lookup"><span data-stu-id="9581e-187">The following is an example of how the  **Rows** element should look.</span></span>
    


```
  <Rows>
  <Row>
    <Field Name="Title">Tom Higginbotham</Field>
    <Field Name="Division">Manufacturing</Field>
    <Field Name="OrientationStage">Completed</Field>
  </Row>
  <Row>
    <Field Name="Title">Satomi Hayakawa</Field>
  </Row>
  <Row>
    <Field Name="Title">Cassi Hicks</Field>
  </Row>
  <Row>
    <Field Name="Title">Lertchai Treetawatchaiwong</Field>
  </Row>
</Rows>
```


## <a name="specify-the-permissions-to-the-host-web-that-the-add-in-needs"></a><span data-ttu-id="9581e-188">Установка необходимых надстройке разрешений для хост-сайта</span><span class="sxs-lookup"><span data-stu-id="9581e-188">Specify the permissions to the host web that the add-in needs</span></span>

<span data-ttu-id="9581e-p120">Ваша надстройка автоматически получает разрешение на полный контроль над ее сайтом, поэтому до сих пор вам не нужно было указывать, какие разрешения необходимы для надстройки. Для взаимодействия с данными на хост-сайте вам потребуется отдельно запросить разрешения на доступ к хост-сайту. Надстройке Employee Orientation необходимо разрешение для добавления элементов в календарь на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="9581e-p120">Your add-in automatically has full control permission to its own add-in web, so until now you have not needed to specify what permissions it needs. But you must specifically request permissions to the host web to interact with its data. The Employee Orientation add-in needs permission to add items to the calendar in the host web.</span></span> 
 

 

1. <span data-ttu-id="9581e-192">В **обозревателе решений** откройте файл appmanifest.xml.</span><span class="sxs-lookup"><span data-stu-id="9581e-192">From  **Solution Explorer**, open the appmanifest.xml file.</span></span> 
    
 
2. <span data-ttu-id="9581e-193">В конструкторе манифеста перейдите на вкладку **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="9581e-193">In the manifest designer, open the  **Permissions** tab.</span></span>
    
 
3. <span data-ttu-id="9581e-194">В раскрывающемся списке из верхней строки столбца **Область** выберите значение **Список**.</span><span class="sxs-lookup"><span data-stu-id="9581e-194">In the top row of the  **Scope** column, choose **List** from the drop down.</span></span>
    
 
4. <span data-ttu-id="9581e-195">В столбце **Разрешение** выберите **Управление**.</span><span class="sxs-lookup"><span data-stu-id="9581e-195">In the  **Permission** column, choose **Manage**.</span></span>
    
 
5. <span data-ttu-id="9581e-p121">Если оставить столбец **Свойства** пустым, надстройка будет запрашивать разрешение на запись в каждый список на хост-сайте. Рекомендуем предоставлять надстройкам только те разрешения, которые необходимы для их работы. В манифесте надстройки невозможно предоставить разрешения только для определенного экземпляра списка, но можно предоставить надстройке разрешения только для тех экземпляров, которые созданы на основе определенного базового шаблона. Базовый шаблон списка календаря — это шаблон **Events** с числовым идентификатором 106.</span><span class="sxs-lookup"><span data-stu-id="9581e-p121">If the  **Properties** column is left blank, then the add-in is asking for write permission to every list on the host web. It is a good practice to limit add-ins to only the permissions that they need. There isn't any way, in the add-in manifest, to limit permissions to a specific list instance, but it is possible to limit the add-in to only list instances that are built on a specific base list template. The base list template of a calendar is **Events** whose numeric ID is 106.</span></span>
    
    <span data-ttu-id="9581e-p122">В той же строке нажмите ячейку **Свойства**, чтобы в ней появилась кнопка **Изменить**. Теперь список разрешений должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="9581e-p122">Click the  **Properties** cell of the same row to make the **Edit** button appear in the cell. The permissions list should now look similar to the following:</span></span>
    

    <span data-ttu-id="9581e-202">**Список разрешений с кнопкой "Изменить"**</span><span class="sxs-lookup"><span data-stu-id="9581e-202">**Permission list with Edit button visible**</span></span>

 

  ![Список разрешений на вкладке "Разрешения" в надстройке "Конструктор манифестов" для Visual Studio с кнопкой "Редактировать", видимой в ячейке столбца "Свойства"](../images/03780b79-aca8-44d1-b0bf-d80833d08627.PNG)
 

 

 
6. <span data-ttu-id="9581e-204">Нажмите кнопку **Изменить**. Откроется диалоговое окно **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="9581e-204">Choose  **Edit** to open the **Properties** dialog.</span></span>
    
 
7. <span data-ttu-id="9581e-p123">Задайте для параметра **Имя** значение BaseTemplateID, а для параметра **Значение** — 106. Теперь диалоговое окно должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="9581e-p123">Set  **Name** toBaseTemplateID, set  **Value** to106. The dialog should now look like the following:</span></span>
    
    <span data-ttu-id="9581e-207">**Диалоговое окно свойств разрешений списка**</span><span class="sxs-lookup"><span data-stu-id="9581e-207">**List permission properties dialog**</span></span>

 

  ![Диалоговое окно свойств для разрешений списка в Visual Studio, где для свойства задано имя "Базовый код списка" и значение 106.](../images/13773fdd-5606-4f35-b8d5-14aad54cffb7.PNG)
 

    <span data-ttu-id="9581e-p124">Нажмите кнопку **ОК**. Теперь вкладка **Разрешения** должна выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="9581e-p124">Choose  **OK**. The  **Permissions** tab should now look similar to the following:</span></span>
    

    <span data-ttu-id="9581e-211">**Вкладка разрешений в конструкторе манифеста надстройки в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9581e-211">**Permissions tab of add-in manifest designer in Visual Studio**</span></span>

 

  ![Вкладка "Разрешения" в надстройке "Конструктор манифестов" для Visual Studio, показывающая, что этой надстройке нужно разрешение управления для списков с базовым типом 106.](../images/14d5a820-ab44-4d12-98de-6672884bf344.PNG)
 

 

 

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="9581e-213">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="9581e-213">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="9581e-p125">Убедитесь, что календарь хост-сайта подготовлен, как описано ранее в данной статье. В нем должно быть одно событие с именем "Orient Cassi Hicks" (Вводное обучение для Cassi Hicks).</span><span class="sxs-lookup"><span data-stu-id="9581e-p125">Be sure the host web calendar is prepared as described earlier in this article. It should have a single event, named "Orient Cassi Hicks".</span></span>
    
 
2. <span data-ttu-id="9581e-216">Включите всплывающие окна в браузере, который Visual Studio использует при отладке.</span><span class="sxs-lookup"><span data-stu-id="9581e-216">Enable popups on the browser that Visual Studio uses when you debug.</span></span>
    
 
3. <span data-ttu-id="9581e-p126">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="9581e-p126">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
4. <span data-ttu-id="9581e-p127">Откроется форма согласия на предоставление разрешений, в которой вы можете предоставить надстройке необходимые ей разрешения. На странице имеется раскрывающийся список, в котором представлены все календари на хост-сайте. Выберите **Расписание вводного обучения для сотрудников**, а затем нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="9581e-p127">The permission consent form opens where you can grant the add-in the permission it seeks. There is a drop down list on the page where you can choose from among all the calendars on the host web. Choose  **Employee Orientation Schedule**, and then choose  **Trust It**.</span></span>
    
    <span data-ttu-id="9581e-222">**Запрос согласия для надстройки SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9581e-222">**SharePoint Add-in consent prompt**</span></span>

 

  ![Запрос согласия в надстройке SharePoint с кратким описанием разрешений, необходимых для надстройки, а также кнопками "Доверять" и "Отмена".](../images/99209248-8927-4fc2-abfc-53d530376516.PNG)
 

 

 
5. <span data-ttu-id="9581e-224">После полной загрузки начальной страницы надстройки нажмите кнопку **Добавить элементы в расписание**.</span><span class="sxs-lookup"><span data-stu-id="9581e-224">When the add-in's start page has completely loaded, choose the  **Ensure Items are Scheduled** button.</span></span>
    
    <span data-ttu-id="9581e-225">**Домашняя страница надстройки "Employee Orientation" (Обучение сотрудников) с новой кнопкой**</span><span class="sxs-lookup"><span data-stu-id="9581e-225">**Employee Orientation home page with new button**</span></span>

 

  ![Домашняя страница надстройки "Employee Orientation" (Обучение сотрудников) с новой кнопкой с надписью "Ensure Items are Scheduled" (Добавить элементы в расписание).](../images/72b78f79-78c0-41db-90d5-8f67e1c17b0e.PNG)
 

 

 
6. <span data-ttu-id="9581e-p128">В случае выполнения какой-либо из функций обратного вызова для обработки сбоев вы увидите созданное ею сообщение об ошибке. В противном случае появится сообщение об успешном выполнении, созданное последней функцией обратного вызова: **There was one or more unscheduled orientations and they have been added to the Employee Orientation Schedule calendar** (Обнаружена одна или несколько незапланированных задач обучения, и они были добавлены в календарь с расписанием вводного обучения для сотрудников).</span><span class="sxs-lookup"><span data-stu-id="9581e-p128">If any of the failure callback functions is run, you will see the error message alert that your callback functions create. Otherwise, you will see the success message created by the final success callback:  **There was one or more unscheduled orientations and they have been added to the Employee Orientation Schedule calendar.**.</span></span>
    
 
7. <span data-ttu-id="9581e-p129">Перейдите к календарю **Employee Orientation Schedule** (Расписание вводного обучения для сотрудников) на хост-сайте. Например, перейдите по ссылке навигации на начальную страницу сайта разработчика, а затем выберите **Содержимое сайта**. Затем выберите плитку **Employee Orientation Schedule** (Расписание вводного обучения для сотрудников), но не плитку **Employee Orientation** (Обучение сотрудников).</span><span class="sxs-lookup"><span data-stu-id="9581e-p129">Navigate to the  **Employee Orientation Schedule** calendar on the host web. For example, choose the breadcrumb link to your developer site's home page and choose **Site Contents**. Then choose the  **Employee Orientation Schedule** tile (not the **Employee Orientation** tile).</span></span>
    
    <span data-ttu-id="9581e-p130">Календарь должен выглядеть примерно так, как показано ниже. В ходе выполнения сценария было обнаружено, что уже имеется событие для Cassi Hicks, поэтому еще одно событие для нее не создавалось. Вместо этого были созданы события для двух других сотрудников с состоянием обучения **Not Started** (Не начато). Кроме того, не было создано событие для сотрудника, чей процесс вводного обучения уже прошел этап **Not Started** (Не начато).</span><span class="sxs-lookup"><span data-stu-id="9581e-p130">The calendar should look similar to the following. The script detected that there was already an event for Cassi Hicks, so it did not create a second one for her. It created events for the other two employees whose orientation was in the  **Not Started** state. It also did not create an event for the employee whose orientation was past the **Not Started** state.</span></span>
    

    <span data-ttu-id="9581e-236">**Календарь после добавления двух новых событий**</span><span class="sxs-lookup"><span data-stu-id="9581e-236">**Calendar after two new events added**</span></span>

 

  ![Календарь "Employee Orientation" (Обучение сотрудников) с новыми событиями, добавленными для обучения двух сотрудников 10-го и 11-го числа месяца](../images/f8037509-4bf1-4c69-a673-ee6fe0f0dcb7.PNG)
 

 

 
8.  <span data-ttu-id="9581e-238">*Прежде чем еще раз нажать кнопку **Ensure Items are Scheduled** (Добавить элементы в расписание), обязательно удалите два новых события из календаря.*</span><span class="sxs-lookup"><span data-stu-id="9581e-238">*Be sure you delete the two new events from the calendar before you press the  **Ensure Items are Scheduled** again.*</span></span> 
    
 
9. <span data-ttu-id="9581e-p131">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="9581e-p131">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
10. <span data-ttu-id="9581e-p132">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="9581e-p132">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="9581e-243"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="9581e-243"></span></span>

<span data-ttu-id="9581e-244">Теперь вы можете перейти к более сложным задачам, связанным с надстройками SharePoint, размещаемыми в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="9581e-244">Go on to advanced work in SharePoint-hosted SharePoint Add-ins:</span></span> 
 

 

-  [<span data-ttu-id="9581e-245">Проектирование надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-245">Design SharePoint Add-ins</span></span>](design-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="9581e-246">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-246">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="9581e-247">Публикация надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-247">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="9581e-248">Средства и среды для разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9581e-248">Tools and environments for developing SharePoint Add-ins</span></span>](tools-and-environments-for-developing-sharepoint-add-ins.md)
    
 

