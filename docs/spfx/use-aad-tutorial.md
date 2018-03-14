---
title: "Использование API, защищенных с помощью Azure AD, в SharePoint Framework"
description: "В руководстве по использованию класса AadHttpClient или MSGraphClient рассмотрено подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework."
ms.date: 02/15/2018
ms.prod: sharepoint
ms.openlocfilehash: ee57316a47fdb2edc5a8309cc4402534919501fb
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="consuming-apis-secured-with-azure-ad-within-the-sharepoint-framework"></a>Использование API, защищенных с помощью Azure AD, в SharePoint Framework

> [!IMPORTANT]
> Клиентские объекты `AadHttpClient` и `MSGraphClient` находятся на стадии тестирования и могут меняться. Не используйте их в рабочей среде. Также обратите внимание, что свойства `webApiPermissionRequests` в `package-solution.json` не поддерживаются в производственных клиентах.

Использование REST API, защищенных с помощью Azure Active Directory (Azure AD) и Open Authorization (OAuth 2.0), из клиентской веб-части или расширения SharePoint Framework — распространенный бизнес-сценарий корпоративного уровня.

Вы можете использовать SharePoint Framework версии 1.4.1 для вызова REST API Microsoft Graph или любого другого REST API, зарегистрированного в Azure AD. 

Из этой статьи вы узнаете, как создать решение SharePoint Framework, которое использует API Microsoft Graph с особым набором разрешений. Общий обзор этой технологии см. в статье [Подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework](use-aadhttpclient.md).

