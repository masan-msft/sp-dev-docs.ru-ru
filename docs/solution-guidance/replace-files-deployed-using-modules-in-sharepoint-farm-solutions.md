---
title: "Замените файлы развернуты с помощью модули решений фермы SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3ea55aa39c86acc513ce65954e9ed5cf2195902b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="replace-files-deployed-using-modules-in-sharepoint-farm-solutions"></a>Замените файлы развернуты с помощью модули решений фермы SharePoint

Замените файлы, такие как главные страницы и макеты страниц в SharePoint, которые были развернуты с использованием модулей в решениях фермы, отправка и обновление ссылок для использования новых файлов.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Если вы развернули файлов декларативно с использованием модулей в решениях фермы, узнайте, как преобразовать их в новые решения, обновите ссылки на файлы и обеспечить аналогичную функциональность, с помощью клиентской объектной модели (CSOM). В прошлом модули использовались для развертывания файлы, такие как главные страницы и макеты страниц. В этой статье описывается использование процесса преобразования:

1. Отправка новых главных страниц и макетов страниц.
    
2. Обновите ссылки для использования нового главные страницы и файлы компоновки страниц.
    
Использование этого преобразования обработки, когда:

- Существующих решений фермы используется модули для развертывания файлов.
    
-  Вы хотите заменить главные страницы и макеты страниц в решений фермы с новой главной страницы и макеты страниц, чтобы они могут быть перенесены в SharePoint Online.
    
- Установки типов контента документов на главные страницы и макеты страниц в решении фермы декларативно.

**Важные:**  Решения фермы нельзя перенести в SharePoint Online. Применение методики и кода, описанного в данной статье, можно создать новое решение с аналогичными возможностями, обеспечивающие решений фермы обновления ссылки на файлы, и затем можно развернуть новое решение в SharePoint Online. Можно отключить функцию и отозвать предыдущей решения фермы. Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения. Например, в этой статье не рассматривается, как выполнить проверку подлинности с помощью Office 365, как реализовать обработку исключений обязательные и т. д. Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).

## <a name="before-you-begin"></a>Перед началом работы

В идеальном варианте следует ознакомиться существующих решений фермы, узнайте о методах, описанных в этой статье и затем планирование применение этих методов для своих сценариев. Если не знакомы с решениями фермы или нет существующее решение фермы для работы с могут быть полезны позволяет:

- Загрузите [решение Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet). Просмотрите упражнения 1 в [замены файлов подготовить, используя модулей в решениях полного доверия](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-1%20Replacement%20of%20files%20deployed%20via%20Modules/Lab.md) для быстрого Общие сведения о главных страниц и страницы макетов может были созданы в прошлом.
    
- Ознакомьтесь с решениями фермы. Для получения дополнительных сведений см. [Обзор архитектуры SharePoint 2010](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) и[создания решений фермы в SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).
    
Перед запуском примера кода необходимо включите функции публикации на веб-сайтов и сайта с помощью следующих процедур.

1. Чтобы включить функцию **Инфраструктуры публикации SharePoint Server** на семейства веб-сайтов:
    
    1. Откройте сайт SharePoint и перейдите в раздел **Параметры** > **Параметры сайта**.
    
    2. **Администрирование семейства веб-сайтов**выберите **возможности семейства сайтов**.
    
    3. **Инфраструктуры публикации SharePoint Server**нажмите кнопку **активировать**.
    
2. Чтобы включить функцию **Публикации SharePoint Server** на сайте:
    
    1. Откройте сайт SharePoint и перейдите в раздел **Параметры** > **Параметры сайта**.
    
    2. В списке **Действия сайта**выберите **Управление возможностями сайта**.
    
    3. На **Публикации SharePoint Server**нажмите кнопку **активировать**.
    
Настройка проекта Visual Studio:

1. Загрузите [Образец проекта](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/Student.zip). Выберите **Представление необработанные** для загрузки образец проекта, извлеките файлы из ZIP-файл и затем перейдите к папке Module9/ModuleReplacement.
    
2. Откройте ModuleReplacement.sln.
    
