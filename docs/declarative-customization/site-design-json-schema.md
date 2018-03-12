---
title: "Схема JSON для макетов сайтов"
description: "Справочник по схеме JSON для создания макетов сайтов SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: f8cf39af5a98155d6b8af3cf38251f8198d2a395
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="site-design-json-schema"></a><span data-ttu-id="b6a36-103">Схема JSON для макетов сайтов</span><span class="sxs-lookup"><span data-stu-id="b6a36-103">Site design JSON schema</span></span>

<span data-ttu-id="b6a36-104">Макет сайта представляет собой список действий.</span><span class="sxs-lookup"><span data-stu-id="b6a36-104">The site design is a list of actions.</span></span> <span data-ttu-id="b6a36-105">Сложные действия, например создание списка, также содержат вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="b6a36-105">For more complex actions, such as creating a list, there are also subactions.</span></span> <span data-ttu-id="b6a36-106">Каждое действие указывается с помощью значения verb (команды).</span><span class="sxs-lookup"><span data-stu-id="b6a36-106">Each action is specified by a "verb" value.</span></span> <span data-ttu-id="b6a36-107">Действия-команды выполняются в том порядке, в котором они указаны в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="b6a36-107">Verb actions are run in the order they appear in the JSON script.</span></span> <span data-ttu-id="b6a36-108">Используйте только указанные здесь действия-команды, иначе при попытке загрузить скрипт сайта возникнет ошибка "не удается обработать действие".</span><span class="sxs-lookup"><span data-stu-id="b6a36-108">Only the verb actions listed here can be used, otherwise an "unable to handle action" error will be thrown when trying to upload a site script.</span></span> <span data-ttu-id="b6a36-109">Со временем список действий будет расширяться.</span><span class="sxs-lookup"><span data-stu-id="b6a36-109">More actions will be added over time.</span></span> 

<span data-ttu-id="b6a36-110">Общая структура JSON выглядит так:</span><span class="sxs-lookup"><span data-stu-id="b6a36-110">The overall JSON structure is specified as follows:</span></span>

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

## <a name="create-a-new-sharepoint-list"></a><span data-ttu-id="b6a36-111">Создание списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="b6a36-111">Create a new SharePoint list</span></span>

<span data-ttu-id="b6a36-112">Используйте команду **createSPList** для создания списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b6a36-112">Use the **createSPList** verb to create a new SharePoint list.</span></span>

<span data-ttu-id="b6a36-113">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-113">JSON values:</span></span>

