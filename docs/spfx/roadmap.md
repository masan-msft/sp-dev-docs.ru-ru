---
title: "План развития SharePoint Framework"
description: "Современные возможности настройки, выпущенные после выхода общедоступной версии."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 8d3f750b278715a49269d5db2a57f6a839d6b2f2
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="caef3-103">План развития SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-103">SharePoint Framework roadmap</span></span>

<span data-ttu-id="caef3-104">Первый выпуск SharePoint Framework поддерживал только клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="caef3-104">The first release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="caef3-105">С того момента мы не прекращаем предоставлять новые современные возможности для настройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="caef3-105">This was, however, just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="caef3-106">Вот список основных возможностей, выпущенных после выхода общедоступной версии:</span><span class="sxs-lookup"><span data-stu-id="caef3-106">Following is a list of key capabilities released after General Availability:</span></span>

- [<span data-ttu-id="caef3-107">Поддержка развертывания на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="caef3-107">Tenant-scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="caef3-108">Поддержка локальной среды для SharePoint 2016 (пакет дополнительных компонентов 2)</span><span class="sxs-lookup"><span data-stu-id="caef3-108">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="caef3-109">Расширения SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-109">SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="caef3-110">Свойства клиента</span><span class="sxs-lookup"><span data-stu-id="caef3-110">Tenant properties</span></span>](./tenant-properties.md)
- [<span data-ttu-id="caef3-111">API управления жизненным циклом приложений для решений и надстроек SPFx</span><span class="sxs-lookup"><span data-stu-id="caef3-111">Application Lifecycle Management (ALM) APIs for SPFx solutions and add-ins</span></span>](../apis/alm-api-for-spfx-add-ins.md)
- [<span data-ttu-id="caef3-112">Поддержка Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="caef3-112">Office UI Fabric Core support</span></span>](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [<span data-ttu-id="caef3-113">Каталог приложений семейства веб-сайтов и упаковка ресурсов</span><span class="sxs-lookup"><span data-stu-id="caef3-113">Asset packaging and site collection app catalog</span></span>](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> <span data-ttu-id="caef3-114">Ниже приведен список задач, над которыми работают инженеры SharePoint.</span><span class="sxs-lookup"><span data-stu-id="caef3-114">This is a list of areas that SharePoint engineering has in the backlog and is looking into.</span></span> <span data-ttu-id="caef3-115">Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).</span><span class="sxs-lookup"><span data-stu-id="caef3-115">This does **NOT** mean that all of them will be delivered, but we are looking into getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="caef3-116">Общие улучшения</span><span class="sxs-lookup"><span data-stu-id="caef3-116">General improvements</span></span>

- <span data-ttu-id="caef3-117">Удобство вызова API Graph для доступа к данным пользователей (GraphHttpClient в предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="caef3-117">Easy access to Graph API to access user specific information (GraphHttpClient in preview)</span></span>
- <span data-ttu-id="caef3-118">Веб-перехватчики уровня сайта</span><span class="sxs-lookup"><span data-stu-id="caef3-118">Site level WebHooks</span></span>
- <span data-ttu-id="caef3-119">Обновленные сведения о хранении при поддержке SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-119">Updated 'store' story with SharePoint Framework support</span></span>
- <span data-ttu-id="caef3-120">Отдел в магазине для решений SharePoint Framework с простым каналом распространения для независимых поставщиков ПО</span><span class="sxs-lookup"><span data-stu-id="caef3-120">'Store' story for SharePoint Framework solutions with easy distribution channel for ISVs</span></span> 

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="caef3-121">Клиентские веб-части++ и надстройки</span><span class="sxs-lookup"><span data-stu-id="caef3-121">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="caef3-122">Поддержка более сложных сценариев и взаимодействий с веб-частями</span><span class="sxs-lookup"><span data-stu-id="caef3-122">Support more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="caef3-123">Обмен данными между веб-частями</span><span class="sxs-lookup"><span data-stu-id="caef3-123">Part-to-part communication</span></span>
    - <span data-ttu-id="caef3-124">Изоляция JavaScript Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-124">JavaScript Framework isolation</span></span>
    - <span data-ttu-id="caef3-125">Модель "разработчик-любитель" для простых задач разработки</span><span class="sxs-lookup"><span data-stu-id="caef3-125">"Citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="caef3-126">Реализация современных технологий оформления веб-частей</span><span class="sxs-lookup"><span data-stu-id="caef3-126">Bring add-ins to the modern world: let’s make them play nicer with the new UX</span></span>
    - <span data-ttu-id="caef3-127">Регистрация в Azure AD</span><span class="sxs-lookup"><span data-stu-id="caef3-127">Azure AD registration</span></span>
    - <span data-ttu-id="caef3-128">Встроенная поддержка адаптивного дизайна</span><span class="sxs-lookup"><span data-stu-id="caef3-128">Native responsive support</span></span>
    - <span data-ttu-id="caef3-129">Создание надстроек с помощью SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-129">Build add-ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="caef3-130">Управление жизненным циклом приложений</span><span class="sxs-lookup"><span data-stu-id="caef3-130">Application Lifecycle Management</span></span>

- <span data-ttu-id="caef3-131">Упрощенная процедура утверждения: больше не нужно знать администратора клиента</span><span class="sxs-lookup"><span data-stu-id="caef3-131">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="caef3-132">Владелец инициирует процедуру утверждения.</span><span class="sxs-lookup"><span data-stu-id="caef3-132">Owner initiates the approval process.</span></span>
    - <span data-ttu-id="caef3-133">Администратор клиента автоматически получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="caef3-133">Tenant admin gets automatically notified.</span></span>
    - <span data-ttu-id="caef3-134">Параметры для управления процедурой утверждения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="caef3-134">Settings to control the default experience around approval process.</span></span>


## <a name="developer-experience"></a><span data-ttu-id="caef3-135">Среда разработки</span><span class="sxs-lookup"><span data-stu-id="caef3-135">Developer experience</span></span>

- <span data-ttu-id="caef3-136">SharePoint Framework Workbench 2.0: разработка расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-136">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="caef3-137">Компоненты цепочки инструментов</span><span class="sxs-lookup"><span data-stu-id="caef3-137">Toolchain components</span></span>
- <span data-ttu-id="caef3-138">Дополнительные шаблоны Yeoman</span><span class="sxs-lookup"><span data-stu-id="caef3-138">Additional Yeoman templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="caef3-139">Возможности, предоставленные ранее</span><span class="sxs-lookup"><span data-stu-id="caef3-139">Already shipped capabilities</span></span>

<span data-ttu-id="caef3-140">В следующих разделах перечислены возможности, предоставленные ранее.</span><span class="sxs-lookup"><span data-stu-id="caef3-140">The following sections list older items that have already shipped.</span></span>

### <a name="asset-packaging"></a><span data-ttu-id="caef3-141">Упаковка ресурсов</span><span class="sxs-lookup"><span data-stu-id="caef3-141">Asset packaging</span></span>

- <span data-ttu-id="caef3-142">Автоматическое размещение кода в CDN.</span><span class="sxs-lookup"><span data-stu-id="caef3-142">Automatic CDN hosting for code.</span></span> <span data-ttu-id="caef3-143">Добавление пакета JavaScript в пакет приложения, который автоматически развертывается в библиотеке, размещаемой в сети CDN Office 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="caef3-143">Package JavaScript bundle into app package, which is automatically deployed to a library that gets hosted on your tenant Office 365 CDN.</span></span>

### <a name="alm-rest-apis"></a><span data-ttu-id="caef3-144">REST API ALM</span><span class="sxs-lookup"><span data-stu-id="caef3-144">ALM REST APIs</span></span>

- <span data-ttu-id="caef3-145">REST API ALM.</span><span class="sxs-lookup"><span data-stu-id="caef3-145">ALM REST APIs.</span></span> <span data-ttu-id="caef3-146">Развертывание, активация, удаление и обновление приложений и надстроек.</span><span class="sxs-lookup"><span data-stu-id="caef3-146">Deploy, activate, delete, and upgrade apps and add-ins.</span></span>
- <span data-ttu-id="caef3-147">REST API ALM, поддерживающие *все* объекты в каталоге приложений, в том числе надстройки.</span><span class="sxs-lookup"><span data-stu-id="caef3-147">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins.</span></span>
- <span data-ttu-id="caef3-148">CSOM и командлеты PowerShell, выпущенные по инициативе сообщества разработчиков ПО с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="caef3-148">CSOM and PowerShell cmdlets released as an open source community initiative.</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="caef3-149">Поддержка внедрения JavaScript (JSLink, дополнительные действия пользователей)</span><span class="sxs-lookup"><span data-stu-id="caef3-149">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="caef3-150">Те же цепочка инструментов и модель развертывания, что и для клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="caef3-150">The same toolchain and deployment model as client-side web parts.</span></span>
- <span data-ttu-id="caef3-151">Наследование от строго типизированного базового класса везде, где это возможно, вместо прямого управления моделью DOM страницы.</span><span class="sxs-lookup"><span data-stu-id="caef3-151">Derive from a strongly typed base class wherever possible, rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="caef3-152">Расширение современного интерфейса с помощью современных компонентов, похожих на дополнительные действия и JSLink в классическом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="caef3-152">Enable modern extension usage with modern experiences similar to Custom Actions and JSLink in classic experience.</span></span>
- <span data-ttu-id="caef3-153">Работа с NoScript через каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="caef3-153">Work with NoScript via tenant App Catalog.</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="caef3-154">Поддержка локальной среды для SharePoint 2016 (пакет дополнительных компонентов 2)</span><span class="sxs-lookup"><span data-stu-id="caef3-154">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="caef3-155">Реализована в пакете дополнительных компонентов 2 для SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="caef3-155">Shipping as part of Feature Pack 2 for SharePoint 2016.</span></span>
- <span data-ttu-id="caef3-156">Те же возможности, что и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="caef3-156">Similar feature capabilities as in SharePoint Online.</span></span>
- <span data-ttu-id="caef3-157">Цель — создать общую платформу разработки для локальной среды и облака.</span><span class="sxs-lookup"><span data-stu-id="caef3-157">Target is to provide common development platform across on-premises and the cloud.</span></span>
- <span data-ttu-id="caef3-158">Использование современной цепочки инструментов и открытого кода в локальных средах.</span><span class="sxs-lookup"><span data-stu-id="caef3-158">Leveraging modern toolchain and open source in on-premises environments.</span></span>
- <span data-ttu-id="caef3-159">Ориентация на версию SharePoint 2016 в 2017 г.</span><span class="sxs-lookup"><span data-stu-id="caef3-159">Targeting SharePoint 2016 version during calendar year 2017.</span></span>


## <a name="see-also"></a><span data-ttu-id="caef3-160">См. также</span><span class="sxs-lookup"><span data-stu-id="caef3-160">See also</span></span>

- [<span data-ttu-id="caef3-161">Блоги на сайте dev.office.com</span><span class="sxs-lookup"><span data-stu-id="caef3-161">dev.office.com blog</span></span>](https://dev.office.com/blogs)
- [<span data-ttu-id="caef3-162">Учетная запись OfficeDev в Твиттере</span><span class="sxs-lookup"><span data-stu-id="caef3-162">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
- [<span data-ttu-id="caef3-163">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="caef3-163">SharePoint Framework Overview</span></span>](sharepoint-framework-overview.md)
