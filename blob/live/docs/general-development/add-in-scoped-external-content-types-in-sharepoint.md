---
title: "Добавьте в пределах внешние типы контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a34cbbba-dc38-4d3d-b796-d54b5848bdfb
ms.openlocfilehash: b551602cd4a87422e50e5523e86b6a5e5be8514b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="add-in-scoped-external-content-types-in-sharepoint"></a><span data-ttu-id="4ac73-102">Добавьте в пределах внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-102">Add-in-scoped external content types in SharePoint</span></span>
<span data-ttu-id="4ac73-103">Сведения о внешних типов контента, для которых установлены или областью действия на уровне надстройки в SharePoint и позволяют создавать насыщенные Add-ins SharePoint с помощью внешних источников данных.</span><span class="sxs-lookup"><span data-stu-id="4ac73-103">Learn about external content types that are installed or scoped at the add-in level in SharePoint and enable you to create data-rich SharePoint Add-ins using external data sources.</span></span>
## <a name="overview-of-add-in-scoped-external-content-types-in-sharepoint"></a><span data-ttu-id="4ac73-104">Общие сведения о добавьте в пределах внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-104">Overview of add-in-scoped external content types in SharePoint</span></span>
<span data-ttu-id="4ac73-105"><a name="Appscopedect_overview"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-105"></span></span>

<span data-ttu-id="4ac73-p101">В SharePoint 2010 могут устанавливать и использовать внешние типы контента только на уровне фермы. Это часто вызывает проблемы для разработчиков, поскольку даже для простых приложений администратора были вынуждены принимать участие из-за права доступа, необходимые для установки на уровне фермы.</span><span class="sxs-lookup"><span data-stu-id="4ac73-p101">In SharePoint 2010, you can install and use external content types only at the farm level. This often causes problems for developers because even for simple applications, an administrator had to be involved because of the access rights that are needed to install at the farm level.</span></span>
  
    
    
<span data-ttu-id="4ac73-108">В SharePoint по сути изоляции приложений в более автономных единиц, называемое надстройками надстройки содержат все ресурсы, необходимые для запуска.</span><span class="sxs-lookup"><span data-stu-id="4ac73-108">In SharePoint, applications are basically isolated into more autonomous units called add-ins. Add-ins contain all the resources they need to run.</span></span> <span data-ttu-id="4ac73-109">Данный подход позволяет приложения для изолируется от других приложений.</span><span class="sxs-lookup"><span data-stu-id="4ac73-109">This approach enables a running application to be insulated from other applications.</span></span> <span data-ttu-id="4ac73-110">Преимущества данной архитектуры, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4ac73-110">The benefits of this architecture are as follows:</span></span>
  
    
    

- <span data-ttu-id="4ac73-111">Можно создать надстроек, выровненные с помощью новой модели приложения для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4ac73-111">You can create add-ins that are aligned with the new application model of SharePoint.</span></span>
    
  
- <span data-ttu-id="4ac73-112">Можно создать надстроек, доступа к внешним данным из SAP, Netflix и частный и других типов данных без привлечения администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="4ac73-112">You can create add-ins that access external data from SAP, Netflix, and proprietary and other types of data without involving the tenant administrator.</span></span>
    
  
- <span data-ttu-id="4ac73-113">Доступ к внешним приложениям поддерживать через Службы Business Connectivity Services (BCS), который предоставляет согласованную и универсальный интерфейс, который может использоваться другими приложениями SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4ac73-113">Access to external applications is maintained through Business Connectivity Services (BCS), which provides a consistent and uniform interface that can be used by other SharePoint applications.</span></span>
    
  
<span data-ttu-id="4ac73-114">Добавьте в пределах внешние типы контента предоставляют доступ к внешним данным в приложении.</span><span class="sxs-lookup"><span data-stu-id="4ac73-114">Add-in-scoped external content types provide access to external data within an app.</span></span>
  
    
    

## <a name="prerequisites-for-working-with-add-in-scoped-external-content-types"></a><span data-ttu-id="4ac73-115">Необходимые условия для работы с добавления в пределах внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="4ac73-115">Prerequisites for working with add-in-scoped external content types</span></span>
<span data-ttu-id="4ac73-116"><a name="Appscopedect_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-116"></span></span>

