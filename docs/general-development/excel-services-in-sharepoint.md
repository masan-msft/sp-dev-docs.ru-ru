---
title: "Службы Excel в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f7e13fcb-a86a-4a1e-af59-3bace98ce9d7
ms.openlocfilehash: 2621e87cfaf5fb2de6da2b1f518bf5828101044d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-in-sharepoint"></a><span data-ttu-id="832c5-102">Службы Excel в SharePoint</span><span class="sxs-lookup"><span data-stu-id="832c5-102">Excel Services in SharePoint</span></span>
<span data-ttu-id="832c5-103">Узнайте о новых возможностях в службах Excel в SharePoint и как их использовать в работу разработчика.</span><span class="sxs-lookup"><span data-stu-id="832c5-103">Learn about the new capabilities in Excel Services in SharePoint and how you can use them in your own development efforts.</span></span>
## <a name="whats-new-in-excel-services-for-developers"></a><span data-ttu-id="832c5-104">Новые возможности служб Excel для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="832c5-104">What's new in Excel Services for developers</span></span>
<span data-ttu-id="832c5-105"><a name="xlsWhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="832c5-105"></span></span>

<span data-ttu-id="832c5-106">SharePoint предлагает новые технологии для Excel Services─such как пользовательских функций ECMAScript (JavaScript, JScript) и интерактивные View─and Excel улучшения для существующих технологий, таких как ODATA REST и обновления объект ECMAScript (JavaScript, JScript) API-Интерфейс модель (JavaScript JSOM).</span><span class="sxs-lookup"><span data-stu-id="832c5-106">SharePoint brings new technologies to Excel Services─such as ECMAScript (JavaScript, JScript) UDFs and Excel Interactive View─and new enhancements to existing technologies, such as ODATA for REST, and updates to the ECMAScript (JavaScript, JScript) Object Model (JSOM) API.</span></span>
  
    
    

### <a name="javascript-udfs"></a><span data-ttu-id="832c5-107">Пользовательские функции JavaScript</span><span class="sxs-lookup"><span data-stu-id="832c5-107">JavaScript UDFs</span></span>
<span data-ttu-id="832c5-108"><a name="xlsJsUdfs"> </a></span><span class="sxs-lookup"><span data-stu-id="832c5-108"></span></span>

<span data-ttu-id="832c5-109">Службы Excel уже позволяет создавать пользовательские функции (UDF), с помощью управляемого кода.</span><span class="sxs-lookup"><span data-stu-id="832c5-109">Excel Services already lets you create user-defined functions (UDFs) using managed code.</span></span> <span data-ttu-id="832c5-110">Службы Excel в SharePoint представлен новый вид из пользовательских Функций, пользовательских функций ECMAScript (JavaScript, JScript).</span><span class="sxs-lookup"><span data-stu-id="832c5-110">Excel Services in SharePoint introduces a new kind of UDF—ECMAScript (JavaScript, JScript) UDFs.</span></span> <span data-ttu-id="832c5-111">Пользовательские функции JavaScript, выполняются в контексте браузер: либо в книге Excel, которая размещается в Excel Web Access веб-части в SharePoint или в книге, встроенные в веб-страницу узла.</span><span class="sxs-lookup"><span data-stu-id="832c5-111">JavaScript UDFs run in the context of the browser: either in a Excel workbook that is hosted in an Excel Web Access Web Part on SharePoint, or in a workbook that is embedded on a host webpage.</span></span> 
  
    
    

### <a name="odata-in-excel-services"></a><span data-ttu-id="832c5-112">OData в службах Excel</span><span class="sxs-lookup"><span data-stu-id="832c5-112">OData in Excel Services</span></span>
<span data-ttu-id="832c5-113"><a name="xlsOdata"> </a></span><span class="sxs-lookup"><span data-stu-id="832c5-113"></span></span>

