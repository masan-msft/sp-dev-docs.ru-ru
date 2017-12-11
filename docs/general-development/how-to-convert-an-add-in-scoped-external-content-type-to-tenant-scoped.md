---
title: "Преобразование внешнего типа контента для надстройки во внешний тип контента для клиента"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 35c5d670-e402-4641-b3c5-6f61ae1ec69b
ms.openlocfilehash: 0304979fc002526faaa390c87575cf8e97574c66
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="convert-an-add-in-scoped-external-content-type-to-tenant-scoped"></a><span data-ttu-id="c7461-102">Преобразование внешнего типа контента для надстройки во внешний тип контента для клиента</span><span class="sxs-lookup"><span data-stu-id="c7461-102">Convert an add-in-scoped external content type to tenant-scoped</span></span>

<span data-ttu-id="c7461-p101">Сведения о создании основе внешнего типа контента с помощью средств Visual Studio 2012 для автоматического создания и импорта его в Business Connectivity Services (BCS) метаданные хранилища, чтобы они могут использоваться в рабочей области для всей клиента. Модели BDC, сложных определения XML из внешнего источника данных. Они используются при определении внешних типов контента для BCS. Они являются очень неудобен для создания вручную, поэтому средства были созданы для автоматического создания файлов, с помощью Visual Studio 2012 и Инструменты разработчика Office для Visual Studio 2012. С помощью этих средств, можно создать пакет .app, с помощью Visual Studio публикации и затем откройте пакет для извлечения файла модели.</span><span class="sxs-lookup"><span data-stu-id="c7461-p101">Learn how to create an OData-based external content type using Visual Studio 2012 auto-generation tools and import it into the Business Connectivity Services (BCS) metadata store so that it can be used across an entire tenant workspace. BDC models are complex XML definitions of an external data source. They are used when defining external content types for BCS. They are very difficult to build manually, so tools have been built to automatically generate the files using Visual Studio 2012 and Office Developer Tools for Visual Studio 2012. Using these tools, you can create an .app package using Visual Studio publishing, and then open that package to extract the model file.</span></span>
  
    
    


## <a name="extract-the-bdc-model-file-from-a-visual-studio-add-in-package"></a><span data-ttu-id="c7461-108">Извлеките файл модели BDC из пакета надстройки Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7461-108">Extract the BDC model file from a Visual Studio add-in package</span></span>

<span data-ttu-id="c7461-109">Далее показано, как создать основе внешнего типа контента и импортируйте его в хранилище метаданных BCS, чтобы они могут использоваться в рабочей области для всей клиента.</span><span class="sxs-lookup"><span data-stu-id="c7461-109">The following steps show you how to create the OData-based external content type and then import it into the BCS metadata store so that it can be used across an entire tenant workspace.</span></span>
  
    
    

### <a name="to-create-a-bdc-model-file-from-an-odata-source"></a><span data-ttu-id="c7461-110">Создание файла модели BDC из источника OData</span><span class="sxs-lookup"><span data-stu-id="c7461-110">To create a BDC model file from an OData source</span></span>


