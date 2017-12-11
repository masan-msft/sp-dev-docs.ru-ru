---
title: "Пример сценария делегирования, федерации и проверки подлинности в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 43ed1eaec1f6e5ec9e29e032162b271d2830b41d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sample-delegation-federation-and-authentication-scenario-in-sharepoint"></a><span data-ttu-id="7a5c2-102">Пример сценария делегирования, федерации и проверки подлинности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7a5c2-102">Sample delegation, federation, and authentication scenario in SharePoint</span></span>
<span data-ttu-id="7a5c2-103">В этой статье приведены примеры сценариев для делегирования удостоверений и федерации удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-103">This article provides sample scenarios for identity delegation and identity federation.</span></span>
## <a name="sample-scenarios"></a><span data-ttu-id="7a5c2-104">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="7a5c2-104">Sample scenarios</span></span>
<span data-ttu-id="7a5c2-105"><a name="SP15_SampleDelegation_SampleScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="7a5c2-105"></span></span>

<span data-ttu-id="7a5c2-106">Следующие вымышленной компании и их сказано бизнес-потребности в используются примеры сценариев, описанные в этой статье:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-106">The following fictional companies and their stated business needs are used in the sample scenarios that are described in this article:</span></span>
  
    
    

- <span data-ttu-id="7a5c2-p101">**Гибридные Contoso**  это международных автомобилей модуль питания компания занимается первоначальной электрический и на основе ячейки топлива гибридных обработчики для car производители внутри и за ее пределами США. В стратегических усилий в соответствии с частями, упорядочения требования клиентов ИТ-подразделения в домене Contoso получает задачу разработки и развертывания безопасных Интернет частей упорядочения приложения с помощью имени узла Contoso.com. Это приложение также необходимо задать несколько уровней доступа для различных внутренних пользователей (сотрудники) и внешних пользователей (сотрудников производитель автомобиль). Для сведения к минимуму затраты на обслуживание части, порядок приложения, ИТ также необходимо избежать необходимости для приложения, использование и обслуживание хранилища дополнительных учетных записей для внутренних и внешних пользователей для доступа к приложению.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p101">**Contoso Hybrid** is an international automobile engine supply company that specializes in manufacturing electric and fuel cell-based hybrid engines to car manufactures inside and outside of the United States. In a strategic effort to meet the parts ordering demands of its customers, the IT department at Contoso is tasked with developing and deploying a secure Internet-accessible parts ordering application through their host name, Contoso.com. This application must also provide multiple levels of access for various internal users (Contoso employees) and external users (car manufacturer employees). To minimize costs associated with maintaining the parts ordering application, IT must also avoid the need for the application to use and maintain an additional account store for internal and external users to access the application.</span></span>
    
  
- <span data-ttu-id="7a5c2-p102">**Fabrikam моторов** является шведский производителя fuel-efficient compact автомобилей и небольшой автомобилей, по всему миру известно его точки низкой цены на гибридном автомобили. Несмотря на то, что продажи постоянно год за годом ускорением для Fabrikam, было заметно повысить на гибридный модуль сбоев в рамках их первого года в автомобилей, проданных клиентам. Fabrikam моторов на обслуживание стандартной для высокого уровня службы его необходимо реализовать более эффективный способ для части модуля гибридной для заказанных через гибридные Contoso.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p102">**Fabrikam Motors** is a Swedish manufacturer of fuel-efficient compact cars and small cars that is known worldwide for its low price point on hybrid automobiles. Although sales have accelerated consistently year after year for Fabrikam, there has been a noticeable increase in hybrid engine failure rates within their first year, in cars sold to customers. For Fabrikam Motors to maintain its standard for high levels of service, it must implement a more efficient way for hybrid engine parts to be ordered through Contoso Hybrid.</span></span>
    
  
<span data-ttu-id="7a5c2-113">Ниже перечислены связанные понятия.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-113">The following are related concepts:</span></span>
  
    
    

