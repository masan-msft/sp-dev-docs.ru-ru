---
title: "Изолированная преобразования руководство по решениям для-получатели компонентов."
ms.date: 11/03/2017
ms.openlocfilehash: 91430d1523ad40acba163b86d369958f7273f219
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sandbox-solution-transformation-guidance---feature-receivers"></a>Изолированная преобразования руководство по решениям для-получатели компонентов. 
Преобразования или преобразования на основе кода изолированных решений в объектная модель SharePoint. Сведения о стратегии преобразования существующей функциональности объектная модель SharePoint или альтернативных решений и параметры.

_**Применимо к:** Add-ins for SharePoint | SharePoint 2013 | SharePoint 2016 | SharePoint Online_


## <a name="summary"></a>Summary
Приемники компонентов обычно используются для применения к сайтам SharePoint вида конфигурации или параметры при активации компонента или при создании сайта (если в веб-шаблон аудио- и веб-шаблон, соответствующий компонент). Приемники компонентов были развернуты с помощью изолированных решений в SharePoint Online, но с момента с возможностью настройки не могут не logner использоваться, альтернативные разработки необходимо принять. 

Подхода, можно обрабатывать приемники компонента в SharePoint немного отличаться в объектная модель SharePoint, от полного доверия кодом или в закодированные изолированные решения. Необходимо будет повторно создать решение в нет на месте, использование удаленных интерфейсов API (CSOM/REST) для применения необходимых конфигураций на сайты, которые ранее существовавшего в receiver(s) компонента. 


## <a name="options-for-replacing-feature-receivers"></a>Параметры для замены получатели компонентов.
<a name="sectionSection2"> </a>

