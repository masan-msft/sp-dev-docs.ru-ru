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
# <a name="configure-web-part-icon"></a><span data-ttu-id="a59ba-102">Настройка значка веб-части</span><span class="sxs-lookup"><span data-stu-id="a59ba-102">Configure web part.</span></span>

<span data-ttu-id="a59ba-103">Выбрав значок, иллюстрирующий назначение веб-части, вы поможете пользователям находить ее среди остальных веб-частей, доступных на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="a59ba-103">Selecting an icon that illustrates the purpose of your web part, makes it easier for users to find your web part among other all web parts available in the toolbox.</span></span> <span data-ttu-id="a59ba-104">В этой статье описываются различные способы, которыми вы можете настраивать значки для своих веб-частей.</span><span class="sxs-lookup"><span data-stu-id="a59ba-104">This article explains the different options available to you to configure the icon for your web parts.</span></span>

## <a name="preconfiguring-web-parts"></a><span data-ttu-id="a59ba-105">Предварительная настройка веб-частей</span><span class="sxs-lookup"><span data-stu-id="a59ba-105">Preconfiguring web parts</span></span>

<span data-ttu-id="a59ba-106">Значок веб-части определяется в ее манифесте среди заранее настроенных записей.</span><span class="sxs-lookup"><span data-stu-id="a59ba-106">Web part icon is defined in the web part manifest as a part of preconfigured entries.</span></span> <span data-ttu-id="a59ba-107">Если у вашей веб-части несколько назначений и ее можно настраивать в соответствии с потребностями пользователя, то для каждой конфигурации можно задать отдельный значок, указывающий ее назначение.</span><span class="sxs-lookup"><span data-stu-id="a59ba-107">If you have a multipurpose web part, that can be configured to meet different needs, each configuration can have a different icon indicating its purpose.</span></span> <span data-ttu-id="a59ba-108">Наглядный значок поможет пользователям находить нужную веб-часть.</span><span class="sxs-lookup"><span data-stu-id="a59ba-108">Using a representative icon helps users find the web part they are looking for.</span></span> <span data-ttu-id="a59ba-109">Дополнительные сведения о предварительной настройке веб-частей см. в [этом руководстве](../guidance/simplify-adding-web-parts-with-preconfigured-entries.md).</span><span class="sxs-lookup"><span data-stu-id="a59ba-109">For more information about preconfiguring your web parts see the [guidance on preconfiguring web parts](../guidance/simplify-adding-web-parts-with-preconfigured-entries.md).</span></span>

## <a name="configuring-web-part-icon"></a><span data-ttu-id="a59ba-110">Настройка значка веб-части</span><span class="sxs-lookup"><span data-stu-id="a59ba-110">Configuring web part icon</span></span>

<span data-ttu-id="a59ba-111">В SharePoint Framework доступен ряд способов определения значков для веб-частей.</span><span class="sxs-lookup"><span data-stu-id="a59ba-111">SharePoint Framework offers you a number of ways to define the icon for your web part.</span></span>

### <a name="using-office-ui-fabric-icon-font"></a><span data-ttu-id="a59ba-112">Использование шрифта значков Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="a59ba-112">Using Office UI Fabric icon font</span></span>

<span data-ttu-id="a59ba-113">Один из способов определения значка для веб-части — использование свойства **officeFabricIconFontName**.</span><span class="sxs-lookup"><span data-stu-id="a59ba-113">One way to define the icon for your web part is by using the **officeFabricIconFontName** property.</span></span> <span data-ttu-id="a59ba-114">С помощью этого свойства можно выбрать один из значков, входящих в состав Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="a59ba-114">This property allows you to choose one of the icons offered as a part of Office UI Fabric.</span></span>

