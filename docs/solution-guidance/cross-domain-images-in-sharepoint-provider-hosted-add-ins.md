---
title: "Изображения между доменами в SharePoint размещение у поставщика в надстройках"
ms.date: 11/03/2017
ms.openlocfilehash: 3260b534a87fbb097fdaa5910a1c41f276514733
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="cross-domain-images-in-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="1e112-102">Изображения между доменами в SharePoint размещение у поставщика в надстройках</span><span class="sxs-lookup"><span data-stu-id="1e112-102">Cross-domain images in SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="1e112-103">Использование изображения между доменами в размещенном у поставщика надстроек.</span><span class="sxs-lookup"><span data-stu-id="1e112-103">Use images across domains in provider-hosted add-ins.</span></span>

<span data-ttu-id="1e112-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="1e112-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="1e112-105">Может потребоваться отображения изображений на сайте SharePoint в размещенном у поставщика надстройки. Поскольку у поставщика надстроек выполняются на удаленной веб-, отличаются доменов для надстройки размещением у поставщика и сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1e112-105">You might want to display images from a SharePoint site in your provider-hosted add-ins. Because provider-hosted add-ins run on a remote web, the domains for your provider-hosted add-in and your SharePoint site are different.</span></span> <span data-ttu-id="1e112-106">Например надстройки могут выполняться в Microsoft Azure и вы пытаетесь Показывать изображение из Office 365.</span><span class="sxs-lookup"><span data-stu-id="1e112-106">For example, your add-in might run on Microsoft Azure, and you're trying to show an image from Office 365.</span></span> <span data-ttu-id="1e112-107">Так как размещение у поставщика в надстройке пересечение доменов для доступа к изображения, SharePoint требуется проверка подлинности пользователя перед надстройки размещением у поставщика показывает изображения.</span><span class="sxs-lookup"><span data-stu-id="1e112-107">Because your provider-hosted add-in crosses domains to access the image, SharePoint requires user authorization before the provider-hosted add-in shows the image.</span></span>

<span data-ttu-id="1e112-108">Пример кода [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) показано, как размещение у поставщика в надстройке можно использовать маркер доступа SharePoint и службы REST для получения изображений из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1e112-108">The [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) code sample shows how a provider-hosted add-in can use a SharePoint access token and a REST service to retrieve images from SharePoint.</span></span> <span data-ttu-id="1e112-109">Службы REST возвращается в кодировке Base64 строку, которая используется для отображения изображения в браузере.</span><span class="sxs-lookup"><span data-stu-id="1e112-109">The REST service returns a Base64-encoded string, which is used to show the image in the browser.</span></span> <span data-ttu-id="1e112-110">Использование решения в этом примере для отображения изображений, хранящихся в SharePoint в размещенном у поставщика надстроек с помощью кода на сервере или на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="1e112-110">Use the solution in this sample to show images stored in SharePoint in provider-hosted add-ins by using either server-side or client-side code.</span></span>

<span data-ttu-id="1e112-111">**Примечание:** Так как он использует конечных точек REST, можно использовать на сервере или клиентский код для извлечения изображения.</span><span class="sxs-lookup"><span data-stu-id="1e112-111">**Note:** Because the sample uses a REST endpoint, you can use either server-side or client-side code to retrieve your image.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e112-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1e112-112">Before you begin</span></span>

