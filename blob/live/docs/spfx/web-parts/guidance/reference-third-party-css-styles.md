---
title: "Ссылки на сторонние стили CSS в веб-частях SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1ab9f28dad1a77af1cb652f29e4f5b23c1c96e4a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="reference-third-party-css-styles-in-sharepoint-framework-web-parts"></a><span data-ttu-id="1378b-102">Ссылки на сторонние стили CSS в веб-частях SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="1378b-102">Reference third-party CSS styles in SharePoint Framework web parts</span></span>

<span data-ttu-id="1378b-p101">Существует множество сторонних библиотек, которые можно использовать для создания полнофункциональных клиентских веб-частей SharePoint Framework. Кроме сценариев, эти библиотеки часто содержат дополнительные ресурсы, такие как таблицы стилей. Эта статья показывает два разных подхода, позволяющих включить сторонние стили CSS в веб-части, а также описывает, как каждый из них влияет на создание пакета веб-частей. Веб-часть, которая приведена в этой статье для примера, использует библиотеки jQuery и jQuery UI для отображения элемента Accordion.</span><span class="sxs-lookup"><span data-stu-id="1378b-p101">There are many third-party libraries that you can leverage to build rich SharePoint Framework client-side web parts. In addition to scripts, these libraries often contain additional assets such as stylesheets. This article shows two different approaches to include third-party CSS styles in web parts and how each approach affects the resulting web part bundle. The example web part discussed in this article uses jQuery and jQuery UI to display an accordion.</span></span>

![Элемент Accordion jQuery UI, отрисованный клиентской веб-частью SharePoint Framework](../../../images/thirdpartycss-accordion-styled.png)

> [!NOTE] 
> <span data-ttu-id="1378b-108">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки для создания клиентских веб-частей SharePoint](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="1378b-108">[Note:](../../set-up-your-development-environment.md) Before following the steps in this article, be sure to set up your SharePoint client-side web part development environment.</span></span>

## <a name="prepare-the-project"></a><span data-ttu-id="1378b-109">Подготовка проекта</span><span class="sxs-lookup"><span data-stu-id="1378b-109">Prepare the project</span></span>

### <a name="create-a-new-project"></a><span data-ttu-id="1378b-110">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="1378b-110">Create a new project</span></span>

<span data-ttu-id="1378b-111">Для начала создайте папку проекта.</span><span class="sxs-lookup"><span data-stu-id="1378b-111">Start by creating a new folder for your project.</span></span>

```sh
md js-thirdpartycss
```

<span data-ttu-id="1378b-112">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="1378b-112">Go to the project folder.</span></span>

```sh
cd js-thirdpartycss
```

<span data-ttu-id="1378b-113">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="1378b-113">In the project folder run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="1378b-114">Когда отобразится соответствующий запрос, введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="1378b-114">When prompted, enter the following values:</span></span>

- <span data-ttu-id="1378b-115">**js-thirdpartycss** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="1378b-115">**js-thirdpartycss** as your solution name</span></span>
- <span data-ttu-id="1378b-116">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="1378b-116">**Use the current folder** for the location to place the files</span></span>
- <span data-ttu-id="1378b-117">**no javaScript web framework** (Без платформы веб-приложений JavaScript) в качестве отправной точки для создания веб-части;</span><span class="sxs-lookup"><span data-stu-id="1378b-117">**no javaScript web framework** as the starting point to build the web part</span></span>
- <span data-ttu-id="1378b-118">**jQuery accordion** (Элемент Accordion jQuery) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="1378b-118">**jQuery accordion** as your web part name</span></span>
- <span data-ttu-id="1378b-119">**Shows jQuery accordion** (Отображает элемент Accordion jQuery) в качестве описания веб-части.</span><span class="sxs-lookup"><span data-stu-id="1378b-119">**Shows jQuery accordion** as your web part description</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/thirdpartycss-yeoman.png)

<span data-ttu-id="1378b-121">После завершения скаффолдинга блокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1378b-121">Once the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

