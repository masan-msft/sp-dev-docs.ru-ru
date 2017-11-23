---
title: "Элемент управления SharePoint Online набора навигации"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ba93e5c0-e591-48d0-a716-a08ec7ef6cea
ms.openlocfilehash: d2f13eba8daea7cdf8fb865c3762ce6fad95da92
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-online-suite-navigation-control"></a><span data-ttu-id="03759-102">Элемент управления SharePoint Online набора навигации</span><span class="sxs-lookup"><span data-stu-id="03759-102">SharePoint Online Suite Navigation control</span></span>
<span data-ttu-id="03759-p101">Сведения о главной страницы разметка для элемента управления навигации Suite, SharePoint Online. {вставьте введение}</span><span class="sxs-lookup"><span data-stu-id="03759-p101">Learn about master page markup for the Suite Navigation control in SharePoint Online. {insert introductory content}</span></span>
  
    
    


## <a name="sharepoint-online-suite-navigation-control"></a><span data-ttu-id="03759-105">Элемент управления SharePoint Online набора навигации</span><span class="sxs-lookup"><span data-stu-id="03759-105">SharePoint Online Suite Navigation control</span></span>

<span data-ttu-id="03759-p102">Элемент управления навигацией Suite отображает согласованные верхняя панель навигации в SharePoint Online. Этот элемент управления теперь является частью все ненастраиваемые ожидания введите главной страницы.</span><span class="sxs-lookup"><span data-stu-id="03759-p102">The Suite Navigation control renders a consistent top navigation bar in SharePoint Online. This control is now a part of all uncustomized out-of-the-box master pages.</span></span>
  
    
    
<span data-ttu-id="03759-p103">Если главная страница была настроена, оно не получают новый элемент управления навигации набора приложений. Чтобы добавить этот элемент управления к настраиваемой главной страницы, замените  `suiteBar` `<div>` разметка, которая соответствует типу узла, который вы используете.</span><span class="sxs-lookup"><span data-stu-id="03759-p103">If a master page was customized, it will not pick up the new Suite Navigation control. To add this control to your custom master page, replace the  `suiteBar` `<div>` with the markup that corresponds to the type of site you're using.</span></span>
  
    
    
<span data-ttu-id="03759-p104">Новый элемент управления навигации Suite поддерживает любую тему, применяемых к сайту. Если вы хотите изменить цвет панели навигации верхнего уровня, применить тему.</span><span class="sxs-lookup"><span data-stu-id="03759-p104">The new Suite Navigation control supports any theme applied to the site. If you want to change the color of the top navigation bar, apply a theme.</span></span>
  
    
    

> <span data-ttu-id="03759-112">**Важные:** При настройке сайта, рекомендуется применять темы.</span><span class="sxs-lookup"><span data-stu-id="03759-112">**Important:** When customizing a site, the best practice is to apply a theme.</span></span> <span data-ttu-id="03759-113">При использовании настраиваемого CSS к сайту настраиваемого CSS могут быть разорваны в будущем Если элемент управления навигацией Suite обновляется еще раз в службе.</span><span class="sxs-lookup"><span data-stu-id="03759-113">While you can apply custom CSS to the site, custom CSS may break in the future if the Suite Navigation control is updated again in the service.</span></span> 
  
    
    


> <span data-ttu-id="03759-114">**Осторожность:** Если вы не хотите использовать новый элемент управления, удалите разметку набора навигации на главной странице и добавьте пользовательской разметки.</span><span class="sxs-lookup"><span data-stu-id="03759-114">**Caution:** If you do not want to use the new control, remove the Suite Navigation markup from your master page and add custom markup.</span></span> <span data-ttu-id="03759-115">Тем не менее Обратите внимание, что настраиваемые главные страницы риск не набор обновлений по умолчанию для элементов управления главную страницу или новые функциональные возможности, что ненастраиваемые главной страницы.</span><span class="sxs-lookup"><span data-stu-id="03759-115">However, be aware that customized master pages run the risk of not picking up updates to default master page controls or new functionality that is added to uncustomized master pages.</span></span> <span data-ttu-id="03759-116">Использование настраиваемой главной страницы создает риск, что обновления нарушит функциональные возможности или стилей веб-узла.</span><span class="sxs-lookup"><span data-stu-id="03759-116">Using a customized master page introduces the risk that service updates will break the functionality or style of your site.</span></span> 
  
    
    


