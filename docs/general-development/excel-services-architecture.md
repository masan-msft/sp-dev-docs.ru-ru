---
title: "Архитектура служб Excel"
ms.date: 09/25/2017
keywords: excel services design
f1_keywords:
- excel services design
ms.prod: sharepoint
ms.assetid: e0349b4a-2d52-46c4-a167-801e9c24eaca
ms.openlocfilehash: 3202d7163ad080462e98dd73fb05bf3f60eae7cd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="excel-services-architecture"></a><span data-ttu-id="93175-103">Архитектура служб Excel</span><span class="sxs-lookup"><span data-stu-id="93175-103">Excel Services Architecture</span></span>

<span data-ttu-id="93175-p101">Службы Службы Excel входят в состав Microsoft SharePoint Server 2010. Службы Excel построены на базе технологий ASP.NET и SharePoint Foundation. Ниже перечислены ключевые компоненты Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="93175-p101">Excel Services is part of Microsoft SharePoint Server 2010. Excel Services is built on ASP.NET and SharePoint Foundation technologies. Following are the core components in Excel Services:</span></span>
  
    
    


- <span data-ttu-id="93175-107">Веб-клиент Excel</span><span class="sxs-lookup"><span data-stu-id="93175-107">Excel Web Access</span></span>
    
  
- <span data-ttu-id="93175-108">Веб-службы Excel</span><span class="sxs-lookup"><span data-stu-id="93175-108">Excel Web Services</span></span>
    
  
- <span data-ttu-id="93175-109">Пользовательские функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="93175-109">User-defined functions (UDFs)</span></span>
    
  
- <span data-ttu-id="93175-110">ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="93175-110">ECMAScript (JavaScript, JScript)</span></span>
    
  
- <span data-ttu-id="93175-111">Служба REST</span><span class="sxs-lookup"><span data-stu-id="93175-111">Representational State Transfer (REST) service</span></span>
    
  
- <span data-ttu-id="93175-112">Службы вычислений Excel</span><span class="sxs-lookup"><span data-stu-id="93175-112">Excel Calculation Services</span></span>
    
