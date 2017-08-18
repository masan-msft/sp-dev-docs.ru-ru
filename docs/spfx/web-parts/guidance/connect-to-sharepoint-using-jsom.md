# <a name="connect-to-sharepoint-using-the-javascript-object-model-jsom"></a><span data-ttu-id="7a828-101">Подключение к SharePoint с помощью объектной модели JavaScript (JSOM)</span><span class="sxs-lookup"><span data-stu-id="7a828-101">Connect to SharePoint using the JavaScript Object Model (JSOM)</span></span>

<span data-ttu-id="7a828-p101">В прошлом при создании модификаций для SharePoint вы могли использовать объектную модель JavaScript (JSOM) для связи с SharePoint. Это больше не является рекомендуемым подходом (см. раздел **Замечания** ниже), но все еще приемлемо в некоторых случаях, например при переносе кода. В этой статье показано, как использовать SharePoint JSOM при создании решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="7a828-p101">In the past, when building SharePoint customizations you might have used the SharePoint JavaScript Object Model (JSOM) to communicate with SharePoint. This is no longer the recommended path (see **Considerations** below), but there are still valid use cases such as code migration. This article demonstrates how to use SharePoint JSOM when building solutions on the SharePoint Framework.</span></span>

> <span data-ttu-id="7a828-105">**Примечание.** Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки SharePoint Framework](../../set-up-your-development-environment).</span><span class="sxs-lookup"><span data-stu-id="7a828-105">**Note:** Before following the steps in this article, be sure to [set up your development environment](../../set-up-your-development-environment) for building SharePoint Framework solutions.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="7a828-106">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="7a828-106">Create a New Project</span></span>

<span data-ttu-id="7a828-107">С помощью консоли создайте папку для проекта:</span><span class="sxs-lookup"><span data-stu-id="7a828-107">From the console, create a new folder for your project:</span></span>

```sh
md react-sharepointlists
```

<span data-ttu-id="7a828-108">Перейдите в папку проекта:</span><span class="sxs-lookup"><span data-stu-id="7a828-108">Go to the project folder.</span></span>

```sh
cd react-sharepointlists
```

<span data-ttu-id="7a828-109">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="7a828-109">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="7a828-110">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="7a828-110">When prompted, enter the following values:</span></span>

- <span data-ttu-id="7a828-111">**react-sharepointlists** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="7a828-111">**react-sharepointlists** as your solution name.</span></span>
- <span data-ttu-id="7a828-112">выберите **Webpart** в качестве типа создаваемого клиентского компонента;</span><span class="sxs-lookup"><span data-stu-id="7a828-112">Choose **Extension (Preview)** as the client-side component type to be created.</span></span>
- <span data-ttu-id="7a828-113">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="7a828-113">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="7a828-114">**React** в качестве начальной платформы для создания веб-части;</span><span class="sxs-lookup"><span data-stu-id="7a828-114">**React** as the starting point to build the web part</span></span>
- <span data-ttu-id="7a828-115">**Списки SharePoint** в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="7a828-115">**SharePoint lists** as your web part name.</span></span>
- <span data-ttu-id="7a828-116">**Показывает имена списков на текущем сайте** в качестве описания веб-части.</span><span class="sxs-lookup"><span data-stu-id="7a828-116">**Shows names of lists in the current site** as your web part description.</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../../images/tutorial-spjsom-yo-sharepoint.png)

<span data-ttu-id="7a828-p102">Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="7a828-p102">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../../images/tutorial-spjsom-vscode.png)

<span data-ttu-id="7a828-121">Чтобы открыть каталог в Visual Studio Code, введите в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7a828-121">To open the directory in Visual Studio Code, from the console type:</span></span>
```sh
code .
```

## <a name="referencing-jsom"></a><span data-ttu-id="7a828-122">Создание ссылок на JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-122">Referencing JSOM</span></span>
<span data-ttu-id="7a828-p103">Чтобы использовать модель SharePoint JSOM в компоненте SharePoint Framework, необходимо сначала сослаться на нее. В прошлом она была сразу доступна на страницах. В SharePoint Framework ее необходимо загружать в явном виде.</span><span class="sxs-lookup"><span data-stu-id="7a828-p103">In order to use the SharePoint JSOM in your SharePoint Framework client-side web part, you have to reference it first. Where in the past it was already available on the page for you to use, in SharePoint Framework solutions, it has to be explicitly loaded.</span></span>

