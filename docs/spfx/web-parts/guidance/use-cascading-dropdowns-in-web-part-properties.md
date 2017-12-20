---
title: "Использование каскадных раскрывающихся меню для свойств веб-частей"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9bb9a2e5677827d66e56502dd20f23d912c9ff9c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-cascading-dropdowns-in-web-part-properties"></a><span data-ttu-id="6fd50-102">Использование каскадных раскрывающихся меню для свойств веб-частей</span><span class="sxs-lookup"><span data-stu-id="6fd50-102">Use cascading dropdowns in web part properties</span></span>

<span data-ttu-id="6fd50-p101">Когда вы создаете панель свойств для клиентских веб-частей SharePoint, параметры одного свойства веб-части могут отображаться с учетом значения, выбранного для другого свойства. Такое обычно происходит, если применяются каскадные раскрывающиеся меню. В этой статье описано, как создавать каскадные раскрывающиеся меню на панели свойств веб-части, не создавая соответствующий пользовательский элемент управления.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p101">When designing the property pane for your SharePoint client-side web parts, you may have one web part property that displays its options based on the  value selected in another property. This scenario typically occurs when implementing cascading dropdown controls. In this article, you will learn how to create cascading dropdown controls in the web part property pane without developing a custom property pane control.</span></span>

![Раскрывающееся меню отключено, а заполнитель веб-части сообщает о загрузке обновленного списка элементов](../../../images/react-cascading-dropdowns-loading-indicator-when-loading-items.png)

<span data-ttu-id="6fd50-107">Исходный код рабочей веб-части доступен на сайте GitHub по адресу [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span><span class="sxs-lookup"><span data-stu-id="6fd50-107">The source of the working web part is available on GitHub at [https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span></span>

> [!NOTE] 
> <span data-ttu-id="6fd50-108">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки для создания клиентских веб-частей SharePoint](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="6fd50-108">[Note:](../../set-up-your-development-environment.md) Before following the steps in this article, be sure to set up your SharePoint client-side web part development environment.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="6fd50-109">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="6fd50-109">Create new project</span></span>

<span data-ttu-id="6fd50-110">Для начала создайте папку проекта.</span><span class="sxs-lookup"><span data-stu-id="6fd50-110">Start by creating a new folder for your project.</span></span>

```sh
md react-cascadingdropdowns
```

<span data-ttu-id="6fd50-111">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="6fd50-111">Go to the project folder.</span></span>

```sh
cd react-cascadingdropdowns
```

<span data-ttu-id="6fd50-112">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="6fd50-112">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="6fd50-113">Когда отобразится соответствующий запрос, введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6fd50-113">When prompted, enter the following values:</span></span>

- <span data-ttu-id="6fd50-114">**react-cascadingdropdowns** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="6fd50-114">**react-cascadingdropdowns** as your solution name</span></span>
- <span data-ttu-id="6fd50-115">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="6fd50-115">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="6fd50-116">**React** как отправную точку создания веб-части;</span><span class="sxs-lookup"><span data-stu-id="6fd50-116">**React** as the starting point to build the web part</span></span>
- <span data-ttu-id="6fd50-117">**List items** (Элементы списка) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="6fd50-117">**List items** as your web part name</span></span>
- <span data-ttu-id="6fd50-118">**Shows list items from the selected list** (Показывает элементы списка из выбранного списка) в качестве описания веб-части.</span><span class="sxs-lookup"><span data-stu-id="6fd50-118">**Shows list items from the selected list** as your web part description</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/react-cascading-dropdowns-yo-sharepoint.png)

<span data-ttu-id="6fd50-120">После завершения скаффолдинга блокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6fd50-120">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="6fd50-121">Далее откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="6fd50-121">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="6fd50-122">В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="6fd50-122">This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/react-cascading-dropdowns-visual-studio-code.png)

## <a name="define-a-web-part-property-to-store-the-selected-list"></a><span data-ttu-id="6fd50-124">Определение свойства веб-части для хранения выбранного списка</span><span class="sxs-lookup"><span data-stu-id="6fd50-124">Define a web part property to store the selected list</span></span>

<span data-ttu-id="6fd50-p103">Вы создадите веб-часть, отображающую элементы выбранного списка SharePoint. Пользователи смогут выбрать список на панели свойств веб-части. Для хранения выбранного списка создайте свойство веб-части с именем **listName**.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p103">You will build a web part that displays list items from a selected SharePoint list. Users will be able to select a list in the web part property pane. To store the selected list create a new web part property named **listName**.</span></span>

<span data-ttu-id="6fd50-p104">В редакторе кода откройте файл **src/webparts/listItems/ListItemsWebPartManifest.json**. Замените свойство по умолчанию **description** на новое свойство `listName`.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p104">In the code editor, open the **src/webparts/listItems/ListItemsWebPartManifest.json** file. Replace the default **description** property with a new property named `listName`.</span></span>

![Манифест веб-части с выделенным свойством списка веб-части](../../../images/react-cascading-dropdowns-listname-property-web-part-manifest.png)

<span data-ttu-id="6fd50-131">Далее откройте файл **src/webparts/listItems/IListItemsWebPartProps.ts** и замените его содержимое на следующее:</span><span class="sxs-lookup"><span data-stu-id="6fd50-131">Next, open the **src/webparts/listItems/IListItemsWebPartProps.ts** file, and replace its contents with:</span></span>

```ts
export interface IListItemsWebPartProps {
  listName: string;
}
```

<span data-ttu-id="6fd50-132">В файле **src/webparts/listItems/ListItemsWebPart.ts** измените метод **render** на следующий:</span><span class="sxs-lookup"><span data-stu-id="6fd50-132">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the **render** method to:</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  public render(): void {
    const element: React.ReactElement<IListItemsProps> = React.createElement(ListItems, {
      listName: this.properties.listName
    });

    ReactDom.render(element, this.domElement);
  }
  // ...
}
```

<span data-ttu-id="6fd50-133">Измените метод **propertyPaneSettings** на следующий:</span><span class="sxs-lookup"><span data-stu-id="6fd50-133">Update the **propertyPaneSettings** getter to:</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
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

<span data-ttu-id="6fd50-134">В файле **src/webparts/listItems/loc/mystrings.d.ts** измените интерфейс **IListItemsStrings** на следующий:</span><span class="sxs-lookup"><span data-stu-id="6fd50-134">In the **src/webparts/listItems/loc/mystrings.d.ts** file, change the **IListItemsStrings** interface to:</span></span>

```ts
declare interface IListItemsStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListNameFieldLabel: string;
}
```

<span data-ttu-id="6fd50-135">В файле **src/webparts/listItems/loc/en-us.js** добавьте отсутствующее определение для строки **ListNameFieldLabel**.</span><span class="sxs-lookup"><span data-stu-id="6fd50-135">In the **src/webparts/listItems/loc/en-us.js** file, add the missing definition for the **ListNameFieldLabel** string.</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "ListNameFieldLabel": "List"
  }
});
```

