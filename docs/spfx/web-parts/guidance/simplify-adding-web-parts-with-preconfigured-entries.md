---
title: "Упрощенное добавление веб-частей с помощью предварительно настроенных записей"
description: "Используйте предварительно настроенные записи в клиентской веб-части SharePoint Framework, чтобы предоставлять пользователям уже настроенные версии веб-части."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: a77add94c3a099dc8c81123a0a7defd8f9ee370a
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="simplify-adding-web-parts-with-preconfigured-entries"></a><span data-ttu-id="2d424-103">Упрощенное добавление веб-частей с помощью предварительно настроенных записей</span><span class="sxs-lookup"><span data-stu-id="2d424-103">Simplify adding web parts with preconfigured entries</span></span>

<span data-ttu-id="2d424-104">Сложные клиентские веб-части SharePoint Framework часто содержат много свойств, которые необходимо настраивать пользователю.</span><span class="sxs-lookup"><span data-stu-id="2d424-104">More complex SharePoint Framework client-side web parts likely have many properties that the user must configure.</span></span> <span data-ttu-id="2d424-105">Вы можете помочь пользователям, добавив предварительно настроенные записи свойств для определенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="2d424-105">You can help users by adding preconfigured property entries for specific scenarios.</span></span> <span data-ttu-id="2d424-106">Такая запись инициализирует веб-часть, используя предварительно заданные значения.</span><span class="sxs-lookup"><span data-stu-id="2d424-106">A preconfigured entry initializes the web part with pre-set values.</span></span>