```sh
npm shrinkwrap
```

<span data-ttu-id="1378b-122">Далее откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="1378b-122">Next, open your project folder in your code editor.</span></span> <span data-ttu-id="1378b-123">В инструкциях и на снимках экрана из этой статьи указан Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="1378b-123">This article uses Visual Studio Code in the steps and screenshots but you can use any editor you prefer.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/thirdpartycss-visual-studio-code.png)

### <a name="add-test-content"></a><span data-ttu-id="1378b-125">Добавление содержимого теста</span><span class="sxs-lookup"><span data-stu-id="1378b-125">Add test content</span></span>

<span data-ttu-id="1378b-p103">В редакторе кода откройте файл **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts**. Замените код метода **render** следующим:</span><span class="sxs-lookup"><span data-stu-id="1378b-p103">In the code editor open the **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts** file. Change the **render** method to:</span></span>

```ts
export default class JQueryAccordionWebPart extends BaseClientSideWebPart<IJQueryAccordionWebPartProps> {
  // ...
  public render(): void {
    this.domElement.innerHTML = `
      <div>
        <div class="accordion">
          <h3>Information</h3>
          <div>
            <p>
            The Volcanoes, crags, and caves park is a scenic destination for
            many visitors each year. To ensure everyone has a good
            experience and to preserve the natural beauty, access is
            restricted based on a permit system.
            </p>
            <p>
            Activities include viewing active volcanoes, skiing on mountains,
            walking across lava fields, and caving (spelunking) in caves
            left behind by the lava.
            </p>
          </div>
          <h3>Snow permit</h3>
          <div>
            <p>
            The Northern region has snow in the mountains during winter.
            Purchase a snow permit for access to approved ski areas.
            </p>
          </div>
          <h3>Hiking permit</h3>
          <div>
            <p>
            The entire region has hiking trails for your enjoyment.
            Purchase a hiking permit for access to approved trails.
            </p>
          </div>
          <h3>Volcano access</h3>
          <div>
            <p>
            The volcanic region is beautiful but also dangerous. Each
            area may have restrictions based on wind and volcanic
            conditions. There are three type of permits based on activity.
            </p>
            <ul>
              <li>Volcano drive car pass</li>
              <li>Lava field access permit</li>
              <li>Caving permit</li>
            </ul>
          </div>
        </div>
      </div>`;

      ($('.accordion', this.domElement) as any).accordion();
  }
  // ...
}
```

<span data-ttu-id="1378b-p104">Если вы создадите проект сейчас, то отобразится сообщение об ошибке, уведомляющее о том, что параметр **$** не определен. Причина кроется в том, что проект обращается к библиотеке jQuery, не загрузив ее. Загрузить библиотеку можно двумя способами. Какой бы вы ни выбрали, это не отобразится на использовании скриптов в коде.</span><span class="sxs-lookup"><span data-stu-id="1378b-p104">If you build the project now, you get an error stating that **$** is undefined. This is because the project refers to jQuery without loading it first. There are two approaches to loading the libraries. Neither approach impacts how you use the scripts in code.</span></span>

## <a name="approach-1-include-third-party-libraries-in-the-bundle"></a><span data-ttu-id="1378b-132">Способ 1. Включение в пакет веб-частей сторонних библиотек</span><span class="sxs-lookup"><span data-stu-id="1378b-132">Approach 1: Include third-party libraries in the bundle</span></span>

<span data-ttu-id="1378b-p105">Самый простой способ ссылаться на стороннюю библиотеку в проектах SharePoint Framework — включить ее в созданный пакет веб-частей. Библиотека устанавливается как пакет, ссылки на нее добавляются в проект. Когда проект будет упаковываться, Webpack соберет ссылки на библиотеку и включит их в созданный пакет веб-частей.</span><span class="sxs-lookup"><span data-stu-id="1378b-p105">The easiest way to reference a third-party library in SharePoint Framework projects is to include it in the generated bundle. The library is installed as a package and referenced in the project. When bundling the project, Webpack will pick up the reference to the library and include it in the generated bundle.</span></span>

