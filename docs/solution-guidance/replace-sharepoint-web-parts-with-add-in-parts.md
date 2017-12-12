---
title: "Замените надстройки части веб-частей SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: af8c3eb1d5f314332542247f811b9a25daf0702a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="replace-sharepoint-web-parts-with-add-in-parts"></a><span data-ttu-id="e6762-102">Замените надстройки части веб-частей SharePoint</span><span class="sxs-lookup"><span data-stu-id="e6762-102">Replace SharePoint Web Parts with add-in parts</span></span>

<span data-ttu-id="e6762-103">Используйте процесс преобразования для замены веб-частей с помощью надстройки частей с помощью объектной модели клиента SharePoint (CSOM).</span><span class="sxs-lookup"><span data-stu-id="e6762-103">Use the transformation process to replace Web Parts with add-in parts by using the SharePoint client object model (CSOM).</span></span>

<span data-ttu-id="e6762-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="e6762-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="e6762-105">Процесс преобразования можно использовать для замены части надстройки на страницах веб-частей SharePoint с помощью CSOM поиск и удаление определенного веб-частей, а затем добавляя новые части надстройки.</span><span class="sxs-lookup"><span data-stu-id="e6762-105">You can use the transformation process to replace SharePoint Web Parts with add-in parts on pages by using CSOM to find and remove specific Web Parts, and then adding the new add-in parts.</span></span>

<span data-ttu-id="e6762-106">**Важные:**  Решения фермы нельзя перенести в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e6762-106">**Important:**  Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="e6762-107">Применение методики и кода, описанного в данной статье, можно создать новое решение с аналогичными возможностями, что полностью решений фермы, который можно развернуть в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e6762-107">By applying the techniques and code described in this article, you can build a new solution with similar functionality that your farm solutions provide, which can then be deployed to SharePoint Online.</span></span> <span data-ttu-id="e6762-108">После применения этих методов страницы будут обновлены для использования надстройки части, которые можно перенести в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e6762-108">After you apply these techniques, your pages will be updated to use add-in parts, which can then be migrated to SharePoint Online.</span></span> <span data-ttu-id="e6762-109">Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения.</span><span class="sxs-lookup"><span data-stu-id="e6762-109">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="e6762-110">Например, в этой статье не рассматривается проходить проверку подлинности в Office 365, как реализовать обработку исключений обязательные и т. д.</span><span class="sxs-lookup"><span data-stu-id="e6762-110">For example, this article does not discuss how to authenticate to Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="e6762-111">Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="e6762-111">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e6762-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e6762-112">Before you begin</span></span>

<span data-ttu-id="e6762-113">Перед выполнением действия, описанные в этой статье для замены части надстройки веб-частей, убедитесь, что вы:</span><span class="sxs-lookup"><span data-stu-id="e6762-113">Before performing the steps in this article to replace your Web Parts with add-in parts, make sure that you:</span></span>

