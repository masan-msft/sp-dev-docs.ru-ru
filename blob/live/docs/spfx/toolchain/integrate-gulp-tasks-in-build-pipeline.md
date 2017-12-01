---
title: "Интеграция задач gulp в цепочку инструментов SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 6dd97e3d939228969c86e0ab7272008b40c3bf31
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="integrate-gulp-tasks-in-sharepoint-framework-toolchain"></a><span data-ttu-id="d9e6f-102">Интеграция задач gulp в цепочку инструментов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="d9e6f-102">Integrate gulp tasks in SharePoint Framework toolchain</span></span>

<span data-ttu-id="d9e6f-103">Средства разработки клиентских приложений для SharePoint позволяют применять [gulp](http://gulpjs.com/) для запуска следующих задач по сборке:</span><span class="sxs-lookup"><span data-stu-id="d9e6f-103">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="d9e6f-104">добавление в пакет и минификация файлов JavaScript и CSS;</span><span class="sxs-lookup"><span data-stu-id="d9e6f-104">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="d9e6f-105">запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;</span><span class="sxs-lookup"><span data-stu-id="d9e6f-105">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="d9e6f-106">компиляция файлов LESS или SASS в CSS;</span><span class="sxs-lookup"><span data-stu-id="d9e6f-106">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="d9e6f-107">компиляция файлов TypeScript в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-107">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="d9e6f-108">Одна из распространенных задач, которую нужно добавить в цепочку инструментов SharePoint Framework, — интеграция специальных задач gulp в конвейер сборки.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-108">One common task you would want to add to the SharePoint Framework toolchain is to integrate your custom gulp tasks in the build pipeline.</span></span>

## <a name="gulp-tasks"></a><span data-ttu-id="d9e6f-109">Задачи gulp</span><span class="sxs-lookup"><span data-stu-id="d9e6f-109">Gulp tasks</span></span>
<span data-ttu-id="d9e6f-110">Обычно задачи gulp определяются в `gulpfile.js` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d9e6f-110">Normally gulp tasks are defined in the `gulpfile.js` as:</span></span>

```js
gulp.task('somename', function() {
  // Do stuff
});
```

<span data-ttu-id="d9e6f-p101">При работе с цепочкой инструментов SharePoint Framework необходимо определить задачи в конвейере сборки платформы. После определения и регистрации в конвейере задача добавляется в цепочку инструментов.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p101">When working with the SharePoint Framework toolchain, it is necessary to define your tasks in the framework's build pipeline. Once defined and registered with the pipeline, the task will be added to the toolchain.</span></span>

<span data-ttu-id="d9e6f-p102">В SharePoint Framework используется [обычная цепочка инструментов сборки](sharepoint-framework-toolchain.md#common-build-tool-packages), которая состоит из набора пакетов npm с общими задачами сборки. Поэтому задачи по умолчанию определяются в обычном пакете, в отличие от ситуации, когда используется `gulpfile.js` клиентского проекта. Чтобы просмотреть доступные задачи, выполните следующую команду в консоли для каталога проекта:</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p102">SharePoint Framework uses a [common build toolchain](sharepoint-framework-toolchain.md#common-build-tool-packages) which consists of a set of npm packages that share common build tasks. And hence, the default tasks are defined in the common package as opposed to your client-side project's `gulpfile.js`. To see the available tasks, you can execute the following command in a console within your project directory:</span></span>

```
gulp --tasks
```

<span data-ttu-id="d9e6f-116">При выполнении этой команды будет выведен список всех доступных задач.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-116">The command above will list all the available tasks.</span></span>

![Доступные задачи gulp](../../images/gulp-tasks-available.png)

## <a name="custom-gulp-tasks"></a><span data-ttu-id="d9e6f-118">Специальные задачи gulp</span><span class="sxs-lookup"><span data-stu-id="d9e6f-118">Custom gulp tasks</span></span>
<span data-ttu-id="d9e6f-p103">Для добавления специальных задач нужно определить их в `gulpfile.js`. Откройте `gulpfile.js` в редакторе кода. Код по умолчанию инициализирует цепочку инструментов SharePoint Framework и глобальный экземпляр `gulp` для этой цепочки. Любые добавляемые специальные задачи необходимо определять до инициализации глобального экземпляра `gulp`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p103">To add your custom tasks, you will define the custom tasks in the `gulpfile.js`. Open the `gulpfile.js` in your code editor. The default code initializes the SharePoint Framework toolchain and the global `gulp` instance for the toolchain. Any custom tasks added should be defined before initializing the global `gulp` instance.</span></span>

### <a name="add-your-custom-task"></a><span data-ttu-id="d9e6f-123">Добавление специальной задачи</span><span class="sxs-lookup"><span data-stu-id="d9e6f-123">Add your custom task</span></span>
<span data-ttu-id="d9e6f-124">Для добавления специальной задачи gulp следует добавить новую подзадачу в конвейер сборки SharePoint Framework с помощью функции [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task).</span><span class="sxs-lookup"><span data-stu-id="d9e6f-124">To add your custom gulp task, you will add a new sub task to the SharePoint Framework build pipeline using the [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task) function:</span></span>

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  this.log('Hello, World!');   
  // use functions from gulp task here  
});
```

<span data-ttu-id="d9e6f-125">Если используется поток, будет возвращен поток.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-125">In the case of a stream, you will return the stream:</span></span>

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  return gulp.src('images/*.png')
             .pipe(gulp.dest('public'));
});
```

