# <a name="use-page-placeholders-from-application-customizer-hello-world-part-2"></a><span data-ttu-id="4dd07-101">Использование заполнителей страниц из настройщика приложений (Hello World, часть 2)</span><span class="sxs-lookup"><span data-stu-id="4dd07-101">Use page placeholders from Application Customizer (Hello World part 2)</span></span>

<span data-ttu-id="4dd07-102">Настройщики приложений обеспечивают доступ к известным местам на страницах SharePoint, которые можно менять в соответствии с организационными и функциональными требованиями.</span><span class="sxs-lookup"><span data-stu-id="4dd07-102">Application Customizers provide access to well-known locations on SharePoint pages that you can modify based on your business and functional requirements.</span></span> <span data-ttu-id="4dd07-103">Например, вы можете создать динамические верхний и нижний колонтитулы, которые отображаются на всех страницах в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4dd07-103">For example, you can create dynamic header and footer experiences that render across all the pages in SharePoint Online.</span></span> 

<span data-ttu-id="4dd07-104">Эта модель сопоставима с использованием коллекции **UserCustomAction** в объекте **Site** или **Web** для изменения страницы с помощью пользовательского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4dd07-104">This model is similar to using a **UserCustomAction** collection in a **Site** or **Web** object to modify the page experience via custom JavaScript.</span></span> <span data-ttu-id="4dd07-105">Основное отличие или преимущество расширений SharePoint Framework (SPFx) в том, что элементы страницы не меняются при изменении структуры HTML/DOM в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4dd07-105">The key difference or advantage with SharePoint Framework (SPFx) Extensions is that your page elements won't change if changes are made to the HTML/DOM structure in SharePoint Online.</span></span>

<span data-ttu-id="4dd07-106">В этой статье описано, как сделать так, чтобы [расширение Hello World](./build-a-hello-world-extension.md) использовало заполнители страниц.</span><span class="sxs-lookup"><span data-stu-id="4dd07-106">This article describes how to extend your [Hello World extension](./build-a-hello-world-extension.md) to take advantage of page placeholders.</span></span> <span data-ttu-id="4dd07-107">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="4dd07-107">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span>

<a href="https://www.youtube.com/watch?v=3LXuYBaJ1Lc">
<img src="../../../images/spfx-ext-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="get-access-to-page-placeholders"></a><span data-ttu-id="4dd07-108">Получение доступа к заполнителям страниц</span><span class="sxs-lookup"><span data-stu-id="4dd07-108">Get access to page placeholders</span></span>

<span data-ttu-id="4dd07-109">Расширения настройщика приложений поддерживаются в областях `Site`, `Web` и `List`.</span><span class="sxs-lookup"><span data-stu-id="4dd07-109">Application Customizer extensions are supported with `Site`, `Web`, and `List` scopes.</span></span> <span data-ttu-id="4dd07-110">Вы можете контролировать место и способ регистрации настройщика приложений в клиенте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4dd07-110">You can control the scope by deciding where or how the Application Customizer will be registered in your SharePoint tenant.</span></span> <span data-ttu-id="4dd07-111">Когда настройщик приложений существует в области и отображается, вы можете использовать следующий метод, чтобы получить доступ к заполнителю.</span><span class="sxs-lookup"><span data-stu-id="4dd07-111">When the Application Customizer exists in the scope and is being rendered, you can use the following method to get access to the placeholder.</span></span> 

```ts
    // Handling the Bottom placeholder
    if (!this._bottomPlaceholder) {
      this._bottomPlaceholder =
        this.context.placeholderProvider.tryCreateContent(
          PlaceholderName.Bottom,
          { onDispose: this._onDispose });
    ...
    }
```

<span data-ttu-id="4dd07-112">После этого вы полностью контролируете, какие элементы показываются конечному пользователю.</span><span class="sxs-lookup"><span data-stu-id="4dd07-112">After you get the placeholder object, you have full control over what will be presented to the end user.</span></span>

