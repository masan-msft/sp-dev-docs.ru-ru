---
title: "Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript"
ms.date: 11/03/2017
ms.openlocfilehash: d5ab48173acb91fdcdfd0ce1ce4c57c86bef49a0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="customize-your-sharepoint-site-ui-by-using-javascript"></a><span data-ttu-id="debb3-102">Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="debb3-102">Customize your SharePoint site UI by using JavaScript</span></span>

<span data-ttu-id="debb3-103">Пользовательский Интерфейс сайт SharePoint можно обновить с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="debb3-103">You can update your SharePoint site's UI by using JavaScript.</span></span>
    
<span data-ttu-id="debb3-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="debb3-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="debb3-105">Пример надстройки [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) добавляет сообщение о состоянии панели всех страниц на сайте SharePoint и удаляет ссылку **новый дочерний сайт** на странице **Контент сайта** с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="debb3-105">The [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) sample add-in adds a status bar message to all pages on a SharePoint site, and removes the **new subsite** link from the **Site Contents** page by using JavaScript.</span></span> 
    
<span data-ttu-id="debb3-106">Используйте это решение, если вы хотите применить обновления пользовательского интерфейса на сайт SharePoint с помощью JavaScript (иногда называется способ внедрения JavaScript) вместо создания настраиваемых главных страниц.</span><span class="sxs-lookup"><span data-stu-id="debb3-106">Use this solution if you want to apply UI updates to your SharePoint site by using JavaScript (sometimes referred to as the Embed JavaScript technique) instead of creating custom master pages.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="debb3-107">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="debb3-107">Before you begin</span></span>
<span data-ttu-id="debb3-108"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="debb3-108"></span></span>

