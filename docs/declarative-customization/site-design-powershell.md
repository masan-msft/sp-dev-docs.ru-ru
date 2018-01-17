---
title: "Командлеты PowerShell для макетов и скриптов сайтов SharePoint"
description: "Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell."
ms.date: 12/14/2017
ms.openlocfilehash: e6f9f0324cb0879317d04aa9873ad168072073cc
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a><span data-ttu-id="806c2-103">Командлеты PowerShell для макетов и скриптов сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="806c2-103">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="806c2-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="806c2-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="806c2-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="806c2-105">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="806c2-106">Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="806c2-106">Use PowerShell cmdlets to create, retrieve, and remove site designs and site scripts.</span></span>

## <a name="getting-started"></a><span data-ttu-id="806c2-107">Начало работы</span><span class="sxs-lookup"><span data-stu-id="806c2-107">Getting started</span></span>

<span data-ttu-id="806c2-108">Чтобы использовать командлеты PowerShell, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="806c2-108">To run the PowerShell cmdlets for theme management, you'll need to do the following:</span></span>

1. <span data-ttu-id="806c2-109">Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="806c2-109">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="806c2-110">Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="806c2-110">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="806c2-111">Подключитесь к клиенту SharePoint, следуя инструкциям в статье [Подключение к PowerShell в SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx).</span><span class="sxs-lookup"><span data-stu-id="806c2-111">Follow the instructions at [Connect to SharePoint Online PowerShell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="806c2-112">Чтобы проверить настройки, попробуйте выполнить командлет **Get-SPOSiteScript**, считывающий текущий список скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-112">To verify your setup, try using the **Get-SPOSiteScript** cmdlet to read the current list of site scripts.</span></span> <span data-ttu-id="806c2-113">Если командлет выполнится без ошибок, то можно двигаться дальше.</span><span class="sxs-lookup"><span data-stu-id="806c2-113">If the cmdlet runs and returns False with no errors, as shown in the following example, you're ready to proceed.</span></span>

## <a name="site-design-cmdlets"></a><span data-ttu-id="806c2-114">Командлеты для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="806c2-114">Site design cmdlets</span></span>

<span data-ttu-id="806c2-115">Для управления макетами и скриптами сайтов в PowerShell доступны следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="806c2-115">The following cmdlets are available for managing site themes from PowerShell:</span></span>

- <span data-ttu-id="806c2-116">**Add-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="806c2-116">**Add-SPOSiteDesign**</span></span>
- <span data-ttu-id="806c2-117">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="806c2-117">**Add-SPOSiteScript**</span></span>
- <span data-ttu-id="806c2-118">**Get-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="806c2-118">**Get-SPOSiteDesign**</span></span>
- <span data-ttu-id="806c2-119">**Get-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="806c2-119">**Get-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="806c2-120">**Get-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="806c2-120">**Get-SPOSiteScript**</span></span>
- <span data-ttu-id="806c2-121">**Grant-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="806c2-121">**Grant-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="806c2-122">**Remove-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="806c2-122">**Remove-SPOSiteDesign**</span></span>
- <span data-ttu-id="806c2-123">**Remove-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="806c2-123">**Remove-SPOSiteScript**</span></span>
- <span data-ttu-id="806c2-124">**Revoke-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="806c2-124">**Revoke-SPOSiteDesignRights**</span></span>

<!--
- **Set-SPOSiteDesign**
- **Set-SPOSiteScript**
-->

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a><span data-ttu-id="806c2-125">Add-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="806c2-125">Add-SPOSiteDesign</span></span>

<span data-ttu-id="806c2-126">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="806c2-126">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

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

### <a name="parameters"></a><span data-ttu-id="806c2-127">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-127">Parameters</span></span>

|<span data-ttu-id="806c2-128">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-128">Parameter</span></span>  | <span data-ttu-id="806c2-129">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-129">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="806c2-130">-Title</span><span class="sxs-lookup"><span data-stu-id="806c2-130">title</span></span>                 | <span data-ttu-id="806c2-131">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-131">The display name of the web site.</span></span> |
|<span data-ttu-id="806c2-132">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="806c2-132">-WebTemplate</span></span>           | <span data-ttu-id="806c2-133">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="806c2-133">Identifies which base template to add the design to.</span></span> <span data-ttu-id="806c2-134">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="806c2-134">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="806c2-135">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="806c2-135">-SiteScripts</span></span>           | <span data-ttu-id="806c2-136">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-136">An array of one or more site scripts.</span></span> <span data-ttu-id="806c2-137">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="806c2-137">Each is identified by an ID.</span></span> <span data-ttu-id="806c2-138">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="806c2-138">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="806c2-139">[-Description]</span><span class="sxs-lookup"><span data-stu-id="806c2-139">Description</span></span>         | <span data-ttu-id="806c2-140">Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-140">The display description of site design.</span></span> |
|<span data-ttu-id="806c2-141">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="806c2-141">[-PreviewImageUrl]</span></span>     | <span data-ttu-id="806c2-142">URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="806c2-142">The URL of a preview image.</span></span> <span data-ttu-id="806c2-143">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="806c2-143">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="806c2-144">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="806c2-144">[-PreviewImageAltText]</span></span> | <span data-ttu-id="806c2-145">Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="806c2-145">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="806c2-146">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="806c2-146">isDefault</span></span>           | <span data-ttu-id="806c2-147">Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="806c2-147">A switch that if provided, applies the site design to the default site template.</span></span> <span data-ttu-id="806c2-148">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md)</span><span class="sxs-lookup"><span data-stu-id="806c2-148">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="806c2-149">Ниже представлен пример создания макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-149">Here's an example of creating a new site design.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview"
```

## <a name="add-spositescript"></a><span data-ttu-id="806c2-150">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="806c2-150">**Add-SPOSiteScript**</span></span>

<span data-ttu-id="806c2-151">Отправляет новый скрипт сайта для использования напрямую или в макете сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-151">Uploads a new site script for use either directly or in a site design.</span></span>

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-152">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-152">Parameters</span></span>

|<span data-ttu-id="806c2-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-153">Parameter</span></span>     | <span data-ttu-id="806c2-154">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-154">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-155">-Title</span><span class="sxs-lookup"><span data-stu-id="806c2-155">title</span></span>       | <span data-ttu-id="806c2-156">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-156">The display name of the web site.</span></span> |
| <span data-ttu-id="806c2-157">-Content</span><span class="sxs-lookup"><span data-stu-id="806c2-157">Content</span></span>     | <span data-ttu-id="806c2-158">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="806c2-158">JSON value that describes the script.</span></span> <span data-ttu-id="806c2-159">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="806c2-159">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="806c2-160">-Description</span><span class="sxs-lookup"><span data-stu-id="806c2-160">Description</span></span> | <span data-ttu-id="806c2-161">Описание скрипта.</span><span class="sxs-lookup"><span data-stu-id="806c2-161">A description of the error.</span></span> |

<span data-ttu-id="806c2-162">Ниже приведен пример добавления сайта из приведенного ниже скрипта в файле.</span><span class="sxs-lookup"><span data-stu-id="806c2-162">Here's an example of adding a new site from the following script in a file.</span></span>

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a><span data-ttu-id="806c2-163">Get-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="806c2-163">Get-SPOSiteDesign</span></span>

<span data-ttu-id="806c2-164">Получает сведения о макетах сайтов, находящихся в клиенте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="806c2-164">Gets details about site designs that are on the SharePoint tenant.</span></span> <span data-ttu-id="806c2-165">Вы можете указать ИД макета сайта, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="806c2-165">You can specify an ID of a specific site design to retrieve.</span></span> <span data-ttu-id="806c2-166">Если параметры не указаны, отображаются сведения обо всех макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="806c2-166">If there are no parameters listed, then details about all site designs are listed.</span></span>

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-167">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-167">Parameters</span></span>

|<span data-ttu-id="806c2-168">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-168">Parameter</span></span>     | <span data-ttu-id="806c2-169">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-169">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-170">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-170">Identity</span></span>  | <span data-ttu-id="806c2-171">ИД макета сайта, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="806c2-171">The ID of the site design to retrieve.</span></span> |

<span data-ttu-id="806c2-172">Ниже приведены пример получения сведений о макете сайта и образец отклика.</span><span class="sxs-lookup"><span data-stu-id="806c2-172">Here's an example and sample response of getting site design details.</span></span>

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863

Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a><span data-ttu-id="806c2-173">Get-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="806c2-173">Get-SPOSiteDesignRights</span></span>

<span data-ttu-id="806c2-174">Выводит список субъектов и их прав на использование макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-174">Displays a list of principals and their rights for usage of the site design.</span></span> <span data-ttu-id="806c2-175">С его помощью можно определить область действия макета сайта для пользователей клиента.</span><span class="sxs-lookup"><span data-stu-id="806c2-175">This can be used to determine the scope that your site design has with users on the tenant.</span></span>

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-176">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-176">Parameters</span></span>

|<span data-ttu-id="806c2-177">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-177">Parameter</span></span>     | <span data-ttu-id="806c2-178">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-178">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-179">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-179">Identity</span></span>  | <span data-ttu-id="806c2-180">ИД макета сайта для получения сведений об области.</span><span class="sxs-lookup"><span data-stu-id="806c2-180">The ID of the site design to get scoping information.</span></span> |

<span data-ttu-id="806c2-181">Ниже приведен пример получения сведений о правах для макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-181">Here's an example of getting the rights for a site design.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1

DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="get-spositescript"></a><span data-ttu-id="806c2-182">Get-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="806c2-182">Get-SPOSiteScript</span></span>

<span data-ttu-id="806c2-183">Выводит сведения об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="806c2-183">Displays information about existing site scripts.</span></span> <span data-ttu-id="806c2-184">Если параметры не указаны, этот командлет возвращает свойства **Id**, **Title**, **Description** и **Version** каждого скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-184">When no parameter is provided, this cmdlet returns the **Id**, **Title**, **Description**, and **Version** of each site script.</span></span> <span data-ttu-id="806c2-185">Если указан ИД скрипта, этот командлет также возвращает свойство **Content**, содержащее код JSON скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-185">When a site script ID is provided, this cmdlet also returns the **Content**, which is the JSON of the site script.</span></span>

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-186">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-186">Parameters</span></span>

|<span data-ttu-id="806c2-187">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-187">Parameter</span></span>     | <span data-ttu-id="806c2-188">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-188">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-189">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-189">Identity</span></span>  | <span data-ttu-id="806c2-190">Идентификатор скрипта сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="806c2-190">The ID of the site script to get information about.</span></span> |

<span data-ttu-id="806c2-191">В примере ниже показано, как получить сведения о скрипте для определенного идентификатора скрипта.</span><span class="sxs-lookup"><span data-stu-id="806c2-191">Here's an example that shows how to get script information for a specific script ID.</span></span>

```powershell
PS C:\scripts> Get-SPOSiteScript 07702c07-0485-426f-b710-4704241caad9

