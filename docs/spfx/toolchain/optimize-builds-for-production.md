---
title: "Оптимизация сборок SharePoint Framework для рабочей среды"
description: "Узнайте, чем отличаются отладочные и конечные сборки, а также как оптимизировать пакет для использования в рабочих средах."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 95bd3bc98c5a0bf509ffd3bf790d22a9d5e9ac93
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="optimize-sharepoint-framework-builds-for-production"></a><span data-ttu-id="c2b4f-103">Оптимизация сборок SharePoint Framework для рабочей среды</span><span class="sxs-lookup"><span data-stu-id="c2b4f-103">Optimize SharePoint Framework builds for production</span></span>

<span data-ttu-id="c2b4f-104">При развертывании решений SharePoint Framework в рабочей среде следует всегда использовать оптимизированную конечную сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-104">When deploying SharePoint Framework solutions to production you should always use a release build of your project which is optimized for performance. This article illustrates the main differences between debug and release builds and shows how you can optimize your bundle for use in production environments.</span></span> <span data-ttu-id="c2b4f-105">В этой статье иллюстрируются основные отличия между отладочными и конечными сборками, а также показано, как оптимизировать пакет для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-105">When deploying SharePoint Framework solutions to production you should always use a release build of your project which is optimized for performance. This article illustrates the main differences between debug and release builds and shows how you can optimize your bundle for use in production environments.</span></span>

## <a name="use-release-builds-in-production"></a><span data-ttu-id="c2b4f-106">Используйте конечные сборки в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="c2b4f-106">Use release builds in production</span></span>

<span data-ttu-id="c2b4f-p102">При сборке проекта SharePoint Framework вы можете выбрать режим отладки или выпуска. По умолчанию проекты SharePoint Framework собираются в режиме отладки, что упрощает отладку кода. Но когда код готов и работает надлежащим образом, необходимо собрать его для выпуска, чтобы оптимизировать приложение для выполнения в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-p102">When building a SharePoint Framework project, you can choose whether you want to build it in a debug or release mode. By default, SharePoint Framework projects are built in debug mode, which makes it easier for you to debug code. But when your code is finished and is working as expected, you should build it in release mode to optimize it for running in the production environment.</span></span>

<span data-ttu-id="c2b4f-110">Дополнительные сведения о сборке проекта в режиме выпуска см. в статье [Цепочка инструментов SharePoint Framework](./sharepoint-framework-toolchain.md).</span><span class="sxs-lookup"><span data-stu-id="c2b4f-110">For more information about building your project in release mode, see the [SharePoint Framework Toolchain](./sharepoint-framework-toolchain.md) article.</span></span>

<span data-ttu-id="c2b4f-111">Основное отличие между результатами сборки в режимах отладки и выпуска состоит в том, что размер пакета для выпуска значительно меньше, чем у аналогичного пакета для отладки.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-111">The main difference between the output of a debug and release build is, that the release version of the generated bundle is minified and significantly smaller in size than its debug equivalent. To illustrate the difference, compare the size of the debug and release version of a SharePoint Framework project with a web part using Angular.</span></span> <span data-ttu-id="c2b4f-112">Чтобы увидеть разницу, сравните размеры проектов SharePoint Framework, собранных для отладки и выпуска, в веб-части на платформе Angular.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-112">The main difference between the output of a debug and release build is, that the release version of the generated bundle is minified and significantly smaller in size than its debug equivalent. To illustrate the difference, compare the size of the debug and release version of a SharePoint Framework project with a web part using Angular.</span></span>

![Изображение с двумя окнами проводника, в которых выделены версии пакета для отладки и выпуска](../../images/guidance-productionbuilds-debug-vs-ship-bundle.png)

