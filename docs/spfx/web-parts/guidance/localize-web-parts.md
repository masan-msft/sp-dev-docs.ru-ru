---
title: "Локализация клиентских веб-частей SharePoint Framework"
description: "Сделайте свою веб-часть SharePoint Framework более привлекательной, локализовав ее для пользователей SharePoint по всему миру."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 980dda1cee0518edc9db169e2c8b3bc05cb0509c
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="localize-sharepoint-framework-client-side-web-parts"></a>Локализация клиентских веб-частей SharePoint Framework

Вы можете увеличить привлекательность клиентской веб-части SharePoint Framework, локализовав ее для пользователей SharePoint по всему миру. В этой статье показано, как локализовать веб-часть на нидерландский язык (Нидерланды) и проверить, отображаются ли правильно локализованные значения.

> [!NOTE] 
> Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки для создания клиентских веб-частей SharePoint](../../set-up-your-development-environment.md).

## <a name="prepare-the-project"></a>Подготовка проекта

### <a name="create-a-new-project"></a>Создание проекта

1. Создайте папку для проекта.

  ```sh
  md react-localization
  ```

2. Перейдите в папку проекта.

  ```sh
  cd react-localization
  ```

3. В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.

  ```sh
  yo @microsoft/sharepoint
  ```

4. Когда появится соответствующий запрос, укажите следующие значения:

  - **react-localization** в качестве имени решения;
  - **SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) в качестве набора базовых пакетов;
  - **Use the current folder** (Использовать текущую папку) в качестве расположения файлов;
  - **y** для того, чтобы можно было выполнять развертывание на уровне клиента;
  - **WebPart** (Веб-часть) в качестве типа создаваемого компонента;
  - **Greeting** (Приветствие) в качестве имени веб-части;
  - **Greets the user** (Приветствие пользователя) в качестве описания веб-части;
  - **React** в качестве отправной точки создания веб-части.

  <br/>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/localization-yo-sharepoint.png)

5. После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:

  ```sh
  npm shrinkwrap
  ```

6. Откройте папку проекта в редакторе кода. В этой статье в инструкциях и на снимках экрана используется Visual Studio Code, но вы можете использовать любой другой редактор.

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/localization-visual-studio-code.png)

### <a name="replace-the-default-code"></a>Замена кода по умолчанию

1. В редакторе кода откройте файл **./src/webparts/greeting/GreetingWebPart.ts** и замените определение интерфейса `IGreetingWebPartProps` следующим кодом:

  ```typescript
  export interface IGreetingWebPartProps {
    greeting: string;
  }
  ```

2. В том же файле замените класс **GreetingWebPart** следующим кодом:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {

    public render(): void {
      const element: React.ReactElement<IGreetingProps > = React.createElement(
        Greeting,
        {
          greeting: this.properties.greeting
        }
      );

      ReactDom.render(element, this.domElement);
    }

    protected get dataVersion(): Version {
      return Version.parse('1.0');
    }

    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.DisplayGroupName,
                groupFields: [
                  PropertyPaneTextField('greeting', {
                    label: strings.GreetingFieldLabel
                  })
                ]
              }
            ]
          }
        ]
      };
    }
  }
  ```

3. Обновите основной компонент React. Для этого откройте файл **./src/webparts/greeting/components/Greeting.tsx** и вставьте следующий код вместо существующего:

  ```typescript
  import * as React from 'react';
  import styles from './Greeting.module.scss';
  import { IGreetingProps } from './IGreetingProps';
  import { escape } from '@microsoft/sp-lodash-subset';

  export default class Greeting extends React.Component<IGreetingProps, {}> {
    public render(): JSX.Element {
      return (
        <div className={styles.greeting}>
          <div className={styles.container}>
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
                <span className='ms-font-xl ms-fontColor-white'>
                  Welcome to SharePoint!
                </span>
                <p className='ms-font-l ms-fontColor-white'>
                  Customize SharePoint experiences using Web Parts.
                </p>
                <p className='ms-font-l ms-fontColor-white'>
                  {escape(this.props.greeting)}
                </p>
                <a href="https://aka.ms/spfx" className={styles.button}>
                  <span className={styles.label}>Learn more</span>
                </a>
              </div>
            </div>
          </div>
        </div>
      );
    }
  }
  ```

4. Обновите интерфейс основного компонента React, открыв файл **./src/webparts/greeting/components/IGreetingProps.tsx** и заменив код на следующий:

  ```tsx
  import { IGreetingWebPartProps } from '../GreetingWebPart';

  export interface IGreetingProps extends IGreetingWebPartProps {
  }
  ```

5. Обновите файл определения типа локализации TypeScript, открыв файл **./src/webparts/greeting/loc/mystrings.d.ts** и заменив код на следующий:

  ```typescript
  declare interface IGreetingWebPartStrings {
    PropertyPaneDescription: string;
    DisplayGroupName: string;
    GreetingFieldLabel: string;
  }

  declare module 'GreetingWebPartStrings' {
    const strings: IGreetingWebPartStrings;
    export = strings;
  }
  ```

6. Обновите файл английского языка (США). Для этого откройте файл **./src/webparts/greeting/loc/en-us.js** и вставьте следующий код вместо существующего:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Greeting web part configuration",
      "DisplayGroupName": "Display",
      "GreetingFieldLabel": "Greeting to show in the web part"
    }
  });
  ```

