---
title: "Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint"
description: "Создайте простую веб-часть на базе компонента DocumentCard, доступного в Office UI Fabric React."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: b36054c7d0cfebbf306fe63f40c982c9fefa7a24
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="use-office-ui-fabric-react-components-in-your-sharepoint-client-side-web-part"></a><span data-ttu-id="d8085-103">Использование компонентов Office UI Fabric React в клиентской веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8085-103">Use Office UI Fabric React components in your SharePoint client-side web part</span></span>

<span data-ttu-id="d8085-104">В этой статье описано, как создать простую веб-часть на базе компонента DocumentCard, доступного в [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react).</span><span class="sxs-lookup"><span data-stu-id="d8085-104">This article describes how to build a simple web part that uses the DocumentCard component of [Office UI Fabric React](https://github.com/OfficeDev/office-ui-fabric-react).</span></span> <span data-ttu-id="d8085-105">Office UI Fabric React — это клиентская платформа, позволяющая создавать решения для Office и Office 365.</span><span class="sxs-lookup"><span data-stu-id="d8085-105">Office UI Fabric React is the front-end framework for building experiences for Office and Office 365.</span></span> <span data-ttu-id="d8085-106">Она включает большую коллекцию адаптивных компонентов для мобильных устройств, с помощью которых вы легко сможете создавать веб-части на языке дизайна Office.</span><span class="sxs-lookup"><span data-stu-id="d8085-106">Fabric React includes a robust collection of responsive, mobile-first components that make it easy for you to create web experiences by using the Office Design Language.</span></span>

<span data-ttu-id="d8085-107">На приведенном ниже изображении показан компонент DocumentCard, созданный с помощью Office UI Fabric React.</span><span class="sxs-lookup"><span data-stu-id="d8085-107">The following image shows a DocumentCard component created with Office UI Fabric React.</span></span>

![Изображение компонента DocumentCard Fabric в SharePoint Workbench](../../../images/fabric-components-doc-card-view-ex.png)

<span data-ttu-id="d8085-109">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7).</span><span class="sxs-lookup"><span data-stu-id="d8085-109">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7).</span></span> 

<a href="https://www.youtube.com/watch?v=1YRu4-nZot4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=7">
<img src="../../../images/spfx-youtube-tutorial6.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="create-a-new-web-part-project"></a><span data-ttu-id="d8085-110">Создание проекта веб-части</span><span class="sxs-lookup"><span data-stu-id="d8085-110">Create a new web part project</span></span>

1. <span data-ttu-id="d8085-111">Создайте каталог проекта в любом расположении:</span><span class="sxs-lookup"><span data-stu-id="d8085-111">Create a new project directory in your favorite location:</span></span>

  ```
  md documentcardexample-webpart
  ```
    
2. <span data-ttu-id="d8085-112">Перейдите к каталогу проекта:</span><span class="sxs-lookup"><span data-stu-id="d8085-112">Go to the project directory:</span></span>

  ```
  cd documentcardexample-webpart
  ```

3. <span data-ttu-id="d8085-113">Убедитесь, что у вас установлена последняя версия `@microsoft/generator-sharepoint`, и создайте веб-часть, запустив генератор Yeoman для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="d8085-113">Make sure you have the latest version of `@microsoft/generator-sharepoint` installed and create a new web part by running the Yeoman SharePoint generator:</span></span>

  ```
  yo @microsoft/sharepoint
  ```
    
4. <span data-ttu-id="d8085-114">Когда появится запрос:</span><span class="sxs-lookup"><span data-stu-id="d8085-114">When prompted:</span></span>

  * <span data-ttu-id="d8085-115">Оставьте имя по умолчанию (**documentcardexample-webpart**) для своего решения и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d8085-115">Accept the default **documentcardexample-webpart** as your solution name and choose **Enter**.</span></span>
  * <span data-ttu-id="d8085-116">Выберите **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d8085-116">Select SharePoint Online only (latest), and select Enter.</span></span>
  * <span data-ttu-id="d8085-117">Выберите вариант **Use the current folder** (Использовать текущую папку) для размещения файлов.</span><span class="sxs-lookup"><span data-stu-id="d8085-117">Select **Use the current folder** for where to place the files.</span></span>
  * <span data-ttu-id="d8085-118">Выберите **N**, чтобы сделать установку расширения, выполняемую напрямую, обязательной на каждом сайте при его использовании.</span><span class="sxs-lookup"><span data-stu-id="d8085-118">Select **N** to require the extension to be installed on each site explicitly when it's being used.</span></span> 
  * <span data-ttu-id="d8085-119">Выберите **WebPart** в качестве типа создаваемого клиентского компонента.</span><span class="sxs-lookup"><span data-stu-id="d8085-119">Select **Extension** as the client-side component type to be created.</span></span> 

