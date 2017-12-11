---
title: "Концепции и удостоверения, основанные на утверждениях, в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d96c7cf4-2e48-4223-a3c0-42368d079b74
ms.openlocfilehash: 45834f7699463a2ee849edc78e9c7d34166d3bbb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="claims-based-identity-and-concepts-in-sharepoint"></a><span data-ttu-id="60a47-102">Концепции и удостоверения, основанные на утверждениях, в SharePoint</span><span class="sxs-lookup"><span data-stu-id="60a47-102">Claims-based identity and concepts in SharePoint</span></span>

## <a name="claims-based-identity-model"></a><span data-ttu-id="60a47-103">Модели удостоверений на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="60a47-103">Claims-based identity model</span></span>

<span data-ttu-id="60a47-p101">При создании утверждения приложения пользователь представляет удостоверения для приложения как набор утверждений. Имя пользователя может иметь одно утверждение, другой может быть адресом электронной почты. В данном случае, что в системе внешних идентификаторов настроены для вашего приложения все сведения, необходимые о пользователя при каждом запросе, а также шифрования учетных данных, получаемых приложением, поступающие из надежного источника Software assurance.</span><span class="sxs-lookup"><span data-stu-id="60a47-p101">When you build claims-aware applications, the user presents an identity to your application as a set of claims. One claim could be the user's name, another might be an email address. The idea here is that an external identity system is configured to give your application all the information it needs about the user with each request, along with cryptographic assurance that the identity data received by your application comes from a trusted source.</span></span>
  
    
    
<span data-ttu-id="60a47-107">С этой моделью проще обеспечить единый вход и освободить ваше приложение от выполнения таких задач, как:</span><span class="sxs-lookup"><span data-stu-id="60a47-107">Under this model, single sign-on is much easier to achieve, and your application is no longer responsible for the following:</span></span>
  
    
    

- <span data-ttu-id="60a47-108">проверка подлинности пользователей;</span><span class="sxs-lookup"><span data-stu-id="60a47-108">Authenticating users</span></span>
    
  
- <span data-ttu-id="60a47-109">хранение пользовательских учетных записей и паролей;</span><span class="sxs-lookup"><span data-stu-id="60a47-109">Storing user accounts and passwords</span></span>
    
  
- <span data-ttu-id="60a47-110">обращение в каталог предприятия для поиска данных об удостоверении пользователя;</span><span class="sxs-lookup"><span data-stu-id="60a47-110">Calling to enterprise directories to look up user identity details</span></span>
    
  
- <span data-ttu-id="60a47-111">интеграция с системами удостоверений других платформ и компаний.</span><span class="sxs-lookup"><span data-stu-id="60a47-111">Integrating with identity systems from other platforms or companies</span></span>
    
  
<span data-ttu-id="60a47-p102">В этой модели приложение устанавливает связанные с идентификатором решения на основе заявок, предоставленные пользователем. Это может быть что-либо из личной настройки простое приложение с имя пользователя, для авторизации пользователя для доступа к выше функций значение и ресурсов в приложении.</span><span class="sxs-lookup"><span data-stu-id="60a47-p102">Under this model, your application makes identity-related decisions based on claims supplied by the user. This could be anything from simple application personalization with the user's first name, to authorizing the user to access higher value features and resources in your application.</span></span>
  
    
    
<span data-ttu-id="60a47-114">В следующих разделах представлены термины и понятия, которые помогут вам понять архитектура удостоверение, основанное на утверждениях.</span><span class="sxs-lookup"><span data-stu-id="60a47-114">The following sections introduce terminology and concepts to help you understand the claims-based identity architecture.</span></span>
  
    
    

### <a name="identity-a-set-of-attributes-that-describe-an-entity"></a><span data-ttu-id="60a47-115">Удостоверение: Набор атрибутов, определяющих сущности</span><span class="sxs-lookup"><span data-stu-id="60a47-115">Identity: A set of attributes that describe an entity</span></span>

<span data-ttu-id="60a47-116">IDENTITY  это набор атрибутов, определяющих пользователем или другой сущности, в систему, которая требуется для обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="60a47-116">Identity is a set of attributes that describe a user, or some other entity, in a system that you want to secure.</span></span>
  
    
    