7. В манифесте веб-части обновите значение по умолчанию для свойства **greeting**, открыв файл **./src/webparts/greeting/GreetingWebPart.manifest.json** и заменив раздел **properties** следующим кодом:

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": { "default": "Other" },
      "title": { "default": "Greeting" },
      "description": { "default": "Greets the user" },
      "officeFabricIconFontName": "Page",
      "properties": {
        "greeting": "Hello"
      }
    }]
  }
  ```

8. Проверьте, правильно ли применены все изменения, с помощью следующей команды:

  ```sh
  gulp serve
  ```

9. В SharePoint Workbench добавьте веб-часть на страницу и откройте ее конфигурацию.

  ![Веб-часть приветствия добавлена на страницу, область свойств открыта](../../../images/localization-initial-changes.png)

## <a name="localize-the-web-part-manifest"></a>Локализация манифеста веб-части

Каждая клиентская веб-часть SharePoint Framework состоит из кода и манифеста. Манифест содержит сведения о веб-части, такие как название, описание и значок. При добавлении веб-части на страницу пользователи видят сведения из ее манифеста. 

Эти сведения помогают пользователю решить, нужна ли ему данная веб-часть. Название и описание должны правильно отражать функциональность веб-части, если вы хотите, чтобы ею пользовались. Если веб-часть используется не только на англоязычных сайтах, то локализация метаданных сделает ее еще удобнее для пользователей.

В манифесте веб-части можно указывать локализованные значения некоторых свойств, например названия и описания. Полный список всех свойств манифеста веб-части, поддерживающих локализацию, см. в статье [Упрощенное добавление веб-частей с помощью предварительно настроенных записей](./simplify-adding-web-parts-with-preconfigured-entries.md#properties-of-a-preconfiguredentries-array-item). 

Свойства, поддерживающие локализацию, относятся к типу **ILocalizedString**. Для каждой локализованной строки должно быть указано по крайней мере значение по умолчанию (при необходимости можно указать значения для других языковых стандартов).

### <a name="add-localized-values-for-title-description-and-group-name"></a>Добавление локализованных значений для названия, описания и имени группы

1. Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.manifest.json**. 

2. В массиве **preconfiguredEntries** добавьте переводы для свойств **title**, **description** и **group** на нидерландском языке (Нидерланды), вставив следующий код вместо существующего:

  ```json
  {
    // ...
    "preconfiguredEntries": [{
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": { "default": "Other", "nl-nl": "Anders" },
      "title": { "default": "Greeting", "nl-nl": "Begroeting" },
      "description": { "default": "Greets the user", "nl-nl": "Begroet de gebruiker" },
      "officeFabricIconFontName": "Page",
      "properties": {
        "greeting": "Hello"
      }
    }]
  }
  ```

3. Чтобы проверить, работает ли проект, выполните следующую команду:

  ```sh
  gulp serve
  ```

> [!NOTE] 
> К сожалению, в настоящее время в SharePoint Workbench невозможно просматривать локализованные значения из манифеста веб-части. Всегда используется перевод по умолчанию.

## <a name="localize-the-web-part-property-pane"></a>Локализация области свойств веб-части

Пользователям часто приходится настраивать веб-часть для конкретных нужд. Подписав параметры конфигурации, вы можете сделать веб-часть удобнее для пользователей и сократить количество обращений в службу поддержки за помощью в настройке.

Область свойств веб-части состоит из нескольких разделов. В каждом разделе есть заголовок и один или несколько элементов, с помощью которых пользователи могут настраивать веб-часть. Каждый из этих элементов содержит описание его назначения. 

По умолчанию веб-части загружают строковые подписи из файла ресурсов JavaScript. Если вы создавали классические веб-части с помощью решений с полным доверием, они похожи на RESX-файлы ресурсов. Использовать эти файлы ресурсов необязательно, строки можно включать непосредственно в код. Однако настоятельно рекомендуем использовать такие файлы. Немного дополнительных служебных данных — ничего по сравнению с усилиями, необходимыми для извлечения всех подписей, если впоследствии вам потребуется перевести веб-часть.

Файлы локализации, используемые веб-частью, хранятся в папке **./src/webparts/greeting/loc**.

![Файлы локализации, используемые клиентской веб-частью SharePoint Framework, выделенные в Visual Studio Code](../../../images/localization-loc-folder.png)

<br/>

Папка **loc** содержит файл определения типа TypeScript (**./src/webpart/greeting/loc/mystrings.d.ts**), который сообщает TypeScript о различных строках в локализованных файлах. На основе сведений из этого файла редактор кода может предоставлять подсказки IntelliSense при работе со строками в коде. Кроме того, при сборке проекта TypeScript может проверять, не ссылаетесь ли вы на неопределенные строки.

![Подсказки IntelliSense для локализованных строк в Visual Studio Code](../../../images/localization-intellisense.png)

<br/>

Переведенные строки для каждого языкового стандарта, поддерживаемого веб-частью, содержатся в обычном файле JavaScript (не TypeScript) с именем в нижнем регистре (например, **en-us.js**).

![Шаблон стандартного файла локализации, сформированный с новым проектом SharePoint Framework](../../../images/localization-standard-locale-file.png)

<br/>

> [!IMPORTANT] 
> Внимательно проверяйте, чтобы все ключи, указанные в файле определения типа TypeScript как локализуемые, были переведены во всех файлах локализации JavaScript.

По умолчанию в SharePoint Framework используется языковой стандарт en-US. Если языковой стандарт сайта не поддерживается веб-частью, SharePoint Framework использует языковой стандарт по умолчанию (en-US). 

Чтобы переопределить этот параметр, создайте файл языкового стандарта **default.js** со значениями на предпочитаемом языке. Имя **default.js** не соответствует соглашению об именовании языковых стандартов, но оно дает указание SharePoint Framework использовать этот файл языкового стандарта, а не английский язык (США).

### <a name="add-localized-values-for-web-part-property-pane-strings"></a>Добавление локализованных значений для строк области свойств веб-части

1. В папке **./src/webparts/greetings/loc** создайте файл **nl-nl.js** и введите следующий код:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
      "DisplayGroupName": "Weergave",
      "GreetingFieldLabel": "Begroeting die in het webonderdeel getoond wordt"
    }
  });
  ```