<span data-ttu-id="7a828-126">Сослаться на SharePoint JSOM в SharePoint Framework можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="7a828-126">There are two ways to reference SharePoint JSOM in the SharePoint Framework:</span></span> 
- <span data-ttu-id="7a828-127">**декларативно** — через конфигурацию;</span><span class="sxs-lookup"><span data-stu-id="7a828-127">**Declarative** - through configuration</span></span>
- <span data-ttu-id="7a828-128">**принудительно** — через код.</span><span class="sxs-lookup"><span data-stu-id="7a828-128">**Imperative** - through code</span></span>

<span data-ttu-id="7a828-129">У каждого из этих подходов есть свои преимущества и недостатки, каждый из которых важно понимать.</span><span class="sxs-lookup"><span data-stu-id="7a828-129">Each of these approaches have advantages and disadvantages and it's important for you to understand each of them.</span></span>

## <a name="reference-jsom-declaratively"></a><span data-ttu-id="7a828-130">Создание декларативной ссылки на JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-130">Reference JSOM declaratively</span></span>

<span data-ttu-id="7a828-p104">Ссылаясь на JSOM декларативно, сначала необходимо зарегистрировать API SharePoint JSOM в качестве внешних сценариев в проекте SharePoint Framework. Откройте в редакторе кода файл **./config/config.json** и добавьте в разделе **externals** следующий код:</span><span class="sxs-lookup"><span data-stu-id="7a828-p104">The first step, is to register the SharePoint JSOM API as external scripts in your SharePoint Framework project. In the code editor open the ./config/config.json file and to the externals section add:</span></span>

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

<span data-ttu-id="7a828-p105">Каждая запись указывает на один из файлов сценариев, которые в совокупности обеспечивают поддержку SharePoint JSOM в компоненте SPFx. Эти сценарии распространяются в виде немодульных сценариев, поэтому для каждой записи регистрации необходимо указать URL-адрес (с помощью свойства `path`) и имя, используемое сценарием (с помощью свойства `globalName`). Чтобы эти сценарии загружались в правильном порядке, необходимо указать зависимости между ними с помощью свойства `globalDependencies`.</span><span class="sxs-lookup"><span data-stu-id="7a828-p105">Each of the entries points to a different script file that together allow you to use the SharePoint JSOM in your client-side web part. All these scripts are distributed as non-module scripts, which is why each registration entry requires a URL, specified using the path`path` property, and the name used by the script, provided in the globalName`globalName` property. To ensure that these scripts load in the right order, the dependencies between these scripts are specified using the globalDependencies`globalDependencies` property.</span></span>

<span data-ttu-id="7a828-137">В зависимости от используемых функций JSOM могут потребоваться дополнительные скрипты (например, sp.taxonomy.js).</span><span class="sxs-lookup"><span data-stu-id="7a828-137">Additional scripts may need to be added depending on the JSOM functionality you are using (e.g. sp.taxonomy.js).</span></span>

### <a name="install-typescript-typings-for-sharepoint-jsom"></a><span data-ttu-id="7a828-138">Установка определений типов TypeScript для SharePoint JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-138">Install TypeScript typings for SharePoint JSOM</span></span>

<span data-ttu-id="7a828-p106">Следующий этап — установка и настройка определений типов TypeScript для SharePoint JSOM. Это позволяет пользоваться функциями, обеспечивающими безопасность типов TypeScript при работе с SharePoint JSOM.</span><span class="sxs-lookup"><span data-stu-id="7a828-p106">The next step is to install and configure TypeScript typings for SharePoint JSOM. This will allow you to benefit of the TypeScript's type safety features when working with SharePoint JSOM.</span></span>

<span data-ttu-id="7a828-141">С помощью консоли выполните в каталоге проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7a828-141">From the console, execute the following command within your project directory:</span></span>

```sh
npm install @types/microsoft-ajax @types/sharepoint --save-dev
```

<span data-ttu-id="7a828-p107">Модель SharePoint JSOM не распространяется в виде модуля, поэтому ее невозможно импортировать непосредственно в код. Вместо этого необходимо зарегистрировать определения ее типов TypeScript глобально. Откройте в редакторе кода файл **./tsconfig.json**, а затем в свойстве `types` (сразу после записи **webpack-env**) добавьте ссылки на **microsoft-ajax** и **sharepoint**:</span><span class="sxs-lookup"><span data-stu-id="7a828-p107">Because SharePoint JSOM is not distributed as a module and you cannot import it directly in your code, you have to register its TypeScript typings globally. In the code editor, open the **./tsconfig.json** file, and in the types`types` property, right after the **webpack-env** entry, add references to **microsoft-ajax** and **sharepoint**.</span></span>

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

