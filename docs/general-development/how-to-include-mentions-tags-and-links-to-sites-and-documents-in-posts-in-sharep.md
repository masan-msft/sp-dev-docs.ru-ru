---
title: "Как включить упоминания, теги и ссылки на сайты и документы в публикации в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 975da333-372b-4bf6-a3f4-7452db369f04
ms.openlocfilehash: 3ca0f7365a2000525cef8492ff685ac3a514a86f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharepoint"></a>Как: Включение упоминания, теги и ссылки на сайты и документы в публикации в SharePoint
Узнайте, как добавлять объекты [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) микроблога публикации, которые отображаются в виде упоминания, теги и ссылки на веб-каналов социальных SharePoint.
В социальных веб-канал простейшей формой post контента содержит только текст, но также можно добавлять ссылки, которые отображаются в виде упоминания теги и ссылки на веб-сайты, сайты SharePoint и документы. Для этого добавьте объекты [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойство [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который определяет post. Публикации о может содержать несколько ссылок.
  
    
    


> **Примечание:** Чтобы добавить содержимое post внедренные изображения, видео или документы, добавьте объект [SocialAttachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialAttachment.aspx) свойством [SocialPostCreationData.Attachment](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.Attachment.aspx) . Дополнительные сведения можно [как: Внедрение изображения, видео и документы в публикации в SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md). 
  
    
    


API, описанных в этой статье  от клиентской объектной модели .NET. Тем не менее если вы используете другой API, такие как JavaScript объектной модели, имена объектов или соответствующий интерфейс API может отличаться. В разделе  [Дополнительные ресурсы](#bk_addresources) для ссылки на документацию для API, связанных с ними.
  
    
    


## <a name="prerequisites-for-using-the-code-examples-to-add-links-to-a-post-in-sharepoint"></a>Необходимые условия для использования примеров кода для добавления ссылок на публикацию в SharePoint
<a name="bk_preReqs"> </a>

Примеры кода в этой статье показано, как добавлять ссылки на микроблога публикации. В этих примерах: от консольных приложений, использующих на следующие сборки SharePoint:
  
    
    

- Microsoft.SharePoint.Client
    
  
- Microsoft.SharePoint.Client.Runtime
    
  
- Microsoft.SharePoint.Client.UserProfilies
    
  
Инструкции о настройке среды разработки и создайте консольное приложение, см [как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md).
  
    
    

## <a name="example-include-links-to-websites-sharepoint-sites-and-documents-in-a-post-in-sharepoint"></a>Пример: Включение ссылки на веб-сайты, сайты SharePoint и документов в записи в SharePoint
<a name="bkmk_addLinks"> </a>

В следующем примере кода публикует сообщение, которое содержит ссылки на веб-сайт, сайт SharePoint и документа. В нем показано, как:
  
    
    

- Создание  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) объектов, которые представляют ссылки. Каждый экземпляр задает поле [SocialDataItemType](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.aspx) типа связи, отображаемый текст для ссылки и связи URI.
    
  
- Добавьте заполнители текста post, чтобы указать, где должны отображаться отображаемый текст.
    
  
- Добавьте объекты ссылок свойство  [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.
    
  

> **Примечание:** На данный момент SharePoint значками ссылки на веб-сайты, сайты SharePoint и документов, таким же образом, но рекомендуется, выберите тип [сайта](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Site.aspx) и типа [документа](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Document.aspx) для сайтов SharePoint и документов.
  
    
    

Социальные веб-канала щелкнув ссылку на веб-сайта, сайт SharePoint или документ откроется элемента в отдельном окне браузера.
  
    
    

> **Примечание:** Изменение значений заполнитель для переменных URL-адрес, прежде чем запускать код. 
  
    
    




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


## <a name="example-mention-someone-in-a-post-in-sharepoint"></a>Пример: Укажите, кто-то в записи в SharePoint
<a name="bkmk_addMention"> </a>

В следующем примере кода публикует post, в котором упомянут пользователь. В нем показано, как:
  
    
    

- Создайте объект  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) для представления упоминания, который является ссылка на пользователя. [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) указывает поле [SocialDataItemType.User](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.User.aspx) и имя учетной записи упомянутый человека. Имя учетной записи можно задать с помощью для входа пользователя или адрес электронной почты.
    
  
- Добавьте заполнитель текста post, чтобы указать, которой должен отображаться отображаемое имя упомянутый контакта.
    
  
- Добавьте  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойство [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.
    
  
Социальные веб-канала нажав кнопку упоминание перенаправляет страницы упомянутый пользователя **о**.
  
    
    

> **Примечание:** Изменение значений заполнитель для переменных **serverURL** и **имя учетной записи** , прежде чем запускать код.
  
    
    




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


## <a name="example-include-a-tag-in-a-post-in-sharepoint"></a>Пример: Включение тега в записи в SharePoint
<a name="bkmk_addTag"> </a>

В следующем примере кода публикует сообщение, которое содержит тег. В нем показано, как:
  
    
    

- Создайте объект  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) для представления тега. [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) указывает поле [SocialDataItemType.Tag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItemType.Tag.aspx) и имя тега, который должен содержать **#** символов.
    
  
- Добавьте заполнитель текста post, чтобы указать, где должны отображаться тега.
    
  
- Добавьте  [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) свойство [ContentItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.ContentItems.aspx) объекта [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) , который используется для создания post.
    
  
Социальные веб-канала нажав кнопку тега будет перенаправлять тег **о** страницу. Если тег еще не существует, сервер создает его.
  
    
    

> **Примечание:** Изменение значений заполнитель для переменных **serverURL** и **tagName** , прежде чем запускать код.
  
    
    




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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [SocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialPostCreationData.aspx) и [SocialDataItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.SocialDataItem.aspx) в клиентской объектной модели
    
  
-  [SocialPostCreationData](http://msdn.microsoft.com/library/f0e1fa3e-6fc9-48e0-5570-92091abfef33%28Office.15%29.aspx) и [SocialDataItem](http://msdn.microsoft.com/library/757e7b62-66a6-b03f-0ff0-769a42eb2b4a%28Office.15%29.aspx) в объектной модели JavaScript
    
  
-  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [SPSocialPostCreationData](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialPostCreationData.aspx) и [SPSocialDataItem](https://msdn.microsoft.com/library/Microsoft.Office.Server.Social.SPSocialDataItem.aspx) в серверной объектной модели
    
  