5. <span data-ttu-id="d8085-120">Далее вам потребуется указать определенные сведения о веб-части:</span><span class="sxs-lookup"><span data-stu-id="d8085-120">The next set of prompts will ask for specific information about your web part:</span></span>

  * <span data-ttu-id="d8085-121">Укажите **DocumentCardExample** в качестве имени своей веб-части и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d8085-121">Use **DocumentCardExample** for your web part name and choose **Enter**.</span></span>
  * <span data-ttu-id="d8085-122">Оставьте **описание DocumentCardExample** по умолчанию и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d8085-122">Accept the default **DocumentCardExample description** and choose **Enter**.</span></span>
  * <span data-ttu-id="d8085-123">Выберите **React** в качестве платформы и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d8085-123">Select **React** as the framework and choose **Enter**.</span></span>

  <span data-ttu-id="d8085-124">После этого Yeoman установит необходимые зависимости и сформирует шаблоны файлов решения.</span><span class="sxs-lookup"><span data-stu-id="d8085-124">At this point, Yeoman installs the required dependencies and scaffolds the solution files along with the HelloWorld extension.</span></span> <span data-ttu-id="d8085-125">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d8085-125">This might take a few minutes.</span></span> <span data-ttu-id="d8085-126">Yeoman также включит в проект веб-часть DocumentCardExample, применяя к нему скаффолдинг.</span><span class="sxs-lookup"><span data-stu-id="d8085-126">Yeoman scaffolds the project to include your DocumentCardExample web part as well.</span></span>

6. <span data-ttu-id="d8085-127">После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d8085-127">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

7. <span data-ttu-id="d8085-128">Затем введите следующую команду, чтобы открыть проект веб-части в Visual Studio Code:</span><span class="sxs-lookup"><span data-stu-id="d8085-128">Next, type the following to open the web part project in Visual Studio Code:</span></span>

  ```
  code .
  ```
    
  <span data-ttu-id="d8085-129">Теперь проект веб-части создан с помощью платформы React.</span><span class="sxs-lookup"><span data-stu-id="d8085-129">You now have a web part project with the React framework.</span></span>

8. <span data-ttu-id="d8085-130">Откройте **DocumentCardExampleWebPart.ts** в папке **src\webparts\documentCardExample**.</span><span class="sxs-lookup"><span data-stu-id="d8085-130">Open **DocumentCardExampleWebPart.ts** from the **src\webparts\documentCardExample** folder.</span></span> 

  <span data-ttu-id="d8085-131">Как вы видите, метод `render` создает элемент React и обрабатывает его в элементе DOM веб-части.</span><span class="sxs-lookup"><span data-stu-id="d8085-131">As you can see, the `render` method creates a react element and renders it in the web part DOM.</span></span>

  ```ts
    public render(): void {
      const element: React.ReactElement<IDocumentCardExampleProps > = React.createElement(
        DocumentCardExample,
        {
          description: this.properties.description
        }
      );
  ```
    
9. <span data-ttu-id="d8085-132">Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**.</span><span class="sxs-lookup"><span data-stu-id="d8085-132">Open **DocumentCardExample.tsx** from the **src\webparts\documentCardExample\components** folder.</span></span> 
    
  <span data-ttu-id="d8085-133">Это основной компонент React, добавленный генератором Yeoman в ваш проект, который обрабатывается в элементе DOM веб-части.</span><span class="sxs-lookup"><span data-stu-id="d8085-133">This is the main react component that Yeoman added to your project that renders in the web part DOM.</span></span>

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

## <a name="add-an-office-ui-fabric-component"></a><span data-ttu-id="d8085-134">Добавление компонента Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="d8085-134">Add an Office UI Fabric component</span></span>

