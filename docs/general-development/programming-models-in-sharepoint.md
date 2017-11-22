---
title: "Модели программирования в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 061985ec-6129-4e91-991b-a72488ce1d34
ms.openlocfilehash: cce12394144f3ca00ec5b0d3efdd69918c0fdf38
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="programming-models-in-sharepoint"></a><span data-ttu-id="70eca-102">Модели программирования в SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-102">Programming models in SharePoint</span></span>

<span data-ttu-id="70eca-p101">Вы можете создавать приложения для платформы SharePoint разными способами. Приложения можно разделить на следующие группы в зависимости от средств, используемых для их создания, моделей программирования, методов упаковки и развертывания, а также устройств, на которых они работают.</span><span class="sxs-lookup"><span data-stu-id="70eca-p101">You can develop applications for the SharePoint platform in many ways. These applications can be usefully categorized into the following groups based on the tools used to create them, the programming models used to develop them, the methods by which they are packaged and deployed, the methods by which they are marketed, and the devices on which they run.</span></span>
  
    
    


- <span data-ttu-id="70eca-105">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-105">SharePoint Add-ins</span></span>
    
  
- <span data-ttu-id="70eca-106">Сайты публикации SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-106">SharePoint publishing sites</span></span>
    
  
- <span data-ttu-id="70eca-107">Решения фермы SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-107">SharePoint farm solutions</span></span>
    
  
- <span data-ttu-id="70eca-108">Мобильные надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-108">Mobile add-ins for SharePoint</span></span>
    
  
- <span data-ttu-id="70eca-109">Повторно используемые компоненты для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-109">Reusable components for SharePoint</span></span>
    
  
<span data-ttu-id="70eca-p102">Эти категории  *не*  взаимоисключающие. Например, сайт публикации можно создать как Надстройка SharePoint. В следующих разделах описываются эти категории и представлены сведения о документации для каждой из них.</span><span class="sxs-lookup"><span data-stu-id="70eca-p102">These categories are  *not*  mutually exclusive. For example, you can develop a publishing site as an SharePoint Add-in. The following sections define these categories and guide you to the documentation for each.</span></span>
## <a name="add-ins-for-sharepoint"></a><span data-ttu-id="70eca-113">Надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-113">Add-ins for SharePoint</span></span>
<span data-ttu-id="70eca-114"><a name="Apps"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-114"></span></span>

<span data-ttu-id="70eca-p103">Надстройка SharePoint аналогично надстройкам на мобильном устройстве. Это решение для автономной работы, которое выполняет относительно небольшое количество связанных задач, легко устанавливается и удаляется без ошибок. Пользователи могут найти и скачать Надстройки SharePoint из магазина надстроек SharePoint или из корпоративного каталога надстроек своей организации. Надстройка SharePoint может содержать классические компоненты SharePoint, такие как списки, настраиваемые страницы веб-сайта, веб-части, рабочие процессы и типы контента. Но Надстройка SharePoint также может предоставлять доступ к удаленному веб-приложению и удаленным данным в SharePoint. Кроме того, в Надстройка SharePoint могут использоваться компоненты SharePoint и удаленные компоненты. Надстройки SharePoint  это очень надежные приложения, их настраиваемая логика всегда перемещается "вверх" в облако или "вниз" на клиентские компьютеры. Они никогда не выполняются на серверах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="70eca-p103">A SharePoint Add-in is similar to an add-in on a mobile device. It is a stand-alone productivity solution that does a small number of related tasks, installs easily, and uninstalls cleanly. Users can discover and download SharePoint Add-ins from a public SharePoint add-in store or from their organization's corporate add-in catalog. A SharePoint Add-in can include classic SharePoint components such as lists, custom website pages, Web Parts, workflows, and content types. But an SharePoint Add-in can also surface a remote web application and remote data in SharePoint. A SharePoint Add-in can also include both SharePoint and remote components. SharePoint Add-ins are very safe applications whose custom logic is always shifted "up" to the cloud or "down" to the client computers. It never runs on the SharePoint servers.</span></span>
  
    
    
