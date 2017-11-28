---
title: "Интеграция Yammer в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a83623a32b398ae32ce7cebc7ac5d37c823a2e3f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="yammer-integration-in-the-sharepoint-add-in-model"></a><span data-ttu-id="9543e-102">Интеграция Yammer в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="9543e-102">Yammer integration in the SharePoint add-in model</span></span>
=================================================

<a name="summary"></a><span data-ttu-id="9543e-103">Summary</span><span class="sxs-lookup"><span data-stu-id="9543e-103">Summary</span></span>
-------

<span data-ttu-id="9543e-104">Выбор подхода к интеграции сети Yammer с помощью SharePoint аналогична в новой модели надстройки SharePoint как есть с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="9543e-104">The approach you take to integrate Yammer with SharePoint is the same in the new SharePoint Add-in model as it is with Full Trust Code.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="9543e-105">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="9543e-105">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="9543e-106">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее интеграции сети Yammer с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-106">As a rule of a thumb, we would like to provide the following high level guidelines to integrate Yammer with SharePoint.</span></span>

- <span data-ttu-id="9543e-107">Yammer интеграции может использоваться в локальной и среды Office 365 SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-107">Yammer integration may be used in both on-premises and Office 365  SharePoint environments.</span></span>
- <span data-ttu-id="9543e-108">Удаленный подготовки шаблон можно использовать для создания группы Yammer и/или Yammer OpenGraph объекты для упрощения бесед при создании новых сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-108">You can use the remote provisioning pattern to create Yammer groups and/or Yammer OpenGraph objects to facilitate conversations when you create new SharePoint sites.</span></span>
- <span data-ttu-id="9543e-109">Можно использовать-стандартной внедрить возможность быстро и легко интеграции сети Yammer с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-109">You can use the out-of-the-box embed functionality to quickly and easily integrate Yammer with SharePoint.</span></span>
    + <span data-ttu-id="9543e-110">Для использования внедрить вы должны контейнер 400 пикселей HTML и более в приложении.</span><span class="sxs-lookup"><span data-stu-id="9543e-110">To use embed you need a HTML container 400 pixels or larger in your application.</span></span>
- <span data-ttu-id="9543e-111">Yammer пакеты SDK и API-интерфейсы REST можно использовать для создания настраиваемой интеграции функций.</span><span class="sxs-lookup"><span data-stu-id="9543e-111">You can use the Yammer SDKs and REST APIs to create customized integration functionality.</span></span>

<a name="options-to-integrate-yammer-with-sharepoint"></a><span data-ttu-id="9543e-112">Параметры для интеграции сети Yammer с SharePoint</span><span class="sxs-lookup"><span data-stu-id="9543e-112">Options to integrate Yammer with SharePoint</span></span>
-------------------------------------------

<span data-ttu-id="9543e-113">У вас есть несколько вариантов для интеграции сети Yammer с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-113">You have a few options to integrate Yammer with SharePoint.</span></span>

- <span data-ttu-id="9543e-114">Внедрить</span><span class="sxs-lookup"><span data-stu-id="9543e-114">Embed</span></span>
    + <span data-ttu-id="9543e-115">Группа, тема, My и каналы новостей пользователей</span><span class="sxs-lookup"><span data-stu-id="9543e-115">Group, Topic, My, and User Feeds</span></span>
    + <span data-ttu-id="9543e-116">OpenGraph веб-каналов</span><span class="sxs-lookup"><span data-stu-id="9543e-116">OpenGraph Feeds</span></span>
- <span data-ttu-id="9543e-117">Yammer OpenGraph API и/или интерфейса API REST Yammer с Yammer пакеты SDK</span><span class="sxs-lookup"><span data-stu-id="9543e-117">Yammer OpenGraph API and/or Yammer REST API with Yammer SDKs</span></span>
    
<a name="embed"></a><span data-ttu-id="9543e-118">Внедрить</span><span class="sxs-lookup"><span data-stu-id="9543e-118">Embed</span></span>
-----

<span data-ttu-id="9543e-119">В этом параметре внедрять Yammer, веб-канал на веб-странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-119">In this option you embed a Yammer feed in a SharePoint web page.</span></span>
    
