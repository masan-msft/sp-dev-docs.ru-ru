---
title: "Массовая отправка документов пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3dce2044fa25e5ec1f231c6511b2186f6c9191d8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="bulk-upload-documents-sample-add-in-for-sharepoint"></a>Массовая отправка документов пример надстройки для SharePoint

В рамках стратегии Enterprise Content Management (ECM) то можете выполнить массовый отправка документов в библиотеках документов, в том числе OneDrive для бизнеса.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

> [!NOTE] 
> Пример отправляет один файл в библиотеку документов. Отправить несколько файлов, вам потребуются для расширения примера.

Эта надстройка используется консольное приложение для загрузки файлов с помощью вызовов интерфейса API REST. Параметры конфигурации задаются в XML и CSV-файл. Если вы хотите используйте этого решения:

- Отправка файлов в SharePoint Online.
    
- Перенос в Office 365 и воспользуйтесь средством настраиваемых миграции для перемещения файлов.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.BulkDocumentUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.BulkDocumentUploader) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать в образце кода, сделайте следующее:


1. Редактирование файла OneDriveUploader.xml следующие сведения:
    
    - Расположение, где вы хотите сохранить текст и CSV файлов журнала.
    
    - Путь к файлу сопоставления CSV-файл (например, C:\PnP\Samples\Core.BulkDocumentUploader\Input\SharePointSites.csv).
    
    - Расположение файлов политики компании для загрузки (например, C:\PnP\Samples\Core.BulkDocumentUploader\Input\OneDriveFiles).
    
    - SharePoint Online учетные данные.
    
    - Действие документа (отправить или удалить).
    
    - Новое имя файла для применения в файл после отправки файла в библиотеку документов (например, DOCUMENT.xlsx ПОЛИТИКИ компании).
    
2. В файле сопоставления SharePointSites.csv список URL-адрес библиотеки документов для передачи файлов и имя файла политики компании для загрузки. 
    
3. Добавьте путь к файлу OneDriveUploader.xml в качестве аргумента командной строки. Для этого откройте свойства проекта Core.BulkDocumentUploader в обозревателе решений и выберите **Свойства** > **отладки**, как показано на рисунке 1.
    
    **На рисунке 1. Установка OneDriveUploader.xml в качестве аргумента командной строки в свойствах проекта**

    ![Снимок экрана в области свойства Core.BulkDocumentUploader с выделенным отладки.](media/f1d950b4-82be-4800-9ccc-07fa2c739fad.png)


## <a name="using-the-corebulkdocumentuploader-sample-app"></a>Использование примера приложения Core.BulkDocumentUploader
<a name="sectionSection1"> </a>

В методе **Main** в Program.cs метод **RecurseActions** вызывает метод **Run** в OneDriveMapper.cs. Метод **Run** Получает расположение файлов для загрузки из SharePointSites.csv и затем вызывает метод **IterateCollection** .

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

В файле SharePointSite.csv перечислены файл для загрузки и библиотеки документов для загрузки этого файла. Метод **IterateCollection** затем выполняет следующие действия, чтобы отправить файл в библиотеку документов:

1. Получает файл для загрузки. 
    
2. Гарантирует, что пользователь имеет разрешения для добавления элементов.
    
3. Создает объект **HttpWebRequest** с помощью файлов cookie проверки подлинности, строки запроса REST Отправка документа и метод HTTP-запроса действие.
    
4. Выполняется отправка файла.

> [!NOTE] 
> Имя файла перезаписывается со значением **FileUploadName** , указанное в OneDriveUploader.xml.

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)   
-  [Пример Core.LargeFileUpload](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)
    
