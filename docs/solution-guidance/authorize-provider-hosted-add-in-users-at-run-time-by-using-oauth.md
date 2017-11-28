---
title: "Авторизации у поставщика надстройки пользователей во время выполнения с помощью OAuth"
ms.date: 11/03/2017
ms.openlocfilehash: bf89754b71a892bef15b3ec05bf60b7f5bd39b5d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="authorize-provider-hosted-add-in-users-at-run-time-by-using-oauth"></a>Авторизации у поставщика надстройки пользователей во время выполнения с помощью OAuth

Предоставить авторизованный доступ к ресурсам SharePoint с помощью OAuth в размещение у поставщика в надстройках во время выполнения.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Как правило пользователям доступа к SharePoint надстройки с Открытие сайта SharePoint, выбрав **Контент сайта**и затем выбрать надстройку. SharePoint перенаправляет пользователей на удаленной веб-, где размещение у поставщика в надстройке выполняется. Так как пользователям получить доступ к надстройки из SharePoint, пользователи могут с SharePoint получения надстройки.

Кроме того Если пользователи перейти непосредственно к URL-адрес надстройки размещением у поставщика, что надстройка авторизовать их во время выполнения с помощью OAuth. В этом сценарии надстройка размещением у поставщика должен обрабатывать авторизации так как пользователь не был впервые прав с SharePoint. В примере [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) показано, как динамически запроса разрешения на веб-сайте с помощью OAuth.
Используйте для этого решения:

- Авторизации пользователей, у которых перейти непосредственно к надстройка размещением у поставщика, а не доступ к надстройки из SharePoint. Например не может разрешить пользователям использовать пользовательский Интерфейс SharePoint. Вместо этого пользователи могут использовать у поставщика надстройки, которая отображает соответствующие данные извлекаются из SharePoint.
    
- Выполните построение у поставщика надстройки, который может выполнять проверку подлинности пользователей с помощью OAuth и может продаваться через магазина Office.
    
## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать пример кода: 

- Убедитесь в том, что требуется разрешение на **Управление** на сайте. Дополнительные сведения на [Общие сведения об уровнях разрешений](https://support.office.com/article/Understanding-permission-levels-87ECBB0E-6550-491A-8826-C075E4859848).
    
- Регистрация надстройки на сайте SharePoint с помощью AppRegNew.aspx: 
    
    1. Перейдите к appregnew.aspx на сайте SharePoint. Например если вы хотите использовать надстройки на сайте contoso.sharepoint.com, перейдите к http://contoso.sharepoint.com/_layouts/15/appregnew.aspx.
    
    2. Нажмите кнопку **Создать** , чтобы создать новый **идентификатор клиента**.
    
    3. Нажмите кнопку **Создать** , чтобы создать новый **Секрет клиента**. 
    
    4. Введите название для надстройки в поле **Название**.
    
    5. В **домен надстройки**введите URL-адрес надстройки размещением у поставщика. Например введите localhost. 
    
    6. В **URI перенаправления**введите URL-адрес надстройки размещением у поставщика. SharePoint будет перенаправлен добавьте в этот URL-адрес после авторизации и подтверждения согласия. Например введите https://localhost:44363/домашней/обратного вызова. Можно получить имя домена и порта номер из свойства **URL-адрес SSL** на Core.DynamicPermissionsWeb проекта в Visual Studio.
    
    7. Нажмите кнопку **Создать**. 
    
- Скопируйте идентификатор клиента и секрет клиента в элементе **appSettings** в Core.DynamicPermissionsWeb\web.config.

## <a name="using-the-coredynamicpermissions-add-in"></a>С помощью надстройки Core.DynamicPermissions

При выполнении примера кода:

1. В **подключение к Office 365**введите URL-адрес сайта SharePoint, которую вы зарегистрировали надстройки на и нажмите кнопку **Подключить**. Например введите https://contoso.sharepoint.com.
    
2. Вход на сайт Office 365.
    
3. Если требуется предоставить разрешения для разрешения, которые требуется добавить в, выберите **Доверять**. Обратите внимание на то, что вы будете перенаправлены на страницу /_layouts/15/OAuthAuthorize.aspx. 
    
    **Примечание:**  Ваше пользователь должен иметь разрешения на **Управление** для предоставления разрешения для разрешения, которые требуется добавить в. Дополнительные сведения в [процесс авторизации OAuth кода для SharePoint надстройки](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).

4. В **успешно установлено в домен Contoso**введите имя нового списка для создания и затем выберите **Создать список**.
    
5. Убедитесь, что **списки в Contoso**, где отображаются все списки, которые относятся к сайту Contoso, отображаются нового списка. 
    
При выборе **подключение** на **подключение к Office 365**, **подключение** в Controllers\HomeController.cs вызывается, который затем вызывает **TokenRepository.Connect** . URL-адрес, введенный пользователем на **подключение к Office 365** передается **TokenRepository.Connect** как **hostUrl**.

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
 public ActionResult Connect(string hostUrl)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Connect(hostUrl);
            return View();            
        }