> [!IMPORTANT]
> Вы можете использовать API Microsoft Graph с SharePoint Framework более ранних версий, чем 1.4.1, через собственный клиент **graphHttpClient** или вручную через неявный поток OAuth [ADAL JS](https://github.com/AzureAD/azure-activedirectory-library-for-js). Однако первый подход связан с предопределенным набором разрешений, который имеет некоторые ограничения, а второй сложен с точки зрения разработки. Инструкции по реализации неявного потока OAuth см. в статье [Подключение к API, защищенным с помощью Azure Active Directory](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/web-parts/guidance/connect-to-api-secured-with-aad).

## <a name="SolutionOverview"></a>Обзор решения

В этой статье описано, как создать клиентскую веб-часть, которая позволяет искать пользователей в текущем клиенте, как показано на следующем снимке экрана. Поиск основан на Microsoft Graph, и для него требуются разрешения не ниже User.ReadBasic.All.

![Клиентская веб-часть с текстовым полем и кнопкой для поиска пользователей в клиенте](../images/use-aad-tutorial-video.gif)

Клиентская веб-часть позволяет искать пользователей по имени и показывает всех подходящих пользователей через компонент **DetailsList** из Office UI Fabric. В области свойств веб-части есть параметр для выбора способа доступа к Microsoft Graph. Начиная с SharePoint Framework версии 1.4.1 для доступа к Microsoft Graph можно использовать собственный клиент Graph (**MSGraphClient**) или низкоуровневый тип, используемый для доступа к любому REST API, защищенному с помощью Azure AD (**AadHttpClient**).

> [!NOTE]
> Исходный код этого решения представлен в репозитории GitHub [spfx-api-scopes-tutorial](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/tutorials/spfx-api-scopes-tutorial).

Если вы уже знаете, как создавать решения SharePoint Framework, можете перейти к [настройке запросов на получение разрешений API](#ConfiguringApiPermissions).

## <a name="CreatingInitialSolution"></a>Создание исходного решения
Если у вас установлена старая версия генератора SharePoint Framework, необходимо обновить ее до версии 1.4.1 или более поздней. Для этого выполните следующую команду, чтобы глобально установить последнюю версию пакета.

```sh
npm install -g @microsoft/generator-sharepoint
```

После этого создайте новое решение SharePoint Framework:

* Создайте папку в своей файловой системе. В ней будет храниться исходный код решения. Измените текущий путь, указав эту папку.
* Запустите генератор Yeoman, чтобы сформировать шаблоны нового решения.

   ```sh
   yo @microsoft/sharepoint
   ```
* В решении сделайте следующее:
    * Укажите имя решения (например, *spfx-api-scopes-tutorial*).
    * В качестве целевой среды укажите *SharePoint Online only (latest)* (Только SharePoint Online, последняя версия).
    * Используйте текущую папку.
    * Укажите, следует ли развертывать решение глобально в целевом клиенте.
    * Выберите тип решения "WebPart".
    * Назовите веб-часть *GraphConsumer*.
    * Добавьте описание.
    * Выберите React в качестве платформы разработки.

![Пользовательский интерфейс генератора Yeoman при формировании шаблонов решения SPFx](../images/graphconsumer-yeoman-generator.png)

* Запустите Visual Studio Code (или другой редактор кода) в контексте текущей папки.

```sh
code .
```

## <a name="ConfiguringBaseElements"></a>Настройка базовых элементов веб-части
После этого настройте исходные элементы клиентской веб-части.

### <a name="ConfigureCustomProperties"></a>Настройка особых свойств
Создайте файл исходного кода в папке *src/webparts/graphConsumer/components* решения.
Назовите новый файл *ClientMode.ts* и объявите с его помощью объект TypeScript *enum* с доступными значениями свойства **ClientMode** веб-части.

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

Теперь обновите метод **getPropertyPaneConfiguration()** клиентской веб-части так, чтобы он поддерживал выбор вариантов в области свойств. Ниже показана новая реализация этого метода.

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

Кроме того, необходимо обновить метод **render** клиентской веб-части, чтобы создавать должным образом настроенный экземпляр компонента React для отрисовки. Ниже показано определение метода обновления.

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

Чтобы этот код работал, нужно добавить операторы import в начале файла *GraphConsumerWebPart.ts*, как показано ниже.

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

### <a name="UpdateResourceStrings"></a>Обновление строк ресурсов
Чтобы скомпилировать решение, необходимо обновить файл *mystrings.d.ts* в папке *src/webparts/graphConsumer/loc* этого решения. Замените код интерфейса, который определяет строку ресурсов, приведенным ниже кодом.

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

### <a name="UpdateStyles"></a>Обновление стиля клиентской веб-части
Вам также нужно обновить файл стилей SCSS. Откройте файл *GraphConsumer.module.scss* в папке *src/webparts/graphConsumer/components* решения. Добавьте следующие классы стилей сразу после класса **.title**:

```SCSS
  .form {
    @include ms-font-l;
    @include ms-fontColor-white;
  }

  label {
    @include ms-fontColor-white;
  }
```

### <a name="UpdateReactComponent"></a>Обновление компонента React, отображающего веб-часть
Теперь вы можете обновить компонент React **GraphConsumer** в папке *src/webparts/graphConsumer/components* решения.
Сначала обновите файл *IGraphConsumerProps.ts*, чтобы принять особые свойства, необходимые для реализации веб-части. Ниже показано обновленное содержимое файла *IGraphConsumerProps.ts*.

```TS
import { WebPartContext } from '@microsoft/sp-webpart-base';
import { ClientMode } from './ClientMode';

export interface IGraphConsumerProps {
  clientMode: ClientMode;
  context: WebPartContext;
}
```
Обратите внимание на импорт определения перечисления **ClientMode**, а также на импорт типа **WebPartContext**. Они понадобятся вам позже.

Создайте интерфейс для хранения состояния компонента React. Создайте файл в папке *src/webparts/graphConsumer/components* и назовите его *IGraphConsumerState.ts*. Ниже показано определение интерфейса.

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

Интерфейс будет использоваться для определения структуры пользователей, полученной из текущего клиента и привязанной к компоненту **DetailsList** в пользовательском интерфейсе.

После этого обновите файл *GraphConsumer.tsx*. Сначала добавьте операторы для импорта определенных ранее типов.

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

Обратите внимание на импорт компонентов **IGraphConsumerProps**, **IGraphConsumerState**, **ClientMode** и **IUserItem**. Также импортируются некоторые компоненты Office UI Fabric, используемые для отрисовки пользовательского интерфейса компонента React.

После операций импорта определите структуру столбцов для компонента **DetailsList** из Office UI Fabric.

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

Этот массив будет использоваться в параметрах компонента **DetailsList**, как видно по методу **render()** компонента React. Замените этот компонент приведенным ниже кодом.

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

Обновите объявление типа компонента React и добавьте конструктор, как показано ниже.

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

Для сбора критериев поиска компоненту **TextField** требуются некоторые правила проверки и обработчики событий. Ниже показаны реализации метода.

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

Компонент **PrimaryButton** вызывает функцию **_search()**, которая определяет, какую клиентскую технологию использовать для вызова Microsoft Graph.

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

Экземпляр компонента **DetailsList** отрисовывается в методе **render()** на тот случай, если в свойстве **users** состояния компонента имеются элементы.

## <a name="ConfiguringApiPermissions"></a>Настройка запросов на получение разрешений API

Чтобы использовать Microsoft Graph или другой сторонний REST API, в манифесте решения необходимо явно объявить требуемые разрешения с точки зрения OAuth.

В SharePoint Framework 1.4.1 или более новой версии для этого можно настроить свойство **webApiPermissionRequests** в файле *package-solution.json* из папки *config* в решении. Ниже показан фрагмент этого файла для текущего решения. Скопируйте объявление свойства **webApiPermissionRequests**.

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

Обратите внимание на объект **webApiPermissionRequests**, представляющий собой массив элементов **webApiPermissionRequest**. Каждый элемент определяет *ресурс* и *область* для запроса на получение разрешений.
Значением *resource* может быть имя или ObjectId (в Azure AD) ресурса, для которого требуется настроить запрос на получение разрешений. Для Microsoft Graph используется имя "Microsoft Graph". Значение ObjectId не уникально и зависит от клиента.
Значением *scope* может быть имя разрешения или уникальный идентификатор этого разрешения. Имя разрешения можно получить из документации по API. Идентификатор разрешения можно получить из файла манифеста API.

> [!NOTE]
> Все доступные разрешения перечислены в [справочнике по разрешениям Microsoft Graph](https://developer.microsoft.com/ru-RU/graph/docs/concepts/permissions_reference). По умолчанию у субъекта-службы нет явных разрешений на доступ к Microsoft Graph. Однако, запросив маркер доступа для Microsoft Graph, вы получите маркер с разрешением `user_impersonation`, с помощью которого можно считывать сведения о пользователях (User.Read.All). Вы можете запрашивать дополнительные разрешения, а администраторы клиентов — предоставлять их. Дополнительные сведения см. в статье [Подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework](use-aadhttpclient.md).


Для поиска пользователей и получения свойств **displayName**, **mail** и **userPrincipalName** достаточно разрешения User.ReadBasic.All.

Когда вы упакуете и развернете решение, вам (или администратору) нужно будет предоставить ему запрашиваемые разрешения. Дополнительные сведения см. в разделе [Развертывание решения и предоставление разрешений](#DeploymentAndPermissionsGrant).

## <a name="ConsumingTheGraph"></a>Использование Microsoft Graph
Теперь вы можете реализовать методы для использования Microsoft Graph. У вас есть два варианта:
* использовать клиентский объект **AadHttpClient**;
* использовать клиентский объект **MSGraphClient**.

С помощью клиентского объекта **AadHttpClient** можно использовать Microsoft Graph или любой другой сторонний (или встроенный) REST API.

Клиентской объект **MSGraphClient** подходит только для использования Microsoft Graph. Он использует клиентский объект **AadHttpClient** и поддерживает текучий синтаксис пакета SDK Microsoft Graph.

### <a name="AadHttpClient"></a>Использование AadHttpClient
Чтобы использовать любой REST API с помощью клиентского объекта **AadHttpClient**, создайте экземпляр типа **AadHttpClient** и укажите свойство *serviceScope* текущего контекста и URI целевой службы.

Созданный объект предоставит методы для выполнения следующих запросов:

* **get** (отправляет HTTP-запрос GET);
* **post** (отправляет HTTP-запрос POST);
* **fetch** (отправляет любой HTTP-запрос в зависимости от указанных аргументов *HttpClientConfiguration* и *IHttpClientOptions*).

Так как все эти методы поддерживают асинхронную модель разработки с использованием JavaScript и TypeScript, вы можете обрабатывать их результаты с помощью обещаний.

Ниже показан метод **_searchWithAad()** из демо-решения.

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

Метод **get()** получает URL-адрес запроса OData в качестве входного аргумента. В случае успешного выполнения запроса возвращается объект JSON с ответом.

### <a name="MSGraphClient"></a>Использование MSGraphClient
Если планируете использовать Microsoft Graph, можно воспользоваться клиентским объектом **MSGraphClient**, который предоставляет более текучий синтаксис.
Ниже показана реализация метода **_searchWithGraph()** из демо-решения.

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

Чтобы создать экземпляр типа **MSGraphClient**, передайте его ключ службы методу **consume()** объекта *serviceScope* для текущего контекста.
Затем используйте текучий API из пакета SDK Microsoft Graph, чтобы определить запрос OData, который будет выполняться для целевой конечной точки Microsoft Graph.
В результате вы получите ответ JSON, который потребуется раскодировать и сопоставить с типизированным результатом.

> [!NOTE]
> Вы можете использовать полностью типизированный подход, используя [типы TypeScript Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings).

## <a name="DeploymentAndPermissionsGrant"></a>Развертывание решения и предоставление разрешений
Теперь все готово к сборке, компоновке, упаковыванию и развертыванию решения. Выполните команды gulp для правильной сборки решения.

```sh
gulp build
```

Используйте следующую команду, чтобы объединить в пакет и упаковать решение.

```sh
gulp bundle
gulp package-solution
```

После этого перейдите в каталог приложений целевого клиента и отправьте пакет решения. Пакет решения находится в папке *sharepoint/solution* решения. Это SPPKG-файл.
После отправки пакета решения в каталоге приложений откроется примерно такое диалоговое окно:

![Снимок экрана: пользовательский интерфейс каталога приложений во время отправки пакета решения](../images/graphconsumer-tutorial-appcatalog-prompt.png)

В нижней части экрана отображается сообщение о том, что для пакета решения необходимо утвердить разрешения. Это вызвано свойством **webApiPermissionRequests** в файле *package-solution.json*.

Откройте Центр администрирования SharePoint и перейдите по ссылке **Попробуйте новый Центр администрирования SharePoint** в правом верхнем углу экрана.

![Снимок экрана: ссылка "Попробуйте новый Центр администрирования SharePoint"](../images/graphconsumer-open-new-admin-center.png)

В новом Центре администрирования выберите пункт меню **Управление WebApiPermission** в меню быстрого запуска слева. Теперь страница будет выглядеть приблизительно следующим образом:

![Снимок экрана: страница управления WebApiPermission](../images/graphconsumer-webapipermission-management.png)

> [!NOTE]
> Звездочки в пользовательском интерфейсе нового Центра администрирования означают, что функции находятся на стадии тестирования.

На этой странице вы (или любой другой администратор вашего клиента SharePoint Online) можете утвердить или отклонить любой запрос на получение разрешений, ожидающий проверки. Обратите внимание: вы не видите, какой пакет решения запрашивает разрешение, так как разрешения определяются на уровне клиента и для уникального приложения. 

> [!NOTE]
> Дополнительные сведения о принципе работы разрешений на уровне клиента см. в статьях, указанных в разделе [См. также](#SeeAlso).

Выберите разрешение, запрашиваемое в файле решения *package-solution.json*, выберите **Разрешите или запретите доступ** и нажмите **Утвердить**. Ниже показана панель Центра администрирования.

![Снимок экрана: страница управления WebApiPermission во время утверждения](../images/graphconsumer-webapipermission-approval.png)

Вы также можете выбрать разрешение, ожидающее утверждения, и нажать кнопку **Утвердить или отклонить** на панели инструментов.

![Снимок экрана: страница управления WebApiPermission во время утверждения](../images/graphconsumer-webapipermission-approval-approve.png)

Готово!

## <a name="SolutionTesting"></a>Тестирование решения
Запустите решение с помощью указанной ниже команды gulp.

```sh
gulp serve --nobrowser
```

Откройте браузер и перейдите на страницу SharePoint Framework Workbench:

```TXT
https://<your-tenant>.sharepoint.com/_layouts/15/Workbench.aspx
```

Добавьте клиентскую веб-часть *GraphConsumer*, выберите *Режим клиента* и попробуйте найти пользователей.
При первом запросе появится и исчезнет всплывающее окно. Это окно входа, используемое библиотекой ADAL JS, с помощью которой SharePoint Framework получает маркер доступа из Azure AD, используя неявный поток OAuth.

![Снимок экрана: пользовательский интерфейс демо-приложения](../images/use-aad-tutorial-video.gif)

Вот и все! Теперь вы можете создавать корпоративные решения, использующие REST API, защищенные с помощью Azure AD.

<a name="SeeAlso"></a>

## <a name="see-also"></a>См. также
* [Подключение к API, защищенным службой Azure AD, в решениях SharePoint Framework](use-aadhttpclient.md)
* [Использование MSGraphClient для подключения к Microsoft Graph](use-msgraph.md)