<span data-ttu-id="c2b4f-114">Версия пакета для отладки занимает 1255 КБ, а аналогичный пакет для выпуска — всего 177 КБ.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-114">The debug version of the bundle is 1255 KB while its release equivalent is only 177 KB.</span></span> <span data-ttu-id="c2b4f-115">Разница в размере между пакетами для отладки и выпуска зависит от того, какие библиотеки используются в проекте.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-115">The difference in size between the debug and release version of the generated bundle differs depending on the libraries used in your project.</span></span> <span data-ttu-id="c2b4f-116">Однако конечная сборка всегда будет значительно меньше отладочной, поэтому в рабочей среде всегда следует развертывать конечные сборки.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-116">Still, the release build is always significantly smaller than a debug build, which is why you should always deploy the output of release builds to production.</span></span>

## <a name="dont-include-third-party-libraries-in-the-bundle"></a><span data-ttu-id="c2b4f-117">Не включайте в пакет сторонние библиотеки</span><span class="sxs-lookup"><span data-stu-id="c2b4f-117">Don't include third party libraries in the bundle</span></span>

<span data-ttu-id="c2b4f-118">При сборке решений SharePoint Framework можно использовать множество готовых библиотек JavaScript для решения основных задач.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-118">When building SharePoint Framework solutions, you can benefit from many existing JavaScript libraries to solve common problems.</span></span> <span data-ttu-id="c2b4f-119">Использование готовых библиотек позволяет успевать больше и сосредоточиться на конкретных задачах организации, а не на разработке стандартных функций.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-119">When building SharePoint Framework solutions, you can benefit of many existing JavaScript libraries to solve common problems. Using existing libraries allows you to be more productive and lets you focus on the added value for your organization, instead of on developing generic functionality, required by your solution.</span></span>

<span data-ttu-id="c2b4f-120">По умолчанию, если в проекте есть ссылки на сторонние библиотеки, SharePoint Framework включает их в создаваемый пакет.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-120">By default, when referencing third-party libraries in your project, SharePoint Framework includes them in the generated bundle.</span></span> <span data-ttu-id="c2b4f-121">В результате пользователям решения приходится скачивать одну и ту же библиотеку несколько раз (с каждым компонентом).</span><span class="sxs-lookup"><span data-stu-id="c2b4f-121">As a result, users working with your solution end up downloading the same library multiple times, once with each component.</span></span> <span data-ttu-id="c2b4f-122">Общий размер страницы значительно возрастает, а вместе с ним и время загрузки. Это портит впечатление от решения, особенно в медленных сетях.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-122">The total page size grows significantly, taking longer to load and leading to a poor user experience, particularly on slower networks.</span></span>

![Средства разработчика в Microsoft Edge, где на вкладке "Сеть" показаны два загружаемых пакета веб-частей](../../images/guidance-productionbuilds-two-bundles-with-libraries.png)

<span data-ttu-id="c2b4f-124">Советуем загружать сторонние библиотеки со среды внешнего размещения: общедоступной сети CDN или среды, принадлежащей вашей организации.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-124">When working with third-party libraries, you should always consider loading them from an external location: either a public CDN or a hosting location owned by your organization.</span></span> <span data-ttu-id="c2b4f-125">Это позволяет исключить библиотеку из пакета, значительно сокращая его размер.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-125">This allows you to exclude the library from your bundle, significantly decreasing its size.</span></span> 

<span data-ttu-id="c2b4f-126">Кроме того, если среда, из которой загружается библиотека, оптимизирована для доставки статических ресурсов, пользователям решения достаточно будет скачать библиотеку всего один раз.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-126">Additionally, if the hosting location from which you are loading the library is optimized for serving static assets, users working with your solution need to load the library only once.</span></span> <span data-ttu-id="c2b4f-127">При последующих запросах и даже при использовании решения спустя время веб-браузер будет использовать копию библиотеки из кэша, а не скачивать ее заново.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-127">On subsequent requests, or even when using your solution in the future, the web browser reuses the previously cached copy of the library rather than downloading it again.</span></span> <span data-ttu-id="c2b4f-128">В результате страница с решением будет загружаться значительно быстрее.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-128">As a result, the page with your solution loads significantly faster.</span></span>

