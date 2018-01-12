---
title: "Общие сведения о службах Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5fa22ebb-e507-4ffc-a425-e755502feae2
ms.openlocfilehash: f460fb94b6a18af7a544006b078995f95ce36e69
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="excel-services-overview"></a><span data-ttu-id="2f0af-102">Общие сведения о службах Excel</span><span class="sxs-lookup"><span data-stu-id="2f0af-102">Excel Services Overview</span></span>

<span data-ttu-id="2f0af-p101">Службы Excel  это приложение службы, позволяющее загружать, вычислять и отображать книги Microsoft Excel в Microsoft SharePoint. Службы Excel впервые представлено в Microsoft Office SharePoint Server 2007.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p101">Excel Services is a service application that enables you to load, calculate, and display Microsoft Excel workbooks on Microsoft SharePoint. Excel Services was first introduced in Microsoft Office SharePoint Server 2007.</span></span>
  
    
    

<span data-ttu-id="2f0af-p102">С помощью Службы Excel можно повторно и совместно использовать книги Excel на порталах и панелях мониторинга SharePoint. Например, финансовые аналитики, бизнес-планировщики или инженеры могут создавать содержимое в Excel и предоставлять его для общего доступа с помощью портала и панели мониторинга SharePoint без написания пользовательского кода. Можно управлять отображением данных и поддерживать единую версию книги Excel. Есть четыре основных интерфейса для Службы Excel:</span><span class="sxs-lookup"><span data-stu-id="2f0af-p102">By using Excel Services, you can reuse and share Excel workbooks on SharePoint portals and dashboards. For example, financial analysts, business planners, or engineers can create content in Excel and share it with others by using an SharePoint portal and dashboard—without writing custom code. You can control what data is displayed, and you can maintain a single version of your Excel workbook. There are four primary interfaces for Excel Services:</span></span> 
  
    
    


- <span data-ttu-id="2f0af-109">Веб-часть Веб-клиент Excel, позволяющая просматривать динамическую книгу с помощью браузера и взаимодействовать с ней</span><span class="sxs-lookup"><span data-stu-id="2f0af-109">An Excel Web Access Web Part, which enables you to view and interact with a live workbook by using a browser</span></span> 
    
  
- <span data-ttu-id="2f0af-110">Веб-службы Excel для программного доступа.</span><span class="sxs-lookup"><span data-stu-id="2f0af-110">Excel Web Services for programmatic access</span></span>
    
  
- <span data-ttu-id="2f0af-111">Объектная модель ECMAScript (JavaScript, JScript) для автоматизации и настройки, контроля элемента управления Веб-клиент Excel, помощи в создании более удобных интегрированных решений, а также для предоставления пользовательских функций для расширения возможностей объектной модели ECMAScript (JavaScript, JScript).</span><span class="sxs-lookup"><span data-stu-id="2f0af-111">An ECMAScript (JavaScript, JScript) object model for automating and customizing, and to drive the Excel Web Access control and help build more compelling, integrated solutions as well as the ability to user user-defined functions to extend the ECMAScript (JavaScript, JScript) object model</span></span>
    
  
- <span data-ttu-id="2f0af-112">Интерфейс REST API для доступа к частям книг непосредственно по URL-адресу</span><span class="sxs-lookup"><span data-stu-id="2f0af-112">A Representational State Transfer (REST) API for accessing workbook parts directly through a URL</span></span>
    
> [!NOTE]
> <span data-ttu-id="2f0af-p103">[!Примечание] Функция интерактивного представления Excel отключена. Сведения об удалении этой функции из вашего веб-сайта см. в разделе  [Удаление интерактивное представление Excel из веб-страницы](removing-excel-interactive-view-from-a-webpage.md).</span><span class="sxs-lookup"><span data-stu-id="2f0af-p103">The Excel Interactive View feature has been disabled. For information about removing this feature from your website, see  [Removing Excel Interactive View from a webpage](removing-excel-interactive-view-from-a-webpage.md).</span></span> 
  
    
    

<span data-ttu-id="2f0af-115">Вы также можете расширять службы вычислений Excel с помощью пользовательских функций (UDF).</span><span class="sxs-lookup"><span data-stu-id="2f0af-115">You can also extend Excel Calculation Services by using user-defined functions (UDFs).</span></span>

