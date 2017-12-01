---
title: "Подключение к SharePoint с помощью объектной модели JavaScript (JSOM)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cbaaf3811d6975b6fb94d14b451722f396f10cc0
ms.sourcegitcommit: 9c458121628425716442abddbc97a1f61f18a74c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2017
---
# <a name="connect-to-sharepoint-using-the-javascript-object-model-jsom"></a><span data-ttu-id="ed4dc-102">Подключение к SharePoint с помощью объектной модели JavaScript (JSOM)</span><span class="sxs-lookup"><span data-stu-id="ed4dc-102">Connect to SharePoint using the JavaScript Object Model (JSOM)</span></span>

<span data-ttu-id="ed4dc-p101">В прошлом при создании модификаций для SharePoint вы могли использовать объектную модель JavaScript (JSOM) для связи с SharePoint. Это больше не является рекомендуемым подходом (см. раздел **Замечания** ниже), но все еще приемлемо в некоторых случаях, например при переносе кода. В этой статье показано, как использовать SharePoint JSOM при создании решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p101">In the past, when building SharePoint customizations you might have used the SharePoint JavaScript Object Model (JSOM) to communicate with SharePoint. This is no longer the recommended path (see **Considerations** below), but there are still valid use cases such as code migration. This article demonstrates how to use SharePoint JSOM when building solutions on the SharePoint Framework.</span></span>

