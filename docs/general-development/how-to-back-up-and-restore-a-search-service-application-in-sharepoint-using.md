---
title: Резервное копирование и восстановление приложения службы поиска в SharePoint с помощью VSS
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 87ee28e6-8170-4dba-8c9d-f04ab9e632dc
ms.openlocfilehash: d4c0a4985eb0098fe2367cc66490657cdbd437a8
ms.sourcegitcommit: a3cd408c6878f5b04730287a0a4f81c557653864
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2018
---
# <a name="back-up-and-restore-a-search-service-application-in-sharepoint-using-vss"></a>Резервное копирование и восстановление приложения службы поиска в SharePoint с помощью VSS

Узнайте, как резервное копирование и восстановление приложения-службы поиска в SharePoint с помощью тома теневой копии Service (VSS).

## <a name="prerequisites-for-backing-up-and-restoring-sharepoint-with-the-volume-shadow-copy-service"></a>Необходимые условия для резервного копирования и восстановления SharePoint с помощью службы теневого копирования томов

Чтобы программного резервного копирования и восстановления решения для SharePoint, необходимо понять, как работает служба теневого копирования ТОМОВ и интерфейс SharePoint с ним.
  
    
    

**В таблице 1. Основные понятия, которые для резервного копирования и восстановления SharePoint с помощью службы теневого копирования томов**


