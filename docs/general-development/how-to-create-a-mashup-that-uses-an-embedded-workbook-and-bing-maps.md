---
title: "Создание веб-приложения, использующего внедренной книги и карт Bing"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3cfeb8d7-84b8-4673-bc92-b176cba4ac3e
ms.openlocfilehash: 3ffda7629e52045086e8dcd45e97c959058d7951
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-mashup-that-uses-an-embedded-workbook-and-bing-maps"></a><span data-ttu-id="9b866-102">Создание веб-приложения, использующего внедренной книги и карт Bing</span><span class="sxs-lookup"><span data-stu-id="9b866-102">Create a mashup that uses an embedded workbook and Bing Maps</span></span>

<span data-ttu-id="9b866-103">В этой статье рассматриваются основные мощные веб-веб-приложения, который объединяет внедренные книги Excel и Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="9b866-103">This article walks you through a powerful Web-based mashup that combines an embedded Excel workbook and Bing Maps.</span></span>
  
    
    


## <a name="about-the-destination-explorer"></a><span data-ttu-id="9b866-104">О «Explorer назначения»</span><span class="sxs-lookup"><span data-stu-id="9b866-104">About the "Destination Explorer"</span></span>

<span data-ttu-id="9b866-105">Обозреватель назначения — веб-приложения, позволяющий пользователю выбрать нужную область, конечный тип (Город или приостановки), определенное назначение внутри области и попытайтесь сведений о погоде или посетителей с расположением за месяц.</span><span class="sxs-lookup"><span data-stu-id="9b866-105">The Destination Explorer is a mashup that lets the user choose a region, a destination type (city or park), a specific destination within the region, and then see weather information or number of visitors to the destination by month.</span></span>
  
    
    
<span data-ttu-id="9b866-106">Когда пользователь выбирает различные параметры в пользовательском Интерфейсе, JavaScript используется для обработки событий и передайте изменения в книгу на OneDrive.</span><span class="sxs-lookup"><span data-stu-id="9b866-106">When the user selects different options from the UI, JavaScript is used to process the events and pass the changes to the workbook on OneDrive.</span></span> <span data-ttu-id="9b866-107">Книга пересчитывает самого на основании изменений и уведомляет Explorer назначения после завершения с помощью функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="9b866-107">The workbook recalculates itself based on the changes and notifies the Destination Explorer when it is finished using callback functions.</span></span> <span data-ttu-id="9b866-108">В зависимости от того, что пользователь было изменено Explorer назначения может получить дополнительные данные из книги поездки, обновите представление карты Bing, скрыть диаграмм либо замены диаграммы, в настоящее время, на котором отображается.</span><span class="sxs-lookup"><span data-stu-id="9b866-108">Depending on what the user changed, the Destination Explorer may either get more data from the Travel workbook, update the view of the Bing Map, hide the charts, or swap the chart that is currently showing.</span></span>
  
    
    
 <span data-ttu-id="9b866-109">**«Командировки книги»**</span><span class="sxs-lookup"><span data-stu-id="9b866-109">**The "Travel workbook"**</span></span>
  
    
    
<span data-ttu-id="9b866-110">Конечный Explorer сильно зависит от внедренной книги, содержащий все назначения имена, статистика для прогноза погоды и числа посетителей и две диаграммы для отображения данных ежемесячный прогноза погоды и ежемесячный данных обхода.</span><span class="sxs-lookup"><span data-stu-id="9b866-110">The Destination Explorer depends heavily on an embedded workbook that contains all the destination names, statistics for weather and visitor numbers, and two charts for displaying monthly weather data and monthly visitor data.</span></span>
  
    
    
 <span data-ttu-id="9b866-111">**API JavaScript служб Excel**</span><span class="sxs-lookup"><span data-stu-id="9b866-111">**Excel Services JavaScript API**</span></span>
  
    
    
