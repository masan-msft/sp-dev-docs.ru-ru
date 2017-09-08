# <a name="build-your-first-listview-command-set-extension"></a><span data-ttu-id="957ec-101">Создание первого расширения с набором команд ListView</span><span class="sxs-lookup"><span data-stu-id="957ec-101">Build your first ListView Command Set extension</span></span>

><span data-ttu-id="957ec-p101">**Примечание.** Расширения для платформы SharePoint Framework находятся на этапе тестирования и могут меняться. В настоящее время расширения SharePoint Framework невозможно использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="957ec-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="957ec-p102">Расширения — это клиентские компоненты, которые запускаются в контексте страницы SharePoint. Расширения можно развертывать в SharePoint Online, а для их создания можно использовать современные инструменты и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="957ec-p102">Extensions are client-side components that run inside the context of a SharePoint page. Extensions can be deployed to SharePoint Online and you can use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="957ec-106">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=iW0LQQqAY0Y&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="957ec-106">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=iW0LQQqAY0Y&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=iW0LQQqAY0Y&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorialcommand.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="957ec-107">Создание проекта расширения</span><span class="sxs-lookup"><span data-stu-id="957ec-107">Create an extension project</span></span>
<span data-ttu-id="957ec-108">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="957ec-108">Create a new project directory in your favorite location.</span></span>

```
md command-extension
```

<span data-ttu-id="957ec-109">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="957ec-109">Go to the project directory.</span></span>

```
cd command-extension
```

<span data-ttu-id="957ec-110">Создайте расширение HelloWorld, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="957ec-110">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="957ec-111">Когда появится запрос, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="957ec-111">When prompted:</span></span>

