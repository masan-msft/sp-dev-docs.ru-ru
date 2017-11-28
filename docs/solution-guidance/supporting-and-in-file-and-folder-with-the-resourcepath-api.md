---
title: "Поддержка % и # в файлах и папках с помощью API ResourcePath"
ms.date: 11/03/2017
ms.openlocfilehash: 4667020c2387650d8ad84dc000afa785f7b07016
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="supporting--and--in-file-and-folder-with-the-resourcepath-api"></a>Поддержка % и # в файлах и папках с помощью API ResourcePath

Поддержка % и # в файлах и папках развертывается в SharePoint Online.  К сожалению из-за существующих структур API и вызов шаблонов, работа с именами могут иногда неоднозначность.  Можно найти [Дополнительные фон за это в нашем блоге разработчика](https://dev.office.com/blogs/upcoming-changes-to-sharepoint-and-onedrive-for-business-apis-to-support-and-in-file-names).  Таким образом были добавлены новые интерфейсы API SharePoint Online клиента объектной модели (CSOM) рабочей области для обеспечения поддержки # до % символов.

## <a name="resourcepath"></a>ResourcePath
 
Как краткий обзор Обратите внимание на то, существующий дескриптор на основе строки API-интерфейсов SharePoint (например, SPFileCollection.GetByUrl) оба кодируются и автоматически декодировать URL-адресов, если предполагается, что подразумевает % и # символов пути зашифрованную URL-адрес.  С помощью поддержки % и # в файлы и папки, в этом автоматическая обработка теперь инспектором так как он может привести к игнорировать или mishandle имена файлов с помощью % и # в них нижестоящие кода.
 
Новый класс-- `Microsoft.SharePoint.Client.ResourcePath` --был добавлен к интерфейсам API.  Класс ResourcePath является основой для поддержки этих новых символов.  Она позволяет новые, однозначное устранения элемент в SharePoint и OneDrive для бизнеса, поскольку предполагается, что и работает только с декодированное URL-адреса. Он заменяет на основе строки пути для представления полное (абсолютный) или partial (относительный) URL-адрес семейства веб-сайтов, сайта, файла, папки или других артефактов и OneDrive для бизнеса. Для правильной поддержки % и # внутри URL-адреса, необходимо будет использовать API на основе ResourcePath, а также декодировать URL-адреса.
 
ResourcePath простую структуру, вызвав статической функции `ResourcePath.FromDecodedUrl(string)`. Входное значение, переданное может осуществляться из объекта ResourcePath вызов свойства DecodedUrl. 
 
