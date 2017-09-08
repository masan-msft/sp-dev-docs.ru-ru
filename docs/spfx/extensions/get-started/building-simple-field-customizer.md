# <a name="build-your-first-field-customizer-extension"></a><span data-ttu-id="4aebb-101">Создание первого расширения для настройки полей</span><span class="sxs-lookup"><span data-stu-id="4aebb-101">Build your first Field Customizer extension</span></span>

><span data-ttu-id="4aebb-p101">**Примечание.** Расширения для платформы SharePoint Framework находятся на этапе тестирования и могут меняться. В настоящее время расширения SharePoint Framework невозможно использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="4aebb-p102">Расширения — это клиентские компоненты, которые запускаются в контексте страницы SharePoint. Расширения можно развертывать в SharePoint Online, а для их создания можно использовать современные инструменты и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p102">Extensions are client-side components that run inside the context of a SharePoint page. Extensions can be deployed to SharePoint Online and you can use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="4aebb-106">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=fijOzUmlXrY&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="4aebb-106">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=fijOzUmlXrY&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=fijOzUmlXrY&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorialfield.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="4aebb-107">Создание проекта расширения</span><span class="sxs-lookup"><span data-stu-id="4aebb-107">Create an extension project</span></span>
<span data-ttu-id="4aebb-108">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="4aebb-108">Create a new project directory in your favorite location.</span></span>

```
md field-extension
```

<span data-ttu-id="4aebb-109">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="4aebb-109">Go to the project directory.</span></span>

```
cd field-extension
```

<span data-ttu-id="4aebb-110">Создайте расширение HelloWorld, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4aebb-110">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>

```
yo @microsoft/sharepoint
```

<span data-ttu-id="4aebb-111">Когда появится запрос, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4aebb-111">When prompted:</span></span>

