<span data-ttu-id="8a618-p108">Так как мы определяем поток, будет возвращен поток в функции `build.subTask` для конвейера сборки. Затем конвейером сборки будет асинхронно выполнен поток gulp.</span><span class="sxs-lookup"><span data-stu-id="8a618-p108">Since we are defining the stream, we return the stream in the `build.subTask` function to the build pipeline. The build pipeline will then asynchronously execute this gulp stream.</span></span>

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

<span data-ttu-id="8a618-148">После этого можно выполнить задачу в командной строке gulp следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8a618-148">Now, you can execute this task from the gulp command line as follows:</span></span>

```js
gulp resize-images
```

![image-resize-task](../../images/gulp-extend-image-resize-task.png)

<span data-ttu-id="8a618-150">Эта задача `resize-images` отобразится также в списке доступных задач проекта при выполнении `gulp --tasks`.</span><span class="sxs-lookup"><span data-stu-id="8a618-150">You will also see this `resize-images` task in the available tasks for your project when you execute `gulp --tasks`:</span></span>

![image-resize-task with available tasks](../../images/gulp-extend-image-resize-available-tasks.png)




