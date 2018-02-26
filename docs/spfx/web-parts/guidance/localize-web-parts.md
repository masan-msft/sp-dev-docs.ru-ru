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
# <a name="localize-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="3ec4e-103">Локализация клиентских веб-частей SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="3ec4e-103">Localize SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="3ec4e-p101">Вы можете увеличить привлекательность клиентской веб-части SharePoint Framework, локализовав ее для пользователей SharePoint по всему миру. В этой статье показано, как локализовать веб-часть на нидерландский язык (Нидерланды) и проверить, отображаются ли правильно локализованные значения.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-p101">You can broaden the appeal of your SharePoint Framework client-side web part by localizing it for different languages spoken by SharePoint users all over the world. In this article, you will localize a web part to the Dutch (Netherlands) locale, and verify that the localized values are displayed correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="3ec4e-106">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки для создания клиентских веб-частей SharePoint](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-106">Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="prepare-the-project"></a><span data-ttu-id="3ec4e-107">Подготовка проекта</span><span class="sxs-lookup"><span data-stu-id="3ec4e-107">Prepare the project</span></span>

### <a name="create-a-new-project"></a><span data-ttu-id="3ec4e-108">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="3ec4e-108">Create a new project</span></span>

1. <span data-ttu-id="3ec4e-109">Создайте папку для проекта.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-109">Create a new folder for your project:</span></span>

  ```sh
  md react-localization
  ```

2. <span data-ttu-id="3ec4e-110">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-110">Go to the project folder.</span></span>

  ```sh
  cd react-localization
  ```

3. <span data-ttu-id="3ec4e-111">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-111">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="3ec4e-112">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-112">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="3ec4e-113">**react-localization** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-113">**react-localization** as your solution name.</span></span>
  - <span data-ttu-id="3ec4e-114">**SharePoint Online only (latest)** (Только SharePoint Online, последняя версия) в качестве набора базовых пакетов;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-114">**SharePoint Online only (latest)** as the baseline package set.</span></span>
  - <span data-ttu-id="3ec4e-115">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-115">**Use the current folder** for the location to place the files.</span></span>
  - <span data-ttu-id="3ec4e-116">**y** для того, чтобы можно было выполнять развертывание на уровне клиента;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-116">**y** to allow tenant-wide deployment.</span></span>
  - <span data-ttu-id="3ec4e-117">**WebPart** (Веб-часть) в качестве типа создаваемого компонента;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-117">**WebPart** as the type of component to develop.</span></span>
  - <span data-ttu-id="3ec4e-118">**Greeting** (Приветствие) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-118">**Greeting** as your web part name.</span></span>
  - <span data-ttu-id="3ec4e-119">**Greets the user** (Приветствие пользователя) в качестве описания веб-части;</span><span class="sxs-lookup"><span data-stu-id="3ec4e-119">**Greets the user** as your web part description.</span></span>
  - <span data-ttu-id="3ec4e-120">**React** в качестве отправной точки создания веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-120">**React** as the starting point to build the web part.</span></span>

  <br/>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/localization-yo-sharepoint.png)

5. <span data-ttu-id="3ec4e-122">После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-122">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="3ec4e-123">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-123">Open your project folder in your code editor.</span></span> <span data-ttu-id="3ec4e-124">В этой статье в инструкциях и на снимках экрана используется Visual Studio Code, но вы можете использовать любой другой редактор.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-124">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span>

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/localization-visual-studio-code.png)

### <a name="replace-the-default-code"></a><span data-ttu-id="3ec4e-126">Замена кода по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3ec4e-126">Replace the default code</span></span>

1. <span data-ttu-id="3ec4e-127">В редакторе кода откройте файл **./src/webparts/greeting/GreetingWebPart.ts** и замените определение интерфейса `IGreetingWebPartProps` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-127">In the code editor, open the **./src/webparts/greeting/GreetingWebPart.ts** file and update the definition of the `IGreetingWebPartProps` interface to the following code:</span></span>

  ```typescript
  export interface IGreetingWebPartProps {
    greeting: string;
  }
  ```

2. <span data-ttu-id="3ec4e-128">В том же файле замените класс **GreetingWebPart** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-128">Next, in the same file and change the **GreetingWebPart** class to:</span></span>

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

3. <span data-ttu-id="3ec4e-129">Обновите основной компонент React. Для этого откройте файл **./src/webparts/greeting/components/Greeting.tsx** и вставьте следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-129">Update the main React component by opening the **./src/webparts/greeting/components/Greeting.tsx** file and changing its code to:</span></span>

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

4. <span data-ttu-id="3ec4e-130">Обновите интерфейс основного компонента React, открыв файл **./src/webparts/greeting/components/IGreetingProps.tsx** и заменив код на следующий:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-130">Update the main React component interface by opening the **./src/webparts/greeting/components/IGreetingProps.tsx** file and changing its code to:</span></span>

  ```tsx
  import { IGreetingWebPartProps } from '../GreetingWebPart';

  export interface IGreetingProps extends IGreetingWebPartProps {
  }
  ```

5. <span data-ttu-id="3ec4e-131">Обновите файл определения типа локализации TypeScript, открыв файл **./src/webparts/greeting/loc/mystrings.d.ts** и заменив код на следующий:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-131">Update the localization TypeScript type definition file by opening the **./src/webparts/greeting/loc/mystrings.d.ts** file and changing its code to:</span></span>

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

