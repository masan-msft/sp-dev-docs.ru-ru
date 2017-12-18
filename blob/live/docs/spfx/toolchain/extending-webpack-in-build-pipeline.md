---
title: "Расширение конфигурации Webpack в цепочке инструментов SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c5156ce434a791658de3798ff0d7de2e73c42fb2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="extending-webpack-in-the-sharepoint-framework-toolchain"></a><span data-ttu-id="31969-102">Расширение конфигурации Webpack в цепочке инструментов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="31969-102">Extending webpack in the SharePoint Framework toolchain</span></span>

<span data-ttu-id="31969-103">[Webpack](https://Webpack.js.org/) — это средство увязки модулей JavaScript в пакеты. На основе выбранных вами файлов JavaScript и их зависимостей это средство создает один или несколько файлов JavaScript, чтобы можно было загружать различные части кода для различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="31969-103">[Webpack](https://Webpack.js.org/) is a JavaScript module bundler that takes your JavaScript files and its dependencies and generates one or more JavaScript bundles so you can load different bundles for different scenarios.</span></span>

<span data-ttu-id="31969-104">Для увязки файлов в пакеты цепочка инструментов платформы использует CommonJS.</span><span class="sxs-lookup"><span data-stu-id="31969-104">The framework toolchain uses CommonJS for bundling.</span></span> <span data-ttu-id="31969-105">Это позволяет определять модули и указывать, где вы хотите использовать их.</span><span class="sxs-lookup"><span data-stu-id="31969-105">This enables you to define modules and where you want to use them.</span></span> <span data-ttu-id="31969-106">Кроме того, цепочка инструментов использует SystemJS (универсальный загрузчик модулей) для загрузки ваших модулей.</span><span class="sxs-lookup"><span data-stu-id="31969-106">The toolchain also uses SystemJS, a universal module loader, to load your modules.</span></span> <span data-ttu-id="31969-107">Благодаря этому можно задавать области для веб-частей и гарантировать, что каждая веб-часть будет выполняться в ее собственном пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="31969-107">This helps you to scope your web parts by making sure that each web part is executed in its own namespace.</span></span>

<span data-ttu-id="31969-108">Одна из стандартных задач, которую вам, возможно, потребуется добавить в цепочку инструментов SharePoint Framework, — расширение конфигурации Webpack с использованием пользовательских загрузчиков и подключаемых модулей.</span><span class="sxs-lookup"><span data-stu-id="31969-108">One common task you would want to add to the SharePoint Framework toolchain is to extend the webpack configuration with custom loaders and plugins.</span></span>

## <a name="using-webpack-loaders"></a><span data-ttu-id="31969-109">Использование загрузчиков Webpack</span><span class="sxs-lookup"><span data-stu-id="31969-109">Using webpack loaders</span></span>
<span data-ttu-id="31969-110">Во время разработки часто требуется импортировать и использовать ресурсы, не относящиеся к JavaScript, например изображения или шаблоны.</span><span class="sxs-lookup"><span data-stu-id="31969-110">There are many cases where one would like to import and utilize a non-JavaScript resource during development, typically this is done with images or templates.</span></span> <span data-ttu-id="31969-111">[Загрузчик Webpack](https://webpack.js.org/loaders/) преобразовывает ресурс так, что его сможет использовать ваше приложение JavaScript, либо предоставляет простую ссылку, понятную для приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="31969-111">A [Webpack loader](https://webpack.js.org/loaders/) will convert the resource into something that can be utilized by your JavaScript application or provide a simple reference that your JavaScript application can understand.</span></span> <span data-ttu-id="31969-112">Например, шаблон Markdown можно скомпилировать и преобразовать в текстовую строку, а ресурс изображения можно преобразовать во встроенное изображение в кодировке Base64. Кроме того, можно создать ссылку на ресурс изображения в виде URL-адреса и скопировать его в каталог `dist` для развертывания.</span><span class="sxs-lookup"><span data-stu-id="31969-112">For example, a Markdown template may be compiled and converted to a text string, while a image resource may be converted to an inlined Base64 image, or it may be referenced as a URL and copied to your `dist` directory for deployment.</span></span>

<span data-ttu-id="31969-113">Существует целый ряд полезных загрузчиков. Некоторые из них уже используются в стандартной конфигурации Webpack в SharePoint Framework, например следующие:</span><span class="sxs-lookup"><span data-stu-id="31969-113">There are a number of useful loaders, several of which are already used by the standard SharePoint Framework webpack configuration, such as:</span></span>

- <span data-ttu-id="31969-114">html-loader;</span><span class="sxs-lookup"><span data-stu-id="31969-114">html-loader</span></span>
- <span data-ttu-id="31969-115">json-loader;</span><span class="sxs-lookup"><span data-stu-id="31969-115">json-loader</span></span>
- <span data-ttu-id="31969-116">loader-load-themed-styles.</span><span class="sxs-lookup"><span data-stu-id="31969-116">loader-load-themed-styles</span></span>

<span data-ttu-id="31969-117">Расширение конфигурации Webpack платформы с использованием пользовательских загрузчиков — это понятный линейный процесс, описанный [в документации по Webpack](https://webpack.js.org/contribute/writing-a-loader/).</span><span class="sxs-lookup"><span data-stu-id="31969-117">Extending the framework webpack configuration with custom loaders is a straightforward process which is documented [here in the webpack documentation](https://webpack.js.org/contribute/writing-a-loader/).</span></span>

> <span data-ttu-id="31969-118">Дополнительные сведения о загрузчиках см. в [документации по загрузчикам Webpack](https://webpack.js.org/loaders/)</span><span class="sxs-lookup"><span data-stu-id="31969-118">You can find more details on the loaders from [webpack loaders documentation](https://webpack.js.org/loaders/)</span></span>

## <a name="example-using-the-markdown-loader-package"></a><span data-ttu-id="31969-119">Пример: использование пакета markdown-loader</span><span class="sxs-lookup"><span data-stu-id="31969-119">Example: Using the markdown-loader package</span></span>
<span data-ttu-id="31969-120">В качестве примера рассмотрим [пакет markdown-loader](https://www.npmjs.com/package/markdown-loader).</span><span class="sxs-lookup"><span data-stu-id="31969-120">As an example, let's use the [markdown-loader package](https://www.npmjs.com/package/markdown-loader).</span></span>  <span data-ttu-id="31969-121">Это загрузчик, с помощью которого вы можете ссылаться на файл `.md` и выводить его в качестве строки HTML.</span><span class="sxs-lookup"><span data-stu-id="31969-121">As an example, let's use the markdown-loader package.  It's a loader which allows you to reference an `.md` file and output it as HTML string.</span></span>

<span data-ttu-id="31969-122">Готовый образец можно скачать [здесь](https://aka.ms/spfx-extend-Webpack-sample).</span><span class="sxs-lookup"><span data-stu-id="31969-122">You can download the completed sample [here](https://aka.ms/spfx-extend-Webpack-sample).</span></span>

### <a name="step-1---install-the-package"></a><span data-ttu-id="31969-123">Этап 1. Установка пакета</span><span class="sxs-lookup"><span data-stu-id="31969-123">Step 1 - Install the package</span></span>
<span data-ttu-id="31969-124">Добавим в проект ссылку на пакет markdown-loader.</span><span class="sxs-lookup"><span data-stu-id="31969-124">Let's reference markdown-loader in our project.</span></span>

```
npm i --save markdown-loader
```

### <a name="step-2---configure-webpack"></a><span data-ttu-id="31969-125">Этап 2. Настройка Webpack</span><span class="sxs-lookup"><span data-stu-id="31969-125">Step 2 - Configure Webpack</span></span>
<span data-ttu-id="31969-126">Теперь, когда у нас установлен пакет, давайте настроим конфигурацию Webpack для SharePoint Framework так, чтобы она включала пакет `markdown-loader`.</span><span class="sxs-lookup"><span data-stu-id="31969-126">Now that we have the package installed, lets now configure the SharePoint Framework webpack configuration to include the markdown-loader.</span></span>

<span data-ttu-id="31969-127">В [документации по пакету markdown-loader](https://github.com/peerigon/markdown-loader) показано, как расширить конфигурацию Webpack, чтобы она включала загрузчик:</span><span class="sxs-lookup"><span data-stu-id="31969-127">In the [documentation of markdown-loader](https://github.com/peerigon/markdown-loader), it shows how to extend the webpack configuration to include the loader:</span></span>

```JavaScript
{
  module: {
    rules: [
      {
        test: /\.md$/,
        use: [
          {
            loader: 'html-loader'
          },
          {
            loader: 'markdown-loader',
            options: {
              /* options for markdown-loader here */
            }
          }
        ]
      }
    ]
  }
}
```

<span data-ttu-id="31969-128">Давайте посмотрим, что делает эта конфигурация.</span><span class="sxs-lookup"><span data-stu-id="31969-128">Let's take a look at what this configuration is doing:</span></span>
  - <span data-ttu-id="31969-129">Массив `rules` в конфигурации Webpack определяет набор проверок путей к файлам и загрузчики, которые следует использовать при обнаружении ресурса, соответствующего условиям проверки.</span><span class="sxs-lookup"><span data-stu-id="31969-129">The `rules` array in the Webpack configuration defines a set of file path tests and the loaders that should be used when a resource is found that matches the test.</span></span> <span data-ttu-id="31969-130">В этом случае свойство `test` выполняет проверку путей к файлам, которые заканчиваются на `.md`.</span><span class="sxs-lookup"><span data-stu-id="31969-130">In this case, the `test` property checks for file paths that end with `.md`.</span></span>
  - <span data-ttu-id="31969-131">Массив `use` описывает список загрузчиков, которые последовательно применяются к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="31969-131">The `use` array describes a list of loaders that are applied sequentially to the resource.</span></span> <span data-ttu-id="31969-132">Они применяются, начиная с последнего загрузчика и заканчивая первым.</span><span class="sxs-lookup"><span data-stu-id="31969-132">They are applied from last to first.</span></span> <span data-ttu-id="31969-133">В данном случае первым будет применен загрузчик `markdown-loader`, а последним — `html-loader`.</span><span class="sxs-lookup"><span data-stu-id="31969-133">In this case, the first loader to be applied will be `markdown-loader` and the last loader to be applied will be `html-loader`.</span></span>
  - <span data-ttu-id="31969-134">Если указано несколько загрузчиков, результаты работы каждого загрузчика передаются следующему.</span><span class="sxs-lookup"><span data-stu-id="31969-134">When multiple loaders are specified, the result of each loader is piped to the next.</span></span>

<span data-ttu-id="31969-135">Мы будем использовать эти сведения для настройки загрузчика в нашем проекте.</span><span class="sxs-lookup"><span data-stu-id="31969-135">We will use this information to configure it in our project.</span></span>

<span data-ttu-id="31969-136">Чтобы добавить этот пользовательский загрузчик в конфигурацию Webpack для SharePoint Framework, необходимо поручить задаче сборки настроить Webpack.</span><span class="sxs-lookup"><span data-stu-id="31969-136">In order to add this custom loader into the SharePoint Framework Webpack configuration, we will need to instruct the build task to configure Webpack.</span></span> <span data-ttu-id="31969-137">Задачи сборки определены в файле gulp (`gulpfile.js`), который находится в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="31969-137">The build tasks are defined in the gulp file - `gulpfile.js` - which is located at the root of your project.</span></span>

<span data-ttu-id="31969-138">Измените файл `gulpfile.js`, добавив следующий код перед строкой `build.initialize(gulp);`:</span><span class="sxs-lookup"><span data-stu-id="31969-138">Edit the `gulpfile.js` and add the following code right before `build.initialize(gulp);`:</span></span>

```JavaScript
build.configureWebpack.mergeConfig({
  additionalConfiguration: (generatedConfiguration) => {
    generatedConfiguration.module.rules.push(
      {
        test: /\.md$/,
        use: [
          {
            loader: 'html-loader'
          },
          {
            loader: 'markdown-loader'
          }
        ]
      }
    );

    return generatedConfiguration;
  }
});
```

<span data-ttu-id="31969-139">Давайте разберем, что делает этот фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="31969-139">Let's walk through what this code snippet is doing:</span></span>
  - <span data-ttu-id="31969-140">Как следует из ее названия, задача `ConfigureWebpackTask` (как проиллюстрировано в примере `build.configureWebpack`) настраивает Webpack.</span><span class="sxs-lookup"><span data-stu-id="31969-140">As its name implies, the `ConfigureWebpackTask` (instantiated as `build.configureWebpack`) configures webpack for us.</span></span> <span data-ttu-id="31969-141">Существует много особых конфигураций для сборки проектов SPFx, поэтому в данной задаче используется нетривиальная логика.</span><span class="sxs-lookup"><span data-stu-id="31969-141">There is a lot of special configuration that happens to build SPFx projects, so there is some nontrivial logic in this task.</span></span>
  - <span data-ttu-id="31969-142">Задача `ConfigureWebpackTask` получает необязательное свойство `additionalConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="31969-142">The `ConfigureWebpackTask` takes an optional `additionalConfiguration` property.</span></span> <span data-ttu-id="31969-143">Нам необходимо настроить это свойство для функции, которая получает созданную конфигурацию, вносит в нее необходимые нам изменения, а затем возвращает измененную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="31969-143">We want to set this property to a function which takes the generated configuration, makes our modifications to it, and then returns the updated configuration.</span></span> <span data-ttu-id="31969-144">**Обратите внимание, что эта функция должна обязательно возвращать конфигурацию Webpack в цепочку инструментов, в противном случае Webpack будет настроен неправильно.**</span><span class="sxs-lookup"><span data-stu-id="31969-144">**Note that this function must return a Webpack configuration to the toolchain, otherwise Webpack will not be configured correctly.**</span></span>
  - <span data-ttu-id="31969-145">В теле функции, которую мы задали для `additionalConfiguration`, просто отправьте новое правило в существующий набор правил в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="31969-145">Inside the body of the function that we set to `additionalConfiguration`, simply push a new rule onto the existing set of rules in the configuration.</span></span> <span data-ttu-id="31969-146">Обратите внимание, что это новое правило очень похоже на пример в фрагменте конфигурации в начале **этапа 2**.</span><span class="sxs-lookup"><span data-stu-id="31969-146">Notice that this new rule is very similar to example in the configuration snippet at the top of **Step 2**.</span></span>

> <span data-ttu-id="31969-147">Используя этот подход, вы можете полностью заменить конфигурацию Webpack, используемую по умолчанию в цепочке инструментов, но для достижения максимальной производительности и оптимизации не рекомендуется делать это, если иное не указано в документации.</span><span class="sxs-lookup"><span data-stu-id="31969-147">While you are able to completely replace the toolchain's default webpack configuration using this approach, to get the maximum benefit with performance and optimization, it is not recommended to do so unless stated otherwise in the documentation.</span></span>

### <a name="step-3---update-your-code"></a><span data-ttu-id="31969-148">Этап 3. Внесение изменений в код</span><span class="sxs-lookup"><span data-stu-id="31969-148">Step 3 - Update your code</span></span>
<span data-ttu-id="31969-149">Теперь, когда мы настроили загрузчик, давайте обновим код и добавим несколько файлов, чтобы протестировать сценарий.</span><span class="sxs-lookup"><span data-stu-id="31969-149">Now that we have configured the loader, lets update our code and add few files to test the scenario.</span></span>

<span data-ttu-id="31969-150">Создайте файл `my-markdown.md` с текстом Markdown в каталоге `src` папки проекта.</span><span class="sxs-lookup"><span data-stu-id="31969-150">Create a file `my-markdown.md` in the `src` directory of your project folder with some Markdown text in it.</span></span>

```md
#Hello Markdown

*Markdown* is a simple markup format to write content.

You can also format text as **bold** or *italics* or ***bold italics***
```

<span data-ttu-id="31969-151">При сборке проекта загрузчик markdown-loader Webpack преобразует этот текст в строку HTML.</span><span class="sxs-lookup"><span data-stu-id="31969-151">When you build the project, the Webpack markdown-loader will convert this markdown text to a HTML string.</span></span> <span data-ttu-id="31969-152">Чтобы использовать эту строку HTML в любом из ваших исходных файлов `*.ts`, добавьте следующую строку `require()` в начале файла после кода импорта:</span><span class="sxs-lookup"><span data-stu-id="31969-152">When you build the project, the webpack markdown-loader will convert this markdown text to a HTML string. To use this HTML string in any of your source `*.ts` files, add the following `require()` line at the top of the file after your imports, for example:</span></span>


```TypeScript
const markdownString: string = require<string>('./../../../../src/readme.md');
```

<span data-ttu-id="31969-153">По умолчанию Webpack будет искать файл в папке `lib`, но по умолчанию файлы `.md` не копируются в папку `lib`, поэтому необходимо составить довольно длинный относительный путь.</span><span class="sxs-lookup"><span data-stu-id="31969-153">Webpack by default will look in the `lib` folder for the file, but by default `.md` files don't get copied to the `lib` folder, meaning we need to create a rather lengthy relative path. We can control this setting by defining a config file to tell the toolchain to copy  files to the lib folder.</span></span> <span data-ttu-id="31969-154">Мы можем изменить этот параметр, определив файл конфигурации, и сообщить цепочке инструментов, что необходимо скопировать файлы `md` в папку lib.</span><span class="sxs-lookup"><span data-stu-id="31969-154">We can control this setting by defining a config file to tell the toolchain to copy `md` files to the lib folder.</span></span>

<span data-ttu-id="31969-155">Создайте файл `copy-static-assets.json` в каталоге `config`, чтобы сообщить системе сборки, что необходимо скопировать некоторые дополнительные файлы из папки `src` в папку `lib`.</span><span class="sxs-lookup"><span data-stu-id="31969-155">Create a file `copy-static-assets.json` in the `config` directory to tell the build system to copy some additional files from `src` to `lib`.</span></span> <span data-ttu-id="31969-156">По умолчанию эта задача сборки копирует файлы с расширениями, которые понятны конфигурации Webpack, используемой по умолчанию, цепочки инструментов (например, `png` и `json`), поэтому нам просто необходимо поручить ей скопировать файлы `md`.</span><span class="sxs-lookup"><span data-stu-id="31969-156">Create a file  in the  directory to tell the build system to copy some additional files from  to . By default, this build task copies files with extensions that the default toolchain webpack configuration understands (like `png` and `json`), so we just need to tell it to also copy `md` files.</span></span>

```JSON
{
  "includeExtensions": [
    "md"
  ]
}
```

<span data-ttu-id="31969-157">Теперь в операторе `require` вместо относительного пути можно использовать путь к файлу, например:</span><span class="sxs-lookup"><span data-stu-id="31969-157">Now instead of using the relative path, you can use the file path in your `require` statement, for example:</span></span>

```TypeScript
const markdownString: string = require<string>('./../../readme.md');
```

<span data-ttu-id="31969-158">Вы можете ссылаться на эту строку в коде, например:</span><span class="sxs-lookup"><span data-stu-id="31969-158">You can then reference this string in your code, for example:</span></span>

``` TypeScript
public render(): void {
  this.domElement.innerHTML = markdownString;
}
```

### <a name="step-4---build-and-test-your-code"></a><span data-ttu-id="31969-159">Этап 4. Сборка и тестирование кода</span><span class="sxs-lookup"><span data-stu-id="31969-159">Step 4 - Build and test your code</span></span>
<span data-ttu-id="31969-160">Чтобы собрать и протестировать код, выполните в консоли следующую команду для корневого каталога проекта:</span><span class="sxs-lookup"><span data-stu-id="31969-160">To build and test your code, execute the following command in a console in the root of your project directory:</span></span>

```
gulp serve
```
