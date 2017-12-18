---
title: "Локализация пользовательского интерфейса элементов пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 2bf8abc77c9cbe3058fba8544400bea1a6b405c7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="localize-ui-elements-sample-add-in-for-sharepoint"></a><span data-ttu-id="0a982-102">Локализация пользовательского интерфейса элементов пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a982-102">Localize UI elements sample add-in for SharePoint</span></span>

<span data-ttu-id="0a982-103">Элементы пользовательского интерфейса SharePoint можно локализовать с помощью JavaScript для замены текстовое значение значение элемента пользовательского интерфейса со значением переведенный текст, загруженными из файла ресурсов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0a982-103">You can localize SharePoint UI elements by using JavaScript to replace the text value of a UI element value with a translated text value loaded from a JavaScript resource file.</span></span> 

<span data-ttu-id="0a982-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="0a982-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="0a982-105">Пример надстройки [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) показано, как использовать JavaScript для замены текстового значения элементов пользовательского интерфейса SharePoint со значением переведенный текст, который считываются из файла ресурсов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0a982-105">The [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) sample add-in shows you how to use JavaScript to replace the text value of a SharePoint UI element with a translated text value, which is read from a JavaScript resource file.</span></span> 

> [!NOTE] 
> <span data-ttu-id="0a982-106">Вы несете ответственность за обеспечение значения переведенный текст в файле ресурсов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0a982-106">You are responsible for maintaining the translated text values in the JavaScript resource file.</span></span> 

<span data-ttu-id="0a982-107">В этом примере код использует размещение у поставщика в надстройке для:</span><span class="sxs-lookup"><span data-stu-id="0a982-107">This code sample uses a provider-hosted add-in to:</span></span>

- <span data-ttu-id="0a982-108">Локализация страница сайта или панели быстрого запуска ссылку заголовка с определенным текстовые значения.</span><span class="sxs-lookup"><span data-stu-id="0a982-108">Localize a site page or Quick Launch link title with specific text values.</span></span>
    
- <span data-ttu-id="0a982-109">Сохранить страницу сайта или панели быстрого запуска ссылку заголовка в основной язык, а также предоставлять переведенные версии веб-страницы и панели быстрого запуска title ссылку на другом языке во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="0a982-109">Preserve a site page or Quick Launch link title in a primary language, and provide translated versions of the site page and Quick Launch link title in another language at run time.</span></span>
    
- <span data-ttu-id="0a982-110">Использование файлов ресурсов JavaScript для локализации со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="0a982-110">Use JavaScript resource files for client side localization.</span></span>
    
- <span data-ttu-id="0a982-111">Ссылка на файл JavaScript на сайте SharePoint, с помощью дополнительного действия.</span><span class="sxs-lookup"><span data-stu-id="0a982-111">Link a JavaScript file to a SharePoint site using a custom action.</span></span>
    
- <span data-ttu-id="0a982-112">Проверьте региональные параметры пользовательского интерфейса веб-узла, а затем загружать значения текста для конкретного языка и региональных параметров из файла ресурсов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0a982-112">Check the UI culture of the site and then load culture-specific text values from a JavaScript resource file.</span></span>
    
- <span data-ttu-id="0a982-113">Замените значения текста для конкретного языка и региональных параметров с помощью jQuery страница сайта и заголовки ссылок на панели быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="0a982-113">Overwrite site page and Quick Launch link titles with culture-specific text values using jQuery.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0a982-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0a982-114">Before you begin</span></span>
<span data-ttu-id="0a982-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="0a982-115"></span></span>

