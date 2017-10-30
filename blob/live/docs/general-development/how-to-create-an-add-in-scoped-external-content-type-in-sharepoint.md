---
title: "Как создать добавить в пределах внешнего типа контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: de4b50a3-84da-48ce-9ba0-fe06571e52a8
ms.openlocfilehash: 385bec9d7904031dee03347afc83974da7c3b6a0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-an-add-in-scoped-external-content-type-in-sharepoint"></a><span data-ttu-id="c9e84-102">Как: создать добавить в пределах внешнего типа контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-102">How to: Create an add-in-scoped external content type in SharePoint</span></span>
<span data-ttu-id="c9e84-103">Узнайте, как создать внешний тип контента, который можно устанавливать, защищать и использовать в Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9e84-103">Learn how to create external content types that can be installed, secured, and used in an SharePoint Add-in.</span></span>
## <a name="prerequisites-for-developing-add-in-scoped-external-content-types"></a><span data-ttu-id="c9e84-104">Предварительные требования для разработки добавьте в пределах внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="c9e84-104">Prerequisites for developing add-in-scoped external content types</span></span>
<span data-ttu-id="c9e84-105"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="c9e84-105"></span></span>

<span data-ttu-id="c9e84-106">Для начала разработки добавьте в пределах внешних типов контента, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="c9e84-106">To get started developing add-in-scoped external content types, you need the following:</span></span>
  
    
    

- <span data-ttu-id="c9e84-107">SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-107">SharePoint</span></span>
    
  
- <span data-ttu-id="c9e84-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c9e84-108">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="c9e84-109">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c9e84-109">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="c9e84-110">Опубликованные службы OData, доступные через Интернет</span><span class="sxs-lookup"><span data-stu-id="c9e84-110">A published OData service available through the Internet</span></span>
    
  
<span data-ttu-id="c9e84-111">Сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c9e84-111">For information about setting up a SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="create-an-add-in-scoped-external-content-type"></a><span data-ttu-id="c9e84-112">Создание добавить в пределах внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="c9e84-112">Create an add-in-scoped external content type</span></span>
<span data-ttu-id="c9e84-113"><a name="bkmk_CreateECT"> </a></span><span class="sxs-lookup"><span data-stu-id="c9e84-113"></span></span>

<span data-ttu-id="c9e84-114">Далее показано, как создать внешний тип контента на основе источника Open Data protocol (OData) и изменить его ограничиваться вашей Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9e84-114">The following steps show how to create an external content type based on an Open Data protocol (OData) source, and how to modify it to be scoped to your SharePoint Add-in.</span></span>
  
    
    

### <a name="to-create-a-new-sharepoint-add-in"></a><span data-ttu-id="c9e84-115">Чтобы создать новый Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-115">To create a new SharePoint Add-in</span></span>


1. <span data-ttu-id="c9e84-116">Откройте Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="c9e84-116">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="c9e84-117">Создайте проект **надстройки для SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="c9e84-117">Create an **Add-in for SharePoint** project.</span></span>
    
  
3. <span data-ttu-id="c9e84-p101">Укажите параметры надстроек, включая имя, URL-адрес сайта для отладки надстройки и способ для размещения надстройки (автоматическим размещением, размещением у поставщика или размещением в SharePoint). Для получения дополнительных сведений см  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9e84-p101">Specify the add-in settings, including add-in name, the site URL for debugging the add-in, and how you would like to host the add-in (Autohosted, Provider-hosted, or SharePoint-hosted). For more information, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
    
  
4. <span data-ttu-id="c9e84-120">Нажмите кнопку **Готово**, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="c9e84-120">Choose **Finish** to create the app.</span></span>
    
  
<span data-ttu-id="c9e84-121">Для завершения действия по созданию Надстройки SharePoint см.:</span><span class="sxs-lookup"><span data-stu-id="c9e84-121">For complete steps for creating SharePoint Add-ins, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="c9e84-122">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="c9e84-122">Get started creating provider-hosted SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/3038dd73-41ee-436f-8c78-ef8e6869bf7b%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c9e84-123">Инструкции. Создание базового приложения с автоматическим размещением для SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-123">How to: Create a basic autohosted app for SharePoint</span></span>](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c9e84-124">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-124">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx)
    
  

### <a name="to-generate-the-external-content-type"></a><span data-ttu-id="c9e84-125">Для создания внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="c9e84-125">To generate the external content type</span></span>


1. <span data-ttu-id="c9e84-126">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="c9e84-126">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
    <span data-ttu-id="c9e84-127">Будет запущен мастер, которая поможет вам найти выбранного источника данных и создать модель BDC.</span><span class="sxs-lookup"><span data-stu-id="c9e84-127">This starts a wizard that helps you find the selected data source and create the BDC model.</span></span>
    
  
2. <span data-ttu-id="c9e84-p102">На странице **Настройка источника OData** введите URL-адрес, который вы хотите подключиться к службы OData. URL-адрес должен выглядеть примерно следующим образом: `http://services.odata.org/Northwind/Northwind.svc/`.</span><span class="sxs-lookup"><span data-stu-id="c9e84-p102">On the **Set OData Source** page, enter the URL of the OData service that you want to connect to. The URL should look something like this: `http://services.odata.org/Northwind/Northwind.svc/`.</span></span>
    
    <span data-ttu-id="c9e84-130">Укажите имя для источника OData.</span><span class="sxs-lookup"><span data-stu-id="c9e84-130">Specify a name for your OData source.</span></span>
    
    > <span data-ttu-id="c9e84-131">**Примечание:** В данном примере необходимо использовать службы данных "Борей", который доступен в списке производители, расположенный на [веб-сайт Open Data Protocol](http://www.odata.org).</span><span class="sxs-lookup"><span data-stu-id="c9e84-131">**Note:** For this example, you will use the Northwind service that is available from the producers list located on the  [Open Data Protocol website](http://www.odata.org).</span></span> 
3. <span data-ttu-id="c9e84-p103">Появится список сущностей отображение данных, предоставляемые интерфейсом службы OData. Выберите один или несколько сущностей и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c9e84-p103">A list appears showing data entities that are being exposed by the OData Service. Select one or more of the entities, and choose **Finish**.</span></span>
    
  

### <a name="to-deploy-the-add-in-scoped-external-content-type"></a><span data-ttu-id="c9e84-134">Чтобы развернуть добавить в пределах внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="c9e84-134">To deploy the add-in-scoped external content type</span></span>


- <span data-ttu-id="c9e84-135">Нажмите клавишу F5, чтобы скомпилировать и передача файлов проекта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9e84-135">Press F5 to compile the project and upload the project files to SharePoint.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="c9e84-136">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c9e84-136">Additional resources</span></span>
<span data-ttu-id="c9e84-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c9e84-137"></span></span>


-  [<span data-ttu-id="c9e84-138">Добавьте в пределах внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-138">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c9e84-139">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-139">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c9e84-140">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-140">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c9e84-141">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-141">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c9e84-142">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-142">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c9e84-143">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9e84-143">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  