6. <span data-ttu-id="3ec4e-132">Обновите файл английского языка (США). Для этого откройте файл **./src/webparts/greeting/loc/en-us.js** и вставьте следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-132">Update the US English locale file by opening the **./src/webparts/greeting/loc/en-us.js** file and changing its code to:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Greeting web part configuration",
      "DisplayGroupName": "Display",
      "GreetingFieldLabel": "Greeting to show in the web part"
    }
  });
  ```

7. <span data-ttu-id="3ec4e-133">В манифесте веб-части обновите значение по умолчанию для свойства **greeting**, открыв файл **./src/webparts/greeting/GreetingWebPart.manifest.json** и заменив раздел **properties** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-133">In the web part manifest update the default value of the **greeting** property by opening the **./src/webparts/greeting/GreetingWebPart.manifest.json** file and changing the **properties** section to:</span></span>

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

8. <span data-ttu-id="3ec4e-134">Проверьте, правильно ли применены все изменения, с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-134">Verify that you have applied all changes correctly by running the following command:</span></span>

  ```sh
  gulp serve
  ```

9. <span data-ttu-id="3ec4e-135">В SharePoint Workbench добавьте веб-часть на страницу и откройте ее конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-135">In the SharePoint workbench add the web part to the page and open its configuration.</span></span>

  ![Веб-часть приветствия добавлена на страницу, область свойств открыта](../../../images/localization-initial-changes.png)

## <a name="localize-the-web-part-manifest"></a><span data-ttu-id="3ec4e-137">Локализация манифеста веб-части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-137">Localize the web part manifest</span></span>

<span data-ttu-id="3ec4e-138">Каждая клиентская веб-часть SharePoint Framework состоит из кода и манифеста.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-138">Every SharePoint Framework client-side web part consists of code and a manifest.</span></span> <span data-ttu-id="3ec4e-139">Манифест содержит сведения о веб-части, такие как название, описание и значок.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-139">The manifest provides information about the web part such as its title, description, and icon.</span></span> <span data-ttu-id="3ec4e-140">При добавлении веб-части на страницу пользователи видят сведения из ее манифеста.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-140">When adding a web part to the page, the information from the web part manifest is displayed to users.</span></span> 

<span data-ttu-id="3ec4e-141">Эти сведения помогают пользователю решить, нужна ли ему данная веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-141">Using this information, users decide if the web part is the one that they are looking for.</span></span> <span data-ttu-id="3ec4e-142">Название и описание должны правильно отражать функциональность веб-части, если вы хотите, чтобы ею пользовались.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-142">Providing a title and description that correctly reflect the web part's functionality is essential if you want your web part to be used.</span></span> <span data-ttu-id="3ec4e-143">Если веб-часть используется не только на англоязычных сайтах, то локализация метаданных сделает ее еще удобнее для пользователей.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-143">If your web part is used on non-English sites, localizing its metadata can improve the user experience even further.</span></span>

<span data-ttu-id="3ec4e-144">В манифесте веб-части можно указывать локализованные значения некоторых свойств, например названия и описания.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-144">Some properties defined in the web part manifest, such as title or description, support specifying localized values.</span></span> <span data-ttu-id="3ec4e-145">Полный список всех свойств манифеста веб-части, поддерживающих локализацию, см. в статье [Упрощенное добавление веб-частей с помощью предварительно настроенных записей](./simplify-adding-web-parts-with-preconfigured-entries.md#properties-of-a-preconfiguredentries-array-item).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-145">For the complete list of all web part manifest properties that support localization read the [Simplify adding web parts with preconfigured entries](./simplify-adding-web-parts-with-preconfigured-entries.md#properties-of-a-preconfiguredentries-array-item) article.</span></span> 

<span data-ttu-id="3ec4e-146">Свойства, поддерживающие локализацию, относятся к типу **ILocalizedString**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-146">Properties that support localization are of type **ILocalizedString**.</span></span> <span data-ttu-id="3ec4e-147">Для каждой локализованной строки должно быть указано по крайней мере значение по умолчанию (при необходимости можно указать значения для других языковых стандартов).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-147">Each localized string must specify at least the default value and optionally values for other locales.</span></span>

### <a name="add-localized-values-for-title-description-and-group-name"></a><span data-ttu-id="3ec4e-148">Добавление локализованных значений для названия, описания и имени группы</span><span class="sxs-lookup"><span data-stu-id="3ec4e-148">Add localized values for title, description, and group name</span></span>

1. <span data-ttu-id="3ec4e-149">Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-149">In the code editor open the **./src/webparts/greeting/GreetingWebPart.manifest.json** file.</span></span> 

2. <span data-ttu-id="3ec4e-150">В массиве **preconfiguredEntries** добавьте переводы для свойств **title**, **description** и **group** на нидерландском языке (Нидерланды), вставив следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-150">In the **preconfiguredEntries** array add translations for the **title**, **description**, and **group** properties in Dutch (Netherlands), by changing the code to:</span></span>

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

3. <span data-ttu-id="3ec4e-151">Чтобы проверить, работает ли проект, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-151">Run the following command to verify that the project is working:</span></span>

  ```sh
  gulp serve
  ```

> [!NOTE] 
> <span data-ttu-id="3ec4e-152">К сожалению, в настоящее время в SharePoint Workbench невозможно просматривать локализованные значения из манифеста веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-152">Unfortunately, the SharePoint workbench doesn't currently support previewing the localized values from the web part manifest.</span></span> <span data-ttu-id="3ec4e-153">Всегда используется перевод по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-153">It always uses the default translation.</span></span>

## <a name="localize-the-web-part-property-pane"></a><span data-ttu-id="3ec4e-154">Локализация области свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-154">Localize the web part property pane</span></span>

<span data-ttu-id="3ec4e-155">Пользователям часто приходится настраивать веб-часть для конкретных нужд.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-155">When working with a web part, a user often needs to configure it for their specific needs.</span></span> <span data-ttu-id="3ec4e-156">Подписав параметры конфигурации, вы можете сделать веб-часть удобнее для пользователей и сократить количество обращений в службу поддержки за помощью в настройке.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-156">When working with web parts users often need to configure it for their specific needs. Providing descriptive labels for the different configuration settings improves the usability of the web part, and decreases the number of support requests from users for help configuring web parts.</span></span>

<span data-ttu-id="3ec4e-157">Область свойств веб-части состоит из нескольких разделов.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-157">The web part property pane consists of sections.</span></span> <span data-ttu-id="3ec4e-158">В каждом разделе есть заголовок и один или несколько элементов, с помощью которых пользователи могут настраивать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-158">Each section has a header and one or more controls that allow users to configure the web part.</span></span> <span data-ttu-id="3ec4e-159">Каждый из этих элементов содержит описание его назначения.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-159">Each of these controls contains a label that describes its purpose.</span></span> 

<span data-ttu-id="3ec4e-160">По умолчанию веб-части загружают строковые подписи из файла ресурсов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-160">By default, web parts load the string labels from a JavaScript resource file.</span></span> <span data-ttu-id="3ec4e-161">Если вы создавали классические веб-части с помощью решений с полным доверием, они похожи на RESX-файлы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-161">If you've built classic web parts with full-trust solutions, they resemble .resx resource files.</span></span> <span data-ttu-id="3ec4e-162">Использовать эти файлы ресурсов необязательно, строки можно включать непосредственно в код.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-162">It's not required to use these resource files, and you could include the strings directly in code.</span></span> <span data-ttu-id="3ec4e-163">Однако настоятельно рекомендуем использовать такие файлы.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-163">However, it's highly recommended that you use resource files.</span></span> <span data-ttu-id="3ec4e-164">Немного дополнительных служебных данных — ничего по сравнению с усилиями, необходимыми для извлечения всех подписей, если впоследствии вам потребуется перевести веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-164">The little additional overhead they add outweighs the effort required to extract all labels afterwards should you need to translate the web part later on.</span></span>

<span data-ttu-id="3ec4e-165">Файлы локализации, используемые веб-частью, хранятся в папке **./src/webparts/greeting/loc**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-165">The localization files used by the web part are stored in the **./src/webparts/greeting/loc** folder.</span></span>

![Файлы локализации, используемые клиентской веб-частью SharePoint Framework, выделенные в Visual Studio Code](../../../images/localization-loc-folder.png)

<br/>

<span data-ttu-id="3ec4e-167">Папка **loc** содержит файл определения типа TypeScript (**./src/webpart/greeting/loc/mystrings.d.ts**), который сообщает TypeScript о различных строках в локализованных файлах.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-167">The **loc** folder contains a TypeScript type definition file (**./src/webpart/greeting/loc/mystrings.d.ts**) that informs TypeScript of the different strings included in the localized files.</span></span> <span data-ttu-id="3ec4e-168">На основе сведений из этого файла редактор кода может предоставлять подсказки IntelliSense при работе со строками в коде.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-168">Using the information from this file, your code editor can provide you with IntelliSense when working with strings in code.</span></span> <span data-ttu-id="3ec4e-169">Кроме того, при сборке проекта TypeScript может проверять, не ссылаетесь ли вы на неопределенные строки.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-169">Additionally, while building your project, TypeScript can verify that you're not referring to a string that hasn't been defined.</span></span>

![Подсказки IntelliSense для локализованных строк в Visual Studio Code](../../../images/localization-intellisense.png)

<br/>

<span data-ttu-id="3ec4e-171">Переведенные строки для каждого языкового стандарта, поддерживаемого веб-частью, содержатся в обычном файле JavaScript (не TypeScript) с именем в нижнем регистре (например, **en-us.js**).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-171">For each locale supported by your web part, there is also a plain JavaScript file (not TypeScript) named in lowercase after the locale (for example **en-us.js**) containing the translated strings.</span></span>

![Шаблон стандартного файла локализации, сформированный с новым проектом SharePoint Framework](../../../images/localization-standard-locale-file.png)

<br/>

> [!IMPORTANT] 
> <span data-ttu-id="3ec4e-173">Внимательно проверяйте, чтобы все ключи, указанные в файле определения типа TypeScript как локализуемые, были переведены во всех файлах локализации JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-173">Important: You should pay extra attention to verifying that all keys specified in the TypeScript type definition file for localization have translations in all localization JavaScript files.</span></span>

<span data-ttu-id="3ec4e-174">По умолчанию в SharePoint Framework используется языковой стандарт en-US.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-174">en-US is the default locale used by the SharePoint Framework.</span></span> <span data-ttu-id="3ec4e-175">Если языковой стандарт сайта не поддерживается веб-частью, SharePoint Framework использует языковой стандарт по умолчанию (en-US).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-175">If your web part is used on a site using a locale not supported by your web part, the SharePoint Framework will use en-US as the default locale.</span></span> 

<span data-ttu-id="3ec4e-176">Чтобы переопределить этот параметр, создайте файл языкового стандарта **default.js** со значениями на предпочитаемом языке.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-176">You can override this behavior by creating a locale file named **default.js** with the translations in your preferred language.</span></span> <span data-ttu-id="3ec4e-177">Имя **default.js** не соответствует соглашению об именовании языковых стандартов, но оно дает указание SharePoint Framework использовать этот файл языкового стандарта, а не английский язык (США).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-177">While the name **default.js** doesn't follow the locale naming convention, it signals to the SharePoint Framework build process to use that particular locale file as the fallback locale instead of the standard US English locale.</span></span>

### <a name="add-localized-values-for-web-part-property-pane-strings"></a><span data-ttu-id="3ec4e-178">Добавление локализованных значений для строк области свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-178">Add localized values for web part property pane strings</span></span>

1. <span data-ttu-id="3ec4e-179">В папке **./src/webparts/greetings/loc** создайте файл **nl-nl.js** и введите следующий код:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-179">In the **./src/webparts/greetings/loc** folder create new file named **nl-nl.js** and enter the following code:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
      "DisplayGroupName": "Weergave",
      "GreetingFieldLabel": "Begroeting die in het webonderdeel getoond wordt"
    }
  });
  ```

