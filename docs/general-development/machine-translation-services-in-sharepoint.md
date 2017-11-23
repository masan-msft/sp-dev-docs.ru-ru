---
title: "Службы машинного перевода в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 15a81428-da94-40b8-8ed4-6a12f05661e2
ms.openlocfilehash: e8a47de97c63f8c438d19e07a549a939cce30357
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="machine-translation-services-in-sharepoint"></a>Службы машинного перевода в SharePoint
Узнайте о службе машинного перевода — новом приложении службы в SharePoint, выполняющем автоматический машинный перевод файлов и сайтов.
## <a name="machine-translation-service-overview"></a>Обзор службы машинного перевода
<a name="TranslationSvc_Overview"> </a>


> **Примечание.** Используя службу машинного перевода, пользователи могут отправлять контент на перевод в корпорацию Майкрософт. Он может использоваться для улучшения качества переводов. Если вы используете службу машинного перевода в своем приложении, сообщите пользователям, что они могут отправлять контент на перевод в корпорацию Майкрософт и что Майкрософт может использовать его для улучшения качества переводов. Дополнительные сведения см. в статье о конфиденциальности Microsoft Translator. 
  
    
    

Служба машинного перевода — новое приложение службы в SharePoint, выполняющее автоматический машинный перевод файлов и сайтов. Обрабатывая запрос на перевод, приложение службы машинного перевода пересылает его в облачную службу машинного перевода [Microsoft Translator](http://www.microsoft.com/ru-RU/translator/), где выполняется сам перевод. Эта облачная служба также обеспечивает перевод в Microsoft Office, Lync, Yammer и Bing.
  
    
    
Приложение службы машинного перевода обрабатывает запросы на перевод в асинхронном и синхронном режимах. Асинхронные запросы на перевод обрабатываются при выполнении задания таймера. Интервал задания таймера по умолчанию составляет 15 минут. Вы можете изменить этот параметр в Центре администрирования или с помощью Windows PowerShell. Вы также можете задать немедленное выполнение таймера, используя следующую команду:
  
    
    



```

$tj = get-sptimerjob "Sharepoint Translation Services"
$tj.Runnow()
```

Синхронные запросы на перевод обрабатываются по мере их отправки.
  
    
    

### <a name="shared-components-with-word-automation-services"></a>Общие компоненты с Word Automation Services
<a name="TranslationSvc_SharedWAS"> </a>

У архитектуры службы машинного перевода несколько общих компонентов с архитектурой Microsoft Word Automation Services. Дополнительные сведения см. в статье [Архитектура служб Word Automation Services](http://msdn.microsoft.com/library/567bf68d-46bb-4ee8-981d-186549b9e5b8%28Office.15%29.aspx).
  
    
    
Объектная модель службы машинного перевода похожа на объектную модель Word Automation Services.
  
    
    

## <a name="using-the-machine-translation-service-server-object-model"></a>Использование серверной объектной модели службы машинного перевода
<a name="TranslationSvc_ServerOM"> </a>

Приложения, которые используют серверную объектную модель, должны выполняться непосредственно на сервере с SharePoint. Сведения о создании приложений с удаленным размещением см. в разделе [Использование клиентской объектной модели службы машинного перевода](#TranslationSvc_UsingCSOM) далее в этой статье. Серверная объектная модель службы машинного перевода находится в пространстве имен **Microsoft.Office.TranslationServices** в Microsoft.Office.TranslationServices.dll.
  
    
    
Серверная объектная модель позволяет отправлять запросы в приложение службы машинного перевода в асинхронном или синхронном режиме (для мгновенного перевода). Приложение службы машинного перевода включает две рабочих очереди для хранения запросов на перевод: асинхронную и синхронную. Запросы в синхронной очереди имеют более высокий приоритет и переводятся раньше, чем запросы в асинхронной очереди. Запросы направляются в одну из этих очередей в зависимости от используемого класса.
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
Пример использования серверной объектной модели из консольного приложения приведен в статье [SharePoint: доступ к службе машинного перевода с помощью серверной объектной модели](http://code.msdn.microsoft.com/SharePoint-Access-86639c3d ).
  
    
    

### <a name="asynchronous-translation-using-the-server-object-model"></a>Асинхронный перевод с помощью серверной объектной модели

Класс **TranslationJob** определяет набор элементов для перевода. Это может быть один файл или все файлы в папке либо библиотеке документов. Задания, которые передаются таким образом, хранятся в базе данных переводов. Каждый раз, когда выполняется задание таймера, определенные задания извлекаются из базы данных переводов и добавляются в асинхронную очередь. Интервал задания таймера по умолчанию составляет 15 минут.
  
    
    
Ниже показано, как выполнить асинхронный перевод одного файла.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture)); 
job.AddFile(input, output);
job.Start(); 

```

Приведенный ниже код показывает, как выполнять асинхронный перевод для всех файлов в папке.
  
    
    



```VB.net

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture));
using (SPSite siteIn = new SPSite(inputFolder))
{
    using (SPWeb webIn = siteIn.OpenWeb())
    {
        using (SPWeb webOut = siteOut.OpenWeb())
        {
            SPFolder folderIn = webIn.GetFolder(inputFolder);
            SPFolder folderOut = webOut.GetFolder(outputFolder);                    
            job.AddFolder(folderIn, folderOut, true);
            job.Start();
        }
    }
}
```

Приведенный ниже код показывает, как выполнять асинхронный перевод для всех файлов в библиотеке документов.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture));
using (SPSite siteIn = new SPSite(inputList))
{
    using (SPWeb webIn = siteIn.OpenWeb())
    {
        using (SPSite siteOut = new SPSite(outputList))
        {
            using (SPWeb webOut = siteOut.OpenWeb())
            {
                SPDocumentLibrary listIn = (SPDocumentLibrary)webIn.GetList(inputList);
                SPDocumentLibrary listOut = (SPDocumentLibrary)webOut.GetList(outputList);
                job.AddLibrary(listIn, listOut);
                job.Start();
            }
        }
    }
}
```


