<span data-ttu-id="42538-p108">Обратите внимание на использование относительного пути с оператором `require` для загрузки изображений. На данный момент нужно выполнить незначительные настройки в файле gulpfile.js, чтобы средство webpack должным образом обрабатывало эти изображения.</span><span class="sxs-lookup"><span data-stu-id="42538-p108">Notice the use of relative path with a `require` statement to load images. Currently, you need to perform small configuration in the gulpfile.js to enable these images to get processed properly by webpack.</span></span>

Обратите внимание на использование относительного пути с оператором `require` для загрузки изображений. На данный момент нужно выполнить незначительные настройки в файле gulpfile.js, чтобы средство webpack должным образом обрабатывало эти изображения.
    
<span data-ttu-id="42538-150">Откройте **gulpfile.js** в папке **root**.</span><span class="sxs-lookup"><span data-stu-id="42538-150">Open **gulpfile.js** from the **root** folder.</span></span> 
    
<span data-ttu-id="42538-151">Добавьте приведенный ниже код над строкой кода `build.initialize(gulp);`.</span><span class="sxs-lookup"><span data-stu-id="42538-151">Add the following code just above the `build.initialize(gulp);` code line.</span></span>
    
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
    
<span data-ttu-id="42538-152">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="42538-152">Save the file.</span></span>

<span data-ttu-id="42538-153">Полный код для файла **gulpfile.js** должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="42538-153">Your full **gulpfile.js** file should look as follows.</span></span>

```js
'use strict';

const gulp = require('gulp');
const build = require('@microsoft/sp-build-web');

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

### <a name="copy-the-image-assets"></a><span data-ttu-id="42538-154">Копирование ресурсов изображений</span><span class="sxs-lookup"><span data-stu-id="42538-154">Copy the image assets</span></span>

<span data-ttu-id="42538-155">Скопируйте следующие изображения в папку **src\webparts\documentCardExample\components**:</span><span class="sxs-lookup"><span data-stu-id="42538-155">Copy the following images to your **src\webparts\documentCardExample** folder:</span></span>

* <span data-ttu-id="42538-156">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png);</span><span class="sxs-lookup"><span data-stu-id="42538-156">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)</span></span>
* <span data-ttu-id="42538-157">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png);</span><span class="sxs-lookup"><span data-stu-id="42538-157">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)</span></span>
* <span data-ttu-id="42538-158">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png).</span><span class="sxs-lookup"><span data-stu-id="42538-158">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)</span></span>

### <a name="preview-the-web-part-in-workbench"></a><span data-ttu-id="42538-159">Просмотр веб-части в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="42538-159">Preview the web part in workbench</span></span>

<span data-ttu-id="42538-160">В консоли введите следующий код, чтобы просмотреть свою веб-часть в рабочей среде:</span><span class="sxs-lookup"><span data-stu-id="42538-160">In the console, type the following to preview your web part in workbench:</span></span>
    
```
gulp serve
```
    
<span data-ttu-id="42538-161">На панели элементов выберите веб-часть `DocumentCardExample` для добавления:</span><span class="sxs-lookup"><span data-stu-id="42538-161">In the toolbox, select your `DocumentCardExample` web part to add:</span></span>
    
![Изображение компонента DocumentCard Fabric в рабочей среде SharePoint](../../../../images/fabric-components-doc-card-view-ex.png)
