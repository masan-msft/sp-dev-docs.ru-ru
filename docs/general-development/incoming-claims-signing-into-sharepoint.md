---
title: "Входящая подписывание на основе утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 08c687aa-e485-4269-aea8-4333da3588a5
ms.openlocfilehash: 982b9d2b6f65c73223ed4c317e631b017d87c980
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="incoming-claims-signing-into-sharepoint"></a><span data-ttu-id="e75c5-102">Входящих утверждений: вход в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e75c5-102">Incoming claims: Signing into SharePoint</span></span>

## <a name="signing-in-to-sharepoint"></a><span data-ttu-id="e75c5-103">Вход в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e75c5-103">Signing in to SharePoint</span></span>

<span data-ttu-id="e75c5-p101">При входе пользователя в систему SharePoint Server, маркер пользователя проверка и затем используется для входа в SharePoint. Маркер пользователя  это маркер безопасности, выданный поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p101">When a user signs in to SharePoint Server, the user's token is validated and then used to sign in to SharePoint. The user's token is a security token issued by a claims provider.</span></span>
  
    
    

> <span data-ttu-id="e75c5-106">**Примечание:** Сведения о проверки подлинности для одной фермы SharePoint и проверки подлинности утверждений между фермами SharePoint можно [планирование проверки подлинности на основе утверждений](http://technet.microsoft.com/en-us/library/cc262350.aspx) на сайте TechNet.</span><span class="sxs-lookup"><span data-stu-id="e75c5-106">**Note:** For information about claims authentication for a single SharePoint farm and inter-farm SharePoint claims authentication, see  [Plan for claims authentication](http://technet.microsoft.com/en-us/library/cc262350.aspx) on TechNet.</span></span>
  
    
    


### <a name="windows-claims-mode-sign-in"></a><span data-ttu-id="e75c5-107">Режим входа на основе утверждений Windows</span><span class="sxs-lookup"><span data-stu-id="e75c5-107">Windows claims mode sign-in</span></span>

<span data-ttu-id="e75c5-p102">В Windows утверждений режим входа на основе входа в происходит на запрос проверки подлинности встроенная проверка подлинности Windows с помощью согласование (NTLM/Kerberos). Однако после создания объекта  [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) (который представляет пользователя Windows), SharePoint Server преобразует объект [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) в объект [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) (который представляет представление на основе утверждений для пользователя).</span><span class="sxs-lookup"><span data-stu-id="e75c5-p102">In Windows claims mode sign-in, the sign-in happens with Integrated Windows authentication challenge by using Negotiate (NTLM/Kerberos). But, after the  [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) object (which represents a Windows user) is created, SharePoint Server converts the [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) object into a [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) object (which represents a claims-based representation of a user).</span></span>
  
    
    
<span data-ttu-id="e75c5-p103">затем SharePoint Server делает расширения утверждений и обрабатывает получившийся маркер, который был создан с SharePoint Server. Это означает, что некоторые функции (например, одним экземпляром поддержка для приложения-службы и пользовательских поставщиков утверждений) в SharePoint Server работы, даже если клиенты считаете, SharePoint Server в основном режиме входа в систему Windows. Интерфейс входа в режим утверждений Windows является встроенной по умолчанию для SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p103">SharePoint Server then does claims augmentation and handles the resulting token that is issued by SharePoint Server. This means that some features (for example, multitenant support for service applications and custom claims providers) in SharePoint Server work, even though the clients believe that SharePoint Server is in native Windows login mode. The Windows claims-mode sign-in experience is the built-in default for SharePoint Server.</span></span> 
  
    
    
<span data-ttu-id="e75c5-p104">Все типы входа в утверждений используют пассивный вход. Пассивный вход происходит с помощью Windows задачей, но со страницы отдельный вход, поступает через 302 перенаправления. Этот режим полезен, когда более одного способа включена, а пользователь должен выбрать между поставщиками утверждений, поддерживаемых. Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office. Некоторые клиенты Office выполните другой протокол.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p104">All claims sign-in types rely on passive sign-in. The passive sign-in happens by using Windows challenge, but from a separate login page that arrives through a 302 redirect. This mode is useful when more than one sign-in method is turned on and the user must choose between the supported claims providers. Win32 clients must support the forms-based authentication that is implemented in Office clients. Some Office clients follow a different protocol.</span></span>
  
    
    

### <a name="saml-passive-sign-in-mode"></a><span data-ttu-id="e75c5-118">режим пассивного входа SAML;</span><span class="sxs-lookup"><span data-stu-id="e75c5-118">SAML passive sign-in mode</span></span>

<span data-ttu-id="e75c5-p105">В разметке языка SAML (Security Assertion) пассивный вход, при входе пользователя в, клиента (это может быть веб-страницы) перенаправляется поставщика утверждений назначенного (например, Windows Live ID поставщика утверждений). После поставщика утверждений выполняет проверку подлинности пользователя, SharePoint Server принимает SAML маркеров доклад поставщика утверждений, обрабатывает маркер SAML, а затем дополняет утверждений.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p105">In Security Assertion Markup Language (SAML) passive sign-in, when a user signs in, the client (which might be a webpage) is redirected to the designated claims provider (for example, the Windows Live ID claims provider). After the claims provider authenticates the user, SharePoint Server takes the SAML token presented by the claims provider, processes the SAML token, and then augments the claims.</span></span>
  
    
    
<span data-ttu-id="e75c5-p106">Для поставщиков на основе SAML-утверждений поставщика утверждений как федерации Active Directory Services (ADFS) и поставщика утверждений Windows Live ID, вход с помощью SAML пассивный режим входа является единственным способом. SAML пассивный вход является модель SharePoint online удостоверения.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p106">For SAML-based claims providers, like the Active Directory Federation Services (ADFS) claims provider and the Windows Live ID claims provider, signing in by using the SAML passive sign-in mode is the only supported way. The SAML passive sign-in is the SharePoint online identity model.</span></span>
  
    
    

> <span data-ttu-id="e75c5-123">**Примечание:** SAML пассивный вход описывает процесс входа.</span><span class="sxs-lookup"><span data-stu-id="e75c5-123">**Note:** SAML passive sign-in describes the process of signing in.</span></span> <span data-ttu-id="e75c5-124">Когда вход для веб-приложения настроен на прием маркеров из поставщика доверенных входа в систему, этот тип входа называется SAML пассивный вход.</span><span class="sxs-lookup"><span data-stu-id="e75c5-124">When a sign-in for a web application is configured to accept tokens from a trusted login provider, this type of sign-in is called SAML passive sign-in.</span></span> <span data-ttu-id="e75c5-125">Поставщика доверенных входа в систему — это внешние (то есть, внешними по отношению к SharePoint) служба маркеров безопасности (STS), доверяющей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e75c5-125">A trusted login provider is an external (that is, external to SharePoint) security token service (STS) that SharePoint trusts.</span></span> 
  
    
    

<span data-ttu-id="e75c5-126">Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office.</span><span class="sxs-lookup"><span data-stu-id="e75c5-126">Win32 clients must support the forms-based authentication that is implemented in Office clients.</span></span>
  
    
    

### <a name="aspnet-membership-and-role-passive-sign-in"></a><span data-ttu-id="e75c5-127">пассивный вход с помощью членства ASP.NET и роли;</span><span class="sxs-lookup"><span data-stu-id="e75c5-127">ASP.NET membership and role passive sign-in</span></span>

<span data-ttu-id="e75c5-p108">В ASP.NET членства и ролей пассивный вход входа в происходит путем перенаправления клиента на веб-страницу, где размещены элементы управления ASP.NET в журнал. После создания объекта идентификатор, представляющий идентификатор пользователя, SharePoint Server преобразует его в объект  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) (который представляет представление на основе утверждений для пользователя).</span><span class="sxs-lookup"><span data-stu-id="e75c5-p108">In ASP.NET membership and role passive sign-in, the sign-in happens by redirecting the client to a webpage where the ASP.NET log-in controls are hosted. After the identity object that represents a user identity is created, SharePoint Server converts it to a  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) object (which represents a claims-based representation of a user).</span></span>
  
    
    
