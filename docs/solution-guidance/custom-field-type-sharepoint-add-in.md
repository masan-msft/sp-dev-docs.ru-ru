---
title: "Тип настраиваемого поля в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 550669c2e1cb7e766f93ed1ae00fc0962421bace
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="custom-field-type-in-the-sharepoint-add-in-model"></a><span data-ttu-id="e3e03-102">Тип настраиваемого поля в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="e3e03-102">Custom field type in the SharePoint add-in model</span></span>
================================================

<a name="summary"></a><span data-ttu-id="e3e03-103">Summary</span><span class="sxs-lookup"><span data-stu-id="e3e03-103">Summary</span></span>
-------

<span data-ttu-id="e3e03-104">Выбор подхода для обеспечения работы настраиваемого конечного пользователя отличается новой модели надстройки SharePoint от был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="e3e03-104">The approach you take to provide customized end user experiences is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="e3e03-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, настраиваемые типы полей были созданы с помощью кода на сервере объектной модели SharePoint путем наследования от одного из классов встроенных типов полей для создания файла развертывания типов полей (XML).</span><span class="sxs-lookup"><span data-stu-id="e3e03-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, custom field types were created with the SharePoint server-side object model code by inheriting from one of the built-in field type classes and creating a field type deployment file (XML).</span></span> <span data-ttu-id="e3e03-106">Эти компоненты были развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-106">These components were deployed via SharePoint solutions.</span></span> 

<span data-ttu-id="e3e03-107">В сценарии модели надстройки SharePoint каждый раз пользовательское реализуются с помощью обработки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e3e03-107">In a SharePoint Add-ins model scenario, customized end user experiences are implemented via client-side rendering.</span></span> <span data-ttu-id="e3e03-108">В этот подход файлы JavaScript, используемых для реализации работы настраиваемого конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="e3e03-108">In this approach, JavaScript files are used to implement customized end user experiences.</span></span> <span data-ttu-id="e3e03-109">Удаленный подготовки шаблон развертывает файлы JavaScript и регистрирует их с полями SharePoint через свойство JSLink.</span><span class="sxs-lookup"><span data-stu-id="e3e03-109">The remote provisioning pattern deploys the JavaScript files and registers them with SharePoint fields via the JSLink property.</span></span>

<span data-ttu-id="e3e03-110">С точки зрения конечного пользователя, и возможность/результат выглядит так же.</span><span class="sxs-lookup"><span data-stu-id="e3e03-110">From an end user's perspective the capability/result looks the same.</span></span>

<span data-ttu-id="e3e03-111">Вот несколько примеров настраиваемого типа поля, который реализует Google карты.</span><span class="sxs-lookup"><span data-stu-id="e3e03-111">Here are some examples of custom field type that implements a Google map.</span></span> <span data-ttu-id="e3e03-112">Эти поступают из примера PnP [Branding.JSLink](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink) Office 365.</span><span class="sxs-lookup"><span data-stu-id="e3e03-112">These come from the [Branding.JSLink](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink) Office 365 PnP Sample.</span></span>

<span data-ttu-id="e3e03-113">**Google карты эскизов отображается в представлении списка:**</span><span class="sxs-lookup"><span data-stu-id="e3e03-113">**Thumbnail Google map images displayed in a list view:**</span></span>

![Два представления карты Google, отражающая точка расположении Microsoft территории и расположение области.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps.png)

<span data-ttu-id="e3e03-115">**Встроенное редактирование отображение большего эскиза карты Google:**
![сопоставляет два Google.</span><span class="sxs-lookup"><span data-stu-id="e3e03-115">**Inline editing showing a larger Google map thumbnail:**
![Two Google maps.</span></span> <span data-ttu-id="e3e03-116">Отображение точка расположении территории Microsoft со ссылкой выберите расположение, другие представление со значениями области расположение территории корпорации Майкрософт со ссылкой на изменение фигуры одно представление.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Edit.png)</span><span class="sxs-lookup"><span data-stu-id="e3e03-116">One view showing the Microsoft Campus Location Point with a link to Select Location, the other view showing the Microsoft Campus Location Area with a link to Edit Shape.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Edit.png)</span></span>