* <span data-ttu-id="957ec-112">Оставьте значение по умолчанию (**command-extension**) для имени решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="957ec-112">Accept the default value of **command-extension** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="957ec-113">Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="957ec-113">Choose **Use the current folder** and press **Enter**.</span></span>
* <span data-ttu-id="957ec-114">Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="957ec-114">Choose **N** to require extension to be installed on each site explicitly when it's being used.</span></span> 
* <span data-ttu-id="957ec-115">Выберите для создаваемого клиентского компонента тип **Extension (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="957ec-115">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="957ec-116">Выберите для создаваемого расширения тип **ListView Command Set (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="957ec-116">Choose **ListView Command Set (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="957ec-117">Далее вам потребуется указать определенные сведения о расширении.</span><span class="sxs-lookup"><span data-stu-id="957ec-117">The next set of prompts will ask for specific information about your extension:</span></span>

* <span data-ttu-id="957ec-118">Оставьте значение по умолчанию (**HelloWorld**) для имени решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="957ec-118">Accept the default value of **HelloWorld** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="957ec-119">Оставьте значение по умолчанию (**HelloWorld description**) для описания решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="957ec-119">Accept the default value of **HelloWorld description** as your extension description and press **Enter**.</span></span>

![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../../images/ext-com-yeoman-prompts.png)

<span data-ttu-id="957ec-p103">После этого Yeoman установит необходимые зависимости и сформирует файлы решения, а также расширение **HelloWorld**. Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="957ec-p103">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** extension. This might take a few minutes.</span></span> 

<span data-ttu-id="957ec-123">После успешного скаффолдинга должно появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="957ec-123">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

!["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../../images/ext-com-yeoman-complete.png)

<span data-ttu-id="957ec-125">Сведения об устранении неполадок см. в статье [Известные проблемы](../../web-parts/basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="957ec-125">For information about troubleshooting any errors, see [Known issues](../../web-parts/basics/known-issues).</span></span>

<span data-ttu-id="957ec-126">Завершив формирование решения, введите в консоли приведенную ниже команду, чтобы запустить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="957ec-126">Once the solution scaffolding is completed, type the following into the console to start Visual Studio Code.</span></span>

```
code .
```

> <span data-ttu-id="957ec-127">Обратите внимание, что клиентское решение SharePoint создано с помощью HTML и TypeScript, поэтому для разработки расширения можно использовать любой редактор кода, который поддерживает клиентское программирование.</span><span class="sxs-lookup"><span data-stu-id="957ec-127">Notice that because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

<span data-ttu-id="957ec-p104">Обратите внимание, что стандартная структура решения аналогична структуре клиентских веб-частей. Это базовая структура решения SharePoint Framework, многие параметры которой не зависят от типа решения.</span><span class="sxs-lookup"><span data-stu-id="957ec-p104">Notice how the default solution structure is like the solution structure of client-side web parts. This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

![Решение SharePoint Framework, открытое после первоначального формирования](../../../../images/ext-com-vscode-solution-structure.png)

<span data-ttu-id="957ec-131">Откройте файл **HelloWorldCommandSet.manifest.json** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="957ec-131">Open **HelloWorldCommandSet.manifest.json** in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="957ec-p105">В этом файле определяются тип расширения и уникальный идентификатор **id** для него. Этот идентификатор потребуется позже, при отладке и развертывании расширения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="957ec-p105">This file defines your extension type and a unique identifier **“id”** for your extension. You’ll need this unique identifier later when debugging and deploying your extension to SharePoint.</span></span>

<span data-ttu-id="957ec-p106">Кроме того, обратите внимание на фактические определения команд в файле манифеста. Это кнопки, которые будут отображаться в соответствии с целью регистрации. В используемом по умолчанию шаблоне вы найдете две разные кнопки: *Command One* и *Command Two*.</span><span class="sxs-lookup"><span data-stu-id="957ec-p106">Notice also the actual command definitions in the manifest file. These are the actual buttons which will be exposed based on the registration target. In the default template, you'll find two different buttons: *"Command One"* and *"Command Two"*</span></span>

![Содержимое манифеста набора команд ListView в формате JSON](../../../../images/ext-com-vscode-manifest.png)

> <span data-ttu-id="957ec-p107">В настоящее время ссылки на изображения не работают надлежащим образом, если не обращаться к ним из абсолютных расположений сети CDN в манифесте. Это будет исправлено в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="957ec-p107">Currently, images are not properly referenced unless you are referring to them from absolute locations in a CDN within your manifest. This will be improved in future releases.</span></span>

## <a name="coding-your-listview-command-set"></a><span data-ttu-id="957ec-140">Написание кода набора команд ListView</span><span class="sxs-lookup"><span data-stu-id="957ec-140">Coding your ListView Command Set</span></span> 
<span data-ttu-id="957ec-141">Откройте файл **HelloWorldCommandSet.ts** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="957ec-141">Open the **HelloWorldCommandSet.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="957ec-142">Обратите внимание, что базовый класс для набора команд ListView импортируется из пакета **sp-listview-extensibility**, который содержит код платформы SharePoint Framework, необходимый для набора команд ListView.</span><span class="sxs-lookup"><span data-stu-id="957ec-142">Notice that the base class for the ListView Command Set is imported from the **sp-listview-extensibility** package, which contains SharePoint framework code required by the ListView Command Set.</span></span>

```ts
import { override } from '@microsoft/decorators';
import { Log } from '@microsoft/sp-core-library';
import {
  BaseListViewCommandSet,
  Command,
  IListViewCommandSetListViewUpdatedParameters,
  IListViewCommandSetExecuteEventParameters
} from '@microsoft/sp-listview-extensibility';
```

<span data-ttu-id="957ec-143">Поведение настраиваемых кнопок определяется в методах **onListViewUpdated()** и **OnExecute()**.</span><span class="sxs-lookup"><span data-stu-id="957ec-143">The behavior for your custom buttons is contained in the **onRefreshCommand()** and **OnExecute()** methods.</span></span>

<span data-ttu-id="957ec-p108">Событие **onListViewUpdated()** происходит отдельно для каждой команды (например, элемента меню), когда в ListView происходит изменение и необходимо обновить пользовательский интерфейс. Параметр `“event”` функции представляет сведения об отрисовываемой команде. Обработчик может использовать эти сведения, чтобы настроить заголовок или видимость, например если команда должна отображаться, только когда в представлении списка выбрано определенное количество элементов. Ниже представлена реализация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="957ec-p108">The **onRefreshCommand()** event occurs separately for each command (e.g. menu item), whenever the application attempts to display it in the UI. The `“event”` function parameter represents information about the command being rendered. The handler can use this information to customize the title or adjust the visibility. For example, if a command should only be shown when a certain number of items are selected in the list view. Here's the default implementation:</span></span>

<span data-ttu-id="957ec-p109">При использовании метода `“tryGetCommand”` вы получите объект Command, представляющий собой команду, отображаемую в пользовательском интерфейсе. Вы можете изменять его значения, например `“title”` или `“visible”`, для изменения элемента пользовательского интерфейса. SPFx использует эту информацию при обновлении команд. При этом сохраняется их состояние из последней прорисовки, поэтому, если для команды задано значение `“visible = false”`, она будет оставаться невидимой, пока снова не будет задано значение `“visible = true”`.</span><span class="sxs-lookup"><span data-stu-id="957ec-p109">When using the method `“tryGetCommand”` you’ll get a Command object, which is a representation of the command that shows in the UI. You can modify its values, like `“title”`, or `“visible”` in order to modify the UI element. SPFx will use this information when re-rendering the commands. These objects keep the state from the last render, so if a command is set to `“visible = false”` it will remain invisible until is set back to `“visible = true”`.</span></span>

```ts
  @override
  public onListViewUpdated(event: IListViewCommandSetListViewUpdatedParameters): void {
    if (this.properties.disabledCommandIds) {
      for (const commandId of this.properties.disabledCommandIds) {
        const command: Command | undefined = this.tryGetCommand(commandId);
        if (command && command.visible) {
          Log.info(LOG_SOURCE, `Hiding command ${commandId}`);
          command.visible = false;
        }
      }
    }
  }
```
<span data-ttu-id="957ec-p110">Метод **OnExecute()** определяет действия, совершаемые при выполнении команды (например, при выборе пункта меню). В стандартной реализации в зависимости от нажатой кнопки отображаются разные сообщения:</span><span class="sxs-lookup"><span data-stu-id="957ec-p110">The **OnExecute()** method defines what happens when a command is executed (e.g. the menu item is clicked). In the default implementation, different messages are shown based on which button was clicked:</span></span> 

```ts
  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.commandId) {
      case 'COMMAND_1':
        alert(`Clicked ${strings.Command1}`);
        break;
      case 'COMMAND_2':
        alert(`Clicked ${strings.Command2}`);
        break;
      default:
        throw new Error('Unknown command');
    }
  }
```


## <a name="debugging-your-listview-command-set-using-gulp-serve-and-query-string-parameters"></a><span data-ttu-id="957ec-155">Отладка набора команд ListView с помощью gulp serve и параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="957ec-155">Debugging your ListView Command Set using gulp serve and query string parameters</span></span>
<span data-ttu-id="957ec-p111">В настоящее время расширения SharePoint Framework невозможно тестировать с помощью локального рабочего места, поэтому тестировать и разрабатывать их следует непосредственно на активном сайте SharePoint Online. Однако при этом не требуется развертывать модификацию в каталоге приложений, что делает отладку простой и эффективной.</span><span class="sxs-lookup"><span data-stu-id="957ec-p111">SharePoint Framework extensions cannot be currently tested using the local workbench, so you'll need to test and develop them directly against a live SharePoint Online site. You do not, however, need to deploy your customization to the app catalog to do this, which keeps the debugging experience simple and efficient.</span></span> 

<span data-ttu-id="957ec-158">Для начала скомпилируйте код и разместите скомпилированные файлы с локального компьютера, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="957ec-158">First, compile your code and host the compiled files from the local machine by running this command:</span></span>
```
gulp serve --nobrowser
```

<span data-ttu-id="957ec-159">Обратите внимание, что мы использовали параметр `--nobrowser`, так как локальная отладка расширений сейчас не поддерживается, то есть нет смысла запускать локальное рабочее место.</span><span class="sxs-lookup"><span data-stu-id="957ec-159">Notice that we used the `--nobrowser` option, since there's no value in launching the local workbench since you currently cannot debug extensions locally.</span></span>

<span data-ttu-id="957ec-160">Когда компиляция кода завершится без ошибок, полученный манифест будет доступен по адресу *http://localhost:4321*.</span><span class="sxs-lookup"><span data-stu-id="957ec-160">Once it compiles the code without errors, it will serve the resulting manifest from *http://localhost:4321*.</span></span>

<span data-ttu-id="957ec-161">Перейдите к любому списку SharePoint на сайте SharePoint Online с помощью современного интерфейса.</span><span class="sxs-lookup"><span data-stu-id="957ec-161">Navigate to any SharePoint list in your SharePoint Online site using the modern experience.</span></span>

<span data-ttu-id="957ec-162">Так как наш набор команд ListView размещается из localhost и запущен, мы можем использовать определенные параметры запроса отладки для выполнения кода в представлении списка.</span><span class="sxs-lookup"><span data-stu-id="957ec-162">Since our ListView Command Set is hosted from localhost and is running, we can use specific debug query parameters to execute the code in the list view.</span></span>

<span data-ttu-id="957ec-p112">Добавьте к URL-адресу приведенные ниже параметры строки запроса. Обратите внимание, что вам потребуется обновить GUID в соответствии с идентификатором расширения с набором команд для представления списка, указанным в файле **HelloWorldCommandSet.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="957ec-p112">Append the following query string parameters to the URL. Notice that you will need to update the GUID to match the ID of your list view command set extension available in the **HelloWorldCommandSet.manifest.json** file:</span></span>

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"6a6ac29e-258e-4a2c-8de3-6bdd358cdb54":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

* <span data-ttu-id="957ec-p113">**loadSPFX=true:** гарантирует, что платформа SharePoint Framework загружается на странице. Для оптимальной производительности платформа обычно не загружается, если не зарегистрировано хотя бы одно расширение. Так как пока не зарегистрировано ни одного расширения, нам необходимо отдавать явную команду на загрузку платформы.</span><span class="sxs-lookup"><span data-stu-id="957ec-p113">**loadSPFX=true:**  ensures that the SharePoint Framework is loaded on the page. For performance reasons, the framework is not normally loaded unless at least one extension is registered. Since no components are registered yet, we must explicitly load the framework.</span></span>
* <span data-ttu-id="957ec-p114">**debugManifestsFile:** указывает, что нам требуется загрузить компоненты SPFx, предоставляемые локально. Как правило, загрузчик ищет компоненты только в каталоге приложений (для развернутого решения) и на сервере манифестов SharePoint (для системных библиотек).</span><span class="sxs-lookup"><span data-stu-id="957ec-p114">**debugManifestsFile:**  specifies that we want to load SPFx components that are being locally served. Normally the loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>
* <span data-ttu-id="957ec-p115">**customActions:** этот параметр запроса URL-адреса имитирует дополнительное действие. Для этого объекта *CustomAction* можно задать множество параметров, влияющих на внешний вид, удобство использования и расположение кнопки. Мы рассмотрим их позже.</span><span class="sxs-lookup"><span data-stu-id="957ec-p115">**customActions:**  this URL query parameter simulates a custom action. There are many properties you can set on this *CustomAction* object that affect the look, feel, and location of your button; we’ll cover them all later.</span></span>
    * <span data-ttu-id="957ec-172">**Key:** — GUID расширения.</span><span class="sxs-lookup"><span data-stu-id="957ec-172">**Key:** guid of the extension</span></span>
    * <span data-ttu-id="957ec-p116">**Location:** — расположение, в котором отображаются команды. Доступные значения:</span><span class="sxs-lookup"><span data-stu-id="957ec-p116">**Location:** where the commands are displayed. The possible values are:</span></span>
        * <span data-ttu-id="957ec-175">**ClientSideExtension.ListViewCommandSet.ContextMenu** — контекстное меню элементов;</span><span class="sxs-lookup"><span data-stu-id="957ec-175">**ClientSideExtension.ListViewCommandSet.ContextMenu:**  The context menu of the item(s)</span></span>
        * <span data-ttu-id="957ec-176">**ClientSideExtension.ListViewCommandSet.CommandBar** — меню верхнего уровня для набора команд в списке или библиотеке;</span><span class="sxs-lookup"><span data-stu-id="957ec-176">**ClientSideExtension.ListViewCommandSet.CommandBar:** The top command set menu in a list or library</span></span>
        * <span data-ttu-id="957ec-177">**ClientSideExtension.ListViewCommandSet** — контекстное меню и панель команд (соответствует параметру SPUserCustomAction.Location="CommandUI.Ribbon").</span><span class="sxs-lookup"><span data-stu-id="957ec-177">**ClientSideExtension.ListViewCommandSet:** Both the context menu and the command bar (Corresponds to SPUserCustomAction.Location="CommandUI.Ribbon")</span></span>
* <span data-ttu-id="957ec-178">**Properties:** — необязательный объект JSON, содержащий свойства, которые будут доступны через элемент `this.properties`.</span><span class="sxs-lookup"><span data-stu-id="957ec-178">**Properties:** an optional JSON object containing properties that will be available via the `this.properties` member.</span></span>

<span data-ttu-id="957ec-179">Полный URL-адрес должен выглядеть примерно так, как показано ниже, но соответствовать URL-адресу и расположению списка.</span><span class="sxs-lookup"><span data-stu-id="957ec-179">The full URL should look similar to the following, depending on your tenant URL and the location of the list.</span></span>

```
contoso.sharepoint.com/Lists/Orders/AllItems.aspx?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"6a6ac29e-258e-4a2c-8de3-6bdd358cdb54":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

<span data-ttu-id="957ec-180">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="957ec-180">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted.</span></span>

![Согласие на загрузку скриптов отладки](../../../../images/ext-com-accept-debug-scripts.png)

<span data-ttu-id="957ec-182">Обратите внимание на две новые кнопки с подписями *Command One* и *Command Two*, доступные на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="957ec-182">Notice two new buttons available in the toolbar with titles of *Command One* and *Command Two*.</span></span>

![Согласие на загрузку скриптов отладки](../../../../images/ext-com-default-customizer-output.png)

## <a name="enhancing-the-listview-command-set-rendering"></a><span data-ttu-id="957ec-184">Улучшение отрисовки набора команд ListView</span><span class="sxs-lookup"><span data-stu-id="957ec-184">Enhancing the ListView Command Set rendering</span></span>
<span data-ttu-id="957ec-185">Мы воспользуемся новым API диалоговых окон, позволяющим легко выводить модальные диалоговые окна с помощью кода.</span><span class="sxs-lookup"><span data-stu-id="957ec-185">We'll take advantage of a new Dialog API, which can be used to show modal dialogs easily from your code.</span></span> 

<span data-ttu-id="957ec-186">Вернитесь к консоли и выполните приведенную ниже команду, чтобы включить API диалоговых окон в наше решение.</span><span class="sxs-lookup"><span data-stu-id="957ec-186">Return to the console and execute the following command to include the dialog API in our solution.</span></span>

``` 
npm install @microsoft/sp-dialog --save
```

<span data-ttu-id="957ec-187">Вернитесь к Visual Studio Code (или другому редактору, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="957ec-187">Return to Visual Studio Code (or your preferred editor).</span></span>

<span data-ttu-id="957ec-188">Откройте файл **HelloWorldCommandSet.ts** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="957ec-188">Open **HelloWorldCommandSet.ts** from the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="957ec-189">Добавьте приведенный ниже оператор импорта для класса `Dialog` из `@microsoft/sp-dialog` после имеющихся операторов импорта.</span><span class="sxs-lookup"><span data-stu-id="957ec-189">Add the following import statement for the `Dialog` class from `@microsoft/sp-dialog` after the existing import statements.</span></span> 

```ts
import { Dialog } from '@microsoft/sp-dialog';
``` 

<span data-ttu-id="957ec-190">Измените метод **onExecute** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="957ec-190">Update the **onExecute** method as follows</span></span>

```ts
  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.commandId) {
      case 'COMMAND_1':
        Dialog.alert(`Clicked ${strings.Command1}`);
        break;
      case 'COMMAND_2':
        Dialog.prompt(`Clicked ${strings.Command2}. Enter something to alert:`).then((value: string) => {
          Dialog.alert(value);
        });
        break;
      default:
        throw new Error('Unknown command');
    }
  }
``` 
<span data-ttu-id="957ec-p117">Вернитесь к окну консоли и убедитесь, что не возникло никаких исключений. Если в localhost еще нет запущенных решений, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="957ec-p117">Switch back to your console window and ensure that you do not have any exceptions. If you do not already have the solution running in localhost, execute the following command:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="957ec-193">Вернитесь к представлению списка и используйте те же параметры запроса, что и раньше. Идентификатор должен совпадать с идентификатором расширения, указанным в файле **HelloWorldCommandSet.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="957ec-193">Return to the list view and use the same query parameters used previously with the Id matching your extension identifier available in the **HelloWorldCommandSet.manifest.json** file.</span></span>

<span data-ttu-id="957ec-194">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="957ec-194">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted.</span></span>

![Согласие на загрузку скриптов отладки](../../../../images/ext-com-accept-debug-scripts.png)

<span data-ttu-id="957ec-p118">На панели инструментов по-прежнему отображаются те же кнопки, но их поведение при нажатии изменилось. Теперь мы работаем с новым API диалоговых окон, который легко использовать с решениями даже для сложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="957ec-p118">We still have the same buttons in the toolbar, but you'll notice they behave differently if you click them one-by-one. Now we are using the new dialog API, which can be easily used with your solutions even for complex scenarios.</span></span> 

![Диалоговое окно, отображаемое на странице](../../../../images/ext-com-dialog-output.png)

## <a name="adding-a-listview-command-set-to-a-solution-package-for-deployment"></a><span data-ttu-id="957ec-199">Добавление набора команд ListView к пакету решения для развертывания</span><span class="sxs-lookup"><span data-stu-id="957ec-199">Adding a ListView Command Set to a solution package for deployment</span></span>

<span data-ttu-id="957ec-200">Вернитесь к решению в Visual Studio Code (или другом редакторе, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="957ec-200">Return to your solution in Visual Studio Code (or to your preferred editor).</span></span>

<span data-ttu-id="957ec-201">Для начала необходимо создать папку **assets**, в которую мы поместим все ресурсы платформы компонентов, используемые для подготовки структур SharePoint при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="957ec-201">We'll first need to create an **assets** folder where we will place all feature framework assets used to provision SharePoint structures when the package is installed.</span></span>

* <span data-ttu-id="957ec-202">Создайте папку **sharepoint** в корневой папке решения.</span><span class="sxs-lookup"><span data-stu-id="957ec-202">Create a folder named **sharepoint** in the root of the solution</span></span>
* <span data-ttu-id="957ec-203">Создайте папку **assets** в только что созданной папке **sharepoint**.</span><span class="sxs-lookup"><span data-stu-id="957ec-203">Create a folder named **assets** as a sub folder within the just created **sharepoint** folder</span></span>

<span data-ttu-id="957ec-204">Структура решения должна быть примерно такой, как на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="957ec-204">Your solution structure should look similar to the following picture:</span></span>

![Папка assets в структуре решения](../../../../images/ext-com-assets-folder.png)

### <a name="add-an-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="957ec-206">Добавление файла element.xml для определений SharePoint</span><span class="sxs-lookup"><span data-stu-id="957ec-206">Add an elements.xml file for SharePoint definitions</span></span>

<span data-ttu-id="957ec-207">Создайте в папке **sharepoint\assets** файл **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="957ec-207">Create a new file inside the **sharepoint\assets** folder named **elements.xml**</span></span>

<span data-ttu-id="957ec-p119">Скопируйте приведенную ниже структуру XML в файл **elements.xml**. Обязательно замените значение свойства **ClientSideComponentId** на уникальный идентификатор набора команд ListView, указанный в файле **HelloWorldCommandSet.manifest.json** из папки **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="957ec-p119">Copy the following xml structure into **elements.xml**. Be sure to update the **ClientSideComponentId** property to the unique Id of your ListView Command Set available in the **HelloWorldCommandSet.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="957ec-p120">Обратите внимание, что мы используем определенное значение расположения `ClientSideExtension.ListViewCommandSet.CommandBar`, чтобы указать, что это набор команд ListView, который должен отображаться на панели команд. Мы также задаем для параметра `RegistrationId` значение **100**, а для параметра `RegistrationType` — значение **List**, чтобы автоматически связать дополнительное действие с универсальными списками.</span><span class="sxs-lookup"><span data-stu-id="957ec-p120">Notice that we use a specific location value of `ClientSideExtension.ListViewCommandSet.CommandBar` to define that this is a ListView Command Set and it should be displayed in the command bar. We also define the `RegistrationId` as **100** and the `RegistrationType` as **List** to associate this custom action automatically with generic lists.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxListViewCommandSet"
        RegistrationId="100"
        RegistrationType="List"
        Location="ClientSideExtension.ListViewCommandSet.CommandBar"
        ClientSideComponentId="5fc73e12-8085-4a4b-8743-f6d02ffe1240">

    </CustomAction>

</Elements>
```

<span data-ttu-id="957ec-212">Допустимые значения расположений, которые можно использовать с набором команд ListView:</span><span class="sxs-lookup"><span data-stu-id="957ec-212">Possible location values which can be used with a ListView Command Set:</span></span>

* <span data-ttu-id="957ec-213">`ClientSideExtension.ListViewCommandSet.CommandBar` — панель инструментов списка или библиотеки;</span><span class="sxs-lookup"><span data-stu-id="957ec-213">`ClientSideExtension.ListViewCommandSet.CommandBar` - Toolbar of the list or library</span></span>
* <span data-ttu-id="957ec-214">`ClientSideExtension.ListViewCommandSet.ContextMenu` — контекстное меню для элементов списка или библиотеки;</span><span class="sxs-lookup"><span data-stu-id="957ec-214">`ClientSideExtension.ListViewCommandSet.ContextMenu` - Context menu for list or library items</span></span>
* <span data-ttu-id="957ec-215">`ClientSideExtension.ListViewCommandSet` — регистрация команд для панели инструментов и контекстного меню.</span><span class="sxs-lookup"><span data-stu-id="957ec-215">`ClientSideExtension.ListViewCommandSet` - Register commands to both the toolbar and to the context menu</span></span>

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="957ec-216">Проверка учета определений в конвейере сборки</span><span class="sxs-lookup"><span data-stu-id="957ec-216">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="957ec-p121">Откройте файл **package-solution.json** из папки **config**. В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="957ec-p121">Open **package-solution.json** from the **config** folder. The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

```json
{
  "solution": {
    "name": "command-extension-client-side-solution",
    "id": "dfffbe21-e422-4c0f-a302-d7d62a30c1bf",
    "version": "1.0.0.0",
    "skipFeatureDeployment": false,
  },
  "paths": {
    "zippedPackage": "solution/command-extension.sppkg"
  }
}
```

<span data-ttu-id="957ec-p122">Чтобы убедиться, что новый файл **elements.xml** учитывается при упаковке решения, необходимо включить определение компонента для пакета решения. Добавим определение JSON для нужного компонента в структуру решения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="957ec-p122">To ensure that our newly added **elements.xml** file is taken into account while the solution is being packaged, we'll need to include a Feature Framework feature definition for the solution package. Let's include a JSON definition for the needed feature inside of the solution structure as demonstrated below.</span></span>

```json
{
  "solution": {
    "name": "command-extension-client-side-solution",
    "id": "dfffbe21-e422-4c0f-a302-d7d62a30c1bf",
    "version": "1.0.0.0",
    "skipFeatureDeployment": false,    
    "features": [{
      "title": "ListView Command Set - Deployment of custom action.",
      "description": "Deploys a custom action with ClientSideComponentId association",
      "id": "456da147-ced2-3036-b564-8dad5c1c2e35",
      "version": "1.0.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ]
      }
    }]
  },
  "paths": {
    "zippedPackage": "solution/command-extension.sppkg"
  }
}
```

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="957ec-221">Развертывание расширения в SharePoint Online и размещение кода JavaScript с локального узла</span><span class="sxs-lookup"><span data-stu-id="957ec-221">Deploy the Extension to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="957ec-222">Теперь все готово для развертывания решения на сайте SharePoint и автоматического связывания с объектом *CustomAction* на уровне сайта.</span><span class="sxs-lookup"><span data-stu-id="957ec-222">Now you are ready to deploy the solution to a SharePoint site and to have the *CustomAction* automatically associated on the site level.</span></span>

<span data-ttu-id="957ec-223">Чтобы упаковать клиентское решение, содержащее расширение, и получить базовую структуру, готовую к упаковке, введите в окне консоли приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="957ec-223">In the console window, enter the following command to package your client-side solution that contains the extension, so that we get the basic structure ready for packaging:</span></span>

```
gulp bundle
```

<span data-ttu-id="957ec-224">Затем выполните следующую команду, чтобы создать пакет решения:</span><span class="sxs-lookup"><span data-stu-id="957ec-224">Next, execute the following command so that the solution package is created:</span></span>

```
gulp package-solution
```

<span data-ttu-id="957ec-225">Эта команда создаст пакет в папке **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="957ec-225">The command will create the package in the **sharepoint/solution** folder:</span></span>

```
command-extension.sppkg
```

<span data-ttu-id="957ec-226">Далее вам потребуется развернуть созданный пакет в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="957ec-226">Next you need to deploy the package that was generated to the App Catalog.</span></span>

<span data-ttu-id="957ec-227">Перейдите к **каталогу приложений** вашего клиента и откройте библиотеку **Приложения для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="957ec-227">Go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

<span data-ttu-id="957ec-p123">Отправьте или перетащите файл `command-extension.sppkg` из папки **sharepoint/solution** в каталог приложений. В SharePoint откроется диалоговое окно с предложением доверять клиентскому решению.</span><span class="sxs-lookup"><span data-stu-id="957ec-p123">Upload or drag and drop the `command-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog. SharePoint will display a dialog and ask you to trust the client-side solution.</span></span>

<span data-ttu-id="957ec-p124">Обратите внимание, что мы не обновляли URL-адреса для размещения решения в этом развертывании, чтобы URL-адрес по-прежнему указывал на `https://localhost:4321`. Нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="957ec-p124">Notice that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to `https://localhost:4321`. Click the **Deploy** button.</span></span>

![Операция доверия при отправке в каталог приложений](../../../../images/ext-com-sppkg-deploy-trust.png)

<span data-ttu-id="957ec-p125">Вернитесь к консоли и убедитесь, что решение запущено. Если это не так, выполните в папке решения следующую команду:</span><span class="sxs-lookup"><span data-stu-id="957ec-p125">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="957ec-p126">Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения.</span><span class="sxs-lookup"><span data-stu-id="957ec-p126">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

<span data-ttu-id="957ec-237">Нажмите значок шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**, чтобы перейти на страницу "Приложения".</span><span class="sxs-lookup"><span data-stu-id="957ec-237">Chose the gear icon on the top navigation bar on the right and choose **Add an app** to go to your Apps page.</span></span>

<span data-ttu-id="957ec-238">В поле **Поиск** введите **extension** и нажмите клавишу *ВВОД*, чтобы отфильтровать приложения.</span><span class="sxs-lookup"><span data-stu-id="957ec-238">In the **Search** box, enter '**command**' and press *Enter* to filter your apps.</span></span>

![Установка набора команд ListView на сайте](../../../../images/ext-com-install-solution-to-site.png)

<span data-ttu-id="957ec-p127">Выберите приложение **command-extension-client-side-solution**, чтобы установить его на сайте. По завершении установки обновите страницу, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="957ec-p127">Choose the **command-extension-client-side-solution** app to install the solution on the site. When the installation is completed, refresh the page by pressing **F5**.</span></span>

<span data-ttu-id="957ec-242">Когда приложение будет успешно установлено, нажмите кнопку **Создать** на панели инструментов страницы **Содержимое сайта** и выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="957ec-242">When the application has been successfully installed, Click **New** from the toolbar on the **Site Contents** page and choose **List**</span></span>

![Создание списка](../../../../images/ext-com-create-new-list.png)

<span data-ttu-id="957ec-244">Укажите имя **Sample** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="957ec-244">Provide the name as **Sample** and click **Create**.</span></span>

<span data-ttu-id="957ec-245">Обратите внимание, что кнопки **Command One** и **Command Two** отрисовываются на панели задач в соответствии с изменениями набора команд ListView.</span><span class="sxs-lookup"><span data-stu-id="957ec-245">Notice how **Command One** and **Command Two** are being rendered in the toolbar based on your ListView Command Set customizations.</span></span> 

![Дополнительные кнопки на панели инструментов](../../../../images/ext-com-dialog-visible-deployment.png)