### <a name="reference-sharepoint-jsom-scripts-in-a-react-component"></a><span data-ttu-id="7a828-145">Создание ссылок на сценарии SharePoint JSOM в компоненте React</span><span class="sxs-lookup"><span data-stu-id="7a828-145">Reference SharePoint JSOM Scripts in a React Component</span></span>

<span data-ttu-id="7a828-p108">Чтобы загружать сценарии SharePoint JSOM в компоненте SPFx, необходимо ссылаться на них в коде компонента. В этом примере мы добавим ссылки в компоненте React, где JSOM будет использоваться для связи с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7a828-p108">To load the SharePoint JSOM scripts in the client-side web part, you have to reference them in the web part's code. In this example you will add the references in the React component, where JSOM will be used to communicate with SharePoint.</span></span>

<span data-ttu-id="7a828-p109">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. После последнего оператора `import` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7a828-p109">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. After the last import`import` statement add the following code:</span></span>

```ts
require('sp-init');
require('microsoft-ajax');
require('sp-runtime');
require('sharepoint');
```

<span data-ttu-id="7a828-150">Эти имена соответствуют добавленным ранее внешним ссылкам, поэтому SharePoint Framework загрузит соответствующие сценарии с указанных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="7a828-150">As these names correspond to the external references you added previously, SharePoint Framework will load these script from the specified URLs.</span></span>

### <a name="show-titles-of-sharepoint-lists-in-the-current-site-using-jsom"></a><span data-ttu-id="7a828-151">Отображение названий списков SharePoint на текущем сайте с помощью JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-151">Show titles of SharePoint lists in the current site using JSOM</span></span>

<span data-ttu-id="7a828-152">Чтобы продемонстрировать связь с SharePoint с помощью SharePoint JSOM, мы создадим и покажем заголовки всех списков SharePoint на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="7a828-152">To illustrate using SharePoint JSOM for communicating with SharePoint, you will retrieve and render the titles of all SharePoint lists located in the current site.</span></span>

#### <a name="add-siteurl-to-the-react-components-properties"></a><span data-ttu-id="7a828-153">Добавление свойства _siteUrl_ для компонента React</span><span class="sxs-lookup"><span data-stu-id="7a828-153">Add _siteUrl_ to the React Component's Properties</span></span>

<span data-ttu-id="7a828-p110">Чтобы подключиться к SharePoint, компонент React должен знать URL-адрес текущего сайта. Этот URL-адрес доступен в родительской веб-части, и его можно передавать компоненту через его свойства.</span><span class="sxs-lookup"><span data-stu-id="7a828-p110">In order to connect to SharePoint, the React component must know the URL of the current site. That URL is available in the parent web part and can be passed into the component through its properties.</span></span>

<span data-ttu-id="7a828-156">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** и добавьте к интерфейсу `ISharePointListsProps` свойство `siteUrl`:</span><span class="sxs-lookup"><span data-stu-id="7a828-156">In the code editor, open the **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** file and to the ISharePointListsProps`ISharePointListsProps` interface add the siteUrl`siteUrl` property:</span></span>

```ts
export interface ISharePointListsProps {
  description: string;
  siteUrl: string;
}
```

<span data-ttu-id="7a828-157">Чтобы передать компоненту URL-адрес текущего сайта, откройте файл **./src/webparts/sharePointLists/SharePointListsWebPart.ts** и замените код метода `render` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="7a828-157">To pass the URL of the current site into the component, in the code editor, open the **./src/webparts/sharePointLists/SharePointListsWebPart.ts** file and change the render`render` method to:</span></span>

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

#### <a name="define-the-react-components-state"></a><span data-ttu-id="7a828-158">Определение состояния компонента React</span><span class="sxs-lookup"><span data-stu-id="7a828-158">Define the React Component's State</span></span>

<span data-ttu-id="7a828-p111">Компонент React загрузит данные из SharePoint и покажет их пользователю. Текущее состояние компонента React моделируется с помощью интерфейса состояний, который мы добавим.</span><span class="sxs-lookup"><span data-stu-id="7a828-p111">The React component will load data from SharePoint and render it to the user. The current state of the React component is modeled using a state interface.</span></span>