<span data-ttu-id="1e112-113">Чтобы начать работу, загрузите пример надстройки [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="1e112-113">To get started, download the [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-corecrossdomainimages-code-sample"></a><span data-ttu-id="1e112-114">Использование примера кода Core.CrossDomainImages</span><span class="sxs-lookup"><span data-stu-id="1e112-114">Using the Core.CrossDomainImages code sample</span></span>

<span data-ttu-id="1e112-115">При запуске в этом примере Default.aspx пытается загрузить следующее:</span><span class="sxs-lookup"><span data-stu-id="1e112-115">When you run this sample, Default.aspx tries to load the following:</span></span>

- <span data-ttu-id="1e112-116">Изображение 1, с помощью абсолютный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1e112-116">Image 1, by using the absolute URL.</span></span> 
    
- <span data-ttu-id="1e112-117">Изображение 2, с помощью вызова на сервере для конечных точек REST, который возвращает строку в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1e112-117">Image 2, by using a server-side call to a REST endpoint that returns a Base64-encoded string.</span></span>
    
- <span data-ttu-id="1e112-118">Изображение 3, с помощью вызова со стороны клиента для конечных точек REST, который возвращает строку в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1e112-118">Image 3, by using a client-side call to a REST endpoint that returns a Base64-encoded string.</span></span>
    
<span data-ttu-id="1e112-119">**Примечание:** Изображение 1 не выполняет обработку, так как надстройки пересечение доменов для получения изображения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1e112-119">**Note:** Image 1 does not render because the add-in crosses domains to get to the image in SharePoint.</span></span> <span data-ttu-id="1e112-120">Обратите внимание, что URL-адрес надстройки размещением у поставщика запускается на localhost.</span><span class="sxs-lookup"><span data-stu-id="1e112-120">Notice that the URL of the provider-hosted add-in runs on localhost.</span></span> <span data-ttu-id="1e112-121">Откройте контекстное меню (щелкните правой кнопкой мыши) для образа 1 и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="1e112-121">Open the shortcut menu (right-click) for Image 1, and then choose **Properties**.</span></span> <span data-ttu-id="1e112-122">Обратите внимание на то, что **(URL-адреса)** пытается получить изображение из надстройки веб-приложения не localhost.</span><span class="sxs-lookup"><span data-stu-id="1e112-122">Notice that the **Address (URL)** is trying to retrieve the image from the add-in web, not localhost.</span></span> <span data-ttu-id="1e112-123">Так как надстройка размещением у поставщика пересечение доменов для связи с веб-надстройки, чтобы получить доступ к изображения требуется проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="1e112-123">Because the provider-hosted add-in crosses domains to reach the add-in web, authentication is required in order to access the image.</span></span> <span data-ttu-id="1e112-124">Убедитесь, что доступ к изображение 1 URL-адрес напрямую, в отличие от вызова доменам в размещенном у поставщика надстройки, разрешается без ошибок, копирование и вставка **(URL-адреса)** в новом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="1e112-124">Verify that accessing Image 1's URL directly, as opposed to the cross-domain call in the provider-hosted add-in, resolves without an error by copying and pasting **Address (URL)** into a new browser window.</span></span> <span data-ttu-id="1e112-125">Обратите внимание, что изображение 1 отображается без ошибок.</span><span class="sxs-lookup"><span data-stu-id="1e112-125">Notice that Image 1 displays without an error.</span></span> <span data-ttu-id="1e112-126">Сравнение источника изображения 1 для источника изображения 2.</span><span class="sxs-lookup"><span data-stu-id="1e112-126">Compare the source of Image 1 to the source of Image 2.</span></span> <span data-ttu-id="1e112-127">Обратите внимание на то, что **Адрес (URL)** указывает строка в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1e112-127">Notice that the **Address (URL)** points to a Base64-encoded string.</span></span>

<span data-ttu-id="1e112-128">При загрузке Default.aspx **Page_Load** запускает и выполняет следующее:</span><span class="sxs-lookup"><span data-stu-id="1e112-128">When Default.aspx loads, **Page_Load** runs and does the following:</span></span>

1. <span data-ttu-id="1e112-129">Задает Image1.ImageUrl абсолютный путь к изображению.</span><span class="sxs-lookup"><span data-stu-id="1e112-129">Sets Image1.ImageUrl to the absolute path of the image.</span></span>
    
2. <span data-ttu-id="1e112-130">Создает экземпляр ImgService.</span><span class="sxs-lookup"><span data-stu-id="1e112-130">Instantiates ImgService.</span></span> <span data-ttu-id="1e112-131">ImgService — это конечная точка REST, на котором выполняется в том же домене, что надстройка размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="1e112-131">ImgService is a REST endpoint that runs in the same domain as the provider-hosted add-in.</span></span>
    
3. <span data-ttu-id="1e112-132">Задает строку в кодировке Base64, которое возвращает **ImgService.GetImage** Image2.ImageUrl.</span><span class="sxs-lookup"><span data-stu-id="1e112-132">Sets Image2.ImageUrl to the Base64-encoded string that **ImgService.GetImage** returns.</span></span> <span data-ttu-id="1e112-133">Маркер доступа, сайтов, папку и имя файла, передаются в качестве параметров **ImgService.GetImage**.</span><span class="sxs-lookup"><span data-stu-id="1e112-133">Access token, site, folder, and file name are passed as parameters to **ImgService.GetImage**.</span></span>
    
<span data-ttu-id="1e112-134">**Примечание:** Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="1e112-134">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
 protected void Page_Load(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                // Set the access token in a hidden field for client-side code to use.
                hdnAccessToken.Value = spContext.UserAccessTokenForSPAppWeb;

                // Set the URLs to the images.
                Image1.ImageUrl = spContext.SPAppWebUrl + "AppImages/O365.png";
                Services.ImgService svc = new Services.ImgService();
                Image2.ImageUrl = svc.GetImage(spContext.UserAccessTokenForSPAppWeb, spContext.SPAppWebUrl.ToString(), "AppImages", "O365.png");
            }
        }
```

<span data-ttu-id="1e112-135">**GetImage** выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1e112-135">**GetImage** does the following:</span></span>

1. <span data-ttu-id="1e112-136">Использует **URL-адрес** для хранения конечных точек GetFolderByServerRelativeUrl REST URI, который будет использоваться для извлечения изображения из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1e112-136">Uses **url** to store the GetFolderByServerRelativeUrl REST endpoint URI, which will be used to retrieve the image from SharePoint.</span></span> <span data-ttu-id="1e112-137">Дополнительные сведения по [ссылаться на файлы и папки API -Интерфейс REST](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e112-137">You can learn more at [Files and folders REST API reference](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx).</span></span>
    
2. <span data-ttu-id="1e112-138">Создает объект [HttpWebRequest](https://msdn.microsoft.com/library/system.net.httpwebrequest.aspx) с помощью **URL-адреса** .</span><span class="sxs-lookup"><span data-stu-id="1e112-138">Instantiates an [HttpWebRequest](https://msdn.microsoft.com/library/system.net.httpwebrequest.aspx) object by using **url** .</span></span>
    
3. <span data-ttu-id="1e112-139">Добавляет заголовок Authorization HttpWebRequest объект, который содержит маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="1e112-139">Adds an Authorization header to the HttpWebRequest object that contains the access token.</span></span> 
    
<span data-ttu-id="1e112-140">После получения вызов URI конечной точки, возвращенные потока — это строка в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="1e112-140">After the GET call is made to the endpoint URI, the returned stream is a Base64-encoded string.</span></span> <span data-ttu-id="1e112-141">Возвращенная строка имеет значение атрибута **src** изображения.</span><span class="sxs-lookup"><span data-stu-id="1e112-141">The returned string is set to the **src** attribute of the image.</span></span>

```C#
 public string GetImage(string accessToken, string site, string folder, string file)
        {
            // Create the HttpWebRequest to call the REST endpoint.
            string url = String.Format("{0}_api/web/GetFolderByServerRelativeUrl('{1}')/Files('{2}')/$value", site, folder, file);
            HttpWebRequest request = WebRequest.Create(url) as HttpWebRequest;
            request.Headers.Add("Authorization", "Bearer" + " " + accessToken);
            using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
            {
                using (var sourceStream = response.GetResponseStream())
                {
                    using (var newStream = new MemoryStream())
                    {
                        sourceSteam.CopyTo(newStream);
                        byte[] bytes = newStream.ToArray();
                        return "data:image/png;base64, " + Convert.ToBase64String(bytes);
                    }
                }
            }
        }
```

<span data-ttu-id="1e112-142">После завершения **Page_Load** Default.aspx запускает клиентский код в файл Default.aspx, которая загружает изображение 3.</span><span class="sxs-lookup"><span data-stu-id="1e112-142">After **Page_Load** finishes, Default.aspx runs the client-side code in Default.aspx, which loads Image 3.</span></span> <span data-ttu-id="1e112-143">Клиентский код вызывает **GetImage** с помощью jQuery Ajax.</span><span class="sxs-lookup"><span data-stu-id="1e112-143">The client-side code calls **GetImage** by using jQuery Ajax.</span></span> <span data-ttu-id="1e112-144">Когда **GetImage** успешно возвращает строку в кодировке Base64, Возвращенная строка имеет значение атрибута **src** Image3.</span><span class="sxs-lookup"><span data-stu-id="1e112-144">When **GetImage** returns the Base64-encoded string successfully, the **src** attribute on Image3 is set to the returned string.</span></span>

```
  ...

                  $.ajax({
                url: '../Services/ImgService.svc/GetImage?accessToken=' + $('#hdnAccessToken').val() + '&amp;site=' + encodeURIComponent(appWebUrl + '/') + '&amp;folder=AppImages&amp;file=O365.png',
                dataType: 'json',
                success: function (data) {
                    $('#Image3').attr('src', data.d);
                },
                error: function (err) {
                    alert('error occurred');
                }
            });

           ...

```

## <a name="additional-resources"></a><span data-ttu-id="1e112-145">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1e112-145">Additional resources</span></span>
<span data-ttu-id="1e112-146"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="1e112-146"></span></span>

- [<span data-ttu-id="1e112-147">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="1e112-147">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
