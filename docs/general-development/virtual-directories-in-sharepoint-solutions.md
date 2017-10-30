---
title: "Виртуальные каталоги в решениях SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c26c4160-31be-4358-89cf-082b8a1e6a6c
ms.openlocfilehash: 93be71d76718e12439ea7d9d359639a139dfb89d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="virtual-directories-in-sharepoint-solutions"></a><span data-ttu-id="0c853-102">Виртуальные каталоги в решениях SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c853-102">Virtual directories in SharePoint solutions</span></span>
<span data-ttu-id="0c853-103">Сведения о влиянии изменения в систему виртуального каталога на создание решений фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c853-103">Learn about how changes in the virtual directory system affect how you create farm solutions in SharePoint.</span></span>
## <a name="make-your-solutions-compatible-with-the-new-ui-mode-system"></a><span data-ttu-id="0c853-104">Сделать решений совместимым с новой системы режим пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0c853-104">Make your solutions compatible with the new UI mode system</span></span>

<span data-ttu-id="0c853-105">Когда с помощью Microsoft SharePoint 2010 Software Development Kit (SDK), но разработки для SharePoint, изменяется в системе виртуального каталога, который необходимо учитывать при работе.</span><span class="sxs-lookup"><span data-stu-id="0c853-105">When you are using the Microsoft SharePoint 2010 Software Development Kit (SDK), but developing for SharePoint, there is a change in the virtual directory system that you need to consider as you work.</span></span> <span data-ttu-id="0c853-106">Изменение является побочные эффекты компонента SharePoint, которая позволяет семейства веб-сайтов в SharePoint 2010 или режиме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c853-106">The change is a side effect of the new SharePoint feature that enables a site collection to run in either SharePoint 2010 mode or SharePoint mode.</span></span> <span data-ttu-id="0c853-107">Режимы иногда называются orUI уровни совместимости версий.</span><span class="sxs-lookup"><span data-stu-id="0c853-107">The modes are sometimes called compatibility levels orUI versions.</span></span> <span data-ttu-id="0c853-108">Поиск файлов в виртуальные папки `_layouts` или `_controltemplates`, SharePoint необходимо использовать версию файлов в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ (иногда называемую кусте 15) или в соответствующем 14 кусте, в зависимости от режима семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="0c853-108">For files in the virtual folders  `_layouts` or `_controltemplates`, SharePoint needs to use the version of the files in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ (sometimes called the 15 hive) or in the corresponding 14 hive, depending on the mode of the site collection.</span></span> <span data-ttu-id="0c853-109">Добавляет SharePoint «/ 15» в виртуальном каталоге сразу после имя виртуального каталога, чтобы сообщить, что следует использовать файлы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c853-109">SharePoint adds "/15" into the virtual directory path just after the virtual directory name to signal that the SharePoint files should be used.</span></span> <span data-ttu-id="0c853-110">Отсутствие дополнительные строки указывает, следует ли использовать файлы SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="0c853-110">The absence of that extra string indicates that SharePoint 2010 files should be used.</span></span>
  
    
    