### <a name="install-libraries"></a><span data-ttu-id="1378b-136">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="1378b-136">Install libraries</span></span>

<span data-ttu-id="1378b-137">Установите библиотеки jQuery и jQuery UI, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="1378b-137">Install jQuery and jQuery UI by running the following command:</span></span>

```sh
npm install jquery jquery-ui --save
```

<span data-ttu-id="1378b-138">Так как вы создаете веб-часть, используя TypeScript, вам понадобятся определения типов TypeScript для библиотеки jQuery. Их можно установить, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="1378b-138">Because you are building your web part in TypeScript you also need TypeScript typings for jQuery that you can install by running the following command:</span></span>

```sh
npm install @types/jquery --save
```

### <a name="reference-libraries-in-the-web-part"></a><span data-ttu-id="1378b-139">Добавление ссылок на библиотеки в веб-частях</span><span class="sxs-lookup"><span data-stu-id="1378b-139">Reference libraries in the web part</span></span>

<span data-ttu-id="1378b-p106">Когда вы установите библиотеки, нужно будет добавить на них ссылки в проект. В редакторе кода откройте файл **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts**. В верхней его части, сразу после последнего оператора **import**, добавьте ссылки на jQuery и jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="1378b-p106">After installing libraries, the next step is to reference them in the project. In the code editor open the **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts** file. In its top section, just below the last **import** statement, add references to jQuery and jQuery UI.</span></span>

```ts
import * as $ from 'jquery';
require('../../../node_modules/jquery-ui/ui/widgets/accordion');
```

<span data-ttu-id="1378b-p107">Так как вы установили определения типов TypeScript для пакета jQuery, вы можете добавить ссылки на него с помощью оператора **import**. Пакет jQuery UI создается иначе. Сколько бы модулей ни структурировалось, не существует основной точки входа со ссылкой на все компоненты, которые вы можете использовать. Необходимо добавлять ссылку на каждый конкретный компонент, который требуется. Точка входа этого компонента содержит все ссылки на зависимости, необходимые для его правильной работы.</span><span class="sxs-lookup"><span data-stu-id="1378b-p107">Because you installed the TypeScript typings for the jQuery package, you can reference it using an **import** statement. However, the jQuery UI package is built differently. Unlike how many modules are structured, there is no main entry point with a reference to all components that you can use. Instead you refer directly to the specific component that you want to use. The entry point of that component contains all references to dependencies that it needs to work correctly.</span></span>

<span data-ttu-id="1378b-148">Подтвердите сборку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1378b-148">Confirm that the project is building by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="1378b-149">Когда вы добавите веб-часть на холст, элемент Accordion должен заработать.</span><span class="sxs-lookup"><span data-stu-id="1378b-149">After adding the web part to the canvas you should see the accordion working.</span></span>

![Элемент Accordion jQuery UI без стилей, отрисованный клиентской веб-частью SharePoint Framework](../../../images/thirdpartycss-accordion-not-styled.png)

<span data-ttu-id="1378b-p108">Вы пока добавили ссылки только на скрипты jQuery UI, поэтому элемент Accordion отображается без стилей. Далее следует добавить недостающие таблицы стилей CSS, чтобы оформить этот элемент должным образом.</span><span class="sxs-lookup"><span data-stu-id="1378b-p108">At this point you have referenced only the jQuery UI scripts which explains why the accordion is not styled. Next you will add the missing CSS stylesheets to brand the accordion.</span></span>

### <a name="reference-third-party-css-stylesheets-in-the-web-part"></a><span data-ttu-id="1378b-153">Добавление ссылок на сторонние таблицы стилей CSS в веб-части</span><span class="sxs-lookup"><span data-stu-id="1378b-153">Reference third-party CSS stylesheets in the web part</span></span>