2. Убедитесь, что ключи в файле определения типа TypeScript для локализации соответствуют содержимому файлов языковых стандартов в случае английского (США) и нидерландского (Нидерланды) языков.

  ![Файл определения типа TypeScript для локализации и файлы языковых стандартов для английского (США) и нидерландского (Нидерланды) языков, открытые рядом в Visual Studio Code](../../../images/localization-keys-comparison.png)

### <a name="verify-the-localized-web-part-property-pane-strings"></a>Проверка локализованных строк в области свойств веб части

При проверке веб-частей с помощью размещенной версии SharePoint Workbench или сайтов групп в клиенте разработчика по умолчанию используется языковой стандарт сайта контекста, выраженный свойством **spPageContextInfo.currentUICultureName**. 

При проверке веб-частей с помощью локальной версии SharePoint Workbench SharePoint Framework по умолчанию использует языковой стандарт en-US для отображения строк области свойств веб-части. Проверить значения из других языковых стандартов, поддерживаемых веб-частью, можно двумя способами.

#### <a name="specify-the-locale-to-be-tested-in-the-project-configuration"></a>Указание проверяемого языкового стандарта в конфигурации проекта

Чтобы указать проверяемый языковой стандарт в SharePoint Workbench, можно изменить конфигурацию проекта. Этот способ удобен, если вы и ваши коллеги работаете с языковым стандартом в течение долгого времени или создаете веб-часть, которая не поддерживает английский язык (США). 

1. В редакторе кода откройте файл **./config/write-manifests.json** и вставьте следующий код вместо существующего:

  ```json
  {
    "cdnBasePath": "<!-- PATH TO CDN -->",
    "debugLocale": "nl-nl"
  }
  ```

2. Запустите SharePoint Workbench с помощью следующей команды:

  ```sh
  gulp serve
  ```

  Добавив веб-часть на страницу и открыв ее конфигурацию, вы увидите, что строки в области свойств веб-части отображаются на нидерландском языке (Нидерланды).

  ![Строка области свойств веб-части на нидерландском языке (Нидерланды)](../../../images/localization-property-pane-nl-nl.png)

#### <a name="specify-the-locale-to-be-tested-by-using-the-command-line-argument"></a>Указание проверяемого языкового стандарта с помощью аргумента командной строки

Еще один способ задать языковой стандарт, который будет использоваться локальной областью SharePoint Workbench, — указать его в качестве аргумента задачи gulp. 

- Запустите SharePoint Workbench с помощью следующей команды:

  ```sh
  gulp serve --locale=nl-nl
  ```

  Открыв конфигурацию веб-части, вы увидите, что все строки в области свойств отображаются на нидерландском (Нидерланды), а не на английском языке (США), используемом по умолчанию.

  ![Строка области свойств веб-части на нидерландском языке (Нидерланды)](../../../images/localization-property-pane-nl-nl.png)

## <a name="localize-web-part-contents"></a>Локализация содержимого веб-части

Необходимо локализовать не только строки в области свойств веб части, но и все строки, отображаемые в веб-части. Для этого можно воспользоваться тем же способом, что и при локализации строк в области свойств. Добавьте ключ в файле определения TypeScript для каждой локализуемой строки и переведите ее на каждый из поддерживаемых языков в файле JavaScript соответствующего языкового стандарта.

### <a name="globalize-the-web-part-strings"></a>Глобализация строк веб части

Строки стандартной веб-части, созданной на основе шаблонного проекта SharePoint Framework, внедрены в код. Прежде чем локализовать эти строки, необходимо заменить их ссылками на локализованные строки. Этот процесс часто называют **глобализацией** или **интернационализацией** (или просто **i18n**).

1. В редакторе кода откройте файл **./src/webparts/greeting/components/Greetings.tsx**. 

2. В верхней части файла, сразу же после последнего оператора `import`, добавьте ссылку на локализованные строки:

  ```typescript
  import * as strings from 'GreetingWebPartStrings';
  ```