<span data-ttu-id="0a982-116">Чтобы начать работу, загрузите пример надстройки [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="0a982-116">To get started, download the  [Core.JavaScriptCustomization](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="0a982-117">Прежде чем запустить этот пример кода Настройка языковых параметров на вашем сайте и задать язык отображения на странице профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="0a982-117">Before you run this code sample, configure the language settings on your site, and set the display language on your user's profile page.</span></span>

### <a name="to-configure-the-language-settings-on-your-site"></a><span data-ttu-id="0a982-118">Настройка языковых параметров сайта</span><span class="sxs-lookup"><span data-stu-id="0a982-118">To configure the language settings on your site</span></span>

1. <span data-ttu-id="0a982-119">На сайте группы выберите **Параметры** > **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="0a982-119">On your team site, choose  **Settings** > **Site settings**.</span></span>
    
2. <span data-ttu-id="0a982-120">**Администрирование веб-сайтов**выберите **языковые параметры**.</span><span class="sxs-lookup"><span data-stu-id="0a982-120">In  **Site Administration**, choose  **Language settings**.</span></span>
    
3. <span data-ttu-id="0a982-121">На странице **Языковых параметров** в **Альтернативные языки**выберите альтернативные языки, которые должны поддерживать веб-узла.</span><span class="sxs-lookup"><span data-stu-id="0a982-121">On the  **Language Settings** page, in **Alternate language(s)**, choose the alternate languages your site should support.</span></span> <span data-ttu-id="0a982-122">Например выберите **французский** и **финский**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="0a982-122">For example, choose  **French** and **Finnish**, as shown in Figure 1.</span></span>
    
4. <span data-ttu-id="0a982-123">Нажмите кнопку  **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0a982-123">Choose  **OK**.</span></span>

### <a name="to-set-the-display-language-on-your-users-profile-page"></a><span data-ttu-id="0a982-124">Чтобы задать язык отображения на странице профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="0a982-124">To set the display language on your user's profile page</span></span>

1. <span data-ttu-id="0a982-125">В верхней части сайта Office 365 выберите изображение профиля и выберите команду **сведения обо мне,** как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="0a982-125">At the top of your Office 365 site, choose your profile picture, and then choose  **About me,** as shown in Figure 2.</span></span>
    
2. <span data-ttu-id="0a982-126">На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.</span><span class="sxs-lookup"><span data-stu-id="0a982-126">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="0a982-127">Нажмите кнопку с многоточием (...) для Дополнительные параметры и затем выберите **языка и региона**.</span><span class="sxs-lookup"><span data-stu-id="0a982-127">Choose the ellipsis (...) for additional options, and then choose  **Language and Region**.</span></span>
    
4. <span data-ttu-id="0a982-128">На **Мой языки**нажмите кнопку Новый язык в раскрывающемся списке **выбрать новый язык** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a982-128">In  **My Display Languages**, choose a new language in the  **Pick a new language** dropdown, then choose **Add**.</span></span> <span data-ttu-id="0a982-129">Например выберите французский и финский, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="0a982-129">For example, choose French and Finnish, as shown in Figure 3.</span></span> <span data-ttu-id="0a982-130">Может потребоваться перемещение предпочитаемый язык вверх или вниз, выбрав вверх и вниз стрелки.</span><span class="sxs-lookup"><span data-stu-id="0a982-130">You might need to move your preferred language up or down by choosing the up and down arrows.</span></span>
    
5. <span data-ttu-id="0a982-131">Выберите команду **Сохранить все и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="0a982-131">Choose  **Save all and close**.</span></span>

> [!NOTE] 
> <span data-ttu-id="0a982-132">Выполнение может занять несколько минут для сайта отобразить в выбранные языки.</span><span class="sxs-lookup"><span data-stu-id="0a982-132">It might take a few minutes for your site to render in the selected language(s).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0a982-133">CSOM периодически добавлены новые функции.</span><span class="sxs-lookup"><span data-stu-id="0a982-133">The CSOM is periodically updated with new features.</span></span> <span data-ttu-id="0a982-134">Если CSOM предоставляет новые функции для обновления веб-страницы или панели быстрого запуска заголовки ссылок, рекомендуется использовать новые возможности в CSOM вместо описанные здесь.</span><span class="sxs-lookup"><span data-stu-id="0a982-134">If the CSOM provides new features to update site page or Quick Launch link titles, we recommend that you use the new features in the CSOM instead of the options discussed here.</span></span>

<span data-ttu-id="0a982-135">**На рисунке 1. Настройка языка для сайта**</span><span class="sxs-lookup"><span data-stu-id="0a982-135">**Figure 1. Setting the language for a site**</span></span>

![Снимок экрана, на странице параметров языковых параметров сайта](media/0265dd57-cf25-4879-a6df-68072ffa5270.png)

<span data-ttu-id="0a982-137">**На рисунке 2. Переход к странице профиля пользователя, выбрав сведения обо мне**</span><span class="sxs-lookup"><span data-stu-id="0a982-137">**Figure 2. Navigating to a user's profile page by choosing About me**</span></span>

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением](media/e3971203-7011-40ad-ab1b-341af2df28fc.png)

<span data-ttu-id="0a982-139">**На рисунке 3. Изменение языка интерфейса пользователя на странице профиля пользователя**</span><span class="sxs-lookup"><span data-stu-id="0a982-139">**Figure 3. Changing a user's display language settings on the user's profile page**</span></span>

![Снимок экрана раздела языка и региона на странице "Изменение сведений"](media/ff41b24e-42eb-48ca-83cd-00d88ef753bd.png)

<span data-ttu-id="0a982-141">Прежде чем запускать [сценарии 2](#bk_Scenario2) этот пример кода, выполните следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="0a982-141">Before you run  [Scenario 2](#bk_Scenario2) of this code sample, complete the following tasks.</span></span>

### <a name="to-create-a-quick-launch-link"></a><span data-ttu-id="0a982-142">Создание ссылки на панели быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="0a982-142">To create a Quick Launch link</span></span>

1. <span data-ttu-id="0a982-143">На хост-сайта выберите команду **Изменить СВЯЗИ**.</span><span class="sxs-lookup"><span data-stu-id="0a982-143">On the host web, choose  **EDIT LINKS**.</span></span>
    
2. <span data-ttu-id="0a982-144">Выберите **ссылку**, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="0a982-144">Choose  **link**, as shown in Figure 4.</span></span>
    
3. <span data-ttu-id="0a982-145">В **текст для отображения**введите **Моя запись панели быстрого запуска**.</span><span class="sxs-lookup"><span data-stu-id="0a982-145">In  **Text to display**, enter  **My quicklaunch entry**.</span></span>
    
4. <span data-ttu-id="0a982-146">В поле **адрес**введите URL-адрес веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="0a982-146">In  **Address**, enter the URL of a website.</span></span>
    
5. <span data-ttu-id="0a982-147">Нажмите **кнопку ОК,** > **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0a982-147">Choose  **OK** > **Save**.</span></span>

<span data-ttu-id="0a982-148">**На рисунке 4. Добавление ссылки на панели быстрого запуска**</span><span class="sxs-lookup"><span data-stu-id="0a982-148">**Figure 4. Adding a link to the Quick Launch**</span></span>

![Снимок экрана, на странице Изменение СВЯЗЕЙ со ссылкой на с выделением](media/fcb28647-1576-4e86-8ca7-15f3ce8d85fb.png)

### <a name="to-create-a-site-page"></a><span data-ttu-id="0a982-150">Создание страницы сайта</span><span class="sxs-lookup"><span data-stu-id="0a982-150">To create a site page</span></span>

1. <span data-ttu-id="0a982-151">На веб-сайт, щелкните **Содержимое сайта** > **Страниц сайта** > **новый**.</span><span class="sxs-lookup"><span data-stu-id="0a982-151">On the host web, choose  **Site Contents** > **Site Pages** > **new**.</span></span>
    
2. <span data-ttu-id="0a982-152">В поле **новое имя страницы** введите **Hello SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="0a982-152">In  **New page name,** enter **Hello SharePoint**.</span></span>
    
3. <span data-ttu-id="0a982-153">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0a982-153">Choose  **Create**.</span></span>
    
4. <span data-ttu-id="0a982-154">Введите **Тестовая страница** в теле страницы.</span><span class="sxs-lookup"><span data-stu-id="0a982-154">Enter  **Test page** in the body of the page.</span></span>
    
5. <span data-ttu-id="0a982-155">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0a982-155">Choose  **Save**.</span></span>

## <a name="using-the-corejavascriptcustomization-sample-app"></a><span data-ttu-id="0a982-156">Использование примера приложения Core.JavaScriptCustomization</span><span class="sxs-lookup"><span data-stu-id="0a982-156">Using the Core.JavaScriptCustomization sample app</span></span>
<span data-ttu-id="0a982-157"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="0a982-157"></span></span>

<span data-ttu-id="0a982-158">При запуске в этом примере отображается приложение, размещаемое у поставщика как показано на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="0a982-158">When you run this code sample, a provider-hosted application appears, as shown in Figure 5.</span></span> <span data-ttu-id="0a982-159">В этой статье описаны сценарии 1 и 2 сценарий способов, описанных в сценарии 1 и 2 сценарий может использовать для предоставления локализованных версий страницы сайта и заголовки ссылок на панели быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="0a982-159">This article describes Scenario 1 and Scenario 2 because you might use the techniques in Scenario 1 and Scenario 2 to provide localized versions of your site page and Quick Launch link titles.</span></span> 

<span data-ttu-id="0a982-160">**На рисунке 5. Начальная страница приложения Core.JavaScriptCustomization**</span><span class="sxs-lookup"><span data-stu-id="0a982-160">**Figure 5. Start page of the Core.JavaScriptCustomization app**</span></span>

![Снимок экрана, показывающий начальной странице Core.JavaScriptCustomization приложения](media/133a6c15-7b96-4418-b795-a7bdab63ead4.png)
### <a name="scenario-1"></a><span data-ttu-id="0a982-162">Сценарий 1</span><span class="sxs-lookup"><span data-stu-id="0a982-162">Scenario 1</span></span>

<span data-ttu-id="0a982-163">Сценарий 1 показано, как добавить ссылку на файл JavaScript на сайте SharePoint, с помощью дополнительного действия.</span><span class="sxs-lookup"><span data-stu-id="0a982-163">Scenario 1 shows how to add a reference to a JavaScript file on a SharePoint site using a custom action.</span></span> <span data-ttu-id="0a982-164">Кнопки **параметров вставки** вызывает метод **btnSubmit_Click** в scenario1.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="0a982-164">Choosing the  **Inject customization** button calls the **btnSubmit_Click** method in scenario1.aspx.cs.</span></span> <span data-ttu-id="0a982-165">Метод **btnSubmit_Click** вызывает **AddJsLink** для добавления ссылки на файлы JavaScript, с помощью дополнительного действия на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="0a982-165">The **btnSubmit_Click** method calls **AddJsLink** to add references to JavaScript files using a custom action on the host web.</span></span>

<span data-ttu-id="0a982-166">На рисунке 6 показан на начальной странице сценарии 1.</span><span class="sxs-lookup"><span data-stu-id="0a982-166">Figure 6 shows the start page for Scenario 1.</span></span>

<span data-ttu-id="0a982-167">**На рисунке 6. Сценарий 1 начальной страницы**</span><span class="sxs-lookup"><span data-stu-id="0a982-167">**Figure 6. Scenario 1 start page**</span></span>

![Снимок экрана с начальной страницы для сценария 1](media/16972165-5f94-497f-b58c-0e1075d9616a.png)

<span data-ttu-id="0a982-169">Метод **AddJSLink** является частью файла JavaScriptExtensions.cs в **OfficeDevPnP.Core**.</span><span class="sxs-lookup"><span data-stu-id="0a982-169">The  **AddJSLink** method is part of the JavaScriptExtensions.cs file in **OfficeDevPnP.Core**.</span></span>  <span data-ttu-id="0a982-170">**AddJSLink** требуется указать строку, представляющую идентификатор для назначения настраиваемого действия, что строка, содержащая точку с запятой запятыми список URL-адресов для файлов JavaScript, которые вы хотите добавить в веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="0a982-170">**AddJSLink** requires that you supply a string representing the identifier to assign to the custom action, and a string containing a semicolon delimited list of URLs to the JavaScript files that you want to add to the host web.</span></span> <span data-ttu-id="0a982-171">Обратите внимание, что этот пример кода добавляет ссылку на Scripts\scenario1.js, который добавляет сообщение о состоянии панели веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="0a982-171">Note that this code sample adds a reference to Scripts\scenario1.js, which adds a status bar message to the host web.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="0a982-172">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="0a982-172">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
protected void btnSubmit_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var cc = spContext.CreateUserClientContextForSPHost())
            {
                cc.Web.AddJsLink(Utilities.Scenario1Key, Utilities.BuildScenarioJavaScriptUrl(Utilities.Scenario1Key, this.Request));
            }
        }
