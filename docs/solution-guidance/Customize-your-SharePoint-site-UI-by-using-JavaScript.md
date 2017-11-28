---
title: "Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript"
ms.date: 11/03/2017
ms.openlocfilehash: d5ab48173acb91fdcdfd0ce1ce4c57c86bef49a0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="customize-your-sharepoint-site-ui-by-using-javascript"></a>Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript

Пользовательский Интерфейс сайт SharePoint можно обновить с помощью JavaScript.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Пример надстройки [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) добавляет сообщение о состоянии панели всех страниц на сайте SharePoint и удаляет ссылку **новый дочерний сайт** на странице **Контент сайта** с помощью JavaScript. 
    
Используйте это решение, если вы хотите применить обновления пользовательского интерфейса на сайт SharePoint с помощью JavaScript (иногда называется способ внедрения JavaScript) вместо создания настраиваемых главных страниц. 

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-coreembedjavascript-app"></a>С помощью приложения Core.EmbedJavaScript
<a name="sectionSection1"> </a>

При выполнении этого примера кода, размещение у поставщика в надстройке отображается, как показано на рисунке 1. 

**На рисунке 1. Снимок экрана Core.EmbedJavaScript добавьте в начало страницы**

![Снимок экрана с начальной страницы примера внедрения JavaScript](media/bdbf1df9-5027-4c6c-8ae9-152747fbbc1c.png)

Выбор **настройки Embed** настраивает сайт SharePoint с:

- Создание панели сообщение о состоянии на все страницы на сайте SharePoint, как показано на рисунке 2.
    
- Удаление ссылок **нового дочернего сайта** из **Контент сайта** , как показано на рисунке 3.

**На рисунке 2. Снимок экрана строка состояния, добавлен на все страницы**

![Строка состояния, добавлен на все страницы сайта SharePoint](media/ccae4093-4640-4339-a5f2-1df66c117cdc.png)

**На рисунке 3. Снимок экрана новой ссылки дочернего сайта, удалены из странице контент сайта**

![Новый дочерний сайт ссылку на содержимое сайта было удалено.](media/0631ce39-76e8-446a-b628-f41c2a066e4c.png)

Выбор **настройки внедрить** на рисунке 1 вызывает **btnSubmit_Click** default.aspx. **btnSubmit_Click** вызывается **AddJsLink**, который выполняет следующие:

1. Создает строку, представляющую определения блока скрипта. Это определение блок скрипта указывает на файл JavaScript (scenario1.js), который находится на все страницы на сайте SharePoint. 
    