* <span data-ttu-id="4aebb-112">Оставьте значение по умолчанию (**field-extension**) для имени решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-112">Accept the default value of **field-extension** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="4aebb-113">Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-113">Choose **Use the current folder** and press **Enter**.</span></span>
* <span data-ttu-id="4aebb-114">Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="4aebb-114">Choose **N** to require extension to be installed on each site explicitly when it's being used.</span></span>
* <span data-ttu-id="4aebb-115">Выберите для создаваемого клиентского компонента тип **Extension (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-115">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="4aebb-116">Выберите для создаваемого расширения тип **Field Customizer (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-116">Choose **Field Customizer (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="4aebb-117">Далее вам потребуется указать определенные сведения о расширении.</span><span class="sxs-lookup"><span data-stu-id="4aebb-117">The next set of prompts will ask for specific information about your extension:</span></span>

* <span data-ttu-id="4aebb-118">Оставьте значение по умолчанию (**HelloWorld**) для имени решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-118">Accept the default value of **HelloWorld** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="4aebb-119">Оставьте значение по умолчанию (**HelloWorld description**) для описания решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-119">Accept the default value of **HelloWorld description** as your extension description and press **Enter**.</span></span>
* <span data-ttu-id="4aebb-120">Оставьте платформу, выбранную по умолчанию (**No JavaScript Framework**), и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-120">Accept the default **No JavaScript Framework** as the framework selection and press **Enter**</span></span> 

![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../../images/ext-field-yeoman-prompts.png)

<span data-ttu-id="4aebb-p103">После этого Yeoman установит необходимые зависимости и сформирует файлы решения, а также расширение **HelloWorld**. Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p103">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the **HelloWorld** extension. This might take a few minutes.</span></span> 

<span data-ttu-id="4aebb-124">После успешного скаффолдинга должно появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="4aebb-124">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

!["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../../images/ext-field-yeoman-complete.png)

<span data-ttu-id="4aebb-126">Сведения об устранении неполадок см. в статье [Известные проблемы](../basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="4aebb-126">For information about troubleshooting any errors, see [Known issues](../basics/known-issues).</span></span>

<span data-ttu-id="4aebb-127">Завершив формирование решения, введите в консоли приведенную ниже команду, чтобы запустить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="4aebb-127">Once the solution scaffolding is completed, type the following into the console to start Visual Studio Code.</span></span>

```
code .
```

> <span data-ttu-id="4aebb-128">Обратите внимание, что клиентское решение SharePoint создано с помощью HTML и TypeScript, поэтому для разработки расширения можно использовать любой редактор кода, который поддерживает клиентское программирование.</span><span class="sxs-lookup"><span data-stu-id="4aebb-128">Notice that because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

<span data-ttu-id="4aebb-p104">Обратите внимание, что стандартная структура решения аналогична структуре клиентских веб-частей. Это базовая структура решения SharePoint Framework, многие параметры которой не зависят от типа решения.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p104">Notice how the default solution structure is like the solution structure of client-side web parts. This is the basic SharePoint Framework solution structure with similar configuration options across all solution types.</span></span>

![Решение SharePoint Framework, открытое после первоначального формирования](../../../../images/ext-field-vscode-solution-structure.png)

<span data-ttu-id="4aebb-132">Откройте файл **HelloWorldFieldCustomizer.manifest.json** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-132">Open **HelloWorldFieldCustomizer.manifest.json** at the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="4aebb-p105">В этом файле определяются тип расширения и уникальный идентификатор **id** для него. Этот идентификатор потребуется позже, при отладке и развертывании расширения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p105">This file defines your extension type and a unique identifier **“id”** for your extension. You’ll need this unique identifier later when debugging and deploying your extension to SharePoint.</span></span>

![Содержимое манифеста настройщика полей в формате JSON](../../../../images/ext-field-vscode-manifest.png)

## <a name="coding-your-field-customizer"></a><span data-ttu-id="4aebb-136">Написание кода настройщика полей</span><span class="sxs-lookup"><span data-stu-id="4aebb-136">Coding your Field Customizer</span></span> 
<span data-ttu-id="4aebb-137">Откройте файл **HelloWorldFieldCustomizer.ts** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-137">Open the **HelloWorldFieldCustomizer.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="4aebb-138">Обратите внимание, что базовый класс для настройщика полей импортируется из пакета **sp-application-base**, который содержит код платформы SharePoint Framework, необходимый для настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="4aebb-138">Notice that the base class for the Field Customizer is imported from the **sp-application-base** package, which contains SharePoint framework code required by the Field Customizer.</span></span>

```ts
import { Log } from '@microsoft/sp-core-library';
import { override } from '@microsoft/decorators';
import {
  BaseFieldCustomizer,
  IFieldCustomizerCellEventParameters
} from '@microsoft/sp-listview-extensibility';
```

<span data-ttu-id="4aebb-139">Логика настройщика полей содержится в методах **OnInit()**, **onRenderCell()** и **onDisposeCell()**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-139">The logic for your Field Customizer is contained in the **OnInit()**, **onRenderCell()**, and **onDisposeCell()** methods.</span></span>

* <span data-ttu-id="4aebb-p106">**onInit():** — здесь выполняется вся настройка, необходимая для расширения. Это событие происходит после назначения `this.context` и `this.properties`, но до того, как модель DOM будет готова. Как и в случае с веб-частями, `onInit()` возвращает обещание, с помощью которого можно выполнять асинхронные операции. `onRenderCell()` не будет вызываться, пока обещание не будет разрешено. Если вам это не нужно, просто верните `Promise.resolve<void>();`.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p106">**onInit():**  this is where you should perform any setup needed for your extension. This event occurs after `this.context` and `this.properties` are assigned, but before the page DOM is ready. As with web parts, `onInit()` returns a promise that you can use to perform asynchronous operations; `onRenderCell()` will not be called until your promise has resolved. If you don’t need that, simply return `Promise.resolve<void>();`.</span></span>
* <span data-ttu-id="4aebb-p107">**onRenderCell():** это событие происходит при отрисовке каждой ячейки. Оно предоставляет элемент HTML `event.domElement`, в который код может записывать содержимое.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p107">**onRenderCell():**  This event occurs before each cell is rendered. It provides an `event.domElement` HTML element where your code can write its content.</span></span>
* <span data-ttu-id="4aebb-p108">**onDisposeCell():** — это событие, которое происходит сразу после удаления `event.cellDiv`. Его можно использовать для освобождения ресурсов, выделенных во время отрисовки полей. Например, если обработчик события `onRenderCell()` подключил элемент React, то для его освобождения необходимо использовать метод `onDisposeCell()`. В противном случае произойдет утечка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p108">**onDisposeCell():** This event occurs immediately before the `event.cellDiv` is deleted. It can be used to free any resources that were allocated during field rendering. For example, if `onRenderCell()` mounted a React element, `onDisposeCell()` must be used to free it, otherwise a resource leak would occur.</span></span> 

<span data-ttu-id="4aebb-149">Ниже представлено содержимое методов **onRenderCell()** и **onDisposeCell()** в решении по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4aebb-149">Below are the contents of **onRenderCell()** and **onDisposeCell()** in the default solution:</span></span>

```ts
  @override
  public onRenderCell(event: IFieldCustomizerCellEventParameters): void {
    // Use this method to perform your custom cell rendering.
    const text: string = `['${event.fieldValue}']`;

    event.domElement.innerText = text;

    event.domElement.classList.add(styles.cell);
  }

  @override
  public onDisposeCell(event: IFieldCustomizerCellEventParameters): void {
    // This method should be used to free any resources that were allocated during rendering.
    // For example, if your onRenderCell() called ReactDOM.render(), then you should
    // call ReactDOM.unmountComponentAtNode() here.
    super.onDisposeCell(event);
  }
```

## <a name="debugging-your-field-customizer-using-gulp-serve-and-query-string-parameters"></a><span data-ttu-id="4aebb-150">Отладка настройщика полей с помощью gulp serve и параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="4aebb-150">Debugging your Field Customizer using gulp serve and query string parameters</span></span>
<span data-ttu-id="4aebb-p109">В настоящее время расширения SharePoint Framework невозможно тестировать с помощью локального рабочего места, поэтому тестировать и разрабатывать их следует непосредственно на активном сайте SharePoint Online. Однако при этом не требуется развертывать модификацию в каталоге приложений, что делает отладку простой и эффективной.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p109">SharePoint Framework extensions cannot currently be tested using the local workbench, so you'll need to test and develop them directly against a live SharePoint Online site. You do not however need to deploy your customization to the app catalog to do this, which keeps the debugging experience simple and efficient.</span></span>

<span data-ttu-id="4aebb-153">Для начала скомпилируйте код и разместите скомпилированные файлы с локального компьютера, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4aebb-153">First, compile your code and host the compiled files from the local machine by running this command:</span></span>
```
gulp serve --nobrowser
```

<span data-ttu-id="4aebb-154">Обратите внимание, что мы использовали параметр `--nobrowser`, так как нет смысла запускать локальную рабочую область — сейчас нельзя отлаживать расширения локально.</span><span class="sxs-lookup"><span data-stu-id="4aebb-154">Notice that we used the `--nobrowser` option, since there's no value in launching the local workbench since you currently cannot debug extensions locally.</span></span>

<span data-ttu-id="4aebb-155">Когда компиляция кода завершится без ошибок, полученный манифест будет доступен по адресу https://localhost:4321.</span><span class="sxs-lookup"><span data-stu-id="4aebb-155">Once it compiles the code without errors, it will serve the resulting manifest from http://localhost:4321.</span></span>

![gulp serve](../../../../images/ext-field-gulp-serve.png)

<span data-ttu-id="4aebb-157">Для тестирования расширения перейдите к сайту в клиенте SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4aebb-157">To test your extension, navigate to a site in your SharePoint Online tenant.</span></span>

<span data-ttu-id="4aebb-158">Откройте страницу **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-158">Move to the **Site Contents** page.</span></span>

<span data-ttu-id="4aebb-159">Нажмите кнопку **Создать** на панели инструментов и выберите **Список**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-159">Click **New** from the toolbar and choose **List**:</span></span>

![Создание списка](../../../../images/ext-field-create-new-list.png)

<span data-ttu-id="4aebb-161">Создайте список под названием *Заказы* и нажмите кнопку **Создать**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-161">Create a new list named *Orders* and click **Create**:</span></span>

![Создание списка под названием "Заказы"](../../../../images/ext-field-create-new-list-order.png)

<span data-ttu-id="4aebb-163">Нажмите значок **плюс** и выберите **Число**, чтобы создать числовое поле для списка:</span><span class="sxs-lookup"><span data-stu-id="4aebb-163">Click the **plus** sign and choose **Number** to create a new Number field for the list:</span></span>

![Создание числового поля](../../../../images/ext-field-new-number-field.png)

<span data-ttu-id="4aebb-165">Задайте для поля имя **Процент** и нажмите кнопку **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-165">Set name of the field to **Percent** and click **Save**:</span></span>

![Создание поля под названием "Процент"](../../../../images/ext-field-new-number-field-percent.png)

<span data-ttu-id="4aebb-p110">Добавьте несколько элементов с различными числами в процентное поле. Позже мы изменим отрисовку, чтобы разные числа отображались по-разному в соответствии с вашей реализацией.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p110">Add a few items with different numbers in the percent field. We'll modify the rendering later in this tutorial, so the different numbers will be presented differently based on your custom implementation.</span></span>

![Создание элементов в новом списке с разными значениями в поле "Процент"](../../../../images/ext-field-create-items-to-list.png)

<span data-ttu-id="4aebb-170">Так как наш настройщик полей размещается в localhost и запущен, мы можем использовать определенные параметры запроса отладки для выполнения кода в новом списке.</span><span class="sxs-lookup"><span data-stu-id="4aebb-170">Since our Field Customizer is still hosted in localhost and is running, we can use specific debug query parameters to execute the code in the newly created list.</span></span>

<span data-ttu-id="4aebb-p111">Добавьте к URL-адресу приведенные ниже параметры строки запроса. Обратите внимание, что вам потребуется обновить идентификатор в соответствии с идентификатором расширения, указанным в файле **HelloWorldFieldCustomizer.manifest.json**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-p111">Append the following query string parameters to the URL. Notice that you will need to update the id to match your own extension identifier available from the **HelloWorldFieldCustomizer.manifest.json** file:</span></span>

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Percent":{"id":"7e7a4262-d02b-49bf-bfcb-e6ef1716aaef","properties":{"sampleText":"Hello!"}}}
```
<span data-ttu-id="4aebb-173">Дополнительные сведения о параметрах запросов URL-адресов</span><span class="sxs-lookup"><span data-stu-id="4aebb-173">More detail about the URL query parameters:</span></span>

* <span data-ttu-id="4aebb-p112">**loadSPFX=true:** гарантирует, что платформа SharePoint Framework загружается на странице. Для оптимальной производительности платформа обычно не загружается, если не зарегистрировано хотя бы одно расширение. Так как пока не зарегистрировано ни одного расширения, нам необходимо отдавать явную команду на загрузку платформы.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p112">**loadSPFX=true:**  ensures that the SharePoint Framework is loaded on the page. For performance reasons, the framework is not normally loaded unless at least one extension is registered. Since no components are registered yet, we must explicitly load the framework.</span></span>
* <span data-ttu-id="4aebb-p113">**debugManifestsFile:** указывает, что нам требуется загрузить компоненты SPFx, предоставляемые локально. Как правило, загрузчик ищет компоненты только в каталоге приложений (для развернутого решения) и на сервере манифестов SharePoint (для системных библиотек).</span><span class="sxs-lookup"><span data-stu-id="4aebb-p113">**debugManifestsFile:**  specifies that we want to load SPFx components that are being locally served. Normally the loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>
* <span data-ttu-id="4aebb-p114">**fieldCustomizers:** указывает поля в списке, отрисовку которых должен контролировать настройщик полей. Параметр ID указывает GUID расширения, который следует использовать для управления отрисовкой поля. Параметр properties — это необязательная текстовая строка, содержащая объект JSON, который будет десериализован в `this.properties` для вашего расширения.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p114">**fieldCustomizers**:  Indicates which fields in your list should have their rendering controlled by the Field Customizer. The ID parameter specifies the GUID of the extension that should be used to control the rendering of the field. The properties parameter is an optional text string containing a JSON object that will be deserialized into `this.properties` for your extension.</span></span>
    * <span data-ttu-id="4aebb-182">**Key:** в качестве ключа используйте внутреннее имя поля.</span><span class="sxs-lookup"><span data-stu-id="4aebb-182">**Key:** use the internal name of the field as the key</span></span>
    * <span data-ttu-id="4aebb-183">**Id:** — GUID расширения для настройки полей, связанный с этим полем.</span><span class="sxs-lookup"><span data-stu-id="4aebb-183">**Id:** the guid of the field customizer extension associated with this field</span></span>
    * <span data-ttu-id="4aebb-p115">**Properties:** — значения свойств, определенные в расширении. В данном примере *sampleText* — это свойство, определенное расширением.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p115">**Properties:** property values defined in the extension. In this example, *‘sampleText’* is a property defined by the extension</span></span>

<span data-ttu-id="4aebb-186">Полный URL-адрес должен выглядеть примерно так, как показано ниже, но соответствовать URL-адресу и расположению нового списка.</span><span class="sxs-lookup"><span data-stu-id="4aebb-186">The full URL should look similar to the following, depending on your tenant URL and the location of the newly created list:</span></span>

```
contoso.sharepoint.com/Lists/Orders/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Percent":{"id":"7e7a4262-d02b-49bf-bfcb-e6ef1716aaef","properties":{"sampleText":"Hello!"}}}
```

<span data-ttu-id="4aebb-187">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="4aebb-187">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted:</span></span>

![Согласие на загрузку скриптов отладки](../../../../images/ext-field-accept-debug-scripts.png)

<span data-ttu-id="4aebb-189">Обратите внимание, что процентные значения теперь представлены с дополнительными символами [ ]:</span><span class="sxs-lookup"><span data-stu-id="4aebb-189">Notice how the Percent values are now presented with additional [ ] characters:</span></span>

![Согласие на загрузку скриптов отладки](../../../../images/ext-field-default-customizer-output.png)

## <a name="enhancing-the-field-customizer-rendering"></a><span data-ttu-id="4aebb-191">Улучшение отрисовки настройщика полей</span><span class="sxs-lookup"><span data-stu-id="4aebb-191">Enhancing the Field Customizer rendering</span></span>
<span data-ttu-id="4aebb-192">Теперь, когда мы успешно протестировали встроенную отправную точку для создания настройщика полей, пришло время немного изменить логику для более аккуратной отрисовки значения поля.</span><span class="sxs-lookup"><span data-stu-id="4aebb-192">Now that we have successfully tested the out of the box starting point of the Field Customizer, let's modify the logic slightly to have a more polished rendering of the field value.</span></span> 

<span data-ttu-id="4aebb-193">Откройте файл **HelloWorld.module.scss** в папке **src\extensions\helloWorld** и измените определение стиля, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4aebb-193">Open the **HelloWorld.module.scss** file in the **src\extensions\helloWorld** folder and update the styling definition as follows.</span></span>

```
.HelloWorld {
  .cell {
    display: 'inline-block';
  }
  .full {
    background-color: '#e5e5e5';
    width: '100px';
  }
}

```
<span data-ttu-id="4aebb-194">Откройте файл **HelloWorldFieldCustomizer.ts** в папке **src\extensions\helloWorld** и измените метод **onRednerCell**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4aebb-194">Open the **HelloWorldFieldCustomizer.ts** file in the **src\extensions\helloWorld** folder and update the **onRednerCell** method as follows.</span></span>

```ts
  @override
  public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

    event.domElement.classList.add(styles.cell);
    event.domElement.innerHTML = `
                <div class='${styles.full}'>
                  <div style='width: ${event.fieldValue}px; background:#0094ff; color:#c0c0c0'>
                    &nbsp; ${event.fieldValue}
                  </div>
                </div>`;
  }
```

<span data-ttu-id="4aebb-p116">Вернитесь к окну консоли и убедитесь, что не возникло никаких исключений. Если в *localhost* еще нет запущенных решений, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4aebb-p116">Switch back to your console window and ensure that you do not have any exceptions. If you do not already have the solution running in localhost, execute the following command:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="4aebb-197">Вернитесь к созданному ранее списку и используйте тот же параметр запроса, что и раньше, с полем "Заказы" и идентификатором, замененным на идентификатор расширения, который указан в файле **HelloWorldFieldCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-197">Move back to your previously created list and use the same query parameter as used previously with the Field being 'Percent' and the Id being updated to your extension identifier available from the **HelloWorldFieldCustomizer.manifest.json** file.</span></span>

<span data-ttu-id="4aebb-198">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="4aebb-198">Accept the loading of Debug Manifests, by clicking **Load debug scripts** when prompted.</span></span>

![Согласие на загрузку скриптов отладки](../../../../images/ext-field-accept-debug-scripts.png)

<span data-ttu-id="4aebb-p117">Обратите внимание, что мы полностью изменили стиль отрисовки поля. Значение поля указывается с помощью его графического представления.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p117">Notice how we have changed the field rendering style completely. The field value is indicated using a graphical representation of the value.</span></span>

![Графическое представление процента](../../../../images/ext-field-percent-field-graphic.png)

## <a name="add-the-field-definition-to-the-solution-package-for-deployment"></a><span data-ttu-id="4aebb-203">Добавление определения поля в пакет решения для развертывания</span><span class="sxs-lookup"><span data-stu-id="4aebb-203">Add the field definition to the solution package for deployment</span></span>
<span data-ttu-id="4aebb-p118">Теперь, когда мы надлежащим образом протестировали решение в режиме отладки, мы можем упаковать его для автоматического развертывания в составе пакета решения, развертываемого на сайтах. Для этого нужно выполнить несколько операций.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p118">Now that we have tested our solution properly in debug mode, we can package this to be deployed automatically as part of the solution package deployed to the sites. There are few things to take care of here.</span></span>

1. <span data-ttu-id="4aebb-206">Установите пакет решения на нужном сайте, чтобы манифест расширения попал в список разрешенных для запуска.</span><span class="sxs-lookup"><span data-stu-id="4aebb-206">Install the solution package to the site where it should be installed, so that the extension manifest is being white listed for execution</span></span>
2. <span data-ttu-id="4aebb-p119">Свяжите настройщик полей с существующим полем на сайте. Это можно сделать программным способом (CSOM/REST) или с помощью платформы компонентов в пакете решения SharePoint Framework. Ниже перечислены свойства, которые необходимо связать с объектом *SPField* на уровне сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p119">Associate the Field Customizer to an existing field in the site. This can be performed programmatically (CSOM/REST) or by using the feature framework inside of the SharePoint Framework solution package. You'll need to associate the following properties in the *SPField* object at the site or list level.</span></span>
    * <span data-ttu-id="4aebb-210">**ClientSiteComponentId:** — это идентификатор (GUID) настройщика приложений, установленного в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="4aebb-210">**ClientSiteComponentId:** This is the identifier (GUID) of the Field Customizer, which has been installed in the app catalog.</span></span> 
    * <span data-ttu-id="4aebb-211">**ClientSideComponentProperties:** это необязательный параметр, с помощью которого можно предоставлять свойства для экземпляра настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="4aebb-211">**ClientSideComponentProperties:** This is an optional parameter, which can be used to provide properties for the Field Customizer instance.</span></span>

> <span data-ttu-id="4aebb-p120">Обратите внимание, что вы можете указать, требуется ли добавлять решение, содержащее ваше расширение, на сайт, используя параметр `skipFeatureDeployment` в файле **package-solution.json**. Даже если устанавливать решение на сайт не требуется, чтобы расширение было видимым, свойство **ClientSideComponentId** необходимо связать с конкретными объектами.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p120">Notice, you can control the requirement to add a solution containing your extension to the site by using `skipFeatureDeployment` setting in **package-solution.json**. Event though you would not require solution to be installed on the site, you'd need to associate **ClientSideComponentId** to specific objects for the extension to be visible.</span></span> 

<span data-ttu-id="4aebb-214">На следующих этапах мы создадим определение поля, которое затем будет автоматически развернуто с необходимыми параметрами при установке пакета решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="4aebb-214">In the following steps, we'll create a new field definition, which will then be automatically deployed with the needed configurations when the solution package is installed on a site.</span></span>

<span data-ttu-id="4aebb-215">Вернитесь к решению в Visual Studio Code (или другом редакторе, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="4aebb-215">Return to your solution in Visual Studio Code (or to your preferred editor).</span></span>

<span data-ttu-id="4aebb-216">Для начала необходимо создать папку **assets**, в которую мы поместим все ресурсы платформы компонентов, используемые для подготовки структур SharePoint при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="4aebb-216">We'll first need to create an **assets** folder where we will place all feature framework assets used to provision SharePoint structures when the package is installed.</span></span>

* <span data-ttu-id="4aebb-217">Создайте папку **sharepoint** в корневой папке решения.</span><span class="sxs-lookup"><span data-stu-id="4aebb-217">Create a folder named **sharepoint** in the root of the solution</span></span>
* <span data-ttu-id="4aebb-218">Создайте папку **assets** в только что созданной папке **sharepoint**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-218">Create a folder named **assets** as a sub folder of the just created **sharepoint** folder</span></span>

<span data-ttu-id="4aebb-219">Структура решения должна быть примерно такой, как на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="4aebb-219">Your solution structure should look similar to the following picture:</span></span>

![Папка assets в структуре решения](../../../../images/ext-field-assets-folder.png)

### <a name="add-an-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="4aebb-221">Добавление файла element.xml для определений SharePoint</span><span class="sxs-lookup"><span data-stu-id="4aebb-221">Add an elements.xml file for SharePoint definitions</span></span>
<span data-ttu-id="4aebb-222">Создайте в папке **sharepoint\assets** файл **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-222">Create a new file inside the **sharepoint\assets** folder named **elements.xml**</span></span>

<span data-ttu-id="4aebb-p121">Скопируйте приведенную ниже структуру XML в файл **elements.xml**. Обязательно замените значение свойства **ClientSideComponentId** на уникальный идентификатор настройщика полей, указанный в файле **HelloWorldFieldCustomizer.manifest.json** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p121">Copy the following xml structure into **elements.xml**. Be sure to update the **ClientSideComponentId** property to the unique Id of your Field Customizer available in the **HelloWorldFieldCustomizer.manifest.json** file in the** src\extensions\helloWorld** folder.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <Field ID="{060E50AC-E9C1-3D3C-B1F9-DE0BCAC200F6}"
            Name="SPFxPercentage"
            DisplayName="Percentage"
            Type="Number"
            Min="0"
            Required="FALSE"
            Group="SPFx Columns"
            ClientSideComponentId="7e7a4262-d02b-49bf-bfcb-e6ef1716aaef">
    </Field>

</Elements>
```

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="4aebb-225">Проверка учета определений в конвейере сборки</span><span class="sxs-lookup"><span data-stu-id="4aebb-225">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="4aebb-p122">Откройте файл **package-solution.json** из папки **config**. В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="4aebb-p122">Open **package-solution.json** from the **config** folder. The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

```json
{
  "solution": {
    "name": "field-extension-client-side-solution",
    "id": "11cd343e-1ce6-462c-8acb-929804d0c3b2",
    "version": "1.0.0.0",
    "skipFeatureDeployment": false
  },
  "paths": {
    "zippedPackage": "solution/field-extension.sppkg"
  }
}


```

<span data-ttu-id="4aebb-p123">Чтобы убедиться, что новый файл **elements.xml** учитывается при упаковке решения, необходимо включить определение компонента для пакета решения. Добавим определение JSON для нужного компонента в структуру решения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p123">To ensure that our newly added **elements.xml** file is taken into account while solution is being packaged, we'll need to include a Feature Framework feature definition for the solution package. Let's include a JSON definition for the needed feature inside of the solution structure as demonstrated below.</span></span>

```json
{
  "solution": {
    "name": "field-extension-client-side-solution",
    "id": "11cd343e-1ce6-462c-8acb-929804d0c3b2",
    "version": "1.0.0.0",
    "skipFeatureDeployment": false,
    "features": [{
      "title": "Field Extension - Deployment of custom field.",
      "description": "Deploys a custom field with ClientSideComponentId association",
      "id": "123fe847-ced2-3036-b564-8dad5c6c6e83",
      "version": "1.0.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ]
      }
    }]
  },
  "paths": {
    "zippedPackage": "solution/field-extension.sppkg"
  }
}

```

## <a name="deploy-the-field-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="4aebb-230">Развертывание поля в SharePoint Online и размещение кода JavaScript с локального узла</span><span class="sxs-lookup"><span data-stu-id="4aebb-230">Deploy the field to SharePoint Online and host JavaScript from local host</span></span>
<span data-ttu-id="4aebb-231">Теперь все готово для развертывания решения на сайте SharePoint и автоматического добавления связывания в поле.</span><span class="sxs-lookup"><span data-stu-id="4aebb-231">Now you are ready to deploy the solution to a SharePoint site and to get the field association automatically included in a field.</span></span> 

<span data-ttu-id="4aebb-232">Чтобы упаковать клиентское решение, содержащее расширение, и получить базовую структуру, готовую к упаковке, введите в окне консоли приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="4aebb-232">In the console window, enter the following command to package your client-side solution that contains the extension, so that we get the basic structure ready for packaging:</span></span>

```
gulp bundle
```

<span data-ttu-id="4aebb-233">Затем выполните следующую команду, чтобы создать пакет решения:</span><span class="sxs-lookup"><span data-stu-id="4aebb-233">Next, execute the following command so that the solution package is created:</span></span>

```
gulp package-solution
```

<span data-ttu-id="4aebb-234">Эта команда создаст пакет в папке **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-234">The command will create the package in the **sharepoint/solution** folder:</span></span>

```
field-extension.sppkg
```

<span data-ttu-id="4aebb-235">Далее вам потребуется развернуть созданный пакет в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="4aebb-235">Next you need to deploy the package that was generated to the App Catalog.</span></span>

<span data-ttu-id="4aebb-236">Перейдите к **каталогу приложений** вашего клиента и откройте библиотеку **Приложения для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-236">Go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

<span data-ttu-id="4aebb-p124">Отправьте или перетащите файл `field-extension.sppkg` из папки **sharepoint/solution** в каталог приложений. В SharePoint откроется диалоговое окно с предложением доверять клиентскому решению.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p124">Upload or drag and drop the `field-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog. SharePoint will display a dialog and ask you to trust the client-side solution.</span></span>

<span data-ttu-id="4aebb-p125">Обратите внимание, что мы не обновляли URL-адреса для размещения решения в этом развертывании, чтобы URL-адрес по-прежнему указывал на https://localhost:4321. Нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p125">Notice that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to https://localhost:4321. Click the **Deploy** button.</span></span>

![Диалоговое окно развертывания](../../../../images/ext-field-sppkg-deploy-trust.png)

<span data-ttu-id="4aebb-p126">Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p126">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

<span data-ttu-id="4aebb-244">Нажмите значок шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**, чтобы перейти к странице "Приложения".</span><span class="sxs-lookup"><span data-stu-id="4aebb-244">Choose the gears icon on the top navigation bar on the right and choose **Add an app** to go to your Apps page.</span></span>

<span data-ttu-id="4aebb-245">В поле **Поиск** введите **field** и нажмите клавишу *ВВОД*, чтобы отфильтровать приложения.</span><span class="sxs-lookup"><span data-stu-id="4aebb-245">In the **Search** box, enter '**field**' and press *Enter* to filter your apps.</span></span>

![Установка настройщика полей на сайте](../../../../images/ext-field-install-solution-to-site.png)

<span data-ttu-id="4aebb-p127">Выберите приложение **field-extension-client-side-solution**, чтобы установить его на сайте. По завершении установки обновите страницу, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p127">Choose the **field-extension-client-side-solution** app to install the solution on the site. Once the installation is completed, refresh the page by pressing **F5**.</span></span>

<span data-ttu-id="4aebb-249">После установки решения нажмите кнопку **Создать** на панели инструментов страницы **Содержимое сайта** и выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-249">When the solution has been installed, Click **New** from the toolbar in **Site Contents** page and choose **List**:</span></span>

![Создание списка](../../../../images/ext-field-create-new-list.png)

<span data-ttu-id="4aebb-251">Создайте список под названием **Накладные**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-251">Create a list named **Invoices**:</span></span>

<span data-ttu-id="4aebb-252">После создания списка вернитесь к странице **Содержимое сайта** и выберите пункт **Параметры** в контекстном меню нового списка:</span><span class="sxs-lookup"><span data-stu-id="4aebb-252">When the new list has been created, move back to the **Site Contents** page and choose **Settings** from the context menu of the just created list:</span></span>

![Параметры нового списка](../../../../images/ext-field-list-settings.png)

<span data-ttu-id="4aebb-254">Выберите параметр **Добавить из существующих столбцов сайта** в разделе **Столбцы**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-254">Choose **Add from existing site columns** under the **Columns** section:</span></span>

<span data-ttu-id="4aebb-255">Выберите поле **Процент**, подготовленное с помощью пакета решения, в группе **Столбцы SPFx**:</span><span class="sxs-lookup"><span data-stu-id="4aebb-255">Choose the **Percentage** field which was provisioned from the solution package, under the **SPFx Columns** group:</span></span>

![Параметры нового списка](../../../../images/ext-field-add-field-to-list.png)

<span data-ttu-id="4aebb-257">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4aebb-257">Click **OK**.</span></span>

<span data-ttu-id="4aebb-p128">Вернитесь к консоли и убедитесь, что решение запущено. Если это не так, выполните в папке решения следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4aebb-p128">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>

```
gulp serve --nobrowser
```
<span data-ttu-id="4aebb-260">Перейдите к новому списку **Накладные** и добавьте в столбец "Процент" несколько новых элементов с разными значениями, чтобы увидеть, как поле отрисовывается без параметров запроса отладки.</span><span class="sxs-lookup"><span data-stu-id="4aebb-260">Navigate to the newly created **Invoices** list and add a few new items to the list with different values in the Percentage column to see how the field is being rendered without the Debug query parameters.</span></span>

![Отрисовка поля без параметров запроса отладки](../../../../images/ext-field-render-field-without-debug.png)

<span data-ttu-id="4aebb-262">В этом случае код JavaScript по-прежнему размещается в localhost, но вы также можете переместить ресурсы в любую сеть CDN и обновить URL-адрес, чтобы ресурсы JavaScript можно было загружать не только из localhost.</span><span class="sxs-lookup"><span data-stu-id="4aebb-262">In this case, we continued to host the JavaScript from the localhost, but you could just as well relocate the assets to any CDN and update the URL to enable the loading of the JavaScript assets outside of the localhost as well.</span></span> 

<span data-ttu-id="4aebb-p129">Процесс публикации приложения не зависит от типа расширения. Вы можете выполнить действия из указанной ниже статьи, чтобы обновить ресурсы, размещенные в сети CDN.</span><span class="sxs-lookup"><span data-stu-id="4aebb-p129">The process for publishing your app is identical among the different extension types. You can follow the following publishing steps to update the assets to be hosted from a CDN.</span></span>

* <span data-ttu-id="4aebb-265">[Развертывание расширения для Office 365 в сети доставки содержимого](./hosting-extension-from-office365-cdn.md).</span><span class="sxs-lookup"><span data-stu-id="4aebb-265">[Deploy extension to Office 365 CDN](./hosting-extension-from-office365-cdn.md).</span></span>
