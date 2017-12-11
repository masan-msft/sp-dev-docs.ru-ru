---
title: "Запрашивающие стороны VSS и SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0b2e5a4e-40f0-4ccf-a21a-7274921f2169
ms.openlocfilehash: e33fbaaaed785786e6be0abca0d691748dc0798f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="vss-requestors-and-sharepoint"></a><span data-ttu-id="def4c-102">Запрашивающие стороны VSS и SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-102">VSS requestors and SharePoint</span></span>
 <span data-ttu-id="def4c-103">**Сводка:** Сведения о работе системы запросившая сторона службы теневого копирования томов (VSS) системы с помощью Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="def4c-103">**Summary:** Learn about how the requestor system of the Volume Shadow Copy Service (VSS) system works with Microsoft SharePoint.</span></span>
<span data-ttu-id="def4c-104">Служба теневого копирования ТОМОВ в Windows Server можно использовать для создания приложений, резервное копирование и восстановление Microsoft SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="def4c-104">VSS in Windows Server can be used to create applications that back up and restore Microsoft SharePoint Foundation.</span></span> <span data-ttu-id="def4c-105">Служба теневого копирования ТОМОВ предоставляет инфраструктуру, которая позволяет программам управления хранилищами сторонних производителей, бизнес-приложениями и поставщиками оборудования для взаимодействия при создании и управлении теневые копии.</span><span class="sxs-lookup"><span data-stu-id="def4c-105">The VSS provides an infrastructure that enables third-party storage management programs, business programs, and hardware providers to cooperate in creating and managing shadow copies.</span></span> <span data-ttu-id="def4c-106">Решения, основанные на этом инфраструктуры можно использовать теневые копии (или зеркальной копии) для резервного копирования и восстановления одного или нескольких баз данных SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="def4c-106">Solutions based on this infrastructure can use the shadow copies (or mirrored copies) to back up and restore one or more SharePoint Foundation databases.</span></span>
  
    
    


## <a name="vss-requestor-system"></a><span data-ttu-id="def4c-107">Система запросившая сторона службы теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="def4c-107">VSS requestor system</span></span>

<span data-ttu-id="def4c-p102">Служба теневого копирования ТОМОВ координирует взаимодействие между источниками запросов (приложениями резервного копирования), писатели (приложений Windows SharePoint Foundation и Microsoft SQL Server) и поставщиков (системы, программного обеспечения или оборудования компонентами, создающими теневые копии). Чтобы использовать функцию VSS для резервного копирования SharePoint Foundation, программа резервного копирования должен включать запросившая сторона службы теневого копирования ТОМОВ, знает о SharePoint Foundation. Поскольку программа резервного копирования, которая предоставляется вместе с Windows Server имеет нет такого запрашивающего, организации должны использовать приложения резервного копирования сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="def4c-p102">The VSS coordinates communication among requestors (backup applications), Writers (Windows applications such as SharePoint Foundation and Microsoft SQL Server), and Providers (system, software, or hardware components that create the shadow copies). To use the VSS feature to back up SharePoint Foundation, the backup program must include a VSS requestor that is aware of SharePoint Foundation. Because the backup program that is provided with Windows Server has no such requestor, organizations must use third-party backup applications.</span></span>
  
    
    
<span data-ttu-id="def4c-p103">Чтобы обеспечить совместимость с SharePoint Foundation, приложения резервного копирования, основанные на VSS, должны удовлетворять двум основным требованиям, гарантирующим целостность и возможность восстановления теневых копий. Клиенты должны получить от своих поставщиков средств резервного копирования подтверждение, что приложения резервного копирования соответствуют требованиям совместимости с системой SharePoint Foundation, перечисленным в данном разделе.</span><span class="sxs-lookup"><span data-stu-id="def4c-p103">To be compliant with SharePoint Foundation, backup applications that are based on VSS must follow two basic requirements to ensure the integrity and recoverability of shadow copy backups. Customers should verify with their backup vendors that the backup application fulfills the compliance requirements for SharePoint Foundation listed in this topic.</span></span>
  
    
    
<span data-ttu-id="def4c-113">Ниже приведены требования системы SharePoint Foundation, которым должно удовлетворять приложение резервного копирования, создающее теневую копию, для обеспечения целостности и возможности восстановления баз данных SharePoint Foundation:</span><span class="sxs-lookup"><span data-stu-id="def4c-113">Following are the SharePoint Foundation requirements that a shadow copy backup application must follow to ensure the integrity and recoverability of SharePoint Foundation databases:</span></span> 
  
    
    

