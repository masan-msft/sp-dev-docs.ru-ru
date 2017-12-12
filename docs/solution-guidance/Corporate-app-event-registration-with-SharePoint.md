---
title: "Корпоративный события приложения интеграция с SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 959fea4e8fcdfe5c73a9a53e6c5da09c325d781d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="corporate-event-app-integration-with-sharepoint"></a>Корпоративный события приложения интеграция с SharePoint

Интеграция надстроек для SharePoint в бизнес-операции с помощью размещение у поставщика в надстройке, который можно реализовать несколько сложных бизнес-задач.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Пример [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) показано, как реализовать систему управления централизованного корпоративных событий как размещение у поставщика надстройки, которая интегрируется с существующими приложениями бизнес (LOB).

В частности [BusinessApps.CorporateEventApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp) примере показано, как реализовать веб-приложения ASP.NET, взаимодействующий с SharePoint в качестве хранилища данных для сущностей LOB. Он также показано, как реализовать несколько действий в сложных бизнес-задачу с одной размещением у поставщика надстройки.
В этом примере приложения реализует систему централизованного управления, состоящую из объектов SharePoint (списков и типов контента). Для каждого нового типа контента он создает соответствующие LOB сущности в веб-приложение ASP.NET. Компоненты веб-приложения, как удаленного выполнения размещены надстройки из частей в интерфейсе SharePoint, а также страниц, запущены на удаленного веб-узла. Надстройка переопределяет начальная страница по умолчанию для сайта SharePoint, чтобы его можно представить фирменной символикой пользовательского интерфейса на домашней странице сайта.

## <a name="using-the-businessappscorporateeventapp-sample"></a>Использование примера BusinessApps.CorporateEventApp

При запуске примера приложения BusinessApps.CorporateEventApp на домашнюю страницу предоставляет возможность возможность настройки образца. Также вы указывает на количество ресурсов для получения дополнительных сведений.

При выборе **Пуск конфигурации**вы перейдите на страницу конфигурации, как показано на рисунке 1. При выборе **инициализации хранилища данных** на странице Настройка примера развертывает объектов SharePoint и образцы данных, которые поддерживают примера.

**На рисунке 1. Страница настройки**

![Снимок экрана, которая отображает экран данных initialize](media/ee213035-b014-45cc-94f4-d8c1c58a047e.png)

После инициализации хранилища данных, можно вернуться на сайт для просмотра новой начальной страницы (страница EventsHome.aspx), которой заполняется две веб-части, которые добавить в развертывание, как показано на рисунке 2. В левом столбце вы увидите четыре новых списков, установленные приложением, с демонстрационных данных выполняется заполнение списка корпоративных событий.

**На рисунке 2. Начальная страница с веб-частей инициализации**

![Снимок экрана, показывающий начальной страницы надстройка с веб-частями развернут](media/aa4dbd35-70f0-43c2-845c-615632090c44.png)

Каждой веб-части содержит ссылки на каждый из отображения событий, где можно просмотреть сведения о событии. При выборе ссылки на страницу сведений события запускает отдельно на удаленном узле, как показано на рисунке 3. Вы можете **вернуться к сайта** на странице для возврата на сайте SharePoint, а также чтобы зарегистрироваться для события.

**На рисунке 3. Страница сведений о событии**

![Снимок экрана, которая отображает пользовательский Интерфейс надстройки с корпоративной события экран сведения о событии](media/b967e4ec-e0a6-4aae-af81-e22b92cef0d9.png)

Страница регистрации также работает отдельно на удаленном узле, а также содержит ссылку на сайт узла SharePoint (см). После завершения регистрации для события ваше имя будет отображаться в списке только что установленного **Регистрация событий** .

**На рисунке 4. Страница регистрации событий**

![Снимок экрана, которая отображает экран регистрации событий корпоративных событий приложения](media/d2ec4156-5806-4b20-ab5b-3d25fcc33f1a.png)