### <a name="register-your-task-with-gulp-command-line"></a><span data-ttu-id="d9e6f-126">Регистрация задачи с помощью командной строки gulp</span><span class="sxs-lookup"><span data-stu-id="d9e6f-126">Register your task with gulp command line</span></span>
<span data-ttu-id="d9e6f-127">После определения специальной задачи ее можно зарегистрировать с помощью командной строки gulp, используя функцию `build.task`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-127">Once the custom task is defined, you can then register this custom task with the gulp command line using the `build.task` function:</span></span>

```js
// Register the task with gulp command line
let helloWorldTask = build.task('hello-world', helloWorldSubtask);
```

><span data-ttu-id="d9e6f-128">Примечание. Любые добавляемые специальные задачи необходимо определять до инициализации глобального экземпляра `gulp`, т. е. перед такой строкой кода: `build.initialize(gulp);`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-128">Note: Any custom tasks added should be defined before initializing the global `gulp` instance, that is before the following line of code: `build.initialize(gulp);`</span></span>

<span data-ttu-id="d9e6f-129">Теперь можно выполнить специальную команду в командной строке следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d9e6f-129">Now you can execute your custom command in the command line as follows:</span></span>

```js
gulp hello-world
```

><span data-ttu-id="d9e6f-p104">Примечание. Невозможно выполнить подзадачу, зарегистрированную с помощью функции `build.subTask`, непосредственно в командной строке. Можно выполнить только задачу, зарегистрированную с помощью функции `build.task`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p104">Note: You cannot execute the sub task registered using the `build.subTask` function directly from the command line. You can only execute the task registered using the `build.task` function.</span></span>

### <a name="execute-your-custom-task-before-or-after-available-tasks"></a><span data-ttu-id="d9e6f-132">Выполнение специальной задачи до или после доступных задач</span><span class="sxs-lookup"><span data-stu-id="d9e6f-132">Execute your custom task before or after available tasks</span></span>
<span data-ttu-id="d9e6f-p105">Специальную задачу можно также добавить для выполнения до или после указанных доступных задач gulp. Следующие задачи gulp позволяют вставить специальную задачу до или после другой задачи:</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p105">You can also add this custom task to be executed before or after certain available gulp tasks. The following gulp tasks allow you to inject your custom task before or after task:</span></span>

- <span data-ttu-id="d9e6f-135">общая задача сборки (содержит все доступные задачи);</span><span class="sxs-lookup"><span data-stu-id="d9e6f-135">Generic build task (that consists all the available tasks)</span></span>
- <span data-ttu-id="d9e6f-136">задача TypeScript.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-136">TypeScript task</span></span>

