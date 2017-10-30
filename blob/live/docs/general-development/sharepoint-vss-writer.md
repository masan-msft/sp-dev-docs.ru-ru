---
title: "Служба модуля записи VSS SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f83577e4-ebb8-44e5-8dec-a3ca5878b7fd
ms.openlocfilehash: 017a84bf57af7bf675a3825cb3a8a3dd2a9076fa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-vss-writer"></a><span data-ttu-id="e2c34-102">Служба модуля записи VSS SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2c34-102">SharePoint VSS Writer</span></span>
 <span data-ttu-id="e2c34-103">**Сводка:** Сведения о характеристики и функции модуля записи службы теневого копирования томов (VSS) для Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e2c34-103">**Summary:** Learn about the characteristics and features of the Volume Shadow Copy Service (VSS) writer for Microsoft SharePoint.</span></span>
<span data-ttu-id="e2c34-104">Служба теневого копирования ТОМОВ, включенные в состав Windows Server — это инфраструктуры, которая предоставляет возможности встроенных теневой копии.</span><span class="sxs-lookup"><span data-stu-id="e2c34-104">The VSS included with Windows Server is the infrastructure that provides built-in shadow copy capabilities.</span></span> <span data-ttu-id="e2c34-105">Теневые копии, созданные с VSS дополнить администратор хранилища ленту архивирования решения для резервного копирования, предоставляя высоким качеством копий момент времени, которые можно создавать и легко восстановить и эффективно, тем самым помогая упростить ряд аспектов хранения и Управление данными.</span><span class="sxs-lookup"><span data-stu-id="e2c34-105">Shadow copies created by VSS augment the storage administrator's tape backup archival solutions, providing high fidelity point-in-time copies that can be created and restored easily and effectively, thereby helping to simplify several aspects of storage and data management.</span></span> <span data-ttu-id="e2c34-106">Microsoft SharePoint Foundation используется служба теневого копирования ТОМОВ для упрощения резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="e2c34-106">Microsoft SharePoint Foundation uses VSS to simplify backup and restore operations.</span></span> 
  
    
    


## <a name="characteristics-of-the-system"></a><span data-ttu-id="e2c34-107">Характеристики системы</span><span class="sxs-lookup"><span data-stu-id="e2c34-107">Characteristics of the System</span></span>

<span data-ttu-id="e2c34-108">Ниже приведены компоненты решения VSS SharePoint Foundation и характеристики:</span><span class="sxs-lookup"><span data-stu-id="e2c34-108">Following are the SharePoint Foundation VSS solution features and characteristics:</span></span>
  
    
    

