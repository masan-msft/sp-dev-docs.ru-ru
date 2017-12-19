---
title: "Классификация «современный» сайты SharePoint"
description: "Настройка из него классификации сайта поля для современных сайтов SharePoint."
ms.date: 12/19/2017
ms.openlocfilehash: 8dbff0c128f96120a693a9341604b00616700e64
ms.sourcegitcommit: bf4bc1e80c6ef1a0ff479039ef9ae0ee84d5f6b4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="sharepoint-modern-sites-classification"></a><span data-ttu-id="10556-103">Классификация «современный» сайты SharePoint</span><span class="sxs-lookup"><span data-stu-id="10556-103">SharePoint "modern" sites classification</span></span>
<span data-ttu-id="10556-104">При создании «современный» сайтов в SharePoint Online, при необходимости можно выбрать «Классификация сайта» для определения чувствительности данные сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-104">When you create "modern" sites in SharePoint Online, you can optionally select a 'Site Classification' to define the sensitivity of your site data.</span></span> <span data-ttu-id="10556-105">Цель классификации сайтов — разрешить управление кластеры сайтов на основе их классификации из управления и соблюдения Перспектива, а также для автоматизации процессов управления на основе классификации сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-105">The goal of site classification is to allow managing clusters of sites based on their classification from a governance and compliance perspective, as well as to automate governance processes based on site classification.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10556-106">По умолчанию не установлен флажок «Классификации сайта» и необходимо настроить на уровне Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10556-106">The 'Site Classification' option is not enabled by default, and you need to configure it at the Azure AD level.</span></span>

## <a name="enabling-site-classification-in-your-tenant"></a><span data-ttu-id="10556-107">Включение «Классификации сайта» клиента</span><span class="sxs-lookup"><span data-stu-id="10556-107">Enabling 'Site Classification' in your tenant</span></span>

<span data-ttu-id="10556-108">Для максимальной эффективности «Классификации сайта» необходимо включить эту возможность на уровне Azure AD конечного клиента.</span><span class="sxs-lookup"><span data-stu-id="10556-108">In order to benefit of 'Site Classification' you need to enable this capability at the Azure AD level, in your target tenant.</span></span> <span data-ttu-id="10556-109">Если эта возможность включена, вы увидите дополнительные поля «Как sensititive — это данные?»</span><span class="sxs-lookup"><span data-stu-id="10556-109">Once you have enabled this capability, you will see an additional field 'How sensititive is your data?'</span></span> <span data-ttu-id="10556-110">При создании новых сайтов «современный».</span><span class="sxs-lookup"><span data-stu-id="10556-110">while creating new "modern" sites.</span></span> <span data-ttu-id="10556-111">На следующем рисунке видно, как выглядит в поле «Классификации сайта».</span><span class="sxs-lookup"><span data-stu-id="10556-111">In the following figure you can see how the 'Site Classification' field looks like.</span></span>

![Параметр «Классификации сайта» при создании «современный» сайта в SharePoint Online](media/modern-experiences/site-classification-ui.png)

<span data-ttu-id="10556-113">В приведенном ниже рисунке видно классификации, в заголовке «современный» сайта с выделением.</span><span class="sxs-lookup"><span data-stu-id="10556-113">While in the following figure, you can see the classification highlighted in the header of a "modern" site.</span></span>

![В заголовке «современный» сайта с выделением «Классификации сайта»](media/modern-experiences/site-classification-ui-output.png)

### <a name="enabling-site-classification-with-powershell"></a><span data-ttu-id="10556-115">Включение «Сайта классификации» с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="10556-115">Enabling 'Site Classification' with PowerShell</span></span>
<span data-ttu-id="10556-116">Чтобы включить функцию «Классификации сайта» может выполнять набор кода PowerShell, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="10556-116">To enable the 'Site Classification' capability you can execute a bunch of PowerShell code, like the one illustrated below.</span></span>

```ps
# Install the AzureAD Preview Module for PowerShell
Install-Module AzureADPreview

# Connect to Azure AD
Connect-AzureAD

# Create new directory setting and set initial values
$template = Get-AzureADDirectorySettingTemplate | where { $_.DisplayName -eq "Group.Unified" }

$setting = $template.CreateDirectorySetting()
$setting["UsageGuidelinesUrl"] = "https://aka.ms/sppnp"
$setting["ClassificationList"] = "HBI, MBI, LBI, GDPR"
$setting["DefaultClassification"] = "MBI"
New-AzureADDirectorySetting -DirectorySetting $setting

```