### <a name="synchronous-translation-using-the-server-object-model"></a>Синхронный перевод с помощью серверной объектной модели

С помощью класса **SyncTranslator** можно запрашивать мгновенный перевод файлов и потоков. Маршрутизация этих запросов отличается от маршрутизации запросов, выполняемых с помощью класса **TranslationJob**. Они немедленно добавляются в синхронную очередь для обработки. Класс **TranslationItemInfo** содержит сведения об одном элементе, переводимом службой машинного перевода. Метод **SyncTranslator.Translate** возвращает экземпляр этого класса в заданиях синхронного перевода.
  
    
    
Ниже показано, как выполнить синхронный перевод одного файла.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
TranslationItemInfo itemInfo = job.Translate(input, output);

```

Приведенный ниже код показывает, как выполнять синхронный перевод для потока.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
FileStream inputStream = new FileStream(input, FileMode.Open);
FileStream outputStream = new FileStream(output, FileMode.Create);     
TranslationItemInfo itemInfo = job.Translate(inputStream, outputStream, fileFormat);
inputStream.Close();
outputStream.Flush();
outputStream.Close();

```

Приведенный ниже код показывает, как выполнять синхронный перевод для последовательности байтов.
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
Byte[] inputByte;
Byte[] outputByte;
inputByte = File.ReadAllBytes(input);
outputByte = null;
TranslationItemInfo itemInfo = job.Translate(inputByte, out outputByte, fileFormat);
FileStream outputStream = File.Open(output, FileMode.Create);
MemoryStream memoryStream = new MemoryStream(outputByte);
memoryStream.WriteTo(outputStream);
outputStream.Flush();
outputStream.Close();

