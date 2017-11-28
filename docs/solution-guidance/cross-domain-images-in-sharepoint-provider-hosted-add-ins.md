---
title: "Изображения между доменами в SharePoint размещение у поставщика в надстройках"
ms.date: 11/03/2017
ms.openlocfilehash: 3260b534a87fbb097fdaa5910a1c41f276514733
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="cross-domain-images-in-sharepoint-provider-hosted-add-ins"></a>Изображения между доменами в SharePoint размещение у поставщика в надстройках

Использование изображения между доменами в размещенном у поставщика надстроек.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Может потребоваться отображения изображений на сайте SharePoint в размещенном у поставщика надстройки. Поскольку у поставщика надстроек выполняются на удаленной веб-, отличаются доменов для надстройки размещением у поставщика и сайта SharePoint. Например надстройки могут выполняться в Microsoft Azure и вы пытаетесь Показывать изображение из Office 365. Так как размещение у поставщика в надстройке пересечение доменов для доступа к изображения, SharePoint требуется проверка подлинности пользователя перед надстройки размещением у поставщика показывает изображения.

Пример кода [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) показано, как размещение у поставщика в надстройке можно использовать маркер доступа SharePoint и службы REST для получения изображений из SharePoint. Службы REST возвращается в кодировке Base64 строку, которая используется для отображения изображения в браузере. Использование решения в этом примере для отображения изображений, хранящихся в SharePoint в размещенном у поставщика надстроек с помощью кода на сервере или на клиентском компьютере.

**Примечание:** Так как он использует конечных точек REST, можно использовать на сервере или клиентский код для извлечения изображения.

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-corecrossdomainimages-code-sample"></a>Использование примера кода Core.CrossDomainImages

При запуске в этом примере Default.aspx пытается загрузить следующее:

- Изображение 1, с помощью абсолютный URL-адрес. 
    
- Изображение 2, с помощью вызова на сервере для конечных точек REST, который возвращает строку в кодировке Base64.
    
- Изображение 3, с помощью вызова со стороны клиента для конечных точек REST, который возвращает строку в кодировке Base64.
    
**Примечание:** Изображение 1 не выполняет обработку, так как надстройки пересечение доменов для получения изображения в SharePoint. Обратите внимание, что URL-адрес надстройки размещением у поставщика запускается на localhost. Откройте контекстное меню (щелкните правой кнопкой мыши) для образа 1 и выберите пункт **Свойства**. Обратите внимание на то, что **(URL-адреса)** пытается получить изображение из надстройки веб-приложения не localhost. Так как надстройка размещением у поставщика пересечение доменов для связи с веб-надстройки, чтобы получить доступ к изображения требуется проверка подлинности. Убедитесь, что доступ к изображение 1 URL-адрес напрямую, в отличие от вызова доменам в размещенном у поставщика надстройки, разрешается без ошибок, копирование и вставка **(URL-адреса)** в новом окне браузера. Обратите внимание, что изображение 1 отображается без ошибок. Сравнение источника изображения 1 для источника изображения 2. Обратите внимание на то, что **Адрес (URL)** указывает строка в кодировке Base64.

При загрузке Default.aspx **Page_Load** запускает и выполняет следующее:

1. Задает Image1.ImageUrl абсолютный путь к изображению.
    
2. Создает экземпляр ImgService. ImgService — это конечная точка REST, на котором выполняется в том же домене, что надстройка размещением у поставщика.
    
3. Задает строку в кодировке Base64, которое возвращает **ImgService.GetImage** Image2.ImageUrl. Маркер доступа, сайтов, папку и имя файла, передаются в качестве параметров **ImgService.GetImage**.
    
**Примечание:** Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

**GetImage** выполняет следующие действия:

1. Использует **URL-адрес** для хранения конечных точек GetFolderByServerRelativeUrl REST URI, который будет использоваться для извлечения изображения из SharePoint. Дополнительные сведения по [ссылаться на файлы и папки API -Интерфейс REST](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx).
    
2. Создает объект [HttpWebRequest](https://msdn.microsoft.com/library/system.net.httpwebrequest.aspx) с помощью **URL-адреса** .
    
3. Добавляет заголовок Authorization HttpWebRequest объект, который содержит маркер доступа. 
    
После получения вызов URI конечной точки, возвращенные потока — это строка в кодировке Base64. Возвращенная строка имеет значение атрибута **src** изображения.

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

После завершения **Page_Load** Default.aspx запускает клиентский код в файл Default.aspx, которая загружает изображение 3. Клиентский код вызывает **GetImage** с помощью jQuery Ajax. Когда **GetImage** успешно возвращает строку в кодировке Base64, Возвращенная строка имеет значение атрибута **src** Image3.

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

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
