---
title: "Схема JSON для макетов сайтов"
description: "Справочник по схеме JSON для создания макетов сайтов SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: ed952df480601945f1214282658c55d5eb63b5a9
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="site-design-json-schema"></a><span data-ttu-id="d4fc7-103">Схема JSON для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="d4fc7-103">Site design JSON schema</span></span>

> [!NOTE]
> <span data-ttu-id="d4fc7-104">Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="d4fc7-105">В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="d4fc7-106">Макет сайта представляет собой список действий.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-106">The site design is a list of actions.</span></span> <span data-ttu-id="d4fc7-107">Сложные действия, например создание списка, также содержат вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-107">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="d4fc7-108">Каждое действие указывается с помощью значения verb (команды).</span><span class="sxs-lookup"><span data-stu-id="d4fc7-108">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="d4fc7-109">Действия-команды выполняются в том порядке, в котором они указаны в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-109">Verb actions are run in the order they appear in the JSON script.</span></span> <span data-ttu-id="d4fc7-110">Используйте только указанные здесь действия-команды, иначе при попытке загрузить скрипт сайта возникнет ошибка "не удается обработать действие".</span><span class="sxs-lookup"><span data-stu-id="d4fc7-110">Only the verb actions listed here can be used, otherwise an "unable to handle action" error will be thrown when trying to upload a site script.</span></span> <span data-ttu-id="d4fc7-111">Со временем список действий будет расширяться.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-111">More actions will be added over time.</span></span> 

<span data-ttu-id="d4fc7-112">Общая структура JSON выглядит так:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-112">The overall JSON structure is specified as follows:</span></span>

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

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="d4fc7-113">Создание списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="d4fc7-113">Create a new SharePoint list</span></span>

<span data-ttu-id="d4fc7-114">Используйте команду **createSPList** для создания списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-114">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="d4fc7-115">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-115">JSON values:</span></span>

- <span data-ttu-id="d4fc7-116">**listName** — имя списка, которое видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-116">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="d4fc7-117">**templateType** — тип шаблона, применяемый к списку.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-117">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="d4fc7-118">Как правило, используется значение 100.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-118">Typically you would use value 100.</span></span> <span data-ttu-id="d4fc7-119">Значения типов шаблонов указываются в [перечислении SPListTemplateType](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4fc7-119">Template type values are documented in [SPListTemplateType enumeration](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).</span></span>
- <span data-ttu-id="d4fc7-120">**subactions** — массив действий, выполняемых в указанном порядке для создания списка.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-120">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="d4fc7-121">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-121">Example:</span></span>

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

<span data-ttu-id="d4fc7-122">Массив дочерних действий содержит дополнительные действия для создания списка.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-122">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="d4fc7-123">Вложенные действия также указываются с помощью значения **verb**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-123">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="d4fc7-124">setTitle</span><span class="sxs-lookup"><span data-stu-id="d4fc7-124">setTitle</span></span>

<span data-ttu-id="d4fc7-125">Задает название, обозначающее список в представлениях.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-125">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="d4fc7-126">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-126">JSON value:</span></span>

- <span data-ttu-id="d4fc7-127">**title** — название списка.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-127">**title** - The title of the new list.</span></span>

<span data-ttu-id="d4fc7-128">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-128">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="d4fc7-129">setDescription</span><span class="sxs-lookup"><span data-stu-id="d4fc7-129">setDescription</span></span>

<span data-ttu-id="d4fc7-130">Задает описание списка.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-130">Sets the description of the list.</span></span>

<span data-ttu-id="d4fc7-131">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-131">JSON value:</span></span>

- <span data-ttu-id="d4fc7-132">**description** — описание нового списка.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-132">**description** - The description of the new list.</span></span>

<span data-ttu-id="d4fc7-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-133">Example:</span></span>

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="d4fc7-134">addSPField</span><span class="sxs-lookup"><span data-stu-id="d4fc7-134">addSPField</span></span>

<span data-ttu-id="d4fc7-135">Добавляет новое поле.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-135">Adds a new field.</span></span>

<span data-ttu-id="d4fc7-136">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-136">JSON values:</span></span>

- <span data-ttu-id="d4fc7-137">**fieldType** — можно задать тип поля **Text**, **Note**, **Number**, **Boolean**, **User** или **DateTime**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-137">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="d4fc7-138">**displayName** — отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-138">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="d4fc7-139">**isRequired** — значение True, если это поле обязательно должно содержать данные. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-139">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="d4fc7-140">**addToDefaultView** — значение True, если поле будет добавлено в представление по умолчанию. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-140">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="d4fc7-141">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-141">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="d4fc7-142">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="d4fc7-142">deleteSPField</span></span>

<span data-ttu-id="d4fc7-143">Удаляет стандартное поле, предоставленное выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-143">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="d4fc7-144">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-144">JSON value:</span></span>

- <span data-ttu-id="d4fc7-145">**displayName** — отображаемое имя удаляемого поля.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-145">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="d4fc7-146">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-146">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="d4fc7-147">addContentType</span><span class="sxs-lookup"><span data-stu-id="d4fc7-147">addContentType</span></span>

<span data-ttu-id="d4fc7-148">Добавляет тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-148">Adds a content type to the list.</span></span>

<span data-ttu-id="d4fc7-149">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-149">JSON value:</span></span>

- <span data-ttu-id="d4fc7-150">**name** — имя добавляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-150">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="d4fc7-151">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-151">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="d4fc7-152">removeContentType</span><span class="sxs-lookup"><span data-stu-id="d4fc7-152">removeContentType</span></span>

