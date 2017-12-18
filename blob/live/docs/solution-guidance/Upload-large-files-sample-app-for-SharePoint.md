---
title: "Загрузка больших файлов примера надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a6c04ffcdf8d6714250dee1ba0709c869c338b9f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upload-large-files-sample-add-in-for-sharepoint"></a><span data-ttu-id="16a46-102">Загрузка больших файлов примера надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="16a46-102">Upload large files sample add-in for SharePoint</span></span>

<span data-ttu-id="16a46-103">Передавать файлы, размер которых превышает 2 МБ для SharePoint и SharePoint Online с помощью SaveBinaryDirect, ContentStream, StartUpload, ContinueUpload и FinishUpload.</span><span class="sxs-lookup"><span data-stu-id="16a46-103">Upload files larger than 2MB to SharePoint and SharePoint Online using SaveBinaryDirect, ContentStream, StartUpload, ContinueUpload and FinishUpload.</span></span> 

<span data-ttu-id="16a46-104">_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="16a46-104">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="16a46-105">[Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) примере показано, как использовать размещение у поставщика в надстройке для отправки больших файлов в SharePoint, а также пропускать ограничение на передачу файлов 2 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-105">The  [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) sample shows you how to use a provider-hosted add-in to upload large files to SharePoint, and how to bypass the 2 MB file upload limit.</span></span> <span data-ttu-id="16a46-106">Используйте это решение, если вы хотите отправить файлы, размер которых превышает 2 МБ для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="16a46-106">Use this solution if you want to upload files that are larger than 2 MB to SharePoint.</span></span> <span data-ttu-id="16a46-107">В этом примере запускается как консольное приложение, которое отправляет большие файлы в библиотеке документов, используя один из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="16a46-107">This sample runs as a console application that uploads large files to a document library by using one of the following methods:</span></span>

