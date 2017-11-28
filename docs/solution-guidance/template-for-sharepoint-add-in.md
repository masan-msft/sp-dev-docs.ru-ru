---
title: "XYZ объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: f7985dea33c851019185b25ffb26241ddbc73cd2
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="xyz-in-the-sharepoint-add-in-model"></a><span data-ttu-id="dd83f-102">XYZ объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd83f-102">XYZ in the SharePoint add-in model</span></span>
==================================

<a name="summary"></a><span data-ttu-id="dd83f-103">Summary</span><span class="sxs-lookup"><span data-stu-id="dd83f-103">Summary</span></span>
-------

- <span data-ttu-id="dd83f-104">Необходимо предоставить контекст и краткое описание как было сделано возможность с помощью FTC</span><span class="sxs-lookup"><span data-stu-id="dd83f-104">Need to Provide context and short introduction how the capability was done using FTC</span></span>
- <span data-ttu-id="dd83f-105">Обзор — очень важно небольшой и четкие, чтобы создать мы контекст статьи.</span><span class="sxs-lookup"><span data-stu-id="dd83f-105">Summary is really important to keep small and crisp, so that we get the context of the article.</span></span>

<a name="why-would-you-customize-xyz"></a><span data-ttu-id="dd83f-106">Почему настроить XYZ?</span><span class="sxs-lookup"><span data-stu-id="dd83f-106">Why would you customize XYZ?</span></span>
----------------------------------------------------

<span data-ttu-id="dd83f-107">В этом разделе содержатся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="dd83f-107">This section contains the following information:</span></span>
- <span data-ttu-id="dd83f-108">Рекомендации по работе</span><span class="sxs-lookup"><span data-stu-id="dd83f-108">Guidelines</span></span>
    + <span data-ttu-id="dd83f-109">Пример маркера Sub</span><span class="sxs-lookup"><span data-stu-id="dd83f-109">Sub bullet example</span></span>
- <span data-ttu-id="dd83f-110">Summary</span><span class="sxs-lookup"><span data-stu-id="dd83f-110">Summary</span></span>
- <span data-ttu-id="dd83f-111">Пример</span><span class="sxs-lookup"><span data-stu-id="dd83f-111">Example</span></span>

<a name="challenges-applying-xyz-customizations"></a><span data-ttu-id="dd83f-112">Проблемы, связанные с применение настроек XYZ</span><span class="sxs-lookup"><span data-stu-id="dd83f-112">Challenges applying XYZ customizations</span></span>
----------------------------------------------------------------------

<span data-ttu-id="dd83f-113">Начнем с определения возможности проблемой и что мы пытаетесь решить здесь.</span><span class="sxs-lookup"><span data-stu-id="dd83f-113">Let’s start with defining what is the challenge and what are we trying to solve here.</span></span> 

<span data-ttu-id="dd83f-114">**Пример изображения**</span><span class="sxs-lookup"><span data-stu-id="dd83f-114">**Sample Image**</span></span>

![Пример изображения замещающий текст](media/Recipes/Themes/Agenda.png)

<span data-ttu-id="dd83f-116">В этом разделе содержатся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="dd83f-116">This section contains the following information:</span></span>
- <span data-ttu-id="dd83f-117">Проблемы, связанные с</span><span class="sxs-lookup"><span data-stu-id="dd83f-117">Challenges</span></span>
- <span data-ttu-id="dd83f-118">Различные варианты применения настройки</span><span class="sxs-lookup"><span data-stu-id="dd83f-118">Different options for applying customization</span></span>

<span data-ttu-id="dd83f-119">В этом разделе содержатся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="dd83f-119">This section contains the following information:</span></span>

- <span data-ttu-id="dd83f-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="dd83f-120">Options</span></span>
- <span data-ttu-id="dd83f-121">Параметры уровня набора приложений Office 365</span><span class="sxs-lookup"><span data-stu-id="dd83f-121">Office 365 suite level settings</span></span>

