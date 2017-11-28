---
title: "Сведения о выполнении авторизации для клиентов, размещенных в средах Германии, Китай и правительственных \"мне Нравится\""
ms.date: 11/03/2017
ms.openlocfilehash: 537ab7cc5b7536ba977a9563639271ef5620559d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="authorization-considerations-for-tenants-hosted-in-the-germany-china-or-us-government-environments"></a><span data-ttu-id="843fa-102">Сведения о выполнении авторизации для клиентов, размещенных в средах Германии, Китай и правительственных "мне Нравится"</span><span class="sxs-lookup"><span data-stu-id="843fa-102">Authorization considerations for tenants hosted in the Germany, China or US Government environments</span></span>

<span data-ttu-id="843fa-103">Если клиент Office 365 размещено в среде, определенные как Германия, Китай или "мне Нравится" государственных среды, то нужен это в учетной записи при разработке для вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="843fa-103">When your Office 365 tenant is hosted in an specific environment like the Germany, China or US Government environments then you'll need to take this in account when you're developing against your tenant.</span></span> 

<span data-ttu-id="843fa-104">_**Применимо к:** Office 365, размещенных в средах Германии, Китай и правительственных "мне Нравится"_</span><span class="sxs-lookup"><span data-stu-id="843fa-104">_**Applies to:** Office 365 hosted in the Germany, China or US Government environments_</span></span>


## <a name="introduction"></a><span data-ttu-id="843fa-105">Введение</span><span class="sxs-lookup"><span data-stu-id="843fa-105">Introduction</span></span>
<span data-ttu-id="843fa-106"><a name="introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-106"></span></span>