- <span data-ttu-id="7a5c2-p103">**Федерации удостоверений**. Описание установки федерации между гибридного Contoso и моторов Fabrikam, чтобы Fabrikam пользователей интерфейс единого входа при доступе к ресурсам гибридного Contoso.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p103">**Identity federation**. Explains the establishment of federation between Contoso Hybrid and Fabrikam Motors so that Fabrikam users get a single sign-on experience when accessing Contoso Hybrid resources.</span></span>
    
  
- <span data-ttu-id="7a5c2-p104">**Делегирование удостоверений**. Объясняет возможность доступа к ресурсам из Contoso гибридного веб-службы, который требует маркер ActAs; то есть служба требует идентификатор интерпретации абонентом (обычно удостоверение службы) и исходного пользователя, инициировавшего запрос (обычно идентификатор интерактивного пользователя).</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p104">**Identity delegation**. Explains the ability to access the resources from a Contoso Hybrid web service that requires an ActAs token; that is, the service requires the identity of the immediate caller (typically the identity of the service) and the original user who initiated the request (typically the identity of the interactive user).</span></span>
    
  

## <a name="identity-delegation"></a><span data-ttu-id="7a5c2-118">Делегирование удостоверений</span><span class="sxs-lookup"><span data-stu-id="7a5c2-118">Identity delegation</span></span>
<span data-ttu-id="7a5c2-119"><a name="SP15_SampleDelegation_IdentityDelegation"> </a></span><span class="sxs-lookup"><span data-stu-id="7a5c2-119"></span></span>

<span data-ttu-id="7a5c2-p105">В этом сценарии описывается приложение, которое требуется доступ к ресурсам сервера, которые требуют цепочки делегирования удостоверений для выполнения проверки контроля доступа. Цепочка делегирования простой удостоверения обычно состоит из сведения о исходного вызова и идентификатором непосредственно вызывающего метода.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p105">This scenario describes an application that needs to access back-end resources that require the identity delegation chain to perform access control checks. A simple identity delegation chain usually consists of the information on the initial caller and the identity of the immediate caller.</span></span> 
  
    
    
<span data-ttu-id="7a5c2-p106">С помощью модели делегирования Kerberos на платформе Windows сегодня ресурсы серверной имеют доступ только к identity непосредственно вызывающего метода и не, начальной вызывающего абонента. В этой модели обычно называемую модель доверенной подсистемы. Windows Identity Foundation (WIF) сохраняет идентификатор исходного вызова и интерпретации вызывающего абонента в цепочке делегирования с помощью свойства  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p106">With the Kerberos delegation model on the Windows platform today, the back-end resources have access only to the identity of the immediate caller and not to that of the initial caller. This model is commonly referred to as the trusted subsystem model. Windows Identity Foundation (WIF) maintains the identity of the initial caller and the immediate caller in the delegation chain by using the  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) property.</span></span>
  
    
    
<span data-ttu-id="7a5c2-p107">На рисунке 1 показано сценарий делегирования типичного удостоверений, в котором сотрудников компании Fabrikam получает доступ к ресурсам, предоставляемые в приложении Contoso.com. **На рисунке 1. Вызов проверки подлинности федерации**</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p107">Figure 1 shows a typical identity delegation scenario in which a Fabrikam employee accesses resources exposed in a Contoso.com application. **Figure 1. Claims federation authentication**</span></span>

  
    
    

  
    
    
![Сценарий делегирования удостоверений, основанных на утверждениях](../images/44928b39-5683-4bce-8ddf-31d886243b87.gif)
  
    
    
