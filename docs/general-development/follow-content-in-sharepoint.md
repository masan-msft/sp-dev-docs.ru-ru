---
title: "Подписка на контент в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 30e68cd6-6e55-4cf9-afd6-7139b0a97288
ms.openlocfilehash: e670bd3dbf8c50a98c1ac5c5599b565bd42aef7e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="follow-content-in-sharepoint"></a>Подписка на контент в SharePoint
Узнайте о типичные задачи программирования для следующее содержимое (документы, сайты и теги) в SharePoint.
## <a name="apis-for-following-content-in-sharepoint"></a>API-интерфейсы для следующих контента в SharePoint
<a name="bkmk_APIversions"> </a>

Когда пользователи выполнения документы, сайты или теги, обновлений состояния из документов, бесед на сайты и уведомления тега использовать показа в их канала новостей. Функции, связанные с следующее содержимое может отображаться на **канал новостей** и на **следующих** страницах контента.
  
    
    
SharePoint предоставляет следующие интерфейсы API, которые можно использовать для программного выполнения контента:
  
    
    

- Клиентские объектные модели для управляемого кода
    
  - Клиентская объектная модель .NET
    
  
  - Клиентская объектная модель Silverlight
    
  
  - Клиентская объектная модель для мобильных устройств.
    
  
- Объектная модель JavaScript
    
  
- Служба передачи репрезентативного состояния (REST).
    
  
- Объектная модель сервера
    
  
Рекомендуется при разработке для SharePoint при вы можете Используйте клиентские API-интерфейсы. API-интерфейсов клиента включают клиентской объектной модели, объектной модели JavaScript и службы REST. Дополнительные сведения об интерфейсах API в SharePoint и их использовании см. раздел [Выбор право API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    
Каждый API включает в себя объект диспетчера, используемая для выполнения основных задач по следующее содержимое.
  
> [!NOTE]
> Же API используются следить за людьми. [Подписка на людей в SharePoint](follow-people-in-sharepoint.md) в разделе Общие сведения о задачах следующие сотрудники.
  
    
    

В таблице 1 приведены диспетчер и другие ключевые объекты (или ресурсы REST) в API-интерфейсы и библиотека классов (или точка доступа) где их можно найти.
  
> [!NOTE]
> [!Примечание] Модель Silverlight и мобильная клиентская объектная модель не включены в таблицу 1 или таблицу 2, так как они предоставляют такой же основной функционал, как и клиентская объектная модель .NET, и одинаковые подписи. Клиентская объектная модель Silverlight определена в Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll, а мобильная клиентская объектная модель  в Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**В таблице 1. API-интерфейсов SharePoint используется для следующих содержимого программным путем**

|**API**|**Основные объекты**|
|:-----|:-----|
|Клиентская объектная модель .NET  <br/> См.: [как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)|Объект диспетчера:            [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) <br/> Основное пространство имен:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) <br/> Другие ключевые объекты:            [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) , [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) , [SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) , [SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx) <br/> Библиотека классов:           Microsoft.SharePoint.Client.UserProfiles.dll  |
|Объектная модель JavaScript|Объект диспетчера:            [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) <br/> Основное пространство имен:            [SP. Социальные](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx) <br/> Другие ключевые объекты:            [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx),  [SocialActorInfo](http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx),  [SocialActorType](http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx),  [SocialActorTypes](http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx) <br/> Библиотека классов:           SP.UserProfiles.js  |
|Служба REST  <br/> Просмотреть [как: с помощью службы REST в SharePoint, выполните документы, сайты и тегов](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)|Руководитель ресурсов:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md) <br/> Основное пространство имен (OData):           **sp.social.SocialRestFollowingManager** <br/> Другие ключевые ресурсы:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes** <br/> Точка доступа:            `<siteUri>/_api/social.following` |
|Серверная объектная модель.|Объект диспетчера:            [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) <br/> Основное пространство имен:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx) <br/> Другие ключевые объекты:            [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) , [SPSocialActorInfo](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx) , [SPSocialActorType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx) , [SPSocialActorTypes](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx) <br/> Библиотека классов:           Microsoft.Office.Server.UserProfiles.dll  |
   

## <a name="common-programming-tasks-for-following-content-in-sharepoint"></a>Типичные задачи программирования для следующих контента в SharePoint
<a name="bkmk_CommonTasks"> </a>

В таблице 2 перечислены типичные задачи программирования для следующее содержимое и элементы, которые можно использовать для их выполнения. Члены: от клиентской объектной модели .NET (CSOM), JavaScript объектной модели (JSOM), служба REST и серверной объектной модели (SSOM).
  
> [!NOTE]
> Же API используются следить за людьми. [Подписка на людей в SharePoint](follow-people-in-sharepoint.md) в разделе Общие сведения о задачах следующие сотрудники.
  
    
    


**В таблице 2. API для распространенных задач для следующих контента в SharePoint**


