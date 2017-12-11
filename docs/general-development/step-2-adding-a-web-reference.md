---
title: "Этап 2. Добавление веб-ссылки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e9175863-ddb4-4750-847d-d53cb59b33cb
ms.openlocfilehash: 8f306628c2fa335631c441c905bfb1d6d87e79d8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="step-2-adding-a-web-reference"></a><span data-ttu-id="b201c-102">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="b201c-102">Step 2: Adding a Web Reference</span></span>

<span data-ttu-id="b201c-p101">Обнаружение веб-службы  это процесс, с помощью которого клиент определяет местоположение веб-службы и получает соответствующее описание службы. Процесс обнаружения веб-службы в Visual Studio включает опрос веб-сайта в соответствии с заданным алгоритмом. Целью этого процесса является выяснение расположения описания службы, которое является документом XML, использующим язык WSDL.</span><span class="sxs-lookup"><span data-stu-id="b201c-p101">Web service discovery is the process by which a client locates a Web service and obtains its service description. The process of Web service discovery in Visual Studio involves interrogating a Web site following a predetermined algorithm. The goal of the process is to locate the service description, which is an XML document that uses the Web Services Description Language (WSDL).</span></span>
  
    
    

<span data-ttu-id="b201c-p102">В описании службы указывается, какие службы доступны и каким образом осуществляется взаимодействие с этими службами. В отсутствие описания службы программное взаимодействие с веб-службой невозможно. Приложение должно располагать средствами взаимодействия с веб-службой и поиска ее расположения во время выполнения. При добавлении в проект для веб-службы веб-ссылки создается прокси-класс, который взаимодействует с веб-службой и обеспечивает локальное представление веб-службы. Дополнительные сведения см. в разделе "Веб-ссылки и создание прокси-класса веб-службы XML" в документации Microsoft Visual Studio 2005.</span><span class="sxs-lookup"><span data-stu-id="b201c-p102">The service description describes what services are available and how to interact with those services. Without a service description, it is impossible to programmatically interact with a Web service. Your application must have a means to communicate with the Web service and to locate it at run time. Adding a Web reference to your project for the Web service does this by generating a proxy class that interfaces with the Web service and provides a local representation of the Web service. For more information, see "Web References and Generating an XML Web Service Proxy" in the Microsoft Visual Studio 2005 documentation.</span></span>
  
    
    


## <a name="to-add-a-web-reference"></a><span data-ttu-id="b201c-111">Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="b201c-111">To add a Web Reference</span></span>


1. <span data-ttu-id="b201c-112">В меню **Проект** выберите пункт **Добавить веб-ссылку**.</span><span class="sxs-lookup"><span data-stu-id="b201c-112">On the **Project** menu, click **Add Web Reference**.</span></span>
    
  
2. <span data-ttu-id="b201c-p103">В поле **URL-адрес** диалогового окна **Добавить веб-ссылку** введите URL-адрес для получения описания веб-служб Веб-службы Excel, например `http://<server>/<customsite>/_vti_bin/excelservice.asmx` или `http://<server>/_vti_bin/excelservice.asmx`. Затем нажмите кнопку **Найти**, чтобы получить сведения о веб-службе.</span><span class="sxs-lookup"><span data-stu-id="b201c-p103">In the **URL** box of the **Add Web Reference** dialog box, type the URL to obtain the service description of the Excel Web Services, such as `http://<server>/<customsite>/_vti_bin/excelservice.asmx` or `http://<server>/_vti_bin/excelservice.asmx`. Then click **Go** to retrieve information about the Web service.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b201c-115">[!Примечание] Кроме того, диалоговое окно **Добавить веб-ссылку** можно открыть в области **Обозреватель решений**, щелкнув элемент **Ссылки** правой кнопкой мыши и выбрав **Добавить веб-ссылку**.</span><span class="sxs-lookup"><span data-stu-id="b201c-115">You can also open the **Add Web Reference** dialog box in the **Solution Explorer** pane by right-clicking **References** and selecting **Add Web Reference**.</span></span> 
    
3. <span data-ttu-id="b201c-116">В поле **Имя веб-ссылки** задайте имяExcelWebService.</span><span class="sxs-lookup"><span data-stu-id="b201c-116">In the **Web reference name** box, rename the Web reference toExcelWebService.</span></span>
    
  
4. <span data-ttu-id="b201c-117">Нажмите кнопку **Добавить ссылку**, чтобы добавить веб-ссылку в нужную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="b201c-117">Click **Add Reference** to add a Web reference for the target Web service.</span></span>
    
  
5. <span data-ttu-id="b201c-118">Visual Studio выполнит загрузку описания службы и создание прокси-класса для взаимодействия приложения и веб-служб Веб-службы Excel.</span><span class="sxs-lookup"><span data-stu-id="b201c-118">Visual Studio downloads the service description and generates a proxy class to interface between your application and Excel Web Services.</span></span> 
    
  
6. <span data-ttu-id="b201c-119">Дополнительные сведения см. в разделе  [Доступ к API SOAP](accessing-the-soap-api.md).</span><span class="sxs-lookup"><span data-stu-id="b201c-119">For more information, see  [Accessing the SOAP API](accessing-the-soap-api.md).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="b201c-120">См. также</span><span class="sxs-lookup"><span data-stu-id="b201c-120">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="b201c-121">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="b201c-121">Concepts</span></span>


  
    
    
 [<span data-ttu-id="b201c-122">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="b201c-122">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="b201c-123">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="b201c-123">Other resources</span></span>


  
    
    
 [<span data-ttu-id="b201c-124">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="b201c-124">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="b201c-125">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="b201c-125">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="b201c-126">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="b201c-126">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="b201c-127">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="b201c-127">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