|**Подход**|**Дополнительные сведения**|
|:-----|:-----|
|PowerShell на основе настроек|<p>Использование скриптов PowerShell для подготовки новых семейств сайтов (и потенциально sub сайтам) там, где необходимых настроек, применяются использование удаленных интерфейсов API. Обычно это делается в приложениях с помощью CSOM и напрямую скриптов PowerShell или с помощью команды PnP PowerShell, который предоставляет простой способ изменения сайтов и контента удаленно.</p><p><lu><li>[PnP модуля подготовки](https://github.com/SharePoint/PnP-PowerShell)</li><li>[PnP PowerShell - Приступая к работе с последними обновлениями](http://dev.office.com/blogs/pnp-powershell-getting-started-with-latest-updates)</li></lu></p>|
|Настройки на основе кода|<p>Можно применить необходимые настройки, также с помощью управляемого кода с помощью API удаленного. Это означает, что либо применяются их как часть административные операции при создании сайта или применить настройки для SharePoint, которое будет подключено в коде в качестве части элементов пользовательского интерфейса, как, overiding логику создания сайта sub , таким образом, можно связать настроек в рамках подготовки логики.</p><p><lu><li>[Удаленный подготовки шаблон для создания сайтов sub](https://channel9.msdn.com/blogs/OfficeDevPnP/Using-remote-provisioning-pattern-for-sub-site-creation)</li><li>[Компонент основной PnP CSOM](https://github.com/SharePoint/PnP-sites-core)</li></lu></p>|

## <a name="design-considerations"></a>Рекомендации по проектированию
### <a name="powershell-based-provisioning"></a>PowerShell на основе подготовки
В этой модели прекрасно работает, если вашей подготовки модели сайтов основано на административных действий.
- Требуется ли скрипт для выполнения, который применяет необходимые настройки создаваемые сайты
- Можно сочетать процедуры создания сайтов, если выполняемые административные операции
- Не требуется инфраструктуры размещения.
- Невозможно автоматически объединить в рамках процесса создания сайта sub

### <a name="code-based-provisioning"></a>На основе кода подготовки
- Может потребоваться инфраструктуры, размещения, если в сочетании с операций конечного пользователя
- Можно использовать управляемый код, который выполняется в любом месте с помощью API-интерфейсы CSOM/REST для необходимых операций
- Можно использовать для переопределения Создание ссылки на сайт sub позволяют интегрировать в SharePoint
- Можно автоматизировать семейства веб-сайтов и дочерних сайта подготовки использование удаленных интерфейсов API

> Если вы хотите предоставить автоматического способ применения необходимые удаленный код в процессе создания логики сайта sub, необходимо переопределить sub ссылки на сайт с помощью пользовательских дополнительных действий. Этот параметр используется только availale на сайтах, которые используете классический режим вокруг библиотек и списков. 


## <a name="reference-approaches"></a>Справочник по подходов
### <a name="applying-needed-customizations-to-sites-using-powershell"></a>Применение необходимые настройки сайтов с помощью PowerShell
Вот простой скрипт, который использует PnP PowerShell Отправка цвет темы файла с компьютера к SharePoint Online и активирует, на сайте SharePoint. 

> В этом примере использует [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell), который содержит более 150 командлеты PowerShell предназначены для конфигурации сайта и управления активами. 

```postscript 

Connect-SPOnline –Url https://yoursite.sharepoint.com/ –Credentials (Get-Credential)
Add-SPOFile -Path c:\temp\company.spcolor -Folder /_catalogs/theme/15/
Set-SPOTheme -ColorPaletteUrl /_catalogs/theme/15/company.spcolor

```

### <a name="applying-needed-customizations-to-sites-using-code"></a>Применение необходимые настройки сайтов, с помощью кода
Здесь — это простой код, использующий SharePoint Online CSOM для активации пользовательской темы, сначала Отправка активов на сайт SharePoint и последующей активации пользовательской темы. 

> В этом примере использует [PnP CSOM основных компонента](https://github.com/SharePoint/PnP-sites-core), который расширяет собственным из поля операций, краткие сведения о дополнительных набор методов для общих операций. Также же операции можно выполнить с помощью собственного CSOM, но будет значительно более сложного кода.

```csharp

// Upload assets to theme folder
clientContext.Site.RootWeb.UploadThemeFile(
        HostingEnvironment.MapPath(string.Format("~/{0}", "Resources/Themes/SPC/SPCTheme.spcolor")));
clientContext.Site.RootWeb.UploadThemeFile(
        HostingEnvironment.MapPath(string.Format("~/{0}", "Resources/Themes/SPC/SPCbg.jpg")));

Web web = clientContext.Web;
// loading RootWeb.ServerRelativeUrl property;
clientContext.Load(clientContext.Site, w => w.RootWeb.ServerRelativeUrl); 
clientContext.ExecuteQuery();
// Let's first upload the contoso theme to host web, if it does not exist there
web.CreateComposedLookByUrl("Contoso",
                clientContext.Site.RootWeb.ServerRelativeUrl + "/_catalogs/theme/15/SPCTheme.spcolor",
                null,
                clientContext.Site.RootWeb.ServerRelativeUrl + "/_catalogs/theme/15/SPCbg.jpg",
                string.Empty);

// Setting the Contoos theme to host web
web.SetComposedLookByUrl("Green");

```

При использовании подхода на основе кода, рекомендуется использовать для управления шаблона, который будет существенно упростить разработку [PnP модуля подготовки](http://dev.office.com/blogs/sharepoint-pnp-remote-provisioning-engine-august-2016) . 

## <a name="removing-sandbox-solution-containing-feature-receiver-code-from-your-site"></a>Удаление изолированного решения, содержащий код приемника компонента с веб-узла
<a name="sectionSection3"></a> При решении изолированной среды содержит логику приемников компонента для отключения компонента и не важно, что те, которые выполняются, перед окончательным удалением с возможностью поддержки, следует убедиться, отключаются, что подобные возможности перед Поддержка с возможностью отключена из SharePoint Online. Изолированные решения можно удалить из SharePoint Online после поддержка с возможностью отключена, но не будет выполняться код приемника компонента, несмотря на то, что функции начало перемещаются из сайта. 

При отключении существующего изолированного решения с сайтов, все файлы развернуты с помощью декларативных параметров не будут удалены, однако или активы компонента автоматически быть отключена. Выполнение кода в приемник компонента, зависит от времени при отключении изолированные решения. 


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>
-  [Удаление на основе кода изолированных решений в SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [Руководство по преобразованию изолированных решений](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/blob/master/README.md) - сценарий на основе настроек
-  [Обучение PnP основных CSOM](https://blogs.msdn.microsoft.com/vesku/2016/04/12/office-dev-pnp-core-componenttraining-package/) - кода на основе параметров
