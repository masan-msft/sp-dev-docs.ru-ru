---
title: "Отладка решений SharePoint Framework в Visual Studio Code"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: dc0e94994a910be9904a37d3d60bb4b9380a4b92
ms.sourcegitcommit: 2bf3ef24357127fd92fbc1f89d34b11cc9787553
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/01/2017
---
# <a name="debug-sharepoint-framework-solutions-in-visual-studio-code"></a><span data-ttu-id="ace16-102">Отладка решений SharePoint Framework в Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ace16-102">Debug SharePoint Framework solutions in Visual Studio Code</span></span>

<span data-ttu-id="ace16-p101">Visual Studio Code — это популярный редактор кода, часто используемый для создания решений SharePoint Framework. Настроив отладку решения SharePoint Framework в Visual Studio Code, вы можете эффективнее пошагово выполнять код и исправлять ошибки. В этой статье описываются необходимые условия и действия по настройке Visual Studio Code для отладки решений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="ace16-p101">Visual Studio Code is a popular code editor frequently used for building SharePoint Framework solutions. By setting up debugging of your SharePoint Framework solution in Visual Studio Code, you can more efficiently step through your code and fix errors. This article describes the prerequisites and configuration steps required to configure Visual Studio Code for debugging SharePoint Framework solutions.</span></span>

<span data-ttu-id="ace16-106">Шаги по включению отладки в Visual Studio Code также приведены в видео [на канале SharePoint PnP на YouTube](https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG).</span><span class="sxs-lookup"><span data-stu-id="ace16-106">You can also see the required steps to enable debugging in Visaul Studio Code by watching a video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG).</span></span> 

<a href="https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/spfx-debug-youtube.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="prerequisites"></a><span data-ttu-id="ace16-107">Обязательные условия</span><span class="sxs-lookup"><span data-stu-id="ace16-107">Prerequisites</span></span>

<span data-ttu-id="ace16-108">Настроить Visual Studio Code для отладки решений SharePoint Framework проще всего с помощью Google Chrome и расширения Debugger for Chrome.</span><span class="sxs-lookup"><span data-stu-id="ace16-108">The easiest way to configure Visual Studio Code to debug SharePoint Framework solutions is by using Google Chrome and the Debugger for Chrome Visual Studio Code extension.</span></span> <span data-ttu-id="ace16-109">Начиная с генератора yeoman для SharePoint Framework версии 1.3.4, шаблоны проекта (веб-частей и расширений) по умолчанию будут поставляться с предварительно установленными требуемыми компонентами и будут требовать установку необходимых расширений Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ace16-109">Starting with the SharePoint Framework yeoman generator version 1.3.4, the default project (web parts and extensions) templates will come setup with the pre-requisites and will prompt for the required Visual Studio Code extensions to install.</span></span> <span data-ttu-id="ace16-110">В этом случае вам будет предложено установить отладчик для расширения Visual Studio Code для Chrome.</span><span class="sxs-lookup"><span data-stu-id="ace16-110">In this case, it will prompt to install Debugger for Chrome Visual Studio Code extension.</span></span>

<span data-ttu-id="ace16-111">Вам также понадобится браузер Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="ace16-111">You will also need Google Chrome browser.</span></span> <span data-ttu-id="ace16-112">Скачайте и установите последнюю версию Google Chrome со страницы [https://www.google.com/chrome/browser/desktop/index.html](https://www.google.com/chrome/browser/desktop/index.html).</span><span class="sxs-lookup"><span data-stu-id="ace16-112">Download and install the latest version of Google Chrome from [https://www.google.com/chrome/browser/desktop/index.html](https://www.google.com/chrome/browser/desktop/index.html).</span></span>

<span data-ttu-id="ace16-113">Если вы используете генератор yeoman для SharePoint Framework версии раньше за 1.3.4, то вы можете установить расширение отладчика для Chrome для Visual Studio Code из [магазина Visual Studio](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome).</span><span class="sxs-lookup"><span data-stu-id="ace16-113">If you are using an older SharePoint Framework yeoman generator, older than 1.3.4, then you can install the Chrome debugger extension for Visual Studio Code from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome).</span></span>

