---
title: "Создание внешнего типа контента из источника OData в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bc60ea49-c44e-4531-af62-06b8cf77d35d
ms.openlocfilehash: 9ddf00811e05fcca25b4c4f406ac22ce5de9aca0
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-an-external-content-type-from-an-odata-source-in-sharepoint"></a><span data-ttu-id="c3add-102">Создание внешнего типа контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-102">Create an external content type from an OData source in SharePoint</span></span>

<span data-ttu-id="c3add-103">Узнайте, как использовать Visual Studio 2012 для обнаружения опубликованного источника OData и создать для повторного использования внешний тип контента для использования в Business Connectivity Services (BCS) в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c3add-103">Learn how to use Visual Studio 2012 to discover a published OData source and create a reusable external content type for use in Business Connectivity Services (BCS) in SharePoint.</span></span>

## <a name="prerequisites-for-creating-odata-based-external-content-types"></a><span data-ttu-id="c3add-104">Необходимые условия для создания на основе OData внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="c3add-104">Prerequisites for creating OData-based external content types</span></span>
<span data-ttu-id="c3add-105"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="c3add-105"></span></span>

<span data-ttu-id="c3add-106">Чтобы создать внешний тип контента из источника Open Data protocol (OData), необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="c3add-106">To create an external content type from an Open Data protocol (OData) source, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="c3add-107">Экземпляр SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-107">An instance of SharePoint</span></span>
    
  
- <span data-ttu-id="c3add-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c3add-108">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="c3add-109">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c3add-109">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="c3add-110">Опубликованные службы OData, доступные через Интернет</span><span class="sxs-lookup"><span data-stu-id="c3add-110">A published OData service available through the Internet</span></span>
    
  
<span data-ttu-id="c3add-111">Сведения о настройке среды разработки SharePoint см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c3add-111">For information about how to set up your SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

> <span data-ttu-id="c3add-112">**Примечание:** SharePoint Designer 2013 не может использоваться для моделей BDC автоматически заполнять из источника OData.</span><span class="sxs-lookup"><span data-stu-id="c3add-112">**Note:** SharePoint Designer 2013 can't be used to autogenerate BDC models from an OData source.</span></span> <span data-ttu-id="c3add-113">Вместо этого можно использовать Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="c3add-113">You can use Visual Studio 2012 instead.</span></span> 
  
    
    


### <a name="core-concepts-for-working-with-odata-external-content-types"></a><span data-ttu-id="c3add-114">Основные понятия, которые для работы с внешними типами контента OData</span><span class="sxs-lookup"><span data-stu-id="c3add-114">Core concepts for working with OData external content types</span></span>

<span data-ttu-id="c3add-115">В следующих статьях представлены общие сведения о OData и соединитель OData в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c3add-115">The following articles provide background information about OData and the OData connector in SharePoint.</span></span>
  
    
    

<span data-ttu-id="c3add-116">**В таблице 1. Основные понятия, которые OData внешних типов контента**</span><span class="sxs-lookup"><span data-stu-id="c3add-116">**Table 1. Core concepts for OData external content types**</span></span>


