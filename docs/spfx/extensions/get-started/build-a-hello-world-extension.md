---
title: "Создание первого расширения SharePoint Framework (Hello World, часть 1)"
description: "Создайте проект расширения, а затем напишите и отладьте настройщик заполнителей."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 3126f663ca6d7df21b37448386dd3baafe1fb1f8
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="build-your-first-sharepoint-framework-extension-hello-world-part-1"></a><span data-ttu-id="dfa2c-103">Создание первого расширения SharePoint Framework (Hello World, часть 1)</span><span class="sxs-lookup"><span data-stu-id="dfa2c-103">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>

<span data-ttu-id="dfa2c-p101">Расширения SharePoint Framework (SPFx) — это клиентские компоненты, которые запускаются в контексте страницы SharePoint. Расширения можно развертывать в SharePoint Online, используя для их создания современные инструменты и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-p101">SharePoint Framework (SPFx) Extensions are client-side components that run inside the context of a SharePoint page. You can deploy extensions to SharePoint Online, and you can use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="dfa2c-106">Действия, описанные в этой статье, также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-106">You can follow the steps in this article by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=yrFNu6K7iuU">
<img src="../../../images/spfx-ext-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="dfa2c-107">Создание проекта расширения</span><span class="sxs-lookup"><span data-stu-id="dfa2c-107">Create an extension project</span></span>

1. <span data-ttu-id="dfa2c-108">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-108">Create a new project directory in your favorite location.</span></span>

    ```
    md app-extension
    ```

2. <span data-ttu-id="dfa2c-109">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-109">Go to the project directory.</span></span>

    ```
    cd app-extension
    ```

3. <span data-ttu-id="dfa2c-110">Создайте расширение HelloWorld, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-110">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

    ```
    yo @microsoft/sharepoint
    ```

4. <span data-ttu-id="dfa2c-111">Когда появится запрос:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-111">When prompted:</span></span>

    * <span data-ttu-id="dfa2c-112">Оставьте имя решения по умолчанию **app-extension** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-112">Accept the default app-extension as your solution name, and press Enter.</span></span>
    * <span data-ttu-id="dfa2c-113">Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-113">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
    * <span data-ttu-id="dfa2c-114">Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-114">Select **Use the current folder**, and select Enter.</span></span>
    * <span data-ttu-id="dfa2c-115">Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-115">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
    * <span data-ttu-id="dfa2c-116">Выберите **Extension** (Расширение) в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-116">Select **Extension** as the client-side component type to be created.</span></span> 
    * <span data-ttu-id="dfa2c-117">Выберите для создаваемого расширения тип **Настройщик заполнителей**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-117">Select **Field Customizer** as the extension type to be created.</span></span>