<span data-ttu-id="d9e6f-p106">Задачи SharePoint Framework доступны на платформе сборки по умолчанию. Платформа сборки — это коллекция задач, определенных для конкретной цели. В нашем случае это создание клиентских пакетов. Доступ к платформе по умолчанию, а также к функциям выполнения до и после задачи можно получить с помощью объекта `build.rig`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p106">The SharePoint Framework tasks are available in the default build rig. The build rig is a collection of tasks defined for a specific purpose. In our case, building client-side packages. You can access this default rig using the `build.rig` object and get access to the pre and post task functions:</span></span>
 
```js
//execute before the typescript subtask
build.rig.addPreBuildTask(helloWorldTask);

// execute after TypeScript task
build.rig.addPostTypescriptTask(helloWorldTask);

//execute after all tasks
build.rig.addPostBuildTask(helloWorldTask);
```

## <a name="example-custom-image-resize-task"></a><span data-ttu-id="d9e6f-141">Пример. Специальная задача по изменению размера изображения</span><span class="sxs-lookup"><span data-stu-id="d9e6f-141">Example: Custom image resize task</span></span>
<span data-ttu-id="d9e6f-p107">В качестве примера используем [задачу gulp по изменению размера изображения](https://www.npmjs.com/package/gulp-image-resize).  Это простая задача по изменению размера изображения.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p107">As an example, let's use the [image resize gulp task](https://www.npmjs.com/package/gulp-image-resize).  It's a simple task that allows you to resize images.</span></span>

<span data-ttu-id="d9e6f-144">Готовый образец можно скачать [здесь](https://aka.ms/spfx-extend-gulp-sample).</span><span class="sxs-lookup"><span data-stu-id="d9e6f-144">You can download the completed sample [here](https://aka.ms/spfx-extend-gulp-sample).</span></span>

<span data-ttu-id="d9e6f-145">В [документации к этой специальной задаче по изменению размера изображения](https://www.npmjs.com/package/gulp-image-resize#example) показано, как ее использовать.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-145">In the [image resize task's documentation](https://www.npmjs.com/package/gulp-image-resize#example), it shows how to use this custom task:</span></span>

```js
var gulp = require('gulp');
var imageResize = require('gulp-image-resize');
 
gulp.task('default', function () {
  gulp.src('test.png')
    .pipe(imageResize({
      width : 100,
      height : 100,
      crop : true,
      upscale : false
    }))
    .pipe(gulp.dest('dist'));
});
```

<span data-ttu-id="d9e6f-146">Мы применим эти сведения для добавления данной задачи в проект с помощью функций `build.subTask` и `build.task`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-146">We will use this information to add this task in our project using the `build.subTask` and `build.task` functions:</span></span>

```js
var imageResize = require('gulp-image-resize');

let imageResizeSubTask = build.subTask('image-resize-subtask', function(gulp, buildOptions, done){
    return gulp.src('images/*.jpg')
               .pipe(imageResize({
                   width: 100,
                   height: 100,
                   crop: false                   
               }))
               .pipe(gulp.dest(path.join(buildOptions.libFolder, 'images')))
});

let imageResizeTask = build.task('resize-images', imageResizeSubTask);
```

<span data-ttu-id="d9e6f-p108">Так как мы определяем поток, будет возвращен поток в функции `build.subTask` для конвейера сборки. Затем конвейером сборки будет асинхронно выполнен поток gulp.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-p108">Since we are defining the stream, we return the stream in the `build.subTask` function to the build pipeline. The build pipeline will then asynchronously execute this gulp stream.</span></span> 

<span data-ttu-id="d9e6f-149">После этого можно выполнить задачу в командной строке gulp следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d9e6f-149">Now, you can execute this task from the gulp command line as follows:</span></span>

```js
gulp resize-images
```

![image-resize-task](../../images/gulp-extend-image-resize-task.png)

<span data-ttu-id="d9e6f-151">Эта задача `resize-images` отобразится также в списке доступных задач проекта при выполнении `gulp --tasks`.</span><span class="sxs-lookup"><span data-stu-id="d9e6f-151">You will also see this `resize-images` task in the available tasks for your project when you execute `gulp --tasks`:</span></span>

![image-resize-task with available tasks](../../images/gulp-extend-image-resize-available-tasks.png)




