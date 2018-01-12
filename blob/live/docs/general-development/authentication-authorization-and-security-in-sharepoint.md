---
title: "Проверка подлинности, авторизация и безопасность в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8734790c-eb75-4d78-9604-7cc23b33b693
ms.openlocfilehash: 86ef3bb99435bf9a7c5c02e46c4f5a09b2a22765
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="authentication-authorization-and-security-in-sharepoint"></a><span data-ttu-id="3143a-102">Проверка подлинности, авторизация и безопасность в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3143a-102">Authentication, authorization, and security in SharePoint</span></span>

## <a name="whats-new-in-sharepoint-for-authentication-authorization-and-security"></a><span data-ttu-id="3143a-103">Новые возможности SharePoint для проверки подлинности, авторизации и безопасности</span><span class="sxs-lookup"><span data-stu-id="3143a-103">What's new in SharePoint for authentication, authorization, and security</span></span>
<span data-ttu-id="3143a-104"><a name="SP15_AuthenticationAuthorizationSecurity_WhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="3143a-104"><a name="SP15_AuthenticationAuthorizationSecurity_WhatsNew"> </a></span></span>

<span data-ttu-id="3143a-105">Ниже приведены некоторые улучшения, добавленные в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="3143a-105">The following are some of the enhancements added to SharePoint:</span></span> 
  
    
    

