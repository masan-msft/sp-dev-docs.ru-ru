# <a name="validate-web-part-property-values"></a><span data-ttu-id="ced0d-101">Проверка значений свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="ced0d-101">Validate web part property values</span></span>

<span data-ttu-id="ced0d-p101">Пользователи могут настраивать веб-части в соответствии со своими потребностями с помощью свойств. Проверяйте указанные значения конфигурации, чтобы пользователям было проще настроить веб-часть и удобнее с ней работать. Из этой статьи вы узнаете, как проверять значения свойств клиентских веб-частей в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p101">When working with web parts, users can configure them to meet their needs using their properties. By validating the provided configuration values you can make it easier for users to configure the web part and improve the overall user experience of working with your web part. In this article you will learn how to validate web part property values in SharePoint Framework client-side web parts.</span></span>

> <span data-ttu-id="ced0d-105">**Примечание.** Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment) для создания решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="ced0d-105">**Note:** Before following the steps in this article, be sure to [set up your development environment](../../set-up-your-development-environment) for building SharePoint Framework solutions.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="ced0d-106">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="ced0d-106">Create new project</span></span>

<span data-ttu-id="ced0d-107">Для начала создайте папку проекта.</span><span class="sxs-lookup"><span data-stu-id="ced0d-107">Start by creating a new folder for your project.</span></span>

```sh
md react-listinfo
```

<span data-ttu-id="ced0d-108">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="ced0d-108">Go to the project folder.</span></span>

```sh
cd react-listinfo
```

<span data-ttu-id="ced0d-109">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="ced0d-109">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="ced0d-110">Укажите следующее:</span><span class="sxs-lookup"><span data-stu-id="ced0d-110">When prompted, enter the following values:</span></span>

- <span data-ttu-id="ced0d-111">имя решения — **react-listinfo**;</span><span class="sxs-lookup"><span data-stu-id="ced0d-111">**react-listinfo** as your solution name</span></span>
- <span data-ttu-id="ced0d-112">расположение файлов — **Use the current folder** (Использовать текущую папку);</span><span class="sxs-lookup"><span data-stu-id="ced0d-112">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="ced0d-113">отправную точку создания веб-части — **React**;</span><span class="sxs-lookup"><span data-stu-id="ced0d-113">**React** as the starting point to build the web part</span></span>
- <span data-ttu-id="ced0d-114">имя веб-части — **List info** (Сведения списка);</span><span class="sxs-lookup"><span data-stu-id="ced0d-114">**List info** as your web part name</span></span>
- <span data-ttu-id="ced0d-115">описание веб-части — **Shows information about the selected list** (Показывает сведения о выбранном списке).</span><span class="sxs-lookup"><span data-stu-id="ced0d-115">**Shows information about the selected list** as your web part description</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../../images/property-validation-yeoman-generator.png)

<span data-ttu-id="ced0d-p102">Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p102">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../../images/property-validation-visual-studio-code.png)

## <a name="validate-web-part-property-values-in-the-sharepoint-framework"></a><span data-ttu-id="ced0d-120">Проверка значений свойств веб-части в SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="ced0d-120">Validate web part property values in the SharePoint Framework</span></span>

<span data-ttu-id="ced0d-p103">В SharePoint Framework разработчики могут проверять значения свойств веб-части двумя способами. Значение можно проверить непосредственно в коде веб-части или с помощью внешнего API. Первый способ удобен, если вам нужно проверить простые значения, например минимальную/максимальную длину, обязательные свойства или распознавание простых шаблонов, например почтового индекса. Если проверка основана на бизнес-логике, например проверка номера социального страхования или членства в группе безопасности, лучше вызывать внешние API.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p103">SharePoint Framework offers developers two ways for validating values of web part properties. You can validate the value directly, inside web part's code, or you can call an external API to perform the validation there. Validating values inline is useful for performing simple validations such as minimal/maximum length, required properties or simple pattern recognition, like a ZIP code. Whenever the validation is based on business logic, such as checking a social security number or a security group membership, calling external APIs is a better approach.</span></span>

