<span data-ttu-id="c78e2-p108">Создайте файл `copy-static-assets.json` в каталоге `config`, чтобы система сборки копировала некоторые дополнительные файлы из `src` в `lib`. По умолчанию эта задача сборки копирует файлы с расширениями, которые распознает стандартная конфигурация webpack цепочки инструментов (например, `png` и `json`), поэтому мы просто поручим ей также копировать файлы `md`.</span><span class="sxs-lookup"><span data-stu-id="c78e2-p108">Create a file `copy-static-assets.json` in the `config` directory to tell the build system to copy some additional files from `src` to `lib`. By default, this build task copies files with extensions that the default toolchain webpack configuration understands (like `png` and `json`), so we just need to tell it to also copy `md` files.</span></span> 

Создайте файл `copy-static-assets.json` в каталоге `config`, чтобы система сборки копировала некоторые дополнительные файлы из `src` в `lib`. По умолчанию эта задача сборки копирует файлы с расширениями, которые распознает стандартная конфигурация webpack цепочки инструментов (например, `png` и `json`), поэтому мы просто поручим ей также копировать файлы `md`.

```JSON
{
  "includeExtensions": [
    "md"
  ]
}
```

<span data-ttu-id="c78e2-144">Теперь в операторе `require` вместо относительного пути можно использовать путь к файлу, например:</span><span class="sxs-lookup"><span data-stu-id="c78e2-144">Now instead of using the relative path, you can use the file path in your `require` statement, for example:</span></span>

```TypeScript
const strMarkdownString = require("../../readme.md") as string;
```
 
<span data-ttu-id="c78e2-145">Вы можете ссылаться на эту строку в коде, например:</span><span class="sxs-lookup"><span data-stu-id="c78e2-145">You can then reference this string in your code, for example:</span></span>

``` TypeScript
public render(): void {
  this.domElement.innerHTML = strMarkdownString;
}
```

### <a name="step-4---build-and-test-your-code"></a><span data-ttu-id="c78e2-146">Этап 4. Сборка и тестирование кода</span><span class="sxs-lookup"><span data-stu-id="c78e2-146">Step 4 - Build and test your code</span></span>
<span data-ttu-id="c78e2-147">Чтобы собрать и протестировать код, выполните в консоли следующую команду для корневого каталога проекта:</span><span class="sxs-lookup"><span data-stu-id="c78e2-147">To build and test your code, execute the following command in a console in the root of your project directory:</span></span>

```
gulp serve
```