## <a name="debug-configurations"></a><span data-ttu-id="ace16-114">Конфигурации отладки</span><span class="sxs-lookup"><span data-stu-id="ace16-114">Debug configurations</span></span>

<span data-ttu-id="ace16-115">Конфигурация отладки находится в файле launch.json в папке рабочей области Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="ace16-115">You can locate the debug configurations in the launch.json file under the Visua Studio Code workspace folder:</span></span>

```
project-name\.vscode
```

<span data-ttu-id="ace16-116">Launch.json содержит две конфигурации отладки:</span><span class="sxs-lookup"><span data-stu-id="ace16-116">The launch.json contains two debug configurations:</span></span>
* <span data-ttu-id="ace16-117">Конфигурация локальной рабочей области</span><span class="sxs-lookup"><span data-stu-id="ace16-117">Local workbench configuration</span></span>
* <span data-ttu-id="ace16-118">Конфигурация размещенной рабочей области</span><span class="sxs-lookup"><span data-stu-id="ace16-118">Hosted workbench configuration</span></span>

## <a name="debug-sharepoint-framework-solution-using-local-workbench"></a><span data-ttu-id="ace16-119">Отладка решения SharePoint Framework с помощью локальной рабочей области</span><span class="sxs-lookup"><span data-stu-id="ace16-119">Debug SharePoint Framework solution using local workbench</span></span>

<span data-ttu-id="ace16-p104">Вы можете использовать локальную рабочую область, чтобы проверить, корректно ли работает веб-часть. Локальная рабочая область хорошо подходит для тестирования всех сценариев, не требующих связи с SharePoint, а также для автономной разработки.</span><span class="sxs-lookup"><span data-stu-id="ace16-p104">When building SharePoint Framework solutions, you can use the local workbench to verify that your web part is working correctly. Using local workbench is convenient for testing all scenarios that do not require communicating with SharePoint as well as for offline development.</span></span>

<span data-ttu-id="ace16-122">Настроив Visual Studio Code для отладки решений SharePoint Framework с помощью Google Chrome и локальной рабочей области, вы можете проверить, корректно ли все работает.</span><span class="sxs-lookup"><span data-stu-id="ace16-122">With Visual Studio Code configured for debugging SharePoint Framework solutions using Google Chrome and the local workbench, you can verify that everything is working as expected.</span></span>

### <a name="configure-a-breakpoint"></a><span data-ttu-id="ace16-123">Настройка точки останова</span><span class="sxs-lookup"><span data-stu-id="ace16-123">Configure a breakpoint</span></span>

<span data-ttu-id="ace16-124">В Visual Studio Code откройте основной исходный файл веб-части и добавьте точку останова на первой строке метода **render**. Для этого щелкните слева от номера строки или выделите строку кода в редакторе и нажмите клавишу **F9**.</span><span class="sxs-lookup"><span data-stu-id="ace16-124">In Visual Studio Code open the main web part source file and add a breakpoint in the first line of the **render** method by either clicking on the margin left to the line number or by highlighting the code line in the editor and pressing the **F9** key.</span></span>

![Точка останова в клиентской веб-части SharePoint Framework в Visual Studio Code](../images/vscode-debugging-breakpoint-configured.png)

