---
title: "Новые возможности для разработчиков в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 068d0b99-1762-42de-b6c9-acb1cffc6e31
ms.openlocfilehash: 07e78edc42f4c9277047950a3a8554917a1f4e91
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-for-developers-in-sharepoint"></a>Новые возможности для разработчиков в SharePoint
В этой статье описываются новые возможности и функции SharePoint, в том числе новая модель облачных надстроек, средства разработки, улучшения платформы, мобильные надстройки и многое другое.
## <a name="cloud-add-in-model"></a>Модель облачных надстроек
<a name="bmSpApps"> </a>

В SharePoint реализована модель облачных надстроек, которая позволяет создавать надстройки. Надстройки SharePoint — это автономные инструменты, расширяющие возможности веб-сайта SharePoint. Надстройка может включать такие компоненты SharePoint, как списки, рабочие процессы и страницы сайтов, но она также может предоставлять доступ к удаленному веб-приложению и удаленным данным в SharePoint. Надстройка не зависит или почти не зависит от другого программного обеспечения на устройстве или платформе, где она установлена, кроме встроенного программного обеспечения платформы. Это обеспечивает простую установку и бесследное удаление. У надстроек нет пользовательского кода, выполняемого на серверах SharePoint. Пользовательский код передается между облаком и клиентскими компьютерами. Кроме того, в SharePoint реализована инновационная модель доставки надстроек, которая включает Магазин Office и Каталог надстроек.

<a href="../sp-add-ins/sharepoint-add-ins.md"><img alt="SharePoint Add-ins" src="../images/wn_cloud_1.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md"><img alt="SharePoint Store" src="../images/wn_cloud_2.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md"><img alt="Add-ins Catalog" src="../images/wn_cloud_3.png" /></a>

## <a name="familiar-programming-model-using-web-standards"></a>Знакомая модель программирования с использованием веб-стандартов
<a name="bmWebStandards"> </a>

С помощью SharePoint любые веб-разработчики, включая тех, что работают с платформами других компаний (не Майкрософт), могут легко создавать решения для SharePoint. Это стало возможным благодаря тому, что SharePoint основан на общепринятых веб-стандартах, таких как HTML, CSS и JavaScript. Кроме того, реализация зависит от распространенных протоколов, таких как OData и OAuth.
  

  <a href="../sp-add-ins/sharepoint-add-ins.md"><img alt="HTML/JavaScript" src="../images/wn_WebStandards_1.png" /></a>&nbsp;&nbsp;<a href="using-odata-sources-with-business-connectivity-services-in-sharepoint.md"><img alt="OData" src="../images/wn_WebStandards_2.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/get-to-know-the-sharepoint-rest-service.md" target="_blank"><img alt="REST" src="../images/wn_WebStandards_3.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/authorization-and-authentication-of-sharepoint-add-ins.md"><img alt="OAuth" src="../images/wn_WebStandards_4.png" /></a>


## <a name="development-tools"></a>Средства разработки
<a name="bmDevTools"> </a>

Текущий выпуск отражает огромные успехи в оптимизации существующих инструментов разработки, таких как Visual Studio и SharePoint Designer, а также предоставляет новое средство Средства разработки Napa для Office 365 для разработки надстроек. Новая унифицированная система проектов в Visual Studio позволяет создавать Надстройки SharePoint, Надстройки Office и Надстройки SharePoint, в том числе Надстройки Office и Надстройки Office, размещенные в SharePoint. Помимо шаблонов проекта SharePoint, которые были доступны в предыдущих версиях, Visual Studio 2012 теперь содержит новый шаблон проекта надстройки в папке "Надстройки", Надстройки для SharePoint. Несколько новых свойств добавлены в окно свойств и на страницу свойств для поддержки проектов Надстройка SharePoint. В числе других улучшений полная поддержка разработки на основе модели облачных надстроек, включая поддержку OData и OAuth, и полную поддержку разработки для платформы Workflow Manager Client 1.0.

<a href="https://dev.office.com/docs/add-ins/overview/office-add-ins" target="_blank"><img alt="Napa Office 365 Development Tools" src="../images/wn_DevTools_1.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/what-s-new-in-office-developer-tools-for-visual-studio.md"><img alt="Visual Studio" src="../images/wn_DevTools_2.png" /></a>&nbsp;&nbsp;<a href="workflow-development-in-sharepoint-designer-and-visio.md"><img alt="SharePoint Designer" src="../images/wn_DevTools_3.png" /></a>

## <a name="core-platform-enhancements"></a>Основные улучшения платформы
<a name="bmPlatformEnhance"> </a>

В более общем смысле продукт SharePoint был усовершенствован для поддержки новой облачной архитектуры и платформы разработки на основе приложений. Во всем, начиная API-интерфейсами SharePoint на самом низком уровне и заканчивая интеграцией с социальными сетями, SharePoint разработан для поддержки среды разработки расширенных приложений. Помимо использования конечных точек REST для веб-служб, существует новый интерфейс API для разработки клиентских и серверных решений. Теперь, в дополнение к обработке на стороне клиента, поддерживаются и удаленные приемники событий. 
  