### <a name="suite-navigation-control-for-intranet-sites"></a><span data-ttu-id="03759-117">Пакет управления навигации для сайтов интрасети</span><span class="sxs-lookup"><span data-stu-id="03759-117">Suite Navigation control for intranet sites</span></span>

<span data-ttu-id="03759-p107">Для сайтов интрасети используйте следующую разметку главной страницы для элемента управления навигации набора приложений. В таблице 1 перечислены веб-элементы управления используются в коде набора навигации.</span><span class="sxs-lookup"><span data-stu-id="03759-p107">For intranet sites, use the following master page markup for the Suite Navigation control. Table 1 lists web controls used in the Suite Navigation code.</span></span>
  
    
    

<span data-ttu-id="03759-120">**В таблице 1. Веб-элементы управления навигации набора приложений для сайтов интрасети**</span><span class="sxs-lookup"><span data-stu-id="03759-120">**Table 1. Suite Navigation web controls for intranet sites**</span></span>


|<span data-ttu-id="03759-121">**веб-элемент управления**</span><span class="sxs-lookup"><span data-stu-id="03759-121">**Web Control**</span></span>|<span data-ttu-id="03759-122">**Описание**</span><span class="sxs-lookup"><span data-stu-id="03759-122">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="03759-123">SharePoint:Menu</span><span class="sxs-lookup"><span data-stu-id="03759-123">SharePoint:Menu</span></span>  <br/> |<span data-ttu-id="03759-124">Отображает меню на веб-странице ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03759-124">Displays a menu in an ASP.NET web page.</span></span>  <br/> |
|<span data-ttu-id="03759-125">SharePoint:MenuItemTemplate</span><span class="sxs-lookup"><span data-stu-id="03759-125">SharePoint:MenuItemTemplate</span></span>  <br/> |<span data-ttu-id="03759-126">Представляет элемент управления, который создает элемент в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="03759-126">Represents a control that creates an item in a drop-down menu.</span></span>  <br/> |
   

