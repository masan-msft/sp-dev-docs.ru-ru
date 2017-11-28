---
title: "Замените типов контента SharePoint и столбцы сайта"
ms.date: 11/03/2017
ms.openlocfilehash: a707962d8a46dbc2f82a3bccd8668613f078d13d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-content-types-and-site-columns"></a>Замените типов контента SharePoint и столбцы сайта

Замените контента типов и столбцов сайта, добавьте столбцы сайта новые типы контента и замените типов контента новые типы контента SharePoint с помощью CSOM.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Изучение процесса преобразования для использования при замене типов контента и столбцы сайта, добавления столбцов сайта в новые типы контента и затем замена предыдущих типов контента на новые типы контента, с помощью клиентской объектной модели SharePoint (CSOM).

**Важные:**  Решения фермы нельзя перенести в SharePoint Online. Применение методики и кода, описанного в данной статье, можно создать новое решение, которое использует обновленные типов контента и столбцы сайта и обеспечивает аналогичные функциональные возможности для решений фермы или декларативные изолированные решения. Затем новое решение можно развернуть в SharePoint Online. Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения. Например, в этой статье не рассматривается проходить проверку подлинности в Office 365, как реализовать обработку исключений обязательные и т. д. Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).

## <a name="replace-content-types-and-site-columns"></a>Замените типов контента и столбцы сайта

Чтобы заменить типов контента и столбцов сайта с помощью CSOM:

1. Создание нового типа контента. 
    
2. Создание новых столбцов сайта (также называется полей).
    
3. Добавление новых столбцов сайта для нового типа контента.
    
4. Замените старый ссылки типа контента нового типа контента.
    
В следующем коде **Main** показывает о порядке операций для выполнения для замены типов контента и столбцы сайта с помощью CSOM.

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

В следующем коде **GetContentTypeByName** Получает тип контента из текущего сайта с:

1. Для получения [ContentTypeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.aspx)используется свойство [Web.ContentTypes](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.contenttypes.aspx) , которое представляет коллекцию типов контента на текущем сайте.
    
2. Поиск и затем возвращает типа контента с сайта, с которых отвечают условию в контента введите имя имя существующего типа контента, который отправляется с помощью параметра **name** .

```C#
private static ContentType GetContentTypeByName(ClientContext cc, Web web, string name)
{
    ContentTypeCollection contentTypes = web.ContentTypes;
    cc.Load(contentTypes);
    cc.ExecuteQuery();
    return contentTypes.FirstOrDefault(o => o.Name == name);
}
```

В следующем коде **CreateContentType** создает новый тип контента с:

1. Создание константа вызывает **это элемент contentTypeName** для хранения имени типа контента. Имя нового типа контента будет присвоено имя предыдущей типа контента.
    
2. Вызов **GetContentTypeByName** для поиска соответствующего типа контента на сайте.
    
3. Если тип контента уже существует, не требуется никаких действий не требуется, и элемент управления возвращает **Main** при вызове **возврата** . Если тип контента не существует, тип контента задано с помощью объекта [ContentTypeCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecreationinformation.aspx) , называется **newCt**. **NewCt.Id** с помощью идентификатора типа контента базового документа **0x0101**назначается новый идентификатор типа контента. Дополнительные сведения см в [Иерархии типов контента Base](https://msdn.microsoft.com/library/office/ms452896%28v=office.14%29.aspx).
    
4. Добавление нового типа контента, с помощью [ContentTypeCollection.Add](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.add.aspx).

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

В следующем коде **CreateSiteColumn** создается новый столбец сайта с:

1. Создание константа, называется **fieldName** для хранения имени поля. Имя нового поля будет присвоено имя предыдущей поля.
    
2. Получение столбцов сайта, определенных на сайте с помощью свойства [Web.Fields](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.fields.aspx) .
    
3. Поиск соответствующие поля на сайте, сопоставляя имена полей на сайт, который **fieldName**. Если это поле уже существует, не требуется никаких действий не требуется, и элемент управления возвращает **Main** при вызове **возврата** . Если это поле не существует, CAML строка, задающая схема поля назначается **FieldAsXML**и поле создается с помощью [FieldCollection.AddFieldAsXml](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldcollection.addfieldasxml.aspx).

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

В следующем коде **AddSiteColumnToContentType** создает соединение между типа содержимого и поля с:

1. Загрузка типа контента, а затем ссылки на поля в этом типе контента с помощью свойства [ContentType.FieldLinks](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.fieldlinks.aspx) .
    
2. Загрузка поля.
    
3. Определение, относится ли тип контента в поле с помощью **contentType.FieldLinks.Any (f = > f.Name == fieldName)** в соответствии с на имя поля.
    
4.  Если тип контента уже ссылается на поле, не требуется никаких действий не требуется и управление передается обратно **Main** при вызове **возврата** . Если тип контента не ссылается на поле, поле ссылку задано для объекта [FieldLinkCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.fieldlinkcreationinformation.aspx) .
    
5. Добавление объекта **FieldLinkCreationInformation** свойство **ContentType.FieldLinks** .

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

В следующем коде **ReplaceContentType** проверяет все элементы в все библиотеки для контента, который ссылается на старый тип контента, а затем заменяет эти ссылки нового типа контента (**ContosoDocumentByCSOM**) с:

1. Назначение старый идентификатор типа контента на константу.
    
2. Получение нового типа контента с помощью **GetContentTypeByName**.
    
3. Получение всех списков на сайте с помощью [Web.Lists](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.web.lists.aspx).
    
4. Загрузка всех списков на сайте и все типы контента на каждый список с помощью **«копия». Нагрузки (списков, l = > l.Include (список = > список. Типы содержимого)**.
    
5. Для каждого списка возвращаемых поиск типов контента списка в соответствии с типом контента с старый идентификатор типа контента с помощью списка **. ContentTypes.Any (c = > c.StringId.StartsWith(oldContentTypeId))**. Если совпадение найдено, **listsWithContentType**добавляется в список со старого типа контента.
    
6. Для каждого списка в **listsWithContentType**:
    
  1. Определение, подключен ли новый тип контента в список. Если новый тип контента, не подключенного к списку, используйте [ContentTypeCollection.AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) присоединение новый тип контента в список.
    
  2. Получение всех элементов списка в списке.
    
  3. Для каждого элемента списка начало идентификатор типа контента элемента списка. Определить, является ли идентификатор типа контента элемента списка, равное старый идентификатор типа контента. Если идентификаторы типов контента не равны, перейдите к следующему элементу списка. Если равны идентификаторами типов контента, используйте [ContentType.StringId](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.stringid.aspx) для назначения нового идентификатора типа контента для элемента списка.
    

**Примечание:**  — Это старый тип контента по-прежнему в списке, но больше не используются. Теперь удалите старый тип контента из списков и затем отозвать его. В этой статье описывается, как заменить типов контента документов только. При замене типов контента на макетах страниц, убедитесь, что вы обновите свойство [AssociatedContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.publishing.pagelayout.associatedcontenttype.aspx) на каждый макет страницы в коллекции веб-сайтов.

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

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Преобразование решений ферм для модели надстроек SharePoint](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [SharePoint 2013](https://msdn.microsoft.com/library/office/jj162979.aspx)