<span data-ttu-id="dd83f-122">В этом разделе содержатся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="dd83f-122">This section contains the following information:</span></span>

- <span data-ttu-id="dd83f-123">Вариант</span><span class="sxs-lookup"><span data-stu-id="dd83f-123">Describe the option</span></span>
- <span data-ttu-id="dd83f-124">Включать схемы, если это имеет смысл</span><span class="sxs-lookup"><span data-stu-id="dd83f-124">Include a diagram if it makes sense</span></span>
- <span data-ttu-id="dd83f-125">Показать пример когда хорошо работает этот параметр</span><span class="sxs-lookup"><span data-stu-id="dd83f-125">Show an example of when this option works well</span></span>
- <span data-ttu-id="dd83f-126">Указание на технические примечания о этот параметр</span><span class="sxs-lookup"><span data-stu-id="dd83f-126">Point out any technical notes about this option</span></span>

<a name="related-links"></a><span data-ttu-id="dd83f-127">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="dd83f-127">Related links</span></span>
=============
- [<span data-ttu-id="dd83f-128">Настройка OneDrive для бизнеса сайты с моделью приложений (статья блога MSDN)</span><span class="sxs-lookup"><span data-stu-id="dd83f-128">Customizing OneDrive for Business sites with app model (MSDN blog article)</span></span>](http://blogs.msdn.com/b/vesku/archive/2015/01/01/customizing-onedrive-for-business-sites-with-app-model.aspx)
- <span data-ttu-id="dd83f-129">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="dd83f-129">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="dd83f-130">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="dd83f-130">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="dd83f-131">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="dd83f-131">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="dd83f-132">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="dd83f-132">Related PnP samples</span></span>
===================

- <span data-ttu-id="dd83f-133">Настройка OD4B сайтов с использованием шаблона асинхронного</span><span class="sxs-lookup"><span data-stu-id="dd83f-133">Customizing OD4B sites using Async pattern</span></span>
- <span data-ttu-id="dd83f-134">Классический надстройки часть и синхронизации процесс для настройки сайта OD4B</span><span class="sxs-lookup"><span data-stu-id="dd83f-134">Classic add-in part and sync process for OD4B site customization</span></span>
- <span data-ttu-id="dd83f-135">Предварительное создание OD4B сайты для пользователей</span><span class="sxs-lookup"><span data-stu-id="dd83f-135">Pre-create OD4B sites for users</span></span>
- <span data-ttu-id="dd83f-136">Примеры и содержимое в http://aka.ms/OfficeDevPnP</span><span class="sxs-lookup"><span data-stu-id="dd83f-136">Samples and content at http://aka.ms/OfficeDevPnP</span></span>

<a name="applies-to"></a><span data-ttu-id="dd83f-137">Применимо к</span><span class="sxs-lookup"><span data-stu-id="dd83f-137">Applies to</span></span>
==========
- <span data-ttu-id="dd83f-138">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="dd83f-138">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="dd83f-139">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="dd83f-139">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="dd83f-140">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="dd83f-140">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="dd83f-141">**Необходимо знать все возможные варианты выбора, можно еще здесь и точных имен для них.**</span><span class="sxs-lookup"><span data-stu-id="dd83f-141">**Need to know all the possible choices we can have here and the exact names for them.**</span></span>

<span data-ttu-id="dd83f-142">*Шаблонов для выделенными и в локальной, совпадают с помощью надстройки SharePoint методики модели, но существуют некоторые отличия на основе возможных технологий, которые можно использовать.*</span><span class="sxs-lookup"><span data-stu-id="dd83f-142">*Patterns for Dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies which can be used.*</span></span>

<span data-ttu-id="dd83f-143">**Существуют ли другие стандартные заметки следующим образом, мы можем использовать через статьи?**</span><span class="sxs-lookup"><span data-stu-id="dd83f-143">**Are there any other standard notes like this we might use across articles?**</span></span>
