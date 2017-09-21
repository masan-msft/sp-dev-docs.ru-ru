# <a name="use-page-placeholders-from-application-customizer-hello-world-part-2"></a>Использование заполнителей страниц из настройщика приложений (Hello World, часть 2)

>**Примечание.** Расширения SharePoint Framework находятся на этапе тестирования и могут меняться. В настоящее время их невозможно использовать в рабочих средах.

Настройщики приложений обеспечивают доступ к известным местам на страницах SharePoint, которые можно менять в соответствии с организационными и функциональными требованиями. Например, вы можете создать динамические верхний и нижний колонтитулы, которые отображаются на всех страницах в SharePoint Online. 

Эта модель сопоставима с использованием коллекции **UserCustomAction** в объекте **Site** или **Web** для изменения страницы с помощью пользовательского кода JavaScript. Основное отличие или преимущество расширений SharePoint Framework (SPFx) в том, что элементы страницы не меняются при изменении структуры HTML/DOM в SharePoint Online.

В этой статье описано, как сделать так, чтобы [расширение Hello World](./build-a-hello-world-extension.md) использовало заполнители страниц. Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).

<a href="https://www.youtube.com/watch?v=ipRw6o6bOTw&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorial2.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="get-access-to-page-placeholders"></a>Получение доступа к заполнителям страниц

Расширения настройщика приложений поддерживаются в областях `Site`, `Web` и `List`. Вы можете контролировать место и способ регистрации настройщика приложений в клиенте SharePoint. Когда настройщик приложений существует в области и отображается, вы можете использовать следующий метод, чтобы получить доступ к заполнителю. 

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

После этого вы полностью контролируете, какие элементы показываются конечному пользователю.

Обратите внимание, что вы запрашиваете известный заполнитель, используя соответствующий известный идентификатор. В этом случае код получает доступ к нижнему колонтитулу страницы, используя идентификатор `Bottom`. 

Позже вы измените настройщик приложений Hello World, чтобы получить доступ к заполнителям и изменить их, добавив пользовательские элементы HTML.

1. В Visual Studio Code (или другой интегрированной среде разработки) откройте файл **src\extensions\helloWorld\HelloWorldApplicationCustomizer.ts.**

2. Добавьте объекты `PlaceholderContent` и `PlaceholderName` к оператору импорта из `@microsoft/sp-application-base`, изменив его следующим образом:

    ```ts
    import {
      BaseApplicationCustomizer, 
      PlaceholderContent,
      PlaceholderName
    } from '@microsoft/sp-application-base';
    ```
    
      Кроме того, добавьте следующие операторы импорта после кода импорта `strings` в начале файла:


        ```ts
        import styles from './AppCustomizer.module.scss';
        import { escape } from '@microsoft/sp-lodash-subset'; 
        ```

      Для экранирования свойств настройщика приложений используется функция `escape`. На следующих этапах вы создадите определения стилей для выходных данных.  

3. Создайте файл с именем **AppCustomizer.module.scss** в папке **src\extensions\helloWorld**. 

4. Измените файл **AppCustomizer.module.scss** следующим образом:

    >**Примечание.** Это стили, которые будут использоваться в выходном HTML-коде для верхнего и нижнего колонтитулов.

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

5. Вернитесь к файлу **HelloWorldApplicationCustomizer.ts** и измените интерфейс **IHelloWorldApplicationCustomizerProperties**, добавив к нему свойства Header и Footer, как показано ниже.

      **Примечание.** Если ваш набор команд использует входные данные ClientSideComponentProperties в формате JSON, он будет десериализован в объект `BaseExtension.properties`. Вы можете определить интерфейс для его описания.

    ```ts
    export interface IHelloWorldApplicationCustomizerProperties {
      Top: string;
      Bottom: string;
    }
    ```

6. Добавьте следующие частные переменные в класс **HelloWorldApplicationCustomizer**. В этом случае это могут быть локальные переменные в методе `onRender`, но если вы хотите, чтобы они были доступны другим объектам, определите их как частные переменные. 

      ```ts
      export default class HelloWorldApplicationCustomizer
        extends BaseApplicationCustomizer<IHelloWorldApplicationCustomizerProperties> {

        // These have been added
        private _topPlaceholder: PlaceholderContent | undefined;
        private _bottomPlaceholder: PlaceholderContent | undefined;
    ```

7. Обновите код метода `onInit` как показано ниже.

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


8. Создайте новый частный метод `_renderPlaceHolders` со следующим кодом:



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

      * Используйте метод `this.context.placeholderProvider.tryCreateContent` для доступа к заполнителю.
      * Код расширения не должен предполагать, что нужный заполнитель доступен.
      * Код ожидает настраиваемые свойства `Top` и `Bottom`. Если свойства существуют, они будут отображаться в заполнителях.
      * Обратите внимание, что путь к коду верхнего и нижнего заполнителей почти идентичный. Он отличается только используемыми переменными и определениями стиля.

9. Добавьте приведенный ниже метод после метода `_renderPlaceHolders`. В этом случае вы просто выводите сообщение в консоли, когда расширение удаляется со страницы. 

      ```ts
        private _onDispose(): void {
          console.log('[HelloWorldApplicationCustomizer._onDispose] Disposed custom top and bottom placeholders.');
        }
      ```

Теперь можно проверить код в SharePoint Online.

## <a name="test-your-code"></a>Проверка кода

Перейдите в окно консоли, в котором запущена команда `gulp serve`, и проверьте наличие ошибок. Gulp сообщает обо всех ошибках в консоли; исправьте их, чтобы продолжить работу.

Если решение не запущено, используйте следующую команду, чтобы проверить наличие ошибок.

```
gulp serve --nobrowser
```

Перейдите в современный список в SharePoint Online. Это может быть список или библиотека. 

Для тестирования расширения добавьте в URL-адрес следующие параметры строки запроса:


```
?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```

* Обратите внимание, что GUID, используемый в этом параметре запроса, должен совпадать с атрибутом ID настройщика приложений. Он доступен в файле **HelloWorldApplicationCustomizer.manifest.json**.
* Свойства JSON Header и Footer используются для отправки параметров или конфигураций в настройщик приложений. В этом случае вы просто выводите эти значения. Вы также можете настроить поведение на основе свойств, используемых в производстве. 

Полный URL-адрес должен выглядеть примерно следующим образом:

```
contoso.sharepoint.com/Lists/Contoso/AllItems.aspx?loadSPFX=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"e5625e23-5c5a-4007-a335-e6c2c3afa485":{"location":"ClientSideExtension.ApplicationCustomizer","properties":{"Top":"Top area of the page","Bottom":"Bottom area in the page"}}}
```

Выберите **Загрузить скрипты отладки**, чтобы продолжить загрузку скриптов с локального узла.

![Запрос разрешения на отладку манифеста на странице](../../../../images/ext-app-debug-manifest-message.png)

Теперь на странице должны отображаться пользовательские верхний и нижний колонтитулы. 

![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a>Дальнейшие действия
Поздравляем, вы создали собственные верхний и нижний колонтитулы с помощью настройщика приложений! Далее см. статью [Развертывание расширения в SharePoint (Hello World, часть 3)](./serving-your-extension-from-sharepoint.md). Вы узнаете, как развернуть и просмотреть расширение Hello World в семействе веб-сайтов SharePoint, не используя параметры запроса **Debug**. 