- <span data-ttu-id="e2c34-p102">**Единый модуль записи ссылок VSS**. До настоящего времени отсутствовал эффективный способ описания данных приложений для приложений резервного копирования. Для работы с данными приложений на различных платформах Windows в приложениях резервного копирования использовалось множество интерфейсов API, для которых требовалось написание специального кода. Применение модуля записи VSS SharePoint Foundation (который в дальнейшем называется "модуль записи SPF-VSS") позволяет значительно повысить эффективность резервного копирования данных в SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p102">**A single VSS reference writer.** There has been no easy way for applications to describe their data to backup applications. To successfully back up various Windows platform applications, backup applications have an excessive number of APIs that they need to write specific code for. The SharePoint Foundation VSS writer (hereafter called "the SPF-VSS Writer") enables backup applications to take advantage of the single writer to backup SharePoint Foundation.</span></span>
    
  
- <span data-ttu-id="e2c34-p103">**Полное резервное копирование и восстановление фермы в аварийных ситуациях**. При использовании модуля записи SPF-VSS приложение резервного копирования (запрашивающая сторона) обращается к интерфейсу API VSS и запрашивает резервное копирование или восстановление всей фермы SharePoint Foundation, в том числе параметров настройки и конфигурации фермы. (Хранилище конфигурации IIS, которое в основном представляет файл  `applicationhost.config`, не включается. Его необходимо архивировать и восстанавливать отдельно.)</span><span class="sxs-lookup"><span data-stu-id="e2c34-p103">**Full farm backup and restore for catastrophe.** The SPF-VSS Writer enables a backup application (requestor) to access the VSS API to request a backup or a restore operation for an entire SharePoint Foundation farm, including a single box setup or a farm configuration. (The IIS configuration store, which is primarily the `applicationhost.config` file, is not included. It must be backed up and restored separately.)</span></span>
    
  
- <span data-ttu-id="e2c34-p104">**Детализация на уровне базы данных**. При использовании модуля записи SPF-VSS запрашивающая сторона может выбрать для включения в операции резервного копирования и восстановления все базы данных, сегмент баз данных (множественный выбор) или отдельную базу (одиночный выбор). В модуле записи поддерживается выбор любых баз данных, за исключением баз данных конфигурации и баз данных контента центра администрирования. Резервное копирование и восстановление этих баз данных осуществляются только в составе всей фермы. (Хранилище конфигурации IIS не включается. Его необходимо архивировать и восстанавливать отдельно.)</span><span class="sxs-lookup"><span data-stu-id="e2c34-p104">**Database level granularity**. The SPF-VSS Writer enables a requestor to select all databases, a segment of the databases (multiple select), or a single database (single select) for both backup and restore operations. All databases, except configuration and the Central Administration content database, are selectable through the writer. The configuration and Central Administration content databases can be backed up and restored only as part of the whole farm. (The IIS configuration store is not included. It must be backed up and restored separately.)</span></span>
    
  
- <span data-ttu-id="e2c34-p105">**Опись баз данных**. Перед выполнением резервного копирования модулем записи SPF-VSS создается плоский список баз данных, выбранных для резервного копирования в ферме. Этот список возвращается запрашивающей стороне и используется для выполнения резервного копирования в месте физического расположения базы данных.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p105">**Inventory of databases.** Before backup, the SPF-VSS Writer generates a flat list of databases selected for backup within the farm. The list is returned to the requestor so that backup can be run on the location where the database is physically located.</span></span>
    
  
- <span data-ttu-id="e2c34-p106">**Поддержка ферм**. Модуль записи обеспечивает ограниченную поддержку синхронизации резервного копирования и восстановления фермы SharePoint Foundation. Модуль записи предоставляет запрашивающей стороне список серверов, баз данных и файлов, связанных с фермой. Запрашивающая сторона устанавливает подключение к каждому из серверов и вызывает модуль записи SPF-VSS для создания на них резервных копий или запуска операций восстановления.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p106">**Farm support.** The writer understands and provides support to synchronize backup and recovery on a SharePoint Foundation farm in a limited way. The writer provides the requestor with a list of servers, databases, and files associated with the farm. The requestor is responsible for making a separate connection to each server to call the SPF-VSS Writer on that server to generate the backup or to run the restore operation.</span></span>
    
  
- <span data-ttu-id="e2c34-p107">**Непрерывное резервное копирование контента**. Если в процессе резервного копирования файла он изменяется в приложении, возможно повреждение файла. В службе VSS создается моментальный снимок файлов, включаемых в теневую копию, что позволяет не прерывать работу с исходными файлами.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p107">**Backup content without interruption.** If an application modifies a file while it is being backed up, the file could become corrupt. VSS enables a quick snapshot of the files to the shadow copy, while the application continues to operate at the original location without interruption.</span></span>
    
  
- <span data-ttu-id="e2c34-p108">**Подключаемое резервное копирование и восстановление баз данных сторонних производителей**. Модуль записи SPF-VSS поддерживает подключаемое (расширяемое) резервное копирование решений сторонних производителей, построенных на базе SharePoint Foundation. Однако в процесс резервного копирования могут включаться только те базы данных, которые зарегистрированы в базе данных конфигурации. Другие дополнительные файлы и незарегистрированные базы данных не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p108">**Third-party pluggable database backup and recovery.** The SPF-VSS Writer offers pluggable/extensible backup for third-party solutions built on top of SharePoint Foundation. However, only databases that are registered within the configuration database are included in the writer. Any additional files and unregistered databases are not included.</span></span>
    
  
- <span data-ttu-id="e2c34-p109">**Резервное копирование и восстановление файлов индекса поиска**. Поскольку файлы индекса поиска хранятся в файловой системе, для их резервного копирования требуется отдельный модуль записи. Чтобы разрешить эту проблему, в SharePoint Foundation используется отдельный модуль записи, предназначенный для работы с файлами индекса поиска. Для упрощения резервного копирования в SharePoint Foundation объявляются зависимости между модулями записи, которые обеспечивают резервное копирование или восстановление файлов индекса поиска при резервном копировании зарегистрированных в ферме баз данных.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p109">**Search index files backup and recovery.** Because search index files are stored in the file system, a separate file writer is needed to them up back up. To resolve this, SharePoint Foundation includes a separate search writer that handles search index files. To simplify the process for backup application writers, SharePoint Foundation declares cross-writer dependencies in such a way that search index files are also backed up or restored when backing up registered databases in the farm.</span></span>
    
  
- <span data-ttu-id="e2c34-p110">**Полный откат**. Модуль записи SPF-VSS обрабатывает все компоненты в развертывании SharePoint Foundation, в том числе базы данных конфигурации и контента, а также базу данных и индекс поиска. Как отмечено ранее, модуль записи также имеет зависимость от модуля поиска, обрабатывающего все файлы индексов поиска для резервного копирования и восстановления. Во время восстановления модуль записи поддерживает полный откат развертывания SharePoint Foundation за счет восстановления предыдущей резервной копии фермы. (Хранилище конфигурации IIS не включается. Оно должно архивироваться и восстанавливаться отдельно.)</span><span class="sxs-lookup"><span data-stu-id="e2c34-p110">**Full rollback.** The SPF-VSS Writer handles all components within a SharePoint Foundation deployment, including the configuration database and the content databases and the Search database and index. As mentioned previously, the writer also has a dependency on the Search writer, which handles all the Search index files for backup and recovery. At the time of recovery, the writer can roll back the entire SharePoint Foundation deployment by restoring a previous farm backup. (The IIS configuration store is not included. It must be backed up and restored separately.)</span></span>
    
    > <span data-ttu-id="e2c34-147">**Примечание:** Важные сведения о восстановлений в разделе «Восстановление» в [опросчики VSS и SharePoint](vss-requestors-and-sharepoint.md) .</span><span class="sxs-lookup"><span data-stu-id="e2c34-147">**Note:** See "Restoring" in  [VSS requestors and SharePoint](vss-requestors-and-sharepoint.md) for important information about restorations.</span></span>
