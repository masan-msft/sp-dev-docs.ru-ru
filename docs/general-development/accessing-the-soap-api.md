---
title: "Доступ к API SOAP"
ms.date: 09/25/2017
keywords: soap
f1_keywords: soap
ms.prod: sharepoint
ms.assetid: 36e8e3d5-83ac-4bd3-b556-1af132add3eb
ms.openlocfilehash: 41b6656034d9e67fedca44684444bfb73d667e02
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="accessing-the-soap-api"></a><span data-ttu-id="32531-103">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="32531-103">Accessing the SOAP API</span></span>

<span data-ttu-id="32531-p101">Веб-службы Excel использует Simple Object Access Protocol (SOAP) по протоколу HTTP и действует как интерфейс связи между клиентских программ и Службы Excel. Веб-службы состоит из набора сложный тип объектов, которые можно использовать для доступа к всех функциональных возможностей Веб-службы Excel и методов. Для вызова службы, должен ссылаться Веб-службы Excel языка описания веб-служб (WSDL).</span><span class="sxs-lookup"><span data-stu-id="32531-p101">Excel Web Services uses Simple Object Access Protocol (SOAP) over HTTP and acts as a communications interface between client programs and Excel Services. The Web service consists of methods and a set of complex type objects that you can use to access the complete functionality of Excel Web Services. To call the service, you must reference the Excel Web Services Web Services Description Language (WSDL).</span></span>
  
    
    


## <a name="referencing-the-wsdl"></a><span data-ttu-id="32531-107">Создание ссылок на WSDL</span><span class="sxs-lookup"><span data-stu-id="32531-107">Referencing the WSDL</span></span>

<span data-ttu-id="32531-p102">Для успешного вызова веб-службы, необходимо знать, как получить доступ к службе, какие операции службы поддерживает, какие параметры службы ожидает и возвращает какие службы. WSDL предоставляет эти сведения в XML-документ, чтение или обработки компьютером.</span><span class="sxs-lookup"><span data-stu-id="32531-p102">To call a Web service successfully, you must know how to access the service, what operations the service supports, what parameters the service expects, and what the service returns. WSDL provides this information in an XML document that can be read or processed by a computer.</span></span>
  
    
    
<span data-ttu-id="32531-p103">WSDL для конечной точки Веб-службы Excel доступен через  `ExcelServices.asmx?wsdl`. WSDL можно размещать на наборы средств разработки, которые поддерживают SOAP и веб-службы, такие как Microsoft .NET Framework SDK.</span><span class="sxs-lookup"><span data-stu-id="32531-p103">The WSDL for the Excel Web Services endpoint is accessed through  `ExcelServices.asmx?wsdl`. WSDL can be consumed by development kits that support SOAP and Web services, such as the Microsoft .NET Framework SDK.</span></span>
  
    
    
<span data-ttu-id="32531-112">В следующем примере показано формат URL-адрес для WSDL-файла Веб-службы Excel:</span><span class="sxs-lookup"><span data-stu-id="32531-112">The following example shows the format of the URL to the Excel Web Services WSDL file:</span></span>
  
    
    
 `http://<server>/<customsite>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
<span data-ttu-id="32531-113">Если специализированный сайт отсутствует, можно использовать следующий URL-адрес временно:</span><span class="sxs-lookup"><span data-stu-id="32531-113">If you do not have a custom site, you can use the following URL temporarily:</span></span>
  
    
    
 `http://<server>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
<span data-ttu-id="32531-114">Рекомендуется создать настраиваемые сайта и затем использовать URL-адрес, который содержит настраиваемого веб-сайта в формат URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="32531-114">It is recommended that you create a custom site, and then use the URL that includes the custom site in the URL format.</span></span>
  
    
    
<span data-ttu-id="32531-115">В следующей таблице описываются каждый элемент в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="32531-115">The following table describes each element in the URL.</span></span>
  
    
    


|<span data-ttu-id="32531-116">**URL-адрес элемента**</span><span class="sxs-lookup"><span data-stu-id="32531-116">**URL element**</span></span>|<span data-ttu-id="32531-117">**Description**</span><span class="sxs-lookup"><span data-stu-id="32531-117">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="32531-118">_server_</span><span class="sxs-lookup"><span data-stu-id="32531-118">_server_</span></span> <br/> |<span data-ttu-id="32531-119">Имя сервера, на котором развернут Microsoft SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="32531-119">The name of the server on which Microsoft SharePoint Server 2010 is deployed.</span></span>  <br/> |
| <span data-ttu-id="32531-120">_customsite_</span><span class="sxs-lookup"><span data-stu-id="32531-120">_customsite_</span></span> <br/> |<span data-ttu-id="32531-121">Сайт настраиваемых SharePoint Server 2010, администратор сервера создает.</span><span class="sxs-lookup"><span data-stu-id="32531-121">A custom SharePoint Server 2010 site that the server administrator creates.</span></span>  <br/> |
| <span data-ttu-id="32531-122">_<endpointname>.asmx_</span><span class="sxs-lookup"><span data-stu-id="32531-122">_<endpointname>.asmx_</span></span> <br/> |<span data-ttu-id="32531-p104">Имя конечной точки веб-службы. Для Веб-службы Excel это  `ExcelService.asmx`.</span><span class="sxs-lookup"><span data-stu-id="32531-p104">The name of the Web service endpoint. For Excel Web Services, it is  `ExcelService.asmx`.  </span></span><br/> |
   
<span data-ttu-id="32531-125">Дополнительные сведения о формате WSDL см WSDL веб Consortium (W3C) http://www.w3.org/TR/wsdl.</span><span class="sxs-lookup"><span data-stu-id="32531-125">For more information about the WSDL format, see the World Wide Web Consortium (W3C) WSDL specification at http://www.w3.org/TR/wsdl.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="32531-126">См. также</span><span class="sxs-lookup"><span data-stu-id="32531-126">See also</span></span>


#### <a name="other-resources"></a><span data-ttu-id="32531-127">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="32531-127">Other resources</span></span>


  
    
    
 [<span data-ttu-id="32531-128">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="32531-128">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="32531-129">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="32531-129">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="32531-130">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="32531-130">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="32531-131">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="32531-131">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="32531-132">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="32531-132">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