> [!NOTE] 
> <span data-ttu-id="2d424-107">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки для создания клиентских веб-частей SharePoint](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="2d424-107">Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="web-part-preconfigured-entries"></a><span data-ttu-id="2d424-108">Предварительно настроенные записи веб-части</span><span class="sxs-lookup"><span data-stu-id="2d424-108">What are web part preconfigured entries</span></span>

<span data-ttu-id="2d424-109">Каждая клиентская веб-часть SharePoint Framework состоит из двух частей:</span><span class="sxs-lookup"><span data-stu-id="2d424-109">Each SharePoint Framework client-side web part consists of two pieces: the manifest, that describes the web part, and the web part code.</span></span> 

- <span data-ttu-id="2d424-110">манифест, описывающий веб-часть;</span><span class="sxs-lookup"><span data-stu-id="2d424-110">The manifest that describes the web part</span></span>
- <span data-ttu-id="2d424-111">код веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-111">The web part code</span></span>

<span data-ttu-id="2d424-112">Среди свойств, указанных в манифесте веб части, есть свойство **preconfiguredEntries**.</span><span class="sxs-lookup"><span data-stu-id="2d424-112">One of the properties specified in the web part manifest is the **preconfiguredEntries** property.</span></span>

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "6737645a-4443-4210-a70e-e5e2a219133a",
  "alias": "GalleryWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,

  "preconfiguredEntries": [{
    "groupId": "1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489", // Discover
    "group": { "default": "Under Development" },
    "title": { "default": "Gallery" },
    "description": { "default": "Shows items from the selected list" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "Gallery"
    }
  }]
}
```

<span data-ttu-id="2d424-p102">Свойство **preconfiguredEntries** предоставляет сведения о веб-части, которые используются на панели элементов. Когда пользователь добавляет веб-часть на страницу, данные из свойства **preconfiguredEntries** используются для отображения веб-части на панели элементов и определения ее параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d424-p102">The **preconfiguredEntries** property provides information about your web part for use in the web part toolbox. When users add web parts to the page, the information from the **preconfiguredEntries** property is used to display the web part in the toolbox and define its default settings when it's added to the page.</span></span>

<span data-ttu-id="2d424-115">Если вы уже создавали классические веб-части, включающие решения с полным доверием, можете рассматривать каждую запись в массиве **preconfiguredEntries** как соответствующий **WEBPART**-файл.</span><span class="sxs-lookup"><span data-stu-id="2d424-115">If you've built classic web parts with full-trust solutions, you can think of each entry in the **preconfiguredEntries** array as corresponding to a **.webpart** file.</span></span> <span data-ttu-id="2d424-116">Как и **WEBPART**-файл, каждая запись в свойстве **preconfiguredEntries** связана с кодом веб-части и задает основные сведения о ней, например название или описание, а также значения свойств по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d424-116">If you've built classic web parts with full-trust solutions, then you can think of each entry in the preconfiguredEntries array as corresponding to a .webpart file. Just like a **.webpart** file, each entry in the **preconfiguredEntries** property is linked to the web part code and specifies basic information about the web part such as its title or description as well as default values for its properties.</span></span>

### <a name="properties-of-a-preconfiguredentries-array-item"></a><span data-ttu-id="2d424-117">Свойства элемента массива **preconfiguredEntries**</span><span class="sxs-lookup"><span data-stu-id="2d424-117">Properties of a **preconfiguredEntries** array item</span></span>

<span data-ttu-id="2d424-p104">Каждый элемент массива **preconfiguredEntries** состоит из нескольких свойств. В приведенной ниже таблице описывается назначение каждого свойства.</span><span class="sxs-lookup"><span data-stu-id="2d424-p104">Each item in the **preconfiguredEntries** array consists of several properties. The following table explains the purpose of each property.</span></span>

|<span data-ttu-id="2d424-120">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="2d424-120">Property name</span></span> |<span data-ttu-id="2d424-121">Тип значения</span><span class="sxs-lookup"><span data-stu-id="2d424-121">Value type</span></span> |<span data-ttu-id="2d424-122">Обязательное</span><span class="sxs-lookup"><span data-stu-id="2d424-122">Required</span></span>  |<span data-ttu-id="2d424-123">Назначение</span><span class="sxs-lookup"><span data-stu-id="2d424-123">Purpose</span></span>  |<span data-ttu-id="2d424-124">Пример значения</span><span class="sxs-lookup"><span data-stu-id="2d424-124">Sample value</span></span> |
|:-------------|:----------|:--------:|:---------|:-------------|
|<span data-ttu-id="2d424-125">title</span><span class="sxs-lookup"><span data-stu-id="2d424-125">title</span></span>         |<span data-ttu-id="2d424-126">ILocalizedString</span><span class="sxs-lookup"><span data-stu-id="2d424-126">ILocalizedString</span></span> |<span data-ttu-id="2d424-127">Да</span><span class="sxs-lookup"><span data-stu-id="2d424-127">yes</span></span> |<span data-ttu-id="2d424-128">Название веб-части, которое отображается на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="2d424-128">The web part title that is displayed in the toolbox.</span></span> |`"title": { "default": "Weather", "nl-nl": "Weerbericht" }`|
|<span data-ttu-id="2d424-129">description</span><span class="sxs-lookup"><span data-stu-id="2d424-129">description</span></span>             |<span data-ttu-id="2d424-130">ILocalizedString</span><span class="sxs-lookup"><span data-stu-id="2d424-130">ILocalizedString</span></span>|<span data-ttu-id="2d424-131">Да</span><span class="sxs-lookup"><span data-stu-id="2d424-131">yes</span></span>     |<span data-ttu-id="2d424-132">Описание веб-части, которое отображается в подсказках панели элементов.</span><span class="sxs-lookup"><span data-stu-id="2d424-132">The web part description that is displayed in the toolbox tooltips.</span></span>|`"description": { "default": "Shows weather in the given location", "nl-nl": "Toont weerbericht voor de opgegeven locatie" } `|
|<span data-ttu-id="2d424-133">officeFabricIconFontName</span><span class="sxs-lookup"><span data-stu-id="2d424-133">officeFabricIconFontName</span></span>|<span data-ttu-id="2d424-134">string</span><span class="sxs-lookup"><span data-stu-id="2d424-134">string</span></span>          |<span data-ttu-id="2d424-135">Нет</span><span class="sxs-lookup"><span data-stu-id="2d424-135">no</span></span>      |<span data-ttu-id="2d424-136">Значок веб-части, который отображается на панели элементов.</span><span class="sxs-lookup"><span data-stu-id="2d424-136">The web part title that is displayed in the toolbox.</span></span> <span data-ttu-id="2d424-137">Значение этого параметра должно быть одним из [имен значков Office UI Fabric](https://dev.office.com/fabric#/styles/icons).</span><span class="sxs-lookup"><span data-stu-id="2d424-137">Its value must be one of the [Office UI Fabric icon names](https://dev.office.com/fabric#/styles/icons).</span></span> <span data-ttu-id="2d424-138">Если у этого свойства есть значение, свойство **iconImageUrl** игнорируется.</span><span class="sxs-lookup"><span data-stu-id="2d424-138">If this property has a value, the **iconImageUrl** property is ignored.</span></span>|`"officeFabricIconFontName": "Sunny"`|
|<span data-ttu-id="2d424-139">iconImageUrl</span><span class="sxs-lookup"><span data-stu-id="2d424-139">iconImageUrl</span></span>            |<span data-ttu-id="2d424-140">string</span><span class="sxs-lookup"><span data-stu-id="2d424-140">string</span></span>          |<span data-ttu-id="2d424-141">Нет</span><span class="sxs-lookup"><span data-stu-id="2d424-141">no</span></span>      |<span data-ttu-id="2d424-142">Значок веб-части, который отображается на панели элементов и представлен URL-адресом изображения.</span><span class="sxs-lookup"><span data-stu-id="2d424-142">The icon for the web part that is displayed in the toolbox and is represented by an image URL.</span></span> <span data-ttu-id="2d424-143">Размер изображения, находящегося по этому URL-адресу, должен составлять 40 x 28 пикселей.</span><span class="sxs-lookup"><span data-stu-id="2d424-143">The image at the URL must be exactly 40x28 px.</span></span> <span data-ttu-id="2d424-144">Если у свойства **officeFabricIconName** нет значения, необходимо его задать.</span><span class="sxs-lookup"><span data-stu-id="2d424-144">If the **officeFabricIconName** property does not have a value, this property must have a value.</span></span>|`"iconImageUrl": "https://cdn.contoso.com/weather.png"`|
|<span data-ttu-id="2d424-145">groupId</span><span class="sxs-lookup"><span data-stu-id="2d424-145">groupId</span></span>                 |<span data-ttu-id="2d424-146">string</span><span class="sxs-lookup"><span data-stu-id="2d424-146">string</span></span>          |<span data-ttu-id="2d424-147">да</span><span class="sxs-lookup"><span data-stu-id="2d424-147">yes</span></span>     |<span data-ttu-id="2d424-148">Идентификатор группы, определяющий, какая современная группа содержит веб-часть на современной странице сайта.</span><span class="sxs-lookup"><span data-stu-id="2d424-148">The group id to determine which modern group contains the web part in modern site page.</span></span> <span data-ttu-id="2d424-149">Платформа SharePoint Framework резервирует идентификаторы для [стандартных групп](#predefined-modern-groups).</span><span class="sxs-lookup"><span data-stu-id="2d424-149">The SharePoint Framework reserves group ids for [predefined groups](#predefined-modern-groups).</span></span> <span data-ttu-id="2d424-150">Разработчик может выбрать одну из них.</span><span class="sxs-lookup"><span data-stu-id="2d424-150">The developer can pick one from those groups.</span></span> <span data-ttu-id="2d424-151">Если разработчик указывает идентификатор, не относящийся к стандартной группе, веб-часть возвращается в группу **Другие**.</span><span class="sxs-lookup"><span data-stu-id="2d424-151">If the developer fills an id not in the predefined groups, it falls back to **Other** group.</span></span>|`"groupId": "1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489"`|
|<span data-ttu-id="2d424-152">group</span><span class="sxs-lookup"><span data-stu-id="2d424-152">group</span></span>                   |<span data-ttu-id="2d424-153">ILocalizedString</span><span class="sxs-lookup"><span data-stu-id="2d424-153">ILocalizedString</span></span>|<span data-ttu-id="2d424-154">нет</span><span class="sxs-lookup"><span data-stu-id="2d424-154">no</span></span>      |<span data-ttu-id="2d424-155">Имя группы, в которой будет отображаться веб-часть на классической странице.</span><span class="sxs-lookup"><span data-stu-id="2d424-155">The group name in web part picker to contain the web part in the classic page.</span></span> <span data-ttu-id="2d424-156">Если значение не указано, веб-часть отображается в группе **Разное**.</span><span class="sxs-lookup"><span data-stu-id="2d424-156">If no value is provided, then the web part will be displayed in the **Miscellaneous** group.</span></span>|`"group": { "default": "Content", "nl-nl": "Inhoud" }`|
|<span data-ttu-id="2d424-157">dataVersion</span><span class="sxs-lookup"><span data-stu-id="2d424-157">dataVersion</span></span>             |<span data-ttu-id="2d424-158">string</span><span class="sxs-lookup"><span data-stu-id="2d424-158">string</span></span>          |<span data-ttu-id="2d424-159">нет</span><span class="sxs-lookup"><span data-stu-id="2d424-159">no</span></span>      |<span data-ttu-id="2d424-160">Это поле используется для указания версии предварительно настроенных данных, предоставленных веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-160">Use this field to specify the data version of the pre-configured data provided to the web part.</span></span> <span data-ttu-id="2d424-161">Обратите внимание, что версия данных и поле версии в манифесте — это не одно и то же.</span><span class="sxs-lookup"><span data-stu-id="2d424-161">Note that data version is different from the version field in the manifest.</span></span> <span data-ttu-id="2d424-162">Версия манифеста используется для управления версиями кода веб-части, а версия данных — для управления версиями сериализованных данных веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-162">The manifest version is used to control the versioning of the web part code, while data version is used to control the versioning of the serialized data of the web part.</span></span> <span data-ttu-id="2d424-163">Дополнительные сведения см. в описании поля dataVersion для веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-163">Refer to the dataVersion field of your web part for more information.</span></span> <span data-ttu-id="2d424-164">Поддерживаемый формат значений: версия MAJOR.MINOR</span><span class="sxs-lookup"><span data-stu-id="2d424-164">Supported values format: MAJOR.MINOR version</span></span>|`"dataVersion": "1.0"`|
|<span data-ttu-id="2d424-165">properties</span><span class="sxs-lookup"><span data-stu-id="2d424-165">properties</span></span>              |<span data-ttu-id="2d424-166">TProperties</span><span class="sxs-lookup"><span data-stu-id="2d424-166">TProperties</span></span>     |<span data-ttu-id="2d424-167">да</span><span class="sxs-lookup"><span data-stu-id="2d424-167">yes</span></span>     |<span data-ttu-id="2d424-168">Объект пары "ключ-значение" со значениями по умолчанию для свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-168">A Key-value pair object with default values for web part properties.</span></span>|`"properties": { "location": "Redmond", "numberOfDays": 3, "showIcon": true }`|

<br/>

<span data-ttu-id="2d424-169">Некоторые свойства веб-части принимают значения типа **ILocalizedString**.</span><span class="sxs-lookup"><span data-stu-id="2d424-169">Some web part properties have a value of type **ILocalizedString**.</span></span> <span data-ttu-id="2d424-170">Этот тип представляет собой объект пары "ключ-значение", с помощью которого разработчики могут указывать строки для различных языковых стандартов.</span><span class="sxs-lookup"><span data-stu-id="2d424-170">This type is a key-value pair object that allows developers to specify strings for the different locales.</span></span> <span data-ttu-id="2d424-171">Значение типа **ILocalizedString** должно содержать хотя бы значение **default**.</span><span class="sxs-lookup"><span data-stu-id="2d424-171">At a minimum, a value of type **ILocalizedString** must contain the **default** value.</span></span> 

<span data-ttu-id="2d424-172">При необходимости разработчик может указать перевод этого значения для разных языковых стандартов, поддерживаемых веб-частью.</span><span class="sxs-lookup"><span data-stu-id="2d424-172">Optionally, developers can provide the translations of that value to the different locales that their web part supports.</span></span> <span data-ttu-id="2d424-173">Если веб-часть размещена на странице для языкового стандарта, не указанного в локализованной строке, используется значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d424-173">If the web part is placed on a page in a locale that isn't listed in the localized string, the default value is used instead.</span></span>

<span data-ttu-id="2d424-174">Допустимые значения **ILocalizedString**:</span><span class="sxs-lookup"><span data-stu-id="2d424-174">Valid **ILocalizedString** values:</span></span>

```json
"title": {
  "default": "Weather",
  "nl-nl": "Weerbericht"
}
```

```json
"title": {
  "default": "Weather"
}
```

<br/>

<span data-ttu-id="2d424-175">Значение **ILocalizedString**, не являющееся допустимым, так как отсутствует ключ **default**:</span><span class="sxs-lookup"><span data-stu-id="2d424-175">A **ILocalizedString** value that is not valid because the **default** key is missing:</span></span>

```json
"title": {
  "en-us": "Weather"
}
```

### <a name="predefined-modern-groups"></a><span data-ttu-id="2d424-176">Предварительно определенные современные группы</span><span class="sxs-lookup"><span data-stu-id="2d424-176">Predefined modern groups</span></span>

<span data-ttu-id="2d424-177">В приведенной ниже таблице представлены 7 стандартных групп.</span><span class="sxs-lookup"><span data-stu-id="2d424-177">There are 7 out of the box groups as shown in the following table.</span></span> <span data-ttu-id="2d424-178">Используйте идентификатор группы в свойстве `groupId`.</span><span class="sxs-lookup"><span data-stu-id="2d424-178">Use the group ID in the `groupId` property.</span></span>

| <span data-ttu-id="2d424-179">Имя группы</span><span class="sxs-lookup"><span data-stu-id="2d424-179">Group Name</span></span>                      | <span data-ttu-id="2d424-180">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="2d424-180">ID</span></span>                                     | <span data-ttu-id="2d424-181">Содержимое группы</span><span class="sxs-lookup"><span data-stu-id="2d424-181">Group includes...</span></span> |   
|---------------------------------|----------------------------------------|---------------|
| <span data-ttu-id="2d424-182">Текст, мультимедиа и контент</span><span class="sxs-lookup"><span data-stu-id="2d424-182">Text, media, and content</span></span>        | `cf066440-0614-43d6-98ae-0b31cf14c7c3` | <span data-ttu-id="2d424-183">Веб-части, отображающие текст, мультимедиа, документы, информацию из Интернета и другой контент.</span><span class="sxs-lookup"><span data-stu-id="2d424-183">This group includes web parts that display text, multi-media, documents, information from the web, and other rich content.</span></span> |
| <span data-ttu-id="2d424-184">Обнаружение</span><span class="sxs-lookup"><span data-stu-id="2d424-184">Discover</span></span>                        | `1edbd9a8-0bfb-4aa2-9afd-14b8c45dd489` | <span data-ttu-id="2d424-185">Веб-части, которые упорядочивают, группируют и фильтруют контент, помогая пользователям находить нужные сведения.</span><span class="sxs-lookup"><span data-stu-id="2d424-185">This group includes web parts that organize, group, and filter content to help users discover information.</span></span>                 |
| <span data-ttu-id="2d424-186">Связь и совместная работа</span><span class="sxs-lookup"><span data-stu-id="2d424-186">Communication and collaboration</span></span> | `75e22ed5-fa14-4829-850a-c890608aca2d` | <span data-ttu-id="2d424-187">Веб-части, которые помогают делиться информацией, а также упрощают работу в команде и социальное взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="2d424-187">This group includes web parts that facilitate information sharing, team work, and social interactions.</span></span>                     |
| <span data-ttu-id="2d424-188">Планирование и процессы</span><span class="sxs-lookup"><span data-stu-id="2d424-188">Planning and process</span></span>            | `1bc7927e-4a5e-4520-b540-71305c79c20a` | <span data-ttu-id="2d424-189">Веб-части, которые повышают производительность команды при помощи инструментов планирования и управления процессами.</span><span class="sxs-lookup"><span data-stu-id="2d424-189">This group includes web parts that empower team productivity with the use of planning and process tools.</span></span>                   |
| <span data-ttu-id="2d424-190">Бизнес и аналитика</span><span class="sxs-lookup"><span data-stu-id="2d424-190">Business and intelligence</span></span>       | `4aca9e90-eff5-4fa1-bac7-728f5f157b66` | <span data-ttu-id="2d424-191">Веб-части для отслеживания и анализа данных, а также для интеграции бизнес-процессов со страницами.</span><span class="sxs-lookup"><span data-stu-id="2d424-191">This group includes web parts for tracking and analyzing data, and for integrating business flow with pages.</span></span>               |
| <span data-ttu-id="2d424-192">Инструменты сайта</span><span class="sxs-lookup"><span data-stu-id="2d424-192">Site tools</span></span>                      | `070951d7-94da-4db8-b06e-9d581f1f55b1` | <span data-ttu-id="2d424-193">Веб-части для управления сайтом и получения сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="2d424-193">This group includes web parts for site information and management.</span></span>                                                         |
| <span data-ttu-id="2d424-194">Другие</span><span class="sxs-lookup"><span data-stu-id="2d424-194">Other</span></span>                           | `5c03119e-3074-46fd-976b-c60198311f70` | <span data-ttu-id="2d424-195">Веб-части, не входящие в другие группы.</span><span class="sxs-lookup"><span data-stu-id="2d424-195">This group includes web parts not in other groups.</span></span>                                                                         |

<span data-ttu-id="2d424-196">Если разработчик использует идентификатор, не указанный в приведенном выше списке, веб-часть возвращается в группу **Другие**.</span><span class="sxs-lookup"><span data-stu-id="2d424-196">If the developer fills an id not in the above list, the web part will fall back to **Other** group.</span></span>

<span data-ttu-id="2d424-p113">Чтобы увидеть, как можно использовать предварительно настроенные записи при создании веб-частей, вы можете создать пример веб-части с коллекцией. С помощью нескольких свойств пользователи могут настраивать эту веб-часть так, чтобы в ней определенным образом отображались элементы из выбранного списка. Для краткости мы опустим фактическую реализацию логики веб-части и сосредоточимся на том, как предоставлять предварительно настроенные версии веб-части коллекции с помощью свойства **preconfiguredEntries**.</span><span class="sxs-lookup"><span data-stu-id="2d424-p113">To see how you can use preconfigured entries when building web parts, you will build a sample gallery web part. Using several properties, users can configure this web part to show items from a selected list in a specific way. For brevity, you will omit the actual implementation of the web part logic and will focus on using the **preconfiguredEntries** property to provide preconfigured versions of the gallery web part.</span></span>

![Область свойств веб-части с различными свойствами, которые необходимо настроить пользователям](../../../images/preconfiguredentries-needs-configuration.png)

## <a name="create-a-new-web-part-project"></a><span data-ttu-id="2d424-201">Создание проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="2d424-201">Create a new web part project</span></span>

1. <span data-ttu-id="2d424-202">Для начала создайте папку проекта.</span><span class="sxs-lookup"><span data-stu-id="2d424-202">Start by creating a new folder for your project.</span></span>

  ```sh
  md react-preconfiguredentries
  ```

2. <span data-ttu-id="2d424-203">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="2d424-203">Go to the project folder.</span></span>

  ```sh
  cd react-preconfiguredentries
  ```

3. <span data-ttu-id="2d424-204">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="2d424-204">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="2d424-205">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2d424-205">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="2d424-206">**react-preconfiguredentries** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="2d424-206">**react-preconfiguredentries** as your solution name</span></span>
  - <span data-ttu-id="2d424-207">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="2d424-207">**Use the current folder** for the location to place the files</span></span>
  - <span data-ttu-id="2d424-208">**Gallery** (Коллекция) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="2d424-208">**Gallery** as your web part name</span></span>
  - <span data-ttu-id="2d424-209">**Shows items from the selected list** (Показывает элементы из выбранного списка) в качестве описания веб-части;</span><span class="sxs-lookup"><span data-stu-id="2d424-209">**Shows items from the selected list** as your web part description</span></span>
  - <span data-ttu-id="2d424-210">**React** как отправную точку создания веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-210">**React** as the starting point to build the web part</span></span>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/preconfiguredentries-yeoman.png)

5. <span data-ttu-id="2d424-212">По завершении формирования шаблона заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d424-212">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="2d424-213">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="2d424-213">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="2d424-214">В инструкциях и на снимках экрана из этой статьи используется Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="2d424-214">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor you prefer.</span></span>

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/preconfiguredentries-visual-studio-code.png)

## <a name="add-web-part-properties"></a><span data-ttu-id="2d424-216">Добавление свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="2d424-216">Add web part properties</span></span>

<span data-ttu-id="2d424-217">Добавьте свойства в манифесте веб-части, чтобы пользователи могли настраивать веб-часть коллекции.</span><span class="sxs-lookup"><span data-stu-id="2d424-217">In the web part manifest, add web part properties so that users can configure the gallery web part. In the code editor, open the ./src/webparts/gallery/GalleryWebPart.manifest.json file. Replace the properties section with the following JSON:</span></span> 

1. <span data-ttu-id="2d424-218">Откройте в редакторе кода файл **./src/webparts/gallery/GalleryWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="2d424-218">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the preconfiguredEntries property to:</span></span> 

2. <span data-ttu-id="2d424-219">Замените раздел **properties** следующим кодом JSON:</span><span class="sxs-lookup"><span data-stu-id="2d424-219">Replace the **properties** section with the following JSON:</span></span>

  ```json
  {
    //...
    "preconfiguredEntries": [{
      //...
      "properties": {
        "listName": "",
        "order": "",
        "numberOfItems": 10,
        "style": ""
      }
    }]
  }
  ```

  <span data-ttu-id="2d424-220">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="2d424-220">Note the following about this code:</span></span>
  - <span data-ttu-id="2d424-221">Свойство **listName** задает имя списка, элементы которого будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="2d424-221">The **listName** property specifies the name of the list from which list items should be displayed.</span></span> 
  - <span data-ttu-id="2d424-222">Свойство **order** задает порядок отображения элементов: по возрастанию или убыванию времени добавления.</span><span class="sxs-lookup"><span data-stu-id="2d424-222">The **order** property specifies the order in which items should be shown, that is chronological, or reverse chronological order.</span></span> 
  - <span data-ttu-id="2d424-223">Свойство **numberOfItems** задает количество отображаемых элементов.</span><span class="sxs-lookup"><span data-stu-id="2d424-223">The **numberOfItems** property specifies how many items should be displayed.</span></span> 
  - <span data-ttu-id="2d424-224">Свойство **style** задает способ отображения элементов, например в виде эскизов (удобно для показа изображений) или списка (лучше подходит для документов).</span><span class="sxs-lookup"><span data-stu-id="2d424-224">The **style** property specifies how the items should be displayed, such as thumbnails, which is useful for showing images, or as a list, which is more suitable for documents.</span></span>

  <span data-ttu-id="2d424-225">Указанные в манифесте свойства веб-части также необходимо добавить в интерфейс свойств.</span><span class="sxs-lookup"><span data-stu-id="2d424-225">Web part properties specified in the manifest must also be added to the web part properties interface. In the code editor, open the ./src/webparts/gallery/IGalleryWebPartProps.ts file. Change its code to:</span></span> 
  
3. <span data-ttu-id="2d424-226">Откройте в редакторе кода файл **./src/webparts/gallery/IGalleryWebPartProps.ts**.</span><span class="sxs-lookup"><span data-stu-id="2d424-226">In the code editor, open the **./src/webparts/gallery/loc/mystrings.d.ts** file. Change its code to:</span></span> <span data-ttu-id="2d424-227">Измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="2d424-227">Change its contents to:</span></span>

  ```ts
  export interface IGalleryWebPartProps {
    listName: string;
    order: string;
    numberOfItems: number;
    style: string;
  }
  ```

  <span data-ttu-id="2d424-228">Создавая клиентские веб-части SharePoint Framework с помощью React, после того как вы измените интерфейс свойств веб-части, необходимо обновить метод **render**, который использует этот интерфейс для создания главного компонента React.</span><span class="sxs-lookup"><span data-stu-id="2d424-228">When building SharePoint Framework client-side web parts using React, after changing the web part properties interface, you need to update the web part's **render** method that uses that interface to create an instance of the main React component. In the code editor, open the ./src/webparts/gallery/GalleryWebPart.ts file. Change the web part render method to:</span></span> 
  
4. <span data-ttu-id="2d424-229">Откройте в редакторе кода файл **./src/webparts/gallery/GalleryWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="2d424-229">In the code editor open the **./src/webparts/toDo/ToDoWebPart.ts** file.</span></span> <span data-ttu-id="2d424-230">Замените содержимое метода **render** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2d424-230">Change the **render** method to:</span></span>

  ```ts
  export default class GalleryWebPart extends BaseClientSideWebPart<IGalleryWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IGalleryProps> = React.createElement(Gallery, {
        listName: this.properties.listName,
        order: this.properties.order,
        numberOfItems: this.properties.numberOfItems,
        style: this.properties.style
      });

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

