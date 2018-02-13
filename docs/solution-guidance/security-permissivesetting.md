# <a name="introduction"></a><span data-ttu-id="decdc-101">Введение</span><span class="sxs-lookup"><span data-stu-id="decdc-101">Introduction</span></span>
<span data-ttu-id="decdc-102">Большая часть SharePoint Online клиентов значками open работу в файл с помощью **строго** модели.</span><span class="sxs-lookup"><span data-stu-id="decdc-102">Most of the SharePoint Online tenants handles the file open experience using the **strict** model.</span></span> <span data-ttu-id="decdc-103">В результате все файлы, которые потенциально могут вызывать вред (например HTML-файл, внедренный сценарий) не выполняются в браузере, но загружается или отображаться в виде необработанное содержимое (Предварительный просмотр HTML-код в современном пользовательского интерфейса).</span><span class="sxs-lookup"><span data-stu-id="decdc-103">As a result, all files which can potentially cause harm (e.g. a html file having embedded script) are not executed in the browser but downloaded or shown as raw content (html preview in the modern user experience).</span></span> <span data-ttu-id="decdc-104">Если клиент настроен с помощью **Нестрогое** модель взаимодействия открыть файл будет выполняться файла, например получение выполняется HTML-файла в библиотеке документов и страница отображается в браузере.</span><span class="sxs-lookup"><span data-stu-id="decdc-104">If your tenant is configured using the **permissive** model then the file open experience will execute the file, for example a html file in a document library does get executed and page is shown in the browser.</span></span> <span data-ttu-id="decdc-105">В strict этого файла будут загружены.</span><span class="sxs-lookup"><span data-stu-id="decdc-105">In strict this file would be downloaded.</span></span>

<span data-ttu-id="decdc-106">Сегодня по умолчанию строгие и вы уже не могут переключиться вашего клиента для разрешительной модели.</span><span class="sxs-lookup"><span data-stu-id="decdc-106">Today the default setting is strict, and you already cannot switch your tenant to the permissive model.</span></span> <span data-ttu-id="decdc-107">Для клиентов, которым переключения, чтобы Нестрогое из прошлых элементов изменит: Нестрогое модель клиента является устаревшим, в этот момент всех клиентов переключается в strict.</span><span class="sxs-lookup"><span data-stu-id="decdc-107">For tenants that switched to permissive in the past things will change: the tenant permissive model will be deprecated, at that point all tenants will be switched to strict.</span></span>


