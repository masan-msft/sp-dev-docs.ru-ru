# <a name="sharepoint-framework-development-tools-and-libraries"></a>Библиотеки и средства разработки платформы SharePoint Framework

Платформа SharePoint Framework включает несколько клиентских библиотек JavaScript, которые можно использовать для создания решений. В этой статье рассмотрены инструменты и библиотеки, которые можно использовать для разработки клиентских веб-частей.

## <a name="typescript"></a>TypeScript
TypeScript — это типизированная расширенная версия языка JavaScript. Код TypeScript компилируется в обычный JavaScript. Клиентские средства разработки для SharePoint основаны на классах, модулях и интерфейсах TypeScript. С их помощью можно создавать надежные клиентские веб-части. 

Чтобы начать работу с TypeScript, ознакомьтесь со следующими ресурсами:

* [краткое руководство по TypeScript](https://www.typescriptlang.org/docs/tutorial.html);
* [интерактивная среда TypeScript](https://www.typescriptlang.org/play/index.html);
* [справочник по TypeScript](https://www.typescriptlang.org/docs/handbook/basic-types.html);
* [сообщество, посвященное TypeScript, на Stack Overflow](https://stackoverflow.com/questions/tagged/typescript).

## <a name="javascript-frameworks"></a>Платформы JavaScript
Для разработки клиентских веб-частей можно выбрать любую из нескольких платформ JavaScript. Вот самые популярные из них:

* [React](https://facebook.github.io/react/);
* [AngularJS 1.x](https://docs.angularjs.org/tutorial);
* [Angular 2 для TypeScript 2.x](https://angular.io/docs/ts/latest/quickstart.html);
* [Handlebars](http://handlebarsjs.com/).

Так как клиентские веб-части — это компоненты, которые перетаскиваются на страницу SharePoint, рекомендуем выбрать платформу JavaScript, поддерживающую модель подобных компонентов. Все упрощенные платформы, такие как React, Handlebars и Angular 2, поддерживают модель компонентов и прекрасно подходят для создания клиентских веб-частей. 

Рекомендуем также ознакомиться с [основной библиотекой JavaScript PnP для SharePoint](https://github.com/SharePoint/PnP-JS-Core), которая создана сообществом для простого доступа к REST API для SharePoint. 

## <a name="node-package-manager-npm"></a>Диспетчер пакетов npm

Средства клиентской разработки для SharePoint позволяют использовать диспетчер пакетов [npm](https://www.npmjs.com/), который похож на [NuGet](https://www.nuget.org/), для управления зависимостями и другими необходимыми вспомогательными элементами JavaScript. Этот диспетчер обычно устанавливается вместе с Node.js.

Дополнительные сведения о npm см. в соответствующей [документации](https://docs.npmjs.com/).

## <a name="nodejs"></a>Node.js

Node.js — это кроссплатформенная среда выполнения с открытым кодом для размещения кода JavaScript и работы с ним. С помощью Node.js можно разрабатывать серверные веб-приложения, написанные на JavaScript. Экосистема Node.js тесно связана с npm и средствами запуска задач, такими как gulp, для обеспечения доступа к эффективной среде создания приложений на JavaScript. Платформа Node.js подобна IIS Express или IIS, но включает также средства, которые упрощают клиентскую разработку. 

Дополнительные сведения о Node.js:

* [сведения о Node.js](https://nodejs.org/en/about/);
* [справочная документация по API Node.js](https://nodejs.org/api/);
* [примеры использования Node.js](https://nodejs.org/api/synopsis.html).

## <a name="gulp-task-runner"></a>Средство запуска задач Gulp
Средства клиентской разработки для SharePoint позволяют использовать [Gulp](http://gulpjs.com/) в качестве средства запуска таких задач по сборке, как:

* добавление в пакет и минификация файлов JavaScript и CSS;
* запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;
* компиляция файлов LESS или SASS в CSS;
* компиляция файлов TypeScript в JavaScript.

Дополнительные сведения о Gulp:

* [информация для начала работы с Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md);
* [TypeScript и Gulp](https://www.typescriptlang.org/docs/handbook/gulp.html);
* [статьи о Gulp](https://github.com/gulpjs/gulp/blob/master/docs/README.md#articles).

## <a name="webpack"></a>Webpack

Webpack — это средство увязки модулей в пакеты, которое создает один или несколько пакетов JavaScript из файлов веб-частей и зависимостей, благодаря чему можно загрузить различные пакеты для разных сценариев.

Набором средств разработки для объединения используется [CommonJS](https://webpack.github.io/docs/commonjs.html). Это позволяет определить модули и место их использования. Цепочка инструментов использует [SystemJS](https://github.com/systemjs/systemjs), универсальный загрузчик модулей. Это позволяет определить области для веб-частей, так как обеспечивает выполнение каждой веб-части в отдельном пространстве имен.

Дополнительные сведения о Webpack:

* [документация по Webpack](http://webpack.github.io/docs/what-is-webpack.html);
* [TypeScript, React и Webpack](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html).

## <a name="yeoman-generators"></a>Генераторы Yeoman
[Yeoman](http://yeoman.io/) помогает эффективно запускать новые проекты благодаря соответствующим рекомендациям и инструментам. Генератор Yeoman для SharePoint будет доступен в качестве компонента платформы для запуска новых проектов клиентских веб-частей. 

Дополнительные сведения о Yeoman см. в следующих статьях:

* [Скаффолдинг веб-приложения с помощью Yeoman](http://yeoman.io/codelab/index.html);
* [Список доступных генераторов Yeoman](http://yeoman.io/generators/).

Вот некоторые популярные генераторы Yeoman, подходящие для определенной платформы:

* [generator-react-webpack](https://github.com/newtriks/generator-react-webpack);
* [generator-angular](https://www.npmjs.com/package/generator-angular).

## <a name="source-code-editors"></a>Редакторы исходного кода
SharePoint Framework — клиентская платформа, поэтому вы можете выбрать удобный для себя редактор кода HTML или JavaScript, например:

* [Visual Studio Code](https://code.visualstudio.com/);
* [Atom](https://atom.io);
* [Webstorm](https://www.jetbrains.com/webstorm).

В примерах, приведенных в документации по SharePoint Framework, указывается Visual Studio Code. Visual Studio Code — мощный редактор исходного кода, предложенный корпорацией Майкрософт, который занимает мало места на диске и работает на компьютерах с Windows, Mac OS или Linux. Он изначально поддерживает JavaScript, TypeScript и Node.js, а также предусматривает использование богатой экосистемы расширений для других языков (например, C++, C#, Python, PHP) и сред выполнения.

## <a name="sharepoint-rest-apis"></a>Интерфейсы REST API для SharePoint

Платформа SharePoint Framework обеспечивает ключевые возможности интеграции с SharePoint и предназначена для веб-разработки. Интерфейсы REST API для SharePoint позволяют взаимодействовать с SharePoint и другими рабочими нагрузками, которые влияют на функциональность веб-части. 

Рекомендуем ознакомиться со следующими интерфейсами REST API:

* [REST API для списков SharePoint](https://msdn.microsoft.com/ru-ru/library/office/dn292552.aspx).

## <a name="patterns-and-practices"></a>PnP (Patterns and Practices)

Благодаря проекту [Office Dev Patterns and Practices / SharePoint Pattern and Practices (PnP)](http://aka.ms/officedevpnp) доступны примеры кодов, шаблоны и другие ресурсы, которые помогут преобразовать существующее решение в решение на базе SharePoint Framework. Обязательно ознакомьтесь с этими примерами кодов и рекомендациями.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [SharePoint Framework](sharepoint-framework-overview)
* [Создание клиентской веб-части Hello World](web-parts/get-started/build-a-hello-world-web-part)
