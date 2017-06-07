# <a name="integrate-gulp-tasks-in-sharepoint-framework-toolchain"></a>Интеграция задач gulp в цепочку инструментов SharePoint Framework

Средства разработки клиентских приложений для SharePoint позволяют применять [gulp](http://gulpjs.com/) для запуска следующих задач по сборке:

* добавление в пакет и минификация файлов JavaScript и CSS;
* запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;
* компиляция файлов LESS или SASS в CSS;
* компиляция файлов TypeScript в JavaScript.

Одна из распространенных задач, которую нужно добавить в цепочку инструментов SharePoint Framework, — интеграция специальных задач gulp в конвейер сборки.

## <a name="gulp-tasks"></a>Задачи gulp
Обычно задачи gulp определяются в `gulpfile.js` следующим образом:

```js
gulp.task('somename', function() {
  // Do stuff
});
```

При работе с цепочкой инструментов SharePoint Framework необходимо определить задачи в конвейере сборки платформы. После определения и регистрации в конвейере задача добавляется в цепочку инструментов.

В SharePoint Framework используется [обычная цепочка инструментов сборки](sharepoint-framework-toolchain.md#common-build-tools-packages), которая состоит из набора пакетов npm с общими задачами сборки. Поэтому задачи по умолчанию определяются в обычном пакете, в отличие от ситуации, когда используется `gulpfile.js` клиентского проекта. Чтобы просмотреть доступные задачи, выполните следующую команду в консоли для каталога проекта:

```
gulp --tasks
```

При выполнении этой команды будет выведен список всех доступных задач.

![Доступные задачи gulp](../../images/gulp-tasks-available.png)

## <a name="custom-gulp-tasks"></a>Специальные задачи gulp
Для добавления специальных задач нужно определить их в `gulpfile.js`. Откройте `gulpfile.js` в редакторе кода. Код по умолчанию инициализирует цепочку инструментов SharePoint Framework и глобальный экземпляр `gulp` для этой цепочки. Любые добавляемые специальные задачи необходимо определять до инициализации глобального экземпляра `gulp`.

### <a name="add-your-custom-task"></a>Добавление специальной задачи
Для добавления специальной задачи gulp следует добавить новую подзадачу в конвейер сборки SharePoint Framework с помощью функции [`build.subTask`](https://github.com/Microsoft/gulp-core-build#defining-a-custom-task).

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  this.log('Hello, World!');   
  // use functions from gulp task here  
});
```

Если используется поток, будет возвращен поток.

```js
let helloWorldSubtask = build.subTask('log-hello-world-subtask', function(gulp, buildOptions, done) {
  return gulp.src('images/*.png')
             .pipe(gulp.dest('public'));
});
```

### <a name="register-your-task-with-gulp-command-line"></a>Регистрация задачи с помощью командной строки gulp
После определения специальной задачи ее можно зарегистрировать с помощью командной строки gulp, используя функцию `build.task`.

```js
// Register the task with gulp command line
let helloWorldTask = build.task('hello-world', helloWorldSubtask);
```

>Примечание. Любые добавляемые специальные задачи необходимо определять до инициализации глобального экземпляра `gulp`, т. е. перед такой строкой кода: `build.initialize(gulp);`.

Теперь можно выполнить специальную команду в командной строке следующим образом:

```js
gulp hello-world
```

>Примечание. Невозможно выполнить подзадачу, зарегистрированную с помощью функции `build.subTask`, непосредственно в командной строке. Можно выполнить только задачу, зарегистрированную с помощью функции `build.task`.

### <a name="execute-your-custom-task-before-or-after-available-tasks"></a>Выполнение специальной задачи до или после доступных задач
Специальную задачу можно также добавить для выполнения до или после указанных доступных задач gulp. Следующие задачи gulp позволяют вставить специальную задачу до или после другой задачи:

- общая задача сборки (содержит все доступные задачи);
- задача TypeScript.

Задачи SharePoint Framework доступны на платформе сборки по умолчанию. Платформа сборки — это коллекция задач, определенных для конкретной цели. В нашем случае это создание клиентских пакетов. Доступ к платформе по умолчанию, а также к функциям выполнения до и после задачи можно получить с помощью объекта `build.rig`.
 
```js
//execute before the typescript subtask
build.rig.addPreBuildTask(helloWorldTask);

// execute after TypeScript task
build.rig.addPostTypescriptTask(helloWorldTask);

//execute after all tasks
build.rig.addPostBuildTask(helloWorldTask);
```

## <a name="example-custom-image-resize-task"></a>Пример. Специальная задача по изменению размера изображения
В качестве примера используем [задачу gulp по изменению размера изображения](https://www.npmjs.com/package/gulp-image-resize).  Это простая задача по изменению размера изображения.

Готовый образец можно скачать [здесь](https://aka.ms/spfx-extend-gulp-sample).

В [документации к этой специальной задаче по изменению размера изображения](https://www.npmjs.com/package/gulp-image-resize#example) показано, как ее использовать.

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

Мы применим эти сведения для добавления данной задачи в проект с помощью функций `build.subTask` и `build.task`.

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

Так как мы определяем поток, будет возвращен поток в функции `build.subTask` для конвейера сборки. Затем конвейером сборки будет асинхронно выполнен поток gulp. 

После этого можно выполнить задачу в командной строке gulp следующим образом:

```js
gulp resize-images
```

![image-resize-task](../../images/gulp-extend-image-resize-task.png)

Эта задача `resize-images` отобразится также в списке доступных задач проекта при выполнении `gulp --tasks`.

![image-resize-task with available tasks](../../images/gulp-extend-image-resize-available-tasks.png)