<span data-ttu-id="7a828-161">С помощью редактора кода создайте в папке **./src/webparts/sharePointLists/components** файл **ISharePointListsState.ts** и вставьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="7a828-161">In the code editor, in the **./src/webparts/sharePointLists/components** folder, create a new file named **ISharePointListsState.ts** and paste the following contents:</span></span>

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
}
```

#### <a name="add-state-to-the-react-component"></a><span data-ttu-id="7a828-162">Добавление состояния компонента React</span><span class="sxs-lookup"><span data-stu-id="7a828-162">Add state to the React component</span></span>

<span data-ttu-id="7a828-163">Определив интерфейс, описывающий форму состояния компонента, необходимо сделать так, чтобы компонент React использовал этот интерфейс состояния.</span><span class="sxs-lookup"><span data-stu-id="7a828-163">Having defined the interface describing the shape of the component's state, the next step is to have the React component use that state interface.</span></span>

<span data-ttu-id="7a828-p112">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Под существующими операторами `import` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7a828-p112">In the code editor, open the ./src/webparts/sharePointLists/components/SharePointLists.tsx file. To the list of import statements add:</span></span>

```ts
import { ISharePointListsState } from './ISharePointListsState';
```

<span data-ttu-id="7a828-166">Затем измените подпись класса `SharePointLists` на следующую:</span><span class="sxs-lookup"><span data-stu-id="7a828-166">Next, change the signature of the SharePointLists`SharePointLists` class to:</span></span>

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
}
```

<span data-ttu-id="7a828-167">В классе `SharePointLists` добавьте конструктор со значением состояния по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="7a828-167">In the SharePointLists`SharePointLists` class add a constructor with the default state value.</span></span>

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

#### <a name="load-information-about-sharepoint-lists-from-the-current-site-using-jsom"></a><span data-ttu-id="7a828-168">Загрузка сведений о списках SharePoint с текущего сайта с помощью JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-168">Load information about SharePoint lists from the current site using JSOM</span></span>

<span data-ttu-id="7a828-169">Пример клиентской веб-части, используемый в этой статье, загружает сведения из списков SharePoint на текущем сайте после нажатия кнопки.</span><span class="sxs-lookup"><span data-stu-id="7a828-169">The sample client-side web part used in this article loads information about SharePoint lists in the current site after clicking a button.</span></span>

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="7a828-p113">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. В классе `SharePointLists` добавьте метод `getListsTitles`:</span><span class="sxs-lookup"><span data-stu-id="7a828-p113">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. In the SharePointLists`SharePointLists` class add a new method named getListsTitles`getListsTitles`:</span></span>

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

<span data-ttu-id="7a828-173">Чтобы обеспечить правильное определение области метода, мы привяжем его к веб-части в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="7a828-173">To ensure the correct scoping of the method, bind it to the web part in the constructor.</span></span>

<span data-ttu-id="7a828-174">Используйте SharePoint JSOM в методе `getListsTitles`, чтобы загрузить названия списков SharePoint на текущем сайте:</span><span class="sxs-lookup"><span data-stu-id="7a828-174">In the getListsTitles`getListsTitles` method, use SharePoint JSOM to load the titles of SharePoint lists in the current site:</span></span>

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

<span data-ttu-id="7a828-p114">Для начала мы сбрасываем состояние компонента, чтобы сообщить пользователю, что компонент будет загружать сведения из SharePoint. Затем мы создаем новый экземпляр контекста SharePoint с помощью URL-адреса текущего сайта, переданного компоненту через его свойства. С помощью SharePoint JSOM мы загружаем списки с текущего сайта, а для повышения производительности запроса указываем, что следует загружать только свойство `Title`. Затем мы выполняем запрос, вызвав метод `executeQueryAsync` и передав две функции обратного вызова. После выполнения запроса мы просматриваем коллекцию полученных списков, сохраняем их названия в массиве и обновляем состояние компонента.</span><span class="sxs-lookup"><span data-stu-id="7a828-p114">You start with resetting the component's state to communicate to the user that the component will be loading information from SharePoint. Then, using the URL of the current site passed to the component through its properties, you instantiate a new SharePoint context. Using the SharePoint JSOM you load lists from the current site, and to optimize the request for performance, you specify, that only the Title`Title` property should be loaded. Next, you execute the query by calling the executeQueryAsync`executeQueryAsync` method and passing two callback functions. Once the query is completed, you enumerate through the collection of retrieved lists, store their titles in an array and update the component's state.</span></span>

