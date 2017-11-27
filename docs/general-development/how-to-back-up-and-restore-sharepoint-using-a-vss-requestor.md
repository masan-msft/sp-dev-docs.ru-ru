---
title: "Резервное копирование и восстановление SharePoint с использованием модуля запросов VSS"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: cab5ba90-bd23-4cec-82d7-529e3f86ba88
ms.openlocfilehash: 76664d750be4e8ecf98dae4fc5aa106d2c8864e7
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="back-up-and-restore-sharepoint-using-a-vss-requestor"></a><span data-ttu-id="941f7-102">Резервное копирование и восстановление SharePoint с использованием модуля запросов VSS</span><span class="sxs-lookup"><span data-stu-id="941f7-102">Back up and restore SharePoint using a VSS requestor</span></span>

<span data-ttu-id="941f7-103">Узнайте, как резервного и восстановления с помощью запросившая сторона службы теневого копирования томов (VSS) для Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="941f7-103">Learn how to back and restore using a Volume Shadow Copy Service (VSS) requestor for Microsoft SharePoint.</span></span>

## <a name="backing-up-and-restoring-with-the-requestor"></a><span data-ttu-id="941f7-104">Резервное копирование и восстановление с запрашивающего</span><span class="sxs-lookup"><span data-stu-id="941f7-104">Backing up and restoring with the requestor</span></span>

<span data-ttu-id="941f7-105">Используйте следующую процедуру для резервного копирования и восстановления данных Microsoft SharePoint Foundation , с помощью приложения VSS requestor.</span><span class="sxs-lookup"><span data-stu-id="941f7-105">Use the following procedure to back up and restore Microsoft SharePoint Foundation data using your VSS requestor.</span></span>
  
    
    

### <a name="to-back-up-and-restore-data-by-using-your-requestor"></a><span data-ttu-id="941f7-106">Для резервного копирования и восстановления данных с помощью приложения requestor</span><span class="sxs-lookup"><span data-stu-id="941f7-106">To back up and restore data by using your requestor</span></span>


