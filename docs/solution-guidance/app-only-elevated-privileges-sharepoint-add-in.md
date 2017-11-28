---
title: "Права только для приложений и с повышенными привилегиями в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 126e9e578d517c3076b9b6e7153df81506538dc0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="app-only-and-elevated-privileges-in-the-sharepoint-add-in-model"></a><span data-ttu-id="3a21c-102">Права только для приложений и с повышенными привилегиями в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a21c-102">App-only and elevated privileges in the SharePoint add-in model</span></span>
===============================================================

<a name="summary"></a><span data-ttu-id="3a21c-103">Summary</span><span class="sxs-lookup"><span data-stu-id="3a21c-103">Summary</span></span>
-------

<span data-ttu-id="3a21c-104">Подхода, можно повысить уровень привилегий в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="3a21c-104">The approach you take to elevate privileges in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="3a21c-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, RunWithElevatedPrivileges API используется с код на сервере объектной модели SharePoint и развернуты с помощью решений фермы.</span><span class="sxs-lookup"><span data-stu-id="3a21c-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the RunWithElevatedPrivileges API is used with the SharePoint server-side object model code and deployed via Farm Solutions.</span></span>

<span data-ttu-id="3a21c-106">В SharePoint надстройки модели сценарий, AllowAppOnlyPolicy разрешений или учетную запись службы используется для разрешения текущего пользователя для выполнения операций, они не авторизации для выполнения.</span><span class="sxs-lookup"><span data-stu-id="3a21c-106">In an SharePoint Add-in model scenario, the AllowAppOnlyPolicy permission or a service account is used to allow the current user to execute operations they are not authorize to perform.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="3a21c-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="3a21c-107">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="3a21c-108">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для повышения привилегий в коде.</span><span class="sxs-lookup"><span data-stu-id="3a21c-108">As a rule of a thumb, we would like to provide the following high-level guidelines for elevating privileges in code.</span></span>

- <span data-ttu-id="3a21c-109">AllowAppOnlyPolicy не работает с</span><span class="sxs-lookup"><span data-stu-id="3a21c-109">AllowAppOnlyPolicy does not work with</span></span> 
    + <span data-ttu-id="3a21c-110">Поиск — Если целевой объект локальная версия SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-110">Search - if target is SharePoint On-Premises.</span></span> <span data-ttu-id="3a21c-111">SharePoint Online поддержка добавлена ([запись в блоге](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))</span><span class="sxs-lookup"><span data-stu-id="3a21c-111">SharePoint Online support for it has been added ([blog post](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))</span></span>
    + <span data-ttu-id="3a21c-112">Операции CSOM профиля пользователя, за исключением того, что можно использовать API обновления массового профилей пользователей с разрешениями только для приложений</span><span class="sxs-lookup"><span data-stu-id="3a21c-112">User Profile CSOM operations, except that the User Profile Bulk Update API can be used with app-only permissions</span></span>
    + <span data-ttu-id="3a21c-113">Обновление записей службы таксономии (запись) — чтение works **Примечание:** в следующих ситуациях, необходимо использовать учетную запись службы.</span><span class="sxs-lookup"><span data-stu-id="3a21c-113">Updating taxonomy service entries (write) - read works **Note:** In these scenarios you need to use a specific service account.</span></span>
- <span data-ttu-id="3a21c-114">AllowAppOnlyPolicy аналогично RunWithElevatedPrivileges, но не точно так же.</span><span class="sxs-lookup"><span data-stu-id="3a21c-114">AllowAppOnlyPolicy is similar to RunWithElevatedPrivileges, but not exactly the same.</span></span>
    + <span data-ttu-id="3a21c-115">AllowAppOnlyPolicy выполняет код на основании разрешения, предоставленные для SharePoint надстройки, не от имени другого пользователя, который имеет соответствующие разрешения на выполнение операции.</span><span class="sxs-lookup"><span data-stu-id="3a21c-115">AllowAppOnlyPolicy executes code based on the permissions granted to the SharePoint Add-in, not on behalf of another user who has the appropriate permissions to perform an operation.</span></span>

<span data-ttu-id="3a21c-116">Ниже приведен пример возвращает маркер политики приложения и использовать его для создания объекта контекста.</span><span class="sxs-lookup"><span data-stu-id="3a21c-116">Here is an example of returning an App Only Policy token and using it to create a context object.</span></span>

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

