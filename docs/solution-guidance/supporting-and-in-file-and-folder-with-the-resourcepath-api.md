---
title: "Поддержка % и # в файлах и папках с помощью API ResourcePath"
ms.date: 11/03/2017
ms.openlocfilehash: 4667020c2387650d8ad84dc000afa785f7b07016
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="supporting--and--in-file-and-folder-with-the-resourcepath-api"></a><span data-ttu-id="d572d-102">Поддержка % и # в файлах и папках с помощью API ResourcePath</span><span class="sxs-lookup"><span data-stu-id="d572d-102">Supporting % and # in file and folder with the ResourcePath API</span></span>

<span data-ttu-id="d572d-103">Поддержка % и # в файлах и папках развертывается в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d572d-103">Support for % and # in file and folder is being deployed within SharePoint Online.</span></span>  <span data-ttu-id="d572d-104">К сожалению из-за существующих структур API и вызов шаблонов, работа с именами могут иногда неоднозначность.</span><span class="sxs-lookup"><span data-stu-id="d572d-104">Unfortunately, due to existing API structures and calling patterns, working with these file names can sometimes become ambiguous.</span></span>  <span data-ttu-id="d572d-105">Можно найти [Дополнительные фон за это в нашем блоге разработчика](https://dev.office.com/blogs/upcoming-changes-to-sharepoint-and-onedrive-for-business-apis-to-support-and-in-file-names).</span><span class="sxs-lookup"><span data-stu-id="d572d-105">You can find [more background behind this on our developer blog](https://dev.office.com/blogs/upcoming-changes-to-sharepoint-and-onedrive-for-business-apis-to-support-and-in-file-names).</span></span>  <span data-ttu-id="d572d-106">Таким образом были добавлены новые интерфейсы API SharePoint Online клиента объектной модели (CSOM) рабочей области для обеспечения поддержки # до % символов.</span><span class="sxs-lookup"><span data-stu-id="d572d-106">In summary, new APIs have been added to the SharePoint Online client object model (CSOM) surface to provide support for # and % characters.</span></span>

## <a name="resourcepath"></a><span data-ttu-id="d572d-107">ResourcePath</span><span class="sxs-lookup"><span data-stu-id="d572d-107">ResourcePath</span></span>
 
<span data-ttu-id="d572d-108">Как краткий обзор Обратите внимание на то, существующий дескриптор на основе строки API-интерфейсов SharePoint (например, SPFileCollection.GetByUrl) оба кодируются и автоматически декодировать URL-адресов, если предполагается, что подразумевает % и # символов пути зашифрованную URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d572d-108">As a recap, note that existing String-based SharePoint APIs (such as SPFileCollection.GetByUrl) handle both encoded and decoded URLs by automatically assuming that % and # characters in a path imply that the URL has been encoded.</span></span>  <span data-ttu-id="d572d-109">С помощью поддержки % и # в файлы и папки, в этом автоматическая обработка теперь инспектором так как он может привести к игнорировать или mishandle имена файлов с помощью % и # в них нижестоящие кода.</span><span class="sxs-lookup"><span data-stu-id="d572d-109">With new support % and # in file and folder, this automatic treatment is now problematic because it may cause downstream code to ignore or mishandle filenames with % and # in them.</span></span>
 
<span data-ttu-id="d572d-110">Новый класс-- `Microsoft.SharePoint.Client.ResourcePath` --был добавлен к интерфейсам API.</span><span class="sxs-lookup"><span data-stu-id="d572d-110">A new class -- `Microsoft.SharePoint.Client.ResourcePath` -- has been added to APIs.</span></span>  <span data-ttu-id="d572d-111">Класс ResourcePath является основой для поддержки этих новых символов.</span><span class="sxs-lookup"><span data-stu-id="d572d-111">The ResourcePath class is fundamental to the support of these new characters.</span></span>  <span data-ttu-id="d572d-112">Она позволяет новые, однозначное устранения элемент в SharePoint и OneDrive для бизнеса, поскольку предполагается, что и работает только с декодированное URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d572d-112">It provides a new, unambiguous way to address an item within SharePoint and OneDrive for Business, because it assumes and only works with decoded URLs.</span></span> <span data-ttu-id="d572d-113">Он заменяет на основе строки пути для представления полное (абсолютный) или partial (относительный) URL-адрес семейства веб-сайтов, сайта, файла, папки или других артефактов и OneDrive для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="d572d-113">It replaces String-based paths to represent a full (absolute) or partial (relative) URL for a site collection, site, file, folder or other artifact and OneDrive for Business.</span></span> <span data-ttu-id="d572d-114">Для правильной поддержки % и # внутри URL-адреса, необходимо будет использовать API на основе ResourcePath, а также декодировать URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d572d-114">To properly support % and # within URLs, you will need to use the ResourcePath-based APIs along with Decoded URLs.</span></span>
 
