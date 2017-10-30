---
title: "Как создать внешний список с помощью источника данных OData в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 601fbfce-a0c6-43dd-8398-540d094c083c
ms.openlocfilehash: c0fe48ca9061d22f5aade9b3afbf15ba306f0ae0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint"></a><span data-ttu-id="3729c-102">Как: Создание внешнего списка с помощью источника данных OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-102">How to: Create an external list using an OData data source in SharePoint</span></span>
<span data-ttu-id="3729c-103">Узнайте, как программно создать внешний список и привязать его к внешнему типу контента на основе OData в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3729c-103">Learn how to create an external list programmatically and bind it to an OData-based external content type in SharePoint.</span></span>
<span data-ttu-id="3729c-104">Несмотря на то, что опытный пользователь или администратор SharePoint скорее всего будет создать внешний список с помощью SharePoint Designer 2013, разработчик будет интересовать возможность создания внешних списков с помощью средств их торговые разработчика Office и Visual Studio 2012 Средства Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="3729c-104">Although a power user or SharePoint administrator will likely create an external list using SharePoint Designer 2013, a developer will be interested in the ability to create external lists using the tools of their trade, Visual Studio 2012 and the Office Developer Tools for Visual Studio 2012.</span></span> <span data-ttu-id="3729c-105">Это обеспечивает большую гибкость для добавления функций и Упакуйте решение, которое включает функции Business Connectivity Services (BCS) для последующего развертывания в одну или многие размещения сред.</span><span class="sxs-lookup"><span data-stu-id="3729c-105">This gives them more flexibility to add functionality and to package a solution that includes Business Connectivity Services (BCS) features for later deployment into one or many host environments.</span></span>
  
    
    


## <a name="prerequisites-for-creating-an-external-list"></a><span data-ttu-id="3729c-106">Необходимые условия для создания внешнего списка</span><span class="sxs-lookup"><span data-stu-id="3729c-106">Prerequisites for creating an external list</span></span>
<span data-ttu-id="3729c-107"><a name="bkmk_Prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="3729c-107"></span></span>

<span data-ttu-id="3729c-108">Создание внешнего списка из источника OData необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="3729c-108">The following components are needed to create an external list from an OData source:</span></span>
  
    
    