- <span data-ttu-id="3a21c-117">При использовании AllowAppOnlyPolicy, помните о работает только в размещенном у поставщика SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="3a21c-117">When using the AllowAppOnlyPolicy, keep in mind it only works in Provider-hosted SharePoint Add-ins.</span></span>
- <span data-ttu-id="3a21c-118">AllowAppOnlyPolicy не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="3a21c-118">AllowAppOnlyPolicy does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>
- <span data-ttu-id="3a21c-119">Учетные записи служб, определяются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-119">Service accounts are defined in SharePoint.</span></span>
    + <span data-ttu-id="3a21c-120">В клиента Office 365 в зависимости от функциональных возможностей у требований к коду, учетные записи служб может потребоваться лицензии Office 365, назначенные им.</span><span class="sxs-lookup"><span data-stu-id="3a21c-120">In an Office 365 tenancy, depending what functionality your code requirements have, the service accounts may need an Office 365 license assigned to them.</span></span>
    + <span data-ttu-id="3a21c-121">Можно создать учетные записи служб на отдельных основы надстройки SharePoint или использование одной учетной записи для всех SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="3a21c-121">You can create service accounts on a per SharePoint Add-in basis, or use a single account for all SharePoint Add-ins.</span></span>
    + <span data-ttu-id="3a21c-122">Создание понятными и описательными имен для учетных записей служб, можно легко отслеживать операций, выполняемых ими.</span><span class="sxs-lookup"><span data-stu-id="3a21c-122">Create clear and descriptive names for the service accounts so you can easily track the operations they perform.</span></span>
    
    <span data-ttu-id="3a21c-123">Например: Если надстройки SharePoint изменяет элементы списков, столбец Автор изменений для элементов списка отображается имя учетной записи службы, связанной с помощью надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-123">For example: If your SharePoint Add-in modifies list items, the Modified By column for the list items will display the name of the service account associated with the SharePoint Add-in.</span></span>

