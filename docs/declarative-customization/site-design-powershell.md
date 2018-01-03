---
title: "Командлеты PowerShell для макетов и скриптов сайтов SharePoint"
description: "Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell."
ms.date: 12/14/2017
ms.openlocfilehash: d28a487c20970973cd11a26532068b54c095d939
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a><span data-ttu-id="83188-103">Командлеты PowerShell для макетов и скриптов сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="83188-103">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="83188-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="83188-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="83188-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="83188-105">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="83188-106">Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83188-106">Use PowerShell cmdlets to create, retrieve, and remove site designs and site scripts.</span></span>

## <a name="getting-started"></a><span data-ttu-id="83188-107">Начало работы</span><span class="sxs-lookup"><span data-stu-id="83188-107">Getting started</span></span>

<span data-ttu-id="83188-108">Чтобы использовать командлеты PowerShell, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="83188-108">To run the PowerShell cmdlets for theme management, you'll need to do the following:</span></span>

1. <span data-ttu-id="83188-109">Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="83188-109">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="83188-110">Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="83188-110">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="83188-111">Подключитесь к клиенту SharePoint, следуя инструкциям в статье [Подключение к PowerShell в SharePoint Online]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx)).</span><span class="sxs-lookup"><span data-stu-id="83188-111">Follow the instructions at [Connect to SharePoint Online PowerShell]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx)) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="83188-112">Чтобы проверить настройки, попробуйте выполнить командлет **Get-SPOSiteScript**, считывающий текущий список скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-112">To verify your setup, try using the **Get-SPOSiteScript** cmdlet to read the current list of site scripts.</span></span> <span data-ttu-id="83188-113">Если командлет выполнится без ошибок, то можно двигаться дальше.</span><span class="sxs-lookup"><span data-stu-id="83188-113">If the cmdlet runs and returns False with no errors, as shown in the following example, you're ready to proceed.</span></span>

## <a name="site-design-cmdlets"></a><span data-ttu-id="83188-114">Командлеты для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="83188-114">Site design cmdlets</span></span>

<span data-ttu-id="83188-115">Для управления макетами и скриптами сайтов в PowerShell доступны следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="83188-115">The following cmdlets are available for managing site themes from PowerShell:</span></span>

- <span data-ttu-id="83188-116">**Add-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="83188-116">**Add-SPOSiteDesign**</span></span>
- <span data-ttu-id="83188-117">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="83188-117">**Add-SPOSiteScript**</span></span>
- <span data-ttu-id="83188-118">**Get-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="83188-118">**Get-SPOSiteDesign**</span></span>
- <span data-ttu-id="83188-119">**Get-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="83188-119">**Get-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="83188-120">**Get-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="83188-120">**Get-SPOSiteScript**</span></span>
- <span data-ttu-id="83188-121">**Grant-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="83188-121">**Grant-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="83188-122">**Remove-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="83188-122">**Remove-SPOSiteDesign**</span></span>
- <span data-ttu-id="83188-123">**Remove-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="83188-123">**Remove-SPOSiteScript**</span></span>
- <span data-ttu-id="83188-124">**Revoke-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="83188-124">**Revoke-SPOSiteDesignRights**</span></span>

<!--
- **Set-SPOSiteDesign**
- **Set-SPOSiteScript**
-->

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a><span data-ttu-id="83188-125">Add-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="83188-125">Add-SPOSiteDesign</span></span>

<span data-ttu-id="83188-126">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="83188-126">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