3. Замените содержимое класса **Greeting** следующим кодом:

  ```typescript
  // ...
  export default class Greeting extends React.Component<IGreetingProps, {}> {
    public render(): JSX.Element {
      return (
        <div className={styles.greeting}>
          <div className={styles.container}>
            <div className={`ms-Grid-row ms-bgColor-themeDark ms-fontColor-white ${styles.row}`}>
              <div className="ms-Grid-col ms-u-lg10 ms-u-xl8 ms-u-xlPush2 ms-u-lgPush1">
                <span className='ms-font-xl ms-fontColor-white'>
                  Welcome to SharePoint!
                </span>
                <p className='ms-font-l ms-fontColor-white'>
                  Customize SharePoint experiences using Web Parts.
                </p>
                <p className='ms-font-l ms-fontColor-white'>
                  {escape(this.props.greeting)}
                </p>
                <a href="https://aka.ms/spfx" className={styles.button}>
                  <span className={styles.label}>{strings.LearnMoreButtonLabel}</span>
                </a>
              </div>
            </div>
          </div>
        </div>
      );
    }
  }
  ```

### <a name="add-the-new-string-to-the-localization-typescript-type-definition-file"></a>Добавление новой строки в файл определения типа локализации TypeScript

После замены строки на ссылку нужно добавить эту строку в файлы локализации, используемые веб-частью. 

- В редакторе кода откройте файл **./src/webparts/greetings/loc/mystrings.d.ts** и вставьте следующий код вместо существующего:

  ```typescript
  declare interface IGreetingWebPartStrings {
    PropertyPaneDescription: string;
    DisplayGroupName: string;
    GreetingFieldLabel: string;
    LearnMoreButtonLabel: string;
  }

  declare module 'greetingStrings' {
    const strings: IGreetingWebPartStrings;
    export = strings;
  }

  ```

### <a name="add-localized-values-for-the-new-string"></a>Добавление локализованных значений для новой строки

Вам осталось лишь указать локализованные версии для новой строки во всех языковых стандартах, поддерживаемых веб-частью. 

1. В редакторе кода откройте файл **./src/webparts/greeting/loc/en-us.js** и вставьте следующий код вместо существующего:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Greeting web part configuration",
      "DisplayGroupName": "Display",
      "GreetingFieldLabel": "Greeting to show in the web part",
      "LearnMoreButtonLabel": "Learn more"
    }
  });
  ```

2. Откройте файл **./src/webparts/greeting/loc/nl-nl.js** и вставьте следующий код вместо существующего:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
      "DisplayGroupName": "Weergave",
      "GreetingFieldLabel": "Begroeting die in het webonderdeel getoond wordt",
      "LearnMoreButtonLabel": "Meer informatie"
    }
  });
  ```

3. Проверьте, правильно ли отображается переведенная строка, с помощью следующей команды:

  ```sh
  gulp serve --locale=nl-nl
  ```

  <br/>

  ![Кнопка "Подробнее" на нидерландском языке (Нидерланды)](../../../images/localization-learn-more-nl-nl.png)

## <a name="improve-globalizing-and-localizing-web-parts-by-using-pseudo-locales"></a>Как улучшить глобализацию и локализацию веб-частей с помощью псевдолокалей

Локализация веб-частей во время разработки имеет явные преимущества, но разработчики часто ею пренебрегают. Часто проект переводят в конце, и тест-инженерам трудно проверить, весь ли код поддерживает другие языковые стандарты.

Одни и те же слова на разных языках имеют разную длину. Например, предложение, переведенное с английского на немецкий или нидерландский, может стать на 35 % длиннее. Если перевод не доступен заранее, разработчикам и дизайнерам трудно проверить, поместятся ли длинные строки в пользовательском интерфейсе.

В некоторых языках используются специальные знаки, кроме стандартного набора символов ASCII. Если разработчики используют нестандартный шрифт, некоторые специальные знаки могут не поддерживаться.

Если вы узнаете обо всех этих проблемах в конце проекта, скорее всего, возникнут задержки и понадобятся дорогостоящие исправления. SharePoint Framework позволяет разработчикам использовать языковые псевдостандарты, чтобы решить эти проблемы при создании веб-частей.

> [!TIP] 
> **Что такое псевдолокали?** Псевдолокали —это языковые стандарты, предназначенные для проверки поддержки специальных знаков, языков с письмом справа налево, размещения длинных строк в пользовательском интерфейсе и других аспектов локализации.

### <a name="add-the-base-pseudo-locale"></a>Добавление базовой псевдолокали

