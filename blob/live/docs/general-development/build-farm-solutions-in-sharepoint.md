---
title: "Создавайте решения фермы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 96c32f08-ad93-49af-b8d0-9d194a48cc79
ms.openlocfilehash: 8cc5fbc9d9b26d0048cd0e42e611ff9707847079
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="build-farm-solutions-in-sharepoint"></a><span data-ttu-id="d735f-102">Создавайте решения фермы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d735f-102">Build farm solutions in SharePoint</span></span>
<span data-ttu-id="d735f-103">Узнайте о нашей документации по разработке, упаковки и развертывания административные расширения для SharePoint с использованием решений фермы.</span><span class="sxs-lookup"><span data-stu-id="d735f-103">Get an overview of our documentation about developing, packaging, and deploying administrative extensions to SharePoint using farm solutions.</span></span>
## <a name="what-are-farm-solutions"></a><span data-ttu-id="d735f-104">Что такое решений фермы</span><span class="sxs-lookup"><span data-stu-id="d735f-104">What are farm solutions?</span></span>
<span data-ttu-id="d735f-105"><a name="WhatAreFarmSolutions"> </a></span><span class="sxs-lookup"><span data-stu-id="d735f-105"></span></span>

<span data-ttu-id="d735f-106">SharePoint имеет собственную систему для установки расширений SharePoint административным функциям, отличный от других приложений Windows и платформ.</span><span class="sxs-lookup"><span data-stu-id="d735f-106">SharePoint has its own system for installing extensions to SharePoint administrative functions that is different from other Windows applications and platforms.</span></span> <span data-ttu-id="d735f-107">Не возникает отсутствует MSI-файл или технологии ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="d735f-107">No MSI file or ClickOnce technology is involved.</span></span> <span data-ttu-id="d735f-108">Вместо этого сборки, XML и другие файлы в расширении объединены в одного файла, который вызывается пакета решения.</span><span class="sxs-lookup"><span data-stu-id="d735f-108">Instead, the assemblies, XML, and other files in the extension are bundled into a single file, which is called a solution package.</span></span> <span data-ttu-id="d735f-109">Пакет решения имеет формат на основе .cab, но расширением WSP-файл.</span><span class="sxs-lookup"><span data-stu-id="d735f-109">A solution package has a .cab-based format but a .wsp file extension.</span></span> <span data-ttu-id="d735f-110">Пакет может содержать функций SharePoint и все их дочерние компоненты Помимо определенных типов компонентов, которые не развертываются в функции.</span><span class="sxs-lookup"><span data-stu-id="d735f-110">The package can contain SharePoint Features and all their child components in addition to certain kinds of components that are not deployed in Features.</span></span> <span data-ttu-id="d735f-111">Администраторы фермы загрузить пакеты место хранения всей ферме из которой они могут быть развернуты и их возможности.</span><span class="sxs-lookup"><span data-stu-id="d735f-111">Farm administrators upload the packages to a farm-wide storage location from where they can be deployed and their Features activated.</span></span>
  
    
    
