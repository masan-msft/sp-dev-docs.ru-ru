---
title: "Внедрение изображения, видео и документы в публикации в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 9927b9e7-daea-4261-80fa-4cc25f489e22
ms.openlocfilehash: f06a936839773e58837042fea884082aaeabe36e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="embed-images-videos-and-documents-in-posts-in-sharepoint"></a><span data-ttu-id="0adad-102">Внедрение изображения, видео и документы в публикации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-102">Embed images, videos, and documents in posts in SharePoint</span></span>

<span data-ttu-id="0adad-103">Узнайте, как добавлять в записи микроблога объекты [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx), которые отображаются в каналах SharePoint в виде внедренных рисунков, видеозаписей и документов.</span><span class="sxs-lookup"><span data-stu-id="0adad-103">Learn how to add  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) objects to microblog posts, which render as embedded pictures, videos, and documents in SharePoint social feeds.</span></span>
<span data-ttu-id="0adad-104">В это социальные веб-канал простейшей формой post контента содержит только текст, но также можно добавить внедренные изображения, видео и документы.</span><span class="sxs-lookup"><span data-stu-id="0adad-104">In a social feed, the simplest form of post content contains only text, but you can also add embedded pictures, videos, and documents.</span></span> <span data-ttu-id="0adad-105">Для этого воспользуйтесь свойством [вложений](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) в объекте [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , определяющий post.</span><span class="sxs-lookup"><span data-stu-id="0adad-105">To do this, you use the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property on the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that defines the post.</span></span> <span data-ttu-id="0adad-106">Публикации о может содержать одно вложение, что представленный объектом [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0adad-106">Posts can contain one attachment, which is represented by a [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object.</span></span>
  
    
    


> <span data-ttu-id="0adad-107">**Примечание:** Добавление упоминаются, тег или ссылка для записи контента, добавьте объект [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойством [SocialPostCreationData.ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0adad-107">**Note:** To add a mention, tag, or link to a post's content, you add a  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) object to the [SocialPostCreationData.ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) property.</span></span> <span data-ttu-id="0adad-108">Дополнительные сведения можно [как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).</span><span class="sxs-lookup"><span data-stu-id="0adad-108">For more information, see [How to: Include mentions, tags, and links to sites and documents in posts in SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).</span></span> 
  
    
    


<span data-ttu-id="0adad-p103">API, описанных в этой статье  от клиентской объектной модели .NET. Если вы используете другой API, такие как JavaScript объектной модели, имена объектов или соответствующий интерфейс API может отличаться. В разделе  [Дополнительные ресурсы](#bk_addresources) для ссылки на документацию для API, связанных с ними.</span><span class="sxs-lookup"><span data-stu-id="0adad-p103">The API described in this article is from the .NET client object model. If you're using another API, such as the JavaScript object model, the object names or corresponding API might be different. See  [Additional resources](#bk_addresources) for links to documentation for related APIs.</span></span>
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-attachments-to-a-post"></a><span data-ttu-id="0adad-112">Необходимые условия для использования примеров кода для добавления вложений на публикацию</span><span class="sxs-lookup"><span data-stu-id="0adad-112">Prerequisites for using the code examples to add attachments to a post</span></span>
<span data-ttu-id="0adad-113"><a name="bk_preReqs"> </a></span><span class="sxs-lookup"><span data-stu-id="0adad-113"></span></span>

<span data-ttu-id="0adad-p104">Примеры кода в этой статье демонстрируется добавление изображения, видео и отправляет документ вложения на микроблога. В этих примерах: от консольного приложения, использующего следующие сборки SharePoint:</span><span class="sxs-lookup"><span data-stu-id="0adad-p104">The code examples in this article show how to add image, video, and document attachments to microblog posts. These examples are from a console application that uses the following SharePoint assemblies:</span></span>
  
    
    

- <span data-ttu-id="0adad-116">Microsoft.SharePoint.Client</span><span class="sxs-lookup"><span data-stu-id="0adad-116">Microsoft.SharePoint.Client</span></span>
    
  
- <span data-ttu-id="0adad-117">Microsoft.SharePoint.Client.Runtime</span><span class="sxs-lookup"><span data-stu-id="0adad-117">Microsoft.SharePoint.Client.Runtime</span></span>
    
  
- <span data-ttu-id="0adad-118">Microsoft.SharePoint.Client.UserProfilies</span><span class="sxs-lookup"><span data-stu-id="0adad-118">Microsoft.SharePoint.Client.UserProfilies</span></span>
    
  
<span data-ttu-id="0adad-119">Для использования примеров, описанных в этой статье, необходимо загрузить изображение, видео и документа.</span><span class="sxs-lookup"><span data-stu-id="0adad-119">To use the examples in this article, you'll need to upload an image, a video, and a document.</span></span> <span data-ttu-id="0adad-120">Для использования примеров видео на сервере должна быть включена возможность видео и видео файлов должны храниться в библиотеки активов.</span><span class="sxs-lookup"><span data-stu-id="0adad-120">To use the video example, the video feature must be enabled on the server and the video file must be stored in an asset library.</span></span> <span data-ttu-id="0adad-121">Чтобы использовать пример документов в локальной среде, Office Online необходимо настроить в среде.</span><span class="sxs-lookup"><span data-stu-id="0adad-121">To use the document example in an on-premises environment, Office Online must be configured in the environment.</span></span> <span data-ttu-id="0adad-122">Дополнительные сведения см в [планировании библиотеки цифровых активов в SharePoint](http://technet.microsoft.com/en-us/library/ee414275.aspx) и [Настроить SharePoint для использования Office Online](http://technet.microsoft.com/en-us/library/ff431687.aspx).</span><span class="sxs-lookup"><span data-stu-id="0adad-122">For more information, see  [Plan digital asset libraries in SharePoint](http://technet.microsoft.com/en-us/library/ee414275.aspx) and [Configure SharePoint to use Office Online](http://technet.microsoft.com/en-us/library/ff431687.aspx).</span></span>
  
    
    
<span data-ttu-id="0adad-123">Инструкции о настройке среды разработки и создайте консольное приложение, см [как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0adad-123">For instructions about how to set up your development environment and create a console application, see  [How to: Create and delete posts and retrieve the social feed by using the .NET client object model in SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).</span></span>
  
    
    

## <a name="example-embed-an-image-in-a-post-in-sharepoint"></a><span data-ttu-id="0adad-124">Пример: Внедрите изображение в записи в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-124">Example: Embed an image in a post in SharePoint</span></span>
<span data-ttu-id="0adad-125"><a name="bkmk_addImage"> </a></span><span class="sxs-lookup"><span data-stu-id="0adad-125"></span></span>

<span data-ttu-id="0adad-p106">В следующем примере кода публикует сообщение, содержащее встроенное изображение. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="0adad-p106">The following code example publishes a post that contains an embedded image. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="0adad-p107">Создайте объект  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) , который представляет изображение. [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) указывает поле [SocialAttachmentKind.Image](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachmentKind.Image.aspx) и URI файла изображения.</span><span class="sxs-lookup"><span data-stu-id="0adad-p107">Create a  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object that represents the image. The [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) specifies the [SocialAttachmentKind.Image](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachmentKind.Image.aspx) field and the URI of the image file.</span></span>
    
  
- <span data-ttu-id="0adad-130">Добавьте объект изображение свойству  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.</span><span class="sxs-lookup"><span data-stu-id="0adad-130">Add the image object to the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="0adad-131">Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="0adad-131">Change the placeholder values for the URL variables before you run the code.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace EmbedImageInPost
{
    class Program
    {
        static void Main(string[] args)
        {

            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string imageUrl = "http://serverName/Shared%20Documents/imageName.jpg";

            // Define the image attachment that you want to embed in the post.
            SocialAttachment attachment = new SocialAttachment()
            {
                AttachmentKind = SocialAttachmentKind.Image,
                Uri = imageUrl
            };

            // Define properties for the post and add the attachment.
            SocialPostCreationData postCreationData = new SocialPostCreationData();
            postCreationData.ContentText = "Look at this!";
            postCreationData.Attachment = attachment;

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


## <a name="embed-a-video-in-a-post-in-sharepoint"></a><span data-ttu-id="0adad-132">Внедрение видео в записи в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-132">Embed a video in a post in SharePoint</span></span>
<span data-ttu-id="0adad-133"><a name="bkmk_addVideo"> </a></span><span class="sxs-lookup"><span data-stu-id="0adad-133"></span></span>

<span data-ttu-id="0adad-p108">В следующем примере кода публикует сообщение, содержащее внедренным видео. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="0adad-p108">The following code example publishes a post that contains an embedded video. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="0adad-136">Получите объект  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) , который представляет видео вложений с помощью метода [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0adad-136">Get the  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object that represents the video attachment by using the [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) method.</span></span>
    
  
- <span data-ttu-id="0adad-137">Добавление видео вложения в свойство  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.</span><span class="sxs-lookup"><span data-stu-id="0adad-137">Add the video attachment to the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="0adad-p109">В этом примере требуется функции видео, чтобы включить на сервер и файл видео, чтобы передать на библиотеки активов.  [Необходимые условия для использования примеров кода](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) для получения дополнительных сведений см.</span><span class="sxs-lookup"><span data-stu-id="0adad-p109">This example requires the video features to be enabled on the server and the video file to be uploaded to an asset library. See the  [prerequisites for using the code examples](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) for more information.</span></span>
  
    
    
<span data-ttu-id="0adad-140">Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="0adad-140">Change the placeholder values for the URL variables before you run the code.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace EmbedVideoInPost
{
    class Program
    {
        static void Main(string[] args)
        {
            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName/siteName/";
            const string videoUrl = "http://serverName/Asset%20Library/fileName?Web=1";

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Get the video attachment from the server.
                ClientResult<SocialAttachment> attachment = feedManager.GetPreview(videoUrl);
                clientContext.ExecuteQuery();

                // Define properties for the post and add the attachment.
                SocialPostCreationData postCreationData = new SocialPostCreationData();
                postCreationData.ContentText = "Look at this!";
                postCreationData.Attachment = attachment.Value;

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


## <a name="example-embed-a-document-in-a-post-in-sharepoint"></a><span data-ttu-id="0adad-141">Пример: Внедрение документов в записи в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-141">Example: Embed a document in a post in SharePoint</span></span>
<span data-ttu-id="0adad-142"><a name="bkmk_addDoc"> </a></span><span class="sxs-lookup"><span data-stu-id="0adad-142"></span></span>

<span data-ttu-id="0adad-p110">В следующем примере кода публикует сообщение, содержащее внедренным документом. В нем показано, как:</span><span class="sxs-lookup"><span data-stu-id="0adad-p110">The following code example publishes a post that contains an embedded document. It shows how to:</span></span>
  
    
    

- <span data-ttu-id="0adad-145">Получите объект  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) , который представляет вложение документов с помощью метода [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) .</span><span class="sxs-lookup"><span data-stu-id="0adad-145">Get the  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) object that represents the document attachment by using the [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) method.</span></span>
    
  
- <span data-ttu-id="0adad-146">Добавьте вложение документа в свойство  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.</span><span class="sxs-lookup"><span data-stu-id="0adad-146">Add the document attachment to the  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) property of the [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) object that's used to create the post.</span></span>
    
  
<span data-ttu-id="0adad-147">Для использования в этом примере в локальной среде, необходимо настроить среду для использования Office Online.</span><span class="sxs-lookup"><span data-stu-id="0adad-147">To use this example in an on-premises environment, your environment must be configured to use Office Online.</span></span> <span data-ttu-id="0adad-148">[Необходимые условия для использования примеров кода](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) для получения дополнительных сведений см.</span><span class="sxs-lookup"><span data-stu-id="0adad-148">See the  [prerequisites for using the code examples](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) for more information.</span></span> <span data-ttu-id="0adad-149">В противном случае вы можете разместить ссылку на документ, как описано в статье [как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).</span><span class="sxs-lookup"><span data-stu-id="0adad-149">Otherwise, you can post a link to the document as described in [How to: Include mentions, tags, and links to sites and documents in posts in SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).</span></span>
  
    
    
<span data-ttu-id="0adad-150">Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.</span><span class="sxs-lookup"><span data-stu-id="0adad-150">Change the placeholder values for the URL variables before you run the code.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.Social;

namespace EmbedDocumentInPost
{
    class Program
    {
        static void Main(string[] args)
        {
            // Replace the following placeholder values with the actual values.
            const string serverUrl = "http://serverName";
            const string documentUrl = "http://serverName/Shared%20Documents/fileName.docx";

            try
            {

                // Get the context and the SocialFeedManager instance.
                ClientContext clientContext = new ClientContext(serverUrl);
                SocialFeedManager feedManager = new SocialFeedManager(clientContext);

                // Get the document attachment from the server.
                ClientResult<SocialAttachment> attachment = feedManager.GetPreview(documentUrl);
                clientContext.ExecuteQuery();

                // Define properties for the post and add the attachment.
                SocialPostCreationData postCreationData = new SocialPostCreationData();
                postCreationData.ContentText = "Post with a document.";
                postCreationData.Attachment = attachment.Value;

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


## <a name="additional-resources"></a><span data-ttu-id="0adad-151">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0adad-151">Additional resources</span></span>
<span data-ttu-id="0adad-152"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0adad-152"></span></span>


-  [<span data-ttu-id="0adad-153">Работа с социальными веб-каналами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-153">Work with social feeds in SharePoint</span></span>](work-with-social-feeds-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0adad-154">Как добавлять в записи упоминания, теги и ссылки на сайты и документы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-154">How to: Include mentions, tags, and links to sites and documents in posts in SharePoint</span></span>](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
    
  
-  <span data-ttu-id="0adad-155">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) и [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) в клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="0adad-155">[SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) and [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) in the client object models</span></span>
    
  
-  <span data-ttu-id="0adad-156">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) и [SocialAttachment](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx) в объектной модели JavaScript</span><span class="sxs-lookup"><span data-stu-id="0adad-156">[SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) and [SocialAttachment](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx) in the JavaScript object model</span></span>
    
  
-  [<span data-ttu-id="0adad-157">Social feed REST API reference for SharePoint</span><span class="sxs-lookup"><span data-stu-id="0adad-157">Social feed REST API reference for SharePoint</span></span>](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  <span data-ttu-id="0adad-158">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) и [SPSocialAttachment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialAttachment.aspx) в серверной объектной модели</span><span class="sxs-lookup"><span data-stu-id="0adad-158">[SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) and [SPSocialAttachment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialAttachment.aspx) in the server object model</span></span>
    
  