<span data-ttu-id="e75c5-p109">SharePoint Server то выполняет расширения утверждений. Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p109">SharePoint Server then does claims augmentation. Win32 clients must support the forms-based authentication that is implemented in Office clients.</span></span>
  
    
    

### <a name="windows-classic-mode-sign-in"></a><span data-ttu-id="e75c5-132">Классический режим входа Windows</span><span class="sxs-lookup"><span data-stu-id="e75c5-132">Windows classic mode sign-in</span></span>

<span data-ttu-id="e75c5-p110">Учетное классического режима Windows поддерживается в этой версии. В Windows классический режим входа на основе входа в происходит с запросом встроенная проверка подлинности с помощью согласование (NTLM/Kerberos). Выполняется без расширения утверждений, поэтому некоторые функции (например, одним экземпляром поддержка для приложения-службы и пользовательских поставщиков утверждений) не работают при входе пользователя в в этом режиме.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p110">The Windows classic mode sign-in is deprecated in this release. In Windows classic mode sign-in, the sign-in happens with the Integrated Windows authentication challenge by using Negotiate (NTLM/Kerberos). No claims augmentation is done, so some features (for example, multitenant support for service applications and custom claims providers) do not work when a user signs in by using this mode.</span></span>
  
    
    
<span data-ttu-id="e75c5-136">Некоторые приложения-службы может также потребоваться режим утверждений для некоторых функций.</span><span class="sxs-lookup"><span data-stu-id="e75c5-136">Some service applications may also require claims mode for some features.</span></span> 
  
    
    

### <a name="anonymous-access"></a><span data-ttu-id="e75c5-137">анонимный доступ;</span><span class="sxs-lookup"><span data-stu-id="e75c5-137">Anonymous access</span></span>

<span data-ttu-id="e75c5-p111">Можно включить анонимный доступ для веб-приложения. Администраторы сайтов в веб-приложении можно разрешить анонимный доступ. Если анонимные пользователи требуется получить доступ к защищенным ресурсам, они нажмите кнопку входа в систему, чтобы предоставить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p111">You can enable anonymous access for a web application. Administrators of sites within the web application can choose to allow anonymous access. If anonymous users want to gain access to secured resources, they can click a logon button to submit their credentials.</span></span> 
  
    
    
<span data-ttu-id="e75c5-p112">SharePoint Server то выполняет расширения утверждений. Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office.</span><span class="sxs-lookup"><span data-stu-id="e75c5-p112">SharePoint Server then does claims augmentation. Win32 clients must support the forms-based authentication that is implemented in Office clients.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="e75c5-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e75c5-143">Additional resources</span></span>
<span data-ttu-id="e75c5-144"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e75c5-144"></span></span>


-  [<span data-ttu-id="e75c5-145">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e75c5-145">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e75c5-146">Поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e75c5-146">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e75c5-147">Как: создать поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e75c5-147">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e75c5-148">Как: развернуть поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e75c5-148">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

