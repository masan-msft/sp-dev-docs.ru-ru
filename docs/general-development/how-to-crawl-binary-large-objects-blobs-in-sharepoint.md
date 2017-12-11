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
# <a name="crawl-binary-large-objects-blobs-in-sharepoint"></a><span data-ttu-id="b4946-102">Обход больших двоичных объектов (BLOB) в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4946-102">Crawl binary large objects (BLOBs) in SharePoint</span></span>

<span data-ttu-id="b4946-103">Узнайте, как можно модифицировать файл модели BCS для соединителя индексации BCS базы данных, чтобы включить программу-обходчик для Поиск в SharePoint для обхода больших двоичных объектов (BLOB), хранимых в базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b4946-103">Learn how to modify the BDC model file for a database BCS indexing connector to enable the Search in SharePoint crawler to crawl binary large object (BLOB) data stored in a SQL Server database.</span></span>

## <a name="crawling-blob-data"></a><span data-ttu-id="b4946-104">Обход данных объектов BLOB</span><span class="sxs-lookup"><span data-stu-id="b4946-104">Crawling BLOB data</span></span>
<span data-ttu-id="b4946-105"><a name="HowToCrawlBlobs_CrawlingBlobData"> </a></span><span class="sxs-lookup"><span data-stu-id="b4946-105"></span></span>

<span data-ttu-id="b4946-p101">Для поддержки Служба подключения к бизнес-данным (BDC) чтения типов данных больших двоичных ОБЪЕКТОВ, который можно использовать для потоковой передачи данных больших двоичных ОБЪЕКТОВ из внешних систем. Для этого необходимо проверить таблицы базы данных, содержащий внешних данных  это установки для этого. Метод **StreamAccessor** затем добавьте в файл модели BDC для соединителя индексации BCS внешнего контента источника.</span><span class="sxs-lookup"><span data-stu-id="b4946-p101">The Business Data Connectivity (BDC) service supports reading BLOB data types, which is useful for streaming BLOB data from external systems. For this to work, you need to ensure that the database table containing the external data is set up to support this. You then add a **StreamAccessor** method to the BDC model file for the external content source's BCS indexing connector.</span></span>
  
    
    

## <a name="configuring-the-sql-server-database-table-for-blob-data"></a><span data-ttu-id="b4946-109">Настройка таблицы базы данных SQL Server для данных больших двоичных ОБЪЕКТОВ</span><span class="sxs-lookup"><span data-stu-id="b4946-109">Configuring the SQL Server database table for BLOB data</span></span>
<span data-ttu-id="b4946-110"><a name="HowToCrawlBlobs_ConfiguringSQL"> </a></span><span class="sxs-lookup"><span data-stu-id="b4946-110"></span></span>

<span data-ttu-id="b4946-p102">Таблица базы данных Microsoft SQL Server должна содержать столбец, определяющий расширение или тип MIME для данных объектов BLOB. Если в схеме таблицы базы данных столбец, содержащий эти данные, отсутствует, необходимо добавить его в схему. В следующих таблицах представлен образец схемы таблицы базы данных, содержащие такой столбец, и образцы соответствующих значений, хранящиеся в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="b4946-p102">The Microsoft SQL Server database table must have a column that specifies either the extension or the MIME type of the BLOB data. If the database table schema does not include a column with this information, you must add it to the schema. The following tables contain an example of a database table schema with this column and sample values for it that are stored in the database table.</span></span>
  
    
    

<span data-ttu-id="b4946-114">**Таблица 1. Образец схемы таблицы базы данных**</span><span class="sxs-lookup"><span data-stu-id="b4946-114">**Table 1. Sample database table schema**</span></span>