<span data-ttu-id="d572d-115">ResourcePath простую структуру, вызвав статической функции `ResourcePath.FromDecodedUrl(string)`.</span><span class="sxs-lookup"><span data-stu-id="d572d-115">ResourcePath can be simply constructed by calling a static function `ResourcePath.FromDecodedUrl(string)`.</span></span> <span data-ttu-id="d572d-116">Входное значение, переданное может осуществляться из объекта ResourcePath вызов свойства DecodedUrl.</span><span class="sxs-lookup"><span data-stu-id="d572d-116">The passed in input value can be accessed from the ResourcePath object by calling the property DecodedUrl.</span></span> 
 
<span data-ttu-id="d572d-117">Для существующих вызовов, в основе строки URL-адреса, необходимо определить ли путь к коду, приводя к на основе строки звонки URL-адрес, предоставленных с URL-адреса конечной и ли тех код пути, также может ссылки привязки (то есть: дополнения #bookmark на в верхней части файла URL-адреса.)</span><span class="sxs-lookup"><span data-stu-id="d572d-117">For existing calls that take in a String-based URL, you will need to determine whether the code path leading to String-based URL calls were provided with encoded or decoded URLs, and whether those code paths also permitted Anchor links (that is: #bookmark additions on top of the file URL.)</span></span>

> <span data-ttu-id="d572d-118">Примечание: Не просто найти и заменить существующий режимы работы на основе строку URL-адрес API-интерфейсов с `ResourcePath.FromDecodedUrl`.</span><span class="sxs-lookup"><span data-stu-id="d572d-118">Note: Do not simply find and replace existing usages of String-based URL APIs with `ResourcePath.FromDecodedUrl`.</span></span>  <span data-ttu-id="d572d-119">Необходимо правильно определить URL-адрес и потенциально декодировать URL-адреса, перед использованием сначала `ResourcePath.FromDecodedUrl(string)` API.</span><span class="sxs-lookup"><span data-stu-id="d572d-119">You will need to properly determine URL and potentially decode URLs first before using the `ResourcePath.FromDecodedUrl(string)` API.</span></span>

<span data-ttu-id="d572d-120">В тех случаях, где протоколе, приводя к вызов API SharePoint на основе String используется **Декодировать URL-адреса (например, «FY17 Report.docx»)**, а затем можно просто замените эти вызовы с `ResourcePath.FromDecodedUrl(string)` и эквивалентные методы ResourcePath, перечисленных ниже.</span><span class="sxs-lookup"><span data-stu-id="d572d-120">In cases where a codepath leading to a String-based SharePoint API call used **Decoded URLs (e.g., 'FY17 Report.docx')**, then you can simply replace these calls with `ResourcePath.FromDecodedUrl(string)` and equivalent ResourcePath methods listed below.</span></span>
 
<span data-ttu-id="d572d-121">Обратите внимание, что во многих случаях, где чтение URL-адрес из SharePoint с помощью API-интерфейсов, ResourcePath также позволяет сделать эти шаблоны кода согласованность, поэтому ResourcePath можно использовать вместо URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d572d-121">Note that in many cases where you read the URL from SharePoint via APIs, the ResourcePath is also provided to make these code patterns more consistent, so you can use the ResourcePath instead of URL.</span></span>
 
<span data-ttu-id="d572d-122">Также Обратите внимание, что это изменение распространяется и на основе SharePoint REST вызовов, а также.</span><span class="sxs-lookup"><span data-stu-id="d572d-122">Also note that this change also applies to SharePoint REST-based calls, as well.</span></span>  <span data-ttu-id="d572d-123">Ознакомьтесь со сценариями ниже, чтобы просмотреть примеры эти новые интерфейсы API в REST.</span><span class="sxs-lookup"><span data-stu-id="d572d-123">Please review the scenarios below to see examples of these new APIs in REST.</span></span>

## <a name="new-apis-that-are-based-on-resourcepath-and-supports--and-"></a><span data-ttu-id="d572d-124">Новые интерфейсы API, которые основаны на ResourcePath и поддерживает # и %</span><span class="sxs-lookup"><span data-stu-id="d572d-124">New APIs that are based on ResourcePath and supports # and %</span></span>
 
<span data-ttu-id="d572d-125">Ниже приведены новые интерфейсы API, мы представили заменить существующие интерфейсы API для поддержки # и %.</span><span class="sxs-lookup"><span data-stu-id="d572d-125">Below are the new APIs that we introduced to replace the existing APIs in order to support # and %.</span></span> <span data-ttu-id="d572d-126">Мы в списке старый интерфейс API и новые API рядом друг с другом для вашей сравнения.</span><span class="sxs-lookup"><span data-stu-id="d572d-126">We listed the old API and the new API side by side for your comparison.</span></span> <span data-ttu-id="d572d-127">Основные функциональные возможности этих API не изменяется, однако изменить способ представления расположение элемента.</span><span class="sxs-lookup"><span data-stu-id="d572d-127">The core functionality of these APIs does not change, but how to represent the location of the item is changed.</span></span>
 
<span data-ttu-id="d572d-128">Документация по новые интерфейсы API можно ссылаться на https://msdn.microsoft.com/en-us/library/jj193041.aspx.</span><span class="sxs-lookup"><span data-stu-id="d572d-128">The documentation of new APIs can be referred at https://msdn.microsoft.com/en-us/library/jj193041.aspx.</span></span>  <span data-ttu-id="d572d-129">Перечислены .net CSOM ниже интерфейсы API, но новые методы, также доступны в эквивалентный формы в нашей библиотеки JavaScript CSOM.</span><span class="sxs-lookup"><span data-stu-id="d572d-129">We have listed the .net CSOM APIs below, but the new methods are also available in equivalent form in our JavaScript CSOM libraries.</span></span>
 
<span data-ttu-id="d572d-130">**Сборки Microsoft.SharePoint.Client.dll**</span><span class="sxs-lookup"><span data-stu-id="d572d-130">**Assembly Microsoft.SharePoint.Client.dll**</span></span>

| <span data-ttu-id="d572d-131">Тип</span><span class="sxs-lookup"><span data-stu-id="d572d-131">Type</span></span> | <span data-ttu-id="d572d-132">Старый метод</span><span class="sxs-lookup"><span data-stu-id="d572d-132">Old Method</span></span> | <span data-ttu-id="d572d-133">Новый метод</span><span class="sxs-lookup"><span data-stu-id="d572d-133">New Method</span></span> | 
|----------|-------------|------|
| <span data-ttu-id="d572d-134">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="d572d-134">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="d572d-135">AddItem(Microsoft.SharePoint.SPListItemCreationInformation)</span><span class="sxs-lookup"><span data-stu-id="d572d-135">AddItem(Microsoft.SharePoint.SPListItemCreationInformation)</span></span> | <span data-ttu-id="d572d-136">AddItemUsingPath (SPListItemCreationInformationUsingPath параметров)</span><span class="sxs-lookup"><span data-stu-id="d572d-136">AddItemUsingPath(SPListItemCreationInformationUsingPath parameters)</span></span> | 
| <span data-ttu-id="d572d-137">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="d572d-137">Microsoft.SharePoint.SPFile</span></span> | <span data-ttu-id="d572d-138">MoveTo (System.String, Microsoft.SharePoint.SPMoveOperations)</span><span class="sxs-lookup"><span data-stu-id="d572d-138">MoveTo(System.String, Microsoft.SharePoint.SPMoveOperations)</span></span> | <span data-ttu-id="d572d-139">MoveToUsingPath (SPResourcePath newPath, SPMoveOperations moveOperations)</span><span class="sxs-lookup"><span data-stu-id="d572d-139">MoveToUsingPath(SPResourcePath newPath, SPMoveOperations moveOperations)</span></span> | 
| <span data-ttu-id="d572d-140">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="d572d-140">Microsoft.SharePoint.SPFile</span></span> | <span data-ttu-id="d572d-141">CopyTo (System.String, Boolean)</span><span class="sxs-lookup"><span data-stu-id="d572d-141">CopyTo(System.String, Boolean)</span></span> | <span data-ttu-id="d572d-142">CopyToUsingPath (SPResourcePath newPath, перезаписать bool)</span><span class="sxs-lookup"><span data-stu-id="d572d-142">CopyToUsingPath(SPResourcePath newPath, bool overwrite)</span></span> | 
| <span data-ttu-id="d572d-143">Microsoft.SharePoint.SPFileCollection</span><span class="sxs-lookup"><span data-stu-id="d572d-143">Microsoft.SharePoint.SPFileCollection</span></span> | <span data-ttu-id="d572d-144">GetByUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-144">GetByUrl(System.String)</span></span> | <span data-ttu-id="d572d-145">GetByPath(SPResourcePath)</span><span class="sxs-lookup"><span data-stu-id="d572d-145">GetByPath(SPResourcePath)</span></span> | 
| <span data-ttu-id="d572d-146">Microsoft.SharePoint.SPFileCollection</span><span class="sxs-lookup"><span data-stu-id="d572d-146">Microsoft.SharePoint.SPFileCollection</span></span> | <span data-ttu-id="d572d-147">Добавление (System.String, Microsoft.SharePoint.SPTemplateFileType)</span><span class="sxs-lookup"><span data-stu-id="d572d-147">Add(System.String, Microsoft.SharePoint.SPTemplateFileType)</span></span> | <span data-ttu-id="d572d-148">AddUsingPath (SPResourcePath, SPFileCollectionAddWithTemplateParameters)</span><span class="sxs-lookup"><span data-stu-id="d572d-148">AddUsingPath(SPResourcePath, SPFileCollectionAddWithTemplateParameters)</span></span> | 
| <span data-ttu-id="d572d-149">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="d572d-149">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="d572d-150">MoveTo(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-150">MoveTo(System.String)</span></span> | <span data-ttu-id="d572d-151">MoveToUsingPath (SPResourcePath newPath)</span><span class="sxs-lookup"><span data-stu-id="d572d-151">MoveToUsingPath(SPResourcePath newPath)</span></span> | 
| <span data-ttu-id="d572d-152">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="d572d-152">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="d572d-153">AddSubFolder(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-153">AddSubFolder(System.String)</span></span> | <span data-ttu-id="d572d-154">AddSubFolderUsingPath (SPResourcePath leafPath)</span><span class="sxs-lookup"><span data-stu-id="d572d-154">AddSubFolderUsingPath(SPResourcePath leafPath)</span></span> | 
| <span data-ttu-id="d572d-155">Microsoft.SharePoint.SPFolderCollection</span><span class="sxs-lookup"><span data-stu-id="d572d-155">Microsoft.SharePoint.SPFolderCollection</span></span> | <span data-ttu-id="d572d-156">GetByUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-156">GetByUrl(System.String)</span></span> | <span data-ttu-id="d572d-157">GetByPath (SPResourcePath путь)</span><span class="sxs-lookup"><span data-stu-id="d572d-157">GetByPath(SPResourcePath path)</span></span> | 
| <span data-ttu-id="d572d-158">Microsoft.SharePoint.SPFolderCollection</span><span class="sxs-lookup"><span data-stu-id="d572d-158">Microsoft.SharePoint.SPFolderCollection</span></span> | <span data-ttu-id="d572d-159">Add(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-159">Add(System.String)</span></span> | <span data-ttu-id="d572d-160">AddUsingPath (SPResourcePath пути, параметры SPFolderCreationInformation)</span><span class="sxs-lookup"><span data-stu-id="d572d-160">AddUsingPath(SPResourcePath path, SPFolderCreationInformation parameters)</span></span> | 
|  | <span data-ttu-id="d572d-161">AddWithOverwrite (строка URL-адреса, перезаписать bool)</span><span class="sxs-lookup"><span data-stu-id="d572d-161">AddWithOverwrite(string url, bool overwrite)</span></span> |  | 
| <span data-ttu-id="d572d-162">Microsoft.SharePoint.SPRemoteWeb</span><span class="sxs-lookup"><span data-stu-id="d572d-162">Microsoft.SharePoint.SPRemoteWeb</span></span> | <span data-ttu-id="d572d-163">GetFileByServerRelativeUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-163">GetFileByServerRelativeUrl(System.String)</span></span> | <span data-ttu-id="d572d-164">GetFileByServerRelativePath (SPResourcePath путь)</span><span class="sxs-lookup"><span data-stu-id="d572d-164">GetFileByServerRelativePath(SPResourcePath path)</span></span> | 
| <span data-ttu-id="d572d-165">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="d572d-165">Microsoft.SharePoint.SPWeb</span></span> | <span data-ttu-id="d572d-166">GetList(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-166">GetList(System.String)</span></span> | <span data-ttu-id="d572d-167">GetListUsingPath(SPResourcePath)</span><span class="sxs-lookup"><span data-stu-id="d572d-167">GetListUsingPath(SPResourcePath)</span></span> | 
| <span data-ttu-id="d572d-168">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="d572d-168">Microsoft.SharePoint.SPWeb</span></span> | <span data-ttu-id="d572d-169">GetListItem(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-169">GetListItem(System.String)</span></span> | <span data-ttu-id="d572d-170">GetListItemUsingPath(SPResourcePath)</span><span class="sxs-lookup"><span data-stu-id="d572d-170">GetListItemUsingPath(SPResourcePath)</span></span> | 


<span data-ttu-id="d572d-171">Следующие объекты CSOM получить ResourcePath свойства, которые могут использоваться в выше API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="d572d-171">The following CSOM objects return ResourcePath properties that can be used in above APIs.</span></span> <span data-ttu-id="d572d-172">Несмотря на то, что старый свойство также возвращает декодированное URL-адреса, свойство ResourcePath предоставляется для удобства, простоты и ясности в вызова выше API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="d572d-172">Although the old property also returns decoded URLs, the new ResourcePath property is provided for convenience, simplicity and clarity in calling above APIs.</span></span>  <span data-ttu-id="d572d-173">Одно исключение — это является свойство SPFolder.WelcomePage, которое ранее возвращенный кодированных и некодированных URL-адресов; Теперь однозначно возвращаются через свойство WelcomePagePath.</span><span class="sxs-lookup"><span data-stu-id="d572d-173">The one exception to this is the SPFolder.WelcomePage property, which formerly returned both encoded and unencoded URLs; this is now unambiguously returned via the WelcomePagePath property.</span></span>

| <span data-ttu-id="d572d-174">Тип</span><span class="sxs-lookup"><span data-stu-id="d572d-174">Type</span></span> | <span data-ttu-id="d572d-175">Старый свойство</span><span class="sxs-lookup"><span data-stu-id="d572d-175">Old Property</span></span> | <span data-ttu-id="d572d-176">Новое свойство</span><span class="sxs-lookup"><span data-stu-id="d572d-176">New Property</span></span> | 
|----------|-------------|------|
| <span data-ttu-id="d572d-177">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="d572d-177">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="d572d-178">DefaultViewUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-178">DefaultViewUrl</span></span> | <span data-ttu-id="d572d-179">DefaultViewPath</span><span class="sxs-lookup"><span data-stu-id="d572d-179">DefaultViewPath</span></span> | 
| <span data-ttu-id="d572d-180">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="d572d-180">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="d572d-181">DefaultEditFormUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-181">DefaultEditFormUrl</span></span> | <span data-ttu-id="d572d-182">DefaultEditFormPath</span><span class="sxs-lookup"><span data-stu-id="d572d-182">DefaultEditFormPath</span></span> | 
| <span data-ttu-id="d572d-183">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="d572d-183">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="d572d-184">DefaultNewFormUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-184">DefaultNewFormUrl</span></span> | <span data-ttu-id="d572d-185">DefaultNewFormPath</span><span class="sxs-lookup"><span data-stu-id="d572d-185">DefaultNewFormPath</span></span> | 
| <span data-ttu-id="d572d-186">Microsoft.SharePoint.SPList</span><span class="sxs-lookup"><span data-stu-id="d572d-186">Microsoft.SharePoint.SPList</span></span> | <span data-ttu-id="d572d-187">DefaultDisplayFormUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-187">DefaultDisplayFormUrl</span></span> | <span data-ttu-id="d572d-188">DefaultDisplayFormPath</span><span class="sxs-lookup"><span data-stu-id="d572d-188">DefaultDisplayFormPath</span></span> | 
| <span data-ttu-id="d572d-189">Microsoft.SharePoint.SPAttachment</span><span class="sxs-lookup"><span data-stu-id="d572d-189">Microsoft.SharePoint.SPAttachment</span></span> | <span data-ttu-id="d572d-190">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-190">ServerRelativeUrl</span></span> | <span data-ttu-id="d572d-191">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="d572d-191">ServerRelativePath</span></span> | 
| <span data-ttu-id="d572d-192">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="d572d-192">Microsoft.SharePoint.SPFile</span></span> | <span data-ttu-id="d572d-193">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-193">ServerRelativeUrl</span></span> | <span data-ttu-id="d572d-194">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="d572d-194">ServerRelativePath</span></span> | 
| <span data-ttu-id="d572d-195">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="d572d-195">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="d572d-196">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-196">ServerRelativeUrl</span></span> | <span data-ttu-id="d572d-197">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="d572d-197">ServerRelativePath</span></span> | 
| <span data-ttu-id="d572d-198">Microsoft.SharePoint.SPFolder</span><span class="sxs-lookup"><span data-stu-id="d572d-198">Microsoft.SharePoint.SPFolder</span></span> | <span data-ttu-id="d572d-199">WelcomePage</span><span class="sxs-lookup"><span data-stu-id="d572d-199">WelcomePage</span></span> | <span data-ttu-id="d572d-200">WelcomePagePath / WelcomePageParameters</span><span class="sxs-lookup"><span data-stu-id="d572d-200">WelcomePagePath/ WelcomePageParameters</span></span> | 
| <span data-ttu-id="d572d-201">Microsoft.SharePoint.SPView</span><span class="sxs-lookup"><span data-stu-id="d572d-201">Microsoft.SharePoint.SPView</span></span> | <span data-ttu-id="d572d-202">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-202">ServerRelativeUrl</span></span> | <span data-ttu-id="d572d-203">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="d572d-203">ServerRelativePath</span></span> | 
| <span data-ttu-id="d572d-204">Microsoft.SharePoint.SPDocumentLibraryInformation</span><span class="sxs-lookup"><span data-stu-id="d572d-204">Microsoft.SharePoint.SPDocumentLibraryInformation</span></span> | <span data-ttu-id="d572d-205">ServerRelativeUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-205">ServerRelativeUrl</span></span> | <span data-ttu-id="d572d-206">ServerRelativePath</span><span class="sxs-lookup"><span data-stu-id="d572d-206">ServerRelativePath</span></span> | 


## <a name="existing-apis-that-are-not-ambiguous-about-the-url-formant-and-can-supports--and-"></a><span data-ttu-id="d572d-207">Существующие интерфейсы API, не являются неоднозначные о formant URL-адрес, а можно # и %</span><span class="sxs-lookup"><span data-stu-id="d572d-207">Existing APIs that are not ambiguous about the URL formant and can supports # and %</span></span>
 
<span data-ttu-id="d572d-208">Следующие интерфейсы API только принимают должным образом закодированный URL-адреса в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="d572d-208">The following APIs only accept properly encoded URLs as input.</span></span> <span data-ttu-id="d572d-209">Они также поддерживают в разделе закодированный URL-адресов, при условии, что URL-адрес может использоваться любой однозначно.</span><span class="sxs-lookup"><span data-stu-id="d572d-209">They also support under-encoded URLs as long as the URL can be consumed without any ambiguity.</span></span> <span data-ttu-id="d572d-210">Иными словами по крайней мере # или % символов в поле путь URL-адреса должны быть закодированы %.</span><span class="sxs-lookup"><span data-stu-id="d572d-210">In order words, at least # or % characters in the path of the URL should be % encoded.</span></span> <span data-ttu-id="d572d-211">Эти интерфейсы API будет продолжать работать в соответствии с существующей.</span><span class="sxs-lookup"><span data-stu-id="d572d-211">These APIs will continue to work in the existing way.</span></span> <span data-ttu-id="d572d-212">«#» в URL-адрес обрабатывается как разделитель фрагмент, но не является частью URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d572d-212">'#' in the URL is treated as a fragment delimiter, but not part of URL path.</span></span>

| <span data-ttu-id="d572d-213">Тип</span><span class="sxs-lookup"><span data-stu-id="d572d-213">Type</span></span> | <span data-ttu-id="d572d-214">Старый свойство</span><span class="sxs-lookup"><span data-stu-id="d572d-214">Old Property</span></span> | 
|----------|-------------|
| <span data-ttu-id="d572d-215">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="d572d-215">Microsoft.SharePoint.SPWeb</span></span> |  <span data-ttu-id="d572d-216">GetFileByUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-216">GetFileByUrl(System.String)</span></span> |
| <span data-ttu-id="d572d-217">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="d572d-217">Microsoft.SharePoint.SPWeb</span></span> |  <span data-ttu-id="d572d-218">GetFileByWOPIFrameUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-218">GetFileByWOPIFrameUrl(System.String)</span></span> |
| <span data-ttu-id="d572d-219">Microsoft.SharePoint.SPWeb</span><span class="sxs-lookup"><span data-stu-id="d572d-219">Microsoft.SharePoint.SPWeb</span></span> |  <span data-ttu-id="d572d-220">GetFileByLinkingUrl(System.String)</span><span class="sxs-lookup"><span data-stu-id="d572d-220">GetFileByLinkingUrl(System.String)</span></span> |

<span data-ttu-id="d572d-221">Для возврата System.Uri с кодировкой однозначное для использования с выше API-интерфейсы добавляются следующие свойства C#.</span><span class="sxs-lookup"><span data-stu-id="d572d-221">The following C# properties are added to return System.Uri with unambiguous encoding for use with the above APIs.</span></span> <span data-ttu-id="d572d-222">Старые вариант под возвращаемых API-интерфейсы декодировать URL-адреса и, поскольку они никогда не содержатся # или % символов, URL-адрес не был неоднозначным.</span><span class="sxs-lookup"><span data-stu-id="d572d-222">The older variant of the below APIs returned decoded URLs and since they never contained # or % characters, the URL was not ambiguous.</span></span> <span data-ttu-id="d572d-223">Перейти вперед, мы не должны нарушили декодированное поведение старые варианты преобразования % и # символов в пути.</span><span class="sxs-lookup"><span data-stu-id="d572d-223">Going forward, we did not want to break the decoded behavior of the older variants to encode % and # characters in path.</span></span> <span data-ttu-id="d572d-224">Таким образом были созданы новые интерфейсы API.</span><span class="sxs-lookup"><span data-stu-id="d572d-224">Therefore, new APIs were created.</span></span>
 
| <span data-ttu-id="d572d-225">Тип</span><span class="sxs-lookup"><span data-stu-id="d572d-225">Type</span></span>   |      <span data-ttu-id="d572d-226">Старый свойство</span><span class="sxs-lookup"><span data-stu-id="d572d-226">Old Property</span></span>      |  <span data-ttu-id="d572d-227">Новое свойство</span><span class="sxs-lookup"><span data-stu-id="d572d-227">New Property</span></span> |
|----------|-------------|------|
| <span data-ttu-id="d572d-228">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="d572d-228">Microsoft.SharePoint.SPFile</span></span> |  <span data-ttu-id="d572d-229">LinkingUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-229">LinkingUrl</span></span> | <span data-ttu-id="d572d-230">LinkingUri</span><span class="sxs-lookup"><span data-stu-id="d572d-230">LinkingUri</span></span> |
| <span data-ttu-id="d572d-231">Microsoft.SharePoint.SPFile</span><span class="sxs-lookup"><span data-stu-id="d572d-231">Microsoft.SharePoint.SPFile</span></span> |  <span data-ttu-id="d572d-232">ServerRedirectedEmbedUrl</span><span class="sxs-lookup"><span data-stu-id="d572d-232">ServerRedirectedEmbedUrl</span></span> | <span data-ttu-id="d572d-233">ServerRedirectedEmbedUri</span><span class="sxs-lookup"><span data-stu-id="d572d-233">ServerRedirectedEmbedUri</span></span> |


## <a name="sample-code"></a><span data-ttu-id="d572d-234">Пример кода</span><span class="sxs-lookup"><span data-stu-id="d572d-234">Sample code</span></span>

<span data-ttu-id="d572d-235">Ниже приведены некоторые примеры кода для базовых сценариев в CSOM.</span><span class="sxs-lookup"><span data-stu-id="d572d-235">Here are some sample code for basic scenarios in CSOM:</span></span>
 
- <span data-ttu-id="d572d-236">Добавить файл в папку (.net)</span><span class="sxs-lookup"><span data-stu-id="d572d-236">Add a file to a folder (.net)</span></span>

```C#
  ClientContext context = new ClientContext("http://site");
  Web web = context.Web;
  // Get the parent folder
  ResourcePath folderPath = ResourcePath.FromDecodedUrl("/Shared Documents");
  Folder parentFolder = web.GetFolderByServerRelativePath(folderPath);
 
  // Create the parameters used to add a file
  ResourcePath filePath = ResourcePath.FromDecodedUrl("/Shared Documents/hello world.txt");
  byte[] fileContent = System.Text.Encoding.UTF8.GetBytes("sample file content");
  FileCollectionAddParameters fileAddParameters = new FileCollectionAddParameters();
  fileAddParameters.Overwrite = true;
  using (MemoryStream contentStream = new MemoryStream(fileContent))
  {
    // Add a file
    Microsoft.SharePoint.Client.File addedFile = parentFolder.Files.AddUsingPath(filePath, fileAddParameters, contentStream);
 
    // Select properties of added file to inspect
    context.Load(addedFile, f => f.UniqueId, f1 => f1.ServerRelativePath);
 
    // Perform the actual operation
    context.ExecuteQuery();
 
    // Print the results
    Console.WriteLine(
      "Added File [UniqueId:{0}] [ServerRelativePath:{1}]",
      addedFile.UniqueId,
      addedFile.ServerRelativePath.DecodedUrl);
  }

```

- <span data-ttu-id="d572d-237">Добавить вложенную папку в папку (.net)</span><span class="sxs-lookup"><span data-stu-id="d572d-237">Add a sub-folder to a folder  (.net)</span></span>

```C#
    ClientContext context = new ClientContext("http://site");
    Web web = context.Web;
    // Get the parent folder
    ResourcePath folderPath = ResourcePath.FromDecodedUrl("/Shared Documents");
    Folder parentFolder = web.GetFolderByServerRelativePath(folderPath);
 
    // Create the parameters used to add a folder
    ResourcePath subFolderPath = ResourcePath.FromDecodedUrl("/Shared Documents/sub folder");
    FolderCollectionAddParameters folderAddParameters = new FolderCollectionAddParameters();
    folderAddParameters.Overwrite = true;
 
    // Add a sub folder
    Folder addedFolder = parentFolder.Folders.AddUsingPath(subFolderPath, folderAddParameters);
 
    // Select properties of added file to inspect
    context.Load(addedFolder, f => f.UniqueId, f1 => f1.ServerRelativePath);
 
    // Perform the actual operation
    context.ExecuteQuery();
 
    // Print the results
    Console.WriteLine(
        "Added Folder [UniqueId:{0}] [ServerRelativePath:{1}]",
        addedFolder.UniqueId,
        addedFolder.ServerRelativePath.DecodedUrl);
```

- <span data-ttu-id="d572d-238">Получение файла в веб-сайта (.net)</span><span class="sxs-lookup"><span data-stu-id="d572d-238">Get a file in the web (.net)</span></span>

```C#
    ClientContext context = new ClientContext("http://site");
    Web web = context.Web;
    // Get the file
    ResourcePath filePath = ResourcePath.FromDecodedUrl("/Shared Documents/hello world.txt");
    File file = web.GetFileByServerRelativePath(filePath);
 
    // Select properties of the file
    context.Load(file, f => f.UniqueId, f1 => f1.ServerRelativePath);
 
    // Perform the actual operation
    context.ExecuteQuery();
 
    // Print the results
    Console.WriteLine(
        "File Properties [UniqueId:{0}] [ServerRelativePath:{1}]",
        file.UniqueId,
        file.ServerRelativePath.DecodedUrl);
```

<span data-ttu-id="d572d-239">Ниже приведены некоторые примеры кода для базовых сценариев в REST.</span><span class="sxs-lookup"><span data-stu-id="d572d-239">Here are some sample code for basic scenarios in REST:</span></span>

- <span data-ttu-id="d572d-240">Получение папки</span><span class="sxs-lookup"><span data-stu-id="d572d-240">Get Folders</span></span>

```
url: http://site url/_api/web/GetFolderByServerRelativePath(decodedUrl='folder name')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

- <span data-ttu-id="d572d-241">Создание папки</span><span class="sxs-lookup"><span data-stu-id="d572d-241">Create Folder</span></span>
 
```
url: http://site url/_api/web/Folders/AddUsingPath(decodedurl='/document library relative url/folder name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
 
```
 
- <span data-ttu-id="d572d-242">Получение файлов</span><span class="sxs-lookup"><span data-stu-id="d572d-242">Get Files</span></span>
 
```
url: http://site url/_api/web/GetFileByServerRelativePath(decodedUrl='folder name/file name')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
 
- <span data-ttu-id="d572d-243">Добавление файлов</span><span class="sxs-lookup"><span data-stu-id="d572d-243">Add Files</span></span>
 
```
url: http://site url/_api/web/GetFolderByServerRelativePath(decodedUrl='folder name')/Files/AddStubUsingPath(decodedurl='testfile.txt')
methods: POST
Headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    Content-Length: length
 
```
