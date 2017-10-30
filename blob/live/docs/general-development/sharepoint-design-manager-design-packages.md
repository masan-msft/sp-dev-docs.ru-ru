---
title: "Пакеты разработки дизайнер SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 85ad1993-4d75-4806-9097-b934865a899a
ms.openlocfilehash: 7f8998bf6ef9f4eca0592c498d377a2920611976
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-design-manager-design-packages"></a><span data-ttu-id="d3daa-102">Пакеты разработки дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3daa-102">SharePoint Design Manager design packages</span></span>
<span data-ttu-id="d3daa-103">Узнайте, как создавать и экспортировать визуальный Дизайн семейства веб-сайтов SharePoint в виде пакета.</span><span class="sxs-lookup"><span data-stu-id="d3daa-103">Learn how to build and export the visual design of a SharePoint site collection as a package.</span></span>
## <a name="overview-of-design-packages"></a><span data-ttu-id="d3daa-104">Обзор конструктора пакетов</span><span class="sxs-lookup"><span data-stu-id="d3daa-104">Overview of Design Packages</span></span>
<span data-ttu-id="d3daa-105"><a name="int"> </a></span><span class="sxs-lookup"><span data-stu-id="d3daa-105"></span></span>

<span data-ttu-id="d3daa-106">В SharePoint руководитель проекта может помочь разработчиков веб-приложений и дизайнеры построения и экспортировать визуальный Дизайн семейства веб-сайтов SharePoint в виде пакета.</span><span class="sxs-lookup"><span data-stu-id="d3daa-106">In SharePoint, Design Manager can help web developers and designers build and export the visual design of a SharePoint site collection as a package.</span></span> <span data-ttu-id="d3daa-107">Этот пакет можно легко распространяется или другом обозначены групп для установки на их семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="d3daa-107">This package can easily be distributed to customers, or other designated groups, for installation on their site collections.</span></span> <span data-ttu-id="d3daa-108">Этот новый компонент уменьшает сложность переноса проектов и упрощает для клиентов реализовать аутсорсинг задач визуальный Дизайн своих сайтов.</span><span class="sxs-lookup"><span data-stu-id="d3daa-108">This new feature reduces the complexity of transporting designs, and makes it easier for customers to outsource the visual design of their sites.</span></span> <span data-ttu-id="d3daa-109">Например некоторые сценарии использования могут включать следующее:</span><span class="sxs-lookup"><span data-stu-id="d3daa-109">For example, some usage scenarios can include the following:</span></span>
  
    
    

- <span data-ttu-id="d3daa-p102">**Новые разработки**  компании с ограниченной web возможности средств разработки может контракта бюро поставщика для обновления их текущего сайта SharePoint с современными интерпретации. Деятельностью организации можно создавать сайт и легко упаковать содержимое для импорта обратно в ферме SharePoint компании.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p102">**New Design** —A company with limited web design capabilities might contract a vendor agency to refresh their current SharePoint site with a more modern interpretation. The agency can create the site and easily package the contents for importing back into the company SharePoint farm.</span></span>
    
  
- <span data-ttu-id="d3daa-112">**Межсайтовой публикации** — предприятии ИТ отдела, с помощью публикации на нескольких сайтах в SharePoint может потребоваться совместно использовать визуальный Дизайн в нескольких семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="d3daa-112">**Cross-Site Publishing** —An enterprise IT department using cross-site publishing in SharePoint might have to share a visual design across multiple site collections.</span></span> <span data-ttu-id="d3daa-113">Они самостоятельно создавать сайт и хотите простой способ передачи Разработка через несколько веб-сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3daa-113">They create the site in-house and want a simple way to transport the design across several SharePoint websites.</span></span> <span data-ttu-id="d3daa-114">Функциональные возможности пакета проектирования через диспетчер устройств позволяет им для экспорта и импорта с ограниченной Административная поддержка и сложности.</span><span class="sxs-lookup"><span data-stu-id="d3daa-114">The design package functionality through Device Manager enables them to export and import with reduced administrative support and complexity.</span></span>
    
  
<span data-ttu-id="d3daa-115">В этой статье, помогут вам понять упаковки разработки в SharePoint, предоставляя Обзор создания пакетов и содержатся рекомендации рабочего процесса для пакета экспорта и импорта.</span><span class="sxs-lookup"><span data-stu-id="d3daa-115">This article can help you understand design packaging in SharePoint by providing an overview of package creation, and offers workflow guidance for package exporting and importing.</span></span> <span data-ttu-id="d3daa-116">В ней также рассматриваются необходимые разрешения для определенных операций и разработка архитектуры пакета.</span><span class="sxs-lookup"><span data-stu-id="d3daa-116">It also discusses required permissions for specific operations, and design package architecture.</span></span>
  
    
    

