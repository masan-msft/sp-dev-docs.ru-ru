---
title: "Подписка на людей в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0fa2e235-63d0-41b1-9eed-4aeb2f59a14d
ms.openlocfilehash: a381aff03097d52cf611cc93adb49904155ae376
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="follow-people-in-sharepoint"></a>Подписка на людей в SharePoint
Сведения о распространенных задач программирования для следующих пользователей в SharePoint.
## <a name="apis-for-following-people-in-sharepoint"></a>API-интерфейсы для следующих пользователей в SharePoint
<a name="bkmk_APIversions"> </a>

Если пользователь людей в SharePoint, микроблога записи в блогах, что публикация людей и уведомлений о их действий отображаются в канале новостей пользователя. Функции, связанные с следующие сотрудники могут просматриваться на страницах **канала новостей** и **людей, у меня есть подписка** .
  
    
    
SharePoint предоставляет следующие интерфейсы API, которые можно использовать для программного подписка на людей.
  
    
    

- Клиентские объектные модели для управляемого кода
    
  - Клиентская объектная модель .NET
    
  
  - Клиентская объектная модель Silverlight
    
  
  - Клиентская объектная модель для мобильных устройств.
    
  
- Объектная модель JavaScript
    
  
- Служба передачи репрезентативного состояния (REST).
    
  
- Объектная модель сервера
    
  
Рекомендуется при разработке для SharePoint при вы можете Используйте клиентские API-интерфейсы. API-интерфейсов клиента включают клиентской объектной модели, объектной модели JavaScript и службы REST. Дополнительные сведения об интерфейсах API в SharePoint и их использовании см. раздел [Выбор право API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Каждый API включает в себя объект диспетчера, который используется для выполнения основных задач для следующих пользователей.
  
> [!NOTE]
> Интерфейса API используются для подписка на контент. [Подписка на контент в SharePoint](follow-content-in-sharepoint.md) в разделе Общие сведения о задачах следующее содержимое.
  
    
    

В таблице 1 приведены диспетчер и другие ключевые объекты (или ресурсы REST) в API-интерфейсы и библиотека классов (или точка доступа) где их можно найти.
  
> [!NOTE]
> [!Примечание] Silverlight и мобильных устройств клиентской объектной модели не включаются явным образом в таблице 1 или в таблице 2, так как они обеспечивают основные функциональные возможности, аналогичные клиентской объектной модели .NET и использовать же цифровые подписи. Клиентская объектная модель Silverlight определяется в Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll и мобильных устройств клиентской объектной модели определяется в Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**В таблице 1. API-интерфейсов SharePoint используются для следующих пользователей программными средствами**

|**API**|**Основные объекты**|
|:-----|:-----|
|Клиентская объектная модель .NET  <br/> См.: [как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)|Объект диспетчера:            [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) <br/> Основное пространство имен:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) <br/> Другие ключевые объекты:            [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) , [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) , [SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) , [SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) <br/> Библиотека классов:           Microsoft.SharePoint.Client.UserProfiles.dll |
|Объектная модель JavaScript  <br/> См.: [как: подписка на людей с помощью объектной модели JavaScript в SharePoint](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)|Объект диспетчера:            [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) <br/> Основное пространство имен:           **SP.Social** <br/> Другие ключевые объекты:            [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx),  [SocialActorInfo](http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx),  [SocialActorType](http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx),  [SocialActorTypes](http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx) <br/> Библиотека классов:           SP.UserProfiles.js |
|Служба REST  <br/> См.: [людей и контент Справочник по интерфейсу API службы REST для SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)|Руководитель ресурсов:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md) <br/> URI конечной точки:            `<siteUri>/_api/social.following` <br/> Основное пространство имен (OData.md): **sp.social.SocialRestFollowingManager** <br/> Другие ключевые ресурсы:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes**|
|Серверная объектная модель. |Объект диспетчера:            [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) <br/> Основное пространство имен:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) <br/> Другие ключевые объекты:            [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) , [SPSocialActorInfo](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx) , [SPSocialActorType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx) , [SPSocialActorTypes](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx) <br/> Библиотека классов:           Microsoft.Office.Server.UserProfiles.dll |
   

