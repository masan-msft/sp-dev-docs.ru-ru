# <a name="using-page-placeholders-from-application-customizer-hello-world-part-2"></a><span data-ttu-id="62624-101">Использование заполнителей страниц в настройщике приложений (Hello World, часть 2)</span><span class="sxs-lookup"><span data-stu-id="62624-101">Using page placeholders from Application Customizer (Hello World part 2)</span></span>

><span data-ttu-id="62624-p101">**Примечание.** Расширения для платформы SharePoint Framework находятся на этапе тестирования и могут меняться. В настоящее время расширения SharePoint Framework невозможно использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="62624-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="62624-p102">Настройщики приложений также предоставляют доступ к известным расположениям на странице, которые можно менять в соответствии с бизнес-требованиями и необходимыми функциями. К типичным примерам относятся динамические верхние и нижние колонтитулы, которые отображаются на всех страницах в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="62624-p102">Application Customizers also provide access to well known locations in the page, which you can modify based on your business and functional requirements. Typical scenarios would be dynamic header and footer experiences, which would be visible across all the pages in SharePoint Online.</span></span> 

<span data-ttu-id="62624-p103">Эта модель подобна использованию коллекции UserCustomAction в объекте Site или Web для связывания пользовательских ресурсов JavaScript и изменения внешнего вида страницы. Ключевое отличие (или преимущество) расширений SPFx заключается в том, что на странице гарантированно отображаются некоторые элементы независимо от изменений структуры HTML или модели DOM в будущих выпусках SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="62624-p103">This model is similar to using a UserCustomAction collection in a Site or Web object to associate custom JavaScript to modify the page experience. The key difference or advantage with SPFx extensions is that you have guaranteed elements on the page regardless of any HTML/DOM structure modifications in future changes to SharePoint Online.</span></span>

<span data-ttu-id="62624-108">В этой статье мы продолжим совершенствовать расширение Hello World, создание которого описывается в предыдущей статье, — [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./build-a-hello-world-extension.md) — для использования заполнителей страниц.</span><span class="sxs-lookup"><span data-stu-id="62624-108">In this article, we'll continue extending the hello world extension built in the previous article [Build your first SharePoint Framework Extension (Hello World part 1)](./build-a-hello-world-extension.md) to take advantage of the page placeholders.</span></span>

<span data-ttu-id="62624-109">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="62624-109">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span>

<a href="https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="getting-access-to-page-placeholders"></a><span data-ttu-id="62624-110">Получение доступа к заполнителям страниц</span><span class="sxs-lookup"><span data-stu-id="62624-110">Getting access to page placeholders</span></span>

<span data-ttu-id="62624-p104">Расширения настройщиков приложений поддерживаются в областях `Site`, `Web` и `List`. Вы можете управлять областью, выбирая, где и как настройщик приложений будет регистрироваться в клиенте SharePoint. Если настройщик приложений существует в области и отрисовывается, то вы можете получить доступ к заполнителю с помощью описанного ниже способа. Получив объект заполнителя, вы можете полностью контролировать элементы, которые видны пользователю.</span><span class="sxs-lookup"><span data-stu-id="62624-p104">Application Customizer extensions are supported with `Site`, `Web` and `List` scopes. You can control the scope by deciding where or how the Application Customizer will be registered in your SharePoint tenant. When the Application Customizer exists in the scope and is being rendered, you can use the following method to get access to the placeholder. Once you have received the placeholder object, you have full control over what will be presented to the end user.</span></span>

<span data-ttu-id="62624-p105">Обратите внимание, что вы запрашиваете известный заполнитель по соответствующему известному идентификатору. В этом случае код получает доступ к разделу нижнего колонтитула страницы по идентификатору `Bottom`.</span><span class="sxs-lookup"><span data-stu-id="62624-p105">Notice that we are requesting a well-known placeholder by using the corresponding well-known identifier. In this case, the code is accessing the header section of the page using the `Bottom` identifier.</span></span> 

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

<span data-ttu-id="62624-117">На последующих этапах мы изменим созданный ранее настройщик приложений Hello World, чтобы получить доступ к заполнителям и изменить их содержимое, добавив к ним пользовательские элементы HTML.</span><span class="sxs-lookup"><span data-stu-id="62624-117">In the following steps, we'll modify the previously created hello word Application Customizer to access placeholders and modify their content by adding custom html elements to them.</span></span>

<span data-ttu-id="62624-118">Перейдите в Visual Studio Code (или другую интегрированную среду разработки) и откройте файл **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**</span><span class="sxs-lookup"><span data-stu-id="62624-118">Switch to Visual Studio Code (or your preferred IDE) and open **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**</span></span>

<span data-ttu-id="62624-119">Добавьте объекты `PlaceholderContent` и `PlaceholderName` к оператору импорта из `@microsoft/sp-application-base`, изменив его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62624-119">Add the `PlaceholderContent` to the import from `@microsoft/sp-application-base` by updating the import statement as follows:</span></span>

```ts
import {
  BaseApplicationCustomizer, 
  PlaceholderContent,
  PlaceholderName
} from '@microsoft/sp-application-base';
```