- <span data-ttu-id="b6a36-114">**listName** — имя списка, которое видят пользователи.</span><span class="sxs-lookup"><span data-stu-id="b6a36-114">**listName** - The name of the list for users to identify it with.</span></span>
- <span data-ttu-id="b6a36-115">**templateType** — тип шаблона, применяемый к списку.</span><span class="sxs-lookup"><span data-stu-id="b6a36-115">**templateType** - Which template to apply to the list.</span></span> <span data-ttu-id="b6a36-116">Как правило, используется значение 100.</span><span class="sxs-lookup"><span data-stu-id="b6a36-116">Typically you would use value 100.</span></span> <span data-ttu-id="b6a36-117">Значения типов шаблонов указываются в [перечислении SPListTemplateType](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6a36-117">Template type values are documented in [SPListTemplateType enumeration](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).</span></span>
- <span data-ttu-id="b6a36-118">**subactions** — массив действий, выполняемых в указанном порядке для создания списка.</span><span class="sxs-lookup"><span data-stu-id="b6a36-118">**subactions** - An array of actions that run in the order listed to create your list.</span></span>

<span data-ttu-id="b6a36-119">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-119">Example:</span></span>

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

<span data-ttu-id="b6a36-120">Массив дочерних действий содержит дополнительные действия для создания списка.</span><span class="sxs-lookup"><span data-stu-id="b6a36-120">The subactions array provides additional actions to specify how to construct the list.</span></span> <span data-ttu-id="b6a36-121">Вложенные действия также указываются с помощью значения **verb**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-121">Subactions are also specified using a **verb** value.</span></span>

### <a name="settitle"></a><span data-ttu-id="b6a36-122">setTitle</span><span class="sxs-lookup"><span data-stu-id="b6a36-122">setTitle</span></span>

<span data-ttu-id="b6a36-123">Задает название, обозначающее список в представлениях.</span><span class="sxs-lookup"><span data-stu-id="b6a36-123">Sets a title which identifies the list in views.</span></span>

<span data-ttu-id="b6a36-124">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-124">JSON value:</span></span>

- <span data-ttu-id="b6a36-125">**title** — название списка.</span><span class="sxs-lookup"><span data-stu-id="b6a36-125">**title** - The title of the new list.</span></span>

<span data-ttu-id="b6a36-126">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-126">Example:</span></span>

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a><span data-ttu-id="b6a36-127">setDescription</span><span class="sxs-lookup"><span data-stu-id="b6a36-127">setDescription</span></span>

<span data-ttu-id="b6a36-128">Задает описание списка.</span><span class="sxs-lookup"><span data-stu-id="b6a36-128">Sets the description of the list.</span></span>

<span data-ttu-id="b6a36-129">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-129">JSON value:</span></span>

- <span data-ttu-id="b6a36-130">**description** — описание нового списка.</span><span class="sxs-lookup"><span data-stu-id="b6a36-130">**description** - The description of the new list.</span></span>

<span data-ttu-id="b6a36-131">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-131">Example:</span></span>

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a><span data-ttu-id="b6a36-132">addSPField</span><span class="sxs-lookup"><span data-stu-id="b6a36-132">addSPField</span></span>

<span data-ttu-id="b6a36-133">Добавляет новое поле.</span><span class="sxs-lookup"><span data-stu-id="b6a36-133">Adds a new field.</span></span>

<span data-ttu-id="b6a36-134">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-134">JSON values:</span></span>

- <span data-ttu-id="b6a36-135">**fieldType** — можно задать тип поля **Text**, **Note**, **Number**, **Boolean**, **User** или **DateTime**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-135">**fieldType** - The field type can be set to **Text**, **Note**, **Number**, **Boolean**, **User**, or **DateTime**.</span></span>
- <span data-ttu-id="b6a36-136">**displayName** — отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="b6a36-136">**displayName** - The display name of the field.</span></span>
- <span data-ttu-id="b6a36-137">**isRequired** — значение True, если это поле обязательно должно содержать данные. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="b6a36-137">**isRequired** - True if this field is required to contain information; otherwise, false.</span></span>
- <span data-ttu-id="b6a36-138">**addToDefaultView** — значение True, если поле будет добавлено в представление по умолчанию. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="b6a36-138">**addToDefaultView** - True if the field will be added to the default view; otherwise, false.</span></span>

<span data-ttu-id="b6a36-139">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-139">Example:</span></span>

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a><span data-ttu-id="b6a36-140">deleteSPField</span><span class="sxs-lookup"><span data-stu-id="b6a36-140">deleteSPField</span></span>

<span data-ttu-id="b6a36-141">Удаляет стандартное поле, предоставленное выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="b6a36-141">Deletes a default field that was provided by the selected template type.</span></span>

<span data-ttu-id="b6a36-142">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-142">JSON value:</span></span>

- <span data-ttu-id="b6a36-143">**displayName** — отображаемое имя удаляемого поля.</span><span class="sxs-lookup"><span data-stu-id="b6a36-143">**displayName** - The display name to identify the field to delete.</span></span>

<span data-ttu-id="b6a36-144">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-144">Example:</span></span>

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a><span data-ttu-id="b6a36-145">addContentType</span><span class="sxs-lookup"><span data-stu-id="b6a36-145">addContentType</span></span>

<span data-ttu-id="b6a36-146">Добавляет тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="b6a36-146">Adds a content type to the list.</span></span> <span data-ttu-id="b6a36-147">В настоящее время доступны только ограниченные типы контента по умолчанию, которые включены в шаблон сайта.</span><span class="sxs-lookup"><span data-stu-id="b6a36-147">Currently these are limited to only the default content types included in the site template.</span></span>

<span data-ttu-id="b6a36-148">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-148">JSON value:</span></span>

- <span data-ttu-id="b6a36-149">**name** — имя добавляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="b6a36-149">**name** - The name of the content type to add.</span></span>

<span data-ttu-id="b6a36-150">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-150">Example:</span></span>

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a><span data-ttu-id="b6a36-151">removeContentType</span><span class="sxs-lookup"><span data-stu-id="b6a36-151">removeContentType</span></span>

<span data-ttu-id="b6a36-152">Удаляет тип контента, предоставленный выбранным типом шаблона.</span><span class="sxs-lookup"><span data-stu-id="b6a36-152">Removes a content type that was provided by the selected template type.</span></span>

<span data-ttu-id="b6a36-153">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-153">JSON value:</span></span>

- <span data-ttu-id="b6a36-154">**name** — имя удаляемого типа контента.</span><span class="sxs-lookup"><span data-stu-id="b6a36-154">**name** - The name of the content type to remove.</span></span>

<span data-ttu-id="b6a36-155">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-155">Example:</span></span>

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a><span data-ttu-id="b6a36-156">setSPFieldCustomFormatter</span><span class="sxs-lookup"><span data-stu-id="b6a36-156">setSPFieldCustomFormatter</span></span>

<span data-ttu-id="b6a36-157">Задает форматирование столбца для поля.</span><span class="sxs-lookup"><span data-stu-id="b6a36-157">Sets column formatting for a field.</span></span> <span data-ttu-id="b6a36-158">Дополнительные сведения о форматировании столбцов см. в статье [Настройка SharePoint с помощью форматирования столбцов](column-formatting.md).</span><span class="sxs-lookup"><span data-stu-id="b6a36-158">For more information on column formatting see [Use column formatting to customize SharePoint](column-formatting.md).</span></span>

<span data-ttu-id="b6a36-159">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-159">JSON values:</span></span>

- <span data-ttu-id="b6a36-160">**fieldDisplayName** — отображаемое имя обрабатываемого поля.</span><span class="sxs-lookup"><span data-stu-id="b6a36-160">**fieldDisplayName** - The display name of the field to operate on.</span></span>
- <span data-ttu-id="b6a36-161">**formatterJSON** — объект JSON, используемый в качестве ресурса CustomFormatter для поля.</span><span class="sxs-lookup"><span data-stu-id="b6a36-161">**formatterJSON** - A JSON object to use as the field CustomFormatter.</span></span>

<span data-ttu-id="b6a36-162">Пример. В этом примере показано форматирование столбца чисел для его отображения в виде гистограммы</span><span class="sxs-lookup"><span data-stu-id="b6a36-162">Example: In this example we are formatting a number column as a data bar</span></span>

```json
                {
                    "verb": "setSPFieldCustomFormatter",
                    "fieldDisplayName": "Effort (days)",
                    "formatterJSON":
                    {
                        "debugMode": true,
                        "elmType": "div",
                        "txtContent": "@currentField",
                        "attributes": {
                            "class": "sp-field-dataBars"
                        },
                        "style": {
                            "width": {
                                "operator": "?",
                                "operands": [
                                    {
                                        "operator": ">",
                                        "operands": [
                                            "@currentField",
                                            "20"
                                        ]
                                    },
                                    "100%",
                                    {
                                        "operator": "+",
                                        "operands": [
                                            {
                                                "operator": "toString()",
                                                "operands": [
                                                    {
                                                        "operator": "*",
                                                        "operands": [
                                                            "@currentField",
                                                            5
                                                        ]
                                                    }
                                                ]
                                            },
                                            "%"
                                        ]
                                    }
                                ]
                            }
                        }
                    }
                }
```

## <a name="add-a-navigation-link"></a><span data-ttu-id="b6a36-163">Добавление ссылки для перехода</span><span class="sxs-lookup"><span data-stu-id="b6a36-163">Add a navigation link</span></span>

<span data-ttu-id="b6a36-164">Чтобы добавить на сайт ссылку для перехода, используйте команду **addNavLink**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-164">Use the **addNavLink** verb to add a new navigation link to the site.</span></span> 

<span data-ttu-id="b6a36-165">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-165">JSON values:</span></span>

- <span data-ttu-id="b6a36-166">**url** — URL-адрес добавляемой ссылки.</span><span class="sxs-lookup"><span data-stu-id="b6a36-166">**url** - The url of the link to add.</span></span>
- <span data-ttu-id="b6a36-167">**displayName** — отображаемое имя ссылки.</span><span class="sxs-lookup"><span data-stu-id="b6a36-167">**displayName** - The display name of the link.</span></span>
- <span data-ttu-id="b6a36-168">**isWebRelative** — значение True, если ссылка указывается относительно сайта. В противном случае используется значение False.</span><span class="sxs-lookup"><span data-stu-id="b6a36-168">**isWebRelative** - True if the link is web relative; otherwise, false.</span></span>

<span data-ttu-id="b6a36-169">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-169">Example:</span></span>

> [!NOTE]
> <span data-ttu-id="b6a36-170">При добавлении ссылки на вложенный элемент сайта (например, список) обязательно указывайте путь от корневого сайта.</span><span class="sxs-lookup"><span data-stu-id="b6a36-170">If you add a link to a nested site item - like a list - be sure to add the path reference from the root.</span></span> 


```json
{
   "verb": "addNavLink",
   "url": "/Customer Event Collateral",
   "displayName": "Event Collateral",
   "isWebRelative": true
},
{
   "verb": "addNavLink",
   "url": "/Lists/Project Activities",
   "displayName": "Project Activities",
   "isWebRelative": true
 }
```

## <a name="apply-a-theme"></a><span data-ttu-id="b6a36-171">Применение темы</span><span class="sxs-lookup"><span data-stu-id="b6a36-171">Apply a theme</span></span>

<span data-ttu-id="b6a36-172">Чтобы добавить на сайт собственную тему, используйте команду **applyTheme**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-172">Use the **applyTheme** verb to add a custom theme to the site.</span></span> <span data-ttu-id="b6a36-173">Дополнительные сведения о создании и добавлении тем см. в статье [Настройка тем SharePoint](site-theming/sharepoint-site-theming-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a36-173">For more information on how to construct and upload these themes, see [SharePoint site theming](site-theming/sharepoint-site-theming-overview.md).</span></span> <span data-ttu-id="b6a36-174">Обратите внимание, что эта команда подходит только для применения собственных тем. Чтобы применить одну из встроенных тем SharePoint, скопируйте ее и добавьте ссылку на копию.</span><span class="sxs-lookup"><span data-stu-id="b6a36-174">Note that this site action only works for applying custom themes; to apply one of our in-product SharePoint themes, create a copy as a custom one and reference that one.</span></span>

<span data-ttu-id="b6a36-175">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-175">JSON value:</span></span>

- <span data-ttu-id="b6a36-176">**themeName** — имя применяемой темы.</span><span class="sxs-lookup"><span data-stu-id="b6a36-176">**themeName** - The name of the theme to apply.</span></span>

<span data-ttu-id="b6a36-177">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-177">Example:</span></span>

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

## <a name="set-a-site-logo"></a><span data-ttu-id="b6a36-178">Установка логотипа сайта</span><span class="sxs-lookup"><span data-stu-id="b6a36-178">Set a site logo</span></span>

<span data-ttu-id="b6a36-179">Чтобы указать логотип для сайта, используйте команду **setSiteLogo**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-179">Use the **setSiteLogo** verb to specify a logo for your site.</span></span> <span data-ttu-id="b6a36-180">Это действие работает только с шаблоном сайта для общения (68).</span><span class="sxs-lookup"><span data-stu-id="b6a36-180">This action only works on the communication site template (68).</span></span>

<span data-ttu-id="b6a36-181">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-181">JSON value:</span></span>

- <span data-ttu-id="b6a36-182">**url** — URL-адрес изображения логотипа.</span><span class="sxs-lookup"><span data-stu-id="b6a36-182">**url** - The url of the logo image to use.</span></span>

<span data-ttu-id="b6a36-183">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-183">Example:</span></span>

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a><span data-ttu-id="b6a36-184">Присоединение к сайту-концентратору</span><span class="sxs-lookup"><span data-stu-id="b6a36-184">Join a hub site</span></span>

<span data-ttu-id="b6a36-185">Чтобы присоединить сайт к назначенному центральному сайту, используйте команду **joinHubSite**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-185">Use the **joinHubSite** verb to join the site to a hub.</span></span> 

<span data-ttu-id="b6a36-186">Значение JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-186">JSON value:</span></span>

- <span data-ttu-id="b6a36-187">**hubSiteId** — ИД подключаемого сайта-концентратора.</span><span class="sxs-lookup"><span data-stu-id="b6a36-187">**hubSiteId** - The ID of the hub site to join.</span></span>

<span data-ttu-id="b6a36-188">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-188">Example:</span></span>

<!-- TBD: add link to Dave's hub site documentation -->

> [!NOTE]
> <span data-ttu-id="b6a36-189">Центральные сайты представляют собой новые возможности, которые впервые предложены пользователям в выпуске Targeted в марте 2018.</span><span class="sxs-lookup"><span data-stu-id="b6a36-189">Hub sites are a new feature that are just rolling out to customers in Targeted Release in March 2018.</span></span> 

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a><span data-ttu-id="b6a36-190">Вызов потока</span><span class="sxs-lookup"><span data-stu-id="b6a36-190">Trigger a flow</span></span>

<span data-ttu-id="b6a36-191">Чтобы запустить настраиваемый поток, используйте команду **triggerFlow**.</span><span class="sxs-lookup"><span data-stu-id="b6a36-191">Use the **triggerFlow** verb to kick off a custom flow.</span></span>
<!-- update this with example from trigger workflow topic -->

<span data-ttu-id="b6a36-192">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-192">JSON values:</span></span>

- <span data-ttu-id="b6a36-193">**url** — URL-адрес для вызова потока.</span><span class="sxs-lookup"><span data-stu-id="b6a36-193">**url** - A trigger URL of the flow.</span></span>
- <span data-ttu-id="b6a36-194">**name** — имя потока.</span><span class="sxs-lookup"><span data-stu-id="b6a36-194">**name** - The name of the flow.</span></span>
- <span data-ttu-id="b6a36-195">**parameters** — набор необязательных параметров, передаваемых в поток.</span><span class="sxs-lookup"><span data-stu-id="b6a36-195">**parameters** - An optional set of parameters to pass into the flow.</span></span>

<span data-ttu-id="b6a36-196">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-196">Example:</span></span>

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
## <a name="setsiteexternalsharingcapability"></a><span data-ttu-id="b6a36-197">setSiteExternalSharingCapability</span><span class="sxs-lookup"><span data-stu-id="b6a36-197">setSiteExternalSharingCapability</span></span>

<span data-ttu-id="b6a36-198">Действие **setSiteExternalSharingCapability** используется для управления гостевым доступом.</span><span class="sxs-lookup"><span data-stu-id="b6a36-198">Use the **setSiteExternalSharingCapability** to manage guest access.</span></span> <span data-ttu-id="b6a36-199">Дополнительные сведения об этих параметрах см. на странице: https://support.office.com/ru-ru/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85</span><span class="sxs-lookup"><span data-stu-id="b6a36-199">For details on these settings refer to: https://support.office.com/en-us/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85</span></span>

<!-- update this table matrix -->

<span data-ttu-id="b6a36-200">Значения JSON:</span><span class="sxs-lookup"><span data-stu-id="b6a36-200">JSON values:</span></span>

- <span data-ttu-id="b6a36-201">**capability** — обязательный параметр, указывающий варианты предоставления доступа для семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="b6a36-201">**capability** - A required parameter to specify the sharing option for the site collection.</span></span> <span data-ttu-id="b6a36-202">Возможно четыре варианта: Disabled, ExistingExternalUserSharingOnly, ExternalUserSharingOnly, ExternalUserAndGuestSharing</span><span class="sxs-lookup"><span data-stu-id="b6a36-202">The four options are: Disabled, ExistingExternalUserSharingOnly, ExternalUserSharingOnly, ExternalUserAndGuestSharing</span></span>

<span data-ttu-id="b6a36-203">Пример:</span><span class="sxs-lookup"><span data-stu-id="b6a36-203">Example:</span></span>

```json
{
   "verb": "setSiteExternalSharingCapability",
   "capability": "Disabled"
}
```