|<span data-ttu-id="c3add-117">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="c3add-117">**Article title**</span></span>|<span data-ttu-id="c3add-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="c3add-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="c3add-119">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-119">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="c3add-120">Начало работы с Создание внешних типов контента на основе источников OData и узнайте, как использовать эти данные в SharePoint или Office компонентов.</span><span class="sxs-lookup"><span data-stu-id="c3add-120">Get started with creating external content types based on OData sources, and learn how to use that data in SharePoint or Office components.</span></span>  <br/> |
| [<span data-ttu-id="c3add-121">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-121">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="c3add-122">Сведения о внешних типов контента службы BCS и что необходимо для их создания в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c3add-122">Learn about BCS external content types and what you need to start creating them in SharePoint.</span></span>  <br/> |
   

## <a name="create-an-odata-based-external-content-type"></a><span data-ttu-id="c3add-123">Создание на основе OData внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="c3add-123">Create an OData-based external content type</span></span>
<span data-ttu-id="c3add-124"><a name="bkmk_CreatingODataECT"> </a></span><span class="sxs-lookup"><span data-stu-id="c3add-124"></span></span>

<span data-ttu-id="c3add-125">Далее показано, как использовать Visual Studio 2012 для создания внешнего типа контента на основе источника OData.</span><span class="sxs-lookup"><span data-stu-id="c3add-125">The following steps show how to use Visual Studio 2012 to create an external content type based on an OData source.</span></span>
  
    
    

### <a name="to-create-a-new-sharepoint-add-in"></a><span data-ttu-id="c3add-126">Чтобы создать новый Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-126">To create a new SharePoint Add-in</span></span>


1. <span data-ttu-id="c3add-127">В Visual Studio 2012 создайте новый проект **приложения для SharePoint,** расположенный в узле **шаблона SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="c3add-127">In Visual Studio 2012, create a new **App for SharePoint** project, which is located under the **SharePoint template** node.</span></span>
    
  
2. <span data-ttu-id="c3add-128">Назовите проект и нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="c3add-128">Name your project, and choose **OK**.</span></span>
    
  
3. <span data-ttu-id="c3add-129">Чтобы настроить параметры SharePoint, введите имя для вашего приложения и URL-адрес сервера SharePoint, которые вам будет находиться в режиме отладки от.</span><span class="sxs-lookup"><span data-stu-id="c3add-129">To specify the SharePoint settings, enter a name for your app, and the URL of the SharePoint server you will be debugging against.</span></span>
    
  
4. <span data-ttu-id="c3add-130">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c3add-130">Choose **Finish**.</span></span>
    
  
<span data-ttu-id="c3add-131">После создания проекта можно использовать новые автоматическое формирование, создание для источников OData и добавьте модели BDC для источника OData для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c3add-131">After the project is created, you use the new autogeneration tooling for OData sources and add a BDC model for the OData source to your app.</span></span>
  
    
    

### <a name="to-add-a-new-bdc-model"></a><span data-ttu-id="c3add-132">Добавление новой модели BDC</span><span class="sxs-lookup"><span data-stu-id="c3add-132">To add a new BDC model</span></span>


1. <span data-ttu-id="c3add-133">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="c3add-133">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
    <span data-ttu-id="c3add-134">Будет запущен мастер, который поможет обнаружить выбранного источника данных и создать модель BDC.</span><span class="sxs-lookup"><span data-stu-id="c3add-134">This starts a wizard that will help you discover the selected data source and create the BDC model.</span></span>
    
  
2. <span data-ttu-id="c3add-p102">Первая страница мастера используется для сбора URL-адрес службы данных. На странице **Укажите источника OData** введите URL-адрес, который вы хотите подключиться к службы OData. URL-адрес должен выглядеть следующим образом: `http://services.odata.org/Northwind/Northwind.svc/`.</span><span class="sxs-lookup"><span data-stu-id="c3add-p102">The first page of the wizard is used to collect the URL of the data service. On the **Specify OData Source** page, enter the URL of the OData service that you want to connect to. The URL should resemble the following: `http://services.odata.org/Northwind/Northwind.svc/`.</span></span>
    
    > <span data-ttu-id="c3add-138">**Примечание:** Службы данных "Борей", который доступен в списке производители, найденные на [веб-сайт Open Data Protocol](http://www.odata.org/ecosystem#liveservices)будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="c3add-138">**Note:** You will show the Northwind service that is available from the producers list found on the  [Open Data Protocol website](http://www.odata.org/ecosystem#liveservices).</span></span> 
3. <span data-ttu-id="c3add-139">Выберите имя для источника OData и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c3add-139">Choose a name for your OData source, and then choose **Next**.</span></span>
    
  
4. <span data-ttu-id="c3add-p103">Появится список сущностей данные, предоставляемые интерфейсом службы OData. Выберите один или несколько сущностей и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c3add-p103">A list of data entities that are being exposed by the OData Service appears. Select one or more of the entities, and choose **Finish**.</span></span>
    
  

### <a name="to-view-the-structure-of-the-entities"></a><span data-ttu-id="c3add-142">Чтобы просмотреть структуру сущностей</span><span class="sxs-lookup"><span data-stu-id="c3add-142">To view the structure of the entities</span></span>


- <span data-ttu-id="c3add-p104">Обратите внимание, что Visual Studio, создать новую папку с именем внешних типов контента. В этой папке можно найти вложенную папку с именем новый источник данных. При дальнейшей развернуть это, появится элемент, представляющий объект, который вы выбрали. Чтобы просмотреть графический список сущностей и их типы, откройте файл **внешнего типа контента**, который требуется просмотреть.</span><span class="sxs-lookup"><span data-stu-id="c3add-p104">Notice that Visual Studio created a new folder named External Content Types. Inside that folder, you will find a subfolder with the name of your new data source. If you further expand this, you will see an item that represents the entity you selected. To view a graphical list of the entities and their types, open the **ect** file that you want to view.</span></span>
    
    <span data-ttu-id="c3add-147">XML-код сущности, можно также просмотреть, открыв файлы внешнего типа контента в редакторе XML.</span><span class="sxs-lookup"><span data-stu-id="c3add-147">You can also view the XML of the entities by opening the ect files in an XML editor.</span></span>
    
  

## <a name="use-a-stream-accessor-for-the-odata-source"></a><span data-ttu-id="c3add-148">Использование доступа к данным потока для источника OData</span><span class="sxs-lookup"><span data-stu-id="c3add-148">Use a stream accessor for the OData source</span></span>
<span data-ttu-id="c3add-149"><a name="bkmk_UseStreamAccessor"> </a></span><span class="sxs-lookup"><span data-stu-id="c3add-149"></span></span>

<span data-ttu-id="c3add-150">Путем добавления следующего кода можно получить доступ к потоку данных, можно использовать соединитель OData.</span><span class="sxs-lookup"><span data-stu-id="c3add-150">Using the following code, you can access a data stream that the OData connector can use.</span></span>
  
    
    

```cs

/*Invoke  Stream Accessor Method */
        internal void ExecuteStreamAccessorMethod(IEntityInstance entityInstance, string streamAccessorName)
        {
            this.Log.Comment("ExecuteStreamAccessorMethod enter");
            this.Log.Comment("streamAccesor method" + streamAccessorName);
            IStreamableField isf = entityInstance.GetStreamableField(streamAccessorName);
            Stream resStream = isf.GetData();
            using (BinaryReader reader = new BinaryReader(resStream))
            {
                using (FileStream fs = File.Create(@"C:\\" + entityInstance.GetIdentity().GetIdentifierValues()[0] + ".jpg"))
                {
                    int bytesRead = 0;
                    do
                    {
                        int nrBytes = 80 * 1000 * 1000;
                        byte[] streamData = new byte[nrBytes];
                        bytesRead = reader.Read(streamData, 0, nrBytes);
                        this.Log.Comment("Total Bytes Read - " + bytesRead);
                        if (bytesRead > 0)
                        {
                            fs.Write(streamData, 0, bytesRead);
                        }
                    } while (bytesRead > 0);
                }
            }
            isf.Dispose();
            this.Log.Comment("ExecuteStreamAccessorMethod Exit" );
        }
```


## <a name="next-steps"></a><span data-ttu-id="c3add-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3add-151">Next steps</span></span>
<span data-ttu-id="c3add-152"><a name="bkmk_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="c3add-152"></span></span>

<span data-ttu-id="c3add-153">После создания внешнего типа контента его можно использовать на предоставление данных в SharePoint с помощью встроенных объектов (внешние списки, веб-части Business данных или пользовательский код).</span><span class="sxs-lookup"><span data-stu-id="c3add-153">After you have built an external content type, you can then use it to present data inside SharePoint by using the built-in objects (external lists, Business Data Web Parts, or custom code).</span></span>
  
    
    
<span data-ttu-id="c3add-154">Дополнительные сведения можно [как: Создание внешнего списка с помощью источника данных OData в SharePoint](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c3add-154">For more information, see  [How to: Create an external list using an OData data source in SharePoint](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="c3add-155">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c3add-155">Additional resources</span></span>
<span data-ttu-id="c3add-156"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="c3add-156"></span></span>


-  [<span data-ttu-id="c3add-157">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-157">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c3add-158">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-158">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c3add-159">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-159">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c3add-160">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c3add-160">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  

