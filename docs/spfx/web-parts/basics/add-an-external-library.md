---
title: "Добавление внешней библиотеки в клиентскую веб-часть SharePoint"
description: "Добавление внешней библиотеки JavaScript в пакет и совместное использование библиотек."
ms.date: 01/29/2018
ms.prod: sharepoint
ms.openlocfilehash: 7b5091f531ad16127aa71299f9c1951cbb2c853c
ms.sourcegitcommit: e4bf60eabffe63dc07f96824167d249c0678db82
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/30/2018
---
# <a name="add-an-external-library-to-your-sharepoint-client-side-web-part"></a><span data-ttu-id="8c55a-103">Добавление внешней библиотеки в клиентскую веб-часть SharePoint</span><span class="sxs-lookup"><span data-stu-id="8c55a-103">Add an external library to your SharePoint client-side web part</span></span>

<span data-ttu-id="8c55a-p101">Вам может понадобиться добавить в веб-часть одну или несколько библиотек JavaScript. В этой статье описано, как добавить внешнюю библиотеку в пакет и использовать библиотеки в нескольких веб-частях.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p101">You might want to include one or more JavaScript libraries in your web part. This article shows you how to bundle an external library and share libraries.</span></span>

## <a name="bundle-a-script"></a><span data-ttu-id="8c55a-106">Добавление сценария в пакет</span><span class="sxs-lookup"><span data-stu-id="8c55a-106">Bundle a script</span></span>

<span data-ttu-id="8c55a-107">По умолчанию средство увязки веб-частей в пакеты автоматически добавляет библиотеки, которые представляют собой зависимости для модуля веб-части.</span><span class="sxs-lookup"><span data-stu-id="8c55a-107">By default, the web part bundler automatically includes any library that is a dependency of the web part module.</span></span> <span data-ttu-id="8c55a-108">Это означает, что такие библиотеки развертываются в том же файле пакета JavaScript, что и веб-часть.</span><span class="sxs-lookup"><span data-stu-id="8c55a-108">This means that the library is deployed in the same JavaScript bundle file as your web part.</span></span> <span data-ttu-id="8c55a-109">Это удобно в случае небольших библиотек, которые не используются в нескольких веб-частях.</span><span class="sxs-lookup"><span data-stu-id="8c55a-109">This is more useful for smaller libraries that are not used in multiple web parts.</span></span>

### <a name="example"></a><span data-ttu-id="8c55a-110">Пример</span><span class="sxs-lookup"><span data-stu-id="8c55a-110">Example</span></span>

