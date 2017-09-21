# <a name="set-up-your-sharepoint-client-side-web-part-development-environment"></a><span data-ttu-id="8b177-101">Настройка среды разработки клиентских веб-частей SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b177-101">Set up your SharePoint client-side web part development environment</span></span>

<span data-ttu-id="8b177-p101">Для создания клиентских веб-частей SharePoint можно использовать Visual Studio или другую среду разработки. Вы можете использовать компьютер Mac либо компьютер под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="8b177-p101">You can use Visual Studio, or your own custom development environment to build SharePoint client-side web parts. You can use a Mac, PC, or Linux.</span></span>

><span data-ttu-id="8b177-104">**Примечание.** Прежде чем выполнять действия, указанные в этой статье, обязательно [настройте клиент Office 365](./set-up-your-developer-tenant).</span><span class="sxs-lookup"><span data-stu-id="8b177-104">**Note:** Before following the steps in this article, be sure to [Set up your Office 365 Tenant](./set-up-your-developer-tenant).</span></span>

<span data-ttu-id="8b177-105">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=1).</span><span class="sxs-lookup"><span data-stu-id="8b177-105">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq&index=1).</span></span> 

<span data-ttu-id="8b177-106"><a href="https://www.youtube.com/watch?v=_fxYexlUhe0&t=5s&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq"> <img src="../../images/spfx-youtube-tutorial0.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a></span><span class="sxs-lookup"><span data-stu-id="8b177-106"></span></span>


## <a name="install-developer-tools"></a><span data-ttu-id="8b177-107">Установка средств разработчика</span><span class="sxs-lookup"><span data-stu-id="8b177-107">Install developer tools</span></span>

