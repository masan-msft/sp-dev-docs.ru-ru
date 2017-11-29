---
title: "Авторизации у поставщика надстройки пользователей во время выполнения с помощью OAuth"
ms.date: 11/03/2017
ms.openlocfilehash: bf89754b71a892bef15b3ec05bf60b7f5bd39b5d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="authorize-provider-hosted-add-in-users-at-run-time-by-using-oauth"></a><span data-ttu-id="06041-102">Авторизации у поставщика надстройки пользователей во время выполнения с помощью OAuth</span><span class="sxs-lookup"><span data-stu-id="06041-102">Authorize provider-hosted add-in users at run time by using OAuth</span></span>

<span data-ttu-id="06041-103">Предоставить авторизованный доступ к ресурсам SharePoint с помощью OAuth в размещение у поставщика в надстройках во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="06041-103">Provide authorized access to SharePoint resources by using OAuth in provider-hosted add-ins at run time.</span></span>

<span data-ttu-id="06041-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="06041-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="06041-105">Как правило пользователям доступа к SharePoint надстройки с Открытие сайта SharePoint, выбрав **Контент сайта**и затем выбрать надстройку.</span><span class="sxs-lookup"><span data-stu-id="06041-105">Normally, your users access SharePoint add-ins by opening a SharePoint site, choosing  **Site Contents**, and then choosing the add-in.</span></span> <span data-ttu-id="06041-106">SharePoint перенаправляет пользователей на удаленной веб-, где размещение у поставщика в надстройке выполняется.</span><span class="sxs-lookup"><span data-stu-id="06041-106">SharePoint redirects users to the remote web where your provider-hosted add-in runs.</span></span> <span data-ttu-id="06041-107">Так как пользователям получить доступ к надстройки из SharePoint, пользователи могут с SharePoint получения надстройки.</span><span class="sxs-lookup"><span data-stu-id="06041-107">Because users access the add-in from SharePoint, users are authorized by SharePoint before they can access the add-in.</span></span>

<span data-ttu-id="06041-108">Кроме того Если пользователи перейти непосредственно к URL-адрес надстройки размещением у поставщика, что надстройка авторизовать их во время выполнения с помощью OAuth.</span><span class="sxs-lookup"><span data-stu-id="06041-108">Alternatively, if your users go directly to the URL of your provider-hosted add-in, that add-in must authorize them at run time by using OAuth.</span></span> <span data-ttu-id="06041-109">В этом сценарии надстройка размещением у поставщика должен обрабатывать авторизации так как пользователь не был впервые прав с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-109">In this scenario, the provider-hosted add-in must handle authorization because your user wasn't authorized by SharePoint first.</span></span> <span data-ttu-id="06041-110">В примере [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) показано, как динамически запроса разрешения на веб-сайте с помощью OAuth.</span><span class="sxs-lookup"><span data-stu-id="06041-110">The [Core.DynamicPermissions ](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) sample shows you how to dynamically request permissions from a website by using OAuth.</span></span>
<span data-ttu-id="06041-111">Используйте для этого решения:</span><span class="sxs-lookup"><span data-stu-id="06041-111">Use this solution to:</span></span>

- <span data-ttu-id="06041-112">Авторизации пользователей, у которых перейти непосредственно к надстройка размещением у поставщика, а не доступ к надстройки из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-112">Authorize users who navigate directly to your provider-hosted add-in rather than accessing your add-in from SharePoint.</span></span> <span data-ttu-id="06041-113">Например не может разрешить пользователям использовать пользовательский Интерфейс SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-113">For example, you might not want your users to use the SharePoint UI.</span></span> <span data-ttu-id="06041-114">Вместо этого пользователи могут использовать у поставщика надстройки, которая отображает соответствующие данные извлекаются из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-114">Instead, your users might use a provider-hosted add-in that shows relevant data retrieved from SharePoint.</span></span>
    
- <span data-ttu-id="06041-115">Выполните построение у поставщика надстройки, который может выполнять проверку подлинности пользователей с помощью OAuth и может продаваться через магазина Office.</span><span class="sxs-lookup"><span data-stu-id="06041-115">Build a provider-hosted add-in that can authenticate users with OAuth, and that can be sold through the Office Store.</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="06041-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="06041-116">Before you begin</span></span>