<span data-ttu-id="1378b-p109">Ссылки на сторонние таблицы стилей CSS, представляющие собой часть установленных в проекте пакетов, можно добавить так же легко, как и ссылки на сами пакеты. SharePoint Framework обеспечивает стандартную поддержку загрузки CSS-файлов с помощью Webpack.</span><span class="sxs-lookup"><span data-stu-id="1378b-p109">Adding references to third-party CSS stylesheets that are a part of packages installed in the project is as simple as adding references to the packages themselves. The SharePoint Framework offers standard support for loading CSS files through Webpack.</span></span>

<span data-ttu-id="1378b-p110">В редакторе кода откройте файл **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts**. Сразу под последним оператором **require** добавьте ссылки на CSS-файлы Accordion jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="1378b-p110">In the code editor open the **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts** file. Just below the last **require** statement, add references to jQuery UI accordion CSS files.</span></span>

```ts
require('../../../node_modules/jquery-ui/themes/base/core.css');
require('../../../node_modules/jquery-ui/themes/base/accordion.css');
require('../../../node_modules/jquery-ui/themes/base/theme.css');
```

<span data-ttu-id="1378b-p111">Добавить ссылки на CSS-файлы, которые представляют собой часть пакета в проекте, можно так же, как и ссылки на файлы JavaScript. Все, что нужно сделать, — указать относительный путь к CSS-файлу, который необходимо загрузить, включая расширение **CSS**. Когда вы будете упаковывать проект, Webpack обработает эти ссылки и включит файлы в созданный пакет веб-частей.</span><span class="sxs-lookup"><span data-stu-id="1378b-p111">Referencing CSS files that are part of a package in the project is similar to adding references to JavaScript files. All you need to do is specify the relative path to the CSS file that you want to load including the **.css** extension. When bundling the project, Webpack will process these references and include the files in the generated web part bundle.</span></span>

<span data-ttu-id="1378b-161">Подтвердите сборку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1378b-161">Confirm that the project is building by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="1378b-162">Элемент Accordion должен будет правильно отображаться, к нему будет применена стандартная тема jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="1378b-162">The accordion should be displayed correctly and branded using the standard jQuery UI theme.</span></span>

![Элемент Accordion jQuery UI, к которому применена стандартная тема jQuery UI и который отрисован клиентской веб-частью SharePoint Framework](../../../images/thirdpartycss-accordion-styled.png)

### <a name="analyze-the-contents-of-the-generated-web-part-bundle"></a><span data-ttu-id="1378b-164">Анализ содержимого пакета веб-частей, который уже создан</span><span class="sxs-lookup"><span data-stu-id="1378b-164">Analyze the contents of the generated web part bundle</span></span>

<span data-ttu-id="1378b-p112">Самый простой способ использовать сторонние библиотеки и их ресурсы — включить их в созданный пакет веб-частей. В этом случае Webpack автоматически урегулирует все зависимости между разными библиотеками и обеспечит загрузку скриптов в правильном порядке. Недостаток такого подхода: ресурсы, на которые добавляются ссылки, загружаются отдельно для каждой веб-части. Если у вас несколько веб-частей в проекте, каждая из которых использует jQuery UI, все они загрузят собственную копию jQuery UI, что замедлит обработку страницы.</span><span class="sxs-lookup"><span data-stu-id="1378b-p112">The easiest way to use third-party libraries and their resources is by including them in the generated web part bundle. In this approach Webpack will automatically resolve all dependencies between the different libraries and will ensure that all scripts are loaded in the correct order. The downside of this approach is that all referenced resources are loaded separately with every web part. So if you have multiple web parts in your project, all using jQuery UI, each web part will load its own copy of jQuery UI and slow down the page.</span></span>