Id          : 07702c07-0485-426f-b710-4704241caad9
Title       : Contoso theme
Description :
Content     : {
                  "$schema": "schema.json",
                      "actions": [
                          {
                             "verb": "applyTheme",
                             "themeName": "Custom Cyan"
                          }
                      ],
                          "bindata": { },
                  "version": 1
              }
Version     : 1
```

## <a name="grant-spositedesignrights"></a><span data-ttu-id="806c2-192">Grant-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="806c2-192">Grant-SPOSiteDesignRights</span></span>

<span data-ttu-id="806c2-193">Используется для применения разрешений к набору пользователей или группе безопасности. Определяет область видимости макета сайта в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="806c2-193">Used to apply permissions to set of users or security group, effectively scoping visibility of site design in UX.</span></span> <span data-ttu-id="806c2-194">По умолчанию макеты являются общедоступными.</span><span class="sxs-lookup"><span data-stu-id="806c2-194">They start off public.</span></span> <span data-ttu-id="806c2-195">Однако после установки разрешений доступ к ним смогут получать только те группы и пользователи, у которых есть разрешения.</span><span class="sxs-lookup"><span data-stu-id="806c2-195">But once you set permissions, only those groups or users with permissions can access the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-196">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-196">Parameters</span></span>

|<span data-ttu-id="806c2-197">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-197">Parameter</span></span>     | <span data-ttu-id="806c2-198">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-198">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-199">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-199">Identity</span></span>  | <span data-ttu-id="806c2-200">ИД макета сайта для получения сведений об области.</span><span class="sxs-lookup"><span data-stu-id="806c2-200">The ID of the site design to get scoping information.</span></span> |
| <span data-ttu-id="806c2-201">-Principals</span><span class="sxs-lookup"><span data-stu-id="806c2-201">-Principals</span></span>  | <span data-ttu-id="806c2-202">Один или несколько субъектов, для которых добавляются разрешения.</span><span class="sxs-lookup"><span data-stu-id="806c2-202">One or more principles to add permissions for.</span></span> |
| <span data-ttu-id="806c2-203">-Rights</span><span class="sxs-lookup"><span data-stu-id="806c2-203">Rights</span></span>      | <span data-ttu-id="806c2-204">Всегда задано значение **View**.</span><span class="sxs-lookup"><span data-stu-id="806c2-204">Always set to the value **View**.</span></span> <span data-ttu-id="806c2-205">Любой пользователь и любая группа с разрешениями на просмотр могут просматривать и использовать макет сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-205">Any user or group with view permissions can view and use the site design.</span></span> |

<span data-ttu-id="806c2-206">В приведенном ниже примере показано, как предоставить права для макета сайта пользователю Nestor (пользователю на вымышленном сайте Contoso).</span><span class="sxs-lookup"><span data-stu-id="806c2-206">Here's an example of how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="remove-spositedesign"></a><span data-ttu-id="806c2-207">Remove-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="806c2-207">Remove-SPOSiteDesign</span></span>

<span data-ttu-id="806c2-208">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-208">Removes a site design.</span></span> <span data-ttu-id="806c2-209">Он больше не будет отображаться в пользовательском интерфейсе создания сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-209">It will no longer appear in the UI for creating a new site.</span></span>

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-210">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-210">Parameters</span></span>

|<span data-ttu-id="806c2-211">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-211">Parameter</span></span>     | <span data-ttu-id="806c2-212">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-212">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-213">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-213">Identity</span></span>  | <span data-ttu-id="806c2-214">Идентификатор макета сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="806c2-214">The ID of the site design to remove.</span></span> |

<span data-ttu-id="806c2-215">Ниже приведен пример удаления макета сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-215">Here's an example that shows how to remove a site design.</span></span>

```powershell