3. Откройте settings.xml. Просмотр и обновление следующие атрибуты в соответствии с требованиями:
    
    1.  элемент **masterpage** - использует **атрибут** для указания новой главной страницы, развертывание в коллекции главных страниц, а атрибут **заменяет** определяет существующей главной страницы в коллекции главных страниц.
    
    2.  элемент **pageLayout** - использует атрибут **файла** , чтобы указать новый файл макета страницы, атрибут **заменяет** для выбора существующего файла макета страницы и некоторые другие атрибуты, чтобы указать сведения о дополнительных страницы макета.

    **Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

    ```XML
        <?xml version="1.0" encoding="utf-8" ?>
        <branding>
          <masterPages>
               <masterPage file="contoso_app.master" replaces="contoso.master"/>
          </masterPages>
          <pageLayouts>
               <pageLayout file="ContosoWelcomeLinksApp.aspx" replaces="ContosoWelcomeLinks.aspx" title="Contoso Welcome Links add-in" associatedContentTypeName="Contoso Web Page" defaultLayout="true" />
          </pageLayouts>
        </branding>
    
    ```

4. В MasterPageGalleryFiles.cs **MasterPageGalleryFile** и **LayoutFile** классы определяются бизнес-объекты, в которых хранятся сведения о новых главных страниц и макетов страниц для отправки в SharePoint.

## <a name="upload-and-update-references-to-master-pages"></a>Отправка и обновление ссылок на главных страницах

Для загрузки и обновления ссылок на новые главные страницы на сайте SharePoint:

1. В файле Program.cs добавьте следующий оператор **using** .
    
    ```C#
        using System.Security;
    ```

2. В файле Program.cs добавьте следующие методы для выполнения проверки подлинности в Office 365.
    
  ```C#
  static SecureString GetPassword()
        {
            SecureString sStrPwd = new SecureString();
            try
            {
                Console.Write("Password: ");

                for (ConsoleKeyInfo keyInfo = Console.ReadKey(true); keyInfo.Key != ConsoleKey.Enter; keyInfo = Console.ReadKey(true))
                {
                    if (keyInfo.Key == ConsoleKey.Backspace)
                    {
                        if (sStrPwd.Length > 0)
                        {
                            sStrPwd.RemoveAt(sStrPwd.Length - 1);
                            Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                            Console.Write(" ");
                            Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                        }
                    }
                    else if (keyInfo.Key != ConsoleKey.Enter)
                    {
                        Console.Write("*");
                        sStrPwd.AppendChar(keyInfo.KeyChar);
                    }

                }
                Console.WriteLine("");
            }
            catch (Exception e)
            {
                sStrPwd = null;
                Console.WriteLine(e.Message);
            }

            return sStrPwd;
        }

        static string GetUserName()
        {
            string strUserName = string.Empty;
            try
            {
                Console.Write("Username: ");
                strUserName = Console.ReadLine();
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
                strUserName = string.Empty;
            }
            return strUserName;
        }
  ```

