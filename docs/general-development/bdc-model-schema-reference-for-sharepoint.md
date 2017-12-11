---
title: "Справочник по схеме модели BDC для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 979a5ffc-f033-4e72-b2d1-11d8cb1b294a
ms.openlocfilehash: dd78f6a347894eff60149df672d251cfa4c26bd7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="bdc-model-schema-reference-for-sharepoint"></a>Справочник по схеме модели BDC для SharePoint
Содержит справочную документацию по схеме модели BDC (BDCMetadata.xsd), который можно использовать для создания внешних типов контента в SharePoint. 
 [BDCMetadata.xsd](http://schemas.microsoft.com/windows/2007/BusinessDataCatalog)
  
    
    


## <a name="accesscontrolentry-element"></a>Элемент AccessControlEntry
<a name="bkmk_AccessControlEntry"> </a>

Содержит запись управления доступом (ACE), которая определяет права доступа для родительского элемента.
  
    
    
В статье  [Обзор системы безопасности служб Business Connectivity Services](http://technet.microsoft.com/en-us/library/ee661734%28office.14%29.aspx) приведены дополнительные сведения о Business Connectivity Services и системе безопасности.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML

<AccessControlEntry Principal = "String"> </AccessControlEntry>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Principal  <br/> |Обязательный атрибут.  <br/> Имя участника безопасности, содержащего эту запись управления доступом.  <br/> Тип атрибута: **String** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Right в элементе AccessControlEntry (схема BDCMetadata)](http://msdn.microsoft.com/library/a2e4bd6c-2306-b657-7290-cc9c9b262911%28Office.15%29.aspx) <br/> |Элемент **Right**, который задает разрешения, доступные для участника безопасности. <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Список управления доступом (ACL), содержащий эту запись управления доступом.  <br/> |
   

## <a name="accesscontrollist-element"></a>Элемент AccessControlList
<a name="bkmk_AccessControlList"> </a>

Определяет список управления доступом (ACL) для родительского элемента.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<AccessControlList></AccessControlList>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент AccessControlEntry в AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |Элемент управления доступом (ACE).  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Model (схема BDCMetadata)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |Модель, которая содержит внешние типы контента в бизнес-приложение.  <br/> |
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Элементы LobSystem, которые содержатся в модели.  <br/> |
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Внешний тип контента.  <br/> |
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Метод внешнего типа контента.  <br/> |
| [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |Связь.  <br/> |
| [Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |Экземпляр метода внешнего типа контента.  <br/> |
   

## <a name="action-element"></a>Элемент Action
<a name="bkmk_Action"> </a>

Указывает действие, поддерживаемых внешнего типа контента.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    
Действия устранить разрыв между SharePoint и Office 2013 и внешняя система пользовательского интерфейса, предоставляя ссылку на внешнюю систему. 
  
    
    
По умолчанию Служба подключения к бизнес-данным (BDC) предоставляет действий, таких как **View Item**, **Edit Item**и **Delete Item** после модели эти операции в модели BDC. Помимо этих действий по умолчанию можно создать действия для других функций, которые необходимо присоединить к внешним типом контента. Например, можно использовать действия для выполнения простых действий, таких как отправка сообщения электронной почты для клиента из внешнего типа контента клиента или открытие клиента домашней страницы в браузере.
  
    
    
Действия, передаются с внешним типом контента. То есть, после определения действия для внешнего типа контента, то действие отображается везде отображать этот внешний тип контента, в внешнего списка или веб-часть бизнес данных или в столбец внешних данных. 
  
    
    



```XML
<Action Position = "Integer" IsOpenedInNewWindow = "Boolean" Url = "String" ImageUrl = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Action>
```

В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Position** <br/> |Обязательный атрибут.  <br/> Предлагаемые положение это действие среди других действий этот внешний тип контента.  <br/> Тип атрибута: **Integer** <br/> |
|**IsOpenedInNewWindow** <br/> |Необязательный.  <br/> Указывает ли результаты выполнения действия в новом окне интерфейса пользователя.  <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**Url** <br/> |Обязательный атрибут.  <br/> URL-адрес для перехода при вызове действия. Строка URL-адреса  это строка формата .NET Framework. Каждого описателя формата (например, {0}) соответствует параметру **Action**.<br/> Тип атрибута: **String** <br/> |
|**ImageUrl** <br/> |Необязательный.  <br/> Абсолютный или относительный путь для изображения значка для действия. Изображение значка должен быть 16 x 16 пикселей.<br/> Тип атрибута: **String** <br/> |
|**Name** <br/> |Обязательный атрибут.  <br/> Имя этого действия.  <br/> Тип атрибута: **String** <br/> |
|**DefaultDisplayName** <br/> |Необязательный атрибут.  <br/> Отображаемое имя по умолчанию для этого действия.  <br/> Тип атрибута: **String** <br/> |
|**IsCached** <br/> |Необязательный атрибут.  <br/> Указывает, используется ли это действие часто. Это используется клиентская среда BDC для кэширования этого действия.<br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена действие.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства действия.  <br/> |
| [Элемент ActionParameters в элементе Action (схема BDCMetadata)](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |Параметры действия.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Actions в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |Список действий для внешнего типа контента.  <br/> |
   

## <a name="actionparameter-element"></a>Элемент ActionParameter
<a name="bkmk_ActionParameter"> </a>

Задает параметры действия на основе URL-адреса. Определяет способ параметризации URL-адреса действия с данными, связанными с **EntityInstance**.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    
Атрибут URL-адреса действия на основе URL-адреса может принимать параметры с помощью элемента **ActionParameter**.
  
    
    

> **Важно:**
> **ActionParameters** может представлять значения идентификатора, а также значений, которые соответствуют **дескрипторами типов** в **SpecificFinder** **сущности**. **ActionParameter** представляет значение идентификатора при наличии свойство **IdOrdinal** . Значение свойства указывает индекс идентификатор, значение которого представляет этот **ActionParameter** . Если свойство **IdOrdinal** не указан, **ActionParameter** представляет **дескриптор типа**, а атрибут **Name** указывает, представленное какие дескриптор типа. **Имя** атрибута указано как **Временный путь**. 
  
    
    

Элемент **ActionParameter** принимает следующее свойство.
  
    
    

> **Важные:** В свойствах учитывается регистр. 
  
    
    


**Свойства**


|**Свойство**|**Тип**|**Описание**|**Обязательный атрибут.**|**Значение по умолчанию**|**Ограничения/Приемлемые значения**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|**IdOrdinal** <br/> |**System.Int32** <br/> |Указывает, представляет ли **ActionParameter** идентификатор вместо поля. <br/> |Необязательный  <br/> |||
   



```XML
<ActionParameter Index = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </ActionParameter>
```

В следующих разделах приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Index** <br/> |Обязательный атрибут.  <br/> Порядковый атрибут, который определяет позицию этого параметра **ActionParameter** среди других параметров **ActionParameters** в URL-адресе. <br/> Тип атрибута: **Integer** <br/> |
|**Name** <br/> |Обязательный атрибут.  <br/> Имя **ActionParameter**.  <br/> Тип атрибута: **String** <br/> |
|**DefaultDisplayName** <br/> |Необязательный атрибут.  <br/> Отображаемое по умолчанию имя параметра **ActionParameter**.  <br/> Тип атрибута: **String** <br/> |
|**IsCached** <br/> |Необязательный атрибут.  <br/> Задает частоту использования этого параметра **ActionParameter**. Этот атрибут используется клиентской средой выполнения подключения к бизнес-данным для кэширования данного **Action**. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованное имя параметра **ActionParameter** по умолчанию.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства **ActionParameter**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент ActionParameters в элементе Action (схема BDCMetadata)](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |Элемент **ActionParameters**, содержащий этот **ActionParameter**.  <br/> |
   

## <a name="actionparameters-element"></a>Элемент ActionParameters
<a name="bkmk_ActionParameters"> </a>

Задает список **ActionParameters** для действия.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<ActionParameters></ActionParameters>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет.
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент ActionParameter в элементе ActionParameters (схема BDCMetadata)](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> |**ActionParameter**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Action в Actions (схема BDCMetadata)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |**Action**, к которой относятся следующие **ActionParameters**. <br/> |
   

## <a name="actions-element"></a>Элемент Actions
<a name="bkmk_Actions"> </a>

Указывает список действий внешнего типа контента.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Actions></Actions>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Action в Actions (схема BDCMetadata)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |Действие внешнего типа контента.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Внешний тип контента, к которой относятся следующие действия.  <br/> |
   

## <a name="association-element"></a>Элемент сопоставления
<a name="bkmk_Association"> </a>

Элемент сопоставления связывает связанных внешних типов контента в системе. Например, клиент связан с заказа на продажу в системе AdventureWorks: клиенту делает заказов на продажу. Связь хранит указатели на источника и назначения внешних типов контента и указатель на бизнес-логики (объект **MethodInstance** ), который позволяет клиенту получить внешний тип контента назначения из внешнего типа контента источника. Обход **Association**  это вызов метода во внешней системе.
  
    
    

  
    
    
 **Пространство имен:** http://schemas.microsoft.com/windows/2007/BusinessDataCatalog
  
    
    
 **Схема:** BDCMetadata
  
    
    

> **Важные:** В свойствах учитывается регистр. 
  
    
    


**Свойства**


|**Свойство**|**Тип**|**Описание**|**Обязательный**|**Значение по умолчанию**|**Ограничения/Приемлемые значения**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|**HideOnProfilePage** <br/> |**System.Boolean** <br/> |Указывает, следует ли добавить связанного внешнего типа контента на страницу профиля главной внешнего типа контента.  <br/> |Необязательный  <br/> |||
   



```XML
<Association Type = "String" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Association>
```

В следующих разделах приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Type** <br/> |Обязательный атрибут.  <br/> **MethodInstanceType**, определяющее тип связи. <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/>         <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>AssociationNavigator</p></td><td><p>**MethodInstance**  это **AssociationNavigator**.</p></td></tr><tr><td><p>Соединитель</p></td><td><p>**MethodInstance**  это **Associator**.</p></td></tr><tr><td><p>Метод disassociator</p></td><td><p>**MethodInstance**  это **Disassociator**.</p></td></tr><tr><td><p>**Данные BulkAssociatedIdEnumerator**</p></td><td><p>**MethodInstance**  это **BulkAssociatedIdEnumerator**.</p></td></tr><tr><td><p>**Метод BulkAssociationNavigator**</p></td><td><p>**MethodInstance**  это **BulkAssociationNavigator**.</p></td></tr></tbody></table>|
|Значение по умолчанию  <br/> |Необязательное.  <br/> Указывает, является ли связь по умолчанию среди всех сопоставлений, общий доступ к его тип, содержащего внешнего типа контента. Если параметр имеет значение **true**, связь, по умолчанию среди всех сопоставлений, общий доступ к его тип, содержащего внешнего типа контента. Если параметр имеет значение **false**, связь не по умолчанию среди всех сопоставлений, общий доступ к его тип, содержащего внешнего типа контента. <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|ReturnParameterName  <br/> |Необязательное.  <br/> Имя параметра, который содержит **ReturnTypeDescriptor** связи. Атрибут **Direction** параметр должен содержать значение "В работе", "InOut" или "Вернуть". <br/> Тип атрибута: **String** <br/> |
|ReturnTypeDescriptorName  <br/> |Необязательное.  <br/> Это рекомендуется. Вместо этого используйте **ReturnTypeDescriptorPath**.<br/> Тип атрибута: **String** <br/> |
|ReturnTypeDescriptorLevel  <br/> |Необязательное.  <br/> Это рекомендуется. Вместо этого используйте **ReturnTypeDescriptorPath**.<br/> Тип атрибута: **Integer** <br/> |
|ReturnTypeDescriptorPath  <br/> |Необязательное.  <br/> Точками путь **TypeDescriptor** связи. <br/> Тип атрибута: **String** <br/> |
|Имя  <br/> |Обязательный атрибут.  <br/> Имя связи.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |Необязательный атрибут.  <br/> Отображаемое имя по умолчанию для сопоставления.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Необязательный атрибут.  <br/> Указывает, используются ли часто этого сопоставления.  <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Элемент **LocalizedDisplayNames** Указывает список локализованные имена для сопоставления. <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Элемент Properties указывает свойства связи.  <br/> |
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Элемент **AccessControlList** указывает набор прав доступа для сопоставления. <br/> |
| [Элемент SourceEntity в элементе Association (схема BDCMetadata)](http://msdn.microsoft.com/library/19fb5f38-4e85-7fb0-2562-281b9a9ffbef%28Office.15%29.aspx) <br/> |Элемент **SourceEntity** указывает внешний тип контента источника в связь. <br/> |
| [Элемент DestinationEntity в элементе Association (схема BDCMetadata)](http://msdn.microsoft.com/library/15c53c3b-888d-67c7-af7d-ef36922eeebc%28Office.15%29.aspx) <br/> |Элемент **DestinationEntity** указывает внешний тип контента назначения в связь. <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элементы "экземпляры метода" в методе (схема BDCMetadata)](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |Элемент **MethodInstances**, которая содержит связь. <br/> |
   

## <a name="associationgroup-element"></a>Элемент AssociationGroup
<a name="bkmk_AssociationGroup"> </a>

Указывает **AssociationGroup**. **AssociationGroup**  это конструкция, связанных с ними **AssociationMethods**, связывает вместе. Например **GetOrdersForCustomer**, **GetCustomerForOrder**и **AssociateCustomerToOrder** являются все методы связи, которые работают на же отношение между клиентом и порядке.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    
 **AssociationGroup** должны быть определены в элементе сущности, которая является целевой **AssociationReferences**, не помечены как **Reverse**или источника **AssociationReferences**, помеченные как обратный.
  
    
    



```XML
<AssociationGroup Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </AssociationGroup>
```

В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Name** <br/> |Обязательный атрибут.  <br/> Имя **AssociationGroup**.  <br/> Тип атрибута: **String** <br/> |
|**DefaultDisplayName** <br/> |Необязательный атрибут.  <br/> Отображаемое имя по умолчанию **AssociationGroup**.  <br/> Тип атрибута: **String** <br/> |
|**IsCached** <br/> |Необязательный атрибут.  <br/> Указывает, используется ли **AssociationGroup** часто. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена **AssociationGroup**.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства **AssociationGroup**.  <br/> |
| [Элемент AssociationReference в AssociationGroup (схема BDCMetadata)](http://msdn.microsoft.com/library/e32c5267-53b0-9ff0-6e9a-1cb00d9f1d57%28Office.15%29.aspx) <br/> |**AssociationReference** из **AssociationGroup**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент AssociationGroups в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |Элемент **AssociationGroups**, содержащий этот **AssociationGroup**.  <br/> |
   

## <a name="associationgroups-element"></a>Элемент AssociationGroups
<a name="bkmk_AssociationGroups"> </a>

Указывает список элементов **AssociationGroup**.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<AssociationGroups></AssociationGroups>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |**AssociationGroup**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Внешний тип контента, с которым связана этот элемент **AssociationGroups**. <br/> |
   

## <a name="associationreference-element"></a>Элемент AssociationReference
<a name="bkmk_AssociationReference"> </a>

Задает **AssociationReference** **AssociationGroup**.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<AssociationReference EntityNamespace = "String" EntityName = "String" AssociationName = "String" Reverse = "Boolean"> </AssociationReference>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Пространство имен сущности  <br/> |Необязательный атрибут.  <br/> Пространство имен внешнего типа контента, где определяется **Association**. Если указан параметр **EntityName**, **EntityNamespace** является обязательным. <br/> Тип атрибута: **String** <br/> |
|EntityName  <br/> |Необязательный атрибут.  <br/> Имя внешнего типа контента, где определяется **Association**. Если указан параметр **EntityNamespace**, **EntityName** является обязательным. <br/> Тип атрибута: **String** <br/> |
|AssociationName  <br/> |Обязательный атрибут.  <br/> Имя **Association**.  <br/> Тип атрибута: **String** <br/> |
|Обратный  <br/> |Необязательный атрибут.  <br/> Указывает, что указанный **Association** имеет его источника и назначения на обратный. Это означает, что **Association** работает в обратном направлении, по сравнению с другими связей в одном **AssociationGroup**. Например если **AssociationGroup** ссылается на **Association** "GetOrdersForCustomer", возвращение порядок элементов для заданного элемента клиента, затем **AssociationGroup**  это в направлении клиента в порядке. Другие **AssociationReference**, создание ссылок на другой связи "GetCustomerForOrder", должны быть отмечены как обратный, из-за этого сопоставления в направлении заказов для клиента. <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |**AssociationGroup**, к которому принадлежит этот **AssociationReference**. <br/> |
   

## <a name="converttype-element"></a>Элемент ConvertType
<a name="bkmk_ConvertType"> </a>

Задает правило, которое требуется преобразовать тип данных значения данных в другой тип данных.
  
    
    
 **Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 Схема: **Schema:** BDCMetadata
  
    
    
Элемент Convert правило для преобразования типа данных значения данных в другой тип данных. Если правила применяются в порядке, это правило определяет тип данных значения данных для преобразования в тип данных, заданный атрибутом BDCType. Если правила применяются в обратном порядке, это правило определяет тип данных значения данных для преобразования в тип данных, заданный атрибутом **LOBType**. Например это правило можно указать преобразование значение даты, полученный из внешней системы, в языка и региональных параметров конфиденциальных строка, которая будет отображаться в конечном счете для пользователя, и преобразование обновленное значение для этой строки обратно в даты, совместимое с внешней системы.
  
    
    

> **Предупреждение:**
> **ConvertType** не поддерживает преобразование между **System.String** и **System.DateTime**не григорианский календарь. 
  
    
    




```XML
<ConvertType LOBType = "String" BDCType = "String"> </ConvertType>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|LOBType  <br/> |Обязательный атрибут.  <br/> Тип данных для преобразования значения в при правила применяются в обратном порядке.  <br/> Тип атрибута: **String** <br/> |
|BDCType  <br/> |Обязательный атрибут.  <br/> Тип данных для преобразования значения в при применении правила в порядке.  <br/> Тип атрибута: **String** <br/> |
|LOBLocale  <br/> |Необязательный атрибут.  <br/> Языковой стандарт данные, получаемые из внешней системы.  <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Interpretation в элементе TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |Правила, применяемые к данным, хранящимся в структуры данных, представленные в **TypeDescriptor**.  <br/> |
   

## <a name="defaultvalue-element"></a>Элемент DefaultValue
<a name="bkmk_DefaultValue"> </a>

Представляет значение по умолчанию.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<DefaultValue MethodInstanceName = "String" Type = "String"> </DefaultValue>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**MethodInstanceName** <br/> |Обязательный атрибут.  <br/> Имя **MethodInstance**, к которому применяется этот DefaultValue. <br/> Тип атрибута: **String** <br/> |
|**Type** <br/> | Обязательный атрибут. <br/>  Тип данных по умолчанию. <br/>  Ниже приведены допустимые значения для этого атрибута. <br/> **System.Int16** <br/> **System.Int32** <br/> **System.Int64** <br/> **System.Single** <br/> **System.Double** <br/> **System.Decimal** <br/> **System.Boolean** <br/> **System.Byte** <br/> **System.UInt16** <br/> **System.UInt32** <br/> **System.UInt64** <br/> **System.Guid** <br/> **System.String** <br/> **System.DateTime** <br/>  Любой другой тип serializable (например, где  `Type.IsSerializable == true`)  <br/>  Тип атрибута: **String** <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент DefaultValues в элементе TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx)||
   

## <a name="defaultvalues-element"></a>Элемент DefaultValues
<a name="bkmk_DefaultValues"> </a>

Задает список **DefaultValues** **TypeDescriptor**.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<DefaultValues></DefaultValues>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент DefaultValue в элементе DefaultValues (схема BDCMetadata)](http://msdn.microsoft.com/library/ddb67f64-6361-7b59-6724-4680484d585d%28Office.15%29.aspx) <br/> |Значение по умолчанию **TypeDescriptor** для **MethodInstance**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |**TypeDescriptor**, к которой относятся следующие **DefaultValues**. <br/> |
   

## <a name="destinationentity-element"></a>Элемент DestinationEntity
<a name="bkmk_DestinationEntity"> </a>

Определяет внешний тип контента назначения в **Association**.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<DestinationEntity Namespace = "String" Name = "String"> </DestinationEntity>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Namespace** <br/> |Обязательный атрибут.  <br/> Имя пространства имен сущности.  <br/> Тип атрибута: **String** <br/> |
|**Name** <br/> |Обязательный атрибут.  <br/> Имя конечной сущности.  <br/> Тип атрибута: **String** <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)||
   

## <a name="entities-element"></a>Элемент сущности
<a name="bkmk_Entities"> </a>

Указывает список внешних типов контента в внешней системы.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Entities></Entities>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Внешний тип контента в внешней системы.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Внешняя система.  <br/> |
   

## <a name="entity-element"></a>Элемент сущности
<a name="bkmk_Entity"> </a>

Указывает внешний тип контента.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Entity Namespace = "String" Version = "String" EstimatedInstanceCount = "Integer" DefaultOperationMode = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Entity>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Namespace** <br/> |Обязательный атрибут.  <br/> Пространство имен, которому принадлежит этот внешний тип контента.  <br/> Тип атрибута: **String** <br/> **Примечание**: пространство имен не должны содержать специальные знак звездочка " **\***«.           |
|**Version** <br/> |Обязательный атрибут.  <br/> Номер версии данного внешнего типа контента.  <br/> Тип атрибута: **String** <br/> **Осторожность:** При изменении модели BDC, необходимо увеличить номер версии внешнего типа контента. При изменении структуры внешнего типа контента, следует увеличить основной номер. Структурные изменения примеры Добавление поля **SpecificFinder** или изменение поле идентификатора. Если изменения не влияет на структуру внешнего типа контента, например при добавлении метода creator, изменение сведения о подключении или при изменении имена дескрипторов **бизнес-системам** и тип, необходимо изменить номер сборки и номер редакции.          |
|**EstimatedInstanceCount** <br/> |Необязательный атрибут.  <br/> Предполагаемое количество внешних элементов, содержащихся в во внешней системе.  <br/> Значение по умолчанию: 10000  <br/> Тип атрибута: **Integer** <br/> |
|**DefaultOperationMode** <br/> |Необязательный атрибут.  <br/> Задает поведение по умолчанию при взаимодействии с внешней системы во время создания, удаления, обновления или чтение внешних элементов.  <br/> Значение по умолчанию: по умолчанию  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>Оперативный режим</p></td><td><p>Кэшированные внешние элементы для всех операций обхода и напрямую взаимодействовать с внешней системы.</p></td></tr><tr><td><p>Кэширования данных</p></td><td><p>Выполните <b>Создание</b>, <b>Чтение</b>, <b>обновление</b> и <b>Удаление</b> операций непосредственно с внешним кэшированные элементы. Для операций <b>чтения</b> если запрошенные внешние элементы в кэше, используйте внешние элементы в кэше. В противном случае обход кэша для получения внешних элементов из внешней системы и поместить его в кэш для дальнейшего использования. </p></td></tr><tr><td><p>Автономный режим</p></td><td><p>Выполните <b>Создание</b>, <b>Чтение</b>, <b>обновление</b> и <b>Удаление</b> операций с кэшированные внешние элементы.</p></td></tr><tr><td><p>Значение по умолчанию</p></td><td><p>Используйте системы по умолчанию. При этом используется режим кэширования, если среда поддерживает кэширование внешние элементы.</p></td></tr></tbody></table>|
|Name  <br/> |Обязательный атрибут.  <br/> Имя внешнего типа контента.  <br/> Тип атрибута: **String** <br/> **Примечание**: имя внешнего типа контента не должны содержать специальные знак звездочка " **\***«.           |
|DefaultDisplayName  <br/> |Необязательный атрибут.  <br/> По умолчанию отображаемое имя внешнего типа контента.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Необязательный атрибут.  <br/> Указывает, будет ли часто используемые этот внешний тип контента. Если параметр имеет значение true, Служба подключения к бизнес-данным (BDC) будет кэшировать этот внешний тип контента в памяти.<br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованное имя данного внешнего типа контента.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства данного внешнего типа контента.  <br/> |
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Список управления доступом (ACL) этого внешнего типа контента.  <br/> |
| [Элемент Identifiers в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |Идентификаторы внешнего типа контента.  <br/> |
| [Элемент Methods в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |Методы внешнего типа контента.  <br/> |
| [Элемент AssociationGroups в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |Связь группы внешнего типа контента.  <br/> |
| [Элемент Actions в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |Действия внешнего типа контента.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Entities в LobSystem (схема BDCMetadata)](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |Список внешних типов контента в этом внешней системы.  <br/> |
   

## <a name="filterdescriptor-element"></a>Элемент FilterDescriptor
<a name="bkmk_FilterDescriptor"> </a>

Задает дескриптор фильтра для метода.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<FilterDescriptor Type = "String" FilterField = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </FilterDescriptor>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Тип  <br/> |Обязательный атрибут.  <br/> Тип дескриптора фильтра.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>Limit</p></td><td><p>Используется при запросе внешние системы и значения, из которых можно интерпретации ограничение на количество внешние элементы **экземпляры сущностей** , которые возвращаются при вызове метода, к которому он принадлежит.</p></td></tr><tr><td><p>PageNumber</p></td><td><p /></td></tr><tr><td><p>Wildcard</p></td><td><p>Используется при запросе внешней системы. Его значение представляет шаблон регулярных и подстановочных знаков, который является, с которым сравнивается значение отдельного поля set **EntityInstances**. Внешняя система возвращает только тех **EntityInstances**, значения поля соответствуют заданному шаблону. </p></td></tr><tr><td><p>UserContext</p></td><td><p>Используется при запросе внешней системы. В качестве значения этого свойства любым клиентским приложением может автоматически задаваться удостоверение пользователя, вызывающего внешнюю систему. В дальнейшем это значение может использоваться внешней системой для авторизации и фильтрации возвращаемых результатов.</p></td></tr><tr><td><p>UserCulture</p></td><td><p /></td></tr><tr><td><p>Username</p></td><td><p /></td></tr><tr><td><p>Password</p></td><td /></tr><tr><td><p>LastId</p></td><td /></tr><tr><td><p>SsoTicket</p></td><td /></tr><tr><td><p>UserProfile</p></td><td><p>Используется при запросе внешней системы. Для получения значения этого свойства необходимо проверить текущий профиль пользователя. Это значение используется внешней системой для фильтрации возвращаемых результатов.</p></td></tr><tr><td><p>Comparison</p></td><td><p>Используется при запросе внешней системы. Во внешней системе возможно сравнение значения атрибута **ComparisonFilter** со значением отдельного поля в наборе элементов **EntityInstances**. В этом случае возвращаются только те элементы **EntityInstances**, для которых значения поля прошли проверку сравнением. </p></td></tr><tr><td><p>Временная метка</p></td><td /></tr><tr><td><p>Input</p></td><td><p>Используется при вызове операции во внешней системе. Во внешней системе значение атрибута **InputFilter** может использоваться в качестве дополнительных аргументов операции.</p></td></tr><tr><td><p>Output</p></td><td><p>Используется при вызове операции во внешней системе. Дополнительные результаты операции, которые недоступны для получения с помощью атрибута **ReturnTypeDescriptor**, извлекаются в качестве значения атрибута **InputOutputFilter**. </p></td></tr><tr><td><p>InputOutput</p></td><td><p>Используется при вызове операции во внешней системе. Значение атрибута **InputOutputFilter** может использоваться во внешней системе в качестве дополнительных аргументов операции. Дополнительные результаты операции, которые недоступны для получения с помощью атрибута **ReturnTypeDescriptor**, извлекаются в качестве значения атрибута **InputOutputFilter**. </p></td></tr><tr><td><p>Batching</p></td><td /></tr><tr><td><p>BatchingTermination</p></td><td /></tr><tr><td><p>ActivityId</p></td><td><p>Атрибут **ActivityId** используется при вызове операции внешней системы. Этому атрибуту присваивается значение, соответствующее идентификатору GUID, который представляет текущий контекст операции. Если это значение недоступно, формируется случайный идентификатор GUID. В SharePoint Foundation 2010 в этом фильтре используется идентификатор **CorrelationID**. </p></td></tr></tbody></table>
|FilterField  <br/> |Необязательный.  <br/> Тип атрибута: **String** <br/> |
|Имя  <br/> |Обязательный атрибут.  <br/> Имя дескриптора фильтра.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |Необязательный атрибут.  <br/> Установленное по умолчанию отображаемое имя дескриптора фильтра.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Необязательный атрибут.  <br/> Задает частоту использования этого дескриптора фильтра. Если установлено значение **true**, в службе Служба подключения к бизнес-данным (BDC) выполняется кэширование этого дескриптора в памяти.<br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные отображаемые имена дескриптора фильтра.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства дескриптора фильтра.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент FilterDescriptors в элементе Method (схема BDCMetadata)](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |Список дескрипторов фильтра для метода.  <br/> |
   

## <a name="filterdescriptors-element"></a>Элемент FilterDescriptors
<a name="bkmk_FilterDescriptors"> </a>

Задает список дескрипторов фильтра для метода.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<FilterDescriptors></FilterDescriptors>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент FilterDescriptor в элементе FilterDescriptors (схема BDCMetadata)](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> |Дескриптор фильтра.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Метод, которому принадлежит этот список дескрипторов фильтра.  <br/> |
   

## <a name="identifier-element"></a>Идентификатор элемента
<a name="bkmk_Identifier"> </a>

Задает идентификатор внешнего типа контента.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
> [!NOTE]
> 
> [!Примечание] Служба подключения к бизнес-данным (BDC) позволяет сопоставления идентификаторов для полей с типами данных допускает значение NULL. Тем не менее для основного идентификаторов BDC приведет к ошибке при **null**значение из этих идентификаторов. 
  
    
    




```XML
<Identifier TypeName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Identifier>
```

В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|TypeName  <br/> |Обязательный атрибут.  <br/> Тип данных значение, соответствующее идентификатору.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>System.Boolean</p></td><td><p>Бит.</p></td></tr><tr><td><p>System.Byte</p></td><td><p>Число в диапазоне от 0 до 255 включительно.</p></td></tr><tr><td><p>System.Char</p></td><td><p>Символ Юникода.</p></td></tr><tr><td><p>System.DateTime</p></td><td><p>Даты и времени от 12:00:00 полночь 1 января 1 Domini Anno (Common эра) в 11:59:59 P.M. 31 декабря, 9999 года (Common эра) включительно, с разрешением до 100 наносекунд.</p></td></tr><tr><td><p>System.Decimal</p></td><td><p>Число в диапазоне от отрицательные 79,228,162,514,264,337,593,543,950,335 для плюс 79,228,162,514,264,337,593,543,950,335 включительно.</p></td></tr><tr><td><p>System.Double</p></td><td><p>Двойной точности число от отрицательные 1, 79769313486232E308 для положительных 1, 79769313486232E308 включительно и положительного, отрицательные нулю, положительное infinity, отрицательные infinity и не является числовым (NaN). </p></td></tr><tr><td><p>System.Guid</p></td><td><p>ИДЕНТИФИКАТОР GUID.</p></td></tr><tr><td><p>System.Int16</p></td><td><p>Число в диапазоне от минус 32768 до положительное 32767 включительно.</p></td></tr><tr><td><p>System.Int32</p></td><td><p>Число от 0 до 4 294 967 295 включительно.</p></td></tr><tr><td><p>System.Int64</p></td><td><p>Число в диапазоне от 0 до 18446744073709551615 включительно.</p></td></tr><tr><td><p>System.SByte</p></td><td><p>Число в диапазоне от минус 128 до плюс 127 включительно.</p></td></tr><tr><td><p>System.Single</p></td><td><p>Запятой одинарной точности число в диапазоне минус 3, 402823E38 для положительных 3, 402823E38 включительно.</p></td></tr><tr><td><p>System.String</p></td><td><p>Строка текста в формате Юникода.</p></td></tr><tr><td><p>System.TimeSpan</p></td><td><p>Продолжительность от отрицательные 10675199 дней 2 часа 48 минут 5 секунд 477 миллисекунд 580 миллисекундах 800 наносекунд до положительное 10675199 дней 2 часа 48 минут 5 секунд 477 миллисекунд 580 включительно, в решение 100 наносекунд наносекунд 800 миллисекундах.</p></td></tr><tr><td><p>System.UInt16</p></td><td><p>Число в диапазоне от 0 до 65535 включительно.</p></td></tr><tr><td><p>System.UInt32</p></td><td><p>Число от 0 до 4 294 967 295 включительно.</p></td></tr><tr><td><p>System.UInt64</p></td><td><p>Число от 0 до 18,446,744,709,551,615 включительно.</p></td></tr></tbody></table>
|Name  <br/> |Обязательный атрибут.  <br/> Имя идентификатора.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |Необязательный атрибут.  <br/> По умолчанию отображаемое имя идентификатора.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Необязательный атрибут.  <br/> Указывает, используется ли этот идентификатор часто. Если параметр имеет значение **true**, Служба подключения к бизнес-данным (BDC) кэширует идентификатор в памяти.<br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованное имя идентификатора.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства идентификатора.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Identifiers в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |Список идентификаторов для внешнего типа контента.  <br/> |
   

## <a name="identifiers-element"></a>Элемент Identifiers
<a name="bkmk_Identifiers"> </a>

Задает список идентификаторов для внешнего типа контента.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Identifiers></Identifiers>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Identifier в элементе Identifiers (схема BDCMetadata)](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> |Задает идентификатор.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Внешний тип контента, которому принадлежит этот список идентификаторов.  <br/> |
   

## <a name="interpretation-element"></a>Элемент интерпретации
<a name="bkmk_Interpretation"> </a>

Задает правил, применяемых к данным, хранящимся в структуры данных, представленного **дескриптор типа**. Эти правила обычно указываются изменение значений данных, возвращаемых внешней системы для упрощения их представления в пользовательском интерфейсе. Когда значение получен из внешней системы, заданных правил должны применяться в порядке, в котором они указаны в элементе **Interpretation**. Первое правило должны быть установлены в значение данных, полученных из внешней системы; последовательных правила применяются к значению от приложения предыдущее правило. Когда значение отправляется для внешней системы, заданных правил должны применяться в обратном порядке, в котором они указаны в элементе **Interpretation**. Первое правило должны быть установлены в значение данных, полученных от пользователя. последовательных правила применяются к значению от приложения предыдущее правило.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Interpretation></Interpretation>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент ConvertType в элементе Interpretation (схема BDCMetadata)](http://msdn.microsoft.com/library/c474cf2c-b631-f3c9-daf1-f05d3e0d385f%28Office.15%29.aspx) <br/> |Элемент **ConvertType**, указывающее, преобразования типа данных в другой тип данных. <br/> |
| [Элемент NormalizeDateTime в элементе Interpretation (схема BDCMetadata)](http://msdn.microsoft.com/library/bbae3bfa-0754-d576-2bee-1ac0e8508a57%28Office.15%29.aspx) <br/> |Элемент **NormalizeDateTime**, который указывает преобразования представление даты и времени значения, полученные из внешней системы в другое представление. <br/> |
|NormalizeString  <br/> |Элемент **NormalizeString**, который указывает преобразования строковое представление значения, полученного из внешней системы в другое представление. <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |Элемент **TypeDescriptor**. <br/> |
   

## <a name="lobsystem-element"></a>Элемент бизнес-системы
<a name="bkmk_LobSystem"> </a>

Представляет внешний источник данных.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<LobSystem Type = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystem>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Тип  <br/> |Тип **LobSystem**.  <br/> Обязательный атрибут.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>База данных</p></td><td><p>Представленный внешний источник данных представляет собой базу данных.</p></td></tr><tr><td><p>DotNetAssembly</p></td><td><p>Представленный внешнего источника данных представляют собой набор классов .NET Framework.</p></td></tr><tr><td><p>WCF</p></td><td><p>Представленный внешнего источника данных является конечной точки службы WCF.</p></td></tr><tr><td><p>WebService</p></td><td><p>Представленный внешний источник данных  это веб-службы. Это был удален, вместо этого использовать WCF.</p></td></tr><tr><td><p>Пользовательский сервер</p></td><td><p>Представленный внешний источник данных имеет настраиваемого соединителя, реализованные для управления подключения и для передачи данных.</p></td></tr></tbody></table>|
|Name  <br/> |Имя **бизнес-системы**.  <br/> Обязательный атрибут.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |По умолчанию отображаемое имя **бизнес-системы**.  <br/> Необязательный.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Указывает, используются ли часто **бизнес-системы** . Если часто используемые службы подключения к бизнес-данных (BDC) кэширует **бизнес-системы**.  <br/> Необязательный атрибут.  <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена **LobSystem**.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Задает свойства **LobSystem**.  <br/> |
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Указывает список управления доступом (ACL) **LobSystem**.  <br/> |
| [Элемент Proxy в объекте LobSystem (схема BDCMetadata)](http://msdn.microsoft.com/library/8ec2e7b0-156f-ff4a-a87b-fe5764e4875b%28Office.15%29.aspx) <br/> |Прокси предоставленного пользователем идентичен, которая будет создана, если этот элемент не был задан.  <br/> |
| [Элемент LobSystemInstances в элементе LobSystem (схема BDCMetadata)](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |Задает внешнюю систему экземпляров данной внешней системы.  <br/> |
| [Элемент Entities в LobSystem (схема BDCMetadata)](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |Указывает внешних типов контента в этом внешней системы.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystems в модели (схема BDCMetadata)](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |Задает список внешних систем в этой модели.  <br/> |
   

## <a name="lobsysteminstance-element"></a>Элемент бизнес-системы
<a name="bkmk_LobSystemInstance"> </a>

Задает экземпляр внешней системы.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<LobSystemInstance Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystemInstance>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Имя  <br/> |Обязательный атрибут.  <br/> Имя экземпляра внешней системы.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |Необязательный атрибут.  <br/> По умолчанию отображаемое имя экземпляра внешней системы.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Необязательный атрибут.  <br/> Указывает, используется ли этот экземпляр внешней системы часто. Если параметр имеет значение **true**, Служба подключения к бизнес-данным (BDC) кэширует экземпляра внешней системы.<br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена данного экземпляра внешней системы.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства этого экземпляра внешней системы.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystemInstances в элементе LobSystem (схема BDCMetadata)](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |Список экземпляров внешней системы.  <br/> |
   

## <a name="lobsysteminstances-element"></a>Элемент LobSystemInstances
<a name="bkmk_LobSystemInstances"> </a>

Указывает список экземпляров внешней системы.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<LobSystemInstances></LobSystemInstances>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystemInstance в элементе LobSystemInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> |Экземпляр внешней системы.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Внешняя система.  <br/> |
   

## <a name="lobsystems-element"></a>Элемент бизнес-системам
<a name="bkmk_LobSystems"> </a>

Указывает список элементов **LobSystem** модели.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<LobSystems></LobSystems>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Элемент **LobSystem**, указывающее, внешней системе. <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Model (схема BDCMetadata)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |Определение приложения (модели BDC).  <br/> |
   

## <a name="localizeddisplayname-element"></a>Элемент LocalizedDisplayName
<a name="bkmk_LocalizedDisplayName"> </a>

Локализованное имя.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<LocalizedDisplayName LCID = "Integer"> </LocalizedDisplayName>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Код языка  <br/> |Обязательный атрибут.  <br/> Идентификатор код языка (LCID).  <br/> Тип атрибута: **Integer** <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Элемент **LocalizedDisplayNames**, содержащий этот **LocalizedDisplayName**.  <br/> |
   

## <a name="localizeddisplaynames-element"></a>Элемент LocalizedDisplayNames
<a name="bkmk_LocalizedDisplayNames"> </a>

Задает список локализованные имена **MetadataObject**.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<LocalizedDisplayNames></LocalizedDisplayNames>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayName в элементе LocalizedDisplayNames (схема BDCMetadata)](http://msdn.microsoft.com/library/93fb80ef-6347-b463-da90-4980d872678e%28Office.15%29.aspx) <br/> |Локализованное имя.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Model (схема BDCMetadata)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [Элемент LobSystemInstance в элементе LobSystemInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [Элемент Identifier в элементе Identifiers (схема BDCMetadata)](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| [Элемент FilterDescriptor в элементе FilterDescriptors (схема BDCMetadata)](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [Элемент Parameter в элементе Parameters (схема BDCMetadata)](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [Элемент TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| [Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| [Элемент Action в Actions (схема BDCMetadata)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [Элемент ActionParameter в элементе ActionParameters (схема BDCMetadata)](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="metadataobject-element"></a>Элемент метаданных (MetadataObject)
<a name="bkmk_MetadataObject"> </a>

 **Пространство имен**
  
    
    
 **Схема:**
  
    
    



```XML

```

В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    
 **Дочерние элементы**
  
    
    
 **Родительский элемент**
  
    
    

## <a name="method-element"></a>Элемент Method
<a name="bkmk_Method"> </a>

Задает метод для внешнего типа контента.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Method IsStatic = "Boolean" LobName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Method>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|IsStatic  <br/> |Необязательный атрибут.  <br/> Задает необходимость использования при выполнении этого метода внешнего элемента ( **EntityInstance**) в качестве контекста выполнения. Если присвоено значение **true**, этот метод является статическим и не требует отдельного элемента **EntityInstance** для определения контекста выполнения. Если присвоено значение **false**, метод является методом экземпляра и требует элемент **EntityInstance** для определения контекста выполнения. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
|LobName  <br/> |Необязательный атрибут.  <br/> Имя операции внешней системы, которая представлена этим методом.  <br/> Тип атрибута: **String** <br/> |
|Имя  <br/> |Обязательный атрибут.  <br/> Имя метода.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |Необязательный атрибут.  <br/> Установленное по умолчанию отображаемое имя метода.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Необязательный атрибут.  <br/> Задает частоту использования этого метода. Если установлено значение **true**, в службе Служба подключения к бизнес-данным (BDC) выполняется кэширование этого метода в памяти.<br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные отображаемые имена метода.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства метода.  <br/> |
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Список управления доступом (ACL) для этого метода.  <br/> |
| [Элемент FilterDescriptors в элементе Method (схема BDCMetadata)](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |Дескрипторы фильтра для этого метода.  <br/> |
| [Элемент Parameters в методе (схема BDCMetadata)](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |Параметры метода. Метод содержит не более одного возвращаемого параметра.  <br/> |
| [Элементы "экземпляры метода" в методе (схема BDCMetadata)](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |Экземпляры метода.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Methods в элементе Entity (схема BDCMetadata)](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |Список методов для внешнего типа контента.  <br/> |
   

## <a name="methodinstance-element"></a>Элемент экземпляра метода
<a name="bkmk_MethodInstance"> </a>

Указывает **MethodInstance**.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    
Следующих двух случаях в модели BDC привести  [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception%28v=vs.110%29.aspx) во время выполнения:
  
    
    

- Два **SpecificFinder** экземпляры метода, которые возвращают один и тот же набор полей.
    
  
- Два **SpecificFinder** экземпляры метода, у которых такое же число полей и использующих одинаковое число полей с другой экземпляр метода, такие как **Finder**.
    
  



```XML
<MethodInstance Type = "Strig" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </MethodInstance>
```

В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Type** <br/> |Обязательный атрибут.  <br/> Указывает тип **MethodInstance**.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>Служба поиска</p></td><td><p>Тип **MethodInstance**, который можно вызвать для возврата коллекции ноль или больше **EntityInstances** определенного **Entity**. входные данные **Finder** определяется **FilterDescriptors**, содержащиеся в **Method**, содержащий **Finder**. </p></td></tr><tr><td><p>SpecificFinder</p></td><td><p>Тип **MethodInstance**, который можно вызвать для возврата определенного **EntityInstance** определенных **Entity**, учитывая его **EntityInstanceId**. входные данные **SpecificFinder** определен и упорядоченные по **Identifiers**, связанных с **Entity**. </p></td></tr><tr><td><p>GenericInvoker</p></td><td><p>Тип **MethodInstance**, который можно вызывать для выполнения определенных задач из внешней системы. **GenericInvoker** ввода и вывода относится только к **Method**. </p></td></tr><tr><td><p>IdEnumerator</p></td><td><p>Тип **MethodInstance**, который можно вызвать для возврата значения **Field**, которые представляют идентификатор **EntityInstances** определенных **Entity**. Входные данные **IdEnumerator** определяется **FilterDescriptors**, содержащиеся в метод, который содержит **IdEnumerator** для получения списка идентификаторов, которые являются уникальные ключи для каждого объекта, который должен быть доступен для поиска. Этот экземпляр метода позволяет внешним данным поиска в SharePoint Server. </p></td></tr><tr><td><p>ChangedIdEnumerator</p></td><td><p>Тип **MethodInstance**, которые могут вызываться для извлечения **EntityInstanceIds** **EntityInstances**, были изменены за внешней системы времени.</p></td></tr><tr><td><p>DeletedIdEnumerator</p></td><td><p>Тип **MethodInstance**, которые могут вызываться для извлечения **EntityInstanceIds** **EntityInstances**, были удалены из внешней системы через указанное время.</p></td></tr><tr><td><p>Скалярные</p></td><td><p>**MethodInstance**, которое возвращает значение типа single, можно вызвать во внешней системе. Например можно использовать экземпляр скалярные метода для получения всех продаж, сделанных до определенной даты из внешней системы. **Entities** иметь экземпляры скалярные метод ноль или больше. </p></td></tr><tr><td><p>AccessChecker</p></td><td><p>Тип **MethodInstance**, который можно вызывать для получения разрешений, для которых есть вызывающего участника безопасности для каждого из коллекции **EntityInstances**, выявленные с указанным **EntityInstanceIds**.</p></td></tr><tr><td><p>Автор</p></td><td><p>Тип **MethodInstance**, которые могут вызываться для создания **EntityInstance**. Набор полей, которые необходимы для создания **EntityInstance** называется представление создателя. </p></td></tr><tr><td><p>Удаления</p></td><td><p>Тип **MethodInstance**, который можно вызывать для удаления **EntityInstance** с указанным **EntityInstanceId**.</p></td></tr><tr><td><p>Обновления</p></td><td><p>Тип **MethodInstance**, который можно вызывать для обновления **EntityInstance**, определяемую средством указанного **EntityInstanceId**. Набор полей, которые требуются для обновления **EntityInstance** называется Updater представления. Набор полей, значения которого должен передаваться перед их изменением называется PreUpdater представления. </p></td></tr><tr><td><p>StreamAccessor</p></td><td><p>Тип **MethodInstance**, которые могут вызываться для извлечения поля **EntityInstance** в виде поток данных в байтах.</p></td></tr><tr><td><p>Binarysecuritydescriptoraccessor используется</p></td><td><p>Тип **MethodInstance**, которые могут вызываться для извлечения последовательность байтов из внешней системы. Последовательность байтов системной описывается набор из участников безопасности и связанные разрешения, которые каждого участника безопасности для **EntityInstance** определила с указанным **EntityInstanceId**. </p></td></tr><tr><td><p>Метод BulkSpecificFinder</p></td><td><p>Тип **MethodInstance**, который можно вызвать для возврата набора определенных **EntityInstances** **Entity**набора соответствующего **EntityInstanceIds**.</p></td></tr><tr><td><p>BulkIdEnumerator</p></td><td><p>Тип **MethodInstance**, которые могут вызываться для извлечения минимальные сведения о внешние элементы, соответствующие заданным удостоверения. Для оптимизации синхронизации кэширования данных можно использовать этот экземпляр метода. Этот метод должен возвращать только удостоверения и сведения о версии внешних элементов, которые соответствуют заданным **Identities**, который вызывающему приложению можно сравнить с локальной версией для определения наличия изменений и если да, запросить измененных элементов внешнего обновлять кэшированные данные. </p></td></tr></tbody></table>
|**Значение по умолчанию** <br/> |Необязательное.  <br/> Указывает, является ли **MethodInstance** по умолчанию среди всех **MethodInstances**, совместно использующих типа внутри содержащей внешнего типа контента ( **Entity**).  <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**ReturnParameterName** <br/> |Необязательное.  <br/> Имя **Parameter**, содержащий **ReturnTypeDescriptor** из **MethodInstance**. Атрибут **Direction** **Parameter** должен быть атрибут **ParameterDirection** со значением **Out**, **InOut**или **Return**. <br/> Этот атрибут должен быть указан для всех типов **MethodInstances** за исключением **GenericInvoker**, **Creator**, **Deleter**и **Updater**.  <br/> Тип атрибута: **String** <br/> |
|**ReturnTypeDescriptorLevel** <br/> |Необязательное.  <br/> Это рекомендуется. Вместо этого используйте **ReturnTypeDescriptorPath**.<br/> Тип атрибута: **Integer** <br/> |
|**ReturnTypeDescriptorPath** <br/> |Необязательное.  <br/> Точками путь **TypeDescriptor** связи. <br/> Тип атрибута: **String** <br/> |
|**Name** <br/> |Обязательный атрибут.  <br/> Указывает имя **MethodInstance**.  <br/> Тип атрибута: **String** <br/> |
|**DefaultDisplayName** <br/> |Необязательный атрибут.  <br/> Задает отображаемое имя по умолчанию для **MethodInstance**.  <br/> Тип атрибута: **String** <br/> |
|**IsCached** <br/> |Необязательный атрибут.  <br/> Указывает, используется ли **MethodInstance** часто. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные отображаемые имена **MethodInstance**.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства **MethodInstance**.  <br/> |
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Списки управления доступом (ACL) из **MethodInstance**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элементы "экземпляры метода" в методе (схема BDCMetadata)](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |Элемент **MethodInstances**, содержащий этот **MethodInstance**.  <br/> |
   

## <a name="methodinstances-element"></a>Элемент "экземпляр метода"
<a name="bkmk_MethodInstances"> </a>

Указывает список связей и экземпляров метода.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<MethodInstances></MethodInstances>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |Связь.  <br/> |
| [Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |Экземпляр метода.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Метод, которому принадлежит этот экземпляр метода.  <br/> |
   

## <a name="methods-element"></a>Элемент Methods
<a name="bkmk_Methods"> </a>

Задает список методов для внешнего типа контента.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Methods></Methods>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Задает метод.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |Внешний тип контента, которому принадлежит этот список методов.  <br/> |
   

## <a name="model-element"></a>Элемент модели
<a name="bkmk_Model"> </a>

Задает корневой элемент, представляющий определения приложения. Модели определять внешние типы контента, содержащиеся в внешних приложений. 
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Model Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Model>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Имя  <br/> |Имя **Model**.  <br/> Обязательный атрибут.  <br/> Тип атрибута: **String** <br/> |
|DefaultDisplayName  <br/> |Отображаемое имя по умолчанию **Model**.  <br/> Необязательный атрибут.  <br/> Тип атрибута: **String** <br/> |
|IsCached  <br/> |Указывает, используется ли **Model** часто. Если установлено значение **true**, **Model** кэшируется с Служба подключения к бизнес-данным (BDC). <br/> Необязательный атрибут.  <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена **Model**.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства **Model**.  <br/> |
| [Элемент AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |Список управления доступом (ACL) из **Model**.  <br/> |
| [Элемент LobSystems в модели (схема BDCMetadata)](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |**LobSystems**, содержащиеся в этом **Model**.  <br/> |
   
 **Родительский элемент**
  
    
    
Нет
  
    
    

## <a name="normalizedatetime-element"></a>Элемент NormalizeDateTime
<a name="bkmk_NormalizeDateTime"> </a>

Задает правило, которое используется для преобразования представления значения даты и времени в другое представление. Например это правило можно указать преобразование значения, представленного в формате UTC в локальный часовой пояс. 
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<NormalizeDateTime LobDateTimeMode = "String"> </NormalizeDateTime>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**LobDateTimeMode** <br/> |Обязательный атрибут.  <br/> Указывает преобразования для применения.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>UTC</p></td><td><p>Значение, полученных из внешней системы  в формате UTC (время по Гринвичу). Если получено значение **Local**, он преобразуется в формате UTC. BDC отправляет UTC во внешней системе.</p></td></tr><tr><td><p>Local</p></td><td><p>Значение, полученных из внешней системы: **Local**. Если значение, полученных из внешней системы **Local**, его будут преобразованы в формате UTC. BDC отправляет **Local** во внешней системе. </p></td></tr><tr><td><p>Не определено.</p></td><td><p>Значение, отправленные с внешней системы не указан тип. BDC предполагается, что значение задается в формате UTC с помощью перезаписи вид быть UTC. BDC отправляет UTC значения как не указан тип во внешней системе.</p></td></tr></tbody></table>
|
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Interpretation в элементе TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |Элемент **Interpretation**, указывающее, правил, применяемых к данным, которые хранятся в структуры данных, представленного **TypeDescriptor**.  <br/> |
   

## <a name="normalizestring-element"></a>Элемент NormalizeString
<a name="bkmk_NormalizeString"> </a>

Задает параметр для метода.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML

```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
 **Дочерние элементы**
  
    
    
 **Родительский элемент**
  
    
    

## <a name="parameter-element"></a>Элемент параметра
<a name="bkmk_Parameter"> </a>

Задает параметр для метода.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Parameter Direction = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Parameter>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Direction  <br/> |Обязательный атрибут.  <br/> Направление параметра.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>Поддержка IPv6</p></td><td><p>Представленный **Parameter** является входным параметром.</p></td></tr><tr><td><p>Выходной</p></td><td><p>Параметр представленного является выходного параметра.</p></td></tr><tr><td><p>Вход</p></td><td><p>Параметр представленного является входных и выходных параметров. В C# они соответствуют «**ссылка**».</p></td></tr><tr><td><p>Возврат</p></td><td><p>Параметр представленного является возвращаемого параметра.</p></td></tr></tbody></table>
|**Name** <br/> |Обязательный атрибут.  <br/> Имя параметра.  <br/> Тип атрибута: **String** <br/> |
|**DefaultDisplayName** <br/> |Необязательный атрибут.  <br/> Отображаемое имя по умолчанию для параметра.  <br/> Тип атрибута: **String** <br/> |
|**IsCached** <br/> |Необязательный атрибут.  <br/> Указывает, используется ли **Parameter** часто. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена параметр.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства параметра.  <br/> |
| [Дескриптор типа](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> |Корневой дескриптор типа параметра.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Parameters в методе (схема BDCMetadata)](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |Элемент **Parameters**, содержащий этот параметр. <br/> |
   

## <a name="parameters-element"></a>Параметры элемента
<a name="bkmk_Parameters"> </a>

Указывает список параметров метода.
  
    
    

  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Parameters></Parameters>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Parameter в элементе Parameters (схема BDCMetadata)](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> |Параметр.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |Метод, к которой принадлежит этих параметров.  <br/> |
   

## <a name="properties-element"></a>Элемент Properties
<a name="bkmk_Properties"> </a>

Указывает список свойств объекта метаданных.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Properties></Properties>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Property в свойствах (схема BDCMetadata)](http://msdn.microsoft.com/library/2e6e8d5d-ef3b-c536-f3d1-ad2039b92c24%28Office.15%29.aspx) <br/> |Задает свойство.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Model (схема BDCMetadata)](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [Элемент LobSystemInstance в элементе LobSystemInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [Элемент Entity в элементе Entities (схема BDCMetadata)](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [Элемент Identifier в элементе Identifiers (схема BDCMetadata)](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [Элемент Method в элементе Methods (схема BDCMetadata)](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| [Элемент FilterDescriptor в элементе FilterDescriptors (схема BDCMetadata)](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [Элемент Parameter в элементе Parameters (схема BDCMetadata)](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [Дескриптор типа](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
| [Элемент TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| [Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| [Элемент Action в Actions (схема BDCMetadata)](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [Элемент ActionParameter в элементе ActionParameters (схема BDCMetadata)](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="property-element"></a>Элемент Property
<a name="bkmk_Property"> </a>

Указывает имя и тип свойства объекта метаданных.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Property Name = "String" Type = "String"> </Property>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Name** <br/> |Обязательный атрибут.  <br/> Задает имя свойства.  <br/> Тип атрибута: **String** <br/> |
|**Type** <br/> |Обязательный атрибут.  <br/> Указывает тип данных свойства.  <br/> Тип атрибута: **String** <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Элемент **Properties**, содержащий это свойство. <br/> |
   

## <a name="proxy-element"></a>Элемент прокси-сервера
<a name="bkmk_Proxy"> </a>

Прокси предоставленного пользователем идентичен, которая будет создана, если этот элемент не был задан. Используется для повышения производительности путем удаления нагрузка создания прокси-сервера. Чтобы указать настраиваемые бизнес-логики, который подключается к внешней системы, необходимо использовать сборки подключения .NET тип внешних систем.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Proxy></Proxy>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LobSystem в LobSystems (схема BDCMetadata)](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |Элемент **LobSystem**, к которому применяется этот прокси-сервера. <br/> |
   

## <a name="right-element"></a>Элемент вправо
<a name="bkmk_Right"> </a>

Разрешение доступа к одной записи управления доступом (ACE).
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<Right BdcRight = "String"> </Right>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|BdcRight  <br/> |Обязательный атрибут.  <br/> Разрешения, доступные для участника безопасности, удерживая вправо.  <br/> В следующей таблице приведен список возможных значений этого атрибута.  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p>Значение</p></th><th><p>Описание</p></th></tr></thead><tbody><tr><td><p>Нет</p></td><td><p>Нет разрешений.</p></td></tr><tr><td><p>Выполнение</p></td><td><p>Участник безопасности, представленного имеет разрешения на вызов **MethodInstance**.</p></td></tr><tr><td><p>Изменить</p></td><td><p>Представленный участника безопасности имеет разрешение на изменение атрибутов объекта метаданных или ее отношения с другими объектами метаданных.</p></td></tr><tr><td><p>SetPermissions</p></td><td><p>Представленный участника безопасности имеет разрешение на изменение набор разрешений для объекта метаданных.</p></td></tr><tr><td><p>SelectableInClients</p></td><td><p>Участника безопасности, представленного имеет разрешение на выбор эти права ссылается на объект метаданных. Если пользователь не имеет этого разрешения, объект метаданных не должна быть доступно для выбора.</p></td></tr></tbody></table>
|
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент AccessControlEntry в AccessControlList (схема BDCMetadata)](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |Элемент **AccessControlEntry**, содержащий эти права. <br/> |
   

## <a name="sourceentity-element"></a>Элемент SourceEntity
<a name="bkmk_SourceEntity"> </a>

Указывает источник внешнего типа контента из **Association**.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<SourceEntity Namespace = "String" Name = "String"> </SourceEntity>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|Пространство имен  <br/> |Обязательный атрибут.  <br/> Пространство имен внешнего типа контента, который является источником **Association**, содержащий данный элемент. <br/> Тип атрибута: String  <br/> |
|Имя  <br/> |Обязательный атрибут.  <br/> Имя внешнего типа контента, который является источником **Association**, содержащий данный элемент. <br/> Тип атрибута: **String** <br/> |
   
 **Дочерние элементы**
  
    
    
Нет
  
    
    
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |**Association**, содержащий данный элемент. <br/> |
   

## <a name="typedescriptor-element"></a>Элемент дескриптор типа
<a name="bkmk_TypeDescriptor"> </a>

Указывает **TypeDescriptor**.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<TypeDescriptor TypeName = "String" LobName = "String" IdentifierEntityNamespace = "String" IdentifierEntityName = "String" IdentifierName = "String" ForeignIdentifierAssociationName = "String" ForeignIdentifierAssociationEntityName = "String" ForeignIdentifierAssociationEntityNamespace = "String" AssociatedFilter = "String" IsCollection = "Boolean" ReadOnly = "Boolean" CreatorField = "Boolean" UpdaterField = "Boolean" PreUpdaterField = "Boolean" Significant = "Boolean" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </TypeDescriptor>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    


|**Атрибут**|**Описание**|
|:-----|:-----|
|**Имя типа** <br/> |Обязательный атрибут.  <br/> Идентификатор типа данных, представленного **TypeDescriptor**структуры данных.  <br/> Тип атрибута: **String** <br/> |
|**LobName** <br/> |Необязательный атрибут.  <br/> Структура данных, представленного **TypeDescriptor**. По умолчанию значение этого атрибута  имя **TypeDescriptor**. Например с именем «CN1A» структура данных системы бизнес-(LOB) можно представить в виде **TypeDescriptor** атрибутом **Name**, равное "Customer Name", если атрибут **LobName** этот **TypeDescriptor** равен "CN1A". <br/> Тип атрибута: **String** <br/> |
|**IdentifierEntityNamespace** <br/> |Необязательный атрибут.  <br/> Пространство имен внешнего типа контента, который содержит идентификатор, который ссылается на **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Identifier**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **IdentifierEntityName** и **IdentifierName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  это пространство имен внешнего типа контента, который содержит метод, содержащий параметр, содержащий **TypeDescriptor**. <br/> Тип атрибута: **String** <br/> |
|**Identifierentityname выполните следующие действия** <br/> |Необязательный атрибут.  <br/> Имя **Entity**, содержащий **Identifier**, который ссылается c **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Identifier**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **IdentifierEntityNamespace** и **IdentifierName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  имя **Entity**, содержащий **Method**, содержащий **Parameter**, содержащий **TypeDescriptor**. <br/> Тип атрибута: **String** <br/> |
|**IdentifierName** <br/> |Необязательный атрибут.  <br/> Имя **Identifier** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Identifier**, этот атрибут не должна быть указан. <br/> Тип атрибута: **String** <br/> |
|**ForeignIdentifierAssociationName** <br/> |Необязательный атрибут.  <br/> Имя **Association** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Association**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, атрибут **IdentifierName** также должен быть указан. Атрибут **ForeignIdentifierAssociationName** должен быть указан при **Identifier**, на который ссылается этот **TypeDescriptor** относится к **Association**и **Identifier** находится исходный **Entity** из **Association**. <br/> Тип атрибута: **String** <br/> |
|**ForeignIdentifierAssociationEntityName** <br/> |Необязательный атрибут.  <br/> Имя **Entity**, содержащий **Association** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Association**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **ForeignIdentifierAssociationEntityNamespace** и **ForeignIdentifierAssociationName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  имя **Entity**, содержащий **Method**, содержащий **Parameter**, содержащий **TypeDescriptor**. <br/> Тип атрибута: **String** <br/> |
|**ForeignIdentifierAssociationEntityNamespace** <br/> |Необязательный атрибут.  <br/> Пространство имен **Entity**, содержащий **Association** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Association**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **ForeignIdentifierAssociationEntityName** и **ForeignIdentifierAssociationName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  это пространство имен **Entity**, содержащий **Method**, содержащий **Parameter**, содержащий **TypeDescriptor**. <br/> Тип атрибута: **String** <br/> |
|**AssociatedFilter** <br/> |Необязательный атрибут.  <br/> Имя **FilterDescriptor**, связанный с **TypeDescriptor**. Если **TypeDescriptor** не связан с **FilterDescriptor** этого атрибута должно отсутствовать. <br/> Тип атрибута: **String** <br/> |
|**IsCollection** <br/> |Необязательный атрибут.  <br/> Указывает, представляет ли **TypeDescriptor** структуру данных single или коллекцию структур данных. <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**Только для чтения** <br/> |Необязательный атрибут.  <br/> Указывает, можно ли изменить данные, хранящиеся в структуре данных, представленного **TypeDescriptor**. Этот атрибут не должно быть указано, если значение атрибута **Direction** **Parameter**, содержащий **TypeDescriptor**  "In". <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**CreatorField** <br/> |Необязательный атрибут.  <br/> Указывает, представляет ли поле для **MethodInstances** типа **Creator**, содержащихся в **Method**, содержащий **Parameter**, содержащий **TypeDescriptor** **TypeDescriptor**.  <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**UpdaterField** <br/> |Необязательный атрибут.  <br/> Указывает, представляет ли поле для **MethodInstances** типа **Updater**, содержащихся в **Method**, содержащий **Parameter**, содержащий **TypeDescriptor** **TypeDescriptor**. Если этот атрибут является атрибутом **PreUpdaterField** не должен быть указан. <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**PreUpdaterField** <br/> |Необязательный атрибут.  <br/> Указывает, является ли структура данных, представленного **TypeDescriptor** хранит последнее значение данных, полученных из внешней системы поля для **MethodInstances** типа **Updater**. Если этот атрибут является атрибутом **UpdaterField** не должен быть указан. <br/> Значение по умолчанию: **false** <br/> Тип атрибута: **Boolean** <br/> |
|**Significant** <br/> |Необязательный атрибут.  <br/> Указывает, включены ли значения, хранящиеся в структуре данных, представленного в этом **TypeDescriptor** в расчете хэш-код или для сравнения значения, хранящиеся в структуры данных. Например, **TypeDescriptor**, представляющее фамилии клиента учитывается при определении ли записи был изменен и поэтому он имеет значение, тогда как **TypeDescriptor**, представляющий дату, на котором последние записи клиента изменения обычно не учитывается для определения, были ли изменены записи, и его не значительные. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
|**Name** <br/> |Обязательный атрибут.  <br/> Имя **TypeDescriptor**.  <br/> Тип атрибута: **String** <br/> **Примечание**: имя **дескриптор типа** не должно содержать специальные символы для косой черты («/»), period (".»), или открывающей скобки (» [»).          |
|**DefaultDisplayName** <br/> |Необязательный атрибут.  <br/> Отображаемое имя **TypeDescriptor**.  <br/> Тип атрибута: **String** <br/> |
|**IsCached** <br/> |Необязательный атрибут.  <br/> Указывает, используется ли **TypeDescriptor** часто. <br/> Значение по умолчанию: **true** <br/> Тип атрибута: **Boolean** <br/> |
   
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |Локализованные имена **TypeDescriptor**.  <br/> |
| [Элемент Properties в элементе MetadataObject (схема BDCMetadata)](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |Свойства **TypeDescriptor**.  <br/> Если **TypeDescriptor** имеет тип **System.String**, элемент **Properties** может содержать **Property** из типа **System.Int32** с атрибутом **Name**, равным **Size**. Значение **Property** указывает ожидаемый Максимальная длина строки значения структуры данных, описываемые в этом **TypeDescriptor**. <br/> |
| [Элемент Interpretation в элементе TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |Правила для данных, сохраненных в структуре данных, представленного **TypeDescriptor**.  <br/> |
| [Элемент DefaultValues в элементе TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx) <br/> |Значения по умолчанию **TypeDescriptor**.  <br/> |
| [Элемент TypeDescriptors в TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx) <br/> |Дочерние **TypeDescriptors** **TypeDescriptor**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент TypeDescriptors в TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx)||
   

## <a name="typedescriptors-element"></a>Элемент дескрипторы типов
<a name="bkmk_TypeDescriptors"> </a>

Задает список **TypeDescriptors** родительский объект TypeDescriptor.
  
    
    
 **Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`
  
    
    
 **Схема:** BDCMetadata
  
    
    



```XML
<TypeDescriptors></TypeDescriptors>
```

В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.
  
    
    
 **Атрибуты**
  
    
    
Нет
  
    
    
 **Дочерние элементы**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |**TypeDescriptor**.  <br/> |
   
 **Родительский элемент**
  
    
    


|**Элемент**|**Описание**|
|:-----|:-----|
| [Элемент TypeDescriptor (схема BDCMetadata)](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [Дескриптор типа](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
   

## <a name="see-also"></a>См. также
<a name="bkmk_Addres"> </a>


-  [Изменения в схеме модели BDC для SharePoint](changes-in-the-bdc-model-schema-for-sharepoint.md)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
