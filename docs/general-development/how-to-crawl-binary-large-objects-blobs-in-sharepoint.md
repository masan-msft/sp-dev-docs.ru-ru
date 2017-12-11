---
title: "Обход больших двоичных объектов (BLOB) в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 99b3dd51-1651-4300-a2de-33681f4cc258
ms.openlocfilehash: 7b2804c5e24e5938ced28926626f2e21a8eb2993
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="crawl-binary-large-objects-blobs-in-sharepoint"></a>Обход больших двоичных объектов (BLOB) в SharePoint

Узнайте, как можно модифицировать файл модели BCS для соединителя индексации BCS базы данных, чтобы включить программу-обходчик для Поиск в SharePoint для обхода больших двоичных объектов (BLOB), хранимых в базе данных SQL Server.

## <a name="crawling-blob-data"></a>Обход данных объектов BLOB
<a name="HowToCrawlBlobs_CrawlingBlobData"> </a>

Для поддержки Служба подключения к бизнес-данным (BDC) чтения типов данных больших двоичных ОБЪЕКТОВ, который можно использовать для потоковой передачи данных больших двоичных ОБЪЕКТОВ из внешних систем. Для этого необходимо проверить таблицы базы данных, содержащий внешних данных  это установки для этого. Метод **StreamAccessor** затем добавьте в файл модели BDC для соединителя индексации BCS внешнего контента источника.
  
    
    

## <a name="configuring-the-sql-server-database-table-for-blob-data"></a>Настройка таблицы базы данных SQL Server для данных больших двоичных ОБЪЕКТОВ
<a name="HowToCrawlBlobs_ConfiguringSQL"> </a>

Таблица базы данных Microsoft SQL Server должна содержать столбец, определяющий расширение или тип MIME для данных объектов BLOB. Если в схеме таблицы базы данных столбец, содержащий эти данные, отсутствует, необходимо добавить его в схему. В следующих таблицах представлен образец схемы таблицы базы данных, содержащие такой столбец, и образцы соответствующих значений, хранящиеся в таблице базы данных.
  
    
    

**Таблица 1. Образец схемы таблицы базы данных**


|**Имя столбца**|**Тип данных**|
|:-----|:-----|
|Id  <br/> |Int  <br/> |
|DisplayName  <br/> |nvarchar(50)  <br/> |
|Расширение  <br/> |nvarchar(50)  <br/> |
|Данные  <br/> |varbinary(MAX)  <br/> |
|contentType  <br/> |nvarchar(MAX)  <br/> |
   

**Таблица 2. Образцы значений таблицы базы данных**


|**Id**|**Отображаемое имя**|**Расширение**|**Данные**|**Тип контента**|
|:-----|:-----|:-----|:-----|:-----|
|1  <br/> |File1  <br/> |.docx  <br/> |0x504B…  <br/> |application/vnd.openxmlformats-officedocument.wordprocessingml.document  <br/> |
|2  <br/> |File2  <br/> |DOC-файл  <br/> |0xD...  <br/> |приложение/msword  <br/> |
|3  <br/> |File3  <br/> |.txt  <br/> |OxE...  <br/> |text/plain  <br/> |
   

## <a name="modifying-the-bdc-model-file-to-enable-crawling-of-blob-data"></a>Изменение файла модели BDC для включения обхода данных больших двоичных ОБЪЕКТОВ
<a name="HowToCrawlBlobs_BDCModelFile"> </a>

