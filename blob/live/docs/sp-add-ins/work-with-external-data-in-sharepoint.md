---
title: "Работа с внешними данными в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a3d356feac69517b2d0f0e443460ea984605f8fe
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="work-with-external-data-in-sharepoint"></a><span data-ttu-id="e1ab1-102">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1ab1-102">Work with external data in SharePoint</span></span>
<span data-ttu-id="e1ab1-103">Здесь вы найдете ресурсы и рекомендации по доступу к внешним данным и операциям с ними с помощью JavaScript на страницах надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e1ab1-103">Find resources and guidance for accessing and manipulating external data with JavaScript on pages in SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="e1ab1-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="e1ab1-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="use-javascript-in-sharepoint-add-ins"></a><span data-ttu-id="e1ab1-107">Использование JavaScript в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1ab1-107">Use JavaScript in SharePoint Add-ins</span></span>
<span data-ttu-id="e1ab1-108"><a name="SP15Workdata_Working"> </a></span><span class="sxs-lookup"><span data-stu-id="e1ab1-108"><a name="SP15Workdata_Working"> </a></span></span>

<span data-ttu-id="e1ab1-p102">В Надстройки SharePoint часто необходимо получать данные, предоставляемые удаленным веб-приложением или службой на странице или в компоненте SharePoint, и управлять ими. Так как пользовательский код не разрешен на серверах SharePoint, надстройка должна использовать для этой цели JavaScript. Модель для надстроек SharePoint предоставляет несколько вариантов для доступа к удаленным данным и службам.</span><span class="sxs-lookup"><span data-stu-id="e1ab1-p102">In your SharePoint Add-ins, you will frequently have to retrieve and manipulate data that is exposed by a remote web application or service from within a SharePoint page or component. Because custom code is not allowed on the SharePoint servers, your add-in must use JavaScript for this purpose. The model for SharePoint Add-ins provides multiple options for accessing the remote data and services.</span></span>
 

 

### <a name="use-the-sharepoint-cross-domain-javascript-library-to-access-external-data"></a><span data-ttu-id="e1ab1-112">Использование междоменной библиотеки JavaScriptSharePoint для доступа к внешним данным</span><span class="sxs-lookup"><span data-stu-id="e1ab1-112">Use the SharePoint cross-domain JavaScript library to access external data</span></span>

<span data-ttu-id="e1ab1-p103">Междоменную библиотеку можно использовать в вашем удаленном веб-приложении для получения доступа к данным, если вы предоставляете пользовательскую страницу прокси, расположенную в удаленной инфраструктуре. Как разработчик вы должны работать с настраиваемой логикой, например, механизмом проверки подлинности (если он существует) для удаленного приложения, и несете ответственность за реализацию пользовательской страницы прокси. Используйте междоменную библиотеку, если необходимо осуществлять взаимодействие между удаленным источником данных и страницей SharePoint на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="e1ab1-p103">You can use the cross-domain library to access data in your remote web application if you provide a custom proxy page that is hosted in the remote infrastructure. As the developer, you are responsible for implementing the custom proxy page and you have to deal with custom logic such as the authentication mechanism, if there is one, to the remote application. Use the cross-domain library if you want the communication between the remote data source and the SharePoint page to occur at the client level.</span></span>
 

 
<span data-ttu-id="e1ab1-116">Сведения о том, как использовать библиотеку таким способом, см. в статье [Создание пользовательской прокси-страницы для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab1-116">For details about how to use the library in this way, see  [Create a custom proxy page for the cross-domain library in SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md).</span></span>
 

 

 <span data-ttu-id="e1ab1-p104">**Примечание.** Междоменную библиотеку SharePoint также можно использовать в другом направлении, т. е. JavaScript на удаленных веб-страницах с ее помощью может получать доступ к данным в SharePoint. Дополнительные сведения о таком применении библиотеки см. в статье [Создание надстроек SharePoint, использующих междоменную библиотеку](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab1-p104">**Note**  The SharePoint cross-domain library can also be used in the other direction; that is, JavaScript on remote web pages can use it to access data from SharePoint. For more information about this use of the library, see  [Creating SharePoint Add-ins that use the cross-domain library](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md).</span></span>
 


### <a name="use-the-sharepoint-web-proxy-to-access-external-data"></a><span data-ttu-id="e1ab1-119">Доступ ко внешним данным с помощью веб-прокси SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1ab1-119">Use the SharePoint web proxy to access external data</span></span>

<span data-ttu-id="e1ab1-p105">Вы можете использовать веб-прокси, который предоставляется в клиентской объектной модели JavaScript, для доступа к удаленным данным. (Веб-прокси также доступны в клиентской объектной модели .NET, но ее невозможно применять в коде, работающем на серверах SharePoint). При использовании веб-прокси вы передаете запрос инициализации в SharePoint. В свою очередь, SharePoint запрашивает данные в определенной конечной точке и передает ответ обратно на вашу страницу. Используйте веб-прокси, если необходимо осуществлять взаимодействие между удаленным источником данных и страницей SharePoint на уровне сервера.</span><span class="sxs-lookup"><span data-stu-id="e1ab1-p105">You can use the web proxy that is exposed in the JavaScript client object model to access remote data. (The proxy is also available in the .NET client-side object model (CSOM), but you cannot use that object model in code that runs on the SharePoint servers.) When you use the web proxy, you issue the initial request to SharePoint. In turn, SharePoint requests the data to the specified endpoint and forwards the response back to your page. Use the web proxy when you want the communication between the remote data source and the SharePoint page to occur at the server level.</span></span>
 

 
<span data-ttu-id="e1ab1-124">Дополнительные сведения о том, как использовать прокси, см. в статье [Отправка запросов удаленной службе с помощью веб-прокси в SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e1ab1-124">For details about how to use the proxy, see  [Query a remote service using the web proxy in SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="e1ab1-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e1ab1-125">Additional resources</span></span>
<span data-ttu-id="e1ab1-126"><a name="SP15Workdata_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="e1ab1-126"><a name="SP15Workdata_AddRes"> </a></span></span>


-  [<span data-ttu-id="e1ab1-127">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1ab1-127">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="e1ab1-128">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e1ab1-128">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 