<span data-ttu-id="1378b-p113">Чтобы посмотреть, как добавление библиотек повлияло на размер созданного пакета веб-части, после упаковки проекта откройте файл **./dist/js-thirdpartycss.stats.html** в веб-браузере. Наведите указатель мыши на диаграмму, и вы увидите, например, что размер CSS-файлов пользовательского интерфейса jQuery, на которые ссылается веб-часть, составляет более 6 % от размера всего пакета веб-части.</span><span class="sxs-lookup"><span data-stu-id="1378b-p113">To see the impact of the libraries on the size of the generated web part bundle, after bundling the project open the **./temp/stats/js-thirdpartycss.stats.html** file in the web browser. Move your mouse over the chart and you will see, for example, that the jQuery UI CSS files referenced by the web part make up over 6% of the total web part bundle size.</span></span>

![CSS-файл пользовательского интерфейса jQuery, выделенный в диаграмме, демонстрирующей размер составляющих созданного пакета веб-части](../../../images/thirdpartycss-jquery-ui-css-size.png)

<span data-ttu-id="1378b-p114">Как указано под диаграммой, показаны приблизительные значения, дающие представление о размере отладочной версии пакета веб-частей. Версия пакета веб-частей, предназначенная для выпуска, будет значительно меньше. И все же не помешает знать, каковы составляющие пакета веб-частей и каков размер каждой из них по сравнению с другими элементами этого пакета.</span><span class="sxs-lookup"><span data-stu-id="1378b-p114">As mentioned in the disclaimer below the chart, the sizes are indicative and reflect the size of the debug version of the bundle. The release version of the bundle would be significantly smaller. Still it's good to realize which different pieces compose the web part bundle and what's their relative size compared to other elements in the bundle.</span></span>

## <a name="approach-2-load-third-party-libraries-from-a-url"></a><span data-ttu-id="1378b-175">Способ 2. Загрузка сторонних библиотек по URL-ссылке</span><span class="sxs-lookup"><span data-stu-id="1378b-175">Approach 2: Load third-party libraries from a URL</span></span>

<span data-ttu-id="1378b-p115">Еще один способ ссылаться на сторонние библиотеки в SharePoint Framework — использовать для этого URL-ссылки (например, ссылки на CDN или локально управляемое расположение). Основное преимущество этого подхода заключается в том, что если вы загружаете часто используемую библиотеку из общедоступного расположения, существует вероятность, что пользователь уже скачал ее на свой компьютер. В этом случае SharePoint Framework повторно использует кэшированную библиотеку, что ускорит загрузку вашей веб-части.</span><span class="sxs-lookup"><span data-stu-id="1378b-p115">Another way to reference third-party libraries in the SharePoint Framework is by referencing them from a URL such as a public CDN or a privately managed location. The biggest benefit is that if you're loading a frequently used library from a public location, there is a chance that users might already have that particular library downloaded on their computer. In that case the SharePoint Framework will reuse the cached library loading your web part faster.</span></span>

<span data-ttu-id="1378b-p116">Даже если вы не можете использовать общедоступную сеть CDN для централизованной загрузки библиотек, такой способ хорош для увеличения производительности. Указание URL-ссылки позволяет пользователям применять скрипт на всем портале, скачав его всего лишь раз, что значительно ускоряет загрузку страниц и улучшает впечатления от использования.</span><span class="sxs-lookup"><span data-stu-id="1378b-p116">Even if you cannot use a public CDN to load libraries from a central location it is a good practice from the performance point of view. Pointing to a URL allows your users to download the script only once and reuse it across the whole portal, significantly speeding up loading pages and improving the user experience.</span></span>

<span data-ttu-id="1378b-p117">Выбирая загрузку сторонних библиотек по общедоступным URL-ссылкам, помните, что использование этих библиотек связано с некоторым риском. Так как вы не управляете расположением, в котором размещен определенный скрипт, вы не можете быть уверены в содержимом. Скрипты, загруженные SharePoint Framework, выполняются в контексте текущего пользователя и могут делать все, что разрешено пользователю. Кроме того, если у ресурса, на котором размещены скрипты, не будет доступа к Интернету, веб-часть не будет работать.</span><span class="sxs-lookup"><span data-stu-id="1378b-p117">When loading third-party libraries from public URLs keep in mind that there is a risk involved in using those libraries. Since you don't manage the hosting location of any particular script you can't be sure of its contents. Scripts loaded by the SharePoint Framework run under the context of the current user and are allowed to do whatever that user can do. Also, if the hosting location is offline, your web part won't work.</span></span>

