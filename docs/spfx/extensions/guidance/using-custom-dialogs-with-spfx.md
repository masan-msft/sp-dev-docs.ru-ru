---
title: "Учебник: использование настраиваемых диалоговых окон с расширениями SharePoint Framework"
description: "Создание настраиваемого диалогового окна и его использование в контексте расширения ListView Command Set."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 00e66b3c45e35c2dd83f19799996c42dc8d6b0b5
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a><span data-ttu-id="10926-103">Использование настраиваемых диалоговых окон с расширениями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="10926-103">Use custom dialog boxes with SharePoint Framework Extensions</span></span>

<span data-ttu-id="10926-104">Вы можете использовать настраиваемые диалоговые окна, доступные в пакете **[@microsoft/sp-dialog](https://www.npmjs.com/package/@microsoft/sp-dialog)**, в контексте расширений SharePoint Framework или клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="10926-104">You can use custom dialog boxes, available from the [@microsoft/sp-dialog](https://www.npmjs.com/package/@microsoft/sp-dialog) package, within the context of SharePoint Framework Extensions or client-side web parts.</span></span> 

<span data-ttu-id="10926-105">В этой статье описываются создание настраиваемого диалогового окна и его использование в контексте расширения ListView Command Set.</span><span class="sxs-lookup"><span data-stu-id="10926-105">This article describes how to create a custom dialog box and use it within the context of a ListView Command Set extension.</span></span>

<span data-ttu-id="10926-106">Пример кода, рассматриваемый в этой статье, можно найти в репозитории [sp-dev-fx-extensions](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog).</span><span class="sxs-lookup"><span data-stu-id="10926-106">You can access the sample code that this article is based on in the [sp-dev-fx-extensions](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog) repo.</span></span>

## <a name="set-up-your-development-environment"></a><span data-ttu-id="10926-107">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="10926-107">Set up your development environment</span></span>

<span data-ttu-id="10926-108">Чтобы создать настраиваемое диалоговое окно, необходимо выполнить действия, описанные в статье [Настройка среды разработки](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="10926-108">To create a custom dialog box, you need to follow the steps in [Set up your development environment](../../set-up-your-development-environment.md).</span></span> <span data-ttu-id="10926-109">Убедитесь, что вы используете последние версии шаблонов Yeoman для SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="10926-109">Make sure that you're using the latest SharePoint Framework Yeoman templates.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="10926-110">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="10926-110">Create a new project</span></span>

1. <span data-ttu-id="10926-111">Создайте папку проекта с помощью любой консоли:</span><span class="sxs-lookup"><span data-stu-id="10926-111">Create a new folder for the project by using your console of choice:</span></span>

  ```sh
  md dialog-cmd
  ```

2. <span data-ttu-id="10926-112">Перейдите в эту папку:</span><span class="sxs-lookup"><span data-stu-id="10926-112">Enter that folder:</span></span>

  ```sh
  cd dialog-cmd
  ```

3. <span data-ttu-id="10926-113">Запустите генератор Yeoman для SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="10926-113">Run the Yeoman generator for the SharePoint Framework:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="10926-114">Когда появится запрос, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="10926-114">When prompted:</span></span>

  * <span data-ttu-id="10926-115">Оставьте значение по умолчанию (**dialog-cmd**) для имени решения, а затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="10926-115">Accept the default value of **dialog-cmd** as your solution name, and then select Enter.</span></span>
  * <span data-ttu-id="10926-116">Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="10926-116">Select **SharePoint Online only (latest)**, and then select Enter.</span></span>
  * <span data-ttu-id="10926-117">Выберите **Use the current folder** (Использовать текущую папку), а затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="10926-117">Select **Use the current folder**, and then select Enter.</span></span>
  * <span data-ttu-id="10926-118">Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="10926-118">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span>
  * <span data-ttu-id="10926-119">Выберите **Extension** (Расширение) в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="10926-119">Select **Extension** as the client-side component type to be created.</span></span> 
  * <span data-ttu-id="10926-120">Выберите для создаваемого расширения тип **ListView Command Set**.</span><span class="sxs-lookup"><span data-stu-id="10926-120">Select **ListView Command Set** as the extension type to be created.</span></span>

5. <span data-ttu-id="10926-121">Далее вам потребуется указать определенные сведения о расширении:</span><span class="sxs-lookup"><span data-stu-id="10926-121">The next set of prompts asks for specific information about your extension:</span></span>

  * <span data-ttu-id="10926-122">Используйте значение **DialogDemo** для имени решения, а затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="10926-122">Use the value of **DialogDemo** as your extension name, and then select Enter.</span></span>
  * <span data-ttu-id="10926-123">Оставьте значение по умолчанию (**DialogDemo description**) для описания решения, а затем нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="10926-123">Accept the default value of **DialogDemo description** as your extension description, and then select Enter.</span></span>

  ![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../images/ext-com-dialog-yeoman-prompts.png)

  <span data-ttu-id="10926-125">После этого Yeoman установит необходимые зависимости и сформирует шаблоны файлов решения, а также расширение **DialogDemo**.</span><span class="sxs-lookup"><span data-stu-id="10926-125">At this point, Yeoman installs the required dependencies and scaffolds the solution files along with the **DialogDemo** extension.</span></span> <span data-ttu-id="10926-126">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="10926-126">This might take a few minutes.</span></span>

  <span data-ttu-id="10926-127">Когда скаффолдинг успешно закончится, появится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="10926-127">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

  ![Формирование шаблона клиентского решения SharePoint успешно выполнено](../../../images/ext-com-dialog-yeoman-complete.png)

6. <span data-ttu-id="10926-129">По завершении формирования шаблона заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="10926-129">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

7. <span data-ttu-id="10926-130">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="10926-130">Open your project folder in your code editor.</span></span> <span data-ttu-id="10926-131">В этой статье в инструкциях и на снимках экрана используется Visual Studio Code, но вы можете использовать любой другой редактор.</span><span class="sxs-lookup"><span data-stu-id="10926-131">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span> <span data-ttu-id="10926-132">Чтобы открыть папку в Visual Studio Code, выполните следующую команду в консоли:</span><span class="sxs-lookup"><span data-stu-id="10926-132">To open the folder in Visual Studio Code, use the following command in the console:</span></span>

  ```sh
  code .
  ```

  <br/>

  ![Исходная структура Visual Studio Code после скаффолдинга](../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a><span data-ttu-id="10926-134">Изменение манифеста расширения</span><span class="sxs-lookup"><span data-stu-id="10926-134">Modify the extension manifest</span></span>

<span data-ttu-id="10926-p104">Настройте манифест расширения так, чтобы в расширении была только одна кнопка. В редакторе кода откройте файл **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**. Замените раздел команд на следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="10926-p104">In the extension manifest, configure the extension to have only one button. In the code editor, open the **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json** file. Replace the commands section with the following JSON:</span></span>

```json
{
  //...
  "items": {
    "COMMAND_1": {
      "title": { "default": "Open Custom Dialog" },
      "iconImageUrl": "icons/request.png",
      "type": "command"
    }
  }
}
```

## <a name="create-a-custom-dialog-box"></a><span data-ttu-id="10926-138">Создание настраиваемого диалогового окна</span><span class="sxs-lookup"><span data-stu-id="10926-138">Create a custom dialog box</span></span>

1. <span data-ttu-id="10926-139">Создайте файл с именем **ColorPickerDialog.tsx** в папке **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="10926-139">Create a new file called **ColorPickerDialog.tsx** in the **./src/extensions/dialogDemo/** folder.</span></span>

2. <span data-ttu-id="10926-140">Добавьте приведенные ниже операторы импорта в начале нового файла.</span><span class="sxs-lookup"><span data-stu-id="10926-140">Add the following import statements at the top of the newly created file.</span></span> <span data-ttu-id="10926-141">Вы создаете настраиваемое диалоговое окно с помощью [компонентов Office UI Fabric React](https://developer.microsoft.com/ru-RU/fabric#/components), поэтому реализация будет основана на React.</span><span class="sxs-lookup"><span data-stu-id="10926-141">You're creating your custom dialog box by using the [Office UI Fabric React components](https://developer.microsoft.com/ru-RU/fabric#/components), so the implementation is in React.</span></span> 

  ```typescript
  import * as React from 'react';
  import * as ReactDOM from 'react-dom';
  import { BaseDialog, IDialogConfiguration } from '@microsoft/sp-dialog';
  import {
    autobind,
    ColorPicker,
    PrimaryButton,
    Button,
    DialogFooter,
    DialogContent
  } from 'office-ui-fabric-react';

  ```

3. <span data-ttu-id="10926-142">Добавьте приведенное ниже определение интерфейса сразу после операторов импорта.</span><span class="sxs-lookup"><span data-stu-id="10926-142">Add the following interface definition just under the import statements.</span></span> <span data-ttu-id="10926-143">Оно будет использоваться для передачи сведений и функций между расширением ListView Command Set и настраиваемым диалоговым окном.</span><span class="sxs-lookup"><span data-stu-id="10926-143">This is used to pass information and functions between your ListView Command Set extension and your custom dialog box.</span></span>

  ```typescript
  interface IColorPickerDialogContentProps {
    message: string;
    close: () => void;
    submit: (color: string) => void;
    defaultColor?: string;
  }
  ```

4. <span data-ttu-id="10926-144">Добавьте приведенный ниже класс сразу после определения интерфейса.</span><span class="sxs-lookup"><span data-stu-id="10926-144">Add the following class just under the interface definition.</span></span> <span data-ttu-id="10926-145">Этот класс React отвечает за отрисовку пользовательского интерфейса в настраиваемом диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="10926-145">This React class is responsible for rendering the UI experiences inside the custom dialog box.</span></span> <span data-ttu-id="10926-146">Обратите внимание, что мы используем компоненты Office UI Fabric React для фактической отрисовки и просто передаем необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="10926-146">Notice that you use the Office UI Fabric React components for actual rendering and just pass the needed properties.</span></span>  

  ```typescript
  class ColorPickerDialogContent extends React.Component<IColorPickerDialogContentProps, {}> {
    private _pickedColor: string;

    constructor(props) {
      super(props);
      // Default Color
      this._pickedColor = props.defaultColor || '#FFFFFF';
    }

    public render(): JSX.Element {
      return <DialogContent
        title='Color Picker'
        subText={this.props.message}
        onDismiss={this.props.close}
        showCloseButton={true}
      >
        <ColorPicker color={this._pickedColor} onColorChanged={this._onColorChange} />
        <DialogFooter>
          <Button text='Cancel' title='Cancel' onClick={this.props.close} />
          <PrimaryButton text='OK' title='OK' onClick={() => { this.props.submit(this._pickedColor); }} />
        </DialogFooter>
      </DialogContent>;
    }

    @autobind
    private _onColorChange(color: string): void {
      this._pickedColor = color;
    }
  }
  ```

5. <span data-ttu-id="10926-147">Добавьте приведенное ниже определение класса для настраиваемого диалогового окна под только что добавленным классом `ColorPickerDialogContent`.</span><span class="sxs-lookup"><span data-stu-id="10926-147">Add the following class definition for your custom dialog box under the `ColorPickerDialogContent` class that you just added.</span></span> <span data-ttu-id="10926-148">Это фактическое настраиваемое диалоговое окно, которое вызывается по нажатию кнопки "Набор команд ListView" и наследуется от объекта `BaseDialog`.</span><span class="sxs-lookup"><span data-stu-id="10926-148">This is the actual custom dialog box that is called from the ListView Command Set button click and is inherited from the `BaseDialog`.</span></span>

  ```typescript
  export default class ColorPickerDialog extends BaseDialog {
    public message: string;
    public colorCode: string;

    public render(): void {
      ReactDOM.render(<ColorPickerDialogContent
        close={ this.close }
        message={ this.message }
        defaultColor={ this.colorCode }
        submit={ this._submit }
      />, this.domElement);
    }

    public getConfig(): IDialogConfiguration {
      return {
        isBlocking: false
      };
    }

    @autobind
    private _submit(color: string): void {
      this.colorCode = color;
      this.close();
    }
  }
  ```

## <a name="associate-the-dialog-box-with-the-listview-command-set-button-click"></a><span data-ttu-id="10926-149">Связывание диалогового окна с нажатием кнопки "Набор команд ListView"</span><span class="sxs-lookup"><span data-stu-id="10926-149">Associate the dialog box with the ListView Command Set button click</span></span>

<span data-ttu-id="10926-150">Чтобы связать настраиваемое диалоговое окно с набором команд ListView, добавьте код инициализации диалогового окна в операцию нажатия кнопки.</span><span class="sxs-lookup"><span data-stu-id="10926-150">To associate the custom dialog box with your custom ListView Command Set, add the code to initiate the dialog box within the button click operation.</span></span>

1. <span data-ttu-id="10926-151">В редакторе кода откройте файл **DialogDemoCommandSet.ts** из папки **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="10926-151">In the code editor, open the **DialogDemoCommandSet.ts** file from the **./src/extensions/dialogDemo/** folder.</span></span>

2. <span data-ttu-id="10926-p109">Добавьте приведенные ниже операторы импорта под имеющимся оператором импорта **strings**. Они предназначены для использования настраиваемого диалогового окна в контексте набора команд ListView.</span><span class="sxs-lookup"><span data-stu-id="10926-p109">Add the following import statements under the existing **strings** import. These are for using the custom dialog box in the context of your ListView Command Set.</span></span> 

  ```typescript
  import ColorPickerDialog from './ColorPickerDialog';
  ```

3. <span data-ttu-id="10926-p110">Добавьте приведенное ниже определение переменной `_colorCode` над функцией `onInit` в классе `DialogDemoCommandSet`. Оно используется для хранения цвета, выбранного в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="10926-p110">Add the following `_colorCode` variable definition above the `onInit` function in the `DialogDemoCommandSet` class. This is used to store the color picker dialog box result.</span></span>

  ```typescript
    private _colorCode: string;
  ```

4. <span data-ttu-id="10926-p111">Измените функцию `onExecute`, как показано ниже. Этот код:</span><span class="sxs-lookup"><span data-stu-id="10926-p111">Update the `onExecute` function as follows. This code does the following:</span></span>

  * <span data-ttu-id="10926-158">инициализирует настраиваемое диалоговое окно;</span><span class="sxs-lookup"><span data-stu-id="10926-158">Initiates the custom dialog box.</span></span>
  * <span data-ttu-id="10926-159">передает сообщение, используемое в качестве заголовка диалогового окна;</span><span class="sxs-lookup"><span data-stu-id="10926-159">Passes a message for the dialog box, which is used for the title.</span></span>
  * <span data-ttu-id="10926-160">передает код цвета диалогового окна со стандартным значением, если оно еще не задано;</span><span class="sxs-lookup"><span data-stu-id="10926-160">Passes a color code for the dialog box with a default value, if not yet set.</span></span>
  * <span data-ttu-id="10926-161">показывает настраиваемое диалоговое окно;</span><span class="sxs-lookup"><span data-stu-id="10926-161">Shows the custom dialog box.</span></span>
  * <span data-ttu-id="10926-162">получает и сохраняет значение, возвращаемое диалоговым окном;</span><span class="sxs-lookup"><span data-stu-id="10926-162">Receives and stores the return value from the dialog box.</span></span>
  * <span data-ttu-id="10926-163">показывает полученное значение в стандартном диалоговом окне с помощью функции `Dialog.alert()`.</span><span class="sxs-lookup"><span data-stu-id="10926-163">Shows the received value in a default dialog box by using the `Dialog.alert()` function.</span></span>

  ```typescript
    @override
    public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
      switch (event.itemId) {
        case 'COMMAND_1':
          const dialog: ColorPickerDialog = new ColorPickerDialog();
          dialog.message = 'Pick a color:';
          // Use 'EEEEEE' as the default color for first usage
          dialog.colorCode = this._colorCode || '#EEEEEE';
          dialog.show().then(() => {
            this._colorCode = dialog.colorCode;
            Dialog.alert(`Picked color: ${dialog.colorCode}`);
          });
          break;
        default:
          throw new Error('Unknown command');
      }
    }
  ```

## <a name="test-the-dialog-box-in-your-tenant"></a><span data-ttu-id="10926-164">Тестирование диалогового окна в клиенте</span><span class="sxs-lookup"><span data-stu-id="10926-164">Test the dialog box in your tenant</span></span>

1. <span data-ttu-id="10926-165">Откройте файл **serve.json** в папке **./config/** и обновите в нем текущие параметры.</span><span class="sxs-lookup"><span data-stu-id="10926-165">Open the **serve.json** file in the **./config/** folder and update the current settings in the file.</span></span> <span data-ttu-id="10926-166">Этот файл призван упростить отладку расширений SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="10926-166">This file is used to make debugging on SharePoint Framework Extensions easier.</span></span> <span data-ttu-id="10926-167">Вы можете обновить содержимое файла в соответствии с данными клиента и сайта, на котором будет тестироваться расширение.</span><span class="sxs-lookup"><span data-stu-id="10926-167">You can update the file content to match your own tenant and site details where you want to test your extension.</span></span> <span data-ttu-id="10926-168">В первую очередь следует изменить значение свойства `pageUrl` в определении JSON так, чтобы оно соответствовало вашему клиенту.</span><span class="sxs-lookup"><span data-stu-id="10926-168">The key value to update is the `pageUrl` property in the json definition to match your own tenant.</span></span>

2. <span data-ttu-id="10926-169">Измените свойство `pageUrl` так, чтобы оно указывало на URL-адрес списка, в котором нужно тестировать функции диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="10926-169">Update `pageUrl` to point to a list URL where you want to test the dialog functionality.</span></span>

  ```sh
    "serveConfigurations": {
      "default": {
        "pageUrl": "https://sppnp.sharepoint.com/sites/team/Shared%20Documents/Forms/AllItems.aspx",
        "customActions": {
          "9b98b919-fe5e-4758-ac91-6d62e582c4fe": {
            "location": "ClientSideExtension.ListViewCommandSet.CommandBar",
            "properties": {
              "sampleTextOne": "One item is selected in the list",
              "sampleTextTwo": "This command is always visible."
            }
          }
        }
      },
  ```

  > [!NOTE]
  > <span data-ttu-id="10926-170">Уникальный идентификатор расширения автоматически обновляется для этого файла во время первоначального формирования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="10926-170">The unique identifier of your extension is automatically updated to this file during initial scaffolding.</span></span> <span data-ttu-id="10926-171">Если вы обновляете свойства, которые используются расширением, следует обновить файл **serve.json**, прежде чем приступать к отладке.</span><span class="sxs-lookup"><span data-stu-id="10926-171">If you update the properties that your extension uses, you should update **serve.json** before you start debugging.</span></span>

3. <span data-ttu-id="10926-172">Вернитесь к консоли и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="10926-172">Return to the console and run the following command:</span></span>

  ```sh
  gulp serve
  ```

  <span data-ttu-id="10926-173">Начнется упаковка решения, а полученный манифест станет доступен по адресу `localhost`.</span><span class="sxs-lookup"><span data-stu-id="10926-173">This starts the bundling of your solution and serves the resulting manifest from the `localhost` address.</span></span> <span data-ttu-id="10926-174">В соответствии с конфигурацией из файла **serve.json** в браузере также откроется определенный URL-адрес, а параметры запроса будут автоматически заданы согласно конфигурации решения.</span><span class="sxs-lookup"><span data-stu-id="10926-174">Due to the configuration in the **serve.json** file, it also opens up a browser in the specific URL and automatically sets the query parameters based on the solution configuration.</span></span>

4. <span data-ttu-id="10926-175">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="10926-175">Accept the loading of debug manifests by selecting **Load debug scripts** when prompted.</span></span>

  ![Предупреждение о разрешении скриптов отладки](../../../images/ext-com-dialog-debug-scripts.png)

  <span data-ttu-id="10926-177">Обратите внимание, что новая кнопка *не* отображается на панели инструментов по умолчанию, так как стандартное решение требует выбора одного элемента списка.</span><span class="sxs-lookup"><span data-stu-id="10926-177">Notice that the new button is *not* visible in the toolbar by default because the default solution requires that you select one item from the list.</span></span> <span data-ttu-id="10926-178">Если список или библиотека не содержит элементов, создайте элемент или отправьте документ.</span><span class="sxs-lookup"><span data-stu-id="10926-178">If you do not have any items in the list or library, create an item or upload a document.</span></span> 

5. <span data-ttu-id="10926-179">Выберите элемент из списка или библиотеки. Обратите внимание, что на панели инструментов появится кнопка с текстом **Open Custom Dialog** (Открыть настраиваемое диалоговое окно).</span><span class="sxs-lookup"><span data-stu-id="10926-179">Select an item from the list or library, and notice how the **Open Custom Dialog** button is visible in the toolbar.</span></span>

  ![Кнопка "Open Custom Dialog" (Открыть настраиваемое диалоговое окно) на панели инструментов](../../../images/ext-com-dialog-button-in-toolbar.png)

6. <span data-ttu-id="10926-181">Нажмите кнопку **Open Custom Dialog** (Открыть настраиваемое диалоговое окно), чтобы настраиваемое диалоговое окно отобразилось в представлении списка.</span><span class="sxs-lookup"><span data-stu-id="10926-181">Click the **Open Custom Dialog** button to see your custom dialog box rendered within the list view.</span></span> 

  ![Палитра, отображаемая в режиме диалогового окна](../../../images/ext-com-dialog-visible-dialog.png)

7. <span data-ttu-id="10926-183">Выберите цвет в **палитре** и нажмите кнопку **ОК**, чтобы проверить, как код возвращает вызывающей стороне выбранное значение,</span><span class="sxs-lookup"><span data-stu-id="10926-183">Select a color in the **Color Picker**, and then select **OK** to test how the code is returning the selected value back to the caller.</span></span> <span data-ttu-id="10926-184">которое затем отображается в стандартном диалоговом окне предупреждения.</span><span class="sxs-lookup"><span data-stu-id="10926-184">The selection is then shown by using the default alert dialog box.</span></span>

  ![Диалоговое окно со сведениями о выбранном цвете](../../../images/ext-com-dialog-oob-alert-dialog.png)

> [!NOTE]
> <span data-ttu-id="10926-186">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="10926-186">If you find an issue in the documentation or in SharePoint Framework, report that to SharePoint engineering by using the [issue list at the sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="10926-187">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="10926-187">Thanks for your input in advance.</span></span>

## <a name="see-also"></a><span data-ttu-id="10926-188">См. также</span><span class="sxs-lookup"><span data-stu-id="10926-188">See also</span></span>

- [<span data-ttu-id="10926-189">Обзор расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="10926-189">Overview of SharePoint Framework Extensions</span></span>](../overview-extensions.md)