---
title: "Обновление пакетов SharePoint Framework"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b8d542ac73d1739faff65f4636cffdef062a3c00
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-sharepoint-framework-packages"></a><span data-ttu-id="f549c-102">Обновление пакетов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="f549c-102">Update SharePoint Framework packages</span></span> 

<span data-ttu-id="f549c-103">Средства клиентской разработки для SharePoint управляют зависимостями и другими необходимыми вспомогательными элементами JavaScript с помощью диспетчера пакетов [npm](https://www.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="f549c-103">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span> <span data-ttu-id="f549c-104">Этот диспетчер обычно устанавливается вместе с Node.js.</span><span class="sxs-lookup"><span data-stu-id="f549c-104">npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="f549c-105">При создании нового клиентского решения генератор Yeoman для SharePoint получает последние версии необходимых для проекта пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="f549c-105">When you create a new client-side solution, the yeoman generator for SharePoint fetches the latest SharePoint Framework packages required for your client-side project.</span></span> <span data-ttu-id="f549c-106">По мере работы над проектом пакеты могут устаревать.</span><span class="sxs-lookup"><span data-stu-id="f549c-106">As you build your project, your existing packages could be outdated as there could be new versions of one or more packages available.</span></span> <span data-ttu-id="f549c-107">Изучив [заметки о выпуске](https://aka.ms/spfx-release-notes), касающиеся определенного выпуска или последней версии пакета, вы можете решить обновить пакеты SharePoint Framework, используемые в проекте.</span><span class="sxs-lookup"><span data-stu-id="f549c-107">Based on the [release notes](https://aka.ms/spfx-release-notes) for a particular release or the latest package, you may decide to update your SharePoint Framework packages used in your project.</span></span> <span data-ttu-id="f549c-108">Пакеты SharePoint Framework включают установленные в проекте пакеты npm, например [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), и глобально установленные пакеты npm, например [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="f549c-108">SharePoint Framework packages include both the npm packages you have installed in your project, for example: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), and npm packages installed globally, for example: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span></span> 

<span data-ttu-id="f549c-109">Рекомендуем время от времени обновлять пакеты SharePoint Framework, чтобы получать доступ к последним изменениям и исправлениям.</span><span class="sxs-lookup"><span data-stu-id="f549c-109">While it may not be required, it is recommended you update the SharePoint Framework packages every so often so that you can get the latest changes and fixes that have been released.</span></span> 

## <a name="find-outdated-packages-in-your-project"></a><span data-ttu-id="f549c-110">Поиск устаревших пакетов в проекте</span><span class="sxs-lookup"><span data-stu-id="f549c-110">Find outdated packages in your project</span></span>
<span data-ttu-id="f549c-111">Чтобы найти устаревшие пакеты, в том числе пакеты SharePoint Framework и другие пакеты, от которых зависит проект, перейдите в каталог проекта и выполните в нем следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f549c-111">To find the outdated packages in your client-side project, including SharePoint Framework and other packages your project depends on, run the following command in a console in the same directory as your project.</span></span> 

```
npm outdated
```

<span data-ttu-id="f549c-112">На основе файла</span><span class="sxs-lookup"><span data-stu-id="f549c-112">The command will list the following information about the packages your project depends on. This information is looked up from the  file located in the root of your project directory and npm registry.</span></span> <span data-ttu-id="f549c-113">`package.json`, расположенного в корневом каталоге проекта, и реестра npm будут выведены следующие сведения о пакетах:</span><span class="sxs-lookup"><span data-stu-id="f549c-113">The command will list the following information about the packages your project depends on. This information is looked up from the `package.json` file located in the root of your project directory and npm registry.</span></span>

* <span data-ttu-id="f549c-114">версия, установленная в проекте;</span><span class="sxs-lookup"><span data-stu-id="f549c-114">Current version installed in your project</span></span>
* <span data-ttu-id="f549c-115">версия, запрашиваемая проектом (указана в файле `package.json`);</span><span class="sxs-lookup"><span data-stu-id="f549c-115">Version requested by your project (available in `package.json`)</span></span>
* <span data-ttu-id="f549c-116">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="f549c-116">Latest version available</span></span>

![Устаревшие пакеты NPM](../../images/npm-outdated-packages-list.png)

<span data-ttu-id="f549c-118">Имена пакетов SharePoint Framework начинаются с такого идентификатора области npm и префикса:</span><span class="sxs-lookup"><span data-stu-id="f549c-118">To identify the SharePoint Framework packages, look for the package names that start with the following npm scope and prefix:</span></span>

```
@microsoft/sp-
```
<span data-ttu-id="f549c-119">Помимо пакетов Framework вам также может понадобиться обновить пакеты `react` и `office-ui-fabric-react`.</span><span class="sxs-lookup"><span data-stu-id="f549c-119">Along with the framework packages, you may also need to update `react` and `office-ui-fabric-react` packages.</span></span> <span data-ttu-id="f549c-120">Обязательно ознакомьтесь с [заметками о конкретном выпуске](https://aka.ms/spfx-release-notes), чтобы определить, какие пакеты нужно обновить, и запланируйте обновление.</span><span class="sxs-lookup"><span data-stu-id="f549c-120">Along with the framework packages, you may also need to update  and  packages. Make sure you read the [release notes](https://aka.ms/spfx-release-notes) for that specific release to infer which packages require updates and plan accordingly.</span></span>

### <a name="update-packages"></a><span data-ttu-id="f549c-121">Обновление пакетов</span><span class="sxs-lookup"><span data-stu-id="f549c-121">Update packages</span></span>
<span data-ttu-id="f549c-122">Чтобы обновить пакеты до последней версии, необходимо изменить сведения о них в файле `package.json`, а затем получить новые пакеты.</span><span class="sxs-lookup"><span data-stu-id="f549c-122">To update one or more packages to the latest version, you will need to edit the package(s) information in the `package.json` file and then fetch the latest packages.</span></span>

#### <a name="update-package-versions"></a><span data-ttu-id="f549c-123">Изменение версий пакетов</span><span class="sxs-lookup"><span data-stu-id="f549c-123">Update package versions</span></span>
<span data-ttu-id="f549c-124">Откройте проект в любом редакторе кода и найдите файл `package.json` в корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="f549c-124">Open your project in your favorite code editor and locate the `package.json` file in the root of your project directory.</span></span>

<span data-ttu-id="f549c-125">В файле `package.json` найдите пакеты в разделах `dependencies` и `devDependencies` и измените версию на последнюю доступную версию, указанную в команде `npm outdated`.</span><span class="sxs-lookup"><span data-stu-id="f549c-125">In the `package.json` file, locate the package(s) under the `dependencies` and `devDependencies` section and update the version to the latest version available that was listed in the `npm outdated` command. For example, the image below highlights the version updates to SharePoint Framework packages, the left section referring to the old and the right section referring to the latest package versions.</span></span> <span data-ttu-id="f549c-126">Например, на изображении ниже выделены измененные версии пакетов SharePoint Framework (слева — старые, а справа — новые).</span><span class="sxs-lookup"><span data-stu-id="f549c-126">In the  file, locate the package(s) under the  and  section and update the version to the latest version available that was listed in the  command. For example, the image below highlights the version updates to SharePoint Framework packages, the left section referring to the old and the right section referring to the latest package versions.</span></span>

![Изменение версий пакетов в файле package.json](../../images/npm-update-packagejson-versions.png)

<span data-ttu-id="f549c-128">После изменения версий пакетов сохраните файл `package.json`.</span><span class="sxs-lookup"><span data-stu-id="f549c-128">Once you have updated the package versions, Save the `package.json` file.</span></span>

#### <a name="update-packages"></a><span data-ttu-id="f549c-129">Обновление пакетов</span><span class="sxs-lookup"><span data-stu-id="f549c-129">Update packages</span></span>
<span data-ttu-id="f549c-p106">Откройте любую консоль и перейдите в корневой каталог проекта. Следуйте приведенным ниже инструкциям, чтобы обновить пакеты до последней версии.</span><span class="sxs-lookup"><span data-stu-id="f549c-p106">Open your favorite console and navigate to the root of your project directory. Follow the instructions below to successfully update the packages to its latest version.</span></span>

<span data-ttu-id="f549c-132">Удалите папку `node_modules`.</span><span class="sxs-lookup"><span data-stu-id="f549c-132">Delete the content of the folder `node_modules`.</span></span> <span data-ttu-id="f549c-133">В этой папке npm локально устанавливает пакеты для проекта.</span><span class="sxs-lookup"><span data-stu-id="f549c-133">Delete the  folder. This is the folder where npm installs the packages locally for your project. Deleting this folder forces npm to fetch the latest and not duplicate existing packages.</span></span> <span data-ttu-id="f549c-134">Если удалить эту папку, npm получит новые пакеты, а не будет копировать существующие.</span><span class="sxs-lookup"><span data-stu-id="f549c-134">Delete the  folder. This is the folder where npm installs the packages locally for your project. Deleting this folder forces npm to fetch the latest and not duplicate existing packages.</span></span>

<span data-ttu-id="f549c-135">Если вы используете компьютер Mac или среду Linux, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f549c-135">If you are using a Mac or a Linux environment, then run the following command:</span></span>

```
rm -rf node_modules/
```

<span data-ttu-id="f549c-136">Если вы используете среду Windows, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f549c-136">If you are using a Windows environment, then run the following command:</span></span>

```
 rd /s /q node_modules/
```

<span data-ttu-id="f549c-137">Теперь выполните следующую команду, чтобы получить новые пакеты из реестра npm:</span><span class="sxs-lookup"><span data-stu-id="f549c-137">Now, execute the following command to fetch the latest packages from the npm registry:</span></span>

```
npm install
```

<span data-ttu-id="f549c-138">Эта команда создаст папку `node_modules` и установит все пакеты, от которых зависит проект, а также их зависимости на основе данных из файла `package.json`.</span><span class="sxs-lookup"><span data-stu-id="f549c-138">This command will create the `node_modules` folder and install all the packages your project depends on and its dependencies based on the information available in the `package.json` file. As we updated the file with the latest versions, npm will now have the latest packages and their dependencies installed.</span></span> <span data-ttu-id="f549c-139">Npm установит последние версии и все их взаимосвязи, так как именно эти версии мы указали в файле.</span><span class="sxs-lookup"><span data-stu-id="f549c-139">This command will create the  folder and install all the packages your project depends on and its dependencies based on the information available in the  file. As we updated the file with the latest versions, npm will now have the latest packages and their dependencies installed.</span></span> 

<span data-ttu-id="f549c-140">После установки пакетов выполните следующую команду, чтобы удалить артефакты старой сборки:</span><span class="sxs-lookup"><span data-stu-id="f549c-140">Once the packages are installed, execute the following command to clean up any old build artifacts:</span></span>

```
gulp clean
```

### <a name="update-your-code"></a><span data-ttu-id="f549c-141">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="f549c-141">Update your code</span></span>
<span data-ttu-id="f549c-142">В зависимости от того, насколько существенно изменен API, может потребоваться обновить существующий код и файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="f549c-142">Depending on breaking API changes, you may have to update your existing project code and config files.</span></span> <span data-ttu-id="f549c-143">О существенных изменениях и модификациях, которые нужно внести в существующий код, можно узнать из [заметок о выпуске](https://aka.ms/spfx-release-notes).</span><span class="sxs-lookup"><span data-stu-id="f549c-143">For each release, the [release notes](https://aka.ms/spfx-release-notes) will highlight any such breaking changes and the modifications required to your existing code.</span></span> <span data-ttu-id="f549c-144">Внесите необходимые исправления в код.</span><span class="sxs-lookup"><span data-stu-id="f549c-144">You will need to make sure you update your code with those fixes.</span></span>

<span data-ttu-id="f549c-145">Вы всегда можете выполнить сборку проекта, чтобы посмотреть, есть ли ошибки и предупреждения, выполнив команду в консоли в каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="f549c-145">You can always build the project to see if you have any errors and warnings by running the command in a console in your project directory:</span></span>

```
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a><span data-ttu-id="f549c-146">Обновление генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f549c-146">Update yeoman generator for SharePoint</span></span>
<span data-ttu-id="f549c-147">В отличие от пакетов npm, которые устанавливаются под определенный клиентский проект, генератор Yeoman для SharePoint устанавливается на компьютере глобально.</span><span class="sxs-lookup"><span data-stu-id="f549c-147">Unlike the npm packages that are installed to a specific client-side project, the yeoman generator for SharePoint is installed globally in your machine.</span></span>

<span data-ttu-id="f549c-148">Чтобы узнать, устарел ли генератор Yeoman для SharePoint, выполните в консоли указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="f549c-148">To find if the yeoman generator for SharePoint is out of date, run the following command in a console window.</span></span> 

```
npm outdated -g
```

<span data-ttu-id="f549c-p110">На основе версий, установленных на компьютере, и реестра npm будут выведены следующие сведения о глобально установленных на компьютере пакетах:</span><span class="sxs-lookup"><span data-stu-id="f549c-p110">The command will list the following information about the packages installed globally in your machine. This information is looked up from the versions installed in your machine and the npm registry.</span></span>

* <span data-ttu-id="f549c-151">текущая версия, глобально установленная на компьютере;</span><span class="sxs-lookup"><span data-stu-id="f549c-151">Current version installed globally in your machine</span></span>
* <span data-ttu-id="f549c-152">версия, которую вы запросили при установке;</span><span class="sxs-lookup"><span data-stu-id="f549c-152">Version requested by you when you installed</span></span>
* <span data-ttu-id="f549c-153">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="f549c-153">Latest version available</span></span>

![Устаревшие глобальные пакеты NPM](../../images/npm-outdated-global-packages-list.png)

<span data-ttu-id="f549c-155">Имя пакета генератора выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f549c-155">To identify the generator package, look for the following package name:</span></span>

```
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a><span data-ttu-id="f549c-156">Обновление пакета генератора</span><span class="sxs-lookup"><span data-stu-id="f549c-156">Update generator package</span></span>
<span data-ttu-id="f549c-157">Чтобы обновить генератор до последней опубликованной версии, откройте любую консоль и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f549c-157">Open your favorite console and execute the following command to update the generator to its latest published version:</span></span>

```
npm install @microsoft/generator-sharepoint@latest -g
```

<span data-ttu-id="f549c-p111">Команда обновит генератор Yeoman для SharePoint и его зависимости до последней опубликованной версии. Для проверки выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f549c-p111">The command will update the yeoman generator for SharePoint to the latest published version along with its depedencies. You can validate this by executing the following command in the console:</span></span>

```
npm ls @microsoft/generator-sharepoint -g --depth=0
```






 
