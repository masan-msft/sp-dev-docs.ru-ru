---
title: "Замените типов контента SharePoint и столбцы сайта"
ms.date: 11/03/2017
ms.openlocfilehash: a707962d8a46dbc2f82a3bccd8668613f078d13d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-content-types-and-site-columns"></a><span data-ttu-id="654be-102">Замените типов контента SharePoint и столбцы сайта</span><span class="sxs-lookup"><span data-stu-id="654be-102">Replace SharePoint content types and site columns</span></span>

<span data-ttu-id="654be-103">Замените контента типов и столбцов сайта, добавьте столбцы сайта новые типы контента и замените типов контента новые типы контента SharePoint с помощью CSOM.</span><span class="sxs-lookup"><span data-stu-id="654be-103">Use CSOM to replace SharePoint content types and site columns, add site columns to new content types, and replace the content types with new content types.</span></span>

<span data-ttu-id="654be-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="654be-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="654be-105">Изучение процесса преобразования для использования при замене типов контента и столбцы сайта, добавления столбцов сайта в новые типы контента и затем замена предыдущих типов контента на новые типы контента, с помощью клиентской объектной модели SharePoint (CSOM).</span><span class="sxs-lookup"><span data-stu-id="654be-105">Learn the transformation process to use when replacing content types and site columns, adding site columns to new content types, and then replacing previous content types with new content types using the SharePoint client-side object model (CSOM).</span></span>

<span data-ttu-id="654be-106">**Важные:**  Решения фермы нельзя перенести в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="654be-106">**Important:**  Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="654be-107">Применение методики и кода, описанного в данной статье, можно создать новое решение, которое использует обновленные типов контента и столбцы сайта и обеспечивает аналогичные функциональные возможности для решений фермы или декларативные изолированные решения.</span><span class="sxs-lookup"><span data-stu-id="654be-107">By applying the techniques and code described in this article, you can build a new solution that uses updated content types and site columns and provides similar functionality to your farm solutions or declarative sandbox solutions.</span></span> <span data-ttu-id="654be-108">Затем новое решение можно развернуть в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="654be-108">The new solution can then be deployed to SharePoint Online.</span></span> <span data-ttu-id="654be-109">Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения.</span><span class="sxs-lookup"><span data-stu-id="654be-109">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="654be-110">Например, в этой статье не рассматривается проходить проверку подлинности в Office 365, как реализовать обработку исключений обязательные и т. д.</span><span class="sxs-lookup"><span data-stu-id="654be-110">For example, this article does not discuss how to authenticate to Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="654be-111">Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="654be-111">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span>

## <a name="replace-content-types-and-site-columns"></a><span data-ttu-id="654be-112">Замените типов контента и столбцы сайта</span><span class="sxs-lookup"><span data-stu-id="654be-112">Replace content types and site columns</span></span>

<span data-ttu-id="654be-113">Чтобы заменить типов контента и столбцов сайта с помощью CSOM:</span><span class="sxs-lookup"><span data-stu-id="654be-113">To replace content types and site columns by using CSOM:</span></span>

1. <span data-ttu-id="654be-114">Создание нового типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-114">Create a new content type.</span></span> 
    
2. <span data-ttu-id="654be-115">Создание новых столбцов сайта (также называется полей).</span><span class="sxs-lookup"><span data-stu-id="654be-115">Create new site columns (also referred to as fields).</span></span>
    
3. <span data-ttu-id="654be-116">Добавление новых столбцов сайта для нового типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-116">Add the new site columns to the new content type.</span></span>
    
4. <span data-ttu-id="654be-117">Замените старый ссылки типа контента нового типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-117">Replace old content type references with the new content type.</span></span>
    
<span data-ttu-id="654be-118">В следующем коде **Main** показывает о порядке операций для выполнения для замены типов контента и столбцы сайта с помощью CSOM.</span><span class="sxs-lookup"><span data-stu-id="654be-118">In the following code,  **Main** shows the order of operations to perform to replace content types and site columns by using CSOM.</span></span>