> [!NOTE]
> <span data-ttu-id="10556-117">Обратите внимание, что занимает while (по 1 час и более) имеют параметры, доступные в пользовательский Интерфейс Office 365.</span><span class="sxs-lookup"><span data-stu-id="10556-117">Please, consider that it takes a while (about 1 hour or more) to have the settings available in the UI of Office 365.</span></span>

<span data-ttu-id="10556-118">О фрагмент кода над текстом стоит сказать, что во время этой записи необходимо использовать предварительной версии AzureAD командлеты, но довольно скоро будет иметь возможность использовать с RTM-версией.</span><span class="sxs-lookup"><span data-stu-id="10556-118">About the code snippet above, it worth it to say that at the time of this writing you have to use the preview version of the AzureAD cmdlets, but pretty soon you will be able to use the RTM version.</span></span>
<span data-ttu-id="10556-119">После завершения установки командлеты AzureAD нужно просто подключиться к клиенту Azure AD конечного, которой резервное клиенту конечного SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="10556-119">Once you have installed the AzureAD cmdlets, you simply need to connect to the target Azure AD tenant, which is backing your target SharePoint Online tenant.</span></span>
<span data-ttu-id="10556-120">С помощью командлета _Get-AzureADDirectorySettingTemplate_ вы получите ссылку на «Установка шаблона» для «единой группы», которого является шаблон со _DisplayName_ из «Group.Unified».</span><span class="sxs-lookup"><span data-stu-id="10556-120">Using the _Get-AzureADDirectorySettingTemplate_ cmdlet you get a reference to the 'Setting Template' for the 'Unified Groups', which is the one with _DisplayName_ of 'Group.Unified'.</span></span>
<span data-ttu-id="10556-121">После шаблона, можно настроить параметры шаблона, создавая новые _DirectorySetting_ и предоставление значения параметров по словарю.</span><span class="sxs-lookup"><span data-stu-id="10556-121">Once you have the template, you can configure the settings of that template by creating a new _DirectorySetting_ and providing the setting values through a dictionary.</span></span>

<span data-ttu-id="10556-122">Основные параметры, с точки зрения «Классификации сайта» являются:</span><span class="sxs-lookup"><span data-stu-id="10556-122">The main settings, from a 'Site Classification' perspective are:</span></span>
* <span data-ttu-id="10556-123">**UsageGuidelinesUrl**: URL-адрес страницы, где объясняется параметры различных классификации.</span><span class="sxs-lookup"><span data-stu-id="10556-123">**UsageGuidelinesUrl**: the URL of a page where you can explain what are the different classification options.</span></span> <span data-ttu-id="10556-124">Ссылка на этой странице будет отображаться в форме создания сайта и в заголовке каждого секретная сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-124">A link to that page will show up in the site creation form and in the header of every classified site.</span></span>
* <span data-ttu-id="10556-125">**ClassificationList**: разделенный запятыми список значений для списка параметров «Классификации сайта».</span><span class="sxs-lookup"><span data-stu-id="10556-125">**ClassificationList**: a comma separated list of values for the 'Site Classification' options list.</span></span>
* <span data-ttu-id="10556-126">**DefaultClassification**: значение по умолчанию для «Классификации сайта».</span><span class="sxs-lookup"><span data-stu-id="10556-126">**DefaultClassification**: the default value for the 'Site Classification'.</span></span>

### <a name="enabling-site-classification-with-pnp-core-library"></a><span data-ttu-id="10556-127">Включение «Сайта классификации» с библиотекой PnP ядра</span><span class="sxs-lookup"><span data-stu-id="10556-127">Enabling 'Site Classification' with PnP Core Library</span></span>

<span data-ttu-id="10556-128">Другая возможность, которые необходимо включить функцию «Классификации сайта» — это использовать PnP основной библиотеки, содержащей несколько методов расширения для управления классификации в коде C#.</span><span class="sxs-lookup"><span data-stu-id="10556-128">Another option that you have to enable the 'Site Classification' capability is to leverage the PnP Core Library, which provides few extension methods to manage classification in C# code.</span></span>
<span data-ttu-id="10556-129">Например для включения «Классификации сайта» можно написать кода C#, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="10556-129">For example, to enable the 'Site Classification' you can write C# code like the one illustrated below.</span></span>