- <span data-ttu-id="9543e-120">Этот параметр, быстро и легко реализуется.</span><span class="sxs-lookup"><span data-stu-id="9543e-120">This option is quickly and easily implemented.</span></span>
- <span data-ttu-id="9543e-121">Этот параметр позволяет управлять ограниченный аспектов веб-канал и как он находится.</span><span class="sxs-lookup"><span data-stu-id="9543e-121">This option allows you to control limited aspects of the feed and how it appears.</span></span>

<span data-ttu-id="9543e-122">На странице SharePoint с помощью внедрить выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9543e-122">Using embed looks like this in your SharePoint page:</span></span>

![Стандартные страницы сайта SharePoint team с текстовое поле, которое содержит текст, начать беседу.](media/Recipes/Yammer/YammerEmbed.png)

<span data-ttu-id="9543e-125">В следующей таблице описываются каждого типа ожидания введите встраивания веб-канал, чтобы воспользоваться с Yammer.</span><span class="sxs-lookup"><span data-stu-id="9543e-125">The following table describes each type of Yammer feed you can access with embed out-of-the-box.</span></span>

<span data-ttu-id="9543e-126">Веб-канала</span><span class="sxs-lookup"><span data-stu-id="9543e-126">Feed</span></span> | <span data-ttu-id="9543e-127">Описание</span><span class="sxs-lookup"><span data-stu-id="9543e-127">Description</span></span> | <span data-ttu-id="9543e-128">FeedType</span><span class="sxs-lookup"><span data-stu-id="9543e-128">FeedType</span></span> | <span data-ttu-id="9543e-129">Пример использования</span><span class="sxs-lookup"><span data-stu-id="9543e-129">Use Case</span></span>
---- | ----------- | -------- | --------
<span data-ttu-id="9543e-130">Мой канал</span><span class="sxs-lookup"><span data-stu-id="9543e-130">My Feed</span></span> | <span data-ttu-id="9543e-131">Веб-каналов, где будут доставляться беседы для пользователей Yammer.</span><span class="sxs-lookup"><span data-stu-id="9543e-131">My Feeds are where conversations are delivered for Yammer users.</span></span> | <span data-ttu-id="9543e-132">MyFeed</span><span class="sxs-lookup"><span data-stu-id="9543e-132">MyFeed</span></span> | <span data-ttu-id="9543e-133">Сайт главной страницы или рабочей области сайте.</span><span class="sxs-lookup"><span data-stu-id="9543e-133">My Site homepage or workspace site.</span></span>
<span data-ttu-id="9543e-134">Веб-канал пользователя</span><span class="sxs-lookup"><span data-stu-id="9543e-134">User Feed</span></span> | <span data-ttu-id="9543e-135">Все беседы, размещенные отдельного пользователя в сети Yammer.</span><span class="sxs-lookup"><span data-stu-id="9543e-135">All the conversations posted by a specific user in Yammer.</span></span> | <span data-ttu-id="9543e-136">пользователь;</span><span class="sxs-lookup"><span data-stu-id="9543e-136">User</span></span> | <span data-ttu-id="9543e-137">Страницы профилей пользователей в каталоге системы.</span><span class="sxs-lookup"><span data-stu-id="9543e-137">Profile pages for users in a system directory.</span></span>
<span data-ttu-id="9543e-138">Раздел веб-канал</span><span class="sxs-lookup"><span data-stu-id="9543e-138">Topic Feed</span></span> | <span data-ttu-id="9543e-139">Канал бесед, которые помечены раздел в Yammer.</span><span class="sxs-lookup"><span data-stu-id="9543e-139">A feed of conversations that have been tagged with a topic in Yammer.</span></span> | <span data-ttu-id="9543e-140">Раздел</span><span class="sxs-lookup"><span data-stu-id="9543e-140">Topic</span></span> | <span data-ttu-id="9543e-141">На странице событий во внутренней сети.</span><span class="sxs-lookup"><span data-stu-id="9543e-141">An event page on an intranet.</span></span>
<span data-ttu-id="9543e-142">Канал группы</span><span class="sxs-lookup"><span data-stu-id="9543e-142">Group Feed</span></span> | <span data-ttu-id="9543e-143">Канал бесед, которые были учтены в указанной группы.</span><span class="sxs-lookup"><span data-stu-id="9543e-143">A feed of conversations that have been posted in a specified group.</span></span> | <span data-ttu-id="9543e-144">Group</span><span class="sxs-lookup"><span data-stu-id="9543e-144">Group</span></span> | <span data-ttu-id="9543e-145">Страница группы во внутренней сети.</span><span class="sxs-lookup"><span data-stu-id="9543e-145">A team page on an intranet.</span></span>

