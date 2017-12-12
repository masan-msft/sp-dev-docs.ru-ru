---
title: "Массовая отправка документов пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3dce2044fa25e5ec1f231c6511b2186f6c9191d8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="bulk-upload-documents-sample-add-in-for-sharepoint"></a><span data-ttu-id="e93ce-102">Массовая отправка документов пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="e93ce-102">Bulk upload documents sample add-in for SharePoint</span></span>

<span data-ttu-id="e93ce-103">В рамках стратегии Enterprise Content Management (ECM) то можете выполнить массовый отправка документов в библиотеках документов, в том числе OneDrive для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="e93ce-103">As part of your Enterprise Content Management (ECM) strategy, you can bulk upload documents to document libraries, including OneDrive for Business.</span></span>
    
<span data-ttu-id="e93ce-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="e93ce-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

> [!NOTE] 
> <span data-ttu-id="e93ce-105">Пример отправляет один файл в библиотеку документов.</span><span class="sxs-lookup"><span data-stu-id="e93ce-105">The sample uploads one file to a document library.</span></span> <span data-ttu-id="e93ce-106">Отправить несколько файлов, вам потребуются для расширения примера.</span><span class="sxs-lookup"><span data-stu-id="e93ce-106">To upload multiple files, you'll need to extend the sample.</span></span>

<span data-ttu-id="e93ce-107">Эта надстройка используется консольное приложение для загрузки файлов с помощью вызовов интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="e93ce-107">This add-in uses a console application to upload files by using REST API calls.</span></span> <span data-ttu-id="e93ce-108">Параметры конфигурации задаются в XML и CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="e93ce-108">Configuration settings are specified in an XML and a CSV file.</span></span> <span data-ttu-id="e93ce-109">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="e93ce-109">Use this solution if you want to:</span></span>

- <span data-ttu-id="e93ce-110">Отправка файлов в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e93ce-110">Upload files to SharePoint Online.</span></span>
    
- <span data-ttu-id="e93ce-111">Перенос в Office 365 и воспользуйтесь средством настраиваемых миграции для перемещения файлов.</span><span class="sxs-lookup"><span data-stu-id="e93ce-111">Migrate to Office 365 and use a custom migration tool to move your files.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e93ce-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e93ce-112">Before you begin</span></span>
<span data-ttu-id="e93ce-113"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="e93ce-113"></span></span>

