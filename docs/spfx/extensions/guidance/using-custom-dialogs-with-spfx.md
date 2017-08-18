# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a><span data-ttu-id="97d11-101">Использование настраиваемых диалоговых окон с расширениями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="97d11-101">Use custom dialog boxes with SharePoint Framework Extensions</span></span>

<span data-ttu-id="97d11-102">Вы можете использовать настраиваемые диалоговые окна, доступные в пакете **@microsoft/sp-dialog**, в контексте расширений SharePoint Framework или клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="97d11-102">You can use custom dialog boxes, available from the **@microsoft/sp-dialog** package, within the context of SharePoint Framework Extensions or client-side web parts.</span></span> 

<span data-ttu-id="97d11-103">В этой статье описываются создание настраиваемого диалогового окна и его использование в контексте расширения с набором команд ListView.</span><span class="sxs-lookup"><span data-stu-id="97d11-103">This article describes how to create a custom dialog box and use it within the context of a ListView Command Set extension.</span></span>

><span data-ttu-id="97d11-p101">**Примечание.** В настоящее время функция настраиваемых диалоговых окон находится на этапе тестирования. Перед выпуском мы хотим собрать ваши отзывы. Чтобы оставить отзыв, [оформите отчет о проблеме в репозитории GitHub](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="97d11-p101">**Note:** The custom dialog box feature is currently in preview. We are looking for your feedback before we release. To provide feedback, [file an issue in our GitHub repo](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

> <span data-ttu-id="97d11-107">Обратите внимание, что в настоящее время отладка настраиваемых наборов команд ListView в SharePoint Online доступна только в современном интерфейсе списков на классических сайтах групп, размещенных в **клиенте разработчика**.</span><span class="sxs-lookup"><span data-stu-id="97d11-107">Notice that debugging Custom ListView Sets in the SharePoint Online is currently only available from modern list experience in classic team sites hosted on dev tenant.</span></span>


<span data-ttu-id="97d11-108">Пример кода, на котором основана эта статья, можно найти в репозитории [](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog).</span><span class="sxs-lookup"><span data-stu-id="97d11-108">You can access the sample code that this article is based on in the [](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog) repo.</span></span>

## <a name="set-up-your-development-environment"></a><span data-ttu-id="97d11-109">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="97d11-109">Set up your development environment</span></span>

<span data-ttu-id="97d11-p102">Чтобы создать настраиваемое диалоговое окно, необходимо выполнить действия, описанные в статье [Настройка среды разработки](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment). Убедитесь, что вы используете последние версии шаблонов Yeoman для SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="97d11-p102">To create a custom dialog box, you'll need to follow the steps in the [Set up your development environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment). Make sure that you're using the latest SharePoint Framework Yeoman templates.</span></span> 

<span data-ttu-id="97d11-112">Чтобы обновить шаблоны Yeoman для SharePoint Framework, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="97d11-112">To update your SharePoint Framework Yeoman templates, run the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint`
```

## <a name="create-a-new-project"></a><span data-ttu-id="97d11-113">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="97d11-113">Create a new project</span></span>

<span data-ttu-id="97d11-114">Создайте папку проекта с помощью любой консоли:</span><span class="sxs-lookup"><span data-stu-id="97d11-114">Start by creating a new folder for the project using your console of choice:</span></span>

```sh
md dialog-cmd
```

<span data-ttu-id="97d11-115">Перейдите к этой папке:</span><span class="sxs-lookup"><span data-stu-id="97d11-115">And enter that folder:</span></span>

```sh
cd dialog-cmd
```

<span data-ttu-id="97d11-116">Запустите генератор Yeoman для SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="97d11-116">The run the Yeoman generator for SharePoint Framework</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="97d11-117">Когда появится запрос, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="97d11-117">When prompted:</span></span>

* <span data-ttu-id="97d11-118">Оставьте значение по умолчанию (**dialog-cmd**) для имени решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="97d11-118">Accept the default value of **dialog-cmd** as your solution name and press **Enter**.</span></span>
* <span data-ttu-id="97d11-119">Выберите для создаваемого клиентского компонента тип **Extension (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="97d11-119">Choose **Extension (Preview)** as the client-side component type to be created.</span></span> 
* <span data-ttu-id="97d11-120">Выберите для создаваемого расширения тип **ListView Command Set (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="97d11-120">Choose **ListView Command Set (Preview)** as the extension type to be created.</span></span>

<span data-ttu-id="97d11-121">Далее вам потребуется указать определенные сведения о расширении.</span><span class="sxs-lookup"><span data-stu-id="97d11-121">The next set of prompts will ask for specific information about your extension:</span></span>

* <span data-ttu-id="97d11-122">Используйте значение **DialogDemo** для имени решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="97d11-122">Accept the default value of **DialogDemo** as your extension name and press **Enter**.</span></span>
* <span data-ttu-id="97d11-123">Оставьте значение по умолчанию (**DialogDemo description**) для описания решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="97d11-123">Accept the default value of **DialogDemo description** as your extension description and press **Enter**.</span></span>

![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../../images/ext-com-dialog-yeoman-prompts.png)

<span data-ttu-id="97d11-p103">После этого Yeoman установит необходимые зависимости и сформирует файлы решения, а также расширение *DialogDemo*. Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="97d11-p103">At this point, Yeoman will install the required dependencies and scaffold the solution files along with the *HelloWorld* extension. This might take a few minutes.</span></span> 

<span data-ttu-id="97d11-127">После успешного формирования должно появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="97d11-127">When the scaffold is complete, you should see the following message indicating a successful scaffold:</span></span>

!["Формирование клиентского решения SharePoint успешно выполнено".](../../../../images/ext-com-dialog-yeoman-complete.png)

><span data-ttu-id="97d11-129">**Примечание.** Сведения об устранении неполадок см. в статье [Известные проблемы](../basics/known-issues).</span><span class="sxs-lookup"><span data-stu-id="97d11-129">For information about troubleshooting any errors, see [Known issues](../basics/known-issues).</span></span>

<span data-ttu-id="97d11-p104">Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор. Чтобы открыть папку в Visual Studio Code, выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="97d11-p104">When the scaffolding is complete, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots, but you can use any editor you prefer. To open the folder in Visual Studio Code, use the following command in the console:</span></span>

```sh
code .
```

![Исходная структура Visual Studio Code после формирования](../../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a><span data-ttu-id="97d11-134">Изменение манифеста расширения</span><span class="sxs-lookup"><span data-stu-id="97d11-134">Modify the extension manifest</span></span>

<span data-ttu-id="97d11-p105">Настройте манифест расширения так, чтобы в расширении была только одна кнопка. В редакторе кода откройте файл **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**. Замените раздел команд на следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="97d11-p105">In the extension manifest, configure extension to have only one button. In the code editor, open the **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json** file. Replace the commands section with the following JSON:</span></span>

```json
{
  //...
  "commands": {
    "COMMAND_1": {
      "title": "Open Custom Dialog",
      "iconImageUrl": "icons/request.png"
    }
  }
}
```

## <a name="add-the-sp-dialog-package-to-the-solution"></a><span data-ttu-id="97d11-138">Добавление пакета sp-dialog в решение</span><span class="sxs-lookup"><span data-stu-id="97d11-138">Add the sp-dialog package to the solution</span></span>

<span data-ttu-id="97d11-139">Вернитесь к консоли и выполните приведенную ниже команду, чтобы включить API диалоговых окон в свое решение.</span><span class="sxs-lookup"><span data-stu-id="97d11-139">Return to the console and execute the following command to include the dialog API in our solution.</span></span>

```sh
npm install @microsoft/sp-dialog --save
```

<span data-ttu-id="97d11-p106">Так как вы используете параметр `--save`, эта зависимость будет добавлена в файл **package.json**. Это гарантирует, что она будет автоматически установлена при выполнении команды `npm install` (это важно при восстановлении или клонировании проекта в другом месте).</span><span class="sxs-lookup"><span data-stu-id="97d11-p106">Because you're using the `--save` option, this dependency will be added to the **package.json** file. This ensures that it will be installed automatically when the `npm install` command runs (this is important when you restore or clone your project elsewhere).</span></span>

<span data-ttu-id="97d11-142">Вернитесь к Visual Studio Code (или другому редактору, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="97d11-142">Return to Visual Studio Code (or your preferred editor).</span></span>

## <a name="create-a-custom-dialog-box"></a><span data-ttu-id="97d11-143">Создание настраиваемого диалогового окна</span><span class="sxs-lookup"><span data-stu-id="97d11-143">Create a custom dialog box</span></span>

<span data-ttu-id="97d11-144">Создайте файл с именем **ColorPickerDialog.tsx** в папке **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="97d11-144">Create a new file called **ColorPickerDialog.tsx** to **./src/extensions/dialogDemo/** folder.</span></span>

<span data-ttu-id="97d11-p107">Добавьте приведенный ниже оператор импорта в начале нового файла. Мы создаем настраиваемое диалоговое окно с помощью [компонентов Office UI Fabric React](https://dev.office.com/fabric#/components), поэтому реализация будет основана на React.</span><span class="sxs-lookup"><span data-stu-id="97d11-p107">Add following import statements on the start of the newly created file. We are creating our custom dialog using Office UI Fabric React components, so the implementation will be in React.</span></span> 

> <span data-ttu-id="97d11-147">**Примечание** В настоящее время компонент `DialogContent` предоставляется из каталога `@microsoft/sp-dialog`, но будет включен в состав компонентов Office UI Fabric React.</span><span class="sxs-lookup"><span data-stu-id="97d11-147">**Note:** Currently the `DialogContent` component is coming from `@microsoft/sp-dialog`, but it will be included as part of the Office UI Fabric React components soon.</span></span> 

```ts
import * as React from 'react';
import * as ReactDOM from 'react-dom';
import { BaseDialog, IDialogConfiguration } from '@microsoft/sp-dialog';
import {
  autobind,
  ColorPicker,
  PrimaryButton,
  Button,
  DialogFooter
  // DialogContent <- This should be imported here for third parties
} from 'office-ui-fabric-react';
// Note: DialogContent is available in v2.32.0 of office-ui-fabric-react
// As a workaround we're importing it from sp-dialog until the next version bump
import { DialogContent } from '@microsoft/sp-dialog';
```

<span data-ttu-id="97d11-p108">Добавьте приведенное ниже определение интерфейса сразу после операторов импорта. Оно будет использоваться для передачи сведений и функций между набором команд ListView и настраиваемым диалоговым окном.</span><span class="sxs-lookup"><span data-stu-id="97d11-p108">Add following interface definition just below the import statements. This wil be used to bypass needed information and functions between the ListView Command Set extension and custom dialog.</span></span>

```ts
interface IColorPickerDialogContentProps {
  message: string;
  close: () => void;
  submit: (color: string) => void;
  defaultColor?: string;
}
```

<span data-ttu-id="97d11-p109">Добавьте приведенный ниже класс сразу после определения интерфейса. Этот класс React отвечает за отрисовку пользовательского интерфейса в настраиваемом диалоговом окне. Обратите внимание, что мы используем компоненты Office UI Fabric React для фактической отрисовки и просто передаем необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="97d11-p109">Add following class just below the interface definition. This React class is responsible for rendering the UI experiences inside of the custom dialog. Notice that we use the Office UI Fabric React components for actual rendering and just bypass the needed properties.</span></span>  

```ts
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
<span data-ttu-id="97d11-p110">Добавьте приведенное ниже определение класса к настраиваемому диалоговому окну под только что добавленным классом `ColorPickerDialogContent`. Это фактическое настраиваемое диалоговое окно, которое будет вызываться по нажатию кнопки набору команд ListView и наследуется от объекта `BaseDialog`.</span><span class="sxs-lookup"><span data-stu-id="97d11-p110">Add following class definition for our custom dialog under the just added class code. This one is the actual custom dialog, which will be called from the button click and which is inherited from the BaseDialog.</span></span>

```ts
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

## <a name="associate-the-custom-dialog-box-with-the-listview-command-set-button-click"></a><span data-ttu-id="97d11-155">Связывание настраиваемого диалогового окна с нажатием кнопки набора команд ListView</span><span class="sxs-lookup"><span data-stu-id="97d11-155">Associate the custom dialog box with the ListView Command Set button click</span></span>
<span data-ttu-id="97d11-156">Чтобы связать настраиваемое диалоговое окно с набором команд ListView, добавьте код инициализации диалогового окна в операцию нажатия кнопки.</span><span class="sxs-lookup"><span data-stu-id="97d11-156">To associate the custom dialog button to custom ListView Command Set, the code to initiate the dialog has to be added for the button click operation.</span></span>

<span data-ttu-id="97d11-157">В редакторе кода откройте файл **DialogDemoCommandSet.ts** из папки **./src/extensions/dialogDemo/**.</span><span class="sxs-lookup"><span data-stu-id="97d11-157">In the code editor, open the  **DialogDemoCommandSet.ts** file from **./src/extensions/dialogDemo/** folder.</span></span>

<span data-ttu-id="97d11-p111">Добавьте приведенные ниже операторы импорта под имеющимся оператором импорта **strings**. Они предназначены для использования настраиваемого диалогового окна в контексте набора команд ListView.</span><span class="sxs-lookup"><span data-stu-id="97d11-p111">Add following import statements under the existing **strings** import. These are for using the just created custom dialog in the context of ListView Command Set.</span></span> 

```ts
import { Dialog } from '@microsoft/sp-dialog';
import ColorPickerDialog from './ColorPickerDialog';
```

<span data-ttu-id="97d11-p112">Добавьте приведенное ниже определение переменной `_colorCode` над функцией `onInit` в классе `DialogDemoCommandSet`. Оно используется для хранения цвета, выбранного в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="97d11-p112">Add following `_colorCode` variable definition above `onInit` function in the `DialogDemoCommandSet` class. This is used to store teh color picker dialog result.</span></span>

```ts
  private _colorCode: string;
```

<span data-ttu-id="97d11-p113">Измените функцию `onExecute`, как показано ниже. Этот код:</span><span class="sxs-lookup"><span data-stu-id="97d11-p113">Update the `onExecute` function as follows. This code does the following:</span></span>

* <span data-ttu-id="97d11-164">инициализирует настраиваемое диалоговое окно;</span><span class="sxs-lookup"><span data-stu-id="97d11-164">Initiates the custom dialog box.</span></span>
* <span data-ttu-id="97d11-165">передает диалоговому окну сообщение, которое будет использоваться в качестве заголовка;</span><span class="sxs-lookup"><span data-stu-id="97d11-165">Passes a message for the dialog box, which is used for the title.</span></span>
* <span data-ttu-id="97d11-166">передает код цвета диалоговому окну со значением по умолчанию, если оно еще не задано;</span><span class="sxs-lookup"><span data-stu-id="97d11-166">Bypass color code for the dialog with default value, if not yet set</span></span>
* <span data-ttu-id="97d11-167">показывает настраиваемое диалоговое окно;</span><span class="sxs-lookup"><span data-stu-id="97d11-167">Shows the custom dialog box.</span></span>
* <span data-ttu-id="97d11-168">получает и сохраняет значение, возвращаемое диалоговым окном;</span><span class="sxs-lookup"><span data-stu-id="97d11-168">Receives and stores the return value from the dialog box.</span></span>
* <span data-ttu-id="97d11-169">показывает полученное значение в диалоговом окне по умолчанию с помощью функции `Dialog.alert()`.</span><span class="sxs-lookup"><span data-stu-id="97d11-169">Shows the received value in a default dialog box using the `Dialog.alert()` function.</span></span>

```ts
  @override
  public onExecute(event: IListViewCommandSetExecuteEventParameters): void {
    switch (event.commandId) {
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

## <a name="test-the-custom-dialog-box-in-your-tenant"></a><span data-ttu-id="97d11-170">Тестирование настраиваемого диалогового окна в клиенте</span><span class="sxs-lookup"><span data-stu-id="97d11-170">Test the custom dialog box in your tenant</span></span>

<span data-ttu-id="97d11-171">Откройте файл **DialogDemoCommandSet.manifest.json** в папке **./src/extensions/dialogDemo/** и скопируйте значение **id**, которое будет использоваться в качестве параметра запроса отладки.</span><span class="sxs-lookup"><span data-stu-id="97d11-171">Move to **DialogDemoCommandSet.manifest.json** file in **./src/extensions/dialogDemo/** folder and copy **id** value, which will be used in the debug query parameter.</span></span>

<span data-ttu-id="97d11-172">Вернитесь к консоли и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="97d11-172">Return to the console and run the following command:</span></span>

```sh
gulp serve --nobrowser
```

<span data-ttu-id="97d11-p114">Обратите внимание, что мы используем параметр `--nobrowser`. Запускать локальное рабочее место не требуется, так как в настоящее время невозможно выполнять отладку расширений локально.</span><span class="sxs-lookup"><span data-stu-id="97d11-p114">Notice that you use the `--nobrowser` option. You don't need to launch the local workbench because you currently cannot debug extensions locally.</span></span>

<span data-ttu-id="97d11-175">Начнется упаковка решения, а полученный манифест станет доступен по адресу `localhost`.</span><span class="sxs-lookup"><span data-stu-id="97d11-175">This will start bundling and will serve the resulting manifest from `localhost` address.</span></span>

![Исходная структура Visual Studio Code после формирования](../../../../images/ext-com-dialog-gulp-serve.png)

<span data-ttu-id="97d11-177">Для тестирования расширения перейдите к сайту в клиенте разработчика приложений для SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="97d11-177">To test your extension, navigate to a site in your SharePoint Online tenant.</span></span>

<span data-ttu-id="97d11-178">Перейдите к существующему настраиваемому списку на сайте, содержащему несколько элементов, или создайте список и добавьте в него несколько элементов для тестирования.</span><span class="sxs-lookup"><span data-stu-id="97d11-178">Move to an existing custom list in the site with some items or create a new list and add few items to it for testing purposes.</span></span> 

<span data-ttu-id="97d11-p115">Добавьте к URL-адресу приведенные ниже параметры строки запроса. Обратите внимание, что вам потребуется обновить параметр **id** в соответствии с идентификатором расширения, указанным в файле **DialogDemoCommandSet.manifest.json**:</span><span class="sxs-lookup"><span data-stu-id="97d11-p115">Append the following query string parameters to the URL. Notice that you will need to update the **id** to match your own extension identifier available from the **DialogDemoCommandSet.manifest.json** file:</span></span>

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"8701f44c-8c81-4e54-999d-62763e8f34d2":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

<span data-ttu-id="97d11-181">Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.</span><span class="sxs-lookup"><span data-stu-id="97d11-181">Accept the loading of Debug Manifests by clicking **Load debug scripts** when prompted:</span></span>

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-debug-scripts.png)

<span data-ttu-id="97d11-183">Обратите внимание, что на панели инструментов списка отображается кнопка с текстом *Open Custom Dialog box* (Открыть настраиваемое диалоговое окно).</span><span class="sxs-lookup"><span data-stu-id="97d11-183">Notice that the new button is visible in the toolbar of the list with the text *Open Custom Dialog box*.</span></span>

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-button-in-toolbar.png)

<span data-ttu-id="97d11-185">Нажмите кнопку *Open Custom Dialog box*, чтобы настраиваемое диалоговое окно открылось в представлении списка.</span><span class="sxs-lookup"><span data-stu-id="97d11-185">Choose the *Open Custom Dialog box* button to see your custom dialog box rendered within the list view.</span></span> 

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-visible-dialog.png)

<span data-ttu-id="97d11-p116">Выберите цвет в *палитре* и нажмите кнопку **ОК**, чтобы проверить, как код возвращает вызывающей стороне выбранное значение, которое затем отображается в стандартном диалоговом окне предупреждения.</span><span class="sxs-lookup"><span data-stu-id="97d11-p116">Choose a color in the *Color Picker* and click **OK** to test how the code is returning selected value back to caller, which is then shown using out-of-the-box alert dialog.</span></span>

![Стандартное диалоговое окно предупреждения](../../../../images/ext-com-dialog-oob-alert-dialog.png)