```

<SharePoint:AjaxDelta runat="server" id="suiteBarDelta" BlockElement="true" CssClass="ms-dialogHidden ms-fullWidth noindex">
<div id="suiteMenuData" class="ms-hide">
<wssuc:Welcome id="IdWelcomeData" runat="server" EnableViewState="false" RenderDataOnly="true"/>
   <span class="ms-siteactions-root" id="siteactiontd">
   <SharePoint:SiteActions runat="server" accesskey="<%$Resources:wss,tb_SiteActions_AK%>"
id="SiteActionsMenuMainData"
PrefixHtml=""
SuffixHtml=""
ImageUrl="/_layouts/15/images/spcommon.png?rev=32"
ThemeKey="spcommon"
MenuAlignment="Right"
LargeIconMode="false"
>
<CustomTemplate>
<SharePoint:Menu runat="server" Visible="false"/>
<SharePoint:FeatureMenuTemplate runat="server"
FeatureScope="Site"
Location="Microsoft.SharePoint.StandardMenu"
GroupId="SiteActions"
UseShortId="true"
>
  <SharePoint:MenuItemTemplate runat="server"
  id="MenuItem_ShareThisSite"
  Text="<%$Resources:wss,siteactions_sharethissite%>"
  Description="<%$Resources:wss,siteactions_sharethissitedescription%>"
  MenuGroupId="100"
  Sequence="110"
  UseShortId="true"
  PermissionsString="ViewPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_EditPage"
  Text="<%$Resources:wss,siteactions_editpage15%>"
  Description="<%$Resources:wss,siteactions_editpagedescriptionv4%>"
  ImageUrl="/_layouts/15/images/ActionsEditPage.png?rev=32"
  MenuGroupId="200"
  Sequence="210"
  PermissionsString="EditListItems"
  ClientOnClickNavigateUrl="javascript:ChangeLayoutMode(false);" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_CreatePage"
  Text="<%$Resources:wss,siteactions_addpage15%>"
  Description="<%$Resources:wss,siteactions_createpagedesc%>"
  ImageUrl="/_layouts/15/images/NewContentPageHH.png?rev=32"
  MenuGroupId="200"
  Sequence="220"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="OpenCreateWebPageDialog('~siteLayouts/createwebpage.aspx')"
  PermissionsString="AddListItems, EditListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Create"
  Text="<%$Resources:wss,siteactions_addapp15%>"
  Description="<%$Resources:wss,siteactions_createdesc%>"
  MenuGroupId="200"
  Sequence="230"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/addanapp.aspx')"
  PermissionsString="ManageLists, ManageSubwebs"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ViewAllSiteContents"
  Text="<%$Resources:wss,quiklnch_allcontent_15%>"
  Description="<%$Resources:wss,siteactions_allcontentdescription%>"
  ImageUrl="/_layouts/15/images/allcontent32.png?rev=32"
  MenuGroupId="200"
  Sequence="240"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/viewlsts.aspx"
  PermissionsString="ViewFormPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ChangeTheLook"
  Text="<%$Resources:wss,siteactions_changethelook15%>"
  Description="<%$Resources:wss,siteactions_changethelookdesc15%>"
  MenuGroupId="300"
  Sequence="310"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/designgallery.aspx"
  PermissionsString="ApplyThemeAndBorder,ApplyStyleSheets,Open,ViewPages,OpenItems,ViewListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Settings"
  Text="<%$Resources:wss,siteactions_settings15%>"
  Description="<%$Resources:wss,siteactions_sitesettingsdescriptionv4%>"
  ImageUrl="/_layouts/15/images/settingsIcon.png?rev=32"
  MenuGroupId="300"
  Sequence="320"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/settings.aspx')"
  PermissionsString="EnumeratePermissions,ManageWeb,ManageSubwebs,AddAndCustomizePages,ApplyThemeAndBorder,ManageAlerts,ManageLists,ViewUsageData"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_SwitchToMobileView"
  Visible="false"
  Text="<%$Resources:wss,siteactions_switchtomobileview%>"
  Description="<%$Resources:wss,siteactions_switchtomobileviewdesc%>"
  MenuGroupId="300"
  Sequence="330"
  UseShortId="true"
  ClientOnClickScript="STSNavigate(StURLSetVar2(ajaxNavigate.get_href(), 'mobile', '1'));" />
</SharePoint:FeatureMenuTemplate>
</CustomTemplate>
  </SharePoint:SiteActions></span>
</div>
<SharePoint:ScriptBlock runat="server">
var g_navBarHelpDefaultKey = "HelpHome";
</SharePoint:ScriptBlock>
<SharePoint:DelegateControl id="ID_SuiteBarDelegate" ControlId="SuiteBarDelegate" runat="server" />
</SharePoint:AjaxDelta>
```


#### <a name="learning-about-suite-navigation-web-controls-for-public-facing-sites"></a><span data-ttu-id="03759-127">Общие сведения о навигации набора веб-элементы управления для сайтов общедоступный</span><span class="sxs-lookup"><span data-stu-id="03759-127">Learning about Suite Navigation web controls for public-facing sites</span></span>

<span data-ttu-id="03759-p108">Общедоступный сайтов используйте следующую разметку главной страницы для элемента управления навигации набора приложений. В таблице 2 перечислены веб-элементы управления используются в коде набора навигации.</span><span class="sxs-lookup"><span data-stu-id="03759-p108">For public-facing sites, use the following master page markup for the Suite Navigation control. Table 2 lists web controls used in the Suite Navigation code.</span></span>
  
    
    

<span data-ttu-id="03759-130">**В таблице 2. Веб-элементы управления навигации Suite общедоступный сайтов**</span><span class="sxs-lookup"><span data-stu-id="03759-130">**Table 2. Suite Navigation web controls for public-facing sites**</span></span>


