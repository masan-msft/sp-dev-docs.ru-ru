---
title: "Поставщик утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5918d5b6-5fd6-4f41-9473-a15b1491d056
ms.openlocfilehash: cd935e975f4c469079905c1afe242da790f33e2f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="claims-provider-in-sharepoint"></a><span data-ttu-id="47465-102">Поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="47465-102">Claims provider in SharePoint</span></span>

## <a name="claims-providers"></a><span data-ttu-id="47465-103">поставщики утверждений</span><span class="sxs-lookup"><span data-stu-id="47465-103">Claims providers</span></span>

<span data-ttu-id="47465-p101">Поставщик утверждений в SharePoint Server вопросы утверждений и пакеты утверждений на основе маркеров безопасности, то есть, в маркер пользователя. При входе пользователя в систему SharePoint Server, маркер пользователя проверка и затем используется для входа в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="47465-p101">A claims provider in SharePoint Server issues claims and packages claims into security tokens, that is, into the user's token. When a user signs in to SharePoint Server, the user's token is validated and then used to sign in to SharePoint.</span></span>
  
    
    
<span data-ttu-id="47465-106">Поставщик утверждений в SharePoint имеет две роли: приращения и комплектации.</span><span class="sxs-lookup"><span data-stu-id="47465-106">A claims provider in SharePoint has two roles: augmentation and picking.</span></span>
  
    
    

