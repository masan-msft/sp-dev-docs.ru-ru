---
title: "Модули в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c985fed4a6cb047efc81d5b7cf5d11bb17601a84
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="modules-in-the-sharepoint-add-in-model"></a><span data-ttu-id="7cac7-102">Модули в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="7cac7-102">Modules in the SharePoint add-in model</span></span>
======================================

<a name="summary"></a><span data-ttu-id="7cac7-103">Summary</span><span class="sxs-lookup"><span data-stu-id="7cac7-103">Summary</span></span>
-------

<span data-ttu-id="7cac7-104">Подход времени для развертывания артефактов в среде SharePoint отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="7cac7-104">The approach you take to deploy artifacts to a SharePoint environment is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="7cac7-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, модулей, определенных в декларативном кода (компонент framework XML-файлы) были добавлены компоненты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, modules defined in declarative code (feature framework XML files) were added to SharePoint features.</span></span> <span data-ttu-id="7cac7-106">Модули включен список артефакты для развертывания на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-106">The modules included the list of artifacts to deploy to the SharePoint server.</span></span> <span data-ttu-id="7cac7-107">Модули были добавлены компоненты SharePoint и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-107">The modules were added to SharePoint features and deployed via SharePoint Solutions.</span></span> <span data-ttu-id="7cac7-108">После включения компонента артефакты, определенные в модули были развернуты в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-108">Upon feature activation, the artifacts defined in the modules were deployed to the SharePoint environment.</span></span>

<span data-ttu-id="7cac7-109">В модели сценарий надстройки SharePoint удаленного подготовки шаблон используется для развертывания артефактов для среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-109">In a SharePoint Add-in model scenario, the remote provisioning pattern is used to deploy artifacts to SharePoint environments.</span></span>

<a name="terminology"></a><span data-ttu-id="7cac7-110">Терминология</span><span class="sxs-lookup"><span data-stu-id="7cac7-110">Terminology</span></span>
-----------

<span data-ttu-id="7cac7-111">Термин *артефакты* упоминается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7cac7-111">The term *artifacts* is referred to throughout this article.</span></span> <span data-ttu-id="7cac7-112">Артефакты ссылается на элементы, которые обычно развертываются в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-112">Artifacts refers to items that are typically deployed to a SharePoint environment.</span></span> <span data-ttu-id="7cac7-113">Артефакты обычно включают:</span><span class="sxs-lookup"><span data-stu-id="7cac7-113">Artifacts typically include:</span></span>

- <span data-ttu-id="7cac7-114">файлы JavaScript;</span><span class="sxs-lookup"><span data-stu-id="7cac7-114">JavaScript files</span></span>
- <span data-ttu-id="7cac7-115">CSS-файлы</span><span class="sxs-lookup"><span data-stu-id="7cac7-115">CSS files</span></span>
- <span data-ttu-id="7cac7-116">Файлы изображений (.jpg, .gif, .png, и т.д.)</span><span class="sxs-lookup"><span data-stu-id="7cac7-116">Image files (.jpg, .gif, .png, etc.)</span></span>
- <span data-ttu-id="7cac7-117">Главные страницы</span><span class="sxs-lookup"><span data-stu-id="7cac7-117">Master Pages</span></span>
- <span data-ttu-id="7cac7-118">Макеты страниц</span><span class="sxs-lookup"><span data-stu-id="7cac7-118">Page Layouts</span></span>
- <span data-ttu-id="7cac7-119">Элементы списка</span><span class="sxs-lookup"><span data-stu-id="7cac7-119">List Items</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="7cac7-120">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="7cac7-120">High-level guidelines</span></span>
---------------------

<span data-ttu-id="7cac7-121">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для развертывания артефактов для среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-121">As a rule of a thumb, we would like to provide the following high-level guidelines to deploy artifacts to SharePoint environments.</span></span>

- <span data-ttu-id="7cac7-122">Шаблон удаленного подготовки (SharePoint клиентской объектной модели и API-Интерфейс SharePoint REST) для развертывания артефактов для среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-122">Use the remote provisioning pattern (SharePoint Client Side Object Model and SharePoint REST API) to deploy artifacts to SharePoint environments.</span></span>
- <span data-ttu-id="7cac7-123">Не используйте модули декларативного кода или компонента framework XML-файлы для развертывания артефактов для среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-123">Do not use declarative code modules or feature framework XML files to deploy artifacts to SharePoint environments.</span></span>

<span data-ttu-id="7cac7-124">**Отладка**</span><span class="sxs-lookup"><span data-stu-id="7cac7-124">**Debugging**</span></span>

