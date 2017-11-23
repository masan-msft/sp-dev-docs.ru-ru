---
title: "Как резервное копирование и восстановление приложения-службы поиска в SharePoint с использованием служба теневого копирования ТОМОВ"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 87ee28e6-8170-4dba-8c9d-f04ab9e632dc
ms.openlocfilehash: 20d1cfd4d8056c3b38405b3e14f4351eb3454322
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using-vss"></a><span data-ttu-id="eb7bc-102">Как: резервное копирование и восстановление приложения-службы поиска в SharePoint с использованием служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="eb7bc-102">How to: Back up and restore a search service application in SharePoint using VSS</span></span>
 <span data-ttu-id="eb7bc-103">**Сводка:** Узнайте, как резервное копирование и восстановление приложения-службы поиска в SharePoint с помощью тома теневой копии Service (VSS).</span><span class="sxs-lookup"><span data-stu-id="eb7bc-103">**Summary:** Learn how to back up and restore a search service application in SharePoint by using the Volume Shadow Copy Service (VSS).</span></span>
## <a name="prerequisites-for-backing-up-and-restoring-sharepoint-with-the-volume-shadow-copy-service"></a><span data-ttu-id="eb7bc-104">Необходимые условия для резервного копирования и восстановления SharePoint с помощью службы теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="eb7bc-104">Prerequisites for backing up and restoring SharePoint with the Volume Shadow Copy Service</span></span>

<span data-ttu-id="eb7bc-105">Чтобы программного резервного копирования и восстановления решения для SharePoint, необходимо понять, как работает служба теневого копирования ТОМОВ и интерфейс SharePoint с ним.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-105">To program a backup and restore solution for SharePoint, you need to understand how VSS works and the SharePoint interface with it.</span></span>
  
    
    

<span data-ttu-id="eb7bc-106">**В таблице 1. Основные понятия, которые для резервного копирования и восстановления SharePoint с помощью службы теневого копирования томов**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-106">**Table 1. Core concepts for backing up and restoring SharePoint with the Volume Shadow Copy Service**</span></span>