1. В папке **./src/webparts/greeting/loc** добавьте новый файл **qps ploc.js** и вставьте следующий код:

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "[!!! Gřèèƭïñϱ ωèβ ƥářƭ çôñƒïϱúřáƭïôñ ℓôřè₥ ïƥƨú !!!]",
      "DisplayGroupName": "[!!! Ðïƨƥℓá¥ ℓ !!!]",
      "GreetingFieldLabel": "[!!! Gřèèƭïñϱ ƭô ƨλôω ïñ ƭλè ωèβ ƥářƭ ℓôřè₥ ïƥƨú !!!]",
      "LearnMoreButtonLabel": "[!!! £èářñ ₥ôřè ℓôř !!!]"
    }
  });
  ```

  > [!TIP] 
  > Вы можете преобразовать строки на английском (США), используя базовую псевдолокаль, на сайте [Pseudolocalize!](http://www.pseudolocalize.com). Увеличив длину сгенерированной строки на 35 %, можно смоделировать длину строк, переведенных на более длинные языки, например немецкий или нидерландский. Кроме того, заключив переводы в скобки и восклицательные знаки, вам будет проще понять, помещается ли на экране вся строка.

2. Проверьте проект с помощью базового языкового псевдостандарта, выполнив следующую команду:

  ```sh
  gulp serve --locale=qps-ploc
  ```

  После добавления веб-части на страницу вы сразу увидите, что две строки в веб-части не интернационализированы и отображаются на английском языке (США), а не на базовом языковом псевдостандарте.

  ![Две строки в веб-части отображаются на английском языке (США), несмотря на проверку с использованием базовой псевдолокали](../../../images/localization-web-part-body-qps-ploc.png)

3. Откройте область свойств веб-части и убедитесь, что все строки и специальные знаки отображаются правильно и помещаются в отведенном для них месте.

  ![Область свойств веб-части во время проверки веб-части в локальной рабочей области при помощи базовой псевдолокали](../../../images/localization-web-part-property-pane-qps-ploc.png)

## <a name="localize-web-part-settings-values"></a>Локализация значений параметров веб-части

SharePoint поддерживает многоязычный пользовательский интерфейс (MUI), где администратор сайта может включить несколько языков интерфейса. Сайт будет автоматически отображаться на языке, выбранном пользователем.

Веб-части, используемые на многоязычных сайтах, должны автоматически определять текущий язык и отображать содержимое на этом языке. SharePoint Framework упрощает этот процесс, автоматически загружая файл ресурсов, соответствующий текущему языку. Кроме того, при проверке веб-частей SharePoint Framework с помощью размещенной версии SharePoint Workbench также автоматически используется язык, выбранный пользователем.

Значения, настроенные с помощью свойств веб-части, не хранятся в файлах ресурсов. По умолчанию заданное значение используется как есть, что может привести к несоответствиям. Например, может отображаться приветствие на английском языке, в то время как пользователь выбрал нидерландский.

![Приветствие отображается на английском языке (США), несмотря на то что для рабочей области выбран нидерландский (Нидерланды)](../../../images/localization-english-greeting-dutch-workbench.png)

<br/>

Используя стандартные блоки, доступные в SharePoint Framework, вы можете сделать так, чтобы веб-часть хранила значения конфигурации на нескольких языках. Для каждого из поддерживаемых языков в области свойств отображается текстовое поле, где пользователь может ввести переведенное значение этого свойства.

![Несколько текстовых полей в области свойств веб-части, в которых можно ввести перевод значений](../../../images/localization-multilingual-properties.png)

> [!NOTE] 
> Для проверки веб-части, показанной в этой статье, используется многоязычный веб-сайт SharePoint с поддержкой английского (США), нидерландского и немецкого языков. Дополнительные сведения о включении дополнительных языков на сайтах SharePoint см. в статье [Выбор языков, которые должны быть доступны для пользовательского интерфейса сайта](https://support.office.com/ru-RU/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8).

### <a name="add-list-of-languages-supported-by-sharepoint-online"></a>Добавление списка языков, поддерживаемых SharePoint Online

Список языков, включенных на многоязычном сайте SharePoint, возвращается в виде массива кодов языка, например **1033** для английского (США). 

Однако используемый в данный момент язык возвращается в виде строки, например **en-US** для английского (США). Так как JavaScript не преобразовывает код языка в имя языкового стандарта и наоборот автоматически, вам нужно делать это самостоятельно.

1. Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.ts**. 

2. Добавьте переменную **locales** в уже имеющийся класс **GreetingWebPart**, используя следующий код:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    private locales = {
      1025: 'ar-SA',
      1026: 'bg-BG',
      1027: 'ca-ES',
      1028: 'zh-TW',
      1029: 'cs-CZ',
      1030: 'da-DK',
      1031: 'de-DE',
      1032: 'el-GR',
      1033: 'en-US',
      1035: 'fi-FI',
      1036: 'fr-FR',
      1037: 'he-IL',
      1038: 'hu-HU',
      1040: 'it-IT',
      1041: 'ja-JP',
      1042: 'ko-KR',
      1043: 'nl-NL',
      1044: 'nb-NO',
      1045: 'pl-PL',
      1046: 'pt-BR',
      1048: 'ro-RO',
      1049: 'ru-RU',
      1050: 'hr-HR',
      1051: 'sk-SK',
      1053: 'sv-SE',
      1054: 'th-TH',
      1055: 'tr-TR',
      1057: 'id-ID',
      1058: 'uk-UA',
      1060: 'sl-SI',
      1061: 'et-EE',
      1062: 'lv-LV',
      1063: 'lt-LT',
      1066: 'vi-VN',
      1068: 'az-Latn-AZ',
      1069: 'eu-ES',
      1071: 'mk-MK',
      1081: 'hi-IN',
      1086: 'ms-MY',
      1087: 'kk-KZ',
      1106: 'cy-GB',
      1110: 'gl-ES',
      1164: 'prs-AF',
      2052: 'zh-CN',
      2070: 'pt-PT',
      2074: 'sr-Latn-CS',
      2108: 'ga-IE',
      3082: 'es-ES',
      5146: 'bs-Latn-BA',
      9242: 'sr-Latn-RS',
      10266: 'sr-Cyrl-RS',
    };

    // ...
  }
  ```

  В переменной **locales** указаны все языки, поддерживаемые SharePoint Online.