- <span data-ttu-id="3a21c-124">При проверке подлинности с помощью учетных записей служб, вы должны получить имя пользователя и пароль для учетной записи службы.</span><span class="sxs-lookup"><span data-stu-id="3a21c-124">When authenticating with service accounts, you must retrieve a user name and password for the service account.</span></span>
    + <span data-ttu-id="3a21c-125">Приведенный ниже фрагмент кода иллюстрирует, используя имя пользователя и пароль для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3a21c-125">The code snippet below illustrates using a user name and password to authenticate.</span></span>
    + <span data-ttu-id="3a21c-126">Будьте внимательны для хранения и извлечения имя пользователя и пароль безопасным образом.</span><span class="sxs-lookup"><span data-stu-id="3a21c-126">Take care to store and retrieve the user name and password in a secure fashion.</span></span>

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {
    
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<a name="options-to-elevate-permissions"></a><span data-ttu-id="3a21c-127">Параметры, чтобы повысить уровень разрешений</span><span class="sxs-lookup"><span data-stu-id="3a21c-127">Options to elevate permissions</span></span>
------------------------------

<span data-ttu-id="3a21c-128">У вас есть две возможности повышения уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="3a21c-128">You have a couple of options to elevate permissions.</span></span>

- <span data-ttu-id="3a21c-129">OAuth (AllowAppOnlyPolicy)</span><span class="sxs-lookup"><span data-stu-id="3a21c-129">OAuth (AllowAppOnlyPolicy)</span></span>
    + <span data-ttu-id="3a21c-130">S2S (sub вариант)</span><span class="sxs-lookup"><span data-stu-id="3a21c-130">S2S (sub option)</span></span>
    + <span data-ttu-id="3a21c-131">ACS (sub вариант)</span><span class="sxs-lookup"><span data-stu-id="3a21c-131">ACS (sub option)</span></span>
- <span data-ttu-id="3a21c-132">Учетная запись службы</span><span class="sxs-lookup"><span data-stu-id="3a21c-132">Service Account</span></span>
    + <span data-ttu-id="3a21c-133">Удаленно размещенных кода (пример: Azure WebJob)</span><span class="sxs-lookup"><span data-stu-id="3a21c-133">Remotely hosted code (Example: Azure WebJob)</span></span>

<a name="oauth-allowapponlypolicy"></a><span data-ttu-id="3a21c-134">OAuth (AllowAppOnlyPolicy)</span><span class="sxs-lookup"><span data-stu-id="3a21c-134">OAuth (AllowAppOnlyPolicy)</span></span>
--------------------------
<span data-ttu-id="3a21c-135">В этом параметре AllowAppOnlyPolicy задано значение true в элемент AppPermissionRequests и разрешения, заданный в манифесте добавить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-135">In this option the AllowAppOnlyPolicy is set to true in the AppPermissionRequests element and permissions are set in the SharePoint Add-in manifest.</span></span> <span data-ttu-id="3a21c-136">OAuth используется для получения маркера доступа, чтобы разрешить надстройки SharePoint для выполнения операций, имеющий разрешения на выполнение.</span><span class="sxs-lookup"><span data-stu-id="3a21c-136">OAuth is used to return access tokens to allow the SharePoint Add-in to execute operations it has permissions to perform.</span></span>

<span data-ttu-id="3a21c-137">**Параметр sub S2S**</span><span class="sxs-lookup"><span data-stu-id="3a21c-137">**S2S sub option**</span></span>

<span data-ttu-id="3a21c-138">S2S sub параметр работает только в локальной среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-138">The S2S sub option only works in on-premises SharePoint environments.</span></span>

<span data-ttu-id="3a21c-139">При проверке подлинности с помощью OAuth в сценарии S2S метод **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** используется для получения маркера доступа для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-139">When authenticating via OAuth in an S2S scenario the **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** method is used to return the access token for the SharePoint Add-in.</span></span>  <span data-ttu-id="3a21c-140">Маркер доступа позволяет надстройки SharePoint для выполнения любых операций, предоставленные надстройки SharePoint в манифесте добавить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-140">The access token allows the SharePoint Add-in to perform any operations the SharePoint Add-in is granted in the SharePoint Add-in manifest.</span></span>

<span data-ttu-id="3a21c-141">Этот параметр не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="3a21c-141">This option does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>

<span data-ttu-id="3a21c-142">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="3a21c-142">**When is it a good fit?**</span></span>

<span data-ttu-id="3a21c-143">Если вам необходимо повысить уровень привилегий в сценарии SharePoint S2S это является хорошим выбором, поскольку этот параметр, для работы с S2S и очень просто реализовать.</span><span class="sxs-lookup"><span data-stu-id="3a21c-143">When you need to elevate privileges in a SharePoint S2S scenario this is a good option because this option works with S2S and is very easy to implement.</span></span>

<span data-ttu-id="3a21c-144">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="3a21c-144">**Getting Started**</span></span>

<span data-ttu-id="3a21c-145">Следующей статье показано, как использовать AllowAppOnlyPolicy с S2S.</span><span class="sxs-lookup"><span data-stu-id="3a21c-145">The following article demonstrates how to use AllowAppOnlyPolicy with S2S.</span></span>

- [<span data-ttu-id="3a21c-146">Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)</span><span class="sxs-lookup"><span data-stu-id="3a21c-146">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<span data-ttu-id="3a21c-147">**Параметр sub ACS**</span><span class="sxs-lookup"><span data-stu-id="3a21c-147">**ACS sub option**</span></span>

<span data-ttu-id="3a21c-148">Параметр sub ACS работать в средах Office 365 SharePoint и локальных.</span><span class="sxs-lookup"><span data-stu-id="3a21c-148">The ACS sub option work in on-premises and Office 365 SharePoint environments.</span></span>

<span data-ttu-id="3a21c-149">При проверке подлинности с помощью OAuth в сценарии ACS **TokenHelper::GetAppOnlyAccessTokenmethod** используется для получения маркера доступа для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-149">When authenticating via OAuth in an ACS scenario the **TokenHelper::GetAppOnlyAccessTokenmethod** is used to return the access token for the SharePoint Add-in.</span></span>  <span data-ttu-id="3a21c-150">Метод **TokenHelper::GetClientContextWithAccessToken** вызывается для возвращения контекста клиента, необходимые для выполнения каких-либо надстройки SharePoint имеет разрешения на выполнение операций, основанные на разрешения, предоставленные в манифесте добавить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-150">Then, the **TokenHelper::GetClientContextWithAccessToken** method is invoked to return the client context necessary to perform any operations the SharePoint Add-in has permission to do based on the permissions granted in the SharePoint Add-in manifest.</span></span>

<span data-ttu-id="3a21c-151">Этот параметр не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="3a21c-151">This option does not execute code on behalf of a user and therefore may not be appropriate for all scenarios.</span></span>

<span data-ttu-id="3a21c-152">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="3a21c-152">**When is it a good fit?**</span></span>

<span data-ttu-id="3a21c-153">Если вам необходимо повысить уровень привилегий в сценарии SharePoint ACS это является хорошим выбором, поскольку этот параметр, для работы с ACS и очень просто реализовать.</span><span class="sxs-lookup"><span data-stu-id="3a21c-153">When you need to elevate privileges in a SharePoint ACS scenario this is a good option because this option works with ACS and is very easy to implement.</span></span>  <span data-ttu-id="3a21c-154">Этот параметр используется подходит, если у вас есть в локальной среде SharePoint, имеющей отношения доверия с ACS.</span><span class="sxs-lookup"><span data-stu-id="3a21c-154">This option is a good fit when you have an on-premises SharePoint environment that has an established trust with ACS.</span></span>  <span data-ttu-id="3a21c-155">Это единственным вариантом OAuth, когда у вас есть в среде Office 365 SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a21c-155">This is your only OAuth option when you have a Office 365 SharePoint environment.</span></span>

<span data-ttu-id="3a21c-156">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="3a21c-156">**Getting Started**</span></span>

<span data-ttu-id="3a21c-157">В следующей статье демонстрируется использование AllowAppOnlyPolicy с ACS.</span><span class="sxs-lookup"><span data-stu-id="3a21c-157">The following article demonstrates how to use AllowAppOnlyPolicy with ACS.</span></span>

- [<span data-ttu-id="3a21c-158">Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)</span><span class="sxs-lookup"><span data-stu-id="3a21c-158">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<a name="service-account"></a><span data-ttu-id="3a21c-159">Учетная запись службы</span><span class="sxs-lookup"><span data-stu-id="3a21c-159">Service Account</span></span>
---------------
<span data-ttu-id="3a21c-160">В этом шаблоне класс SharePointOnlineCredentials используется для установки контекста пользователя, который выполняет код.</span><span class="sxs-lookup"><span data-stu-id="3a21c-160">In this pattern, the SharePointOnlineCredentials class is used to establish the context of a user that executes code.</span></span>

<span data-ttu-id="3a21c-161">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="3a21c-161">**When is it a good fit?**</span></span>

<span data-ttu-id="3a21c-162">Для выполнения кода от имени определенного пользователя (учетная запись службы) это является хорошим выбором, так как он выполняет действия на пользователя (учетная запись службы) и разрешений SharePoint надстройки.</span><span class="sxs-lookup"><span data-stu-id="3a21c-162">When you need to execute code on behalf of a specific user (service account) this is a good option because it performs actions on the user's (service account) and the SharePoint Add-in's permissions.</span></span>

<span data-ttu-id="3a21c-163">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="3a21c-163">**Getting Started**</span></span>

<span data-ttu-id="3a21c-164">В следующей статье описывается, как класс SharePointOnlineCredentials используется для установки контекста пользователя, который выполняет код.</span><span class="sxs-lookup"><span data-stu-id="3a21c-164">The following article demonstrates how the SharePointOnlineCredentials class is used to establish the context of a user that executes code.</span></span>

- [<span data-ttu-id="3a21c-165">Начало работы по построению WebJobs Azure («задания таймера») для Office 365 сайтов (раздел сведения о выполнении проверки подлинности) - статья блога Zimmergren Тобиаса</span><span class="sxs-lookup"><span data-stu-id="3a21c-165">Getting Started with building Azure WebJobs ("Timer Jobs") for your Office 365 sites (Authentication considerations section) - Tobias Zimmergren Blog Article</span></span>](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)

<a name="related-links"></a><span data-ttu-id="3a21c-166">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="3a21c-166">Related links</span></span>
=============
- [<span data-ttu-id="3a21c-167">Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)</span><span class="sxs-lookup"><span data-stu-id="3a21c-167">SharePoint 2013 App Only Policy Made Easy (Kirk Evans - MSDN Blog Post)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)
- [<span data-ttu-id="3a21c-168">Начало работы по построению WebJobs Azure («задания таймера») для Office 365 сайтов (раздел сведения о выполнении проверки подлинности) - статья блога Zimmergren Тобиаса</span><span class="sxs-lookup"><span data-stu-id="3a21c-168">Getting Started with building Azure WebJobs ("Timer Jobs") for your Office 365 sites (Authentication considerations section) - Tobias Zimmergren Blog Article</span></span>](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)
- [<span data-ttu-id="3a21c-169">Класс SharePointOnlineCredentials (документация по API MSDN)</span><span class="sxs-lookup"><span data-stu-id="3a21c-169">SharePointOnlineCredentials class (MSDN API Documentation)</span></span>](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.sharepointonlinecredentials.aspx)
- [<span data-ttu-id="3a21c-170">С помощью надстройки только аудио- и только разрешения с помощью запросов поиска в SharePoint Online — на статья блога Vesa Juvonen</span><span class="sxs-lookup"><span data-stu-id="3a21c-170">Using add-in only / app-only permissions with search queries in SharePoint Online - Vesa Juvonen Blog Article</span></span>](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)
- <span data-ttu-id="3a21c-171">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="3a21c-171">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="3a21c-172">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="3a21c-172">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="3a21c-173">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="3a21c-173">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="3a21c-174">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="3a21c-174">Related PnP samples</span></span>
===================

- [<span data-ttu-id="3a21c-175">Core.SimpleTimerJob (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="3a21c-175">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- <span data-ttu-id="3a21c-176">Примеры и содержимое в https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="3a21c-176">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="3a21c-177">Применимо к</span><span class="sxs-lookup"><span data-stu-id="3a21c-177">Applies to</span></span>
==========
- <span data-ttu-id="3a21c-178">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="3a21c-178">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="3a21c-179">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="3a21c-179">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="3a21c-180">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="3a21c-180">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="3a21c-181">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="3a21c-181">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
