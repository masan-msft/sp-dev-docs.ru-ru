---
title: "Создание надстроек SharePoint, которые могут использовать анонимные пользователи"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 55d3a96a340e62ae27fbcd89dca3e9edc57d116b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-sharepoint-add-ins-that-can-be-used-by-anonymous-users"></a><span data-ttu-id="c9dd5-102">Создание надстроек SharePoint, которые могут использовать анонимные пользователи</span><span class="sxs-lookup"><span data-stu-id="c9dd5-102">Create SharePoint Add-ins that can be used by anonymous users</span></span>
<span data-ttu-id="c9dd5-103">Узнайте, как создавать надстройки SharePoint, которые могут использовать анонимные пользователи на общедоступных веб-сайтах Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-103">Learn how to create SharePoint Add-ins that can be used by anonymous users on public-facing Microsoft SharePoint sites.</span></span>
 

 <span data-ttu-id="c9dd5-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="c9dd5-107">**Важно!** При использовании термина "*локальная среда* SharePoint" в этой статье предполагается, что установлен пакет обновления 1 (SP1) для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-107">**Important**  Wherever  *on-premise*  SharePoint is mentioned in this article, we assume that Service Pack 1 for SharePoint has been installed.</span></span>
 


## <a name="prerequisites-for-creating-anonymously-accessible-sharepoint-add-ins"></a><span data-ttu-id="c9dd5-108">Предварительные требования для создания надстроек SharePoint с анонимным доступом</span><span class="sxs-lookup"><span data-stu-id="c9dd5-108">Prerequisites for creating anonymously accessible SharePoint Add-ins</span></span>

<span data-ttu-id="c9dd5-109">Анонимный доступ возможен для Надстройки SharePoint, размещенных в SharePoint и у поставщика. В зависимости от типа приложения изучите один из следующих наборов требований:</span><span class="sxs-lookup"><span data-stu-id="c9dd5-109">Anonymous access is possible for SharePoint-hosted and provider-hosted SharePoint Add-ins. Depending on which type you create, review one of the following sets of prerequisites:</span></span>
 