3. Добавьте два метода class, которые будут преобразовывать имя языкового стандарта в код языка и наоборот:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...

    private getLocaleId(localeName: string): number {
      const pos: number = (Object as any).values(this.locales).indexOf(localeName);
      if (pos > -1) {
        return parseInt(Object.keys(this.locales)[pos]);
      }
      else {
        return 0;
      }
    }

    private getLocaleName(localeId: number): string {
      const pos: number = Object.keys(this.locales).indexOf(localeId.toString());
      if (pos > -1) {
        return (Object as any).values(this.locales)[pos];
      }
      else {
        return '';
      }
    }
  }
  ```

### <a name="remove-the-standard-greeting-web-part-property"></a>Удаление стандартного свойства веб-части greeting

Изначально свойство **greeting** веб-части Greeting было определено, и пользователь мог указать приветствие, которое будет отображаться на экране. Чтобы веб-часть работала на многоязычных сайтах SharePoint, следует хранить несколько значений — по одному для каждого языка. Так как невозможно заранее узнать, какие языки будут включены на сайте, вы можете динамически генерировать свойства веб-части в среде выполнения, а не использовать одно статическое свойство.

1. Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.manifest.json**. 

2. Удалите свойство **greeting** из свойства **properties**:

  ```json
  {
    // ...

    "preconfiguredEntries": [{
      "groupId": "5c03119e-3074-46fd-976b-c60198311f70", // Other
      "group": { "default": "Other", "nl-nl": "Anders" },
      "title": { "default": "Greeting", "nl-nl": "Begroeting" },
      "description": { "default": "Greets the user", "nl-nl": "Begroet de gebruiker" },
      "officeFabricIconFontName": "Page",
      "properties": {
      }
    }]
  }
  ```

3. Откройте файл **./src/webparts/greeting/GreetingWebPart.ts**.

4. Удалите свойство **greeting** из определения интерфейса `IGreetingWebPartProps`:

  ```typescript
  export interface IGreetingWebPartProps {
  }
  ```

5. Так как основной компонент React должен показывать приветствие, откройте файл **./src/webparts/greeting/components/IGreetingProps.ts** и замените интерфейс **IGreetingProps** следующим кодом:

  ```typescript
  export interface IGreetingProps {
    greeting: string;
  }
  ```

  Это изменение позволяет передать приветствие из веб-части в компонент React.

### <a name="display-property-pane-text-fields-for-all-enabled-languages"></a>Отображение текстовых полей области свойств для всех включенных языков

Изначально пользователь мог настроить приветствие с помощью конфигурации веб-части. Пользователь мог настроить одно значение, отображаемое для всех пользователей, независимо от их основного языка. Получая список языков, включенных на текущем сайте, вы можете динамически показывать текстовые поля, чтобы пользователь мог добавлять в них переводы.

#### <a name="load-information-about-languages-enabled-on-the-current-site"></a>Загрузка сведений о языках, включенных на текущем сайте

Прежде всего нужно загрузить сведения обо всех языках, включенных на текущем сайте. 

1. Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.ts**. 

2. Добавьте новую переменную класса **supportedLanguageIds**:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...
    private supportedLanguageIds: number[];
    // ...
  }
  ```

  Так как мы будем запрашивать данные в SharePoint, для выполнения операций воспользуемся HTTP-клиентом SharePoint. 
  
3. Добавьте приведенные ниже операции импорта прямо перед классом **GreetingWebPart**.

  ```typescript
  import {
    SPHttpClient,
    SPHttpClientResponse
  } from '@microsoft/sp-http';
  ```

4. В классе **GreetingWebPart** добавьте новый метод **getSupportedLanguageIds**:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...

    private getSupportedLanguageIds(): Promise<number[]> {
      return new Promise<number[]>((resolve: (supportedLanguageIds: number[]) => void, reject: (error: any) => void): void => {
        if (this.supportedLanguageIds) {
          resolve(this.supportedLanguageIds);
          return;
        }

        this.context.spHttpClient.get(this.context.pageContext.web.absoluteUrl + '/_api/web?$select=SupportedUILanguageIds', SPHttpClient.configurations.v1)
        .then((response: SPHttpClientResponse): Promise<{ SupportedUILanguageIds: number[] }> => {
          return response.json();
        }).then((siteInfo: { SupportedUILanguageIds: number[] }): void => {
          this.supportedLanguageIds = siteInfo.SupportedUILanguageIds;
          resolve(siteInfo.SupportedUILanguageIds);
        }, (error: any): void => {
          reject(error);
        });
      });
    }
  }
  ```

Список языков, включенных на текущем сайте, достаточно загрузить один раз. Если сведения о языках еще не загружены, метод использует стандартный HTTP-клиент SharePoint Framework, чтобы вызвать REST API SharePoint и получить сведения о языках, включенных на текущем сайте.

#### <a name="dynamically-render-text-fields-for-all-languages"></a>Динамическая отрисовка текстовых полей для всех языков

Теперь, когда вы можете получать сведения о языках, включенных на текущем сайте, для каждого из них будут отображаться текстовые поля, в которых пользователь сможет указать переводы приветствия.

1. Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.ts**.

2. Добавьте новую переменную класса **greetingFields** в класс **GreetingWebPart**:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...
    private greetingFields: IPropertyPaneField<any>[] = [];
    // ...
  }
  ```