1. <span data-ttu-id="c7461-111">В Visual Studio 2012 создайте проект **надстройки для SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="c7461-111">In Visual Studio 2012, create an **Add-in for SharePoint** project.</span></span>
    
  
2. <span data-ttu-id="c7461-p102">Укажите параметры надстроек, включая имя, URL-адрес сайта для отладки надстройку, и как будут размещены надстройки ( **автоматическим размещением**, **размещением у поставщика** или **размещением в SharePoint** ). Для получения дополнительных сведений см [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7461-p102">Specify the add-in settings, including add-in name, the site URL for debugging the add-in, and how you want to host the add-in ( **Autohosted**, **Provider-hosted**, or **SharePoint-hosted**). For more information, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
3. <span data-ttu-id="c7461-114">Нажмите кнопку **Готово**, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="c7461-114">Choose **Finish** to create the app.</span></span>
    
  
4. <span data-ttu-id="c7461-115">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="c7461-115">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
    <span data-ttu-id="c7461-116">Будет запущен мастер, которая поможет вам найти выбранного источника данных и создать модель BDC.</span><span class="sxs-lookup"><span data-stu-id="c7461-116">This starts a wizard that helps you find the selected data source and create the BDC model.</span></span>
    
  
5. <span data-ttu-id="c7461-p103">На странице **Настройка источника OData** введите URL-адрес, который вы хотите подключиться к службы OData. URL-адрес должен выглядеть примерно следующим образом: `http://services.odata.org/Northwind/Northwind.svc/`.</span><span class="sxs-lookup"><span data-stu-id="c7461-p103">On the **Set OData Source** page, enter the URL of the OData service that you want to connect to. The URL should look something like this: `http://services.odata.org/Northwind/Northwind.svc/`.</span></span>
    
    <span data-ttu-id="c7461-119">Укажите имя для источника OData.</span><span class="sxs-lookup"><span data-stu-id="c7461-119">Specify a name for your OData source.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c7461-120">[!Примечание] В данном примере необходимо использовать службы данных "Борей", который доступен в списке производители, расположенные на  [веб-сайт Open Data Protocol](http://www.odata.org).</span><span class="sxs-lookup"><span data-stu-id="c7461-120">For this example, you will use the Northwind service that is available from the producers list located on the  [Open Data Protocol website](http://www.odata.org).</span></span> 

6. <span data-ttu-id="c7461-p104">Появится список сущностей отображение данных, предоставляемые интерфейсом службы OData. Выберите один или несколько сущностей и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c7461-p104">A list appears showing data entities that are being exposed by the OData Service. Select one or more of the entities, and choose **Finish**.</span></span>
    
  

### <a name="to-deploy-the-add-in-scoped-external-content-type-as-an-add-in-package"></a><span data-ttu-id="c7461-123">Развернуть как пакет надстроек add в пределах внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="c7461-123">To deploy the add-in-scoped external content type as an add-in package</span></span>


1. <span data-ttu-id="c7461-124">В Visual Studio, в меню **Построение** выберите команду **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c7461-124">In Visual Studio, on the **Build** menu, choose **Publish**.</span></span>
    
  
2. <span data-ttu-id="c7461-125">Укажите имя пакета, укажите сохранить расположение на локальных жестких дисков и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c7461-125">Name the package, specify the save location on your local hard drive, and choose **Finish**.</span></span>
    
  

### <a name="to-extract-the-model-file-from-the-app-package"></a><span data-ttu-id="c7461-126">Чтобы извлечь файл модели из пакета .app</span><span class="sxs-lookup"><span data-stu-id="c7461-126">To extract the model file from the .app package</span></span>


1. <span data-ttu-id="c7461-127">Откройте папку, где создается пакет .app.</span><span class="sxs-lookup"><span data-stu-id="c7461-127">Open the folder where the .app package is created.</span></span>
    
  
2.  <span data-ttu-id="c7461-128">Измените расширение имени файла с .app наZIP.</span><span class="sxs-lookup"><span data-stu-id="c7461-128">Change the file name extension from.app to.zip.</span></span>
    
  
3. <span data-ttu-id="c7461-129">Извлеките ZIP-архив в локальную папку.</span><span class="sxs-lookup"><span data-stu-id="c7461-129">Extract the ZIP package to a local folder.</span></span>
    
  
4. <span data-ttu-id="c7461-130">Откройте папку извлеченные найти WSP-файл.</span><span class="sxs-lookup"><span data-stu-id="c7461-130">Open the extracted folder to find the WSP file.</span></span>
    
  
5. <span data-ttu-id="c7461-131">Перемещение WSP-файла в другое расположение.</span><span class="sxs-lookup"><span data-stu-id="c7461-131">Move the WSP file to another location.</span></span>
    
  
6. <span data-ttu-id="c7461-132">Измените расширение имени файла .wsp на этот файл .cab.</span><span class="sxs-lookup"><span data-stu-id="c7461-132">Change the .wsp file name extension on this file to .cab.</span></span>
    
  
7. <span data-ttu-id="c7461-133">Откройте CAB-файл и файл Bdcmodel.bdcm.</span><span class="sxs-lookup"><span data-stu-id="c7461-133">Open the .cab file, and you will find the Bdcmodel.bdcm file.</span></span>
    
  
8. <span data-ttu-id="c7461-134">Сохраните файл Bdcmodel.bdcm в другое расположение.</span><span class="sxs-lookup"><span data-stu-id="c7461-134">Save the Bdcmodel.bdcm file to another location.</span></span>
    
  

### <a name="to-import-the-model-file-using-sharepoint-central-administration-pages"></a><span data-ttu-id="c7461-135">Чтобы импортировать файл модели, с помощью страниц центра администрирования SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7461-135">To import the model file using SharePoint Central Administration pages</span></span>


1. <span data-ttu-id="c7461-136">Откройте SharePoint Online или SharePoint в локальных страниц центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="c7461-136">Open SharePoint Online or SharePoint on-premises Central Administration pages.</span></span>
    
  
2. <span data-ttu-id="c7461-137">Выберите **Управление обслуживать приложения**.</span><span class="sxs-lookup"><span data-stu-id="c7461-137">Choose **Manage serve applications**.</span></span>
    
  
3. <span data-ttu-id="c7461-138">Выберите **Служба подключения к бизнес-данным**.</span><span class="sxs-lookup"><span data-stu-id="c7461-138">Choose **Business Data Connectivity Service**.</span></span>
    
  
4. <span data-ttu-id="c7461-139">Выберите ссылку **импорта** на ленте сервера.</span><span class="sxs-lookup"><span data-stu-id="c7461-139">Choose the **Import** link on the server ribbon.</span></span>
    
  
5. <span data-ttu-id="c7461-140">Нажмите кнопку **Обзор**, чтобы указать расположение, куда были извлечены BDCM-файл.</span><span class="sxs-lookup"><span data-stu-id="c7461-140">Choose the **Browse** button to specify the location where you extracted the .bdcm file.</span></span>
    
  
6. <span data-ttu-id="c7461-141">Оставьте параметры по умолчанию и нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="c7461-141">Keep the default settings, and then choose **Import**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="c7461-142">См. также</span><span class="sxs-lookup"><span data-stu-id="c7461-142">See also</span></span>
<span data-ttu-id="c7461-143"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c7461-143"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="c7461-144">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7461-144">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c7461-145">Как: создание добавить в пределах внешнего типа контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7461-145">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c7461-146">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7461-146">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c7461-147">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c7461-147">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c7461-148">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="c7461-148">Open Data Protocol</span></span>](http://www.odata.org)
    
  

  
    
    