## <a name="creating-a-design-package"></a><span data-ttu-id="d3daa-117">Создание пакета конструктора</span><span class="sxs-lookup"><span data-stu-id="d3daa-117">Creating a design package</span></span>
<span data-ttu-id="d3daa-118"><a name="package"> </a></span><span class="sxs-lookup"><span data-stu-id="d3daa-118"></span></span>

<span data-ttu-id="d3daa-p105">Пользователь создает пакета конструктора, называется пакет решения SharePoint (WSP-файл) на сайте SharePoint, через дизайнер в **Настройках сайта**. Шаг для создания пакета образом другие действия дизайнер для фирменной настройки и публикации сайта SharePoint, включая передача файлов проекта, Создание главной страницы и изменение макетов страниц. После публикации сайта является сравнительно легко процесс создания WSP-файла для экспорта.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p105">A user creates a design package, called a SharePoint solution package (.wsp file) on their SharePoint site, through Design Manager in **Site Settings**. The step for creating the package follows other Design Manager steps for branding and publishing a SharePoint site, including uploading design files, creating a master page, and editing page layouts. After the site is published, it is a relatively simple process to create the .wsp file for export.</span></span>
  
    
    
<span data-ttu-id="d3daa-122">На рисунке 1 показано параметр в диспетчере оформления для создания пакета проектирования и присвоение ему имени.</span><span class="sxs-lookup"><span data-stu-id="d3daa-122">Figure 1 shows the option in Design Manager for naming and creating the design package.</span></span>
  
    
    

<span data-ttu-id="d3daa-123">**На рисунке 1. Экспорт пакета проектирования**</span><span class="sxs-lookup"><span data-stu-id="d3daa-123">**Figure 1. Exporting a design package**</span></span>

  
    
    

  
    
    
![Экспортирование пакета конструктора](../images/sp15Con_DesignPackageExp_Figure1.png)
  
    
    