### <a name="install-typings-for-libraries"></a><span data-ttu-id="1378b-185">Установка определений типов для библиотек</span><span class="sxs-lookup"><span data-stu-id="1378b-185">Install typings for libraries</span></span>

<span data-ttu-id="1378b-p118">Когда веб-часть ссылается на сторонние библиотеки с использованием URL-ссылки, вам не нужно их устанавливать как пакеты в проекте. Необходимо установить соответствующие определения типов TypeScript, чтобы при разработке выполнять проверки безопасности типов.</span><span class="sxs-lookup"><span data-stu-id="1378b-p118">When you reference third-party libraries from a URL, you don't need to install them as packages in your project. You do have to install their TypeScript typings if you want the benefit of type safety checks during development.</span></span>

<span data-ttu-id="1378b-188">Если вы начали с пустого проекта, созданного согласно инструкциям, приведенным ранее в этой статье, установите определения типов TypeScript для jQuery, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1378b-188">Assuming you start with an empty project created as described previously in this article, install TypeScript typings for jQuery by running the following command:</span></span>

```sh
npm install @types/jquery --save
```

### <a name="specify-urls-of-libraries"></a><span data-ttu-id="1378b-189">Указание URL-ссылок для библиотек</span><span class="sxs-lookup"><span data-stu-id="1378b-189">Specify URLs of libraries</span></span>

<span data-ttu-id="1378b-p119">Чтобы загрузить сторонние библиотеки по URL-ссылкам, необходимо указать URL-ссылки в конфигурации вашего проекта. В редакторе кода откройте файл **./config/config.json**. В разделе **externals** добавьте следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="1378b-p119">To load third-party libraries from a URL, you have to specify the URL where they are located in the configuration of your project. In the code editor open the **./config/config.json** file. In the **externals** section add the following JSON:</span></span>

```json
{
  //...
  "externals": {
    //...
    "jquery": "https://code.jquery.com/jquery-3.1.1.min.js",
    "jquery-ui": "https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"
    //...
  }
  //...
}
```

### <a name="reference-libraries-from-the-url-in-the-web-part"></a><span data-ttu-id="1378b-193">Обращение веб-частей к библиотекам с помощью URL-ссылок</span><span class="sxs-lookup"><span data-stu-id="1378b-193">Reference libraries from the URL in the web part</span></span>

<span data-ttu-id="1378b-p120">Определив URL-ссылку, которую SharePoint Framework следует использовать для загрузки jQuery и jQuery UI, следует добавить в проект ссылки на эти библиотеки. В редакторе кода откройте файл **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts**. В верхней его части, сразу после последнего оператора **import**, добавьте указанные ниже ссылки на jQuery и jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="1378b-p120">Having specified the URL that the SharePoint Framework should use to load jQuery and jQuery UI, the next step is to reference them in the project. In the code editor open the **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts** file. In its top section, just below the last **import** statement, add the following references to jQuery and jQuery UI:</span></span>

```ts
import * as $ from 'jquery';
require('jquery-ui');
```

<span data-ttu-id="1378b-p121">Обращение к обеим библиотекам с помощью URL-ссылок похоже на добавление ссылок на эти библиотеки при их установке как пакетов в проекте. Так как у библиотеки jQuery есть установленные определения типов TypeScript, на нее можно ссылаться с помощью оператора **import**. В случае jQuery UI нужно только загрузить скрипт на страницу.</span><span class="sxs-lookup"><span data-stu-id="1378b-p121">Compared to how you were referencing both libraries when they were installed as packages in your project, referencing them from the URL is very similar. Because jQuery has its TypeScript typings installed it can be referenced using an **import** statement. For jQuery UI all you want is to load the script on the page.</span></span>