<span data-ttu-id="d735f-p102">В отличие от Надстройки SharePointрешения ферм содержит код, который развертывается на серверах SharePoint и выполняет вызовы объектной модели SharePoint server. Эти сборки всегда выполняются с уровнем полного доверия. Кроме того функции в решения ферм может иметь область по ширине семейства веб-сайтов, веб-приложения или всей фермы, в дополнение к области функции веб-сайта в Надстройки SharePoint. Эти аспекты решения ферм иногда сделать администраторов фермы идут на их установку, если они поступают из известного и надежного источника. По этой причине расширения SharePoint, которые в первую очередь для конечных пользователей необходимо разработать как Надстройки SharePoint, не решения ферм. Решения фермы можно использовать для настройки административных функций SharePoint, таких как задания таймера настраиваемых, настраиваемых Windows PowerShell командлетов и расширения центра администрирования. Дополнительные сведения о преимуществах Надстройки SharePoint и способов использования решения ферм см  [Сравнение надстроек SharePoint с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d735f-p102">Unlike SharePoint Add-ins, farm solutions contain code that is deployed to the SharePoint servers and makes calls to the SharePoint server object model. These assemblies always run with full trust. Moreover, the Features in farm solutions can have scope as wide as the site collection, web application, or whole farm, in addition to the website scope of Features in SharePoint Add-ins. These aspects of farm solutions sometimes make farm administrators reluctant to install them, unless they come from a well-known and trusted source. For this reason, SharePoint extensions that are primarily for use by end users should be developed as SharePoint Add-ins, not farm solutions. Farm solutions should be used for customizations of SharePoint administrative functions, such as custom timer jobs, custom Windows PowerShell cmdlets, and extensions of Central Administration. For more on the advantages of SharePoint Add-ins and the uses of farm solutions, see  [SharePoint Add-ins compared with SharePoint solutions](sharepoint-add-ins-compared-with-sharepoint-solutions.md).</span></span>
  
    
    

## <a name="guide-to-the-developer-documentation-for-farm-solutions"></a><span data-ttu-id="d735f-118">Руководство по документации для разработчиков для решений фермы</span><span class="sxs-lookup"><span data-stu-id="d735f-118">Guide to the developer documentation for farm solutions</span></span>
<span data-ttu-id="d735f-119"><a name="Guide"> </a></span><span class="sxs-lookup"><span data-stu-id="d735f-119"></span></span>

<span data-ttu-id="d735f-120">Разработка решений фермы была изменена мало SharePoint 2010, поэтому в этом разделе содержатся ссылки на SharePoint 2010 SDK.</span><span class="sxs-lookup"><span data-stu-id="d735f-120">Development of farm solutions has changed very little since SharePoint 2010, so this section contains links to the SharePoint 2010 SDK.</span></span> <span data-ttu-id="d735f-121">Чтобы избежать путаницы, помнить следующее все время при использовании пакета SDK SharePoint 2010 для разработки с помощью SharePoint:</span><span class="sxs-lookup"><span data-stu-id="d735f-121">To avoid confusion, keep the following points in mind at all times when using the SharePoint 2010 SDK to develop against SharePoint:</span></span>
  
    
    

- <span data-ttu-id="d735f-122">Вы увидите много ссылок на «изолированных решений», в пакет SDK для SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="d735f-122">You will see many references to "sandboxed solutions" in the SharePoint 2010 SDK.</span></span> <span data-ttu-id="d735f-123">Изолированные решения с помощью пользовательского кода не поддерживаются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d735f-123">Sandboxed solutions with custom code are deprecated in SharePoint.</span></span> <span data-ttu-id="d735f-124">изолированные решения «без кода» еще действителен.</span><span class="sxs-lookup"><span data-stu-id="d735f-124">"no code" sandboxed solutions are still viable.</span></span>
    
  
- <span data-ttu-id="d735f-p105">Мы рекомендуем использовать этот решения ферм в первую очередь для административные расширения не были сохранены в SharePoint 2010. Таким образом многие из этих примеров и другую документацию Пакет SDK для SharePoint 2010 может быть о расширениях конечных пользователей, развернутые в виде решения ферм.</span><span class="sxs-lookup"><span data-stu-id="d735f-p105">Our recommendation that farm solutions be used primarily for administrative extensions did not apply in SharePoint 2010. Therefore, many of the samples and other documentation in the SharePoint 2010 SDK may be about end-user extensions that are deployed as farm solutions.</span></span>
    
  
- <span data-ttu-id="d735f-127">Термины «на сервере» или «код сервера» в SharePoint 2010 SDK обратитесь к код, вызывающий серверной объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d735f-127">The terms "server-side" or "server code" in the SharePoint 2010 SDK refer to code that calls the SharePoint server object model.</span></span> <span data-ttu-id="d735f-128">Выполните эти термины *не* ссылаться на код, выполняющийся на удаленных веб-серверах (то есть, веб-серверы внешними по отношению к ферме SharePoint).</span><span class="sxs-lookup"><span data-stu-id="d735f-128">These terms do  *not*  refer to code that runs on remote web servers (that is, web servers external to the SharePoint farm).</span></span> <span data-ttu-id="d735f-129">Пример кода, вызывающего SharePoint из удаленного веб-сервера, в SharePoint 2010 и SharePoint, всегда использует один из *клиентских* объектных моделей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d735f-129">Code that calls SharePoint from remote web servers, in both SharePoint 2010 and SharePoint, always uses one of the SharePoint *client*  object models.</span></span> <span data-ttu-id="d735f-130">В пакет SDK для SharePoint 2010 такой код будет называемое «со стороны клиента» или «код клиента».</span><span class="sxs-lookup"><span data-stu-id="d735f-130">In the SharePoint 2010 SDK, such code would be called "client-side" or "client code."</span></span>
    
  
- <span data-ttu-id="d735f-131">Сборки в решении фермы в SharePoint 2010 может быть развернуты с помощью политик безопасности пользовательского доступа (CAS).</span><span class="sxs-lookup"><span data-stu-id="d735f-131">The assemblies in a farm solution in SharePoint 2010 could be deployed with Custom Access Security (CAS) policies.</span></span> <span data-ttu-id="d735f-132">Такие политики игнорируются в SharePoint; все сборки в решениях фермы в SharePoint выполняются с уровнем полного доверия.</span><span class="sxs-lookup"><span data-stu-id="d735f-132">Such policies are ignored in SharePoint; all assemblies in farm solutions in SharePoint run with full trust.</span></span>
    
  

### <a name="packaging-and-deployment"></a><span data-ttu-id="d735f-133">Упаковка и развертывание</span><span class="sxs-lookup"><span data-stu-id="d735f-133">Packaging and deployment</span></span>

<span data-ttu-id="d735f-p108">Основы упаковки, установка, обновление и локализация решения ферм описаны в  [Обзор решений](http://msdn.microsoft.com/library/1983cab9-4b29-494a-a62a-0f8e83908744%28Office.15%29.aspx) и узел [Решения для фермы](http://msdn.microsoft.com/library/845f7524-b9ff-412b-aa29-3afacda91100%28Office.15%29.aspx). Разработка для определенного компонентов SharePoint для включения в решение фермы объясняется в соответствующие узлы Пакет SDK для SharePoint 2010. Большая часть компонентов в решение фермы следует инкапсулированную в настраиваемых компонентов SharePoint. Сведения о проектировании и создании функции можно узле  [Работа с компонентами](http://msdn.microsoft.com/library/ce5f5ce5-1429-439e-9261-2c4ba9788cc1%28Office.15%29.aspx)Пакет SDK для SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="d735f-p108">The basics of packaging, installing, updating, and localizing farm solutions are explained in  [Solutions Overview](http://msdn.microsoft.com/library/1983cab9-4b29-494a-a62a-0f8e83908744%28Office.15%29.aspx) and the node [Farm Solutions in SharePoint 2010](http://msdn.microsoft.com/library/845f7524-b9ff-412b-aa29-3afacda91100%28Office.15%29.aspx). Development of particular SharePoint components for inclusion in a farm solution is explained in the relevant nodes of SharePoint 2010 SDK. Most of the components in a farm solution should be encapsulated in one or more custom SharePoint Features. For information about designing and creating Features, see the  [Working with Features](http://msdn.microsoft.com/library/ce5f5ce5-1429-439e-9261-2c4ba9788cc1%28Office.15%29.aspx) node of the SharePoint 2010 SDK.</span></span>
  
    
    

### <a name="administrative-extensions"></a><span data-ttu-id="d735f-138">Административные расширения</span><span class="sxs-lookup"><span data-stu-id="d735f-138">Administrative extensions</span></span>

<span data-ttu-id="d735f-p109">Руководство по расширение административных функций в ферме SharePoint  в узле  [Администрирование Windows SharePoint Services](http://msdn.microsoft.com/library/cdcc1b8a-4144-446f-b471-03d4a754a8ab%28Office.15%29.aspx)Пакет SDK для SharePoint 2010. Там можно найти пояснения о расширении центра администрирования, создания настраиваемых Windows PowerShell командлеты, настройка обновления и миграции, настройка резервных копий и настройки ведения журнала событий SharePoint. Один раздел описывается настройка фермы SharePoint работоспособность и производительность, измерение системы. Инструкции по созданию настраиваемого задания таймера в разделе  [Практическое руководство. Запуск кода на всех веб-серверах](http://msdn.microsoft.com/library/1bbb11b4-a342-4bed-9e7a-b8b13edd0ccc%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d735f-p109">Guidance about extending the administrative functions in a SharePoint farm is in the  [Windows SharePoint Services Administration](http://msdn.microsoft.com/library/cdcc1b8a-4144-446f-b471-03d4a754a8ab%28Office.15%29.aspx) node of the SharePoint 2010 SDK. There you can find explanations about extending Central Administration, creating custom Windows PowerShell cmdlets, customizing upgrades and migration, customizing backups, and customizing SharePoint event logging. One section explains how to customize the SharePoint farm health and performance measuring system. For instructions about creating a custom timer job, see [How to: Run Code on All Web Servers](http://msdn.microsoft.com/library/1bbb11b4-a342-4bed-9e7a-b8b13edd0ccc%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="d735f-143">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="d735f-143">In this section</span></span>
<span data-ttu-id="d735f-144"><a name="Guide"> </a></span><span class="sxs-lookup"><span data-stu-id="d735f-144"></span></span>

<span data-ttu-id="d735f-145">В этом разделе описываются способы, в котором изменен разработки решений SharePoint  *имеет*  .</span><span class="sxs-lookup"><span data-stu-id="d735f-145">The topics in this section describe the ways in which development of SharePoint solutions  *has*  changed.</span></span>
  
    
    

-  [<span data-ttu-id="d735f-146">Как: Настройка типа поля, с использованием обработки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="d735f-146">How to: Customize a field type using client-side rendering</span></span>](how-to-customize-a-field-type-using-client-side-rendering.md)
    
  
-  [<span data-ttu-id="d735f-147">URL-адреса и маркеры в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d735f-147">URLs and tokens in SharePoint</span></span>](urls-and-tokens-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d735f-148">Виртуальные каталоги в решениях SharePoint</span><span class="sxs-lookup"><span data-stu-id="d735f-148">Virtual directories in SharePoint solutions</span></span>](virtual-directories-in-sharepoint-solutions.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="d735f-149">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d735f-149">Additional resources</span></span>
<span data-ttu-id="d735f-150"><a name="SP15buildfarm_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d735f-150"></span></span>


-  [<span data-ttu-id="d735f-151">Модели программирования в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d735f-151">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  

