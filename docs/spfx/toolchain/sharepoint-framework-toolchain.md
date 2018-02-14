---
title: "Цепочка инструментов SharePoint Framework"
description: "Цепочка инструментов — это набор инструментов сборки, пакетов платформы и других элементов, которые управляют созданием и развертыванием клиентских проектов SharePoint Framework."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: dfbe1efbe50c74b842dd797ab688487147a63730
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-toolchain"></a>Цепочка инструментов SharePoint Framework

Цепочка инструментов SharePoint Framework — это набор инструментов сборки, пакетов платформы и других элементов, которые управляют созданием и развертыванием клиентских проектов. 

Цепочка инструментов:

- позволяет создавать клиентские компоненты, такие как веб-части; 
- позволяет проверять клиентские компоненты в локальной среде разработки с помощью таких инструментов, как SharePoint Workbench; 
- обеспечивает упаковку и развертывание компонентов в SharePoint; 
- содержит набор команд сборки для компиляции кода, упаковки клиентского проекта в пакет приложения SharePoint и других важных задач. 

## <a name="use-npm-packages"></a>Использование пакетов npm

Прежде чем познакомиться с различными компонентами цепочки инструментов, важно понять, как в SharePoint Framework используется [npm](https://www.npmjs.com/) для управления различными модулями проекта. npm — это один из основных диспетчеров пакетов с открытым кодом для клиентской разработки JavaScript. 

Обычный пакет npm состоит из одного или нескольких многократно используемых файлов кода JavaScript, называемых модулями, а также списка пакетов зависимостей. При установке пакета npm также устанавливает эти зависимости. 

Официальный [реестр npm](https://www.npmjs.com/) состоит из сотни пакетов, которые можно скачать для создания приложения. Вы также можете [публиковать собственные пакеты](https://docs.npmjs.com/getting-started/what-is-npm) в npm и делиться ими с другими разработчиками. Платформа SharePoint Framework использует некоторые пакеты npm в цепочке инструментов, а также публикует [собственные пакеты в реестре npm](https://www.npmjs.com/search?q=%40microsoft%2Fsp-). 

### <a name="sharepoint-framework-packages"></a>Пакеты SharePoint Framework

Платформа SharePoint Framework состоит из нескольких пакетов npm, которые позволяют создавать клиентские решения для SharePoint. 

В SharePoint Framework представлены следующие пакеты npm:

* [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint). Подключаемый модуль [Yeoman](http://yeoman.io/) для платформы SharePoint Framework. С помощью этого генератора разработчики могут быстро настроить проект клиентской веб-части и установить оптимальные значения по умолчанию.

* [@microsoft/sp-client-base](https://www.npmjs.com/package/@microsoft/sp-client-base). Определяет основные библиотеки для клиентских приложений, созданных с помощью SharePoint Framework.

* [@microsoft/sp-webpart-workbench](https://www.npmjs.com/package/@microsoft/sp-webpart-workbench). SharePoint Workbench — это отдельная среда для тестирования и отладки клиентских веб-частей.

* [@microsoft/sp-module-loader](https://www.npmjs.com/package/@microsoft/sp-module-loader). Загрузчик модулей, который управляет версиями и загрузкой клиентских компонентов, веб-частей и других ресурсов. Он также предоставляет базовые службы диагностики. Он основан на знакомых стандартах, таких как SystemJS и WebPack, и первым загружается на странице.

* [@microsoft/sp-module-interfaces](https://www.npmjs.com/package/@microsoft/sp-module-interfaces). Определяет несколько интерфейсов модулей, которые используются загрузчиком модулей SharePoint Framework и системой сборки.

* [@microsoft/sp-lodash-subset](https://www.npmjs.com/package/@microsoft/sp-lodash-subset). Предоставляет пользовательский пакет [lodash](https://lodash.com/) для загрузчика модулей SharePoint Framework. Чтобы повысить производительность среды выполнения, он включает только наиболее важные функции lodash.

* [@microsoft/sp-tslint-rules](https://www.npmjs.com/package/@microsoft/sp-tslint-rules). Определяет пользовательские правила tslint для клиентских проектов SharePoint.

* [@microsoft/office-ui-fabric-react-bundle](https://www.npmjs.com/package/@microsoft/office-ui-fabric-react-bundle). Предоставляет пользовательский пакет [office-ui-fabric-react](https://www.npmjs.com/package/office-ui-fabric-react), оптимизированный для загрузчика модулей SharePoint Framework.

### <a name="common-build-tool-packages"></a>Стандартные пакеты инструментов сборки

Наряду с пакетами SharePoint Framework, для компиляции кода TypeScript в JavaScript, преобразования SCSS в CSS и других задач сборки также используется стандартный набор инструментов сборки.

Ниже приведены стандартные пакеты инструментов сборки npm, представленные в SharePoint Framework.

* [@microsoft/sp-build-core-tasks](https://www.npmjs.com/package/@microsoft/sp-build-core-tasks). Набор задач для системы сборки SharePoint Framework, основанной на gulp. Пакет `sp-build-core-tasks` реализует операции, относящиеся только к SharePoint, такие как упаковка и манифесты.

* [@microsoft/sp-build-web](https://www.npmjs.com/package/@microsoft/sp-build-web). Импортирует и настраивает набор задач сборки для целевого режима сборки, который запустится в веб-браузере (а не в среде Node.js). Этот пакет должен импортироваться напрямую файлом gulp, который использует систему сборки SharePoint Framework. 

* [@microsoft/gulp-core-build](https://www.npmjs.com/package/@microsoft/gulp-core-build). Основные задачи gulp для создания TypeScript, HTML, less и других форматов сборки. Этот пакет зависит от других пакетов npm, которые содержат следующие задачи:
    - [@microsoft/gulp-core-build-typescript](https://www.npmjs.com/package/@microsoft/gulp-core-build-typescript)
    - [@microsoft/gulp-core-build-sass](https://www.npmjs.com/package/@microsoft/gulp-core-build-sass);
    - [@microsoft/gulp-core-build-webpack](https://www.npmjs.com/package/@microsoft/gulp-core-build-webpack);
    - [@microsoft/gulp-core-build-serve](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve);
    - [@microsoft/gulp-core-build-karma](https://www.npmjs.com/package/@microsoft/gulp-core-build-karma);
    - [@microsoft/gulp-core-build-mocha](https://www.npmjs.com/package/@microsoft/gulp-core-build-mocha).

* [@microsoft/loader-cased-file](https://www.npmjs.com/package/@microsoft/loader-cased-file). Программа-оболочка для [загрузчика файлов](https://www.npmjs.com/package/file-loader) webpack, которую можно использовать для изменения регистра полученного имени файла. Это удобно, например, при использовании сети доставки содержимого (CDN), в которой разрешены только имена файлов в нижнем регистре.

* [@microsoft/loader-load-themed-styles](https://www.npmjs.com/package/@microsoft/loader-load-themed-styles). Загрузчик, который создает программу-оболочку для загрузки CSS в сценарии, эквивалентном `require('load-themed-styles').loadStyles( /* css text */ )`. Он заменяет загрузчик стилей.

* [@microsoft/loader-raw-script](https://www.npmjs.com/package/@microsoft/loader-raw-script). Загрузчик, который загружает содержимое файла сценария прямо в пакет webpack с помощью `eval(…)`.

* [@microsoft/loader-set-webpack-public-path](https://www.npmjs.com/package/@microsoft/loader-set-webpack-public-path). Загрузчик, который устанавливает значение переменной __webpack_public_path__, указанное в аргументах (может быть добавлено к свойству SystemJS baseURL).

## <a name="scaffold-a-new-client-side-project"></a>Формирование шаблонов нового клиентского проекта

Генератор SharePoint выполняет скаффолдинг клиентского проекта с веб-частью. Генератор также скачивает и настраивает необходимые компоненты цепочки инструментов для указанного клиентского проекта.  

### <a name="install-npm-packages"></a>Установка пакетов npm

Генератор устанавливает необходимые пакеты npm локально в папке проекта. npm позволяет устанавливать пакет локально и глобально. Оба варианта имеют свои преимущества, но если ваш код зависит от модулей этих пакетов, [лучше](https://nodejs.org/en/blog/npm/npm-1-0-global-vs-local-installation/) устанавливать их локально. Код веб-части зависит от различных пакетов сборки (общих и относящихся только к SharePoint), и поэтому эти пакеты необходимо устанавливать локально. 

Так как пакеты устанавливаются локально, npm также устанавливает связанные с ними зависимости. Установленные пакеты можно найти в папке `node_modules` в папке проекта. Эта папка содержит пакеты, а также все их зависимости. В идеале эта папка должна содержать десятки и сотни папок, так как пакеты npm всегда разбиваются на небольшие модули, что приводит к установке десятков и сотен пакетов. Основные пакеты SharePoint Framework расположены в папке `node_modules\@microsoft`. `@microsoft` — это область npm, которая представляет все [пакеты, опубликованные корпорацией Майкрософт](https://www.npmjs.com/~microsoft).

Каждый раз, когда вы создаете проект с помощью генератора, последний локально устанавливает пакеты SharePoint Framework, а также зависимости для этого проекта. Таким образом, благодаря npm вы можете легко управлять проектами веб-частей, не затрагивая другие проекты в локальной среде разработки. 

### <a name="specify-dependencies-with-packagejson"></a>Указание зависимостей с помощью файла package.json

Файл `package.json` в клиентском проекте определяет список зависимостей проекта. Список определяет, какие зависимости необходимо устанавливать. Как описано выше, каждая зависимость может содержать несколько других зависимостей. Диспетчер npm позволяет определять зависимости среды выполнения и сборки для пакета с помощью свойств `dependencies` и `devDependencies`. Свойство `devDependencies` пригодится, если нужно использовать этот модуль в коде, например при создании веб-частей.

Ниже приведен файл `package.json` из [веб-части hello world](../web-parts/get-started/build-a-hello-world-web-part.md).

```json 
{
  "name": "helloword-webpart",
  "version": "0.0.1",
  "private": true,
  "engines": {
    "node": ">=0.10.0"
  },
  "dependencies": {
    "@microsoft/sp-client-base": "~1.0.0",
    "@microsoft/sp-core-library": "~1.0.0",
    "@microsoft/sp-webpart-base": "~1.0.0",
    "@types/webpack-env": ">=1.12.1 <1.14.0"
  },
  "devDependencies": {
    "@microsoft/sp-build-web": "~1.0.0",
    "@microsoft/sp-module-interfaces": "~1.0.0",
    "@microsoft/sp-webpart-workbench": "~1.0.0",
    "gulp": "~3.9.1",
    "@types/chai": ">=3.4.34 <3.6.0",
    "@types/mocha": ">=2.2.33 <2.6.0"
  },
  "scripts": {
    "build": "gulp bundle",
    "clean": "gulp clean",
    "test": "gulp test"
  }
}
```

Для проекта устанавливается много пакетов, но они необходимы только для создания веб-части в среде разработки. С помощью этих пакетов вы можете добавлять зависимости от модулей, а также собирать, компилировать, объединять в пакет и упаковывать веб-часть для развертывания. Последняя минифицированная объединенная в пакет версия веб-части, развернутая на сервере CDN или в SharePoint, не включает эти пакеты. Но вы можете включить некоторые модули в зависимости от потребностей. Дополнительные сведения см. в статье [Добавление внешней библиотеки в веб-часть](../web-parts/basics/add-an-external-library.md).

### <a name="work-with-source-control-systems"></a>Работа с системами управления версиями

Вместе с количеством зависимостей проекта увеличивается количество пакетов для установки. Не возвращайте папку `node_modules`, которая содержит все зависимости, в систему управления версиями. Папку `node_modules` следует исключить из списка файлов, которые пропускаются при возврате. 

Если вы используете систему управления версиями `git`, проект веб-части, созданный генератором Yeoman, содержит файл `.gitignore`, который, помимо прочего, исключает папку `node_modules`. 

Когда вы впервые извлекаете или клонируете проект веб-части из системы управления версиями, выполните следующую команду, чтобы инициализировать и установить все зависимости проекта локально:

```
npm i
```

После выполнения команды диспетчер npm проверяет файл `package.json` и устанавливает необходимые зависимости. 

## <a name="build-tasks"></a>Создание задач

Платформа SharePoint Framework использует средство запуска задач [gulp](http://gulpjs.com/) для обработки следующих процессов:

* добавление в пакет и минификация файлов JavaScript и CSS;
* запуск инструментов для вызова задач по добавлению в пакет и минификации перед каждой сборкой;
* компиляция файлов LESS или SASS в CSS;
* компиляция файлов TypeScript в JavaScript.

Цепочка инструментов состоит из следующих задач gulp, определенных в пакете [@microsoft/sp-build-core-tasks](https://www.npmjs.com/package/@microsoft/sp-build-core-tasks):

* **build**: создает проект клиентского решения.
* **bundle**: объединяет точку входа проекта клиентского решения и все его зависимости в один файл JavaScript.
* **serve**: запускает проект клиентского решения и ресурсы с локального компьютера.
* **clean**: удаляет артефакты сборки проекта клиентского решения из предыдущей сборки и каталогов целевого объекта сборки (lib и dist).
* **test**: запускает модульные тесты для проекта клиентского решения (если они доступны). 
* **package-solution**: помещает клиентское решение в пакет SharePoint.
* **deploy-azure-storage**: развертывает ресурсы проекта клиентского решения в хранилище Azure. 

Чтобы инициировать задачу, добавьте ее имя к команде gulp. Например, для компиляции и просмотра веб-части в SharePoint Workbench выполните следующую команду:

```
gulp serve
```

> [!NOTE] 
> Невозможно выполнять несколько задач одновременно.

Задача `serve` выполняет различные задачи и открывает SharePoint Workbench.

![задача gulp serve](../../images/toolchain-gulp-serve-task.png)

### <a name="build-targets"></a>Целевые режимы сборки

На предыдущем снимке экрана указан следующий целевой режим сборки:

```
Build target: DEBUG
```

Если параметр не задан, целевой режим команд — BUILD. Если параметр `ship` задан, целевой режим команд — SHIP.

Обычно, когда проект веб-части готов к отгрузке или развертыванию на рабочем сервере, используется целевой режим SHIP. Для других сценариев, таких как проверка и отладка, используется целевой режим BUILD. Целевой режим SHIP также гарантирует, что выполнена сборка минифицированной версии пакета веб-части. 

Чтобы использовать режим SHIP, добавьте к имени задачи `--ship`:

```
gulp --ship
```

В режиме DEBUG задачи сборки копируют все ресурсы веб-части, в том числе пакет веб-части, в папку `dist`.

В режиме SHIP задачи сборки копируют все ресурсы веб-части, в том числе пакет веб-части, в папку `temp\deploy`.

## <a name="see-also"></a>См. также

- [Средства разработки и библиотеки платформы SharePoint Framework](../tools-and-libraries.md)
- [Скаффолдинг проектов с помощью генератора Yeoman для SharePoint](scaffolding-projects-using-yeoman-sharepoint-generator.md)
- [Обзор SharePoint Framework](../sharepoint-framework-overview.md)
