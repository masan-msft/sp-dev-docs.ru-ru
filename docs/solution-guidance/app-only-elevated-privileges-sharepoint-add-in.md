---
title: "Права только для приложений и с повышенными привилегиями в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 9bcdbe3f5bb31e0c01fac300bb237bf0134c84a1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
<a name="app-only-and-elevated-privileges-in-the-sharepoint-add-in-model"></a><span data-ttu-id="64d85-102">Права только для приложений и с повышенными привилегиями в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="64d85-102">App-only and elevated privileges in the SharePoint add-in model</span></span>
===============================================================

<a name="summary"></a><span data-ttu-id="64d85-103">Summary</span><span class="sxs-lookup"><span data-stu-id="64d85-103">Summary</span></span>
-------

<span data-ttu-id="64d85-104">Подхода, можно повысить уровень привилегий в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="64d85-104">The approach you take to elevate privileges in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="64d85-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, RunWithElevatedPrivileges API используется с код на сервере объектной модели SharePoint и развернуты с помощью решений фермы.</span><span class="sxs-lookup"><span data-stu-id="64d85-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the RunWithElevatedPrivileges API is used with the SharePoint server-side object model code and deployed via Farm Solutions.</span></span>

<span data-ttu-id="64d85-106">В SharePoint надстройки модели сценарий, AllowAppOnlyPolicy разрешений или учетную запись службы используется для разрешения текущего пользователя для выполнения операций, они не авторизации для выполнения.</span><span class="sxs-lookup"><span data-stu-id="64d85-106">In an SharePoint Add-in model scenario, the AllowAppOnlyPolicy permission or a service account is used to allow the current user to execute operations they are not authorize to perform.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="64d85-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="64d85-107">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="64d85-108">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для повышения привилегий в коде.</span><span class="sxs-lookup"><span data-stu-id="64d85-108">As a rule of a thumb, we would like to provide the following high-level guidelines for elevating privileges in code.</span></span>

- <span data-ttu-id="64d85-109">AllowAppOnlyPolicy не работает с</span><span class="sxs-lookup"><span data-stu-id="64d85-109">AllowAppOnlyPolicy does not work with</span></span> 
    + <span data-ttu-id="64d85-110">Поиск — Если целевой объект локальная версия SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-110">Search - if target is SharePoint On-Premises.</span></span> <span data-ttu-id="64d85-111">SharePoint Online поддержка добавлена ([запись в блоге](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))</span><span class="sxs-lookup"><span data-stu-id="64d85-111">SharePoint Online support for it has been added ([blog post](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))</span></span>
    + <span data-ttu-id="64d85-112">Операции CSOM профиля пользователя, за исключением того, что можно использовать API обновления массового профилей пользователей с разрешениями только для приложений</span><span class="sxs-lookup"><span data-stu-id="64d85-112">User Profile CSOM operations, except that the User Profile Bulk Update API can be used with app-only permissions</span></span>
    + <span data-ttu-id="64d85-113">Обновление записей службы таксономии (запись) — чтение works</span><span class="sxs-lookup"><span data-stu-id="64d85-113">Updating taxonomy service entries (write) - read works</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="64d85-114">В следующих ситуациях необходимо использовать учетную запись службы.</span><span class="sxs-lookup"><span data-stu-id="64d85-114">In these scenarios you need to use a specific service account.</span></span>

- <span data-ttu-id="64d85-115">AllowAppOnlyPolicy аналогично RunWithElevatedPrivileges, но не точно так же.</span><span class="sxs-lookup"><span data-stu-id="64d85-115">AllowAppOnlyPolicy is similar to RunWithElevatedPrivileges, but not exactly the same.</span></span>
    + <span data-ttu-id="64d85-116">AllowAppOnlyPolicy выполняет код на основании разрешения, предоставленные для SharePoint надстройки, не от имени другого пользователя, который имеет соответствующие разрешения на выполнение операции.</span><span class="sxs-lookup"><span data-stu-id="64d85-116">AllowAppOnlyPolicy executes code based on the permissions granted to the SharePoint Add-in, not on behalf of another user who has the appropriate permissions to perform an operation.</span></span>

<span data-ttu-id="64d85-117">Ниже приведен пример возвращает маркер политики приложения и использовать его для создания объекта контекста.</span><span class="sxs-lookup"><span data-stu-id="64d85-117">Here is an example of returning an App Only Policy token and using it to create a context object.</span></span>

    Uri siteUrl = new Uri(ConfigurationManager.AppSettings["MySiteUrl"]);
    try
    {
        //Connect to the give site using App Only token
        string realm = TokenHelper.GetRealmFromTargetUrl(siteUrl);
        var token = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUrl.Authority, realm).AccessToken;

        using (var ctx = TokenHelper.GetClientContextWithAccessToken(siteUrl.ToString(), token))
        {
            // Perform operations using the app only token access. 
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error in execution: " + ex.Message);
    }

