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
# <a name="whats-new-for-developers-in-social-and-collaboration-features-in-sharepoint"></a>Новые возможности социальных сетей и совместной работы в SharePoint для разработчиков
Узнайте о новых и измененных возможности социальных вычислений и совместной работы для личных сайтов и веб-узел сообщества сценариев разработки в SharePoint.
Возможности социальных сетей и совместной работы в SharePoint упростить для пользователей для связи и быть в курсе мероприятиям и уведомляться. Улучшенная социальных канал на личных сайтах и сайтах групп помогает пользователям изучить людей и контент фрагментов. Новая функция веб-узел сообщества предоставляют возможности расширенными возможностями сообщества, который позволяет легко найти и обмениваться информацией и найдите те, кто имеет схожими интересами.
  
    
    

Подробный обзор новых социальных сетей и совместной работы функций в SharePoint просмотрите [новые возможности социальных сетей в SharePoint](http://technet.microsoft.com/en-us/library/jj219766%28v=office.15%29) на сайте TechNet. Дополнительные сведения о программировании с использованием возможности социальных сетей и совместной работы можно [возможности социальных сетей и совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md).
## <a name="new-and-changed-my-site-features-in-sharepoint"></a>Новые и измененные функции личного сайта в SharePoint
<a name="bkmk_Social"> </a>

Личный сайт API-Интерфейс, который включает профили пользователей и Социальный контент, содержит множество новых и измененных функций. Новые функции для личных сайтов и веб-сайтов групп обеспечивает интерактивных сообщений в пределах веб-каналов, упрощающая пользователям всегда оставаться на связи для пользователей и контента, которые имеют значения для них.
  
    
    
На странице **канал новостей** на SharePoint отображаются некоторые из этих улучшений, включая текстовое поле, которое позволяет пользователям быстро размещать публикации и микроблога канал интерактивных, естественного публикации и обновляет из людей и контент, который является пользователь следующие.
  
    
    

### <a name="new-social-namespace-provides-apis-for-social-feeds-and-following-people-and-content"></a>Новое пространство имен социальных предоставляет API для социальных веб-каналов и подписки на людей и контент

Пространство имен **Social** содержит основной API для работы с веб-каналов и публикации в микроблога и следующие сотрудники и контента. Для получения дополнительных сведений см [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) для клиентской объектной модели .NET, [SP. Социальные](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) для JavaScript объектной модели и [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) для серверной объектной модели.
  
    
    

> **Примечание:** API в пространстве имен [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) является устаревшим. В разделе [устарел и удаленным социальные API личных сайтов и функций](#bkmk_DeprecatedAPI). 
  
    
    


### <a name="new-client-apis-for-social-feeds-following-people-and-content-and-user-properties-in-sharepoint"></a>Новый клиент API-интерфейсы для социальных каналов следующими свойствами людей и контент и пользователя в SharePoint

SharePoint включает в себя новые клиентские API-интерфейсы, которые можно использовать для работы с социальными веб-каналами, следуйте людей и контента и извлечения свойств пользователя в сети, локальной и разработке для мобильных устройств. По возможности следует использовать клиентские интерфейсы API для разработки SharePoint вместо использования server объектной модели или веб-служб. API-интерфейсов клиента включают управляемой клиентской объектной модели, объектной модели JavaScript и службы представлений состояния (REST). При разработке надстройки SharePoint необходимо использовать API клиента.
  
    
    
Не все функциональные возможности на сервере в сборке Microsoft.Office.Server.UserProfiles доступен из клиентских API-интерфейсов. Например нет нет доступа на стороне клиента API-интерфейса в пространстве имен  [Microsoft.Office.Server.Audience](https://msdn.microsoft.com/library/Microsoft.Office.Server.Audience.aspx) , пространство имен [Microsoft.Office.Server.ReputationModel](https://msdn.microsoft.com/library/Microsoft.Office.Server.ReputationModel.aspx) или пространство имен [Microsoft.Office.Server.SocialData](https://msdn.microsoft.com/library/Microsoft.Office.Server.SocialData.aspx) . Доступные API-интерфейсы см пространства имен [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) и пространства имен [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) .
  
    
    
Сведения о том, как получить доступ к личных сайтов социальных клиентские API в разделе [Приступая к разработке с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md). Дополнительные сведения об API наборах в SharePoint и способы их использования, см. раздел [Выбор право API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    

### <a name="use-the-profileloadercreatepersonalsiteenqueuebulk-method-to-provision-personal-sites-and-onedrive-for-business-for-multiple-users-my-site-host-administrators-on-sharepoint-online-only"></a>Метод ProfileLoader.CreatePersonalSiteEnqueueBulk используется для подготовки личных сайтов и OneDrive для бизнеса для нескольких пользователей (Администраторы узлаЛичный сайт на SharePoint Online только)
<a name="bk_CreatePersonalSiteEnqueueBulk"> </a>

Личный сайт Администраторы узла можно использовать метод **ProfileLoader.CreatePersonalSiteEnqueueBulk** для подготовки личных сайтов для нескольких пользователей на SharePoint Online, которые включают функции, например OneDrive для бизнеса и на странице сайтов программными средствами.
  
    
    
В следующем примере кода используется клиентская объектная модель .NET в консольное приложение. Перед запуском в примере добавьте ссылки на Microsoft.SharePoint.Client.dll, Microsoft.SharePoint.Client.Runtime.dll и библиотеке Microsoft.SharePoint.Client.UserProfiles.dll и измените значения заполнителей для переменных **userName**, **passwordStr**и **serverUrl**. Переменная **serverUrl** должен быть URL-адрес SharePoint Online центра администрирования.
  
    
    

> **Примечание:** Чтобы получить требуемый клиент библиотеки DLL, загрузите пакет [SDK для компонентов SharePoint Online клиента](http://www.microsoft.com/en-us/download/details.aspx?id=42038). 
  
    
    




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

Чтобы использовать метод **CreatePersonalSiteEnqueueBulk** с Windows PowerShell, сначала измените значения заполнитель (URL-адрес SharePoint Online Центр администрирования и имена пользователей) в следующие команды и выполните команды в Командная консоль SharePoint.
  
    
    



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

Дополнительные сведения можно [, чтобы программными средствами подготовки личных сайтов (One Drive для бизнеса) в Office 365?](http://blogs.msdn.com/b/frank_marasco/archive/2014/03/25/so-you-want-to-programmatically-provision-personal-sites-one-drive-for-business-in-office-365.aspx) и [Использования Windows PowerShell для администрирования SharePoint](http://technet.microsoft.com/en-us/library/ee806878%28v=office.15%29.aspx).
  
    
    

### <a name="new-objects-for-users-and-user-properties-in-sharepoint"></a>Новые объекты для пользователей и свойства пользователей в SharePoint
<a name="bkmk_NewUserObjects"> </a>

SharePoint включает в себя новые объекты, которые представляют пользователей и свойств пользователя:
  
    
    

- Объект  [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) представляет пользователей (и других сущностей) для веб-канала активности и следующие действия.
    
  
- Объект  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) содержит общие пользователя и свойств профиля пользователя.
    
  

> **Примечание:** Server объектной модели версии являются [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) и [PersonProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PersonProperties.aspx) объектов.
  
    
    

SharePoint также включает в себя новый объект [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) со стороны клиента, который предоставляет методы, которые можно использовать для создания личного сайта для текущего пользователя. Тем не менее он не содержит все свойства пользователей, которые содержит объект [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) на сервере. Для доступа к все свойства пользователя из клиентского кода, используйте метод [PeopleManager.GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) или метод [PeopleManager.GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) (профиль пользователя, который свойства хранятся в [PersonProperties.UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) свойство) или используйте [PeopleManager.GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) метод или метод [PeopleManager.GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) .
  
    
    

### <a name="new-client-side-people-picker-control"></a>Новый элемент управления средства выбора людей со стороны клиента
<a name="bkmk_NewUserObjects"> </a>

Элемент управления "Выбор людей" со стороны клиента является элементом управления HTML и JavaScript, который обеспечивает поддержку браузеров для выбора пользователей, групп и утверждений. Можно настроить средство выбора с теми же настройками, как на сервере версию элемента управления, включая свойства этого элемента управления (например, позволяя пользователи или пользователи и группы) и веб-параметров конфигурации на уровне приложения (например, параметры Доменные службы Active Directory или определения отдельного леса). Для получения дополнительных сведений см  [Использование клиентского элемента управления "Выбор людей" в надстройках для SharePoint с размещением в SharePoint](http://msdn.microsoft.com/library/383f265f-ed44-4d09-b2f6-366f13d52347%28Office.15%29.aspx).
  
    
    

### <a name="deprecated-and-removed-my-site-social-api-and-features"></a>Устаревшие и удаленным Личный сайт API и функции
<a name="bkmk_DeprecatedAPI"> </a>

Следующие личных сайтов социальных API и функции поддерживаются в SharePoint:
  
    
    

- API в пространстве имен [Microsoft.Office.Server.ActivityFeed](https://msdn.microsoft.com/library/Microsoft.Office.Server.ActivityFeed.aspx) является устаревшим. **Социальные** пространство имен предоставляет API для Программная работа с социальными веб-каналами в SharePoint. Для обеспечения обратной совместимости, **событие ActivityEvent** элементы из SharePoint 2010 отображаются в качестве события, которые не могут быть дан ответ каналов SharePoint. (Миграцию события должна быть включена в центре администрирования).
    
  
- Новые интерфейсы API в службе REST, клиентской объектной модели и объектной моделью JavaScript заменяется Личный сайт RSS-канал (ActivityFeed.aspx). Перенос пользовательских SharePoint 2010 код, использующий этот интерфейс API (желательно клиента API), замените все запросы на ActivityFeed.aspx звонков на новые API и веб-канала данных, которые возвращаются в формате Нотация объектов JavaScript (JSON) маркер.
    
  
- Веб-часть **Последние действия** заменяется новой веб-части **канала новостей**, который поддерживает многопоточные бесед и динамическое извлечение веб-канала активности.
    
    > **Примечание:** Мы не поддерживаем использование настроек веб-части канала новостей или другом веб-канал веб-частей (например, сайт веб-канал веб-часть на веб-сайтов групп). Если настроить эти веб-части, например с помощью JavaScript переопределений, обратите внимание, что настройки могут быть разорваны в обновления для SharePoint. 
- Веб-часть **Социальных комментариев** является устаревшим.
    
  
- Следующие события активности больше не будет автоматически сообщить веб-канал: профиля обновления, предстоящие день рождения, предстоящие годовщина работы, новые членства и изменение диспетчера. Тем не менее можно создать приемники настраиваемых событий для этих действий. Новые события социальных не были добавлены.
    
  
- Рекомендуется использовать следующие поля в перечислении [конфиденциальности](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.Privacy.aspx) : **Контакты**, название **организации**и **Manager**. SharePoint предоставляет только **частных** ( **Только я**) и **общедоступных** ( **все**) параметры конфиденциальности. Существующие параметры конфиденциальности, сохраняются до их изменения пользователем. Чтобы перенести пользовательского кода SharePoint 2010, которая использует этот интерфейс API, замените все ссылки на поля не рекомендуемые для использования конфиденциальности.
    
  
- **Следующие сотрудники** API, доступного из **SocialFollowingManager** заменяющей функциональность **коллег** из SharePoint Server 2010. Страница **коллеги** заменяется **я отслеживаю** страницы. Функция **групп**, которая позволяет пользователям организации коллег в группы больше не доступен.
    
  
- Профили организаций являются устаревшими в SharePoint и устаревшие следующих типов: **OrganizationProfile**, **OrganizationProfileManager**, **OrganizationMembershipType**, **OrganizationNotFoundException**, ** OrganizationProfileChange**, **OrganizationProfileChangeQuery**, **OrganizationProfileMembershipChange**и **OrganizationProfileValueCollection**.
    
  
- Функция **Мои ссылки** , удаленные в SharePoint.
    
  

## <a name="new-community-site-feature-in-sharepoint"></a>Новая функция веб-узел сообщества в SharePoint
<a name="bkmk_Collab"> </a>

Новая функция веб-узел сообщества включает в себя новый шаблон сайта и улучшение качества обсуждений. Функции такие как репутации, категории, основные вопросы, тип вопрос post и ответов на наиболее позволяют членам сообщества легко найти популярные обсуждения, информацию и людей со схожими интересами. Члены построения репутации, как они участвовать в сообществах.
  
    
    
Компонент веб-узел сообщества не предоставляют доступ к определенным API для разработки. Чтобы расширить возможности веб-узел сообщества, используется сайт SharePoint и список API-интерфейсы непосредственно. Например можно использовать API-интерфейсов SharePoint шаблоны сайтов и списков, создания пользовательских действий из сообществ для социальных веб-канал, интегрировать сведения о репутации в результатах поиска, настроить модели репутации или создавать рабочие процессы для Модерация обсуждений.
  
    
    
Следующий список содержит сведения о разработке с использованием функций веб-узел сообщества:
  
    
    

- Сайты сообщества используют шаблон сайта **Community** ( [Id](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.WebTemplate.Id.aspx) = **62**). Шаблон сайта недоступен для общедоступных веб-сайтов. Тип шаблона списка доска обсуждений   [DiscussionBoard](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.ListTemplateType.DiscussionBoard.aspx) (значение = **108**).
    
  
- Активация компонента **Веб-узел сообщества** активирует **CommunityEventReceiver** приемника событий.
    
  
- Для настройки представления отрисовки списка со стороны клиента, необходимо использовать переопределений JavaScript для замены в представление. Не удается расширить представлений списка с помощью SharePoint API. Для получения дополнительных сведений см [представления списка в SharePoint надстройки с использованием обработки на стороне клиента](http://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86%28Office.15%29.aspx).
    
  
- Сайты сообществ использовать асинхронные события для обновления объектов. Асинхронные события выполняются в фоновом режиме, может привести  *Сохранить*  конфликтов при обновлении списки или элементы списка и дескриптор объекта могут стать устаревших.
    
    В качестве решения обработки исключений, возвращаемых вызовов **Update** обновить экземпляр перед повторить вызов и цикл для нескольких повторных попыток, как показано в следующем примере кода.
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15NewSocial_addlresources"> </a>


-  [Социальные функции и функции совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Новые возможности для разработчиков в SharePoint](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [Новые возможности социальных сетей в SharePoint](http://technet.microsoft.com/en-us/library/jj219766%28v=office.15%29)
    
  

