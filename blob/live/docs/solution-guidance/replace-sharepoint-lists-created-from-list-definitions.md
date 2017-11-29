---
title: "Замените списки SharePoint, созданный из определений списков"
ms.date: 11/03/2017
ms.openlocfilehash: 99caef124d7b5162839dff092d7760f7ec9dbdf3
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="replace-sharepoint-lists-created-from-list-definitions"></a><span data-ttu-id="ca022-102">Замените списки SharePoint, созданный из определений списков</span><span class="sxs-lookup"><span data-stu-id="ca022-102">Replace SharePoint lists created from list definitions</span></span>
<span data-ttu-id="ca022-103">Замените списков и библиотек, которые были созданы с помощью определения списка в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ca022-103">Replace lists and libraries that were created by using list definitions in SharePoint.</span></span> 

<span data-ttu-id="ca022-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="ca022-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="ca022-105">Если определений списков используется для создания списков в решении фермы, узнайте, как преобразовать их в новые решения, обеспечивающие аналогичную функциональность, с помощью клиентской объектной модели (CSOM).</span><span class="sxs-lookup"><span data-stu-id="ca022-105">If you used list definitions to create lists in your farm solution, learn how to transform them into new solutions that provide similar functionality using the client object model (CSOM).</span></span> <span data-ttu-id="ca022-106">В этой статье описывается использование клиентской объектной модели (CSOM) для:</span><span class="sxs-lookup"><span data-stu-id="ca022-106">This article describes how to use the client object model (CSOM) to:</span></span>

- <span data-ttu-id="ca022-107">Поиск списков и библиотек, которые были созданы с помощью определения списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-107">Find lists and libraries that were created by using list definitions.</span></span>
    
- <span data-ttu-id="ca022-108">Создайте и настройте новые списки.</span><span class="sxs-lookup"><span data-stu-id="ca022-108">Create and configure new lists.</span></span>
    
- <span data-ttu-id="ca022-109">Добавление и удаление представлений из списков.</span><span class="sxs-lookup"><span data-stu-id="ca022-109">Add and remove views from lists.</span></span>
    
- <span data-ttu-id="ca022-110">Перенос контента из исходного списка в новый список.</span><span class="sxs-lookup"><span data-stu-id="ca022-110">Migrate content from the original list to the new list.</span></span>

