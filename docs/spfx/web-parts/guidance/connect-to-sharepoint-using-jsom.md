# <a name="connect-to-sharepoint-using-the-javascript-object-model-jsom"></a>Подключение к SharePoint с помощью объектной модели JavaScript (JSOM)

В прошлом при создании модификаций для SharePoint вы могли использовать объектную модель JavaScript (JSOM) для связи с SharePoint. В этой статье показано, как использовать SharePoint JSOM при создании решений на платформе SharePoint Framework.

> **Примечание.** Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки клиентских веб-частей для SharePoint](../../set-up-your-development-environment).

## <a name="create-a-new-project"></a>Создание проекта

Для начала создайте папку проекта.

```sh
md react-sharepointlists
```

Перейдите в папку проекта.

```sh
cd react-sharepointlists
```

В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.

```sh
yo @microsoft/sharepoint
```

Введите следующие значения:

- **react-sharepointlists** в качестве имени решения;
- **Use the current folder** (Использовать текущую папку) в качестве расположения файлов;
- **React** в качестве отправной точки создания веб-части;
- **Списки SharePoint** в качестве имени веб-части;
- **Показывает имена списков на текущем сайте** в качестве описания веб-части.

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../../images/tutorial-spjsom-yo-sharepoint.png)

Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор.

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../../images/tutorial-spjsom-vscode.png)

## <a name="reference-jsom-declaratively"></a>Создание декларативной ссылки на JSOM

Чтобы использовать SharePoint JSOM в клиентской веб-части SharePoint Framework, для начала необходимо сослаться на эту объектную модель. Раньше она была сразу доступна для использования на странице, но в решениях SharePoint Framework ее необходимо загружать в явном виде.

Ссылаться на SharePoint JSOM в SharePoint Framework можно двумя способами: декларативно (через конфигурацию) и принудительно (в коде веб-части). У каждого из этих подходов есть свои преимущества и недостатки, которые важно понимать.

### <a name="register-sharepoint-jsom-api-as-external-scripts"></a>Регистрация API SharePoint JSOM в качестве внешних сценариев

Для начала необходимо зарегистрировать API SharePoint JSOM в качестве внешних сценариев в проекте SharePoint Framework. Откройте в редакторе кода файл **./config/config.json** и добавьте в разделе **externals** следующий код:

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

Каждая запись указывает на один из файлов сценариев, которые в совокупности обеспечивают поддержку SharePoint JSOM в клиентской веб-части. Эти сценарии распространяются в виде немодульных сценариев, поэтому для каждой записи регистрации необходимо указать URL-адрес (с помощью свойства **path**) и имя, используемое сценарием (с помощью свойства **globalName**). Чтобы эти сценарии загружались в правильном порядке, необходимо указать зависимости между ними с помощью свойства **globalDependencies**.

### <a name="install-typescript-typings-for-sharepoint-jsom"></a>Установка определений типов TypeScript для SharePoint JSOM

Следующий этап — установка и настройка определений типов TypeScript для SharePoint JSOM. Это позволит вам пользоваться функциями, обеспечивающими безопасность типов TypeScript при работе с SharePoint JSOM.

Введите в командной строке следующую команду:

```sh
npm install @types/microsoft-ajax @types/sharepoint --save-dev
```

Так как модель SharePoint JSOM не распространяется в виде модуля и ее невозможно импортировать непосредственно в код, необходимо зарегистрировать определения ее типов TypeScript глобально. Откройте в редакторе кода файл **./tsconfig.json**, а затем в свойстве **types** (сразу после записи **webpack-env**) добавьте ссылки на **microsoft-ajax** и **sharepoint**.

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

### <a name="reference-sharepoint-jsom-scripts-in-the-react-component"></a>Создание ссылок на сценарии SharePoint JSOM в компоненте React

Чтобы загружать сценарии SharePoint JSOM в клиентской веб-части, необходимо ссылаться на них в коде веб-части. В этом примере мы добавим ссылки в компоненте React, где JSOM будет использоваться для связи с SharePoint.

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. После последнего оператора **import** добавьте следующий код:

```ts
require('sp-init');
require('microsoft-ajax');
require('sp-runtime');
require('sharepoint');
```

Эти имена соответствуют добавленным ранее внешним ссылкам, поэтому SharePoint Framework загрузит соответствующие сценарии с указанных URL-адресов.

### <a name="show-titles-of-sharepoint-lists-in-the-current-site-using-jsom"></a>Отображение названий списков SharePoint на текущем сайте с помощью JSOM

Чтобы продемонстрировать связь с SharePoint с помощью SharePoint JSOM, мы создадим и покажем заголовки всех списков SharePoint на текущем сайте.

#### <a name="add-siteurl-to-components-properties"></a>Добавление свойства siteUrl для компонента

Чтобы подключиться к SharePoint, компонент React должен знать URL-адрес текущего сайта. Этот URL-адрес доступен в родительской веб-части, и его можно передавать компоненту через его свойства.

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/ISharePointListsProps.ts** и добавьте к интерфейсу **ISharePointListsProps** свойство **siteUrl**:

