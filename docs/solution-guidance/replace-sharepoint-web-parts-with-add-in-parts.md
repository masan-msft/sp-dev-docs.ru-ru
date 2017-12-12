---
title: "Замените надстройки части веб-частей SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: af8c3eb1d5f314332542247f811b9a25daf0702a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="replace-sharepoint-web-parts-with-add-in-parts"></a>Замените надстройки части веб-частей SharePoint

Используйте процесс преобразования для замены веб-частей с помощью надстройки частей с помощью объектной модели клиента SharePoint (CSOM).

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Процесс преобразования можно использовать для замены части надстройки на страницах веб-частей SharePoint с помощью CSOM поиск и удаление определенного веб-частей, а затем добавляя новые части надстройки.

**Важные:**  Решения фермы нельзя перенести в SharePoint Online. Применение методики и кода, описанного в данной статье, можно создать новое решение с аналогичными возможностями, что полностью решений фермы, который можно развернуть в SharePoint Online. После применения этих методов страницы будут обновлены для использования надстройки части, которые можно перенести в SharePoint Online. Код, приведенный в данной статье требуется дополнительный код для обеспечения полностью рабочее решения. Например, в этой статье не рассматривается проходить проверку подлинности в Office 365, как реализовать обработку исключений обязательные и т. д. Дополнительные примеры кода в разделе [Шаблоны разработчика Office 365 и рекомендациям проекта](https://github.com/SharePoint/PnP).

## <a name="before-you-begin"></a>Перед началом работы

Перед выполнением действия, описанные в этой статье для замены части надстройки веб-частей, убедитесь, что вы:

- Используется в среде SharePoint, который настроен для поддержки надстройками SharePoint Online настроена поддержка надстроек. При использовании SharePoint Server 2013 в локальной в статье [Configure среде для SharePoint Add-ins (SharePoint 2013)](https://technet.microsoft.com/library/fp161236%28v=office.15%29).
    
- Развернули новую часть надстройки в SharePoint.
    
- Назначен надстройки разрешения на **Полный доступ** в **Web**. Дополнительные сведения можно [Добавить разрешений в SharePoint 2013](https://msdn.microsoft.com/library/office/fp142383.aspx).

## <a name="replace-web-parts-with-add-in-parts"></a>Замените надстройки части веб-частей

Замена веб-частей на новые части:

1. Экспорт части новой надстройки. Используйте экспортированного часть надстройки для получения определения части надстройки. 
    
2. Поиск всех страниц с веб-частями для замены и нажмите Удалить веб-части. 
    
3. Создание новой надстройки части на странице с помощью надстройки часть определения. 
    
Замените части добавить в веб-части с помощью CSOM, необходимо для получения определение части надстройки на экспорт части надстройки. Экспорт части надстройки для получения определение части надстройки:

1. Откройте сайт SharePoint и выберите **Параметры**или значок шестеренки и выберите команду **Изменить страницу**.
    
2. На ленте выберите команду **Вставить** > **части надстройки**.
    
3. Выберите часть надстройки и нажмите кнопку **Добавить**.
    
4. Если надстройка часть добавляется на страницу, нажмите стрелку вниз в верхнем правом углу части надстройки и выберите **Изменить веб-часть**.
    
5. В **расширенной**в **Режиме экспорта** выберите команду **экспортировать все данные**и нажмите кнопку **ОК**.
    
6. Вернувшись на страницу "Правка" с частью надстройки отображается, нажмите кнопку со стрелкой вниз в верхнем правом углу части надстройки и нажмите кнопку **Экспорт**.
    
7. Выберите команду **Сохранить**.
    
8. После завершения загрузки нажмите кнопку **Открыть папку**.
    
9. Откройте **Блокнот**, а затем выберите **файл** > **Open**.
    
10. Выберите файл надстройки часть, который был загружен и выберите команду **Открыть** для просмотра определение части надстройки.
    
> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

Для использования в коде CSOM определение части надстройки:

- Замените все двойные кавычки ("") пары двойные кавычки ("») в определении части надстройки.
    
- Назначьте определение части добавить в строку, которая будет использоваться в коде CSOM.

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

**ReplaceWebPartsWithAppParts** запускает процесс поиска веб-частей необходимо заменить:

1. Получение некоторые свойства из [Web](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.web.aspx) , чтобы найти библиотеку **страниц** на сайте.
    
2. В библиотеке **страниц** получение элементов списка и файл, связанный с элементом списка.
    
3. Для каждого элемента списка, возвращенный из библиотеки **страниц** вызов **FindWebPartToReplace**.

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

**FindWebPartToReplace** находит веб-частей, должна быть заменена новой части надстройки с:

1. Настройка **страницы** в файл, связанный с элементом списка, возвращенный из библиотеки **страниц** .
    
2. Чтобы найти все веб-части на определенную страницу с помощью [LimitedWebPartManager](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.aspx) . Название каждой веб-части также возвращается в лямбда-выражения.
    
3. Для каждого веб-части в диспетчере веб-части [веб-части](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.webparts.aspx) свойство, определение ли замена заголовка веб-части и переменной **oldWebPartTitle** , которая задано значение заголовка веб-части, совпадают. Если заголовок веб-части и **oldWebPartTitle** равны, позвонить **ReplaceWebPart**; в противном случае перейдите к следующей итерации цикла **foreach** .

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

**ReplaceWebPart** заменяет новой веб-части с:

1. С помощью [LimitedWebPartManager.ImportWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.importwebpart.aspx) для преобразования XML-строка в **appPartXml** в [WebPartDefinition](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.aspx).
    
2. Добавление веб-части на страницу в определенной зоне веб-частей с помощью [LimitedWebPartManager.AddWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.limitedwebpartmanager.addwebpart.aspx) . Убедитесь, передайте **КодЗоны** **AddWebPart**, в противном случае возникает исключение при запуске **ExecuteQuery** .
    
3. Чтобы удалить старые веб-часть со страницы с помощью [WebPartDefinition.DeleteWebPart](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.webparts.webpartdefinition.deletewebpart.aspx) .

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Преобразование решений ферм для модели надстроек SharePoint](Transform-farm-solutions-to-the-SharePoint-app-model.md)
    
- [Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Scenarios/Provisioning.Pages)