## <a name="common-programming-tasks-for-following-people-in-sharepoint"></a>Типичные задачи программирования для следующих пользователей в SharePoint
<a name="bkmk_CommonTasks"> </a>

В таблице 2 перечислены типичные задачи программирования для следующих пользователей и члены, которые можно использовать для их выполнения. Члены: от клиентской объектной модели .NET (CSOM), JavaScript объектной модели (JSOM), служба REST и серверной объектной модели (SSOM).
  
> [!NOTE]
> Интерфейса API используются для подписка на контент. [Подписка на контент в SharePoint](follow-content-in-sharepoint.md) в разделе Общие сведения о задачах следующее содержимое.
  
    
    

Объект **SocialFollowingManager** объединяет основных следующие сотрудники и контента следующие функциональные возможности для текущего пользователя. Тем не менее, объект **PeopleManager** (см. в таблице 3) предоставляет функциональные возможности, **SocialFollowingManager** не предоставляет, включая методы для получения следующие сотрудники состояние других пользователей.
  
    
    

**В таблице 2. API для распространенных задач для следующих пользователей с помощью объекта SocialFollowingManager**


|**Задача**|**Участники**|
|:-----|:-----|
|Создание экземпляра объекта диспетчера в контексте текущего пользователя |CSOM:  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) <br/> **SocialFollowingManager**JSOM: <br/> REST:  `<siteUri>/_api/social.following` <br/> SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)|
|Создайте экземпляр объекта диспетчера в контексте определенного пользователя |CSOM: не реализовано  <br/> JSOM: не реализовано  <br/> REST: не реализовано  <br/> SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) (перегрузка)|
|У текущего пользователя создайте (остановить следующие) другого пользователя |CSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) ) <br/> JSOM:  [выполните](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) ( [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx))  <br/> REST: **POST** [`<siteUri>/_api/social.following/Follow`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Follow) ([`<siteUri>/_api/social.following/StopFollowing`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_StopFollowing)) и передайте параметр _actor_ в теле запроса <br/> SSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx) )|
|Узнать, является ли текущий пользователь является следующие конкретному пользователю |CSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) <br/> JSOM:  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.following/my/IsFollowed`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_IsFollowed) и передайте параметр _actor_ в теле запроса <br/> SSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx)|
|Получить пользователей, которые отслеживаются текущего пользователя |CSOM:  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowers.aspx) <br/> JSOM:  [getFollowers](http://msdn.microsoft.com/library/ae4a944b-c043-05fb-c74b-101d2ce4a813%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/Followers`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followers)<br/> SSOM:  [GetFollowers](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowers.aspx)|
|Получение людей, выполнив текущего пользователя |CSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) <br/> JSOM:  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/Followed(types=1)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed)<br/> SSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx)|
|Получение числа людей, выполнив текущего пользователя |CSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) <br/> JSOM:  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/FollowedCount(types=1)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount)<br/> SSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx)|
|Получить пользователей, которые текущий пользователь может потребоваться выполнить |CSOM:  [GetSuggestions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetSuggestions.aspx) <br/> JSOM:  [getSuggestions](http://msdn.microsoft.com/library/95fd9c48-6974-ec08-d3e9-00c2c76f4f79%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/Suggestions`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Suggestions)<br/> SSOM:  [GetSuggestions](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetSuggestions.aspx)|
   
В таблице 3 показаны элементы **PeopleManager** можно использовать для дополнительных функций следующие сотрудники.
  
    
    

**В таблице 3. API для распространенных задач для следующих пользователей с помощью объекта PeopleManager**


|**Задача**|**Участники**|
|:-----|:-----|
|Узнать ли список **людей, у меня есть подписка** для текущего пользователя общедоступных|CSOM:  [IsMyPeopleListPublic](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.IsMyPeopleListPublic.aspx) <br/> JSOM:  [isMyPeopleListPublic](http://msdn.microsoft.com/library/2ffc73a5-24ce-1ed4-d850-a6fea4c773bb%28Office.15%29.aspx) <br/> REST: [IsMyPeopleListPublic](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerProperties)<br/>Пример: **Получение**`<siteUri>/_api/SP.UserProfiles.PeopleManager/IsMyPeopleListPublic` <br/> SSOM:  [IsMyPeopleListPublic](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.IsMyPeopleListPublic.aspx)|
|Узнать, является ли кто-то после текущего пользователя |CSOM:  [AmIFollowedBy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.AmIFollowedBy.aspx) <br/> JSOM:  [amIFollowedBy](http://msdn.microsoft.com/library/3641c469-0063-054d-355d-e56697cb08ae%28Office.15%29.aspx) <br/> REST: [AmIFollowedBy](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerAmIFollowedBy)<br/>Пример: **Получение**`<siteUri>/_api/SP.UserProfiles.PeopleManager/AmIFollowedBy(accountName=@v)?@v='domain\\user'` <br/> SSOM:  [AmIFollowedBy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.AmIFollowedBy.aspx)|
|Получить пользователей, которые после определенного пользователя |CSOM:  [GetPeopleFollowedBy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPeopleFollowedBy.aspx) <br/> JSOM:  [getPeopleFollowedBy](http://msdn.microsoft.com/library/e781c0fa-b14a-40ef-976b-b1c6c82beb89%28Office.15%29.aspx) <br/> REST: [GetPeopleFollowedBy](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerGetPeopleFollowedBy)<br/>Пример: **Получение**`<siteUri>/_api/SP.UserProfiles.PeopleManager/GetPeopleFollowedBy(accountName=@v)?@v='domain\\user'` <br/> SSOM:  [GetPeopleFollowedBy](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.GetPeopleFollowedBy.aspx)|
|Получить пользователей, которые отслеживаются конкретному пользователю |CSOM:  [GetFollowersFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetFollowersFor.aspx) <br/> JSOM:  [getFollowersFor](http://msdn.microsoft.com/library/51ef3b75-42b2-4efb-4441-e088dc7d168e%28Office.15%29.aspx) <br/> REST: [GetFollowersFor](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerGetFollowersFor)<br/>Пример: **Получение**`<siteUri>/_api/SP.UserProfiles.PeopleManager/GetFollowersFor(accountName=@v)?@v='domain\\user'` <br/> SSOM:  [GetFollowersFor](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.GetFollowersFor.aspx)|
|Узнать, ли конкретному пользователю следующие другому пользователю |CSOM:  [IsFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.IsFollowing.aspx) <br/> JSOM:  [isFollowing](http://msdn.microsoft.com/library/6a5ce6cb-c710-9e19-0cb9-7fae9e013ec8%28Office.15%29.aspx) <br/> REST: [IsFollowing](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerIsFollowing) (статический)<br/>Пример: **Получение**`<siteUri>/_api/SP_UserProfiles_PeopleManager_IsFollowing(possibleFollowerAccountName=@v,possibleFolloweeAccountName=@y)?@v='domain\\user'&amp;@y='domain\\user'` <br/> SSOM:  [IsFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.IsFollowing.aspx)|
   

## <a name="how-people-suggestions-works-on-sharepoint-online"></a>Как работают предложения людей на SharePoint Online
<a name="bk_PeopleSuggestions"> </a>

Результаты для предложений людей зависят от установленных следующие сотрудники активности. Если пользователь пользователем, имеющим mutual ниже с теми, кто пользователь уже не выполнив следующие предложения, предлагается.
  
    
    
Сведения, связанные с ниже индексируется во время обход контента при поиске. По завершении обхода аналитика поиска необходимо анализировать для обхода следующие сведения и выходных данных предложения пользователей. По умолчанию выполните поиск analytics выполняется один раз в день.
  
    
    
Когда пользователь открывает страницу **я отслеживаю**, вызывается метод  [PeopleManager.GetMySuggestions()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMySuggestions.aspx) . [GetMySuggestions](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMySuggestions.aspx) ищет новые предложения для текущего пользователя, обновляет предложений пользователя в базе данных и представляет предложений на странице.
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addResources"> </a>


-  [Социальные функции и функции совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Подписка на контент в SharePoint](follow-content-in-sharepoint.md)
    
  
-  [Справочник по API REST для профилей пользователей](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)
    
  
-  [Как подписываться на пользователей, используя клиентскую объектную модель .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)
    
  
-  [Как подписываться на пользователей, используя объектную модель JavaScript в SharePoint](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)
    
  
-  [Following people and content REST API reference for SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