<span data-ttu-id="1378b-p122">Так как вы зарегистрировали **jquery** и **jquery-ui** в конфигурации проекта как внешние ресурсы, когда вы будете добавлять ссылку на любую из этих библиотек, SharePoint Framework с помощью указанных URL-ссылок загрузит их в среде выполнения. Когда вы будете упаковывать проект, эти ресурсы будут отмечены как внешние и, как следствие, исключены из пакета веб-частей.</span><span class="sxs-lookup"><span data-stu-id="1378b-p122">Because you registered **jquery** and **jquery-ui** in the project configuration as external resources, when you reference any of these libraries, the SharePoint Framework will use the specified URLs to load them at runtime. When bundling the project, these resources will be marked as externals and will therefore be excluded from the bundle.</span></span>

<span data-ttu-id="1378b-202">Единственное отличие заключается в том, что ранее вы указывали загрузку элемента Accordion из пакета jQuery UI, а сейчас ссылаетесь на jQuery UI из сети CDN, содержащей все компоненты jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="1378b-202">One difference to keep in mind is that previously you specified to load the accordion from the jQuery UI package, but now you're referring to jQuery UI from the CDN which contains all jQuery UI components.</span></span>

<span data-ttu-id="1378b-203">Подтвердите сборку проекта, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="1378b-203">Confirm that the project is building by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="1378b-204">Когда вы добавите веб-часть на холст, элемент Accordion должен заработать.</span><span class="sxs-lookup"><span data-stu-id="1378b-204">After adding the web part to the canvas you should see the accordion working.</span></span>

![Элемент Accordion jQuery UI без стилей, отрисованный клиентской веб-частью SharePoint Framework](../../../images/thirdpartycss-accordion-not-styled.png)

<span data-ttu-id="1378b-p123">В веб-браузере откройте средства разработчика, перейдите на вкладку с запросами сети и повторно загрузите страницу. Библиотеки jQuery и jQuery UI должны загрузиться из CDN.</span><span class="sxs-lookup"><span data-stu-id="1378b-p123">In your web browser, open the developer tools, switch to the tab showing the network requests, and reload the page. You should see how both jQuery and jQuery UI are loaded from the CDN.</span></span>

![Запросы для библиотек jQuery и jQuery UI, выделенные в окне средств разработчика, открытом в Microsoft Edge](../../../images/thirdpartycss-libraries-cdn.png)

<span data-ttu-id="1378b-p124">Вы пока добавили ссылки только на скрипты jQuery UI, поэтому элемент Accordion отображается без стилей. Далее следует добавить недостающие таблицы стилей CSS, чтобы оформить этот элемент должным образом.</span><span class="sxs-lookup"><span data-stu-id="1378b-p124">At this point you have referenced only the jQuery UI scripts which explains why the accordion is not styled. Next you will add the missing CSS stylesheets to brand the accordion.</span></span>

### <a name="reference-third-party-css-stylesheets-from-url-in-the-web-part"></a><span data-ttu-id="1378b-211">Добавление в веб-часть ссылок на сторонние таблицы стилей CSS с помощью URL-ссылок</span><span class="sxs-lookup"><span data-stu-id="1378b-211">Reference third-party CSS stylesheets from URL in the web part</span></span>

<span data-ttu-id="1378b-p125">Добавление ссылок на сторонние таблицы стилей CSS с помощью URL-ссылок отличается от добавления ссылок на ресурсы из пакетов проектов. Конфигурация проекта в файле **config.json** позволяет указывать внешние ресурсы только для сценариев. Чтобы добавить ссылки на таблицы стилей CSS с помощью URL-ссылки, нужно использовать **SPComponentLoader**.</span><span class="sxs-lookup"><span data-stu-id="1378b-p125">Adding references to third-party CSS stylesheets from a URL is different than referencing resources from project packages. While the project configuration in the **config.json** file allows you to specify external resources, it applies only to scripts. To reference CSS stylesheets from a URL you have to use the **SPComponentLoader** instead.</span></span>

