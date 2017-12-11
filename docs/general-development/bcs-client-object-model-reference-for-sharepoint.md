---
title: "BCS клиента Справочник по объектной модели для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fe7d12a3-6ea9-47f9-b69e-f66da9e661dc
ms.openlocfilehash: 270b8d32d5f416f9e4ac37f1452ea672a737b5b1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="bcs-client-object-model-reference-for-sharepoint"></a>BCS клиента Справочник по объектной модели для SharePoint

  
    
    
![Ссылки и библиотеки класса](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
Сведения об объектах, доступных для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемые Business Connectivity Services (BCS).
Доступны следующие объекты для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, взаимодействующий с Business Connectivity Services (BCS). BCS объектной модели, компоненты, предоставляемые клиентскую объектную модель, находятся в библиотеке Microsoft.SharePoint.Client.dll.
  
    
    


## <a name="entity-object"></a>Объект сущности
<a name="bkmk_Entity"> </a>

Объект **Entity** по сути представляет таблицу в базе данных. Методы и свойства, представленные здесь Показать объекты, которые можно управлять с помощью клиентской библиотеки кода. Каждый из этих вызовов сопоставляет непосредственно звонка server объектной модели. Тем не менее они могут вызываться отключением клиента, такие как и в веб-браузере с помощью JavaScript.
  
    
    

**Методы**


|**Методы**|**Подпись метода**|**Описание**|
|:-----|:-----|:-----|
|**Create** <br/> | `Identity Create(FieldValueDictionary fieldValues, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**FindSpecificDefault** <br/> | `EntityInstance FindSpecificDefault(Identity identity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**FindspecificByBdcIDDefault** <br/> | `EntityInstance FindSpecific(Identity identity, string specificFinderName, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**FindSpecificByBdcID** <br/> | `EntityInstance FindSpecificByBdcIDDefault(string BdcIdentity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|**GetCreatorView** <br/> | `EntityInstance FindSpecificByBdcID(string BdcIdentity, string specificFinderName,LobSystemInstance LobSystemInstanceName)` <br/> ||
|**GetDefaultSpecificFinderView** <br/> | `View GetCreatorView(string methodInstanceName)` <br/> ||
|**GetSpecificFinderView_Client** <br/> | `View GetDefaultSpecificFinderView()` <br/> ||
|**GetUpdaterView_Client** <br/> | `View GetSpecificFinderView_Client( string specificFinderName)` <br/> ||
|**GetIdentifiers** <br/> | `View GetUpdaterView_Client(string updaterName)` <br/> ||
|**GetIdentifiers()** <br/> |||
   

**Свойства**


|**Свойство**|**Описание**|
|:-----|:-----|
| `long EstimatedInstanceCount { get; }` <br/> |Получает число ожидаемых внешние элементы этого внешнего типа контента.  <br/> |
| `string Name { get; }` <br/> |Возвращает имя объекта метаданных.  <br/> |
| `string Namespace { get; }` <br/> |Возвращает пространство имен класса данных.  <br/> |
| `int GetIdentifierCount()` <br/> ||
   

## <a name="entityinstance-method"></a>Метод экземпляра сущности
<a name="bkmk_EntityInstance"> </a>


**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP. BusinessData.Runtime** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**Delete** <br/> |void  <br/> |Удаление внешнего элемента.  <br/> |
|**FromXml** <br/> |void  <br/> |Задает значения в словаре из указанного XML.  <br/> **Подпись метода**          `FromXml(string xml)` <br/> |
|**GetIdentity** <br/> |Identity  <br/> |Получает идентификатор этого внешнего элемента.  <br/> |
|**Delete** <br/> |void  <br/> |Удаление внешнего элемента.  <br/> |
|**ToXml** <br/> |string  <br/> |Извлекает значения в формате XML.  <br/> |
|**Update** <br/> |void  <br/> |Отправляет данные изменения, внесенные внешнего элемента.  <br/> |
   

  
    
    

**Properties**


|**Свойство**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
| `this[string fieldDotNotation] { get; set; }` <br/> |Объект  <br/> |Получает или задает значение поля, на который ссылается точечную нотацию.  <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |строка  <br/> ||
   

## <a name="entityview-method"></a>Метод EntityView
<a name="bkmk_entityview"> </a>

Определяет настраиваемое представление данных **сущности**
  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP. BusinessData** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**GetDefaultValues_Client()** <br/> |**Словаря** <br/> |Получает словарь значение поля, который содержит значения по умолчанию для этого представления.  <br/> |
|**GetXmlSchema()** <br/> |**string** <br/> |Возвращает схему XML для представления.  <br/> |
|**GetType (строка fieldDotNotation)** <br/> |**string** <br/> |Получает тип указанного поля.  <br/> |
|**GetType (строка fieldDotNotation)** <br/> |**Дескриптор типа** <br/> |Получает объект **TypeDescriptor**, соответствующий заданным точечную нотацию. <br/> |
   

**Properties**


|**Свойство**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
| `Fields { get; }` <br/> |**FieldCollection** <br/> |Получает коллекцию всех полей в представлении.  <br/> |
| `Name { get; }` <br/> |**string** <br/> |Получает имя объекта **View** <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |**string** <br/> |Получает имя специальный метод поиска **MethodInstance**, которая связана с этого представления. <br/> |
   

## <a name="lobsystem-method"></a>Метод бизнес-системы
<a name="bkmk_LobSystem"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP. BusinessData** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**GetLobSystemInstances()** <br/> |**void** <br/> |Предоставляет список экземпляров системы LOB.  <br/> |
|**Name** <br/> |**void** <br/> |Получает имя **LobSystem**.  <br/> |
   

**Properties**


|**Свойство**|**Описание**|
|:-----|:-----|
|Нет  <br/> ||
   

## <a name="lobsysteminstance-method"></a>Метод бизнес-системы
<a name="bkmk_LobSystemInstance"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP. BusinessData** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|Нет.  <br/> |**void** <br/> ||
   

**Properties**


|**Свойство**|**Описание**|
|:-----|:-----|
|Нет  <br/> ||
   

## <a name="identifier-method"></a>Метод идентификатор
<a name="bkmk_Identifier"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP. BusinessData** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**ContainsLocalizedDisplayName** <br/> |**bool** <br/> |Определяет, содержит ли объект метаданных локализованное отображаемое имя.  <br/> |
|**GetDefaultDisplayName** <br/> |**string** <br/> |Возвращает отображаемое имя по умолчанию.  <br/> |
|**GetLocalizedDisplayName** <br/> |**string** <br/> |Возвращает локализованное отображаемое имя.  <br/> |
   

**Properties**


|**Свойство**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
| `IdentifierType {get;}` <br/> |**string** <br/> |Возвращает тип идентификатора.  <br/> |
| `Name {get;}` <br/> |**string** <br/> |Получает имя идентификатора.  <br/> |
   

## <a name="identifiercollection-method"></a>Метод IdentifierCollection
<a name="bkmk_IdentifierCollection"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel.Collections** <br/> |**SP. BusinessData.Collections** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|Нет.  <br/> |**void** <br/> ||
   

**Properties**


|**Свойство**|**Описание**|
|:-----|:-----|
|Нет  <br/> ||
   

## <a name="identity-method"></a>Метод удостоверений
<a name="bkmk_Identity"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP. BusinessData.Runtime** <br/> |
   

**Конструктор**


|**Конструктор**|**Описание**|
|:-----|:-----|
| `public Identity (Object[] identifierValues)` <br/> |Создает новый экземпляр класса с помощью массив значений идентификаторов.  <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**Serialize** <br/> |**string** <br/> |Возвращает строковое представление удостоверения.  <br/> |
   

**Properties**


|**Свойство**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
| `IdentifierCount { get; }` <br/> |**int** <br/> |Возвращает число идентификаторов.  <br/> |
| `IsTemporary { get; }` <br/> |**bool** <br/> |Проверяет, является ли идентификатор временного.  <br/> |
| `this[int identifierIndex] { get; }` <br/> |**Object** <br/> |Получает элемент по указанному индексу. CSOM не поддерживает на основе int индексирования. На основе строки доступа к данным реализован для того же.  <br/> |
| `TemporaryId { get; }` <br/> |**Guid** <br/> |Возвращает временной части удостоверения.  <br/> |
   

## <a name="fieldvaluedictionary-method"></a>Метод словаря
<a name="bkmk_FieldValueDictionary"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP. BusinessData.Runtime** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**FromXml** <br/> |**void** <br/> |Задает значения в словаре из указанного XML.  <br/> |
|**GetCollectionSize** <br/> |целое  <br/> |Возвращает размер семейства сайтов, на который ссылается точечную нотацию.  <br/> |
|**ToXml** <br/> |string  <br/> |Извлекает значения в формате XML.  <br/> |
   

**Properties**


|**Свойство**|**Описание**|
|:-----|:-----|
| `Object this[string fieldDotNotation] { get; set; }` <br/> |Получает или задает значение поля, на который ссылается точечную нотацию.  <br/> |
   

## <a name="entityfieldcollection-method"></a>Метод EntityFieldCollection
<a name="bkmk_EntityFieldCollection"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP. BusinessData.Runtime** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|Нет.  <br/> |**void** <br/> ||
   

**Properties**


|**Свойство**|**Описание**|
|:-----|:-----|
|Нет  <br/> ||
   

## <a name="entityfield-method"></a>Метод EntityField
<a name="bkmk_Entityfield"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.Runtime** <br/> |**SP. BusinessData.Runtime** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|Нет  <br/> |void  <br/> ||
   

**Properties**


|**Свойство**|**Возвращаемый тип**|**Только чтение**|**Описание**|
|:-----|:-----|:-----|:-----|
|**ContainsLocalizedDisplayName** <br/> |**Boolean** <br/> |Да  <br/> |Определяет, содержит ли поле локализованное отображаемое имя.  <br/> |
|**DefaultDisplayName** <br/> |**string** <br/> |Да  <br/> |Получает отображаемое имя по умолчанию поля.  <br/> |
|**GetLocalizedDisplayName** <br/> |**string** <br/> ||Получает локализованное отображаемое имя поля.  <br/> |
|**Name** <br/> |**string** <br/> |Да  <br/> |Получает имя поля.  <br/> |
   

## <a name="typedescriptor-class"></a>Класс TypeDescriptor
<a name="bkmk_TypeDescriptor"> </a>


  
    
    

**Пространства имен**


|**Managed (Управляемая)**|**JavaScript**|
|:-----|:-----|
|**Microsoft.BusinessData.MetadataModel** <br/> |**SP. BusinessData** <br/> |
   

**Методы**


|**Метод**|**Возвращаемый тип**|**Только чтение**|**Описание**|
|:-----|:-----|:-----|:-----|
|**ContainsLocalizedDisplayName()** <br/> |**Boolean** <br/> |Да  <br/> |Определяет, содержит ли дескриптор типа локализованное отображаемое имя.  <br/> |
|**GetLocalizedDisplayName()** <br/> |**string** <br/> |Да  <br/> |Возвращает локализованное отображаемое имя.  <br/> |
|**GetDefaultDisplayName()** <br/> |**string** <br/> ||Возвращает отображаемое имя по умолчанию.  <br/> |
   

**Properties**


|**Свойство**|**Возвращаемый тип**|**Описание**|
|:-----|:-----|:-----|
|**Name** <br/> |string  <br/> |Получает имя поля.  <br/> |
|**Имя типа** <br/> |string  <br/> |Получает имя типа данных, представленного в этом дескриптором типа.  <br/> |
|**IsReadOnly** <br/> |Логический  <br/> |Определяет, является ли этот тип дескриптора структуру данных только для чтения.  <br/> |
|**ContainsReadOnly** <br/> |Логический  <br/> |Определяет, представляют ли этот дескриптор типа или одного из его дочерние элементы структуры данных только для чтения.  <br/> |
|**IsCollection** <br/> |Логический  <br/> |Определяет, представляет ли описанного типа структуры данных семейства сайтов.  <br/> |
   

## <a name="interfaces"></a>Интерфейсы
<a name="bkmk_Interfaces"> </a>

Пространство имен является **Microsoft.BusinessData.MetadataModel**.
  
    
    


|**Интерфейс**|**Описание**|
|:-----|:-----|
|**IMetadataCatalog** <br/> |Точка входа для объектной модели BDC. Используйте **DatabaseBasedMetadataCatalog** на сервере.<br/> |
|**ILobSystem** <br/> |Содержит сведения о внешней системе.  <br/> |
|**IEntity** <br/> |Внешний тип контента в хранилище метаданных службы подключения к бизнес-данным.  <br/> |
|**IMethod** <br/> |Операция, которую можно выполнить с внешним типом контента.  <br/> |
|**IEntityInstance** <br/> |Экземпляр сущности (также известной как внешнего элемента) представляет собой отдельный элемент, возвращенный из внешней системы в BDC.  <br/> Интерфейс **IEntityInstance** выделяет используемых источников данных и изолирует клиентов от необходимости сведения схемы написания кода конкретного приложения; позволяет им получить доступ к всем бизнес-данным в одном упрощенный способ. С помощью интерфейса **IEntityInstance**, можно работать со строкой данных из базы данных в точно так же, так как работа с сложную структуру .NET Framework, возвращаемый веб-службой. <br/> Экземпляр сущности в BDC имеет специальной семантики, подключенного к нему. Например имеет возможность знать, какие поля или поля строки, представляющие идентификатор для экземпляра сущности и позволяет звонить методы, такие как **GetAssociated**, **GetIdentifierValues**и **Execute**на этот экземпляр сущности. <br/> |
|**IEntityInstanceEnumerator** <br/> |Перечислителя может использоваться для чтения данных в коллекции внешние элементы, но не может использоваться для изменения коллекции. **IEntityInstanceEnumerator** поддерживает потоковая передача и поэтому очень полезен при возврате серверного приложения больших объемов данных.<br/> |
   

## <a name="client-object-model-faq"></a>Вопросы и ответы по объектной модели клиента
<a name="bkmk_ClientObjectModelFAQ"> </a>


- **Does <Method> тег нужно включить в запрос CAML при запросе внешнего списка**
    
    Нет. 
    
  
- **Есть ли необходимость всех полей во внешний список с помощью запроса CAML?**
    
    Использование тега текст ViewXML в модели BDC, разработчик можно указать только те поля, которые необходимы и CSOM API-интерфейсы для списков будет возвращать только те поля.
    
  

## <a name="see-also"></a>См. также
<a name="bkmk_Addres"> </a>


-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [Справка по API клиента .NET для SharePoint](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx)
    
  
-  [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
