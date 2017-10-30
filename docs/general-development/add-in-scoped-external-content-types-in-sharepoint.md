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
# <a name="add-in-scoped-external-content-types-in-sharepoint"></a>Добавьте в пределах внешние типы контента в SharePoint
Сведения о внешних типов контента, для которых установлены или областью действия на уровне надстройки в SharePoint и позволяют создавать насыщенные Add-ins SharePoint с помощью внешних источников данных.
## <a name="overview-of-add-in-scoped-external-content-types-in-sharepoint"></a>Общие сведения о добавьте в пределах внешние типы контента в SharePoint
<a name="Appscopedect_overview"> </a>

В SharePoint 2010 могут устанавливать и использовать внешние типы контента только на уровне фермы. Это часто вызывает проблемы для разработчиков, поскольку даже для простых приложений администратора были вынуждены принимать участие из-за права доступа, необходимые для установки на уровне фермы.
  
    
    
В SharePoint по сути изоляции приложений в более автономных единиц, называемое надстройками надстройки содержат все ресурсы, необходимые для запуска. Данный подход позволяет приложения для изолируется от других приложений. Преимущества данной архитектуры, следующим образом:
  
    
    

- Можно создать надстроек, выровненные с помощью новой модели приложения для SharePoint.
    
  
- Можно создать надстроек, доступа к внешним данным из SAP, Netflix и частный и других типов данных без привлечения администратора клиента.
    
  
- Доступ к внешним приложениям поддерживать через Службы Business Connectivity Services (BCS), который предоставляет согласованную и универсальный интерфейс, который может использоваться другими приложениями SharePoint.
    
  
Добавьте в пределах внешние типы контента предоставляют доступ к внешним данным в приложении.
  
    
    

## <a name="prerequisites-for-working-with-add-in-scoped-external-content-types"></a>Необходимые условия для работы с добавления в пределах внешних типов контента
<a name="Appscopedect_Prereq"> </a>

Ниже приведены требования для разработки внешних типов контента, которые находятся на уровне надстройки:
  
    
    

- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- SharePoint
    
  
Сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="add-in-scoped-external-content-type-essentials"></a>Добавьте в пределах внешнего типа контента essentials

В таблице 1 представлены некоторые основные концепции, которые необходимо ознакомиться с при работе с добавления в пределах внешних типов контента.
  
    
    

**В таблице 1. Основные понятия, которые для понимания добавьте в пределах внешних типов контента**


|**Статья**|**Описание**|
|:-----|:-----|
| [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md) <br/> |Сведения о создании BCS внешних типов контента.  <br/> |
| [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.  <br/> |
| [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx) <br/> |Узнайте, как создать простой SharePoint хостингом надстройки с помощью Инструменты разработчика Office для Visual Studio 2012.  <br/> |
   

## <a name="what-can-you-do-with-add-in-scoped-external-content-types"></a>Что можно делать с добавления в пределах внешних типов контента
<a name="Appscopedect_Tasks"> </a>

Для предоставления доступа к внешним данным из отдельных надстроек  основная причина для добавления добавить в пределах внешнего типа контента. Это позволяет выполните следующее: 
  
    
    

- Ограничение доступа к внешние типы контента для конкретного приложения.
    
  
- Развертывание внешних типов контента в пределах приложения.
    
  

### <a name="create-add-in-scoped-external-content-types"></a>Добавьте в пределах внешних типов контента
<a name="Appscopedect_createect"> </a>

Понятие каталога на основе файла метаданных была введена в SharePoint 2010. Позволяет указать, что файл, содержащий XML-код необходимый для определения внешних типов контента. Этот файл могут быть развернуты внутри пакета WSP и относится только к приложению, предназначенную для. С помощью этого файла метаданных, внешние типы контента можно ограничить уровень надстройки.
  
    
    
В SharePoint чтобы добавить свойство, которое указывает, области применения была изменена **SPListDataSource** .
  
    
    
Этот класс выступает в качестве моста между **SPList** и внешнего списка. Использование связанного **SPList** для получения данных и полей сущности. Получить экземпляр **SPListDataSource** из свойства **HasExternalDataSource** . При **HasExternalDataSource** не равно null, объект **SPList** данные являются внешними по отношению к SharePoint.
  
    
    
Если вы хотите добавить добавить в пределах внешнего типа контента, это свойство имеет значение **Add-in**.
  
    
    
Свойство **MetadataCatalogFileName** используется для определения файла модели BDC, который содержит определение внешнего типа контента. Это свойство может быть определен декларативно или программно, но не в SharePoint пользовательского интерфейса (UI).
  
    
    
Следующем примере показано, как задать свойство **MetadataCatalogFileName** декларативно.
  
    
    



```XML

<DataSource>
  <Property Name="Entity" Value="Customer" />
  <Property Name="EntityNamespace" Value="SAP" />
  <Property Name="LobSystemInstanceName" Value="SAPClient1" />
  <Property Name="SpecificFinder" Value="ReadCustomer" />
  <Property Name=" MetadataCatalogFileName" Value="BDCMetadata.bdcm" />
</DataSource>
```


> **Примечание:** Администраторы сайтов можно установить надстройки, использующие областью действия ect приложения, но только администраторы SiteCollection может предоставить разрешения для приложений для использования подключения к службе BCS. 
  
    
    


### <a name="deploy-an-add-in-scoped-external-content-type-in-a-custom-feature-in-a-wsp-file"></a>Развертывание добавить в пределах внешнего типа контента в настраиваемый компонент в WSP-файла
<a name="Appscopedect_deployect"> </a>

Модели BDC можно включить в WSP-файла для развертывания. Следующем примере показано, как включить модели BDC в приложение.
  
    
    

```XML

<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <BdcModel Path="BDCMetadata.bdcm">
  </BdcModel>
</Elements>

```


> **Важные:** Только один файл модели BDC можно включить на надстройки. При BDCMetadata.bdcm имя файла в этом примере файл модели фактически может быть любое имя, выбранное при условии, что соответствует имени файла, который является в атрибуте **путь** к файлу модели BDC.
  
    
    


> **Примечание:** Только Open Data protocol (OData) подключений для добавления в пределах внешних типов контента. 
  
    
    


### <a name="set-security-credentials-for-an-external-system"></a>Задать учетные данные безопасности для внешней системы
<a name="Appscopedect_deployect"> </a>

Чтобы получить доступ к данным на защищенном внешней системы, необходимо настроить модели BDC с соответствующие учетные данные.
  
    
    
Следующем примере показано, как задать учетные данные безопасности для внешней системы в добавить в пределах внешних типов контента, внести изменения в файл Elements.xml приложения.
  
    
    



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


## <a name="in-this-section"></a>В этом разделе
<a name="Appscopedect_inthissection"> </a>


-  [Как: создание добавить в пределах внешнего типа контента в SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [Доступ ко внешним данным с помощью REST в SharePoint](how-to-access-external-data-with-rest-in-sharepoint.md)
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="Appscopedect_Addres"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Внешние события и оповещения в SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

