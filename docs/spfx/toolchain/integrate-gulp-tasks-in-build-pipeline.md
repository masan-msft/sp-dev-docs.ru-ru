---
title: "Интеграция задач gulp в цепочку инструментов SharePoint Framework"
description: "Интеграция настраиваемых задач gulp в конвейере сборки."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 2af62e4c0b06015d47a0dec137344a7a40507649
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="integrate-gulp-tasks-in-sharepoint-framework-toolchain"></a><span data-ttu-id="2d32b-103">Интеграция задач gulp в цепочку инструментов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="2d32b-103">Integrate gulp tasks in SharePoint Framework toolchain</span></span>

<span data-ttu-id="2d32b-104">Средства разработки клиентских приложений для SharePoint позволяют применять [gulp](http://gulpjs.com/) для запуска следующих задач по сборке:</span><span class="sxs-lookup"><span data-stu-id="2d32b-104">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="2d32b-105">добавление в пакет и минификация файлов JavaScript и CSS;</span><span class="sxs-lookup"><span data-stu-id="2d32b-105">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="2d32b-106">запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;</span><span class="sxs-lookup"><span data-stu-id="2d32b-106">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="2d32b-107">компиляция файлов LESS или SASS в CSS;</span><span class="sxs-lookup"><span data-stu-id="2d32b-107">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="2d32b-108">компиляция файлов TypeScript в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2d32b-108">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="2d32b-109">Одна из распространенных задач, которую можно добавить в цепочку инструментов SharePoint Framework, — интеграция специальных задач gulp в конвейер сборки.</span><span class="sxs-lookup"><span data-stu-id="2d32b-109">One common task you would want to add to the SharePoint Framework toolchain is to integrate your custom gulp tasks in the build pipeline.</span></span>

## <a name="gulp-tasks"></a><span data-ttu-id="2d32b-110">Задачи gulp</span><span class="sxs-lookup"><span data-stu-id="2d32b-110">Gulp tasks</span></span>
<span data-ttu-id="2d32b-111">Обычно задачи gulp определяются в `gulpfile.js` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2d32b-111">Normally gulp tasks are defined in the `gulpfile.js` as:</span></span>

```js
gulp.task('somename', function() {
  // Do stuff
});
```

<br/>

<span data-ttu-id="2d32b-112">При работе с цепочкой инструментов SharePoint Framework необходимо определить задачи в конвейере сборки платформы.</span><span class="sxs-lookup"><span data-stu-id="2d32b-112">When working with the SharePoint Framework toolchain, it is necessary to define your tasks in the framework's build pipeline. Once defined and registered with the pipeline, the task will be added to the toolchain.</span></span> <span data-ttu-id="2d32b-113">После определения и регистрации в конвейере задача добавляется в цепочку инструментов.</span><span class="sxs-lookup"><span data-stu-id="2d32b-113">After the task is defined and registered with the pipeline, it is added to the toolchain.</span></span>

<span data-ttu-id="2d32b-114">В SharePoint Framework используется [обычная цепочка инструментов сборки](sharepoint-framework-toolchain.md#common-build-tool-packages), которая состоит из набора пакетов npm с общими задачами сборки.</span><span class="sxs-lookup"><span data-stu-id="2d32b-114">SharePoint Framework uses a [common build toolchain](sharepoint-framework-toolchain.md#common-build-tool-packages) that consists of a set of npm packages that share common build tasks.</span></span> <span data-ttu-id="2d32b-115">Поэтому задачи по умолчанию определяются в обычном пакете, в отличие от ситуации, когда используется `gulpfile.js` клиентского проекта.</span><span class="sxs-lookup"><span data-stu-id="2d32b-115">Hence, the default tasks are defined in the common package as opposed to your client-side project's `gulpfile.js`.</span></span> <span data-ttu-id="2d32b-116">Чтобы просмотреть доступные задачи, выполните следующую команду в консоли для каталога проекта:</span><span class="sxs-lookup"><span data-stu-id="2d32b-116">To see the available tasks, you can execute the following command in a console within your project directory:</span></span>

```js
gulp --tasks
```

<br/>

<span data-ttu-id="2d32b-117">Эта команда перечисляет все доступные задачи.</span><span class="sxs-lookup"><span data-stu-id="2d32b-117">This command lists all the available tasks.</span></span>

![Доступные задачи gulp](../../images/gulp-tasks-available.png)

## <a name="custom-gulp-tasks"></a><span data-ttu-id="2d32b-119">Специальные задачи gulp</span><span class="sxs-lookup"><span data-stu-id="2d32b-119">Custom gulp tasks</span></span>

<span data-ttu-id="2d32b-120">Для добавления специальных задач нужно определить их в `gulpfile.js`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-120">To add your custom tasks, define the custom tasks in the `gulpfile.js`.</span></span> 

<span data-ttu-id="2d32b-121">Откройте `gulpfile.js` в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="2d32b-121">Open the `gulpfile.js` in your code editor.</span></span> <span data-ttu-id="2d32b-122">Код по умолчанию инициализирует цепочку инструментов SharePoint Framework и глобальный экземпляр `gulp` для этой цепочки.</span><span class="sxs-lookup"><span data-stu-id="2d32b-122">The default code initializes the SharePoint Framework toolchain and the global `gulp` instance for the toolchain.</span></span> <span data-ttu-id="2d32b-123">Любые добавляемые специальные задачи необходимо определять до инициализации глобального экземпляра `gulp`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-123">Note: Any custom tasks added should be defined before initializing the global  instance, that is before the following line of code: </span></span>

### <a name="add-your-custom-task"></a><span data-ttu-id="2d32b-124">Добавление специальной задачи</span><span class="sxs-lookup"><span data-stu-id="2d32b-124">Add your custom task</span></span>

<span data-ttu-id="2d32b-125">Для добавления специальной задачи gulp добавьте новую подзадачу в конвейер сборки SharePoint Framework с помощью функции [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task).</span><span class="sxs-lookup"><span data-stu-id="2d32b-125">To add your custom gulp task, you will add a new sub task to the SharePoint Framework build pipeline using the [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task) function:</span></span>

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  this.log('Hello, World!');   
  // use functions from gulp task here  
});
```

<br/>

<span data-ttu-id="2d32b-126">Если используется поток, будет возвращен поток.</span><span class="sxs-lookup"><span data-stu-id="2d32b-126">In the case of a stream, you will return the stream:</span></span>

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  return gulp.src('images/*.png')
             .pipe(gulp.dest('public'));
});
```

