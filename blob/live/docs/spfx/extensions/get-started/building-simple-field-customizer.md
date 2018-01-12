# <a name="build-your-first-field-customizer-extension"></a><span data-ttu-id="b36d9-101">Создание первого расширения для настройки полей</span><span class="sxs-lookup"><span data-stu-id="b36d9-101">Build your first Field Customizer Extension</span></span>

<span data-ttu-id="b36d9-102">Расширения — это клиентские компоненты, которые запускаются в контексте страницы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b36d9-102">Extensions are client-side components that run inside the context of a SharePoint page.</span></span> <span data-ttu-id="b36d9-103">Расширения можно развертывать в SharePoint Online, а для их создания также можно использовать современные инструменты и библиотеки JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b36d9-103">Extensions can be deployed to SharePoint Online, and you can use modern JavaScript tools and libraries to build them.</span></span>

<span data-ttu-id="b36d9-104">В этой статье описано, как создать свое первое расширение для настройки полей.</span><span class="sxs-lookup"><span data-stu-id="b36d9-104">This article describes how to create your first Field Customizer Extension.</span></span> <span data-ttu-id="b36d9-105">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=fijOzUmlXrY&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="b36d9-105">You can follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=fijOzUmlXrY&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=4wgZy5tm4yo">
<img src="../../../images/spfx-ext-youtube-tutorialfield.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="create-an-extension-project"></a><span data-ttu-id="b36d9-106">Создание проекта расширения</span><span class="sxs-lookup"><span data-stu-id="b36d9-106">Create an extension project</span></span>

1. <span data-ttu-id="b36d9-107">Создайте каталог проекта в любом расположении.</span><span class="sxs-lookup"><span data-stu-id="b36d9-107">Create a new project directory in your favorite location.</span></span>
    
    ```
    md field-extension
    ```
    
2. <span data-ttu-id="b36d9-108">Перейдите к каталогу проекта.</span><span class="sxs-lookup"><span data-stu-id="b36d9-108">Go to the project directory.</span></span>
    
    ```
    cd field-extension
    ```
    
3. <span data-ttu-id="b36d9-109">Создайте расширение HelloWorld, запустив генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b36d9-109">Create a new HelloWorld extension by running the Yeoman SharePoint Generator.</span></span>
    
    ```
    yo @microsoft/sharepoint
    ```
    
4. <span data-ttu-id="b36d9-110">Когда появится запрос, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b36d9-110">When prompted:</span></span>
    
    * <span data-ttu-id="b36d9-111">Оставьте значение по умолчанию **field-extension** для имени решения и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b36d9-111">Accept the default value of **field-extension** as your solution name, and then select Enter.</span></span>
    * <span data-ttu-id="b36d9-112">Выберите **Только SharePoint Online (новая версия)** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b36d9-112">Select **SharePoint Online only (latest)**, and select Enter.</span></span>
    * <span data-ttu-id="b36d9-113">Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b36d9-113">Select **Use the current folder**, and select Enter.</span></span>
    * <span data-ttu-id="b36d9-114">Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="b36d9-114">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span>
    * <span data-ttu-id="b36d9-115">Выберите **Расширение** в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="b36d9-115">Select **Extension** as the client-side component type to be created.</span></span> 
    * <span data-ttu-id="b36d9-116">Выберите для создаваемого расширения тип **Настройщик полей**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-116">Select **Field Customizer** as the extension type to be created.</span></span>
    