<span data-ttu-id="ced0d-p104">Чтобы проверить значение свойства веб-части, нужно реализовать обработчик для события **onGetErrorMessage** этого свойства. При проверке в коде обработчик событий возвращает строку с ошибкой проверки или пустую строку, если указанное значение допустимо. При проверке с помощью удаленных API обработчик событий возвращает обещание строки. Если указанное значение недопустимо, обещание превращается в сообщение об ошибке. Если указанное значение допустимо, обещание превращается в пустую строку.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p104">In order to validate the value of a web part property, you have to implement the event handler for the **onGetErrorMessage** event of that particular property. For inline validation the event handler should return a string with the validation error or an empty string if the provided value is valid. For validation using remote APIs the event handler returns a promise of string. If the provided value is invalid the promise resolves with the error message. If the provided value is valid then the promise resolves with an empty string.</span></span>

### <a name="validate-web-part-property-values-inline"></a><span data-ttu-id="ced0d-130">Проверка значений свойств веб-части в коде</span><span class="sxs-lookup"><span data-stu-id="ced0d-130">Validate web part property values inline</span></span>

<span data-ttu-id="ced0d-p105">На этом этапе вы убедитесь, что свойство веб-части Description указано и содержит не более 40 символов. Эта проверка выполняется непосредственно в коде.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p105">In this step you will verify that the description web part property is specified and its value is not longer than 40 characters. You will do this using the inline validation process.</span></span>

