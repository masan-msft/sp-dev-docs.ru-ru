---
title: Использование экспериментального мини-приложения People Picker в надстройках SharePoint
description: Используйте мини-приложение People Picker в ваших надстройках, чтобы помочь пользователям находить и выбирать людей и группы.
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 72cde6161c46b1495485c3562d101fd4b0d57567
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="use-the-experimental-people-picker-widget-in-sharepoint-add-ins"></a><span data-ttu-id="b82b1-103">Использование экспериментального мини-приложения People Picker в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="b82b1-103">Use the experimental People Picker widget in SharePoint Add-ins</span></span>

<span data-ttu-id="b82b1-104">Мини-приложение People Picker может использоваться на любой веб-странице, даже если она не размещена в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b82b1-104">You can use the People Picker widget on any web page, even if the page is not hosted in SharePoint.</span></span> <span data-ttu-id="b82b1-105">Используйте мини-приложение People Picker в ваших надстройках, чтобы помочь пользователям находить и выбирать людей и группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-105">Learn how to use the People Picker widget on any web page, even if the page is not hosted in SharePoint. Use the People Picker widget in your add-ins to help users find and select people and groups.</span></span>

> [!WARNING] 
> <span data-ttu-id="b82b1-106">Экспериментальные мини-приложения Office для веб-страниц предоставляются только в целях исследования и сбора отзывов.</span><span class="sxs-lookup"><span data-stu-id="b82b1-106">The Office Web Widgets - Experimental are only provided for research and feedback purposes.</span></span> <span data-ttu-id="b82b1-107">Не следует использовать их в производственных сценариях.</span><span class="sxs-lookup"><span data-stu-id="b82b1-107">Do not use in production scenarios.</span></span> <span data-ttu-id="b82b1-108">Поведение мини-приложений Office для веб-страниц может существенно измениться в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="b82b1-108">The Office Web Widgets behavior may change significantly in future releases.</span></span> <span data-ttu-id="b82b1-109">Ознакомьтесь с [условиями лицензии на экспериментальные мини-приложения Office для веб-страниц](office-web-widgetsexperimental-license-terms.md).</span><span class="sxs-lookup"><span data-stu-id="b82b1-109">Read and review the [Office Web Widgets - Experimental License Terms](office-web-widgetsexperimental-license-terms.md).</span></span>

<span data-ttu-id="b82b1-p103">Используя в надстройках экспериментальный виджет "Выбор людей", вы можете помочь пользователям находить и выбирать людей и группы в клиенте. Когда пользователь вводит текст в текстовом поле, виджет загружает контакты, чьи имена или адреса электронной почты соответствуют запросу.</span><span class="sxs-lookup"><span data-stu-id="b82b1-p103">You can use the experimental People Picker widget in add-ins to help your users find and select people and groups in a tenant. Users can start typing in the text box and the widget retrieves the people whose name or e-mail matches the text.</span></span>

<br/>

<span data-ttu-id="b82b1-112">**Обработка запроса мини-приложением People Picker**</span><span class="sxs-lookup"><span data-stu-id="b82b1-112">**Figure 1. People Picker widget solving a query**</span></span>

![Экспериментальный элемент управления People Picker на странице](../images/PeoplePicker_basic.png)

<span data-ttu-id="b82b1-p104">Ваша надстройка может получить доступ к выбранным контактам путем считывания свойства **selectedItems** мини-приложения. Свойство selectedItems является массивом объектов, которые представляют собой людей или группы. В таблице ниже приведены доступные свойства объекта пользователя.</span><span class="sxs-lookup"><span data-stu-id="b82b1-p104">Your add-in can access the selected people by reading the **selectedItems** property of the widget. The selectedItems property is an array of objects that represent people or groups. The following table shows the available properties of the user object.</span></span>

<br/>

