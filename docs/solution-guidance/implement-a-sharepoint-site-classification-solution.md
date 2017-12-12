---
title: "Реализация решения SharePoint классификации"
ms.date: 11/03/2017
ms.openlocfilehash: 366b09990039dcb23ad21bf3259d3cafe1c9cee9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="implement-a-sharepoint-site-classification-solution"></a><span data-ttu-id="48977-102">Реализация решения SharePoint классификации</span><span class="sxs-lookup"><span data-stu-id="48977-102">Implement a SharePoint site classification solution</span></span>

<span data-ttu-id="48977-103">Реализация решения классификации сайта в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="48977-103">Implement a site classification solution in SharePoint.</span></span>

<span data-ttu-id="48977-104">_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="48977-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="48977-105">Даже с надлежащего руководства сайтов SharePoint могут распространением и расти из элемента управления.</span><span class="sxs-lookup"><span data-stu-id="48977-105">Even with good governance, SharePoint sites can proliferate and grow out of control.</span></span> <span data-ttu-id="48977-106">Сайты создаются, как они необходимы, но и редко.</span><span class="sxs-lookup"><span data-stu-id="48977-106">Sites are created as they are needed, but are rarely deleted.</span></span> <span data-ttu-id="48977-107">Обход контента при поиске является Заработная с неиспользуемых семейств сайтов и поиска создает устаревшую и имеют значения результатов.</span><span class="sxs-lookup"><span data-stu-id="48977-107">Search crawl is burdened by unused site collections, and search produces outdated and irrelevant results.</span></span> <span data-ttu-id="48977-108">Классификация сайта можно определить и сохранить конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="48977-108">Site classification allows you to identify and preserve sensitive data.</span></span> <span data-ttu-id="48977-109">В этой статье показано, как использовать образец [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) для внедрения решения классификации сайта, а также использование политик сайтов SharePoint для применения параметров удаления.</span><span class="sxs-lookup"><span data-stu-id="48977-109">This article shows you how to use the [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) sample to implement a site classification solution, as well as use SharePoint site policies to enforce deletion.</span></span> <span data-ttu-id="48977-110">В этом решении можно интегрировать в существующие решения лучше управлять сайтов по подготовке сайта.</span><span class="sxs-lookup"><span data-stu-id="48977-110">You can integrate this solution into your existing site provisioning solution to better manage your sites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="48977-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="48977-111">Before you begin</span></span>