После проверки того, что в таблице базы данных содержит расширение или сведения о типе MIME для данных больших двоичных ОБЪЕКТОВ, Microsoft SharePoint Designer можно использовать для создания внешнего типа контента, основанный на таблицу, содержащую данные больших двоичных ОБЪЕКТОВ. Затем можно создать все операции. Для получения дополнительных сведений см  [Создание внешних типов контента](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx) и [Инструкции. Создание внешнего типа контента на основе таблицы SQL Server](http://msdn.microsoft.com/library/5c42a679-d71d-46c6-aabc-d63c6cad3846%28Office.15%29.aspx). 
  
    
    
После создания внешнего типа контента объектов BLOB, все готово для изменения файла модели BDC для включения функции обхода контента. Не удается внести эти изменения в SharePoint Designer. Поэтому необходимо экспортировать файл модели BDC и использовать редактор XML, чтобы выполнить эти изменения вручную.
  
    
    

### <a name="to-export-the-bdc-model-file-for-the-blob-external-content-type"></a>Экспорт файла модели подключения к бизнес-данным для внешнего типа контента объектов BLOB


1. В SharePoint Designer щелкните **Внешние типы контента** в левой панели навигации для отображения внешних типов контента, определенных в том, что хранилища метаданных BDC веб-узла этого приложения-службы.
    
  
2. В списке **Внешние типы контента** выберите внешний тип контента объектов BLOB. После этого нажмите **Экспорт модели подключения к бизнес-данным** на Лента сервера.
    
  
3. Введите имя в текстовом поле **Имя модели подключения к бизнес-данным** и нажмите **OK**.
    
  
4. Выберите путь для сохранения файла модели BDC (BDCM) и нажмите **Сохранить**.
    
  

### <a name="to-enable-crawling-of-the-blob-external-content-type"></a>Включение обхода для внешнего типа контента объектов BLOB


1. В редакторе XML откройте файл модели BDC, создание которого описано в предыдущем разделе.
    
  
2. Создайте новый метод, возвращающий поле объектов BLOB. Необходимо определить экземпляр метода типа **StreamAccessor** для этого метода, как показано в следующем примере.
    
    > [!NOTE]
    > [!Примечание] В этом примере используется имя таблицы «Attachment». 

```XML
  
<Method Name="GetData">
  <Properties>
    <Property Name="RdbCommandText" Type="System.String">SELECT Data FROM [dbo].[Attachment] WHERE [Id] = @Id </Property>
    <Property Name="RdbCommandType" Type="System.Data.CommandType, System.Data, Version=2.0.0.0, Culture=neutral, 
      PublicKeyToken=b77a5c561934e089">Text</Property>
  </Properties>
  <Parameters>
    <Parameter Direction="In" Name="@Id">
      <TypeDescriptor TypeName="System.Int32" IdentifierName="Id" Name="Id" />
    </Parameter>
    <Parameter Name="StreamData" Direction="Return">
      <TypeDescriptor TypeName="System.Data.IDataReader, System.Data, 
        Version=2.0.3600.0, Culture=neutral, 
        PublicKeyToken=b77a5c561934e089" 
        IsCollection="true" Name="DataReaderTypeDescriptorName">
        <TypeDescriptors>
          <TypeDescriptor TypeName="System.Data.IDataRecord, System.Data, 
            Version=2.0.3600.0, 
            Culture=neutral, 
            PublicKeyToken=b77a5c561934e089" 
            Name="DataRecordTypeDescriptorName">
            <TypeDescriptors>
              <TypeDescriptor TypeName="System.Data.SqlTypes.SqlBytes, System.Data, 
                Version=2.0.3600.0, 
                Culture=neutral, 
                PublicKeyToken=b77a5c561934e089" Name="Data" />
            </TypeDescriptors>
          </TypeDescriptor>
        </TypeDescriptors>
      </TypeDescriptor>
     </Parameter>
    </Parameters>
  <MethodInstances>
    <MethodInstance Name="DataAccessor" 
      Type="StreamAccessor" 
      ReturnParameterName="StreamData" 
      ReturnTypeDescriptorName="Data">
      <Properties>
<!-- If extension field is available-->
        <Property Name="Extension" Type="System.String">Extension</Property>
<!--If MimeType is available-->
        <Property Name="ContentType" Type="System.String">ContentType</Property>
<!--If attachments is to be displayed in profile pages, add the following property-->
        <Property Name="MimeTypeField" Type="System.String">ContentType</Property>
      </Properties>
    </MethodInstance>
  </MethodInstances>
</Method>
```


    If the MIME type is the same for all the BLOBs, you can replace this line of code from the previous example: 
  
    
    
 `<Property Name="ContentType" Type="System.String">ContentType</Property>`
  
    
    
следующей строкой кода: 
  
    
    
 `<Property Name=" ContentType " Type="System.String">application/vnd.openxmlformats-officedocument.wordprocessingml.document</Property>`
    
  
3. Повторно импортируйте файл модели с помощью Business Connectivity Services администрирования приложения-службы пользовательского интерфейса. 
    
  
4. Создание источника контента для внешнего типа контента.
    
  
5. Запустите полный обход источника контента. 
    
  

## <a name="see-also"></a>См. также
<a name="SP15Crawlblobs_addlresources"> </a>


-  [Инфраструктура соединителей поиска в SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Создание внешних типов контента](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx)
    
  
-  [Фрагмент XML-кода: моделирование метода StreamAccessor](http://msdn.microsoft.com/library/bd60cc2e-f7f6-421c-9d2a-60e8512b9893%28Office.15%29.aspx)
    
  