> <span data-ttu-id="ed4dc-106">**Примечание.** Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки SharePoint Framework](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="ed4dc-106">**Note:** Before following the steps in this article, be sure to [set up your SharePoint Framework development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="ed4dc-107">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="ed4dc-107">Create a New Project</span></span>

<span data-ttu-id="ed4dc-108">С помощью консоли создайте папку для проекта:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-108">From the console, create a new folder for your project:</span></span>

```sh
md react-sharepointlists
```

<span data-ttu-id="ed4dc-109">Перейдите в папку проекта:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-109">Go to the project folder:</span></span>

```sh
cd react-sharepointlists
```

<span data-ttu-id="ed4dc-110">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-110">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="ed4dc-111">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-111">When prompted, enter the following values:</span></span>

- <span data-ttu-id="ed4dc-112">**react-sharepointlists** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="ed4dc-112">**react-sharepointlists** as your solution name.</span></span>
- <span data-ttu-id="ed4dc-113">выберите **Webpart** в качестве типа создаваемого клиентского компонента;</span><span class="sxs-lookup"><span data-stu-id="ed4dc-113">Choose **Webpart** as the client-side component type to be created.</span></span>
- <span data-ttu-id="ed4dc-114">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="ed4dc-114">**Use the current folder** for the location to place the files.</span></span>
- <span data-ttu-id="ed4dc-115">**React** в качестве начальной платформы для создания веб-части;</span><span class="sxs-lookup"><span data-stu-id="ed4dc-115">**React** as the starting framework to build the web part.</span></span>
- <span data-ttu-id="ed4dc-116">**Списки SharePoint** в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="ed4dc-116">**SharePoint lists** as your web part name.</span></span>
- <span data-ttu-id="ed4dc-117">**Показывает имена списков на текущем сайте** в качестве описания веб-части.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-117">**Shows names of lists in the current site** as your web part description.</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/tutorial-spjsom-yo-sharepoint.png)

<span data-ttu-id="ed4dc-119">После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-119">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="ed4dc-120">Далее откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-120">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="ed4dc-121">В этой статье в инструкциях и на снимках экрана указан Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-121">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/tutorial-spjsom-vscode.png)

<span data-ttu-id="ed4dc-123">Чтобы открыть каталог в Visual Studio Code, введите в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-123">To open the directory in Visual Studio Code, from the console type:</span></span>
```sh
code .
```

## <a name="referencing-jsom"></a><span data-ttu-id="ed4dc-124">Создание ссылок на JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-124">Referencing JSOM</span></span>
<span data-ttu-id="ed4dc-p103">Чтобы использовать модель SharePoint JSOM в компоненте SharePoint Framework, необходимо сначала сослаться на нее. В прошлом она была сразу доступна на страницах. В SharePoint Framework ее необходимо загружать в явном виде.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p103">In order to use SharePoint JSOM in your SharePoint Framework component, you must first reference it. In the past it was already available on the page for you to use. In the SharePoint Framework, it has to be explicitly loaded.</span></span>

<span data-ttu-id="ed4dc-128">Сослаться на SharePoint JSOM в SharePoint Framework можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-128">There are two ways to reference SharePoint JSOM in the SharePoint Framework:</span></span> 
- <span data-ttu-id="ed4dc-129">**декларативно** — через конфигурацию;</span><span class="sxs-lookup"><span data-stu-id="ed4dc-129">**Declarative** - through configuration</span></span>
- <span data-ttu-id="ed4dc-130">**принудительно** — через код.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-130">**Imperative** - through code</span></span>

<span data-ttu-id="ed4dc-131">У каждого из этих подходов есть свои преимущества и недостатки, каждый из которых важно понимать.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-131">Each of these approaches have advantages and disadvantages and it's important for you to understand each of them.</span></span>

## <a name="reference-jsom-declaratively"></a><span data-ttu-id="ed4dc-132">Создание декларативной ссылки на JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-132">Reference JSOM Declaratively</span></span>

<span data-ttu-id="ed4dc-p104">Ссылаясь на JSOM декларативно, сначала необходимо зарегистрировать API SharePoint JSOM в качестве внешних сценариев в проекте SharePoint Framework. Откройте в редакторе кода файл **./config/config.json** и добавьте в разделе **externals** следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p104">When referencing JSOM declaratively, the first step is to register the SharePoint JSOM API as external scripts within your SharePoint Framework project. In your code editor, open the **./config/config.json** file and add the following to the **externals** section:</span></span>

```json
{
  // ...
  "externals": {
    "sp-init": {
      "path": "https://contoso.sharepoint.com/_layouts/15/init.js",
      "globalName": "$_global_init"
    },
    "microsoft-ajax": {
      "path": "https://contoso.sharepoint.com/_layouts/15/MicrosoftAjax.js",
      "globalName": "Sys",
      "globalDependencies": [
        "sp-init"
      ]
    },
    "sp-runtime": {
      "path": "https://contoso.sharepoint.com/_layouts/15/SP.Runtime.js",
      "globalName": "SP",
      "globalDependencies": [
        "microsoft-ajax"
      ]
    },
    "sharepoint": {
      "path": "https://contoso.sharepoint.com/_layouts/15/SP.js",
      "globalName": "SP",
      "globalDependencies": [
        "sp-runtime"
      ]
    }
  }
  // ...
}
```

<span data-ttu-id="ed4dc-p105">Каждая запись указывает на один из файлов сценариев, которые в совокупности обеспечивают поддержку SharePoint JSOM в компоненте SPFx. Эти сценарии распространяются в виде немодульных сценариев, поэтому для каждой записи регистрации необходимо указать URL-адрес (с помощью свойства `path`) и имя, используемое сценарием (с помощью свойства `globalName`). Чтобы эти сценарии загружались в правильном порядке, необходимо указать зависимости между ними с помощью свойства `globalDependencies`.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p105">Each of the entries points to different script files that together allows you to use SharePoint JSOM in your SPFx component. All of these scripts are distributed as non-module scripts. This is why each registration entry requires a URL, (specified using the `path` property) and the name used by the script (provided in the `globalName` property). To ensure that these scripts load in the right order, the dependencies between these scripts are specified using the `globalDependencies` property.</span></span>

<span data-ttu-id="ed4dc-139">В зависимости от используемых функций JSOM могут потребоваться дополнительные скрипты (например, sp.taxonomy.js).</span><span class="sxs-lookup"><span data-stu-id="ed4dc-139">Additional scripts may need to be added depending on the JSOM functionality you are using (e.g. sp.taxonomy.js).</span></span>

### <a name="install-typescript-typings-for-sharepoint-jsom"></a><span data-ttu-id="ed4dc-140">Установка определений типов TypeScript для SharePoint JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-140">Install TypeScript Typings for SharePoint JSOM</span></span>

<span data-ttu-id="ed4dc-p106">Следующий этап — установка и настройка определений типов TypeScript для SharePoint JSOM. Это позволяет пользоваться функциями, обеспечивающими безопасность типов TypeScript при работе с SharePoint JSOM.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p106">The next step is to install and configure TypeScript typings for SharePoint JSOM. This allows you to benefit from TypeScript's type safety features when working with SharePoint JSOM.</span></span>

<span data-ttu-id="ed4dc-143">С помощью консоли выполните в каталоге проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-143">From the console, execute the following command within your project directory:</span></span>

```sh
npm install @types/microsoft-ajax @types/sharepoint --save-dev
```

<span data-ttu-id="ed4dc-p107">Модель SharePoint JSOM не распространяется в виде модуля, поэтому ее невозможно импортировать непосредственно в код. Вместо этого необходимо зарегистрировать определения ее типов TypeScript глобально. Откройте в редакторе кода файл **./tsconfig.json**, а затем в свойстве `types` (сразу после записи **webpack-env**) добавьте ссылки на **microsoft-ajax** и **sharepoint**:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p107">SharePoint JSOM is not distributed as a module and so you cannot import it directly in your code. Instead, you need to register its TypeScript typings globally. In the code editor, open the **./tsconfig.json** file, and in the `types` property, right after the **webpack-env** entry, add references to **microsoft-ajax** and **sharepoint**:</span></span>

```json
{
  "compilerOptions": {
    // ...
    "types": [
      "es6-promise",
      "es6-collections",
      "webpack-env",
      "microsoft-ajax",
      "sharepoint"
    ]
  }
}
```

### <a name="reference-sharepoint-jsom-scripts-in-a-react-component"></a><span data-ttu-id="ed4dc-147">Создание ссылок на сценарии SharePoint JSOM в компоненте React</span><span class="sxs-lookup"><span data-stu-id="ed4dc-147">Reference SharePoint JSOM Scripts in a React Component</span></span>

<span data-ttu-id="ed4dc-p108">Чтобы загружать сценарии SharePoint JSOM в компоненте SPFx, необходимо ссылаться на них в коде компонента. В этом примере мы добавим ссылки в компоненте React, где JSOM будет использоваться для связи с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p108">To load the SharePoint JSOM scripts in your SPFx component, you have to reference them in the component's code. In this example, you will add the references in a React component where JSOM will be used to communicate with SharePoint.</span></span>

<span data-ttu-id="ed4dc-p109">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. После последнего оператора `import` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p109">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. After the last `import` statement add the following code:</span></span>

```ts
require('sp-init');
require('microsoft-ajax');
require('sp-runtime');
require('sharepoint');
```

<span data-ttu-id="ed4dc-152">Эти имена соответствуют добавленным ранее внешним ссылкам, поэтому SharePoint Framework загрузит соответствующие сценарии с указанных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-152">These names correspond to the external references you added previously so SharePoint Framework will load these scripts from the specified URLs.</span></span>

### <a name="show-titles-of-sharepoint-lists-in-the-current-site-using-jsom"></a><span data-ttu-id="ed4dc-153">Отображение названий списков SharePoint на текущем сайте с помощью JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-153">Show Titles of SharePoint Lists in the Current Site Using JSOM</span></span>

<span data-ttu-id="ed4dc-154">Чтобы продемонстрировать связь с SharePoint с помощью SharePoint JSOM, мы создадим и покажем заголовки всех списков SharePoint на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-154">To demonstrate using SharePoint JSOM for communicating with SharePoint, you will retrieve and render the titles of all SharePoint lists located in the current site.</span></span>

#### <a name="add-siteurl-to-the-react-components-properties"></a><span data-ttu-id="ed4dc-155">Добавление свойства _siteUrl_ для компонента React</span><span class="sxs-lookup"><span data-stu-id="ed4dc-155">Add _siteUrl_ to the React Component's Properties</span></span>

<span data-ttu-id="ed4dc-p110">Чтобы подключиться к SharePoint, компонент React должен знать URL-адрес текущего сайта. Этот URL-адрес доступен в родительской веб-части, и его можно передавать компоненту через его свойства.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p110">In order to connect to SharePoint, the React component must know the URL of the current site. That URL is available in the parent web part and can be passed into the component through its properties.</span></span>

<span data-ttu-id="ed4dc-158">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** и добавьте к интерфейсу `ISharePointListsProps` свойство `siteUrl`:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-158">In the code editor, open the **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** file and to the `ISharePointListsProps` interface add the `siteUrl` property:</span></span>

```ts
export interface ISharePointListsProps {
  description: string;
  siteUrl: string;
}
```

<span data-ttu-id="ed4dc-159">Чтобы передать компоненту URL-адрес текущего сайта, откройте файл **./src/webparts/sharePointLists/SharePointListsWebPart.ts** и замените код метода `render` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-159">To pass the URL of the current site into the component, open the **./src/webparts/sharePointLists/SharePointListsWebPart.ts** file in the code editor and change the `render` method to:</span></span>

```ts
export default class SharePointListsWebPart extends BaseClientSideWebPart<ISharePointListsWebPartProps> {
  public render(): void {
    const element: React.ReactElement<ISharePointListsProps > = React.createElement(
      SharePointLists,
      {
        description: this.properties.description,
        siteUrl: this.context.pageContext.web.absoluteUrl
      }
    );

    ReactDom.render(element, this.domElement);
  }

  // ...
}
```

#### <a name="define-the-react-components-state"></a><span data-ttu-id="ed4dc-160">Определение состояния компонента React</span><span class="sxs-lookup"><span data-stu-id="ed4dc-160">Define the React Component's State</span></span>

<span data-ttu-id="ed4dc-p111">Компонент React загрузит данные из SharePoint и покажет их пользователю. Текущее состояние компонента React моделируется с помощью интерфейса состояний, который мы добавим.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p111">The React component will load data from SharePoint and render it to the user. The current state of the React component is modeled using a state interface we will add.</span></span>

<span data-ttu-id="ed4dc-163">С помощью редактора кода создайте в папке **./src/webparts/sharePointLists/components** файл **ISharePointListsState.ts** и вставьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-163">In the code editor, in the **./src/webparts/sharePointLists/components** folder, create a new file named **ISharePointListsState.ts** and paste the following contents:</span></span>

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
}
```

#### <a name="add-state-to-the-react-component"></a><span data-ttu-id="ed4dc-164">Добавление состояния компонента React</span><span class="sxs-lookup"><span data-stu-id="ed4dc-164">Add State to the React component</span></span>

<span data-ttu-id="ed4dc-165">Определив интерфейс, описывающий форму состояния компонента, необходимо сделать так, чтобы компонент React использовал этот интерфейс состояния.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-165">Having defined the interface describing the shape of the component's state, the next step is to have the React component use that state interface.</span></span>

<span data-ttu-id="ed4dc-p112">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Под существующими операторами `import` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p112">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Beneath the existing `import` statements add:</span></span>

```ts
import { ISharePointListsState } from './ISharePointListsState';
```

<span data-ttu-id="ed4dc-168">Затем измените подпись класса `SharePointLists` на следующую:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-168">Next, change the signature of the `SharePointLists` class to:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
}
```

<span data-ttu-id="ed4dc-169">В классе `SharePointLists` добавьте конструктор со значением состояния по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-169">In the `SharePointLists` class, add a constructor with the default state value:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  constructor(props?: ISharePointListsProps, context?: any) {
    super();

    this.state = {
      listTitles: [],
      loadingLists: false,
      error: null
    };
  }

  // ...
}
```

#### <a name="load-information-about-sharepoint-lists-from-the-current-site-using-jsom"></a><span data-ttu-id="ed4dc-170">Загрузка сведений о списках SharePoint с текущего сайта с помощью JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-170">Load Information About SharePoint Lists From the Current Site Using JSOM</span></span>

<span data-ttu-id="ed4dc-171">Пример клиентской веб-части, используемый в этой статье, загружает сведения из списков SharePoint на текущем сайте после нажатия кнопки.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-171">The sample client-side web part used in this article loads information about SharePoint lists in the current site after clicking a button.</span></span>

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="ed4dc-p113">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. В классе `SharePointLists` добавьте метод `getListsTitles`:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p113">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. In the `SharePointLists` class add a new method named `getListsTitles`:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  constructor(props?: ISharePointListsProps, context?: any) {
    super();

    this.state = {
      listTitles: [],
      loadingLists: false,
      error: null
    };

    this.getListsTitles = this.getListsTitles.bind(this);
  }

  // ...

  private getListsTitles(): void {
  }
}
```