Для существующих вызовов, в основе строки URL-адреса, необходимо определить ли путь к коду, приводя к на основе строки звонки URL-адрес, предоставленных с URL-адреса конечной и ли тех код пути, также может ссылки привязки (то есть: дополнения #bookmark на в верхней части файла URL-адреса.)

> Примечание: Не просто найти и заменить существующий режимы работы на основе строку URL-адрес API-интерфейсов с `ResourcePath.FromDecodedUrl`.  Необходимо правильно определить URL-адрес и потенциально декодировать URL-адреса, перед использованием сначала `ResourcePath.FromDecodedUrl(string)` API.

В тех случаях, где протоколе, приводя к вызов API SharePoint на основе String используется **Декодировать URL-адреса (например, «FY17 Report.docx»)**, а затем можно просто замените эти вызовы с `ResourcePath.FromDecodedUrl(string)` и эквивалентные методы ResourcePath, перечисленных ниже.
 
Обратите внимание, что во многих случаях, где чтение URL-адрес из SharePoint с помощью API-интерфейсов, ResourcePath также позволяет сделать эти шаблоны кода согласованность, поэтому ResourcePath можно использовать вместо URL-адреса.
 
Также Обратите внимание, что это изменение распространяется и на основе SharePoint REST вызовов, а также.  Ознакомьтесь со сценариями ниже, чтобы просмотреть примеры эти новые интерфейсы API в REST.

## <a name="new-apis-that-are-based-on-resourcepath-and-supports--and-"></a>Новые интерфейсы API, которые основаны на ResourcePath и поддерживает # и %
 
Ниже приведены новые интерфейсы API, мы представили заменить существующие интерфейсы API для поддержки # и %. Мы в списке старый интерфейс API и новые API рядом друг с другом для вашей сравнения. Основные функциональные возможности этих API не изменяется, однако изменить способ представления расположение элемента.
 
Документация по новые интерфейсы API можно ссылаться на https://msdn.microsoft.com/en-us/library/jj193041.aspx.  Перечислены .net CSOM ниже интерфейсы API, но новые методы, также доступны в эквивалентный формы в нашей библиотеки JavaScript CSOM.
 
**Сборки Microsoft.SharePoint.Client.dll**

| Тип | Старый метод | Новый метод | 
|----------|-------------|------|
| Microsoft.SharePoint.SPList | AddItem(Microsoft.SharePoint.SPListItemCreationInformation) | AddItemUsingPath (SPListItemCreationInformationUsingPath параметров) | 
| Microsoft.SharePoint.SPFile | MoveTo (System.String, Microsoft.SharePoint.SPMoveOperations) | MoveToUsingPath (SPResourcePath newPath, SPMoveOperations moveOperations) | 
| Microsoft.SharePoint.SPFile | CopyTo (System.String, Boolean) | CopyToUsingPath (SPResourcePath newPath, перезаписать bool) | 
| Microsoft.SharePoint.SPFileCollection | GetByUrl(System.String) | GetByPath(SPResourcePath) | 
| Microsoft.SharePoint.SPFileCollection | Добавление (System.String, Microsoft.SharePoint.SPTemplateFileType) | AddUsingPath (SPResourcePath, SPFileCollectionAddWithTemplateParameters) | 
| Microsoft.SharePoint.SPFolder | MoveTo(System.String) | MoveToUsingPath (SPResourcePath newPath) | 
| Microsoft.SharePoint.SPFolder | AddSubFolder(System.String) | AddSubFolderUsingPath (SPResourcePath leafPath) | 
| Microsoft.SharePoint.SPFolderCollection | GetByUrl(System.String) | GetByPath (SPResourcePath путь) | 
| Microsoft.SharePoint.SPFolderCollection | Add(System.String) | AddUsingPath (SPResourcePath пути, параметры SPFolderCreationInformation) | 
|  | AddWithOverwrite (строка URL-адреса, перезаписать bool) |  | 
| Microsoft.SharePoint.SPRemoteWeb | GetFileByServerRelativeUrl(System.String) | GetFileByServerRelativePath (SPResourcePath путь) | 
| Microsoft.SharePoint.SPWeb | GetList(System.String) | GetListUsingPath(SPResourcePath) | 
| Microsoft.SharePoint.SPWeb | GetListItem(System.String) | GetListItemUsingPath(SPResourcePath) | 


Следующие объекты CSOM получить ResourcePath свойства, которые могут использоваться в выше API-интерфейсы. Несмотря на то, что старый свойство также возвращает декодированное URL-адреса, свойство ResourcePath предоставляется для удобства, простоты и ясности в вызова выше API-интерфейсы.  Одно исключение — это является свойство SPFolder.WelcomePage, которое ранее возвращенный кодированных и некодированных URL-адресов; Теперь однозначно возвращаются через свойство WelcomePagePath.

| Тип | Старый свойство | Новое свойство | 
|----------|-------------|------|
| Microsoft.SharePoint.SPList | DefaultViewUrl | DefaultViewPath | 
| Microsoft.SharePoint.SPList | DefaultEditFormUrl | DefaultEditFormPath | 
| Microsoft.SharePoint.SPList | DefaultNewFormUrl | DefaultNewFormPath | 
| Microsoft.SharePoint.SPList | DefaultDisplayFormUrl | DefaultDisplayFormPath | 
| Microsoft.SharePoint.SPAttachment | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPFile | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPFolder | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPFolder | WelcomePage | WelcomePagePath / WelcomePageParameters | 
| Microsoft.SharePoint.SPView | ServerRelativeUrl | ServerRelativePath | 
| Microsoft.SharePoint.SPDocumentLibraryInformation | ServerRelativeUrl | ServerRelativePath | 


## <a name="existing-apis-that-are-not-ambiguous-about-the-url-formant-and-can-supports--and-"></a>Существующие интерфейсы API, не являются неоднозначные о formant URL-адрес, а можно # и %
 
Следующие интерфейсы API только принимают должным образом закодированный URL-адреса в качестве входных данных. Они также поддерживают в разделе закодированный URL-адресов, при условии, что URL-адрес может использоваться любой однозначно. Иными словами по крайней мере # или % символов в поле путь URL-адреса должны быть закодированы %. Эти интерфейсы API будет продолжать работать в соответствии с существующей. «#» в URL-адрес обрабатывается как разделитель фрагмент, но не является частью URL-адрес.

| Тип | Старый свойство | 
|----------|-------------|
| Microsoft.SharePoint.SPWeb |  GetFileByUrl(System.String) |
| Microsoft.SharePoint.SPWeb |  GetFileByWOPIFrameUrl(System.String) |
| Microsoft.SharePoint.SPWeb |  GetFileByLinkingUrl(System.String) |

Для возврата System.Uri с кодировкой однозначное для использования с выше API-интерфейсы добавляются следующие свойства C#. Старые вариант под возвращаемых API-интерфейсы декодировать URL-адреса и, поскольку они никогда не содержатся # или % символов, URL-адрес не был неоднозначным. Перейти вперед, мы не должны нарушили декодированное поведение старые варианты преобразования % и # символов в пути. Таким образом были созданы новые интерфейсы API.
 
| Тип   |      Старый свойство      |  Новое свойство |
|----------|-------------|------|
| Microsoft.SharePoint.SPFile |  LinkingUrl | LinkingUri |
| Microsoft.SharePoint.SPFile |  ServerRedirectedEmbedUrl | ServerRedirectedEmbedUri |


## <a name="sample-code"></a>Пример кода

Ниже приведены некоторые примеры кода для базовых сценариев в CSOM.
 
- Добавить файл в папку (.net)

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

- Добавить вложенную папку в папку (.net)

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

- Получение файла в веб-сайта (.net)

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

Ниже приведены некоторые примеры кода для базовых сценариев в REST.

- Получение папки

```
url: http://site url/_api/web/GetFolderByServerRelativePath(decodedUrl='folder name')
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

- Создание папки
 
```
url: http://site url/_api/web/Folders/AddUsingPath(decodedurl='/document library relative url/folder name')
method: POST
headers:
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
 
```
 
- Получение файлов
 
```
url: http://site url/_api/web/GetFileByServerRelativePath(decodedUrl='folder name/file name')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
 
- Добавление файлов
 
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