## <a name="verify-the-contents-of-your-bundle"></a><span data-ttu-id="c2b4f-129">Проверка содержимого пакета</span><span class="sxs-lookup"><span data-stu-id="c2b4f-129">Verify the contents of your bundle</span></span>

<span data-ttu-id="c2b4f-130">Чтобы получить представление о размере создаваемых пакетов, разверните конфигурацию Webpack в проекте или просмотрите статистику в SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-130">To better understand the size of the generated bundles, you can extend the webpack configuration in your project and have the SharePoint Framework generate bundle statistics.</span></span>

<span data-ttu-id="c2b4f-131">Сначала установите пакет **webpack-bundle-analyzer** в проекте, выполнив в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2b4f-131">First, install the **webpack-bundle-analyzer** package in your project, by executing in the command line:</span></span>

```sh
npm install webpack-bundle-analyzer --save-dev
```

<br/>

<span data-ttu-id="c2b4f-132">Затем замените содержимое файла **gulpfile.js** в проекте следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c2b4f-132">Next, change the contents of the **gulpfile.js** file in your project to:</span></span>

```js
'use strict';

const gulp = require('gulp');
const path = require('path');
const build = require('@microsoft/sp-build-web');
const bundleAnalyzer = require('webpack-bundle-analyzer');

build.configureWebpack.mergeConfig({
  additionalConfiguration: (generatedConfiguration) => {
    const lastDirName = path.basename(__dirname);
    const dropPath = path.join(__dirname, 'temp', 'stats');
    generatedConfiguration.plugins.push(new bundleAnalyzer.BundleAnalyzerPlugin({
      openAnalyzer: false,
      analyzerMode: 'static',
      reportFilename: path.join(dropPath, `${lastDirName}.stats.html`),
      generateStatsFile: true,
      statsFilename: path.join(dropPath, `${lastDirName}.stats.json`),
      logLevel: 'error'
    }));

    return generatedConfiguration;
  }
});

build.initialize(gulp);
```

<br/>

<span data-ttu-id="c2b4f-133">При следующем использовании команды `gulp bundle` в папке **temp/stats** проекта будут сгенерированы файлы статистики.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-133">Next time you bundle your project using the `gulp bundle` task, you will see the bundle stats files generated in the **temp/stats** folder in your project.</span></span> <span data-ttu-id="c2b4f-134">Один из этих файлов представляет собой диаграмму "дерево", на которой показаны различные скрипты, включенные в сгенерированный пакет.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-134">One of the generated stats file, is a treemap showing the different scripts included in the generated bundle.</span></span> <span data-ttu-id="c2b4f-135">Вы можете найти эту визуализацию в файле **./temp/stats/[solution-name].stats.html**.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-135">You can find this visualization in the **./temp/stats/[solution-name].stats.html** file.</span></span>

<br/>

<img alt="Webpack bundle analyzer treemap illustrating the contents of a sample SharePoint Framework bundle" src="../../images/guidance-productionbuilds-webpack-bundlestats-chart-angular.png" width="800">

<span data-ttu-id="c2b4f-136">Диаграмма "дерево" анализатора пакетов Webpack помогает убедиться, что созданный пакет не содержит лишних скриптов, и проверить, как включенные скрипты влияют на общий размер пакета.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-136">Using the Webpack bundle analyzer treemap is a convenient way for you to verify, that the generated bundle doesn't contain any unnecessary scripts and how the included scripts affect the total bundle size.</span></span> <span data-ttu-id="c2b4f-137">Помните, что отображаемый размер относится к отладочной сборке, а конечная сборка будет значительно меньше.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-137">Keep in mind, that the displayed size reflects the debug build and would be significantly smaller for a release build.</span></span>