<span data-ttu-id="62624-120">Кроме того, добавьте следующие операторы импорта после кода импорта `strings` в начале файла:</span><span class="sxs-lookup"><span data-stu-id="62624-120">Also add the following import statements after the `strings` import at the top of the file:</span></span>

* <span data-ttu-id="62624-121">На последующих этапах мы создадим определения стилей для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="62624-121">We will create style definitions for the output in the following steps</span></span>
* <span data-ttu-id="62624-122">Для отмены свойств настройщика приложений используется функция `escape`.</span><span class="sxs-lookup"><span data-stu-id="62624-122">`escape` is used to escape Application Customizer properties</span></span>  

```ts
import styles from './AppCustomizer.module.scss';
import { escape } from '@microsoft/sp-lodash-subset'; 
```

<span data-ttu-id="62624-123">Создайте файл с именем **AppCustomizer.module.scss** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="62624-123">Create a new file named **AppCustomizer.module.scss** under the **src\extensions\helloWorld** folder.</span></span> 

<span data-ttu-id="62624-124">Измените файл **AppCustomizer.module.scss** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62624-124">Update **AppCustomizer.module.scss** as follows:</span></span>

* <span data-ttu-id="62624-125">Это стили, которые будут использоваться в выходном коде HTML для заполнителей верхнего и нижнего колонтитулов.</span><span class="sxs-lookup"><span data-stu-id="62624-125">These are the styles that will be used within the outputed html for the header and footer placeholders.</span></span>

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

<span data-ttu-id="62624-126">Вернитесь к файлу **HelloWorldApplicationCustomizer.ts** и измените интерфейс **IHelloWorldApplicationCustomizerProperties**, добавив к нему свойства Header и Footer, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="62624-126">Move back to **HelloWorldApplicationCustomizer.ts** and update the **IHelloWorldApplicationCustomizerProperties** interface to have specific properties for Header and Footer as follows.</span></span>

* <span data-ttu-id="62624-p106">Если ваш набор команд использует входные данные ClientSideComponentProperties в формате JSON, он будет десериализован в объект `BaseExtension.properties`. Вы можете определить интерфейс для его описания.</span><span class="sxs-lookup"><span data-stu-id="62624-p106">If your command set uses the ClientSideComponentProperties JSON input, it will be deserialized into the `BaseExtension.properties` object. You can define an interface to describe it.</span></span>

```ts
export interface IHelloWorldApplicationCustomizerProperties {
  Top: string;
  Bottom: string;
}
```

<span data-ttu-id="62624-p107">Добавьте приведенные ниже частные переменные в класс **HelloWorldApplicationCustomizer**. В данном сценарии это могут быть обычные локальные переменные в методе `onRender`, но если вы хотите сделать их доступными другим объектам, вы можете определить их как частные переменные.</span><span class="sxs-lookup"><span data-stu-id="62624-p107">Add the following private variables inside of the **HelloWorldApplicationCustomizer** class. In this scenario, these could just be local variables in an `onRender` method, but if you want to share them with other objects you define them as private variables.</span></span> 

```ts
export default class HelloWorldApplicationCustomizer
  extends BaseApplicationCustomizer<IHelloWorldApplicationCustomizerProperties> {
  
  // These have been added
  private _topPlaceholder: PlaceholderContent | undefined;
  private _bottomPlaceholder: PlaceholderContent | undefined;
```

<span data-ttu-id="62624-131">Обновите код метода `onInit` как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="62624-131">Update the `onInit` method as follows</span></span>

```ts
  @override
  public onInit(): Promise<void> {
    Log.info(LOG_SOURCE, `Initialized ${strings.Title}`);

    // Added to handle possible changes on the existence of placeholders
    this.context.placeholderProvider.changedEvent.add(this, this._renderPlaceHolders);

    // Call render method for generating the needed html elements
    this._renderPlaceHolders();
    return Promise.resolve<void>();
  }
```


<span data-ttu-id="62624-132">Создайте новый частный метод `_renderPlaceHolders` со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="62624-132">Create new `_renderPlaceHolders` private method with the following code:</span></span>

* <span data-ttu-id="62624-133">Мы используем метод `this.context.placeholderProvider.tryCreateContent` для доступа к заполнителю.</span><span class="sxs-lookup"><span data-stu-id="62624-133">We use `this.context.placeholderProvider.tryCreateContent` to get access on the placeholder</span></span>
* <span data-ttu-id="62624-134">Код расширения не должен предполагать, что нужный заполнитель доступен.</span><span class="sxs-lookup"><span data-stu-id="62624-134">Extension code should not assume that the expected placeholder is available</span></span>
* <span data-ttu-id="62624-p108">Код ожидает настраиваемые свойства `Top` и `Bottom`. Если свойства существуют, они будут отрисовываться в заполнителях.</span><span class="sxs-lookup"><span data-stu-id="62624-p108">The code expects custom properties called `Top`and `Bottom`. If the properties exist, they will be rendered inside of the placeholders.</span></span>
* <span data-ttu-id="62624-p109">Обратите внимание, что в приведенном ниже пути к коду для верхних и нижних заполнителей практически идентичны. Единственные отличия связаны с используемыми переменными и определениями стилей.</span><span class="sxs-lookup"><span data-stu-id="62624-p109">Notice that the code path for both the header and the footer is almost identical in the below method. The only differences are the variables used and the style definitions.</span></span>

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