```powershell
Add-SPOSiteDesign
  -Title <string>
  -WebTemplate <string>
  -SiteScripts <SPOSiteScriptPipeBind[]>
  [-Description <string>]
  [-PreviewImageUrl <string>]
  [-PreviewImageAltText <string>]
  [-IsDefault]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-127">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-127">Parameters</span></span>

|<span data-ttu-id="83188-128">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-128">Parameter</span></span>  | <span data-ttu-id="83188-129">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-129">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="83188-130">-Title</span><span class="sxs-lookup"><span data-stu-id="83188-130">title</span></span>                 | <span data-ttu-id="83188-131">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-131">The display name of the web site.</span></span> |
|<span data-ttu-id="83188-132">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="83188-132">-WebTemplate</span></span>           | <span data-ttu-id="83188-133">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="83188-133">Identifies which base template to add the design to.</span></span> <span data-ttu-id="83188-134">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="83188-134">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="83188-135">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="83188-135">-SiteScripts</span></span>           | <span data-ttu-id="83188-136">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-136">An array of one or more site scripts.</span></span> <span data-ttu-id="83188-137">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="83188-137">Each is identified by an ID.</span></span> <span data-ttu-id="83188-138">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="83188-138">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="83188-139">[-Description]</span><span class="sxs-lookup"><span data-stu-id="83188-139">Description</span></span>         | <span data-ttu-id="83188-140">Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-140">The display description of site design.</span></span> |
|<span data-ttu-id="83188-141">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="83188-141">[-PreviewImageUrl]</span></span>     | <span data-ttu-id="83188-142">URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="83188-142">The URL of a preview image.</span></span> <span data-ttu-id="83188-143">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="83188-143">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="83188-144">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="83188-144">[-PreviewImageAltText]</span></span> | <span data-ttu-id="83188-145">Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="83188-145">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="83188-146">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="83188-146">isDefault</span></span>           | <span data-ttu-id="83188-147">Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="83188-147">A switch that if provided, applies the site design to the default site template.</span></span> <!-- For more information see [Applying a site design to a default SharePoint template](site-design-apply-default-template.md) --> |

<span data-ttu-id="83188-148">Ниже представлен пример создания макета сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-148">Here's an example of creating a new site design.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview" `
  -IsDefault $false
```

## <a name="add-spositescript"></a><span data-ttu-id="83188-149">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="83188-149">**Add-SPOSiteScript**</span></span>

<span data-ttu-id="83188-150">Отправляет новый скрипт сайта в коллекцию для использования напрямую или в макете сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-150">Uploads a new site script to the gallery for use either directly or in a site design.</span></span> <span data-ttu-id="83188-151">Этот командлет будет поддерживать файл встроенного скрипта.</span><span class="sxs-lookup"><span data-stu-id="83188-151">This cmdlet will support inline script; file</span></span>

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-152">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-152">Parameters</span></span>

|<span data-ttu-id="83188-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-153">Parameter</span></span>     | <span data-ttu-id="83188-154">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-154">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-155">-Title</span><span class="sxs-lookup"><span data-stu-id="83188-155">title</span></span>       | <span data-ttu-id="83188-156">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-156">The display name of the web site.</span></span> |
| <span data-ttu-id="83188-157">-Content</span><span class="sxs-lookup"><span data-stu-id="83188-157">Content</span></span>     | <span data-ttu-id="83188-158">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="83188-158">JSON value that describes the script.</span></span> <span data-ttu-id="83188-159">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="83188-159">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="83188-160">-Description</span><span class="sxs-lookup"><span data-stu-id="83188-160">Description</span></span> | <span data-ttu-id="83188-161">Описание скрипта.</span><span class="sxs-lookup"><span data-stu-id="83188-161">A description of the error.</span></span> |

<span data-ttu-id="83188-162">Ниже приведен пример добавления сайта из приведенного ниже скрипта в файле.</span><span class="sxs-lookup"><span data-stu-id="83188-162">Here's an example of adding a new site from the following script in a file.</span></span>

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a><span data-ttu-id="83188-163">Get-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="83188-163">Get-SPOSiteDesign</span></span>

<span data-ttu-id="83188-164">Получает сведения о макетах сайтов, находящихся в клиенте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="83188-164">Gets details about site designs that are on the SharePoint tenant.</span></span> <span data-ttu-id="83188-165">Вы можете указать ИД макета сайта, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="83188-165">You can specify an ID of a specific site design to retrieve.</span></span> <span data-ttu-id="83188-166">Если параметры не указаны, отображаются сведения обо всех макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="83188-166">If there are no parameters listed, then details about all site designs are listed.</span></span>

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-167">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-167">Parameters</span></span>

|<span data-ttu-id="83188-168">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-168">Parameter</span></span>     | <span data-ttu-id="83188-169">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-169">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-170">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-170">Identity</span></span>  | <span data-ttu-id="83188-171">ИД макета сайта, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="83188-171">The ID of the site design to retrieve.</span></span> |

<span data-ttu-id="83188-172">Ниже приведены пример получения сведений о макете сайта и образец отклика.</span><span class="sxs-lookup"><span data-stu-id="83188-172">Here's an example and sample response of getting site design details.</span></span>

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863
```

