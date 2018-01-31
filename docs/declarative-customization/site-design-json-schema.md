---
title: "Схема JSON для макетов сайтов"
description: "Справочник по схеме JSON для создания макетов сайтов SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: e5495608c10bac18ee98f858736d117a02c5f2a5
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="site-design-json-schema"></a><span data-ttu-id="790ac-103">Схема JSON для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="790ac-103">Site design JSON schema</span></span>

> [!NOTE]
> <span data-ttu-id="790ac-104">Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="790ac-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="790ac-105">В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.</span><span class="sxs-lookup"><span data-stu-id="790ac-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="790ac-106">Макет сайта представляет собой список действий.</span><span class="sxs-lookup"><span data-stu-id="790ac-106">The site design is a list of actions.</span></span> <span data-ttu-id="790ac-107">Сложные действия, например создание списка, также содержат вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="790ac-107">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="790ac-108">Каждое действие указывается с помощью значения verb (команды).</span><span class="sxs-lookup"><span data-stu-id="790ac-108">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="790ac-109">Действия-команды выполняются в том порядке, в котором они указаны в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="790ac-109">Verb actions are run in the order they appear in the JSON script.</span></span> <span data-ttu-id="790ac-110">Используйте только указанные здесь действия-команды, иначе при попытке загрузить скрипт сайта возникнет ошибка "не удается обработать действие".</span><span class="sxs-lookup"><span data-stu-id="790ac-110">Only the verb actions listed here can be used, otherwise an "unable to handle action" error will be thrown when trying to upload a site script.</span></span> <span data-ttu-id="790ac-111">Со временем список действий будет расширяться.</span><span class="sxs-lookup"><span data-stu-id="790ac-111">More actions will be added over time.</span></span> 

<span data-ttu-id="790ac-112">Общая структура JSON выглядит так:</span><span class="sxs-lookup"><span data-stu-id="790ac-112">The overall JSON structure is specified as follows:</span></span>

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

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="790ac-113">Создание списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="790ac-113">Create a new SharePoint list</span></span>

<span data-ttu-id="790ac-114">Используйте команду **createSPList** для создания списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="790ac-114">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="790ac-115">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-115">JSON values:</span></span>

- <span data-ttu-id="790ac-116">**listName** — имя списка, которое видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="790ac-116">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="790ac-117">**templateType** — тип шаблона, применяемый к списку.</span><span class="sxs-lookup"><span data-stu-id="790ac-117">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="790ac-118">Как правило, используется значение 100.</span><span class="sxs-lookup"><span data-stu-id="790ac-118">Typically you would use value 100.</span></span> <span data-ttu-id="790ac-119">Значения типов шаблонов указываются в [перечислении SPListTemplateType](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).</span><span class="sxs-lookup"><span data-stu-id="790ac-119">Template type values are documented in [SPListTemplateType enumeration](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).</span></span>
- <span data-ttu-id="790ac-120">**subactions** — массив действий, выполняемых в указанном порядке для создания списка.</span><span class="sxs-lookup"><span data-stu-id="790ac-120">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="790ac-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-121">Example:</span></span>

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

<span data-ttu-id="790ac-122">Массив дочерних действий содержит дополнительные действия для создания списка.</span><span class="sxs-lookup"><span data-stu-id="790ac-122">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="790ac-123">Вложенные действия также указываются с помощью значения **verb**.</span><span class="sxs-lookup"><span data-stu-id="790ac-123">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="790ac-124">setTitle</span><span class="sxs-lookup"><span data-stu-id="790ac-124">setTitle</span></span>

<span data-ttu-id="790ac-125">Задает название, обозначающее список в представлениях.</span><span class="sxs-lookup"><span data-stu-id="790ac-125">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="790ac-126">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-126">JSON value:</span></span>

- <span data-ttu-id="790ac-127">**title** — название списка.</span><span class="sxs-lookup"><span data-stu-id="790ac-127">**title** - The title of the new list.</span></span>

<span data-ttu-id="790ac-128">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-128">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="790ac-129">setDescription</span><span class="sxs-lookup"><span data-stu-id="790ac-129">setDescription</span></span>