<span data-ttu-id="4dd07-113">Обратите внимание, что вы запрашиваете известный заполнитель, используя соответствующий известный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4dd07-113">Notice that you're requesting a well-known placeholder by using the corresponding well-known identifier.</span></span> <span data-ttu-id="4dd07-114">В этом случае код получает доступ к нижнему колонтитулу страницы, используя идентификатор `Bottom`.</span><span class="sxs-lookup"><span data-stu-id="4dd07-114">In this case, the code is accessing the footer section of the page using the `Bottom` identifier.</span></span> 

<span data-ttu-id="4dd07-115">Позже вы измените настройщик приложений Hello World, чтобы получить доступ к заполнителям и изменить их, добавив пользовательские элементы HTML.</span><span class="sxs-lookup"><span data-stu-id="4dd07-115">In the following steps, you'll modify the Hello World Application Customizer to access and modify placeholders by adding custom HTML elements.</span></span>

1. <span data-ttu-id="4dd07-116">В Visual Studio Code (или другой интегрированной среде разработки) откройте файл **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**</span><span class="sxs-lookup"><span data-stu-id="4dd07-116">In Visual Studio Code (or your preferred IDE), open **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**</span></span>

2. <span data-ttu-id="4dd07-117">Добавьте объекты `PlaceholderContent` и `PlaceholderName` к оператору импорта из `@microsoft/sp-application-base`, изменив его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4dd07-117">Add the `PlaceholderContent` and `PlaceholderName` to the import from `@microsoft/sp-application-base` by updating the import statement as follows:</span></span>

    ```ts
    import {
      BaseApplicationCustomizer, 
      PlaceholderContent,
      PlaceholderName
    } from '@microsoft/sp-application-base';
    ```
    
      <span data-ttu-id="4dd07-118">Кроме того, добавьте следующие операторы импорта после кода импорта `strings` в начале файла:</span><span class="sxs-lookup"><span data-stu-id="4dd07-118">Also add the following import statements after the `strings` import at the top of the file:</span></span>

    ```ts
    import styles from './AppCustomizer.module.scss';
    import { escape } from '@microsoft/sp-lodash-subset'; 
    ```

    <span data-ttu-id="4dd07-119">Для экранирования свойств настройщика приложений используется функция `escape`.</span><span class="sxs-lookup"><span data-stu-id="4dd07-119">You use `escape` to escape Application Customizer properties.</span></span> <span data-ttu-id="4dd07-120">На следующих этапах вы создадите определения стилей для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4dd07-120">You'll create style definitions for the output in the following steps.</span></span>  

3. <span data-ttu-id="4dd07-121">Создайте файл с именем **AppCustomizer.module.scss** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="4dd07-121">Create a new file named **AppCustomizer.module.scss** under the **src\extensions\helloWorld** folder.</span></span> 

4. <span data-ttu-id="4dd07-122">Измените файл **AppCustomizer.module.scss** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4dd07-122">Update **AppCustomizer.module.scss** as follows:</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dd07-123">Это стили, которые будут использоваться в выходном HTML-коде для верхнего и нижнего колонтитулов.</span><span class="sxs-lookup"><span data-stu-id="4dd07-123">Note: These are the styles that will be used in the HTML output for the header and footer placeholders.</span></span>

      ```css
      .app {
        .top {
          height:60px;
          text-align:center;
          line-height:2.5;
          font-weight:bold;
          display: flex;
          align-items: center;
          justify-content: center;
        }

        .bottom {
          height:40px;
          text-align:center;
          line-height:2.5;
          font-weight:bold;
          display: flex;
          align-items: center;
          justify-content: center;
        }
      }
      ```