1. <span data-ttu-id="8c55a-111">Добавьте [библиотеку проверки](https://www.npmjs.com/package/validator) строк в веб-часть.</span><span class="sxs-lookup"><span data-stu-id="8c55a-111">Include the string validating library [validator](https://www.npmjs.com/package/validator) package into a web part.</span></span>

2. <span data-ttu-id="8c55a-112">Скачайте пакет средств проверки, используя npm:</span><span class="sxs-lookup"><span data-stu-id="8c55a-112">Download the validator package from npm:</span></span>

    ```sh
    npm install validator --save
    ```

    > [!NOTE] 
    > <span data-ttu-id="8c55a-p103">Так как вы используете TypeScript, для добавляемого пакета нужны определения типов. Это очень важно при написании кода, так как TypeScript — это просто расширенная версия JavaScript. При компиляции код TypeScript преобразуется в код JavaScript. Для поиска определений типов можно использовать **npm**, например `npm install @types/{package} --save`.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p103">Because you're using TypeScript, you need typings for the package you add. This is essential when you are writing code because TypeScript is just a superset of JavaScript. All the TypeScript code is still converted to JavaScript code when you compile. You can search for and find typings by using **npm**, for example: `npm install @types/{package} --save`</span></span>

3. <span data-ttu-id="8c55a-117">Создайте в папке веб-части файл с именем `validator.d.ts` и добавьте приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="8c55a-117">Create a file in the your web part's folder called `validator.d.ts` and add the following:</span></span>

    ```typescript
    declare module "validator" {
        export function isEmail(email: string): boolean;
        export function isAscii(text: string): boolean;
    }
    ```

    > [!NOTE] 
    > <span data-ttu-id="8c55a-118">Для некоторых библиотек нет определений типов.</span><span class="sxs-lookup"><span data-stu-id="8c55a-118">Some libraries do not have typings.</span></span> <span data-ttu-id="8c55a-119">Предположим, что [сообщество еще не создало файл определений типов](https://www.npmjs.com/package/@types/validator) для библиотеки Validator.</span><span class="sxs-lookup"><span data-stu-id="8c55a-119">While the validator library does have a [community provided typings file](https://www.npmjs.com/package/@types/validator), for this scenario let's assume it does not.</span></span> <span data-ttu-id="8c55a-120">В этом случае нужно задать собственный файл определений типов `.d.ts` для библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8c55a-120">Note: Some libraries do not have typings. Validator is one of them. In this case you would want to define your own typings definition `.d.ts` file for the library. The following code shows an example.</span></span> <span data-ttu-id="8c55a-121">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="8c55a-121">The following code shows an example token file.</span></span>

4. <span data-ttu-id="8c55a-122">Импортируйте определения типов в файле веб-части:</span><span class="sxs-lookup"><span data-stu-id="8c55a-122">In your web part file, import the typings:</span></span>

    ```typescript
    import * as validator from 'validator';
    ```

5. <span data-ttu-id="8c55a-123">Укажите библиотеку проверки в коде веб-части:</span><span class="sxs-lookup"><span data-stu-id="8c55a-123">Use the validator library in your web part code:</span></span>

    ```typescript
    validator.isEmail('someone@example.com');
    ```

## <a name="share-a-library-among-multiple-web-parts"></a><span data-ttu-id="8c55a-124">Использование библиотеки несколькими веб-частями</span><span class="sxs-lookup"><span data-stu-id="8c55a-124">Share a library among multiple web parts</span></span>

<span data-ttu-id="8c55a-p105">Клиентское решение может включать несколько веб-частей. Для них может потребоваться импортировать или использовать одну и ту же библиотеку. В таких случаях не добавляйте библиотеку в пакет, а включите ее в отдельный файл JavaScript, чтобы повысить эффективность и улучшить кэширование. Особенно это касается больших библиотек.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p105">Your client-side solution might include multiple web parts. These web parts might need to import or share the same library. In such cases, instead of bundling the library, you should include it in a separate JavaScript file to improve performance and caching. This is especially true of larger libraries.</span></span>

### <a name="example"></a><span data-ttu-id="8c55a-129">Пример</span><span class="sxs-lookup"><span data-stu-id="8c55a-129">Example</span></span>

<span data-ttu-id="8c55a-130">В этом примере пакет [marked](https://www.npmjs.com/package/marked) (компилятор markdown) помещается в отдельный пакет для совместного использования.</span><span class="sxs-lookup"><span data-stu-id="8c55a-130">In this example, you will share the [marked](https://www.npmjs.com/package/marked) package - a Markdown compiler - in a separate bundle.</span></span>

1. <span data-ttu-id="8c55a-131">Скачайте пакет **marked** с помощью npm:</span><span class="sxs-lookup"><span data-stu-id="8c55a-131">Download the **marked** package from npm:</span></span>

    ```sh
    npm install marked --save
    ```

2. <span data-ttu-id="8c55a-132">Скачайте определения типов:</span><span class="sxs-lookup"><span data-stu-id="8c55a-132">Download the typings:</span></span>

    ```sh
    npm install @types/marked --save
    ```

3. <span data-ttu-id="8c55a-133">Измените **config/config.json** и добавьте запись в схему **externals**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-133">Edit the **config/config.json**, and add an entry to the **externals** map.</span></span> <span data-ttu-id="8c55a-134">В результате средство увязки поместит эту библиотеку в отдельный файл,</span><span class="sxs-lookup"><span data-stu-id="8c55a-134">This is what tells the bundler to put this in a separate file.</span></span> <span data-ttu-id="8c55a-135">а не добавит в пакет:</span><span class="sxs-lookup"><span data-stu-id="8c55a-135">This prevents the bundler from bundling this library:</span></span>

    ```json
    "marked": "node_modules/marked/marked.min.js"
    ```

4. <span data-ttu-id="8c55a-136">Теперь, когда мы добавили пакет и определения типов для библиотеки, добавьте оператор для импорта библиотеки `marked` в веб-части:</span><span class="sxs-lookup"><span data-stu-id="8c55a-136">Add the statement to import the `marked` library in your web part now that we have added the package and typings for the library:</span></span>

    ```typescript
    import * as marked from 'marked';
    ```

5. <span data-ttu-id="8c55a-137">Укажите библиотеку в своей веб-части:</span><span class="sxs-lookup"><span data-stu-id="8c55a-137">Use the library in your web part:</span></span>

    ```typescript
    console.log(marked('I am using __markdown__.'));
    ```

## <a name="load-a-script-from-a-cdn"></a><span data-ttu-id="8c55a-138">Загрузка сценария из сети CDN</span><span class="sxs-lookup"><span data-stu-id="8c55a-138">Loading a script from a CDN</span></span>

<span data-ttu-id="8c55a-139">Вы можете не загружать библиотеку из пакета npm, а загрузить сценарий из сети доставки содержимого (CDN).</span><span class="sxs-lookup"><span data-stu-id="8c55a-139">Instead of loading the library from an npm package, you might want to load a script from a Content Delivery Network (CDN).</span></span> <span data-ttu-id="8c55a-140">Для этого измените файл **config.json**, чтобы обеспечить загрузку библиотеки с использованием URL-адреса CDN.</span><span class="sxs-lookup"><span data-stu-id="8c55a-140">Instead of loading the library from a npm package, you might want to load a script from a CDN. To do so, edit the **config.json** file to load the library from its CDN URL.</span></span>

### <a name="example"></a><span data-ttu-id="8c55a-141">Пример</span><span class="sxs-lookup"><span data-stu-id="8c55a-141">Example</span></span>

<span data-ttu-id="8c55a-p108">В этом примере из CDN загружается jQuery. Пакет npm устанавливать не нужно. Но определения типов все равно нужно установить.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p108">In this example, you will load jQuery from CDN. You don't need to install the npm package. However, you still need to install the typings.</span></span>

1. <span data-ttu-id="8c55a-145">Установите определения типов для jQuery:</span><span class="sxs-lookup"><span data-stu-id="8c55a-145">Install the typings for jQuery:</span></span>

    ```sh
    npm install --save @types/jquery
    ```

2. <span data-ttu-id="8c55a-p109">Обновите файл `config.json` в папке `config` для загрузки jQuery из CDN. Добавьте запись в поле `externals`:</span><span class="sxs-lookup"><span data-stu-id="8c55a-p109">Update the `config.json` in the `config` folder to load jQuery from CDN. Add an entry to the `externals` field:</span></span>

    ```json
    "jquery": "https://code.jquery.com/jquery-3.1.0.min.js"
    ```

3. <span data-ttu-id="8c55a-148">Импортируйте jQuery в веб-часть:</span><span class="sxs-lookup"><span data-stu-id="8c55a-148">Import jQuery in your web part:</span></span>

    ```typescript
    import * as $ from 'jquery';
    ```

4. <span data-ttu-id="8c55a-149">Используйте jQuery в своей веб-части:</span><span class="sxs-lookup"><span data-stu-id="8c55a-149">Use jQuery in your web part:</span></span>

    ```javascript
    alert( $('#foo').val() );
    ```

## <a name="load-a-non-amd-module"></a><span data-ttu-id="8c55a-150">Загрузка модуля, отличного от AMD-модуля</span><span class="sxs-lookup"><span data-stu-id="8c55a-150">Loading a non-AMD module</span></span>

<span data-ttu-id="8c55a-p110">Некоторые сценарии JavaScript предусматривают хранение библиотек в глобальном пространстве имен. Такой подход устарел. Сейчас используются модули [ES6](https://github.com/lukehoban/es6features/blob/master/README.md#modules), [UMD (Universal Module Definitions)](https://github.com/umdjs/umd) / [AMD (Asynchronous Module Definitions)](https://en.wikipedia.org/wiki/Asynchronous_module_definition). Возможно, вам потребуется загрузить такие библиотеки в веб-часть.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p110">Some scripts follow the legacy JavaScript pattern of storing the library on the global namespace. This pattern is now deprecated in favor of [Universal Module Definitions (UMD)](https://github.com/umdjs/umd) / [Asynchronous Module Definitions (AMD)](https://en.wikipedia.org/wiki/Asynchronous_module_definition) or [ES6 modules](https://github.com/lukehoban/es6features/blob/master/README.md#modules). However, you might need to load such libraries in your web part.</span></span>

> [!TIP] 
> <span data-ttu-id="8c55a-154">Трудно определить вручную, является ли загружаемый сценарий сценарием AMD,</span><span class="sxs-lookup"><span data-stu-id="8c55a-154">It's difficult to determine manually whether the script that you're trying to load is an AMD or a non-AMD script.</span></span> <span data-ttu-id="8c55a-155">особенно если он минифицирован.</span><span class="sxs-lookup"><span data-stu-id="8c55a-155">This is especially the case if the script that you're trying to load is minified.</span></span> <span data-ttu-id="8c55a-156">Если ваш сценарий размещен по общедоступному URL-адресу, вы можете использовать бесплатный инструмент [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/), чтобы автоматически определить тип сценария.</span><span class="sxs-lookup"><span data-stu-id="8c55a-156">If your script is hosted on a publicly accessible URL, you can use the free [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/) tool to determine the type of script for you.</span></span> <span data-ttu-id="8c55a-157">Кроме того, этот инструмент позволяет узнать, правильно ли настроен место размещения, с которого загружается сценарий.</span><span class="sxs-lookup"><span data-stu-id="8c55a-157">Additionally, this tool lets you know whether the hosting location from which you're loading the script is properly configured.</span></span>

<span data-ttu-id="8c55a-158">Чтобы загрузить модуль, созданный не с помощью AMD, добавьте дополнительное свойство в запись в файле **config.json**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-158">To load a non-AMD module, you add an additional property to the entry in your **config.json** file.</span></span>

### <a name="example"></a><span data-ttu-id="8c55a-159">Пример</span><span class="sxs-lookup"><span data-stu-id="8c55a-159">Example</span></span>

<span data-ttu-id="8c55a-p112">В этом примере из CDN Contoso загружается фиктивный модуль, отличный от AMD-модуля. Эти действия предназначены для любого сценария, отличного от AMD-сценария, в каталоге src/ или node_modules/.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p112">In this example, you will load a fictional non-AMD module from Contoso's CDN. These steps  apply for any non-AMD script in your src/ or node_modules/ directory.</span></span>

<span data-ttu-id="8c55a-p113">Сценарий называется **Contoso.js**. Путь к нему: **https://contoso.com/contoso.js**. Вот его содержимое:</span><span class="sxs-lookup"><span data-stu-id="8c55a-p113">The script is called **Contoso.js** and is stored at **https://contoso.com/contoso.js**. Its contents are:</span></span>

```javascript
var ContosoJS = {
  say: function(text) { alert(text); },
  sayHello: function(name) { alert('Hello, ' + name + '!'); }
};
```

<br/>

1. <span data-ttu-id="8c55a-164">Создайте определения типов для сценария в файле **contoso.d.ts** из папки веб-части.</span><span class="sxs-lookup"><span data-stu-id="8c55a-164">Create typings for the script in a file called **contoso.d.ts** in the web part folder.</span></span>

    ```typescript
    declare module "contoso" {
        interface IContoso {
            say(text: string): void;
            sayHello(name: string): void;
        }
        var contoso: IContoso;
        export = contoso;
    }
    ```

2. <span data-ttu-id="8c55a-p114">Включите этот сценарий в файл **config.json**. Добавьте запись в схему **externals**:</span><span class="sxs-lookup"><span data-stu-id="8c55a-p114">Update the **config.json** file to include this script. Add an entry to the **externals** map:</span></span>

    ```json
    {
        "contoso": {
            "path": "https://contoso.com/contoso.js",
            "globalName": "ContosoJS"
        }
    }
    ```

3. <span data-ttu-id="8c55a-167">Добавьте операцию импорта в код веб-части:</span><span class="sxs-lookup"><span data-stu-id="8c55a-167">Add an import to your web part code:</span></span>

    ```typescript
    import contoso from 'contoso';
    ```

4. <span data-ttu-id="8c55a-168">Используйте библиотеку contoso в своем коде:</span><span class="sxs-lookup"><span data-stu-id="8c55a-168">Use the contoso library in your code:</span></span>

    ```typescript
    contoso.sayHello(username);
    ```

## <a name="load-a-library-that-has-a-dependency-on-another-library"></a><span data-ttu-id="8c55a-169">Загрузка библиотеки с зависимостью от другой библиотеки</span><span class="sxs-lookup"><span data-stu-id="8c55a-169">Loading a library that has a dependency on another library</span></span>

<span data-ttu-id="8c55a-170">Многие библиотеки содержат зависимости от другой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8c55a-170">Many libraries have dependencies on another library.</span></span> <span data-ttu-id="8c55a-171">Такие зависимости можно указать в файле **config.json** с помощью свойства **globalDependencies**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-171">Many libraries have dependencies on another library. You can specify such dependencies in the **config.json** file using the **globalDependencies** property.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8c55a-172">Обратите внимание, что это поле не нужно указывать для AMD-модулей. Они импортируют друг друга правильно.</span><span class="sxs-lookup"><span data-stu-id="8c55a-172">Note that you don't have to specify this field for non-AMD modules; they will properly import each other. However, it is important to note that a non-AMD module have a AMD module as a dependency.</span></span> <span data-ttu-id="8c55a-173">Однако AMD-модуль не может зависеть от модуля, отличного от AMD.</span><span class="sxs-lookup"><span data-stu-id="8c55a-173">However, a non-AMD module cannot have an AMD module as a dependency.</span></span> <span data-ttu-id="8c55a-174">В некоторых случаях можно загрузить сценарий AMD в виде сценария, отличного от AMD.</span><span class="sxs-lookup"><span data-stu-id="8c55a-174">In some cases, it is possible to load an AMD script as a non-AMD script.</span></span> <span data-ttu-id="8c55a-175">Это часто требуется при работе с библиотекой jQuery, которая сама по себе является сценарием AMD, и подключаемыми модулями jQuery, которые в большинстве случаев распространяются как сценарии, отличные от AMD, и зависят от jQuery.</span><span class="sxs-lookup"><span data-stu-id="8c55a-175">This is often required when working with jQuery, which by itself is an AMD script, and jQuery plug-ins, which most of the time are distributed as non-AMD scripts and which depend on jQuery.</span></span>

<span data-ttu-id="8c55a-176">Ниже приведены два примера.</span><span class="sxs-lookup"><span data-stu-id="8c55a-176">There are two examples of this.</span></span>

### <a name="non-amd-module-has-a-non-amd-module-dependency"></a><span data-ttu-id="8c55a-177">Для модуля, отличного от AMD-модуля, предусмотрена соответствующая зависимость</span><span class="sxs-lookup"><span data-stu-id="8c55a-177">Non-AMD module has a non-AMD module dependency</span></span>

<span data-ttu-id="8c55a-p117">В этом примере используются два вымышленных сценария. Они хранятся в папке **src/**, но их также можно загрузить из CDN.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p117">This example involves two fictional scripts. These are in the **src/** folder, although they can also be loaded from a CDN.</span></span>

<span data-ttu-id="8c55a-180">**ContosoUI.js**</span><span class="sxs-lookup"><span data-stu-id="8c55a-180">**ContosoUI.js**</span></span>

```javascript
Contoso.EventList = {
    alert: function() {
        var events = Contoso.getEvents();
        events.forEach( function(event) {
            alert(event);
        });
    }
}
```

<span data-ttu-id="8c55a-181">**ContosoCore.js**</span><span class="sxs-lookup"><span data-stu-id="8c55a-181">**ContosoCore.js**</span></span>

```javascript
var Contoso = {
    getEvents: function() {
        return ['A', 'B', 'C'];
    }
};
```

<br/>

1. <span data-ttu-id="8c55a-p118">Добавьте или создайте определения типов для этого класса. В этом случае нужно создать файл `Contoso.d.ts`, который содержит определения типов для обоих файлов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p118">Add or create typings for this class. In this case, you will create `Contoso.d.ts`, which contains typings for both JavaScript files.</span></span>

    <span data-ttu-id="8c55a-184">**contoso.d.ts**</span><span class="sxs-lookup"><span data-stu-id="8c55a-184">**contoso.d.ts**</span></span>

    ```typescript
    declare module "contoso" {
        interface IEventList {
            alert(): void;
        }
        interface IContoso {
            getEvents(): string[];
            EventList: IEventList;
        }
        var contoso: IContoso;
        export = contoso;
    }
    ```

2. <span data-ttu-id="8c55a-p119">Обновите файл **config.json**. Добавьте две записи в **externals**:</span><span class="sxs-lookup"><span data-stu-id="8c55a-p119">Update the **config.json** file. Add two entries to **externals**:</span></span>

    ```json
    {
        "contoso": {
            "path": "/src/ContosoCore.js",
            "globalName": "Contoso"
        },
        "contoso-ui": {
            "path": "/src/ContosoUI.js",
            "globalName": "Contoso",
            "globalDependencies": ["contoso"]
        }
    }
    ```

3. <span data-ttu-id="8c55a-187">Добавьте операции импорта для Contoso и ContosoUI:</span><span class="sxs-lookup"><span data-stu-id="8c55a-187">Add imports for Contoso and ContosoUI:</span></span>

    ```typescript
    import contoso = require('contoso');
    require('contoso-ui');
    ```

4. <span data-ttu-id="8c55a-188">Укажите библиотеки в своем коде:</span><span class="sxs-lookup"><span data-stu-id="8c55a-188">Use the libraries in your code:</span></span>

    ```typescript
    contoso.EventList.alert();
    ```

## <a name="load-sharepoint-jsom"></a><span data-ttu-id="8c55a-189">Загрузка JSOM SharePoint</span><span class="sxs-lookup"><span data-stu-id="8c55a-189">Load SharePoint JSOM Scripts Using SPComponentLoader</span></span>

<span data-ttu-id="8c55a-p120">Модели JSOM SharePoint загружаются практически так же, как сценарии с зависимостями, отличные от AMD-сценариев. Это значит, что используются параметры **globalName** и **globalDependency**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-p120">Loading SharePoint JSOM is essentially the same scenario as loading non-AMD scripts that have dependencies. This means using both the **globalName** and **globalDependency** options.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8c55a-192">Обратите внимание, что приведенный ниже подход вызовет ошибки на классических страницах SharePoint, где модель JSOM уже загружена.</span><span class="sxs-lookup"><span data-stu-id="8c55a-192">Note that the following approach causes errors in classic SharePoint pages, where SharePoint JSOM is already loaded.</span></span> <span data-ttu-id="8c55a-193">Если ваша веб-часть должна работать как с классическими, так и современными страницами, нужно сначала проверить, доступна ли модель JSOM, а если нет, загрузить ее динамически с помощью **SPComponentLoader**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-193">Important: Please note, that the following approach will cause error in classic SharePoint pages, where SharePoint JSOM is already loaded. If you require your web part to work with both classic and modern pages then you should first check if SharePoint JSOM is already available and if it isn't, load it dynamically using the **SPComponentLoader**.</span></span>

<br/>

1. <span data-ttu-id="8c55a-194">Установите определения типов для Microsoft Ajax (зависимости для определений типов JSOM представлены ниже).</span><span class="sxs-lookup"><span data-stu-id="8c55a-194">Install typings for Microsoft Ajax which is a dependency for JSOM typings:</span></span>

    ```sh
    npm install @types/microsoft-ajax --save
    ```

2. <span data-ttu-id="8c55a-195">Установите определения типов для JSOM:</span><span class="sxs-lookup"><span data-stu-id="8c55a-195">Install typings for the JSOM:</span></span>

    ```sh
    npm install @types/sharepoint --save
    ```

3. <span data-ttu-id="8c55a-196">Добавьте записи в файл `config.json`:</span><span class="sxs-lookup"><span data-stu-id="8c55a-196">Add entries to the `config.json`:</span></span>

    ```json
    {
        "sp-init": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/init.js",
            "globalName": "$_global_init"
        },
        "microsoft-ajax": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/MicrosoftAjax.js",
            "globalName": "Sys",
            "globalDependencies": [ "sp-init" ]
        },
        "sp-runtime": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/SP.Runtime.js",
            "globalName": "SP",
            "globalDependencies": [ "microsoft-ajax" ]
        },
        "sharepoint": {
            "path": "https://CONTOSO.sharepoint.com/_layouts/15/SP.js",
            "globalName": "SP",
            "globalDependencies": [ "sp-runtime" ]
        }
    }
    ```

4. <span data-ttu-id="8c55a-197">Добавьте в веб-часть операторы `require`:</span><span class="sxs-lookup"><span data-stu-id="8c55a-197">In your web part, add the require statements:</span></span>

    ```typescript
    require('sp-init');
    require('microsoft-ajax');
    require('sp-runtime');
    require('sharepoint');
    ```

## <a name="load-localized-resources"></a><span data-ttu-id="8c55a-198">Загрузка локализованных ресурсов</span><span class="sxs-lookup"><span data-stu-id="8c55a-198">Load localized resources</span></span>

<span data-ttu-id="8c55a-199">В файле **config.json** есть схема **localizedResources**, с помощью которой можно описать, как загружать локализованные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8c55a-199">You can use a map in **config.json** called **localizedResources** to describe how to load localized resources.</span></span> <span data-ttu-id="8c55a-200">Пути в этой схеме заданы относительно папки **lib** и не должны содержать начальную косую черту (**/**).</span><span class="sxs-lookup"><span data-stu-id="8c55a-200">There is a map in config.json called localizedResources with which you can describe how to load localized resources. Paths in this map are relative to the **lib** folder and must not contain a leading slash (**/**).</span></span>

<span data-ttu-id="8c55a-p123">В этом примере у вас есть папка **src/strings/**. В этой папке несколько файлов JavaScript, таких как **en-us.js**, **fr-fr.js**, **de-de.js**. Так как каждый из этих файлов должен загружаться загрузчиком модулей, они должны содержать оберточный код CommonJS. Например, в случае файла **en-us.js**:</span><span class="sxs-lookup"><span data-stu-id="8c55a-p123">In this example, you have a folder **src/strings/**. In this folder are several JavaScript files with names such as **en-us.js**, **fr-fr.js**, **de-de.js**. Because each of these files must be loadable by the module loader, they must contain a CommonJS wrapper. For example, in **en-us.js**:</span></span>

```typescript
  define([], function() {
    return {
      "PropertyPaneDescription": "Description",
      "BasicGroupName": "Group Name",
      "DescriptionFieldLabel": "Description Field"
    }
  });
```

<br/>

1. <span data-ttu-id="8c55a-205">Измените файл **config.json**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-205">Edit the **config.json** file.</span></span> <span data-ttu-id="8c55a-206">Добавьте запись в схему **localizedResources**.</span><span class="sxs-lookup"><span data-stu-id="8c55a-206">Add an entry to **localizedResources**.</span></span> <span data-ttu-id="8c55a-207">`{locale}` — это замещающий токен для имени языкового стандарта.</span><span class="sxs-lookup"><span data-stu-id="8c55a-207">`{locale}` is a placeholder token for the locale name:</span></span>

    ```json
    {
        "strings": "strings/{locale}.js"
    }
    ```

2. <span data-ttu-id="8c55a-p125">Добавьте определения типов для строк. В этом случае у вас есть файл **MyStrings.d.ts**:</span><span class="sxs-lookup"><span data-stu-id="8c55a-p125">Add typings for your strings. In this case, you have a file **MyStrings.d.ts**:</span></span>

    ```typescript
    declare interface IStrings {
        webpartTitle: string;
        initialPrompt: string;
        exitPrompt: string;
    }

    declare module 'mystrings' {
        const strings: IStrings;
        export = strings;
    }
    ```

3. <span data-ttu-id="8c55a-210">Добавьте операции импорта для строк в проекте:</span><span class="sxs-lookup"><span data-stu-id="8c55a-210">Add imports for the strings in your project:</span></span>

    ```typescript
    import * as strings from 'mystrings';
    ```

4. <span data-ttu-id="8c55a-211">Используйте строки в своем проекте:</span><span class="sxs-lookup"><span data-stu-id="8c55a-211">Use the strings in your project:</span></span>

    ```typescript
    alert(strings.initialPrompt);
    ```

## <a name="see-also"></a><span data-ttu-id="8c55a-212">См. также</span><span class="sxs-lookup"><span data-stu-id="8c55a-212">See also</span></span>

- [<span data-ttu-id="8c55a-213">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="8c55a-213">SharePoint Framework Extensions Overview</span></span>](../../sharepoint-framework-overview.md)