<span data-ttu-id="ced0d-p106">В редакторе кода откройте файл **./src/webparts/listInfo/ListInfoWebPart.ts**. Добавьте метод **validateDescription** в класс **ListInfoWebPart** с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="ced0d-p106">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file. In the **ListInfoWebPart** class, add the **validateDescription** method with the following code:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

  private validateDescription(value: string): string {
    if (value === null ||
      value.trim().length === 0) {
      return 'Provide a description';
    }

    if (value.length > 40) {
      return 'Description should not be longer than 40 characters';
    }

    return '';
  }
}
```

<span data-ttu-id="ced0d-p107">Метод **validateDescription** проверяет, указано ли описание и не содержит ли оно более 40 символов. Если указанное описание недопустимо, метод возвращает сообщение об ошибке проверки. Если указанное значение допустимо, возвращается пустая строка.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p107">The **validateDescription** method checks if the description is provided and if it isn't longer than 40 characters. If the provided description is invalid, the method returns an error message corresponding to the validation error. If the provided value is correct it returns an empty string.</span></span>

<span data-ttu-id="ced0d-p108">После этого необходимо правильно связать метод **validateDescription** со свойством **Description** веб-части. В классе **ListInfoWebPart** измените реализацию метода **getPropertyPaneConfiguration** на такую:</span><span class="sxs-lookup"><span data-stu-id="ced0d-p108">Next, you have to associate the **validateDescription** method with the **description** web part property. In the **ListInfoWebPart** class change the implementation of the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

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
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="ced0d-140">Вы расширили определение свойства **Description** веб-части, определив метод **validateDescription** как обработчик события **onGetErrorMessage**.</span><span class="sxs-lookup"><span data-stu-id="ced0d-140">You have extended the definition of the **description** web part with defining the **validateDescription** method as the event handler for the **onGetErrorMessage** event.</span></span>

<span data-ttu-id="ced0d-141">Чтобы просмотреть результат проверки, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ced0d-141">Run the following command to see the result of the validation:</span></span>

```sh
gulp serve
```

<span data-ttu-id="ced0d-p109">В рабочей области добавьте веб-часть на холст и откройте ее свойства. Если вы удалите описание, то увидите первую ошибку проверки.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p109">In the workbench, add the web part to canvas and open its properties. If you remove the description you should see the first validation error.</span></span>

![Ошибка проверки: не указано значение обязательного свойства](../../../../images/property-validation-empty-description-error.png)

<span data-ttu-id="ced0d-p110">Затем введите значение, которое содержит более 40 символов. Под текстовым полем появится еще одна ошибка проверки.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p110">Next, try providing a value that's longer than 40 characters. You should see another validation error displayed below the text field.</span></span>

![Ошибка проверки: превышена допустимая длина значения](../../../../images/property-validation-description-too-long-error.png)

<span data-ttu-id="ced0d-p111">Обратите внимание: если указано недопустимое значение, в веб-части отображается последнее допустимое значение. Кроме того, если в режиме нереактивной области свойств указано недопустимое свойство веб-части, кнопка **Применить** отключается, чтобы пользователь не мог применить недействительную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p111">Notice, that when providing an invalid value, the web part is rendered showing the last valid value. Additionally, in the non-reactive property pane mode, if one of the web part properties is invalid, the **Apply** button is disabled, preventing the user from applying the invalid configuration.</span></span>

![Отключенная кнопка "Применить" при недопустимом значении свойства веб-части](../../../../images/property-validation-description-error-apply-disabled.png)

### <a name="validate-web-part-property-values-using-remote-apis"></a><span data-ttu-id="ced0d-151">Проверка значений свойств веб-части с помощью удаленных API</span><span class="sxs-lookup"><span data-stu-id="ced0d-151">Validate web part property values using remote APIs</span></span>

<span data-ttu-id="ced0d-p112">В некоторых случаях проверка значений свойств веб-части может быть сложнее и требовать определенной бизнес-логики. В таких случаях будет эффективнее проверить значение с помощью существующих API, а не реализовывать и поддерживать бизнес-логику в веб-части.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p112">In some scenarios, validating web part property values can be more complex and require specific business logic. In such cases it might be more efficient for you to validate the value using an existing API rather than implementing and maintaining the business logic in the web part.</span></span>

<span data-ttu-id="ced0d-154">На этом этапе вы реализуете логику, которая проверяет, существует ли на текущем сайте SharePoint список с именем, указанным в свойствах веб-части.</span><span class="sxs-lookup"><span data-stu-id="ced0d-154">In this step you will implement validation logic that checks if the list with the name specified in the web part properties exists in the current SharePoint site.</span></span>

#### <a name="add-the-listname-web-part-property"></a><span data-ttu-id="ced0d-155">Добавление свойства веб-части listName</span><span class="sxs-lookup"><span data-stu-id="ced0d-155">Add the listName web part property</span></span>

<span data-ttu-id="ced0d-p113">В редакторе кода откройте файл **./src/webparts/listInfo/ListInfoWebPart.manifest.json**. В свойстве **properties** добавьте свойство **listName**. В качестве значения по умолчанию укажите пустую строку:</span><span class="sxs-lookup"><span data-stu-id="ced0d-p113">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.manifest.json** file. In the **properties** property add a new property named **listName** with the default value set to an empty string:</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",
  "id": "1ec8f92d-ea55-4584-bf50-bac435c916bf",
  "alias": "ListInfoWebPart",
  "componentType": "WebPart",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

  "preconfiguredEntries": [{
    "groupId": "1ec8f92d-ea55-4584-bf50-bac435c916bf",
    "group": { "default": "Under Development" },
    "title": { "default": "List info" },
    "description": { "default": "Shows information about the selected list" },
    "officeFabricIconFontName": "Page",
    "properties": {
      "description": "List info"
    }
  }]
}
```

<span data-ttu-id="ced0d-158">После этого в редакторе кода откройте файл **./src/webparts/listInfo/IListInfoWebPartProps.ts** и расширьте определение интерфейса, добавив свойство **listName** типа string.</span><span class="sxs-lookup"><span data-stu-id="ced0d-158">Next, in the code editor open the **./src/webparts/listInfo/IListInfoWebPartProps.ts** file and extend the interface definition with the **listName** property of type string.</span></span>