<span data-ttu-id="6fd50-136">В файле **src/webparts/listItems/components/ListItems.tsx** замените содержимое метода **render** следующим:</span><span class="sxs-lookup"><span data-stu-id="6fd50-136">In the **src/webparts/listItems/components/ListItems.tsx** file, change the contents of the **render** method to:</span></span>

```tsx
export default class ListItems extends React.Component<IListItemsProps, {}> {
 public render(): JSX.Element {
    return (
        <div className={styles.listItems}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.listName)}</p>
              <a href="https://aka.ms/spfx" className={styles.button}>
                <span className={styles.label}>Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```
<span data-ttu-id="6fd50-137">В файле **src/webparts/listItems/components/IListItemsProps.ts** замените интерфейс **IListItemsProps** следующим:</span><span class="sxs-lookup"><span data-stu-id="6fd50-137">In the **src/webparts/listItems/components/IListItemsProps.ts** file, change the **IListItemsProps** interface to:</span></span>

```ts
export interface IListItemsProps {
  listName: string;
}
```

<span data-ttu-id="6fd50-138">Чтобы убедиться, что проект работает, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6fd50-138">Run the following command to verify that the project is running:</span></span>

```sh
gulp serve
```

<span data-ttu-id="6fd50-p105">В веб-браузере добавьте веб-часть **List items** на полотно и откройте ее свойства. Убедитесь, что значение свойства **List** отображается в теле веб-части.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p105">In the web browser, add the **List items** web part to the canvas and open its properties. Verify that the value set for the **List** property is displayed in the web part body.</span></span>

![Веб-часть, в которой отображается значение свойства listName](../../../images/react-cascading-dropdowns-web-part-first-run.png)

## <a name="populate-the-dropdown-with-sharepoint-lists-to-choose-from"></a><span data-ttu-id="6fd50-142">Заполнение раскрывающегося меню списками SharePoint, из которых следует выбирать</span><span class="sxs-lookup"><span data-stu-id="6fd50-142">Populate the dropdown with SharePoint lists to choose from</span></span>

<span data-ttu-id="6fd50-p106">На этом этапе пользователь указывает, какой список должна использовать веб-часть, вручную введя его. В этом случае возможна ошибка, в идеале пользователь должен выбрать один из существующих списков на текущем сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p106">At this point, a user specifies which list the web part should use by manually entering the list name. This is error-prone and ideally you want users to choose one of the lists existing in the current SharePoint site.</span></span>

### <a name="use-dropdown-control-to-render-the-listname-property"></a><span data-ttu-id="6fd50-145">Отрисовка свойства listName с использованием раскрывающегося меню</span><span class="sxs-lookup"><span data-stu-id="6fd50-145">Use dropdown control to render the listName property</span></span>

