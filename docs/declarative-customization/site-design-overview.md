---
title: "Общие сведения о макетах и скриптах сайтов SharePoint"
description: "Узнайте, как автоматизировать подготовку новых сайтов SharePoint с пользовательскими конфигурациями, используя скрипты и макеты сайтов SharePoint."
ms.date: 01/08/2018
ms.openlocfilehash: dc6790872003dab760d77f178346d7cb930c4d0d
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="sharepoint-site-design-and-site-script-overview"></a><span data-ttu-id="4e344-103">Общие сведения о макетах и скриптах сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e344-103">SharePoint site design and site script overview</span></span>

> [!NOTE]
> <span data-ttu-id="4e344-104">Макеты и скрипты сайта выпущены в производство и доступны для общего использования.</span><span class="sxs-lookup"><span data-stu-id="4e344-104">Site designs and site scripts have been released to production and are available for general use.</span></span>

<span data-ttu-id="4e344-105">Автоматизируйте подготовку новых или уже существующих современных сайтов SharePoint с собственными конфигурациями, используя макеты и скрипты.</span><span class="sxs-lookup"><span data-stu-id="4e344-105">Use site designs and site scripts to automate provisioning new SharePoint sites using your own custom configurations.</span></span> <span data-ttu-id="4e344-106">Когда пользователи в организации создают сайты SharePoint, часто требуется обеспечить некоторый уровень согласованности.</span><span class="sxs-lookup"><span data-stu-id="4e344-106">When people in your organization create new SharePoint sites, you often need to ensure some level of consistency.</span></span> <span data-ttu-id="4e344-107">Например, к каждому новому сайту может потребоваться применять надлежащий фирменный стиль и темы.</span><span class="sxs-lookup"><span data-stu-id="4e344-107">For example, you may need proper branding and theming applied to each new site.</span></span> <span data-ttu-id="4e344-108">Вы также можете использовать подробные скрипты подготовки сайтов (например, модуль подготовки PnP), которые должны применяться при создании каждого сайта.</span><span class="sxs-lookup"><span data-stu-id="4e344-108">You may also have detailed site provisioning scripts, such as using the PnP provisioning engine, that need to be applied each time a new site is created.</span></span> <span data-ttu-id="4e344-109">В этой статье описывается использование макетов и скриптов сайтов для создания пользовательских конфигураций, применяемых при создании сайтов.</span><span class="sxs-lookup"><span data-stu-id="4e344-109">This article describes how you can use site designs and site scripts to provide custom configurations to apply when new sites are created.</span></span>

## <a name="how-site-designs-work"></a><span data-ttu-id="4e344-110">Как работают макеты сайтов</span><span class="sxs-lookup"><span data-stu-id="4e344-110">How site designs work</span></span>

<span data-ttu-id="4e344-111">Макеты сайтов подобны шаблонам.</span><span class="sxs-lookup"><span data-stu-id="4e344-111">Site designs are like a template.</span></span> <span data-ttu-id="4e344-112">Их можно использовать при создании сайтов, чтобы выполнять с ними одну и ту же последовательность действий.</span><span class="sxs-lookup"><span data-stu-id="4e344-112">They can be used each time a new site is created to apply a consistent set of actions.</span></span> <span data-ttu-id="4e344-113">Их также можно применять к существующим современным сайтам, например сайтам групп и сайтам для общения.</span><span class="sxs-lookup"><span data-stu-id="4e344-113">They can also be applied to existing modern sites (Group-connected Team and communication).</span></span> <span data-ttu-id="4e344-114">Как правило, большинство действий (например, установка темы или создание списков) влияет на сам сайт.</span><span class="sxs-lookup"><span data-stu-id="4e344-114">Most actions typically affect the site itself, such as setting the theme, or creating lists.</span></span> <span data-ttu-id="4e344-115">Однако макет сайта также может включать другие действия, такие как запись URL-адреса нового сайта в журнал или отправка твита.</span><span class="sxs-lookup"><span data-stu-id="4e344-115">But a site design can also include other actions, such as recording the new site URL to a log, or sending a tweet.</span></span>