```


### <a name="permissions"></a>Разрешения
<a name="TranslationSvc_Permissions"> </a>

Если пользователь, для которого выполняется задание перевода, может получить доступ к файлу, который нужно перевести, и расположению соответствующих выходных данных, пользователь отменяет проверку безопасности, и выполняется перевод.
  
    
    

## <a name="using-the-machine-translation-services-client-object-model"></a>Использование клиентской объектной модели службы машинного перевода
<a name="TranslationSvc_UsingCSOM"> </a>

Служба машинного перевода также включает клиентскую объектную модель (CSOM), которая обеспечивает доступ к API для разработки интернет-, локальных и мобильных приложений. Клиентские приложения могут использовать CSOM для доступа к контенту и функциям сервера. При этом большинство функций перевода реализуются на сервере, но CSOM все же отличается от серверной объектной модели. Поддерживается асинхронный перевод отдельных файлов и файлов в библиотеке документов или папке. Синхронный перевод файлов поддерживается, а файловых потоков — нет.
  
    
    
CSOM службы машинного перевода включает управляемую клиентскую объектную модель .NET, а также объектные модели Microsoft Silverlight и JavaScript. Она встроена в CSOM SharePoint. Поэтому клиентский код сначала получает доступ к CSOM SharePoint, а затем к CSOM службы машинного перевода. 
  
    
    
Дополнительные сведения о модели CSOM SharePoint см. в статье [Клиентская объектная модель SharePoint 2010](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx). Дополнительные сведения об объекте **ClientContext**, представляющем собой точку входа в CSOM, см. в статье [Контекст клиента как центральный объект](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).
  
    
    
В таблице 1 показаны эквивалентные объекты, предоставляемые API CSOM для серверных объектов службы машинного перевода. 
  
    
    

**Таблица 1. API серверной объектной модели и их эквиваленты CSOM**


|**Сервер**|**Управляемая модель .NET и Silverlight**|**JavaScript**|
|:-----|:-----|:-----|
|Microsoft.Office.TranslationServices.TranslationJob  <br/> |Microsoft.Office.TranslationServices.Client.TranslationJob  <br/> |SP.Translation.TranslationJob  <br/> |
|Microsoft.Office.TranslationServices.TranslationJobInfo  <br/> |Microsoft.Office.TranslationServices.Client.TranslationJobInfo  <br/> |SP.Translation.TranslationJobInfo  <br/> |
|Microsoft.Office.TranslationServices.TranslationItemInfo  <br/> |Microsoft.Office.TranslationServices.Client.TranslationItemInfo  <br/> |SP.Translation.TranslationItemInfo  <br/> |
|Microsoft.Office.TranslationServices.TranslationJobStatus  <br/> |Microsoft.Office.TranslationServices.Client.TranslationJobStatus  <br/> |SP.Translation.TranslationJobStatus  <br/> |
|Microsoft.Office.TranslationServices.SyncTranslator  <br/> |Microsoft.Office.TranslationServices.Client.SyncTranslator  <br/> |SP.Translation.SyncTranslator  <br/> |
   

### <a name="machine-translation-service-net-managed-csom-and-silverlight-csom"></a>Управляемая CSOM .NET службы машинного перевода и CSOM Silverlight
<a name="TranslationSvc_ManagedCSOM"> </a>

Управляемая CSOM .NET: получите экземпляр **ClientContext** (расположенный в пространстве имен **Microsoft.SharePoint.Client** в Microsoft.SharePoint.Client.dll). Затем воспользуйтесь объектной моделью в пространстве имен **Microsoft.Office.TranslationServices.Client** в Microsoft.Office.TranslationServices.Client.dll.
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
Пример использования управляемой CSOM .NET приведен в статье [SharePoint: доступ к службе машинного перевода с помощью клиентской объектной модели](http://code.msdn.microsoft.com/SharePoint-Perform-a-8e53b06a).
  
    
    
CSOM Silverlight: получите экземпляр **ClientContext** (расположенный в пространстве имен **Microsoft.SharePoint.Client** в Microsoft.SharePoint.Client.Silverlight.dll). Затем воспользуйтесь объектной моделью в пространстве имен **Microsoft.Office.TranslationServices.Client** из Microsoft.Office.TranslationServices.Silverlight.dll.
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
Пример использования CSOM Silverlight приведен в статье [SharePoint: доступ к службе машинного перевода из приложения Silverlight](http://code.msdn.microsoft.com/SharePoint-Access-cdaff6b2).
  
    
    
Чтобы выполнить асинхронный перевод одного файла:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture  = "cultureID";
string name = "translationJobName";
string  inputFile =  "http://serverName/path/inputFileName";
string outputFile = "http://serverName/path/outputFileName";
TranslationJob job = new TranslationJob(clientContext , culture);
job.AddFile(inputFile , outputFile);
job.Name = name;
job.Start();
clientContext.Load(job);
clientContext.ExecuteQuery();
//To retrieve the translation job ID.
string jobID = job.JobId;
```