<span data-ttu-id="4ac73-117">Ниже приведены требования для разработки внешних типов контента, которые находятся на уровне надстройки:</span><span class="sxs-lookup"><span data-stu-id="4ac73-117">The following are the requirements for developing external content types that are scoped at the add-in level:</span></span>
  
    
    

- <span data-ttu-id="4ac73-118">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4ac73-118">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="4ac73-119">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4ac73-119">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="4ac73-120">SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-120">SharePoint</span></span>
    
  
<span data-ttu-id="4ac73-121">Сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="4ac73-121">For information about setting up your SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="add-in-scoped-external-content-type-essentials"></a><span data-ttu-id="4ac73-122">Добавьте в пределах внешнего типа контента essentials</span><span class="sxs-lookup"><span data-stu-id="4ac73-122">Add-in-scoped external content type essentials</span></span>

<span data-ttu-id="4ac73-123">В таблице 1 представлены некоторые основные концепции, которые необходимо ознакомиться с при работе с добавления в пределах внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="4ac73-123">Table 1 contains some core concepts that you should be familiar with when working with add-in-scoped external content types.</span></span>
  
    
    

<span data-ttu-id="4ac73-124">**В таблице 1. Основные понятия, которые для понимания добавьте в пределах внешних типов контента**</span><span class="sxs-lookup"><span data-stu-id="4ac73-124">**Table 1. Core concepts for understanding add-in-scoped external content types**</span></span>


