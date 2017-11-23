---
title: "Новые возможности Word Automation Services для разработчиков (en)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 00d2cf8d-93b0-4aab-8e76-31a6bb2f0dcb
ms.openlocfilehash: c01450d5a61edd71ee767c6028bd94937dd5e124
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-word-automation-services-for-developers"></a><span data-ttu-id="68ca9-102">Новые возможности Word Automation Services для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="68ca9-102">What's new in Word Automation Services for developers</span></span>
<span data-ttu-id="68ca9-103">Этот раздел содержит общий обзор дополнений и усовершенствований в службы Word Automation Services для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="68ca9-103">This topic provides a high-level overview of the additions and enhancements for developers in Word Automation Services.</span></span> <span data-ttu-id="68ca9-104">В Microsoft SharePoint основной дополнение к Word Automation Services — поддержка «по запросу» файл запросов на преобразование.</span><span class="sxs-lookup"><span data-stu-id="68ca9-104">In Microsoft SharePoint the primary addition to Word Automation Services is support for "on demand" file conversion requests.</span></span> <span data-ttu-id="68ca9-105">Наиболее значительное расширение возможностей Word Automation Services добавлена поддержка использование потоков в качестве входных данных и выходные данные задания преобразования.</span><span class="sxs-lookup"><span data-stu-id="68ca9-105">The most significant enhancement to Word Automation Services is added support for using streams as input to and output from conversion jobs.</span></span>
## <a name="create-an-on-demand-file-conversion"></a><span data-ttu-id="68ca9-106">Создайте на преобразование файла запросами</span><span class="sxs-lookup"><span data-stu-id="68ca9-106">Create an on demand file conversion</span></span>
<span data-ttu-id="68ca9-107"><a name="was15CreateOnDemandConversion"> </a></span><span class="sxs-lookup"><span data-stu-id="68ca9-107"><a name="was15CreateOnDemandConversion"> </a></span></span>

<span data-ttu-id="68ca9-108">В веб-службы Word Automation Services в Microsoft SharePoint, можно создавать по запросу преобразованием файлов запрашивает сразу же обработки результатов в файл conversionthat.</span><span class="sxs-lookup"><span data-stu-id="68ca9-108">In Word Automation Services in Microsoft SharePoint you can now create on demand file conversion requests that result in file conversionthat are processed immediately.</span></span> <span data-ttu-id="68ca9-109">В SharePoint 2010 вам нужно создать задание преобразования файлов в коде и затем запустить преобразование, с помощью метода ConversionJob.Start.</span><span class="sxs-lookup"><span data-stu-id="68ca9-109">In SharePoint 2010, you would create a file conversion job in your code and then start the conversion using the ConversionJob.Start method.</span></span> <span data-ttu-id="68ca9-110">Задание преобразования нажмите Начать на основе интервала, задайте в службы Word Automation Services, как часто следует запускать задания преобразования.</span><span class="sxs-lookup"><span data-stu-id="68ca9-110">The conversion job would then start based on the interval set in Word Automation Services for how often to start conversion jobs.</span></span> <span data-ttu-id="68ca9-111">Периодичностью задания таймера SharePoint будет запустить задание преобразования.</span><span class="sxs-lookup"><span data-stu-id="68ca9-111">At the interval, the SharePoint Timer Job would start the conversion job.</span></span> <span data-ttu-id="68ca9-112">С помощью метода задания таймера на основе soonest можно начать преобразование задания равен 1 минуте.</span><span class="sxs-lookup"><span data-stu-id="68ca9-112">Using the Timer Job based method, the soonest you can start a conversion job is 1 minute.</span></span> 
  
    
    
<span data-ttu-id="68ca9-113">Теперь в службы Word Automation Services в Microsoft SharePoint, вы можете добавлена для создания запроса на преобразование файла, который обрабатывается как только вы отправить и преобразования, запускается немедленно и не зависит от задания таймера SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68ca9-113">Now, in Word Automation Services in Microsoft SharePoint, you have the added option to create a file conversion request that's processed as soon as you submit it and the conversion is started immediately and does not depend on the SharePoint Timer Job.</span></span> 
  
    
    
