# <a name="build-your-first-sharepoint-framework-extension-hello-world-part-1"></a><span data-ttu-id="d2e88-101">Создание первого расширения SharePoint Framework (Hello World, часть 1)</span><span class="sxs-lookup"><span data-stu-id="d2e88-101">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>

<span data-ttu-id="d2e88-p101">Расширения SharePoint Framework (SPFx) — это клиентские компоненты, которые запускаются в контексте страницы SharePoint. Расширения можно развертывать в SharePoint Online, используя для их создания современные инструменты и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p101">SharePoint Framework (SPFx) Extensions are client-side components that run inside the context of a SharePoint page. You can deploy extensions to SharePoint Online, and you can use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="d2e88-104">В этой статье описано, как создать свое первое расширение SharePoint Framework Hello World.</span><span class="sxs-lookup"><span data-stu-id="d2e88-104">This article describes how to create your first Hello World SharePoint Framework Extension.</span></span> <span data-ttu-id="d2e88-105">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="d2e88-105">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=0BeS0HukW24&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=yrFNu6K7iuU">
<img src="../../../images/spfx-ext-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="d2e88-106">Создание проекта расширения</span><span class="sxs-lookup"><span data-stu-id="d2e88-106">Create an extension project</span></span>

1. <span data-ttu-id="d2e88-107">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="d2e88-107">Create a new project directory in your favorite location.</span></span>

    ```
    md app-extension
    ```

2. <span data-ttu-id="d2e88-108">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="d2e88-108">Go to the project directory.</span></span>

    ```
    cd app-extension
    ```

3. <span data-ttu-id="d2e88-109">Создайте расширение HelloWorld, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d2e88-109">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

    ```
    yo @microsoft/sharepoint
    ```

4. <span data-ttu-id="d2e88-110">Когда появится запрос, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d2e88-110">When prompted:</span></span>

    * <span data-ttu-id="d2e88-111">Оставьте имя решения по умолчанию **app-extension** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-111">Accept the default **app-extension** as your solution name, and press **Enter**.</span></span>
    * <span data-ttu-id="d2e88-112">Выберите **Только SharePoint Online (новая версия)** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-112">Choose **SharePoint Online only (latest)**, and press **Enter**.</span></span>
    * <span data-ttu-id="d2e88-113">Выберите **Использовать текущую папку** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-113">Choose **Use the current folder**, and press **Enter**.</span></span>
    * <span data-ttu-id="d2e88-114">Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="d2e88-114">Choose **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
    * <span data-ttu-id="d2e88-115">Выберите **Расширение** в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="d2e88-115">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
    * <span data-ttu-id="d2e88-116">Выберите для создаваемого расширения тип **Настройщик приложения**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-116">Choose **Application Customizer (Preview)** as the extension type to be created.</span></span>

