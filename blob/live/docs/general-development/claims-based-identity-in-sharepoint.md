---
title: "Удостоверение, основанное на основе утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 32b6af2a-72f3-4302-a6af-5f00143cbf67
ms.openlocfilehash: 7df5c259861cb43a36d5c7290a45698614ebfd20
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="claims-based-identity-in-sharepoint"></a><span data-ttu-id="a728c-102">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a728c-102">Claims-based identity in SharePoint</span></span>
<span data-ttu-id="a728c-103">Сведения о базовых компонента архитектура идентификации на основе утверждений в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a728c-103">Learn about the fundamentals of claims-based identity architecture in SharePoint.</span></span>
## <a name="claims-based-authentication"></a><span data-ttu-id="a728c-104">Проверка подлинности на основе утверждений</span><span class="sxs-lookup"><span data-stu-id="a728c-104">Claims-based authentication</span></span>

<span data-ttu-id="a728c-p101">Проверка подлинности на основе утверждений позволяет систем и приложений для проверки подлинности пользователя, без взаимодействия с пользователем раскрыть более личные сведения (например, номера социального страхования и Дата рождения), чем требуется. Пример проверки подлинности на основе утверждений  кто-то бренда старше 18 лет или кто-то бренда в группе маркетинга компании. Внешняя система (проверяющая сторона) требует только доверяет проверки подлинности, можно проверить эти заявки разрешать пользователям проходить проверку подлинности для определенных функций.</span><span class="sxs-lookup"><span data-stu-id="a728c-p101">Claims-based authentication enables systems and applications to authenticate a user without requiring the user to disclose more personal information (such as social security number and date of birth) than necessary. An example of claims-based authentication is someone claiming to be over 18 years old or someone claiming to be in a company's marketing group. An external system (relying party) needs only to trust the authentication authority that can validate those claims to allow the user to be authenticated for specific functions.</span></span>
  
    
    

### <a name="claims-a-set-of-information-about-a-subject"></a><span data-ttu-id="a728c-108">Утверждений: Набор сведений по теме</span><span class="sxs-lookup"><span data-stu-id="a728c-108">Claims: A set of information about a subject</span></span>

<span data-ttu-id="a728c-p102">Адекватный способ подумайте, утверждений  как набор сведений о некоторых темы. Этой теме чаще всего  это пользователь, но также может быть приложения, компьютер или что-то еще. Удостоверение передается в сети, представлен какой-либо маркера (также известной как маркера безопасности).</span><span class="sxs-lookup"><span data-stu-id="a728c-p102">The clearest way to think about claims is as a set of information about some subject. This subject is most often a person, but it might also be an application, a computer, or something else. When an identity is transmitted on the network, it is represented by some kind of token (also known as a security token).</span></span> 
  
    
    
<span data-ttu-id="a728c-p103">Утверждения  это часть сведений о теме, которая объявляет поставщика утверждений по данной теме. Это заявление о тему (например, имя), которое будет создано по теме о самого или другого субъекта. Можно представить утверждения несколько сведения об удостоверениях, например, адрес электронной почты, имя, срок хранения или членство в роли продаж. Это уникальный идентификатор, представляющий конкретного пользователя, приложения, компьютера или другой сущности. Включение этого лица для получения доступа к нескольким ресурсам, например, приложений и сетевых ресурсов, не вводя учетные данные несколько раз. Кроме того позволяет ресурсы для проверки запросов от сущности. Чем больше на основе утверждений, что приложение получает, тем больше вы знаете о пользователя.</span><span class="sxs-lookup"><span data-stu-id="a728c-p103">A claim is a piece of information about a subject that a claims provider asserts about that subject. It is a statement about a subject (for example, a name) that is made by a subject about itself or another subject. You can think of a claim as a bit of identity information, such as email address, name, age, or membership in the sales role. It is a unique identifier that represents a specific user, application, computer, or other entity. It enables that entity to gain access to multiple resources, such as applications and network resources, without entering credentials multiple times. It also enables resources to validate requests from an entity. The more claims that an application receives, the more you know about your user.</span></span>
  
    
    