|**Статья**|**Описание**|
|:-----|:-----|
| [Службы теневого копирования томов](http://msdn.microsoft.com/en-us/library/windows/desktop/bb968832%28v=vs.85%29.aspx) и его дочерних статьи. |Сведения о службе теневого копирования ТОМОВ и объясняется, как программировать для него.  |
| [Службы Windows SharePoint Services и служба теневого копирования томов](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx) и его дочерних статьи. |Общие сведения и пошаговые руководства по резервному копированию и восстановлению данных SharePoint, с помощью интерфейса SharePoint и служба теневого копирования ТОМОВ с помощью службы VSS.  |
   

## <a name="use-the-volume-shadow-copy-service-to-back-up-and-restore-a-search-service-application"></a>Использование службы теневого копирования томов для резервного копирования и восстановления приложения-службы поиска
<a name="Use"> </a>

Следующие процедуры предназначены для помощи разработчикам с создания приложения резервного копирования и восстановления, с помощью службы VSS. Если вы — ИТ-специалист, ищущий инструкции для резервного копирования или восстановления приложения-службы поиска SharePoint, видеть [резервное копирование и восстановление SharePoint](http://technet.microsoft.com/en-us/library/ee662536.aspx). 
  
    
    
 **Необходимых компонентов:** Загрузить и установить [пакет SDK для Microsoft Windows для Windows 7 и .NET Framework 4](http://www.microsoft.com/en-us/download/details.aspx?id=8279) на сервер с приложением-службой поиска (SSA) и на каждый сервер с компонентом индексирования поиска. Помимо прочего это будет установить `C:\\Program Files\\Microsoft SDKs\\Windows\\v7.1\\Bin\\x64\\vsstools`vshadow.exe и betest.exe.
  
    
    

> **Совет:** Для получения дополнительных сведений о командлетов Windows PowerShell, упомянутые в этой статье видеть [Windows PowerShell для SharePoint reference](http://technet.microsoft.com/en-us/library/ee890108.aspx). 
  
    
    


### <a name="to-register-the-sharepoint-vss-writer-and-prepare-the-servers-for-backing-up-and-restoring"></a>Регистрация модуля записи VSS SharePoint и Подготовка серверов для резервного копирования и восстановления


- Регистрация модуля записи VSS SharePoint с помощью одного из следующих методов:
    
  - В **Меню Администрирование** откройте **службы** и запустить службу **Модуля записи VSS SharePoint**.
    
  
  - Откройте командную консоль и выполните  `stsadm.exe -o registerwsswriter`. Программы stsadm было получено на %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\ КОРЗИНЫ. Убедитесь, что служба запущена в **служб** в **Меню Администрирование**.
    
  

### <a name="to-back-up-a-sharepoint-search-service-application-using-vss"></a>Резервное копирование приложения службы поиска SharePoint с помощью служба теневого копирования ТОМОВ


1. Получение метаданных служба теневого копирования ТОМОВ путем выполнения  `vshadow.exe -wm > writers.txt` командной строки на каждом сервере, который содержит компонент индекса, а также на компьютере, на котором работает SQL Server, где размещены базы данных поиска. Файл writers.txt, созданный перечислены все записи VSS, связанный с сервером. Используйте этот файл дальнейшие действия для создания файлов манифеста для приложения-службы поиска (SSA) и индекс поиска.
1. Выполните следующие действия для создания манифеста для SSA на компьютере, на котором работает SQL Server, где размещены базы данных поиска.
1. Создайте XML-файл и скопируйте в него следующий: 

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

1. Замените заполнители 10 в этот файл с соответствующими значениями из файла writer.txt, который вы создали на первом шаге. Используйте следующие таблицы в качестве руководства. 

    > [!NOTE]
    > [!Примечание] В правом столбце  _SSA_ является имя приложения-службы поиска.

    **В таблице 2. Файл манифеста заполнители SSA и значениями, полученными из writers.txt**

    |**Заполнитель**|**Расположение сведения в writers.txt.**|
    |:-----|:-----|
    | _SharePoint Services Writer ID_ |Идентификатор GUID WriterId из списка в разделе запись «Записи SharePoint Services»  |
    | _PathSSA_ |Запись логический путь, имя приложения-службы поиска в запись «Записи SharePoint Services» в списке  |
    | _PathC_ |Запись логический путь из списка для компонент с именем" _SSA__CrawlStore" в запись "Записи SharePoint Services"  |
    | _PathA_ |Запись логический путь из списка для компонент с именем" _SSA_ _AnalyticsReportingStore" в запись "Записи SharePoint Services" |
    | _PathL_ |Запись логический путь из списка для компонент с именем" _SSA__LinksStore" в запись "Записи SharePoint Services"  |
    | _SQL Server Writer ID_ |Идентификатор GUID WriterId из списка в разделе запись «SqlServerWriter»  |
    | _PathDbSSA_ |Операция логический путь из списка для компонента с именем приложения-службы поиска в записи «SqlServerWriter»  |
    | _PathDbC_ |Запись логический путь из списка для компонент с именем" _SSA__CrawlStore" операции "SqlServerWriter"  |
    | _PathDbA_ |Запись логический путь из списка для компонент с именем" _SSA__AnalyticsReportingStore" операции "SqlServerWriter"  |
    | _PathDbL_ |Запись логический путь из списка для компонент с именем" _SSA__LinksStore" операции "SqlServerWriter"  |

    Это файл манифеста SSA. В качестве примера завершенный файл манифеста SSA см [файлов манифеста](#Examples).

1. Выполните следующие действия для создания манифеста для поиска файлов индекса. Повторите эти действия на каждом сервере, содержащий компонент индекса.
1. Создайте XML-файл и скопируйте в него следующий:

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

2. Замените заполнители шесть в этот файл с соответствующими значениями из файла writer.txt, который вы создали на первом шаге. Используйте следующие таблицы в качестве руководства.

   **В таблице 3. Заполнители файл манифеста индекса поиска и значениями, полученными из writer.txt**

    |**Заполнитель**|**Расположение сведения в writers.txt**|
    |:-----|:-----|
    | _SharePoint Services Writer ID_ <br/> |Идентификатор GUID WriterId из списка в разделе запись «Записи SharePoint Services»  <br/> |
    | _PathIndex_ <br/> |Операция логический путь из списка для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи SharePoint Services»  <br/> |
    | _NameIndex_ <br/> |Запись имени, перечисленных для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи SharePoint Services»  <br/> |
    | _OSearch15 Writer ID_ <br/> |Идентификатор GUID WriterId из списка в разделе запись «Записи VSS OSearch15»  <br/> |
    | _PathOSearch15_ <br/> |Запись логический путь, указанные для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи VSS OSearch15». Это обычно пустым.  <br/> |
    | _IndexComponentGroup_ <br/> |Запись имени, перечисленных для компонента, имена которых начинаются с «IndexComponentGroup» в запись «Записи VSS OSearch15»  <br/> |

    Это файл манифеста индекса поиска. Пример завершенных поискового индекса-файл манифеста, пример [файлов манифеста](#Examples).

1. (Необязательно) Запишите размеры папок **IndexComponent** на каждом сервере, который содержит компонент индекса. Эти сведения можно использовать более поздней версии для проверки резервной копии.
1. На любом сервере в ферме откройте Командная консоль SharePoint и выполните следующие команды, где  _name of search service application_  SSA, требуется выполнить резервное. Не закрывайте окно Командная консоль SharePoint позже.

    ```powershell
    $ssa = Get-SpenterpriseSearchServiceApplication -Identity "name of search service application"
    Suspend-SPEnterpriseSearchServiceApplication -Identity $ssa
    ```

1. Выполните резервное копирование баз данных SSA и индекса, выполнив следующие действия:
1. На сервере с базами данных SSA выполните следующую команду в командной строке, где  _destination backup folder_  это полный путь к папке для резервных копий файлов, _backup log file_  это полный путь и имя файла резервной копии журнала и _SSA manifest file_  это путь и имя файла манифеста SSA.

    ```shell
    betest.exe /v /b /d "destination backup folder" /s "backup log file" /x "SSA manifest file"
    ```

1. На сервере с окном open Командная консоль SharePoint выполните указанную ниже команду, где  _topology file name_  это полный путь и имя экспортируемого файла, содержащего сведения о топологии. Необходимо использовать этот файл в процедуре восстановления для SSA.

    ```powershell
    Export-SPEnterpriseSearchTopology -SearchApplication $ssa -Filename "topology file name"
    ```

1. Убедитесь, что файл создан.
1. На каждом сервере, содержащий компонент индекса выполните следующую команду в командной строке, где  _destination backup folder_  это полный путь к папке для резервных копий файлов, _backup log file_  это полный путь и имя файла резервной копии журнала и _index manifest file_  это путь и имя файла манифеста индекса.

    ```shell
    betest.exe /v /b /d "destination backup folder" /s "backup log file" /x "index manifest file"
    ```

1. (Необязательно) Проверьте индекс папки, которые были созданы резервные копии. Убедитесь, что имена папок и размеры совпадают с учетными записями в предыдущем шаге.


### <a name="to-restore-a-sharepoint-search-service-application-using-vss"></a>Для восстановления приложения службы поиска SharePoint с помощью служба теневого копирования ТОМОВ


1. На любом сервере в ферме откройте Командная консоль SharePoint и выполните следующие команды для удаления существующего приложения службы поиска и его прокси-сервер, где  _name of search service application_ является SSA, которую требуется восстановить, а _name of proxy_  его прокси приложения. Обратите внимание, что этот _name of SSA proxy_  это обычно совпадает с именем SSA с слово "Прокси" добавлен в конец. Переключатель `RemoveData` гарантирует, что удаляются баз данных поиска.

    ```powershell
    $ssa = Get-SPEnterpriseSearchServiceApplication -Identity "name of search service application"
    Remove-SPEnterpriseSearchServiceApplication -Identity $ssa -RemoveData
    Remove-SPEnterpriseSearchServiceApplicationProxy -Identity "name of SSA proxy"
    ```

1. На том же сервере выполните следующую команду в командную строку для восстановления баз данных SSA, где  _destination backup folder_  это полный путь к папке для резервных копий файлов, _backup log file_  это полный путь и имя файла резервной копии журнала и _SSA manifest file_  это путь и имя файла манифеста SSA.

    ```shell
    betest.exe /v /r /d "destination backup folder" /s "backup log file" /x SSA_manifest_file
    ```

1. На том же сервере откройте Командная консоль SharePoint и выполните следующие строки, чтобы восстановить SSA, где  _application pool name_  это имя нового пула, _domain\\user_  это доменное имя пула приложений входит в систему в качестве пользователя, _name of the search service application_  это имя SSA и _topology_file_name_  это путь и имя файла топология, созданному при SSA была создана резервная копия.

    > [!TIP]
    > [!Совет] В этом коде создается новый удостоверения пула приложений для запуска восстановленных SSA, но можно также использовать существующую учетную запись с помощью командлета **Get-SPServiceApplicationPool**.

    ```powershell
    $applicationPool = New-SPServiceApplicationPool -name "application pool name" -account "domain\\user"
    Restore-SPEnterpriseSearchServiceApplication -Name "name of the search service application" -ApplicationPool $applicationPool -TopologyFile "topology_file_name" -KeepId
    ```

1. Создание прокси-сервера для SSA с помощью следующих командлетов. Мы рекомендуем использовать те же значения для  _name of the search service application_ и _name of SSA proxy_, как используется в шаге 1.

    ```powershell
    $ssa = Get-SpenterpriseSearchServiceApplication -Identity "name of search service application"
    New-SPEnterpriseSearchServiceApplicationProxy -Name "name of SSA proxy" -SearchApplication $ssa
    ```

1. (Необязательно) Проверьте существование SSA и его прокси-сервер, откройте **Центр администрирования**. Выберите **Управление приложениями-службами** и убедитесь, что указано SSA и его прокси-сервера.
1. (Необязательно) Нажмите кнопку SSA в списке служб и на открывшейся странице убедитесь, что в таблице **Топология приложения поиска** соответствует топология, который был экспортирован в процедуры резервного копирования. (Можно также проверить топологию с помощью командлета **Get-SPEnterpriseSearchStatus**.)
1. Восстановите файлы индекса, используя следующую процедуру **на всех серверах с компонентами индекса**.
1. Остановить хост-контроллер службы в **Администрирование > службы**, или выполнив следующий командлет в Командная консоль SharePoint:

    ```powershell
    stop-service SPSearchHostController
    ```

1. На тех же серверах выполните следующую команду в командной строке, где  _index manifest file_  это путь и имя файла манифеста индекса, созданный в процедуры резервного копирования.

    ```shell
    betest.exe /v /r /d "destination backup folder" /s "backup log file" /x "index manifest file"
    ```

1. (Необязательно) Убедитесь, что имена папок и размеры равны, записанные в процедуры резервного копирования.
1. Для каждого компонента индекса переименуйте данных в папке данных, выполнив следующие действия:
1. В Командная консоль SharePoint выполните следующий командлет.
    
    ```powershell
    Get-SPEnterpriseSearchVssDataPath
    ```

1. Выходные данные командлета запишите последнюю часть каждый идентификатор GUID. Например если одну строку выходных данных  `IndexComponentGroup_e255918b-6ab0-4d7c-8049-720b2744c62f`, запишите 720b2744c62f.
1. В **Обозревателе файлов** (или **Проводник** Windows Server 2008) перейдите к `C:\\Program Files\\Microsoft Office Servers\\15.0\\Data\\Office Server\\Applications\\Search\\Nodes\\24488A\\IndexComponentN\\storage\\data`, где  *N*   число компонент индекса.
1. Каждая из этих папок имеет вложенной папке, имя которых начинается с «Пакет обновления», а затем 12 шестнадцатеричных цифр, за которым следует номер версии. Для каждого из этих вложенных папок, в которых 12 шестнадцатеричных цифр соответствуют окончания идентификатор GUID, записанные в предыдущем шаге переименуйте вложенной папке в importindex. В качестве основного примера будет переименуйте вложенной папке  `SP720b2744c62f.1.I.1.0` вimportindex.
1. Перезапустить хост-контроллер службы в **Администрирование > службы**, или выполнив следующий командлет в Командная консоль SharePoint:

    ```powershell
    start-service SPSearchHostController
    ```

1. Убедитесь, что имена папок индекса данные возвращаются обратно в их предыдущее имя. (В качестве основного примера, это может быть "" SP720b2744c62f.1.I.1.0 ".)
1. (Необязательно) Проверьте соответствие размеры папок **IndexComponent** размеры, записанные в процедуры резервного копирования.
1. Перезапустите SSA.
1. На затронутых серверах запустите следующий командлет в Командная консоль SharePoint, чтобы проверить правильность работы приложения службы поиска:

    ```powershell
    Get-SPEnterpriseSearchStatus
    ```

1. Проверка работы передачи данных и поиска для новых документов. Например, проверьте размер индекса с помощью запроса "размер > = 0". Добавить новый документ и убедитесь, что для поиска.
    
  

## <a name="example-manifest-files"></a>Пример файлов манифестов
<a name="Examples"> </a>

 **Файл манифеста SSA**

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

 **Файл манифеста индекса**

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Службы Windows SharePoint Services и служба теневого копирования томов](http://msdn.microsoft.com/library/adae101a-078e-40b9-9cfa-db2cfb10270a%28Office.15%29.aspx)
    
  