<span data-ttu-id="c2b4f-138">Более подробные сведения, используемые для создания визуализации, включены в файл **./dist/[solution-name].stats.json**.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-138">More detailed information, used to generate the visualization, is included in the **./dist/[solution-name].stats.json** file.</span></span> <span data-ttu-id="c2b4f-139">С помощью этого файла вы можете узнать, почему тот или иной скрипт был включен в пакет и используется ли он в нескольких пакетах.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-139">Using this file you can find out why a specific script has been included in the bundle or if a particular script is used in multiple bundles.</span></span> <span data-ttu-id="c2b4f-140">Эти сведения помогут вам оптимизировать пакеты и ускорить загрузку решения.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-140">With this information you can optimize your bundles improving the loading time of your solution.</span></span>

## <a name="choose-your-primary-client-side-library"></a><span data-ttu-id="c2b4f-141">Выбор основной клиентской библиотеки</span><span class="sxs-lookup"><span data-stu-id="c2b4f-141">Choose your primary client-side library</span></span>

<span data-ttu-id="c2b4f-142">Если несколько компонентов на одной или нескольких страницах портала используют одну и ту же библиотеку, загружаемую с одного URL-адреса, веб-браузер использует ранее кэшированную копию, что ускоряет загрузку портала.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-142">If there are multiple components on the same page, or even on different pages across the portal, and they all use the same library loaded from the same URL, the web browser also reuses the copy it cached previously, which leads to the portal loading faster.</span></span> 

<span data-ttu-id="c2b4f-143">Именно по этой причине важно оптимизировать использование библиотек и версий, а также источников, из которых они загружаются. Это относится не только к конкретному проекту, но и ко всей организации.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-143">This is exactly why it is essential for organizations to rationalize which libraries and versions they use and where they load from, not only for a specific project but for the whole organization.</span></span> <span data-ttu-id="c2b4f-144">Эти меры скажутся на производительности пользователей, работающих с разными приложениями, так как скорость загрузки увеличится.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-144">Such a policy allows users working with the different applications to be more productive by loading the applications faster.</span></span> <span data-ttu-id="c2b4f-145">Использование уже загруженных ресурсов также позволяет ограничить нагрузку на сеть, освобождая пропускную способность для других целей.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-145">By reusing the previously downloaded assets, the load on the network is limited, freeing its bandwidth for other purposes.</span></span>