5. <span data-ttu-id="2d424-231">Измените главный компонент React так, чтобы отображались значения свойств.</span><span class="sxs-lookup"><span data-stu-id="2d424-231">Update the main React component to display the values of the properties.</span></span> <span data-ttu-id="2d424-232">Если веб-часть не настроена, должен отображаться стандартный заполнитель веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-232">If the web part hasn't been configured, show the standard web part placeholder.</span></span> <span data-ttu-id="2d424-233">Откройте в редакторе кода файл **./src/webparts/gallery/components/Gallery.tsx** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="2d424-233">In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file and change its code to:</span></span>

  ```ts
  import * as React from 'react';
  import styles from './Gallery.module.scss';
  import { IGalleryProps } from './IGalleryProps';

  export default class Gallery extends React.Component<IGalleryProps, void> {
    public render(): JSX.Element {
      if (this.needsConfiguration()) {
        return <div className="ms-Grid" style={{ color: "#666", backgroundColor: "#f4f4f4", padding: "80px 0", alignItems: "center", boxAlign: "center" }}>
          <div className="ms-Grid-row" style={{ color: "#333" }}>
            <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
            <div className="ms-Grid-col ms-u-sm12 ms-u-md6" style={{ height: "100%", whiteSpace: "nowrap", textAlign: "center" }}>
              <i className="ms-fontSize-su ms-Icon ms-Icon--ThumbnailView" style={{ display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}></i><span className="ms-fontWeight-light ms-fontSize-xxl" style={{ paddingLeft: "20px", display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}>Gallery</span>
            </div>
            <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
          </div>
          <div className="ms-Grid-row" style={{ width: "65%", verticalAlign: "middle", margin: "0 auto", textAlign: "center" }}>
            <span style={{ color: "#666", fontSize: "17px", display: "inline-block", margin: "24px 0", fontWeight: 100 }}>Show items from the selected list</span>
          </div>
          <div className="ms-Grid-row"></div>
        </div>;
      }
      else {
        return (
          <div className={styles.gallery}>
            <div className={styles.container}>
              <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
                <div className='ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1'>
                  <span className="ms-font-xl ms-fontColor-white">
                    Welcome to SharePoint!
                  </span>
                  <p className='ms-font-l ms-fontColor-white'>
                    Customize SharePoint experiences using Web Parts.
                  </p>
                  <p className='ms-font-l ms-fontColor-white'>
                    List: {this.props.listName}<br />
                    Order: {this.props.order}<br />
                    Number of items: {this.props.numberOfItems}<br />
                    Style: {this.props.style}
                  </p>
                  <a href="https://aka.ms/spfx" className={styles.button}>
                    <span className={styles.label}>Learn more</span>
                  </a>
                </div>
              </div>
            </div>
          </div>
        );
      }
    }

    private needsConfiguration(): boolean {
      return Gallery.isEmpty(this.props.listName) ||
        Gallery.isEmpty(this.props.order) ||
        Gallery.isEmpty(this.props.style);
    }

    private static isEmpty(value: string): boolean {
      return value === undefined ||
        value === null ||
        value.length === 0;
    }
  }
  ```