Файл Models\DataInitializer.cs содержит код, который выполняется при нажатии этой кнопки. Код в этом файле создает и развертывает четыре новых списков SharePoint, наряду с четырьмя соответствующих типов контента:

- Корпоративных событий
    
- Регистрация событий
    
- Докладчики
    
- Сеансы событий
    
Код в этом файле использует метод, аналогичный тому, который используется в образце [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages) , чтобы добавить пользовательскую страницу на сайте.

```
            // Create default wiki page.
            web.AddWikiPage("Site Pages", "EventsHome.aspx");
AddWikiPage is an extension method from the Core.DevPnPCore project to add a new page to the site. This new page also becomes the new WelcomePage for the site. It also prepares to add the web parts to this page.
            var welcomePage = "SitePages/EventsHome.aspx";
            var serverRelativeUrl = UrlUtility.Combine(web.ServerRelativeUrl, welcomePage);

            File webPartPage = web.GetFileByServerRelativeUrl(serverRelativeUrl);

            if (webPartPage == null) {
                return;
            }

            web.Context.Load(webPartPage);
            web.Context.Load(webPartPage.ListItemAllFields);
            web.Context.Load(web.RootFolder);
            web.Context.ExecuteQuery();

            web.RootFolder.WelcomePage = welcomePage;
            web.RootFolder.Update();
            web.Context.ExecuteQuery();

```

Файл Models\DataInitializer.cs также определяет XML-код для обоих веб-частей, которые отображаются на новой странице приветствия и затем добавляет каждой из них на страницу. В следующих примерах показано, как это работает для веб-части известных событий.

**Определение веб-части XML**

```XML
            var webPart1 = new WebPartEntity(){
                WebPartXml = @"<webParts>
  <webPart xmlns='http://schemas.microsoft.com/WebPart/v3'>
    <metaData>
      <type name='Microsoft.SharePoint.WebPartPages.ClientWebPart, Microsoft.SharePoint, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c' />
      <importErrorMessage>Cannot import this Web Part.</importErrorMessage>
    </metaData>
    <data>
      <properties>
        <property name='Description' type='string'>Displays featured events</property>
        <property name='FeatureId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>3a6d7f41-2de8-4e69-b4b4-0325bd56b32c</property>
        <property name='Title' type='string'>Featured Events</property>
        <property name='ProductWebId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>12ae648f-27db-4a97-9c63-37155d3ace1e</property>
        <property name='WebPartName' type='string'>FeaturedEvents</property>
        <property name='ProductId' type='System.Guid, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'>3a6d7f41-2de8-4e69-b4b4-0325bd56b32b</property>
        <property name='ChromeState' type='chromestate'>Normal</property>
      </properties>
    </data>
  </webPart>
</webParts>",
                WebPartIndex = 0,
                WebPartTitle = "Featured Events",
                WebPartZone = "Rich Content"
            };

```

**Добавить веб-части на страницу**

```XML
            var limitedWebPartManager = webPartPage.GetLimitedWebPartManager(Microsoft.SharePoint.Client.WebParts.PersonalizationScope.Shared);
            web.Context.Load(limitedWebPartManager.WebParts);
            web.Context.ExecuteQuery();

            for (var i = 0; i < limitedWebPartManager.WebParts.Count; i++) {
                limitedWebPartManager.WebParts[i].DeleteWebPart();
            }
            web.Context.ExecuteQuery();

            var oWebPartDefinition1 = limitedWebPartManager.ImportWebPart(webPart1.WebPartXml);
            var oWebPartDefinition2 = limitedWebPartManager.ImportWebPart(webPart2.WebPartXml);
            var wpdNew1 = limitedWebPartManager.AddWebPart(oWebPartDefinition1.WebPart, webPart1.WebPartZone, webPart1.WebPartIndex);
            var wpdNew2 = limitedWebPartManager.AddWebPart(oWebPartDefinition2.WebPart, webPart2.WebPartZone, webPart2.WebPartIndex);
            web.Context.Load(wpdNew1);
            web.Context.Load(wpdNew2);
            web.Context.ExecuteQuery();

```