<span data-ttu-id="790ac-130">Задает описание списка.</span><span class="sxs-lookup"><span data-stu-id="790ac-130">Sets the description of the list.</span></span>

<span data-ttu-id="790ac-131">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-131">JSON value:</span></span>

- <span data-ttu-id="790ac-132">**description** — описание нового списка.</span><span class="sxs-lookup"><span data-stu-id="790ac-132">**description** - The description of the new list.</span></span>

<span data-ttu-id="790ac-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-133">Example:</span></span>

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="790ac-134">addSPField</span><span class="sxs-lookup"><span data-stu-id="790ac-134">addSPField</span></span>

<span data-ttu-id="790ac-135">Добавляет новое поле.</span><span class="sxs-lookup"><span data-stu-id="790ac-135">Adds a new field.</span></span>

<span data-ttu-id="790ac-136">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-136">JSON values:</span></span>

- <span data-ttu-id="790ac-137">**fieldType** — можно задать тип поля **Text**, **Note**, **Number**, **Boolean**, **User** или **DateTime**.</span><span class="sxs-lookup"><span data-stu-id="790ac-137">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="790ac-138">**displayName** — отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="790ac-138">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="790ac-139">**isRequired** — значение True, если это поле обязательно должно содержать данные. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="790ac-139">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="790ac-140">**addToDefaultView** — значение True, если поле будет добавлено в представление по умолчанию. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="790ac-140">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="790ac-141">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-141">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="790ac-142">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="790ac-142">deleteSPField</span></span>

<span data-ttu-id="790ac-143">Удаляет стандартное поле, предоставленное выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="790ac-143">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="790ac-144">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-144">JSON value:</span></span>

- <span data-ttu-id="790ac-145">**displayName** — отображаемое имя удаляемого поля.</span><span class="sxs-lookup"><span data-stu-id="790ac-145">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="790ac-146">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-146">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="790ac-147">addContentType</span><span class="sxs-lookup"><span data-stu-id="790ac-147">addContentType</span></span>

<span data-ttu-id="790ac-148">Добавляет тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="790ac-148">Adds a content type to the list.</span></span>

<span data-ttu-id="790ac-149">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-149">JSON value:</span></span>

- <span data-ttu-id="790ac-150">**name** — имя добавляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="790ac-150">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="790ac-151">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-151">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="790ac-152">removeContentType</span><span class="sxs-lookup"><span data-stu-id="790ac-152">removeContentType</span></span>

<span data-ttu-id="790ac-153">Удаляет тип контента, предоставленный выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="790ac-153">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="790ac-154">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-154">JSON value:</span></span>

- <span data-ttu-id="790ac-155">**name** — имя удаляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="790ac-155">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="790ac-156">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-156">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="790ac-157">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="790ac-157">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="790ac-158">Задает форматирование столбца для поля.</span><span class="sxs-lookup"><span data-stu-id="790ac-158">Sets column formatting for a field.</span></span> <span data-ttu-id="790ac-159">Дополнительные сведения о форматировании столбцов см. в статье [Настройка SharePoint с помощью форматирования столбцов](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="790ac-159">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="790ac-160">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-160">JSON values:</span></span>

- <span data-ttu-id="790ac-161">**fieldDisplayName** — отображаемое имя обрабатываемого поля.</span><span class="sxs-lookup"><span data-stu-id="790ac-161">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="790ac-162">**formatterJSON** — объект JSON, используемый в качестве ресурса CustomFormatter для поля.</span><span class="sxs-lookup"><span data-stu-id="790ac-162">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="790ac-163">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-163">Example:</span></span>

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a><span data-ttu-id="790ac-164">Добавление ссылки для перехода</span><span class="sxs-lookup"><span data-stu-id="790ac-164">Add a navigation link</span></span>

<span data-ttu-id="790ac-165">Чтобы добавить на сайт ссылку для перехода, используйте команду **addNavLink**.</span><span class="sxs-lookup"><span data-stu-id="790ac-165">Use the **addNavLink** verb to add a new navigation link to the site.</span></span>

