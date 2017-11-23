---
title: "Приступая к разработке с использованием социальных функций в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8852ce36-8309-45a7-a141-2e10ac17a123
ms.openlocfilehash: 9566ab4fde6513c7a22e537bac66a6880ded981a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-developing-with-social-features-in-sharepoint"></a><span data-ttu-id="c47bf-102">Приступая к разработке с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-102">Get started developing with social features in SharePoint</span></span>
<span data-ttu-id="c47bf-103">Начало работы по программированию с социальными веб-каналами SharePoint и микроблога публикации, следуя людей и содержимое (документы, сайты и теги) и работа с профилями пользователей.</span><span class="sxs-lookup"><span data-stu-id="c47bf-103">Get started programming with SharePoint social feeds and microblog posts, following people and content (documents, sites, and tags), and working with user profiles.</span></span>

    
 [<span data-ttu-id="c47bf-104">как управление социальными компонентами приложений и решений в?</span><span class="sxs-lookup"><span data-stu-id="c47bf-104">How can I use social features in apps and solutions?</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bk_HowToUseSocialFeatures)
  
    
    
 [<span data-ttu-id="c47bf-105">Параметр среды разработки</span><span class="sxs-lookup"><span data-stu-id="c47bf-105">Setting up the development environment</span></span>](get-started-developing-with-social-features-in-sharepoint.md#DevEnvironment)
  
    
    
 [<span data-ttu-id="c47bf-106">сценарии разработки для социальных компонентов</span><span class="sxs-lookup"><span data-stu-id="c47bf-106">Development scenarios for social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#DevScenarios)
  
    
    
 [<span data-ttu-id="c47bf-107">руководства по программированию с использованием социальных функций</span><span class="sxs-lookup"><span data-stu-id="c47bf-107">How-tos for programming with social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bk_GetStarted)
  
    
    
 [<span data-ttu-id="c47bf-108">API-интерфейсы для программирования с использованием социальных функций</span><span class="sxs-lookup"><span data-stu-id="c47bf-108">APIs for programming with social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#SocialApis)
  
    
    
 [<span data-ttu-id="c47bf-109">запроса разрешений для доступа к социальные функции</span><span class="sxs-lookup"><span data-stu-id="c47bf-109">App permission requests for accessing social features</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bkmk_AppPerms)
  
    
    
 [<span data-ttu-id="c47bf-110">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c47bf-110">Additional resources</span></span>](get-started-developing-with-social-features-in-sharepoint.md#bk_AddResources)
  
    
    


## <a name="how-can-i-use-social-features-in-sharepoint-apps-and-solutions"></a><span data-ttu-id="c47bf-111">Использование социальных функций в SharePoint приложений и решений</span><span class="sxs-lookup"><span data-stu-id="c47bf-111">How can I use social features in SharePoint apps and solutions?</span></span>
<span data-ttu-id="c47bf-112"><a name="bk_HowToUseSocialFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-112"></span></span>

<span data-ttu-id="c47bf-113">Социальные функции в приложений и решений SharePoint может помочь подключиться, обмениваться данными и совместно работать друг с другом и поиска, отслеживания и совместного использования важное содержимое и сведения о.</span><span class="sxs-lookup"><span data-stu-id="c47bf-113">Social features in SharePoint apps and solutions can help people to connect, communicate, and collaborate with each other and find, track, and share important content and information.</span></span> <span data-ttu-id="c47bf-114">Вы можете добавить новых социальных функций или расширяющих его возможности, которые уже доступны в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c47bf-114">You can add new social features or extend the features that are already available in SharePoint.</span></span> <span data-ttu-id="c47bf-115">Например можно создать приложение, которое позволяет находить и подписка на людей, которые имеют общие моменты, создание настраиваемой визуализации веб-канала данных или публикации пользовательских действий в веб-канал.</span><span class="sxs-lookup"><span data-stu-id="c47bf-115">For example, you can create an app that lets you find and follow people who have a common interest, create a custom visualization of feed data, or publish custom activities to the feed.</span></span>
  
    
    
<span data-ttu-id="c47bf-p102">Возможности, описанные в этой статье выравнивание для пользователей, веб-каналов и дополнительные функциональные возможности, найдите на личных сайтов и веб-сайтов групп. Модель качества и репутации форум на сайты сообщества не предоставляют доступ к определенным интерфейсам API, поэтому использовать сайт SharePoint и список API-интерфейсы непосредственно к расширить. Для получения дополнительных сведений см  [Новый веб-узел сообщества](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab).</span><span class="sxs-lookup"><span data-stu-id="c47bf-p102">The features described in this article align to the people, feeds, and following functionality that you find on personal sites and team sites. The forum experience and reputation model on Community Sites don't expose a specific API, so you use SharePoint site and list APIs directly to extend that functionality. For more information, see  [New Community Site feature](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab).</span></span>
  
    
    
<span data-ttu-id="c47bf-119">Перед началом разработки, вы должны знать, где будет выполняться код, какая среда SharePoint, его можно было запускать на и какие функциональные возможности будет предоставлять.</span><span class="sxs-lookup"><span data-stu-id="c47bf-119">Before you start developing, you should know where your code will run, what SharePoint environment it will run on, and what functionality it will provide.</span></span> <span data-ttu-id="c47bf-120">Эти факторы помогут выбрать тип приложения для создания и какие API-интерфейса или API-интерфейсы для использования.</span><span class="sxs-lookup"><span data-stu-id="c47bf-120">These factors help you choose the kind of app to create and which API or APIs to use.</span></span> <span data-ttu-id="c47bf-121">Сведения содержатся в разделе [Choose право API в SharePoint](choose-the-right-api-set-in-sharepoint.md) и [надстройки SharePoint по сравнению с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md) , которая поможет вам решить.</span><span class="sxs-lookup"><span data-stu-id="c47bf-121">See  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md) and [SharePoint Add-ins compared with SharePoint solutions](sharepoint-add-ins-compared-with-sharepoint-solutions.md) for information that can help you decide.</span></span>
  
    
    

### <a name="setting-up-your-development-environment"></a><span data-ttu-id="c47bf-122">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="c47bf-122">Setting up your development environment</span></span>
<span data-ttu-id="c47bf-123"><a name="DevEnvironment"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-123"></span></span>

<span data-ttu-id="c47bf-124">Для начала разработки с использованием социальных функций, то необходимо:</span><span class="sxs-lookup"><span data-stu-id="c47bf-124">To get started developing with social features, you'll need:</span></span>
  
    
    

- <span data-ttu-id="c47bf-125">SharePoint или SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="c47bf-125">SharePoint or SharePoint Online</span></span>
    
- <span data-ttu-id="c47bf-126">Visual Studio 2012 или Visual Studio 2013 со средствами для разработчиков Office для Visual Studio 2013 — или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="c47bf-126">Visual Studio 2012 or Visual Studio 2013, with Office Developer Tools for Visual Studio 2013 - or newer</span></span>
  

  
<span data-ttu-id="c47bf-127">Дополнительные инструкции в разделе [Настройка среды Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md) и [Настройка компонентов социальных сетей в SharePoint](http://technet.microsoft.com/ru-ru/library/fp161267%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c47bf-127">For more guidance, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md) and [Configure social computing features in SharePoint](http://technet.microsoft.com/ru-ru/library/fp161267%28v=office.15%29.aspx).</span></span>
  
    
    

### <a name="development-scenarios-for-social-features-in-sharepoint"></a><span data-ttu-id="c47bf-128">Сценарии разработки для социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-128">Development scenarios for social features in SharePoint</span></span>
<span data-ttu-id="c47bf-129"><a name="DevScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-129"></span></span>

<span data-ttu-id="c47bf-p104">Сценарии разработки высокого уровня для социальных компонентов относятся работа с социальными веб-каналами, подписки на людей и содержимое (документы, сайты и теги) и работа со свойствами пользователей. В таблице 1 приведены ссылки на статьи с описанием основных интерфейсы API, которая используется для доступа к функции для каждого сценария и типичные задачи программирования.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p104">High-level development scenarios for social features include working with social feeds, following people and content (documents, sites, and tags), and working with user properties. Table 1 contains links to articles that describe the primary APIs that you use to access functionality for each scenario and common programming tasks.</span></span>
  
    
    
<span data-ttu-id="c47bf-132">В следующих статьях описываются основные интерфейсы API и задачи программирования для разработки конкретного сценария:</span><span class="sxs-lookup"><span data-stu-id="c47bf-132">The following articles describe the primary APIs and programming tasks for the particular development scenario:</span></span>
  
    
    

-  [<span data-ttu-id="c47bf-133">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-133">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c47bf-134">Подписка на людей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-134">Follow people in SharePoint</span></span>](follow-people-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c47bf-135">Подписка на контент в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-135">Follow content in SharePoint</span></span>](follow-content-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c47bf-136">Работа с профилями пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-136">Work with user profiles in SharePoint</span></span>](work-with-user-profiles-in-sharepoint.md)
    
  

### <a name="how-tos-for-programming-with-social-features-in-sharepoint"></a><span data-ttu-id="c47bf-137">Руководства по программированию с использованием социальных функций в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-137">How-tos for programming with social features in SharePoint</span></span>
<span data-ttu-id="c47bf-138"><a name="bk_GetStarted"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-138"></span></span>

<span data-ttu-id="c47bf-p105">После того как настроить среду разработки и выберите сценария можно начать работу, программирование с использованием социальных функций. В таблице 1 приведены ссылки на статьи, в которых показано, как выполнять базовые задачи программирования с использованием социальных функций.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p105">After you set up your development environment and choose your scenario, you can get started programming with social features. Table 1 contains links to articles that show how to do basic programming tasks with social features.</span></span>
  
    
    

<span data-ttu-id="c47bf-141">**В таблице 1. Статьи с инструкциями по разработке с использованием социальных функций**</span><span class="sxs-lookup"><span data-stu-id="c47bf-141">**Table 1. How-to articles for developing with social features**</span></span>


|<span data-ttu-id="c47bf-142">**Функциональная область**</span><span class="sxs-lookup"><span data-stu-id="c47bf-142">**Feature area**</span></span>|<span data-ttu-id="c47bf-143">**Описание**</span><span class="sxs-lookup"><span data-stu-id="c47bf-143">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="c47bf-144">Как: сведения для чтения и записи социальных канал, чтобы с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-144">How to: Learn to read and write to the social feed by using the .NET client object model in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-net-client-object.md)|<span data-ttu-id="c47bf-145">Познакомьтесь с помощью подробные инструкции по созданию приложения, которое считывает и записывает социальных канал, чтобы с помощью клиентской объектной модели .NET.</span><span class="sxs-lookup"><span data-stu-id="c47bf-145">Walk through detailed steps for creating an application that reads and writes to the social feed by using the .NET client object model.</span></span>|
| [<span data-ttu-id="c47bf-146">Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-146">How to: Learn to read and write to the social feed by using the REST service in SharePoint</span></span>](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)|<span data-ttu-id="c47bf-147">Познакомьтесь с помощью подробные инструкции по созданию приложения, которое считывает и записывает социальные веб-канал с помощью службы REST.</span><span class="sxs-lookup"><span data-stu-id="c47bf-147">Walk through detailed steps for creating an application that reads and writes to the social feed by using the REST service.</span></span>|
| [<span data-ttu-id="c47bf-148">Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-148">How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)|<span data-ttu-id="c47bf-149">Узнайте, как создавать и удалять и публикации в микроблога и извлечение социальных веб-каналов с помощью клиентской объектной модели .NET.</span><span class="sxs-lookup"><span data-stu-id="c47bf-149">Learn how to create and delete and microblog posts and retrieve social feeds by using the .NET client object model.</span></span>|
| [<span data-ttu-id="c47bf-150">Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-150">How to: Create and delete posts and retrieve the social feed by using the JavaScript object model in SharePoint</span></span>](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)|<span data-ttu-id="c47bf-151">Узнайте, как создавать и удалять и публикации в микроблога и извлечение социальных веб-каналов с помощью объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c47bf-151">Learn how to create and delete and microblog posts and retrieve social feeds by using the JavaScript object model.</span></span>|
| [<span data-ttu-id="c47bf-152">Как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-152">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)|<span data-ttu-id="c47bf-153">Узнайте, как добавлять объекты **SocialDataItem** микроблога публикации, которые отображаются в виде упоминания, теги и ссылок в социальных веб-каналов.</span><span class="sxs-lookup"><span data-stu-id="c47bf-153">Learn how to add **SocialDataItem** objects to microblog posts, which render as mentions, tags, and links in social feeds.</span></span>|
| [<span data-ttu-id="c47bf-154">Как: Внедрение изображения, видео и документы в публикации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-154">How to: Embed images, videos, and documents in posts in SharePoint</span></span>](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md)|<span data-ttu-id="c47bf-155">Узнайте, как добавлять объекты **SocialAttachment** микроблога публикации, которые отображаются в виде внедренного изображения, видео и документами в социальных веб-каналов.</span><span class="sxs-lookup"><span data-stu-id="c47bf-155">Learn how to add **SocialAttachment** objects to microblog posts, which render as embedded pictures, videos, and documents in social feeds.</span></span>|
| [<span data-ttu-id="c47bf-156">Как: подписка на людей с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-156">How to: Follow people by using the .NET client object model in SharePoint</span></span>](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)|<span data-ttu-id="c47bf-157">Узнайте, как работа с функциями следующих пользователей с помощью клиентской объектной модели .NET.</span><span class="sxs-lookup"><span data-stu-id="c47bf-157">Learn how to work with Following People features by using the .NET client object model.</span></span>|
| [<span data-ttu-id="c47bf-158">Как: подписка на людей с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-158">How to: Follow people by using the JavaScript object model in SharePoint</span></span>](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)|<span data-ttu-id="c47bf-159">Узнайте, как работа с функциями следующих пользователей с помощью объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c47bf-159">Learn how to work with Following People features by using the JavaScript object model.</span></span>|
| [<span data-ttu-id="c47bf-160">Как: выполните документов и сайтов с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-160">How to: Follow documents and sites by using the .NET client object model in SharePoint</span></span>](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)|<span data-ttu-id="c47bf-161">Узнайте, как работа с функциями следующие контента с помощью клиентской объектной модели .NET.</span><span class="sxs-lookup"><span data-stu-id="c47bf-161">Learn how to work with Following Content features by using the .NET client object model.</span></span>|
| [<span data-ttu-id="c47bf-162">Как: выполните документы, сайты и теги с помощью службы REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-162">How to: Follow documents, sites, and tags by using the REST service in SharePoint</span></span>](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)|<span data-ttu-id="c47bf-163">Узнайте, как работа с функциями следующие контента с помощью службы REST.</span><span class="sxs-lookup"><span data-stu-id="c47bf-163">Learn how to work with Following Content features by using the REST service.</span></span>|
| [<span data-ttu-id="c47bf-164">Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-164">How to: Retrieve user profile properties by using the .NET client object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)|<span data-ttu-id="c47bf-165">Узнайте, как получение свойств профиля пользователя с помощью клиентской объектной модели .NET.</span><span class="sxs-lookup"><span data-stu-id="c47bf-165">Learn how to retrieve user profile properties by using the .NET client object model.</span></span>|
| [<span data-ttu-id="c47bf-166">Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-166">How to: Retrieve user profile properties by using the JavaScript object model in SharePoint</span></span>](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)|<span data-ttu-id="c47bf-167">Узнайте, как получение свойств профиля пользователя с помощью объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c47bf-167">Learn how to retrieve user profile properties by using the JavaScript object model.</span></span>|
| [<span data-ttu-id="c47bf-168">Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-168">How to: Work with user profiles and organization profiles by using the server object model in SharePoint</span></span>](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|<span data-ttu-id="c47bf-169">Узнайте, как создание, получение и управление свойства и профили пользователей с помощью объектной модели сервера.</span><span class="sxs-lookup"><span data-stu-id="c47bf-169">Learn how to create, retrieve, and manage user profiles and properties by using the server object model.</span></span>|
   

### <a name="apis-for-programming-with-sharepoint-social-features"></a><span data-ttu-id="c47bf-170">API-интерфейсы для программирования с использованием социальных функций SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-170">APIs for programming with SharePoint social features</span></span>
<span data-ttu-id="c47bf-171"><a name="SocialApis"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-171"></span></span>

<span data-ttu-id="c47bf-172">Несмотря на то, что приложений и решений для доступа к SharePoint по-разному, после доступа к SharePoint по сути так же, как используется социальные API.</span><span class="sxs-lookup"><span data-stu-id="c47bf-172">Although apps and solutions access SharePoint differently, after you do access SharePoint you use the social APIs in basically the same way.</span></span> <span data-ttu-id="c47bf-173">В таблице 2 показаны интерфейсы API для программирования с использованием веб-канал, выполнив, и профили пользователей возможности в SharePoint и пути к исходным файлам на сервере.</span><span class="sxs-lookup"><span data-stu-id="c47bf-173">Table 2 shows the APIs for programming with feed, following, and user profiles features in SharePoint and the paths to the source files on the server.</span></span>
  
    
    

<span data-ttu-id="c47bf-174">**В таблице 2. API-интерфейсы для программирования с использованием социальных функций**</span><span class="sxs-lookup"><span data-stu-id="c47bf-174">**Table 2. APIs for programming with social features**</span></span>


|<span data-ttu-id="c47bf-175">**Имя API**</span><span class="sxs-lookup"><span data-stu-id="c47bf-175">**API name**</span></span>|<span data-ttu-id="c47bf-176">**Источник и путь**</span><span class="sxs-lookup"><span data-stu-id="c47bf-176">**Source and path**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="c47bf-177">Клиентская объектная модель .NET</span><span class="sxs-lookup"><span data-stu-id="c47bf-177">.NET client object model</span></span>](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)|<span data-ttu-id="c47bf-178">Библиотеке Microsoft.SharePoint.Client.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="c47bf-178">Microsoft.SharePoint.Client.UserProfiles.dll</span></span><br/><span data-ttu-id="c47bf-179">в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="c47bf-179">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>|
|<span data-ttu-id="c47bf-180">клиентская объектная модель Silverlight;</span><span class="sxs-lookup"><span data-stu-id="c47bf-180">Silverlight client object model</span></span>|<span data-ttu-id="c47bf-181">Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="c47bf-181">Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll</span></span><br/><span data-ttu-id="c47bf-182">в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ШАБЛОНА\\МАКЕТОВ\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="c47bf-182">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>|
|<span data-ttu-id="c47bf-183">мобильная клиентская объектная модель.</span><span class="sxs-lookup"><span data-stu-id="c47bf-183">Mobile client object model</span></span>|<span data-ttu-id="c47bf-184">Microsoft.SharePoint.Client.UserProfiles.Phone.dll</span><span class="sxs-lookup"><span data-stu-id="c47bf-184">Microsoft.SharePoint.Client.UserProfiles.Phone.dll</span></span><br/><span data-ttu-id="c47bf-185">в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ШАБЛОНА\\МАКЕТОВ\\ClientBin</span><span class="sxs-lookup"><span data-stu-id="c47bf-185">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin</span></span>|
| [<span data-ttu-id="c47bf-186">Объектная модель JavaScript</span><span class="sxs-lookup"><span data-stu-id="c47bf-186">JavaScript object model</span></span>](http://msdn.microsoft.com/library/95cb5427-8514-4e9a-8eee-7ed4b82ec01b%28Office.15%29.aspx)|<span data-ttu-id="c47bf-187">SP. UserProfiles.js</span><span class="sxs-lookup"><span data-stu-id="c47bf-187">SP.UserProfiles.js</span></span><br/><span data-ttu-id="c47bf-188">в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ШАБЛОНА\\МАКЕТОВ</span><span class="sxs-lookup"><span data-stu-id="c47bf-188">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS</span></span>|
|<span data-ttu-id="c47bf-189">Служба передачи репрезентативного состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="c47bf-189">Representational State Transfer (REST) service</span></span>| [`http://<site url>/_api/social.feed`](social-feed-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/social.following`](following-people-and-content-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/SP.UserProfiles.PeopleManager`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx.md#bk_PeopleManager)|
| [<span data-ttu-id="c47bf-190">Серверная объектная модель.</span><span class="sxs-lookup"><span data-stu-id="c47bf-190">Server object model</span></span>](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)|<span data-ttu-id="c47bf-191">Microsoft.Office.Server.UserProfiles.dll</span><span class="sxs-lookup"><span data-stu-id="c47bf-191">Microsoft.Office.Server.UserProfiles.dll</span></span><br/><span data-ttu-id="c47bf-192">в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ISAPI</span><span class="sxs-lookup"><span data-stu-id="c47bf-192">in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ISAPI</span></span>|
   

> <span data-ttu-id="c47bf-193">**Примечание:** Не все функциональные возможности на сервере в сборке Microsoft.Office.Server.UserProfiles доступен из клиентских API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c47bf-193">**Note:** Not all server-side functionality in the Microsoft.Office.Server.UserProfiles assembly is available from client APIs.</span></span> <span data-ttu-id="c47bf-194">Доступные API-интерфейсы см пространства имен [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) и пространства имен [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c47bf-194">To see which APIs are available, see the  [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) namespace and the [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) namespace.</span></span>
  
    
    


## <a name="app-permission-requests-for-accessing-social-features-in-sharepoint-add-ins"></a><span data-ttu-id="c47bf-195">Запросы разрешений приложения для доступа к социальных функций в Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-195">App permission requests for accessing social features in SharePoint Add-ins</span></span>
<span data-ttu-id="c47bf-196"><a name="bkmk_AppPerms"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-196"></span></span>

<span data-ttu-id="c47bf-197">Надстройка SharePoint должен запрашивать разрешения, необходимые для доступа к ресурсам SharePoint от пользователя, который установит ее.</span><span class="sxs-lookup"><span data-stu-id="c47bf-197">An SharePoint Add-in must request the permissions that it needs to access SharePoint resources from the user who installs it.</span></span> <span data-ttu-id="c47bf-198">Например приложения, которая публикует веб-канал должен запрашивать разрешение **Write** (минимум) на канал.</span><span class="sxs-lookup"><span data-stu-id="c47bf-198">For example, an app that posts to the feed should request **Write** permission (at minimum) to the feed.</span></span> <span data-ttu-id="c47bf-199">Укажите разрешения, которые приложения должны в AppManifest.xml файлов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c47bf-199">You specify the permissions that your app need in the AppManifest.xml file in Visual Studio.</span></span>
  
    
    
<span data-ttu-id="c47bf-200">Запросы разрешений приложения распространяются среда развертывания SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c47bf-200">App permission requests are scoped to the SharePoint deployment landscape.</span></span> <span data-ttu-id="c47bf-201">В таблице 3 перечислены имена областей (с соответствующей области коды URI) и доступные права на доступ к социальных функций.</span><span class="sxs-lookup"><span data-stu-id="c47bf-201">Table 3 shows the scope names (with corresponding scope URIs) and the available rights for accessing social features.</span></span> <span data-ttu-id="c47bf-202">Дополнительные сведения можно [Добавить разрешения в SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx), [Add-in типы политик авторизации в SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx)и [Планирование управления разрешениями приложений в SharePoint](http://technet.microsoft.com/ru-ru/library/jj219576%28office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c47bf-202">For more information, see  [Add-in permissions in SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx),  [Add-in authorization policy types in SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx), and  [Plan app permissions management in SharePoint](http://technet.microsoft.com/ru-ru/library/jj219576%28office.15%29.aspx).</span></span>
  
    
    

<span data-ttu-id="c47bf-203">**В таблице 3. Приложение области разрешений и доступные права для социальных функций в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="c47bf-203">**Table 3. App permission scopes and available rights for social features in SharePoint**</span></span>


|<span data-ttu-id="c47bf-204">**Название области**</span><span class="sxs-lookup"><span data-stu-id="c47bf-204">**Scope name**</span></span>|<span data-ttu-id="c47bf-205">**Описание**</span><span class="sxs-lookup"><span data-stu-id="c47bf-205">**Description**</span></span>|<span data-ttu-id="c47bf-206">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="c47bf-206">**Available rights**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="c47bf-207">Профили пользователей</span><span class="sxs-lookup"><span data-stu-id="c47bf-207">User Profiles</span></span><br/>`http://sharepoint/social/tenant`|<span data-ttu-id="c47bf-p110">Область запроса разрешений для доступа к все профили пользователей. Можно изменить только изображение профиля; все другие свойства профиля пользователя доступны только для чтения для Надстройки SharePoint. Необходимо установить, администратор клиента.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p110">The permission request scope used to access all user profiles. Only the profile picture can be changed; all other user profile properties are read-only for SharePoint Add-ins. Must be installed by a tenant administrator.</span></span>|<span data-ttu-id="c47bf-210">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="c47bf-210">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="c47bf-211">Ядро</span><span class="sxs-lookup"><span data-stu-id="c47bf-211">Core</span></span><br/>`http://sharepoint/social/core`|<span data-ttu-id="c47bf-p111">Область запроса разрешений, используемые для доступа к его отслеживаемого содержимого и общих метаданных, которую использует функции микроблогов. Область применяется только к личные сайты, которые поддерживают следующие материалы. Если приложение устанавливается на любой другой тип сайта, используйте уровне клиентов.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p111">The permission request scope used to access the user's followed content and shared metadata that is used by microblogging features. This scope applies only to personal sites that support following content. If the app installs on any other type of site, use the Tenant scope.</span></span>|<span data-ttu-id="c47bf-215">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="c47bf-215">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="c47bf-216">Веб-канал новостей</span><span class="sxs-lookup"><span data-stu-id="c47bf-216">News Feed</span></span><br/>`http://sharepoint/social/microfeed`|<span data-ttu-id="c47bf-p112">Область запроса разрешений для доступа к его веб-канал или канал группы. Область применяется для личных сайтов, поддерживающих микроблогов или сайты рабочих групп, где активирован компонент **Веб-каналов сайтов**. Если приложение устанавливается на любой другой тип сайта, используйте уровне клиентов.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p112">The permission request scope used to access the user's feed or the team feed. This scope applies to personal sites that support microblogging or to team sites where the **Site Feed** feature is activated. If the app installs on any other type of site, use the Tenant scope.</span></span>|<span data-ttu-id="c47bf-220">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="c47bf-220">Read, Write, Manage, FullControl</span></span>|
| `http://sharepoint/social/trimming`|<span data-ttu-id="c47bf-p113">Эта область запроса разрешений, служит для определения, следует ли отображать контент обрезать безопасности социальных веб-канала к приложениям. Если это разрешение высоким уровнем доверия не предоставлено, часть содержимого (например, действия о документах и сайты, которые приложение не имеет разрешений на) обрезать из веб-канала данных, который возвращается в приложение даже в том случае, если у пользователя есть достаточные разрешения. Это разрешение необходимо вручную добавить в файл манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p113">This permission request scope used to determine whether to display security-trimmed content in the social feed to apps. If this high-trust permission is not granted, some content (such as activities about documents and sites that the app doesn't have permissions to) is trimmed from the feed data that's returned to the app, even if the user has sufficient permissions. This permission must be manually added to the app's manifest file.</span></span>|<span data-ttu-id="c47bf-224">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="c47bf-224">Read, Write, Manage, FullControl</span></span>|
   

### <a name="what-youll-need-to-consider-when-requesting-app-permissions"></a><span data-ttu-id="c47bf-225">Что необходимо учитывать при запросе разрешений приложения</span><span class="sxs-lookup"><span data-stu-id="c47bf-225">What you'll need to consider when requesting app permissions</span></span>

<span data-ttu-id="c47bf-226">Следует иметь в виду следующие соображения при указании приложения разрешения на использование социальных компонентов:</span><span class="sxs-lookup"><span data-stu-id="c47bf-226">You should be aware of the following considerations when you specify app permissions for social features:</span></span>
  
    
    

- <span data-ttu-id="c47bf-p114">Приложения, которые задают **FullControl** правами не допускается для Магазин Office приложений. Права **Read**, **Write**и **Manage** могут Магазин Office приложений.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p114">Apps that specify **FullControl** rights are not allowed for Office Store apps. Only **Read**, **Write**, and **Manage** rights are allowed for Office Store apps.</span></span>
    
  
- <span data-ttu-id="c47bf-p115">Можно задать разрешения для веб-каналов и следующие функции с помощью основных, канала новостей и областей клиента ( `http://sharepoint/content/tenant`). Область клиента представляет всей аренды установки приложения, включая областей ядро и веб-канал новостей. Поэтому если ваше приложение уже указывает права, которые требуется на уровне клиента, не нужно запрашивать разрешения на уровне ядра или веб-канал новостей.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p115">You can specify permissions for feed and following features by using the Core, News Feed, and Tenant ( `http://sharepoint/content/tenant`) scopes. The Tenant scope represents the whole tenancy where an app is installed, including the Core and News Feed scopes. So if your app already specifies the rights that it needs at the Tenant scope, then you don't need to request permissions at the Core or News Feed scope.</span></span>
    
  
- <span data-ttu-id="c47bf-p116">Во время разработки, используйте уровне клиентов, если вы получаете "SocialListNotFound: социальные списка не существует на личном узле" или «Файл не найден» сообщения. Если вы хотите использовать область основных или веб-канала новостей в вашем приложении, вы можете проверить разрешения, открыв приложения из каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="c47bf-p116">During development, use the Tenant scope if you get a "SocialListNotFound : The Social list does not exist in your personal site" or "File Not Found" message. If you want to use the Core or News Feed scope in your app, you can test the permissions by opening the app from the app catalog.</span></span>
    
  
- <span data-ttu-id="c47bf-p117">Основные области применяется к личные сайты, которые поддерживают следующие материалы. На уровне веб-канал новостей применяется для личных сайтов, поддерживающих микроблогов или сайты рабочих групп, где активирован компонент **Веб-каналов сайтов**. Если приложение будет установлен на любой другой тип сайта, необходимо использовать уровне клиентов. В разделе  [Сроки аренды и области развертывания надстроек для SharePoint](http://msdn.microsoft.com/library/1ceb3142-a7a5-453e-920f-5f953a79401a%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c47bf-p117">The Core scope applies to personal sites that support following content. The News Feed scope applies to personal sites that support microblogging or to team sites where the **Site Feed** feature is activated. If the app will be installed on any other type of site, you must use the Tenant scope. See [Tenancies and deployment scopes for SharePoint Add-ins](http://msdn.microsoft.com/library/1ceb3142-a7a5-453e-920f-5f953a79401a%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="c47bf-238">Администратор клиента должен быть установлен приложений, запрашивающих права для области профили пользователей и их нельзя установить в версии Office 365 для малого бизнеса расширенный SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="c47bf-238">Apps that request rights for the User Profiles scope must be installed by a tenant administrator, and they cannot be installed in Office 365 Small Business Premium version of SharePoint Online.</span></span>
    
  
- <span data-ttu-id="c47bf-239">Если не выполняются требования к активации лицензирования или компонент для возможности социальных вычислений и микроблогов, пользователи получают сообщение о том, что они не могут установить приложение.</span><span class="sxs-lookup"><span data-stu-id="c47bf-239">If licensing or feature activation requirements for social and microblogging features are not met, users get a message saying that they can't install the app.</span></span>
    
  
- <span data-ttu-id="c47bf-240">Приложения, которые запускаются за пределами SharePoint может запрашивать разрешение на динамически (за исключением **Полный доступ**).</span><span class="sxs-lookup"><span data-stu-id="c47bf-240">Apps that are launched outside of SharePoint can request permission on-the-fly (except **Full Control**).</span></span> <span data-ttu-id="c47bf-241">Для получения дополнительных сведений см [процесс авторизации OAuth кода для SharePoint надстройки](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c47bf-241">For more information, see  [Authorization Code OAuth flow for SharePoint Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="c47bf-242">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c47bf-242">Additional resources</span></span>
<span data-ttu-id="c47bf-243"><a name="bk_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="c47bf-243"></span></span>

 <span data-ttu-id="c47bf-244">**Основные статьи**</span><span class="sxs-lookup"><span data-stu-id="c47bf-244">**Conceptual articles**</span></span>
  
    
    

-  [<span data-ttu-id="c47bf-245">Функции социальных медиа и совместной работы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-245">Social and collaboration features in SharePoint</span></span>](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c47bf-246">Новые возможности социальных сетей и совместной работы в SharePoint для разработчиков</span><span class="sxs-lookup"><span data-stu-id="c47bf-246">What's new for developers in social and collaboration features in SharePoint</span></span>](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md)
    
  
-  [<span data-ttu-id="c47bf-247">Планирование социальных вычислений и совместной работы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-247">Plan for social computing and collaboration in SharePoint</span></span>](http://technet.microsoft.com/ru-ru/library/ee662531%28v=office.15%29)
    
  
-  [<span data-ttu-id="c47bf-248">Настройка компонентов социальных сетей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-248">Configure social computing features in SharePoint</span></span>](http://technet.microsoft.com/ru-ru/library/fp161267%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="c47bf-249">Социальные терминология и концепции сетей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-249">Social computing terminology and concepts in SharePoint</span></span>](http://technet.microsoft.com/ru-ru/library/jj219804%28v=office.15%29.aspx)
    
  
 <span data-ttu-id="c47bf-250">**Справочная документация**</span><span class="sxs-lookup"><span data-stu-id="c47bf-250">**Reference documentation**</span></span>
  
    
    

-  [<span data-ttu-id="c47bf-251">Библиотека классов клиента социальных сетей</span><span class="sxs-lookup"><span data-stu-id="c47bf-251">Social client class library</span></span>](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c47bf-252">SP. Справочник по JavaScript UserProfiles.js</span><span class="sxs-lookup"><span data-stu-id="c47bf-252">SP.UserProfiles.js JavaScript Reference</span></span>](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c47bf-253">Social feed REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-253">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="c47bf-254">Following people and content REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="c47bf-254">Following people and content REST API reference for SharePoint</span></span>](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="c47bf-255">Справочник по API REST для профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="c47bf-255">User profiles REST API reference</span></span>](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c47bf-256">Библиотека классов сервера SharePoint социальных сетей</span><span class="sxs-lookup"><span data-stu-id="c47bf-256">SharePoint Social server class library</span></span>](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)
    
  