<span data-ttu-id="6fd50-p107">Вверху веб-части добавьте в классе **ListItemsWebPart** ссылку на класс **PropertyPaneDropdown**. Замените часть кода, которая загружает класс **PropertyPaneTextField** (import), следующим:</span><span class="sxs-lookup"><span data-stu-id="6fd50-p107">In the **ListItemsWebPart** class add a reference to the **PropertyPaneDropdown** class in the top section of the web part. Replace the import clause that loads the **PropertyPaneTextField** class with:</span></span>

```ts
import {
  BaseClientSideWebPart,
  IPropertyPaneConfiguration,
  PropertyPaneTextField,
  PropertyPaneDropdown,
  IPropertyPaneDropdownOption
} from '@microsoft/sp-webpart-base';
```

<span data-ttu-id="6fd50-148">В классе **ListItemsWebPart** добавьте новую переменную **lists** для хранения сведений обо всех доступных списках на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="6fd50-148">In the **ListItemsWebPart** class, add a new variable named **lists** to store information about all available lists in the current site.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  private lists: IPropertyPaneDropdownOption[];
  // ...
}
```

<span data-ttu-id="6fd50-p108">Далее добавьте новую переменную класса **listsDropdownDisabled**. Она определяет, включено ли раскрывающееся меню со списками. Пока веб-часть не получит сведения о доступных списках на текущем сайте, раскрывающееся меню должно быть отключено.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p108">Next, add a new class variable named **listsDropdownDisabled**. This variable determines whether the list dropdown is enabled or not. Until the web part retrieves the information about the lists available in the current site, the dropdown should be disabled.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private listsDropdownDisabled: boolean = true;
  // ...
}
```

<span data-ttu-id="6fd50-152">Измените метод считывания **propertyPaneSettings** так, чтобы он использовал раскрывающееся меню для отрисовки свойства **listName**.</span><span class="sxs-lookup"><span data-stu-id="6fd50-152">Change the **propertyPaneSettings** getter to use the dropdown control to render the **listName** property.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  protected get propertyPaneSettings(): IPropertyPaneSettings {
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
                PropertyPaneDropdown('listName', {
                  label: strings.ListNameFieldLabel,
                  options: this.lists,
                  disabled: this.listsDropdownDisabled
                })
              ]
            }
          ]
        }
      ]
    };
  }
}
```

<span data-ttu-id="6fd50-153">Чтобы проверить правильность работы, выполните указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="6fd50-153">Run the following command to verify that it's working as expected:</span></span>

```sh
gulp serve
```

![Свойство listName, отрисованное на панели свойств веб-части с использованием раскрывающегося меню](../../../images/react-cascading-dropdowns-listname-property-pane-dropdown.png)

### <a name="show-available-lists-in-the-list-dropdown"></a><span data-ttu-id="6fd50-155">Отображение доступных списков в раскрывающемся меню</span><span class="sxs-lookup"><span data-stu-id="6fd50-155">Show available lists in the list dropdown</span></span>

<span data-ttu-id="6fd50-p109">Ранее вы сопоставляли раскрывающееся меню свойства **listName** со свойством класса **lists**. Так как вы пока не загрузили в него никаких значений, раскрывающееся меню **List** на панели свойств веб-части остается отключенным. На этом этапе веб-часть загрузит сведения о доступных списках.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p109">Previously, you associated the dropdown control of the **listName** property with the **lists** class property. Since you haven't loaded any values into it yet, the **List** dropdown in the web part property pane remains disabled. In this step, you will extend the web part to load the information about available lists.</span></span>

#### <a name="add-a-method-to-load-available-lists"></a><span data-ttu-id="6fd50-159">Добавление метода для загрузки доступных списков</span><span class="sxs-lookup"><span data-stu-id="6fd50-159">Add a method to load available lists</span></span>

<span data-ttu-id="6fd50-p110">В классе **ListItemsWebPart** добавьте метод для загрузки доступных списков. В этой статье используются фиктивные данные, но вы также можете вызвать REST API SharePoint, чтобы извлечь список доступных списков из текущего веб-сайта. Для имитации загрузки параметров из внешней службы метод использует двухсекундную задержку.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p110">In the **ListItemsWebPart** class, add a method to load available lists. In this article you will use mock data, but you could also call the SharePoint REST API to retrieve the list of available lists from the current web. To simulate loading options from an external service the method uses a two-second delay.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private loadLists(): Promise<IPropertyPaneDropdownOption[]> {
    return new Promise<IPropertyPaneDropdownOption[]>((resolve: (options: IPropertyPaneDropdownOption[]) => void, reject: (error: any) => void) => {
      setTimeout((): void => {
        resolve([{
          key: 'sharedDocuments',
          text: 'Shared Documents'
        },
        {
          key: 'myDocuments',
          text: 'My Documents'
        }]);
      }, 2000);
    });
  }
}
```