<span data-ttu-id="ed4dc-175">Чтобы обеспечить правильное определение области метода, мы привяжем его к веб-части в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-175">To ensure the correct scoping of the method, we bind it to the web part in the constructor.</span></span>

<span data-ttu-id="ed4dc-176">Используйте SharePoint JSOM в методе `getListsTitles`, чтобы загрузить названия списков SharePoint на текущем сайте:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-176">In the `getListsTitles` method, use SharePoint JSOM to load the titles of SharePoint lists in the current site:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  private getListsTitles(): void {
    this.setState({
      loadingLists: true,
      listTitles: [],
      error: null
    });

    const context: SP.ClientContext = new SP.ClientContext(this.props.siteUrl);
    const lists: SP.ListCollection = context.get_web().get_lists();
    context.load(lists, 'Include(Title)');
    context.executeQueryAsync((sender: any, args: SP.ClientRequestSucceededEventArgs): void => {
      const listEnumerator: IEnumerator<SP.List> = lists.getEnumerator();

      const titles: string[] = [];
      while (listEnumerator.moveNext()) {
        const list: SP.List = listEnumerator.get_current();
        titles.push(list.get_title());
      }

      this.setState((prevState: ISharePointListsState, props: ISharePointListsProps): ISharePointListsState => {
        prevState.listTitles = titles;
        prevState.loadingLists = false;
        return prevState;
      });
    }, (sender: any, args: SP.ClientRequestFailedEventArgs): void => {
      this.setState({
        loadingLists: false,
        listTitles: [],
        error: args.get_message()
      });
    });
  }
}
```

<span data-ttu-id="ed4dc-p114">Для начала мы сбрасываем состояние компонента, чтобы сообщить пользователю, что компонент будет загружать сведения из SharePoint. Затем мы создаем новый экземпляр контекста SharePoint с помощью URL-адреса текущего сайта, переданного компоненту через его свойства. С помощью SharePoint JSOM мы загружаем списки с текущего сайта, а для повышения производительности запроса указываем, что следует загружать только свойство `Title`. Затем мы выполняем запрос, вызвав метод `executeQueryAsync` и передав две функции обратного вызова. После выполнения запроса мы просматриваем коллекцию полученных списков, сохраняем их названия в массиве и обновляем состояние компонента.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p114">We start with resetting the component's state to communicate to the user that the component will be loading information from SharePoint. Then, using the URL of the current site passed to the component through its properties, we instantiate a new SharePoint context. Using SharePoint JSOM, we load lists from the current site. To optimize the request for performance, we specify that only the `Title` property should be loaded. Next, we execute the query by calling the `executeQueryAsync` method and passing two callback functions. Once the query is completed, we enumerate through the collection of retrieved lists, store their titles in an array, and update the component's state.</span></span>

#### <a name="render-the-titles-of-sharepoint-lists-in-the-current-site"></a><span data-ttu-id="ed4dc-183">Отображение названий списков SharePoint на текущем сайте</span><span class="sxs-lookup"><span data-stu-id="ed4dc-183">Render the Titles of SharePoint Lists in the Current Site</span></span>

<span data-ttu-id="ed4dc-p115">После загрузки названий списков SharePoint на текущем сайте остается только показать их в компоненте. Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx** и обновите метод `render`:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p115">Having loaded the titles of SharePoint lists in the current site, the final step is to render them in the component. In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file and update the `render` method:</span></span>

```tsx
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public render(): React.ReactElement<ISharePointListsProps> {
    const titles: JSX.Element[] = this.state.listTitles.map((listTitle: string, index: number, listTitles: string[]): JSX.Element => {
      return <li key={index}>{listTitle}</li>;
    });

    return (
      <div className={styles.sharePointLists}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.description)}</p>
              <a className={styles.button} onClick={this.getListsTitles} role="button">
                <span className={styles.label}>Get lists titles</span>
              </a><br />
              {this.state.loadingLists &&
                <span>Loading lists...</span>}
              {this.state.error &&
                <span>An error has occurred while loading lists: {this.state.error}</span>}
              {this.state.error === null && titles &&
                <ul>
                  {titles}
                </ul>}
            </div>
          </div>
        </div>
      </div>
    );
  }
  // ...
}
```

<span data-ttu-id="ed4dc-p116">На этом этапе у вас должна быть возможность добавить веб-часть на страницу и просмотреть названия списков SharePoint на текущем сайте. Чтобы убедиться, что проект работает надлежащим образом, выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p116">At this point, you should be able to add your web part to the page and see the titles of SharePoint lists in the current site. To verify that the project is working correctly, run the following command from the console:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="ed4dc-188">Мы используем SharePoint JSOM для связи с SharePoint, поэтому веб-часть необходимо протестировать с помощью размещенной версии рабочего места SharePoint (именно поэтому указывается параметр `--nobrowser` — он предотвращает автоматическую загрузку локального рабочего места).</span><span class="sxs-lookup"><span data-stu-id="ed4dc-188">As you are using SharePoint JSOM to communicate with SharePoint, you have to test the web part using the hosted version of the SharePoint workbench (which is why the `--nobrowser` parameter is specified to prevent the automatic loading of the local workbench).</span></span>

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="ed4dc-p117">Декларативные ссылки на сценарии SharePoint JSOM (как на внешние сценарии) удобно использовать, и они делают код более удобочитаемым. Недостаток этого способа заключается в том, что необходимо указывать абсолютные URL-адреса источников, из которых загружаются сценарии SharePoint JSOM. Если вы используете отдельные клиенты SharePoint для разработки, тестирования и работы, то потребуется приложить дополнительные усилия, чтобы изменить эти URL-адреса для разных сред. В таких случаях также можно принудительно ссылаться на JSOM с помощью класса [SPComponentLoader](https://dev.office.com/sharepoint/reference/spfx/sp-loader/spcomponentloader), чтобы загружать сценарии в коде компонента SPFx.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p117">Referencing SharePoint JSOM scripts declaratively as external scripts is convenient and allows you to keep your code clean. One disadvantage, however, is that it requires specifying absolute URLs to the location from which SharePoint JSOM scripts should be loaded. If you're using separate SharePoint tenants for development, testing, and production, then it will require some additional work to change these URLs for the different environments accordingly. In such cases, you may consider referencing JSOM imperatively by using the [SPComponentLoader](https://dev.office.com/sharepoint/reference/spfx/sp-loader/spcomponentloader) to load the scripts in the SPFx component's code.</span></span>

## <a name="reference-jsom-imperatively"></a><span data-ttu-id="ed4dc-194">Создание принудительной ссылки на JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-194">Reference JSOM imperatively</span></span>

<span data-ttu-id="ed4dc-p118">Еще один способ загрузки библиотек JavaScript в проектах SharePoint Framework — использование класса `SPComponentLoader`. `SPComponentLoader` — это вспомогательный класс SharePoint Framework, призванный помочь вам загружать сценарии и другие ресурсы в своих компонентах. Одно из преимуществ класса `SPComponentLoader` по сравнению с декларативной загрузкой сценариев заключается в том, что вы можете использовать URL-адреса относительно сервера. Это удобно, если для разных этапов разработки используются разные клиенты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p118">Another way to load JavaScript libraries in SharePoint Framework projects, is by using the `SPComponentLoader`. `SPComponentLoader` is a utility class provided with the SharePoint Framework designed to help you load scripts and other resources in your components. One benefit of using the `SPComponentLoader` over loading scripts declaratively is that it allows you to use server-relative URLs which is more convenient when using different SharePoint tenants for the different stages of your development process.</span></span>

> <span data-ttu-id="ed4dc-198">В этом разделе руководства рассматривается изменение кода, создание которого описывается в разделе "Создание декларативной ссылки на JSOM" выше.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-198">For this portion of the tutorial, we'll be adjusting the code we created previously in the Declarative section above.</span></span>

### <a name="declarative-reference-cleanup"></a><span data-ttu-id="ed4dc-199">Удаление декларативных ссылок</span><span class="sxs-lookup"><span data-stu-id="ed4dc-199">Declarative Reference Cleanup</span></span>

<span data-ttu-id="ed4dc-200">Если вы выполнили действия из разделов, посвященных декларативным ссылкам, то вам потребуется удалить эти ссылки.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-200">If you followed the steps in the declarative reference sections above, you'll need to remove those references.</span></span>

<span data-ttu-id="ed4dc-p119">Для начала удалите имеющиеся ссылки на внешние сценарии. Откройте в редакторе кода файл **./config/config.json** и удалите из свойства **externals** все записи:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p119">First, remove the existing external script references. In the code editor, open the **./config/config.json** file and from the **externals** property, remove all entries:</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/config.2.0.schema.json",
  "version": "2.0",
  "bundles": {
    "share-point-lists-web-part": {
      "components": [
        {
          "entrypoint": "./lib/webparts/sharePointLists/SharePointListsWebPart.js",
          "manifest": "./src/webparts/sharePointLists/SharePointListsWebPart.manifest.json"
        }
      ]
    }
  },
  "externals": {},
  "localizedResources": {
    "SharePointListsWebPartStrings": "lib/webparts/sharePointLists/loc/{locale}.js"
  }
}
```

