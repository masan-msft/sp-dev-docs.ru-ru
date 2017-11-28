---
title: "Повышенными привилегиями в SharePoint надстройки"
ms.date: 11/03/2017
ms.openlocfilehash: 8102a3acc77efbc492c9ef7e62649851b5388954
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="elevated-privileges-in-sharepoint-add-ins"></a><span data-ttu-id="1a852-102">Повышенными привилегиями в SharePoint надстройки</span><span class="sxs-lookup"><span data-stu-id="1a852-102">Elevated privileges in SharePoint Add-ins</span></span>

<span data-ttu-id="1a852-103">Повысить уровень привилегий в SharePoint надстройки с помощью политики только для приложений или учетные записи служб.</span><span class="sxs-lookup"><span data-stu-id="1a852-103">Use the app-only policy or service accounts to elevate privileges in SharePoint Add-ins.</span></span>

<span data-ttu-id="1a852-104">_**Применимо к:** приложений для SharePoint | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="1a852-104">_**Applies to:** apps for SharePoint | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="1a852-105">Повысить уровень привилегий в решениях SharePoint надстройки и фермы используются различные методы.</span><span class="sxs-lookup"><span data-stu-id="1a852-105">Different methods are used to elevate privileges in SharePoint Add-ins and farm solutions.</span></span> <span data-ttu-id="1a852-106">Решения фермы повышать привилегии с помощью RunWithElevatedPrivileges(SPSecurity.CodeToRunElevated), которому принадлежит к модели объектов на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1a852-106">Farm solutions elevate privileges by using RunWithElevatedPrivileges(SPSecurity.CodeToRunElevated), which belongs to the SharePoint server-side object model.</span></span> <span data-ttu-id="1a852-107">Надстройки SharePoint использовать политики только для приложений или учетные записи служб.</span><span class="sxs-lookup"><span data-stu-id="1a852-107">SharePoint Add-ins use either the app-only policy or service accounts.</span></span>

<span data-ttu-id="1a852-108">Может потребоваться использовать повышенными привилегиями в надстройке при:</span><span class="sxs-lookup"><span data-stu-id="1a852-108">You might want to use elevated privileges in your add-in when:</span></span>

* <span data-ttu-id="1a852-109">Надстройка выполняет действия для пользователей, которые пользователи не имеют достаточное количество отдельных разрешений для выполнения.</span><span class="sxs-lookup"><span data-stu-id="1a852-109">Your add-in performs actions for users that the users don't have adequate individual permissions to complete.</span></span> <span data-ttu-id="1a852-110">Администраторы могут не назначить пользователям определенные разрешения из-за слишком высокого уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="1a852-110">Administrators might not assign users certain permissions because the permission level is too high.</span></span>

   <span data-ttu-id="1a852-111">Вашей организации, например реализовать решения, пользователи должны использовать для создания семейств веб-сайтов по подготовке семейства настраиваемых веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="1a852-111">Your organization might, for example, implement a custom site collection provisioning solution that users must use to create site collections.</span></span> <span data-ttu-id="1a852-112">Организации могут указать, что все новые семейства сайтов должен иметь определенные списки, типы контента или поля, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="1a852-112">Your organization might specify that all new site collections must have certain lists, content types, or fields associated with them.</span></span> <span data-ttu-id="1a852-113">Если пользователи создают семейство сайтов на свое усмотрение, они могут или может не забудьте для создания этих объектов на его нового семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="1a852-113">If users create site collections on their own, they might or might not remember to create these objects on their new site collection.</span></span> <span data-ttu-id="1a852-114">В этом сценарии пользователи создают семейство сайтов с помощью надстройки, но пользователям не назначены разрешения на создание семейств веб-сайтов по отдельности.</span><span class="sxs-lookup"><span data-stu-id="1a852-114">In this scenario, users create site collections by using the add-in, but users aren't individually assigned permissions to create site collections.</span></span>