<span data-ttu-id="9b866-112">Веб-приложения с помощью интерфейса API JavaScript служб Excel для внедрения книги и взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="9b866-112">The mashup uses the Excel Services JavaScript API to embed the workbook and to interact with it.</span></span> <span data-ttu-id="9b866-113">Чтобы использовать API JavaScript служб Excel, имеется только для ссылки в исходном расположении API в коде.</span><span class="sxs-lookup"><span data-stu-id="9b866-113">To use the Excel Services JavaScript API, you only have to reference the API source location in your code.</span></span> <span data-ttu-id="9b866-114">Получив доступ к API JavaScript служб Excel, можно программными средствами внедрить и работать с книгой Excel.</span><span class="sxs-lookup"><span data-stu-id="9b866-114">Once you have access to the Excel Services JavaScript API, you can programmatically embed and work with an Excel workbook.</span></span>
  
    
    
 <span data-ttu-id="9b866-115">**Карты Bing API JavaScript**</span><span class="sxs-lookup"><span data-stu-id="9b866-115">**Bing Maps JavaScript API**</span></span>
  
    
    
<span data-ttu-id="9b866-116">Веб-приложения также использует Bing Maps API для отображения в расположениях, выбранные в рабочей книге внутри карты Bing.</span><span class="sxs-lookup"><span data-stu-id="9b866-116">The mashup also uses the Bing Maps API to display the locations selected on the workbook inside a Bing Map.</span></span> <span data-ttu-id="9b866-117">Так же, как другие библиотеки JavaScript все, что вам потребуется выполнить — Справочник по библиотеке API в коде для включения Bing Map в вашей веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9b866-117">Just like any other JavaScript library, all you have to do is reference the API library in your code in order to include a Bing Map in your mashup.</span></span>
  
    
    

## <a name="creating-the-destination-explorer-mashup"></a><span data-ttu-id="9b866-118">Создание веб-приложения «Explorer назначения»</span><span class="sxs-lookup"><span data-stu-id="9b866-118">Creating the "Destination Explorer" Mashup</span></span>

<span data-ttu-id="9b866-119">Чтобы создать данное гибридное приложение, мы за трех основных шагов:</span><span class="sxs-lookup"><span data-stu-id="9b866-119">To create this mashup, we followed 3 basic steps:</span></span>
  
    
    