2. <span data-ttu-id="3ec4e-180">Убедитесь, что ключи в файле определения типа TypeScript для локализации соответствуют содержимому файлов языковых стандартов в случае английского (США) и нидерландского (Нидерланды) языков.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-180">Verify that the keys in the TypeScript type definition file for localization match the contents of the locale files for US English and Dutch (Netherlands).</span></span>

  ![Файл определения типа TypeScript для локализации и файлы языковых стандартов для английского (США) и нидерландского (Нидерланды) языков, открытые рядом в Visual Studio Code](../../../images/localization-keys-comparison.png)

### <a name="verify-the-localized-web-part-property-pane-strings"></a><span data-ttu-id="3ec4e-182">Проверка локализованных строк в области свойств веб части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-182">Verify the localized web part property pane strings</span></span>

<span data-ttu-id="3ec4e-183">При проверке веб-частей с помощью размещенной версии SharePoint Workbench или сайтов групп в клиенте разработчика по умолчанию используется языковой стандарт сайта контекста, выраженный свойством **spPageContextInfo.currentUICultureName**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-183">When testing web parts using the hosted version of the SharePoint workbench or team sites on a developer tenant the locale of the context site expressed by the **spPageContextInfo.currentUICultureName** property is used as the default locale.</span></span> 

<span data-ttu-id="3ec4e-184">При проверке веб-частей с помощью локальной версии SharePoint Workbench SharePoint Framework по умолчанию использует языковой стандарт en-US для отображения строк области свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-184">When testing web parts using the local SharePoint workbench, the SharePoint Framework uses by default the en-US locale to display web part property pane strings.</span></span> <span data-ttu-id="3ec4e-185">Проверить значения из других языковых стандартов, поддерживаемых веб-частью, можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-185">There are two ways in which you can test the values from other locales supported by your web part.</span></span>

#### <a name="specify-the-locale-to-be-tested-in-the-project-configuration"></a><span data-ttu-id="3ec4e-186">Указание проверяемого языкового стандарта в конфигурации проекта</span><span class="sxs-lookup"><span data-stu-id="3ec4e-186">Specify the locale to be tested in the project configuration</span></span>

<span data-ttu-id="3ec4e-187">Чтобы указать проверяемый языковой стандарт в SharePoint Workbench, можно изменить конфигурацию проекта.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-187">One way to specify the locale to be tested in the SharePoint workbench is by editing the project configuration.</span></span> <span data-ttu-id="3ec4e-188">Этот способ удобен, если вы и ваши коллеги работаете с языковым стандартом в течение долгого времени или создаете веб-часть, которая не поддерживает английский язык (США).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-188">This approach is useful if you and your team members are working with a locale for a longer period of time or if you're building a web part that doesn't support US English.</span></span> 

1. <span data-ttu-id="3ec4e-189">В редакторе кода откройте файл **./config/write-manifests.json** и вставьте следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-189">In the code editor open the **./config/write-manifests.json** file and change its code to:</span></span>

  ```json
  {
    "cdnBasePath": "<!-- PATH TO CDN -->",
    "debugLocale": "nl-nl"
  }
  ```

2. <span data-ttu-id="3ec4e-190">Запустите SharePoint Workbench с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-190">Start the SharePoint workbench by running the following command:</span></span>

  ```sh
  gulp serve
  ```

  <span data-ttu-id="3ec4e-191">Добавив веб-часть на страницу и открыв ее конфигурацию, вы увидите, что строки в области свойств веб-части отображаются на нидерландском языке (Нидерланды).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-191">When you add the web part to the page and open its configuration you will see the strings in the web part property pane displayed in Dutch (Netherlands).</span></span>

  ![Строка области свойств веб-части на нидерландском языке (Нидерланды)](../../../images/localization-property-pane-nl-nl.png)

#### <a name="specify-the-locale-to-be-tested-by-using-the-command-line-argument"></a><span data-ttu-id="3ec4e-193">Указание проверяемого языкового стандарта с помощью аргумента командной строки</span><span class="sxs-lookup"><span data-stu-id="3ec4e-193">Specify the locale to be tested using the command line argument</span></span>

<span data-ttu-id="3ec4e-194">Еще один способ задать языковой стандарт, который будет использоваться локальной областью SharePoint Workbench, — указать его в качестве аргумента задачи gulp.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-194">Another way to specify the locale to be used by the local SharePoint workbench is to specify it as an argument for the gulp task. Start the SharePoint workbench by running the following command:</span></span> 

- <span data-ttu-id="3ec4e-195">Запустите SharePoint Workbench с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-195">Start the SharePoint workbench by running the following command:</span></span>

  ```sh
  gulp serve --locale=nl-nl
  ```

  <span data-ttu-id="3ec4e-196">Открыв конфигурацию веб-части, вы увидите, что все строки в области свойств отображаются на нидерландском (Нидерланды), а не на английском языке (США), используемом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-196">Once again, when you open your web part's configuration you will see that all property pane strings are displayed in Dutch (Netherlands) rather than the default US English.</span></span>

  ![Строка области свойств веб-части на нидерландском языке (Нидерланды)](../../../images/localization-property-pane-nl-nl.png)

## <a name="localize-web-part-contents"></a><span data-ttu-id="3ec4e-198">Локализация содержимого веб-части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-198">Localize web part contents</span></span>