<span data-ttu-id="62624-p110">Добавьте приведенный ниже метод после метода `_renderPlaceHolders`. В этом случае мы просто выводим сообщение в консоли, когда расширение удаляется со страницы.</span><span class="sxs-lookup"><span data-stu-id="62624-p110">Add the following method after the `_renderPlaceHolders` method. In this case, we simply output a console message, when the extension is removed from the page.</span></span> 

```ts
  private _onDispose(): void {
    console.log('[HelloWorldApplicationCustomizer._onDispose] Disposed custom top and bottom placeholders.');
  }
```

<span data-ttu-id="62624-141">Теперь код готов к тестированию в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="62624-141">The code is now ready to be tested in SharePoint Online.</span></span>

<span data-ttu-id="62624-p111">Перейдите в окно консоли, в котором запущена команда `gulp serve`, и проверьте наличие ошибок. Если gulp сообщил об ошибках, их нужно исправить.</span><span class="sxs-lookup"><span data-stu-id="62624-p111">Switch to the console window that is running `gulp serve` and check if there are any errors. If there are errors, gulp reports them in the console and you will need to fix them before proceeding.</span></span>

<span data-ttu-id="62624-144">Если в данный момент решение не запущено, выполните приведенную ниже команду и убедитесь, что не возникает никаких ошибок.</span><span class="sxs-lookup"><span data-stu-id="62624-144">If you don't have the solution running currently, execute the following command and ensure you don't have any errors.</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="62624-p112">Перейдите ко встроенному списку в SharePoint Online. Это может быть список или библиотека для первоначального тестирования.</span><span class="sxs-lookup"><span data-stu-id="62624-p112">Navigate to an out of the box modern list in SharePoint Online. This can be a list or a library for the initial testing.</span></span> 

<span data-ttu-id="62624-147">Для тестирования расширения добавьте к URL-адресу следующие параметры строки запроса:</span><span class="sxs-lookup"><span data-stu-id="62624-147">To test your extension, append the following query string parameters to the URL:</span></span>

* <span data-ttu-id="62624-148">Обратите внимание, что GUID, используемый в этом параметре запроса, должен совпадать с атрибутом ID настройщика приложений, указанным в файле **HelloWorldApplicationCustomizer.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="62624-148">Notice that the GUID used in this query parameter has to match on the ID attribute of your Application Customizer available from **HelloWorldApplicationCustomizer.manifest.json**.</span></span>
* <span data-ttu-id="62624-p113">Мы также используем свойства JSON Header и Footer, чтобы предоставлять параметры или модификации в настройщик приложений. В данном случае мы просто выводим эти значения, но вы можете настроить поведение в соответствии со свойствами, используемыми в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="62624-p113">We also use Header and Footer JSON properties to provide parameters or configurations to the Application Customizer. In this case, we simply output these values, but you could adjust the behavior based on the properties in actual production usage.</span></span> 

```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```
<span data-ttu-id="62624-151">Полный URL-адрес запроса должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="62624-151">The full URL to request would be something like the following:</span></span>

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```

![Запрос разрешения на отладку манифеста на странице](../../../../images/ext-app-debug-manifest-message.png)

<span data-ttu-id="62624-153">Нажмите кнопку **Загрузить скрипты отладки**, чтобы продолжить загрузку скриптов с локального узла.</span><span class="sxs-lookup"><span data-stu-id="62624-153">Click the "**Load debug scripts**" button to continue loading scripts from your local host.</span></span>

<span data-ttu-id="62624-154">Теперь на странице должно отображаться пользовательское содержимое верхнего и нижнего колонтитулов.</span><span class="sxs-lookup"><span data-stu-id="62624-154">You should now see the custom header and footer content in your page.</span></span> 

![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a><span data-ttu-id="62624-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62624-156">Next steps</span></span>
<span data-ttu-id="62624-p114">Поздравляем! Вы создали собственные верхний и нижний колонтитул с помощью настройщика приложений. Вы можете продолжить разработку расширения Hello World в следующей статье — [Развертывание расширения в семействе веб-сайтов (Hello World, часть 3)](./serving-your-extension-from-sharepoint.md). Вы научитесь развертывать и просматривать расширение Hello World в семействе веб-сайтов SharePoint, не используя параметры запроса **Debug**.</span><span class="sxs-lookup"><span data-stu-id="62624-p114">Congratulations on building your own custom header and footer using the Application Customizer! You can continue building out your Hello World Extension in the next topic [Deploy your extension to site collection (Hello world part 3)](./serving-your-extension-from-sharepoint.md). You will learn how to deploy and preview the Hello World extension in a SharePoint site collection without using **Debug** query parameters.</span></span> 