### <a name="register-your-task-with-gulp-command-line"></a><span data-ttu-id="2d32b-127">Регистрация задачи с помощью командной строки gulp</span><span class="sxs-lookup"><span data-stu-id="2d32b-127">Register your task with gulp command line</span></span>
<span data-ttu-id="2d32b-128">После определения специальной задачи ее можно зарегистрировать с помощью командной строки gulp, используя функцию `build.task`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-128">Once the custom task is defined, you can then register this custom task with the gulp command line using the `build.task` function:</span></span>

```js
// Register the task with gulp command line
let helloWorldTask = build.task('hello-world', helloWorldSubtask);
```

> [!NOTE] 
> <span data-ttu-id="2d32b-129">Любые добавляемые специальные задачи необходимо определять до инициализации глобального экземпляра `gulp`, т. е. перед такой строкой кода: `build.initialize(gulp);`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-129">Note: Any custom tasks added should be defined before initializing the global `gulp` instance, that is before the following line of code: `build.initialize(gulp);`</span></span>

<br/>

<span data-ttu-id="2d32b-130">Теперь можно выполнить специальную команду в командной строке следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2d32b-130">Now you can execute your custom command in the command line as follows:</span></span>

```js
gulp hello-world
```

> [!NOTE] 
> <span data-ttu-id="2d32b-131">Невозможно выполнить подзадачу, зарегистрированную с помощью функции `build.subTask`, непосредственно в командной строке.</span><span class="sxs-lookup"><span data-stu-id="2d32b-131">You cannot execute the subtask registered by using the `build.subTask` function directly from the command line.</span></span> <span data-ttu-id="2d32b-132">Можно выполнить только задачу, зарегистрированную с помощью функции `build.task`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-132">You can only execute the task registered by using the `build.task` function.</span></span>

### <a name="execute-your-custom-task-before-or-after-available-tasks"></a><span data-ttu-id="2d32b-133">Выполнение специальной задачи до или после доступных задач</span><span class="sxs-lookup"><span data-stu-id="2d32b-133">Execute your custom task before or after available tasks</span></span>
<span data-ttu-id="2d32b-134">Специальную задачу можно также добавить для выполнения до или после указанных доступных задач gulp.</span><span class="sxs-lookup"><span data-stu-id="2d32b-134">You can also add this custom task to be executed before or after certain available gulp tasks. The following gulp tasks allow you to inject your custom task before or after task:</span></span> <span data-ttu-id="2d32b-135">Следующие задачи gulp позволяют вставить специальную задачу до или после такой задачи:</span><span class="sxs-lookup"><span data-stu-id="2d32b-135">You can also add this custom task to be executed before or after certain available gulp tasks. The following gulp tasks allow you to inject your custom task before or after task:</span></span>