<span data-ttu-id="e3e03-117">**Диалоговое окно включения встроенная Правка:**
![карты Google отображение фигуры территории корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e3e03-117">**A dialog enabling inline editing:**
![A Google Map showing the Microsoft Campus Shape.</span></span> <span data-ttu-id="e3e03-118">Считывает текст на изображении, щелкните на карте, чтобы поместить маркерами и создание фигуры.</span><span class="sxs-lookup"><span data-stu-id="e3e03-118">Text on the image reads, Click on the map to place markers and create your shape.</span></span> <span data-ttu-id="e3e03-119">Завершить, щелкнув на первый маркер.</span><span class="sxs-lookup"><span data-stu-id="e3e03-119">Finish by clicking on the first marker.</span></span> <span data-ttu-id="e3e03-120">Перетащите каждый из маркеров вокруг или щелкните Дополнительные параметры.</span><span class="sxs-lookup"><span data-stu-id="e3e03-120">You can drag each of the markers around, or click on them for more options.</span></span> <span data-ttu-id="e3e03-121">Кнопка очистки соответствия выше можно использовать для удаления всех маркеров.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Shape_Edit.png)</span><span class="sxs-lookup"><span data-stu-id="e3e03-121">You can use the Clear Map button above to remove all markers.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Shape_Edit.png)</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="e3e03-122">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="e3e03-122">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="e3e03-123">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для реализации обработки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e3e03-123">As a rule of a thumb, we would like to provide the following high-level guidelines for implementing client-side rendering.</span></span>

- <span data-ttu-id="e3e03-124">Для реализации настраиваемые типы полей используйте файлы JavaScript и обработки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e3e03-124">Use JavaScript files and client-side rendering to implement custom field types.</span></span>
- <span data-ttu-id="e3e03-125">Шаблон удаленного подготовки для развертывания файлов JavaScript и зарегистрировать их с полями SharePoint или веб-частей представления списка.</span><span class="sxs-lookup"><span data-stu-id="e3e03-125">Use the remote provisioning pattern to deploy JavaScript files and register them with SharePoint fields or List View Web Parts.</span></span>
- <span data-ttu-id="e3e03-126">Регистрация файлов JavaScript с ядром стратегия минимальной загрузки (MDS), чтобы убедиться, что модуль MDS принять во внимание файлов JavaScript пользовательской визуализации.</span><span class="sxs-lookup"><span data-stu-id="e3e03-126">Register the JavaScript files with the Minimal Download Strategy (MDS) engine to ensure the MDS engine is aware of the custom rendering JavaScript files.</span></span>
- <span data-ttu-id="e3e03-127">Установка для свойства JSLink хост-сайта требуется по крайней мере полное разрешение на уровне веб-, поэтому этот подход не подходит для надстроек в магазине SharePoint</span><span class="sxs-lookup"><span data-stu-id="e3e03-127">Setting JSLink property to host web requires at least full permission at web level, so this approach is not suitable for add-ins at the SharePoint store</span></span>

<a name="options-to-implement-client-side-rendering-with-javascript-files-via-the-jslink-property"></a><span data-ttu-id="e3e03-128">Параметры для реализации обработки на стороне клиента с помощью файлов JavaScript через свойство JSLink</span><span class="sxs-lookup"><span data-stu-id="e3e03-128">Options to implement client-side rendering with JavaScript files via the JSLink property</span></span>
----------------------------------------------------------------------------------------

<span data-ttu-id="e3e03-129">У вас есть две возможности для реализации обработки на стороне клиента с помощью файлов JavaScript через свойство JSLink.</span><span class="sxs-lookup"><span data-stu-id="e3e03-129">You have a couple of options to implement client-side rendering with JavaScript files via the JSLink property.</span></span>

- <span data-ttu-id="e3e03-130">Присвойте свойству JSLink на веб-часть представления списка, который отображает список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-130">Set the JSLink property on a List View Web Part that renders a view of a SharePoint list.</span></span> 
- <span data-ttu-id="e3e03-131">Присвойте свойству JSLink для поля SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-131">Set the JSLink property for a SharePoint field.</span></span> 
- <span data-ttu-id="e3e03-132">Присвойте свойству JSLink для типа контента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-132">Set the JSLink property for a SharePoint content type.</span></span> 
    

<a name="set-the-jslink-property-on-a-list-view-web-part-that-renders-a-view-of-a-sharepoint-list"></a><span data-ttu-id="e3e03-133">Присвойте свойству JSLink на веб-часть представления списка, который отображает представление списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="e3e03-133">Set the JSLink property on a List View Web Part that renders a view of a SharePoint list</span></span>
-----------------------------------------------------------------------------------------
<span data-ttu-id="e3e03-134">В этот параметр, задайте свойству JSLink на WebPartDefinition.</span><span class="sxs-lookup"><span data-stu-id="e3e03-134">In this option you set the JSLink property on a WebPartDefinition.</span></span>
    