#### <a name="load-information-about-available-lists-into-the-list-dropdown"></a><span data-ttu-id="6fd50-163">Загрузка сведений о доступных списках в раскрывающееся меню со списками</span><span class="sxs-lookup"><span data-stu-id="6fd50-163">Load information about available lists into the list dropdown</span></span>

<span data-ttu-id="6fd50-164">В классе **ListItemsWebPart** переопределите метод **onPropertyPaneConfigurationStart**, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="6fd50-164">In the **ListItemsWebPart** class, override the **onPropertyPaneConfigurationStart** method using the following code:</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  protected onPropertyPaneConfigurationStart(): void {
    this.listsDropdownDisabled = !this.lists;

    if (this.lists) {
      return;
    }

    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'lists');

    this.loadLists()
      .then((listOptions: IPropertyPaneDropdownOption[]): void => {
        this.lists = listOptions;
        this.listsDropdownDisabled = false;
        this.context.propertyPane.refresh();
        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        this.render();
      });
  }
  // ...
}
```

<span data-ttu-id="6fd50-p111">SharePoint Framework вызывает метод **onPropertyPaneConfigurationStart** после открытия панели свойств для веб-части. Сначала метод проверяет, загружена ли информация о доступных списках на текущем сайте. Если она загружена, будет включено раскрывающееся меню со списками. Если она пока не загружена, отобразится индикатор загрузки, информирующий пользователя о том, что веб-часть загружает сведения о списках.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p111">The **onPropertyPaneConfigurationStart** method is called by the SharePoint Framework after the web part property pane for the web part has been opened. First, the method checks if the information about the lists available in the current site has been loaded. If the list information is loaded, then the list dropdown will be enabled. If the list information about lists has not been loaded yet, the loading indicator is displayed which informs the user that the web part is loading information about lists.</span></span>

![Индикатор загрузки, отображающийся в веб-части во время загрузки информации о доступных списках](../../../images/react-cascading-dropdowns-loading-indicator-when-loading-list-info.png)

<span data-ttu-id="6fd50-p112">Когда информация о доступных списках загрузится, метод назначит полученные данные переменной класса **lists**, благодаря чему будет возможно отображение этих сведений в раскрывающемся меню со списками. Далее будет включено раскрывающееся меню, позволяющее пользователю выбрать список. Благодаря вызову метода **this.context.propertyPane.refresh()** обновляется область свойств веб-части, чтобы отобразить последние изменения в раскрывающемся меню со списками. Когда информация загрузится, индикатор загрузки будет удален благодаря вызову метода **clearLoadingIndicator**. Так как при вызове метода очищается пользовательский интерфейс веб-части, вызывается метод **render**, чтобы веб-часть отрисовалась вновь.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p112">After the information about available lists has been loaded the method assigns the retrieved data to the **lists** class variable, from which it can be used by the list dropdown. Next, the dropdown is enabled allowing the user to select a list. By calling  **this.context.propertyPane.refresh()** the web part property pane is refreshed and it reflects the latest changes to the list dropdown. Once list information is loaded, the loading indicator is removed by a call to the **clearLoadingIndicator** method. Since calling this method clears the web part user interface, the **render** method is called to force the web part to re-render.</span></span>

<span data-ttu-id="6fd50-175">Выполните следующую команду, чтобы убедиться, что всё работает правильно:</span><span class="sxs-lookup"><span data-stu-id="6fd50-175">Run the following command to confirm that everything is working as expected:</span></span>

```sh
gulp serve
```

<span data-ttu-id="6fd50-176">Когда вы добавляете веб-часть на холст и открываете панель ее свойств, раскрывающееся меню со списками должно заполниться доступными списками, из которых может выбирать пользователь.</span><span class="sxs-lookup"><span data-stu-id="6fd50-176">When you add a web part to the canvas and open its property pane, you should see the lists dropdown filled with available lists for the user to choose from.</span></span>

![Раскрывающееся меню со списками на панели свойств веб-части, в котором показаны доступные списки](../../../images/react-cascading-dropdowns-list-dropdown-available-lists.png)

## <a name="allow-users-to-select-an-item-from-the-selected-list"></a><span data-ttu-id="6fd50-178">Предоставление пользователям возможности выбрать элемент в указанном списке</span><span class="sxs-lookup"><span data-stu-id="6fd50-178">Allow users to select an item from the selected list</span></span>

<span data-ttu-id="6fd50-179">При создании веб-частей часто требуется предоставить пользователям возможность выбирать из набора значений, которые определяются ранее указанным значением (например, выбрать страну после указания континента или выбрать элемент списка после указания списка).</span><span class="sxs-lookup"><span data-stu-id="6fd50-179">When building web parts you often need to allow users to choose an option from a set of values determined by a previously selected value, such as choosing a country/region based on the selected continent or choosing a list item from a selected list.</span></span> <span data-ttu-id="6fd50-180">Это позволяют сделать каскадные раскрывающиеся меню.</span><span class="sxs-lookup"><span data-stu-id="6fd50-180">This user experience is often referred to as cascading dropdowns.</span></span> <span data-ttu-id="6fd50-181">Вы можете создать каскадные раскрывающиеся меню на панели свойств веб-части, используя стандартные возможности клиентских веб-частей SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="6fd50-181">Using the standard SharePoint Framework client-side web parts capabilities you can build cascading dropdowns in the web part property pane.</span></span> <span data-ttu-id="6fd50-182">Для этого вы добавите в ранее созданную веб-часть возможность выбрать элемент списка, обусловленный выбранным списком.</span><span class="sxs-lookup"><span data-stu-id="6fd50-182">To learn how to do it you will extend the previously built web part with the ability to choose a list item based on the previously selected list.</span></span>

![Раскрывающееся меню со списками, открытое на панели свойств веб-части](../../../images/react-cascading-dropdowns-item-dropdown-list-items.png)

### <a name="add-item-web-part-property"></a><span data-ttu-id="6fd50-184">Добавление свойства веб-части item</span><span class="sxs-lookup"><span data-stu-id="6fd50-184">Add item web part property</span></span>

<span data-ttu-id="6fd50-p114">В редакторе кода откройте файл **src/webparts/listItems/ListItemsWebPart.manifest.json**. В разделе **properties** добавьте свойство **itemName**, чтобы оно выглядело следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6fd50-p114">In the code editor open the **src/webparts/listItems/ListItemsWebPart.manifest.json** file. To the **properties** section add a new property named **itemName** so that it appears as follows:</span></span>

```json
{
  // ...
  "properties": {
    "listName": "",
    "itemName": ""
  }
  // ...
}
```

![Манифест веб-части с выделенным свойством веб-части itemName](../../../images/react-cascading-dropdowns-itemname-property-web-part-manifest.png)

<span data-ttu-id="6fd50-188">Замените код в файле **src/webparts/listItems/IListItemsWebPartProps.ts** следующим:</span><span class="sxs-lookup"><span data-stu-id="6fd50-188">Change the code in the **src/webparts/listItems/IListItemsWebPartProps.ts** file to:</span></span>

```ts
export interface IListItemsWebPartProps {
  listName: string;
  itemName: string;
}
```

<span data-ttu-id="6fd50-189">Замените код в файле **src/webparts/listItems/components/IListItemsProps.ts** следующим:</span><span class="sxs-lookup"><span data-stu-id="6fd50-189">Change the code in the **src/webparts/listItems/components/IListItemsProps.ts** file to:</span></span>

```ts
export interface IListItemsProps {
  listName: string;
  itemName: string;
}
```

<span data-ttu-id="6fd50-190">В файле **src/webparts/listItems/ListItemsWebPart.ts** замените код метода **render** следующим:</span><span class="sxs-lookup"><span data-stu-id="6fd50-190">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the code of the **render** method to:</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  public render(): void {
    const element: React.ReactElement<IListItemsProps> = React.createElement(ListItems, {
      listName: this.properties.listName,
      itemName: this.properties.itemName
    });

    ReactDom.render(element, this.domElement);
  }
  // ...
}
```

