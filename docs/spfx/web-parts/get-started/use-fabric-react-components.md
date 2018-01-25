---
title: "Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint"
description: "Создайте простую веб-часть на базе компонента DocumentCard, доступного в Office UI Fabric React."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 6dca176399de46565511ba6ae252408f22e515ef
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="use-office-ui-fabric-react-components-in-your-sharepoint-client-side-web-part"></a>Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint

В этой статье описано, как создать простую веб-часть на базе компонента DocumentCard, доступного в [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react). Office UI Fabric React — это клиентская платформа, позволяющая создавать решения для Office и Office 365. Она включает большую коллекцию адаптивных компонентов для мобильных устройств, с помощью которых вы легко сможете создавать веб-части на языке дизайна Office.

На приведенном ниже изображении показан компонент DocumentCard, созданный с помощью Office UI Fabric React.

![Изображение компонента DocumentCard Fabric в SharePoint Workbench](../../../images/fabric-components-doc-card-view-ex.png)

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7). 

<a href="https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7">
<img src="../../../images/spfx-youtube-tutorial6.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a>Создание проекта веб-части

1. Создайте каталог проекта в любом расположении:

  ```
  md documentcardexample-webpart
  ```
    
2. Перейдите к каталогу проекта:

  ```
  cd documentcardexample-webpart
  ```

3. Убедитесь, что у вас установлена последняя версия `@microsoft/generator-sharepoint`, и создайте веб-часть, запустив генератор Yeoman для SharePoint:

  ```
  yo @microsoft/sharepoint
  ```
    
4. Когда появится запрос, сделайте следующее:

  * Оставьте имя по умолчанию (**doc2umentcardexample-webpart**) для своего решения и нажмите клавишу ВВОД.
  * Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу ВВОД.
  * Выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.
  * Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании. 
  * Выберите **WebPart** в качестве типа создаваемого клиентского компонента. 

5. Ниже требуется указать информацию о веб-части:

  * Укажите **DocumentCardExample** в качестве имени своей веб-части и нажмите клавишу ВВОД.
  * Оставьте **описание DocumentCardExample** по умолчанию и нажмите клавишу ВВОД.
  * Выберите **React** в качестве платформы и нажмите клавишу ВВОД.

  После этого Yeoman установит необходимые зависимости и сформирует шаблоны файлов решения. Это может занять несколько минут. Yeoman также включит в проект веб-часть DocumentCardExample, применяя к нему скаффолдинг.

6. После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:

  ```sh
  npm shrinkwrap
  ```

7. Затем введите следующую команду, чтобы открыть проект веб-части в Visual Studio Code:

  ```
  code .
  ```
    
  Теперь проект веб-части создан с помощью платформы React.

8. Откройте **DocumentCardExampleWebPart.ts** в папке **src\webparts\documentCardExample**. 

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
    
9. Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**. 
    
  Это основной компонент React, добавленный генератором Yeoman в ваш проект, который обрабатывается в элементе DOM веб-части.

  ```HTML
  export default class DocumentCardExample extends React.Component<IDocumentCardExampleProps, {}> {
    public render(): React.ReactElement<IDocumentCardExampleProps> {
      return (
        <div className={ styles.documentCardExample }>
          <div className={ styles.container }>
            <div className={ styles.row }>
              <div className={ styles.column }>
                <span className={ styles.title }>Welcome to SharePoint!</span>
                <p className={ styles.subTitle }>Customize SharePoint experiences using Web Parts.</p>
                <p className={ styles.description }>{escape(this.props.description)}</p>
                <a href="https://aka.ms/spfx" className={ styles.button }>
                  <span className={ styles.label }>Learn more</span>
                </a>
              </div>
            </div>
          </div>
        </div>
      );
    }
  }

  ```

## <a name="add-an-office-ui-fabric-component"></a>Добавление компонента Office UI Fabric

Для создания *новых современных элементов интерфейсах* в SharePoint используется Office UI Fabric и Office UI Fabric React как клиентская платформа по умолчанию. Поэтому SharePoint Framework предусматривает наличие версии Office UI Fabric и Office UI Fabric React по умолчанию, которая соответствует версии, доступной в SharePoint. Благодаря этому в создаваемой веб-части используется правильная версия стилей и компонентов Fabric при развертывании в SharePoint. 

