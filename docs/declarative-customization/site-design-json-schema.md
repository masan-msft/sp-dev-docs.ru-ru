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
# <a name="site-design-json-schema"></a>Схема JSON для макетов сайтов

Макет сайта представляет собой список действий. Сложные действия, например создание списка, также содержат вложенные действия. Каждое действие указывается с помощью значения verb (команды). Действия-команды выполняются в том порядке, в котором они указаны в скрипте JSON. Используйте только указанные здесь действия-команды, иначе при попытке загрузить скрипт сайта возникнет ошибка "не удается обработать действие". Со временем список действий будет расширяться. 

Общая структура JSON выглядит так:

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

## <a name="create-a-new-sharepoint-list"></a>Создание списка SharePoint

Используйте команду **createSPList** для создания списка SharePoint.

Значения JSON:

- **listName** — имя списка, которое видят пользователи.
- **templateType** — тип шаблона, применяемый к списку. Как правило, используется значение 100. Значения типов шаблонов указываются в [перечислении SPListTemplateType](https://msdn.microsoft.com/ru-RU/library/microsoft.sharepoint.splisttemplatetype.aspx).
- **subactions** — массив действий, выполняемых в указанном порядке для создания списка.

Пример:

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

Массив дочерних действий содержит дополнительные действия для создания списка. Вложенные действия также указываются с помощью значения **verb**.

### <a name="settitle"></a>setTitle

Задает название, обозначающее список в представлениях.

Значение JSON:

- **title** — название списка.

Пример:

```json
{
   "verb": "setTitle",
   "title": "Customers and Orders"
}
```

### <a name="setdescription"></a>setDescription

Задает описание списка.

Значение JSON:

- **description** — описание нового списка.

Пример:

```json
{
   "verb": "setDescription",
   "description": "List of Customers and Orders"
}
```

### <a name="addspfield"></a>addSPField

Добавляет новое поле.

Значения JSON:

- **fieldType** — можно задать тип поля **Text**, **Note**, **Number**, **Boolean**, **User** или **DateTime**.
- **displayName** — отображаемое имя поля.
- **isRequired** — значение True, если это поле обязательно должно содержать данные. В противном случае используется значение False.
- **addToDefaultView** — значение True, если поле будет добавлено в представление по умолчанию. В противном случае используется значение False.

Пример:

```json
{
   "verb": "addSPField",
   "fieldType": "Text",
   "displayName": "Customer Name",
   "isRequired": false,
   "addToDefaultView": true
}
```

### <a name="deletespfield"></a>deleteSPField

Удаляет стандартное поле, предоставленное выбранным типом шаблона.

Значение JSON:

- **displayName** — отображаемое имя удаляемого поля.

Пример:

```json
{
   "verb": "deleteSPField",
   "displayName": "Modified"
}
```

### <a name="addcontenttype"></a>addContentType

Добавляет тип контента в список. В настоящее время доступны только ограниченные типы контента по умолчанию, которые включены в шаблон сайта.

Значение JSON:

- **name** — имя добавляемого типа контента.

Пример:

```json
{
   "verb": "addContentType",
   "name": "name"
}
```

### <a name="removecontenttype"></a>removeContentType

Удаляет тип контента, предоставленный выбранным типом шаблона.

Значение JSON:

- **name** — имя удаляемого типа контента.

Пример:

```json
{
   "verb": "removeContentType",
   "name": "name"
}
```

### <a name="setspfieldcustomformatter"></a>setSPFieldCustomFormatter

Задает форматирование столбца для поля. Дополнительные сведения о форматировании столбцов см. в статье [Настройка SharePoint с помощью форматирования столбцов](column-formatting.md).

Значения JSON:

- **fieldDisplayName** — отображаемое имя обрабатываемого поля.
- **formatterJSON** — объект JSON, используемый в качестве ресурса CustomFormatter для поля.

Пример. В этом примере показано форматирование столбца чисел для его отображения в виде гистограммы

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

## <a name="add-a-navigation-link"></a>Добавление ссылки для перехода

Чтобы добавить на сайт ссылку для перехода, используйте команду **addNavLink**. 

Значения JSON:

- **url** — URL-адрес добавляемой ссылки.
- **displayName** — отображаемое имя ссылки.
- **isWebRelative** — значение True, если ссылка указывается относительно сайта. В противном случае используется значение False.

Пример:

> [!NOTE]
> При добавлении ссылки на вложенный элемент сайта (например, список) обязательно указывайте путь от корневого сайта. 


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

## <a name="apply-a-theme"></a>Применение темы

Чтобы добавить на сайт собственную тему, используйте команду **applyTheme**. Дополнительные сведения о создании и добавлении тем см. в статье [Настройка тем SharePoint](site-theming/sharepoint-site-theming-overview.md). Обратите внимание, что эта команда подходит только для применения собственных тем. Чтобы применить одну из встроенных тем SharePoint, скопируйте ее и добавьте ссылку на копию.

Значение JSON:

- **themeName** — имя применяемой темы.

Пример:

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

## <a name="set-a-site-logo"></a>Установка логотипа сайта

Чтобы указать логотип для сайта, используйте команду **setSiteLogo**. Это действие работает только с шаблоном сайта для общения (68).

Значение JSON:

- **url** — URL-адрес изображения логотипа.

Пример:

```json
{
    "verb": "setSiteLogo",
    "url": "/Customer Event Collateral/logo.jpg"
}
```

## <a name="join-a-hub-site"></a>Присоединение к сайту-концентратору

Чтобы присоединить сайт к назначенному центральному сайту, используйте команду **joinHubSite**. 

Значение JSON:

- **hubSiteId** — ИД подключаемого сайта-концентратора.

Пример:

<!-- TBD: add link to Dave's hub site documentation -->

> [!NOTE]
> Центральные сайты представляют собой новые возможности, которые впервые предложены пользователям в выпуске Targeted в марте 2018. 

```json
{
    "verb": "joinHubSite",
    "hubSiteId": "e337cc17-b355-45d2-8dd4-e056f1bcf6f6"
}
```

## <a name="trigger-a-flow"></a>Вызов потока

Чтобы запустить настраиваемый поток, используйте команду **triggerFlow**.
<!-- update this with example from trigger workflow topic -->

Значения JSON:

- **url** — URL-адрес для вызова потока.
- **name** — имя потока.
- **parameters** — набор необязательных параметров, передаваемых в поток.

Пример:

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
## <a name="setsiteexternalsharingcapability"></a>setSiteExternalSharingCapability

Действие **setSiteExternalSharingCapability** используется для управления гостевым доступом. Дополнительные сведения об этих параметрах см. на странице: https://support.office.com/ru-ru/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85

<!-- update this table matrix -->

Значения JSON:

- **capability** — обязательный параметр, указывающий варианты предоставления доступа для семейства веб-сайтов. Возможно четыре варианта: Disabled, ExistingExternalUserSharingOnly, ExternalUserSharingOnly, ExternalUserAndGuestSharing

Пример:

```json
{
   "verb": "setSiteExternalSharingCapability",
   "capability": "Disabled"
}
```