<span data-ttu-id="654be-119">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="654be-119">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
static void Main(string[] args)
{
    using (var clientContext = new ClientContext("http://contoso.sharepoint.com"))
    {

        Web web = clientContext.Web;
        
        CreateContentType(clientContext, web);
        CreateSiteColumn(clientContext, web);
        AddSiteColumnToContentType(clientContext, web);

        // Replace the old content type with the new content type.
        ReplaceContentType(clientContext, web);
    }

}
```

<span data-ttu-id="654be-120">В следующем коде **GetContentTypeByName** Получает тип контента из текущего сайта с:</span><span class="sxs-lookup"><span data-stu-id="654be-120">In the following code,  **GetContentTypeByName** gets a content type from the current site by:</span></span>

1. <span data-ttu-id="654be-121">Для получения [ContentTypeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.aspx)используется свойство [Web.ContentTypes](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.contenttypes.aspx) , которое представляет коллекцию типов контента на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="654be-121">Using the [Web.ContentTypes](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.contenttypes.aspx) property to get a [ContentTypeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.aspx), which is a collection of content types on the current site.</span></span>
    
2. <span data-ttu-id="654be-122">Поиск и затем возвращает типа контента с сайта, с которых отвечают условию в контента введите имя имя существующего типа контента, который отправляется с помощью параметра **name** .</span><span class="sxs-lookup"><span data-stu-id="654be-122">Finding and then returning a content type from the site, by matching the site content type name to the name of the existing content type, which is submitted by the **name** parameter.</span></span>

```C#
private static ContentType GetContentTypeByName(ClientContext cc, Web web, string name)
{
    ContentTypeCollection contentTypes = web.ContentTypes;
    cc.Load(contentTypes);
    cc.ExecuteQuery();
    return contentTypes.FirstOrDefault(o => o.Name == name);
}
```

<span data-ttu-id="654be-123">В следующем коде **CreateContentType** создает новый тип контента с:</span><span class="sxs-lookup"><span data-stu-id="654be-123">In the following code,  **CreateContentType** creates a new content type by:</span></span>

1. <span data-ttu-id="654be-124">Создание константа вызывает **это элемент contentTypeName** для хранения имени типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-124">Creating a constant called  **contentTypeName** to store the name of the content type.</span></span> <span data-ttu-id="654be-125">Имя нового типа контента будет присвоено имя предыдущей типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-125">The name of the new content type will be set to the name of the previous content type.</span></span>
    
2. <span data-ttu-id="654be-126">Вызов **GetContentTypeByName** для поиска соответствующего типа контента на сайте.</span><span class="sxs-lookup"><span data-stu-id="654be-126">Calling  **GetContentTypeByName** to find a matching content type on the site.</span></span>
    
3. <span data-ttu-id="654be-127">Если тип контента уже существует, не требуется никаких действий не требуется, и элемент управления возвращает **Main** при вызове **возврата** .</span><span class="sxs-lookup"><span data-stu-id="654be-127">If the content type already exists, no further action is necessary and control passes back to  **Main** when **return** is called.</span></span> <span data-ttu-id="654be-128">Если тип контента не существует, тип контента задано с помощью объекта [ContentTypeCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecreationinformation.aspx) , называется **newCt**.</span><span class="sxs-lookup"><span data-stu-id="654be-128">If the content type does not exist, content type properties are set using a [ContentTypeCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecreationinformation.aspx) object called **newCt**.</span></span> <span data-ttu-id="654be-129">**NewCt.Id** с помощью идентификатора типа контента базового документа **0x0101**назначается новый идентификатор типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-129">The new content type ID is assigned to **newCt.Id** using the base document content type ID **0x0101**.</span></span> <span data-ttu-id="654be-130">Дополнительные сведения см в [Иерархии типов контента Base](https://msdn.microsoft.com/library/office/ms452896%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="654be-130">For more information, see [Base Content Type Hierarchy](https://msdn.microsoft.com/library/office/ms452896%28v=office.14%29.aspx).</span></span>
    
4. <span data-ttu-id="654be-131">Добавление нового типа контента, с помощью [ContentTypeCollection.Add](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.add.aspx).</span><span class="sxs-lookup"><span data-stu-id="654be-131">Adding the new content type using [ContentTypeCollection.Add](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.add.aspx).</span></span>

```C#
private static void CreateContentType(ClientContext cc, Web web)
{
    // The new content type will be created using this name.
    const string contentTypeName = "ContosoDocumentByCSOM";

    // Determine whether the content type already exists.
    var contentType = GetContentTypeByName(cc, web, contentTypeName);

    // The content type exists already. No further action required.
    if (contentType != null) return;

    // Create the content type using the ContentTypeInformation object.
    ContentTypeCreationInformation newCt = new ContentTypeCreationInformation();
    newCt.Name = "ContosoDocumentByCSOM";

    // Create the new content type based on the out-of-the-box document (0x0101) and assign the ID to the new content type.
    newCt.Id = "0x0101009189AB5D3D2647B580F011DA2F356FB2";

    // Assign the content type to a specific content type group.
    newCt.Group = "Contoso Content Types";

    ContentType myContentType = web.ContentTypes.Add(newCt);
    cc.ExecuteQuery();
}
```

<span data-ttu-id="654be-132">В следующем коде **CreateSiteColumn** создается новый столбец сайта с:</span><span class="sxs-lookup"><span data-stu-id="654be-132">In the following code,  **CreateSiteColumn** creates a new site column by:</span></span>

1. <span data-ttu-id="654be-133">Создание константа, называется **fieldName** для хранения имени поля.</span><span class="sxs-lookup"><span data-stu-id="654be-133">Creating a constant called  **fieldName** to store the name of the field.</span></span> <span data-ttu-id="654be-134">Имя нового поля будет присвоено имя предыдущей поля.</span><span class="sxs-lookup"><span data-stu-id="654be-134">The name of the new field will be set to the name of the previous field.</span></span>
    
2. <span data-ttu-id="654be-135">Получение столбцов сайта, определенных на сайте с помощью свойства [Web.Fields](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.fields.aspx) .</span><span class="sxs-lookup"><span data-stu-id="654be-135">Getting the site columns defined on the site by using the [Web.Fields](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.fields.aspx) property.</span></span>
    
3. <span data-ttu-id="654be-136">Поиск соответствующие поля на сайте, сопоставляя имена полей на сайт, который **fieldName**.</span><span class="sxs-lookup"><span data-stu-id="654be-136">Finding a matching field on the site by matching the field names on the site to  **fieldName**.</span></span> <span data-ttu-id="654be-137">Если это поле уже существует, не требуется никаких действий не требуется, и элемент управления возвращает **Main** при вызове **возврата** .</span><span class="sxs-lookup"><span data-stu-id="654be-137">If the field already exists, no further action is necessary and control passes back to **Main** when **return** is called.</span></span> <span data-ttu-id="654be-138">Если это поле не существует, CAML строка, задающая схема поля назначается **FieldAsXML**и поле создается с помощью [FieldCollection.AddFieldAsXml](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldcollection.addfieldasxml.aspx).</span><span class="sxs-lookup"><span data-stu-id="654be-138">If the field does not exist, a CAML string specifying the field schema is assigned to **FieldAsXML**, and then the field is created using [FieldCollection.AddFieldAsXml](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldcollection.addfieldasxml.aspx).</span></span>

```C#
private static void CreateSiteColumn(ClientContext cc, Web web)
{
    // The new field will be created using this name.
    const string fieldName = "ContosoStringCSOM";

    // Load the list of fields on the site.
    FieldCollection fields = web.Fields;
    cc.Load(fields);
    cc.ExecuteQuery();

    // Check fields on the site for a match.
    var fieldExists = fields.Any(f => f.InternalName == fieldName);

     // The field exists already. No further action required.    
    if (fieldExists) return;

    // Field does not exist, so create the new field.
    string FieldAsXML = @"<Field ID='{CB8E24F6-E1EE-4482-877B-19A51B4BE319}' 
                                Name='" + fieldName + @"' 
                                DisplayName='Contoso String by CSOM' 
                                Type='Text' 
                                Hidden='False' 
                                Group='Contoso Site Columns' 
                                Description='Contoso Text Field' />";
    Field fld = fields.AddFieldAsXml(FieldAsXML, true, AddFieldOptions.DefaultValue);
    cc.ExecuteQuery();
}
```

<span data-ttu-id="654be-139">В следующем коде **AddSiteColumnToContentType** создает соединение между типа содержимого и поля с:</span><span class="sxs-lookup"><span data-stu-id="654be-139">In the following code,  **AddSiteColumnToContentType** creates a connection between the content type and field by:</span></span>

1. <span data-ttu-id="654be-140">Загрузка типа контента, а затем ссылки на поля в этом типе контента с помощью свойства [ContentType.FieldLinks](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.fieldlinks.aspx) .</span><span class="sxs-lookup"><span data-stu-id="654be-140">Loading the content type, and then the field references in that content type by using the [ContentType.FieldLinks](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.fieldlinks.aspx) property.</span></span>
    
2. <span data-ttu-id="654be-141">Загрузка поля.</span><span class="sxs-lookup"><span data-stu-id="654be-141">Loading the field.</span></span>
    
3. <span data-ttu-id="654be-142">Определение, относится ли тип контента в поле с помощью **contentType.FieldLinks.Any (f = > f.Name == fieldName)** в соответствии с на имя поля.</span><span class="sxs-lookup"><span data-stu-id="654be-142">Determining whether the content type refers to the field by using  **contentType.FieldLinks.Any(f => f.Name == fieldName)** to match on the field name.</span></span>
    
4.  <span data-ttu-id="654be-143">Если тип контента уже ссылается на поле, не требуется никаких действий не требуется и управление передается обратно **Main** при вызове **возврата** .</span><span class="sxs-lookup"><span data-stu-id="654be-143">If the content type refers to the field already, no further action is necessary and control passes back to **Main** when **return** is called.</span></span> <span data-ttu-id="654be-144">Если тип контента не ссылается на поле, поле ссылку задано для объекта [FieldLinkCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldlinkcreationinformation.aspx) .</span><span class="sxs-lookup"><span data-stu-id="654be-144">If the content type does not refer to the field, field reference properties are set on a [FieldLinkCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldlinkcreationinformation.aspx) object.</span></span>
    
5. <span data-ttu-id="654be-145">Добавление объекта **FieldLinkCreationInformation** свойство **ContentType.FieldLinks** .</span><span class="sxs-lookup"><span data-stu-id="654be-145">Adding the  **FieldLinkCreationInformation** object to the **ContentType.FieldLinks** property.</span></span>

```C#
private static void AddSiteColumnToContentType(ClientContext cc, Web web)
{
    // The name of the content type. 
    const string contentTypeName = "ContosoDocumentByCSOM";
    // The field name
    const string fieldName = "ContosoStringCSOM";

    // Load the content type.
    var contentType = GetContentTypeByName(cc, web, contentTypeName);
    if (contentType == null) return; // content type was not found

    // Load field references in the content type.
    cc.Load(contentType.FieldLinks);
    cc.ExecuteQuery();

    // Load the new field.
    Field fld = web.Fields.GetByInternalNameOrTitle(fieldName);
    cc.Load(fld);
    cc.ExecuteQuery();

    // Determine whether the content type refers to the field.
    var hasFieldConnected = contentType.FieldLinks.Any(f => f.Name == fieldName);

    // A reference exists already, no further action is required.
    if (hasFieldConnected) return;

    // The reference does not exist, so we have to create the reference.
    FieldLinkCreationInformation link = new FieldLinkCreationInformation();
    link.Field = fld;
    contentType.FieldLinks.Add(link);
    contentType.Update(true);
    cc.ExecuteQuery();
}
```

<span data-ttu-id="654be-146">В следующем коде **ReplaceContentType** проверяет все элементы в все библиотеки для контента, который ссылается на старый тип контента, а затем заменяет эти ссылки нового типа контента (**ContosoDocumentByCSOM**) с:</span><span class="sxs-lookup"><span data-stu-id="654be-146">In the following code,  **ReplaceContentType** checks all items in all libraries for content that references the old content type, and then replaces those references with the new content type (**ContosoDocumentByCSOM**) by:</span></span>

1. <span data-ttu-id="654be-147">Назначение старый идентификатор типа контента на константу.</span><span class="sxs-lookup"><span data-stu-id="654be-147">Assigning the old content type ID to a constant.</span></span>
    
2. <span data-ttu-id="654be-148">Получение нового типа контента с помощью **GetContentTypeByName**.</span><span class="sxs-lookup"><span data-stu-id="654be-148">Getting the new content type by using  **GetContentTypeByName**.</span></span>
    
3. <span data-ttu-id="654be-149">Получение всех списков на сайте с помощью [Web.Lists](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.lists.aspx).</span><span class="sxs-lookup"><span data-stu-id="654be-149">Getting all the lists on the site by using [Web.Lists](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.lists.aspx).</span></span>
    
4. <span data-ttu-id="654be-150">Загрузка всех списков на сайте и все типы контента на каждый список с помощью **«копия». Нагрузки (списков, l = > l.Include (список = > список. Типы содержимого)**.</span><span class="sxs-lookup"><span data-stu-id="654be-150">Loading all the lists on the site, and all content types on each list by using  **cc.Load(lists, l => l.Include(list => list.ContentTypes)**.</span></span>
    
5. <span data-ttu-id="654be-151">Для каждого списка возвращаемых поиск типов контента списка в соответствии с типом контента с старый идентификатор типа контента с помощью списка **. ContentTypes.Any (c = > c.StringId.StartsWith(oldContentTypeId))**.</span><span class="sxs-lookup"><span data-stu-id="654be-151">For each returned list, searching the list's content types to match a content type with the old content type ID by using  **list.ContentTypes.Any(c => c.StringId.StartsWith(oldContentTypeId))**.</span></span> <span data-ttu-id="654be-152">Если совпадение найдено, **listsWithContentType**добавляется в список со старого типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-152">If a match is found, the list with the old content type is added to **listsWithContentType**.</span></span>
    
6. <span data-ttu-id="654be-153">Для каждого списка в **listsWithContentType**:</span><span class="sxs-lookup"><span data-stu-id="654be-153">For each list in  **listsWithContentType**:</span></span>
    
  1. <span data-ttu-id="654be-154">Определение, подключен ли новый тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="654be-154">Determining whether the new content type is attached to the list.</span></span> <span data-ttu-id="654be-155">Если новый тип контента, не подключенного к списку, используйте [ContentTypeCollection.AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) присоединение новый тип контента в список.</span><span class="sxs-lookup"><span data-stu-id="654be-155">If the new content type is not attached to the list, use [ContentTypeCollection.AddExistingContentType ](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) to attach the new content type to the list.</span></span>
    
  2. <span data-ttu-id="654be-156">Получение всех элементов списка в списке.</span><span class="sxs-lookup"><span data-stu-id="654be-156">Getting all list items in the list.</span></span>
    
  3. <span data-ttu-id="654be-157">Для каждого элемента списка начало идентификатор типа контента элемента списка.</span><span class="sxs-lookup"><span data-stu-id="654be-157">For each list item, getting the content type ID of the list item.</span></span> <span data-ttu-id="654be-158">Определить, является ли идентификатор типа контента элемента списка, равное старый идентификатор типа контента.</span><span class="sxs-lookup"><span data-stu-id="654be-158">Determine whether the content type ID of the list item is equal to the old content type ID.</span></span> <span data-ttu-id="654be-159">Если идентификаторы типов контента не равны, перейдите к следующему элементу списка.</span><span class="sxs-lookup"><span data-stu-id="654be-159">If the content type IDs are not equal, skip to the next list item.</span></span> <span data-ttu-id="654be-160">Если равны идентификаторами типов контента, используйте [ContentType.StringId](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.stringid.aspx) для назначения нового идентификатора типа контента для элемента списка.</span><span class="sxs-lookup"><span data-stu-id="654be-160">If the content type IDs are equal, use [ContentType.StringId](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.stringid.aspx) to assign the new content type ID to the list item.</span></span>
    

<span data-ttu-id="654be-161">**Примечание:**  — Это старый тип контента по-прежнему в списке, но больше не используются.</span><span class="sxs-lookup"><span data-stu-id="654be-161">**Note:**  The old content type is still in the list but it is not used anymore.</span></span> <span data-ttu-id="654be-162">Теперь удалите старый тип контента из списков и затем отозвать его. В этой статье описывается, как заменить типов контента документов только.</span><span class="sxs-lookup"><span data-stu-id="654be-162">You can now delete the old content type from the lists, and then retract it.This article describes how to replace document content types only.</span></span> <span data-ttu-id="654be-163">При замене типов контента на макетах страниц, убедитесь, что вы обновите свойство [AssociatedContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.publishing.pagelayout.associatedcontenttype.aspx) на каждый макет страницы в коллекции веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="654be-163">If you are replacing content types on page layouts, ensure you update the [AssociatedContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.publishing.pagelayout.associatedcontenttype.aspx) property on each page layout in the site collection.</span></span>

```C#
private static void ReplaceContentType(ClientContext cc, Web web)
{
    // The old content type. 
    const string oldContentTypeId = "0x010100C32DDAB6381C44868DCD5ADC4A5307D6";
    // The new content type name
    const string newContentTypeName = "ContosoDocumentByCSOM";

    // Get the new content type and lists on the site.
    ContentType newContentType = GetContentTypeByName(cc, web, newContentTypeName);
    ListCollection lists = web.Lists;
    
    // Load the new content type and the content types on all lists on the site. 
    cc.Load(newContentType);
    cc.Load(lists,
            l => l.Include(list => list.ContentTypes));
    cc.ExecuteQuery();
    var listsWithContentType = new List<List>();
    foreach (List list in lists)
    {
        bool hasOldContentType = list.ContentTypes.Any(c => c.StringId.StartsWith(oldContentTypeId));
        if (hasOldContentType)
        {
            listsWithContentType.Add(list);
        }
    }
    foreach (List list in listsWithContentType)
    {
        // Determine whether the new content type is already attached to the list.
        var listHasContentTypeAttached = list.ContentTypes.Any(c => c.Name == newContentTypeName);
        if (!listHasContentTypeAttached)
        {
            // Attach content type to list.
            list.ContentTypes.AddExistingContentType(newContentType);
            cc.ExecuteQuery();
        }
        // Get all list items.
        CamlQuery query = CamlQuery.CreateAllItemsQuery();
        ListItemCollection items = list.GetItems(query);
        cc.Load(items);
        cc.ExecuteQuery();

        // For each list item, determine whether the old content type is used, and then update to the new content type. 
        foreach (ListItem listItem in items)
        {
            // Get the current content type for this list item.
            var currentContentTypeId = listItem["ContentTypeId"] + "";
            var isOldContentTypeAssigned = currentContentTypeId.StartsWith(oldContentTypeId);

            // This item does not use the old content type - skip to next list item.
            if (!isOldContentTypeAssigned) continue;

            // Update the list item content type to the new content type.
            listItem["ContentTypeId"] = newContentType.StringId; // new content type Id;
            listItem.Update();
        }
        // Save all changes.
        cc.ExecuteQuery();
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="654be-164">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="654be-164">Additional resources</span></span>
<span data-ttu-id="654be-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="654be-165"></span></span>

- [<span data-ttu-id="654be-166">Преобразование решений ферм для модели надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="654be-166">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="654be-167">SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="654be-167">SharePoint 2013</span></span>](https://msdn.microsoft.com/library/office/jj162979.aspx)