|<span data-ttu-id="4ac73-125">**Статья**</span><span class="sxs-lookup"><span data-stu-id="4ac73-125">**Article**</span></span>|<span data-ttu-id="4ac73-126">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4ac73-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="4ac73-127">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-127">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="4ac73-128">Сведения о создании BCS внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="4ac73-128">Learn how to create BCS external content types.</span></span>  <br/> |
| [<span data-ttu-id="4ac73-129">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-129">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="4ac73-130">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.</span><span class="sxs-lookup"><span data-stu-id="4ac73-130">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>  <br/> |
| [<span data-ttu-id="4ac73-131">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-131">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx) <br/> |<span data-ttu-id="4ac73-132">Узнайте, как создать простой SharePoint хостингом надстройки с помощью Инструменты разработчика Office для Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="4ac73-132">Learn how to create a basic SharePoint-hosted add-in by using the Office Developer Tools for Visual Studio 2012.</span></span>  <br/> |
   

## <a name="what-can-you-do-with-add-in-scoped-external-content-types"></a><span data-ttu-id="4ac73-133">Что можно делать с добавления в пределах внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="4ac73-133">What can you do with add-in-scoped external content types?</span></span>
<span data-ttu-id="4ac73-134"><a name="Appscopedect_Tasks"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-134"></span></span>

<span data-ttu-id="4ac73-p103">Для предоставления доступа к внешним данным из отдельных надстроек  основная причина для добавления добавить в пределах внешнего типа контента. Это позволяет выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="4ac73-p103">The primary reason for adding an add-in-scoped external content type is to provide access to external data from an individual add-in. This allows you to do the following:</span></span> 
  
    
    

- <span data-ttu-id="4ac73-137">Ограничение доступа к внешние типы контента для конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="4ac73-137">Limit access to external content types to a particular app.</span></span>
    
  
- <span data-ttu-id="4ac73-138">Развертывание внешних типов контента в пределах приложения.</span><span class="sxs-lookup"><span data-stu-id="4ac73-138">Deploy external content types within an app.</span></span>
    
  

### <a name="create-add-in-scoped-external-content-types"></a><span data-ttu-id="4ac73-139">Добавьте в пределах внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="4ac73-139">Create add-in-scoped external content types</span></span>
<span data-ttu-id="4ac73-140"><a name="Appscopedect_createect"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-140"></span></span>

<span data-ttu-id="4ac73-p104">Понятие каталога на основе файла метаданных была введена в SharePoint 2010. Позволяет указать, что файл, содержащий XML-код необходимый для определения внешних типов контента. Этот файл могут быть развернуты внутри пакета WSP и относится только к приложению, предназначенную для. С помощью этого файла метаданных, внешние типы контента можно ограничить уровень надстройки.</span><span class="sxs-lookup"><span data-stu-id="4ac73-p104">The concept of a file-based metadata catalog was introduced in SharePoint 2010. It enables you to specify a file that contains the XML needed to define external content types. This file can be deployed within a WSP package and pertains only to the application that it is scoped for. By using this metadata file, external content types can be restricted to the add-in level.</span></span>
  
    
    
<span data-ttu-id="4ac73-145">В SharePoint чтобы добавить свойство, которое указывает, области применения была изменена **SPListDataSource** .</span><span class="sxs-lookup"><span data-stu-id="4ac73-145">In SharePoint, **SPListDataSource** has been modified to add a property that indicates the scope of the application.</span></span>
  
    
    
<span data-ttu-id="4ac73-146">Этот класс выступает в качестве моста между **SPList** и внешнего списка.</span><span class="sxs-lookup"><span data-stu-id="4ac73-146">This class serves as the bridge between **SPList** and an external list.</span></span> <span data-ttu-id="4ac73-147">Использование связанного **SPList** для получения данных и полей сущности.</span><span class="sxs-lookup"><span data-stu-id="4ac73-147">Use the associated **SPList** to retrieve entity fields and data.</span></span> <span data-ttu-id="4ac73-148">Получить экземпляр **SPListDataSource** из свойства **HasExternalDataSource** .</span><span class="sxs-lookup"><span data-stu-id="4ac73-148">Retrieve an instance of **SPListDataSource** from the **HasExternalDataSource** property.</span></span> <span data-ttu-id="4ac73-149">При **HasExternalDataSource** не равно null, объект **SPList** данные являются внешними по отношению к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4ac73-149">When **HasExternalDataSource** is not null, the **SPList** object's data is external to SharePoint.</span></span>
  
    
    
<span data-ttu-id="4ac73-150">Если вы хотите добавить добавить в пределах внешнего типа контента, это свойство имеет значение **Add-in**.</span><span class="sxs-lookup"><span data-stu-id="4ac73-150">When you want to add an add-in-scoped external content type, this property is set to **Add-in**.</span></span>
  
    
    
<span data-ttu-id="4ac73-p106">Свойство **MetadataCatalogFileName** используется для определения файла модели BDC, который содержит определение внешнего типа контента. Это свойство может быть определен декларативно или программно, но не в SharePoint пользовательского интерфейса (UI).</span><span class="sxs-lookup"><span data-stu-id="4ac73-p106">The **MetadataCatalogFileName** property is used to define the BDC model file that contains the external content type definition. This property can be defined declaratively or programmatically, but not in the SharePoint user interface (UI).</span></span>
  
    
    
<span data-ttu-id="4ac73-153">Следующем примере показано, как задать свойство **MetadataCatalogFileName** декларативно.</span><span class="sxs-lookup"><span data-stu-id="4ac73-153">The following example shows how to set the **MetadataCatalogFileName** property declaratively.</span></span>
  
    
    



```XML

<DataSource>
  <Property Name="Entity" Value="Customer" />
  <Property Name="EntityNamespace" Value="SAP" />
  <Property Name="LobSystemInstanceName" Value="SAPClient1" />
  <Property Name="SpecificFinder" Value="ReadCustomer" />
  <Property Name=" MetadataCatalogFileName" Value="BDCMetadata.bdcm" />
</DataSource>
```


> <span data-ttu-id="4ac73-154">**Примечание:** Администраторы сайтов можно установить надстройки, использующие областью действия ect приложения, но только администраторы SiteCollection может предоставить разрешения для приложений для использования подключения к службе BCS.</span><span class="sxs-lookup"><span data-stu-id="4ac73-154">**Note:** Site administrators can install add-ins that use App-Scoped-ECTs, but only SiteCollection administrators can grant permissions for Apps to Use BCS Connections.</span></span> 
  
    
    


### <a name="deploy-an-add-in-scoped-external-content-type-in-a-custom-feature-in-a-wsp-file"></a><span data-ttu-id="4ac73-155">Развертывание добавить в пределах внешнего типа контента в настраиваемый компонент в WSP-файла</span><span class="sxs-lookup"><span data-stu-id="4ac73-155">Deploy an add-in-scoped external content type in a custom Feature in a WSP file</span></span>
<span data-ttu-id="4ac73-156"><a name="Appscopedect_deployect"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-156"></span></span>

<span data-ttu-id="4ac73-p107">Модели BDC можно включить в WSP-файла для развертывания. Следующем примере показано, как включить модели BDC в приложение.</span><span class="sxs-lookup"><span data-stu-id="4ac73-p107">You can include a BDC model in a WSP file for deployment. The following example shows how to include a BDC model in the app.</span></span>
  
    
    

```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
  </BdcModel>
</Elements>

```


> <span data-ttu-id="4ac73-159">**Важные:** Только один файл модели BDC можно включить на надстройки.</span><span class="sxs-lookup"><span data-stu-id="4ac73-159">**Important:** Only one BDC model file can be included per add-in.</span></span> <span data-ttu-id="4ac73-160">При BDCMetadata.bdcm имя файла в этом примере файл модели фактически может быть любое имя, выбранное при условии, что соответствует имени файла, который является в атрибуте **путь** к файлу модели BDC.</span><span class="sxs-lookup"><span data-stu-id="4ac73-160">While the file name in this example is BDCMetadata.bdcm, the model file can actually be any name you choose as long as the file name matches that is in the **Path** attribute of the BDC model file.</span></span>
  
    
    


> <span data-ttu-id="4ac73-161">**Примечание:** Только Open Data protocol (OData) подключений для добавления в пределах внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="4ac73-161">**Note:** Only Open Data protocol (OData) connections are allowed for add-in-scoped external content types.</span></span> 
  
    
    


### <a name="set-security-credentials-for-an-external-system"></a><span data-ttu-id="4ac73-162">Задать учетные данные безопасности для внешней системы</span><span class="sxs-lookup"><span data-stu-id="4ac73-162">Set security credentials for an external system</span></span>
<span data-ttu-id="4ac73-163"><a name="Appscopedect_deployect"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-163"></span></span>

<span data-ttu-id="4ac73-164">Чтобы получить доступ к данным на защищенном внешней системы, необходимо настроить модели BDC с соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="4ac73-164">In order to access data on a secured external system, you must configure the BDC model with the appropriate credentials.</span></span>
  
    
    
<span data-ttu-id="4ac73-165">Следующем примере показано, как задать учетные данные безопасности для внешней системы в добавить в пределах внешних типов контента, внести изменения в файл Elements.xml приложения.</span><span class="sxs-lookup"><span data-stu-id="4ac73-165">The following example shows how to set security credentials for an external system in add-in-scoped external content types by modifying the Elements.xml file of the app.</span></span>
  
    
    



```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
    <LobSystem Name="SAP">
       <LobSystemInstance Name="SAPInst" RequireCredentials="true" CredentialsDescription="Credentials to connect to SAP"/>
    </LobSystem>
    <LobSystem Name="SQL">
       <LobSystemInstance Name="App Database" DataSource="SQL-Azure" RequireCredentials="true" />
    </LobSystem>
  </BdcModel>
</Elements>

```


## <a name="in-this-section"></a><span data-ttu-id="4ac73-166">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="4ac73-166">In this section</span></span>
<span data-ttu-id="4ac73-167"><a name="Appscopedect_inthissection"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-167"></span></span>


-  [<span data-ttu-id="4ac73-168">Как: создание добавить в пределах внешнего типа контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-168">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4ac73-169">Доступ ко внешним данным с помощью REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-169">How to: Access external data with REST in SharePoint</span></span>](how-to-access-external-data-with-rest-in-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="4ac73-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4ac73-170">Additional resources</span></span>
<span data-ttu-id="4ac73-171"><a name="Appscopedect_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="4ac73-171"></span></span>


-  [<span data-ttu-id="4ac73-172">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-172">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4ac73-173">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-173">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="4ac73-174">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-174">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="4ac73-175">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-175">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4ac73-176">Внешние события и оповещения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-176">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4ac73-177">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-177">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4ac73-178">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4ac73-178">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