<span data-ttu-id="7cac7-125">Существует возможность отладки процесса развертывания, при использовании кода является большим преимуществом с использованием кода для развертывания артефактов.</span><span class="sxs-lookup"><span data-stu-id="7cac7-125">A big advantage of using code to deploy artifacts is you are able to debug the deployment process when you use code.</span></span> <span data-ttu-id="7cac7-126">Это невозможно для отладки процесса развертывания, при использовании модулей декларативного кода или компонента framework XML-файлы для развертывания артефактов для среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7cac7-126">It is impossible to debug the deployment process when using declarative code modules or feature framework XML files to deploy artifacts to SharePoint environments.</span></span>

<span data-ttu-id="7cac7-127">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="7cac7-127">**Getting started**</span></span>

<span data-ttu-id="7cac7-128">В следующих примерах кода PnP O365 демонстрируется создание SharePoint Add-ins, разворачивают артефакты в среде SharePoint с удаленного подготовки шаблон.</span><span class="sxs-lookup"><span data-stu-id="7cac7-128">The following O365 PnP code samples demonstrate how to create a SharePoint Add-ins that use the remote provisioning pattern to deploy artifacts to a SharePoint environment.</span></span>

  <span data-ttu-id="7cac7-129">В этом примере показано, как создавать новые папки в библиотеку стилей и добавление файлов JavaScript и изображения для новых файлов.</span><span class="sxs-lookup"><span data-stu-id="7cac7-129">This sample demonstrates how to create a new folders in the Style Library and add JavaScript files and images to the new files.</span></span>