<span data-ttu-id="c2b4f-146">Дополнительные сведения о работе с внешними библиотеками см. в статье [Использование существующих библиотек JavaScript в клиентских веб-частях SharePoint Frameworks](../web-parts/guidance/use-existing-javascript-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="c2b4f-146">For more information about working with external libraries see the [Use existing JavaScript libraries in SharePoint Framework client-side web parts](../web-parts/guidance/use-existing-javascript-libraries.md) article.</span></span>

## <a name="reference-only-the-necessary-components"></a><span data-ttu-id="c2b4f-147">Ссылайтесь только на необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="c2b4f-147">Reference only the necessary components</span></span>

<span data-ttu-id="c2b4f-148">Иногда при работе с внешней библиотекой может быть необходима лишь небольшая ее часть.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-148">Sometimes when working with external libraries, you might actually not need the whole library but only a small portion of it.</span></span> <span data-ttu-id="c2b4f-149">Включив всю библиотеку, вы увеличите размер пакета, замедлив его загрузку.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-149">Including the whole library unnecessarily adds to the size of your bundle, increasing its load time.</span></span> <span data-ttu-id="c2b4f-150">Советуем загружать только необходимые части той или иной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-150">Instead, you should always consider loading only the specific parts of the particular library that you actually need.</span></span>

<span data-ttu-id="c2b4f-151">В качестве примера возьмем библиотеку [Lodash](https://lodash.com).</span><span class="sxs-lookup"><span data-stu-id="c2b4f-151">To illustrate this, take the [Lodash](https://lodash.com) library as an example.</span></span> <span data-ttu-id="c2b4f-152">Lodash — это коллекция служебных программ, помогающих выполнять определенные операции в коде.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-152">Lodash is a collection of utilities helping you to perform certain operations in your code.</span></span> <span data-ttu-id="c2b4f-153">Высока вероятность того, что при работе с Lodash вам потребуется лишь несколько отдельных методов, а не вся библиотека.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-153">The odds are high, that when working with Lodash, you will only need a few specific methods rather than the complete library.</span></span> 

<span data-ttu-id="c2b4f-154">Если ссылаться на всю библиотеку с помощью приведенного ниже кода, к неоптимизированному пакету добавится 527 КБ.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-154">However, if you referenced the whole library by using the following code, it adds 527 KB to your unoptimized bundle:</span></span>

```typescript
import * as _ from 'lodash';
```

<br/>

<img alt="The complete Lodash library included in a bundle, highlighted in the Webpack bundle analyzer treemap" src="../../images/guidance-productionbuilds-import-lodash.png" width="800">

<br/>

<span data-ttu-id="c2b4f-155">Если же ссылаться только на определенный метод Lodash с помощью приведенного ниже кода, то к неоптимизированному пакету добавится только 45 КБ.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-155">Instead, if you referenced only the specific Lodash method by using the following code, it adds 45 KB to your unoptimized bundle:</span></span>

```typescript
const at: any = require('lodash/at');
```

<br/>

![Включенный в пакет метод Lodash, выделенный на диаграмме "дерево" анализатора пакетов Webpack](../../images/guidance-productionbuilds-import-lodash-at.png)

<span data-ttu-id="c2b4f-157">В случае библиотеки Lodash, как и с некоторыми другими библиотеками, у ссылок на отдельные методы есть свои недостатки.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-157">Specifically with regards to Lodash, but which could also be the case with other libraries, referencing specific methods instead of the whole library comes with a price.</span></span> 

<span data-ttu-id="c2b4f-158">В настоящее время библиотека Lodash не поддерживает загрузку конкретных методов в проектах SharePoint Framework с помощью нотации **import**.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-158">Currently, Lodash doesn't support loading specific methods inside of SharePoint Framework projects using the **import** notation.</span></span> <span data-ttu-id="c2b4f-159">Вместо этого необходимо использовать оператор **require**, не обеспечивающий такую же безопасность типов, как оператор **import**.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-159">Instead, you have to use a **require** statement which doesn't offer you the typesafety capabilities that using the **import** statement does.</span></span> <span data-ttu-id="c2b4f-160">Стоит ли загружать значительно больше кода для обеспечения дополнительной безопасности типов? Решать вам.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-160">Eventually it is up to you to decide if loading significantly more code into your bundles is worth preserving the typesafety capabilities.</span></span>

> [!NOTE] 
> <span data-ttu-id="c2b4f-161">Некоторые из методов Lodash включены в библиотеку **@microsoft/sp-lodash-subset**, входящую в состав SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-161">Some of the Lodash methods are provided with the SharePoint Framework in the **@microsoft/sp-lodash-subset** library.</span></span> <span data-ttu-id="c2b4f-162">Прежде чем использовать Lodash, проверьте, нет ли нужного вам метода в библиотеке **@microsoft/sp-lodash-subset**. Она уже входит в состав SharePoint Framework, поэтому ее не требуется включать в пакет решения.</span><span class="sxs-lookup"><span data-stu-id="c2b4f-162">Before using Lodash, verify if the method that you want to use isn't already available in the **@microsoft/sp-lodash-subset** library, which is already available as a part of the SharePoint Framework and does not need to be included in your bundle.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2b4f-163">См. также</span><span class="sxs-lookup"><span data-stu-id="c2b4f-163">See also</span></span>

- [<span data-ttu-id="c2b4f-164">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="c2b4f-164">SharePoint Framework Overview</span></span>](../sharepoint-framework-overview.md)