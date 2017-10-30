---
title: "Разработка с помощью Duet Enterprise 2.0"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c3ef38aa-559e-4832-95c7-75e222c77624
ms.openlocfilehash: 15b9ac70484db215dd36a46d3648999aa26664e5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="developing-with-duet-enterprise-20"></a>Разработка с помощью Duet Enterprise 2.0

## <a name="overview"></a>Обзор
<a name="Overview"> </a>

Duet Enterprise 2.0 является последней версии совместная работа между Microsoft и SAP, чтобы разрешить пользователям SharePoint для работы с данными из системы SAP. Объединяет компоненты SAP, а также SharePoint и SharePoint Online. Она дает разработчику создавать компоненты, которые позволяют пользователям для переноса данных из системы SAP в знакомой среде SharePoint.
  
    
    

## <a name="features-of-duet-enterprise-20"></a>Функции Duet Enterprise 2.0
<a name="Overview"> </a>

При правильной установки и настройки, Duet Enterprise 2.0 будет предоставлять следующие возможности:
  
    
    

- Можно работать с данными в системы SAP в SharePoint с помощью Business данных веб-частей, внешних списков и пользовательских компонентов.
    
  
- Использование данных SAP в SharePoint без кода с помощью встроенных компонентов.
    
  
- С помощью отчетов систем внутри приложения SAP.
    
  
- Использовать специальные веб-части, установленные вместе с Duet Enterprise 2.0 для добавления данных SAP на страницы SharePoint
    
  
- Использование рабочего процесса SAP в приложении.
    
  
- JavaScript на стороне клиента могут использоваться разработчиками для взаимодействия с внешними данными SAP.
    
  
- Обеспечение безопасной данных с помощью OAuth для проверки подлинности.
    
  

## <a name="setting-up-the-development-environment"></a>Настройка среды разработки
<a name="SettingUp"> </a>

Разработка надстройки SharePoint с помощью Duet Enterprise 2.0, в основном совпадает с точно создание стандартной надстройки SharePoint. Visual Studio можно использовать для расширения возможностей приложений и работать в среде надежной среды разработки Visual Studio.
  
    
    

## <a name="adding-external-content-types"></a>Добавление внешних типов контента
<a name="AddingECT"> </a>

Для доступа к внешним данным, размещенное в системе SAP, необходимо добавить внешний тип контента. Поскольку данных SAP предоставляется через конечные точки OData, средства для автоматического создания, установленные в Visual Studio можно использовать для [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) , областью действия на уровне приложения.
  
    
    
Выполните следующие действия для создания внешнего типа контента.
  
    
    

### <a name="creating-an-external-content-type-from-an-sap-odata-endpoint"></a>Создание внешнего типа контента из конечную точку SAP OData


1. В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.
    
  
2. На странице **Укажите источника OData** введите URL-адрес службы рабочих процессов Duet Enterprise.
    
  
3. Выберите имя для источника OData.
    
  
4. Выбор сущностей, которые требуются.
    
  
5. Нажмите кнопку **Готово**.
    
  
Visual Studio создаст новую папку с именем внешних типов контента, где можно найти только что созданный модели BDC.
  
    
    

## <a name="configuring-the-bdc-model"></a>Настройка модели BDC
<a name="ConfiguringProject"> </a>

Важно сделайте проект работать, заключается в добавлении свойство **ODataExtensionProvider** для модели BDC. Это свойство определяет поставщик расширения, который предоставляет BCS с расширениями SAP, необходимые для создания кода приложения.
  
    
    
В этом примере показаны свойства, добавленные в модели BDC:
  
    
    



```XML

<LobSystem Type="OData" Name="LOB_SYSTEM_NAME">
                     <Properties>
                          <Property Name="ODataServiceMetadataUrl" Type="System.String">
                               https://<DUET_METADATA_URL>:443/sap/opu/odata/sap/ 
                               ZANDY_PO_HEADER_SRV/$metadata</Property>
                          <Property Name="ODataServicesVersion" Type="System.String">2.0</Property>
                          <Property Name="ODataExtensionProvider" Type="System.String"> 
                               OBA.Server.Canary.ObaOdataServerExtensionProvider, 
                               OBA.Server.SSOProvider, 
                               Version=15.0.0.0, 
                               Culture=neutral, 
                               PublicKeyToken=71e9bce111e9429c</Property>
                          <Property Name="TraceHeader" Type="System.String">SAP-PASSPORT</Property>
                     </Properties>

```


## <a name="using-duet-starter-services-to-develop-custom-apps"></a>Использование Duet starter services для разработки настраиваемых приложений
<a name="UsingDuetStarterServices"> </a>

Duet Enterprise 2.0 устанавливается несколько служб starter к файловой системе на сервере SharePoint. Установка по умолчанию, эти файлы находятся в C:\\Program Files\\Duet Enterprise\\2.0\\решений\\Starter Services. Эти действия включают: 
  
    
    

- OBACustomerWorkspace
    
  
- OBAOrderToCash
    
  
- OBAPortal
    
  
- OBAProductCenter
    
  
Каждый из этих решений содержит WSP файлов, решения и другие вспомогательные файлы, необходимые для их реализации.
  
    
    
Эти решения можно использовать для просмотра, что можно сделать с Duet Enterprise 2.0 и какие шаблоны разработки, но не поддерживаются для использования в Надстройки SharePoint.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="ConNavExample_resources"> </a>


-  [Duet Enterprise для Microsoft SharePoint и SAP Server 2.0](http://technet.microsoft.com/en-us/library/ff972436.aspx)
    
  
-  [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Центр разработчиков Visual Studio](http://msdn.microsoft.com/en-us/vstudio/default)
    
  
-  [Разработка на базе Office с помощью Visual Studio](http://msdn.microsoft.com/en-us/office/hh133430)
    
  

