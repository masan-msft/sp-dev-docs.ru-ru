---
title: "Настройка страниц сайта «современный»"
description: "Использовать настраиваемый фирменный стиль в SharePoint Online, добавления «современный» страницы программными средствами и добавление, удаление или обновление со стороны клиента веб-частей на страницах «современный»."
ms.date: 11/09/2017
ms.openlocfilehash: b22eabf437eab007a1f58a3ebfcb9c8b830805f8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="customizing-modern-site-pages"></a>Настройка страниц сайта «современный»

В 2016 взаимодействия «современный» страница была выпущена с SharePoint team. Страницы сайта современных рабочих групп быстро и легко автора и поддерживает расширенный мультимедийного содержимого. Кроме того, документы будут отображаться на любом устройстве, в браузере или из мобильного приложения SharePoint. 

Страницы SharePoint созданных с помощью веб-части, которые можно настроить в соответствии со своими потребностями. Можно добавить документы, видео, изображений, действия сайта, веб-каналы Yammer и другие. Выберите + входа и выберите веб-часть из панели элементов, чтобы добавить содержимое на страницу. Новый «выделена содержимого» веб-часть позволяет установить критерии, чтобы определенного содержимого динамически и автоматически заполняет в этой области страницы. С помощью платформы SharePoint, разработчики могут создавать настраиваемые веб-части, отображаются справа на панели элементов.