|<span data-ttu-id="03759-131">**веб-элемент управления**</span><span class="sxs-lookup"><span data-stu-id="03759-131">**Web Control**</span></span>|<span data-ttu-id="03759-132">**Описание**</span><span class="sxs-lookup"><span data-stu-id="03759-132">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="03759-133">SharePoint:DelegateControl</span><span class="sxs-lookup"><span data-stu-id="03759-133">SharePoint:DelegateControl</span></span>  <br/> |<span data-ttu-id="03759-p109">Отображение веб-элемент управления ASP.NET. Элементы управления делегат делают их кандидата элементы управления подключаемый и доступных для трассировки.</span><span class="sxs-lookup"><span data-stu-id="03759-p109">Renders an ASP.NET web control. Delegate controls make their candidate controls pluggable and traceable.</span></span>  <br/> |
|<span data-ttu-id="03759-136">SharePoint:FeatureMenuTemplate</span><span class="sxs-lookup"><span data-stu-id="03759-136">SharePoint:FeatureMenuTemplate</span></span>  <br/> |<span data-ttu-id="03759-137">Представляет элемент управления, который создает шаблон для отображения в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="03759-137">Represents a control that creates a template for a drop-down menu.</span></span>  <br/> |
|<span data-ttu-id="03759-138">SharePoint:Menu</span><span class="sxs-lookup"><span data-stu-id="03759-138">SharePoint:Menu</span></span>  <br/> |<span data-ttu-id="03759-139">Отображает меню на веб-странице ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03759-139">Displays a menu in an ASP.NET web page.</span></span>  <br/> |
|<span data-ttu-id="03759-140">SharePoint:MenuItemTemplate</span><span class="sxs-lookup"><span data-stu-id="03759-140">SharePoint:MenuItemTemplate</span></span>  <br/> |<span data-ttu-id="03759-141">Представляет элемент управления, который создает элемент в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="03759-141">Represents a control that creates an item in a drop-down menu.</span></span>  <br/> |
|<span data-ttu-id="03759-142">SharePoint:ScriptBlock</span><span class="sxs-lookup"><span data-stu-id="03759-142">SharePoint:ScriptBlock</span></span>  <br/> |<span data-ttu-id="03759-143">Представляет элемент управления блок скрипта на странице.</span><span class="sxs-lookup"><span data-stu-id="03759-143">Represents a script block control on a page.</span></span>  <br/> |
|<span data-ttu-id="03759-144">SharePoint:SiteActions</span><span class="sxs-lookup"><span data-stu-id="03759-144">SharePoint:SiteActions</span></span>  <br/> |<span data-ttu-id="03759-145">Представляет элемент управления шаблона для меню "Действия сайта".</span><span class="sxs-lookup"><span data-stu-id="03759-145">Represents a template control for the Site Action menu.</span></span>  <br/> |
|<span data-ttu-id="03759-146">SharePoint:SPSecurityTrimmedControl</span><span class="sxs-lookup"><span data-stu-id="03759-146">SharePoint:SPSecurityTrimmedControl</span></span>  <br/> |<span data-ttu-id="03759-147">Отображает условно содержимое элемента управления для текущего пользователя только в том случае, если текущий пользователь имеет разрешения, определенные в **PermissionString**.</span><span class="sxs-lookup"><span data-stu-id="03759-147">Renders conditionally the contents of the control to the current user only if the current user has permissions defined in the **PermissionString**.</span></span>  <br/> |
   

### <a name="suite-navigation-control-for-public-facing-sites"></a><span data-ttu-id="03759-148">Элемент управления навигацией Suite общедоступный сайтов</span><span class="sxs-lookup"><span data-stu-id="03759-148">Suite Navigation control for public-facing sites</span></span>


