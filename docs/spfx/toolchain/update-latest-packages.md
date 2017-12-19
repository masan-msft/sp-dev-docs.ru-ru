---
title: "Обновление пакетов SharePoint Framework"
ms.date: 11/29/2017
ms.prod: sharepoint
ms.openlocfilehash: decc266ab1f5d06e3e3a804ba65b06bfac8ac9c3
ms.sourcegitcommit: 46d5fee38ab8849df2d47541ee53b4dd71a613db
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2017
---
# <a name="update-sharepoint-framework-packages"></a><span data-ttu-id="d8d61-102">Обновление пакетов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="d8d61-102">Update SharePoint Framework packages</span></span>

<span data-ttu-id="d8d61-103">Средства клиентской разработки для SharePoint управляют зависимостями и другими необходимыми вспомогательными элементами JavaScript с помощью диспетчера пакетов [npm](https://www.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="d8d61-103">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager to manage dependencies and other required JavaScript helpers. npm is typically included as part of Node.js setup.</span></span> <span data-ttu-id="d8d61-104">Этот диспетчер обычно устанавливается вместе с Node.js.</span><span class="sxs-lookup"><span data-stu-id="d8d61-104">npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="d8d61-105">При создании нового клиентского решения генератор Yeoman для SharePoint получает последние версии необходимых для проекта пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="d8d61-105">When you create a new client-side solution, the yeoman generator for SharePoint fetches the latest SharePoint Framework packages required for your client-side project.</span></span> <span data-ttu-id="d8d61-106">По мере работы над проектом пакеты могут устаревать.</span><span class="sxs-lookup"><span data-stu-id="d8d61-106">As you build your project, your existing packages could be outdated as there could be new versions of one or more packages available.</span></span> <span data-ttu-id="d8d61-107">Изучив [заметки о выпуске](https://aka.ms/spfx-release-notes), касающиеся определенного выпуска или последней версии пакета, вы можете решить обновить пакеты SharePoint Framework, используемые в проекте.</span><span class="sxs-lookup"><span data-stu-id="d8d61-107">Based on the [release notes](https://aka.ms/spfx-release-notes) for a particular release or the latest package, you may decide to update your SharePoint Framework packages used in your project.</span></span> <span data-ttu-id="d8d61-108">Пакеты SharePoint Framework включают установленные в проекте пакеты npm, например [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), и глобально установленные пакеты npm, например [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="d8d61-108">SharePoint Framework packages include both the npm packages you have installed in your project, for example: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), and npm packages installed globally, for example: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span></span> 

> [!TIP]
> <span data-ttu-id="d8d61-109">Рекомендуем время от времени обновлять пакеты SharePoint Framework, чтобы получать доступ к последним изменениям и исправлениям.</span><span class="sxs-lookup"><span data-stu-id="d8d61-109">While it may not be required, it is recommended you update the SharePoint Framework packages every so often so that you can get the latest changes and fixes that have been released.</span></span>

## <a name="find-outdated-packages-in-your-project"></a><span data-ttu-id="d8d61-110">Поиск устаревших пакетов в проекте</span><span class="sxs-lookup"><span data-stu-id="d8d61-110">Find outdated packages in your project</span></span>

<span data-ttu-id="d8d61-111">Чтобы найти устаревшие пакеты, в том числе пакеты SharePoint Framework и другие пакеты, от которых зависит проект, перейдите в каталог проекта и выполните в нем следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d8d61-111">To find the outdated packages in your client-side project, including SharePoint Framework and other packages your project depends on, run the following command in a console in the same directory as your project.</span></span> 

```sh
npm outdated
```

<span data-ttu-id="d8d61-112">На основе файла</span><span class="sxs-lookup"><span data-stu-id="d8d61-112">The command will list the following information about the packages your project depends on. This information is looked up from the  file located in the root of your project directory and npm registry.</span></span> <span data-ttu-id="d8d61-113">`package.json`, расположенного в корневом каталоге проекта, и реестра npm будут выведены следующие сведения о пакетах:</span><span class="sxs-lookup"><span data-stu-id="d8d61-113">The command will list the following information about the packages your project depends on. This information is looked up from the `package.json` file located in the root of your project directory and npm registry.</span></span>

* <span data-ttu-id="d8d61-114">версия, установленная в проекте;</span><span class="sxs-lookup"><span data-stu-id="d8d61-114">Current version installed in your project</span></span>
* <span data-ttu-id="d8d61-115">версия, запрашиваемая проектом (указана в файле `package.json`);</span><span class="sxs-lookup"><span data-stu-id="d8d61-115">Version requested by your project (available in `package.json`)</span></span>
* <span data-ttu-id="d8d61-116">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="d8d61-116">Latest version available</span></span>

![Устаревшие пакеты NPM](../../images/npm-outdated-packages-list.png)

<span data-ttu-id="d8d61-118">Имена пакетов SharePoint Framework начинаются с такого идентификатора области npm и префикса:</span><span class="sxs-lookup"><span data-stu-id="d8d61-118">To identify the SharePoint Framework packages, look for the package names that start with the following npm scope and prefix:</span></span>

```text
@microsoft/sp-
```

<span data-ttu-id="d8d61-119">Помимо пакетов Framework вам также может понадобиться обновить пакеты `react` и `office-ui-fabric-react`.</span><span class="sxs-lookup"><span data-stu-id="d8d61-119">Along with the framework packages, you may also need to update `react` and `office-ui-fabric-react` packages.</span></span> <span data-ttu-id="d8d61-120">Обязательно ознакомьтесь с [заметками о конкретном выпуске](https://aka.ms/spfx-release-notes), чтобы определить, какие пакеты нужно обновить, и запланируйте обновление.</span><span class="sxs-lookup"><span data-stu-id="d8d61-120">Along with the framework packages, you may also need to update  and  packages. Make sure you read the [release notes](https://aka.ms/spfx-release-notes) for that specific release to infer which packages require updates and plan accordingly.</span></span>

### <a name="using-npm-outdated-with-project-targeting-sharepoint-2016"></a><span data-ttu-id="d8d61-121">Использование npm предыдущей версии в проекте для SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="d8d61-121">Using npm outdated with project targeting SharePoint 2016</span></span>

<span data-ttu-id="d8d61-122">Начиная с пакета дополнительных компонентов 2, SharePoint 2016 поддерживает решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="d8d61-122">Starting from Feature Pack 2, SharePoint 2016 supports SharePoint Framework solutions.</span></span> <span data-ttu-id="d8d61-123">SharePoint 2016 использует версию SharePoint Framework, выпущенную раньше той, которая доступна в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d8d61-123">SharePoint 2016 uses an older version of the SharePoint Framework, than the version available in SharePoint Online.</span></span> <span data-ttu-id="d8d61-124">При скаффолдинге новых проектов генератор Yeoman для SharePoint Framework предложит указать, какую версию должно использовать решение. Если оно будет использовать последнюю версию SharePoint Framework, оно будет работать только в SharePoint Online, если более старую — оно будет работать в SharePoint 2016 и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d8d61-124">When scaffolding new projects, the SharePoint Framework Yeoman generator prompts you to choose if your solution should be using the latest version of the SharePoint Framework and be working only with SharePoint Online or if it should use an older version of the SharePoint Framework and work with both SharePoint 2016 and SharePoint Online.</span></span>

<span data-ttu-id="d8d61-125">Когда вы выполните команду `npm outdated` в проекте для SharePoint Online и SharePoint 2016, отобразятся последние версии пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="d8d61-125">When you run the `npm outdated` command in a project targeting both SharePoint Online and SharePoint 2016, it will show you the latest versions of the SharePoint Framework packages.</span></span> <span data-ttu-id="d8d61-126">Эти версии работают только в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="d8d61-126">These versions however work only with SharePoint Online.</span></span> <span data-ttu-id="d8d61-127">Если вы обновите свое решение так, чтобы оно использовало эти последние пакеты, оно перестанет работать в SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="d8d61-127">If you would update your solution to use these latest packages, it would not work with SharePoint 2016 anymore.</span></span>

<span data-ttu-id="d8d61-128">Работая с решениями SharePoint Framework, совместимыми с локальной средой SharePoint, всегда проверяйте, какой уровень исправления у целевой фермы SharePoint и какую версию SharePoint Framework она поддерживает.</span><span class="sxs-lookup"><span data-stu-id="d8d61-128">When working with SharePoint Framework solutions compatible with SharePoint hosted on-premises, you should always verify which patch level the target SharePoint farm has and which version of the SharePoint Framework it supports.</span></span>

### <a name="update-packages"></a><span data-ttu-id="d8d61-129">Обновление пакетов</span><span class="sxs-lookup"><span data-stu-id="d8d61-129">Update packages</span></span>

<span data-ttu-id="d8d61-130">При обновлении версий пакетов всегда используйте диспетчер пакетов (npm или Yarn).</span><span class="sxs-lookup"><span data-stu-id="d8d61-130">When updating packages to newer versions, you should always use your package manager (npm or Yarn).</span></span> <span data-ttu-id="d8d61-131">Не следует редактировать файл `package.json` вручную.</span><span class="sxs-lookup"><span data-stu-id="d8d61-131">You should not edit the `package.json` file manually.</span></span> <span data-ttu-id="d8d61-132">Если вы будете следовать рекомендациям по использованию файла блокировки, изменения, внесенные в файл `package.json`, будут проигнорированы.</span><span class="sxs-lookup"><span data-stu-id="d8d61-132">If you follow the recommended practice of using a lock file, your changes to the `package.json` file would be ignored.</span></span>

<span data-ttu-id="d8d61-133">Начните с определения того, какие пакеты нужно обновить и какие новые версии хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="d8d61-133">Start with identifying which packages need updating and which newer version you want to use.</span></span> <span data-ttu-id="d8d61-134">Обратите внимание на то, что не всегда возможно использовать последнюю версию определенного пакета, так как она может быть несовместима с другими зависимостями SharePoint Framework, такими как TypeScript.</span><span class="sxs-lookup"><span data-stu-id="d8d61-134">Please note, that it might not always be possible for you to use the latest version of the given package as it might be incompatible with other SharePoint Framework dependencies, such as TypeScript.</span></span>

<span data-ttu-id="d8d61-135">Для каждого пакета, который нужно обновить, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d8d61-135">For each package that you want to update, run the following command:</span></span>

```sh
npm install mypackage@newversion --save
```

<span data-ttu-id="d8d61-136">Например, если вы используете AngularJS версии 1.5.9 и хотите выполнить обновление до версии 1.6.5, нужно выполнить такую команду:</span><span class="sxs-lookup"><span data-stu-id="d8d61-136">For example, if you were using AngularJS version v1.5.9 and wanted to update to version 1.6.5, you would run:</span></span>

```sh
npm install angular@1.6.5 --save
```

<span data-ttu-id="d8d61-137">При обновлении пакета с помощью npm установится указанная версия пакета в проекте, а также обновится номер версии в зависимостях файла package.json и файл блокировки, используемый в проекте.</span><span class="sxs-lookup"><span data-stu-id="d8d61-137">Updating the package using npm will install the specified version of the package in your project, update the version number in the package.json file dependencies and the lock file used in your project.</span></span>

<span data-ttu-id="d8d61-138">После установки пакетов выполните следующую команду, чтобы очистить артефакты старой сборки:</span><span class="sxs-lookup"><span data-stu-id="d8d61-138">Once the packages are installed, execute the following command to clean up any old build artifacts:</span></span>

```sh
gulp clean
```

### <a name="update-your-code"></a><span data-ttu-id="d8d61-139">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="d8d61-139">Update your code</span></span>

<span data-ttu-id="d8d61-140">В зависимости от того, насколько существенно изменен API, может потребоваться обновить существующий код и файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="d8d61-140">Depending on breaking API changes, you may have to update your existing project code and config files.</span></span> <span data-ttu-id="d8d61-141">О существенных изменениях и модификациях, которые нужно внести в существующий код, можно узнать из [заметок о выпуске](https://aka.ms/spfx-release-notes).</span><span class="sxs-lookup"><span data-stu-id="d8d61-141">For each release, the [release notes](https://aka.ms/spfx-release-notes) will highlight any such breaking changes and the modifications required to your existing code.</span></span> <span data-ttu-id="d8d61-142">Внесите необходимые исправления в код.</span><span class="sxs-lookup"><span data-stu-id="d8d61-142">You will need to make sure you update your code with those fixes.</span></span>

<span data-ttu-id="d8d61-143">Вы всегда можете выполнить сборку проекта, чтобы посмотреть, есть ли ошибки и предупреждения, выполнив команду в консоли в каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="d8d61-143">You can always build the project to see if you have any errors and warnings by running the command in a console in your project directory:</span></span>

```sh
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a><span data-ttu-id="d8d61-144">Обновление генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8d61-144">Update yeoman generator for SharePoint</span></span>

<span data-ttu-id="d8d61-145">Если вы установили генератор Yeoman для SharePoint Framework глобально, вы можете проверить, нужно ли его обновлять, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d8d61-145">If you have installed the SharePoint Framework Yeoman generator globally, you can find out if it requires updating by running the following command:</span></span>

```sh
npm outdated -g
```

<span data-ttu-id="d8d61-p110">На основе версий, установленных на компьютере, и реестра npm будут выведены следующие сведения о глобально установленных на компьютере пакетах:</span><span class="sxs-lookup"><span data-stu-id="d8d61-p110">The command will list the following information about the packages installed globally in your machine. This information is looked up from the versions installed in your machine and the npm registry.</span></span>

* <span data-ttu-id="d8d61-148">текущая версия, глобально установленная на компьютере;</span><span class="sxs-lookup"><span data-stu-id="d8d61-148">Current version installed globally in your machine</span></span>
* <span data-ttu-id="d8d61-149">версия, которую вы запросили при установке;</span><span class="sxs-lookup"><span data-stu-id="d8d61-149">Version requested by you when you installed</span></span>
* <span data-ttu-id="d8d61-150">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="d8d61-150">Latest version available</span></span>

![Устаревшие глобальные пакеты NPM](../../images/npm-outdated-global-packages-list.png)

<span data-ttu-id="d8d61-152">Имя пакета генератора выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d8d61-152">To identify the generator package, look for the following package name:</span></span>

```sh
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a><span data-ttu-id="d8d61-153">Обновление пакета генератора</span><span class="sxs-lookup"><span data-stu-id="d8d61-153">Update generator package</span></span>

<span data-ttu-id="d8d61-154">Чтобы обновить генератор до последней опубликованной версии, откройте любую консоль и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d8d61-154">Open your favorite console and execute the following command to update the generator to its latest published version:</span></span>

```sh
npm install @microsoft/generator-sharepoint@latest -g
```

<span data-ttu-id="d8d61-155">Команда обновит генератор Yeoman для SharePoint и его зависимости до последней опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="d8d61-155">The command will update the yeoman generator for SharePoint to the latest published version along with its depedencies. You can validate this by executing the following command in the console:</span></span> <span data-ttu-id="d8d61-156">Для проверки выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d8d61-156">You can validate this by executing the following command in the console:</span></span>

```sh
npm ls @microsoft/generator-sharepoint -g --depth=0
```

## <a name="additional-resources"></a><span data-ttu-id="d8d61-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d8d61-157">Additional resources</span></span>

* [<span data-ttu-id="d8d61-158">Обновление проектов SharePoint Framework (руководство для команды разработчиков)</span><span class="sxs-lookup"><span data-stu-id="d8d61-158">Upgrading SharePoint Framework projects (Team-based development guidance)</span></span>](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/team-based-development-on-sharepoint-framework#upgrading-sharepoint-framework-projects)
* [<span data-ttu-id="d8d61-159">Обновление элементов SharePoint (Подготовка ресурсов SharePoint)</span><span class="sxs-lookup"><span data-stu-id="d8d61-159">Upgrade SharePoint items (Provisioning SharePoint assets)</span></span>](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/toolchain/provision-sharepoint-assets#upgrade-sharepoint-items)