```C#
// Connect to the admin central of your tenant
using (var adminContext = new ClientContext("https://[tenant]-admin.sharepoint.com/"))
{
    // Provide a valid set of credentials
    adminContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Create a new instance of the Tenant class of CSOM
    var tenant = new Tenant(adminContext);

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    var accessToken = getAzureADAccessToken();

    // Define the list of classifications
    var newClassificationList = new List<String>();
    newClassificationList.Add("HBI");
    newClassificationList.Add("MBI");
    newClassificationList.Add("LBI");
    newClassificationList.Add("GDPR");

    // Use the PnP extension method to enable 'Site Classification'
    // Including a default classification value and a the URL to an informative page
    tenant.EnableSiteClassifications(accessToken, newClassificationList, "MBI", "http://aka.ms/OfficeDevPnP");
}

```

## <a name="updating-or-removing-site-classification-in-your-tenant"></a><span data-ttu-id="10556-130">Обновление или удаление «Сайта классификации» клиента</span><span class="sxs-lookup"><span data-stu-id="10556-130">Updating or Removing 'Site Classification' in your tenant</span></span>

<span data-ttu-id="10556-131">Как для включения «Сайта классификации», обновлении или удалении параметра можно выполнить с помощью PowerShell или PnP Библиотека базовых.</span><span class="sxs-lookup"><span data-stu-id="10556-131">As like as for enabling the 'Site Classification', updating or removing the setting can be done either using PowerShell or PnP Core Library.</span></span>

### <a name="updating-or-removing-site-classification-with-powershell"></a><span data-ttu-id="10556-132">Обновление или удаление «Веб-сайтов классификации» с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="10556-132">Updating or Removing 'Site Classification' with PowerShell</span></span>

<span data-ttu-id="10556-133">Если вам потребуется обновить параметры «Классификации сайта» после этого, можно использовать следующий фрагмент PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10556-133">If you need to update the 'Site Classification' settings afterwards, you can use the following PowerShell snippet.</span></span>

```PowerShell
# Connect to Azure AD
Connect-AzureAD

# Read current settings
(Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }).Values

# Update settings
$currentSettings = Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }
$currentSettings["UsageGuidelinesUrl"] = "https://aka.ms/sppnp"
$currentSettings["ClassificationList"] = "HBI, MBI, LBI, GDPR"
$currentSettings["DefaultClassification"] = "MBI"
Set-AzureADDirectorySetting -Id $currentSettings.Id -DirectorySetting $currentSettings
```

> [!NOTE]
> <span data-ttu-id="10556-134">Обратите внимание, что необходимое while (по 1 час и более) для настройки обновляются в пользовательский Интерфейс Office 365.</span><span class="sxs-lookup"><span data-stu-id="10556-134">Please, consider that it takes a while (about 1 hour or more) to have the settings updated in the UI of Office 365.</span></span> <span data-ttu-id="10556-135">Тем не менее его не следует быть большая проблема, так как не следует очень часто обновлять параметры «Классификации сайта».</span><span class="sxs-lookup"><span data-stu-id="10556-135">However, it shouldn't be a big issue, because you shouldn't update the 'Site Classification' settings very often.</span></span>

<span data-ttu-id="10556-136">Как вы видите, нужно просто поиск параметр папка со значением _DisplayName_ «Group.Unified», а затем обновите его значения параметров и применить изменения с помощью командлета _Set-AzureADDirectorySetting_ .</span><span class="sxs-lookup"><span data-stu-id="10556-136">As you can see, you simply need to search for the Directory Setting with a _DisplayName_ value of 'Group.Unified' and then you can update its setting values and apply the changes by using the _Set-AzureADDirectorySetting_ cmdlet.</span></span>

<span data-ttu-id="10556-137">Для удаления «Классификации сайта» можно использовать командлет _Remove-AzureADDirectorySetting_ , как в следующем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="10556-137">To remove a 'Site Classification' you can use the _Remove-AzureADDirectorySetting_ cmdlet, like in the following code snippet.</span></span>

```ps
# Delete settings
$currentSettings = Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }
Remove-AzureADDirectorySetting -Id $currentSettings.Id
```

### <a name="updating-or-removing-site-classification-with-pnp-core-library"></a><span data-ttu-id="10556-138">Обновление или удаление «Веб-сайтов классификации» с помощью PnP основной библиотеки</span><span class="sxs-lookup"><span data-stu-id="10556-138">Updating or Removing 'Site Classification' with PnP Core Library</span></span>