|<span data-ttu-id="eb7bc-107">**Статья**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-107">**Article**</span></span>|<span data-ttu-id="eb7bc-108">**Описание**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-108">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="eb7bc-109">[Службы теневого копирования томов](http://msdn.microsoft.com/ru-ru/library/windows/desktop/bb968832%28v=vs.85%29.aspx) и его дочерних статьи.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-109">[Volume Shadow Copy Service](http://msdn.microsoft.com/ru-ru/library/windows/desktop/bb968832%28v=vs.85%29.aspx) and its child articles.</span></span> <br/> |<span data-ttu-id="eb7bc-110">Сведения о службе теневого копирования ТОМОВ и объясняется, как программировать для него.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-110">Learn about the VSS and how to program for it.</span></span>  <br/> |
| <span data-ttu-id="eb7bc-111">[Службы Windows SharePoint Services и служба теневого копирования томов](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx) и его дочерних статьи.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-111">[Windows SharePoint Services and the Volume Shadow Copy Service](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx) and its child articles.</span></span> <br/> |<span data-ttu-id="eb7bc-112">Общие сведения и пошаговые руководства по резервному копированию и восстановлению данных SharePoint, с помощью интерфейса SharePoint и служба теневого копирования ТОМОВ с помощью службы VSS.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-112">Overview information and step-by-step, how-to procedures for backing up and restoring SharePoint data using the VSS and the SharePoint interface with VSS.</span></span>  <br/> |
   

## <a name="use-the-volume-shadow-copy-service-to-back-up-and-restore-a-search-service-application"></a><span data-ttu-id="eb7bc-113">Использование службы теневого копирования томов для резервного копирования и восстановления приложения-службы поиска</span><span class="sxs-lookup"><span data-stu-id="eb7bc-113">Use the Volume Shadow Copy Service to back up and restore a search service application</span></span>
<span data-ttu-id="eb7bc-114"><a name="Use"> </a></span><span class="sxs-lookup"><span data-stu-id="eb7bc-114"></span></span>

<span data-ttu-id="eb7bc-115">Следующие процедуры предназначены для помощи разработчикам с создания приложения резервного копирования и восстановления, с помощью службы VSS.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-115">The following procedures are intended to help developers with creating a backup/restore application that uses the VSS.</span></span> <span data-ttu-id="eb7bc-116">Если вы — ИТ-специалист, ищущий инструкции для резервного копирования или восстановления приложения-службы поиска SharePoint, видеть [резервное копирование и восстановление SharePoint](http://technet.microsoft.com/ru-ru/library/ee662536.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb7bc-116">If you are an IT professional looking for instructions for how to back up or restore a SharePoint search service application, see  [Backup and restore SharePoint](http://technet.microsoft.com/ru-ru/library/ee662536.aspx).</span></span> 
  
    
    
 <span data-ttu-id="eb7bc-p102">**Необходимых компонентов:** Загрузить и установить [пакет SDK для Microsoft Windows для Windows 7 и .NET Framework 4](http://www.microsoft.com/en-us/download/details.aspx?id=8279) на сервер с приложением-службой поиска (SSA) и на каждый сервер с компонентом индексирования поиска. Помимо прочего это будет установить `C:\\Program Files\\Microsoft SDKs\\Windows\\v7.1\\Bin\\x64\\vsstools`vshadow.exe и betest.exe.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p102">**Prerequisite:** Download and install [Microsoft Windows SDK for Windows 7 and .NET Framework 4](http://www.microsoft.com/en-us/download/details.aspx?id=8279) to the server with the search service application (SSA) and to every server with a search index component. Among other things, this will install vshadow.exe and betest.exe to `C:\\Program Files\\Microsoft SDKs\\Windows\\v7.1\\Bin\\x64\\vsstools`.</span></span>
  
    
    

> <span data-ttu-id="eb7bc-119">**Совет:** Для получения дополнительных сведений о командлетов Windows PowerShell, упомянутые в этой статье видеть [Windows PowerShell для SharePoint reference](http://technet.microsoft.com/ru-ru/library/ee890108.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb7bc-119">**Tip:** For details about the Windows PowerShell cmdlets mentioned in this article, see  [Windows PowerShell for SharePoint reference](http://technet.microsoft.com/ru-ru/library/ee890108.aspx).</span></span> 
  
    
    


### <a name="to-register-the-sharepoint-vss-writer-and-prepare-the-servers-for-backing-up-and-restoring"></a><span data-ttu-id="eb7bc-120">Регистрация модуля записи VSS SharePoint и Подготовка серверов для резервного копирования и восстановления</span><span class="sxs-lookup"><span data-stu-id="eb7bc-120">To register the SharePoint VSS Writer and prepare the servers for backing up and restoring</span></span>


- <span data-ttu-id="eb7bc-121">Регистрация модуля записи VSS SharePoint с помощью одного из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-121">Register the SharePoint VSS Writer with either of these methods:</span></span>
    
  - <span data-ttu-id="eb7bc-122">В **Меню Администрирование** откройте **службы** и запустить службу **Модуля записи VSS SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-122">Open **Services** in **Administrative Tools** and start the **SharePoint VSS Writer** service.</span></span>
    
  
  - <span data-ttu-id="eb7bc-p103">Откройте командную консоль и выполните  `stsadm.exe -o registerwsswriter`. Программы stsadm было получено на %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ КОРЗИНЫ. Убедитесь, что служба запущена в **служб** в **Меню Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p103">Open a command console and execute  `stsadm.exe -o registerwsswriter`. The stsadm utility is found in %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\BIN. Verify that the service is running in **Services** in **Administrative Tools**.</span></span>
    
  

### <a name="to-back-up-a-sharepoint-search-service-application-using-vss"></a><span data-ttu-id="eb7bc-126">Резервное копирование приложения службы поиска SharePoint с помощью служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="eb7bc-126">To back up a SharePoint search service application using VSS</span></span>


1. <span data-ttu-id="eb7bc-p104">Получение метаданных служба теневого копирования ТОМОВ путем выполнения  `vshadow.exe -wm > writers.txt` командной строки на каждом сервере, который содержит компонент индекса, а также на компьютере, на котором работает SQL Server, где размещены базы данных поиска. Файл writers.txt, созданный перечислены все записи VSS, связанный с сервером. Используйте этот файл дальнейшие действия для создания файлов манифеста для приложения-службы поиска (SSA) и индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p104">Get VSS metadata by executing  `vshadow.exe -wm > writers.txt` at a command line on each server that contains an index component and also on the computer that is running SQL Server where the search databases are located. The writers.txt file that is created lists all VSS writers associated with the server. You use this file in the next steps to generate manifest files for the search service application (SSA) and search index.</span></span>
    
  
2. <span data-ttu-id="eb7bc-130">Выполните следующие действия для создания манифеста для SSA на компьютере, на котором работает SQL Server, где размещены базы данных поиска.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-130">Follow these steps to create a manifest for the SSA on the computer that is running SQL Server where the search databases are located.</span></span>
    
1. <span data-ttu-id="eb7bc-131">Создайте XML-файл и скопируйте в него следующий:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-131">Create an XML file and copy the following into it:</span></span> 
    
```XML
  
<BETest>
  <Writer writerid="SharePoint Services Writer ID">
    <Component logicalPath="PathSSA" componentName="SearchAppOffice" />
    <Component logicalPath="PathC" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="PathA" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="PathL" componentName="SearchAppOffice_LinksStore" />
  </Writer>
  <Writer writerid="SQL Server Writer ID">
    <Component logicalPath="PathDbSSA" componentName="SearchAppOffice" />
    <Component logicalPath="PathDbC" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="PathDbA" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="PathDbL" componentName="SearchAppOffice_LinksStore" />
  </Writer>
</BETest>

```

2. <span data-ttu-id="eb7bc-p105">Замените заполнители 10 в этот файл с соответствующими значениями из файла writer.txt, который вы создали на первом шаге. Используйте следующие таблицы в качестве руководства.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p105">Replace the 10 placeholders in this file with appropriate values from the writer.txt file that you generated in the first step. Use the following table as a guide.</span></span> 
    
    > <span data-ttu-id="eb7bc-134">**Примечание:** В правом столбце _SSA_ является имя приложения-службы поиска.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-134">**Note:** In the right-hand column,  _SSA_ is itself a placeholder for the name of the Search Service Application.</span></span>

   <span data-ttu-id="eb7bc-135">**В таблице 2. Файл манифеста заполнители SSA и значениями, полученными из writers.txt**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-135">**Table 2. SSA manifest file placeholders and values from writers.txt**</span></span>


|<span data-ttu-id="eb7bc-136">**Заполнитель**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-136">**Placeholder**</span></span>|<span data-ttu-id="eb7bc-137">**Расположение сведения в writers.txt.**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-137">**Where the information is located in writers.txt.**</span></span>|
|:-----|:-----|
| <span data-ttu-id="eb7bc-138">_SharePoint Services Writer ID_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-138">_SharePoint Services Writer ID_</span></span> <br/> |<span data-ttu-id="eb7bc-139">Идентификатор GUID WriterId из списка в разделе запись «Записи SharePoint Services»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-139">The WriterId GUID listed under the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-140">_PathSSA_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-140">_PathSSA_</span></span> <br/> |<span data-ttu-id="eb7bc-141">Запись логический путь, имя приложения-службы поиска в запись «Записи SharePoint Services» в списке</span><span class="sxs-lookup"><span data-stu-id="eb7bc-141">The logical path entry listed with the name of the Search Service Application in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-142">_PathC_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-142">_PathC_</span></span> <br/> |<span data-ttu-id="eb7bc-143">Запись логический путь из списка для компонент с именем" _SSA__CrawlStore" в запись "Записи SharePoint Services"</span><span class="sxs-lookup"><span data-stu-id="eb7bc-143">The logical path entry listed for the component named " _SSA__CrawlStore" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-144">_PathA_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-144">_PathA_</span></span> <br/> |<span data-ttu-id="eb7bc-145">Запись логический путь из списка для компонент с именем" _SSA_ _AnalyticsReportingStore" в запись "Записи SharePoint Services"</span><span class="sxs-lookup"><span data-stu-id="eb7bc-145">The logical path entry listed for the component named " _SSA_ _AnalyticsReportingStore" in the "SharePoint Services Writer" entry</span></span> <br/> |
| <span data-ttu-id="eb7bc-146">_PathL_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-146">_PathL_</span></span> <br/> |<span data-ttu-id="eb7bc-147">Запись логический путь из списка для компонент с именем" _SSA__LinksStore" в запись "Записи SharePoint Services"</span><span class="sxs-lookup"><span data-stu-id="eb7bc-147">The logical path entry listed for the component named " _SSA__LinksStore" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-148">_SQL Server Writer ID_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-148">_SQL Server Writer ID_</span></span> <br/> |<span data-ttu-id="eb7bc-149">Идентификатор GUID WriterId из списка в разделе запись «SqlServerWriter»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-149">The WriterId GUID listed under the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-150">_PathDbSSA_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-150">_PathDbSSA_</span></span> <br/> |<span data-ttu-id="eb7bc-151">Операция логический путь из списка для компонента с именем приложения-службы поиска в записи «SqlServerWriter»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-151">The logical path entry listed for the component with the name of the Search Service Application in the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-152">_PathDbC_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-152">_PathDbC_</span></span> <br/> |<span data-ttu-id="eb7bc-153">Запись логический путь из списка для компонент с именем" _SSA__CrawlStore" операции "SqlServerWriter"</span><span class="sxs-lookup"><span data-stu-id="eb7bc-153">The logical path entry listed for the component named " _SSA__CrawlStore" in the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-154">_PathDbA_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-154">_PathDbA_</span></span> <br/> |<span data-ttu-id="eb7bc-155">Запись логический путь из списка для компонент с именем" _SSA__AnalyticsReportingStore" операции "SqlServerWriter"</span><span class="sxs-lookup"><span data-stu-id="eb7bc-155">The logical path entry listed for the component named " _SSA__AnalyticsReportingStore" in the "SqlServerWriter" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-156">_PathDbL_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-156">_PathDbL_</span></span> <br/> |<span data-ttu-id="eb7bc-157">Запись логический путь из списка для компонент с именем" _SSA__LinksStore" операции "SqlServerWriter"</span><span class="sxs-lookup"><span data-stu-id="eb7bc-157">The logical path entry listed for the component named " _SSA__LinksStore" in the "SqlServerWriter" entry</span></span>  <br/> |
   

    This is the SSA manifest file. For an example of a completed SSA manifest file, see  [Example manifest files](#Examples).
    
  
3. <span data-ttu-id="eb7bc-p106">Выполните следующие действия для создания манифеста для поиска файлов индекса. Повторите эти действия на каждом сервере, содержащий компонент индекса.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p106">Follow these steps to create a manifest for the search index files. Repeat these steps on every server that has an index component.</span></span>
    
1. <span data-ttu-id="eb7bc-160">Создайте XML-файл и скопируйте в него следующий:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-160">Create an XML file and copy the following into it:</span></span>
    
```XML
  
<BETest>
   <Writer writerid="SharePoint Services Writer ID">
      <Component logicalPath="PathIndex" componentName="NameIndex" />
   </Writer>
   <Writer writerid="OSearch15 Writer ID">
      <Component logicalPath="PathOSearch15" componentName="IndexComponentGroup" />
   </Writer>    
</BETest>
```

2. <span data-ttu-id="eb7bc-p107">Замените заполнители шесть в этот файл с соответствующими значениями из файла writer.txt, который вы создали на первом шаге. Используйте следующие таблицы в качестве руководства.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p107">Replace the six placeholders in this file with appropriate values from the writer.txt file that you generated in the first step. Use the following table as a guide.</span></span>
    
   <span data-ttu-id="eb7bc-163">**В таблице 3. Заполнители файл манифеста индекса поиска и значениями, полученными из writer.txt**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-163">**Table 3. Search index manifest file placeholders and values from writer.txt**</span></span>


|<span data-ttu-id="eb7bc-164">**Заполнитель**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-164">**Placeholder**</span></span>|<span data-ttu-id="eb7bc-165">**Расположение сведения в writers.txt**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-165">**Where the information is located in writers.txt**</span></span>|
|:-----|:-----|
| <span data-ttu-id="eb7bc-166">_SharePoint Services Writer ID_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-166">_SharePoint Services Writer ID_</span></span> <br/> |<span data-ttu-id="eb7bc-167">Идентификатор GUID WriterId из списка в разделе запись «Записи SharePoint Services»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-167">The WriterId GUID listed under the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-168">_PathIndex_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-168">_PathIndex_</span></span> <br/> |<span data-ttu-id="eb7bc-169">Операция логический путь из списка для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи SharePoint Services»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-169">The logical path entry listed for the component whose name starts with "IndexComponentGroup" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-170">_NameIndex_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-170">_NameIndex_</span></span> <br/> |<span data-ttu-id="eb7bc-171">Запись имени, перечисленных для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи SharePoint Services»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-171">The name entry listed for the component whose name starts with "IndexComponentGroup" in the "SharePoint Services Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-172">_OSearch15 Writer ID_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-172">_OSearch15 Writer ID_</span></span> <br/> |<span data-ttu-id="eb7bc-173">Идентификатор GUID WriterId из списка в разделе запись «Записи VSS OSearch15»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-173">The WriterId GUID listed under the "OSearch15 VSS Writer" entry</span></span>  <br/> |
| <span data-ttu-id="eb7bc-174">_PathOSearch15_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-174">_PathOSearch15_</span></span> <br/> |<span data-ttu-id="eb7bc-p108">Запись логический путь, указанные для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи VSS OSearch15». Это обычно пустым.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p108">The logical path entry listed for the component whose name starts with "IndexComponentGroup" in the "OSearch15 VSS Writer" entry. It is normally empty.</span></span>  <br/> |
| <span data-ttu-id="eb7bc-177">_IndexComponentGroup_</span><span class="sxs-lookup"><span data-stu-id="eb7bc-177">_IndexComponentGroup_</span></span> <br/> |<span data-ttu-id="eb7bc-178">Запись имени, перечисленных для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи VSS OSearch15»</span><span class="sxs-lookup"><span data-stu-id="eb7bc-178">The name entry listed for the component whose name starts with "IndexComponentGroup" in the "OSearch15 VSS Writer" entry</span></span>  <br/> |
   

    This is the search index manifest file. For an example of a completed search index manifest file, see  [Example manifest files](#Examples).
    
  
4. <span data-ttu-id="eb7bc-p109">(Необязательно) Запишите размеры папок **IndexComponent** на каждом сервере, который содержит компонент индекса. Эти сведения можно использовать более поздней версии для проверки резервной копии.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p109">(Optional) Record the sizes of **IndexComponent** folders on each server that contains an index component. You can use this information later to verify the backup.</span></span>
    
  
5. <span data-ttu-id="eb7bc-p110">На любом сервере в ферме откройте Командная консоль SharePoint и выполните следующие команды, где  _name of search service application_  SSA, требуется выполнить резервное. Не закрывайте окно Командная консоль SharePoint позже.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p110">On any server in the farm, open the SharePoint Management Shell and execute the following lines, where  _name of search service application_ is the SSA that you want to back up. Leave the SharePoint Management Shell window open afterward.</span></span>
    
```
  
$ssa = Get-SpenterpriseSearchServiceApplication -Identity "name of search service application"
Suspend-SPEnterpriseSearchServiceApplication -Identity $ssa
```

6. <span data-ttu-id="eb7bc-183">Выполните резервное копирование баз данных SSA и индекса, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-183">Perform backups of the SSA databases and the index by following these steps:</span></span>
    
1. <span data-ttu-id="eb7bc-184">На сервере с базами данных SSA выполните следующую команду в командной строке, где  _destination backup folder_  это полный путь к папке для резервных копий файлов, _backup log file_  это полный путь и имя файла резервной копии журнала и _SSA manifest file_  это путь и имя файла манифеста SSA.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-184">On the server with the SSA databases, execute the following command at a command line, where  _destination backup folder_ is the full path of the folder for the backup files, _backup log file_ is the full path and name of the backup log file, and _SSA manifest file_ is the path and file name of the SSA manifest file.</span></span>
    
```
  
betest.exe /v /b /d "destination backup folder" /s "backup log file" /x "SSA manifest file"
```

2. <span data-ttu-id="eb7bc-p111">На сервере с окном open Командная консоль SharePoint выполните указанную ниже команду, где  _topology file name_  это полный путь и имя экспортируемого файла, содержащего сведения о топологии. Необходимо использовать этот файл в процедуре восстановления для SSA.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p111">On the server with the open SharePoint Management Shell window, execute the following line, where  _topology file name_ is the full path and name of the exported file containing the topology information. You will use this file in the restore procedure for the SSA.</span></span>
    
```
  Export-SPEnterpriseSearchTopology -SearchApplication $ssa -Filename "topology file name"
```

3. <span data-ttu-id="eb7bc-187">Убедитесь, что файл создан.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-187">Verify that the file is created.</span></span>
    
  
4. <span data-ttu-id="eb7bc-188">На каждом сервере, содержащий компонент индекса выполните следующую команду в командной строке, где  _destination backup folder_  это полный путь к папке для резервных копий файлов, _backup log file_  это полный путь и имя файла резервной копии журнала и _index manifest file_  это путь и имя файла манифеста индекса.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-188">On each server that has an index component, execute the following at a command line, where  _destination backup folder_ is the full path of the folder for the backup files, _backup log file_ is the full path and name of the backup log file, and _index manifest file_ is the path and file name of the index manifest.</span></span>
    
```
  betest.exe /v /b /d "destination backup folder" /s "backup log file" /x "index manifest file"
```

5. <span data-ttu-id="eb7bc-p112">(Необязательно) Проверьте индекс папки, которые были созданы резервные копии. Убедитесь, что имена папок и размеры совпадают с учетными записями в предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p112">(Optional) Inspect the index folders that have been backed up. Verify that folder names and sizes match with those recorded in the earlier step.</span></span>
    
  

### <a name="to-restore-a-sharepoint-search-service-application-using-vss"></a><span data-ttu-id="eb7bc-191">Для восстановления приложения службы поиска SharePoint с помощью служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="eb7bc-191">To restore a SharePoint search service application using VSS</span></span>


1. <span data-ttu-id="eb7bc-p113">На любом сервере в ферме откройте Командная консоль SharePoint и выполните следующие команды для удаления существующего приложения службы поиска и его прокси-сервер, где  _name of search service application_ является SSA, которую требуется восстановить, а _name of proxy_  его прокси приложения. Обратите внимание, что этот _name of SSA proxy_  это обычно совпадает с именем SSA с слово "Прокси" добавлен в конец. Переключатель `RemoveData` гарантирует, что удаляются баз данных поиска.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p113">On any server in the farm, open the SharePoint Management Shell and execute the following lines to remove the existing search service application and its proxy, where  _name of search service application_ is the SSA that you want to restore and _name of proxy_ is its application proxy. Note that _name of SSA proxy_ is normally the same as the name of the SSA with the word "Proxy" added to the end. The `RemoveData` switch ensures that the search databases are removed.</span></span>
    
```
  $ssa = Get-SPEnterpriseSearchServiceApplication -Identity "name of search service application"
Remove-SPEnterpriseSearchServiceApplication -Identity $ssa -RemoveData
Remove-SPEnterpriseSearchServiceApplicationProxy -Identity "name of SSA proxy"
```

2. <span data-ttu-id="eb7bc-195">На том же сервере выполните следующую команду в командную строку для восстановления баз данных SSA, где  _destination backup folder_  это полный путь к папке для резервных копий файлов, _backup log file_  это полный путь и имя файла резервной копии журнала и _SSA manifest file_  это путь и имя файла манифеста SSA.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-195">On the same server, execute the following at a command line to restore the SSA databases, where  _destination backup folder_ is the full path of the folder for the backup files, _backup log file_ is the full path and name of the backup log file, and _SSA manifest file_ is the path and file name of the SSA manifest file.</span></span>
    
```
  
betest.exe /v /r /d "destination backup folder" /s "backup log file" /x SSA_manifest_file
```

3. <span data-ttu-id="eb7bc-196">На том же сервере откройте Командная консоль SharePoint и выполните следующие строки, чтобы восстановить SSA, где  _application pool name_  это имя нового пула, _domain\\user_  это доменное имя пула приложений входит в систему в качестве пользователя, _name of the search service application_  это имя SSA и _topology_file_name_  это путь и имя файла топология, созданному при SSA была создана резервная копия.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-196">On the same server, open a SharePoint Management Shell and execute the following lines to restore the SSA, where  _application pool name_ is the name of the new pool, _domain\\user_ is the domain name of the user that the application pool logs in as, _name of the search service application_ is the name of the SSA, and _topology_file_name_ is the path and name of the typology file you created when the SSA was backed up.</span></span>
    
    > <span data-ttu-id="eb7bc-197">**Совет:** В этом коде создается новый удостоверения пула приложений для запуска восстановленных SSA, но можно также использовать существующую учетную запись с помощью командлета **Get-SPServiceApplicationPool** .</span><span class="sxs-lookup"><span data-stu-id="eb7bc-197">**Tip:** This code creates a new application pool identity to run the restored SSA, but you can also use an existing account with the **Get-SPServiceApplicationPool** cmdlet.</span></span>

```
  $applicationPool = New-SPServiceApplicationPool -name "application pool name" -account "domain\\user"
Restore-SPEnterpriseSearchServiceApplication -Name "name of the search service application" -ApplicationPool $applicationPool -TopologyFile "topology_file_name" -KeepId
```

4. <span data-ttu-id="eb7bc-p114">Создание прокси-сервера для SSA с помощью следующих командлетов. Мы рекомендуем использовать те же значения для  _name of the search service application_ и _name of SSA proxy_, как используется в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p114">Create a proxy for the SSA with the following cmdlets. We recommend that you use the same values for  _name of the search service application_ and _name of SSA proxy_ as you used in step 1.</span></span>
    
```
  
$ssa = Get-SpenterpriseSearchServiceApplication -Identity "name of search service application"
New-SPEnterpriseSearchServiceApplicationProxy -Name "name of SSA proxy" -SearchApplication $ssa
```

5. <span data-ttu-id="eb7bc-p115">(Необязательно) Проверьте существование SSA и его прокси-сервер, откройте **Центр администрирования**. Выберите **Управление приложениями-службами** и убедитесь, что указано SSA и его прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p115">(Optional) Verify that the SSA and its proxy exist by opening **Central Administration**. Choose **Manage Service Applications** and verify that the SSA and its proxy are listed.</span></span>
    
  
6. <span data-ttu-id="eb7bc-p116">(Необязательно) Нажмите кнопку SSA в списке служб и на открывшейся странице убедитесь, что в таблице **Топология приложения поиска** соответствует топология, который был экспортирован в процедуры резервного копирования. (Можно также проверить топологию с помощью командлета **Get-SPEnterpriseSearchStatus**.)</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p116">(Optional) Click the SSA on the list of services, and then, on the page that opens, verify that the **Search Application Topology** table matches the typology that you exported in the backup procedure. (You can also verify the topology with the cmdlet **Get-SPEnterpriseSearchStatus**.)</span></span>
    
  
7. <span data-ttu-id="eb7bc-204">Восстановите файлы индекса, используя следующую процедуру **на всех серверах с компонентами индекса**.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-204">Restore the index files with the following procedure **on all servers with index components**.</span></span>
    
1. <span data-ttu-id="eb7bc-205">Остановить хост-контроллер службы в **Администрирование > службы**, или выполнив следующий командлет в Командная консоль SharePoint:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-205">Stop the Host Controller service either in **Administrative Tools > Services**, or by executing the following cmdlet in SharePoint Management Shell:</span></span>
    
```
  
stop-service SPSearchHostController
```

2. <span data-ttu-id="eb7bc-206">На тех же серверах выполните следующую команду в командной строке, где  _index manifest file_  это путь и имя файла манифеста индекса, созданный в процедуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-206">On the same servers, execute the following at a command line, where  _index manifest file_ is the path and file name of the index manifest that you created in the backup procedure.</span></span>
    
```
  betest.exe /v /r /d "destination backup folder" /s "backup log file" /x "index manifest file"
```

3. <span data-ttu-id="eb7bc-207">(Необязательно) Убедитесь, что имена папок и размеры равны, записанные в процедуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-207">(Optional) Verify that the folder names and sizes match those that you recorded in the backup procedure.</span></span>
    
  
4. <span data-ttu-id="eb7bc-208">Для каждого компонента индекса переименуйте данных в папке данных, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-208">For every index component, rename data under the data folder by following these steps:</span></span>
    
1. <span data-ttu-id="eb7bc-209">В Командная консоль SharePoint выполните следующий командлет.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-209">In SharePoint Management Shell, execute the following cmdlet.</span></span>
    
```
  Get-SPEnterpriseSearchVssDataPath
```

2. <span data-ttu-id="eb7bc-p117">Выходные данные командлета запишите последнюю часть каждый идентификатор GUID. Например если одну строку выходных данных  `IndexComponentGroup_e255918b-6ab0-4d7c-8049-720b2744c62f`, запишите 720b2744c62f.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p117">From the output of the cmdlet, record the last part of each GUID. For example, if one line of the output is  `IndexComponentGroup_e255918b-6ab0-4d7c-8049-720b2744c62f`, record 720b2744c62f.</span></span>
    
  
3. <span data-ttu-id="eb7bc-212">В **Обозревателе файлов** (или **Проводник** Windows Server 2008) перейдите к `C:\\Program Files\\Microsoft Office Servers\\15.0\\Data\\Office Server\\Applications\\Search\\Nodes\\24488A\\IndexComponentN\\storage\\data`, где  *N*   число компонент индекса.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-212">In **File Explorer** (or **Windows Explorer** on Windows Server 2008), navigate to `C:\\Program Files\\Microsoft Office Servers\\15.0\\Data\\Office Server\\Applications\\Search\\Nodes\\24488A\\IndexComponentN\\storage\\data`, where  *N*  is the number of an index component.</span></span>
    
  
4. <span data-ttu-id="eb7bc-p118">Каждая из этих папок имеет вложенной папке, имя которых начинается с «Пакет обновления», а затем 12 шестнадцатеричных цифр, за которым следует номер версии. Для каждого из этих вложенных папок, в которых 12 шестнадцатеричных цифр соответствуют окончания идентификатор GUID, записанные в предыдущем шаге переименуйте вложенной папке в importindex. В качестве основного примера будет переименуйте вложенной папке  `SP720b2744c62f.1.I.1.0` вimportindex.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p118">Each of these folders has a subfolder whose name begins with "SP" followed by 12 hex digits followed by a version number. For each of these subfolders where the 12 hex digits match one of the GUID endings that you recorded in the earlier step, rename the subfolder to importindex. In the continuing example, you would rename the subfolder  `SP720b2744c62f.1.I.1.0` toimportindex.</span></span>
    
  
5. <span data-ttu-id="eb7bc-216">Перезапустить хост-контроллер службы в **Администрирование > службы**, или выполнив следующий командлет в Командная консоль SharePoint:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-216">Restart the host controller service either in **Administrative Tools > Services**, or by executing the following cmdlet in SharePoint Management Shell:</span></span>
    
```
  start-service SPSearchHostController
```

6. <span data-ttu-id="eb7bc-p119">Убедитесь, что имена папок индекса данные возвращаются обратно в их предыдущее имя. (В качестве основного примера, это может быть "" SP720b2744c62f.1.I.1.0 ".)</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p119">Verify that the index data folder names have reverted back to their previous name. (In the continuing example, this would be "'SP720b2744c62f.1.I.1.0".)</span></span>
    
  
8. <span data-ttu-id="eb7bc-219">(Необязательно) Проверьте соответствие размеры папок **IndexComponent** размеры, записанные в процедуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-219">(Optional) Verify that the sizes of **IndexComponent** folders match the sizes you recorded in the backup procedure.</span></span>
    
  
9. <span data-ttu-id="eb7bc-220">Перезапустите SSA.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-220">Restart the SSA.</span></span>
    
  
10. <span data-ttu-id="eb7bc-221">На затронутых серверах запустите следующий командлет в Командная консоль SharePoint, чтобы проверить правильность работы приложения службы поиска:</span><span class="sxs-lookup"><span data-stu-id="eb7bc-221">On all the affected servers, run the following cmdlet in SharePoint Management Shell to verify that the search application service is running properly:</span></span>
    
```
  Get-SPEnterpriseSearchStatus
```

11. <span data-ttu-id="eb7bc-p120">Проверка работы передачи данных и поиска для новых документов. Например, проверьте размер индекса с помощью запроса "размер > = 0". Добавить новый документ и убедитесь, что для поиска.</span><span class="sxs-lookup"><span data-stu-id="eb7bc-p120">Verify that feeding and searching for new documents works. For example, check the size of the index by using the query "size>=0". Also add a new document and verify that it is searchable.</span></span>
    
  

## <a name="example-manifest-files"></a><span data-ttu-id="eb7bc-225">Пример файлов манифестов</span><span class="sxs-lookup"><span data-stu-id="eb7bc-225">Example manifest files</span></span>
<span data-ttu-id="eb7bc-226"><a name="Examples"> </a></span><span class="sxs-lookup"><span data-stu-id="eb7bc-226"></span></span>

 <span data-ttu-id="eb7bc-227">**Файл манифеста SSA**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-227">**SSA manifest file**</span></span>
  
    
    

```XML
<BETest>
  <Writer writerid="da452614-4858-5e53-a512-38aab25c61ad">
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\2e1f9435-d714-4bcb-be8d-ae1214e2ea22" componentName="SearchAppOffice" />
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\b8bb09b8-a823-43b0-a131-7bd5464f91fb" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\20c0c0b5-2086-4b16-8ce8-2cecb5186ebe" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\15004c47-21ca-441e-80fe-9e068ef4ad14" componentName="SearchAppOffice_LinksStore" />
  </Writer>
  <Writer writerid="a65faa63-5ea8-4ebc-9dbd-a0c4db26912a">
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice" />
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice_CrawlStore" />
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice_AnalyticsReportingStore" />
    <Component logicalPath="DDDVSS4\\SQLEXPRESS" componentName="SearchAppOffice_LinksStore" />
  </Writer>
</BETest>

```

 <span data-ttu-id="eb7bc-228">**Файл манифеста индекса**</span><span class="sxs-lookup"><span data-stu-id="eb7bc-228">**Index manifest file**</span></span>
  
    
    



```XML

<BETest>
  <Writer writerid="da452614-4858-5e53-a512-38aab25c61ad">
    <Component logicalPath="3bca1050-c15a-4987-93dc-8f911d35a0ba\\cfbddb07-2409-4b3d-997b-ee1b936c3dbd" componentName="IndexComponentGroup_3bca1050-c15a-4987-93dc-8f911d35a0ba" />
  </Writer>
  <Writer writerid="0ff1ce15-0201-0000-0000-000000000000">
    <Component logicalPath="" componentName="IndexComponentGroup_3bca1050-c15a-4987-93dc-8f911d35a0ba" />
  </Writer>
</BETest>
```


## <a name="additional-resources"></a><span data-ttu-id="eb7bc-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="eb7bc-229">Additional resources</span></span>
<span data-ttu-id="eb7bc-230"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="eb7bc-230"></span></span>


-  [<span data-ttu-id="eb7bc-231">Службы Windows SharePoint Services и служба теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="eb7bc-231">Windows SharePoint Services and the Volume Shadow Copy Service</span></span>](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx)
    
  