```
   
> [!NOTE] 
> <span data-ttu-id="0a982-173">SharePoint 2013 с помощью стратегия минимальной загрузки для сокращения объема данных, браузер загружает при переходе между страницами на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a982-173">SharePoint 2013 uses Minimal Download Strategy to reduce the amount of data the browser downloads when users navigate between pages on a SharePoint site.</span></span> <span data-ttu-id="0a982-174">[Стратегия минимальной загрузки](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx)Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="0a982-174">For more information, see  [Minimal Download Strategy overview](http://msdn.microsoft.com/library/9caa7d99-1e74-4889-96c7-ba5a10772ad7.aspx).</span></span> <span data-ttu-id="0a982-175">В scenario1.js следующий код гарантирует, что ли стратегия минимальной загрузки используется на сайте SharePoint, этот метод **RemoteManager_Inject** всегда вызывается для запуска кода JavaScript для добавления панели сообщение о состоянии хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="0a982-175">In scenario1.js, the following code ensures that whether or not Minimal Download Strategy is used on your SharePoint site, the  **RemoteManager_Inject** method is always called to run the JavaScript code to add the status bar message to the host web.</span></span>

```
if ("undefined" != typeof g_MinimalDownload &amp;&amp; g_MinimalDownload &amp;&amp; (window.location.pathname.toLowerCase()).endsWith("/_layouts/15/start.aspx") &amp;&amp; "undefined" != typeof asyncDeltaManager) {
    // Register script for MDS if possible.
    RegisterModuleInit("scenario1.js", RemoteManager_Inject); //MDS registration
    RemoteManager_Inject(); //non MDS scenario
} else {
    RemoteManager_Inject();
}
```

> [!NOTE] 
> <span data-ttu-id="0a982-176">Некоторые файлы JavaScript может зависеть от других файлов JavaScript для загрузки во-первых, прежде чем их можно было запустить и выполнить операцию.</span><span class="sxs-lookup"><span data-stu-id="0a982-176">Some JavaScript files may depend on other JavaScript files to be loaded first, before they can run and complete successfully.</span></span> <span data-ttu-id="0a982-177">Следующая конструкция кода из **RemoteManager_Inject** используется функция **loadScript** в scenario1.js для первой загрузки jQuery, а затем продолжить выполнение оставшийся код JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0a982-177">The following code construct from  **RemoteManager_Inject** uses the **loadScript** function in scenario1.js to first load jQuery, then continue running the remaining JavaScript code.</span></span>

```
var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";

    // Load jQuery first, then continue running the rest of the code.
    loadScript(jQuery, function () {
     // Add additional JavaScript code here to complete your task. 
});
```

<span data-ttu-id="0a982-178">Выберите **веб-узел**.</span><span class="sxs-lookup"><span data-stu-id="0a982-178">Choose  **Back to Site**.</span></span> <span data-ttu-id="0a982-179">Как показано на рисунке 7, веб-сайт теперь отображается сообщение о состоянии панели, который был добавлен с scenario1.js.</span><span class="sxs-lookup"><span data-stu-id="0a982-179">As shown in Figure 7, the host web now displays a status bar message that was added by scenario1.js.</span></span>

<span data-ttu-id="0a982-180">**На рисунке 7. Сообщение о состоянии панели, добавленных на сайт группы, с помощью JavaScript**</span><span class="sxs-lookup"><span data-stu-id="0a982-180">**Figure 7. Status bar message added to a team site using JavaScript**</span></span>

![Снимок экрана с сообщением панели состояния, добавленных на сайт группы с помощью JavaScript](media/c5d6fb6d-f05f-49aa-a3c5-af1240ee9135.png)

### <a name="scenario-2"></a><span data-ttu-id="0a982-182">Сценарий 2</span><span class="sxs-lookup"><span data-stu-id="0a982-182">Scenario 2</span></span>
<span data-ttu-id="0a982-183"><a name="bk_Scenario2"> </a></span><span class="sxs-lookup"><span data-stu-id="0a982-183"></span></span>

<span data-ttu-id="0a982-184">Сценарий 2 использует метод, описанный в сценарии 1 замена текста пользовательского интерфейса на чтение из файла ресурсов JavaScript переведенный текст.</span><span class="sxs-lookup"><span data-stu-id="0a982-184">Scenario 2 uses the technique described in Scenario 1 to replace UI text with translated text read from a JavaScript resource file.</span></span> <span data-ttu-id="0a982-185">Сценарий 2 заменяет заголовок панели быстрого запуска ссылку ( **Моя запись панели быстрого запуска**) и сайт страницы заголовка ( **Hello SharePoint**), созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="0a982-185">Scenario 2 replaces the Quick Launch link title ( **My quicklaunch entry**) and site page title ( **Hello SharePoint**) that you created earlier.</span></span> <span data-ttu-id="0a982-186">Сценарий 2 подключает файл JavaScript, которые переведенного текстовые значения из переменных в допустимом формате файлов ресурсов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0a982-186">Scenario 2 attaches a JavaScript file which reads translated text values from variables in culture-specific JavaScript resource files.</span></span> <span data-ttu-id="0a982-187">Сценарий 2 обновляет пользовательский Интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0a982-187">Scenario 2 then updates the UI.</span></span> <span data-ttu-id="0a982-188">На рисунке 8 показана начальная страница для сценария 2.</span><span class="sxs-lookup"><span data-stu-id="0a982-188">Figure 8 shows the start page for Scenario 2.</span></span>

<span data-ttu-id="0a982-189">**На рисунке 8. Сценарий 2 начальной страницы**</span><span class="sxs-lookup"><span data-stu-id="0a982-189">**Figure 8. Scenario 2 start page**</span></span>

![Снимок экрана с начальной страницы для сценария 2](media/c706060b-e77d-4ae6-99c4-43dee80ff7d3.png)

<span data-ttu-id="0a982-191">Как показано на рисунке 8, выбор **параметров вставки** применяются следующие изменения к сайту:</span><span class="sxs-lookup"><span data-stu-id="0a982-191">As shown in Figure 8, choosing  **Inject customization** applies the following changes to the site:</span></span>

- <span data-ttu-id="0a982-192">Заголовок панели быстрого запуска ссылку **Моя запись панели быстрого запуска** изменяется на **Contoso ссылок**.</span><span class="sxs-lookup"><span data-stu-id="0a982-192">The Quick Launch link title  **My quicklaunch entry** is changed to **Contoso link**.</span></span>
    
- <span data-ttu-id="0a982-193">Заголовок страницы сайта **Hello SharePoint** изменяется на **Contoso страницы**.</span><span class="sxs-lookup"><span data-stu-id="0a982-193">The  **Hello SharePoint** site page title is changed to **Contoso page**.</span></span>

<span data-ttu-id="0a982-194">**На рисунке 9. Сценарий 2 настроек**</span><span class="sxs-lookup"><span data-stu-id="0a982-194">**Figure 9. Scenario 2 customizations**</span></span>

![Сценарий 2 настроек](media/47e8ec40-d291-496f-8677-01eb46441df2.png)
    
> [!NOTE] 
> <span data-ttu-id="0a982-196">Если необходимые значения для быстрого запуска ссылку название и заголовок страницы сайта, отличаются от условий показано на рисунке 8 изменить переменные **quickLauch_Scenario2** и **pageTitle_HelloSharePoint** в ресурсов JavaScript файлы scenario2.en us.js или scenario2.NL-nl.js.</span><span class="sxs-lookup"><span data-stu-id="0a982-196">If your values for the Quick Launch link title and site page title differ from those shown in Figure 8, edit the  **quickLauch_Scenario2** and **pageTitle_HelloSharePoint** variables in the JavaScript resource files scenario2.en-us.js or scenario2.nl-nl.js.</span></span> <span data-ttu-id="0a982-197">Затем снова запустите пример кода.</span><span class="sxs-lookup"><span data-stu-id="0a982-197">Then run the code sample again.</span></span> <span data-ttu-id="0a982-198">В файле scenario2.en us.js хранятся ресурсы для конкретного языка и региональных параметров Английский (США).</span><span class="sxs-lookup"><span data-stu-id="0a982-198">The scenario2.en-us.js file stores English (US) culture-specific resources.</span></span> <span data-ttu-id="0a982-199">В файле scenario2.nl nl.js хранятся голландский ресурсы для конкретного языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="0a982-199">The scenario2.nl-nl.js file stores Dutch culture-specific resources.</span></span> <span data-ttu-id="0a982-200">При тестировании этот пример кода, использующий другой язык, рассмотрите возможность создания другой файл ресурсов JavaScript, с помощью же соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="0a982-200">If you are testing this code sample using another language, consider creating another JavaScript resource file using the same naming convention.</span></span>

<span data-ttu-id="0a982-201">Как и в сценарии 1, **btnSubmit_Click** в scenario2.aspx.cs вызывает **AddJsLink** , чтобы добавить ссылку на файл Scripts\scenario2.js.</span><span class="sxs-lookup"><span data-stu-id="0a982-201">Similar to Scenario 1,  **btnSubmit_Click** in scenario2.aspx.cs calls **AddJsLink** to add a reference to the Scripts\scenario2.js file.</span></span> <span data-ttu-id="0a982-202">В scenario2.js функция **RemoteManager_Inject** вызывает функцию **TranslateQuickLaunch** , которая выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="0a982-202">In scenario2.js, the **RemoteManager_Inject** function calls the **TranslateQuickLaunch** function, which performs the following tasks:</span></span>

- <span data-ttu-id="0a982-203">Определяет узел языка и региональных параметров с помощью **_spPageContextInfo.currentUICultureName**.</span><span class="sxs-lookup"><span data-stu-id="0a982-203">Determines the site's culture using  **_spPageContextInfo.currentUICultureName**.</span></span>
    
- <span data-ttu-id="0a982-204">Загружает файл ресурсов JavaScript, содержащий ресурсы конкретного языка и региональных параметров, которые соответствуют языка и региональных параметров пользовательского интерфейса веб-узла.</span><span class="sxs-lookup"><span data-stu-id="0a982-204">Loads the JavaScript resource file containing culture specific resources that match the UI culture of the site.</span></span> <span data-ttu-id="0a982-205">Например если язык и региональные параметры веб-узла русский (Россия), загрузки файла scenario2.en us.js.</span><span class="sxs-lookup"><span data-stu-id="0a982-205">For example, if the site's culture was English (United States), the scenario2.en-us.js file is loaded.</span></span>
    
- <span data-ttu-id="0a982-206">Заменяет значение переменной **quickLauch_Scenario2** , чтение из файлов ресурсов JavaScript **Моя запись панели быстрого запуска** .</span><span class="sxs-lookup"><span data-stu-id="0a982-206">Replaces  **my quicklaunch entry** with the value of the **quickLauch_Scenario2** variable read from the JavaScript resource file.</span></span>

```
function RemoteManager_Inject() {

    var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";
    
    loadScript(jQuery, function () {
        SP.SOD.executeOrDelayUntilScriptLoaded(function () { TranslateQuickLaunch(); }, 'sp.js');
    });
}