<span data-ttu-id="ed4dc-203">Так как сценарии SharePoint JSOM больше не регистрируются как внешние сценарии, на них невозможно ссылаться в коде напрямую.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-203">With the SharePoint JSOM scripts no longer being registered as external scripts, you cannot reference them directly in your code.</span></span>

<span data-ttu-id="ed4dc-204">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx** и удалите операторы `require`, указывающие на разные сценарии SharePoint JSOM.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-204">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file and remove the `require` statements pointing to the different SharePoint JSOM scripts.</span></span>

### <a name="wait-to-load-data-until-the-jsom-scripts-are-loaded"></a><span data-ttu-id="ed4dc-205">Задержка загрузки данных до загрузки сценариев JSOM</span><span class="sxs-lookup"><span data-stu-id="ed4dc-205">Wait to Load Data Until the JSOM Scripts are Loaded</span></span>

<span data-ttu-id="ed4dc-p120">Основные функции создаваемой в этом руководстве клиентской веб-части зависят от SharePoint JSOM. Загрузка этих сценариев может занимать некоторое время, зависящее от ряда факторов. Это следует учитывать при создании компонентов SPFx, использующих JSOM. При добавлении на страницу веб-часть должна сообщать пользователю, что она загружает необходимые компоненты, и давать ему понять, когда она готова к использованию. Для этого необходимо расширить состояние компонента React с помощью дополнительного свойства, позволяющего отслеживать состояние загрузки сценариев JSOM.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p120">The primary functionality of the client-side web part that we are building in this tutorial depends on SharePoint JSOM. Depending on a number of factors, loading these scripts could take a few moments. When building SPFx components that utilize JSOM, you should take that into account. When added to the page, the web part should communicate to the user that it's loading its prerequisites and should make it clear when it's ready to be used. To support this, extend the React component's state with an additional property to track the status of loading the JSOM scripts.</span></span>

