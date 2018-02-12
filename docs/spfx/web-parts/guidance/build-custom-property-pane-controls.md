---
title: "Создание пользовательских элементов управления для области свойств"
description: "Создайте пользовательское раскрывающееся меню, которое асинхронно загружает данные из внешней службы, не блокируя пользовательский интерфейс клиентской веб-части SharePoint."
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: e4b38566a0e6425db8756288c98d8c88f6d89780
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="build-custom-controls-for-the-property-pane"></a><span data-ttu-id="483e4-103">Создание пользовательских элементов управления для области свойств</span><span class="sxs-lookup"><span data-stu-id="483e4-103">Build custom controls for the property pane</span></span>

<span data-ttu-id="483e4-104">SharePoint Framework содержит набор стандартных элементов управления для области свойств,</span><span class="sxs-lookup"><span data-stu-id="483e4-104">The SharePoint Framework contains a set of standard controls for the property pane.</span></span> <span data-ttu-id="483e4-105">но иногда нужны дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="483e4-105">But sometimes you need additional functionality beyond the basic controls.</span></span> <span data-ttu-id="483e4-106">Вам может понадобиться асинхронное обновление данных в элементе управления или определенный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="483e4-106">You might need asynchronous updates to the data on a control or a specific user interface.</span></span> <span data-ttu-id="483e4-107">Создайте пользовательский элемент управления для области свойств, чтобы получить необходимые функции.</span><span class="sxs-lookup"><span data-stu-id="483e4-107">Build a custom control for the property pane to get the functionality you need.</span></span>

<span data-ttu-id="483e4-108">В этой статье показано, как создать пользовательское раскрывающееся меню, которое асинхронно загружает данные из внешней службы, не блокируя пользовательский интерфейс веб-части.</span><span class="sxs-lookup"><span data-stu-id="483e4-108">In this article, you will build a custom dropdown control that loads its data asynchronously from an external service without blocking the user interface of the web part.</span></span>

![Раскрывающееся меню элементов загружает доступные элементы после выбора списка в раскрывающемся меню списков](../../../images/custom-property-pane-control-cascading-loading-items.png)

<span data-ttu-id="483e4-110">Исходный код рабочей веб-части доступен на сайте GitHub по адресу [sp-dev-fx-webparts/samples/react-custompropertypanecontrols/](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span><span class="sxs-lookup"><span data-stu-id="483e4-110">The source of the working web part is available on GitHub at [sp-dev-fx-webparts/samples/react-custompropertypanecontrols/](https://github.com/SharePoint/sp-dev-fx-webparts/tree/master/samples/react-custompropertypanecontrols).</span></span>

> [!NOTE] 
> <span data-ttu-id="483e4-111">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки](../../set-up-your-development-environment.md) для создания решений на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="483e4-111">Before following the steps in this article, be sure to [set up your development environment](../../set-up-your-development-environment.md) for building SharePoint Framework solutions.</span></span>

## <a name="create-new-project"></a><span data-ttu-id="483e4-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="483e4-112">Create new project</span></span>

1. <span data-ttu-id="483e4-113">Для начала создайте папку проекта:</span><span class="sxs-lookup"><span data-stu-id="483e4-113">Start by creating a new folder for your project:</span></span>

  ```sh
  md react-custompropertypanecontrol
  ```

2. <span data-ttu-id="483e4-114">Перейдите в папку проекта:</span><span class="sxs-lookup"><span data-stu-id="483e4-114">Go to the project folder:</span></span>

  ```sh
  cd react-custompropertypanecontrol
  ```

3. <span data-ttu-id="483e4-115">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="483e4-115">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="483e4-116">Когда отобразится соответствующий запрос, введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="483e4-116">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="483e4-117">имя решения — **react-custompropertypanecontrol**</span><span class="sxs-lookup"><span data-stu-id="483e4-117">**react-custompropertypanecontrol** as your solution name</span></span>
  - <span data-ttu-id="483e4-118">расположение файлов — **Use the current folder** (Использовать текущую папку)</span><span class="sxs-lookup"><span data-stu-id="483e4-118">**Use the current folder** for the location to place the files</span></span>
  - <span data-ttu-id="483e4-119">имя веб-части **List items** (Элементы списка)</span><span class="sxs-lookup"><span data-stu-id="483e4-119">**List items** as your web part name</span></span>
  - <span data-ttu-id="483e4-120">описание веб-части — **Shows list items from the selected list** (Показывает элементы списка из выбранного списка)</span><span class="sxs-lookup"><span data-stu-id="483e4-120">**Shows list items from the selected list** as your web part description</span></span>
  - <span data-ttu-id="483e4-121">отправная точка создания веб-части — **React**</span><span class="sxs-lookup"><span data-stu-id="483e4-121">**React** as the starting point to build the web part</span></span>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/custom-property-pane-control-yeoman.png)

5. <span data-ttu-id="483e4-123">По завершении скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="483e4-123">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="483e4-124">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="483e4-124">Open your project folder in your code editor.</span></span> <span data-ttu-id="483e4-125">В инструкциях и на снимках экрана из этой статьи используется Visual Studio Code, но вы можете использовать любой другой редактор.</span><span class="sxs-lookup"><span data-stu-id="483e4-125">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span>

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/custom-property-pane-control-visual-studio-code.png)

## <a name="define-web-part-property-for-storing-the-selected-list"></a><span data-ttu-id="483e4-127">Определение свойства веб-части для хранения выбранного списка</span><span class="sxs-lookup"><span data-stu-id="483e4-127">Define web part property for storing the selected list</span></span>

<span data-ttu-id="483e4-128">В веб-части, которую вы создаете, появятся элементы из выбранного списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="483e4-128">The web part you are building shows list items from the selected SharePoint list.</span></span> <span data-ttu-id="483e4-129">Пользователи смогут выбрать список в свойствах веб-части.</span><span class="sxs-lookup"><span data-stu-id="483e4-129">Users are able to select a list in the web part properties.</span></span> <span data-ttu-id="483e4-130">Для хранения выбранного списка создайте свойство веб-части с именем **listName**.</span><span class="sxs-lookup"><span data-stu-id="483e4-130">To store the selected list, create a new web part property named **listName**.</span></span>

1. <span data-ttu-id="483e4-p104">В редакторе кода откройте файл **src/webparts/listItems/ListItemsWebPartManifest.json**. Замените свойство по умолчанию **description** на новое свойство `listName`.</span><span class="sxs-lookup"><span data-stu-id="483e4-p104">In the code editor, open the **src/webparts/listItems/ListItemsWebPartManifest.json** file. Replace the default **description** property with a new property named `listName`.</span></span>

  ![Манифест веб-части с выделенным свойством listName](../../../images/custom-property-pane-control-list-property-web-part-manifest.png)

2. <span data-ttu-id="483e4-134">Откройте файл **src/webparts/listItems/IListItemsWebPartProps.ts** и замените его содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="483e4-134">Open the **src/webparts/listItems/IListItemsWebPartProps.ts** file and replace its contents with:</span></span>

  ```typescript
  export interface IListItemsWebPartProps {
    listName: string;
  }
  ```

3. <span data-ttu-id="483e4-135">В файле **src/webparts/listItems/ListItemsWebPart.ts** замените метод **render** на следующий:</span><span class="sxs-lookup"><span data-stu-id="483e4-135">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the **render** method to:</span></span>

  ```typescript
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

4. <span data-ttu-id="483e4-136">Обновите метод **getPropertyPaneConfiguration** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483e4-136">Update the **getPropertyPaneConfiguration** method to:</span></span>

  ```typescript
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
                    label: strings.ListFieldLabel
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