<span data-ttu-id="832c5-114">SharePoint Server 2010 появился API-Интерфейс REST для использования в считывание и запись сведений в книгах Excel, хранящиеся в библиотеках документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="832c5-114">SharePoint Server 2010 introduced the REST API for use in getting and setting information in Excel Workbooks stored in SharePoint document libraries.</span></span> <span data-ttu-id="832c5-115">SharePoint добавляет новый способ запроса данных из служб Excel, использующего Open Data Protocol (OData) которого можно использовать для получения сведений обо всех ресурсах служб Excel.</span><span class="sxs-lookup"><span data-stu-id="832c5-115">SharePoint adds a new way to request data from Excel Services that uses the Open Data Protocol (OData) which you can use to get information about Excel Services resources.</span></span> <span data-ttu-id="832c5-116">Эта новая служба во многом зависит от существующего интерфейса API REST служб Excel.</span><span class="sxs-lookup"><span data-stu-id="832c5-116">This new service relies heavily on the existing Excel Services REST API.</span></span>
  
    
    

### 
<span data-ttu-id="832c5-117"><a name="xlsOdata"> </a></span><span class="sxs-lookup"><span data-stu-id="832c5-117"></span></span>


> <span data-ttu-id="832c5-118">**Примечание:** Интерактивное представление Excel возможность отключена.</span><span class="sxs-lookup"><span data-stu-id="832c5-118">**Note:** The Excel Interactive View feature has been disabled.</span></span> <span data-ttu-id="832c5-119">Сведения об удалении этой функции из веб-сайте содержатся [Удаление интерактивное представление Excel из веб-страницы](removing-excel-interactive-view-from-a-webpage.md).</span><span class="sxs-lookup"><span data-stu-id="832c5-119">For information about removing this feature from your website, see  [Removing Excel Interactive View from a webpage](removing-excel-interactive-view-from-a-webpage.md).</span></span> 
  
    
    


## <a name="in-this-section"></a><span data-ttu-id="832c5-120">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="832c5-120">In this section</span></span>
<span data-ttu-id="832c5-121"><a name="xlsWhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="832c5-121"></span></span>


-  [<span data-ttu-id="832c5-122">Getting Started with Excel Services</span><span class="sxs-lookup"><span data-stu-id="832c5-122">Getting Started with Excel Services</span></span>](getting-started-with-excel-services.md)
    
  
-  [<span data-ttu-id="832c5-123">Excel Web Services</span><span class="sxs-lookup"><span data-stu-id="832c5-123">Excel Web Services</span></span>](excel-web-services.md)
    
  
-  [<span data-ttu-id="832c5-124">Excel Services User-Defined Functions</span><span class="sxs-lookup"><span data-stu-id="832c5-124">Excel Services User-Defined Functions</span></span>](excel-services-user-defined-functions.md)
    
  
-  [<span data-ttu-id="832c5-125">Excel Web Access</span><span class="sxs-lookup"><span data-stu-id="832c5-125">Excel Web Access</span></span>](excel-web-access.md)
    
  
-  [<span data-ttu-id="832c5-126">Службы Excel ECMAScript (JavaScript, JScript)</span><span class="sxs-lookup"><span data-stu-id="832c5-126">Excel Services ECMAScript (JavaScript, JScript)</span></span>](excel-services-ecmascript-javascript-jscript.md)
    
  
-  [<span data-ttu-id="832c5-127">API-интерфейс REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="832c5-127">Excel Services REST API</span></span>](excel-services-rest-api.md)
    
  
-  [<span data-ttu-id="832c5-128">General Guidelines</span><span class="sxs-lookup"><span data-stu-id="832c5-128">General Guidelines</span></span>](general-guidelines.md)
    
  
-  [<span data-ttu-id="832c5-129">Удаление интерактивное представление Excel из веб-страницы</span><span class="sxs-lookup"><span data-stu-id="832c5-129">Removing Excel Interactive View from a webpage</span></span>](removing-excel-interactive-view-from-a-webpage.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="832c5-130">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="832c5-130">Additional resources</span></span>
<span data-ttu-id="832c5-131"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="832c5-131"></span></span>


-  [<span data-ttu-id="832c5-132">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="832c5-132">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="832c5-133">Службы приложений Office 2013 и SharePoint</span><span class="sxs-lookup"><span data-stu-id="832c5-133">Office 2013 and SharePoint application services</span></span>](office-and-sharepoint-application-services.md)
    
  

  
    
    