<span data-ttu-id="10556-139">Другая возможность, у вас есть является использование PnP Библиотека базовых.</span><span class="sxs-lookup"><span data-stu-id="10556-139">Another option that you have is to use the PnP Core Library.</span></span>
<span data-ttu-id="10556-140">Например для обновления «Классификации сайта» можно написать кода C#, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="10556-140">For example, to update the 'Site Classification' you can write C# code like the one illustrated below.</span></span>

```C#
// Connect to the admin central of your tenant
using (var adminContext = new ClientContext("https://[tenant]-admin.sharepoint.com/"))
{
    // Provide a valid set of credentials
    adminContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Create a new instance of the Tenant class of CSOM
    var tenant = new Tenant(adminContext);

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    var accessToken = getAzureADAccessToken();

    // Retrieve the current set of values for 'Site Classification'
    var classificationList = tenant.GetSiteClassificationList(accessToken);
    
    // And update it by adding a new value
    var updatedClassificationList = new List<String>(classificationList);
    updatedClassificationList.Add("TopSecret");

    // Update the 'Site Classification' settings accordingly
    tenant.UpdateSiteClassificationSettings(accessToken, updatedClassificationList, "MBI", "http://aka.ms/SharePointPnP");
}
```

<span data-ttu-id="10556-141">Кроме того чтобы отключить и удалить параметры «Классификации сайта», можно использовать фрагмент кода, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="10556-141">Moreover, in order to disable and remove the 'Site Classification' settings, you can use a code snippet like the following one.</span></span>

```C#
// Connect to the admin central of your tenant
using (var adminContext = new ClientContext("https://[tenant]-admin.sharepoint.com/"))
{
    // Provide a valid set of credentials
    adminContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Create a new instance of the Tenant class of CSOM
    var tenant = new Tenant(adminContext);

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    var accessToken = getAzureADAccessToken();

    // Disable the 'Site Classification' settings
    tenant.DisableSiteClassifications(accessToken);
}
```

## <a name="managing-the-classification-of-a-site"></a><span data-ttu-id="10556-142">Управление классификации сайта</span><span class="sxs-lookup"><span data-stu-id="10556-142">Managing the classification of a site</span></span>

<span data-ttu-id="10556-143">Значения классификации для сайта может читать или обновлены, более поздней версии для с помощью пользовательского интерфейса из SharePoint Online, как показано на следующем рисунке, изменив параметры «Сведения о сайта».</span><span class="sxs-lookup"><span data-stu-id="10556-143">The value of classification for a site can be read, or updated, later on using the UI of SharePoint Online, as you can see in the following figure, by editing the 'Site Information' settings.</span></span>

![Параметр «Классификации сайта» во время редактирования «Сведения о сайте» параметры «современный» сайта в SharePoint Online](media/modern-experiences/site-classification-update-ui.png)

### <a name="programmatically-reading-the-classification-of-a-site"></a><span data-ttu-id="10556-145">Программными средствами чтения с классификацией сайта</span><span class="sxs-lookup"><span data-stu-id="10556-145">Programmatically reading the classification of a site</span></span>

<span data-ttu-id="10556-146">С точки зрения разработчика можно использовать CSOM и REST API из SharePoint Online для чтения и записи значения классификации для определенного сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-146">From a developer's perspective, you can use CSOM and the REST API of SharePoint Online to read and write the value of classification for a specific site.</span></span> <span data-ttu-id="10556-147">На самом деле каждого семейства сайтов SharePoint Online имеет свойство _классификации_ , которые можно использовать для чтения с классификацией сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-147">In fact, every SharePoint Online site collection has the _Classification_ property that you can use to read the site classification.</span></span> 

<span data-ttu-id="10556-148">Здесь представлен фрагмент PowerShell для этого.</span><span class="sxs-lookup"><span data-stu-id="10556-148">Here you can see a PowerShell snippet to do that.</span></span>

```ps
# Delete settings
Connect-PnPOnline "https://[tenant].sharepoint.com/sites/[modernsite]" -Credentials [credentials]

$site = Get-PnPSite
$classificationValue = Get-PnPProperty -ClientObject $site -Property Classification
Write-Host $classificationValue
```

