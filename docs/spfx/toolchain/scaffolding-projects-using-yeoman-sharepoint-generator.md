# <a name="scaffold-projects-using-yeoman-sharepoint-generator"></a><span data-ttu-id="2aec4-101">Скаффолдинг проектов с помощью генератора yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2aec4-101">Scaffold projects using yeoman SharePoint generator</span></span>

<span data-ttu-id="2aec4-p101">[Yeoman](http://yeoman.io/) помогает эффективно запускать новые проекты благодаря соответствующим рекомендациям и инструментам. С помощью генератора yeoman для SharePoint разработчики могут инициализировать проекты, чтобы создавать, упаковывать и развертывать решения SharePoint. Генератор предоставляет стандартные инструменты сборки, стереотипный код и стандартный веб-сайт для тестирования веб-частей.</span><span class="sxs-lookup"><span data-stu-id="2aec4-p101">[Yeoman](http://yeoman.io/) helps you to kickstart new projects, prescribing best practices and tools to help you stay productive. Using the yeoman SharePoint generator, developers are able to scaffold new client-side solution projects to build, package and deploy SharePoint solutions. The generator provides common build tools, boilerplate code, and a common playground web site to host web parts for testing.</span></span>

## <a name="installing-the-yeoman-sharepoint-generator"></a><span data-ttu-id="2aec4-105">Установка генератора yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2aec4-105">Installing the yeoman SharePoint generator</span></span>

<span data-ttu-id="2aec4-p102">Генератор yeoman для SharePoint доступен в составе платформы как [пакет npm](https://www.npmjs.com/package/@microsoft/generator-sharepoint). Чтобы установить генератор, выполните следующую команду в консоли:</span><span class="sxs-lookup"><span data-stu-id="2aec4-p102">Yeoman SharePoint generator is available as part of the framework as a [npm package](https://www.npmjs.com/package/@microsoft/generator-sharepoint). You can install the generator by executing the following command in a console:</span></span>

```
npm install @microsoft/generator-sharepoint -g
```

><span data-ttu-id="2aec4-p103">**Примечание.** Генератор yeoman для SharePoint должен развертываться глобально с первой общедоступной версией. Существуют известные проблемы при локальной установке в проекте, которые планируется устранить после выпуска общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="2aec4-p103">**Note:** Yeoman generator for SharePoint is targeted to get deployed globally with the initial General Availability (GA) version. There are some known issues if it's installed locally to the project, which are planned to be addressed post GA.</span></span>

<span data-ttu-id="2aec4-110">Рекомендуем воспользоваться [этими инструкциями](../set-up-your-development-environment.md), чтобы установить на компьютер полный набор инструментов разработчика, в том числе генератор yeoman для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2aec4-110">It is recommended you follow the [set up your development environment](../set-up-your-development-environment.md) to configure your machine with the complete set of developer tools, including yeoman SharePoint generator.</span></span> 

## <a name="using-the-yeoman-sharepoint-generator"></a><span data-ttu-id="2aec4-111">Использование генератора yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2aec4-111">Using the yeoman SharePoint generator</span></span>

<span data-ttu-id="2aec4-112">Чтобы вызвать генератор после установки, просто введите следующую команду в консоли:</span><span class="sxs-lookup"><span data-stu-id="2aec4-112">Once the generator is installed, you can invoke the generator by just typing the following command in a console:</span></span>

```
yo
```

<span data-ttu-id="2aec4-p104">Появится список всех генераторов, доступных на вашем компьютере. Выберите `@microsoft/sharepoint`, чтобы вызвать генератор SharePoint и следуйте инструкциям, чтобы создать клиентское решение:</span><span class="sxs-lookup"><span data-stu-id="2aec4-p104">The command will list all of the generators available in your machine. Select the `@microsoft/sharepoint` to invoke the SharePoint generator and continue with the prompts to successfully create your client-side solution:</span></span>

![Генератор yeoman для SharePoint](../../images/yeoman-sp-generator.png)

## <a name="available-command-line-options-for-the-generator"></a><span data-ttu-id="2aec4-116">Доступные параметры командной строки для генератора</span><span class="sxs-lookup"><span data-stu-id="2aec4-116">Available command line options for the generator</span></span>

<span data-ttu-id="2aec4-117">Параметры командной строки, доступные генератору Yeoman для SharePoint, позволяют не следовать отображаемым на экране инструкциям, а выполнять скаффолдинг проектов с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="2aec4-117">You can use the command line options available with the yeoman SharePoint generator to scaffold projects in one command instead of going through the prompts. Execute the following command to see the list of  command line options available for the SharePoint generator:</span></span> <span data-ttu-id="2aec4-118">Выполните следующую команду, чтобы просмотреть список параметров командной строки, доступных генератору Yeoman для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="2aec4-118">Execute the following command to see the list of command line options available for the SharePoint generator:</span></span>

```
yo @microsoft/generator-sharepoint --help
```

![Параметры командной строки, доступные генератору Yeoman для SharePoint](../../images/yeoman-sp-cmdline-options.png)

<span data-ttu-id="2aec4-120">Параметр</span><span class="sxs-lookup"><span data-stu-id="2aec4-120">Option</span></span> | <span data-ttu-id="2aec4-121">Описание</span><span class="sxs-lookup"><span data-stu-id="2aec4-121">Description</span></span> 
-----|------
<span data-ttu-id="2aec4-122">--help</span><span class="sxs-lookup"><span data-stu-id="2aec4-122">HELP</span></span>|<span data-ttu-id="2aec4-123">Печать сведений об использовании генератора и его параметров.</span><span class="sxs-lookup"><span data-stu-id="2aec4-123">Print the generator's options and usage.</span></span>
<span data-ttu-id="2aec4-124">--skip-cache</span><span class="sxs-lookup"><span data-stu-id="2aec4-124">--skip-cache</span></span>|<span data-ttu-id="2aec4-125">Ответы на запросы не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="2aec4-125">Do not remember prompt answers.</span></span> <span data-ttu-id="2aec4-126">По умолчанию: *false*.</span><span class="sxs-lookup"><span data-stu-id="2aec4-126">Default: *False*</span></span>
<span data-ttu-id="2aec4-127">--skip-install</span><span class="sxs-lookup"><span data-stu-id="2aec4-127">--skip-install</span></span>|<span data-ttu-id="2aec4-128">Зависимости не устанавливаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="2aec4-128">Do no automatically install dependencies.</span></span> <span data-ttu-id="2aec4-129">По умолчанию: *false*.</span><span class="sxs-lookup"><span data-stu-id="2aec4-129">Default: *False*</span></span>
<span data-ttu-id="2aec4-130">--componentType</span><span class="sxs-lookup"><span data-stu-id="2aec4-130">--componentType</span></span>|<span data-ttu-id="2aec4-131">Тип компонента.</span><span class="sxs-lookup"><span data-stu-id="2aec4-131">The type of component.</span></span> <span data-ttu-id="2aec4-132">Сейчас поддерживаются WebPart и Extension (то есть веб-часть и расширение).</span><span class="sxs-lookup"><span data-stu-id="2aec4-132">Currently "webpart" or "extension" is supported</span></span>
<span data-ttu-id="2aec4-133">--componentDescription</span><span class="sxs-lookup"><span data-stu-id="2aec4-133">--componentDescription</span></span>|<span data-ttu-id="2aec4-134">Описание компонента.</span><span class="sxs-lookup"><span data-stu-id="2aec4-134">Description of the component.</span></span>
<span data-ttu-id="2aec4-135">--componentName</span><span class="sxs-lookup"><span data-stu-id="2aec4-135">--componentName</span></span>|<span data-ttu-id="2aec4-136">Имя компонента.</span><span class="sxs-lookup"><span data-stu-id="2aec4-136">Name of the component.</span></span>
<span data-ttu-id="2aec4-137">--framework</span><span class="sxs-lookup"><span data-stu-id="2aec4-137">--framework</span></span>|<span data-ttu-id="2aec4-p109">Платформа, которую необходимо использовать для решения: React, Knockout или платформа, отличная от JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2aec4-p109">Framework to use for the solution. Choose one from "none", "react", "knockout".</span></span>
<span data-ttu-id="2aec4-140">--extensionType</span><span class="sxs-lookup"><span data-stu-id="2aec4-140">--extensionType</span></span>|<span data-ttu-id="2aec4-141">Тип расширения. Сейчас поддерживаются ApplicationCustomizer, FieldCustomizer, ListViewCommandSet.</span><span class="sxs-lookup"><span data-stu-id="2aec4-141">The type of extension: Currently "ApplicationCustomizer", "FieldCustomizer", "ListViewCommandSet"</span></span>
<span data-ttu-id="2aec4-142">--solutionName</span><span class="sxs-lookup"><span data-stu-id="2aec4-142">--solutionName</span></span>|<span data-ttu-id="2aec4-143">Имя клиентского решения, а также имя папки.</span><span class="sxs-lookup"><span data-stu-id="2aec4-143">Client-side solution name, as well as folder name.</span></span>
<span data-ttu-id="2aec4-144">--environment</span><span class="sxs-lookup"><span data-stu-id="2aec4-144">Environment</span></span>|<span data-ttu-id="2aec4-145">Целевая среда для решения:</span><span class="sxs-lookup"><span data-stu-id="2aec4-145">The target environment for the solution.</span></span> <span data-ttu-id="2aec4-146">локальная (onprem) или SharePoint Online (spo).</span><span class="sxs-lookup"><span data-stu-id="2aec4-146">Either "onprem" or "spo".</span></span>

<span data-ttu-id="2aec4-147">В приведенной ниже таблице указаны доступные аргументы.</span><span class="sxs-lookup"><span data-stu-id="2aec4-147">Following table lists the available arguments.</span></span>

<span data-ttu-id="2aec4-148">Аргумент</span><span class="sxs-lookup"><span data-stu-id="2aec4-148">Argument</span></span> | <span data-ttu-id="2aec4-149">Описание</span><span class="sxs-lookup"><span data-stu-id="2aec4-149">Description</span></span> | <span data-ttu-id="2aec4-150">Тип</span><span class="sxs-lookup"><span data-stu-id="2aec4-150">Type</span></span> | <span data-ttu-id="2aec4-151">Обязательный</span><span class="sxs-lookup"><span data-stu-id="2aec4-151">Required</span></span> |
-- | -- | -- | -- |
<span data-ttu-id="2aec4-152">skipFeatureDeployment</span><span class="sxs-lookup"><span data-stu-id="2aec4-152">skipFeatureDeployment</span></span> | <span data-ttu-id="2aec4-153">Если указан, позволяет администратору клиента сделать так, что развертывание компонентов на всех сайтах будет выполнено сразу. В этом случае администратору не нужно будет запускать развертывание компонентов и добавлять приложения на сайтах.</span><span class="sxs-lookup"><span data-stu-id="2aec4-153">If specified, allow the tenant admin the choice of being able to deploy the components to all sites immediately without running any feature deployment or adding apps in sites.</span></span> | <span data-ttu-id="2aec4-154">Boolean</span><span class="sxs-lookup"><span data-stu-id="2aec4-154">Boolean</span></span> | <span data-ttu-id="2aec4-155">false</span><span class="sxs-lookup"><span data-stu-id="2aec4-155">false</span></span> | 

<span data-ttu-id="2aec4-156">Ниже приведен пример команды, которая создает решение hello-world с веб-частью HelloWorld на платформе React, предназначенное только для SharePoint Online и предусматривающее возможность развертывания на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="2aec4-156">Below is an example of a command that creates a solution called "hello-world" with a web part "HelloWorld" with "react" framework targeted only to SharePoint Online with tenant-scoped deployment optional enabled:</span></span>

```
yo @microsoft/sharepoint --solutionName "hello-world" --framework "react" --componentType "webpart" --componentName "HelloWorld" --componentDescription "HelloWorld web part" --skip-install --environment "spo" skipFeatureDeployment true
```

> <span data-ttu-id="2aec4-157">Обратите внимание на то, что некоторые параметры связаны зависимостями.</span><span class="sxs-lookup"><span data-stu-id="2aec4-157">Notice that some of the options have dependencies between each other.</span></span> <span data-ttu-id="2aec4-158">Вы не можете создать, например, расширение с параметром локальной среды.</span><span class="sxs-lookup"><span data-stu-id="2aec4-158">You cannot for example create extension with on-premises option.</span></span>

### <a name="notes-on---skip-install"></a><span data-ttu-id="2aec4-159">Примечания по --skip-install</span><span class="sxs-lookup"><span data-stu-id="2aec4-159">Notes on --skip-install</span></span> 

<span data-ttu-id="2aec4-p112">Команда `--skip-install` позволяет инициализировать проект, не устанавливая зависимости. Для успешной сборки проекта вам потребуется установить зависимости позже после скаффолдинга проекта.</span><span class="sxs-lookup"><span data-stu-id="2aec4-p112">Using the `--skip-install` command will scaffold the project and skip installing dependencies. This means, to successfully build the project, you will need to install the dependencies later once the project is scaffolded.</span></span> 

<span data-ttu-id="2aec4-p113">При сборке проекта без установки зависимостей возникнет следующая ошибка. Она означает, что вам нужно установить зависимости перед сборкой проекта:</span><span class="sxs-lookup"><span data-stu-id="2aec4-p113">If you try to build your project without installing the dependencies, then you will get the following error. This indicates you need to install the dependencies before building the project:</span></span>

```
Local gulp not found in ~/<project-name>
Try running: npm install gulp
```

<span data-ttu-id="2aec4-164">Вы можете выполнить следующую команду, чтобы установить зависимости:</span><span class="sxs-lookup"><span data-stu-id="2aec4-164">You can execute the following command to install the dependencies:</span></span>

```
npm install
```