3. Замените оператор **import** для пакета **@microsoft/sp-webpart-base** следующим кодом:

  ```typescript
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneTextField,
    IPropertyPaneField
  } from '@microsoft/sp-webpart-base';
  ```

4. Измените метод **propertyPaneSettings**, чтобы он получал список текстовых полей из новой переменной класса **greetingFields**:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...

      protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.GreetingGroupName,
                groupFields: this.greetingFields
              }
            ]
          }
        ]
      };
    }

    // ...
  }
  ```

  Если на сайте включено несколько языков, то в веб-части отображается несколько полей, в которых пользователь сможет ввести приветствие. Чтобы пользователям было понятно, что эти поля связаны друг с другом, поместите их в отдельную группу. 
  
5. В редакторе кода откройте файл **./src/webparts/greeting/loc/mystrings.d.ts** и измените его код на следующий:

  ```typescript
  declare interface IGreetingWebPartStrings {
    PropertyPaneDescription: string;
    GreetingGroupName: string;
    LearnMoreButtonLabel: string;
  }

  declare module 'GreetingWebPartStrings' {
    const strings: IGreetingWebPartStrings;
    export = strings;
  }
  ```

6. Обновите файлы ресурсов соответствующим образом, чтобы указать значения строки **GreetingGroupName**.

  **./src/webparts/greeting/loc/en-us.js**

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Greeting web part configuration",
      "GreetingGroupName": "Greeting to show in the web part",
      "LearnMoreButtonLabel": "Learn more"
    }
  });
  ```

  **./src/webparts/greeting/loc/nl-nl.js**

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
      "GreetingGroupName": "Begroeting die in het webonderdeel getoond wordt",
      "LearnMoreButtonLabel": "Meer informatie"
    }
  });
  ```

  **./src/webparts/greeting/loc/qps-ploc.js**

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "[!!! Gřèèƭïñϱ ωèβ ƥářƭ çôñƒïϱúřáƭïôñ ℓôřè₥ ïƥƨú !!!]",
      "GreetingGroupName": "[!!! Gřèèƭïñϱ ƭô ƨλôω ïñ ƭλè ωèβ ƥářƭ ℓôřè₥ ïƥƨú !!!]",
      "LearnMoreButtonLabel": "[!!! £èářñ ₥ôřè ℓôř !!!]"
    }
  });
  ```

7. В файле **./src/webparts/greeting/GreetingWebPart.ts** переопределите метод **onPropertyPaneConfigurationStart** с помощью следующего кода:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...
    protected onPropertyPaneConfigurationStart(): void {
      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'languages');

      this.getSupportedLanguageIds()
        .then((supportedLanguageIds: number[]): void => {
          this.greetingFields = [];
          supportedLanguageIds.forEach(localeId => {
            this.greetingFields.push(PropertyPaneTextField(`greeting_${localeId}`, {
              label: this.getLocaleName(localeId)
            }));
          });

          this.context.propertyPane.refresh();
          this.context.statusRenderer.clearLoadingIndicator(this.domElement);
          this.render();
        });
    }
  }
  ```

  Когда пользователь открывает область свойств веб-части, метод загружает сведения о языках, включенных на текущем сайте. Так как загрузка этих сведений может занять некоторое время, метод выводит индикатор загрузки. 
  
  После загрузки сведений о включенных языках метод создает текстовое поле области свойств, связанное с динамическим свойством веб-части **greeting__lcid_**, например **greeting_1033** для английского (США).
  
  Когда текстовые поля для всех включенных языков созданы, метод обновляет область свойств, вызывая метод **IPropertyPaneAccessor.refresh**. 
  
  После этого метод удаляет индикатор загрузки и обновляет веб-часть.

  ![Текстовые поля для всех включенных языков отображаются в области свойств веб-части](../../../images/localization-multilingual-properties.png)

### <a name="show-the-greeting-for-the-preferred-user-language"></a>Отображение приветствия на выбранном пользователем языке

Изначально в веб-части отображалось одно и то же приветствие для всех пользователей, независимо от языка, который они выбрали. Теперь, когда в веб-части сохранены различные переводы приветствия, оно должно отображаться на языке, выбранном текущим пользователем.

1. В файле **./src/webparts/greeting/GreetingWebPart.ts** замените метод **render** веб-части следующим кодом:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...

    public render(): void {
      const element: React.ReactElement<IGreetingProps> = React.createElement(Greeting, {
        greeting: this.getGreeting()
      });

      ReactDom.render(element, this.domElement);
    }
  }
  ```