<span data-ttu-id="68ca9-p103">Одним из способов, учитывайте следующее различие между в очередь запросов на преобразование файла запросами и SharePoint на основе временного задания преобразования заданий  понять, в очередь запросов на преобразование файла запросами обрабатываются синхронно, тогда как задания преобразования на основе задание таймера SharePoint происходят асинхронно. Архитектура Word Automation Services была переработана для поддержки нового типа для запроса на преобразование файла запросами и существующих преобразования файлов задания таймера на основе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68ca9-p103">One way to think about the difference between on demand file conversion requests and the SharePoint Time Job-based conversion jobs is to understand that on demand file conversion requests are handled synchronously, whereas SharePoint Timer Job-based conversion jobs happen asynchronously. The Word Automation Services architecture was redesigned to support both the new kind of on demand file conversion request and the existing SharePoint Timer Job based file conversions.</span></span>
  
    
    

<span data-ttu-id="68ca9-116">**На рисунке 1. Архитектура Word Automation Services 2013**</span><span class="sxs-lookup"><span data-stu-id="68ca9-116">**Figure 1. Word Automation Services 2013 architecture**</span></span>

  
    
    

  
    
    
![Архитектура Word Automation Services 2013](../images/SPS15CON_WAS_Architecture.png)
  
    
    
<span data-ttu-id="68ca9-118">На рисунке 1, можно убедиться, что архитектура Word Automation Services поддерживается 2 отдельных очередей для преобразования: одна очередь для на запросами (Интерпретация) файла преобразования запросов и одной очереди для заданий преобразования на основе задания таймера SharePoint на запросы с запросами помещаются в интерпретации основе очереди документов, где преобразования обрабатываются немедленно.</span><span class="sxs-lookup"><span data-stu-id="68ca9-118">In figure 1, you can see that the Word Automation Services architecture maintains 2 separate queues for conversions: one queue for on demand (immediate) file conversion requests and one queue for SharePoint Timer Job-based conversion jobs on demand requests are placed in the immediate based document queue where the conversions are processed immediately.</span></span>
  
    
    
<span data-ttu-id="68ca9-p104">С другой стороны задания преобразования на основе задания таймера SharePoint, помещаются в очередь документ на основе задания таймера. Задания преобразования для этих запросов на запуск периодичностью для службы Word Automation Services. Запросов на преобразование в очереди документ на основе интерпретации всегда имеют приоритет над задания преобразования в документ на основе задание таймера очереди.</span><span class="sxs-lookup"><span data-stu-id="68ca9-p104">In contrast, the SharePoint Timer Job-based conversion jobs are placed in the Timer Job-based document queue. Conversion jobs for these requests start at the interval set for Word Automation Services. Conversion requests in the immediate-based document queue always have priority over conversion jobs in the Timer Job-based document queue.</span></span>
  
    
    

### <a name="key-points"></a><span data-ttu-id="68ca9-122">Ключевые моменты</span><span class="sxs-lookup"><span data-stu-id="68ca9-122">Key points</span></span>


- <span data-ttu-id="68ca9-123">По запросу преобразования файлов запросами-это дополнительный компонент и не замените существующее задание преобразования на основе задания таймера SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68ca9-123">An on demand file conversion request is an additional feature and doesn't replace the existing SharePoint Timer Job-based conversion job.</span></span> <span data-ttu-id="68ca9-124">Это означает, что решения, которые компилируются и выполнили в SharePoint 2010 будет продолжать скомпилировать и запустить в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68ca9-124">That means that solutions that compiled and ran in SharePoint 2010 will continue to compile and run in SharePoint.</span></span>
    
  
- <span data-ttu-id="68ca9-125">Чтобы на запросов на преобразование файла запросами только для одного файла за раз</span><span class="sxs-lookup"><span data-stu-id="68ca9-125">You can make on demand file conversion requests for only one file at a time</span></span>
    
  
- <span data-ttu-id="68ca9-p106">Word Automation Services всегда будет определять приоритеты для задания преобразования файлов запросами через задания преобразования на основании SharePoint задания таймера. Если Word Automation Services уже работает на задание преобразования файлов, который использует SharePoint задание таймера, Word Automation Services прерывать задания и переключения на работают на задание преобразования файлов запросами до его завершения. Оно будет переключитесь в работать на задание преобразования файлов на основе задание таймера SharePoint</span><span class="sxs-lookup"><span data-stu-id="68ca9-p106">Word Automation Services will always prioritize on demand file conversion jobs over conversion jobs based on the SharePoint Timer Job. If Word Automation Services is already working on a file conversion job that uses the SharePoint Timer Job, Word Automation Services will interrupt that job and switch over to work on the on demand file conversion job until it is completed. It will then switch back to work on the SharePoint Timer Job-based file conversion job</span></span>
    
  