function TranslateQuickLaunch() {
    // Load jQuery and if complete, load the JS resource file.
    var scriptUrl = "";
    var scriptRevision = "";
    // iterate over the scripts loaded on the page to find the scenario2 script. Then use the script URL to dynamically build the URL for the resource file to be loaded.
    $('script').each(function (i, el) {
        if (el.src.toLowerCase().indexOf('scenario2.js') > -1) {
            scriptUrl = el.src;
            scriptRevision = scriptUrl.substring(scriptUrl.indexOf('.js') + 3);
            scriptUrl = scriptUrl.substring(0, scriptUrl.indexOf('.js'));
        }
    })

    var resourcesFile = scriptUrl + "." + _spPageContextInfo.currentUICultureName.toLowerCase() + ".js" + scriptRevision;
    // Load the JS resource file based on the user's language settings.
    loadScript(resourcesFile, function () {

        // General changes that apply to all loaded pages.
        // ----------------------------------------------

        // Update the Quick Launch labels.
        // Note that you can use the jQuery  function to iterate over all elements that match your jQuery selector.
        $("span.ms-navedit-flyoutArrow").each(function () {
            if (this.innerText.toLowerCase().indexOf('my quicklaunch entry') > -1) {
                // Update the label.
                $(this).find('.menu-item-text').text(quickLauch_Scenario2);
                // Update the tooltip.
                $(this).parent().attr("title", quickLauch_Scenario2);
            }
        });

        // Page specific changes require an IsOnPage call.
        // ----------------------------------------------------------

        // Change the title of the "Hello SharePoint" page.
        if (IsOnPage("Hello%20SharePoint.aspx")) {
            $("#DeltaPlaceHolderPageTitleInTitleArea").find("A").each(function () {
                if ($(this).text().toLowerCase().indexOf("hello sharepoint") > -1) {
                    // Update the label.
                    $(this).text(pageTitle_HelloSharePoint);
                    // Update the tooltip.
                    $(this).attr("title", pageTitle_HelloSharePoint);
                }
            });
        }

    });
}
```

## <a name="see-also"></a><span data-ttu-id="0a982-207">См. также</span><span class="sxs-lookup"><span data-stu-id="0a982-207">See also</span></span>
<span data-ttu-id="0a982-208"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0a982-208"></span></span>

-  [<span data-ttu-id="0a982-209">Локализация решения для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="0a982-209">Localization solutions for SharePoint 2013 and SharePoint Online</span></span>](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [<span data-ttu-id="0a982-210">Core.JavaScriptCustomization</span><span class="sxs-lookup"><span data-stu-id="0a982-210">Core.JavaScriptCustomization</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
