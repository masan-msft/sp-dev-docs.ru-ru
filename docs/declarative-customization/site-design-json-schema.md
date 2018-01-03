---
title: "Схема JSON для макетов сайтов"
description: "Справочник по схеме JSON для создания макетов сайтов SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: 0b1d0a0bd79d89e269744ca0646eb30b4ed0e731
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="site-design-json-schema"></a><span data-ttu-id="ed6dd-103">Схема JSON для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="ed6dd-103">Site design JSON schema</span></span>

> [!NOTE]
> <span data-ttu-id="ed6dd-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="ed6dd-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-105">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="ed6dd-106">Макет сайта представляет собой список действий.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-106">The site design is a list of actions.</span></span> <span data-ttu-id="ed6dd-107">Сложные действия, например создание списка, также содержат вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-107">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="ed6dd-108">Каждое действие указывается с помощью значения verb (команды).</span><span class="sxs-lookup"><span data-stu-id="ed6dd-108">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="ed6dd-109">Действия-команды выполняются в том порядке, в котором они указаны в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-109">Verb actions are run in the order they appear in the JSON script.</span></span>

<span data-ttu-id="ed6dd-110">Общая структура JSON выглядит так:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-110">The overall JSON structure is specified as follows:</span></span>

```json
{
    "$schema": "schema.json",
        "actions": [
            ...
            <one or more verb actions>
            ...
        ],
        "bindata": { },
        "version": 1
};
```

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="ed6dd-111">Создание списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="ed6dd-111">Create a new entry in a SharePoint list</span></span>

<span data-ttu-id="ed6dd-112">Используйте команду **createSPList** для создания списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-112">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="ed6dd-113">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-113">JSON values:</span></span>

- <span data-ttu-id="ed6dd-114">**listName** — имя списка, которое видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-114">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="ed6dd-115">**templateType** — тип шаблона, применяемый к списку.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-115">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="ed6dd-116">Как правило, используется значение 100.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-116">Typically you would use value 100.</span></span> <span data-ttu-id="ed6dd-117">Значения типов шаблонов указываются в [перечислении SPListTemplateType]((https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx)).</span><span class="sxs-lookup"><span data-stu-id="ed6dd-117">Template type values are documented in [SPListTemplateType enumeration]((https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx)).</span></span>
- <span data-ttu-id="ed6dd-118">**subactions** — массив действий, выполняемых в указанном порядке для создания списка.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-118">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="ed6dd-119">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-119">Example:</span></span>

```json
{
    "verb": "createSPList",
    "listName": "Customer Tracking",
    "templateType": 100,
    "subactions": [
        {
            "verb": "SetDescription",
            "description": "List of Customers and Orders"
         }
    ]
}
```

<span data-ttu-id="ed6dd-120">Массив дочерних действий содержит дополнительные действия для создания списка.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-120">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="ed6dd-121">Вложенные действия также указываются с помощью значения **verb**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-121">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="ed6dd-122">setTitle</span><span class="sxs-lookup"><span data-stu-id="ed6dd-122">setTitle</span></span>

<span data-ttu-id="ed6dd-123">Задает название, обозначающее список в представлениях.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-123">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="ed6dd-124">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-124">JSON value:</span></span>

- <span data-ttu-id="ed6dd-125">**title** — название списка.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-125">**title** - The title of the new list.</span></span>

<span data-ttu-id="ed6dd-126">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-126">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="ed6dd-127">setDescription</span><span class="sxs-lookup"><span data-stu-id="ed6dd-127">setDescription</span></span>

<span data-ttu-id="ed6dd-128">Задает описание списка.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-128">Sets the description of the list.</span></span>

<span data-ttu-id="ed6dd-129">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-129">JSON value:</span></span>

- <span data-ttu-id="ed6dd-130">**description** — описание нового списка.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-130">**description** - The description of the new list.</span></span>

<span data-ttu-id="ed6dd-131">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-131">Example:</span></span>