Чтобы выполнить асинхронный перевод для папки:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture = "cultureID";
string name = "translationJobName";
string inputFolder = clientContext.Web.GetFolderByServerRelativeUrl("inFolderPath");
string outputFolder = clientContext.Web.GetFolderByServerRelativeUrl("outFolderPath");  
TranslationJob job = new TranslationJob(clientContext , culture);
job.AddFolder(inputFolder, outputFolder, true);
job.Name = name;
job.Start();            
clientContext.Load(job);
clientContext.ExecuteQuery();
//To retrieve the translation job ID.
string jobID = job.JobId;
```

Чтобы выполнить асинхронный перевод для библиотеки:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture = "cultureID";
string name = "translationJobName";
string inputLibrary = clientContext.Web.Lists.GetByTitle("inputLibraryName");
string outputLibrary = clientContext.Web.Lists.GetByTitle("outputLibraryName");
TranslationJob job = new TranslationJob(clientContext , culture);
job.AddFolder(inputLibrary , outputLibrary , true);
job.Name = name;
job.Start();            
clientContext.Load(job);
clientContext.ExecuteQuery();
//To retrieve the translation job ID.
string jobID = job.JobId;
```

Чтобы выполнить синхронный перевод одного файла:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
string culture = "cultureID"
string inputFile = "http://serverName/path/inputFileName";
string outputFile = "http://serverName/path/outputFileName";
SyncTranslator job = new SyncTranslator(clientContext , culture);
job.OutputSaveBehavior = SaveBehavior.AlwaysOverwrite;
ClientResult<TranslationItemInfo> cr = job.Translate(inputFile, outputFile );
clientContext.ExecuteQuery(); 
//To retrieve additional information about the translation job.
string errorCode = clientContext.Value.ErrorCode;
string errorMessage = clientContext.Value.ErrorMessage;
string translateID = clientContext.Value.TranslationId;
string succeedResult  = clientContext.Value.Succeeded;
string failResult  = clientContext.Value.Failed;
string cancelStatus = clientContext.Value.Canceled;
string inProgressStatus = clientContext.Value.InProgress;
string notStartedStatus = clientContext.Value.NotStarted;
```

Чтобы получить все языки, поддерживаемые службой машинного перевода:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> supportedLanguages = TranslationJob.EnumerateSupportedLanguages(clientContext);
clientContext.ExecuteQuery();
foreach (string item in supportedLanguages)
{
    Console.Write(item + ", ");
}
```

Чтобы проверить, поддерживается ли конкретный язык:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsLanguageSupported(clientContext, "language");
clientContext.ExecuteQuery();
```

Чтобы получить все расширения имен файлов, поддерживаемые службой машинного перевода:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> fileExt = TranslationJob.EnumerateSupportedFileExtensions(clientContext);
clientContext.ExecuteQuery();
foreach (string item in fileExt)
{
    Console.Write(item + ", ");
}
```