<span data-ttu-id="843fa-107">Корпорация Майкрософт конкретных развертываний Office 365 в Германию, Китай и для государственных учреждений "мне Нравится" для удовлетворения соответствующих определенным правилам в тех областях.</span><span class="sxs-lookup"><span data-stu-id="843fa-107">Microsoft has specific Office 365 deployments in Germany, China and for US Government to fulfill the specific regulations for those areas.</span></span> <span data-ttu-id="843fa-108">Следующие ссылки предоставляют дополнительные контекста:</span><span class="sxs-lookup"><span data-stu-id="843fa-108">Below links provide more context:</span></span>
- [<span data-ttu-id="843fa-109">Office 365 Германия</span><span class="sxs-lookup"><span data-stu-id="843fa-109">Office 365 Germany</span></span>](https://technet.microsoft.com/en-us/library/mt793278.aspx)
- [<span data-ttu-id="843fa-110">Office 365 обслуживается 21Vianet (Китай)</span><span class="sxs-lookup"><span data-stu-id="843fa-110">Office 365 operated by 21Vianet (China)</span></span>](https://technet.microsoft.com/en-us/library/mt651782.aspx)
- [<span data-ttu-id="843fa-111">Office 365 государственных организаций США.</span><span class="sxs-lookup"><span data-stu-id="843fa-111">Office 365 US Government</span></span>](https://technet.microsoft.com/library/mt774581.aspx)

<span data-ttu-id="843fa-112">Если вы являетесь разработчиком целевого приложения для SharePoint Online, размещенных в этих средах then необходимо воспользоваться учетной записью, имеющей эти среды собственные выделенные конечные точки проверки подлинности Azure AD, как разработчик необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="843fa-112">If you are a developer targeting applications for SharePoint Online hosted in these environments then you'll need to take in account that these environments have their own dedicated Azure AD authentication endpoints that you as developer need to use.</span></span> <span data-ttu-id="843fa-113">Ниже главы поясняется, как использовать эти выделенного конечных точек для типичного параметров настройки SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="843fa-113">Below chapters explain how do use these dedicated endpoints for the typical SharePoint Online customization options.</span></span>

## <a name="using-azure-ad-to-authorize"></a><span data-ttu-id="843fa-114">С помощью Azure AD для авторизации</span><span class="sxs-lookup"><span data-stu-id="843fa-114">Using Azure AD to authorize</span></span>
<span data-ttu-id="843fa-115"><a name="usingazureadtoauthorize"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-115"></span></span>

### <a name="azure-ad-endpoints"></a><span data-ttu-id="843fa-116">Конечные точки Azure AD</span><span class="sxs-lookup"><span data-stu-id="843fa-116">Azure AD endpoints</span></span>
<span data-ttu-id="843fa-117"><a name="adendpoints"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-117"></span></span>

<span data-ttu-id="843fa-118">Когда приложению Azure AD для авторизации необходимо использовать правильный конечной точки.</span><span class="sxs-lookup"><span data-stu-id="843fa-118">When your Azure AD application needs to authorize it needs to use the correct endpoint.</span></span> <span data-ttu-id="843fa-119">Приведенной ниже таблице описаны конечных точек для использования в зависимости от того, где был определен приложения Azure AD:</span><span class="sxs-lookup"><span data-stu-id="843fa-119">Below table describes the endpoints to use depending on where your Azure AD application has been defined:</span></span>

|<span data-ttu-id="843fa-120">**Среда**</span><span class="sxs-lookup"><span data-stu-id="843fa-120">**Environment**</span></span>|<span data-ttu-id="843fa-121">**Конечная точка**</span><span class="sxs-lookup"><span data-stu-id="843fa-121">**Endpoint**</span></span>|
|:-----|:-----|
| <span data-ttu-id="843fa-122">Рабочая</span><span class="sxs-lookup"><span data-stu-id="843fa-122">Production</span></span> | <span data-ttu-id="843fa-123">https://Login.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="843fa-123">https://login.windows.net</span></span> |
| <span data-ttu-id="843fa-124">Германия</span><span class="sxs-lookup"><span data-stu-id="843fa-124">Germany</span></span> | <span data-ttu-id="843fa-125">https://Login.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="843fa-125">https://login.microsoftonline.de</span></span> |
| <span data-ttu-id="843fa-126">Китай</span><span class="sxs-lookup"><span data-stu-id="843fa-126">China</span></span> | <span data-ttu-id="843fa-127">https://Login.chinacloudapi.CN</span><span class="sxs-lookup"><span data-stu-id="843fa-127">https://login.chinacloudapi.cn</span></span> |
| <span data-ttu-id="843fa-128">Правительства США</span><span class="sxs-lookup"><span data-stu-id="843fa-128">US Government</span></span> | <span data-ttu-id="843fa-129">https://Login-US.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="843fa-129">https://login-us.microsoftonline.com</span></span> |

### <a name="using-pnp-to-authorize-using-azure-ad"></a><span data-ttu-id="843fa-130">С помощью PnP для авторизации с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="843fa-130">Using PnP to authorize using Azure AD</span></span>
<span data-ttu-id="843fa-131"><a name="adpnp"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-131"></span></span>

<span data-ttu-id="843fa-132">PnP [помощью класса AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) предлагает простой способ получить объект SharePoint ClientContext при использовании приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="843fa-132">The PnP [AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) offers an easy way to obtain an SharePoint ClientContext object when you're using an Azure AD application.</span></span> <span data-ttu-id="843fa-133">Затронутые методы были расширены с помощью дополнительного `AzureEnvironment` enum</span><span class="sxs-lookup"><span data-stu-id="843fa-133">The impacted methods have been extended with an optional `AzureEnvironment` enum</span></span>

```c#
/// <summary>
/// Enum to identify the supported Office 365 hosting environments
/// </summary>
public enum AzureEnvironment
{
    Production=0,
    PPE=1,
    China=2,
    Germany=3,
    USGovernment=4
}
```

<span data-ttu-id="843fa-134">Ниже фрагменте показано только приложения на авторизации, обратите внимание на то последним параметром в `GetAzureADAppOnlyAuthenticatedContext` метод:</span><span class="sxs-lookup"><span data-stu-id="843fa-134">Below snippet shows an app-only authorization, notice the last parameter in the `GetAzureADAppOnlyAuthenticatedContext` method:</span></span>
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "079d8797-cebc-4cda-a3e0-xxxx"; 
string pfxPassword = "my password";
ClientContext cc = new AuthenticationManager().GetAzureADAppOnlyAuthenticatedContext(siteUrl, 
            aadAppId, "contoso.onmicrosoft.de", @"C:\contoso.pfx", pfxPassword, AzureEnvironment.Germany);
```

<span data-ttu-id="843fa-135">Другой фрагмент, на котором отображается интерактивного пользователя для входа с помощью `GetAzureADNativeApplicationAuthenticatedContext` метод:</span><span class="sxs-lookup"><span data-stu-id="843fa-135">Another snippet is showing an interactive user login using the `GetAzureADNativeApplicationAuthenticatedContext` method:</span></span>

```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "ff76a9f4-430b-4ee4-8602-xxxx"; 
ClientContext cc = new AuthenticationManager().GetAzureADNativeApplicationAuthenticatedContext(siteUrl, 
            aadAppId, "https://contoso.com/test", environment: AzureEnvironment.Germany);
```

## <a name="using-azure-acs-to-authorize-your-sharepoint-add-in"></a><span data-ttu-id="843fa-136">С помощью Azure ACS для авторизации надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="843fa-136">Using Azure ACS to authorize your SharePoint add-in</span></span>
<span data-ttu-id="843fa-137"><a name="usingazureacs"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-137"></span></span>

<span data-ttu-id="843fa-138">При создании SharePoint надстроек они будут авторизации обычно низким уровнем доверия, зависит от Azure ACS как descrived в [создании SharePoint Add-ins, использующих авторизации с низким уровнем доверия](https://msdn.microsoft.com/en-us/library/office/dn790707.aspx).</span><span class="sxs-lookup"><span data-stu-id="843fa-138">When you create SharePoint add-ins they'll typically low-trust authorization which depends on Azure ACS as descrived in [Creating SharePoint Add-ins that use low-trust authorization](https://msdn.microsoft.com/en-us/library/office/dn790707.aspx).</span></span>


### <a name="azure-acs-endpoints"></a><span data-ttu-id="843fa-139">Конечные точки Azure ACS</span><span class="sxs-lookup"><span data-stu-id="843fa-139">Azure ACS endpoints</span></span>
<span data-ttu-id="843fa-140"><a name="endpointsacs"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-140"></span></span>


|<span data-ttu-id="843fa-141">**Среда**</span><span class="sxs-lookup"><span data-stu-id="843fa-141">**Environment**</span></span>|<span data-ttu-id="843fa-142">**Префикс конечной точки**</span><span class="sxs-lookup"><span data-stu-id="843fa-142">**Endpoint prefix**</span></span>|<span data-ttu-id="843fa-143">**Конечная точка**</span><span class="sxs-lookup"><span data-stu-id="843fa-143">**Endpoint**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="843fa-144">Рабочая</span><span class="sxs-lookup"><span data-stu-id="843fa-144">Production</span></span> | <span data-ttu-id="843fa-145">учетные записи</span><span class="sxs-lookup"><span data-stu-id="843fa-145">accounts</span></span> | <span data-ttu-id="843fa-146">AccessControl.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="843fa-146">accesscontrol.windows.net</span></span> |
| <span data-ttu-id="843fa-147">Германия</span><span class="sxs-lookup"><span data-stu-id="843fa-147">Germany</span></span> | <span data-ttu-id="843fa-148">для входа</span><span class="sxs-lookup"><span data-stu-id="843fa-148">login</span></span> | <span data-ttu-id="843fa-149">microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="843fa-149">microsoftonline.de</span></span> |
| <span data-ttu-id="843fa-150">Китай</span><span class="sxs-lookup"><span data-stu-id="843fa-150">China</span></span> | <span data-ttu-id="843fa-151">учетные записи</span><span class="sxs-lookup"><span data-stu-id="843fa-151">accounts</span></span> | <span data-ttu-id="843fa-152">AccessControl.chinacloudapi.CN</span><span class="sxs-lookup"><span data-stu-id="843fa-152">accesscontrol.chinacloudapi.cn</span></span> |
| <span data-ttu-id="843fa-153">Правительства США</span><span class="sxs-lookup"><span data-stu-id="843fa-153">US Government</span></span> | <span data-ttu-id="843fa-154">учетные записи</span><span class="sxs-lookup"><span data-stu-id="843fa-154">accounts</span></span> | <span data-ttu-id="843fa-155">AccessControl.Windows.NET</span><span class="sxs-lookup"><span data-stu-id="843fa-155">accesscontrol.windows.net</span></span> |

<span data-ttu-id="843fa-156">С помощью URL-адрес конечной точки этой модели ACS отформатированное как https:// + конечной точки префикс + / + конечной точки.</span><span class="sxs-lookup"><span data-stu-id="843fa-156">Using this model the ACS endpoint url to use is formatted like https:// + endpoint prefix + / + endpoint.</span></span> <span data-ttu-id="843fa-157">Поэтому URL-адрес для рабочей среды будет https://accounts.accesscontrol.windows.net, одно для Германии будет https://login.microsoftonline.de.</span><span class="sxs-lookup"><span data-stu-id="843fa-157">So the URL for production will be https://accounts.accesscontrol.windows.net, the one for Germany will be https://login.microsoftonline.de.</span></span>

### <a name="updating-tokenhelpercs-in-your-applications"></a><span data-ttu-id="843fa-158">Обновление tokenhelper.cs в приложениях</span><span class="sxs-lookup"><span data-stu-id="843fa-158">Updating tokenhelper.cs in your applications</span></span>
<span data-ttu-id="843fa-159"><a name="tokenhelperacs"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-159"></span></span>

<span data-ttu-id="843fa-160">При необходимости выполните SharePoint надстройки авторизации с помощью Azure ACS, а затем вы используете `tokenhelper.cs` (или `tokenhelper.vb`).</span><span class="sxs-lookup"><span data-stu-id="843fa-160">When you want to do SharePoint add-in authorization using Azure ACS then you're using `tokenhelper.cs` (or `tokenhelper.vb`).</span></span> <span data-ttu-id="843fa-161">Класс tokenhelper по умолчанию будет иметь жестко ссылки на конечные точки Azure ACS и методы для получения конечной точки службы ACS, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="843fa-161">The default tokenhelper class will have hardcoded references to the Azure ACS endpoints and methods to acquire the ACS endpoint as shown below:</span></span>

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.windows.net";

...
```

#### <a name="tokenhelpercs-updates-for-germany"></a><span data-ttu-id="843fa-162">Обновления Tokenhelper.cs для Германии</span><span class="sxs-lookup"><span data-stu-id="843fa-162">Tokenhelper.cs updates for Germany</span></span>
<span data-ttu-id="843fa-163">Обновление статические переменные `GlobalEndPointPrefix` и `AcsHostUrl` к значениям Германия Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="843fa-163">Update the static variables `GlobalEndPointPrefix` and `AcsHostUrl` to the Germany Azure ACS values.</span></span>

```C#
...

private static string GlobalEndPointPrefix = "login";
private static string AcsHostUrl = "microsoftonline.de";

...
```

#### <a name="tokenhelpercs-updates-for-china"></a><span data-ttu-id="843fa-164">Обновления Tokenhelper.cs для Китая</span><span class="sxs-lookup"><span data-stu-id="843fa-164">Tokenhelper.cs updates for China</span></span>
<span data-ttu-id="843fa-165">Обновление статические переменные `GlobalEndPointPrefix` и `AcsHostUrl` для Китая Azure ACS значений:</span><span class="sxs-lookup"><span data-stu-id="843fa-165">Update the static variables `GlobalEndPointPrefix` and `AcsHostUrl` to the China Azure ACS values:</span></span>

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.chinacloudapi.cn";

...
```

### <a name="using-pnp-to-authorize-your-add-in-using-azure-acs"></a><span data-ttu-id="843fa-166">С помощью PnP для авторизации надстройки с помощью Azure ACS</span><span class="sxs-lookup"><span data-stu-id="843fa-166">Using PnP to authorize your add-in using Azure ACS</span></span>
<span data-ttu-id="843fa-167"><a name="pnpacs"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-167"></span></span>

<span data-ttu-id="843fa-168">PnP [помощью класса AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) предлагает простой способ получить объект SharePoint ClientContext при работе с Azure ACS для авторизации.</span><span class="sxs-lookup"><span data-stu-id="843fa-168">The PnP [AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) offers an easy way to obtain an SharePoint ClientContext object when you're using Azure ACS to authorize.</span></span> <span data-ttu-id="843fa-169">Затронутые методы были расширены с помощью дополнительного `AzureEnvironment` enum</span><span class="sxs-lookup"><span data-stu-id="843fa-169">The impacted methods have been extended with an optional `AzureEnvironment` enum</span></span>

```c#
/// <summary>
/// Enum to identify the supported Office 365 hosting environments
/// </summary>
public enum AzureEnvironment
{
    Production=0,
    PPE=1,
    China=2,
    Germany=3,
    USGovernment=4
}
```

<span data-ttu-id="843fa-170">Ниже фрагменте показано только приложения на авторизации, обратите внимание на то последним параметром в `GetAppOnlyAuthenticatedContext` метод:</span><span class="sxs-lookup"><span data-stu-id="843fa-170">Below snippet shows an app-only authorization, notice the last parameter in the `GetAppOnlyAuthenticatedContext` method:</span></span>
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string acsAppId = "955c10f2-7072-47f8-8bc1-xxxxx"; 
string acsAppSecret = "jgTolmGXU9DW8hUKgletoxxxxx"; 
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext(siteUrl, acsAppId, 
                acsAppSecret, AzureEnvironment.Germany);
```


### <a name="additional-resources"></a><span data-ttu-id="843fa-171">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="843fa-171">Additional resources</span></span>
<span data-ttu-id="843fa-172"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="843fa-172"></span></span>

- [<span data-ttu-id="843fa-173">Ознакомьтесь с Office 365 Германия</span><span class="sxs-lookup"><span data-stu-id="843fa-173">Learn about Office 365 Germany</span></span>](https://support.office.com/en-US/article/Learn-about-Office-365-Germany-8a5a4bbc-667a-4cac-8769-d8ac9015db4c) 
- [<span data-ttu-id="843fa-174">Узнайте об Office 365, которой с 21Vianet (Китай)</span><span class="sxs-lookup"><span data-stu-id="843fa-174">Learn about Office 365 operated by 21Vianet (China)</span></span>](https://support.office.com/en-us/article/Learn-about-Office-365-operated-by-21Vianet-A8AB5061-3346-4DA0-BB7C-5260822B53AE)