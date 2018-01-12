---
title: "Схема JSON для макетов сайтов"
description: "Справочник по схеме JSON для создания макетов сайтов SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: 8fcc88c854b948c785db6181fa66e307128b343d
ms.sourcegitcommit: 7b6ce94b477d9b587beaa059eb9aa7cd6235efde
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="site-design-json-schema"></a><span data-ttu-id="401f0-103">Схема JSON для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="401f0-103">Site design JSON schema</span></span>

> [!NOTE]
> <span data-ttu-id="401f0-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="401f0-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="401f0-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="401f0-105">They are not currently supported for use in production environments.</span></span>

<span data-ttu-id="401f0-106">Макет сайта представляет собой список действий.</span><span class="sxs-lookup"><span data-stu-id="401f0-106">The site design is a list of actions.</span></span> <span data-ttu-id="401f0-107">Сложные действия, например создание списка, также содержат вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="401f0-107">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="401f0-108">Каждое действие указывается с помощью значения verb (команды).</span><span class="sxs-lookup"><span data-stu-id="401f0-108">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="401f0-109">Действия-команды выполняются в том порядке, в котором они указаны в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="401f0-109">Verb actions are run in the order they appear in the JSON script.</span></span>

<span data-ttu-id="401f0-110">Общая структура JSON выглядит так:</span><span class="sxs-lookup"><span data-stu-id="401f0-110">The overall JSON structure is specified as follows:</span></span>

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

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="401f0-111">Создание списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="401f0-111">Create a new SharePoint list</span></span>

<span data-ttu-id="401f0-112">Используйте команду **createSPList** для создания списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="401f0-112">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="401f0-113">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-113">JSON values:</span></span>

- <span data-ttu-id="401f0-114">**listName** — имя списка, которое видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="401f0-114">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="401f0-115">**templateType** — тип шаблона, применяемый к списку.</span><span class="sxs-lookup"><span data-stu-id="401f0-115">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="401f0-116">Как правило, используется значение 100.</span><span class="sxs-lookup"><span data-stu-id="401f0-116">Typically you would use value 100.</span></span> <span data-ttu-id="401f0-117">Значения типов шаблонов указываются в [перечислении SPListTemplateType]((https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx)).</span><span class="sxs-lookup"><span data-stu-id="401f0-117">Template type values are documented in [SPListTemplateType enumeration]((https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx)).</span></span>
- <span data-ttu-id="401f0-118">**subactions** — массив действий, выполняемых в указанном порядке для создания списка.</span><span class="sxs-lookup"><span data-stu-id="401f0-118">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="401f0-119">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-119">Example:</span></span>

```json
{
    "verb": "createSPList",
    "listName": "Customer Tracking",
    "templateType": 100,
    "subactions": [
        {
            "verb": "setDescription",
            "description": "List of Customers and Orders"
         }
    ]
}
```

<span data-ttu-id="401f0-120">Массив дочерних действий содержит дополнительные действия для создания списка.</span><span class="sxs-lookup"><span data-stu-id="401f0-120">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="401f0-121">Вложенные действия также указываются с помощью значения **verb**.</span><span class="sxs-lookup"><span data-stu-id="401f0-121">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="401f0-122">setTitle</span><span class="sxs-lookup"><span data-stu-id="401f0-122">setTitle</span></span>

<span data-ttu-id="401f0-123">Задает название, обозначающее список в представлениях.</span><span class="sxs-lookup"><span data-stu-id="401f0-123">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="401f0-124">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-124">JSON value:</span></span>

- <span data-ttu-id="401f0-125">**title** — название списка.</span><span class="sxs-lookup"><span data-stu-id="401f0-125">**title** - The title of the new list.</span></span>

<span data-ttu-id="401f0-126">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-126">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="401f0-127">setDescription</span><span class="sxs-lookup"><span data-stu-id="401f0-127">setDescription</span></span>

<span data-ttu-id="401f0-128">Задает описание списка.</span><span class="sxs-lookup"><span data-stu-id="401f0-128">Sets the description of the list.</span></span>

