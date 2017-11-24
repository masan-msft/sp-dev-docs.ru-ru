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
# <a name="machine-translation-services-in-sharepoint"></a><span data-ttu-id="f6cd7-102">Службы машинного перевода в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6cd7-102">Machine Translation Services in SharePoint 2013</span></span>
<span data-ttu-id="f6cd7-103">Узнайте о службе машинного перевода — новом приложении службы в SharePoint, выполняющем автоматический машинный перевод файлов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-103">Learn about the spmts, which is a new service application in sp15allshort that provides automatic machine translation of files and sites.</span></span>
## <a name="machine-translation-service-overview"></a><span data-ttu-id="f6cd7-104">Обзор службы машинного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-104">Machine Translation Service</span></span>
<span data-ttu-id="f6cd7-105"><a name="TranslationSvc_Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-105"></span></span>


> <span data-ttu-id="f6cd7-106">**Примечание.** Используя службу машинного перевода, пользователи могут отправлять контент на перевод в корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-106">**Note:** Using machine translation will allow users to send content to Microsoft for translation.</span></span> <span data-ttu-id="f6cd7-107">Он может использоваться для улучшения качества переводов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-107">This application will allow users to send content to Microsoft for translation. Microsoft may use content users send us to improve the quality of translations.</span></span> <span data-ttu-id="f6cd7-108">Если вы используете службу машинного перевода в своем приложении, сообщите пользователям, что они могут отправлять контент на перевод в корпорацию Майкрософт и что Майкрософт может использовать его для улучшения качества переводов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-108">
>     Using machine translation will allow users to send content to Microsoft for translation. Microsoft may use content users send us to improve the quality of translations. If you use the Machine Translation Service in your application, you are responsible for informing users that this application will allow users to send content to Microsoft for translation and that Microsoft may use content users send us to improve the quality of translations. See Microsoft Translator Privacy for more information.
</span></span> <span data-ttu-id="f6cd7-109">Дополнительные сведения см. в статье о конфиденциальности Microsoft Translator.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-109">See Microsoft Translator Privacy for more information.</span></span> 
  
    
    