> <span data-ttu-id="47465-107">**Примечание:** Сведения о том, как создать поставщик утверждений можно [как: создать поставщик утверждений в SharePoint](how-to-create-a-claims-provider-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="47465-107">**Note:** For information about how to create a claims provider, see  [How to: Create a claims provider in SharePoint](how-to-create-a-claims-provider-in-sharepoint.md).</span></span> 
  
    
    


### <a name="claims-augmentation"></a><span data-ttu-id="47465-108">расширение утверждений</span><span class="sxs-lookup"><span data-stu-id="47465-108">Claims augmentation</span></span>

<span data-ttu-id="47465-p102">В роли приращения поставщика утверждений дополняет маркера пользователя с помощью утверждений во время входа позволяет приращения утверждений приложения для расширения дополнительных утверждений в маркер пользователя. Например с управлением Windows вход, службы каталогов Active Directory можно дополнить все группы безопасности пользователя в маркер пользователя Windows. С помощью на основе утверждений вход приложение управления (CRM) отношения клиента можно дополнить роли из базы данных CRM. Включить этих утверждений в маркер пользователя, ресурсы авторизации для этих утверждений. То есть эти утверждения используются для определения, имеет ли конкретному пользователю доступ к определенным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="47465-p102">In the augmentation role, a claims provider augments a user token with claims during sign-in. Claims augmentation enables an application to augment additional claims into the user's token. For example, with Windows-based log-in, the Active Directory directory service can augment all of a user's security groups into the user's Windows token. With claims-based log-in, a customer relationship management (CRM) application can augment roles from a CRM database. By including these claims in the user's token, resources can be authorized against these claims. That is, these claims are used to determine whether a particular user has access to specific resources.</span></span>
  
    
    

### <a name="claims-picking"></a><span data-ttu-id="47465-115">Выбора утверждений</span><span class="sxs-lookup"><span data-stu-id="47465-115">Claims picking</span></span>

<span data-ttu-id="47465-p103">В комплектации роли поставщика утверждений предоставляет список, разрешения, поиска и понятное отображаемое функциональные возможности утверждений в средстве выбора людей. Утверждений, комплектации позволяет приложению для отображения утверждений в средстве выбора людей, например при настройке безопасности сайта SharePoint или службы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="47465-p103">In the picking role, a claims provider provides listing, resolve, search, and friendly display of claims functionality in the people picker. Claims picking enables an application to surface claims in the people picker, for example when configuring the security of a SharePoint site or SharePoint service.</span></span> 
  
    
    

## <a name="claims-provider-use-scenarios"></a><span data-ttu-id="47465-118">Сценарии использования поставщика утверждений</span><span class="sxs-lookup"><span data-stu-id="47465-118">Claims provider use scenarios</span></span>

<span data-ttu-id="47465-p104">Поставщики утверждений, используемые для решения различных сценариев. Ниже приведены некоторые примеры сценариев использования поставщиков утверждений для решения.</span><span class="sxs-lookup"><span data-stu-id="47465-p104">Claims providers are used to solve different scenarios. The following are some examples of the scenarios that you can use claims providers to solve.</span></span>
  
    
    

### <a name="list-resolve-and-search"></a><span data-ttu-id="47465-121">Список, разрешения и поиска</span><span class="sxs-lookup"><span data-stu-id="47465-121">List, resolve, and search</span></span>

<span data-ttu-id="47465-p105">В SharePoint Server существует встроенных утверждений поставщиков, чтобы включить список, устранения и поиска для поставщиков встроенной проверки подлинности. Примеры поставщиков встроенной проверки подлинности: Windows Active Directory, проверку подлинности на основе форм и надежных издателей маркеров безопасности SAML Assertion Markup Language (), то есть, Служба маркеров безопасности (STS).</span><span class="sxs-lookup"><span data-stu-id="47465-p105">In SharePoint Server, there are built-in claims providers to enable list, resolve, and search for built-in authentication providers. Examples of built-in authentication providers are Windows Active Directory, forms-based authentication, and trusted Security Assertion Markup Language (SAML) token issuers—that is, a security token service (STS).</span></span> 
  
    
    
<span data-ttu-id="47465-p106">Для надежного поставщика маркеров SAML SharePoint Server не предоставляет список или поиска. Когда пользователь вводит некоторые значения, SharePoint Server всегда разрешает ее. Это означает, что при вводе adam@contoso.comпринимает значение "Выбор людей". Это, так как не стандартный, который указывает, как Служба маркеров безопасности (STS) разрешается, реализующий поиска или перечислены утверждения значения.</span><span class="sxs-lookup"><span data-stu-id="47465-p106">For a trusted SAML token issuer, SharePoint Server does not offer list or search. When a user enters some value, SharePoint Server always resolves it. This means that if you enter adam@contoso.com, the people picker accepts the value. This is because there is no industry standard that specifies how an STS resolves, implements search, or lists claim values.</span></span>
  
    
    
<span data-ttu-id="47465-p107">Пользователи могут переопределить встроенной требований для реализации настраиваемого поиска, разрешения имен и возможности списка. Это очень полезно в сценариях, как с помощью надежного поставщика маркеров SAML.</span><span class="sxs-lookup"><span data-stu-id="47465-p107">Users can override the built-in claims provider to implement custom search, name resolution, and list features. This is very useful in scenarios like using a trusted SAML token issuer.</span></span>
  
    
    

### <a name="authenticated-users-or-all-users-claims"></a><span data-ttu-id="47465-130">Пользователи, прошедшие проверку и утверждения всех пользователей</span><span class="sxs-lookup"><span data-stu-id="47465-130">Authenticated users or All Users claims</span></span>

<span data-ttu-id="47465-p108">В SharePoint Server существуют некоторые поставщики определенные встроенные утверждения, которые позволяют реализации поддержка понятия, такие как прошедших проверку пользователей. Это также известной как Все пользователи. Этот сценарий позволяет вам права для всех пользователей из заданного проверки подлинности поставщика.</span><span class="sxs-lookup"><span data-stu-id="47465-p108">In SharePoint Server, there are some specific built-in claims providers that enable implementation support for concepts like authenticated users. This is also known as an All Users claim. This scenario enables you to grant rights to all users from a given authentication provider.</span></span>
  
    
    

> <span data-ttu-id="47465-134">**Примечание:** Поставщик проверки подлинности может быть Windows Active Directory, проверку подлинности на основе форм или надежный поставщик маркеров SAML (то есть, STS).</span><span class="sxs-lookup"><span data-stu-id="47465-134">**Note:** An authentication provider can be a Windows Active Directory, forms-based authentication, or a trusted SAML token issuer (that is, an STS).</span></span> 
  
    
    

<span data-ttu-id="47465-p109">В SharePoint Server имеется также систем поставщика утверждений, которое добавляет некоторые внутренних утверждений, используемый службой таксономии. Например добавляет удостоверения и приложений пула учетной записи фермы.</span><span class="sxs-lookup"><span data-stu-id="47465-p109">In SharePoint Server, there is also a systems claims provider that adds some internal claims used by a taxonomy service. For example, it adds farm identity and application pool account.</span></span>
  
    
    

### <a name="adding-claims-to-an-original-token"></a><span data-ttu-id="47465-137">Добавление утверждений, исходного маркера</span><span class="sxs-lookup"><span data-stu-id="47465-137">Adding claims to an original token</span></span>

<span data-ttu-id="47465-p110">Некоторые из поставщиков утверждений встроенных также используется для добавления утверждений от исходного «маркер». Word «маркер» помечается в кавычках, так как некоторые поставщики проверки подлинности, например, на основе форм проверки подлинности (то есть, ASP.NET поставщики членства и ролей), не предоставляют реальных маркер. В этом случае представьте этот маркер с точки зрения понятий.</span><span class="sxs-lookup"><span data-stu-id="47465-p110">Some of the built-in claims providers are also used to add the claims from the original "token". The word "token" is marked in quotes because some authentication providers, for example, forms-based authentication (that is, ASP.NET membership and role providers), do not provide a real token. In this case, think of this token from a conceptual perspective.</span></span>
  
    
    
<span data-ttu-id="47465-p111">Может потребоваться добавить дополнительные утверждения исходный маркер утверждений пользователя. Для этого сценария может потребоваться поставщика утверждений. Например поставщика утверждений может потребоваться добавление роли SAP исходный маркер утверждений пользователя.</span><span class="sxs-lookup"><span data-stu-id="47465-p111">It might be necessary to add additional claims to a user's original claims token. For this scenario, a claims provider might be needed. For example, a claims provider might be needed to add SAP roles to a user's original claims token.</span></span>
  
    
    

### <a name="identity-not-from-original-token"></a><span data-ttu-id="47465-144">Удостоверение не от исходного маркера</span><span class="sxs-lookup"><span data-stu-id="47465-144">Identity not from original token</span></span>

<span data-ttu-id="47465-p112">Предположим, сценарий, где в системе имеет некоторые специальные требования для выбора людей и маркеров утверждений. В этом сценарии вы знаете удостоверения пользователя на основании уникальный идентификатор Passport (PUID) Microsoft .NET и исходного пользователя. Тем не менее сведения о пользователе поступившим не от исходного маркера пользователя; текст поступает из пользовательских Active Directory. Имеется также некоторые дополнительные группы Active Directory, которые пользователь может принадлежать, которые не находятся в исходного маркера пользователя (выданный Windows Live ID). В этом сценарии вы создавать поставщика утверждений для удовлетворения потребностей пользователя относящиеся к системе.</span><span class="sxs-lookup"><span data-stu-id="47465-p112">Assume a scenario where your system has some specific requirements for people picking and token claims. In this scenario, you know the identity of the user based on the Microsoft .NET Passport Unique ID (PUID) and the original user. However, the information about the user does not come from the original user token; it comes from your custom Active Directory. You also have some additional Active Directory groups that the user may belong to, which are not contained in the original user token (issued by Windows Live ID). In this scenario, you can build a claims provider to meet your system-specific needs.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="47465-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="47465-150">Additional resources</span></span>
<span data-ttu-id="47465-151"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="47465-151"></span></span>


-  [<span data-ttu-id="47465-152">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="47465-152">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="47465-153">Входящих утверждений: вход в SharePoint</span><span class="sxs-lookup"><span data-stu-id="47465-153">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="47465-154">Как: создать поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="47465-154">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="47465-155">Как: развернуть поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="47465-155">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

