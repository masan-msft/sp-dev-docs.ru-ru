# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a>Использование настраиваемых диалоговых окон с расширениями SharePoint Framework

Вы можете использовать настраиваемые диалоговые окна, доступные в пакете **@microsoft/sp-dialog**, в контексте расширений SharePoint Framework или клиентских веб-частей. 

В этой статье описываются создание настраиваемого диалогового окна и его использование в контексте расширения с набором команд ListView.

>**Примечание.** В настоящее время функция настраиваемых диалоговых окон находится на этапе тестирования. Перед выпуском мы хотим собрать ваши отзывы. Чтобы оставить отзыв, [оформите отчет о проблеме в репозитории GitHub](https://github.com/SharePoint/sp-dev-docs/issues).

> Обратите внимание, что в настоящее время отладка настраиваемых наборов команд ListView в SharePoint Online доступна только в современном интерфейсе списков на классических сайтах групп, размещенных в **клиенте разработчика**.


Пример кода, на котором основана эта статья, можно найти в репозитории [](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog).

## <a name="set-up-your-development-environment"></a>Настройка среды разработки

Чтобы создать настраиваемое диалоговое окно, необходимо выполнить действия, описанные в статье [Настройка среды разработки](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment). Убедитесь, что вы используете последние версии шаблонов Yeoman для SharePoint Framework. 

Чтобы обновить шаблоны Yeoman для SharePoint Framework, выполните следующую команду:

```sh
npm install -g @microsoft/generator-sharepoint`
```

## <a name="create-a-new-project"></a>Создание проекта

Создайте папку проекта с помощью любой консоли:

```sh
md dialog-cmd
```

Перейдите к этой папке:

```sh
cd dialog-cmd
```

Запустите генератор Yeoman для SharePoint Framework.

```sh
yo @microsoft/sharepoint
```

Когда появится запрос, выполните указанные ниже действия.

* Оставьте значение по умолчанию (**dialog-cmd**) для имени решения и нажмите клавишу **ВВОД**.
* Выберите для создаваемого клиентского компонента тип **Extension (Preview)**. 
* Выберите для создаваемого расширения тип **ListView Command Set (Preview)**.

Далее вам потребуется указать определенные сведения о расширении.

* Используйте значение **DialogDemo** для имени решения и нажмите клавишу **ВВОД**.
* Оставьте значение по умолчанию (**DialogDemo description**) для описания решения и нажмите клавишу **ВВОД**.

![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../../images/ext-com-dialog-yeoman-prompts.png)

После этого Yeoman установит необходимые зависимости и сформирует файлы решения, а также расширение *DialogDemo*. Это может занять несколько минут. 

После успешного формирования должно появиться следующее сообщение:

!["Формирование клиентского решения SharePoint успешно выполнено".](../../../../images/ext-com-dialog-yeoman-complete.png)

>**Примечание.** Сведения об устранении неполадок см. в статье [Известные проблемы](../basics/known-issues).

Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор. Чтобы открыть папку в Visual Studio Code, выполните в консоли следующую команду:

```sh
code .
```

![Исходная структура Visual Studio Code после формирования](../../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a>Изменение манифеста расширения

Настройте манифест расширения так, чтобы в расширении была только одна кнопка. В редакторе кода откройте файл **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**. Замените раздел команд на следующий код JSON:

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

## <a name="add-the-sp-dialog-package-to-the-solution"></a>Добавление пакета sp-dialog в решение

Вернитесь к консоли и выполните приведенную ниже команду, чтобы включить API диалоговых окон в свое решение.

```sh
npm install @microsoft/sp-dialog --save
```

Так как вы используете параметр `--save`, эта зависимость будет добавлена в файл **package.json**. Это гарантирует, что она будет автоматически установлена при выполнении команды `npm install` (это важно при восстановлении или клонировании проекта в другом месте).

Вернитесь к Visual Studio Code (или другому редактору, который вы используете).

## <a name="create-a-custom-dialog-box"></a>Создание настраиваемого диалогового окна

Создайте файл с именем **ColorPickerDialog.tsx** в папке **./src/extensions/dialogDemo/**.

Добавьте приведенный ниже оператор импорта в начале нового файла. Мы создаем настраиваемое диалоговое окно с помощью [компонентов Office UI Fabric React](https://dev.office.com/fabric#/components), поэтому реализация будет основана на React. 

> **Примечание** В настоящее время компонент `DialogContent` предоставляется из каталога `@microsoft/sp-dialog`, но будет включен в состав компонентов Office UI Fabric React. 

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

Добавьте приведенное ниже определение интерфейса сразу после операторов импорта. Оно будет использоваться для передачи сведений и функций между набором команд ListView и настраиваемым диалоговым окном.

```ts
interface IColorPickerDialogContentProps {
  message: string;
  close: () => void;
  submit: (color: string) => void;
  defaultColor?: string;
}
```

Добавьте приведенный ниже класс сразу после определения интерфейса. Этот класс React отвечает за отрисовку пользовательского интерфейса в настраиваемом диалоговом окне. Обратите внимание, что мы используем компоненты Office UI Fabric React для фактической отрисовки и просто передаем необходимые свойства.  

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
Добавьте приведенное ниже определение класса к настраиваемому диалоговому окну под только что добавленным классом `ColorPickerDialogContent`. Это фактическое настраиваемое диалоговое окно, которое будет вызываться по нажатию кнопки набору команд ListView и наследуется от объекта `BaseDialog`.

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

## <a name="associate-the-custom-dialog-box-with-the-listview-command-set-button-click"></a>Связывание настраиваемого диалогового окна с нажатием кнопки набора команд ListView
Чтобы связать настраиваемое диалоговое окно с набором команд ListView, добавьте код инициализации диалогового окна в операцию нажатия кнопки.

В редакторе кода откройте файл **DialogDemoCommandSet.ts** из папки **./src/extensions/dialogDemo/**.

Добавьте приведенные ниже операторы импорта под имеющимся оператором импорта **strings**. Они предназначены для использования настраиваемого диалогового окна в контексте набора команд ListView. 

```ts
import { Dialog } from '@microsoft/sp-dialog';
import ColorPickerDialog from './ColorPickerDialog';
```

Добавьте приведенное ниже определение переменной `_colorCode` над функцией `onInit` в классе `DialogDemoCommandSet`. Оно используется для хранения цвета, выбранного в диалоговом окне.

```ts
  private _colorCode: string;
```

Измените функцию `onExecute`, как показано ниже. Этот код:

* инициализирует настраиваемое диалоговое окно;
* передает диалоговому окну сообщение, которое будет использоваться в качестве заголовка;
* передает код цвета диалоговому окну со значением по умолчанию, если оно еще не задано;
* показывает настраиваемое диалоговое окно;
* получает и сохраняет значение, возвращаемое диалоговым окном;
* показывает полученное значение в диалоговом окне по умолчанию с помощью функции `Dialog.alert()`.

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

## <a name="test-the-custom-dialog-box-in-your-tenant"></a>Тестирование настраиваемого диалогового окна в клиенте

Откройте файл **DialogDemoCommandSet.manifest.json** в папке **./src/extensions/dialogDemo/** и скопируйте значение **id**, которое будет использоваться в качестве параметра запроса отладки.

Вернитесь к консоли и выполните следующую команду:

```sh
gulp serve --nobrowser
```

Обратите внимание, что мы используем параметр `--nobrowser`. Запускать локальное рабочее место не требуется, так как в настоящее время невозможно выполнять отладку расширений локально.

Начнется упаковка решения, а полученный манифест станет доступен по адресу `localhost`.

![Исходная структура Visual Studio Code после формирования](../../../../images/ext-com-dialog-gulp-serve.png)

Для тестирования расширения перейдите к сайту в клиенте разработчика приложений для SharePoint Online.

Перейдите к существующему настраиваемому списку на сайте, содержащему несколько элементов, или создайте список и добавьте в него несколько элементов для тестирования. 

Добавьте к URL-адресу приведенные ниже параметры строки запроса. Обратите внимание, что вам потребуется обновить параметр **id** в соответствии с идентификатором расширения, указанным в файле **DialogDemoCommandSet.manifest.json**:

```
?loadSpfx=true&debugManifestsFile=https://localhost:4321/temp/manifests.js&customActions={"8701f44c-8c81-4e54-999d-62763e8f34d2":{"location":"ClientSideExtension.ListViewCommandSet.CommandBar"}}
```

Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-debug-scripts.png)

Обратите внимание, что на панели инструментов списка отображается кнопка с текстом *Open Custom Dialog box* (Открыть настраиваемое диалоговое окно).

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-button-in-toolbar.png)

Нажмите кнопку *Open Custom Dialog box*, чтобы настраиваемое диалоговое окно открылось в представлении списка. 

![Предупреждение о разрешении скриптов отладки](../../../../images/ext-com-dialog-visible-dialog.png)

Выберите цвет в *палитре* и нажмите кнопку **ОК**, чтобы проверить, как код возвращает вызывающей стороне выбранное значение, которое затем отображается в стандартном диалоговом окне предупреждения.

![Стандартное диалоговое окно предупреждения](../../../../images/ext-com-dialog-oob-alert-dialog.png)