<span data-ttu-id="e93ce-114">Чтобы начать работу, загрузите пример надстройки [Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="e93ce-114">To get started, download the  [Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="e93ce-115">Прежде чем запускать в образце кода, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e93ce-115">Before you run the code sample, do the following:</span></span>


1. <span data-ttu-id="e93ce-116">Редактирование файла OneDriveUploader.xml следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e93ce-116">Edit the OneDriveUploader.xml file with the following information:</span></span>
    
    - <span data-ttu-id="e93ce-117">Расположение, где вы хотите сохранить текст и CSV файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="e93ce-117">The location where you want to save your text and CSV log files.</span></span>
    
    - <span data-ttu-id="e93ce-118">Путь к файлу сопоставления CSV-файл (например, C:\PnP\Samples\Core.BulkDocumentUploader\Input\SharePointSites.csv).</span><span class="sxs-lookup"><span data-stu-id="e93ce-118">The file path to your CSV mapping file (for example, C:\PnP\Samples\Core.BulkDocumentUploader\Input\SharePointSites.csv).</span></span>
    
    - <span data-ttu-id="e93ce-119">Расположение файлов политики компании для загрузки (например, C:\PnP\Samples\Core.BulkDocumentUploader\Input\OneDriveFiles).</span><span class="sxs-lookup"><span data-stu-id="e93ce-119">The location of the company policy files to upload (for example, C:\PnP\Samples\Core.BulkDocumentUploader\Input\OneDriveFiles).</span></span>
    
    - <span data-ttu-id="e93ce-120">SharePoint Online учетные данные.</span><span class="sxs-lookup"><span data-stu-id="e93ce-120">Your SharePoint Online credentials.</span></span>
    
    - <span data-ttu-id="e93ce-121">Действие документа (отправить или удалить).</span><span class="sxs-lookup"><span data-stu-id="e93ce-121">The document action to perform (either upload or delete).</span></span>
    
    - <span data-ttu-id="e93ce-122">Новое имя файла для применения в файл после отправки файла в библиотеку документов (например, DOCUMENT.xlsx ПОЛИТИКИ компании).</span><span class="sxs-lookup"><span data-stu-id="e93ce-122">The new file name to apply to the file after the file is uploaded to the document library (for example, COMPANY POLICY DOCUMENT.xlsx).</span></span>
    
2. <span data-ttu-id="e93ce-123">В файле сопоставления SharePointSites.csv список URL-адрес библиотеки документов для передачи файлов и имя файла политики компании для загрузки.</span><span class="sxs-lookup"><span data-stu-id="e93ce-123">In the SharePointSites.csv mapping file, list the document library URL to upload files to, and the name of the company policy file to upload.</span></span> 
    
3. <span data-ttu-id="e93ce-124">Добавьте путь к файлу OneDriveUploader.xml в качестве аргумента командной строки.</span><span class="sxs-lookup"><span data-stu-id="e93ce-124">Add the file path of the OneDriveUploader.xml file as a command-line argument.</span></span> <span data-ttu-id="e93ce-125">Для этого откройте свойства проекта Core.BulkDocumentUploader в обозревателе решений и выберите **Свойства** > **отладки**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="e93ce-125">To do this, open the Core.BulkDocumentUploader project properties in Solution Explorer, and then choose  **Properties** > **Debug**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="e93ce-126">**На рисунке 1. Установка OneDriveUploader.xml в качестве аргумента командной строки в свойствах проекта**</span><span class="sxs-lookup"><span data-stu-id="e93ce-126">**Figure 1. Setting OneDriveUploader.xml as a command-line argument in the project properties**</span></span>

    ![Снимок экрана в области свойства Core.BulkDocumentUploader с выделенным отладки.](media/f1d950b4-82be-4800-9ccc-07fa2c739fad.png)


## <a name="using-the-corebulkdocumentuploader-sample-app"></a><span data-ttu-id="e93ce-128">Использование примера приложения Core.BulkDocumentUploader</span><span class="sxs-lookup"><span data-stu-id="e93ce-128">Using the Core.BulkDocumentUploader sample app</span></span>
<span data-ttu-id="e93ce-129"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="e93ce-129"></span></span>

<span data-ttu-id="e93ce-130">В методе **Main** в Program.cs метод **RecurseActions** вызывает метод **Run** в OneDriveMapper.cs.</span><span class="sxs-lookup"><span data-stu-id="e93ce-130">From the  **Main** method in Program.cs, the **RecurseActions** method calls the **Run** method in OneDriveMapper.cs.</span></span> <span data-ttu-id="e93ce-131">Метод **Run** Получает расположение файлов для загрузки из SharePointSites.csv и затем вызывает метод **IterateCollection** .</span><span class="sxs-lookup"><span data-stu-id="e93ce-131">The **Run** method gets the location of the file to upload from SharePointSites.csv, and then calls the **IterateCollection** method.</span></span>

> [!NOTE] 
> <span data-ttu-id="e93ce-132">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="e93ce-132">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public override void Run(BaseAction parentAction, DateTime CurrentTime, LogHelper logger)
        {
            CsvProcessor csvProcessor = new CsvProcessor();

            logger.LogVerbose(string.Format("Attempting to read mapping CSV file '{0}'", this.UserMappingCSVFile));

            using (StreamReader reader = new StreamReader(this.UserMappingCSVFile))
            {
                csvProcessor.Execute(reader, (entries, y) => { IterateCollection(entries, logger); }, logger);
            }
        }

```

<span data-ttu-id="e93ce-133">В файле SharePointSite.csv перечислены файл для загрузки и библиотеки документов для загрузки этого файла.</span><span class="sxs-lookup"><span data-stu-id="e93ce-133">The SharePointSite.csv file lists a file to upload and the document library to upload that file to.</span></span> <span data-ttu-id="e93ce-134">Метод **IterateCollection** затем выполняет следующие действия, чтобы отправить файл в библиотеку документов:</span><span class="sxs-lookup"><span data-stu-id="e93ce-134">The  **IterateCollection** method then does the following to upload the file to the document library:</span></span>

1. <span data-ttu-id="e93ce-135">Получает файл для загрузки.</span><span class="sxs-lookup"><span data-stu-id="e93ce-135">Gets the file to upload.</span></span> 
    
2. <span data-ttu-id="e93ce-136">Гарантирует, что пользователь имеет разрешения для добавления элементов.</span><span class="sxs-lookup"><span data-stu-id="e93ce-136">Ensures that the user has permissions to add items.</span></span>
    
3. <span data-ttu-id="e93ce-137">Создает объект **HttpWebRequest** с помощью файлов cookie проверки подлинности, строки запроса REST Отправка документа и метод HTTP-запроса действие.</span><span class="sxs-lookup"><span data-stu-id="e93ce-137">Creates the  **HttpWebRequest** object with the authentication cookie, the REST string request to upload the document, and the HTTP request action method.</span></span>
    
4. <span data-ttu-id="e93ce-138">Выполняется отправка файла.</span><span class="sxs-lookup"><span data-stu-id="e93ce-138">Performs the file upload.</span></span>

> [!NOTE] 
> <span data-ttu-id="e93ce-139">Имя файла перезаписывается со значением **FileUploadName** , указанное в OneDriveUploader.xml.</span><span class="sxs-lookup"><span data-stu-id="e93ce-139">The file name is overwritten with the value of  **FileUploadName** specified in OneDriveUploader.xml.</span></span>

```C#
public override void IterateCollection(Collection<string> entries, LogHelper logger)
        {
            Stopwatch IterationSW = new Stopwatch();
            IterationSW.Start();

            logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Establishing context object to: '{0}'", entries[this.SiteIndex]));

            try
            {
                // Use the context of the current iteration URL for current user item.
                using (ClientContext context = new ClientContext(entries[this.SiteIndex]))
                {
                    using (SecureString password = new SecureString())
                    {
                        foreach (char c in this.Password.ToCharArray())
                        {
                            password.AppendChar(c);
                        }

                        context.Credentials = new SharePointOnlineCredentials(this.UserName, password);

                        // Get the file to upload from the directory.
                        FileInfo theFileToUpload = new FileInfo(Path.Combine(this.DirectoryLocation + "\\", entries[this.FileIndex] + ".xlsx"));

                        logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Attempting to {0} file {1}", this.DocumentAction, theFileToUpload));

                        // Ensure that the account has permissions to access.
                        BasePermissions perm = new BasePermissions();
                        perm.Set(PermissionKind.AddListItems);

                        ConditionalScope scope = new ConditionalScope(context, () => context.Web.DoesUserHavePermissions(perm).Value);

                        using(scope.StartScope())
                        {
                            Stopwatch tempSW = new Stopwatch();
                            tempSW.Start();

                            int success = 0;

                            while(tempSW.Elapsed.TotalSeconds < 20)
                            {
                                var digest = context.GetFormDigestDirect();

                                string cookie = ((SharePointOnlineCredentials)context.Credentials).GetAuthenticationCookie(new Uri(entries[this.SiteIndex])).TrimStart("SPOIDCRL=".ToCharArray());

                                using (Stream s = theFileToUpload.OpenRead())
                                {
                                    // Define REST string request to upload document to context. This string specifies the Documents folder, but you can specify another document library.
                                    string theTargetUri = string.Format(CultureInfo.CurrentCulture, "{0}/_api/web/lists/getByTitle('Documents')/RootFolder/Files/add(url='{1}',overwrite='true')?", entries[this.SiteIndex], this.FileUploadName);

                                    // Define REST HTTP request object.
                                    HttpWebRequest SPORequest = (HttpWebRequest)HttpWebRequest.Create(theTargetUri);

                                    // Define HTTP request action method.
                                    if (this.DocumentAction == "Upload")
                                    {
                                        SPORequest.Method = "POST";
                                    }
                                    else if (this.DocumentAction == "Delete")
                                    {
                                        SPORequest.Method = "DELETE";
                                    }
                                    else
                                    {
                                        logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "There was a problem with the HTTP request in DocumentAction attribute of XML file"));
                                        throw new Exception("The HTTP Request operation is not supported, please check the value of DocumentAction in the XML file");
                                    }

                                    // Build out additional HTTP request details.
                                    SPORequest.Accept = "application/json;odata=verbose";
                                    SPORequest.Headers.Add("X-RequestDigest", digest.DigestValue);
                                    SPORequest.ContentLength = s.Length;
                                    SPORequest.ContentType = "application/octet-stream";

                                    // Handle authentication to context through cookie.
                                    SPORequest.CookieContainer = new CookieContainer();
                                    SPORequest.CookieContainer.Add(new Cookie("SPOIDCRL", cookie, string.Empty, new Uri(entries[this.SiteIndex]).Authority));

                                    // Perform file upload/deletion.
                                    using (Stream requestStream = SPORequest.GetRequestStream())
                                    {
                                        s.CopyTo(requestStream);
                                    }

                                    // Get HTTP response to determine success of operation.
                                    HttpWebResponse SPOResponse = (HttpWebResponse)SPORequest.GetResponse();

                                    logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Successfully '{0}' file {1}", this.DocumentAction, theFileToUpload));
                                    logger.LogOutcome(entries[this.SiteIndex], "SUCCCESS");

                                    success = 1;

                                    // Dispose of the HTTP response.
                                    SPOResponse.Close();

                                    break;
                                }
                                                       
                            }

                            tempSW.Stop();

                            if (success != 1)
                            {
                                throw new Exception("The HTTP Request operation exceeded the timeout of 20 seconds");
                            }

                        }
                    }
                }

            }
            catch(Exception ex)
            {
                logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "There was an issue performing '{0}' on to the URL '{1}' with exception: {2}", this.DocumentAction, entries[this.SiteIndex], ex.Message));
                logger.LogOutcome(entries[this.SiteIndex], "FAILURE");
            }
            finally
            {
                IterationSW.Stop();
                logger.LogVerbose(string.Format(CultureInfo.CurrentCulture, "Completed processing URL:'{0}' in {1} seconds", entries[this.SiteIndex], IterationSW.ElapsedMilliseconds/1000));
            }
        }

```

## <a name="see-also"></a><span data-ttu-id="e93ce-140">См. также</span><span class="sxs-lookup"><span data-stu-id="e93ce-140">See also</span></span>
<span data-ttu-id="e93ce-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e93ce-141"></span></span>

-  [<span data-ttu-id="e93ce-142">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e93ce-142">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)   
-  [<span data-ttu-id="e93ce-143">Пример Core.LargeFileUpload</span><span class="sxs-lookup"><span data-stu-id="e93ce-143">Core.LargeFileUpload sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)
    