<span data-ttu-id="70eca-123">Общие сведения о Модель для надстроек SharePoint см. в статье  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx). Дополнительные сведения см. в статьях  [Сравнение надстроек SharePoint с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md) и [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-123">For an introduction to the model for SharePoint Add-ins, see  [SharePoint Add-ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx). For more information, see  [SharePoint Add-ins compared with SharePoint solutions](sharepoint-add-ins-compared-with-sharepoint-solutions.md), and  [Choose the right API set in SharePoint](choose-the-right-api-set-in-sharepoint.md).</span></span>
  
    
    

## <a name="sharepoint-publishing-sites"></a><span data-ttu-id="70eca-124">Сайты публикации SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-124">SharePoint publishing sites</span></span>
<span data-ttu-id="70eca-125"><a name="ECM"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-125"></span></span>

<span data-ttu-id="70eca-p104">Сайты публикации SharePoint предоставляют удобные возможности публикации контента с высоким уровнем поддержки и соблюдения требований. Они также обеспечивают управление документами, записями, таксономией и типами контента. Дополнительные сведения см. в статье  [Создание сайтов для SharePoint](build-sites-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-p104">SharePoint publishing sites provide large-scale content publishing with a high degree of maintainability and regulation compliance. They also provide management of documents, records, taxonomy, and content types. For more information, see  [Build sites for SharePoint](build-sites-for-sharepoint.md).</span></span>
  
    
    

## <a name="sharepoint-farm-solutions"></a><span data-ttu-id="70eca-129">Решения фермы SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-129">SharePoint farm solutions</span></span>
<span data-ttu-id="70eca-130"><a name="Solutions"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-130"></span></span>

<span data-ttu-id="70eca-p105">решения ферм SharePoint  это доверенные расширения SharePoint, настраиваемая логика которых вызывает серверную объектную модель SharePoint и выполняется с полным доверием на серверах SharePoint. Эти решения, в основном, предназначены для специальных расширений администрирования SharePoint, таких как задания таймера, настраиваемые команды Windows PowerShell и расширения центра администрирования. Решения фермы распространяются как пакеты решений SharePoint. Администраторы фермы загружают их в общее хранилище, из которого их можно развернуть. Компоненты решения ферм может работать на уровне фермы, веб-приложения, семейства веб-сайтов или веб-сайта. Дополнительные сведения см. в статье  [Создавайте решения фермы в SharePoint](build-farm-solutions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-p105">SharePoint farm solutions are trusted SharePoint extensions whose custom logic calls the SharePoint server object model and runs with full trust on the SharePoint servers. These solutions are primarily for custom administrative extensions of SharePoint, such as timer jobs, custom Windows PowerShell commands, and extensions of Central Administration. Farm solutions are distributed as SharePoint solution packages that farm administrators upload to a farm-wide storage location from which they can be deployed. Components in farm solutions can have farm, web application, site collection, or website scope. For more information, see  [Build farm solutions in SharePoint](build-farm-solutions-in-sharepoint.md).</span></span>
  
    
    

## <a name="mobile-add-ins-for-sharepoint"></a><span data-ttu-id="70eca-136">Мобильные надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-136">Mobile add-ins for SharePoint</span></span>
<span data-ttu-id="70eca-137"><a name="Mobile"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-137"></span></span>

<span data-ttu-id="70eca-p106">Приложения для Windows Phone и приложения на базе сторонних мобильных платформ могут получать доступ к веб-сайтам и данным SharePoint. Средства для создания приложений Windows Phone, которые взаимодействуют с SharePoint, доступны для установки в Visual Studio 2010 и Visual Studio 2012. Управляемый API клиента SharePoint доступен только для устройств с Windows Phone. Мобильные устройства, в том числе сторонних производителей, также могут получить доступ к данным SharePoint через конечные точки SharePoint REST или OData. Дополнительные сведения см. в статье  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-p106">Windows Phone apps, and apps built on non-Microsoft mobile platforms, can access SharePoint websites and data. Tools for building Windows Phone apps that interact with SharePoint are available for installation on Visual Studio 2010 and Visual Studio 2012. A SharePoint client managed API just for use on Windows Phone devices is available. Mobile devices, including non-Microsoft devices, can also access SharePoint data through SharePoint REST/OData endpoints. For more information, see  [Build Windows Phone apps that access SharePoint](build-windows-phone-apps-that-access-sharepoint.md).</span></span>
  
    
    

## <a name="reusable-components-for-sharepoint"></a><span data-ttu-id="70eca-143">Повторно используемые компоненты для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-143">Reusable components for SharePoint</span></span>
<span data-ttu-id="70eca-144"><a name="Reuse"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-144"></span></span>

<span data-ttu-id="70eca-p107">Платформа SharePoint и Visual Studio 2012 обеспечивают инкапсуляцию и повторное использование элементов приложения, в том числе элементов, созданных с помощью кода, скриптов и XML-разметки. Дополнительные сведения см. в статье  [Создание повторно используемых компонентов для SharePoint](build-reusable-components-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-p107">The SharePoint platform and Visual Studio 2012 enable encapsulation and reuse of application elements, including elements created with code, script, and XML markup. For more information, see  [Build reusable components for SharePoint](build-reusable-components-for-sharepoint.md).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="70eca-147">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="70eca-147">In this section</span></span>
<span data-ttu-id="70eca-148"><a name="Reuse"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-148"></span></span>


-  [<span data-ttu-id="70eca-149">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-149">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="70eca-150">Создавайте решения фермы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-150">Build farm solutions in SharePoint</span></span>](build-farm-solutions-in-sharepoint.md)
    
  
-  [<span data-ttu-id="70eca-151">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-151">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="70eca-152">Создание повторно используемых компонентов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-152">Build reusable components for SharePoint</span></span>](build-reusable-components-for-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="70eca-153">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="70eca-153">Additional resources</span></span>
<span data-ttu-id="70eca-154"><a name="SP15devinSP_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="70eca-154"></span></span>


-  [<span data-ttu-id="70eca-155">Настройка общей среды разработки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-155">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [<span data-ttu-id="70eca-156">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-156">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="70eca-157">Специальные возможности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="70eca-157">Accessibility in SharePoint</span></span>](accessibility-in-sharepoint.md)
    
  
