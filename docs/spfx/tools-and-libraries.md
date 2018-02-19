---
title: "Библиотеки и средства разработки платформы SharePoint Framework"
description: "Сборка решений и разработка клиентских веб-частей с помощью клиентских библиотек JavaScript."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 5c256aae2c4fb4453f1b6a2b5fb4e91ede8ce78f
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="sharepoint-framework-development-tools-and-libraries"></a><span data-ttu-id="f9584-103">Библиотеки и средства разработки платформы SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f9584-103">SharePoint Framework development tools and libraries</span></span>

<span data-ttu-id="f9584-p101">Платформа SharePoint Framework включает несколько клиентских библиотек JavaScript, которые можно использовать для создания решений. В этой статье рассмотрены инструменты и библиотеки, которые можно использовать для разработки клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="f9584-p101">The SharePoint Framework includes several client-side JavaScript libraries that you can use to build your solutions. This article provides an overview of the tools and libraries that you can use to develop client-side web parts.</span></span>

## <a name="typescript"></a><span data-ttu-id="f9584-106">TypeScript</span><span class="sxs-lookup"><span data-stu-id="f9584-106">TypeScript</span></span>

<span data-ttu-id="f9584-p102">TypeScript — это типизированная расширенная версия языка JavaScript. Код TypeScript компилируется в обычный JavaScript. Клиентские средства разработки для SharePoint основаны на классах, модулях и интерфейсах TypeScript. С их помощью можно создавать надежные клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="f9584-p102">TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. SharePoint client-side development tools are built using TypeScript classes, modules, and interfaces. You can use these to build robust client-side web parts.</span></span> 

<span data-ttu-id="f9584-110">Чтобы начать работу с TypeScript, ознакомьтесь со следующими ресурсами:</span><span class="sxs-lookup"><span data-stu-id="f9584-110">To get started with TypeScript, see the following resources:</span></span>

