---
title: "Новые возможности социальных сетей и совместной работы в SharePoint для разработчиков"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 65365b1d-cde5-47cd-8b04-1b76be0e3490
ms.openlocfilehash: e07b0d576b096667251b2aff377593bae634823e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-for-developers-in-social-and-collaboration-features-in-sharepoint"></a><span data-ttu-id="c91cf-102">Новые возможности социальных сетей и совместной работы в SharePoint для разработчиков</span><span class="sxs-lookup"><span data-stu-id="c91cf-102">What's new for developers in social and collaboration features in SharePoint</span></span>
<span data-ttu-id="c91cf-103">Узнайте о новых и измененных возможности социальных вычислений и совместной работы для личных сайтов и веб-узел сообщества сценариев разработки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c91cf-103">Learn about new and changed social and collaboration features for My Site and Community Site development scenarios in SharePoint.</span></span>
<span data-ttu-id="c91cf-104">Возможности социальных сетей и совместной работы в SharePoint упростить для пользователей для связи и быть в курсе мероприятиям и уведомляться.</span><span class="sxs-lookup"><span data-stu-id="c91cf-104">Social and collaboration features in SharePoint make it easy for users to communicate and to stay engaged and informed.</span></span> <span data-ttu-id="c91cf-105">Улучшенная социальных канал на личных сайтах и сайтах групп помогает пользователям изучить людей и контент фрагментов.</span><span class="sxs-lookup"><span data-stu-id="c91cf-105">The improved social feed on personal sites and team sites helps users to keep up-to-date with the people and content that they care about.</span></span> <span data-ttu-id="c91cf-106">Новая функция веб-узел сообщества предоставляют возможности расширенными возможностями сообщества, который позволяет легко найти и обмениваться информацией и найдите те, кто имеет схожими интересами.</span><span class="sxs-lookup"><span data-stu-id="c91cf-106">The new Community Site feature provides a rich community experience that lets users easily find and share information and find people who have similar interests.</span></span>
  
    
    

