---
title: "Командлеты PowerShell для макетов и скриптов сайтов SharePoint"
description: "Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell."
ms.date: 01/08/2018
ms.openlocfilehash: ed87e70844bd68acdef5e52d46c7619b020e85b2
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a><span data-ttu-id="a9168-103">Командлеты PowerShell для макетов и скриптов сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9168-103">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="a9168-104">Макеты и скрипты сайта выпущены в производство и доступны для общего использования.</span><span class="sxs-lookup"><span data-stu-id="a9168-104">Site designs and site scripts have been released to production and are available for general use.</span></span> 

<span data-ttu-id="a9168-105">Создавайте, получайте, обновляйте и удаляйте макеты и скрипты новых и уже существующих современных сайтов, используя командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9168-105">Use PowerShell cmdlets to create, retrieve, update, and remove site designs and site scripts to new and existing modern site collections.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a9168-106">Начало работы</span><span class="sxs-lookup"><span data-stu-id="a9168-106">Getting started</span></span>

<span data-ttu-id="a9168-107">Чтобы использовать командлеты PowerShell, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="a9168-107">To run the PowerShell cmdlets, you'll need to do the following:</span></span>

1. <span data-ttu-id="a9168-108">Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="a9168-108">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="a9168-109">Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="a9168-109">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="a9168-110">Подключитесь к клиенту SharePoint, следуя инструкциям в статье [Подключение к PowerShell в SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9168-110">Follow the instructions at [Connect to SharePoint Online PowerShell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="a9168-111">Чтобы проверить настройки, попробуйте выполнить командлет **Get-SPOSiteScript**, считывающий текущий список скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-111">To verify your setup, try using the **Get-SPOSiteScript** cmdlet to read the current list of site scripts.</span></span> <span data-ttu-id="a9168-112">Если командлет выполнится без ошибок, то можно двигаться дальше.</span><span class="sxs-lookup"><span data-stu-id="a9168-112">If the cmdlet runs and returns with no errors, you're ready to proceed.</span></span>

## <a name="site-design-cmdlets"></a><span data-ttu-id="a9168-113">Командлеты для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="a9168-113">Site design cmdlets</span></span>

<span data-ttu-id="a9168-114">Для управления макетами и скриптами сайтов в PowerShell доступны следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="a9168-114">The following cmdlets are available for managing site designs and site scripts from PowerShell:</span></span>

- <span data-ttu-id="a9168-115">**Add-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="a9168-115">**Add-SPOSiteDesign**</span></span>
- <span data-ttu-id="a9168-116">**Add-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="a9168-116">**Add-SPOSiteScript**</span></span>
- <span data-ttu-id="a9168-117">**Get-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="a9168-117">**Get-SPOSiteDesign**</span></span>
- <span data-ttu-id="a9168-118">**Get-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="a9168-118">**Get-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="a9168-119">**Get-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="a9168-119">**Get-SPOSiteScript**</span></span>
- <span data-ttu-id="a9168-120">**Grant-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="a9168-120">**Grant-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="a9168-121">**Invoke-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="a9168-121">**Invoke-SPOSiteDesign**</span></span>
- <span data-ttu-id="a9168-122">**Remove-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="a9168-122">**Remove-SPOSiteDesign**</span></span>
- <span data-ttu-id="a9168-123">**Remove-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="a9168-123">**Remove-SPOSiteScript**</span></span>
- <span data-ttu-id="a9168-124">**Revoke-SPOSiteDesignRights**</span><span class="sxs-lookup"><span data-stu-id="a9168-124">**Revoke-SPOSiteDesignRights**</span></span>
- <span data-ttu-id="a9168-125">**Set-SPOSiteDesign**</span><span class="sxs-lookup"><span data-stu-id="a9168-125">**Set-SPOSiteDesign**</span></span>
- <span data-ttu-id="a9168-126">**Set-SPOSiteScript**</span><span class="sxs-lookup"><span data-stu-id="a9168-126">**Set-SPOSiteScript**</span></span>

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a><span data-ttu-id="a9168-127">Add-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="a9168-127">Add-SPOSiteDesign</span></span>

<span data-ttu-id="a9168-128">Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a9168-128">Creates a new site design available to users when they create a new site from the SharePoint home page.</span></span>

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

### <a name="parameters"></a><span data-ttu-id="a9168-129">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-129">Parameters</span></span>

|<span data-ttu-id="a9168-130">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-130">Parameter</span></span>  | <span data-ttu-id="a9168-131">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-131">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="a9168-132">-Title</span><span class="sxs-lookup"><span data-stu-id="a9168-132">-Title</span></span>                 | <span data-ttu-id="a9168-133">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-133">The display name of the site design.</span></span> |
|<span data-ttu-id="a9168-134">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="a9168-134">-WebTemplate</span></span>           | <span data-ttu-id="a9168-135">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="a9168-135">Identifies which base template to add the design to.</span></span> <span data-ttu-id="a9168-136">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="a9168-136">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="a9168-137">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="a9168-137">-SiteScripts</span></span>           | <span data-ttu-id="a9168-138">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-138">An array of one or more site scripts.</span></span> <span data-ttu-id="a9168-139">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="a9168-139">Each is identified by an ID.</span></span> <span data-ttu-id="a9168-140">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="a9168-140">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="a9168-141">[-Description]</span><span class="sxs-lookup"><span data-stu-id="a9168-141">[-Description]</span></span>         | <span data-ttu-id="a9168-142">Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-142">The display description of site design.</span></span> |
|<span data-ttu-id="a9168-143">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="a9168-143">[-PreviewImageUrl]</span></span>     | <span data-ttu-id="a9168-144">URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="a9168-144">The URL of a preview image.</span></span> <span data-ttu-id="a9168-145">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="a9168-145">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="a9168-146">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="a9168-146">[-PreviewImageAltText]</span></span> | <span data-ttu-id="a9168-147">Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="a9168-147">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="a9168-148">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="a9168-148">[-IsDefault]</span></span>           | <span data-ttu-id="a9168-149">Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9168-149">A switch that if provided, applies the site design to the default site template.</span></span> <span data-ttu-id="a9168-150">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="a9168-150">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="a9168-151">Приведенный ниже код создает макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-151">The following example creates a new site design.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview"
```

## <a name="add-spositescript"></a><span data-ttu-id="a9168-152">Add-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="a9168-152">Add-SPOSiteScript</span></span>

<span data-ttu-id="a9168-153">Отправляет новый скрипт сайта для использования напрямую или в макете сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-153">Uploads a new site script for use either directly or in a site design.</span></span>

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-154">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-154">Parameters</span></span>

|<span data-ttu-id="a9168-155">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-155">Parameter</span></span>     | <span data-ttu-id="a9168-156">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-156">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-157">-Title</span><span class="sxs-lookup"><span data-stu-id="a9168-157">-Title</span></span>       | <span data-ttu-id="a9168-158">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-158">The display name of the site design.</span></span> |
| <span data-ttu-id="a9168-159">-Content</span><span class="sxs-lookup"><span data-stu-id="a9168-159">-Content</span></span>     | <span data-ttu-id="a9168-160">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="a9168-160">JSON value that describes the script.</span></span> <span data-ttu-id="a9168-161">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9168-161">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="a9168-162">-Description</span><span class="sxs-lookup"><span data-stu-id="a9168-162">-Description</span></span> | <span data-ttu-id="a9168-163">Описание скрипта.</span><span class="sxs-lookup"><span data-stu-id="a9168-163">A description of the script.</span></span> |

<span data-ttu-id="a9168-164">Приведенный ниже пример кода добавляет новый логотип сайта из приведенного ниже скрипта в файле.</span><span class="sxs-lookup"><span data-stu-id="a9168-164">The following example adds a new site from the following script in a file.</span></span>

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a><span data-ttu-id="a9168-165">Get-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="a9168-165">Get-SPOSiteDesign</span></span>

<span data-ttu-id="a9168-166">Получает сведения о макетах сайтов, находящихся в клиенте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a9168-166">Gets details about site designs that are on the SharePoint tenant.</span></span> <span data-ttu-id="a9168-167">Вы можете указать ИД макета сайта, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="a9168-167">You can specify an ID of a specific site design to retrieve.</span></span> <span data-ttu-id="a9168-168">Если параметры не указаны, отображаются сведения обо всех макетах сайтов.</span><span class="sxs-lookup"><span data-stu-id="a9168-168">If there are no parameters listed, then details about all site designs are listed.</span></span>

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-169">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-169">Parameters</span></span>

|<span data-ttu-id="a9168-170">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-170">Parameter</span></span>     | <span data-ttu-id="a9168-171">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-171">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-172">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="a9168-172">[-Identity]</span></span>  | <span data-ttu-id="a9168-173">ИД макета сайта, который требуется получить.</span><span class="sxs-lookup"><span data-stu-id="a9168-173">The ID of the site design to retrieve.</span></span> |

<span data-ttu-id="a9168-174">В примерах кода и отклика, приведенных ниже, показано получение сведений о макете сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-174">The following example and sample response shows how to get site design details.</span></span>

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863

Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a><span data-ttu-id="a9168-175">Get-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="a9168-175">Get-SPOSiteDesignRights</span></span>

<span data-ttu-id="a9168-176">Выводит список субъектов и их прав на использование макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-176">Displays a list of principals and their rights for usage of the site design.</span></span> <span data-ttu-id="a9168-177">С его помощью можно определить область действия макета сайта для пользователей клиента.</span><span class="sxs-lookup"><span data-stu-id="a9168-177">This can be used to determine the scope that your site design has with users on the tenant.</span></span>

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-178">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-178">Parameters</span></span>

|<span data-ttu-id="a9168-179">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-179">Parameter</span></span>     | <span data-ttu-id="a9168-180">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-180">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-181">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="a9168-181">[-Identity]</span></span>  | <span data-ttu-id="a9168-182">ИД макета сайта для получения сведений об области.</span><span class="sxs-lookup"><span data-stu-id="a9168-182">The ID of the site design to get scoping information.</span></span> |

<span data-ttu-id="a9168-183">Приведенный ниже пример кода обеспечивает получение прав для макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-183">The following example gets the rights for a site design.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1

DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="get-spositescript"></a><span data-ttu-id="a9168-184">Get-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="a9168-184">Get-SPOSiteScript</span></span>

<span data-ttu-id="a9168-185">Выводит сведения об имеющихся скриптах сайтов.</span><span class="sxs-lookup"><span data-stu-id="a9168-185">Displays information about existing site scripts.</span></span> <span data-ttu-id="a9168-186">Если параметры не указаны, этот командлет возвращает свойства **Id**, **Title**, **Description** и **Version** каждого скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-186">When no parameter is provided, this cmdlet returns the **Id**, **Title**, **Description**, and **Version** of each site script.</span></span> <span data-ttu-id="a9168-187">Если указан ИД скрипта, этот командлет также возвращает свойство **Content**, содержащее код JSON скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-187">When a site script ID is provided, this cmdlet also returns the **Content**, which is the JSON of the site script.</span></span>

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-188">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-188">Parameters</span></span>

|<span data-ttu-id="a9168-189">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-189">Parameter</span></span>     | <span data-ttu-id="a9168-190">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-190">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-191">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="a9168-191">[-Identity]</span></span>  | <span data-ttu-id="a9168-192">Идентификатор скрипта сайта, сведения о котором требуется получить.</span><span class="sxs-lookup"><span data-stu-id="a9168-192">The ID of the site script to get information about.</span></span> |

<span data-ttu-id="a9168-193">Приведенный ниже пример кода получает сведения о скрипте для определенного идентификатора скрипта.</span><span class="sxs-lookup"><span data-stu-id="a9168-193">The following example shows how to get script information for a specific script ID.</span></span>

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

## <a name="grant-spositedesignrights"></a><span data-ttu-id="a9168-194">Grant-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="a9168-194">Grant-SPOSiteDesignRights</span></span>

<span data-ttu-id="a9168-195">Используется для применения разрешений к набору пользователей или группе безопасности. Определяет область видимости макета сайта в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="a9168-195">Used to apply permissions to set of users or security group, effectively scoping visibility of site design in UX.</span></span> <span data-ttu-id="a9168-196">По умолчанию макеты являются общедоступными.</span><span class="sxs-lookup"><span data-stu-id="a9168-196">They start off public.</span></span> <span data-ttu-id="a9168-197">Однако после установки разрешений доступ к ним смогут получать только те группы и пользователи, у которых есть разрешения.</span><span class="sxs-lookup"><span data-stu-id="a9168-197">But once you set permissions, only those groups or users with permissions can access the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-198">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-198">Parameters</span></span>

|<span data-ttu-id="a9168-199">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-199">Parameter</span></span>     | <span data-ttu-id="a9168-200">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-200">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-201">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="a9168-201">[-Identity]</span></span>  | <span data-ttu-id="a9168-202">ИД макета сайта для получения сведений об области.</span><span class="sxs-lookup"><span data-stu-id="a9168-202">The ID of the site design to get scoping information.</span></span> |
| <span data-ttu-id="a9168-203">-Principals</span><span class="sxs-lookup"><span data-stu-id="a9168-203">-Principals</span></span>  | <span data-ttu-id="a9168-204">Один или несколько субъектов, для которых добавляются разрешения.</span><span class="sxs-lookup"><span data-stu-id="a9168-204">One or more principles to add permissions for.</span></span> |
| <span data-ttu-id="a9168-205">-Rights</span><span class="sxs-lookup"><span data-stu-id="a9168-205">-Rights</span></span>      | <span data-ttu-id="a9168-206">Всегда задано значение **View**.</span><span class="sxs-lookup"><span data-stu-id="a9168-206">Always set to the value **View**.</span></span> <span data-ttu-id="a9168-207">Любой пользователь и любая группа с разрешениями на просмотр могут просматривать и использовать макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-207">Any user or group with view permissions can view and use the site design.</span></span> |

<span data-ttu-id="a9168-208">Приведенный ниже пример кода предоставляет пользователю Nestor права на просмотр макета сайта (на вымышленном сайте Contoso).</span><span class="sxs-lookup"><span data-stu-id="a9168-208">The following example shows how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="invoke-spositedesign"></a><span data-ttu-id="a9168-209">Invoke-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="a9168-209">Invoke-SPOSiteDesign</span></span>

<span data-ttu-id="a9168-210">Применяет опубликованный макет сайта к указанному целевому объекту семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a9168-210">Applies a published site design to a specified site collection target.</span></span> <span data-ttu-id="a9168-211">Это позволяет применить макет сайта к существующему семейству веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a9168-211">This allows a site design to be applied to an existing site collection.</span></span>

```powershell
Invoke-SPOSiteDesign
  [-Identity]
  -WebUrl <string>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-212">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-212">Parameters</span></span>

|<span data-ttu-id="a9168-213">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-213">Parameter</span></span>     | <span data-ttu-id="a9168-214">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-214">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-215">-Identity</span><span class="sxs-lookup"><span data-stu-id="a9168-215">[-Identity]</span></span>       | <span data-ttu-id="a9168-216">Идентификатор макета сайта, который требуется применить.</span><span class="sxs-lookup"><span data-stu-id="a9168-216">The ID of the site design to delete.</span></span> |
| <span data-ttu-id="a9168-217">-WebUrl</span><span class="sxs-lookup"><span data-stu-id="a9168-217">webUrl</span></span>    | <span data-ttu-id="a9168-218">URL-адрес семейства веб-сайтов, к которому применяется макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-218">The Url of the site collection where the site design will be applied.</span></span>|

<span data-ttu-id="a9168-219">В примере ниже показано применение макета сайта, скрипт которого создает два списка, форматирует несколько столбцов, добавляет списки в структуру навигации веб-сайта, а затем соединяет сайт с существующим центральным сайтом.</span><span class="sxs-lookup"><span data-stu-id="a9168-219">The following example applies a site design whose script creates two lists, formats several of the columns, adds the lists to the site navigation, and then joins the site to an existing hub site.</span></span>

```powershell
C:\> Invoke-SPOSiteDesign -Identity 501z8c32-4147-44d4-8607-26c2f67cae82 -WebUrl "https://contoso.sharepoint.com/sites/projectgo”

Title                                             Outcome
----------------------------------------------    -------
Create or update list Project Activities          Success
Update list description                           Success
Create column Project Status                      Success
Create column Effort (days)                       Success
Set custom formatter for field Project Status     Success
Set custom formatter for field Effort (days)      Success
Create or update list Project Collateral          Success
Create column Due Date                            Success
Set custom formatter for field Due Date           Success
Add Project Activities to left nav                Success
Add Project Collateral to left nav                Success
Add to Hub Site                                   Success
```

## <a name="remove-spositedesign"></a><span data-ttu-id="a9168-220">Remove-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="a9168-220">Remove-SPOSiteDesign</span></span>

<span data-ttu-id="a9168-221">Удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-221">Removes a site design.</span></span> <span data-ttu-id="a9168-222">Он больше не будет отображаться в пользовательском интерфейсе создания сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-222">It will no longer appear in the UI for creating a new site.</span></span>

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-223">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-223">Parameters</span></span>

|<span data-ttu-id="a9168-224">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-224">Parameter</span></span>     | <span data-ttu-id="a9168-225">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-225">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-226">]</span><span class="sxs-lookup"><span data-stu-id="a9168-226">[-Identity]</span></span>  | <span data-ttu-id="a9168-227">Идентификатор макета сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="a9168-227">The ID of the site design to remove.</span></span> |

<span data-ttu-id="a9168-228">Приведенный ниже пример кода удаляет макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-228">The following example shows how to remove a site design.</span></span>

```powershell

```

## <a name="remove-spositescript"></a><span data-ttu-id="a9168-229">Remove-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="a9168-229">Remove-SPOSiteScript</span></span>

<span data-ttu-id="a9168-230">Удаляет скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-230">Removes a site script.</span></span> <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-231">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-231">Parameters</span></span>

|<span data-ttu-id="a9168-232">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-232">Parameter</span></span>     | <span data-ttu-id="a9168-233">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-233">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-234">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="a9168-234">[-Identity]</span></span>  | <span data-ttu-id="a9168-235">ИД скрипта сайта, который требуется удалить.</span><span class="sxs-lookup"><span data-stu-id="a9168-235">The ID of the site script to remove.</span></span> |

```powershell
C:\> Remove-SPOSiteDesign 21209d88-38de-4844-9823-f1f600a1179a
```

## <a name="revoke-spositedesignrights"></a><span data-ttu-id="a9168-236">Revoke-SPOSiteDesignRights</span><span class="sxs-lookup"><span data-stu-id="a9168-236">Revoke-SPOSiteDesignRights</span></span>

<span data-ttu-id="a9168-237">Отзывает права доступа к макету сайта для указанных субъектов.</span><span class="sxs-lookup"><span data-stu-id="a9168-237">Revokes rights for specified principals from a site design.</span></span>

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-238">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-238">Parameters</span></span>

|<span data-ttu-id="a9168-239">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-239">Parameter</span></span>     | <span data-ttu-id="a9168-240">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-240">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-241">[-Identity]</span><span class="sxs-lookup"><span data-stu-id="a9168-241">[-Identity]</span></span>  | <span data-ttu-id="a9168-242">ИД макета сайта, для которого требуется отозвать права.</span><span class="sxs-lookup"><span data-stu-id="a9168-242">The ID of the site design from which to revoke rights.</span></span> |
| <span data-ttu-id="a9168-243">-Principals</span><span class="sxs-lookup"><span data-stu-id="a9168-243">-Principals</span></span>  | <span data-ttu-id="a9168-244">Один или несколько субъектов, для которых требуется отозвать права доступа к указанному макету сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-244">One or more principals to revoke rights on the specified site design.</span></span> |

<span data-ttu-id="a9168-245">В приведенном ниже примере показано, как отозвать права на доступ к макету сайта для пользователя Nestor.</span><span class="sxs-lookup"><span data-stu-id="a9168-245">The following example shows how to revoke rights to a site design for Nestor.</span></span>

```powershell
PS C:\> Revoke-SPOSiteDesignRights 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
   -Principals "nestorw@contoso.onmicrosoft.com"
```

<!--
## Set-SPOSiteDesign (TBD)
Updates a previously uploaded site design.
## Set-SPOSiteScript (TBD)
Updates a previously uploaded site script.
-->

## <a name="set-spositedesign"></a><span data-ttu-id="a9168-246">Set-SPOSiteDesign</span><span class="sxs-lookup"><span data-stu-id="a9168-246">Set-SPOSiteDesign</span></span>

<span data-ttu-id="a9168-247">Обновляет загруженный ранее макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-247">Updates a previously uploaded site design.</span></span> 

```powershell
Set-SPOSiteDesign
  -Identity <SPOSiteDesignPipeBind[]>
  [-Title <string>]
  [-WebTemplate <string>]
  [-SiteScripts <SPOSiteScriptPipeBind[]>]
  [-Description <string>]
  [-PreviewImageUrl <string>]
  [-PreviewImageAltText <string>]
  [-IsDefault]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-248">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-248">Parameters</span></span>

|<span data-ttu-id="a9168-249">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-249">Parameter</span></span>  | <span data-ttu-id="a9168-250">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-250">Description</span></span>  |
|-----------|--------------|
|<span data-ttu-id="a9168-251">-Title</span><span class="sxs-lookup"><span data-stu-id="a9168-251">-Title</span></span>                 | <span data-ttu-id="a9168-252">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-252">The display name of the site design.</span></span> |
|<span data-ttu-id="a9168-253">-WebTemplate</span><span class="sxs-lookup"><span data-stu-id="a9168-253">-WebTemplate</span></span>           | <span data-ttu-id="a9168-254">Указывает, к какому базовому шаблону будет добавлен макет.</span><span class="sxs-lookup"><span data-stu-id="a9168-254">Identifies which base template to add the design to.</span></span> <span data-ttu-id="a9168-255">Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="a9168-255">Use the value **64** for the Team site template, and the value **68** for the Communication site template.</span></span> |
|<span data-ttu-id="a9168-256">-SiteScripts</span><span class="sxs-lookup"><span data-stu-id="a9168-256">-SiteScripts</span></span>           | <span data-ttu-id="a9168-257">Массив из одного или нескольких скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-257">An array of one or more site scripts.</span></span> <span data-ttu-id="a9168-258">Каждый из них определяется по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="a9168-258">Each is identified by an ID.</span></span> <span data-ttu-id="a9168-259">Скрипты будут выполняться в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="a9168-259">The scripts will run in the order listed.</span></span> |
|<span data-ttu-id="a9168-260">[-Description]</span><span class="sxs-lookup"><span data-stu-id="a9168-260">[-Description]</span></span>         | <span data-ttu-id="a9168-261">Отображаемое описание макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-261">The display description of site design.</span></span> |
|<span data-ttu-id="a9168-262">[-PreviewImageUrl]</span><span class="sxs-lookup"><span data-stu-id="a9168-262">[-PreviewImageUrl]</span></span>     | <span data-ttu-id="a9168-263">URL-адрес изображения для предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="a9168-263">The URL of a preview image.</span></span> <span data-ttu-id="a9168-264">Если он не указан, в SharePoint будет использоваться стандартное изображение.</span><span class="sxs-lookup"><span data-stu-id="a9168-264">If none is specified SharePoint will use a generic image.</span></span> |
|<span data-ttu-id="a9168-265">[-PreviewImageAltText]</span><span class="sxs-lookup"><span data-stu-id="a9168-265">[-PreviewImageAltText]</span></span> | <span data-ttu-id="a9168-266">Замещающий текст с описанием изображения для специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="a9168-266">The alt text description of the image for accessibility.</span></span> |
|<span data-ttu-id="a9168-267">[-IsDefault]</span><span class="sxs-lookup"><span data-stu-id="a9168-267">[-IsDefault]</span></span>           | <span data-ttu-id="a9168-268">Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9168-268">A switch that if provided, applies the site design to the default site template.</span></span> <span data-ttu-id="a9168-269">Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="a9168-269">For more information see [Customize a default site design](customize-default-site-design.md)</span></span> |

<span data-ttu-id="a9168-270">Приведенный ниже код обновляет созданный ранее макет сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-270">The following example updates a previously created site design.</span></span>

```powershell
C:\> Set-SPOSiteDesign `
  -Title "Contoso customer tracking - version 2" `
  -WebTemplate "68" `
  -Description "Updated site design for list schema that tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview - version 2"
```
## <a name="set-spositescript"></a><span data-ttu-id="a9168-271">Set-SPOSiteScript</span><span class="sxs-lookup"><span data-stu-id="a9168-271">Set-SPOSiteScript</span></span>

<span data-ttu-id="a9168-272">Обновляет загруженный ранее скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-272">Updates a previously uploaded site script.</span></span>

```powershell
Set-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="a9168-273">Параметры</span><span class="sxs-lookup"><span data-stu-id="a9168-273">Parameters</span></span>

|<span data-ttu-id="a9168-274">Параметр</span><span class="sxs-lookup"><span data-stu-id="a9168-274">Parameter</span></span>     | <span data-ttu-id="a9168-275">Описание</span><span class="sxs-lookup"><span data-stu-id="a9168-275">Description</span></span>  |
|--------------|--------------|
| <span data-ttu-id="a9168-276">-Title</span><span class="sxs-lookup"><span data-stu-id="a9168-276">-Title</span></span>       | <span data-ttu-id="a9168-277">Отображаемое имя макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-277">The display name of the site design.</span></span> |
| <span data-ttu-id="a9168-278">-Content</span><span class="sxs-lookup"><span data-stu-id="a9168-278">-Content</span></span>     | <span data-ttu-id="a9168-279">Значение JSON, описывающее скрипт.</span><span class="sxs-lookup"><span data-stu-id="a9168-279">JSON value that describes the script.</span></span> <span data-ttu-id="a9168-280">Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a9168-280">For more information, see [JSON reference](site-design-json-schema.md).</span></span>|
| <span data-ttu-id="a9168-281">-Description</span><span class="sxs-lookup"><span data-stu-id="a9168-281">-Description</span></span> | <span data-ttu-id="a9168-282">Описание скрипта.</span><span class="sxs-lookup"><span data-stu-id="a9168-282">A description of the script.</span></span> |

<span data-ttu-id="a9168-283">Приведенный ниже код обновляет созданный ранее скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="a9168-283">The following example updates a previously created site script.</span></span> <span data-ttu-id="a9168-284">Все макеты сайтов с ним будут выполнять обновленный скрипт.</span><span class="sxs-lookup"><span data-stu-id="a9168-284">Any site designs referencing it will executed the updated script.</span></span> 

```json
{
    "$schema": "schema.json",
        "actions": [
            {
                "verb": "addNavLink",
                "url": "/Custom Library",
                "displayName": "Custom Library Updated",
                "isWebRelative": true
            },
            {
                "verb": "addNavLink",
                "url": "/Lists/Custom List",
                "displayName": "Custom List Updated",
                "isWebRelative": true
            },
            {
                "verb": "applyTheme",
                themeName: "Contoso Explorers"
            }
        ],
            "bindata": { },
    "version": 2
}
```
<span data-ttu-id="a9168-285">Скопируйте в буфер</span><span class="sxs-lookup"><span data-stu-id="a9168-285">Copy to clipboard</span></span>

```powershell
C:\> $script = Get-Clipboard -Raw
C:\> Set-SPOSiteScript -Identity 7647d3d6-1046-41fe-a798-4ff66b099d12 -Content $script -Description "Update site script to change links and apply Contoso Explorers theme"
```

## <a name="see-also"></a><span data-ttu-id="a9168-286">См. также</span><span class="sxs-lookup"><span data-stu-id="a9168-286">See also</span></span>

- [<span data-ttu-id="a9168-287">Справочные материалы по схеме JSON</span><span class="sxs-lookup"><span data-stu-id="a9168-287">JSON schema reference</span></span>](site-design-json-schema.md)
- [<span data-ttu-id="a9168-288">REST API</span><span class="sxs-lookup"><span data-stu-id="a9168-288">REST API</span></span>](site-design-rest-api.md)
- [<span data-ttu-id="a9168-289">Применение области к макету сайта</span><span class="sxs-lookup"><span data-stu-id="a9168-289">Apply a scope to your site design</span></span>](site-design-scoping.md)
