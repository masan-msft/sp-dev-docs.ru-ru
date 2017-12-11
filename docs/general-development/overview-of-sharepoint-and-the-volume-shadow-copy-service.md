---
title: "Обзор SharePoint и службы теневого копирования томов"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d1cb6653-bfc0-4af2-b221-d7d30cb40d84
ms.openlocfilehash: 16ba81e41273df0243063aeae3d80030b718fa61
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-sharepoint-and-the-volume-shadow-copy-service"></a><span data-ttu-id="72167-102">Обзор SharePoint и службы теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="72167-102">Overview of SharePoint and the Volume Shadow Copy Service</span></span>
 <span data-ttu-id="72167-103">**Сводка:** Сведения об интерфейсе Microsoft SharePoint для службы теневого копирования томов (VSS).</span><span class="sxs-lookup"><span data-stu-id="72167-103">**Summary:** Learn about the Microsoft SharePoint interface to the Volume Shadow Copy Service (VSS).</span></span>
<span data-ttu-id="72167-104">Для резервного копирования поставщиков тома теневой копии Service (VSS) упрощает резервное копирование Microsoft server решений с помощью централизованного API.</span><span class="sxs-lookup"><span data-stu-id="72167-104">For backup vendors, the Volume Shadow Copy Service (VSS) simplifies backing up Microsoft server solutions by using a centralized API.</span></span> <span data-ttu-id="72167-105">Microsoft SharePoint Foundation включает в себя ссылочной модуля записи VSS (в дальнейшем, называемое «SPF-VSS Writer»), которая интегрируется с платформой резервного копирования Windows служба теневого копирования ТОМОВ Включение приложений резервного копирования для резервного копирования и восстановления данных SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="72167-105">Microsoft SharePoint Foundation includes a referential VSS writer (hereafter, called "the SPF-VSS Writer") that integrates with the Windows VSS backup framework, enabling backup applications to back up and restore SharePoint Foundation data.</span></span> <span data-ttu-id="72167-106">Он поддерживает аварийное перезаписи сценария для всей фермы (включенные индекс поиска).</span><span class="sxs-lookup"><span data-stu-id="72167-106">It supports a catastrophic overwrite scenario for the entire farm (search index included).</span></span> <span data-ttu-id="72167-107">На восстановление он подключается баз данных, а также сведения об сопоставлений.</span><span class="sxs-lookup"><span data-stu-id="72167-107">On recovery, it hooks up databases and synchronizes site mappings.</span></span>
  
    
    


## <a name="design-of-the-system"></a><span data-ttu-id="72167-108">Проектирование системы</span><span class="sxs-lookup"><span data-stu-id="72167-108">Design of the System</span></span>

<span data-ttu-id="72167-109">На следующем рисунке показаны основные компоненты системы: Microsoft Windows Server и службы теневого копирования томов, SharePoint Foundation (и записи SPF-VSS для Windows Server теневого копирования тома) и приложение стороннего (или настраиваемого) резервного копирования и восстановления (включая запрашивающего и поставщика).</span><span class="sxs-lookup"><span data-stu-id="72167-109">The following figure shows the main components in the system: Microsoft Windows Server (and the Volume Shadow Copy Service), SharePoint Foundation (and the SPF-VSS Writer for the Windows Server Volume Shadow Copy Service), and the third-party (or custom) backup/restore application (including the requestor and the provider).</span></span>
  
    
    

  
    
    
![Отношения между SharePoint и VSS](../images/77a290e8-e4aa-4c54-b1ec-3d74bf3962b6.gif)
  
    
    
<span data-ttu-id="72167-p102">VSS взаимодействует с файловой системой Windows Server и драйвера запоминающего устройства через стороннего (или настраиваемого) поставщика. Поставщик оборудования необходимо определить, где создается теневая копия. VSS абстрагирует конкретной аппаратной теневой копии, поэтому приложение резервного копирования и восстановления можно получить доступ к теневой копии единообразную не зная деталей оборудования.</span><span class="sxs-lookup"><span data-stu-id="72167-p102">The VSS communicates with the Windows Server file system and with the mass storage device driver through a third-party (or custom) provider. The hardware provider must determine where the shadow copy is created. The VSS abstracts the hardware-specific shadow copy so the backup/restore application can access the shadow copy in a uniform manner without knowing the hardware implementation details.</span></span> 
  
    
    