2. Использует [UserCustomActions](https://msdn.microsoft.com/library/office/microsoft.sharepoint.spweb.usercustomactions%28v=office.15%29.aspx) для получения всех пользовательских дополнительных действий определенных на сайте SharePoint. Удалить любые существующие ссылку на файл JavaScript с именем scenario1.js.
    
3.  Создание нового настраиваемого действия и назначает определения блок скрипта, созданной на шаге 1 для нового настраиваемого действия.
    
4. Добавление нового настраиваемого действия на веб-сайт.
    
Все страницы на сайте SharePoint, теперь можно было запускать scenario1.js и отображения настройки интерфейса пользователя, показано на рисунке 2 и на рисунке 3.
    
**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
 public void AddJsLink(ClientContext ctx, Web web)
        {
            string scenarioUrl = String.Format("{0}://{1}:{2}/Scripts", this.Request.Url.Scheme, 
                                                this.Request.Url.DnsSafeHost, this.Request.Url.Port);
            string revision = Guid.NewGuid().ToString().Replace("-", "");
            string jsLink = string.Format("{0}/{1}?rev={2}", scenarioUrl, "scenario1.js", revision);

            StringBuilder scripts = new StringBuilder(@"
                var headID = document.getElementsByTagName('head')[0]; 
                var");

            scripts.AppendFormat(@"
                newScript = document.createElement('script');
                newScript.type = 'text/javascript';
                newScript.src = '{0}';
                headID.appendChild(newScript);", jsLink);
            string scriptBlock = scripts.ToString();

            var existingActions = web.UserCustomActions;
            ctx.Load(existingActions);
            ctx.ExecuteQuery();
            var actions = existingActions.ToArray();
            foreach (var action in actions)
            {
                if (action.Description == "scenario1" &amp;&amp;
                    action.Location == "ScriptLink")
                {
                    action.DeleteObject();
                    ctx.ExecuteQuery();
                }
            }

            var newAction = existingActions.Add();
            newAction.Description = "scenario1";
            newAction.Location = "ScriptLink";

            newAction.ScriptBlock = scriptBlock;
            newAction.Update();
            ctx.Load(web, s => s.UserCustomActions);
            ctx.ExecuteQuery();
        }
```

SharePoint использует стратегия минимальной загрузки (MDS) для сокращения объема данных, браузер загружает при переходе между страницами на сайте SharePoint. [Стратегия минимальной загрузки](https://msdn.microsoft.com/library/office/dn456544%28v=office.15%29.aspx)Дополнительные сведения см. В scenario1.js следующий код гарантирует, что ли сайт SharePoint использует стратегия минимальной загрузки, **RemoteManager_Inject** всегда выполняется.

```
// Is MDS enabled?
if ("undefined" != typeof g_MinimalDownload &amp;&amp; g_MinimalDownload &amp;&amp; (window.location.pathname.toLowerCase()).endsWith("/_layouts/15/start.aspx") &amp;&amp; "undefined" != typeof asyncDeltaManager) {
    // Register script for MDS if possible
    RegisterModuleInit("scenario1.js", RemoteManager_Inject); //MDS registration
    RemoteManager_Inject(); //non MDS run
} else {
    RemoteManager_Inject();
}
```

На сайте SharePoint, **RemoteManager_Inject** выполняет следующие задачи:

- Создает в строке состояния на хост-сайта.  **RemoteManager_Inject** использует [SP. SOD.executeOrDelayUntilScriptLoaded](https://msdn.microsoft.com/library/office/ff411788%28v=office.14%29.aspx) для обеспечения sp.js для начала загрузки до вызова метода **SetStatusBar** для добавления в строке состояния на сайт. Так как асинхронной загрузки файлов JavaScript, с помощью **SP. SOD.executeOrDelayUntilScriptLoaded** обеспечивает файл JavaScript (sp.js) загружается перед код вызывает функцию, определенную в этот файл JavaScript.
    
- Скрывает ссылки **нового дочернего сайта** на странице **Контент сайта** .

```
function RemoteManager_Inject() {

    loadScript(jQuery, function () {
        $(document).ready(function () {
            var message = "<img src='/_Layouts/Images/STS_ListItem_43216.gif' align='absmiddle'> <font color='#AA0000'>JavaScript customization is <i>fun</i>!</font>"

            // Execute status setter only after SP.JS has been loaded
            SP.SOD.executeOrDelayUntilScriptLoaded(function () { SetStatusBar(message); }, 'sp.js');

            // Customize the viewlsts.aspx page
            if (IsOnPage("viewlsts.aspx")) {
                //hide the subsites link on the viewlsts.aspx page
                $("#createnewsite").parent().hide();
            }
        });
    });
}

function SetStatusBar(message) {
    var strStatusID = SP.UI.Status.addStatus("Information : ", message, true);
    SP.UI.Status.setStatusPriColor(strStatusID, "yellow");
}

function IsOnPage(pageName) {
    if (window.location.href.toLowerCase().indexOf(pageName.toLowerCase()) > -1) {
        return true;
    } else {
        return false;
    }
}

```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
    
-  [Как: настраивать представление списка в надстройках для SharePoint с использованием обработки на стороне клиента](https://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86.aspx)