<span data-ttu-id="7a5c2-128">Сотрудников, участвующих в этом сценарии являются:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-128">The fictional users participating in this scenario are:</span></span>
- <span data-ttu-id="7a5c2-129">Фрэнк: Fabrikam сотрудник, которому требуется доступ к ресурсам компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-129">Frank: A Fabrikam employee who wants to access Contoso resources.</span></span>
    
  
- <span data-ttu-id="7a5c2-130">Daniel: Contoso приложения разработчика, который реализует необходимые изменения в приложении.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-130">Daniel: A Contoso application developer who implements the necessary changes in the application.</span></span>
    
  
- <span data-ttu-id="7a5c2-131">Режим ADAM: Contoso ИТ-администратор.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-131">Adam: The Contoso IT administrator.</span></span>
    
  
<span data-ttu-id="7a5c2-132">Компоненты, используемые в этом сценарии являются:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-132">The components involved in this scenario are:</span></span>
- <span data-ttu-id="7a5c2-p108">Web1: веб-приложения со ссылками на серверной ресурсы, которые требуют делегированного удостоверения исходного вызова. Это приложение создается с ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p108">web1: A web application with links to back-end resources that require the delegated identity of the initial caller. This application is built with ASP.NET.</span></span>
    
  
- <span data-ttu-id="7a5c2-p109">Веб-служба, которая обращается к компьютера под управлением Microsoft SQL Server, где требуется делегированного удостоверения начальной звонящего и непосредственно вызывающего метода. Эта служба построенных с помощью Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p109">A web service that accesses a computer running Microsoft SQL Server, which requires the delegated identity of the initial caller and of the immediate caller. This service is built with Windows Communication Foundation (WCF).</span></span>
    
  
- <span data-ttu-id="7a5c2-p110">sts1: служба маркеров безопасности (STS), который выполняет роль поставщика федерации и выдает утверждения, которые ожидаются приложением (web1). Она установила доверие с Fabrikam.com, а также с приложением.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p110">sts1: A security token service (STS) that is in the role of federation provider, and emits claims that are expected by the application (web1). It has established trust with Fabrikam.com and also with the application.</span></span>
    
  
- <span data-ttu-id="7a5c2-p111">sts2: службы маркеров безопасности, который выполняет роль поставщика удостоверений для Fabrikam.com и, которая предоставляет конечную точку, для проверки подлинности используются сотрудников компании Fabrikam. Он устанавливает отношение доверия с Contoso.com, чтобы между сотрудниками компании Fabrikam могут получить доступ к ресурсам на Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p111">sts2: An STS that is in the role of identity provider for Fabrikam.com and that provides an endpoint that the Fabrikam employee uses to authenticate. It has established trust with Contoso.com so that Fabrikam employees are allowed to access resources on Contoso.com.</span></span>
    
  
<span data-ttu-id="7a5c2-p112">Обратите внимание на то, что термин «Маркер ActAs» относится к маркер, выданный STS и, которая содержит удостоверение пользователя. Свойство  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) содержит удостоверений службы маркеров безопасности.Как показано на рисунке 1 приведен поток в этом сценарии:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p112">Note that the term "ActAs token" refers to a token that is issued by an STS and that contains the user's identity. The  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) property contains the STS's identity.As shown in Figure 1, the flow in this scenario is:</span></span>
  
    
    

1. <span data-ttu-id="7a5c2-p113">Contoso приложение настроено для получения маркера ActAs, содержащая идентификатор сотрудника компании Fabrikam и интерпретации вызывающей стороны в свойстве  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) . Daniel реализует эти изменения к приложению.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p113">The Contoso application is configured to obtain an ActAs token that contains both the Fabrikam employee's identity and the immediate caller's identity in the  [Delegate()](https://msdn.microsoft.com/en-us/library/cc310252.aspx) property. Daniel implements these changes to the application.</span></span>
    
  
2. <span data-ttu-id="7a5c2-p114">Contoso приложение настроено для передачи маркера ActAs серверной службы. Daniel реализует эти изменения к приложению.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p114">The Contoso application is configured to pass the ActAs token to the back-end service. Daniel implements these changes to the application.</span></span>
    
  
3. <span data-ttu-id="7a5c2-p115">Веб-служба Contoso настроена для проверки маркера ActAs путем вызова sts1. Режим ADAM позволяет sts1 обработать запросы на передачу.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p115">The Contoso web service is configured to validate the ActAs token by calling sts1. Adam enables sts1 to process delegation requests.</span></span>
    
  
4. <span data-ttu-id="7a5c2-149">Пользователь Fabrikam Фрэнк осуществляет доступ к приложению Contoso и он получает доступ к ресурсам сервера.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-149">Fabrikam user Frank accesses the Contoso application and is given access to the back-end resources.</span></span>
    
  

## <a name="federated-authentication"></a><span data-ttu-id="7a5c2-150">Федеративная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="7a5c2-150">Federated authentication</span></span>
<span data-ttu-id="7a5c2-151"><a name="SP15_SampleDelegation_FederatedAuth"> </a></span><span class="sxs-lookup"><span data-stu-id="7a5c2-151"></span></span>