> [!NOTE]
> <span data-ttu-id="2f0af-116">Дополнительные сведения о службах вычислений Excel см. в статье [Архитектура служб Excel](excel-services-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="2f0af-116">[Note:](excel-services-architecture.md) For more information about Excel Calculation Services, see  Excel Services Architecture.</span></span> 
  
    
    

<span data-ttu-id="2f0af-p104">С помощью Службы Excel можно просматривать интерактивные книги с помощью только браузера. Это означает, что можно сохранять книги Excel и взаимодействовать с ними из сайтов портала.Также можно взаимодействовать с данными на основе Excel путем сортировки, фильтрации, развертывания или свертывания сводных таблиц, а также передачи в них параметров; это предоставляет возможность выполнения анализа опубликованных книг. Можно взаимодействовать с книгой без изменения опубликованной книги, что ценно для авторов и потребителей отчетов.Службы Excel поддерживает книги, подключенные к внешним источникам данных. Можно внедрять строки подключения к внешним источникам данных в книгу или сохранять их централизованно в файле библиотеки подключений к данным.Также можно делать выбранные ячейки на листах редактируемыми, делая их именованными диапазонами (параметрами). Элементы, выбранные для отображения, при сохранении в Службы Excel отображаются в области **Параметры** в Веб-клиент Excel. Значения этих именованных диапазонов можно изменять в области **Параметры** и обновлять книгу. Также можно использовать веб-часть фильтра портала для фильтрации сразу нескольких веб-частей (Веб-клиент Excel и других типов веб-частей).Однако невозможно использовать Службы Excel для создания новых книг или редактирования существующих. Чтобы создать книгу для использования с Службы Excel, можно использовать Microsoft Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p104">By using Excel Services, you can view live, interactive workbooks by using only a browser. This means that you can save Excel workbooks and interact with them from within portal sites.You can also interact with Excel-based data by sorting, filtering, expanding, or collapsing PivotTables, and by passing in parameters; this provides the ability to perform analysis on published workbooks. You can interact with a workbook without changing the published workbook—which is valuable for report authors and report consumers.Excel Services supports workbooks that are connected to external data sources. You can embed connection strings to external data sources in the workbook or save them centrally in a data connection library file.You can also make selected cells in worksheets editable by making them named ranges (parameters). Items that you choose to make viewable, when you save to Excel Services, appear in the **Parameters** pane in Excel Web Access. You can change the values of these named ranges in the **Parameters** pane and refresh the workbook. You can also use the portal's filter Web Part to filter several Web Parts (Excel Web Access and other types of Web Parts) together.However, you cannot use Excel Services to create new workbooks or to edit existing workbooks. To author a workbook for use with Excel Services, you can use Microsoft Excel 2013.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0af-125">Microsoft Excel Online в составе Office Online также поддерживает книги Excel в браузере.</span><span class="sxs-lookup"><span data-stu-id="2f0af-125">Microsoft Excel Online, part of Office Online, also supports Excel workbooks in the browser.</span></span> <span data-ttu-id="2f0af-126">Дополнительные сведения об Excel Online см. в статье [Краткие руководства по началу работы с Office](http://office.microsoft.com/ru-RU/support/getting-started-with-office-FX102809998.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f0af-126">For more information about Excel Online, see  [Get started with the new Office](http://office.microsoft.com/ru-RU/support/getting-started-with-office-FX102809998.aspx).</span></span> 
  
    
    

<span data-ttu-id="2f0af-p106">Для Службы Excel также есть веб-служба. Можно использовать Веб-службы Excel для загрузки книг, задания значений в ячейках и диапазонах, обновления подключений к внешним данным, вычисления данных на листах и извлечения вычисленных результатов (включая значения ячеек, вычисленные данные книги целиком или снимок книги). В SharePoint также можно выполнять сохранение (в том числе копий) и участвовать в сеансах совместного редактирования при помощи Веб-службы Excel.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p106">Excel Services also has a Web service. You can use Excel Web Services to load workbooks, set values in cells and ranges, refresh external data connections, calculate worksheets, and extract calculated results (including cell values, the entire calculated workbook, or a snapshot of the workbook). In SharePoint, you can also save, save a copy, and participate in collaborative editing sessions by using Excel Web Services.</span></span>

> [!NOTE]
> <span data-ttu-id="2f0af-130">Дополнительные сведения о моментальных снимках см. в статье [Получение всей книги или моментального снимка](how-to-get-an-entire-workbook-or-a-snapshot.md).</span><span class="sxs-lookup"><span data-stu-id="2f0af-130">[Note:](how-to-get-an-entire-workbook-or-a-snapshot.md) For more information about snapshots, see  How to: Get an Entire Workbook or a Snapshot.</span></span> 
  
    
    

<span data-ttu-id="2f0af-131">Службы Excel поддерживает UDF, которые можно использовать для расширения возможностей Службы вычислений Excel  например, для реализации настраиваемых библиотек вычисления или для чтения данных из веб-служб и источников данных, не поддерживаемых Службы Excel.Службы Excel разработан как масштабируемый, надежный сервер корпоративного класса, предоставляющий функции и точность вычислений Excel.</span><span class="sxs-lookup"><span data-stu-id="2f0af-131">Excel Services supports UDFs, which you can use to extend the capabilities of Excel Calculation Services—for example, to implement custom calculation libraries or to read data from Web services and data sources that are not natively supported by Excel Services.Excel Services is designed to be a scalable, robust, enterprise-class server that provides feature and calculation fidelity with Excel.</span></span>
## <a name="scenarios-and-features"></a><span data-ttu-id="2f0af-132">Сценарии и функции</span><span class="sxs-lookup"><span data-stu-id="2f0af-132">Scenarios and Features</span></span>

<span data-ttu-id="2f0af-133">Службы Excel поддерживает множество различных сценариев и функций, некоторые из которых описаны в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="2f0af-133">Excel Services supports many different scenarios and features, some of which are described in this section.</span></span> 
  
    
    

### <a name="business-intelligence-portal-and-workbook-analysis"></a><span data-ttu-id="2f0af-134">Портал бизнес аналитики и анализ книги</span><span class="sxs-lookup"><span data-stu-id="2f0af-134">Business Intelligence Portal and Workbook Analysis</span></span>

<span data-ttu-id="2f0af-p107">Портал бизнес-аналитики отображает системы показателей и отчеты, а также позволяет пользователям просматривать данные при помощи только браузера. Функция **Центр бизнес-аналитики** в SharePoint Server включает в себя функциональность портала бизнес-аналитики и панели мониторинга. На рис. 1 показана панель мониторинга центра отчетов с уже настроенными библиотекой отчетов, диаграммой и ключевыми индикаторами производительности.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p107">A business intelligence portal displays scorecards and reports, and enables users to explore data by using only a browser. The **BI Center** feature in SharePoint Server includes a business intelligence portal and dashboard functionalities. Figure 1 shows a report center dashboard with a library of reports, a chart, and Key Performance Indicators (KPIs) already set up.</span></span>
  
    
    
<span data-ttu-id="2f0af-p108">Службы Excel также позволяет вычислять данные на сервере. Службы Excel участвует в **Центре бизнес-аналитики**, предоставляя возможность вычисления и предоставления контента на основе Excel на интегрированных панелях мониторинга бизнес-аналитики. Можно отобразить книгу Excel с помощью веб-части Веб-клиент Excel, подключиться к внешнему источнику данных и взаимодействовать с данными в книге.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p108">Excel Services also enables you to calculate data on the server. Excel Services participates in the **BI Center** by providing the ability to calculate and expose Excel-based content on integrated BI dashboards.You can display an Excel workbook by using the Excel Web Access Web Part, connect to external data sources, and further interact with the data in the workbook.</span></span>
  
    
    
 <span data-ttu-id="2f0af-140">На рисунке 1 показана панель мониторинга с веб-частью фильтра и книгами Excel, отображаемыми при помощи веб-частей Веб-клиент Excel.</span><span class="sxs-lookup"><span data-stu-id="2f0af-140">Figure 1 shows a dashboard with a filter Web Part, and Excel workbooks displayed by using Excel Web Access Web Parts.</span></span>
  
    
    

<span data-ttu-id="2f0af-141">**Рисунок 1. Панель мониторинга с фильтром и контентом Excel**</span><span class="sxs-lookup"><span data-stu-id="2f0af-141">**Figure 1. Dashboard with filtering and Excel content**</span></span>

  
    
    

  
    
    
![Панель мониторинга с фильтрацией и содержимым Excel](../images/17740d96-b5cf-4a0f-938d-a0d0d1e91f1e.GIF)
  
    
    
<span data-ttu-id="2f0af-p109">Помимо участия в интегрированных панелях мониторинга, Службы Excel также можно использовать для отображения всех или части книг Excel для предоставления пользователям возможности взаимодействия с их контентом в знакомом пользовательском интерфейсе Excel. На рисунке 2 показан отображаемый диапазон и ячейки, предоставляемые для ввода пользователем через параметры. Обозначение определенных ячеек как параметров позволяет пользователям изменять значения в этих ячейках на листе с помощью полей редактирования в правой области. Затем Службы Excel повторно вычисляет лист на основе новых значений.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p109">In addition to participating in integrated dashboards, Excel Services can also be used to display all or part of Excel workbooks to enable users to interact with that content in the familiar Excel user interface. Figure 2 shows a range being displayed, and cells being exposed for user input through parameters. Designating specific cells as parameters enables users to change values in those cells in a worksheet by using the edit boxes in the right pane. Excel Services then recalculates the worksheet based on the new values.</span></span>
  
    
    
<span data-ttu-id="2f0af-p110">Если требуется использовать определение функциональные возможности в Excel или анализировать книгу с использованием всех функциональных возможностей Excel, можно открыть книгу в Excel, нажав кнопку **Открыть в Excel**. Также можно открыть книгу в Excel для ее печати и для работы в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p110">If you want to use certain functionalities in Excel or if you want to analyze a workbook by using all Excel functionalities, you can open a workbook in Excel by clicking **Open in Excel**. You can also open a workbook in Excel to print it and to work offline.</span></span>
  
> [!NOTE]
> <span data-ttu-id="2f0af-149">Чтобы открыть книгу с помощью команды **Открыть в Excel**, необходимы права на открытие.</span><span class="sxs-lookup"><span data-stu-id="2f0af-149">Note: To open a workbook by using the **Open in Excel** command, you must have "open" rights.</span></span> <span data-ttu-id="2f0af-150">Дополнительные сведения см. в следующем разделе, **Управление книгами**, и статье [Разрешения пользователей и уровни разрешений](http://technet.microsoft.com/ru-RU/library/cc721640%28office.14%29.aspx) на сайте [TechNet](http://technet.microsoft.com/ru-RU/library/cc263215%28office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f0af-150">For more information, see the next section, **Managing Workbooks**, and  [User Permissions and Permission Levels](http://technet.microsoft.com/ru-RU/library/cc721640%28office.14%29.aspx) on [TechNet](http://technet.microsoft.com/ru-RU/library/cc263215%28office.14%29.aspx).</span></span> <span data-ttu-id="2f0af-151">Даже пользователи, не обладающие правами на открытие, могут открывать моментальные снимки в Excel.</span><span class="sxs-lookup"><span data-stu-id="2f0af-151">Users who do not have "open" rights can still open a snapshot in Excel.</span></span> 
  
    
    


<span data-ttu-id="2f0af-152">**Рис. 2. Использование панели "Параметры"**</span><span class="sxs-lookup"><span data-stu-id="2f0af-152">**Figure 2. Using the Parameters pane**</span></span>

  
    
    

  
    
    
![Использование панели "Параметры"](../images/65926095-d833-4eb2-b899-9efe40e2d540.GIF)
  
    
    
<span data-ttu-id="2f0af-154">Также можно анализировать, сводить данные и взаимодействовать с ними при помощи Веб-клиент Excel.</span><span class="sxs-lookup"><span data-stu-id="2f0af-154">You can also analyze, pivot, and interact with data by using Excel Web Access.</span></span>
  
    
    
<span data-ttu-id="2f0af-155">Дополнительные сведения о Службы Excel и возможности бизнес-аналитики в SharePoint см. в документации по бизнес-аналитике в справке SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="2f0af-155">For more information about Excel Services and business intelligence capability in SharePoint, see the business intelligence documentation in SharePoint Server Help.</span></span> 
  
    
    

### <a name="managing-workbooks"></a><span data-ttu-id="2f0af-156">Управление книгами</span><span class="sxs-lookup"><span data-stu-id="2f0af-156">Managing Workbooks</span></span>

<span data-ttu-id="2f0af-157">Возможности управления книгами и их блокировки в Службы Excel позволяют:</span><span class="sxs-lookup"><span data-stu-id="2f0af-157">The workbook management and lockdown capabilities of Excel Services enable you to:</span></span>
  
    
    

- <span data-ttu-id="2f0af-p112">Сохранять только одну копию книги, которая создается и изменяется доверенным автором в централизованном, безопасном расположении, вместо хранения нескольких копий на компьютере каждого пользователя. Правильную версию листа проще найти, предоставить для общего доступа и использовать в Excel, SharePoint и других приложениях.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p112">Maintain only one copy of a workbook, that is created and changed by a trusted author in a central, secure place, instead of maintaining multiple copies on each user's computer. The correct version of the worksheet is easier to find, share, and use from within Excel, SharePoint, and other applications.</span></span> 
    
  
- <span data-ttu-id="2f0af-p113">Обеспечивать безопасность и защиту моделей книг и внутренних данных. Можно предоставить пользователям права только на просмотр, чтобы ограничить доступ к книге. Например, можно запретить пользователям открывать книгу в Excel или ограничить их возможности просмотра книги. Пользователи могут иметь доступ к контенту книги, открытому автором для общего доступа, через браузер, но не иметь возможности открыть книгу в клиенте Excel, просматривать формулы, вспомогательный контент или другую интеллектуальную собственность, которая может содержаться в книге.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p113">Secure and protect workbook models and back-end data. You can give users view-only rights to limit access to the workbook. For example, you can prevent users from opening a workbook by using Excel or you can control what they are allowed to view in a workbook. Users can have browser-based access to the content in a workbook that the author wants to share, but no ability to open the workbook in the Excel client, view formulas, or view supporting content or other intellectual property that may be in the workbook.</span></span> 
    
  
- <span data-ttu-id="2f0af-164">Создание снимков книги.</span><span class="sxs-lookup"><span data-stu-id="2f0af-164">Create snapshots of a workbook.</span></span>
    
  
<span data-ttu-id="2f0af-p114">Приложение Службы Excel оптимизировано для большого числа пользователей и книг. Также оно может помогать при балансировке вычислительной нагрузки в ферме серверов.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p114">Excel Services is optimized for many users and many workbooks. It can also help load-balance calculation across the server farm.</span></span>
  
    
    
<span data-ttu-id="2f0af-167">Дополнительные сведения об управлении книгами с помощью Службы Excel см. в документации по SharePoint Server на сайте  [TechNet](http://technet.microsoft.com/ru-RU/library/ee424405%28office.14%29.aspx) или в справке SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="2f0af-167">For more information about managing workbooks by using Excel Services, see the SharePoint Server documentation on  [TechNet](http://technet.microsoft.com/ru-RU/library/ee424405%28office.14%29.aspx) or SharePoint Server Help.</span></span>
  
    
    

### <a name="programmatic-access-through-custom-net-applications"></a><span data-ttu-id="2f0af-168">Программный доступ с помощью настраиваемых приложений .NET</span><span class="sxs-lookup"><span data-stu-id="2f0af-168">Programmatic Access through Custom .NET Applications</span></span>

<span data-ttu-id="2f0af-169">Можно создавать настраиваемые приложения  например, приложения ASP.NET,  которые:</span><span class="sxs-lookup"><span data-stu-id="2f0af-169">You can create custom applications—for example, ASP.NET applications—that:</span></span>
  
    
    

- <span data-ttu-id="2f0af-170">Вызывают Веб-службы Excel для доступа, параметризации и вычисления книг.</span><span class="sxs-lookup"><span data-stu-id="2f0af-170">Call Excel Web Services to access, parameterize, and calculate workbooks.</span></span>
    
  
- <span data-ttu-id="2f0af-171">Открывают, обновляют внешние данные, задают ячейки или диапазоны, повторно вычисляют, участвуют в сеансах совместного редактирования с другими приложениями или пользователя, сохраняют, а также сохраняют с изменением имени или формата.</span><span class="sxs-lookup"><span data-stu-id="2f0af-171">Open, refresh external data, set cells or ranges, recalculate, participate in collaborative editing sessions with other applications or people, save, and save as.</span></span> 
    
  
- <span data-ttu-id="2f0af-p115">Используют настраиваемые потоки операций для планирования операций вычисления или отправки уведомления по электронной почте. (Для этого используются возможности SharePoint, не собственная часть Службы Excel.)</span><span class="sxs-lookup"><span data-stu-id="2f0af-p115">Use custom workflows to schedule calculation operations or send e-mail notifications. (This uses SharePoint capabilities and is not a native part of Excel Services.)</span></span>
    
  

### <a name="user-defined-functions-udfs"></a><span data-ttu-id="2f0af-174">Пользовательские функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="2f0af-174">User-Defined Functions (UDFs)</span></span>

<span data-ttu-id="2f0af-175">Кроме того, можно использовать пользовательские функции Службы Excel, позволяющие с помощью формул в ячейках вызывать настраиваемые функции, написанные в управляемом коде и развернутые в SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="2f0af-175">You can also use Excel Services UDFs, which enable you to use formulas in a cell to call custom functions that are written in managed code and deployed to SharePoint Server.</span></span>
  
    
    
<span data-ttu-id="2f0af-176">Дополнительные сведения о пользовательских функциях в Службы Excel см. в статье  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="2f0af-176">For more information about UDFs in Excel Services, see  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).</span></span>
  
    
    

### <a name="ecmascript-javascript-jscript"></a><span data-ttu-id="2f0af-177">ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="2f0af-177">ECMAScript (JavaScript, JScript)</span></span>

<span data-ttu-id="2f0af-p116">Также можно использовать объектную модель JavaScript в Службы Excel для автоматизации, настройки элемент управления веб-части Веб-клиент Excel и управления им. Можно использовать объектную модель JavaScript для построения более удобных и интегрированных решений.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p116">You can also use the JavaScript object model in Excel Services to automate, customize, and drive the Excel Web Access Web Part control. You can use the JavaScript object model to build more compelling and integrated solutions.</span></span>
  
    
    

### <a name="javascript-user-defined-functions-udfs"></a><span data-ttu-id="2f0af-180">Пользовательские функции JavaScript (UDF)</span><span class="sxs-lookup"><span data-stu-id="2f0af-180">JavaScript user-defined functions (UDFs)</span></span>

<span data-ttu-id="2f0af-p117">Появившиеся в Службы Microsoft Excel и Microsoft SharePoint новые пользовательские функции ECMAScript (JavaScript, JScript) позволяют добавлять настраиваемые функции в Excel при использовании внедренных книг Excel с OneDrive или веб-части Веб-клиент ExcelВеб-клиент Excel в SharePoint. Кроме встроенных функций, используемых в Excel, вы можете добавить собственные настраиваемые функции с помощью пользовательских функций JavaScript, которые можно вызвать из внутренних формул в .</span><span class="sxs-lookup"><span data-stu-id="2f0af-p117">New in Microsoft Excel Services and Microsoft SharePoint, ECMAScript (JavaScript, JScript) UDFs enable you to add custom functions to Excel when you are using an embedded Excel workbook with OneDrive or an Excel Web AccessExcel Web Access Web Part in SharePoint. Besides the built-in functions that you use in Excel, you can add your own, custom functions using JavaScript UDFs that you can call from inside formulas in .</span></span>
  
    
    
<span data-ttu-id="2f0af-p118">Пользовательские функции JavaScript похожи на  [пользовательские функции](http://msdn.microsoft.com/ru-RU/library/ms499792.aspx), которые вы можете создать для Microsoft Excel. Разница состоит в том, что пользовательские функции JavaScript используются только в книгах, внедренных в веб-страницу, и существуют только на этой веб-странице.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p118">JavaScript UDFs are similar to  [UDFs](http://msdn.microsoft.com/ru-RU/library/ms499792.aspx) that you can create for Microsoft Excel. The difference is that JavaScript UDFs are only used in workbooks embedded in a webpage and only exist on that web page.</span></span>
  
    
    

### <a name="javascript-object-model"></a><span data-ttu-id="2f0af-185">Объектная модель JavaScript</span><span class="sxs-lookup"><span data-stu-id="2f0af-185">JavaScript Object Model</span></span>

<span data-ttu-id="2f0af-186">API JSOM для Службы Excel теперь включает следующие функции:</span><span class="sxs-lookup"><span data-stu-id="2f0af-186">The Excel Services JSOM API now includes the following:</span></span>
  
    
    

- <span data-ttu-id="2f0af-p119">Возможность перезагрузить внедренную книгу. Теперь вы можете сбросить данные внедренной книги, вернув данные из файла базовой книги.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p119">The ability to reload the embedded workbook. Now you can reset the embedded workbook to the data in the underlying workbook file.</span></span>
    
  
- <span data-ttu-id="2f0af-p120">Перемещаемые объекты, созданные пользователем. Для объекта EwaControl существуют новые методы добавления или удаления созданных вами перемещаемых объектов.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p120">User-created floating objects. The EwaControl object has new methods that let you add/remove floating objects that you create.</span></span>
    
  
- <span data-ttu-id="2f0af-191">Больший контроль над видимой областью элемента управления Ewa.</span><span class="sxs-lookup"><span data-stu-id="2f0af-191">More control over viewable area of the Ewa control.</span></span>
    
  
- <span data-ttu-id="2f0af-p121">Событие SheetChanged. Это событие возникает при каких-либо изменениях на листе, таких как обновление ячеек, удаление или очистка ячеек, копирование, вырезание и вставка диапазонов, отмена и повтор действия.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p121">SheetChanged Event. This event raises when something changes on a sheet, such as updating cells, deleting or clearing cells, copying, cutting or pasting ranges, and undo/redo actions.</span></span>
    
  
- <span data-ttu-id="2f0af-p122">Включение проверки данных. Теперь вы можете проверить данные, введенные пользователем.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p122">Enabling data validation. You can now validate data that is entered by a user.</span></span>
    
  

### <a name="rest-api"></a><span data-ttu-id="2f0af-196">REST API</span><span class="sxs-lookup"><span data-stu-id="2f0af-196">REST API</span></span>

<span data-ttu-id="2f0af-p123">Можно использовать API-интерфейс REST в Службы Excel для прямого доступа к частям книги по URL-адресу. Механизмы обнаружения, встроенные в Службы Excel API-интерфейс REST, позволяют разработчиками и пользователям просматривать контент книги вручную или программно.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p123">You can use the REST API in Excel Services to access workbook parts or elements directly through a URL. The discovery mechanisms built into the Excel Services REST API enable developers and users to explore the content of the workbook manually or programmatically.</span></span> 
  
    
    
<span data-ttu-id="2f0af-199">Дополнительные сведения об API-интерфейсе REST Службы Excel см. в статье  [API-интерфейс REST служб Excel](excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="2f0af-199">For more information about the REST API in Excel Services, see  [Excel Services REST API](excel-services-rest-api.md).</span></span>
  
    
    

### <a name="rest-odata"></a><span data-ttu-id="2f0af-200">ODATA REST</span><span class="sxs-lookup"><span data-stu-id="2f0af-200">REST ODATA</span></span>

<span data-ttu-id="2f0af-p124">Новые функции Службы Microsoft Excel и Microsoft SharePoint. С помощью новых возможностей OData в REST API для Службы Excel можно запрашивать таблицы в книгах Excel в качестве OData. Например, для запроса метаданных Excel о доступных ресурсах в книге SampleWorkbook.xlsx с помощью вызова REST используйте приведенный ниже синтаксис.</span><span class="sxs-lookup"><span data-stu-id="2f0af-p124">New in Microsoft Excel Services and Microsoft SharePoint, by using the new OData functionality in the Excel Services REST API, you can request the tables inside an Excel workbook as OData. For example, to request Excel metadata about available resources in the SampleWorkbook.xlsx workbook using a REST call, you use the following syntax.</span></span>
  
    
    
<span data-ttu-id="2f0af-203">http://\<имя_сервера\>/_vti_bin/ExcelRest.aspx/Docs/Documents/SampleWorkbook.xlsx/model Дополнительные сведения о REST API см. в разделе</span><span class="sxs-lookup"><span data-stu-id="2f0af-203">http://\<ServerName\>/_vti_bin/ExcelRest.aspx/Docs/Documents/SampleWorkbook.xlsx/model For more information about the REST API, see the</span></span> 
  
    
    
 <span data-ttu-id="2f0af-204">[API-интерфейс REST служб Excel 2010](http://msdn.microsoft.com/ru-RU/library/ee556413.aspx) документации по пакету SDK SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f0af-204">[Excel Services 2010 REST API](http://msdn.microsoft.com/ru-RU/library/ee556413.aspx) documentation in the SharePoint SDK documentation.</span></span>
  
    
    
<span data-ttu-id="2f0af-205">Чтобы запросить метаданные о доступных ресурсах в книге SampleWorkbook.xlsx с помощью OData, используйте тот же синтаксис REST, но заменив /Model на /Odata, как показано в приведенном ниже запросе.</span><span class="sxs-lookup"><span data-stu-id="2f0af-205">To request metadata about available resources in the SampleWorkbook.xlsx workbook using OData, use the same REST syntax, except replace /Model with /Odata as in the following request.</span></span> 
  
    
    
<span data-ttu-id="2f0af-206">http://\<имя_сервера\>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/OData</span><span class="sxs-lookup"><span data-stu-id="2f0af-206">http://\<ServerName\>/_vti_bin/ExcelRest.aspx/Docs/Documents/sampleWorkbook.xlsx/OData</span></span>
  
    
    
<span data-ttu-id="2f0af-207">Здесь вы можете использовать параметры системных запросов OData, чтобы получать конкретные сведения о таблицах в книге.</span><span class="sxs-lookup"><span data-stu-id="2f0af-207">From there you can use OData system query options to get specific information about tables inside the workbook.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="2f0af-208">См. также</span><span class="sxs-lookup"><span data-stu-id="2f0af-208">See also</span></span>


-  [<span data-ttu-id="2f0af-209">Excel Services Development Roadmap</span><span class="sxs-lookup"><span data-stu-id="2f0af-209">Excel Services Development Roadmap</span></span>](excel-services-development-roadmap.md)
    
  
-  [<span data-ttu-id="2f0af-210">Архитектура служб Excel</span><span class="sxs-lookup"><span data-stu-id="2f0af-210">Excel Services Architecture</span></span>](excel-services-architecture.md)
    
  
-  [<span data-ttu-id="2f0af-211">Общие сведения о пользовательских функций JavaScript</span><span class="sxs-lookup"><span data-stu-id="2f0af-211">JavaScript user-defined functions overview</span></span>](javascript-user-defined-functions-overview.md)
    
  
-  [<span data-ttu-id="2f0af-212">С помощью OData с помощью служб Excel REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f0af-212">Using OData with Excel Services REST in SharePoint</span></span>](using-odata-with-excel-services-rest-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2f0af-213">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="2f0af-213">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
    
  
-  [<span data-ttu-id="2f0af-214">Frequently Asked Questions About Excel Services UDFs</span><span class="sxs-lookup"><span data-stu-id="2f0af-214">Frequently Asked Questions About Excel Services UDFs</span></span>](frequently-asked-questions-about-excel-services-udfs.md)
    
  
-  [<span data-ttu-id="2f0af-215">Unsupported Features in Excel Services</span><span class="sxs-lookup"><span data-stu-id="2f0af-215">Unsupported Features in Excel Services</span></span>](http://msdn.microsoft.com/library/5868e672-4786-4fed-9168-07ff538f6f5c%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="2f0af-216">Блоги, форумы и ресурсы для служб Excel</span><span class="sxs-lookup"><span data-stu-id="2f0af-216">Excel Services Blogs, Forums, and Resources</span></span>](excel-services-blogs-forums-and-resources.md)
    
  