- <span data-ttu-id="3729c-109">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3729c-109">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="3729c-110">SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-110">SharePoint</span></span>
    
  
- <span data-ttu-id="3729c-111">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="3729c-111">Office Developer Tools for Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="3729c-112">A опубликовано внешнего типа контента на основе источника OData: сведения содержатся в разделе [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3729c-112">A published external content type based on an OData source: For instructions, see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
    
  
<span data-ttu-id="3729c-113">Сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3729c-113">For information about setting up a SharePoint development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="core-concepts-for-creating-external-lists"></a><span data-ttu-id="3729c-114">Основные понятия, которые для создания внешних списков</span><span class="sxs-lookup"><span data-stu-id="3729c-114">Core concepts for creating external lists</span></span>

<span data-ttu-id="3729c-115">В следующих статьях представлены сведения о Надстройки SharePoint и прочие сведения для создания внешних списков.</span><span class="sxs-lookup"><span data-stu-id="3729c-115">The following articles provide information about SharePoint Add-ins and other background information for creating external lists.</span></span>
  
    
    

<span data-ttu-id="3729c-116">**В таблице 1. Основные понятия, которые для внешних списков**</span><span class="sxs-lookup"><span data-stu-id="3729c-116">**Table 1. Core concepts for external lists**</span></span>


|<span data-ttu-id="3729c-117">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="3729c-117">**Article title**</span></span>|<span data-ttu-id="3729c-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3729c-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="3729c-119">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-119">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="3729c-120">Сведения о службах Business Connectivity Services и того, как предоставлять внешних данных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3729c-120">Learn about Business Connectivity Services and how you can expose external data in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="3729c-121">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-121">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |<span data-ttu-id="3729c-122">Узнайте о новой модели приложения в SharePoint, которое позволяет создавать приложения, представляющие собой небольшие, простые в использовании решения для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="3729c-122">Learn about the new app model in SharePoint that enables you to create apps, which are small, easy-to-use solutions for end users.</span></span>  <br/> |
| [<span data-ttu-id="3729c-123">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-123">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx) <br/> |<span data-ttu-id="3729c-124">Информация о различных способах размещения Надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3729c-124">Learn about the different ways that you can host SharePoint Add-ins.</span></span>  <br/> |
   

## <a name="create-a-new-external-list"></a><span data-ttu-id="3729c-125">Создание нового внешнего списка</span><span class="sxs-lookup"><span data-stu-id="3729c-125">Create a new external list</span></span>
<span data-ttu-id="3729c-126"><a name="bkmk_CreateNewVList"> </a></span><span class="sxs-lookup"><span data-stu-id="3729c-126"></span></span>

<span data-ttu-id="3729c-127">Ниже показано, как создать новый внешний список, привязки на основе внешнего типа контента и публикация в SharePoint с помощью Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="3729c-127">The following procedures will show you how to create a new external list, bind it to OData-based external content type, and publish to SharePoint using Visual Studio 2012.</span></span>
  
    
    

> <span data-ttu-id="3729c-128">**Примечание:** Первый шаг предполагается, что вы создали внешнего типа контента, как описано в статье [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3729c-128">**Note:** The first step assumes that you have successfully created an external content type, as described in  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span> 
  
    
    


### <a name="to-add-an-external-list-automatically"></a><span data-ttu-id="3729c-129">Чтобы автоматически добавлять внешнего списка</span><span class="sxs-lookup"><span data-stu-id="3729c-129">To add an external list automatically</span></span>


1. <span data-ttu-id="3729c-p102">Если требуется добавить простой список в проект, который отражает в внешний тип контента, можно использовать средства Автоматическое формирование Visual Studio 2012. Список создается при создании внешнего типа контента. При установите флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**, обнаруженных в второй этап процесса автоматическое формирование (Выбор шаг сущности данных), мастер создает XML-объявления и добавлять новые внешние типы контента для каждого элемента, который вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="3729c-p102">If you just want to add a simple list to your project that reflects what is in your external content type, you can use the Visual Studio 2012 autogeneration tools. The list is created when the external content type is created. When you select the **Create list instances for the selected data entities (except Service Operations)** check box found in the second step of the autogeneration process (Select the Data Entities step), the wizard creates the XML declarations and add new external content types for each entity you selected.</span></span>
    
  
2. <span data-ttu-id="3729c-133">Нажмите клавишу F5, чтобы развернуть проект и новый список также развернуть.</span><span class="sxs-lookup"><span data-stu-id="3729c-133">Press F5 to deploy the project, and the new list is also deployed.</span></span>
    
  
<span data-ttu-id="3729c-134">В целях тестирования, может потребоваться изменить файл AppManifest.xml таким образом, чтобы начальная страница приложения  это список, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="3729c-134">For testing purposes, you may want to modify the AppManifest.xml file so that the starting page of the app is the list you just created.</span></span> 
  
    
    

### <a name="to-modify-the-appmanifestxml-file"></a><span data-ttu-id="3729c-135">Изменение файла AppManifest.xml</span><span class="sxs-lookup"><span data-stu-id="3729c-135">To modify the AppManifest.xml file</span></span>


1. <span data-ttu-id="3729c-136">Откройте файл AppManifest.xml, с помощью XML-редактора.</span><span class="sxs-lookup"><span data-stu-id="3729c-136">Open the AppManifest.xml file using an XML editor.</span></span>
    
  
2. <span data-ttu-id="3729c-137">Найдите \<StartPage\> тег.</span><span class="sxs-lookup"><span data-stu-id="3729c-137">Find the \<StartPage\> tag.</span></span>
    
  
3. <span data-ttu-id="3729c-138">Измените значение на  `~appWebUrl/Lists/Employees`.</span><span class="sxs-lookup"><span data-stu-id="3729c-138">Change the value to  `~appWebUrl/Lists/Employees`.</span></span>
    
  
4. <span data-ttu-id="3729c-139">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="3729c-139">Save your changes.</span></span>
    
  

### <a name="to-publish-the-project"></a><span data-ttu-id="3729c-140">Публикация проекта</span><span class="sxs-lookup"><span data-stu-id="3729c-140">To publish the project</span></span>


- <span data-ttu-id="3729c-141">Нажмите клавишу F5, чтобы развернуть проект и внешнего списка.</span><span class="sxs-lookup"><span data-stu-id="3729c-141">Press F5 to deploy your project and external list.</span></span> 
    
    <span data-ttu-id="3729c-142">Откройте веб-браузер и перейдите в созданный новый список.</span><span class="sxs-lookup"><span data-stu-id="3729c-142">Open a web browser, and navigate to the new list you created.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="3729c-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3729c-143">Additional resources</span></span>
<span data-ttu-id="3729c-144"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3729c-144"></span></span>


-  [<span data-ttu-id="3729c-145">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-145">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3729c-146">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-146">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3729c-147">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-147">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3729c-148">Инструкции. Создание базового приложения с автоматическим размещением для SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-148">How to: Create a basic autohosted app for SharePoint</span></span>](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="3729c-149">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3729c-149">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

