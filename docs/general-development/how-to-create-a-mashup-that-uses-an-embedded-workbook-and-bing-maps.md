---
title: "Как создать веб-приложения, использующего внедренной книги и карт Bing"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3cfeb8d7-84b8-4673-bc92-b176cba4ac3e
ms.openlocfilehash: 4fd4caf9c77aec37a888fd74cf819037e7372af1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-mashup-that-uses-an-embedded-workbook-and-bing-maps"></a>Как: Создание веб-приложения, использующего внедренной книги и карт Bing

В этой статье рассматриваются основные мощные веб-веб-приложения, который объединяет внедренные книги Excel и Bing Maps.
  
    
    


## <a name="about-the-destination-explorer"></a>О «Explorer назначения»

Обозреватель назначения — веб-приложения, позволяющий пользователю выбрать нужную область, конечный тип (Город или приостановки), определенное назначение внутри области и попытайтесь сведений о погоде или посетителей с расположением за месяц.
  
    
    
Когда пользователь выбирает различные параметры в пользовательском Интерфейсе, JavaScript используется для обработки событий и передайте изменения в книгу на OneDrive. Книга пересчитывает самого на основании изменений и уведомляет Explorer назначения после завершения с помощью функции обратного вызова. В зависимости от того, что пользователь было изменено Explorer назначения может получить дополнительные данные из книги поездки, обновите представление карты Bing, скрыть диаграмм либо замены диаграммы, в настоящее время, на котором отображается.
  
    
    
 **«Командировки книги»**
  
    
    
Конечный Explorer сильно зависит от внедренной книги, содержащий все назначения имена, статистика для прогноза погоды и числа посетителей и две диаграммы для отображения данных ежемесячный прогноза погоды и ежемесячный данных обхода.
  
    
    
 **API JavaScript служб Excel**
  
    
    
Веб-приложения с помощью интерфейса API JavaScript служб Excel для внедрения книги и взаимодействовать с ним. Чтобы использовать API JavaScript служб Excel, имеется только для ссылки в исходном расположении API в коде. Получив доступ к API JavaScript служб Excel, можно программными средствами внедрить и работать с книгой Excel.
  
    
    
 **Карты Bing API JavaScript**
  
    
    
Веб-приложения также использует Bing Maps API для отображения в расположениях, выбранные в рабочей книге внутри карты Bing. Так же, как другие библиотеки JavaScript все, что вам потребуется выполнить — Справочник по библиотеке API в коде для включения Bing Map в вашей веб-приложения.
  
    
    

## <a name="creating-the-destination-explorer-mashup"></a>Создание веб-приложения «Explorer назначения»

Чтобы создать данное гибридное приложение, мы за трех основных шагов:
  
    
    

