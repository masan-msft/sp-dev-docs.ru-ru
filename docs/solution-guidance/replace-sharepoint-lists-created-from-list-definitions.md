---
title: "Замените списки SharePoint, созданный из определений списков"
ms.date: 11/03/2017
ms.openlocfilehash: 99caef124d7b5162839dff092d7760f7ec9dbdf3
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-lists-created-from-list-definitions"></a>Замените списки SharePoint, созданный из определений списков
Замените списков и библиотек, которые были созданы с помощью определения списка в SharePoint. 

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Если определений списков используется для создания списков в решении фермы, узнайте, как преобразовать их в новые решения, обеспечивающие аналогичную функциональность, с помощью клиентской объектной модели (CSOM). В этой статье описывается использование клиентской объектной модели (CSOM) для:

- Поиск списков и библиотек, которые были созданы с помощью определения списка.
    
- Создайте и настройте новые списки.
    
- Добавление и удаление представлений из списков.
    
- Перенос контента из исходного списка в новый список.

**Важно!** <p>Решения фермы нельзя перенести в SharePoint Online. Применение методики и кода, описанного в данной статье, можно создать новое решение с аналогичными возможностями, что полностью решений фермы, который можно развернуть в SharePoint Online. При использовании подхода к преобразования на месте может потребоваться развертывание нового решения в SharePoint Online. При использовании две или переноса содержимого подход средств сторонних производителей могут создать списки. Для получения дополнительных сведений см [преобразования подходов для развертывания новой надстройки SharePoint](https://msdn.microsoft.com/library/dn986827.aspx#sectionSection1). Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения. Например, в этой статье не рассматривается проходить проверку подлинности в Office 365, как реализовать обработку исключений обязательные и т. д. Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).</p><p>Используйте методы, описанные в этой статье описывается обновление только несколько списков за раз. Кроме того при поиске списков, чтобы обновить не следует фильтровать списков по типу списка.</p>

## <a name="before-you-begin"></a>Перед началом работы

В идеальном варианте следует ознакомиться существующих решений фермы, узнайте о методах, описанных в этой статье и затем планирование применение этих методов для существующих решений фермы. Если не знакомы с решениями фермы или нет существующее решение фермы для работы с могут быть полезны позволяет:

1. Загрузите [решение Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet). Просмотрите [Анализ исходное состояние сайта и библиотеки для замены](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-2%20Replacing%20Lists%20Created%20from%20Custom%20Templates/Lab.md#examine-the-initial-state-of-the-site-and-library-for-replacement) для получения быстрого представление о, как списки созданные декларативно с помощью определения списка.
    
    **Примечание:**  В Contoso.Intranet в файле elements.xml для SP\ListTemplate\LTContosoLibrary идентификатор для пользовательский шаблон списка — 10003. Это будет использоваться для идентификации шаблона, который использовался для создания списка. Также просмотрите параметры конфигурации и представления, которые определены в списке.

2. Ознакомьтесь с решениями фермы. Для получения дополнительных сведений см. [Обзор архитектуры SharePoint 2010](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) и [создания решений фермы в SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).
    
## <a name="replace-lists-created-from-list-definitions"></a>Замените списков, созданных из определений списков

Чтобы заменить списков, созданных из определений списков:

1. Поиск списков, которые были созданы с помощью определенного базового шаблона.
    
2. Создание нового списка с помощью определения списка ожидания введите. 
    
3. Настройте параметры списка.
    
4. Задавать типы контента на основе типов контента, которые были установлены в исходном списке нового списка.
    
5. (Необязательно) Добавьте представления. 
    
6. (Необязательно) Удаление представлений.
    
7. Перенос контента из исходного списка в новый список.
    
В следующем примере кода метод показано, как найти списков, которые были созданы с помощью определенного базового шаблона. Этот метод:

1. Использует [ClientContext](https://msdn.microsoft.com/library/microsoft.sharepoint.client.clientcontext.aspx) для получения всех списков на текущем сайте, с помощью [Web.Lists](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.lists.aspx). Инструкции Include используется в лямбда-выражения для возврата коллекции списков. Возвращенный списки должны иметь значения свойств, заданные для [BaseTemplate](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetemplate.aspx), [BaseType](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetype.aspx)и [Название](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.title.aspx).
    
2. Для каждого списка в коллекции возвращенные списков Если **List.BaseTemplate** равен 10003, добавляет списка коллекцию списков, чтобы заменить, называется **listsToReplace**. Имейте в виду, что 10003 был идентификатор шаблона настраиваемый список, которые мы reviewed в образце Contoso.Intranet.

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
static void Main(string[] args)
{
    using (var clientContext = new ClientContext("http://w15-sp/sites/ftclab"))
    {
        Web web = clientContext.Web;
        ListCollection listCollection = web.Lists;
        clientContext.Load(listCollection,
                            l => l.Include(list => list.BaseTemplate,
                                            list => list.BaseType,
                                            list => list.Title));
        clientContext.ExecuteQuery();
        var listsToReplace = new List<List>();
        foreach (List list in listCollection)
        {
            // 10003 is the custom list template ID of the list template you're replacing.
            if (list.BaseTemplate == 10003)
            {
                listsToReplace.Add(list);
            }
        }
        foreach (List list in listsToReplace)
        {
            ReplaceList(clientContext, listCollection, list);
        }
    }
}
```

**Важные:**  В предыдущем примере кода сначала итерации по ListCollection, чтобы выбрать, какие списки необходимо изменить, а затем вызвать ReplaceList, которая начинается изменения списков. Этот шаблон является обязательным, так как изменение контента семейства сайтов при итерации по коллекции вызовет исключение.

После определения списка, который следует заменить **ReplaceList** показывает о порядке операций для выполнения для замены в списке.

```C#
private static void ReplaceList(ClientContext clientContext, ListCollection listCollection, List listToBeReplaced)
{
    var newList = CreateReplacementList(clientContext, listCollection, listToBeReplaced);

    SetListSettings(clientContext, listToBeReplaced, newList);

    SetContentTypes(clientContext, listToBeReplaced, newList);

    AddViews(clientContext, listToBeReplaced, newList);

    RemoveViews(clientContext, listToBeReplaced, newList);

    MigrateContent(clientContext, listToBeReplaced, newList);
}
```

Чтобы создать новый список, **CreateReplacementList** использует [ListCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.listcreationinformation.aspx). Заголовок нового списка имеет значение заголовка существующий список с надстройкой к нему. Перечисление [ListTemplateType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.listtemplatetype.aspx) используется для установки типа шаблонов списков в библиотеке документов. При создании списка на основе типа другой шаблон убедитесь, что используется правильный шаблон тип. Например при создании календарного списка используйте **ListTemplateType.Events** вместо **ListTemplateType.DocumentLibrary**.

```C#
private static List CreateReplacementList(ClientContext clientContext, ListCollection lists,List listToBeReplaced)
{
    var creationInformation = new ListCreationInformation
    {
        Title = listToBeReplaced.Title + "add-in",
        TemplateType = (int) ListTemplateType.DocumentLibrary,
    };
    List newList = lists.Add(creationInformation);
    clientContext.ExecuteQuery();
    return newList;
}
```

**SetListSettings** применяются параметры исходного списка новый список с:

1. Получение различных параметров списка из исходного списка.
    
2. Применить параметр списка из исходного списка в новый список.

```C#
private static void SetListSettings(ClientContext clientContext, List listToBeReplaced, List newList)
{
    clientContext.Load(listToBeReplaced, 
                        l => l.EnableVersioning, 
                        l => l.EnableModeration, 
                        l => l.EnableMinorVersions,
                        l => l.DraftVersionVisibility );
    clientContext.ExecuteQuery();
    newList.EnableVersioning = listToBeReplaced.EnableVersioning;
    newList.EnableModeration = listToBeReplaced.EnableModeration;
    newList.EnableMinorVersions= listToBeReplaced.EnableMinorVersions;
    newList.DraftVersionVisibility = listToBeReplaced.DraftVersionVisibility;
    newList.Update();
    clientContext.ExecuteQuery();
}
```

**Примечание:**  На основе требований, параметры списка исходное списков может отличаться. Проверьте параметры списка и измените **SetListSettings** , чтобы убедиться, что для новых списков, применяются первоначальные параметры списка.

**SetContentTypes** задает типы контента на новый список с:

1. Получение сведений о типе контента из исходного списка.
    
2. Получение сведений о типе контента из нового списка.
    
3. Определение, позволяет ли исходный список типов контента. Если исходный список не включает типы контента, **SetContentTypes** завершает работу. Если исходный список включены типы контента, а затем **SetContentTypes** позволяет типов контента на новый список с помощью **newList.ContentTypesEnabled = true**.
    
4. Для каждого типа контента, в исходном списке, поиск по контенту типы в новом списке, чтобы найти подходящий тип на основе имени типа контента с помощью **newList.ContentTypes.Any контента (компьютерной телефонии = > компьютерной телефонии. Имя == contentType.Name)**. Если тип контента не новый список, он добавляется в список.
    
5. Загрузка **newList** еще раз, так как [AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) , могут измениться типов контента.
    
6. Для каждого типа контента в **newList**определение, соответствует ли тип контента типа контента в исходном списке, основанный на [ContentType.Name](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.name.aspx) с помощью **listToBeReplaced.ContentTypes.Any (компьютерной телефонии = > компьютерной телефонии. Имя == contentType.Name)**. Если совпадение не найдено, тип контента добавляется к **contentTypesToDelete** к удалению из нового списка.
    
7. Удаление типа контента, вызвав [ContentType.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.deleteobject.aspx).

**Примечание:**  Если вы используете подхода к преобразования на месте и типов содержимого были развернуты декларативно с помощью структура компонентов, необходимо: 

 1. Создание новых типов контента.

 2. Задайте тип контента для элементов списка при переносе контента из исходного списка в новый список в MigrateContent.


```C#
private static void SetContentTypes(ClientContext clientContext, List listToBeReplaced, List newList)
{
    clientContext.Load(listToBeReplaced,
                        l => l.ContentTypesEnabled,
                        l => l.ContentTypes);
    clientContext.Load(newList,
                        l => l.ContentTypesEnabled,
                        l => l.ContentTypes);
    clientContext.ExecuteQuery();

    // If the original list doesn't use content types, do not proceed any further.
    if (!listToBeReplaced.ContentTypesEnabled) return;

    newList.ContentTypesEnabled = true;
    newList.Update();
    clientContext.ExecuteQuery();
    foreach (var contentType in listToBeReplaced.ContentTypes)
    {
        if (!newList.ContentTypes.Any(ct => ct.Name == contentType.Name))
        {
            // Current content type needs to be added to the new list. Note that the content type is added to the list, not the site.           
            newList.ContentTypes.AddExistingContentType(contentType.Parent);
            newList.Update();
            clientContext.ExecuteQuery();
        }
    }
    // Reload the content types on newList because they might have changed when AddExistingContentType was called. 
    clientContext.Load(newList, l => l.ContentTypes);
    clientContext.ExecuteQuery();
    // Remove any content types that are not needed.
    var contentTypesToDelete = new List<ContentType>();
    foreach (var contentType in newList.ContentTypes)
    {
        if (!listToBeReplaced.ContentTypes.Any(ct => ct.Name == contentType.Name))
        {
            // Current content type needs to be removed from new list.
            contentTypesToDelete.Add(contentType);
        }
    }
    foreach (var contentType in contentTypesToDelete)
    {
        contentType.DeleteObject();
    }
    newList.Update();
    clientContext.ExecuteQuery();
}
```

**Примечание:**  На этом этапе новый список может принимать контент из исходного списка. Также при необходимости можно добавлять и удалять представлений. 

Пользователи могут добавлять или удалять представления, определенные для списка, в соответствии с их потребностям. По этой причине может потребоваться добавление или удаление представления нового списка.  **AddViews** добавляет представления из исходного списка в новый список с:

1. Получение всех представлений в исходном списке с помощью [List.Views](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.views.aspx) .
    
2. Загрузить различные свойства представления в коллекции **представлений** с помощью лямбда-выражения.
    
3. Для каждого представления в исходном списке, создание представления с помощью [ViewCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewcreationinformation.aspx). Различные свойства устанавливаются на новое представление на основе свойств представления из исходного представления. Вспомогательный метод **GetViewType** вызывается для определения [ViewType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewtype.aspx) представления. Новое представление добавляется в список представлений, называется **viewsToCreate**.
    
4. Добавление представлений в коллекции **List.Views** с помощью метода **Add** в коллекции представлений списка.

```C#
private static void AddViews(ClientContext clientContext, List listToBeReplaced, List newList)
{
    ViewCollection views = listToBeReplaced.Views;
    clientContext.Load(views,
                        v => v.Include(view => view.Paged,
                            view => view.PersonalView,
                            view => view.ViewQuery,
                            view => view.Title,
                            view => view.RowLimit,
                            view => view.DefaultView,
                            view => view.ViewFields,
                            view => view.ViewType));
    clientContext.ExecuteQuery();

    // Build a list of views which exist on the original list only.
    var viewsToCreate = new List<ViewCreationInformation>();
    foreach (View view in listToBeReplaced.Views)
    {
      var createInfo = new ViewCreationInformation
      {
          Paged = view.Paged,
          PersonalView = view.PersonalView,
          Query = view.ViewQuery,
          Title = view.Title,
          RowLimit = view.RowLimit,
          SetAsDefaultView = view.DefaultView,
          ViewFields = view.ViewFields.ToArray(),
          ViewTypeKind = GetViewType(view.ViewType),
      };
      viewsToCreate.Add(createInfo);
    }
    
    foreach (ViewCreationInformation newView in viewsToCreate)
    {
        newList.Views.Add(newView);
    }
    newList.Update();
}

private static ViewType GetViewType(string viewType)
{
    switch (viewType)
    {
        case "HTML":
            return ViewType.Html;
        case "GRID":
            return ViewType.Grid;
        case "CALENDAR":
            return ViewType.Calendar;
        case "RECURRENCE":
            return ViewType.Recurrence;
        case "CHART":
            return ViewType.Chart;
        case "GANTT":
            return ViewType.Gantt;
        default:
            return ViewType.None;
    }
}
```

В следующем коде **RemoveViews** удаляет представления из новый список с:

1. Получение представлений списка на новый список с помощью свойства **List.Views** .
    
2. Для каждого представления в новом списке, определение ли это представление не существует в исходном списке, сопоставляя на просмотр заголовка с помощью **! listToBeReplaced.Views.Any (v = > v.Title == представления. Название**. Если представление в новом списке не имеет соответствующего представления в исходном списке, добавьте представление **viewsToRemove**.
    
3. Удаление всех представлений в **viewsToRemove** с помощью [View.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.view.deleteobject.aspx).
    
```C#
private static void RemoveViews(ClientContext clientContext, List listToBeReplaced, List newList)
{
    // Get the list of views on the new list.
    clientContext.Load(newList, l => l.Views);
    clientContext.ExecuteQuery();

    var viewsToRemove = new List<View>();
    foreach (View view in newList.Views)
    {
        if (!listToBeReplaced.Views.Any(v => v.Title == view.Title))
        {
            // If there is no matching view in the source list, add the view to the list of views to be deleted.
            viewsToRemove.Add(view);
        }
    }
    foreach (View view in viewsToRemove)
    {
        view.DeleteObject();
    }
    newList.Update();
    clientContext.ExecuteQuery();
}
```

**MigrateContent** переносит контент из исходного списка в новый список с:

1. Получение назначения для копирования файлов или в корневую папку нового списка с помощью [List.RootFolder](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.rootfolder.aspx). URL-адрес относительно сервера конечную папку списка извлекаются с помощью [Folder.ServerRelativeUrl](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.folder.serverrelativeurl.aspx).
    
2. Получение исходных файлов или в корневую папку исходного списка с помощью **List.RootFolder**. Относительный к серверу URL-адрес папки списка и все файлы в корневой папке источника загружаются с помощью объекта **clientContext** .
    
3. Для каждого файла в источнике создается **новый URL-адрес**, который хранит новый URL-адрес файла. **новый URL-адрес** создается путем замены в корневой папке источника с корневой папки назначения.
    
4. Скопируйте файл с URL-адресом конечной корневой папки с помощью [File.CopyTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.copyto.aspx) . Кроме того можно использовать метод [File.MoveTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.moveto.aspx) для перемещения URL-адрес конечного файла.
    
**Примечание:**  Следующий код возвращает все элементы списка. В рабочей среде рассмотрите возможность оптимизации следующий код, реализовав цикла и перенос небольшое количество элементов списка с помощью нескольких итераций.

```C#
private static void MigrateContent(ClientContext clientContext, List listToBeReplaced, List newList)
{
    ListItemCollection items = listToBeReplaced.GetItems(CamlQuery.CreateAllItemsQuery());
    Folder destination = newList.RootFolder;
    Folder source = listToBeReplaced.RootFolder;
    clientContext.Load(destination,
                        d => d.ServerRelativeUrl);
    clientContext.Load(source,
                        s => s.Files,
                        s => s.ServerRelativeUrl);
    clientContext.Load(items,
                        i => i.IncludeWithDefaultProperties(item => item.File));
    clientContext.ExecuteQuery();


    foreach (File file in source.Files)
    {
        string newUrl = file.ServerRelativeUrl.Replace(source.ServerRelativeUrl, destination.ServerRelativeUrl);
          file.CopyTo(newUrl, true);
          //file.MoveTo(newUrl, MoveOperations.Overwrite);
    }
    clientContext.ExecuteQuery();
}
```

**Примечание:**  Предыдущего кода показано, как миграция файлов, хранящихся в корневую папку списка. Если список вложенных папок, необходимо добавить дополнительный код для перемещения вложенных папках и их содержимое. Если в вашем списке используется рабочих процессов, чтобы сопоставить рабочий процесс для нового списка необходим дополнительный код.

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Преобразование решений ферм для модели надстроек SharePoint](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [SharePoint 2013](https://msdn.microsoft.com/library/office/jj162979.aspx)