5. <span data-ttu-id="4dd07-124">Вернитесь к файлу **HelloWorldApplicationCustomizer.ts** и измените интерфейс **IHelloWorldApplicationCustomizerProperties**, добавив к нему свойства Header и Footer, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4dd07-124">In the **HelloWorldApplicationCustomizer.ts** file, update the **IHelloWorldApplicationCustomizerProperties** interface to add specific properties for Header and Footer, as follows.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4dd07-p107">Если ваш набор команд использует входные данные ClientSideComponentProperties в формате JSON, он будет десериализован в объект `BaseExtension.properties`. Вы можете определить интерфейс для его описания.</span><span class="sxs-lookup"><span data-stu-id="4dd07-p107">If your command set uses the ClientSideComponentProperties JSON input, it will be deserialized into the `BaseExtension.properties` object. You can define an interface to describe it.</span></span>

    ```ts
    export interface IHelloWorldApplicationCustomizerProperties {
      Top: string;
      Bottom: string;
    }
    ```

6. <span data-ttu-id="4dd07-127">Добавьте следующие частные переменные в класс **HelloWorldApplicationCustomizer**.</span><span class="sxs-lookup"><span data-stu-id="4dd07-127">Add the following private variables inside the **HelloWorldApplicationCustomizer** class.</span></span> <span data-ttu-id="4dd07-128">В этом случае это могут быть локальные переменные в методе `onRender`, но если вы хотите, чтобы они были доступны другим объектам, определите их как частные переменные.</span><span class="sxs-lookup"><span data-stu-id="4dd07-128">In this scenario, these can just be local variables in an `onRender` method, but if you want to share them with other objects,  define them as private variables.</span></span> 

      ```ts
      export default class HelloWorldApplicationCustomizer
        extends BaseApplicationCustomizer<IHelloWorldApplicationCustomizerProperties> {

        // These have been added
        private _topPlaceholder: PlaceholderContent | undefined;
        private _bottomPlaceholder: PlaceholderContent | undefined;
    ```

7. <span data-ttu-id="4dd07-129">Обновите код метода `onInit` как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4dd07-129">Update the `onInit` method code as follows:</span></span>

      ```ts
        @override
        public onInit(): Promise<void> {
          Log.info(LOG_SOURCE, `Initialized ${strings.Title}`);

          // Added to handle possible changes on the existence of placeholders.
          this.context.placeholderProvider.changedEvent.add(this, this._renderPlaceHolders);

          // Call render method for generating the HTML elements.
          this._renderPlaceHolders();
          return Promise.resolve<void>();
        }
      ```