### <a name="claim-a-piece-of-identity-information"></a><span data-ttu-id="60a47-117">Утверждение: Часть сведений об удостоверениях</span><span class="sxs-lookup"><span data-stu-id="60a47-117">Claim: A piece of identity information</span></span>

<span data-ttu-id="60a47-p103">Представьте утверждения как часть сведений об удостоверениях (например, имя, адрес электронной почты, срок хранения в или членство в роли продаж). Приложение получает дополнительные утверждения, тем больше вы знаете о пользователя. Они называются «утверждений» вместо "атрибуты", как обычно используется при описании каталогов предприятия, из-за метода доставки. В этой модели приложение не выполнять поиск атрибутов пользователя в каталоге. Вместо этого пользователь посылает утверждения для приложения, и приложение проверяет их. Каждый утверждения осуществляется поставщика и в утверждения только так же, как вы доверяете поставщика. Например доверять утверждения, сделанных с контроллера домена вашей компании, больше, чем вы доверяете утверждения, сделанные пользователем.</span><span class="sxs-lookup"><span data-stu-id="60a47-p103">Think of a claim as a piece of identity information (for example, name, email address, age, or membership in the Sales role). The more claims your application receives, the more you know about your user. These are called "claims" rather than "attributes," as is commonly used in describing enterprise directories, because of the delivery method. In this model, your application does not look up user attributes in a directory. Instead, the user delivers claims to your application, and your application examines them. Each claim is made by an issuer, and you trust the claim only as much as you trust the issuer. For example, you trust a claim made by your company's domain controller more than you trust a claim made by the user.</span></span>
  
    
    

### <a name="security-token-a-serialized-set-of-claims"></a><span data-ttu-id="60a47-125">Маркер безопасности: сериализованных набор утверждений</span><span class="sxs-lookup"><span data-stu-id="60a47-125">Security token: A serialized set of claims</span></span>

<span data-ttu-id="60a47-p104">Пользователь предоставляет набор утверждений в приложение с запросом. В веб-службе этих утверждений переносятся в заголовке безопасности конверте SOAP. В браузере веб-приложения утверждений браузер пользователя, поставляемых через HTTP POST и более поздних версий могут кэшироваться в файле cookie, при желании сеанса. Независимо от того, как эти утверждений поступают должен быть сериализованным. Маркер безопасности  это сериализованных набор утверждений цифровой подписью, выдан. Подпись важно: дает Software assurance пользователя не только составляют утверждений и отправлять их для вас. В случаях низким уровнем безопасности криптографии нет необходимости, можно использовать неподписанные маркеры, когда этого сценария не описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="60a47-p104">The user delivers a set of claims to your application with a request. In a web service, these claims are carried in the security header of the SOAP envelope. In a browser-based web application, the claims arrive through an HTTP POST from the user's browser, and may later be cached in a cookie if a session is desired. Regardless of how these claims arrive, they must be serialized. A security token is a serialized set of claims that is digitally signed by the issuing authority. The signature is important: it gives you assurance that the user did not just make up claims and send them to you. In low-security situations where cryptography is not necessary or desired, you can use unsigned tokens, but that scenario is not described in this article.</span></span>
  
    
    
<span data-ttu-id="60a47-p105">Один из основных компонентов в Windows Identity Foundation (WIF) является возможность создания и чтения маркеров безопасности. WIF Microsoft .NET Framework обрабатывать все действия, шифрования и представить приложения с набором утверждения, которые могут читать.</span><span class="sxs-lookup"><span data-stu-id="60a47-p105">One of the core features in Windows Identity Foundation (WIF) is the ability to create and read security tokens. WIF and the Microsoft .NET Framework handle all of the cryptographic work, and present your application with a set of claims that it can read.</span></span>
  
    
    

### <a name="security-token-service-sts"></a><span data-ttu-id="60a47-135">Служба маркеров безопасности (STS)</span><span class="sxs-lookup"><span data-stu-id="60a47-135">Security token service (STS)</span></span>