```ts
export interface IListInfoWebPartProps {
  description: string;
  listName: string;
}
```

<span data-ttu-id="ced0d-159">Чтобы завершить добавление нового свойства веб-части, откройте файл **./src/webparts/listInfo/ListInfoWebPart.ts** в редакторе кода и измените реализацию метода **getPropertyPaneConfiguration** на такую:</span><span class="sxs-lookup"><span data-stu-id="ced0d-159">Finish adding the new web part property, by opening in the code editor the **./src/webparts/listInfo/ListInfoWebPart.ts** file and changing the implementation of the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

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
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="ced0d-160">Добавьте недостающую строку ресурса **ListNameFieldLabel**. Для этого измените код файла **./src/webparts/listInfo/loc/mystrings.d.ts** на такой:</span><span class="sxs-lookup"><span data-stu-id="ced0d-160">Add the missing **ListNameFieldLabel** resource string by changing the code of the **./src/webparts/listInfo/loc/mystrings.d.ts** file to:</span></span>

```ts
declare interface IListInfoStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  DescriptionFieldLabel: string;
  ListNameFieldLabel: string;
}

declare module 'listInfoStrings' {
  const strings: IListInfoStrings;
  export = strings;
}
```

<span data-ttu-id="ced0d-161">а код **./src/webparts/listInfo/loc/ru-ru.js** — на такой:</span><span class="sxs-lookup"><span data-stu-id="ced0d-161">and the code of the **./src/webparts/listInfo/loc/en-us.js** to:</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "DescriptionFieldLabel": "Description Field",
    "ListNameFieldLabel": "List name"
  }
});
```

<span data-ttu-id="ced0d-162">Выполните следующую команду, чтобы проверить, что проект запущен, а добавленное свойство имени списка отображается в области свойств веб-части:</span><span class="sxs-lookup"><span data-stu-id="ced0d-162">Run the following command to verify that the project is running and that the newly added list name property is displayed in the web part property pane:</span></span>

```sh
gulp serve
```

![Свойство имени списка отображается в области свойств веб-части](../../../../images/property-validation-list-name-property.png)

#### <a name="validate-the-name-of-the-list-using-the-sharepoint-rest-api"></a><span data-ttu-id="ced0d-164">Проверка имени списка с помощью REST API SharePoint</span><span class="sxs-lookup"><span data-stu-id="ced0d-164">Validate the name of the list using the SharePoint REST API</span></span>

<span data-ttu-id="ced0d-165">На этом этапе вы проверите указанное имя списка и узнаете, соответствует ли оно существующему списку на текущем сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ced0d-165">In this step you will validate the provided list name and check if it corresponds to an existing list in the current SharePoint site.</span></span>

<span data-ttu-id="ced0d-166">В редакторе кода откройте файл **./src/webparts/listInfo/ListInfoWebPart.ts** и добавьте следующие ссылки:</span><span class="sxs-lookup"><span data-stu-id="ced0d-166">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file and add the following references:</span></span>

```ts
import { SPHttpClient, SPHttpClientResponse } from '@microsoft/sp-http';
import { escape } from '@microsoft/sp-lodash-subset';
```

<span data-ttu-id="ced0d-167">Добавьте метод **validateListName** в класс **ListInfoWebPart** с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="ced0d-167">Next, to the **ListInfoWebPart** class add the **validateListName** method with the following code:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

  private validateListName(value: string): Promise<string> {
    return new Promise<string>((resolve: (validationErrorMessage: string) => void, reject: (error: any) => void): void => {
      if (value === null ||
        value.length === 0) {
        resolve('Provide the list name');
        return;
      }

      this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + `/_api/web/lists/getByTitle('${escape(value)}')?$select=Id`, SPHttpClient.configurations.v1)
        .then((response: SPHttpClientResponse): void => {
          if (response.ok) {
            resolve('');
            return;
          }
          else if (response.status === 404) {
            resolve(`List '${escape(value)}' doesn't exist in the current site`);
            return;
          }
          else {
            resolve(`Error: ${response.statusText}. Please try again`);
            return;
          }
        })
        .catch((error: any): void => {
          resolve(error);
        });
    });
  }
}
```

<span data-ttu-id="ced0d-p114">Сначала метод **validateListName** проверит, было ли указано имя списка. Если нет, обещание превращается в соответствующую ошибку проверки. Если пользователь указал имя списка, метод **validateListName** использует класс **SPHttpClient** для вызова REST API SharePoint и проверит, существует ли список с указанным именем.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p114">First, the **validateListName** method checks if a list name has been provided. If not, it resolves the promise with a relevant validation error. If the user has provided a list name, the **validateListName** method uses the **SPHttpClient** to call the SharePoint REST API and check if the list with the specified name exists.</span></span>

<span data-ttu-id="ced0d-p115">Если на текущем сайте существует список с указанным именем, будет возвращен код состояния 200 OK, а метод **validateListName** вернет обещание с пустой строкой, подтверждая, что соответствующий заданному значению список существует. Если список с указанным именем не существует, будет возвращен другой код. Скорее всего, это будет ответ "404 — не найдено", но если запрос не будет выполнен по другой причине, то может быть возвращен другой код состояния. В обоих случаях метод **validateListName** покажет пользователю соответствующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p115">If the list with the specified name exists in the current site, the response will return a 200 OK status code and the **validateListName** method will resolve the promise with an empty string, confirming that the provided value represents a valid list. If the list with the specified name doesn't exist, the response will return a different code. Typically it will be a 404 Not Found response, but if the request failed in some other way a different status code can be returned. In both cases the **validateListName** method will display a relevant error message to the user.</span></span>

<span data-ttu-id="ced0d-p116">После определения метода проверки имени списка необходимо настроить его как обработчик проверки для свойства веб-части **listName**. В классе **ListInfoWebPart** замените код метода **getPropertyPaneConfiguration** на такой:</span><span class="sxs-lookup"><span data-stu-id="ced0d-p116">With the list name validation method defined, the next step is to configure it as the validation handler for the **listName** web part property. In the **ListInfoWebPart** class replace the code of the **getPropertyPaneConfiguration** method with:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

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
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel,
                  onGetErrorMessage: this.validateListName.bind(this)
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}
```