#### <a name="load-css-from-the-url-using-the-spcomponentloader"></a><span data-ttu-id="1378b-215">Загрузка CSS-файла с помощью URL-ссылки и SPComponentLoader</span><span class="sxs-lookup"><span data-stu-id="1378b-215">Load CSS from the URL using the SPComponentLoader</span></span>

<span data-ttu-id="1378b-p126">В редакторе кода откройте файл **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts**. В верхней части файла, сразу после оператора **import**, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="1378b-p126">In the code editor open the **./src/webparts/jQueryAccordion/JQueryAccordionWebPart.ts** file. In the top section of the file, just after the last **import** statement, add the following code:</span></span>

```ts
import { SPComponentLoader } from '@microsoft/sp-loader';
```

<span data-ttu-id="1378b-218">В том же файле переопределите метод onInit () так, как представлено ниже.</span><span class="sxs-lookup"><span data-stu-id="1378b-218">In the same file override the onInit() method as follows:</span></span>

```ts
export default class JQueryAccordionWebPart extends BaseClientSideWebPart<IJQueryAccordionWebPartProps> {
  protected onInit(): Promise<void> {
    SPComponentLoader.loadCss('https://code.jquery.com/ui/1.12.1/themes/base/jquery-ui.min.css');
    return super.onInit();
  }

  // ...
}
```

<span data-ttu-id="1378b-p127">Когда на странице создан экземпляр веб-части, она загрузит CSS-файл jQuery с помощью указанной URL-ссылки. Эта таблица стилей CSS — объединенная и оптимизированная версия CSS jQuery UI, содержащая базовые стили, тему и оформление для всех компонентов.</span><span class="sxs-lookup"><span data-stu-id="1378b-p127">When the web part is instantiated on the page, it will load the jQuery UI CSS from the specified URL. This CSS stylesheet is the combined and optimized version of the jQuery UI CSS that contains the basic styles, theme, and styling for all components.</span></span>

<span data-ttu-id="1378b-221">Подтвердите сборку проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1378b-221">Confirm that the project is building by running the following command:</span></span>

```sh
gulp serve
```

<span data-ttu-id="1378b-222">Элемент Accordion должен будет правильно отображаться, к нему будет применена стандартная тема jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="1378b-222">The accordion should be displayed correctly and branded using the standard jQuery UI Theme.</span></span>

![Элемент Accordion jQuery UI, к которому применена стандартная тема jQuery UI и который отрисован клиентской веб-частью SharePoint Framework](../../../images/thirdpartycss-accordion-styled.png)

### <a name="analyze-the-contents-of-the-generated-web-part-bundle-loading-resources-from-url"></a><span data-ttu-id="1378b-224">Анализ содержимого созданного пакета веб-части, который загружает ресурсы с URL-адреса</span><span class="sxs-lookup"><span data-stu-id="1378b-224">Analyze the contents of the generated web part bundle loading resources from URL</span></span>

<span data-ttu-id="1378b-p128">Создав проект в веб-браузере, откройте файл **./temp/stats/js-thirdpartycss.stats.html**. Обратите внимание, что общий размер пакета веб-части значительно уменьшился (сейчас он составляет 7 КБ, а когда в него включались библиотека jQuery и ее пользовательский интерфейс, он превышал 300 КБ), а также что библиотека jQuery и ее пользовательский интерфейс не указаны в диаграмме, так как они были загружены в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="1378b-p128">After building the project in the web browser open the **./temp/stats/js-thirdpartycss.stats.html** file. Notice how the overall bundle is significantly smaller (7KB compared to over 300KB when including jQuery and jQuery UI in the bundle) and how jQuery and jQuery UI are not listed in the chart since they are loaded at runtime.</span></span>