8. <span data-ttu-id="4dd07-130">Создайте новый частный метод `_renderPlaceHolders` со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="4dd07-130">Create a new `_renderPlaceHolders` private method with the following code:</span></span>

      ```ts
        private _renderPlaceHolders(): void {

          console.log('HelloWorldApplicationCustomizer._renderPlaceHolders()');
          console.log('Available placeholders: ',
        this.context.placeholderProvider.placeholderNames.map(name => PlaceholderName[name]).join(', '));

          // Handling the top placeholder
          if (!this._topPlaceholder) {
        this._topPlaceholder =
          this.context.placeholderProvider.tryCreateContent(
            PlaceholderName.Top,
            { onDispose: this._onDispose });

        // The extension should not assume that the expected placeholder is available.
        if (!this._topPlaceholder) {
          console.error('The expected placeholder (Top) was not found.');
          return;
        }

        if (this.properties) {
          let topString: string = this.properties.Top;
          if (!topString) {
            topString = '(Top property was not defined.)';
          }

          if (this._topPlaceholder.domElement) {
            this._topPlaceholder.domElement.innerHTML = `
              <div class="${styles.app}">
                <div class="ms-bgColor-themeDark ms-fontColor-white ${styles.top}">
                  <i class="ms-Icon ms-Icon--Info" aria-hidden="true"></i> ${escape(topString)}
                </div>
              </div>`;
          }
        }
          }

          // Handling the bottom placeholder
          if (!this._bottomPlaceholder) {
        this._bottomPlaceholder =
          this.context.placeholderProvider.tryCreateContent(
            PlaceholderName.Bottom,
            { onDispose: this._onDispose });

        // The extension should not assume that the expected placeholder is available.
        if (!this._bottomPlaceholder) {
          console.error('The expected placeholder (Bottom) was not found.');
          return;
        }

        if (this.properties) {
          let bottomString: string = this.properties.Bottom;
          if (!bottomString) {
            bottomString = '(Bottom property was not defined.)';
          }

          if (this._bottomPlaceholder.domElement) {
            this._bottomPlaceholder.domElement.innerHTML = `
              <div class="${styles.app}">
                <div class="ms-bgColor-themeDark ms-fontColor-white ${styles.bottom}">
                  <i class="ms-Icon ms-Icon--Info" aria-hidden="true"></i> ${escape(bottomString)}
                </div>
              </div>`;
          }
        }
          }
        }
      ```

      * <span data-ttu-id="4dd07-131">Используйте метод `this.context.placeholderProvider.tryCreateContent` для доступа к заполнителю.</span><span class="sxs-lookup"><span data-stu-id="4dd07-131">Use `this.context.placeholderProvider.tryCreateContent` to get access to the placeholder.</span></span>
      * <span data-ttu-id="4dd07-132">Код расширения не должен предполагать, что нужный заполнитель доступен.</span><span class="sxs-lookup"><span data-stu-id="4dd07-132">Extension code should not assume that the expected placeholder is available.</span></span>
      * <span data-ttu-id="4dd07-133">Код ожидает настраиваемые свойства `Top` и `Bottom`.</span><span class="sxs-lookup"><span data-stu-id="4dd07-133">The code expects custom properties called `Top` and `Bottom`.</span></span> <span data-ttu-id="4dd07-134">Если свойства существуют, они будут отображаться в заполнителях.</span><span class="sxs-lookup"><span data-stu-id="4dd07-134">If the properties exist, they will render inside the placeholders.</span></span>
      * <span data-ttu-id="4dd07-135">Обратите внимание, что путь к коду верхнего и нижнего заполнителей почти идентичный.</span><span class="sxs-lookup"><span data-stu-id="4dd07-135">Notice that the code path for both the top and the bottom placeholders is almost identical.</span></span> <span data-ttu-id="4dd07-136">Он отличается только используемыми переменными и определениями стиля.</span><span class="sxs-lookup"><span data-stu-id="4dd07-136">The only differences are the variables used and the style definitions.</span></span>

9. <span data-ttu-id="4dd07-137">Добавьте приведенный ниже метод после метода `_renderPlaceHolders`.</span><span class="sxs-lookup"><span data-stu-id="4dd07-137">Add the following method after the `_renderPlaceHolders` method.</span></span> <span data-ttu-id="4dd07-138">В этом случае вы просто выводите сообщение в консоли, когда расширение удаляется со страницы.</span><span class="sxs-lookup"><span data-stu-id="4dd07-138">In this case, you simply output a console message when the extension is removed from the page.</span></span> 

      ```ts
        private _onDispose(): void {
          console.log('[HelloWorldApplicationCustomizer._onDispose] Disposed custom top and bottom placeholders.');
        }
      ```

<span data-ttu-id="4dd07-139">Теперь можно проверить код в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4dd07-139">You're now ready to test your code in SharePoint Online.</span></span>

## <a name="test-your-code"></a><span data-ttu-id="4dd07-140">Проверка кода</span><span class="sxs-lookup"><span data-stu-id="4dd07-140">Test your code</span></span>

<span data-ttu-id="4dd07-141">Перейдите в окно консоли, в котором запущена команда `gulp serve`, и проверьте наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="4dd07-141">Switch to the console window that is running `gulp serve` and check for errors.</span></span> <span data-ttu-id="4dd07-142">Gulp сообщает обо всех ошибках в консоли; исправьте их, чтобы продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="4dd07-142">Gulp reports any errors in the console; you'll need to fix them before you proceed.</span></span>

<span data-ttu-id="4dd07-143">Если решение не запущено, используйте следующую команду, чтобы проверить наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="4dd07-143">If you don't have the solution running, use the following command to check for errors.</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="4dd07-144">Перейдите в современный список в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="4dd07-144">Go to a modern list in SharePoint Online.</span></span> <span data-ttu-id="4dd07-145">Это может быть список или библиотека.</span><span class="sxs-lookup"><span data-stu-id="4dd07-145">This can be a list or a library.</span></span> 