Чтобы проверить, поддерживается ли конкретное расширение имени файла:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsFileExtensionSupported(clientContext, "fileExtension");
clientContext.ExecuteQuery();

```

Чтобы проверить ограничение на размер файла для конкретного расширения:
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<int> maxSize;
maxSize = TranslationJob.GetMaximumFileSize(clientContext, "fileExtension");
clientContext.ExecuteQuery();
```


### <a name="machine-translation-service-javascript-csom"></a>CSOM JavaScript службы машинного перевода
<a name="TranslationSvc_JavaScriptCSOM"> </a>

Получите экземпляр **SP.ClientContext**, а затем воспользуйтесь объектной моделью в файле SP.Translation.js.
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
Пример использования CSOM JavaScript приведен в статье [SharePoint: доступ к службе машинного перевода с помощью JavaScript](http://code.msdn.microsoft.com/SharePoint-Accessing-647f6dd9).
  
    
    
Чтобы выполнить асинхронный перевод одного файла:
  
    
    



```

var asyncJob;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
asyncJob = SP.Translation.TranslationJob.newObject(clientContext, "cultureID");
asyncJob.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
asyncJob.addFile("inputFilePath", "outputFilePath");
asyncJob.set_name("translationJobName");
asyncJob.start();
clientContext.load(asyncJob);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededASync),Function.createDelegate(this, this.onQueryFailed));
```

Чтобы выполнить асинхронный перевод для папки:
  
    
    



```

var asyncJob;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
asyncJob = SP.Translation.TranslationJob.newObject(clientContext, "cultureID");
asyncJob.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
var inputFolder = clientContext.get_web().getFolderByServerRelativeUrl("inputFilePath");
var outputFolder = clientContext.get_web().getFolderByServerRelativeUrl("outputFilePath");
asyncJob.addFolder(inputFolder, outputFolder, true);
asyncJob.set_name("translationJobName");
asyncJob.start();
clientContext.load(asyncJob);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededASync),Function.createDelegate(this, this.onQueryFailed));
```

Чтобы выполнить асинхронный перевод для библиотеки:
  
    
    



```

var asyncJob;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
asyncJob = SP.Translation.TranslationJob.newObject(clientContext, "cultureID");
asyncJob.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
var inputLibrary= clientContext.get_web().get_lists().getByTitle("inputFilePath");
var outputLibrary= clientContext.get_web().get_lists().getByTitle("outputFilePath");
asyncJob.addLibrary(inputLibrary, outputLibrary);
asyncJob.set_name("translationJobName");
asyncJob.start();
clientContext.load(asyncJob);
clientContext.executeQueryAsync(Function.createDelegate(this,this.onQuerySucceededASync),Function.createDelegate(this, this.onQueryFailed));
```

Чтобы выполнить синхронный перевод одного файла:
  
    
    



```

var result;
var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var job = SP.Translation.SyncTranslator.newObject(clientContext, "cultureID");
job.set_outputSaveBehavior(SP.Translation.SaveBehavior.alwaysOverwrite);
result = job.translate("inputFilePath", "outputFilePath");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededSync),
Function.createDelegate(this, this.onQueryFailed));
```

Чтобы получить все языки, поддерживаемые службой машинного перевода:
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedLanguages(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllLang),Function.createDelegate(this, this.onQueryFailed));
```

Чтобы проверить, поддерживается ли конкретный язык:
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isLanguageSupported(clientContext," language");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestLang),Function.createDelegate(this, this.onQueryFailed));
```

Чтобы получить все расширения имен файлов, поддерживаемые службой машинного перевода:
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedFileExtensions(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllFileExt),Function.createDelegate(this, this.onQueryFailed));
```

Чтобы проверить, поддерживается ли конкретное расширение имени файла:
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isFileExtensionSupported(clientContext," fileExtension");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestFileExt),Function.createDelegate(this, this.onQueryFailed));
```


