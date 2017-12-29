---
title: "Создание первой клиентской веб-части SharePoint (Hello World, часть 1)"
ms.date: 12/05/2017
ms.prod: sharepoint
ms.openlocfilehash: 9a5fefeb0e5dac79958534dd4819a905ff608635
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="build-your-first-sharepoint-client-side-web-part-hello-world-part-1"></a><span data-ttu-id="4c973-102">Создание первой клиентской веб-части SharePoint (Hello World, часть 1)</span><span class="sxs-lookup"><span data-stu-id="4c973-102">Build your first SharePoint client-side web part (Hello World part 1)</span></span>

<span data-ttu-id="4c973-p101">Клиентские веб-части — это клиентские компоненты, которые запускаются в контексте страницы SharePoint. Клиентские веб-части можно развертывать в SharePoint Online, а для их создания также можно использовать современные инструменты и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4c973-p101">Client-side web parts are client-side components that run inside the context of a SharePoint page. Client-side web parts can be deployed to SharePoint Online, and you can also use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="4c973-105">Поддержка клиентских веб-частей:</span><span class="sxs-lookup"><span data-stu-id="4c973-105">Client-side web parts support:</span></span>

* <span data-ttu-id="4c973-106">Создание при помощи HTML и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4c973-106">Building with HTML and JavaScript.</span></span>
* <span data-ttu-id="4c973-107">Как SharePoint Online, так и локальные среды.</span><span class="sxs-lookup"><span data-stu-id="4c973-107">Both SharePoint online and on-premises environments.</span></span>

> [!NOTE]
> <span data-ttu-id="4c973-108">Прежде чем выполнять действия, описанные в этой статье, обязательно [настройте среду разработки](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="4c973-108">Before following the steps in this article, be sure to [Set up your development environment](../../set-up-your-development-environment.md).</span></span>

<span data-ttu-id="4c973-109">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=YqUIX2pMUzg&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=2).</span><span class="sxs-lookup"><span data-stu-id="4c973-109">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=YqUIX2pMUzg&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=2).</span></span> 

<a href="https://www.youtube.com/watch?v=YqUIX2pMUzg&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=2">
<img src="../../../images/spfx-youtube-tutorial1.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a><span data-ttu-id="4c973-110">Создание проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-110">Create a new web part project</span></span>
<span data-ttu-id="4c973-111">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="4c973-111">Create a new project directory in your favorite location.</span></span>
    
```
md helloworld-webpart
```

<span data-ttu-id="4c973-112">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="4c973-112">Go to the project directory.</span></span>

```
cd helloworld-webpart
```

<span data-ttu-id="4c973-113">Создайте веб-часть HelloWorld, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c973-113">Create a new HelloWorld web part by running the Yeoman SharePoint Generator.</span></span>

```
yo @microsoft/sharepoint
```
    
<span data-ttu-id="4c973-114">Когда появится запрос:</span><span class="sxs-lookup"><span data-stu-id="4c973-114">When prompted:</span></span>

* <span data-ttu-id="4c973-115">Оставьте имя по умолчанию (**helloworld-webpart**) для своего решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c973-115">Accept the default **helloworld-webpart** as your solution name and choose **Enter**.</span></span>
* <span data-ttu-id="4c973-116">Выберите **Только SharePoint Online (новая версия)** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c973-116">Choose **SharePoint Online only (latest)**, and press **Enter**.</span></span>
* <span data-ttu-id="4c973-117">Выберите вариант **Использовать текущую папку** для размещения файлов.</span><span class="sxs-lookup"><span data-stu-id="4c973-117">Select **Use the current folder** for where to place the files.</span></span>
* <span data-ttu-id="4c973-118">Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="4c973-118">Choose **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
* <span data-ttu-id="4c973-119">Выберите **WebPart** в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="4c973-119">Choose **WebPart** as the client-side component type to be created.</span></span> 

<span data-ttu-id="4c973-120">Далее вам потребуется указать определенные сведения о веб-части:</span><span class="sxs-lookup"><span data-stu-id="4c973-120">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="4c973-121">Оставьте имя по умолчанию (**HelloWorld**) для своей веб-части и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c973-121">Accept the default **HelloWorld** as your web part name and choose **Enter**.</span></span>
* <span data-ttu-id="4c973-122">Оставьте **описание HelloWorld** по умолчанию для своей веб-части и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c973-122">Accept the default **HelloWorld description** as your web part description and choose **Enter**.</span></span>
* <span data-ttu-id="4c973-123">Оставьте выбранным параметр **No javascript web framework** (Не использовать платформу веб-решений на базе JavaScript) по умолчанию и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4c973-123">Accept the default **No javascript web framework** as the framework you would like to use and choose **Enter**.</span></span>