- <span data-ttu-id="e2c34-p111">**Синхронизация баз данных после восстановления**. Чтобы обеспечить синхронизацию всех баз данных в ферме, по завершении восстановления каждая база автоматически отсоединяется от фермы и повторно подсоединяется к ней. Выполнение дополнительных процедур для синхронизации восстановленных баз данных не требуется.</span><span class="sxs-lookup"><span data-stu-id="e2c34-p111">**Post-restore synchronization of databases.** To ensure that all databases are synchronized with the farm after a restore operation is complete, each of the databases are automatically detached and reattached to the farm post recovery. Administrators do not need to run additional procedures to resynchronize the restored databases.</span></span>
    
  

> <span data-ttu-id="e2c34-151">**Важные:** Если вы используете псевдонимы SQL в ферме серверов SharePoint Foundation для подключения к SQL Server, необходимо установить компоненты клиентского подключения SQL на серверах фермы перед использованием модуля записи SPF-VSS для резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="e2c34-151">**Important:** If you use SQL aliases in your SharePoint Foundation farm to connect to the SQL Server, then you must install the SQL client connectivity components on your farm servers in order to use the SPF-VSS writer for backup/restore.</span></span> <span data-ttu-id="e2c34-152">Компоненты включают поставщик SQL WMI для управление конфигурацией, которое модуля записи SPF-VSS требуется определить псевдонимы SQL к правильному серверу SQL.</span><span class="sxs-lookup"><span data-stu-id="e2c34-152">The components include SQL WMI provider for configuration management, which the SPF-VSS writer needs to resolve SQL aliases to the correct SQL Server.</span></span> <span data-ttu-id="e2c34-153">Необязательно для установки средства управления, такие как SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e2c34-153">It is not necessary to install any of the management tools such as SQL Management Studio.</span></span> <span data-ttu-id="e2c34-154">Необходимо использовать тот же источник установки (например, DVD с данными), которая используется для установки полной версии SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e2c34-154">You must use the same installation source (for example, a data DVD) that you would use to install the full SQL Server product.</span></span> <span data-ttu-id="e2c34-155">(Не используйте отдельные, автономного версии клиентских компонентов.</span><span class="sxs-lookup"><span data-stu-id="e2c34-155">(Do not use the separate, stand-alone, version of the client components.</span></span> <span data-ttu-id="e2c34-156">Эта версия не включает поставщик SQL WMI.) Выберите для создания настраиваемой установки и выберите только клиентских компонентов для установки.</span><span class="sxs-lookup"><span data-stu-id="e2c34-156">That version does not include the SQL WMI provider.) Choose to make a custom installation and choose only the client components to install.</span></span> 
  
    
    