```
Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a><span data-ttu-id="83188-173">Get-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="83188-173">Get-SPOSiteDesignRights</span></span>

<span data-ttu-id="83188-174">Выводит список субъектов и их прав на использование макета сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-174">Displays a list of principals and their rights for usage of the site design.</span></span> <span data-ttu-id="83188-175">С его помощью можно определить область действия макета сайта для пользователей клиента.</span><span class="sxs-lookup"><span data-stu-id="83188-175">This can be used to determine the scope that your site design has with users on the tenant.</span></span>

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-176">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-176">Parameters</span></span>

|<span data-ttu-id="83188-177">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-177">Parameter</span></span>     | <span data-ttu-id="83188-178">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-178">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-179">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-179">Identity</span></span>  | <span data-ttu-id="83188-180">ИД макета сайта для получения сведений об области.</span><span class="sxs-lookup"><span data-stu-id="83188-180">The ID of the site design to get scoping information.</span></span> |

<span data-ttu-id="83188-181">Ниже приведен пример получения сведений о правах для макета сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-181">Here's an example of getting the rights for a site design.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.sharepoint.com   View
```

## <a name="get-spositescript"></a><span data-ttu-id="83188-182">Get-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="83188-182">Get-SPOSiteScript</span></span>

<span data-ttu-id="83188-183">Выводит сведения об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="83188-183">Displays information about existing site scripts.</span></span> <span data-ttu-id="83188-184">Если параметры не указаны, этот командлет возвращает свойства **Id**, **Title**, **Description** и **Version** каждого скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-184">When no parameter is provided, this cmdlet returns the **Id**, **Title**, **Description**, and **Version** of each site script.</span></span> <span data-ttu-id="83188-185">Если указан ИД скрипта, этот командлет также возвращает свойство **Content**, содержащее код JSON скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-185">When a site script ID is provided, this cmdlet also returns the **Content**, which is the JSON of the site script.</span></span>

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-186">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-186">Parameters</span></span>

|<span data-ttu-id="83188-187">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-187">Parameter</span></span>     | <span data-ttu-id="83188-188">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-188">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-189">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-189">Identity</span></span>  | <span data-ttu-id="83188-190">ИД скрипта сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="83188-190">The ID of the site script to get information about.</span></span> |

## <a name="grant-spositedesignrights"></a><span data-ttu-id="83188-191">Grant-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="83188-191">Grant-SPOSiteDesignRights</span></span>

<span data-ttu-id="83188-192">Используется для применения разрешений к набору пользователей или группе безопасности. Определяет область видимости макета сайта в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="83188-192">Used to apply permissions to set of users or security group, effectively scoping visibility of site design in UX.</span></span> <span data-ttu-id="83188-193">По умолчанию макеты являются общедоступными.</span><span class="sxs-lookup"><span data-stu-id="83188-193">They start off public.</span></span> <span data-ttu-id="83188-194">Однако после установки разрешений доступ к ним смогут получать только те группы и пользователи, у которых есть разрешения.</span><span class="sxs-lookup"><span data-stu-id="83188-194">But once you set permissions, only those groups or users with permissions can access the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-195">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-195">Parameters</span></span>

|<span data-ttu-id="83188-196">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-196">Parameter</span></span>     | <span data-ttu-id="83188-197">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-197">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-198">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-198">Identity</span></span>  | <span data-ttu-id="83188-199">ИД макета сайта для получения сведений об области.</span><span class="sxs-lookup"><span data-stu-id="83188-199">The ID of the site design to get scoping information.</span></span> |
| <span data-ttu-id="83188-200">-Principals</span><span class="sxs-lookup"><span data-stu-id="83188-200">-Principals</span></span>  | <span data-ttu-id="83188-201">Один или несколько субъектов, для которых добавляются разрешения.</span><span class="sxs-lookup"><span data-stu-id="83188-201">One or more principles to add permissions for.</span></span> |
| <span data-ttu-id="83188-202">-Rights</span><span class="sxs-lookup"><span data-stu-id="83188-202">Rights</span></span>      | <span data-ttu-id="83188-203">Всегда задано значение **View**.</span><span class="sxs-lookup"><span data-stu-id="83188-203">Always set to the value **View**.</span></span> <span data-ttu-id="83188-204">Любой пользователь и любая группа с разрешениями на просмотр могут просматривать и использовать макет сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-204">Any user or group with view permissions can view and use the site design.</span></span> |

