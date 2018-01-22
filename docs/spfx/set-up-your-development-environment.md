---
title: "Как настроить среду разработки SharePoint Framework"
description: "Создавайте решения SharePoint Framework, используя Visual Studio или собственную среду разработки. Можно использовать Mac, ПК с Windows или Linux."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 0c849ef4ad13962ecb4e3cfd8dc34aec0baab523
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="set-up-your-sharepoint-framework-development-environment"></a><span data-ttu-id="b6be0-104">Как настроить среду разработки SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b6be0-104">Set up your SharePoint Framework development environment</span></span>

<span data-ttu-id="b6be0-105">Для создания решений SharePoint Framework можно использовать Visual Studio или собственную среду разработки.</span><span class="sxs-lookup"><span data-stu-id="b6be0-105">You can use Visual Studio, or your own custom development environment to build SharePoint Framework solutions. You can use a Mac, PC, or Linux.</span></span> <span data-ttu-id="b6be0-106">Можно использовать Mac, ПК с Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="b6be0-106">You can use a Mac, PC, or Linux.</span></span>

> [!NOTE] 
> <span data-ttu-id="b6be0-107">Прежде чем выполнять действия, описанные в этой статье, [настройте клиент Office 365](./set-up-your-developer-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b6be0-107">Note: Before following the steps in this article, be sure to [Set up your Office 365 Tenant](./set-up-your-developer-tenant.md).</span></span>

<span data-ttu-id="b6be0-108">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span><span class="sxs-lookup"><span data-stu-id="b6be0-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<span data-ttu-id="b6be0-109"><a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span><span class="sxs-lookup"><span data-stu-id="b6be0-109"></span></span>

## <a name="install-developer-tools"></a><span data-ttu-id="b6be0-110">Установка средств разработчика</span><span class="sxs-lookup"><span data-stu-id="b6be0-110">Install developer tools</span></span>

### <a name="install-nodejs"></a><span data-ttu-id="b6be0-111">Установка NodeJS</span><span class="sxs-lookup"><span data-stu-id="b6be0-111">Install Node.js.</span></span>

<span data-ttu-id="b6be0-112">Установка [NodeJS версии 6.x](https://nodejs.org/download/release/latest-v6.x/).</span><span class="sxs-lookup"><span data-stu-id="b6be0-112">Install [NodeJS version 6.x](https://nodejs.org/download/release/latest-v6.x/).</span></span> 

- <span data-ttu-id="b6be0-113">Если у вас Windows, используйте установщики msi для простой настройки NodeJS. Эти установщики можно скачать, перейдя по указанной выше ссылке.</span><span class="sxs-lookup"><span data-stu-id="b6be0-113">If you are in Windows, you can use the msi installers in the above link for easiest way to setup NodeJS</span></span>
- <span data-ttu-id="b6be0-114">Если у вас уже установлена библиотека NodeJS, проверьте, последняя ли это версия, используя команду `node -v`.</span><span class="sxs-lookup"><span data-stu-id="b6be0-114">If you have NodeJS already installed please check you have the latest version using `node -v`. It should return the current LTS version.</span></span> <span data-ttu-id="b6be0-115">Она должна вернуть текущую [версию LTS](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="b6be0-115">It should return the current [LTS version](https://nodejs.org/en/download/).</span></span> 
- <span data-ttu-id="b6be0-116">Если у вас компьютер Mac, рекомендуем устанавливать платформу NodeJS и управлять ею с помощью [homebrew](http://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="b6be0-116">If you are using a Mac, it is recommended you use [homebrew](http://brew.sh/) to install and manage NodeJS.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b6be0-117">Конвейер сборки SharePoint Framework сейчас не поддерживает версию LTS Node.js.</span><span class="sxs-lookup"><span data-stu-id="b6be0-117">Note: The SharePoint Framework build pipeline doesn't currently support the LTS version of Node.js.</span></span> <span data-ttu-id="b6be0-118">Скачайте [Node.js версии 6.11.5](https://nodejs.org/download/release/latest-v6.x/).</span><span class="sxs-lookup"><span data-stu-id="b6be0-118">Instead, download [Node.js version 6.11.5](https://nodejs.org/download/release/latest-v6.x/).</span></span> <span data-ttu-id="b6be0-119">При этом установится npm 3.10.10.</span><span class="sxs-lookup"><span data-stu-id="b6be0-119">This installs npm 3.10.10.</span></span> <span data-ttu-id="b6be0-120">Обратите внимание на то, что вы используете npm версии 5.x. Необходимо перейти на более раннюю версию npm, выполнив команду `npm install -g npm@3`.</span><span class="sxs-lookup"><span data-stu-id="b6be0-120">Note that if you have a v5.x version of npm, you will need to downgrade to an older npm version by using the following command: `npm install -g npm@3`.</span></span>

### <a name="install-a-code-editor"></a><span data-ttu-id="b6be0-121">Установка редактора кода</span><span class="sxs-lookup"><span data-stu-id="b6be0-121">Install a code editor</span></span>

<span data-ttu-id="b6be0-122">Для создания веб-частей можно использовать любой редактор кода или интерфейс IDE, поддерживающий клиентскую разработку, например:</span><span class="sxs-lookup"><span data-stu-id="b6be0-122">Install a code editor. You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

- [<span data-ttu-id="b6be0-123">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b6be0-123">Visual Studio Code</span></span>](https://code.visualstudio.com/)
- [<span data-ttu-id="b6be0-124">Atom</span><span class="sxs-lookup"><span data-stu-id="b6be0-124">Atom</span></span>](https://atom.io)
- [<span data-ttu-id="b6be0-125">Webstorm</span><span class="sxs-lookup"><span data-stu-id="b6be0-125">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

<span data-ttu-id="b6be0-126">В указаниях и примерах в этой статье используется [Visual Studio Code](https://code.visualstudio.com/), но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="b6be0-126">The steps and examples in this documentation use [Visual Studio Code](https://code.visualstudio.com/), but you can use any editor of your choice.</span></span>

### <a name="if-you-are-using-ubuntu"></a><span data-ttu-id="b6be0-127">Если используется Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b6be0-127">If you are using Ubuntu</span></span>

<span data-ttu-id="b6be0-128">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="b6be0-128">You need to install compiler tools using the following command:</span></span>

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a><span data-ttu-id="b6be0-129">Если используется Fedora</span><span class="sxs-lookup"><span data-stu-id="b6be0-129">If you are using fedora</span></span>

<span data-ttu-id="b6be0-130">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="b6be0-130">You need to install compiler tools using the following command:</span></span>

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a><span data-ttu-id="b6be0-131">Установка Yeoman и gulp</span><span class="sxs-lookup"><span data-stu-id="b6be0-131">Install Yeoman and gulp</span></span>

<span data-ttu-id="b6be0-132">[Yeoman](http://yeoman.io/) помогает запускать новые проекты, предоставляя рекомендации и инструменты, которые позволят сохранить эффективность работы.</span><span class="sxs-lookup"><span data-stu-id="b6be0-132">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive.</span></span> <span data-ttu-id="b6be0-133">Средства клиентской разработки SharePoint включают генератор Yeoman для создания веб-частей.</span><span class="sxs-lookup"><span data-stu-id="b6be0-133">SharePoint client-side development tools include a Yeoman generator for creating new web parts.</span></span> <span data-ttu-id="b6be0-134">Генератор предоставляет общие средства сборки, стандартный код и общий веб-сайт для тестирования веб-частей.</span><span class="sxs-lookup"><span data-stu-id="b6be0-134">The generator provides common build tools, common boilerplate code, and a common playground website to host web parts for testing.</span></span>

<span data-ttu-id="b6be0-135">Чтобы установить Yeoman и gulp, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b6be0-135">Enter the following command to install Yeoman and gulp:</span></span>

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a><span data-ttu-id="b6be0-136">Установка генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b6be0-136">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="b6be0-137">С помощью генератора веб-частей Yeoman для SharePoint можно быстро создать проект клиентского решения SharePoint с правильной цепочкой инструментов и структурой проекта.</span><span class="sxs-lookup"><span data-stu-id="b6be0-137">The Yeoman SharePoint web part generator helps you quickly create a SharePoint client-side solution project with the right toolchain and project structure.</span></span>

<span data-ttu-id="b6be0-138">Чтобы глобально установить генератор Yeoman для SharePoint Framework, введите такую команду:</span><span class="sxs-lookup"><span data-stu-id="b6be0-138">To install the SharePoint Framework Yeoman generator globally, enter the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint
```

<span data-ttu-id="b6be0-139">Чтобы можно было переходить между различными проектами, созданными с помощью разных версий генератора Yeoman для SharePoint, установите генератор локально как зависимость разработки в папке проекта с помощью такой команды:</span><span class="sxs-lookup"><span data-stu-id="b6be0-139">If you need to switch between the different projects created using different versions of the SharePoint Framework Yeoman generator, you can install the generator locally as a development dependency in the project folder by executing the following command:</span></span>

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

## <a name="optional-tools"></a><span data-ttu-id="b6be0-140">Дополнительные средства</span><span class="sxs-lookup"><span data-stu-id="b6be0-140">Optional tools</span></span>

<span data-ttu-id="b6be0-141">Вам также могут пригодиться следующие средства:</span><span class="sxs-lookup"><span data-stu-id="b6be0-141">Here are some tools that might come in handy as well:</span></span>

* <span data-ttu-id="b6be0-142">[Fiddler](https://www.telerik.com/fiddler);</span><span class="sxs-lookup"><span data-stu-id="b6be0-142">[Fiddler](https://www.telerik.com/fiddler)</span></span>
* <span data-ttu-id="b6be0-143">[подключаемый модуль Postman для Chrome](https://www.getpostman.com/docs/postman/launching_postman/navigating_postman);</span><span class="sxs-lookup"><span data-stu-id="b6be0-143">[Postman plugin for Chrome](https://www.getpostman.com/docs/postman/launching_postman/navigating_postman)</span></span>
* <span data-ttu-id="b6be0-144">[Cmder для Windows](http://cmder.net/);</span><span class="sxs-lookup"><span data-stu-id="b6be0-144">[Cmder for Windows](http://cmder.net/)</span></span>
* <span data-ttu-id="b6be0-145">[Oh My Zsh для Mac](http://ohmyz.sh/);</span><span class="sxs-lookup"><span data-stu-id="b6be0-145">[Oh My Zsh for Mac](http://ohmyz.sh/)</span></span>
* <span data-ttu-id="b6be0-146">[службы управления версиями Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="b6be0-146">[Git source control tools](https://git-scm.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6be0-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6be0-147">Next steps</span></span>

<span data-ttu-id="b6be0-148">Теперь вы готовы [создать свою первую клиентскую веб-часть](web-parts/get-started/build-a-hello-world-web-part.md)!</span><span class="sxs-lookup"><span data-stu-id="b6be0-148">You are now ready to [build your first client-side web part](web-parts/get-started/build-a-hello-world-web-part.md)!</span></span>

> [!NOTE]
> <span data-ttu-id="b6be0-149">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="b6be0-149">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="b6be0-150">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="b6be0-150">Thanks for your input advance.</span></span>