<span data-ttu-id="6fd50-191">В файле **src/webparts/listItems/loc/mystrings.d.ts** измените интерфейс **IListItemsStrings** на следующий:</span><span class="sxs-lookup"><span data-stu-id="6fd50-191">In the **src/webparts/listItems/loc/mystrings.d.ts** file, change the **IListItemsStrings** interface to:</span></span>

```ts
declare interface IListItemsStrings {
  PropertyPaneDescription: string;
  BasicGroupName: string;
  ListNameFieldLabel: string;
  ItemNameFieldLabel: string;
}
```

<span data-ttu-id="6fd50-192">В файле **src/webparts/listItems/loc/en-us.js** добавьте отсутствующее определение для строки **ItemNameFieldLabel**.</span><span class="sxs-lookup"><span data-stu-id="6fd50-192">In the **src/webparts/listItems/loc/en-us.js** file, add the missing definition for the **ItemNameFieldLabel** string.</span></span>

```js
define([], function() {
  return {
    "PropertyPaneDescription": "Description",
    "BasicGroupName": "Group Name",
    "ListNameFieldLabel": "List",
    "ItemNameFieldLabel": "Item"
  }
});
```

### <a name="render-the-value-of-the-item-web-part-property"></a><span data-ttu-id="6fd50-193">Отрисовка значения свойства веб-части item</span><span class="sxs-lookup"><span data-stu-id="6fd50-193">Render the value of the item web part property</span></span>

