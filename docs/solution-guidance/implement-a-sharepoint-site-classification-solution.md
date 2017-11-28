---
title: "Реализация решения SharePoint классификации"
ms.date: 11/03/2017
ms.openlocfilehash: e1ab5cde87390d51a648815cce427ae4930aab85
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="implement-a-sharepoint-site-classification-solution"></a>Реализация решения SharePoint классификации

Реализация решения классификации сайта в SharePoint.

_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Даже с надлежащего руководства сайтов SharePoint могут распространением и расти из элемента управления. Сайты создаются, как они необходимы, но и редко. Обход контента при поиске является Заработная с неиспользуемых семейств сайтов и поиска создает устаревшую и имеют значения результатов. Классификация сайта можно определить и сохранить конфиденциальные данные. В этой статье показано, как использовать образец [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) для внедрения решения классификации сайта, а также использование политик сайтов SharePoint для применения параметров удаления. В этом решении можно интегрировать в существующие решения лучше управлять сайтов по подготовке сайта.

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите образец [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="define-and-set-site-policies"></a>Определения и настройки политики сайта

Сначала необходимо для определения и настройки политики сайта, которые будут доступны в все семейства сайтов. В примере Core.SiteClassification относится к SharePoint Online MT, но можно также использовать в SharePoint Online выделенных или локальная версия SharePoint. Политики сайта задайте в концентраторе типов контента, расположенный в SharePoint Online MT в `https://[tenanatname]/sites/contentTypeHub`. Чтобы настроить политику сайта, перейдите в раздел **Параметры** > **Администрирование семейства веб-сайтов** > **Политики сайта** > ** Создание **. Откроется страница **Новой политики сайта** . Дополнительные сведения о параметрах политики можно [Обзор политик сайта в SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).

На странице **Создание политики сайта** заполните следующие поля:

-  **Имя:** HBI
    
-  **Описание:** Это super секрета.
    
- Установите переключатель **автоматического удаления сайтов**.
    
- Для **событие удаления:**, используйте сайт, созданный Дата + 1 лет.
    
- Выберите **Отправить уведомление по электронной почте владельцам веб-сайтов дальнем до удаления:** флажок и задайте для него значение 1 месяц.
    
- Выберите **отправлять уведомления звонящему каждые:** флажок и задайте для него значение 14 дней.
    
- Выберите **владельцев можно отложить предстоящее удаления для:** флажок и задайте для него значение 1 месяц.
    
- Установите флажок **семейства веб-сайтов будет доступно только для чтения, при ее закрытии** .
    
Повторите эти действия несколько раз, для имен **MBI** и **LBI**. Используйте различные настройки для удаления или сохранения политик. После завершения работы могут публиковать новые политики.

## <a name="insert-a-custom-action"></a>Вставка дополнительного действия

Можно добавить настраиваемое действие для классификации сайта на странице " **Параметры** " и значок **устройства SharePoint** . Это действие доступно только для пользователей с разрешением на **ManageWeb** . Для получения дополнительных сведений см [по умолчанию расположений пользовательских действий и идентификаторы](http://msdn.microsoft.com/en-us/library/office/bb802730%28v=office.15%29.aspx).

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
/// <summary>
/// Adds a custom Action to a Site Collection.
/// </summary>
/// <param name="ctx">The Authenticated client context.</param>
/// <param name="hostUrl">The Provider hosted URL for the Application</param>

static void AddCustomAction(ClientContext ctx, string hostUrl)
{
    var _web = ctx.Web;
    ctx.Load(_web);
    ctx.ExecuteQuery();

    // You only want the action to show up if you have manage web permissions.
    BasePermissions _manageWebPermission = new BasePermissions();
    _manageWebPermission.Set(PermissionKind.ManageWeb);

    CustomActionEntity _entity = new CustomActionEntity()
    {
        Group = "SiteTasks",
        Location = "Microsoft.SharePoint.SiteSettings",
        Title = "Site Classification",
        Sequence = 1000,
        Url = string.Format(hostUrl, ctx.Url),
        Rights = _manageWebPermission,
    };

    CustomActionEntity _siteActionSC = new CustomActionEntity()
    {
        Group = "SiteActions",
        Location = "Microsoft.SharePoint.StandardMenu",
        Title = "Site Classification",
        Sequence = 1000,
        Url = string.Format(hostUrl, ctx.Url),
        Rights = _manageWebPermission
    };
    _web.AddCustomAction(_entity);
    _web.AddCustomAction(_siteActionSC);
}
```

## <a name="custom-site-classification"></a>Классификация настраиваемого сайта

Страница **Изменить сведения о сайта** выберите указанные ниже параметры конкретного классификации:

-  **Область аудитории:** Задайте значение **предприятия**, **организации**или **группы**.
    
-  **Классификации безопасности:** Задайте значение одной из категорий классификации, введенного, такие как **LBI**.
    
-  **Срок действия:** Переопределите срок действия по умолчанию, основанное на классификации введенных ранее.
    
**Сделать доступными аудитории** и **Классификации сайта** для поиска и будет управляемого свойства, связанные с ними после обходе. Затем можно использовать эти свойства для поиска конкретных типов сайтов с помощью настраиваемого скрытого списка в пределах семейства веб-сайтов. В этом списке реализована в проекте [Core.SiteClassification.Common](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification/Core.SiteClassification.Common) в классе **SiteManagerImpl** .

```C#
private void CreateSiteClassificationList(ClientContext ctx)
{
  var _newList = new ListCreationInformation()
    {
    Title = SiteClassificationList.SiteClassificationListTitle,
    Description = SiteClassificationList.SiteClassificationDesc,
    TemplateType = (int)ListTemplateType.GenericList,
    Url = SiteClassificationList.SiteClassificationUrl,
    QuickLaunchOption = QuickLaunchOptions.Off
    };

  if(!ctx.Web.ContentTypeExistsById(SiteClassificationContentType.SITEINFORMATION_CT_ID))
    {
    // Content type.
    ContentType _contentType = ctx.Web.CreateContentType(SiteClassificationContentType.SITEINFORMATION_CT_NAME,
    SiteClassificationContentType.SITEINFORMATION_CT_DESC,
    SiteClassificationContentType.SITEINFORMATION_CT_ID,
    SiteClassificationContentType.SITEINFORMATION_CT_GROUP);

    FieldLink _titleFieldLink = _contentType.FieldLinks.GetById(new Guid("fa564e0f-0c70-4ab9-b863-0177e6ddd247"));
    titleFieldLink.Required = false;
    contentType.Update(false);

    // Key Field.
    ctx.Web.CreateField(SiteClassificationFields.FLD_KEY_ID, 
      SiteClassificationFields.FLD_KEY_INTERNAL_NAME, 
      FieldType.Text, 
      SiteClassificationFields.FLD_KEY_DISPLAY_NAME, 
      SiteClassificationFields.FIELDS_GROUPNAME);

    // Value field.
    ctx.Web.CreateField(SiteClassificationFields.FLD_VALUE_ID, 
      SiteClassificationFields.FLD_VALUE_INTERNAL_NAME, 
      FieldType.Text, 
      SiteClassificationFields.FLD_VALUE_DISPLAY_NAME, 
      SiteClassificationFields.FIELDS_GROUPNAME);

    // Add Key Field to content type.
    ctx.Web.AddFieldToContentTypeById(SiteClassificationContentType.SITEINFORMATION_CT_ID, 
      SiteClassificationFields.FLD_KEY_ID.ToString(), 
      true);

    // Add Value Field to content type.
    ctx.Web.AddFieldToContentTypeById(SiteClassificationContentType.SITEINFORMATION_CT_ID,
      SiteClassificationFields.FLD_VALUE_ID.ToString(),
      true);
    }

  var _list = ctx.Web.Lists.Add(_newList);

  list.Hidden = true;
  list.ContentTypesEnabled = true;
  list.Update();
  ctx.Web.AddContentTypeToListById(SiteClassificationList.SiteClassificationListTitle,
    SiteClassificationContentType.SITEINFORMATION_CT_ID, true);
  this.CreateCustomPropertiesInList(_list);
  ctx.ExecuteQuery();
  this.RemoveFromQuickLaunch(ctx, SiteClassificationList.SiteClassificationListTitle);

}
```

По умолчанию при создании списка, из коробки или с помощью CSOM, списке будут доступны в меню " **последние** ". Списка должен быть скрыты, однако. Следующий код удаляет элемент из меню "Последние".

```C#
private void RemoveFromQuickLaunch(ClientContext ctx, string listName)
  {
  Site _site = ctx.Site;
  Web _web = _site.RootWeb;

  ctx.Load(_web, x => x.Navigation, x => x.Navigation.QuickLaunch);
  ctx.ExecuteQuery();

  var _vNode = from NavigationNode _navNode in _web.Navigation.QuickLaunch
      where _navNode.Title == "Recent"
      select _navNode;

  NavigationNode _nNode = _vNode.First<NavigationNode>();
  ctx.Load(_nNode.Children);
  ctx.ExecuteQuery();
  var vcNode = from NavigationNode cn in _nNode.Children
     where cn.Title == listName
     select cn;
  NavigationNode _cNode = vcNode.First<NavigationNode>();
 _cNode.DeleteObject();
  ctx.ExecuteQuery();    
  }
```

Пример Core.SiteClassification предоставляет возможность, что администратор или пользователь с разрешением можно удалить нового списка. При обращении к ним на этой странице список создается еще раз, но примера не устанавливает свойства обратно. Это позволяет избежать расширяя примера для изменения разрешений в списке, чтобы только администраторы имеют доступ. Кроме того можно использовать пример PnP [Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration) выполнять проверки в списке и соответствующим образом уведомления администраторов сайта.

Проверка списка также реализован в классе **SiteManagerImpl** **инициализацию** элементов.

```C#
internal void Initialize(ClientContext ctx)
{
try {
         var _web = ctx.Web;
         var lists = _web.Lists;
         ctx.Load(_web);
         ctx.Load(lists, lc => lc.Where(l => l.Title == SiteClassificationList.SiteClassificationListTitle));
         ctx.ExecuteQuery();
                
          if (lists.Count == 0) {
                this.CreateSiteClassificationList(ctx); 
          }
      }
      catch(Exception _ex)
         {

         }
     }
}
```

**Примечание:**  Для получения дополнительных сведений см. [Создание списка на веб-сайт, когда надстройки SharePoint установлен и удаляет его из списка последних (en)](http://blogs.technet.com/b/speschka/archive/2014/05/07/create-a-list-in-the-host-web-when-your-sharepoint-app-is-installed-and-remove-it-from-the-recent-stuff-list.aspx).

## <a name="add-a-classification-indicator-to-site-page"></a>Добавить индикатор классификации страницу сайта

Индикатор можно добавить на страницу сайта, чтобы отобразить его классификации. Core.SiteClassificationsample показано, как рисунок, демонстрирующий классификации встраивается рядом с полем **Заголовка сайта**. В более ранних версиях SharePoint это делается с помощью серверного замещаемого элемента управления. Несмотря на то, что можно использовать пользовательскую главную страницу с помощью JavaScript, в этом примере используются внедренных шаблон JavaScript. При изменении **Политики сайта** на странице **Изменить сведения о сайта** , при этом изменяется индикатор сайта для отображения небольшое окно с помощью разный цвет фона для каждого из параметров классификации сайта.

Следующий метод определен в проекте, сценарии и classifier.js Core.SiteClassificationWeb. Изображения хранятся в веб-сайте Microsoft Azure. Вам необходимо изменить жестко заданные URL-адреса в соответствии со средой.

```C#
function setClassifier() {
    if (!classified)
    {
        var clientContext = SP.ClientContext.get_current();
        var query = "<View><Query><Where><Eq><FieldRef Name='SC_METADATA_KEY'/><Value Type='Text'>sc_BusinessImpact</Value></Eq></Where></Query><ViewFields><FieldRef Name='ID'/><FieldRef Name='SC_METADATA_KEY'/><FieldRef Name='SC_METADATA_VALUE'/></ViewFields></View>";
        var list = clientContext.get_web().get_lists().getByTitle("Site Information");
        clientContext.load(list);
        var camlQuery = new SP.CamlQuery();
        camlQuery.set_viewXml(query);
        var listItems = list.getItems(camlQuery);
        clientContext.load(listItems);

        clientContext.executeQueryAsync(Function.createDelegate(this, function (sender, args) {
            var listItemInfo;
            var listItemEnumerator = listItems.getEnumerator();

            while (listItemEnumerator.moveNext()) {
                listItemInfo = listItemEnumerator.get_current().get_item('SC_METADATA_VALUE');
                
                var pageTitle = $('#pageTitle')[0].innerHTML;
                if (pageTitle.indexOf("img") > -1) {
                    classified = true;
                }
                else {
                    var siteClassification = listItemInfo;
                    if (siteClassification == "HBI") {
                        var img = $("<a href='http://insertyourpolicy' target=_blank><img id=classifer name=classifer src='https://spmanaged.azurewebsites.net/content/img/hbi.png' title='Site contains personally identifiable information (PII), or unauthorized release of information on this site would cause severe or catastrophic loss to Contoso.' alt='Site contains personally identifiable information (PII), or unauthorized release of information on this site would cause severe or catastrophic loss to Contoso.'></a>");
                        $('#pageTitle').prepend(img);
                        classified = true;
                    }
                    else if (siteClassification == "MBI") {
                        var img = $("<a href='http://insertyourpolicy' target=_blank><img id=classifer name=classifer src='https://spmanaged.azurewebsites.net/content/img/mbi.png' title='Unauthorized release of information on this site would cause severe impact to Contoso.' alt='Unauthorized release of information on this site would cause severe impact to Contoso.'></a>");
                        $('#pageTitle').prepend(img);
                        classified = true;
                    }
                    else if (siteClassification == "LBI") {
                        var img = $("<a href='http://insertyourpolicy' target=_blank><img id=classifer name=classifer src='https://spmanaged.azurewebsites.net/content/img/lbi.png' title='Limited or no impact to Contoso if publically released.' alt='Limited or no impact to Contoso if publically released.'></a>");
                        $('#pageTitle').prepend(img);
                        classified = true;
                    }
                }
            }
        }));
    }
```

## <a name="alternative-approach"></a>Альтернативный подход

Метод расширения **Web.AddIndexedPropertyBagKey** в файле ObjectPropertyBagEntry.cs в[OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core) можно использовать для хранения значения классификации в контейнеры свойств узла вместо списка. Этот метод позволяет контейнеры свойств для обхода или с возможностью поиска.

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Решения по подготовке сайтов SharePoint](sharepoint-site-provisioning-solutions.md)
    
- [Пример OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core)
    
- [Пример Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration)