<span data-ttu-id="4e344-116">Вы можете создавать макеты сайтов и регистрировать их в SharePoint, используя один из современных шаблонов сайтов: сайт группы или сайт для общения.</span><span class="sxs-lookup"><span data-stu-id="4e344-116">You create site designs and register them in SharePoint to one of the modern template sites: the team site, or communication site.</span></span> <span data-ttu-id="4e344-117">Ниже описывается, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="4e344-117">You can see how this works in the following steps.</span></span>

1. <span data-ttu-id="4e344-118">Перейдите на домашнюю страницу SharePoint в клиенте разработчика.</span><span class="sxs-lookup"><span data-stu-id="4e344-118">Go to the SharePoint home page on your developer tenant.</span></span>
1. <span data-ttu-id="4e344-119">Нажмите **Создать сайт**.</span><span class="sxs-lookup"><span data-stu-id="4e344-119">Choose **Create site**.</span></span>

    <span data-ttu-id="4e344-120">Вы увидите два современных шаблона сайтов: **Сайт группы** и **Сайт для общения**.</span><span class="sxs-lookup"><span data-stu-id="4e344-120">You'll see the two modern template sites: **Team site**, and **Communication site**.</span></span>

1. <span data-ttu-id="4e344-121">Выберите **Сайт для общения**.</span><span class="sxs-lookup"><span data-stu-id="4e344-121">Choose **Communication site**.</span></span>

    <span data-ttu-id="4e344-122">На сайте общения есть поле **Выберите оформление**, где по умолчанию доступны следующие три макета:</span><span class="sxs-lookup"><span data-stu-id="4e344-122">The communication site has a **Choose a design** box in which comes with the following site designs.</span></span>

    - <span data-ttu-id="4e344-123">"Статья";</span><span class="sxs-lookup"><span data-stu-id="4e344-123">Topic</span></span>
    - <span data-ttu-id="4e344-124">"Демонстрация";</span><span class="sxs-lookup"><span data-stu-id="4e344-124">Showcase</span></span>
    - <span data-ttu-id="4e344-125">"Пустой".</span><span class="sxs-lookup"><span data-stu-id="4e344-125">Blank</span></span>

<span data-ttu-id="4e344-126">Это стандартные макеты сайтов.</span><span class="sxs-lookup"><span data-stu-id="4e344-126">These are the default site designs.</span></span> <span data-ttu-id="4e344-127">У каждого макета сайта есть заголовок, описание и изображение.</span><span class="sxs-lookup"><span data-stu-id="4e344-127">For each site design there is a title, description, and image.</span></span>

![Стандартные заголовок, описание и изображение макета в шаблоне сайта для общения](images/site-designs-listed-on-communication-site-template.png)