1. <span data-ttu-id="9b866-120">Сохранение книги на OneDrive.</span><span class="sxs-lookup"><span data-stu-id="9b866-120">Store the workbook on OneDrive.</span></span> <span data-ttu-id="9b866-121">Получить дополнительные сведения на странице [OneDrive](https://onedrive.live.com/about/en-us/) .</span><span class="sxs-lookup"><span data-stu-id="9b866-121">Find more information on the  [OneDrive](https://onedrive.live.com/about/en-us/) page.</span></span>
    
  
2. <span data-ttu-id="9b866-122">Внедрение книги на странице.</span><span class="sxs-lookup"><span data-stu-id="9b866-122">Embed the workbook on the page.</span></span> <span data-ttu-id="9b866-123">Дополнительные сведения по внедрение рабочих книг в OneDrive [здесь](http://office.microsoft.com/en-us/excel-help/share-it-embed-an-excel-workbook-on-your-blog-HA102029502.aspx?CTT=5&amp;origin=HA102775335).</span><span class="sxs-lookup"><span data-stu-id="9b866-123">Find more information on embedding workbooks from OneDrive  [here](http://office.microsoft.com/en-us/excel-help/share-it-embed-an-excel-workbook-on-your-blog-HA102029502.aspx?CTT=5&amp;origin=HA102775335).</span></span>
    
  
3. <span data-ttu-id="9b866-124">Объединения его с помощью службы Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="9b866-124">Mash it up with Bing Maps.</span></span> <span data-ttu-id="9b866-125">Этот шаг будет рассмотрен в следующих разделах более подробно.</span><span class="sxs-lookup"><span data-stu-id="9b866-125">This step is covered in more detail in the following sections.</span></span>
    
  

  
    
    

## <a name="mashup-excel-services-and-bing-maps"></a><span data-ttu-id="9b866-126">В службах Excel веб-приложения и Bing Maps</span><span class="sxs-lookup"><span data-stu-id="9b866-126">Mashup Excel Services and Bing Maps</span></span>

<span data-ttu-id="9b866-127">После сохранения книги в общую папку на OneDrive и внедрение книги на веб-страницу узла функциональные возможности службы Bing Maps в сочетании с взаимодействия для внедренной книги для создания веб-приложения *Explorer назначения* .</span><span class="sxs-lookup"><span data-stu-id="9b866-127">After storing the workbook in a public folder on OneDrive, and after embedding the workbook on the host web page, the Bing Maps functionality is combined with interactions on the embedded workbook to create the  *Destination Explorer*  Mashup.</span></span>
  
    
    
<span data-ttu-id="9b866-128">Интеграция происходит в следующие три этапа:</span><span class="sxs-lookup"><span data-stu-id="9b866-128">The integration happens in the following 3 steps:</span></span>
  
    
    

- <span data-ttu-id="9b866-129">Создание структуры страниц для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9b866-129">Create the page structure for the mashup</span></span>
    
  
- <span data-ttu-id="9b866-130">Инициализация диаграммы внедренной книги и карты Bing</span><span class="sxs-lookup"><span data-stu-id="9b866-130">Initialize the embedded workbook charts and the Bing Map</span></span>
    
  
- <span data-ttu-id="9b866-131">Создайте соответствующий обратного вызова функции</span><span class="sxs-lookup"><span data-stu-id="9b866-131">Create the appropriate callback functions</span></span>
    
  

1. <span data-ttu-id="9b866-132">**Создание структуры страниц для веб-приложения**</span><span class="sxs-lookup"><span data-stu-id="9b866-132">**Create the page structure for the mashup**</span></span>
    
    <span data-ttu-id="9b866-133">Выберите элемент HTML на странице веб-заполненный данными из книги поездок при загрузке страницы или каждый раз, когда пользователь изменяет текущий регионе или другой тип назначения.</span><span class="sxs-lookup"><span data-stu-id="9b866-133">An HTML select control on the web page is populated with data from the Travel workbook when the page loads or whenever the user changes the current region or the destination type.</span></span> <span data-ttu-id="9b866-134">Определение для данного элемента управления select ( *назначения* ) показано в **фрагмент 1**.</span><span class="sxs-lookup"><span data-stu-id="9b866-134">The definition for this select control ( *destinations*  ) is shown in **Snippet 1**.</span></span> <span data-ttu-id="9b866-135">**1 фрагмент** также показаны определения для ключевых элементов на странице: **chartDiv**, **chartDiv2**и **mapDiv**.</span><span class="sxs-lookup"><span data-stu-id="9b866-135">**Snippet 1** also shows the definition for the other key elements on the page: **chartDiv**, **chartDiv2**, and **mapDiv**.</span></span> <span data-ttu-id="9b866-136">Элементы div диаграммы являются контейнерами для две диаграммы, определенные в книге командировок.</span><span class="sxs-lookup"><span data-stu-id="9b866-136">The chart div elements are containers for the two charts defined in the Travel workbook.</span></span> <span data-ttu-id="9b866-137">Карта div является контейнером для управления карты Bing.</span><span class="sxs-lookup"><span data-stu-id="9b866-137">The map div is the container for the Bing Map control.</span></span>
    
    <span data-ttu-id="9b866-138">**Фрагмент 1: Структурирование веб-страницы**</span><span class="sxs-lookup"><span data-stu-id="9b866-138">**Snippet 1: Structuring the web page**</span></span>
    


```HTML
  
<!-- HTML omitted for brevity -->
    <select id="destinations" style="width: 150px" name="destinations"
      onchange="onDestinationChange()">
    </select>
    <!-- HTML omitted for brevity -->
    <div id="chartDiv" style="width: 483px; height: 318px"></div>
    <div id="chartDiv2" style="width: 483px; height: 318px; display: none"></div>
    <!-- HTML omitted for brevity -->
    <div id="mapDiv" style="position:relative; width:693px; height:400px;"></div>
    <!-- HTML omitted for brevity -->

```

2. <span data-ttu-id="9b866-139">**Инициализация диаграммы внедренной книги и карты Bing**</span><span class="sxs-lookup"><span data-stu-id="9b866-139">**Initialize the embedded workbook charts and the Bing Map**</span></span>
    
    <span data-ttu-id="9b866-140">Следующим шагом является для инициализации компонентов Excel и Bing Map при загрузке страницы.</span><span class="sxs-lookup"><span data-stu-id="9b866-140">The next step is to initialize the Excel components and the Bing Map when the page loads.</span></span> <span data-ttu-id="9b866-141">Чтобы получить доступ к внедренной книги Excel программным путем, необходимо сослаться на него в маркер файла.</span><span class="sxs-lookup"><span data-stu-id="9b866-141">In order to access an embedded Excel workbook programmatically, you need to refer to it by a file token.</span></span> <span data-ttu-id="9b866-142">Просмотрите [http://msdn.microsoft.com/en-us/library/hh315812.aspx](http://msdn.microsoft.com/en-us/library/hh315812.aspx%28Office.15%29.aspx) сведения о том, как получить маркер соответствующего файла для книги.</span><span class="sxs-lookup"><span data-stu-id="9b866-142">See  [http://msdn.microsoft.com/en-us/library/hh315812.aspx](http://msdn.microsoft.com/en-us/library/hh315812.aspx%28Office.15%29.aspx) for information on how to get the appropriate file token for your workbook.</span></span>
    
    <span data-ttu-id="9b866-143">Код в **2 фрагмента** завершает три основных задачи в обработчике событий **Page_Load** .</span><span class="sxs-lookup"><span data-stu-id="9b866-143">The code in **Snippet 2** completes three main tasks inside the **Page_Load** event handler.</span></span> <span data-ttu-id="9b866-144">Во-первых устанавливает ссылку на поездки книги для отображения диаграмм, с именем *Диаграмма 1* внутри элемента **chartDiv** на веб-странице.</span><span class="sxs-lookup"><span data-stu-id="9b866-144">First, it establishes a reference to the Travel workbook to display the chart named *Chart 1*  inside the **chartDiv** element on the web page.</span></span> <span data-ttu-id="9b866-145">Во-вторых он вызывает простой функции с именем **GetMap** для инициализации карты Bing.</span><span class="sxs-lookup"><span data-stu-id="9b866-145">Second, it calls a simple function named **GetMap** to initialize the Bing Map.</span></span> <span data-ttu-id="9b866-146">В-третьих он создает ссылку на второй Travel книги для отображения диаграмм, с именем *Диаграмма 2* внутри элемента **chartDiv2** .</span><span class="sxs-lookup"><span data-stu-id="9b866-146">Third, it creates a second reference to the Travel workbook to display the chart named *Chart 2*  inside the **chartDiv2** element.</span></span>
    
    <span data-ttu-id="9b866-147">**Фрагмент 2: Инициализация страницы**</span><span class="sxs-lookup"><span data-stu-id="9b866-147">**Snippet 2: Initializing the Page**</span></span>
    


```
  
// Use this file token to reference your OneDrive hosted workbook in Excel's APIs
    var fileToken = "TOKEN TO YOUR WORKBOOK GOES HERE";
    var map;
    var ewaChart = null;
    var ewaChart2 = null;
  
    // Set the page event handlers for onload and unload.
    if (window.attachEvent) {
    window.attachEvent("onload", Page_Load);
    }
    else {
    // For some browsers window.attachEvent does not exist.
    window.addEventListener("DOMContentLoaded", Page_Load, false);
    }
  
    hideCharts();
     
    // Page load event handler
    function Page_Load() {
     
    // Load Excel Chart
    var props = {
    item: "Chart 1",
    uiOptions: {
    showParametersTaskPane: false
    },
    interactivityOptions: {
    allowTypingAndFormulaEntry: true,
    allowParameterModification: false,
    allowSorting: false,
    allowFiltering: false,
    allowPivotTableInteractivity: false
    }
    };
    Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv", props, onEwaChartLoaded);
     
    // Load the Bing map
    GetMap();

    // Load the 2nd Excel Chart
    var props = {
    item: "Chart 2",
    uiOptions: {
    showParametersTaskPane: false
    },
    interactivityOptions: {
    allowTypingAndFormulaEntry: true,
    allowParameterModification: false,
    allowSorting: false,
    allowFiltering: false,
    allowPivotTableInteractivity: false
    }
    };
    Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv2", props, onEwaChart2Loaded);
    }
     
    // Setup the Bing Map's initial view
    function GetMap() {
     
    map = new Microsoft.Maps.Map(document.getElementById("mapDiv"),
    { credentials: "YOUR CREDENTIALS",
    center: new Microsoft.Maps.Location(37.2802459560, -112.738963),
    mapTypeId: Microsoft.Maps.MapTypeId.road,
    zoom: 3 });

```

3. <span data-ttu-id="9b866-148">**Создайте соответствующий обратного вызова функции**</span><span class="sxs-lookup"><span data-stu-id="9b866-148">**Create the appropriate callback functions**</span></span>
    
    <span data-ttu-id="9b866-149">Все вызовы функций в API JavaScript служб Excel обычно вступили в функции обратного вызова как параметр.</span><span class="sxs-lookup"><span data-stu-id="9b866-149">All calls to functions in the Excel Services JavaScript API usually take a callback as a parameter to the function.</span></span> <span data-ttu-id="9b866-150">Параметр обратного вызова — имя вашего JavaScript, которая должна выполняться после завершения вызова API JavaScript служб Excel с помощью функции.</span><span class="sxs-lookup"><span data-stu-id="9b866-150">The callback parameter is the name of the function in your JavaScript that should be run when the call to the Excel Services JavaScript API completes.</span></span> <span data-ttu-id="9b866-151">Вы видите обратный вызов, используемый в функции **EwaControl.loadEwaAsync** в **фрагменте 2**:</span><span class="sxs-lookup"><span data-stu-id="9b866-151">You can see a callback used in the **EwaControl.loadEwaAsync** function in **Snippet 2**:</span></span>
    


```
  
Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv", props, onEwaChartLoaded);
```


    The callback used here is **onEwaChartLoaded**. This launches the following chain of calls to the Excel Services JavaScript API and callbacks within the Destination Explorer. The callbacks used in this chain are:
    
  - <span data-ttu-id="9b866-152">**onEwaChartLoaded()** — эта функция сохраняет ссылку для управления веб-клиента Excel, связанные с диаграммой.</span><span class="sxs-lookup"><span data-stu-id="9b866-152">**onEwaChartLoaded()** - This function saves a reference to the Excel Web Access Control associated with the chart.</span></span> <span data-ttu-id="9b866-153">Когда элемент управления, вызывает метод **getRangeA1Async()** для получения диапазона, представленное имя *OutputTopFiveDetails* .</span><span class="sxs-lookup"><span data-stu-id="9b866-153">After it has the control, it calls the method **getRangeA1Async()** to get the range represented by the name *OutputTopFiveDetails*  .</span></span>
    
  
  - <span data-ttu-id="9b866-154">**onGotDetailRange()** - вызов к **getRangeA1Async()** возвращает диапазона, а не значений, поэтому этот обратного вызова вызывается метод **getValuesAsync()** для получения значения, связанные с диапазоном.</span><span class="sxs-lookup"><span data-stu-id="9b866-154">**onGotDetailRange()** - The call to **getRangeA1Async()** returns the range, not the values so this callback calls the method **getValuesAsync()** to get the values associated with the range.</span></span>
    
  
  - <span data-ttu-id="9b866-155">**onGotDetailValues()** - значения, связанные с диапазоном хранятся в переменной для дальнейшего использования, а затем этот метод вызывает следующих методов, определенных в обозревателе назначения:</span><span class="sxs-lookup"><span data-stu-id="9b866-155">**onGotDetailValues()** - The values associated with the range are stored in a variable for later use and then this method calls the following methods defined within the Destination Explorer:</span></span>
    
  - <span data-ttu-id="9b866-156">Выберите элемент с назначениями в диапазоне *OutputTopFiveDetails* заполняет **loadDestinations()** -</span><span class="sxs-lookup"><span data-stu-id="9b866-156">**loadDestinations()** - Populates the select element with the destinations within the range *OutputTopFiveDetails*</span></span> 
    
  
  - <span data-ttu-id="9b866-157">**updateMap()** - обновляет карты, если это необходимо</span><span class="sxs-lookup"><span data-stu-id="9b866-157">**updateMap()** - Updates the map if necessary</span></span>
    
  
  - <span data-ttu-id="9b866-158">диаграмма обновляется **updateChart()** - при необходимости</span><span class="sxs-lookup"><span data-stu-id="9b866-158">**updateChart()** - Updates the chart if necessary</span></span>
    
  

    <span data-ttu-id="9b866-159">Цепочка обратных вызовов, показано в **фрагмент 3** предназначено для обновлять данные, отображаемые на странице "HTML".</span><span class="sxs-lookup"><span data-stu-id="9b866-159">The purpose of the chain of callbacks shown in **Snippet 3** is to update the data shown on the HTML page.</span></span> <span data-ttu-id="9b866-160">Есть другой цепочки функции обратного вызова, используется для изменения данных в книге командировок.</span><span class="sxs-lookup"><span data-stu-id="9b866-160">There is another chain of callback functions used to modify data within the Travel workbook.</span></span> <span data-ttu-id="9b866-161">Например при изменении региона из Северной Америки в Европе, несколько важных необходимыми повторного заполнения списка назначений, обновление карты и скрытие диаграмм.</span><span class="sxs-lookup"><span data-stu-id="9b866-161">For example, if you change the region from North America to Europe, several things need to happen such as repopulating the list of destinations, updating the map, and hiding the charts.</span></span> <span data-ttu-id="9b866-162">Повторного заполнения списка назначения — это первое, что должно происходить и это, вам необходимо изменить данные в Excel.</span><span class="sxs-lookup"><span data-stu-id="9b866-162">Repopulating the list of destination is the first thing that needs to happen and this involves modifying data in Excel.</span></span> <span data-ttu-id="9b866-163">**Фрагмент 3** показан код для выполнения этих задач.</span><span class="sxs-lookup"><span data-stu-id="9b866-163">**Snippet 3** shows the code for these tasks.</span></span> <span data-ttu-id="9b866-164">Обратите внимание, функцию с именем **updateExcel()** и связанные обратного вызова с именем **onGotRange()** обрабатывать операции по связыванию изменение значений на листе входные данные книги командировок.</span><span class="sxs-lookup"><span data-stu-id="9b866-164">Note that the function named **updateExcel()** and an associated callback named **onGotRange()** handle the chore of changing values on the Input worksheet of the Travel workbook.</span></span>
    
    <span data-ttu-id="9b866-165">**Фрагмент 3: Цепочки обратного вызова для изменения исходные данные в книге поездки**</span><span class="sxs-lookup"><span data-stu-id="9b866-165">**Snippet 3: The callback chain for modifying inputs in the Travel workbook**</span></span>
    


```
  // Event handler called when user selects a different region.
    function onRegionChange() {
    currentDestination = '';
    var e = document.getElementById("regions");
    currentRegion = e.options[e.selectedIndex].text;
    updateExcel();
    }
     
    // Event handler called when user selects a different destination.
    function onDestinationChange() {
    var select = document.getElementById('destinations');
    var i = select.selectedIndex;
    currentDestination = select.options[i].text;
    updateChart();
    updateMap(false);
    }
    // Event handler called when user selects a different destination type.
    function onTypeChange(type) {
    currentDestination = '';
    currentDestinationType = type;
    updateExcel();
    }
     
    // Called from onTypeChange and onRegionChange when user selects a different destination type or region
    function updateExcel() {
    ewaChart.getActiveWorkbook().getRangeA1Async("Input!Inputs", onGotRange, 0);
    ewaChart2.getActiveWorkbook().getRangeA1Async("Input!Inputs", onGotRange, 1);
    }
     
    // Callback - called from updateExcel - sets input values according to user selections
    function onGotRange(result) {
    var range = result.getReturnValue();
    var values = new Array(2);
    values[0] = new Array(1);
    values[0][0] = currentRegion;
    values[1] = new Array(1);
    values[1][0] = currentDestinationType;
    range.setValuesAsync(values, null, null);
     
    // Initiate process of refreshing the script variable detailRangeValues
    if (result.getUserContext() == 0)
    ewaChart.getActiveWorkbook().getRangeA1Async("Output!OutputTopFiveDetails", onGotDetailRange, null);
    }

```


## <a name="conclusion"></a><span data-ttu-id="9b866-166">Заключение</span><span class="sxs-lookup"><span data-stu-id="9b866-166">Conclusion</span></span>
<span data-ttu-id="9b866-167"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9b866-167"></span></span>

<span data-ttu-id="9b866-168">В этом пошаговом руководстве описывается пример как разработчиков веб-приложений можно создать насыщенное и интерактивное гибридных веб-приложений с помощью служб Excel и других технологий.</span><span class="sxs-lookup"><span data-stu-id="9b866-168">This walkthrough gives an example of how web developers can create rich, interactive mashups using Excel Services and other technologies.</span></span> 
  
    
    