3. В файле Program.cs добавьте следующий код в метод **Main** , который выполняет следующие задачи:
    
    1. Загружает файл settings.xml.
    
    2. Возвращает ссылку на коллекцию главных страниц с помощью [GetCatalog](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.getcatalog.aspx)(116). Главные страницы можно было выгрузить в коллекции главных страниц. Идентификатор шаблона списка коллекции главных страниц — 116. Для получения дополнительных сведений см [Элемент ListTemplate (Site)](https://msdn.microsoft.com/library/ms439434.aspx). Загружаются другие сведения о коллекции главных страниц, включая использование [List.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.contenttypes.aspx) для получения типов контента, связанные с коллекции главных страниц.
    
    3. Загружает свойства веб-объект, включая Web.ContentTypes, Web.MasterUrl и Web.CustomMasterUrl.
    
    4. Задает **parentMasterPageContentTypeId** идентификатор типа контента, главных страниц. Дополнительные сведения см в[Иерархии типов контента Base](https://msdn.microsoft.com/library/ms452896%28v=office.14%29.aspx).
    
    5. Получает тип контента, главных страниц в коллекции главных страниц. Этот тип контента используется для задания типа контента новой главной страницы далее в этой статье. 
    
    ```C#
    static void Main(string[] args)
        { 
            string userName = GetUserName();
            SecureString pwd = GetPassword();
            
         // End program if no credentials were entered.
            if (string.IsNullOrEmpty(userName) || (pwd == null))
              return;
                                   
            using (var clientContext = new ClientContext("http://sharepoint.contoso.com"))
            {
                            
                clientContext.AuthenticationMode = ClientAuthenticationMode.Default;
                clientContext.Credentials = new SharePointOnlineCredentials(userName, pwd);
                    
                XDocument settings = XDocument.Load("settings.xml");
    
                // Get a reference to the master page gallery which will be used to upload new master pages. 
             
                Web web = clientContext.Web;
                List gallery = web.GetCatalog(116);
                Folder folder = gallery.RootFolder;
            
                 // Load additional master page gallery properties.
                clientContext.Load(folder);
                clientContext.Load(gallery,
                                    g => g.ContentTypes,
                                    g => g.RootFolder.ServerRelativeUrl);
        
                // Load the content types and master page information from the web.
                clientContext.Load(web,
                                    w => w.ContentTypes,
                                    w => w.MasterUrl,
                                    w => w.CustomMasterUrl);
                clientContext.ExecuteQuery();
    
                // Get the content type for the master page from the master page gallery using the content type ID for masterpages (0x010105).
                const string parentMasterPageContentTypeId = "0x010105";  
                ContentType masterPageContentType = gallery.ContentTypes.FirstOrDefault(ct => ct.StringId.StartsWith(parentMasterPageContentTypeId));
                UploadAndSetMasterPages(web, folder, clientContext, settings, masterPageContentType.StringId);
                             
            }
    
        }
    ```

4. В файле Program.cs добавьте в метод **UploadAndSetMasterPages** , который создает список **MasterPageGalleryFile** бизнес-объекты с:
    
    1. Чтение всех **masterPage** элементы, определенные в settings.xml.
    
    2. Для каждого элемента **masterPage** , который определяет главную страницу отправка в SharePoint, загрузка значения атрибутов в бизнес-объект **MasterPageGalleryFile** .
    
    3. Для каждого объекта business **MasterPageGalleryFile** в списке, что вызов **UploadAndSetMasterPage**.
    
    ```C#
        
    private static void UploadAndSetMasterPages(Web web, Folder folder, ClientContext clientContext, XDocument settings, string contentTypeId)
    {
        IList<MasterPageGalleryFile> masterPages = (from m in settings.Descendants("masterPage")
                                                    select new MasterPageGalleryFile
                                                    {
                                                        File = (string)m.Attribute("file"),
                                                        Replaces = (string)m.Attribute("replaces"),
                                                        ContentTypeId = contentTypeId
                                                    }).ToList();
        foreach (MasterPageGalleryFile masterPage in masterPages)
        {
            UploadAndSetMasterPage(web, folder, clientContext, masterPage);
        }
    }
    ```

5. В файле Program.cs добавьте в метод **UploadAndSetMasterPage** , который выполняет следующие задачи:
    
    1. Извлекает главной страницы.
    
    2. Загружает новый файл с помощью [FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx).
    
    3. Получает элемент списка, связанного с загруженных файлов.
    
    4. Задает различные свойства элемента списка, включая установку идентификатор типа контента элемента списка идентификатор типа контента главной страницы.
    
    5. Проверка в, публикацию и утверждает новой главной страницы. 
    
    6. Если главной страницы текущего сайта или настраиваемой главной страницы URL-адрес имеет значение old главной страницы, обновляет [Web.MasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.masterurl.aspx) или[Web.CustomMasterUrl](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.custommasterurl.aspx) , чтобы использовать URL-адрес недавно добавленные главной страницы.
    
    ```C#
      private static void UploadAndSetMasterPage(Web web, Folder folder, ClientContext clientContext, MasterPageGalleryFile masterPage)
    {
        using (var fileReadingStream = System.IO.File.OpenRead(masterPage.File))
        {
            // If necessary, ensure that the master page is checked out.
            PublishingHelper.CheckOutFile(web, masterPage.File, folder.ServerRelativeUrl);
    
    // Use the FileCreationInformation class to upload the new file.
            var fileInfo = new FileCreationInformation();
            fileInfo.ContentStream = fileReadingStream;
            fileInfo.Overwrite = true;
            fileInfo.Url = masterPage.File;
            File file = folder.Files.Add(fileInfo);
    
    // Get the list item associated with the newly uploaded master page file.
            ListItem item = file.ListItemAllFields;
            clientContext.Load(file.ListItemAllFields);
            clientContext.Load(file,
                                f => f.CheckOutType,
                                f => f.Level,
                                f => f.ServerRelativeUrl);
            clientContext.ExecuteQuery();
    
    item["ContentTypeId"] = masterPage.ContentTypeId;
            item["UIVersion"] = Convert.ToString(15);
            item["MasterPageDescription"] = "Master Page Uploaded using CSOM";
            item.Update();
            clientContext.ExecuteQuery();
    
    // If necessary, check in, publish, and approve the new master page file. 
            PublishingHelper.CheckInPublishAndApproveFile(file);
    
    // On the current site, update the master page references to use the new master page. 
            if (web.MasterUrl.EndsWith("/" + masterPage.Replaces))
            {
                web.MasterUrl = file.ServerRelativeUrl;
            }
            if (web.CustomMasterUrl.EndsWith("/" + masterPage.Replaces))
            {
                web.CustomMasterUrl = file.ServerRelativeUrl;
            }
            web.Update();
            clientContext.ExecuteQuery();
        }
    }
    ```

## <a name="upload-and-update-references-to-page-layouts"></a>Отправка и обновление ссылок в макеты страниц

**Примечание:**  В примерах кода в этом разделе Построение на примеры кода в предыдущем разделе данной статьи. 

Чтобы заменить макеты страниц, которые были развернуты с использованием модулей в решениях фермы, отправка и обновление ссылки для использования новых файлов макет страницы с:


1. Обновление **методе** приведенный ниже код. Этот код содержит дополнительные действия для загрузки и обновления ссылки на файлы макета страницы, включая:
    
    1. Установка **parentPageLayoutContentTypeId** для идентификатора типа контента макета страницы.
    
    2.  Получение типа контента, которая соответствует **parentPageLayoutContentTypeId** из коллекции главных страниц.
    
    3. Вызов **UploadPageLayoutsAndUpdateReferences**.
    
    ```C#
                static void Main(string[] args)
        { 
            string userName = GetUserName();
            SecureString pwd = GetPassword();
            
         // End program if no credentials were entered.
            if (string.IsNullOrEmpty(userName) || (pwd == null))
              return;
                                   
            using (var clientContext = new ClientContext("http://sharepoint.contoso.com"))
            {
                            
                clientContext.AuthenticationMode = ClientAuthenticationMode.Default;
                clientContext.Credentials = new SharePointOnlineCredentials(userName, pwd);
                    
                XDocument settings = XDocument.Load("settings.xml");
    
                // Get a reference to the master page gallery, which will be used to upload new master pages. 
             
                Web web = clientContext.Web;
                List gallery = web.GetCatalog(116);
                Folder folder = gallery.RootFolder;
            
                 // Load additional master page gallery properties. 
                clientContext.Load(folder);
                clientContext.Load(gallery,
                                    g => g.ContentTypes,
                                    g => g.RootFolder.ServerRelativeUrl);
        
                // Load the content types and master page information from the web.
                clientContext.Load(web,
                                    w => w.ContentTypes,
                                    w => w.MasterUrl,
                                    w => w.CustomMasterUrl);
                clientContext.ExecuteQuery();
    
                // Get the content type for the master page from the master page gallery using the content type ID for masterpages (0x010105).
                const string parentMasterPageContentTypeId = "0x010105";  
                ContentType masterPageContentType = gallery.ContentTypes.FirstOrDefault(ct => ct.StringId.StartsWith(parentMasterPageContentTypeId));
                UploadAndSetMasterPages(web, folder, clientContext, settings, masterPageContentType.StringId);
                             
    
               // Get the content type ID for the page layout, and then update references to the page layouts.
               const string parentPageLayoutContentTypeId = "0x01010007FF3E057FA8AB4AA42FCB67B453FFC100E214EEE741181F4E9F7ACC43278EE811"; 
               ContentType pageLayoutContentType = gallery.ContentTypes.FirstOrDefault(ct => ct.StringId.StartsWith(parentPageLayoutContentTypeId));
               UploadPageLayoutsAndUpdateReferences(web, folder, clientContext, settings, pageLayoutContentType.StringId);
            }
    
        }
    ```

2. В файле Program.cs добавьте в метод **UploadPageLayoutsAndUpdateReferences** , который необходимо выполнить следующие действия:
    
    1. Считывает сведения о замене макета страницы, чтение элементов **pagelayout** settings.xml, хранение сведения о замене макета страницы в **LayoutFile** бизнес-объектов и Добавление бизнес-объекты в список.
    
    2. Для каждого макета страницы для замены:
    
        1. Запросы типов контента сайта с помощью [Web.ContentTypes](https://msdn.microsoft.com/library/microsoft.sharepoint.client.web.contenttypes.aspx) поиск соответствующего контента введите, где имя типа контента сайта равно **associatedContentTypeName** , указанных в settings.xml для нового макета страницы.
    
        2. Вызывает **UploadPageLayout**.
    
        3. Вызывает **UpdatePages** для обновления существующих страниц для использования новых макетов страниц.

  ```C#
        private static void UploadPageLayoutsAndUpdateReferences(Web web, Folder folder, ClientContext clientContext, XDocument settings, string contentTypeId)
{
    // Read the replacement settings stored in pageLayout elements in settings.xml.
    IList<LayoutFile> pageLayouts = (from m in settings.Descendants("pageLayout")
                                 select new LayoutFile
                                 {
                                     File = (string)m.Attribute("file"),
                                     Replaces = (string)m.Attribute("replaces"),
                                     Title = (string)m.Attribute("title"),
                                     ContentTypeId = contentTypeId,
                                     AssociatedContentTypeName = (string)m.Attribute("associatedContentTypeName"),
                                     DefaultLayout = m.Attribute("defaultLayout") != null &amp;&amp; (bool)m.Attribute("defaultLayout")
                                 }).ToList();

// Update the content type association.
            foreach (LayoutFile pageLayout in pageLayouts)
    {
        ContentType associatedContentType =
            web.ContentTypes.FirstOrDefault(ct => ct.Name == pageLayout.AssociatedContentTypeName);
        pageLayout.AssociatedContentTypeId = associatedContentType.StringId;                
        UploadPageLayout(web, folder, clientContext, pageLayout);
    }
            
            UpdatePages(web, clientContext, pageLayouts);
        }

  ```

3.  В файле Program.cs добавьте в метод **UploadPageLayout** , который выполняет следующие задачи:
    
    1. Извлекает файл макета страницы.
    
    2. Загружает новый файл с помощью [FileCreationInformation](https://msdn.microsoft.com/library/microsoft.sharepoint.client.filecreationinformation.aspx).
    
    3. Получает элемент списка, связанного с загруженных файлов.
    
    4. Задает различные свойства элемента списка, включая **ContentTypeId** и **PublishingAssociatedContentType**.
    
    5. Проверка в, публикацию и утверждает новый файл макета страницы.
    
    6.  Для удаления ссылки на старый файл макета страницы, звонки **PublishingHelper.UpdateAvailablePageLayouts** , чтобы обновить данные XML хранятся в свойстве **PageLayouts** на текущем сайте.
    
    7. Если значение атрибута **defaultLayout** загруженных файлов макет страницы с settings.xml задано значение **true** , использует **PublishingHelper.SetDefaultPageLayout** для обновления XML, сохраненный в свойстве **DefaultPageLayout** на текущего сайта.
    

    ```C#
    private static void UploadPageLayout(Web web, Folder folder, ClientContext clientContext, LayoutFile pageLayout)
    {
        using (var fileReadingStream = System.IO.File.OpenRead(pageLayout.File))
        {
            PublishingHelper.CheckOutFile(web, pageLayout.File, folder.ServerRelativeUrl);
            // Use FileCreationInformation to upload the new page layout file.
            var fileInfo = new FileCreationInformation();
            fileInfo.ContentStream = fileReadingStream;
            fileInfo.Overwrite = true;
            fileInfo.Url = pageLayout.File;
            File file = folder.Files.Add(fileInfo);
            // Get the list item associated with the newly uploaded file.
            ListItem item = file.ListItemAllFields;
            clientContext.Load(file.ListItemAllFields);
            clientContext.Load(file,
                                f => f.CheckOutType,
                                f => f.Level,
                                f => f.ServerRelativeUrl);
            clientContext.ExecuteQuery();
    
    item["ContentTypeId"] = pageLayout.ContentTypeId;
            item["Title"] = pageLayout.Title;
            item["PublishingAssociatedContentType"] = string.Format(";#{0};#{1};#", pageLayout.AssociatedContentTypeName, pageLayout.AssociatedContentTypeId);
            item.Update();
            clientContext.ExecuteQuery();
    
    PublishingHelper.CheckInPublishAndApproveFile(file);
    
    PublishingHelper.UpdateAvailablePageLayouts(web, clientContext, pageLayout, file);
    
    if (pageLayout.DefaultLayout)
            {
                PublishingHelper.SetDefaultPageLayout(web, clientContext, file);
            }
        }
    }
    ```

4. В файле Program.cs добавьте в метод **UpdatePages** , который выполняет следующие задачи:
    
    1. Получает библиотеки **страниц** , а затем получает все элементы списка в библиотеке **страниц** .
    
    2. Для каждого элемента списка с помощью поля **PublishingPageLayout** элемента списка для поиска соответствия макета страницы для обновления, который был указан в settings.xml и теперь хранятся в **pagelayouts** . Если элемент списка **PublishingPageLayout** поля необходимо обновить для ссылки на новый макет страницы:
    
        1. Извлекает файл элемента списка с помощью **PublishingHelper.CheckOutFile**.
    
        2. Обновляет URL-адрес макет страницы, обратитесь к файлу нового макета страницы, а затем обновляет поле **PublishingPageLayout** элемента списка.
    
        3. Проверка в, публикацию и утверждает файла, указанный элемент списка.

    ```C#
    private static void UpdatePages(Web web, ClientContext clientContext, IList<LayoutFile> pageLayouts)
    {
        // Get the Pages Library, and then get all the list items in it.
        List pagesList = web.Lists.GetByTitle("Pages");
        var allItemsQuery = CamlQuery.CreateAllItemsQuery();
        ListItemCollection items = pagesList.GetItems(allItemsQuery);
        clientContext.Load(items);
        clientContext.ExecuteQuery();
        foreach (ListItem item in items)
        {
            // Only update those pages that are using a page layout which is being replaced.
            var pageLayout = item["PublishingPageLayout"] as FieldUrlValue;
            if (pageLayout != null)
            {
                LayoutFile matchingLayout = pageLayouts.FirstOrDefault(p => pageLayout.Url.EndsWith("/" + p.Replaces));
                if (matchingLayout != null)
                {
                    // Check out the page so that we can update the page layout. 
                    PublishingHelper.CheckOutFile(web, item);
    
    // Update the pageLayout reference.
                    pageLayout.Url = pageLayout.Url.Replace(matchingLayout.Replaces, matchingLayout.File);
                    item["PublishingPageLayout"] = pageLayout;
                    item.Update();
                    File file = item.File;
    
    // Get the file and other attributes so that you can check in the file.
                    clientContext.Load(file,
                        f => f.Level,
                        f => f.CheckOutType);
                    clientContext.ExecuteQuery();
    
    
                    PublishingHelper.CheckInPublishAndApproveFile(file);
                }
            }
        }
    }
    ```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Преобразование решений ферм для модели надстроек SharePoint](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [SharePoint 2013](https://msdn.microsoft.com/library/office/jj162979.aspx)