```ts
export interface ISharePointListsProps {
  description: string;
  siteUrl: string;
}
```

Чтобы передать компоненту URL-адрес текущего сайта, откройте в редакторе кода файл **./src/webparts/sharePointLists/SharePointListsWebPart.ts** и замените код метода **render** на следующий код:

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

#### <a name="define-components-state"></a>Определение состояния компонента

Компонент React загрузит данные из SharePoint и покажет их пользователю. Текущее состояние компонента React моделируется с помощью интерфейса состояний.

С помощью редактора кода создайте в папке **./src/webparts/sharePointLists/components** файл **ISharePointListsState.ts** и вставьте следующий текст:

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
}
```

#### <a name="add-state-to-the-react-component"></a>Добавление состояния компонента React

Определив интерфейс, описывающий форму состояния компонента, необходимо сделать так, чтобы компонент React использовал этот интерфейс состояния.

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. В списке операторов импорта добавьте следующий код:

```ts
import { ISharePointListsState } from './ISharePointListsState';
```

Затем измените подпись класса **SharePointLists** на следующую:

```ts
export default class SharePointLists extends React.Component<ISharePointListsProps, ISharePointListsState> {
  // ...
}
```

В классе **SharePointLists** добавьте конструктор со значением состояния по умолчанию.

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

#### <a name="load-information-about-sharepoint-lists-from-the-current-site-using-jsom"></a>Загрузка сведений о списках SharePoint с текущего сайта с помощью JSOM

Пример клиентской веб-части, используемый в этой статье, загружает сведения из списков SharePoint на текущем сайте после нажатия кнопки.

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../../images/tutorial-spjsom-web-part-list-titles.png)

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. В классе **SharePointLists** добавьте метод **getListsTitles**:

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

Чтобы обеспечить правильное определение области метода, привяжите его к веб-части в конструкторе.

Используйте SharePoint JSOM в методе **getListsTitles**, чтобы загрузить названия списков SharePoint на текущем сайте:

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

Для начала сбросьте состояние компонента, чтобы сообщить пользователю, что компонент будет загружать сведения из SharePoint. Затем создайте новый экземпляр контекста SharePoint с помощью URL-адреса текущего сайта, переданного компоненту через его свойства. С помощью SharePoint JSOM мы загружаем списки с текущего сайта, а для повышения производительности запроса указываем, что следует загружать только свойство **Title**. Затем выполните запрос, вызвав метод **executeQueryAsync** и передав две функции обратного вызова. Завершив выполнение запроса, мы просматриваем коллекцию полученных списков, сохраняем их названия в массиве и обновляем состояние компонента.

#### <a name="render-the-titles-of-sharepoint-lists-in-the-current-site"></a>Отображение названий списков SharePoint на текущем сайте

После загрузки названий списков SharePoint на текущем сайте остается только показать их в компоненте. Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx** и обновите метод **render**:

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

На этом этапе у вас должна быть возможность добавить веб-часть на страницу и просмотреть названия списков SharePoint на текущем сайте. Чтобы убедиться, что проект работает надлежащим образом, выполните следующую команду:

```sh
gulp serve --nobrowser
```

Мы используем SharePoint JSOM для связи с SharePoint, поэтому веб-часть необходимо протестировать с помощью размещенной версии рабочего места SharePoint.

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../../images/tutorial-spjsom-web-part-list-titles.png)

Декларативные ссылки на сценарии SharePoint JSOM (как на внешние сценарии) удобно использовать, и они делают код более удобочитаемым. Недостаток этого способа заключается в том, что необходимо указывать абсолютные URL-адреса источников, из которых загружаются сценарии SharePoint JSOM. Если вы используете отдельные клиенты SharePoint для разработки, тестирования и работы, то потребуется приложить дополнительные усилия, чтобы изменить эти URL-адреса для разных сред. В таких случаях также можно загружать сценарии в коде веб-части с помощью класса [SPComponentLoader](https://dev.office.com/sharepoint/reference/spfx/sp-loader/spcomponentloader).

## <a name="reference-jsom-imperatively"></a>Создание принудительной ссылки на JSOM

Еще один способ загрузки библиотек JavaScript в проектах SharePoint Framework — использование класса SPComponentLoader. SPComponentLoader — это вспомогательный класс SharePoint Framework, призванный помочь вам загружать сценарии и другие ресурсы в своих компонентах. Одно из преимуществ класса SPComponentLoader по сравнению с декларативной загрузкой сценариев заключается в том, что вы можете использовать URL-адреса относительно сервера. Это удобно, если вы используете разные клиенты SharePoint для разных этапов разработки.

### <a name="remove-external-references"></a>Удаление внешних ссылок

Прежде чем продолжить, удалите имеющиеся ссылки на внешние сценарии. Откройте в редакторе кода файл **./config/config.json** и удалите из свойства **externals** все записи:

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

### <a name="remove-references-in-code"></a>Удаление ссылок в коде

Так как сценарии SharePoint JSOM больше не регистрируются как внешние сценарии, на них невозможно ссылаться в коде напрямую.

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx** и удалите операторы **require**, указывающие на разные сценарии SharePoint JSOM.

### <a name="wait-with-loading-data-until-the-jsom-scripts-are-loaded"></a>Задержка загрузки данных до загрузки сценариев JSOM

Основные функции создаваемой клиентской веб-части зависят от SharePoint JSOM. Загрузка этих сценариев может занять некоторое время, зависящее от ряда факторов, и это следует учитывать при создании веб-части. При добавлении на страницу веб-часть должна сообщать пользователю о загрузке необходимых компонентов и ясно показывать, когда она готова к использованию. Для этого необходимо расширить состояние компонента React с помощью дополнительного свойства для отслеживания состояния загрузки сценариев JSOM.

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/ISharePointListsState.ts** и вставьте следующий код:

```ts
export interface ISharePointListsState {
    listTitles: string[];
    loadingLists: boolean;
    error: string;
    loadingScripts: boolean;
}
```

Затем добавьте новое свойство к определениям состояний в компоненте React. Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Обновите конструктор, вставив следующий код:

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

В том же файле замените код метода **getListsTitles** на следующий:

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

Чтобы сообщать пользователю о состоянии загрузки сценариев SharePoint JSOM, добавьте оператор **import**, ссылающийся на компонент **Placeholder**, и замените код метода **render** на следующий:

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

Когда состояние компонента React будет указывать на загрузку сценариев SharePoint JSOM, появится стандартный заполнитель SharePoint Framework. После загрузки сценариев в веб-части появится стандартное содержимое с кнопкой, позволяющей пользователям загрузить сведения о списках SharePoint на текущем сайте.

### <a name="load-sharepoint-jsom-scripts-using-spcomponentloader"></a>Загрузка сценариев SharePoint JSOM с помощью класса SPComponentLoader

Клиентская веб-часть должна загружать сценарии SharePoint JSOM только один раз. В этом примере (при условии, что веб-часть состоит из одного компонента React), загружать сценарии SharePoint JSOM лучше всего в методе **componentDidMount** компонента React, который выполняется только один раз после создания экземпляра компонента.

Откройте в редакторе кода файл **./src/webparts/sharePointLists/components/SharePointLists.tsx**. Добавьте в начале файла оператор **import**, ссылающийся на класс **SPComponentLoader**. Затем в классе **SharePointLists** добавьте метод **componentDidMount**:

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

Используя цепочку обещаний, вы загружаете различные сценарии, которые в совокупности обеспечивают поддержку SharePoint JSOM в клиентской веб-части SharePoint Framework. Обратите внимание, что благодаря классу SPComponentLoader вы можете использовать URL-адреса относительно сервера, которые загружают сценарии из текущего клиента SharePoint. После загрузки всех сценариев необходимо обновить состояние компонента React, подтверждая, что все необходимые компоненты загружены, а веб-часть готова к использованию.

Убедитесь, что веб-часть работает надлежащим образом, выполнив следующую команду:

```sh
gulp serve --nobrowser
```

Как и раньше, в веб-части должны отображаться названия списков SharePoint на текущем сайте.

![Клиентская веб-часть SharePoint Framework с названиями списков SharePoint на текущем сайте](../../../../images/tutorial-spjsom-web-part-list-titles.png)

Для использования класса SPComponentLoader требуются дополнительные усилия, но вы получаете возможность указывать URL-адреса относительно сервера. Это удобно в тех случаях, когда для разработки, тестирования и работы используются разные клиенты.

## <a name="considerations"></a>Замечания

В прошлом при создании клиентских модификаций на платформах SharePoint вы могли использовать SharePoint JSOM для связи с SharePoint. В настоящее время рекомендуется использовать REST API SharePoint или [основную библиотеку PnP JavaScript](https://github.com/SharePoint/PnP-JS-Core).

Модель SharePoint JSOM появилась несколько лет назад и стала первым шагом к обеспечению поддержки клиентских решений на платформах SharePoint. В настоящее время поддержка этой модели не так активна, так что она может предоставлять не все возможности, доступные в REST и основной библиотеке PnP JavaScript.

Еще одно преимущество REST API SharePoint и основной библиотеки PnP JavaScript заключается в том, что в обоих случаях вы можете использовать обещания. Это значительно упрощает написание асинхронного кода.

Если у вас есть модификации с использованием SharePoint JSOM, которые планируется перенести на платформу SharePoint Framework, то в этой статье вы найдете необходимые сведения об использовании SharePoint JSOM в решениях SharePoint Framework. В долгосрочной перспективе рекомендуем изменить решение так, чтобы для связи с SharePoint использовались REST API SharePoint или основная библиотека PnP JavaScript.