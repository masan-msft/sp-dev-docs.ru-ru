---
title: "Внедрение изображения, видео и документы в публикации в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 9927b9e7-daea-4261-80fa-4cc25f489e22
ms.openlocfilehash: f253398d85d12fc53ce85130fef66c632f22b588
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="embed-images-videos-and-documents-in-posts-in-sharepoint"></a>Внедрение изображения, видео и документы в публикации в SharePoint

Узнайте, как добавлять в записи микроблога объекты [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx), которые отображаются в каналах SharePoint в виде внедренных рисунков, видеозаписей и документов.
В это социальные веб-канал простейшей формой post контента содержит только текст, но также можно добавить внедренные изображения, видео и документы. Для этого воспользуйтесь свойством [вложений](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) в объекте [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , определяющий post. Публикации о может содержать одно вложение, что представленный объектом [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) .
  
> [!NOTE]
> Добавление упоминаются, тег или ссылка для записи контента, добавьте объект [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойством [SocialPostCreationData.ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) . Дополнительные сведения можно [как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md). 
  
    
    


API, описанных в этой статье  от клиентской объектной модели .NET. Если вы используете другой API, такие как JavaScript объектной модели, имена объектов или соответствующий интерфейс API может отличаться. В разделе  [Дополнительные ресурсы](#bk_addresources) для ссылки на документацию для API, связанных с ними.
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-attachments-to-a-post"></a>Необходимые условия для использования примеров кода для добавления вложений на публикацию
<a name="bk_preReqs"> </a>

Примеры кода в этой статье демонстрируется добавление изображения, видео и отправляет документ вложения на микроблога. В этих примерах: от консольного приложения, использующего следующие сборки SharePoint:
  
    
    

- Microsoft.SharePoint.Client
    
  
- Microsoft.SharePoint.Client.Runtime
    
  
- Microsoft.SharePoint.Client.UserProfilies
    
  
Для использования примеров, описанных в этой статье, необходимо загрузить изображение, видео и документа. Для использования примеров видео на сервере должна быть включена возможность видео и видео файлов должны храниться в библиотеки активов. Чтобы использовать пример документов в локальной среде, Office Online необходимо настроить в среде. Дополнительные сведения см в [планировании библиотеки цифровых активов в SharePoint](http://technet.microsoft.com/en-us/library/ee414275.aspx) и [Настроить SharePoint для использования Office Online](http://technet.microsoft.com/en-us/library/ff431687.aspx).
  
    
    
Инструкции о настройке среды разработки и создайте консольное приложение, см [как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).
  
    
    

## <a name="example-embed-an-image-in-a-post-in-sharepoint"></a>Пример: Внедрите изображение в записи в SharePoint
<a name="bkmk_addImage"> </a>

В следующем примере кода публикует сообщение, содержащее встроенное изображение. В нем показано, как:
  
    
    

- Создайте объект  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) , который представляет изображение. [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) указывает поле [SocialAttachmentKind.Image](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachmentKind.Image.aspx) и URI файла изображения.
    
  
- Добавьте объект изображение свойству  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.
    
  
Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.
  
    
    



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


## <a name="embed-a-video-in-a-post-in-sharepoint"></a>Внедрение видео в записи в SharePoint
<a name="bkmk_addVideo"> </a>

В следующем примере кода публикует сообщение, содержащее внедренным видео. В нем показано, как:
  
    
    

- Получите объект  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) , который представляет видео вложений с помощью метода [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) .
    
  
- Добавление видео вложения в свойство  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.
    
  
В этом примере требуется функции видео, чтобы включить на сервер и файл видео, чтобы передать на библиотеки активов.  [Необходимые условия для использования примеров кода](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) для получения дополнительных сведений см.
  
    
    
Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.
  
    
    



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


## <a name="example-embed-a-document-in-a-post-in-sharepoint"></a>Пример: Внедрение документов в записи в SharePoint
<a name="bkmk_addDoc"> </a>

В следующем примере кода публикует сообщение, содержащее внедренным документом. В нем показано, как:
  
    
    

- Получите объект  [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) , который представляет вложение документов с помощью метода [SocialFeedManager.GetPreview](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialFeedManager.GetPreview.aspx) .
    
  
- Добавьте вложение документа в свойство  [Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.
    
  
Для использования в этом примере в локальной среде, необходимо настроить среду для использования Office Online. [Необходимые условия для использования примеров кода](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md#bk_preReqs) для получения дополнительных сведений см. В противном случае вы можете разместить ссылку на документ, как описано в статье [как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md).
  
    
    
Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код.
  
    
    



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


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [Как добавлять в записи упоминания, теги и ссылки на сайты и документы в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)
    
  
-  [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) и [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) в клиентской объектной модели
    
  
-  [SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) и [SocialAttachment](http://msdn.microsoft.com/library/dfdee790-a1b0-19c8-0e92-5a6e058ba4db%28Office.15%29.aspx) в объектной модели JavaScript
    
  
-  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) и [SPSocialAttachment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialAttachment.aspx) в серверной объектной модели
    
  

