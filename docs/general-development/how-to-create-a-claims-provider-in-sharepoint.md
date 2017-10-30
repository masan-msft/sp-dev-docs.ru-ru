---
title: "Как создать поставщик утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8f3228ca-57fd-4253-a07d-abeb63298c58
ms.openlocfilehash: 12d42c832cfe9741306adf78ba3d1bc4a708ac5d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-claims-provider-in-sharepoint"></a>Как: создать поставщик утверждений в SharePoint
Узнайте, как создать и реализовать поставщика утверждений SharePoint, который соответствует требованиям по приращению и отбору утверждений.
Поставщик утверждений выдает утверждения и упаковывает утверждений в маркеры безопасности. Поставщик утверждений имеет две роли: приращения и комплектации.
  
    
    

Расширение утверждения позволяет приложению для расширения дополнительных утверждений в маркер пользователя. Например с управлением Windows вход, службы каталогов Active Directory можно дополнить все группы безопасности пользователя в маркер пользователя Windows. С помощью на основе утверждений вход приложение управления (CRM) отношения клиента можно дополнить роли из базы данных CRM. Благодаря использованию этих утверждений в маркер пользователя, ресурсы авторизации для этих утверждений. То есть эти утверждения используются для определения, имеет ли конкретному пользователю доступ к определенным ресурсам. Утверждения могут отображаться в элементе управления средства выбора людей посредством выбора утверждений. Выбора позволяет утверждений приложения для отображения на основе утверждений в средстве выбора людей, например, при настройке параметров безопасности сайта SharePoint или службы SharePoint. Эта функция позволяет указывать поиска, разрешения и понятное отображаемое утверждений.
  
    
    


> **Примечание:** "Выбор людей" с возможностью выбора утверждений иногда называется элемент управления Выбор утверждений. Дополнительные сведения см в [средстве выбора людей и поставщика утверждений планирования](http://technet.microsoft.com/en-us/library/gg602063.aspx). 
  
    
    

Для создания поставщика утверждений сначала необходимо создать класс, производный от класса **SPClaimProvider**.
> **Совет:** Пример кода и Дополнительные сведения о **SPClaimProvider** класс и его члены в разделе [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) . Пошаговые руководства, советы и примеры кода, в разделе [утверждения и безопасность: технические статьи и примеры кода на MSDN](http://msdn.microsoft.com/library/f773fd4a-53ec-4656-bd08-e6c435e6f103%28Office.15%29.aspx). 
  
    
    


## <a name="required-implementations"></a>Обязательные реализации
<a name="SP15_HowToCreateClaimsProvider_ReqImplementations"> </a>

Перечисленные ниже методы и свойства являются обязательными при создании поставщика утверждений.
  
    
    

### <a name="required"></a>Обязательное свойство.

Свойство  [Name](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.Name.aspx) является обязательным. Его имя должно быть уникальным в пределах фермы.
  
    
    

```cs

public abstract String Name
      
```


### <a name="required-for-claims-picker"></a>Требуется для элемента управления "Выбор утверждений"

Утверждения могут отображаться в элементе управления "Выбор людей" при выборе утверждений. Следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) являются обязательными, если требуется реализовать выбор утверждений в элементе управления "Выбор людей".
  
    
    

```cs

protected abstract void FillSchema(SPProviderSchema schema);
     protected abstract void FillClaimTypes(List<String> claimTypes);
     protected abstract void FillClaimValueTypes(List<String> claimValueTypes);
     protected abstract void FillEntityTypes(List<String> entityTypes);

```


### <a name="required-for-claims-augmentation"></a>Требуется для расширения утверждений

При добавлении дополнительных утверждений в маркер безопасности пользователя выполняется расширение утверждений. Если требуется расширить утверждения, необходимо реализовать следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .
  
    
    

```cs

public abstract bool SupportsEntityInformation
      protected abstract void FillClaimsForEntity(Uri context, SPClaim entity, List<SPClaim> claims);

```


### <a name="required-for-displaying-hierarchy-on-the-left-pane-of-the-claims-picker"></a>Требуется для отображения иерархии в левой панели элемента управления "Выбор утверждений"

Если требуется отобразить иерархию в левой панели элемента управления "Выбор утверждений", необходимо реализовать следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .
  
    
    

```cs

public abstract bool SupportsHierarchy
     protected abstract void FillHierarchy(Uri context, String[] entityTypes, String hierarchyNodeID, int numberOfLevels, bool includeEntityData, SPProviderHierarchyTree hierarchy);

```


### <a name="required-for-resolving-claims-in-the-type-in-control-of-the-claims-picker"></a>Требуется для разрешения утверждений в элементе управления "Ввод" элемента управления "Выбор утверждений"

Если требуется разрешать утверждения с помощью элемента управления "Ввод" элемента управления "Выбор утверждений", необходимо реализовать следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .
  
    
    

```cs

public abstract bool SupportsResolve
     protected abstract void FillResolve(Uri context, String[] entityTypes, String resolveInput, List<PickerEntity> resolved);
     protected abstract void FillResolve(Uri context, String[] entityTypes, SPClaim resolveInput, List<PickerEntity> resolved);

```


### <a name="required-for-searching-for-claims-in-the-claims-picker"></a>Требуется для поиска утверждений в средстве выбора утверждений

Если требуется реализовать функцию поиска в элементе управления "Выбор утверждений", необходимо реализовать следующее свойство и метод в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .
  
    
    

```cs

public abstract bool SupportsSearch
     protected abstract void FillSearch(Uri context, String[] entityTypes, String searchPattern, String hierarchyNodeID, int maxCount, SPProviderHierarchyTree searchTree);

```


## <a name="useful-helper-method"></a>Полезный вспомогательный метод
<a name="SP15_HowToCreateClaimsProvider_UsefulHelperMethod"> </a>

Для создания объектов  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) можно также использовать вспомогательный метод.
  
    
    

### <a name="useful-helper-method-for-creating-spclaim-objects"></a>Полезный вспомогательный метод для создания объектов SPClaim

В примере ниже показан вспомогательный метод для создания объектов  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) .
  
    
    

```cs

protected SPClaim CreateClaim(String claimType, String value, String valueType)
```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_HowToCreateClaimsProvider_AdditionalResources"> </a>


-  [Удостоверение, основанное на основе утверждений в SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Входящих утверждений: вход в SharePoint](incoming-claims-signing-into-sharepoint.md)
    
  
-  [Поставщик утверждений в SharePoint](claims-provider-in-sharepoint.md)
    
  
-  [Как: развернуть поставщик утверждений в SharePoint](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

