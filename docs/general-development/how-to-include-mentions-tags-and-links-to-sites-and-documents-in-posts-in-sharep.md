---
title: "Включить упоминания, теги и ссылки на сайты и документы в публикации в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 975da333-372b-4bf6-a3f4-7452db369f04
ms.openlocfilehash: f0af1c97baf6da530358f2a2ff86f29e2f9bb03e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharepoint"></a><span data-ttu-id="83d01-102">Включить упоминания, теги и ссылки на сайты и документы в публикации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-102">Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>

<span data-ttu-id="83d01-103">Узнайте, как добавлять в записи микроблога объекты [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx), которые отображаются в каналах SharePoint в виде упоминаний, тегов или ссылок.</span><span class="sxs-lookup"><span data-stu-id="83d01-103">Learn how to add  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) objects to microblog posts, which render as mentions, tags, or links in SharePoint social feeds.</span></span>
<span data-ttu-id="83d01-104">В социальных веб-канал простейшей формой post контента содержит только текст, но также можно добавлять ссылки, которые отображаются в виде упоминания теги и ссылки на веб-сайты, сайты SharePoint и документы.</span><span class="sxs-lookup"><span data-stu-id="83d01-104">In a social feed, the simplest form of post content contains only text, but you can also add links that render as mentions, tags, or links to websites, SharePoint sites, and documents.</span></span> <span data-ttu-id="83d01-105">Для этого добавьте объекты [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойство [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который определяет post.</span><span class="sxs-lookup"><span data-stu-id="83d01-105">To do this, you add  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) objects to the [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that defines the post.</span></span> <span data-ttu-id="83d01-106">Публикации о может содержать несколько ссылок.</span><span class="sxs-lookup"><span data-stu-id="83d01-106">Posts can contain multiple links.</span></span>
  
    
    


> <span data-ttu-id="83d01-107">**Примечание:** Чтобы добавить содержимое post внедренные изображения, видео или документы, добавьте объект [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) свойством [SocialPostCreationData.Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="83d01-107">**Note:** To add embedded pictures, videos, or documents to a post's content, you add a  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object to the [SocialPostCreationData.Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property.</span></span> <span data-ttu-id="83d01-108">Дополнительные сведения можно [как: Внедрение изображения, видео и документы в публикации в SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md).</span><span class="sxs-lookup"><span data-stu-id="83d01-108">For more information, see [How to: Embed images, videos, and documents in posts in SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md).</span></span> 
  
    
    


<span data-ttu-id="83d01-p103">API, описанных в этой статье  от клиентской объектной модели .NET. Тем не менее если вы используете другой API, такие как JavaScript объектной модели, имена объектов или соответствующий интерфейс API может отличаться. В разделе  [Дополнительные ресурсы](#bk_addresources) для ссылки на документацию для API, связанных с ними.</span><span class="sxs-lookup"><span data-stu-id="83d01-p103">The API described in this article is from the .NET client object model. However, if you're using another API, such as the JavaScript object model, the object names or corresponding API might be different. See  [Additional resources](#bk_addresources) for links to documentation for related APIs.</span></span>
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-links-to-a-post-in-sharepoint"></a><span data-ttu-id="83d01-112">Необходимые условия для использования примеров кода для добавления ссылок на публикацию в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-112">Prerequisites for using the code examples to add links to a post in SharePoint</span></span>
<span data-ttu-id="83d01-113"><a name="bk_preReqs"> </a></span><span class="sxs-lookup"><span data-stu-id="83d01-113"><a name="bk_preReqs"> </a></span></span>

<span data-ttu-id="83d01-p104">Примеры кода в этой статье показано, как добавлять ссылки на микроблога публикации. В этих примерах: от консольных приложений, использующих на следующие сборки SharePoint:</span><span class="sxs-lookup"><span data-stu-id="83d01-p104">The code examples in this article show how to add links to microblog posts. These examples are from console applications that use the following SharePoint assemblies:</span></span>
  
    
    

- <span data-ttu-id="83d01-116">Microsoft.SharePoint.Client</span><span class="sxs-lookup"><span data-stu-id="83d01-116">Microsoft.SharePoint.Client</span></span>
    
  
- <span data-ttu-id="83d01-117">Microsoft.SharePoint.Client.Runtime</span><span class="sxs-lookup"><span data-stu-id="83d01-117">Microsoft.SharePoint.Client.Runtime</span></span>
    
  
- <span data-ttu-id="83d01-118">Microsoft.SharePoint.Client.UserProfilies</span><span class="sxs-lookup"><span data-stu-id="83d01-118">Microsoft.SharePoint.Client.UserProfilies</span></span>
    
  
<span data-ttu-id="83d01-119">Инструкции о настройке среды разработки и создайте консольное приложение, см [как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span><span class="sxs-lookup"><span data-stu-id="83d01-119">For instructions about how to set up your development environment and create a console application, see  [How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span></span>
  
    
    

## <a name="example-include-links-to-websites-sharepoint-sites-and-documents-in-a-post-in-sharepoint"></a><span data-ttu-id="83d01-120">Пример: Включение ссылки на веб-сайты, сайты SharePoint и документов в записи в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-120">Example: Include links to websites, SharePoint sites, and documents in a post in SharePoint</span></span>
<span data-ttu-id="83d01-121"><a name="bkmk_addLinks"> </a></span><span class="sxs-lookup"><span data-stu-id="83d01-121"><a name="bkmk_addLinks"> </a></span></span>

<span data-ttu-id="83d01-p105">В следующем примере кода публикует сообщение, которое содержит ссылки на веб-сайт, сайт SharePoint и документа. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="83d01-p105">The following code example publishes a post that contains links to a website, a SharePoint site, and a document. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="83d01-p106">Создание  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) объектов, которые представляют ссылки. Каждый экземпляр задает поле [SocialDataItemType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.aspx) типа связи, отображаемый текст для ссылки и связи URI.</span><span class="sxs-lookup"><span data-stu-id="83d01-p106">Create  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) objects that represent the links. Each instance sets the [SocialDataItemType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.aspx) field for the link type, the display text for the link, and the link URI.</span></span>
    
  
- <span data-ttu-id="83d01-126">Добавьте заполнители текста post, чтобы указать, где должны отображаться отображаемый текст.</span><span class="sxs-lookup"><span data-stu-id="83d01-126">Add placeholders to the post text to indicate where the link's display text should appear.</span></span>
    
  
- <span data-ttu-id="83d01-127">Добавьте объекты ссылок свойство  [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.</span><span class="sxs-lookup"><span data-stu-id="83d01-127">Add the link objects to the  [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  

> <span data-ttu-id="83d01-128">**Примечание:** На данный момент SharePoint значками ссылки на веб-сайты, сайты SharePoint и документов, таким же образом, но рекомендуется, выберите тип [сайта](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Site.aspx) и типа [документа](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Document.aspx) для сайтов SharePoint и документов.</span><span class="sxs-lookup"><span data-stu-id="83d01-128">**Note:** Currently, SharePoint handles links to websites, SharePoint sites, and documents in the same way, but as a best practice, choose the  [Site](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Site.aspx) type and the [Document](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Document.aspx) type for SharePoint sites and documents.</span></span>
  
    
    

<span data-ttu-id="83d01-129">Социальные веб-канала щелкнув ссылку на веб-сайта, сайт SharePoint или документ откроется элемента в отдельном окне браузера.</span><span class="sxs-lookup"><span data-stu-id="83d01-129">In the social feed, clicking a link to a website, SharePoint site, or document opens the item in a separate browser window.</span></span>
  
    
    

> <span data-ttu-id="83d01-130">**Примечание:** Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="83d01-130">**Note:** Change the placeholder values for the URL variables before you run the code.</span></span> 
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace IncludeLinksInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string websiteLinkUrl = "http://bing.com";
            const string siteLinkUrl = "http://serverName/siteName/";
            const string docLinkUrl = "http://serverName/Shared%20Documents/docName.txt";

            // Define the link to a website that you want to include in the post.
            SocialDataItem websiteLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Link,
                Text = "link to a website",
                Uri = websiteLinkUrl
            };

            // Define the link to a SharePoint site that you want to include in the post.
            SocialDataItem siteLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Site,
                Text = "link to a SharePoint site",
                Uri = siteLinkUrl
            };

            // Define the link to a document that you want to include in the post.
            SocialDataItem docLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Document,
                Text = "link to a document",
                Uri = docLinkUrl
            };

            // Add the links to the post's creation data.
            // Put placeholders ({n}) where you want the links to appear in the post text,
            // and then add the links to the post's content items.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "Check out this {0}, {1}, and {2}.";
            postCreationData.ContentItems = new SocialDataItem[3] { 
                    websiteLink, 
                    siteLink, 
                    docLink 
                };
            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Publish the post. This is a root post to the user's feed, so specify
                // null for the targetId parameter.
                feedManager.CreatePost(null, postCreationData);
                clientContext.ExecuteQuery();
                Console.Write("The post was published.");
                Console.ReadLine();
            }
            catch (Exception ex)
            {
                Console.Write("Error publishing the post: " + ex.Message);
                Console.ReadLine();
            }
        }
    }
}

