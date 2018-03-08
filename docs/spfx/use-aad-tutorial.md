---
title: "Руководство: использование API, защищенных с помощью Azure Active Directory, в SharePoint Framework"
description: "В руководстве по использованию класса AadHttpClient или MSGraphClient рассмотрено подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework."
ms.date: 02/15/2018
ms.prod: sharepoint
ms.openlocfilehash: 26927db641a11ae95eb85b92cc8b255e9a3167bb
ms.sourcegitcommit: b4110530e7dcb42282023a562073e5aebd20db19
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/21/2018
---
# <a name="tutorial-consuming-apis-secured-with-azure-active-directory-within-sharepoint-framework"></a>Руководство: использование API, защищенных с помощью Azure Active Directory, в SharePoint Framework

Очень распространенный бизнес-сценарий для эффективных корпоративных решений — использование REST API, защищенного с помощью Azure Active Directory (Azure AD) и Open Authorization (OAuth 2.0), из решения SharePoint Framework, будь то клиентская веб-часть или расширение.
В SharePoint Framework 1.4.1 или более поздней версии доступен ряд встроенных возможностей, которые легко удовлетворят это бизнес-требование, позволяя использовать Microsoft Graph со специальным набором областей разрешений или любой другой REST API в качестве специальной службы, зарегистрированной в Azure AD.

> [!IMPORTANT]
> В настоящее время `AadHttpClient` и `MSGraphClient` предоставляются в ознакомительных целях и могут меняться. Не следует использовать эти возможности в рабочей среде. Кроме того, обратите внимание, что использование свойств `webApiPermissionRequests` в `package-solution.json` не поддерживается для обычных клиентов.