Так как при создании решения мы выбрали платформу React, генератор установил также правильную версию Office UI Fabric React. Можно напрямую импортировать компоненты Fabric в компоненты React без дополнительных усилий. 

> [!NOTE]
> С текущим выпуском SharePoint Framework рекомендуем использовать Office UI Fabric и Office UI Fabric React, поставляемые с генератором. Не рекомендуем обновлять пакеты Office UI Fabric и Office UI Fabric React отдельно, так как возможен конфликт с уже имеющейся версией в SharePoint, из-за чего ваша веб-часть может не работать.

### <a name="to-add-an-office-ui-fabric-component"></a>Добавление компонента Office UI Fabric

1. Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**. 

2. Добавьте оператор `import` в верхнюю часть файла, чтобы импортировать нужные компоненты Fabric React.

  ```ts
  import {
    DocumentCard,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity,
    IDocumentCardPreviewProps
  } from 'office-ui-fabric-react/lib/DocumentCard';
  ```

3. Удалите текущий метод `render` и добавьте следующий обновленный метод `render`:

  ```ts
    public render(): JSX.Element {
      const previewProps: IDocumentCardPreviewProps = {
        previewImages: [
          {
            previewImageSrc: String(require('./document-preview.png')),
            iconSrc: String(require('./icon-ppt.png')),
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
                { name: 'Kat Larrson', profileImageSrc: String(require('./avatar-kat.png')) }
              ]
            }
          />
        </DocumentCard>
      );
    }
  ```

4. Сохраните файл.

  В этом коде компонент DocumentCard включает несколько дополнительных разделов:

  * DocumentCardPreview;
  * DocumentCardTitle;
  * DocumentCardActivity.

  Свойство `previewProps` включает некоторые свойства DocumentCardPreview.

5. Обратите внимание на то, что для загрузки изображений для оператора `require` указывается относительный путь. На данный момент нужно выполнить незначительные настройки в файле gulpfile.js, чтобы средство webpack должным образом обрабатывало эти изображения.
    
6. Откройте **gulpfile.js** в папке **root**. 
    
7. Добавьте приведенный ниже код над строкой кода `build.initialize(gulp);`.
    
  ```js
  build.configureWebpack.mergeConfig({  
      additionalConfiguration: (generatedConfiguration) => {
          if (build.getConfig().production) {
              var basePath = build.writeManifests.taskConfig.cdnBasePath;
              if (!basePath.endsWith('/')) {
                  basePath += '/';
              }
              generatedConfiguration.output.publicPath = basePath;
          }
          else {
              generatedConfiguration.output.publicPath = "/dist/";
          }
          return generatedConfiguration;
      }
  });
  ```
    
8. Сохраните файл.

  Полный код для файла **gulpfile.js** должен выглядеть так, как показано ниже.

  ```js
  'use strict';

  const gulp = require('gulp');
  const build = require('@microsoft/sp-build-web');
  build.addSuppression(`Warning - [sass] The local CSS class 'ms-Grid' is not camelCase and will not be type-safe.`);

  build.configureWebpack.mergeConfig({
    additionalConfiguration: (generatedConfiguration) => {
        if (build.getConfig().production) {
            var basePath = build.writeManifests.taskConfig.cdnBasePath;
            if (!basePath.endsWith('/')) {
                basePath += '/';
            }
            generatedConfiguration.output.publicPath = basePath;
        }
        else {
            generatedConfiguration.output.publicPath = "/dist/";
        }
        return generatedConfiguration;
    }
  });

  build.initialize(gulp);

  ```

## <a name="copy-the-image-assets"></a>Копирование ресурсов изображений

Скопируйте следующие изображения в папку **src\webparts\documentCardExample\components**:

* [avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png);
* [icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png);
* [document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png).

## <a name="preview-the-web-part-in-workbench"></a>Просмотр веб-части в Workbench

1. В консоли введите следующий код, чтобы просмотреть свою веб-часть в Workbench:
    
  ```
  gulp serve
  ```
    
2. На панели элементов выберите веб-часть `DocumentCardExample` для добавления:
    
  ![Изображение компонента DocumentCard Fabric в SharePoint Workbench](../../../images/fabric-components-doc-card-view-ex.png)

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!

## <a name="see-also"></a>См. также

- [Создание первой клиентской веб-части SharePoint](build-a-hello-world-web-part.md)