<span data-ttu-id="ace16-126">В Visual Studio Code откройте меню **Вид** и выберите пункт **Интегрированный терминал** или нажмите клавиши **CTRL+\`**.</span><span class="sxs-lookup"><span data-stu-id="ace16-126">In Visual Studio Code, from the **View** menu select the **Integrated Terminal** option or press **CTRL+\`** on the keyboard. In the terminal run the following command:</span></span> <span data-ttu-id="ace16-127">В терминале выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ace16-127">From the terminal, run the following command:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="ace16-128">При этом будет выполнена сборка решения SharePoint Framework и запустится локальный веб-сервер для предоставления выходных файлов.</span><span class="sxs-lookup"><span data-stu-id="ace16-128">Running this command will build your SharePoint Framework solution and start the local webserver to serve the output files. Because the debugger will start its own instance of the browser, you use the --nobrowser argument to prevent the serve task from opening a browser window.</span></span> <span data-ttu-id="ace16-129">Так как отладчик запустит собственный экземпляр браузера, мы используем аргумент **--nobrowser**, чтобы задача **serve** не открывала окно браузера.</span><span class="sxs-lookup"><span data-stu-id="ace16-129">Running this command will build your SharePoint Framework solution and start the local webserver to serve the output files. Because the debugger will start its own instance of the browser, you use the **--nobrowser** argument to prevent the **serve** task from opening a browser window.</span></span>

![Команда gulp serve в интегрированном терминале Visual Studio Code](../images/vscode-debugging-gulp-serve.png)

### <a name="start-debugging-in-visual-studio-code"></a><span data-ttu-id="ace16-131">Начало отладки с помощью Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ace16-131">Start debugging in Visual Studio Code</span></span>

<span data-ttu-id="ace16-132">Когда задача gulp будет выполнена, переместите фокус в область кода Visual Studio Code и нажмите клавишу **F5** (или выберите в меню **Отладка** пункт **Запустить отладку**).</span><span class="sxs-lookup"><span data-stu-id="ace16-132">Once the gulp task is finished, move the focus to the code area of Visual Studio Code and press **F5** (or from the **Debug** menu select the **Start Debugging** option). The debug mode in Visual Studio Code will start, changing the color of the status bar to orange and a new window of Google Chrome will open showing the local version of the SharePoint workbench.</span></span> <span data-ttu-id="ace16-133">Будет запущен режим отладки Visual Studio Code: цвет строки состояния изменится на оранжевый, и откроется новое окно Google Chrome с локальной версией рабочей области SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ace16-133">Once the gulp task is finished, move the focus to the code area of Visual Studio Code and press F5 (or from the Debug menu select the Start Debugging option). The debug mode in Visual Studio Code will start, changing the color of the status bar to orange and a new window of Google Chrome will open showing the local version of the SharePoint workbench.</span></span>

![Visual Studio Code в режиме отладки рядом с браузером Google Chrome, в котором отображается локальная версия рабочей области SharePoint](../images/vscode-debugging-chrome-started.png)

> <span data-ttu-id="ace16-p108">Обратите внимание, что в этот момент точка останова отключена, так как код веб-части еще не загружен. SharePoint Framework загружает веб-части по запросу только после их добавления на страницу.</span><span class="sxs-lookup"><span data-stu-id="ace16-p108">Note, that at this point the breakpoint is disabled, because the web part's code hasn't been loaded yet. SharePoint Framework loads web parts on demand only after they have been added to the page.</span></span>

### <a name="add-web-part-to-canvas"></a><span data-ttu-id="ace16-137">Добавление веб-части на холст</span><span class="sxs-lookup"><span data-stu-id="ace16-137">Add web part to canvas</span></span>

<span data-ttu-id="ace16-138">Чтобы убедиться, что отладка работает, добавьте веб-часть на холст в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="ace16-138">To verify that debugging is working, in the workbench add your web part to the canvas.</span></span>

![Панель элементов веб-части в рабочей области SharePoint](../images/vscode-debugging-adding-web-part-to-canvas.png)

<span data-ttu-id="ace16-140">Обратите внимание, что после загрузки кода на страницу индикатор точки останова изменился на активный.</span><span class="sxs-lookup"><span data-stu-id="ace16-140">Notice, that with the code loaded on the page, the breakpoint indicator changed to active.</span></span>

![Активная точка останова после добавления веб-части на холст](../images/vscode-debugging-breakpoint-active.png)

<span data-ttu-id="ace16-142">Если теперь обновить страницу, в Visual Studio Code будет достигнута точка останова, и вы сможете проверить все свойства и пошагово выполнить код.</span><span class="sxs-lookup"><span data-stu-id="ace16-142">If you now reload the page, your breakpoint in Visual Studio Code will be hit, and you will be able to inspect all properties and step through the code.</span></span>

![Достигнутая точка останова в Visual Studio Code](../images/vscode-debugging-breakpoint-hit.png)

## <a name="debug-sharepoint-framework-solution-using-hosted-workbench"></a><span data-ttu-id="ace16-144">Отладка решения SharePoint Framework с помощью размещенной рабочей области</span><span class="sxs-lookup"><span data-stu-id="ace16-144">Debug SharePoint Framework solution using hosted workbench</span></span>

<span data-ttu-id="ace16-145">Чтобы проверить взаимодействие решения с SharePoint,</span><span class="sxs-lookup"><span data-stu-id="ace16-145">When building SharePoint Framework solutions that communicate with SharePoint you might want to verify the interaction between your solution in SharePoint.</span></span> <span data-ttu-id="ace16-146">можно использовать размещенную версию рабочей области SharePoint, доступную в каждом клиенте Office 365 по адресу **https://yourtenant.sharepoint.com/_layouts/workbench.aspx**.</span><span class="sxs-lookup"><span data-stu-id="ace16-146">To do this easily, you can use the hosted version of the SharePoint workbench which is available on every Office 365 tenant at **https://yourtenant.sharepoint.com/_layouts/workbench.aspx**.</span></span> <span data-ttu-id="ace16-147">При создании решений SharePoint Framework вы будете регулярно выполнять такие проверки, поэтому рекомендуем создать отдельную конфигурацию отладки для размещенной версии рабочей области SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ace16-147">When building SharePoint Framework solutions, you will be doing such tests regularly and it is a good idea to create a separate debug configuration for the hosted version of the SharePoint workbench.</span></span>

<span data-ttu-id="ace16-148">Откройте launch.json и измените свойство *url* в конфигурации *размещенной рабочей области* на URL-адрес вашего сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ace16-148">Open launch.json and update the *url* property under *Hosted workbench* configuration to your SharePoint site URL.</span></span>

```json
"url": "https://enter-your-SharePoint-site/_layouts/workbench.aspx",
```
<span data-ttu-id="ace16-149">В Visual Studio Code откройте панель **Отладка** и в раскрывающемся списке **Конфигурации** выберите новую конфигурацию **Размещенная рабочая область**.</span><span class="sxs-lookup"><span data-stu-id="ace16-149">With the debug configuration for the hosted workbench ready, verify that it's working correctly. In Visual Studio Code, activate the **Debug** pane and in the **Configurations** drop-down, select the newly added **Hosted workbench** configuration.</span></span>

![Конфигурация Hosted workbench, выбранная в раскрывающемся списке конфигураций отладки в Visual Studio Code](../images/vscode-debugging-debugging-hosted-workbench.png)

<span data-ttu-id="ace16-151">Затем запустите отладку. Для этого нажмите клавишу **F5** или выберите в меню **Отладка** пункт **Запустить отладку**.</span><span class="sxs-lookup"><span data-stu-id="ace16-151">Next, start debugging either by pressing the **F5** key or by selecting from the **Debug** menu the **Start Debugging** option.</span></span> <span data-ttu-id="ace16-152">Visual Studio Code переключится в режим отладки (это будет видно по оранжевой строке состояния), а расширение Debugger for Chrome откроет новое окно Google Chrome со страницей входа в Office 365.</span><span class="sxs-lookup"><span data-stu-id="ace16-152">Next, start debugging either by pressing the F5 key or by selecting from the Debug menu the Start Debugging option. Visual Studio Code will switch into debug mode, indicated by the orange status bar, and the Debugger for Chrome extension will open a new instance of Google Chrome with the Office 365 login page.</span></span>

![Страница входа в Office 365, открытая в Google Chrome после запуска отладки в размещенной рабочей области](../images/vscode-debugging-o365-login.png)

<span data-ttu-id="ace16-154">После входа добавьте веб-часть на холст и обновите рабочую область. Как и в случае с локальной рабочей областью, в Visual Studio Code будет достигнута точка останова, и сможете проверить переменные и пошагово выполнить код.</span><span class="sxs-lookup"><span data-stu-id="ace16-154">After you log in, add the web part to the canvas and refresh the workbench, just like with the local workbench, you will see the breakpoint in Visual Studio Code be hit and you will be able to inspect variables and step through the code.</span></span>

![Достигнута точка останова в Visual Studio Code при отладке клиентской веб-части SharePoint Framework в размещенной рабочей области](../images/vscode-debugging-breakpoint-hit-o365.png)

## <a name="for-older-projects"></a><span data-ttu-id="ace16-156">Для более ранних проектов</span><span class="sxs-lookup"><span data-stu-id="ace16-156">For older projects</span></span>
<span data-ttu-id="ace16-157">Если вы используете более раннюю версию генератора yeoman для SharePoint Framework, следуйте инструкциям ниже, чтобы создать файл launch.json вручную.</span><span class="sxs-lookup"><span data-stu-id="ace16-157">If you are using an older version of SharePoint Framework yeoman generator, then follow the steps below to create the launch.json file manually.</span></span>

### <a name="create-debug-configuration-for-local-workbench"></a><span data-ttu-id="ace16-158">Создание конфигурации отладки для локальной рабочей области</span><span class="sxs-lookup"><span data-stu-id="ace16-158">Create debug configuration for local workbench</span></span>

<span data-ttu-id="ace16-159">Откройте в Visual Studio Code панель **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="ace16-159">In Visual Studio Code activate the **Debug** pane.</span></span>

![Панель отладки в Visual Studio Code](../images/vscode-debugging-vscode-debug.png)

<span data-ttu-id="ace16-161">В верхней части панели откройте раскрывающийся список **Конфигурации** и выберите пункт **Добавить конфигурацию...**</span><span class="sxs-lookup"><span data-stu-id="ace16-161">In the top section of the pane, open the **Configurations** drop-down and select the **Add Configuration...** option.</span></span>

![Пункт "Добавить конфигурацию" в раскрывающемся списке конфигураций отладки](../images/vscode-debugging-add-debug-configuration.png)

<span data-ttu-id="ace16-163">Выберите **Chrome** в списке сред отладки.</span><span class="sxs-lookup"><span data-stu-id="ace16-163">From the list of debug environments select **Chrome**.</span></span>

![Браузер Chrome выбран в качестве среды отладки для новой конфигурации](../images/vscode-debugging-chrome-debug-environment.png)

<span data-ttu-id="ace16-165">Замените содержимое созданного файла **launch.json** на следующее:</span><span class="sxs-lookup"><span data-stu-id="ace16-165">Replace the contents of the generated **launch.json** file with:</span></span>

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Local workbench",
            "type": "chrome",
            "request": "launch",
            "url": "https://localhost:4321/temp/workbench.html",
            "webRoot": "${workspaceRoot}",
            "sourceMaps": true,
            "sourceMapPathOverrides": {
                "webpack:///../../../src/*": "${webRoot}/src/*",
                "webpack:///../../../../src/*": "${webRoot}/src/*",
                "webpack:///../../../../../src/*": "${webRoot}/src/*"
            },
            "runtimeArgs": [
                "--remote-debugging-port=9222"
            ]
        }
    ]
}
```