## <a name="perform-file-conversions-on-streams"></a><span data-ttu-id="68ca9-129">Преобразования файлов потоков</span><span class="sxs-lookup"><span data-stu-id="68ca9-129">Perform file conversions on streams</span></span>
<span data-ttu-id="68ca9-130"><a name="was15PerformStreamConversion"> </a></span><span class="sxs-lookup"><span data-stu-id="68ca9-130"><a name="was15PerformStreamConversion"> </a></span></span>

<span data-ttu-id="68ca9-131">Новая функция в Word Automation Services в Microsoft SharePoint — для поддержки преобразования потоков.</span><span class="sxs-lookup"><span data-stu-id="68ca9-131">The other new feature in Word Automation Services in Microsoft SharePoint is support for converting streams.</span></span> <span data-ttu-id="68ca9-132">В SharePoint 2010, можно было только преобразовать файлы, которые были сохранены в библиотеках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68ca9-132">In SharePoint 2010, you could only convert files that were stored in SharePoint libraries.</span></span> <span data-ttu-id="68ca9-133">Теперь можно преобразовать файлы, которые хранятся вне SharePoint с использованием потоков.</span><span class="sxs-lookup"><span data-stu-id="68ca9-133">Now you can also convert files that are stored outside SharePoint using streams.</span></span>
  
    
    

### <a name="key-points"></a><span data-ttu-id="68ca9-134">Ключевые моменты</span><span class="sxs-lookup"><span data-stu-id="68ca9-134">Key points</span></span>


- <span data-ttu-id="68ca9-135">Можно использовать только потоков как входные данные при создании на задание преобразования файлов запросами</span><span class="sxs-lookup"><span data-stu-id="68ca9-135">You can only use streams as input when you're creating an on demand file conversion job</span></span>
    
  
- <span data-ttu-id="68ca9-136">Из-за описанные выше точки можно преобразовать только один поток за раз</span><span class="sxs-lookup"><span data-stu-id="68ca9-136">Because of the foregoing point, you can only convert one stream at a time</span></span>
    
  
<span data-ttu-id="68ca9-137">С добавлением в очередь запросов на преобразование файла запросами и для поддержки преобразования потоков Word Automation Services значительно улучшено для включения с повышенной сценариев для преобразования документов.</span><span class="sxs-lookup"><span data-stu-id="68ca9-137">With the addition of on demand file conversion requests and support for converting streams, Word Automation Services has been significantly enhanced to enable a greater range of document conversion scenarios.</span></span>
  
    
    

### <a name="additional-resources"></a><span data-ttu-id="68ca9-138">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="68ca9-138">Additional resources</span></span>
<span data-ttu-id="68ca9-139"><a name="was15AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="68ca9-139"><a name="was15AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="68ca9-140">Службы Word Automation Services в SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="68ca9-140">Word Automation Services in SharePoint Server 2010</span></span>](http://msdn.microsoft.com/ru-ru/library/ee558278)
    
  
-  [<span data-ttu-id="68ca9-141">Службы Word Automation Services Class библиотеки</span><span class="sxs-lookup"><span data-stu-id="68ca9-141">Word Automation Services Class Library</span></span>](http://msdn.microsoft.com/ru-ru/library/ee559408)
    
  

