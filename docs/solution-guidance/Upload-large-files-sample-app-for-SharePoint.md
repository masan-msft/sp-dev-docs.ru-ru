---
title: "Загрузка больших файлов примера надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a6c04ffcdf8d6714250dee1ba0709c869c338b9f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upload-large-files-sample-add-in-for-sharepoint"></a>Загрузка больших файлов примера надстройки для SharePoint

Передавать файлы, размер которых превышает 2 МБ для SharePoint и SharePoint Online с помощью SaveBinaryDirect, ContentStream, StartUpload, ContinueUpload и FinishUpload. 

_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_

[Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) примере показано, как использовать размещение у поставщика в надстройке для отправки больших файлов в SharePoint, а также пропускать ограничение на передачу файлов 2 МБ. Используйте это решение, если вы хотите отправить файлы, размер которых превышает 2 МБ для SharePoint. В этом примере запускается как консольное приложение, которое отправляет большие файлы в библиотеке документов, используя один из следующих методов:

- ** [SaveBinaryDirect](https://msdn.microsoft.com/library/office/ee538285.aspx)** метод в классе **Microsoft.SharePoint.Client.File** .
    
- ** [ContentStream](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.contentstream.aspx)** свойства класса **FileCreationInformation** .
    
- ** [StartUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.startupload.aspx)**, ** [ContinueUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.continueupload.aspx) ** и ** [FinishUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.finishupload.aspx)** методов класса **файла** .
    
В следующей таблице перечислены методы передачи файлов, которые доступны и описывает способы использования каждого метода.

**Параметры для загрузки файлов**

|**Параметр Отправить файл**|**Сведения о выполнении**|**Когда это следует использовать?**|**Поддерживаемые платформы**|
|:-----|:-----|:-----|:-----|
| Свойство [содержимого](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.content.aspx) на класс **FileCreationInformation** .|Максимальный размер файла, который можно загрузить — 2 МБ. Время ожидания истекает через 30 минут.|Используйте для загрузки файлов, которые являются только менее 2 МБ. |SharePoint Server 2013, SharePoint Online|
| Метод **SaveBinaryDirect** класса **файла** .|Нет ограничений на размер файла. Время ожидания истекает через 30 минут.|Используйте этот метод только в том случае, если вы используете политику проверки подлинности пользователя. Политики проверки подлинности пользователя недоступны в надстройки уровня приложения для SharePoint, но можно использовать в собственный устройства приложений, Windows PowerShell и консольных приложений Windows.|SharePoint Server 2013, SharePoint Online|
| Свойство **ContentStream** класса **FileCreationInformation** .|Нет ограничений на размер файла. Время ожидания истекает через 30 минут.|Рекомендуется для:<br/>-SharePoint Server 2013.<br/>-SharePoint Online, если файл меньше 10 МБ.|SharePoint Server 2013, SharePoint Online|
|Загрузите файл как набор фрагментов, с помощью методов **StartUpload**, **ContinueUpload**и **FinishUpload** **файл** класса.|Нет ограничений на размер файла. Время ожидания истекает через 30 минут. Каждый блок файла необходимо загрузить несколько 30 минут после завершения предыдущих блока, чтобы избежать тайм-аута. |Рекомендуется для SharePoint Online, если файл превышает 10 МБ.|SharePoint Online|

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-corelargefileupload-sample-app"></a>Использование примера приложения Core.LargeFileUpload
<a name="sectionSection1"> </a>

При запуске в этом примере отображается консольное приложение. Необходимо указать SharePoint Online URL-адрес сайта семейства сайтов и учетные данные для входа для Office 365. После проверки подлинности консольное приложение отображает исключение. Исключение происходит, когда с помощью метода **UploadDocumentContent** в FileUploadService.cs пытается использовать свойство **FileCreationInformation.Content** для отправки файла, размер которого превышает 2 МБ. **UploadDocumentContent** также создает библиотеки документов, именем **: документы** , если он еще не существует. Далее в этом примере кода используется в библиотеке **документов** .

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
public void UploadDocumentContent(ClientContext ctx, string libraryName, string filePath)
        {
            Web web = ctx.Web;

            // Ensure that target library exists. Create if it is missing.
            if (!LibraryExists(ctx, web, libraryName))
            {
                CreateLibrary(ctx, web, libraryName);
            }

            FileCreationInformation newFile = new FileCreationInformation();

         // The next line of code causes an exception to be thrown for files larger than 2 MB.
            newFile.Content = System.IO.File.ReadAllBytes(filePath);
            newFile.Url = System.IO.Path.GetFileName(filePath);

            // Get instances to the given library.
            List docs = web.Lists.GetByTitle(libraryName);
            
 // Add file to the library.
            Microsoft.SharePoint.Client.File uploadFile = docs.RootFolder.Files.Add(newFile);
            ctx.Load(uploadFile);
            ctx.ExecuteQuery();
        } 

```

В FileUploadService.cs в этом примере кода предоставляет три варианта, которые можно использовать для отправки больших файлов в библиотеку документов.

- Метод **File.SaveBinaryDirect** .
    
- Свойство **FileCreationInformation.ContentStream** .
    
- Методы **StartUpload**, **ContinueUpload**и **FinishUpload** на **файл** классов.
    
В FileUploadService.cs **SaveBinaryDirect** использует метод **Microsoft.SharePoint.Client.File.SaveBinaryDirect** с помощью объекта **FileStream** для загрузки файлов в библиотеку документов.

```C#
public void SaveBinaryDirect(ClientContext ctx, string libraryName, string filePath)
        {
            Web web = ctx.Web;
            // Ensure that the target library exists. Create it if it is missing.
            if (!LibraryExists(ctx, web, libraryName))
            {
                CreateLibrary(ctx, web, libraryName);
            }

            using (FileStream fs = new FileStream(filePath, FileMode.Open))
            {
                Microsoft.SharePoint.Client.File.SaveBinaryDirect(ctx, string.Format("/{0}/{1}", libraryName, System.IO.Path.GetFileName(filePath)), fs, true);
            }

        } 

```

В FileUploadService.cs **UploadDocumentContentStream** использует свойство **FileCreationInformation.ContentStream** с помощью объекта **FileStream** для передачи файла в библиотеку документов.

```C#
public void UploadDocumentContentStream(ClientContext ctx, string libraryName, string filePath)
        {

            Web web = ctx.Web;
            // Ensure that the target library exists. Create it if it is missing.
            if (!LibraryExists(ctx, web, libraryName))
            {
                CreateLibrary(ctx, web, libraryName);
            }

            using (FileStream fs = new FileStream(filePath, FileMode.Open))
            {
                FileCreationInformation flciNewFile = new FileCreationInformation();

                // This is the key difference for the first case - using ContentStream property
                flciNewFile.ContentStream = fs;
                flciNewFile.Url = System.IO.Path.GetFileName(filePath);
                flciNewFile.Overwrite = true;

                List docs = web.Lists.GetByTitle(libraryName);
                Microsoft.SharePoint.Client.File uploadFile = docs.RootFolder.Files.Add(flciNewFile);

                ctx.Load(uploadFile);
                ctx.ExecuteQuery();
            }
        }

```

В FileUploadService.cs **UploadFileSlicePerSlice** отправляет большого файла в библиотеке документов как набор блоки или фрагментов. **UploadFileSlicePerSlice** выполняет следующие задачи:

1. Получает новый GUID. Отправка файла в виде фрагментов, необходимо использовать уникальный идентификатор GUID. 
    
2. Вычисляет размер блока фрагмента в байтах. Чтобы вычислить размер блока в байтах, **UploadFileSlicePerSlice** использует **fileChunkSizeInMB**, который определяет размер отдельных фрагментов в МБ. 
    
3. Тесты, если размер файла для загрузки ( **размер файла**) меньше или равно размер блока ( **размер блока**).
    
    1. Если **размер файла** меньше или равно размер блока, позволяет гарантировать по-прежнему передачи файла с помощью свойства **FileCreationInformation.ContentStream** . Имейте в виду, что размер блока рекомендуемые 10 МБ или больше.
      
    2. Если **размер файла** превышает размер блока:
    
        1. Часть файла считывается в **буфер**.
    
        2. Если размер блока равен размер файла, считывания весь файл. Блока копируется в **lastBuffer**.  **lastBuffer** используется **File.FinishUpload** , чтобы отправить блока.
    
    3. Если размер блока не равно размер файла, имеется несколько блоков для чтения из файла.  Отправка первого блока называется **File.StartUpload** . **fileoffset**, используемый в качестве начальной точки следующего блока, затем задается число байтов, переданных с первого блока. Следующий фрагмент считывается, если последнего блока не достигнуто, **File.ContinueUpload** называется отправка следующая часть файла. Процесс повторяется до последнего часть считывается. При чтении последнего блока **File.FinishUpload** загружает последнего блока и сохраняет файл. Содержимое файла затем изменены после завершения этого метода.

> [!NOTE] 
> Необходимо учитывайте следующие рекомендации:
- Используйте механизм повторных попыток в случае отправки прерывается. При прерывании загружаемого файла файл называется незаконченный файла. Вы можете перезапустить Отправка незаконченный файла сразу после загрузки была прервана. Незаконченный файлы удаляются из server от 6 часов до 24 часов после прерывания незаконченный файла. Этот период удаления может изменяться без предварительного уведомления.
- После отправки файла в виде фрагментов в SharePoint Online, блокировки ставится на файл в SharePoint Online. При прерывании файл остается заблокированным 15 минут. Если следующая часть файла не загружаться в SharePoint Online в течение 15 минут, удаляется блокировки. После удаления блокировки можно возобновить отправку пользователями или другой пользователь может запустить отправки файла в. Если другой пользователь запускает отправки файла в, незаконченный файл удаляется из SharePoint Online. Период времени, блокировка остается в файл после прерывания передаваемых можно изменить без предварительного уведомления.
- Можно изменить размер блока. Рекомендуется использовать размер блока 10 МБ.
- Возобновите прервано блока, отслеживание которых фрагментов отправлен успешно.

Блоки, нужно передать последовательно. Не удается загрузить фрагменты одновременно (например, с помощью многопоточные подход).

```
 public Microsoft.SharePoint.Client.File UploadFileSlicePerSlice(ClientContext ctx, string libraryName, string fileName, int fileChunkSizeInMB = 3)
        {
            // Each sliced upload requires a unique ID.
            Guid uploadId = Guid.NewGuid();

            // Get the name of the file.
            string uniqueFileName = Path.GetFileName(fileName);

            // Ensure that target library exists, and create it if it is missing.
            if (!LibraryExists(ctx, ctx.Web, libraryName))
            {
                CreateLibrary(ctx, ctx.Web, libraryName);
            }
            // Get the folder to upload into. 
            List docs = ctx.Web.Lists.GetByTitle(libraryName);
            ctx.Load(docs, l => l.RootFolder);
            // Get the information about the folder that will hold the file.
            ctx.Load(docs.RootFolder, f => f.ServerRelativeUrl);
            ctx.ExecuteQuery();

            // File object.
            Microsoft.SharePoint.Client.File uploadFile;

            // Calculate block size in bytes.
            int blockSize = fileChunkSizeInMB * 1024 * 1024;

            // Get the information about the folder that will hold the file.
            ctx.Load(docs.RootFolder, f => f.ServerRelativeUrl);
            ctx.ExecuteQuery();


            // Get the size of the file.
            long fileSize = new FileInfo(fileName).Length;

            if (fileSize <= blockSize)
            {
                // Use regular approach.
                using (FileStream fs = new FileStream(fileName, FileMode.Open))
                {
                    FileCreationInformation fileInfo = new FileCreationInformation();
                    fileInfo.ContentStream = fs;
                    fileInfo.Url = uniqueFileName;
                    fileInfo.Overwrite = true;
                    uploadFile = docs.RootFolder.Files.Add(fileInfo);
                    ctx.Load(uploadFile);
                    ctx.ExecuteQuery();
                    // Return the file object for the uploaded file.
                    return uploadFile;
                }
            }
            else
            {
                // Use large file upload approach.
                ClientResult<long> bytesUploaded = null;

                FileStream fs = null;
                try
                {
                    fs = System.IO.File.Open(fileName, FileMode.Open, FileAccess.Read, FileShare.ReadWrite);
                    using (BinaryReader br = new BinaryReader(fs))
                    {
                        byte[] buffer = new byte[blockSize];
                        Byte[] lastBuffer = null;
                        long fileoffset = 0;
                        long totalBytesRead = 0;
                        int bytesRead;
                        bool first = true;
                        bool last = false;

                        // Read data from file system in blocks. 
                        while ((bytesRead = br.Read(buffer, 0, buffer.Length)) > 0)
                        {
                            totalBytesRead = totalBytesRead + bytesRead;

                            // You've reached the end of the file.
                            if (totalBytesRead == fileSize)
                            {
                                last = true;
                                // Copy to a new buffer that has the correct size.
                                lastBuffer = new byte[bytesRead];
                                Array.Copy(buffer, 0, lastBuffer, 0, bytesRead);
                            }

                            if (first)
                            {
                                using (MemoryStream contentStream = new MemoryStream())
                                {
                                    // Add an empty file.
                                    FileCreationInformation fileInfo = new FileCreationInformation();
                                    fileInfo.ContentStream = contentStream;
                                    fileInfo.Url = uniqueFileName;
                                    fileInfo.Overwrite = true;
                                    uploadFile = docs.RootFolder.Files.Add(fileInfo);

                                    // Start upload by uploading the first slice. 
                                    using (MemoryStream s = new MemoryStream(buffer))
                                    {
                                        // Call the start upload method on the first slice.
                                        bytesUploaded = uploadFile.StartUpload(uploadId, s);
                                        ctx.ExecuteQuery();
                                        // fileoffset is the pointer where the next slice will be added.
                                        fileoffset = bytesUploaded.Value;
                                    }

                                    // You can only start the upload once.
                                    first = false;
                                }
                            }
                            else
                            {
                                // Get a reference to your file.
                                uploadFile = ctx.Web.GetFileByServerRelativeUrl(docs.RootFolder.ServerRelativeUrl + System.IO.Path.AltDirectorySeparatorChar + uniqueFileName);

                                if (last)
                                {
                                    // Is this the last slice of data?
                                    using (MemoryStream s = new MemoryStream(lastBuffer))
                                    {
                                        // End sliced upload by calling FinishUpload.
                                        uploadFile = uploadFile.FinishUpload(uploadId, fileoffset, s);
                                        ctx.ExecuteQuery();

                                        // Return the file object for the uploaded file.
                                        return uploadFile;
                                    }
                                }
                                else
                                {
                                    using (MemoryStream s = new MemoryStream(buffer))
                                    {
                                        // Continue sliced upload.
                                        bytesUploaded = uploadFile.ContinueUpload(uploadId, fileoffset, s);
                                        ctx.ExecuteQuery();
                                        // Update fileoffset for the next slice.
                                        fileoffset = bytesUploaded.Value;
                                    }
                                }
                            }

                        } // while ((bytesRead = br.Read(buffer, 0, buffer.Length)) > 0)
                    }
                }
                finally
                {
                    if (fs != null)
                    {
                        fs.Dispose();
                    }
                }
            }

            return null;
        }
```

После завершения пример кода на узле Office 365, можно перейти в библиотеку **документов** , выбрав **последние** > **документов**. Убедитесь, что в библиотеке **документов** содержит три больших файлов.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление контентом корпоративных решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Пример Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader)