|**Задача**|**Участники**|
|:-----|:-----|
|Создание экземпляра объекта диспетчера в контексте текущего пользователя|CSOM:  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx) <br/> JSOM:  [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx) <br/> REST:  `<siteUri>/_api/social.following` <br/> SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)|
|Создайте экземпляр объекта диспетчера в контексте указанного пользователя|CSOM: не реализовано  <br/> JSOM: не реализовано  <br/> REST: не реализовано  <br/> SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) (перегрузка)|
|У текущего пользователя создайте (остановить следующие) элемента|CSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) ) <br/> JSOM:  [выполните](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) ( [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx))  <br/> REST: **POST** [`<siteUri>/_api/social.following/Follow`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Follow) ( [`<siteUri>/_api/social.following/StopFollowing`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_StopFollowing)) и передайте параметр _actor_ в теле запроса <br/> SSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx) )|
|Узнать, является ли текущий пользователь является после определенного элемента|CSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx) <br/> JSOM:  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx) <br/> REST: **POST** [`<siteUri>/_api/social.following/IsFollowed`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_IsFollowed) и передайте параметр _actor_ в теле запроса <br/> SSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx)|
|Получение документы, сайты и/или теги, выполнив текущего пользователя|CSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx) <br/> JSOM:  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx) <br/> REST: **Получение** [`<siteUri>/_api/social.following/my/Followed(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed) (документы = **2**, сайты = **4**, теги = публикацию повторно **8**)  <br/> SSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx)|
|Получение числа документы, сайты и/или теги, на которые подписан пользователь|CSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx) <br/> JSOM:  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx) <br/> REST: **Получение** [`<siteUri>/_api/social.following/my/FollowedCount(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount) (документы = **2**, сайты = **4**, теги = публикацию повторно **8**)  <br/> SSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx)|
|Получение URI-адрес сайта, в котором приведены число документов текущего пользователя|CSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedDocumentsUri.aspx) <br/> JSOM:  [followedDocumentsUri](http://msdn.microsoft.com/library/3a70b9c7-abd7-94ff-d730-70298673d6ec%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/FollowedDocumentsUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedDocumentsUri) <br/> SSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedDocumentsUri.aspx)|
|Получение URI-адрес сайта, в котором приведены число сайтов текущего пользователя|CSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedSitesUri.aspx) <br/> JSOM:  [followedSitesUri](http://msdn.microsoft.com/library/829404bc-1b3a-7545-5e95-0922df330084%28Office.15%29.aspx) <br/> REST: **GET** [`<siteUri>/_api/social.following/my/FollowedSitesUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedSitesUri) <br/> SSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedSitesUri.aspx)|
   
> [!NOTE]
> Примеры, показывающие, как использовать службы REST для подписка на контент, в разделе [как: с помощью службы REST в SharePoint, выполните документы, сайты и тегов](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md). 
  
    
    


## <a name="how-to-get-a-tags-guid-based-on-the-tags-name-by-using-the-javascript-object-model"></a>Как получить идентификатор GUID тега на основании имя тега с помощью объектной модели JavaScript
<a name="bk_getTagGuid"> </a>

Start и stop отслеживание тега или чтобы узнать, совместимо ли текущий пользователь после его необходимо использовать идентификатор GUID тега. Приведенный ниже код показано, как получить GUID на основе имени тега.
  
    
    
Прежде чем запустить код необходимо добавить ссылку на **sp.taxonomy.js** и измените имя тега заполнитель с именем существующего тега.
  
    
    



```

function getTagGuid() {
    var tagName = '#tally';
    var clientContext = new SP.ClientContext.get_current();
    var label = SP.Taxonomy.LabelMatchInformation.newObject(clientContext);
    label.set_termLabel(tagName);
    label.set_trimUnavailable(false);
    var taxSession = SP.Taxonomy.TaxonomySession.getTaxonomySession(clientContext);
    var termStore = taxSession.getDefaultKeywordsTermStore();
    var termSet = termStore.get_hashTagsTermSet();
    terms = termSet.getTerms(label);
    clientContext.load(terms);
    clientContext.executeQueryAsync(
        function () {
            var tag = terms.get_item(0);
            if (tag !== null) {
                var tagGuid = tag.get_id().toString();
                if (!SP.ScriptUtility.isNullOrEmptyString(tagGuid)) {
                    alert(tagGuid);
                }
            }
        },
        function (sender, args) {
            alert(args.get_message());
        }
    );
}

```


## <a name="see-also"></a>См. также
<a name="bk_addResources"> </a>


-  [Как подписываться на документы и сайты, используя клиентскую объектную модель .NET в SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  
-  [Как подписываться на документы, сайты и теги, используя службу REST в SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [Following people and content REST API reference for SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [Социальные функции и функции совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Подписка на людей в SharePoint](follow-people-in-sharepoint.md)
    
  
