# <a name="use-sp-pnp-js-with-sharepoint-framework-web-parts"></a>Использование sp-pnp-js с веб-частями SharePoint Framework

Вы можете использовать библиотеку [sp-pnp-js](https://www.npmjs.com/package/sp-pnp-js) при создании веб-частей SharePoint Framework (SPFx). Эта библиотека предоставляет текучий API, обеспечивающий интуитивно понятное составление запросов REST, а также поддерживает пакетную обработку и кэширование. Дополнительные сведения вы найдете на [домашней странице проекта](https://github.com/SharePoint/PnP-JS-Core), содержащей ссылки на документацию, примеры и другие ресурсы, которые помогут вам приступить к работе.

Вы можете скачать [полный исходный код](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js) для этой статьи на сайте с примерами.

## <a name="setup-your-environment"></a>Настройка среды

Прежде чем выполнять действия, описанные в этом руководстве, [настройте среду](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) для разработки с помощью SharePoint Framework.

## <a name="create-a-new-project"></a>Создание проекта

Для начала создайте папку проекта с помощью любой консоли:

```sh
md spfx-sp-pnp-js-example
```

Перейдите к этой папке:

```sh
cd spfx-sp-pnp-js-example
```

Запустите генератор Yeoman для SPFx:

```sh
yo @microsoft/sharepoint
```

Введите следующие значения при настройке нового проекта:

- **spfx-sp-pnp-js-example** в качестве имени решения (оставьте значение по умолчанию);
- **Current Folder** (Текущая папка) в качестве расположения решения;
- **Knockout** в качестве платформы;
- **SPPnPJSExample** в качестве имени веб-части;
- **Example of using sp-pnp-js within SPFx** (Пример использования sp-pnp-js в SPFx) в качестве описания.

![Скаффолдинг проекта завершен](../../../../images/sp-pnp-js-guide-completed-setup.png)


Когда скаффолдинг будет завершен, откройте проект в любом редакторе кода. На представленных здесь снимках экрана используется [Visual Studio Code](https://code.visualstudio.com/). Чтобы открыть каталог в Visual Studio Code, введите в консоли следующую команду:

```sh
code .
```

![Проект, впервые открытый в Visual Studio Code](../../../../images/sp-pnp-js-guide-first-open.png)

## <a name="install-and-setup-sp-pnp-js"></a>Установка и настройка sp-pnp-js

После создания проекта необходимо установить и настроить sp-pnp-js, начиная с установки пакета. Эти инструкции применимы к проектам любых типов (React и т. д.).

```sh
npm install sp-pnp-js --save
```

Библиотека sp-pnp-js составляет запросы REST, поэтому ей необходим URL-адрес для отправки этих запросов. Работая с классическими сайтами и страницами, мы можем воспользоваться глобальной переменной `_spPageContextInfo`. Но в случае SPFx применение этой переменной либо невозможно, либо может быть неправильным. Следовательно, нужно использовать объект [context](https://dev.office.com/sharepoint/reference/spfx/sp-webpart-base/iwebpartcontext), входящий в состав платформы. Убедиться в правильности настройки запросов можно [двумя способами](https://github.com/SharePoint/PnP-JS-Core/wiki/Using-sp-pnp-js-in-SharePoint-Framework#establish-context). В этом примере мы воспользуемся методом `onInit`.

### <a name="update-oninit-in-sppnpjsexamplewebpartts"></a>Обновление метода onInit в файле SpPnPjsExampleWebPart.ts

Откройте файл **src\webparts\spPnPjsExample\SpPnPjsExampleWebPart.ts** и добавьте оператор импорта для корневого объекта pnp.

```TypeScript
import pnp from "sp-pnp-js";
```

Замените код метода `onInit` приведенным ниже. Мы добавляем блок после вызова метода `super.onInit()`. Это делается для того, чтобы платформа могла инициализировать все необходимое, а библиотека настраивалась после выполнения этих действий.

```TypeScript
/**
 * Initialize the web part.
 */
protected onInit(): Promise<void> {
  this._id = _instance++;

  const tagName: string = `ComponentElement-${this._id}`;
  this._componentElement = this._createComponentElement(tagName);
  this._registerComponent(tagName);

  // When the web part description is changed, notify the view model to update.
  this._koDescription.subscribe((newValue: string) => {
    this._shouter.notifySubscribers(newValue, 'description');
  });

  const bindings: ISpPnPjsExampleBindingContext = {
    description: this.properties.description,
    shouter: this._shouter
  };

  ko.applyBindings(bindings, this._componentElement);

  return super.onInit().then(_ => {
    pnp.setup({
      spfxContext: this.context
    });
  });
}
```

## <a name="update-the-viewmodel"></a>Обновление модели ViewModel

Затем необходимо заменить содержимое файла **SpPnPjsExampleViewModel.ts** приведенным ниже кодом. Мы добавляем операцию импорта элементов pnp, интерфейс для определения полей элемента списка, некоторые наблюдаемые объекты для отслеживания списка элементов и новой формы элемента, а также методы для считывания, добавления и удаления элементов. Мы также добавили метод `ensureList`, использующий метод `lists.ensure`, чтобы проверять наличие списка (и создавать его при необходимости). Подготавливать ресурсы можно множеством способов, но мы выбрали этот метод, чтобы продемонстрировать создание списка, поля и элементов с помощью пакетной обработки в одном методе.

Из этого можно сделать вывод, что при использовании sp-pnp-js приходится писать намного меньше кода для обработки запросов, и вы можете сосредоточиться на бизнес-логике.

```TypeScript
import * as ko from 'knockout';
import styles from './SpPnPjsExample.module.scss';
import { ISpPnPjsExampleWebPartProps } from './ISpPnPjsExampleWebPartProps';
import pnp, { List, ListEnsureResult, ItemAddResult } from "sp-pnp-js";

export interface ISpPnPjsExampleBindingContext extends ISpPnPjsExampleWebPartProps {
  shouter: KnockoutSubscribable<{}>;
}

/**
 * Interface which defines the fields in our list items
 */
export interface OrderListItem {
  Id: number;
  Title: string;
  OrderNumber: string;
}

export default class SpPnPjsExampleViewModel {

  public description: KnockoutObservable<string> = ko.observable('');
  public newItemTitle: KnockoutObservable<string> = ko.observable('');
  public newItemNumber: KnockoutObservable<string> = ko.observable('');
  public items: KnockoutObservableArray<OrderListItem> = ko.observableArray([]);

  public labelClass: string = styles.label;
  public helloWorldClass: string = styles.helloWorld;
  public containerClass: string = styles.container;
  public rowClass: string = `ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`;
  public buttonClass: string = `ms-Button ${styles.button}`;

  constructor(bindings: ISpPnPjsExampleBindingContext) {
    this.description(bindings.description);

    // When the web part description is updated, change this view model's description.
    bindings.shouter.subscribe((value: string) => {
      this.description(value);
    }, this, 'description');

    // Load the items
    this.getItems().then(items => {

      this.items(items);
    });
  }

  /**
   * Gets the items from the list
   */
  private getItems(): Promise<OrderListItem[]> {

    return this.ensureList().then(list => {

      // Here we are using the getAs operator so that our returned value will be typed
      return list.items.select("Id", "Title", "OrderNumber").getAs<OrderListItem[]>();
    });
  }

  /**
   * Adds an item to the list
   */
  public addItem(): void {

    if (this.newItemTitle() !== "" && this.newItemNumber() !== "") {

      this.ensureList().then(list => {

        // Add the new item to the SharePoint list
        list.items.add({
          Title: this.newItemTitle(),
          OrderNumber: this.newItemNumber(),
        }).then((iar: ItemAddResult) => {

          // Add the new item to the display
          this.items.push({
            Id: iar.data.Id,
            OrderNumber: iar.data.OrderNumber,
            Title: iar.data.Title,
          });

          // Clear the form
          this.newItemTitle("");
          this.newItemNumber("");
        });
      });
    }
  }

  /**
   * Deletes an item from the list
   */
  public deleteItem(data): void {

    if (confirm("Are you sure you want to delete this item?")) {
      this.ensureList().then(list => {
        list.items.getById(data.Id).delete().then(_ => {
          this.items.remove(data);
        });
      }).catch((e: Error) => {
        alert(`There was an error deleting the item: ${e.message}`);
      });
    }
  }

  /**
   * Ensures the list exists. If not, it creates it and adds some default example data
   */
  private ensureList(): Promise<List> {

    return new Promise<List>((resolve, reject) => {

      // Use lists.ensure to always have the list available
      pnp.sp.web.lists.ensure("SPPnPJSExampleList").then((ler: ListEnsureResult) => {

        if (ler.created) {

          // We created the list on this call, so let's add a column
          ler.list.fields.addText("OrderNumber").then(_ => {

            // And we will also add a few items so we can see some example data
            // Here we use batching

            // Create a batch
            let batch = pnp.sp.web.createBatch();

            ler.list.getListItemEntityTypeFullName().then(typeName => {

              ler.list.items.inBatch(batch).add({
                Title: "Title 1",
                OrderNumber: "4826492"
              }, typeName);

              ler.list.items.inBatch(batch).add({
                Title: "Title 2",
                OrderNumber: "828475"
              }, typeName);

              ler.list.items.inBatch(batch).add({
                Title: "Title 3",
                OrderNumber: "75638923"
              }, typeName);

              // Excute the batched operations
              batch.execute().then(_ => {
                // All of the items have been added within the batch

                resolve(ler.list);

              }).catch(e => reject(e));

            }).catch(e => reject(e));

          }).catch(e => reject(e));

        } else {

          resolve(ler.list);
        }

      }).catch(e => reject(e));
    });
  }
}
```
## <a name="update-the-template"></a>Обновление шаблона

Напоследок нам необходимо обновить шаблон в соответствии с функциями, добавленными в ViewModel. Скопируйте приведенный ниже код в файл **SpPnPjsExample.template.html**. Мы добавили строку заголовка, цикл foreach для коллекции элементов и форму, позволяющую добавлять новые элементы в список.

```html
<div data-bind="attr: {class:helloWorldClass}">
  <div data-bind="attr: {class:containerClass}">

    <div data-bind="attr: {class:rowClass}">
      <div class="ms-Grid-col ms-u-sm12">
        <span class="ms-font-xl ms-fontColor-white ms-fontWeight-semibold" data-bind="text: description"></span>
      </div>
    </div>

    <div data-bind="attr: {class:rowClass}">
      <div class="ms-Grid-col ms-u-sm6">
        <span class="ms-font-l ms-fontColor-white ms-fontWeight-semibold">Title</span>
      </div>
      <div class="ms-Grid-col  ms-u-sm6">
        <span class="ms-font-l ms-fontColor-white ms-fontWeight-semibold">Order Number</span>
      </div>
    </div>

    <!-- ko foreach: items -->
    <div data-bind="attr: {class:$parent.rowClass}">
      <div class="ms-Grid-col ms-u-sm6">
        <span class="ms-font-l ms-fontColor-white" data-bind="text: Title"></span>
      </div>
      <div class="ms-Grid-col  ms-u-sm5">
        <span class="ms-font-l ms-fontColor-white" data-bind="text: OrderNumber"></span>
      </div>
      <div class="ms-Grid-col  ms-u-sm1">
        <i class="ms-Icon ms-Icon--Delete" aria-hidden="true" data-bind="click: $parent.deleteItem.bind($parent, $data)"></i>
      </div>
    </div>
    <!-- /ko -->

    <div data-bind="attr: {class:rowClass}">
      <div class="ms-Grid-col  ms-u-sm12">
        <span class="ms-font-l ms-fontColor-white ms-fontWeight-semibold">Add New</span>
      </div>
    </div>

    <div data-bind="attr: {class:rowClass}">
      <form data-bind="submit: addItem">
        <div class="ms-Grid-col ms-u-sm5">
          <input class="ms-TextField-field" placeholder="Title" data-bind='value: newItemTitle, valueUpdate: "afterkeydown"' />
        </div>
        <div class="ms-Grid-col ms-u-sm5">
          <input class="ms-TextField-field" placeholder="Order Number" data-bind='value: newItemNumber, valueUpdate: "afterkeydown"'
          />
        </div>
        <div class="ms-Grid-col ms-u-sm2">
          <button class="ms-Button--default ms-Button" type="submit" data-bind="enable: newItemTitle().length > 0 && newItemNumber().length > 0"><span class="ms-Button-label">Add</span></button>
        </div>
      </form>
    </div>

  </div>
</div>
```
## <a name="run-the-example"></a>Запуск примера

Запустите пример и добавьте веб-часть в размещаемое рабочее место SharePoint (/_layouts/workbench.aspx), чтобы увидеть ее в действии.

```sh
gulp serve --nobrowser
```

![Первый запуск проекта](../../../../images/sp-pnp-js-guide-first-run.png)

Вы можете удалять имеющиеся элементы, нажимая значок урны, и добавлять новые, указывая значения в обоих полях и нажимая кнопку добавления.

## <a name="next-steps"></a>Дальнейшие действия

Библиотека sp-pnp-js содержит огромный выбор функций и расширений. В [руководстве разработчика](https://github.com/SharePoint/PnP-JS-Core/wiki/Developer-Guide) вы найдете примеры, инструкции и советы по использованию и настройке библиотеки.

## <a name="production-deployment"></a>Развертывание в рабочей среде

Когда вы будете готовы к развертыванию решения и захотите выполнить сборку с использованием флага `--ship`, отметьте sp-pnp-js как внешнюю библиотеку в конфигурации. Для этого обновите файл **config/config.js**, добавив следующую строку в раздел externals:

```
"sp-pnp-js": "https://cdnjs.cloudflare.com/ajax/libs/sp-pnp-js/2.0.1/pnp.min.js"
```

В представленной выше конфигурации используется общедоступная сеть CDN, но URL-адрес может быть внутренним путем или другим расположением, которое требуется использовать. Измените номер версии в URL-адресе в соответствии с целевой версией.

## <a name="improving-the-example---mock-data"></a>Улучшение примера: фиктивные данные

В идеале пример должен подходить как для локальной среды программирования, так и для такой, которая размещена в SharePoint. Чтобы обеспечить это, необходимо создать фиктивную модель ViewModel и обновить код веб-части, как показано ниже.

### <a name="mock-viewmodel"></a>Фиктивная модель ViewModel

Добавьте новый файл с именем **MockSpPnPjsExampleViewModel.ts** к остальным файлам веб-части. Замените содержимое этого файла приведенным ниже кодом. При этом у вас будет тот же набор функций, но с решением можно будет работать в локальной среде, не рассчитывая на доступность SharePoint.

```TypeScript
import * as ko from 'knockout';
import styles from './SpPnPjsExample.module.scss';
import { ISpPnPjsExampleWebPartProps } from './ISpPnPjsExampleWebPartProps';
import pnp, { List, ListEnsureResult, ItemAddResult } from "sp-pnp-js";
import { ISpPnPjsExampleBindingContext, OrderListItem } from './SpPnPjsExampleViewModel';

export default class MockSpPnPjsExampleViewModel {

    public description: KnockoutObservable<string> = ko.observable('');
    public newItemTitle: KnockoutObservable<string> = ko.observable('');
    public newItemNumber: KnockoutObservable<string> = ko.observable('');
    public items: KnockoutObservableArray<OrderListItem> = ko.observableArray([]);

    public labelClass: string = styles.label;
    public helloWorldClass: string = styles.helloWorld;
    public containerClass: string = styles.container;
    public rowClass: string = `ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`;
    public buttonClass: string = `ms-Button ${styles.button}`;

    constructor(bindings: ISpPnPjsExampleBindingContext) {
        this.description(bindings.description);

        // When the web part description is updated, change this view model's description.
        bindings.shouter.subscribe((value: string) => {
            this.description(value);
        }, this, 'description');

        // Load the items
        this.getItems().then(items => {

            this.items(items);
        });
    }

    /**
     * Simulates getting the items from the list
     */
    private getItems(): Promise<OrderListItem[]> {
        return Promise.resolve([{
            Id: 1,
            Title: "Mock Item 1",
            OrderNumber: "12345"
        },
        {
            Id: 2,
            Title: "Mock Item 2",
            OrderNumber: "12345"
        },
        {
            Id: 3,
            Title: "Mock Item 3",
            OrderNumber: "12345"
        }]);
    }

    /**
     * Simulates adding an item to the list
     */
    public addItem(): void {

        if (this.newItemTitle() !== "" && this.newItemNumber() !== "") {

            // Add the new item to the display
            this.items.push({
                Id: this.items.length,
                OrderNumber: this.newItemNumber(),
                Title: this.newItemTitle(),
            });

            // Clear the form
            this.newItemTitle("");
            this.newItemNumber("");
        }
    }

    /**
     * Simulates deleting an item from the list
     */
    public deleteItem(data): void {

        if (confirm("Are you sure you want to delete this item?")) {
            this.items.remove(data);
        }
    }
}
```
### <a name="update-webpart"></a>Обновление веб-части

Наконец, нам необходимо обновить веб-часть, чтобы она использовала фиктивные данные по мере необходимости. Откройте файл **SpPnPjsExampleWebPart.ts**. Импортируйте только что созданный фиктивный сайт ViewModel.

```TypeScript
import MockSpPnPjsExampleViewModel from './MockSpPnPjsExampleViewModel';
```
Затем найдите метод `_registerComponent` и измените его, как показано ниже.

```TypeScript
private _registerComponent(tagName: string): void {

  if (Environment.type === EnvironmentType.Local) {
    console.log("here I am.")
    ko.components.register(
      tagName,
      {
        viewModel: MockSpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  } else {
    ko.components.register(
      tagName,
      {
        viewModel: SpPnPjsExampleViewModel,
        template: require('./SpPnPjsExample.template.html'),
        synchronous: false
      }
    );
  }
}
```
Наконец, введите в консоли команду `gulp serve`, чтобы открыть локальную среду программирования, которая теперь будет работать с фиктивными данными. (Если у вас уже запущен сервер, остановите его работу с помощью клавиш CTRL+C, а затем снова запустите.)

```sh
gulp serve
```

![Проект, запущенный в локальной среде программирования с фиктивными данными](../../../../images/sp-pnp-js-guide-with-mock-data.png)


## <a name="download-full-example-code"></a>Полный пример кода

Помните, что вы можете скачать полный пример кода [здесь](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).

## <a name="provide-feedback--report-issues"></a>Отзывы и отчеты о неполадках

Если у вас есть отзывы или вы хотите сообщить о проблеме с библиотекой sp-pnp-js, воспользуйтесь [списком проблем](https://github.com/SharePoint/PnP-JS-Core/issues) в этом репозитории.