<span data-ttu-id="790ac-166">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-166">JSON values:</span></span>

- <span data-ttu-id="790ac-167">**url** — URL-адрес добавляемой ссылки.</span><span class="sxs-lookup"><span data-stu-id="790ac-167">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="790ac-168">**displayName** — отображаемое имя ссылки.</span><span class="sxs-lookup"><span data-stu-id="790ac-168">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="790ac-169">**isWebRelative** — значение True, если ссылка указывается относительно сайта. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="790ac-169">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="790ac-170">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-170">Example:</span></span>

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a><span data-ttu-id="790ac-171">Применение темы</span><span class="sxs-lookup"><span data-stu-id="790ac-171">Apply a theme</span></span>

<span data-ttu-id="790ac-172">Чтобы добавить на сайт тему, используйте команду **applyTheme**.</span><span class="sxs-lookup"><span data-stu-id="790ac-172">Use the **applyTheme** verb to add a theme to the site.</span></span> <span data-ttu-id="790ac-173">Дополнительные сведения о темах см. в статье [Настройка тем для сайтов SharePoint](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="790ac-173">For more information on themes, see [SharePoint site theming](site-theming/sharepoint-site-theming-overview.md).</span></span>

<span data-ttu-id="790ac-174">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-174">JSON value:</span></span>

- <span data-ttu-id="790ac-175">**themeName** — имя применяемой темы.</span><span class="sxs-lookup"><span data-stu-id="790ac-175">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="790ac-176">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-176">Example:</span></span>

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

## <a name="set-a-site-logo"></a><span data-ttu-id="790ac-177">Установка логотипа сайта</span><span class="sxs-lookup"><span data-stu-id="790ac-177">Set a site logo</span></span>

<span data-ttu-id="790ac-178">Чтобы указать логотип для сайта, используйте команду **setSiteLogo**.</span><span class="sxs-lookup"><span data-stu-id="790ac-178">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="790ac-179">Это действие работает только с шаблоном сайта для общения (68).</span><span class="sxs-lookup"><span data-stu-id="790ac-179">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="790ac-180">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-180">JSON value:</span></span>

- <span data-ttu-id="790ac-181">**url** — URL-адрес изображения логотипа.</span><span class="sxs-lookup"><span data-stu-id="790ac-181">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="790ac-182">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-182">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="790ac-183">Присоединение к сайту-концентратору</span><span class="sxs-lookup"><span data-stu-id="790ac-183">Join a hub site</span></span>

<span data-ttu-id="790ac-184">Чтобы присоединить сайт к концентратору, используйте команду **joinHubSite**.</span><span class="sxs-lookup"><span data-stu-id="790ac-184">Use the **joinHubSite** verb to join the site to a hub.</span></span> <!-- TBD provide link to more information on hubs and how to get the id -->

<span data-ttu-id="790ac-185">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-185">JSON value:</span></span>

- <span data-ttu-id="790ac-186">**hubSiteId** — ИД подключаемого сайта-концентратора.</span><span class="sxs-lookup"><span data-stu-id="790ac-186">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="790ac-187">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-187">Example:</span></span>

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="790ac-188">Вызов потока</span><span class="sxs-lookup"><span data-stu-id="790ac-188">Trigger a flow</span></span>

<span data-ttu-id="790ac-189">Чтобы запустить настраиваемый поток, используйте команду **triggerFlow**.</span><span class="sxs-lookup"><span data-stu-id="790ac-189">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="790ac-190">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="790ac-190">JSON values:</span></span>

- <span data-ttu-id="790ac-191">**url** — URL-адрес для вызова потока.</span><span class="sxs-lookup"><span data-stu-id="790ac-191">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="790ac-192">**name** — имя потока.</span><span class="sxs-lookup"><span data-stu-id="790ac-192">**name** - The name of the flow.</span></span>
- <span data-ttu-id="790ac-193">**parameters** — набор необязательных параметров, передаваемых в поток.</span><span class="sxs-lookup"><span data-stu-id="790ac-193">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="790ac-194">Пример:</span><span class="sxs-lookup"><span data-stu-id="790ac-194">Example:</span></span>

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