6. <span data-ttu-id="2d424-234">Обновите интерфейс основного компонента React в соответствии со свойством веб-части Interface, так как мы обходим все свойства веб-части для этого компонента.</span><span class="sxs-lookup"><span data-stu-id="2d424-234">Update the main React component Interface to match on the web part property Interface, since we are bypassing all the web part properties to this component. In the code editor, open the ./src/webparts/gallery/components/IGalleryProps.ts file and change its code to:</span></span> <span data-ttu-id="2d424-235">Откройте в редакторе кода файл **./src/webparts/gallery/components/IGalleryProps.ts** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="2d424-235">In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file and change its code to:</span></span>

  ```ts
  import { IGalleryWebPartProps } from '../IGalleryWebPartProps';

  export interface IGalleryProps extends IGalleryWebPartProps {
  }
  ```

## <a name="render-web-part-properties-in-the-property-pane"></a><span data-ttu-id="2d424-236">Отображение свойств веб-части в области свойств</span><span class="sxs-lookup"><span data-stu-id="2d424-236">Render web part properties in the property pane</span></span>

<span data-ttu-id="2d424-237">Чтобы пользователи могли настраивать веб-часть с помощью новых свойств, эти свойства должны отображаться в области свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-237">For users to be able to use the newly defined properties to configure the web part, the properties must be displayed in the web part property pane. In the code editor, open the ./src/webparts/gallery/GalleryWebPart.ts file. In the top section of the file change the @microsoft/sp-webpart-base import statement to:</span></span> 