<span data-ttu-id="a728c-119">Утверждения переданными одно или несколько значений и затем упакованный в маркеров безопасности, выдаваемых Служба маркеров безопасности (STS).</span><span class="sxs-lookup"><span data-stu-id="a728c-119">A claim is given one or more values and then packaged in security tokens that are issued by a security token service (STS).</span></span>
  
    
    
<span data-ttu-id="a728c-p104">Word, утверждения используется вместо wordатрибутов , обычно используемый в мире каталога предприятия, из-за метода доставки. В этой модели приложение не выполнять поиск атрибутов пользователя в каталоге. Вместо этого пользователь посылает утверждения для приложения. Каждый утверждения осуществляется поставщика и в утверждения только так же, как вы доверяете поставщика. Например доверять утверждения, сделанных с контроллера домена вашей компании больше, чем утверждения, сделанные пользователем. API утверждений имеет свойство издателя, которая позволяет узнать, кто выдал заявку.</span><span class="sxs-lookup"><span data-stu-id="a728c-p104">The word claim is used, instead of the wordattributes that is more commonly used in the enterprise directory world, because of the delivery method. In this model, your application does not look up user attributes in a directory. Instead, the user delivers claims to your application. Each claim is made by an issuer, and you trust the claim only as much as you trust the issuer. For example, you trust a claim made by your company's domain controller more than a claim made by the user. The claims API has an issuer property that enables you to find out who issued the claim.</span></span>
  
    
    

### <a name="tokens-information-about-an-identity"></a><span data-ttu-id="a728c-126">Маркеры: Сведения о удостоверение</span><span class="sxs-lookup"><span data-stu-id="a728c-126">Tokens: Information about an identity</span></span>

<span data-ttu-id="a728c-p105">Маркер  это набор в байтах, которое выражает сведения о identity. Эта информация состоит из одного или нескольких утверждений, каждая из которых содержит сведения о теме, к которому применяется этот маркер. Утверждений в маркере обычно содержат данные, например имя пользователя, который представляет их. Они также может содержать множество типов других сведений  утверждениям не ограничены и даже включать не требуется, имя субъекта. И, как и предполагает word утверждений , это приложение, которое получает маркер автоматически не принимает сведения, которые он содержит. Вместо этого полученных маркер обычно проверяется каким-либо образом перед приложение использует какие-либо утверждения, которые он содержит.</span><span class="sxs-lookup"><span data-stu-id="a728c-p105">A token is a set of bytes that expresses information about an identity. This information consists of one or more claims, each of which contains some information about the subject to which this token applies. The claims in a token commonly contain information such as the name of the user who presents it. They can also contain many sorts of other information—claims are not limited to, and do not even need to include, a subject's name. And, as the word claims suggests, an application that receives a token does not automatically accept the information that it contains. Instead, a received token is usually validated in some way before an application uses any claims that it contains.</span></span>
  
    
    
<span data-ttu-id="a728c-p106">Основные концепции  это что утверждения не только что уникальный идентификатор, который определяет ресурс, приложения или пользователя. Это набор утверждений (то есть, значения), используемый для описания ресурсов, приложения или пользователя. Утверждения также используются для авторизации доступа.</span><span class="sxs-lookup"><span data-stu-id="a728c-p106">The key concept is that a claim is not just a unique identifier that identifies the resource, application, or user. It is a set of claims (that is, values) that is used to describe the resource, application, or user. The claims are also used to authorize access.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="a728c-136">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a728c-136">Additional resources</span></span>
<span data-ttu-id="a728c-137"><a name="SP15_RoleInheritance_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a728c-137"></span></span>


-  [<span data-ttu-id="a728c-138">Проверка подлинности, авторизация и безопасность в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a728c-138">Authentication, authorization, and security in SharePoint</span></span>](authentication-authorization-and-security-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a728c-139">Входящих утверждений: вход в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a728c-139">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="a728c-140">Поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a728c-140">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a728c-141">Как: создать поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a728c-141">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a728c-142">Как: развернуть поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a728c-142">How to: Deploy a claims provider in SharePoint</span></span>](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  