|<span data-ttu-id="b4946-115">**Имя столбца**</span><span class="sxs-lookup"><span data-stu-id="b4946-115">**Column Name**</span></span>|<span data-ttu-id="b4946-116">**Тип данных**</span><span class="sxs-lookup"><span data-stu-id="b4946-116">**Data Type**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b4946-117">Id</span><span class="sxs-lookup"><span data-stu-id="b4946-117">Id</span></span>  <br/> |<span data-ttu-id="b4946-118">Int</span><span class="sxs-lookup"><span data-stu-id="b4946-118">Int</span></span>  <br/> |
|<span data-ttu-id="b4946-119">DisplayName</span><span class="sxs-lookup"><span data-stu-id="b4946-119">DisplayName</span></span>  <br/> |<span data-ttu-id="b4946-120">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="b4946-120">nvarchar(50)</span></span>  <br/> |
|<span data-ttu-id="b4946-121">Расширение</span><span class="sxs-lookup"><span data-stu-id="b4946-121">Extension</span></span>  <br/> |<span data-ttu-id="b4946-122">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="b4946-122">nvarchar(50)</span></span>  <br/> |
|<span data-ttu-id="b4946-123">Данные</span><span class="sxs-lookup"><span data-stu-id="b4946-123">Data</span></span>  <br/> |<span data-ttu-id="b4946-124">varbinary(MAX)</span><span class="sxs-lookup"><span data-stu-id="b4946-124">varbinary(MAX)</span></span>  <br/> |
|<span data-ttu-id="b4946-125">contentType</span><span class="sxs-lookup"><span data-stu-id="b4946-125">ContentType</span></span>  <br/> |<span data-ttu-id="b4946-126">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="b4946-126">nvarchar(MAX)</span></span>  <br/> |
   

<span data-ttu-id="b4946-127">**Таблица 2. Образцы значений таблицы базы данных**</span><span class="sxs-lookup"><span data-stu-id="b4946-127">**Table 2. Sample database table values**</span></span>


|<span data-ttu-id="b4946-128">**Id**</span><span class="sxs-lookup"><span data-stu-id="b4946-128">**Id**</span></span>|<span data-ttu-id="b4946-129">**Отображаемое имя**</span><span class="sxs-lookup"><span data-stu-id="b4946-129">**Display Name**</span></span>|<span data-ttu-id="b4946-130">**Расширение**</span><span class="sxs-lookup"><span data-stu-id="b4946-130">**Extension**</span></span>|<span data-ttu-id="b4946-131">**Данные**</span><span class="sxs-lookup"><span data-stu-id="b4946-131">**Data**</span></span>|<span data-ttu-id="b4946-132">**Тип контента**</span><span class="sxs-lookup"><span data-stu-id="b4946-132">**Content Type**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="b4946-133">1</span><span class="sxs-lookup"><span data-stu-id="b4946-133">1</span></span>  <br/> |<span data-ttu-id="b4946-134">File1</span><span class="sxs-lookup"><span data-stu-id="b4946-134">File1</span></span>  <br/> |<span data-ttu-id="b4946-135">.docx</span><span class="sxs-lookup"><span data-stu-id="b4946-135">.docx</span></span>  <br/> |<span data-ttu-id="b4946-136">0x504B…</span><span class="sxs-lookup"><span data-stu-id="b4946-136">0x504B…</span></span>  <br/> |<span data-ttu-id="b4946-137">application/vnd.openxmlformats-officedocument.wordprocessingml.document</span><span class="sxs-lookup"><span data-stu-id="b4946-137">application/vnd.openxmlformats-officedocument.wordprocessingml.document</span></span>  <br/> |
|<span data-ttu-id="b4946-138">2</span><span class="sxs-lookup"><span data-stu-id="b4946-138">2</span></span>  <br/> |<span data-ttu-id="b4946-139">File2</span><span class="sxs-lookup"><span data-stu-id="b4946-139">File2</span></span>  <br/> |<span data-ttu-id="b4946-140">DOC-файл</span><span class="sxs-lookup"><span data-stu-id="b4946-140">.doc</span></span>  <br/> |<span data-ttu-id="b4946-141">0xD...</span><span class="sxs-lookup"><span data-stu-id="b4946-141">0xD…</span></span>  <br/> |<span data-ttu-id="b4946-142">приложение/msword</span><span class="sxs-lookup"><span data-stu-id="b4946-142">application/msword</span></span>  <br/> |
|<span data-ttu-id="b4946-143">3</span><span class="sxs-lookup"><span data-stu-id="b4946-143">3</span></span>  <br/> |<span data-ttu-id="b4946-144">File3</span><span class="sxs-lookup"><span data-stu-id="b4946-144">File3</span></span>  <br/> |<span data-ttu-id="b4946-145">.txt</span><span class="sxs-lookup"><span data-stu-id="b4946-145">.txt</span></span>  <br/> |<span data-ttu-id="b4946-146">OxE...</span><span class="sxs-lookup"><span data-stu-id="b4946-146">OxE…</span></span>  <br/> |<span data-ttu-id="b4946-147">text/plain</span><span class="sxs-lookup"><span data-stu-id="b4946-147">text/plain</span></span>  <br/> |
   