- <span data-ttu-id="2d32b-136">общая задача сборки (содержит все доступные задачи);</span><span class="sxs-lookup"><span data-stu-id="2d32b-136">Generic build task (that consists all the available tasks)</span></span>
- <span data-ttu-id="2d32b-137">задача TypeScript.</span><span class="sxs-lookup"><span data-stu-id="2d32b-137">TypeScript task</span></span>

<span data-ttu-id="2d32b-138">Задачи SharePoint Framework доступны на платформе сборки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d32b-138">The SharePoint Framework tasks are available in the default build rig.</span></span> <span data-ttu-id="2d32b-139">Платформа сборки — это коллекция задач, определенных для конкретной цели (в нашем случае это сборка пакетов на стороне клиента).</span><span class="sxs-lookup"><span data-stu-id="2d32b-139">The build rig is a collection of tasks defined for a specific purpose, in our case, building client-side packages.</span></span> <span data-ttu-id="2d32b-140">Доступ к платформе по умолчанию, а также к функциям выполнения до и после задачи можно получить с помощью объекта `build.rig`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-140">You can access this default rig by using the `build.rig` object and then get access to the pre- and post-task functions:</span></span>
 
```js
// execute before the TypeScript subtask
build.rig.addPreBuildTask(helloWorldTask);

// execute after TypeScript subtask
build.rig.addPostTypescriptTask(helloWorldTask);

// execute after all tasks
build.rig.addPostBuildTask(helloWorldTask);
```

## <a name="example-custom-image-resize-task"></a><span data-ttu-id="2d32b-141">Пример. Специальная задача по изменению размера изображения</span><span class="sxs-lookup"><span data-stu-id="2d32b-141">Example: Custom image resize task</span></span>

<span data-ttu-id="2d32b-p107">В качестве примера используем [задачу gulp по изменению размера изображения](https://www.npmjs.com/package/gulp-image-resize).  Это простая задача по изменению размера изображения.</span><span class="sxs-lookup"><span data-stu-id="2d32b-p107">As an example, let's use the [image resize gulp task](https://www.npmjs.com/package/gulp-image-resize).  It's a simple task that allows you to resize images.</span></span>

<span data-ttu-id="2d32b-144">Вы можете скачать готовый образец по ссылке [samples/js-extend-gulp/](https://aka.ms/spfx-extend-gulp-sample).</span><span class="sxs-lookup"><span data-stu-id="2d32b-144">You can download the completed sample [here](https://aka.ms/spfx-extend-gulp-sample).</span></span>

<span data-ttu-id="2d32b-145">В [документации к этой специальной задаче по изменению размера изображения](https://www.npmjs.com/package/gulp-image-resize#example) показано, как ее использовать.</span><span class="sxs-lookup"><span data-stu-id="2d32b-145">In the [image resize task's documentation](https://www.npmjs.com/package/gulp-image-resize#example), it shows how to use this custom task:</span></span>

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

<br/>

<span data-ttu-id="2d32b-146">Мы используем эти сведения для добавления данной задачи в проект с помощью функций `build.subTask` и `build.task`:</span><span class="sxs-lookup"><span data-stu-id="2d32b-146">We will use this information to add this task in our project using the `build.subTask` and `build.task` functions:</span></span>

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

<br/>

<span data-ttu-id="2d32b-p108">Так как мы определяем поток, будет возвращен поток в функции `build.subTask` для конвейера сборки. Затем конвейер сборки асинхронно выполняет этот поток gulp.</span><span class="sxs-lookup"><span data-stu-id="2d32b-p108">Since we are defining the stream, we return the stream in the `build.subTask` function to the build pipeline. The build pipeline will then asynchronously execute this gulp stream.</span></span> 

<span data-ttu-id="2d32b-149">После этого можно выполнить задачу в командной строке gulp следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2d32b-149">Now, you can execute this task from the gulp command line as follows:</span></span>

```js
gulp resize-images
```

<br/>

![image-resize-task](../../images/gulp-extend-image-resize-task.png)

<br/>

<span data-ttu-id="2d32b-151">Эта задача `resize-images` отображается также в списке доступных задач проекта при выполнении `gulp --tasks`.</span><span class="sxs-lookup"><span data-stu-id="2d32b-151">You will also see this `resize-images` task in the available tasks for your project when you execute `gulp --tasks`:</span></span>

![image-resize-task with available tasks](../../images/gulp-extend-image-resize-available-tasks.png)

## <a name="see-also"></a><span data-ttu-id="2d32b-153">См. также</span><span class="sxs-lookup"><span data-stu-id="2d32b-153">See also</span></span>

- [<span data-ttu-id="2d32b-154">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="2d32b-154">SharePoint Framework Overview</span></span>](../sharepoint-framework-overview.md)




