---
title: "Размещение клиентской веб-части в сети доставки содержимого Office 365"
ms.date: 12/11/2017
ms.prod: sharepoint
ms.openlocfilehash: 3abc6748269fe9709678c6b02b514662cc156587
ms.sourcegitcommit: 6018dbb696faef5f60ebf0f79f830385fab2a4d8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="hosting-client-side-web-part-from-office-365-cdn-hello-world-part-4"></a><span data-ttu-id="15cb9-102">Размещение клиентской веб-части в сети доставки содержимого Office 365 (Hello World, часть 4)</span><span class="sxs-lookup"><span data-stu-id="15cb9-102">Hosting extension from Office 365 CDN (Hello world part 4)</span></span>

<span data-ttu-id="15cb9-p101">В данной статье описано размещение клиентской веб-части в сети CDN Office 365. Эта сеть представляет собой простое решение для размещения ресурсов непосредственно в собственном клиенте Office 365. В ней можно размещать любые статические ресурсы, используемые в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="15cb9-p101">This article describes how to host your client-side web part from Office 365 CDN. Office 365 CDN provide you easy solution to host your assets directly from your own Office 365 tenant. It can be used for hosting any static assets, which are used in SharePoint Online. You can find more details around the Office 365 CDN capability from following blog post.</span></span> 

> [!NOTE]
> <span data-ttu-id="15cb9-106">Разместить ресурсы веб-части можно несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="15cb9-106">There are multiple different hosting options for your web part assets.</span></span> <span data-ttu-id="15cb9-107">В этом руководстве описана сеть CDN Office 365, но можно также использовать [сеть доставки содержимого Azure](./deploy-web-part-to-cdn.md) или просто разместить ресурсы в библиотеке SharePoint из своего клиента.</span><span class="sxs-lookup"><span data-stu-id="15cb9-107">This tutorial concentrates on showing the Azure CDN option, but you could also use the [Office 365 CDN](./deploy-web-part-to-cdn.md) or simply host your assets from SharePoint library from your tenant.</span></span> <span data-ttu-id="15cb9-108">Последний вариант предоставляет такие же возможности, но уступает сетям CDN в производительности.</span><span class="sxs-lookup"><span data-stu-id="15cb9-108">In the latter case, you would not benefit from the CDN performance improvements, but that would also work from the functionality perspective.</span></span> <span data-ttu-id="15cb9-109">Ресурсы можно разместить в любом расположении, к которому пользователи могут получить доступ с помощью протокола HTTP(S).</span><span class="sxs-lookup"><span data-stu-id="15cb9-109">Any location which end users can access using HTTP would be technically suitable for hosting the assets for end users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15cb9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="15cb9-110">Prerequisites</span></span>

<span data-ttu-id="15cb9-111">Прежде чем приступать к работе, убедитесь, что выполнены следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="15cb9-111">Make sure that you have completed the following tasks before you begin:</span></span>

* [<span data-ttu-id="15cb9-112">Создание первой клиентской веб-части</span><span class="sxs-lookup"><span data-stu-id="15cb9-112">Build your first client-side web part</span></span>](./build-a-hello-world-web-part.md)
* [<span data-ttu-id="15cb9-113">Подключение клиентской веб-части к SharePoint</span><span class="sxs-lookup"><span data-stu-id="15cb9-113">Connect your client-side web part to SharePoint</span></span>](./connect-to-sharepoint.md)
* [<span data-ttu-id="15cb9-114">Развертывание клиентской веб-части на классической странице SharePoint</span><span class="sxs-lookup"><span data-stu-id="15cb9-114">Deploy your client-side web part to a classic SharePoint page</span></span>](./serve-your-web-part-in-a-sharepoint-page.md)


