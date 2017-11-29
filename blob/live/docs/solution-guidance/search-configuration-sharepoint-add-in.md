---
title: "Настройка поиска в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 9a84ae5aa1a12322227c9182c9ff0f5fb1798e48
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="search-configuration-in-the-sharepoint-add-in-model"></a><span data-ttu-id="437d0-102">Настройка поиска в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="437d0-102">Search configuration in the SharePoint add-in model</span></span>
===================================================

<a name="summary"></a><span data-ttu-id="437d0-103">Summary</span><span class="sxs-lookup"><span data-stu-id="437d0-103">Summary</span></span>
-------

<span data-ttu-id="437d0-104">Выбор подхода для настройки системы поиска отличается новой модели надстройки SharePoint от был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="437d0-104">The approach you take to configure search is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="437d0-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, объектной модели SharePoint на сервере было используется для настройки поиска и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="437d0-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the SharePoint Server-side Object Model was used to configure search, and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="437d0-106">В SharePoint надстройки модели сценарии используйте объектную модель SharePoint на стороне клиента (CSOM) или интерфейса API REST для настройки системы поиска.</span><span class="sxs-lookup"><span data-stu-id="437d0-106">In an SharePoint Add-in model scenario, you use the SharePoint Client-side Object Model (CSOM) or REST API to configure search.</span></span> <span data-ttu-id="437d0-107">Этот шаблон обычно называемую *удаленного подготовки шаблон*.</span><span class="sxs-lookup"><span data-stu-id="437d0-107">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="437d0-108">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="437d0-108">High-level guidelines</span></span>
---------------------

<span data-ttu-id="437d0-109">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для настройки системы поиска в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="437d0-109">As a rule of a thumb, we would like to provide the following high-level guidelines to configure search in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="437d0-110">Используйте SharePoint со стороны клиента API объектной модели (CSOM) для настройки поиска по возможности, Импорт и экспорт параметров конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="437d0-110">Use the SharePoint Client-side Object Model (CSOM) API to configure search whenever possible by importing and exporting search configuration settings.</span></span>
- <span data-ttu-id="437d0-111">Не все параметры конфигурации поиска в настоящее время доступны через SharePoint CSOM API.</span><span class="sxs-lookup"><span data-stu-id="437d0-111">Not all search configuration settings are currently available via the SharePoint CSOM API.</span></span>
    + <span data-ttu-id="437d0-112">В разделе [экспорта и импорта параметров конфигурации настраиваемого поиска в SharePoint Server 2013 (статья TechNet)](https://technet.microsoft.com/en-us/library/jj871675.aspx#BKMK_2) для списка параметров поиска, которые можно экспортировать и импортировать.</span><span class="sxs-lookup"><span data-stu-id="437d0-112">See the [Export and import customized search configuration settings in SharePoint Server 2013 (TechNet Article)](https://technet.microsoft.com/en-us/library/jj871675.aspx#BKMK_2) for a list of search configuration settings that can be exported and imported.</span></span>
    + <span data-ttu-id="437d0-113">Если параметр конфигурации поиска не может быть установлено с помощью CSOM пользовательский интерфейс администрирования требуется для установки значений конфигурации.</span><span class="sxs-lookup"><span data-stu-id="437d0-113">If a search configuration setting is not able to be set using the CSOM then the Administration user interface is required to set configuration values.</span></span>
- <span data-ttu-id="437d0-114">API-Интерфейс REST SharePoint не может (в настоящее время) Импорт или экспорт параметров конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="437d0-114">The SharePoint REST API is not capable (at this time) of importing or exporting search configuration settings.</span></span>

<span data-ttu-id="437d0-115">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="437d0-115">**Getting started**</span></span>

<span data-ttu-id="437d0-116">Следующий пример демонстрирует Импорт и экспорт параметров поиска между клиентами, семейств веб-сайтов и сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="437d0-116">The following sample demonstrates how to import and export search settings between SharePoint tenants, site collections and sites.</span></span>

- [<span data-ttu-id="437d0-117">Core.SearchSettingsPortability (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="437d0-117">Core.SearchSettingsPortability (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)

<a name="related-links"></a><span data-ttu-id="437d0-118">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="437d0-118">Related links</span></span>
=============

- <span data-ttu-id="437d0-119">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="437d0-119">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="437d0-120">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="437d0-120">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="437d0-121">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="437d0-121">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="437d0-122">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="437d0-122">Related PnP samples</span></span>
===================

- [<span data-ttu-id="437d0-123">Core.SearchSettingsPortability (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="437d0-123">Core.SearchSettingsPortability (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)
- <span data-ttu-id="437d0-124">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="437d0-124">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="437d0-125">Применимо к</span><span class="sxs-lookup"><span data-stu-id="437d0-125">Applies to</span></span>
==========
- <span data-ttu-id="437d0-126">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="437d0-126">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="437d0-127">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="437d0-127">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="437d0-128">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="437d0-128">SharePoint 2013 on-premises</span></span>
