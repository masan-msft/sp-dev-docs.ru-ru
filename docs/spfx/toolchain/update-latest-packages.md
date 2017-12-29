---
title: "Обновление пакетов SharePoint Framework"
ms.date: 11/29/2017
ms.prod: sharepoint
ms.openlocfilehash: 665c22ffea27a8b62d433cfb4932625664638e0a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="update-sharepoint-framework-packages"></a><span data-ttu-id="b801d-102">Обновление пакетов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b801d-102">Update SharePoint Framework packages</span></span>

<span data-ttu-id="b801d-103">Средства клиентской разработки для SharePoint управляют зависимостями и другими необходимыми вспомогательными элементами JavaScript с помощью диспетчера пакетов [npm](https://www.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="b801d-103">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager to manage dependencies and other required JavaScript helpers.</span></span> <span data-ttu-id="b801d-104">Этот диспетчер обычно устанавливается вместе с Node.js.</span><span class="sxs-lookup"><span data-stu-id="b801d-104">npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="b801d-105">При создании нового клиентского решения генератор Yeoman для SharePoint получает последние версии необходимых для проекта пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b801d-105">When you create a new client-side solution, the yeoman generator for SharePoint fetches the latest SharePoint Framework packages required for your client-side project.</span></span> <span data-ttu-id="b801d-106">По мере работы над проектом пакеты могут устаревать.</span><span class="sxs-lookup"><span data-stu-id="b801d-106">As you build your project, your existing packages could be outdated as there could be new versions of one or more packages available.</span></span> <span data-ttu-id="b801d-107">Изучив [заметки о выпуске](https://aka.ms/spfx-release-notes), касающиеся определенного выпуска или последней версии пакета, вы можете решить обновить пакеты SharePoint Framework, используемые в проекте.</span><span class="sxs-lookup"><span data-stu-id="b801d-107">Based on the [release notes](https://aka.ms/spfx-release-notes) for a particular release or the latest package, you may decide to update your SharePoint Framework packages used in your project.</span></span> <span data-ttu-id="b801d-108">Пакеты SharePoint Framework включают установленные в проекте пакеты npm, например [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), и глобально установленные пакеты npm, например [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="b801d-108">SharePoint Framework packages include both the npm packages you have installed in your project, for example: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), and npm packages installed globally, for example: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span></span> 

> [!TIP]
> <span data-ttu-id="b801d-109">Рекомендуем время от времени обновлять пакеты SharePoint Framework, чтобы получать доступ к последним изменениям и исправлениям.</span><span class="sxs-lookup"><span data-stu-id="b801d-109">While it may not be required, it is recommended you update the SharePoint Framework packages every so often so that you can get the latest changes and fixes that have been released.</span></span>

## <a name="find-outdated-packages-in-your-project"></a><span data-ttu-id="b801d-110">Поиск устаревших пакетов в проекте</span><span class="sxs-lookup"><span data-stu-id="b801d-110">Find outdated packages in your project</span></span>

<span data-ttu-id="b801d-111">Чтобы найти устаревшие пакеты, в том числе пакеты SharePoint Framework и другие пакеты, от которых зависит проект, перейдите в каталог проекта и выполните в нем следующую команду.</span><span class="sxs-lookup"><span data-stu-id="b801d-111">To find the outdated packages in your client-side project, including SharePoint Framework and other packages your project depends on, run the following command in a console in the same directory as your project.</span></span> 

```sh
npm outdated
```

<span data-ttu-id="b801d-112">На основе файла</span><span class="sxs-lookup"><span data-stu-id="b801d-112">The command will list the following information about the packages your project depends on.</span></span> <span data-ttu-id="b801d-113">`package.json`, расположенного в корневом каталоге проекта, и реестра npm будут выведены следующие сведения о пакетах:</span><span class="sxs-lookup"><span data-stu-id="b801d-113">This information is looked up from the `package.json` file located in the root of your project directory and npm registry.</span></span>

* <span data-ttu-id="b801d-114">версия, установленная в проекте;</span><span class="sxs-lookup"><span data-stu-id="b801d-114">Current version installed in your project</span></span>
* <span data-ttu-id="b801d-115">версия, запрашиваемая проектом (указана в файле `package.json`);</span><span class="sxs-lookup"><span data-stu-id="b801d-115">Version requested by your project (available in `package.json`)</span></span>
* <span data-ttu-id="b801d-116">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="b801d-116">Latest version available</span></span>

![Устаревшие пакеты NPM](../../images/npm-outdated-packages-list.png)

<span data-ttu-id="b801d-118">Имена пакетов SharePoint Framework начинаются с такого идентификатора области npm и префикса:</span><span class="sxs-lookup"><span data-stu-id="b801d-118">To identify the SharePoint Framework packages, look for the package names that start with the following npm scope and prefix:</span></span>

```text
@microsoft/sp-
```

<span data-ttu-id="b801d-119">Помимо пакетов Framework вам также может понадобиться обновить пакеты `react` и `office-ui-fabric-react`.</span><span class="sxs-lookup"><span data-stu-id="b801d-119">Along with the framework packages, you may also need to update `react` and `office-ui-fabric-react` packages.</span></span> <span data-ttu-id="b801d-120">Обязательно ознакомьтесь с [заметками о конкретном выпуске](https://aka.ms/spfx-release-notes), чтобы определить, какие пакеты нужно обновить, и запланируйте обновление.</span><span class="sxs-lookup"><span data-stu-id="b801d-120">Make sure you read the [release notes](https://aka.ms/spfx-release-notes) for that specific release to infer which packages require updates and plan accordingly.</span></span>

### <a name="using-npm-outdated-with-project-targeting-sharepoint-2016"></a><span data-ttu-id="b801d-121">Использование npm предыдущей версии в проекте для SharePoint 2016</span><span class="sxs-lookup"><span data-stu-id="b801d-121">Using npm outdated with project targeting SharePoint 2016</span></span>

<span data-ttu-id="b801d-122">Начиная с пакета дополнительных компонентов 2, SharePoint 2016 поддерживает решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b801d-122">Starting from Feature Pack 2, SharePoint 2016 supports SharePoint Framework solutions.</span></span> <span data-ttu-id="b801d-123">SharePoint 2016 использует версию SharePoint Framework, выпущенную раньше той, которая доступна в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b801d-123">SharePoint 2016 uses an older version of the SharePoint Framework, than the version available in SharePoint Online.</span></span> <span data-ttu-id="b801d-124">При скаффолдинге новых проектов генератор Yeoman для SharePoint Framework предложит указать, какую версию должно использовать решение. Если оно будет использовать последнюю версию SharePoint Framework, оно будет работать только в SharePoint Online, если более старую — оно будет работать в SharePoint 2016 и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b801d-124">When scaffolding new projects, the SharePoint Framework Yeoman generator prompts you to choose if your solution should be using the latest version of the SharePoint Framework and be working only with SharePoint Online or if it should use an older version of the SharePoint Framework and work with both SharePoint 2016 and SharePoint Online.</span></span>

<span data-ttu-id="b801d-125">Когда вы выполните команду `npm outdated` в проекте для SharePoint Online и SharePoint 2016, отобразятся последние версии пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b801d-125">When you run the `npm outdated` command in a project targeting both SharePoint Online and SharePoint 2016, it will show you the latest versions of the SharePoint Framework packages.</span></span> <span data-ttu-id="b801d-126">Эти версии работают только в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="b801d-126">These versions however work only with SharePoint Online.</span></span> <span data-ttu-id="b801d-127">Если вы обновите свое решение так, чтобы оно использовало эти последние пакеты, оно перестанет работать в SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="b801d-127">If you would update your solution to use these latest packages, it would not work with SharePoint 2016 anymore.</span></span>

<span data-ttu-id="b801d-128">Работая с решениями SharePoint Framework, совместимыми с локальной средой SharePoint, всегда проверяйте, какой уровень исправления у целевой фермы SharePoint и какую версию SharePoint Framework она поддерживает.</span><span class="sxs-lookup"><span data-stu-id="b801d-128">When working with SharePoint Framework solutions compatible with SharePoint hosted on-premises, you should always verify which patch level the target SharePoint farm has and which version of the SharePoint Framework it supports.</span></span>

### <a name="update-packages"></a><span data-ttu-id="b801d-129">Обновление пакетов</span><span class="sxs-lookup"><span data-stu-id="b801d-129">Update packages</span></span>

<span data-ttu-id="b801d-130">При обновлении версий пакетов всегда используйте диспетчер пакетов (npm или Yarn).</span><span class="sxs-lookup"><span data-stu-id="b801d-130">When updating packages to newer versions, you should always use your package manager (npm or Yarn).</span></span> <span data-ttu-id="b801d-131">Не следует редактировать файл `package.json` вручную.</span><span class="sxs-lookup"><span data-stu-id="b801d-131">You should not edit the `package.json` file manually.</span></span> <span data-ttu-id="b801d-132">Если вы будете следовать рекомендациям по использованию файла блокировки, изменения, внесенные в файл `package.json`, будут проигнорированы.</span><span class="sxs-lookup"><span data-stu-id="b801d-132">If you follow the recommended practice of using a lock file, your changes to the `package.json` file would be ignored.</span></span>

<span data-ttu-id="b801d-133">Начните с определения того, какие пакеты нужно обновить и какие новые версии хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="b801d-133">Start with identifying which packages need updating and which newer version you want to use.</span></span> <span data-ttu-id="b801d-134">Обратите внимание на то, что не всегда возможно использовать последнюю версию определенного пакета, так как она может быть несовместима с другими зависимостями SharePoint Framework, такими как TypeScript.</span><span class="sxs-lookup"><span data-stu-id="b801d-134">Please note, that it might not always be possible for you to use the latest version of the given package as it might be incompatible with other SharePoint Framework dependencies, such as TypeScript.</span></span>

<span data-ttu-id="b801d-135">Для каждого пакета, который нужно обновить, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b801d-135">For each package that you want to update, run the following command:</span></span>

```sh
npm install mypackage@newversion --save
```

<span data-ttu-id="b801d-136">Например, если вы используете AngularJS версии 1.5.9 и хотите выполнить обновление до версии 1.6.5, нужно выполнить такую команду:</span><span class="sxs-lookup"><span data-stu-id="b801d-136">For example, if you were using AngularJS version v1.5.9 and wanted to update to version 1.6.5, you would run:</span></span>

```sh
npm install angular@1.6.5 --save
```

<span data-ttu-id="b801d-137">При обновлении пакета с помощью npm установится указанная версия пакета в проекте, а также обновится номер версии в зависимостях файла package.json и файл блокировки, используемый в проекте.</span><span class="sxs-lookup"><span data-stu-id="b801d-137">Updating the package using npm will install the specified version of the package in your project, update the version number in the package.json file dependencies and the lock file used in your project.</span></span>

<span data-ttu-id="b801d-138">После установки пакетов выполните следующую команду, чтобы очистить артефакты старой сборки:</span><span class="sxs-lookup"><span data-stu-id="b801d-138">Once the packages are installed, execute the following command to clean up any old build artifacts:</span></span>

```sh
gulp clean
```

### <a name="update-your-code"></a><span data-ttu-id="b801d-139">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="b801d-139">Update your code</span></span>

<span data-ttu-id="b801d-140">В зависимости от того, насколько существенно изменен API, может потребоваться обновить существующий код и файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="b801d-140">Depending on breaking API changes, you may have to update your existing project code and config files.</span></span> <span data-ttu-id="b801d-141">О существенных изменениях и модификациях, которые нужно внести в существующий код, можно узнать из [заметок о выпуске](https://aka.ms/spfx-release-notes).</span><span class="sxs-lookup"><span data-stu-id="b801d-141">For each release, the [release notes](https://aka.ms/spfx-release-notes) will highlight any such breaking changes and the modifications required to your existing code.</span></span> <span data-ttu-id="b801d-142">Внесите необходимые исправления в код.</span><span class="sxs-lookup"><span data-stu-id="b801d-142">You will need to make sure you update your code with those fixes.</span></span>

<span data-ttu-id="b801d-143">Вы всегда можете выполнить сборку проекта, чтобы посмотреть, есть ли ошибки и предупреждения, выполнив команду в консоли в каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="b801d-143">You can always build the project to see if you have any errors and warnings by running the command in a console in your project directory:</span></span>

```sh
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a><span data-ttu-id="b801d-144">Обновление генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b801d-144">Update yeoman generator for SharePoint</span></span>

<span data-ttu-id="b801d-145">Если вы установили генератор Yeoman для SharePoint Framework глобально, вы можете проверить, нужно ли его обновлять, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b801d-145">If you have installed the SharePoint Framework Yeoman generator globally, you can find out if it requires updating by running the following command:</span></span>

```sh
npm outdated -g
```

<span data-ttu-id="b801d-p110">На основе версий, установленных на компьютере, и реестра npm будут выведены следующие сведения о глобально установленных на компьютере пакетах:</span><span class="sxs-lookup"><span data-stu-id="b801d-p110">The command will list the following information about the packages installed globally in your machine. This information is looked up from the versions installed in your machine and the npm registry.</span></span>

* <span data-ttu-id="b801d-148">текущая версия, глобально установленная на компьютере;</span><span class="sxs-lookup"><span data-stu-id="b801d-148">Current version installed globally in your machine</span></span>
* <span data-ttu-id="b801d-149">версия, которую вы запросили при установке;</span><span class="sxs-lookup"><span data-stu-id="b801d-149">Version requested by you when you installed</span></span>
* <span data-ttu-id="b801d-150">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="b801d-150">Latest version available</span></span>

![Устаревшие глобальные пакеты NPM](../../images/npm-outdated-global-packages-list.png)

<span data-ttu-id="b801d-152">Имя пакета генератора выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b801d-152">To identify the generator package, look for the following package name:</span></span>

```sh
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a><span data-ttu-id="b801d-153">Обновление пакета генератора</span><span class="sxs-lookup"><span data-stu-id="b801d-153">Update generator package</span></span>

<span data-ttu-id="b801d-154">Чтобы обновить генератор до последней опубликованной версии, откройте любую консоль и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b801d-154">Open your favorite console and execute the following command to update the generator to its latest published version:</span></span>

```sh
npm install @microsoft/generator-sharepoint@latest -g
```

<span data-ttu-id="b801d-155">Команда обновит генератор Yeoman для SharePoint и его зависимости до последней опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="b801d-155">The command will update the yeoman generator for SharePoint to the latest published version along with its depedencies. You can validate this by executing the following command in the console:</span></span> <span data-ttu-id="b801d-156">Для проверки выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b801d-156">You can validate this by executing the following command in the console:</span></span>

```sh
npm ls @microsoft/generator-sharepoint -g --depth=0
```

## <a name="see-also"></a><span data-ttu-id="b801d-157">См. также</span><span class="sxs-lookup"><span data-stu-id="b801d-157">See also</span></span>

* [<span data-ttu-id="b801d-158">Обновление проектов SharePoint Framework (руководство для команды разработчиков)</span><span class="sxs-lookup"><span data-stu-id="b801d-158">Upgrading SharePoint Framework projects (Team-based development guidance)</span></span>](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/team-based-development-on-sharepoint-framework#upgrading-sharepoint-framework-projects)
* [<span data-ttu-id="b801d-159">Обновление элементов SharePoint (Подготовка ресурсов SharePoint)</span><span class="sxs-lookup"><span data-stu-id="b801d-159">Upgrade SharePoint items (Provisioning SharePoint assets)</span></span>](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/toolchain/provision-sharepoint-assets#upgrade-sharepoint-items)