## <a name="functions-performed-by-the-spf-vss-writer"></a><span data-ttu-id="e2c34-157">Функции модуля записи SPF-VSS</span><span class="sxs-lookup"><span data-stu-id="e2c34-157">Functions Performed by the SPF-VSS Writer</span></span>

<span data-ttu-id="e2c34-158">Модуль записи SPF-VSS предназначен для выполнения следующих функций.</span><span class="sxs-lookup"><span data-stu-id="e2c34-158">The SPF-VSS Writer performs the following functions:</span></span>
  
    
    

1. <span data-ttu-id="e2c34-159">Построение компонентов SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="e2c34-159">Builds SharePoint Foundation components.</span></span>
    
  - <span data-ttu-id="e2c34-160">Создание полного списка компонентов в ферме SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="e2c34-160">Generates a full list of all components within the SharePoint Foundation farm.</span></span>
    
  
  - <span data-ttu-id="e2c34-161">Необязательная привязка к процессам резервного копирования или восстановления.</span><span class="sxs-lookup"><span data-stu-id="e2c34-161">Is not necessarily tied to backup process or restore process.</span></span>
    
  

  ![SharePoint и служба теневого копирования томов](../images/99376713-6a54-4d88-9b05-068578169506.gif)
  

  

  
2. <span data-ttu-id="e2c34-163">Резервное копирование фермы или базы данных.</span><span class="sxs-lookup"><span data-stu-id="e2c34-163">Backs up farm or database.</span></span>
    
  - <span data-ttu-id="e2c34-164">Запрос резервного копирования фермы или базы данных SharePoint Foundation с помощью службы VSS.</span><span class="sxs-lookup"><span data-stu-id="e2c34-164">Requests a SharePoint Foundation (farm/database) backup via VSS.</span></span>
    
  

  ![SharePoint и служба теневого копирования томов](../images/97765b6d-51e9-4d07-8b5d-3e93c0508b16.gif)
  

  

  
3. <span data-ttu-id="e2c34-166">Восстановление фермы или базы данных.</span><span class="sxs-lookup"><span data-stu-id="e2c34-166">Restores a farm or database.</span></span>
    
  - <span data-ttu-id="e2c34-167">Запрос восстановления фермы или базы данных SharePoint Foundation с помощью службы VSS.</span><span class="sxs-lookup"><span data-stu-id="e2c34-167">Requests a SharePoint Foundation (farm/database) recovery via VSS.</span></span>
    
  
  - <span data-ttu-id="e2c34-168">Реализация метода **postRestore()** для синхронизации таблиц сайта.</span><span class="sxs-lookup"><span data-stu-id="e2c34-168">Implements **postRestore()** to synchronize sites table.</span></span>
    
  

  ![SharePoint и служба теневого копирования томов](../images/b86ecdb8-88a7-4407-af86-07d2442235dc.gif)
  

  

  

## <a name="next-steps"></a><span data-ttu-id="e2c34-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2c34-170">Next steps</span></span>
<span data-ttu-id="e2c34-171"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="e2c34-171"></span></span>

<span data-ttu-id="e2c34-172">Узнайте, как создавать и использовать запросов VSS для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="e2c34-172">Learn how to create and use a VSS requestor for SharePoint:</span></span>
  
    
    

-  [<span data-ttu-id="e2c34-173">Опросчики VSS и SharePoint</span><span class="sxs-lookup"><span data-stu-id="e2c34-173">VSS requestors and SharePoint</span></span>](vss-requestors-and-sharepoint.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="e2c34-174">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e2c34-174">Additional resources</span></span>
<span data-ttu-id="e2c34-175"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e2c34-175"></span></span>


-  [<span data-ttu-id="e2c34-176">Общие сведения о SharePoint и службы теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="e2c34-176">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  