<span data-ttu-id="10556-149">Если требуется прочитать значение «Классификации сайта», с помощью службы REST, например в рамках среды SharePoint со стороны клиента веб-части, можно использовать следующие конечная точка REST:</span><span class="sxs-lookup"><span data-stu-id="10556-149">If you like to read the 'Site Classification' value using REST, for example within a SharePoint Framework client-side web part, you can use the following REST endpoint:</span></span>

```TEXT
https://[tenant].sharepoint.com/sites/[modernsite]/_api/site/Classification
```

<span data-ttu-id="10556-150">На основе классификации значения сайта, можно определить пользовательскую политику правил и автоматизации.</span><span class="sxs-lookup"><span data-stu-id="10556-150">Based on the classification value of a site, you can define automation and custom policy rules.</span></span>

<span data-ttu-id="10556-151">В PnP Библиотека базовых отсутствует метод расширения для объекта сайта из CSOM, что позволяет легко прочитать значение классификации сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-151">In the PnP Core Library there is an extension method for the Site object of CSOM, which allows you to easily read the classification value of a site.</span></span> <span data-ttu-id="10556-152">В следующем фрагменте кода можно узнать, как внедрить с помощью этого метода расширения.</span><span class="sxs-lookup"><span data-stu-id="10556-152">In the following code snippet you can see how to leverage this extension method.</span></span>

```C#
// Connect to the target site collectiion
using (var clientContext = new ClientContext("https://[tenant].sharepoint.com/sites/[modernsite]"))
{
    // Provide a valid set of credentials
    clientContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Read the current classification value
    var currentClassification = clientContext.Site.GetSiteClassification();
}
```

### <a name="programmatically-updating-the-classification-of-a-site"></a><span data-ttu-id="10556-153">Программное обновление классификации сайта</span><span class="sxs-lookup"><span data-stu-id="10556-153">Programmatically updating the classification of a site</span></span>

<span data-ttu-id="10556-154">Если целевой сайт «современный» связи, можно использовать свойство _классификации_ CSOM слишком обновление значения.</span><span class="sxs-lookup"><span data-stu-id="10556-154">If your target is a  "modern" communication site, you can use the _Classification_ property of CSOM to update the value, too.</span></span>

<span data-ttu-id="10556-155">Если целевой сайт группы «современный» и обновить значение классификации, следует использовать Microsoft Graph, поскольку со значением свойства _классификации_ CSOM просто реплицирует значение свойства _классификации_ в Office 365 В группе.</span><span class="sxs-lookup"><span data-stu-id="10556-155">If your target is a "modern" team site and you want to update the classification value, you should use the Microsoft Graph because the _Classification_ property of CSOM simply replicates the value of the _classification_ property of the Office 365 Group.</span></span>

> [!NOTE]
> <span data-ttu-id="10556-156">Подробные сведения о том, как обновить группу Office 365, с помощью Microsoft Graph в документе, [Обновление группы](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_update)можно найти Далее.</span><span class="sxs-lookup"><span data-stu-id="10556-156">You can find further details about how to update an Office 365 Group using the Microsoft Graph in the document [Update group](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_update).</span></span>

<span data-ttu-id="10556-157">Чтобы облегчить обновить классификацию сайта в существует PnP Библиотека базовых — это метод расширения, которое применяется для вас правом поведение, в зависимости от типа «современный» сайта.</span><span class="sxs-lookup"><span data-stu-id="10556-157">In order to make it easier for you to update the classification of a site, in the PnP Core Library there is an extension method that applies for you the right behavior, depending on the "modern" site type.</span></span> <span data-ttu-id="10556-158">В следующем фрагменте кода можно узнать, как использовать его.</span><span class="sxs-lookup"><span data-stu-id="10556-158">In the following code excerpt you can see how to use it.</span></span>

```C#
// Connect to the target site collectiion
using (var clientContext = new ClientContext("https://[tenant].sharepoint.com/sites/[modernsite]"))
{
    // Provide a valid set of credentials
    clientContext.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[name-of-your-credentials]");

    // Get an Azure AD Access Token using ADAL, MSAL, or whatever else you like
    // This is needed only if your target is a "modern" team site
    var accessToken = getAzureADAccessToken();

    // Update the classification value, where the accessToken is an optional argument
    clientContext.Site.SetSiteClassification("MBI", accessToken);

    // Read back the new classification value (it can take a while to get back the new value)
    var currentClassification = clientContext.Site.GetSiteClassification();
}
```