<span data-ttu-id="4e344-129">Шаблон сайта группы содержит только один стандартный макет с именем **Сайт группы**.</span><span class="sxs-lookup"><span data-stu-id="4e344-129">Had you chosen the team site template, it contains only one default site design named **Team site**.</span></span> <span data-ttu-id="4e344-130">Дополнительные сведения о том, как можно изменить стандартные макеты сайта, см. в [этой статье](customize-default-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="4e344-130">For additional information on how you can change the default site designs, see [Customize a default site design](customize-default-site-design.md).</span></span>

<span data-ttu-id="4e344-131">После выбора макета SharePoint создает новый сайт и выполняет скрипты для его макета.</span><span class="sxs-lookup"><span data-stu-id="4e344-131">When a site design is selected, SharePoint creates the new site, and runs site scripts for the site design.</span></span> <span data-ttu-id="4e344-132">Скрипты сайта описывают задачи, такие как создание списков или применение темы.</span><span class="sxs-lookup"><span data-stu-id="4e344-132">The site scripts detail the work such as creating new lists, or applying a theme.</span></span> <span data-ttu-id="4e344-133">После выполнения действий из скриптов SharePoint выводит подробные сведения о результатах этих действий в области выполнения.</span><span class="sxs-lookup"><span data-stu-id="4e344-133">When the actions in the scripts are completed, SharePoint displays detailed results of those actions in a progress pane.</span></span>

![Область выполнения со списком завершенных действий из макета сайта](images/progress-pane.png)

> [!NOTE]
> <span data-ttu-id="4e344-135">Теперь макеты сайтов можно применять к ранее созданным семействам современных сайтов.</span><span class="sxs-lookup"><span data-stu-id="4e344-135">Site designs can now be applied to previously created modern site collections.</span></span> <span data-ttu-id="4e344-136">Дополнительные сведения см. в статьях, посвященных REST и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e344-136">See the REST and PowerShell articles for more details.</span></span>

## <a name="anatomy-of-a-site-script"></a><span data-ttu-id="4e344-137">Структура скрипта сайта</span><span class="sxs-lookup"><span data-stu-id="4e344-137">Anatomy of a site script</span></span>

<span data-ttu-id="4e344-138">Скрипты сайтов — это JSON-файлы, в которых указывается упорядоченный список действий, выполняемых при создании сайта.</span><span class="sxs-lookup"><span data-stu-id="4e344-138">Site scripts are JSON files that specify an ordered list of actions to run when creating the new site.</span></span> <span data-ttu-id="4e344-139">Действия выполняются в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="4e344-139">The actions are run in the order listed.</span></span> <span data-ttu-id="4e344-140">Ниже приведен пример скрипта с двумя действиями верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="4e344-140">The following example is a script that has two top-level actions.</span></span> <span data-ttu-id="4e344-141">Сначала он применяет ранее созданную тему с именем **Contoso Explorers**.</span><span class="sxs-lookup"><span data-stu-id="4e344-141">First it applies a theme that was previously created named **Contoso Explorers**.</span></span> <span data-ttu-id="4e344-142">Затем он создает список **Customer Tracking**.</span><span class="sxs-lookup"><span data-stu-id="4e344-142">Then it creates a **Customer Tracking** list.</span></span>

```json
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
           "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
}
```

<span data-ttu-id="4e344-143">Каждое действие в скрипте сайта задается с помощью значения **verb** в JSON.</span><span class="sxs-lookup"><span data-stu-id="4e344-143">Each action in a site script is specified by a **verb** value in the JSON.</span></span> <span data-ttu-id="4e344-144">В предыдущем скрипте первое действие указывается с помощью команды **applyTheme**.</span><span class="sxs-lookup"><span data-stu-id="4e344-144">In the previous script the first action is specified by the **applyTheme** verb.</span></span> <span data-ttu-id="4e344-145">Затем команда **createSPList** создает список.</span><span class="sxs-lookup"><span data-stu-id="4e344-145">Then the **createSPList** verb creates the list.</span></span> <span data-ttu-id="4e344-146">Обратите внимание, что команда **createSPList** содержит собственный набор команд, выполняющих дополнительные действия только со списком.</span><span class="sxs-lookup"><span data-stu-id="4e344-146">Notice that the **createSPList** verb contains its own set of verbs which run additional actions on just the list.</span></span>

<span data-ttu-id="4e344-147">Доступны следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4e344-147">Available actions include:</span></span>

- <span data-ttu-id="4e344-148">создание списка;</span><span class="sxs-lookup"><span data-stu-id="4e344-148">Creating a new list</span></span>
- <span data-ttu-id="4e344-149">применение темы;</span><span class="sxs-lookup"><span data-stu-id="4e344-149">Applying a theme</span></span>
- <span data-ttu-id="4e344-150">установка логотипа сайта;</span><span class="sxs-lookup"><span data-stu-id="4e344-150">Setting a site logo</span></span>
- <span data-ttu-id="4e344-151">добавление навигации;</span><span class="sxs-lookup"><span data-stu-id="4e344-151">Adding navigation</span></span>
- <span data-ttu-id="4e344-152">запуск потока Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="4e344-152">Triggering a Microsoft flow</span></span>

<span data-ttu-id="4e344-153">Скрипты сайта можно повторно запускать на том же сайте после подготовки.</span><span class="sxs-lookup"><span data-stu-id="4e344-153">Site scripts can be run again on the same site after provisioning.</span></span> <span data-ttu-id="4e344-154">Это можно делать только программным способом.</span><span class="sxs-lookup"><span data-stu-id="4e344-154">This can only be done programmatically.</span></span> <span data-ttu-id="4e344-155">Скрипты сайтов являются неразрушающими, то есть при повторном запуске они гарантируют, что сайт соответствует конфигурации из скрипта.</span><span class="sxs-lookup"><span data-stu-id="4e344-155">Site scripts are non-destructive, so when they run again, they ensure that the site matches the configuration in the script.</span></span> <span data-ttu-id="4e344-156">Например, если на сайте уже есть список с таким же именем, как у создаваемого скриптом, то скрипт только добавит недостающие поля в имеющийся список.</span><span class="sxs-lookup"><span data-stu-id="4e344-156">For example, if the site already has a list with the same name that the site script is creating, the site script will only add missing fields to the existing list.</span></span> <span data-ttu-id="4e344-157">Обратите также внимание на то, что скрипты сайта ограничены 30 кумулятивными действиями (для одного или нескольких скриптов, которые могут быть вызваны в макете сайта).</span><span class="sxs-lookup"><span data-stu-id="4e344-157">Also, please note that site scripts are limited to 30 cumulative actions (across one or more scripts that may be called in a site design).</span></span>

## <a name="using-powershell-or-rest-to-work-with-site-designs-and-site-scripts"></a><span data-ttu-id="4e344-158">Работа с макетами и скриптами сайтов с помощью PowerShell или REST</span><span class="sxs-lookup"><span data-stu-id="4e344-158">Using PowerShell or REST to work with site designs and site scripts</span></span>

<span data-ttu-id="4e344-159">Вы можете создавать макеты и скрипты сайтов с помощью PowerShell или REST API.</span><span class="sxs-lookup"><span data-stu-id="4e344-159">You can create site designs and site scripts by using PowerShell, or the REST API.</span></span> <span data-ttu-id="4e344-160">В приведенном ниже примере создаются скрипт сайта и макет, использующий этот скрипт.</span><span class="sxs-lookup"><span data-stu-id="4e344-160">The following example creates a site script and a site design that uses the site script.</span></span> <!-- The PowerShell example loads the script from a file, while the REST example has the script inline. -->

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' `
     -Raw | `
     Add-SPOSiteScript `
    -Title "Contoso theme and list"

Id          : 2756067f-d818-4933-a514-2a2b2c50fb06
Title       : Contoso theme and list
Description :
Content     :
Version     : 0

C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "2756067f-d818-4933-a514-2a2b2c50fb06" `
  -Description "Creates customer list and applies standard theme"
```

<!-- 
```javascript
var site_script = {
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
};

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title,Description=@desc)?@title='Contoso theme and list'&@desc='this script creates a list named customer tracking and sets the contoso explorers company theme'", site_script);

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign",{
  info:{
    Title:"Contoso customer tracking", Description:"Creates customer list and applies standard theme",  SiteScriptIds:["607aed52-6d61-490a-b692-c0f58a6981a1"],  WebTemplate:"64"
   }
  });
```
-->

<span data-ttu-id="4e344-161">В предыдущем примере командлет **Add-SPOSiteScript** или REST API **CreateSiteScript** возвращает ИД скрипта сайта. Он используется для параметра **SiteScripts** в последующем вызове командлета **Add-SPO-SiteDesign** или REST API **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="4e344-161">In the previous example, the **Add-SPOSiteScript** cmdlet, or **CreateSiteScript** REST API returns a site script id. This is used for the **SiteScripts** parameter in the subsequent call to the **Add-SPO-SiteDesign** cmdlet, or **CreateSiteDesign** REST API.</span></span>

<span data-ttu-id="4e344-162">Параметр **WebTemplate** со значением 64 указывает, что макет сайта регистрируется с шаблоном сайта группы.</span><span class="sxs-lookup"><span data-stu-id="4e344-162">The **WebTemplate** parameter set to the value 64 indicates to register this site design with the team site template.</span></span> <span data-ttu-id="4e344-163">Значение 68 указывает на шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="4e344-163">The value 68 would indicate the communication site template.</span></span> <span data-ttu-id="4e344-164">Параметры **Title** и **Description** отображаются, когда пользователь просматривает макеты сайтов во время создания сайта группы.</span><span class="sxs-lookup"><span data-stu-id="4e344-164">The **Title** and **Description** parameters will be displayed when a user views site designs as they create a new team site.</span></span>

> [!NOTE]
> <span data-ttu-id="4e344-165">Макет сайта может выполнять множество скриптов.</span><span class="sxs-lookup"><span data-stu-id="4e344-165">A site design can run multiple scripts.</span></span> <span data-ttu-id="4e344-166">Их идентификаторы передаются в массиве. Скрипты выполняются в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="4e344-166">The script IDs are passed in an array, and they will run in the order listed.</span></span>

<span data-ttu-id="4e344-167">Пошаговые инструкции по созданию макета сайта см. в [этой статье](get-started-create-site-design.md).</span><span class="sxs-lookup"><span data-stu-id="4e344-167">For step-by-step information on creating a site design, see [Get started creating site designs](get-started-create-site-design.md).</span></span>

## <a name="pnp-provisioning-and-customization-using-microsoft-flow"></a><span data-ttu-id="4e344-168">Подготовка PnP и настройка с помощью Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="4e344-168">PnP Provisioning and customization using Microsoft Flow</span></span>

<span data-ttu-id="4e344-169">Возможности скриптов сайтов включают вызов потока Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="4e344-169">One action provided by site scripts is the ability to trigger a Microsoft flow.</span></span> <span data-ttu-id="4e344-170">Благодаря этому вы можете указать любое дополнительное действие помимо доступных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e344-170">This allows you to specify any custom action you need beyond the actions provided natively in site scripts.</span></span>

<span data-ttu-id="4e344-171">Если для автоматизации создания сайта используется модуль подготовки PnP, то вы можете использовать поток Microsoft Flow для интеграции с макетами сайтов.</span><span class="sxs-lookup"><span data-stu-id="4e344-171">If you use the PnP provisioning engine to automate site creation, then you can use a Microsoft flow to integrate with site designs.</span></span> <span data-ttu-id="4e344-172">С помощью этой методики вы можете сохранить все имеющиеся скрипты подготовки, а также создавать новые.</span><span class="sxs-lookup"><span data-stu-id="4e344-172">You can maintain all of your existing provisioning scripts as well as create new custom provisioning scripts using this technique.</span></span>

![процесс вызова потока Microsoft Flow](images/process-for-triggering-a-custom-flow.png)

<span data-ttu-id="4e344-174">Этот процесс описывается ниже.</span><span class="sxs-lookup"><span data-stu-id="4e344-174">The process works as follows:</span></span>

1. <span data-ttu-id="4e344-175">Скрипт создает экземпляр потока Microsoft Flow, используя URL-адрес с дополнительными сведениями.</span><span class="sxs-lookup"><span data-stu-id="4e344-175">The script instantiates your Microsoft flow using a URL with additional details.</span></span>
1. <span data-ttu-id="4e344-176">Поток отправляет сообщение в настроенную вами очередь службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4e344-176">The flow sends a message to an Azure storage queue that you have configured.</span></span>
1. <span data-ttu-id="4e344-177">Сообщение вызывает настроенную вами функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="4e344-177">The message triggers a call to an Azure function that you have configured.</span></span>
1. <span data-ttu-id="4e344-178">Функция Azure выполняет пользовательский скрипт (например, модуль подготовки PnP), чтобы подготовить пользовательские конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4e344-178">The Azure function runs your custom script, such as the PnP provisioning engine, to apply your custom configurations.</span></span>

<span data-ttu-id="4e344-179">Пошаговое руководстве по настройке потока Microsoft Flow с помощью модуля подготовки PnP см. в [этой статье](site-design-pnp-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4e344-179">For a step-by-step tutorial on how to configure your own Microsoft flow with PnP provisioning, see [Build a complete site design using the PnP provisioning engine](site-design-pnp-provisioning.md).</span></span>

## <a name="scoping"></a><span data-ttu-id="4e344-180">Определение области</span><span class="sxs-lookup"><span data-stu-id="4e344-180">Scoping</span></span>

<span data-ttu-id="4e344-181">Вы можете настраивать макеты сайтов, чтобы они отображались только для определенных групп пользователей в организации.</span><span class="sxs-lookup"><span data-stu-id="4e344-181">You can configure site designs to only appear for specific groups or people in your organization.</span></span> <span data-ttu-id="4e344-182">Другие пользователи не будут видеть эти макеты.</span><span class="sxs-lookup"><span data-stu-id="4e344-182">This is useful to ensure that people only see the site designs intended for them.</span></span> <span data-ttu-id="4e344-183">Например, можно сделать так, чтобы макеты для бухгалтерии видели только бухгалтеры</span><span class="sxs-lookup"><span data-stu-id="4e344-183">For example, you might want the accounting department to only see site designs specifically for them.</span></span> <span data-ttu-id="4e344-184">и больше никто.</span><span class="sxs-lookup"><span data-stu-id="4e344-184">And the accounting site designs may not make sense to show to anyone else.</span></span>

<span data-ttu-id="4e344-185">После создания макета сайта он по умолчанию виден всем пользователям.</span><span class="sxs-lookup"><span data-stu-id="4e344-185">By default a site design can be viewed by everyone when it is created.</span></span> <span data-ttu-id="4e344-186">Области применяются с помощью командлета **Grant-SPOSiteDesignRights** или REST API **GrantSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="4e344-186">Scopes are applied by using the **Grant-SPOSiteDesignRights** cmdlet, or the **GrantSiteDesignRights** REST API.</span></span>  <span data-ttu-id="4e344-187">В качестве области можно указывать пользователей или группы безопасности, поддерживающие почту.</span><span class="sxs-lookup"><span data-stu-id="4e344-187">You can specify the scope by user, or a mail-enabled security group.</span></span> <span data-ttu-id="4e344-188">В приведенном ниже примере показано, как предоставить пользователю Nestor (на вымышленном сайте Contoso) права на просмотр макета.</span><span class="sxs-lookup"><span data-stu-id="4e344-188">The following example shows how to add Nestor (a user at the fictional Contoso site) view rights on a site design.</span></span>

> [!div class="tabbedCodeSnippets"]
```powershell
Grant-SPOSiteDesignRights `
  -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
  -Principals "nestorw@contoso.onmicrosoft.com" `
  -Rights View
```

<!--
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"44252d09-62c4-4913-9eb0-a2a8b8d7f863", principalNames:["nestorw@contoso.onmicrosoft.com”], grantedRights:1});
```
-->
<span data-ttu-id="4e344-189">Дополнительные сведения о работе с областями см. в [этой статье](site-design-scoping.md).</span><span class="sxs-lookup"><span data-stu-id="4e344-189">For more information about working with scopes, see [Scoping access to site designs](site-design-scoping.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4e344-190">См. также</span><span class="sxs-lookup"><span data-stu-id="4e344-190">See also</span></span>

- [<span data-ttu-id="4e344-191">Приступая к созданию макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="4e344-191">Get started creating site designs</span></span>](get-started-create-site-design.md)
- [<span data-ttu-id="4e344-192">Применение области к макету сайта</span><span class="sxs-lookup"><span data-stu-id="4e344-192">Apply a scope to your site design</span></span>](site-design-scoping.md)
- [<span data-ttu-id="4e344-193">Схема JSON для макета сайта</span><span class="sxs-lookup"><span data-stu-id="4e344-193">Site design JSON schema</span></span>](site-design-json-schema.md)
- [<span data-ttu-id="4e344-194">Командлеты PowerShell для макетов и скриптов сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e344-194">PowerShell cmdlets for SharePoint site designs and site scripts</span></span>](site-design-powershell.md)
- [<span data-ttu-id="4e344-195">REST API макетов и скриптов сайтов</span><span class="sxs-lookup"><span data-stu-id="4e344-195">Site design and site script REST API</span></span>](site-design-rest-api.md)
- [<span data-ttu-id="4e344-196">Примеры макетов сайта</span><span class="sxs-lookup"><span data-stu-id="4e344-196">Site design examples</span></span>](https://github.com/SharePoint/sp-dev-site-scripts)
