---
title: "Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint"
ms.date: 12/05/2017
ms.prod: sharepoint
ms.openlocfilehash: c522ec86e6c15886f82661ff9f4edec7427ce40f
ms.sourcegitcommit: 1f752afb40ff133e2fae14337e09392cc5d9d181
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="use-office-ui-fabric-react-components-in-your-sharepoint-client-side-web-part"></a><span data-ttu-id="cec33-102">Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="cec33-102">Use Office UI Fabric React components in your SharePoint client-side web part</span></span>

<span data-ttu-id="cec33-p101">В этой статье описано, как создать простую веб-часть на базе компонента DocumentCard, доступного в [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react). Office UI Fabric React — это клиентская платформа, позволяющая создавать решения для Office и Office 365. Она включает большую коллекцию адаптивных компонентов для мобильных устройств, с помощью которых вы легко сможете создавать веб-части на языке дизайна Office.</span><span class="sxs-lookup"><span data-stu-id="cec33-p101">This article describes how to build a simple web part that uses the DocumentCard component of [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react). Office UI Fabric React is the front-end framework for building experiences for Office and Office 365. Fabric React includes a robust collection of responsive, mobile-first components that make it easy for you to create web experiences using the Office Design Language.</span></span>

<span data-ttu-id="cec33-106">На приведенном ниже изображении показан компонент DocumentCard, созданный с помощью Office UI Fabric React.</span><span class="sxs-lookup"><span data-stu-id="cec33-106">The following image shows a DocumentCard component created with Office UI Fabric React.</span></span>

![Изображение компонента DocumentCard Fabric в рабочей среде SharePoint](../../../images/fabric-components-doc-card-view-ex.png)

<span data-ttu-id="cec33-108">Указанные ниже действия также показаны в видео на [канале SharePoint PnP на YouTube](https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7).</span><span class="sxs-lookup"><span data-stu-id="cec33-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7).</span></span> 

<a href="https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7">
<img src="../../../images/spfx-youtube-tutorial6.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="creating-a-new-web-part-project"></a><span data-ttu-id="cec33-109">Создание проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="cec33-109">Creating a new Web Part project</span></span>

<span data-ttu-id="cec33-110">Создайте каталог проекта в любом расположении:</span><span class="sxs-lookup"><span data-stu-id="cec33-110">Create a new project directory in your favorite location:</span></span>

```
md documentcardexample-webpart
```
    
<span data-ttu-id="cec33-111">Перейдите к каталогу проекта:</span><span class="sxs-lookup"><span data-stu-id="cec33-111">Go to the project directory:</span></span>

```
cd documentcardexample-webpart
```

<span data-ttu-id="cec33-112">Убедитесь, что у вас установлена последняя версия `@microsoft/generator-sharepoint`, и создайте веб-часть, запустив генератор Yeoman для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="cec33-112">Make sure you have the latest version of `@microsoft/generator-sharepoint` installed and create a new web part by running the Yeoman SharePoint generator:</span></span>

```
yo @microsoft/sharepoint
```
    
<span data-ttu-id="cec33-113">Когда появится запрос:</span><span class="sxs-lookup"><span data-stu-id="cec33-113">When prompted:</span></span>

* <span data-ttu-id="cec33-114">Оставьте имя по умолчанию **documentcardexample-webpart** для своего решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="cec33-114">Accept the default **documentcardexample-webpart** as your solution name and choose **Enter**.</span></span>
* <span data-ttu-id="cec33-115">Выберите **Только SharePoint Online (новая версия)** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="cec33-115">Choose **SharePoint Online only (latest)**, and press **Enter**.</span></span>
* <span data-ttu-id="cec33-116">Выберите вариант **Использовать текущую папку** для размещения файлов.</span><span class="sxs-lookup"><span data-stu-id="cec33-116">Select **Use the current folder** for where to place the files.</span></span>
* <span data-ttu-id="cec33-117">Выберите **N**, чтобы сделать установку расширения обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="cec33-117">Choose **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
* <span data-ttu-id="cec33-118">Выберите **WebPart** в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="cec33-118">Choose **WebPart** as the client-side component type to be created.</span></span> 

<span data-ttu-id="cec33-119">Далее потребуется указать определенные сведения о веб-части:</span><span class="sxs-lookup"><span data-stu-id="cec33-119">The next set of prompts will ask for specific information about your web part:</span></span>

* <span data-ttu-id="cec33-120">Укажите **DocumentCardExample** в качестве имени своей веб-части и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="cec33-120">Use **DocumentCardExample** for your web part name and choose **Enter**.</span></span>
* <span data-ttu-id="cec33-121">Оставьте **описание DocumentCardExample** по умолчанию и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="cec33-121">Accept the default **DocumentCardExample description** and choose **Enter**.</span></span>
* <span data-ttu-id="cec33-122">Выберите **React** в качестве платформы и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="cec33-122">Select **React** as the framework and choose **Enter**.</span></span>