<span data-ttu-id="83188-205">В приведенном ниже примере показано, как предоставить права для макета сайта пользователю Nestor (пользователю на вымышленном сайте Contoso).</span><span class="sxs-lookup"><span data-stu-id="83188-205">Here's an example of how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.sharepoint.com" `
         -Rights View
```

## <a name="remove-spositedesign"></a><span data-ttu-id="83188-206">Remove-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="83188-206">Remove-SPOSiteDesign</span></span>

<span data-ttu-id="83188-207">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-207">Removes a site design.</span></span> <span data-ttu-id="83188-208">Он больше не будет отображаться в пользовательском интерфейсе создания сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-208">It will no longer appear in the UI for creating a new site.</span></span>

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-209">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-209">Parameters</span></span>

|<span data-ttu-id="83188-210">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-210">Parameter</span></span>     | <span data-ttu-id="83188-211">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-211">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-212">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-212">Identity</span></span>  | <span data-ttu-id="83188-213">ИД макета сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="83188-213">The ID of the site design to remove.</span></span> |

## <a name="remove-spositescript"></a><span data-ttu-id="83188-214">Remove-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="83188-214">Remove-SPOSiteScript</span></span>

<span data-ttu-id="83188-215">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-215">Removes a site script.</span></span> <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-216">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-216">Parameters</span></span>

|<span data-ttu-id="83188-217">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-217">Parameter</span></span>     | <span data-ttu-id="83188-218">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-218">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-219">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-219">Identity</span></span>  | <span data-ttu-id="83188-220">ИД скрипта сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="83188-220">The ID of the site script to remove.</span></span> |

## <a name="revoke-spositedesignrights"></a><span data-ttu-id="83188-221">Revoke-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="83188-221">Revoke-SPOSiteDesignRights</span></span>

<span data-ttu-id="83188-222">Отзывает права доступа к макету сайта для указанных субъектов.</span><span class="sxs-lookup"><span data-stu-id="83188-222">Revokes rights for specified principals from a site design.</span></span>

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="83188-223">Параметры</span><span class="sxs-lookup"><span data-stu-id="83188-223">Parameters</span></span>

|<span data-ttu-id="83188-224">Параметр</span><span class="sxs-lookup"><span data-stu-id="83188-224">Parameter</span></span>     | <span data-ttu-id="83188-225">Описание</span><span class="sxs-lookup"><span data-stu-id="83188-225">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="83188-226">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="83188-226">Identity</span></span>  | <span data-ttu-id="83188-227">ИД макета сайта, для которого требуется отозвать права.</span><span class="sxs-lookup"><span data-stu-id="83188-227">The ID of the site design from which to revoke rights.</span></span> |
| <span data-ttu-id="83188-228">-Principals</span><span class="sxs-lookup"><span data-stu-id="83188-228">-Principals</span></span>  | <span data-ttu-id="83188-229">Один или несколько субъектов, для которых требуется отозвать права доступа к указанному макету сайта.</span><span class="sxs-lookup"><span data-stu-id="83188-229">One or more principals to revoke rights on the specified site design.</span></span> |

<!--
## Set-SPOSiteDesign (TBD)

## Set-SPOSiteScript (TBD)
-->

<span data-ttu-id="83188-230">Разработчики могут также использовать [REST API](site-design-rest-api.md) SharePoint для управления темами.</span><span class="sxs-lookup"><span data-stu-id="83188-230">Developers can also use the SharePoint [REST API](site-design-rest-api.md) to handle theme management tasks.</span></span>

<span data-ttu-id="83188-231">Сведения об определении и сохранении тем см. в [справочнике по схеме JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="83188-231">For information about how themes are defined and stored, see [JSON schema reference](site-design-json-schema.md).</span></span>