---
title: "Работа с профилями пользователей в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7437a7a8-85cb-4233-84af-1eec30dd54b2
ms.openlocfilehash: 4561b7e5f0cab4370c01421f19edc50bd803bd5d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="work-with-user-profiles-in-sharepoint"></a>Работа с профилями пользователей в SharePoint
Узнайте о распространенных задачах программирования для работы с профилями пользователей в SharePoint.
## <a name="apis-for-working-with-user-profiles-in-sharepoint"></a>Интерфейсы API для работы с профилями пользователей в SharePoint
<a name="bkmk_APIversions"> </a>

Профили пользователей и их свойства предоставляют сведения о пользователях SharePoint. SharePoint предоставляет следующие API для программной работы с профилями пользователей:
  
    
    

- Клиентские объектные модели для управляемого кода
    
  - Клиентская объектная модель .NET
    
  
  - Клиентская объектная модель Silverlight
    
  
  - Клиентская объектная модель для мобильных устройств.
    
  
- Объектная модель JavaScript
    
  
- Служба передачи репрезентативного состояния (REST).
    
  
- Объектная модель сервера
    
  
Согласно передовой практике в разработке SharePoint, используйте клиентские интерфейсы API, когда это возможно. Клиентские интерфейсы API включают клиентскую объектную модель .NET, объектную модель JavaScript и службу REST. Более подробную информацию об интерфейсах API в SharePoint и их использовании можно узнать в статье  [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    

> **Примечание.** Не все функции, включенные в сборку **Microsoft.Office.Server.UserProfiles**, доступны в клиентских API. Например, для создания и изменения профилей пользователей необходимо использовать серверную объектную модель, так как они доступны только для чтения в клиентских API (за исключением аватара пользователя). Кроме того, со стороны клиента невозможно получить доступ к некоторым пространствам имен, например [Microsoft.Office.Server.Audience](https://msdn.microsoft.com/library/Microsoft.Office.Server.Audience.aspx), [Microsoft.Office.Server.ReputationModel](https://msdn.microsoft.com/library/Microsoft.Office.Server.ReputationModel.aspx) или [Microsoft.Office.Server.SocialData](https://msdn.microsoft.com/library/Microsoft.Office.Server.SocialData.aspx). Сведения о том, какие функции поддерживаются клиентскими API, см. в статьях [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) и [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx).
  
    
    

Каждый интерфейс API включает диспетчер объектов, который можно использовать для выполнения основных задач, связанных с профилем. В таблице 1 приведен диспетчер и другие ключевые объекты (или источники REST) в интерфейсах API, а также библиотека классов (или точка доступа), где их можно найти.
  
    
    

> **Примечание.** Клиентские объектные модели для Silverlight и мобильных устройств не представлены в таблицах 1 и 2, так как они предоставляют те же основные функции, что и клиентская объектная модель .NET, и используют те же подписи. Клиентская объектная модель Silverlight определена в библиотеке Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll, а клиентская объектная модель для мобильных устройств — в библиотеке Microsoft.SharePoint.Client.UserProfiles.Phone.dll. 
  
    
    


**Таблица 1. API SharePoint, используемые для программной работы с профилями пользователей**

|**API**|**Ключевой объект**|
|:-----|:-----|
|Клиентская объектная модель .NET  <br/> См. статью  [Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)|Диспетчер объектов:            [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) <br/> Основное пространство имен:            [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) <br/> Другие ключевые объекты:            [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) , [ProfileLoader](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.aspx) , [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) <br/> Библиотека классов:           Microsoft.SharePoint.Client.UserProfiles.dll |
|Объектная модель JavaScript  <br/> См. статью  [Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)|Диспетчер объектов:            [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) <br/> Основное пространство имен:            [SP.UserProfiles](http://msdn.microsoft.com/library/8c1fcceb-cd9a-b25c-32f4-1cfb0578278c%28Office.15%29.aspx) <br/> Другие ключевые объекты:            [PersonProperties](http://msdn.microsoft.com/library/0274d97f-b697-f436-2aaf-f5bcf9b70df8%28Office.15%29.aspx),  [ProfileLoader](http://msdn.microsoft.com/library/c8dd9919-66a9-fffc-1100-14472d2ec2cb%28Office.15%29.aspx),  [UserProfile](http://msdn.microsoft.com/library/f8c4a219-fbaa-2e50-1bd5-fdc80051b33d%28Office.15%29.aspx) <br/> Библиотека классов:           SP.UserProfiles.js |
|Служба REST  <br/> См. статью  [Справочник по API REST для профилей пользователей](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)|Диспетчер объектов:            [PeopleManager](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManager) <br/> URI конечной точки:            `http://<siteUri>/_api/SP.UserProfiles.PeopleManager` <br/> Основное пространство имен:           **SP.UserProfiles** <br/> Другие ключевые ресурсы:            [PersonProperties](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PersonProperties),  [ProfileLoader](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_ProfileLoader),  [UserProfile](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_UserProfile)|
|Объектная модель сервера  <br/> См. статью  [Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|Диспетчер объектов:            [UserProfileManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.aspx) , [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx) <br/> Основное пространство имен:            [Microsoft.Office.Server.UserProfiles](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.aspx) <br/> Другие ключевые объекты:            [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) , [CorePropertyManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.CorePropertyManager.aspx) , [ProfilePropertyManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfilePropertyManager.aspx) , [ProfileSubtypeManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypeManager.aspx) , [ProfileSubtypePropertyManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileSubtypePropertyManager.aspx) , [ProfileTypePropertyManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.ProfileTypePropertyManager.aspx) <br/> Библиотека классов:           Microsoft.Office.Server.UserProfiles.dll |
   

## <a name="common-programming-tasks-for-working-with-user-profiles-in-sharepoint"></a>Общие задачи программирования для работы с профилями пользователей в SharePoint
<a name="bkmk_CommonTasks"> </a>

В таблице 2 приведены распространенные задачи программирования для работы с профилями пользователей и участники, используемые для их выполнения. Участники находятся в клиентской объектной модели .NET (CSOM), объектной модели JavaScript (JSOM), службе REST и серверной объектной модели (SSOM).
  
    
    

**Таблица 2. Интерфейс API для общих задач программирования для работы с профилями пользователей**


|**Задача**|**Участники**|
|:-----|:-----|
|Создание экземпляра объекта диспетчера в контексте текущего пользователя |CSOM:  [PeopleManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.aspx) <br/> JSOM: [PeopleManager](http://msdn.microsoft.com/library/985fd2df-0e31-6ece-b846-ba2ccb156d00%28Office.15%29.aspx) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManager)<br/> SSOM: [UserProfileManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.aspx) (перегруженный) или [PeopleManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.aspx)|
|Изменение изображения в профиле текущего пользователя |CSOM:  [SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.SetMyProfilePicture.aspx) <br/> JSOM: [setMyProfilePicture](http://msdn.microsoft.com/library/a4f8d745-f211-e750-4fd0-047091804683%28Office.15%29.aspx) <br/> REST: **POST** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/SetMyProfilePicture`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerSetMyProfilePicture) и передача параметра _picture_ в тексте запроса <br/> SSOM: [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) [PropertyConstants.PictureUrl].Value или [SetMyProfilePicture](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.SetMyProfilePicture.aspx)|
|Получение свойств текущего пользователя |CSOM:  [GetMyProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetMyProperties.aspx) <br/> JSOM: [getMyProperties](http://msdn.microsoft.com/library/be001abc-a431-8d48-8e6f-161251aa19ac%28Office.15%29.aspx) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/GetMyProperties`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerGetMyProperties) (или получение некоторых основных свойств пользователя из конечной точки `/_api/social.feed/my` или `/_api/social.following/my`)  <br/> SSOM: [GetUserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.GetUserProfile.aspx)|
|Получение свойств конкретного пользователя |CSOM:  [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetPropertiesFor.aspx) <br/> JSOM: [getPropertiesFor](http://msdn.microsoft.com/library/097464db-2630-4c7a-fd0c-0f333680b5a4%28Office.15%29.aspx) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)?@v='domain\\user'`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerGetPropertiesFor) <br/> SSOM: [GetUserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.GetUserProfile.aspx) (перегруженный) или [GetPropertiesFor](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PeopleManager.GetPropertiesFor.aspx)|
|Получение свойств профиля пользователя для конкретного пользователя |CSOM:  [GetUserProfilePropertiesFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertiesFor.aspx) <br/> JSOM: [getUserProfilePropertiesFor](http://msdn.microsoft.com/library/8674e96f-d320-4a50-1580-9a4568842ee5%28Office.15%29.aspx) <br/> REST: не реализовано. Вызовите метод [GetPropertiesFor](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerGetPropertiesFor), а затем получите свойства профиля пользователя из свойства **UserProfileProperties** возвращаемого объекта **PersonProperties**. <br/> SSOM: [GetEnumerator](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.GetEnumerator.aspx)|
|Получение конкретного свойства профиля пользователя для пользователя |CSOM:  [GetUserProfilePropertyFor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PeopleManager.GetUserProfilePropertyFor.aspx) <br/> JSOM: [getUserProfilePropertyFor](http://msdn.microsoft.com/library/da048bfa-54c6-8216-e8ef-09bd84f68d8d%28Office.15%29.aspx) <br/> REST: **GET** [`http://<siteUri>/_api/SP.UserProfiles.PeopleManager/GetUserProfilePropertyFor(accountName=@v,propertyName='PreferredName')?@v='domain\\user'`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_PeopleManagerGetUserProfilePropertyFor) <br/> SSOM: [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) (перегруженный) с указанием имени свойства в индексаторе|
|Получение профиля пользователя |CSOM:  [GetUserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.ProfileLoader.GetUserProfile.aspx) (возвращает [клиентский профиль пользователя](work-with-user-profiles-in-sharepoint.md#bkmk_NewUserObjects) только для текущего пользователя) <br/> JSOM: [getUserProfile](http://msdn.microsoft.com/library/8e30e811-5da1-b6d0-a8b5-befea9b22496%28Office.15%29.aspx) (возвращает [клиентский профиль пользователя](work-with-user-profiles-in-sharepoint.md#bkmk_NewUserObjects) только для текущего пользователя) <br/> REST: **POST** [`http://<siteUri>/_api/SP.UserProfiles.ProfileLoader.GetProfileLoader/GetUserProfile`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx.md#bk_ProfileLoaderGetProfileLoader) (возвращает [клиентский профиль пользователя](work-with-user-profiles-in-sharepoint.md#bkmk_NewUserObjects) только для текущего пользователя) <br/> SSOM: [GetUserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.GetUserProfile.aspx) (перегруженный)|
|Узнать, существует ли учетная запись пользователя |CSOM: не реализовано  <br/> JSOM: не реализовано  <br/> REST: не реализовано  <br/> SSOM:  [UserExists](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.UserExists.aspx)|
|Создание или изменение профилей пользователей, а также свойств и атрибутов профиля пользователя  <br/> (Клиентские интерфейсы API могут изменять изображение профиля. См. задачу "Изменение изображения в профиле пользователя" в этой таблице.) |CSOM: не реализовано  <br/> JSOM: не реализовано  <br/> REST: не реализовано  <br/> SSOM: несколько вариантов. Ознакомьтесь со статьей [Инструкции. Работа с профилями пользователей и организации с использованием серверной объектной модели в SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|
|Удаление профиля пользователя |CSOM: не реализовано  <br/> JSOM: не реализовано  <br/> REST: не реализовано  <br/> SSOM:  [RemoveProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.RemoveProfile.aspx) или [RemoveUserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfileManager.RemoveUserProfile.aspx) (перегружен)|
|Подготовка личного сайта пользователя |CSOM:  [CreatePersonalSiteEnque](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.CreatePersonalSiteEnque.aspx) (перегружен) <br/> JSOM: [createPersonalSiteEnque](http://msdn.microsoft.com/library/f4bcb82d-4048-0b29-9bc6-ce70ead49988%28Office.15%29.aspx) (перегруженный) <br/> REST: **POST** [`http://<siteUri>/_api/SP.UserProfiles.ProfileLoader.GetProfileLoader/GetUserProfile/CreatePersonalSiteEnqueue`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx#bk_UserProfileCreatePersonalSiteEnque) <br/> SSOM: [CreatePersonalSite()](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.CreatePersonalSite.aspx) (перегруженный)|
|Подготовка одного или нескольких личных сайтов пользователей  <br/> Доступно только для администраторов узлов Личный сайт на SharePoint Online |CSOM:  [CreatePersonalSiteEnqueueBulk](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bk_CreatePersonalSiteEnqueueBulk) <br/> JSOM: **createPersonalSiteEnqueueBulk** <br/> REST: **POST** [`https://<domain>-admin.sharepoint.com/_api/SP.UserProfiles.ProfileLoader.GetProfileLoader/CreatePersonalSiteEnqueueBulk`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx.md#bk_ProfileLoaderCreatePersonalSiteEnqueueBulk) с передачей массива строк электронных адресов для параметра _emailIDs_ (до 200 символов) в тексте запроса (например, `{'emailIDs':['usera@contoso.onmicrosoft.com','userb@contoso.onmicrosoft.com']}`).  <br/> SSOM: **CreatePersonalSiteEnqueueBulk**|
   

## <a name="new-objects-for-users-and-user-properties-in-sharepoint"></a>Новые объекты для пользователей и свойства пользователей в SharePoint
<a name="bkmk_NewUserObjects"> </a>

SharePoint содержит следующие новые объекты, которые представляют пользователей и их свойства:
  
    
    

- Объекты [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) и [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) представляют пользователей (а также документы, сайты и задачи) для действий с веб-каналами и подписками.
    
  
- Новый клиентский объект  [UserProfile](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.UserProfile.aspx) , предоставляющий методы для создания личных веб-сайтов для текущего пользователя. Однако данный объект содержит не все свойства, имеющиеся в объекте [UserProfile](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.UserProfile.aspx) .
    
  
- Объект  [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) содержит общие свойства пользователей, и его свойство [UserProfileProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.UserProfileProperties.aspx) содержит свойства профилей пользователей. [PersonProperties](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.PersonProperties.aspx) является основным интерфейсом API, предназначенным для доступа к свойствам пользователя из кода на стороне клиента.
    
  

> **Примечание.** В серверной объектной модели им соответствуют объекты [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) и [PersonProperties](https://msdn.microsoft.com/library/Microsoft.Office.Server.UserProfiles.PersonProperties.aspx).
  
    
    


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_AdditionalResources"> </a>


-  [Социальные функции и функции совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Начало разработки с использованием социальных функций в SharePoint](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)
    
  
-  [Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)
    
  
-  [Справочник по API REST для профилей пользователей](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)
    
  
-  [Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)
    
  
-  [Подписка на людей в SharePoint](follow-people-in-sharepoint.md)
    
  