|<span data-ttu-id="b82b1-117">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="b82b1-117">**Property**</span></span>|<span data-ttu-id="b82b1-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="b82b1-118">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b82b1-119">**department**</span><span class="sxs-lookup"><span data-stu-id="b82b1-119">**department**</span></span>|<span data-ttu-id="b82b1-120">Подразделение пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-120">Represents the department of the user or group.</span></span>|
|<span data-ttu-id="b82b1-121">**displayName**</span><span class="sxs-lookup"><span data-stu-id="b82b1-121">**displayName**</span></span>|<span data-ttu-id="b82b1-122">Отображаемое имя пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-122">Represents the display name of the user or group.</span></span>|
|<span data-ttu-id="b82b1-123">**email**</span><span class="sxs-lookup"><span data-stu-id="b82b1-123">**email**</span></span>|<span data-ttu-id="b82b1-124">Электронный адрес пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-124">Represents the e-mail address of the user or group.</span></span>|
|<span data-ttu-id="b82b1-125">**isResolved**</span><span class="sxs-lookup"><span data-stu-id="b82b1-125">**isResolved**</span></span>|<span data-ttu-id="b82b1-126">Указывает, удалось ли мини-приложению разрешить текст для пользователя или группы в клиенте.</span><span class="sxs-lookup"><span data-stu-id="b82b1-126">Indicates if the widget has successfully resolved the text in the widget against a user or group in the tenant.</span></span>|
|<span data-ttu-id="b82b1-127">**jobTitle**</span><span class="sxs-lookup"><span data-stu-id="b82b1-127">**jobTitle**</span></span>|<span data-ttu-id="b82b1-128">Должность пользователя.</span><span class="sxs-lookup"><span data-stu-id="b82b1-128">Represents the job title of the user.</span></span>|
|<span data-ttu-id="b82b1-129">**loginName**</span><span class="sxs-lookup"><span data-stu-id="b82b1-129">**loginName**</span></span>|<span data-ttu-id="b82b1-130">Имя для входа пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-130">The sign-in name of the user or group.</span></span>|
|<span data-ttu-id="b82b1-131">**mobile**</span><span class="sxs-lookup"><span data-stu-id="b82b1-131">**mobile**</span></span>|<span data-ttu-id="b82b1-132">Номер мобильного телефона пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-132">Represents the mobile phone number of the user or group.</span></span>|
|<span data-ttu-id="b82b1-133">**principalId**</span><span class="sxs-lookup"><span data-stu-id="b82b1-133">**principalId**</span></span>|<span data-ttu-id="b82b1-134">Основной идентификатор пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-134">Represents the principal ID of the user or group.</span></span>|
|<span data-ttu-id="b82b1-135">**principalType**</span><span class="sxs-lookup"><span data-stu-id="b82b1-135">**principalType**</span></span>|<span data-ttu-id="b82b1-p105">Указывает, является ли элемент пользователем или группой. Принимает значение 1, если это пользователь, и 4, если это группа.</span><span class="sxs-lookup"><span data-stu-id="b82b1-p105">Indicates if the item is a user or a group. It has a value of 1 if it's a user, 4 if it's a group.</span></span>|
|<span data-ttu-id="b82b1-138">**sipAddress**</span><span class="sxs-lookup"><span data-stu-id="b82b1-138">**sipAddress**</span></span>|<span data-ttu-id="b82b1-139">SIP-адрес пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-139">Represents the sip address of the user or group.</span></span>|
|<span data-ttu-id="b82b1-140">**text**</span><span class="sxs-lookup"><span data-stu-id="b82b1-140">**text**</span></span>|<span data-ttu-id="b82b1-141">Текстовый заголовок имени пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-141">Represents the text title of the user or group name.</span></span>|

<br/>

<span data-ttu-id="b82b1-p106">Мини-приложение "Выбор людей" имеет кэш последних использовавшихся записей (MRU). В кэше хранятся пять последних записей, которые были обработаны мини-приложением.</span><span class="sxs-lookup"><span data-stu-id="b82b1-p106">The People Picker widget has a cache of the most recently used (MRU) entries. The cache stores the five latest entries that the widget resolved.</span></span>
 
## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="b82b1-144">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="b82b1-144">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="b82b1-145">Для использования примеров, описанных в этой статье, вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="b82b1-145">To use the examples in this article, you need the following:</span></span>