<a href="https://msdn.microsoft.com/library/fp161347.aspx" target="_blank"><img alt="REST endpoints" src="../images/wn_Platform_1.png" /></a>&nbsp;&nbsp;<a href="choose-the-right-api-set-in-sharepoint.md"><img alt="New client and server APIs" src="../images/wn_Platform_2.png" /></a>&nbsp;&nbsp;<a href="how-to-customize-a-field-type-using-client-side-rendering.md"><img alt="Client-side rendering" src="../images/wn_Platform_3.png" /></a>&nbsp;&nbsp;<a href="../sp-add-ins/handle-events-in-sharepoint-add-ins.md"><img alt="Remote event receivers" src="../images/wn_Platform_4.png" /></a>

    
    
    

## <a name="mobility"></a>Мобильность
<a name="bmMobility"> </a>

С помощью SharePoint вы можете объединить приложения Windows Phone 7 с локальными или работающими в облаке удаленными службами и приложениями SharePoint (например, использующими SharePoint Online), для создания мощных и действительно портативных приложений, которые работают не только на традиционных настольных компьютерах и ноутбуках, но и на мобильных устройствах. Новые возможности для мобильных приложений в SharePoint основаны на существующих средствах и технологиях Майкрософт, такие как SharePoint, Windows Phone 7, Visual Studio и Microsoft Silverlight. Можно разрабатывать мобильные приложения на основе SharePoint для Windows Phone, используя новый шаблон мастера приложения SharePoint дл телефонов в Visual Studio. С его помощью можно создавать простые мобильные приложения на основе списков. Кроме того, вы можете интегрировать новые возможности, представленные в SharePoint, такие как тип поля географического расположения и push-уведомления от SharePoint Server, в своих мобильных приложениях.

<a href="overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md"><img alt="Visual Studio app templates" src="../images/wn_Mobility_.png" /></a>&nbsp;&nbsp;<a href="how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md"><img alt="Push notifications" src="../images/wn_Mobility_2.png" /></a>&nbsp;&nbsp;<a href="integrating-location-and-map-functionality-in-sharepoint.md"><img alt="Location and maps" src="../images/wn_Mobility_3.png" /></a>

## <a name="social-and-collaboration"></a>Социальные сети и совместная работа
<a name="bmSocial"> </a>

Новые и улучшенные возможности для взаимодействия с социальными сетями и совместной работы позволяют пользователям легко обмениваться данными и всегда оставаться в курсе событий. Улучшенные социальные веб-каналы Личный сайт помогают следить за интересующими людьми и контентом в социальных сетях. Новый сайт сообщества предоставляет расширенный интерфейс сообщества, позволяя пользователям легко находить информацию и обмениваться ей, а также находить людей с похожими интересами.

<a href="work-with-social-feeds-in-sharepoint.md"><img alt="Interactive feed" src="../images/wn_Social_1.png" /></a>&nbsp;&nbsp;<a href="what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab"><img alt="Community site" src="../images/wn_Social_2.png" /></a>&nbsp;&nbsp;<a href="follow-people-in-sharepoint.md"><img alt="Follow people" src="../images/wn_Social_3.png" /></a>&nbsp;&nbsp;<a href="follow-content-in-sharepoint.md"><img alt="Follow sites" src="../images/wn_Social_4.png" /></a>

## <a name="search"></a>Поиск
<a name="bmSearch"> </a>

Система поиска в SharePoint получила ряд усовершенствований, в том числе обработка пользовательского контента с помощью веб-службы повышения качества контента, а также новая платформа представления типов результатов поиска. Кроме того, были внесены значительные улучшения в язык KQL.

<a href="custom-content-processing-with-the-content-enrichment-web-service-callout.md"><img alt="Consolidated search platform" src="../images/wn_search_1.png" /></a>&nbsp;&nbsp;<a href="what-s-new-in-sharepoint-search-for-developers.md"><img alt="Rich results framework" src="../images/wn_search_2.png" /></a>&nbsp;&nbsp;<a href="building-search-queries-in-sharepoint.md"><img alt="KQL enhnacements" src="../images/wn_search_3.png" /></a>

## <a name="workflows"></a>Рабочие процессы
<a name="bmWorkflow"> </a>