<span data-ttu-id="0c853-111">В этом новой системы влияет на вам при разработке решений SharePoint и приложения, особенно при использовании пакета SDK SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="0c853-111">This new system has implications for you as you develop SharePoint solutions and apps, particularly when you are using the SharePoint 2010 SDK.</span></span> <span data-ttu-id="0c853-112">В любой SharePoint Add-in (который выполнить только в режиме SharePoint) и в любой решение SharePoint, которые только будут использоваться в семейств веб-сайтов, на которых выполняется в режиме SharePoint, необходимо добавить «/ 15» выберите вариант все `_layouts` и `_controltemplates` виртуального пути можно создать e решения или приложения.</span><span class="sxs-lookup"><span data-stu-id="0c853-112">In any SharePoint Add-in (which only run in SharePoint mode) and in any SharePoint solution that you know is only going to be used in site collections that run in SharePoint mode, you need to add the "/15" yourself to all the  `_layouts` and `_controltemplates` virtual paths you create in your solution/app.</span></span> <span data-ttu-id="0c853-113">(если только с указанием пути ASPX-файла), даже если эта строка не отображается в любой инструкции, чтение в пакет SDK для SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="0c853-113">(unless the path is pointing to an *.aspx file), even though this string does not appear in any instructions you read in the SharePoint 2010 SDK.</span></span> <span data-ttu-id="0c853-114">Например, если пакет SDK для SharePoint 2010, этот параметр можно воспользоваться `~/_layouts/images/myimage.png`, следует использовать `~/_layouts/15/images/myimage.png` при разработке для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c853-114">For example, if the SharePoint 2010 SDK instructs you to use `~/_layouts/images/myimage.png`, you should use  `~/_layouts/15/images/myimage.png` when you are developing for SharePoint.</span></span>
  
    
    
<span data-ttu-id="0c853-p103">Если вам потребуется сделать совместимым с семейств веб-сайтов из любого из режима решения, ветвление логику для определения режима в текущем семействе сайтов и создать виртуальный путь к соответствующим образом. Свойство  [CompatibilityLevel](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.CompatibilityLevel.aspx) , которое возможности также доступны на всех клиентских объектных моделей SharePoint и интерфейс REST,  одну позицию, где код можно проверить, для режима. Класс [SPUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.aspx) также имеет несколько новых свойств для помощи в управлении уровень совместимости имеющихся. Они не доступны в клиентской объектной модели. И, наконец существует несколько элементов управления в SharePoint, которые предоставляют свойство **UIVersion**, которое кода можно также использовать для поиска текущий уровень совместимости.</span><span class="sxs-lookup"><span data-stu-id="0c853-p103">If you need to make your solution compatible with site collections of either mode, you need branching logic to determine the mode of the current site collection and construct the virtual path accordingly. The  [CompatibilityLevel](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.CompatibilityLevel.aspx) property, which is also available in all the SharePoint client object models and the REST interface, is one place where your code can check for the mode. The [SPUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.aspx) class also has several new properties to aid in managing compatibility level in your solutions. These are not available in the client object models. Finally, there are several controls in SharePoint that expose a **UIVersion** property that your code can also use to find the current compatibility level.</span></span>
  
    
    

> <span data-ttu-id="0c853-120">**Примечание:** Если файл виртуальный путь *.aspx, SharePoint автоматическое определение режим в текущем семействе сайтов и возврата файла из соответствующего куста.</span><span class="sxs-lookup"><span data-stu-id="0c853-120">**Note:** If the file in the virtual path is *.aspx, SharePoint will automatically detect the mode of the current site collection and return the file from the appropriate hive.</span></span> <span data-ttu-id="0c853-121">Поэтому необходимо вставить «/ 15» в виртуальный путь.</span><span class="sxs-lookup"><span data-stu-id="0c853-121">So you do not have to insert the "/15" into the virtual path.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="0c853-122">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0c853-122">Additional resources</span></span>
<span data-ttu-id="0c853-123"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0c853-123"></span></span>


-  [<span data-ttu-id="0c853-124">Создавайте решения фермы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c853-124">Build farm solutions in SharePoint</span></span>](build-farm-solutions-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0c853-125">Планирование развертывания решений фермы для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c853-125">Planning Deployment of Farm Solutions for SharePoint</span></span>](http://blogs.technet.com/b/mspfe/archive/2013/02/04/planning-deployment-of-farm-solutions-for-sharepoint.aspx)
    
  
-  [<span data-ttu-id="0c853-126">SPUtility properties</span><span class="sxs-lookup"><span data-stu-id="0c853-126">SPUtility properties</span></span>](http://msdn.microsoft.com/library/Properties.T:Microsoft.SharePoint.Utilities.SPUtility.aspx)
    
  