<span data-ttu-id="401f0-129">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-129">JSON value:</span></span>

- <span data-ttu-id="401f0-130">**description** — описание нового списка.</span><span class="sxs-lookup"><span data-stu-id="401f0-130">**description** - The description of the new list.</span></span>

<span data-ttu-id="401f0-131">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-131">Example:</span></span>

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="401f0-132">addSPField</span><span class="sxs-lookup"><span data-stu-id="401f0-132">addSPField</span></span>

<span data-ttu-id="401f0-133">Добавляет новое поле.</span><span class="sxs-lookup"><span data-stu-id="401f0-133">Adds a new field.</span></span>

<span data-ttu-id="401f0-134">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-134">JSON values:</span></span>

- <span data-ttu-id="401f0-135">**fieldType** — можно задать тип поля **Text**, **Note**, **Number**, **Boolean**, **User** или **DateTime**.</span><span class="sxs-lookup"><span data-stu-id="401f0-135">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="401f0-136">**displayName** — отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="401f0-136">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="401f0-137">**isRequired** — значение True, если это поле обязательно должно содержать данные. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="401f0-137">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="401f0-138">**addToDefaultView** — значение True, если поле будет добавлено в представление по умолчанию. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="401f0-138">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="401f0-139">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-139">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="401f0-140">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="401f0-140">deleteSPField</span></span>

<span data-ttu-id="401f0-141">Удаляет стандартное поле, предоставленное выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="401f0-141">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="401f0-142">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-142">JSON value:</span></span>

- <span data-ttu-id="401f0-143">**displayName** — отображаемое имя удаляемого поля.</span><span class="sxs-lookup"><span data-stu-id="401f0-143">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="401f0-144">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-144">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="401f0-145">addContentType</span><span class="sxs-lookup"><span data-stu-id="401f0-145">addContentType</span></span>

<span data-ttu-id="401f0-146">Добавляет тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="401f0-146">Adds a content type to the list.</span></span>

<span data-ttu-id="401f0-147">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-147">JSON value:</span></span>

- <span data-ttu-id="401f0-148">**name** — имя добавляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="401f0-148">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="401f0-149">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-149">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="401f0-150">removeContentType</span><span class="sxs-lookup"><span data-stu-id="401f0-150">removeContentType</span></span>

<span data-ttu-id="401f0-151">Удаляет тип контента, предоставленный выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="401f0-151">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="401f0-152">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-152">JSON value:</span></span>

- <span data-ttu-id="401f0-153">**name** — имя удаляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="401f0-153">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="401f0-154">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-154">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="401f0-155">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="401f0-155">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="401f0-156">Задает форматирование столбца для поля.</span><span class="sxs-lookup"><span data-stu-id="401f0-156">Sets column formatting for a field.</span></span> <span data-ttu-id="401f0-157">Дополнительные сведения о форматировании столбцов см. в статье [Настройка SharePoint с помощью форматирования столбцов](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="401f0-157">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="401f0-158">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-158">JSON values:</span></span>

- <span data-ttu-id="401f0-159">**fieldDisplayName** — отображаемое имя обрабатываемого поля.</span><span class="sxs-lookup"><span data-stu-id="401f0-159">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="401f0-160">**formatterJSON** — объект JSON, используемый в качестве ресурса CustomFormatter для поля.</span><span class="sxs-lookup"><span data-stu-id="401f0-160">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="401f0-161">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-161">Example:</span></span>

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a><span data-ttu-id="401f0-162">Добавление ссылки для перехода</span><span class="sxs-lookup"><span data-stu-id="401f0-162">Add a navigation link</span></span>

<span data-ttu-id="401f0-163">Чтобы добавить на сайт ссылку для перехода, используйте команду **addNavLink**.</span><span class="sxs-lookup"><span data-stu-id="401f0-163">Use the **addNavLink** verb to add a new navigation link to the site.</span></span>

<span data-ttu-id="401f0-164">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-164">JSON values:</span></span>