<span data-ttu-id="ed4dc-211">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/ISharePointListsState.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-211">In the code editor, open the **./src/webparts/sharePointLists/components/ISharePointListsState.ts** file and paste the following code:</span></span>

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
    loadingScripts: boolean;
}
```

<span data-ttu-id="ed4dc-p121">Затем добавьте новое свойство к определениям состояний в компоненте React. Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Обновите конструктор, вставив следующий код:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p121">Next, add the newly added property to the state definitions in the React component. In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Update the constructor to the following code:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  constructor(props?: ISharePointListsProps, context?: any) {
    super();

    this.state = {
      listTitles: [],
      loadingLists: false,
      error: null,
      loadingScripts: true
    };

    this.getListsTitles = this.getListsTitles.bind(this);
  }
  // ...
}
```

<span data-ttu-id="ed4dc-215">В том же файле обновите метод `getListsTitles` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-215">In the same file, update the `getListsTitles` method to the following code:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  private getListsTitles(): void {
    this.setState({
      loadingLists: true,
      listTitles: [],
      error: null,
      loadingScripts: false
    });

    const context: SP.ClientContext = new SP.ClientContext(this.props.siteUrl);
    const lists: SP.ListCollection = context.get_web().get_lists();
    context.load(lists, 'Include(Title)');
    context.executeQueryAsync((sender: any, args: SP.ClientRequestSucceededEventArgs): void => {
      const listEnumerator: IEnumerator<SP.List> = lists.getEnumerator();

      const titles: string[] = [];
      while (listEnumerator.moveNext()) {
        const list: SP.List = listEnumerator.get_current();
        titles.push(list.get_title());
      }

      this.setState((prevState: ISharePointListsState, props: ISharePointListsProps): ISharePointListsState => {
        prevState.listTitles = titles;
        prevState.loadingLists = false;
        return prevState;
      });
    }, (sender: any, args: SP.ClientRequestFailedEventArgs): void => {
      this.setState({
        loadingLists: false,
        listTitles: [],
        error: args.get_message(),
        loadingScripts: false
      });
    });
  }
}
```

<span data-ttu-id="ed4dc-216">Чтобы сообщать пользователю о состоянии загрузки сценариев SharePoint JSOM, обновите метод `render` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-216">To communicate the status of loading the SharePoint JSOM scripts to the user, update the `render` method to the following code:</span></span>

```tsx
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public render(): React.ReactElement<ISharePointListsProps> {
    const titles: JSX.Element[] = this.state.listTitles.map((listTitle: string, index: number, listTitles: string[]): JSX.Element => {
      return <li key={index}>{listTitle}</li>;
    });

    return (
      <div className={styles.sharePointLists}>
        <div className={styles.container}>
          {this.state.loadingScripts &&
            <div className="ms-Grid" style={{ color: "#666", backgroundColor: "#f4f4f4", padding: "80px 0", alignItems: "center", boxAlign: "center" }}>
              <div className="ms-Grid-row" style={{ color: "#333" }}>
                <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
                <div className="ms-Grid-col ms-u-sm12 ms-u-md6" style={{ height: "100%", whiteSpace: "nowrap", textAlign: "center" }}>
                  <i className="ms-fontSize-su ms-Icon ms-Icon--CustomList" style={{ display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}></i><span className="ms-fontWeight-light ms-fontSize-xxl" style={{ paddingLeft: "20px", display: "inline-block", verticalAlign: "middle", whiteSpace: "normal" }}>SharePoint lists</span>
                </div>
                <div className="ms-Grid-col ms-u-hiddenSm ms-u-md3"></div>
              </div>
              <div className="ms-Grid-row" style={{ width: "65%", verticalAlign: "middle", margin: "0 auto", textAlign: "center" }}>
                <span style={{ color: "#666", fontSize: "17px", display: "inline-block", margin: "24px 0", fontWeight: 100 }}>Loading SharePoint JSOM scripts...</span>
              </div>
              <div className="ms-Grid-row"></div>
            </div>}
          {this.state.loadingScripts === false &&
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
                <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
                <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
                <p className="ms-font-l ms-fontColor-white">{escape(this.props.description)}</p>
                <a className={styles.button} onClick={this.getListsTitles} role="button">
                  <span className={styles.label}>Get lists titles</span>
                </a><br />
                {this.state.loadingLists &&
                  <span>Loading lists...</span>}
                {this.state.error &&
                  <span>An error has occurred while loading lists: {this.state.error}</span>}
                {this.state.error === null && titles &&
                  <ul>
                    {titles}
                  </ul>}
              </div>
            </div>
          }
        </div>
      </div>
    );
  }
  // ...
}
```

<span data-ttu-id="ed4dc-p122">Когда состояние компонента React указывает на загрузку сценариев SharePoint JSOM, появляется заполнитель. После загрузки сценариев в веб-части появится обычное содержимое с кнопкой, позволяющей пользователям загрузить сведения о списках SharePoint на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p122">When the React component's state indicates that the SharePoint JSOM scripts are being loaded, it will display a placeholder. Once the scripts have been loaded, the web part will display the expected content with the button allowing users to load the information about SharePoint lists in the current site.</span></span>

### <a name="load-sharepoint-jsom-scripts-using-spcomponentloader"></a><span data-ttu-id="ed4dc-219">Загрузка сценариев SharePoint JSOM с помощью класса SPComponentLoader</span><span class="sxs-lookup"><span data-stu-id="ed4dc-219">Load SharePoint JSOM Scripts Using SPComponentLoader</span></span>

<span data-ttu-id="ed4dc-p123">Компоненты SPFx должны загружать сценарии SharePoint JSOM только один раз. В этом примере (при условии, что веб-часть состоит из одного компонента React), загружать сценарии SharePoint JSOM лучше всего в методе `componentDidMount` компонента React, который выполняется только один раз после создания экземпляра компонента.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p123">SPFx components should load SharePoint JSOM scripts only once. In this example, given that the web part consists of a single React component, the best place to load SharePoint JSOM scripts is inside the React component's `componentDidMount` method, which executes only once after the component has been instantiated.</span></span>

<span data-ttu-id="ed4dc-p124">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Добавьте в начале файла оператор `import`, ссылающийся на класс `SPComponentLoader`. Затем в классе `SharePointLists` добавьте метод `componentDidMount`:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p124">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. In the top section of the file, add an `import` statement referencing the `SPComponentLoader`. Then, in the `SharePointLists` class, add the `componentDidMount` method:</span></span>

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';

export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public componentDidMount(): void {
    SPComponentLoader.loadScript('/_layouts/15/init.js', {
      globalExportsName: '$_global_init'
    })
    .then((): Promise<{}> => {
      return SPComponentLoader.loadScript('/_layouts/15/MicrosoftAjax.js', {
        globalExportsName: 'Sys'
      });
    })
    .then((): Promise<{}> => {
      return SPComponentLoader.loadScript('/_layouts/15/SP.Runtime.js', {
        globalExportsName: 'SP'
      });
    })
    .then((): Promise<{}> => {
      return SPComponentLoader.loadScript('/_layouts/15/SP.js', {
        globalExportsName: 'SP'
      });
    })
    .then((): void => {
      this.setState((prevState: ISharePointListsState, props: ISharePointListsProps): ISharePointListsState => {
        prevState.loadingScripts = false;
        return prevState;
      });
    });
  }
  // ...
}
```