<span data-ttu-id="d8085-135">Для создания *новых современных элементов интерфейсах* в SharePoint используется Office UI Fabric и Office UI Fabric React как клиентская платформа по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d8085-135">The *new modern experiences* in SharePoint use Office UI Fabric and Office UI Fabric React as the default front-end framework for building the new experiences.</span></span> <span data-ttu-id="d8085-136">Поэтому SharePoint Framework предусматривает наличие версии Office UI Fabric и Office UI Fabric React по умолчанию, которая соответствует версии, доступной в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d8085-136">As a result, SharePoint Framework ships with a default version of Office UI Fabric and Fabric React that matches the version available in SharePoint.</span></span> <span data-ttu-id="d8085-137">Благодаря этому в создаваемой веб-части используется правильная версия стилей и компонентов Fabric при развертывании в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d8085-137">This ensures that the web part you are building uses the right version of the Fabric styles and components when deployed to SharePoint.</span></span> 

<span data-ttu-id="d8085-138">Так как при создании решения мы выбрали платформу React, генератор установил также правильную версию Office UI Fabric React.</span><span class="sxs-lookup"><span data-stu-id="d8085-138">Since we chose React as our framework when creating the solution, the generator installed the right version of Office UI Fabric React as well. You can directly import the Fabric components in your react components without any additional work.</span></span> <span data-ttu-id="d8085-139">Можно напрямую импортировать компоненты Fabric в компоненты React без дополнительных усилий.</span><span class="sxs-lookup"><span data-stu-id="d8085-139">You can directly import the Fabric components in your react components without any additional work.</span></span> 

> [!NOTE]
> <span data-ttu-id="d8085-140">С текущим выпуском SharePoint Framework рекомендуем использовать Office UI Fabric и Office UI Fabric React, поставляемые с генератором.</span><span class="sxs-lookup"><span data-stu-id="d8085-140">With the current release of the SharePoint Framework, it is recommended to use the Office UI Fabric and Fabric React that ships with the generator.</span></span> <span data-ttu-id="d8085-141">Не рекомендуем обновлять пакеты Office UI Fabric и Office UI Fabric React отдельно, так как возможен конфликт с уже имеющейся версией в SharePoint, из-за чего ваша веб-часть может не работать.</span><span class="sxs-lookup"><span data-stu-id="d8085-141">It is not recommended to update the Office UI Fabric and Fabric React packages independently as it might conflict with the already available version in SharePoint and as a result your web part may fail to function as expected.</span></span>

### <a name="to-add-an-office-ui-fabric-component"></a><span data-ttu-id="d8085-142">Добавление компонента Office UI Fabric</span><span class="sxs-lookup"><span data-stu-id="d8085-142">Add an Office UI Fabric component</span></span>

1. <span data-ttu-id="d8085-143">Откройте **DocumentCardExample.tsx** в папке **src\webparts\documentCardExample\components**.</span><span class="sxs-lookup"><span data-stu-id="d8085-143">Open **DocumentCardExample.tsx** from the **src\webparts\documentCardExample\components** folder.</span></span> 

2. <span data-ttu-id="d8085-144">Добавьте оператор `import` в верхнюю часть файла, чтобы импортировать нужные компоненты Fabric React.</span><span class="sxs-lookup"><span data-stu-id="d8085-144">Add the following `import` statement to to the top of the file to import fabric react components that we want to use.</span></span>

  ```ts
  import {
    DocumentCard,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity,
    IDocumentCardPreviewProps
  } from 'office-ui-fabric-react/lib/DocumentCard';
  ```

3. <span data-ttu-id="d8085-145">Удалите текущий метод `render` и добавьте следующий обновленный метод `render`:</span><span class="sxs-lookup"><span data-stu-id="d8085-145">Delete the current `render` method and add the following updated `render` method:</span></span>

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

4. <span data-ttu-id="d8085-146">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="d8085-146">Save the file.</span></span>

  <span data-ttu-id="d8085-147">В этом коде компонент DocumentCard включает несколько дополнительных разделов:</span><span class="sxs-lookup"><span data-stu-id="d8085-147">In this code, the DocumentCard component includes some extra sections:</span></span>

  * <span data-ttu-id="d8085-148">DocumentCardPreview;</span><span class="sxs-lookup"><span data-stu-id="d8085-148">DocumentCardPreview</span></span>
  * <span data-ttu-id="d8085-149">DocumentCardTitle;</span><span class="sxs-lookup"><span data-stu-id="d8085-149">DocumentCardTitle</span></span>
  * <span data-ttu-id="d8085-150">DocumentCardActivity.</span><span class="sxs-lookup"><span data-stu-id="d8085-150">DocumentCardActivity</span></span>

  <span data-ttu-id="d8085-151">Свойство `previewProps` включает некоторые свойства DocumentCardPreview.</span><span class="sxs-lookup"><span data-stu-id="d8085-151">The `previewProps` property includes some properties of the DocumentCardPreview.</span></span>