- <span data-ttu-id="64d85-118">При использовании AllowAppOnlyPolicy, помните о работает только в размещенном у поставщика SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="64d85-118">When using the AllowAppOnlyPolicy, keep in mind it only works in Provider-hosted SharePoint Add-ins.</span></span>
- <span data-ttu-id="64d85-119">AllowAppOnlyPolicy не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="64d85-119">AllowAppOnlyPolicy does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>
- <span data-ttu-id="64d85-120">Учетные записи служб, определяются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-120">Service accounts are defined in SharePoint.</span></span>
    + <span data-ttu-id="64d85-121">В клиента Office 365 в зависимости от функциональных возможностей у требований к коду, учетные записи служб может потребоваться лицензии Office 365, назначенные им.</span><span class="sxs-lookup"><span data-stu-id="64d85-121">In an Office 365 tenancy, depending what functionality your code requirements have, the service accounts may need an Office 365 license assigned to them.</span></span>
    + <span data-ttu-id="64d85-122">Можно создать учетные записи служб на отдельных основы надстройки SharePoint или использование одной учетной записи для всех SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="64d85-122">You can create service accounts on a per SharePoint Add-in basis, or use a single account for all SharePoint Add-ins.</span></span>
    + <span data-ttu-id="64d85-123">Создание понятными и описательными имен для учетных записей служб, можно легко отслеживать операций, выполняемых ими.</span><span class="sxs-lookup"><span data-stu-id="64d85-123">Create clear and descriptive names for the service accounts so you can easily track the operations they perform.</span></span>
    
    <span data-ttu-id="64d85-124">Например: Если надстройки SharePoint изменяет элементы списков, столбец Автор изменений для элементов списка отображается имя учетной записи службы, связанной с помощью надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-124">For example: If your SharePoint Add-in modifies list items, the Modified By column for the list items will display the name of the service account associated with the SharePoint Add-in.</span></span>

