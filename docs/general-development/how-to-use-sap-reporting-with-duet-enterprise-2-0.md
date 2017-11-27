---
title: "Использование отчетов SAP с Duet Enterprise 2.0 (en)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a54c6cd2-2283-440d-af55-e98e3212caa1
ms.openlocfilehash: 089a22b0f96c4dd2cb5d4a7ad1808b4307986fb2
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="use-sap-reporting-with-duet-enterprise-20"></a><span data-ttu-id="3317d-102">Использование отчетов SAP с Duet Enterprise 2.0 (en)</span><span class="sxs-lookup"><span data-stu-id="3317d-102">Use SAP Reporting with Duet Enterprise 2.0</span></span>

## <a name="introduction"></a><span data-ttu-id="3317d-103">Введение</span><span class="sxs-lookup"><span data-stu-id="3317d-103">Introduction</span></span>
<span data-ttu-id="3317d-104"><a name="bkmk_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="3317d-104"><a name="bkmk_Introduction"> </a></span></span>

<span data-ttu-id="3317d-105">Duet Enterprise 2.0 предоставляет возможность интеграции компонентов отчетов Duet в рамках вашей Надстройка SharePoint, выполнив несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="3317d-105">Duet Enterprise 2.0 gives you the ability to integrate the Duet reporting features within your SharePoint Add-in by doing a little customization.</span></span>
  
    
    
<span data-ttu-id="3317d-p101">С помощью скрытый элемент, установленных с Duet  секрет для включения отчетов для вашего приложения. Необходимо будет сшивания эту функцию для настраиваемых компонентов, чтобы при создании приложения компонентов отчетов SAP будут доступны для приложения.</span><span class="sxs-lookup"><span data-stu-id="3317d-p101">The secret to enabling reporting for your app is by using a hidden feature installed by Duet. You will need to staple this feature to custom features, so that when the app is instantiated, the SAP reporting features will be made available to the app.</span></span>
  
    
    

## <a name="enabling-the-features"></a><span data-ttu-id="3317d-108">Включение компонентов</span><span class="sxs-lookup"><span data-stu-id="3317d-108">Enabling the features</span></span>
<span data-ttu-id="3317d-109"><a name="bkmk_EnablingTheFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="3317d-109"><a name="bkmk_EnablingTheFeatures"> </a></span></span>

<span data-ttu-id="3317d-110">Чтобы включить компоненты отчетов Duet, последовательность активации необходимо тщательно следовать.</span><span class="sxs-lookup"><span data-stu-id="3317d-110">To enable the Duet reporting features, the sequence of activation must be carefully followed.</span></span>
  
    
    

### <a name="to-create-a-feature-to-add-the-app-scoped-external-content-type"></a><span data-ttu-id="3317d-111">Чтобы создать компонент для добавления области приложения внешнего типа контента:</span><span class="sxs-lookup"><span data-stu-id="3317d-111">To create a feature to add the app-scoped external content type:</span></span>


1. <span data-ttu-id="3317d-p102">Внутри вашей Duet отчетов приложения в **Обозревателе решений** щелкните правой кнопкой мыши имя проекта. Нажмите кнопку **Добавить**, **типов контента для внешнего источника данных**. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3317d-p102">Inside your Duet reporting app, in the **Solution Explorer**, right click the project name. Choose **Add**, **Content Types for an External Data Source**. Click **Next**.</span></span>
    
  
2. <span data-ttu-id="3317d-115">Введите URL-адрес конечной точки отчетов SAP как источника OData.</span><span class="sxs-lookup"><span data-stu-id="3317d-115">Enter the URL for the SAP Reporting endpoint as the OData Source.</span></span>
    
  
3. <span data-ttu-id="3317d-116">Выберите сущности и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3317d-116">Select the Entities, and choose **Finish**.</span></span>
    
  
4. <span data-ttu-id="3317d-p103">Откройте созданный внешний тип контента для просмотра свойств LSI. Обратите внимание, что они совпадают с требованиями для уровня фермы внешнего типа контента за исключением **ODataconnectionSettingsId**.</span><span class="sxs-lookup"><span data-stu-id="3317d-p103">Open the newly created external content type to view the LSI properties. You will notice that they are the same as for the farm-scoped external content type except for the **ODataconnectionSettingsId**.</span></span>
    
  

### <a name="to-create-a-feature-to-enable-the-hidden-duet-features"></a><span data-ttu-id="3317d-119">Чтобы создать компонент можно включить скрытые компоненты Duet:</span><span class="sxs-lookup"><span data-stu-id="3317d-119">To create a feature to enable the hidden Duet features:</span></span>


1. <span data-ttu-id="3317d-p104">Добавьте другой новой функцией в проект. Имя заголовка **AddDuetReporting**.</span><span class="sxs-lookup"><span data-stu-id="3317d-p104">Add another new feature to your project. Name the title **AddDuetReporting**.</span></span>
    
    <span data-ttu-id="3317d-122">Эта функция будет, зависят от функции **DuetReportingForApps** и **AddReportingModel**.</span><span class="sxs-lookup"><span data-stu-id="3317d-122">This feature will have a dependency on the **AddReportingModel** and the **DuetReportingForApps** features.</span></span>
    
  
2. <span data-ttu-id="3317d-123">Добавьте следующий код в файл **элементы**.</span><span class="sxs-lookup"><span data-stu-id="3317d-123">Add the following code to the **Elements** file.</span></span>
    