```json
{
   "verb": "SetDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="ed6dd-132">addSPField</span><span class="sxs-lookup"><span data-stu-id="ed6dd-132">addSPField</span></span>

<span data-ttu-id="ed6dd-133">Добавляет новое поле.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-133">Adds a new field.</span></span>

<span data-ttu-id="ed6dd-134">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-134">JSON values:</span></span>

- <span data-ttu-id="ed6dd-135">**fieldType** — можно задать тип поля **Text**, **Note**, **Number**, **Boolean**, **User** или **DateTime**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-135">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="ed6dd-136">**displayName** — отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-136">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="ed6dd-137">**isRequired** — значение True, если это поле обязательно должно содержать данные. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-137">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="ed6dd-138">**addToDefaultView** — значение True, если поле будет добавлено в представление по умолчанию. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-138">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="ed6dd-139">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-139">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="ed6dd-140">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="ed6dd-140">deleteSPField</span></span>

<span data-ttu-id="ed6dd-141">Удаляет стандартное поле, предоставленное выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-141">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="ed6dd-142">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-142">JSON value:</span></span>

- <span data-ttu-id="ed6dd-143">**displayName** — отображаемое имя удаляемого поля.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-143">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="ed6dd-144">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-144">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="ed6dd-145">addContentType</span><span class="sxs-lookup"><span data-stu-id="ed6dd-145">addContentType</span></span>

<span data-ttu-id="ed6dd-146">Добавляет тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-146">Adds a new content type to the collection.</span></span>

<span data-ttu-id="ed6dd-147">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-147">JSON value:</span></span>

- <span data-ttu-id="ed6dd-148">**name** — имя добавляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-148">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="ed6dd-149">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-149">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="ed6dd-150">removeContentType</span><span class="sxs-lookup"><span data-stu-id="ed6dd-150">removeContentType</span></span>

<span data-ttu-id="ed6dd-151">Удаляет тип контента, предоставленный выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-151">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="ed6dd-152">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-152">JSON value:</span></span>

- <span data-ttu-id="ed6dd-153">**name** — имя удаляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-153">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="ed6dd-154">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-154">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="ed6dd-155">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="ed6dd-155">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="ed6dd-156">Задает форматирование столбца для поля.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-156">Sets column formatting for a field.</span></span> <span data-ttu-id="ed6dd-157">Дополнительные сведения о форматировании столбцов см. в статье [Настройка SharePoint с помощью форматирования столбцов](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="ed6dd-157">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="ed6dd-158">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-158">JSON values:</span></span>

- <span data-ttu-id="ed6dd-159">**fieldDisplayName** — отображаемое имя обрабатываемого поля.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-159">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="ed6dd-160">**formatterJSON** — объект JSON, используемый в качестве ресурса CustomFormatter для поля.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-160">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="ed6dd-161">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-161">Example:</span></span>

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a><span data-ttu-id="ed6dd-162">Добавление ссылки для перехода</span><span class="sxs-lookup"><span data-stu-id="ed6dd-162">Add a navigation link</span></span>

<span data-ttu-id="ed6dd-163">Чтобы добавить на сайт ссылку для перехода, используйте команду **addNavLink**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-163">Use the **addNavLink** verb to add a new navigation link to the site.</span></span>

<span data-ttu-id="ed6dd-164">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-164">JSON values:</span></span>

- <span data-ttu-id="ed6dd-165">**url** — URL-адрес добавляемой ссылки.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-165">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="ed6dd-166">**displayName** — отображаемое имя ссылки.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-166">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="ed6dd-167">**isWebRelative** — значение True, если ссылка указывается относительно сайта. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-167">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="ed6dd-168">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-168">Example:</span></span>

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a><span data-ttu-id="ed6dd-169">Применение темы</span><span class="sxs-lookup"><span data-stu-id="ed6dd-169">Apply a theme</span></span>

<span data-ttu-id="ed6dd-170">Чтобы добавить на сайт тему, используйте команду **applyTheme**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-170">Use the **applyTheme** verb to add a theme to the site.</span></span> <span data-ttu-id="ed6dd-171">Дополнительные сведения о темах см. в статье [Настройка тем для сайтов SharePoint](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed6dd-171">For more information about default themes, see [SharePoint site theming: JSON schema](site-theming/sharepoint-site-theming-overview.md).</span></span>

<span data-ttu-id="ed6dd-172">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-172">JSON value:</span></span>

- <span data-ttu-id="ed6dd-173">**themeName** — имя применяемой темы.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-173">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="ed6dd-174">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-174">Example:</span></span>

<!-- TBD: add link to Doug's Blue Yonder theme with note you need to create it first -->

```json
{
   "verb": "applyTheme",
   "themeName": "Blue Yonder"
}
```

<!-- 
## Create a page

Use the **createPage** verb to create a new page on the site.

JSON values:

- **fileName** - The name of the file.
- **setAsHomePage** - True if this page is the home page; otherwise, false.
- **pageData** - An object with additional information about the page. **pageData** requires the following values:
  - **Title** - The title of the page.
  - **BannerImageUrl** - A URL specifying the location of an image to display for the banner. <TBD: need more info>
  - **CanvasContent1** - Content for the page specified as XML. <TBD: need more info>
  - **LayoutWebpartsContent** - JSON for the layout. <TBD: need more info>

Example:

```json
{
   "verb": "createPage",
   "fileName": "event-collateral.aspx",
   "pageData":
        {
            "Title": "Comment customer events",
            "BannerImageUrl": "/Customer Event Collateral/customer.jpg",
            "CanvasContent1": "<xml>",
            "LayoutWebpartsContent": "{json}"
        },
    "setAsHomePage": true
}
```
-->

## <a name="set-a-site-logo"></a><span data-ttu-id="ed6dd-175">Установка логотипа сайта</span><span class="sxs-lookup"><span data-stu-id="ed6dd-175">Set a site logo</span></span>

<span data-ttu-id="ed6dd-176">Чтобы указать логотип для сайта, используйте команду **setSiteLogo**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-176">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="ed6dd-177">Это действие работает только с шаблоном сайта для общения (68).</span><span class="sxs-lookup"><span data-stu-id="ed6dd-177">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="ed6dd-178">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-178">JSON value:</span></span>

- <span data-ttu-id="ed6dd-179">**url** — URL-адрес изображения логотипа.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-179">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="ed6dd-180">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-180">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="ed6dd-181">Присоединение к сайту-концентратору</span><span class="sxs-lookup"><span data-stu-id="ed6dd-181">Join a hub site</span></span>

<span data-ttu-id="ed6dd-182">Чтобы присоединить сайт к концентратору, используйте команду **joinHubSite**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-182">Use the **joinHubSite** verb to join the site to a hub.</span></span> <!-- TBD provide link to more information on hubs and how to get the id -->

<span data-ttu-id="ed6dd-183">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-183">JSON value:</span></span>

- <span data-ttu-id="ed6dd-184">**hubSiteId** — ИД подключаемого сайта-концентратора.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-184">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="ed6dd-185">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-185">Example:</span></span>

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="ed6dd-186">Вызов потока</span><span class="sxs-lookup"><span data-stu-id="ed6dd-186">Trigger a flow</span></span>

<span data-ttu-id="ed6dd-187">Чтобы запустить настраиваемый поток, используйте команду **triggerFlow**.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-187">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="ed6dd-188">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-188">JSON values:</span></span>

- <span data-ttu-id="ed6dd-189">**url** — URL-адрес для вызова потока.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-189">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="ed6dd-190">**name** — имя потока.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-190">**name** - The name of the flow.</span></span>
- <span data-ttu-id="ed6dd-191">**parameters** — набор необязательных параметров, передаваемых в поток.</span><span class="sxs-lookup"><span data-stu-id="ed6dd-191">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="ed6dd-192">Пример:</span><span class="sxs-lookup"><span data-stu-id="ed6dd-192">Example:</span></span>

```json
 {
    "verb": "triggerFlow",
    "url": "<A trigger URL of the Flow.>",
    "name": "Record and tweet site creation event",
    "parameters": {
        "event": "Microsoft Event",
        "product": "SharePoint"
    }
}
```