* <span data-ttu-id="f9584-111">[краткое руководство по TypeScript](https://www.typescriptlang.org/docs/tutorial.html);</span><span class="sxs-lookup"><span data-stu-id="f9584-111">[TypeScript Quick Start](https://www.typescriptlang.org/docs/tutorial.html)</span></span>
* <span data-ttu-id="f9584-112">[интерактивная среда TypeScript](https://www.typescriptlang.org/play/index.html);</span><span class="sxs-lookup"><span data-stu-id="f9584-112">[TypeScript Playground](https://www.typescriptlang.org/play/index.html)</span></span>
* <span data-ttu-id="f9584-113">[справочник по TypeScript](https://www.typescriptlang.org/docs/handbook/basic-types.html);</span><span class="sxs-lookup"><span data-stu-id="f9584-113">[TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/basic-types.html)</span></span>
* <span data-ttu-id="f9584-114">[сообщество, посвященное TypeScript, на Stack Overflow](https://stackoverflow.com/questions/tagged/typescript).</span><span class="sxs-lookup"><span data-stu-id="f9584-114">[TypeScript community on Stack Overflow](https://stackoverflow.com/questions/tagged/typescript)</span></span>

## <a name="javascript-frameworks"></a><span data-ttu-id="f9584-115">Платформы JavaScript</span><span class="sxs-lookup"><span data-stu-id="f9584-115">JavaScript frameworks</span></span>
<span data-ttu-id="f9584-p103">Для разработки клиентских веб-частей можно выбрать любую из нескольких платформ JavaScript. Вот самые популярные из них:</span><span class="sxs-lookup"><span data-stu-id="f9584-p103">You can choose any one of a number of JavaScript frameworks to develop client-side web parts. The following are some of the most popular:</span></span>

* <span data-ttu-id="f9584-118">[React](https://facebook.github.io/react/);</span><span class="sxs-lookup"><span data-stu-id="f9584-118">[React](https://facebook.github.io/react/)</span></span>
* <span data-ttu-id="f9584-119">[AngularJS 1.x](https://docs.angularjs.org/tutorial);</span><span class="sxs-lookup"><span data-stu-id="f9584-119">[AngularJS 1.x](https://docs.angularjs.org/tutorial)</span></span>
* <span data-ttu-id="f9584-120">[Angular 2 для TypeScript 2.x](https://angular.io/guide/quickstart);</span><span class="sxs-lookup"><span data-stu-id="f9584-120">[Angular 2 for TypeScript 2.x](https://angular.io/guide/quickstart)</span></span>
* <span data-ttu-id="f9584-121">[Handlebars](http://handlebarsjs.com/).</span><span class="sxs-lookup"><span data-stu-id="f9584-121">[Handlebars](http://handlebarsjs.com/)</span></span>

<span data-ttu-id="f9584-p104">Так как клиентские веб-части — это компоненты, которые перетаскиваются на страницу SharePoint, рекомендуем выбрать платформу JavaScript, поддерживающую модель подобных компонентов. Все упрощенные платформы, такие как React, Handlebars и Angular 2, поддерживают модель компонентов и прекрасно подходят для создания клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="f9584-p104">Because client-side web parts are components that are dropped into a SharePoint page, we recommend that you choose a JavaScript framework that supports a similar component model. Lightweight frameworks such as React, Handlebars, and Angular 2 all support a component model and are well suited to building client-side web parts.</span></span> 

<span data-ttu-id="f9584-124">Рекомендуем также ознакомиться с [основной библиотекой JavaScript PnP для SharePoint](https://github.com/SharePoint/PnP-JS-Core), которая создана сообществом для простого доступа к REST API для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f9584-124">We also recommend you to have a look on [SharePoint PnP JavaScript Core library](https://github.com/SharePoint/PnP-JS-Core), which is a community driven effort targeted for providing easy access on SharePoint REST APIs.</span></span> 

## <a name="node-package-manager-npm"></a><span data-ttu-id="f9584-125">Диспетчер пакетов npm</span><span class="sxs-lookup"><span data-stu-id="f9584-125">Node Package Manager (npm)</span></span>

<span data-ttu-id="f9584-p105">Средства клиентской разработки для SharePoint позволяют использовать диспетчер пакетов [npm](https://www.npmjs.com/), который похож на [NuGet](https://www.nuget.org/), для управления зависимостями и другими необходимыми вспомогательными элементами JavaScript. Этот диспетчер обычно устанавливается вместе с Node.js.</span><span class="sxs-lookup"><span data-stu-id="f9584-p105">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager, which is similar to [NuGet](https://www.nuget.org/), to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="f9584-128">Дополнительные сведения о npm см. в соответствующей [документации](https://docs.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="f9584-128">For more information about npm, see the [npm documentation](https://docs.npmjs.com/).</span></span>

## <a name="nodejs"></a><span data-ttu-id="f9584-129">Node.js</span><span class="sxs-lookup"><span data-stu-id="f9584-129">Node.js</span></span>

<span data-ttu-id="f9584-130">Node.js — это кроссплатформенная среда выполнения с открытым кодом для размещения кода JavaScript и работы с ним.</span><span class="sxs-lookup"><span data-stu-id="f9584-130">Node.js is an open source, cross-platform runtime environment for hosting and serving JavaScript code.</span></span> <span data-ttu-id="f9584-131">Вы можете использовать Node.js для разработки серверных веб-приложений на JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f9584-131">You can use Node.js to develop server-side web applications written in JavaScript.</span></span> <span data-ttu-id="f9584-132">Экосистема Node.js, npm и средств запуска задач, таких как gulp, — это эффективная среда для создания приложений на JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f9584-132">The Node.js ecosystem is tightly coupled with npm and task runners such as gulp to provide an efficient environment for building JavaScript-based applications.</span></span> <span data-ttu-id="f9584-133">Платформа Node.js подобна IIS Express или IIS, но включает также средства, которые упрощают клиентскую разработку.</span><span class="sxs-lookup"><span data-stu-id="f9584-133">Node.js is similar to IIS Express or IIS, but includes tools to simplify client-side development.</span></span> 

<span data-ttu-id="f9584-134">Дополнительные сведения о Node.js:</span><span class="sxs-lookup"><span data-stu-id="f9584-134">For more information about Node.js, see the following:</span></span>

* <span data-ttu-id="f9584-135">[сведения о Node.js](https://nodejs.org/en/about/);</span><span class="sxs-lookup"><span data-stu-id="f9584-135">[About Node.js](https://nodejs.org/en/about/)</span></span>
* <span data-ttu-id="f9584-136">[справочная документация по API Node.js](https://nodejs.org/api/);</span><span class="sxs-lookup"><span data-stu-id="f9584-136">[Node.js API reference documentation](https://nodejs.org/api/)</span></span>
* <span data-ttu-id="f9584-137">[примеры использования Node.js](https://nodejs.org/api/synopsis.html).</span><span class="sxs-lookup"><span data-stu-id="f9584-137">[Node.js Usage and Example](https://nodejs.org/api/synopsis.html)</span></span>

## <a name="gulp-task-runner"></a><span data-ttu-id="f9584-138">Средство запуска задач Gulp</span><span class="sxs-lookup"><span data-stu-id="f9584-138">Gulp task runner</span></span>
<span data-ttu-id="f9584-139">Средства клиентской разработки для SharePoint позволяют использовать [Gulp](http://gulpjs.com/) в качестве средства запуска таких задач по сборке, как:</span><span class="sxs-lookup"><span data-stu-id="f9584-139">SharePoint client-side development tools use [gulp](http://gulpjs.com/) as the build process task runner to:</span></span>

* <span data-ttu-id="f9584-140">добавление в пакет и минификация файлов JavaScript и CSS;</span><span class="sxs-lookup"><span data-stu-id="f9584-140">Bundle and minify JavaScript and CSS files.</span></span>
* <span data-ttu-id="f9584-141">запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;</span><span class="sxs-lookup"><span data-stu-id="f9584-141">Run tools to call the bundling and minification tasks before each build.</span></span>
* <span data-ttu-id="f9584-142">компиляция файлов LESS или SASS в CSS;</span><span class="sxs-lookup"><span data-stu-id="f9584-142">Compile LESS or SASS files to CSS.</span></span>
* <span data-ttu-id="f9584-143">компиляция файлов TypeScript в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f9584-143">Compile TypeScript files to JavaScript.</span></span>

<span data-ttu-id="f9584-144">Дополнительные сведения о Gulp:</span><span class="sxs-lookup"><span data-stu-id="f9584-144">For more information about gulp, see the following:</span></span>

* <span data-ttu-id="f9584-145">[информация для начала работы с Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md);</span><span class="sxs-lookup"><span data-stu-id="f9584-145">[Getting started with Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)</span></span>
* <span data-ttu-id="f9584-146">[TypeScript и Gulp](https://www.typescriptlang.org/docs/handbook/gulp.html);</span><span class="sxs-lookup"><span data-stu-id="f9584-146">[TypeScript and Gulp](https://www.typescriptlang.org/docs/handbook/gulp.html)</span></span>
* <span data-ttu-id="f9584-147">[статьи о Gulp](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles).</span><span class="sxs-lookup"><span data-stu-id="f9584-147">[Articles about Gulp](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles)</span></span>

## <a name="webpack"></a><span data-ttu-id="f9584-148">Webpack</span><span class="sxs-lookup"><span data-stu-id="f9584-148">Webpack</span></span>

<span data-ttu-id="f9584-149">Webpack — это средство, которое создает один или несколько пакетов JavaScript из файлов веб-частей и зависимостей, что позволяет загружать различные пакеты для разных сценариев.</span><span class="sxs-lookup"><span data-stu-id="f9584-149">Webpack is a module bundler that takes your web part files an dependencies and generates one or more JavaScript bundles so you can load different bundles for different scenarios.</span></span>

<span data-ttu-id="f9584-p107">Набором средств разработки для объединения используется [CommonJS](https://webpack.js.org/). Это позволяет определить модули и место их использования. Цепочка инструментов использует [SystemJS](https://github.com/systemjs/systemjs), универсальный загрузчик модулей. Это позволяет определить области для веб-частей, так как обеспечивает выполнение каждой веб-части в отдельном пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="f9584-p107">The development tool chain uses [CommonJS](https://webpack.js.org/) for bundling. This enables you to define modules and where you want to use them. The tool chain also uses [SystemJS](https://github.com/systemjs/systemjs), a universal module loader, to load your modules. This helps you to scope your web parts by making sure that each web part is executed in its own namespace.</span></span>

<span data-ttu-id="f9584-154">Дополнительные сведения о Webpack:</span><span class="sxs-lookup"><span data-stu-id="f9584-154">For more information about webpack, see the following:</span></span>

* [<span data-ttu-id="f9584-155">Документация по Webpack</span><span class="sxs-lookup"><span data-stu-id="f9584-155">Webpack documentation</span></span>](https://webpack.js.org/)
* [<span data-ttu-id="f9584-156">TypeScript, React и Webpack</span><span class="sxs-lookup"><span data-stu-id="f9584-156">TypeScript, React, and Webpack</span></span>](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html)

## <a name="yeoman-generators"></a><span data-ttu-id="f9584-157">Генераторы Yeoman</span><span class="sxs-lookup"><span data-stu-id="f9584-157">Yeoman generators</span></span>

<span data-ttu-id="f9584-158">[Yeoman](http://yeoman.io/) помогает начинать новые проекты, предоставляя рекомендации и инструменты для продуктивной работы.</span><span class="sxs-lookup"><span data-stu-id="f9584-158">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="f9584-159">Генератор Yeoman для SharePoint входит в состав платформы и позволяет создавать новые клиентские веб-части.</span><span class="sxs-lookup"><span data-stu-id="f9584-159">The Yeoman SharePoint generator is available as part of the framework to kickstart new client-side web part projects.</span></span> 

<span data-ttu-id="f9584-160">Дополнительные сведения о Yeoman см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f9584-160">For more information about Yeoman, see the following:</span></span>

* [<span data-ttu-id="f9584-161">Скаффолдинг веб-приложения с помощью Yeoman</span><span class="sxs-lookup"><span data-stu-id="f9584-161">Scaffold a web app with Yeoman</span></span>](http://yeoman.io/codelab/index.html)
* [<span data-ttu-id="f9584-162">Список доступных генераторов Yeoman</span><span class="sxs-lookup"><span data-stu-id="f9584-162">List of available Yeoman generators</span></span>](http://yeoman.io/generators/)
* [<span data-ttu-id="f9584-163">Скаффолдинг проектов с помощью генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f9584-163">Scaffold projects using yeoman SharePoint generator</span></span>](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md)

<span data-ttu-id="f9584-164">Вы можете воспользоваться одним из следующих генераторов Yeoman, в зависимости от выбранной платформы:</span><span class="sxs-lookup"><span data-stu-id="f9584-164">The following are some common Yeoman generators that you can try, depending on your choice of framework:</span></span>

* <span data-ttu-id="f9584-165">[generator-react-webpack](https://github.com/react-webpack-generators/generator-react-webpack);</span><span class="sxs-lookup"><span data-stu-id="f9584-165">[generator-react-webpack](https://github.com/react-webpack-generators/generator-react-webpack)</span></span>
* <span data-ttu-id="f9584-166">[generator-angular](https://www.npmjs.com/package/generator-angular).</span><span class="sxs-lookup"><span data-stu-id="f9584-166">[generator-angular](https://www.npmjs.com/package/generator-angular)</span></span>

## <a name="source-code-editors"></a><span data-ttu-id="f9584-167">Редакторы исходного кода</span><span class="sxs-lookup"><span data-stu-id="f9584-167">Source code editors</span></span>

<span data-ttu-id="f9584-168">SharePoint Framework — клиентская платформа, поэтому вы можете выбрать удобный для себя редактор кода HTML или JavaScript, например:</span><span class="sxs-lookup"><span data-stu-id="f9584-168">SharePoint Framework is client-side driven and thus you can use your choice of HTML/JavaScript code editors, such as:</span></span>

* <span data-ttu-id="f9584-169">[Visual Studio Code](https://code.visualstudio.com/);</span><span class="sxs-lookup"><span data-stu-id="f9584-169">[Visual Studio Code](https://code.visualstudio.com/)</span></span>
* <span data-ttu-id="f9584-170">[Atom](https://atom.io);</span><span class="sxs-lookup"><span data-stu-id="f9584-170">[Atom](https://atom.io)</span></span>
* <span data-ttu-id="f9584-171">[Webstorm](https://www.jetbrains.com/webstorm).</span><span class="sxs-lookup"><span data-stu-id="f9584-171">[Webstorm](https://www.jetbrains.com/webstorm)</span></span>

<span data-ttu-id="f9584-172">В примерах, приведенных в документации по SharePoint Framework, используется Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f9584-172">SharePoint Framework documentation uses Visual Studio code in the steps and examples.</span></span> <span data-ttu-id="f9584-173">Visual Studio Code — мощный редактор исходного кода от корпорации Майкрософт, который занимает мало места на диске и работает на компьютерах с Windows, Mac OS и Linux.</span><span class="sxs-lookup"><span data-stu-id="f9584-173">Visual Studio Code is a lightweight but powerful source code editor from Microsoft that runs on your desktop and is available for Windows, Mac, and Linux.</span></span> <span data-ttu-id="f9584-174">Он изначально поддерживает JavaScript, TypeScript и Node.js, а также предусматривает использование богатой экосистемы расширений для других языков (например, C++, C#, Python, PHP) и сред выполнения.</span><span class="sxs-lookup"><span data-stu-id="f9584-174">It comes with built-in support for JavaScript, TypeScript, and Node.js, and has a rich ecosystem of extensions for other languages (such as C++, C#, Python, PHP) and runtimes.</span></span>

## <a name="sharepoint-rest-apis"></a><span data-ttu-id="f9584-175">REST API SharePoint</span><span class="sxs-lookup"><span data-stu-id="f9584-175">SharePoint REST APIs</span></span>

<span data-ttu-id="f9584-p110">Платформа SharePoint Framework обеспечивает ключевые возможности интеграции с SharePoint и предназначена для веб-разработки. Интерфейсы REST API для SharePoint позволяют взаимодействовать с SharePoint и другими рабочими нагрузками, которые влияют на функциональность веб-части.</span><span class="sxs-lookup"><span data-stu-id="f9584-p110">The SharePoint Framework provides key integrations with SharePoint experiences and targets web development. The SharePoint REST APIs enable you to interact with  SharePoint and other workloads that shape your web part functionality.</span></span> 

<span data-ttu-id="f9584-178">Рекомендуем ознакомиться со следующими интерфейсами REST API:</span><span class="sxs-lookup"><span data-stu-id="f9584-178">We recommend that you become familiar with the following set of REST APIs:</span></span>

* <span data-ttu-id="f9584-179">[REST API для списков SharePoint](../sp-add-ins/working-with-lists-and-list-items-with-rest.md).</span><span class="sxs-lookup"><span data-stu-id="f9584-179">[SharePoint List REST APIs](../sp-add-ins/working-with-lists-and-list-items-with-rest.md)</span></span>

## <a name="patterns-and-practices"></a><span data-ttu-id="f9584-180">PnP (Patterns and Practices)</span><span class="sxs-lookup"><span data-stu-id="f9584-180">Patterns and Practices</span></span>

<span data-ttu-id="f9584-p111">Благодаря проекту [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) доступны примеры кодов, шаблоны и другие ресурсы, которые помогут преобразовать существующее решение в решение на базе SharePoint Framework. Обязательно ознакомьтесь с этими примерами кодов и рекомендациями.</span><span class="sxs-lookup"><span data-stu-id="f9584-p111">The [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) initiative provides code samples, patterns, and other resources to help you transform your existing solution to the SharePoint Framework. Be sure to become familiar with the code samples and guidance that is available through the PnP effort.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9584-183">См. также</span><span class="sxs-lookup"><span data-stu-id="f9584-183">See also</span></span>

- [<span data-ttu-id="f9584-184">Цепочка инструментов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f9584-184">SharePoint Framework Toolchain</span></span>](toolchain/sharepoint-framework-toolchain.md)
- [<span data-ttu-id="f9584-185">Создание клиентской веб-части Hello World</span><span class="sxs-lookup"><span data-stu-id="f9584-185">Build a Hello World client-side web part</span></span>](web-parts/get-started/build-a-hello-world-web-part.md)
- [<span data-ttu-id="f9584-186">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f9584-186">SharePoint Framework Overview</span></span>](sharepoint-framework-overview.md)