<span data-ttu-id="60a47-p106">Служба маркеров безопасности (STS)  это коммуникации, обеспечивающая, знаки и маркеров безопасности проблемы в соответствии с взаимодействующие протоколы, описанные в разделе "Стандарты" в этой статье. Существует много работы, входящий в реализации этих протоколов, но WIF делает все это работать за вас, что делает возможным для тех, кто не является протоколы под руководством экспертов, чтобы получить STS регистрация и запуск с минимальными усилиями.</span><span class="sxs-lookup"><span data-stu-id="60a47-p106">A security token service (STS) is the plumbing that builds, signs, and issues security tokens according to the interoperable protocols discussed in the "Standards" section of this article. There is a lot of work that goes into implementing these protocols, but WIF does all of this work for you, making it possible for someone who is not a protocols expert to get an STS up and running with little effort.</span></span> 
  
    
    
<span data-ttu-id="60a47-p107">WIF упрощает создание собственных STS. Это необходимо решить, как реализовать логику или правил, обеспечивающие ее (часто называется политика безопасности).</span><span class="sxs-lookup"><span data-stu-id="60a47-p107">WIF makes it easier to build your own STS. It is up to you to figure out how to implement the logic, or rules, that enforce it (often referred to as security policy).</span></span>
  
    
    

### <a name="issuing-authority"></a><span data-ttu-id="60a47-140">issuing authority</span><span class="sxs-lookup"><span data-stu-id="60a47-140">Issuing authority</span></span>

<span data-ttu-id="60a47-p108">Существует множество различных типов сертификатов, из контроллеров домена, выдача билетов Kerberos центрам сертификации, которые выдают сертификаты X.509. Конкретный тип центра сертификации, обсуждаемые в этой статье проблем маркеров безопасности, которые содержат утверждений. В этом сертификации  это веб-приложения или веб-службе, маркеры безопасности. Необходимо иметь возможность выдачи соответствующих прав утверждений, присвоенное конечного, проверяющей стороной и пользователя, отправившего запрос и может быть отвечает за взаимодействия с хранилищ пользователей для поиска утверждений и проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="60a47-p108">There are many different types of issuing authorities, from domain controllers that issue Kerberos tickets, to certificate authorities that issue X.509 certificates. The specific type of authority discussed in this article issues security tokens that contain claims. This issuing authority is a web application or web service that issues security tokens. It must be able to issue the proper claims given the target relying party and the user making the request, and might be responsible for interacting with user stores to look up claims and authenticate users.</span></span>
  
    
    
<span data-ttu-id="60a47-p109">Любые сертификации выбран, он центральной роли в решении удостоверения. Если проверка подлинности принимать из приложения, опираясь на основе утверждений, передача ответственности в эту службу и попросите его для проверки подлинности пользователей от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="60a47-p109">Whatever issuing authority you choose, it plays a central role in your identity solution. When you factor authentication out of your application by relying on claims, you are passing responsibility to that authority and asking it to authenticate users on your behalf.</span></span>
  
    
    

### <a name="relying-parties"></a><span data-ttu-id="60a47-147">Проверяющей стороны</span><span class="sxs-lookup"><span data-stu-id="60a47-147">Relying parties</span></span>

<span data-ttu-id="60a47-p110">При создании приложения, основанный на утверждениях построении проверяющей стороной приложения. Синонимы для проверяющей стороны включают «утверждения приложением» и «приложения на основе утверждений». Веб-приложений и веб-службы могут быть проверяющими сторонами.</span><span class="sxs-lookup"><span data-stu-id="60a47-p110">When you build an application that relies on claims, you are building a relying party application. Synonyms for a relying party include "claims-aware application" and "claims-based application". Web applications and web services can both be relying parties.</span></span>
  
    
    
<span data-ttu-id="60a47-p111">Проверяющая сторона приложение использует маркеры, выданные STS и извлекает утверждений из маркеров их использования для удостоверения задач, связанных с. Службы маркеров безопасности поддерживает два типа проверяющей стороне приложения: ASP.NET веб-приложений и Windows Communication Foundation (WCF) веб-службы.</span><span class="sxs-lookup"><span data-stu-id="60a47-p111">A relying party application consumes tokens issued by an STS and extracts claims from tokens to use them for identity related tasks. The STS supports two types of relying party application: ASP.NET web applications, and Windows Communication Foundation (WCF) web services.</span></span>
  
    
    

### <a name="standards"></a><span data-ttu-id="60a47-153">Стандарты</span><span class="sxs-lookup"><span data-stu-id="60a47-153">Standards</span></span>

