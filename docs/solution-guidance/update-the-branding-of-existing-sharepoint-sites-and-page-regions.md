---
title: "Фирменная символика существующих сайтов SharePoint и области страницы обновления"
ms.date: 11/03/2017
ms.openlocfilehash: 16a4e6aa21f267c008660837b765e2bd2e47a940
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="update-the-branding-of-existing-sharepoint-sites-and-page-regions"></a>Фирменная символика существующих сайтов SharePoint и области страницы обновления

Настройка, а затем обновите фирменной настройки существующих сайтов SharePoint или областей страниц SharePoint, включая ленту, структуры переходов сайта, в меню Параметры, представлении дерева и содержимого страницы.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Можно обновить фирменной символики на существующих сайтах SharePoint и семейств веб-сайтов, а также настраивать области страниц SharePoint. Можно сделать, например, при обновлении до новой версии сайта. 

## <a name="refresh-branding-of-existing-sites-and-subsites"></a>Обновить фирменной настройки существующих сайтов и дочерних сайтов

Образец [Branding.Refresh](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Branding.Refresh) в проекте [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев показано, как использовать библиотеку OfficeDevPnP.Core для итерации по существующих сайтов и дочерние сайты для проверки и обновления применения фирменной символики. В примере показано обновление фирменной символики сайта, но также может использоваться для выполните другие действия, такие как развертывание новой библиотеки в список сайтов или обновление настраиваемых действий, который был развернут во время подготовки. Можно использовать тот же самый процесс для перемещения существующих сайтов до новой версии.

Операция состоит из двух этапов:

- Получите сайтами, которые требуется обновить.
    
- Обновите сайты.

### <a name="step-one-get-the-sites-you-want-to-update"></a>Первый шаг: получение сайтов, которую требуется обновить

Во-первых ознакомьтесь со списком сайтов и дочерних сайтов, которые требуется обновить. Примера показано, как это сделать с помощью функции поиска, но другие параметры включают чтение из каталога сайтов или предоставления управления пользовательского интерфейса, где администраторы могут указать список. Следующий пример показывает способы использования функций поиска для создания списка.

```
// Get a list of sites. Search is one way to get this list, an alternative can be a site directory.
List<SiteEntity> sites = cc.Web.SiteSearchScopedByUrl("https://bertonline.sharepoint.com");

// Generic settings (apply changes on all webs or just root web).
bool applyChangesToAllWebs = true;

// Optionally further refine the list of returned site collections.
var filteredSites = from p in sites
                    where p.Url.Contains("13003")
                    select p;

List<SiteEntity> sitesAndSubSites = new List<SiteEntity>();
if (applyChangesToAllWebs)
{
  // You want to update all sites, so the list of sites is extended to all subsites.
  foreach (SiteEntity site in filteredSites)
  {
    sitesAndSubSites.Add(new SiteEntity() { Url = site.Url, 
                                            Title = site.Title, 
                                            Template = site.Template });
    GetSubSites(cc, site.Url, ref sitesAndSubSites);
  }
  sites = sitesAndSubSites;
}
```

Вызов **GetSubSites** является рекурсивный извлечении дерева дочернего сайта. После получило дерево Проверьте правильность число, возвращаемое перед тем как продолжить.

### <a name="step-two-update-the-branding"></a>Шаг 2: обновление фирменной символики

После выбора сайта для обработки, можно использовать OfficeDevPnP.Core методы для работы с сайта. Примера показано, как это сделать для фирменного стиля, но так же, как могут быть обработаны любой тип изменения.

В примере используется шаблон, который использует контейнер свойств web для хранения сведений о текущих параметрах. Код сначала считывает значения контейнера свойств веб-сайта и затем выполняет действие, которое подходит для каждого значения.

```
// Verify that you have a property bag entry.
string themeName = cc.Web.GetPropertyBagValueString(BRANDING_THEME, "");

if (!String.IsNullOrEmpty(themeName))
{
  // If no theme property bag entry, assume no theme has been applied.
  if (themeName.Equals(currentThemeName, StringComparison.InvariantCultureIgnoreCase))
  {
    // The applied theme matches to the theme you want to update.
    int? brandingVersion = cc.Web.GetPropertyBagValueInt(BRANDING_VERSION, 0);
    if (brandingVersion < currentBrandingVersion)
    {
      DeployTheme(cc, currentThemeName);
      // Set the web propertybag entries
      cc.Web.SetPropertyBagValue(BRANDING_THEME, currentThemeName);
      cc.Web.SetPropertyBagValue(BRANDING_VERSION, currentBrandingVersion);
    }
  }
  else
  {
    if (forceBranding)
    {
      DeployTheme(cc, currentThemeName);
      // Set the web propertybag entries.
      cc.Web.SetPropertyBagValue(BRANDING_THEME, currentThemeName);
      cc.Web.SetPropertyBagValue(BRANDING_VERSION, currentBrandingVersion);
    }
  }
}
```

Код, который затем обновляет темы не вызывает затруднений и основано на OfficeDevPnP.Core методы.

```
string themeRoot = Path.Combine(AppRootPath, String.Format(@"Themes\{0}", themeName));
string spColorFile = Path.Combine(themeRoot, string.Format("{0}.spcolor", themeName));
string spFontFile = Path.Combine(themeRoot, string.Format("{0}.spfont", themeName));
string backgroundFile = Path.Combine(themeRoot, string.Format("{0}bg.jpg", themeName));
string logoFile = Path.Combine(themeRoot, string.Format("{0}logo.png", themeName));

if (IsThisASubSite(cc.Url))
{
  // Retrieve the context of the root site of the site collection.
  using (ClientContext ccParent = new ClientContext(GetRootSite(cc.Url)))
  {
    ccParent.Credentials = cc.Credentials;
    cc.Web.DeployThemeToSubWeb(ccParent.Web, themeName, spColorFile, spFontFile, backgroundFile, "");
    cc.Web.SetThemeToSubWeb(ccParent.Web, themeName);
  }
}
else
{
  cc.Web.DeployThemeToWeb(themeName, spColorFile, spFontFile, backgroundFile, "");
  cc.Web.SetThemeToWeb(themeName);
}
```

## <a name="customize-regions-of-a-sharepoint-page"></a>Настройка областей страницы SharePoint

При целью является Настройка областей страницы SharePoint, можно использовать сочетание удаленного подготовки и пользовательские каскадные таблицы стилей (CSS) на файлы, связанные с областями страницы. Изначально затем, необходимо знать о том, какие файлы SharePoint связаны с различные регионы на странице SharePoint. 

**В таблице 1. Области страницы SharePoint и связанные с ними файлы**

|**Область страницы**|** Связанные файлы **|**Дополнительные сведения**|
|:-----|:-----|:-----|
|Лента|Какие-либо главные страницы по умолчанию. Соответствующий CSS: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Основной - body: #s4-рабочей области</p></li><li><p>Панель набора - слева: #suiteBarLeft</p></li><li><p>Панель набора - справа: #suiteBarRight</p></li><li><p>Контейнер ленты: #globalNavBox</p></li></ul>|Можно ли скрыть с помощью кнопки **сосредоточиться на содержимом** .|
|Набор навигации|Какие-либо главные страницы по умолчанию. |Можно ли скрыть с помощью кнопки **сосредоточиться на содержимом** .|
|Набор ссылок||Можно ли скрыть с помощью кнопки **сосредоточиться на содержимом** .|
|Меню приветствие|.master|Можно ли скрыть с помощью кнопки **сосредоточиться на содержимом** .|
|Меню "Параметры" или шестеренки|.master|Пример в разделе [FTC для КАМЕРУ - настраиваемые действия и свойства мешке записей из пакета обновления надстройки](http://blogs.msdn.com/b/vesku/archive/2013/10/02/ftc-to-cam-custom-actions-and-property-bag-entries.aspx).|
|Справка|.master||
|Контекстные вкладки ленты|Любой главной страницы по умолчанию.|Примеры см.: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/df1e4e32-ef58-4b51-8ac8-a8c3690e648b/sharepoint-2013-duplicate-contextual-tabs?forum=sharepointdevelopment" target="_blank">Контекстные вкладки повторяющихся SharePoint 2013</a></p></li><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/a3640d58-afe1-41d0-ac83-bd7886c37355/hide-a-contextual-ribbon-tab?forum=crmdevelopment" target="_blank">Скрытие вкладки контекстной ленте</a></p></li><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/201306cf-5874-4778-b773-f870c67cee94/hideshow-contextual-tab-on-click-event-of-subgrid?forum=crmdevelopment" target="_blank">Показать/скрыть контекстных вкладок на щелкните событие вложенной сетке</a></p></li></ul>|
|Панель быстрого доступа|.master|Можно ли скрыть с помощью кнопки **сосредоточиться на содержимом** .|
|Эмблема сайта|.master<p>Соответствующий CSS:.ms-sitelcon-img</p>||
|Верхней панели навигации|Панель навигации CSOM или JSOM<p>.master</p>Соответствующий CSS (не в режиме редактирования): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Новый элемент выбран:.ms-core-listMenu-horizontalBox li.static >.ms - core.listMenu-выбранного</p></li><li><p>Новый элемент меняющуюся: .mscore listMenu horizontalBox li.static > a.ms-core-listMenu-элемента: при наведении</p></li><li><p>Стрелка всплывающего:.ms-core-listMenu-horizontalBox .dynamic-children.additional фон</p></li><li><p>Элемент навигации (в соответствии с элементами меню верхнего уровня):.ms-core-listMenu-horizontalBox li.static >.ms основных listMenu элементов</p></li><li><p>Всплывающее окно: ul.dynamic.ms основных listMenu элемента</p></li><li><p>Контейнер всплывающего: ul.dynamic</p></li><li><p>Изменение ссылок:.ms-navedit-editLinksText > охватывать >.ms - метаданных</p></li></ul>Соответствующий CSS (в режиме редактирования): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Ссылку навигационная панель изменение режима:.ms-core-listMenu-horizontalBox.ms-core-listMenuEdit > tr > .msnavedit linkCell >.ms основных listMenu элементов</p></li><li><p>Добавление ссылки:.ms-core-listMenu-horizontalBox a.ms-navedit-addNewLink</p></li></ul>||
|Заголовок страницы|Соответствующий CSS (в режиме редактирования): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Заголовок страницы и заголовок страницы со ссылкой на:.ms основной заголовок,.ms основной заголовок</p></li><li><p>Кнопка Описание: #ms-pageDescriptionDiv</p></li><li><p>Описание: с расширением JS выноски mainElement</p></li><li><p>Стрелка поле Описание: с расширением JS выноски заостренная часть</p></li><li><p>Описание: с расширением JS выноски текста</p></li></ul>||
|Поле поиска|Панель навигации CSOM или JSOM<p>.master</p>Соответствующий CSS: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Граница поля поиска:.ms-поиск sb границы</p></li><li><p>Меняющаяся границы поля поиска:.ms-поиск sb границы: при наведении</p></li><li><p>Поиск границы при нажатии:.ms поиск sb borderFocused</p></li><li><p>Поля текстовое поле поиска:.ms-поиск sb-borderFocused</p></li><li><p>Текст поля поиска:.ms-поиск sb</p></li><li><p>Поля текстовое поле поиска:.ms-поиск sb поиск</p></li><li><p>Поиск</p></li></ul>||
|Левой области переходов|Панель навигации CSOM или JSOM<p>.master</p>|Дополнительные сведения содержатся: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms558975(v=office.14).aspx" target="_blank">Как: Настройка навигации в SharePoint Server</a></p></li><li><p><a href="http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02(Office.15).aspx" target="_blank">Управляемая навигация в SharePoint 2013</a></p></li></ul>|
|Просмотр дерева|.master|Дополнительные сведения см в [настройке встроенных навигатор Treeview](https://social.msdn.microsoft.com/Forums/sharepoint/en-US/dd4d49fd-e107-469d-b326-d37c86ff66b8/how-to-customize-the-builtin-treeview-navigator-?forum=sharepointcustomizationprevious).|
|Контент страницы|Страницы макета и контент страницы<br>Зона веб-частей и веб-частей<p>Соответствующий CSS (зона веб-частей и веб-частей):</p><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Зона веб-частей:.ms веб-части зонами</p></li><li><p>Веб часть лица:.ms-webpartzone ячейки</p></li><li><p>Заголовок веб-части:.ms-webpart-titleText</p></li><li><p>Веб-часть со ссылкой на:.ms веб-части titleText ></p></li><li><p>Веб часть тело:.ms-WPBody</p></li></ul>|Дополнительные сведения можно [как: создать макет страницы в SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx)|

Примеры использования связанные сведения о настройке областей на странице см в проекте [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев:

- [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
    
- [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Scenarios/Branding.Themes)

### <a name="required-minimal-content-placeholders-in-default-sharepoint-master-pages"></a>Требуется «Минимальная» заполнителей контента в главных страницах SharePoint по умолчанию

Главных страницах SharePoint требует использования заполнителей контента, которые отобразить основные элементы содержимого и структуры, должна поддерживать жизненный цикл страницы на странице SharePoint. В таблице 2 перечислены и описаны заполнителей контента.

**В таблице 2. Минимальные требуемые заполнителей контента главной страницы SharePoint**

|**Заполнитель контента**|**Содержит контент для**|
|:-----|:-----|
|PlaceHolderAdditionalPageHead|Дополнительные элементы в <head> раздел страницы.|
|PlaceHolderBodyAreaClass|Дополнительные стили в заголовке страницы.|
|PlaceHolderBodyLeftBorder|Элемент левая граница для основной части страницы.|
|PlaceHolderBodyRightBorder|Элемент справа для основной части страницы.|
|PlaceHolderCalendarNavigator|Выбор даты для перехода в календаре, когда на странице отображается календарь.|
|PlaceHolderFormDigest|Безопасный элемент управления «сводка формы».|
|PlaceHolderGlobalNavigation|Глобальная цепочка для переходов (навигации сверху).|
|PlaceHolderGlobalNavigationSiteMap|Карта сайта в глобальной навигации (в начало навигации).|
|PlaceHolderHorizontalNav|Верхнее меню переходов страницы (в начало навигации).|
|PlaceHolderLeftActions|Нижнем левом углу области переходов (навигации слева).|
|PlaceHolderLeftNavBar|Левой области переходов (навигации слева).|
|PlaceHolderLeftNavBarDataSource|Источник данных для левого меню переходов (навигации слева).|
|PlaceHolderLeftNavBarTop|Верхней левой области переходов (навигации слева).|
|PlaceHolderMain|Основное содержимое страницы (содержимое страницы).|
|PlaceHolderMiniConsole|Уровня страницы команды, такие как изменить страницу, История и Входящие ссылки на странице корпоративного вики-сайта.|
|PlaceHolderNavSpacer|Ширина левой области переходов (навигации слева).|
|PlaceHolderPageDescription|Описание содержимого страницы.|
|PlaceHolderPageImage|Значок страницы в левом верхнем углу страницы (ленты).|
|PlaceHolderPageTitle|Заголовок страницы (&lt;заголовок&gt;) (Page Title) отображается в строке заголовка окна браузера.|
|PlaceHolderPageTitleInTitle|Заголовок страницы (Page Title) отображается сразу под ее цепочкой. |
|PlaceHolderQuickLaunchBottom|В нижней части панели быстрого запуска навигации (в начало навигации).|
|PlaceHolderQuickLaunchTop|В верхней части панели быстрого запуска навигации (в начало навигации).|
|PlaceHolderSearchArea|Область, где поле поиска элемент управления отображается (поле поиска).|
|PlaceHolderSiteName|Имя узла (набора навигации).|
|PlaceHolderTitleAreaClass|Область заголовка страницы (набора навигации).|
|PlaceHolderTitleAreaSeparator|Теней в области заголовка (набора навигации).|
|PlaceHolderTitleBreadCrumb|Область заголовка контента цепочки переходов. |
|PlaceHolderTitleLeftBorder|Левая граница области заголовка (набора навигации).|
|PlaceHolderTitleRightMargin|Правое поле области заголовка (набора навигации).|
|PlaceHolderTopNavBar|Верхняя область переходов (навигации сверху).|
|PlaceHolderUtilities|Дополнительного содержимого, которые должны встречаться в нижней части страницы (содержимое страницы).|
|SPNavigation|Включает в себя операций, связанных с навигации.|
|WSSDesignConsole|Страницы, элементы управления для изменений страница находится в режиме редактирования.|

При удалении заполнителей контента, перечисленные в таблице 2 из в главную страницу SharePoint SharePoint возникает ошибка. Вы можете добавить заполнитель контента с помощью скрытых видимость скрывает содержимого из конечных пользователей.

Дополнительные сведения см в [Windows SharePoint Services по умолчанию главные страницы](https://msdn.microsoft.com/en-us/library/office/ms467402%28v=office.12%29.aspx) (в этой статье описываются функциональные возможности в SharePoint Services 3, но по-прежнему применяется контента). В разделе также [Работа с элементами управления заполнитель контента](https://support.office.com/en-us/article/Working-with-content-placeholder-controls-d8b87b85-d1ef-409d-a5c7-044890f89288?CorrelationId=517ec37c-89ef-40d9-b70e-54aa63ac994f&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

По умолчанию главной страницы SharePoint, такие как seattle.master и oslo.master содержат множество заполнителей более контента не требует SharePoint. Например, эти главные страницы состоят `<SharePoint:Themes runat="server">` и `<SharePoint.CssRegistration runat="server">` элементов управления.

Элементы управления **темы** и **CssRegistration** запуска во время жизненного цикла страницы. С помощью удаленного подготовки шаблона, можно использовать настраиваемое действие для добавления элемента управления сервера для регистрации настраиваемых CSS.

Заполнителей контента, которые не отображаются по-прежнему работает должным образом, но они создают содержимое будет пропущено исходного HTML-кода, который распознает браузеры. Заполнитель контента с `Visible="false"` скрыто.

**Важные:**  Не создавать настраиваемые заполнители в настраиваемых главных страниц, существующих в ожидания введите главных страницах, такие как Seattle.master и Oslo.master. Это приведет к аварийное исключения.

### <a name="sharepoint-online-suite-navigation-control"></a>Элемент управления SharePoint Online набора навигации

SharePoint Online об новой главной страницы разметки для элемента управления **Навигации Suite** , который отображает верхней панели навигации. Разметка по умолчанию для элемента управления **Навигации Suite** отличается в зависимости от того, является ли сайт интрасети или общедоступный. Для получения дополнительных сведений об элементе управления **Навигации Suite** и примеры кода для интрасети и сайтов общедоступный, можно добавить к главным страницам, содержатся в разделе [Управление SharePoint Online набора навигации](http://msdn.microsoft.com/library/ba93e5c0-e591-48d0-a716-a08ec7ef6cea%28Office.15%29.aspx).

### <a name="use-csom-to-customize-the-regions-of-a-sharepoint-page"></a>Настройте областей на странице SharePoint с помощью CSOM

Как правило рекомендуется использовать класс [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) для добавления или удаления ссылок и других элементов. Это значение variant SharePoint с использованием элемента [CustomAction](https://msdn.microsoft.com/en-us/library/office/ms460194.aspx) , который может распознавать как часть структура компонентов, если вы знакомы с помощью модели кода с полным доверием. Несмотря на то, что **настраиваемое действие** элемента и компонента framework подготовки шаблон специально не поддерживаются в клиентской объектной модели (CSOM), же идентификаторы расположение, доступные в элемент **CustomAction** можно использовать в коде CSOM .

```
<CustomAction
  RequiredAdmin = "Delegated | Farm | Machine"
  ControlAssembly = "Text"
  ControlClass = "Text"
  ControlSrc = "Text"
  Description = "Text"
  FeatureId = "Text"
  GroupId = "Text"
  Id = "Text"
  ImageUrl = "Text"
  Location = "Text"
  RegistrationId = "Text"
  RegistrationType = "Text"
  RequireSiteAdministrator = "TRUE" | "FALSE"
  Rights = "Text"
  RootWebOnly = "TRUE" | "FALSE"
  ScriptSrc = "Text"
  ScriptBlock = "Text"
  Sequence = "Integer"
  ShowInLists = "TRUE" | "FALSE"
  ShowInReadOnlyContentTypes = "TRUE" | "FALSE"
  ShowInSealedContentTypes = "TRUE" | "FALSE"
  Title = "Text"
  UIVersion = "Integer">
</CustomAction>
```

### <a name="customize-the-sharepoint-ribbon"></a>Настройка ленты SharePoint

При настройке ленты HTML-код, который сервер отображает присваивается имя класса, который нужно назначить настраиваемых стилей. Чтобы использовать эту функцию, перейдите в библиотеку стилей и создайте CSS-файла для каждого стиля, который нужно добавить на ленту. Можно добавить настраиваемые стили два раздела на ленте: **Элементы страницы** и **Стили текста.** Используйте следующий синтаксис для стилей, которые можно добавить:

- Для ** раздел страницы элементы **: `span.ms-rteElement-<yourowndefinedname>`. Кроме того можно использовать стили H1, H2, H3 или H4, который будет вставлено для текста, стиль применяется к.
    
- В разделе **Стили текста** : `.ms-rteEStyle-<yourowndefinedname>`.
    
В определении класса CSS, добавьте следующую строку: 

`-ms-name:"The name visual in the ribbon for your style";`

Теперь можно завершить определение сведений пользовательский класс CSS в пользовательский CSS-файл.

### <a name="customize-suite-navigation-on-a-web-part-page"></a>Настройка набора переходов на странице веб-частей

В SharePoint 2013 пользовательского интерфейса имеет современный внешний вид и функции, основанный на странице заголовков. Например Live заголовков отображаются на странице SharePoint 2013 по умолчанию по умолчанию. Верхней панели навигации позволяет пользователям просматривать и получать доступ к социального контента и OneDrive для бизнеса. Можно настроить внешний вид и функции из этих областей с помощью CSS и JavaScript.

После создания веб-страницы, добавьте скрипт редактор веб части (SEWP) недоступны зону веб-частей. Добавление на страницу кода JavaScript, можно использовать эту веб-часть. Можно добавить код JavaScript для SEWP, определяющая на верхней панели навигации по его **Ид_элемента**и скрыть его, задав его свойство visibility скрытых.

### <a name="customize-the-settings-menu-or-gear"></a>Настройка параметров меню или шестеренки

Записи [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) классов и свойств контейнера можно использовать для настройки меню Параметры любого сайта SharePoint, как показано в следующем примере кода.

```
public void AddCustomActions(ClientContext clientContext)
{
    // Add a site settings link if it doesn't already exist.
    if (!CustomActionAlreadyExists(clientContext, "Sample_CustomSiteSetting"))
    {
        // Add a site settings link.
        UserCustomAction siteSettingLink = clientContext.Web.UserCustomActions.Add();
        siteSettingLink.Group = "SiteTasks";
        siteSettingLink.Location = "Microsoft.SharePoint.SiteSettings";
        siteSettingLink.Name = "Sample_CustomSiteSetting";
        siteSettingLink.Sequence = 1000;
        siteSettingLink.Url = string.Format(DeployManager.appUrl, clientContext.Url);
        siteSettingLink.Title = "Modify Site Metadata";
        siteSettingLink.Update();
        clientContext.ExecuteQuery();
    }

    // Add a site actions link, if it doesn't already exist.
    if (!CustomActionAlreadyExists(clientContext, "Sample_CustomAction"))
    {
        UserCustomAction siteAction = clientContext.Web.UserCustomActions.Add();
        siteAction.Group = "SiteActions";
        siteAction.Location = "Microsoft.SharePoint.StandardMenu";
        siteAction.Name = "Sample_CustomAction";
        siteAction.Sequence = 1000;
        siteAction.Url = string.Format(DeployManager.appUrl, clientContext.Url); ;
        siteAction.Title = "Modify Site Metadata";
        siteAction.Update();
        clientContext.ExecuteQuery();
    }
}
```

### <a name="customize-the-tree-view"></a>Настройка представления дерева

Чтобы изменить ширину представления дерева, добавьте `<div>` теги тега дерева в главную страницу и назначьте классов CSS с атрибутом ширины стиля для `<div>`. Можно увеличить ширину панели **Быстрого запуска** навигации, добавив следующие определения стилей CSS-файл.

```
.ms-nav {
  width: 220 px;
}
```

### <a name="customize-page-content"></a>Настройка содержимого страницы

Требования для настройки содержимого страницы зависят от контента, при включении на странице. Для настройки меню « **Действия сайта** », можно использовать объект [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) для подготовки фирменной символики в веб-части.

При создании сайта публикации увидеть [как: создать макет страницы в SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx) чтобы освоить основы. Макеты страниц зависят от доступности класса [ContentTypeId](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.contenttypeid.aspx) в CSOM. Как и для других элементов, которые не доступны в CSOM можно использовать службы Windows Communication Foundation (WCF) для работы с **ContentTypeId** как временное.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint](SharePoint-site-branding-and-page-customization-solutions.md)
    
- [Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта](Branding-and-site-provisioning-solutions-for-SharePoint.md)