<span data-ttu-id="ca022-111">**Важно!**</span><span class="sxs-lookup"><span data-stu-id="ca022-111">**Important**</span></span> <p><span data-ttu-id="ca022-112">Решения фермы нельзя перенести в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="ca022-112">Farm solutions cannot be migrated to SharePoint Online.</span></span> <span data-ttu-id="ca022-113">Применение методики и кода, описанного в данной статье, можно создать новое решение с аналогичными возможностями, что полностью решений фермы, который можно развернуть в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="ca022-113">By applying the techniques and code described in this article, you can build a new solution with similar functionality that your farm solutions provide, which can then be deployed to SharePoint Online.</span></span> <span data-ttu-id="ca022-114">При использовании подхода к преобразования на месте может потребоваться развертывание нового решения в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="ca022-114">If you are using an in-place transformation approach, you may need to deploy the new solution to SharePoint Online.</span></span> <span data-ttu-id="ca022-115">При использовании две или переноса содержимого подход средств сторонних производителей могут создать списки.</span><span class="sxs-lookup"><span data-stu-id="ca022-115">If you are using the Swing or content migration approach, the third-party tools may create the lists for you.</span></span> <span data-ttu-id="ca022-116">Для получения дополнительных сведений см [преобразования подходов для развертывания новой надстройки SharePoint](https://msdn.microsoft.com/library/dn986827.aspx#sectionSection1).</span><span class="sxs-lookup"><span data-stu-id="ca022-116">For more information, see [Transformation approaches to deploy your new SharePoint Add-in](https://msdn.microsoft.com/library/dn986827.aspx#sectionSection1).</span></span> <span data-ttu-id="ca022-117">Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения.</span><span class="sxs-lookup"><span data-stu-id="ca022-117">The code in this article requires additional code to provide a fully working solution.</span></span> <span data-ttu-id="ca022-118">Например, в этой статье не рассматривается проходить проверку подлинности в Office 365, как реализовать обработку исключений обязательные и т. д.</span><span class="sxs-lookup"><span data-stu-id="ca022-118">For example, this article does not discuss how to authenticate to Office 365, how to implement required exception handling, and so on.</span></span> <span data-ttu-id="ca022-119">Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).</span><span class="sxs-lookup"><span data-stu-id="ca022-119">For additional code samples, see the [Office 365 Developer Patterns and Practices project](https://github.com/SharePoint/PnP).</span></span></p><p><span data-ttu-id="ca022-120">Используйте методы, описанные в этой статье описывается обновление только несколько списков за раз.</span><span class="sxs-lookup"><span data-stu-id="ca022-120">Use the techniques described in this article to update only a few lists at a time.</span></span> <span data-ttu-id="ca022-121">Кроме того при поиске списков, чтобы обновить не следует фильтровать списков по типу списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-121">Also, when finding lists to update, you should not filter the lists by list type.</span></span></p>

## <a name="before-you-begin"></a><span data-ttu-id="ca022-122">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="ca022-122">Before you begin</span></span>

<span data-ttu-id="ca022-123">В идеальном варианте следует ознакомиться существующих решений фермы, узнайте о методах, описанных в этой статье и затем планирование применение этих методов для существующих решений фермы.</span><span class="sxs-lookup"><span data-stu-id="ca022-123">Ideally, you should review your existing farm solutions, learn about the techniques described in this article, and then plan how to apply these techniques to your existing farm solutions.</span></span> <span data-ttu-id="ca022-124">Если не знакомы с решениями фермы или нет существующее решение фермы для работы с могут быть полезны позволяет:</span><span class="sxs-lookup"><span data-stu-id="ca022-124">If you are unfamiliar with farm solutions or do not have an existing farm solution to work with, it might be helpful for you to:</span></span>

1. <span data-ttu-id="ca022-125">Загрузите [решение Contoso.Intranet](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet).</span><span class="sxs-lookup"><span data-stu-id="ca022-125">Download the [Contoso.Intranet solution](https://github.com/SharePoint/PnP/tree/master/Reference%20Material/Contoso.Intranet).</span></span> <span data-ttu-id="ca022-126">Просмотрите [Анализ исходное состояние сайта и библиотеки для замены](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-2%20Replacing%20Lists%20Created%20from%20Custom%20Templates/Lab.md#examine-the-initial-state-of-the-site-and-library-for-replacement) для получения быстрого представление о, как списки созданные декларативно с помощью определения списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-126">Review [Examine the initial state of the site and library for replacement](https://github.com/SharePoint/TrainingContent/blob/master/O3658/10%20Transformation%20guidance%20from%20farm%20solutions%20to%20app%20model/10-2%20Replacing%20Lists%20Created%20from%20Custom%20Templates/Lab.md#examine-the-initial-state-of-the-site-and-library-for-replacement) to get a quick understanding of how lists were created declaratively using list definitions.</span></span>
    
    <span data-ttu-id="ca022-127">**Примечание:**  В Contoso.Intranet в файле elements.xml для SP\ListTemplate\LTContosoLibrary идентификатор для пользовательский шаблон списка — 10003.</span><span class="sxs-lookup"><span data-stu-id="ca022-127">**Note:**  In Contoso.Intranet, in the elements.xml file for SP\ListTemplate\LTContosoLibrary, the ID for the custom list template is 10003.</span></span> <span data-ttu-id="ca022-128">Это будет использоваться для идентификации шаблона, который использовался для создания списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-128">You will use this to identify the template that was used to create the list.</span></span> <span data-ttu-id="ca022-129">Также просмотрите параметры конфигурации и представления, которые определены в списке.</span><span class="sxs-lookup"><span data-stu-id="ca022-129">Also review the configuration settings and views that are defined on your list.</span></span>

2. <span data-ttu-id="ca022-130">Ознакомьтесь с решениями фермы.</span><span class="sxs-lookup"><span data-stu-id="ca022-130">Learn about farm solutions.</span></span> <span data-ttu-id="ca022-131">Для получения дополнительных сведений см. [Обзор архитектуры SharePoint 2010](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) и [создания решений фермы в SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-131">For more information, see [SharePoint 2010 Architectures Overview](https://msdn.microsoft.com/en-us/library/office/gg552610%28v=office.14%29.aspx) and [Build farm solutions in SharePoint 2013](https://msdn.microsoft.com/library/jj163902.aspx).</span></span>
    
## <a name="replace-lists-created-from-list-definitions"></a><span data-ttu-id="ca022-132">Замените списков, созданных из определений списков</span><span class="sxs-lookup"><span data-stu-id="ca022-132">Replace lists created from list definitions</span></span>

<span data-ttu-id="ca022-133">Чтобы заменить списков, созданных из определений списков:</span><span class="sxs-lookup"><span data-stu-id="ca022-133">To replace lists created from list definitions:</span></span>

1. <span data-ttu-id="ca022-134">Поиск списков, которые были созданы с помощью определенного базового шаблона.</span><span class="sxs-lookup"><span data-stu-id="ca022-134">Find lists that were created using a specific base template.</span></span>
    
2. <span data-ttu-id="ca022-135">Создание нового списка с помощью определения списка ожидания введите.</span><span class="sxs-lookup"><span data-stu-id="ca022-135">Create the new list using the out-of-the-box list definition.</span></span> 
    
3. <span data-ttu-id="ca022-136">Настройте параметры списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-136">Configure list settings.</span></span>
    
4. <span data-ttu-id="ca022-137">Задавать типы контента на основе типов контента, которые были установлены в исходном списке нового списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-137">Set content types on the new list based on the content types that were set on the original list.</span></span>
    
5. <span data-ttu-id="ca022-138">(Необязательно) Добавьте представления.</span><span class="sxs-lookup"><span data-stu-id="ca022-138">(Optional) Add views.</span></span> 
    
6. <span data-ttu-id="ca022-139">(Необязательно) Удаление представлений.</span><span class="sxs-lookup"><span data-stu-id="ca022-139">(Optional) Remove views.</span></span>
    
7. <span data-ttu-id="ca022-140">Перенос контента из исходного списка в новый список.</span><span class="sxs-lookup"><span data-stu-id="ca022-140">Migrate content from the original list to the new list.</span></span>
    
<span data-ttu-id="ca022-141">В следующем примере кода метод показано, как найти списков, которые были созданы с помощью определенного базового шаблона.</span><span class="sxs-lookup"><span data-stu-id="ca022-141">In the following code, the method shows how to find lists that were created using a specific base template.</span></span> <span data-ttu-id="ca022-142">Этот метод:</span><span class="sxs-lookup"><span data-stu-id="ca022-142">This method:</span></span>

1. <span data-ttu-id="ca022-143">Использует [ClientContext](https://msdn.microsoft.com/library/microsoft.sharepoint.client.clientcontext.aspx) для получения всех списков на текущем сайте, с помощью [Web.Lists](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.lists.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-143">Uses the [ClientContext](https://msdn.microsoft.com/library/microsoft.sharepoint.client.clientcontext.aspx) to get all lists in the current web using [Web.Lists](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.lists.aspx).</span></span> <span data-ttu-id="ca022-144">Инструкции Include используется в лямбда-выражения для возврата коллекции списков.</span><span class="sxs-lookup"><span data-stu-id="ca022-144">The Include statement is used in the lambda expression to return a collection of lists.</span></span> <span data-ttu-id="ca022-145">Возвращенный списки должны иметь значения свойств, заданные для [BaseTemplate](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetemplate.aspx), [BaseType](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetype.aspx)и [Название](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.title.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-145">The returned lists must all have property values specified for [BaseTemplate](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetemplate.aspx), [BaseType](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.basetype.aspx), and [Title](https://msdn.microsoft.com/library/microsoft.sharepoint.client.list.title.aspx).</span></span>
    
2. <span data-ttu-id="ca022-146">Для каждого списка в коллекции возвращенные списков Если **List.BaseTemplate** равен 10003, добавляет списка коллекцию списков, чтобы заменить, называется **listsToReplace**.</span><span class="sxs-lookup"><span data-stu-id="ca022-146">For each list in the collection of returned lists, if the  **List.BaseTemplate** is equal to 10003, adds the list to a collection of lists to be replaced, called **listsToReplace**.</span></span> <span data-ttu-id="ca022-147">Имейте в виду, что 10003 был идентификатор шаблона настраиваемый список, которые мы reviewed в образце Contoso.Intranet.</span><span class="sxs-lookup"><span data-stu-id="ca022-147">Remember that 10003 was the custom list template's identifier we reviewed in the Contoso.Intranet sample.</span></span>

<span data-ttu-id="ca022-148">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="ca022-148">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="ca022-149">**Важные:**  В предыдущем примере кода сначала итерации по ListCollection, чтобы выбрать, какие списки необходимо изменить, а затем вызвать ReplaceList, которая начинается изменения списков.</span><span class="sxs-lookup"><span data-stu-id="ca022-149">**Important:**  In the previous code, you first iterate over the ListCollection to select which lists need to be modified, and then call ReplaceList, which starts modifying the lists.</span></span> <span data-ttu-id="ca022-150">Этот шаблон является обязательным, так как изменение контента семейства сайтов при итерации по коллекции вызовет исключение.</span><span class="sxs-lookup"><span data-stu-id="ca022-150">This pattern is required because modifying the content of a collection while iterating over the collection will throw an exception.</span></span>

<span data-ttu-id="ca022-151">После определения списка, который следует заменить **ReplaceList** показывает о порядке операций для выполнения для замены в списке.</span><span class="sxs-lookup"><span data-stu-id="ca022-151">After identifying a list that should be replaced,  **ReplaceList** shows the order of operations to perform to replace the list.</span></span>

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

<span data-ttu-id="ca022-152">Чтобы создать новый список, **CreateReplacementList** использует [ListCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.listcreationinformation.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-152">To create a new list,  **CreateReplacementList** uses [ListCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.listcreationinformation.aspx).</span></span> <span data-ttu-id="ca022-153">Заголовок нового списка имеет значение заголовка существующий список с надстройкой к нему.</span><span class="sxs-lookup"><span data-stu-id="ca022-153">The title of the new list is set to the title of the existing list, with Add-in appended to it.</span></span> <span data-ttu-id="ca022-154">Перечисление [ListTemplateType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.listtemplatetype.aspx) используется для установки типа шаблонов списков в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="ca022-154">The [ListTemplateType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.listtemplatetype.aspx) enumeration is used to set the list's template type to a document library.</span></span> <span data-ttu-id="ca022-155">При создании списка на основе типа другой шаблон убедитесь, что используется правильный шаблон тип.</span><span class="sxs-lookup"><span data-stu-id="ca022-155">If you are creating a list based on a different template type, make sure to use the correct template type.</span></span> <span data-ttu-id="ca022-156">Например при создании календарного списка используйте **ListTemplateType.Events** вместо **ListTemplateType.DocumentLibrary**.</span><span class="sxs-lookup"><span data-stu-id="ca022-156">For example, if you are creating a calendar list, use **ListTemplateType.Events** instead of **ListTemplateType.DocumentLibrary**.</span></span>

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

<span data-ttu-id="ca022-157">**SetListSettings** применяются параметры исходного списка новый список с:</span><span class="sxs-lookup"><span data-stu-id="ca022-157">**SetListSettings** applies the original list settings to the new list by:</span></span>

1. <span data-ttu-id="ca022-158">Получение различных параметров списка из исходного списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-158">Getting various list settings from the original list.</span></span>
    
2. <span data-ttu-id="ca022-159">Применить параметр списка из исходного списка в новый список.</span><span class="sxs-lookup"><span data-stu-id="ca022-159">Applying the list setting from the original list to the new list.</span></span>

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

<span data-ttu-id="ca022-160">**Примечание:**  На основе требований, параметры списка исходное списков может отличаться.</span><span class="sxs-lookup"><span data-stu-id="ca022-160">**Note:**  Based on your requirements, the list settings of your original lists might be different.</span></span> <span data-ttu-id="ca022-161">Проверьте параметры списка и измените **SetListSettings** , чтобы убедиться, что для новых списков, применяются первоначальные параметры списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-161">Review your list settings and change  **SetListSettings** to ensure that your original list settings are applied to your new lists.</span></span>

<span data-ttu-id="ca022-162">**SetContentTypes** задает типы контента на новый список с:</span><span class="sxs-lookup"><span data-stu-id="ca022-162">**SetContentTypes** sets the content types on the new list by:</span></span>

1. <span data-ttu-id="ca022-163">Получение сведений о типе контента из исходного списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-163">Getting content type information from the original list.</span></span>
    
2. <span data-ttu-id="ca022-164">Получение сведений о типе контента из нового списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-164">Getting content type information from the new list.</span></span>
    
3. <span data-ttu-id="ca022-165">Определение, позволяет ли исходный список типов контента.</span><span class="sxs-lookup"><span data-stu-id="ca022-165">Determining whether the original list enables content types.</span></span> <span data-ttu-id="ca022-166">Если исходный список не включает типы контента, **SetContentTypes** завершает работу.</span><span class="sxs-lookup"><span data-stu-id="ca022-166">If the original list does not enable content types,  **SetContentTypes** exits.</span></span> <span data-ttu-id="ca022-167">Если исходный список включены типы контента, а затем **SetContentTypes** позволяет типов контента на новый список с помощью **newList.ContentTypesEnabled = true**.</span><span class="sxs-lookup"><span data-stu-id="ca022-167">If the original list enabled content types, then **SetContentTypes** enables content types on the new list using **newList.ContentTypesEnabled = true**.</span></span>
    
4. <span data-ttu-id="ca022-168">Для каждого типа контента, в исходном списке, поиск по контенту типы в новом списке, чтобы найти подходящий тип на основе имени типа контента с помощью **newList.ContentTypes.Any контента (компьютерной телефонии = > компьютерной телефонии. Имя == contentType.Name)**.</span><span class="sxs-lookup"><span data-stu-id="ca022-168">For each content type in the original list, searching the content types on the new list to find a matching content type based on name of the content type by using  **newList.ContentTypes.Any(ct => ct.Name == contentType.Name)**.</span></span> <span data-ttu-id="ca022-169">Если тип контента не новый список, он добавляется в список.</span><span class="sxs-lookup"><span data-stu-id="ca022-169">If the content type is not in the new list, it is added to the list.</span></span>
    
5. <span data-ttu-id="ca022-170">Загрузка **newList** еще раз, так как [AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) , могут измениться типов контента.</span><span class="sxs-lookup"><span data-stu-id="ca022-170">Loading  **newList** a second time because [AddExistingContentType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttypecollection.addexistingcontenttype.aspx) might have changed the content types.</span></span>
    
6. <span data-ttu-id="ca022-171">Для каждого типа контента в **newList**определение, соответствует ли тип контента типа контента в исходном списке, основанный на [ContentType.Name](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.name.aspx) с помощью **listToBeReplaced.ContentTypes.Any (компьютерной телефонии = > компьютерной телефонии. Имя == contentType.Name)**.</span><span class="sxs-lookup"><span data-stu-id="ca022-171">For each content type in  **newList**, determining whether the content type matches a content type in the original list based on [ContentType.Name](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.name.aspx) by using **listToBeReplaced.ContentTypes.Any(ct => ct.Name == contentType.Name)**.</span></span> <span data-ttu-id="ca022-172">Если совпадение не найдено, тип контента добавляется к **contentTypesToDelete** к удалению из нового списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-172">If a match is not found, the content type is added to **contentTypesToDelete** to be deleted from the new list.</span></span>
    
7. <span data-ttu-id="ca022-173">Удаление типа контента, вызвав [ContentType.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.deleteobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-173">Deleting the content type by calling [ContentType.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.contenttype.deleteobject.aspx).</span></span>

<span data-ttu-id="ca022-174">**Примечание:**  Если вы используете подхода к преобразования на месте и типов содержимого были развернуты декларативно с помощью структура компонентов, необходимо:</span><span class="sxs-lookup"><span data-stu-id="ca022-174">**Note:**  If you are using an in-place transformation approach, and your content types were deployed declaratively using the Feature framework, you need to:</span></span> 

 1. <span data-ttu-id="ca022-175">Создание новых типов контента.</span><span class="sxs-lookup"><span data-stu-id="ca022-175">Create new content types.</span></span>

 2. <span data-ttu-id="ca022-176">Задайте тип контента для элементов списка при переносе контента из исходного списка в новый список в MigrateContent.</span><span class="sxs-lookup"><span data-stu-id="ca022-176">Set the content type on the list items when migrating the content from the original list to the new list in MigrateContent.</span></span>


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

<span data-ttu-id="ca022-177">**Примечание:**  На этом этапе новый список может принимать контент из исходного списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-177">**Note:**  At this point, the new list can accept content from the original list.</span></span> <span data-ttu-id="ca022-178">Также при необходимости можно добавлять и удалять представлений.</span><span class="sxs-lookup"><span data-stu-id="ca022-178">You can also optionally add and remove views.</span></span> 

<span data-ttu-id="ca022-179">Пользователи могут добавлять или удалять представления, определенные для списка, в соответствии с их потребностям.</span><span class="sxs-lookup"><span data-stu-id="ca022-179">Users can add or remove views defined on a list to meet their business needs.</span></span> <span data-ttu-id="ca022-180">По этой причине может потребоваться добавление или удаление представления нового списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-180">For this reason, you might need to add or remove views on the new list.</span></span>  <span data-ttu-id="ca022-181">**AddViews** добавляет представления из исходного списка в новый список с:</span><span class="sxs-lookup"><span data-stu-id="ca022-181">**AddViews** adds views from the original list to the new list by:</span></span>

1. <span data-ttu-id="ca022-182">Получение всех представлений в исходном списке с помощью [List.Views](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.views.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ca022-182">Using [List.Views](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.views.aspx) to get all views on the original list.</span></span>
    
2. <span data-ttu-id="ca022-183">Загрузить различные свойства представления в коллекции **представлений** с помощью лямбда-выражения.</span><span class="sxs-lookup"><span data-stu-id="ca022-183">Using the lambda expression to load various view properties on the  **views** collection.</span></span>
    
3. <span data-ttu-id="ca022-184">Для каждого представления в исходном списке, создание представления с помощью [ViewCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewcreationinformation.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-184">For each view in the original list, creating a view by using [ViewCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewcreationinformation.aspx).</span></span> <span data-ttu-id="ca022-185">Различные свойства устанавливаются на новое представление на основе свойств представления из исходного представления.</span><span class="sxs-lookup"><span data-stu-id="ca022-185">Various properties are set on the new view based on view properties from the original view.</span></span> <span data-ttu-id="ca022-186">Вспомогательный метод **GetViewType** вызывается для определения [ViewType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewtype.aspx) представления.</span><span class="sxs-lookup"><span data-stu-id="ca022-186">The  **GetViewType** helper method is called to determine the [ViewType](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.viewtype.aspx) of the view.</span></span> <span data-ttu-id="ca022-187">Новое представление добавляется в список представлений, называется **viewsToCreate**.</span><span class="sxs-lookup"><span data-stu-id="ca022-187">The new view is then added to the list of views called **viewsToCreate**.</span></span>
    
4. <span data-ttu-id="ca022-188">Добавление представлений в коллекции **List.Views** с помощью метода **Add** в коллекции представлений списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-188">Adding the views to the  **List.Views** collection by using the **Add** method on the list's Views collection.</span></span>

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

<span data-ttu-id="ca022-189">В следующем коде **RemoveViews** удаляет представления из новый список с:</span><span class="sxs-lookup"><span data-stu-id="ca022-189">In the following code,  **RemoveViews** removes views from the new list by:</span></span>

1. <span data-ttu-id="ca022-190">Получение представлений списка на новый список с помощью свойства **List.Views** .</span><span class="sxs-lookup"><span data-stu-id="ca022-190">Getting the list views on the new list using the  **List.Views** property.</span></span>
    
2. <span data-ttu-id="ca022-191">Для каждого представления в новом списке, определение ли это представление не существует в исходном списке, сопоставляя на просмотр заголовка с помощью **! listToBeReplaced.Views.Any (v = > v.Title == представления. Название**.</span><span class="sxs-lookup"><span data-stu-id="ca022-191">For each view on the new list, determining whether that view does not exist in the original list by matching on the view's title by using  **!listToBeReplaced.Views.Any(v => v.Title == view.Title**.</span></span> <span data-ttu-id="ca022-192">Если представление в новом списке не имеет соответствующего представления в исходном списке, добавьте представление **viewsToRemove**.</span><span class="sxs-lookup"><span data-stu-id="ca022-192">If a view in the new list does not have a matching view in the original list, then add the view to **viewsToRemove**.</span></span>
    
3. <span data-ttu-id="ca022-193">Удаление всех представлений в **viewsToRemove** с помощью [View.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.view.deleteobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-193">Deleting all views in  **viewsToRemove** by using [View.DeleteObject](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.view.deleteobject.aspx).</span></span>
    
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

<span data-ttu-id="ca022-194">**MigrateContent** переносит контент из исходного списка в новый список с:</span><span class="sxs-lookup"><span data-stu-id="ca022-194">**MigrateContent** migrates the content from the original list to the new list by:</span></span>

1. <span data-ttu-id="ca022-195">Получение назначения для копирования файлов или в корневую папку нового списка с помощью [List.RootFolder](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.rootfolder.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-195">Retrieving the destination to copy the files to, or the root folder of the new list, by using [List.RootFolder](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.rootfolder.aspx).</span></span> <span data-ttu-id="ca022-196">URL-адрес относительно сервера конечную папку списка извлекаются с помощью [Folder.ServerRelativeUrl](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.folder.serverrelativeurl.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca022-196">The server-relative URL of the destination list folder is retrieved by using [Folder.ServerRelativeUrl](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.folder.serverrelativeurl.aspx).</span></span>
    
2. <span data-ttu-id="ca022-197">Получение исходных файлов или в корневую папку исходного списка с помощью **List.RootFolder**.</span><span class="sxs-lookup"><span data-stu-id="ca022-197">Retrieving the source of the files, or the root folder of the original list, by using  **List.RootFolder**.</span></span> <span data-ttu-id="ca022-198">Относительный к серверу URL-адрес папки списка и все файлы в корневой папке источника загружаются с помощью объекта **clientContext** .</span><span class="sxs-lookup"><span data-stu-id="ca022-198">The server-relative URL of the list folder and all the files in the source's root folder are loaded by using the **clientContext** object.</span></span>
    
3. <span data-ttu-id="ca022-199">Для каждого файла в источнике создается **новый URL-адрес**, который хранит новый URL-адрес файла.</span><span class="sxs-lookup"><span data-stu-id="ca022-199">For each file in the source, creating  **newUrl**, which stores the new URL of the file.</span></span> <span data-ttu-id="ca022-200">**новый URL-адрес** создается путем замены в корневой папке источника с корневой папки назначения.</span><span class="sxs-lookup"><span data-stu-id="ca022-200">**newUrl** is created by replacing the source root folder with the destination's root folder.</span></span>
    
4. <span data-ttu-id="ca022-201">Скопируйте файл с URL-адресом конечной корневой папки с помощью [File.CopyTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.copyto.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ca022-201">Using [File.CopyTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.copyto.aspx) to copy the file to the URL of the destination root folder.</span></span> <span data-ttu-id="ca022-202">Кроме того можно использовать метод [File.MoveTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.moveto.aspx) для перемещения URL-адрес конечного файла.</span><span class="sxs-lookup"><span data-stu-id="ca022-202">Alternatively, you might choose to use the [File.MoveTo](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.file.moveto.aspx) method to move the file to the destination URL.</span></span>
    
<span data-ttu-id="ca022-203">**Примечание:**  Следующий код возвращает все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-203">**Note:**  The following code returns all list items.</span></span> <span data-ttu-id="ca022-204">В рабочей среде рассмотрите возможность оптимизации следующий код, реализовав цикла и перенос небольшое количество элементов списка с помощью нескольких итераций.</span><span class="sxs-lookup"><span data-stu-id="ca022-204">In your production environment, consider optimizing the following code by implementing a loop, and using multiple iterations to migrate small amounts of list items.</span></span>

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

<span data-ttu-id="ca022-205">**Примечание:**  Предыдущего кода показано, как миграция файлов, хранящихся в корневую папку списка.</span><span class="sxs-lookup"><span data-stu-id="ca022-205">**Note:**  The previous code shows how to migrate files stored in the root folder of a list.</span></span> <span data-ttu-id="ca022-206">Если список вложенных папок, необходимо добавить дополнительный код для перемещения вложенных папках и их содержимое.</span><span class="sxs-lookup"><span data-stu-id="ca022-206">If your list has subfolders, you will need to add additional code to migrate the subfolders and their contents.</span></span> <span data-ttu-id="ca022-207">Если в вашем списке используется рабочих процессов, чтобы сопоставить рабочий процесс для нового списка необходим дополнительный код.</span><span class="sxs-lookup"><span data-stu-id="ca022-207">If your list uses workflows, additional code is required to associate the workflow to the new list.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca022-208">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ca022-208">Additional resources</span></span>
<span data-ttu-id="ca022-209"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ca022-209"></span></span>

- [<span data-ttu-id="ca022-210">Преобразование решений ферм для модели надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="ca022-210">Transform farm solutions to the SharePoint add-in model</span></span>](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [<span data-ttu-id="ca022-211">SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="ca022-211">SharePoint 2013</span></span>](https://msdn.microsoft.com/library/office/jj162979.aspx)