#### <a name="render-the-titles-of-sharepoint-lists-in-the-current-site"></a><span data-ttu-id="7a828-181">Отображение названий списков SharePoint на текущем сайте</span><span class="sxs-lookup"><span data-stu-id="7a828-181">Render the titles of SharePoint lists in the current site</span></span>

<span data-ttu-id="7a828-p115">После загрузки названий списков SharePoint на текущем сайте остается только показать их в компоненте. Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx** и обновите метод `render`:</span><span class="sxs-lookup"><span data-stu-id="7a828-p115">Having loaded the titles of SharePoint lists in the current site, the last part left, is to render them in the component. In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file and update the render`render` method:</span></span>

```tsx
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public render(): React.ReactElement<ISharePointListsProps> {
    const titles: JSX.Element[] = this.state.listTitles.map((listTitle: string, index: number, listTitles: string[]): JSX.Element => {
      return <li key={index}>{listTitle}</li>;
    });

    return (
      <div className={styles.helloWorld}>
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

<span data-ttu-id="7a828-p116">На этом этапе у вас должна быть возможность добавить веб-часть на страницу и просмотреть названия списков SharePoint на текущем сайте. Чтобы убедиться, что проект работает надлежащим образом, выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7a828-p116">At this point you should be able to add your web part to the page and see the titles of SharePoint lists in the current site. To verify that the project is working correctly, run the following command:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="7a828-186">Мы используем SharePoint JSOM для связи с SharePoint, поэтому веб-часть необходимо протестировать с помощью размещенной версии рабочего места SharePoint (именно поэтому указывается параметр `--nobrowser` — он предотвращает автоматическую загрузку локального рабочего места).</span><span class="sxs-lookup"><span data-stu-id="7a828-186">As you are using SharePoint JSOM to communicate with SharePoint, you have to test the web part using the hosted version of the SharePoint workbench (which is why the `--nobrowser` parameter is specified to prevent the automatic loading of the local workbench).</span></span>

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="7a828-p117">Декларативные ссылки на сценарии SharePoint JSOM (как на внешние сценарии) удобно использовать, и они делают код более удобочитаемым. Недостаток этого способа заключается в том, что необходимо указывать абсолютные URL-адреса источников, из которых загружаются сценарии SharePoint JSOM. Если вы используете отдельные клиенты SharePoint для разработки, тестирования и работы, то потребуется приложить дополнительные усилия, чтобы изменить эти URL-адреса для разных сред. В таких случаях также можно принудительно ссылаться на JSOM с помощью класса [SPComponentLoader](https://dev.office.com/sharepoint/reference/spfx/sp-loader/spcomponentloader), чтобы загружать сценарии в коде компонента SPFx.</span><span class="sxs-lookup"><span data-stu-id="7a828-p117">Referencing SharePoint JSOM scripts declaratively as external scripts is convenient and allows you to keep your code clean. One disadvantage that it has, is that it requires specifying absolute URLs to the location from which SharePoint JSOM scripts should be loaded. If you're using separate SharePoint tenants for development, testing and production, then it would require some additional work from you to change these URLs for the different environments accordingly. In such cases you could also consider using the [SPComponentLoader](https://dev.office.com/sharepoint/reference/spfx/sp-loader/spcomponentloader) to load the scripts in the web part's code.</span></span>

## <a name="reference-jsom-imperatively"></a><span data-ttu-id="7a828-192">Создание принудительной ссылки на JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-192">Reference JSOM imperatively</span></span>

<span data-ttu-id="7a828-p118">Еще один способ загрузки библиотек JavaScript в проектах SharePoint Framework — использование класса `SPComponentLoader`. `SPComponentLoader` — это вспомогательный класс SharePoint Framework, призванный помочь вам загружать сценарии и другие ресурсы в своих компонентах. Одно из преимуществ класса `SPComponentLoader` по сравнению с декларативной загрузкой сценариев заключается в том, что вы можете использовать URL-адреса относительно сервера. Это удобно, если для разных этапов разработки используются разные клиенты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7a828-p118">Another way to load JavaScript libraries in SharePoint Framework projects, is by using the SPComponentLoader. SPComponentLoader is a utility class provided with the SharePoint Framework designed to help you load scripts and other resources in your components. One benefit of using the SPComponentLoader over loading scripts declaratively is, that it allows you to use server-relative URLs which is more convenient if you're using different SharePoint tenants for the different stages of your development process.</span></span>

> <span data-ttu-id="7a828-196">В этом разделе руководства рассматривается изменение кода, создание которого описывается в разделе "Создание декларативной ссылки на JSOM" выше.</span><span class="sxs-lookup"><span data-stu-id="7a828-196">For this portion of the tutorial, we'll be adjusting the code we created previously in the Declarative section above.</span></span>

### <a name="declarative-reference-cleanup"></a><span data-ttu-id="7a828-197">Удаление декларативных ссылок</span><span class="sxs-lookup"><span data-stu-id="7a828-197">Declarative Reference Cleanup</span></span>

<span data-ttu-id="7a828-198">Если вы выполнили действия из разделов, посвященных декларативным ссылкам, то вам потребуется удалить эти ссылки.</span><span class="sxs-lookup"><span data-stu-id="7a828-198">If you followed the steps in the declarative reference sections above, you'll need to remove those references.</span></span>

<span data-ttu-id="7a828-p119">Для начала удалите имеющиеся ссылки на внешние сценарии. Откройте в редакторе кода файл **./config/config.json** и удалите из свойства **externals** все записи:</span><span class="sxs-lookup"><span data-stu-id="7a828-p119">Before you proceed, remove the existing external script references. In the code editor, open the **./config/config.json** file and from the **externals** property, remove all entries:</span></span>

```json
{
  "entries": [
    {
      "entry": "./lib/webparts/sharePointLists/SharePointListsWebPart.js",
      "manifest": "./src/webparts/sharePointLists/SharePointListsWebPart.manifest.json",
      "outputPath": "./dist/share-point-lists.bundle.js"
    }
  ],
  "externals": {},
  "localizedResources": {
    "sharePointListsStrings": "webparts/sharePointLists/loc/{locale}.js"
  }
}
```

<span data-ttu-id="7a828-201">Так как сценарии SharePoint JSOM больше не регистрируются как внешние сценарии, на них невозможно ссылаться в коде напрямую.</span><span class="sxs-lookup"><span data-stu-id="7a828-201">With the SharePoint JSOM scripts no longer being registered as external scripts, you cannot reference them directly in your code.</span></span>

<span data-ttu-id="7a828-202">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx** и удалите операторы `require`, указывающие на разные сценарии SharePoint JSOM.</span><span class="sxs-lookup"><span data-stu-id="7a828-202">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file and remove the require`require` statements pointing to the different SharePoint JSOM scripts.</span></span>

### <a name="wait-to-load-data-until-the-jsom-scripts-are-loaded"></a><span data-ttu-id="7a828-203">Задержка загрузки данных до загрузки сценариев JSOM</span><span class="sxs-lookup"><span data-stu-id="7a828-203">Wait to Load Data Until the JSOM Scripts are Loaded</span></span>

<span data-ttu-id="7a828-p120">Основные функции создаваемой в этом руководстве клиентской веб-части зависят от SharePoint JSOM. Загрузка этих сценариев может занимать некоторое время, зависящее от ряда факторов. Это следует учитывать при создании компонентов SPFx, использующих JSOM. При добавлении на страницу веб-часть должна сообщать пользователю, что она загружает необходимые компоненты, и давать ему понять, когда она готова к использованию. Для этого необходимо расширить состояние компонента React с помощью дополнительного свойства, позволяющего отслеживать состояние загрузки сценариев JSOM.</span><span class="sxs-lookup"><span data-stu-id="7a828-p120">The primary functionality of the client-side web part that you are building, depends on SharePoint JSOM. Depending on a number of factors, loading these scripts could take a moment, and when building the web part you should take it into account. When added to the page, the web part should communicate to the user, that it's loading its prerequisites and should make it clear, when it's ready to use. To support this, extend the React component's state with an additional property to track the status of loading the JSOM scripts.</span></span>

<span data-ttu-id="7a828-209">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/ISharePointListsState.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7a828-209">In the code editor, open the **./src/webparts/sharePointLists/components/ISharePointListsState.ts** file and paste the following code:</span></span>

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
    loadingScripts: boolean;
}
```