<span data-ttu-id="ace16-166">В этой конфигурации используется отладчик **chrome**, входящий в состав расширения **Debugger for Chrome**.</span><span class="sxs-lookup"><span data-stu-id="ace16-166">This configuration uses the **chrome** debugger provided with the **Debugger for Chrome** extension.</span></span> <span data-ttu-id="ace16-167">Он указывает на URL-адрес локальной рабочей области в качестве отправной точки.</span><span class="sxs-lookup"><span data-stu-id="ace16-167">It points to the URL of the local workbench as the starting point.</span></span> <span data-ttu-id="ace16-168">При отладке кода TypeScript важна конфигурация, с помощью которой отладчик сопоставляет код JavaScript, выполняемый в браузере, с исходным кодом TypeScript.</span><span class="sxs-lookup"><span data-stu-id="ace16-168">This configuration uses the chrome debugger provided with the Debugger for Chrome extension. It points to the URL of the local workbench as the starting point. What is essential in debugging TypeScript code, is the configuration of source maps that the debugger uses to map the JavaScript running in the browser to the original TypeScript code.</span></span>

### <a name="create-debug-configuration-for-hosted-workbench"></a><span data-ttu-id="ace16-169">Создание конфигурации отладки для размещенной рабочей области</span><span class="sxs-lookup"><span data-stu-id="ace16-169">Create debug configuration for hosted workbench</span></span>