<span data-ttu-id="7a5c2-p116">Федеративная проверка подлинности позволяет Служба маркеров безопасности (STS) в одном домене доверия для предоставления сведения о проверке подлинности STS в другой домен доверия при отношение доверия между двумя доменами. В качестве примера показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p116">Federated authentication allows a security token service (STS) in one trust domain to provide authentication information to an STS in another trust domain when there is a trust relationship between the two domains. An example of this is shown in Figure 2.</span></span>
  
    
    

<span data-ttu-id="7a5c2-154">**На рисунке 2. Сценарий федерации на основе утверждений**</span><span class="sxs-lookup"><span data-stu-id="7a5c2-154">**Figure 2. Claims federation scenario**</span></span>

  
    
    

  
    
    
![Вызов проверки подлинности федерации](../images/f0a9be9a-434a-4650-ad57-1fb90b016dd1.gif)
  
    
    

  
    
    

1. <span data-ttu-id="7a5c2-156">Клиент в доверенном домене Fabrikam отправляет запрос к приложению проверяющей стороны в домене Contoso доверия.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-156">A client in the Fabrikam trust domain sends a request to a relying party application in the Contoso trust domain.</span></span>
    
  
2. <span data-ttu-id="7a5c2-p117">Для STS в домене Contoso доверия проверяющей стороны перенаправляет клиента. В этом службы маркеров безопасности не имеет сведений клиента.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p117">The relying party redirects the client to an STS in the Contoso trust domain. This STS has no knowledge of the client.</span></span>
    
  
3. <span data-ttu-id="7a5c2-159">Службы маркеров безопасности Contoso перенаправляет клиента на STS в домене Fabrikam доверия, с которым доверия домен Contoso имеет отношение доверия.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-159">The Contoso STS redirects the client to an STS in the Fabrikam trust domain, with which the Contoso trust domain has a trust relationship.</span></span>
    
  
4. <span data-ttu-id="7a5c2-160">Fabrikam STS проверяет удостоверение клиента, а маркер безопасности для службы маркеров безопасности Contoso.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-160">The Fabrikam STS verifies the client's identity and issues a security token to the Contoso STS.</span></span>
    
  
5. <span data-ttu-id="7a5c2-161">Службы маркеров безопасности Contoso использует маркер Fabrikam создание собственной маркер, который отправляет на проверяющей стороной.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-161">The Contoso STS uses the Fabrikam token to create its own token, which it sends to the relying party.</span></span>
    
  
6. <span data-ttu-id="7a5c2-162">Проверяющей стороной извлекает передавать утверждения клиента из маркер безопасности и используется для принятия решения проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-162">The relying party extracts the client's claims from the security token and makes an authentication decision.</span></span>
    
  
<span data-ttu-id="7a5c2-p118">Этот сценарий описывает интерфейс входа для сотрудников партнеров, когда она пытается получить доступ к ресурсам домена другого партнера. Она должна вход только один раз. Существует три основных участников в сценарии интеграции: имя поставщика удостоверений, поставщик федерации и проверяющей стороной. WIF предлагает API-интерфейсы для построения всем три игры.На рисунке 3 показаны федерации типичного сценария, где требуется доступ к ресурсам Contoso.com без необходимости войдите сотрудников компании Fabrikam; то есть сотрудников компании Fabrikam хочет использовать единый вход. **На рисунке 3. Сценарий делегирования удостоверений на основе утверждений**</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p118">This scenario describes a sign-on experience for a partner employee when she tries to access resources from another partner's domain. She has to sign-on only once. There are three major players in a federation scenario: an identity provider, a federation provider, and a relying party. WIF offers APIs to build all three players. Figure 3 shows a typical federation scenario where a Fabrikam employee wants to access Contoso.com resources without having to re-login; that is, the Fabrikam employee wants to use single sign-on. **Figure 3. Claims identity delegation scenario**</span></span>

  
    
    

  
    
    
![Вызов сценария федерации](../images/903d3109-d567-4156-a44f-29793c42ae45.gif)
  
    
    