<span data-ttu-id="60a47-p112">Чтобы сделать все это взаимодействующие, несколько WS-* стандартов в предыдущем сценарии. Получить политику с помощью WS-MetadataExchange и сама политика является структурированной спецификации WS-Policy. Службы маркеров безопасности предоставляет конечные точки, которые реализуют спецификация WS-Trust, который описывает, как для запроса и получения маркеров безопасности. Большинство маркер безопасности служб маркеры today проблему, отформатированный с помощью разметки языка SAML (Security Assertion). SAML является отрасли словарь в XML, который может использоваться для представления утверждений функциональную совместимость. Или, в случае multiplatform это позволяет общаться с STS на совершенно другой платформы и обеспечения единого входа для всех приложений, независимо от платформы.</span><span class="sxs-lookup"><span data-stu-id="60a47-p112">To make all of this interoperable, several WS-* standards are used in the previous scenario. Policy is retrieved by using WS-MetadataExchange, and the policy itself is structured according to the WS-Policy specification. The STS exposes endpoints that implement the WS-Trust specification, which describes how to request and receive security tokens. Most security token services today issue tokens formatted with Security Assertion Markup Language (SAML). SAML is an industry-recognized XML vocabulary that can be used to represent claims in an interoperable way. Or, in a multiplatform situation, this enables you to communicate with an STS on an entirely different platform and achieve single sign-on across all of your applications, regardless of platform.</span></span>
  
    
    

### <a name="browser-based-applications"></a><span data-ttu-id="60a47-160">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="60a47-160">Browser-based applications</span></span>

<span data-ttu-id="60a47-p113">Смарт-клиенты не только те, которые можно использовать модель идентификации на основе утверждений. Веб-приложения (также называется пассивной клиентов) также можно использовать его. В следующем сценарии описывается, как это работает.</span><span class="sxs-lookup"><span data-stu-id="60a47-p113">Smart clients are not the only ones who can use the claims-based identity model. Browser-based applications (also referred to as passive clients) can also use it. The following scenario describes how this works.</span></span>
  
    
    
<span data-ttu-id="60a47-p114">Во-первых пользователь наводит браузера на веб-приложения (проверяющей стороной приложение). Веб-приложения, перенаправляет браузер для службы маркеров безопасности, чтобы проверка подлинности пользователя. Службы маркеров безопасности размещается в простой веб-приложения, которое считывает входящего запроса, выполняет проверку подлинности пользователя с помощью стандартных механизмов HTTP и создает маркер SAML и возвращает фрагмент кода ECMAScript (JavaScript, JScript), браузер для инициации HTTP POST, который отправляет маркер SAML проверяющей стороной. Основная часть этой записи содержит утверждения, которые запрошено проверяющей стороной. На этом этапе чаще всего для проверяющей стороны упаковка утверждений в файле cookie, чтобы пользователь не имеет для перенаправления для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="60a47-p114">First, the user points a browser at a claims-aware web application (the relying party application). The web application redirects the browser to the STS so that the user can be authenticated. The STS is hosted in a simple web application that reads the incoming request, authenticates the user by using standard HTTP mechanisms, and then creates a SAML token and replies with a piece of ECMAScript (JavaScript, JScript) code that causes the browser to initiate an HTTP POST that sends the SAML token back to the relying party. The body of this POST contains the claims that the relying party requested. At this point, it is common for the relying party to package the claims into a cookie so that the user does not have to be redirected for each request.</span></span>
  
    
    

### <a name="claims-to-windows-token-service-c2wts"></a><span data-ttu-id="60a47-169">Служба c2WTS</span><span class="sxs-lookup"><span data-stu-id="60a47-169">Claims to Windows Token Service (c2WTS)</span></span>

<span data-ttu-id="60a47-p115">Служба c2WTS  это компонент Windows Identity Foundation (WIF). c2WTS извлекает утверждения имени участника-пользователя (UPN) из маркеров безопасности, отличных от Windows, например, маркеров SAML и X.509, и создает маркеры безопасности Windows уровня олицетворения. Это позволяет приложению проверяющей стороны олицетворять пользователя. Это может потребоваться для доступа к серверным ресурсам, например, ресурсам Microsoft SQL Server, которые являются внешними по отношению к приложению проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="60a47-p115">The Claims to Windows Token Service (c2WTS) is a feature of Windows Identity Foundation (WIF). The c2WTS extracts user principal name (UPN) claims from non-Windows security tokens, such as SAML and X.509 tokens, and generates impersonation-level Windows security tokens. This allows a relying party application to impersonate the user. This might be needed to access back-end resources, such as Microsoft SQL Servers, that are external to the computer running the relying party application.</span></span>
  
    
    