<span data-ttu-id="9543e-146">Если вам потребуется за пределы возможностей каналы Yammer вне поля в таблице, можно использовать OpenGraph могут внедрять параметр.</span><span class="sxs-lookup"><span data-stu-id="9543e-146">If you need to go beyond the capabilities of the out-of-the-box Yammer feeds in the table above you can use the OpenGraph embed option.</span></span>  <span data-ttu-id="9543e-147">Этот параметр позволяет управлять веб-канала.</span><span class="sxs-lookup"><span data-stu-id="9543e-147">This option gives you more control of the feed.</span></span>  <span data-ttu-id="9543e-148">В следующей таблице показан пример.</span><span class="sxs-lookup"><span data-stu-id="9543e-148">The following table illustrates such an example.</span></span>

<span data-ttu-id="9543e-149">Веб-канала</span><span class="sxs-lookup"><span data-stu-id="9543e-149">Feed</span></span> | <span data-ttu-id="9543e-150">Описание</span><span class="sxs-lookup"><span data-stu-id="9543e-150">Description</span></span> | <span data-ttu-id="9543e-151">FeedType</span><span class="sxs-lookup"><span data-stu-id="9543e-151">FeedType</span></span> | <span data-ttu-id="9543e-152">Пример использования</span><span class="sxs-lookup"><span data-stu-id="9543e-152">Use Case</span></span>
---- | ----------- | -------- | --------
<span data-ttu-id="9543e-153">Комментарий веб-канал</span><span class="sxs-lookup"><span data-stu-id="9543e-153">Comment  Feed</span></span> | <span data-ttu-id="9543e-154">Используется в Yammer диаграммы прикладной программный Интерфейс для облегчения беседы вокруг объекта приложения.</span><span class="sxs-lookup"><span data-stu-id="9543e-154">Uses Yammer’s Open Graph API to facilitate conversation around an application object.</span></span> | <span data-ttu-id="9543e-155">Пользовательский</span><span class="sxs-lookup"><span data-stu-id="9543e-155">Custom</span></span> | <span data-ttu-id="9543e-156">Возможность в мультимедиа или пользовательского приложения CRM странице сведений в системе управления цифровыми активами.</span><span class="sxs-lookup"><span data-stu-id="9543e-156">An opportunity in a custom CRM application, or a media detail page in a digital asset management system.</span></span>

<span data-ttu-id="9543e-157">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="9543e-157">**When is it a good fit?**</span></span>

<span data-ttu-id="9543e-158">При попытке интегрировать каналы Yammer с сайтами SharePoint и возможности ожидания введите канал embed соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="9543e-158">When you are trying to integrate Yammer feeds with SharePoint sites and the out-of-the-box capabilities of the embed feed meet your needs.</span></span>

<span data-ttu-id="9543e-159">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="9543e-159">**Getting Started**</span></span>

<span data-ttu-id="9543e-160">Следующий пример демонстрирует Подготовка сайтов с помощью канала Yammer узла вместо новостей по умолчанию для сайта.</span><span class="sxs-lookup"><span data-stu-id="9543e-160">The following sample demonstrates how to provision sites with a Yammer feed associated with the site in place of the default news feed for the site.</span></span>