<span data-ttu-id="72167-p103">Хранилище SharePoint Foundation является компонентом SharePoint Foundation и обращается к SharePoint Foundation группы хранения файловой системой Windows Server. В файловой системе каждая группа хранения SharePoint Foundation содержит конфигурации, содержимое, сторонним базам данных, зарегистрированные в файлы индекса поиска и базы данных конфигурации и базы данных поиска. Также включены все службы построены на SharePoint Foundation платформу приложения службы.</span><span class="sxs-lookup"><span data-stu-id="72167-p103">The SharePoint Foundation store is a component of SharePoint Foundation and accesses SharePoint Foundation storage groups through the Windows Server file system. Within the file system, each SharePoint Foundation storage group includes configuration, content, Search databases, and any third-party databases registered in the configuration database and search index files. Also included are any services built on the SharePoint Foundation Service Application Framework.</span></span> 
  
    
    
<span data-ttu-id="72167-p104">Чтобы обеспечить поддержку VSS, SharePoint Foundation включает в себя записи SPF-VSS. Модуль записи SPF-VSS координирует в хранилище SharePoint Foundation (действующие от имени запрашивающей стороны) и отключить перед его резервное копирование группы хранения и Чтобы разморозить и подключить группу хранения после резервного копирования завершена.</span><span class="sxs-lookup"><span data-stu-id="72167-p104">To support the VSS, SharePoint Foundation includes the SPF-VSS Writer. The SPF-VSS Writer coordinates with the SharePoint Foundation store (operating on behalf of the requestor) to freeze and dismount the storage group before backing it up, and then to unfreeze and mount the storage group after the backup is complete.</span></span>
  
    
    
<span data-ttu-id="72167-119">Во время восстановления резервное копирование и восстановление приложения указывает, что модуль записи SPF-VSS для координации с хранилищем SharePoint Foundation (действующие от имени запрашивающего) отключить группы хранения и файлы базы данных подключить группу хранения.</span><span class="sxs-lookup"><span data-stu-id="72167-119">During a recovery, the backup/restore application instructs the SPF-VSS Writer to coordinate with the SharePoint Foundation store (operating on behalf of the requestor) to dismount the storage group, replace the database files, and mount the storage group.</span></span>
  
> [!NOTE]
> <span data-ttu-id="72167-120">Важные сведения о восстановлений в разделе «Восстановление» в [опросчики VSS и SharePoint](vss-requestors-and-sharepoint.md) .</span><span class="sxs-lookup"><span data-stu-id="72167-120">See "Restoring" in  [VSS requestors and SharePoint](vss-requestors-and-sharepoint.md) for important information about restorations.</span></span>
  
    
    

<span data-ttu-id="72167-p105">Запрашивающая сторона является приложением стороннего (или настраиваемого) предназначен для использования VSS для правильной резервное копирование и восстановление данных SharePoint Foundation . Запрашивающая сторона взаимодействует со службой VSS для получения информации о SharePoint Foundation, команда создания теневых копий и доступа к данным для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="72167-p105">A requestor is a third-party (or custom) application designed to use the VSS to properly back up and restore SharePoint Foundation data. The requestor communicates with the VSS to obtain information about SharePoint Foundation, command the creation of shadow copies, and gain access to the data for backup.</span></span> 
  
    
    
<span data-ttu-id="72167-p106">При восстановлении, запрашивающая сторона также взаимодействует с VSS для подготовки системы к операции восстановления, а затем поместить данные обратно на запоминающее устройство. Программа архивации/восстановления также отвечает за работу с сервером Windows для чтения и записи данных на носителе архива, ли архивировать ленты, сети хранения данных или другой носитель данных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="72167-p106">When restoring, the requestor also communicates with the VSS to prepare the system for the restore operation, and then to put the data back onto the mass storage device. The backup/restore application is also responsible for working with Windows Server to read data from and write data to the backup storage media, whether a tape archive, a storage area network, or other backup medium.</span></span> 
  
    
    
<span data-ttu-id="72167-125">Сведения, необходимые для успешного выполнения резервного копирования операций и восстановления между SharePoint Foundation, VSS и приложений резервного копирования и восстановления, передается как часть метаданных модуля записи SPF VSS.</span><span class="sxs-lookup"><span data-stu-id="72167-125">Information needed to successfully complete backup and restore operations among SharePoint Foundation, the VSS, and the backup/restore application is transferred as part of the SPF-VSS Writer metadata.</span></span>
  
    
    
<span data-ttu-id="72167-126">Ниже приведен высокоуровневый последовательность событий при выполнении операций резервного копирования или восстановления.</span><span class="sxs-lookup"><span data-stu-id="72167-126">The following is the high-level sequence of events during backup or restore operations:</span></span>
  
    
    

  
    
    

