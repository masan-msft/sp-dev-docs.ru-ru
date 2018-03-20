---
title: "Как настроить среду разработки SharePoint Framework"
description: "Создавайте решения SharePoint Framework, используя Visual Studio или собственную среду разработки. Можно использовать Mac, ПК с Windows или Linux."
ms.date: 03/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 9649955bf36bd821d1ff53fcef2a774050919b8c
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="set-up-your-sharepoint-framework-development-environment"></a><span data-ttu-id="29b5e-104">Как настроить среду разработки SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="29b5e-104">Set up your SharePoint Framework development environment</span></span>

<span data-ttu-id="29b5e-105">Для создания решений SharePoint Framework можно использовать Visual Studio или собственную среду разработки.</span><span class="sxs-lookup"><span data-stu-id="29b5e-105">You can use Visual Studio or your own custom development environment to build SharePoint Framework solutions.</span></span> <span data-ttu-id="29b5e-106">Можно использовать Mac, ПК с Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="29b5e-106">You can use a Mac, PC, or Linux.</span></span>

> [!NOTE] 
> <span data-ttu-id="29b5e-107">Прежде чем выполнять действия, описанные в этой статье, [настройте клиент Office 365](./set-up-your-developer-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="29b5e-107">Before following the steps in this article, be sure to [Set up your Office 365 tenant](./set-up-your-developer-tenant.md).</span></span>

<span data-ttu-id="29b5e-108">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span><span class="sxs-lookup"><span data-stu-id="29b5e-108">You can also follow these steps by watching this video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<span data-ttu-id="29b5e-109"><a href="https://www.youtube.com/watch?v=-tXf8gxjmOI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span><span class="sxs-lookup"><span data-stu-id="29b5e-109"><a href="https://www.youtube.com/watch?v=-tXf8gxjmOI&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span></span>

## <a name="install-developer-tools"></a><span data-ttu-id="29b5e-110">Установка средств разработчика</span><span class="sxs-lookup"><span data-stu-id="29b5e-110">Install developer tools</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="29b5e-111">Установка NodeJS</span><span class="sxs-lookup"><span data-stu-id="29b5e-111">Install NodeJS</span></span>

<span data-ttu-id="29b5e-112">Установка [LTS-версии NodeJS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="29b5e-112">Install [NodeJS LTS version](https://nodejs.org).</span></span> 

- <span data-ttu-id="29b5e-113">Если у вас Windows, используйте установщики msi для простой настройки NodeJS. Эти установщики можно скачать, перейдя по указанной выше ссылке.</span><span class="sxs-lookup"><span data-stu-id="29b5e-113">If you are in Windows, you can use the msi installers in this link for the easiest way to set up NodeJS.</span></span>
- <span data-ttu-id="29b5e-114">Если у вас уже установлена библиотека NodeJS, проверьте, последняя ли это версия, используя команду `node -v`.</span><span class="sxs-lookup"><span data-stu-id="29b5e-114">If you have NodeJS already installed, check that you have the latest version by using `node -v`.</span></span> <span data-ttu-id="29b5e-115">Она должна вернуть текущую [версию LTS](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="29b5e-115">It should return the current [LTS version](https://nodejs.org/en/download/).</span></span> 
- <span data-ttu-id="29b5e-116">Если у вас компьютер Mac, рекомендуем устанавливать платформу NodeJS и управлять ею с помощью [homebrew](http://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="29b5e-116">If you are using a Mac, we recommend that you use [homebrew](http://brew.sh/) to install and manage NodeJS.</span></span> 

> [!NOTE] 
> <span data-ttu-id="29b5e-117">Текущая LTS-версия NodeJS — 8.9.4.</span><span class="sxs-lookup"><span data-stu-id="29b5e-117">Current LTS version of NodeJS is 8.9.4.</span></span> <span data-ttu-id="29b5e-118">Обратите внимание на то, что версии 9.x сейчас не поддерживаются при разработке на платформе SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="29b5e-118">Notice that 9.x versions are currently not supported with SharePoint Framework development.</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="29b5e-119">Установка редактора кода</span><span class="sxs-lookup"><span data-stu-id="29b5e-119">Install a code editor</span></span>

<span data-ttu-id="29b5e-120">Для создания веб-частей можно использовать любой редактор кода или интерфейс IDE, поддерживающий клиентскую разработку, например:</span><span class="sxs-lookup"><span data-stu-id="29b5e-120">You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

- [<span data-ttu-id="29b5e-121">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="29b5e-121">Visual Studio Code</span></span>](https://code.visualstudio.com/)
- <span data-ttu-id="29b5e-122">[Atom](https://atom.io);</span><span class="sxs-lookup"><span data-stu-id="29b5e-122">[Atom](https://atom.io)</span></span>
- [<span data-ttu-id="29b5e-123">Webstorm</span><span class="sxs-lookup"><span data-stu-id="29b5e-123">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

<span data-ttu-id="29b5e-124">В указаниях и примерах в этой статье используется [Visual Studio Code](https://code.visualstudio.com/), но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="29b5e-124">The steps and examples in this documentation use [Visual Studio Code](https://code.visualstudio.com/), but you can use any editor of your choice.</span></span>

### <a name="if-you-are-using-ubuntu"></a><span data-ttu-id="29b5e-125">Если используется Ubuntu</span><span class="sxs-lookup"><span data-stu-id="29b5e-125">If you are using Ubuntu</span></span>

<span data-ttu-id="29b5e-126">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="29b5e-126">You need to install compiler tools by using the following command:</span></span>

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a><span data-ttu-id="29b5e-127">Если используется Fedora</span><span class="sxs-lookup"><span data-stu-id="29b5e-127">If you are using fedora</span></span>

<span data-ttu-id="29b5e-128">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="29b5e-128">You need to install compiler tools by using the following command:</span></span>

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a><span data-ttu-id="29b5e-129">Установка Yeoman и gulp</span><span class="sxs-lookup"><span data-stu-id="29b5e-129">Install Yeoman and gulp</span></span>

<span data-ttu-id="29b5e-130">[Yeoman](http://yeoman.io/) помогает запускать новые проекты, предоставляя рекомендации и инструменты, которые позволят сохранить эффективность работы.</span><span class="sxs-lookup"><span data-stu-id="29b5e-130">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="29b5e-131">Средства клиентской разработки SharePoint включают генератор Yeoman для создания веб-частей.</span><span class="sxs-lookup"><span data-stu-id="29b5e-131">SharePoint client-side development tools include a Yeoman generator for creating new web parts.</span></span> <span data-ttu-id="29b5e-132">Генератор предоставляет общие средства сборки, стандартный код и общий веб-сайт для тестирования веб-частей.</span><span class="sxs-lookup"><span data-stu-id="29b5e-132">The generator provides common build tools, common boilerplate code, and a common playground website to host web parts for testing.</span></span>

<span data-ttu-id="29b5e-133">Чтобы установить Yeoman и gulp, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="29b5e-133">Enter the following command to install Yeoman and gulp:</span></span>

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a><span data-ttu-id="29b5e-134">Установка генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="29b5e-134">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="29b5e-135">С помощью генератора веб-частей Yeoman для SharePoint можно быстро создать проект клиентского решения SharePoint с правильной цепочкой инструментов и структурой проекта.</span><span class="sxs-lookup"><span data-stu-id="29b5e-135">The Yeoman SharePoint web part generator helps you quickly create a SharePoint client-side solution project with the right toolchain and project structure.</span></span>

<span data-ttu-id="29b5e-136">Чтобы глобально установить генератор Yeoman для SharePoint Framework, введите такую команду:</span><span class="sxs-lookup"><span data-stu-id="29b5e-136">To install the SharePoint Framework Yeoman generator globally, enter the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint
```

<span data-ttu-id="29b5e-137">Чтобы можно было переходить между различными проектами, созданными с помощью разных версий генератора Yeoman для SharePoint, установите генератор локально как зависимость разработки в папке проекта с помощью такой команды:</span><span class="sxs-lookup"><span data-stu-id="29b5e-137">If you need to switch between the different projects created by using different versions of the SharePoint Framework Yeoman generator, you can install the generator locally as a development dependency in the project folder by executing the following command:</span></span>

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

<span data-ttu-id="29b5e-138">Дополнительные сведения о генераторе Yeoman SharePoint см. в статье [Скаффолдинг проектов с помощью генератора Yeoman SharePoint](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md).</span><span class="sxs-lookup"><span data-stu-id="29b5e-138">For more information about the Yeoman SharePoint generator, see [Scaffold projects by using Yeoman SharePoint generator](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md).</span></span>

## <a name="optional-tools"></a><span data-ttu-id="29b5e-139">Дополнительные средства</span><span class="sxs-lookup"><span data-stu-id="29b5e-139">Optional tools</span></span>

<span data-ttu-id="29b5e-140">Вам также могут пригодиться следующие средства:</span><span class="sxs-lookup"><span data-stu-id="29b5e-140">Following are some tools that might come in handy as well:</span></span>

* <span data-ttu-id="29b5e-141">[Fiddler](https://www.telerik.com/fiddler);</span><span class="sxs-lookup"><span data-stu-id="29b5e-141">[Fiddler](https://www.telerik.com/fiddler)</span></span>
* <span data-ttu-id="29b5e-142">[подключаемый модуль Postman для Chrome](https://www.getpostman.com/docs/postman/launching_postman/navigating_postman);</span><span class="sxs-lookup"><span data-stu-id="29b5e-142">[Postman plug-in for Chrome](https://www.getpostman.com/docs/postman/launching_postman/navigating_postman)</span></span>
* <span data-ttu-id="29b5e-143">[Cmder для Windows](http://cmder.net/);</span><span class="sxs-lookup"><span data-stu-id="29b5e-143">[Cmder for Windows](http://cmder.net/)</span></span>
* <span data-ttu-id="29b5e-144">[Oh My Zsh для Mac](http://ohmyz.sh/);</span><span class="sxs-lookup"><span data-stu-id="29b5e-144">[Oh My Zsh for Mac](http://ohmyz.sh/)</span></span>
* <span data-ttu-id="29b5e-145">[службы управления версиями Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="29b5e-145">[Git source control tools](https://git-scm.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="29b5e-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29b5e-146">Next steps</span></span>

<span data-ttu-id="29b5e-147">Теперь вы готовы [создать свою первую клиентскую веб-часть](web-parts/get-started/build-a-hello-world-web-part.md)!</span><span class="sxs-lookup"><span data-stu-id="29b5e-147">You are now ready to [build your first client-side web part](web-parts/get-started/build-a-hello-world-web-part.md)!</span></span>

> [!NOTE]
> <span data-ttu-id="29b5e-148">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="29b5e-148">If you find an issue in the documentation or in the SharePoint Framework, report that to SharePoint engineering by using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="29b5e-149">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="29b5e-149">Thanks for your input in advance.</span></span>