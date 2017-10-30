---
title: "Управление жизненным циклом приложений SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a
ms.openlocfilehash: a969bc3ae2e64de2214e8e85443ddc3164c10341
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-application-lifecycle-management"></a><span data-ttu-id="3d850-102">Управление жизненным циклом приложений SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-102">SharePoint Application Lifecycle Management</span></span>
<span data-ttu-id="3d850-103">Применяет основные понятия управления Жизненным циклом приложения и рекомендации для разработки приложений с помощью технологий SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-103">Applies common application lifecycle management (ALM) concepts and practices to application development using SharePoint technologies.</span></span>

<span data-ttu-id="3d850-104">**Автор:** Эрик Чарран, корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3d850-104">**Provided by:** Eric Charran, Microsoft Corporation</span></span>

<span data-ttu-id="3d850-105">**Участники:** (VESA juvonen), корпорация Майкрософт | Стив пешка, корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3d850-105">**Contributors:** Vesa Juvonen, Microsoft Corporation | Steve Peschka, Microsoft Corporation</span></span>

> <span data-ttu-id="3d850-106">**Важные:** В этом разделе имеются ссылки на автоматическое размещение надстройки SharePoint. Программа предварительного просмотра для приложения с автоматическим размещением его завершения.</span><span class="sxs-lookup"><span data-stu-id="3d850-106">**Important:** This topic refers to autohosted SharePoint Add-ins. The preview program for autohosted apps has ended.</span></span> <span data-ttu-id="3d850-107">Можно игнорировать все упоминания автоматически размещаемых надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-107">Please disregard all references to autohosted SharePoint Add-ins.</span></span> 


## <a name="overview-of-application-lifecycle-management-alm"></a><span data-ttu-id="3d850-108">Обзор управления жизненным циклом приложения</span><span class="sxs-lookup"><span data-stu-id="3d850-108">Overview of application lifecycle management (ALM)</span></span>
<span data-ttu-id="3d850-109"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-109"></span></span>

<span data-ttu-id="3d850-110">Microsoft SharePoint предоставляет разработчикам ряд параметров для создания и развертывания приложений, основанных на основе технологий SharePoint, в локальной и размещенной или общедоступных облачных платформ.</span><span class="sxs-lookup"><span data-stu-id="3d850-110">Microsoft SharePoint gives developers several options for creating and deploying applications that are based on SharePoint technologies, for both on-premises and in hosted or public cloud platforms.</span></span> <span data-ttu-id="3d850-111">SharePoint предоставляет повышенной гибкостью в фигуре приложений может занять а также новые возможности с помощью технологий, основанный на стандартах с приложениями.</span><span class="sxs-lookup"><span data-stu-id="3d850-111">SharePoint offers increased flexibility in the shape applications can take as well as new options for using standards-based technologies with applications.</span></span> <span data-ttu-id="3d850-112">Хотя эти возможности приложений и варианты развертывания для получения нового inSharePoint модели приложения предоставляют эффективные средства для разработчиков для создания новых и иммерсивном приложений разработчики должны иметь возможность infuse качества, тестирования и управления жизненным циклом Приложений сведения о выполнении в процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="3d850-112">Although these application capabilities and deployment options afforded by the new application model inSharePoint provide an effective means for developers to create new and immersive applications, developers must be able to infuse quality, testing and ALM considerations into the development process.</span></span> <span data-ttu-id="3d850-113">Эта статья относится основные понятия управления жизненным циклом Приложений и рекомендации для разработки приложений с помощью технологий SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-113">This article applies common ALM concepts and practices to application development using SharePoint technologies.</span></span>

### <a name="whats-new"></a><span data-ttu-id="3d850-114">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="3d850-114">What's new</span></span>
<span data-ttu-id="3d850-115"><a name="WhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-115"></span></span>

<span data-ttu-id="3d850-116">SharePoint устанавливает новая концепция для реализации приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-116">SharePoint establishes a new paradigm for implementing applications.</span></span> <span data-ttu-id="3d850-117">Из-за этот shift при разработке приложений с помощью SharePoint технологий, разработчики и архитекторы должна быть исчерпывающие сведения о новых шаблонов разработки приложений, рекомендации и модели развертывания для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-117">Because of this shift in application development with SharePoint technologies, developers and architects should have a thorough understanding of the new application development patterns, practices, and deployment models for SharePoint.</span></span> <span data-ttu-id="3d850-118">Важно Обратите внимание, что хотя модели приложения для разработки решений с использованием SharePoint была изменена, многие шаблоны, используемые для разработки решения, включая выбор технологий, способы реализации объектов на одной линии существующей web технологии разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-118">It's important to note that while the application model for developing solutions with SharePoint has changed, many of the patterns used for solution development including choice of technologies, implementation techniques are in line with existing web application development technologies.</span></span>
  
    
    
<span data-ttu-id="3d850-119">Следующие ресурсы в структуре типов приложений, которые могут быть созданы с помощью технологий SharePoint и содержат сведения о выполнении для в локальной и облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-119">The following resources outline the application types that can be constructed using SharePoint technologies and contain considerations for both on-premises and cloud applications.</span></span> <span data-ttu-id="3d850-120">Изучить варианты размещения SharePoint Add-ins, видеть [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-120">To understand hosting options for SharePoint Add-ins, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="3d850-121">Кроме того Корпорация Майкрософт рекомендует клиентам для оценки технологии, используемые при разработке приложений с помощью SharePoint, как это делается расширенный набор вариантов для реализации решения.</span><span class="sxs-lookup"><span data-stu-id="3d850-121">Additionally, Microsoft advises customers to evaluate the technologies used when developing applications with SharePoint as there is a wider set of choices for solution implementation.</span></span> <span data-ttu-id="3d850-122">При создании приложений клиентам сосредоточиться на использование основанный на стандартах технологий, таких как HTML5 и JavaScript для представления и пользователь взаимодействия уровней, пока OData и OAuth можно использовать для доступа на основе службы резервного включая служб SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-122">When creating applications, customers can focus on leveraging standards-based technologies such as HTML5 and JavaScript for presentation and user experience layers, while OData and OAuth can be leveraged for service-based access to back end services including SharePoint.</span></span> <span data-ttu-id="3d850-123">Пользователям следует тщательно, требуются ли кода полного доверия (то есть, скомпилированной сборки, развернутые в SharePoint).</span><span class="sxs-lookup"><span data-stu-id="3d850-123">Customers should consider carefully whether full trust code (that is, compiled assemblies deployed to SharePoint) are required.</span></span> <span data-ttu-id="3d850-124">Несмотря на то, что продолжая применять эту концепцию разработки, а по-прежнему действительный и обязательный в некоторых случаях, накладывают значительной нагрузки на процесс управления жизненным циклом Приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-124">although continuing to use that development paradigm, while still valid and required in some situations, does impose significant overhead on the ALM process.</span></span>
  
    
    