- <span data-ttu-id="401f0-165">**url** — URL-адрес добавляемой ссылки.</span><span class="sxs-lookup"><span data-stu-id="401f0-165">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="401f0-166">**displayName** — отображаемое имя ссылки.</span><span class="sxs-lookup"><span data-stu-id="401f0-166">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="401f0-167">**isWebRelative** — значение True, если ссылка указывается относительно сайта. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="401f0-167">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="401f0-168">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-168">Example:</span></span>

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a><span data-ttu-id="401f0-169">Применение темы</span><span class="sxs-lookup"><span data-stu-id="401f0-169">Apply a theme</span></span>

<span data-ttu-id="401f0-170">Чтобы добавить на сайт тему, используйте команду **applyTheme**.</span><span class="sxs-lookup"><span data-stu-id="401f0-170">Use the **applyTheme** verb to add a theme to the site.</span></span> <span data-ttu-id="401f0-171">Дополнительные сведения о темах см. в статье [Настройка тем для сайтов SharePoint](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="401f0-171">For more information on themes, see [SharePoint site theming](site-theming/sharepoint-site-theming-overview.md).</span></span>

<span data-ttu-id="401f0-172">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-172">JSON value:</span></span>

- <span data-ttu-id="401f0-173">**themeName** — имя применяемой темы.</span><span class="sxs-lookup"><span data-stu-id="401f0-173">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="401f0-174">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-174">Example:</span></span>

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

## <a name="set-a-site-logo"></a><span data-ttu-id="401f0-175">Установка логотипа сайта</span><span class="sxs-lookup"><span data-stu-id="401f0-175">Set a site logo</span></span>

<span data-ttu-id="401f0-176">Чтобы указать логотип для сайта, используйте команду **setSiteLogo**.</span><span class="sxs-lookup"><span data-stu-id="401f0-176">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="401f0-177">Это действие работает только с шаблоном сайта для общения (68).</span><span class="sxs-lookup"><span data-stu-id="401f0-177">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="401f0-178">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-178">JSON value:</span></span>

- <span data-ttu-id="401f0-179">**url** — URL-адрес изображения логотипа.</span><span class="sxs-lookup"><span data-stu-id="401f0-179">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="401f0-180">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-180">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="401f0-181">Присоединение к сайту-концентратору</span><span class="sxs-lookup"><span data-stu-id="401f0-181">Join a hub site</span></span>

<span data-ttu-id="401f0-182">Чтобы присоединить сайт к концентратору, используйте команду **joinHubSite**.</span><span class="sxs-lookup"><span data-stu-id="401f0-182">Use the **joinHubSite** verb to join the site to a hub.</span></span> <!-- TBD provide link to more information on hubs and how to get the id -->

<span data-ttu-id="401f0-183">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-183">JSON value:</span></span>

- <span data-ttu-id="401f0-184">**hubSiteId** — ИД подключаемого сайта-концентратора.</span><span class="sxs-lookup"><span data-stu-id="401f0-184">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="401f0-185">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-185">Example:</span></span>

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="401f0-186">Вызов потока</span><span class="sxs-lookup"><span data-stu-id="401f0-186">Trigger a flow</span></span>

<span data-ttu-id="401f0-187">Чтобы запустить настраиваемый поток, используйте команду **triggerFlow**.</span><span class="sxs-lookup"><span data-stu-id="401f0-187">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="401f0-188">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="401f0-188">JSON values:</span></span>

- <span data-ttu-id="401f0-189">**url** — URL-адрес для вызова потока.</span><span class="sxs-lookup"><span data-stu-id="401f0-189">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="401f0-190">**name** — имя потока.</span><span class="sxs-lookup"><span data-stu-id="401f0-190">**name** - The name of the flow.</span></span>
- <span data-ttu-id="401f0-191">**parameters** — набор необязательных параметров, передаваемых в поток.</span><span class="sxs-lookup"><span data-stu-id="401f0-191">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="401f0-192">Пример:</span><span class="sxs-lookup"><span data-stu-id="401f0-192">Example:</span></span>

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