```

<SharePoint:AjaxDelta runat="server" id="suiteBarDelta" BlockElement="true" CssClass="ms-dialogHidden ms-fullWidth noindex">
  <SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AuthenticatedUsersOnly" EmitDiv="true">
<div id="suiteMenuData" class="ms-hide">
<wssuc:Welcome id="IdWelcomeData" runat="server" EnableViewState="false" RenderDataOnly="true"/>
   <span class="ms-siteactions-root" id="siteactiontd">
   <SharePoint:SiteActions runat="server" accesskey="<%$Resources:wss,tb_SiteActions_AK%>"
id="SiteActionsMenuMainData"
PrefixHtml=""
SuffixHtml=""
ImageUrl="/_layouts/15/images/spcommon.png?rev=32"
ThemeKey="spcommon"
MenuAlignment="Right"
LargeIconMode="false"
>
<CustomTemplate>
<SharePoint:Menu runat="server" Visible="false"/>
<SharePoint:FeatureMenuTemplate runat="server"
FeatureScope="Site"
Location="Microsoft.SharePoint.StandardMenu"
GroupId="SiteActions"
UseShortId="true"
>
  <SharePoint:MenuItemTemplate runat="server"
  id="MenuItem_ShareThisSite"
  Text="<%$Resources:wss,siteactions_sharethissite%>"
  Description="<%$Resources:wss,siteactions_sharethissitedescription%>"
  MenuGroupId="100"
  Sequence="110"
  UseShortId="true"
  PermissionsString="ViewPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_EditPage"
  Text="<%$Resources:wss,siteactions_editpage15%>"
  Description="<%$Resources:wss,siteactions_editpagedescriptionv4%>"
  ImageUrl="/_layouts/15/images/ActionsEditPage.png?rev=32"
  MenuGroupId="200"
  Sequence="210"
  PermissionsString="EditListItems"
  ClientOnClickNavigateUrl="javascript:ChangeLayoutMode(false);" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_CreatePage"
  Text="<%$Resources:wss,siteactions_addpage15%>"
  Description="<%$Resources:wss,siteactions_createpagedesc%>"
  ImageUrl="/_layouts/15/images/NewContentPageHH.png?rev=32"
  MenuGroupId="200"
  Sequence="220"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="OpenCreateWebPageDialog('~siteLayouts/createwebpage.aspx')"
  PermissionsString="AddListItems, EditListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Create"
  Text="<%$Resources:wss,siteactions_addapp15%>"
  Description="<%$Resources:wss,siteactions_createdesc%>"
  MenuGroupId="200"
  Sequence="230"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/addanapp.aspx')"
  PermissionsString="ManageLists, ManageSubwebs"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ViewAllSiteContents"
  Text="<%$Resources:wss,quiklnch_allcontent_15%>"
  Description="<%$Resources:wss,siteactions_allcontentdescription%>"
  ImageUrl="/_layouts/15/images/allcontent32.png?rev=32"
  MenuGroupId="200"
  Sequence="240"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/viewlsts.aspx"
  PermissionsString="ViewFormPages"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_ChangeTheLook"
  Text="<%$Resources:wss,siteactions_changethelook15%>"
  Description="<%$Resources:wss,siteactions_changethelookdesc15%>"
  MenuGroupId="300"
  Sequence="310"
  UseShortId="true"
  ClientOnClickNavigateUrl="~siteLayouts/designgallery.aspx"
  PermissionsString="ApplyThemeAndBorder,ApplyStyleSheets,Open,ViewPages,OpenItems,ViewListItems"
  PermissionMode="All" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_Settings"
  Text="<%$Resources:wss,siteactions_settings15%>"
  Description="<%$Resources:wss,siteactions_sitesettingsdescriptionv4%>"
  ImageUrl="/_layouts/15/images/settingsIcon.png?rev=32"
  MenuGroupId="300"
  Sequence="320"
  UseShortId="true"
  ClientOnClickScriptContainingPrefixedUrl="GoToPage('~siteLayouts/settings.aspx')"
  PermissionsString="EnumeratePermissions,ManageWeb,ManageSubwebs,AddAndCustomizePages,ApplyThemeAndBorder,ManageAlerts,ManageLists,ViewUsageData"
  PermissionMode="Any" />
  <SharePoint:MenuItemTemplate runat="server" id="MenuItem_SwitchToMobileView"
  Visible="false"
  Text="<%$Resources:wss,siteactions_switchtomobileview%>"
  Description="<%$Resources:wss,siteactions_switchtomobileviewdesc%>"
  MenuGroupId="300"
  Sequence="330"
  UseShortId="true"
  ClientOnClickScript="STSNavigate(StURLSetVar2(ajaxNavigate.get_href(), 'mobile', '1'));" />
</SharePoint:FeatureMenuTemplate>
</CustomTemplate>
  </SharePoint:SiteActions></span>
</div>
<SharePoint:ScriptBlock runat="server">
var g_navBarHelpDefaultKey = "HelpHome";
</SharePoint:ScriptBlock>
<SharePoint:DelegateControl id="ID_SuiteBarDelegate" ControlId="SuiteBarDelegate" runat="server" />
  </SharePoint:SPSecurityTrimmedControl>
```


## <a name="additional-resources"></a><span data-ttu-id="03759-149">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="03759-149">Additional resources</span></span>
<span data-ttu-id="03759-150"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="03759-150"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="03759-151">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="03759-151">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="03759-152">Новые возможности разработки сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="03759-152">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  
-  [<span data-ttu-id="03759-153">Menu control overview (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="03759-153">Menu control overview (ASP.NET)</span></span>](http://msdn.microsoft.com/ru-ru/library/ecs0x9w5%28v=vs.90%29.aspx.aspx)
    
  