<span data-ttu-id="ed4dc-p125">Используя цепочку обещаний, мы загружаем различные сценарии, которые в совокупности обеспечивают поддержку SharePoint JSOM в компоненте SharePoint Framework. Обратите внимание, что благодаря классу `SPComponentLoader` вы можете использовать URL-адреса относительно сервера, которые загружают сценарии из текущего клиента SharePoint. После загрузки всех сценариев необходимо обновить состояние компонента React, подтверждая, что все необходимые компоненты загружены, а веб-часть готова к использованию.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p125">Using a series of chained promises, we load the different scripts that together enable using SharePoint JSOM in your SharePoint Framework component. Note, how by using the `SPComponentLoader` you can use server-relative URLs that will load the scripts from the current SharePoint tenant. Once all scripts have been loaded, you update the React component's state confirming that all prerequisites have been loaded and the web part is ready to use.</span></span>

<span data-ttu-id="ed4dc-228">Убедитесь, что веб-часть работает надлежащим образом, выполнив в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed4dc-228">Confirm that the web part is working as expected by running the following command from the console:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="ed4dc-229">Как и раньше, в веб-части должны появиться названия списков SharePoint на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-229">Just as before, the web part should show the titles of SharePoint lists in the current site.</span></span>

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="ed4dc-231">Для использования класса `SPComponentLoader` требуются дополнительные усилия, но вы получаете возможность указывать URL-адреса относительно сервера. Это удобно в тех случаях, когда для разработки, тестирования и работы используются разные клиенты.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-231">While using the `SPComponentLoader` requires some additional effort, it allows you to use server-relative URLs which is beneficial in scenarios when you're using different tenants for development, testing, and production.</span></span>