- <span data-ttu-id="64d85-125">При проверке подлинности с помощью учетных записей служб, вы должны получить имя пользователя и пароль для учетной записи службы.</span><span class="sxs-lookup"><span data-stu-id="64d85-125">When authenticating with service accounts, you must retrieve a user name and password for the service account.</span></span>
    + <span data-ttu-id="64d85-126">Приведенный ниже фрагмент кода иллюстрирует, используя имя пользователя и пароль для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="64d85-126">The code snippet below illustrates using a user name and password to authenticate.</span></span>
    + <span data-ttu-id="64d85-127">Будьте внимательны для хранения и извлечения имя пользователя и пароль безопасным образом.</span><span class="sxs-lookup"><span data-stu-id="64d85-127">Take care to store and retrieve the user name and password in a secure fashion.</span></span>

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {
    
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<a name="options-to-elevate-permissions"></a><span data-ttu-id="64d85-128">Параметры, чтобы повысить уровень разрешений</span><span class="sxs-lookup"><span data-stu-id="64d85-128">Options to elevate permissions</span></span>
------------------------------

<span data-ttu-id="64d85-129">У вас есть две возможности повышения уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="64d85-129">You have a couple of options to elevate permissions.</span></span>

- <span data-ttu-id="64d85-130">OAuth (AllowAppOnlyPolicy)</span><span class="sxs-lookup"><span data-stu-id="64d85-130">OAuth (AllowAppOnlyPolicy)</span></span>
    + <span data-ttu-id="64d85-131">S2S (sub вариант)</span><span class="sxs-lookup"><span data-stu-id="64d85-131">S2S (sub option)</span></span>
    + <span data-ttu-id="64d85-132">ACS (sub вариант)</span><span class="sxs-lookup"><span data-stu-id="64d85-132">ACS (sub option)</span></span>
- <span data-ttu-id="64d85-133">Учетная запись службы</span><span class="sxs-lookup"><span data-stu-id="64d85-133">Service Account</span></span>
    + <span data-ttu-id="64d85-134">Удаленно размещенных кода (пример: Azure WebJob)</span><span class="sxs-lookup"><span data-stu-id="64d85-134">Remotely hosted code (Example: Azure WebJob)</span></span>

<a name="oauth-allowapponlypolicy"></a><span data-ttu-id="64d85-135">OAuth (AllowAppOnlyPolicy)</span><span class="sxs-lookup"><span data-stu-id="64d85-135">OAuth (AllowAppOnlyPolicy)</span></span>
--------------------------
<span data-ttu-id="64d85-136">В этом параметре AllowAppOnlyPolicy задано значение true в элемент AppPermissionRequests и разрешения, заданный в манифесте добавить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-136">In this option the AllowAppOnlyPolicy is set to true in the AppPermissionRequests element and permissions are set in the SharePoint Add-in manifest.</span></span> <span data-ttu-id="64d85-137">OAuth используется для получения маркера доступа, чтобы разрешить надстройки SharePoint для выполнения операций, имеющий разрешения на выполнение.</span><span class="sxs-lookup"><span data-stu-id="64d85-137">OAuth is used to return access tokens to allow the SharePoint Add-in to execute operations it has permissions to perform.</span></span>

<span data-ttu-id="64d85-138">**Параметр sub S2S**</span><span class="sxs-lookup"><span data-stu-id="64d85-138">**S2S sub option**</span></span>

<span data-ttu-id="64d85-139">S2S sub параметр работает только в локальной среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-139">The S2S sub option only works in on-premises SharePoint environments.</span></span>

<span data-ttu-id="64d85-140">При проверке подлинности с помощью OAuth в сценарии S2S метод **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** используется для получения маркера доступа для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-140">When authenticating via OAuth in an S2S scenario the **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** method is used to return the access token for the SharePoint Add-in.</span></span>  <span data-ttu-id="64d85-141">Маркер доступа позволяет надстройки SharePoint для выполнения любых операций, предоставленные надстройки SharePoint в манифесте добавить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-141">The access token allows the SharePoint Add-in to perform any operations the SharePoint Add-in is granted in the SharePoint Add-in manifest.</span></span>

<span data-ttu-id="64d85-142">Этот параметр не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="64d85-142">This option does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>

<span data-ttu-id="64d85-143">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="64d85-143">**When is it a good fit?**</span></span>

<span data-ttu-id="64d85-144">Если вам необходимо повысить уровень привилегий в сценарии SharePoint S2S это является хорошим выбором, поскольку этот параметр, для работы с S2S и очень просто реализовать.</span><span class="sxs-lookup"><span data-stu-id="64d85-144">When you need to elevate privileges in a SharePoint S2S scenario this is a good option because this option works with S2S and is very easy to implement.</span></span>

<span data-ttu-id="64d85-145">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="64d85-145">**Getting Started**</span></span>

<span data-ttu-id="64d85-146">Следующей статье показано, как использовать AllowAppOnlyPolicy с S2S.</span><span class="sxs-lookup"><span data-stu-id="64d85-146">The following article demonstrates how to use AllowAppOnlyPolicy with S2S.</span></span>

- [<span data-ttu-id="64d85-147">Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)</span><span class="sxs-lookup"><span data-stu-id="64d85-147">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<span data-ttu-id="64d85-148">**Параметр sub ACS**</span><span class="sxs-lookup"><span data-stu-id="64d85-148">**ACS sub option**</span></span>

<span data-ttu-id="64d85-149">Параметр sub ACS работать в средах Office 365 SharePoint и локальных.</span><span class="sxs-lookup"><span data-stu-id="64d85-149">The ACS sub option work in on-premises and Office 365 SharePoint environments.</span></span>

<span data-ttu-id="64d85-150">При проверке подлинности с помощью OAuth в сценарии ACS **TokenHelper::GetAppOnlyAccessTokenmethod** используется для получения маркера доступа для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-150">When authenticating via OAuth in an ACS scenario the **TokenHelper::GetAppOnlyAccessTokenmethod** is used to return the access token for the SharePoint Add-in.</span></span>  <span data-ttu-id="64d85-151">Метод **TokenHelper::GetClientContextWithAccessToken** вызывается для возвращения контекста клиента, необходимые для выполнения каких-либо надстройки SharePoint имеет разрешения на выполнение операций, основанные на разрешения, предоставленные в манифесте добавить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-151">Then, the **TokenHelper::GetClientContextWithAccessToken** method is invoked to return the client context necessary to perform any operations the SharePoint Add-in has permission to do based on the permissions granted in the SharePoint Add-in manifest.</span></span>

<span data-ttu-id="64d85-152">Этот параметр не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="64d85-152">This option does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>

<span data-ttu-id="64d85-153">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="64d85-153">**When is it a good fit?**</span></span>

<span data-ttu-id="64d85-154">Если вам необходимо повысить уровень привилегий в сценарии SharePoint ACS это является хорошим выбором, поскольку этот параметр, для работы с ACS и очень просто реализовать.</span><span class="sxs-lookup"><span data-stu-id="64d85-154">When you need to elevate privileges in a SharePoint ACS scenario this is a good option because this option works with ACS and is very easy to implement.</span></span>  <span data-ttu-id="64d85-155">Этот параметр используется подходит, если у вас есть в локальной среде SharePoint, имеющей отношения доверия с ACS.</span><span class="sxs-lookup"><span data-stu-id="64d85-155">This option is a good fit when you have an on-premises SharePoint environment that has an established trust with ACS.</span></span>  <span data-ttu-id="64d85-156">Это единственным вариантом OAuth, когда у вас есть в среде Office 365 SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d85-156">This is your only OAuth option when you have a Office 365 SharePoint environment.</span></span>

<span data-ttu-id="64d85-157">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="64d85-157">**Getting Started**</span></span>

<span data-ttu-id="64d85-158">В следующей статье демонстрируется использование AllowAppOnlyPolicy с ACS.</span><span class="sxs-lookup"><span data-stu-id="64d85-158">The following article demonstrates how to use AllowAppOnlyPolicy with ACS.</span></span>

- [<span data-ttu-id="64d85-159">Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)</span><span class="sxs-lookup"><span data-stu-id="64d85-159">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<a name="service-account"></a><span data-ttu-id="64d85-160">Учетная запись службы</span><span class="sxs-lookup"><span data-stu-id="64d85-160">Service Account</span></span>
---------------
<span data-ttu-id="64d85-161">В этом шаблоне класс SharePointOnlineCredentials используется для установки контекста пользователя, который выполняет код.</span><span class="sxs-lookup"><span data-stu-id="64d85-161">In this pattern, the SharePointOnlineCredentials class is used to establish the context of a user that executes code.</span></span>

<span data-ttu-id="64d85-162">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="64d85-162">**When is it a good fit?**</span></span>

<span data-ttu-id="64d85-163">Для выполнения кода от имени определенного пользователя (учетная запись службы) это является хорошим выбором, так как он выполняет действия на пользователя (учетная запись службы) и разрешений SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="64d85-163">When you need to execute code on behalf of a specific user (service account) this is a good option because it performs actions on the user's (service account) and the SharePoint Add-in's permissions.</span></span>

<span data-ttu-id="64d85-164">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="64d85-164">**Getting Started**</span></span>

<span data-ttu-id="64d85-165">В следующей статье описывается, как класс SharePointOnlineCredentials используется для установки контекста пользователя, который выполняет код.</span><span class="sxs-lookup"><span data-stu-id="64d85-165">The following article demonstrates how the SharePointOnlineCredentials class is used to establish the context of a user that executes code.</span></span>

- [<span data-ttu-id="64d85-166">Начало работы по построению WebJobs Azure («задания таймера») для Office 365 сайтов (раздел сведения о выполнении проверки подлинности) - статья блога Zimmergren Тобиаса</span><span class="sxs-lookup"><span data-stu-id="64d85-166">Getting Started with building Azure WebJobs ("Timer Jobs") for your Office 365 sites (Authentication considerations section) - Tobias Zimmergren Blog Article</span></span>](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)

<a name="related-links"></a><span data-ttu-id="64d85-167">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="64d85-167">Related links</span></span>
=============
- [<span data-ttu-id="64d85-168">Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)</span><span class="sxs-lookup"><span data-stu-id="64d85-168">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)
- [<span data-ttu-id="64d85-169">Начало работы по построению WebJobs Azure («задания таймера») для Office 365 сайтов (раздел сведения о выполнении проверки подлинности) - статья блога Zimmergren Тобиаса</span><span class="sxs-lookup"><span data-stu-id="64d85-169">Getting Started with building Azure WebJobs ("Timer Jobs") for your Office 365 sites (Authentication considerations section) - Tobias Zimmergren Blog Article</span></span>](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)
- [<span data-ttu-id="64d85-170">Класс SharePointOnlineCredentials (документация по API MSDN)</span><span class="sxs-lookup"><span data-stu-id="64d85-170">SharePointOnlineCredentials class (MSDN API Documentation)</span></span>](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.sharepointonlinecredentials.aspx)
- [<span data-ttu-id="64d85-171">С помощью надстройки только аудио- и только разрешения с помощью запросов поиска в SharePoint Online — на статья блога Vesa Juvonen</span><span class="sxs-lookup"><span data-stu-id="64d85-171">Using add-in only / app-only permissions with search queries in SharePoint Online - Vesa Juvonen Blog Article</span></span>](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)
- <span data-ttu-id="64d85-172">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="64d85-172">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="64d85-173">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="64d85-173">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="64d85-174">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="64d85-174">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="64d85-175">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="64d85-175">Related PnP samples</span></span>
===================

- [<span data-ttu-id="64d85-176">Core.SimpleTimerJob (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="64d85-176">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- <span data-ttu-id="64d85-177">Примеры и содержимое в https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="64d85-177">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="64d85-178">Применимо к</span><span class="sxs-lookup"><span data-stu-id="64d85-178">Applies to</span></span>
==========
- <span data-ttu-id="64d85-179">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="64d85-179">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="64d85-180">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="64d85-180">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="64d85-181">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="64d85-181">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="64d85-182">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="64d85-182">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