![](https://blogs.office.com/wp-content/uploads/2016/08/New-capabilities-in-SharePoint-Online-team-sites-including-integration-with-Office-365-Groups-1.gif)

В этой статье основное внимание уделяется вариантов расширения в рамках взаимодействия пользователя со страницы «современный». Если вы хотите узнать больше о функциональных возможностей, предоставляемых «современный» каждый раз, просмотрите [новые возможности в SharePoint Online веб-сайтов групп включая интеграцию с Office 365 группами](https://blogs.office.com/2016/08/31/new-capabilities-in-sharepoint-online-team-sites-including-integration-with-office-365-groups).

В оставшейся части этой статьи мы будем использовать «современный» для нового пользовательского интерфейса и «классический» для прежних версий пользовательского интерфейса. 

> [!IMPORTANT]
> Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».

## <a name="supported-customizations-for-modern-pages"></a>Поддерживаемые настроек для страниц «современный»

Число настройки, доступные для страниц «современный» отслеживает передовых и в этой статье, мы предлагаем сведения и примеры поддерживаемые параметры. Группы разработчиков SharePoint работает на другие варианты технической поддержки в будущем. В следующем списке приведено краткий обзор поддерживаемые возможности для «современный» страниц:

 - Настраиваемый фирменный стиль
 - Добавление «современный» страницы программными средствами
 - Добавление, удаление и обновление со стороны клиента веб-частей на страницах «современный»
 - Альтернативные макеты (Примечание на *Виртуальный Summit SharePoint*)

Эти настройки в настоящее время не поддерживается для «современный» страниц:

 - Добавление «классический» веб-частей на страницах «современный»
 - Настраиваемые CSS с помощью свойства web AlternateCSSUrl
 - Настраиваемый JavaScript, внедренные с помощью пользовательских дополнительных действий (Примечание на *Расширения Framework SharePoint*)
 - Настраиваемые главные страницы (расширенный фирменной символики будет поддерживаться более поздней версии с помощью альтернативных параметров)
 - Стратегия минимальной загрузки (MDS)

> [!NOTE]
> - Не рекомендуется совместное использование функции «современный» страница с «классический» порталов публикации SharePoint. По умолчанию функциональные возможности «современный» страница не включена «классический» публикации порталов SharePoint.
> - В 2017 июня [расширения Framework SharePoint занялся preview для разработчиков](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview). Использование этих расширений Framework SharePoint, можно управлять визуализации поля с помощью пользовательского кода и создание пользователя настраиваемых действий, выполняемых пользовательского кода. Для получения дополнительных сведений см [Overview of Framework расширения SharePoint](http://aka.ms/spfx-extensions). 
> - В 2017 мая, во время Summit виртуального SharePoint мы объявили об изменении [сайты обмена данными с макетами настраиваемая страница](https://blogs.office.com/2017/05/16/new-sharepoint-and-onedrive-capabilities-accelerate-your-digital-transformation/).  

<a name="themingimpact"> </a>
## <a name="custom-branding"></a>Настраиваемый фирменный стиль

Если использовать пользовательскую тему веб-узла, эта тема учитывается сайтами «современный» страницы, как показано в следующем примере.

*На рисунке 1. Современный страница с настраиваемой фирменной настройки поступающих от параметры темы*

<img src="media/modern-experiences/modern-page-with-custom-theme.png" alt="Modern page with custom branding coming from theme settings" width="600">

<a name="sitesversusmodernpages"> </a>
## <a name="why-a-site-may-not-have-modern-pages-functionality"></a>Почему сайта не предусмотрено функциональные возможности «современный» страниц

«Современный» страницы будут доставляться с помощью компонента уровня веб-страниц сайта (B6917CB1-93A0-4B97-A84D-7CF49975D4EC), поэтому при активации этого компонента веб-узла есть параметр, чтобы использовать «современный» страницы. Когда Microsoft для развертывания этой функции, мы включено это для всех сайтов «современный» team (ГРУППА #0 сайтов), а также для большинства «классический» веб-сайтов групп (STS #0). 

Если сайт группы «классический» наибольшее количество веб-частей или вики-страницы, компонент не был включен автоматически и то же самое применяется к веб-сайтов «классический» групп с помощью функции публикации включен. Если необходимо, чтобы функциональность «современный» страницы на этих сайтах, по-прежнему можно включить функцию страниц сайта. Это также означает, что на основании других шаблонах узлов нет доступных функциональных возможностей «современный» страниц. 

Выше говорили о как компонента «современный» страница была включена на существующих сайтах. При создании нового «современный» или «классический» сайт группы (ГРУППА #0 или STS #0), «современный» страниц сайта она включена во время подготовки. На веб-сайтах, основанных на другие шаблоны не включается «современный» компонент страницы сайта.

<a name="configuremodernpages"> </a>
## <a name="configuring-the-end-user-experience"></a>Настройка конечных пользователей

Имеется несколько возможностей для управления ли использовать взаимодействия пользователя со страницы «современный» или «классический». 

### <a name="tenant-level-configuration"></a>Конфигурирование на уровне клиента

Если необходимо полностью отключить «современный» качества, рекомендуется использовать параметр базы данных для клиента. Перейдите в центр администрирования клиента (например, contoso-admin.sharepoint.com), перейдите в раздел Параметры и выберите «классический» качества.

*На рисунке 2. Раздел страницы сайта в SharePoint для клиентов, областью действия параметров в пользовательский Интерфейс администрирования*

![Раздел страницы сайта в SharePoint для клиентов, областью действия параметров в пользовательский Интерфейс администрирования](media/modern-experiences/site-pages-setting-admin-ui.png)

> [!NOTE]
> - Установка уровня клиента может быть несколько некоторая путаница; **Запретить пользователям Создание страниц сайта** фактически возвращает «классический» качества.
> - Кэширования текущей конфигурации и приемку сеанса сразу же показано влияние это изменение.

### <a name="web-level-configuration"></a>Уровень веб-конфигурации

Вы можете запретить веб-сайт с помощью взаимодействия пользователя со страницы «современный», отключив функцию уровня веб-сайта с Идентификатором **B6917CB1-93A0-4B97-A84D-7CF49975D4EC** (имя = «Страницы сайта»). Чтобы повторно включить взаимодействия пользователя со страницы «современный» на уровне веб-, необходимо снова включить функцию.

Чтобы включить или отключить необходимых компонентов с помощью следующих [PnP PowerShell](http://aka.ms/sppnp-powershell) :

```PowerShell
# Connect to a site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Prevent site pages at web level
Disable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
# And again enable site pages at web
#Enable-PnPFeature -Identity B6917CB1-93A0-4B97-A84D-7CF49975D4EC -Scope Web 
```

> [!NOTE]
> При отключении компонента, больше не создаются новые страницы «современный», но уже созданную страниц всегда оставаться на работу с помощью «современный» пользовательского интерфейса. 

### <a name="commenting-configuration"></a>Комментирования конфигурации

По умолчанию пользователи могут добавлять комментарии (июля 2017) на страницах «современный». Если ваша организация не требуется эта функция, она может быть отключена от клиента центра администрирования на странице "Параметры".

*На рисунке 3. Включение или отключение комментариев*

![Включение или отключение комментариев](http://i.imgur.com/atl91Vh.png)

> [!NOTE]
> Можно также программными средствами управлять комментирования поведение с помощью сайта и клиентов интерфейсы API (требуется SharePoint со стороны клиента объектной модели (CSOM) версии 16.1.6621.1200 или более поздней версии):
> - Microsoft.Online.SharePoint.TenantAdministration.SiteProperties.CommentsOnSitePagesDisabled 
> - Microsoft.SharePoint.Client.Site.CommentsOnSitePagesDisabled


## <a name="programming-modern-pages"></a>Программирование «современный» страниц

### <a name="adding-modern-pages"></a>Добавление страниц «современный»
Создание страницы «современный» сводится к Создание элемента списка в библиотеке страниц сайта и ее назначения правильный тип контента в сочетании с параметру некоторые дополнительные свойства, как показано в следующем фрагменте кода:

```C#
// pagesLibrary is List object for the "site pages" library of the site
ListItem item = pagesLibrary.RootFolder.Files.AddTemplateFile(serverRelativePageName, TemplateFileType.ClientSidePage).ListItemAllFields;

// Make this page a "modern" page
item["ContentTypeId"] = "0x0101009D1CB255DA76424F860D91F20E6C4118";
item["Title"] = System.IO.Path.GetFileNameWithoutExtension("mypage.aspx");
item["ClientSideApplicationId"] = "b6917cb1-93a0-4b97-a84d-7cf49975d4ec";
item["PageLayoutType"] = "Article";
item["PromotedState"] = "0";
item["CanvasContent1"] = "<div></div>";
item["BannerImageUrl"] = "/_layouts/15/images/sitepagethumbnail.png";
item.Update();
clientContext.Load(item);
clientContext.ExecuteQuery();

```

<br/>

При использовании PnP (по состоянию на выпуск 2017 марта), вы можете использовать возможности наших методы расширения, которое позволяет модели для добавления на страницу легко:

```C#
cc.Web.AddClientSidePage("mypage.aspx", true);
```

> [!IMPORTANT]
> По состоянию на сентябрь 2017, страниц, созданных с помощью `AddTemplateFile` метод имеет предварительного просмотра при наведении на странице результатов поиска. Корпорация Майкрософт работает на исправление/alternative решения базы данных для.

### <a name="using-the-pnp-support-for-modern-pages-and-client-side-web-parts"></a>С помощью PnP поддержки для клиентских веб-частей и страниц «современный»

По состоянию на выпуска 2017 марта [PnP сайты core библиотека](http://aka.ms/sppnp) поддерживает создание, обновление и удаление страницы со стороны клиента. В этом разделе представлены сведения о работе со страницы со стороны клиента с помощью [PnP сайты core библиотеки на репозиториев](https://github.com/SharePoint/PnP-Sites-Core).

#### <a name="create-a-new-page-and-add-a-text-web-part"></a>Создайте новую страницу и добавьте веб-часть текста

В этом примере мы создайте новую страницу со стороны клиента в памяти, добавление элемента управления редактора форматированного текста и наконец сохранить страницу в библиотеке страниц сайта с mypage.aspx. Первым шагом является создание экземпляра ClientSidePage, а затем мы создать элемент управления, который мы добавьте на страницу с помощью `AddControl` метод. После этого страница сохраняется.

```C#
// cc is the ClientContext instance for the site you're working with
ClientSidePage myPage = new ClientSidePage(cc);

ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks" };
myPage.AddControl(txt1, 0);
myPage.Save("mypage.aspx");
```

#### <a name="load-an-existing-page"></a>Загрузить существующей страницы 

Изменение или копирование существующей страницы, необходимо этой странице можно загрузить в PnP клиентской объектной модели; Загрузка «преобразований» HTML-контент в объектную модель, которую можно изменять. Загрузка существующей страницы выполняется с помощью `Load` метод.

```C#
// load the page with name "page3.aspx"
ClientSidePage p = ClientSidePage.Load(cc, "page3.aspx");

// perform your page updates
...

// save the page back to SharePoint
p.Save()
```

#### <a name="add-a-section"></a>Добавление раздела

Страницы могут иметь гибкий макет; можно добавить один или несколько разделов на странице, и эти разделы могут иметь до трех столбцов. Разделы можно добавить на страницы с помощью пользовательского интерфейса SharePoint или это можно сделать программным способом.

```C#
var page2 = cc.Web.AddClientSidePage("PageWithSections.aspx", true);
page2.AddSection(CanvasSectionTemplate.ThreeColumn, 5);
page2.AddSection(CanvasSectionTemplate.TwoColumn, 10);
```

#### <a name="add-an-out-of-the-box-web-part"></a>Добавление ожидания введите веб-части 
В следующем примере показано, как добавить клиентские веб-части вне поля **изображения** на странице. Обратите внимание, что мы экземпляра веб-части объект с помощью `InstantiateDefaultWebPart` вызова метода. После начала веб-части ее задано значение свойства по умолчанию, определенных в манифесте части web. Для большинства веб-частей вам потребуется обновить свойства, как показано в этом примере.

```C#
ClientSidePage page5 = new ClientSidePage(cc);
var imageWebPart = page5.InstantiateDefaultWebPart(DefaultClientSideWebParts.Image);
imageWebPart.Properties["imageSourceType"] = 2;
imageWebPart.Properties["siteId"] = "c827cb03-d059-4956-83d0-cd60e02e3b41";
imageWebPart.Properties["webId"] = "9fafd7c0-e8c3-4a3c-9e87-4232c481ca26";
imageWebPart.Properties["listId"] = "78d1b1ac-7590-49e7-b812-55f37c018c4b";
imageWebPart.Properties["uniqueId"] = "3C27A419-66D0-4C36-BF24-BD6147719052";
imageWebPart.Properties["imgWidth"] = 1002;
imageWebPart.Properties["imgHeight"] = 469;
page5.AddControl(imageWebPart);
page5.Save("page5.aspx");

```

#### <a name="add-a-custom-client-side-web-part"></a>Добавление настраиваемых со стороны клиента веб-части

Предыдущих примерах показано, как работать с ожидания введите веб-частями, но можно также добавить настраиваемые встроенные со стороны клиента веб-частей на страницу. Сначала необходимо получение часть информации в сети с помощью `AvailableClientSideComponents` метод и выполните поиск веб-часть и сведения, поиск для создания экземпляра `ClientSideWebPart` экземпляра, который добавляется на страницу на предыдущем этапе.

```C#
ClientSidePage p = new ClientSidePage(cc);

// get a list of possible client side web parts that can be added
var components = p.AvailableClientSideComponents();

// Find our custom "HelloWord" web part
var myWebPart = components.Where(s => s.ComponentType == 1 && s.Name == "HelloWorld").FirstOrDefault();
if (myWebPart != null)
{
    // Instantiate a client side web part from our found web part information
    ClientSideWebPart helloWp = new ClientSideWebPart(myWebPart) { Order = 10 };
    // Add the custom client side web part to the page
    p.AddControl(helloWp);
}

// Persist the page to SharePoint
p.Save("PnPRocks.aspx");
```

#### <a name="adjust-control-order"></a>Измените порядок элементов управления
Существуют различные методы для управления порядком, в котором отображаются элементы управления на странице. — Это ключевой аспект `Order` атрибут на фактический элемент управления: список элементов управления сортироваться по значению, `Order` атрибут при созданный HTML-страницы, и порядок, в HTML-код также порядок во время отображения страницы.

```C#
// Set the order when initiating the control
ClientSideText txt1 = new ClientSideText() { Text = "PnP Rocks", Order = 5 };

// Set the order when you add the control to the page, in this case we want the control to be the first
myPage.AddControl(txt1, -1);

// Manipulate the control order on the page...e.g. move a control to the back
myPage.Controls[1].Order = 10;

```

#### <a name="delete-a-control"></a>Удаление элемента управления

Если вы хотите удалить элемент управления со страницы, просто можно вызвать `Delete` метод в элементе управления и сохранить страницу назад.

```C#
ClientSidePage deleteDemoPage = ClientSidePage.Load(cc, "page3.aspx");
deleteDemoPage.Controls[0].Delete();
deleteDemoPage.Save();
```

#### <a name="delete-a-page"></a>Удаление страницы 

И, наконец можно удалить страницу со стороны клиента.

```C#
ClientSidePage p = ClientSidePage.Load(cc, "deleteme.aspx");
p.Delete();
```

#### <a name="class-model"></a>Класс модели

На следующем рисунке показаны наиболее важные классы, которые вы будете работать с при использовании объектной модели PnP страницы со стороны клиента.

*На рисунке 4. PnP клиентской объектной модели*

![PnP клиентской объектной модели](media/pnpclientsideobjectmodel.png)

## <a name="additional-considerations"></a>Дополнительные сведения о выполнении

Постепенно описываются дополнительные параметры настройки для взаимодействия пользователя со страницы «современный». Эти параметры способ выравнивания в выпуске дополнительные возможности среды SharePoint. На данный момент нет расписание не точное, но при выпуске новых возможностей взаимодействия «современный» статьи будут обновляться.

## <a name="see-also"></a>См. также

- [Настройка "современных" интерфейсов в SharePoint Online](modern-experience-customizations.md)
- [Разрешить или запретить создание современных веб-страниц конечными пользователями](https://support.office.com/en-us/article/Allow-or-prevent-creation-of-modern-site-pages-by-end-users-c41d9cc8-c5c0-46b4-8b87-ea66abc6e63b?ui=en-US&rs=en-US&ad=US)
