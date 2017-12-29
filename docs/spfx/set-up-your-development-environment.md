---
title: "Как настроить среду разработки SharePoint Framework"
ms.date: 12/11/2017
ms.prod: sharepoint
ms.openlocfilehash: 1259ceae3b13efdd0d359734fef6d080696a2c6a
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="set-up-your-sharepoint-framework-development-environment"></a><span data-ttu-id="de407-102">Как настроить среду разработки SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="de407-102">Set up your SharePoint client-side web part development environment</span></span>

<span data-ttu-id="de407-p101">Создавать решения SharePoint Framework можно в Visual Studio или другой среде разработки. Вы можете использовать компьютер Mac либо компьютер под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="de407-p101">You can use Visual Studio, or your own custom development environment to build SharePoint client-side web parts. You can use a Mac, PC, or Linux.</span></span>

><span data-ttu-id="de407-105">**Примечание.** Прежде чем выполнять действия, указанные в этой статье, обязательно [настройте клиент Office 365](./set-up-your-developer-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="de407-105">**Note:** Before following the steps in this article, be sure to [Set up your Office 365 Tenant](./set-up-your-developer-tenant.md).</span></span>

<span data-ttu-id="de407-106">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span><span class="sxs-lookup"><span data-stu-id="de407-106">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<span data-ttu-id="de407-107"><a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span><span class="sxs-lookup"><span data-stu-id="de407-107"><a href="https://www.youtube.com/watch?v=WX9FL0BjE0I&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span></span>

## <a name="install-developer-tools"></a><span data-ttu-id="de407-108">Установка средств разработчика</span><span class="sxs-lookup"><span data-stu-id="de407-108">Install developer tools</span></span>

### <a name="nodejs"></a><span data-ttu-id="de407-109">NodeJS</span><span class="sxs-lookup"><span data-stu-id="de407-109">NodeJS</span></span>

<span data-ttu-id="de407-110">Установка [NodeJS версии 6.x](https://nodejs.org/download/release/latest-v6.x/).</span><span class="sxs-lookup"><span data-stu-id="de407-110">Install [NodeJS version 6.x](https://nodejs.org/download/release/latest-v6.x/).</span></span> 

* <span data-ttu-id="de407-111">Если у вас Windows, используйте установщики msi, чтобы было проще настроить NodeJS. Эти установщики можно скачать, перейдя по указанной выше ссылке.</span><span class="sxs-lookup"><span data-stu-id="de407-111">If you are in Windows, you can use the msi installers in the above link for easiest way to setup NodeJS</span></span>
* <span data-ttu-id="de407-p102">Если у вас уже установлена платформа NodeJS, убедитесь, что установлена последняя версия, с помощью команды `node -v`. Она должна вернуть текущую [версию LTS](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="de407-p102">If you have NodeJS already installed please check you have the latest version using `node -v`. It should return the current [LTS version](https://nodejs.org/en/download/).</span></span> 
* <span data-ttu-id="de407-114">Если вы используете компьютер Mac, рекомендуем устанавливать платформу NodeJS и управлять ею с помощью [homebrew](http://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="de407-114">If you are using a Mac, it is recommended you use [homebrew](http://brew.sh/) to install and manage NodeJS.</span></span> 

><span data-ttu-id="de407-115">**Примечание.** Конвейер сборки SharePoint Framework сейчас не поддерживает версию LTS Node.js.</span><span class="sxs-lookup"><span data-stu-id="de407-115">**Note:** The SharePoint Framework build pipeline doesn't currently support the LTS version of Node.js.</span></span> <span data-ttu-id="de407-116">Скачайте [Node.js версии 6.11.5](https://nodejs.org/download/release/latest-v6.x/).</span><span class="sxs-lookup"><span data-stu-id="de407-116">Instead, download [Node.js version 6.11.5](https://nodejs.org/download/release/latest-v6.x/).</span></span> <span data-ttu-id="de407-117">При этом установится npm 3.10.10.</span><span class="sxs-lookup"><span data-stu-id="de407-117">This installs npm 3.10.10.</span></span> <span data-ttu-id="de407-118">Обратите внимание, что вы используете npm версии 5.x. Необходимо перейти на более раннюю версию npm, выполнив команду `npm install -g npm@3`.</span><span class="sxs-lookup"><span data-stu-id="de407-118">Note that if you have a v5.x version of npm, you will need to downgrade to an older npm version by using the following command: `npm install -g npm@3`.</span></span>

### <a name="code-editors"></a><span data-ttu-id="de407-119">Редакторы кода</span><span class="sxs-lookup"><span data-stu-id="de407-119">Code Editors</span></span>

<span data-ttu-id="de407-p104">Установите редактор кода. Для создания веб-частей можно использовать любой редактор кода или интерфейс IDE, поддерживающий клиентскую разработку, например:</span><span class="sxs-lookup"><span data-stu-id="de407-p104">Install a code editor. You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

* <span data-ttu-id="de407-122">[Visual Studio Code](https://code.visualstudio.com/);</span><span class="sxs-lookup"><span data-stu-id="de407-122">[Visual Studio Code](https://code.visualstudio.com/)</span></span>
* <span data-ttu-id="de407-123">[Atom](https://atom.io);</span><span class="sxs-lookup"><span data-stu-id="de407-123">[Atom](https://atom.io)</span></span>
* <span data-ttu-id="de407-124">[Webstorm](https://www.jetbrains.com/webstorm).</span><span class="sxs-lookup"><span data-stu-id="de407-124">[Webstorm](https://www.jetbrains.com/webstorm)</span></span>

<span data-ttu-id="de407-125">В указаниях и примерах в этой статье используется [Visual Studio Code](https://code.visualstudio.com/), но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="de407-125">The steps and examples in this documentation use [Visual Studio Code](https://code.visualstudio.com/), but you can use any editor of your choice.</span></span>

### <a name="if-you-are-using-ubuntu"></a><span data-ttu-id="de407-126">Если используется Ubuntu</span><span class="sxs-lookup"><span data-stu-id="de407-126">If you are using Ubuntu</span></span>

<span data-ttu-id="de407-127">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="de407-127">You need to install compiler tools using the following command:</span></span>

```sh
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a><span data-ttu-id="de407-128">Если используется Fedora</span><span class="sxs-lookup"><span data-stu-id="de407-128">If you are using fedora</span></span>

<span data-ttu-id="de407-129">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="de407-129">You need to install compiler tools using the following command:</span></span>

```sh
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a><span data-ttu-id="de407-130">Установка Yeoman и gulp</span><span class="sxs-lookup"><span data-stu-id="de407-130">Install Yeoman and gulp</span></span>

<span data-ttu-id="de407-p105">[Yeoman](http://yeoman.io/) помогает запускать новые проекты, предоставляя рекомендации и инструменты, которые позволят сохранить эффективность работы. Средства клиентской разработки SharePoint включают генератор Yeoman для создания веб-частей. Генератор предоставляет общие средства сборки, стандартный код и общий веб-сайт для тестирования веб-частей.</span><span class="sxs-lookup"><span data-stu-id="de407-p105">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive. SharePoint client-side development tools include a Yeoman generator for creating new web parts. The generator provides common build tools, common boilerplate code, and a common playground web site to host web parts for testing.</span></span>

<span data-ttu-id="de407-134">Чтобы установить Yeoman и gulp, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="de407-134">Enter the following command to install Yeoman and gulp:</span></span>

```sh
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a><span data-ttu-id="de407-135">Установка генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="de407-135">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="de407-136">С помощью генератора веб-частей Yeoman для SharePoint можно быстро создать проект клиентского решения SharePoint с правильной цепочкой инструментов и структурой проекта.</span><span class="sxs-lookup"><span data-stu-id="de407-136">The Yeoman SharePoint web part generator helps you quickly create a SharePoint client-side solution project with the right toolchain and project structure.</span></span>

<span data-ttu-id="de407-137">Чтобы глобально установить генератор Yeoman для SharePoint Framework, введите такую команду:</span><span class="sxs-lookup"><span data-stu-id="de407-137">To install the SharePoint Framework Yeoman generator globally, enter the following command:</span></span>

```sh
npm install -g @microsoft/generator-sharepoint
```

<span data-ttu-id="de407-138">Чтобы можно было переходить между различными проектами, созданными с помощью разных версий генератора Yeoman для SharePoint, установите генератор локально как зависимость разработки в папке проекта с помощью такой команды:</span><span class="sxs-lookup"><span data-stu-id="de407-138">If you need to switch between the different projects created using different versions of the SharePoint Framework Yeoman generator, you can install the generator locally as a development dependency in the project folder by executing the following command:</span></span>

```sh
npm install @microsoft/generator-sharepoint --save-dev
```

## <a name="optional-tools"></a><span data-ttu-id="de407-139">Дополнительные средства</span><span class="sxs-lookup"><span data-stu-id="de407-139">Optional tools</span></span>

<span data-ttu-id="de407-140">Вам также могут пригодиться следующие средства:</span><span class="sxs-lookup"><span data-stu-id="de407-140">Here are some tools that might come in handy as well:</span></span>

* [<span data-ttu-id="de407-141">Fiddler</span><span class="sxs-lookup"><span data-stu-id="de407-141">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="de407-142">Подключаемый модуль Postman для Chrome</span><span class="sxs-lookup"><span data-stu-id="de407-142">Postman plugin for Chrome</span></span>](https://www.getpostman.com/docs/introduction)
* [<span data-ttu-id="de407-143">Cmder для Windows</span><span class="sxs-lookup"><span data-stu-id="de407-143">Cmder for Windows</span></span>](http://cmder.net/)
* [<span data-ttu-id="de407-144">Oh My Zsh для Mac</span><span class="sxs-lookup"><span data-stu-id="de407-144">Oh My Zsh for Mac</span></span>](http://ohmyz.sh/)
* [<span data-ttu-id="de407-145">Службы управления версиями Git</span><span class="sxs-lookup"><span data-stu-id="de407-145">Git source control tools</span></span>](https://git-scm.com/)

## <a name="next-steps"></a><span data-ttu-id="de407-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de407-146">Next steps</span></span>

<span data-ttu-id="de407-147">Теперь вы готовы [создать свою первую клиентскую веб-часть](web-parts/get-started/build-a-hello-world-web-part.md)!</span><span class="sxs-lookup"><span data-stu-id="de407-147">You are now ready to [build your first client-side web part](web-parts/get-started/build-a-hello-world-web-part.md)!</span></span>

> [!NOTE]
> <span data-ttu-id="de407-148">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint в [репозитории sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="de407-148">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="de407-149">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="de407-149">Thanks for your input advance.</span></span>