1. <span data-ttu-id="72167-127">Резервной копии программы (или агент) запускает запланированное задание.</span><span class="sxs-lookup"><span data-stu-id="72167-127">The backup program (or agent) runs a scheduled job.</span></span> 
    
  
2. <span data-ttu-id="72167-128">Запросчик службы VSS в программе резервного копирования/восстановления отправляет команду VSS вступили теневую копию выбранных SharePoint Foundation группы хранения.</span><span class="sxs-lookup"><span data-stu-id="72167-128">The VSS requestor in the backup/restore application sends a command to the VSS to take a shadow copy of the selected SharePoint Foundation storage groups.</span></span> 
    
  
3. <span data-ttu-id="72167-p107">VSS взаимодействует с записи SPF-VSS для подготовки моментальной резервной копии. SharePoint Foundation запрещает административных действий для группы хранения, проверяет зависимости тома и приостанавливает все операции записи в базу данных и файлы журнала транзакций, предоставляя доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="72167-p107">The VSS communicates with the SPF-VSS Writer to prepare for a snapshot backup. SharePoint Foundation prohibits administrative actions against the storage group, checks volume dependencies, and suspends all write operations to database and transaction log files while allowing read-only access.</span></span> 
    
  
4. <span data-ttu-id="72167-131">VSS взаимодействует с соответствующим поставщиком хранилища для создания теневой копии тома хранилища, содержащего группу хранения SharePoint Foundation .</span><span class="sxs-lookup"><span data-stu-id="72167-131">The VSS communicates with the appropriate storage provider to create a shadow copy of the storage volume that contains the SharePoint Foundation storage group.</span></span> 
    
  
5. <span data-ttu-id="72167-132">VSS освобождает SharePoint Foundation , чтобы вернуться в обычный режим работы.</span><span class="sxs-lookup"><span data-stu-id="72167-132">The VSS releases SharePoint Foundation to resume ordinary operations.</span></span>
    
  
6. <span data-ttu-id="72167-p108">Запросчик службы VSS проверяет целостность резервной копии до передачи сигналов резервное копирование выполнено успешно. SharePoint Foundation регистрирует время последнего резервного копирования базы данных.</span><span class="sxs-lookup"><span data-stu-id="72167-p108">The VSS requestor verifies the integrity of the backup set prior to signaling that the backup succeeded. SharePoint Foundation records the time of the last backup for the database.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="72167-135">См. также</span><span class="sxs-lookup"><span data-stu-id="72167-135">See also</span></span>
<span data-ttu-id="72167-136"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="72167-136"></span></span>


-  [<span data-ttu-id="72167-137">Модуль записи SharePoint VSS</span><span class="sxs-lookup"><span data-stu-id="72167-137">SharePoint VSS Writer</span></span>](sharepoint-vss-writer.md)
    
  
-  [<span data-ttu-id="72167-138">Опросчики VSS и SharePoint</span><span class="sxs-lookup"><span data-stu-id="72167-138">VSS requestors and SharePoint</span></span>](vss-requestors-and-sharepoint.md)
    
  
-  [<span data-ttu-id="72167-139">Как: создание опросчика VSS для использования с SharePoint</span><span class="sxs-lookup"><span data-stu-id="72167-139">How to: Create a VSS requestor for use with SharePoint</span></span>](how-to-create-a-vss-requestor-for-use-with-sharepoint.md)
    
  
-  [<span data-ttu-id="72167-140">Как: резервное копирование и восстановление SharePoint с использованием модуля запросов VSS</span><span class="sxs-lookup"><span data-stu-id="72167-140">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="72167-141">Как: резервное копирование и восстановление приложения-службы поиска в SharePoint с использованием служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="72167-141">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  
-  [<span data-ttu-id="72167-142">Starting and Configuring the WSS Writer Service</span><span class="sxs-lookup"><span data-stu-id="72167-142">Starting and Configuring the WSS Writer Service</span></span>](http://msdn.microsoft.com/library/c9243dd6-e61e-4783-9fef-48d0122f1c09.aspx)
    
  
-  [<span data-ttu-id="72167-143">Служба теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="72167-143">Volume Shadow Copy Service</span></span>](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx)
    
  
-  [<span data-ttu-id="72167-144">Тома теневой копии службы Технический справочник</span><span class="sxs-lookup"><span data-stu-id="72167-144">Volume Shadow Copy Service Technical Reference</span></span>](http://msdn.microsoft.com/en-us/library/windows/desktop/aa384648%28v=vs.85%29.aspx)
    
  