1. <span data-ttu-id="2d424-238">Откройте в редакторе кода файл **./src/webparts/gallery/GalleryWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="2d424-238">In the code editor open the **./src/webparts/toDo/ToDoWebPart.ts** file.</span></span> <span data-ttu-id="2d424-239">В верхнем разделе файла замените оператор импорта **@microsoft/sp-webpart-base** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2d424-239">In the top section of the file, change the **@microsoft/sp-webpart-base** import statement to:</span></span>

  ```ts
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneDropdown,
    PropertyPaneSlider,
    PropertyPaneChoiceGroup
  } from '@microsoft/sp-webpart-base';
  ```

2. <span data-ttu-id="2d424-240">Замените содержимое метода **propertyPaneSettings** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2d424-240">Change the **propertyPaneSettings** to:</span></span>

  ```ts
  export default class GalleryWebPart extends BaseClientSideWebPart<IGalleryWebPartProps> {
    // ...
    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.BasicGroupName,
                groupFields: [
                  PropertyPaneDropdown('listName', {
                    label: strings.ListNameFieldLabel,
                    options: [{
                      key: 'Documents',
                      text: 'Documents'
                    },
                    {
                      key: 'Images',
                      text: 'Images'
                    }]
                  }),
                  PropertyPaneChoiceGroup('order', {
                    label: strings.OrderFieldLabel,
                    options: [{
                      key: 'chronological',
                      text: strings.OrderFieldChronologicalOptionLabel
                    },
                    {
                      key: 'reversed',
                      text: strings.OrderFieldReversedOptionLabel
                    }]
                  }),
                  PropertyPaneSlider('numberOfItems', {
                    label: strings.NumberOfItemsFieldLabel,
                    min: 1,
                    max: 10,
                    step: 1
                  }),
                  PropertyPaneChoiceGroup('style', {
                    label: strings.StyleFieldLabel,
                    options: [{
                      key: 'thumbnails',
                      text: strings.StyleFieldThumbnailsOptionLabel
                    },
                    {
                      key: 'list',
                      text: strings.StyleFieldListOptionLabel
                    }]
                  })
                ]
              }
            ]
          }
        ]
      };
    }
  }
  ```