<span data-ttu-id="f6cd7-110">Служба машинного перевода — новое приложение службы в SharePoint, выполняющее автоматический машинный перевод файлов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-110">Learn about the spmts, which is a new service application in sp15allshort that provides automatic machine translation of files and sites.</span></span> <span data-ttu-id="f6cd7-111">Обрабатывая запрос на перевод, приложение службы машинного перевода пересылает его в облачную службу машинного перевода [Microsoft Translator](http://www.microsoft.com/ru-RU/translator/), где выполняется сам перевод.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-111">When the Machine Translation Service application processes a translation request, it forwards the request to the  [Microsoft Translator](http://www.microsoft.com/ru-RU/translator/) cloud-hosted machine translation service, where the actual translation work is performed.</span></span> <span data-ttu-id="f6cd7-112">Эта облачная служба также обеспечивает перевод в Microsoft Office, Lync, Yammer и Bing.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-112">This cloud-service also powers the Microsoft Office, Lync, Yammer and Bing translation features.</span></span>
  
    
    
<span data-ttu-id="f6cd7-113">Приложение службы машинного перевода обрабатывает запросы на перевод в асинхронном и синхронном режимах.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-113">The Machine Translation Service application processes translation requests asynchronously and synchronously.</span></span> <span data-ttu-id="f6cd7-114">Асинхронные запросы на перевод обрабатываются при выполнении задания таймера.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-114">Asynchronous translation requests are processed when the translation timer job executes.</span></span> <span data-ttu-id="f6cd7-115">Интервал задания таймера по умолчанию составляет 15 минут. Вы можете изменить этот параметр в Центре администрирования или с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-115">The default interval of the translation timer job is 15 minutes; you can manage this setting in Central Administration or by using Windows PowerShell.</span></span> <span data-ttu-id="f6cd7-116">Вы также можете задать немедленное выполнение таймера, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-116">You can also set the timer to execute immediately using the following command:</span></span>
  
    
    



```

$tj = get-sptimerjob "Sharepoint Translation Services"
$tj.Runnow()
```

<span data-ttu-id="f6cd7-117">Синхронные запросы на перевод обрабатываются по мере их отправки.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-117">Synchronous translation requests are processed as soon as they are submitted.</span></span>
  
    
    

### <a name="shared-components-with-word-automation-services"></a><span data-ttu-id="f6cd7-118">Общие компоненты с Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="f6cd7-118">Shared components with Word Automation Services</span></span>
<span data-ttu-id="f6cd7-119"><a name="TranslationSvc_SharedWAS"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-119"></span></span>

<span data-ttu-id="f6cd7-120">У архитектуры службы машинного перевода несколько общих компонентов с архитектурой Microsoft Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-120">The Machine Translation Service architecture shares several components from the Microsoft Word Automation Services architecture.</span></span> <span data-ttu-id="f6cd7-121">Дополнительные сведения см. в статье [Архитектура служб Word Automation Services](http://msdn.microsoft.com/library/567bf68d-46bb-4ee8-981d-186549b9e5b8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-121">For more information about the Word Automation Services architecture, see  [Word Automation Services Architecture](http://msdn.microsoft.com/library/567bf68d-46bb-4ee8-981d-186549b9e5b8%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="f6cd7-122">Объектная модель службы машинного перевода похожа на объектную модель Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-122">The Machine Translation Service object model is modeled after the Word Automation Services object model, so if you are familiar with Word Automation Services programming, you'll find similarities with programming against the Machine Translation Service object model.</span></span>
  
    
    

## <a name="using-the-machine-translation-service-server-object-model"></a><span data-ttu-id="f6cd7-123">Использование серверной объектной модели службы машинного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-123">Using the Machine Translation Service server object model</span></span>
<span data-ttu-id="f6cd7-124"><a name="TranslationSvc_ServerOM"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-124"></span></span>

<span data-ttu-id="f6cd7-125">Приложения, которые используют серверную объектную модель, должны выполняться непосредственно на сервере с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-125">Applications that use the server object model must run directly on a server that is running SharePoint.</span></span> <span data-ttu-id="f6cd7-126">Сведения о создании приложений с удаленным размещением см. в разделе [Использование клиентской объектной модели службы машинного перевода](#TranslationSvc_UsingCSOM) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-126">For information about creating applications that can be hosted remotely, see  [Using the Machine Translation Services client object model](#TranslationSvc_UsingCSOM) later in this topic.</span></span> <span data-ttu-id="f6cd7-127">Серверная объектная модель службы машинного перевода находится в пространстве имен **Microsoft.Office.TranslationServices** в Microsoft.Office.TranslationServices.dll.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-127">The Machine Translation Service server object model resides in the **Microsoft.Office.TranslationServices** namespace, which is located in Microsoft.Office.TranslationServices.dll.</span></span>
  
    
    
<span data-ttu-id="f6cd7-128">Серверная объектная модель позволяет отправлять запросы в приложение службы машинного перевода в асинхронном или синхронном режиме (для мгновенного перевода).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-128">Using the server object model, you can submit requests to the Machine Translation Service application asynchronously or synchronously (for instant translation).</span></span> <span data-ttu-id="f6cd7-129">Приложение службы машинного перевода включает две рабочих очереди для хранения запросов на перевод: асинхронную и синхронную.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-129">The Machine Translation Service application has two working queues for storing translation requests: the asynchronous queue and the synchronous queue.</span></span> <span data-ttu-id="f6cd7-130">Запросы в синхронной очереди имеют более высокий приоритет и переводятся раньше, чем запросы в асинхронной очереди.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-130">Requests in the synchronous queue are treated as higher priority and are translated before requests in the asynchronous queue.</span></span> <span data-ttu-id="f6cd7-131">Запросы направляются в одну из этих очередей в зависимости от используемого класса.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-131">The requests are routed to one of these queues based on the class that you use.</span></span>
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="f6cd7-133">Пример использования серверной объектной модели из консольного приложения приведен в статье [SharePoint: доступ к службе машинного перевода с помощью серверной объектной модели](http://code.msdn.microsoft.com/SharePoint-Access-86639c3d ).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-133">  For sample code demonstrating how to use the server object model from a console application, see  SharePoint 2013: Access Machine Translation Service using server object model http://code.msdn.microsoft.com/SharePoint-2013-Access-86639c3d  .</span></span>
  
    
    

### <a name="asynchronous-translation-using-the-server-object-model"></a><span data-ttu-id="f6cd7-134">Асинхронный перевод с помощью серверной объектной модели</span><span class="sxs-lookup"><span data-stu-id="f6cd7-134">Asynchronous translation using the server object model</span></span>

<span data-ttu-id="f6cd7-135">Класс **TranslationJob** определяет набор элементов для перевода.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-135">The **TranslationJob** class defines a set of items to be translated.</span></span> <span data-ttu-id="f6cd7-136">Это может быть один файл или все файлы в папке либо библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-136">This can be a single file or every file within a folder or document library.</span></span> <span data-ttu-id="f6cd7-137">Задания, которые передаются таким образом, хранятся в базе данных переводов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-137">Translation jobs that are submitted this way are stored in the translation database.</span></span> <span data-ttu-id="f6cd7-138">Каждый раз, когда выполняется задание таймера, определенные задания извлекаются из базы данных переводов и добавляются в асинхронную очередь.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-138">Each time the translation timer job runs, it takes some of the jobs from the translation database and adds them to the asynchronous queue to be translated.</span></span> <span data-ttu-id="f6cd7-139">Интервал задания таймера по умолчанию составляет 15 минут.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-139">The default interval of the translation timer job is 15 minutes.</span></span>
  
    
    
<span data-ttu-id="f6cd7-140">Ниже показано, как выполнить асинхронный перевод одного файла.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-140">The following code shows how to translate a single file asynchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
TranslationJob job = new TranslationJob(sc, CultureInfo.GetCultureInfo(culture)); 
job.AddFile(input, output);
job.Start(); 

```

<span data-ttu-id="f6cd7-141">Приведенный ниже код показывает, как выполнять асинхронный перевод для всех файлов в папке.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-141">The following code shows how to translate every file within a folder asynchronously.</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-142">Приведенный ниже код показывает, как выполнять асинхронный перевод для всех файлов в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-142">The following code shows how to translate every file within a document library asynchronously.</span></span>
  
    
    



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


### <a name="synchronous-translation-using-the-server-object-model"></a><span data-ttu-id="f6cd7-143">Синхронный перевод с помощью серверной объектной модели</span><span class="sxs-lookup"><span data-stu-id="f6cd7-143">Synchronous translation using the server object model</span></span>

<span data-ttu-id="f6cd7-144">С помощью класса **SyncTranslator** можно запрашивать мгновенный перевод файлов и потоков.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-144">You use the **SyncTranslator** class to request instant translation for files and streams.</span></span> <span data-ttu-id="f6cd7-145">Маршрутизация этих запросов отличается от маршрутизации запросов, выполняемых с помощью класса **TranslationJob**.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-145">Translation requests that are made by using this class are not routed the same way as requests that are made by using the **TranslationJob** class.</span></span> <span data-ttu-id="f6cd7-146">Они немедленно добавляются в синхронную очередь для обработки.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-146">They are immediately added to the synchronous queue to be processed.</span></span> <span data-ttu-id="f6cd7-147">Класс **TranslationItemInfo** содержит сведения об одном элементе, переводимом службой машинного перевода.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-147">The **TranslationItemInfo** class contains the details for a single item that is translated by the Machine Translation Service.</span></span> <span data-ttu-id="f6cd7-148">Метод **SyncTranslator.Translate** возвращает экземпляр этого класса в заданиях синхронного перевода.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-148">The **SyncTranslator.Translate** method returns an instance of this class in synchronous translation jobs.</span></span>
  
    
    
<span data-ttu-id="f6cd7-149">Ниже показано, как выполнить синхронный перевод одного файла.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-149">The following code shows how to translate a single file synchronously.</span></span>
  
    
    



```cs

SPServiceContext sc = SPServiceContext.GetContext(new SPSite(site));
SyncTranslator job = new SyncTranslator(sc, CultureInfo.GetCultureInfo(jobCulture));
TranslationItemInfo itemInfo = job.Translate(input, output);

```

<span data-ttu-id="f6cd7-150">Приведенный ниже код показывает, как выполнять синхронный перевод для потока.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-150">The following code shows how to translate a stream synchronously.</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-151">Приведенный ниже код показывает, как выполнять синхронный перевод для последовательности байтов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-151">The following code shows how to translate a sequence of bytes synchronously.</span></span>
  
    
    



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


### <a name="permissions"></a><span data-ttu-id="f6cd7-152">Разрешения</span><span class="sxs-lookup"><span data-stu-id="f6cd7-152">Permissions</span></span>
<span data-ttu-id="f6cd7-153"><a name="TranslationSvc_Permissions"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-153"></span></span>

<span data-ttu-id="f6cd7-154">Если пользователь, для которого выполняется задание перевода, может получить доступ к файлу, который нужно перевести, и расположению соответствующих выходных данных, пользователь отменяет проверку безопасности, и выполняется перевод.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-154">If the user who the translation request is running for can access the file to be translated, and that user can access the output location for the file, the user clears the security check and the file is translated.</span></span>
  
    
    

## <a name="using-the-machine-translation-services-client-object-model"></a><span data-ttu-id="f6cd7-155">Использование клиентской объектной модели службы машинного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-155">Using the Machine Translation Services client object model</span></span>
<span data-ttu-id="f6cd7-156"><a name="TranslationSvc_UsingCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-156"></span></span>

<span data-ttu-id="f6cd7-157">Служба машинного перевода также включает клиентскую объектную модель (CSOM), которая обеспечивает доступ к API для разработки интернет-, локальных и мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-157">Machine Translation Service also includes a client object model (CSOM) that enables access to the Machine Translation Service API for online, on-premises, and mobile development.</span></span> <span data-ttu-id="f6cd7-158">Клиентские приложения могут использовать CSOM для доступа к контенту и функциям сервера.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-158">Client applications can use the CSOM to access server content and functionality.</span></span> <span data-ttu-id="f6cd7-159">При этом большинство функций перевода реализуются на сервере, но CSOM все же отличается от серверной объектной модели.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-159">The CSOM implements most of the translation functionality of the server, but the CSOM and the server-side object model do not have one-to-one parity.</span></span> <span data-ttu-id="f6cd7-160">Поддерживается асинхронный перевод отдельных файлов и файлов в библиотеке документов или папке.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-160">Asynchronous translation of individual files, and files in a document library or folder are supported.</span></span> <span data-ttu-id="f6cd7-161">Синхронный перевод файлов поддерживается, а файловых потоков — нет.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-161">Synchronous translation of files is supported, but file streams are not supported.</span></span>
  
    
    
<span data-ttu-id="f6cd7-162">CSOM службы машинного перевода включает управляемую клиентскую объектную модель .NET, а также объектные модели Microsoft Silverlight и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-162">The Machine Translation Service CSOM includes a .NET managed client-side object model and Microsoft Silverlight and JavaScript object models.</span></span> <span data-ttu-id="f6cd7-163">Она встроена в CSOM SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-163">It is built on the SharePoint CSOM.</span></span> <span data-ttu-id="f6cd7-164">Поэтому клиентский код сначала получает доступ к CSOM SharePoint, а затем к CSOM службы машинного перевода.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-164">Therefore, client code first accesses the SharePoint CSOM and then accesses the Machine Translation Service CSOM.</span></span> 
  
    
    
<span data-ttu-id="f6cd7-165">Дополнительные сведения о модели CSOM SharePoint см. в статье [Клиентская объектная модель SharePoint 2010](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-165">For more information about the SharePoint CSOM, see  [SharePoint 2010 Client Object Model](http://msdn.microsoft.com/library/8c086b11-2b8b-41ec-82ae-cd4fef0aeac6%28Office.15%29.aspx).</span></span> <span data-ttu-id="f6cd7-166">Дополнительные сведения об объекте **ClientContext**, представляющем собой точку входа в CSOM, см. в статье [Контекст клиента как центральный объект](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-166">For more information about the **ClientContext** object, which is the entry point to the CSOM, see [Client Context as Central Object](http://msdn.microsoft.com/library/6299f0df-ab4c-40e6-b709-ec80271c99b3%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="f6cd7-167">В таблице 1 показаны эквивалентные объекты, предоставляемые API CSOM для серверных объектов службы машинного перевода.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-167">Table 1 shows the equivalent objects that the CSOM APIs provide for the spmts server objects.</span></span> 
  
    
    

<span data-ttu-id="f6cd7-168">**Таблица 1. API серверной объектной модели и их эквиваленты CSOM**</span><span class="sxs-lookup"><span data-stu-id="f6cd7-168">**Table 1.  Server object model APIs and their CSOM equivalents**</span></span>


|<span data-ttu-id="f6cd7-169">**Сервер**</span><span class="sxs-lookup"><span data-stu-id="f6cd7-169">**server**</span></span>|<span data-ttu-id="f6cd7-170">**Управляемая модель .NET и Silverlight**</span><span class="sxs-lookup"><span data-stu-id="f6cd7-170">**.NET Managed and Silverlight**</span></span>|<span data-ttu-id="f6cd7-171">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="f6cd7-171">**JavaScript**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="f6cd7-172">Microsoft.Office.TranslationServices.TranslationJob</span><span class="sxs-lookup"><span data-stu-id="f6cd7-172">Microsoft.Office.TranslationServices.TranslationJob</span></span>  <br/> |<span data-ttu-id="f6cd7-173">Microsoft.Office.TranslationServices.Client.TranslationJob</span><span class="sxs-lookup"><span data-stu-id="f6cd7-173">Microsoft.Office.TranslationServices.Client.TranslationJob</span></span>  <br/> |<span data-ttu-id="f6cd7-174">SP.Translation.TranslationJob</span><span class="sxs-lookup"><span data-stu-id="f6cd7-174">SP.Translation.TranslationJob</span></span>  <br/> |
|<span data-ttu-id="f6cd7-175">Microsoft.Office.TranslationServices.TranslationJobInfo</span><span class="sxs-lookup"><span data-stu-id="f6cd7-175">Microsoft.Office.TranslationServices.TranslationJobInfo</span></span>  <br/> |<span data-ttu-id="f6cd7-176">Microsoft.Office.TranslationServices.Client.TranslationJobInfo</span><span class="sxs-lookup"><span data-stu-id="f6cd7-176">Microsoft.Office.TranslationServices.Client.TranslationJobInfo</span></span>  <br/> |<span data-ttu-id="f6cd7-177">SP.Translation.TranslationJobInfo</span><span class="sxs-lookup"><span data-stu-id="f6cd7-177">SP.Translation.TranslationJobInfo</span></span>  <br/> |
|<span data-ttu-id="f6cd7-178">Microsoft.Office.TranslationServices.TranslationItemInfo</span><span class="sxs-lookup"><span data-stu-id="f6cd7-178">Microsoft.Office.TranslationServices.TranslationItemInfo</span></span>  <br/> |<span data-ttu-id="f6cd7-179">Microsoft.Office.TranslationServices.Client.TranslationItemInfo</span><span class="sxs-lookup"><span data-stu-id="f6cd7-179">Microsoft.Office.TranslationServices.Client.TranslationItemInfo</span></span>  <br/> |<span data-ttu-id="f6cd7-180">SP.Translation.TranslationItemInfo</span><span class="sxs-lookup"><span data-stu-id="f6cd7-180">SP.Translation.TranslationItemInfo</span></span>  <br/> |
|<span data-ttu-id="f6cd7-181">Microsoft.Office.TranslationServices.TranslationJobStatus</span><span class="sxs-lookup"><span data-stu-id="f6cd7-181">Microsoft.Office.TranslationServices.TranslationJobStatus</span></span>  <br/> |<span data-ttu-id="f6cd7-182">Microsoft.Office.TranslationServices.Client.TranslationJobStatus</span><span class="sxs-lookup"><span data-stu-id="f6cd7-182">Microsoft.Office.TranslationServices.Client.TranslationJobStatus</span></span>  <br/> |<span data-ttu-id="f6cd7-183">SP.Translation.TranslationJobStatus</span><span class="sxs-lookup"><span data-stu-id="f6cd7-183">SP.Translation.TranslationJobStatus</span></span>  <br/> |
|<span data-ttu-id="f6cd7-184">Microsoft.Office.TranslationServices.SyncTranslator</span><span class="sxs-lookup"><span data-stu-id="f6cd7-184">Microsoft.Office.TranslationServices.SyncTranslator</span></span>  <br/> |<span data-ttu-id="f6cd7-185">Microsoft.Office.TranslationServices.Client.SyncTranslator</span><span class="sxs-lookup"><span data-stu-id="f6cd7-185">Microsoft.Office.TranslationServices.Client.SyncTranslator</span></span>  <br/> |<span data-ttu-id="f6cd7-186">SP.Translation.SyncTranslator</span><span class="sxs-lookup"><span data-stu-id="f6cd7-186">SP.Translation.SyncTranslator</span></span>  <br/> |
   

### <a name="machine-translation-service-net-managed-csom-and-silverlight-csom"></a><span data-ttu-id="f6cd7-187">Управляемая CSOM .NET службы машинного перевода и CSOM Silverlight</span><span class="sxs-lookup"><span data-stu-id="f6cd7-187">Machine Translation Service .NET managed CSOM and Silverlight CSOM</span></span>
<span data-ttu-id="f6cd7-188"><a name="TranslationSvc_ManagedCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-188"></span></span>

<span data-ttu-id="f6cd7-189">Управляемая CSOM .NET: получите экземпляр **ClientContext** (расположенный в пространстве имен **Microsoft.SharePoint.Client** в Microsoft.SharePoint.Client.dll).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-189">For the .NET managed CSOM, get a **ClientContext** instance (located in the **Microsoft.SharePoint.Client** namespace in the Microsoft.SharePoint.Client.dll). Then use the object model in the Microsoft.Office.TranslationServices.Client namespace in the Microsoft.Office.TranslationServices.Client.dll.</span></span> <span data-ttu-id="f6cd7-190">Затем воспользуйтесь объектной моделью в пространстве имен **Microsoft.Office.TranslationServices.Client** в Microsoft.Office.TranslationServices.Client.dll.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-190">For the .NET managed CSOM, get a **ClientContext** instance (located in the Microsoft.SharePoint.Client namespace in the Microsoft.SharePoint.Client.dll). Then use the object model in the Microsoft.Office.TranslationServices.Client namespace in the Microsoft.Office.TranslationServices.Client.dll.</span></span>
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="f6cd7-192">Пример использования управляемой CSOM .NET приведен в статье [SharePoint: доступ к службе машинного перевода с помощью клиентской объектной модели](http://code.msdn.microsoft.com/SharePoint-Perform-a-8e53b06a).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-192">  For sample code demonstrating how to use the .NET Managed CSOM, see  SharePoint 2013: Access Machine Translation Service using the client object model http://code.msdn.microsoft.com/SharePoint-2013-Perform-a-8e53b06a .</span></span>
  
    
    
<span data-ttu-id="f6cd7-193">CSOM Silverlight: получите экземпляр **ClientContext** (расположенный в пространстве имен **Microsoft.SharePoint.Client** в Microsoft.SharePoint.Client.Silverlight.dll).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-193">For the silverlightnv2 CSOM, get a ClientContext instance (located in the Microsoft.SharePoint.Client namespace in the Microsoft.SharePoint.Client.Silverlight.dll). Then use the object model in the Microsoft.Office.TranslationServices.Client namespace in the Microsoft.Office.TranslationServices.Silverlight.dll.</span></span> <span data-ttu-id="f6cd7-194">Затем воспользуйтесь объектной моделью в пространстве имен **Microsoft.Office.TranslationServices.Client** из Microsoft.Office.TranslationServices.Silverlight.dll.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-194">For the silverlightnv2 CSOM, get a **ClientContext** instance (located in the Microsoft.SharePoint.Client namespace in the Microsoft.SharePoint.Client.Silverlight.dll). Then use the object model in the Microsoft.Office.TranslationServices.Client namespace in the Microsoft.Office.TranslationServices.Silverlight.dll.</span></span>
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="f6cd7-196">Пример использования CSOM Silverlight приведен в статье [SharePoint: доступ к службе машинного перевода из приложения Silverlight](http://code.msdn.microsoft.com/SharePoint-Access-cdaff6b2).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-196">  For sample code demonstrating how to use the silverlightnv2 CSOM, see  SharePoint 2013: Access Machine Translation Service from Silverlight application http://code.msdn.microsoft.com/SharePoint-2013-Access-cdaff6b2 .</span></span>
  
    
    
<span data-ttu-id="f6cd7-197">Чтобы выполнить асинхронный перевод одного файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-197">To translate a single file asynchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-198">Чтобы выполнить асинхронный перевод для папки:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-198">To translate a folder asynchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-199">Чтобы выполнить асинхронный перевод для библиотеки:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-199">To translate a library asynchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-200">Чтобы выполнить синхронный перевод одного файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-200">To translate a single file synchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-201">Чтобы получить все языки, поддерживаемые службой машинного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-201">To retrieve all languages that are supported by the spmts:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> supportedLanguages = TranslationJob.EnumerateSupportedLanguages(clientContext);
clientContext.ExecuteQuery();
foreach (string item in supportedLanguages)
{
    Console.Write(item + ", ");
}
```

<span data-ttu-id="f6cd7-202">Чтобы проверить, поддерживается ли конкретный язык:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-202">To check whether a specific language is supported:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsLanguageSupported(clientContext, "language");
clientContext.ExecuteQuery();
```

<span data-ttu-id="f6cd7-203">Чтобы получить все расширения имен файлов, поддерживаемые службой машинного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-203">To retrieve all the file name extensions that are supported by the spmts:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
IEnumerable<string> fileExt = TranslationJob.EnumerateSupportedFileExtensions(clientContext);
clientContext.ExecuteQuery();
foreach (string item in fileExt)
{
    Console.Write(item + ", ");
}
```

<span data-ttu-id="f6cd7-204">Чтобы проверить, поддерживается ли конкретное расширение имени файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-204">To check whether a specific file name extension is supported:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<bool> isSupported;
isSupported = TranslationJob.IsFileExtensionSupported(clientContext, "fileExtension");
clientContext.ExecuteQuery();

```

<span data-ttu-id="f6cd7-205">Чтобы проверить ограничение на размер файла для конкретного расширения:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-205">To check the file size limit for a specific file name extension:</span></span>
  
    
    



```cs

ClientContext clientContext = new ClientContext("http://serverName/sites/siteCollectionPath");
clientResult<int> maxSize;
maxSize = TranslationJob.GetMaximumFileSize(clientContext, "fileExtension");
clientContext.ExecuteQuery();
```


### <a name="machine-translation-service-javascript-csom"></a><span data-ttu-id="f6cd7-206">CSOM JavaScript службы машинного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-206">Machine Translation Service JavaScript CSOM</span></span>
<span data-ttu-id="f6cd7-207"><a name="TranslationSvc_JavaScriptCSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-207"></span></span>

<span data-ttu-id="f6cd7-208">Получите экземпляр **SP.ClientContext**, а затем воспользуйтесь объектной моделью в файле SP.Translation.js.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-208">For the ecmascriptshort CSOM, get an SP.ClientContext instance, and then use the object model in the SP.Translation.js file.</span></span>
  
    
    

  
    
    
![Связанные фрагменты кода и примеры приложений](../images/mod_icon_links_samples.png)
  
    
    
<span data-ttu-id="f6cd7-210">Пример использования CSOM JavaScript приведен в статье [SharePoint: доступ к службе машинного перевода с помощью JavaScript](http://code.msdn.microsoft.com/SharePoint-Accessing-647f6dd9).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-210">  For sample code demonstrating how to use the ecmascriptshort CSOM, see  SharePoint 2013: Accessing the Machine Translation Service with JavaScript http://code.msdn.microsoft.com/SharePoint-2013-Accessing-647f6dd9 .</span></span>
  
    
    
<span data-ttu-id="f6cd7-211">Чтобы выполнить асинхронный перевод одного файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-211">To translate a single file asynchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-212">Чтобы выполнить асинхронный перевод для папки:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-212">To translate a folder asynchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-213">Чтобы выполнить асинхронный перевод для библиотеки:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-213">To translate a library asynchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-214">Чтобы выполнить синхронный перевод одного файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-214">To translate a single file synchronously:</span></span>
  
    
    



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

<span data-ttu-id="f6cd7-215">Чтобы получить все языки, поддерживаемые службой машинного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-215">To retrieve all languages that are supported by the spmts:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedLanguages(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllLang),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="f6cd7-216">Чтобы проверить, поддерживается ли конкретный язык:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-216">To check whether a specific language is supported:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isLanguageSupported(clientContext," language");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestLang),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="f6cd7-217">Чтобы получить все расширения имен файлов, поддерживаемые службой машинного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-217">To retrieve all the file name extensions that are supported by the spmts:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.enumerateSupportedFileExtensions(clientContext);
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededListAllFileExt),Function.createDelegate(this, this.onQueryFailed));
```

<span data-ttu-id="f6cd7-218">Чтобы проверить, поддерживается ли конкретное расширение имени файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-218">To check whether a specific file name extension is supported:</span></span>
  
    
    



```

var clientContext = new SP.ClientContext("serverRelativeUrl");
var contextSite = clientContext.get_site();
var result= SP.Translation.TranslationJob.isFileExtensionSupported(clientContext," fileExtension");
clientContext.executeQueryAsync(Function.createDelegate(this, this.onQuerySucceededTestFileExt),Function.createDelegate(this, this.onQueryFailed));
```


## <a name="machine-translation-service-rest-service"></a><span data-ttu-id="f6cd7-219">Служба REST службы машинного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-219">Machine Translation Service REST service</span></span>
<span data-ttu-id="f6cd7-220"><a name="TranslationSvc_REST"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-220"></span></span>

<span data-ttu-id="f6cd7-221">SharePoint включает службу передачи репрезентативного состояния (REST), позволяющую удаленно управлять приложением службы машинного перевода с помощью любой технологии, которая поддерживает веб-запросы REST.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-221">sp15allshort includes a Representational State Transfer (REST) service that enables you to remotely interact with the spmts application by using any technology that supports REST web requests. For general information about REST in sp15allshort, see Client programming using the SharePoint '15' REST service.</span></span> <span data-ttu-id="f6cd7-222">Общую информацию о службе REST в SharePoint см. в статье [Использование операций запросов OData в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6cd7-222">For general information about the REST service in SharePoint 2013, see  [Use OData query operations in SharePoint REST requests](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).</span></span>
  
    
    

### <a name="ansynchronous-translation-rest-api"></a><span data-ttu-id="f6cd7-223">REST API для асинхронного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-223">Ansynchronous Translation REST API</span></span>

<span data-ttu-id="f6cd7-224">REST API для асинхронного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-224">The REST API for performing asynchronous translation is as follows: http://serverName/_api/TranslationJob('language')</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')`
  
    
    
<span data-ttu-id="f6cd7-225">Чтобы выполнить асинхронный перевод одного файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-225">To translate a single file asynchronously:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFile(inputFile='/path/intput file', outputFile='/path/output file')`
  
    
    
<span data-ttu-id="f6cd7-226">Чтобы выполнить асинхронный перевод для папки:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-226">To translate a folder asynchronously:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateFolder(inputFolder='/path/in', outputFolder='/path/out')`
  
    
    
<span data-ttu-id="f6cd7-227">Чтобы выполнить асинхронный перевод библиотеки:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-227">To translate a library asynchronously:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob('language')/TranslateLibrary(inputLibrary='/LibraryName', outputLibrary='/LibraryName'')`
  
    
    

### <a name="synchronous-translation-rest-api"></a><span data-ttu-id="f6cd7-228">REST API для синхронного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-228">Synchronous Translation REST API</span></span>

<span data-ttu-id="f6cd7-229">Служба REST службы машинного перевода поддерживает только синхронный перевод файлов.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-229">The Machine Translation Service REST service supports only synchronous translation of files.</span></span> <span data-ttu-id="f6cd7-230">Соответствующий API:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-230">The API for this is as follows:</span></span> 
  
    
    
 `http://serverName/_api/SyncTranslator('language')/Translate(outputFile='/path/output file', inputFile='/path/input file')`
  
    
    

### <a name="additional-machine-translation-service-rest-apis"></a><span data-ttu-id="f6cd7-231">Дополнительные REST API службы машинного перевода</span><span class="sxs-lookup"><span data-stu-id="f6cd7-231">Additional Machine Translation Service REST APIs</span></span>

<span data-ttu-id="f6cd7-232">Служба REST службы машинного перевода включает дополнительные API, которые позволяют получить информацию о возможностях приложения службы машинного перевода и состоянии задания на перевод.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-232">The spmts REST service includes additional APIs that you can use to retrieve information about the spmts application capabilities and translation job status.</span></span>
  
    
    
<span data-ttu-id="f6cd7-233">Чтобы получить все языки, поддерживаемые службой машинного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-233">To retrieve all languages supported by Machine Translation Service:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedLanguages`
  
    
    
<span data-ttu-id="f6cd7-234">Чтобы проверить, поддерживается ли конкретный язык:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-234">To check whether a specific language is supported:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.IsLanguageSupported('language')`
  
    
    
<span data-ttu-id="f6cd7-235">Чтобы получить все расширения имени файла, поддерживаемые службой машинного перевода:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-235">To retrieve all the file name extensions that are supported by the spmts:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.EnumerateSupportedFileEXtensions`
  
    
    
<span data-ttu-id="f6cd7-236">Чтобы проверить, поддерживается ли конкретное расширение имени файла:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-236">To check whether a specific file name extension is supported:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.IsFileExtensionSupported('extension')`
  
    
    
<span data-ttu-id="f6cd7-237">Чтобы проверить ограничение на размер файла для конкретного расширения:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-237">To check the file size limit for a specific file name extension:</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.GetMaximumFileSize('extension')`
  
    
    
<span data-ttu-id="f6cd7-238">Чтобы получить список всех заданий на асинхронный перевод:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-238">To retrieve a list of all the asynchronous translation jobs: http://serverName/_api/TranslationJobStatus.GetAllJobs</span></span> 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllJobs`
  
    
    
<span data-ttu-id="f6cd7-239">Чтобы получить список всех активных заданий на асинхронный перевод:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-239">To retrieve a list of all the active asynchronous translation jobs: http://serverName/_api/TranslationJobStatus.GetAllActiveJobs</span></span> 
  
    
    
 `http://serverName/_api/TranslationJobStatus.GetAllActiveJobs`
  
    
    
<span data-ttu-id="f6cd7-240">Чтобы получить информацию о конкретном задании на асинхронный перевод:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-240">To retrieve the document information for a specific asynchronous translation job: http://serverName/_api/TranslationJobStatus('jobid')/GetAllItems</span></span> 
  
    
    
 `http://serverName/_api/TranslationJobStatus('jobid')/GetAllItems`
  
    
    
<span data-ttu-id="f6cd7-241">Чтобы отменить задание на асинхронный перевод:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-241">To cancel an asynchronous translation job: http://serverName/_api/TranslationJob.CancelJob('jobid')</span></span> 
  
    
    
 `http://serverName/_api/TranslationJob.CancelJob('jobid')`
  
    
    

## <a name="requirements-for-microsoft-word-documents"></a><span data-ttu-id="f6cd7-242">Требования для документов Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="f6cd7-242">Requirements for Microsoft Word Documents</span></span>
<span data-ttu-id="f6cd7-243"><a name="TranslationSvc_REST"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-243"></span></span>

<span data-ttu-id="f6cd7-p116">Служба машинного перевода SharePoint переводит документы Microsoft Word с языка абзаца. Например, если абзац написан на испанском языке, но для него выбран английский язык, служба перевода не переведет его на английский, потому что этот язык для него уже выбран.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-p116">SharePoint Machine Translation Service uses the paragraph language as the Source Language when it translates Microsoft Word documents. For example, if the paragraph is written in Spanish but the language for the paragraph is set to English, the Translation Service will not translate it to English. This is because it is already set to English.</span></span>
  
    
    

### <a name="to-set-the-paragraph-language-follow-these-steps"></a><span data-ttu-id="f6cd7-247">Чтобы выбрать язык абзаца, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f6cd7-247">To set the paragraph language, follow these steps:</span></span>


1. <span data-ttu-id="f6cd7-248">Выделите абзац.</span><span class="sxs-lookup"><span data-stu-id="f6cd7-248">Select the paragraph.</span></span>
    
  
2.  <span data-ttu-id="f6cd7-249">Перейдите на вкладку ленты "Рецензирование".</span><span class="sxs-lookup"><span data-stu-id="f6cd7-249">Click the Review Ribbon tab.</span></span>
    
  
3.  <span data-ttu-id="f6cd7-250">Откройте раскрывающееся меню "Язык" и выберите "Язык проверки правописания".</span><span class="sxs-lookup"><span data-stu-id="f6cd7-250">Click Language from the drop-down menu, and choose Set Proofing Language.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="f6cd7-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f6cd7-251">Additional resources</span></span>
<span data-ttu-id="f6cd7-252"><a name="TranslationSvc_AR"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cd7-252"></span></span>


-  [<span data-ttu-id="f6cd7-253">Службы приложений Office 2013 и SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6cd7-253">Office 2013 and SharePoint application services</span></span>](office-and-sharepoint-application-services.md)
    
  