<span data-ttu-id="3ec4e-199">Необходимо локализовать не только строки в области свойств веб части, но и все строки, отображаемые в веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-199">The same way that you localize web part property pane strings, you should localize all strings displayed by the web part in its body.</span></span> <span data-ttu-id="3ec4e-200">Для этого можно воспользоваться тем же способом, что и при локализации строк в области свойств.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-200">You can use the same approach that you use when localizing web part property pane strings.</span></span> <span data-ttu-id="3ec4e-201">Добавьте ключ в файле определения TypeScript для каждой локализуемой строки и переведите ее на каждый из поддерживаемых языков в файле JavaScript соответствующего языкового стандарта.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-201">The same way you localize web part property pane strings, you should localize all strings displayed by the web part in its body. You can use the same approach that you use when localizing web part property pane strings. For every string to be localized, add a key in the localization TypeScript definition file, and then translate the string to each of the supported locales in the corresponding locale JavaScript file.</span></span>

### <a name="globalize-the-web-part-strings"></a><span data-ttu-id="3ec4e-202">Глобализация строк веб части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-202">Globalize the web part strings</span></span>

<span data-ttu-id="3ec4e-203">Строки стандартной веб-части, созданной на основе шаблонного проекта SharePoint Framework, внедрены в код.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-203">The default web part provided with the scaffolded SharePoint Framework project has its strings embedded in the code.</span></span> <span data-ttu-id="3ec4e-204">Прежде чем локализовать эти строки, необходимо заменить их ссылками на локализованные строки.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-204">Before you can localize these strings you have to replace them with references to the localized strings.</span></span> <span data-ttu-id="3ec4e-205">Этот процесс часто называют **глобализацией** или **интернационализацией** (или просто **i18n**).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-205">This process is often referred to as **globalization** or **internationalization** (or **i18n** for short).</span></span>

1. <span data-ttu-id="3ec4e-206">В редакторе кода откройте файл **./src/webparts/greeting/components/Greetings.tsx**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-206">In the code editor, open the **./src/webparts/greeting/components/Greetings.tsx** file.</span></span> 

2. <span data-ttu-id="3ec4e-207">В верхней части файла, сразу же после последнего оператора `import`, добавьте ссылку на локализованные строки:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-207">In the top section of the file, directly after the last `import` statement, add a reference to the localized strings:</span></span>

  ```typescript
  import * as strings from 'GreetingWebPartStrings';
  ```

3. <span data-ttu-id="3ec4e-208">Замените содержимое класса **Greeting** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-208">Next, replace the contents of the **Greeting** class with the following code:</span></span>

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

### <a name="add-the-new-string-to-the-localization-typescript-type-definition-file"></a><span data-ttu-id="3ec4e-209">Добавление новой строки в файл определения типа локализации TypeScript</span><span class="sxs-lookup"><span data-stu-id="3ec4e-209">Add the new string to the localization TypeScript type definition file</span></span>

<span data-ttu-id="3ec4e-210">После замены строки на ссылку нужно добавить эту строку в файлы локализации, используемые веб-частью.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-210">Having replaced the string with a reference, the next step is to add that string to the localization files used by the web part.</span></span> 

- <span data-ttu-id="3ec4e-211">В редакторе кода откройте файл **./src/webparts/greetings/loc/mystrings.d.ts** и вставьте следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-211">In the code editor open the **./src/webparts/greetings/loc/mystrings.d.ts** file, and change its code to:</span></span>

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

### <a name="add-localized-values-for-the-new-string"></a><span data-ttu-id="3ec4e-212">Добавление локализованных значений для новой строки</span><span class="sxs-lookup"><span data-stu-id="3ec4e-212">Add localized values for the new string</span></span>

<span data-ttu-id="3ec4e-213">Вам осталось лишь указать локализованные версии для новой строки во всех языковых стандартах, поддерживаемых веб-частью.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-213">The last step is to provide localized versions for the new string in all locales supported by the web part.</span></span> 

1. <span data-ttu-id="3ec4e-214">В редакторе кода откройте файл **./src/webparts/greeting/loc/en-us.js** и вставьте следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-214">In the code editor, open the **./src/webparts/greeting/loc/en-us.js** file and change its code to:</span></span>

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

2. <span data-ttu-id="3ec4e-215">Откройте файл **./src/webparts/greeting/loc/nl-nl.js** и вставьте следующий код вместо существующего:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-215">Next, open the **./src/webparts/greeting/loc/nl-nl.js** file and change its code to:</span></span>

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

3. <span data-ttu-id="3ec4e-216">Проверьте, правильно ли отображается переведенная строка, с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-216">Confirm that the translated string is correctly displayed by running the following command:</span></span>

  ```sh
  gulp serve --locale=nl-nl
  ```

  <br/>

  ![Кнопка "Подробнее" на нидерландском языке (Нидерланды)](../../../images/localization-learn-more-nl-nl.png)

## <a name="improve-globalizing-and-localizing-web-parts-by-using-pseudo-locales"></a><span data-ttu-id="3ec4e-218">Как улучшить глобализацию и локализацию веб-частей с помощью псевдолокалей</span><span class="sxs-lookup"><span data-stu-id="3ec4e-218">Improve globalizing and localizing web parts using pseudo-locales</span></span>

<span data-ttu-id="3ec4e-219">Локализация веб-частей во время разработки имеет явные преимущества, но разработчики часто ею пренебрегают.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-219">Using localization when building web parts offers clear benefits but is also something that developers overlook easily.</span></span> <span data-ttu-id="3ec4e-220">Часто проект переводят в конце, и тест-инженерам трудно проверить, весь ли код поддерживает другие языковые стандарты.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-220">Using localization when building web parts offers clear benefits but is also something that developers overlook easily. Often, translations to other locales are provided later in the project and it's hard for testers to verify that all code will properly support the different locales.</span></span>

<span data-ttu-id="3ec4e-221">Одни и те же слова на разных языках имеют разную длину.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-221">The same words in different locales have different lengths.</span></span> <span data-ttu-id="3ec4e-222">Например, предложение, переведенное с английского на немецкий или нидерландский, может стать на 35 % длиннее.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-222">For example, the same sentence translated from English to German or Dutch can become 35% longer.</span></span> <span data-ttu-id="3ec4e-223">Если перевод не доступен заранее, разработчикам и дизайнерам трудно проверить, поместятся ли длинные строки в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-223">Without all translations available upfront, it's difficult for developers and designers to ensure that the user interface can properly accommodate longer strings.</span></span>

<span data-ttu-id="3ec4e-p120">В некоторых языках используются специальные знаки, кроме стандартного набора символов ASCII. Если разработчики используют нестандартный шрифт, некоторые специальные знаки могут не поддерживаться.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-p120">Some languages use special characters beyond the standard ASCII character set. If designers use a non-standard font, it is possible that the font doesn't properly support some special characters.</span></span>

<span data-ttu-id="3ec4e-p121">Если вы узнаете обо всех этих проблемах в конце проекта, скорее всего, возникнут задержки и понадобятся дорогостоящие исправления. SharePoint Framework позволяет разработчикам использовать языковые псевдостандарты, чтобы решить эти проблемы при создании веб-частей.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-p121">Finding out about all these issues late in the project will likely lead to delays and costly fixes. The SharePoint Framework allows developers to use pseudo-locales to address these issues while building web parts.</span></span>

> [!TIP] 
> <span data-ttu-id="3ec4e-228">**Что такое псевдолокали?**</span><span class="sxs-lookup"><span data-stu-id="3ec4e-228">**What are pseudo-locales?**</span></span> <span data-ttu-id="3ec4e-229">Псевдолокали —это языковые стандарты, предназначенные для проверки поддержки специальных знаков, языков с письмом справа налево, размещения длинных строк в пользовательском интерфейсе и других аспектов локализации.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-229">Pseudo-locales are locales designed to test software for proper support of the different aspects of the localization process such as support for special characters, right-to-left languages, or accommodating longer strings in the user interface.</span></span>

