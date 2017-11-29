---
title: "Отправка веб-частей в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c7e6e7a4bc6d843661ecd7c27d71381f47254ca9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="upload-web-parts-in-sharepoint"></a><span data-ttu-id="a7758-102">Отправка веб-частей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a7758-102">Upload Web Parts in SharePoint</span></span>

<span data-ttu-id="a7758-103">Развертывание предварительно настроенным, стандартный SharePoint веб-частей для пользователей.</span><span class="sxs-lookup"><span data-stu-id="a7758-103">Deploy pre-configured, standard SharePoint Web Parts for your users.</span></span>

<span data-ttu-id="a7758-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="a7758-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="a7758-105">Можно загрузить предварительно настроенным, стандартных веб-частей SharePoint для пользователей, чтобы добавлять на свои сайты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a7758-105">You can upload pre-configured, standard SharePoint Web Parts for users to add to their SharePoint sites.</span></span> <span data-ttu-id="a7758-106">Например можно передать предварительно настроенный:</span><span class="sxs-lookup"><span data-stu-id="a7758-106">For example, you can upload a pre-configured:</span></span>

- <span data-ttu-id="a7758-107">Редактор сценариев веб-часть, которая использует файлы JavaScript на удаленной веб.</span><span class="sxs-lookup"><span data-stu-id="a7758-107">Script Editor Web Part that uses JavaScript files on the remote web.</span></span>
    
- <span data-ttu-id="a7758-108">Веб-часть поиска контента.</span><span class="sxs-lookup"><span data-stu-id="a7758-108">Content Search Web Part.</span></span>
    
<span data-ttu-id="a7758-109">В этой статье рассматриваются предварительная настройка веб-части редактора скрипта для использования файлов JavaScript на удаленной веб-для выполнения настройки пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a7758-109">This article discusses pre-configuring the Script Editor Web Part to use JavaScript files on the remote web to perform UI customization.</span></span> <span data-ttu-id="a7758-110">Используйте для этого решения:</span><span class="sxs-lookup"><span data-stu-id="a7758-110">Use this solution to:</span></span>

- <span data-ttu-id="a7758-111">Используйте в сценарии с удаленного веб-узла в веб-части, а не ссылающегося скрипты из списка **Ресурсы сайта** на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="a7758-111">Use script files from the remote web in your Web Parts rather than referencing scripts from the **Site Assets** list on the host web.</span></span>
    
- <span data-ttu-id="a7758-112">Развертывание предварительно настроенную веб-частей в настраиваемой процедуры подготовки сайта.</span><span class="sxs-lookup"><span data-stu-id="a7758-112">Deploy pre-configured Web Parts in your custom site provisioning process.</span></span> <span data-ttu-id="a7758-113">Например как часть настраиваемой процедуры подготовки сайта, можно отображать сведения об использовании политики сайта для пользователя при создании нового сайта.</span><span class="sxs-lookup"><span data-stu-id="a7758-113">For example, as part of your custom site provisioning process, you might want to display site usage policy information to the user when a new site is created.</span></span> 
    
- <span data-ttu-id="a7758-114">Автоматически Загрузите содержимое отфильтрованные в веб-частей для пользователей.</span><span class="sxs-lookup"><span data-stu-id="a7758-114">Automatically load filtered content in your Web Parts for your users.</span></span> <span data-ttu-id="a7758-115">Например файл сценария может отображать сведения местные новости, чтение из внешней системы.</span><span class="sxs-lookup"><span data-stu-id="a7758-115">For example, your script file can display local news information read from an external system.</span></span>
    
- <span data-ttu-id="a7758-116">Разрешение пользователям самостоятельно добавлять дополнительные функции для веб-узла с помощью веб-частей из **Коллекции веб-частей**.</span><span class="sxs-lookup"><span data-stu-id="a7758-116">Allow users to add additional functionality to their site by using Web Parts from the **Web Part Gallery**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7758-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a7758-117">Before you begin</span></span>