```


## <a name="example-mention-someone-in-a-post-in-sharepoint"></a><span data-ttu-id="83d01-131">Пример: Укажите, кто-то в записи в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-131">Example: Mention someone in a post in SharePoint</span></span>
<span data-ttu-id="83d01-132"><a name="bkmk_addMention"> </a></span><span class="sxs-lookup"><span data-stu-id="83d01-132"><a name="bkmk_addMention"> </a></span></span>

<span data-ttu-id="83d01-p107">В следующем примере кода публикует post, в котором упомянут пользователь. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="83d01-p107">The following code example publishes a post that mentions a user. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="83d01-p108">Создайте объект  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) для представления упоминания, который является ссылка на пользователя. [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) указывает поле [SocialDataItemType.User](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.User.aspx) и имя учетной записи упомянутый человека. Имя учетной записи можно задать с помощью для входа пользователя или адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="83d01-p108">Create a  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) object to represent a mention, which is a link to a user. The [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) specifies the [SocialDataItemType.User](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.User.aspx) field and the mentioned person's account name. You can set the account name by using either the person's login or email address.</span></span>
    
  
- <span data-ttu-id="83d01-138">Добавьте заполнитель текста post, чтобы указать, которой должен отображаться отображаемое имя упомянутый контакта.</span><span class="sxs-lookup"><span data-stu-id="83d01-138">Add a placeholder to the post text to indicate where the mentioned person's display name should appear.</span></span>
    
  
- <span data-ttu-id="83d01-139">Добавьте  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойство [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.</span><span class="sxs-lookup"><span data-stu-id="83d01-139">Add the  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) to the [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="83d01-140">Социальные веб-канала нажав кнопку упоминание перенаправляет страницы упомянутый пользователя **о**.</span><span class="sxs-lookup"><span data-stu-id="83d01-140">In the social feed, clicking a mention redirects to the mentioned person's **About** page.</span></span>
  
    
    

> <span data-ttu-id="83d01-141">**Примечание:** Изменение значений заполнитель для переменных **serverURL** и **имя учетной записи** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="83d01-141">**Note:** Change the placeholder values for the **serverURL** and **accountName** variables before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace IncludeMentionInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string accountName = @"domain\\name or email address";

            // Define the mention link that you want to include in the post.
            SocialDataItem userMentionLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.User,
                AccountName = accountName
            };

            // Add the mention to the post's creation data.
            // Put a placeholder ({0}) where you want the mention to appear in the post text,
            // and then add the mention to the post's content items.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "{0} does great work!";
            postCreationData.ContentItems = new SocialDataItem[1] { userMentionLink, };

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Publish the post. This is a root post to the user's feed, so specify
                // null for the targetId parameter.
                feedManager.CreatePost(null, postCreationData);
                clientContext.ExecuteQuery();
                Console.Write("The post was published.");
                Console.ReadLine();
            }
            catch (Exception ex)
            {
                Console.Write("Error publishing the post: " + ex.Message);
                Console.ReadLine();
            }
        }
    }
}

```