<span data-ttu-id="15cb9-115">Эти действия также показаны в видео [канала SharePoint PnP на сайте YouTube](https://www.youtube.com/watch?v=MEZMs8VMVQ0&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span><span class="sxs-lookup"><span data-stu-id="15cb9-115">You can also follow follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=MEZMs8VMVQ0&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq).</span></span>

<a href="https://www.youtube.com/watch?v=MEZMs8VMVQ0&list=PLR9nK3mnD-OXvSWvS2zglCzz4iplhVrKq">
<img src="../../../images/spfx-youtube-tutorial4.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>



## <a name="enable-cdn-in-your-office-365-tenant"></a><span data-ttu-id="15cb9-116">Включение сети доставки содержимого в клиенте Office 365</span><span class="sxs-lookup"><span data-stu-id="15cb9-116">Enable CDN in your Office 365 tenant</span></span>
<span data-ttu-id="15cb9-117">Скачайте последнюю версию командной консоли SharePoint Online на [сайте загрузки Майкрософт](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="15cb9-117">Ensure that you have latest version of the SharePoint Online Management Shell by downloading it from [Microsoft Download site](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

> [!TIP]
> <span data-ttu-id="15cb9-118">Командную консоль SPO невозможно использовать на компьютерах без Windows.</span><span class="sxs-lookup"><span data-stu-id="15cb9-118">If you are using non-Windows machine, you cannot use the SPO Management Shell.</span></span> <span data-ttu-id="15cb9-119">Однако вы можете управлять этими параметрами с помощью [интерфейса командной строки Office 365](https://sharepoint.github.io/office365-cli/).</span><span class="sxs-lookup"><span data-stu-id="15cb9-119">You can however manage these settings using [Office 365 CLI](https://sharepoint.github.io/office365-cli/).</span></span>

<span data-ttu-id="15cb9-120">Подключитесь к клиенту SharePoint Online с помощью сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15cb9-120">Connect to your SharePoint Online tenant with PowerShell session.</span></span>
```
Connect-SPOService -Url https://contoso-admin.sharepoint.com
```

<span data-ttu-id="15cb9-121">Чтобы узнать текущее состояние настроек общедоступной CDN для клиента, поочередно выполните указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="15cb9-121">Get current status of public CDN settings from tenant level by executing following commands one-by-one.</span></span> 
```
Get-SPOTenantCdnEnabled -CdnType Public
Get-SPOTenantCdnOrigins -CdnType Public
Get-SPOTenantCdnPolicies -CdnType Public
```
<span data-ttu-id="15cb9-122">Включите общедоступную сеть доставки содержимого в клиенте.</span><span class="sxs-lookup"><span data-stu-id="15cb9-122">Enable public CDN in the tenant</span></span>
```
Set-SPOTenantCdnEnabled -CdnType Public
```
<span data-ttu-id="15cb9-123">Чтобы подтвердить настройки, введите "Y" и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="15cb9-123">Confirm settings by selecting 'Y' and pressing **Enter**</span></span>

![Включение общедоступной сети доставки содержимого в клиенте](../../../images/cdn-enable-o365-public-cdn.png)

<span data-ttu-id="15cb9-p104">Теперь в клиенте включена общедоступная CDN с использованием разрешенной конфигурации типов файлов по умолчанию. Это означает, что поддерживаются следующие типы файлов: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, WOFF.</span><span class="sxs-lookup"><span data-stu-id="15cb9-p104">Now public CDN has been enabled in the tenant using the default file type configuration allowed. This means that the following file type extensions are supported: "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF".</span></span>

<span data-ttu-id="15cb9-127">Решения SharePoint Framework могут автоматически использовать общедоступную сеть CDN Office 365, если она включена в клиенте.</span><span class="sxs-lookup"><span data-stu-id="15cb9-127">SharePoint Framework solutions can automatically benefit from the Office 365 Public CDN as long as it's enabled in your tenant.</span></span> <span data-ttu-id="15cb9-128">Если сеть CDN включена, источник `*/CLIENTSIDEASSETS` автоматически добавляется как допустимый.</span><span class="sxs-lookup"><span data-stu-id="15cb9-128">When CDN is enabled, `*/CLIENTSIDEASSETS` origin is automatically added as valid a valid origin.</span></span>

> [!NOTE]
> <span data-ttu-id="15cb9-129">Если вы уже включали общедоступную сеть доставки содержимого Office 365, ее следует заново включить, чтобы запись `*/CLIENTSIDEASSETS` была добавлена как допустимый источник общедоступной сети CDN.</span><span class="sxs-lookup"><span data-stu-id="15cb9-129">If you have previously enabled Office 365 CDN, you should re-enable the public CDN, so that you will have the `*/CLIENTSIDEASSETS`entry added as valid CDN origin for public CDN.</span></span>

<span data-ttu-id="15cb9-130">Вы можете проверить текущую конфигурацию конечных точек. Выполните приведенную ниже команду, чтобы получить список источников сетей CDN из клиента.</span><span class="sxs-lookup"><span data-stu-id="15cb9-130">You can double check the current setup of your end-points.Execute the following command to get the list of CDN origins from your tenant</span></span>
```
Get-SPOTenantCdnOrigins -CdnType Public
```
<span data-ttu-id="15cb9-p106">Обратите внимание, что новый источник указан как допустимый источник CDN. Настройка источника займет некоторое время (приблизительно 15 минут), поэтому мы пока можем создать тестовую веб-часть, которая будет размещена в источнике, когда развертывание будет завершено.</span><span class="sxs-lookup"><span data-stu-id="15cb9-p106">Notice that your newly added origin is listed as a valid CDN origin. Final configuration of the origin will take a while (approximately 15 minutes), so we can continue by creating your test web part, which will be hosted from the origin, when the deployment is completed.</span></span> 

![Список общедоступных источников в клиенте](../../../images/cdn-public-origins.png)

> [!NOTE]
> <span data-ttu-id="15cb9-134">Если рядом с названием источника нет уведомления о *настройке в состоянии ожидания*, он готов к использованию в клиенте.</span><span class="sxs-lookup"><span data-stu-id="15cb9-134">When origin is listed without the *(configuration pending)* text, it is ready to be used in your tenant.</span></span> <span data-ttu-id="15cb9-135">Это означает, что выполняется настройка SharePoint Online и системы CDN.</span><span class="sxs-lookup"><span data-stu-id="15cb9-135">This is the indication of an on-going configuration between SharePoint Online and CDN system.</span></span> 


## <a name="project-directory"></a><span data-ttu-id="15cb9-136">Каталог проекта</span><span class="sxs-lookup"><span data-stu-id="15cb9-136">Project directory</span></span>

<span data-ttu-id="15cb9-137">Переключитесь на консоль и убедитесь, что по-прежнему выбран каталог проекта, который использовался для настройки проекта веб-части.</span><span class="sxs-lookup"><span data-stu-id="15cb9-137">Switch to console and make sure you are still in the project directory you used to set up your web part project.</span></span>

<span data-ttu-id="15cb9-138">Завершите задачу **gulp serve** (если она выполняется), нажав клавиши **CTRL+C**, и убедитесь, что выбран каталог проекта:</span><span class="sxs-lookup"><span data-stu-id="15cb9-138">End the possible **gulp serve** task by choosing **Ctrl+C** and ensure that you are in your project directory:</span></span>

```
cd helloworld-webpart
```

# <a name="review-solution-settings"></a><span data-ttu-id="15cb9-139">Проверка параметров решения</span><span class="sxs-lookup"><span data-stu-id="15cb9-139">Review solution settings</span></span> 

<span data-ttu-id="15cb9-140">Откройте проект веб-части **HelloWorldWebPart** в Visual Studio Code или другой среде IDE.</span><span class="sxs-lookup"><span data-stu-id="15cb9-140">Open the **HelloWorldWebPart** web part project in Visual Studio Code, or your preferred IDE.</span></span>

<span data-ttu-id="15cb9-141">Откройте файл **package-solution.json** в папке **config**.</span><span class="sxs-lookup"><span data-stu-id="15cb9-141">Open **package-solution.json** from the **config** folder.</span></span>

<span data-ttu-id="15cb9-142">В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="15cb9-142">The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

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

<span data-ttu-id="15cb9-143">По умолчанию для параметра **includeClientSideAssets** задано значение `true`. Это означает, что статические ресурсы автоматически упаковываются в *SPPKG*-файлы, а ресурсы не требуется отдельно размещать во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="15cb9-143">Default value for the **includeClientSideAssets** is `true`, which means that static assets are packaged automatically inside of the *.sppkg* files and you do not need to separately host your assets from external system.</span></span> 

<span data-ttu-id="15cb9-144">Если *сеть доставки содержимого Office 365* включена, она будет автоматически использоваться с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="15cb9-144">If *Office 365 CDN* is enabled, it will be used automatically with default settings.</span></span> <span data-ttu-id="15cb9-145">Если *сеть доставки содержимого Office 365* не включена, ресурсы будут предоставляться из семейства веб-сайтов с каталогом приложений.</span><span class="sxs-lookup"><span data-stu-id="15cb9-145">If *Office 365 CDN* is not enabled, assets will be served from app catalog site collection.</span></span> 

> [!NOTE]
> <span data-ttu-id="15cb9-146">Начиная с SharePoint Framework версии 1.4, статические ресурсы по умолчанию упаковываются в SPPKG-файлы.</span><span class="sxs-lookup"><span data-stu-id="15cb9-146">Starting from the SharePoint Framework v1.4, static assets are by default packaged inside of the sppkg package.</span></span> <span data-ttu-id="15cb9-147">При развертывании пакета в каталоге приложений он автоматически размещается в сети CDN Office 365 (если она включена) или по URL-адресу каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="15cb9-147">When package is deployed in app catalog, they are automatically being hosted either from Office 365 CDN (if enabled) or from app catalog URL.</span></span> <span data-ttu-id="15cb9-148">Вы можете управлять этим поведением с помощью параметра `includeClientSideAssets` в файле `package-solution.json`.</span><span class="sxs-lookup"><span data-stu-id="15cb9-148">You can control this behavior with the `includeClientSideAssets` setting in `package-solution.json` file.</span></span>

## <a name="prepare-web-part-assets-to-deploy"></a><span data-ttu-id="15cb9-149">Подготовка ресурсов веб-части к развертыванию</span><span class="sxs-lookup"><span data-stu-id="15cb9-149">Prepare web part assets to deploy</span></span>

<span data-ttu-id="15cb9-150">Выполните приведенные ниже задачи, чтобы упаковать решение.</span><span class="sxs-lookup"><span data-stu-id="15cb9-150">Execute the following tasks to bundle your solution</span></span>
* <span data-ttu-id="15cb9-151">При этом будет выполнена сборка выпуска проекта с использованием динамической метки в качестве URL-адреса для размещения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="15cb9-151">This will execute a release build of your project by using a dynamic label as the host URL for your assets.</span></span> <span data-ttu-id="15cb9-152">Этот URL-адрес будет автоматически обновляться в соответствии с параметрами CDN, заданными для клиента.</span><span class="sxs-lookup"><span data-stu-id="15cb9-152">This URL will be automatically updated based on your tenant CDN settings.</span></span>

```
gulp bundle --ship
```

<span data-ttu-id="15cb9-153">Выполните указанную ниже задачу, чтобы упаковать решение.</span><span class="sxs-lookup"><span data-stu-id="15cb9-153">Execute the following task to package your solution</span></span>

```
gulp package-solution --ship
```

<span data-ttu-id="15cb9-154">Эта команда создаст обновленный пакет **helloworld-webpart.sppkg** в папке **sharepoint/solution**.</span><span class="sxs-lookup"><span data-stu-id="15cb9-154">This command will create an updated **helloworld-webpart.sppkg** package on the **sharepoint/solution** folder.</span></span>

> [!NOTE]
> <span data-ttu-id="15cb9-155">Если вам интересно, какие именно ресурсы упаковываются в SPPKG-файл, ознакомьтесь с содержимым папки **sharepoint/solution/debug**.</span><span class="sxs-lookup"><span data-stu-id="15cb9-155">If you are interested on what actually got packaged inside of the sppkg file, you can have a look omn the content of the **sharepoint/solution/debug** folder.</span></span>

<span data-ttu-id="15cb9-156">Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте.</span><span class="sxs-lookup"><span data-stu-id="15cb9-156">Upload or drag & drop the newly created client-side solution package to the app catalog in your tenant.</span></span> 

<span data-ttu-id="15cb9-157">Так как вы уже развернули пакет, вам будет предложено заменить существующий пакет.</span><span class="sxs-lookup"><span data-stu-id="15cb9-157">Because you already  deployed the package, you will be prompted as to whether to replace the existing package.</span></span>

![Переопределение существующего решения](../../../images/cdn-override-helloworld-webpart-package.png)

<span data-ttu-id="15cb9-159">Нажмите "Заменить".</span><span class="sxs-lookup"><span data-stu-id="15cb9-159">Choose Replace it.</span></span>

![Всплывающее окно при установке решения SPFx в каталоге приложений](../../../images/cnd-trust-helloworld-webpart-solution.png)

<span data-ttu-id="15cb9-161">Обратите внимание, что в списке **доменов** указана среда *SharePoint Online*.</span><span class="sxs-lookup"><span data-stu-id="15cb9-161">Notice how the **domain** list in the prompt is saying *SharePoint Online*.</span></span> <span data-ttu-id="15cb9-162">Это вызвано тем, что контент предоставляется либо из сети CDN Office 365, либо из каталога приложений (в зависимости от параметров клиента).</span><span class="sxs-lookup"><span data-stu-id="15cb9-162">This is since the content is either served from the Office 365 CDN or from app catalog, depending on the tenant settings.</span></span>

<span data-ttu-id="15cb9-163">Нажмите кнопку **Развернуть**</span><span class="sxs-lookup"><span data-stu-id="15cb9-163">Choose **Deploy**</span></span>

<span data-ttu-id="15cb9-164">Откройте сайт, где ранее было установлено решение **helloworld-webpart-client-side-solution**, или установите решение на новом сайте.</span><span class="sxs-lookup"><span data-stu-id="15cb9-164">Open a site where previously installed the **helloworld-webpart-client-side-solution** solution or install solution to a new site.</span></span>

<span data-ttu-id="15cb9-165">Когда решение будет установлено, в меню со значком *шестеренки* выберите пункт **Добавление страницы**, затем в окне выбора веб-частей для современной страницы нажмите **HelloWorld**, чтобы добавить настраиваемую веб-часть на страницу.</span><span class="sxs-lookup"><span data-stu-id="15cb9-165">After the solution has been installed, chose **Add a page** from the *gear* menu and pick **HelloWorld** from the modern page web part picker</span></span>

![Веб-часть HelloWorld в средстве выбора веб-частей для современной страницы](../../../images/cdn-web-part-picker.png)

<span data-ttu-id="15cb9-167">Обратите внимание: веб-часть отображается, несмотря на то что служба node.js не запущена локально.</span><span class="sxs-lookup"><span data-stu-id="15cb9-167">Notice how the web part is rendered even though you are not running the node.js service locally.</span></span> 

![Веб-часть HelloWorld на современной странице в режиме редактирования](../../../images/cdn-web-part-rendering.png)

<span data-ttu-id="15cb9-169">Сохраните изменения на странице с веб-частью.</span><span class="sxs-lookup"><span data-stu-id="15cb9-169">Save changes on the page with web part on it.</span></span>

<span data-ttu-id="15cb9-170">Нажмите клавишу **F12**, чтобы открыть инструменты разработчика.</span><span class="sxs-lookup"><span data-stu-id="15cb9-170">Press **F12** to open up developer tools.</span></span>

<span data-ttu-id="15cb9-171">Разверните узел **publiccdn.sharepointonline.com** в источнике и обратите внимание, что файл **hello-world-web-part** загружается с URL-адреса общедоступной сети доставки содержимого, динамически указывающего на библиотеку, расположенную в семействе веб-сайтов каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="15cb9-171">Extend **publiccdn.sharepointonline.com** under the source and notice how the **hello-world-web-part** file is loaded from the Public CDN URL pointing dynamically to a library located under the app catalog site collection.</span></span>

![Пакет веб-части HelloWorld из общедоступной сети CDN по указанному URL-адресу на вкладке "Источники" в области инструментов разработчика Chrome](../../../images/cdn-web-part-f12-source.png)

> [!NOTE]
> <span data-ttu-id="15cb9-173">Если в вашем клиенте не включена сеть CDN, а в файле **package-solution.json** для параметра `includeClientSideAssets` задано значение `true`, то URL-адрес для загрузки ресурсов будет динамически обновляться и указывать непосредственно на папку ClientSideAssets, расположенную в семействе веб-сайтов с каталогом приложений.</span><span class="sxs-lookup"><span data-stu-id="15cb9-173">If you would not have CDN enabled in your tenant and the `includeClientSideAssets` setting would be `true`in the **package-solution.json**, loading URL for the assets would be dynamically updated and pointing directly to the ClientSideAssets folder located in the app catalog site collection.</span></span> <span data-ttu-id="15cb9-174">В данном случае используется URL-адрес `https://sppnp.microsoft.com/sites/apps/ClientSideAssets/`.</span><span class="sxs-lookup"><span data-stu-id="15cb9-174">In this example case, URL would be `https://sppnp.microsoft.com/sites/apps/ClientSideAssets/`.</span></span>

<span data-ttu-id="15cb9-175">Поздравляем! Вы развернули веб-часть в SharePoint Online, автоматически разместив ее в сети доставки содержимого Office 365.</span><span class="sxs-lookup"><span data-stu-id="15cb9-175">Now you have deployed your custom web part to SharePoint Online and it's being hosted from the Office 365 CDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15cb9-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="15cb9-176">Next steps</span></span>

<span data-ttu-id="15cb9-177">Вы можете загрузить jQuery и jQuery UI, а затем собрать веб-часть jQuery Accordion.</span><span class="sxs-lookup"><span data-stu-id="15cb9-177">You can load jQuery, jQuery UI and build a jQuery Accordion web part.</span></span> <span data-ttu-id="15cb9-178">Дальнейшие указания см. в статье [Добавление элемента "аккордеон" jQueryUI в клиентскую веб-часть](./add-jqueryui-accordion-to-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="15cb9-178">To continue, see [Add jQueryUI Accordion to your client-side web part](./add-jqueryui-accordion-to-web-part.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15cb9-179">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="15cb9-179">If you find an issue in the documentation or in the SharePoint Framework, please report that to SharePoint engineering using the [issue list at sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="15cb9-180">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="15cb9-180">Thanks for your input advance.</span></span>