- <span data-ttu-id="16a46-108">** [SaveBinaryDirect](https://msdn.microsoft.com/library/office/ee538285.aspx)** метод в классе **Microsoft.SharePoint.Client.File** .</span><span class="sxs-lookup"><span data-stu-id="16a46-108">The  ** [SaveBinaryDirect](https://msdn.microsoft.com/library/office/ee538285.aspx)** method on the **Microsoft.SharePoint.Client.File** class.</span></span>
    
- <span data-ttu-id="16a46-109">** [ContentStream](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.contentstream.aspx)** свойства класса **FileCreationInformation** .</span><span class="sxs-lookup"><span data-stu-id="16a46-109">The  ** [ContentStream](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.contentstream.aspx)** property on the **FileCreationInformation** class.</span></span>
    
- <span data-ttu-id="16a46-110">** [StartUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.startupload.aspx)**, ** [ContinueUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.continueupload.aspx) ** и ** [FinishUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.finishupload.aspx)** методов класса **файла** .</span><span class="sxs-lookup"><span data-stu-id="16a46-110">The  ** [StartUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.startupload.aspx)**,  ** [ContinueUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.continueupload.aspx)** and ** [FinishUpload](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.finishupload.aspx)** methods on the **File** class.</span></span>
    
<span data-ttu-id="16a46-111">В следующей таблице перечислены методы передачи файлов, которые доступны и описывает способы использования каждого метода.</span><span class="sxs-lookup"><span data-stu-id="16a46-111">The following table lists the file upload methods that are available and describes when to use each method.</span></span>

<span data-ttu-id="16a46-112">**Параметры для загрузки файлов**</span><span class="sxs-lookup"><span data-stu-id="16a46-112">**Options for uploading files**</span></span>

|<span data-ttu-id="16a46-113">**Параметр Отправить файл**</span><span class="sxs-lookup"><span data-stu-id="16a46-113">**File upload option**</span></span>|<span data-ttu-id="16a46-114">**Сведения о выполнении**</span><span class="sxs-lookup"><span data-stu-id="16a46-114">**Considerations**</span></span>|<span data-ttu-id="16a46-115">**Когда это следует использовать?**</span><span class="sxs-lookup"><span data-stu-id="16a46-115">**When should you use this?**</span></span>|<span data-ttu-id="16a46-116">**Поддерживаемые платформы**</span><span class="sxs-lookup"><span data-stu-id="16a46-116">**Supported platforms**</span></span>|
|:-----|:-----|:-----|:-----|
| <span data-ttu-id="16a46-117">Свойство [содержимого](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.content.aspx) на класс **FileCreationInformation** .</span><span class="sxs-lookup"><span data-stu-id="16a46-117">[Content](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.content.aspx) property on the **FileCreationInformation** class.</span></span>|<span data-ttu-id="16a46-118">Максимальный размер файла, который можно загрузить — 2 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-118">Maximum file size that can be uploaded is 2 MB.</span></span> <span data-ttu-id="16a46-119">Время ожидания истекает через 30 минут.</span><span class="sxs-lookup"><span data-stu-id="16a46-119">Time-out occurs after 30 minutes.</span></span>|<span data-ttu-id="16a46-120">Используйте для загрузки файлов, которые являются только менее 2 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-120">Use to upload files that are less than 2 MB only.</span></span> |<span data-ttu-id="16a46-121">SharePoint Server 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="16a46-121">SharePoint Server 2013, SharePoint Online</span></span>|
| <span data-ttu-id="16a46-122">Метод **SaveBinaryDirect** класса **файла** .</span><span class="sxs-lookup"><span data-stu-id="16a46-122">**SaveBinaryDirect** method on the **File** class.</span></span>|<span data-ttu-id="16a46-123">Нет ограничений на размер файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-123">No file size limits.</span></span> <span data-ttu-id="16a46-124">Время ожидания истекает через 30 минут.</span><span class="sxs-lookup"><span data-stu-id="16a46-124">Time-out occurs after 30 minutes.</span></span>|<span data-ttu-id="16a46-125">Используйте этот метод только в том случае, если вы используете политику проверки подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="16a46-125">Only use this method if you're using a user-only authentication policy.</span></span> <span data-ttu-id="16a46-126">Политики проверки подлинности пользователя недоступны в надстройки уровня приложения для SharePoint, но можно использовать в собственный устройства приложений, Windows PowerShell и консольных приложений Windows.</span><span class="sxs-lookup"><span data-stu-id="16a46-126">User-only authentication policy is not available in an add-in for SharePoint, but can be used in native device apps, Windows PowerShell, and Windows console applications.</span></span>|<span data-ttu-id="16a46-127">SharePoint Server 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="16a46-127">SharePoint Server 2013, SharePoint Online</span></span>|
| <span data-ttu-id="16a46-128">Свойство **ContentStream** класса **FileCreationInformation** .</span><span class="sxs-lookup"><span data-stu-id="16a46-128">**ContentStream** property on the **FileCreationInformation** class.</span></span>|<span data-ttu-id="16a46-129">Нет ограничений на размер файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-129">No file size limits.</span></span> <span data-ttu-id="16a46-130">Время ожидания истекает через 30 минут.</span><span class="sxs-lookup"><span data-stu-id="16a46-130">Time-out occurs after 30 minutes.</span></span>|<span data-ttu-id="16a46-131">Рекомендуется для:</span><span class="sxs-lookup"><span data-stu-id="16a46-131">Recommended for:</span></span><br/><span data-ttu-id="16a46-132">-SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="16a46-132">- SharePoint Server 2013.</span></span><br/><span data-ttu-id="16a46-133">-SharePoint Online, если файл меньше 10 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-133">- SharePoint Online when the file is smaller than 10 MB.</span></span>|<span data-ttu-id="16a46-134">SharePoint Server 2013, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="16a46-134">SharePoint Server 2013, SharePoint Online</span></span>|
|<span data-ttu-id="16a46-135">Загрузите файл как набор фрагментов, с помощью методов **StartUpload**, **ContinueUpload**и **FinishUpload** **файл** класса.</span><span class="sxs-lookup"><span data-stu-id="16a46-135">Upload a single file as a set of chunks using the  **StartUpload**,  **ContinueUpload**, and  **FinishUpload** methods on the **File** class.</span></span>|<span data-ttu-id="16a46-136">Нет ограничений на размер файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-136">No file size limits.</span></span> <span data-ttu-id="16a46-137">Время ожидания истекает через 30 минут.</span><span class="sxs-lookup"><span data-stu-id="16a46-137">Time-out occurs after 30 minutes.</span></span> <span data-ttu-id="16a46-138">Каждый блок файла необходимо загрузить несколько 30 минут после завершения предыдущих блока, чтобы избежать тайм-аута.</span><span class="sxs-lookup"><span data-stu-id="16a46-138">Each chunk of the file must upload within 30 minutes of completion of the previous chunk to avoid the time-out.</span></span> |<span data-ttu-id="16a46-139">Рекомендуется для SharePoint Online, если файл превышает 10 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-139">Recommended for SharePoint Online when the file is larger than 10 MB.</span></span>|<span data-ttu-id="16a46-140">SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="16a46-140">SharePoint Online</span></span>|

## <a name="before-you-begin"></a><span data-ttu-id="16a46-141">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="16a46-141">Before you begin</span></span>
<span data-ttu-id="16a46-142"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="16a46-142"></span></span>

<span data-ttu-id="16a46-143">Чтобы начать работу, загрузите пример надстройки [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="16a46-143">To get started, download the  [Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-corelargefileupload-sample-app"></a><span data-ttu-id="16a46-144">Использование примера приложения Core.LargeFileUpload</span><span class="sxs-lookup"><span data-stu-id="16a46-144">Using the Core.LargeFileUpload sample app</span></span>
<span data-ttu-id="16a46-145"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="16a46-145"></span></span>

<span data-ttu-id="16a46-146">При запуске в этом примере отображается консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="16a46-146">When you start this code sample, a console application appears.</span></span> <span data-ttu-id="16a46-147">Необходимо указать SharePoint Online URL-адрес сайта семейства сайтов и учетные данные для входа для Office 365.</span><span class="sxs-lookup"><span data-stu-id="16a46-147">You must supply a SharePoint Online site collection URL and your logon credentials for Office 365.</span></span> <span data-ttu-id="16a46-148">После проверки подлинности консольное приложение отображает исключение.</span><span class="sxs-lookup"><span data-stu-id="16a46-148">After authentication, the console application displays an exception.</span></span> <span data-ttu-id="16a46-149">Исключение происходит, когда с помощью метода **UploadDocumentContent** в FileUploadService.cs пытается использовать свойство **FileCreationInformation.Content** для отправки файла, размер которого превышает 2 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-149">The exception occurs when the  **UploadDocumentContent** method in FileUploadService.cs tries to use the **FileCreationInformation.Content** property to upload a file that is larger than 2 MB.</span></span> <span data-ttu-id="16a46-150">**UploadDocumentContent** также создает библиотеки документов, именем **: документы** , если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="16a46-150">**UploadDocumentContent** also creates a document library called **Docs** if it does not already exist.</span></span> <span data-ttu-id="16a46-151">Далее в этом примере кода используется в библиотеке **документов** .</span><span class="sxs-lookup"><span data-stu-id="16a46-151">The **Docs** document library is used later in this code sample.</span></span>

> [!NOTE] 
> <span data-ttu-id="16a46-152">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="16a46-152">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="16a46-153">В FileUploadService.cs в этом примере кода предоставляет три варианта, которые можно использовать для отправки больших файлов в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="16a46-153">In FileUploadService.cs, this code sample provides three options that you can use to upload large files to a document library:</span></span>

- <span data-ttu-id="16a46-154">Метод **File.SaveBinaryDirect** .</span><span class="sxs-lookup"><span data-stu-id="16a46-154">The  **File.SaveBinaryDirect** method.</span></span>
    
- <span data-ttu-id="16a46-155">Свойство **FileCreationInformation.ContentStream** .</span><span class="sxs-lookup"><span data-stu-id="16a46-155">The  **FileCreationInformation.ContentStream** property.</span></span>
    
- <span data-ttu-id="16a46-156">Методы **StartUpload**, **ContinueUpload**и **FinishUpload** на **файл** классов.</span><span class="sxs-lookup"><span data-stu-id="16a46-156">The  **StartUpload**,  **ContinueUpload**, and  **FinishUpload** methods on the **File** class.</span></span>
    
<span data-ttu-id="16a46-157">В FileUploadService.cs **SaveBinaryDirect** использует метод **Microsoft.SharePoint.Client.File.SaveBinaryDirect** с помощью объекта **FileStream** для загрузки файлов в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="16a46-157">In FileUploadService.cs,  **SaveBinaryDirect** uses the **Microsoft.SharePoint.Client.File.SaveBinaryDirect** method with a **FileStream** object to upload files to a document library.</span></span>

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

<span data-ttu-id="16a46-158">В FileUploadService.cs **UploadDocumentContentStream** использует свойство **FileCreationInformation.ContentStream** с помощью объекта **FileStream** для передачи файла в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="16a46-158">In FileUploadService.cs,  **UploadDocumentContentStream** uses the **FileCreationInformation.ContentStream** property with the **FileStream** object to upload a file to a document library.</span></span>

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

<span data-ttu-id="16a46-159">В FileUploadService.cs **UploadFileSlicePerSlice** отправляет большого файла в библиотеке документов как набор блоки или фрагментов.</span><span class="sxs-lookup"><span data-stu-id="16a46-159">In FileUploadService.cs,  **UploadFileSlicePerSlice** uploads a large file to a document library as a set of chunks or fragments.</span></span> <span data-ttu-id="16a46-160">**UploadFileSlicePerSlice** выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="16a46-160">**UploadFileSlicePerSlice** performs the following tasks:</span></span>

1. <span data-ttu-id="16a46-161">Получает новый GUID.</span><span class="sxs-lookup"><span data-stu-id="16a46-161">Gets a new GUID.</span></span> <span data-ttu-id="16a46-162">Отправка файла в виде фрагментов, необходимо использовать уникальный идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="16a46-162">To upload a file in chunks, you must use a unique GUID.</span></span> 
    
2. <span data-ttu-id="16a46-163">Вычисляет размер блока фрагмента в байтах.</span><span class="sxs-lookup"><span data-stu-id="16a46-163">Calculates the block size of the chunk in bytes.</span></span> <span data-ttu-id="16a46-164">Чтобы вычислить размер блока в байтах, **UploadFileSlicePerSlice** использует **fileChunkSizeInMB**, который определяет размер отдельных фрагментов в МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-164">To calculate the block size in bytes,  **UploadFileSlicePerSlice** uses **fileChunkSizeInMB**, which specifies the size of the individual chunks in MB.</span></span> 
    
3. <span data-ttu-id="16a46-165">Тесты, если размер файла для загрузки ( **размер файла**) меньше или равно размер блока ( **размер блока**).</span><span class="sxs-lookup"><span data-stu-id="16a46-165">Tests if the size of the file to upload ( **fileSize**) is less than or equal to the chunk size ( **blockSize**).</span></span>
    
    1. <span data-ttu-id="16a46-166">Если **размер файла** меньше или равно размер блока, позволяет гарантировать по-прежнему передачи файла с помощью свойства **FileCreationInformation.ContentStream** .</span><span class="sxs-lookup"><span data-stu-id="16a46-166">If  **fileSize** is less than or equal to the chunk size, the sample ensures that the file is still uploaded by using the **FileCreationInformation.ContentStream** property.</span></span> <span data-ttu-id="16a46-167">Имейте в виду, что размер блока рекомендуемые 10 МБ или больше.</span><span class="sxs-lookup"><span data-stu-id="16a46-167">Remember that the recommended chunk size is 10 MB or larger.</span></span>
      
    2. <span data-ttu-id="16a46-168">Если **размер файла** превышает размер блока:</span><span class="sxs-lookup"><span data-stu-id="16a46-168">If  **fileSize** is larger than the chunk size:</span></span>
    
        1. <span data-ttu-id="16a46-169">Часть файла считывается в **буфер**.</span><span class="sxs-lookup"><span data-stu-id="16a46-169">A chunk of the file is read into  **buffer**.</span></span>
    
        2. <span data-ttu-id="16a46-170">Если размер блока равен размер файла, считывания весь файл.</span><span class="sxs-lookup"><span data-stu-id="16a46-170">If the chunk size is equal to the file size, the entire file was read.</span></span> <span data-ttu-id="16a46-171">Блока копируется в **lastBuffer**.</span><span class="sxs-lookup"><span data-stu-id="16a46-171">The chunk is copied to  **lastBuffer**.</span></span>  <span data-ttu-id="16a46-172">**lastBuffer** используется **File.FinishUpload** , чтобы отправить блока.</span><span class="sxs-lookup"><span data-stu-id="16a46-172">**lastBuffer** then uses **File.FinishUpload** to upload the chunk.</span></span>
    
    3. <span data-ttu-id="16a46-173">Если размер блока не равно размер файла, имеется несколько блоков для чтения из файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-173">If the chunk size is not equal to the file size, there is more than one chunk to read from the file.</span></span>  <span data-ttu-id="16a46-174">Отправка первого блока называется **File.StartUpload** .</span><span class="sxs-lookup"><span data-stu-id="16a46-174">**File.StartUpload** is called to upload the first chunk.</span></span> <span data-ttu-id="16a46-175">**fileoffset**, используемый в качестве начальной точки следующего блока, затем задается число байтов, переданных с первого блока.</span><span class="sxs-lookup"><span data-stu-id="16a46-175">**fileoffset**, which is used as the starting point of the next chunk, is then set to the amount of bytes uploaded from the first chunk.</span></span> <span data-ttu-id="16a46-176">Следующий фрагмент считывается, если последнего блока не достигнуто, **File.ContinueUpload** называется отправка следующая часть файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-176">When the next chunk is read, if the last chunk has not been reached,  **File.ContinueUpload** is called to upload the next chunk of the file.</span></span> <span data-ttu-id="16a46-177">Процесс повторяется до последнего часть считывается.</span><span class="sxs-lookup"><span data-stu-id="16a46-177">The process repeats until the last chunk is read.</span></span> <span data-ttu-id="16a46-178">При чтении последнего блока **File.FinishUpload** загружает последнего блока и сохраняет файл.</span><span class="sxs-lookup"><span data-stu-id="16a46-178">When the last chunk is read, **File.FinishUpload** uploads the last chunk and commits the file.</span></span> <span data-ttu-id="16a46-179">Содержимое файла затем изменены после завершения этого метода.</span><span class="sxs-lookup"><span data-stu-id="16a46-179">The file content is then changed when this method is finished.</span></span>

> [!NOTE] 
> <span data-ttu-id="16a46-180">Необходимо учитывайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="16a46-180">Consider the following best practices:</span></span>
- <span data-ttu-id="16a46-181">Используйте механизм повторных попыток в случае отправки прерывается.</span><span class="sxs-lookup"><span data-stu-id="16a46-181">Use a retry mechanism in case your upload is interrupted.</span></span> <span data-ttu-id="16a46-182">При прерывании загружаемого файла файл называется незаконченный файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-182">When an uploaded file is interrupted, the file is called an unfinished file.</span></span> <span data-ttu-id="16a46-183">Вы можете перезапустить Отправка незаконченный файла сразу после загрузки была прервана.</span><span class="sxs-lookup"><span data-stu-id="16a46-183">You may restart uploading an unfinished file soon after the upload was interrupted.</span></span> <span data-ttu-id="16a46-184">Незаконченный файлы удаляются из server от 6 часов до 24 часов после прерывания незаконченный файла.</span><span class="sxs-lookup"><span data-stu-id="16a46-184">Unfinished files are removed from the server between 6 hours to 24 hours after the unfinished file was interrupted.</span></span> <span data-ttu-id="16a46-185">Этот период удаления может изменяться без предварительного уведомления.</span><span class="sxs-lookup"><span data-stu-id="16a46-185">This removal period might change without notice.</span></span>
- <span data-ttu-id="16a46-186">После отправки файла в виде фрагментов в SharePoint Online, блокировки ставится на файл в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="16a46-186">When uploading a file in chunks to SharePoint Online, a lock is placed on the file in SharePoint Online.</span></span> <span data-ttu-id="16a46-187">При прерывании файл остается заблокированным 15 минут.</span><span class="sxs-lookup"><span data-stu-id="16a46-187">When an interruption occurs, the file remains locked for 15 minutes.</span></span> <span data-ttu-id="16a46-188">Если следующая часть файла не загружаться в SharePoint Online в течение 15 минут, удаляется блокировки.</span><span class="sxs-lookup"><span data-stu-id="16a46-188">If the next chunk of the file is not uploaded to SharePoint Online within 15 minutes, the lock is removed.</span></span> <span data-ttu-id="16a46-189">После удаления блокировки можно возобновить отправку пользователями или другой пользователь может запустить отправки файла в.</span><span class="sxs-lookup"><span data-stu-id="16a46-189">After the lock is removed, you can resume uploading, or another user can start uploading the file.</span></span> <span data-ttu-id="16a46-190">Если другой пользователь запускает отправки файла в, незаконченный файл удаляется из SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="16a46-190">If another user starts uploading the file, your unfinished file is removed from SharePoint Online.</span></span> <span data-ttu-id="16a46-191">Период времени, блокировка остается в файл после прерывания передаваемых можно изменить без предварительного уведомления.</span><span class="sxs-lookup"><span data-stu-id="16a46-191">The period of time the lock remains on a file after an upload is interrupted can change without notice.</span></span>
- <span data-ttu-id="16a46-192">Можно изменить размер блока.</span><span class="sxs-lookup"><span data-stu-id="16a46-192">You might change the chunk size.</span></span> <span data-ttu-id="16a46-193">Рекомендуется использовать размер блока 10 МБ.</span><span class="sxs-lookup"><span data-stu-id="16a46-193">We recommend using a chunk size of 10 MB.</span></span>
- <span data-ttu-id="16a46-194">Возобновите прервано блока, отслеживание которых фрагментов отправлен успешно.</span><span class="sxs-lookup"><span data-stu-id="16a46-194">Resume an interrupted chunk by tracking which chunks uploaded successfully.</span></span>

<span data-ttu-id="16a46-195">Блоки, нужно передать последовательно.</span><span class="sxs-lookup"><span data-stu-id="16a46-195">Chunks must be uploaded in sequential order.</span></span> <span data-ttu-id="16a46-196">Не удается загрузить фрагменты одновременно (например, с помощью многопоточные подход).</span><span class="sxs-lookup"><span data-stu-id="16a46-196">You cannot upload slices concurrently (for example, by using a multithreaded approach).</span></span>

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

<span data-ttu-id="16a46-197">После завершения пример кода на узле Office 365, можно перейти в библиотеку **документов** , выбрав **последние** > **документов**. Убедитесь, что в библиотеке **документов** содержит три больших файлов.</span><span class="sxs-lookup"><span data-stu-id="16a46-197">After the code sample is finished, in your Office 365 site, you can go to the  **Docs** document library by choosing **Recent** > **Docs**. Verify that the  **Docs** document library contains three large files.</span></span>

## <a name="see-also"></a><span data-ttu-id="16a46-198">См. также</span><span class="sxs-lookup"><span data-stu-id="16a46-198">See also</span></span>
<span data-ttu-id="16a46-199"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="16a46-199"></span></span>

-  [<span data-ttu-id="16a46-200">Управление контентом корпоративных решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="16a46-200">Enterprise content management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="16a46-201">Пример Core.BulkDocumentUploader</span><span class="sxs-lookup"><span data-stu-id="16a46-201">Core.BulkDocumentUploader sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader)