## <a name="example-include-a-tag-in-a-post-in-sharepoint"></a><span data-ttu-id="83d01-142">Пример: Включение тега в записи в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-142">Example: Include a tag in a post in SharePoint</span></span>
<span data-ttu-id="83d01-143"><a name="bkmk_addTag"> </a></span><span class="sxs-lookup"><span data-stu-id="83d01-143"><a name="bkmk_addTag"> </a></span></span>

<span data-ttu-id="83d01-p109">В следующем примере кода публикует сообщение, которое содержит тег. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="83d01-p109">The following code example publishes a post that includes a tag. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="83d01-p110">Создайте объект  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) для представления тега. [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) указывает поле [SocialDataItemType.Tag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Tag.aspx) и имя тега, который должен содержать **#** символов.</span><span class="sxs-lookup"><span data-stu-id="83d01-p110">Create a  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) object to represent the tag. The [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) specifies the [SocialDataItemType.Tag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Tag.aspx) field and the tag name, which must include a **#** character.</span></span>
    
  
- <span data-ttu-id="83d01-148">Добавьте заполнитель текста post, чтобы указать, где должны отображаться тега.</span><span class="sxs-lookup"><span data-stu-id="83d01-148">Add a placeholder to the post text to indicate where the tag should appear.</span></span>
    
  
- <span data-ttu-id="83d01-149">Добавьте  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойство [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.</span><span class="sxs-lookup"><span data-stu-id="83d01-149">Add the  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) to the [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="83d01-p111">Социальные веб-канала нажав кнопку тега будет перенаправлять тег **о** страницу. Если тег еще не существует, сервер создает его.</span><span class="sxs-lookup"><span data-stu-id="83d01-p111">In the social feed, clicking a tag redirects to the tag's **About** page. If the tag doesn't already exist, the server creates it.</span></span>
  
    
    

> <span data-ttu-id="83d01-152">**Примечание:** Изменение значений заполнитель для переменных **serverURL** и **tagName** , прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="83d01-152">**Note:** Change the placeholder values for the **serverURL** and **tagName** variables before you run the code.</span></span>
  
    
    




```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace IncludeTagInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string tagName = "#" + "tagName";

            // Define the link to a tag that you want to include in the post. If the tag is new, the
            // server adds it to the tags collection.
            SocialDataItem tagLink = new SocialDataItem
            {
                ItemType = SocialDataItemType.Tag,
                Text = tagName
            };

            // Add the tag to the post's creation data.
            // Put a placeholder ({0}) where you want the tag to appear in the post text,
            // and then add the tag to the post's content items.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "I like {0}.";
            postCreationData.ContentItems = new SocialDataItem[1] { tagLink };

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Publish the post. This is a root post to the user's feed, so specify
                // null for the targetId parameter.
                feedManager.CreatePost(null, postCreationData);
                clientContext.ExecuteQuery();
                Console.Write("The post was published.");
                Console.ReadLine();
            }
            catch (Exception ex)
            {
                Console.Write("Error publishing the post: " + ex.Message);
                Console.ReadLine();
            }
        }
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="83d01-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="83d01-153">Additional resources</span></span>
<span data-ttu-id="83d01-154"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="83d01-154"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="83d01-155">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-155">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  <span data-ttu-id="83d01-156">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) и [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) в клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="83d01-156">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) and [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) in the client object models</span></span>
    
  
-  <span data-ttu-id="83d01-157">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) и [SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx) в объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="83d01-157">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) and [SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx) in the JavaScript object model</span></span>
    
  
-  [<span data-ttu-id="83d01-158">Social feed REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="83d01-158">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  <span data-ttu-id="83d01-159">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) и [SPSocialDataItem](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialDataItem.aspx) в серверной объектной модели</span><span class="sxs-lookup"><span data-stu-id="83d01-159">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) and [SPSocialDataItem](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialDataItem.aspx) in the server object model</span></span>
    
  

