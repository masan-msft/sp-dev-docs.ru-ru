---
title: "Библиотеки и средства разработки платформы SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a8a75e7161cce1de606161bd589042a9a38e26c4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-framework-development-tools-and-libraries"></a><span data-ttu-id="73e5d-102">Библиотеки и средства разработки платформы SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="73e5d-102">SharePoint Framework development tools and libraries</span></span>

<span data-ttu-id="73e5d-p101">Платформа SharePoint Framework включает несколько клиентских библиотек JavaScript, которые можно использовать для создания решений. В этой статье рассмотрены инструменты и библиотеки, которые можно использовать для разработки клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p101">The SharePoint Framework includes several client-side JavaScript libraries that you can use to build your solutions. This article provides an overview of the tools and libraries that you can use to develop client-side web parts.</span></span>

## <a name="typescript"></a><span data-ttu-id="73e5d-105">TypeScript</span><span class="sxs-lookup"><span data-stu-id="73e5d-105">TypeScript</span></span>
<span data-ttu-id="73e5d-p102">TypeScript — это типизированная расширенная версия языка JavaScript. Код TypeScript компилируется в обычный JavaScript. Клиентские средства разработки для SharePoint основаны на классах, модулях и интерфейсах TypeScript. С их помощью можно создавать надежные клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p102">TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. SharePoint client-side development tools are built using TypeScript classes, modules, and interfaces. You can use these to build robust client-side web parts.</span></span> 

<span data-ttu-id="73e5d-109">Чтобы начать работу с TypeScript, ознакомьтесь со следующими ресурсами:</span><span class="sxs-lookup"><span data-stu-id="73e5d-109">To get started with TypeScript, see the following resources:</span></span>