### <a name="add-the-base-pseudo-locale"></a><span data-ttu-id="3ec4e-230">Добавление базовой псевдолокали</span><span class="sxs-lookup"><span data-stu-id="3ec4e-230">Add the base pseudo-locale</span></span>

1. <span data-ttu-id="3ec4e-231">В папке **./src/webparts/greeting/loc** добавьте новый файл **qps ploc.js** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-231">In the **./src/webparts/greeting/loc** folder, add a new file named **qps-ploc.js** and paste the following code:</span></span>

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
  > <span data-ttu-id="3ec4e-232">Вы можете преобразовать строки на английском (США), используя базовую псевдолокаль, на сайте [Pseudolocalize!](http://www.pseudolocalize.com).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-232">You can convert US English strings to their base pseudo-locale equivalent at [Pseudolocalize!](http://www.pseudolocalize.com).</span></span> <span data-ttu-id="3ec4e-233">Увеличив длину сгенерированной строки на 35 %, можно смоделировать длину строк, переведенных на более длинные языки, например немецкий или нидерландский.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-233">Tip: you can convert US English strings to their base pseudo-locale equivalent at http://www.pseudolocalize.com. By increasing the length of the generated string with 35% you should be able to simulate the length of strings translated to longer locales such as German or Dutch.</span></span> <span data-ttu-id="3ec4e-234">Кроме того, заключив переводы в скобки и восклицательные знаки, вам будет проще понять, помещается ли на экране вся строка.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-234">Additionally, by surrounding the translations with brackets and exclamation marks you can more easily see if the whole string is displayed on the screen.</span></span>

2. <span data-ttu-id="3ec4e-235">Проверьте проект с помощью базового языкового псевдостандарта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-235">Test the project using the base pseudo-locale by running the following command:</span></span>

  ```sh
  gulp serve --locale=qps-ploc
  ```

  <span data-ttu-id="3ec4e-236">После добавления веб-части на страницу вы сразу увидите, что две строки в веб-части не интернационализированы и отображаются на английском языке (США), а не на базовом языковом псевдостандарте.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-236">After adding the web part to the page, you can quickly see that there are two strings in the web part body that have not been internationalized and are still displayed in US English rather than in the base pseudo-locale.</span></span>

  ![Две строки в веб-части отображаются на английском языке (США), несмотря на проверку с использованием базовой псевдолокали](../../../images/localization-web-part-body-qps-ploc.png)

3. <span data-ttu-id="3ec4e-238">Откройте область свойств веб-части и убедитесь, что все строки и специальные знаки отображаются правильно и помещаются в отведенном для них месте.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-238">If you open the web part property pane, you can confirm that all strings and their special characters are displayed properly and that they fit in the available space correctly.</span></span>

  ![Область свойств веб-части во время проверки веб-части в локальной рабочей области при помощи базовой псевдолокали](../../../images/localization-web-part-property-pane-qps-ploc.png)

## <a name="localize-web-part-settings-values"></a><span data-ttu-id="3ec4e-240">Локализация значений параметров веб-части</span><span class="sxs-lookup"><span data-stu-id="3ec4e-240">Localize web part settings values</span></span>

<span data-ttu-id="3ec4e-241">SharePoint поддерживает многоязычный пользовательский интерфейс (MUI), где администратор сайта может включить несколько языков интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-241">Microsoft SharePoint supports Multilingual User Interface (MUI) where the site administrator can enable multiple languages for the user interface. When the user visits the site, its UI will automatically be displayed using the preferred language based on that user's preferences.</span></span> <span data-ttu-id="3ec4e-242">Сайт будет автоматически отображаться на языке, выбранном пользователем.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-242">Microsoft SharePoint supports Multilingual User Interface (MUI) where the site administrator can enable multiple languages for the user interface. When the user visits the site, its UI will automatically be displayed using the preferred language based on that user's preferences.</span></span>

<span data-ttu-id="3ec4e-243">Веб-части, используемые на многоязычных сайтах, должны автоматически определять текущий язык и отображать содержимое на этом языке.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-243">Web parts used on multilingual sites should automatically detect the currently used language and display their contents in that language.</span></span> <span data-ttu-id="3ec4e-244">SharePoint Framework упрощает этот процесс, автоматически загружая файл ресурсов, соответствующий текущему языку.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-244">The SharePoint Framework simplifies this process by automatically loading the resource file corresponding to the currently used language.</span></span> <span data-ttu-id="3ec4e-245">Кроме того, при проверке веб-частей SharePoint Framework с помощью размещенной версии SharePoint Workbench также автоматически используется язык, выбранный пользователем.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-245">Additionally, when testing SharePoint Framework web parts using the hosted version of the SharePoint Workbench, the Workbench also automatically uses the language preferred by the user.</span></span>

<span data-ttu-id="3ec4e-246">Значения, настроенные с помощью свойств веб-части, не хранятся в файлах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-246">Values configured through web part properties are not stored in resource files.</span></span> <span data-ttu-id="3ec4e-247">По умолчанию заданное значение используется как есть, что может привести к несоответствиям. Например, может отображаться приветствие на английском языке, в то время как пользователь выбрал нидерландский.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-247">Values configured through web part properties are not stored in resource files. By default, the configured value is used as-is, which might lead to inconsistencies such as greeting the user in English when the user's preferred language is Dutch.</span></span>

![Приветствие отображается на английском языке (США), несмотря на то что для рабочей области выбран нидерландский (Нидерланды)](../../../images/localization-english-greeting-dutch-workbench.png)

<br/>

<span data-ttu-id="3ec4e-249">Используя стандартные блоки, доступные в SharePoint Framework, вы можете сделать так, чтобы веб-часть хранила значения конфигурации на нескольких языках.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-249">Using the building blocks provided with the SharePoint Framework, you can extend your web part with support for storing web part configuration values in multiple languages. For each of the supported languages the property pane will display a separate text field in which the user can enter the translated value for that property.</span></span> <span data-ttu-id="3ec4e-250">Для каждого из поддерживаемых языков в области свойств отображается текстовое поле, где пользователь может ввести переведенное значение этого свойства.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-250">Using the building blocks provided with the SharePoint Framework, you can extend your web part with support for storing web part configuration values in multiple languages. For each of the supported languages the property pane will display a separate text field in which the user can enter the translated value for that property.</span></span>

![Несколько текстовых полей в области свойств веб-части, в которых можно ввести перевод значений](../../../images/localization-multilingual-properties.png)

> [!NOTE] 
> <span data-ttu-id="3ec4e-252">Для проверки веб-части, показанной в этой статье, используется многоязычный веб-сайт SharePoint с поддержкой английского (США), нидерландского и немецкого языков.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-252">The SharePoint site used to test the web part shown in this article is a multilingual site with the US English, Dutch, and German languages enabled.</span></span> <span data-ttu-id="3ec4e-253">Дополнительные сведения о включении дополнительных языков на сайтах SharePoint см. в статье [Выбор языков, которые должны быть доступны для пользовательского интерфейса сайта](https://support.office.com/ru-RU/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-253">For more information about enabling additional languages in SharePoint sites see the [Choose the languages you want to make available for a site’s user interface](https://support.office.com/ru-RU/article/Choose-the-languages-you-want-to-make-available-for-a-site-s-user-interface-16d3a83c-05ab-4b50-8fbb-ff576a3351e8) support article.</span></span>

### <a name="add-list-of-languages-supported-by-sharepoint-online"></a><span data-ttu-id="3ec4e-254">Добавление списка языков, поддерживаемых SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="3ec4e-254">Add list of languages supported by SharePoint Online</span></span>

<span data-ttu-id="3ec4e-255">Список языков, включенных на многоязычном сайте SharePoint, возвращается в виде массива кодов языка, например **1033** для английского (США).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-255">The list of languages enabled on a multilingual SharePoint site is returned as an array of locale identifiers (LCID).</span></span> 

<span data-ttu-id="3ec4e-256">Однако используемый в данный момент язык возвращается в виде строки, например **en-US** для английского (США).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-256">However, the currently used language is returned as a string, for example, **en-US** for US English.</span></span> <span data-ttu-id="3ec4e-257">Так как JavaScript не преобразовывает код языка в имя языкового стандарта и наоборот автоматически, вам нужно делать это самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-257">As JavaScript doesn't have a native way of converting the LCID number to the locale name, and vice-versa, you have to do it yourself.</span></span>

1. <span data-ttu-id="3ec4e-258">Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-258">In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file, and add a new class variable named supportedLanguageIds:</span></span> 

2. <span data-ttu-id="3ec4e-259">Добавьте переменную **locales** в уже имеющийся класс **GreetingWebPart**, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-259">In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file and add a new class variable named **locales** inside of existing **GreetingWebPart** with the following code:</span></span>

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

  <span data-ttu-id="3ec4e-260">В переменной **locales** указаны все языки, поддерживаемые SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-260">The **locales** variable lists all languages supported by SharePoint Online.</span></span>

3. <span data-ttu-id="3ec4e-261">Добавьте два метода class, которые будут преобразовывать имя языкового стандарта в код языка и наоборот:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-261">Next, add two class methods that will allow you to get the LCID from the locale name, and the locale name from the LCID:</span></span>

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

### <a name="remove-the-standard-greeting-web-part-property"></a><span data-ttu-id="3ec4e-262">Удаление стандартного свойства веб-части greeting</span><span class="sxs-lookup"><span data-stu-id="3ec4e-262">Remove the standard greeting web part property</span></span>

<span data-ttu-id="3ec4e-263">Изначально свойство **greeting** веб-части Greeting было определено, и пользователь мог указать приветствие, которое будет отображаться на экране.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-263">Originally, the Greeting web part had the **greeting** property defined where the user could specify the greeting to be displayed on the screen.</span></span> <span data-ttu-id="3ec4e-264">Чтобы веб-часть работала на многоязычных сайтах SharePoint, следует хранить несколько значений — по одному для каждого языка.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-264">To adapt the web part to support multilingual SharePoint sites, you need to store multiple values; one for each language.</span></span> <span data-ttu-id="3ec4e-265">Так как невозможно заранее узнать, какие языки будут включены на сайте, вы можете динамически генерировать свойства веб-части в среде выполнения, а не использовать одно статическое свойство.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-265">Because you cannot know up front which languages will be enabled on the site, rather than using one static web part property, you will dynamically generate web part properties at runtime.</span></span>

1. <span data-ttu-id="3ec4e-266">Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.manifest.json**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-266">In the code editor open the **./src/webparts/greeting/GreetingWebPart.manifest.json** file.</span></span> 

2. <span data-ttu-id="3ec4e-267">Удалите свойство **greeting** из свойства **properties**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-267">Remove the **greeting** property from the **properties** property:</span></span>

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

3. <span data-ttu-id="3ec4e-268">Откройте файл **./src/webparts/greeting/GreetingWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-268">Open the **./src/webparts/greeting/GreetingWebPart.ts** file.</span></span>

4. <span data-ttu-id="3ec4e-269">Удалите свойство **greeting** из определения интерфейса `IGreetingWebPartProps`:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-269">Remove the **** property from the `IGreetingWebPartProps` interface.</span></span>

  ```typescript
  export interface IGreetingWebPartProps {
  }
  ```

5. <span data-ttu-id="3ec4e-270">Так как основной компонент React должен показывать приветствие, откройте файл **./src/webparts/greeting/components/IGreetingProps.ts** и замените интерфейс **IGreetingProps** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-270">Because the main React component should display a greeting, open the **./src/webparts/greeting/components/IGreetingProps.ts** file, and change the **IGreetingProps** interface to:</span></span>

  ```typescript
  export interface IGreetingProps {
    greeting: string;
  }
  ```

  <span data-ttu-id="3ec4e-271">Это изменение позволяет передать приветствие из веб-части в компонент React.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-271">With this modification, you can pass the greeting to be displayed from the web part to the React component.</span></span>

### <a name="display-property-pane-text-fields-for-all-enabled-languages"></a><span data-ttu-id="3ec4e-272">Отображение текстовых полей области свойств для всех включенных языков</span><span class="sxs-lookup"><span data-stu-id="3ec4e-272">Display property pane text fields for all enabled languages</span></span>

<span data-ttu-id="3ec4e-273">Изначально пользователь мог настроить приветствие с помощью конфигурации веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-273">Initially, by using the web part configuration, the user could configure a welcome message.</span></span> <span data-ttu-id="3ec4e-274">Пользователь мог настроить одно значение, отображаемое для всех пользователей, независимо от их основного языка.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-274">The web part allowed the user to configure a single value that was displayed to all users no matter what their language preference was.</span></span> <span data-ttu-id="3ec4e-275">Получая список языков, включенных на текущем сайте, вы можете динамически показывать текстовые поля, чтобы пользователь мог добавлять в них переводы.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-275">By retrieving the list of languages enabled on the current site, you can dynamically display text fields to allow the user to provide translations for all the languages enabled on the site.</span></span>

#### <a name="load-information-about-languages-enabled-on-the-current-site"></a><span data-ttu-id="3ec4e-276">Загрузка сведений о языках, включенных на текущем сайте</span><span class="sxs-lookup"><span data-stu-id="3ec4e-276">Load information about languages enabled in the current site</span></span>

<span data-ttu-id="3ec4e-277">Прежде всего нужно загрузить сведения обо всех языках, включенных на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-277">The first step is to load the information about all languages enabled in the current site.</span></span> 

1. <span data-ttu-id="3ec4e-278">Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-278">In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file, and add a new class variable named supportedLanguageIds:</span></span> 

2. <span data-ttu-id="3ec4e-279">Добавьте новую переменную класса **supportedLanguageIds**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-279">Add a new class variable named **itemsDropdownDisabled**.</span></span>

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...
    private supportedLanguageIds: number[];
    // ...
  }
  ```

  <span data-ttu-id="3ec4e-280">Так как мы будем запрашивать данные в SharePoint, для выполнения операций воспользуемся HTTP-клиентом SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-280">Since we will be querying data in SharePoint, we will be using SharePoint Http Client for the operations.</span></span> 
  
3. <span data-ttu-id="3ec4e-281">Добавьте приведенные ниже операции импорта прямо перед классом **GreetingWebPart**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-281">Add following imports just above the **GreetingWebPart**.</span></span>

  ```typescript
  import {
    SPHttpClient,
    SPHttpClientResponse
  } from '@microsoft/sp-http';
  ```

4. <span data-ttu-id="3ec4e-282">В классе **GreetingWebPart** добавьте новый метод **getSupportedLanguageIds**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-282">Next, in the **GreetingWebPart** class, add a new method named **getSupportedLanguageIds**:</span></span>

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

<span data-ttu-id="3ec4e-283">Список языков, включенных на текущем сайте, достаточно загрузить один раз.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-283">The list of languages enabled on the current site should be loaded only once.</span></span> <span data-ttu-id="3ec4e-284">Если сведения о языках еще не загружены, метод использует стандартный HTTP-клиент SharePoint Framework, чтобы вызвать REST API SharePoint и получить сведения о языках, включенных на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-284">The list of languages enabled in the current site should be loaded only once. If the information about the languages hasn't been loaded yet, the method uses the standard SharePoint Framework HTTP Client to call the SharePoint REST API and retrieve the information about languages enabled on the current site.</span></span>

#### <a name="dynamically-render-text-fields-for-all-languages"></a><span data-ttu-id="3ec4e-285">Динамическая отрисовка текстовых полей для всех языков</span><span class="sxs-lookup"><span data-stu-id="3ec4e-285">Dynamically render text fields for all languages</span></span>

<span data-ttu-id="3ec4e-286">Теперь, когда вы можете получать сведения о языках, включенных на текущем сайте, для каждого из них будут отображаться текстовые поля, в которых пользователь сможет указать переводы приветствия.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-286">Now that you can retrieve the information about the languages enabled on the current site, you will display text fields for each of these languages so that the user can specify translated values for the greeting message.</span></span>

1. <span data-ttu-id="3ec4e-287">Откройте в редакторе кода файл **./src/webparts/greeting/GreetingWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-287">In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file, and add a new class variable named supportedLanguageIds:</span></span>

2. <span data-ttu-id="3ec4e-288">Добавьте новую переменную класса **greetingFields** в класс **GreetingWebPart**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-288">In the code editor, open the ./src/webparts/greeting/GreetingWebPart.ts file, and add a new class variable named **greetingFields** to the **GreetingWebPart** class:</span></span>

  ```typescript
  export default class GreetingWebPart extends BaseClientSideWebPart<IGreetingWebPartProps> {
    // ...
    private greetingFields: IPropertyPaneField<any>[] = [];
    // ...
  }
  ```

3. <span data-ttu-id="3ec4e-289">Замените оператор **import** для пакета **@microsoft/sp-webpart-base** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-289">Change the **import** statement for the **@microsoft/sp-webpart-base** package to:</span></span>

  ```typescript
  import {
    BaseClientSideWebPart,
    IPropertyPaneConfiguration,
    PropertyPaneTextField,
    IPropertyPaneField
  } from '@microsoft/sp-webpart-base';
  ```

4. <span data-ttu-id="3ec4e-290">Измените метод **propertyPaneSettings**, чтобы он получал список текстовых полей из новой переменной класса **greetingFields**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-290">Change the **propertyPaneSettings** getter to get the list of text fields from the newly added **greetingFields** class variable:</span></span>

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

  <span data-ttu-id="3ec4e-291">Если на сайте включено несколько языков, то в веб-части отображается несколько полей, в которых пользователь сможет ввести приветствие.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-291">If the site has multiple languages enabled, the web part will render multiple fields for the user to enter the greeting message.</span></span> <span data-ttu-id="3ec4e-292">Чтобы пользователям было понятно, что эти поля связаны друг с другом, поместите их в отдельную группу.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-292">To make it clear that these fields belong together, put them in a separate group.</span></span> 
  
5. <span data-ttu-id="3ec4e-293">В редакторе кода откройте файл **./src/webparts/greeting/loc/mystrings.d.ts** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-293">In the code editor, open the **./src/webparts/greeting/loc/mystrings.d.ts** file, and change its code to:</span></span>

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

6. <span data-ttu-id="3ec4e-294">Обновите файлы ресурсов соответствующим образом, чтобы указать значения строки **GreetingGroupName**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-294">Update the resource files accordingly to provide values for the **GreetingGroupName** string.</span></span>

  <span data-ttu-id="3ec4e-295">**./src/webparts/greeting/loc/en-us.js**</span><span class="sxs-lookup"><span data-stu-id="3ec4e-295">**./src/webparts/greeting/loc/en-us.js**:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Greeting web part configuration",
      "GreetingGroupName": "Greeting to show in the web part",
      "LearnMoreButtonLabel": "Learn more"
    }
  });
  ```

  <span data-ttu-id="3ec4e-296">**./src/webparts/greeting/loc/nl-nl.js**</span><span class="sxs-lookup"><span data-stu-id="3ec4e-296">**./src/webparts/greeting/loc/nl-nl.js**:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "Instellingen van het begroeting webonderdeel",
      "GreetingGroupName": "Begroeting die in het webonderdeel getoond wordt",
      "LearnMoreButtonLabel": "Meer informatie"
    }
  });
  ```

  <span data-ttu-id="3ec4e-297">**./src/webparts/greeting/loc/qps-ploc.js**</span><span class="sxs-lookup"><span data-stu-id="3ec4e-297">**./src/webparts/greeting/loc/qps-ploc.js**:</span></span>

  ```js
  define([], function() {
    return {
      "PropertyPaneDescription": "[!!! Gřèèƭïñϱ ωèβ ƥářƭ çôñƒïϱúřáƭïôñ ℓôřè₥ ïƥƨú !!!]",
      "GreetingGroupName": "[!!! Gřèèƭïñϱ ƭô ƨλôω ïñ ƭλè ωèβ ƥářƭ ℓôřè₥ ïƥƨú !!!]",
      "LearnMoreButtonLabel": "[!!! £èářñ ₥ôřè ℓôř !!!]"
    }
  });
  ```

7. <span data-ttu-id="3ec4e-298">В файле **./src/webparts/greeting/GreetingWebPart.ts** переопределите метод **onPropertyPaneConfigurationStart** с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-298">In the **./src/webparts/greeting/GreetingWebPart.ts** file override the **onPropertyPaneConfigurationStart** method using the code:</span></span>

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

  <span data-ttu-id="3ec4e-299">Когда пользователь открывает область свойств веб-части, метод загружает сведения о языках, включенных на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-299">When the user opens the web part property pane, the method will load the information about the languages enabled in the current site.</span></span> <span data-ttu-id="3ec4e-300">Так как загрузка этих сведений может занять некоторое время, метод выводит индикатор загрузки.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-300">Because loading this information might take a moment, the method displays a loading indicator communicating its status to the user.</span></span> 
  
  <span data-ttu-id="3ec4e-301">После загрузки сведений о включенных языках метод создает текстовое поле области свойств, связанное с динамическим свойством веб-части **greeting__lcid_**, например **greeting_1033** для английского (США).</span><span class="sxs-lookup"><span data-stu-id="3ec4e-301">Once the information about the enabled languages is loaded, the method creates a new property pane text field linked to a dynamic web part property named **greeting__lcid_**.</span></span>
  
  <span data-ttu-id="3ec4e-302">Когда текстовые поля для всех включенных языков созданы, метод обновляет область свойств, вызывая метод **IPropertyPaneAccessor.refresh**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-302">Once text fields for all enabled languages are constructed, the method refreshes the property pane by calling the **IPropertyPaneAccessor.refresh** method.</span></span> 
  
  <span data-ttu-id="3ec4e-303">После этого метод удаляет индикатор загрузки и обновляет веб-часть.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-303">Finally, the method clears the web part loading indicator and re-renders the web part body.</span></span>

  ![Текстовые поля для всех включенных языков отображаются в области свойств веб-части](../../../images/localization-multilingual-properties.png)

### <a name="show-the-greeting-for-the-preferred-user-language"></a><span data-ttu-id="3ec4e-305">Отображение приветствия на выбранном пользователем языке</span><span class="sxs-lookup"><span data-stu-id="3ec4e-305">Show the greeting for the preferred user language</span></span>

<span data-ttu-id="3ec4e-306">Изначально в веб-части отображалось одно и то же приветствие для всех пользователей, независимо от языка, который они выбрали.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-306">Originally, the web part showed the same greeting for all users no matter what their preferred language was.</span></span> <span data-ttu-id="3ec4e-307">Теперь, когда в веб-части сохранены различные переводы приветствия, оно должно отображаться на языке, выбранном текущим пользователем.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-307">Originally the web part showed the same greeting for all users no matter their preferred language. Now that the web part has different translations of the welcome message stored, it should display the greeting using the language preferred by the current user.</span></span>

1. <span data-ttu-id="3ec4e-308">В файле **./src/webparts/greeting/GreetingWebPart.ts** замените метод **render** веб-части следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-308">In the **./src/webparts/greeting/GreetingWebPart.ts** file, change the web part's **render** method to:</span></span>

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

2. <span data-ttu-id="3ec4e-309">В классе **GreetingWebPart** добавьте новый метод **getGreeting**:</span><span class="sxs-lookup"><span data-stu-id="3ec4e-309">Next, in the **GreetingWebPart** add a new method named **getGreeting**:</span></span>

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

  <span data-ttu-id="3ec4e-310">Этот метод возвращает текущий язык и преобразует его в код языка.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-310">This method gets the currently used language and converts it to a locale ID. Then it returns the value of the greeting property translated to that language.</span></span> <span data-ttu-id="3ec4e-311">Затем он возвращает значение свойства greeting, переведенное на этот язык.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-311">It then returns the value of the greeting property translated to that language.</span></span>

## <a name="localization-in-different-build-types"></a><span data-ttu-id="3ec4e-312">Локализация в различных типах сборки</span><span class="sxs-lookup"><span data-stu-id="3ec4e-312">Localization in different build types</span></span>

<span data-ttu-id="3ec4e-313">В зависимости от выбранного режима сборки SharePoint Framework обрабатывает файлы локализации по-разному.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-313">Depending on the selected build mode, the SharePoint Framework handles localization files differently. Following are some of the differences between the files generated in a debug and a release build.</span></span> <span data-ttu-id="3ec4e-314">Ниже перечислены некоторые отличия между файлами, созданными в отладочной и конечной сборках.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-314">Depending on the selected build mode, the SharePoint Framework handles localization files differently. Following are some of the differences between the files generated in a debug and a release build.</span></span>

### <a name="localization-files-in-the-debug-build"></a><span data-ttu-id="3ec4e-315">Файлы локализации в отладочной сборке</span><span class="sxs-lookup"><span data-stu-id="3ec4e-315">Localization files in the debug build</span></span>

<span data-ttu-id="3ec4e-316">При сборке проектов SharePoint Framework в режиме отладки в манифест веб-части включаются только сведения о языковом стандарте по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-316">When building SharePoint Framework projects in debug mode, only the information about the default locale is included in the generated web part manifest.</span></span> <span data-ttu-id="3ec4e-317">В режиме отладки SharePoint Framework использует заданный по умолчанию языковой стандарт en-US либо языковой стандарт, указанный в настройках проекта или с помощью аргумента командной строки **locale**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-317">In debug mode SharePoint Framework either uses the default en-US locale or the locale that has been specified in the project configuration or using the **locale** argument in command line.</span></span> 

<span data-ttu-id="3ec4e-318">Файлы ресурсов с переведенными строками не включаются в папку **dist**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-318">Resource files with translated strings are not included in the output **dist** folder.</span></span> <span data-ttu-id="3ec4e-319">SharePoint Framework загружает их в среде выполнения из промежуточной папки **lib**, используя путь в манифесте веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-319">Instead they are loaded at runtime from the intermediate **lib** folder using the path in the generated web part manifest.</span></span>

<span data-ttu-id="3ec4e-320">Проверив сведения о модуле **GreetingWebPartStrings** в манифесте веб-части, созданном во время отладочной сборки, вы увидите, что несмотря на разнообразие языковых стандартов, поддерживаемых веб-частью (en-US, nl-NL и qps-ploc), по умолчанию используется путь к файлу ресурсов en-US, хранящемуся в промежуточной папке.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-320">Looking at the information about the **GreetingWebPartStrings** module in the web part manifest generated during a debug build, you can see that despite the different locales supported by the web part (en-US, nl-NL and qps-ploc) the path to the en-US resource file stored in the intermediate location has been assigned as the default path of the localization module.</span></span>

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

### <a name="localization-files-in-the-release-build"></a><span data-ttu-id="3ec4e-321">Файлы локализации в сборке выпуска</span><span class="sxs-lookup"><span data-stu-id="3ec4e-321">Localization files in the release build</span></span>

<span data-ttu-id="3ec4e-322">При сборке проектов SharePoint Framework в режиме выпуска в манифест веб-части включаются сведения обо всех доступных языковых стандартах.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-322">When building SharePoint Framework projects in release mode, the information about all available locales is included in the generated web part manifest.</span></span> <span data-ttu-id="3ec4e-323">Кроме того, ресурсы для каждого языкового стандарта хранятся в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-323">Additionally, resources for each locale are stored in a separate file.</span></span> <span data-ttu-id="3ec4e-324">Эти файлы ресурсов вместе с манифестом и пакетом веб-части копируются в папку **./temp/deploy**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-324">These resource files are copied, along with the web part manifest and the web part bundle to the **./temp/deploy** folder.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3ec4e-325">В конечных сборках файлы ресурсов копируются только в папку **./temp/deploy** и не копируются в папку **./dist**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-325">Important: In release builds resource files are copied only to the **./temp/deploy** folder and not to the **./dist** folder.</span></span> <span data-ttu-id="3ec4e-326">При развертывании веб-части в рабочей среде всегда следует использовать файлы из папки **./temp/deploy**. Тогда точно будут развернуты все файлы, необходимые для веб-части.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-326">When deploying your web part to production you should always use files from the **./temp/deploy** folder to ensure that you are deploying all files required by your web part.</span></span>

<span data-ttu-id="3ec4e-327">Проверив последний манифест веб-части, созданный в сборке выпуска, вы увидите, что теперь модуль **GreetingWebPartStrings** содержит ссылки на все поддерживаемые языковые стандарты.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-327">Examining the latest web part manifest generated in a release build, you can see that now the **GreetingWebPartStrings** module contains references to all supported locales.</span></span>

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

<span data-ttu-id="3ec4e-328">При загрузке веб-части на странице SharePoint Framework автоматически загружает файл ресурсов для соответствующего языкового стандарта, используя сведения с сайта контекста.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-328">When loading the web part on the page, the SharePoint Framework will automatically load the resource file for the corresponding locale by using the information from the context site.</span></span> <span data-ttu-id="3ec4e-329">Если соответствующий файл ресурсов не найден, SharePoint Framework загружает файл, указанный в свойстве **defaultPath**.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-329">If no matching resource file is found, the SharePoint Framework will load the file specified in the **defaultPath** property.</span></span> 

<span data-ttu-id="3ec4e-330">Благодаря разделению файлов ресурсов SharePoint Framework может загружать на странице данные только для того языкового стандарта, который используется на сайте.</span><span class="sxs-lookup"><span data-stu-id="3ec4e-330">By keeping the resource files separate, the SharePoint Framework minimizes the amount of data loaded on the page to the locale that matches the one used in the site.</span></span>

## <a name="see-also"></a><span data-ttu-id="3ec4e-331">См. также</span><span class="sxs-lookup"><span data-stu-id="3ec4e-331">See also</span></span>

- [<span data-ttu-id="3ec4e-332">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="3ec4e-332">SharePoint Framework Overview</span></span>](../../sharepoint-framework-overview.md)