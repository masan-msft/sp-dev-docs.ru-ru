---
title: "Настройка значка веб-части"
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 672f0cc67a47ff42756638798448f03085f36a9d
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="configure-web-part-icon"></a>Настройка значка веб-части

Выбрав значок, иллюстрирующий назначение веб-части, вы поможете пользователям находить ее среди остальных веб-частей, доступных на панели элементов. В этой статье описываются различные способы, которыми вы можете настраивать значки для своих веб-частей.

## <a name="preconfiguring-web-parts"></a>Предварительная настройка веб-частей

Значок веб-части определяется в ее манифесте среди заранее настроенных записей. Если у вашей веб-части несколько назначений и ее можно настраивать в соответствии с потребностями пользователя, то для каждой конфигурации можно задать отдельный значок, указывающий ее назначение. Наглядный значок поможет пользователям находить нужную веб-часть. Дополнительные сведения о предварительной настройке веб-частей см. в [этом руководстве](../guidance/simplify-adding-web-parts-with-preconfigured-entries.md).

## <a name="configuring-web-part-icon"></a>Настройка значка веб-части

В SharePoint Framework доступен ряд способов определения значков для веб-частей.

### <a name="using-office-ui-fabric-icon-font"></a>Использование шрифта значков Office UI Fabric

Один из способов определения значка для веб-части — использование свойства **officeFabricIconFontName**. С помощью этого свойства можно выбрать один из значков, входящих в состав Office UI Fabric.

> Список доступных значков Office UI Fabric представлен на странице [https://developer.microsoft.com/ru-ru/fabric#/styles/icons](https://developer.microsoft.com/ru-RU/fabric#/styles/icons).

Чтобы использовать определенный значок, скопируйте его имя со страницы обзора значков Office UI Fabric и вставьте в качестве значения свойства **officeFabricIconFontName** в манифесте веб-части.

![Стрелка от имени значка на странице с обзором значков Office UI Fabric к коду манифеста веб-части](../../../images/webparticon_officeuifabricicon.png)

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "bcae7077-85cb-41a0-b3d3-2084f268a211",
  "alias": "WeatherWebPart",
  "componentType": "WebPart",
  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,
  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,
  "preconfiguredEntries": [
    {
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": {
        "default": "Other"
      },
      "title": {
        "default": "Weather"
      },
      "description": {
        "default": "Shows current weather in the given location"
      },
      "officeFabricIconFontName": "Sunny",
      "properties": {
        "location": "Munich"
      }
    }
  ]
}
```

При добавлении веб-части на страницу выбранный значок будет отображаться на панели элементов.

![Выбранный значок Office UI Fabric, представляющий веб-часть на панели элементов](../../../images/webparticon_toolbox_officeuifabricicon.png)

Большое преимущество этого подхода заключается в том, что файл изображения значка не требуется развертывать вместе с ресурсами веб-части. Кроме того, на компьютерах с другим разрешением или другими параметрами специальных возможностей значок будет автоматически адаптироваться без потери качества.

### <a name="using-an-external-icon-image"></a>Использование внешнего изображения для значка

Несмотря на то что Office UI Fabric предоставляет множество изображений, при создании веб-частей вам может потребоваться использовать значок, относящийся к вашей организации, чтобы четко отделить свои веб-части от других веб-частей (как собственных, так и сторонних) на панели элементов.

Помимо значков Office UI Fabric, на платформе SharePoint Framework также можно использовать изображения. Чтобы использовать изображение в качестве значка веб-части, укажите его абсолютный URL-адрес в свойстве **iconImageUrl** в манифесте веб-части.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "bcae7077-85cb-41a0-b3d3-2084f268a211",
  "alias": "WeatherWebPart",
  "componentType": "WebPart",
  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,
  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,
  "preconfiguredEntries": [
    {
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": {
        "default": "Other"
      },
      "title": {
        "default": "Weather"
      },
      "description": {
        "default": "Shows current weather in the given location"
      },
      "iconImageUrl": "https://assets.contoso.com/weather.png",
      "properties": {
        "location": "Munich"
      }
    }
  ]
}
```

Размер значка веб-части, отображаемого на панели элементов, составляет 40 x 28 пикселей. Если указано изображение большего размера, оно будет уменьшено с сохранением пропорций.

![Пользовательское изображение, используемое в качестве значка веб-части на панели элементов](../../../images/webparticon_toolbox_imagepng.png)

Использование пользовательских изображений обеспечивает более широкие возможности выбора значка для веб-части, но при этом их требуется развертывать вместе с другими ресурсами веб-части. Кроме того, качество изображения может снизиться при использовании высокого разрешения или некоторых специальных возможностей. Во избежание снижения качества можно использовать векторные изображения в формате SVG, которые также поддерживаются на платформе SharePoint Framework.

### <a name="using-a-base64-encoded-image"></a>Использование изображения в кодировке Base64

Если применяется пользовательское изображение, можно не указывать абсолютный URL-адрес файла изображения, размещенного вместе с другими ресурсами веб-части, а закодировать изображение в формате Base64 и использовать строку Base64 вместо URL-адреса.

> В Интернете доступен ряд служб, с помощью которых можно закодировать изображение в формате Base64, например [https://www.base64-image.de](https://www.base64-image.de).

После кодирования изображения скопируйте строку Base64 и используйте ее в качестве значения свойства **iconImageUrl** в манифесте веб-части.

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "bcae7077-85cb-41a0-b3d3-2084f268a211",
  "alias": "WeatherWebPart",
  "componentType": "WebPart",
  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,
  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,
  "preconfiguredEntries": [
    {
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": {
        "default": "Other"
      },
      "title": {
        "default": "Weather"
      },
      "description": {
        "default": "Shows current weather in the given location"
      },
      "iconImageUrl": "data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMTAyMiIgaGVpZ2h0PSI5NzgiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6c3ZnPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CiA8Zz4KICA8dGl0bGU+TGF5ZXIgMTwvdGl...",
      "properties": {
        "location": "Munich"
      }
    }
  ]
}
```

![Изображение в кодировке Base64, отображаемое в качестве значка веб-части на панели элементов](../../../images/webparticon_toolbox_base64.png)

Кодировка Base64 подходит как для растровых изображений (например, PNG-файлов), так и для векторных изображений в формате SVG. Значительное преимущество использования изображений в кодировке Base64 заключается в том, что изображение значка веб-части необходимо развернуть отдельно.

## <a name="additional-considerations"></a>Дополнительные сведения

У каждой веб-части должен быть значок. Если значок веб-части указывается с помощью свойств **officeFabricIconFontName** и **iconImageUrl**, будет использоваться значок, указанный в свойстве **officeFabricIconFontName**. Если значок Office UI Fabric не используется, необходимо указать URL-адрес в свойстве **iconImageUrl**.