* <span data-ttu-id="73e5d-110">[краткое руководство по TypeScript](https://www.typescriptlang.org/docs/tutorial.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-110">[TypeScript Quick Start](https://www.typescriptlang.org/docs/tutorial.html)</span></span>
* <span data-ttu-id="73e5d-111">[интерактивная среда TypeScript](https://www.typescriptlang.org/play/index.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-111">[TypeScript Playground](https://www.typescriptlang.org/play/index.html)</span></span>
* <span data-ttu-id="73e5d-112">[справочник по TypeScript](https://www.typescriptlang.org/docs/handbook/basic-types.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-112">[TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/basic-types.html)</span></span>
* <span data-ttu-id="73e5d-113">[сообщество, посвященное TypeScript, на Stack Overflow](https://stackoverflow.com/questions/tagged/typescript).</span><span class="sxs-lookup"><span data-stu-id="73e5d-113">[TypeScript community on Stack Overflow](https://stackoverflow.com/questions/tagged/typescript)</span></span>

## <a name="javascript-frameworks"></a><span data-ttu-id="73e5d-114">Платформы JavaScript</span><span class="sxs-lookup"><span data-stu-id="73e5d-114">JavaScript frameworks</span></span>
<span data-ttu-id="73e5d-p103">Для разработки клиентских веб-частей можно выбрать любую из нескольких платформ JavaScript. Вот самые популярные из них:</span><span class="sxs-lookup"><span data-stu-id="73e5d-p103">You can choose any one of a number of JavaScript frameworks to develop client-side web parts. The following are some of the most popular:</span></span>

* <span data-ttu-id="73e5d-117">[React](https://facebook.github.io/react/);</span><span class="sxs-lookup"><span data-stu-id="73e5d-117">[React](https://facebook.github.io/react/)</span></span>
* <span data-ttu-id="73e5d-118">[AngularJS 1.x](https://docs.angularjs.org/tutorial);</span><span class="sxs-lookup"><span data-stu-id="73e5d-118">[AngularJS 1.x](https://docs.angularjs.org/tutorial)</span></span>
* <span data-ttu-id="73e5d-119">[Angular 2 для TypeScript 2.x](https://angular.io/docs/ts/latest/quickstart.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-119">[Angular 2 for TypeScript 2.x](https://angular.io/docs/ts/latest/quickstart.html)</span></span>
* <span data-ttu-id="73e5d-120">[Handlebars](http://handlebarsjs.com/).</span><span class="sxs-lookup"><span data-stu-id="73e5d-120">[Handlebars](http://handlebarsjs.com/)</span></span>

<span data-ttu-id="73e5d-p104">Так как клиентские веб-части — это компоненты, которые перетаскиваются на страницу SharePoint, рекомендуем выбрать платформу JavaScript, поддерживающую модель подобных компонентов. Все упрощенные платформы, такие как React, Handlebars и Angular 2, поддерживают модель компонентов и прекрасно подходят для создания клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p104">Because client-side web parts are components that are dropped into a SharePoint page, we recommend that you choose a JavaScript framework that supports a similar component model. Lightweight frameworks such as React, Handlebars, and Angular 2 all support a component model and are well suited to building client-side web parts.</span></span> 

<span data-ttu-id="73e5d-123">Рекомендуем также ознакомиться с [основной библиотекой JavaScript PnP для SharePoint](https://github.com/SharePoint/PnP-JS-Core), которая создана сообществом для простого доступа к REST API для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="73e5d-123">We also recommend you to have a look on [SharePoint PnP JavaScript Core library](https://github.com/SharePoint/PnP-JS-Core), which is a community driven effort targeted for providing easy access on SharePoint REST APIs.</span></span> 

## <a name="node-package-manager-npm"></a><span data-ttu-id="73e5d-124">Диспетчер пакетов npm</span><span class="sxs-lookup"><span data-stu-id="73e5d-124">Node Package Manager (npm)</span></span>

<span data-ttu-id="73e5d-p105">Средства клиентской разработки для SharePoint позволяют использовать диспетчер пакетов [npm](https://www.npmjs.com/), который похож на [NuGet](https://www.nuget.org/), для управления зависимостями и другими необходимыми вспомогательными элементами JavaScript. Этот диспетчер обычно устанавливается вместе с Node.js.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p105">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager, which is similar to [NuGet](https://www.nuget.org/), to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="73e5d-127">Дополнительные сведения о npm см. в соответствующей [документации](https://docs.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="73e5d-127">For more information about npm, see the [npm documentation](https://docs.npmjs.com/).</span></span>

## <a name="nodejs"></a><span data-ttu-id="73e5d-128">Node.js</span><span class="sxs-lookup"><span data-stu-id="73e5d-128">Node.js</span></span>

<span data-ttu-id="73e5d-p106">Node.js — это кроссплатформенная среда выполнения с открытым кодом для размещения кода JavaScript и работы с ним. С помощью Node.js можно разрабатывать серверные веб-приложения, написанные на JavaScript. Экосистема Node.js тесно связана с npm и средствами запуска задач, такими как gulp, для обеспечения доступа к эффективной среде создания приложений на JavaScript. Платформа Node.js подобна IIS Express или IIS, но включает также средства, которые упрощают клиентскую разработку.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p106">Node.js is an open source, cross-platform runtime environment for hosting and serving JavaScript code. You can use node.js develop server-side web applications written in JavaScript. The Node.js ecosystem is tightly coupled with npm and task runners such as gulp to provide an efficient environment for building JavaScript-based applications. Node.js is similar to IIS Express or IIS, but includes tools to simplify client-side development.</span></span> 

<span data-ttu-id="73e5d-133">Дополнительные сведения о Node.js:</span><span class="sxs-lookup"><span data-stu-id="73e5d-133">For more information about Node.js, see the following:</span></span>

* <span data-ttu-id="73e5d-134">[сведения о Node.js](https://nodejs.org/en/about/);</span><span class="sxs-lookup"><span data-stu-id="73e5d-134">[About Node.js](https://nodejs.org/en/about/)</span></span>
* <span data-ttu-id="73e5d-135">[справочная документация по API Node.js](https://nodejs.org/api/);</span><span class="sxs-lookup"><span data-stu-id="73e5d-135">[Node.js API reference documentation](https://nodejs.org/api/)</span></span>
* <span data-ttu-id="73e5d-136">[примеры использования Node.js](https://nodejs.org/api/synopsis.html).</span><span class="sxs-lookup"><span data-stu-id="73e5d-136">[Node.js Usage and Example](https://nodejs.org/api/synopsis.html)</span></span>

## <a name="gulp-task-runner"></a><span data-ttu-id="73e5d-137">Средство запуска задач Gulp</span><span class="sxs-lookup"><span data-stu-id="73e5d-137">Gulp task runner</span></span>
<span data-ttu-id="73e5d-138">Средства клиентской разработки для SharePoint позволяют использовать [Gulp](http://gulpjs.com/) в качестве средства запуска таких задач по сборке, как:</span><span class="sxs-lookup"><span data-stu-id="73e5d-138">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="73e5d-139">добавление в пакет и минификация файлов JavaScript и CSS;</span><span class="sxs-lookup"><span data-stu-id="73e5d-139">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="73e5d-140">запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;</span><span class="sxs-lookup"><span data-stu-id="73e5d-140">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="73e5d-141">компиляция файлов LESS или SASS в CSS;</span><span class="sxs-lookup"><span data-stu-id="73e5d-141">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="73e5d-142">компиляция файлов TypeScript в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="73e5d-142">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="73e5d-143">Дополнительные сведения о Gulp:</span><span class="sxs-lookup"><span data-stu-id="73e5d-143">For more information about gulp, see the following:</span></span>

* <span data-ttu-id="73e5d-144">[информация для начала работы с Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md);</span><span class="sxs-lookup"><span data-stu-id="73e5d-144">[Getting started with Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)</span></span>
* <span data-ttu-id="73e5d-145">[TypeScript и Gulp](https://www.typescriptlang.org/docs/handbook/gulp.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-145">[TypeScript and Gulp](https://www.typescriptlang.org/docs/handbook/gulp.html)</span></span>
* <span data-ttu-id="73e5d-146">[статьи о Gulp](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles).</span><span class="sxs-lookup"><span data-stu-id="73e5d-146">[Articles about Gulp](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles)</span></span>

## <a name="webpack"></a><span data-ttu-id="73e5d-147">Webpack</span><span class="sxs-lookup"><span data-stu-id="73e5d-147">Webpack</span></span>

<span data-ttu-id="73e5d-148">Webpack — это средство увязки модулей в пакеты, которое создает один или несколько пакетов JavaScript из файлов веб-частей и зависимостей, благодаря чему можно загрузить различные пакеты для разных сценариев.</span><span class="sxs-lookup"><span data-stu-id="73e5d-148">Webpack is a module bundler that takes your web part files an dependencies and generates one or more JavaScript bundles so you can load different bundles for different scenarios.</span></span>

<span data-ttu-id="73e5d-p107">Набором средств разработки для объединения используется [CommonJS](https://webpack.github.io/docs/commonjs.html). Это позволяет определить модули и место их использования. Цепочка инструментов использует [SystemJS](https://github.com/systemjs/systemjs), универсальный загрузчик модулей. Это позволяет определить области для веб-частей, так как обеспечивает выполнение каждой веб-части в отдельном пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p107">The development tool chain uses [CommonJS](https://webpack.github.io/docs/commonjs.html) for bundling. This enables you to define modules and where you want to use them. The tool chain also uses [SystemJS](https://github.com/systemjs/systemjs), a universal module loader, to load your modules. This helps you to scope your web parts by making sure that each web part is executed in its own namespace.</span></span>

<span data-ttu-id="73e5d-153">Дополнительные сведения о Webpack:</span><span class="sxs-lookup"><span data-stu-id="73e5d-153">For more information about webpack, see the following:</span></span>

* <span data-ttu-id="73e5d-154">[документация по Webpack](http://webpack.github.io/docs/what-is-webpack.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-154">[Webpack documentation](http://webpack.github.io/docs/what-is-webpack.html)</span></span>
* <span data-ttu-id="73e5d-155">[TypeScript, React и Webpack](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html).</span><span class="sxs-lookup"><span data-stu-id="73e5d-155">[TypeScript, React, and Webpack](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)</span></span>

## <a name="yeoman-generators"></a><span data-ttu-id="73e5d-156">Генераторы Yeoman</span><span class="sxs-lookup"><span data-stu-id="73e5d-156">Yeoman generators</span></span>
<span data-ttu-id="73e5d-p108">[Yeoman](http://yeoman.io/) помогает эффективно запускать новые проекты благодаря соответствующим рекомендациям и инструментам. Генератор Yeoman для SharePoint будет доступен в качестве компонента платформы для запуска новых проектов клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p108">[Yeoman](http://yeoman.io/) helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. SharePoint Yeoman generator will be available as part of the framework to kickstart new client-side web part projects.</span></span> 

<span data-ttu-id="73e5d-159">Дополнительные сведения о Yeoman см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="73e5d-159">For more information about Yeoman, see the following:</span></span>

* <span data-ttu-id="73e5d-160">[Скаффолдинг веб-приложения с помощью Yeoman](http://yeoman.io/codelab/index.html);</span><span class="sxs-lookup"><span data-stu-id="73e5d-160">[Scaffold a web app with Yeoman](http://yeoman.io/codelab/index.html)</span></span>
* <span data-ttu-id="73e5d-161">[Список доступных генераторов Yeoman](http://yeoman.io/generators/).</span><span class="sxs-lookup"><span data-stu-id="73e5d-161">[List of available Yeoman generators](http://yeoman.io/generators/)</span></span>

<span data-ttu-id="73e5d-162">Вот некоторые популярные генераторы Yeoman, подходящие для определенной платформы:</span><span class="sxs-lookup"><span data-stu-id="73e5d-162">The following are some common Yeoman generators that you can try, depending on your choice of framework:</span></span>

* <span data-ttu-id="73e5d-163">[generator-react-webpack](https://github.com/newtriks/generator-react-webpack);</span><span class="sxs-lookup"><span data-stu-id="73e5d-163">[generator-react-webpack](https://github.com/newtriks/generator-react-webpack)</span></span>
* <span data-ttu-id="73e5d-164">[generator-angular](https://www.npmjs.com/package/generator-angular).</span><span class="sxs-lookup"><span data-stu-id="73e5d-164">[generator-angular](https://www.npmjs.com/package/generator-angular)</span></span>

## <a name="source-code-editors"></a><span data-ttu-id="73e5d-165">Редакторы исходного кода</span><span class="sxs-lookup"><span data-stu-id="73e5d-165">Source code editors</span></span>
<span data-ttu-id="73e5d-166">SharePoint Framework — клиентская платформа, поэтому вы можете выбрать удобный для себя редактор кода HTML или JavaScript, например:</span><span class="sxs-lookup"><span data-stu-id="73e5d-166">SharePoint Framework is client-side driven and thus you can use your choice of HTML/JavaScript code editors, such as:</span></span>

* <span data-ttu-id="73e5d-167">[Visual Studio Code](https://code.visualstudio.com/);</span><span class="sxs-lookup"><span data-stu-id="73e5d-167">[Visual Studio Code](https://code.visualstudio.com/)</span></span>
* <span data-ttu-id="73e5d-168">[Atom](https://atom.io);</span><span class="sxs-lookup"><span data-stu-id="73e5d-168">[Atom](https://atom.io)</span></span>
* <span data-ttu-id="73e5d-169">[Webstorm](https://www.jetbrains.com/webstorm).</span><span class="sxs-lookup"><span data-stu-id="73e5d-169">[Webstorm](https://www.jetbrains.com/webstorm)</span></span>

<span data-ttu-id="73e5d-p109">В примерах, приведенных в документации по SharePoint Framework, указывается Visual Studio Code. Visual Studio Code — мощный редактор исходного кода, предложенный корпорацией Майкрософт, который занимает мало места на диске и работает на компьютерах с Windows, Mac OS или Linux. Он изначально поддерживает JavaScript, TypeScript и Node.js, а также предусматривает использование богатой экосистемы расширений для других языков (например, C++, C#, Python, PHP) и сред выполнения.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p109">SharePoint Framework documentation uses Visual Studio code in the docs and examples. Visual Studio Code is a lightweight but powerful source code editor from Microsoft which runs on your desktop and is available for Windows, Mac and Linux. It comes with built-in support for JavaScript, TypeScript and Node.js and has a rich ecosystem of extensions for other languages (such as C++, C#, Python, PHP) and runtimes.</span></span>

## <a name="sharepoint-rest-apis"></a><span data-ttu-id="73e5d-173">Интерфейсы REST API для SharePoint</span><span class="sxs-lookup"><span data-stu-id="73e5d-173">SharePoint REST APIs</span></span>

<span data-ttu-id="73e5d-p110">Платформа SharePoint Framework обеспечивает ключевые возможности интеграции с SharePoint и предназначена для веб-разработки. Интерфейсы REST API для SharePoint позволяют взаимодействовать с SharePoint и другими рабочими нагрузками, которые влияют на функциональность веб-части.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p110">The SharePoint Framework provides key integrations with SharePoint experiences and targets web development. The SharePoint REST APIs enable you to interact with  SharePoint and other workloads that shape your web part functionality.</span></span> 

<span data-ttu-id="73e5d-176">Рекомендуем ознакомиться со следующими интерфейсами REST API:</span><span class="sxs-lookup"><span data-stu-id="73e5d-176">We recommend that you become familiar with the following set of REST APIs:</span></span>

* <span data-ttu-id="73e5d-177">[REST API для списков SharePoint](https://msdn.microsoft.com/ru-RU/library/office/dn292552.aspx).</span><span class="sxs-lookup"><span data-stu-id="73e5d-177">[SharePoint List REST APIs](https://msdn.microsoft.com/ru-RU/library/office/dn292552.aspx)</span></span>

## <a name="patterns-and-practices"></a><span data-ttu-id="73e5d-178">PnP (Patterns and Practices)</span><span class="sxs-lookup"><span data-stu-id="73e5d-178">Patterns and Practices</span></span>

<span data-ttu-id="73e5d-p111">Благодаря проекту [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) доступны примеры кодов, шаблоны и другие ресурсы, которые помогут преобразовать существующее решение в решение на базе SharePoint Framework. Обязательно ознакомьтесь с этими примерами кодов и рекомендациями.</span><span class="sxs-lookup"><span data-stu-id="73e5d-p111">The [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) initiative provides code samples, patterns, and other resources to help you transform your existing solution to the SharePoint Framework. Be sure to become familiar with the code samples and guidance that is available through the PnP effort.</span></span>

## <a name="see-also"></a><span data-ttu-id="73e5d-181">См. также</span><span class="sxs-lookup"><span data-stu-id="73e5d-181">See also</span></span>

* [<span data-ttu-id="73e5d-182">SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="73e5d-182">SharePoint Framework</span></span>](sharepoint-framework-overview.md)
* [<span data-ttu-id="73e5d-183">Создание клиентской веб-части Hello World</span><span class="sxs-lookup"><span data-stu-id="73e5d-183">Build a Hello World client-side web part</span></span>](web-parts/get-started/build-a-hello-world-web-part.md)