2. В классе **GreetingWebPart** добавьте новый метод **getGreeting**:

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...

    private getGreeting(): string {
      let localeId: number = this.getLocaleId(this.context.pageContext.cultureInfo.currentUICultureName);
      if (localeId === 0) {
        localeId = 1033;
      }

      return this.properties[`greeting_${localeId}`];
    }

    // ...
  }
  ```

  Этот метод возвращает текущий язык и преобразует его в код языка. Затем он возвращает значение свойства greeting, переведенное на этот язык.

## <a name="localization-in-different-build-types"></a>Локализация в различных типах сборки

В зависимости от выбранного режима сборки SharePoint Framework обрабатывает файлы локализации по-разному. Ниже перечислены некоторые отличия между файлами, созданными в отладочной и конечной сборках.

### <a name="localization-files-in-the-debug-build"></a>Файлы локализации в отладочной сборке

При сборке проектов SharePoint Framework в режиме отладки в манифест веб-части включаются только сведения о языковом стандарте по умолчанию. В режиме отладки SharePoint Framework использует заданный по умолчанию языковой стандарт en-US либо языковой стандарт, указанный в настройках проекта или с помощью аргумента командной строки **locale**. 

Файлы ресурсов с переведенными строками не включаются в папку **dist**. SharePoint Framework загружает их в среде выполнения из промежуточной папки **lib**, используя путь в манифесте веб-части.

Проверив сведения о модуле **GreetingWebPartStrings** в манифесте веб-части, созданном во время отладочной сборки, вы увидите, что несмотря на разнообразие языковых стандартов, поддерживаемых веб-частью (en-US, nl-NL и qps-ploc), по умолчанию используется путь к файлу ресурсов en-US, хранящемуся в промежуточной папке.

```json
{
  "id": "edbc4e31-6085-4ffa-85f4-eeffcb0ea2d4",
  "alias": "GreetingWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,
  // ...
  "loaderConfig": {
    "entryModuleId": "greeting-web-part",
    "internalModuleBaseUrls": [
      "https://localhost:4321/"
    ],
    "scriptResources": {
      "greeting-web-part": {
        "type": "path",
        "path": "dist/greeting-web-part.js"
      },
      "GreetingWebPartStrings": {
        "defaultPath": "lib/webparts/greeting/loc/en-us.js",
        "type": "localizedPath",
        "paths": {
          "en-US": "lib/webparts/greeting/loc/en-us.js",
          "nl-NL": "lib/webparts/greeting/loc/nl-nl.js",
          "qps-ploc": "lib/webparts/greeting/loc/qps-ploc.js"
        }
      },
      // ...
    }
  }
}
```

### <a name="localization-files-in-the-release-build"></a>Файлы локализации в сборке выпуска

При сборке проектов SharePoint Framework в режиме выпуска в манифест веб-части включаются сведения обо всех доступных языковых стандартах. Кроме того, ресурсы для каждого языкового стандарта хранятся в отдельном файле. Эти файлы ресурсов вместе с манифестом и пакетом веб-части копируются в папку **./temp/deploy**.

> [!IMPORTANT] 
> В конечных сборках файлы ресурсов копируются только в папку **./temp/deploy** и не копируются в папку **./dist**. При развертывании веб-части в рабочей среде всегда следует использовать файлы из папки **./temp/deploy**. Тогда точно будут развернуты все файлы, необходимые для веб-части.

Проверив последний манифест веб-части, созданный в сборке выпуска, вы увидите, что теперь модуль **GreetingWebPartStrings** содержит ссылки на все поддерживаемые языковые стандарты.

```json
{
  "id": "edbc4e31-6085-4ffa-85f4-eeffcb0ea2d4",
  "alias": "GreetingWebPart",
  "componentType": "WebPart",
  "version": "0.0.1",
  "manifestVersion": 2,
  // ...
  "loaderConfig": {
    "entryModuleId": "greeting-web-part",
    "internalModuleBaseUrls": [
      "https://cdn.contoso.com/"
    ],
    "scriptResources": {
      "greeting-web-part": {
        "type": "path",
        "path": "greeting-web-part_159d9eb591c6716cae6d0ff15b78a19a.js"
      },
      "GreetingWebPartStrings": {
        "defaultPath": "react-localization-greetingwebpartstrings_en-us_b5e89eba6e8d819bf1647b3ab505dae5.js",
        "type": "localizedPath",
        "paths": {
          "en-US": "react-localization-greetingwebpartstrings_en-us_b5e89eba6e8d819bf1647b3ab505dae5.js",
          "nl-NL": "react-localization-greetingwebpartstrings_nl-nl_d6e80ff75385975e7737774e0802641e.js",
          "qps-ploc": "react-localization-greetingwebpartstrings_qps-ploc_effe5ee4af9cadee91bbf84327eb7308.js"
        }
      },
      // ...
    }
  }
}
```

При загрузке веб-части на странице SharePoint Framework автоматически загружает файл ресурсов для соответствующего языкового стандарта, используя сведения с сайта контекста. Если соответствующий файл ресурсов не найден, SharePoint Framework загружает файл, указанный в свойстве **defaultPath**. 

Благодаря разделению файлов ресурсов SharePoint Framework может загружать на странице данные только для того языкового стандарта, который используется на сайте.

## <a name="see-also"></a>См. также

- [Обзор SharePoint Framework](../../sharepoint-framework-overview.md)