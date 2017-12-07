---
title: "Использование sp-pnp-js с веб-частями SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e0f86a7ed8d0c3c09e00087819b2608d8c67eccf
ms.sourcegitcommit: 9c458121628425716442abddbc97a1f61f18a74c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2017
---
# <a name="use-sp-pnp-js-with-sharepoint-framework-web-parts"></a><span data-ttu-id="cf4d8-102">Использование sp-pnp-js с веб-частями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="cf4d8-102">Use sp-pnp-js with SharePoint Framework Web Parts</span></span>

<span data-ttu-id="cf4d8-p101">Вы можете использовать библиотеку [sp-pnp-js](https://www.npmjs.com/package/sp-pnp-js) при создании веб-частей SharePoint Framework (SPFx). Эта библиотека предоставляет текучий API, обеспечивающий интуитивно понятное составление запросов REST, а также поддерживает пакетную обработку и кэширование. Дополнительные сведения вы найдете на [домашней странице проекта](https://github.com/SharePoint/PnP-JS-Core), содержащей ссылки на документацию, примеры и другие ресурсы, которые помогут вам приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p101">You may opt to use the [sp-pnp-js](https://www.npmjs.com/package/sp-pnp-js) library when building your SharePoint Framework (SPFx) web parts. This library provides a fluent API to make building your REST queries intuitive and supports batching and caching. You can learn more on the [project's homepage](https://github.com/SharePoint/PnP-JS-Core) which has links to documentation, samples, and other resources to help you get started.</span></span>

<span data-ttu-id="cf4d8-106">Вы можете скачать [полный исходный код](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js) для этой статьи на сайте с примерами.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-106">You can download the [full source](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js) for this article from the samples site.</span></span>

## <a name="setup-your-environment"></a><span data-ttu-id="cf4d8-107">Настройка среды</span><span class="sxs-lookup"><span data-stu-id="cf4d8-107">Setup your Environment</span></span>

<span data-ttu-id="cf4d8-108">Прежде чем выполнять действия, описанные в этом руководстве, [настройте среду](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) для разработки с помощью SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-108">Before you can complete this guide, you will need to ensure you have [setup your environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment) for development using the SharePoint Framework.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="cf4d8-109">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="cf4d8-109">Create a New Project</span></span>

<span data-ttu-id="cf4d8-110">Для начала создайте папку проекта с помощью любой консоли:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-110">Start by creating a new folder for the project using your console of choice:</span></span>

```sh
md spfx-sp-pnp-js-example
```

<span data-ttu-id="cf4d8-111">Перейдите к этой папке:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-111">And enter that folder:</span></span>

```sh
cd spfx-sp-pnp-js-example
```

<span data-ttu-id="cf4d8-112">Запустите генератор Yeoman для SPFx:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-112">Then run the Yeoman generator for SPFx:</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="cf4d8-113">Введите следующие значения при настройке нового проекта:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-113">Enter the following values when prompted during the setup of the new project:</span></span>

- <span data-ttu-id="cf4d8-114">**spfx-sp-pnp-js-example** в качестве имени решения (оставьте значение по умолчанию);</span><span class="sxs-lookup"><span data-stu-id="cf4d8-114">**spfx-sp-pnp-js-example** as solution name (keep default)</span></span>
- <span data-ttu-id="cf4d8-115">**SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) в качестве версии базовых пакетов;</span><span class="sxs-lookup"><span data-stu-id="cf4d8-115">**SharePoint Online only (latest)** as the baseline packages version</span></span>
- <span data-ttu-id="cf4d8-116">**Current Folder** (Текущая папка) в качестве расположения решения;</span><span class="sxs-lookup"><span data-stu-id="cf4d8-116">**Current Folder** as the solution location</span></span>
- <span data-ttu-id="cf4d8-117">**Y** для разрешения администратору клиента развертывать решение на всех сайтах;</span><span class="sxs-lookup"><span data-stu-id="cf4d8-117">**Y** as allow tenant admin to deploy solution to all sites</span></span>
- <span data-ttu-id="cf4d8-118">**WebPart** в качестве компонента, который необходимо создать;</span><span class="sxs-lookup"><span data-stu-id="cf4d8-118">**WebPart** as the client-side component to create</span></span>
- <span data-ttu-id="cf4d8-119">**SPPnPJSExample** в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="cf4d8-119">**SPPnPJSExample** as the name of the web part</span></span>
- <span data-ttu-id="cf4d8-120">**Example of using sp-pnp-js within SPFx** (Пример использования sp-pnp-js в SPFx) в качестве описания;</span><span class="sxs-lookup"><span data-stu-id="cf4d8-120">**Example of using sp-pnp-js within SPFx** as the description</span></span>
- <span data-ttu-id="cf4d8-121">**Knockout** в качестве платформы.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-121">**Knockout** as the framework</span></span>