-  [<span data-ttu-id="c9dd5-110">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9dd5-110">Get Started Creating SharePoint Hosted SharePoint add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
-  [<span data-ttu-id="c9dd5-111">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="c9dd5-111">Get Started Creating Provider-Hosted SharePoint add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
<span data-ttu-id="c9dd5-p102">Вам также потребуется семейство сайтов в тестовой установке SharePoint, настроенной для анонимного доступа. Если у вас есть Сайт разработчиков Office 365, то уже существует связанное общедоступное семейство сайтов, использующее специальное определение общедоступного веб-сайта. (Дополнительные сведения об использовании общедоступных веб-сайтов в Microsoft SharePoint Online см. в статье  [Справка по общедоступному веб-сайту для Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).) Данное определение сайта недоступно для локальных установок SharePoint, поэтому если ваша тестовая установка находится в локальной среде, вам потребуются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p102">You will also need a site collection in your test SharePoint installation that is configured for anonymous access. If you have an Office 365 Developer Site, there is already a public site collection associated with it that uses a special Public Website site definition. (For more information about the use of Public Websites in Microsoft SharePoint Online, see  [Public Website help for Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).) That site definition is not available for on premises SharePoint installations. So if your test installation is on-premises, you will need:</span></span>
 

 

- <span data-ttu-id="c9dd5-p103">Веб-приложение SharePoint, настроенное для предоставления анонимного доступа. Его необходимо настроить после установки тестируемого Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p103">A SharePoint web application that is configured to allow anonymous access. But this configuration must occur after the SharePoint Add-in that you are testing has been installed.</span></span>
    
 
- <span data-ttu-id="c9dd5-p104">Семейство веб-сайтов в веб-приложении, которое также настроено для предоставления анонимного доступа. Его необходимо настроить после установки тестируемого Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p104">A site collection within the web application that is itself configured for anonymous access. But this configuration must occur after the SharePoint Add-in that you are testing has been installed.</span></span>
    
 
- <span data-ttu-id="c9dd5-120">Если ваша надстройка размещается в SharePoint и имеет доступ к списку SharePoint, это значит, что список в семействе веб-сайтов настроен для анонимного доступа.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-120">If your add-in is SharePoint-hosted and accesses a SharePoint list, a list in the site collection that is configured for anonymous access.</span></span>
    
 
<span data-ttu-id="c9dd5-121">Инструкции для этих задач находятся в разделе [Настройка веб-приложения, семейства веб-сайтов и списка SharePoint для анонимного доступа](#Configuring).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-121">Instructions for these tasks are in the section  [Configuring an SharePoint web application and site collection and list for anonymous access](#Configuring).</span></span>
 

 

## <a name="limitations-on-the-use-of-sharepoint-add-ins-by-anonymous-users"></a><span data-ttu-id="c9dd5-122">Ограничения на использование надстроек SharePoint анонимными пользователями</span><span class="sxs-lookup"><span data-stu-id="c9dd5-122">Limitations on the use of SharePoint Add-ins by anonymous users</span></span>

<span data-ttu-id="c9dd5-123">При разработке надстройки SharePoint учитывайте следующие факты:</span><span class="sxs-lookup"><span data-stu-id="c9dd5-123">Consider the following facts as you design your SharePoint Add-in:</span></span>
 

 

- <span data-ttu-id="c9dd5-p105">Если Надстройка SharePoint запускается из SharePoint, оно должно содержать дополнительное действие, часть надстройки или должно запускаться с помощью настраиваемой ссылки на странице. Это связано с тем, что анонимные пользователи не могут запускать надстройку с помощью ее плитки. Для запуска надстроек с помощью плитки используется специальная  [страница приложения](http://msdn.microsoft.com/library/685c8e01-b163-4b5e-888c-421d9ecbb25e%28Office.15%29.aspx), недоступная анонимным пользователям. Другой вариант позволить запускать надстройку за пределами SharePoint, при этом требуется использовать политику авторизации только для надстройки.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p105">If the SharePoint Add-in is launched from SharePoint, it has to include a custom action or an add-in part, or it must be launched from a custom link on a page. This is because anonymous users cannot launch the add-in by its tile. The mechanism by which add-ins are launched from the tile requires the use of a special  [application page](http://msdn.microsoft.com/library/685c8e01-b163-4b5e-888c-421d9ecbb25e%28Office.15%29.aspx) that is not accessible to anonymous users. Another option is to make the add-in launchable from outside SharePoint, in which case it has to use theadd-in-only authorization policy.</span></span>
    
 
- <span data-ttu-id="c9dd5-p106">Анонимные пользователи могут только запускать надстройки SharePoint, установленные другими. Это связано с тем, что анонимные пользователи не могут открывать страницу **Добавление надстройки**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p106">An anonymous user can only launch SharePoint Add-ins that have been installed by others. This is because anonymous users cannot open the  **Add an Add-in** page.</span></span>
    
 
- <span data-ttu-id="c9dd5-p107">Когда вошедший в систему пользователь переходит на веб-сайт в локальном веб-приложении SharePoint, настроенном для анонимного доступа, удостоверение пользователя меняется на **системную учетную запись**. С помощью этого удостоверения устанавливать надстройки SharePoint нельзя. Так как анонимные пользователи также не могут устанавливать надстройки, это означает, что если веб-приложение настроено для анонимного доступа, никто не сможет установить надстройки SharePoint. Соответственно, следует установить надстройки SharePoint на веб-сайты в веб-приложении SharePoint до настройки анонимного доступа в веб-приложении. Чтобы установить другие надстройки позже, необходимо временно отключить анонимный доступ в веб-приложении. Это позволит устанавливать надстройки пользователю, вошедшему в систему.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p107">When a logged in user navigates to a website in an on-premises SharePoint web application that has been configured for anonymous access, the user's identity changes to  **System Account**. This identity cannot install SharePoint Add-ins. Since anonymous users also cannot install add-ins, this means that nobody can install a SharePoint Add-ins when the web application is configured for anonymous access. Accordingly, SharePoint Add-ins should be installed to websites in the SharePoint web application before the web application is configured for anonymous access. If other add-ins need to be installed later, the web application must be temporarily changed to disable anonymous access so that the add-ins can be installed by a logged in user.</span></span>
    
 
- <span data-ttu-id="c9dd5-p108">Чтобы разрешить использование интерфейсов API REST службы поиска SharePoint на локальном веб-сайте SharePoint, необходимо настроить XML запроса. Дополнительные сведения см. в статье о  [включении анонимных запросов поиска REST](http://msdn.microsoft.com/library/office/jj163876.aspx#bk_AnonymousREST).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p108">To enable the SharePoint Search REST APIs in an on-premises SharePoint website, you to configure some query XML. For details, see  [Enabling anonymous Search REST queries](http://msdn.microsoft.com/library/office/jj163876.aspx#bk_AnonymousREST).</span></span>
    
 
- <span data-ttu-id="c9dd5-p109">Данные на сайте надстройки не обходятся индексаторами поиска, поэтому пользовательские данные необходимо развернуть удаленно или на хост-сайте. Это относится ко всем Надстройки SharePoint, но мы решили упомянуть об этом, так как в приложениях с анонимным доступом часто требуются функции поиска.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p109">Data on the add-in web is not crawled by the search indexers, so custom data must be deployed remotely or in the host web. This applies to all SharePoint Add-ins, but we note it here because add-ins intended for anonymous access often require search functionality.</span></span>
    
 

## <a name="creating-provider-hosted-add-ins-that-are-anonymously-accessible"></a><span data-ttu-id="c9dd5-138">Создание надстроек, размещенных у поставщика, которые доступны анонимным пользователям</span><span class="sxs-lookup"><span data-stu-id="c9dd5-138">Creating provider-hosted add-ins that are anonymously accessible</span></span>
<span data-ttu-id="c9dd5-139"><a name="Cloud-hosted"> </a></span><span class="sxs-lookup"><span data-stu-id="c9dd5-139"></span></span>

<span data-ttu-id="c9dd5-p110">Чтобы сделать размещаемую у поставщика надстройку доступной анонимным пользователям, нужно просто настроить ее для использования политики авторизации только для надстройки. При применении этой политики SharePoint даже не включает пользовательский контекст, поэтому не имеет значения, являются ли пользователи анонимными. Администратор клиента, который устанавливает надстройку, должен предоставить субъекту надстройки разрешения для хост-сайта (и любые разрешения для родительского семейства сайтов или родительского клиента). Как и для любых других надстроек, разрешения для доступа к хост-сайту запрашиваются в манифесте надстройки.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p110">Making a provider-hosted add-in accessible to anonymous users is simply a matter of configuring it to use the add-in-only authorization policy. When this policy is used, SharePoint does not even include a user context, so it doesn't matter that the user is anonymous. It is only necessary that the add-in principal is granted any permissions it needs to the host web -- and any it needs to the parent site collection or parent tenancy -- by the tenant administrator that installs the add-in. You request permissions to the host web in the add-in manifest just as you would any add-in.</span></span>
 

 

 <span data-ttu-id="c9dd5-p111">**Примечание.** Если сайт SharePoint доступен анонимным пользователям, то обычно на нем разрешен доступ по протоколу HTTP, а не HTTPS. В этом сценарии при использовании политики только для надстроек существуют потенциальные проблемы для безопасности. Дополнительные сведения и описание способа устранения таких проблем см. в записи блога [Что каждый разработчик должен знать о приложениях SharePoint, CSOM и анонимных сайтах публикации](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p111">**Note**  If the SharePoint site is accessible to anonymous users, it typically allows HTTP access, rather than HTTPS. There are potential security issues when the add-in-only policy is used for add-ins in this scenario. For details and a method of mitigating them, see  [What Every Developer Needs to Know About SharePoint Add-ins, CSOM, and Anonymous Publishing Sites](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span></span>
 

<span data-ttu-id="c9dd5-147">Для разработки надстройки, использующей политику только для надстроек, необходимо выполнить две вещи:</span><span class="sxs-lookup"><span data-stu-id="c9dd5-147">Designing an add-in to use the add-in-only policy requires two things:</span></span>
 

 

- <span data-ttu-id="c9dd5-148">Вы должны добавить строку `AllowAppOnlyPolicy="true"` в элемент **AppPermissionRequests**, находящийся в манифесте надстройки.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-148">You must add  `AllowAppOnlyPolicy="true"` to the **AppPermissionRequests** element in the add-in manifest.</span></span>
    
 
- <span data-ttu-id="c9dd5-p112">Код должен запрашивать маркер доступа только для надстроек с сервера авторизации OAuth. Если вы работаете с управляемым кодом, существуют API-интерфейсы, предназначенные специально для этой цели и размещенные в файлах кода, созданных Инструменты разработчика Microsoft Office для Visual Studio: SharePointContext.cs (или с расширением VB) и TokenHelper.cs (или с расширением VB).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p112">Your code must ask for an add-in-only access token from the OAuth authorization server. If you are working with managed code, there are APIs specifically created for this purpose in the code files that are generated by Microsoft Office Developer Tools for Visual Studio: SharePointContext.cs (or .vb) and TokenHelper.cs (or .vb).</span></span>
    
 
<span data-ttu-id="c9dd5-151">Дополнительные сведения о политике только для надстройки (с фрагментами кода), разрешениях для надстроек и манифесте надстройки см. в следующих темах:</span><span class="sxs-lookup"><span data-stu-id="c9dd5-151">For details about the add-in-only policy (with code snippets), add-in permissions, and the add-in manifest see these topics:</span></span>
 

 

-  [<span data-ttu-id="c9dd5-152">Типы политик авторизации надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9dd5-152">Add-in authorization policy types in SharePoint</span></span>](add-in-authorization-policy-types-in-sharepoint.md)
    
 
-  [<span data-ttu-id="c9dd5-153">Разрешения для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9dd5-153">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint.md)
    
 
-  [<span data-ttu-id="c9dd5-154">Изучение структуры манифеста приложения и пакета надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9dd5-154">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md)
    
 

## <a name="creating-sharepoint-hosted-add-ins-that-are-anonymously-accessible"></a><span data-ttu-id="c9dd5-155">Создание надстроек, размещенных в SharePoint, которые доступны анонимным пользователям</span><span class="sxs-lookup"><span data-stu-id="c9dd5-155">Creating SharePoint-hosted add-ins that are anonymously accessible</span></span>
<span data-ttu-id="c9dd5-156"><a name="SP-hosted"> </a></span><span class="sxs-lookup"><span data-stu-id="c9dd5-156"></span></span>

<span data-ttu-id="c9dd5-p113">Для создания размещенной в SharePoint надстройки, которую могут запускать анонимные пользователи, не требуются специальные методики. Ее можно создать так же, как любую другую надстройку, размещенную в SharePoint. Дополнительные сведения см. в статьях  [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md) и [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p113">Creating a SharePoint-hosted add-in that can be run by anonymous users does not require any special techniques. You create it the same way you would create any SharePoint-hosted add-in. For details, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md) and [Complete basic operations using JavaScript library code in SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md).</span></span>
 

 
<span data-ttu-id="c9dd5-p114">Для предоставления анонимным пользователям доступа к надстройке, размещенной в SharePoint, важно то, что семейство сайтов SharePoint Online настраивает администратор клиента, чтобы разрешить анонимный доступ. Разработчик надстройки не может выполнить такую настройку в надстройке, удаленном приемнике событий надстройки или в инфраструктуре установке надстройки для SharePoint. Вы можете добавить настраиваемый список или библиотеку в надстройку, но Язык CAML не предоставляет возможностей для предварительной настройки анонимного доступа. Поэтому его придется настроить после установки надстройки.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p114">What's really crucial for making a SharePoint-hosted add-in usable by anonymous access is that the SharePoint Online site collection is configured by a tenant administrator to allow anonymous access. There is no way that you as a developer of a SharePoint-hosted add-in can make this configuration from the add-in, or a remote add-in event receiver, or with the SharePoint add-in installation infrastructure. You can include a custom list or library in the add-in, but Collaborative Application Markup Language (CAML) does not provide any way to preconfigure it for anonymous access, so it would have to be configured after the add-in is installed.</span></span>
 

 
<span data-ttu-id="c9dd5-p115">Если для продажи своей надстройки вы используете Магазин Office, и существенная часть потенциальных клиентов сочтет ее полезной при наличии доступа для анонимных пользователей, то в этом случае следует указать это требование в описании надстройки. Кроме того, рекомендуется добавить указанную ниже версию процедуры **настройки семейства веб-сайтов SharePoint Online для анонимного доступа** на страницу поддержки вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p115">If you are marketing your add-in through the Office Store, and a significant portion of your potential customers would find the add-in most useful if it is accessible to anonymous users, then you should consider mentioning this configuration requirement in your add-in description. Consider also including a version of the procedure  **To configure a SharePoint Online site collection for anonymous access** below in your add-in's support page.</span></span>
 

 
<span data-ttu-id="c9dd5-p116">Если ваша надстройка использует объектную модель JavaScript (JSOM) в SharePoint, существует одно очень важное требование к конфигурации. По умолчанию анонимным пользователям доступна только малая часть API JSOM. Для доступа к другим API у пользователей должно быть разрешение **Использование удаленных интерфейсов**, которое отсутствует у анонимных пользователей. Это требование необходимо отключить в родительском семействе веб-сайтов или родительском веб-приложении SharePoint веб-сайта, на котором установлена надстройка, как описано в разделе [Настройка веб-приложения, семейства веб-сайтов и списка SharePoint для анонимного доступа](#Configuring).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p116">If your add-in uses SharePoint's JavaScript object model (JSOM), there is one configuration requirement that is very crucial. Only a very small portion of the JSOM APIs are accessible by default to anonymous users. All others require that a user have the  **Use Remote Interfaces** permission and anonymous users do not have this permission. This requirement has to be turned off in the parent site collection or parent SharePoint web application of the website where the add-in is installed, as described in [Configuring an SharePoint web application and site collection and list for anonymous access](#Configuring).</span></span>
 

 

 <span data-ttu-id="c9dd5-p117">**Примечание.** Отключение требования наличия разрешения **Использование удаленных интерфейсов** у пользователей влияет на конфиденциальность информации. Дополнительные сведения см. в записи блога [о том, что каждый разработчик должен знать о приложениях SharePoint, CSOM и анонимных сайтах публикации](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p117">**Note**  Turning off the requirement that users have the  **Use Remote Interfaces** permission has implications for information privacy. For details, see [What Every Developer Needs to Know About SharePoint Add-ins, CSOM, and Anonymous Publishing Sites](http://blogs.msdn.com/b/kaevans/archive/2013/10/24/what-every-developer-needs-to-know-about-sharepoint-apps-csom-and-anonymous-publishing-sites.aspx).</span></span>
 


## <a name="limitations-of-sharepoint-hosted-add-ins-for-anonymous-users"></a><span data-ttu-id="c9dd5-171">Ограничения, налагаемые на надстройки, размещенные в SharePoint и доступные для анонимных пользователей</span><span class="sxs-lookup"><span data-stu-id="c9dd5-171">Limitations of SharePoint-hosted add-ins for anonymous users</span></span>
<span data-ttu-id="c9dd5-172"><a name="SP-hosted"> </a></span><span class="sxs-lookup"><span data-stu-id="c9dd5-172"></span></span>

<span data-ttu-id="c9dd5-173">Будем честны: надстройки, размещаемые в SharePoint и доступные для анонимных пользователей, имеют несколько важных ограничений, которые необходимо учитывать:</span><span class="sxs-lookup"><span data-stu-id="c9dd5-173">We'll be honest with you: there are some significant limitations on SharePoint-hosted add-ins for anonymous users that you need to be aware of:</span></span>
 

 

- <span data-ttu-id="c9dd5-p118">Невозможно сделать список или библиотеку в SharePoint Online доступными анонимным пользователям. Соответственно, API-интерфейсы JSOM, взаимодействующие со списками и библиотеками, не работают в SharePoint Online для анонимных пользователей.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p118">It is not possible to make a list or library on a SharePoint Online accessible to anonymous users. Accordingly, JSOM APIs that involve interaction with lists or libraries do not work on SharePoint Online for anonymous users.</span></span>
    
 
- <span data-ttu-id="c9dd5-p119">Размещенная в SharePoint надстройка, установленная на  *локальном*  веб-сайте SharePoint, может использовать все API JSOM. Тем не менее необходимо *вручную*  настроить веб-приложение, семейство сайтов и его списки и библиотеки для анонимного доступа, а требование наличия разрешения на **использование удаленных интерфейсов** следует отключить. Если надстройка устанавливает настраиваемые списки и библиотеки на сайт надстройки, то пользователям необходимо вручную настроить их для анонимного доступа после установки надстройки.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p119">A SharePoint-hosted add-in installed to an  *on-premises*  SharePoint website can make use all of the JSOM APIs. However, the web application, site collection, and lists/libraries must be *manually*  configured for anonymous access, and the **Use Remote Interfaces** permission requirement must be disabled. If the add-in installs custom lists/libraries to the add-in web, users are responsible for manually configuring these for anonymous access after add-in installation.</span></span>
    
 
- <span data-ttu-id="c9dd5-179">Так как данные на сайте надстройки не обходятся индексаторами поиска и не существует способа установки настраиваемых списков или библиотек на хост-сайте, а у размещенных в SharePoint надстроек не может быть удаленных компонентов или приемников событий, пользовательские данные в размещенной в SharePoint надстройке недоступны для поиска.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-179">Because data on the add-in web is not crawled by the search indexers, and because there is no way to install custom lists or libraries to the host web, and because SharePoint-hosted add-ins cannot have remote components or event receivers, custom data in a SharePoint-hosted add-in is not searchable.</span></span>
    
 

## <a name="configuring-an-sharepoint-web-application-and-site-collection-and-list-for-anonymous-access"></a><span data-ttu-id="c9dd5-180">Настройка веб-приложения, семейства веб-сайтов и списка SharePoint для анонимного доступа</span><span class="sxs-lookup"><span data-stu-id="c9dd5-180">Configuring an SharePoint web application and site collection and list for anonymous access</span></span>
<span data-ttu-id="c9dd5-181"><a name="Configuring"> </a></span><span class="sxs-lookup"><span data-stu-id="c9dd5-181"></span></span>

<span data-ttu-id="c9dd5-p120">Если тестовая установка SharePoint расположена в локальной среде, необходимо выполнить первые две процедуры, представленные ниже, чтобы проверить, доступно ли ваше Надстройка SharePoint анонимным пользователям. Пользователи, устанавливающие ваше Надстройка SharePoint, также должны выполнить эти процедуры для родительского семейства сайтов и веб-приложения любого веб-сайта, на котором установлено ваше Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p120">If your test SharePoint installation is on-premises, you must carry out the first two procedures below in order to test whether your SharePoint Add-in can be used by anonymous users. The customers who install your SharePoint Add-in must also carry out these procedures for the parent site collection and web application of any website where your SharePoint Add-in is installed.</span></span>
 

 

 <span data-ttu-id="c9dd5-p121">**Важно!** Если это возможно, установите надстройку SharePoint на веб-сайт *до* выполнения первых двух процедур. Невозможно установить надстройки на какой-либо веб-сайт в локальном веб-приложении SharePoint, если это веб-приложение было настроено для анонимного доступа. Если оно уже настроено для анонимного доступа, то чтобы установить надстройку, необходимо временно отключить анонимный доступ.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p121">**Important**  If possible, you should install the SharePoint Add-in to a website  *before*  you carry out the first two procedures. Add-ins cannot be installed to any website in an on-premise SharePoint web application when the web application has been configured for anonymous access. If the web application has already been configured for anonymous access, you have to reverse that setting temporarily in order to install the add-in.</span></span>
 


### <a name="to-configure-the-parent-web-application-for-anonymous-access"></a><span data-ttu-id="c9dd5-187">Настройка родительского веб-приложения для анонимного доступа </span><span class="sxs-lookup"><span data-stu-id="c9dd5-187">To configure the parent web application for anonymous access</span></span>


1. <span data-ttu-id="c9dd5-188">В **центре администрирования** выберите **Управление приложениями**, а затем — **Управление веб-приложениями**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-188">In  **Central Administration**, choose  **Application Management**, and then  **Manage Web Applications**.</span></span>
    
 
2. <span data-ttu-id="c9dd5-p122">(Необязательно) Если вы не хотите разрешать анонимный доступ для существующих веб-приложений SharePoint, создайте новое веб-приложение. (Хотя на форме создания веб-приложения можно разрешить анонимный доступ,  *не используйте соответствующий параметр*  . Анонимный доступ следует включать только *после*  установки Надстройка SharePoint.) Дополнительные сведения см. в статье [Create a web application in SharePoint](http://msdn.microsoft.com/library/121c8d83-a508-4437-978b-303096aa59df.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p122">(Optional) If you don't want to allow anonymous access for any of the existing SharePoint web applications, create a new web application. (Although the web application creation form gives you the option of allowing anonymous access,  *do not use this option*  . Anonymous access should not be enabled until *after*  the SharePoint Add-in is installed.) For details, see [Create a web application in SharePoint](http://msdn.microsoft.com/library/121c8d83-a508-4437-978b-303096aa59df.aspx).</span></span>
    
 
3. <span data-ttu-id="c9dd5-192">В списке веб-приложений выберите приложение, которое необходимо сделать доступным для анонимных пользователей, и выберите на ленте команду **Поставщики проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-192">On the list of web applications, select the one that is to be accessible by anonymous users, and select  **Authentication Providers** on the ribbon.</span></span>
    
 
4. <span data-ttu-id="c9dd5-p123">В открывшейся выноске выберите зону, для которой следует включить анонимный доступ. Как правило, это зона **Интернет** или **По умолчанию**. После этого откроется форма **Изменение параметров проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p123">On the callout that opens, choose the zone for which anonymous access is to be enabled. Typically, this is  **Internet** or **Default**. The  **Edit Authentication** form opens.</span></span>
    
 
5. <span data-ttu-id="c9dd5-p124">Установите флажок **Разрешить анонимный доступ**, если это еще не сделано. Этот параметр задает настройку по умолчанию, которую можно отключить для определенных семейств веб-сайтов. Но если не включить данный параметр для веб-приложения, вы не сможете разрешить анонимный доступ для какого-либо семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p124">Check the  **Enable anonymous access** box, it if isn't enabled already. This sets a default that can be turned off for specific site collections, but if you do not enable this for the web application, you cannot enable it for any site collections.</span></span>
    
 
6. <span data-ttu-id="c9dd5-p125">(Необязательно.) Снимите флажок **Требовать разрешения на использование удаленных интерфейсов**. Это позволит коду и сценариям, выполняемым в контексте анонимного пользователя, совершать вызовы клиентской объектной модели SharePoint в каждом семействе веб-сайтов. Повторно включить это требование для семейств веб-сайтов невозможно. Если оставить флажок установленным, то по умолчанию анонимные пользователи не смогут получить доступ к клиентским объектным моделям, но вы можете отключить это требование (и предоставить доступ) для определенных семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p125">(Optional) Uncheck the  **Require Use Remote Interfaces permission** box. Doing so allows code and script running in the context of an anonymous user to make calls to SharePoint's client object model on every site collection. You cannot re-enable the requirement for any site collections. Leaving the box checked means that by default anonymous users cannot access the client object models, but you can disable the requirement (and give them access) for specific site collections.</span></span>
    
     <span data-ttu-id="c9dd5-p126">**Примечание.** Если вы разрабатываете надстройки SharePoint для анонимных пользователей, этот параметр имеет значение только для надстроек, размещенных в SharePoint. Надстройки SharePoint, размещенные у поставщика и предназначенные для анонимного доступа, используют способ, не зависящий от разрешений пользователей. Дополнительные сведения см. в разделе [Создание надстроек, размещенных у поставщика, которые доступны анонимным пользователям](#Cloud-hosted) выше.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p126">**Note**  In the context of developing SharePoint Add-ins for anonymous users, this setting is only meaningful for SharePoint-hosted add-ins. Provider-hosted SharePoint Add-ins that are designed for anonymous users use a technique that makes the user's permissions irrelevant. For more information about this, see the section  [Creating provider-hosted add-ins that are anonymously accessible](#Cloud-hosted) above.</span></span>
7. <span data-ttu-id="c9dd5-204">Чтобы закрыть форму, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-204">Choose  **Save** to close the form.</span></span>
    
 
8. <span data-ttu-id="c9dd5-205">С выделенным веб-приложением выберите на ленте пункт **Политика анонимного доступа**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-205">With the web application still highlighted, select  **Anonymous Policy** on the ribbon.</span></span>
    
 
9. <span data-ttu-id="c9dd5-p127">В форме **Ограничения для анонимного доступа** выберите зону и убедитесь, что переключатель **Нет** активирован. Если тестируемой надстройке SharePoint требуются права на доступ к данным SharePoint, выберите переключатель **Запретить запись**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p127">In the  **Anonymous Access Restrictions** form, choose the zone and be sure that the **None** radio button is enabled. If the SharePoint Add-in that you are testing needs only read rights to SharePoint data, enable **Deny Write** instead.</span></span>
    
     <span data-ttu-id="c9dd5-208">**Примечание.** Если вы разрабатываете надстройки SharePoint для анонимных пользователей, то это еще один параметр, который имеет значение только для надстроек, размещенных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-208">**Note**  This is another setting that, in the context of developing SharePoint Add-ins for anonymous users, is only meaningful for SharePoint-hosted add-ins.</span></span>
10. <span data-ttu-id="c9dd5-209">Если на этапе 2 вы создали новое веб-приложение, вам необходимо создать в нем семейство веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-209">If you created a new web application in step 2, you have to create a site collection in it.</span></span>
    
 

### <a name="to-configure-an-on-premises-site-collection-for-anonymous-access"></a><span data-ttu-id="c9dd5-210">Настройка локального семейства веб-сайтов для анонимного доступа</span><span class="sxs-lookup"><span data-stu-id="c9dd5-210">To configure an on-premises site collection for anonymous access</span></span>


1. <span data-ttu-id="c9dd5-211">На домашней странице семейства веб-сайтов в веб-приложении выберите значок шестеренки, а затем — пункт **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-211">On the home page of a site collection in the web application, select the gear icon and then  **Site Settings**.</span></span>
    
 
2. <span data-ttu-id="c9dd5-212">В разделе **Пользователи и разрешения** на странице **Параметры сайта** выберите пункт **Разрешения для сайта**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-212">In the  **Users and Permissions** section of the **Site Settings** page, select **Site permissions**.</span></span>
    
 
3. <span data-ttu-id="c9dd5-213">На ленте выберите **Анонимный доступ**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-213">Choose  **Anonymous Access** on the ribbon.</span></span>
    
 
4. <span data-ttu-id="c9dd5-p128">На форме **Анонимный доступ** выберите **Разрешен ко всему сайту** или **Списки и библиотеки** в зависимости от уровня доступа, необходимого для тестируемой надстройки. (Независимо от выбранного параметра анонимные пользователи не смогут получить доступ к списку или библиотеке в надстройке, размещенной в SharePoint, если список или библиотека не были отдельно настроены для анонимного доступа. Ниже показано, как это сделать.)</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p128">On the  **Anonymous Access** form, choose either **Entire Web site** or **Lists and libraries**, depending on the level of access the add-in that you are testing needs. (Regardless of which option you choose, anonymous users cannot access a list or library with a SharePoint-hosted add-in unless the list of library is individually configured to all anonymous access. A procedure below describes how to do this.</span></span>
    
 
5. <span data-ttu-id="c9dd5-p129">Если тестируемой надстройке требуется доступ к клиентской объектной модели SharePoint, убедитесь, что флажок **Требовать разрешения на использование удаленных интерфейсов** *не* установлен. Если флажок недоступен, это значит, что требование было отключено на уровне веб-приложения, что равносильно снятию флажка. (Как было указано в предыдущей процедуре, если вы разрабатываете надстройки SharePoint для анонимных пользователей, то этот параметр имеет значение только для приложений, размещенных в SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p129">If the add-in you are testing needs to access the SharePoint client object model, ensure that the  **Require Use Remote Interfaces permission** box is *not*  checked. If the checkbox is grayed out, then the requirement was turned off at the web application level which has the same effect as the box being unchecked. (As noted in the previous procedure, this setting, in the context of developing SharePoint Add-ins for anonymous users, is only meaningful for SharePoint-hosted apps.)</span></span>
    
 

 <span data-ttu-id="c9dd5-p130">**Важно!** Следующую процедуру можно выполнить на общедоступном веб-сайте в SharePoint Online. (Дополнительные сведения об использовании общедоступных веб-сайтов в Microsoft SharePoint Online см. в статье [Сведения об общедоступных веб-сайтах в Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).)</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p130">**Important**  The following procedure can only be carried out on a public website in SharePoint Online. (For more information about the use of Public Websites in Microsoft SharePoint Online, see  [Public Website help for Office 365](http://office.microsoft.com/en-gb/office365-sharepoint-online-enterprise-help/public-website-help-for-office-365-HA102891740.aspx?CTT=1).)</span></span>
 


### <a name="to-configure-a-sharepoint-online-site-collection-for-anonymous-access"></a><span data-ttu-id="c9dd5-222">Настройка семейства веб-сайтов SharePoint Online для анонимного доступа</span><span class="sxs-lookup"><span data-stu-id="c9dd5-222">To configure a SharePoint Online site collection for anonymous access</span></span>


1. <span data-ttu-id="c9dd5-223">Выполните вход в Office 365 с правами администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-223">Login to Office 365 as a tenant administrator.</span></span>
    
 
2. <span data-ttu-id="c9dd5-p131">В верхнем правом углу домашней страницы семейства веб-сайтов выберите пункт **Сделать веб-сайт общедоступным**. Это действие также отключает параметр **Требовать разрешение на использование удаленных интерфейсов**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p131">On the home page of the site collection, choose  **MAKE WEBSITE ONLINE** near the upper right corner of the page. This action also turns off the **Use Remote Interfaces permission** requirement.</span></span>
    
 
<span data-ttu-id="c9dd5-p132">Если вы разрабатываете размещенную в SharePoint надстройку, которая получает доступ к списку SharePoint, необходимо выполнить указанную ниже процедуру в тестовом семействе сайтов. Пользователи надстройки также должны сделать это на любом веб-сайте, где она установлено. Не существует программного или описательного способа настройки анонимного доступа для списка. Надстройки могут устанавливать настраиваемые списки, но невозможно предварительно настроить анонимный доступ для списков. Настройка выполняется вручную после установки надстройки. Если вы создаете размещенное у поставщика Надстройка SharePoint для анонимных пользователей, эта процедура не требуется.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p132">If you are developing a SharePoint-hosted add-in and it accesses a SharePoint list, you must also carry out the following procedure in your test site collection. Customers who use your add-in will need to do this as well on any website where the add-in is installed. There is no way that an add-in can programmatically or descriptively configure a list for anonymous access. Add-ins can install custom lists, but there is no way to preconfigure such lists for anonymous access. The configuration must still be done manually after the add-in is installed. If you are developing a provider-hosted SharePoint Add-in for anonymous users, this procedure is not required.</span></span>
 

 

 <span data-ttu-id="c9dd5-232">**Примечание.** Данную процедуру невозможно выполнить в семействе веб-сайтов SharePoint Online, поэтому размещенные в SharePoint надстройки, которые установлены в SharePoint Online и предназначены для анонимных пользователей, не смогут получать доступ к спискам и библиотекам.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-232">**Note**  This procedure cannot be carried out in a SharePoint Online site collection, so SharePoint-hosted add-ins that are installed to SharePoint Online and intended for use by anonymous users cannot access lists or libraries.</span></span>
 


### <a name="to-configure-an-list-or-library-for-anonymous-access"></a><span data-ttu-id="c9dd5-233">Настройка списка или библиотеки для анонимного доступа</span><span class="sxs-lookup"><span data-stu-id="c9dd5-233">To configure an list or library for anonymous access</span></span>


1. <span data-ttu-id="c9dd5-p133">Перейдите к списку или библиотеке, к которым обращается тестируемая надстройка SharePoint, и откройте **Параметры списка** или **Параметры библиотеки**. Для сайта SharePoint Online необходимо войти в систему в качестве администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p133">Navigate to a list or library that the SharePoint Add-in that you are testing accesses and open the  **List Settings** or **Library Settings**. For a SharePoint Online site, you must be logged in as a tenant administrator.</span></span>
    
 
2. <span data-ttu-id="c9dd5-236">Выберите **Разрешения для этого списка или библиотеки**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-236">Choose  **Permissions for this list/library**.</span></span>
    
 
3. <span data-ttu-id="c9dd5-237">На открывшейся странице выберите **Прекратить наследование разрешений** на вкладке **Разрешения** и нажмите **ОК** в запросе подтверждения.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-237">On the page that opens, choose  **Stop Inheriting Permissions** on the **Permissions** tab, and then choose **OK** on the confirmation prompt.</span></span>
    
 
4. <span data-ttu-id="c9dd5-238">Выберите **Анонимный доступ** на вкладке **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-238">Choose  **Anonymous Access** on the **Permission** tab.</span></span>
    
 
5. <span data-ttu-id="c9dd5-p134">В открывшейся форме **Анонимный доступ** выберите все разрешения, необходимые пользователям надстройки SharePoint. Вы можете разрешить просмотр, изменение, добавление и удаление элементов. Однако предоставить полный доступ не удастся; это сделано для того, чтобы анонимные пользователи не могли изменить схему или параметры списка.</span><span class="sxs-lookup"><span data-stu-id="c9dd5-p134">On the  **Anonymous Access** form that opens, select all of the permissions that that users of the SharePoint Add-in require. You can grant permission to View, Edit, Add, and Delete items. You cannot grant Full Control, so anonymous users cannot change the schema of the list or change list settings.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="c9dd5-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c9dd5-242">Additional resources</span></span>
<span data-ttu-id="c9dd5-243"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c9dd5-243"></span></span>


-  [<span data-ttu-id="c9dd5-244">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9dd5-244">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 