# <a name="is-my-tenant-impacted"></a><span data-ttu-id="decdc-108">Мои клиента на которые оказывает?</span><span class="sxs-lookup"><span data-stu-id="decdc-108">Is my tenant impacted?</span></span>
<span data-ttu-id="decdc-109">Для этого рекомендуется, установив параметр PermissiveBrowserFileHandlingOverride, с помощью [Office 365 PowerShell для SharePoint Online](https://technet.microsoft.com/en-us/library/fp161362.aspx):</span><span class="sxs-lookup"><span data-stu-id="decdc-109">The recommended approach to check this is by checking the PermissiveBrowserFileHandlingOverride setting using [Office 365 PowerShell for SharePoint Online](https://technet.microsoft.com/en-us/library/fp161362.aspx):</span></span>

```PowerShell
Connect-SPOService -url https://contoso-admin.sharepoint.com
$tenant = get-spotenant
$tenant.PermissiveBrowserFileHandlingOverride
```

<span data-ttu-id="decdc-110">Если это приводит к **значение False,** затем вашего клиента это не повлияет на, если задано значение **True,** а затем необходимо подготовить предстоящие прекратить.</span><span class="sxs-lookup"><span data-stu-id="decdc-110">If this results in **False** then your tenant is not impacted, if this is set to **True** then you need prepare for the upcoming deprecation.</span></span> 

# <a name="how-can-i-prepare-for-changing-permissive-into-strict"></a><span data-ttu-id="decdc-111">Как подготовить для изменения разрешений в strict</span><span class="sxs-lookup"><span data-stu-id="decdc-111">How can I prepare for changing permissive into strict?</span></span>

![Показывает Нестрогое strict модели](media/permissivetostrictmodel.png)

## <a name="step-1-assess-the-impact"></a><span data-ttu-id="decdc-113">Шаг 1: Оценить влияние</span><span class="sxs-lookup"><span data-stu-id="decdc-113">Step 1: Assess the impact</span></span>
<span data-ttu-id="decdc-114">Общие сведения о относится какие файлы — это первый шаг и вы можете сделать это с помощью сканера Нестрогое файлов.</span><span class="sxs-lookup"><span data-stu-id="decdc-114">Understanding which files are impacted is a first step and you can do that via the permissive file scanner.</span></span> <span data-ttu-id="decdc-115">В разделе [Нестрогое сканера SharePoint](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.PermissiveFile.Scanner) для получения дополнительных сведений о сканер и способы его использования.</span><span class="sxs-lookup"><span data-stu-id="decdc-115">See the [SharePoint Permissive Scanner](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.PermissiveFile.Scanner) to learn more about the scanner and how to use it.</span></span> <span data-ttu-id="decdc-116">В конфигурации по умолчанию в этом сканера ищет файлы html/html, но с помощью параметров командной строки можно запросить сканера для поиска дополнительных типов файлов.</span><span class="sxs-lookup"><span data-stu-id="decdc-116">In the default configuration this scanner searches for html/html files, but using the command line options you can request the scanner to search for additional filetypes.</span></span>

<span data-ttu-id="decdc-117">В результате сканер является CSV-файла, где перечислены все задействованной (html/htm + необязательно других типов файлов) файлов, в том числе сведения о html/htm-файлы (число ссылок и сценарии, которые используются, последнего изменения данных, количество просмотров).</span><span class="sxs-lookup"><span data-stu-id="decdc-117">The result of the scanner is CSV file listing all the impacted (html/htm + optional other file types) files, including information about the html/htm files (number of links and scripts that are used, last change data, number of views).</span></span>

## <a name="step-2-analyze-the-scan-results"></a><span data-ttu-id="decdc-118">Этап 2: Анализ результатов проверки</span><span class="sxs-lookup"><span data-stu-id="decdc-118">Step 2: Analyze the scan results</span></span>
<span data-ttu-id="decdc-119">После списка задействованной файлов необходимо оценить которого, если эти файлы и сайты, использующие эти файлы, соответствующие по-прежнему business.</span><span class="sxs-lookup"><span data-stu-id="decdc-119">Once you’ve the list of impacted files you need to assess which if these files and the sites holding these files are still business relevant.</span></span> <span data-ttu-id="decdc-120">Файл и/или сайт может быть устарели, а если so исправлению эти файлы/сайты могут быть пропущены.</span><span class="sxs-lookup"><span data-stu-id="decdc-120">The file and/or site might be stale and if so remediation of those files/sites might be skipped.</span></span> <span data-ttu-id="decdc-121">Чтобы помочь вам с Общие сведения об отчете потребностей бизнеса содержит Администраторы семейства сайтов и владельцев сайтов, предоставляя необходимые сведения для контактов.</span><span class="sxs-lookup"><span data-stu-id="decdc-121">To help you with understanding the business need the report contains the site collection admins and site owners, providing you the needed information to contact them.</span></span>

## <a name="step-3-remediate-the-files"></a><span data-ttu-id="decdc-122">Шаг 3: Устранение файлы</span><span class="sxs-lookup"><span data-stu-id="decdc-122">Step 3: Remediate the files</span></span>
<span data-ttu-id="decdc-123">Если файлы по-прежнему важны и необходимо иметь возможность выполнять файлы после клиента была перемещена в strict параметр по-прежнему, необходимо исправить файлы, как описано в следующей главы.</span><span class="sxs-lookup"><span data-stu-id="decdc-123">If the files are still important and you’ll want to continue to be able to execute the files once the tenant has moved to the strict setting, then you’ll need to remediate the files as explained in the next chapters.</span></span> 

# <a name="remediation-process-for-htmlhtm-files"></a><span data-ttu-id="decdc-124">Процесс обновления для html/htm-файлы</span><span class="sxs-lookup"><span data-stu-id="decdc-124">Remediation process for html/htm files</span></span>
<span data-ttu-id="decdc-125">Основная причина клиентам использовать именно Нестрогое режима является, поскольку они хотят иметь возможность использовать HTML-файлы из внутри библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="decdc-125">The main reason for customers sticking with permissive mode is because they want to be able to use html files from inside a document library.</span></span> <span data-ttu-id="decdc-126">Как уже было сказано, прежде чем после перемещения в strict эти файлы будут просто загрузить и автоматически открывать больше.</span><span class="sxs-lookup"><span data-stu-id="decdc-126">As mentioned before once moved to strict these files will simply download and not automatically open anymore.</span></span>
<span data-ttu-id="decdc-127">Для этих файлов html/html исправлению простой: Если пользователь/приложение с разрешениями администратора семейства сайтов или владельца веб-сайта имени html/htm-файлы на ASPX-файлы, затем снова открыть эти файлы.</span><span class="sxs-lookup"><span data-stu-id="decdc-127">For these html/html files the remediation is simple: if a user/app with site owner or site collection admin permissions renames the html/htm files to ASPX files then these files do open again.</span></span> <span data-ttu-id="decdc-128">Ниже отображает [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) как это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="decdc-128">Below [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) shows a how this can be done.</span></span> <span data-ttu-id="decdc-129">Предположим, что HTML-файл с следующий URL-адрес: https://contoso.sharepoint.com/sites/permissive/html/newfile.html.</span><span class="sxs-lookup"><span data-stu-id="decdc-129">Assume you’ve a html file with following url: https://contoso.sharepoint.com/sites/permissive/html/newfile.html.</span></span> 

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Rename-PnPFile -ServerRelativeUrl /sites/permissive/html/newfile.html -TargetFileName newfile.aspx -OverwriteIfAlreadyExists
```

<span data-ttu-id="decdc-130">Более поздней версии для будут отображаться в этой статье скрипта, который можно выполнить полную «исправления» для всего семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="decdc-130">Later on this article a script will be shown that can perform a full "remediation" of a complete site collection.</span></span>

## <a name="who-can-perform-this-rename"></a><span data-ttu-id="decdc-131">Кто может выполнять переименуйте?</span><span class="sxs-lookup"><span data-stu-id="decdc-131">Who can perform this rename?</span></span>
<span data-ttu-id="decdc-132">Переименование должен выполнить пользователи, имеющие разрешение AddAndCustomizePages (ACP), который по умолчанию предоставляется владельцы сайтов или администраторы семейств сайтов.</span><span class="sxs-lookup"><span data-stu-id="decdc-132">The rename must be performed by users having the AddAndCustomizePages (ACP) permission, which by default is granted to site collection administrators or site owners.</span></span> <span data-ttu-id="decdc-133">Если rename выполняется с пользователя с помощью измените уровень разрешений (так участники сайта) затем осуществляется rename, однако результирующую ASPX-файл не помеченных для выполнения и таким образом будет загружена и не выполнена.</span><span class="sxs-lookup"><span data-stu-id="decdc-133">If the rename is done by a user with Edit the permission level (so site members) then the rename is done, but the resulting .aspx file is not marked for execution and as such will be downloaded and not executed.</span></span> 

<span data-ttu-id="decdc-134">Если вы собираетесь выполнить массовое переименование скорее всего, будет использоваться субъект приложения вместо учетной записи пользователя и то же применяется: участника приложения должны быть разрешения ACP (например уровнем разрешений полный доступ) этой функции необходимо выполнение.</span><span class="sxs-lookup"><span data-stu-id="decdc-134">When you want to do a bulk rename you most likely will use an app principal instead of a user account and there the same applies: the app principal needs the ACP permission (e.g. Full Control permission level) to make this work.</span></span>

## <a name="what-about-embedded-links-to-other-htmlhtm-files"></a><span data-ttu-id="decdc-135">Как насчет внедренные ссылки на другие файлы html/htm?</span><span class="sxs-lookup"><span data-stu-id="decdc-135">What about embedded links to other html/htm files?</span></span>
<span data-ttu-id="decdc-136">Мои ссылки файлы html/htm для других html/htm-файлы в той же папке или во вложенной папке... будет эти ссылки не работают, если файлы переименовываются aspx?</span><span class="sxs-lookup"><span data-stu-id="decdc-136">My html/htm files link to other html/htm files in the same folder or in a subfolder…will these links break if the files are renamed to aspx?</span></span> <span data-ttu-id="decdc-137">Если базовый переименовать выполняется с помощью вызов MoveTo API, а затем большая часть относительные ссылки в файле html автоматически исправленные быть ссылки на файлы aspx по сути переименование структура вложенных html/htm-файлы, которые связь друг с другом можно сделать, только Переименование файлов, все ссылки внутри документы будут обрабатываться rename.</span><span class="sxs-lookup"><span data-stu-id="decdc-137">If the underlying rename is done using the MoveTo API call then most of the relative links inside the html file are automatically fixed to be links to aspx files…essentially renaming a structure of nested html/htm files which link to each other can be done by only renaming the actual files, all the links inside the documents will be handled by the rename.</span></span>

> [!NOTE]
> <span data-ttu-id="decdc-138">Автоматическое переименование не работает, если HTML-документ ссылок, указывающих файлы в другом семействе сайтов или когда ссылки динамически создаются с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="decdc-138">The automatic renaming will not work when the html document has links pointing to files in another site collection or when the links are dynamically generated using JavaScript.</span></span> <span data-ttu-id="decdc-139">В таких случаях вручную действия необходимы для исправления ссылок.</span><span class="sxs-lookup"><span data-stu-id="decdc-139">In those cases, manual actions are required to fixup the links.</span></span>

## <a name="what-about-htmlhtml-files-referenced-in-a-content-editor-web-part"></a><span data-ttu-id="decdc-140">Как насчет html/HTML-файлы по ссылке в веб-части редактора контента?</span><span class="sxs-lookup"><span data-stu-id="decdc-140">What about html/html files referenced in a content editor web part?</span></span>
<span data-ttu-id="decdc-141">Общий шаблон при работе с веб-части редактора контента ссылается на файл html/htm.</span><span class="sxs-lookup"><span data-stu-id="decdc-141">A common pattern when working with the content editor web part is referencing a html/htm file.</span></span> <span data-ttu-id="decdc-142">При переименовании файлов html/htm, на который указывает ссылка ASPX-файл, а затем SharePoint будет автоматически также обновите ссылку в веб-части редактора контента, что по состоянию на этот момент означает, что веб-часть редактора контента будут загружать ASPX-файл вместо html/htm-файл.</span><span class="sxs-lookup"><span data-stu-id="decdc-142">When the referenced html/htm file is renamed to a .aspx file then SharePoint will automatically also update the reference in the content editor web part, meaning as of that moment the content editor web part will load the .aspx file instead of the html/htm file.</span></span> <span data-ttu-id="decdc-143">Чтобы переименовать файлы, используемые на веб-части редактора контента можно совместно с другими файлы html/htm.</span><span class="sxs-lookup"><span data-stu-id="decdc-143">So files used by the content editor web part can be renamed together with all the other html/htm files.</span></span>

## <a name="what-about-sites-having-the-noscript-feature-enabled"></a><span data-ttu-id="decdc-144">Какие сведения о сайтах с включенным средством «noscript»</span><span class="sxs-lookup"><span data-stu-id="decdc-144">What about sites having the “noscript” feature enabled</span></span>
<span data-ttu-id="decdc-145">Все сайты «Современный» (современных группового сайта, сайт связи) имеют функцию «noscript» включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="decdc-145">All “modern” sites (modern team site, communication site) have the “noscript” feature turned on by default.</span></span> <span data-ttu-id="decdc-146">Таким образом, что никто не имеет разрешение AddAndCustomizePages (ACP), чтобы никто можно выполнить успешное переименовать из html/htm для aspx.</span><span class="sxs-lookup"><span data-stu-id="decdc-146">The result of this is that no one will have the AddAndCustomizePages (ACP) permission, so no one can perform a successful rename from html/htm to aspx.</span></span> <span data-ttu-id="decdc-147">Как правило html/htm-файлы live в веб-сайтов (перенесенных) классический групп этой проблемы не существует.</span><span class="sxs-lookup"><span data-stu-id="decdc-147">Typically, the html/htm files live in (migrated) classic team sites so this problem is not there.</span></span> <span data-ttu-id="decdc-148">В случае, используемого на сайте «noscript» вам потребуются для первого отключить функцию «noscript», выполнить операции и затем снова включить «noscript».</span><span class="sxs-lookup"><span data-stu-id="decdc-148">In the case you are working in a “noscript” site you’ll need to first turn off the “noscript” feature, perform the renames and then turn on “noscript” again.</span></span> <span data-ttu-id="decdc-149">В результате html/htm-файлы могут быть выполнены еще раз, но Обратите внимание на то, что каждого изменения на эти файлы будут помечены не исполняемый файл еще раз.</span><span class="sxs-lookup"><span data-stu-id="decdc-149">As a result the html/htm files can be executed again, but do note that each change on these files will mark them as non-executable again.</span></span> <span data-ttu-id="decdc-150">Отключение «noscript» еще раз и обновление файла будет обрабатывать это.</span><span class="sxs-lookup"><span data-stu-id="decdc-150">Turning off “noscript” again and updating the file will handle this.</span></span>

## <a name="in-the-modern-document-library-experience-the-aspx-file-initially-do-not-seem-to-open"></a><span data-ttu-id="decdc-151">В работу библиотеки документов современных файла aspx изначально не вступают в откройте?</span><span class="sxs-lookup"><span data-stu-id="decdc-151">In the modern document library experience the aspx file initially do not seem to open?</span></span>
<span data-ttu-id="decdc-152">Работу библиотеки документов современных «предполагается» определенного типа файлов после добавления файла и при доступе к файлу в первый раз вы увидите, что aspx-файлы открываются неправильно.</span><span class="sxs-lookup"><span data-stu-id="decdc-152">The modern document library experience “assumes” a certain file type when the file was added and when accessing the file for the first time you’ll see that aspx files are opened wrongly.</span></span> <span data-ttu-id="decdc-153">Тем не менее второй попытки выполнения файла.</span><span class="sxs-lookup"><span data-stu-id="decdc-153">Second attempt however does execute the file.</span></span> <span data-ttu-id="decdc-154">Избегайте введите этой проблемы рекомендуется выполнить программными средствами раскрывающемся каждого переименованный файл один раз, что дает возможность правильно установить файл SharePoint.</span><span class="sxs-lookup"><span data-stu-id="decdc-154">The avoid this problem it’s recommended to programmatically pull down each renamed file once, which gives SharePoint the opportunity to correctly set the file type.</span></span> <span data-ttu-id="decdc-155">Ниже отображает [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) как это можно сделать:</span><span class="sxs-lookup"><span data-stu-id="decdc-155">Below [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) shows a how this can be done:</span></span>

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Get-PnPFile -Url /sites/permissive/html/newfile.aspx -Path c:\temp -Filename newfile.aspx -AsFile
```

> [!NOTE]
> <span data-ttu-id="decdc-156">Это действие «загрузить» включен в скрипт, который может выполнять полный «исправления» для всего семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="decdc-156">This "download" step is included in the script that can perform a full "remediation" of a complete site collection.</span></span>

# <a name="remediation-of-other-file-types"></a><span data-ttu-id="decdc-157">Исправление других типов файлов</span><span class="sxs-lookup"><span data-stu-id="decdc-157">Remediation of other file types</span></span>
<span data-ttu-id="decdc-158">HTML/htm-файлы должны использовать режим разрешений, но что о других типов файлов основные причины для клиентов?</span><span class="sxs-lookup"><span data-stu-id="decdc-158">Html/htm files are the major reason for customers to use the permissive mode but what about other file types?</span></span> <span data-ttu-id="decdc-159">Для многих распространенных форматов файлов SharePoint Online предоставляют возможность просмотра как описано в этом [блоге](https://techcommunity.microsoft.com/t5/OneDrive-for-Business/Announcing-New-File-Viewers-Available-for-OneDrive-For-Business/td-p/60040).</span><span class="sxs-lookup"><span data-stu-id="decdc-159">For the many common file formats SharePoint Online does offer a preview capability as explained in this [blog](https://techcommunity.microsoft.com/t5/OneDrive-for-Business/Announcing-New-File-Viewers-Available-for-OneDrive-For-Business/td-p/60040).</span></span> <span data-ttu-id="decdc-160">SharePoint Online можно выполнить предварительный просмотр следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="decdc-160">SharePoint Online can preview the following formats:</span></span>

## <a name="documents"></a><span data-ttu-id="decdc-161">Документы</span><span class="sxs-lookup"><span data-stu-id="decdc-161">Documents</span></span>
<span data-ttu-id="decdc-162">CSV, doc, docm, docx, dotx, eml, сообщение, odp, программ ods odt, pdf, pot, potm, potx, pps, ppsx, ppt, pptm, pptx, rtf, vsd, vsdx, xls, xlsb, xlsm, xlsx</span><span class="sxs-lookup"><span data-stu-id="decdc-162">csv, doc, docm, docx, dotx, eml, msg, odp, ods, odt, pdf, pot, potm, potx, pps, ppsx, ppt, pptm, pptx, rtf, vsd, vsdx, xls, xlsb, xlsm, xlsx</span></span>

## <a name="images"></a><span data-ttu-id="decdc-163">изображения;</span><span class="sxs-lookup"><span data-stu-id="decdc-163">Images</span></span>
<span data-ttu-id="decdc-164">AI, arw, bmp, cr2, eps, erf, gif, ico, значок, jpeg, jpg, mrw, nef, orf, pict, png, psd, временных файлов Интернета, tiff</span><span class="sxs-lookup"><span data-stu-id="decdc-164">ai, arw, bmp, cr2, eps, erf, gif, ico, icon, jpeg, jpg, mrw, nef, orf, pict, png, psd, tif, tiff</span></span>

## <a name="video"></a><span data-ttu-id="decdc-165">Видео</span><span class="sxs-lookup"><span data-stu-id="decdc-165">Video</span></span>
<span data-ttu-id="decdc-166">3GP, m4v, mov, MP4 (en), wmv</span><span class="sxs-lookup"><span data-stu-id="decdc-166">3gp, m4v, mov, mp4, wmv</span></span>

## <a name="3d"></a><span data-ttu-id="decdc-167">3D</span><span class="sxs-lookup"><span data-stu-id="decdc-167">3D</span></span>
<span data-ttu-id="decdc-168">3mf, fbx, obj, лист, stl</span><span class="sxs-lookup"><span data-stu-id="decdc-168">3mf, fbx, obj, ply, stl</span></span>

## <a name="medical"></a><span data-ttu-id="decdc-169">Медицинского обслуживания</span><span class="sxs-lookup"><span data-stu-id="decdc-169">Medical</span></span>
<span data-ttu-id="decdc-170">DCM dcm30, dic, dicm, dicom</span><span class="sxs-lookup"><span data-stu-id="decdc-170">dcm, dcm30, dic, dicm, dicom</span></span>

## <a name="text-and-code"></a><span data-ttu-id="decdc-171">Текст и кода</span><span class="sxs-lookup"><span data-stu-id="decdc-171">Text and code</span></span>
<span data-ttu-id="decdc-172">abap, ada, adp, ahk как, as3, asc, ascx, asm, asp, awk, bash, bash_login, bash_logout, bash_profile, bashrc, bat, списка литературы, bsh, построения, построитель, c, c ++ capfile, cc, cfc, куб, cfml, cl, clj, cls, cmake, cmd, кофе, cpp, cpt, cpy, cs, cshtml, cson, csproj, css, CTP-версия , cxx, d, ddl, di, dif, копирования, disco, dml, dtd, dtml, el, emakefile, erb, erl, f, f90, f95, федерации Active Directory, ФСС, fsscript, fsx, gemfile, gemspec, gitconfig, последовательно выберите, хорошую, gvy, h, h ++ (en), haml, рули, hbs, hcp, hh, hpp, hrl, hs, htc, hxx, idl, iim, inc, inf, ini, inl, ipp , irbrc, jade, jav, java, js, jsp, jsx, l меньше lhs, lisp, журнала, lst, ltx, lua, m, сделать, markdn, наценки, md, mdown, mkdn, ml, mli, mll, mly, мм, лиственный, nfo, opml, osascript выходной параметр p, pas, исправление, php, php2, php3, php4, php5, phtml, pl, plist, pm, модуль, pp , профиля, свойства, ps1, pt, копировать, pyw, r, rake, rb, rbx, rc, re readme, reg, rest, resw, resx, rhtml, rjs, rprofile, rpy, RSS-канал, rst, rxml, s, sass, scala, диспетчер управления службами, sconscript, sconstruct, скрипт, scss, sgml, показывать, shtml, sml, sql, Стилисти, tcl, tex, текст, textile, доменов верхнего уровня, tli, шаблон, библиотека параллельных задач, txt, vb, vi, vim, WSDL-файлу, xhtml, xml, xoml, xsd, xsl, xslt, yaml, yaws, yml, zip, zsh</span><span class="sxs-lookup"><span data-stu-id="decdc-172">abap, ada, adp, ahk, as, as3, asc, ascx, asm, asp, awk, bash, bash_login, bash_logout, bash_profile, bashrc, bat, bib, bsh, build, builder, c, c++, capfile, cc, cfc, cfm, cfml, cl, clj, cls, cmake, cmd, coffee, cpp, cpt, cpy, cs, cshtml, cson, csproj, css, ctp, cxx, d, ddl, di, dif, diff, disco, dml, dtd, dtml, el, emakefile, erb, erl, f, f90, f95, fs, fsi, fsscript, fsx, gemfile, gemspec, gitconfig, go, groovy, gvy, h, h++, haml, handlebars, hbs, hcp, hh, hpp, hrl, hs, htc, hxx, idl, iim, inc, inf, ini, inl, ipp, irbrc, jade, jav, java, js, jsp, jsx, l, less, lhs, lisp, log, lst, ltx, lua, m, make, markdn, markdown, md, mdown, mkdn, ml, mli, mll, mly, mm, mud, nfo, opml, osascript, out, p, pas, patch, php, php2, php3, php4, php5, phtml, pl, plist, pm, pod, pp, profile, properties, ps1, pt, py, pyw, r, rake, rb, rbx, rc, re, readme, reg, rest, resw, resx, rhtml, rjs, rprofile, rpy, rss, rst, rxml, s, sass, scala, scm, sconscript, sconstruct, script, scss, sgml, sh, shtml, sml, sql, sty, tcl, tex, text, textile, tld, tli, tmpl, tpl, txt, vb, vi, vim, wsdl, xhtml, xml, xoml, xsd, xsl, xslt, yaml, yaws, yml, zip, zsh</span></span>

# <a name="sample-script-that-can-remediate-a-complete-site-collection"></a><span data-ttu-id="decdc-173">Пример сценария, который можно Устранение всего семейства сайтов</span><span class="sxs-lookup"><span data-stu-id="decdc-173">Sample script that can remediate a complete site collection</span></span>
<span data-ttu-id="decdc-174">Этот сценарий можно использовать в качестве отправной основы коррекции уровня семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="decdc-174">This script can be used as a starting basis for a site collection scoped remediation.</span></span> <span data-ttu-id="decdc-175">Скрипт будет выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="decdc-175">The script will do the following:</span></span>
- <span data-ttu-id="decdc-176">Установка PnP PowerShell, если еще не установлены</span><span class="sxs-lookup"><span data-stu-id="decdc-176">Install PnP-PowerShell if not yet installed</span></span>
- <span data-ttu-id="decdc-177">Поиск всех html/htm-файлы в коллекции веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="decdc-177">Use search to find all the html/htm files in the site collection</span></span>
- <span data-ttu-id="decdc-178">Переименуйте эти файлы в .aspx</span><span class="sxs-lookup"><span data-stu-id="decdc-178">Rename those files to .aspx</span></span>
- <span data-ttu-id="decdc-179">Загрузить переименованный файл, чтобы включить его для работы на первый доступа в пользовательском интерфейсе современных документов библиотеки</span><span class="sxs-lookup"><span data-stu-id="decdc-179">Download the renamed file to enable it to work on first access in the modern document library user interface</span></span>


```PowerShell
# This script does rename .htm and .html files to .aspx files. Doing so enables these files to be "executed" in SharePoint Online 
# which has it's file handling configured to be strict. See https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-permissivesetting 
# for more details

function PermissiveRemediateASiteCollection
{
    param([string] $siteCollectionUrl, [string] $winCredentialsManagerLabel)
    
    $siteCollectionUrl = $siteCollectionUrl.TrimEnd("/");

    # Gets or Sets the tenant admin credentials.
    $credentials = $null

    if(![String]::IsNullOrEmpty($winCredentialsManagerLabel) -and (Get-PnPStoredCredential -Name $winCredentialsManagerLabel) -ne $null)
    {
        $credentials = $winCredentialsManagerLabel
    }
    else
    {
        # Prompts for credentials, if not found in the Windows Credential Manager.
        $email = Read-Host -Prompt "Please enter admin email"
        $pass = Read-host -AsSecureString "Please enter admin password"
        $credentials = New-Object –TypeName "System.Management.Automation.PSCredential" –ArgumentList $email, $pass
    }

    if($credentials -eq $null) 
    {
        Write-Host "Error: No credentials supplied." -ForegroundColor Red
        exit 1
    }

    Connect-PnPOnline -Url $siteCollectionUrl -Credentials $credentials -Verbose

    Write-Host "Using search to obtain a list of files to remediate..."
    Try
    {
        $searchQuery = "((fileextension=htm OR fileextension=html) AND contentclass=STS_ListItem_DocumentLibrary AND Path:$siteCollectionUrl/*)"
        $htmlFiles = Submit-PnPSearchQuery -Query $searchQuery -TrimDuplicates:$false -All
    }
    Catch [Exception]
    {
       $ErrorMessage = $_.Exception.Message
       Write-Host "Error: Search query to find the files to remediate failed...exiting the script" -ForegroundColor Red 
       Write-Host "Error: $ErrorMessage" -ForegroundColor Red 
       exit 1
    }

    # if no files were found then bail out
    if ($htmlFiles.RowCount -eq 0)
    {
        Write-Host "No files found to remediate...exiting the script" -ForegroundColor Green
        exit 0
    }
    else
    {
        Write-Host "Found" $htmlFiles.RowCount "files to remediate" -ForegroundColor Green
    }

    # Create temp folder if not yet existing
    $path = "$env:TEMP\permissivefix"
    If(!(test-path $path))
    {
          New-Item -ItemType Directory -Force -Path $path
    }

    # iterate over the found files and rename them
    foreach($htmlFile in $htmlFiles.ResultRows)
    {
        Try
        {
            $web = $htmlFile.SPWebUrl
            Write-Host "Connected to $web..."
            Connect-PnPOnline -Url $web -Credentials $credentials

            $fileToRename = $htmlFile.OriginalPath
            Write-Host "Renaming $fileToRename..."

            # Get the server relative path
            $serverRelativePath = $fileToRename.Replace("https://", "")
            $serverRelativePath = $serverRelativePath.Substring($serverRelativePath.IndexOf("/"))
            #Write-Host $serverRelativePath

            # Get new file name and server relative path
            $newFileName = $serverRelativePath.Substring($serverRelativePath.LastIndexOf("/") + 1).ToLower()
            $serverRelativePathNew = $serverRelativePath
            if ($newFileName.EndsWith(".html"))
            {
                $newFileName = $newFileName.Replace(".html", ".aspx")
                $serverRelativePathNew = $serverRelativePathNew.Replace(".html", ".aspx")
            } 
            elseif($newFileName.EndsWith(".htm"))
            {
                $newFileName = $newFileName.Replace(".htm", ".aspx")
                $serverRelativePathNew = $serverRelativePathNew.Replace(".html", ".aspx")
            }
        
            # Perform the file rename
            Rename-PnPFile -ServerRelativeUrl $serverRelativePath -TargetFileName $newFileName -OverwriteIfAlreadyExists -Force
        
            # Download the file once to ensure it works correctly in modern UI
            Get-PnPFile -Url $serverRelativePathNew -Path $path -Filename $newFileName -AsFile -Force
        }
        Catch [Exception]
        {
           $ErrorMessage = $_.Exception.Message
           Write-Host "Error: Rename of file $serverRelativePath failed" -ForegroundColor Red 
           Write-Host "Error: $ErrorMessage" -ForegroundColor Red 
        }
    }

    # Cleanup the temp folder
    Write-Host "Cleaning up the temp folder $path"
    Remove-Item $path -Recurse -ErrorAction Ignore

    Write-Host "Remediation done for site collection $siteCollectionUrl" -BackgroundColor DarkGreen -ForegroundColor White
}

#######################################################
# MAIN section                                        #
#######################################################

# Url of the site collection to remediate
$siteCollectionUrlToRemediate = "https://contoso.sharepoint.com/sites/testsite"
# If you use credential manager then specify the used credential manager entry, if left blank you'll be asked for a user/pwd
$credentialManagerCredentialToUse = "credmandreference"

# Ensure PnP PowerShell is loaded
if (-not (Get-Module -ListAvailable -Name SharePointPnPPowerShellOnline)) 
{
    Install-Module SharePointPnPPowerShellOnline
}

Import-Module SharePointPnPPowerShellOnline

# Remediate the given site collection
PermissiveRemediateASiteCollection $siteCollectionUrlToRemediate $credentialManagerCredentialToUse

```

<span data-ttu-id="decdc-180">Пример выходных данных выполнения скрипта удачном выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="decdc-180">The sample output of succesful script run looks like this:</span></span>

```Txt
WARNING: The names of some imported commands from the module 'SharePointPnPPowerShellOnline' include unapproved verbs that might make them less discoverable. To find the commands with unapproved ver
bs, run the Import-Module command again with the Verbose parameter. For a list of approved verbs, type Get-Verb.
VERBOSE: PnP PowerShell Cmdlets (2.22.1801.0): Connected to https://contoso.sharepoint.com/sites/testsite
Using search to obtain a list of files to remediate...
Found 15 files to remediate


    Directory: C:\Users\demouser\AppData\Local\Temp


Mode                LastWriteTime         Length Name                                                                                                                                                
----                -------------         ------ ----                                                                                                                                                
d-----        7/02/2018     19:48                permissivefix                                                                                                                                       
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/About.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/brol.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/imagetarget.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/sample_html_afternoscript9.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/bla.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/sample_html.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/home2.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/howtouse.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/home.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/team_home.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/imagesource.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/bla2.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/wikipage.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/newfile_html.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/Home3.html...
Cleaning up the temp folder C:\Users\demouser\AppData\Local\Temp\permissivefix
Remediation done for site collection https://contoso.sharepoint.com/sites/testsite

```