<span data-ttu-id="ced0d-177">Чтобы просмотреть результат проверки, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ced0d-177">Run the following command to see the result of the validation:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="ced0d-178">Так как метод проверки имени списка взаимодействует с REST API SharePoint, необходимо проверить веб-часть в размещенной версии рабочей области SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ced0d-178">Because the list name validation method communicates with the SharePoint REST API, you have to test the web part in the hosted version of the SharePoint workbench.</span></span>

<span data-ttu-id="ced0d-p117">Добавьте веб-часть на холст и откройте ее свойства. Так как вы не указали значение имени списка по умолчанию (обязательное свойство), отобразится ошибка проверки.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p117">Add the web part to the canvas and open its properties. Because you haven't specified a default value for the list name, which is a required property, you will see a validation error.</span></span>

![Ошибка проверки: не указано значение обязательного свойства](../../../../images/property-validation-empty-list-name-error.png)

<span data-ttu-id="ced0d-182">Если указать имя списка, который не существует, веб-часть покажет сообщение о том, что такой список не существует на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="ced0d-182">If you provide a name of a list that doesn't exist, the web part will display a validation error stating that the list you specified doesn't exist in the current site.</span></span>

![Ошибка проверки: указано имя списка, не существующее на текущем сайте](../../../../images/property-validation-invalid-list-name-error.png)

<span data-ttu-id="ced0d-184">Если вы укажете имя существующего списка, ошибка проверки исчезнет.</span><span class="sxs-lookup"><span data-stu-id="ced0d-184">If you specify a name of an existing list, the validation error will disappear.</span></span>

![Указано действительное имя списка, ошибки проверки нет](../../../../images/property-validation-valid-list-name.png)