<span data-ttu-id="a7758-118">Чтобы начать работу, загрузите пример надстройки [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) из проекта [Office 365 для разработчиков шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="a7758-118">To get started, download the [Core.AppScriptPart ](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) sample add-in from the [Office365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreappscriptpart-add-in"></a><span data-ttu-id="a7758-119">С помощью надстройки Core.AppScriptPart</span><span class="sxs-lookup"><span data-stu-id="a7758-119">Using the Core.AppScriptPart add-in</span></span>

<span data-ttu-id="a7758-120">При запуске примера кода и выберите **Запуск сценария**:</span><span class="sxs-lookup"><span data-stu-id="a7758-120">When you run the code sample and choose **Run Scenario**:</span></span>

1. <span data-ttu-id="a7758-121">Выберите **веб-узел**.</span><span class="sxs-lookup"><span data-stu-id="a7758-121">Choose **Back to Site**.</span></span>
    
2. <span data-ttu-id="a7758-122">**Страница**выбора > **Изменить** > **Вставка** > **веб-части**.</span><span class="sxs-lookup"><span data-stu-id="a7758-122">Choose **PAGE** > **Edit** > **INSERT** > **Web Part**.</span></span>
    
3. <span data-ttu-id="a7758-123">В **категории**нажмите кнопку **Добавить в части сценария**и выберите **данные профилей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a7758-123">In **Categories**, choose **Add-in Script Part**, and then choose **User profile information**.</span></span>
    
4. <span data-ttu-id="a7758-124">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7758-124">Choose **Add**.</span></span>
    
5. <span data-ttu-id="a7758-125">В раскрывающемся списке в правом верхнем углу веб-части **сведений профиля пользователя** выберите **Изменить веб-часть**.</span><span class="sxs-lookup"><span data-stu-id="a7758-125">In the drop-down in the upper-right corner of the **User profile information** Web Part, choose **Edit Web Part**.</span></span>
    
6. <span data-ttu-id="a7758-126">Выберите **Изменить ФРАГМЕНТ**.</span><span class="sxs-lookup"><span data-stu-id="a7758-126">Choose **EDIT SNIPPET**.</span></span>
    
7. <span data-ttu-id="a7758-127">Просмотр ** &lt;СЦЕНАРИЙ&gt; ** элемент.</span><span class="sxs-lookup"><span data-stu-id="a7758-127">Review the **&lt;SCRIPT&gt;** element.</span></span>
    
    <span data-ttu-id="a7758-128">Обратите внимание на то, что ссылки атрибут **src** на JavaScript файла на удаленный веб.</span><span class="sxs-lookup"><span data-stu-id="a7758-128">Notice that the  **src** attribute links to a JavaScript file on the remote web.</span></span> <span data-ttu-id="a7758-129">** &lt;СЦЕНАРИЙ&gt; ** элемент задается свойство **содержимого** в Core.AppScriptPartWeb\userprofileinformation.webpart, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a7758-129">The **&lt;SCRIPT&gt;** element is set by the **Content** property in the Core.AppScriptPartWeb\userprofileinformation.webpart, as shown in the following example.</span></span> <span data-ttu-id="a7758-130">Файл JavaScript, связанный с помощью атрибута **src** — Core.AppScriptPartWeb\Scripts\userprofileinformation.js.</span><span class="sxs-lookup"><span data-stu-id="a7758-130">The JavaScript file linked to by the **src** attribute is Core.AppScriptPartWeb\Scripts\userprofileinformation.js.</span></span> <span data-ttu-id="a7758-131">Userprofileinformation.js считывает сведения о текущем пользователе профилей из службы профилей пользователей, а затем отображает эти сведения в веб-части.</span><span class="sxs-lookup"><span data-stu-id="a7758-131">Userprofileinformation.js reads the current user's profile information from the user profile service, and then displays this information in the Web Part.</span></span>
    
     <span data-ttu-id="a7758-132">**Примечание:** Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="a7758-132">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

  ```XML
  <property name="Content" type="string">&amp;lt;script type="text/javascript" src="https://localhost:44361/scripts/userprofileinformation.js"&amp;gt;&amp;lt;/script&amp;gt;
&amp;lt;div id="UserProfileAboutMe"&amp;gt;&amp;lt;div&amp;gt;
  </property>
  ```

8. <span data-ttu-id="a7758-133">Нажмите кнопку **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="a7758-133">Choose **Cancel**.</span></span>
    
9. <span data-ttu-id="a7758-134">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7758-134">Choose **Save**.</span></span>

<span data-ttu-id="a7758-135">**Примечание:** Если изображения профилей пользователей не отображается, откройте OneDrive для бизнеса сайта и затем вернуться на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="a7758-135">**Note:** If your user profile image does not display, open your OneDrive for Business site, and then return to the host web.</span></span>

<span data-ttu-id="a7758-136">В Core.AppScriptPartWeb\Pages\Default.aspx **Запустите сценарий** работает **btnScenario_Click**, который выполняет следующие:</span><span class="sxs-lookup"><span data-stu-id="a7758-136">In Core.AppScriptPartWeb\Pages\Default.aspx, **Run Scenario** runs **btnScenario_Click**, which does the following:</span></span>

1. <span data-ttu-id="a7758-137">Возвращает ссылку на **Коллекцию веб-частей** папки.</span><span class="sxs-lookup"><span data-stu-id="a7758-137">Gets a reference to the **Web Part Gallery** folder.</span></span>
    
2. <span data-ttu-id="a7758-138">Использует [FileCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.aspx) для создания файла userprofileinformation.webpart Отправка из надстройки размещением у поставщика в **Коллекцию веб-частей**.</span><span class="sxs-lookup"><span data-stu-id="a7758-138">Uses [FileCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.aspx) to create the userprofileinformation.webpart file to upload from the provider-hosted add-in to the **Web Part Gallery**.</span></span> <span data-ttu-id="a7758-139">Папка **. Files.Add** метод добавляет файл в **Коллекцию веб-частей**.</span><span class="sxs-lookup"><span data-stu-id="a7758-139">The **folder.Files.Add** method adds the file to the **Web Part Gallery**.</span></span>
    
3. <span data-ttu-id="a7758-140">Извлекает все элементы списка в **Коллекцию веб-частей**, а затем выполняет поиск userprofileinformation.webpart.</span><span class="sxs-lookup"><span data-stu-id="a7758-140">Retrieves all list items in the **Web Part Gallery**, and then searches for userprofileinformation.webpart.</span></span>
    
4. <span data-ttu-id="a7758-141">При обнаружении userprofileinformation.webpart назначает веб-части в пользовательскую группу с именем **Add-in части скрипта**.</span><span class="sxs-lookup"><span data-stu-id="a7758-141">When userprofileinformation.webpart is found, assigns the Web Part to a custom group named **Add-in Script Part**.</span></span>

```C#
protected void btnScenario_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                var folder = clientContext.Web.Lists.GetByTitle("Web Part Gallery").RootFolder;
                clientContext.Load(folder);
                clientContext.ExecuteQuery();

                // Upload the "userprofileinformation.webpart" file.
                using (var stream = System.IO.File.OpenRead(
                                Server.MapPath("~/userprofileinformation.webpart")))
                {
                    FileCreationInformation fileInfo = new FileCreationInformation();
                    fileInfo.ContentStream = stream;
                    fileInfo.Overwrite = true;
                    fileInfo.Url = "userprofileinformation.webpart";
                    File file = folder.Files.Add(fileInfo);
                    clientContext.ExecuteQuery();
                }

                // Update the group that the Web Part belongs to. Start by getting all list items in the Web Part Gallery, and then find the Web Part that was just uploaded.
                var list = clientContext.Web.Lists.GetByTitle("Web Part Gallery");
                CamlQuery camlQuery = CamlQuery.CreateAllItemsQuery(100);
                Microsoft.SharePoint.Client.ListItemCollection items = list.GetItems(camlQuery);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
                foreach (var item in items)
                {
                    // Create new group.
                    if (item["FileLeafRef"].ToString().ToLowerInvariant() == "userprofileinformation.webpart")
                    {
                        item["Group"] = "add-in Script Part";
                        item.Update();
                        clientContext.ExecuteQuery();
                    }
                }

                lblStatus.Text = string.Format("add-in script part has been added to Web Part Gallery. You can find 'User Profile Information' script part under 'App Script Part' group in the <a href='{0}'>host web</a>.", spContext.SPHostUrl.ToString());
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="a7758-142">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a7758-142">Additional resources</span></span>
<span data-ttu-id="a7758-143"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a7758-143"></span></span>

- [<span data-ttu-id="a7758-144">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="a7758-144">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [<span data-ttu-id="a7758-145">Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="a7758-145">Customize your SharePoint site UI by using JavaScript</span></span>](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