<span data-ttu-id="6fd50-194">В файле **src/webparts/listItems/components/ListItems.tsx** измените метод **render** на следующий:</span><span class="sxs-lookup"><span data-stu-id="6fd50-194">In the **src/webparts/listItems/components/ListItems.tsx** file, change the **render** method to:</span></span>

```tsx
export default class ListItems extends React.Component<IListItemsProps, {}> {
  public render(): JSX.Element {
    return (
        <div className={styles.listItems}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.listName)}</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.itemName)}</p>
              <a href="https://aka.ms/spfx" className={styles.button}>
                <span className={styles.label}>Learn more</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

### <a name="allow-users-to-choose-the-item-from-a-list"></a><span data-ttu-id="6fd50-195">Предоставление пользователям возможности выбрать элемент списка</span><span class="sxs-lookup"><span data-stu-id="6fd50-195">Allow users to choose the item from a list</span></span>

<span data-ttu-id="6fd50-196">У пользователей должна быть возможность выбрать список в раскрывающемся меню точно так же, как выбрать элемент в списке доступных.</span><span class="sxs-lookup"><span data-stu-id="6fd50-196">Similar to how users can select a list using a dropdown, they should be able to select the item from the list of available items.</span></span>

<span data-ttu-id="6fd50-197">В классе **ListItemsWebPart** добавьте новую переменную **items** для хранения информации о доступных элементах в только что выбранном списке.</span><span class="sxs-lookup"><span data-stu-id="6fd50-197">In the **ListItemsWebPart** class, add a new variable named **items** which you will use to store information about all available items in the currently selected list.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private items: IPropertyPaneDropdownOption[];
  // ...
}
```

<span data-ttu-id="6fd50-p115">Далее добавьте новую переменную класса **itemsDropdownDisabled**. Она определяет, необходимо ли включать раскрывающееся меню. У пользователей должна появиться возможность выбора элемента только после выбора соответствующего списка.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p115">Next, add a new class variable named **itemsDropdownDisabled**. This variable determines whether the items dropdown should be enabled or not. Users should be able to select an item only after they selected a list.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private itemsDropdownDisabled: boolean = true;
  // ...
}
```

<span data-ttu-id="6fd50-201">Измените метод считывания **propertyPaneSettings** так, чтобы он использовал раскрывающееся меню для отрисовки свойства **itemName**.</span><span class="sxs-lookup"><span data-stu-id="6fd50-201">Change the **propertyPaneSettings** getter to use the dropdown control to render the **itemName** property.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
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
                PropertyPaneDropdown('listName', {
                  label: strings.ListNameFieldLabel,
                  options: this.lists,
                  disabled: this.listsDropdownDisabled
                }),
                PropertyPaneDropdown('itemName', {
                  label: strings.ItemNameFieldLabel,
                  options: this.items,
                  disabled: this.itemsDropdownDisabled
                })
              ]
            }
          ]
        }
      ]
    };
  }
}
```

<span data-ttu-id="6fd50-202">Чтобы проверить правильность работы, выполните указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="6fd50-202">Run the following command to verify that it's working as expected:</span></span>

```sh
gulp serve
```

![Свойство itemName, отрисованное на панели свойств веб-части с использованием раскрывающегося меню](../../../images/react-cascading-dropdowns-itemname-property-pane-dropdown.png)

### <a name="show-items-available-in-the-selected-list-in-the-item-dropdown"></a><span data-ttu-id="6fd50-204">Отображение доступных элементов выбранного списка в раскрывающемся меню</span><span class="sxs-lookup"><span data-stu-id="6fd50-204">Show items available in the selected list in the item dropdown</span></span>

<span data-ttu-id="6fd50-p116">Ранее вы определили раскрывающееся меню для отрисовки свойства **itemName** на панели свойств веб-части. Далее следует добавить в веб-часть возможность загружать сведения о доступных элементах выбранного списка и отображать эти элементы в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p116">Previously, you defined a dropdown control to render the **itemName** property in the web part property pane. Next, you will extend the web part to load the information about items available in the selected list and show the items in the item dropdown.</span></span>

#### <a name="add-method-to-load-list-items"></a><span data-ttu-id="6fd50-207">Добавление метода для загрузки элементов списка</span><span class="sxs-lookup"><span data-stu-id="6fd50-207">Add method to load list items</span></span>