<br/>

<span data-ttu-id="2d424-241">В реальной ситуации вы получали бы список списков с текущего сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2d424-241">In a real-life scenario, you would retrieve the list of lists from the current SharePoint site. For brevity, in this example you use a fixed list instead.</span></span> <span data-ttu-id="2d424-242">Для краткости в этом примере используется фиксированный список.</span><span class="sxs-lookup"><span data-stu-id="2d424-242">For brevity, in this example, you use a fixed list instead.</span></span>

## <a name="add-localization-labels"></a><span data-ttu-id="2d424-243">Добавление меток локализации</span><span class="sxs-lookup"><span data-stu-id="2d424-243">Add localization labels</span></span>

1. <span data-ttu-id="2d424-p121">Откройте в редакторе кода файл **./src/webparts/gallery/loc/mystrings.d.ts**. Измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="2d424-p121">In the code editor, open the **./src/webparts/gallery/loc/mystrings.d.ts** file. Change its code to:</span></span>

  ```ts
  declare interface IGalleryStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListNameFieldLabel: string;
    OrderFieldLabel: string;
    OrderFieldChronologicalOptionLabel: string;
    OrderFieldReversedOptionLabel: string;
    NumberOfItemsFieldLabel: string;
    StyleFieldLabel: string;
    StyleFieldThumbnailsOptionLabel: string;
    StyleFieldListOptionLabel: string;
  }

  declare module 'galleryStrings' {
    const strings: IGalleryStrings;
    export = strings;
  }
  ```