## <a name="machine-translation-service-rest-service"></a>Служба REST службы машинного перевода
<a name="TranslationSvc_REST"> </a>

SharePoint включает службу передачи репрезентативного состояния (REST), позволяющую удаленно управлять приложением службы машинного перевода с помощью любой технологии, которая поддерживает веб-запросы REST. Общую информацию о службе REST в SharePoint см. в статье [Использование операций запросов OData в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).
  
    
    

### <a name="ansynchronous-translation-rest-api"></a>REST API для асинхронного перевода

REST API для асинхронного перевода: 
  
    
    
 `http://serverName/_api/TranslationJob('language')`
  
    
    
Чтобы выполнить асинхронный перевод одного файла: 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFile(inputFile='/path/intput file', outputFile='/path/output file')`
  
    
    
Чтобы выполнить асинхронный перевод для папки: 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFolder(inputFolder='/path/in', outputFolder='/path/out')`
  
    
    
Чтобы выполнить асинхронный перевод библиотеки: 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateLibrary(inputLibrary='/LibraryName', outputLibrary='/LibraryName'')`
  
    
    

### <a name="synchronous-translation-rest-api"></a>REST API для синхронного перевода

Служба REST службы машинного перевода поддерживает только синхронный перевод файлов. Соответствующий API: 
  
    
    
 `http://serverName/_api/SyncTranslator('language')/Translate(outputFile='/path/output file', inputFile='/path/input file')`
  
    
    

### <a name="additional-machine-translation-service-rest-apis"></a>Дополнительные REST API службы машинного перевода

Служба REST службы машинного перевода включает дополнительные API, которые позволяют получить информацию о возможностях приложения службы машинного перевода и состоянии задания на перевод.
  
    
    
Чтобы получить все языки, поддерживаемые службой машинного перевода: 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedLanguages`
  
    
    
Чтобы проверить, поддерживается ли конкретный язык: 
  
    
    
 `http://serverName/_api/TranslationJob.IsLanguageSupported('language')`
  
    
    
Чтобы получить все расширения имени файла, поддерживаемые службой машинного перевода: 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedFileEXtensions`
  
    
    
Чтобы проверить, поддерживается ли конкретное расширение имени файла: 
  
    
    
 `http://serverName/_api/TranslationJob.IsFileExtensionSupported('extension')`
  
    
    
Чтобы проверить ограничение на размер файла для конкретного расширения: 
  
    
    
 `http://serverName/_api/TranslationJob.GetMaximumFileSize('extension')`
  
    
    
Чтобы получить список всех заданий на асинхронный перевод: 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllJobs`
  
    
    
Чтобы получить список всех активных заданий на асинхронный перевод: 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllActiveJobs`
  
    
    
Чтобы получить информацию о конкретном задании на асинхронный перевод: 
  
    
    
 `http://serverName/_api/TranslationJobStatus('jobid')/GetAllItems`
  
    
    
Чтобы отменить задание на асинхронный перевод: 
  
    
    
 `http://serverName/_api/TranslationJob.CancelJob('jobid')`
  
    
    

## <a name="requirements-for-microsoft-word-documents"></a>Требования для документов Microsoft Word
<a name="TranslationSvc_REST"> </a>

Служба машинного перевода SharePoint переводит документы Microsoft Word с языка абзаца. Например, если абзац написан на испанском языке, но для него выбран английский язык, служба перевода не переведет его на английский, потому что этот язык для него уже выбран.
  
    
    

### <a name="to-set-the-paragraph-language-follow-these-steps"></a>Чтобы выбрать язык абзаца, сделайте следующее:


1. Выделите абзац.
    
  
2.  Перейдите на вкладку ленты "Рецензирование".
    
  
3.  Откройте раскрывающееся меню "Язык" и выберите "Язык проверки правописания".
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="TranslationSvc_AR"> </a>


-  [Службы приложений Office 2013 и SharePoint](office-and-sharepoint-application-services.md)
    
  