<span data-ttu-id="cec33-p102">После этого Yeoman установит необходимые зависимости и применит скаффолдинг к файлам решения. Это может занять несколько минут. Yeoman также включит в проект веб-часть DocumentCardExample, применяя к нему скаффолдинг.</span><span class="sxs-lookup"><span data-stu-id="cec33-p102">At this point, Yeoman will install the required dependencies and scaffold the solution files. This might take a few minutes. Yeoman will scaffold the project to include your DocumentCardExample web part as well.</span></span>

<span data-ttu-id="cec33-126">После скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cec33-126">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="cec33-127">Далее введите следующий код, чтобы открыть проект веб-части в Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="cec33-127">Next, type the following to open the web part project in Visual Studio Code:</span></span>

```
code .
```
    
<span data-ttu-id="cec33-128">Теперь проект веб-части создан с помощью платформы React.</span><span class="sxs-lookup"><span data-stu-id="cec33-128">You now have a web part project with the React framework.</span></span>

<span data-ttu-id="cec33-129">Откройте **DocumentCardExampleWebPart.ts** в папке **src\webparts\documentCardExample**.</span><span class="sxs-lookup"><span data-stu-id="cec33-129">Open **DocumentCardExampleWebPart.ts** from the **src\webparts\documentCardExample** folder.</span></span> 

<span data-ttu-id="cec33-130">Как вы видите, метод `render` создает элемент React и обрабатывает его в элементе DOM веб-части.</span><span class="sxs-lookup"><span data-stu-id="cec33-130">As you can see, the `render` method creates a react element and renders it in the web part DOM.</span></span>

```ts
  public render(): void {
    const element: React.ReactElement<IDocumentCardExampleProps > = React.createElement(
      DocumentCardExample,
      {
        description: this.properties.description
      }
    );
```
    
<span data-ttu-id="cec33-131">Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**.</span><span class="sxs-lookup"><span data-stu-id="cec33-131">Open **DocumentCardExample.tsx** from the **src\webparts\documentCardExample\components** folder.</span></span> 
    
<span data-ttu-id="cec33-132">Это основной компонент React, добавленный генератором Yeoman в ваш проект, который обрабатывается в элементе DOM веб-части.</span><span class="sxs-lookup"><span data-stu-id="cec33-132">This is the main react component that Yeoman added to your project that renders in the web part DOM.</span></span>

