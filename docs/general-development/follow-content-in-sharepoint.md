---
title: "Подписка на контент в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 30e68cd6-6e55-4cf9-afd6-7139b0a97288
ms.openlocfilehash: 96a334f77bbf9e5b1512290ace4e01b61435548f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="follow-content-in-sharepoint"></a><span data-ttu-id="a8ba7-102">Подписка на контент в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-102">Follow content in SharePoint</span></span>
<span data-ttu-id="a8ba7-103">Узнайте о типичные задачи программирования для следующее содержимое (документы, сайты и теги) в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-103">Learn about common programming tasks for following content (documents, sites, and tags) in SharePoint.</span></span>
## <a name="apis-for-following-content-in-sharepoint"></a><span data-ttu-id="a8ba7-104">API-интерфейсы для следующих контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-104">APIs for following content in SharePoint</span></span>
<span data-ttu-id="a8ba7-105"><a name="bkmk_APIversions"> </a></span><span class="sxs-lookup"><span data-stu-id="a8ba7-105"></span></span>

<span data-ttu-id="a8ba7-p101">Когда пользователи выполнения документы, сайты или теги, обновлений состояния из документов, бесед на сайты и уведомления тега использовать показа в их канала новостей. Функции, связанные с следующее содержимое может отображаться на **канал новостей** и на **следующих** страницах контента.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-p101">When users follow documents, sites, or tags, status updates from documents, conversations on sites, and notifications of tag use show up in their newsfeed. The features related to following content can be seen on the **Newsfeed** and the **Following** content pages.</span></span>
  
    
    
<span data-ttu-id="a8ba7-108">SharePoint предоставляет следующие интерфейсы API, которые можно использовать для программного выполнения контента:</span><span class="sxs-lookup"><span data-stu-id="a8ba7-108">SharePoint provides the following APIs that you can use to programmatically follow content:</span></span>
  
    
    

- <span data-ttu-id="a8ba7-109">Клиентские объектные модели для управляемого кода:</span><span class="sxs-lookup"><span data-stu-id="a8ba7-109">Client object models for managed code</span></span>
    
  - <span data-ttu-id="a8ba7-110">клиентская объектная модель .NET;</span><span class="sxs-lookup"><span data-stu-id="a8ba7-110">.NET client object model</span></span>
    
  
  - <span data-ttu-id="a8ba7-111">клиентская объектная модель Silverlight;</span><span class="sxs-lookup"><span data-stu-id="a8ba7-111">Silverlight client object model</span></span>
    
  
  - <span data-ttu-id="a8ba7-112">мобильная клиентская объектная модель.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-112">Mobile client object model</span></span>
    
  