- <span data-ttu-id="e3e03-135">**Такой подход специально не создать настраиваемый тип поля на уровне SPField.**</span><span class="sxs-lookup"><span data-stu-id="e3e03-135">**This approach does not specifically create a custom field type at the SPField level.**</span></span>
    + <span data-ttu-id="e3e03-136">Таким образом, *пользовательской визуализации применяется только в веб-часть представления списка, где присвойте свойству JSLink*.</span><span class="sxs-lookup"><span data-stu-id="e3e03-136">Therefore, *the custom rendering only applies in the List View Web Part where you set the JSLink property*.</span></span>
- <span data-ttu-id="e3e03-137">Такой подход позволяет изменять с отображением для одного или нескольких полей SharePoint за один раз.</span><span class="sxs-lookup"><span data-stu-id="e3e03-137">This approach allows you to change the rendering for one or more SharePoint fields at once.</span></span>
- <span data-ttu-id="e3e03-138">Этот подход может быть выполнено с помощью декларативного кода с помощью серверного объектной модели SharePoint, с помощью клиентской объектной модели SharePoint (CSOM) или через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3e03-138">This approach may be done with declarative code, with the SharePoint server-side object model, with the SharePoint client-side object model (CSOM), or via PowerShell.</span></span>
    + <span data-ttu-id="e3e03-139">Мы рекомендуем использовать на сервере объектной модели SharePoint, клиентской объектной модели SharePoint или PowerShell для свойства JSLink с помощью удаленного подготовки шаблон.</span><span class="sxs-lookup"><span data-stu-id="e3e03-139">We recommend you use the SharePoint server-side object model, the SharePoint client-side object model, or PowerShell to set the JSLink property via the remote provisioning pattern.</span></span>

<span data-ttu-id="e3e03-140">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="e3e03-140">**When is it a good fit?**</span></span>

<span data-ttu-id="e3e03-141">При необходимости для определения конкретного представления для данных списков SharePoint и изменения представления для более одного поля SharePoint это является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="e3e03-141">When you need to define specific views for SharePoint list data and modify the rendering for more than one SharePoint field, this is a good option.</span></span>

<span data-ttu-id="e3e03-142">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="e3e03-142">**Getting started**</span></span>

<span data-ttu-id="e3e03-143">Следующий пример задает свойство JSLink на веб-часть представления списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-143">The following sample sets the JSLink property on a SharePoint List View Web Part.</span></span>