<span data-ttu-id="06041-117">Чтобы начать работу, загрузите пример надстройки [Core.DynamicPermissions](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="06041-117">To get started, download the [Core.DynamicPermissions ](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.DynamicPermissions) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="06041-118">Прежде чем запускать пример кода:</span><span class="sxs-lookup"><span data-stu-id="06041-118">Before you run the code sample:</span></span> 

- <span data-ttu-id="06041-119">Убедитесь в том, что требуется разрешение на **Управление** на сайте.</span><span class="sxs-lookup"><span data-stu-id="06041-119">Make sure you have  **Manage** permissions on the site.</span></span> <span data-ttu-id="06041-120">Дополнительные сведения на [Общие сведения об уровнях разрешений](https://support.office.com/article/Understanding-permission-levels-87ECBB0E-6550-491A-8826-C075E4859848).</span><span class="sxs-lookup"><span data-stu-id="06041-120">Learn more at [Understanding permission levels](https://support.office.com/article/Understanding-permission-levels-87ECBB0E-6550-491A-8826-C075E4859848).</span></span>
    
- <span data-ttu-id="06041-121">Регистрация надстройки на сайте SharePoint с помощью AppRegNew.aspx:</span><span class="sxs-lookup"><span data-stu-id="06041-121">Register the add-in on a SharePoint site by using AppRegNew.aspx:</span></span> 
    
    1. <span data-ttu-id="06041-122">Перейдите к appregnew.aspx на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-122">Navigate to appregnew.aspx on your SharePoint site.</span></span> <span data-ttu-id="06041-123">Например если вы хотите использовать надстройки на сайте contoso.sharepoint.com, перейдите к http://contoso.sharepoint.com/_layouts/15/appregnew.aspx.</span><span class="sxs-lookup"><span data-stu-id="06041-123">For example, if you want to use your add-in on the contoso.sharepoint.com site, navigate to http://contoso.sharepoint.com/_layouts/15/appregnew.aspx.</span></span>
    
    2. <span data-ttu-id="06041-124">Нажмите кнопку **Создать** , чтобы создать новый **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="06041-124">Choose  **Generate** to generate a new **Client id**.</span></span>
    
    3. <span data-ttu-id="06041-125">Нажмите кнопку **Создать** , чтобы создать новый **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="06041-125">Choose  **Generate** to generate a new **Client Secret**.</span></span> 
    
    4. <span data-ttu-id="06041-126">Введите название для надстройки в поле **Название**.</span><span class="sxs-lookup"><span data-stu-id="06041-126">Enter a title for your add-in in  **Title**.</span></span>
    
    5. <span data-ttu-id="06041-127">В **домен надстройки**введите URL-адрес надстройки размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="06041-127">In  **Add-in Domain**, enter the URL of your provider-hosted add-in.</span></span> <span data-ttu-id="06041-128">Например введите localhost.</span><span class="sxs-lookup"><span data-stu-id="06041-128">For example, enter localhost.</span></span> 
    
    6. <span data-ttu-id="06041-129">В **URI перенаправления**введите URL-адрес надстройки размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="06041-129">In  **Redirect URI**, enter the URL of your provider-hosted add-in.</span></span> <span data-ttu-id="06041-130">SharePoint будет перенаправлен добавьте в этот URL-адрес после авторизации и подтверждения согласия.</span><span class="sxs-lookup"><span data-stu-id="06041-130">SharePoint will redirect your add-in to this URL after authorization and consent is granted.</span></span> <span data-ttu-id="06041-131">Например введите https://localhost:44363/домашней/обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="06041-131">For example, enter https://localhost:44363/Home/Callback.</span></span> <span data-ttu-id="06041-132">Можно получить имя домена и порта номер из свойства **URL-адрес SSL** на Core.DynamicPermissionsWeb проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06041-132">You can get the domain name and port number from the  **SSL URL** property on the Core.DynamicPermissionsWeb project in Visual Studio.</span></span>
    
    7. <span data-ttu-id="06041-133">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="06041-133">Choose  **Create**.</span></span> 
    
- <span data-ttu-id="06041-134">Скопируйте идентификатор клиента и секрет клиента в элементе **appSettings** в Core.DynamicPermissionsWeb\web.config.</span><span class="sxs-lookup"><span data-stu-id="06041-134">Copy the Client ID and Client Secret into the  **appSettings** element in Core.DynamicPermissionsWeb\web.config.</span></span>

## <a name="using-the-coredynamicpermissions-add-in"></a><span data-ttu-id="06041-135">С помощью надстройки Core.DynamicPermissions</span><span class="sxs-lookup"><span data-stu-id="06041-135">Using the Core.DynamicPermissions add-in</span></span>

<span data-ttu-id="06041-136">При выполнении примера кода:</span><span class="sxs-lookup"><span data-stu-id="06041-136">When you run the code sample:</span></span>

1. <span data-ttu-id="06041-137">В **подключение к Office 365**введите URL-адрес сайта SharePoint, которую вы зарегистрировали надстройки на и нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="06041-137">In  **Connect to Office 365**, enter the URL of the SharePoint site that you registered your add-in on, and then choose  **Connect**.</span></span> <span data-ttu-id="06041-138">Например введите https://contoso.sharepoint.com.</span><span class="sxs-lookup"><span data-stu-id="06041-138">For example, enter https://contoso.sharepoint.com.</span></span>
    
2. <span data-ttu-id="06041-139">Вход на сайт Office 365.</span><span class="sxs-lookup"><span data-stu-id="06041-139">Sign in to your Office 365 site.</span></span>
    
3. <span data-ttu-id="06041-140">Если требуется предоставить разрешения для разрешения, которые требуется добавить в, выберите **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="06041-140">If you are asked to grant consent to the permissions the add-in is requesting, choose  **Trust It**.</span></span> <span data-ttu-id="06041-141">Обратите внимание на то, что вы будете перенаправлены на страницу /_layouts/15/OAuthAuthorize.aspx.</span><span class="sxs-lookup"><span data-stu-id="06041-141">Notice that you are redirected to the /_layouts/15/OAuthAuthorize.aspx page.</span></span> 
    
    <span data-ttu-id="06041-142">**Примечание:**  Ваше пользователь должен иметь разрешения на **Управление** для предоставления разрешения для разрешения, которые требуется добавить в.</span><span class="sxs-lookup"><span data-stu-id="06041-142">**Note:**  Your user must have  **Manage** permissions to grant consent to the permissions the add-in is requesting.</span></span> <span data-ttu-id="06041-143">Дополнительные сведения в [процесс авторизации OAuth кода для SharePoint надстройки](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="06041-143">You can learn more at [Authorization Code OAuth flow for SharePoint Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span></span>

4. <span data-ttu-id="06041-144">В **успешно установлено в домен Contoso**введите имя нового списка для создания и затем выберите **Создать список**.</span><span class="sxs-lookup"><span data-stu-id="06041-144">In  **Successfully connected to Contoso**, enter the name of a new list to create, and then choose  **Create List**.</span></span>
    
5. <span data-ttu-id="06041-145">Убедитесь, что **списки в Contoso**, где отображаются все списки, которые относятся к сайту Contoso, отображаются нового списка.</span><span class="sxs-lookup"><span data-stu-id="06041-145">Verify that  **Lists in Contoso**, which shows all the lists that belong to the Contoso site, shows your new list.</span></span> 
    
<span data-ttu-id="06041-146">При выборе **подключение** на **подключение к Office 365**, **подключение** в Controllers\HomeController.cs вызывается, который затем вызывает **TokenRepository.Connect** .</span><span class="sxs-lookup"><span data-stu-id="06041-146">When choosing  **Connect** on **Connect to Office 365**,  **Connect** in Controllers\HomeController.cs is called, which then calls **TokenRepository.Connect** .</span></span> <span data-ttu-id="06041-147">URL-адрес, введенный пользователем на **подключение к Office 365** передается **TokenRepository.Connect** как **hostUrl**.</span><span class="sxs-lookup"><span data-stu-id="06041-147">The URL entered by the user on **Connect to Office 365** is passed to **TokenRepository.Connect** as **hostUrl**.</span></span>

<span data-ttu-id="06041-148">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="06041-148">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
 public ActionResult Connect(string hostUrl)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Connect(hostUrl);
            return View();            
        }
```

<span data-ttu-id="06041-149">**TokenRepository.Connect** вызывает **TokenHelper.GetAuthorizationUrl** .</span><span class="sxs-lookup"><span data-stu-id="06041-149">**TokenRepository.Connect** calls **TokenHelper.GetAuthorizationUrl** .</span></span> <span data-ttu-id="06041-150">**TokenHelper.GetAuthorizationUrl** возвращает URL-адрес перенаправления OAuthAuthorize.aspx с помощью **hostUrl** и необходимые разрешения на ресурс SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-150">**TokenHelper.GetAuthorizationUrl** returns the redirect URL to OAuthAuthorize.aspx using the **hostUrl** and the desired permissions on the SharePoint resource.</span></span> <span data-ttu-id="06041-151">OAuthAuthorize.aspx используется для авторизации пользователей, использующих OAuth.</span><span class="sxs-lookup"><span data-stu-id="06041-151">OAuthAuthorize.aspx is used to authorize users using OAuth.</span></span> <span data-ttu-id="06041-152">При перенаправлении OAuthorize.aspx, пользователь должен войти в Office 365 и затем соглашаетесь с разрешениями надстройки запрашивает или управления безопасностью.</span><span class="sxs-lookup"><span data-stu-id="06041-152">When redirected to OAuthorize.aspx, the user must sign in to Office 365, and then consent to the permissions the add-in is requesting, or trust the add-in.</span></span> <span data-ttu-id="06041-153">Требуемое разрешение на ресурс SharePoint — **Web.Manage** .</span><span class="sxs-lookup"><span data-stu-id="06041-153">The desired permission on the SharePoint resource is **Web.Manage** .</span></span> <span data-ttu-id="06041-154">После проверки подлинности пользователя пример кода создает списки на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-154">After user authorization, the code sample creates lists on the SharePoint site.</span></span> <span data-ttu-id="06041-155">Для создания списков на сайте SharePoint, пользователи должны иметь разрешения **Web.Manage** .</span><span class="sxs-lookup"><span data-stu-id="06041-155">To create lists on a SharePoint site, users must have **Web.Manage** permissions.</span></span>

<span data-ttu-id="06041-156">**Примечание:** Возвращает URL-адрес формы **TokenHelper.GetAuthorizationUrl** **https://contoso.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?IsDlg=1&amp;client_id =<Client ID>&amp;scope=Web.Manage&amp;response_type = код** , где ** &lt;идентификатор клиента&gt; ** добавить в идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="06041-156">**Note:** **TokenHelper.GetAuthorizationUrl** returns a URL of the form **https://contoso.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?IsDlg=1&amp;client_id=<Client ID>&amp;scope=Web.Manage&amp;response_type=code** , where **&lt;Client ID&gt;** is the add-in's Client ID.</span></span> <span data-ttu-id="06041-157">Если надстройка зарегистрирована через панель мониторинга продаж, любого сайта Office 365 можно установить надстройку.</span><span class="sxs-lookup"><span data-stu-id="06041-157">If your add-in is registered through the Seller Dashboard, any Office 365 site can install the add-in.</span></span> <span data-ttu-id="06041-158">Если надстройка не зарегистрирован через панель мониторинга продавца, необходимо зарегистрировать надстройки с помощью appregnew.aspx и обновите Core.DynamicPermissionsWeb\web.config. Для получения дополнительных сведений см[Регистрация надстройки SharePoint 2013](http://msdn.microsoft.com/library/be41a5dc-2af9-4fd9-bf4e-ad6dfa849524%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="06041-158">If your add-in is not registered through the Seller Dashboard, you must register your add-in by using appregnew.aspx, and then update Core.DynamicPermissionsWeb\web.config. To learn more, see[Register SharePoint Add-ins 2013](http://msdn.microsoft.com/library/be41a5dc-2af9-4fd9-bf4e-ad6dfa849524%28Office.15%29.aspx).</span></span>

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

<span data-ttu-id="06041-159">После авторизации надстройки перенаправляется **обратного вызова** в Controllers\HomeController.cs, являющийся перенаправление URI, заданного в appregnew.aspx.</span><span class="sxs-lookup"><span data-stu-id="06041-159">After authorization, the add-in is redirected to  **Callback** in Controllers\HomeController.cs, which is the Redirect URI specified on the appregnew.aspx.</span></span> <span data-ttu-id="06041-160">**TokenHelper** передает код авторизации, **код** **обратного вызова** .</span><span class="sxs-lookup"><span data-stu-id="06041-160">**TokenHelper** passes the authorization code, **code** , to **Callback** .</span></span> <span data-ttu-id="06041-161">Чтобы предоставить маркер доступа, описанных далее в этой статье, код авторизации, **код** , должны быть возвращены в **обратного вызова** .</span><span class="sxs-lookup"><span data-stu-id="06041-161">To grant the access token described later in this article, the authorization code, **code** , must be returned to **Callback** .</span></span> <span data-ttu-id="06041-162">Затем **обратный** вызов **TokenRepository.Callback** .</span><span class="sxs-lookup"><span data-stu-id="06041-162">**Callback** then calls **TokenRepository.Callback** .</span></span>

```C#
 public ActionResult Callback(string code)
        {
            TokenRepository repository = new TokenRepository(Request, Response);
            repository.Callback(code);
            return RedirectToAction("Index");
        }
```

<span data-ttu-id="06041-163">**TokenRepository.Callback** вызывает **TokenCache.UpdateCacheWithCode** , который использует **TokenHelper.GetAccessToken** для получения маркера доступа OAuth на основе кода авторизации, **код** .</span><span class="sxs-lookup"><span data-stu-id="06041-163">**TokenRepository.Callback** calls **TokenCache.UpdateCacheWithCode** , which uses **TokenHelper.GetAccessToken** to obtain an OAuth access token based on the authorization code, **code** .</span></span>

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

<span data-ttu-id="06041-164">Добавьте в теперь имеет маркер доступа для этого пользователя и можно перейти к Создание списков на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="06041-164">Your add-in now has the access token for this user and can proceed to create lists on the SharePoint site.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06041-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="06041-165">Additional resources</span></span>
<span data-ttu-id="06041-166"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="06041-166"></span></span>

- <span data-ttu-id="06041-167">[Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="06041-167">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>
    
