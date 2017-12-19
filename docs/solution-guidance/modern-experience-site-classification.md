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
# <a name="sharepoint-modern-sites-classification"></a>Классификация «современный» сайты SharePoint
При создании «современный» сайтов в SharePoint Online, при необходимости можно выбрать «Классификация сайта» для определения чувствительности данные сайта. Цель классификации сайтов — разрешить управление кластеры сайтов на основе их классификации из управления и соблюдения Перспектива, а также для автоматизации процессов управления на основе классификации сайта.

> [!IMPORTANT]
> По умолчанию не установлен флажок «Классификации сайта» и необходимо настроить на уровне Azure AD.

## <a name="enabling-site-classification-in-your-tenant"></a>Включение «Классификации сайта» клиента

Для максимальной эффективности «Классификации сайта» необходимо включить эту возможность на уровне Azure AD конечного клиента. Если эта возможность включена, вы увидите дополнительные поля «Как sensititive — это данные?» При создании новых сайтов «современный». На следующем рисунке видно, как выглядит в поле «Классификации сайта».

![Параметр «Классификации сайта» при создании «современный» сайта в SharePoint Online](media/modern-experiences/site-classification-ui.png)

В приведенном ниже рисунке видно классификации, в заголовке «современный» сайта с выделением.

![В заголовке «современный» сайта с выделением «Классификации сайта»](media/modern-experiences/site-classification-ui-output.png)

### <a name="enabling-site-classification-with-powershell"></a>Включение «Сайта классификации» с помощью PowerShell
Чтобы включить функцию «Классификации сайта» может выполнять набор кода PowerShell, как показано ниже.

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
> Обратите внимание, что занимает while (по 1 час и более) имеют параметры, доступные в пользовательский Интерфейс Office 365.

О фрагмент кода над текстом стоит сказать, что во время этой записи необходимо использовать предварительной версии AzureAD командлеты, но довольно скоро будет иметь возможность использовать с RTM-версией.
После завершения установки командлеты AzureAD нужно просто подключиться к клиенту Azure AD конечного, которой резервное клиенту конечного SharePoint Online.
С помощью командлета _Get-AzureADDirectorySettingTemplate_ вы получите ссылку на «Установка шаблона» для «единой группы», которого является шаблон со _DisplayName_ из «Group.Unified».
После шаблона, можно настроить параметры шаблона, создавая новые _DirectorySetting_ и предоставление значения параметров по словарю.

Основные параметры, с точки зрения «Классификации сайта» являются:
* **UsageGuidelinesUrl**: URL-адрес страницы, где объясняется параметры различных классификации. Ссылка на этой странице будет отображаться в форме создания сайта и в заголовке каждого секретная сайта.
* **ClassificationList**: разделенный запятыми список значений для списка параметров «Классификации сайта».
* **DefaultClassification**: значение по умолчанию для «Классификации сайта».

### <a name="enabling-site-classification-with-pnp-core-library"></a>Включение «Сайта классификации» с библиотекой PnP ядра

Другая возможность, которые необходимо включить функцию «Классификации сайта» — это использовать PnP основной библиотеки, содержащей несколько методов расширения для управления классификации в коде C#.
Например для включения «Классификации сайта» можно написать кода C#, как показано ниже.

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

## <a name="updating-or-removing-site-classification-in-your-tenant"></a>Обновление или удаление «Сайта классификации» клиента

Как для включения «Сайта классификации», обновлении или удалении параметра можно выполнить с помощью PowerShell или PnP Библиотека базовых.

### <a name="updating-or-removing-site-classification-with-powershell"></a>Обновление или удаление «Веб-сайтов классификации» с помощью PowerShell

Если вам потребуется обновить параметры «Классификации сайта» после этого, можно использовать следующий фрагмент PowerShell.

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
> Обратите внимание, что необходимое while (по 1 час и более) для настройки обновляются в пользовательский Интерфейс Office 365. Тем не менее его не следует быть большая проблема, так как не следует очень часто обновлять параметры «Классификации сайта».

Как вы видите, нужно просто поиск параметр папка со значением _DisplayName_ «Group.Unified», а затем обновите его значения параметров и применить изменения с помощью командлета _Set-AzureADDirectorySetting_ .

Для удаления «Классификации сайта» можно использовать командлет _Remove-AzureADDirectorySetting_ , как в следующем фрагменте кода.

```ps
# Delete settings
$currentSettings = Get-AzureADDirectorySetting | where { $_.DisplayName -eq "Group.Unified" }
Remove-AzureADDirectorySetting -Id $currentSettings.Id
```

### <a name="updating-or-removing-site-classification-with-pnp-core-library"></a>Обновление или удаление «Веб-сайтов классификации» с помощью PnP основной библиотеки

Другая возможность, у вас есть является использование PnP Библиотека базовых.
Например для обновления «Классификации сайта» можно написать кода C#, как показано ниже.

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

Кроме того чтобы отключить и удалить параметры «Классификации сайта», можно использовать фрагмент кода, как показано ниже.

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

## <a name="managing-the-classification-of-a-site"></a>Управление классификации сайта

Значения классификации для сайта может читать или обновлены, более поздней версии для с помощью пользовательского интерфейса из SharePoint Online, как показано на следующем рисунке, изменив параметры «Сведения о сайта».

![Параметр «Классификации сайта» во время редактирования «Сведения о сайте» параметры «современный» сайта в SharePoint Online](media/modern-experiences/site-classification-update-ui.png)

### <a name="programmatically-reading-the-classification-of-a-site"></a>Программными средствами чтения с классификацией сайта

С точки зрения разработчика можно использовать CSOM и REST API из SharePoint Online для чтения и записи значения классификации для определенного сайта. На самом деле каждого семейства сайтов SharePoint Online имеет свойство _классификации_ , которые можно использовать для чтения с классификацией сайта. 

Здесь представлен фрагмент PowerShell для этого.

```ps
# Delete settings
Connect-PnPOnline "https://[tenant].sharepoint.com/sites/[modernsite]" -Credentials [credentials]

$site = Get-PnPSite
$classificationValue = Get-PnPProperty -ClientObject $site -Property Classification
Write-Host $classificationValue
```

Если требуется прочитать значение «Классификации сайта», с помощью службы REST, например в рамках среды SharePoint со стороны клиента веб-части, можно использовать следующие конечная точка REST:

```TEXT
https://[tenant].sharepoint.com/sites/[modernsite]/_api/site/Classification
```

На основе классификации значения сайта, можно определить пользовательскую политику правил и автоматизации.

В PnP Библиотека базовых отсутствует метод расширения для объекта сайта из CSOM, что позволяет легко прочитать значение классификации сайта. В следующем фрагменте кода можно узнать, как внедрить с помощью этого метода расширения.

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

### <a name="programmatically-updating-the-classification-of-a-site"></a>Программное обновление классификации сайта

Если целевой сайт «современный» связи, можно использовать свойство _классификации_ CSOM слишком обновление значения.

Если целевой сайт группы «современный» и обновить значение классификации, следует использовать Microsoft Graph, поскольку со значением свойства _классификации_ CSOM просто реплицирует значение свойства _классификации_ в Office 365 В группе.

> [!NOTE]
> Подробные сведения о том, как обновить группу Office 365, с помощью Microsoft Graph в документе, [Обновление группы](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_update)можно найти Далее.

Чтобы облегчить обновить классификацию сайта в существует PnP Библиотека базовых — это метод расширения, которое применяется для вас правом поведение, в зависимости от типа «современный» сайта. В следующем фрагменте кода можно узнать, как использовать его.

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