```
  
<?xml version="1.0" encoding="utf-8"?>
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="AddDuetReporting" Id="6a55705c-af12-455a-914b-8cf3a31c820e" Scope="Web">
  <ActivationDependencies>
    <ActivationDependency FeatureId="e1fe41d3-7fc3-458f-9a66-6ecf6a39bb2c" FeatureTitle="AddReportingModel" />
    <ActivationDependency FeatureId="9b60ccba-ebfd-4e38-87c8-3dea9cc2680a" FeatureTitle="SAPReportingForApps" />
  </ActivationDependencies>
</Feature>

```

<span data-ttu-id="3317d-p105">Обратите внимание, что последовательность операций в зависимостей активации важна. Во-первых необходимо создать внешний тип контента и затем активируйте компонент **SAPReportingForApps**. Кроме того, обратите внимание, что второй компонент (ID: **9b60ccba-ebfd-4e38-87c8-3dea9cc2680a**) поставляется вместе с Duet Enterprise 2.0, но оно будет помечено как скрытый. При использовании этого подхода можно сделать разработчик использование этой функции и можно свести в возможности отчетов Duet для приложения.</span><span class="sxs-lookup"><span data-stu-id="3317d-p105">Please note that the sequence in activation dependency is important. First, you must create the external content type and then activate the **SAPReportingForApps** feature. Also, note that the second feature (ID: **9b60ccba-ebfd-4e38-87c8-3dea9cc2680a**) is shipped with Duet Enterprise 2.0, but it is marked as hidden. With this approach, a developer can make use of this feature and can bring in Duet Reporting capabilities to an app.</span></span>
  
    
    
<span data-ttu-id="3317d-p106">После активации компонента **DuetReportingForApps** в этот выпуск все артефакты (список отчетов, Lib, формы, и т.д.) и настройки на сайте приложения, но как шаблон сайта приложения не имеет стандартный навигационных ссылок, разработчик приложения должен добавлять элементы пользовательскую страницу для переноса в работе компонентов Duet (например параметры отчета, представление списка библиотеки и форм). Разработчик должен документации стандартных Duet для функции отчетности для получения дополнительных сведений о части компонента и его элементы пользовательского интерфейса. Разработчик может выбрать для создания настраиваемого пользовательского интерфейса для функции точки входа которых для удовлетворения лучше с общей темой приложения.</span><span class="sxs-lookup"><span data-stu-id="3317d-p106">Once the **DuetReportingForApps** feature is activated, it will bring all the artifacts (Report List, Lib, forms, etc.) and customization on the apps site but as the app site template does not have standard navigation links, the app developer needs to add custom page elements to bring out the Duet features (e.g. Report Settings, library list view, and forms). The developer should consult standard Duet documentation for Reporting feature to learn more about the feature and its UI elements. A developer may choose to build up a custom UI for feature entry points which may suit better with the general theme of the app.</span></span>
  
    
    

## <a name="viewing-the-results"></a><span data-ttu-id="3317d-131">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="3317d-131">Viewing the results</span></span>
<span data-ttu-id="3317d-132"><a name="bkmk_ViewingTheResults"> </a></span><span class="sxs-lookup"><span data-stu-id="3317d-132"><a name="bkmk_ViewingTheResults"> </a></span></span>

<span data-ttu-id="3317d-133">Чтобы просмотреть страницу Параметры отчета по умолчанию, перейдите к: **~/Lists/ReportSetting/AllReportTemplate.aspx**.</span><span class="sxs-lookup"><span data-stu-id="3317d-133">To see the default report settings page, navigate to: **~/Lists/ReportSetting/AllReportTemplate.aspx**.</span></span>
  
    
    
<span data-ttu-id="3317d-134">Чтобы просмотреть представление по умолчанию для библиотеки документов, отчетов, перейдите к: **~/ReportsLib/Forms/AllItems.aspx**.</span><span class="sxs-lookup"><span data-stu-id="3317d-134">To see the default view for the report document library, navigate to: **~/ReportsLib/Forms/AllItems.aspx**.</span></span>
  
    
    

## <a name="customizing-the-reports"></a><span data-ttu-id="3317d-135">Настройка отчетов</span><span class="sxs-lookup"><span data-stu-id="3317d-135">Customizing the reports</span></span>
<span data-ttu-id="3317d-136"><a name="bkmk_CustomizingTheReports"> </a></span><span class="sxs-lookup"><span data-stu-id="3317d-136"><a name="bkmk_CustomizingTheReports"> </a></span></span>

<span data-ttu-id="3317d-p107">Внутри приложения разработчик можно создать свой собственный пользовательский Интерфейс (с использованием HTML/JavaScript/Jquery и т.д.) и создать более широких возможностей пользователя с помощью BCS CSOM. После снимки экрана показано аналогичные приложения, где настраиваемых HTML-код на основе пользовательского интерфейса создается с помощью готовые артефакты и интерфейсы API BCS на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="3317d-p107">Inside an app, a developer can also create his own custom UI (using HTML/JavaScript/Jquery etc.) and make use of BCS CSOM to build a richer user experience. Following screenshots shows a similar app where custom HTML based UI is built with the help of OOB artifacts and client side BCS APIs.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="3317d-139">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3317d-139">Additional resources</span></span>
<span data-ttu-id="3317d-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3317d-140"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="3317d-141">Разработка с помощью Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="3317d-141">Developing with Duet Enterprise 2.0</span></span>](developing-with-duet-enterprise-2-0.md)
    
  
-  [<span data-ttu-id="3317d-142">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3317d-142">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3317d-143">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3317d-143">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