- <span data-ttu-id="e6762-114">Используется в среде SharePoint, который настроен для поддержки надстройками SharePoint Online настроена поддержка надстроек. При использовании SharePoint Server 2013 в локальной в статье [Configure среде для SharePoint Add-ins (SharePoint 2013)](https://technet.microsoft.com/library/fp161236%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="e6762-114">Are using a SharePoint environment that is configured to support add-ins. SharePoint Online is configured to support add-ins. If you are using SharePoint Server 2013 on-premises, see [Configure an environment for SharePoint Add-ins (SharePoint 2013)](https://technet.microsoft.com/library/fp161236%28v=office.15%29).</span></span>
    
- <span data-ttu-id="e6762-115">Развернули новую часть надстройки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e6762-115">Have deployed your new add-in part to SharePoint.</span></span>
    
- <span data-ttu-id="e6762-116">Назначен надстройки разрешения на **Полный доступ** в **Web**.</span><span class="sxs-lookup"><span data-stu-id="e6762-116">Have assigned your add-ins  **FullControl** permissions on the **Web**.</span></span> <span data-ttu-id="e6762-117">Дополнительные сведения можно [Добавить разрешений в SharePoint 2013](https://msdn.microsoft.com/library/office/fp142383.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6762-117">For more information, see [Add-in permissions in SharePoint 2013](https://msdn.microsoft.com/library/office/fp142383.aspx).</span></span>

## <a name="replace-web-parts-with-add-in-parts"></a><span data-ttu-id="e6762-118">Замените надстройки части веб-частей</span><span class="sxs-lookup"><span data-stu-id="e6762-118">Replace Web Parts with add-in parts</span></span>

<span data-ttu-id="e6762-119">Замена веб-частей на новые части:</span><span class="sxs-lookup"><span data-stu-id="e6762-119">To replace Web Parts with new add-in parts:</span></span>

1. <span data-ttu-id="e6762-120">Экспорт части новой надстройки.</span><span class="sxs-lookup"><span data-stu-id="e6762-120">Export the new add-in part.</span></span> <span data-ttu-id="e6762-121">Используйте экспортированного часть надстройки для получения определения части надстройки.</span><span class="sxs-lookup"><span data-stu-id="e6762-121">Use the exported add-in part to get the add-in part definition.</span></span> 
    
2. <span data-ttu-id="e6762-122">Поиск всех страниц с веб-частями для замены и нажмите Удалить веб-части.</span><span class="sxs-lookup"><span data-stu-id="e6762-122">Find all pages with Web Parts to be replaced, and then remove the Web Parts.</span></span> 
    
3. <span data-ttu-id="e6762-123">Создание новой надстройки части на странице с помощью надстройки часть определения.</span><span class="sxs-lookup"><span data-stu-id="e6762-123">Create the new add-in part on the page by using the add-in part definition.</span></span> 
    
<span data-ttu-id="e6762-124">Замените части добавить в веб-части с помощью CSOM, необходимо для получения определение части надстройки на экспорт части надстройки.</span><span class="sxs-lookup"><span data-stu-id="e6762-124">To use CSOM to replace a Web Part with an add-in part, you need to get the add-in part definition by exporting the add-in part.</span></span> <span data-ttu-id="e6762-125">Экспорт части надстройки для получения определение части надстройки:</span><span class="sxs-lookup"><span data-stu-id="e6762-125">To export the add-in part to get the add-in part's definition:</span></span>

1. <span data-ttu-id="e6762-126">Откройте сайт SharePoint и выберите **Параметры**или значок шестеренки и выберите команду **Изменить страницу**.</span><span class="sxs-lookup"><span data-stu-id="e6762-126">Open your SharePoint site and choose  **Settings**, or the gear icon, and then choose  **Edit page**.</span></span>
    
2. <span data-ttu-id="e6762-127">На ленте выберите команду **Вставить** > **части надстройки**.</span><span class="sxs-lookup"><span data-stu-id="e6762-127">On the ribbon, choose  **INSERT** > **Add-in Part**.</span></span>
    
3. <span data-ttu-id="e6762-128">Выберите часть надстройки и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e6762-128">Choose your add-in part, and then choose  **Add**.</span></span>
    
4. <span data-ttu-id="e6762-129">Если надстройка часть добавляется на страницу, нажмите стрелку вниз в верхнем правом углу части надстройки и выберите **Изменить веб-часть**.</span><span class="sxs-lookup"><span data-stu-id="e6762-129">When the add-in part is added to your page, choose the down arrow in the top-right corner of the add-in part, and then choose  **Edit Web Part**.</span></span>
    
5. <span data-ttu-id="e6762-130">В **расширенной**в **Режиме экспорта** выберите команду **экспортировать все данные**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e6762-130">In  **Advanced**, in  **Export Mode** choose **Export all data**, and then choose  **OK**.</span></span>
    
6. <span data-ttu-id="e6762-131">Вернувшись на страницу "Правка" с частью надстройки отображается, нажмите кнопку со стрелкой вниз в верхнем правом углу части надстройки и нажмите кнопку **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="e6762-131">When you return to the edit page with your add-in part displayed, choose the down arrow in the top-right corner of the add-in part, and then choose  **Export**.</span></span>
    
7. <span data-ttu-id="e6762-132">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e6762-132">Choose  **Save**.</span></span>
    
8. <span data-ttu-id="e6762-133">После завершения загрузки нажмите кнопку **Открыть папку**.</span><span class="sxs-lookup"><span data-stu-id="e6762-133">After the download completes, choose  **Open folder**.</span></span>
    
9. <span data-ttu-id="e6762-134">Откройте **Блокнот**, а затем выберите **файл** > **Open**.</span><span class="sxs-lookup"><span data-stu-id="e6762-134">Open  **Notepad**, then choose  **File** > **Open**.</span></span>
    
10. <span data-ttu-id="e6762-135">Выберите файл надстройки часть, который был загружен и выберите команду **Открыть** для просмотра определение части надстройки.</span><span class="sxs-lookup"><span data-stu-id="e6762-135">Choose the add-in part file that you downloaded, and then choose  **Open** to view the add-in part definition.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="e6762-136">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="e6762-136">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```XML
<webParts>
  <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
    <metaData>
      <type name="Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name="TitleIconImageUrl" type="string" />
        <property name="Direction" type="direction">NotSet</property>
        <property name="ExportMode" type="exportmode">All</property>
        <property name="HelpUrl" type="string" />
        <property name="Hidden" type="bool">False</property>
        <property name="Description" type="string">WelcomeAppPart Description</property>
        <property name="FeatureId" type="System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">0b846986-3474-4f1a-93cf-b7817ef057f9</property>
        <property name="CatalogIconImageUrl" type="string" />
        <property name="Title" type="string">WelcomeAppPart</property>
        <property name="AllowHide" type="bool">True</property>
        <property name="ProductWebId" type="System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">741c5404-f43e-4f01-acfb-fcd100fc7d24</property>
        <property name="AllowZoneChange" type="bool">True</property>
        <property name="TitleUrl" type="string" />
        <property name="ChromeType" type="chrometype">Default</property>
        <property name="AllowConnect" type="bool">True</property>
        <property name="Width" type="unit" />
        <property name="Height" type="unit" />
        <property name="WebPartName" type="string">WelcomeAppPart</property>
        <property name="HelpMode" type="helpmode">Navigate</property>
        <property name="AllowEdit" type="bool">True</property>
        <property name="AllowMinimize" type="bool">True</property>
        <property name="ProductId" type="System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">0b846986-3474-4f1a-93cf-b7817ef057f8</property>
        <property name="AllowClose" type="bool">True</property>
        <property name="ChromeState" type="chromestate">Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>
```

<span data-ttu-id="e6762-137">Для использования в коде CSOM определение части надстройки:</span><span class="sxs-lookup"><span data-stu-id="e6762-137">To use the add-in part definition in your CSOM code:</span></span>

- <span data-ttu-id="e6762-138">Замените все двойные кавычки ("") пары двойные кавычки ("») в определении части надстройки.</span><span class="sxs-lookup"><span data-stu-id="e6762-138">Replace all double quotes (") with a pair of double quotes ("") in the add-in part definition.</span></span>
    
- <span data-ttu-id="e6762-139">Назначьте определение части добавить в строку, которая будет использоваться в коде CSOM.</span><span class="sxs-lookup"><span data-stu-id="e6762-139">Assign the add-in part definition to a string that will be used in your CSOM code.</span></span>

```C#
private const string appPartXml = @"<webParts>
  <webPart xmlns=""http://schemas.microsoft.com/WebPart/v3"">
    <metaData>
      <type name=""Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"" />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name=""TitleIconImageUrl"" type=""string"" />
        <property name=""Direction"" type=""direction"">NotSet</property>
        <property name=""ExportMode"" type=""exportmode"">All</property>
        <property name=""HelpUrl"" type=""string"" />
        <property name=""Hidden"" type=""bool"">False</property>
        <property name=""Description"" type=""string"">WelcomeAppPart Description</property>
        <property name=""FeatureId"" type=""System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"">0b846986-3474-4f1a-93cf-b7817ef057f9</property>
        <property name=""CatalogIconImageUrl"" type=""string"" />
        <property name=""Title"" type=""string"">WelcomeAppPart Title</property>
        <property name=""AllowHide"" type=""bool"">True</property>
        <property name=""ProductWebId"" type=""System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"">717c00a1-08ea-41a5-a2b7-4c8f9c1ce770</property>
        <property name=""AllowZoneChange"" type=""bool"">True</property>
        <property name=""TitleUrl"" type=""string"" />
        <property name=""ChromeType"" type=""chrometype"">Default</property>
        <property name=""AllowConnect"" type=""bool"">True</property>
        <property name=""Width"" type=""unit"" />
        <property name=""Height"" type=""unit"" />
        <property name=""WebPartName"" type=""string"">WelcomeAppPart</property>
        <property name=""HelpMode"" type=""helpmode"">Navigate</property>
        <property name=""AllowEdit"" type=""bool"">True</property>
        <property name=""AllowMinimize"" type=""bool"">True</property>
        <property name=""ProductId"" type=""System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"">0b846986-3474-4f1a-93cf-b7817ef057f8</property>
        <property name=""AllowClose"" type=""bool"">True</property>
        <property name=""ChromeState"" type=""chromestate"">Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>";
```

<span data-ttu-id="e6762-140">**ReplaceWebPartsWithAppParts** запускает процесс поиска веб-частей необходимо заменить:</span><span class="sxs-lookup"><span data-stu-id="e6762-140">**ReplaceWebPartsWithAppParts** starts the process of finding the Web Parts to be replaced by:</span></span>

1. <span data-ttu-id="e6762-141">Получение некоторые свойства из [Web](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.aspx) , чтобы найти библиотеку **страниц** на сайте.</span><span class="sxs-lookup"><span data-stu-id="e6762-141">Getting some properties from the [Web](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.aspx) to find the **Pages** library on the site.</span></span>
    
2. <span data-ttu-id="e6762-142">В библиотеке **страниц** получение элементов списка и файл, связанный с элементом списка.</span><span class="sxs-lookup"><span data-stu-id="e6762-142">In the  **Pages** library, getting the list items and the file associated with the list item.</span></span>
    
3. <span data-ttu-id="e6762-143">Для каждого элемента списка, возвращенный из библиотеки **страниц** вызов **FindWebPartToReplace**.</span><span class="sxs-lookup"><span data-stu-id="e6762-143">For each list item returned from the  **Pages** library, calling **FindWebPartToReplace**.</span></span>

```C#
protected void ReplaceWebPartsWithAppParts(object sender, EventArgs e)
{
    var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        Web web = clientContext.Web;
        // Get properties from the Web.
        clientContext.Load(web,
                            w => w.ServerRelativeUrl,
                            w => w.AllProperties);
        clientContext.ExecuteQuery();
        // Read the Pages library name from the Web properties.
        var pagesListName = web.AllProperties["__pageslistname"] as string;

        var list = web.Lists.GetByTitle(pagesListName);
        var items = list.GetItems(CamlQuery.CreateAllItemsQuery());
        // Get the file associated with each list item.
        clientContext.Load(items,
                            i => i.Include(
                                    item => item.File));
        clientContext.ExecuteQuery();

        // Iterate through all pages in the Pages list.
        foreach (var item in items)
        {
            FindWebPartForReplacement(item, clientContext, web);
        }
    }
}
```

<span data-ttu-id="e6762-144">**FindWebPartToReplace** находит веб-частей, должна быть заменена новой части надстройки с:</span><span class="sxs-lookup"><span data-stu-id="e6762-144">**FindWebPartToReplace** finds Web Parts that should be replaced with the new add-in part by:</span></span>

1. <span data-ttu-id="e6762-145">Настройка **страницы** в файл, связанный с элементом списка, возвращенный из библиотеки **страниц** .</span><span class="sxs-lookup"><span data-stu-id="e6762-145">Setting  **page** to the file associated with the list item returned from the **Pages** library.</span></span>
    
2. <span data-ttu-id="e6762-146">Чтобы найти все веб-части на определенную страницу с помощью [LimitedWebPartManager](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e6762-146">Using [LimitedWebPartManager](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.aspx) to find all Web Parts on a specific page.</span></span> <span data-ttu-id="e6762-147">Название каждой веб-части также возвращается в лямбда-выражения.</span><span class="sxs-lookup"><span data-stu-id="e6762-147">The title of each Web Part is also returned in the lambda expression.</span></span>
    
3. <span data-ttu-id="e6762-148">Для каждого веб-части в диспетчере веб-части [веб-части](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.webparts.aspx) свойство, определение ли замена заголовка веб-части и переменной **oldWebPartTitle** , которая задано значение заголовка веб-части, совпадают.</span><span class="sxs-lookup"><span data-stu-id="e6762-148">For each Web Part in the Web Part manager's [WebParts](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.webparts.aspx) property, determining whether the Web Part's title and the **oldWebPartTitle** variable, which is set to the title of the Web Part you are replacing, are equal.</span></span> <span data-ttu-id="e6762-149">Если заголовок веб-части и **oldWebPartTitle** равны, позвонить **ReplaceWebPart**; в противном случае перейдите к следующей итерации цикла **foreach** .</span><span class="sxs-lookup"><span data-stu-id="e6762-149">If the Web Part title and **oldWebPartTitle** are equal, call **ReplaceWebPart**; otherwise continue with the next iteration of the **foreach** loop.</span></span>

```C#
private static void FindWebPartToReplace(ListItem item, ClientContext clientContext, Web web)
{
    File page = item.File;
    // Requires Full Control permissions on the Web.
    LimitedWebPartManager webPartManager = page.GetLimitedWebPartManager(PersonalizationScope.Shared);
    clientContext.Load(webPartManager,
                        wpm => wpm.WebParts,
                        wpm => wpm.WebParts.Include(
                                            wp => wp.WebPart.Title));
    clientContext.ExecuteQuery();

    foreach (var oldWebPartDefinition in webPartManager.WebParts)
    {
        var oldWebPart = oldWebPartDefinition.WebPart;
        // Modify the Web Part if we find an old Web Part with the same title.
        if (oldWebPart.Title != oldWebPartTitle) continue;

        ReplaceWebPart(web, item, webPartManager, oldWebPartDefinition, clientContext, page);
    }
}
```

<span data-ttu-id="e6762-150">**ReplaceWebPart** заменяет новой веб-части с:</span><span class="sxs-lookup"><span data-stu-id="e6762-150">**ReplaceWebPart** replaces the new Web Part by:</span></span>

1. <span data-ttu-id="e6762-151">С помощью [LimitedWebPartManager.ImportWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.importwebpart.aspx) для преобразования XML-строка в **appPartXml** в [WebPartDefinition](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6762-151">Using [LimitedWebPartManager.ImportWebPart ](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.importwebpart.aspx) to convert the XML string in **appPartXml** into a [WebPartDefinition](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx).</span></span>
    
2. <span data-ttu-id="e6762-152">Добавление веб-части на страницу в определенной зоне веб-частей с помощью [LimitedWebPartManager.AddWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.addwebpart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e6762-152">Using [LimitedWebPartManager.AddWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.addwebpart.aspx) to add a Web Part to a page in a specific Web Part zone.</span></span> <span data-ttu-id="e6762-153">Убедитесь, передайте **КодЗоны** **AddWebPart**, в противном случае возникает исключение при запуске **ExecuteQuery** .</span><span class="sxs-lookup"><span data-stu-id="e6762-153">Ensure you pass the **zoneId** to **AddWebPart**, otherwise an exception will be thrown when  **ExecuteQuery** runs.</span></span>
    
3. <span data-ttu-id="e6762-154">Чтобы удалить старые веб-часть со страницы с помощью [WebPartDefinition.DeleteWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.deletewebpart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e6762-154">Using [WebPartDefinition.DeleteWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.deletewebpart.aspx) to delete the old Web Part from the page.</span></span>

```C#
private static void ReplaceWebPart(Web web, ListItem item, LimitedWebPartManager webPartManager,
      WebPartDefinition oldWebPartDefinition, ClientContext clientContext, File page)
  {
     
      // Create a Web Part definition using the XML string.
      var definition = webPartManager.ImportWebPart(appPartXml);
      webPartManager.AddWebPart(definition.WebPart, "RightColumn", 0);

      // Delete the old Web Part from the page.
      oldWebPartDefinition.DeleteWebPart();
      clientContext.Load(page,
                          p => p.CheckOutType,
                          p => p.Level);

      clientContext.ExecuteQuery();
     
  }
```

## <a name="see-also"></a><span data-ttu-id="e6762-155">См. также</span><span class="sxs-lookup"><span data-stu-id="e6762-155">See also</span></span>
<span data-ttu-id="e6762-156"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e6762-156"></span></span>

- [<span data-ttu-id="e6762-157">Преобразование решений ферм для модели надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e6762-157">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="e6762-158">Provisioning.Pages</span><span class="sxs-lookup"><span data-stu-id="e6762-158">Provisioning.Pages</span></span>](https://github.com/SharePoint/PnP/tree/master/Scenarios/Provisioning.Pages)
