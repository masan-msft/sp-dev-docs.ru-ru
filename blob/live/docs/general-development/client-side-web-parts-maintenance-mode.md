---
title: "Режим обслуживания клиентских веб-частей"
ms.date: 12/18/2017
ms.prod: sharepoint
ms.assetid: 3ebd2a11-8291-4228-add0-9e0cd899dd3c
ms.openlocfilehash: 208a9ef5fea879fa7d27811595ebc8d37881d3b2
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="maintenance-mode-for-client-side-web-parts"></a><span data-ttu-id="c6210-102">Режим обслуживания клиентских веб-частей</span><span class="sxs-lookup"><span data-stu-id="c6210-102">Maintenance mode for client-side web parts</span></span>

<span data-ttu-id="c6210-103">_**Область применения:** Office 365_</span><span class="sxs-lookup"><span data-stu-id="c6210-103">\*Applies to: Office 365</span></span>

<span data-ttu-id="c6210-104">Работая с клиентскими веб-частями, вы можете загружать их в режиме обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c6210-104">When working with client-side web parts, you can load them in maintenance mode.</span></span> <span data-ttu-id="c6210-105">Это может быть полезно для поиска проблем, связанных с веб-частями, добавленными на страницу.</span><span class="sxs-lookup"><span data-stu-id="c6210-105">The maintenance mode can be helpful when trying to debug issues related to web parts placed on the page.</span></span>

## <a name="switch-to-maintenance-mode"></a><span data-ttu-id="c6210-106">Переключение в режим обслуживания</span><span class="sxs-lookup"><span data-stu-id="c6210-106">Switch to maintenance mode</span></span>

> [!NOTE]
> <span data-ttu-id="c6210-107">Чтобы загрузить страницу в режиме обслуживания, необходимо изменить разрешения для нее.</span><span class="sxs-lookup"><span data-stu-id="c6210-107">In order to load a page in the maintenance mode, you have to have edit permissions for that specific page.</span></span>

<span data-ttu-id="c6210-108">Чтобы переключиться в режим обслуживания, перейдите на страницу и добавьте к URL-адресу `?maintenancemode=true`, например:</span><span class="sxs-lookup"><span data-stu-id="c6210-108">To switch to the maintenance mode, navigate to the page and in the URL append `?maintenancemode=true`, for example:</span></span>

```text
https://contoso.sharepoint.com/sites/team?maintenancemode=true
```

<span data-ttu-id="c6210-109">Чтобы выйти из режима обслуживания, удалите `?maintenancemode=true` из URL-адреса и перезагрузите страницу.</span><span class="sxs-lookup"><span data-stu-id="c6210-109">To leave the maintenance mode, remove `?maintenancemode=true` from the URL and reload the page.</span></span>

## <a name="available-information"></a><span data-ttu-id="c6210-110">Доступные сведения</span><span class="sxs-lookup"><span data-stu-id="c6210-110">Available information</span></span>

<span data-ttu-id="c6210-111">В режиме обслуживания отображаются различные сведения о каждой веб-части на странице.</span><span class="sxs-lookup"><span data-stu-id="c6210-111">The maintenance mode shows various information about each web part on the page.</span></span>

### <a name="web-part-summary"></a><span data-ttu-id="c6210-112">Общие сведения о веб-частях</span><span class="sxs-lookup"><span data-stu-id="c6210-112">Web part summary</span></span>

<span data-ttu-id="c6210-113">В режиме обслуживания отображаются следующие сводные сведения о каждой веб-части:</span><span class="sxs-lookup"><span data-stu-id="c6210-113">When in maintenance mode, for each web part you will see the following summary information:</span></span>

![Сводные сведения о веб-частях, отображаемые в режиме обслуживания](../images/maintenance-mode-summary.png)