1. <span data-ttu-id="941f7-p101">Вручную запустить службу модуля записи VSS SharePoint Foundation. Запустите компонент **Администрирование**, откройте оснастку **Службы** и запустите службы **Теневое копирование томов** и **Модуль записи SharePoint 2010**.</span><span class="sxs-lookup"><span data-stu-id="941f7-p101">Manually start the SharePoint Foundation VSS Writer service. Open **Administrative Tools**, navigate to and open **Services** and start the services called **Volume Shadow Copy** and **SharePoint 2010 VSS Writer**.</span></span>
    
  
2. <span data-ttu-id="941f7-p102">Зарегистрируйте средство записи в реестре Windows, выполнив команду  `STSADM -o registerwsswriter` из системной консоли. Исполняемый файл находится в каталоге "%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN".</span><span class="sxs-lookup"><span data-stu-id="941f7-p102">Register the writer in the Windows registry by running the  `STSADM -o registerwsswriter` command from a system console. The executable is located in the %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN directory.</span></span>
    
  
3. <span data-ttu-id="941f7-111">Повторите шаги 1 и 2 на все серверах SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="941f7-111">Repeat steps 1 and 2 on all SharePoint Foundation servers.</span></span>
    
  
4. <span data-ttu-id="941f7-p103">С помощью приложения Requestor выполните резервное копирование и восстановление данных. Для создания резервной копии или восстановления из SharePoint Foundation можно использовать либо Requestor (как описано в статье  [Обзор службы теневого копирования томов (Возможно, на английском языке)](http://msdn.microsoft.com/en-us/library/aa384649%28VS.85%29.aspx)), либо служебную программу проверки BETest (из пакета  [SDK для VSS (Возможно, на английском языке)](http://www.microsoft.com/downloads/details.aspx?FamilyID=0B4F56E4-0CCC-4626-826A-ED2C4C95C871&amp;displaylang=en)).</span><span class="sxs-lookup"><span data-stu-id="941f7-p103">Use your requestor to back up and restore data. You can either use your requestor (as outlined in the  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/en-us/library/aa384649%28VS.85%29.aspx)) or the BETest test utility (available in the  [VSS SDK](http://www.microsoft.com/downloads/details.aspx?FamilyID=0B4F56E4-0CCC-4626-826A-ED2C4C95C871&amp;displaylang=en)) to back up or restore from SharePoint Foundation.</span></span> 
    
  

## <a name="security-for-running-vss"></a><span data-ttu-id="941f7-114">Безопасность при выполнении VSS</span><span class="sxs-lookup"><span data-stu-id="941f7-114">Security for Running VSS</span></span>

<span data-ttu-id="941f7-115">VSS имеет особые требования для учетных записей, выполняющих средства записи на всех конечных экземплярах серверов для резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="941f7-115">VSS has special requirements for the accounts running the writers on all targeted server instances for backup and restore</span></span>
  
    
    

- <span data-ttu-id="941f7-p104">Выполняющиеся учетные записи должны иметь разрешения для вызова в VSS. По умолчанию VSS требует, чтобы средство записи VSS входило в группу администраторов или операторов резервного копирования на конечном экземпляре сервера. Чтобы другие учетные записи могли обращаться к VSS, можно настроить раздел реестра.</span><span class="sxs-lookup"><span data-stu-id="941f7-p104">The running account must have permission to call into VSS. By default, VSS requires a VSS writer to be a member of the Administrator or Backup Operators group on the targeted server instance. You can configure a registry key to allow other accounts to have access to VSS.</span></span>
    
  
- <span data-ttu-id="941f7-119">Учетная запись должна иметь разрешения на выполнение команд **BACKUP DATABASE** и **RESTORE DATABASE** на серверах баз данных.</span><span class="sxs-lookup"><span data-stu-id="941f7-119">The account must have permission to issue **BACKUP DATABASE** and **RESTORE DATABASE** commands against the database servers.</span></span>
    
  
- <span data-ttu-id="941f7-120">Учетная запись должна иметь разрешения на открытие VDI на сервере SQL Server, где требуется, чтобы клиент был членом группы системных администраторов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="941f7-120">The account must have permission to open up VDI against SQL Server, which requires the client to be a member of the SQL Server sysadmin group.</span></span>
    
  
- <span data-ttu-id="941f7-121">Учетная запись должна выполнять запросы в представлении каталога sys.master_files в основной базе данных на сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="941f7-121">The account must be able to perform queries against the sys.master_files catalog view in the master database on the SQL server.</span></span>
    
  
<span data-ttu-id="941f7-122">Кроме того, для размещения службой таймера SharePoint Foundation (owstimer.exe) служба модуля записи должна быть запущена с учетной записью администратора пула приложений, т. е. с учетной записью "Сетевая служба" в базовой установке SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="941f7-122">Also, to be hosted by the SharePoint Foundation Timer service (owstimer.exe), the writer service must run under the administration application pool account, which is the "Network Service" account in a basic installation of SharePoint Foundation.</span></span> 
  
    
    
 <span data-ttu-id="941f7-123">**Примечание** Маловероятно, что эта учетная запись будет учетной записью администратора локального компьютера, не соответствующей требованиям для VSS, где обрабатываемая учетная запись должна выполняться как учетная запись локальной системы.</span><span class="sxs-lookup"><span data-stu-id="941f7-123">**Note** It is very unlikely that this account will be a local machine admin account, which differs from the requirement for VSS where the processing account must be running as local system.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="941f7-124">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="941f7-124">Additional resources</span></span>
<span data-ttu-id="941f7-125"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="941f7-125"></span></span>


-  [<span data-ttu-id="941f7-126">Общие сведения о SharePoint и службы теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="941f7-126">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