<span data-ttu-id="60a47-p116">c2WTS  это служба Windows, которая устанавливается как часть WIF. По соображениям безопасности c2WTS работает только на основе явного согласия пользователя. Должна быть запущена вручную и работает как учетная запись локальной системы. Администратор должен вручную настроить c2WTS со списком разрешенных абонентов. По умолчанию список пуст.</span><span class="sxs-lookup"><span data-stu-id="60a47-p116">The c2WTS is a Windows service that is installed as part of WIF. For security reasons, the c2WTS works only on an opt-in basis. It must be started manually and it runs as the local system account. An administrator must also manually configure the c2WTS with a list of allowed callers. By default, the list is empty.</span></span> 
  
    
    
<span data-ttu-id="60a47-p117">Если приложение проверяющей стороной работает как учетная запись локальной системы, его не нужно использовать c2WTS. Однако, если приложение проверяющей стороной работает как учетная запись сетевой службы, или ASP.NET приложения, например, может потребоваться использовать c2WTS для доступа к ресурсам на другом компьютере.</span><span class="sxs-lookup"><span data-stu-id="60a47-p117">If your relying party application runs as the local system account, it does not need to use the c2WTS. But, if your relying party application runs as the network service account, or is an ASP.NET application, for example, it might need to use the c2WTS to access resources on another computer.</span></span>
  
    
    
<span data-ttu-id="60a47-p118">Предположим, что у вас есть веб-фермы, состоящее из сервера, на котором выполняется приложение ASP.NET, который получает доступ к базе данных SQL на фоновом сервере. Требуется сделать это приложение утверждения. Однако приложение не может получить доступ к базы данных SQL с помощью утверждений, которая получает из службы маркеров безопасности. Вместо этого он использует c2WTS для преобразования утверждений имени участника-пользователя с маркером безопасности Windows. Это позволяет получить доступ к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="60a47-p118">Suppose that you have a web farm that consists of a server that runs an ASP.NET application, which accesses a SQL database on a back-end server. You want to make this application claims-aware. But, the application can't access the SQL database by using the claim that it receives from an STS. Instead, it uses the c2WTS to convert the UPN claim to a Windows security token. This allows it to access the SQL database.</span></span>
  
> [!NOTE]
> <span data-ttu-id="60a47-p119">[!Примечание] Чтобы разрешить приложению доступ к ресурсам на другом сервере, администратор домена необходимо настроить службы каталогов Active Directory, чтобы разрешить ограниченное делегирование. Сведения о том, как разрешить ограниченное делегирование можно  [способ: использование перенос протокола и ограниченное eelegation в ASP.NET 2.0](http://msdn.microsoft.com/en-us/library/ms998355.aspx).</span><span class="sxs-lookup"><span data-stu-id="60a47-p119">To allow an application to access resources on a different server, a domain administrator must configure the Active Directory directory service to enable constrained delegation. For information about how to enable constrained delegation, see  [How to: Use protocol transition and constrained eelegation in ASP.NET 2.0](http://msdn.microsoft.com/en-us/library/ms998355.aspx).</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="60a47-188">См. также</span><span class="sxs-lookup"><span data-stu-id="60a47-188">See also</span></span>
<span data-ttu-id="60a47-189"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="60a47-189"></span></span>


-  [<span data-ttu-id="60a47-190">Проверка подлинности, авторизация и безопасность в SharePoint</span><span class="sxs-lookup"><span data-stu-id="60a47-190">Authentication, authorization, and security in SharePoint</span></span>](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [<span data-ttu-id="60a47-191">Примерный сценарий делегирования, федерации и проверки подлинности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="60a47-191">Sample delegation, federation, and authentication scenario in SharePoint</span></span>](sample-delegation-federation-and-authentication-scenario-in-sharepoint.md)
    
  
-  [<span data-ttu-id="60a47-192">Определения терминов идентификации на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="60a47-192">Claims-based identity term definitions</span></span>](claims-based-identity-term-definitions.md)
    
  