<span data-ttu-id="6fd50-p117">В файле **src/webparts/listItems/ListItemsWebPart.ts** в классе **ListItemsWebPart** добавьте метод для загрузки доступных элементов из выбранного списка. Как и для загрузки доступных списков, здесь используются фиктивные данные.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p117">In the **src/webparts/listItems/ListItemsWebPart.ts** file, in the **ListItemsWebPart** class add a new method to load available list items from the selected list. Like the method for loading available lists, you will use mock data.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private loadItems(): Promise<IPropertyPaneDropdownOption[]> {
    if (!this.properties.listName) {
      // resolve to empty options since no list has been selected
      return Promise.resolve();
    }

    const wp: ListItemsWebPart = this;

    return new Promise<IPropertyPaneDropdownOption[]>((resolve: (options: IPropertyPaneDropdownOption[]) => void, reject: (error: any) => void) => {
      setTimeout(() => {
        const items = {
          sharedDocuments: [
            {
              key: 'spfx_presentation.pptx',
              text: 'SPFx for the masses'
            },
            {
              key: 'hello-world.spapp',
              text: 'hello-world.spapp'
            }
          ],
          myDocuments: [
            {
              key: 'isaiah_cv.docx',
              text: 'Isaiah CV'
            },
            {
              key: 'isaiah_expenses.xlsx',
              text: 'Isaiah Expenses'
            }
          ]
        };
        resolve(items[wp.properties.listName]);
      }, 2000);
    });
  }
}
```

<span data-ttu-id="6fd50-p118">Метод **loadItems** возвращает фиктивные элементы списка для ранее выбранного списка. Если список не выбран, метод разрешает обещание без данных.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p118">The **loadItems** method returns mock list items for the previously selected list. When no list has been selected, the method resolves the promise without any data.</span></span>

#### <a name="load-information-about-available-items-into-the-item-dropdown"></a><span data-ttu-id="6fd50-212">Загрузка сведений о доступных элементах в раскрывающееся меню</span><span class="sxs-lookup"><span data-stu-id="6fd50-212">Load information about available items into the item dropdown</span></span>

<span data-ttu-id="6fd50-213">В классе **ListItemsWebPart** измените метод **onPropertyPaneConfigurationStart** так, чтобы он загружал элементы выбранного списка.</span><span class="sxs-lookup"><span data-stu-id="6fd50-213">In the **ListItemsWebPart** class, extend the **onPropertyPaneConfigurationStart** method to load items for the selected list.</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  protected onPropertyPaneConfigurationStart(): void {
    this.listsDropdownDisabled = !this.lists;
    this.itemsDropdownDisabled = !this.properties.listName || !this.items;

    if (this.lists) {
      return;
    }

    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'options');

    this.loadLists()
      .then((listOptions: IPropertyPaneDropdownOption[]): Promise<IPropertyPaneDropdownOption[]> => {
        this.lists = listOptions;
        this.listsDropdownDisabled = false;
        this.context.propertyPane.refresh();
        return this.loadItems();
      })
      .then((itemOptions: IPropertyPaneDropdownOption[]): void => {
        this.items = itemOptions;
        this.itemsDropdownDisabled = !this.properties.listName;
        this.context.propertyPane.refresh();
        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        this.render();
      });
  }
  // ...
}
```

<span data-ttu-id="6fd50-p119">При инициализации веб-часть сначала определит, следует ли включать раскрывающееся меню. Если пользователь ранее выбрал список, он сможет выбрать и элемент этого списка. Если он не выбирал список, раскрывающееся меню будет отключено.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p119">When initializing, the web part will first determine if the items dropdown should be enabled or not. If the user previously selected a list, they can select an item from that list. If no list was selected, then the item dropdown is disabled.</span></span>

<span data-ttu-id="6fd50-p120">Измените ранее определенный код, загружающий сведения о доступных списках, так, чтобы он загружал и сведения о доступных элементах выбранного списка. Этот код затем назначит полученные сведения переменной класса **items** для использования в раскрывающемся меню. Наконец код очистит индикатор загрузки и позволит пользователю начать работать с веб-частью.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p120">You extended the previously defined code, which loads the information about available lists, to load the information about items available in the selected list. The code then assigns the retrieved information to the **items** class variable for use by the item dropdown. Finally, the code clears the loading indicator and allows the user to start working with the web part.</span></span>

<span data-ttu-id="6fd50-220">Выполните следующую команду, чтобы убедиться, что всё работает правильно:</span><span class="sxs-lookup"><span data-stu-id="6fd50-220">Run the following command to confirm that everything is working as expected:</span></span>

```sh
gulp serve
```

<span data-ttu-id="6fd50-p121">При необходимости раскрывающееся меню может быть изначально отключено, чтобы пользователи сначала выбирали список. На данном этапе, даже после выбора списка, раскрывающееся меню элементов остается отключенным.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p121">As required, initially the item dropdown is disabled, requiring users to select a list first. But at this point, even after a list has been selected, the item dropdown remains disabled.</span></span>

![Раскрывающееся меню отключено, даже когда выбран список](../../../images/react-cascading-dropdowns-list-selected-item-disabled.png)