### <a name="nodejs"></a><span data-ttu-id="8b177-108">NodeJS</span><span class="sxs-lookup"><span data-stu-id="8b177-108">NodeJS</span></span>
<span data-ttu-id="8b177-109">Установите [NodeJS](https://nodejs.org/en/) с долгосрочной поддержкой (LTS).</span><span class="sxs-lookup"><span data-stu-id="8b177-109">Install [NodeJS](https://nodejs.org/en/) Long Term Support (LTS) version.</span></span>

* <span data-ttu-id="8b177-p102">Если у вас уже установлена библиотека NodeJS, убедитесь, что установлена последняя версия, с помощью команды `node -v`. Она должна вернуть текущую [версию LTS](https://nodejs.org/en/download/).</span><span class="sxs-lookup"><span data-stu-id="8b177-p102">If you have NodeJS already installed please check you have the latest version using `node -v`. It should return the current [LTS version](https://nodejs.org/en/download/).</span></span> 
* <span data-ttu-id="8b177-112">Если вы используете компьютер Mac, рекомендуем устанавливать платформу NodeJS и управлять ею с помощью [homebrew](http://brew.sh/).</span><span class="sxs-lookup"><span data-stu-id="8b177-112">If you are using a Mac, it is recommended you use [homebrew](http://brew.sh/) to install and manage NodeJS.</span></span> 

> <span data-ttu-id="8b177-p103">Обратите внимание на то, что конвейер сборки SPFx сейчас **НЕ** поддерживает npm 5.x, поэтому нужна версия 3 или 4. На момент написания этой статьи LTS-версия NodeJS (6.11.0) устанавливает npm 3.10.10. Когда изменится ситуация с поддержкой, мы добавим соответствующие сведения в этот раздел. Вы можете перейти на использование более ранней версии npm с помощью команды `npm install -g npm@3`.</span><span class="sxs-lookup"><span data-stu-id="8b177-p103">Notice that SPFx build pipeline does **NOT** currently support npm v5.x, so you'll need to use either v3 or v4. At the time of the writing, NodeJS LTS version (v6.11.0) installs npm v3.10.10. We'll update this section when there are changes in the supportability statement. You can downgrade to older npm version with following command `npm install -g npm@3`.</span></span>

### <a name="code-editors"></a><span data-ttu-id="8b177-117">Редакторы кода</span><span class="sxs-lookup"><span data-stu-id="8b177-117">Code Editors</span></span>
<span data-ttu-id="8b177-p104">Установите редактор кода. Для создания веб-частей можно использовать любой редактор кода или интерфейс IDE, поддерживающий клиентскую разработку, например:</span><span class="sxs-lookup"><span data-stu-id="8b177-p104">Install a code editor. You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

* <span data-ttu-id="8b177-120">[Visual Studio Code](https://code.visualstudio.com/);</span><span class="sxs-lookup"><span data-stu-id="8b177-120">[Visual Studio Code](https://code.visualstudio.com/)</span></span>
* <span data-ttu-id="8b177-121">[Atom](https://atom.io);</span><span class="sxs-lookup"><span data-stu-id="8b177-121">[Atom](https://atom.io)</span></span>
* <span data-ttu-id="8b177-122">[Webstorm](https://www.jetbrains.com/webstorm).</span><span class="sxs-lookup"><span data-stu-id="8b177-122">[Webstorm](https://www.jetbrains.com/webstorm)</span></span> 

<span data-ttu-id="8b177-123">В указаниях и примерах в этой статье используется [Visual Studio Code](https://code.visualstudio.com/), но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="8b177-123">The steps and examples in this documentation use [Visual Studio Code](https://code.visualstudio.com/), but you can use any editor of your choice.</span></span> 

### <a name="if-you-are-using-ubuntu"></a><span data-ttu-id="8b177-124">Если используется Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8b177-124">If you are using Ubuntu</span></span>

<span data-ttu-id="8b177-125">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8b177-125">You need to install compiler tools using the following command:</span></span>
    
```
sudo apt-get install build-essential
```

### <a name="if-you-are-using-fedora"></a><span data-ttu-id="8b177-126">Если используется Fedora</span><span class="sxs-lookup"><span data-stu-id="8b177-126">If you are using fedora</span></span>

<span data-ttu-id="8b177-127">Необходимо установить средства компиляции с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8b177-127">You need to install compiler tools using the following command:</span></span>
    
```
sudo yum install make automake gcc gcc-c++ kernel-devel
```

## <a name="install-yeoman-and-gulp"></a><span data-ttu-id="8b177-128">Установка Yeoman и gulp</span><span class="sxs-lookup"><span data-stu-id="8b177-128">Install Yeoman and gulp</span></span>

<span data-ttu-id="8b177-p105">[Yeoman](http://yeoman.io/) помогает запускать новые проекты, предоставляя рекомендации и инструменты, которые позволят сохранить эффективность работы. Средства клиентской разработки SharePoint включают генератор Yeoman для создания веб-частей. Генератор предоставляет общие средства сборки, стандартный код и общий веб-сайт для тестирования веб-частей.</span><span class="sxs-lookup"><span data-stu-id="8b177-p105">[Yeoman](http://yeoman.io/) helps you kick-start new projects, and prescribes best practices and tools to help you stay productive. SharePoint client-side development tools include a Yeoman generator for creating new web parts. The generator provides common build tools, common boilerplate code, and a common playground web site to host web parts for testing.</span></span>

<span data-ttu-id="8b177-132">Чтобы установить Yeoman и gulp, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8b177-132">Enter the following command to install Yeoman and gulp:</span></span>
    
```
npm install -g yo gulp
```

## <a name="install-yeoman-sharepoint-generator"></a><span data-ttu-id="8b177-133">Установка генератора Yeoman для SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b177-133">Install Yeoman SharePoint generator</span></span>

<span data-ttu-id="8b177-134">С помощью генератора веб-частей Yeoman для SharePoint можно быстро создать проект клиентского решения SharePoint с правильной цепочкой инструментов и структурой проекта.</span><span class="sxs-lookup"><span data-stu-id="8b177-134">The Yeoman SharePoint web part generator helps you quickly create a SharePoint client-side solution project with the right toolchain and project structure.</span></span>

<span data-ttu-id="8b177-135">Чтобы установить генератор yeoman для SharePoint, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8b177-135">Enter the following command to install the Yeoman SharePoint generator:</span></span>
    
```
npm install -g @microsoft/generator-sharepoint 
```
><span data-ttu-id="8b177-136">**Примечание.** Генератор Yeoman для SharePoint можно установить как глобально, так и локально.</span><span class="sxs-lookup"><span data-stu-id="8b177-136">**Note:** Yeoman generator for SharePoint can be installed both globally and locally.</span></span> <span data-ttu-id="8b177-137">В этом случае мы устанавливаем генератор Yeoman для SharePoint глобально.</span><span class="sxs-lookup"><span data-stu-id="8b177-137">In this case we are installing the Yeoman generator for SharePoint to be available globally.</span></span> 


## <a name="optional-tools"></a><span data-ttu-id="8b177-138">Дополнительные средства</span><span class="sxs-lookup"><span data-stu-id="8b177-138">Optional tools</span></span>

<span data-ttu-id="8b177-139">Вам также могут пригодиться следующие средства:</span><span class="sxs-lookup"><span data-stu-id="8b177-139">Here are some tools that might come in handy as well:</span></span>

* [<span data-ttu-id="8b177-140">Fiddler</span><span class="sxs-lookup"><span data-stu-id="8b177-140">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="8b177-141">Подключаемый модуль Postman для Chrome</span><span class="sxs-lookup"><span data-stu-id="8b177-141">Postman plugin for Chrome</span></span>](https://www.getpostman.com/docs/introduction)
* [<span data-ttu-id="8b177-142">Cmder для Windows</span><span class="sxs-lookup"><span data-stu-id="8b177-142">Cmder for Windows</span></span>](http://cmder.net/)
* [<span data-ttu-id="8b177-143">Oh My Zsh для Mac</span><span class="sxs-lookup"><span data-stu-id="8b177-143">Oh My Zsh for Mac</span></span>](http://ohmyz.sh/)
* [<span data-ttu-id="8b177-144">Службы управления версиями Git</span><span class="sxs-lookup"><span data-stu-id="8b177-144">Git source control tools</span></span>](https://git-scm.com/)

## <a name="next-steps"></a><span data-ttu-id="8b177-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b177-145">Next steps</span></span>

<span data-ttu-id="8b177-146">Теперь вы готовы [создать свою первую клиентскую веб-часть](web-parts/get-started/build-a-hello-world-web-part)!</span><span class="sxs-lookup"><span data-stu-id="8b177-146">You are now ready to [build your first client-side web part](web-parts/get-started/build-a-hello-world-web-part)!</span></span>