<span data-ttu-id="c6210-115">Свойство</span><span class="sxs-lookup"><span data-stu-id="c6210-115">Property</span></span>|<span data-ttu-id="c6210-116">Описание</span><span class="sxs-lookup"><span data-stu-id="c6210-116">Description</span></span>
--------|-----------
<span data-ttu-id="c6210-117">Alias</span><span class="sxs-lookup"><span data-stu-id="c6210-117">Alias</span></span>|<span data-ttu-id="c6210-118">Псевдоним веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-118">Web part alias</span></span>
<span data-ttu-id="c6210-119">Id</span><span class="sxs-lookup"><span data-stu-id="c6210-119">Id</span></span>|<span data-ttu-id="c6210-120">Уникальный идентификатор веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-120">The unique ID of the web part</span></span>
<span data-ttu-id="c6210-121">InstanceId</span><span class="sxs-lookup"><span data-stu-id="c6210-121">InstanceID</span></span>|<span data-ttu-id="c6210-122">ИД определенного экземпляра веб-части (если на странице есть еще две такие же веб-части, то у них будут одинаковые ИД веб-части, но разные ИД экземпляра).</span><span class="sxs-lookup"><span data-stu-id="c6210-122">The ID of a specific instance of a web part (that is, if you have two more of the same web parts on a page, they will each have the same web part ID, but a different instance ID.</span></span>
<span data-ttu-id="c6210-123">IsInternal</span><span class="sxs-lookup"><span data-stu-id="c6210-123">IsInternal</span></span>|<span data-ttu-id="c6210-124">Указывает, кто является производителем веб-части: корпорация Майкрософт или сторонняя компания.</span><span class="sxs-lookup"><span data-stu-id="c6210-124">Indicates whether the web part was made by Microsoft or a third party.</span></span> <span data-ttu-id="c6210-125">Если задано значение `true`, веб-часть создана корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c6210-125">If `true`, it is made by Microsoft.</span></span> <span data-ttu-id="c6210-126">Если же задано значение `false`, то это веб-часть от стороннего производителя.</span><span class="sxs-lookup"><span data-stu-id="c6210-126">If `false`, it is made by a third party.</span></span>
<span data-ttu-id="c6210-127">Version</span><span class="sxs-lookup"><span data-stu-id="c6210-127">Version</span></span>|<span data-ttu-id="c6210-128">Номер версии веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-128">The version number of the web part.</span></span>
<span data-ttu-id="c6210-129">Environment</span><span class="sxs-lookup"><span data-stu-id="c6210-129">Environment</span></span>|<span data-ttu-id="c6210-130">Перечисление, указывающее, в какой среде работает веб-часть.</span><span class="sxs-lookup"><span data-stu-id="c6210-130">Enumeration indicating the environment on which the web part is running.</span></span> <span data-ttu-id="c6210-131">Допустимые значения: `1` (локальная среда разработки), `2` (SharePoint).</span><span class="sxs-lookup"><span data-stu-id="c6210-131">Possible values: `1` - Local Workbench, `2` - SharePoint</span></span>
<span data-ttu-id="c6210-132">UserAgent</span><span class="sxs-lookup"><span data-stu-id="c6210-132">UserAgent</span></span>|<span data-ttu-id="c6210-133">Строка, содержащая сведения об используемых устройстве и ПО (например, типе и версии браузера).</span><span class="sxs-lookup"><span data-stu-id="c6210-133">A string that contains information about the device and software in use (such as browser type and version).</span></span>

### <a name="web-part-manifest"></a><span data-ttu-id="c6210-134">Манифест веб-части</span><span class="sxs-lookup"><span data-stu-id="c6210-134">Web part manifest</span></span>

<span data-ttu-id="c6210-135">Дополнительные сведения о веб-части можно найти на вкладке **Манифест**.</span><span class="sxs-lookup"><span data-stu-id="c6210-135">To get more information about the web part, switch to the **Manifest** tab.</span></span>

![Сведения из манифеста веб-части, отображаемые в режиме обслуживания](../images/maintenance-mode-manifest.png)

<span data-ttu-id="c6210-137">Изучив данные манифеста, вы можете узнать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="c6210-137">By exploring the manifest information, you can learn details such as:</span></span>

- <span data-ttu-id="c6210-138">где размещен пакет веб-части;</span><span class="sxs-lookup"><span data-stu-id="c6210-138">where the web part bundle is hosted</span></span>
- <span data-ttu-id="c6210-139">какие внешние скрипты загружает веб-часть и откуда;</span><span class="sxs-lookup"><span data-stu-id="c6210-139">which external scripts is the web part loading and from where</span></span>
- <span data-ttu-id="c6210-140">на какой версии SharePoint Framework основана веб-часть;</span><span class="sxs-lookup"><span data-stu-id="c6210-140">what version of the SharePoint Framework has the web part been built on</span></span>
- <span data-ttu-id="c6210-141">какие компоненты SharePoint Framework используются в веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-141">which components of the SharePoint Framework does the web part use</span></span>

<span data-ttu-id="c6210-142">Эти сведения могут быть незаменимы при поисках причины неисправности в определенной веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-142">This information can be invaluable when trying to find a reason why the particular web part is malfunctioning.</span></span>

### <a name="web-part-data"></a><span data-ttu-id="c6210-143">Данные веб-частей</span><span class="sxs-lookup"><span data-stu-id="c6210-143">Web part data</span></span>

<span data-ttu-id="c6210-144">В режиме обслуживания также доступны данные веб-частей.</span><span class="sxs-lookup"><span data-stu-id="c6210-144">Another piece of information available in the maintenance mode, is web part data.</span></span>

![Данные веб-частей, отображаемые в режиме обслуживания](../images/maintenance-mode-data.png)

<span data-ttu-id="c6210-146">На вкладке **Данные** можно просмотреть сведения о конфигурации каждой веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-146">Using the information from the **Data** tab, you can see the configuration for each web part.</span></span> <span data-ttu-id="c6210-147">Это может помочь воспроизвести ошибки, о которых сообщили пользователи, если они вызваны определенной конфигурацией веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-147">This is helpful when trying to reproduce errors reported by users which could be caused by a specific web part configuration.</span></span>

<span data-ttu-id="c6210-148">Если веб-часть [интегрирует свои свойства с SharePoint](../spfx/web-parts/guidance/integrate-web-part-properties-with-sharepoint.md), то в разделе данных отображаются типы и значения, передаваемые в SharePoint для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="c6210-148">If the web part [integrates its properties with SharePoint](../spfx/web-parts/guidance/integrate-web-part-properties-with-sharepoint.md), the data section shows the types and values that are passed to SharePoint for further processing.</span></span>

## <a name="considerations"></a><span data-ttu-id="c6210-149">Замечания</span><span class="sxs-lookup"><span data-stu-id="c6210-149">Considerations</span></span>

- <span data-ttu-id="c6210-150">В режиме обслуживания можно загружать клиентские веб-части, размещенные как на современных, так и на классических страницах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c6210-150">the maintenance mode works for client-side web parts placed on both modern and classic SharePoint pages.</span></span> <span data-ttu-id="c6210-151">Дополнительные сведения об открытии классических веб-частей в режиме обслуживания см. в статье [Открытие и использование страницы обслуживания веб-частей]((https://support.office.com/ru-RU/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2)#PickTab=2016,_2013).</span><span class="sxs-lookup"><span data-stu-id="c6210-151">See the [Open and use the web part maintenance page]((https://support.office.com/ru-RU/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2)#PickTab=2016,_2013) support article, to get more information about opening classic web parts in maintenance view</span></span>
- <span data-ttu-id="c6210-152">Чтобы открыть страницу в режиме обслуживания, необходимы разрешения на редактирование этой страницы.</span><span class="sxs-lookup"><span data-stu-id="c6210-152">to open page in maintenance mode, you have to have edit permissions for that page</span></span>
- <span data-ttu-id="c6210-153">В режиме обслуживания код веб-части не выполняется, а свойства веб-части невозможно редактировать.</span><span class="sxs-lookup"><span data-stu-id="c6210-153">when in maintenance mode, web part code is not being executed and you cannot edit web part properties</span></span>
- <span data-ttu-id="c6210-154">В режиме обслуживания можно удалять и перемещать веб-части на странице.</span><span class="sxs-lookup"><span data-stu-id="c6210-154">in maintenance mode, you can delete or move web parts on the page</span></span>
- <span data-ttu-id="c6210-155">В режиме обслуживания отображаются только сведения о веб-частях.</span><span class="sxs-lookup"><span data-stu-id="c6210-155">the maintenance mode shows only information about web parts.</span></span> <span data-ttu-id="c6210-156">В нем не отображаются сведения о расширениях SharePoint Framework, выполняемых на странице.</span><span class="sxs-lookup"><span data-stu-id="c6210-156">You cannot use it to show information about SharePoint Framework extensions that are executed on the page</span></span>
- <span data-ttu-id="c6210-157">При переключении в режим обслуживания отключается только выполнение кода веб-части.</span><span class="sxs-lookup"><span data-stu-id="c6210-157">switching to maintenance mode only disables executing web part code.</span></span> <span data-ttu-id="c6210-158">Все расширения SharePoint Framework, зарегистрированные на странице, по-прежнему будут работать.</span><span class="sxs-lookup"><span data-stu-id="c6210-158">Any SharePoint Framework extensions registered on the page will still execute</span></span>

## <a name="see-also"></a><span data-ttu-id="c6210-159">См. также</span><span class="sxs-lookup"><span data-stu-id="c6210-159">See also</span></span>

- <span data-ttu-id="c6210-160">[Открытие и использование страницы обслуживания веб-частей]((https://support.office.com/ru-RU/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2))</span><span class="sxs-lookup"><span data-stu-id="c6210-160">[Open and use the web part maintenance page]((https://support.office.com/ru-RU/article/Open-and-use-the-web-part-maintenance-page-eff9ce22-d04a-44dd-ae83-ac29a5e396c2))</span></span>