> [!NOTE]
> <span data-ttu-id="93175-p102">[!Примечание] Microsoft Excel Online, частью Office Online также поддерживает книги Excel в браузере. Дополнительные сведения о Excel Online [Документация по Office Web Apps](https://technet.microsoft.com/en-us/library/ee855124.aspx)см.</span><span class="sxs-lookup"><span data-stu-id="93175-p102">Microsoft Excel Online, part of Office Online, also supports Excel workbooks in the browser. For more information about Excel Online, see  [documentation about Office Web Apps](https://technet.microsoft.com/en-us/library/ee855124.aspx).</span></span> 
  
    
    

<span data-ttu-id="93175-p103">Веб-клиент Excel, Веб-службы Excel, пользовательские функции, JavaScript, службу REST и Службы вычислений Excel можно разбить на две основные группы: компоненты на сервере переднего плана (который также называется интерфейсным веб-сервером) и компоненты на внутреннем сервере приложений. **Компоненты интерфейсного веб-сервера и внутреннего сервера приложений**</span><span class="sxs-lookup"><span data-stu-id="93175-p103">The Excel Web Access, Excel Web Services, UDFs, JavaScript, the REST service, and Excel Calculation Services components can be divided into two major groups: the components on a front-end server (also known as the "Web front end") and the component on a back-end application server. **Components of a Web front end and a back-end application server**</span></span>

  
    
    

  
    
    
![Веб-сервер приложений переднего плана и внутренний веб-сервер приложений](../images/ed480e23-e0e8-4896-93b1-98a94f50b9a0.gif)
  
    
    

  
    
    

  
    
    

## <a name="web-front-end-servers-and-back-end-application-servers"></a><span data-ttu-id="93175-118">Интерфейсный веб-серверы и внутренние серверы приложений</span><span class="sxs-lookup"><span data-stu-id="93175-118">Web Front-End Servers and Back-End Application Servers</span></span>

<span data-ttu-id="93175-p104">Веб-клиент Excel, Веб-службы Excel, пользовательские функции, JavaScript, службу REST и Службы вычислений Excel можно разбить на компоненты, размещенные на интерфейсном веб-сервере, и компоненты, размещенные на внутреннем сервере приложений. На интерфейсном веб-сервере размещаются Веб-клиент Excel, JavaScript, служба REST и Веб-службы Excel. Компонент Службы вычислений Excel размещаются на внутреннем сервере приложений вместе с добавленными администратором сборками пользовательских функций.</span><span class="sxs-lookup"><span data-stu-id="93175-p104">The Excel Web Access, Excel Web Services, UDFs, JavaScript, the REST service, and Excel Calculation Services components can be divided into components on the Web front-end server and components that live on a back-end application server. The Web front end includes Excel Web Access, JavaScript, the REST service, and Excel Web Services. The Excel Calculation Services component resides on the back-end application server, alongside any UDF assemblies that an administrator has added.</span></span>
  
    
    
<span data-ttu-id="93175-p105">В простейшей конфигурации SharePoint Server 2010  один компьютер с приложением SharePoint Server 2010, установленным в режиме изолированной установки  все пять компонентов устанавливаются на один компьютер. Однако в типичной корпоративной среде с большим количеством пользователей компоненты интерфейсного веб-сервера и компоненты внутреннего сервера приложений устанавливаются на разные компьютеры в ферме. Это позволяет масштабировать интерфейсный веб-сервер независимо от внутреннего сервера приложений. Например, в зависимости от потребностей организации можно добавить дополнительные интерфейсные веб-серверы или внутренние серверы приложений.</span><span class="sxs-lookup"><span data-stu-id="93175-p105">In the simplest configuration in SharePoint Server 2010—that is, a single computer running SharePoint Server 2010 as a stand-alone installation—all five components are installed on the same computer. However, in a typical enterprise environment with a large number of users, the components on the Web front-end server and the components on the back-end application server are on different computers in a farm configuration. It is possible to scale out the Web front-end server independently from the back-end application server. For example, you can have more Web front-end servers or more back-end application servers, depending on your organizational needs.</span></span>
  
    
    
<span data-ttu-id="93175-126">Сведения о топологии Службы Excel, масштабируемости, производительности и безопасности обратитесь к документации SharePoint Server 2010 на  [сайте TechNet](http://technet.microsoft.com/en-us/library/cc303422%28office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="93175-126">For information about Excel Services topology, scalability, performance, and security, see the SharePoint Server 2010 documentation on  [TechNet](http://technet.microsoft.com/en-us/library/cc303422%28office.14%29.aspx).</span></span> 
  
    
    

## <a name="excel-web-access"></a><span data-ttu-id="93175-127">Веб-доступ Excel</span><span class="sxs-lookup"><span data-stu-id="93175-127">Excel Web Access</span></span>

<span data-ttu-id="93175-p106">Веб-клиент Excel  это страница средства просмотра и веб-часть Службы Excel, которую можно добавить на любую страницу веб-частей в SharePoint Server 2010. Веб-клиент Excel отображает (иными словами, создает HTML-код) на веб-странице интерактивные книги Excel, позволяя пользователю взаимодействовать с этими книгами и просматривать их. Веб-клиент Excel  это визуальный компонент Службы Excel, предназначенный для пользователей. Веб-клиент Excel, как и любую другую веб-часть, можно использовать в SharePoint Server 2010. Веб-клиент Excel не требует от пользователя установки на клиентском компьютере каких-либо компонентов.</span><span class="sxs-lookup"><span data-stu-id="93175-p106">Excel Web Access is a viewer page and an Excel Services Web Part that you can add to any Web Parts page in SharePoint Server 2010. Excel Web Access renders (in other words, creates the HTML for) live Excel workbooks on a Web page, and enables the user to interact with those workbooks and explore them. Excel Web Access is the visible Excel Services component for the user. You can use Excel Web Access like any other Web Part in SharePoint Server 2010. Excel Web Access does not require the user to install anything on the client computer.</span></span>
  
    
    
<span data-ttu-id="93175-133">Свойства веб-части Excel Web Access можно также настроить.</span><span class="sxs-lookup"><span data-stu-id="93175-133">The Excel Web Access Web Part properties are also customizable.</span></span> <span data-ttu-id="93175-134">Для получения дополнительных сведений см **Microsoft.Office.Excel.Server.WebUI** пространства имен.</span><span class="sxs-lookup"><span data-stu-id="93175-134">For more information, see the **Microsoft.Office.Excel.Server.WebUI** namespace reference documentation.</span></span>
  
    
    

## <a name="excel-web-services"></a><span data-ttu-id="93175-135">Веб-службы Excel</span><span class="sxs-lookup"><span data-stu-id="93175-135">Excel Web Services</span></span>

<span data-ttu-id="93175-p108">Веб-службы Excel  Службы Excel компонент, который позволяет получать доступ к его веб-службы. Вы можете создавать приложения, которые могут вызывать Веб-службы Excel для вычисления, задавать и извлекать значения из книг, а также обновлять подключения к внешним данным. Веб-службы Excel можно внедрить логики книги на сервере в приложения, автоматически обновить книг Excel и создание конкретного приложения пользовательских интерфейсов вокруг служба вычислений Excel на сервере.</span><span class="sxs-lookup"><span data-stu-id="93175-p108">Excel Web Services is the Excel Services component that provides programmatic access to its Web service. You can develop applications that call Excel Web Services to calculate, set, and extract values from workbooks, and to refresh external data connections. By using Excel Web Services, you can incorporate server-side workbook logic into an application, automate the updating of Excel workbooks, and create application-specific user interfaces around server-side Excel calculation.</span></span> 
  
> [!NOTE]
> <span data-ttu-id="93175-p109">[!Примечание] При внесении изменений в книгу  например, при задании значений диапазона с помощью Веб-службы Excel  эти изменения сохраняются в книге только во время текущего сеанса. Изменения не сохраняются и не вносятся в исходную книгу. По завершении текущего сеанса работы с книгой (например, при вызове метода **CloseWorkbook** либо по истечении времени сеанса) все внесенные изменения утрачиваются.> Если вы хотите сохранить изменения, внесенные в книгу, можно использовать метод **GetWorkbook** и затем сохраните книгу. Для получения дополнительных сведений см [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) . Можно также откройте книгу в режиме редактирования и сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="93175-p109">When you make changes to a workbook—for example, by setting values to a range by using Excel Web Services—the changes to the workbook are preserved only for that session. The changes are not saved or persisted back to the original workbook. When the current workbook session ends (for example, when you call the **CloseWorkbook** method, or when the session times out), the changes that you made are lost.> If you want to save changes that you make to a workbook, you can use the **GetWorkbook** method, and then save the workbook. For more information, see [Microsoft.Office.Excel.Server.WebServices](https://msdn.microsoft.com/library/Microsoft.Office.Excel.Server.WebServices.aspx) . You can also open the workbook in edit mode and save the changes.</span></span>
  
    
    

<span data-ttu-id="93175-144">Дополнительные сведения о Веб-службы Excel см. в разделе  [Excel Services Development Roadmap](excel-services-development-roadmap.md).</span><span class="sxs-lookup"><span data-stu-id="93175-144">For more information about Excel Web Services, see  [Excel Services Development Roadmap](excel-services-development-roadmap.md).</span></span>
  
    
    

## <a name="user-defined-functions-udfs"></a><span data-ttu-id="93175-145">Пользовательские функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="93175-145">User-Defined Functions (UDFs)</span></span>

<span data-ttu-id="93175-p110">Службы Excel Пользовательские функции позволяют использовать в ячейках формулы для вызова настраиваемых функций, написанных с помощью управляемого кода и развернутых в SharePoint Server 2010. Дополнительные сведения о пользовательских функциях в Службы Excel см. в разделе  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).</span><span class="sxs-lookup"><span data-stu-id="93175-p110">Excel Services UDFs enable you to use formulas in a cell to call custom functions that are written in managed code and deployed to SharePoint Server 2010. For more information about UDFs in Excel Services, see  [Understanding Excel Services UDFs](understanding-excel-services-udfs.md).</span></span>
  
    
    

## <a name="ecmascript-javascript-jscript"></a><span data-ttu-id="93175-148">ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="93175-148">ECMAScript (JavaScript, JScript)</span></span>

<span data-ttu-id="93175-p111">Объектная модель JavaScript в Службы Excel позволяет разработчикам настраивать, автоматизировать и использовать на странице элемент управления веб-части Веб-клиент Excel. С помощью объектной модели JavaScript можно создавать гибридные веб-приложения и другие интегрированные решения, взаимодействующие с одним или несколькими элементами управления веб-части Веб-клиент Excel на странице или в **iframe** со сценарием на странице. Объектная модель также позволяет добавлять в книги и связанный с ними код дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="93175-p111">The JavaScript object model in Excel Services enables developers to customize, automate, and drive the Excel Web Access Web Part control on a page. By using the JavaScript object model, you can build mashups and other integrated solutions that interact with one or more Excel Web Access Web Part controls on a page or an **iframe** with script on the page. It also enables you to add more capabilities to your workbooks and code around them.</span></span>
  
    
    
<span data-ttu-id="93175-152">Дополнительные сведения об объектной модели JavaScript в Службы Excel справочная документация пространство имен  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) см.</span><span class="sxs-lookup"><span data-stu-id="93175-152">For more information about the JavaScript object model in Excel Services, see the  [Ewa](http://msdn.microsoft.com/library/6fe73191-3213-b986-1ad6-2c3b918a2241%28Office.15%29.aspx) namespace reference documentation.</span></span>
  
    
    

## <a name="rest-api"></a><span data-ttu-id="93175-153">API-интерфейс REST</span><span class="sxs-lookup"><span data-stu-id="93175-153">REST API</span></span>

<span data-ttu-id="93175-p112">API-Интерфейс REST в Службы Excel позволяет получить доступ к компонентам и элементам книги непосредственно через URL-адрес. URL-адрес содержит путь «метки», который является точкой входа на страницу ASPX, к месту расположения файла книги и путь к запрошенный элемент внутри книги.</span><span class="sxs-lookup"><span data-stu-id="93175-p112">The REST API in Excel Services enables you to access workbook parts or elements directly through a URL. The URL contains a "marker" path, which is the entry point to an .aspx page, to the workbook file location, and to the path to the requested element inside the workbook.</span></span> 
  
    
    
<span data-ttu-id="93175-156">Механизмы обнаружения, встроенные в API-Интерфейс REST Службы Excel позволяет разработчикам и пользователей, для изучения содержимого книги, автоматически или вручную.</span><span class="sxs-lookup"><span data-stu-id="93175-156">The discovery mechanisms built into the Excel Services REST API enables developers and users to explore the content of a workbook manually or programmatically.</span></span> 
  
    
    
<span data-ttu-id="93175-157">Дополнительные сведения об API-Интерфейс REST в Службы Excel можно  [API REST служб Excel](excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="93175-157">For more information about the REST API in Excel Services, see  [Excel Services REST API](excel-services-rest-api.md).</span></span> 
  
    
    

## <a name="excel-calculation-services"></a><span data-ttu-id="93175-158">Службы вычислений Excel</span><span class="sxs-lookup"><span data-stu-id="93175-158">Excel Calculation Services</span></span>

<span data-ttu-id="93175-p113">Службы Службы вычислений Excel предназначены для загрузки книг, выполнения вычислений, вызова настраиваемого кода (пользовательских функций) и обновления внешних данных. Для обеспечения интерактивности поддерживается состояние сеанса. Службы Службы вычислений Excel поддерживают сеанс, пока пользователь или вызывающая сторона взаимодействует с книгой. Сеанс завершается, когда вызывающая сторона завершает его явным образом или истекает время сеанса на сервере. Службы Службы Excel кэшируют открытые книги Excel, состояния вычисления и результаты запросов к внешним данным, что обеспечивает более высокую производительность при работе нескольких пользователей с одним набором книг.</span><span class="sxs-lookup"><span data-stu-id="93175-p113">The role of Excel Calculation Services is to load workbooks, calculate workbooks, call custom code (UDFs), and refresh external data. It also maintains the session state for interactivity. Excel Calculation Services maintains a session for the duration of interactions with the same workbook by a user or caller. A session is closed when the caller explicitly closes it or when the session times out on the server. Excel Services caches the opened Excel workbooks, calculation states, and external data query results, for improved performance when multiple users access the same set of workbooks.</span></span>
  
    
    

## <a name="load-balancing"></a><span data-ttu-id="93175-164">Балансировка нагрузки</span><span class="sxs-lookup"><span data-stu-id="93175-164">Load-Balancing</span></span>

<span data-ttu-id="93175-p114">В конфигурациях с несколькими серверами службы Службы Excel обеспечивают балансировку нагрузки при запросах к нескольким экземплярам Службы вычислений Excel в ферме. Если установлено несколько серверов приложений, службы Службы Excel обеспечивают балансировку нагрузки таким образом, чтобы ни один сервер приложений не был перегружен запросами.</span><span class="sxs-lookup"><span data-stu-id="93175-p114">In multiple-server configurations, Excel Services load-balances requests across multiple Excel Calculation Services occurrences in a farm configuration. If your installation includes multiple application servers, Excel Services will balance the load in an attempt to help ensure that no single application server is overloaded by requests.</span></span>
  
    
    
<span data-ttu-id="93175-167">Администраторы могут настроить поведение при балансировке нагрузки.</span><span class="sxs-lookup"><span data-stu-id="93175-167">Administrators can configure the load-balancing behavior.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="93175-168">См. также</span><span class="sxs-lookup"><span data-stu-id="93175-168">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="93175-169">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="93175-169">Concepts</span></span>


  
    
    
 [<span data-ttu-id="93175-170">Общие сведения о службах Excel</span><span class="sxs-lookup"><span data-stu-id="93175-170">Excel Services Overview</span></span>](excel-services-overview.md)
  
    
    
 [<span data-ttu-id="93175-171">Excel Services Development Roadmap</span><span class="sxs-lookup"><span data-stu-id="93175-171">Excel Services Development Roadmap</span></span>](excel-services-development-roadmap.md)
  
    
    
 [<span data-ttu-id="93175-172">Поддерживаемые и неподдерживаемые возможности</span><span class="sxs-lookup"><span data-stu-id="93175-172">Supported and Unsupported Features</span></span>](supported-and-unsupported-features.md)
#### <a name="other-resources"></a><span data-ttu-id="93175-173">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="93175-173">Other resources</span></span>


  
    
    
 [<span data-ttu-id="93175-174">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="93175-174">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