```

## <a name="remove-spositescript"></a><span data-ttu-id="806c2-216">Remove-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="806c2-216">Remove-SPOSiteScript</span></span>

<span data-ttu-id="806c2-217">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-217">Removes a site script.</span></span> <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-218">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-218">Parameters</span></span>

|<span data-ttu-id="806c2-219">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-219">Parameter</span></span>     | <span data-ttu-id="806c2-220">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-220">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-221">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-221">Identity</span></span>  | <span data-ttu-id="806c2-222">ИД скрипта сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="806c2-222">The ID of the site script to remove.</span></span> |

```powershell
C:\> Remove-SPOSiteDesign 21209d88-38de-4844-9823-f1f600a1179a
```

## <a name="revoke-spositedesignrights"></a><span data-ttu-id="806c2-223">Revoke-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="806c2-223">Revoke-SPOSiteDesignRights</span></span>

<span data-ttu-id="806c2-224">Отзывает права доступа к макету сайта для указанных субъектов.</span><span class="sxs-lookup"><span data-stu-id="806c2-224">Revokes rights for specified principals from a site design.</span></span>

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="806c2-225">Параметры</span><span class="sxs-lookup"><span data-stu-id="806c2-225">Parameters</span></span>

|<span data-ttu-id="806c2-226">Параметр</span><span class="sxs-lookup"><span data-stu-id="806c2-226">Parameter</span></span>     | <span data-ttu-id="806c2-227">Описание</span><span class="sxs-lookup"><span data-stu-id="806c2-227">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="806c2-228">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="806c2-228">Identity</span></span>  | <span data-ttu-id="806c2-229">ИД макета сайта, для которого требуется отозвать права.</span><span class="sxs-lookup"><span data-stu-id="806c2-229">The ID of the site design from which to revoke rights.</span></span> |
| <span data-ttu-id="806c2-230">-Principals</span><span class="sxs-lookup"><span data-stu-id="806c2-230">-Principals</span></span>  | <span data-ttu-id="806c2-231">Один или несколько субъектов, для которых требуется отозвать права доступа к указанному макету сайта.</span><span class="sxs-lookup"><span data-stu-id="806c2-231">One or more principals to revoke rights on the specified site design.</span></span> |

<span data-ttu-id="806c2-232">В примере ниже показано, как отозвать права на макет сайта для пользователя Nestor.</span><span class="sxs-lookup"><span data-stu-id="806c2-232">Here's an example that shows how to revoke rights to a site design for Nestor.</span></span>

```powershell
PS C:\> Revoke-SPOSiteDesignRights 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
   -Principals "nestorw@contoso.onmicrosoft.com"
```

<!--
## Set-SPOSiteDesign (TBD)

## Set-SPOSiteScript (TBD)
-->

## <a name="see-also"></a><span data-ttu-id="806c2-233">См. также</span><span class="sxs-lookup"><span data-stu-id="806c2-233">See also</span></span>

- [<span data-ttu-id="806c2-234">Справочные материалы по схеме JSON</span><span class="sxs-lookup"><span data-stu-id="806c2-234">JSON schema reference</span></span>](site-design-json-schema.md)
- <span data-ttu-id="806c2-235">[REST API](site-design-rest-api.md)Применение области к макету сайта](site-design-scoping.md)</span><span class="sxs-lookup"><span data-stu-id="806c2-235">[REST API](site-design-rest-api.md)Apply a scope to your site design](site-design-scoping.md)</span></span>