В каталоге модели веб-проекта можно заметить, что это веб-приложение MVC ASP.NET содержит четыре именами классов, которые соответствуют списков и типов контента, установлено приложение:

- Event.cs (корпоративных событий)
    
- Registration.cs (Регистрация событий)
    
- Session.cs (события сеансов)
    
- Speaker.cs (докладчики)
    
Эти четыре классы и их соответствующие типы содержимого SharePoint вместе составляют четыре LOB записей, использованных в этой надстройки.

Файл DataInitializer.cs добавляет демонстрационных данных для списка **Корпоративных событий** , создав образец объектов **событий** , которые соответствуют с типом контента **Корпоративных событий** и приложение добавляется в список **Корпоративных событий** . При регистрации события приложение создает объект **регистрации** , соответствующий с типом контента **Регистрация событий** и приложение добавляется в список **Регистрации событий** . Образец имеет еще не реализованы полностью объектов **сеанса** и **динамик** , поэтому приложения в настоящее время не работает с объектами.

В следующей таблице приведены свойства необходимость реализовываться классы, наследующие от абстрактного класса **BaseListItem** .

** В таблице 1. Методы для реализации в классы, унаследованные от ** BaseListItem ***

|**Элемент  **|**Описание**|
|:-----|:-----|
|**Это элемент ContentTypeName**|Получает тип контента, связанный с элементом. Если значение null, тип контента библиотеки по умолчанию будет назначен элемент после ее сохранения.|
|**FieldInternalNames**|Список имен полей, которые могут быть кэшированы для повышения производительности при использовании для проверки данных поля до сохранения.|
|ListTitle|Получает заголовок списка (с учетом регистра).|