- <span data-ttu-id="a8ba7-113">Объектная модель JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-113">JavaScript object model</span></span>
    
  
- <span data-ttu-id="a8ba7-114">Служба передачи репрезентативного состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="a8ba7-114">Representational State Transfer (REST) service</span></span>
    
  
- <span data-ttu-id="a8ba7-115">Серверная объектная модель</span><span class="sxs-lookup"><span data-stu-id="a8ba7-115">Server object model</span></span>
    
  
<span data-ttu-id="a8ba7-116">Рекомендуется при разработке для SharePoint при вы можете Используйте клиентские API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-116">As a best practice in SharePoint development, use client APIs when you can.</span></span> <span data-ttu-id="a8ba7-117">API-интерфейсов клиента включают клиентской объектной модели, объектной модели JavaScript и службы REST.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-117">Client APIs include the client object models, a JavaScript object model, and a REST service.</span></span> <span data-ttu-id="a8ba7-118">Дополнительные сведения об интерфейсах API в SharePoint и их использовании см. раздел [Выбор право API в SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="a8ba7-118">For more information about the APIs in SharePoint and when to use them, see  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="a8ba7-119">Каждый API включает в себя объект диспетчера, используемая для выполнения основных задач по следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-119">Each API includes a manager object that you use to perform core tasks for following content.</span></span>
  
    
    

> <span data-ttu-id="a8ba7-120">**Примечание:** Же API используются следить за людьми.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-120">**Note:** The same APIs are used to follow people.</span></span> <span data-ttu-id="a8ba7-121">[Подписка на людей в SharePoint](follow-people-in-sharepoint.md) в разделе Общие сведения о задачах следующие сотрудники.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-121">See  [Follow people in SharePoint](follow-people-in-sharepoint.md) for an overview of Following People tasks.</span></span>
  
    
    

<span data-ttu-id="a8ba7-122">В таблице 1 приведены диспетчер и другие ключевые объекты (или ресурсы REST) в API-интерфейсы и библиотека классов (или точка доступа) где их можно найти.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-122">Table 1 shows the manager and other key objects (or REST resources) in the APIs and the class library (or access point) where you can find them.</span></span>
  
    
    

> <span data-ttu-id="a8ba7-123">**Примечание:** Silverlight и мобильных устройств клиентской объектной модели не включаются в таблице 1 или в таблице 2, так как они обеспечивают основные функциональные возможности, аналогичные клиентской объектной модели .NET и использовать же цифровые подписи.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-123">**Note:** The Silverlight and mobile client object models are not included in Table 1 or Table 2 because they provide the same core functionality as the .NET client object model and use the same signatures.</span></span> <span data-ttu-id="a8ba7-124">Клиентская объектная модель Silverlight определяется в Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll и мобильных устройств клиентской объектной модели определяется в Microsoft.SharePoint.Client.UserProfiles.Phone.dll.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-124">The Silverlight client object model is defined in Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll, and the mobile client object model is defined in Microsoft.SharePoint.Client.UserProfiles.Phone.dll.</span></span> 
  
    
    


<span data-ttu-id="a8ba7-125">**В таблице 1. API-интерфейсов SharePoint используется для следующих содержимого программным путем**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-125">**Table 1. SharePoint APIs used for following content programmatically**</span></span>

|<span data-ttu-id="a8ba7-126">**API**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-126">**API**</span></span>|<span data-ttu-id="a8ba7-127">**Основные объекты**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-127">**Key objects**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a8ba7-128">Клиентская объектная модель .NET</span><span class="sxs-lookup"><span data-stu-id="a8ba7-128">.NET client object model</span></span>  <br/> <span data-ttu-id="a8ba7-129">См.: [как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-129">See:  [How to: Follow documents and sites by using the .NET client object model in SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)</span></span>|<span data-ttu-id="a8ba7-130">Объект диспетчера:            [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-130">Manager object:            [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-131">Основное пространство имен:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-131">Primary namespace:            [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-132">Другие ключевые объекты:            [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) , [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) , [SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) , [SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-132">Other key objects:            [SocialActor](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActor.aspx) , [SocialActorInfo](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorInfo.aspx) , [SocialActorType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorType.aspx) , [SocialActorTypes](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialActorTypes.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-133">Библиотека классов:           Microsoft.SharePoint.Client.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="a8ba7-133">Class library:           Microsoft.SharePoint.Client.UserProfiles.dll</span></span>  |
|<span data-ttu-id="a8ba7-134">Объектная модель JavaScript</span><span class="sxs-lookup"><span data-stu-id="a8ba7-134">JavaScript object model</span></span>|<span data-ttu-id="a8ba7-135">Объект диспетчера:            [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-135">Manager object:            [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-136">Основное пространство имен:            [SP. Социальные](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-136">Primary namespace:            [SP.Social](http://msdn.microsoft.com/library/43d47f01-c085-0e77-bd01-48bcb7d5bb35%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-137">Другие ключевые объекты:            [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx),  [SocialActorInfo](http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx),  [SocialActorType](http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx),  [SocialActorTypes](http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-137">Other key objects:            [SocialActor](http://msdn.microsoft.com/library/4e369fd5-b9b0-9804-957e-b3e39c559cd4%28Office.15%29.aspx),  [SocialActorInfo](http://msdn.microsoft.com/library/d940db32-1561-c868-bb66-0612e2031f17%28Office.15%29.aspx),  [SocialActorType](http://msdn.microsoft.com/library/fbde74da-f292-dc87-0b7e-81bc5b7a880c%28Office.15%29.aspx),  [SocialActorTypes](http://msdn.microsoft.com/library/a460c3e6-ed88-117d-6755-4c5803a154a0%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-138">Библиотека классов:           SP.UserProfiles.js</span><span class="sxs-lookup"><span data-stu-id="a8ba7-138">Class library:           SP.UserProfiles.js</span></span>  |
|<span data-ttu-id="a8ba7-139">Служба REST</span><span class="sxs-lookup"><span data-stu-id="a8ba7-139">REST service</span></span>  <br/> <span data-ttu-id="a8ba7-140">Просмотреть [как: с помощью службы REST в SharePoint, выполните документы, сайты и тегов](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-140">See  [How to: Follow documents, sites, and tags by using the REST service in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)</span></span>|<span data-ttu-id="a8ba7-141">Руководитель ресурсов:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-141">Manager resource:            [social.following](following-people-and-content-rest-api-reference-for-sharepoint.md)</span></span> <br/> <span data-ttu-id="a8ba7-142">Основное пространство имен (OData):           **sp.social.SocialRestFollowingManager**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-142">Primary namespace (OData):           **sp.social.SocialRestFollowingManager**</span></span> <br/> <span data-ttu-id="a8ba7-143">Другие ключевые ресурсы:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-143">Other key resources:           **SocialActor**, **SocialActorInfo**, **SocialActorType**, **SocialActorTypes**</span></span> <br/> <span data-ttu-id="a8ba7-144">Точка доступа:            `<siteUri>/_api/social.following`</span><span class="sxs-lookup"><span data-stu-id="a8ba7-144">Access point:            `<siteUri>/_api/social.following`</span></span> |
|<span data-ttu-id="a8ba7-145">Серверная объектная модель.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-145">Server object model</span></span>|<span data-ttu-id="a8ba7-146">Объект диспетчера:            [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-146">Manager object:            [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-147">Основное пространство имен:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-147">Primary namespace:            [Microsoft.Office.Server.Social](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-148">Другие ключевые объекты:            [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) , [SPSocialActorInfo](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx) , [SPSocialActorType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx) , [SPSocialActorTypes](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-148">Other key objects:            [SPSocialActor](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActor.aspx) , [SPSocialActorInfo](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorInfo.aspx) , [SPSocialActorType](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorType.aspx) , [SPSocialActorTypes](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialActorTypes.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-149">Библиотека классов:           Microsoft.Office.Server.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="a8ba7-149">Class library:           Microsoft.Office.Server.UserProfiles.dll</span></span>  |
   

## <a name="common-programming-tasks-for-following-content-in-sharepoint"></a><span data-ttu-id="a8ba7-150">Типичные задачи программирования для следующих контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-150">Common programming tasks for following content in SharePoint</span></span>
<span data-ttu-id="a8ba7-151"><a name="bkmk_CommonTasks"> </a></span><span class="sxs-lookup"><span data-stu-id="a8ba7-151"></span></span>

<span data-ttu-id="a8ba7-p105">В таблице 2 перечислены типичные задачи программирования для следующее содержимое и элементы, которые можно использовать для их выполнения. Члены: от клиентской объектной модели .NET (CSOM), JavaScript объектной модели (JSOM), служба REST и серверной объектной модели (SSOM).</span><span class="sxs-lookup"><span data-stu-id="a8ba7-p105">Table 2 shows common programming tasks for following content and the members that you use to perform them. Members are from the .NET client object model (CSOM), JavaScript object model (JSOM), REST service, and server object model (SSOM).</span></span>
  
    
    

> <span data-ttu-id="a8ba7-154">**Примечание:** Же API используются следить за людьми.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-154">**Note:** The same APIs are used to follow people.</span></span> <span data-ttu-id="a8ba7-155">[Подписка на людей в SharePoint](follow-people-in-sharepoint.md) в разделе Общие сведения о задачах следующие сотрудники.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-155">See  [Follow people in SharePoint](follow-people-in-sharepoint.md) for an overview of Following People tasks.</span></span>
  
    
    


<span data-ttu-id="a8ba7-156">**В таблице 2. API для распространенных задач для следующих контента в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-156">**Table 2. API for common tasks for following content in SharePoint**</span></span>


|<span data-ttu-id="a8ba7-157">**Задача**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-157">**Task**</span></span>|<span data-ttu-id="a8ba7-158">**Участники**</span><span class="sxs-lookup"><span data-stu-id="a8ba7-158">**Members**</span></span>|
|:-----|:-----|
|<span data-ttu-id="a8ba7-159">Создание экземпляра объекта диспетчера в контексте текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="a8ba7-159">Create an instance of a manager object in the context of the current user</span></span>|<span data-ttu-id="a8ba7-160">CSOM:  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-160">CSOM:  [SocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-161">JSOM:  [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-161">JSOM:  [SocialFollowingManager](http://msdn.microsoft.com/library/9ee1c0c0-b864-f0c3-f0cb-4dd4f1870dfa%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-162">REST:  `<siteUri>/_api/social.following`</span><span class="sxs-lookup"><span data-stu-id="a8ba7-162">REST:  `<siteUri>/_api/social.following`</span></span> <br/> <span data-ttu-id="a8ba7-163">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-163">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx)</span></span>|
|<span data-ttu-id="a8ba7-164">Создайте экземпляр объекта диспетчера в контексте указанного пользователя</span><span class="sxs-lookup"><span data-stu-id="a8ba7-164">Create an instance of a manager object in the context of a specified user</span></span>|<span data-ttu-id="a8ba7-165">CSOM: не реализовано</span><span class="sxs-lookup"><span data-stu-id="a8ba7-165">CSOM: not implemented</span></span>  <br/> <span data-ttu-id="a8ba7-166">JSOM: не реализовано</span><span class="sxs-lookup"><span data-stu-id="a8ba7-166">JSOM: not implemented</span></span>  <br/> <span data-ttu-id="a8ba7-167">REST: не реализовано</span><span class="sxs-lookup"><span data-stu-id="a8ba7-167">REST: not implemented</span></span>  <br/> <span data-ttu-id="a8ba7-168">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) (перегрузка)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-168">SSOM:  [SPSocialFollowingManager](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.aspx) (overloaded)</span></span>|
|<span data-ttu-id="a8ba7-169">У текущего пользователя создайте (остановить следующие) элемента</span><span class="sxs-lookup"><span data-stu-id="a8ba7-169">Have the current user start following (stop following) an item</span></span>|<span data-ttu-id="a8ba7-170">CSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) )</span><span class="sxs-lookup"><span data-stu-id="a8ba7-170">CSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.StopFollowing.aspx) )</span></span> <br/> <span data-ttu-id="a8ba7-171">JSOM:  [выполните](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) ( [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx))</span><span class="sxs-lookup"><span data-stu-id="a8ba7-171">JSOM:  [follow](http://msdn.microsoft.com/library/40d14320-27ba-2941-b0e2-be3b5a407c89%28Office.15%29.aspx) ( [stopFollowing](http://msdn.microsoft.com/library/65b0e9be-dc5e-09fb-c57f-7a933de09a4c%28Office.15%29.aspx))</span></span>  <br/> <span data-ttu-id="a8ba7-172">REST: **POST** [`<siteUri>/_api/social.following/Follow`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Follow) ( [`<siteUri>/_api/social.following/StopFollowing`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_StopFollowing)) и передайте параметр _actor_ в теле запроса</span><span class="sxs-lookup"><span data-stu-id="a8ba7-172">REST: **POST** [`<siteUri>/_api/social.following/Follow`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Follow) ( [`<siteUri>/_api/social.following/StopFollowing`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_StopFollowing))           and pass the _actor_ parameter in the request body</span></span> <br/> <span data-ttu-id="a8ba7-173">SSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx) )</span><span class="sxs-lookup"><span data-stu-id="a8ba7-173">SSOM:  [Follow](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.Follow.aspx) ( [StopFollowing](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.StopFollowing.aspx) )</span></span>|
|<span data-ttu-id="a8ba7-174">Узнать, является ли текущий пользователь является после определенного элемента</span><span class="sxs-lookup"><span data-stu-id="a8ba7-174">Find out whether the current user is following a particular item</span></span>|<span data-ttu-id="a8ba7-175">CSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-175">CSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.IsFollowed.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-176">JSOM:  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-176">JSOM:  [isFollowed](http://msdn.microsoft.com/library/2c1f62e6-fb75-ad4d-c081-36408b418c21%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-177">REST: **POST** [`<siteUri>/_api/social.following/IsFollowed`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_IsFollowed) и передайте параметр _actor_ в теле запроса</span><span class="sxs-lookup"><span data-stu-id="a8ba7-177">REST: **POST** [`<siteUri>/_api/social.following/IsFollowed`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_IsFollowed) and pass the _actor_ parameter in the request body</span></span> <br/> <span data-ttu-id="a8ba7-178">SSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-178">SSOM:  [IsFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.IsFollowed.aspx)</span></span>|
|<span data-ttu-id="a8ba7-179">Получение документы, сайты и/или теги, выполнив текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="a8ba7-179">Get the documents, sites, and/or tags that the current user is following</span></span>|<span data-ttu-id="a8ba7-180">CSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-180">CSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowed.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-181">JSOM:  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-181">JSOM:  [getFollowed](http://msdn.microsoft.com/library/432a7cec-6add-fdb1-a79f-a93414ee8cd3%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-182">REST: **Получение** [`<siteUri>/_api/social.following/my/Followed(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed) (документы = **2**, сайты = **4**, теги = публикацию повторно **8**)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-182">REST: **GET** [`<siteUri>/_api/social.following/my/Followed(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_Followed) (documents = **2**, sites = **4**, tags = **8**.md)</span></span>  <br/> <span data-ttu-id="a8ba7-183">SSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-183">SSOM:  [GetFollowed](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowed.aspx)</span></span>|
|<span data-ttu-id="a8ba7-184">Получение числа документы, сайты и/или теги, на которые подписан пользователь</span><span class="sxs-lookup"><span data-stu-id="a8ba7-184">Get the count of documents, sites, and/or tags that the user is following</span></span>|<span data-ttu-id="a8ba7-185">CSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-185">CSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.GetFollowedCount.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-186">JSOM:  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-186">JSOM:  [getFollowedCount](http://msdn.microsoft.com/library/97b53b4f-481a-cf41-1854-8f3ff860b2bb%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-187">REST: **Получение** [`<siteUri>/_api/social.following/my/FollowedCount(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount) (документы = **2**, сайты = **4**, теги = публикацию повторно **8**)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-187">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedCount(types=2)`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_FollowedCount) (documents = **2**, sites = **4**, tags = **8**.md)</span></span>  <br/> <span data-ttu-id="a8ba7-188">SSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-188">SSOM:  [GetFollowedCount](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.GetFollowedCount.aspx)</span></span>|
|<span data-ttu-id="a8ba7-189">Получение URI-адрес сайта, в котором приведены число документов текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="a8ba7-189">Get the URI of the site that lists the current user's followed documents</span></span>|<span data-ttu-id="a8ba7-190">CSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedDocumentsUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-190">CSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedDocumentsUri.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-191">JSOM:  [followedDocumentsUri](http://msdn.microsoft.com/library/3a70b9c7-abd7-94ff-d730-70298673d6ec%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-191">JSOM:  [followedDocumentsUri](http://msdn.microsoft.com/library/3a70b9c7-abd7-94ff-d730-70298673d6ec%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-192">**Получение** REST:[`<siteUri>/_api/social.following/my/FollowedDocumentsUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedDocumentsUri)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-192">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedDocumentsUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedDocumentsUri)</span></span> <br/> <span data-ttu-id="a8ba7-193">SSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedDocumentsUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-193">SSOM:  [FollowedDocumentsUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedDocumentsUri.aspx)</span></span>|
|<span data-ttu-id="a8ba7-194">Получение URI-адрес сайта, в котором приведены число сайтов текущего пользователя</span><span class="sxs-lookup"><span data-stu-id="a8ba7-194">Get the URI of the site that lists the current user's followed sites</span></span>|<span data-ttu-id="a8ba7-195">CSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedSitesUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-195">CSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFollowingManager.FollowedSitesUri.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-196">JSOM:  [followedSitesUri](http://msdn.microsoft.com/library/829404bc-1b3a-7545-5e95-0922df330084%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-196">JSOM:  [followedSitesUri](http://msdn.microsoft.com/library/829404bc-1b3a-7545-5e95-0922df330084%28Office.15%29.aspx)</span></span> <br/> <span data-ttu-id="a8ba7-197">**Получение** REST:[`<siteUri>/_api/social.following/my/FollowedSitesUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedSitesUri)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-197">REST: **GET** [`<siteUri>/_api/social.following/my/FollowedSitesUri`](following-people-and-content-rest-api-reference-for-sharepoint.md#bk_MyFollowedSitesUri)</span></span> <br/> <span data-ttu-id="a8ba7-198">SSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedSitesUri.aspx)</span><span class="sxs-lookup"><span data-stu-id="a8ba7-198">SSOM:  [FollowedSitesUri](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialFollowingManager.FollowedSitesUri.aspx)</span></span>|
   

> <span data-ttu-id="a8ba7-199">**Примечание:** Примеры, показывающие, как использовать службы REST для подписка на контент, в разделе [как: с помощью службы REST в SharePoint, выполните документы, сайты и тегов](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span><span class="sxs-lookup"><span data-stu-id="a8ba7-199">**Note:** For examples that show how to use the REST service to follow content, see  [How to: Follow documents, sites, and tags by using the REST service in SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md).</span></span> 
  
    
    


## <a name="how-to-get-a-tags-guid-based-on-the-tags-name-by-using-the-javascript-object-model"></a><span data-ttu-id="a8ba7-200">Как получить идентификатор GUID тега на основании имя тега с помощью объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="a8ba7-200">How to get a tag's GUID based on the tag's name by using the JavaScript object model</span></span>
<span data-ttu-id="a8ba7-201"><a name="bk_getTagGuid"> </a></span><span class="sxs-lookup"><span data-stu-id="a8ba7-201"></span></span>

<span data-ttu-id="a8ba7-p107">Start и stop отслеживание тега или чтобы узнать, совместимо ли текущий пользователь после его необходимо использовать идентификатор GUID тега. Приведенный ниже код показано, как получить GUID на основе имени тега.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-p107">To start and stop following a tag or to find out whether the current user is following it, you need to use the tag's GUID. The following code shows how to get the GUID based on the tag name.</span></span>
  
    
    
<span data-ttu-id="a8ba7-204">Прежде чем запустить код необходимо добавить ссылку на **sp.taxonomy.js** и измените имя тега заполнитель с именем существующего тега.</span><span class="sxs-lookup"><span data-stu-id="a8ba7-204">Before you run the code, you need to add a reference to **sp.taxonomy.js** and change the placeholder tag name with the name of an existing tag.</span></span>
  
    
    



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


## <a name="additional-resources"></a><span data-ttu-id="a8ba7-205">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8ba7-205">Additional resources</span></span>
<span data-ttu-id="a8ba7-206"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a8ba7-206"></span></span>


-  [<span data-ttu-id="a8ba7-207">Как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-207">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)
    
  
-  [<span data-ttu-id="a8ba7-208">Как: выполните документы, сайты и теги с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-208">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)
    
  
-  [<span data-ttu-id="a8ba7-209">Following people and content REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-209">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a8ba7-210">Социальные функции и функции совместной работы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-210">Social and collaboration features in SharePoint</span></span>](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a8ba7-211">Начало разработки с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-211">Get started developing with social features in SharePoint</span></span>](get-started-developing-with-social-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a8ba7-212">Подписка на людей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8ba7-212">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  