Workflow Manager Client 1.0  это переработанная инфраструктура рабочих процессов, созданная на основе Windows Workflow Foundation 4. Она предоставляет новые, мощные и гибкие возможности разработки рабочих процессов в SharePoint. Полностью декларативная среда разработки позволяет информационным сотрудникам использовать SharePoint Designer 2013 для создания функциональных рабочих процессов, а новый набор шаблонов проекта рабочего процесса Visual Studio 2012 предоставляет разработчикам доступ к расширенным функциям, таким как настраиваемые действия. Возможно, самое главное преимущество состоит в том, что Workflow Manager Client 1.0 полностью интегрирован с Модель для надстроек SharePoint. Кроме того, рабочие процессы выполняются в облаке, а не в SharePoint, что обеспечивает невероятную гибкость при проектировании Надстройки SharePoint на основе рабочих процессов.

<a href="what-s-new-in-workflows-for-sharepoint.md"><img alt="Execute in the cloud" src="../images/wn_workflow_1.png" /></a>&nbsp;&nbsp;<a href="sharepoint-workflow-fundamentals.md"><img alt="Workflow 4-based infrastructure" src="../images/wn_workflow_2.png" /></a>&nbsp;&nbsp;<a href="workflow-development-in-sharepoint-designer-and-visio.md"><img alt="Declarative authoring" src="../images/wn_workflow_3.png" /></a>&nbsp;&nbsp;<a href="develop-sharepoint-workflows-using-visual-studio.md"><img alt="Designer and project templates" src="../images/wn_workflow_4.png" /></a>

## <a name="enterprise-content-management"></a>Управление корпоративным информационным содержимым
<a name="bmECM"> </a>

В SharePoint вы можете использовать API-интерфейсы клиента.NET, Silverlight, Windows Phone и JavaScript, а также недавно расширенный набор серверных управляемых интерфейсов API .NET, для настройки интерфейсов поведения корпоративного управления информационным содержимым (ECM).

<a href="what-s-new-with-sharepoint-site-development.md"><img alt="Design Manager" src="../images/wn_ecm_1.png" /></a>&nbsp;&nbsp;<a href="managed-navigation-in-sharepoint.md"><img alt="Managed navigation" src="../images/wn_ecm_2.png" /></a>&nbsp;&nbsp;<a href="cross-site-publishing-in-sharepoint.md"><img alt="Cross-site publishing" src="../images/wn_ecm_3.png" /></a>&nbsp;&nbsp;<a href="ediscovery-in-sharepoint.md"><img alt="EDiscovery" src="../images/wn_ecm_4.png" /></a>

## <a name="business-connectivity-services"></a>Business Connectivity Services
<a name="bmBCS"> </a>

Службы Business Connectivity Services (BCS) предоставляет SharePoint доступ к данным из внешних систем, таких как SAP, ERP и CRM, в дополнение к другим приложениям на основе данных, которые доступны через службы WCF или конечные точки OData. Службы BCS в SharePoint были усовершенствованы и расширены. Среди улучшений подключения OData, внешние события, внешние данные в надстройках, фильтрация и сортировка, поддержка REST и другое.

<a href="using-odata-sources-with-business-connectivity-services-in-sharepoint.md"><img alt="OData connector" src="../images/wn_bcs_1.png" /></a>&nbsp;&nbsp;<a href="add-in-scoped-external-content-types-in-sharepoint.md"><img alt="External data in apps" src="../images/wn_bcs_2.png" /></a>&nbsp;&nbsp;<a href="external-events-and-alerts-in-sharepoint.md"><img alt="External events in SharePoint" src="../images/wn_bcs_3.png" /></a>

## <a name="application-services"></a>Службы-приложения
<a name="bmSpServices"> </a>

SharePoint включает несколько служб для работы с данными на сайтах. В SharePoint появилась служба машинного перевода, которая переводит сайты, документы и потоки. SharePoint также включает службы Access и новую модель доступа к данным. Для преобразования файлов и потоков в другие форматы в SharePoint есть службы Word Automation Services и PowerPoint Automation Services (новая возможность). В SharePoint также предусмотрены инструменты для анализа данных, такие как PerformancePoint Services и службы Visio, и полезные новые функции в службах Excel.

<a href="external-events-and-alerts-in-sharepoint.md"><img alt="Translation Services" src="../images/wn_appServices_1.png" /></a>&nbsp;&nbsp;<a href="powerpoint-automation-services-in-sharepoint.md"><img alt="PowerPoint Automation Services" src="../images/wn_appServices_2.png" /></a>&nbsp;&nbsp;<a href="what-s-new-in-access.md"><img alt="Enhanced Access Services" src="../images/wn_appServices_3.png" /></a>&nbsp;&nbsp;<a href="https://msdn.microsoft.com/library/fp161347.aspx" target="_blank"><img alt="Enhanced Excel Services" src="../images/wn_appServices_4.png" /></a>


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bm_Addres"> </a>


-  [Обзор разработки решений с помощью SharePoint](sharepoint-development-overview.md)
    
  
-  [Разработка надстроек для SharePoint](../sp-add-ins/sharepoint-add-ins.md)
    
  
-  [Сравнение надстроек SharePoint с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [Специальные возможности в SharePoint](accessibility-in-sharepoint.md)
    
  