В следующей таблице перечислены методы, которые должны быть реализованы классами, наследующие от абстрактного класса **BaseListItem** . Эти методы возвращают параметры, которые необходимо задать [преобразуемых типов](https://msdn.microsoft.com/en-us/library/75dwhxf7%28v=vs.110%29.aspx) , чтобы их можно использовать на разных платформах.

 **В таблице 2. Методы, возвращающие преобразуемых типов**

|**Метод**|**Описание**|
|:-----|:-----|
|**ReadProperties(ListItem)**|Считывает свойства из объекта **ListItem** , с помощью методов **BaseGet** и **BaseGetEnum** и присваивает им свойства подкласса.|
|**SetProperties(ListItem)**|Задает свойства **ListItem** объекта, с помощью методов **BaseSet** и **BaseSetTaxonomyField** абстрактного класса.|

В следующей таблице перечислены вспомогательные методы от класса **BaseListItem** , необходимо реализовать методы **ReadProperties** и **SetProperties** подклассов.

**В таблице 3. BaseListItem вспомогательные методы**

|**Вспомогательный метод**|**Описание**|
|:-----|:-----|
|**BaseGet (элемент ListItem, внутреннееимя строка)**|Получает свойство, определенного параметром *внутреннееимя* из **ListItem** и возвращает их универсальный тип **T**.|
|**BaseSet (элемент ListItem, внутреннееимя string, значение объекта)**|Задает свойства **ListItem** , определенного параметром *внутреннееимя* .|
|**BaseSetTaxonomyField (элемент ListItem, внутреннееимя строка, строка метки, Guid termId)**|Задает поле таксономии **ListItem** , определенные с помощью параметров *внутреннееимя* и *termId* .|
|**BaseGetEnum (элемент ListItem, внутреннееимя string, T defaultValue)**|Получает значение перечисления свойства, определенного параметром *внутреннееимя* . Возвращает значение параметра *значение по умолчанию* , если свойство не задано.|

Файл Event.cs содержит следующие реализации методов **ReadProperties** и **SetProperties** .

**ReadProperties**

```C#
        protected override void ReadProperties(ListItem item) {
            RegisteredEventId = BaseGet<string>(item, FIELD_REGISTERED_EVENT_ID);
            Description = BaseGet<string>(item, FIELD_DESCRIPTION);
            Category = BaseGet<string>(item, FIELD_CATEGORY);
            EventDate = BaseGet<DateTime?>(item, FIELD_DATE);
            Location = BaseGet<string>(item, FIELD_LOCATION);
            ContactEmail = BaseGet<string>(item, FIELD_CONTACT_EMAIL);
            Status = BaseGetEnum<EventStatus>(item, FIELD_STATUS);
            var imageUrl = BaseGet<FieldUrlValue>(item, FIELD_IMAGE_URL);

            if (imageUrl != null)
                ImageUrl = imageUrl.Url;
        }
SetProperties:
        protected override void SetProperties(ListItem item) {
            BaseSet(item, FIELD_REGISTERED_EVENT_ID, RegisteredEventId);
            BaseSet(item, FIELD_DESCRIPTION, Description);
            BaseSet(item, FIELD_CATEGORY, Category);
            BaseSet(item, FIELD_DATE, EventDate);
            BaseSet(item, FIELD_LOCATION, Location);
            BaseSet(item, FIELD_CONTACT_EMAIL, ContactEmail);
            BaseSet(item, FIELD_STATUS, Status.ToEnumDescription());
            BaseSet(item, FIELD_IMAGE_URL, ImageUrl);
        }

```

В следующих примерах кода показано определение базовых методов **BaseGet** и **BaseSet** в BaseListItem.cs.

**BaseGet**

```
protected T BaseGet<T>(ListItem item, string internalName){
            var field = _fields[internalName.ToLowerInvariant()];
            var value = item[field.InternalName];
            return (T)value;
        }

```

**BaseSet**

```
protected void BaseSet(ListItem item, string internalName, object value) {
            if (_fields.ContainsKey(internalName)) {
                var field = _fields[internalName.ToLowerInvariant()];

                if (field is FieldUrl &amp;&amp; value is string) {
                    var urlValue = new FieldUrlValue() {
                        Url = value.ToString()
                    };
                    value = urlValue;
                }
            }
            item[internalName] = value;
        }
```

Класс **BaseListItem** также содержит **Сохранить** метод, который используется для сохранения каждого объекта LOB, приложение создает и управляет. Этот метод загружает список и определяет, имеет ли текущий элемент идентификатор, который больше 0. Если идентификатор не больше 0, предполагается, что он не является допустимым и создает новый элемент списка. Он использует метод **SetProperties** следует задать свойства **ListItem** и затем задает свойства подкласса с помощью метода **ReadProperties** .

```
public void Save(Web web) {
            var context = web.Context;
            var list = web.GetListByTitle(ListTitle);
            if (!IsNew &amp;&amp; Id > 0) {
                ListItem = list.GetItemById(Id);
            }
            else {
                var listItemCreationInfo = new ListItemCreationInformation();
                ListItem = list.AddItem(listItemCreationInfo);
            }

            // Ensure that the fields have been loaded.
            EnsureFieldsRetrieved(ListItem);

            // Set the properties on the list item.
            SetProperties(ListItem);
            BaseSet(ListItem, TITLE, Title);

            // Use if you want to override the created/modified date.
            //BaseSet(ListItem, CREATED, Created);
            //BaseSet(ListItem, MODIFIED, Modified);

            ListItem.Update();

            if (!string.IsNullOrEmpty(ContentTypeName)) {
                var contentType = list.GetContentTypeByName(ContentTypeName);
                if (contentType != null)
                    BaseSet(ListItem, "ContentTypeId", contentType.Id.StringValue);
            }

            ListItem.Update();

            // Execute the batch.
            context.ExecuteQuery();

            // Reload the properties.
            ListItem.RefreshLoad();
            UpdateBaseProperties(ListItem);
            ReadProperties(ListItem);
        }

```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online](Composite-buisness-apps-for-SharePoint.md)
    
-  [Пример Core.ModifyPages](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ModifyPages)
    
-  [Пример Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
-  [Пример OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