- [<span data-ttu-id="9543e-161">Provisioning.Yammer (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9543e-161">Provisioning.Yammer (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)

<span data-ttu-id="9543e-162">Метод **CreateYammerGroupDiscussionPartXml** в классе [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) , поступающие из примера [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .</span><span class="sxs-lookup"><span data-stu-id="9543e-162">The **CreateYammerGroupDiscussionPartXml** method in the [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) class comes from the [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) sample.</span></span>  <span data-ttu-id="9543e-163">Этот метод создает XML-код для определения части Add-in, который добавляется на страницу SharePoint при подготовке сайта.</span><span class="sxs-lookup"><span data-stu-id="9543e-163">This method creates the XML for an Add-in Part definition that is added to a SharePoint page when a site is provisioned.</span></span>  <span data-ttu-id="9543e-164">Уведомление о **feedType: «группа»** фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="9543e-164">Notice the **feedType: 'group'** portion of the code.</span></span>  <span data-ttu-id="9543e-165">Здесь можно увидеть, что feedType настроена на использование feedType ожидания введите группы.</span><span class="sxs-lookup"><span data-stu-id="9543e-165">Here you can see the feedType is set to use the out-of-the-box group feedType.</span></span>

    public static string CreateYammerGroupDiscussionPartXml(string yammerNetworkName, int yammerGroupId, bool showHeader, bool showFooter, bool useSSO = true)
    {
        StringBuilder wp = new StringBuilder(100);
        wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
        wp.Append("<webParts>");
        wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
        wp.Append("     <metaData>");
        wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
        wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
        wp.Append("     </metaData>");
        wp.Append("     <data>");
        wp.Append("         <properties>");
        wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
        wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
        wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
        wp.Append("             <property name='Content' type='string'>");
        wp.Append("             <![CDATA[");
        wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
        wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
        wp.Append("                 <script type='text/javascript'>  
                                        yam.connect.embedFeed({ container: '#embedded-feed', network: '"
                                        + yammerNetworkName
                                        + @"', feedType: 'group', feedId: '" + yammerGroupId            
                                        + @"', config: { use_sso: " + useSSO.ToString().ToLower()           
                                        + @", header: " + showHeader.ToString().ToLower()
                                        + @", footer: " + showFooter.ToString().ToLower()
                                        + " }}); </script>");
        wp.Append("             ]]>");
        wp.Append("             </property>");
        wp.Append("         </properties>");
        wp.Append("     </data>");
        wp.Append(" </webPart>");
        wp.Append("</webParts>");

        return wp.ToString();
    }

<span data-ttu-id="9543e-166">Метод **CreateYammerOpenGraphDiscussionPartXml** в классе [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) , поступающие из примера [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) .</span><span class="sxs-lookup"><span data-stu-id="9543e-166">The **CreateYammerOpenGraphDiscussionPartXml** method in the [YammerUtility.cs](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Utilities/YammerUtility.cs) class comes from the [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/OfficeDevPnP.Core) sample.</span></span>  <span data-ttu-id="9543e-167">Этот метод создает XML-код для определения части Add-in, который добавляется на страницу SharePoint при подготовке сайта.</span><span class="sxs-lookup"><span data-stu-id="9543e-167">This method creates the XML for an Add-in Part definition that is added to a SharePoint page when a site is provisioned.</span></span>  <span data-ttu-id="9543e-168">Уведомление о **feedType: «открыть график»** фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="9543e-168">Notice the **feedType: 'open-graph'** portion of the code.</span></span>  <span data-ttu-id="9543e-169">Здесь можно увидеть, что feedType настроена на использование OpenGraph API.</span><span class="sxs-lookup"><span data-stu-id="9543e-169">Here you can see the feedType is set to use the OpenGraph API.</span></span>

    public static string CreateYammerOpenGraphDiscussionPartXml(string yammerNetworkName, string url, bool showHeader, 
                                                                    bool showFooter, string postTitle="", string postImageUrl="", 
                                                                    bool useSso = true, string groupId = "")
        {
            StringBuilder wp = new StringBuilder(100);
            wp.Append("<?xml version=\"1.0\" encoding=\"utf-8\" ?>");
            wp.Append("<webParts>");
            wp.Append(" <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>");
            wp.Append("     <metaData>");
            wp.Append("         <type name='Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />");
            wp.Append("         <importErrorMessage>Cannot import this Web Part.</importErrorMessage>");
            wp.Append("     </metaData>");
            wp.Append("     <data>");
            wp.Append("         <properties>");
            wp.Append("             <property name='Title' type='string'>$Resources:core,ScriptEditorWebPartTitle;</property>");
            wp.Append("             <property name='Description' type='string'>$Resources:core,ScriptEditorWebPartDescription;</property>");
            wp.Append("             <property name='ChromeType' type='chrometype'>None</property>");
            wp.Append("             <property name='Content' type='string'>");
            wp.Append("             <![CDATA[");
            wp.Append("                 <div id='embedded-feed' style='height: 500px;'></div>");
            wp.Append("                 <script type='text/javascript' src='https://assets.yammer.com/assets/platform_embed.js'></script>");
            wp.Append("                 <script>");
            wp.Append("                     yam.connect.embedFeed({");
            wp.Append("                       container: '#embedded-feed'");
            wp.Append("                             , feedType: 'open-graph'");
            wp.Append("                             , feedId: ''");
            wp.Append("                             , config: {");
            wp.Append("                                  use_sso: " + useSso.ToString().ToLower());
            wp.Append("                                  , header: " + showHeader.ToString().ToLower());
            wp.Append("                                  , footer: " + showFooter.ToString().ToLower());
            wp.Append("                                  , showOpenGraphPreview: false");
            wp.Append("                                  , defaultToCanonical: false");
            wp.Append("                                  , hideNetworkName: false");
            wp.Append("                                  , promptText: 'Start a conversation'");
            if (!string.IsNullOrEmpty(groupId))
            {
                wp.Append("                              , defaultGroupId: '" + groupId + "'"); 
            }
            wp.Append("                             }");
            wp.Append("                             , objectProperties: {"); 
            wp.Append("                               url: '" + url + "'");
            wp.Append("                               , type: 'page'");
            wp.Append("                               , title: '" + postTitle + "'");
            wp.Append("                               , image: '" + postImageUrl + "'");
            wp.Append("                             }");
            wp.Append("                         });");
            wp.Append("                     </script>");
            wp.Append("             ]]>");
            wp.Append("             </property>");
            wp.Append("         </properties>");
            wp.Append("     </data>");
            wp.Append(" </webPart>");
            wp.Append("</webParts>");

            return wp.ToString();
        }

<span data-ttu-id="9543e-170">Просмотрите [интеграции Yammer веб-каналов для сайтов SharePoint (O365 PnP видео)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites) для просмотра прохода of - [Provisioning.Yammer (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer).</span><span class="sxs-lookup"><span data-stu-id="9543e-170">Watch the [Integrate Yammer feeds to SharePoint sites (O365 PnP Video)](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites) to see a walk through of the - [Provisioning.Yammer (O365 PnP Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer).</span></span>

<span data-ttu-id="9543e-171">Для внедрения Дополнительные сведения о сети Yammer в статье [Yammer внедрения веб-канала (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/embed) .</span><span class="sxs-lookup"><span data-stu-id="9543e-171">For more information about Yammer embed see the [Yammer Embed Feed (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/embed) article.</span></span>

<span data-ttu-id="9543e-172">Дополнительные сведения о Yammer OpenGraph в статье [Open Общие сведения о графике & Формат (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/open-graph) .</span><span class="sxs-lookup"><span data-stu-id="9543e-172">For more information about Yammer OpenGraph see the [Open Graph Introduction & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) article.</span></span>

<a name="yammer-opengraph-api--yammer-rest-api-with-yammer-sdks"></a><span data-ttu-id="9543e-173">Yammer OpenGraph API & API-Интерфейс REST Yammer с Yammer пакеты SDK</span><span class="sxs-lookup"><span data-stu-id="9543e-173">Yammer OpenGraph API & Yammer REST API with Yammer SDKs</span></span>
-------------------------------------------------------

<span data-ttu-id="9543e-174">В этом параметре используется Yammer OpenGraph API и/или интерфейса API REST Yammer с Yammer пакеты SDK для интеграции сети Yammer с помощью SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9543e-174">In this option you use the Yammer OpenGraph API and/or Yammer REST API with Yammer SDKs to integrate Yammer with SharePoint.</span></span>  <span data-ttu-id="9543e-175">Эти API-интерфейсы также могут быть использованы для интеграции сети Yammer с процессами за пределами веб-страниц.</span><span class="sxs-lookup"><span data-stu-id="9543e-175">These APIs may also be used to integrate Yammer with processes outside of web pages.</span></span>  <span data-ttu-id="9543e-176">Такие сценарии примеры служб и длительной операции.</span><span class="sxs-lookup"><span data-stu-id="9543e-176">Examples of such scenarios include services and long running operations.</span></span> 
    
- <span data-ttu-id="9543e-177">Этот параметр занимает больше времени для реализации.</span><span class="sxs-lookup"><span data-stu-id="9543e-177">This option takes longer to implement.</span></span>
- <span data-ttu-id="9543e-178">Этот параметр позволяет управлять все аспекты веб-канал и как оно отображается и взаимодействия с ним.</span><span class="sxs-lookup"><span data-stu-id="9543e-178">This option allows you to control all aspects of the feed and how it appears and how you interact with it.</span></span>

<span data-ttu-id="9543e-179">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="9543e-179">**When is it a good fit?**</span></span>

- <span data-ttu-id="9543e-180">Когда вы пытаетесь интегрировать каналы Yammer с сайтами SharePoint и ожидания введите возможности веб-каналов embed не отвечают вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="9543e-180">When you are trying to integrate Yammer feeds with SharePoint sites and the out-of-the-box capabilities of the embed feeds do not meet your needs.</span></span>
- <span data-ttu-id="9543e-181">Когда вы пытаетесь интеграции каналы Yammer в служб или длительной операции.</span><span class="sxs-lookup"><span data-stu-id="9543e-181">When you are trying to integrate Yammer feeds into services or long running operations.</span></span>

<span data-ttu-id="9543e-182">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="9543e-182">**Getting Started**</span></span>

<span data-ttu-id="9543e-183">Дополнительные сведения о Yammer OpenGraph в статье [Open Общие сведения о графике & Формат (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/open-graph) .</span><span class="sxs-lookup"><span data-stu-id="9543e-183">For more information about Yammer OpenGraph see the [Open Graph Introduction & Format (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/open-graph) article.</span></span>

<span data-ttu-id="9543e-184">Пакеты SDK для Yammer дают возможность проходить проверку подлинности в сети Yammer.</span><span class="sxs-lookup"><span data-stu-id="9543e-184">Yammer SDKs provide you the ability to authenticate to Yammer.</span></span>  <span data-ttu-id="9543e-185">Дополнительные сведения о SDK Yammer увидеть следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="9543e-185">For more information about the Yammer SDKs see the following articles:</span></span>

- [<span data-ttu-id="9543e-186">Пакет SDK для JavaScript</span><span class="sxs-lookup"><span data-stu-id="9543e-186">JavaScript SDK</span></span>](https://developer.yammer.com/v1.0/docs/js-sdk)
- [<span data-ttu-id="9543e-187">Произносится SDK</span><span class="sxs-lookup"><span data-stu-id="9543e-187">Ruby SDK</span></span>](https://developer.yammer.com/v1.0/docs/ruby-sdk)
- [<span data-ttu-id="9543e-188">Python SDK</span><span class="sxs-lookup"><span data-stu-id="9543e-188">Python SDK</span></span>](https://developer.yammer.com/v1.0/docs/python-sdk)
- [<span data-ttu-id="9543e-189">пакет SDK для iOS</span><span class="sxs-lookup"><span data-stu-id="9543e-189">iOS SDK</span></span>](https://developer.yammer.com/v1.0/docs/ios-sdk)
- [<span data-ttu-id="9543e-190">ПАКЕТ SDK ДЛЯ .NET</span><span class="sxs-lookup"><span data-stu-id="9543e-190">.NET SDK</span></span>](https://developer.yammer.com/v1.0/docs/net-sdk)
- [<span data-ttu-id="9543e-191">Windows Phone 8 SDK</span><span class="sxs-lookup"><span data-stu-id="9543e-191">Windows Phone 8 SDK</span></span>](https://developer.yammer.com/v1.0/docs/windows-phone-8-sdk)

<span data-ttu-id="9543e-192">После проверки подлинности в Yammer с помощью SDK Yammer можно вызывать API REST Yammer.</span><span class="sxs-lookup"><span data-stu-id="9543e-192">After you have authenticated to Yammer via the Yammer SDKs you can call the Yammer REST APIs.</span></span>  

<span data-ttu-id="9543e-193">Дополнительные сведения о Yammer API-интерфейсы REST в статье [API -Интерфейс REST & ограничения скорости (Yammer центр для разработчиков)](https://developer.yammer.com/v1.0/docs/rest-api-rate-limits) .</span><span class="sxs-lookup"><span data-stu-id="9543e-193">For more information about Yammer REST APIs see the [REST API & Rate Limits (Yammer Developer Center)](https://developer.yammer.com/v1.0/docs/rest-api-rate-limits) article.</span></span>

<span data-ttu-id="9543e-194">**Примечание проверки подлинности**</span><span class="sxs-lookup"><span data-stu-id="9543e-194">**Authentication Note**</span></span>

<span data-ttu-id="9543e-195">В сценарии, где входа в SharePoint с использованием учетных данных, которые отличаются от учетных данных, используемые для входа в SharePoint с помощью вы можете разработать функцию единого входа для пользователей.</span><span class="sxs-lookup"><span data-stu-id="9543e-195">In a scenario where you sign into SharePoint with credentials that differ from the credentials you use to sign into SharePoint with you may wish to develop a single-sign-on capability for your users.</span></span>  <span data-ttu-id="9543e-196">Пример такой ситуации — при входе в SharePoint с помощью LiveID и нужно входить в Yammer с Microsoft личных или рабочих учетной записи.</span><span class="sxs-lookup"><span data-stu-id="9543e-196">An example of such a scenario is when you sign into SharePoint with a LiveID and you need to sign into Yammer with a Microsoft personal or work account.</span></span>

<span data-ttu-id="9543e-197">Для реализации сценария single sign on может направлять пользователей для входа в Yammer при первом они поступают на страницу SharePoint с помощью настраиваемого компонента Yammer на нем.</span><span class="sxs-lookup"><span data-stu-id="9543e-197">To implement a single-sign-on scenario you can direct your users to sign into Yammer the first time they come to a SharePoint page with your custom Yammer component on it.</span></span> <span data-ttu-id="9543e-198">После входе пользователя в сети Yammer с помощью пакета SDK Yammer можно хранить маркер обновления для пользователя в своем профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="9543e-198">After the user signs into Yammer via the Yammer SDK you can store the refresh token for the user in their user profile.</span></span>  <span data-ttu-id="9543e-199">Затем на последующих посещений страницы можно получить маркер обновления из профиля пользователя и используйте его для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9543e-199">Then, on subsequent visits to the page you can retrieve the refresh token from the user profile and use it to authenticate.</span></span>  <span data-ttu-id="9543e-200">При использовании этого подхода конечных пользователей, достаточно для входа в Yammer при истечении срока действия маркера их обновления.</span><span class="sxs-lookup"><span data-stu-id="9543e-200">With this approach your end users only need to sign into Yammer when their refresh token expires.</span></span>

<a name="related-links"></a><span data-ttu-id="9543e-201">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="9543e-201">Related links</span></span>
=============
- [<span data-ttu-id="9543e-202">Интеграция веб-каналы Yammer на сайтах SharePoint (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="9543e-202">Integrate Yammer feeds to SharePoint sites (O365 PnP Video)</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Integrate-Yammer-feeds-to-SharePoint-sites)
- [<span data-ttu-id="9543e-203">Yammer внедрения веб-канал (Yammer центр для разработчиков)</span><span class="sxs-lookup"><span data-stu-id="9543e-203">Yammer Embed Feed (Yammer Developer Center)</span></span>](https://developer.yammer.com/v1.0/docs/embed)
- [<span data-ttu-id="9543e-204">Общие сведения о графике Open & Формат (Yammer центр для разработчиков)</span><span class="sxs-lookup"><span data-stu-id="9543e-204">Open Graph Introduction & Format (Yammer Developer Center)</span></span>](https://developer.yammer.com/v1.0/docs/open-graph)
- <span data-ttu-id="9543e-205">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="9543e-205">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="9543e-206">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="9543e-206">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="9543e-207">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="9543e-207">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="9543e-208">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="9543e-208">Related PnP samples</span></span>
===================
- [<span data-ttu-id="9543e-209">Provisioning.Yammer (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9543e-209">Provisioning.Yammer (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Yammer)
- [<span data-ttu-id="9543e-210">OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="9543e-210">OfficeDevPnP.Core</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
- <span data-ttu-id="9543e-211">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="9543e-211">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="9543e-212">Применимо к</span><span class="sxs-lookup"><span data-stu-id="9543e-212">Applies to</span></span>
==========
- <span data-ttu-id="9543e-213">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="9543e-213">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="9543e-214">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="9543e-214">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="9543e-215">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="9543e-215">SharePoint 2013 on-premises</span></span>