#### <a name="update-web-part-property-pane-after-selecting-a-list"></a><span data-ttu-id="6fd50-224">Обновление панели свойств веб-части после выбора списка</span><span class="sxs-lookup"><span data-stu-id="6fd50-224">Update web part property pane after selecting a list</span></span>

<span data-ttu-id="6fd50-225">Когда пользователь выбирает список на панели свойств, страница веб-части должна обновиться так, чтобы включить раскрывающееся меню и отобразить список доступных элементов выбранного списка.</span><span class="sxs-lookup"><span data-stu-id="6fd50-225">When a user selects a list in the property pane, the web part should update, enabling the item dropdown and showing the list of items available in the selected list.</span></span>

<span data-ttu-id="6fd50-226">Откройте файл **ListItemsWebPart.ts** и переопределите в классе **ListItemsWebPart** метод **onPropertyPaneFieldChanged**, указав следующий код:</span><span class="sxs-lookup"><span data-stu-id="6fd50-226">In the **ListItemsWebPart.ts** file, in the **ListItemsWebPart** class override the **onPropertyPaneFieldChanged** method with the following code:</span></span>

```ts
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  protected onPropertyPaneFieldChanged(propertyPath: string, oldValue: any, newValue: any): void {
    if (propertyPath === 'listName' &&
        newValue) {
      // push new list value
      super.onPropertyPaneFieldChanged(propertyPath, oldValue, newValue);
      // get previously selected item
      const previousItem: string = this.properties.itemName;
      // reset selected item
      this.properties.itemName = undefined;
      // push new item value
      this.onPropertyPaneFieldChanged('itemName', previousItem, this.properties.itemName);
      // disable item selector until new items are loaded
      this.itemsDropdownDisabled = true;
      // refresh the item selector control by repainting the property pane
      this.context.propertyPane.refresh();
      // communicate loading items
      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'items');

      this.loadItems()
        .then((itemOptions: IPropertyPaneDropdownOption[]): void => {
          // store items
          this.items = itemOptions;
          // enable item selector
          this.itemsDropdownDisabled = false;
          // clear status indicator
          this.context.statusRenderer.clearLoadingIndicator(this.domElement);
          // re-render the web part as clearing the loading indicator removes the web part body
          this.render();
          // refresh the item selector control by repainting the property pane
          this.context.propertyPane.refresh();
        });
    }
    else {
      super.onPropertyPaneFieldChanged(propertyPath, oldValue, newValue);
    }
  }
  // ...
}
```

<span data-ttu-id="6fd50-p122">Когда пользователь выберет список, веб-часть сохранит только что выбранное значение. Так как выбранный список изменился, веб-часть сбросит элемент выбранного ранее списка. Когда список будет выбран, на панель свойств загрузятся элементы конкретного списка. При загрузке элементов у пользователя не должно быть возможности выбрать элемент.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p122">After the user selected a list, the web part persists the newly selected value. Because the selected list changed, the web part resets the previously selected list item. Now that a list is selected, the web part property pane loads list items for that particular list. While loading items, the user shouldn't be able to select an item.</span></span>

<span data-ttu-id="6fd50-p123">Когда элементы выбранного списка загрузятся, они будут назначены переменной класса **items**, с помощью которой раскрывающееся меню сможет их использовать. Когда сведения о доступных элементах списка загрузятся, включится раскрывающееся меню, в котором пользователи смогут выбрать элемент. Индикатор загрузки удаляется, в результате чего очищается тело веб-части. Следовательно, веб-часть должна быть отрисована повторно. Наконец обновляется панель свойств веб-части для отображения последних изменений.</span><span class="sxs-lookup"><span data-stu-id="6fd50-p123">Once the items for the selected list are loaded they are assigned to the **items** class variable from where they can be referenced by the item dropdown. Now that the information about available list items is available, the item dropdown is enabled allowing users to choose an item. The loading indicator is removed which clears the web part body which is why the web part should re-render. Finally the web part property pane refreshes to reflect the latest changes.</span></span>

> [!NOTE] 
> <span data-ttu-id="6fd50-p124">В выпуске 6 SharePoint Framework присутствует ошибка в компоненте Office UI Fabric React Dropdown, из-за которой раскрывающееся меню работает неправильно. Для временного решения проблемы измените строку **12027** в файле **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** с:</span><span class="sxs-lookup"><span data-stu-id="6fd50-p124">**Note:** In drop 6 of the SharePoint Framework there is a bug in the Office UI Fabric React Dropdown component that causes the dropdown control to work incorrectly. A temporary workaround is to edit the **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** file and change line 12027 from:</span></span>
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> <span data-ttu-id="6fd50-237">на значение:</span><span class="sxs-lookup"><span data-stu-id="6fd50-237">to:</span></span>
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

![Раскрывающееся меню на панели свойств веб-части, показывающее доступные элементы выбранного списка](../../../images/react-cascading-dropdowns-item-dropdown-list-items.png)