2. <span data-ttu-id="2d424-246">Добавьте отсутствующие строки ресурсов, открыв файл **./src/webparts/gallery/loc/en-us.js** и изменив его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="2d424-246">Add the missing resource strings by opening in the code editor the **./src/webparts/gallery/loc/en-us.js** file and changing its code to:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListNameFieldLabel": "List",
      "OrderFieldLabel": "Items order",
      "OrderFieldChronologicalOptionLabel": "chronological",
      "OrderFieldReversedOptionLabel": "reversed chronological",
      "NumberOfItemsFieldLabel": "Number of items to show",
      "StyleFieldLabel": "Items display style",
      "StyleFieldThumbnailsOptionLabel": "thumbnails",
      "StyleFieldListOptionLabel": "list"
    }
  });
  ```

3. <span data-ttu-id="2d424-247">Подтвердите сборку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d424-247">Confirm that the project is building by running the following command:</span></span>

  ```sh
  gulp serve
  ```

4. <span data-ttu-id="2d424-248">В веб-браузере добавьте веб-часть на холст и откройте ее область свойств.</span><span class="sxs-lookup"><span data-stu-id="2d424-248">In the web browser add the web part to the canvas and open its property pane. You should see all properties available for users to configure.</span></span> <span data-ttu-id="2d424-249">Должны появиться все свойства, которые могут настраивать пользователи.</span><span class="sxs-lookup"><span data-stu-id="2d424-249">You should see all the properties available for users to configure.</span></span>

  ![Область свойств веб-части с различными свойствами, которые необходимо настроить пользователям](../../../images/preconfiguredentries-needs-configuration.png)

<span data-ttu-id="2d424-251">Для веб-части не заданы значения по умолчанию, поэтому каждый раз, когда пользователь добавляет веб-часть на страницу, ее необходимо настраивать.</span><span class="sxs-lookup"><span data-stu-id="2d424-251">Because you didn't specify any default values for the web part, every time users add the web part to the page they have to configure it first. You can simplify this experience by providing default values for the most common scenarios.</span></span> <span data-ttu-id="2d424-252">Вы можете упростить работу, указав значения по умолчанию для наиболее распространенных ситуаций.</span><span class="sxs-lookup"><span data-stu-id="2d424-252">You can simplify this experience by providing default values for the most common scenarios.</span></span>

## <a name="specify-default-values-for-the-web-part"></a><span data-ttu-id="2d424-253">Указание значений по умолчанию для веб-части</span><span class="sxs-lookup"><span data-stu-id="2d424-253">Specify default values for the web part</span></span>

<span data-ttu-id="2d424-254">Допустим, пользователи часто используют веб-часть коллекции, чтобы показать пять последних добавленных изображений.</span><span class="sxs-lookup"><span data-stu-id="2d424-254">Imagine that users often use the gallery web part to show the five most recently added images. Rather than requiring users to configure the web part each time manually, you could provide them with a preconfigured version using correct settings.</span></span> <span data-ttu-id="2d424-255">Чтобы пользователям не приходилось каждый раз настраивать веб-часть вручную, вы можете предоставить им предварительно настроенную версию с подходящими параметрами.</span><span class="sxs-lookup"><span data-stu-id="2d424-255">Imagine that users often use the gallery web part to show the five most recently added images. Rather than requiring users to configure the web part each time manually, you could provide them with a preconfigured version using correct settings.</span></span>

1. <span data-ttu-id="2d424-p125">Откройте в редакторе кода файл **./src/webparts/gallery/GalleryWebPart.manifest.json**. Измените имеющуюся запись в свойстве **preconfiguredEntries** на следующую:</span><span class="sxs-lookup"><span data-stu-id="2d424-p125">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the existing entry in the **preconfiguredEntries** property to:</span></span>

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent images" },
      "description": { "default": "Shows 5 most recent images" },
      "officeFabricIconFontName": "Picture",
      "properties": {
        "listName": "Images",
        "order": "reversed",
        "numberOfItems": 5,
        "style": "thumbnails"
      }
    }]
  }
  ```

2. <span data-ttu-id="2d424-258">Начните отладку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d424-258">Start debugging the project by running the following command:</span></span>

  ```sh
  gulp serve
  ```

  > [!NOTE] 
  > <span data-ttu-id="2d424-259">Если отладка проекта уже выполнялась, остановите ее и начните заново.</span><span class="sxs-lookup"><span data-stu-id="2d424-259">If you were debugging the project previously, stop debugging and start it again.</span></span> <span data-ttu-id="2d424-260">Изменения, внесенные в манифест веб-части, не отображаются в Workbench во время отладки. Чтобы увидеть их, необходимо повторно собрать проект.</span><span class="sxs-lookup"><span data-stu-id="2d424-260">Changes made to the web part manifest are not automatically reflected in the workbench while debugging, and you have to rebuild the project in order to see them.</span></span>

3. <span data-ttu-id="2d424-261">Открыв панель элементов веб-частей, чтобы добавить веб-часть на холст, вы увидите, что ее название и значок изменились в соответствии с предварительно настроенными параметрами.</span><span class="sxs-lookup"><span data-stu-id="2d424-261">When you open the web part toolbox to add the web part to the canvas, you will see that its name and icon changed to reflect the preconfigured settings.</span></span>

  ![Панель элементов с предварительно настроенной версией веб-части](../../../images/preconfiguredentries-recent-images-toolbox.png)

4. <span data-ttu-id="2d424-263">Веб-часть начнет работать сразу после добавления на страницу, используя предварительно настроенные параметры.</span><span class="sxs-lookup"><span data-stu-id="2d424-263">After adding the web part to the page, it works immediately using the preconfigured settings.</span></span>

  ![Предварительно настроенная веб-часть, работающая сразу после добавления на страницу](../../../images/preconfiguredentries-recent-images-canvas.png)

## <a name="specify-multiple-preconfigured-web-part-entries"></a><span data-ttu-id="2d424-265">Указание нескольких предварительно настроенных записей веб-части</span><span class="sxs-lookup"><span data-stu-id="2d424-265">Specify multiple preconfigured web part entries</span></span>

<span data-ttu-id="2d424-p127">Представьте, что еще одна группа пользователей часто обращается к веб-части коллекции, чтобы просматривать последние добавленные на сайт документы. Чтобы помочь этим пользователям работать с веб-частью, вы можете добавить еще один набор предварительно настроенных записей, соответствующий их потребностям.</span><span class="sxs-lookup"><span data-stu-id="2d424-p127">Imagine that another group of users often uses your gallery web part to show documents recently added to their site. To help them use your web part, you can add another set of presets that addresses their configuration needs.</span></span>

