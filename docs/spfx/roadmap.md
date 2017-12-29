---
title: "План развития SharePoint Framework"
ms.date: 12/15/2017
ms.prod: sharepoint
ms.openlocfilehash: fd8577a51c3a16ffec94cca3958c8853a8ea9dcb
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="sharepoint-framework-roadmap"></a><span data-ttu-id="67f21-102">План развития SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="67f21-102">SharePoint Framework roadmap</span></span>

<span data-ttu-id="67f21-103">Первый выпуск SharePoint Framework поддерживал только клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="67f21-103">First release of the SharePoint Framework contained only support for client-side web parts.</span></span> <span data-ttu-id="67f21-104">В дальнейшем современные возможности настройки SharePoint будут расширяться.</span><span class="sxs-lookup"><span data-stu-id="67f21-104">This was however just a start on the journey for providing additional modern customization capabilities to SharePoint.</span></span> <span data-ttu-id="67f21-105">Есть список основных возможностей, выпущенных после выхода общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="67f21-105">Here is a list of key capabilities released after initial General Availability.</span></span>

- [<span data-ttu-id="67f21-106">Поддержка развертывания на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="67f21-106">Tenant scoped deployment support</span></span>](./tenant-scoped-deployment.md)
- [<span data-ttu-id="67f21-107">Поддержка локальной среды для SharePoint 2016 (пакет дополнительных компонентов 2)</span><span class="sxs-lookup"><span data-stu-id="67f21-107">On-premises support for SharePoint 2016 (Feature Pack 2)</span></span>](./sharepoint-2016-support.md)
- [<span data-ttu-id="67f21-108">Расширения SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="67f21-108">SharePoint Framework Extensions</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="67f21-109">Свойства клиента</span><span class="sxs-lookup"><span data-stu-id="67f21-109">Tenant properties</span></span>](./tenant-properties.md)
- [<span data-ttu-id="67f21-110">API ALM для решений и надстроек SPFx</span><span class="sxs-lookup"><span data-stu-id="67f21-110">ALM APIs for SPFx solutions and add-ins</span></span>](../apis/alm-api-for-spfx-add-ins.md)
- [<span data-ttu-id="67f21-111">Поддержка Office UI Fabric Core</span><span class="sxs-lookup"><span data-stu-id="67f21-111">Office UI Fabric Core support</span></span>](https://dev.office.com/blogs/improved-support-for-office-ui-fabric-core)
- [<span data-ttu-id="67f21-112">Каталог приложений семейства веб-сайтов и упаковка ресурсов</span><span class="sxs-lookup"><span data-stu-id="67f21-112">Asset packaging and site collection app catalog</span></span>](../general-development/site-collection-app-catalog.md)


> [!NOTE]
> <span data-ttu-id="67f21-113">Это список задач, над которыми работают инженеры SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67f21-113">This is a list of areas which SharePoint engineering is having in the backlog and are looking into.</span></span> <span data-ttu-id="67f21-114">Элементы и разделы из этого списка будут постепенно находить воплощение в будущих выпусках SharePoint Framework (**необязательно** все идеи будут реализованы).</span><span class="sxs-lookup"><span data-stu-id="67f21-114">This does **NOT** mean that all of them will be necessarily delivered, but we are looking for getting items and topics from this list gradually released with the future releases of SharePoint Framework.</span></span>

## <a name="general-improvements"></a><span data-ttu-id="67f21-115">Общие улучшения</span><span class="sxs-lookup"><span data-stu-id="67f21-115">General improvements</span></span>

- <span data-ttu-id="67f21-116">Удобство вызова API Graph для доступа к данным пользователей (GraphHttpClient в предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="67f21-116">Easy access to Graph API to access user specific information (GraphHttpClient in preview)</span></span>
- <span data-ttu-id="67f21-117">Веб-перехватчики уровня сайта.</span><span class="sxs-lookup"><span data-stu-id="67f21-117">Site level WebHooks</span></span>

## <a name="client-side-web-parts-and-add-ins"></a><span data-ttu-id="67f21-118">Клиентские веб-части++ и надстройки</span><span class="sxs-lookup"><span data-stu-id="67f21-118">Client-side web parts++ and add-ins</span></span>

- <span data-ttu-id="67f21-119">Поддержка более сложных сценариев и взаимодействий с веб-частями.</span><span class="sxs-lookup"><span data-stu-id="67f21-119">Supporting more complex scenarios and interactions with web parts</span></span>
    - <span data-ttu-id="67f21-120">Обмен данными между веб-частями.</span><span class="sxs-lookup"><span data-stu-id="67f21-120">Part-to-part communication</span></span>
    - <span data-ttu-id="67f21-121">Изоляция платформы JS.</span><span class="sxs-lookup"><span data-stu-id="67f21-121">JS Framework isolation</span></span>
    - <span data-ttu-id="67f21-122">Модель "разработчик-любитель" для простых задач разработки.</span><span class="sxs-lookup"><span data-stu-id="67f21-122">"citizen developer" model for lightweight development</span></span>

- <span data-ttu-id="67f21-123">Реализация современных технологий оформления веб-частей.</span><span class="sxs-lookup"><span data-stu-id="67f21-123">Bring add-ins to the modern world: Let’s make them play nicer with the new UX.</span></span> 
    - <span data-ttu-id="67f21-124">Регистрация в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="67f21-124">Azure AD Registration</span></span>
    - <span data-ttu-id="67f21-125">Встроенная поддержка адаптивного дизайна.</span><span class="sxs-lookup"><span data-stu-id="67f21-125">Native responsive support</span></span>
    - <span data-ttu-id="67f21-126">Создание надстроек с помощью SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="67f21-126">Build Add-Ins with SharePoint Framework</span></span>


## <a name="application-lifecycle-management"></a><span data-ttu-id="67f21-127">Управление жизненным циклом приложений</span><span class="sxs-lookup"><span data-stu-id="67f21-127">Application Lifecycle Management</span></span>

- <span data-ttu-id="67f21-128">Упрощенная процедура утверждения: больше не нужно знать администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="67f21-128">Streamlined approval experience: no need to know who your tenant admin is anymore</span></span>
    - <span data-ttu-id="67f21-129">Владелец инициирует процедуру утверждения.</span><span class="sxs-lookup"><span data-stu-id="67f21-129">Owner initiate the approval process</span></span>
    - <span data-ttu-id="67f21-130">Администратор клиента автоматически получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="67f21-130">Tenant admin gets automatically notified</span></span> 
    - <span data-ttu-id="67f21-131">Параметры для управления процедурой утверждения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="67f21-131">Settings to control the default experience around approval process</span></span>


## <a name="developer-experience"></a><span data-ttu-id="67f21-132">Удобство для разработчиков</span><span class="sxs-lookup"><span data-stu-id="67f21-132">Developer Experience</span></span>
- <span data-ttu-id="67f21-133">SharePoint Framework Workbench 2.0: сведения о развертывании касательно расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="67f21-133">SharePoint Framework Workbench 2.0: Development story for SharePoint Framework Extensions</span></span>
- <span data-ttu-id="67f21-134">Компоненты цепочки инструментов.</span><span class="sxs-lookup"><span data-stu-id="67f21-134">Tool Chain Components</span></span>
- <span data-ttu-id="67f21-135">Дополнительные шаблоны Yeoman.</span><span class="sxs-lookup"><span data-stu-id="67f21-135">Additional Yeoman Templates</span></span>

## <a name="already-shipped-capabilities"></a><span data-ttu-id="67f21-136">Возможности, которые уже обеспечены</span><span class="sxs-lookup"><span data-stu-id="67f21-136">Already shipped capabilities</span></span>

<span data-ttu-id="67f21-137">Ниже перечислены возможности, которые уже реализованы.</span><span class="sxs-lookup"><span data-stu-id="67f21-137">Following chapters are listing older items in the roadmap page, which have been already shipped.</span></span>

### <a name="asset-packaging"></a><span data-ttu-id="67f21-138">Упаковка ресурсов</span><span class="sxs-lookup"><span data-stu-id="67f21-138">Asset packaging</span></span>

- <span data-ttu-id="67f21-139">Автоматическое размещение кода в CDN. Добавление пакета JavaScript в пакет приложения, который затем автоматически развертывается в библиотеке, размещаемой в сети CDN Office 365 клиента.</span><span class="sxs-lookup"><span data-stu-id="67f21-139">Package JavaScript bundle into app package, which is automatically then deployed to a library that gets hosted on your tenant Office 365 CDN</span></span>

### <a name="alm-rest-apis"></a><span data-ttu-id="67f21-140">REST API ALM</span><span class="sxs-lookup"><span data-stu-id="67f21-140">ALM REST APIs</span></span>

- <span data-ttu-id="67f21-141">REST API ALM — развертывание, активация, удаление и обновление приложений и надстроек.</span><span class="sxs-lookup"><span data-stu-id="67f21-141">ALM REST APIs - Deploy, activate, delete and upgrade apps and add-ins</span></span>
- <span data-ttu-id="67f21-142">REST API ALM, поддерживающие *все* объекты в каталоге приложений, в том числе надстройки.</span><span class="sxs-lookup"><span data-stu-id="67f21-142">ALM REST APIs targeted to support *everything* in the App Catalog, including add-ins</span></span>
- <span data-ttu-id="67f21-143">CSOM и командлеты PowerShell, выпущенные по инициативе сообщества разработчиков ПО с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="67f21-143">CSOM and PowerShell cmdlets released as an open source community initiative</span></span>

### <a name="javascript-embedding-support-jslink-user-custom-actions"></a><span data-ttu-id="67f21-144">Поддержка внедрения JavaScript (JSLink, дополнительные действия пользователей)</span><span class="sxs-lookup"><span data-stu-id="67f21-144">JavaScript embedding support (JSLink, User Custom Actions)</span></span> 

- <span data-ttu-id="67f21-145">Те же цепочка инструментов и модель развертывания, что и для клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="67f21-145">The same tool chain and deployment model as client-side web parts</span></span>
- <span data-ttu-id="67f21-146">Наследование от строго типизированного базового класса везде, где это возможно, вместо прямого управления моделью DOM страницы.</span><span class="sxs-lookup"><span data-stu-id="67f21-146">Derive from a strongly typed base class wherever possible rather than manipulating the page DOM directly.</span></span>
- <span data-ttu-id="67f21-147">Обеспечение использования современных расширений и возможностей, подобных дополнительным действиям и JSLink, в случае классического варианта.</span><span class="sxs-lookup"><span data-stu-id="67f21-147">Enable modern extension usage with modern experiences similar as Custom Actions and JS Link in classic experience</span></span>
- <span data-ttu-id="67f21-148">Работа с NoScript через каталог приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="67f21-148">Work with NoScript via tenant app catalog</span></span>

### <a name="on-premises-support---sharepoint-2016-feature-pack-2"></a><span data-ttu-id="67f21-149">SharePoint 2016 с пакетом дополнительных компонентов 2: поддержка локальной среды</span><span class="sxs-lookup"><span data-stu-id="67f21-149">On-premises support - Sharepoint 2016 Feature Pack 2</span></span>

- <span data-ttu-id="67f21-150">Предоставление в составе пакета дополнительных компонентов 2 для SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="67f21-150">Shipping as part of Feature Pack 2 for SharePoint 2016</span></span>
- <span data-ttu-id="67f21-151">Те же возможности, что и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="67f21-151">Similar feature capabilities as in SharePoint Online</span></span>
- <span data-ttu-id="67f21-152">Предоставление общей платформы разработки в локальной среде и облаке.</span><span class="sxs-lookup"><span data-stu-id="67f21-152">Target is to provide common development platform across on-premises and the cloud</span></span>
- <span data-ttu-id="67f21-153">Использование современной цепочки инструментов и открытого кода в локальных средах.</span><span class="sxs-lookup"><span data-stu-id="67f21-153">Leveraging modern toolchain and open source on on-premises environments</span></span>
- <span data-ttu-id="67f21-154">Ориентация на версию SharePoint 2016 в 2017 г.</span><span class="sxs-lookup"><span data-stu-id="67f21-154">Targeting SharePoint 2016 version during calendar year 2017</span></span>


## <a name="see-also"></a><span data-ttu-id="67f21-155">См. также</span><span class="sxs-lookup"><span data-stu-id="67f21-155">See also</span></span>
<span data-ttu-id="67f21-156">Узнавайте о новых выпусках и возможностях SharePoint Framework из следующих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="67f21-156">Please use following resources to stay up to date on the new releases and capabilities being released for SharePoint Framework.</span></span>

* [<span data-ttu-id="67f21-157">dev.office.com blog</span><span class="sxs-lookup"><span data-stu-id="67f21-157">dev.office.com blog</span></span>](https://dev.office.com/blogs)
* [<span data-ttu-id="67f21-158">Учетная запись OfficeDev в Твиттере</span><span class="sxs-lookup"><span data-stu-id="67f21-158">OfficeDev Twitter account</span></span>](https://twitter.com/officedev)