5. <span data-ttu-id="dfa2c-118">Дальше требуется указать информацию о расширении.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-118">The next set of prompts ask for specific information about your extension:</span></span> <span data-ttu-id="dfa2c-119">Когда появится запрос:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-119">When prompted:</span></span>

    * <span data-ttu-id="dfa2c-120">Оставьте значение по умолчанию (**HelloWorld**) для имени расширения и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-120">Accept the default value of **HelloWorld** as your extension name, and then select Enter.</span></span>
    * <span data-ttu-id="dfa2c-121">Оставьте значение по умолчанию (**HelloWorld description**) для описания расширения и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-121">Accept the default value of **HelloWorld description** as your extension description, and select Enter.</span></span>

    <br/>

    ![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../images/ext-yeoman-app-prompts.png)

    > [!NOTE] 
    > <span data-ttu-id="dfa2c-123">Если использовать слишком длинное имя для расширения, могут возникнуть проблемы.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-123">If you use a name for the extension that is too long, you might encounter issues.</span></span> <span data-ttu-id="dfa2c-124">Предоставленные записи используются для создания псевдонима для манифеста настройщика заполнителей в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-124">The entries provided are used to generate an alias entry for the application customizer manifest json file.</span></span> <span data-ttu-id="dfa2c-125">Если длина псевдонима превышает 40 знаков, система выдает исключение при выполнении команды `gulp serve --nobrowser`.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-125">If the alias is longer than 40 characters, you will get an exception when you try to serve the extension using `gulp serve --nobrowser`.</span></span> <span data-ttu-id="dfa2c-126">Чтобы решить эту проблему, обновите запись псевдонима.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-126">You can resolve this by updating the alias entry afterward.</span></span>

    <span data-ttu-id="dfa2c-127">На этом этапе Yeoman устанавливает необходимые зависимости и формирует шаблон файлов решения вместе с расширением **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-127">At this point, Yeoman installs the required dependencies and scaffolds the solution files along with the **HelloWorld** extension.</span></span> <span data-ttu-id="dfa2c-128">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-128">This might take a few minutes.</span></span> 

    <span data-ttu-id="dfa2c-129">Когда скаффолдинг успешно закончится, появится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-129">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

    !["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../images/ext-yeoman-app-complete.png)

    <span data-ttu-id="dfa2c-131">Сведения об устранении неполадок см. в статье [Известные проблемы](../../known-issues-and-common-questions.md).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-131">For information about troubleshooting any errors, see [Known issues](../../known-issues-and-common-questions.md).</span></span>

6. <span data-ttu-id="dfa2c-132">После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-132">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

    ```sh
    npm shrinkwrap
    ```

7. <span data-ttu-id="dfa2c-133">Далее введите в консоли приведенную ниже команду, чтобы запустить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-133">Next, type the following into the console to start Visual Studio Code.</span></span>

    ```
    code .
    ```

    > [!NOTE] 
    > <span data-ttu-id="dfa2c-134">Так как клиентское решение SharePoint основано на HTML и TypeScript, для разработки расширения можно использовать любой редактор кода, поддерживающий клиентскую разработку.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-134">Because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

    <span data-ttu-id="dfa2c-p105">Обратите внимание, что стандартная структура решения аналогична структуре клиентских веб-частей. Это базовая структура решения SharePoint Framework, многие параметры которой не зависят от типа решения.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-p105">Notice how the default solution structure looks like the solution structure for client-side web parts. This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

    ![Решение SharePoint Framework, открытое после первоначального формирования](../../../images/ext-app-vscode-solution-structure.png)

8. <span data-ttu-id="dfa2c-138">Откройте файл **HelloWorldApplicationCustomizer.manifest.json** в папке src\extensions\helloWorld.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-138">Open **HelloWorldApplicationCustomizer.manifest.json** in the src\extensions\helloWorld folder.</span></span>

    <span data-ttu-id="dfa2c-p106">В этом файле определяются тип расширения и уникальный идентификатор для него. Этот идентификатор потребуется позже, при отладке и развертывании расширения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-p106">This file defines your extension type and a unique identifier for your extension. You’ll need this ID later when you debug and deploy your extension to SharePoint.</span></span>

    ![Содержимое манифеста настройщика заполнителей в формате JSON](../../../images/ext-app-vscode-manifest.png)

## <a name="code-your-application-customizer"></a><span data-ttu-id="dfa2c-142">Написание кода настройщика заполнителей</span><span class="sxs-lookup"><span data-stu-id="dfa2c-142">Code your Application Customizer</span></span> 

<span data-ttu-id="dfa2c-143">Откройте файл **HelloWorldApplicationCustomizer.ts** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-143">Open the **HelloWorldApplicationCustomizer.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="dfa2c-144">Обратите внимание, что базовый класс для настройщика заполнителей импортируется из пакета **sp-application-base**, который содержит код платформы SharePoint Framework, необходимый для настройщика заполнителей.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-144">Notice that base class for the Application Customizer is imported from the **sp-application-base** package, which contains SharePoint framework code required by the Application Customizer.</span></span> 

![Оператор импорта ресурса BaseApplicationCustomizer из каталога @microsoft/sp-application-base](../../../images/ext-app-vscode-app-base.png)

<span data-ttu-id="dfa2c-146">Логика настройщика заполнителей содержится в методе **onInit**, который вызывается при первой активации клиентского расширения на странице.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-146">The logic for your Application Customizer is contained in the **onInit** method, which is called when the client-side extension is first activated on the page.</span></span> <span data-ttu-id="dfa2c-147">Это событие происходит после назначения классов `this.context` и `this.properties`.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-147">This event occurs after `this.context` and `this.properties` are assigned.</span></span> <span data-ttu-id="dfa2c-148">Как и в случае с веб-частями, метод `onInit()` возвращает обещание, которое можно использовать для выполнения асинхронных операций.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-148">onInit() is called when the client-side extension is first activated on the page. This event occurs after  and  are assigned. As with web parts, `onInit()` returns a promise that you can use to perform asynchronous operations.</span></span>

> [!NOTE] 
> <span data-ttu-id="dfa2c-p108">Конструктор класса вызывается вначале, когда классы `this.context` и `this.properties` не определены. Пользовательская логика инициализации здесь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-p108">The class constructor is called at an early stage, when `this.context` and `this.properties` are undefined. Custom initiation logic is not supported here.</span></span>

<span data-ttu-id="dfa2c-p109">Ниже представлено содержимое методов **onInit()** в решении по умолчанию. Оно просто записывает журнал на панель мониторинга для разработчиков, а затем выводит простое предупреждение JavaScript при отрисовке страницы.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-p109">The following are the contents of **onInit()** in the default solution. This default solution writes a log to the Dev Dashboard, and then displays a simple JavaScript alert when the page renders.</span></span>

![Метод onInit по умолчанию в коде](../../../images/ext-app-vscode-methods.png)

<span data-ttu-id="dfa2c-154">Если настройщик заполнителей использует входные данные **ClientSideComponentProperties** в формате JSON, он десериализуется в объект **BaseExtension.properties**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-154">If your Application Customizer uses the **ClientSideComponentProperties** JSON input, it is deserialized into the **BaseExtension.properties** object.</span></span> <span data-ttu-id="dfa2c-155">Вы можете определить интерфейс для его описания.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-155">You can define an interface to describe it.</span></span> <span data-ttu-id="dfa2c-156">Шаблон по умолчанию ищет свойство под названием **testMessage**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-156">The default template is looking for a property called **testMessage**.</span></span> <span data-ttu-id="dfa2c-157">Если это свойство указано, он выводит его в предупреждении.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-157">If that property is provided, it outputs it in an alert message.</span></span>

## <a name="debug-your-application-customizer"></a><span data-ttu-id="dfa2c-158">Отладка настройщика заполнителей</span><span class="sxs-lookup"><span data-stu-id="dfa2c-158">Code your Application Customizer</span></span>

<span data-ttu-id="dfa2c-159">В настоящее время для проверки расширений SharePoint Framework нельзя использовать локальную версию Workbench.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-159">You cannot currently use the local workbench to test SharePoint Framework Extensions.</span></span> <span data-ttu-id="dfa2c-160">Их необходимо проверять на активном сайте SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-160">You'll need to test them  against a live SharePoint Online site.</span></span> <span data-ttu-id="dfa2c-161">Для этого не нужно развертывать настройку в каталоге приложений, что делает процесс отладки простым и эффективным.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-161">You don't have to deploy your customization to the App Catalog to do this, which makes the debugging experience simple and efficient.</span></span> 

1. <span data-ttu-id="dfa2c-162">Скомпилируйте код и разместите скомпилированные файлы на локальном компьютере, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-162">First, compile your code and host the compiled files from your local computer by running the following command.</span></span>

    ```
    gulp serve --nobrowser
    ```

    > [!NOTE] 
    > <span data-ttu-id="dfa2c-163">Если у вас не установлен сертификат разработчика SPFx, Workbench сообщит вам, что он не загружает скрипты с домена localhost.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-163">If you do not have the SPFx developer certificate installed, then Workbench will notify you that it is configured not to load scripts from localhost.</span></span> <span data-ttu-id="dfa2c-164">В этом случае остановите выполняющийся в окне консоли процесс, выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика, а затем выполните команду `gulp serve --nobrowser` еще раз.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-164">If you do not have the SPFx developer certificate installed, Workbench will notify you that it is not configured to load scripts from localhost. If this happens, stop the process that is currently running in the console window, run the `gulp trust-dev-cert` command in your project directory console to install the developer certificate, and then run the `gulp serve --nobrowser` command again.</span></span>

    <span data-ttu-id="dfa2c-165">Параметр `--nobrowser` используется, так как запускать локальную версию Workbench не нужно (локальная отладка расширений невозможна).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-165">You use the `--nobrowser` option because you don't need to launch the local workbench, since you can't debug extensions locally.</span></span>

    <span data-ttu-id="dfa2c-166">Когда компиляция кода завершится без ошибок, полученный манифест будет доступен по адресу https://localhost:4321.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-166">When the code compiles without errors, it will serve the resulting manifest from https://localhost:4321.</span></span>

    ![Gulp serve](../../../images/ext-app-gulp-serve.png)

2. <span data-ttu-id="dfa2c-168">Чтобы протестировать расширение, перейдите на современную страницу представления списка в среде SharePoint и добавьте к URL-адресу следующие параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-168">To test your extension, navigate to a modern list view page in your SharePoint environment and append the following query string parameters to the URL:</span></span> <span data-ttu-id="dfa2c-169">Обратите внимание, что идентификатор необходимо обновить в соответствии с идентификатором вашего расширения.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-169">Notice that you will need to update the ID to match your own extension identifier available from the HelloWorldFieldCustomizer.manifest.json file.</span></span> <span data-ttu-id="dfa2c-170">Он указан в файле **HelloWorldApplicationCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-170">This is available in the **HelloWorldApplicationCustomizer.manifest.json** file.</span></span>

    ```json
        ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
    ```

    <span data-ttu-id="dfa2c-171">Дополнительные сведения о параметрах запросов URL-адресов:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-171">More detail about the URL query parameters:</span></span>

    * <span data-ttu-id="dfa2c-172">**loadSPFX=true**</span><span class="sxs-lookup"><span data-stu-id="dfa2c-172">**loadSPFX=true**.</span></span> <span data-ttu-id="dfa2c-173">проверяет, загружена ли на странице платформа SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-173">loadSPFX=true ensures that the SharePoint Framework is loaded on the page.</span></span> <span data-ttu-id="dfa2c-174">Для загрузки платформы должно быть зарегистрировано по крайней мере одно расширение.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-174">For performance reasons, the framework is not normally loaded unless at least one extension is registered.</span></span> <span data-ttu-id="dfa2c-175">Так как компоненты еще не зарегистрированы, платформу нужно загрузить вручную.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-175">Because no components are registered yet, we must explicitly load the framework.</span></span>

    * <span data-ttu-id="dfa2c-176">**debugManifestsFile**</span><span class="sxs-lookup"><span data-stu-id="dfa2c-176">**debugManifestsFile**.</span></span> <span data-ttu-id="dfa2c-177">указывает, что нужно загрузить локально сохраненные компоненты SPFx.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-177">debugManifestsFile specifies that you want to load SPFx components that are locally served.</span></span> <span data-ttu-id="dfa2c-178">Загрузчик ищет компоненты только в каталоге приложений (для развернутого решения) и на сервере манифестов SharePoint (для системных библиотек).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-178">The loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>

    * <span data-ttu-id="dfa2c-179">**customActions**</span><span class="sxs-lookup"><span data-stu-id="dfa2c-179">**customActions**.</span></span> <span data-ttu-id="dfa2c-180">имитируют дополнительное действие.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-180">Simulates a custom action.</span></span> <span data-ttu-id="dfa2c-181">При развертывании и регистрации этого компонента на сайте вы создадите объект **CustomAction** и опишете все свойства, которые можно задать для него.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-181">customActions - Simulates a custom action. When you deploy and register this component in a site, you'll create this **CustomAction** object and describe all the different properties you can set on it.</span></span> 
        * <span data-ttu-id="dfa2c-182">**Key**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-182">Key</span></span> <span data-ttu-id="dfa2c-183">Используйте GUID расширения в качестве ключа, связываемого с дополнительным действием.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-183">Key: use the Guid of the extension as the key to associate with the custom action</span></span> <span data-ttu-id="dfa2c-184">Он должен соответствовать идентификатору расширения, указанному в файле manifest.json.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-184">Key - Use the Guid of the extension as the key to associate with the custom action. This has to match the ID value of your extension, which is available in the extension manifest.json file.</span></span>
        * <span data-ttu-id="dfa2c-185">**Location**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-185">**location**</span></span> <span data-ttu-id="dfa2c-186">Тип дополнительного действия.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-186">The type of action.</span></span> <span data-ttu-id="dfa2c-187">Используйте `ClientSideExtension.ApplicationCustomizer` для расширения "Настройщик заполнителей".</span><span class="sxs-lookup"><span data-stu-id="dfa2c-187">Use `ClientSideExtension.ApplicationCustomizer` for the Application Customizer extension.</span></span>
        * <span data-ttu-id="dfa2c-188">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-188">Properties</span></span> <span data-ttu-id="dfa2c-189">Необязательный объект JSON, содержащий свойства, доступные через элемент **this.properties**.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-189">Properties - An optional JSON object that contains properties that will be available via the **this.properties** member. In this HelloWorld example, it defined a ‘testMessage’ property.</span></span> <span data-ttu-id="dfa2c-190">В этом примере HelloWorld он определяет свойство `testMessage`.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-190">In this HelloWorld example, it defined a `testMessage` property.</span></span>


3. <span data-ttu-id="dfa2c-191">Перейдите в современный список в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-191">Go to a modern list in SharePoint Online.</span></span> <span data-ttu-id="dfa2c-192">Это может быть список или библиотека.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-192">This can be a list or a library.</span></span> <span data-ttu-id="dfa2c-193">Настройщики заполнителей также поддерживаются на современных страницах и на странице "Содержимое сайта".</span><span class="sxs-lookup"><span data-stu-id="dfa2c-193">Application Customizers are also supported in modern pages and on the Site Contents page.</span></span> 

4. <span data-ttu-id="dfa2c-194">Дополните URL-адрес описанными параметрами запроса.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-194">Extend the URL with the additional query parameters described.</span></span> <span data-ttu-id="dfa2c-195">Обратите внимание, что GUID необходимо обновить в соответствии с идентификатором вашего настройщика заполнителей.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-195">Extend the URL with the additional query parameters described. Notice that you'll need to update the GUID to match the ID of your custom Application Customizer.</span></span> 

    <span data-ttu-id="dfa2c-196">Полный URL-адрес должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dfa2c-196">The full URL should look similar to the following:</span></span>

    ```json
    contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
    ```

5. <span data-ttu-id="dfa2c-197">Выберите **Загрузить скрипты отладки**, чтобы продолжить загрузку скриптов с домена localhost.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-197">Choose **Load debug scripts** to continue loading scripts from your local host.</span></span>

    ![Запрос разрешения на отладку манифеста на странице](../../../images/ext-app-debug-manifest-message.png)

    <br/>

    <span data-ttu-id="dfa2c-199">На странице должно появиться сообщение с запросом.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-199">You should now see the dialog message on your page.</span></span>

    ![Hello как предупреждение свойства](../../../images/ext-app-alert-sp-page.png)

    <span data-ttu-id="dfa2c-201">Это диалоговое окно выводится вашим расширением SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-201">This dialog is thrown by your SharePoint Framework Extension.</span></span> <span data-ttu-id="dfa2c-202">Обратите внимание: так как вы указали свойство `testMessage` в составе параметров запроса отладки, оно включено в предупреждение.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-202">Note that because you provided the `testMessage` property as part of the debug query parameters, it's included in the alert message.</span></span> <span data-ttu-id="dfa2c-203">Вы можете настроить экземпляры расширения на основе свойств компонента клиента, которые передаются в режиме выполнения.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-203">You can configure your extension instances based on the client component properties, which are passed for the instance also in runtime mode.</span></span>

> [!NOTE] 
> <span data-ttu-id="dfa2c-p123">Если у вас возникли проблемы с отладкой, проверьте используемые параметры запроса URL-адреса. Некоторые браузеры кодируют параметры, что иногда влияет на поведение запросов.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-p123">If you have issues with debugging, double-check the URL query parameters used for the query. Some browsers encode the parameters and in some scenarios this affects the behavior.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfa2c-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dfa2c-206">Next steps</span></span>

<span data-ttu-id="dfa2c-207">Поздравляем, вы создали свое первое расширение SharePoint Framework!</span><span class="sxs-lookup"><span data-stu-id="dfa2c-207">Congratulations, you got your first SharePoint Framework Extension running!</span></span> 

<span data-ttu-id="dfa2c-208">Продолжение читайте в статье [Использование заполнителей страниц в настройщике заполнителей (Hello World, часть 2)](./using-page-placeholder-with-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-208">To continue building out your extension, see [Using page placeholders from Application Customizer (Hello World part 2)](./using-page-placeholder-with-extensions.md).</span></span> <span data-ttu-id="dfa2c-209">Вы будете работать с тем же проектом и получите доступ к специальным заполнителям для изменения пользовательского интерфейса SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-209">You use the same project and take advantage of specific content placeholders for modifying the UI of SharePoint.</span></span> <span data-ttu-id="dfa2c-210">Обратите внимание, что команда `gulp serve` по-прежнему запущена в окне консоли (или в Visual Studio Code, если вы используете этот редактор).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-210">Notice that the `gulp serve` command is still running in your console window (or in Visual Studio Code if you using that as editor).</span></span> <span data-ttu-id="dfa2c-211">Можете переходить к следующей статье, не останавливая ее.</span><span class="sxs-lookup"><span data-stu-id="dfa2c-211">You can continue to let it run while you go to the next article.</span></span>

> [!NOTE]
> <span data-ttu-id="dfa2c-212">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="dfa2c-212">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="dfa2c-213">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="dfa2c-213">Thanks for your input advance.</span></span>