- <span data-ttu-id="def4c-114">Резервное копирование баз данных и файлов индекса поиска SharePoint Foundation должно выполняться только посредством приложения SPF-VSS Writer.</span><span class="sxs-lookup"><span data-stu-id="def4c-114">SharePoint Foundation databases and search index files must be backed up exclusively through the SPF-VSS Writer.</span></span>
    
  
- <span data-ttu-id="def4c-p104">Приложение резервного копирования должно проверять целостность резервного набора данных теневой копии. Операции восстановления в исходном местоположении должны выполняться исключительно посредством приложения SPF-VSS Writer.</span><span class="sxs-lookup"><span data-stu-id="def4c-p104">The backup application must validate the integrity of the shadow copy backup set. Restore operations to original location must be done exclusively with the SPF-VSS Writer.</span></span>
    
  

## <a name="restoring"></a><span data-ttu-id="def4c-117">Восстановление</span><span class="sxs-lookup"><span data-stu-id="def4c-117">Restoring</span></span>

<span data-ttu-id="def4c-118">Перед восстановлением должны быть выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="def4c-118">Before executing a restoration, the following conditions must be met:</span></span>
  
    
    

- <span data-ttu-id="def4c-119">Следующие службы должны быть  *запущены*  :</span><span class="sxs-lookup"><span data-stu-id="def4c-119">The following services must be  *started*  :</span></span>
    
  - <span data-ttu-id="def4c-120">Служба модуля записи VSS SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-120">SharePoint VSS Writer</span></span>
    
  
  - <span data-ttu-id="def4c-121">Теневое копирование томов</span><span class="sxs-lookup"><span data-stu-id="def4c-121">Volume Shadow Copy</span></span>
    
  
  - <span data-ttu-id="def4c-122">Отслеживание SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-122">SharePoint Tracing</span></span>
    
  
- <span data-ttu-id="def4c-123">Следующие службы должны быть  *остановлены*  :</span><span class="sxs-lookup"><span data-stu-id="def4c-123">The following services must be  *stopped*  :</span></span>
    
  - <span data-ttu-id="def4c-124">Администрирование SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-124">SharePoint Administration</span></span>
    
  
  - <span data-ttu-id="def4c-125">Поиск SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-125">SharePoint Search</span></span>
    
  
  - <span data-ttu-id="def4c-126">Таймер SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-126">SharePoint Timer</span></span>
    
  
  - <span data-ttu-id="def4c-127">Сервер поиска SharePoint (если установлен SharePoint).</span><span class="sxs-lookup"><span data-stu-id="def4c-127">SharePoint Server Search (If SharePoint Server is installed.)</span></span>
    
  
- <span data-ttu-id="def4c-128">Если восстанавливается вся ферма, службы SharePoint Foundation *и IIS*  должны быть остановлены.</span><span class="sxs-lookup"><span data-stu-id="def4c-128">If the whole farm is being restored, SharePoint Foundation *and Internet Information Server (IIS)*  must be shutdown.</span></span>
    
  
- <span data-ttu-id="def4c-129">Если восстанавливаются только выбранные веб-приложения и компоненты, веб-приложения должны быть закрыты, а компоненты не должны использоваться во время восстановления.</span><span class="sxs-lookup"><span data-stu-id="def4c-129">If only selected Web applications or other components are being restored, the Web applications must be shutdown and the components may not be in use during the restoration.</span></span>
    
  

## <a name="next-steps"></a><span data-ttu-id="def4c-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="def4c-130">Next steps</span></span>
<span data-ttu-id="def4c-131"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="def4c-131"></span></span>

<span data-ttu-id="def4c-132">Узнайте, как создавать и использовать запросов VSS для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="def4c-132">Learn how to create and use a VSS requestor for SharePoint:</span></span>
  
    
    

-  [<span data-ttu-id="def4c-133">Как: создание опросчика VSS для использования с SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-133">How to: Create a VSS requestor for use with SharePoint</span></span>](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [<span data-ttu-id="def4c-134">Как: резервное копирование и восстановление SharePoint с использованием модуля запросов VSS</span><span class="sxs-lookup"><span data-stu-id="def4c-134">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="def4c-135">Как: резервное копирование и восстановление приложения-службы поиска в SharePoint с использованием служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="def4c-135">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

## <a name="see-also"></a><span data-ttu-id="def4c-136">См. также</span><span class="sxs-lookup"><span data-stu-id="def4c-136">See also</span></span>
<span data-ttu-id="def4c-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="def4c-137"></span></span>


-  [<span data-ttu-id="def4c-138">Общие сведения о SharePoint и службы теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="def4c-138">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  
-  [<span data-ttu-id="def4c-139">Как: создание опросчика VSS для использования с SharePoint</span><span class="sxs-lookup"><span data-stu-id="def4c-139">How to: Create a VSS requestor for use with SharePoint</span></span>](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [<span data-ttu-id="def4c-140">Как: резервное копирование и восстановление SharePoint с использованием модуля запросов VSS</span><span class="sxs-lookup"><span data-stu-id="def4c-140">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="def4c-141">Как: резервное копирование и восстановление приложения-службы поиска в SharePoint с использованием служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="def4c-141">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

