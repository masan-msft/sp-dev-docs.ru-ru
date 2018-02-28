---
title: "Обновление пакетов SharePoint Framework"
description: "Обновите пакеты npm, которые вы установили в своем проекте или глобально."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 75503d4c67949f28a53940123c5b51bacb67b2ee
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="update-sharepoint-framework-packages"></a><span data-ttu-id="598ee-103">Обновление пакетов SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="598ee-103">Update SharePoint Framework packages</span></span>

<span data-ttu-id="598ee-104">Средства клиентской разработки для SharePoint управляют зависимостями и другими необходимыми вспомогательными элементами JavaScript с помощью диспетчера пакетов [npm](https://www.npmjs.com/).</span><span class="sxs-lookup"><span data-stu-id="598ee-104">SharePoint client-side development tools use the [npm](https://www.npmjs.com/) package manager to manage dependencies and other required JavaScript helpers.</span></span> <span data-ttu-id="598ee-105">Этот диспетчер обычно устанавливается вместе с Node.js.</span><span class="sxs-lookup"><span data-stu-id="598ee-105">npm is typically included as part of Node.js setup.</span></span>

<span data-ttu-id="598ee-106">Когда вы создаете новое клиентское решение, генератор Yeoman для SharePoint получает последние версии необходимых для проекта пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="598ee-106">When you create a new client-side solution, the yeoman generator for SharePoint fetches the latest SharePoint Framework packages required for your client-side project.</span></span> <span data-ttu-id="598ee-107">По мере работы над проектом пакеты могут устаревать.</span><span class="sxs-lookup"><span data-stu-id="598ee-107">As you build your project, your existing packages could be outdated as there could be new versions of one or more packages available.</span></span> 

<span data-ttu-id="598ee-108">Изучив [заметки о выпуске](https://aka.ms/spfx-release-notes), касающиеся определенного выпуска или последней версии пакета, вы можете решить обновить пакеты SharePoint Framework, используемые в проекте.</span><span class="sxs-lookup"><span data-stu-id="598ee-108">Based on the [release notes](https://aka.ms/spfx-release-notes) for a particular release or the latest package, you may decide to update your SharePoint Framework packages used in your project.</span></span> <span data-ttu-id="598ee-109">Пакеты SharePoint Framework включают установленные в проекте пакеты npm, например [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), и глобально установленные пакеты npm, например [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="598ee-109">SharePoint Framework packages include both the npm packages you have installed in your project, for example: [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), and npm packages installed globally, for example: [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint).</span></span> 

> [!TIP]
> <span data-ttu-id="598ee-110">Рекомендуем время от времени обновлять пакеты SharePoint Framework, чтобы получать доступ к последним изменениям и исправлениям.</span><span class="sxs-lookup"><span data-stu-id="598ee-110">While it may not be required, it is recommended you update the SharePoint Framework packages every so often so that you can get the latest changes and fixes that have been released.</span></span>

## <a name="find-outdated-packages"></a><span data-ttu-id="598ee-111">Поиск устаревших пакетов</span><span class="sxs-lookup"><span data-stu-id="598ee-111">Find outdated packages in your project</span></span>

<span data-ttu-id="598ee-112">Чтобы найти устаревшие пакеты, в том числе пакеты SharePoint Framework и другие пакеты, от которых зависит проект, перейдите в каталог проекта и выполните в нем следующую команду.</span><span class="sxs-lookup"><span data-stu-id="598ee-112">To find the outdated packages in your client-side project, including SharePoint Framework and other packages your project depends on, run the following command in a console in the same directory as your project.</span></span> 

```sh
npm outdated
```

<span data-ttu-id="598ee-113">На основе файла</span><span class="sxs-lookup"><span data-stu-id="598ee-113">The command will list the following information about the packages your project depends on.</span></span> <span data-ttu-id="598ee-114">`package.json`, расположенного в корневом каталоге проекта, и реестра npm выводятся следующие сведения о пакетах:</span><span class="sxs-lookup"><span data-stu-id="598ee-114">This information is looked up from the `package.json` file located in the root of your project directory and npm registry.</span></span>

* <span data-ttu-id="598ee-115">версия, установленная в проекте;</span><span class="sxs-lookup"><span data-stu-id="598ee-115">Current version installed in your project</span></span>
* <span data-ttu-id="598ee-116">версия, запрашиваемая проектом (указана в файле `package.json`);</span><span class="sxs-lookup"><span data-stu-id="598ee-116">Version requested by your project (available in `package.json`)</span></span>
* <span data-ttu-id="598ee-117">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="598ee-117">Latest version available</span></span>

![Устаревшие пакеты NPM](../../images/npm-outdated-packages-list.png)

<span data-ttu-id="598ee-119">Имена пакетов SharePoint Framework начинаются с такого идентификатора области npm и префикса:</span><span class="sxs-lookup"><span data-stu-id="598ee-119">To identify the SharePoint Framework packages, look for the package names that start with the following npm scope and prefix:</span></span>

```text
@microsoft/sp-
```

<span data-ttu-id="598ee-120">Помимо пакетов Framework вам также может понадобиться обновить пакеты `react` и `office-ui-fabric-react`.</span><span class="sxs-lookup"><span data-stu-id="598ee-120">Along with the framework packages, you may also need to update `react` and `office-ui-fabric-react` packages.</span></span> <span data-ttu-id="598ee-121">Обязательно ознакомьтесь с [заметками о выпуске](https://aka.ms/spfx-release-notes), чтобы определить, какие пакеты нужно обновить, и запланируйте обновление.</span><span class="sxs-lookup"><span data-stu-id="598ee-121">Make sure you read the [release notes](https://aka.ms/spfx-release-notes) for that specific release to infer which packages require updates and plan accordingly.</span></span>

### <a name="using-the-npm-outdated-command-with-a-project"></a><span data-ttu-id="598ee-122">Использование команды "npm outdated" в проекте</span><span class="sxs-lookup"><span data-stu-id="598ee-122">Using the "npm outdated" command with a project</span></span>

<span data-ttu-id="598ee-123">SharePoint 2016 с пакетом дополнительных компонентов 2 уже поддерживает решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="598ee-123">Starting from Feature Pack 2, SharePoint 2016 supports SharePoint Framework solutions.</span></span> <span data-ttu-id="598ee-124">SharePoint 2016 использует более старую версию SharePoint Framework, чем SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="598ee-124">SharePoint 2016 uses an older version of the SharePoint Framework, than the version available in SharePoint Online.</span></span> 

<span data-ttu-id="598ee-125">Формируя шаблон проекта, генератор Yeoman для SharePoint Framework предлагает выбрать, какую версию должно использовать решение. Если оно будет использовать последнюю версию SharePoint Framework, оно будет работать только в SharePoint Online, если более старую — оно будет работать в SharePoint 2016 и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="598ee-125">When scaffolding new projects, the SharePoint Framework Yeoman generator prompts you to choose if your solution should be using the latest version of the SharePoint Framework and be working only with SharePoint Online or if it should use an older version of the SharePoint Framework and work with both SharePoint 2016 and SharePoint Online.</span></span>

<span data-ttu-id="598ee-126">Команда `npm outdated`, выполняемая в проекте для SharePoint Online и SharePoint 2016, показывает последние версии пакетов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="598ee-126">When you run the `npm outdated` command in a project targeting both SharePoint Online and SharePoint 2016, it will show you the latest versions of the SharePoint Framework packages.</span></span> <span data-ttu-id="598ee-127">Эти версии работают только в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="598ee-127">These versions however work only with SharePoint Online.</span></span> <span data-ttu-id="598ee-128">Если вы обновите пакеты в своем решении, оно перестанет работать в SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="598ee-128">If you would update your solution to use these latest packages, it would not work with SharePoint 2016 anymore.</span></span>

<span data-ttu-id="598ee-129">Работая с решениями SharePoint Framework, совместимыми с локальной средой SharePoint, всегда проверяйте, какой уровень исправления у целевой фермы SharePoint и какую версию SharePoint Framework она поддерживает.</span><span class="sxs-lookup"><span data-stu-id="598ee-129">When working with SharePoint Framework solutions compatible with SharePoint hosted on-premises, you should always verify which patch level the target SharePoint farm has and which version of the SharePoint Framework it supports.</span></span>

## <a name="update-packages"></a><span data-ttu-id="598ee-130">Обновление пакетов</span><span class="sxs-lookup"><span data-stu-id="598ee-130">Update packages</span></span>

<span data-ttu-id="598ee-131">При обновлении версий пакетов всегда используйте диспетчер пакетов (npm или Yarn).</span><span class="sxs-lookup"><span data-stu-id="598ee-131">When updating packages to newer versions, you should always use your package manager (npm or Yarn).</span></span> <span data-ttu-id="598ee-132">Не следует редактировать файл `package.json` вручную.</span><span class="sxs-lookup"><span data-stu-id="598ee-132">You should not edit the `package.json` file manually.</span></span> <span data-ttu-id="598ee-133">Если вы будете следовать рекомендациям по использованию файла блокировки, изменения, внесенные в файл `package.json`, будут проигнорированы.</span><span class="sxs-lookup"><span data-stu-id="598ee-133">If you follow the recommended practice of using a lock file, your changes to the `package.json` file would be ignored.</span></span>

<span data-ttu-id="598ee-134">Начните с определения того, какие пакеты нужно обновить и какие новые версии хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="598ee-134">Start with identifying which packages need updating and which newer version you want to use.</span></span> <span data-ttu-id="598ee-135">Обратите внимание, что не всегда можно использовать последнюю версию определенного пакета, так как она может быть несовместима с другими зависимостями SharePoint Framework, такими как TypeScript.</span><span class="sxs-lookup"><span data-stu-id="598ee-135">Please note, that it might not always be possible for you to use the latest version of the given package as it might be incompatible with other SharePoint Framework dependencies, such as TypeScript.</span></span>

<span data-ttu-id="598ee-136">Для каждого пакета, который нужно обновить, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="598ee-136">For each package that you want to update, run the following command:</span></span>

```sh
npm install mypackage@newversion --save
```

<span data-ttu-id="598ee-137">Например, если вы используете AngularJS версии 1.5.9 и хотите выполнить обновление до версии 1.6.5, нужно выполнить такую команду:</span><span class="sxs-lookup"><span data-stu-id="598ee-137">For example, if you were using AngularJS version v1.5.9 and wanted to update to version 1.6.5, you would run:</span></span>

```sh
npm install angular@1.6.5 --save
```

<span data-ttu-id="598ee-138">При обновлении пакета с помощью npm устанавливается указанная версия пакета, а также обновляется номер версии в зависимостях файла package.json и файл блокировки, используемый в проекте.</span><span class="sxs-lookup"><span data-stu-id="598ee-138">Updating the package using npm will install the specified version of the package in your project, update the version number in the package.json file dependencies and the lock file used in your project.</span></span>

<span data-ttu-id="598ee-139">После установки пакетов выполните следующую команду, чтобы удалить артефакты старой сборки:</span><span class="sxs-lookup"><span data-stu-id="598ee-139">Once the packages are installed, execute the following command to clean up any old build artifacts:</span></span>

```sh
gulp clean
```

## <a name="update-your-code"></a><span data-ttu-id="598ee-140">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="598ee-140">Update your code</span></span>

<span data-ttu-id="598ee-141">В зависимости от того, насколько существенно изменен API, может потребоваться обновить существующий код и файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="598ee-141">Depending on breaking API changes, you may have to update your existing project code and config files.</span></span> <span data-ttu-id="598ee-142">О существенных изменениях и модификациях, которые нужно внести в существующий код, можно узнать из [заметок о выпуске](https://aka.ms/spfx-release-notes).</span><span class="sxs-lookup"><span data-stu-id="598ee-142">For each release, the [release notes](https://aka.ms/spfx-release-notes) will highlight any such breaking changes and the modifications required to your existing code.</span></span> <span data-ttu-id="598ee-143">Внесите необходимые исправления в код.</span><span class="sxs-lookup"><span data-stu-id="598ee-143">You will need to make sure you update your code with those fixes.</span></span>

<span data-ttu-id="598ee-144">Вы всегда можете выполнить сборку проекта, чтобы посмотреть, есть ли ошибки и предупреждения, выполнив команду в консоли в каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="598ee-144">You can always build the project to see if you have any errors and warnings by running the command in a console in your project directory:</span></span>

```sh
gulp build
```

## <a name="update-yeoman-generator"></a><span data-ttu-id="598ee-145">Обновление генератора Yeoman</span><span class="sxs-lookup"><span data-stu-id="598ee-145">Update Yeoman generator</span></span>

<span data-ttu-id="598ee-146">Если вы установили генератор Yeoman для SharePoint Framework глобально, вы можете проверить, нужно ли его обновлять, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="598ee-146">If you have installed the SharePoint Framework Yeoman generator globally, you can find out if it requires updating by running the following command:</span></span>

```sh
npm outdated -g
```

<span data-ttu-id="598ee-147">На основе версий, установленных на компьютере,</span><span class="sxs-lookup"><span data-stu-id="598ee-147">The command lists the following information about the packages installed globally on your machine.</span></span> <span data-ttu-id="598ee-148">и реестра npm выводятся следующие сведения о глобально установленных на компьютере пакетах:</span><span class="sxs-lookup"><span data-stu-id="598ee-148">The command will list the following information about the packages installed globally in your machine. This information is looked up from the versions installed in your machine and the npm registry.</span></span>

* <span data-ttu-id="598ee-149">текущая версия, глобально установленная на компьютере;</span><span class="sxs-lookup"><span data-stu-id="598ee-149">Current version installed globally in your machine</span></span>
* <span data-ttu-id="598ee-150">версия, которую вы запросили при установке;</span><span class="sxs-lookup"><span data-stu-id="598ee-150">Version requested by you when you installed</span></span>
* <span data-ttu-id="598ee-151">последняя доступная версия.</span><span class="sxs-lookup"><span data-stu-id="598ee-151">Latest version available</span></span>

![Устаревшие глобальные пакеты NPM](../../images/npm-outdated-global-packages-list.png)

<span data-ttu-id="598ee-153">Имя пакета генератора выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="598ee-153">To identify the generator package, look for the following package name:</span></span>

```sh
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a><span data-ttu-id="598ee-154">Обновление пакета генератора</span><span class="sxs-lookup"><span data-stu-id="598ee-154">Update generator package</span></span>

<span data-ttu-id="598ee-155">Чтобы обновить генератор до последней опубликованной версии, откройте любую консоль и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="598ee-155">Open your favorite console and execute the following command to update the generator to its latest published version:</span></span>

```sh
npm install @microsoft/generator-sharepoint@latest -g
```

<span data-ttu-id="598ee-156">Команда обновляет генератор Yeoman для SharePoint и его зависимости до последней опубликованной версии.</span><span class="sxs-lookup"><span data-stu-id="598ee-156">The command will update the yeoman generator for SharePoint to the latest published version along with its dependencies.</span></span> <span data-ttu-id="598ee-157">Для проверки выполните в консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="598ee-157">You can validate this by executing the following command in the console:</span></span>

```sh
npm ls @microsoft/generator-sharepoint -g --depth=0
```

## <a name="see-also"></a><span data-ttu-id="598ee-158">См. также</span><span class="sxs-lookup"><span data-stu-id="598ee-158">See also</span></span>

- [<span data-ttu-id="598ee-159">Обновление проектов SharePoint Framework (руководство для команды разработчиков)</span><span class="sxs-lookup"><span data-stu-id="598ee-159">Upgrading SharePoint Framework projects (Team-based development guidance)</span></span>](../team-based-development-on-sharepoint-framework.md#upgrading-sharepoint-framework-projects)
- [<span data-ttu-id="598ee-160">Обновление элементов SharePoint (Подготовка ресурсов SharePoint)</span><span class="sxs-lookup"><span data-stu-id="598ee-160">Upgrade SharePoint items (Provisioning SharePoint assets)</span></span>](provision-sharepoint-assets.md#upgrade-sharepoint-items)
- [<span data-ttu-id="598ee-161">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="598ee-161">SharePoint Framework Overview</span></span>](../sharepoint-framework-overview.md)