## <a name="considerations"></a><span data-ttu-id="ed4dc-232">Замечания</span><span class="sxs-lookup"><span data-stu-id="ed4dc-232">Considerations</span></span>

<span data-ttu-id="ed4dc-p126">В прошлом при создании клиентских модификаций для SharePoint вы могли использовать SharePoint JSOM для связи с SharePoint. Однако в настоящее время рекомендуется использовать REST API SharePoint (напрямую или через [основную библиотеку PnP JavaScript](https://github.com/SharePoint/PnP-JS-Core)).</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p126">In the past, when building client-side customizations on SharePoint you might have used SharePoint JSOM to communicate with SharePoint. However, the recommended approach is to use the SharePoint REST API either directly or through the [PnP JavaScript Core Library](https://github.com/SharePoint/PnP-JS-Core).</span></span>

<span data-ttu-id="ed4dc-p127">Выпуск SharePoint JSOM был первым шагом к поддержке клиентских решений в SharePoint. Но в настоящее время активная поддержка этой модели прекращена, и в ней могут быть доступны не все возможности REST API. Кроме того, независимо от того, используется ли REST API SharePoint напрямую или через основную библиотеку PnP JavaScript, вы можете использовать обещания, что значительно упрощает написание асинхронного кода (оно часто представляло проблему при использовании JSOM).</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p127">When SharePoint JSOM was introduced, it was the first step towards supporting client-side solutions on SharePoint. However, it is no longer being actively maintained and might not offer access to all capabilities available through the REST API. Additionally, whether using the SharePoint REST API directly or through the PnP JavaScript Core Library, you can use promises which significantly simplify writing asynchronous code (a common problem when utilizing JSOM).</span></span>

<span data-ttu-id="ed4dc-238">Несмотря на то что в редких случаях SharePoint JSOM все еще может предоставлять доступ к данным и методам, не поддерживаемым в REST API SharePoint, по мере возможности рекомендуется использовать REST API.</span><span class="sxs-lookup"><span data-stu-id="ed4dc-238">Although there are still a limited number of cases where SharePoint JSOM provides access to data and methods not yet covered by the SharePoint REST API, where possible, the REST API should be preferred.</span></span>

<span data-ttu-id="ed4dc-p128">Если у вас есть модификации с использованием SharePoint JSOM, которые планируется перенести на платформу SharePoint Framework, то в этой статье вы найдете необходимые сведения об использовании SharePoint JSOM в решениях SharePoint Framework. Однако в долгосрочной перспективе рекомендуем изменить решение так, чтобы для связи с SharePoint использовался интерфейс REST API SharePoint (напрямую или через основную библиотеку PnP JavaScript).</span><span class="sxs-lookup"><span data-stu-id="ed4dc-p128">If you have existing customizations using SharePoint JSOM and are considering migrating them to the SharePoint Framework, this article should provide you with the necessary information about using SharePoint JSOM in SharePoint Framework solutions. Longer term, however, you should consider changing how you communicate with SharePoint to either using the SharePoint REST API directly or through the PnP JavaScript Core Library.</span></span>