5. <span data-ttu-id="b36d9-117">Далее вам потребуется указать определенные сведения о расширении:</span><span class="sxs-lookup"><span data-stu-id="b36d9-117">The next set of prompts ask for specific information about your extension:</span></span>
     
    * <span data-ttu-id="b36d9-118">Оставьте значение по умолчанию **HelloWorld** для имени решения и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b36d9-118">Accept the default value of **HelloWorld** as your extension name, and then select Enter.</span></span>
    * <span data-ttu-id="b36d9-119">Оставьте значение по умолчанию **Описание HelloWorld** для описания решения и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b36d9-119">Accept the default value of **HelloWorld description** as your extension description, and select Enter.</span></span>
    * <span data-ttu-id="b36d9-120">Оставьте платформу по умолчанию **Не использовать платформу веб-решений на базе JavaScript** и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b36d9-120">Accept the default value of **No JavaScript Framework** as the framework selection, and select Enter.</span></span> 
    
    <br/>
    
    ![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../images/ext-field-yeoman-prompts.png)
    
    <span data-ttu-id="b36d9-122">После этого Yeoman установит необходимые зависимости и выполнит скаффолдинг файлов решения, а также расширения **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-122">At this point, Yeoman installs the required dependencies and scaffolds the solution files along with the **HelloWorld** extension.</span></span> <span data-ttu-id="b36d9-123">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b36d9-123">This might take a few minutes.</span></span> 
    
    <span data-ttu-id="b36d9-124">Когда скаффолдинг успешно закончится, появится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="b36d9-124">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>
    
    !["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../images/ext-field-yeoman-complete.png)
    
    <span data-ttu-id="b36d9-126">Сведения об устранении неполадок см. в статье [Известные проблемы](../../known-issues-and-common-questions.md).</span><span class="sxs-lookup"><span data-stu-id="b36d9-126">For information about troubleshooting any errors, see [Known issues](../../known-issues-and-common-questions.md).</span></span>

6. <span data-ttu-id="b36d9-127">После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b36d9-127">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

    ```sh
    npm shrinkwrap
    ```
    
7. <span data-ttu-id="b36d9-128">Введите в консоли приведенную ниже команду, чтобы запустить Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b36d9-128">Type the following into the console to start Visual Studio Code.</span></span>
    
    ```
    code .
    ```
    
    > [!NOTE] 
    > <span data-ttu-id="b36d9-129">Так как клиентское решение SharePoint основано на HTML и TypeScript, для разработки расширения можно использовать любой редактор кода, поддерживающий клиентскую разработку.</span><span class="sxs-lookup"><span data-stu-id="b36d9-129">Note: Because the SharePoint client-side solution is HTML/TypeScript based, you can use any code editor that supports client-side development to build your extension.</span></span>

    <span data-ttu-id="b36d9-130">Обратите внимание, что стандартная структура решения похожа на структуру клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="b36d9-130">Note how the default solution structure looks like the solution structure of client-side web parts.</span></span> <span data-ttu-id="b36d9-131">Это основная структура решения SharePoint Framework, ее параметры конфигурации схожи для всех типов решений.</span><span class="sxs-lookup"><span data-stu-id="b36d9-131">This is the basic SharePoint Framework solution structure, with similar configuration options across all solution types.</span></span>

    ![Решение SharePoint Framework, открытое после первоначального скаффолдинга](../../../images/ext-field-vscode-solution-structure.png)

8. <span data-ttu-id="b36d9-133">Откройте файл **HelloWorldFieldCustomizer.manifest.json** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-133">Open **HelloWorldFieldCustomizer.manifest.json** in the **src\extensions\helloWorld** folder.</span></span>

    <span data-ttu-id="b36d9-134">Этот файл определяет тип расширения и уникальный идентификатор `id` для расширения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-134">This file defines your extension type and a unique identifier `id` for your extension.</span></span> <span data-ttu-id="b36d9-135">Этот идентификатор пригодится позже при отладке и развертывании расширения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b36d9-135">You’ll need this unique identifier later when debugging and deploying your extension to SharePoint.</span></span>

    ![Содержимое манифеста настройщика приложений в формате JSON](../../../images/ext-field-vscode-manifest.png)

## <a name="code-your-field-customizer"></a><span data-ttu-id="b36d9-137">Написание кода настройщика полей</span><span class="sxs-lookup"><span data-stu-id="b36d9-137">Code your Field Customizer</span></span> 

<span data-ttu-id="b36d9-138">Откройте файл **HelloWorldFieldCustomizer.ts** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-138">Open the **HelloWorldFieldCustomizer.ts** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="b36d9-139">Обратите внимание, что базовый класс для настройщика полей импортируется из пакета **sp-listview-extensibility**, который содержит код платформы SharePoint Framework, необходимый для настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="b36d9-139">Notice that the base class for the Field Customizer is imported from the **sp-listview-extensibility** package, which contains SharePoint Framework code required by the Field Customizer.</span></span>

```ts
import { Log } from '@microsoft/sp-core-library';
import { override } from '@microsoft/decorators';
import {
  BaseFieldCustomizer,
  IFieldCustomizerCellEventParameters
} from '@microsoft/sp-listview-extensibility';
```

<span data-ttu-id="b36d9-140">Логика настройщика полей содержится в методах **OnInit()**, **onRenderCell()** и **onDisposeCell()**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-140">The logic for your Field Customizer is contained in the **OnInit()**, **onRenderCell()**, and **onDisposeCell()** methods.</span></span>

* <span data-ttu-id="b36d9-p106">В методе **onInit()** выполняется вся настройка, необходимая для расширения. Это событие происходит после назначения `this.context` и `this.properties`, но до того, как модель DOM будет готова. Как и в случае с веб-частями, `onInit()` возвращает обещание, с помощью которого можно выполнять асинхронные операции. `onRenderCell()` не будет вызываться, пока обещание не будет разрешено. Если вам это не нужно, просто верните `Promise.resolve<void>();`.</span><span class="sxs-lookup"><span data-stu-id="b36d9-p106">**onInit()** is where you should perform any setup needed for your extension. This event occurs after `this.context` and `this.properties` are assigned, but before the page DOM is ready. As with web parts, `onInit()` returns a promise that you can use to perform asynchronous operations; `onRenderCell()` will not be called until your promise has resolved. If you don’t need that, simply return `Promise.resolve<void>();`.</span></span>
* <span data-ttu-id="b36d9-145">**onRenderCell()** происходит при отображении каждой ячейки.</span><span class="sxs-lookup"><span data-stu-id="b36d9-145">**onRenderCell()** occurs when each cell is rendered.</span></span> <span data-ttu-id="b36d9-146">Он предоставляет `event.domElement` HTML-элемент, где код может записать его содержимое.</span><span class="sxs-lookup"><span data-stu-id="b36d9-146">It provides an `event.domElement` HTML element where your code can write its content.</span></span>
* <span data-ttu-id="b36d9-147">**onDisposeCell()** происходит непосредственно удалением `event.cellDiv`.</span><span class="sxs-lookup"><span data-stu-id="b36d9-147">**onDisposeCell()** occurs immediately before the `event.cellDiv` is deleted.</span></span> <span data-ttu-id="b36d9-148">Его можно использовать для освобождения ресурсов, которые были выделены во время отображения поля.</span><span class="sxs-lookup"><span data-stu-id="b36d9-148">It can be used to free any resources that were allocated during field rendering.</span></span> <span data-ttu-id="b36d9-149">Например, если подключить `onRenderCell()` к элементу Reach, для его освобождения необходимо использовать `onDisposeCell()`, в противном случае произойдет утечка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b36d9-149">For example, if `onRenderCell()` mounted a React element, `onDisposeCell()` must be used to free it; otherwise, a resource leak would occur.</span></span> 

<span data-ttu-id="b36d9-150">Ниже представлено содержимое методов **onRenderCell()** и **onDisposeCell()** в решении по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b36d9-150">The following are the contents of **onRenderCell()** and **onDisposeCell()** in the default solution:</span></span>

```ts
@override
  public onRenderCell(event: IFieldCustomizerCellEventParameters): void {
    // Use this method to perform your custom cell rendering.
    const text: string = `${this.properties.sampleText}: ${event.fieldValue}`;

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

## <a name="debug-your-field-customizer-using-gulp-serve-and-query-string-parameters"></a><span data-ttu-id="b36d9-151">Отладка настройщика полей с помощью gulp serve и параметров строки запроса</span><span class="sxs-lookup"><span data-stu-id="b36d9-151">Debug your Field Customizer using gulp serve and query string parameters</span></span>
<span data-ttu-id="b36d9-152">В настоящее время использование локального рабочего места для проверки расширений SharePoint Framework невозможно.</span><span class="sxs-lookup"><span data-stu-id="b36d9-152">You cannot currently use the local workbench to test SharePoint Framework Extensions.</span></span> <span data-ttu-id="b36d9-153">Их необходимо проверять и разрабатывать с использованием действующего сайта SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b36d9-153">You'll need to test and develop them directly against a live SharePoint Online site.</span></span> <span data-ttu-id="b36d9-154">Для этого вам не нужно развертывать модификацию каталога приложений, что делает процесс отладки простым и эффективным.</span><span class="sxs-lookup"><span data-stu-id="b36d9-154">You don't have to deploy your customization to the App Catalog to do this, which makes the debugging experience simple and efficient.</span></span>

1. <span data-ttu-id="b36d9-155">Для начала скомпилируйте код и разместите скомпилированные файлы с локального компьютера, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b36d9-155">Compile your code and host the compiled files from the local machine by running this command:</span></span>
    
    ```
    gulp serve --nobrowser
    ```
    
    <span data-ttu-id="b36d9-156">Так как запускать локальную систему разработки не требуется (невозможно выполнять отладку расширений локально), используется параметр `--nobrowser`.</span><span class="sxs-lookup"><span data-stu-id="b36d9-156">You use the `--nobrowser` option because you don't need to launch the local workbench, since you can't debug extensions locally.</span></span>

    <span data-ttu-id="b36d9-157">Когда компиляция кода завершится без ошибок, полученный манифест будет доступен по адресу http://localhost:4321.</span><span class="sxs-lookup"><span data-stu-id="b36d9-157">When the code compiles without errors, it will serve the resulting manifest from https://localhost:4321.</span></span>

    ![gulp serve](../../../images/ext-field-gulp-serve.png)

2. <span data-ttu-id="b36d9-159">Для тестирования расширения перейдите к сайту в клиенте SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b36d9-159">To test your extension, go to a site in your SharePoint Online tenant.</span></span>

3. <span data-ttu-id="b36d9-160">Откройте страницу **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-160">Move to the **Site Contents** page.</span></span>

4. <span data-ttu-id="b36d9-161">На панели инструментов выберите **Создать**, а затем выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-161">On the toolbar, select **New**, and then select **List**.</span></span>
    
    ![Создание списка](../../../images/ext-field-create-new-list.png)
    
5. <span data-ttu-id="b36d9-163">Создайте список под названием **Заказы** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-163">Create a new list named **Orders**, and then select **Create**.</span></span>
    
    ![Создание списка "Заказы"](../../../images/ext-field-create-new-list-order.png)
    
6. <span data-ttu-id="b36d9-165">Нажмите значок **плюс** и выберите **Число**, чтобы создать числовое поле для списка.</span><span class="sxs-lookup"><span data-stu-id="b36d9-165">Select the **plus** sign, and then select **Number** to create a new Number field for the list.</span></span>
    
    ![Создание числового поля](../../../images/ext-field-new-number-field.png)
    
7. <span data-ttu-id="b36d9-167">Для имени поля выберите **Процент**, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-167">Set the name of the field to **Percent**, and then select **Save**.</span></span>
    
    ![Создание поля "Процент"](../../../images/ext-field-new-number-field-percent.png)
    
8. <span data-ttu-id="b36d9-p110">Добавьте несколько элементов с различными числами в процентное поле. Позже мы изменим отрисовку, чтобы разные числа отображались по-разному в соответствии с вашей реализацией.</span><span class="sxs-lookup"><span data-stu-id="b36d9-p110">Add a few items with different numbers in the percent field. We'll modify the rendering later in this tutorial, so the different numbers will be presented differently based on your custom implementation.</span></span>

    ![Создание элементов в новом списке с разными значениями в поле "Процент"](../../../images/ext-field-create-items-to-list.png)

    <span data-ttu-id="b36d9-172">Так как настройщик полей размещается в localhost и запущен, доступны определенные параметры запроса отладки для выполнения кода в новом списке.</span><span class="sxs-lookup"><span data-stu-id="b36d9-172">Because our Field Customizer is still hosted in localhost and is running, we can use specific debug query parameters to execute the code in the newly created list.</span></span>

9. <span data-ttu-id="b36d9-173">Добавьте в URL-адрес приведенные ниже параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="b36d9-173">Append the following query string parameters to the URL.</span></span> <span data-ttu-id="b36d9-174">Обратите внимание, что вам потребуется обновить идентификатор в соответствии с идентификатором расширения, указанным в файле **HelloWorldFieldCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-174">Notice that you will need to update the ID to match your own extension identifier available from the **HelloWorldFieldCustomizer.manifest.json** file.</span></span> <span data-ttu-id="b36d9-175">Дополнительные сведения см. в статье [подробные сведения о URL-адрес запроса параметров](#more-details-about-the-url-query-parameters).</span><span class="sxs-lookup"><span data-stu-id="b36d9-175">For more information, see [More details about the URL query parameters](#more-details-about-the-url-query-parameters).</span></span> 

    ```
    ?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Percent":{"id":"45a1d299-990d-4917-ba62-7cb67158be16","properties":{"sampleText":"Hello!"}}}
    ```
    
    <br/>

    <span data-ttu-id="b36d9-176">Полный URL-адрес должен выглядеть примерно так, как показано ниже, но соответствовать URL-адресу и расположению нового списка:</span><span class="sxs-lookup"><span data-stu-id="b36d9-176">The full URL should look similar to the following, depending on your tenant URL and the location of the newly created list:</span></span>
    
    <br/>
    
    ```
    contoso.sharepoint.com/Lists/Orders/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&fieldCustomizers={"Percent":{"id":"45a1d299-990d-4917-ba62-7cb67158be16","properties":{"sampleText":"Hello!"}}}
    ```
    
10. <span data-ttu-id="b36d9-177">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="b36d9-177">Accept the loading of debug manifests by selecting **Load debug scripts** when prompted.</span></span>

    ![Согласие на загрузку скриптов отладки](../../../images/ext-field-accept-debug-scripts.png)

    <span data-ttu-id="b36d9-179">Обратите внимание, что значения процентов теперь отображаются с дополнительной строкой префикса как `Hello!: `, которая указана как свойство для настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="b36d9-179">Notice how the Percent values are now presented with an additional prefix string as `Hello!: `, which is provided as a property for the Field Customizer.</span></span>

    ![Представление списка с помощью настройщика полей для поля процентов](../../../images/ext-field-default-customizer-output.png)


### <a name="more-details-about-the-url-query-parameters"></a><span data-ttu-id="b36d9-181">Подробнее о параметрах запроса URL</span><span class="sxs-lookup"><span data-stu-id="b36d9-181">More details about the URL query parameters</span></span>

- <span data-ttu-id="b36d9-182">**loadSPFX=true** гарантирует загрузку SharePoint Framework на странице.</span><span class="sxs-lookup"><span data-stu-id="b36d9-182">**loadSPFX=true** ensures that the SharePoint Framework is loaded on the page.</span></span> <span data-ttu-id="b36d9-183">Из соображений производительности платформа обычно загружается, только если зарегистрировано хотя бы одно расширение.</span><span class="sxs-lookup"><span data-stu-id="b36d9-183">For performance reasons, the framework is not normally loaded unless at least one extension is registered.</span></span> <span data-ttu-id="b36d9-184">Так как компоненты еще не зарегистрированы, платформу нужно загрузить напрямую.</span><span class="sxs-lookup"><span data-stu-id="b36d9-184">Because no components are registered yet, we must explicitly load the framework.</span></span>
- <span data-ttu-id="b36d9-185">**debugManifestsFile** указывает, что нужно загрузить компоненты SPFx, предоставляемые локально.</span><span class="sxs-lookup"><span data-stu-id="b36d9-185">**debugManifestsFile** specifies that you want to load SPFx components that are locally served.</span></span> <span data-ttu-id="b36d9-186">Загрузчик ищет компоненты только в каталоге приложений (для развернутого решения) и на сервере манифестов SharePoint (для системных библиотек).</span><span class="sxs-lookup"><span data-stu-id="b36d9-186">The loader only looks for components in the App Catalog (for your deployed solution) and the SharePoint manifest server (for the system libraries).</span></span>
- <span data-ttu-id="b36d9-187">**fieldCustomizers** указывает поля в списке, отображение которых управляется настройщиком полей.</span><span class="sxs-lookup"><span data-stu-id="b36d9-187">**fieldCustomizers** indicates which fields in your list should have their rendering controlled by the Field Customizer.</span></span> <span data-ttu-id="b36d9-188">Параметр ID задает GUID расширения, который будет использоваться для управления отображением поля.</span><span class="sxs-lookup"><span data-stu-id="b36d9-188">The ID parameter specifies the GUID of the extension that should be used to control the rendering of the field.</span></span> <span data-ttu-id="b36d9-189">Параметр properties — это необязательным текстовая строка, содержащая объект JSON, который будет десериализован в `this.properties` для расширения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-189">The properties parameter is an optional text string containing a JSON object that will be deserialized into `this.properties` for your extension.</span></span>
    - <span data-ttu-id="b36d9-190">**Key:** в качестве ключа используйте внутреннее имя поля.</span><span class="sxs-lookup"><span data-stu-id="b36d9-190">**Key**: Use the internal name of the field as the key.</span></span>
    - <span data-ttu-id="b36d9-191">**Id:** GUID расширения для настройки полей, связанный с этим полем.</span><span class="sxs-lookup"><span data-stu-id="b36d9-191">**Id**: The GUID of the Field Customizer extension associated with this field.</span></span>
    - <span data-ttu-id="b36d9-192">**Properties:** значения свойств, определенные в расширении.</span><span class="sxs-lookup"><span data-stu-id="b36d9-192">**Properties**: The property values defined in the extension.</span></span> <span data-ttu-id="b36d9-193">В этом примере `sampleText` является свойством, определенным с помощью расширения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-193">In this example, `sampleText` is a property defined by the extension.</span></span>

<br/>

## <a name="enhance-the-field-customizer-rendering"></a><span data-ttu-id="b36d9-194">Улучшение отображения настройщика полей</span><span class="sxs-lookup"><span data-stu-id="b36d9-194">Enhance the Field Customizer rendering</span></span>
<span data-ttu-id="b36d9-195">Теперь, когда мы успешно протестировали встроенную отправную точку для создания настройщика полей, пришло время немного изменить логику для более аккуратной отрисовки значения поля.</span><span class="sxs-lookup"><span data-stu-id="b36d9-195">Now that we have successfully tested the out-of-the-box starting point of the Field Customizer, let's modify the logic slightly to have a more polished rendering of the field value.</span></span> 

1. <span data-ttu-id="b36d9-196">Откройте файл **HelloWorld.module.scss** в папке **src\extensions\helloWorld** и измените определение стиля, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b36d9-196">Open the **HelloWorld.module.scss** file in the **src\extensions\helloWorld** folder, and update the styling definition as follows.</span></span>

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
    
2. <span data-ttu-id="b36d9-197">Откройте файл **HelloWorldFieldCustomizer.ts** в папке **src\extensions\helloWorld** и измените метод **onRednerCell**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b36d9-197">Open the **HelloWorldFieldCustomizer.ts** file in the **src\extensions\helloWorld** folder, and update the **onRednerCell** method as follows.</span></span>

    ```ts
        @override
        public onRenderCell(event: IFieldCustomizerCellEventParameters): void {

            event.domElement.classList.add(styles.cell);
            event.domElement.innerHTML = `
                    <div class='${styles.HelloWorld}'>
                        <div class='${styles.full}'>
                        <div style='width: ${event.fieldValue}px; background:#0094ff; color:#c0c0c0'>
                            &nbsp; ${event.fieldValue}
                        </div>
                        </div>
                    </div>`;
        }
    ```

3. <span data-ttu-id="b36d9-198">В окне консоли не должно быть исключений.</span><span class="sxs-lookup"><span data-stu-id="b36d9-198">In your console window, ensure that you do not have any exceptions.</span></span> <span data-ttu-id="b36d9-199">Если в *localhost* нет запущенного решения, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b36d9-199">If you do not have the solution running in *localhost*, execute the following command:</span></span>

    ```
    gulp serve --nobrowser
    ```

4. <span data-ttu-id="b36d9-200">Вернитесь к созданному ранее списку и используйте тот же параметр запроса, что и раньше, с полем `Percent` и `ID`, замененным на идентификатор расширения, который указан в файле **HelloWorldFieldCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-200">In your previously created list, use the same query parameter as used previously, with the field being `Percent` and the `ID` being updated to your extension identifier available from the **HelloWorldFieldCustomizer.manifest.json** file.</span></span>

5. <span data-ttu-id="b36d9-201">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="b36d9-201">Accept the loading of debug manifests by selecting **Load debug scripts** when prompted.</span></span>

    ![Согласие на загрузку скриптов отладки](../../../images/ext-field-accept-debug-scripts.png)

    <span data-ttu-id="b36d9-203">Обратите внимание на то, как мы изменили стиль отображения поля, полностью.</span><span class="sxs-lookup"><span data-stu-id="b36d9-203">Note how we changed the field rendering style completely.</span></span> <span data-ttu-id="b36d9-204">Значение поля обозначается с помощью графического представления значения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-204">The field value is indicated by using a graphical representation of the value.</span></span>

    ![Графическое представление процента](../../../images/ext-field-percent-field-graphic.png)

## <a name="add-the-field-definition-to-the-solution-package-for-deployment"></a><span data-ttu-id="b36d9-206">Добавление определения поля в пакет решения для развертывания</span><span class="sxs-lookup"><span data-stu-id="b36d9-206">Add the field definition to the solution package for deployment</span></span>
<span data-ttu-id="b36d9-207">Надлежащим образом протестировав решение в режиме отладки, можно упаковать его для автоматического развертывания в составе пакета решения, развертываемого на сайтах.</span><span class="sxs-lookup"><span data-stu-id="b36d9-207">Now that we have tested our solution properly in debug mode, we can package this to be deployed automatically as part of the solution package deployed to the sites.</span></span> 

1. <span data-ttu-id="b36d9-208">Установите пакет решения на нужном сайте, чтобы манифест расширения попал в список разрешенных для запуска.</span><span class="sxs-lookup"><span data-stu-id="b36d9-208">Install the solution package to the site where it should be installed, so that the extension manifest is white listed for execution.</span></span>

2. <span data-ttu-id="b36d9-209">Связывание настройщика поля с существующим поле на сайте.</span><span class="sxs-lookup"><span data-stu-id="b36d9-209">Associate the Field Customizer to an existing field in the site.</span></span> <span data-ttu-id="b36d9-210">Это можно сделать путем программирования (CSOM/REST) или с помощью функции платформы внутри пакета решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b36d9-210">You can do this programmatically (CSOM/REST) or by using the feature framework inside of the SharePoint Framework solution package.</span></span> <span data-ttu-id="b36d9-211">Вам нужно связать следующие свойства в объекте `SPField` на уровне сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="b36d9-211">You'll need to associate the following properties in the `SPField` object at the site or list level.</span></span>
    - <span data-ttu-id="b36d9-212">**ClientSiteComponentId:** идентификатор (GUID) настройщика приложений, установленный в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="b36d9-212">**ClientSiteComponentId** is the identifier (GUID) of the Field Customizer, which has been installed in the App Catalog.</span></span>
    - <span data-ttu-id="b36d9-213">**ClientSideComponentProperties:** необязательный параметр, с помощью которого можно предоставлять свойства для экземпляра настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="b36d9-213">**ClientSideComponentProperties** is an optional parameter, which can be used to provide properties for the Field Customizer instance.</span></span>

    <span data-ttu-id="b36d9-214">Обратите внимание, что вы можете задать требования для добавления на сайт решения, содержащего расширение, с помощью параметра `skipFeatureDeployment` в **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-214">Note that you can control the requirement to add a solution containing your extension to the site by using the `skipFeatureDeployment` setting in **package-solution.json**.</span></span> <span data-ttu-id="b36d9-215">Хотя вы можете и не требовать установки решения на сайте, необходимо связать **ClientSideComponentId** с отдельными объектами, чтобы расширение было видимым.</span><span class="sxs-lookup"><span data-stu-id="b36d9-215">Even though you would not require the solution to be installed on the site, you'd need to associate **ClientSideComponentId** to specific objects for the extension to be visible.</span></span>

    <span data-ttu-id="b36d9-216">На следующих этапах мы просмотрим автоматически созданное определение поля по умолчанию, которое будет использоваться при автоматическом развертывании необходимых конфигураций при установке пакета решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="b36d9-216">In the following steps, we'll review the default field definition, which was automatically created and will then be used to automatically deploy needed configurations when the solution package is installed on a site.</span></span>

3. <span data-ttu-id="b36d9-217">Вернитесь к решению в Visual Studio Code (или другом редакторе, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="b36d9-217">Return to your solution in Visual Studio Code (or to your preferred editor).</span></span>

4. <span data-ttu-id="b36d9-218">Разверните папку **sharepoint** и вложенную папку **assets** в корне решения для просмотра существующего файла **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-218">Extend the **sharepoint** folder and **assets** subfolder in the root of the solution to see the existing **elements.xml** file.</span></span> 
    
    ![Папка assets в структуре решения](../../../images/ext-field-assets-folder.png)

<br/>

### <a name="review-the-elementsxml-file"></a><span data-ttu-id="b36d9-220">Просмотр файла elements.xml</span><span class="sxs-lookup"><span data-stu-id="b36d9-220">Review the elements.xml file</span></span> 

<span data-ttu-id="b36d9-221">Откройте файл **elements.xml** в папке **sharepoint\assets**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-221">Open the **elements.xml** file inside the **sharepoint\assets** folder.</span></span>

<span data-ttu-id="b36d9-222">Запишите следующую структуру XML в файл **elements.xml**:</span><span class="sxs-lookup"><span data-stu-id="b36d9-222">Note the following XML structure in **elements.xml**.</span></span>  <span data-ttu-id="b36d9-223">Свойство **ClientSideComponentId** автоматически изменено в соответствии с уникальным идентификатором вашего настройщика полей в файле **HelloWorldFieldCustomizer.manifest.json** папки **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-223">The **ClientSideComponentId** property has been automatically updated to the unique ID of your Field Customizer available in the **HelloWorldFieldCustomizer.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

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

<br/>

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="b36d9-224">Проверка учета определений в конвейере сборки</span><span class="sxs-lookup"><span data-stu-id="b36d9-224">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="b36d9-p121">Откройте файл **package-solution.json** в папке **config**. В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="b36d9-p121">Open **package-solution.json** from the **config** folder. The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

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

<span data-ttu-id="b36d9-227">Чтобы убедиться, что файл **element.xml** учитывается при упаковке решения, требуется скаффолдинг по умолчанию для конфигурации, чтобы определить платформу функции для пакета решения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-227">To ensure that the **element.xml** file is taken into account while the solution is being packaged, default scaffolding added needed configuration to define a feature framework feature definition for the solution package.</span></span>


## <a name="deploy-the-field-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="b36d9-228">Развертывание поля в SharePoint Online и размещение кода JavaScript с локального узла</span><span class="sxs-lookup"><span data-stu-id="b36d9-228">Deploy the field to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="b36d9-229">Теперь все готово для развертывания решения на сайте SharePoint и автоматического добавления связывания в поле.</span><span class="sxs-lookup"><span data-stu-id="b36d9-229">Now you are ready to deploy the solution to a SharePoint site and get the field association automatically included in a field.</span></span> 

1. <span data-ttu-id="b36d9-230">Чтобы упаковать клиентское решение, содержащее расширение, и получить базовую структуру, готовую к упаковке, введите в окне консоли приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="b36d9-230">In the console window, enter the following command to package your client-side solution that contains the extension so that we get the basic structure ready for packaging:</span></span>

    ```
    gulp bundle
    ```

2. <span data-ttu-id="b36d9-231">Затем выполните следующую команду, чтобы создать пакет решения:</span><span class="sxs-lookup"><span data-stu-id="b36d9-231">Execute the following command so that the solution package is created:</span></span>

    ```
    gulp package-solution
    ```

    <span data-ttu-id="b36d9-232">Эта команда создаст пакет в папке **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="b36d9-232">The command creates the package in the **sharepoint/solution** folder:</span></span>

    ```
    field-extension.sppkg
    ```

3. <span data-ttu-id="b36d9-233">Далее вам потребуется развернуть созданный пакет в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="b36d9-233">You now need to deploy the package that was generated to the App Catalog.</span></span> <span data-ttu-id="b36d9-234">Для этого перейдите к **каталогу приложений** клиента и откройте библиотеку **Приложения для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-234">To do this, go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

4. <span data-ttu-id="b36d9-235">Отправьте или перетащите файл `field-extension.sppkg` из папки **sharepoint/solution** в каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="b36d9-235">Upload or drag-and-drop the `field-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog.</span></span> <span data-ttu-id="b36d9-236">В SharePoint откроется диалоговое окно с запросом на подтверждение доверия клиентскому решению.</span><span class="sxs-lookup"><span data-stu-id="b36d9-236">SharePoint displays a dialog and asks you to trust the client-side solution.</span></span>

    <span data-ttu-id="b36d9-237">Обратите внимание на то, что мы не обновляли URL-адреса для размещения решения в этом развертывании, поэтому URL-адрес по-прежнему указывает на https://localhost:4321.</span><span class="sxs-lookup"><span data-stu-id="b36d9-237">Note that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to https://localhost:4321.</span></span> 
    
5. <span data-ttu-id="b36d9-238">Нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-238">Select the **Deploy** button.</span></span>

    ![Диалоговое окно развертывания](../../../images/ext-field-sppkg-deploy-trust.png)

6. <span data-ttu-id="b36d9-p124">Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-p124">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

7. <span data-ttu-id="b36d9-242">Нажмите значок шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**, чтобы перейти к странице "Приложения".</span><span class="sxs-lookup"><span data-stu-id="b36d9-242">Select the gears icon on the top navigation bar on the right, and then select **Add an app** to go to your Apps page.</span></span>

8. <span data-ttu-id="b36d9-243">В поле **Поиск** введите **field** и нажмите клавишу ВВОД, чтобы отфильтровать приложения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-243">In the **Search** box, enter **field**, and then select Enter to filter your apps.</span></span>

    ![Установка настройщика полей на сайте](../../../images/ext-field-install-solution-to-site.png)

9. <span data-ttu-id="b36d9-245">Выберите приложение **field-extension-client-side-solution**, чтобы установить решение на сайте.</span><span class="sxs-lookup"><span data-stu-id="b36d9-245">Select the **field-extension-client-side-solution** app to install the solution on the site.</span></span> <span data-ttu-id="b36d9-246">По завершении установки обновите страницу, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-246">After the installation is complete, refresh the page by selecting **F5**.</span></span>

10. <span data-ttu-id="b36d9-247">После установки решения нажмите кнопку **Создать** на панели инструментов страницы **Содержимое сайта** и выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-247">When the solution has been installed, select **New** from the toolbar on the **Site Contents** page, and then select **List**.</span></span>

    ![Создание списка](../../../images/ext-field-create-new-list.png)

11. <span data-ttu-id="b36d9-249">Создайте список под названием **Счета**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-249">Create a list named **Invoices**.</span></span>

12. <span data-ttu-id="b36d9-250">Создав список, на странице **одержимое сайта** выберите **Параметры** из меню нового списка.</span><span class="sxs-lookup"><span data-stu-id="b36d9-250">When the new list is created, on the **Site Contents** page, select **Settings** from the menu of the newly created list.</span></span>

    ![Параметры нового списка](../../../images/ext-field-list-settings.png)

13. <span data-ttu-id="b36d9-252">В разделе **Столбцы** выберите **Добавить из существующих столбцов сайта**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-252">Under **Columns**, select **Add from existing site columns**.</span></span>

14. <span data-ttu-id="b36d9-253">В группе **Столбцы SPFx** выберите поле **Процент**, подготовленное с помощью пакета решения, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-253">Under the **SPFx Columns** group, select the **Percentage** field that was provisioned from the solution package, and then select **OK**.</span></span>

    ![Добавление поля "Процент" в список](../../../images/ext-field-add-field-to-list.png)

15. <span data-ttu-id="b36d9-255">На консоли убедитесь, что решение запущено.</span><span class="sxs-lookup"><span data-stu-id="b36d9-255">On your console, ensure that the solution is running.</span></span> <span data-ttu-id="b36d9-256">Если оно не работает, выполните следующую команду в папке решения:</span><span class="sxs-lookup"><span data-stu-id="b36d9-256">If it's not running, execute the following command in the solution folder:</span></span>

    ```
    gulp serve --nobrowser
    ```

16. <span data-ttu-id="b36d9-257">Выберите только что созданный список **Счета**.</span><span class="sxs-lookup"><span data-stu-id="b36d9-257">Go to the newly created **Invoices** list.</span></span> <span data-ttu-id="b36d9-258">Добавьте в столбец "Процент" несколько новых элементов с разными значениями, чтобы увидеть, как поле отрисовывается без параметров запроса отладки.</span><span class="sxs-lookup"><span data-stu-id="b36d9-258">Add a few items to the list with different values in the Percentage column to determine how the field is rendering without the debug query parameters.</span></span>

![Отрисовка поля без параметров запроса отладки](../../../images/ext-field-render-field-without-debug.png)

<span data-ttu-id="b36d9-260">В этом случае код JavaScript по-прежнему размещается в localhost, но вы также можете переместить ресурсы в любую сеть CDN и обновить URL-адрес, чтобы ресурсы JavaScript можно было загружать не только из localhost.</span><span class="sxs-lookup"><span data-stu-id="b36d9-260">In this case, we continued to host the JavaScript from the localhost, but you could just as well relocate the assets to any CDN and update the URL to enable the loading of the JavaScript assets outside of the localhost as well.</span></span>

<span data-ttu-id="b36d9-261">Публикация приложения не зависит от типа расширения.</span><span class="sxs-lookup"><span data-stu-id="b36d9-261">The process for publishing your app is identical among the different extension types.</span></span> <span data-ttu-id="b36d9-262">Вы можете обновить ресурсы для размещения в сети доставки содержимого, используя инструкции из [этой статьи](./hosting-extension-from-office365-cdn.md).</span><span class="sxs-lookup"><span data-stu-id="b36d9-262">You can use the following publishing steps to update the assets to be hosted from a CDN: [Host extension from Office 365 CDN](./hosting-extension-from-office365-cdn.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b36d9-263">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint в [репозитории sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="b36d9-263">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="b36d9-264">Заранее благодарим за ваш вклад.</span><span class="sxs-lookup"><span data-stu-id="b36d9-264">Thanks for your input advance.</span></span>