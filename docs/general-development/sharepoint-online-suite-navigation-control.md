---
title: "Элемент управления SharePoint Online набора навигации"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ba93e5c0-e591-48d0-a716-a08ec7ef6cea
ms.openlocfilehash: 531253b34f59c05693cef0c7905e48de0b5c2c89
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-online-suite-navigation-control"></a>Элемент управления SharePoint Online набора навигации
Сведения о главной страницы разметка для элемента управления навигации Suite, SharePoint Online. {вставьте введение}
  
    
    


## <a name="sharepoint-online-suite-navigation-control"></a>Элемент управления SharePoint Online набора навигации

Элемент управления навигацией Suite отображает согласованные верхняя панель навигации в SharePoint Online. Этот элемент управления теперь является частью все ненастраиваемые ожидания введите главной страницы.
  
    
    
Если главная страница была настроена, оно не получают новый элемент управления навигации набора приложений. Чтобы добавить этот элемент управления к настраиваемой главной страницы, замените  `suiteBar` `<div>` разметка, которая соответствует типу узла, который вы используете.
  
    
    
Новый элемент управления навигации Suite поддерживает любую тему, применяемых к сайту. Если вы хотите изменить цвет панели навигации верхнего уровня, применить тему.
  
    
    

> **Важные:** При настройке сайта, рекомендуется применять темы. При использовании настраиваемого CSS к сайту настраиваемого CSS могут быть разорваны в будущем Если элемент управления навигацией Suite обновляется еще раз в службе. 
  
    
    


> **Осторожность:** Если вы не хотите использовать новый элемент управления, удалите разметку набора навигации на главной странице и добавьте пользовательской разметки. Тем не менее Обратите внимание, что настраиваемые главные страницы риск не набор обновлений по умолчанию для элементов управления главную страницу или новые функциональные возможности, что ненастраиваемые главной страницы. Использование настраиваемой главной страницы создает риск, что обновления нарушит функциональные возможности или стилей веб-узла. 
  
    
    


### <a name="suite-navigation-control-for-intranet-sites"></a>Пакет управления навигации для сайтов интрасети

Для сайтов интрасети используйте следующую разметку главной страницы для элемента управления навигации набора приложений. В таблице 1 перечислены веб-элементы управления используются в коде набора навигации.
  
    
    

**В таблице 1. Веб-элементы управления навигации набора приложений для сайтов интрасети**


|**веб-элемент управления**|**Описание**|
|:-----|:-----|
|SharePoint:Menu  <br/> |Отображает меню на веб-странице ASP.NET.  <br/> |
|SharePoint:MenuItemTemplate  <br/> |Представляет элемент управления, который создает элемент в раскрывающемся меню.  <br/> |
   

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


#### <a name="learning-about-suite-navigation-web-controls-for-public-facing-sites"></a>Общие сведения о навигации набора веб-элементы управления для сайтов общедоступный

Общедоступный сайтов используйте следующую разметку главной страницы для элемента управления навигации набора приложений. В таблице 2 перечислены веб-элементы управления используются в коде набора навигации.
  
    
    

**В таблице 2. Веб-элементы управления навигации Suite общедоступный сайтов**


|**веб-элемент управления**|**Описание**|
|:-----|:-----|
|SharePoint:DelegateControl  <br/> |Отображение веб-элемент управления ASP.NET. Элементы управления делегат делают их кандидата элементы управления подключаемый и доступных для трассировки.  <br/> |
|SharePoint:FeatureMenuTemplate  <br/> |Представляет элемент управления, который создает шаблон для отображения в раскрывающемся меню.  <br/> |
|SharePoint:Menu  <br/> |Отображает меню на веб-странице ASP.NET.  <br/> |
|SharePoint:MenuItemTemplate  <br/> |Представляет элемент управления, который создает элемент в раскрывающемся меню.  <br/> |
|SharePoint:ScriptBlock  <br/> |Представляет элемент управления блок скрипта на странице.  <br/> |
|SharePoint:SiteActions  <br/> |Представляет элемент управления шаблона для меню "Действия сайта".  <br/> |
|SharePoint:SPSecurityTrimmedControl  <br/> |Отображает условно содержимое элемента управления для текущего пользователя только в том случае, если текущий пользователь имеет разрешения, определенные в **PermissionString**.  <br/> |
   

### <a name="suite-navigation-control-for-public-facing-sites"></a>Элемент управления навигацией Suite общедоступный сайтов


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


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Создание сайтов для SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Новые возможности разработки сайтов в SharePoint](what-s-new-with-sharepoint-site-development.md)
    
  
-  [Menu control overview (ASP.NET)](http://msdn.microsoft.com/en-us/library/ecs0x9w5%28v=vs.90%29.aspx.aspx)
    
  