* <span data-ttu-id="1a852-115">Надстройка не выполняется от имени любого пользователя; Например, для управления или управление процесс.</span><span class="sxs-lookup"><span data-stu-id="1a852-115">Your add-in is not acting on behalf of any user; for example, a governance or management process.</span></span>

## <a name="app-only-policy-authorization"></a><span data-ttu-id="1a852-116">Авторизация политики только для приложений</span><span class="sxs-lookup"><span data-stu-id="1a852-116">App-only policy authorization</span></span>

<span data-ttu-id="1a852-117">Политика только для приложений использует OAuth для проверки подлинности надстройки.</span><span class="sxs-lookup"><span data-stu-id="1a852-117">App-only policy uses OAuth to authenticate your add-in.</span></span> <span data-ttu-id="1a852-118">Когда надстройки используется политика только для приложений, SharePoint проверяет разрешения надстройка субъекта только.</span><span class="sxs-lookup"><span data-stu-id="1a852-118">When your add-in uses the app-only policy, SharePoint checks the permissions of the add-in principal only.</span></span> <span data-ttu-id="1a852-119">Это разрешений, предоставленных для надстройки.</span><span class="sxs-lookup"><span data-stu-id="1a852-119">These are the permissions that were granted to the add-in.</span></span> <span data-ttu-id="1a852-120">Авторизация выполняется успешно, если надстройка имеет достаточные разрешения для выполнения задач, вне зависимости от разрешений, связанный с текущим пользователем.</span><span class="sxs-lookup"><span data-stu-id="1a852-120">Authorization succeeds if the add-in has sufficient permissions to perform the task, regardless of the permissions associated with the current user.</span></span> <span data-ttu-id="1a852-121">После успешного выполнения авторизации для добавления в возвращается маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="1a852-121">When authorization succeeds, an access token is returned to your add-in.</span></span> <span data-ttu-id="1a852-122">Добавьте в будет использовать этот маркер доступа для выполнения любых операций, необходимые для вашего кода.</span><span class="sxs-lookup"><span data-stu-id="1a852-122">Your add-in will use this access token to perform any operations required by your code.</span></span>

