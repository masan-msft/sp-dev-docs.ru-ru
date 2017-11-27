---
title: "Создание поставщика утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8f3228ca-57fd-4253-a07d-abeb63298c58
ms.openlocfilehash: bcc75f6c67d1941197bf60ec07457d456149e1ff
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-a-claims-provider-in-sharepoint"></a><span data-ttu-id="b259b-102">Создание поставщика утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b259b-102">Create a claims provider in SharePoint</span></span>

<span data-ttu-id="b259b-103">Узнайте, как создать и реализовать поставщика утверждений SharePoint, который соответствует требованиям по приращению и отбору утверждений.</span><span class="sxs-lookup"><span data-stu-id="b259b-103">Learn how to create and implement a SharePoint claims provider that fulfills the requirements for claims augmentation and claims picking.</span></span>
<span data-ttu-id="b259b-104">Поставщик утверждений выдает утверждения и упаковывает утверждений в маркеры безопасности.</span><span class="sxs-lookup"><span data-stu-id="b259b-104">A claims provider issues claims and packages claims into security tokens.</span></span> <span data-ttu-id="b259b-105">Поставщик утверждений имеет две роли: приращения и комплектации.</span><span class="sxs-lookup"><span data-stu-id="b259b-105">A claims provider has two roles: augmentation and picking.</span></span>
  
    
    

<span data-ttu-id="b259b-p102">Расширение утверждения позволяет приложению для расширения дополнительных утверждений в маркер пользователя. Например с управлением Windows вход, службы каталогов Active Directory можно дополнить все группы безопасности пользователя в маркер пользователя Windows. С помощью на основе утверждений вход приложение управления (CRM) отношения клиента можно дополнить роли из базы данных CRM. Благодаря использованию этих утверждений в маркер пользователя, ресурсы авторизации для этих утверждений. То есть эти утверждения используются для определения, имеет ли конкретному пользователю доступ к определенным ресурсам. Утверждения могут отображаться в элементе управления средства выбора людей посредством выбора утверждений. Выбора позволяет утверждений приложения для отображения на основе утверждений в средстве выбора людей, например, при настройке параметров безопасности сайта SharePoint или службы SharePoint. Эта функция позволяет указывать поиска, разрешения и понятное отображаемое утверждений.</span><span class="sxs-lookup"><span data-stu-id="b259b-p102">Claims augmentation enables an application to augment additional claims into the user's token. For example, with Windows-based log-in, the Active Directory directory service can augment all of a user's security groups into the user's Windows token. With claims-based log-in, a customer relationship management (CRM) application can augment roles from a CRM database. By having these claims in the user's token, resources can be authorized against these claims. That is, these claims are used to determine whether a particular user has access to specific resources. Claims can be displayed in the people picker control through claims picking. Claims picking enables an application to surface claims in the people picker, for example, when configuring the security of a SharePoint site or SharePoint service. This functionality enables you to provide search, resolve, and friendly display of claims.</span></span>
  
    
    


