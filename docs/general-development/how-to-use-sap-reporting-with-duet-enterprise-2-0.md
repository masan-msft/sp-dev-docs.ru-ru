---
title: "Способ использование отчетов SAP с Duet Enterprise 2.0 (en)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a54c6cd2-2283-440d-af55-e98e3212caa1
ms.openlocfilehash: 0d4e3b0f8ec5d3c54a52017b75768d8bbf6ac748
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-sap-reporting-with-duet-enterprise-20"></a>Способ: использование отчетов SAP с Duet Enterprise 2.0 (en)

## <a name="introduction"></a>Введение
<a name="bkmk_Introduction"> </a>

Duet Enterprise 2.0 предоставляет возможность интеграции компонентов отчетов Duet в рамках вашей Надстройка SharePoint, выполнив несколько параметров.
  
    
    
С помощью скрытый элемент, установленных с Duet  секрет для включения отчетов для вашего приложения. Необходимо будет сшивания эту функцию для настраиваемых компонентов, чтобы при создании приложения компонентов отчетов SAP будут доступны для приложения.
  
    
    

## <a name="enabling-the-features"></a>Включение компонентов
<a name="bkmk_EnablingTheFeatures"> </a>

Чтобы включить компоненты отчетов Duet, последовательность активации необходимо тщательно следовать.
  
    
    

### <a name="to-create-a-feature-to-add-the-app-scoped-external-content-type"></a>Чтобы создать компонент для добавления области приложения внешнего типа контента:


1. Внутри вашей Duet отчетов приложения в **Обозревателе решений** щелкните правой кнопкой мыши имя проекта. Нажмите кнопку **Добавить**, **типов контента для внешнего источника данных**. Нажмите кнопку **Далее**.
    
  
2. Введите URL-адрес конечной точки отчетов SAP как источника OData.
    
  
3. Выберите сущности и нажмите кнопку **Готово**.
    
  
4. Откройте созданный внешний тип контента для просмотра свойств LSI. Обратите внимание, что они совпадают с требованиями для уровня фермы внешнего типа контента за исключением **ODataconnectionSettingsId**.
    
  

### <a name="to-create-a-feature-to-enable-the-hidden-duet-features"></a>Чтобы создать компонент можно включить скрытые компоненты Duet:


1. Добавьте другой новой функцией в проект. Имя заголовка **AddDuetReporting**.
    
    Эта функция будет, зависят от функции **DuetReportingForApps** и **AddReportingModel**.
    
  
2. Добавьте следующий код в файл **элементы**.
    
```
  
<?xml version="1.0" encoding="utf-8"?>
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="AddDuetReporting" Id="6a55705c-af12-455a-914b-8cf3a31c820e" Scope="Web">
  <ActivationDependencies>
    <ActivationDependency FeatureId="e1fe41d3-7fc3-458f-9a66-6ecf6a39bb2c" FeatureTitle="AddReportingModel" />
    <ActivationDependency FeatureId="9b60ccba-ebfd-4e38-87c8-3dea9cc2680a" FeatureTitle="SAPReportingForApps" />
  </ActivationDependencies>
</Feature>

```

Обратите внимание, что последовательность операций в зависимостей активации важна. Во-первых необходимо создать внешний тип контента и затем активируйте компонент **SAPReportingForApps**. Кроме того, обратите внимание, что второй компонент (ID: **9b60ccba-ebfd-4e38-87c8-3dea9cc2680a**) поставляется вместе с Duet Enterprise 2.0, но оно будет помечено как скрытый. При использовании этого подхода можно сделать разработчик использование этой функции и можно свести в возможности отчетов Duet для приложения.
  
    
    
После активации компонента **DuetReportingForApps** в этот выпуск все артефакты (список отчетов, Lib, формы, и т.д.) и настройки на сайте приложения, но как шаблон сайта приложения не имеет стандартный навигационных ссылок, разработчик приложения должен добавлять элементы пользовательскую страницу для переноса в работе компонентов Duet (например параметры отчета, представление списка библиотеки и форм). Разработчик должен документации стандартных Duet для функции отчетности для получения дополнительных сведений о части компонента и его элементы пользовательского интерфейса. Разработчик может выбрать для создания настраиваемого пользовательского интерфейса для функции точки входа которых для удовлетворения лучше с общей темой приложения.
  
    
    

## <a name="viewing-the-results"></a>Просмотр результатов
<a name="bkmk_ViewingTheResults"> </a>

Чтобы просмотреть страницу Параметры отчета по умолчанию, перейдите к: **~/Lists/ReportSetting/AllReportTemplate.aspx**.
  
    
    
Чтобы просмотреть представление по умолчанию для библиотеки документов, отчетов, перейдите к: **~/ReportsLib/Forms/AllItems.aspx**.
  
    
    

## <a name="customizing-the-reports"></a>Настройка отчетов
<a name="bkmk_CustomizingTheReports"> </a>

Внутри приложения разработчик можно создать свой собственный пользовательский Интерфейс (с использованием HTML/JavaScript/Jquery и т.д.) и создать более широких возможностей пользователя с помощью BCS CSOM. После снимки экрана показано аналогичные приложения, где настраиваемых HTML-код на основе пользовательского интерфейса создается с помощью готовые артефакты и интерфейсы API BCS на стороне клиента.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Разработка с помощью Duet Enterprise 2.0](developing-with-duet-enterprise-2-0.md)
    
  
-  [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

