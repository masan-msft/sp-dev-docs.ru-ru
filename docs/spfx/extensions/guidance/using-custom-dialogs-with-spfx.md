# <a name="use-custom-dialog-boxes-with-sharepoint-framework-extensions"></a>Использование настраиваемых диалоговых окон с расширениями SharePoint Framework

Вы можете использовать настраиваемые диалоговые окна, доступные в пакете **@microsoft/sp-dialog**, в контексте расширений SharePoint Framework или клиентских веб-частей. 

В этой статье описываются создание настраиваемого диалогового окна и его использование в контексте расширения ListView Command Set.

Пример кода, рассматриваемый в этой статье, можно найти в репозитории [sp-dev-fx-extensions](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-command-dialog).

## <a name="set-up-your-development-environment"></a>Настройка среды разработки

Чтобы создать настраиваемое диалоговое окно, необходимо выполнить действия, описанные в статье [Настройка среды разработки](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment). Убедитесь, что вы используете последние версии шаблонов Yeoman для SharePoint Framework.

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
* Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу **ВВОД**.
* Выберите **Use the current folder** (Использовать текущую папку) и нажмите клавишу **ВВОД**.
* Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании.
* Выберите **Extension** (Расширение) в качестве типа создаваемого клиентского компонента. 
* Выберите для создаваемого расширения тип **ListView Command Set**.

Далее вам потребуется указать определенные сведения о расширении.

* Используйте значение **DialogDemo** для имени решения и нажмите клавишу **ВВОД**.
* Оставьте значение по умолчанию (**DialogDemo description**) для описания решения и нажмите клавишу **ВВОД**.

![Генератор Yeoman для SharePoint предлагает создать решение расширения](../../../images/ext-com-dialog-yeoman-prompts.png)

После этого Yeoman установит необходимые зависимости и сформирует файлы решения, а также расширение *DialogDemo*. Это может занять несколько минут.

После успешного формирования должно появиться следующее сообщение:

!["Скаффолдинг клиентского решения SharePoint успешно выполнен".](../../../images/ext-com-dialog-yeoman-complete.png)

После скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:

```sh
npm shrinkwrap
```

Далее откройте папку проекта в редакторе кода. В инструкциях и на снимках экрана из этой статьи указан Visual Studio Code, но вы можете использовать любой редактор. Чтобы открыть папку в Visual Studio Code, выполните следующую команду в консоли:

```sh
code .
```

![Исходная структура Visual Studio Code после скаффолдинга](../../../images/ext-com-dialog-vs-code-initial.png)

## <a name="modify-the-extension-manifest"></a>Изменение манифеста расширения

Настройте манифест расширения так, чтобы в расширении была только одна кнопка. В редакторе кода откройте файл **./src/extensions/dialogDemo/DialogDemoCommandSet.manifest.json**. Замените раздел команд на следующий код JSON:

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

## <a name="create-a-custom-dialog-box"></a>Создание настраиваемого диалогового окна

Создайте файл с именем **ColorPickerDialog.tsx** в папке **./src/extensions/dialogDemo/**.

Добавьте приведенный ниже оператор импорта в начале нового файла. Мы создаем настраиваемое диалоговое окно с помощью [компонентов Office UI Fabric React](https://dev.office.com/fabric#/components), поэтому реализация будет основана на React. 


```ts
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

## <a name="test-the-custom-dialog-box-in-your-tenant"></a>Тестирование настраиваемого диалогового окна в клиенте

Откройте файл **serve.json** в папке **./config/** и проверьте текущие параметры в нем. Этот файл призван упростить отладку расширений SharePoint Framework. Вы можете обновить содержимое файла в соответствии с данными клиента и сайта, на котором будет тестироваться расширение. В первую очередь следует изменить значение свойства `pageUrl` в определении JSON так, чтобы оно соответствовало вашему клиенту.

Измените свойство `pageUrl` так, чтобы оно указывало на URL-адрес списка, в котором нужно тестировать функции диалогового окна.

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
> Уникальный идентификатор расширения автоматически обновляется для этого файла во время первоначального скаффолдинга. Если вы меняете свойства, которые будет использовать расширение, следует обновить файл **serve.json**, прежде чем приступать к отладке.

Вернитесь к консоли и выполните следующую команду:

```sh
gulp serve
```

Начнется упаковка решения, а полученный манифест станет доступен по адресу `localhost`. В соответствии с конфигурацией из файла **serve.json** в браузере откроется определенный URL-адрес, а параметры запроса будут автоматически заданы согласно конфигурации решения.

Согласитесь на загрузку манифестов отладки, нажав кнопку **Загрузить скрипты отладки** при появлении соответствующего запроса.

![Предупреждение о разрешении скриптов отладки](../../../images/ext-com-dialog-debug-scripts.png)

Обратите внимание на то, что новая кнопка НЕ отображается на панели инструментов по умолчанию, так как стандартное решение требует выбора одного элемента списка. Если список или библиотека не содержит элементов, создайте элемент или отправьте документ. 

Выберите элемент из списка или библиотеки. После этого на панели инструментов появится кнопка с текстом *Open Custom Dialog box* (Открыть настраиваемое диалоговое окно).

![Кнопка "Open Cusotm Dialog" (Открыть настраиваемое диалоговое окно) на панели инструментов](../../../images/ext-com-dialog-button-in-toolbar.png)

Нажмите кнопку *Open Custom Dialog box* (Открыть настраиваемое диалоговое окно), чтобы настраиваемое диалоговое окно отобразилось в представлении списка. 

![Палитра, отображаемая в режиме диалогового окна](../../../images/ext-com-dialog-visible-dialog.png)

Выберите цвет в *палитре* и нажмите кнопку **ОК**, чтобы проверить, как код возвращает вызывающей стороне выбранное значение, которое затем отображается в стандартном диалоговом окне предупреждения.

![Диалоговое окно со сведениями о выбранном цвете](../../../images/ext-com-dialog-oob-alert-dialog.png)

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!