#### <a name="optimize-validation-using-remote-apis"></a><span data-ttu-id="ced0d-186">Оптимизация проверки с помощью удаленных API</span><span class="sxs-lookup"><span data-stu-id="ced0d-186">Optimize validation using remote APIs</span></span>

<span data-ttu-id="ced0d-p118">При проверке свойств веб-части с помощью удаленных API SharePoint Framework отслеживает изменения элементов управления области свойств и отправляет обновленные значения для проверки в указанный обработчик проверки. По умолчанию время ожидания перед запуском проверки составляет 200 мс. Если пользователь не изменяет определенное значение в течение 200 мс, SharePoint Framework начинает проверку. Если обработчик проверки использует удаленный API, то при каждом запуске проверки этот метод будет отправлять веб-запрос к API на проверку указанного значения. Если пользователь недостаточно быстро печатает, то на проверку будут отправляться частично введенные значения, создавая лишнюю нагрузку на сеть и API. В таких случаях рекомендуем увеличить задержку перед проверкой.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p118">When validating web part properties using remote APIs, SharePoint Framework monitors changes in the property pane controls and sends updated values for validation to the specified validation handler. By default, the SharePoint Framework waits 200ms before triggering the validation process. If the user hasn't changed the particular value for 200ms, the SharePoint Framework will start the validation process. When the validation handler uses a remote API, each time the validation process starts, that method will issue a web request to the API to validate the specified value. If users don't type fast enough, this will result in partially completed values being sent over for validation unnecessarily stressing the network and the API. In such cases you should consider increasing the validation delay.</span></span>

![Отправляемые на проверку веб-запросы с частично введенным именем списка (сетевые инструменты Microsoft Edge)](../../../../images/property-validation-partial-list-name-validation.png)

<span data-ttu-id="ced0d-p119">Задержку перед проверкой можно настроить отдельно для каждого свойства, в зависимости от типа значения, вводимого пользователем. Ниже показано, как увеличить задержку перед проверкой свойства **listName**.</span><span class="sxs-lookup"><span data-stu-id="ced0d-p119">You can configure the validation delay for each property separately, depending on the type of value that users need to provide. Following steps illustrate how to increase the validation delay for the **listName** property.</span></span>

<span data-ttu-id="ced0d-p120">В редакторе кода откройте файл **./src/webparts/listInfo/ListInfoWebPart.ts**. Измените код метода **getPropertyPaneConfiguration** на такой:</span><span class="sxs-lookup"><span data-stu-id="ced0d-p120">In the code editor open the **./src/webparts/listInfo/ListInfoWebPart.ts** file. Change the code of the **getPropertyPaneConfiguration** method to:</span></span>

```ts
export default class ListInfoWebPart extends BaseClientSideWebPart<IListInfoWebPartProps> {
  // ...

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
                PropertyPaneTextField('description', {
                  label: strings.DescriptionFieldLabel,
                  onGetErrorMessage: this.validateDescription.bind(this)
                }),
                PropertyPaneTextField('listName', {
                  label: strings.ListNameFieldLabel,
                  onGetErrorMessage: this.validateListName.bind(this),
                  deferredValidationTime: 500
                })
              ]
            }
          ]
        }
      ]
    };
  }

  // ...
}

```

<span data-ttu-id="ced0d-198">Свойство **deferredValidationTime** устанавливает длительность задержки перед запуском проверки SharePoint Framework (в миллисекундах).</span><span class="sxs-lookup"><span data-stu-id="ced0d-198">The **deferredValidationTime** property specifies the number of milliseconds that the SharePoint Framework will wait before starting the validation process.</span></span>

<span data-ttu-id="ced0d-199">Выполните следующую команду, чтобы проверить установленную задержку:</span><span class="sxs-lookup"><span data-stu-id="ced0d-199">Run the following command to see that the applied delay is working as expected:</span></span>

```sh
gulp serve --nobrowser
```