- [<span data-ttu-id="7cac7-130">Branding.ClientSideRendering (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="7cac7-130">Branding.ClientSideRendering (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + <span data-ttu-id="7cac7-131">В разделе ***UploadJSFiles*** и ***UploadFileToFolder*** методы в [классе Default.aspx.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.ClientSideRendering/Branding.ClientSideRenderingWeb/Pages/Default.aspx.cs) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="7cac7-131">See the ***UploadJSFiles*** and the ***UploadFileToFolder*** methods in the [Default.aspx.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.ClientSideRendering/Branding.ClientSideRenderingWeb/Pages/Default.aspx.cs) for more details.</span></span>
    + <span data-ttu-id="7cac7-132">Эти методы также отображаются под для краткая справка.</span><span class="sxs-lookup"><span data-stu-id="7cac7-132">These methods are also displayed below for quick reference.</span></span>
    
        <span data-ttu-id="7cac7-133">**Создайте папку и отправки файлов JavaScript в папку:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-133">**Create a folder and upload JavaScript files to the folder:**</span></span>

        ```
        void UploadJSFiles(Web web)
        {
            //Delete the folder if it exists
            Microsoft.SharePoint.Client.List list = web.Lists.GetByTitle("Style Library");
            IEnumerable<Folder> results = web.Context.LoadQuery<Folder>(list.RootFolder.Folders.Where(folder => folder.Name == "JSLink-Samples"));
            web.Context.ExecuteQuery();
            Folder samplesJSfolder = results.FirstOrDefault();
        
            if (samplesJSfolder != null)
            {
                samplesJSfolder.DeleteObject();
                web.Context.ExecuteQuery();
            }
        
            //Create new folder
            samplesJSfolder = list.RootFolder.Folders.Add("JSLink-Samples");
            web.Context.Load(samplesJSfolder);
            web.Context.ExecuteQuery();
        
            //Upload JavaScript files to folder
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/Accordion.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/ConfidentialDocuments.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/DisableInput.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/HiddenField.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/PercentComplete.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/PriorityColor.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/ReadOnlySPControls.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/RegexValidator.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/SubstringLongText.js"), samplesJSfolder);
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/DependentFields.js"), samplesJSfolder);
        
            //Create another folder inside the folder that was just created
            Folder imgsFolder = samplesJSfolder.Folders.Add("imgs");
            web.Context.Load(imgsFolder);
            web.Context.ExecuteQuery();
        
            //Upload image files to folder
            UploadFileToFolder(web, Server.MapPath("../Scripts/JSLink-Samples/imgs/Confidential.png"), imgsFolder);
        }
        ```
        <span data-ttu-id="7cac7-134">**Создайте папку и отправки файлы изображений в папку:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-134">**Create a folder and upload image files to the folder:**</span></span>
        ```
        public static void UploadFileToFolder(Web web, string filePath, Folder folder)
            {
            //Create a FileStream to the file to upload
                using (FileStream fs = new FileStream(filePath, FileMode.Open))
                {
                //Create FileCreationInformation object to set file metadata
                    FileCreationInformation flciNewFile = new FileCreationInformation();
    
                    flciNewFile.ContentStream = fs;
                    flciNewFile.Url = System.IO.Path.GetFileName(filePath);
                    flciNewFile.Overwrite = true;
    
                //Upload file to SharePoint
                        Microsoft.SharePoint.Client.File uploadFile = folder.Files.Add(flciNewFile);
    
                //Check in the file
                    uploadFile.CheckIn("CSR sample js file", CheckinType.MajorCheckIn);
    
                    folder.Context.Load(uploadFile);
                    folder.Context.ExecuteQuery();
                }
        }
        ```

<span data-ttu-id="7cac7-135">В этом примере показано, как отправить главные страницы, задайте метаданных главной страницы и применение главной страницы к сайту путем установки свойства CustomMasterUrl веб-объект.</span><span class="sxs-lookup"><span data-stu-id="7cac7-135">This sample demonstrates how to upload master pages, set master page meta data and apply the master page to the site by setting the CustomMasterUrl property on the Web object.</span></span>

- [<span data-ttu-id="7cac7-136">Branding.ApplyBranding (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="7cac7-136">Branding.ApplyBranding (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
    + <span data-ttu-id="7cac7-137">В разделе ***UploadPageLayout***, ***CreatePublishingPage***и ***SetSupportCaseContent*** методы в [классе BrandingHelper.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.ApplyBranding/Branding.ApplyBranding.Console/BrandingHelper.cs) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="7cac7-137">See the ***UploadPageLayout***, ***CreatePublishingPage***, and ***SetSupportCaseContent*** methods in the [BrandingHelper.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.ApplyBranding/Branding.ApplyBranding.Console/BrandingHelper.cs) for more details.</span></span>
    + <span data-ttu-id="7cac7-138">Помимо создания новых элементов в SharePoint, в этом примере показано, как удалить элементы.</span><span class="sxs-lookup"><span data-stu-id="7cac7-138">In addition to creating new items in SharePoint, this sample demonstrates how to remove items.</span></span>  <span data-ttu-id="7cac7-139">Ниже перечислены методы, которые удаления элементов для ссылки.</span><span class="sxs-lookup"><span data-stu-id="7cac7-139">The methods which remove items are listed below for reference.</span></span>  
        <span data-ttu-id="7cac7-140">**Удаление файла:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-140">**Delete a file:**</span></span>
    
        ```
        private static void DeleteFile(Web web, string fileName, string serverPath, string serverFolder)
        {
            var fileUrl = string.Concat(serverPath, serverFolder, (string.IsNullOrEmpty(serverFolder) ? string.Empty : "/"), fileName);
            var fileToDelete = web.GetFileByServerRelativeUrl(fileUrl);
            fileToDelete.DeleteObject();
            web.Context.ExecuteQuery();
        }
    
        ```
        <span data-ttu-id="7cac7-141">**Удаление папки:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-141">**Delete a folder:**</span></span>
        ```
        public static void RemoveFolder(ClientContext clientContext, string folder, string path)
            {
                var web = clientContext.Web;
                var filePath = web.ServerRelativeUrl.TrimEnd(Program.trimChars) + "/" + path + "/";
                var folderToDelete = web.GetFolderByServerRelativeUrl(string.Concat(filePath, folder));
                Console.WriteLine("Removing folder {0} from {1}", folder, path);
                folderToDelete.DeleteObject();
                clientContext.ExecuteQuery();
            }
        ```
        <span data-ttu-id="7cac7-142">**Отмена назначения главной страницы "и" удаление главной страницы**</span><span class="sxs-lookup"><span data-stu-id="7cac7-142">**Un-assign a master page and delete the master page**</span></span>
        ```
        public static void RemoveMasterPage(ClientContext clientContext, string name, string folder)
            {
                var web = clientContext.Web;
                clientContext.Load(web, w => w.AllProperties);
                clientContext.ExecuteQuery();
    
                Console.WriteLine("Deactivating and removing {0} from {1}", name, web.ServerRelativeUrl);            
            
                //set master pages back to the defaults that were being used
                if (web.AllProperties.FieldValues.ContainsKey("OriginalMasterUrl"))
                {
                    web.MasterUrl = (string)web.AllProperties["OriginalMasterUrl"];
                }
                if (web.AllProperties.FieldValues.ContainsKey("CustomMasterUrl"))
                {
                    web.CustomMasterUrl = (string)web.AllProperties["CustomMasterUrl"];
                }
                web.Update();
                clientContext.ExecuteQuery();
    
                //now that the master page is set back to its default, re-reference the web from context and delete the custom master pages
                web = clientContext.Web;
                var lists = web.Lists;
                var gallery = web.GetCatalog(116);
                clientContext.Load(lists, l => l.Include(ll => ll.DefaultViewUrl));
                clientContext.Load(gallery, g => g.RootFolder.ServerRelativeUrl);
                clientContext.ExecuteQuery();
                var masterPath = gallery.RootFolder.ServerRelativeUrl.TrimEnd(new char[] { '/' }) + "/";
                DeleteFile(web, name, masterPath, folder);
            }
        ```
        <span data-ttu-id="7cac7-143">**Удаление макета страницы**</span><span class="sxs-lookup"><span data-stu-id="7cac7-143">**Delete a page layout**</span></span>
        ```
        public static void RemovePageLayout(ClientContext clientContext, string name, string folder)
        {
            var web = clientContext.Web;
                var lists = web.Lists;
                var gallery = web.GetCatalog(116);
                clientContext.Load(lists, l => l.Include(ll => ll.DefaultViewUrl));
                clientContext.Load(gallery, g => g.RootFolder.ServerRelativeUrl);
                clientContext.ExecuteQuery();
    
                Console.WriteLine("Removing page layout {0} from {1}", name, clientContext.Web.ServerRelativeUrl);
    
                var masterPath = gallery.RootFolder.ServerRelativeUrl.TrimEnd(Program.trimChars) + "/";
            
                DeleteFile(web, name, masterPath, folder);
        }
        ```

    + <span data-ttu-id="7cac7-144">Посмотрите, [Применение фирменной символики для сайтов SharePoint с помощью надстройки уровня приложения для SharePoint (Office 365 PnP видео)](https://channel9.msdn.com/Blogs/Office-365-Dev/Applying-Branding-to-SharePoint-Sites-with-an-App-for-SharePoint-Office-365-Developer-Patterns-and-P) для прохода через этот пример.</span><span class="sxs-lookup"><span data-stu-id="7cac7-144">Watch the [Applying Branding to SharePoint Sites with an Add-in for SharePoint (Office 365 PnP Video)](https://channel9.msdn.com/Blogs/Office-365-Dev/Applying-Branding-to-SharePoint-Sites-with-an-App-for-SharePoint-Office-365-Developer-Patterns-and-P) for a walk through of this sample.</span></span>

<span data-ttu-id="7cac7-145">В этом примере немного состоит из everythign в нем.</span><span class="sxs-lookup"><span data-stu-id="7cac7-145">This sample has a little of everythign in it.</span></span>  <span data-ttu-id="7cac7-146">Показывается, как активировать функции публикации, отправка макеты страниц, создание страниц публикации, создать списки, типы контента и элементов списка и создания страниц pblishing и добавление веб-частей и добавить в части страницы.</span><span class="sxs-lookup"><span data-stu-id="7cac7-146">It demonstrates how to activate the publishing features, upload page layouts, create publishing pages, create lists, content types and list items, and creating pblishing pages and adding Web Parts and Add-in Parts to the pages.</span></span>  <span data-ttu-id="7cac7-147">Также демонстрируется развертывание элементов списка на веб-сайт и web-надстройки.</span><span class="sxs-lookup"><span data-stu-id="7cac7-147">It also demonstrates how to deploy list items to both the host web and the Add-in web.</span></span>

- [<span data-ttu-id="7cac7-148">Branding.ClientSideRendering (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="7cac7-148">Branding.ClientSideRendering (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + <span data-ttu-id="7cac7-149">В разделе методы в [классе Utils.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Core.DataStorageModels/Core.DataStorageModelsWeb/Util/Util.cs) примеры этих операций.</span><span class="sxs-lookup"><span data-stu-id="7cac7-149">See the methods in the [Utils.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Core.DataStorageModels/Core.DataStorageModelsWeb/Util/Util.cs) for examples of these operations.</span></span>
    + <span data-ttu-id="7cac7-150">Ниже перечислены эти методы для ссылки.</span><span class="sxs-lookup"><span data-stu-id="7cac7-150">These methods are listed below for reference.</span></span>  
        <span data-ttu-id="7cac7-151">**Активация семейства веб-сайтов и компоненты уровня публикации сайта:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-151">**Activate site collection and site level publishing features:**</span></span>
        ```
        public static void ActivePublishingFeature(ClientContext ctx)
        {
            Guid publishingSiteFeatureId = new Guid("f6924d36-2fa8-4f0b-b16d-06b7250180fa");
            Guid publishingWebFeatureId = new Guid("94c94ca6-b32f-4da9-a9e3-1f3d343d7ecb");
    
            Site clientSite = ctx.Site;
            ctx.Load(clientSite);
    
            FeatureCollection clientSiteFeatures = clientSite.Features;
            ctx.Load(clientSiteFeatures);
    
            //Activate the site feature
            clientSiteFeatures.Add(publishingSiteFeatureId, true, FeatureDefinitionScope.Farm);
            ctx.ExecuteQuery();
    
            FeatureCollection clientWebFeatures = ctx.Web.Features;
            ctx.Load(clientWebFeatures);
    
            //Activate the web feature
            clientWebFeatures.Add(publishingWebFeatureId, true, FeatureDefinitionScope.Farm);
            ctx.ExecuteQuery();
        }
        ```
        <span data-ttu-id="7cac7-152">**Создание списка:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-152">**Create a list:**</span></span>
        ```
        public static List CreateList(ClientContext ctx, int templateType,
                                           string title, string url, QuickLaunchOptions quickLaunchOptions)
        {
            ListCreationInformation listCreationInfo = new ListCreationInformation
            {
                TemplateType = templateType,
                Title = title,
                Url = url,
                QuickLaunchOption = quickLaunchOptions
            };
            List spList = ctx.Web.Lists.Add(listCreationInfo);
            ctx.Load(spList);
            ctx.ExecuteQuery();
    
            return spList;
        }
    
        ```
        <span data-ttu-id="7cac7-153">**Создание типа контента**</span><span class="sxs-lookup"><span data-stu-id="7cac7-153">**Create a content type**</span></span>
        ```
        public static ContentType CreateContentType(ClientContext ctx, string ctyName, string group, string ctyId)
        {
            ContentTypeCreationInformation contentTypeCreation = new ContentTypeCreationInformation();
            contentTypeCreation.Name = ctyName;
            contentTypeCreation.Description = "Custom Content Type";
            contentTypeCreation.Group = group;
            contentTypeCreation.Id = ctyId;
    
            //Add the new content type to the collection
            ContentType ct = ctx.Web.ContentTypes.Add(contentTypeCreation);
            ctx.Load(ct);
            ctx.ExecuteQuery();
    
            return ct;
        }
    
        ```
        <span data-ttu-id="7cac7-154">**Отправка макета страницы**</span><span class="sxs-lookup"><span data-stu-id="7cac7-154">**Upload a page layout**</span></span>
        ```
        public static void UploadPageLayout(ClientContext ctx, string sourcePath, string targetListTitle, string targetUrl)
            {
            using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
            {
                byte[] data = new byte[fs.Length];
                fs.Read(data, 0, data.Length);
                using (MemoryStream ms = new MemoryStream())
                {
                    ms.Write(data, 0, data.Length);
                    var newfile = new FileCreationInformation();
                    newfile.Content = ms.ToArray();
                    newfile.Url = targetUrl;
                    newfile.Overwrite = true;
    
                    List docs = ctx.Web.Lists.GetByTitle(targetListTitle);
                    Microsoft.SharePoint.Client.File uploadedFile = docs.RootFolder.Files.Add(newfile);
                    uploadedFile.CheckOut();
                    uploadedFile.CheckIn("Data storage model", CheckinType.MajorCheckIn);
                    uploadedFile.Publish("Data storage model layout.");
    
                    ctx.Load(uploadedFile);
                    ctx.ExecuteQuery();
                }
            }
        }
    
        ```
        <span data-ttu-id="7cac7-155">**Создайте страницу публикации и назначьте его макет страницы:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-155">**Create a publishing page and set its page layout:**</span></span>
        ```
        public static void CreatePublishingPage(ClientContext clientContext, string pageName, string pagelayoutname, string url, string queryurl)
            {
                var publishingPageName = pageName + ".aspx";
    
                Web web = clientContext.Web;
                clientContext.Load(web);
    
                List pages = web.Lists.GetByTitle("Pages");
                clientContext.Load(pages.RootFolder, f => f.ServerRelativeUrl);
                clientContext.ExecuteQuery();
    
                Microsoft.SharePoint.Client.File file =
                    web.GetFileByServerRelativeUrl(pages.RootFolder.ServerRelativeUrl + "/" + pageName + ".aspx");
                clientContext.Load(file, f => f.Exists);
                clientContext.ExecuteQuery();
                if(file.Exists)
                {
                    file.DeleteObject();
                    clientContext.ExecuteQuery();
                }
                PublishingWeb publishingWeb = PublishingWeb.GetPublishingWeb(clientContext, web);
                clientContext.Load(publishingWeb);
    
                if (publishingWeb != null)
                {
                    List publishingLayouts = clientContext.Site.RootWeb.Lists.GetByTitle("Master Page Gallery");
    
                    ListItemCollection allItems = publishingLayouts.GetItems(CamlQuery.CreateAllItemsQuery());
                    clientContext.Load(allItems, items => items.Include(item => item.DisplayName).Where(obj => obj.DisplayName == pagelayoutname));
                    clientContext.ExecuteQuery();
    
                    ListItem layout = allItems.Where(x => x.DisplayName == pagelayoutname).FirstOrDefault();
                    clientContext.Load(layout);
    
                    PublishingPageInformation publishingpageInfo = new PublishingPageInformation()
                    {
                        Name = publishingPageName,
                        PageLayoutListItem = layout,
                    };
    
                    PublishingPage publishingPage = publishingWeb.AddPublishingPage(publishingpageInfo);
                    publishingPage.ListItem.File.CheckIn(string.Empty, CheckinType.MajorCheckIn);
                    publishingPage.ListItem.File.Publish(string.Empty);
                    clientContext.ExecuteQuery();
                }
                SetSupportCaseContent(clientContext, "SupportCasesPage", url, queryurl);
            }
        ```
        <span data-ttu-id="7cac7-156">**Создание элементов списка**</span><span class="sxs-lookup"><span data-stu-id="7cac7-156">**Create list items**</span></span>
        ```
        public static void AddDemoDataToSupportCasesList(ClientContext ctx, List list, string title,
                                                           string status, string csr, string customerID)
        {
            ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation();
            ListItem newItem = list.AddItem(itemCreateInfo);
            newItem["Title"] = title;
            newItem["FTCAM_Status"] = status;
            newItem["FTCAM_CSR"] = csr;
            newItem["FTCAM_CustomerID"] = customerID;
            newItem.Update();
            ctx.ExecuteQuery();
        }
        ```
        <span data-ttu-id="7cac7-157">**Подготовка контента на страницу публикации (содержимое с веб-части поиска, редактор сценариев веб-части, часть Add-in) и публикации страницы:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-157">**Provision content into a publishing page (Content By Search Web Part, Script Editor Web Part, Add-in Part) and publish the page:**</span></span>
        ```
        public static void SetSupportCaseContent(ClientContext ctx, string pageName, string url, string queryurl)
        {
            List pages = ctx.Web.Lists.GetByTitle("Pages");
            ctx.Load(pages.RootFolder, f => f.ServerRelativeUrl);
            ctx.ExecuteQuery();
    
            Microsoft.SharePoint.Client.File file =
                ctx.Web.GetFileByServerRelativeUrl(pages.RootFolder.ServerRelativeUrl + "/" + pageName + ".aspx");
            ctx.Load(file);
            ctx.ExecuteQuery();
    
            file.CheckOut();
    
            LimitedWebPartManager limitedWebPartManager = file.GetLimitedWebPartManager(PersonalizationScope.Shared);
    
            string quicklaunchmenuFormat =
                @"<div><a href='{0}/{1}'>Sample Home Page</a></div>
                <br />
                <div style='font-weight:bold'>CSR Dashboard</div>
                <div class='cdsm_mainmenu'>
                    <ul>
                        <li><a href='{0}/CSRInfo/{1}'>My CSR Info</a></li>
                        <li><a href='{0}/CallQueue/{1}'>Call Queue</a></li>
                        <li>
                            <span class='collapse_arrow'></span>
                            <span><a href='{0}/CustomerDashboard/{1}'>Customer Dashboard</a></span>
                            <ul>
                                <li><a href='{0}/CustomerDashboard/Orders{1}'>Recent Orders</a></li>
                                <li><a class='current' href='#'>Support Cases</a></li>
                                <li><a href='{0}/CustomerDashboard/Notes{1}'>Notes</a></li>
                            </ul>
                        </li>
                    </ul>
                </div>
                <div class='cdsm_submenu'>
                </div>";
    
            string quicklaunchmenu = string.Format(quicklaunchmenuFormat, url, queryurl);
    
            string qlwebPartXml = "<?xml version=\"1.0\" encoding=\"utf-8\"?><webParts><webPart xmlns=\"http://schemas.microsoft.com/WebPart/v3\"><metaData><type name=\"Microsoft.SharePoint.WebPartPages.ScriptEditorWebPart, Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c\" /><importErrorMessage>Cannot import this Web Part.</importErrorMessage></metaData><data><properties><property name=\"Content\" type=\"string\"><![CDATA[" + quicklaunchmenu + "]]></property><property name=\"ChromeType\" type=\"chrometype\">None</property></properties></data></webPart></webParts>";
            WebPartDefinition qlWpd = limitedWebPartManager.ImportWebPart(qlwebPartXml);
            WebPartDefinition qlWpdNew = limitedWebPartManager.AddWebPart(qlWpd.WebPart, "SupportCasesZoneLeft", 0);
            ctx.Load(qlWpdNew);
    
            //Customer Dropdown List Script Web Part
            string dpwebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/CustomerDropDownlist.webpart");
            WebPartDefinition dpWpd = limitedWebPartManager.ImportWebPart(dpwebPartXml);
            WebPartDefinition dpWpdNew = limitedWebPartManager.AddWebPart(dpWpd.WebPart, "SupportCasesZoneTop", 0);
            ctx.Load(dpWpdNew);
    
            //Support Case CBS Info Web Part
            string cbsInfoWebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/SupportCaseCBSWebPartInfo.webpart");
            WebPartDefinition cbsInfoWpd = limitedWebPartManager.ImportWebPart(cbsInfoWebPartXml);
            WebPartDefinition cbsInfoWpdNew = limitedWebPartManager.AddWebPart(cbsInfoWpd.WebPart, "SupportCasesZoneMiddle", 0);
            ctx.Load(cbsInfoWpdNew);
    
            //Support Case Content By Search Web Part
            string cbswebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/SupportCase CBS Webpart/SupportCaseCBS.webpart");
            WebPartDefinition cbsWpd = limitedWebPartManager.ImportWebPart(cbswebPartXml);
            WebPartDefinition cbsWpdNew = limitedWebPartManager.AddWebPart(cbsWpd.WebPart, "SupportCasesZoneMiddle", 1);
            ctx.Load(cbsWpdNew);
    
            //Support Cases App Part
            string appPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/SupportCaseAppPart.webpart");
            WebPartDefinition appPartWpd = limitedWebPartManager.ImportWebPart(appPartXml);
            WebPartDefinition appPartdNew = limitedWebPartManager.AddWebPart(appPartWpd.WebPart, "SupportCasesZoneBottom", 0);
            ctx.Load(appPartdNew);
    
            //Get Host Web Query String and show support case list web part
            string querywebPartXml = System.IO.File.ReadAllText(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "Assets/GetHostWebQueryStringAndShowList.webpart");
            WebPartDefinition queryWpd = limitedWebPartManager.ImportWebPart(querywebPartXml);
            WebPartDefinition queryWpdNew = limitedWebPartManager.AddWebPart(queryWpd.WebPart, "SupportCasesZoneBottom", 1);
            ctx.Load(queryWpdNew);
    
    
            file.CheckIn("Data storage model", CheckinType.MajorCheckIn);
            file.Publish("Data storage model");
            ctx.Load(file);
            ctx.ExecuteQuery();
        }
    ```

    + <span data-ttu-id="7cac7-158">В разделе ***FillHostWebSupportCasesToThreshold*** и ***FillAppWebNotesListToThreshold*** методы [класса SharePointService.cs](https://github.com/SharePoint/PnP/blob/master/Samples/Core.DataStorageModels/Core.DataStorageModelsWeb/Services/SharePointService.cs) для получения дополнительных сведений о развертывании элементов списка на хост-сайта и на-сайте.</span><span class="sxs-lookup"><span data-stu-id="7cac7-158">See the ***FillHostWebSupportCasesToThreshold*** and the ***FillAppWebNotesListToThreshold*** methods in the [SharePointService.cs class](https://github.com/SharePoint/PnP/blob/master/Samples/Core.DataStorageModels/Core.DataStorageModelsWeb/Services/SharePointService.cs) for more details about deploying list items to both the host web and the Add-in web.</span></span>  
    + <span data-ttu-id="7cac7-159">***Важное примечание:*** Же хост-сайта и добавить в соответствующие web в этом примере демонстрируются могут быть применены к любому типу артефактов выполнить их развертывание в соответствующем расположении.</span><span class="sxs-lookup"><span data-stu-id="7cac7-159">***Important note:*** The same host web and Add-in web approaches demonstrated in this sample may be applied to any type of artifact to deploy them to the appropriate location.</span></span>

        <span data-ttu-id="7cac7-160">**Добавление элементов списка в список хост-сайте:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-160">**Add list items to a list in the host web:**</span></span>
        ```
        public string FillHostWebSupportCasesToThreshold()
            {
                using (var clientContext = SharePointContext.CreateUserClientContextForSPHost())
                {
                    List supportCasesList = clientContext.Web.Lists.GetByTitle("Support Cases");
                    ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation();
                    for (int i = 0; i < 500; i++)
                    {
                        ListItem newItem = supportCasesList.AddItem(itemCreateInfo);
                        newItem["Title"] = "Wrong product received." + i.ToString();
                        newItem["FTCAM_Status"] = "Open";
                        newItem["FTCAM_CSR"] = "bjones";
                        newItem["FTCAM_CustomerID"] = "thresholds test";
                        newItem.Update();
                        if (i % 100 == 0)
                            clientContext.ExecuteQuery();
                    }
                    clientContext.ExecuteQuery();
    
               
                    clientContext.Load(supportCasesList, l => l.ItemCount);
                    clientContext.ExecuteQuery();
    
                    if(supportCasesList.ItemCount>=5000)
                        return "The Host Web Support Cases List has " + supportCasesList.ItemCount + " items, and exceeds the threshold.";
                    else
                        return 500 + " items have been added to the Host Web Support Cases List. " +
                         "There are " + (5000 - supportCasesList.ItemCount) + " items left to add.";    
            }
        }
        ```
    
        <span data-ttu-id="7cac7-161">**Добавление элементов списка в список Добавить в веб-сайта:**</span><span class="sxs-lookup"><span data-stu-id="7cac7-161">**Add list items to a list in the Add-in web:**</span></span>
        ```
        public string FillAppWebNotesListToThreshold()
            {
                using (var clientContext = SharePointContext.CreateUserClientContextForSPAppWeb())
                {
                    List notesList = clientContext.Web.Lists.GetByTitle("Notes");
    
                    var itemCreateInfo = new ListItemCreationInformation();
                    for (int i = 0; i < 500; i++)
                    {
                        ListItem newItem = notesList.AddItem(itemCreateInfo);
                        newItem["Title"] = "Notes Title." + i.ToString();
                        newItem["FTCAM_Description"] = "Notes description";
                        newItem.Update();
                        if (i % 100 == 0)
                            clientContext.ExecuteQuery();
                    }
                    clientContext.ExecuteQuery();
    
                    clientContext.Load(notesList, l => l.ItemCount);
                    clientContext.ExecuteQuery();
    
                    if (notesList.ItemCount >= 5000)
                        return "The Add-in Web Notes List has " + notesList.ItemCount + " items, and exceeds the threshold.";
                    else
                        return 500 + " items have been added to the Add-in Web Notes List. " +
                                       "There are " + (5000-notesList.ItemCount) + " items left to add.";          
                }
            }
        ```
    
<a name="related-links"></a><span data-ttu-id="7cac7-162">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="7cac7-162">Related links</span></span>
=============

- [<span data-ttu-id="7cac7-163">Главные страницы (надстройки SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="7cac7-163">Master Pages (SharePoint Add-in Recipe)</span></span>](master-pages-sharepoint-add-in.md)
- <span data-ttu-id="7cac7-164">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="7cac7-164">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="7cac7-165">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="7cac7-165">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="7cac7-166">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="7cac7-166">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="7cac7-167">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="7cac7-167">Related PnP samples</span></span>
===================

- [<span data-ttu-id="7cac7-168">Branding.ClientSideRendering (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="7cac7-168">Branding.ClientSideRendering (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- [<span data-ttu-id="7cac7-169">Branding.ApplyBranding (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="7cac7-169">Branding.ApplyBranding (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
- [<span data-ttu-id="7cac7-170">Branding.ClientSideRendering (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="7cac7-170">Branding.ClientSideRendering (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- <span data-ttu-id="7cac7-171">Примеры и содержимое в [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span><span class="sxs-lookup"><span data-stu-id="7cac7-171">Samples and content at [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="7cac7-172">Применимо к</span><span class="sxs-lookup"><span data-stu-id="7cac7-172">Applies to</span></span>
==========
- <span data-ttu-id="7cac7-173">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="7cac7-173">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="7cac7-174">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="7cac7-174">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="7cac7-175">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="7cac7-175">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="7cac7-176">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="7cac7-176">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