```

**TokenRepository.Connect** вызывает **TokenHelper.GetAuthorizationUrl** . **TokenHelper.GetAuthorizationUrl** возвращает URL-адрес перенаправления OAuthAuthorize.aspx с помощью **hostUrl** и необходимые разрешения на ресурс SharePoint. OAuthAuthorize.aspx используется для авторизации пользователей, использующих OAuth. При перенаправлении OAuthorize.aspx, пользователь должен войти в Office 365 и затем соглашаетесь с разрешениями надстройки запрашивает или управления безопасностью. Требуемое разрешение на ресурс SharePoint — **Web.Manage** . После проверки подлинности пользователя пример кода создает списки на сайте SharePoint. Для создания списков на сайте SharePoint, пользователи должны иметь разрешения **Web.Manage** .

**Примечание:** Возвращает URL-адрес формы **TokenHelper.GetAuthorizationUrl** **https://contoso.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?IsDlg=1&amp;client_id =<Client ID>&amp;scope=Web.Manage&amp;response_type = код** , где ** &lt;идентификатор клиента&gt; ** добавить в идентификатор клиента. Если надстройка зарегистрирована через панель мониторинга продаж, любого сайта Office 365 можно установить надстройку. Если надстройка не зарегистрирован через панель мониторинга продавца, необходимо зарегистрировать надстройки с помощью appregnew.aspx и обновите Core.DynamicPermissionsWeb\web.config. Для получения дополнительных сведений см[Регистрация надстройки SharePoint 2013](http://msdn.microsoft.com/library/be41a5dc-2af9-4fd9-bf4e-ad6dfa849524%28Office.15%29.aspx).

```C#
 public void Connect(string hostUrl)
        {
            if (!IsConnectedToO365)
            {
                HttpCookie spHostUrlCookie = new HttpCookie("SPHostUrl");
                spHostUrlCookie.Value = hostUrl;
                spHostUrlCookie.Expires = DateTime.Now.AddYears(5);
                _response.Cookies.Add(spHostUrlCookie);
                _response.Redirect(TokenHelper.GetAuthorizationUrl(hostUrl, "Web.Manage"));
            }
        }
```

После авторизации надстройки перенаправляется **обратного вызова** в Controllers\HomeController.cs, являющийся перенаправление URI, заданного в appregnew.aspx. **TokenHelper** передает код авторизации, **код** **обратного вызова** . Чтобы предоставить маркер доступа, описанных далее в этой статье, код авторизации, **код** , должны быть возвращены в **обратного вызова** . Затем **обратный** вызов **TokenRepository.Callback** .

```C#
 public ActionResult Callback(string code)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Callback(code);
            return RedirectToAction("Index");
        }
```

**TokenRepository.Callback** вызывает **TokenCache.UpdateCacheWithCode** , который использует **TokenHelper.GetAccessToken** для получения маркера доступа OAuth на основе кода авторизации, **код** .

```C#
public void Callback(string code)
        {
            HttpCookie spHostUrlCookie = _request.Cookies["SPHostUrl"];
            if (null != spHostUrlCookie)
            {
                Uri sharePointSiteUrl = new Uri(spHostUrlCookie.Value);
                TokenCache.UpdateCacheWithCode(_request, _response, sharePointSiteUrl);
            }
        }
```

```C#
 public static void UpdateCacheWithCode(HttpRequestBase request, HttpResponseBase response, Uri targetUri)
        {
            string refreshToken = TokenHelper.GetAccessToken(request.QueryString["code"], "00000003-0000-0ff1-ce00-000000000000", targetUri.Authority, TokenHelper.GetRealmFromTargetUrl(targetUri), new Uri(request.Url.GetLeftPart(UriPartial.Path))).RefreshToken;
            SetRefreshTokenCookie(response.Cookies, refreshToken);
            SetRefreshTokenCookie(request.Cookies, refreshToken);
        }
```

Добавьте в теперь имеет маркер доступа для этого пользователя и можно перейти к Создание списков на сайте SharePoint. 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).
    