- <span data-ttu-id="3143a-106">Вход пользователей</span><span class="sxs-lookup"><span data-stu-id="3143a-106">User sign-in</span></span>
    
  - <span data-ttu-id="3143a-p101">SharePoint поддерживает оба режима проверки подлинности: на основе утверждений и классический. По умолчанию в SharePoint установлена проверка подлинности на основе утверждений. Мы не рекомендуем использовать классический режим проверки подлинности. Им можно управлять только с помощью Windows PowerShell. Для многих функций SharePoint необходим режим проверки подлинности на основе утверждений.</span><span class="sxs-lookup"><span data-stu-id="3143a-p101">SharePoint continues to offer support for both claims and classic authentication modes. Claims authentication is the default authentication option in SharePoint. Classic-mode authentication is deprecated and can be managed only by using Windows PowerShell. A lot of features in SharePoint require claims-mode.</span></span> 
    
  
  - <span data-ttu-id="3143a-p102">Метод **MigrateUsers** из SharePoint 2010 не рекомендуется для миграции учетных записей. Вместо этого используйте новый командлет Windows PowerShell под названием `Convert-SPWebApplication`. Дополнительные сведение см. в статье  [Настройка проверки подлинности на основе утверждений для веб-приложения с классическим режимом проверки подлинности в SharePoint](http://technet.microsoft.com/en-us/library/gg251985.aspx).</span><span class="sxs-lookup"><span data-stu-id="3143a-p102">The **MigrateUsers** method from SharePoint 2010 is now deprecated, it's no longer the correct way to migrate accounts. To migrate accounts, use the new Windows PowerShell cmdlet called `Convert-SPWebApplication`. For more information see  [Migrate from classic-mode to claims-based authentication in SharePoint](http://technet.microsoft.com/en-us/library/gg251985.aspx).</span></span>
    
  
  - <span data-ttu-id="3143a-p103">Регистрировать поставщиков утверждений больше не требуется. Но необходимо предварительно настроить тип утверждения. Вы можете выбрать символы для типа утверждений. Упорядочивать типы утверждений необязательно.</span><span class="sxs-lookup"><span data-stu-id="3143a-p103">Requirement to register claims providers is eliminated. However, you do have to pre-configure claims type. You can choose the characters for the claim type and there is no enforcement on the ordering of claim types.</span></span>
    
  
  - <span data-ttu-id="3143a-117">SharePoint отслеживает файлы cookie **FedAuth** в новой службе распределенного кэша с помощью кэширования Windows Server AppFabric.</span><span class="sxs-lookup"><span data-stu-id="3143a-117">SharePoint tracks **FedAuth** cookies in the new distributed cache service using Windows Server AppFabric Caching.</span></span>
    
  
  - <span data-ttu-id="3143a-118">Расширенные возможности ведения журнала помогают устранить проблемы с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="3143a-118">Significantly more logging is provided to help troubleshoot authentication issues.</span></span> 
    
  
- <span data-ttu-id="3143a-119">Проверка подлинности служб и приложений</span><span class="sxs-lookup"><span data-stu-id="3143a-119">Services and app authentication</span></span>
    
  - <span data-ttu-id="3143a-p104">В SharePoint теперь можно создавать приложения для SharePoint. Надстройка SharePoint имеет собственное удостоверение и связано с субъектом безопасности, который называется субъектом приложения. Так же как пользователи и группы, субъект приложения имеет определенные разрешения и права.</span><span class="sxs-lookup"><span data-stu-id="3143a-p104">In SharePoint, you now have the ability to create apps for SharePoint. A SharePoint Add-in has its own identity and is associated with a security principal, called an app principal. Like users and groups, an app principal has certain permissions and rights.</span></span> 
    
  
  - <span data-ttu-id="3143a-p105">В SharePoint служба маркеров безопасности предоставляет маркеры доступа для проверки подлинности по протоколу S2S. Эта служба обеспечивает временный доступ к другим службам приложения, например Exchange Server 2013 и Microsoft Lync 2013, а также приложениям для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3143a-p105">In SharePoint, the server-to-server security token service (STS) provides access tokens for server-to-server authentication. The server-to-server STS enables temporary access tokens to access other application services, such as Exchange Server 2013 and Microsoft Lync 2013, and apps for SharePoint.</span></span>
    
  

## <a name="authentication-and-authorization"></a><span data-ttu-id="3143a-125">Проверка подлинности и авторизация</span><span class="sxs-lookup"><span data-stu-id="3143a-125">Authentication and authorization</span></span>
<span data-ttu-id="3143a-126"><a name="SP15_AuthenticationAuthorizationSecurity_AuthenticationAndAuthorization"> </a></span><span class="sxs-lookup"><span data-stu-id="3143a-126"><a name="SP15_AuthenticationAuthorizationSecurity_AuthenticationAndAuthorization"> </a></span></span>

<span data-ttu-id="3143a-p106">SharePoint поддерживает безопасность доступа пользователей на уровне веб-сайта, списка, папки списка или библиотеки и элемента. Управление безопасностью осуществляется на основе ролей на всех уровнях, обеспечивая согласованное управление безопасностью в масштабе всей платформы SharePoint с помощью единообразного пользовательского интерфейса на основе ролей и объектной модели для назначения разрешений в объектах. В результате в системе безопасности на уровне списка, папки или элемента реализована та же пользовательская модель, что и в системе безопасности на уровне веб-сайта, упрощая управление правами пользователей и групп в масштабе веб-сайта. SharePoint также поддерживает уникальные разрешения для папок и элементов, находящихся внутри списков и библиотек документов.</span><span class="sxs-lookup"><span data-stu-id="3143a-p106">SharePoint supports security for user access at the website, list, list or library folder, and item levels. Security management is role-based at all levels, providing coherent security management across the SharePoint platform with a consistent role-based user interface and object model for assigning permissions on objects. As a result, list-level, folder-level, or item-level security implements the same user model as website-level security, making it easier to manage user rights and group rights throughout a website. SharePoint also supports unique permissions on the folders and items contained within lists and document libraries.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="3143a-131">Сведения об авторизации, касающиеся надстроек SharePoint, см. в статье [Авторизация и проверка подлинности для надстроек в SharePoint](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3143a-131">[Note:](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx) For information about authorization related to SharePoint Add-ins, see  Authorization and authentication of SharePoint Add-ins.</span></span> 
  
    
    

<span data-ttu-id="3143a-p107">Авторизацией называется процесс, посредством которого SharePoint обеспечивает безопасность веб-сайтов, списков, папок или элементов с помощью определения того, какие пользователи могут выполнять отдельные действия над данным объектом. Процесс авторизации предполагает, что пользователь уже прошел проверку подлинности, которая является процессом, посредством которого SharePoint идентифицирует текущего пользователя. В SharePoint не реализована собственная система проверки подлинности или управления удостоверениями, но используются внешние системы проверки подлинности (Microsoft Windows или другие).</span><span class="sxs-lookup"><span data-stu-id="3143a-p107">Authorization refers to the process by which SharePoint provides security for websites, lists, folders, or items by determining which users can perform specific actions on a given object. The authorization process assumes that the user has already been authenticated, which refers to the process by which SharePoint identifies the current user. SharePoint does not implement its own system for authentication or identity management, but instead relies on external systems, whether Windows authentication or non-Windows authentication.</span></span>
  
    
    
<span data-ttu-id="3143a-135">SharePoint поддерживает следующие типы проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="3143a-135">SharePoint supports the following types of authentication:</span></span>
  
    
    

- <span data-ttu-id="3143a-p108">**Windows:** поддерживаются все службы IIS и параметры интеграции проверки подлинности Windows, включая обычную проверку подлинности, дайджест-проверку подлинности подпись, сертификаты, NTLM и Kerberos. Проверка подлинности Windows позволяет службам IIS выполнять проверку подлинности для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3143a-p108">**Windows:** All Internet Information Services (IIS) and Windows authentication integration options, including Basic, Digest, Certificates, Windows NT LAN Manager (NTLM), and Kerberos are supported. Windows authentication allows IIS to perform the authentication for SharePoint.</span></span>
    
    <span data-ttu-id="3143a-138">Дополнительные сведения о входе в SharePoint с помощью режима утверждений Windows см. в статье [Входящие утверждения. Вход в SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-138">For information about signing in to SharePoint by using Windows claims mode, see  [Incoming claims: Signing into SharePoint](incoming-claims-signing-into-sharepoint.md).</span></span>
    
    > <span data-ttu-id="3143a-139">
      >    **Важно!** Сведения о задержке олицетворения пользователя см. в статье [Устранение задержки олицетворения вызывающего пользователя](http://msdn.microsoft.com/en-us/library/ff407852.aspx).</span><span class="sxs-lookup"><span data-stu-id="3143a-139">**Important:** For information about suspending impersonation, see [Avoid suspending impersonation of the calling user](http://msdn.microsoft.com/en-us/library/ff407852.aspx).</span></span> 
- <span data-ttu-id="3143a-p109">**Формы ASP.NET:** поддерживается система управления удостоверениями, не относящаяся к Windows, в которой используется подключаемая система проверки подлинности на основе форм ASP.NET. Этот режим позволяет SharePoint работать с разными системами управления удостоверениями, включая внешне определенные группы или роли, такие как протокол LDAP и упрощенные системы управления удостоверениями базы данных. Проверка подлинности на основе форм позволяет платформе ASP.NET выполнять проверку подлинности для SharePoint, часто включая перенаправление на страницу входа. В SharePoint формы ASP.NET поддерживаются только в режиме проверки подлинности на основе утверждений. Поставщик форм должен быть зарегистрирован в веб-приложении, в котором настроена работа с утверждениями.</span><span class="sxs-lookup"><span data-stu-id="3143a-p109">**ASP.NET Forms:** A non-Windows identity management system that uses the pluggable ASP.NET forms-based authentication system is supported. This mode enables SharePoint to work with a variety of identity management systems, including externally defined groups or roles such as Lightweight Directory Access Protocol (LDAP) and light-weight database identity management systems. Forms authentication allows ASP.NET to perform the authentication for SharePoint, often involving a redirect to a log-on page. In SharePoint, ASP.NET forms are supported only under claims authentication. A forms provider must be registered within a web application that is configured for claims.</span></span>
    
    <span data-ttu-id="3143a-145">Сведения о входе в SharePoint с помощью членства в ASP.NET и пассивного входа на основе ролей см. в статье [Входящие утверждения. Вход в SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-145">For information about signing in to SharePoint by using ASP.NET membership and role passive sign-in, see  [Incoming claims: Signing into SharePoint](incoming-claims-signing-into-sharepoint.md).</span></span>
    
  

> [!NOTE]
> <span data-ttu-id="3143a-146">SharePoint не поддерживает работу с поставщиком членства с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="3143a-146">Note: SharePoint does not support working with a case-sensitive membership provider.</span></span> <span data-ttu-id="3143a-147">SharePoint использует хранилище SQL без учета регистра для всех пользователей в базе данных независимо от поставщика членства.</span><span class="sxs-lookup"><span data-stu-id="3143a-147">It uses case-insensitive SQL storage for all users in the database, regardless of the membership provider.</span></span> 
  
    
    


## <a name="claims-based-identity-and-authentication"></a><span data-ttu-id="3143a-148">Удостоверение и проверка подлинности на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="3143a-148">Claims-based identity and authentication</span></span>
<span data-ttu-id="3143a-149"><a name="SP15_AuthenticationAuthorizationSecurity_ClaimsBasedIdentity"> </a></span><span class="sxs-lookup"><span data-stu-id="3143a-149"><a name="SP15_AuthenticationAuthorizationSecurity_ClaimsBasedIdentity"> </a></span></span>

<span data-ttu-id="3143a-150">Удостоверение, основанное на утверждениях,  это модель удостоверений в SharePoint, поддерживающая такие возможности, как проверка подлинности пользователей систем на базе Windows и других ОС, несколько типов проверки подлинности, надежная проверка подлинности в режиме реального времени, широкий спектр типов участников и делегирование удостоверений пользователей между приложениями.</span><span class="sxs-lookup"><span data-stu-id="3143a-150">Claims-based identity is an identity model in SharePoint that includes features such as authentication across users of Windows-based systems and systems that are not Windows-based, multiple authentication types, stronger real-time authentication, a wider set of principal types, and delegation of user identity between applications.</span></span>
  
    
    
<span data-ttu-id="3143a-p111">Когда пользователь входит в SharePoint, его маркер проверяется и затем используется для входа в SharePoint. Маркер пользователя  это маркер безопасности, который выдается поставщиком утверждений. Поддерживаются такие режимы входа или доступа:</span><span class="sxs-lookup"><span data-stu-id="3143a-p111">When a user signs in to SharePoint, the user's token is validated and then used to sign in to SharePoint. The user's token is a security token issued by a claims provider. The following are supported sign-in or access modes:</span></span>
  
    
    

- <span data-ttu-id="3143a-154">режим утверждений Windows (по умолчанию);</span><span class="sxs-lookup"><span data-stu-id="3143a-154">Windows claims-mode sign-in (default)</span></span>
    
  
- <span data-ttu-id="3143a-155">режим пассивного входа SAML;</span><span class="sxs-lookup"><span data-stu-id="3143a-155">SAML passive sign-in mode</span></span>
    
  
- <span data-ttu-id="3143a-156">пассивный вход на основе членства и роли ASP.NET;</span><span class="sxs-lookup"><span data-stu-id="3143a-156">ASP.NET membership and role passive sign-in</span></span>
    
  
- <span data-ttu-id="3143a-157">Вход на основе классического режима Windows (не рекомендуется в этой версии)</span><span class="sxs-lookup"><span data-stu-id="3143a-157">Windows classic-mode sign-in (deprecated in this release)</span></span>
    
  

> [!NOTE]
> <span data-ttu-id="3143a-158">Дополнительные сведения о входе в SharePoint и разных режимах входа см. в статье [Входящие утверждения: вход в SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-158">[Note:](incoming-claims-signing-into-sharepoint.md) For more information about signing into SharePoint and the different sign-in modes, see  Incoming claims: Signing into SharePoint.</span></span> 
  
    
    

<span data-ttu-id="3143a-p112">В приложениях с поддержкой утверждений пользователь предоставляет удостоверение в виде набора утверждений. Одно утверждение может быть именем пользователя, другое  адресом электронной почты. Идея заключается в том, что внешняя система управления удостоверениями передает приложению все необходимые ему данные о пользователе вместе с каждым запросом наряду с криптографическим подтверждением того, что данные удостоверения, полученные приложением, поступают из надежного источника.</span><span class="sxs-lookup"><span data-stu-id="3143a-p112">When you build claims-aware applications, the user presents an identity to your application as a set of claims. One claim could be the user's name, another might be an email address. The idea here is that an external identity system is configured to give your application all the information that it needs about the user with each request, along with cryptographic assurance that the identity data received by your application comes from a trusted source.</span></span>
  
    
    
<span data-ttu-id="3143a-162">С этой моделью проще обеспечить единый вход и освободить ваше приложение от выполнения таких задач, как:</span><span class="sxs-lookup"><span data-stu-id="3143a-162">Under this model, single sign-on is much easier to achieve, and your application is no longer responsible for the following:</span></span>
  
    
    

- <span data-ttu-id="3143a-163">проверка подлинности пользователей;</span><span class="sxs-lookup"><span data-stu-id="3143a-163">Authenticating users</span></span>
    
  
- <span data-ttu-id="3143a-164">хранение пользовательских учетных записей и паролей;</span><span class="sxs-lookup"><span data-stu-id="3143a-164">Storing user accounts and passwords</span></span>
    
  
- <span data-ttu-id="3143a-165">обращение в каталог предприятия для поиска данных об удостоверении пользователя;</span><span class="sxs-lookup"><span data-stu-id="3143a-165">Calling to enterprise directories to look up user identity details</span></span>
    
  
- <span data-ttu-id="3143a-166">интеграция с системами удостоверений других платформ и компаний.</span><span class="sxs-lookup"><span data-stu-id="3143a-166">Integrating with identity systems from other platforms or companies</span></span>
    
  
<span data-ttu-id="3143a-p113">В этой модели ваше приложение принимает решения, связанные с удостоверениями, на основе утверждений, предоставленных пользователем. Такие решения могут варьироваться от простого использования имени пользователя в приложении, до разрешения пользователю обращаться к важным функциям и ресурсам приложения.</span><span class="sxs-lookup"><span data-stu-id="3143a-p113">Under this model, your application makes identity-related decisions based on claims supplied by the user. This could be anything from simple application personalization with the user's first name, to authorizing the user to access higher-value features and resources in your application.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="3143a-169">Дополнительные сведения об удостоверении, основанном на утверждениях, и поставщиках утверждений см. в статьях [Удостоверение, основанное на утверждениях, и концепции в SharePoint](claims-based-identity-and-concepts-in-sharepoint.md) и [Поставщик утверждений в SharePoint](claims-provider-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-169">[Note:](claims-based-identity-and-concepts-in-sharepoint.md) For more information about claims-based identity and claims providers, see  [Claims-based identity and concepts in SharePoint](claims-provider-in-sharepoint.md) and Claims provider in SharePoint.</span></span> 
  
    
    


## <a name="forms-based-authentication"></a><span data-ttu-id="3143a-170">Проверка подлинности на основе форм</span><span class="sxs-lookup"><span data-stu-id="3143a-170">Forms-based authentication</span></span>
<span data-ttu-id="3143a-171"><a name="SP15_AuthenticationAuthorizationSecurity_FormsBasedAuthentication"> </a></span><span class="sxs-lookup"><span data-stu-id="3143a-171"><a name="SP15_AuthenticationAuthorizationSecurity_FormsBasedAuthentication"> </a></span></span>

<span data-ttu-id="3143a-p114">Проверка подлинности на основе форм обеспечивает настраиваемое управление удостоверениями в SharePoint, добавляя поставщика членства, который определяет интерфейсы для идентификации и проверки подлинности отдельных пользователей, и диспетчера ролей, который определяет интерфейсы для группирования отдельных пользователей в логические группы или роли. В SharePoint поставщик членства должен добавить обязательный метод  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx). По имени пользователя система поставщика ролей возвращает список ролей, которым принадлежит пользователь.</span><span class="sxs-lookup"><span data-stu-id="3143a-p114">Forms-based authentication provides custom identity management in SharePoint by implementing a membership provider, which defines interfaces for identifying and authenticating individual users, and a role manager, which defines interfaces for grouping individual users into logical groups or roles. In SharePoint, a membership provider must implement the required  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx) method. Given a user name, the role provider system returns a list of roles to which the user belongs.</span></span>
  
    
    
<span data-ttu-id="3143a-p115">Поставщик членства отвечает за проверку учетных данных с помощью метода  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx) (теперь обязательного в SharePoint). Но фактический маркер пользователя создается службой маркеров безопасности. Она создает маркер пользователя на основе имени пользователя, подтвержденного поставщиком членства, и сведений о членстве в группах, связанных с именем пользователя, которые предоставляются поставщиком членства.</span><span class="sxs-lookup"><span data-stu-id="3143a-p115">The membership provider is responsible for validating the credential information by using the  [System.Web.Security.Membership.ValidateUser](http://msdn.microsoft.com/library/33f4af0b-75c0-4504-b90f-05e742e44a88.aspx) method (required now in SharePoint). But, the actual user token is created by the security token service (STS). The STS creates the user token from the user name validated by the membership provider and from the set of group memberships associated with the user name that are provided by the membership provider.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="3143a-178">Дополнительные сведения о службе токенов безопасности см. в статье [Удостоверение, основанное на утверждениях, и концепции в SharePoint](claims-based-identity-and-concepts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-178">[Note:](claims-based-identity-and-concepts-in-sharepoint.md) For more information about STS, see  Claims-based identity and concepts in SharePoint.</span></span> 
  
    
    

<span data-ttu-id="3143a-p116">Диспетчер ролей необязателен. Так, если пользовательская система проверки подлинности не поддерживает группы, то диспетчер ролей не требуется. SharePoint поддерживает один поставщик членства и один диспетчер ролей для каждой зоны URL-адресов ( [SPUrlZone](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPUrlZone.aspx) ). Роли форм ASP.NET не наследуют связанные с ними права. Вместо этого SharePoint назначает права ролям форм через политики и авторизацию. В SharePoint проверка подлинности на основе форм интегрирована с моделью удостоверений на основе утверждений. Если требуется обойти ограничение на одного поставщика ролей для одной зоны URL-адресов, можно воспользоваться поставщиками утверждений.</span><span class="sxs-lookup"><span data-stu-id="3143a-p116">The role manager is optional. If a custom authentication system does not support groups, a role manager is not necessary. SharePoint supports one membership provider and one role manager per URL zone ( [SPUrlZone](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.SPUrlZone.aspx) ). The ASP.NET forms roles have no inherent rights associated with them. Instead, SharePoint assigns rights to the forms roles through its policies and authorization. In SharePoint, the forms-based authentication is integrated with the claims-based identity model. If you need additional augmentation to bypass the limit of having one role provider per URL zone, you can rely on claims providers.</span></span>
  
    
    

> [!NOTE]
> <span data-ttu-id="3143a-186">Дополнительные сведения об удостоверении, основанном на утверждениях, и поставщиках утверждений см. в статьях [Удостоверение, основанное на утверждениях, и концепции в SharePoint](claims-based-identity-and-concepts-in-sharepoint.md) и [Поставщик утверждений в SharePoint](claims-provider-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-186">[Note:](claims-based-identity-and-concepts-in-sharepoint.md) For more information about claims-based identity and claims providers, see  [Claims-based identity and concepts in SharePoint](claims-provider-in-sharepoint.md) and Claims provider in SharePoint.</span></span> 
  
    
    

<span data-ttu-id="3143a-p117">При пассивном входе на основе и роли членства в ASP.NET вход выполняется путем перенаправления клиента на веб-страницу, на которой размещены элементы управления входа ASP.NET. После создания объекта удостоверения пользователя, SharePoint преобразует его в объект  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) (представление пользователя, основанное на утверждениях).</span><span class="sxs-lookup"><span data-stu-id="3143a-p117">In ASP.NET membership and role passive sign-in, the sign-in happens by redirecting the client to a web page where the ASP.NET log-in controls are hosted. After the identity object that represents a user identity is created, SharePoint converts it to a  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) object (which represents a claims-based representation of a user).</span></span>
  
> [!NOTE]
> <span data-ttu-id="3143a-189">Дополнительные сведения о входе в SharePoint см. в статье [Входящие утверждения: вход в SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3143a-189">[Note:](incoming-claims-signing-into-sharepoint.md) For more information about signing into SharePoint, see  Incoming claims: Signing into SharePoint.</span></span> 
  
    
    

<span data-ttu-id="3143a-p118">SharePoint использует стандартный интерфейс поставщика ролей ASP.NET для сбора сведений о группах текущего пользователя. Для проверки подлинности нет разницы между ролями и группами: это способ группирования пользователей в логические наборы для авторизации. Каждая роль ASP.NET обрабатывается службами SharePoint как доменная группа.</span><span class="sxs-lookup"><span data-stu-id="3143a-p118">SharePoint consumes the standard ASP.NET role provider interface to gather group information about the current user. For authentication purposes, roles and groups are the same thing: a way of grouping users into logical sets for authorization. Each ASP.NET role is treated as a domain group by SharePoint.</span></span> 
  
    
    
<span data-ttu-id="3143a-193">Дополнительные сведения о подключаемой платформе проверки подлинности, которую обеспечивает ASP.NET, см. в документации для разработчиков ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3143a-193">For information about the pluggable authentication framework provided by ASP.NET, see ASP.NET developer documentation.</span></span>
  
> [!NOTE]
> <span data-ttu-id="3143a-194">Дополнительные сведения о проверке подлинности на основе форм см. в статье [Проверка подлинности на основе форм в продуктах и технологиях SharePoint (часть 1): введение](http://msdn.microsoft.com/library/e5efd4d7-b369-49f0-a6f7-431d21daff20%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3143a-194">For more information about forms-based authentication, see [Forms authentication in SharePoint products and technologies (Part 1): Introduction](http://msdn.microsoft.com/library/e5efd4d7-b369-49f0-a6f7-431d21daff20%28Office.15%29.aspx).</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="3143a-195">См. также</span><span class="sxs-lookup"><span data-stu-id="3143a-195">See also</span></span>
<span data-ttu-id="3143a-196"><a name="SP15_AuthenticationAuthorizationSecurity_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3143a-196"><a name="SP15_AuthenticationAuthorizationSecurity_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="3143a-197">Авторизация, пользователи, группы и объектная модель в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3143a-197">Authorization, users, groups, and the object model in SharePoint</span></span>](authorization-users-groups-and-the-object-model-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3143a-198">Роли, наследования, несанкционированное получение прав и изменения паролей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3143a-198">Role, inheritance, elevation of privilege, and password changes in SharePoint</span></span>](role-inheritance-elevation-of-privilege-and-password-changes-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3143a-199">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3143a-199">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3143a-200">Удостоверение, основанное на утверждениях и концепций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3143a-200">Claims-based identity and concepts in SharePoint</span></span>](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3143a-201">Настройки, администрирования и ресурсы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3143a-201">Configuration, administration, and resources in SharePoint</span></span>](configuration-administration-and-resources-in-sharepoint.md)
    
  