![Генератор Yeoman для SharePoint предлагает создать клиентскую веб-часть](../../../images/yeoman-sp-prompts.png)

<span data-ttu-id="4c973-p102">После этого Yeoman установит необходимые зависимости и выполнит скаффолдинг файлов решения, а также веб-части **HelloWorld**. Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4c973-p102">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** web part. This might take a few minutes.</span></span>

<span data-ttu-id="4c973-127">Когда скаффолдинг успешно закончится, появится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="4c973-127">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

!["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../images/yeoman-sp-complete.png)

<span data-ttu-id="4c973-129">Сведения об устранении неполадок см. в статье [Известные проблемы](../../known-issues-and-common-questions.md).</span><span class="sxs-lookup"><span data-stu-id="4c973-129">For information about troubleshooting any errors, see [Known issues](../../known-issues-and-common-questions.md).</span></span>

### <a name="using-your-favorite-code-editor"></a><span data-ttu-id="4c973-130">Использование удобного редактора кода</span><span class="sxs-lookup"><span data-stu-id="4c973-130">Using your favorite Code Editor</span></span>
<span data-ttu-id="4c973-131">Так как клиентские решения SharePoint созданы с помощью HTML и TypeScript, для разработки веб-части можно использовать любой редактор кода, который поддерживает клиентское программирование, например:</span><span class="sxs-lookup"><span data-stu-id="4c973-131">Because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your web part, such as:</span></span>

* <span data-ttu-id="4c973-132">[Visual Studio Code](https://code.visualstudio.com/);</span><span class="sxs-lookup"><span data-stu-id="4c973-132">[Visual Studio Code](https://code.visualstudio.com/)</span></span>
* <span data-ttu-id="4c973-133">[Atom](https://atom.io);</span><span class="sxs-lookup"><span data-stu-id="4c973-133">[Atom](https://atom.io)</span></span>
* <span data-ttu-id="4c973-134">[Webstorm](https://www.jetbrains.com/webstorm).</span><span class="sxs-lookup"><span data-stu-id="4c973-134">[Webstorm](https://www.jetbrains.com/webstorm)</span></span>

<span data-ttu-id="4c973-135">В примерах и инструкциях, приведенных в документации по SharePoint Framework, указывается Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4c973-135">SharePoint Framework documentation uses Visual Studio code in the steps and examples.</span></span> <span data-ttu-id="4c973-136">Visual Studio Code — мощный редактор исходного кода, предложенный корпорацией Майкрософт, который занимает мало места на диске и работает на компьютерах с Windows, Mac OS или Linux.</span><span class="sxs-lookup"><span data-stu-id="4c973-136">Visual Studio Code is a lightweight but powerful source code editor from Microsoft which runs on your desktop and is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="4c973-137">Он изначально поддерживает JavaScript, TypeScript и Node.js, а также предусматривает использование богатой экосистемы расширений для других языков (например, C++, C#, Python, PHP) и сред выполнения.</span><span class="sxs-lookup"><span data-stu-id="4c973-137">It comes with built-in support for JavaScript, TypeScript and Node.js and has a rich ecosystem of extensions for other languages (such as C++, C#, Python, PHP) and runtimes.</span></span>
   
## <a name="preview-the-web-part"></a><span data-ttu-id="4c973-138">Просмотр веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-138">Preview the web part</span></span>
<span data-ttu-id="4c973-p104">Чтобы просмотреть веб-часть, выполните сборку и запустите ее на локальном веб-сервере. В клиентской цепочке инструментов по умолчанию используется конечная точка HTTPS. Но так как сертификат по умолчанию не настроен для локальной среды разработки, браузер сообщит об ошибке сертификата. Цепочка инструментов SPFx включает сертификат разработчика, который можно установить для создания веб-частей.</span><span class="sxs-lookup"><span data-stu-id="4c973-p104">To preview your web part, build and run it on a local web server. The client-side toolchain uses HTTPS endpoint by default. However, since a default certificate is not configured for the local dev environment, your browser will report a certificate error. The SPFx toolchain comes with a developer certificate that you can install for building web parts.</span></span>

<span data-ttu-id="4c973-143">Чтобы установить сертификат разработчика для использования SPFx, перейдите в консоль, откройте каталог **helloworld-webpart** и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4c973-143">To install the developer certificate for use with SPFx development, switch to your console, make sure you are still in the **helloworld-webpart** directory and enter the following command:</span></span>

```
gulp trust-dev-cert
```

<span data-ttu-id="4c973-144">Теперь, когда вы установили сертификат разработчика, введите в консоли следующую команду для сборки и просмотра веб-части:</span><span class="sxs-lookup"><span data-stu-id="4c973-144">Now that we have installed the developer certificate, enter the following command in the console to build and preview your web part:</span></span>

```
gulp serve
```

<span data-ttu-id="4c973-145">Эта команда выполнит ряд задач Gulp, чтобы создать локальный HTTPS-сервер на основе Node по адресу localhost:4321, и запустит браузер по умолчанию для просмотра веб-частей в локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="4c973-145">This command will execute a series of gulp tasks to create a local, Node-based HTTPS server on 'localhost:4321' and launch your default browser to preview web parts from your local dev environment.</span></span>

![Проект веб-части gulp serve](../../../images/helloworld-wp-gulp-serve.png)

<span data-ttu-id="4c973-147">Инструменты клиентской разработки SharePoint используют [Gulp](http://gulpjs.com/) как средство запуска задач для таких задач по сборке, как:</span><span class="sxs-lookup"><span data-stu-id="4c973-147">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the task runner to handle build process tasks such as:</span></span>

* <span data-ttu-id="4c973-148">добавление в пакет и минификация файлов JavaScript и CSS;</span><span class="sxs-lookup"><span data-stu-id="4c973-148">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="4c973-149">запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;</span><span class="sxs-lookup"><span data-stu-id="4c973-149">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="4c973-150">компиляция файлов SASS в CSS;</span><span class="sxs-lookup"><span data-stu-id="4c973-150">Compile SASS files to CSS.</span></span>
* <span data-ttu-id="4c973-151">компиляция файлов TypeScript в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4c973-151">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="4c973-p105">Visual Studio Code поддерживает Gulp и другие средства запуска задач. Нажмите клавиши **CTRL+SHIFT+B** в Windows или **CMD+SHIFT+B** в Mac OS для отладки и просмотра веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c973-p105">Visual Studio Code provides built-in support for gulp and other task runners. Choose **Ctrl+Shift+B** on Windows or **Cmd+Shift+B** on Mac to debug and preview your web part.</span></span> 

### <a name="sharepoint-workbench"></a><span data-ttu-id="4c973-154">SharePoint Workbench</span><span class="sxs-lookup"><span data-stu-id="4c973-154">SharePoint Workbench</span></span>
<span data-ttu-id="4c973-p106">SharePoint Workbench — это рабочая область конструирования для разработчиков, которая позволяет быстро просматривать и проверять веб-части, не развертывая их в SharePoint. SharePoint Workbench включает клиентскую страницу и клиентский холст, на которых можно добавлять, удалять и проверять веб-части, которые находятся в разработке.</span><span class="sxs-lookup"><span data-stu-id="4c973-p106">SharePoint Workbench is a developer design surface that enables you to quickly preview and test web parts without deploying them in SharePoint. SharePoint Workbench includes the client-side page and the client-side canvas in which you can add, delete and test your web parts in development.</span></span>

![Рабочая область SharePoint Workbench, запущенная локально](../../../images/sp-workbench.png)

<span data-ttu-id="4c973-p107">Чтобы добавить веб-часть HelloWorld, нажмите кнопку **Добавить**. Эта кнопка открывает панель элементов со списком веб-частей, которые можно добавить. Список будет включать веб-часть **HelloWorld**, а также другие веб-части, доступные локально в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="4c973-p107">To add the HelloWorld web part, choose the **add** button. The add button opens the toolbox where you can see a list of web parts available for you to add. The list will include the **HelloWorld** web part as well other web parts available locally in your development environment.</span></span>
   
![Панель элементов SharePoint Workbench на localhost](../../../images/sp-workbench-toolbox.png)
   
<span data-ttu-id="4c973-162">Выберите пункт **HelloWorld**, чтобы добавить эту веб-часть на страницу:</span><span class="sxs-lookup"><span data-stu-id="4c973-162">Choose **HelloWorld** to add the web part to the page:</span></span>
   
![Веб-часть HelloWorld в SharePoint Workbench](../../../images/sp-workbench-helloworld-wp.png)

<span data-ttu-id="4c973-164">**Поздравляем!**</span><span class="sxs-lookup"><span data-stu-id="4c973-164">**Congratulations!**</span></span> <span data-ttu-id="4c973-165">Вы только что добавили свою первую клиентскую веб-часть на клиентскую страницу.</span><span class="sxs-lookup"><span data-stu-id="4c973-165">Congratulations! You have just added your first client-side web part to a client-side page.</span></span>
   
<span data-ttu-id="4c973-166">Теперь выберите значок карандаша в крайнем левом углу веб-части, чтобы открыть панель свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c973-166">Now, choose the pencil icon on the far left of the web part to reveal the web part property pane.</span></span>
   
![Панель свойств веб-части HelloWorld](../../../images/sp-workbench-helloworld-pp.png)

<span data-ttu-id="4c973-p109">На панели свойств можно задавать свойства для настройки веб-части. Панель свойств запускается на стороне клиента и имеет одинаковый дизайн для всех веб-частей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c973-p109">The property pane is where you can define properties to customize your web part. The property pane is client-side driven and provides a consistent design across SharePoint.</span></span>
   
<span data-ttu-id="4c973-170">Измените текст в поле **Описание** на текст **Клиентские веб-части — это великолепно!**</span><span class="sxs-lookup"><span data-stu-id="4c973-170">Modify the text in the **Description** text box to **Client-side web parts are awesome!**</span></span>

<span data-ttu-id="4c973-171">Обратите внимание, что при вводе текст в веб-части также меняется.</span><span class="sxs-lookup"><span data-stu-id="4c973-171">Notice how the text in the web part also changes as you type.</span></span> 

<span data-ttu-id="4c973-p110">Теперь вы можете настроить режим обновления для панели свойств, выбрав реактивный или нереактивный вариант. В режиме по умолчанию (реактивном) изменения становятся видны по мере редактирования свойств и сохраняются мгновенно.</span><span class="sxs-lookup"><span data-stu-id="4c973-p110">One of the new capabilities available to the property pane is to configure its update behavior, which can be set to reactive or non-reactive. By default the update behavior is reactive and enables you to see the changes as you edit the properties. The changes are saved instantly as when the behavior is reactive.</span></span>  

## <a name="web-part-project-structure"></a><span data-ttu-id="4c973-175">Структура проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-175">Web part project structure</span></span>
<span data-ttu-id="4c973-176">С помощью Visual Studio Code можно просмотреть структуру проекта веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c973-176">You can use Visual Studio Code to explore the web part project structure.</span></span> 

* <span data-ttu-id="4c973-177">Перейдите на консоль и остановите обработку, нажав клавиши CTRL+C (в Windows).</span><span class="sxs-lookup"><span data-stu-id="4c973-177">In the console, break the processing by pressing Ctrl+C (in Windows)</span></span> 
* <span data-ttu-id="4c973-178">Введите указанную ниже команду, чтобы открыть проект веб-части в Visual Studio Code (или используйте другой редактор):</span><span class="sxs-lookup"><span data-stu-id="4c973-178">Enter the following command to open the web part project in Visual Studio Code (or use your favorite editor):</span></span>

```
code .
```

![Структура проекта HelloWorld](../../../images/helloworld-wp-vscode-project-structure.png)

<span data-ttu-id="4c973-180">Если возникла ошибка, [задайте команду code в PATH](https://code.visualstudio.com/docs/editor/setup).</span><span class="sxs-lookup"><span data-stu-id="4c973-180">If you get an error, you might need to [install the code command in PATH](https://code.visualstudio.com/docs/editor/setup).</span></span>

<span data-ttu-id="4c973-p111">TypeScript — это основной язык для создания клиентских веб-частей SharePoint. TypeScript — это типизированная расширенная версия языка JavaScript. Код TypeScript компилируется в обычный JavaScript. Клиентские средства разработки SharePoint основаны на классах, модулях и интерфейсах TypeScript, что позволяет разработчикам создавать надежные клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c973-p111">TypeScript is the primary language for building SharePoint client-side web parts. TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. SharePoint client-side development tools are built using TypeScript classes, modules, and interfaces to help developers build robust client-side web parts.</span></span> 

<span data-ttu-id="4c973-184">Ниже приведены некоторые ключевые файлы в проекте.</span><span class="sxs-lookup"><span data-stu-id="4c973-184">The following are some key files in the project.</span></span>

### <a name="web-part-class"></a><span data-ttu-id="4c973-185">Класс веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-185">Web part class</span></span>
<span data-ttu-id="4c973-186">**HelloWorldWebPart.ts** в папке **src\webparts\helloworld** определяет основную точку входа для веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c973-186">**HelloWorldWebPart.ts** in **src\webparts\helloworld** folder defines the main entry point for the web part.</span></span> <span data-ttu-id="4c973-187">Класс веб-части **HelloWorldWebPart** расширяет класс **BaseClientSideWebPart**.</span><span class="sxs-lookup"><span data-stu-id="4c973-187">The web part class **HelloWorldWebPart** extends the **BaseClientSideWebPart**.</span></span> <span data-ttu-id="4c973-188">Чтобы клиентская веб-часть была допустимой, она должна расширять класс **BaseClientSideWebPart**.</span><span class="sxs-lookup"><span data-stu-id="4c973-188">Any client-side web part should extend the **BaseClientSideWebPart** class in order to be defined as a valid web part.</span></span>

<span data-ttu-id="4c973-p113">Этот класс обеспечивает минимальную функциональность, необходимую для создания веб-части. Он также предоставляет много параметров для проверки и доступа к свойствам только для чтения, например **displayMode**, другим свойствам веб-частей, контексту веб-частей, а также **instanceId** и **domElement**.</span><span class="sxs-lookup"><span data-stu-id="4c973-p113">**BaseClientSideWebPart** implements the minimal functionality that is required to build a web part. This class also provides many parameters to validate and access to read-only properties such as **displayMode**, web part properties, web part context, web part **instanceId**, the web part **domElement** and much more.</span></span>

<span data-ttu-id="4c973-191">Обратите внимание на то, что класс веб-части определяется как принимающий тип свойства **IHelloWorldWebPartProps**.</span><span class="sxs-lookup"><span data-stu-id="4c973-191">Notice that the web part class is defined to accept a property type **IHelloWorldWebPartProps**.</span></span>

<span data-ttu-id="4c973-192">Тип свойства определяется как интерфейс перед классом **HelloWorldWebPart** в файле **HelloWorldWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="4c973-192">The property type is defined as an interface before **HelloWorldWebPart** class in **HelloWorldWebPart.ts** file.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    description: string;
}
```

<span data-ttu-id="4c973-193">Это определение свойства используется для определения типов настраиваемых свойств для веб-части. Дополнительные сведения см. в разделе, посвященном области свойств, ниже.</span><span class="sxs-lookup"><span data-stu-id="4c973-193">This property definition is used to define custom property types for your web part, which is described in the property pane section later.</span></span> 

#### <a name="web-part-render-method"></a><span data-ttu-id="4c973-194">Метод отрисовки веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-194">Web part render method</span></span>
<span data-ttu-id="4c973-p114">Элемент DOM, в котором должна отрисовываться веб-часть, доступен в методе **render**. Этот метод используется для отрисовки веб-части в этом элементе DOM. В веб-части **HelloWorld** элемент DOM присвоен переменной DIV. Параметры метода включают режим отображения (чтение или редактирование) и настроенные свойства веб-части, если они есть:</span><span class="sxs-lookup"><span data-stu-id="4c973-p114">The DOM element where the web part should be rendered is available in the **render** method. This method is used to render the web part inside that DOM element. In the **HelloWorld** web part, the DOM element is set to a DIV. The method parameters include the display mode (either Read or Edit) and the configured web part properties if any:</span></span> 

```ts
  public render(): void {
    this.domElement.innerHTML = `
      <div class="${ styles.helloWorld }">
        <div class="${ styles.container }">
          <div class="${ styles.row }">
            <div class="${ styles.column }">
              <span class="${ styles.title }">Welcome to SharePoint!</span>
              <p class="${ styles.subTitle }">Customize SharePoint experiences using Web Parts.</p>
              <p class="${ styles.description }">${escape(this.properties.description)}</p>
              <a href="https://aka.ms/spfx" class="${ styles.button }">
                <span class="${ styles.label }">Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>`;
  }
```

<span data-ttu-id="4c973-199">Эта модель достаточно гибкая — в элемент DOM можно загружать веб-части, созданные на любой платформе JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4c973-199">This model is flexible enough so that web parts can be built in any JavaScript framework and loaded into the DOM element.</span></span> 

#### <a name="configure-the-web-part-property-pane"></a><span data-ttu-id="4c973-200">Настройка области свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-200">Configure the Web part property pane</span></span>
<span data-ttu-id="4c973-p115">Область свойств определяется в классе **HelloWorldWebPart**. Панель свойств нужно настраивать в свойстве **propertyPaneSettings**.</span><span class="sxs-lookup"><span data-stu-id="4c973-p115">The property pane is defined in the **HelloWorldWebPart** class. The **propertyPaneSettings** property is where you need to define the property pane.</span></span>

<span data-ttu-id="4c973-203">Когда свойства заданы, вы можете получить к ним доступ в веб-части, используя `this.properties.<property-value>`, как показано в примере с методом **render**:</span><span class="sxs-lookup"><span data-stu-id="4c973-203">When the properties are defined, you can access them in your web part using `this.properties.<property-value>`, as shown in the **render** method:</span></span>

```ts
<p class="${styles.description}">${escape(this.properties.description)}</p>
```

<span data-ttu-id="4c973-204">Обратите внимание, что мы выполняем управляющий код HTML для значения свойства, чтобы убедиться, что строка является допустимой.</span><span class="sxs-lookup"><span data-stu-id="4c973-204">Notice that we are performing a HTML escape on the property's value to ensure a valid string.</span></span>

<span data-ttu-id="4c973-205">Просмотрите статью об [интеграции панели свойств с веб-частью](../basics/integrate-with-property-pane.md), чтобы узнать больше о работе с панелью свойств и типами полей в ней.</span><span class="sxs-lookup"><span data-stu-id="4c973-205">Read the [Integrating property pane with a web part](../basics/integrate-with-property-pane.md) article to learn more about how to work with the property pane and property pane field types.</span></span>

<span data-ttu-id="4c973-p116">Давайте добавим в область свойств еще флажок, раскрывающийся список и переключатель. Для этого сначала импортируйте из платформы соответствующие поля области свойств.</span><span class="sxs-lookup"><span data-stu-id="4c973-p116">Lets now add few more properties - a checkbox, dropdown and a toggle - to the property pane. We first start by importing the respective property pane fields from the framework.</span></span>

<span data-ttu-id="4c973-208">Перейдите к верхней части файла и добавьте приведенный ниже код в раздел импорта из `@microsoft/sp-webpart-base`.</span><span class="sxs-lookup"><span data-stu-id="4c973-208">Scroll to the top of the file and add the following to the import section from `@microsoft/sp-webpart-base`:</span></span>

```ts
PropertyPaneCheckbox,
PropertyPaneDropdown,
PropertyPaneToggle
```

<span data-ttu-id="4c973-209">Полный раздел импорта будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="4c973-209">The complete import section will look like the following:</span></span>

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField,
  PropertyPaneCheckbox,
  PropertyPaneDropdown,
  PropertyPaneToggle
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="4c973-p117">Далее обновите свойства веб-части, включив новые. При этом будут сопоставлены соответствующие поля и типизированные объекты.</span><span class="sxs-lookup"><span data-stu-id="4c973-p117">Next, update the web part properties to include the new properties. This maps the fields to typed objects.</span></span>

<span data-ttu-id="4c973-212">Замените интерфейс **IHelloWorldWebPartProps** приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="4c973-212">Replace the **IHelloWorldWebPartProps** interface with the following code.</span></span>

```ts
export interface IHelloWorldWebPartProps {
    description: string;
    test: string;
    test1: boolean;
    test2: string;
    test3: boolean;
}
```

<span data-ttu-id="4c973-213">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="4c973-213">Save the file.</span></span>

<span data-ttu-id="4c973-214">Замените метод **getPropertyPaneConfiguration** приведенным ниже кодом, который добавляет новые поля области свойств и сопоставляет их с соответствующими типизированными объектами.</span><span class="sxs-lookup"><span data-stu-id="4c973-214">Replace the **getPropertyPaneConfiguration** method with the code below which adds the new property pane fields and maps them to their respective typed objects.</span></span>

```ts
protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
  return {
    pages: [
      {
        header: {
          description: strings.PropertyPaneDescription
        },
        groups: [
          {
            groupName: strings.BasicGroupName,
            groupFields: [
            PropertyPaneTextField('description', {
              label: 'Description'
            }),
            PropertyPaneTextField('test', {
              label: 'Multi-line Text Field',
              multiline: true
            }),
            PropertyPaneCheckbox('test1', {
              text: 'Checkbox'
            }),
            PropertyPaneDropdown('test2', {
              label: 'Dropdown',
              options: [
                { key: '1', text: 'One' },
                { key: '2', text: 'Two' },
                { key: '3', text: 'Three' },
                { key: '4', text: 'Four' }
              ]}),
            PropertyPaneToggle('test3', {
              label: 'Toggle',
              onText: 'On',
              offText: 'Off'
            })
          ]
          }
        ]
      }
    ]
  };
}
```


<span data-ttu-id="4c973-215">После добавления свойств веб-части к ним можно получить доступ так же, как к свойству **description**:</span><span class="sxs-lookup"><span data-stu-id="4c973-215">After you add your properties to the web part properties, you can now access the properties in the same way you accessed the **description** property earlier:</span></span>

```ts
<p class="${ styles.description }">${escape(this.properties.test)}</p>
```

<span data-ttu-id="4c973-216">Чтобы задать значение по умолчанию для этих свойств, необходимо обновить контейнер свойств **properties** манифеста веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c973-216">To set the default value for the properties, you will need to update the web part manifest's **properties** property bag:</span></span>

<span data-ttu-id="4c973-217">Откройте `HelloWorldWebPart.manifest.json` и измените `properties` так:</span><span class="sxs-lookup"><span data-stu-id="4c973-217">Open `HelloWorldWebPart.manifest.json` and modify the `properties` to:</span></span>

```ts
"properties": {
  "description": "HelloWorld",
  "test": "Multi-line text field",
  "test1": true,
  "test2": "2",
  "test3": true
}
```

<span data-ttu-id="4c973-218">Область свойств веб-части будет содержать данные значения по умолчанию для указанных свойств.</span><span class="sxs-lookup"><span data-stu-id="4c973-218">The web part property pane will now have these default values for those properties.</span></span>

### <a name="web-part-manifest"></a><span data-ttu-id="4c973-219">Манифест веб-части</span><span class="sxs-lookup"><span data-stu-id="4c973-219">Web part manifest</span></span>
<span data-ttu-id="4c973-220">Файл **HelloWorldWebPart.manifest.json** определяет метаданные веб-части, такие как версия, идентификатор, отображаемое имя, значок и описание.</span><span class="sxs-lookup"><span data-stu-id="4c973-220">The **HelloWorldWebPart.manifest.json** file defines the web part metadata such as version, id, display name, icon, and description.</span></span> <span data-ttu-id="4c973-221">Все веб-части должны содержать этот манифест.</span><span class="sxs-lookup"><span data-stu-id="4c973-221">Every web part must contain this manifest.</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "7d5437ee-afc2-4e66-914b-80be5ace4056",
  "alias": "HelloWorldWebPart",
  "componentType": "WebPart",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "preconfiguredEntries": [{
    "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
    "group": { "default": "Other" },
    "title": { "default": "HelloWorld" },
    "description": { "default": "HelloWorld description" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "HelloWorld",
      "test": "Multi-line text field",
      "test1": true,
      "test2": "2",
      "test3": true
    }
  }]
}

```

<span data-ttu-id="4c973-p119">Теперь, когда мы добавили новые свойства, опять запустите веб-часть из локальной среды разработки, выполнив приведенную ниже команду. Это также обеспечит правильное применение указанных выше изменений.</span><span class="sxs-lookup"><span data-stu-id="4c973-p119">Now that we have introduced new properties, make sure that you are again hosting the web part from the local development environment by executing following command. This will also ensure that the above changes were correctly applied.</span></span>

```
gulp serve
```

### <a name="preview-the-web-part-in-sharepoint"></a><span data-ttu-id="4c973-224">Просмотр веб-части в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c973-224">Preview the web part in SharePoint</span></span>

<span data-ttu-id="4c973-p120">В SharePoint размещается рабочая область SharePoint Workbench, чтобы вы могли просматривать и проверять локальные веб-части, которые находятся в разработке. Ее основное преимущество состоит в том, что веб-части запускаются в контексте SharePoint, и вы можете работать с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c973-p120">SharePoint Workbench is also hosted in SharePoint to preview and test your local web parts in development. The key advantage is that now you are running in SharePoint context and that you will be able to interact with SharePoint data.</span></span>

<span data-ttu-id="4c973-227">Перейдите по такому URL-адресу: "https://your-sharepoint-tenant.sharepoint.com/_layouts/workbench.aspx".</span><span class="sxs-lookup"><span data-stu-id="4c973-227">Go to the following URL: 'https://your-sharepoint-tenant.sharepoint.com/_layouts/workbench.aspx'</span></span>

> [!NOTE]
> <span data-ttu-id="4c973-228">Если у вас не установлен сертификат разработчика SPFx, рабочая область сообщит вам, что она не загружает сценарии из localhost.</span><span class="sxs-lookup"><span data-stu-id="4c973-228">If you do not have the SPFx developer certificate installed, then Workbench will notify you that it is configured not to load scripts from localhost.</span></span> <span data-ttu-id="4c973-229">Остановите процесс, выполняющийся в данный момент в окне консоли, выполните команду `gulp trust-dev-cert` в консоли каталога проекта, чтобы установить сертификат разработчика, а затем запустите команду `gulp serve` еще раз.</span><span class="sxs-lookup"><span data-stu-id="4c973-229">Stop currently running process in the console window, execute `gulp trust-dev-cert` command in your project directory console to install the developer certificate before running `gulp serve`command again.</span></span>

![Рабочая область SharePoint Workbench, запущенная на сайте SharePoint Online](../../../images/sp-workbench-o365.png)

<span data-ttu-id="4c973-231">Обратите внимание, что рабочая область SharePoint теперь включает панель навигации Office 365.</span><span class="sxs-lookup"><span data-stu-id="4c973-231">Notice that the SharePoint workbench now has the Office 365 Suite navigation bar.</span></span> 

<span data-ttu-id="4c973-p122">Выберите **значок добавления** на холсте, чтобы открыть панель элементов. В панели элементов теперь отображаются веб-части, доступные на сайте с рабочей областью SharePoint, а также веб-часть **HelloWorldWebPart**.</span><span class="sxs-lookup"><span data-stu-id="4c973-p122">Choose **add icon** in the canvas to reveal the toolbox. The toolbox now shows the web parts available on the site where the SharePoint workbench is hosted along with your **HelloWorldWebPart**.</span></span>

![Панель элементов в рабочей области SharePoint, запущенной на сайте SharePoint Online](../../../images/sp-workbench-o365-toolbox.png)

<span data-ttu-id="4c973-235">Добавьте **HelloWorld** из панели элементов.</span><span class="sxs-lookup"><span data-stu-id="4c973-235">Add **HelloWorld** from the toolbox.</span></span> <span data-ttu-id="4c973-236">Теперь ваша веб-часть работает на странице в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c973-236">Now you're running your web part in a page hosted in SharePoint!</span></span>

![Веб-часть HelloWorld в рабочей области SharePoint, запущенной на сайте SharePoint Online](../../../images/sp-workbench-o365-helloworld-wp.png)

> [!NOTE]
> <span data-ttu-id="4c973-238">Цвет веб-части зависит от цвета сайта.</span><span class="sxs-lookup"><span data-stu-id="4c973-238">Color of the web part depends on the colors of the site.</span></span> <span data-ttu-id="4c973-239">По умолчанию веб-часть наследует основные цвета с сайта, на котором она размещена, с помощью динамических ссылок на используемые там стили Office UI Fabric Core.</span><span class="sxs-lookup"><span data-stu-id="4c973-239">By default web parts will inherit the core colors from the site by dynamically referencing Office UI Fabric Core styles used in the site where web part is hosted.</span></span>

<span data-ttu-id="4c973-240">Так как ваша веб-часть по-прежнему находится на этапе разработки и тестирования, ее не нужно упаковывать и развертывать в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c973-240">Because you are still developing and testing your web part, there is no need to package and deploy your web part to SharePoint.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c973-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c973-241">Next steps</span></span>
<span data-ttu-id="4c973-242">Поздравляем с запуском вашей первой веб-части Hello World!</span><span class="sxs-lookup"><span data-stu-id="4c973-242">Congratulations on getting your first Hello World web part running!</span></span> <span data-ttu-id="4c973-243">Теперь стоит ознакомиться со статьей [Подключение к SharePoint](./connect-to-sharepoint.md). В ней описано, как</span><span class="sxs-lookup"><span data-stu-id="4c973-243">Now that your web part is running, you can continue building out your Hello World web part in the next topic, [Connect to SharePoint](./connect-to-sharepoint.md).</span></span> <span data-ttu-id="4c973-244">расширить возможности Hello World, обеспечив взаимодействие с REST API списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c973-244">You will use the same Hello World web part project and add the ability to interact with SharePoint List REST APIs.</span></span> <span data-ttu-id="4c973-245">Обратите внимание на то, что команда `gulp serve` по-прежнему запущена в окне консоли (или в Visual Studio Code, если вы используете этот редактор).</span><span class="sxs-lookup"><span data-stu-id="4c973-245">Notice that the `gulp serve` command is still running in your console window (or in Visual Studio Code if you using the editor.md).</span></span> <span data-ttu-id="4c973-246">Можете переходить к следующей статье, не останавливая ее.</span><span class="sxs-lookup"><span data-stu-id="4c973-246">You can continue to let it run while you go to the next article.</span></span>

> [!NOTE]
> <span data-ttu-id="4c973-247">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="4c973-247">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="4c973-248">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="4c973-248">Thanks for your input advance.</span></span>