<span data-ttu-id="48977-112">Чтобы начать работу, загрузите образец [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="48977-112">To get started, download the [Core.SiteClassification](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification) sample from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="define-and-set-site-policies"></a><span data-ttu-id="48977-113">Определения и настройки политики сайта</span><span class="sxs-lookup"><span data-stu-id="48977-113">Define and set site policies</span></span>

<span data-ttu-id="48977-114">Сначала необходимо для определения и настройки политики сайта, которые будут доступны в все семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="48977-114">Initially, you need to define and set the site policies that will be available in all your site collections.</span></span> <span data-ttu-id="48977-115">В примере Core.SiteClassification относится к SharePoint Online MT, но можно также использовать в SharePoint Online выделенных или локальная версия SharePoint.</span><span class="sxs-lookup"><span data-stu-id="48977-115">The Core.SiteClassification sample applies to SharePoint Online MT, but can be used as well in SharePoint Online Dedicated or SharePoint on-premises.</span></span> <span data-ttu-id="48977-116">Политики сайта задайте в концентраторе типов контента, расположенный в SharePoint Online MT в `https://[tenanatname]/sites/contentTypeHub`.</span><span class="sxs-lookup"><span data-stu-id="48977-116">Site polices are set in the Content Type Hub, which in SharePoint Online MT is located at  `https://[tenanatname]/sites/contentTypeHub`.</span></span> <span data-ttu-id="48977-117">Чтобы настроить политику сайта, перейдите в раздел **Параметры** > **Администрирование семейства веб-сайтов** > **Политики сайта** > ** Создание **.</span><span class="sxs-lookup"><span data-stu-id="48977-117">To set site policies, go to  **Settings** > **Site Collection Administration** > **Site Policies** > ** create**.</span></span> <span data-ttu-id="48977-118">Откроется страница **Новой политики сайта** .</span><span class="sxs-lookup"><span data-stu-id="48977-118">The  **New Site Policy** page appears.</span></span> <span data-ttu-id="48977-119">Дополнительные сведения о параметрах политики можно [Обзор политик сайта в SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="48977-119">For more information about site policy options, see [Overview of site policies in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span></span>

<span data-ttu-id="48977-120">На странице **Создание политики сайта** заполните следующие поля:</span><span class="sxs-lookup"><span data-stu-id="48977-120">On the  **New Site Policy** page, enter the following fields:</span></span>

-  <span data-ttu-id="48977-121">**Имя:** HBI</span><span class="sxs-lookup"><span data-stu-id="48977-121">**Name:** HBI</span></span>
    
-  <span data-ttu-id="48977-122">**Описание:** Это super секрета.</span><span class="sxs-lookup"><span data-stu-id="48977-122">**Description:** This is super secret.</span></span>
    
- <span data-ttu-id="48977-123">Установите переключатель **автоматического удаления сайтов**.</span><span class="sxs-lookup"><span data-stu-id="48977-123">Set radio button  **Delete sites automatically**.</span></span>
    
- <span data-ttu-id="48977-124">Для **событие удаления:**, используйте сайт, созданный Дата + 1 лет.</span><span class="sxs-lookup"><span data-stu-id="48977-124">For  **Deletion Event:**, use Site created date + 1 years.</span></span>
    
- <span data-ttu-id="48977-125">Выберите **Отправить уведомление по электронной почте владельцам веб-сайтов дальнем до удаления:** флажок и задайте для него значение 1 месяц.</span><span class="sxs-lookup"><span data-stu-id="48977-125">Select the  **Send an email notification to site owners this far in advance of deletion:** check box, and set it to 1 months.</span></span>
    
- <span data-ttu-id="48977-126">Выберите **отправлять уведомления звонящему каждые:** флажок и задайте для него значение 14 дней.</span><span class="sxs-lookup"><span data-stu-id="48977-126">Select the  **Send follow-up notifications every:** check box, and set it to 14 days.</span></span>
    
- <span data-ttu-id="48977-127">Выберите **владельцев можно отложить предстоящее удаления для:** флажок и задайте для него значение 1 месяц.</span><span class="sxs-lookup"><span data-stu-id="48977-127">Select the  **Owners can postpone imminent deletion for:** check box, and set it to 1 months.</span></span>
    
- <span data-ttu-id="48977-128">Установите флажок **семейства веб-сайтов будет доступно только для чтения, при ее закрытии** .</span><span class="sxs-lookup"><span data-stu-id="48977-128">Select the  **The site collection will be read-only when it is closed** check box.</span></span>
    
<span data-ttu-id="48977-129">Повторите эти действия несколько раз, для имен **MBI** и **LBI**.</span><span class="sxs-lookup"><span data-stu-id="48977-129">Repeat these steps two more times, for the names  **MBI** and **LBI**.</span></span> <span data-ttu-id="48977-130">Используйте различные настройки для удаления или сохранения политик.</span><span class="sxs-lookup"><span data-stu-id="48977-130">Use different settings for deletion or retention policies.</span></span> <span data-ttu-id="48977-131">После завершения работы могут публиковать новые политики.</span><span class="sxs-lookup"><span data-stu-id="48977-131">When you're finished, you can publish the new policies.</span></span>

## <a name="insert-a-custom-action"></a><span data-ttu-id="48977-132">Вставка дополнительного действия</span><span class="sxs-lookup"><span data-stu-id="48977-132">Insert a custom action</span></span>

<span data-ttu-id="48977-133">Можно добавить настраиваемое действие для классификации сайта на странице " **Параметры** " и значок **устройства SharePoint** .</span><span class="sxs-lookup"><span data-stu-id="48977-133">You can insert a custom action for site classification to the  **Settings** page and the **SharePoint gear** icon.</span></span> <span data-ttu-id="48977-134">Это действие доступно только для пользователей с разрешением на **ManageWeb** .</span><span class="sxs-lookup"><span data-stu-id="48977-134">This action is only available to users with **ManageWeb** permission.</span></span> <span data-ttu-id="48977-135">Для получения дополнительных сведений см [по умолчанию расположений пользовательских действий и идентификаторы](http://msdn.microsoft.com/en-us/library/office/bb802730%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="48977-135">For more information, see [Default Custom Action Locations and IDs](http://msdn.microsoft.com/en-us/library/office/bb802730%28v=office.15%29.aspx).</span></span>

> [!NOTE] 
> <span data-ttu-id="48977-136">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="48977-136">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

## <a name="custom-site-classification"></a><span data-ttu-id="48977-137">Классификация настраиваемого сайта</span><span class="sxs-lookup"><span data-stu-id="48977-137">Custom site classification</span></span>

<span data-ttu-id="48977-138">Страница **Изменить сведения о сайта** выберите указанные ниже параметры конкретного классификации:</span><span class="sxs-lookup"><span data-stu-id="48977-138">You can use the  **Edit Site Information** page to choose the following specific classification options:</span></span>

-  <span data-ttu-id="48977-139">**Область аудитории:** Задайте значение **предприятия**, **организации**или **группы**.</span><span class="sxs-lookup"><span data-stu-id="48977-139">**Audience Scope:** Set to **Enterprise**,  **Organization**, or  **Team**.</span></span>
    
-  <span data-ttu-id="48977-140">**Классификации безопасности:** Задайте значение одной из категорий классификации, введенного, такие как **LBI**.</span><span class="sxs-lookup"><span data-stu-id="48977-140">**Security Classification:** Set to one of the Classification categories you have entered, such as **LBI**.</span></span>
    
-  <span data-ttu-id="48977-141">**Срок действия:** Переопределите срок действия по умолчанию, основанное на классификации введенных ранее.</span><span class="sxs-lookup"><span data-stu-id="48977-141">**Expiration Date:** Override the default expiration date, which is based on the classification previously entered.</span></span>
    
<span data-ttu-id="48977-142">**Сделать доступными аудитории** и **Классификации сайта** для поиска и будет управляемого свойства, связанные с ними после обходе.</span><span class="sxs-lookup"><span data-stu-id="48977-142">Both  **Audience Reach** and **Site Classification** are searchable and will have managed properties associated with them after a crawl takes place.</span></span> <span data-ttu-id="48977-143">Затем можно использовать эти свойства для поиска конкретных типов сайтов с помощью настраиваемого скрытого списка в пределах семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="48977-143">You can then use these properties to search for specific types of sites by using a custom hidden list within the site collection.</span></span> <span data-ttu-id="48977-144">В этом списке реализована в проекте [Core.SiteClassification.Common](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification/Core.SiteClassification.Common) в классе **SiteManagerImpl** .</span><span class="sxs-lookup"><span data-stu-id="48977-144">This list is implemented in the [Core.SiteClassification.Common](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteClassification/Core.SiteClassification.Common) project in the **SiteManagerImpl** class.</span></span>

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

<span data-ttu-id="48977-145">По умолчанию при создании списка, из коробки или с помощью CSOM, списке будут доступны в меню " **последние** ".</span><span class="sxs-lookup"><span data-stu-id="48977-145">By default, when you create a list either out of the box or by using CSOM, the list will be available in the  **Recent** menu.</span></span> <span data-ttu-id="48977-146">Списка должен быть скрыты, однако.</span><span class="sxs-lookup"><span data-stu-id="48977-146">The list needs to be hidden, however.</span></span> <span data-ttu-id="48977-147">Следующий код удаляет элемент из меню "Последние".</span><span class="sxs-lookup"><span data-stu-id="48977-147">The following code removes the item from the Recent menu.</span></span>

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

<span data-ttu-id="48977-148">Пример Core.SiteClassification предоставляет возможность, что администратор или пользователь с разрешением можно удалить нового списка.</span><span class="sxs-lookup"><span data-stu-id="48977-148">The Core.SiteClassification sample provides for the possibility that a site administrator or someone with permission can remove the new list.</span></span> <span data-ttu-id="48977-149">При обращении к ним на этой странице список создается еще раз, но примера не устанавливает свойства обратно.</span><span class="sxs-lookup"><span data-stu-id="48977-149">When this page is accessed, the list is created again, but the sample doesn't set the properties back.</span></span> <span data-ttu-id="48977-150">Это позволяет избежать расширяя примера для изменения разрешений в списке, чтобы только администраторы имеют доступ.</span><span class="sxs-lookup"><span data-stu-id="48977-150">You can avoid this by extending the sample to modify the permissions on the list so that only site collection administrators have access.</span></span> <span data-ttu-id="48977-151">Кроме того можно использовать пример PnP [Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration) выполнять проверки в списке и соответствующим образом уведомления администраторов сайта.</span><span class="sxs-lookup"><span data-stu-id="48977-151">Alternatively, you can use the [Core.SiteEnumeration](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration) PnP sample to do checks on the list and notify site administrators accordingly.</span></span>

<span data-ttu-id="48977-152">Проверка списка также реализован в классе **SiteManagerImpl** **инициализацию** элементов.</span><span class="sxs-lookup"><span data-stu-id="48977-152">The list verification check is also implemented in the  **SiteManagerImpl** class, in the **Initialize** member.</span></span>

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

> [!NOTE] 
> <span data-ttu-id="48977-153">Для получения дополнительных сведений см. [Создание списка на веб-сайт, когда надстройки SharePoint установлен и удаляет его из списка последних (en)](http://blogs.technet.com/b/speschka/archive/2014/05/07/create-a-list-in-the-host-web-when-your-sharepoint-app-is-installed-and-remove-it-from-the-recent-stuff-list.aspx).</span><span class="sxs-lookup"><span data-stu-id="48977-153">For more information, see [Create a list in the host web when your SharePoint add-in is installed, and remove it from the recent stuff list](http://blogs.technet.com/b/speschka/archive/2014/05/07/create-a-list-in-the-host-web-when-your-sharepoint-app-is-installed-and-remove-it-from-the-recent-stuff-list.aspx).</span></span>

## <a name="add-a-classification-indicator-to-site-page"></a><span data-ttu-id="48977-154">Добавить индикатор классификации страницу сайта</span><span class="sxs-lookup"><span data-stu-id="48977-154">Add a classification indicator to site page</span></span>

<span data-ttu-id="48977-155">Индикатор можно добавить на страницу сайта, чтобы отобразить его классификации.</span><span class="sxs-lookup"><span data-stu-id="48977-155">You can add an indicator to a site page to show its classification.</span></span> <span data-ttu-id="48977-156">Core.SiteClassificationsample показано, как рисунок, демонстрирующий классификации встраивается рядом с полем **Заголовка сайта**.</span><span class="sxs-lookup"><span data-stu-id="48977-156">The Core.SiteClassificationsample shows how an image showing classification is embedded next to the  **Site Title**.</span></span> <span data-ttu-id="48977-157">В более ранних версиях SharePoint это делается с помощью серверного замещаемого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="48977-157">In earlier versions of SharePoint, this is done via a server-side delegate control.</span></span> <span data-ttu-id="48977-158">Несмотря на то, что можно использовать пользовательскую главную страницу с помощью JavaScript, в этом примере используются внедренных шаблон JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48977-158">Although you can use a custom master page with JavaScript, this sample uses an embedded JavaScript pattern.</span></span> <span data-ttu-id="48977-159">При изменении **Политики сайта** на странице **Изменить сведения о сайта** , при этом изменяется индикатор сайта для отображения небольшое окно с помощью разный цвет фона для каждого из параметров классификации сайта.</span><span class="sxs-lookup"><span data-stu-id="48977-159">When you change the **Site Policy** in the **Edit Site Information** page, this changes the site indicator to show a small box using different background colors for each of the site classification options.</span></span>

<span data-ttu-id="48977-160">Следующий метод определен в проекте, сценарии и classifier.js Core.SiteClassificationWeb.</span><span class="sxs-lookup"><span data-stu-id="48977-160">The following method is defined in the Core.SiteClassificationWeb project, scripts, and classifier.js.</span></span> <span data-ttu-id="48977-161">Изображения хранятся в веб-сайте Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="48977-161">The images are stored in a Microsoft Azure website.</span></span> <span data-ttu-id="48977-162">Вам необходимо изменить жестко заданные URL-адреса в соответствии со средой.</span><span class="sxs-lookup"><span data-stu-id="48977-162">You will have to change the hard-coded URLs to match your environment.</span></span>

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

## <a name="alternative-approach"></a><span data-ttu-id="48977-163">Альтернативный подход</span><span class="sxs-lookup"><span data-stu-id="48977-163">Alternative approach</span></span>

<span data-ttu-id="48977-164">Метод расширения **Web.AddIndexedPropertyBagKey** в файле ObjectPropertyBagEntry.cs в[OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core) можно использовать для хранения значения классификации в контейнеры свойств узла вместо списка.</span><span class="sxs-lookup"><span data-stu-id="48977-164">You can use extension method  **Web.AddIndexedPropertyBagKey** in the ObjectPropertyBagEntry.cs file in[OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core) to store the classification values in site property bags instead of a list.</span></span> <span data-ttu-id="48977-165">Этот метод позволяет контейнеры свойств для обхода или с возможностью поиска.</span><span class="sxs-lookup"><span data-stu-id="48977-165">The method enables property bags to be crawled or searchable.</span></span>

## <a name="see-also"></a><span data-ttu-id="48977-166">См. также</span><span class="sxs-lookup"><span data-stu-id="48977-166">See also</span></span>
<span data-ttu-id="48977-167"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="48977-167"></span></span>

- [<span data-ttu-id="48977-168">Решения по подготовке сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="48977-168">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="48977-169">Пример OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="48977-169">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP/tree/96eff6153389d6d21358480878de9cc8fa21abab/OfficeDevPnP.Core)
    
- [<span data-ttu-id="48977-170">Пример Core.SiteEnumeration</span><span class="sxs-lookup"><span data-stu-id="48977-170">Core.SiteEnumeration sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SiteEnumeration)