> [!IMPORTANT]
> Вы можете использовать Microsoft Graph с SharePoint Framework версии, предшествующей 1.4.1, применяя либо встроенный элемент **graphHttpClient** контекста SharePoint Framework, либо вручную реализованный неявный поток OAuth с помощью [ADAL JS](https://github.com/AzureAD/azure-activedirectory-library-for-js). Однако первый подход привязан к предопределенному набору областей разрешений (то есть позволяет выполнять только задачи, предусмотренные корпорацией Майкрософт), а второй подход довольно сложен с точки зрения разработки. Тем не менее в статье [Подключение к API, защищенному с помощью Azure Active Directory](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/web-parts/guidance/connect-to-api-secured-with-aad) вы найдете дополнительные сведения о последнем сценарии.

Из этого пошагового руководства вы узнаете, как создать решение SharePoint Framework со специальным набором областей разрешений, использующее Microsoft Graph.

> [!NOTE]
> Чтобы лучше понять общую архитектуру этой возможности, можете ознакомиться со статьей [Подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework](use-aadhttpclient.md).

## <a name="SolutionOverview"></a>Обзор решения
Прежде чем углубляться в тонкости разработки решения, давайте рассмотрим в общих чертах, что мы будем создавать.
На приведенном ниже снимке экрана показан пользовательский интерфейс клиентской веб-части, с помощью которой можно искать пользователей в текущем клиенте. Поиск основан на Microsoft Graph, и для него требуются разрешения не ниже *User.ReadBasic.All*.

![Пользовательский интерфейс примера приложения](../images/use-aad-tutorial-video.gif)

Как видите, с помощью этой клиентской веб-части можно искать пользователей по имени, а все подходящие пользователи отображаются с помощью компонента **DetailsList** из Office UI Fabric. Кроме того, у веб-части есть настраиваемый параметр, доступный в области свойств, для выбора способа доступа к Microsoft Graph. На самом деле, начиная с SharePoint Framework 1.4.1, вы можете получать доступ к Microsoft Graph при помощи собственного клиента Graph (**MSGraphClient**) или низкоуровневого типа для доступа к любому REST API, защищенному с помощью Azure AD (**AadHttpClient**).

> [!NOTE]
> Полный исходный код этого решения доступен в следующем репозитории GitHub: [spfx-api-scopes-tutorial](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/spfx-api-scopes-tutorial).

## <a name="CreatingTheSolution"></a>Создание решения
В последующих разделах представлено пошаговое руководство по созданию решения. Этот процесс состоит из следующих основных этапов:

* [Создание исходного решения.](#CreatingInitialSolution)
* [Настройка базовых элементов веб-части.](#ConfiguringBaseElements)
* [Настройка запросов на получение разрешений API.](#ConfiguringApiPermissions)
* [Использование Microsoft Graph.](#ConsumingTheGraph)
* [Развертывание решения и предоставление разрешений.](#DeploymentAndPermissionsGrant)
* [Тестирование решения.](#SolutionTesting)

Если вы уже уверенно создаете решения SharePoint Framework, можете пропустить вступительные разделы и перейти непосредственно к разделу [Настройка запросов на получение разрешений API](#ConfiguringApiPermissions).

### <a name="CreatingInitialSolution"></a>Создание исходного решения
Во-первых, если у вас установлена старая версия генератора SharePoint Framework, необходимо обновить ее до версии 1.4.1 или более поздней. Для этого можно просто выполнить следующую команду:

```sh
npm install -g @microsoft/generator-sharepoint
```

В глобальном масштабе будет установлена последняя версия пакета.
Затем необходимо создать решение SharePoint Framework, выполнив указанные ниже действия.

* Создайте в файловой системе папку, где будет храниться исходный код решения, и измените текущий путь, указав эту папку.
* Запустите генератор Yeoman, чтобы выполнить скаффолдинг нового решения.

```sh
yo @microsoft/sharepoint
```
* Выберите следующие параметры:
    * Укажите имя решения (например, *spfx-api-scopes-tutorial*).
    * В качестве целевой среды укажите *SharePoint Online only (latest)* (Только SharePoint Online, последняя версия).
    * Оставьте текущую папку.
    * Укажите, следует ли развертывать решение глобально в целевом клиенте.
    * Выберите тип решения "WebPart".
    * Назовите веб-часть *GraphConsumer*.
    * Добавьте описание.
    * Выберите React в качестве платформы разработки.

![Пользовательский интерфейс генератора Yeoman при скаффолдинге решения SPFx](../images/graphconsumer-yeoman-generator.png)

* Запустите Visual Studio Code (или другой редактор кода) в контексте текущей папки.

```sh
code .
```

### <a name="ConfiguringBaseElements"></a>Настройка базовых элементов веб-части
Настало время настроить исходные элементы клиентской веб-части.

#### <a name="ConfigureCustomProperties"></a>Конфигурация настраиваемых свойств
Создайте файл исходного кода в папке *src/webparts/graphConsumer/components* решения.
Назовите его *ClientMode.ts* и объявите объект TypeScript *enum* с доступными значениями свойства "Режим клиента" веб-части.

```TS
export enum ClientMode {
    aad,
    graph,
}
```

Теперь откройте файл *GraphConsumerWebPart.ts* в папке *src/webparts/graphConsumer* решения.
Измените определение интерфейса **IGraphConsumerWebPartProps**, чтобы он принимал значение типа **ClientMode**.

```TS
export interface IGraphConsumerWebPartProps {
  clientMode: ClientMode;
}
```

Теперь обновите метод **getPropertyPaneConfiguration()** клиентской веб-части так, чтобы он поддерживал выбор вариантов в области свойств. Ниже представлена новая реализация этого метода.

```TS
  protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
    return {
      pages: [
        {
          header: {
            description: strings.PropertyPaneDescription
          },
          groups: [
            {
              groupName: strings.BasicGroupName,
              groupFields: [
                PropertyPaneChoiceGroup('clientMode', {
                  label: strings.ClientModeLabel,
                  options: [
                    { key: ClientMode.aad, text: "AadHttpClient"},
                    { key: ClientMode.graph, text: "MSGraphClient"},
                  ]
                }),              
              ]
            }
          ]
        }
      ]
    };
  }
```

Кроме того, необходимо обновить метод *render* клиентской веб-части, чтобы создавать должным образом настроенный экземпляр компонента React для отрисовки. Ниже представлено определение метода обновления.

```TS
  public render(): void {
    const element: React.ReactElement<IGraphConsumerProps > = React.createElement(
      GraphConsumer,
      {
        clientMode: this.properties.clientMode,
        context: this.context,
      }
    );

    ReactDom.render(element, this.domElement);
  }
```

Напоследок, чтобы приведенный выше код работал, необходимо добавить операторы *import* в самом начале файла *GraphConsumerWebPart.ts*. Ниже представлен обновленный раздел импорта для этого файла.

```TS
import * as React from 'react';
import * as ReactDom from 'react-dom';
import { Version } from '@microsoft/sp-core-library';
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneChoiceGroup
} from '@microsoft/sp-webpart-base';

import * as strings from 'GraphConsumerWebPartStrings';
import GraphConsumer from './components/GraphConsumer';
import { IGraphConsumerProps } from './components/IGraphConsumerProps';
import { ClientMode } from './components/ClientMode';
```

Обратите внимание на импорт элемента управления **PropertyPaneChoiceGroup**, а также импорт перечисления **ClientMode**.

#### <a name="UpdateResourceStrings"></a>Обновление строк ресурсов
Чтобы скомпилировать решение, необходимо обновить файл *mystrings.d.ts* в папке *src/webparts/graphConsumer/loc* этого решения. Потребуется заменить интерфейс, в котором определяется строка ресурсов, на следующий фрагмент кода:

```TS
declare interface IGraphConsumerWebPartStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ClientModeLabel: string;
  SearchFor: string;
  SearchForValidationErrorMessage: string;
}
```

Теперь задайте нужные значения для новых строк ресурсов, обновив файл *en-us.js* в той же папке.

```TS
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "ClientModeLabel": "Client Mode",
    "SearchFor": "Search for",
    "SearchForValidationErrorMessage": "Invalid value for 'Search for' field"
  }
});
```

#### <a name="UpdateStyles"></a>Обновление стиля клиентской веб-части
Как и в случае со строками ресурсов, также необходимо немного изменить файл стилей SCSS. Для этого откройте файл *GraphConsumer.module.scss* в папке *src/webparts/graphConsumer/components* решения. Добавьте следующие классы стилей сразу после класса *.title*:

```SCSS
  .form {
    @include ms-font-l;
    @include ms-fontColor-white;
  }

  label {
    @include ms-fontColor-white;
  }
```

#### <a name="UpdateReactComponent"></a>Обновление компонента React, отображающего веб-часть
Теперь вы можете обновить компонент React **GraphConsumer** в папке *src/webparts/graphConsumer/components* решения.
Для начала необходимо обновить файл *IGraphConsumerProps.ts*, чтобы сделать возможным принятие настраиваемых свойств, необходимых для реализации веб-части. Ниже представлено обновленное содержимое файла *IGraphConsumerProps.ts*.

```TS
import { WebPartContext } from '@microsoft/sp-webpart-base';
import { ClientMode } from './ClientMode';

export interface IGraphConsumerProps {
  clientMode: ClientMode;
  context: WebPartContext;
}
```
Обратите внимание на импорт определения перечисления **ClientMode**, а также на импорт типа **WebPartContext**, который будет использоваться позже.

Создайте интерфейс для хранения состояния компонента React. Создайте файл в папке *src/webparts/graphConsumer/components* и назовите его *IGraphConsumerState.ts*. Ниже представлено определение интерфейса.

```TS
import { IUserItem } from './IUserItem';

export interface IGraphConsumerState {
    users: Array<IUserItem>;
    searchFor: string;
  }
```

Определите интерфейс **IUserItem** (в файле *IUserItem.ts*, хранящемся в папке *src/webparts/graphConsumer/components*). Этот интерфейс импортируется в файл состояния.

```TS
export interface IUserItem {
    displayName: string;
    mail: string;
    userPrincipalName: string;
  }
```

Этот интерфейс будет использоваться для определения структуры пользователей, полученной из текущего клиента и привязанной к компоненту DetailsList в пользовательском интерфейсе.

Пришло время обновить файл *GraphConsumer.tsx*. Для начала добавьте операторы для импорта определенных ранее типов.

```TS
import * as React from 'react';
import styles from './GraphConsumer.module.scss';
import * as strings from 'GraphConsumerWebPartStrings';
import { IGraphConsumerProps } from './IGraphConsumerProps';
import { IGraphConsumerState } from './IGraphConsumerState';
import { ClientMode } from './ClientMode';
import { IUserItem } from './IUserItem';
import { escape } from '@microsoft/sp-lodash-subset';

import {
  autobind,
  PrimaryButton,
  TextField,
  Label,
  DetailsList,
  DetailsListLayoutMode,
  CheckboxVisibility,
  SelectionMode
} from 'office-ui-fabric-react';

import { AadHttpClient } from "@microsoft/sp-http";
import { MSGraphClient } from "@microsoft/sp-client-preview";
```

Обратите внимание на импорт компонентов **IGraphConsumerProps**, **IGraphConsumerState**, **ClientMode** и **IUserItem**. Кроме того, импортируются некоторые компоненты Office UI Fabric, используемые для отрисовки пользовательского интерфейса компонента React.

Сразу после операций импорта определите структуру столбцов для компонента **DetailsList** из Office UI Fabric.

```TS
// Configure the columns for the DetailsList component
let _usersListColumns = [
  {
    key: 'displayName',
    name: 'Display name',
    fieldName: 'displayName',
    minWidth: 50,
    maxWidth: 100,
    isResizable: true
  },
  {
    key: 'mail',
    name: 'Mail',
    fieldName: 'mail',
    minWidth: 50,
    maxWidth: 100,
    isResizable: true
  },
  {
    key: 'userPrincipalName',
    name: 'User Principal Name',
    fieldName: 'userPrincipalName',
    minWidth: 100,
    maxWidth: 200,
    isResizable: true
  },
];
```

Определенный выше массив будет использоваться в параметрах компонента **DetailsList**, как видно по методу *render()* компонента React, который необходимо заменить на приведенный ниже фрагмент кода.

```TS
  public render(): React.ReactElement<IGraphConsumerProps> {
    return (
      <div className={ styles.graphConsumer }>
        <div className={ styles.container }>
          <div className={ styles.row }>
            <div className={ styles.column }>
              <span className={ styles.title }>Search for a user!</span>
              <p className={ styles.form }>
                <TextField 
                    label={ strings.SearchFor } 
                    required={ true } 
                    value={ this.state.searchFor }
                    onChanged={ this._onSearchForChanged }
                    onGetErrorMessage={ this._getSearchForErrorMessage }
                  />
              </p>
              <p className={ styles.form }>
                <PrimaryButton 
                    text='Search' 
                    title='Search' 
                    onClick={ this._search } 
                  />
              </p>
              {
                (this.state.users != null && this.state.users.length > 0) ?
                  <p className={ styles.form }>
                  <DetailsList
                      items={ this.state.users }
                      columns={ _usersListColumns }
                      setKey='set'
                      checkboxVisibility={ CheckboxVisibility.hidden }
                      selectionMode={ SelectionMode.none }
                      layoutMode={ DetailsListLayoutMode.fixedColumns }
                      compact={ true }
                  />
                </p>
                : null
              }
            </div>
          </div>
        </div>
      </div>
    );
  }
```

Кроме того, обновите объявление типа компонента React и добавьте конструктор, скопировав приведенный ниже фрагмент кода.

```TS
export default class GraphConsumer extends React.Component<IGraphConsumerProps, IGraphConsumerState> {

  constructor(props: IGraphConsumerProps, state: IGraphConsumerState) {
    super(props);
    
    // Initialize the state of the component
    this.state = {
      users: [],
      searchFor: ""
    };
  }

```

Для сбора критериев поиска компоненту **TextField** требуются некоторые правила проверки и обработчики событий. Ниже приведена реализация этих методов.

```TS
  @autobind
  private _onSearchForChanged(newValue: string): void {

    // Update the component state accordingly to the current user's input
    this.setState({
      searchFor: newValue,
    });
  }

  private _getSearchForErrorMessage(value: string): string {
    // The search for text cannot contain spaces
    return (value == null || value.length == 0 || value.indexOf(" ") < 0)
      ? ''
      : `${strings.SearchForValidationErrorMessage}`;
  }
```

Компонент **PrimaryButton** вызывает функцию *_search()*, которая определяет, какую клиентскую технологию использовать для Microsoft Graph.

```TS
  @autobind
  private _search(): void {

    console.log(this.props.clientMode);

    // Based on the clientMode value search users
    switch (this.props.clientMode)
    {
      case ClientMode.aad:
        this._searchWithAad();
        break;
      case ClientMode.graph:
      this._searchWithGraph();
      break;
    }
  }
```

Как видите, экземпляр компонента **DetailsList** отрисовывается в методе *render()* на тот случай, если в свойстве *users* состояния компонента имеются элементы.

### <a name="ConfiguringApiPermissions"></a>Настройка запросов на получение разрешений API

Чтобы решение могло использовать Microsoft Graph, а также другие сторонние REST API, в его манифесте необходимо явно объявить требуемые разрешения с точки зрения OAuth.

В SharePoint Framework 1.4.1 или более поздней версии для этого можно настроить свойство *webApiPermissionRequests* в файле *package-solution.json* из папки *config* в решении. Ниже представлен фрагмент этого файла для текущего решения. Достаточно скопировать объявление свойства *webApiPermissionRequests*.

```JSON
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "spfx-api-scopes-tutorial-client-side-solution",
    "id": "841cd609-d821-468d-a6e4-2d207b966cd8",
    "version": "1.0.0.0",
    "includeClientSideAssets": true,
    "skipFeatureDeployment": true,
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      }
    ]
  },
  "paths": {
    "zippedPackage": "solution/spfx-api-scopes-tutorial.sppkg"
  }
}
```

Обратите внимание на объект *webApiPermissionRequests*, представляющий собой массив элементов *webApiPermissionRequest*. Каждый элемент определяет *ресурс* и *область* для запроса на получение разрешений.
*Ресурсом* может быть имя или ObjectId (в Azure AD) ресурса, для которого требуется настроить запрос на получение разрешений. Для Microsoft Graph используется имя "Microsoft Graph", а значение ObjectId не уникально и зависит от клиента.
*Областью* может быть имя области разрешений или уникальный идентификатор этой области разрешений. Это имя можно получить из документации для соответствующего API, а идентификатор должен быть указан в файле манифеста этого API.

> [!NOTE]
> Все доступные области разрешений для Microsoft Graph перечислены в документе [Справочник по разрешениям Microsoft Graph](https://developer.microsoft.com/ru-RU/graph/docs/concepts/permissions_reference). По умолчанию субъекту-службе не назначены явные разрешения на доступ к Microsoft Graph. Однако, запросив маркер доступа для Microsoft Graph, вы получите маркер с областью разрешений `user_impersonation`, с помощью которой можно считывать сведения о пользователях (т. е. `User.Read.All`). Разработчики могут запрашивать дополнительные области разрешений, а администраторы клиентов — предоставлять их. Дополнительные сведения см. в справочной [статье, посвященной использованию AadHttpClient](use-aadhttpclient.md).


Для поиска пользователей и получения свойств *displayName*, *mail* и *userPrincipalName* достаточно разрешения *User.ReadBasic.All*.

Позже мы упакуем и развернем решение, а вам (или администратору) потребуется предоставить запрашиваемые разрешения своему решению. Об этом рассказывается в разделе [Развертывание решения и предоставление разрешений](#DeploymentAndPermissionsGrant).

### <a name="ConsumingTheGraph"></a>Использование Microsoft Graph
Теперь вы можете реализовать методы для использования Microsoft Graph. Как вы узнали из раздела [Обзор решения](#SolutionOverview), использовать Microsoft Graph можно двумя способами:
* с помощью клиентского объекта **AadHttpClient**;
* с помощью клиентского объекта **MSGraphClient**.

Первый представляет собой клиентский объект, удобный для использования любого REST API. Следовательно, с его помощью можно использовать Microsoft Graph, а также любой другой сторонний (или встроенный) REST API.
Второй клиентской объект подходит только для использования Microsoft Graph. Он использует клиентский объект **AadHttpClient** и поддерживает текучий синтаксис пакета SDK Microsoft Graph.

#### <a name="AadHttpClient"></a>Использование AadHttpClient
Чтобы использовать любой REST API с помощью клиентского объекта **AadHttpClient**, достаточно создать экземпляр типа **AadHttpClient**, указав свойство *serviceScope* контекста и URI целевой службы.
Созданный объект предоставит следующие методы:
* *get* (отправляет HTTP-запрос GET);
* *post* (отправляет HTTP-запрос POST);
* *fetch* (отправляет любой HTTP-запрос в зависимости от указанных аргументов *HttpClientConfiguration* и *IHttpClientOptions*).

Все эти методы поддерживают асинхронную модель разработки с использованием JavaScript и TypeScript, поэтому вы можете обрабатывать их результаты с помощью обещаний.

Ниже представлен фрагмент кода метода *_searchWithAad()* из нашего примера решения.

```TS
  private _searchWithAad(): void {

    // Log the current operation
    console.log("Using _searchWithAad() method");

    // Using Graph here, but any 1st or 3rd party REST API that requires Azure AD auth can be used here.
    const aadClient: AadHttpClient = new AadHttpClient(
      this.props.context.serviceScope,
      "https://graph.microsoft.com"
    );

    // Search for the users with givenName, surname, or displayName equal to the searchFor value
    aadClient
      .get(
        `https://graph.microsoft.com/v1.0/users?$select=displayName,mail,userPrincipalName&$filter=(givenName%20eq%20'${escape(this.state.searchFor)}')%20or%20(surname%20eq%20'${escape(this.state.searchFor)}')%20or%20(displayName%20eq%20'${escape(this.state.searchFor)}')`,
        AadHttpClient.configurations.v1
      )
      .then(response => {
        return response.json();
      })
      .then(json => {

        // Prepare the output array
        var users: Array<IUserItem> = new Array<IUserItem>();

        // Log the result in the console for testing purposes
        console.log(json);

        // Map the JSON response to the output array
        json.value.map((item: any) => {
          users.push( { 
            displayName: item.displayName,
            mail: item.mail,
            userPrincipalName: item.userPrincipalName,
          });
        });

        // Update the component state accordingly to the result
        this.setState(
          {
            users: users,
          }
        );
      })
      .catch(error => {
        console.error(error);
      });
  }
```

Как видите, метод *get()* получает URL-адрес запроса OData в качестве входного параметра, а в случае успешного запроса возвращает объект JSON с откликом.

#### <a name="MSGraphClient"></a>Использование MSGraphClient
Если планируете применять Microsoft Graph, можно воспользоваться клиентским объектом **MSGraphClient**, который предоставляет более текучий синтаксис.
В приведенном ниже фрагменте кода показана фактическая реализация метода *_searchWithGraph()* из нашего примера решения.

```TS
  private _searchWithGraph(): void {

    // Log the current operation
    console.log("Using _searchWithGraph() method");

    const graphClient: MSGraphClient = this.props.context.serviceScope.consume(
      MSGraphClient.serviceKey
    );

    // From https://github.com/microsoftgraph/msgraph-sdk-javascript sample
    graphClient
      .api("users")
      .version("v1.0")
      .select("displayName,mail,userPrincipalName")
      .filter(`(givenName eq '${escape(this.state.searchFor)}') or (surname eq '${escape(this.state.searchFor)}') or (displayName eq '${escape(this.state.searchFor)}')`)
      .get((err, res) => {  

        if (err) {
          console.error(err);
          return;
        }

        // Prepare the output array
        var users: Array<IUserItem> = new Array<IUserItem>();

        // Map the JSON response to the output array
        res.value.map((item: any) => {
          users.push( { 
            displayName: item.displayName,
            mail: item.mail,
            userPrincipalName: item.userPrincipalName,
          });
        });

        // Update the component state accordingly to the result
        this.setState(
          {
            users: users,
          }
        );
      });
  }
```

Чтобы создать экземпляр типа **MSGraphClient**, передайте его ключ службы методу *consume()* объекта *serviceScope* для текущего контекста.
Затем просто используйте текучий API из пакета SDK Graph, чтобы определить запрос OData, который будет выполняться для целевой конечной точки Microsoft Graph.
В результате вы также получите отклик JSON, который потребуется раскодировать и сопоставить с типизированным результатом.

> [!NOTE]
> Вы даже можете воспользоваться полностью типизированным подходом с использованием [типов TypeScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings).

### <a name="DeploymentAndPermissionsGrant"></a>Развертывание решения и предоставление разрешений
Теперь все готово к сборке, компоновке, упаковыванию и развертыванию решения.
Выполните команды gulp, чтобы выполнить эти задачи.

```sh
gulp build
```

Проверьте сборку решения.

```sh
gulp bundle
gulp package-solution
```

Скомпонуйте и упакуйте решение.
Теперь перейдите к каталогу приложений целевого клиента и отправьте в него пакет решения. Пакет решения находится в папке *sharepoint/solution* решения. Это SPPKG-файл.
После отправки пакета решения в каталоге приложений откроется примерно такое диалоговое окно:

![Пользовательский интерфейс каталога приложений во время отправки пакета решения](../images/graphconsumer-tutorial-appcatalog-prompt.png)

Как видите, в нижней части экрана отображается сообщение о том, что для пакета решения необходимо утвердить разрешения. Это вызвано свойством webApiPermissionRequests в файле *package-solution.json*.

Откройте Центр администрирования SharePoint и перейдите по ссылке "Попробуйте новый Центр администрирования SharePoint" в правом верхнем углу экрана.

![Ссылка "Попробуйте новый Центр администрирования SharePoint"](../images/graphconsumer-open-new-admin-center.png)

В новом Центре администрирования выберите пункт меню "*Управление WebApiPermission" в меню быстрого запуска слева. Откроется примерно такая страница:

![Страница управления WebApiPermission](../images/graphconsumer-webapipermission-management.png)

> [!NOTE]
> Звездочки в пользовательском интерфейсе нового Центра администрирования указывают на то, что функции по-прежнему находятся на стадии предварительного тестирования.

На этой странице вы (или любой другой администратор клиента SPO) можете утвердить или отклонить любой запрос на получение разрешений, ожидающий проверки. Обратите внимание: на ней не видно, какой пакет решения запрашивает разрешение, так как разрешения определяются на уровне клиента и для уникального приложения. 

> [!NOTE]
> Дополнительные сведения о принципе работы областей разрешений на уровне клиента вы найдете в статьях, указанных в разделе [См. также](#SeeAlso).

Выберите разрешение, запрашиваемое в файле решения *package-solution.json*, выберите пункт "Утверждение или отклонение прав доступа" и нажмите "Утвердить" в области справа, как показано на приведенном ниже снимке экрана.

![Страница управления WebApiPermission во время утверждения](../images/graphconsumer-webapipermission-approval.png)

Вы также можете выбрать разрешение, ожидающее утверждения, и нажать кнопку "Утвердить или отклонить" на панели инструментов.

![Страница управления WebApiPermission во время утверждения](../images/graphconsumer-webapipermission-approval-approve.png)

Готово!

### <a name="SolutionTesting"></a>Тестирование решения
Запустите решение с помощью следующей команды gulp:

```sh
gulp serve --nobrowser
```

Откройте браузер и перейдите на страницу SharePoint Framework Workbench по следующему URL-адресу:

```TXT
https://<your-tenant>.sharepoint.com/_layouts/15/Workbench.aspx
```

Добавьте клиентскую веб-часть *GraphConsumer*, выберите *Режим клиента* и попробуйте найти пользователей.
При первом запросе всплывающее окно должно сначала появиться, а затем пропасть. Это окно входа, используемое библиотекой ADAL JS, с помощью которой SharePoint Framework получает маркер доступа из Azure AD, применяя неявный поток OAuth.

![Пользовательский интерфейс примера приложения](../images/use-aad-tutorial-video.gif)

Вот и все! С помощью этой возможности вы можете создавать эффективные корпоративные решения, использующие REST API, защищенный с помощью Azure AD.

<a name="SeeAlso"></a>

## <a name="see-also"></a>См. также
* [Подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework](use-aadhttpclient.md)
* [Использование MSGraphClient для подключения к Microsoft Graph](use-msgraph.md)
