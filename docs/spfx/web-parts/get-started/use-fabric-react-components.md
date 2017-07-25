<span data-ttu-id="fa849-p108">Обратите внимание на то, что для загрузки изображений для оператора `require` указывается относительный путь. В настоящий момент необходимо использовать подключаемый модуль webpack, назначающий общедоступный путь для оператора, и ввести относительный путь к файлу от исходного файла или папки до папки `lib`. Расположение должно совпадать с текущим расположением рабочего источника.</span><span class="sxs-lookup"><span data-stu-id="fa849-p108">Notice the use of relative path with a `require` statement to load images. Currently, you need to use the webpack public path plugin and input the file's relative path from your source file or folder to the `lib` folder. This should be the same as your current working source location.</span></span>

Обратите внимание на то, что для загрузки изображений для оператора `require` указывается относительный путь. В настоящий момент необходимо использовать подключаемый модуль webpack, назначающий общедоступный путь для оператора, и ввести относительный путь к файлу от исходного файла или папки до папки `lib`. Расположение должно совпадать с текущим расположением рабочего источника.
    
<span data-ttu-id="fa849-152">Откройте **DocumentCardExampleWebPart.ts** в папке **src\webparts\documentCardExample**.</span><span class="sxs-lookup"><span data-stu-id="fa849-152">Open **DocumentCardExampleWebPart.ts** from the **src\webparts\documentCardExample** folder.</span></span> 
    
<span data-ttu-id="fa849-153">Добавьте указанный ниже код в верхнюю часть файла, чтобы указать на необходимость подключаемого модуля webpack, назначающего общедоступный путь для оператора.</span><span class="sxs-lookup"><span data-stu-id="fa849-153">Add the following code at the top of the file to require the webpack public path plugin.</span></span>
    
```ts
require('set-webpack-public-path!');
```
    
<span data-ttu-id="fa849-154">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="fa849-154">Save the file.</span></span>

### <a name="copy-the-image-assets"></a><span data-ttu-id="fa849-155">Копирование изображений</span><span class="sxs-lookup"><span data-stu-id="fa849-155">Copy the image assets</span></span>

<span data-ttu-id="fa849-156">Скопируйте следующие изображения в папку **src\webparts\documentCardExample**:</span><span class="sxs-lookup"><span data-stu-id="fa849-156">Copy the following images to your **src\webparts\documentCardExample** folder:</span></span>

* <span data-ttu-id="fa849-157">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png);</span><span class="sxs-lookup"><span data-stu-id="fa849-157">[avatar-kat.png](https://github.com/SharePoint/sp-dev-docs/blob/master/assets/avatar-kat.png)</span></span>
* <span data-ttu-id="fa849-158">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png);</span><span class="sxs-lookup"><span data-stu-id="fa849-158">[icon-ppt.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/icon-ppt.png)</span></span>
* <span data-ttu-id="fa849-159">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png).</span><span class="sxs-lookup"><span data-stu-id="fa849-159">[document-preview.png](https://github.com/SharePoint/sp-dev-docs/tree/master/assets/document-preview.png)</span></span>

### <a name="preview-the-web-part-in-workbench"></a><span data-ttu-id="fa849-160">Просмотр веб-части в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="fa849-160">Preview the web part in workbench</span></span>

<span data-ttu-id="fa849-161">В консоли введите следующий код, чтобы просмотреть свою веб-часть в рабочей среде:</span><span class="sxs-lookup"><span data-stu-id="fa849-161">In the console, type the following to preview your web part in workbench:</span></span>
    
```
gulp serve
```
    
<span data-ttu-id="fa849-162">На панели элементов выберите веб-часть `DocumentCardExample` для добавления:</span><span class="sxs-lookup"><span data-stu-id="fa849-162">In the toolbox, select your `DocumentCardExample` web part to add:</span></span>
    
![Изображение компонента DocumentCard Fabric в рабочей области SharePoint](../../../../images/fabric-components-doc-card-view-ex.png)


## <a name="updating-an-existing-project"></a><span data-ttu-id="fa849-164">Обновление существующего проекта</span><span class="sxs-lookup"><span data-stu-id="fa849-164">Updating an existing project</span></span>

<span data-ttu-id="fa849-165">В файле `package.json` проекта обновите зависимость `@microsoft/sp-build-web` до версии 1.0.1 или выше, удалите каталог `node_modules` проекта и выполните команду `npm install`.</span><span class="sxs-lookup"><span data-stu-id="fa849-165">In your project's `package.json`, update the `@microsoft/sp-build-web` dependency to at least version 1.0.1, delete your project's `node_modules` directory, and run `npm install`.</span></span>