![Скаффолдинг проекта завершен](../../../images/sp-pnp-js-guide-completed-setup.png)

<span data-ttu-id="cf4d8-123">После завершения скаффолдинга блокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-123">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="cf4d8-124">Далее откройте проект в выбранном редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-124">Next, open the project in the code editor of your choosing.</span></span> <span data-ttu-id="cf4d8-125">На приведенных здесь снимках экрана показан [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="cf4d8-125">The screenshots shown here demonstrate [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="cf4d8-126">Чтобы открыть каталог в Visual Studio Code, введите следующее в консоль:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-126">To open the directory within Visual Studio Code, enter the following in the console:</span></span>

```sh
code .
```

![Проект, впервые открытый в Visual Studio Code](../../../images/sp-pnp-js-guide-first-open.png)

## <a name="install-and-setup-sp-pnp-js"></a><span data-ttu-id="cf4d8-128">Установка и настройка sp-pnp-js</span><span class="sxs-lookup"><span data-stu-id="cf4d8-128">Install And Setup sp-pnp-js</span></span>

<span data-ttu-id="cf4d8-p103">После создания проекта необходимо установить и настроить sp-pnp-js, начиная с установки пакета. Эти инструкции применимы к проектам любых типов (React и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p103">Once your project is created you will need to install and setup sp-pnp-js, starting with installing the package. These steps are common for any project type (React, etc).</span></span>

```sh
npm install sp-pnp-js --save
```

<span data-ttu-id="cf4d8-p104">Библиотека sp-pnp-js составляет запросы REST, поэтому ей необходим URL-адрес для отправки этих запросов. Работая с классическими сайтами и страницами, мы можем воспользоваться глобальной переменной `_spPageContextInfo`. Но в случае SPFx применение этой переменной либо невозможно, либо может быть неправильным. Следовательно, нужно использовать объект [context](https://dev.office.com/sharepoint/reference/spfx/sp-webpart-base/iwebpartcontext), входящий в состав платформы. Убедиться в правильности настройки запросов можно [двумя способами](https://github.com/SharePoint/PnP-JS-Core/wiki/Using-sp-pnp-js-in-SharePoint-Framework#establish-context). В этом примере мы воспользуемся методом `onInit`.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p104">Because the sp-pnp-js library constructs REST requests it needs to know the URL to send these requests. When operating within classic sites and pages, we can make use of the global `_spPageContextInfo` variable. Within SPFx, this is not available, or if it is, may not be correct. So we need to rely on the [context](https://dev.office.com/sharepoint/reference/spfx/sp-webpart-base/iwebpartcontext) object supplied by the framework. There are [two ways](https://github.com/SharePoint/PnP-JS-Core/wiki/Using-sp-pnp-js-in-SharePoint-Framework#establish-context) to ensure you have correctly setup your requests, we'll use the `onInit` method in this example.</span></span>

### <a name="update-oninit-in-sppnpjsexamplewebpartts"></a><span data-ttu-id="cf4d8-136">Обновление метода onInit в файле SpPnPjsExampleWebPart.ts</span><span class="sxs-lookup"><span data-stu-id="cf4d8-136">Update onInit in SpPnPjsExampleWebPart.ts</span></span>

<span data-ttu-id="cf4d8-137">Откройте файл **src\webparts\spPnPjsExample\SpPnPjsExampleWebPart.ts** и добавьте оператор импорта для корневого объекта pnp.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-137">Open the **src\webparts\spPnPjsExample\SpPnPjsExampleWebPart.ts** file and add an import statement for the pnp root object:</span></span>

```TypeScript
import pnp from "sp-pnp-js";
```

<span data-ttu-id="cf4d8-p105">Замените код метода `onInit` приведенным ниже. Мы добавляем блок после вызова метода `super.onInit()`. Это делается для того, чтобы платформа могла инициализировать все необходимое, а библиотека настраивалась после выполнения этих действий.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p105">In the `onInit` method, update the code to appear as below. We are adding the block after the `super.onInit()` call. We do this after the `super.onInit` to ensure that the framework has a chance to initialize anything required and that we are setting up the library after those steps are completed.</span></span>

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

## <a name="update-the-viewmodel"></a><span data-ttu-id="cf4d8-141">Обновление модели ViewModel</span><span class="sxs-lookup"><span data-stu-id="cf4d8-141">Update the ViewModel</span></span>

<span data-ttu-id="cf4d8-p106">Затем необходимо заменить содержимое файла **SpPnPjsExampleViewModel.ts** приведенным ниже кодом. Мы добавляем операцию импорта элементов pnp, интерфейс для определения полей элемента списка, некоторые наблюдаемые объекты для отслеживания списка элементов и новой формы элемента, а также методы для считывания, добавления и удаления элементов. Мы также добавили метод `ensureList`, использующий метод `lists.ensure`, чтобы проверять наличие списка (и создавать его при необходимости). Подготавливать ресурсы можно множеством способов, но мы выбрали этот метод, чтобы продемонстрировать создание списка, поля и элементов с помощью пакетной обработки в одном методе.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p106">Next, replace the contents of the **SpPnPjsExampleViewModel.ts** file with the code below. We are adding an import statement for the pnp items, an interface to define our list item's fields, some observables to track both our list of items and the new item form, and methods to support getting, adding, & deleting items. We also added an `ensureList` method which uses the sp-pnp-js `lists.ensure` method to always make sure we have the list (and to create it if necessary). There are many ways to provision resources, but this method was choosen to demonstrate creating a list, field, and items using batching within a single method.</span></span>

<span data-ttu-id="cf4d8-146">Из этого можно сделать вывод, что при использовании sp-pnp-js приходится писать намного меньше кода для обработки запросов, и вы можете сосредоточиться на бизнес-логике.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-146">The takeaway is that by using sp-pnp-js, we write much less code to handle requests and can focus on our business logic.</span></span>

```TypeScript
import * as ko from 'knockout';
import styles from './SpPnPjsExample.module.scss';
import { ISpPnPjsExampleWebPartProps } from './SpPnPjsExampleWebPart';
import pnp, { List, ListEnsureResult, ItemAddResult, FieldAddResult } from "sp-pnp-js";

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

const LIST_EXISTS: string = 'List exists';

export default class SpPnPjsExampleViewModel {
  public description: KnockoutObservable<string> = ko.observable('');
  public newItemTitle: KnockoutObservable<string> = ko.observable('');
  public newItemNumber: KnockoutObservable<string> = ko.observable('');
  public items: KnockoutObservableArray<OrderListItem> = ko.observableArray([]);

  public labelClass: string = styles.label;
  public spPnPjsExampleClass: string = styles.spPnPjsExample;
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
    this.getItems().then((items: OrderListItem[]): void => {
      this.items(items);
    });
  }

  /**
   * Gets the items from the list
   */
  private getItems(): Promise<OrderListItem[]> {
    return this.ensureList().then((list: List): Promise<OrderListItem[]> => {
      // Here we are using the getAs operator so that our returned value will be typed
      return list.items.select("Id", "Title", "OrderNumber").getAs<OrderListItem[]>();
    });
  }

  /**
   * Adds an item to the list
   */
  public addItem(): void {
    if (this.newItemTitle() !== "" && this.newItemNumber() !== "") {
      this.ensureList().then((list: List): Promise<ItemAddResult> => {
        // Add the new item to the SharePoint list
        return list.items.add({
          Title: this.newItemTitle(),
          OrderNumber: this.newItemNumber(),
        });
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
    }
  }

  /**
   * Deletes an item from the list
   */
  public deleteItem(data): void {
    if (!confirm("Are you sure you want to delete this item?")) {
      return;
    }

    this.ensureList().then((list: List): Promise<void> => {
      return list.items.getById(data.Id).delete();
    }).then(_ => {
      this.items.remove(data);
    }).catch((e: Error) => {
      alert(`There was an error deleting the item: ${e.message}`);
    });
  }

  /**
   * Ensures the list exists. If not, it creates it and adds some default example data
   */
  private ensureList(): Promise<List> {
    return new Promise<List>((resolve: (list: List) => void, reject: (err: string) => void): void => {
      let listEnsureResults: ListEnsureResult;
      // Use lists.ensure to always have the list available
      pnp.sp.web.lists.ensure("SPPnPJSExampleList")
        .then((ler: ListEnsureResult): Promise<FieldAddResult> => {
          listEnsureResults = ler;

          if (!ler.created) {
             // resolve main promise
            resolve(ler.list);
            // break promise chain
            return Promise.reject(LIST_EXISTS);
          }

          // We created the list on this call, so let's add a column
          return ler.list.fields.addText("OrderNumber");
        }).then((): Promise<string> => {
          console.warn('Adding items...');
          // And we will also add a few items so we can see some example data
          // Here we use batching
          return listEnsureResults.list.getListItemEntityTypeFullName();
        }).then((typeName: string): Promise<void> => {
          // Create a batch
          const batch = pnp.sp.web.createBatch();
          listEnsureResults.list.items.inBatch(batch).add({
            Title: "Title 1",
            OrderNumber: "4826492"
          }, typeName);

          listEnsureResults.list.items.inBatch(batch).add({
            Title: "Title 2",
            OrderNumber: "828475"
          }, typeName);

          listEnsureResults.list.items.inBatch(batch).add({
            Title: "Title 3",
            OrderNumber: "75638923"
          }, typeName);

          // Execute the batched operations
          return batch.execute();
        }).then((): void => {
          // All of the items have been added within the batch
          resolve(listEnsureResults.list);
        }).catch((e: any): void => {
          if (e !== LIST_EXISTS) {
            reject(e);
          }
        });
    });
  }
}
```

## <a name="update-the-template"></a><span data-ttu-id="cf4d8-147">Обновление шаблона</span><span class="sxs-lookup"><span data-stu-id="cf4d8-147">Update the Template</span></span>

<span data-ttu-id="cf4d8-p107">Напоследок нам необходимо обновить шаблон в соответствии с функциями, добавленными в ViewModel. Скопируйте приведенный ниже код в файл **SpPnPjsExample.template.html**. Мы добавили строку заголовка, цикл foreach для коллекции элементов и форму, позволяющую добавлять новые элементы в список.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p107">Finally, we need to update the template to match the functionality we have added into the ViewModel. Copy the code below into the **SpPnPjsExample.template.html** file. We have added a title row, a foreach repeater for the items collection, and a form allowing you to add new items to the list.</span></span>

```html
<div data-bind="attr: {class:spPnPjsExampleClass}">
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

## <a name="run-the-example"></a><span data-ttu-id="cf4d8-151">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="cf4d8-151">Run the Example</span></span>

<span data-ttu-id="cf4d8-152">Запустите пример и добавьте веб-часть в размещаемое рабочее место SharePoint (/_layouts/workbench.aspx), чтобы увидеть ее в действии.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-152">Start the sample and add the web part to your SharePoint hosted workbench (/_layouts/workbench.aspx) to can see it in action.</span></span>

```sh
gulp serve --nobrowser
```

![Первый запуск проекта](../../../images/sp-pnp-js-guide-first-run.png)

<span data-ttu-id="cf4d8-154">Вы можете удалять имеющиеся элементы, нажимая значок урны, и добавлять новые, указывая значения в обоих полях и нажимая кнопку добавления.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-154">You can delete existing items by clicking on the trashcan icon, or add new items by putting values in both fields and clicking the add button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf4d8-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf4d8-155">Next Steps</span></span>

<span data-ttu-id="cf4d8-p108">Библиотека sp-pnp-js содержит огромный выбор функций и расширений. В [руководстве разработчика](https://github.com/SharePoint/PnP-JS-Core/wiki/Developer-Guide) вы найдете примеры, инструкции и советы по использованию и настройке библиотеки.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p108">The sp-pnp-js library contains a great range of functionality and extensibility. Please check out the [developer guide](https://github.com/SharePoint/PnP-JS-Core/wiki/Developer-Guide) for samples, guidance, and hints on using and configuring the library.</span></span>

## <a name="production-deployment"></a><span data-ttu-id="cf4d8-158">Развертывание в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="cf4d8-158">Production Deployment</span></span>

<span data-ttu-id="cf4d8-p109">Когда вы будете готовы к развертыванию решения и захотите выполнить сборку с использованием флага `--ship`, отметьте sp-pnp-js как внешнюю библиотеку в конфигурации. Для этого обновите файл **config/config.js**, добавив следующую строку в раздел externals:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p109">When you are ready to deploy your solution and want to build using the `--ship` flag you need to mark sp-pnp-js as an external library in the configuration. This is done by updating the SPFx **config/config.js** file to include this line in the externals section:</span></span>

```json
"sp-pnp-js": "https://cdnjs.cloudflare.com/ajax/libs/sp-pnp-js/2.0.1/pnp.min.js"
```

<span data-ttu-id="cf4d8-p110">В представленной выше конфигурации используется общедоступная сеть CDN, но URL-адрес может быть внутренним путем или другим расположением, которое требуется использовать. Измените номер версии в URL-адресе в соответствии с целевой версией.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p110">In the configuration above, we are using the public CDN but the URL can be an internal path or any other location you would like to use. Be sure, however, to update the version number in the URL to match the version you are targeting.</span></span>

## <a name="improving-the-example---mock-data"></a><span data-ttu-id="cf4d8-163">Улучшение примера: фиктивные данные</span><span class="sxs-lookup"><span data-stu-id="cf4d8-163">Improving the Example - Mock Data</span></span>

<span data-ttu-id="cf4d8-p111">В идеале пример должен подходить как для локальной среды программирования, так и для такой, которая размещена в SharePoint. Чтобы обеспечить это, необходимо создать фиктивную модель ViewModel и обновить код веб-части, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p111">Ideally, the sample should work within both the local workbench as well as the SharePoint hosted workbench. To enable this we need to mock our ViewModel and make an update to the web part code as outlined below.</span></span>

### <a name="mock-viewmodel"></a><span data-ttu-id="cf4d8-166">Фиктивная модель ViewModel</span><span class="sxs-lookup"><span data-stu-id="cf4d8-166">Mock ViewModel</span></span>

<span data-ttu-id="cf4d8-p112">Добавьте новый файл с именем **MockSpPnPjsExampleViewModel.ts** к остальным файлам веб-части. Замените содержимое этого файла приведенным ниже кодом. При этом у вас будет тот же набор функций, но с решением можно будет работать в локальной среде, не рассчитывая на доступность SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p112">Add a new file named **MockSpPnPjsExampleViewModel.ts** alongside the other web part files. Update the content of this file using the code below. This will provide the same set of functionality but does not rely on SharePoint being available and will work in the local environment.</span></span>

```TypeScript
import * as ko from 'knockout';
import styles from './SpPnPjsExample.module.scss';
import { ISpPnPjsExampleWebPartProps } from './SpPnPjsExampleWebPart';
import pnp, { List, ListEnsureResult, ItemAddResult } from "sp-pnp-js";
import { ISpPnPjsExampleBindingContext, OrderListItem } from './SpPnPjsExampleViewModel';

export default class MockSpPnPjsExampleViewModel {

    public description: KnockoutObservable<string> = ko.observable('');
    public newItemTitle: KnockoutObservable<string> = ko.observable('');
    public newItemNumber: KnockoutObservable<string> = ko.observable('');
    public items: KnockoutObservableArray<OrderListItem> = ko.observableArray([]);

    public labelClass: string = styles.label;
    public spPnPjsExampleClass: string = styles.spPnPjsExample;
    public containerClass: string = styles.container;
    public rowClass: string = `ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`;
    public buttonClass: string = `ms-Button ${styles.button}`;

    constructor(bindings: ISpPnPjsExampleBindingContext) {
        this.description(bindings.description);

        // When the web part description is updated, change this view model's description.
        bindings.shouter.subscribe((value: string): void => {
            this.description(value);
        }, this, 'description');

        // Load the items
        this.getItems().then((items: OrderListItem[]): void => {
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

### <a name="update-webpart"></a><span data-ttu-id="cf4d8-170">Обновление веб-части</span><span class="sxs-lookup"><span data-stu-id="cf4d8-170">Update Webpart</span></span>

<span data-ttu-id="cf4d8-p113">Наконец, нам необходимо обновить веб-часть, чтобы она использовала фиктивные данные по мере необходимости. Откройте файл **SpPnPjsExampleWebPart.ts**. Импортируйте только что созданный фиктивный сайт ViewModel.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p113">Finally, we need to update the webpart to use the mock data when appropriate. Open the **SpPnPjsExampleWebPart.ts** file. Start by importing the mock ViewModel web just created:</span></span>

```TypeScript
import MockSpPnPjsExampleViewModel from './MockSpPnPjsExampleViewModel';
```

<span data-ttu-id="cf4d8-174">Далее импортируйте типы `Environment` и `EnvironmentType`, которые вы будете использовать для определения типа среды, в которой запущена веб-часть:</span><span class="sxs-lookup"><span data-stu-id="cf4d8-174">Next, import the `Environment` and `EnvironmentType` types that you will use to detect the type of environment the web part is running in:</span></span>

```ts
import { Environment, EnvironmentType } from '@microsoft/sp-core-library';
```

<span data-ttu-id="cf4d8-175">Затем найдите метод `_registerComponent` и измените его, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-175">Then, locate the `_registerComponent` method and update it as shown below:</span></span>

```TypeScript
private _registerComponent(tagName: string): void {
  ko.components.register(
    tagName,
    {
      viewModel: Environment.type === EnvironmentType.Local ?
        MockSpPnPjsExampleViewModel :
        SpPnPjsExampleViewModel,
      template: require('./SpPnPjsExample.template.html'),
      synchronous: false
    }
  );
}
```

<span data-ttu-id="cf4d8-p114">Наконец, введите в консоли команду `gulp serve`, чтобы открыть локальную среду программирования, которая теперь будет работать с фиктивными данными. (Если у вас уже запущен сервер, остановите его работу с помощью клавиш CTRL+C, а затем снова запустите.)</span><span class="sxs-lookup"><span data-stu-id="cf4d8-p114">Finally, type `gulp serve` in the console to bring up the local workbench, which now will work with the mock data. (If you already have the server running, stop it using Ctrl+C and then restart it):</span></span>

```sh
gulp serve
```

![Проект, запущенный в локальной среде программирования с фиктивными данными](../../../images/sp-pnp-js-guide-with-mock-data.png)

## <a name="download-full-example-code"></a><span data-ttu-id="cf4d8-179">Полный пример кода</span><span class="sxs-lookup"><span data-stu-id="cf4d8-179">Download Full Example Code</span></span>

<span data-ttu-id="cf4d8-180">Помните, что вы можете скачать полный пример кода [здесь](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span><span class="sxs-lookup"><span data-stu-id="cf4d8-180">Remember you can find the full sample [here](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/knockout-sp-pnp-js).</span></span>

## <a name="provide-feedback--report-issues"></a><span data-ttu-id="cf4d8-181">Отзывы и отчеты о неполадках</span><span class="sxs-lookup"><span data-stu-id="cf4d8-181">Provide Feedback / Report Issues</span></span>

<span data-ttu-id="cf4d8-182">Если у вас есть отзывы или вы хотите сообщить о проблеме с библиотекой sp-pnp-js, воспользуйтесь [списком проблем](https://github.com/SharePoint/PnP-JS-Core/issues) в этом репозитории.</span><span class="sxs-lookup"><span data-stu-id="cf4d8-182">If you have any feedback or need to report an issue with sp-pnp-js, please use the [issues list](https://github.com/SharePoint/PnP-JS-Core/issues) in that repo.</span></span>
