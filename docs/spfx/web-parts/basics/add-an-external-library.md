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
# <a name="add-an-external-library-to-your-sharepoint-client-side-web-part"></a>Добавление внешней библиотеки в клиентскую веб-часть SharePoint

Вам может понадобиться добавить в веб-часть одну или несколько библиотек JavaScript. В этой статье описано, как добавить внешнюю библиотеку в пакет и использовать библиотеки в нескольких веб-частях.

## <a name="bundle-a-script"></a>Добавление сценария в пакет

По умолчанию средство увязки веб-частей в пакеты автоматически добавляет библиотеки, которые представляют собой зависимости для модуля веб-части. Это означает, что такие библиотеки развертываются в том же файле пакета JavaScript, что и веб-часть. Это удобно в случае небольших библиотек, которые не используются в нескольких веб-частях.

### <a name="example"></a>Пример

1. Добавьте [библиотеку проверки](https://www.npmjs.com/package/validator) строк в веб-часть.

2. Скачайте пакет средств проверки, используя npm:

    ```sh
    npm install validator --save
    ```

    > [!NOTE] 
    > Так как вы используете TypeScript, для добавляемого пакета нужны определения типов. Это очень важно при написании кода, так как TypeScript — это просто расширенная версия JavaScript. При компиляции код TypeScript преобразуется в код JavaScript. Для поиска определений типов можно использовать **npm**, например `npm install @types/{package} --save`.

3. Создайте в папке веб-части файл с именем `validator.d.ts` и добавьте приведенный ниже код.

    ```typescript
    declare module "validator" {
        export function isEmail(email: string): boolean;
        export function isAscii(text: string): boolean;
    }
    ```

    > [!NOTE] 
    > Для некоторых библиотек нет определений типов. Предположим, что [сообщество еще не создало файл определений типов](https://www.npmjs.com/package/@types/validator) для библиотеки Validator. В этом случае нужно задать собственный файл определений типов `.d.ts` для библиотеки. Ниже приведен пример.

4. Импортируйте определения типов в файле веб-части:

    ```typescript
    import * as validator from 'validator';
    ```

5. Укажите библиотеку проверки в коде веб-части:

    ```typescript
    validator.isEmail('someone@example.com');
    ```

## <a name="share-a-library-among-multiple-web-parts"></a>Использование библиотеки несколькими веб-частями

Клиентское решение может включать несколько веб-частей. Для них может потребоваться импортировать или использовать одну и ту же библиотеку. В таких случаях не добавляйте библиотеку в пакет, а включите ее в отдельный файл JavaScript, чтобы повысить эффективность и улучшить кэширование. Особенно это касается больших библиотек.

### <a name="example"></a>Пример

В этом примере пакет [marked](https://www.npmjs.com/package/marked) (компилятор markdown) помещается в отдельный пакет для совместного использования.

1. Скачайте пакет **marked** с помощью npm:

    ```sh
    npm install marked --save
    ```

2. Скачайте определения типов:

    ```sh
    npm install @types/marked --save
    ```

3. Измените **config/config.json** и добавьте запись в схему **externals**. В результате средство увязки поместит эту библиотеку в отдельный файл, а не добавит в пакет:

    ```json
    "marked": "node_modules/marked/marked.min.js"
    ```

4. Теперь, когда мы добавили пакет и определения типов для библиотеки, добавьте оператор для импорта библиотеки `marked` в веб-части:

    ```typescript
    import * as marked from 'marked';
    ```

5. Укажите библиотеку в своей веб-части:

    ```typescript
    console.log(marked('I am using __markdown__.'));
    ```

## <a name="load-a-script-from-a-cdn"></a>Загрузка сценария из сети CDN

Вы можете не загружать библиотеку из пакета npm, а загрузить сценарий из сети доставки содержимого (CDN). Для этого измените файл **config.json**, чтобы обеспечить загрузку библиотеки с использованием URL-адреса CDN.

### <a name="example"></a>Пример

В этом примере из CDN загружается jQuery. Пакет npm устанавливать не нужно. Но определения типов все равно нужно установить.

1. Установите определения типов для jQuery:

    ```sh
    npm install --save @types/jquery
    ```

2. Обновите файл `config.json` в папке `config` для загрузки jQuery из CDN. Добавьте запись в поле `externals`:

    ```json
    "jquery": "https://code.jquery.com/jquery-3.1.0.min.js"
    ```

3. Импортируйте jQuery в веб-часть:

    ```typescript
    import * as $ from 'jquery';
    ```

4. Используйте jQuery в своей веб-части:

    ```javascript
    alert( $('#foo').val() );
    ```

## <a name="load-a-non-amd-module"></a>Загрузка модуля, отличного от AMD-модуля

Некоторые сценарии JavaScript предусматривают хранение библиотек в глобальном пространстве имен. Такой подход устарел. Сейчас используются модули [ES6](https://github.com/lukehoban/es6features/blob/master/README.md#modules), [UMD (Universal Module Definitions)](https://github.com/umdjs/umd) / [AMD (Asynchronous Module Definitions)](https://en.wikipedia.org/wiki/Asynchronous_module_definition). Возможно, вам потребуется загрузить такие библиотеки в веб-часть.

> [!TIP] 
> Трудно определить вручную, является ли загружаемый сценарий сценарием AMD, особенно если он минифицирован. Если ваш сценарий размещен по общедоступному URL-адресу, вы можете использовать бесплатный инструмент [Rencore SharePoint Framework Script Check](https://rencore.com/sharepoint-framework/script-check/), чтобы автоматически определить тип сценария. Кроме того, этот инструмент позволяет узнать, правильно ли настроен место размещения, с которого загружается сценарий.

Чтобы загрузить модуль, созданный не с помощью AMD, добавьте дополнительное свойство в запись в файле **config.json**.

### <a name="example"></a>Пример

В этом примере из CDN Contoso загружается фиктивный модуль, отличный от AMD-модуля. Эти действия предназначены для любого сценария, отличного от AMD-сценария, в каталоге src/ или node_modules/.

Сценарий называется **Contoso.js**. Путь к нему: **https://contoso.com/contoso.js**. Вот его содержимое:

```javascript
var ContosoJS = {
  say: function(text) { alert(text); },
  sayHello: function(name) { alert('Hello, ' + name + '!'); }
};
```

<br/>

1. Создайте определения типов для сценария в файле **contoso.d.ts** из папки веб-части.

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

2. Включите этот сценарий в файл **config.json**. Добавьте запись в схему **externals**:

    ```json
    {
        "contoso": {
            "path": "https://contoso.com/contoso.js",
            "globalName": "ContosoJS"
        }
    }
    ```

3. Добавьте операцию импорта в код веб-части:

    ```typescript
    import contoso from 'contoso';
    ```

4. Используйте библиотеку contoso в своем коде:

    ```typescript
    contoso.sayHello(username);
    ```

## <a name="load-a-library-that-has-a-dependency-on-another-library"></a>Загрузка библиотеки с зависимостью от другой библиотеки

Многие библиотеки содержат зависимости от другой библиотеки. Такие зависимости можно указать в файле **config.json** с помощью свойства **globalDependencies**.

> [!IMPORTANT] 
> Обратите внимание, что это поле не нужно указывать для AMD-модулей. Они импортируют друг друга правильно. Однако AMD-модуль не может зависеть от модуля, отличного от AMD. В некоторых случаях можно загрузить сценарий AMD в виде сценария, отличного от AMD. Это часто требуется при работе с библиотекой jQuery, которая сама по себе является сценарием AMD, и подключаемыми модулями jQuery, которые в большинстве случаев распространяются как сценарии, отличные от AMD, и зависят от jQuery.

Ниже приведены два примера.

### <a name="non-amd-module-has-a-non-amd-module-dependency"></a>Для модуля, отличного от AMD-модуля, предусмотрена соответствующая зависимость

В этом примере используются два вымышленных сценария. Они хранятся в папке **src/**, но их также можно загрузить из CDN.

**ContosoUI.js**

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

**ContosoCore.js**

```javascript
var Contoso = {
    getEvents: function() {
        return ['A', 'B', 'C'];
    }
};
```

<br/>

1. Добавьте или создайте определения типов для этого класса. В этом случае нужно создать файл `Contoso.d.ts`, который содержит определения типов для обоих файлов JavaScript.

    **contoso.d.ts**

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

2. Обновите файл **config.json**. Добавьте две записи в **externals**:

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

3. Добавьте операции импорта для Contoso и ContosoUI:

    ```typescript
    import contoso = require('contoso');
    require('contoso-ui');
    ```

4. Укажите библиотеки в своем коде:

    ```typescript
    contoso.EventList.alert();
    ```

## <a name="load-sharepoint-jsom"></a>Загрузка JSOM SharePoint

Модели JSOM SharePoint загружаются практически так же, как сценарии с зависимостями, отличные от AMD-сценариев. Это значит, что используются параметры **globalName** и **globalDependency**.

> [!IMPORTANT] 
> Обратите внимание, что приведенный ниже подход вызовет ошибки на классических страницах SharePoint, где модель JSOM уже загружена. Если ваша веб-часть должна работать как с классическими, так и современными страницами, нужно сначала проверить, доступна ли модель JSOM, а если нет, загрузить ее динамически с помощью **SPComponentLoader**.

<br/>

1. Установите определения типов для Microsoft Ajax (зависимости для определений типов JSOM представлены ниже).

    ```sh
    npm install @types/microsoft-ajax --save
    ```

2. Установите определения типов для JSOM:

    ```sh
    npm install @types/sharepoint --save
    ```

3. Добавьте записи в файл `config.json`:

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

4. Добавьте в веб-часть операторы `require`:

    ```typescript
    require('sp-init');
    require('microsoft-ajax');
    require('sp-runtime');
    require('sharepoint');
    ```

## <a name="load-localized-resources"></a>Загрузка локализованных ресурсов

В файле **config.json** есть схема **localizedResources**, с помощью которой можно описать, как загружать локализованные ресурсы. Пути в этой схеме заданы относительно папки **lib** и не должны содержать начальную косую черту (**/**).

В этом примере у вас есть папка **src/strings/**. В этой папке несколько файлов JavaScript, таких как **en-us.js**, **fr-fr.js**, **de-de.js**. Так как каждый из этих файлов должен загружаться загрузчиком модулей, они должны содержать оберточный код CommonJS. Например, в случае файла **en-us.js**:

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

1. Измените файл **config.json**. Добавьте запись в схему **localizedResources**. `{locale}` — это замещающий токен для имени языкового стандарта.

    ```json
    {
        "strings": "strings/{locale}.js"
    }
    ```

2. Добавьте определения типов для строк. В этом случае у вас есть файл **MyStrings.d.ts**:

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

3. Добавьте операции импорта для строк в проекте:

    ```typescript
    import * as strings from 'mystrings';
    ```

4. Используйте строки в своем проекте:

    ```typescript
    alert(strings.initialPrompt);
    ```

## <a name="see-also"></a>См. также

- [Обзор SharePoint Framework](../../sharepoint-framework-overview.md)