- <span data-ttu-id="b82b1-146">Visual Studio 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b82b1-146">Visual Studio 2015 or later.</span></span>
- <span data-ttu-id="b82b1-147">Диспетчер пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="b82b1-147">NuGet Package Manager.</span></span> <span data-ttu-id="b82b1-148">Дополнительные сведения см. в статье [Установка NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span><span class="sxs-lookup"><span data-stu-id="b82b1-148">NuGet Package Manager. For more information, see  [Installing NuGet](http://go.microsoft.com/fwlink/?LinkId=271465).</span></span>
- <span data-ttu-id="b82b1-149">Среда разработки SharePoint (для локальных сценариев требуется изоляция приложений).</span><span class="sxs-lookup"><span data-stu-id="b82b1-149">A SharePoint development environment (app isolation required for on-premises scenarios).</span></span>
- <span data-ttu-id="b82b1-150">Пакет NuGet "Экспериментальные мини-приложения Office для веб-страниц".</span><span class="sxs-lookup"><span data-stu-id="b82b1-150">Office Web Widgets - Experimental NuGet gallery page</span></span> <span data-ttu-id="b82b1-151">Дополнительные сведения об установке пакетов NuGet см. в статье [Пользовательский интерфейс диспетчера пакетов NuGet](https://docs.microsoft.com/ru-RU/nuget/tools/package-manager-ui).</span><span class="sxs-lookup"><span data-stu-id="b82b1-151">For more information about how to install a NuGet package, see [NuGet Package Manager UI](https://docs.microsoft.com/ru-RU/nuget/tools/package-manager-ui).</span></span> <span data-ttu-id="b82b1-152">Вы также можете просмотреть [страницу коллекции NuGet](https://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="b82b1-152">You can also browse the [NuGet gallery page](https://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
    
## <a name="use-the-people-picker-widget-in-a-provider-hosted-sharepoint-add-in"></a><span data-ttu-id="b82b1-153">Использование мини-приложения People Picker в надстройке SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="b82b1-153">Use the People Picker widget in a provider-hosted SharePoint Add-in</span></span>

<span data-ttu-id="b82b1-154">В этом примере простая страница размещена вне платформы SharePoint, объявляющей мини-приложение People Picker с помощью разметки.</span><span class="sxs-lookup"><span data-stu-id="b82b1-154">In this example, there is a simple page hosted outside of SharePoint that declares a Desktop List View widget.</span></span> <span data-ttu-id="b82b1-155">Для простоты в этом примере параметры не объявлены, но вы можете посмотреть пример с параметрами в разделе [Дальнейшие действия](#NextSteps).</span><span class="sxs-lookup"><span data-stu-id="b82b1-155">In this example, there is a simple page hosted outside of SharePoint that declares a People Picker widget using markup. To keep things simple, this example doesn't declare any options, but you can see an example with options in the  [NextSteps](#NextSteps) section.</span></span>

<span data-ttu-id="b82b1-156">Чтобы использовать мини-приложение People Picker, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b82b1-156">To use the People Picker widget, you must do the following:</span></span>

- <span data-ttu-id="b82b1-157">Создайте надстройку SharePoint и веб-проекты.</span><span class="sxs-lookup"><span data-stu-id="b82b1-157">Create SharePoint Add-in and web projects.</span></span>

- <span data-ttu-id="b82b1-p110">Создайте модуль на сайте надстройки. Это действие гарантирует создание сайта надстройки при ее развертывании.</span><span class="sxs-lookup"><span data-stu-id="b82b1-p110">Create a module on the add-in web. This step ensures that an add-in web is created when users deploy the add-in.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b82b1-160">Междоменная библиотека требует наличия сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="b82b1-160">Note  The cross-domain library requires the existence of an add-in web. The People Picker widget communicates with SharePoint by using the cross-domain library.</span></span> <span data-ttu-id="b82b1-161">Мини-приложение People Picker взаимодействует с SharePoint посредством междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="b82b1-161">Note  The cross-domain library requires the existence of an add-in web. The People Picker widget communicates with SharePoint by using the cross-domain library.</span></span>

- <span data-ttu-id="b82b1-162">Создайте страницу надстройки, в которой с помощью разметки объявляется экземпляр мини-приложения People Picker.</span><span class="sxs-lookup"><span data-stu-id="b82b1-162">Create an add-in page that declares a People Picker widget instance using markup.</span></span>
    
### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a><span data-ttu-id="b82b1-163">Создание надстройки SharePoint и веб-проектов</span><span class="sxs-lookup"><span data-stu-id="b82b1-163">To create a SharePoint Add-in and web projects</span></span>

1. <span data-ttu-id="b82b1-164">Откройте Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="b82b1-164">Open Visual Studio 2015 as administrator.</span></span> <span data-ttu-id="b82b1-165">(Для этого выберите значок Visual Studio в меню **Пуск** и пункт **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="b82b1-165">(To do this, right-click the Visual Studio 2015 icon on the **Start** menu, and select **Run as administrator**.)</span></span>

2. <span data-ttu-id="b82b1-166">Создайте проект, используя шаблон "Надстройка SharePoint". Шаблон **Надстройка SharePoint** находится в следующем разделе: **Шаблоны** > **Visual C#**, **Office/SharePoint** > **Надстройки**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-166">Create a new project using the SharePoint Add-in 2013 template.The  **SharePoint Add-in 2013** template is located under **Templates** > **Visual C#**,  **Office/SharePoint** > **Add-ins**.</span></span>
    
3. <span data-ttu-id="b82b1-167">Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="b82b1-167">Provide the SharePoint website URL that you want to use for debugging.</span></span>
 
4. <span data-ttu-id="b82b1-168">Выберите для надстройки вариант размещения **Размещено у поставщика**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-168">Select **Provider-hosted** as the hosting option for your add-in.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b82b1-169">Мини-приложение People Picker можно использовать и с другими вариантами размещения, а также с надстройками Office или собственным веб-сайтом.</span><span class="sxs-lookup"><span data-stu-id="b82b1-169">Note You can also use the People Picker widget with other hosting options or even with Office Add-ins or your own website.</span></span>

5. <span data-ttu-id="b82b1-170">Выберите **Приложение веб-форм ASP.NET** в качестве типа проекта веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b82b1-170">Select **ASP.NET Web Forms Application** as the type of web application project.</span></span>
    
6. <span data-ttu-id="b82b1-171">Выберите **службу контроля доступа Windows Azure** в качестве способа проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b82b1-171">Select **Windows Azure Access Control Service** as the authentication option.</span></span>
    

### <a name="to-create-a-module-on-the-add-in-web"></a><span data-ttu-id="b82b1-172">Создание модуля на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="b82b1-172">To create a module on the add-in web</span></span>

1. <span data-ttu-id="b82b1-173">Выберите проект надстройки SharePoint в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-173">Choose the SharePoint Add-in project in  **Solution Explorer**. Choose  AddNew Item…</span></span> <span data-ttu-id="b82b1-174">Выберите **Добавить** > **Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-174">Select **Add** > **New Item**.</span></span>
    
2. <span data-ttu-id="b82b1-175">Выберите **Элементы Visual C#** > **Office/SharePoint** > **Модуль**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-175">Select **Visual C# Items** > **Office/SharePoint** > **Module**.</span></span> <span data-ttu-id="b82b1-176">Укажите имя модуля.</span><span class="sxs-lookup"><span data-stu-id="b82b1-176">Choose  Visual C# ItemsOffice/SharePointModule. Provide a name for your module.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b82b1-177">При создании надстройки с размещением в SharePoint нет необходимости создавать дополнительный модуль.</span><span class="sxs-lookup"><span data-stu-id="b82b1-177">Note  If you're building a SharePoint-hosted add-in, you don't need to create an extra module.</span></span>


### <a name="to-add-a-new-page-that-uses-the-people-picker-widget"></a><span data-ttu-id="b82b1-178">Добавление новой страницы, использующей мини-приложение People Picker</span><span class="sxs-lookup"><span data-stu-id="b82b1-178">To add a new page that uses the People Picker widget</span></span>

1. <span data-ttu-id="b82b1-179">Выберите папку **Страницы** веб-проекта в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-179">Choose the **Pages** folder in the web project in **Solution Explorer**.</span></span>
    
2. <span data-ttu-id="b82b1-p115">Скопируйте приведенный ниже код и вставьте его в **ASPX**-файл проекта. Код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b82b1-p115">Copy the following code and paste it in an **ASPX** file in the project. The code performs the following tasks:</span></span>
    
    - <span data-ttu-id="b82b1-182">добавляет ссылки на необходимые библиотеки и ресурсы Office;</span><span class="sxs-lookup"><span data-stu-id="b82b1-182">Adds references to the required Office libraries and resources.</span></span>
    
    - <span data-ttu-id="b82b1-183">инициализирует среду выполнения элементов управления;</span><span class="sxs-lookup"><span data-stu-id="b82b1-183">Initializes the controls runtime.</span></span>
            
    - <span data-ttu-id="b82b1-184">запускает метод **renderAll** среды выполнения элементов управления Office;</span><span class="sxs-lookup"><span data-stu-id="b82b1-184">Runs the **renderAll** method of the Office Controls runtime.</span></span>
            
    - <span data-ttu-id="b82b1-185">объявляет заполнитель для мини-приложения People Picker.</span><span class="sxs-lookup"><span data-stu-id="b82b1-185">Declares a placeholder for the People Picker widget.</span></span>

    ```HTML
    <!DOCTYPE html>
    <html>
    <head>
    <!-- IE9 or superior -->
        <meta http-equiv="X-UA-Compatible" content="IE=9" >
        <title>People Picker HTML Markup</title>

        <!-- Widgets Specific CSS File -->
        <link 
            rel="stylesheet" 
            type="text/css" 
            href="../Scripts/Office.Controls.css" 
        />

    <!-- Ajax, jQuery, and utils --> 
        <script 
            src=" https://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js.js">
        </script>
        <script 
            src=" https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js">
        </script>
        <script type="text/javascript">
            // Function to retrieve a query string value.
            // For production purposes you may want to use
            //  a library to handle the query string.
            function getQueryStringParameter(paramToRetrieve) {
                var params =
                    document.URL.split("?")[1].split("&amp;");
                var strParams = "";
                for (var i = 0; i < params.length; i = i + 1) {
                    var singleParam = params[i].split("=");
                    if (singleParam[0] == paramToRetrieve)
                        return singleParam[1];
                }
            }
        </script>

    <!-- Cross-Domain Library and Office controls runtime -->
        <script type="text/javascript">
            //Register namespace and variables used through the sample
            Type.registerNamespace("Office.Samples.PeoplePickerBasic");
            //Retrieve context tokens from the querystring
            Office.Samples.PeoplePickerBasic.appWebUrl =
                decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
            Office.Samples.PeoplePickerBasic.hostWebUrl =
                decodeURIComponent(getQueryStringParameter("SPHostUrl"));

            //Pattern to dynamically load JSOM and and the cross-domain library
            var scriptbase =
                Office.Samples.PeoplePickerBasic.hostWebUrl + "/_layouts/15/";

            //Get the cross-domain library
            $.getScript(scriptbase + "SP.RequestExecutor.js",
                //Get the Office controls runtime and 
                //  continue to the createControl function
                function () {
                    $.getScript("../Scripts/Office.Controls.js", createControl)
                }
            );
        </script>

    <!--People Picker -->
        <script 
            src="../Scripts/Office.Controls.PeoplePicker.js" 
            type="text/javascript">
        </script>
    </head>
    <body>
        Basic People Picker sample (HTML markup declaration):
        <div 
                id="PeoplePickerDiv" 
                data-office-control="Office.Controls.PeoplePicker">
        </div>

        <script type="text/javascript">
            function createControl() {
                //Initialize Controls Runtime
                Office.Controls.Runtime.initialize({
                    sharePointHostUrl: Office.Samples.PeoplePickerBasic.hostWebUrl,
                    appWebUrl: Office.Samples.PeoplePickerBasic.appWebUrl
                });

                //Render the widget, this must be executed after the
                //placeholder DOM is loaded
                Office.Controls.Runtime.renderAll();
            }
        </script>
    </body>
    </html>

    ```

<br/>

> [!NOTE] 
> <span data-ttu-id="b82b1-186">В приведенном выше примере кода явно указаны URL-адреса хост-сайта и сайта надстройки, чтобы инициализировать среду выполнения для элементов управления Office.</span><span class="sxs-lookup"><span data-stu-id="b82b1-186">The previous code example explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime.</span></span> <span data-ttu-id="b82b1-187">Однако если URL-адреса хост-сайта и сайта надстройки указаны в параметрах строки запроса **SPAppWebUrl** и **SPHostUrl** соответственно, то вы можете передать пустой объект, и код попытается получить параметры автоматически.</span><span class="sxs-lookup"><span data-stu-id="b82b1-187">Note  The code example above explicitly specifies the host web and add-in web URLs to initialize the Office controls runtime. However, if the add-in web and host web URLs are specified in the  **SPAppWebUrl** and **SPHostUrl** query string parameters, respectively; you can pass an empty object and the code will attempt to get the parameters automatically. The SPAppWebUrl and SPHostUrl parameters are included in the query string when you use the {StandardTokens} token.</span></span> <span data-ttu-id="b82b1-188">Параметры **SPAppWebUrl** и **SPHostUrl** включаются в строку запроса при использовании маркера **{StandardTokens}**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-188">The **SPAppWebUrl** and **SPHostUrl** parameters are included in the query string when you use the **{StandardTokens}** token.</span></span>
 
<span data-ttu-id="b82b1-189">В следующем примере показано, как передавать пустой объект в метод инициализации.</span><span class="sxs-lookup"><span data-stu-id="b82b1-189">The following example shows you how to pass an empty object to the initialize method:</span></span>

```
// Initialize with an empty object and the code 
// will attempt to get the tokens from the
// query string directly.
Office.Controls.Runtime.initialize({});
```


### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="b82b1-190">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="b82b1-190">To build and run the solution</span></span>

1. <span data-ttu-id="b82b1-191">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="b82b1-191">Select the F5 key.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b82b1-192">При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="b82b1-192">Note  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>

2. <span data-ttu-id="b82b1-193">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-193">Select the **Trust It** button.</span></span>
    
3. <span data-ttu-id="b82b1-194">Выберите значок надстройки на странице **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-194">Choose the add-in icon on the  **Site Contents** page.</span></span>
    
<span data-ttu-id="b82b1-195">Чтобы скачать этот пример из коллекции кода, см. пример кода [Использование экспериментального мини-приложения People Picker в надстройке](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="b82b1-195">You can also download this sample from code gallery, see the  [Use the People Picker experimental widget in an add-in](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-57859f85) code sample.</span></span>
 
<span data-ttu-id="b82b1-196"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="b82b1-196"></span></span>

## <a name="next-steps"></a><span data-ttu-id="b82b1-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b82b1-197">Next steps</span></span>

<span data-ttu-id="b82b1-p117">В этой статье описано, как использовать мини-приложение "Выбор людей" в своей надстройке с помощью HTML. Кроме того, вы можете ознакомиться со следующими сценариями и сведениями о мини-приложении.</span><span class="sxs-lookup"><span data-stu-id="b82b1-p117">This article shows how to use the People Picker widget in your add-in by using HTML. You can also explore the following scenarios and details about the widget.</span></span>

### <a name="use-javascript-to-declare-the-people-picker-widget"></a><span data-ttu-id="b82b1-200">Использование JavaScript для объявления мини-приложения People Picker</span><span class="sxs-lookup"><span data-stu-id="b82b1-200">Use JavaScript to declare the People Picker widget</span></span>

<span data-ttu-id="b82b1-201">Для объявления мини-приложения можно использовать JavaScript, а не HTML.</span><span class="sxs-lookup"><span data-stu-id="b82b1-201">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span> <span data-ttu-id="b82b1-202">В этом случае в качестве заполнителя для мини-приложения можно использовать следующую разметку:</span><span class="sxs-lookup"><span data-stu-id="b82b1-202">Depending on your preference, you might want to use the JavaScript instead of HTML to declare the widget. If this is the case you can use the following markup as the placeholder for the widget.</span></span>

```HTML
<div id="PeoplePickerDiv"></div>
```

<br/>

<span data-ttu-id="b82b1-203">Используйте приведенный ниже код JavaScript для создания экземпляров мини-приложения People Picker.</span><span class="sxs-lookup"><span data-stu-id="b82b1-203">Use the following JavaScript code to instantiate the People Picker.</span></span>

```js
new Office.Controls.PeoplePicker(
    document.getElementById("PeoplePickerDiv"), {});
```

<br/>

<span data-ttu-id="b82b1-204">Пример кода, который показывает, как выполнять эти действия, размещен на странице **JSSimple.html** в разделе [Использование экспериментального мини-приложения "Выбор людей" в надстройке](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="b82b1-204">For a code sample that shows how to perform the tasks, see the **JSSimple.html** page in the [Use the People Picker experimental widget in an add-in](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-57859f85) code sample.</span></span>

### <a name="specify-options-for-the-widget"></a><span data-ttu-id="b82b1-205">Указание параметров мини-приложения</span><span class="sxs-lookup"><span data-stu-id="b82b1-205">Specify options for the widget</span></span>

<span data-ttu-id="b82b1-p119">Параметры мини-приложения можно задать с помощью атрибута **data-office-options** в объявлении мини-приложения. Следующий HTML-код демонстрирует способ задания параметров мини-приложения "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="b82b1-p119">You can specify options for the widget by using the **data-office-options** attribute in the widget declaration. The following HTML shows how to specify options for the PeoplePicker widget.</span></span>

```HTML
<div id="PeoplePickerDiv"
        data-office-control="Office.Controls.PeoplePicker"
        data-office-options='{
        "allowMultipleSelections" : true,
        "onChange" : handleChange,
        "placeholder" : "Check the count message, it changes when you add names..."
    }'>
</div>
```

<br/>

<span data-ttu-id="b82b1-208">В приведенном ниже коде показано, как задать параметры при объявлении мини-приложения People Picker с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b82b1-208">The following code shows how to specify options when you declare the PeoplePicker widget using JavaScript.</span></span>

```js
new Office.Controls.PeoplePicker(
    document.getElementById("PeoplePickerDiv"), {
        allowMultipleSelections: true,
        placeholder: "Check the count message, it changes when you add names...",
        onChange: function (ctrl) {
            document.getElementById("count").textContent = 
ctrl.selectedItems.length.toString();
        }
    });
```

<span data-ttu-id="b82b1-209">Кроме того, вы можете указать обработчики для таких событий, как **onChange**, **onAdded** и **onRemoved**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-209">You can also specify event handlers for the **onChange**, **onAdded**, and **onRemoved** events.</span></span> <span data-ttu-id="b82b1-210">Обратите внимание, что в приведенном выше коде обработчик события onChange принимает единственный параметр **ctrl**, который является ссылкой на мини-приложение.</span><span class="sxs-lookup"><span data-stu-id="b82b1-210">You can also specify event handlers for the onChange, onAdded, and onRemoved events. Note in the code above that the event handler for the onChange event receives a single parameter **ctrl**, which is a reference to the widget.</span></span>

<span data-ttu-id="b82b1-211">Пример указания параметров приведен на страницах **MarkupOptions.html** и **JSOptions.html** в разделе [Использование экспериментального мини-приложения "Выбор людей" в надстройке](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="b82b1-211">For an example of how to specify options, see the **MarkupOptions.html** and **JSOptions.html** pages in the [Use the People Picker experimental widget in an add-in](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-57859f85) code sample.</span></span>

### <a name="retrieve-the-people-or-groups-selected-in-the-widget"></a><span data-ttu-id="b82b1-212">Получение пользователей или групп, выбранных в мини-приложении</span><span class="sxs-lookup"><span data-stu-id="b82b1-212">Retrieve the people or groups selected in the widget</span></span>

<span data-ttu-id="b82b1-213">Выполните следующие задачи, чтобы определить, какие люди выбраны в мини-приложении:</span><span class="sxs-lookup"><span data-stu-id="b82b1-213">To retrieve the people in the widget you must perform the following tasks:</span></span>

- <span data-ttu-id="b82b1-214">Получите ссылку на мини-приложение.</span><span class="sxs-lookup"><span data-stu-id="b82b1-214">Get a reference to the widget.</span></span>
    
- <span data-ttu-id="b82b1-215">Получите доступ к свойству **selectedItems** мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="b82b1-215">Access the **selectedItems** property of the widget.</span></span>
    
<span data-ttu-id="b82b1-216">Вы можете получить ссылку на мини-приложение с помощью приведенного ниже синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="b82b1-216">You can get a reference to the widget using the following syntax.</span></span>

```
var pplPicker = document.getElementById("PeoplePickerDiv")._officeControl;
```

<br/>

<span data-ttu-id="b82b1-217">Вы также можете сохранить ссылку при создании экземпляра мини-приложения.</span><span class="sxs-lookup"><span data-stu-id="b82b1-217">You can also save a reference when you instantiate the widget.</span></span>

```
var pplPicker = new Office.Controls.PeoplePicker(
                        document.getElementById("PeoplePickerDiv"), {});
```

<br/>

<span data-ttu-id="b82b1-218">Свойство **selectedItems** — это массив объектов, представляющих людей или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-218">The **selectedItems** property is an array of objects that represent people or groups.</span></span> <span data-ttu-id="b82b1-219">Люди или группы в массиве selectedItems могут быть разрешенными или неразрешенными. Это можно проверить с помощью свойства **isResolved**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-219">People or groups in the selectedItems array can be either resolved or unresolved, which you can check in the **isResolved** property.</span></span> <span data-ttu-id="b82b1-220">В приведенном ниже примере показано, как получить доступ к элементу *i* в массиве и использовать имя пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="b82b1-220">The following example shows how to access the element *i*  in the array and use the name of the person or group.</span></span>

```
var principal = pplPicker.selectedItems[i];
$("#msg").text(principal.text + " is selected in the control.");
```

<br/>

<span data-ttu-id="b82b1-221">Пример способа загрузки выбранных людей или групп из мини-приложения приведен на странице **demo.html** в разделе [Веб-виджеты Office экспериментальная демо-версия](https://code.msdn.microsoft.com/office/SharePoint-2013-Office-Web-6d44aa9e).</span><span class="sxs-lookup"><span data-stu-id="b82b1-221">For an example of how to retrieve the selected people or groups from the widget, see the **demo.html** page of the [Office Web Widgets - Experimental Demo](https://code.msdn.microsoft.com/office/SharePoint-2013-Office-Web-6d44aa9e) code sample.</span></span>

### <a name="customize-the-style-of-the-widget"></a><span data-ttu-id="b82b1-222">Настройка стиля мини-приложения</span><span class="sxs-lookup"><span data-stu-id="b82b1-222">Customize the style of the widget</span></span>

<span data-ttu-id="b82b1-223">Разработчику может потребоваться настроить пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="b82b1-223">As a developer, you might want to customize the look  feel of the widget. The following image shows the HTML hierarchy in the widget after it has been rendered.</span></span> <span data-ttu-id="b82b1-224">На рисунке ниже представлена HTML-иерархия мини-приложения после его преобразования.</span><span class="sxs-lookup"><span data-stu-id="b82b1-224">As a developer, you might want to customize the look  feel of the widget. The following image shows the HTML hierarchy in the widget after it has been rendered.</span></span> <span data-ttu-id="b82b1-225">Мини-приложение определяет множество классов с префиксом **office-peoplepicker**, которые можно найти и настроить в таблице стилей **Office.Controls.css**.</span><span class="sxs-lookup"><span data-stu-id="b82b1-225">The widget defines many classes prefixed by **office-peoplepicker**, which you can find and customize in the **Office.Controls.css** style sheet.</span></span>

<span data-ttu-id="b82b1-226">**HTML-иерархия в мини-приложении People Picker**</span><span class="sxs-lookup"><span data-stu-id="b82b1-226">**Figure 2. HTML hierarchy in the People Picker widget**</span></span>

![HTML-иерархия в мини-приложении People Picker](../images/PeoplePicker_HTMLHierarchy.png)

<span data-ttu-id="b82b1-228">Экспериментальное мини-приложение People Picker позволяет выбирать людей и группы в клиенте, а затем передавать выбранные субъекты в надстройку.</span><span class="sxs-lookup"><span data-stu-id="b82b1-228">You can use the experimental People Picker widget to select people and groups in your tenant, your add-in can then use the principals selected by your users. Please, provide ideas and comments in the  Office Developer Platform UserVoice site.</span></span> <span data-ttu-id="b82b1-229">Свои идеи и комментарии вы можете оставить на [сайте UserVoice для разработчиков Office](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="b82b1-229">Please provide ideas and comments at the [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>


## <a name="see-also"></a><span data-ttu-id="b82b1-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b82b1-230">See also</span></span>
<span data-ttu-id="b82b1-231"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b82b1-231"></span></span>

-  [<span data-ttu-id="b82b1-232">Использование экспериментального мини-приложения Desktop List View в надстройках для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b82b1-232">Use the experimental Desktop List View widget in SharePoint Add-ins</span></span>](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md)
-  [<span data-ttu-id="b82b1-233">Обзор экспериментальных мини-приложений Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="b82b1-233">Office Web Widgets - Experimental overview</span></span>](office-web-widgetsexperimental-overview.md)
-  [<span data-ttu-id="b82b1-234">Создание компонентов взаимодействия с пользователем в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b82b1-234">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
