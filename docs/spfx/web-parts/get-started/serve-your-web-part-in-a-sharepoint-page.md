---
title: "Развертывание клиентской веб-части на странице SharePoint (Hello World, часть 3)"
description: "Разверните клиентскую веб-часть в SharePoint и проверьте ее работу на современной странице SharePoint."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 89bbf4fe214dd74d399005c2986156be13c744c3
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="deploy-your-client-side-web-part-to-a-sharepoint-page-hello-world-part-3"></a><span data-ttu-id="dd533-103">Развертывание клиентской веб-части на странице SharePoint (Hello World, часть 3)</span><span class="sxs-lookup"><span data-stu-id="dd533-103">Deploy your client-side web part to a SharePoint page (Hello World part 3)</span></span>

<span data-ttu-id="dd533-104">Прежде чем приступать к процедурам этой статьи, выполните инструкции из следующих статей:</span><span class="sxs-lookup"><span data-stu-id="dd533-104">Ensure that you have completed the procedures in the following articles before you start:</span></span>

* [<span data-ttu-id="dd533-105">Создание первой клиентской веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd533-105">Build your first SharePoint client-side web part</span></span>](./build-a-hello-world-web-part.md)
* [<span data-ttu-id="dd533-106">Подключение клиентской веб-части к SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd533-106">Connect your client-side web part to SharePoint</span></span>](./connect-to-sharepoint.md)

<span data-ttu-id="dd533-107">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=BpJ01ahxbiY&index=4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span><span class="sxs-lookup"><span data-stu-id="dd533-107">You can also follow these steps by watching this video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=BpJ01ahxbiY&index=4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span> 

<a href="https://www.youtube.com/watch?v=BpJ01ahxbiY&index=4&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../images/spfx-youtube-tutorial3.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="package-the-helloworld-web-part"></a><span data-ttu-id="dd533-108">Упаковка веб-части HelloWorld</span><span class="sxs-lookup"><span data-stu-id="dd533-108">Package the HelloWorld web part</span></span>

1. <span data-ttu-id="dd533-109">В окне консоли перейдите к каталогу проекта веб-части, создание которого описано в статье [Создание первой клиентской веб-части SharePoint](./build-a-hello-world-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="dd533-109">In the console window, go to the web part project directory created in [Build your first SharePoint client-side web part](./build-a-hello-world-web-part.md).</span></span>

  ```
  cd helloworld-webpart
  ```

2. <span data-ttu-id="dd533-110">Если команда `gulp serve` все еще выполняется, остановите ее, нажав клавиши CTRL+C.</span><span class="sxs-lookup"><span data-stu-id="dd533-110">If `gulp serve` is still running, stop it from running by selecting Ctrl+C.</span></span>

  <span data-ttu-id="dd533-111">Чтобы использовать клиентскую веб-часть не в Workbench, а на современных серверных страницах SharePoint, ее необходимо развернуть и зарегистрировать в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dd533-111">Unlike in the Workbench, to use client-side web parts on modern SharePoint server-side pages, you need to deploy and register the web part with SharePoint.</span></span> <span data-ttu-id="dd533-112">Для начала необходимо упаковать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="dd533-112">First you need to package the web part.</span></span>

3. <span data-ttu-id="dd533-113">Откройте проект веб-части **HelloWorldWebPart** в Visual Studio Code или другой предпочитаемой IDE.</span><span class="sxs-lookup"><span data-stu-id="dd533-113">Open the **HelloWorldWebPart** web part project in Visual Studio Code, or your preferred IDE.</span></span>

4. <span data-ttu-id="dd533-114">Откройте файл **package-solution.json** в папке **config**.</span><span class="sxs-lookup"><span data-stu-id="dd533-114">Open **package-solution.json** from the **config** folder.</span></span>

  <span data-ttu-id="dd533-115">В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="dd533-115">The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

  ```json
  {
    "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
    "solution": {
      "name": "helloworld-webpart-client-side-solution",
      "id": "4432f33b-5845-4ca0-827e-a8ae68c7b945",
      "version": "1.0.0.0",
      "includeClientSideAssets": true
    },
    "paths": {
      "zippedPackage": "solution/helloworld-webpart.sppkg"
    }
  }

  ```

5. <span data-ttu-id="dd533-116">Чтобы упаковать клиентское решение, содержащее веб-часть, введите в окне консоли следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dd533-116">In the console window, enter the following command to package your client-side solution that contains the web part:</span></span>

  ```
  gulp package-solution
  ```

  <span data-ttu-id="dd533-117">Эта команда создаст пакет в папке `sharepoint/solution`:</span><span class="sxs-lookup"><span data-stu-id="dd533-117">The command creates the package in the `sharepoint/solution` folder:</span></span>

  ```
  helloworld-webpart.sppkg
  ```

### <a name="package-contents"></a><span data-ttu-id="dd533-118">Содержимое пакета</span><span class="sxs-lookup"><span data-stu-id="dd533-118">Package contents</span></span>

<span data-ttu-id="dd533-119">Чтобы упаковать веб-часть, пакет использует компонент SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dd533-119">The package uses SharePoint Feature to package your web part.</span></span> <span data-ttu-id="dd533-120">По умолчанию задача gulp создает функцию для веб-части.</span><span class="sxs-lookup"><span data-stu-id="dd533-120">By default, the gulp task creates a feature for your web part.</span></span>

<span data-ttu-id="dd533-121">Вы можете просмотреть необработанное содержимое пакета в папке **sharepoint/debug**.</span><span class="sxs-lookup"><span data-stu-id="dd533-121">You can view the raw package contents in the **sharepoint/debug** folder.</span></span> 

<span data-ttu-id="dd533-122">Затем содержимое упаковывается в **SPPKG**-файл.</span><span class="sxs-lookup"><span data-stu-id="dd533-122">The contents are then packaged into an **.sppkg** file.</span></span> <span data-ttu-id="dd533-123">Формат пакета напоминает таковой для пакета надстроек SharePoint. Для упаковки решения используются правила спецификации Microsoft Open Packaging Conventions.</span><span class="sxs-lookup"><span data-stu-id="dd533-123">The package format is very similar to a SharePoint Add-ins package and uses Microsoft Open Packaging Conventions to package your solution.</span></span> 

<span data-ttu-id="dd533-124">Файлы JavaScript, CSS и другие ресурсы включаются в пакет при использовании параметра `--ship`.</span><span class="sxs-lookup"><span data-stu-id="dd533-124">The JavaScript files, CSS, and other assets are packaged inside of the package when the `--ship` option is used.</span></span> <span data-ttu-id="dd533-125">Однако в этом случае мы сначала проверим развертывание и возможности, разместив файлы JavaScript в localhost.</span><span class="sxs-lookup"><span data-stu-id="dd533-125">In this case, however, we will first test deployment and capabilities by hosting JavaScript files from localhost.</span></span> <span data-ttu-id="dd533-126">Этот способ развертывания рассматривается в следующем руководстве.</span><span class="sxs-lookup"><span data-stu-id="dd533-126">This deployment option is explained in the next tutorial.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd533-127">Начиная с SharePoint Framework версии 1.4, статические ресурсы по умолчанию упаковываются в SPPKG-файлы.</span><span class="sxs-lookup"><span data-stu-id="dd533-127">Starting from the SharePoint Framework v1.4, static assets are by default packaged inside of the sppkg package.</span></span> <span data-ttu-id="dd533-128">При развертывании пакета в каталоге приложений ресурсы автоматически размещаются в сети CDN Office 365 (если она включена) или по URL-адресу каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="dd533-128">When a package is deployed in the App Catalog, the assets are automatically hosted either from Office 365 CDN (if enabled) or from an App Catalog URL.</span></span> <span data-ttu-id="dd533-129">Эти действия можно изменить с помощью параметра `includeClientSideAssets` в файле `package-solution.json`.</span><span class="sxs-lookup"><span data-stu-id="dd533-129">You can control this behavior with the `includeClientSideAssets` setting in the `package-solution.json` file.</span></span>


## <a name="deploy-the-helloworld-package-to-app-catalog"></a><span data-ttu-id="dd533-130">Развертывание пакета HelloWorld в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="dd533-130">Deploy the HelloWorld package to app catalog</span></span>

<span data-ttu-id="dd533-131">Теперь необходимо развернуть пакет, созданный в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="dd533-131">Next, you need to deploy the package that was generated to the App Catalog.</span></span>

1. <span data-ttu-id="dd533-132">Перейдите в каталог приложений вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="dd533-132">Go to your site's App Catalog.</span></span>

2. <span data-ttu-id="dd533-133">Отправьте или перетащите файл **helloworld-webpart.sppkg** в каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="dd533-133">Upload or drag and drop the **helloworld-webpart.sppkg** to the App Catalog.</span></span>

  ![Отправка решения в каталог приложений](../../../images/upload-solution-app-catalog.png) 

  <span data-ttu-id="dd533-135">При этом будет развернут пакет клиентского решения.</span><span class="sxs-lookup"><span data-stu-id="dd533-135">This deploys the client-side solution package.</span></span> <span data-ttu-id="dd533-136">Так как это клиентское решение с полным доверием, в SharePoint появится диалоговое окно с предложением разрешить развертывание клиентского решения.</span><span class="sxs-lookup"><span data-stu-id="dd533-136">Because this is a full trust client-side solution, SharePoint displays a dialog and asks you to trust the client-side solution to deploy.</span></span>

  ![Доверие развертыванию клиентского решения](../../../images/sp-app-deploy-trust.png) 
    
3. <span data-ttu-id="dd533-138">Выберите **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="dd533-138">Select **Deploy**.</span></span>


## <a name="install-the-client-side-solution-on-your-site"></a><span data-ttu-id="dd533-139">Установка клиентского решения на сайте</span><span class="sxs-lookup"><span data-stu-id="dd533-139">Install the client-side solution on your site</span></span>

1. <span data-ttu-id="dd533-140">Перейдите к семейству веб-сайтов разработчика.</span><span class="sxs-lookup"><span data-stu-id="dd533-140">Go to your developer site collection.</span></span>

2. <span data-ttu-id="dd533-141">Нажмите значок шестеренки на верхней панели навигации справа и выберите **Добавить приложение**, чтобы перейти к странице "Приложения".</span><span class="sxs-lookup"><span data-stu-id="dd533-141">Select the gears icon on the top nav bar on the right, and then select **Add an app** to go to your Apps page.</span></span>

3. <span data-ttu-id="dd533-142">В **поле поиска** введите **helloworld** и нажмите клавишу ВВОД, чтобы отфильтровать приложения.</span><span class="sxs-lookup"><span data-stu-id="dd533-142">In the **Search** box, enter **helloworld**, and select Enter to filter your apps.</span></span>
    
  ![Добавление приложения на сайт](../../../images/install-app-your-site.png)
    
4. <span data-ttu-id="dd533-144">Выберите приложение **helloworld-webpart-client-side-solution**, чтобы установить его на сайте.</span><span class="sxs-lookup"><span data-stu-id="dd533-144">Select the **helloworld-webpart-client-side-solution** app to install the app on the site.</span></span>
    
  ![Доверие приложению](../../../images/app-installed-your-site.png)

  <span data-ttu-id="dd533-146">Теперь клиентское решение и веб-часть установлены на сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="dd533-146">The client-side solution and the web part are installed on your developer site.</span></span>

<span data-ttu-id="dd533-147">На странице **Содержимое сайта** отображается состояние установки клиентского решения.</span><span class="sxs-lookup"><span data-stu-id="dd533-147">The **Site Contents** page shows you the installation status of your client-side solution.</span></span> <span data-ttu-id="dd533-148">Прежде чем переходить к следующему шагу, убедитесь, что установка завершена.</span><span class="sxs-lookup"><span data-stu-id="dd533-148">Make sure the installation is complete before going to the next step.</span></span>

## <a name="preview-the-web-part-on-a-sharepoint-page"></a><span data-ttu-id="dd533-149">Предварительный просмотр веб-части на странице SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd533-149">Preview the web part on a SharePoint page</span></span>

<span data-ttu-id="dd533-150">Теперь, когда вы развернули и установили клиентское решение, добавьте веб-часть на страницу SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dd533-150">Now that you have deployed and installed the client-side solution, add the web part to a SharePoint page.</span></span> <span data-ttu-id="dd533-151">Помните, что такие ресурсы, как JavaScript и CSS, доступны с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="dd533-151">Remember that resources such as JavaScript and CSS are available from the local computer.</span></span>

1. <span data-ttu-id="dd533-152">Откройте `<your-webpart-guid>.manifest.json` из папки `\dist`.</span><span class="sxs-lookup"><span data-stu-id="dd533-152">Open the `<your-webpart-guid>.manifest.json` from the `\dist` folder.</span></span>
    
  <span data-ttu-id="dd533-153">Обратите внимание на то, что свойство **internalModuleBaseUrls** в разделе **loaderConfig** по-прежнему указывает на локальный компьютер:</span><span class="sxs-lookup"><span data-stu-id="dd533-153">Notice that the **internalModuleBaseUrls** property in the **loaderConfig** entry still refers to your local computer:</span></span>

  ```json
  "internalModuleBaseUrls": [
    "https://`your-local-machine-name`:4321/"
  ]
  ```

2. <span data-ttu-id="dd533-154">Прежде чем добавлять веб-часть на серверную страницу SharePoint, запустите локальный сервер.</span><span class="sxs-lookup"><span data-stu-id="dd533-154">Before adding the web part to a SharePoint server-side page, run the local server.</span></span>
    
3. <span data-ttu-id="dd533-155">В окне консоли с каталогом проекта **helloworld-webpart** выполните задачу gulp, чтобы начать обслуживание с localhost:</span><span class="sxs-lookup"><span data-stu-id="dd533-155">In the console window that has the **helloworld-webpart** project directory, run the gulp task to start serving from localhost:</span></span>
    
  ```
  gulp serve --nobrowser
  ```

  > [!NOTE]
  > <span data-ttu-id="dd533-156">SharePoint Workbench не запускается автоматически при использовании `--nobrowser`.</span><span class="sxs-lookup"><span data-stu-id="dd533-156">`--nobrowser` will not automatically launch the SharePoint Workbench.</span></span>

## <a name="add-the-helloworld-web-part-to-modern-page"></a><span data-ttu-id="dd533-157">Добавление веб-части HelloWorld на современную страницу</span><span class="sxs-lookup"><span data-stu-id="dd533-157">Add the HelloWorld web part to modern page</span></span>

1. <span data-ttu-id="dd533-158">В браузере перейдите на сайт, где только что было установлено решение.</span><span class="sxs-lookup"><span data-stu-id="dd533-158">In your browser, go to your site where the solution was just installed.</span></span>
    
2. <span data-ttu-id="dd533-159">Нажмите значок шестеренки на верхней панели навигации справа и выберите **Добавить страницу**.</span><span class="sxs-lookup"><span data-stu-id="dd533-159">Select the gears icon in the top nav bar on the right, and then select **Add a page**.</span></span>
    
3. <span data-ttu-id="dd533-160">Отредактируйте страницу.</span><span class="sxs-lookup"><span data-stu-id="dd533-160">Edit the page.</span></span> 

4. <span data-ttu-id="dd533-161">Откройте средство выбора веб-частей и выберите веб-часть **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="dd533-161">Open the web part picker and select your **HelloWorld** web part.</span></span>
        
<span data-ttu-id="dd533-162">Из локальной среды будут загружены ресурсы веб-части.</span><span class="sxs-lookup"><span data-stu-id="dd533-162">The web part assets are loaded from the local environment.</span></span> <span data-ttu-id="dd533-163">Чтобы загрузить скрипты, размещенные на локальном компьютере, необходимо разрешить в браузере выполнение небезопасных скриптов.</span><span class="sxs-lookup"><span data-stu-id="dd533-163">To load the scripts hosted on your local computer, you need to enable the browser to load unsafe scripts.</span></span> <span data-ttu-id="dd533-164">Убедитесь, что в вашем браузере включено выполнение небезопасных скриптов для данного сеанса.</span><span class="sxs-lookup"><span data-stu-id="dd533-164">Depending on the browser you are using, make sure you enable loading unsafe scripts for this session.</span></span>
    
<span data-ttu-id="dd533-165">Должна появиться веб-часть **HelloWorld**, создание которой описано в предыдущей статье, получающая списки с текущего сайта.</span><span class="sxs-lookup"><span data-stu-id="dd533-165">You should see the **HelloWorld** web part you built in the previous article that retrieves lists from the current site.</span></span> 

![Веб-часть Hello World на современной странице](../../../images/sp-wp-modern-page.png)

## <a name="edit-web-part-properties"></a><span data-ttu-id="dd533-167">Изменение свойств веб-части</span><span class="sxs-lookup"><span data-stu-id="dd533-167">Edit web part properties</span></span>

1. <span data-ttu-id="dd533-168">Выберите значок **Настроить элемент** (перо) в веб-части, чтобы открыть область свойств.</span><span class="sxs-lookup"><span data-stu-id="dd533-168">Select the **Configure element** icon (pen) in the web part to open the property pane for the web part.</span></span>

  ![Изменение веб-части](../../../images/edit-webpart-modern-page.png)

  <span data-ttu-id="dd533-170">Это та же область свойств, которую вы создали и проверили в Workbench.</span><span class="sxs-lookup"><span data-stu-id="dd533-170">This is the same property pane you built and previewed in the Workbench.</span></span>
    
2. <span data-ttu-id="dd533-171">Измените свойство **Description** (Описание), указав текст **Client-side web parts are awesome!** (Клиентские веб-части — это круто).</span><span class="sxs-lookup"><span data-stu-id="dd533-171">Edit the **Description** property, and enter **Client-side web parts are awesome!**</span></span>
    
  ![Веб-часть Hello World на современной странице](../../../images/sp-wp-modern-page-pp.png)

3. <span data-ttu-id="dd533-173">Обратите внимание на то, что веб-часть обновляется по мере ввода текста, как и на реактивной панели.</span><span class="sxs-lookup"><span data-stu-id="dd533-173">Notice that you still have the same behaviors such as a reactive pane where the web part is updated as you type.</span></span>
    
4. <span data-ttu-id="dd533-174">Выберите значок **x**, чтобы закрыть клиентскую область свойств.</span><span class="sxs-lookup"><span data-stu-id="dd533-174">Select the **x** icon to close the client-side property pane.</span></span>
        
5. <span data-ttu-id="dd533-175">На панели инструментов выберите **Сохранить и закрыть**, чтобы сохранить страницу.</span><span class="sxs-lookup"><span data-stu-id="dd533-175">On the toolbar, select **Save and close** to save the page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd533-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd533-176">Next steps</span></span>

<span data-ttu-id="dd533-177">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="dd533-177">Congratulations!</span></span> <span data-ttu-id="dd533-178">Вы развернули клиентскую веб-часть на современной странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dd533-178">You have deployed a client-side web part to a modern SharePoint page.</span></span> 

<span data-ttu-id="dd533-179">Вы можете продолжить разработку веб-части Hello World, прочитав следующую статью — [Размещение клиентской веб-части в сети доставки содержимого Office 365](./hosting-webpart-from-office-365-cdn.md). Из нее вы узнаете, как развернуть ресурсы веб-части и загрузить их из сети CDN Office 365, а не из localhost.</span><span class="sxs-lookup"><span data-stu-id="dd533-179">You can continue building out your Hello World web part in the next topic [Hosting client-side web part from Office 365 CDN](./hosting-webpart-from-office-365-cdn.md), where you will learn how to deploy and load the web part assets from an Office 365 CDN instead of localhost.</span></span>

> [!NOTE]
> <span data-ttu-id="dd533-180">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="dd533-180">If you find an issue in the documentation or in the SharePoint Framework, report that to SharePoint engineering by using the [issue list at the sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="dd533-181">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="dd533-181">Thanks for your input in advance.</span></span>