- [<span data-ttu-id="e3e03-144">Branding.ClientSideRendering (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="e3e03-144">Branding.ClientSideRendering (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + <span data-ttu-id="e3e03-145">Включает в себя 9 примеров, присвойте свойству JSLink на веб-часть представления списка SharePoint и объяснение реализации каждого примера.</span><span class="sxs-lookup"><span data-stu-id="e3e03-145">Includes 9 samples that set the JSLink property on a SharePoint List View Web Part and an explanation of how each sample was implemented.</span></span>
    + <span data-ttu-id="e3e03-146">Метод RegisterJStoWebPart задает свойство JSLink списка представления веб-части.</span><span class="sxs-lookup"><span data-stu-id="e3e03-146">The RegisterJStoWebPart method sets the List View Web Part's JSLink property.</span></span> 

<a name="set-the-jslink-property-for-a-sharepoint-field"></a><span data-ttu-id="e3e03-147">Задайте для свойства JSLink для поля SharePoint</span><span class="sxs-lookup"><span data-stu-id="e3e03-147">Set the JSLink property for a SharePoint field</span></span>
----------------------------------------------

<span data-ttu-id="e3e03-148">В этот параметр, задайте свойству JSLink на SPField.</span><span class="sxs-lookup"><span data-stu-id="e3e03-148">In this option you set the JSLink property on an SPField.</span></span>
    
- <span data-ttu-id="e3e03-149">**Такой подход специально регистрирует свойство JSLink на уровне SPField.**</span><span class="sxs-lookup"><span data-stu-id="e3e03-149">**This approach specifically registers the JSLink property at the SPField level.**</span></span>
    + <span data-ttu-id="e3e03-150">Таким образом, *пользовательской визуализации будут применяться везде, где отображается SPField*.</span><span class="sxs-lookup"><span data-stu-id="e3e03-150">Therefore, *the custom rendering will apply everywhere the SPField is rendered*.</span></span>
- <span data-ttu-id="e3e03-151">Такой подход позволяет изменить визуализации для одного поля SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-151">This approach allows you to change the rendering for one SharePoint field.</span></span>
- <span data-ttu-id="e3e03-152">Этот подход может быть выполнено с помощью декларативного кода с помощью серверного объектной модели SharePoint, с помощью клиентской объектной модели SharePoint или через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3e03-152">This approach may be done with declarative code, with the SharePoint server-side object model, with the SharePoint client-side object model, or via PowerShell.</span></span>
    + <span data-ttu-id="e3e03-153">Мы рекомендуем использовать на сервере объектной модели SharePoint, клиентской объектной модели SharePoint или PowerShell для свойства JSLink с помощью удаленного подготовки шаблон.</span><span class="sxs-lookup"><span data-stu-id="e3e03-153">We recommend you use the SharePoint server-side object model, the SharePoint client-side object model, or PowerShell to set the JSLink property via the remote provisioning pattern.</span></span>

<span data-ttu-id="e3e03-154">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="e3e03-154">**When is it a good fit?**</span></span>

<span data-ttu-id="e3e03-155">Если вам необходимо определить определенного представления для указанного поля SharePoint и убедитесь, что представление всегда используется при отображении поля, это является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="e3e03-155">When you need to define a specific view for a given SharePoint field and ensure the view is always used when the field is rendered, this is a good option.</span></span>

<span data-ttu-id="e3e03-156">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="e3e03-156">**Getting started**</span></span>

<span data-ttu-id="e3e03-157">Следующие статьи показано, как задать свойство JSLink на SPField.</span><span class="sxs-lookup"><span data-stu-id="e3e03-157">The following articles demonstrate how to set the JSLink property on a SPField.</span></span>

- [<span data-ttu-id="e3e03-158">С помощью свойства JSLink, чтобы изменить способ отображения поля или представления в SharePoint 2013 (Тобиаса Zimmergren)</span><span class="sxs-lookup"><span data-stu-id="e3e03-158">Using the JSLink property to change the way your field or views are rendered in SharePoint 2013 (Tobias Zimmergren)</span></span>](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [<span data-ttu-id="e3e03-159">С помощью JSLink с SharePoint 2013 (журнал MSDN)</span><span class="sxs-lookup"><span data-stu-id="e3e03-159">Using JSLink with SharePoint 2013 (MSDN Magazine)</span></span>](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)

<a name="challenges-with-implementing-client-side-rendering-with-javascript-files-via-the-jslink-property"></a><span data-ttu-id="e3e03-160">Проблемы, связанные с с реализация обработки на стороне клиента с помощью файлов JavaScript через свойство JSLink</span><span class="sxs-lookup"><span data-stu-id="e3e03-160">Challenges with implementing client-side rendering with JavaScript files via the JSLink property</span></span>
------------------------------------------------------------------------------------------------

<span data-ttu-id="e3e03-161">При разработке компонентов настраиваемой обработки на стороне клиента, следует помнить следующее.</span><span class="sxs-lookup"><span data-stu-id="e3e03-161">As you develop custom client-side rendering components, keep in mind the following things.</span></span>

- <span data-ttu-id="e3e03-162">Не все поля SharePoint может быть переопределен с помощью свойства JSLink.</span><span class="sxs-lookup"><span data-stu-id="e3e03-162">Not all SharePoint fields may be overridden with the JSLink property.</span></span>
    + <span data-ttu-id="e3e03-163">TaxonomyField является хорошим примером.</span><span class="sxs-lookup"><span data-stu-id="e3e03-163">The TaxonomyField is a good example.</span></span>
- <span data-ttu-id="e3e03-164">JSLink поддерживает несколько токенов.</span><span class="sxs-lookup"><span data-stu-id="e3e03-164">JSLink supports several tokens.</span></span>
    + <span data-ttu-id="e3e03-165">_layouts</span><span class="sxs-lookup"><span data-stu-id="e3e03-165">_layouts</span></span>
    + <span data-ttu-id="e3e03-166">_SITE</span><span class="sxs-lookup"><span data-stu-id="e3e03-166">_site</span></span>
    + <span data-ttu-id="e3e03-167">_siteCollection</span><span class="sxs-lookup"><span data-stu-id="e3e03-167">_siteCollection</span></span>
    + <span data-ttu-id="e3e03-168">_siteCollectionLayouts</span><span class="sxs-lookup"><span data-stu-id="e3e03-168">_siteCollectionLayouts</span></span>
    + <span data-ttu-id="e3e03-169">_siteLayouts</span><span class="sxs-lookup"><span data-stu-id="e3e03-169">_siteLayouts</span></span>
- <span data-ttu-id="e3e03-170">Файлы JSLink JavaScript можно регистрировать с помощью платформы SharePoint скрипта на запросами (укладки ДЕРНА) для отложенной загрузки файла.</span><span class="sxs-lookup"><span data-stu-id="e3e03-170">You can register the JSLink JavaScript files with the SharePoint Script On Demand (SOD) framework to lazy load the file.</span></span>
    - <span data-ttu-id="e3e03-171">Используйте тег (d) в конце JSLink URL-адрес для регистрации файла с укладки ДЕРНА.</span><span class="sxs-lookup"><span data-stu-id="e3e03-171">Use the (d) tag at the end of the JSLink URL to register the file with the SOD.</span></span>
 
    ```
    ~sitecollection/Style Library/JSLink-Samples/DependentFields.js(d)
    ```
- <span data-ttu-id="e3e03-172">Для загрузки нескольких файлов JavaScript через свойство JSLink.</span><span class="sxs-lookup"><span data-stu-id="e3e03-172">You can load multiple JavaScript files via the JSLink property.</span></span>
    + <span data-ttu-id="e3e03-173">Это особенно удобно, если у вас есть библиотека файлов JavaScript, которые реализуют вашей обработки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="e3e03-173">This is especially helpful if you have a library of JavaScript files that implement your client-side rendering.</span></span>
    + <span data-ttu-id="e3e03-174">Рекомендуется использовать этот подход, когда для мобильных устройств, так как она позволяет обеспечить только что JavaScript, необходимых для реализации обработки на стороне клиента данное поле SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3e03-174">Consider using this approach when targeting mobile devices because it allows you to deliver just the JavaScript you need to implement a given SharePoint field's client-side rendering.</span></span>
    + <span data-ttu-id="e3e03-175">Использование | символ в отдельные файлы JavaScript, который вы хотите загрузить.</span><span class="sxs-lookup"><span data-stu-id="e3e03-175">Use the | character to separate the JavaScript files you wish to load.</span></span> 
    
    ```
    ~sitecollection/Style Library/JSLink-Samples/MainLibrary.js|~sitecollection/Style Library/JSLink-Samples/SpecificField.js**(d)**
    ```

<a name="related-links"></a><span data-ttu-id="e3e03-176">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="e3e03-176">Related links</span></span>
=============
- [<span data-ttu-id="e3e03-177">Свойство SPField.JSLink (документы API MSDN)</span><span class="sxs-lookup"><span data-stu-id="e3e03-177">SPField.JSLink property (MSDN API Docs)</span></span>](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfield.jslink.aspx)
- [<span data-ttu-id="e3e03-178">С помощью свойства JSLink, чтобы изменить способ отображения поля или представления в SharePoint 2013 (Тобиаса Zimmergren)</span><span class="sxs-lookup"><span data-stu-id="e3e03-178">Using the JSLink property to change the way your field or views are rendered in SharePoint 2013 (Tobias Zimmergren)</span></span>](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [<span data-ttu-id="e3e03-179">С помощью JSLink с SharePoint 2013 (журнал MSDN)</span><span class="sxs-lookup"><span data-stu-id="e3e03-179">Using JSLink with SharePoint 2013 (MSDN Magazine)</span></span>](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)
- <span data-ttu-id="e3e03-180">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="e3e03-180">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="e3e03-181">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="e3e03-181">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="e3e03-182">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="e3e03-182">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="e3e03-183">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="e3e03-183">Related PnP samples</span></span>
===================

- [<span data-ttu-id="e3e03-184">Branding.ClientSideRendering (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="e3e03-184">Branding.ClientSideRendering (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- [<span data-ttu-id="e3e03-185">Branding.JSLink (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="e3e03-185">Branding.JSLink (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink)
- <span data-ttu-id="e3e03-186">Примеры и содержимое в https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="e3e03-186">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="e3e03-187">Применимо к</span><span class="sxs-lookup"><span data-stu-id="e3e03-187">Applies to</span></span>
==========
- <span data-ttu-id="e3e03-188">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="e3e03-188">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="e3e03-189">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="e3e03-189">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="e3e03-190">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="e3e03-190">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="e3e03-191">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="e3e03-191">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
