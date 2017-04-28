# <a name="use-office-ui-fabric-react-components-in-your-sharepoint-client-side-web-part"></a>Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint

#### **Важно!** Для использования Office UI Fabric React необходимо обновить существующие проекты, чтобы они использовали @microsoft/sp-build-web@1.0.1 или более поздней версии. См. инструкции в конце этой статьи.

В этой статье описано, как создать простую веб-часть на базе компонента DocumentCard, доступного в [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react). Office UI Fabric React — это клиентская платформа, позволяющая создавать решения для Office и Office 365. Она включает большую коллекцию адаптивных компонентов для мобильных устройств, с помощью которых вы легко сможете создавать веб-части на языке дизайна Office.

На приведенном ниже изображении показан компонент DocumentCard, созданный с помощью Office UI Fabric React.

![Изображение компонента DocumentCard Fabric в рабочей среде SharePoint](../../../../images/fabric-components-doc-card-view-ex.png)

Указанные ниже действия также показаны в видео на [канале SharePoint PnP на YouTube](https://www.youtube.com/watch?v=1N6kNvLxyg4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq). 

<a href="https://www.youtube.com/watch?v=1N6kNvLxyg4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../../images/spfx-youtube-tutorial6.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="creating-a-new-web-part-project"></a>Создание проекта веб-части

Убедитесь, что вы используете последнюю версию. Выполните команду `yo` и следуйте инструкциям на экране, чтобы создать скелет проекта.

Создайте каталог проекта в удобном для вас расположении:

```
md documentcardexample-webpart
```
    
Перейдите к каталогу проекта:

```
cd documentcardexample-webpart
```

Убедитесь, что у вас установлена последняя версия `@microsoft/generator-sharepoint`, и создайте веб-часть, запустив генератор Yeoman для SharePoint:

```
yo @microsoft/sharepoint
```
    
Когда появится запрос:

* Оставьте имя по умолчанию (**documentcardexample-webpart**) для своего решения и нажмите клавишу **ВВОД**.
* Выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.
* Выберите **React** в качестве платформы и нажмите клавишу **ВВОД**.
* Укажите **DocumentCardExample** в качестве имени своей веб-части и нажмите клавишу **ВВОД**.
* Оставьте **описание DocumentCardExample** по умолчанию и нажмите клавишу **ВВОД**.

После этого Yeoman установит необходимые зависимости и применит скаффолдинг к файлам решения. Это может занять несколько минут. Yeoman также включит в проект веб-часть DocumentCardExample, применяя к нему скаффолдинг.
    
Когда процесс скаффолдинга завершится, введите в консоли следующий код, чтобы открыть проект веб-части в редакторе Visual Studio Code:

```
code .
```
    
Создание проекта веб-части с помощью платформы React завершено.

Откройте **DocumentCardExampleWebPart.ts** в папке **src\webparts\documentCardExample**. 

Как вы видите, метод `render` создает элемент React и обрабатывает его в элементе DOM веб-части.

```ts
  public render(): void {
    const element: React.ReactElement<IDocumentCardExampleProps > = React.createElement(
      DocumentCardExample,
      {
        description: this.properties.description
      }
    );
```
    
Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**. 
    
Это основной компонент React, добавленный генератором Yeoman в ваш проект, который обрабатывается в элементе DOM веб-части.

```ts
export default class DocumentCardExample extends React.Component<IDocumentCardExampleProps, void> {
  public render(): React.ReactElement<IDocumentCardExampleProps> {
    return (
      <div className={styles.helloWorld}>
        <div className={styles.container}>
          <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
            <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
              <span className="ms-font-xl ms-fontColor-white">Welcome to SharePoint!</span>
              <p className="ms-font-l ms-fontColor-white">Customize SharePoint experiences using Web Parts.</p>
              <p className="ms-font-l ms-fontColor-white">{escape(this.props.description)}</p>
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

### <a name="add-an-office-ui-fabric-component"></a>Добавление компонента Office UI Fabric

Для создания *новых современных элементов интерфейсах* в SharePoint используется Office UI Fabric и Office UI Fabric React как клиентская платформа по умолчанию. Поэтому SharePoint Framework поставляется с версией Office UI Fabric и Office UI Fabric React по умолчанию, которая соответствует версии, доступной в SharePoint. Благодаря этому в создаваемой веб-части используется правильная версия стилей и компонентов Fabric при развертывании в SharePoint. 

Так как при создании решения мы выбрали платформу React, генератор установил также правильную версию Office UI Fabric React. Можно напрямую импортировать компоненты Fabric в компоненты React без дополнительных усилий. 

>**Примечание.** С первым выпуском SharePoint Framework рекомендуем использовать Office UI Fabric и Office UI Fabric React, поставляемые с генератором. Не рекомендуем обновлять пакеты Office UI Fabric и Office UI Fabric React отдельно, так как возможен конфликт с уже имеющейся версией в SharePoint, из-за чего веб-часть может не работать должным образом. Мы исправим эту проблему в последующих выпусках.

Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**. 

Добавьте оператор `import` в верхнюю часть файла, чтобы импортировать нужные компоненты office-ui-fabric-react.

```ts
import {
    DocumentCard,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity,
    IDocumentCardPreviewProps
} from 'office-ui-fabric-react/lib/DocumentCard';
```

Удалите текущий метод `render` и добавьте следующий обновленный метод `render`:

```ts
public render(): JSX.Element {
    const previewProps: IDocumentCardPreviewProps = {
        previewImages: [
        {
            previewImageSrc: String(require('document-preview.png')),
            iconSrc: String(require('icon-ppt.png')),
            width: 318,
            height: 196,
            accentColor: '#ce4b1f'
        }
        ],
    };

    return (
        <DocumentCard onClickHref='http://bing.com'>
        <DocumentCardPreview { ...previewProps } />
        <DocumentCardTitle title='Revenue stream proposal fiscal year 2016 version02.pptx' />
        <DocumentCardActivity
            activity='Created Feb 23, 2016'
            people={
            [
                { name: 'Kat Larrson', profileImageSrc: String(require('avatar-kat.png')) }
            ]
            }
            />
        </DocumentCard>
    );
}
```
Сохраните файл.

В этом коде компонент DocumentCard включает несколько дополнительных разделов:

* DocumentCardPreview;
* DocumentCardTitle;
* DocumentCardActivity.

Свойство `previewProps` включает некоторые свойства DocumentCardPreview.

Обратите внимание на то, что для загрузки изображений для оператора `require` указывается относительный путь. В настоящий момент необходимо использовать подключаемый модуль webpack, назначающий общедоступный путь для оператора, и ввести относительный путь к файлу от исходного файла или папки до папки `lib`. Расположение должно совпадать с текущим расположением рабочего источника.
    
Откройте **DocumentCardExampleWebPart.ts** в папке **src\webparts\documentCardExample**. 
    
Добавьте указанный ниже код в верхнюю часть файла, чтобы указать на необходимость подключаемого модуля webpack, назначающего общедоступный путь для оператора.
    
```ts
require('set-webpack-public-path!');
```
    
Сохраните файл.

### <a name="copy-the-image-assets"></a>Копирование изображений

Скопируйте следующие изображения в папку **src\webparts\documentCardExample**:

* [avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png);
* [icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png);
* [document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png).

### <a name="preview-the-web-part-in-workbench"></a>Просмотр веб-части в рабочей среде

В консоли введите следующий код, чтобы просмотреть свою веб-часть в рабочей среде:
    
```
gulp serve
```
    
На панели элементов выберите веб-часть `DocumentCardExample` для добавления:
    
![Изображение компонента DocumentCard Fabric в рабочей области SharePoint](../../../../images/fabric-components-doc-card-view-ex.png)


## <a name="updating-an-existing-project"></a>Обновление существующего проекта

В файле `package.json` проекта обновите зависимость `@microsoft/sp-build-web` до версии 1.0.1 или выше, удалите каталог `node_modules` проекта и выполните команду `npm install`.