1. Сохранение книги на OneDrive. Получить дополнительные сведения на странице [OneDrive](https://onedrive.live.com/about/en-us/) .
    
  
2. Внедрение книги на странице. Дополнительные сведения по внедрение рабочих книг в OneDrive [здесь](http://office.microsoft.com/en-us/excel-help/share-it-embed-an-excel-workbook-on-your-blog-HA102029502.aspx?CTT=5&amp;origin=HA102775335).
    
  
3. Объединения его с помощью службы Bing Maps. Этот шаг будет рассмотрен в следующих разделах более подробно.
    
  

  
    
    

## <a name="mashup-excel-services-and-bing-maps"></a>В службах Excel веб-приложения и Bing Maps

После сохранения книги в общую папку на OneDrive и внедрение книги на веб-страницу узла функциональные возможности службы Bing Maps в сочетании с взаимодействия для внедренной книги для создания веб-приложения *Explorer назначения* .
  
    
    
Интеграция происходит в следующие три этапа:
  
    
    

- Создание структуры страниц для веб-приложения
    
  
- Инициализация диаграммы внедренной книги и карты Bing
    
  
- Создайте соответствующий обратного вызова функции
    
  

1. **Создание структуры страниц для веб-приложения**
    
    Выберите элемент HTML на странице веб-заполненный данными из книги поездок при загрузке страницы или каждый раз, когда пользователь изменяет текущий регионе или другой тип назначения. Определение для данного элемента управления select ( *назначения* ) показано в **фрагмент 1**. **1 фрагмент** также показаны определения для ключевых элементов на странице: **chartDiv**, **chartDiv2**и **mapDiv**. Элементы div диаграммы являются контейнерами для две диаграммы, определенные в книге командировок. Карта div является контейнером для управления карты Bing.
    
    **Фрагмент 1: Структурирование веб-страницы**
    


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

2. **Инициализация диаграммы внедренной книги и карты Bing**
    
    Следующим шагом является для инициализации компонентов Excel и Bing Map при загрузке страницы. Чтобы получить доступ к внедренной книги Excel программным путем, необходимо сослаться на него в маркер файла. Просмотрите [http://msdn.microsoft.com/en-us/library/hh315812.aspx](http://msdn.microsoft.com/en-us/library/hh315812.aspx%28Office.15%29.aspx) сведения о том, как получить маркер соответствующего файла для книги.
    
    Код в **2 фрагмента** завершает три основных задачи в обработчике событий **Page_Load** . Во-первых устанавливает ссылку на поездки книги для отображения диаграмм, с именем *Диаграмма 1* внутри элемента **chartDiv** на веб-странице. Во-вторых он вызывает простой функции с именем **GetMap** для инициализации карты Bing. В-третьих он создает ссылку на второй Travel книги для отображения диаграмм, с именем *Диаграмма 2* внутри элемента **chartDiv2** .
    
    **Фрагмент 2: Инициализация страницы**
    


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

3. **Создайте соответствующий обратного вызова функции**
    
    Все вызовы функций в API JavaScript служб Excel обычно вступили в функции обратного вызова как параметр. Параметр обратного вызова — имя вашего JavaScript, которая должна выполняться после завершения вызова API JavaScript служб Excel с помощью функции. Вы видите обратный вызов, используемый в функции **EwaControl.loadEwaAsync** в **фрагменте 2**:
    


```
  
Ewa.EwaControl.loadEwaAsync(fileToken, "chartDiv", props, onEwaChartLoaded);
```


    The callback used here is **onEwaChartLoaded**. This launches the following chain of calls to the Excel Services JavaScript API and callbacks within the Destination Explorer. The callbacks used in this chain are:
    
  - **onEwaChartLoaded()** — эта функция сохраняет ссылку для управления веб-клиента Excel, связанные с диаграммой. Когда элемент управления, вызывает метод **getRangeA1Async()** для получения диапазона, представленное имя *OutputTopFiveDetails* .
    
  
  - **onGotDetailRange()** - вызов к **getRangeA1Async()** возвращает диапазона, а не значений, поэтому этот обратного вызова вызывается метод **getValuesAsync()** для получения значения, связанные с диапазоном.
    
  
  - **onGotDetailValues()** - значения, связанные с диапазоном хранятся в переменной для дальнейшего использования, а затем этот метод вызывает следующих методов, определенных в обозревателе назначения:
    
  - Выберите элемент с назначениями в диапазоне *OutputTopFiveDetails* заполняет **loadDestinations()** - 
    
  
  - **updateMap()** - обновляет карты, если это необходимо
    
  
  - диаграмма обновляется **updateChart()** - при необходимости
    
  

    Цепочка обратных вызовов, показано в **фрагмент 3** предназначено для обновлять данные, отображаемые на странице "HTML". Есть другой цепочки функции обратного вызова, используется для изменения данных в книге командировок. Например при изменении региона из Северной Америки в Европе, несколько важных необходимыми повторного заполнения списка назначений, обновление карты и скрытие диаграмм. Повторного заполнения списка назначения — это первое, что должно происходить и это, вам необходимо изменить данные в Excel. **Фрагмент 3** показан код для выполнения этих задач. Обратите внимание, функцию с именем **updateExcel()** и связанные обратного вызова с именем **onGotRange()** обрабатывать операции по связыванию изменение значений на листе входные данные книги командировок.
    
    **Фрагмент 3: Цепочки обратного вызова для изменения исходные данные в книге поездки**
    


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


## <a name="conclusion"></a>Заключение
<a name="bk_addresources"> </a>

В этом пошаговом руководстве описывается пример как разработчиков веб-приложений можно создать насыщенное и интерактивное гибридных веб-приложений с помощью служб Excel и других технологий. 
  
    
    