1. <span data-ttu-id="2d424-p128">Откройте в редакторе кода файл **./src/webparts/gallery/GalleryWebPart.manifest.json**. Замените содержимое свойства **preconfiguredEntries** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2d424-p128">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the **preconfiguredEntries** property to:</span></span>

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent images" },
      "description": { "default": "Shows 5 most recent images" },
      "officeFabricIconFontName": "Picture",
      "properties": {
        "listName": "Images",
        "order": "reversed",
        "numberOfItems": 5,
        "style": "thumbnails"
      }
    },
    {
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent documents" },
      "description": { "default": "Shows 10 most recent documents" },
      "officeFabricIconFontName": "Documentation",
      "properties": {
        "listName": "Documents",
        "order": "reversed",
        "numberOfItems": 10,
        "style": "list"
      }
    }]
  }
  ```

2. <span data-ttu-id="2d424-270">Обратите внимание, что благодаря другим значениям свойств добавление новой предварительно настроенной записи не влияет на предыдущую.</span><span class="sxs-lookup"><span data-stu-id="2d424-270">Notice how you keep the previous preconfigured entry intact and add another one beside it using different values for properties.</span></span>

3. <span data-ttu-id="2d424-271">Чтобы увидеть результат, запустите отладку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d424-271">To see the result start debugging the project by running the following command:</span></span>

  ```sh
  gulp serve
  ```

4. <span data-ttu-id="2d424-272">Открыв панель элементов веб-частей для добавления веб-части на холст, вы увидите, что можно выбрать одну из двух веб-частей.</span><span class="sxs-lookup"><span data-stu-id="2d424-272">When you open the web part toolbox to add the web part to the canvas, you will see that there are two web parts for you to choose from.</span></span>

  ![Панель элементов с предварительно настроенной версией веб-части](../../../images/preconfiguredentries-multiple-web-parts-toolbox.png)

5. <span data-ttu-id="2d424-274">Веб-часть **Последние документы** начнет работать сразу после добавления на страницу, используя предварительно настроенные параметры.</span><span class="sxs-lookup"><span data-stu-id="2d424-274">After adding the **Recent documents** web part to the page, it works immediately using its specific preconfigured settings.</span></span>

  ![Предварительно настроенная веб-часть "Последние документы", работающая сразу после добавления на страницу](../../../images/preconfiguredentries-recent-documents-canvas.png)

## <a name="specify-an-unconfigured-instance-of-the-web-part"></a><span data-ttu-id="2d424-276">Добавление ненастроенного экземпляра веб-части</span><span class="sxs-lookup"><span data-stu-id="2d424-276">Specify an unconfigured instance of the web part</span></span>

<span data-ttu-id="2d424-277">При создании веб-частей часто требуется обеспечивать поддержку определенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="2d424-277">When building web parts there are often specific scenarios that the web part should support. Providing preconfigured entries for those scenarios makes it easier for users to use the web part.</span></span> <span data-ttu-id="2d424-278">Благодаря предварительно настроенным записям для этих сценариев пользователям будет проще использовать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="2d424-278">When building web parts there are often specific scenarios that the web part should support. Providing preconfigured entries for those scenarios makes it easier for users to use the web part.</span></span>

<span data-ttu-id="2d424-279">В зависимости от того, как вы создаете веб-часть, можно также обеспечить поддержку других непредвиденных случаев.</span><span class="sxs-lookup"><span data-stu-id="2d424-279">Depending on how you build your web part, it could be possible that the web part can support other unforeseen scenarios as well.</span></span> <span data-ttu-id="2d424-280">Если предоставить предварительно настроенные записи только для специфических случаев, пользователи могут не понять, что веб-часть можно использовать в других ситуациях.</span><span class="sxs-lookup"><span data-stu-id="2d424-280">If you only provide specific preconfigured entries, users might not realize they can use your web part for a different scenario.</span></span> <span data-ttu-id="2d424-281">Рекомендуем предоставить универсальный ненастроенный вариант веб-части.</span><span class="sxs-lookup"><span data-stu-id="2d424-281">It might be a good idea to provide a generic unconfigured variant of your web part as well.</span></span>

1. <span data-ttu-id="2d424-p131">Откройте в редакторе кода файл **./src/webparts/gallery/GalleryWebPart.manifest.json**. Замените содержимое свойства **preconfiguredEntries** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="2d424-p131">In the code editor, open the **./src/webparts/gallery/GalleryWebPart.manifest.json** file. Change the **preconfiguredEntries** property to:</span></span>

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent images" },
      "description": { "default": "Shows 5 most recent images" },
      "officeFabricIconFontName": "Picture",
      "properties": {
        "listName": "Images",
        "order": "reversed",
        "numberOfItems": 5,
        "style": "thumbnails"
      }
    },
    {
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Recent documents" },
      "description": { "default": "Shows 10 most recent documents" },
      "officeFabricIconFontName": "Documentation",
      "properties": {
        "listName": "Documents",
        "order": "reversed",
        "numberOfItems": 10,
        "style": "list"
      }
    },
    {
      "groupId": "6737645a-4443-4210-a70e-e5e2a219133a",
      "group": { "default": "Content" },
      "title": { "default": "Gallery" },
      "description": { "default": "Shows items from the selected list" },
      "officeFabricIconFontName": "CustomList",
      "properties": {
        "listName": "",
        "order": "",
        "numberOfItems": 5,
        "style": ""
      }
    }]
  }
  ```

2. <span data-ttu-id="2d424-284">Обратите внимание, что универсальная ненастроенная версия веб-части добавляется к конфигурациям для определенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="2d424-284">Notice that the generic unconfigured version of the web part is added next to the configurations that target specific scenarios.</span></span> <span data-ttu-id="2d424-285">Таким образом, если для потребностей пользователя нет соответствующей конфигурации, он может выбрать универсальную версию и настроить ее по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="2d424-285">The generic unconfigured version of the web part is added beside the configurations that target specific scenarios. This way, if there is no specific configuration addressing users' needs, they can always use the generic version and configure it according to their requirements.</span></span>

3. <span data-ttu-id="2d424-286">Чтобы увидеть результат, запустите отладку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d424-286">To see the result start debugging the project by running the following command:</span></span>

  ```sh
  gulp serve
  ```

4. <span data-ttu-id="2d424-287">Открыв панель элементов веб-частей для добавления веб-части на холст, вы увидите, что теперь пользователь может выбрать одну из трех веб-частей.</span><span class="sxs-lookup"><span data-stu-id="2d424-287">When you open the web part toolbox to add the web part to the canvas, you will see that there are now three web parts that users can choose from.</span></span>

  ![Панель элементов с предварительно настроенной версией веб-части](../../../images/preconfiguredentries-three-configurations-toolbox.png)