<span data-ttu-id="d4fc7-153">Удаляет тип контента, предоставленный выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-153">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="d4fc7-154">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-154">JSON value:</span></span>

- <span data-ttu-id="d4fc7-155">**name** — имя удаляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-155">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="d4fc7-156">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-156">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="d4fc7-157">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="d4fc7-157">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="d4fc7-158">Задает форматирование столбца для поля.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-158">Sets column formatting for a field.</span></span> <span data-ttu-id="d4fc7-159">Дополнительные сведения о форматировании столбцов см. в статье [Настройка SharePoint с помощью форматирования столбцов](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="d4fc7-159">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="d4fc7-160">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-160">JSON values:</span></span>

- <span data-ttu-id="d4fc7-161">**fieldDisplayName** — отображаемое имя обрабатываемого поля.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-161">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="d4fc7-162">**formatterJSON** — объект JSON, используемый в качестве ресурса CustomFormatter для поля.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-162">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="d4fc7-163">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-163">Example:</span></span>

```json
{
   "verb": "setSPFieldCustomFormatter",
   "fieldDisplayName": "name",
   "formatterJSON": "json" 
}
```
<!-- TBD provide an example for formatterJSON in previous example -->

## <a name="add-a-navigation-link"></a><span data-ttu-id="d4fc7-164">Добавление ссылки для перехода</span><span class="sxs-lookup"><span data-stu-id="d4fc7-164">Add a navigation link</span></span>

<span data-ttu-id="d4fc7-165">Чтобы добавить на сайт ссылку для перехода, используйте команду **addNavLink**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-165">Use the **addNavLink** verb to add a new navigation link to the site.</span></span>

<span data-ttu-id="d4fc7-166">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-166">JSON values:</span></span>

- <span data-ttu-id="d4fc7-167">**url** — URL-адрес добавляемой ссылки.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-167">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="d4fc7-168">**displayName** — отображаемое имя ссылки.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-168">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="d4fc7-169">**isWebRelative** — значение True, если ссылка указывается относительно сайта. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-169">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="d4fc7-170">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-170">Example:</span></span>

```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
}
```

## <a name="apply-a-theme"></a><span data-ttu-id="d4fc7-171">Применение темы</span><span class="sxs-lookup"><span data-stu-id="d4fc7-171">Apply a theme</span></span>

<span data-ttu-id="d4fc7-172">Чтобы добавить на сайт собственную тему, используйте команду **applyTheme**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-172">Use the **applyTheme** verb to add a theme to the site.</span></span> <span data-ttu-id="d4fc7-173">Дополнительные сведения о создании и добавлении тем см. в статье [Настройка тем SharePoint](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4fc7-173">For more information on how to construct and upload these themes, see [SharePoint site theming](site-theming/sharepoint-site-theming-overview.md).</span></span> <span data-ttu-id="d4fc7-174">Обратите внимание, что эта команда подходит только для применения собственных тем. Чтобы применить одну из встроенных тем SharePoint, скопируйте ее и добавьте ссылку на копию.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-174">Note that this site action only works for applying custom themes; to apply one of our in-product SharePoint themes, create a copy as a custom one and reference that one.</span></span>

<span data-ttu-id="d4fc7-175">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-175">JSON value:</span></span>

- <span data-ttu-id="d4fc7-176">**themeName** — имя применяемой темы.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-176">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="d4fc7-177">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-177">Example:</span></span>

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

## <a name="set-a-site-logo"></a><span data-ttu-id="d4fc7-178">Установка логотипа сайта</span><span class="sxs-lookup"><span data-stu-id="d4fc7-178">Set a site logo</span></span>

<span data-ttu-id="d4fc7-179">Чтобы указать логотип для сайта, используйте команду **setSiteLogo**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-179">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="d4fc7-180">Это действие работает только с шаблоном сайта для общения (68).</span><span class="sxs-lookup"><span data-stu-id="d4fc7-180">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="d4fc7-181">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-181">JSON value:</span></span>

- <span data-ttu-id="d4fc7-182">**url** — URL-адрес изображения логотипа.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-182">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="d4fc7-183">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-183">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="d4fc7-184">Присоединение к сайту-концентратору</span><span class="sxs-lookup"><span data-stu-id="d4fc7-184">Join a hub site</span></span>

<span data-ttu-id="d4fc7-185">Чтобы присоединить сайт к концентратору, используйте команду **joinHubSite**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-185">Use the **joinHubSite** verb to join the site to a hub.</span></span> <!-- TBD provide link to more information on hubs and how to get the id -->

<span data-ttu-id="d4fc7-186">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-186">JSON value:</span></span>

- <span data-ttu-id="d4fc7-187">**hubSiteId** — ИД подключаемого сайта-концентратора.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-187">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="d4fc7-188">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-188">Example:</span></span>

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="d4fc7-189">Вызов потока</span><span class="sxs-lookup"><span data-stu-id="d4fc7-189">Trigger a flow</span></span>

<span data-ttu-id="d4fc7-190">Чтобы запустить настраиваемый поток, используйте команду **triggerFlow**.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-190">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="d4fc7-191">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-191">JSON values:</span></span>

- <span data-ttu-id="d4fc7-192">**url** — URL-адрес для вызова потока.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-192">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="d4fc7-193">**name** — имя потока.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-193">**name** - The name of the flow.</span></span>
- <span data-ttu-id="d4fc7-194">**parameters** — набор необязательных параметров, передаваемых в поток.</span><span class="sxs-lookup"><span data-stu-id="d4fc7-194">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="d4fc7-195">Пример:</span><span class="sxs-lookup"><span data-stu-id="d4fc7-195">Example:</span></span>

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