5. <span data-ttu-id="d2e88-p103">Далее вам потребуется указать определенные сведения о расширении. Когда появится запрос, сделайте вот что:</span><span class="sxs-lookup"><span data-stu-id="d2e88-p103">The next set of prompts will ask for specific information about your extension. When prompted:</span></span>

    * <span data-ttu-id="d2e88-119">Оставьте значение по умолчанию (**HelloWorld**) для имени расширения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-119">Accept the default **HelloWorld** as your extension name, and press **Enter**.</span></span>
    * <span data-ttu-id="d2e88-120">Оставьте значение по умолчанию (**HelloWorld description**) для описания расширения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-120">Accept the default **HelloWorld description** as your extension description, and press **Enter**.</span></span>

    ![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../images/ext-yeoman-app-prompts.png)

    > <span data-ttu-id="d2e88-122">**Примечание.** Если вы используете слишком длинное имя для расширения, могут возникнуть проблемы.</span><span class="sxs-lookup"><span data-stu-id="d2e88-122">**Note:** If you use a name for the extension that is too long, you might encounter issues.</span></span> <span data-ttu-id="d2e88-123">Предоставленные записи используются для создания записи псевдонима для манифеста настройщика приложений в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="d2e88-123">The entries provided are used to generate an alias entry for the application customizer manifest json file.</span></span> <span data-ttu-id="d2e88-124">Если длина псевдонима превышает 40 знаков, система выдаст ошибку исключения при попытке обработать расширение с помощью `gulp serve --nobrowser`.</span><span class="sxs-lookup"><span data-stu-id="d2e88-124">If the alias is longer than 40 characters, you will get an exception when you try to serve the extension using `gulp serve --nobrowser`.</span></span> <span data-ttu-id="d2e88-125">Впоследствии вы можете решить эту проблему, обновив запись псевдонима.</span><span class="sxs-lookup"><span data-stu-id="d2e88-125">You can resolve this by updating the alias entry afterward.</span></span>

    <span data-ttu-id="d2e88-p105">После этого Yeoman установит необходимые зависимости и сформирует файлы решения, а также расширение **HelloWorld**. Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p105">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** extension. This might take a few minutes.</span></span> 

    <span data-ttu-id="d2e88-128">После успешного скаффолдинга должно появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="d2e88-128">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

    !["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../images/ext-yeoman-app-complete.png)

    <span data-ttu-id="d2e88-130">Сведения об устранении неполадок см. в статье [Известные проблемы](../../known-issues-and-common-questions.md).</span><span class="sxs-lookup"><span data-stu-id="d2e88-130">For information about troubleshooting any errors, see [Known issues](../../known-issues-and-common-questions.md).</span></span>

6. <span data-ttu-id="d2e88-131">После скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2e88-131">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

    ```sh
    npm shrinkwrap
    ```

7. <span data-ttu-id="d2e88-132">Далее введите в консоли приведенную ниже команду, чтобы запустить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d2e88-132">Once solution scaffolding is completed, type the following into the console to start Visual Studio Code.</span></span>

    ```
    code .
    ```

    ><span data-ttu-id="d2e88-133">**Примечание.** Клиентское решение SharePoint создано с помощью HTML и TypeScript, поэтому для разработки расширения можно использовать любой редактор кода, который поддерживает клиентское программирование.</span><span class="sxs-lookup"><span data-stu-id="d2e88-133">**Note:** Because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

    <span data-ttu-id="d2e88-p106">Обратите внимание, что стандартная структура решения аналогична структуре клиентских веб-частей. Это базовая структура решения SharePoint Framework, многие параметры которой не зависят от типа решения.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p106">Notice how the default solution structure looks like the solution structure for client-side web parts. This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

    ![Решение SharePoint Framework, открытое после первоначального формирования](../../../images/ext-app-vscode-solution-structure.png)

8. <span data-ttu-id="d2e88-137">Откройте файл **HelloWorldApplicationCustomizer.manifest.json** в папке src\extensions\helloWorld.</span><span class="sxs-lookup"><span data-stu-id="d2e88-137">Open **HelloWorldApplicationCustomizer.manifest.json** in the src\extensions\helloWorld folder.</span></span>

    <span data-ttu-id="d2e88-p107">В этом файле определяются тип расширения и уникальный идентификатор для него. Этот идентификатор потребуется позже, при отладке и развертывании расширения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p107">This file defines your extension type and a unique identifier for your extension. You’ll need this ID later when you debug and deploy your extension to SharePoint.</span></span>

    ![Содержимое манифеста настройщика приложений в формате JSON](../../../images/ext-app-vscode-manifest.png)

## <a name="code-your-application-customizer"></a><span data-ttu-id="d2e88-141">Написание кода настройщика приложений</span><span class="sxs-lookup"><span data-stu-id="d2e88-141">Code your Application Customizer</span></span> 
<span data-ttu-id="d2e88-142">Откройте файл **HelloWorldApplicationCustomizer.ts** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-142">Open the **HelloWorldApplicationCustomizer.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="d2e88-143">Обратите внимание, что базовый класс для настройщика приложений импортируется из пакета **sp-application-base**, который содержит код платформы SharePoint Framework, необходимый для настройщика приложений.</span><span class="sxs-lookup"><span data-stu-id="d2e88-143">Notice that base class for the Application Customizer is imported from the **sp-application-base** package, which contains SharePoint framework code required by the Application Customizer.</span></span> 

![Оператор импорта ресурса BaseApplicationCustomizer из каталога @microsoft/sp-application-base](../../../images/ext-app-vscode-app-base.png)

<span data-ttu-id="d2e88-145">Логика настройщика приложений содержится в методе **onInit**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-145">The logic for your Application Customizer is contained in the **onInit** method.</span></span>

- <span data-ttu-id="d2e88-p108">**onInit()** вызывается, когда клиентское расширение впервые активируется на странице. Это событие происходит после назначения ```this.context``` и ```this.properties```. Как и в случае с веб-частями, ```onInit()``` возвращает обещание, которое можно использовать для выполнения асинхронных операций.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p108">**onInit()** is called when the client-side extension is first activated on the page. This event occurs after ```this.context``` and ```this.properties``` are assigned. As with web parts, ```onInit()``` returns a promise that you can use to perform asynchronous operations.</span></span>

><span data-ttu-id="d2e88-p109">**Примечание.** Конструктор класса вызывается на раннем этапе, когда элементы ```this.context``` и ```this.properties``` не определены. Пользовательская логика инициализации здесь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p109">**Note:** The class constructor is called at an early stage, when ```this.context``` and ```this.properties``` are undefined. Custom initiation logic is not supported here.</span></span>

<span data-ttu-id="d2e88-p110">Ниже представлено содержимое методов **onInit()** в решении по умолчанию. Оно просто записывает журнал на панель мониторинга для разработчиков, а затем выводит простое предупреждение JavaScript при отрисовке страницы.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p110">The following are the contents of **onInit()** in the default solution. This default solution writes a log to the Dev Dashboard, and then displays a simple JavaScript alert when the page renders.</span></span>

![Метод onInit по умолчанию в коде](../../../images/ext-app-vscode-methods.png)

<span data-ttu-id="d2e88-p111">Если настройщик приложений использует входные данные **ClientSideComponentProperties** в формате JSON, он будет десериализован в объект **BaseExtension.properties**. Вы можете определить интерфейс, описывающий его. Шаблон по умолчанию ищет свойство **testMessage** и, если оно предоставлено, выводит его в качестве предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p111">If your application customizer uses the **ClientSideComponentProperties** JSON input, it will be deserialized into the **BaseExtension.properties** object. You can define an interface to describe it. The default template is looking for a property called **testMessage**. If that property is provided, it outputs it in an alert message.</span></span>

## <a name="debug-your-application-customizer-using-gulp-serve-and-query-string-parameters"></a><span data-ttu-id="d2e88-158">Отладка настройщика приложений с помощью gulp serve и параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="d2e88-158">Debug your Application Customizer using gulp serve and query string parameters</span></span>
<span data-ttu-id="d2e88-159">В настоящее время использование локального рабочего места для проверки расширений SharePoint Framework невозможно.</span><span class="sxs-lookup"><span data-stu-id="d2e88-159">You cannot current use the local workbench to test SharePoint Framework Extensions.</span></span> <span data-ttu-id="d2e88-160">Их необходимо проверить с помощью действующего сайта SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d2e88-160">You'll need to test them  against a live SharePoint Online site.</span></span> <span data-ttu-id="d2e88-161">Для этого вам не нужно развертывать модификацию каталога приложений, что делает процесс отладки простым и эффективным.</span><span class="sxs-lookup"><span data-stu-id="d2e88-161">You don't have to deploy your customization to the app catalog to do this, which makes the debugging experience simple and efficient.</span></span> 

<span data-ttu-id="d2e88-162">Для начала скомпилируйте код и разместите скомпилированные файлы с локального компьютера, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="d2e88-162">First, compile your code and host the compiled files from your local computer by running the following command.</span></span>

```
gulp serve --nobrowser
```

><span data-ttu-id="d2e88-p113">**Примечание.** Если у вас не установлен сертификат разработчика SPFx, среда программирования сообщит вам, что она не загружает сценарии из localhost. Если это произошло, остановите текущий процесс в окне консоли и выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика, а затем выполните команду `gulp serve --nobrowser` еще раз.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p113">**Note:** If you do not have the SPFx developer certificate installed, Workbench will notify you that it is not configured to load scripts from localhost. If this happens, stop the process that is currently running in the console window, run the `gulp trust-dev-cert` command in your project directory console to install the developer certificate, and then run the `gulp serve --nobrowser` command again.</span></span>

<span data-ttu-id="d2e88-165">Так как запускать локальное рабочее место не требуется (в настоящее время невозможно выполнять отладку расширений локально), используется параметр ```--nobrowser```.</span><span class="sxs-lookup"><span data-stu-id="d2e88-165">You use the ```--nobrowser``` option because you don't need to launch the local workbench, since you can't debug extensions locally.</span></span>

<span data-ttu-id="d2e88-166">Когда компиляция кода завершится без ошибок, полученный манифест будет доступен по адресу http://localhost:4321.</span><span class="sxs-lookup"><span data-stu-id="d2e88-166">When the code compiles without errors, it will serve the resulting manifest from http://localhost:4321.</span></span>

![Gulp serve](../../../images/ext-app-gulp-serve.png)

<span data-ttu-id="d2e88-p114">Чтобы проверить расширение, перейдите на современную страницу представления списка в среде SharePoint и добавьте следующие параметры строки запроса в URL-адрес. Обратите внимание, что вам потребуется обновить идентификатор в соответствии с идентификатором расширения. Он указан в файле **HelloWorldApplicationCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p114">To test your extension, go to a modern list view page in your SharePoint environment and append the following query string parameters to the URL. Notice that you will need to update the ID to match your own extension identifier. This is available in the **HelloWorldApplicationCustomizer.manifest.json** file.</span></span>

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
```

<span data-ttu-id="d2e88-171">Дополнительные сведения о параметрах запросов URL-адресов</span><span class="sxs-lookup"><span data-stu-id="d2e88-171">More detail about the URL query parameters:</span></span>

* <span data-ttu-id="d2e88-p115">**loadSPFX=true** — гарантирует, что платформа SharePoint Framework загружается на странице. Для оптимальной производительности платформа обычно не загружается, если не зарегистрировано хотя бы одно расширение. Так как пока не зарегистрировано ни одного расширения, нам необходимо отдавать явную команду на загрузку платформы.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p115">**loadSPFX=true** - Ensures that the SharePoint Framework is loaded on the page. For performance reasons, the framework does not load unless at least one extension is registered. Because no components are registered,you must explicitly load the framework.</span></span>

* <span data-ttu-id="d2e88-p116">**debugManifestsFile** — указывает, что нам требуется загрузить компоненты SPFx, предоставляемые локально. Загрузчик ищет компоненты только в каталоге приложений (для развернутого решения) и на сервере манифестов SharePoint (для системных библиотек).</span><span class="sxs-lookup"><span data-stu-id="d2e88-p116">**debugManifestsFile** - Specifies that you want to load SPFx components that are locally served. The loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>

* <span data-ttu-id="d2e88-p117">**customActions** — имитирует дополнительное действие. При фактическом развертывании и регистрации этого компонента на сайте вы создадите объект **CustomAction** и опишете все свойства, которые можно задать для него.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p117">**customActions** - Simulates a custom action. When you deploy and register this component in a site, you'll create this **CustomAction** object and describe all the different properties you can set on it.</span></span> 
    * <span data-ttu-id="d2e88-p118">**Key** — используйте GUID расширения в качестве ключа для связывания с дополнительным действием. Он должен совпадать с идентификатором расширения, указанным в файле manifest.json.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p118">**Key** - Use the Guid of the extension as the key to associate with the custom action. This has to match the ID value of your extension, which is available in the extension manifest.json file.</span></span>
    * <span data-ttu-id="d2e88-p119">**Location** — тип дополнительного действия. Для расширения настройщика приложений используйте значение "ClientSideExtension.ApplicationCustomizer".</span><span class="sxs-lookup"><span data-stu-id="d2e88-p119">**Location** - The type of custom action. Use "ClientSideExtension.ApplicationCustomizer" for the Application Customizer extension.</span></span>
    * <span data-ttu-id="d2e88-p120">**Properties** — необязательный объект JSON, содержащий свойства, которые будут доступны через элемент **this.properties**. В примере HelloWorld он определен как свойство testMessage.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p120">**Properties** - An optional JSON object that contains properties that will be available via the **this.properties** member. In this HelloWorld example, it defined a ‘testMessage’ property.</span></span>


<span data-ttu-id="d2e88-p121">Перейдите ко встроенному современному списку в SharePoint Online. Это может быть список или библиотека. Настройщики приложений также поддерживаются на современных страницах и на странице "Содержимое сайта".</span><span class="sxs-lookup"><span data-stu-id="d2e88-p121">Go to a modern list in SharePoint Online. This can be either a list or a library. Application customizers are also supported in modern pages and on the Site Contents page.</span></span> 

<span data-ttu-id="d2e88-p122">Расширьте URL-адрес дополнительными параметрами запроса, описанными здесь. Обратите внимание, что вам необходимо будет обновить GUID для соответствия идентификатору вашего настройщика приложений.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p122">Extend the URL with the additional query parameters described. Notice that you'll need to update the GUID to match the ID of your custom Application Customizer.</span></span> 

<span data-ttu-id="d2e88-190">Полный URL-адрес должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d2e88-190">The full URL should look similar to the following:</span></span>

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"testMessage":"Hello as property!"}}}
```

<span data-ttu-id="d2e88-191">Выберите **Загрузить скрипты отладки**, чтобы продолжить загрузку скриптов с локального узла.</span><span class="sxs-lookup"><span data-stu-id="d2e88-191">Choose **Load debug scripts** to continue loading scripts from your local host.</span></span>

![Запрос разрешения на отладку манифеста на странице](../../../images/ext-app-debug-manifest-message.png)

<span data-ttu-id="d2e88-193">На странице должно появиться сообщение с запросом.</span><span class="sxs-lookup"><span data-stu-id="d2e88-193">You should now see the alert message on your page.</span></span>

![Hello как предупреждение свойства](../../../images/ext-app-alert-sp-page.png)

<span data-ttu-id="d2e88-195">Ваше расширение SharePoint Framework открывает это диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d2e88-195">This dialog is thrown by your SharePoint Framework Extension.</span></span> <span data-ttu-id="d2e88-196">Обратите внимание: так как вы указали свойство **testMessage** в составе параметров запроса отладки, оно входит в сообщение с предупреждением.</span><span class="sxs-lookup"><span data-stu-id="d2e88-196">Note that because you provided the **testMessage** property as part of the debug query parameters, it's included in the alert message.</span></span> <span data-ttu-id="d2e88-197">Вы можете настроить ваш экземпляр расширения на основе свойств компонента клиента, которые передаются для экземпляра в режиме среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="d2e88-197">This alert is thrown by your SharePoint Framework Extension. Note that because you provided the testMessage property as part of the debug query parameters, it's included in the alert message. You can configure your extension instances based on the client component properties, which are passed for the instance also in runtime mode.</span></span>

> <span data-ttu-id="d2e88-p124">**Примечание.** Если у вас возникли проблемы с отладкой, проверьте используемые параметры запроса URL-адреса. Некоторые браузеры кодируют параметры, что иногда влияет на поведение запросов.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p124">**Note:** If you have issues with debugging, double-check the URL query parameters used for the query. Some browsers encode the parameters and in some scenarios this affects the behavior.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2e88-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2e88-200">Next steps</span></span>
<span data-ttu-id="d2e88-p125">Поздравляем с успешным запуском вашего первого расширения SharePoint Framework! Чтобы продолжить его создание, ознакомьтесь со следующей статьей — [Использование заполнителей страниц в настройщике приложений (Hello World, часть 2)](./using-page-placeholder-with-extensions.md). Вы будете использовать тот же проект и воспользуетесь определенными заполнителями содержимого, чтобы изменить пользовательский интерфейс SharePoint. Обратите внимание, что команда ```gulp serve``` по-прежнему выполняется в окне консоли (или в Visual Studio Code, если вы используете редактор). Вы можете оставить ее, переходя к следующей статье.</span><span class="sxs-lookup"><span data-stu-id="d2e88-p125">Congratulations, you've gotten your first SharePoint Framework Extension running! To continue building out your extension, see [Using page placeholders from Application Customizer (Hello World part 2)](./using-page-placeholder-with-extensions.md). You will use the same project and take advantage of specific content placeholders for modifying the UI of SharePoint. Notice that the ```gulp serve``` command is still running in your console window (or in Visual Studio Code if you are using the editor). You can continue to let it run while you go to the next article.</span></span>