<span data-ttu-id="3d850-125">Дополнительные сведения о новых технологий гибкой разработки для приложений SharePoint видеть [Обзор для разработчиков SharePoint](sharepoint-development-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d850-125">For more information about the new flexible development technologies for applications on SharePoint, see  [SharePoint development overview](sharepoint-development-overview.md).</span></span>
  
    
    

### <a name="benefits-and-changes"></a><span data-ttu-id="3d850-126">Преимущества и изменения</span><span class="sxs-lookup"><span data-stu-id="3d850-126">Benefits and changes</span></span>
<span data-ttu-id="3d850-127"><a name="Benefits"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-127"></span></span>

<span data-ttu-id="3d850-128">Так как в настоящее время технологии разработки приложений SharePoint поддерживается более гибкий набор языков и программной архитектуры, разработчики должны адаптировать существующий управления жизненным циклом Приложений рекомендации по методы массовой разработки для размещения для их присутствие в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-128">Because SharePoint-supported application development technologies now offer a more flexible assortment of languages and programming architectures, developers need to adapt existing ALM practices around mainstream development techniques to accommodate for their presence within SharePoint.</span></span> <span data-ttu-id="3d850-129">Основные понятия, такие как тестирование, создание при установке, развертывании и контроля качества, может быть развернута для включения развертывания для SharePoint как приложение SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-129">Concepts such as testing, build establishment, deployment, and quality control, can be expanded to include deployment to SharePoint as a SharePoint application.</span></span> <span data-ttu-id="3d850-130">Это может свидетельствовать о несмотря на то, что многие разработчики, которые привык к записи и развертывания на сервере фермы решений, расширения возможностей ядра SharePoint, распространенные управления жизненным циклом Приложений рекомендациям для новой модели гибкой разработки, упростить с помощью SharePoint приложения должны применяться к процесс реализации.</span><span class="sxs-lookup"><span data-stu-id="3d850-130">This may mean that although many developers that are accustomed to writing and deploying server-side farm solutions that extend the core capabilities of SharePoint, common ALM practices for the new flexible development model facilitated by SharePoint applications must be applied to the implementation process.</span></span>
  
    
    
<span data-ttu-id="3d850-131">Как клиенты продолжить переход к реализации SharePoint с размещением в облаке, разработчикам понадобится понять, как расширить понятия управления жизненным циклом Приложений, которые необходимо включить разработки, тестирования и развертывания целевых средах, расположенные вне физических организация.</span><span class="sxs-lookup"><span data-stu-id="3d850-131">As customers continue the transition to cloud-hosted implementations of SharePoint, developers will need to understand how to extend ALM concepts to include development, testing, and deployment target environments that sit outside the physical boundaries of the organization.</span></span> <span data-ttu-id="3d850-132">Этот компонент включает оценку стратегической технологии для проведения разработки приложений, тестирования и развертывания.</span><span class="sxs-lookup"><span data-stu-id="3d850-132">This includes evaluating the technology strategy for conducting application development, testing, and deployment.</span></span>
  
    
    
<span data-ttu-id="3d850-133">Разработчики и архитекторы одинаково может стать хорошо versed в создав решений, которые состоят из нескольких компонентов приложения, которые охватывают или сочетание разных типов варианта размещения.</span><span class="sxs-lookup"><span data-stu-id="3d850-133">Developers and architects alike can become well-versed in synthesizing solutions that consist of multiple application components that span or combine different types of hosting options.</span></span> <span data-ttu-id="3d850-134">Во время этого процесса адаптации процедуры управления жизненным циклом Приложений должны применяться одностороннем этих приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-134">During this adaptation process, ALM procedures should be applied unilaterally to these applications.</span></span> <span data-ttu-id="3d850-135">Например, разработчикам может потребоваться развернуть приложение, которая распределена среди локального развертывания служб (то есть, IIS, ASP.NET, MVC, WebAPI и WCF), Microsoft Azure, SharePoint и SQL Azure, а также возможность тестирования компоненты приложения, чтобы определить качество или ли были представлены все регрессии после предыдущего построения.</span><span class="sxs-lookup"><span data-stu-id="3d850-135">For example, developers may need to deploy an application that spans on-premises services deployment (that is, IIS, ASP.NET, MVC, WebAPI, and WCF), Microsoft Azure, SharePoint, and SQL Azure, while also being able to test the application components to determine quality or whether any regressions have been introduced since a previous build.</span></span> <span data-ttu-id="3d850-136">Эти требования могут относиться значительные shift в том, как разработчики и рабочих групп рассматривать ежедневного процесс построения и развертывания, который хорошо известных процедуры для локальной или решения на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="3d850-136">These requirements may signify a significant shift in how developers and teams regard the daily build and deployment process that is a well-known procedure for on-premises or server-side solutions.</span></span>
  
    
    

### <a name="development-team-considerations"></a><span data-ttu-id="3d850-137">Аспекты рабочих групп разработки</span><span class="sxs-lookup"><span data-stu-id="3d850-137">Development team considerations</span></span>
<span data-ttu-id="3d850-138"><a name="DevTeam"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-138"></span></span>

<span data-ttu-id="3d850-139">Для организаций, имеющих несколько разработчиков приложений или архитектор коллективной разработки для SharePoint следует тщательно планировать для предоставления приложений высокого качества, а также поддерживает достаточно производительность разработчика.</span><span class="sxs-lookup"><span data-stu-id="3d850-139">For organizations that have more than one application developer or architect, team development for SharePoint should be carefully planned to provide the highest-quality applications as well as support sufficient developer productivity.</span></span> <span data-ttu-id="3d850-140">Поскольку метод для проведения разработки приложений увеличено гибкостью, группы должны быть открытым и уверенно не только для управления жизненным циклом Приложений и рекомендации и шаблоны, а также каждый разработчик будет создавать код и убедитесь, качество кода становится частью процесс построения приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-140">Because the method for conducting application development has increased in flexibility, teams will need to be clear and confident not only on ALM practices and patterns, but also on how each developer will write code and ensure that quality code becomes part of the application build process.</span></span>
  
    
    
<span data-ttu-id="3d850-p110">Для этого сначала необходимо выбрать надлежащую среду разработки. Традиционно разработка выполнялась раздельно на виртуальных машинах, подключенных к общему хранилищу кода, который предоставлял возможности сборки, развертывания и тестирования, например Visual Studio TFS 2012. TFS по-прежнему остается мощным инструментальным компонентом стратегии управления жизненным циклом приложения, имеющим центральное значение в процессе разработки, но рабочим группам следует рассмотреть возможности использования TFS в различных типах сред разработки.</span><span class="sxs-lookup"><span data-stu-id="3d850-p110">These considerations begin with selecting the appropriate development environment. Traditionally, development has been relegated to conducting separate development in virtual machines that are connected to a common code repository that provided build, deployment, and testing capabilities, like Visual Studio TFS 2012. TFS is still a strong instrumental component of an ALM strategy, and central to the development effort, but teams should consider how to leverage TFS across the different types of development environment options.</span></span>
  
    
    
<span data-ttu-id="3d850-p111">В зависимости от целевой среды и типа решения (то есть, какие компоненты должны быть размещены локально, а какие  в облачной инфраструктуре или службах), сейчас разработчики могут выбирать различные комбинации новых сред разработки. Такие варианты будут состоять из новых предложений, таких как шаблон сайта разработчика SharePoint, клиент разработчика Office 365, а также традиционные варианты, такие как разработка на основе виртуальных машин с использованием Hyper-V в Windows 8 или Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="3d850-p111">Depending on the target environment, the solution type (that is, which components will be on-premises and which will be hosted in cloud infrastructure or services), developers can now select from a combination of new development environment options. These options will consist of new choices such as the SharePoint developer site template, an Office 365 developer tenant, as well as legacy choices such as virtual machine-based development using Hyper-V in Windows 8 or Windows Server 2012.</span></span>
  
    
    
<span data-ttu-id="3d850-146">В следующем разделе описаны вопросы среды разработки для разработчиков приложений и рабочих групп разработки.</span><span class="sxs-lookup"><span data-stu-id="3d850-146">The following section describes development environment considerations for application developers and development teams.</span></span>
  
    
    

## <a name="development-environment-considerations"></a><span data-ttu-id="3d850-147">Аспекты среды разработки</span><span class="sxs-lookup"><span data-stu-id="3d850-147">Development environment considerations</span></span>
<span data-ttu-id="3d850-148"><a name="DevEnvironment"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-148"></span></span>

<span data-ttu-id="3d850-p112">Выбирать среду разработки следует на основе многих факторов. Выбор будет значительно зависеть от типа разрабатываемого приложения, а также целевой платформы для приложения. Традиционно при разработке приложений для SharePoint Server 2010 разработчики настраивали виртуальные машины и проводили разработку изолированно. Это было связано с тем, что разработка решений с полным доверием могла требовать перезапуска базовых зависимостей SharePoint, таких как IIS, что не позволило бы многим разработчикам использовать одну среду SharePoint. Так как технологии разработки изменились и перед разработчиками открылось больше возможностей для создания приложений, разработчики и рабочие группы должны понимать, какие варианты сред разработки им доступны. На рисунке 1 показана среда разработки и набор различных средств, а также указаны типы решений, которые можно развернуть в целевых средах.</span><span class="sxs-lookup"><span data-stu-id="3d850-p112">The selection of a development environment should be made based on multiple factors. These considerations are largely influenced by the type of application being developed as well as the target platform for the application. Traditionally, when creating applications for SharePoint Server 2010, developers would provision virtual machines and conduct development in isolation. This was due to the fact that deployment of full trust solutions may have required restarts of core SharePoint dependencies, such as IIS, which would prevent multiple developers from using a single SharePoint environment. Because development technologies have changed and the options for developers creating applications have increased, developers and teams should understand the choice of development environments available to them. Figure 1 shows the development environment and tool mix, and includes the types of solutions that can be deployed to the target environments.</span></span>
  
    
    

<span data-ttu-id="3d850-155">**Рисунок 1. Компоненты и средства среды разработки**</span><span class="sxs-lookup"><span data-stu-id="3d850-155">**Figure 1. Development environment components and tools**</span></span>


    
 <span data-ttu-id="3d850-156">[</span><span class="sxs-lookup"><span data-stu-id="3d850-156"></span></span>![Среда разработки приложений может включать Office 365, Visual Studio и виртуальные машины.](../images/AppDevelopmentEnvironment.png)
  
    
    

### <a name="development-environment-philosophy"></a><span data-ttu-id="3d850-158">Философия среды разработки</span><span class="sxs-lookup"><span data-stu-id="3d850-158">Development environment philosophy</span></span>
<span data-ttu-id="3d850-159"><a name="DevPhilosophy"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-159"></span></span>

<span data-ttu-id="3d850-160">Из-за инвестиции в как приложения может быть создан и создана с использованием SharePoint разработчикам необходимо определить, есть ли необходимость проведения разработки с помощью серверного кода.</span><span class="sxs-lookup"><span data-stu-id="3d850-160">Because of the investments made in how applications can be designed and implemented using SharePoint, developers should determine if there is a need to conduct development using server-side code.</span></span> <span data-ttu-id="3d850-161">Поскольку разработчики создают приложения, использующие модель размещаемых в облаке, снижает требования для проведения разработки, которая использует виртуализованных средах специально для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-161">As developers create applications that use the cloud-hosted model, the requirement to conduct development that relies on virtualized environments, specifically for SharePoint, diminishes.</span></span> <span data-ttu-id="3d850-162">Разработчики должны поиска для построения решений с помощью модели разработки удаленного, использующего существующей облачной инфраструктуры (открытых и закрытых).</span><span class="sxs-lookup"><span data-stu-id="3d850-162">Developers should seek to build solutions with the remote-development model that uses existing cloud-based (both public and private) infrastructure.</span></span> <span data-ttu-id="3d850-163">При сред разработки можно быстро и легко подготовить к работе с без необходимости создавать и настраивать виртуализации, разработчики могут инвестировать больше времени в сосредоточиться на производительность разработки и контроля качества, а не в инфраструктуре управления.</span><span class="sxs-lookup"><span data-stu-id="3d850-163">If development environments can be quickly and easily provisioned without having to create and orchestrate virtualization, developers can invest more time in focusing on development productivity and quality, rather than infrastructure management.</span></span>
  
    
    
<span data-ttu-id="3d850-164">Решение о требуют виртуализованной экземпляра SharePoint и новый шаблон сайта разработки SharePoint будут зависеть от того, является ли приложение требует полного доверия код развертываются в SharePoint и работы с ней.</span><span class="sxs-lookup"><span data-stu-id="3d850-164">The decision to require a virtualized instance of SharePoint versus the new SharePoint development site template will depend on whether or not the application requires full trust code to be deployed to SharePoint and run there.</span></span> <span data-ttu-id="3d850-165">При необходимости код не полного доверия, рекомендуется использовать шаблон сайта для разработчиков, которые можно найти в клиентов разработки Office 365 или в пределах организации реализации локального развертывания SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-165">If no full trust code is required, we recommend using the developer site template, which can be found in Office 365 development tenants or within an organization's implementation of on-premises SharePoint.</span></span> <span data-ttu-id="3d850-166">Шаблоны сайтов разработчика предназначены для разработчиков для развертывания приложений непосредственно в SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d850-166">Developer site templates are designed for developers to deploy applications directly to SharePoint from Visual Studio.</span></span> <span data-ttu-id="3d850-167">Сайты для разработчиков Office 365 предварительно настроенного для изоляции приложений и OAuth, так, чтобы разработчики могут записи и тестирования приложений прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="3d850-167">Office 365 developer sites are preconfigured for application isolation and OAuth so that developers can begin writing and testing applications right away.</span></span>
  
    
    
<span data-ttu-id="3d850-168">В следующих разделах подробно описано, когда разработчики могут использовать различные варианты сред для создания приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-168">The following sections describe in detail when developers can use the different environment options to build applications.</span></span>
  
    
    

### <a name="o365-development-sites-public-cloud"></a><span data-ttu-id="3d850-169">Сайты разработки O365 (общедоступное облако)</span><span class="sxs-lookup"><span data-stu-id="3d850-169">O365 development sites (public cloud)</span></span>
<span data-ttu-id="3d850-170"><a name="O365Development"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-170"></span></span>

<span data-ttu-id="3d850-171">На рисунке 2 показано, как разработчики могут использовать Office 365 в качестве среды разработки, и приведены типы средств для создания приложений SharePoint, которые могут размещаться в Office 365.</span><span class="sxs-lookup"><span data-stu-id="3d850-171">Figure 2 shows how developers can use Office 365 as a development environment and includes the types of tools produce SharePoint applications that can be hosted in Office 365.</span></span>
  
    
    

<span data-ttu-id="3d850-172">**Рисунок 2. Разработка приложений Office 365**</span><span class="sxs-lookup"><span data-stu-id="3d850-172">**Figure 2. Office 365 app development**</span></span>

  
    
    
 <span data-ttu-id="3d850-173">[</span><span class="sxs-lookup"><span data-stu-id="3d850-173"></span></span>![Создание приложений для SharePoint с помощью Office 365, Visual Studio и средств разработки Napa.](../images/Office365AppDevelpment.png)
  
    
    
<span data-ttu-id="3d850-p115">Разработчики с подписками MSDN могут получить клиент разработки, содержащий SharePointСайт разработчиков. Сайт разработчиковSharePoint предварительно настроен для разработки приложений. Пользователи могут использовать Visual Studio 2012 не только при разработке приложений, но и с сайтами разработчика Office 365; для формирования приложений на сайте можно использовать Napa. Подробнее о начале работы с Сайт разработчиков Office 365 см. в статье  [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-p115">Developers with MSDN subscriptions can obtain a development tenant that contains aSharePointDeveloper Site. The SharePointDeveloper Site is preconfigured for developing applications. Users can use not only Visual Studio 2012 in developing applications, but with Office 365 developer sites, Napa can be used within the site to construct applications. For more information about getting started with anOffice 365 Developer Site, see  [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="3d850-179">Разработчики могут приступить к созданию приложений, которые будут размещаться в Office 365 и локальных или на другие инфраструктуры в модели размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="3d850-179">Developers can start creating applications that will be hosted in Office 365, on-premises or on other infrastructure in a provider-hosted model.</span></span> <span data-ttu-id="3d850-180">Преимущества этой среде ИТ-инфраструктуры, а другие размещения рекомендации для среды разработки для SharePoint и виртуализации полностью приведены в Office 365, что позволяет разработчикам создавать приложения мгновенно.</span><span class="sxs-lookup"><span data-stu-id="3d850-180">The benefit of this environment is that infrastructure, virtualization and other hosting considerations for a SharePoint development environment are abstracted by Office 365, allowing developers to create applications instantly.</span></span> <span data-ttu-id="3d850-181">Простые внимание для этого типа среды разработки — приложений, требующих полного доверия кода развернутое toSharePoint не может быть размещено.</span><span class="sxs-lookup"><span data-stu-id="3d850-181">A prime consideration for this type of development environment is that applications that require full trust code to be deployed toSharePoint cannot be accommodated.</span></span> <span data-ttu-id="3d850-182">Корпорация Майкрософт рекомендует создавать с помощью клиентской объектной модели SharePoint (CSOM) и клиентские технологии таких asJavaScript насколько это возможно.</span><span class="sxs-lookup"><span data-stu-id="3d850-182">Microsoft recommends using the SharePoint client-side object model (CSOM) and client-side technologies such asJavaScript as much as possible.</span></span> <span data-ttu-id="3d850-183">В случае, если кода полного доверия является обязательным (но не требуется, развертывание кода для запуска на SharePoint), корпорация Майкрософт рекомендует развертывание серверного кода в автоматическое размещение или размещение у поставщика в модели.</span><span class="sxs-lookup"><span data-stu-id="3d850-183">In the event that full trust code is required (but deployment of the code to run on SharePoint is not required), we recommend deploying the server-side code in an autohosted or provider-hosted model.</span></span> <span data-ttu-id="3d850-184">Обратите внимание на то, что эти решения с кодом полного доверия, развернутые в инфраструктуру с размещением у поставщика также используется CSOM, но можно использовать языки, такие как C#.</span><span class="sxs-lookup"><span data-stu-id="3d850-184">Note that these full trust code solutions that are deployed to provider-hosted infrastructure also use the CSOM but can use languages such as C#.</span></span> <span data-ttu-id="3d850-185">Также важно отметить, что эти приложения, развернутые в модели размещением у поставщика можно использовать другие технологии стеки и по-прежнему используется для взаимодействия с помощью SharePoint CSOM.</span><span class="sxs-lookup"><span data-stu-id="3d850-185">It's also important to note that these applications deployed in a provider-hosted model can use other technology stacks and still use the CSOM to interact with SharePoint.</span></span>
  
    
    
<span data-ttu-id="3d850-p117">Рабочим группам разработки, создающим отдельные компоненты или приложения, содержащие большое решение, понадобится централизованная цель развертывания для интеграции тестовых компонентов. Так как каждый разработчик создает компоненты или приложения на собственном сайте разработчика Office 365, необходимо подготовить к работе централизованное семейство веб-сайтов на целевом клиенте или в локальной среде, чтобы иметь возможность развертывать в них компоненты приложений каждого разработчика. Этот подход создаст централизованное место для тестирования интеграции компонентов решения. В  [разделе данного документа, посвященном тестированию](#Testing), этот процесс рассматривается подробнее.</span><span class="sxs-lookup"><span data-stu-id="3d850-p117">Development teams creating separate features or applications that contain a larger solution will need a centralized deployment target to integration test components. Because each developer is creating features or applications on their own Office 365 developer site, a centralized site collection in a target tenant or on-premises environment should be provisioned so that each developer's application components can be deployed there. This approach will allow for a centralized place to conduct integration testing between solution components. The  [testing section of this document](#Testing) reviews this process in more detail.</span></span>
  
    
    

#### <a name="napaoffice-365-development-tools"></a><span data-ttu-id="3d850-190">Средства разработки NapaOffice 365</span><span class="sxs-lookup"><span data-stu-id="3d850-190">NapaOffice 365 development tools</span></span>
<span data-ttu-id="3d850-191"><a name="NapaDevelopment"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-191"></span></span>

<span data-ttu-id="3d850-p118">Разработчики могут использовать средства разработки Napa для упрощения создания приложений на сайте разработчика Office 365. Средства Napa предназначены для разработчиков или опытных пользователей, профессионально разбирающихся в клиентских технологиях, и позволяют быстро разрабатывать и развертывать приложения в качестве прототипа, эксперимента или быстрого бизнес-решения. Эти средства позволяют разрабатывать функции приложений в SharePoint. Но в жизненном цикле приложения могут быть ситуации, когда приложение следует импортировать в Visual Studio. Они могу быть вызваны следующими причинами:</span><span class="sxs-lookup"><span data-stu-id="3d850-p118">The Napadevelopment tools can be used by developers for the simpler creation of applications within an Office 365 developer site. The intention of the Napa tools is for developers, or power users who are proficient in client-side technologies, to quickly develop and deploy applications in a prototype, proof-of-concept or rapid business solution scenario. These tools provide a means of developing application functionality on SharePoint. However, during the lifecycle of an application, there may be points at which the application should be imported into Visual Studio. These conditions are outlined as follows"</span></span>
  
    
    

- <span data-ttu-id="3d850-197">несколько разработчиков участвуют в разработке или разрабатывают различные части решения;</span><span class="sxs-lookup"><span data-stu-id="3d850-197">When more than one developer has to contribute or develop part of the solution</span></span>
    
  
- <span data-ttu-id="3d850-198">приложение достигло уровня зависимости от пользователей, при котором необходимо применять методы управления жизненным циклом;</span><span class="sxs-lookup"><span data-stu-id="3d850-198">When an application reaches a level of dependence by users whom requires the application of lifecycle management practices</span></span>
    
  
- <span data-ttu-id="3d850-199">со временем функциональные требования к приложению изменяются, требуя дополнительных компонентов приложения (например, скомпилированных служб или источников данных);</span><span class="sxs-lookup"><span data-stu-id="3d850-199">When functional requirements for the application change over time to require supplementary solution components (such as compiled services or data sources)</span></span>
    
  
- <span data-ttu-id="3d850-200">приложение требует интеграции с другими приложениями или компонентами решений;</span><span class="sxs-lookup"><span data-stu-id="3d850-200">When the application requires integration with other applications or solution components</span></span>
    
  
- <span data-ttu-id="3d850-201">разработчикам необходимо использовать средства контроля качества, такие как автоматические сборки и тестирование.</span><span class="sxs-lookup"><span data-stu-id="3d850-201">When developers have to use quality control measures such as automated builds and testing</span></span>
    
  
<span data-ttu-id="3d850-202">Когда возникают эти или подобные ситуации, разработчикам необходимо экспортировать решение в среду управления версиями, например TFS, а затем учесть рекомендации и применить процедуры проектирования управления жизненным циклом приложения в последующей разработке приложения.</span><span class="sxs-lookup"><span data-stu-id="3d850-202">Once these or other similar conditions occur, developers must export the solution into a source controlled environment such as TFS and apply ALM design considerations and procedures to the application's future development.</span></span>
  
    
    

### <a name="development-sites-remote-development"></a><span data-ttu-id="3d850-203">Сайты разработки (удаленная разработка)</span><span class="sxs-lookup"><span data-stu-id="3d850-203">Development sites (remote development)</span></span>
<span data-ttu-id="3d850-204"><a name="OnPremDevelopment"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-204"></span></span>

<span data-ttu-id="3d850-p119">Организации или разработчики, которые решили не использовать сайты разработчика Office 365 как основное средство разработки приложений SharePoint, могут использовать локальные сайты разработчика для создания приложений SharePoint. В такой модели возможность сайтов разработчика Office 365 заменяется локальными сайтами разработчика, размещаемыми в ферме SharePoint. Клиенты могут создать частное облако разработки, развернув ферму SharePoint на экземплярах сайта разработчика в компании. Клиенты могут применять собственную автоматизацию управления, чтобы обеспечить создание шаблона сайта разработчика, или использовать возможности продукта SharePoint для подготовки к работе экземпляров сайта разработчика. Эта проиллюстрировано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="3d850-p119">For organizations or developers who choose not to use Office 365 developer sites as a primary means for SharePoint application development, on-premises developer sites can be used to develop SharePoint applications. In this model, the Office 365 developer sites' capability is replaced with on-premises developer sites hosted within a SharePoint farm. Customers can create a development private cloud by deploying a SharePoint farm to house developer site instances. Customers can supply their own governance automation in order to provide developer site template creation or use the SharePoint in-product capabilities to provision developer site instances. Figure 3 illustrates this setup.</span></span>
  
    
    

<span data-ttu-id="3d850-210">**Рисунок 3. Локальная разработка приложения с шаблоном сайта разработчика**</span><span class="sxs-lookup"><span data-stu-id="3d850-210">**Figure 3. On-premises app development with the developer site template**</span></span>

  
    
    
 <span data-ttu-id="3d850-211">[</span><span class="sxs-lookup"><span data-stu-id="3d850-211"></span></span>![Создание приложений для SharePoint в локальном развертывании SharePoint с помощью шаблона сайта для разработчиков](../images/OnPremDevSites.png)
  
    
    
    
    
<span data-ttu-id="3d850-p120">На рисунке 3 показаны средства разработки и типы приложений, доступные благодаря сайтам разработчика при использовании локальной фермы SharePoint в качестве узла. Обратите внимание, что средства разработки NapaOffice 365 нельзя использовать в этой среде, потому что такая возможность есть только на сайтах разработки Office 365.</span><span class="sxs-lookup"><span data-stu-id="3d850-p120">Figure 3 describes the development tools and application types that can be enabled with developer sites when using an on-premises SharePoint farm as a host. Note that NapaOffice 365 development tools cannot be used in this environment as they are a capability only present in Office 365 development sites.</span></span>
  
    
    
<span data-ttu-id="3d850-p121">Фермы SharePoint, на которых размещаются экземпляры Сайт разработчиков, должны отслеживаться и соответствовать целевым значениям для обслуживания, точки восстановления и времени, чтобы разработчики, использующие их для создания приложений, могли работать эффективно и без прерываний. Клиенты могут применять к этой среде концепции частного облака, например гибкость, масштабируемость и структура управления. Управление и операции должны применяться к ферме SharePoint, в которой также размещены сайты разработчика. Это поможет контролировать неотслеживаемую группу из многочисленных сайтов разработчика, которые устарели или не используются, и понимать, когда необходимо масштабировать среду.</span><span class="sxs-lookup"><span data-stu-id="3d850-p121">TheSharePoint farm that hosts Developer Site instances must be monitored and meet service and recovery point and time level objectives so that developers who rely on them to create applications can be productive and not experience outages. Customers can apply private cloud concepts such as elasticity and scale units and a management fabric to this environment. Operations and management have to be applied to the SharePoint farm where the developer sites are hosted also. This will help control unmonitored sprawl of multiple developer sites that are stale or unused and provide a way to understand when the environment has to scale.</span></span>
  
    
    
<span data-ttu-id="3d850-219">Клиенты могут принятие решения об использовании инфраструктура как служба (IaaS) возможности как Microsoft Azure для ферм theSharePoint узлов, которые содержат и размещает сайты для разработчиков или собственные локальные виртуальные или физические среды.</span><span class="sxs-lookup"><span data-stu-id="3d850-219">Customers can decide to use infrastructure as a service (IaaS) capabilities like Microsoft Azure to host theSharePoint farms that contain and host developer sites, or their own on-premises virtual or physical environments.</span></span> <span data-ttu-id="3d850-220">Обратите внимание на то, что с помощью этой модели не требует установки SharePoint на каждом компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="3d850-220">Note that using this model does not require a SharePoint installation for each developer.</span></span> <span data-ttu-id="3d850-221">Разработка удаленных приложений потребуется только средства разработки Visual Studio и Office и SharePoint на рабочей станции разработчика.</span><span class="sxs-lookup"><span data-stu-id="3d850-221">Remote application development will only require Visual Studio and Office and SharePoint development tools on the developer work station.</span></span>
  
    
    
<span data-ttu-id="3d850-p123">Разработчики должны установить инфраструктуру с размещением у поставщика, чтобы развертывать приложения, размещаемые у поставщика. Хотя размещаемые у поставщика компоненты приложения SharePoint могут быть реализованы на широком спектре технологий, разработчики должны подготовить инфраструктуру для размещения тех компонентов приложения, которые работают за пределами SharePoint. Например, если команда разрабатывает приложение SharePoint, компоненты взаимодействия с пользователем и другие компоненты находятся в приложении ASP.NET, группе разработчиков следует использовать локальные версии IIS, SQL Server и др., чтобы применять традиционные шаблоны коллективной разработки управления жизненным циклом приложения для ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3d850-p123">Developers must establish provider-hosted infrastructure to deploy the provider-hosted applications. Although provider-hosted components of a SharePoint application can be implemented in a wide-array of technologies, developers must provide an infrastructure for hosting those components of the application that run outside SharePoint. For example, if a team is developing a SharePoint application whose user experience and other components reside in anASP.NET application, the development team should use local versions of IIS,SQL Server, and so on engage in traditional ALM team development patterns for ASP.NET.</span></span>
  
    
    

### <a name="self-contained-farm-environments-virtualized-farm-development"></a><span data-ttu-id="3d850-225">Автономные среды ферм (разработка виртуализированных ферм)</span><span class="sxs-lookup"><span data-stu-id="3d850-225">Self-contained farm environments (virtualized farm development)</span></span>
<span data-ttu-id="3d850-226"><a name="SelfContained"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-226"></span></span>

<span data-ttu-id="3d850-227">Для этих решений, которые требуют развертывания полного доверия для запуска на ферму SharePoint полная реализация (часто виртуализованной) SharePoint, требуется указать код.</span><span class="sxs-lookup"><span data-stu-id="3d850-227">For those solutions that require the deployment of full trust code to run on a SharePoint farm a full (often virtualized) implementation of SharePoint will be required.</span></span> <span data-ttu-id="3d850-228">Руководство по созданию в локальной среде разработки для SharePoint в разделе [Настройка локальной среды разработки для SharePoint надстройки](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-228">For guidance on how to create an on-premises development environment for SharePoint, see  [Set up an on-premises development environment for SharePoint Add-ins](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="3d850-229">На рисунке 4 показаны типы приложений, которые можно создавать, используя локальную виртуализированную среду.</span><span class="sxs-lookup"><span data-stu-id="3d850-229">Figure 4 shows the types of applications that can be created using an on-premises virtualized environment.</span></span>
  
    
    

<span data-ttu-id="3d850-230">**Рисунок 4. Локальное развертывание с виртуальной средой**</span><span class="sxs-lookup"><span data-stu-id="3d850-230">**Figure 4. On-premises development with a virtual environment**</span></span>

  
    
    
 <span data-ttu-id="3d850-231">[</span><span class="sxs-lookup"><span data-stu-id="3d850-231"></span></span>![Создание приложений для SharePoint в виртуальной локальной среде](../images/AppDevelopmentVirtualEnvironment.png)
  
    
    
    
    
<span data-ttu-id="3d850-p125">Разработчики могут удаленно развертывать SharePoint и размещаемые в облаке приложения в собственных фермах SharePoint, а также разрабатывать решения ферм с полным доверием. Эти фермы часто размещаются на сервере виртуализации, работающем на рабочей станции разработчика или в централизованном частном облаке виртуализации, к которому могут легко получать доступ разработчики. Среда фермы SharePoint обычно отделена от других ферм разработчиков и предоставляет уровень изоляции, необходимый при разработке кода полного доверия, который может требовать перезапуска критически важных служб (то есть IIS).</span><span class="sxs-lookup"><span data-stu-id="3d850-p125">Developers can conduct remote development for the SharePoint and cloud-hosted applications within their own SharePoint farms as well as the development of full trust farm solutions. These farms are often hosted within a virtualization server running either on the developer's workstation or in a centralized virtualization private cloud that can easily be accessible to developers. The SharePoint farm environment is usually separate from other developers' farms and provides a level of isolation that is required when developing full trust code that may require the restart of critical services (that is IIS).</span></span>
  
    
    
<span data-ttu-id="3d850-236">В автономной ферме можно выполнять удаленную разработку, а также разработку кода полного доверия, так как каждая ферма разработки является изолированной и выделенной для одного разработчика.</span><span class="sxs-lookup"><span data-stu-id="3d850-236">Remote development can occur within the self-contained farm as well as the development of full trust code as each development farm is isolated and dedicated to a single developer.</span></span>
  
    
    
<span data-ttu-id="3d850-p126">Организациям или разработчикам придется управлять фермами SharePoint, работающими на виртуальных компьютерах, и обновлять их. Для разработчиков, занимающихся одним приложением, необходимо поддерживать равенство в различных фермах разработки, работающих внутри виртуальных компьютеров. Такой подход гарантирует согласованность каждого компонента кода, разрабатываемого для приложения. Другим распространенным вопросом является стандартная конфигурация для ферм, включая доступ к домену и учетные данные, учетные данные приложения-службы, идентификаторы проверок или учетные записи и другие элементы конфигурации среды (например, сертификаты).</span><span class="sxs-lookup"><span data-stu-id="3d850-p126">Organizations or developers will have to manage and update the SharePoint farms running within the virtual computers. For developers who are contributing to a single application, parity across the development farms running inside the virtual computers must be maintained. This practice ensures that each component of code developed for the application has consistency. Other common considerations are a standard configuration for the farms including domain access and credentials, service application credentials, testing identities or accounts and other environmental configuration elements (such as certificates).</span></span>
  
    
    
<span data-ttu-id="3d850-241">Подобно централизованной ферме для сайтов разработки эти виртуальные машины, на которых работают фермы разработчика SharePoint, могут размещаться на платформах IaaS, например Microsoft Azure, и предложениях локального частного облака.</span><span class="sxs-lookup"><span data-stu-id="3d850-241">Similar to a centralized farm for development sites, these virtual machines running developerSharePoint farms can be hosted in IaaS platforms such as Microsoft Azure, and on-premises private cloud offerings.</span></span>
  
    
    
<span data-ttu-id="3d850-p127">Обратите внимание, что хотя виртуальные машины предлагают существенную изоляцию и независимость от других виртуальных машин разработчика, рабочим группам необходимо стремиться к поддержанию единообразия между конфигурациями виртуальных машин. Это включает общие настройки домена, учетных записей, безопасности и SharePoint, а также подключение к хранилищу системы управления версиями, например Visual Studio Team Foundation Server (TFS).</span><span class="sxs-lookup"><span data-stu-id="3d850-p127">Note that, although virtual machines offer a great deal of isolation and independence from other developer virtual machines, teams should strive to have uniformity between the virtual machine configurations. This includes common domain, account and security, SharePoint configurations and a connection to a source control repository such as Visual Studio Team Foundation Server (TFS).</span></span>
  
    
    

## <a name="alm-design-considerations"></a><span data-ttu-id="3d850-244">Аспекты проектирования управления жизненным циклом приложения</span><span class="sxs-lookup"><span data-stu-id="3d850-244">ALM design considerations</span></span>
<span data-ttu-id="3d850-245"><a name="ALMDesign"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-245"></span></span>

<span data-ttu-id="3d850-p128">При создании приложений SharePoint необходимо учесть несколько аспектов, чтобы внедрить управление и общие методы разработки для единообразия и качества. Применяя принципы управления жизненным циклом приложения к разработке приложения SharePoint, разработчики должны сосредоточить внимание на технических аспектах и вопросах, связанных с процессами.</span><span class="sxs-lookup"><span data-stu-id="3d850-p128">When constructing SharePoint applications, there are several considerations that have to be addressed to provide governance and common development practices for consistency and quality. When applying ALM principles to SharePoint application development, developers must focus on technical considerations as well as process-driven considerations.</span></span>
  
    
    
<span data-ttu-id="3d850-p129">Обычно при разработке приложений требуется поддержка платформы управления жизненным циклом приложения, например Visual Studio Team Foundation Server 2012, особенно для групп разработчиков, занимающихся одним набором проектов. Для приложений SharePoint, как и других технических решений, требуется управление хранилищем кода и версиями, службы сборки, службы тестирования и методы управления выпусками. В следующем разделе описаны соображения по поводу применения управления жизненным циклом приложения к различным моделям приложений для приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-p129">The support of an ALM platform, such as Visual Studio Team Foundation Server 2012, is usually a requirement when conducting application development especially with teams of developers working on the same set of projects. SharePoint applications, like other technical solutions, require code repository management and versioning, build services, testing services, and release management practices. The following section describes considerations for ALM as applied to the different application models for SharePoint applications.</span></span>
  
    
    

### <a name="overview"></a><span data-ttu-id="3d850-251">Обзор</span><span class="sxs-lookup"><span data-stu-id="3d850-251">Overview</span></span>
<span data-ttu-id="3d850-252"><a name="ALMDesignOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-252"></span></span>

<span data-ttu-id="3d850-p130">Соображения управления жизненным циклом приложения должны применяться к каждому типу приложений SharePoint без различий в концепции. Но необходимо настраивать методы и процедуры, касающиеся управления сборкой, тестированием и изменениями.</span><span class="sxs-lookup"><span data-stu-id="3d850-p130">For each type of SharePoint application, the ALM considerations must be applied without variation in concept. However, practices and procedures around build, testing, and change management must be adjusted.</span></span>
  
    
    
<span data-ttu-id="3d850-p131">В некоторых приложениях SharePoint будут использоваться клиентские технологии. Большинству разработчиков, имеющих опыт разработки приложений SharePoint Server 2010, будет необходимо приспосабливаться к разработке и применению принципов управления жизненным циклом приложения к некомпилированному коду. Это включает применение таких концепций, как "сборка", к решению, в котором может не быть скомпилированного кода. В платформах управления жизненным циклом приложения, например Visual Studio 2012, есть встроенные средства проверки сборок, которые сначала компилируют код, а затем запускают тесты проверки сборки.</span><span class="sxs-lookup"><span data-stu-id="3d850-p131">Some SharePoint applications will use client-side technologies. Most developers who have SharePoint Server 2010 application development experience will have to adjust to developing and applying ALM principles to non-compiled code. This adjustment includes applying concepts such as a "build" to a solution that may not have compiled code. ALM platforms such as Visual Studio 2012 have built-in capabilities to validate builds by first compiling the code, and second, by running build verification tests (BVTs) against the build.</span></span>
  
    
    
<span data-ttu-id="3d850-p132">Процесс сборки и тестирования приложений SharePoint должен оставаться согласованным с традиционными процессами разработки приложений. Это включает создание плана сборки платформой управления жизненным циклом приложения, который скомпилирует решение и развернет его в целевую среду.</span><span class="sxs-lookup"><span data-stu-id="3d850-p132">For SharePoint applications, the process relating to build and testing should remain consistent with traditional application development processes. This includes the creation of a build schedule by the ALM platform, which will compile the solution and deploy it into the target environment.</span></span>
  
    
    

### <a name="build-processes"></a><span data-ttu-id="3d850-261">Процессы сборки</span><span class="sxs-lookup"><span data-stu-id="3d850-261">Build processes</span></span>
<span data-ttu-id="3d850-262"><a name="ALMBuildProcess"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-262"></span></span>

<span data-ttu-id="3d850-p133">Платформа управления жизненным циклом приложения упрощает процессы сборки приложений SharePoint. Visual Studio Team Foundation Server 2012 предлагает услуги сборки и тестирования, которые могут запускаться при возврате решений из Visual Studio 2012 (непрерывная интеграция) или с определенными запланированными интервалами.</span><span class="sxs-lookup"><span data-stu-id="3d850-p133">The SharePoint application build processes are facilitated by the ALM platform. Visual Studio Team Foundation Server 2012 provides both build and test services that can be triggered on solution check in from Visual Studio 2012 (continuous integration) or at specified scheduled intervals.</span></span>
  
    
    

#### <a name="sharepoint-build-components"></a><span data-ttu-id="3d850-265">Компоненты сборки SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-265">SharePoint build components</span></span>
<span data-ttu-id="3d850-266"><a name="ALMBuildComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-266"></span></span>

<span data-ttu-id="3d850-267">Планируя процессы сборки для разработки приложений SharePoint, разработчикам необходимо учитывать взаимодействия между компонентами, как показано на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="3d850-267">When planning build processes for SharePoint application development, developers have to consider the interactions between the components, as shown in Figure 5.</span></span>
  
    
    

<span data-ttu-id="3d850-268">**Рисунок 5. Компоненты сборки приложения, размещаемого в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="3d850-268">**Figure 5. SharePoint-hosted app build components**</span></span>

  
    
    

  
    
    
![Построения Visual Studio работают с манифестами, страницами и поддерживающими файлами приложений.](../images/AppDevelopmentClientBuildComponents.png)
  
    
    
<span data-ttu-id="3d850-p134">На рисунке 5 проиллюстрировано логическое представление приложения SharePoint. На этой иллюстрации показано Надстройки, размещаемые в SharePoint и выделены ключевые объекты приложения в составе проекта Visual Studio 2012Надстройки, размещаемые в SharePoint. Проект приложения SharePoint содержит функции, пакет и манифест, которые будут зарегистрированы в SharePoint. Проект также содержит страницы, библиотеки сценариев и другие элементы взаимодействия с пользователем, которые составляют приложение SharePoint. Кроме того, в проекте SharePoint есть поддерживающие файлы, которые включают сертификаты, необходимые для развертывания в целевую среду SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-p134">The illustration in Figure 5 is a logical representation of a SharePoint application. This illustration shows a SharePoint-hosted add-in and highlights key application objects as part of a Visual Studio 2012SharePoint-hosted add-in project. The SharePoint app project contains the features, package, and manifest that will be registered with SharePoint. The project also contains pages, script libraries, and other elements of user experience that constitute the SharePoint application. In addition, the SharePoint project has supporting files which include the necessary certificates for deployment to a target SharePoint environment.</span></span>
  
    
    

<span data-ttu-id="3d850-275">**Рисунок 6. Компоненты сборки приложения с автоматическим размещением и размещением у поставщика**</span><span class="sxs-lookup"><span data-stu-id="3d850-275">**Figure 6. Provider-hosted and autohosted app build components**</span></span>

  
    
    

  
    
    
![Приложения с размещением у поставщика содержат как пакеты приложений SharePoint, так и компоненты, размещаемые в облаке.](../images/ProviderHostedAppBuildComponents.png)
  
    
    
<span data-ttu-id="3d850-p135">На рисунке 6 показано размещаемое в облаке приложение SharePoint (то есть, автоматически размещаемое или размещаемое у поставщика). Главная разница в структуре проекта заключается в том, что решение Visual Studio 2012 содержит проект приложения SharePoint, кроме одного или нескольких проектов, содержащих размещаемые в облаке компоненты приложений. Они могут включать веб-приложения, проекты базы данных SQL или приложения-услуги, которые будут развертываться в Azure или в локальную инфраструктуру, размещаемую у поставщика (например, ASP.NET), и другие компоненты решения. Инструкции по упаковке и развертыванию приложений с высоким уровнем доверия см. в статье  [Упаковка и публикация надстроек с высоким уровнем доверия для SharePoint](http://msdn.microsoft.com/library/3c28aed8-c037-407c-9154-39a74073e170%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-p135">Figure 6 shows a SharePoint cloud-hosted application (that is, autohosted or provider-hosted). The main difference in the project structure is that the Visual Studio 2012 solution contains a SharePoint application project in addition to one or more projects that contain the cloud-hosted application components. These may include web applications, SQL database projects, or service applications that will be deployed to Azure or an on-premises provider hosted infrastructure (such as ASP.NET) and other solution components. For guidance on packaging and deployment with high-trust applications, see  [Package and publish high-trust SharePoint Add-ins](http://msdn.microsoft.com/library/3c28aed8-c037-407c-9154-39a74073e170%28Office.15%29.aspx).</span></span>
  
    
    

<span data-ttu-id="3d850-281">**Рисунок 7. Управление жизненным циклом приложения с Visual Studio Team Foundation Server**</span><span class="sxs-lookup"><span data-stu-id="3d850-281">**Figure 7. ALM with Visual Studio Team Foundation Server**</span></span>

  
    
    

  
    
    
![TFS можно настроить для выполнения действий по сборке и развертыванию приложений SharePoint с помощью определений построений.](../images/ALMWithTFS.png)
  
    
    
<span data-ttu-id="3d850-p136">На рисунке 7 показан TFS в качестве платформы управления жизненным циклом приложения. Рабочие группы будут применять TFS для хранения кода и коллективной разработки, используя локальные или размещаемые в облаке службы TFS корпорации Майкрософт. TFS можно настроить для выполнения действий по сборке и развертыванию приложений SharePoint с помощью определений сборок. TFS также можно использовать для проведения тестов проверки сборки (BVT), которые можно автоматизировать путем выполнения выраженных с помощью кода тестов пользовательского интерфейса, которые входят в определение сборки.</span><span class="sxs-lookup"><span data-stu-id="3d850-p136">Figure 7 shows TFS as the ALM platform. Teams will use TFS to store code and conduct team development either using TFS deployed on-premises or using Microsoft cloud-based TFS services. TFS can be configured to conduct build and deployment activities with a SharePoint application through build definitions. TFS can also be used to conduct build verification tests (BVTs) that may be automated through the execution of coded UI tests that are part of the build definition.</span></span>
  
    
    

<span data-ttu-id="3d850-287">**Рисунок 8. Цели сборки TFS**</span><span class="sxs-lookup"><span data-stu-id="3d850-287">**Figure 8. TFS build targets**</span></span>

  
    
    

  
    
    
![Сценарии, выполняемые определением построения TFS, развертывают компоненты приложений SharePoint в SharePoint Online и локальной службе SharePoint.](../images/TFSBuildTargets.png)
  
    
    
<span data-ttu-id="3d850-p137">На рисунке 8 показаны целевые среды, в которых сценарии, выполняемые определением сборки TFS, будут развертывать компоненты приложения SharePoint. Для приложений, размещаемых в SharePoint, это включает развертывание в SharePoint Online или локальные каталоги приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-p137">Figure 8 shows the target environments where scripts executed by a TFS build definition will deploy the SharePoint application components. For SharePoint-hosted applications this includes deployment to either SharePoint Online or to on-premises SharePoint application catalogs.</span></span>
  
    
    
<span data-ttu-id="3d850-p138">Для приложений SharePoint, размещаемых в облаке, компоненты решения, требующие дополнительной инфраструктуры за пределами SharePoint, развертываются в целевые среды. Для приложений с автоматическим размещением это будет Microsoft Azure. Для приложений с размещением у поставщика такой инфраструктурой может быть Microsoft Azure или другие локальные или размещаемые в IaaS среды.</span><span class="sxs-lookup"><span data-stu-id="3d850-p138">For cloud-hosted SharePoint applications, the components of the solution that require additional infrastructure outside SharePoint are deployed to target environments. For autohosted applications, this will be Microsoft Azure. For provider-hosted applications, this infrastructure can be Microsoft Azure, or other on-premises or IaaS-hosted environments.</span></span>
  
    
    

#### <a name="creating-a-build-for-sharepoint-applications"></a><span data-ttu-id="3d850-294">Создание сборки для приложений SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-294">Creating a build for SharePoint applications</span></span>
<span data-ttu-id="3d850-295"><a name="CreateBuild"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-295"></span></span>

<span data-ttu-id="3d850-p139">TFS предоставляет службы сборки, которые могут компилировать решения, возвращенные в систему управления версиями, и помещать результат в централизованное заданное место для автоматического развертывания в целевые среды. Основной метод настройки TFS для автоматического создания сборок, развертываний и тестирования приложений SharePoint состоит в создании определения сборки в Visual Studio. Определение сборки содержит информацию о том, какие проекты кода следует компилировать, и действиях после компиляции, таких как тестирование и фактическое развертывание в целевые среды. Подробнее о службе сборки Team Foundation см. в статье  [Настройка службы сборки Team Foundation](http://msdn.microsoft.com/en-us/library/vstudio/ee259687.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-p139">TFS provides build services that can compile solutions checked into source control and place the output in a centralized drop location for deployment to target environments in an automated manner. The primary method of configuring TFS to conduct automated builds, deployments, and testing of SharePoint applications is to create a build definition in Visual Studio. The build definition contains information about which code projects to compile, as well as any post-compilation activities such as testing and actual deployment to the target environments. For more information about the Team Foundation Build Service, see  [Set up Team Foundation Build Service](http://msdn.microsoft.com/en-us/library/vstudio/ee259687.aspx).</span></span>
  
    
    
<span data-ttu-id="3d850-p140">Для непрерывной интеграции определение сборки может запускаться, когда разработчики возвращают код. Кроме того, можно запланировать выполнение определения сборки с установленными интервалами.</span><span class="sxs-lookup"><span data-stu-id="3d850-p140">To achieve continuous integration, the build definition can be triggered when developers check in code. Additionally, the build definition can be scheduled to execute at set intervals.</span></span>
  
    
    
<span data-ttu-id="3d850-302">ForSharePoint приложения разработчикам следует использовать проект определения построения [Непрерывной интеграции Office и SharePoint с помощью TFS 2012 г.](http://officesharepointci.codeplex.com/) для достижения запланированные построения и непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="3d850-302">ForSharePoint applications, developers should use the  [Office/SharePoint Continuous Integration with TFS 2012](http://officesharepointci.codeplex.com/) build definitions project to achieve scheduled builds or continuous integration.</span></span> <span data-ttu-id="3d850-303">Этот проект содержит определений построений, сценарии Windows PowerShell и процесс инструкции по настройке Visual Studio Online или в локальной версии TFS, построение и развертывание приложений SharePoint в модели непрерывной интеграции.</span><span class="sxs-lookup"><span data-stu-id="3d850-303">This project provides build definitions, Windows PowerShell scripts, and process instructions on how to configure Visual Studio Online or an on-premises version of TFS to build and deploy SharePoint applications in a continuous integration model.</span></span> <span data-ttu-id="3d850-304">Разработчикам необходимо загрузить компоненты в этот проект и настроить их экземпляр TFS соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="3d850-304">Developers should download the components in this project and configure their instance of TFS accordingly.</span></span> <span data-ttu-id="3d850-305">Подробные инструкции по настройке TFS с определением построения отмеченными для приложений SharePoint и настройке определения построения использовать сценарии Windows PowerShell для развертывания приложений SharePoint в целевую среду [Office / Непрерывной интеграции SharePoint с помощью TFS 2012 документации](http://officesharepointci.codeplex.com/documentation).</span><span class="sxs-lookup"><span data-stu-id="3d850-305">For instructions on how to configure TFS with the provided build definition for SharePoint applications and configure the build definition to use the Windows PowerShell scripts to deploy the SharePoint application to a target environment, see the [Office/SharePoint Continuous Integration with TFS 2012 documentation](http://officesharepointci.codeplex.com/documentation).</span></span>
  
    
    

#### <a name="configuring-build-and-deployment-procedures"></a><span data-ttu-id="3d850-306">Настройка процедур сборки и развертывания</span><span class="sxs-lookup"><span data-stu-id="3d850-306">Configuring build and deployment procedures</span></span>
<span data-ttu-id="3d850-307"><a name="ConfigureBuilds"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-307"></span></span>

<span data-ttu-id="3d850-308">На рисунке 9 показан стандартный процесс для сборок и развертываний приложения SharePoint, когда определение сборки создано, настроено и развернуто в экземпляр TFS рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="3d850-308">Figure 9 shows a standard process for SharePoint application builds and deployments when the build definition has been created, configured, and deployed to the team's instance of TFS.</span></span>
  
    
    

<span data-ttu-id="3d850-309">**Рисунок 9. Процесс сборки и развертывания с TFS**</span><span class="sxs-lookup"><span data-stu-id="3d850-309">**Figure 9. Build and deployment process with TFS**</span></span>

  
    
    
 <span data-ttu-id="3d850-310">[</span><span class="sxs-lookup"><span data-stu-id="3d850-310"></span></span>![Службы построения TFS выполняют действия, указанные в определении построения приложения SharePoint.](../images/ALMBuildDeployProcess.png)
  
    
    
    
<span data-ttu-id="3d850-p142">Разработчик возвращает решение Visual Studio 2012 приложения SharePoint. В зависимости от необходимой конфигурации (то есть, непрерывной интеграции или запланированной сборки) службы сборки TFS будут выполнять действия, указанные определением сборки приложения SharePoint. Это определение, настроенное разработчиками, содержит шаблон процесса сборки непрерывной интеграции, а также инструкции, которые применяются после сборки для выполнения сценариев Windows PowerShell для развертывания приложения. Обратите внимание, что для развертывания приложения в SharePoint Online понадобятся расширения командной консоли SharePoint Online. Подробнее о расширениях командной консоли SharePoint Online см. на странице  [Командная консоль SharePoint Online](http://www.microsoft.com/en-us/download/details.aspx?id=35588) в Центре загрузки.</span><span class="sxs-lookup"><span data-stu-id="3d850-p142">The developer checks in the SharePoint application Visual Studio 2012 solution. Depending on the desired configuration (that is, continuous integration or scheduled build), TFS build services will execute the steps defined by the SharePoint application build definition. This definition, configured by developers, contains the continuous integration build process template as well as post-build instructions to execute Windows PowerShell scripts for application deployment. Note that the SharePoint Online Management Shell extensions will be required in order to deploy the application to SharePoint Online. For more information about SharePoint Online Management Shell extensions, see  [SharePoint Online Management Shell page](http://www.microsoft.com/en-us/download/details.aspx?id=35588) on the Download Center.</span></span>
  
    
    
<span data-ttu-id="3d850-317">Как только будет активирована сборка, TFS скомпилирует проекты, связанные с приложением SharePoint, и выполнит сценарии Windows PowerShell, чтобы развернуть решение в целевую среду SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-317">Once the build has been triggered, TFS will compile the projects associated with the SharePoint application and execute Windows PowerShell scripts to deploy the solution to the target SharePoint environment.</span></span>
  
    
    

#### <a name="trusting-the-sharepoint-application"></a><span data-ttu-id="3d850-318">Доверие приложению SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-318">Trusting the SharePoint application</span></span>
<span data-ttu-id="3d850-319"><a name="TrustingApp"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-319"></span></span>

<span data-ttu-id="3d850-p143">После развертывания компонентов приложения в целевую среду важно обратить внимание, что прежде чем кто-либо получит доступ к приложению, включая автоматические тесты, которые могут быть частью сборки, администратор клиента (или семейства сайтов) должен указать доверие для приложения на странице информации о приложении в SharePoint. Это требование применяется к приложениям с автоматическим размещением и размещением в SharePoint. Этот выполняемый вручную процесс представляет собой изменение в процессе сборки, так как понадобится приостановить тесты, которые обычно выполняются после развертывания в целевую среду, пока не будет указано доверие для приложения.</span><span class="sxs-lookup"><span data-stu-id="3d850-p143">Following deployment of the application components to the target environments, it is important to note that before anyone accessing the application, including automated tests that may be part of the build, a tenant (or site collection) administrator will have to trust the application on the app information page in SharePoint. This requirement applies to autohosted and SharePoint-hosted apps. This manual process represents a change in the build process as tests that would typically run following the deployment to the target environment will have to be suspended until the application is trusted.</span></span>
  
    
    
<span data-ttu-id="3d850-323">Обратите внимание, что для размещаемых в облаке (автоматически или у поставщика) приложений разработчики могут развертывать компоненты, не относящиеся к SharePoint, в инфраструктуру с размещением в облаке отдельно от пакета приложений, развернутого в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-323">Note that for cloud-hosted (auto and provider) applications, developers can deploy the non-SharePoint components to the cloud-hosted infrastructure separately from the application package that is deployed to SharePoint.</span></span>
  
    
    

<span data-ttu-id="3d850-324">**Рисунок 10. Развертывание компонентов, не относящихся к SharePoint**</span><span class="sxs-lookup"><span data-stu-id="3d850-324">**Figure 10. Deploying non-SharePoint components**</span></span>

  
    
    
 <span data-ttu-id="3d850-325">[</span><span class="sxs-lookup"><span data-stu-id="3d850-325"></span></span>![По мере того как разработчики вносят изменения в решение, представляющее приложение SharePoint, могут возникать условия, в которых изменения проектов в рамках решения не распространяются на сам проект приложения SharePoint.](../images/ALMChangeManagement.png)
  
    
    
    
<span data-ttu-id="3d850-p144">Как показано на рисунке 10, когда разработчики вносят изменения в решение, представляющее приложение SharePoint, могут возникать условия, в которых изменения проектов в рамках решения не распространяются на сам проект приложения SharePoint. При таких обстоятельствах нет необходимости повторно развертывать проект приложения SharePoint, так как он не изменился. Изменения, связанные с размещаемыми в облаке проектами, должны быть повторно развернуты.</span><span class="sxs-lookup"><span data-stu-id="3d850-p144">As shown in Figure 10, when developers make changes to the solution that represents the SharePoint application, there may be circumstances where changes are made to the projects within the solution that do not apply to theSharePoint application project itself. In this circumstance, the SharePoint application project does not have to be redeployed as it has not changed. The changes associated with the cloud-hosted projects must be redeployed.</span></span>
  
    
    
<span data-ttu-id="3d850-p145">Можно внести изменения в приложение, которое будет развернуто в инфраструктуру вне SharePoint, отдельно от компонентов приложения, которые развертываются в целевое семейство сайтов или клиент. Для разработчиков это означает, что можно создать процесс автоматической сборки, чтобы развертывать размещаемые в облаке компоненты часто (путем активации) и отдельно от проекта приложения SharePoint. Таким образом, не требуется выполнять вручную действия по утверждению разрешения для приложения на странице информации о приложении в SharePoint, что позволяет более выполнять непрерывные процессы развертывания и тестирования для определения сборки. Компонент приложения SharePoint решения необходимо развертывать только в ситуации, когда элементы этого проекта изменяются и требуют развертывания.</span><span class="sxs-lookup"><span data-stu-id="3d850-p145">Changes to the application that will be deployed to infrastructure outside SharePoint can be done so separately from the application components that get deployed into the target site collection or tenant. For developers, this means that an automated build process can be created to deploy the cloud-hosted components on a frequent (triggered) basis and separately from the SharePoint application project. Thus, the manual step to approve the application's permission on the app information page in SharePoint is not required, allowing for a more continuous deployment and testing process for the build definition. The SharePoint application component of the solution would only have to be deployed in a circumstance were the items within this project changed and required redeployment.</span></span>
  
    
    

### <a name="testing"></a><span data-ttu-id="3d850-334">Тестирование</span><span class="sxs-lookup"><span data-stu-id="3d850-334">Testing</span></span>
<span data-ttu-id="3d850-335"><a name="Testing"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-335"></span></span>

<span data-ttu-id="3d850-p146">Как описано в  [разделе о процессах сборки](#ALMBuildProcess), тестирование приложения  это метод определения того, успешно ли выполнена компиляция и развертывание приложения. Используя тестирование в качестве средства проверки сборки и развертывания приложения, рабочая группа получает представление о качестве, а также узнает о том, когда последние изменения в коде приложения привели к ошибкам в приложении SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-p146">As described in the  [build processes section](#ALMBuildProcess), application testing is a method of determining whether the compilation and deployment of the application was successful. By using testing as a means of verifying the build and deployment of the application, the team is provided with an understanding of quality, as well as a way of knowing when a recent change to the application's code has compromised the SharePoint application.</span></span>
  
    
    
<span data-ttu-id="3d850-338">На рисунке 11 показаны типы подходов тестирования, которые лучше всего использовать с моделями приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-338">Figure 11 shows the types of testing approaches that are best used with SharePoint application models.</span></span>
  
    
    

<span data-ttu-id="3d850-339">**Рисунок 11. Подходы к тестированию**</span><span class="sxs-lookup"><span data-stu-id="3d850-339">**Figure 11. Testing approaches**</span></span>

  
    
    
 <span data-ttu-id="3d850-340">[</span><span class="sxs-lookup"><span data-stu-id="3d850-340"></span></span>![Закодированные тесты пользовательского интерфейса следует выполнять для приложений с размещением в SharePoint, где бизнес-логика и пользовательский интерфейс размещаются в одном слое.](../images/ALMTestingTypes.png)
  
   
    
    
<span data-ttu-id="3d850-p147">На рисунке 11 показано использование различных типов тестов для тестирования приложений SharePoint по типу. Закодированные тесты пользовательского интерфейса следует выполнять для приложений с размещением в SharePoint, где бизнес-логика и пользовательский интерфейс размещаются в одном слое. Тогда как бизнес-логика может быть абстрагирована в библиотеки JavaScript, основным средством тестирования является испытание логики в работе пользователями.</span><span class="sxs-lookup"><span data-stu-id="3d850-p147">Figure 11 suggests the use of different types of tests for testing SharePoint applications by type. Coded UI tests should be used against SharePoint-hosted applications where the business logic and the user experience reside in the same layer. While business logic can be abstracted to JavaScript libraries, a primary means of testing that logic will be through the user experience.</span></span>
  
    
    
<span data-ttu-id="3d850-p148">Размещаемые в облаке приложения (то есть, с автоматическим размещением и размещением у поставщика) могут использовать полностью закодированные тесты пользовательского интерфейса, при этом также используя модульные тесты для проверки компонентов служб решения. Благодаря этому разработчик может быть уверен в качестве реализации размещаемой инфраструктуры приложения с функциональной точки зрения.</span><span class="sxs-lookup"><span data-stu-id="3d850-p148">Cloud-hosted applications (that is, autohosted and provider-hosted) can use fully coded UI tests while also using unit tests for verification of the service components of the solution. This provides developer confidence in the quality of the application's hosted infrastructure implementation from a functional perspective.</span></span>
  
    
    
<span data-ttu-id="3d850-347">В следующих сценариях рассматриваются вопросы закодированных тестов пользовательского интерфейса и других типов тестов в отношении приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d850-347">The following sections review the considerations for coded UI tests and other test types in relation to SharePoint applications.</span></span>
  
    
    

#### <a name="client-side-code-and-coded-ui-tests"></a><span data-ttu-id="3d850-348">Клиентский код и закодированные тесты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="3d850-348">Client-side code and coded UI tests</span></span>
<span data-ttu-id="3d850-349"><a name="CodedUITests"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-349"></span></span>

<span data-ttu-id="3d850-p149">Для тестирования проверки сборки (BVT) и полного тестирования системы рекомендуется использовать закодированные тесты пользовательского интерфейса. В них используются записанные действия для тестирования не только бизнес-логики и среднего уровня приложения, но и взаимодействия с пользователем. Для приложений SharePoint, в которых используется код на стороне клиента, значительная часть точек входа и выполнения бизнес-логики может находиться на уровне взаимодействия с пользователем. Поэтому с помощью закодированных тестов пользовательского интерфейса можно проверять не только взаимодействие с пользователем, но и бизнес-логику приложения. Подробнее о закодированном тесте пользовательского интерфейса см. в статье  [Проверка кода с помощью модели автоматизации пользовательского интерфейса](http://msdn.microsoft.com/en-us/library/dd286726.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-p149">For build verification testing (BVT) as well as complete system testing, coded UI tests are recommended. These tests rely on recorded actions to test not only the business logic and middle tier of the application, but the user experience as well. For SharePoint applications that use client-side code, much of the business logic's entry points and execution may exist in the user experience tier. For this reason, coded UI tests can not only test the user experience, but the business logic of the application as well. For more information about the coded UI test, see  [Verifying Code by Using UI Automation](http://msdn.microsoft.com/en-us/library/dd286726.aspx).</span></span>
  
    
    
<span data-ttu-id="3d850-p150">Закодированные тесты пользовательского интерфейса можно использовать в Надстройки, размещаемые в SharePoint, в которых может быть объединена значительная часть пользовательского интерфейса с бизнес-логикой. Эти тесты, как и другие, можно запускать из определения сборки в TFS, чтобы проверять с их помощью функциональные возможности приложения после развертывания (и приложение является доверенным для SharePoint).</span><span class="sxs-lookup"><span data-stu-id="3d850-p150">Coded UI tests can be used in SharePoint-hosted add-ins where much of the UX and the business logic may be intermixed. These tests, like others can be run from a build definition in TFS so that they can verify an application's functionality after deployment (and the application is trusted by SharePoint).</span></span>
  
    
    

#### <a name="non-coded-ui-tests"></a><span data-ttu-id="3d850-357">Незакодированные тесты пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="3d850-357">Non-coded UI tests</span></span>
<span data-ttu-id="3d850-358"><a name="NonCodedUITests"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-358"></span></span>

<span data-ttu-id="3d850-p151">В ситуациях, когда логика приложения находится вне уровня пользовательского интерфейса приложения, например в приложениях, размещенных в облаке, следует использовать комбинацию из закодированных и незакодированных тестов пользовательского интерфейса. Можно использовать тесты, например традиционные модульные тесты, для проверки качества сборки логики службы, реализованной в инфраструктуре, размещенной у поставщика. Благодаря этому разработчик получает полную уверенность в размещаемых у поставщика компонентах функции решения, которые также охватываются тестами.</span><span class="sxs-lookup"><span data-stu-id="3d850-p151">For circumstances where the application logic exists outside the application's UX layer, such as in cloud-hosted applications, a combination of coded UI tests and non-coded UI tests should be leveraged. Tests such as traditional unit tests can be used to validate the build quality of service logic that is implemented on a provider-hosted infrastructure. This provides the developer with a holistic confidence in the provider-hosted components of the solution function, and are covered from a testing point of view.</span></span>
  
    
    

#### <a name="web-performance-and-load-tests"></a><span data-ttu-id="3d850-362">Веб-тесты производительности и нагрузочные тесты</span><span class="sxs-lookup"><span data-stu-id="3d850-362">Web performance and load tests</span></span>
<span data-ttu-id="3d850-363"><a name="LoadTests"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-363"></span></span>

<span data-ttu-id="3d850-p152">Веб-тесты производительности и нагрузочные тесты предоставляют разработчикам уверенность в том, что нагрузка пользователей на функции приложения меньше ожидаемое или прогнозируемой. Такое тестирование включает определение возможности приложения параллельно обрабатывать прогнозируемую базу пользователей, которая будет изменяться со временем. Как закодированные тесты пользовательского интерфейса, так и модульные тесты можно использовать как веб-тесты производительности и нагрузочные тесты. С помощью платформ управления жизненным циклом приложения, например TFS, эти тесты можно использовать для нагрузочного тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="3d850-p152">Web performance and load tests provide developers with the confidence that the application functions under expected or anticipated user loads. This testing includes determining the application's capability to concurrently handle a predictable user base that will reasonably scale over time. Both coded UI and unit tests can be the source of the web performance and load test. Using an ALM platform like TFS, these tests can be used to load test the application.</span></span>
  
    
    
<span data-ttu-id="3d850-p153">Обратите внимание, что тестирование инфраструктуры не является главной целью этих тестов, когда они используются для проверки приложений SharePoint. Для инфраструктуры (с размещением в SharePoint или у поставщика) необходимо установить аналогичную базу нагрузки и производительности. Веб-тесты производительности и нагрузочные тесты для приложения определяют проблемы инфраструктуры, но их следует рассматривать в первую очередь как средства тестирования производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="3d850-p153">Note that the testing of the infrastructure is not a primary goal of these tests when using them to test SharePoint applications. The infrastructure, whether SharePoint-hosted or provider-hosted, should have a similar load and performance baseline established. The web performance and load tests for the application will highlight infrastructure challenges, but should be regarded primarily as a means to test the application's performance.</span></span>
  
    
    
<span data-ttu-id="3d850-371">Подробнее о веб-тестах производительности и нагрузочных тестах см. в статье  [Проведение тестов производительности приложения перед его выпуском](http://msdn.microsoft.com/en-us/library/vstudio/dn250793.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-371">For more information about web performance and load tests, see  [Run performance tests on an application before a release](http://msdn.microsoft.com/en-us/library/vstudio/dn250793.aspx).</span></span>
  
    
    

#### <a name="quality-and-testing-environments"></a><span data-ttu-id="3d850-372">Качество и тестовые среды</span><span class="sxs-lookup"><span data-stu-id="3d850-372">Quality and testing environments</span></span>
<span data-ttu-id="3d850-373"><a name="TestingEnvironments"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-373"></span></span>

<span data-ttu-id="3d850-p154">Во многих организациях есть несколько сред тестирования, которые могут быть физическими или виртуальными и отдельными друг от друга. Эти среды могут различаться в зависимости от процесса управления жизненным циклом приложения, законодательных требований и комбинации обоих этих факторов. Чтобы определять количество и типы тестовых сред, которые следует использовать рабочим группам, следующее руководство основывается на функциональных методиках, свойственных приложениям SharePoint, а также использует общие методики управления жизненным циклом приложения для разработки программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="3d850-p154">Many organizations have several testing environments that may be either physical, or virtual and separate from each other. These environments can vary based on a team's ALM process, regulatory requirements or a combination of both. To determine the number and types of testing environments that teams should use, the following guidance is based on functional practices specific to SharePoint applications, but also uses ALM practices for software development at large.</span></span>
  
    
    

#### <a name="developer-testing"></a><span data-ttu-id="3d850-377">Тестирование силами разработчиков</span><span class="sxs-lookup"><span data-stu-id="3d850-377">Developer testing</span></span>
<span data-ttu-id="3d850-378"><a name="DevTesting"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-378"></span></span>

<span data-ttu-id="3d850-p155">Тестирование силами разработчиков можно применять в средах, где разработчики создают свой компонент решения. Многие разработчики, работающие над различными аспектами или компонентами более крупного приложения, будут проводить собственные модульные тесты, закодированные тесты пользовательского интерфейса и развертывание кода приложения на своих сайтах разработки.</span><span class="sxs-lookup"><span data-stu-id="3d850-p155">Developer testing can occur in the environment where the developers are creating their component of the solution. Multiple developers, working on different aspects or components of a larger application, will each have unit tests, coded UI tests, and the application code deployed into their development site.</span></span>
  
    
    

<span data-ttu-id="3d850-381">**Рисунок 12. Процесс тестирования силами разработчиков**</span><span class="sxs-lookup"><span data-stu-id="3d850-381">**Figure 12. Developer testing process**</span></span>

  
    
    
 <span data-ttu-id="3d850-382">[</span><span class="sxs-lookup"><span data-stu-id="3d850-382"></span></span>![Разработчики выполняют проверки Visual Studio для компонентов решения, развернутых на собственном сайте Office 365 или локальном сайте разработчика.](../images/ALMDeveloperTesting.png)
  
    
    
    
<span data-ttu-id="3d850-p156">Разработчики будут выполнять проверки Visual Studio для компонентов решения, развернутых на собственном сайте Office 365 или локальном сайте разработчика. Тесты для приложений, размещаемых в облаке, также будут выполняться из Visual Studio на компонентах решения, находящихся в инфраструктуре, размещаемой у поставщика. Эти компоненты будут находиться в подписке Microsoft Azure разработчика.</span><span class="sxs-lookup"><span data-stu-id="3d850-p156">Developers will execute tests from Visual Studio against the solution components deployed in their own Office 365 or on-premises developer site. For cloud-hosted applications, the tests will also be executed from Visual Studio against the solution components that reside on provider-hosted infrastructure. These components will reside in the developer's Microsoft Azure subscription.</span></span>
  
    
    
<span data-ttu-id="3d850-p157">Обратите внимание, что для этого подхода предполагается, что у разработчиков есть как индивидуальные сайты разработчика Office 365, так и подписки Microsoft Azure, предоставляемые через подписки MSDN. Даже если разработчики создают приложения для локального развертывания, эти службы разработчика можно использовать для разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="3d850-p157">Note that this approach assumes that developers either have individual Office 365 developer sites and Microsoft Azure subscriptions, which are supplied through MSDN subscriptions. Even if developers are creating applications for on-premises deployment, these developer services can be used for development and testing.</span></span>
  
    
    
<span data-ttu-id="3d850-p158">Если у разработчиков нет этих служб или им необходимо выполнять всю разработку локально, они будут выполнять тесты для своих компонентов на семействе сайтов разработчика локальной фермы и в зависящей от разработчика инфраструктуре, размещаемой у поставщика. Инфраструктура, размещаемая у поставщика, может находиться на выделенных виртуальных машинах разработчика. Для разработки решений полного доверия разработчикам будет необходима собственная виртуальная ферма SharePoint и размещаемая у поставщика инфраструктура.</span><span class="sxs-lookup"><span data-stu-id="3d850-p158">If developers do not have these services, or are required to do development entirely on-premises, then they will execute tests for their components against an on-premises farm's developer site collection and developer-specific, provider-hosted infrastructure. The provider-hosted infrastructure can reside in developer-dedicated virtual machines. For the development of full-trust solutions, developers would require their own virtual SharePoint farm and provider-hosted infrastructure.</span></span>
  
    
    

#### <a name="integration-and-systems-testing"></a><span data-ttu-id="3d850-392">Интеграция и тестирование систем</span><span class="sxs-lookup"><span data-stu-id="3d850-392">Integration and systems testing</span></span>
<span data-ttu-id="3d850-393"><a name="IntegrationTesting"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-393"></span></span>

<span data-ttu-id="3d850-p159">Для тестирования приложения все компоненты разработки должны быть собраны и развернуты в централизованной среде. Эта среда интеграции предоставляет место, где разработчики могут развертывать созданные ими компоненты решения и наблюдать за их взаимодействием с другими компонентами решения, написанными другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="3d850-p159">In order to test the application, all of the development components should be assembled and deployed in a centralized environment. This integration environment provides a place where developers can deploy and observe the components of the solution they created interacting with other solution components written by other developers.</span></span>
  
    
    

<span data-ttu-id="3d850-396">**Рисунок 13. Среда тестирования интеграции**</span><span class="sxs-lookup"><span data-stu-id="3d850-396">**Figure 13. Integration testing environment**</span></span>

  
    
    
 <span data-ttu-id="3d850-397">[</span><span class="sxs-lookup"><span data-stu-id="3d850-397"></span></span>![TFS построит и развернет приложение SharePoint, а также все необходимые компоненты, в целевых средах.](../images/ALMIntegrationTesting.png)
  
    
    
<span data-ttu-id="3d850-399">Для этого типа тестирования платформу управления жизненным циклом Приложений построит и развернет приложение SharePoint, а также все необходимые компоненты в целевых средах.</span><span class="sxs-lookup"><span data-stu-id="3d850-399">For this type of testing, the ALM platform will build and deploy the SharePoint application and any required components to the target environments.</span></span> <span data-ttu-id="3d850-400">Для приложений, размещенных в SharePoint это будет на сайте Office 365 или на локальном/IaaS семейства сайтов SharePoint, в частности указывается для интеграция и тестирование систем.</span><span class="sxs-lookup"><span data-stu-id="3d850-400">For SharePoint-hosted applications, this will either be an Office 365 site or an on-premises/IaaS SharePoint site collection specifically established for integration and systems testing.</span></span> <span data-ttu-id="3d850-401">Для приложений, размещаемых в облаке SharePoint TFS также развернуть компоненты для централизованного подписки Microsoft Azure, где будут настроены службы специально для тестирования интеграции/систем.</span><span class="sxs-lookup"><span data-stu-id="3d850-401">For SharePoint cloud-hosted applications, TFS will also deploy the components to a centralized Microsoft Azure subscription where the services will be configured specifically for integration/systems testing.</span></span> <span data-ttu-id="3d850-402">TFS будет выполнять закодированные тесты пользовательского интерфейса или подразделения для приложения SharePoint, а также все компоненты, необходимые для решения на размещенной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="3d850-402">TFS will then execute coded UI or unit tests against the SharePoint application, as well as any components that the solution requires on hosted infrastructure.</span></span>
  
    
    

#### <a name="uat-and-qa-testing"></a><span data-ttu-id="3d850-403">Приемочное тестирование пользователями и тестирование контроля качества</span><span class="sxs-lookup"><span data-stu-id="3d850-403">UAT and QA testing</span></span>
<span data-ttu-id="3d850-404"><a name="UATTesting"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-404"></span></span>

<span data-ttu-id="3d850-p161">Для приемочного тестирования пользователями у организаций часто есть отдельные среды, где эта функция выполняется отдельно от тестирования интеграции и систем. Разделение этих сред тестирования позволяет избежать влияния срока автоматического постоянного выпуска и тестирования на действия приемочного тестирования пользователями, когда пользователи могут выполнять тесты на определенной сборке приложения в течение длительного срока.</span><span class="sxs-lookup"><span data-stu-id="3d850-p161">For user acceptance testing (UAT), organizations often have separate environments where this function is performed apart from integration and systems testing. Separating these testing environments prevents the cadence of automated continuous release and testing from interfering with UAT activities where users may be executing tests against a specified build of the application over an extended period of time.</span></span>
  
    
    

<span data-ttu-id="3d850-407">**Рисунок 14. Приемочное тестирование пользователями**</span><span class="sxs-lookup"><span data-stu-id="3d850-407">**Figure 14. UAT testing**</span></span>

  
    
    
 <span data-ttu-id="3d850-408">[</span><span class="sxs-lookup"><span data-stu-id="3d850-408"></span></span>![Пользователи, которым поручено проводить приемочное или организационное тестирование, выполняют тестовые сценарии в стабильной среде, которая фокусируется на известной сборке приложения.](../images/ALMUATTesting.png)
  
    
    
    
<span data-ttu-id="3d850-p162">Как показано на рисунке 14, пользователи, которым поручено проводить приемочное или организационное тестирование, выполняют тестовые сценарии в стабильной среде, которая фокусируется на известной сборке приложения. Пока будет выполняться развертывание и тестирование кода в интегрированной среде, пользователи будут вручную проводить тесты для проверки того, соответствует ли приложение необходимым вариантам использования или тестовым случаям. Приложение и размещаемая у поставщика среда будет развернута (обычно выполняется диспетчером выпусков) в эту тестовую среду. Автоматическое развертывание также возможно. В таком виде развертывания используется выделенное определение сборки приемочного тестирования пользователями в сервере TFS, который зеркалирует сервер, выполняющий развертывание для тестирования интеграции и среды тестирования систем.</span><span class="sxs-lookup"><span data-stu-id="3d850-p162">As shown in Figure 14, users assigned to conduct acceptance testing or organizational testing resources conduct test scripts in a stable environment that is focused on a well-publicized build of the application. While code deployment and testing continues in the integration environment, users will conduct manual testing to validate that the application meets required use or test cases. The application and any provider-hosted infrastructure will be deployed, typically by a release manager, into this testing environment. An automated deployment is possible as well. This sort of deployment uses a dedicated UAT build definition in TFS that mirrors the one that conducts deployment for the integration and systems testing environment.</span></span>
  
    
    
<span data-ttu-id="3d850-p163">Для инфраструктуры, размещаемой в облаке, можно выполнять развертывание в подписку Microsoft Azure, используемую совместно с тестовой средой интеграции или систем, если службам присвоены имена и они настроены для параллельного развертывания в качестве отдельных служб или баз данных. Этот подход предлагает набор служб и баз данных в подписке тестирования Microsoft Azure для тестирования интеграции и систем, а также приемочного тестирования пользователями и тестирования контроля качества, как показано на рисунке 15.</span><span class="sxs-lookup"><span data-stu-id="3d850-p163">For cloud-hosted infrastructure, deployment into a Microsoft Azure subscription that is shared with the integration and systems test environments is possible if the services are named and configured to be deployed side by side as different services or databases. This approach provides a set of services and databases in the testing Microsoft Azure subscription for integration and systems testing as well as UAT and QA testing, as shown in Figure 15.</span></span>
  
    
    

<span data-ttu-id="3d850-417">**Рисунок 15. Тестирование интеграции и приемочное тестирование пользователями**</span><span class="sxs-lookup"><span data-stu-id="3d850-417">**Figure 15. Integration and UAT testing**</span></span>

  
    
    
 <span data-ttu-id="3d850-418">[</span><span class="sxs-lookup"><span data-stu-id="3d850-418"></span></span>![Развертывание в подписку Microsoft Azure, используемую совместно с тестовой средой интеграции или систем, возможно, если службам присвоены имена и они настроены для параллельного развертывания в качестве отдельных служб или баз данных.](../images/ALMIntegrationandUAT.png)
  
   
    
    

#### <a name="code-promotion-practices"></a><span data-ttu-id="3d850-420">Методики распространения кода</span><span class="sxs-lookup"><span data-stu-id="3d850-420">Code promotion practices</span></span>
<span data-ttu-id="3d850-421"><a name="CodePromotion"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-421"></span></span>

<span data-ttu-id="3d850-p164">Процесс распространения кода между средами разработки и тестирования, а также рабочей средой должен выполняться с использованием хорошо определенного процесса управления выпусками. На рисунке 16 показано, как разработчики развертывают компоненты своего решения в среды разработки для модульного тестирования.</span><span class="sxs-lookup"><span data-stu-id="3d850-p164">The code promotion process between the development and testing environments as well as the production environment should be done using a well-defined release management process. In Figure 16, developers conduct deployment of their solution components to development environments for unit testing.</span></span>
  
    
    

<span data-ttu-id="3d850-424">**Рисунок 16. Процесс управления выпусками**</span><span class="sxs-lookup"><span data-stu-id="3d850-424">**Figure 16. Release management process**</span></span>

  
    
    
 <span data-ttu-id="3d850-425">[</span><span class="sxs-lookup"><span data-stu-id="3d850-425"></span></span>![После возврата в TFS процедура автоматического построения компилирует и развертывает решения в целевой среде, где в рамках определения построения в TFS выполняются соответствующие проверки.](../images/ALMCodePromotion.png)
  
   
    
    
<span data-ttu-id="3d850-p165">После возврата в TFS процедура автоматической сборки компилирует и развертывает решения в целевой среде тестирования интеграции и систем, где в рамках определения сборки в TFS выполняются соответствующие проверки. Этот подход включает развертывание компонентов решения, размещаемых у поставщика, в целевую среду (Microsoft Azure или локальные среды). Обратите внимание, что для инфраструктуры Microsoft Azure можно использовать ту же подписку Microsoft Azure, которая использовалась для тестирования интеграции и системы, приемочного тестирования пользователями и тестирования контроля качества, предполагая, что они развернуты в различных пространствах имен и отдельных базах данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3d850-p165">Following a check-in to TFS, an automated build procedure will compile and deploy the solution to the target integration and system testing environment where build verification tests will be executed as part of the build definition in TFS. This approach includes deploying the provider-hosted components of the solution to the target environment (Microsoft Azure or on-premises environments). Note that for Microsoft Azure infrastructure, the Microsoft Azure subscription can be the same one used for both integration and system testing as well as UAT and QA assuming they are deployed to different namespaces and separate SQL databases.</span></span>
  
    
    
<span data-ttu-id="3d850-p166">Диспетчер выпусков или отдельное определение сборки TFS, в большинстве случаев запускаемое вручную, может развертываться в среду агента пользователя или TQA. Этот подход помогает контролировать версию сборки, которую будут тестировать пользователи. Диспетчеры выпусков могут комплектовать сборки из общей папки TFS и самостоятельно выполнять процесс развертывания. Управление выпусками будет применяться в течение всего процесса, от распространения до выпуска, для развертывания приложения в рабочей среде и отслеживания его установки и проверки сборки путем тестов.</span><span class="sxs-lookup"><span data-stu-id="3d850-p166">A release manager or a separate TFS build definition, manually invoked in most cases, can deploy to the UA or TQA environment. This approach helps control the build version that users will be testing against. Release managers can pick up the builds from a TFS share and execute the deployment process themselves. From promotion to production, release management will be involved to deploy the application to the production environment and monitor its installation and build verification through tests.</span></span>
  
    
    

## <a name="application-patching-and-upgrades"></a><span data-ttu-id="3d850-434">Исправления и обновления приложений</span><span class="sxs-lookup"><span data-stu-id="3d850-434">Application patching and upgrades</span></span>
<span data-ttu-id="3d850-435"><a name="AppPatching"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-435"></span></span>

<span data-ttu-id="3d850-436">Конкретные инструкции на как разработчики приложений могут обновление приложений корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3d850-436">Microsoft has specific guidance on how application developers can upgrade applications.</span></span> <span data-ttu-id="3d850-437">Платформа SharePoint поддерживает уведомление о новой версии приложений для пользователей.</span><span class="sxs-lookup"><span data-stu-id="3d850-437">The SharePoint platform supports the notification of new application versions to users.</span></span>
  
    
    
<span data-ttu-id="3d850-438">Соображения по поводу внедрения стратегии исправлений и обновлений приложения SharePoint см. в статье  [Обновление надстроек для SharePoint](http://msdn.microsoft.com/library/3edcb33c-fa9e-4e9e-82d6-5519fd981324%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d850-438">For considerations on establishing a strategy around SharePoint application upgrades and patching, see  [Update SharePoint Add-ins](http://msdn.microsoft.com/library/3edcb33c-fa9e-4e9e-82d6-5519fd981324%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="3d850-p168">Рекомендуемый шаблон изменений приложений согласуется с имеющимися шаблонами разработки кода и инженерной поддержки. Это включает упорядоченное ветвление и объединение устранений ошибок и разработки компонентов, а также добавочных развертываний в целевые каталоги приложений. Предыдущее руководство можно использовать для внесения изменений в приложения для SharePoint и их развертывания в целевые каталоги приложений или магазин.</span><span class="sxs-lookup"><span data-stu-id="3d850-p168">For changes to applications, the recommended pattern to follow is consistent with existing code development and sustained engineering patterns. This includes disciplined branching and merging for bug fixes and feature development as well as incremental deployments to target application catalogs. The preceding guidance can be used to complete changes to applications for SharePoint and deploy them to target application catalogs or the store.</span></span>
  
    
    
<span data-ttu-id="3d850-p169">В статье  [Процедура обновления надстроек для SharePoint](http://msdn.microsoft.com/library/3dba209d-cb98-4e5d-b4b2-fad31e667ca1%28Office.15%29.aspx) представлено дополнительное тактическое руководство по методикам обновления приложений SharePoint. Это включает ускорение тестирования развертывания путем сокращения цикла обновления, в ходе которого обновления приложения отражаются в ферме в тестовых средах. Кроме того, в этой статье приведено руководство по согласовывать состояние в различных моделях развертывания приложений.</span><span class="sxs-lookup"><span data-stu-id="3d850-p169">The information in  [SharePoint Add-ins update process](http://msdn.microsoft.com/library/3dba209d-cb98-4e5d-b4b2-fad31e667ca1%28Office.15%29.aspx) provides additional tactical guidance on the techniques for updating SharePoint applications. This includes accelerating deployment testing by shortening the cycle by which application updates are reflected in the farm in test environments. Additionally, this article has guidance on how to accommodate for state within various application deployment models.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="3d850-445">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3d850-445">Additional resources</span></span>
<span data-ttu-id="3d850-446"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3d850-446"></span></span>


-  [<span data-ttu-id="3d850-447">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-447">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="3d850-448">Настройка службы сборки Team Foundation</span><span class="sxs-lookup"><span data-stu-id="3d850-448">Set up Team Foundation Build Service</span></span>](http://msdn.microsoft.com/en-us/library/vstudio/ee259687.aspx)
    
  
-  [<span data-ttu-id="3d850-449">Использование сайта Office 365 SharePoint для авторизации размещенных у поставщика надстроек на локальном сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-449">Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site</span></span>](http://msdn.microsoft.com/library/2f65ba3f-b246-4064-b4fb-ad18399d387a%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="3d850-450">Обзор разработки решений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d850-450">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  
-  [<span data-ttu-id="3d850-451">Что такое Open Data Protocol?</span><span class="sxs-lookup"><span data-stu-id="3d850-451">What is the Open Data Protocol?</span></span>](http://www.odata.org/)
    
  
-  [<span data-ttu-id="3d850-452">Платформа авторизации OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="3d850-452">The OAuth 2.0 authorization framework</span></span>](http://oauth.net/)
    
  

  
    
    

