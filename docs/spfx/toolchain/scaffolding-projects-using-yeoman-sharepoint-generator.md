---
title: "Формирование шаблонов проектов с помощью генератора Yeoman для SharePoint"
description: "Генератор Yeoman для SharePoint позволяет формировать шаблоны новых проектов клиентских решений, чтобы создавать, упаковывать и развертывать решения SharePoint."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: ac69ce5030289fefce1563fb03b6b0fb1466d470
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="scaffold-projects-by-using-yeoman-sharepoint-generator"></a><span data-ttu-id="54205-103">Формирование шаблонов проектов с помощью генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="54205-103">Scaffold projects using yeoman SharePoint generator</span></span>

<span data-ttu-id="54205-104">[Yeoman](http://yeoman.io/) помогает эффективно запускать новые проекты благодаря соответствующим рекомендациям и инструментам.</span><span class="sxs-lookup"><span data-stu-id="54205-104">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="54205-105">С помощью генератора Yeoman для SharePoint разработчики могут формировать шаблоны новых проектов клиентских решений, чтобы создавать, упаковывать и развертывать решения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="54205-105">Using the Yeoman SharePoint generator, developers are able to scaffold new client-side solution projects to build, package, and deploy SharePoint solutions.</span></span> <span data-ttu-id="54205-106">Генератор предоставляет стандартные инструменты сборки, а также стандартные код и веб-сайт для тестирования веб-частей.</span><span class="sxs-lookup"><span data-stu-id="54205-106">The generator provides common build tools, common boilerplate code, and a common playground website to host web parts for testing.</span></span>

## <a name="install-the-yeoman-sharepoint-generator"></a><span data-ttu-id="54205-107">Установка генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="54205-107">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="54205-108">Генератор Yeoman для SharePoint доступен в составе платформы как [пакет npm](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="54205-108">Yeoman SharePoint generator is available as part of the framework as a [npm package](https://www.npmjs.com/package/@microsoft/generator-sharepoint). You can install the generator by executing the following command in a console:</span></span> <span data-ttu-id="54205-109">Чтобы установить генератор, выполните следующую команду в консоли:</span><span class="sxs-lookup"><span data-stu-id="54205-109">Yeoman SharePoint generator is available as part of the framework as a npm package. You can install the generator by executing the following command in a console:</span></span>

```
npm install @microsoft/generator-sharepoint -g
```

> [!NOTE] 
> <span data-ttu-id="54205-110">Генератор Yeoman для SharePoint должен развертываться глобально с первой общедоступной версией.</span><span class="sxs-lookup"><span data-stu-id="54205-110">The Yeoman SharePoint generator is targeted to get deployed globally with the initial General Availability (GA) version.</span></span> <span data-ttu-id="54205-111">При его локальной установке в проекте могут возникать определенные проблемы, которые будут устранены в одной из следующих версий.</span><span class="sxs-lookup"><span data-stu-id="54205-111">Note: Yeoman generator for SharePoint is targeted to get deployed globally with the initial General Availability (GA) version. There are some known issues if it's installed locally to the project, which are planned to be addressed post GA.</span></span>

<span data-ttu-id="54205-112">Рекомендуем воспользоваться [этими инструкциями по настройке](../set-up-your-development-environment.md), чтобы установить на компьютер полный набор инструментов разработчика, в том числе генератор Yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="54205-112">It is recommended you follow the [set up your development environment](../set-up-your-development-environment.md) to configure your machine with the complete set of developer tools, including yeoman SharePoint generator.</span></span> 

## <a name="use-the-yeoman-sharepoint-generator"></a><span data-ttu-id="54205-113">Использование генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="54205-113">Use the Yeoman SharePoint generator</span></span>

<span data-ttu-id="54205-114">Чтобы вызвать генератор после установки, просто введите в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="54205-114">Once the generator is installed, you can invoke the generator by just typing the following command in a console:</span></span>

```
yo
```

<span data-ttu-id="54205-115">Появится список всех генераторов, доступных на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="54205-115">The command lists all the generators available on your machine.</span></span> <span data-ttu-id="54205-116">Выберите `@microsoft/sharepoint`, чтобы вызвать генератор SharePoint, и следуйте инструкциям, чтобы создать клиентское решение:</span><span class="sxs-lookup"><span data-stu-id="54205-116">The command will list all of the generators available in your machine. Select the `@microsoft/sharepoint` to invoke the SharePoint generator and continue with the prompts to successfully create your client-side solution:</span></span>

![Генератор Yeoman для SharePoint](../../images/yeoman-sp-generator.png)


## <a name="use-available-command-line-options-for-the-generator"></a><span data-ttu-id="54205-118">Использование доступных параметров командной строки для генератора</span><span class="sxs-lookup"><span data-stu-id="54205-118">Use available command-line options for the generator</span></span>

<span data-ttu-id="54205-119">Параметры командной строки, доступные генератору Yeoman для SharePoint, позволяют не следовать отображаемым на экране инструкциям, а формировать шаблоны проектов с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="54205-119">You can use the command line options available with the yeoman SharePoint generator to scaffold projects in one command instead of going through the prompts.</span></span> <span data-ttu-id="54205-120">Выполните следующую команду, чтобы просмотреть список параметров командной строки, доступных генератору Yeoman для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="54205-120">Execute the following command to see the list of command line options available for the SharePoint generator:</span></span>

```
yo @microsoft/generator-sharepoint --help
```

<br/>

![Параметры командной строки, доступные генератору Yeoman для SharePoint](../../images/yeoman-sp-cmdline-options.png)

<br/>

<span data-ttu-id="54205-122">**Параметры командной строки**</span><span class="sxs-lookup"><span data-stu-id="54205-122">**Command-line options**</span></span>

<span data-ttu-id="54205-123">Параметр</span><span class="sxs-lookup"><span data-stu-id="54205-123">Option</span></span> | <span data-ttu-id="54205-124">Описание</span><span class="sxs-lookup"><span data-stu-id="54205-124">Description</span></span> 
-----|------
<span data-ttu-id="54205-125">--help</span><span class="sxs-lookup"><span data-stu-id="54205-125">--help</span></span>|<span data-ttu-id="54205-126">Печать сведений об использовании генератора и его параметров.</span><span class="sxs-lookup"><span data-stu-id="54205-126">Print the generator's options and usage.</span></span>
<span data-ttu-id="54205-127">--skip-cache</span><span class="sxs-lookup"><span data-stu-id="54205-127">--skip-cache</span></span>|<span data-ttu-id="54205-128">Ответы на запросы не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="54205-128">Do not remember prompt answers.</span></span> <span data-ttu-id="54205-129">По умолчанию: *false*.</span><span class="sxs-lookup"><span data-stu-id="54205-129">Default: *false*.</span></span>
<span data-ttu-id="54205-130">--skip-install</span><span class="sxs-lookup"><span data-stu-id="54205-130">--skip-install</span></span>|<span data-ttu-id="54205-131">Зависимости не устанавливаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="54205-131">Do not automatically install dependencies.</span></span> <span data-ttu-id="54205-132">По умолчанию: *false*.</span><span class="sxs-lookup"><span data-stu-id="54205-132">Default: *false*.</span></span>
<span data-ttu-id="54205-133">--componentType</span><span class="sxs-lookup"><span data-stu-id="54205-133">--componentType</span></span>|<span data-ttu-id="54205-134">Тип компонента.</span><span class="sxs-lookup"><span data-stu-id="54205-134">The type of component.</span></span> <span data-ttu-id="54205-135">Сейчас поддерживаются WebPart и Extension (то есть веб-часть и расширение).</span><span class="sxs-lookup"><span data-stu-id="54205-135">Currently "webpart" or "extension" is supported</span></span>
<span data-ttu-id="54205-136">--componentDescription</span><span class="sxs-lookup"><span data-stu-id="54205-136">--componentDescription</span></span>|<span data-ttu-id="54205-137">Описание компонента.</span><span class="sxs-lookup"><span data-stu-id="54205-137">Description of the component.</span></span>
<span data-ttu-id="54205-138">--componentName</span><span class="sxs-lookup"><span data-stu-id="54205-138">--componentName</span></span>|<span data-ttu-id="54205-139">Имя компонента.</span><span class="sxs-lookup"><span data-stu-id="54205-139">Name of the component.</span></span>
<span data-ttu-id="54205-140">--framework</span><span class="sxs-lookup"><span data-stu-id="54205-140">--framework</span></span>|<span data-ttu-id="54205-p109">Платформа, которую необходимо использовать для решения: React, Knockout или платформа, отличная от JavaScript.</span><span class="sxs-lookup"><span data-stu-id="54205-p109">Framework to use for the solution. Choose one from "none", "react", "knockout".</span></span>
<span data-ttu-id="54205-143">--extensionType</span><span class="sxs-lookup"><span data-stu-id="54205-143">--extensionType</span></span>|<span data-ttu-id="54205-144">Тип расширения. Сейчас поддерживаются ApplicationCustomizer, FieldCustomizer, ListViewCommandSet.</span><span class="sxs-lookup"><span data-stu-id="54205-144">The type of extension: Currently "ApplicationCustomizer", "FieldCustomizer", "ListViewCommandSet"</span></span>
<span data-ttu-id="54205-145">--solutionName</span><span class="sxs-lookup"><span data-stu-id="54205-145">--solutionName</span></span>|<span data-ttu-id="54205-146">Имя клиентского решения, а также имя папки.</span><span class="sxs-lookup"><span data-stu-id="54205-146">Client-side solution name, as well as folder name.</span></span>
<span data-ttu-id="54205-147">--environment</span><span class="sxs-lookup"><span data-stu-id="54205-147">--environment</span></span>|<span data-ttu-id="54205-148">Целевая среда для решения:</span><span class="sxs-lookup"><span data-stu-id="54205-148">The target environment for the solution.</span></span> <span data-ttu-id="54205-149">локальная (onprem) или SharePoint Online (spo).</span><span class="sxs-lookup"><span data-stu-id="54205-149">Either "onprem" or "spo".</span></span>

<br/>

<span data-ttu-id="54205-150">**Доступные аргументы**</span><span class="sxs-lookup"><span data-stu-id="54205-150">**Available arguments**</span></span>

<span data-ttu-id="54205-151">Аргумент</span><span class="sxs-lookup"><span data-stu-id="54205-151">Argument</span></span> | <span data-ttu-id="54205-152">Описание</span><span class="sxs-lookup"><span data-stu-id="54205-152">Description</span></span> | <span data-ttu-id="54205-153">Тип</span><span class="sxs-lookup"><span data-stu-id="54205-153">Type</span></span> | <span data-ttu-id="54205-154">Обязательный</span><span class="sxs-lookup"><span data-stu-id="54205-154">Required</span></span> |
-- | -- | -- | -- |
<span data-ttu-id="54205-155">skipFeatureDeployment</span><span class="sxs-lookup"><span data-stu-id="54205-155">skipFeatureDeployment</span></span> | <span data-ttu-id="54205-156">Если указан, позволяет администратору клиента сделать так, что развертывание компонентов на всех сайтах будет выполнено сразу. В этом случае администратору не нужно будет запускать развертывание компонентов и добавлять приложения на сайтах.</span><span class="sxs-lookup"><span data-stu-id="54205-156">If specified, allow the tenant admin the choice of being able to deploy the components to all sites immediately without running any feature deployment or adding apps in sites.</span></span> | <span data-ttu-id="54205-157">Boolean</span><span class="sxs-lookup"><span data-stu-id="54205-157">Boolean</span></span> | <span data-ttu-id="54205-158">false</span><span class="sxs-lookup"><span data-stu-id="54205-158">false</span></span> | 

<br/>

<span data-ttu-id="54205-159">Ниже приведен пример команды, которая создает решение hello-world со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="54205-159">Below is an example of a command that creates a solution called "hello-world" with a web part "HelloWorld" with "react" framework:</span></span>
- <span data-ttu-id="54205-160">включает веб-часть HelloWorld;</span><span class="sxs-lookup"><span data-stu-id="54205-160">A web part "HelloWorld"</span></span> 
- <span data-ttu-id="54205-161">используется платформа React, предназначенная только для SharePoint Online;</span><span class="sxs-lookup"><span data-stu-id="54205-161">The "react" framework targeted only to SharePoint Online</span></span> 
- <span data-ttu-id="54205-162">предусмотрена возможность развертывания на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="54205-162">Tenant-scoped deployment optional enabled</span></span>

<span data-ttu-id="54205-163">Обратите внимание на то, что некоторые параметры связаны зависимостями.</span><span class="sxs-lookup"><span data-stu-id="54205-163">Notice that some of the options have dependencies between each other.</span></span> <span data-ttu-id="54205-164">Например, невозможно создать расширение с параметром локальной среды.</span><span class="sxs-lookup"><span data-stu-id="54205-164">You cannot for example create extension with on-premises option.</span></span>

```
yo @microsoft/sharepoint 
--solutionName "hello-world" 
--framework "react" 
--componentType "webpart" 
--componentName "HelloWorld" 
--componentDescription "HelloWorld web part" 
--skip-install 
--environment "spo" skipFeatureDeployment true
```

<br/>

> [!NOTE]
> <span data-ttu-id="54205-165">Команда `--skip-install` позволяет сформировать шаблоны проекта, не устанавливая зависимости.</span><span class="sxs-lookup"><span data-stu-id="54205-165">Using the `--skip-install` command scaffolds the project and skips installing dependencies.</span></span> <span data-ttu-id="54205-166">Для успешной сборки проекта вам потребуется установить зависимости позже, после формирования шаблонов проекта.</span><span class="sxs-lookup"><span data-stu-id="54205-166">Using the  command will scaffold the project and skip installing dependencies. This means, to successfully build the project, you will need to install the dependencies later once the project is scaffolded.</span></span> 

> <span data-ttu-id="54205-167">Если вы попытаетесь выполнить сборку проекта без установки зависимостей, возникнет указанная ниже ошибка.</span><span class="sxs-lookup"><span data-stu-id="54205-167">If you try to build your project without installing the dependencies, then you will get the following error. This indicates you need to install the dependencies before building the project:</span></span> <span data-ttu-id="54205-168">Она означает, что вам нужно установить зависимости перед сборкой проекта.</span><span class="sxs-lookup"><span data-stu-id="54205-168">This indicates that you need to install the dependencies before building the project:</span></span>

> ```
> Local gulp not found in ~/<project-name>
> Try running: npm install gulp
> ```

> <span data-ttu-id="54205-169">Вы можете выполнить следующую команду, чтобы установить зависимости:</span><span class="sxs-lookup"><span data-stu-id="54205-169">You can execute the following command to install the dependencies:</span></span>

> ```
> npm install
> ```


## <a name="see-also"></a><span data-ttu-id="54205-170">См. также</span><span class="sxs-lookup"><span data-stu-id="54205-170">See also</span></span>

- [<span data-ttu-id="54205-171">Цепочка инструментов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="54205-171">SharePoint Framework Toolchain</span></span>](sharepoint-framework-toolchain.md)
- [<span data-ttu-id="54205-172">Средства разработки и библиотеки платформы SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="54205-172">SharePoint Framework development tools and libraries</span></span>](../tools-and-libraries.md)
- [<span data-ttu-id="54205-173">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="54205-173">SharePoint Framework Extensions Overview</span></span>](../sharepoint-framework-overview.md)