<span data-ttu-id="c91cf-107">Подробный обзор новых социальных сетей и совместной работы функций в SharePoint просмотрите [новые возможности социальных сетей в SharePoint](http://technet.microsoft.com/ru-ru/library/jj219766%28v=office.15%29) на сайте TechNet.</span><span class="sxs-lookup"><span data-stu-id="c91cf-107">For an in-depth overview of the new social and collaboration features in SharePoint, see  [What's new in social computing in SharePoint](http://technet.microsoft.com/ru-ru/library/jj219766%28v=office.15%29) on TechNet.</span></span> <span data-ttu-id="c91cf-108">Дополнительные сведения о программировании с использованием возможности социальных сетей и совместной работы можно [возможности социальных сетей и совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c91cf-108">For more information about programming with social and collaboration features, see [Social and collaboration features in SharePoint](social-and-collaboration-features-in-sharepoint.md).</span></span>
## <a name="new-and-changed-my-site-features-in-sharepoint"></a><span data-ttu-id="c91cf-109">Новые и измененные функции личного сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-109">New and changed My Site features in SharePoint</span></span>
<span data-ttu-id="c91cf-110"><a name="bkmk_Social"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-110"><a name="bkmk_Social"> </a></span></span>

<span data-ttu-id="c91cf-p103">Личный сайт API-Интерфейс, который включает профили пользователей и Социальный контент, содержит множество новых и измененных функций. Новые функции для личных сайтов и веб-сайтов групп обеспечивает интерактивных сообщений в пределах веб-каналов, упрощающая пользователям всегда оставаться на связи для пользователей и контента, которые имеют значения для них.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p103">The My Site Social API, which includes user profiles and social data, contains many new and changed features. New functionality for My Sites and team sites provides an interactive, conversational experience within feeds that makes it easier for users to stay connected to the people and content that matter to them.</span></span>
  
    
    
<span data-ttu-id="c91cf-113">На странице **канал новостей** на SharePoint отображаются некоторые из этих улучшений, включая текстовое поле, которое позволяет пользователям быстро размещать публикации и микроблога канал интерактивных, естественного публикации и обновляет из людей и контент, который является пользователь следующие.</span><span class="sxs-lookup"><span data-stu-id="c91cf-113">The **Newsfeed** page on SharePoint displays several of these improvements, including a text box that enables users to quickly publish microblog posts and an interactive, conversational feed of posts and updates from the people and content that the user is following.</span></span>
  
    
    

### <a name="new-social-namespace-provides-apis-for-social-feeds-and-following-people-and-content"></a><span data-ttu-id="c91cf-114">Новое пространство имен социальных предоставляет API для социальных веб-каналов и подписки на людей и контент</span><span class="sxs-lookup"><span data-stu-id="c91cf-114">New Social namespace provides APIs for social feeds and following people and content</span></span>

<span data-ttu-id="c91cf-p104">Пространство имен **Social** содержит основной API для работы с веб-каналов и публикации в микроблога и следующие сотрудники и контента. Для получения дополнительных сведений см [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) для клиентской объектной модели .NET, [SP. Социальные](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) для JavaScript объектной модели и [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) для серверной объектной модели.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p104">The **Social** namespace contains the primary API for working with feeds and microblog posts and for following people and content. For more information, see [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) for the .NET client object model, [SP.Social](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) for the JavaScript object model, and [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) for the server object model.</span></span>
  
    
    

> <span data-ttu-id="c91cf-117">**Примечание:** API в пространстве имен [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="c91cf-117">**Note:** The API in the  [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) namespace is deprecated.</span></span> <span data-ttu-id="c91cf-118">В разделе [устарел и удаленным социальные API личных сайтов и функций](#bkmk_DeprecatedAPI).</span><span class="sxs-lookup"><span data-stu-id="c91cf-118">See [Deprecated and removed My Site Social API and features](#bkmk_DeprecatedAPI).</span></span> 
  
    
    


### <a name="new-client-apis-for-social-feeds-following-people-and-content-and-user-properties-in-sharepoint"></a><span data-ttu-id="c91cf-119">Новый клиент API-интерфейсы для социальных каналов следующими свойствами людей и контент и пользователя в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-119">New client APIs for social feeds, following people and content, and user properties in SharePoint</span></span>

<span data-ttu-id="c91cf-120">SharePoint включает в себя новые клиентские API-интерфейсы, которые можно использовать для работы с социальными веб-каналами, следуйте людей и контента и извлечения свойств пользователя в сети, локальной и разработке для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="c91cf-120">SharePoint includes new client APIs that you can use to work with social feeds, follow people and content, and retrieve user properties in online, on-premises, and mobile development.</span></span> <span data-ttu-id="c91cf-121">По возможности следует использовать клиентские интерфейсы API для разработки SharePoint вместо использования server объектной модели или веб-служб.</span><span class="sxs-lookup"><span data-stu-id="c91cf-121">When possible, you should use client APIs for SharePoint development instead of using the server object model or web services.</span></span> <span data-ttu-id="c91cf-122">API-интерфейсов клиента включают управляемой клиентской объектной модели, объектной модели JavaScript и службы представлений состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="c91cf-122">Client APIs include managed client object models, a JavaScript object model, and a Representational State Transfer (REST) service.</span></span> <span data-ttu-id="c91cf-123">При разработке надстройки SharePoint необходимо использовать API клиента.</span><span class="sxs-lookup"><span data-stu-id="c91cf-123">If you are developing an SharePoint Add-in, you must use a client API.</span></span>
  
    
    
<span data-ttu-id="c91cf-p107">Не все функциональные возможности на сервере в сборке Microsoft.Office.Server.UserProfiles доступен из клиентских API-интерфейсов. Например нет нет доступа на стороне клиента API-интерфейса в пространстве имен  [Microsoft.Office.Server.Audience](https://msdn.microsoft.com/library/Microsoft.Office.Server.Audience.aspx) , пространство имен [Microsoft.Office.Server.ReputationModel](https://msdn.microsoft.com/library/Microsoft.Office.Server.ReputationModel.aspx) или пространство имен [Microsoft.Office.Server.SocialData](https://msdn.microsoft.com/library/Microsoft.Office.Server.SocialData.aspx) . Доступные API-интерфейсы см пространства имен [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) и пространства имен [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c91cf-p107">Not all server-side functionality in the Microsoft.Office.Server.UserProfiles assembly is available from client APIs. For example, there's no client-side access to the API in the  [Microsoft.Office.Server.Audience](https://msdn.microsoft.com/library/Microsoft.Office.Server.Audience.aspx) namespace, the [Microsoft.Office.Server.ReputationModel](https://msdn.microsoft.com/library/Microsoft.Office.Server.ReputationModel.aspx) namespace, or the [Microsoft.Office.Server.SocialData](https://msdn.microsoft.com/library/Microsoft.Office.Server.SocialData.aspx) namespace. To see which APIs are available, see the [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) namespace and the [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) namespace.</span></span>
  
    
    
<span data-ttu-id="c91cf-127">Сведения о том, как получить доступ к личных сайтов социальных клиентские API в разделе [Приступая к разработке с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c91cf-127">For information about how to access the My Site Social client APIs, see  [Get started developing with social features in SharePoint](get-started-developing-with-social-features-in-sharepoint.md).</span></span> <span data-ttu-id="c91cf-128">Дополнительные сведения об API наборах в SharePoint и способы их использования, см. раздел [Выбор право API в SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c91cf-128">For more information about the API sets in SharePoint and when to use them, see  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    

### <a name="use-the-profileloadercreatepersonalsiteenqueuebulk-method-to-provision-personal-sites-and-onedrive-for-business-for-multiple-users-my-site-host-administrators-on-sharepoint-online-only"></a><span data-ttu-id="c91cf-129">Метод ProfileLoader.CreatePersonalSiteEnqueueBulk используется для подготовки личных сайтов и OneDrive для бизнеса для нескольких пользователей (Администраторы узлаЛичный сайт на SharePoint Online только)</span><span class="sxs-lookup"><span data-stu-id="c91cf-129">Use the ProfileLoader.CreatePersonalSiteEnqueueBulk method to provision personal sites and OneDrive for Business for multiple users (My Site Host administrators on SharePoint Online only)</span></span>
<span data-ttu-id="c91cf-130"><a name="bk_CreatePersonalSiteEnqueueBulk"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-130"><a name="bk_CreatePersonalSiteEnqueueBulk"> </a></span></span>

<span data-ttu-id="c91cf-131">Личный сайт Администраторы узла можно использовать метод **ProfileLoader.CreatePersonalSiteEnqueueBulk** для подготовки личных сайтов для нескольких пользователей на SharePoint Online, которые включают функции, например OneDrive для бизнеса и на странице сайтов программными средствами.</span><span class="sxs-lookup"><span data-stu-id="c91cf-131">My Site Host administrators can use the **ProfileLoader.CreatePersonalSiteEnqueueBulk** method to programmatically provision personal sites for multiple users on SharePoint Online, which include features such as OneDrive for Business and the Sites page.</span></span>
  
    
    
<span data-ttu-id="c91cf-p109">В следующем примере кода используется клиентская объектная модель .NET в консольное приложение. Перед запуском в примере добавьте ссылки на Microsoft.SharePoint.Client.dll, Microsoft.SharePoint.Client.Runtime.dll и библиотеке Microsoft.SharePoint.Client.UserProfiles.dll и измените значения заполнителей для переменных **userName**, **passwordStr**и **serverUrl**. Переменная **serverUrl** должен быть URL-адрес SharePoint Online центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p109">The following code example uses the .NET client object model in a console application. Before you run the example, add references to Microsoft.SharePoint.Client.dll, Microsoft.SharePoint.Client.Runtime.dll and Microsoft.SharePoint.Client.UserProfiles.dll, and change the placeholder values for the **userName**, **passwordStr**, and **serverUrl** variables. The **serverUrl** variable must be the URL of the SharePoint Online Administration Center.</span></span>
  
    
    

> <span data-ttu-id="c91cf-135">**Примечание:** Чтобы получить требуемый клиент библиотеки DLL, загрузите пакет [SDK для компонентов SharePoint Online клиента](http://www.microsoft.com/en-us/download/details.aspx?id=42038).</span><span class="sxs-lookup"><span data-stu-id="c91cf-135">**Note:** To get the required client DLLs, download the  [SharePoint Online Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038).</span></span> 
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Security;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.UserProfiles;

namespace CreatePersonalSiteBulkConsole
{
    class Program
    {
        static void Main(string[] args)
        {
            string userName = "administrator@contoso.onmicrosoft.com";
            string passwordStr = "password";
            string serverUrl = "https://contoso-admin.sharepoint.com/";

            using (var clientContext = new ClientContext(serverUrl))
            {
                SecureString password = new SecureString();
                Array.ForEach(passwordStr.ToCharArray(), c => password.AppendChar(c));

                var credentials = new SharePointOnlineCredentials(userName, password);

                clientContext.Credentials = credentials;

                var web = clientContext.Web;
                clientContext.Load(web);
                clientContext.ExecuteQuery();
                ProfileLoader loader = ProfileLoader.GetProfileLoader(clientContext);

                if (loader == null)
                {
                    throw new InvalidOperationException("Failed to get ProfileLoader");
                }

                string[] userEmails = { "usera@contoso.onmicrosoft.com", "userb@contoso.onmicrosoft.com" };
                loader.CreatePersonalSiteEnqueueBulk(userEmails);
                loader.Context.ExecuteQuery();
            }
        }
    }
}
```

<span data-ttu-id="c91cf-136">Чтобы использовать метод **CreatePersonalSiteEnqueueBulk** с Windows PowerShell, сначала измените значения заполнитель (URL-адрес SharePoint Online Центр администрирования и имена пользователей) в следующие команды и выполните команды в Командная консоль SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c91cf-136">To use the **CreatePersonalSiteEnqueueBulk** method with Windows PowerShell, first change the placeholder values (the URL of the SharePoint Online Administration Center and user names) in the following commands, and then run the commands in the SharePoint Management Shell.</span></span>
  
    
    



```

$webUrl = "https://yoursharepointadmin.sharepoint.com"
$ctx = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)

$web = $ctx.Web
$username = "admin@myadmin.sharepoint.com"
$password = read-host -AsSecureString

$ctx.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($username,$password)

$ctx.Load($web)
$ctx.ExecuteQuery()

[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SharePoint.Client.UserProfiles")

$loader =[Microsoft.SharePoint.Client.UserProfiles.ProfileLoader]::GetProfileLoader($ctx)

#To get profile
$profile = $loader.GetUserProfile()
$ctx.Load($profile)
$ctx.ExecuteQuery()
$profile 
#To enqueue profile
$loader.CreatePersonalSiteEnqueueBulk(@("user1@domain.com")) 
$loader.Context.ExecuteQuery()
```

<span data-ttu-id="c91cf-137">Дополнительные сведения можно [, чтобы программными средствами подготовки личных сайтов (One Drive для бизнеса) в Office 365?](http://blogs.msdn.com/b/frank_marasco/archive/2014/03/25/so-you-want-to-programmatically-provision-personal-sites-one-drive-for-business-in-office-365.aspx) и [Использования Windows PowerShell для администрирования SharePoint](http://technet.microsoft.com/ru-ru/library/ee806878%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91cf-137">For more information, see  [So you want to programmatically provision Personal Sites (One Drive for Business) in Office 365?](http://blogs.msdn.com/b/frank_marasco/archive/2014/03/25/so-you-want-to-programmatically-provision-personal-sites-one-drive-for-business-in-office-365.aspx) and [Use Windows PowerShell to administer SharePoint](http://technet.microsoft.com/ru-ru/library/ee806878%28v=office.15%29.aspx).</span></span>
  
    
    

### <a name="new-objects-for-users-and-user-properties-in-sharepoint"></a><span data-ttu-id="c91cf-138">Новые объекты для пользователей и свойства пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-138">New objects for users and user properties in SharePoint</span></span>
<span data-ttu-id="c91cf-139"><a name="bkmk_NewUserObjects"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-139"><a name="bkmk_NewUserObjects"> </a></span></span>

<span data-ttu-id="c91cf-140">SharePoint включает в себя новые объекты, которые представляют пользователей и свойств пользователя:</span><span class="sxs-lookup"><span data-stu-id="c91cf-140">SharePoint includes new objects that represent users and user properties:</span></span>
  
    
    

- <span data-ttu-id="c91cf-141">Объект  [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) представляет пользователей (и других сущностей) для веб-канала активности и следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c91cf-141">The  [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) object represents users (and other entities) for feed and following activities.</span></span>
    
  
- <span data-ttu-id="c91cf-142">Объект  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) содержит общие пользователя и свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="c91cf-142">The  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) object contains general user properties and user profile properties.</span></span>
    
  

> <span data-ttu-id="c91cf-143">**Примечание:** Server объектной модели версии являются [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) и [PersonProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PersonProperties.aspx) объектов.</span><span class="sxs-lookup"><span data-stu-id="c91cf-143">**Note:** Server object model versions are the  [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) object and the [PersonProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PersonProperties.aspx) object.</span></span>
  
    
    

<span data-ttu-id="c91cf-144">SharePoint также включает в себя новый объект [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) со стороны клиента, который предоставляет методы, которые можно использовать для создания личного сайта для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="c91cf-144">SharePoint also includes a new client-side  [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) object that provides methods you can use to create a personal site for the current user.</span></span> <span data-ttu-id="c91cf-145">Тем не менее он не содержит все свойства пользователей, которые содержит объект [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) на сервере.</span><span class="sxs-lookup"><span data-stu-id="c91cf-145">However, it does not contain all the user properties that the server-side [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) object contains.</span></span> <span data-ttu-id="c91cf-146">Для доступа к все свойства пользователя из клиентского кода, используйте метод [PeopleManager.GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) или метод [PeopleManager.GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) (профиль пользователя, который свойства хранятся в [PersonProperties.UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) свойство) или используйте [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) метод или метод [PeopleManager.GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c91cf-146">To access all user properties from client-side code, use the [PeopleManager.GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) method or [PeopleManager.GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) method (user profile properties are stored in the [PersonProperties.UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) property) or use the [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) method or [PeopleManager.GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) method.</span></span>
  
    
    

### <a name="new-client-side-people-picker-control"></a><span data-ttu-id="c91cf-147">Новый элемент управления средства выбора людей со стороны клиента</span><span class="sxs-lookup"><span data-stu-id="c91cf-147">New client-side people picker control</span></span>
<span data-ttu-id="c91cf-148"><a name="bkmk_NewUserObjects"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-148"><a name="bkmk_NewUserObjects"> </a></span></span>

<span data-ttu-id="c91cf-p111">Элемент управления "Выбор людей" со стороны клиента является элементом управления HTML и JavaScript, который обеспечивает поддержку браузеров для выбора пользователей, групп и утверждений. Можно настроить средство выбора с теми же настройками, как на сервере версию элемента управления, включая свойства этого элемента управления (например, позволяя пользователи или пользователи и группы) и веб-параметров конфигурации на уровне приложения (например, параметры Доменные службы Active Directory или определения отдельного леса). Для получения дополнительных сведений см  [Использование клиентского элемента управления "Выбор людей" в надстройках для SharePoint с размещением в SharePoint](http://msdn.microsoft.com/library/383f265f-ed44-4d09-b2f6-366f13d52347%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91cf-p111">The client-side People Picker control is an HTML and JavaScript control that provides cross-browser support for selecting people, groups, and claims. You can configure the picker with the same settings as the server-side version of the control, including control-specific properties (like allowing multiple users or users and groups) and web application-level configuration settings (like Active Directory Domain Services parameters or targeting particular forests). For more information, see  [Use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins](http://msdn.microsoft.com/library/383f265f-ed44-4d09-b2f6-366f13d52347%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="deprecated-and-removed-my-site-social-api-and-features"></a><span data-ttu-id="c91cf-152">Устаревшие и удаленным Личный сайт API и функции</span><span class="sxs-lookup"><span data-stu-id="c91cf-152">Deprecated and removed My Site Social API and features</span></span>
<span data-ttu-id="c91cf-153"><a name="bkmk_DeprecatedAPI"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-153"><a name="bkmk_DeprecatedAPI"> </a></span></span>

<span data-ttu-id="c91cf-154">Следующие личных сайтов социальных API и функции поддерживаются в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="c91cf-154">The following My Site Social API and features are deprecated in SharePoint:</span></span>
  
    
    

- <span data-ttu-id="c91cf-155">API в пространстве имен [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="c91cf-155">The API in the  [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) namespace is deprecated.</span></span> <span data-ttu-id="c91cf-156">**Социальные** пространство имен предоставляет API для Программная работа с социальными веб-каналами в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c91cf-156">The **Social** namespace provides the API for programmatically working with social feeds in SharePoint.</span></span> <span data-ttu-id="c91cf-157">Для обеспечения обратной совместимости, **событие ActivityEvent** элементы из SharePoint 2010 отображаются в качестве события, которые не могут быть дан ответ каналов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c91cf-157">For backward compatibility, **ActivityEvent** items from SharePoint 2010 are displayed in SharePoint feeds as events that cannot be replied to.</span></span> <span data-ttu-id="c91cf-158">(Миграцию события должна быть включена в центре администрирования).</span><span class="sxs-lookup"><span data-stu-id="c91cf-158">(Legacy event migration must be enabled in Central Administration.)</span></span>
    
  
- <span data-ttu-id="c91cf-p113">Новые интерфейсы API в службе REST, клиентской объектной модели и объектной моделью JavaScript заменяется Личный сайт RSS-канал (ActivityFeed.aspx). Перенос пользовательских SharePoint 2010 код, использующий этот интерфейс API (желательно клиента API), замените все запросы на ActivityFeed.aspx звонков на новые API и веб-канала данных, которые возвращаются в формате Нотация объектов JavaScript (JSON) маркер.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p113">The My Site RSS feed (ActivityFeed.aspx) is replaced with new APIs in the REST service, the client object model, and the JavaScript object model. To migrate custom SharePoint 2010 code that uses this API (preferably a client API), replace all requests to ActivityFeed.aspx with calls to the new API and handle feed data that is returned in JavaScript Object Notation (JSON) format.</span></span>
    
  
- <span data-ttu-id="c91cf-161">Веб-часть **Последние действия** заменяется новой веб-части **канала новостей**, который поддерживает многопоточные бесед и динамическое извлечение веб-канала активности.</span><span class="sxs-lookup"><span data-stu-id="c91cf-161">The **Recent Activities** Web Part is replaced with a new **Newsfeed** Web Part that supports multithreaded conversations and dynamic feed retrieval.</span></span>
    
    > <span data-ttu-id="c91cf-162">**Примечание:** Мы не поддерживаем использование настроек веб-части канала новостей или другом веб-канал веб-частей (например, сайт веб-канал веб-часть на веб-сайтов групп).</span><span class="sxs-lookup"><span data-stu-id="c91cf-162">**Note:** We don't support customizations of the Newsfeed Web Part or other feed Web Parts (such as the Site Feed Web Part on team sites).</span></span> <span data-ttu-id="c91cf-163">Если настроить эти веб-части, например с помощью JavaScript переопределений, обратите внимание, что настройки могут быть разорваны в обновления для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c91cf-163">If you do customize these Web Parts, for example by using JavaScript overrides, be aware that your customizations may break in updates to SharePoint.</span></span> 
- <span data-ttu-id="c91cf-164">Веб-часть **Социальных комментариев** является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="c91cf-164">The **Social Comments** Web Part is deprecated.</span></span>
    
  
- <span data-ttu-id="c91cf-p115">Следующие события активности больше не будет автоматически сообщить веб-канал: профиля обновления, предстоящие день рождения, предстоящие годовщина работы, новые членства и изменение диспетчера. Тем не менее можно создать приемники настраиваемых событий для этих действий. Новые события социальных не были добавлены.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p115">The following activity events no longer automatically inform the feed: profile update, upcoming birthday, upcoming workplace anniversary, new membership, and change of manager. However, you can create custom event receivers for these activities. No new social events have been added.</span></span>
    
  
- <span data-ttu-id="c91cf-168">Рекомендуется использовать следующие поля в перечислении [конфиденциальности](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.Privacy.aspx) : **Контакты**, название **организации**и **Manager**.</span><span class="sxs-lookup"><span data-stu-id="c91cf-168">The following fields in the  [Privacy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.Privacy.aspx) enumeration are deprecated: **Contacts**, **Organization**, and **Manager**.</span></span> <span data-ttu-id="c91cf-169">SharePoint предоставляет только **частных** ( **Только я**) и **общедоступных** ( **все**) параметры конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="c91cf-169">SharePoint offers only **Private** ( **Only Me**) and **Public** ( **Everyone**) privacy settings.</span></span> <span data-ttu-id="c91cf-170">Существующие параметры конфиденциальности, сохраняются до их изменения пользователем.</span><span class="sxs-lookup"><span data-stu-id="c91cf-170">Existing privacy settings are retained until they are changed by the user.</span></span> <span data-ttu-id="c91cf-171">Чтобы перенести пользовательского кода SharePoint 2010, которая использует этот интерфейс API, замените все ссылки на поля не рекомендуемые для использования конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="c91cf-171">To migrate custom SharePoint 2010 code that uses this API, replace all references to the deprecated privacy fields.</span></span>
    
  
- <span data-ttu-id="c91cf-p117">**Следующие сотрудники** API, доступного из **SocialFollowingManager** заменяющей функциональность **коллег** из SharePoint Server 2010. Страница **коллеги** заменяется **я отслеживаю** страницы. Функция **групп**, которая позволяет пользователям организации коллег в группы больше не доступен.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p117">The **Following People** API that is accessed from the **SocialFollowingManager** replaces the **Colleagues** functionality from SharePoint Server 2010. The **Colleagues** page is replaced with the **People I'm following** page. The **Groups** feature that enabled users to organize colleagues into groups is no longer available.</span></span>
    
  
- <span data-ttu-id="c91cf-175">Профили организаций являются устаревшими в SharePoint и устаревшие следующих типов: **OrganizationProfile**, **OrganizationProfileManager**, **OrganizationMembershipType**, **OrganizationNotFoundException**, ** OrganizationProfileChange**, **OrganizationProfileChangeQuery**, **OrganizationProfileMembershipChange**и **OrganizationProfileValueCollection**.</span><span class="sxs-lookup"><span data-stu-id="c91cf-175">Organization profiles are obsolete in SharePoint, and the following types are deprecated: **OrganizationProfile**, **OrganizationProfileManager**, **OrganizationMembershipType**, **OrganizationNotFoundException**, **OrganizationProfileChange**, **OrganizationProfileChangeQuery**, **OrganizationProfileMembershipChange**, and **OrganizationProfileValueCollection**.</span></span>
    
  
- <span data-ttu-id="c91cf-176">Функция **Мои ссылки** , удаленные в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c91cf-176">The **My Links** feature is deprecated in SharePoint.</span></span>
    
  

## <a name="new-community-site-feature-in-sharepoint"></a><span data-ttu-id="c91cf-177">Новая функция веб-узел сообщества в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-177">New Community Site feature in SharePoint</span></span>
<span data-ttu-id="c91cf-178"><a name="bkmk_Collab"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-178"><a name="bkmk_Collab"> </a></span></span>

<span data-ttu-id="c91cf-p118">Новая функция веб-узел сообщества включает в себя новый шаблон сайта и улучшение качества обсуждений. Функции такие как репутации, категории, основные вопросы, тип вопрос post и ответов на наиболее позволяют членам сообщества легко найти популярные обсуждения, информацию и людей со схожими интересами. Члены построения репутации, как они участвовать в сообществах.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p118">The new Community Site feature includes a new site template and improved discussion experience. Features such as reputation, categories, featured discussions, a question-post type, and best replies let community members easily find popular discussions, relevant information, and people with similar interests. Members build reputation as they participate in communities.</span></span>
  
    
    
<span data-ttu-id="c91cf-p119">Компонент веб-узел сообщества не предоставляют доступ к определенным API для разработки. Чтобы расширить возможности веб-узел сообщества, используется сайт SharePoint и список API-интерфейсы непосредственно. Например можно использовать API-интерфейсов SharePoint шаблоны сайтов и списков, создания пользовательских действий из сообществ для социальных веб-канал, интегрировать сведения о репутации в результатах поиска, настроить модели репутации или создавать рабочие процессы для Модерация обсуждений.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p119">The Community Site feature does not expose a specific API for development. To extend Community Site features, you use SharePoint site and list APIs directly. For example, you can use SharePoint APIs to customize the site and list templates, create custom activities from communities for the social feed, integrate reputation information into search results, customize the reputation model, or create workflows to moderate discussions.</span></span>
  
    
    
<span data-ttu-id="c91cf-185">Следующий список содержит сведения о разработке с использованием функций веб-узел сообщества:</span><span class="sxs-lookup"><span data-stu-id="c91cf-185">The following list contains information for developing with Community Site features:</span></span>
  
    
    

- <span data-ttu-id="c91cf-p120">Сайты сообщества используют шаблон сайта **Community** ( [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WebTemplate.Id.aspx) = **62**). Шаблон сайта недоступен для общедоступных веб-сайтов. Тип шаблона списка доска обсуждений   [DiscussionBoard](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ListTemplateType.DiscussionBoard.aspx) (значение = **108**).</span><span class="sxs-lookup"><span data-stu-id="c91cf-p120">Community Sites use the **Community** site template ( [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WebTemplate.Id.aspx) = **62**). The site template is not available for public websites. The template type of the discussion board list is  [DiscussionBoard](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ListTemplateType.DiscussionBoard.aspx) (value = **108**).</span></span>
    
  
- <span data-ttu-id="c91cf-189">Активация компонента **Веб-узел сообщества** активирует **CommunityEventReceiver** приемника событий.</span><span class="sxs-lookup"><span data-stu-id="c91cf-189">Activating the **Community Site** feature activates the **CommunityEventReceiver** event receiver.</span></span>
    
  
- <span data-ttu-id="c91cf-190">Для настройки представления отрисовки списка со стороны клиента, необходимо использовать переопределений JavaScript для замены в представление.</span><span class="sxs-lookup"><span data-stu-id="c91cf-190">To customize the client-side rendered list view, you must use JavaScript overrides to replace the view.</span></span> <span data-ttu-id="c91cf-191">Не удается расширить представлений списка с помощью SharePoint API.</span><span class="sxs-lookup"><span data-stu-id="c91cf-191">List views cannot be extended through the SharePoint API.</span></span> <span data-ttu-id="c91cf-192">Для получения дополнительных сведений см [представления списка в SharePoint надстройки с использованием обработки на стороне клиента](http://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91cf-192">For more information, see  [Customize a list view in SharePoint Add-ins using client-side rendering](http://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="c91cf-p122">Сайты сообществ использовать асинхронные события для обновления объектов. Асинхронные события выполняются в фоновом режиме, может привести  *Сохранить*  конфликтов при обновлении списки или элементы списка и дескриптор объекта могут стать устаревших.</span><span class="sxs-lookup"><span data-stu-id="c91cf-p122">Community Sites use asynchronous events to update objects. If asynchronous events run in the background, you may encounter  *Save*  conflicts when you attempt to update lists or list items, and your handle to the object may become stale.</span></span>
    
    <span data-ttu-id="c91cf-195">В качестве решения обработки исключений, возвращаемых вызовов **Update** обновить экземпляр перед повторить вызов и цикл для нескольких повторных попыток, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="c91cf-195">As a workaround, handle exceptions that are returned by **Update** calls, refresh the instance before you retry the call, and loop for multiple retries, as shown in the following code example.</span></span>
    


```cs
  
int retries = 1;
while (retries <= 10)
{
    try
    {
        spListItem.IconOverlay = urlString;
        spListItem.Update();
        break;
    }
    catch (SPException saveConflict)
    {
        spListItem = web.Lists.GetItemById(spListItem.ID);
        retries++;
        if (retries > 10) throw;
        System.Threading.Thread.Sleep(1000);
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="c91cf-196">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c91cf-196">Additional resources</span></span>
<span data-ttu-id="c91cf-197"><a name="SP15NewSocial_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c91cf-197"><a name="SP15NewSocial_addlresources"> </a></span></span>


-  [<span data-ttu-id="c91cf-198">Социальные функции и функции совместной работы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-198">Social and collaboration features in SharePoint</span></span>](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c91cf-199">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-199">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c91cf-200">Новые возможности для разработчиков в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-200">What's new for developers in SharePoint</span></span>](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c91cf-201">Новые возможности социальных сетей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c91cf-201">What's new in social computing in SharePoint</span></span>](http://technet.microsoft.com/ru-ru/library/jj219766%28v=office.15%29)
    
  