<span data-ttu-id="ace16-170">В Visual Studio Code откройте файл **./.vscode/launch.json**.</span><span class="sxs-lookup"><span data-stu-id="ace16-170">In Visual Studio Code, open the file config\config.json.</span></span> <span data-ttu-id="ace16-171">Скопируйте имеющуюся конфигурацию отладки и укажите URL-адрес размещенной рабочей области:</span><span class="sxs-lookup"><span data-stu-id="ace16-171">In Visual Studio Code open the ./.vscode/launch.json file. Copy the existing debug configuration and use the URL of the hosted workbench:</span></span>

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Local workbench",
            "type": "chrome",
            "request": "launch",
            "url": "https://localhost:4321/temp/workbench.html",
            "webRoot": "${workspaceRoot}",
            "sourceMaps": true,
            "sourceMapPathOverrides": {
                "webpack:///../../../src/*": "${webRoot}/src/*",
                "webpack:///../../../../src/*": "${webRoot}/src/*",
                "webpack:///../../../../../src/*": "${webRoot}/src/*"
            },
            "runtimeArgs": [
                "--remote-debugging-port=9222"
            ]
        },
        {
            "name": "Hosted workbench",
            "type": "chrome",
            "request": "launch",
            "url": "https://contoso.sharepoint.com/_layouts/workbench.aspx",
            "webRoot": "${workspaceRoot}",
            "sourceMaps": true,
            "sourceMapPathOverrides": {
                "webpack:///../../../src/*": "${webRoot}/src/*",
                "webpack:///../../../../src/*": "${webRoot}/src/*",
                "webpack:///../../../../../src/*": "${webRoot}/src/*"
            },
            "runtimeArgs": [
                "--remote-debugging-port=9222"
            ]
        }
    ]
}
```

## <a name="additional-information"></a><span data-ttu-id="ace16-172">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="ace16-172">Additional information</span></span>

- [<span data-ttu-id="ace16-173">Отладка веб-части SharePoint Framework (Элио Струйф)</span><span class="sxs-lookup"><span data-stu-id="ace16-173">How to debug your SharePoint Framework web part (Elio Struyf)</span></span>](http://www.eliostruyf.com/how-to-debug-your-sharepoint-framework-web-part/)
- [<span data-ttu-id="ace16-174">Отладка веб-части SPFx React с помощью Visual Studio Code (Велин Георгиев)</span><span class="sxs-lookup"><span data-stu-id="ace16-174">Debug SPFx React webpart with Visual Studio Code (Velin Georgiev)</span></span>](http://blog.velingeorgiev.pro/how-debug-sharepoint-framework-webpart-visual-studio-code)