5. <span data-ttu-id="483e4-137">В файле **src/webparts/listItems/loc/mystrings.d.ts** измените интерфейс **IListItemsWebPartStrings** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483e4-137">In the **src/webparts/listItems/loc/mystrings.d.ts** file, change the **IListItemsWebPartStrings** interface to:</span></span>

  ```typescript
  declare interface IListItemsWebPartStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListFieldLabel: string;
  }
  ```

6. <span data-ttu-id="483e4-138">В файле **src/webparts/listItems/loc/en-us.js** добавьте отсутствующее определение для строки **ListFieldLabel**.</span><span class="sxs-lookup"><span data-stu-id="483e4-138">In the **src/webparts/listItems/loc/en-us.js** file, add the missing definition for the **ListFieldLabel** string.</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListFieldLabel": "List"
    }
  });
  ```

7. <span data-ttu-id="483e4-139">В файле **src/webparts/listItems/components/ListItems.tsx** замените содержимое метода **render** следующим:</span><span class="sxs-lookup"><span data-stu-id="483e4-139">In the **src/webparts/listItems/components/ListItems.tsx** file, change the contents of the **render** method to:</span></span>

  ```tsx
  export default class ListItems extends React.Component<IListItemsProps, {}> {
    public render(): React.ReactElement<IListItemsProps> {
      return (
        <div className={styles.listItems}>
          <div className={styles.container}>
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-lg10 ms-xl8 ms-xlPush2 ms-lgPush1">
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

8. <span data-ttu-id="483e4-140">Откройте файл **src/webparts/listItems/components/IListItemsProps.ts** и замените его содержимое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="483e4-140">Open the **src/webparts/listItems/components/IListItemsProps.ts** file, and replace its contents with:</span></span>

  ```typescript
  export interface IListItemsProps {
    listName: string;
  }
  ```

9. <span data-ttu-id="483e4-141">Чтобы убедиться, что проект работает, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="483e4-141">Run the following command to verify that the project is running:</span></span>

  ```sh
  gulp serve
  ```

10. <span data-ttu-id="483e4-p105">В веб-браузере добавьте веб-часть **List items** на полотно и откройте ее свойства. Убедитесь, что значение свойства **List** отображается в теле веб-части.</span><span class="sxs-lookup"><span data-stu-id="483e4-p105">In the web browser, add the **List items** web part to the canvas and open its properties. Verify that the value set for the **List** property is displayed in the web part body.</span></span>

  ![Веб-часть, в которой отображается значение свойства listName](../../../images/custom-property-pane-control-web-part-first-run.png)


## <a name="create-asynchronous-dropdown-property-pane-control"></a><span data-ttu-id="483e4-145">Создание асинхронного раскрывающегося меню области свойств</span><span class="sxs-lookup"><span data-stu-id="483e4-145">Create asynchronous dropdown property pane control</span></span>

<span data-ttu-id="483e4-p106">В SharePoint Framework представлено стандартное раскрывающееся меню, которое позволяет пользователям выбирать определенные значения. Все его значения должны быть известны заранее. Если вы хотите загружать значения динамически или загружаете значения асинхронно из внешней службы и не хотите блокировать веб-часть, создайте пользовательское раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-p106">The SharePoint Framework offers you a standard dropdown control that allows users to select a specific value. The dropdown control is built in a way that requires all its values to be known upfront. If you want to load the values dynamically or you're loading values asynchronously from an external service and you don't want to block the whole web part, building a custom dropdown control is a viable option.</span></span>

<span data-ttu-id="483e4-149">Оно состоит из класса, который регистрирует элемент управления в веб-части, и компонента React в SharePoint Framework, который отрисовывает раскрывающееся меню и управляет его данными.</span><span class="sxs-lookup"><span data-stu-id="483e4-149">When creating a custom property pane control that uses React in the SharePoint Framework, the control consists of a class that registers the control with the web part, and a React component that renders the dropdown and manages its data.</span></span>

> [!NOTE] 
> <span data-ttu-id="483e4-150">В выпуске 6 SharePoint Framework в компоненте Office UI Fabric React Dropdown есть ошибка, из-за которой элемент управления, создаваемый в этой статье, работает неправильно.</span><span class="sxs-lookup"><span data-stu-id="483e4-150">In drop 6 of the SharePoint Framework, there is a bug in the Office UI Fabric React Dropdown component that causes the control built in this article to work incorrectly.</span></span> <span data-ttu-id="483e4-151">Чтобы временно решить эту проблему, измените строку **12027** в файле **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js**. Исходный вариант:</span><span class="sxs-lookup"><span data-stu-id="483e4-151">A temporary workaround is to edit the **node_modules/@microsoft/office-ui-fabric-react-bundle/dist/office-ui-fabric-react.bundle.js** file and change line **12027** from:</span></span>
> 
> ```js
> isDisabled: this.props.isDisabled !== undefined ? this.props.isDisabled : this.props.disabled
> ```
>
> <span data-ttu-id="483e4-152">Целевой вариант:</span><span class="sxs-lookup"><span data-stu-id="483e4-152">to:</span></span>
> 
> ```js
> isDisabled: newProps.isDisabled !== undefined ? newProps.isDisabled : newProps.disabled
> ```

### <a name="add-asynchronous-dropdown-property-pane-control-react-component"></a><span data-ttu-id="483e4-153">Добавление компонента React асинхронного раскрывающегося меню области свойств</span><span class="sxs-lookup"><span data-stu-id="483e4-153">Add asynchronous dropdown property pane control React component</span></span>

1. <span data-ttu-id="483e4-154">Создайте папку компонентов.</span><span class="sxs-lookup"><span data-stu-id="483e4-154">Create the components folder.</span></span> <span data-ttu-id="483e4-155">В папке проекта **src** создайте иерархию из трех новых папок, чтобы получилась следующая структура: **src/controls/PropertyPaneAsyncDropdown/components**.</span><span class="sxs-lookup"><span data-stu-id="483e4-155">In the project **src** folder, create a hierarchy of three new folders so that your folder structure appears as **src/controls/PropertyPaneAsyncDropdown/components**.</span></span>

  ![Папка компонентов, выделенная в Visual Studio Code](../../../images/custom-property-pane-control-components-folder.png)

2. <span data-ttu-id="483e4-157">Определите свойства компонента React асинхронного раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-157">Define asynchronous dropdown React component properties.</span></span> <span data-ttu-id="483e4-158">В папке **src/controls/PropertyPaneAsyncDropdown/components** создайте файл **IAsyncDropdownProps.ts** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-158">In the **src/controls/PropertyPaneAsyncDropdown/components** folder, create a new file named **IAsyncDropdownProps.ts**, and enter the following code:</span></span>

  ```typescript
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

  export interface IAsyncDropdownProps {
    label: string;
    loadOptions: () => Promise<IDropdownOption[]>;
    onChanged: (option: IDropdownOption, index?: number) => void;
    selectedKey: string | number;
    disabled: boolean;
    stateKey: string;
  }
  ```

  <span data-ttu-id="483e4-159">Класс **IAsyncDropdownProps** определяет свойства, которые можно настроить в компоненте React, используемом пользовательским элементом управления области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-159">The **IAsyncDropdownProps** class defines properties that can be set on the React component used by the custom property pane control:</span></span> 
  - <span data-ttu-id="483e4-160">Свойство **label** указывает подпись для раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-160">The **label** property specifies the label for the dropdown control.</span></span> 
  - <span data-ttu-id="483e4-161">Для загрузки доступных параметров элемент управления вызывает функцию, связанную с делегатом **loadOptions**.</span><span class="sxs-lookup"><span data-stu-id="483e4-161">The function associated with the **loadOptions** delegate is called by the control to load the available options.</span></span> 
  - <span data-ttu-id="483e4-162">После выбора параметра в раскрывающемся меню вызывается функция, связанная с делегатом **onChanged**.</span><span class="sxs-lookup"><span data-stu-id="483e4-162">The function associated with the **onChanged** delegate is called after the user selects an option in the dropdown.</span></span> 
  - <span data-ttu-id="483e4-163">Свойство **selectedKey** указывает выбранное значение, которое может быть строкой или числом.</span><span class="sxs-lookup"><span data-stu-id="483e4-163">The **selectedKey** property specifies the selected value, which can be a string or a number.</span></span> 
  - <span data-ttu-id="483e4-164">Свойство **disabled** указывает, отключено ли раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-164">The **disabled** property specifies if the dropdown control is disabled or not.</span></span> 
  - <span data-ttu-id="483e4-165">Свойство **stateKey** используется для принудительной повторной отрисовки компонента React.</span><span class="sxs-lookup"><span data-stu-id="483e4-165">The **stateKey** property is used to force the React component to re-render.</span></span>

3. <span data-ttu-id="483e4-166">Определите интерфейс компонента React для асинхронного раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-166">Define asynchronous dropdown React component interface.</span></span> <span data-ttu-id="483e4-167">В папке **src/controls/PropertyPaneAsyncDropdown/components** создайте файл **IAsyncDropdownState.ts** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-167">In the **src/controls/PropertyPaneAsyncDropdown/components** folder, create a new file named **IAsyncDropdownState.ts**, and enter the following code:</span></span>

  ```typescript
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

  export interface IAsyncDropdownState {
    loading: boolean;
    options: IDropdownOption[];
    error: string;
  }
  ```

  <span data-ttu-id="483e4-168">Интерфейс **IAsyncDropdownState** описывает состояние компонента React.</span><span class="sxs-lookup"><span data-stu-id="483e4-168">The **IAsyncDropdownState** interface describes the state of the React component:</span></span>
  - <span data-ttu-id="483e4-169">Свойство **loading** определяет, загружает ли компонент параметры в данный момент.</span><span class="sxs-lookup"><span data-stu-id="483e4-169">The **loading** property determines if the component is loading its options at the given moment.</span></span> 
  - <span data-ttu-id="483e4-170">Свойство **options** содержит все доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="483e4-170">The **options** property contains all available options.</span></span> 
  - <span data-ttu-id="483e4-171">Если произойдет ошибка, она будет назначена свойству **error**, из которого она будет передана пользователю.</span><span class="sxs-lookup"><span data-stu-id="483e4-171">If an error occurred, it is assigned to the **error** property from where it is communicated to the user.</span></span>

4. <span data-ttu-id="483e4-172">Определите компонент React асинхронного раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-172">Define the asynchronous dropdown React component.</span></span> <span data-ttu-id="483e4-173">В папке **src/controls/PropertyPaneAsyncDropdown/components** создайте файл **AsyncDropdown.tsx** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-173">In the **src/controls/PropertyPaneAsyncDropdown/components** folder, create a new file named **AsyncDropdown.tsx**, and enter the following code:</span></span>

  ```typescriptx
  import * as React from 'react';
  import { Dropdown, IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
  import { Spinner } from 'office-ui-fabric-react/lib/components/Spinner';
  import { IAsyncDropdownProps } from './IAsyncDropdownProps';
  import { IAsyncDropdownState } from './IAsyncDropdownState';

  export default class AsyncDropdown extends React.Component<IAsyncDropdownProps, IAsyncDropdownState> {
    private selectedKey: React.ReactText;

    constructor(props: IAsyncDropdownProps, state: IAsyncDropdownState) {
      super(props);
      this.selectedKey = props.selectedKey;

      this.state = {
        loading: false,
        options: undefined,
        error: undefined
      };
    }

    public componentDidMount(): void {
      this.loadOptions();
    }

    public componentDidUpdate(prevProps: IAsyncDropdownProps, prevState: IAsyncDropdownState): void {
      if (this.props.disabled !== prevProps.disabled ||
        this.props.stateKey !== prevProps.stateKey) {
        this.loadOptions();
      }
    }

    private loadOptions(): void {
      this.setState({
        loading: true,
        error: undefined,
        options: undefined
      });

      this.props.loadOptions()
        .then((options: IDropdownOption[]): void => {
          this.setState({
            loading: false,
            error: undefined,
            options: options
          });
        }, (error: any): void => {
          this.setState((prevState: IAsyncDropdownState, props: IAsyncDropdownProps): IAsyncDropdownState => {
            prevState.loading = false;
            prevState.error = error;
            return prevState;
          });
        });
    }

    public render(): JSX.Element {
      const loading: JSX.Element = this.state.loading ? <div><Spinner label={'Loading options...'} /></div> : <div />;
      const error: JSX.Element = this.state.error !== undefined ? <div className={'ms-TextField-errorMessage ms-u-slideDownIn20'}>Error while loading items: {this.state.error}</div> : <div />;

      return (
        <div>
          <Dropdown label={this.props.label}
            disabled={this.props.disabled || this.state.loading || this.state.error !== undefined}
            onChanged={this.onChanged.bind(this)}
            selectedKey={this.selectedKey}
            options={this.state.options} />
          {loading}
          {error}
        </div>
      );
    }

    private onChanged(option: IDropdownOption, index?: number): void {
      this.selectedKey = option.key;
      // reset previously selected options
      const options: IDropdownOption[] = this.state.options;
      options.forEach((o: IDropdownOption): void => {
        if (o.key !== option.key) {
          o.selected = false;
        }
      });
      this.setState((prevState: IAsyncDropdownState, props: IAsyncDropdownProps): IAsyncDropdownState => {
        prevState.options = options;
        return prevState;
      });
      if (this.props.onChanged) {
        this.props.onChanged(option, index);
      }
    }
  }
  ```

  <span data-ttu-id="483e4-174">Класс **AsyncDropdown** представляет компонент React, используемый для отрисовки асинхронного раскрывающегося меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-174">The **AsyncDropdown** class represents the React component used to render the asynchronous dropdown property pane control:</span></span>

  - <span data-ttu-id="483e4-175">При первой загрузке компонента изменится метод **componentDidMount** или его свойство (**disabled** либо **stateKey**), и он загрузит доступные параметры, вызвав метод **loadOptions**, переданный через свойства.</span><span class="sxs-lookup"><span data-stu-id="483e4-175">When the component first loads, the **componentDidMount** method, or its **disabled** or **stateKey** properties, change, and it loads the available options by calling the **loadOptions** method passed through the properties.</span></span> 
  - <span data-ttu-id="483e4-176">После загрузки параметров компонент показывает доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="483e4-176">After the options are loaded, the component updates its state showing the available options.</span></span> 
  - <span data-ttu-id="483e4-177">Раскрывающееся меню отрисовывается с помощью [компонента раскрывающегося меню на базе Office UI Fabric React](https://developer.microsoft.com/ru-RU/fabric#/components/dropdown).</span><span class="sxs-lookup"><span data-stu-id="483e4-177">The dropdown itself is rendered by using the [Office UI Fabric React dropdown component](https://developer.microsoft.com/ru-RU/fabric#/components/dropdown).</span></span> 
  - <span data-ttu-id="483e4-178">Когда компонент загружает доступные параметры, он показывает вертушку, используя [компонент вертушки на базе Office UI Fabric React](https://developer.microsoft.com/ru-RU/fabric#/components/spinner).</span><span class="sxs-lookup"><span data-stu-id="483e4-178">When the component is loading the available options, it displays a spinner by using the [Office UI Fabric React spinner component](https://developer.microsoft.com/ru-RU/fabric#/components/spinner).</span></span>


<span data-ttu-id="483e4-179">Далее необходимо определить пользовательский элемент управления области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-179">The next step is to define the custom property pane control.</span></span> <span data-ttu-id="483e4-180">Этот элемент управления используется в веб-части при определении свойств в области свойств и отрисовывается с помощью заданного компонента React.</span><span class="sxs-lookup"><span data-stu-id="483e4-180">This control is used inside the web part when defining properties in the property pane, and renders using the previously defined React component.</span></span>

### <a name="add-asynchronous-dropdown-property-pane-control"></a><span data-ttu-id="483e4-181">Как добавить асинхронное раскрывающееся меню области свойств</span><span class="sxs-lookup"><span data-stu-id="483e4-181">Add asynchronous dropdown property pane control</span></span>

1. <span data-ttu-id="483e4-182">Определите свойства асинхронного раскрывающегося меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-182">Define asynchronous dropdown property pane control properties.</span></span> <span data-ttu-id="483e4-183">У пользовательского элемента управления области свойств есть два набора свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-183">A custom property pane control has two sets of properties.</span></span> 
  
  <span data-ttu-id="483e4-184">Первый из них доступен для всех и используется для определения свойства веб-части.</span><span class="sxs-lookup"><span data-stu-id="483e4-184">The first set of properties are exposed publicly and are used to define the web part property inside the web part.</span></span> <span data-ttu-id="483e4-185">К этим свойствам компонента относятся подпись, которая отображается рядом с элементом управления, минимальное и максимальное значения вертушки и доступные параметры раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-185">These properties are component-specific properties, such as the label displayed next to the control, minimum and maximum values for a spinner, or available options for a dropdown.</span></span> <span data-ttu-id="483e4-186">Если добавляете пользовательский элемент управления области свойств, тип, описывающий эти свойства, необходимо передавать как тип **TProperties** при реализации интерфейса `IPropertyPaneField<TProperties>`.</span><span class="sxs-lookup"><span data-stu-id="483e4-186">When defining a custom property pane control, the type describing these properties must be passed as the **TProperties** type when implementing the `IPropertyPaneField<TProperties>` interface.</span></span>

  <span data-ttu-id="483e4-p115">Второй набор состоит из личных свойств, которые используются в пользовательском элементе управления области свойств. Для правильной отрисовки пользовательского элемента управления эти свойства должны соответствовать требованиям API SharePoint Framework. Эти свойства должны использовать интерфейс **IPropertyPaneCustomFieldProps** из пакета **@microsoft/sp-webpart-base**.</span><span class="sxs-lookup"><span data-stu-id="483e4-p115">The second set of properties are private properties used internally inside the custom property pane control. These properties have to adhere to the SharePoint Framework APIs for the custom control to render correctly. These properties must implement the **IPropertyPaneCustomFieldProps** interface from the **@microsoft/sp-webpart-base** package.</span></span>

2. <span data-ttu-id="483e4-190">Определите общедоступные свойства для асинхронного раскрывающегося меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-190">Define the public properties for the asynchronous dropdown property pane control.</span></span> <span data-ttu-id="483e4-191">В папке **src/controls/PropertyPaneAsyncDropdown** создайте файл **IPropertyPaneAsyncDropdownProps.ts** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-191">In the **src/controls/PropertyPaneAsyncDropdown** folder, create a new file named **IPropertyPaneAsyncDropdownProps.ts**, and enter the following code:</span></span>

  ```typescript
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';

  export interface IPropertyPaneAsyncDropdownProps {
    label: string;
    loadOptions: () => Promise<IDropdownOption[]>;
    onPropertyChange: (propertyPath: string, newValue: any) => void;
    selectedKey: string | number;
    disabled?: boolean;
  }
  ```

  <span data-ttu-id="483e4-192">В интерфейсе **IPropertyPaneAsyncDropdownProps**:</span><span class="sxs-lookup"><span data-stu-id="483e4-192">In the **IPropertyPaneAsyncDropdownProps** interface:</span></span>
  - <span data-ttu-id="483e4-193">Свойство **label** определяет подпись, которая отображается рядом с раскрывающимся меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-193">The **label** property defines the label displayed next to the dropdown.</span></span> 
  - <span data-ttu-id="483e4-194">Делегат **loadOptions** определяет метод, который вызывается для загрузки доступных параметров раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-194">The **loadOptions** delegate defines the method that is called to load the available dropdown options.</span></span> 
  - <span data-ttu-id="483e4-195">Делегат **onPropertyChange** определяет метод, который вызывается, когда пользователь выбирает значение в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-195">The **onPropertyChange** delegate defines a method that is called when the user selects a value in the dropdown.</span></span> 
  - <span data-ttu-id="483e4-196">Свойство **selectedKey** возвращает выбранное значение раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-196">The **selectedKey** property returns the selected dropdown value.</span></span> 
  - <span data-ttu-id="483e4-197">Свойство **disabled** указывает, отключен ли элемент управления.</span><span class="sxs-lookup"><span data-stu-id="483e4-197">The **disabled** property specifies whether the control is disabled or not.</span></span>

3. <span data-ttu-id="483e4-198">Определите внутренние свойства для асинхронного раскрывающегося меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-198">Define the internal properties for the asynchronous dropdown property pane control.</span></span> <span data-ttu-id="483e4-199">В папке **src/controls/PropertyPaneAsyncDropdown** создайте файл **IPropertyPaneAsyncDropdownInternalProps.ts** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-199">In the **src/controls/PropertyPaneAsyncDropdown** folder, create a new file named **IPropertyPaneAsyncDropdownInternalProps.ts**, and enter the following code:</span></span>

  ```typescript
  import { IPropertyPaneCustomFieldProps } from '@microsoft/sp-webpart-base';
  import { IPropertyPaneAsyncDropdownProps } from './IPropertyPaneAsyncDropdownProps';

  export interface IPropertyPaneAsyncDropdownInternalProps extends IPropertyPaneAsyncDropdownProps, IPropertyPaneCustomFieldProps {
  }
  ```

  <span data-ttu-id="483e4-200">Интерфейс **IPropertyPaneAsyncDropdownInternalProps** не определяет новые свойства, но он объединяет свойства из заданного интерфейса **IPropertyPaneAsyncDropdownProps** и стандартного интерфейса SharePoint Framework **IPropertyPaneCustomFieldProps**, что необходимо для правильной работы пользовательского элемента управления.</span><span class="sxs-lookup"><span data-stu-id="483e4-200">While the **IPropertyPaneAsyncDropdownInternalProps** interface doesn't define any new properties, it combines the properties from the previously defined **IPropertyPaneAsyncDropdownProps** interface and the standard SharePoint Framework **IPropertyPaneCustomFieldProps** interface, which is required for a custom control to run correctly.</span></span>

4. <span data-ttu-id="483e4-201">Определите асинхронное раскрывающееся меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-201">Define the asynchronous dropdown property pane control.</span></span> <span data-ttu-id="483e4-202">В папке **src/controls/PropertyPaneAsyncDropdown** создайте файл **PropertyPaneAsyncDropdown.ts** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-202">In the **src/controls/PropertyPaneAsyncDropdown** folder, create a new file named **PropertyPaneAsyncDropdown.ts**, and enter the following code:</span></span>

  ```typescript
  import * as React from 'react';
  import * as ReactDom from 'react-dom';
  import {
    IPropertyPaneField,
    PropertyPaneFieldType
  } from '@microsoft/sp-webpart-base';
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
  import { IPropertyPaneAsyncDropdownProps } from './IPropertyPaneAsyncDropdownProps';
  import { IPropertyPaneAsyncDropdownInternalProps } from './IPropertyPaneAsyncDropdownInternalProps';
  import AsyncDropdown from './components/AsyncDropdown';
  import { IAsyncDropdownProps } from './components/IAsyncDropdownProps';

  export class PropertyPaneAsyncDropdown implements IPropertyPaneField<IPropertyPaneAsyncDropdownProps> {
    public type: PropertyPaneFieldType = PropertyPaneFieldType.Custom;
    public targetProperty: string;
    public properties: IPropertyPaneAsyncDropdownInternalProps;
    private elem: HTMLElement;

    constructor(targetProperty: string, properties: IPropertyPaneAsyncDropdownProps) {
      this.targetProperty = targetProperty;
      this.properties = {
        key: properties.label,
        label: properties.label,
        loadOptions: properties.loadOptions,
        onPropertyChange: properties.onPropertyChange,
        selectedKey: properties.selectedKey,
        disabled: properties.disabled,
        onRender: this.onRender.bind(this)
      };
    }

    public render(): void {
      if (!this.elem) {
        return;
      }

      this.onRender(this.elem);
    }

    private onRender(elem: HTMLElement): void {
      if (!this.elem) {
        this.elem = elem;
      }

      const element: React.ReactElement<IAsyncDropdownProps> = React.createElement(AsyncDropdown, {
        label: this.properties.label,
        loadOptions: this.properties.loadOptions,
        onChanged: this.onChanged.bind(this),
        selectedKey: this.properties.selectedKey,
        disabled: this.properties.disabled,
        // required to allow the component to be re-rendered by calling this.render() externally
        stateKey: new Date().toString()
      });
      ReactDom.render(element, elem);
    }

    private onChanged(option: IDropdownOption, index?: number): void {
      this.properties.onPropertyChange(this.targetProperty, option.key);
    }
  }
  ```

  <span data-ttu-id="483e4-203">Класс **PropertyPaneAsyncDropdown** реализует стандартный интерфейс SharePoint Framework **IPropertyPaneField**, используя интерфейс **IPropertyPaneAsyncDropdownProps** как контракт для общедоступных свойств, которые можно настроить в веб-части.</span><span class="sxs-lookup"><span data-stu-id="483e4-203">The **PropertyPaneAsyncDropdown** class implements the standard SharePoint Framework **IPropertyPaneField** interface by using the **IPropertyPaneAsyncDropdownProps** interface as a contract for its public properties that can be set from inside the web part.</span></span> <span data-ttu-id="483e4-204">Класс содержит следующие три общедоступные свойства, определяемые интерфейсом **IPropertyPaneField**:</span><span class="sxs-lookup"><span data-stu-id="483e4-204">The class contains the following three public properties defined by the **IPropertyPaneField** interface:</span></span>

  - <span data-ttu-id="483e4-205">**type**. Для пользовательского элемента управления области свойств необходимо использовать значение **PropertyPaneFieldType.Custom**.</span><span class="sxs-lookup"><span data-stu-id="483e4-205">**type**: Must be set to **PropertyPaneFieldType.Custom** for a custom property pane control.</span></span>
  - <span data-ttu-id="483e4-206">**targetProperty**: позволяет указать имя свойства веб-части, которое необходимо использовать с элементом управления.</span><span class="sxs-lookup"><span data-stu-id="483e4-206">**targetProperty**: Used to specify the name of the web part property to be used with the control.</span></span>
  - <span data-ttu-id="483e4-207">**properties**. Позволяет определить свойства элемента управления.</span><span class="sxs-lookup"><span data-stu-id="483e4-207">**properties**: Used to define control-specific properties.</span></span>

  <span data-ttu-id="483e4-208">Обратите внимание на то, что свойство **properties** относится к внутреннему типу **IPropertyPaneAsyncDropdownInternalProps**, а не к общедоступному интерфейсу **IPropertyPaneAsyncDropdownProps**, реализованному классом.</span><span class="sxs-lookup"><span data-stu-id="483e4-208">Notice how the **properties** property is of the internal **IPropertyPaneAsyncDropdownInternalProps** type rather than the public **IPropertyPaneAsyncDropdownProps** interface implemented by the class.</span></span> <span data-ttu-id="483e4-209">Это сделано для того, чтобы свойство **properties** могло определять метод **onRender**, необходимый для SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="483e4-209">This is on purpose so that the **properties** property can define the **onRender** method required by the SharePoint Framework.</span></span> <span data-ttu-id="483e4-210">Если бы метод **onRender** был частью общедоступного интерфейса **IPropertyPaneAsyncDropdownProps**, при использовании асинхронного раскрывающегося меню в веб-части вам потребовалось бы назначить ему значение в веб-части, что нежелательно.</span><span class="sxs-lookup"><span data-stu-id="483e4-210">If the **onRender** method was a part of the public **IPropertyPaneAsyncDropdownProps** interface, when using the asynchronous dropdown control in the web part, you would be required to assign a value to it inside the web part, which isn't desirable.</span></span>

  <span data-ttu-id="483e4-211">Класс **PropertyPaneAsyncDropdown** определяет общедоступный метод **render**, который можно использовать для обновления элемента управления.</span><span class="sxs-lookup"><span data-stu-id="483e4-211">The **PropertyPaneAsyncDropdown** class defines a public **render** method, which can be used to repaint the control.</span></span> <span data-ttu-id="483e4-212">Это удобно при наличии каскадных раскрывающихся меню, когда значение, выбранное в одном, определяет параметры, доступные в другом.</span><span class="sxs-lookup"><span data-stu-id="483e4-212">This is useful in situations such as when you have cascading dropdowns where the value set in one determines the options available in another.</span></span> <span data-ttu-id="483e4-213">Вызов метода **render** после выбора элемента позволяет зависимому раскрывающемуся меню загрузить доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="483e4-213">By calling the **render** method after selecting an item, you can have the dependent dropdown load available options.</span></span> <span data-ttu-id="483e4-214">Чтобы это работало, компонент React должен обнаружить, что элемент управления изменен.</span><span class="sxs-lookup"><span data-stu-id="483e4-214">For this to work, you have to make React detect that the control has changed.</span></span> <span data-ttu-id="483e4-215">Для этого установите текущую дату для свойства **stateKey**.</span><span class="sxs-lookup"><span data-stu-id="483e4-215">This is done by setting the value of the **stateKey** to the current date.</span></span> <span data-ttu-id="483e4-216">В результате при каждом вызове метода **onRender** компонент будет не только заново отрисовываться, но и обновлять доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="483e4-216">Using this trick, every time the **onRender** method is called, the component not only is re-rendered but also updates its available options.</span></span>

## <a name="use-the-asynchronous-dropdown-property-pane-control-in-the-web-part"></a><span data-ttu-id="483e4-217">Как использовать асинхронное раскрывающееся меню области свойств в веб-части</span><span class="sxs-lookup"><span data-stu-id="483e4-217">Use the asynchronous dropdown property pane control in the web part</span></span>

<span data-ttu-id="483e4-218">Теперь, когда асинхронное раскрывающееся меню области свойств готово, необходимо использовать его в веб-части, чтобы пользователи могли выбрать список.</span><span class="sxs-lookup"><span data-stu-id="483e4-218">With the asynchronous dropdown property pane control ready, the next step is to use it inside the web part, allowing users to select a list.</span></span>

### <a name="add-list-info-interface"></a><span data-ttu-id="483e4-219">Добавление интерфейса сведений о списке</span><span class="sxs-lookup"><span data-stu-id="483e4-219">Add list info interface</span></span>

<span data-ttu-id="483e4-220">Чтобы передавать сведения о доступных списках согласованно, определите интерфейс, который будет представлять сведения о списке.</span><span class="sxs-lookup"><span data-stu-id="483e4-220">To pass information about available lists around in a consistent manner, define an interface that represents information about a list.</span></span> <span data-ttu-id="483e4-221">В папке **src/webparts/listItems** создайте файл **IListInfo.ts** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="483e4-221">In the **src/webparts/listItems** folder, create a new file named **IListInfo.ts**, and enter the following code:</span></span>

```typescript
export interface IListInfo {
  Id: string;
  Title: string;
}
```

### <a name="use-the-asynchronous-dropdown-property-pane-control-to-render-the-listname-web-part-property"></a><span data-ttu-id="483e4-222">Как использовать асинхронное раскрывающееся меню области свойств для отрисовки свойства веб-части listName</span><span class="sxs-lookup"><span data-stu-id="483e4-222">Use the asynchronous dropdown property pane control to render the listName web part property</span></span>

1. <span data-ttu-id="483e4-223">Добавьте ссылку на обязательные типы.</span><span class="sxs-lookup"><span data-stu-id="483e4-223">Reference required types.</span></span> <span data-ttu-id="483e4-224">В верхней части файла **src/webparts/listItems/ListItemsWebPart.ts** импортируйте созданный класс **PropertyPaneAsyncDropdown**, добавив следующее:</span><span class="sxs-lookup"><span data-stu-id="483e4-224">In the top section of the **src/webparts/listItems/ListItemsWebPart.ts** file, import the previously created **PropertyPaneAsyncDropdown** class by adding:</span></span>

  ```typescript
  import { PropertyPaneAsyncDropdown } from '../../controls/PropertyPaneAsyncDropdown/PropertyPaneAsyncDropdown';
  ```

2. <span data-ttu-id="483e4-225">После этого кода добавьте ссылку на интерфейс **IDropdownOption** и две вспомогательные функции, необходимые для работы со свойствами веб-части.</span><span class="sxs-lookup"><span data-stu-id="483e4-225">After that code, add a reference to the **IDropdownOption** interface and two helpers functions required to work with web part properties.</span></span>

  ```typescript
  import { IDropdownOption } from 'office-ui-fabric-react/lib/components/Dropdown';
  import { update, get } from '@microsoft/sp-lodash-subset';
  ```

  <br/>

  ![Ссылки на класс PropertyPaneAsyncDropdown и интерфейс IDropdownOption, выделенные в Visual Studio Code](../../../images/custom-property-pane-control-web-part-imports.png)

3. <span data-ttu-id="483e4-227">Добавьте метод для загрузки доступных списков.</span><span class="sxs-lookup"><span data-stu-id="483e4-227">Add method to load available lists.</span></span> <span data-ttu-id="483e4-228">В классе **ListItemsWebPart** добавьте метод для загрузки доступных списков.</span><span class="sxs-lookup"><span data-stu-id="483e4-228">In the **ListItemsWebPart** class, add a method to load available lists.</span></span> <span data-ttu-id="483e4-229">В этой статье используются фиктивные данные, но вы также можете вызвать REST API для SharePoint, чтобы извлечь список доступных списков из текущего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="483e4-229">In this article you use mock data, but you could also call the SharePoint REST API to retrieve the list of available lists from the current web.</span></span> <span data-ttu-id="483e4-230">Для имитации загрузки параметров из внешней службы метод использует двухсекундную задержку.</span><span class="sxs-lookup"><span data-stu-id="483e4-230">To simulate loading options from an external service, the method uses a two second delay.</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private loadLists(): Promise<IDropdownOption[]> {
      return new Promise<IDropdownOption[]>((resolve: (options: IDropdownOption[]) => void, reject: (error: any) => void) => {
        setTimeout(() => {
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

4. <span data-ttu-id="483e4-231">Добавьте метод для обработки изменения значения в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-231">Add method to handle the change of the value in the dropdown.</span></span> <span data-ttu-id="483e4-232">В классе **ListItemsWebPart** добавьте метод **onListChange**.</span><span class="sxs-lookup"><span data-stu-id="483e4-232">In the **ListItemsWebPart** class, add a new method named **onListChange**.</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private onListChange(propertyPath: string, newValue: any): void {
      const oldValue: any = get(this.properties, propertyPath);
      // store new value in web part properties
      update(this.properties, propertyPath, (): any => { return newValue; });
      // refresh web part
      this.render();
    }
  }
  ```

  <span data-ttu-id="483e4-233">После выбора списка в раскрывающемся меню следует сохранять выбранное значение в свойствах веб-части, а веб-часть — отрисовывать повторно для отображения выбранного свойства.</span><span class="sxs-lookup"><span data-stu-id="483e4-233">After selecting a list in the list dropdown, the selected value should be persisted in web part properties, and the web part should be re-rendered to reflect the selected property.</span></span>

5. <span data-ttu-id="483e4-234">Выполните отрисовку свойства веб-части списка с помощью асинхронного раскрывающегося меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-234">Render the list web part property by using the asynchronous dropdown property pane control.</span></span> <span data-ttu-id="483e4-235">В классе **ListItemsWebPart** измените метод **getPropertyPaneConfiguration** так, чтобы он использовал асинхронное раскрывающееся меню области свойств для отрисовки свойства веб-части **listName**.</span><span class="sxs-lookup"><span data-stu-id="483e4-235">In the **ListItemsWebPart** class, change the **getPropertyPaneConfiguration** method to use the asynchronous dropdown property pane control to render the **listName** web part property.</span></span>

  ```typescript
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
                  new PropertyPaneAsyncDropdown('listName', {
                    label: strings.ListFieldLabel,
                    loadOptions: this.loadLists.bind(this),
                    onPropertyChange: this.onListChange.bind(this),
                    selectedKey: this.properties.listName
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

6. <span data-ttu-id="483e4-236">Теперь вы сможете выбрать список, используя новое асинхронное раскрывающееся меню области свойств.</span><span class="sxs-lookup"><span data-stu-id="483e4-236">At this point, you should be able to select a list by using the newly created asynchronous dropdown property pane control.</span></span> <span data-ttu-id="483e4-237">Чтобы убедиться, что элемент управления работает должным образом, откройте командную строку и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="483e4-237">To verify that the control is working as expected, open the command-line and run:</span></span>

  ```sh
  gulp serve
  ```

  <br/>

  ![Асинхронное раскрывающееся меню загружает параметры, не блокируя пользовательский интерфейс веб-части](../../../images/custom-property-pane-control-loading-options.png)

  <br/>

  ![Выбор одного из параметров в асинхронном раскрывающемся меню области свойств](../../../images/custom-property-pane-control-selecting-option.png)

## <a name="implement-cascading-dropdowns-using-the-asynchronous-dropdown-property-pane-control"></a><span data-ttu-id="483e4-240">Реализация каскадных раскрывающихся списков с помощью раскрывающегося меню области свойств</span><span class="sxs-lookup"><span data-stu-id="483e4-240">Implement cascading dropdowns using the asynchronous dropdown property pane control</span></span>

<span data-ttu-id="483e4-241">При создании веб-частей SharePoint Framework может понадобиться реализовать конфигурацию, при которой доступные параметры зависят от другого параметра, выбранного ранее.</span><span class="sxs-lookup"><span data-stu-id="483e4-241">When building SharePoint Framework web parts, you might need to implement a configuration where the available options depend on another option chosen previously.</span></span> <span data-ttu-id="483e4-242">Например, сделать так, чтобы сначала пользователи выбирали список, а затем — элемент из этого списка.</span><span class="sxs-lookup"><span data-stu-id="483e4-242">A common example is to first let users choose a list and from that list select a list item.</span></span> <span data-ttu-id="483e4-243">Список доступных элементов будет зависеть от выбранного списка.</span><span class="sxs-lookup"><span data-stu-id="483e4-243">The list of available items would depend on the selected list.</span></span> <span data-ttu-id="483e4-244">Ниже описано, как реализовать такой сценарий, используя асинхронное раскрывающееся меню области свойств, реализованное на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="483e4-244">Here is how to implement such a scenario by using the asynchronous dropdown property pane control implemented in previous steps.</span></span>

### <a name="add-item-web-part-property"></a><span data-ttu-id="483e4-245">Добавление свойства веб-части item</span><span class="sxs-lookup"><span data-stu-id="483e4-245">Add item web part property</span></span>

1. <span data-ttu-id="483e4-246">В редакторе кода откройте файл **src/webparts/listItems/ListItemsWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="483e4-246">In the code editor, open the **src/webparts/listItems/ListItemsWebPart.manifest.json** file.</span></span> <span data-ttu-id="483e4-247">В разделе **properties** добавьте свойство **item**, чтобы оно выглядело следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483e4-247">To the **properties** section, add a new property named **item** so that it appears as follows:</span></span>

  ```typescript
  // ...
  "properties": {
    "listName": "",
    "item": ""
  }
  // ...
  ```

  <br/>

  ![Манифест веб-части с выделенным свойством веб-части item](../../../images/custom-property-pane-control-item-property-web-part-manifest.png)

2. <span data-ttu-id="483e4-249">Измените код в файле **src/webparts/listItems/IListItemsWebPartProps.ts** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483e4-249">Change the code in the **src/webparts/listItems/IListItemsWebPartProps.ts** file to:</span></span>

  ```typescript
  export interface IListItemsWebPartProps {
    listName: string;
    item: string;
  }
  ```

3. <span data-ttu-id="483e4-250">Измените содержимое файла **src/webparts/listItems/components/IListItemsProps.ts** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483e4-250">Change the contents of the **src/webparts/listItems/components/IListItemsProps.ts** file to:</span></span>

  ```typescript
  export interface IListItemsProps {
    listName: string;
    item: string;
  }
  ```

4. <span data-ttu-id="483e4-251">В файле **src/webparts/listItems/ListItemsWebPart.ts** замените код метода **render** следующим:</span><span class="sxs-lookup"><span data-stu-id="483e4-251">In the **src/webparts/listItems/ListItemsWebPart.ts** file, change the code of the **render** method to:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IListItemsProps> = React.createElement(ListItems, {
        listName: this.properties.listName,
        item: this.properties.item
      });

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

5. <span data-ttu-id="483e4-252">В файле **src/webparts/listItems/loc/mystrings.d.ts** измените интерфейс **IListItemsWebPartStrings** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="483e4-252">In the **src/webparts/listItems/loc/mystrings.d.ts** file, change the **IListItemsWebPartStrings** interface to:</span></span>

  ```typescript
  declare interface IListItemsWebPartStrings {
    PropertyPaneDescription: string;
    BasicGroupName: string;
    ListFieldLabel: string;
    ItemFieldLabel: string;
  }
  ```

6. <span data-ttu-id="483e4-253">В файле **src/webparts/listItems/loc/en-us.js** добавьте отсутствующее определение для строки **ItemFieldLabel**.</span><span class="sxs-lookup"><span data-stu-id="483e4-253">In the **src/webparts/listItems/loc/en-us.js** file, add the missing definition for the **ItemFieldLabel** string:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "ListFieldLabel": "List",
      "ItemFieldLabel": "Item"
    }
  });
  ```

### <a name="render-the-value-of-the-item-web-part-property"></a><span data-ttu-id="483e4-254">Отрисовка значения свойства веб-части item</span><span class="sxs-lookup"><span data-stu-id="483e4-254">Render the value of the item web part property</span></span>

<span data-ttu-id="483e4-255">В файле **src/webparts/listItems/components/ListItems.tsx** замените метод **render** на следующий:</span><span class="sxs-lookup"><span data-stu-id="483e4-255">In the **src/webparts/listItems/components/ListItems.tsx** file, change the **render** method to:</span></span>

```tsx
export default class ListItems extends React.Component<IListItemsProps, {}> {
  public render(): React.ReactElement<IListItemsProps> {
    return (
      <div className={styles.listItems}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-lg10 ms-xl8 ms-xlPush2 ms-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.listName)}</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.item)}</p>
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

### <a name="add-method-to-load-list-items"></a><span data-ttu-id="483e4-256">Добавление метода для загрузки элементов списка</span><span class="sxs-lookup"><span data-stu-id="483e4-256">Add method to load list items</span></span>

<span data-ttu-id="483e4-257">В файле **src/webparts/listItems/ListItemsWebPart.ts** добавьте метод в классе **ListItemsWebPart** для загрузки доступных элементов из выбранного списка.</span><span class="sxs-lookup"><span data-stu-id="483e4-257">In the **src/webparts/listItems/ListItemsWebPart.ts** file, in the **ListItemsWebPart** class, add a new method to load available list items from the selected list.</span></span> <span data-ttu-id="483e4-258">Как и для загрузки доступных списков, здесь используются фиктивные данные.</span><span class="sxs-lookup"><span data-stu-id="483e4-258">Like the method for loading available lists, you use mock data.</span></span> <span data-ttu-id="483e4-259">В зависимости от того, какой список выбран ранее, метод **loadItems** возвращает фиктивные элементы списка.</span><span class="sxs-lookup"><span data-stu-id="483e4-259">Depending on the previously selected list, the **loadItems** method returns mock list items.</span></span> <span data-ttu-id="483e4-260">Если список не выбран, метод разрешает обещание без данных.</span><span class="sxs-lookup"><span data-stu-id="483e4-260">When no list has been selected, the method resolves the promise without any data.</span></span>

```typescript
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private loadItems(): Promise<IDropdownOption[]> {
    if (!this.properties.listName) {
      // resolve to empty options since no list has been selected
      return Promise.resolve();
    }

    const wp: ListItemsWebPart = this;

    return new Promise<IDropdownOption[]>((resolve: (options: IDropdownOption[]) => void, reject: (error: any) => void) => {
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



### <a name="add-method-to-handle-the-selection-of-an-item"></a><span data-ttu-id="483e4-261">Добавление метода для обработки выбора элемента</span><span class="sxs-lookup"><span data-stu-id="483e4-261">Add method to handle the selection of an item</span></span>

<span data-ttu-id="483e4-262">В классе **ListItemsWebPart** добавьте метод **onListItemChange**.</span><span class="sxs-lookup"><span data-stu-id="483e4-262">In the **ListItemsWebPart** class, add a new method named **onListItemChange**.</span></span> <span data-ttu-id="483e4-263">После выбора элемента в раскрывающемся меню веб-часть должна сохранить новое значение в свойствах и обновиться с учетом изменений в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="483e4-263">After selecting an item in the items dropdown, the web part should store the new value in web part properties and re-render the web part to reflect the changes in the user interface.</span></span>

```typescript
export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
  // ...
  private onListItemChange(propertyPath: string, newValue: any): void {
    const oldValue: any = get(this.properties, propertyPath);
    // store new value in web part properties
    update(this.properties, propertyPath, (): any => { return newValue; });
    // refresh web part
    this.render();
  }
}
```


### <a name="render-the-item-web-part-property-in-the-property-pane"></a><span data-ttu-id="483e4-264">Отрисовка свойства веб-части item в области свойств</span><span class="sxs-lookup"><span data-stu-id="483e4-264">Render the item web part property in the property pane</span></span>

1. <span data-ttu-id="483e4-265">В классе **ListItemsWebPart** добавьте свойство класса **itemsDropdown**.</span><span class="sxs-lookup"><span data-stu-id="483e4-265">In the **ListItemsWebPart** class, add a new class property named **itemsDropdown**:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    private itemsDropDown: PropertyPaneAsyncDropdown;
    // ...
  }
  ```

2. <span data-ttu-id="483e4-266">Замените код метода **getPropertyPaneConfiguration** на такой:</span><span class="sxs-lookup"><span data-stu-id="483e4-266">Change the code of the **getPropertyPaneConfiguration** method to:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      // reference to item dropdown needed later after selecting a list
      this.itemsDropDown = new PropertyPaneAsyncDropdown('item', {
        label: strings.ItemFieldLabel,
        loadOptions: this.loadItems.bind(this),
        onPropertyChange: this.onListItemChange.bind(this),
        selectedKey: this.properties.item,
        // should be disabled if no list has been selected
        disabled: !this.properties.listName
      });

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
                  new PropertyPaneAsyncDropdown('listName', {
                    label: strings.ListFieldLabel,
                    loadOptions: this.loadLists.bind(this),
                    onPropertyChange: this.onListChange.bind(this),
                    selectedKey: this.properties.listName
                  }),
                  this.itemsDropDown
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

  <span data-ttu-id="483e4-267">Раскрывающееся меню для свойства item инициализируется так же, как раскрывающееся меню для свойства listName.</span><span class="sxs-lookup"><span data-stu-id="483e4-267">The dropdown for the item property is initialized similarly to the dropdown for the listName property.</span></span> <span data-ttu-id="483e4-268">Единственное отличие состоит в том, что после выбора списка раскрывающееся меню должно обновиться, экземпляр элемента управления должен быть назначен переменной класса.</span><span class="sxs-lookup"><span data-stu-id="483e4-268">The only difference is because after selecting a list, the items dropdown has to be refreshed, an instance of the control has to be assigned to the class variable.</span></span>

### <a name="load-items-for-the-selected-list"></a><span data-ttu-id="483e4-269">Загрузка элементов выбранного списка</span><span class="sxs-lookup"><span data-stu-id="483e4-269">Load items for the selected list</span></span>

<span data-ttu-id="483e4-270">Раскрывающееся меню становится доступным после выбора списка.</span><span class="sxs-lookup"><span data-stu-id="483e4-270">Initially when no list is selected, the items dropdown is disabled and becomes enabled after the user selects a list.</span></span> <span data-ttu-id="483e4-271">После выбора списка загружаются элементы этого списка в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="483e4-271">After selecting a list, the items dropdown also loads list items from that list.</span></span> 

1. <span data-ttu-id="483e4-272">Чтобы реализовать эту логику, дополните ранее заданный метод **onListChange**:</span><span class="sxs-lookup"><span data-stu-id="483e4-272">To implement this logic, extend the previously defined **onListChange** method to:</span></span>

  ```typescript
  export default class ListItemsWebPart extends BaseClientSideWebPart<IListItemsWebPartProps> {
    // ...
    private onListChange(propertyPath: string, newValue: any): void {
      const oldValue: any = get(this.properties, propertyPath);
      // store new value in web part properties
      update(this.properties, propertyPath, (): any => { return newValue; });
      // reset selected item
      this.properties.item = undefined;
      // store new value in web part properties
      update(this.properties, 'item', (): any => { return this.properties.item; });
      // refresh web part
      this.render();
      // reset selected values in item dropdown
      this.itemsDropDown.properties.selectedKey = this.properties.item;
      // allow to load items
      this.itemsDropDown.properties.disabled = false;
      // load items and re-render items dropdown
      this.itemsDropDown.render();
    }
    // ...
  }
  ```

  <span data-ttu-id="483e4-p134">После выбора списка выбранный элемент сбрасывается, сохраняется в свойствах веб-части и сбрасывается в раскрывающемся меню элементов. Раскрывающееся меню для выбора элемента становится доступным и обновляется для загрузки параметров.</span><span class="sxs-lookup"><span data-stu-id="483e4-p134">After selecting a list, the selected item is reset, persisted in web part properties, and reset in the items dropdown. The dropdown for selecting an item becomes enabled, and the dropdown is refreshed in order to load its options.</span></span>

2. <span data-ttu-id="483e4-275">Чтобы убедиться, что все работает должным образом, в командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="483e4-275">To verify that everything is working as expected, in the command-line run:</span></span>

  ```sh
  gulp serve
  ```

  <span data-ttu-id="483e4-276">После первого добавления веб-части на страницу и открытия ее области свойств вы увидите, что оба раскрывающихся меню отключены и загружают параметры.</span><span class="sxs-lookup"><span data-stu-id="483e4-276">After adding the web part to the page for the first time and opening its property pane, you should see both dropdowns disabled and loading their options.</span></span>

  ![Раскрывающиеся меню в области свойств веб-части загружают данные](../../../images/custom-property-pane-control-cascading-loading-lists.png)

  <br/>

  <span data-ttu-id="483e4-p135">После загрузки параметров становится доступным раскрывающееся меню списков. Так как список еще не выбран, раскрывающееся меню элементов остается отключенным.</span><span class="sxs-lookup"><span data-stu-id="483e4-p135">After the options have been loaded, the list dropdown becomes enabled. Because no list has been selected yet, the item dropdown remains disabled.</span></span>

  ![Раскрывающееся меню списков в области свойств веб-части активно. Раскрывающееся меню элементов отключено](../../../images/custom-property-pane-control-cascading-lists-loaded-items-disabled.png)

   <br/>

  <span data-ttu-id="483e4-282">После выбора списка раскрывающееся меню элементов загрузит элементы, доступные в этом списке.</span><span class="sxs-lookup"><span data-stu-id="483e4-282">After selecting a list in the list dropdown the item dropdown will load items available in that list.</span></span>

  ![Раскрывающееся меню элементов загружает доступные элементы после выбора списка в раскрывающемся меню списков](../../../images/custom-property-pane-control-cascading-loading-items.png)

   <br/>

  <span data-ttu-id="483e4-284">После загрузки доступных элементов станет доступным раскрывающееся меню элементов.</span><span class="sxs-lookup"><span data-stu-id="483e4-284">After the available items have been loaded, the item dropdown becomes enabled.</span></span>

  ![Выбор элемента в раскрывающемся меню элементов в области свойств веб-части](../../../images/custom-property-pane-control-cascading-items-loaded-enabled.png)

   <br/>

  <span data-ttu-id="483e4-286">После выбора элемента в раскрывающемся меню элементов веб-часть обновляется для отображения выбранного элемента.</span><span class="sxs-lookup"><span data-stu-id="483e4-286">After selecting an item in the item dropdown the web part is refreshed showing the selected item in its body.</span></span>

  ![Выбранные список и элемент в веб-части](../../../images/custom-property-pane-control-cascading-selected-list-item.png)

## <a name="see-also"></a><span data-ttu-id="483e4-288">См. также</span><span class="sxs-lookup"><span data-stu-id="483e4-288">See also</span></span>

- [<span data-ttu-id="483e4-289">Использование каскадных раскрывающихся меню для свойств веб-частей</span><span class="sxs-lookup"><span data-stu-id="483e4-289">Use cascading dropdowns in web part properties</span></span>](./use-cascading-dropdowns-in-web-part-properties.md)