<span data-ttu-id="1a852-123">Для получения дополнительных сведений см [типы политик авторизации приложений в SharePoint 2013](https://msdn.microsoft.com/library/office/fp179892.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a852-123">For more information, see [App authorization policy types in SharePoint 2013](https://msdn.microsoft.com/library/office/fp179892.aspx).</span></span>

<span data-ttu-id="1a852-124">**Примечание:** Политика только для приложений доступен только для провайдера надстройками SharePoint хостингом надстроек, что доступ к хост-сети необходимо использовать для пользователя и политики приложения.</span><span class="sxs-lookup"><span data-stu-id="1a852-124">**Note:** The app-only policy is available only for provider-hosted add-ins. SharePoint-hosted add-ins that access the host web must use the user+app policy.</span></span>

<span data-ttu-id="1a852-125">Преимущества использования политики только для приложений в вашей надстройки include:</span><span class="sxs-lookup"><span data-stu-id="1a852-125">Benefits of using the app-only policy in your add-in include:</span></span>

* <span data-ttu-id="1a852-126">Необходимо предоставить отдельный пользовательской лицензии.</span><span class="sxs-lookup"><span data-stu-id="1a852-126">You do not need to grant a separate user license.</span></span> <span data-ttu-id="1a852-127">Учетные записи служб требуются отдельные пользовательской лицензии.</span><span class="sxs-lookup"><span data-stu-id="1a852-127">Service accounts require a separate user license.</span></span>

* <span data-ttu-id="1a852-128">Получить более детальный контроль над разрешениями, чем доступно с помощью учетных записей служб.</span><span class="sxs-lookup"><span data-stu-id="1a852-128">You get more granular control over permissions than is available with service accounts.</span></span> <span data-ttu-id="1a852-129">Например могут применять разрешения на полный доступ на веб-узел, который не возможно при использовании учетных записей служб.</span><span class="sxs-lookup"><span data-stu-id="1a852-129">For example, you can apply FullControl permissions on your web, which isn't possible when you use service accounts.</span></span>

<span data-ttu-id="1a852-130">Политика только для приложений нельзя использовать вместе с следующие интерфейсы API:</span><span class="sxs-lookup"><span data-stu-id="1a852-130">You can't use the app-only policy with the following APIs:</span></span>

* <span data-ttu-id="1a852-131">Профиль пользователя</span><span class="sxs-lookup"><span data-stu-id="1a852-131">User Profile</span></span>

* <span data-ttu-id="1a852-132">Поиск</span><span class="sxs-lookup"><span data-stu-id="1a852-132">Search</span></span>

* <span data-ttu-id="1a852-133">Таксономия (применяется только к сценариям, которые ведут к службе управляемых метаданных)</span><span class="sxs-lookup"><span data-stu-id="1a852-133">Taxonomy (this only applies to scenarios that write to the managed metadata service)</span></span>

<span data-ttu-id="1a852-134">Чтобы использовать политики только для приложений, сначала необходимо предоставить разрешения для надстройки с помощью appinv.aspx.</span><span class="sxs-lookup"><span data-stu-id="1a852-134">To use the app-only policy, you first must grant permissions to the add-in by using appinv.aspx.</span></span> <span data-ttu-id="1a852-135">Следующий код из файла AppManifest.xml показано, как установить разрешения для добавления в и политики только для приложений.</span><span class="sxs-lookup"><span data-stu-id="1a852-135">The following code from AppManifest.xml file shows how to set the app-only policy and the permissions for your add-in.</span></span>

```xml
 <AppPermissionRequests AllowAppOnlyPolicy="true">
   <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="FullControl" />
 </AppPermissionRequests>
```

<span data-ttu-id="1a852-136">С помощью политики только для приложений необходимо добавить в использовать авторизации низким или высоким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="1a852-136">Using the app-only policy requires that your add-in use either low-trust or high-trust authorization.</span></span> <span data-ttu-id="1a852-137">Политика не может применяться к междоменной библиотеки JavaScript SharePoint, которая предоставляет третий способ получения авторизованный доступ к ресурсам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1a852-137">The policy is not available with the SharePoint cross-domain JavaScript library, which is a third way of getting authorized access to SharePoint resources.</span></span>

### <a name="low-trust-authorization"></a><span data-ttu-id="1a852-138">Авторизации с низким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="1a852-138">Low-trust authorization</span></span>

<span data-ttu-id="1a852-139">Добавьте в можно использовать авторизации с низким уровнем доверия, при использовании Microsoft Azure Access Control Service (ACS) для установления отношения доверия между надстройка размещением у поставщика и узла Office 365 или в локальной ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1a852-139">Your add-in can use low-trust authorization when using the Microsoft Azure Access Control Service (ACS) to establish trust between your provider-hosted add-in and either your Office 365 site or your on-premises SharePoint farm.</span></span> <span data-ttu-id="1a852-140">Дополнительные сведения по [три системы авторизации для SharePoint 2013 надстройки](https://msdn.microsoft.com/en-us/library/office/dn790706.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a852-140">You can learn more at [Three authorization systems for SharePoint Add-ins 2013](https://msdn.microsoft.com/en-us/library/office/dn790706.aspx).</span></span> <span data-ttu-id="1a852-141">Чтобы получить ссылку на объект [ClientContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.clientcontext.aspx) , добавьте в выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1a852-141">To get a reference to the [ClientContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.clientcontext.aspx) object, your add-in should:</span></span>

1. <span data-ttu-id="1a852-142">Получите маркер доступа с помощью TokenHelper.GetAppOnlyAccessToken.</span><span class="sxs-lookup"><span data-stu-id="1a852-142">Get the access token by using TokenHelper.GetAppOnlyAccessToken.</span></span>

2. <span data-ttu-id="1a852-143">Используйте TokenHelper.GetClientContextWithAccessToken, чтобы получить объект ClientContext.</span><span class="sxs-lookup"><span data-stu-id="1a852-143">Use TokenHelper.GetClientContextWithAccessToken to get the ClientContext object.</span></span>

<span data-ttu-id="1a852-144">**Примечание:** Файл TokenHelper является исходный код, созданное инструменты разработчика Microsoft Office для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a852-144">**Note:** The TokenHelper file is source code that is generated by the Microsoft Office Developer Tools for Visual Studio.</span></span> <span data-ttu-id="1a852-145">Нет справочной документации по его не, но есть широкое комментарии в класс TokenHelper.</span><span class="sxs-lookup"><span data-stu-id="1a852-145">There is no reference documentation for it, but there are extensive comments in the TokenHelper class.</span></span> <span data-ttu-id="1a852-146">Чтобы просмотреть комментарии в коде, создания у поставщика надстройки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a852-146">To see the code comments, create a provider-hosted add-in in Visual Studio.</span></span>

<span data-ttu-id="1a852-147">**Примечание:** Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="1a852-147">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```cs
Uri siteUrl = new Uri(ConfigurationManager.AppSettings["MySiteUrl"]);
try
{
    // Connect to a site using an app-only token.
    string realm = TokenHelper.GetRealmFromTargetUrl(siteUrl);
    var token = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUrl.Authority, realm).AccessToken;

    using (var ctx = TokenHelper.GetClientContextWithAccessToken(siteUrl.ToString(), token))
    {
        // Perform operations on the ClientContext object, which uses the app-only token. 
    }
}
catch (Exception ex)
{
    Console.WriteLine("Error in execution: " + ex.Message);
}
```

### <a name="high-trust-authorization"></a><span data-ttu-id="1a852-148">Авторизации с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="1a852-148">High-trust authorization</span></span>

<span data-ttu-id="1a852-149">Если надстройка использует системы авторизации с высоким уровнем доверия (также известной как протокол S2S), он вызывает другой метод **TokenHelper** : **TokenHelper.GetS2SAccessTokenWithWindowsIdentity**.</span><span class="sxs-lookup"><span data-stu-id="1a852-149">If your add-in uses the high-trust authorization system (also known as S2S protocol), it calls a different **TokenHelper** method: **TokenHelper.GetS2SAccessTokenWithWindowsIdentity**.</span></span>

<span data-ttu-id="1a852-150">**Важные:** **TokenHelper.GetS2SAccessTokenWithWindowsIdentity** используется для них только для приложений и вызывает для пользователя и приложения.</span><span class="sxs-lookup"><span data-stu-id="1a852-150">**Important:** The **TokenHelper.GetS2SAccessTokenWithWindowsIdentity** is used for both app-only and user+app calls.</span></span> <span data-ttu-id="1a852-151">Второй параметр метод, который содержит удостоверение пользователя, определяет, какая политика используется.</span><span class="sxs-lookup"><span data-stu-id="1a852-151">The second parameter of the method, which holds the user identity, determines which policy is used.</span></span> <span data-ttu-id="1a852-152">Передайте **значение null,** чтобы с помощью политики только для приложений.</span><span class="sxs-lookup"><span data-stu-id="1a852-152">Pass **null** to use the app-only policy.</span></span>

## <a name="service-accounts"></a><span data-ttu-id="1a852-153">Учетные записи служб</span><span class="sxs-lookup"><span data-stu-id="1a852-153">Service accounts</span></span>

<span data-ttu-id="1a852-154">Используйте учетные записи служб повысить уровень привилегий для добавления в только в том случае, если политика только для приложений не предоставляет достаточные разрешения на выполнение задачи.</span><span class="sxs-lookup"><span data-stu-id="1a852-154">Use service accounts to elevate privileges for your add-in only when the app-only policy does not provide sufficient permissions to complete your task.</span></span> <span data-ttu-id="1a852-155">Кроме того в некоторых сценариях учетная запись пользователя является обязательным.</span><span class="sxs-lookup"><span data-stu-id="1a852-155">Also, in certain scenarios a user account is required.</span></span> <span data-ttu-id="1a852-156">Например необходимо использовать учетные записи служб, когда код работает с любой из следующих приложений-служб SharePoint:</span><span class="sxs-lookup"><span data-stu-id="1a852-156">For example, you need to use service accounts when your code works with any of the following SharePoint service applications:</span></span>

* <span data-ttu-id="1a852-157">Служба профилей пользователей с помощью клиентской объектной модели (CSOM)</span><span class="sxs-lookup"><span data-stu-id="1a852-157">User Profile service using the client-side object model (CSOM)</span></span>

* <span data-ttu-id="1a852-158">Служба управляемых метаданных</span><span class="sxs-lookup"><span data-stu-id="1a852-158">Managed metadata service</span></span>

* <span data-ttu-id="1a852-159">Поиск</span><span class="sxs-lookup"><span data-stu-id="1a852-159">Search</span></span>

<span data-ttu-id="1a852-160">При планировании использования учетных записей служб в надстройке, необходимо учитывайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1a852-160">When planning to use service accounts in your add-in, consider the following:</span></span>

* <span data-ttu-id="1a852-161">Учетные записи служб требуются отдельные пользовательской лицензии.</span><span class="sxs-lookup"><span data-stu-id="1a852-161">Service accounts require a separate user license.</span></span>

* <span data-ttu-id="1a852-162">Создайте либо одну учетную запись службы каждого надстройки или используйте одну учетную запись службы для всех надстроек в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1a852-162">Create either one service account per add-in, or use one service account for all add-ins in your SharePoint environment.</span></span>

* <span data-ttu-id="1a852-163">Во время проверки подлинности необходимо указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="1a852-163">You must supply the user name and password during authorization.</span></span> <span data-ttu-id="1a852-164">Убедитесь, учетные данные учетной записи службы, хранятся или безопасно извлечен.</span><span class="sxs-lookup"><span data-stu-id="1a852-164">Ensure service account credentials are stored or retrieved securely.</span></span>

* <span data-ttu-id="1a852-165">Прежде чем добавлять в можно выполнить действие на сайте, учетные записи служб сначала необходимо предоставить разрешение для доступа к сайту.</span><span class="sxs-lookup"><span data-stu-id="1a852-165">Before your add-in can perform an action on a site, service accounts first must be granted permission to access the site.</span></span>

<span data-ttu-id="1a852-166">**Примечание:** Надстройки, приобретенных у магазина Office нельзя использовать учетные записи служб.</span><span class="sxs-lookup"><span data-stu-id="1a852-166">**Note:** Add-ins purchased from the Office Store cannot use service accounts.</span></span>

<span data-ttu-id="1a852-167">Ниже показано, как выполнить проверку подлинности с помощью [SharePointOnlineCredentials](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.sharepointonlinecredentials.aspx) с учетной записью службы.</span><span class="sxs-lookup"><span data-stu-id="1a852-167">The following code shows how to authenticate by using [SharePointOnlineCredentials](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.sharepointonlinecredentials.aspx) with a service account.</span></span>

```cs
using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
{

    // Use default authentication mode.
    context.AuthenticationMode = ClientAuthenticationMode.Default;  

    // Specify the credentials for the service account.
    context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
}
```

## <a name="additional-resources"></a><span data-ttu-id="1a852-168">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1a852-168">Additional resources</span></span>

<span data-ttu-id="1a852-169">[Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="1a852-169">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>

<span data-ttu-id="1a852-170">[Add-in типы политик авторизации в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179892.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a852-170">[Add-in authorization policy types in SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179892.aspx).</span></span>

<span data-ttu-id="1a852-171">[Использовать сайт Office 365 SharePoint для авторизации у поставщика надстройки на сайте SharePoint в локальной](https://msdn.microsoft.com/en-us/library/office/dn155905.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a852-171">[Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site](https://msdn.microsoft.com/en-us/library/office/dn155905.aspx).</span></span>