<span data-ttu-id="7a5c2-170">Сотрудников, участвующих в этом сценарии являются:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-170">The fictional users participating in this scenario are:</span></span>
- <span data-ttu-id="7a5c2-171">Фрэнк: Fabrikam сотрудник, которому требуется доступ к ресурсам компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-171">Frank: A Fabrikam employee who wants to access Contoso resources.</span></span>
    
  
- <span data-ttu-id="7a5c2-172">Daniel: Contoso приложения разработчика, который реализует необходимые изменения в приложении.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-172">Daniel: A Contoso application developer who implements the necessary changes in the application.</span></span>
    
  
- <span data-ttu-id="7a5c2-173">Режим ADAM: Contoso ИТ-администратор.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-173">Adam: The Contoso IT administrator.</span></span>
    
  
<span data-ttu-id="7a5c2-174">Компоненты, используемые в этом сценарии являются:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-174">The components involved in this scenario are:</span></span>
- <span data-ttu-id="7a5c2-175">Web1: A частей заказа веб-приложения, созданных с помощью ASP.NET и управляет доступом к соответствующие элементы.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-175">web1: A parts ordering web application that is built with ASP.NET and controls access to the relevant parts.</span></span>
    
  
- <span data-ttu-id="7a5c2-p119">sts1: службы маркеров безопасности, который выполняет роль поставщика федерации в Contoso.com и выдает утверждения, которые ожидаются приложением (web1). Оно установлено отношение доверия с Fabrikam.com и разрешен доступ к между сотрудниками компании Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p119">sts1: An STS that is in the role of federation provider in Contoso.com and emits claims that are expected by the application (web1). It has established trust with Fabrikam.com and is configured to allow access to Fabrikam employees.</span></span>
    
  
- <span data-ttu-id="7a5c2-p120">sts2: службы маркеров безопасности, который выполняет роль поставщика удостоверений в Fabrikam.com и предоставляет конечную точку, к которой выполняется проверка подлинности сотрудников компании Fabrikam. Он устанавливает отношение доверия с Contoso.com, чтобы между сотрудниками компании Fabrikam могут получить доступ к ресурсам Contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-p120">sts2: An STS that is in the role of identity provider in Fabrikam.com and provides an endpoint to which the Fabrikam employee is authenticated. It has established trust with Contoso.com so that Fabrikam employees are allowed to access the Contoso.com resources.</span></span>
    
  
<span data-ttu-id="7a5c2-180">Как показано на рисунке 3  поток в этом сценарии:</span><span class="sxs-lookup"><span data-stu-id="7a5c2-180">As shown in Figure 3, the flow in this scenario is:</span></span>
  
    
    

1. <span data-ttu-id="7a5c2-181">Администратор Contoso Adam настраивает отношения доверия между приложениями (проверяющая сторона) и sts1.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-181">Contoso administrator Adam configures the trust between the application (relying party) and sts1.</span></span>
    
  
2. <span data-ttu-id="7a5c2-182">Администратор Contoso Adam настраивает отношение доверия с sts2 в качестве поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-182">Contoso administrator Adam configures the trust with sts2 as an identity provider.</span></span>
    
  
3. <span data-ttu-id="7a5c2-183">Администратор компании Fabrikam Фрэнк настраивается отношение доверия с sts1 как поставщик федерации и затем обращается к приложения.</span><span class="sxs-lookup"><span data-stu-id="7a5c2-183">Fabrikam administrator Frank configures the trust with sts1 as a federation provider and then accesses the application.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="7a5c2-184">См. также</span><span class="sxs-lookup"><span data-stu-id="7a5c2-184">See also</span></span>
<span data-ttu-id="7a5c2-185"><a name="SP15_SampleDelegation_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="7a5c2-185"></span></span>


-  [<span data-ttu-id="7a5c2-186">Удостоверение, основанное на утверждениях и концепций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7a5c2-186">Claims-based identity and concepts in SharePoint</span></span>](claims-based-identity-and-concepts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7a5c2-187">Определения терминов идентификации на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="7a5c2-187">Claims-based identity term definitions</span></span>](claims-based-identity-term-definitions.md)
    
  