<span data-ttu-id="d3daa-125">Кроме того можно импортировать пакета конструктора из другого семейства сайтов SharePoint через дизайнер на странице приветствия или выбрав команду **Импорт пакета проектирования** в **Настройках сайта**.</span><span class="sxs-lookup"><span data-stu-id="d3daa-125">Alternatively, you can import a design package from another SharePoint site collection through Design Manager on the Welcome page, or by choosing **Import design package** in **Site Settings**.</span></span>
  
    
    

    
> <span data-ttu-id="d3daa-126">**Примечание:** Дополнительные сведения о диспетчере оформления и процесс публикации можно [Обзор диспетчера оформления в SharePoint](overview-of-design-manager-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d3daa-126">**Note:** For more information about Design Manager and the publishing process, see  [Overview of Design Manager in SharePoint](overview-of-design-manager-in-sharepoint.md).</span></span> 
  
    
    

<span data-ttu-id="d3daa-p106">Существует флажок для включения конфигурации поиска в пакете разработки. Выбрать этот параметр, если проектирование сайта и создание результатов поиска условного или управление результатов поиска. Эта конфигурация содержит активов как правила запросов, источники результатов, типы результатов и все модели схемы и ранжирования. Чтобы убедиться, что импорт конфигурации поиска не будет, здесь не должно быть повторяющихся имен для любых элементов конфигурации поиска. Например если имеется правило запроса в семейства веб-сайтов с именем **SampleQueryRule**и импортировать его в другом семейства сайтов с помощью существующего правила с именем **SampleQueryRule**, импорт конфигурации поиска не удается выполнить. Чтобы предотвратить это, можно переименовать или удалить правило запроса в источнике или в целевой системе. Источники результатов и схемы, также должны иметь уникальное имя. Если вы хотите включить конфигурацию поиска в пакет разработки, следующие функции на уровне сайта в разделе **Управление компонентами сайта** необходимо активировать, прежде чем экспортировать пакет разработки:</span><span class="sxs-lookup"><span data-stu-id="d3daa-p106">There is a check box for including the search configuration in the design package. You would choose this option if you are designing a site and creating conditional search results, or controlling the search experience. This configuration contains assets like query rules, result sources, result types, and any schema and ranking models. To ensure that the import of the search configuration does not fail, there must not be duplicate names for any elements of the search configuration. For example, if you have a query rule in a site collection named **SampleQueryRule**, and you import it into another site collection with an existing rule named **SampleQueryRule**, importing the search configuration fails. To prevent this, you can rename or delete the query rule on the source or on the target. Result sources, and the schema, also have to be uniquely named. If you want to include a search configuration in your design package, you must activate the following features at the site level under **Manage Site Features** before you export the design package:</span></span>
  
    
    

- <span data-ttu-id="d3daa-135">Типы контента данные конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="d3daa-135">Search Config Data Content Types</span></span>
    
  
- <span data-ttu-id="d3daa-136">Столбцы сайта данные конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="d3daa-136">Search Config Data Site Columns</span></span>
    
  
- <span data-ttu-id="d3daa-137">Компонент экземпляра список конфигураций поиска</span><span class="sxs-lookup"><span data-stu-id="d3daa-137">Search Config List Instance Feature</span></span>
    
  
- <span data-ttu-id="d3daa-138">Функция шаблона конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="d3daa-138">Search Config Template Feature</span></span>
    
  
<span data-ttu-id="d3daa-p107">Если необходимо, чтобы данный проект нужно опубликовать в целевой системе импорта, следует публикация всех средств разработки или отключение основных управления версиями в библиотеках связанных с в источнике экспорта. Дизайнер экспорт только наиболее поздней версии каждого средства из источника. Например если установлена версия 1.1 главной страницы на исходном его копируются в конечную как черновик. Однако не копируются версии 1.0. Кроме того не экспортируются файлы, извлеченные проекты.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p107">If you want your design to be published on the target of import, you should publish all design assets or disable major versioning in design-related libraries on the source of export. Design Manager exports only the most recent version of each asset from the source. For example, if you have version 1.1 of a master page on the source it will be copied to the target as a draft. But, version 1.0 is not copied. Also, files that are checked out are not exported.</span></span>
  
    
    

## <a name="exporting-and-importing-a-design-package"></a><span data-ttu-id="d3daa-144">Экспорт и Импорт пакета конструктора</span><span class="sxs-lookup"><span data-stu-id="d3daa-144">Exporting and importing a design package</span></span>
<span data-ttu-id="d3daa-145"><a name="work"> </a></span><span class="sxs-lookup"><span data-stu-id="d3daa-145"></span></span>

<span data-ttu-id="d3daa-p108">Рабочий процесс упаковки начала до конца несколькими способами, можно подход с гораздо подход в зависимости от целей и доступные ресурсы. В группу можно реализовать аутсорсинг задач для поставщика агентство или выполнения работы внутри компании, если у вас есть внутренний услуг. В таблице 1 обеспечивает пример рабочего процесса и exchange между клиентом и бюро поставщика разработки, экспорт и Импорт пакета конструктора. Он также предоставляет разрешения, необходимые для операций, связанных с проектирования и операции упаковки.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p108">You can approach an end-to-end packaging workflow several ways, with much of the approach depending on your objectives and available design resources. You may decide to outsource to a vendor agency, or do the work in-house if you have internal resourcing. Table 1 provides a sample workflow and exchange between a client and a vendor agency over the design, exporting, and importing of the design package. It also provides the required permissions for design-related operations, and packaging operations.</span></span>
  
    
    

<span data-ttu-id="d3daa-150">**В таблице 1. Пример структуры пакета рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="d3daa-150">**Table 1. Sample design package workflow**</span></span>


|<span data-ttu-id="d3daa-151">**Шаг**</span><span class="sxs-lookup"><span data-stu-id="d3daa-151">**Step**</span></span>|<span data-ttu-id="d3daa-152">**Действие**</span><span class="sxs-lookup"><span data-stu-id="d3daa-152">**Action**</span></span>|<span data-ttu-id="d3daa-153">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d3daa-153">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="d3daa-154">1</span><span class="sxs-lookup"><span data-stu-id="d3daa-154">1</span></span>  <br/> |<span data-ttu-id="d3daa-155">Поддержки поставщика контракты клиента для создания визуальной разработки.</span><span class="sxs-lookup"><span data-stu-id="d3daa-155">Customer contracts vendor agency to create visual design.</span></span>  <br/> | <span data-ttu-id="d3daa-156">Конструктор поставщика создается сайт, в соответствии с требованиями организации.</span><span class="sxs-lookup"><span data-stu-id="d3daa-156">The vendor designer creates site, based on company requirements.</span></span> <br/> <span data-ttu-id="d3daa-157">**Примечание:**  Конструктор поставщика необходимо иметь уровень разрешений **конструкторы** использовать Дизайнер и создание и экспорт пакетов.</span><span class="sxs-lookup"><span data-stu-id="d3daa-157">**Note:**  The vendor designer must have the **Designers** permission level to use Design Manager and create and export packages.</span></span> <span data-ttu-id="d3daa-158">В частности разрешение **разработки** , обеспечивающий просмотр, добавление, обновление, удаление, утверждение и настройка дизайна.</span><span class="sxs-lookup"><span data-stu-id="d3daa-158">More specifically, the **Design** permission that allows viewing, adding, updating, deleting, approving, and customizing visual designs.</span></span>          |
|<span data-ttu-id="d3daa-159">2</span><span class="sxs-lookup"><span data-stu-id="d3daa-159">2</span></span>  <br/> |<span data-ttu-id="d3daa-160">Конструктор поставщика экспортирует визуальный Дизайн в пакете разработки.</span><span class="sxs-lookup"><span data-stu-id="d3daa-160">Vendor designer exports visual design into a design package.</span></span>  <br/> | <span data-ttu-id="d3daa-161">Конструктор поставщика экспортирует пакет решения SharePoint (WSP-файл) после завершения других необходимых фирменной символики и публикации действия.</span><span class="sxs-lookup"><span data-stu-id="d3daa-161">The vendor designer exports the SharePoint solution package (.wsp file) after completing the other required branding and publishing steps.</span></span> <br/>  <span data-ttu-id="d3daa-162">Пакет разработки доставляется клиента через безопасный канал.</span><span class="sxs-lookup"><span data-stu-id="d3daa-162">The design package is delivered to the customer via a secure channel.</span></span> <br/> |
|<span data-ttu-id="d3daa-163">3</span><span class="sxs-lookup"><span data-stu-id="d3daa-163">3</span></span>  <br/> |<span data-ttu-id="d3daa-164">Визуальный Дизайн импортирует клиента в его указанного семейства сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3daa-164">Customer imports visual design into their specified SharePoint site collection.</span></span>  <br/> | <span data-ttu-id="d3daa-165">Клиент получает пакет разработки через безопасный канал.</span><span class="sxs-lookup"><span data-stu-id="d3daa-165">The customer receives the design package via a secure channel.</span></span> <br/>  <span data-ttu-id="d3daa-166">Через начальная страница в диспетчере оформления или с помощью команды **Импорт пакета проектирования** в **Настройках сайта** клиента импортирует WSP-файл и предоставляет пакет разработки в указанном семействе сайтов.</span><span class="sxs-lookup"><span data-stu-id="d3daa-166">Through the Welcome page in Design Manager or by choosing **Import design package** in **Site Settings**, the customer imports the .wsp file and applies the design package to the specified site collection.</span></span>  <br/> <span data-ttu-id="d3daa-167">**Примечание:**  Клиента необходимо иметь уровень разрешений **конструкторы** использовать Дизайнер и импорта пакетов разработки.</span><span class="sxs-lookup"><span data-stu-id="d3daa-167">**Note:**  The customer must have the **Designers** permission level to use Design Manager and import design packages.</span></span>          |
   

## <a name="understanding-design-package-contents"></a><span data-ttu-id="d3daa-168">Общее представление о содержимое пакета проектирования</span><span class="sxs-lookup"><span data-stu-id="d3daa-168">Understanding design package contents</span></span>
<span data-ttu-id="d3daa-169"><a name="packcont"> </a></span><span class="sxs-lookup"><span data-stu-id="d3daa-169"></span></span>

<span data-ttu-id="d3daa-p110">Несколько файлов включаются в WSP-файл пакета проектирования при его создании через дизайнер. Процесс экспортирует файлы из различных списков и библиотек для формирования общий пакета. При импорте семейства веб-сайтов, эти файлы распространяются в другие расположения, в зависимости от типа файла. В таблице 2 приведены сведения о расположении и тип файлов, экспортируемых в процессе сборки.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p110">Several files are included in the design package .wsp file when it is created through Design Manager. The process exports files from various lists and libraries to form the overall package. While importing to a site collection, these files are distributed to different locations based on file type. Table 2 details the location and type of files exported during the assembly process.</span></span>
  
    
    

<span data-ttu-id="d3daa-174">**В таблице 2. Сводка по содержимое пакета проектирования и exportation расположения файлов**</span><span class="sxs-lookup"><span data-stu-id="d3daa-174">**Table 2. Summary of design package contents and file exportation locations**</span></span>


|<span data-ttu-id="d3daa-175">**Папка для экспорта**</span><span class="sxs-lookup"><span data-stu-id="d3daa-175">**Export Location**</span></span>|<span data-ttu-id="d3daa-176">**Экспортированные активов**</span><span class="sxs-lookup"><span data-stu-id="d3daa-176">**Exported Assets**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d3daa-177">Библиотеки документов</span><span class="sxs-lookup"><span data-stu-id="d3daa-177">Document libraries</span></span>  <br/> | <span data-ttu-id="d3daa-178">Коллекция главных страниц</span><span class="sxs-lookup"><span data-stu-id="d3daa-178">Master Pages Gallery</span></span> <br/>  <span data-ttu-id="d3daa-179">Коллекция тем</span><span class="sxs-lookup"><span data-stu-id="d3daa-179">Themes Gallery</span></span> <br/>  <span data-ttu-id="d3daa-180">Библиотека стилей</span><span class="sxs-lookup"><span data-stu-id="d3daa-180">Style Library</span></span> <br/>  <span data-ttu-id="d3daa-181">библиотека ресурсов сайта;</span><span class="sxs-lookup"><span data-stu-id="d3daa-181">Site Assets Library</span></span> <br/> |
|<span data-ttu-id="d3daa-182">Типы контента, полей</span><span class="sxs-lookup"><span data-stu-id="d3daa-182">Content types, fields</span></span>  <br/> | <span data-ttu-id="d3daa-183">Типы контента, наследующие от типа контента страницы</span><span class="sxs-lookup"><span data-stu-id="d3daa-183">Content types that inherit from the Page content type</span></span> <br/> |
|<span data-ttu-id="d3daa-184">Списки</span><span class="sxs-lookup"><span data-stu-id="d3daa-184">Lists</span></span>  <br/> | <span data-ttu-id="d3daa-185">Макетов</span><span class="sxs-lookup"><span data-stu-id="d3daa-185">Design Gallery</span></span> <br/>  <span data-ttu-id="d3daa-186">Вариантов оформления</span><span class="sxs-lookup"><span data-stu-id="d3daa-186">Composed looks</span></span> <br/>  <span data-ttu-id="d3daa-187">Каналы устройств</span><span class="sxs-lookup"><span data-stu-id="d3daa-187">Device channels</span></span> <br/> |
   

> <span data-ttu-id="d3daa-188">**Примечание:** В SharePoint только настроенные файлы включены в пакеты проекта.</span><span class="sxs-lookup"><span data-stu-id="d3daa-188">**Note:** In SharePoint, only customized files are included in design packages.</span></span> <span data-ttu-id="d3daa-189">Процесс упаковки не будет экспортировать большая часть файлы без дополнительной настройки системы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3daa-189">The packaging process will not export most of the default non-customized system files.</span></span> 
  
    
    

<span data-ttu-id="d3daa-190">В SharePoint не удается удалить пакет импортированного проекта и никогда не следует отключить пакета конструктора через коллекции решений.</span><span class="sxs-lookup"><span data-stu-id="d3daa-190">In SharePoint you cannot uninstall an imported design package, and you should never attempt to deactivate a design package through the solution gallery.</span></span> <span data-ttu-id="d3daa-191">В противном случае типы контента макета страницы, удалены и пользователи не смогут создавать дочерние узлы.</span><span class="sxs-lookup"><span data-stu-id="d3daa-191">If you do, page layout content types are removed and users may not be able to create subsites.</span></span> <span data-ttu-id="d3daa-192">Восстановиться это состояние означает, необходимо выполнить следующие действия которых веб-A = исходного семейства веб-сайтов B = семейство сайтов с пакетом неактивные разработки (некорректном состоянии) и веб-сайтов C = семейства пустой веб-сайтов, созданную вами:</span><span class="sxs-lookup"><span data-stu-id="d3daa-192">To recover from this state, you should perform the following steps where site A= the original site collection, site B = the site collection with the deactivated design package (bad state), and site C = a new, blank site collection that you have created:</span></span>
  
    
    

1. <span data-ttu-id="d3daa-193">Экспорт пакета проектирования из сайта А</span><span class="sxs-lookup"><span data-stu-id="d3daa-193">Export a design package from site A</span></span>
    
  
2. <span data-ttu-id="d3daa-194">Импорт пакета проектирования сайт C</span><span class="sxs-lookup"><span data-stu-id="d3daa-194">Import the design package to site C</span></span>
    
  
3. <span data-ttu-id="d3daa-195">Экспорт пакета проектирования с сайта B</span><span class="sxs-lookup"><span data-stu-id="d3daa-195">Export a design package from site B</span></span>
    
  
4. <span data-ttu-id="d3daa-196">Импорт пакета проектирования сайт C</span><span class="sxs-lookup"><span data-stu-id="d3daa-196">Import the design package to site C</span></span>
    
  
5. <span data-ttu-id="d3daa-197">Экспорт пакета проектирования с сайта</span><span class="sxs-lookup"><span data-stu-id="d3daa-197">Export the design package from site C</span></span>
    
  
6. <span data-ttu-id="d3daa-198">Импорт пакета проектирования сайт B</span><span class="sxs-lookup"><span data-stu-id="d3daa-198">Import the design package to site B</span></span>
    
  
<span data-ttu-id="d3daa-p113">Какие-либо созданы при выгрузке пакет разработки также импортируются каналы устройств и их конфигурация. Однако необходимо повторно связать главных страниц для указанного устройств, каналы, так как эти сопоставления не будет настроен.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p113">Any created device channels, and their configurations, are also imported when the design package is unloaded. But, you have to re-associate master pages to specified device channels because these mappings will not be configured.</span></span>
  
    
    
<span data-ttu-id="d3daa-p114">При импорте пакета конструктора альтернативный URL-адрес CSS не задан, даже в том случае, если один был настроен на источнике экспорта. CSS-классов должны храниться во внешнем файле в коллекции главных страниц, а не в самом файл главной страницы.</span><span class="sxs-lookup"><span data-stu-id="d3daa-p114">When importing a design package, an alternate CSS URL is not set, even if one was configured on the source of export. CSS classes should be stored in an external file in the Master Page Gallery and not in the master page file itself.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="d3daa-203">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3daa-203">Additional resources</span></span>
<span data-ttu-id="d3daa-204"><a name="addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d3daa-204"></span></span>


-  [<span data-ttu-id="d3daa-205">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3daa-205">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3daa-206">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3daa-206">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d3daa-207">Новые возможности разработки сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3daa-207">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  