## <a name="modifying-the-bdc-model-file-to-enable-crawling-of-blob-data"></a><span data-ttu-id="b4946-148">Изменение файла модели BDC для включения обхода данных больших двоичных ОБЪЕКТОВ</span><span class="sxs-lookup"><span data-stu-id="b4946-148">Modifying the BDC model file to enable crawling of BLOB data</span></span>
<span data-ttu-id="b4946-149"><a name="HowToCrawlBlobs_BDCModelFile"> </a></span><span class="sxs-lookup"><span data-stu-id="b4946-149"></span></span>

<span data-ttu-id="b4946-p103">После проверки того, что в таблице базы данных содержит расширение или сведения о типе MIME для данных больших двоичных ОБЪЕКТОВ, Microsoft SharePoint Designer можно использовать для создания внешнего типа контента, основанный на таблицу, содержащую данные больших двоичных ОБЪЕКТОВ. Затем можно создать все операции. Для получения дополнительных сведений см  [Создание внешних типов контента](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx) и [Инструкции. Создание внешнего типа контента на основе таблицы SQL Server](http://msdn.microsoft.com/library/5c42a679-d71d-46c6-aabc-d63c6cad3846%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4946-p103">After you confirm that the database table contains the extension or MIME type information for the BLOB data, you can use Microsoft SharePoint Designer to create an external content type that is based on the table containing the BLOB data. Then, you can create all the operations. For more information, see  [How to: Create External Content Types](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx) and [How to: Create an External Content Type Based on a SQL Server Table](http://msdn.microsoft.com/library/5c42a679-d71d-46c6-aabc-d63c6cad3846%28Office.15%29.aspx).</span></span> 
  
    
    
<span data-ttu-id="b4946-p104">После создания внешнего типа контента объектов BLOB, все готово для изменения файла модели BDC для включения функции обхода контента. Не удается внести эти изменения в SharePoint Designer. Поэтому необходимо экспортировать файл модели BDC и использовать редактор XML, чтобы выполнить эти изменения вручную.</span><span class="sxs-lookup"><span data-stu-id="b4946-p104">After you create the BLOB external content type, you are ready to modify the BDC model file to enable crawling. You cannot make these modifications in SharePoint Designer. So you must export the BDC model file, and use an XML editor to make these changes manually.</span></span>
  
    
    

### <a name="to-export-the-bdc-model-file-for-the-blob-external-content-type"></a><span data-ttu-id="b4946-156">Экспорт файла модели подключения к бизнес-данным для внешнего типа контента объектов BLOB</span><span class="sxs-lookup"><span data-stu-id="b4946-156">To export the BDC model file for the BLOB external content type</span></span>


1. <span data-ttu-id="b4946-157">В SharePoint Designer щелкните **Внешние типы контента** в левой панели навигации для отображения внешних типов контента, определенных в том, что хранилища метаданных BDC веб-узла этого приложения-службы.</span><span class="sxs-lookup"><span data-stu-id="b4946-157">In SharePoint Designer, click **External Content Types** in the left navigation to display the external content types that are defined in that site's service application's BDC metadata store.</span></span>
    
  
2. <span data-ttu-id="b4946-p105">В списке **Внешние типы контента** выберите внешний тип контента объектов BLOB. После этого нажмите **Экспорт модели подключения к бизнес-данным** на Лента сервера.</span><span class="sxs-lookup"><span data-stu-id="b4946-p105">In the **External Content Types** list, select the BLOB external content type. Then, click **Export BDC Model** on the Server ribbon.</span></span>
    
  
3. <span data-ttu-id="b4946-160">Введите имя в текстовом поле **Имя модели подключения к бизнес-данным** и нажмите **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4946-160">Type a name in the **BDC Model Name** text box, and then click **OK**.</span></span>
    
  
4. <span data-ttu-id="b4946-161">Выберите путь для сохранения файла модели BDC (BDCM) и нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b4946-161">Select the location where you want to save the BDC model (.bdcm) file, and then click **Save**.</span></span>
    
  

### <a name="to-enable-crawling-of-the-blob-external-content-type"></a><span data-ttu-id="b4946-162">Включение обхода для внешнего типа контента объектов BLOB</span><span class="sxs-lookup"><span data-stu-id="b4946-162">To enable crawling of the BLOB external content type</span></span>


1. <span data-ttu-id="b4946-163">В редакторе XML откройте файл модели BDC, создание которого описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="b4946-163">In an XML editor, open the BDC model file you created in the previous section.</span></span>
    
  
2. <span data-ttu-id="b4946-p106">Создайте новый метод, возвращающий поле объектов BLOB. Необходимо определить экземпляр метода типа **StreamAccessor** для этого метода, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b4946-p106">Create a new method that returns the BLOB field. You should define a **StreamAccessor** type method instance for this method, as shown in the following example.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b4946-166">[!Примечание] В этом примере используется имя таблицы «Attachment».</span><span class="sxs-lookup"><span data-stu-id="b4946-166">The table name in this example is Attachment.</span></span> 

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
  
    
    
<span data-ttu-id="b4946-167">следующей строкой кода:</span><span class="sxs-lookup"><span data-stu-id="b4946-167">with the following line of code:</span></span> 
  
    
    
 `<Property Name=" ContentType " Type="System.String">application/vnd.openxmlformats-officedocument.wordprocessingml.document</Property>`
    
  
3. <span data-ttu-id="b4946-168">Повторно импортируйте файл модели с помощью Business Connectivity Services администрирования приложения-службы пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b4946-168">Re-import the model file by using the Business Connectivity Services service application administration UI.</span></span> 
    
  
4. <span data-ttu-id="b4946-169">Создание источника контента для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="b4946-169">Create the content source for the external content type.</span></span>
    
  
5. <span data-ttu-id="b4946-170">Запустите полный обход источника контента.</span><span class="sxs-lookup"><span data-stu-id="b4946-170">Launch a full crawl of the content source.</span></span> 
    
  

## <a name="see-also"></a><span data-ttu-id="b4946-171">См. также</span><span class="sxs-lookup"><span data-stu-id="b4946-171">See also</span></span>
<span data-ttu-id="b4946-172"><a name="SP15Crawlblobs_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b4946-172"></span></span>


-  [<span data-ttu-id="b4946-173">Инфраструктура соединителей поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b4946-173">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b4946-174">Создание внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="b4946-174">How to: Create External Content Types</span></span>](http://msdn.microsoft.com/library/811b458c-e209-46df-ba02-8db02bc658db%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="b4946-175">Фрагмент XML-кода: моделирование метода StreamAccessor</span><span class="sxs-lookup"><span data-stu-id="b4946-175">XML Snippet: Modeling a StreamAccessor Method</span></span>](http://msdn.microsoft.com/library/bd60cc2e-f7f6-421c-9d2a-60e8512b9893%28Office.15%29.aspx)
    
  