<span data-ttu-id="7a828-p121">Затем добавьте новое свойство к определениям состояний в компоненте React. Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Обновите конструктор, вставив следующий код:</span><span class="sxs-lookup"><span data-stu-id="7a828-p121">Next, add the newly added property to the state definitions in the React component. In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. Update the constructor to the following code:</span></span>

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

<span data-ttu-id="7a828-213">В том же файле замените код метода `getListsTitles` на следующий:</span><span class="sxs-lookup"><span data-stu-id="7a828-213">In the same file, update the getListsTitles`getListsTitles` method to the following code:</span></span>

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

<span data-ttu-id="7a828-214">Чтобы сообщать пользователю о состоянии загрузки сценариев SharePoint JSOM, добавьте оператор `import`, ссылающийся на компонент `Placeholder`, и замените код метода `render` на следующий:</span><span class="sxs-lookup"><span data-stu-id="7a828-214">To communicate the status of loading the SharePoint JSOM scripts to the user, add the import`import` statement to reference the Placeholder`Placeholder` component and update the render`render` method to the following code:</span></span>

```tsx
import { Placeholder } from '@microsoft/sp-webpart-base';

export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  public render(): React.ReactElement<ISharePointListsProps> {
    const titles: JSX.Element[] = this.state.listTitles.map((listTitle: string, index: number, listTitles: string[]): JSX.Element => {
      return <li key={index}>{listTitle}</li>;
    });

    return (
      <div className={styles.helloWorld}>
        <div className={styles.container}>
          {this.state.loadingScripts &&
            <Placeholder
              icon={'ms-Icon--CustomList'}
              iconText={'SharePoint lists'}
              description={'Loading SharePoint JSOM scripts...'} />}
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

<span data-ttu-id="7a828-p122">Когда состояние компонента React указывает на загрузку сценариев SharePoint JSOM, появляется стандартный заполнитель SharePoint Framework. После загрузки сценариев в веб-части появится обычное содержимое с кнопкой, позволяющей пользователям загрузить сведения о списках SharePoint на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="7a828-p122">When the React component's state will indicate, that the SharePoint JSOM scripts are being loaded, it will display the standard SharePoint Framework placeholder. Once the scripts have been loaded, the web part will display the standard content with the button allowing users to load the information about SharePoint lists in the current site.</span></span>

### <a name="load-sharepoint-jsom-scripts-using-spcomponentloader"></a><span data-ttu-id="7a828-217">Загрузка сценариев SharePoint JSOM с помощью класса SPComponentLoader</span><span class="sxs-lookup"><span data-stu-id="7a828-217">Load SharePoint JSOM scripts using SPComponentLoader</span></span>

<span data-ttu-id="7a828-p123">Компоненты SPFx должны загружать сценарии SharePoint JSOM только один раз. В этом примере (при условии, что веб-часть состоит из одного компонента React), загружать сценарии SharePoint JSOM лучше всего в методе `componentDidMount` компонента React, который выполняется только один раз после создания экземпляра компонента.</span><span class="sxs-lookup"><span data-stu-id="7a828-p123">The client-side web part should load SharePoint JSOM scripts only once. In this example, given that the web part consists of a single React component, the best place to load SharePoint JSOM scripts, is inside the React component's componentDidMount`componentDidMount` method, which executes only once after the component has been instantiated.</span></span>

<span data-ttu-id="7a828-p124">Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Добавьте в начале файла оператор `import`, ссылающийся на класс `SPComponentLoader`. Затем в классе `SharePointLists` добавьте метод `componentDidMount`:</span><span class="sxs-lookup"><span data-stu-id="7a828-p124">In the code editor, open the **./src/webparts/sharePointLists/components/SharePointLists.tsx** file. In the top section of the file, add an import`import` statement referencing the SPComponentLoader`SPComponentLoader`. Then, in the SharePointLists`SharePointLists` class, add the componentDidMount`componentDidMount` method:</span></span>

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';

export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
  private componentDidMount(): void {
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

<span data-ttu-id="7a828-p125">Используя цепочку обещаний, мы загружаем различные сценарии, которые в совокупности обеспечивают поддержку SharePoint JSOM в компоненте SharePoint Framework. Обратите внимание, что благодаря классу `SPComponentLoader` вы можете использовать URL-адреса относительно сервера, которые загружают сценарии из текущего клиента SharePoint. После загрузки всех сценариев необходимо обновить состояние компонента React, подтверждая, что все необходимые компоненты загружены, а веб-часть готова к использованию.</span><span class="sxs-lookup"><span data-stu-id="7a828-p125">Using a number of chained promises, you load the different scripts, that together enable using SharePoint JSOM in your SharePoint Framework client-side web part. Note, how using the SPComponentLoader you can use server-relative URLs that will load the scripts from the current SharePoint tenant. Once all scripts have been loaded, you update the React component's state, confirming that all prerequisites have been loaded and the web part is ready to use.</span></span>

<span data-ttu-id="7a828-226">Убедитесь, что веб-часть работает надлежащим образом, выполнив в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7a828-226">Confirm, that the web part is working as expected by running the following command:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="7a828-227">Как и раньше, в веб-части должны появиться названия списков SharePoint на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="7a828-227">Just as previously, you should see the web part show the titles of SharePoint lists in the current site.</span></span>

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../../images/tutorial-spjsom-web-part-list-titles.png)

<span data-ttu-id="7a828-229">Для использования класса `SPComponentLoader` требуются дополнительные усилия, но вы получаете возможность указывать URL-адреса относительно сервера. Это удобно в тех случаях, когда для разработки, тестирования и работы используются разные клиенты.</span><span class="sxs-lookup"><span data-stu-id="7a828-229">While using the SPComponentLoader requires some additional effort, it allows you to use server-relative URLs, which is beneficial in scenarios when you're using different tenants for development, testing and production.</span></span>

## <a name="considerations"></a><span data-ttu-id="7a828-230">Замечания</span><span class="sxs-lookup"><span data-stu-id="7a828-230">Considerations</span></span>

<span data-ttu-id="7a828-p126">В прошлом при создании клиентских модификаций для SharePoint вы могли использовать SharePoint JSOM для связи с SharePoint. Однако в настоящее время рекомендуется использовать REST API SharePoint (напрямую или через [основную библиотеку PnP JavaScript](https://github.com/SharePoint/PnP-JS-Core)).</span><span class="sxs-lookup"><span data-stu-id="7a828-p126">In the past, when building client-side customizations on the SharePoint platforms, you might have used SharePoint JSOM to communicate with SharePoint. Currently, the recommended approach is, to use either the SharePoint REST API or the [PnP JavaScript Core Library](https://github.com/SharePoint/PnP-JS-Core).</span></span>

<span data-ttu-id="7a828-p127">Выпуск SharePoint JSOM был первым шагом к поддержке клиентских решений в SharePoint. Но в настоящее время активная поддержка этой модели прекращена, и в ней могут быть доступны не все возможности REST API. Кроме того, независимо от того, используется ли REST API SharePoint напрямую или через основную библиотеку PnP JavaScript, вы можете использовать обещания, что значительно упрощает написание асинхронного кода (оно часто представляло проблему при использовании JSOM).</span><span class="sxs-lookup"><span data-stu-id="7a828-p127">When SharePoint JSOM was introduced, it was the first step towards supporting client-side solutions on SharePoint. However, it is no longer being actively maintained and might not offer access to all capabilities available through the REST API. Additionaly, whether using the SharePoint REST API directly or through the PnP JavaScript Core Library, you can use promises which significantly simplify writing asynchronous code (a common problem when utilizing JSOM).</span></span>

<span data-ttu-id="7a828-236">Несмотря на то что в редких случаях SharePoint JSOM все еще может предоставлять доступ к данным и методам, не поддерживаемым в REST API SharePoint, по мере возможности рекомендуется использовать REST API.</span><span class="sxs-lookup"><span data-stu-id="7a828-236">Although there are still a limited number of cases where SharePoint JSOM provides access to data and methods not yet covered by the SharePoint REST API, where possible, the REST API should be preferred.</span></span>

<span data-ttu-id="7a828-p128">Если у вас есть модификации с использованием SharePoint JSOM, которые планируется перенести на платформу SharePoint Framework, то в этой статье вы найдете необходимые сведения об использовании SharePoint JSOM в решениях SharePoint Framework. Однако в долгосрочной перспективе рекомендуем изменить решение так, чтобы для связи с SharePoint использовался интерфейс REST API SharePoint (напрямую или через основную библиотеку PnP JavaScript).</span><span class="sxs-lookup"><span data-stu-id="7a828-p128">If you have existing customizations using SharePoint JSOM and are considering migrating them to the SharePoint Framework, this article should provide you with the necessary information about using SharePoint JSOM in SharePoint Framework solutions. For the longer term, you should consider changing how you communicate with SharePoint to either using the SharePoint REST API or the PnP JavaScript Core Library.</span></span>