```ts
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

### <a name="add-an-office-ui-fabric-component"></a><span data-ttu-id="cec33-133">Добавление компонента Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="cec33-133">Add an Office UI Fabric component</span></span>

<span data-ttu-id="cec33-p103">Для создания *новых современных элементов интерфейсах* в SharePoint используется Office UI Fabric и Office UI Fabric React как клиентская платформа по умолчанию. Поэтому SharePoint Framework поставляется с версией Office UI Fabric и Office UI Fabric React по умолчанию, которая соответствует версии, доступной в SharePoint. Благодаря этому в создаваемой веб-части используется правильная версия стилей и компонентов Fabric при развертывании в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cec33-p103">The *new modern experiences* in SharePoint use Office UI Fabric and Office UI Fabric React as the default front-end framework for building the new experiences. As a result, SharePoint Framework ships with a default version of Office UI Fabric and Fabric React which matches the version available in SharePoint. This ensures the web part you are building uses the right version of the Fabric styles and components when deployed to SharePoint.</span></span> 

<span data-ttu-id="cec33-p104">Так как при создании решения мы выбрали платформу React, генератор установил также правильную версию Office UI Fabric React. Можно напрямую импортировать компоненты Fabric в компоненты React без дополнительных усилий.</span><span class="sxs-lookup"><span data-stu-id="cec33-p104">Since we chose React as our framework when creating the solution, the generator installed the right version of Office UI Fabric React as well. You can directly import the Fabric components in your react components without any additional work.</span></span> 

> [!NOTE]
> <span data-ttu-id="cec33-139">С текущим выпуском SharePoint Framework рекомендуем использовать Office UI Fabric и Office UI Fabric React, поставляемые с генератором.</span><span class="sxs-lookup"><span data-stu-id="cec33-139">With the initial release of the SharePoint Framework, it is recommended to use the Office UI Fabric and Fabric React that ships with the generator.</span></span> <span data-ttu-id="cec33-140">Не рекомендуем обновлять пакеты Office UI Fabric и Office UI Fabric React отдельно, так как возможен конфликт с уже имеющейся версией в SharePoint, из-за чего веб-часть может не работать должным образом.</span><span class="sxs-lookup"><span data-stu-id="cec33-140">It is not recommended to update the Office UI Fabric and Fabric React packages independently as it might conflict with the already available version in SharePoint and as a result your web part may fail to function as expected.</span></span>

<span data-ttu-id="cec33-141">Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**.</span><span class="sxs-lookup"><span data-stu-id="cec33-141">Open **DocumentCardExample.tsx** from the **src\webparts\documentCardExample\components** folder.</span></span> 

<span data-ttu-id="cec33-142">Добавьте оператор `import` в верхнюю часть файла, чтобы импортировать нужные компоненты office-ui-fabric-react.</span><span class="sxs-lookup"><span data-stu-id="cec33-142">Add the following `import` statement to to the top of the file to import fabric react components that we want to use.</span></span>

```ts
import {
    DocumentCard,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity,
    IDocumentCardPreviewProps
} from 'office-ui-fabric-react/lib/DocumentCard';
```

<span data-ttu-id="cec33-143">Удалите текущий метод `render` и добавьте следующий обновленный метод `render`:</span><span class="sxs-lookup"><span data-stu-id="cec33-143">Delete the current `render` method and add the following updated `render` method:</span></span>

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
<span data-ttu-id="cec33-144">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="cec33-144">Save the file.</span></span>

<span data-ttu-id="cec33-145">В этом коде компонент DocumentCard включает несколько дополнительных разделов:</span><span class="sxs-lookup"><span data-stu-id="cec33-145">In this code, the DocumentCard component includes some extra sections:</span></span>

* <span data-ttu-id="cec33-146">DocumentCardPreview;</span><span class="sxs-lookup"><span data-stu-id="cec33-146">DocumentCardPreview</span></span>
* <span data-ttu-id="cec33-147">DocumentCardTitle;</span><span class="sxs-lookup"><span data-stu-id="cec33-147">DocumentCardTitle</span></span>
* <span data-ttu-id="cec33-148">DocumentCardActivity.</span><span class="sxs-lookup"><span data-stu-id="cec33-148">DocumentCardActivity</span></span>

<span data-ttu-id="cec33-149">Свойство `previewProps` включает некоторые свойства DocumentCardPreview.</span><span class="sxs-lookup"><span data-stu-id="cec33-149">The `previewProps` property includes some properties of the DocumentCardPreview.</span></span>

<span data-ttu-id="cec33-p106">Обратите внимание на использование относительного пути с оператором `require` для загрузки изображений. На данный момент нужно выполнить незначительные настройки в файле gulpfile.js, чтобы средство webpack должным образом обрабатывало эти изображения.</span><span class="sxs-lookup"><span data-stu-id="cec33-p106">Notice the use of relative path with a `require` statement to load images. Currently, you need to perform small configuration in the gulpfile.js to enable these images to get processed properly by webpack.</span></span>
    
<span data-ttu-id="cec33-152">Откройте **gulpfile.js** в папке **root**.</span><span class="sxs-lookup"><span data-stu-id="cec33-152">Open **gulpfile.js** from the **root** folder.</span></span> 
    
<span data-ttu-id="cec33-153">Добавьте приведенный ниже код над строкой кода `build.initialize(gulp);`.</span><span class="sxs-lookup"><span data-stu-id="cec33-153">Add the following code just above the `build.initialize(gulp);` code line.</span></span>
    
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
    
<span data-ttu-id="cec33-154">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="cec33-154">Save the file.</span></span>

<span data-ttu-id="cec33-155">Полный код для файла **gulpfile.js** должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cec33-155">Your full **gulpfile.js** file should look as follows.</span></span>

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

### <a name="copy-the-image-assets"></a><span data-ttu-id="cec33-156">Копирование ресурсов изображений</span><span class="sxs-lookup"><span data-stu-id="cec33-156">Copy the image assets</span></span>

<span data-ttu-id="cec33-157">Скопируйте следующие изображения в папку **src\webparts\documentCardExample\components**:</span><span class="sxs-lookup"><span data-stu-id="cec33-157">Copy the following images to your **src\webparts\documentCardExample\components** folder:</span></span>

* <span data-ttu-id="cec33-158">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png);</span><span class="sxs-lookup"><span data-stu-id="cec33-158">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)</span></span>
* <span data-ttu-id="cec33-159">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png);</span><span class="sxs-lookup"><span data-stu-id="cec33-159">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)</span></span>
* <span data-ttu-id="cec33-160">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png).</span><span class="sxs-lookup"><span data-stu-id="cec33-160">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)</span></span>

### <a name="preview-the-web-part-in-workbench"></a><span data-ttu-id="cec33-161">Просмотр веб-части в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="cec33-161">Preview the web part in workbench</span></span>

<span data-ttu-id="cec33-162">В консоли введите следующий код, чтобы просмотреть свою веб-часть в рабочей среде:</span><span class="sxs-lookup"><span data-stu-id="cec33-162">In the console, type the following to preview your web part in workbench:</span></span>
    
```
gulp serve
```
    
<span data-ttu-id="cec33-163">На панели элементов выберите веб-часть `DocumentCardExample` для добавления:</span><span class="sxs-lookup"><span data-stu-id="cec33-163">In the toolbox, select your `DocumentCardExample` web part to add:</span></span>
    
![Изображение компонента DocumentCard Fabric в среде разработки SharePoint](../../../images/fabric-components-doc-card-view-ex.png)

> [!NOTE]
> <span data-ttu-id="cec33-165">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="cec33-165">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="cec33-166">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="cec33-166">Thanks for your input advance.</span></span>