5. <span data-ttu-id="d8085-152">Обратите внимание на то, что для загрузки изображений для оператора `require` указывается относительный путь.</span><span class="sxs-lookup"><span data-stu-id="d8085-152">Notice the use of the relative path with a `require` statement to load images.</span></span> <span data-ttu-id="d8085-153">На данный момент нужно выполнить незначительные настройки в файле gulpfile.js, чтобы средство webpack должным образом обрабатывало эти изображения.</span><span class="sxs-lookup"><span data-stu-id="d8085-153">Notice the use of relative path with a  statement to load images. Currently, you need to perform small configuration in the gulpfile.js to enable these images to get processed properly by webpack.</span></span>
    
6. <span data-ttu-id="d8085-154">Откройте **gulpfile.js** в папке **root**.</span><span class="sxs-lookup"><span data-stu-id="d8085-154">Open **gulpfile.js** from the **root** folder.</span></span> 
    
7. <span data-ttu-id="d8085-155">Добавьте приведенный ниже код над строкой кода `build.initialize(gulp);`.</span><span class="sxs-lookup"><span data-stu-id="d8085-155">Add the following code just above the `build.initialize(gulp);` code line.</span></span>
    
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
    
8. <span data-ttu-id="d8085-156">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="d8085-156">Save the file.</span></span>

  <span data-ttu-id="d8085-157">Полный код для файла **gulpfile.js** должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d8085-157">Your full **gulpfile.js** file should look as follows.</span></span>

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

## <a name="copy-the-image-assets"></a><span data-ttu-id="d8085-158">Копирование ресурсов изображений</span><span class="sxs-lookup"><span data-stu-id="d8085-158">Copy the image assets</span></span>

<span data-ttu-id="d8085-159">Скопируйте следующие изображения в папку **src\webparts\documentCardExample\components**:</span><span class="sxs-lookup"><span data-stu-id="d8085-159">Copy the following images to your **src\webparts\documentCardExample\components** folder:</span></span>

* <span data-ttu-id="d8085-160">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png);</span><span class="sxs-lookup"><span data-stu-id="d8085-160">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)</span></span>
* <span data-ttu-id="d8085-161">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png);</span><span class="sxs-lookup"><span data-stu-id="d8085-161">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)</span></span>
* <span data-ttu-id="d8085-162">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png).</span><span class="sxs-lookup"><span data-stu-id="d8085-162">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)</span></span>

## <a name="preview-the-web-part-in-workbench"></a><span data-ttu-id="d8085-163">Просмотр веб-части в Workbench</span><span class="sxs-lookup"><span data-stu-id="d8085-163">Preview the web part in workbench</span></span>

1. <span data-ttu-id="d8085-164">В консоли введите следующий код, чтобы просмотреть свою веб-часть в Workbench:</span><span class="sxs-lookup"><span data-stu-id="d8085-164">In the console, type the following to preview your web part in workbench:</span></span>
    
  ```
  gulp serve
  ```
    
2. <span data-ttu-id="d8085-165">На панели элементов выберите веб-часть `DocumentCardExample` для добавления:</span><span class="sxs-lookup"><span data-stu-id="d8085-165">In the toolbox, select your `DocumentCardExample` web part to add:</span></span>
    
  ![Изображение компонента DocumentCard Fabric в SharePoint Workbench](../../../images/fabric-components-doc-card-view-ex.png)

> [!NOTE]
> <span data-ttu-id="d8085-167">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="d8085-167">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="d8085-168">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="d8085-168">Thanks for your input advance.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8085-169">См. также</span><span class="sxs-lookup"><span data-stu-id="d8085-169">See also</span></span>

- [<span data-ttu-id="d8085-170">Создание первой клиентской веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8085-170">Build your first SharePoint client-side web part</span></span>](build-a-hello-world-web-part.md)