> <span data-ttu-id="a59ba-115">Список доступных значков Office UI Fabric представлен на странице [https://developer.microsoft.com/ru-ru/fabric#/styles/icons](https://developer.microsoft.com/ru-RU/fabric#/styles/icons).</span><span class="sxs-lookup"><span data-stu-id="a59ba-115">You can find the list of available Office UI Fabric icons at [https://developer.microsoft.com/ru-RU/fabric#/styles/icons](https://developer.microsoft.com/ru-RU/fabric#/styles/icons).</span></span>

<span data-ttu-id="a59ba-116">Чтобы использовать определенный значок, скопируйте его имя со страницы обзора значков Office UI Fabric и вставьте в качестве значения свойства **officeFabricIconFontName** в манифесте веб-части.</span><span class="sxs-lookup"><span data-stu-id="a59ba-116">To use the specific icon, from the Office UI Fabric icons overview page, copy its name, and paste as the value of the **officeFabricIconFontName** property in the manifest of your web part.</span></span>

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

<span data-ttu-id="a59ba-118">При добавлении веб-части на страницу выбранный значок будет отображаться на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="a59ba-118">When adding your web part to the page, the selected icon will be displayed in the toolbox.</span></span>

![Выбранный значок Office UI Fabric, представляющий веб-часть на панели элементов](../../../images/webparticon_toolbox_officeuifabricicon.png)

<span data-ttu-id="a59ba-120">Большое преимущество этого подхода заключается в том, что файл изображения значка не требуется развертывать вместе с ресурсами веб-части.</span><span class="sxs-lookup"><span data-stu-id="a59ba-120">The big benefit of this approach is, that you don't need to deploy the icon image file along with your web part assets.</span></span> <span data-ttu-id="a59ba-121">Кроме того, на компьютерах с другим разрешением или другими параметрами специальных возможностей значок будет автоматически адаптироваться без потери качества.</span><span class="sxs-lookup"><span data-stu-id="a59ba-121">Additionally, on computers using different DPI or other accessibility settings, the icon will automatically adapt to these settings without losing quality.</span></span>

### <a name="using-an-external-icon-image"></a><span data-ttu-id="a59ba-122">Использование внешнего изображения для значка</span><span class="sxs-lookup"><span data-stu-id="a59ba-122">Using an external icon image</span></span>

<span data-ttu-id="a59ba-123">Несмотря на то что Office UI Fabric предоставляет множество изображений, при создании веб-частей вам может потребоваться использовать значок, относящийся к вашей организации, чтобы четко отделить свои веб-части от других веб-частей (как собственных, так и сторонних) на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="a59ba-123">Although Office UI Fabric offers many images, when building web parts, you might want to use something specific to your organization to clearly separate your web parts from other first and third party web parts visible in the toolbox.</span></span>

<span data-ttu-id="a59ba-124">Помимо значков Office UI Fabric, на платформе SharePoint Framework также можно использовать изображения.</span><span class="sxs-lookup"><span data-stu-id="a59ba-124">Next to using Office UI Fabric icons, SharePoint Framework also allows you to use images.</span></span> <span data-ttu-id="a59ba-125">Чтобы использовать изображение в качестве значка веб-части, укажите его абсолютный URL-адрес в свойстве **iconImageUrl** в манифесте веб-части.</span><span class="sxs-lookup"><span data-stu-id="a59ba-125">To use an image as a web part icon, specify its absolute URL in the **iconImageUrl** property in the web part manifest.</span></span>

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

<span data-ttu-id="a59ba-126">Размер значка веб-части, отображаемого на панели элементов, составляет 40 x 28 пикселей.</span><span class="sxs-lookup"><span data-stu-id="a59ba-126">The web part icon image displayed in the toolbox is 40x28px.</span></span> <span data-ttu-id="a59ba-127">Если указано изображение большего размера, оно будет уменьшено с сохранением пропорций.</span><span class="sxs-lookup"><span data-stu-id="a59ba-127">If your image is bigger, it will be sized proportionally to match these dimensions.</span></span>

![Пользовательское изображение, используемое в качестве значка веб-части на панели элементов](../../../images/webparticon_toolbox_imagepng.png)

<span data-ttu-id="a59ba-129">Использование пользовательских изображений обеспечивает более широкие возможности выбора значка для веб-части, но при этом их требуется развертывать вместе с другими ресурсами веб-части.</span><span class="sxs-lookup"><span data-stu-id="a59ba-129">While using custom images gives you more flexibility to choose an icon for your web part, it requires you to deploy them along with your other web part assets.</span></span> <span data-ttu-id="a59ba-130">Кроме того, качество изображения может снизиться при использовании высокого разрешения или некоторых специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="a59ba-130">Additionally, your image might lose quality when displayed in higher DPI or specific accessibility settings.</span></span> <span data-ttu-id="a59ba-131">Во избежание снижения качества можно использовать векторные изображения в формате SVG, которые также поддерживаются на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="a59ba-131">To avoid quality loss, you can use vector-based SVG images which are also supported by the SharePoint Framework.</span></span>

### <a name="using-a-base64-encoded-image"></a><span data-ttu-id="a59ba-132">Использование изображения в кодировке Base64</span><span class="sxs-lookup"><span data-stu-id="a59ba-132">Using a base64 encoded image</span></span>

<span data-ttu-id="a59ba-133">Если применяется пользовательское изображение, можно не указывать абсолютный URL-адрес файла изображения, размещенного вместе с другими ресурсами веб-части, а закодировать изображение в формате Base64 и использовать строку Base64 вместо URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="a59ba-133">When using a custom image, rather than specifying an absolute URL to the image file hosted together with other web part assets, you can have your image base64 encoded and use the base64 string instead of the URL.</span></span>

> <span data-ttu-id="a59ba-134">В Интернете доступен ряд служб, с помощью которых можно закодировать изображение в формате Base64, например [https://www.base64-image.de](https://www.base64-image.de).</span><span class="sxs-lookup"><span data-stu-id="a59ba-134">There are a number of services available on the Internet that you can use to base64 encode your image, such as [https://www.base64-image.de](https://www.base64-image.de).</span></span>

<span data-ttu-id="a59ba-135">После кодирования изображения скопируйте строку Base64 и используйте ее в качестве значения свойства **iconImageUrl** в манифесте веб-части.</span><span class="sxs-lookup"><span data-stu-id="a59ba-135">After encoding the image, copy the base64 string and use it as the value for the **iconImageUrl** property in the web part manifest.</span></span>

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

<span data-ttu-id="a59ba-137">Кодировка Base64 подходит как для растровых изображений (например, PNG-файлов), так и для векторных изображений в формате SVG.</span><span class="sxs-lookup"><span data-stu-id="a59ba-137">Base64 encoding works both for bitmap images such as PNG as well as vector SVG images.</span></span> <span data-ttu-id="a59ba-138">Значительное преимущество использования изображений в кодировке Base64 заключается в том, что изображение значка веб-части необходимо развернуть отдельно.</span><span class="sxs-lookup"><span data-stu-id="a59ba-138">The big benefit of using base64 encoded images is, that you don't need to deploy the web part icon image separately.</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="a59ba-139">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="a59ba-139">Additional considerations</span></span>

<span data-ttu-id="a59ba-140">У каждой веб-части должен быть значок.</span><span class="sxs-lookup"><span data-stu-id="a59ba-140">Each web part must have an icon.</span></span> <span data-ttu-id="a59ba-141">Если значок веб-части указывается с помощью свойств **officeFabricIconFontName** и **iconImageUrl**, будет использоваться значок, указанный в свойстве **officeFabricIconFontName**.</span><span class="sxs-lookup"><span data-stu-id="a59ba-141">If you specify the web part icon using both the **officeFabricIconFontName** and the **iconImageUrl** properties, the icon specified in the **officeFabricIconFontName** will be used.</span></span> <span data-ttu-id="a59ba-142">Если значок Office UI Fabric не используется, необходимо указать URL-адрес в свойстве **iconImageUrl**.</span><span class="sxs-lookup"><span data-stu-id="a59ba-142">If you choose not to use an Office UI Fabric icon, then you have to specify a URL in the **iconImageUrl** property.</span></span>