<span data-ttu-id="debb3-109">Чтобы начать работу, загрузите пример надстройки [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="debb3-109">To get started, download the  [Core.EmbedJavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreembedjavascript-app"></a><span data-ttu-id="debb3-110">С помощью приложения Core.EmbedJavaScript</span><span class="sxs-lookup"><span data-stu-id="debb3-110">Using the Core.EmbedJavaScript app</span></span>
<span data-ttu-id="debb3-111"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="debb3-111"></span></span>

<span data-ttu-id="debb3-112">При выполнении этого примера кода, размещение у поставщика в надстройке отображается, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="debb3-112">When you run this code sample, a provider-hosted add-in appears, as shown in Figure 1.</span></span> 

<span data-ttu-id="debb3-113">**На рисунке 1. Снимок экрана Core.EmbedJavaScript добавьте в начало страницы**</span><span class="sxs-lookup"><span data-stu-id="debb3-113">**Figure 1. Screen shot of Core.EmbedJavaScript add-in start page**</span></span>

![Снимок экрана с начальной страницы примера внедрения JavaScript](media/bdbf1df9-5027-4c6c-8ae9-152747fbbc1c.png)

<span data-ttu-id="debb3-115">Выбор **настройки Embed** настраивает сайт SharePoint с:</span><span class="sxs-lookup"><span data-stu-id="debb3-115">Choosing  **Embed customization** customizes the SharePoint site by:</span></span>

- <span data-ttu-id="debb3-116">Создание панели сообщение о состоянии на все страницы на сайте SharePoint, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="debb3-116">Creating a status bar message on all pages in the SharePoint site, as shown in Figure 2.</span></span>
    
- <span data-ttu-id="debb3-117">Удаление ссылок **нового дочернего сайта** из **Контент сайта** , как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="debb3-117">Removing the  **new subsite** link from **Site Contents** as shown in Figure 3.</span></span>

<span data-ttu-id="debb3-118">**На рисунке 2. Снимок экрана строка состояния, добавлен на все страницы**</span><span class="sxs-lookup"><span data-stu-id="debb3-118">**Figure 2. Screen shot of status bar added to all pages**</span></span>

![Строка состояния, добавлен на все страницы сайта SharePoint](media/ccae4093-4640-4339-a5f2-1df66c117cdc.png)

<span data-ttu-id="debb3-120">**На рисунке 3. Снимок экрана новой ссылки дочернего сайта, удалены из странице контент сайта**</span><span class="sxs-lookup"><span data-stu-id="debb3-120">**Figure 3. Screen shot of new subsite link removed from the Site Contents page**</span></span>

![Новый дочерний сайт ссылку на содержимое сайта было удалено.](media/0631ce39-76e8-446a-b628-f41c2a066e4c.png)

<span data-ttu-id="debb3-122">Выбор **настройки внедрить** на рисунке 1 вызывает **btnSubmit_Click** default.aspx.</span><span class="sxs-lookup"><span data-stu-id="debb3-122">In Figure 1, choosing  **Embed customization** calls **btnSubmit_Click** in default.aspx.</span></span> <span data-ttu-id="debb3-123">**btnSubmit_Click** вызывается **AddJsLink**, который выполняет следующие:</span><span class="sxs-lookup"><span data-stu-id="debb3-123">**btnSubmit_Click** calls **AddJsLink**, which does the following:</span></span>

1. <span data-ttu-id="debb3-124">Создает строку, представляющую определения блока скрипта.</span><span class="sxs-lookup"><span data-stu-id="debb3-124">Creates a string representing a script block definition.</span></span> <span data-ttu-id="debb3-125">Это определение блок скрипта указывает на файл JavaScript (scenario1.js), который находится на все страницы на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="debb3-125">This script block definition points to a JavaScript file (scenario1.js) which is included on all pages on the SharePoint site.</span></span> 
    
2. <span data-ttu-id="debb3-126">Использует [UserCustomActions](https://msdn.microsoft.com/library/office/microsoft.sharepoint.spweb.usercustomactions%28v=office.15%29.aspx) для получения всех пользовательских дополнительных действий определенных на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="debb3-126">Uses  [UserCustomActions](https://msdn.microsoft.com/library/office/microsoft.sharepoint.spweb.usercustomactions%28v=office.15%29.aspx) to get all user custom actions defined on the SharePoint site.</span></span> <span data-ttu-id="debb3-127">Удалить любые существующие ссылку на файл JavaScript с именем scenario1.js.</span><span class="sxs-lookup"><span data-stu-id="debb3-127">Any existing reference to a JavaScript file called scenario1.js is removed.</span></span>
    
3.  <span data-ttu-id="debb3-128">Создание нового настраиваемого действия и назначает определения блок скрипта, созданной на шаге 1 для нового настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="debb3-128">Creates a new custom action, and assigns the script block definition created in step 1 to the new custom action.</span></span>
    
4. <span data-ttu-id="debb3-129">Добавление нового настраиваемого действия на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="debb3-129">Adds the new custom action to the website.</span></span>
    
<span data-ttu-id="debb3-130">Все страницы на сайте SharePoint, теперь можно было запускать scenario1.js и отображения настройки интерфейса пользователя, показано на рисунке 2 и на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="debb3-130">All pages on your SharePoint site will now run scenario1.js and display the UI customizations shown in Figure 2 and Figure 3.</span></span>
    
<span data-ttu-id="debb3-131">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="debb3-131">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="debb3-132">SharePoint использует стратегия минимальной загрузки (MDS) для сокращения объема данных, браузер загружает при переходе между страницами на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="debb3-132">SharePoint uses Minimal Download Strategy (MDS) to reduce the amount of data the browser downloads when users navigate between pages on a SharePoint site.</span></span> <span data-ttu-id="debb3-133">[Стратегия минимальной загрузки](https://msdn.microsoft.com/library/office/dn456544%28v=office.15%29.aspx)Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="debb3-133">For more information, see  [Minimal Download Strategy overview](https://msdn.microsoft.com/library/office/dn456544%28v=office.15%29.aspx).</span></span> <span data-ttu-id="debb3-134">В scenario1.js следующий код гарантирует, что ли сайт SharePoint использует стратегия минимальной загрузки, **RemoteManager_Inject** всегда выполняется.</span><span class="sxs-lookup"><span data-stu-id="debb3-134">In scenario1.js, the following code ensures that whether or not your SharePoint site uses Minimal Download Strategy,  **RemoteManager_Inject** always runs.</span></span>

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

<span data-ttu-id="debb3-135">На сайте SharePoint, **RemoteManager_Inject** выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="debb3-135">**RemoteManager_Inject** performs the following tasks on your SharePoint site:</span></span>

- <span data-ttu-id="debb3-136">Создает в строке состояния на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="debb3-136">Creates a status bar on the host web.</span></span>  <span data-ttu-id="debb3-137">**RemoteManager_Inject** использует [SP. SOD.executeOrDelayUntilScriptLoaded](https://msdn.microsoft.com/library/office/ff411788%28v=office.14%29.aspx) для обеспечения sp.js для начала загрузки до вызова метода **SetStatusBar** для добавления в строке состояния на сайт.</span><span class="sxs-lookup"><span data-stu-id="debb3-137">**RemoteManager_Inject** uses [SP.SOD.executeOrDelayUntilScriptLoaded](https://msdn.microsoft.com/library/office/ff411788%28v=office.14%29.aspx) to ensure sp.js is loaded first, before calling **SetStatusBar** to add the status bar to the site.</span></span> <span data-ttu-id="debb3-138">Так как асинхронной загрузки файлов JavaScript, с помощью **SP. SOD.executeOrDelayUntilScriptLoaded** обеспечивает файл JavaScript (sp.js) загружается перед код вызывает функцию, определенную в этот файл JavaScript.</span><span class="sxs-lookup"><span data-stu-id="debb3-138">Because JavaScript files load asynchronously, using **SP.SOD.executeOrDelayUntilScriptLoaded** ensures your JavaScript file (sp.js) is loaded before your code calls a function defined in that JavaScript file.</span></span>
    
- <span data-ttu-id="debb3-139">Скрывает ссылки **нового дочернего сайта** на странице **Контент сайта** .</span><span class="sxs-lookup"><span data-stu-id="debb3-139">Hides the  **new subsite** link on the **Site Contents** page.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="debb3-140">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="debb3-140">Additional resources</span></span>
<span data-ttu-id="debb3-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="debb3-141"></span></span>

-  [<span data-ttu-id="debb3-142">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="debb3-142">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="debb3-143">Core.JavaScriptCustomization</span><span class="sxs-lookup"><span data-stu-id="debb3-143">Core.JavaScriptCustomization</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
    
-  [<span data-ttu-id="debb3-144">Как: настраивать представление списка в надстройках для SharePoint с использованием обработки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="debb3-144">How to: Customize a list view in add-ins for SharePoint using client-side rendering</span></span>](https://msdn.microsoft.com/library/8d5cabb2-70d0-46a0-bfe0-9e21f8d67d86.aspx)