<span data-ttu-id="4dd07-146">Для тестирования расширения добавьте в URL-адрес следующие параметры строки запроса:</span><span class="sxs-lookup"><span data-stu-id="4dd07-146">To test your extension, append the following query string parameters to the URL:</span></span>


```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```

* <span data-ttu-id="4dd07-147">Обратите внимание, что GUID, используемый в этом параметре запроса, должен совпадать с атрибутом ID настройщика приложений.</span><span class="sxs-lookup"><span data-stu-id="4dd07-147">Notice that the GUID used in this query parameter has to match on the ID attribute of your Application Customizer.</span></span> <span data-ttu-id="4dd07-148">Он доступен в файле **HelloWorldApplicationCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="4dd07-148">This is available in the **HelloWorldApplicationCustomizer.manifest.json** file.</span></span>
* <span data-ttu-id="4dd07-149">Свойства JSON Header и Footer используются для отправки параметров или конфигураций в настройщик приложений.</span><span class="sxs-lookup"><span data-stu-id="4dd07-149">You use Header and Footer JSON properties to provide parameters or configurations to the Application Customizer.</span></span> <span data-ttu-id="4dd07-150">В этом случае вы просто выводите эти значения.</span><span class="sxs-lookup"><span data-stu-id="4dd07-150">In this case, you simply output these values.</span></span> <span data-ttu-id="4dd07-151">Вы также можете настроить поведение на основе свойств, используемых в производстве.</span><span class="sxs-lookup"><span data-stu-id="4dd07-151">You can also adjust the behavior based on the properties used in production.</span></span> 

<span data-ttu-id="4dd07-152">Полный URL-адрес должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4dd07-152">The full URL should look similar to the following:</span></span>

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```

<span data-ttu-id="4dd07-153">Выберите **Загрузить скрипты отладки**, чтобы продолжить загрузку скриптов с локального узла.</span><span class="sxs-lookup"><span data-stu-id="4dd07-153">Choose **Load debug scripts** to continue loading scripts from your local host.</span></span>

![Запрос разрешения на отладку манифеста на странице](../../../images/ext-app-debug-manifest-message.png)

<span data-ttu-id="4dd07-155">Теперь на странице должны отображаться пользовательские верхний и нижний колонтитулы.</span><span class="sxs-lookup"><span data-stu-id="4dd07-155">You should now see the custom header and footer content in your page.</span></span> 

![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a><span data-ttu-id="4dd07-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4dd07-157">Next steps</span></span>
<span data-ttu-id="4dd07-158">Поздравляем, вы создали собственные верхний и нижний колонтитулы с помощью настройщика приложений!</span><span class="sxs-lookup"><span data-stu-id="4dd07-158">Congratulations, you've built your own custom header and footer using the Application Customizer!</span></span> <span data-ttu-id="4dd07-159">Далее см. статью [Развертывание расширения в SharePoint (Hello World, часть 3)](./serving-your-extension-from-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="4dd07-159">To continue building out your extension, see [Deploy your extension to SharePoint (Hello World part 3)](./serving-your-extension-from-sharepoint.md).</span></span> <span data-ttu-id="4dd07-160">Вы узнаете, как развернуть и просмотреть расширение Hello World в семействе веб-сайтов SharePoint, не используя параметры запроса **Debug**.</span><span class="sxs-lookup"><span data-stu-id="4dd07-160">You will learn how to deploy and preview the Hello World extension in a SharePoint site collection without using **Debug** query parameters.</span></span> 

> [!NOTE]
> <span data-ttu-id="4dd07-161">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint в [репозитории sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="4dd07-161">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="4dd07-162">Заранее благодарим за ваш вклад.</span><span class="sxs-lookup"><span data-stu-id="4dd07-162">Thanks for your input advance.</span></span>