> <span data-ttu-id="b259b-114">**Примечание:** "Выбор людей" с возможностью выбора утверждений иногда называется элемент управления Выбор утверждений.</span><span class="sxs-lookup"><span data-stu-id="b259b-114">**Note:** A people picker with claims picking functionality is sometimes referred to as a claims picker.</span></span> <span data-ttu-id="b259b-115">Дополнительные сведения см в [средстве выбора людей и поставщика утверждений планирования](http://technet.microsoft.com/en-us/library/gg602063.aspx).</span><span class="sxs-lookup"><span data-stu-id="b259b-115">For more information, see  [People picker and claims provider planning](http://technet.microsoft.com/en-us/library/gg602063.aspx).</span></span> 
  
    
    

<span data-ttu-id="b259b-116">Для создания поставщика утверждений сначала необходимо создать класс, производный от класса **SPClaimProvider**.</span><span class="sxs-lookup"><span data-stu-id="b259b-116">To write a claims provider, your first step is to create a class that derives from the **SPClaimProvider** class.</span></span>
> <span data-ttu-id="b259b-117">**Совет:** Пример кода и Дополнительные сведения о **SPClaimProvider** класс и его члены в разделе [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b259b-117">**Tip:** For a code example and more information about the **SPClaimProvider** class and its members, see [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .</span></span> <span data-ttu-id="b259b-118">Пошаговые руководства, советы и примеры кода, в разделе [утверждения и безопасность: технические статьи и примеры кода на MSDN](http://msdn.microsoft.com/library/f773fd4a-53ec-4656-bd08-e6c435e6f103%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b259b-118">For walkthroughs, tips, and code samples, see [Claims and Security: Technical articles and code samples on MSDN](http://msdn.microsoft.com/library/f773fd4a-53ec-4656-bd08-e6c435e6f103%28Office.15%29.aspx).</span></span> 
  
    
    


## <a name="required-implementations"></a><span data-ttu-id="b259b-119">Обязательные реализации</span><span class="sxs-lookup"><span data-stu-id="b259b-119">Required implementations</span></span>
<span data-ttu-id="b259b-120"><a name="SP15_HowToCreateClaimsProvider_ReqImplementations"> </a></span><span class="sxs-lookup"><span data-stu-id="b259b-120"></span></span>

<span data-ttu-id="b259b-121">Перечисленные ниже методы и свойства являются обязательными при создании поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="b259b-121">The following are required methods and properties when writing a claims provider.</span></span>
  
    
    

### <a name="required"></a><span data-ttu-id="b259b-122">Обязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="b259b-122">Required</span></span>

<span data-ttu-id="b259b-p105">Свойство  [Name](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.Name.aspx) является обязательным. Его имя должно быть уникальным в пределах фермы.</span><span class="sxs-lookup"><span data-stu-id="b259b-p105">The following  [Name](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.Name.aspx) property is a required property. The name should be unique across the farm.</span></span>
  
    
    

```cs

public abstract String Name
      
```


### <a name="required-for-claims-picker"></a><span data-ttu-id="b259b-125">Требуется для элемента управления "Выбор утверждений"</span><span class="sxs-lookup"><span data-stu-id="b259b-125">Required for claims picker</span></span>

<span data-ttu-id="b259b-p106">Утверждения могут отображаться в элементе управления "Выбор людей" при выборе утверждений. Следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) являются обязательными, если требуется реализовать выбор утверждений в элементе управления "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="b259b-p106">Claims can be displayed in the people picker control through claims picking. The following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class are required methods if you want to implement claim picking in the people picker control.</span></span>
  
    
    

```cs

protected abstract void FillSchema(SPProviderSchema schema);
     protected abstract void FillClaimTypes(List<String> claimTypes);
     protected abstract void FillClaimValueTypes(List<String> claimValueTypes);
     protected abstract void FillEntityTypes(List<String> entityTypes);

```


### <a name="required-for-claims-augmentation"></a><span data-ttu-id="b259b-128">Требуется для расширения утверждений</span><span class="sxs-lookup"><span data-stu-id="b259b-128">Required for claims augmentation</span></span>

<span data-ttu-id="b259b-p107">При добавлении дополнительных утверждений в маркер безопасности пользователя выполняется расширение утверждений. Если требуется расширить утверждения, необходимо реализовать следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b259b-p107">When you include additional claims in a user's security token, you are augmenting claims. If you want to augment claims, you must implement the following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsEntityInformation
      protected abstract void FillClaimsForEntity(Uri context, SPClaim entity, List<SPClaim> claims);

```


### <a name="required-for-displaying-hierarchy-on-the-left-pane-of-the-claims-picker"></a><span data-ttu-id="b259b-131">Требуется для отображения иерархии в левой панели элемента управления "Выбор утверждений"</span><span class="sxs-lookup"><span data-stu-id="b259b-131">Required for displaying hierarchy on the left pane of the claims picker</span></span>

<span data-ttu-id="b259b-132">Если требуется отобразить иерархию в левой панели элемента управления "Выбор утверждений", необходимо реализовать следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b259b-132">If you want to display hierarchy on the left pane of the claims picker, you must implement the following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsHierarchy
     protected abstract void FillHierarchy(Uri context, String[] entityTypes, String hierarchyNodeID, int numberOfLevels, bool includeEntityData, SPProviderHierarchyTree hierarchy);

```


### <a name="required-for-resolving-claims-in-the-type-in-control-of-the-claims-picker"></a><span data-ttu-id="b259b-133">Требуется для разрешения утверждений в элементе управления "Ввод" элемента управления "Выбор утверждений"</span><span class="sxs-lookup"><span data-stu-id="b259b-133">Required for resolving claims in the type-in control of the claims picker</span></span>

<span data-ttu-id="b259b-134">Если требуется разрешать утверждения с помощью элемента управления "Ввод" элемента управления "Выбор утверждений", необходимо реализовать следующие методы в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b259b-134">If you want to be able to resolve claims by using the type-in control of the claims picker, you must implement the following methods in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsResolve
     protected abstract void FillResolve(Uri context, String[] entityTypes, String resolveInput, List<PickerEntity> resolved);
     protected abstract void FillResolve(Uri context, String[] entityTypes, SPClaim resolveInput, List<PickerEntity> resolved);

```


### <a name="required-for-searching-for-claims-in-the-claims-picker"></a><span data-ttu-id="b259b-135">Требуется для поиска утверждений в средстве выбора утверждений</span><span class="sxs-lookup"><span data-stu-id="b259b-135">Required for searching for claims in the claims picker</span></span>

<span data-ttu-id="b259b-136">Если требуется реализовать функцию поиска в элементе управления "Выбор утверждений", необходимо реализовать следующее свойство и метод в классе  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b259b-136">If you want to be able to search for claims in the claims picker, you must implement the following property and method in the  [SPClaimProvider](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProvider.aspx) class.</span></span>
  
    
    

```cs

public abstract bool SupportsSearch
     protected abstract void FillSearch(Uri context, String[] entityTypes, String searchPattern, String hierarchyNodeID, int maxCount, SPProviderHierarchyTree searchTree);

```


## <a name="useful-helper-method"></a><span data-ttu-id="b259b-137">Полезный вспомогательный метод</span><span class="sxs-lookup"><span data-stu-id="b259b-137">Useful helper method</span></span>
<span data-ttu-id="b259b-138"><a name="SP15_HowToCreateClaimsProvider_UsefulHelperMethod"> </a></span><span class="sxs-lookup"><span data-stu-id="b259b-138"></span></span>

<span data-ttu-id="b259b-139">Для создания объектов  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) можно также использовать вспомогательный метод.</span><span class="sxs-lookup"><span data-stu-id="b259b-139">You can also implement a helper method to help you create  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) objects.</span></span>
  
    
    

### <a name="useful-helper-method-for-creating-spclaim-objects"></a><span data-ttu-id="b259b-140">Полезный вспомогательный метод для создания объектов SPClaim</span><span class="sxs-lookup"><span data-stu-id="b259b-140">Useful helper method for creating SPClaim objects</span></span>

<span data-ttu-id="b259b-141">В примере ниже показан вспомогательный метод для создания объектов  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b259b-141">The following is a helper method that you can implement to help you create  [SPClaim](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaim.aspx) objects.</span></span>
  
    
    

```cs

protected SPClaim CreateClaim(String claimType, String value, String valueType)
```


## <a name="additional-resources"></a><span data-ttu-id="b259b-142">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b259b-142">Additional resources</span></span>
<span data-ttu-id="b259b-143"><a name="SP15_HowToCreateClaimsProvider_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="b259b-143"></span></span>


-  [<span data-ttu-id="b259b-144">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b259b-144">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b259b-145">Входящих утверждений: вход в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b259b-145">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="b259b-146">Поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b259b-146">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b259b-147">Как: развернуть поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b259b-147">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

