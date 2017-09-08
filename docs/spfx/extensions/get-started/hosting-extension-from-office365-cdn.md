# <a name="hosting-extension-from-office-365-cdn-hello-world-part-4"></a><span data-ttu-id="85ce3-101">Размещение расширения из сети доставки содержимого Office 365 (Hello World, часть 4)</span><span class="sxs-lookup"><span data-stu-id="85ce3-101">Hosting extension from Office 365 CDN (Hello world part 4)</span></span>

><span data-ttu-id="85ce3-p101">**Примечание.** Расширения для платформы SharePoint Framework находятся на этапе тестирования и могут меняться. В настоящее время расширения SharePoint Framework невозможно использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="85ce3-p102">Из этой статьи вы узнаете, как развернуть настройщик приложений SharePoint Framework для размещения из сети доставки содержимого Office 365, а затем в SharePoint для пользователей. Это продолжение серии статей о расширении Hello World. В предыдущей статье — [Развертывание расширения в SharePoint (Hello World, часть 3)](./using-page-placeholder-with-extensions.md) — описывалось размещение настройщика из localhost.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p102">In this article, you will learn how to deploy your SharePoint Framework Application Customizer to be hosted from an Office 365 CDN and how to deploy that to SharePoint for the end users. This article continues with the hello world extension built in the previous article [# Deploy your extension to SharePoint (Hello world part 3)](./using-page-placeholder-with-extensions.md) where we were still hosting the customizer from localhost.</span></span>

<span data-ttu-id="85ce3-106">Перед началом работы убедитесь, что вы выполнили процедуры, описанные в предыдущих статьях:</span><span class="sxs-lookup"><span data-stu-id="85ce3-106">Be sure you have completed the procedures in the following articles before you start:</span></span>

* [<span data-ttu-id="85ce3-107">Создание первого расширения SharePoint Framework (Hello World, часть 1)</span><span class="sxs-lookup"><span data-stu-id="85ce3-107">Build your first SharePoint Framework Extension (Hello world part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="85ce3-108">Подключение клиентской веб-части к SharePoint (Hello World, часть 2)</span><span class="sxs-lookup"><span data-stu-id="85ce3-108">Connect your client-side web part to SharePoint (Hello world part 2)</span></span>](./using-page-placeholder-with-extensions.md)
* [<span data-ttu-id="85ce3-109">Развертывание расширения в SharePoint (Hello World, часть 3)</span><span class="sxs-lookup"><span data-stu-id="85ce3-109">Deploy your extension to SharePoint (Hello world part 3)</span></span>](./serving-your-extension-from-sharepoint.md)

<span data-ttu-id="85ce3-110">Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="85ce3-110">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV">
<img src="../../../../images/spfx-ext-youtube-tutorial4.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="using-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="85ce3-111">Использование CDN в клиенте Office 365</span><span class="sxs-lookup"><span data-stu-id="85ce3-111">Using the CDN in your Office 365 tenant</span></span>
<span data-ttu-id="85ce3-112">Сеть доставки содержимого Office 365 — самый простой способ размещать решения SharePoint непосредственно из их клиента, пользуясь при этом преимуществами службы сетей доставки содержимого (CDN) для сокращения времени загрузки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="85ce3-112">Office 365 CDN is the easiest way to host SharePoint Framework solutions directly from your tenant while still taking advantage of the Content Delivery Network (CDN) service for faster load times of your assets.</span></span>

## <a name="enabling-the-cdn-in-your-office-365-tenant"></a><span data-ttu-id="85ce3-113">Включение CDN в клиенте Office 365</span><span class="sxs-lookup"><span data-stu-id="85ce3-113">Enabling the CDN in your Office 365 tenant</span></span>
<span data-ttu-id="85ce3-114">Скачайте последнюю версию командной консоли SharePoint Online на [сайте загрузки Майкрософт](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="85ce3-114">Ensure that you have latest version of the SharePoint Online Management Shell by downloading it from the [Microsoft Download site](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

<span data-ttu-id="85ce3-115">Подключитесь к клиенту SharePoint Online с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85ce3-115">Connect to your SharePoint Online tenant through PowerShell:</span></span>
```
Connect-SPOService -Url https://contoso-admin.sharepoint.com
```

<span data-ttu-id="85ce3-116">Чтобы узнать текущее состояние настроек общедоступной сети CDN для клиента, поочередно выполните указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="85ce3-116">Get the current status of public CDN settings from the tenant level by executing the following commands one-by-one.</span></span> 
```
Get-SPOTenantCdnEnabled -CdnType Public
Get-SPOTenantCdnOrigins -CdnType Public
Get-SPOTenantCdnPolicies -CdnType Public
```
<span data-ttu-id="85ce3-117">Включите общедоступную сеть доставки содержимого в клиенте.</span><span class="sxs-lookup"><span data-stu-id="85ce3-117">Enable public CDN in the tenant</span></span>
```
Set-SPOTenantCdnEnabled -CdnType Public
```
<span data-ttu-id="85ce3-p103">Теперь в клиенте включена общедоступная CDN с использованием разрешенной конфигурации типов файлов по умолчанию. Это означает, что поддерживаются следующие типы файлов: CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF, WOFF.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p103">Now public CDN has been enabled in the tenant using the default file type configuration allowed. This means that the following file type extensions are supported: "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF".</span></span>

<span data-ttu-id="85ce3-p104">Откройте браузер и перейдите к семейству веб-сайтов, в котором вы хотите разместить свою библиотеку CDN. Это может быть любое семейство веб-сайтов в клиенте. Это руководство описывает создание библиотеки CDN, но вы также можете использовать отдельную папку в любой существующей библиотеке документов как конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p104">Open up a browser and move to a site collection where you'd like to host your CDN library. This could be any site collection in your tenant. In this tutorial, we will create a specific library to act as your CDN library, but you can also use a specific folder in any existing document library as the CDN endpoint.</span></span>

<span data-ttu-id="85ce3-123">В семействе веб-сайтов создайте библиотеку документов **CDN** и добавьте в нее папку **helloworld**.</span><span class="sxs-lookup"><span data-stu-id="85ce3-123">Create a new document library on your site collection called **CDN** and add a folder named **helloworld** to it.</span></span>

![Папка helloworld-extension в библиотеке CDN](../../../../images/ext-app-cdn-folder-created.png) 

<span data-ttu-id="85ce3-p105">Вернитесь к консоли PowerShell и добавьте новый источник CDN. В этом случае мы задаем источник `*/cdn`, то есть в качестве источника CDN будет выступать любая относительная папка с именем **cdn**.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p105">Move back to the PowerShell console and add a new CDN origin. In this case, we are setting the origin as `*/cdn`, which means that any relative folder with the name of **cdn** will act as a CDN origin.</span></span>
```
Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
```
<span data-ttu-id="85ce3-127">Выполните указанную ниже команду, чтобы получить список источников CDN клиента.</span><span class="sxs-lookup"><span data-stu-id="85ce3-127">Execute the following command to get the list of CDN origins from your tenant</span></span>
```
Get-SPOTenantCdnOrigins -CdnType Public
```
<span data-ttu-id="85ce3-p106">Обратите внимание, что новый источник указан как допустимый источник CDN. Его настройка займет некоторое время (приблизительно 15 минут), поэтому мы пока можем создать тестовое расширение, которое будет размещено в источнике, когда развертывание завершится.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p106">Notice that your newly added origin is listed as a valid CDN origin. Final configuration of the origin will take a while (approximately 15 minutes), so we can continue creating your test extension, which will be hosted from the origin once deployment is completed.</span></span> 

![Список общедоступных источников в клиенте](../../../../images/ext-app-cdn-origins-pending.png)

> <span data-ttu-id="85ce3-p107">Если рядом с названием источника нет уведомления о *настройке в состоянии ожидания*, он готов к использованию в клиенте. Это указывает на выполняющуюся настройку SharePoint Online и системы CDN.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p107">When origin is listed without the *(configuration pending)* text, it is ready to be used in your tenant. This is the indication of an on-going configuration between SharePoint Online and the CDN system.</span></span> 

## <a name="updating-your-solution-project-for-the-cdn-urls"></a><span data-ttu-id="85ce3-133">Обновление проекта решения для URL-адресов CDN</span><span class="sxs-lookup"><span data-stu-id="85ce3-133">Updating your solution project for the CDN URLs</span></span>
<span data-ttu-id="85ce3-134">Вернитесь к ранее созданному решению, чтобы внести необходимые изменения в URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="85ce3-134">Return to the previously created solution to perform the needed URL updates.</span></span>
```
code .
```

<span data-ttu-id="85ce3-135">Обновите файл *write-manifestests.json* (в папке *config*), как показано ниже, чтобы он указывал на конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="85ce3-135">Update the *write-manifests.json* file (under the *config* folder) as follows to point to your CDN endpoint.</span></span> 

* <span data-ttu-id="85ce3-136">Укажите префикс publiccdn.sharepointonline.com и добавьте к URL-адресу путь в клиенте.</span><span class="sxs-lookup"><span data-stu-id="85ce3-136">You will need to use the publiccdn.sharepointonline.com as the prefix and then extend the URL with the actual path of your tenant</span></span>
* <span data-ttu-id="85ce3-137">Формат URL-адреса для сети доставки содержимого:</span><span class="sxs-lookup"><span data-stu-id="85ce3-137">Format of the CDN URL is as follows</span></span>

```
https://publiccdn.sharepointonline.com/<tenant host name>/sites/site/library/folder
```

![Путь к конечной точке CDN в манифесте записи](../../../../images/ext-app-cdn-write-manifest.png)

<span data-ttu-id="85ce3-139">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="85ce3-139">Save your changes.</span></span>

<span data-ttu-id="85ce3-140">Выполните приведенные ниже задачи для упаковки решения.</span><span class="sxs-lookup"><span data-stu-id="85ce3-140">Execute the following tasks to bundle your solution</span></span>

* <span data-ttu-id="85ce3-p108">При этом будет выполнена сборка конечной версии проекта с использованием URL-адреса CDN, указанного в файле **writer-manifest.json**. Результат выполнения команды будет помещен в папку **./temp/deploy**. Эти файлы вам нужно будет добавить в папку SharePoint, представляющую собой конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p108">This will execute a release build of your project using the CDN URL specified in the **write-manifests.json** file. The output of this command will be located in the **./temp/deploy** folder. These are the files which you will need to upload to the SharePoint folder acting as your CDN endpoint.</span></span> 

```
gulp bundle --ship
```

<span data-ttu-id="85ce3-144">Выполните указанную ниже задачу, чтобы упаковать свое решение.</span><span class="sxs-lookup"><span data-stu-id="85ce3-144">Execute the following task to package your solution</span></span>

```
gulp package-solution --ship
```

<span data-ttu-id="85ce3-145">Эта команда создаст пакет **app-extension.sppkg** в папке **sharepoint/solution**, а также подготовит ресурсы в папке **temp/deploy** к развертыванию в CDN.</span><span class="sxs-lookup"><span data-stu-id="85ce3-145">This command will create an **app-extension.sppkg** package in the **sharepoint/solution** folder and also prepare the assets in the **temp/deploy** folder to be deployed to the CDN.</span></span>

<span data-ttu-id="85ce3-p109">Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте. Нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="85ce3-p109">Upload or drag & drop the newly created client-side solution package to the app catalog in your tenant. Click the **Deploy** button.</span></span>

![Диалоговое окно доверия в каталоге приложений с путем к конечной точке CDN](../../../../images/ext-app-approve-cdn-address.png)

<span data-ttu-id="85ce3-149">Отправьте или перетащите файлы из папки **temp/deploy** в созданную ранее папку **CDN/helloworld**.</span><span class="sxs-lookup"><span data-stu-id="85ce3-149">Upload or drag & drop the files in the **temp/deploy** folder to the **CDN/helloworld** folder created earlier.</span></span>

<span data-ttu-id="85ce3-150">Установите новую версию решения на сайте и убедитесь, что она работает должным образом, если в *locahost* нет файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="85ce3-150">Install the new version of the solution to your site and ensure that it's working properly without your *locahost* hosting the JavaScript file.</span></span>

![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../../images/ext-app-header-footer-visible.png)

<span data-ttu-id="85ce3-152">Поздравляем! Вы включили общедоступную сеть CDN в клиенте Office 365 и воспользовались ею в решении!</span><span class="sxs-lookup"><span data-stu-id="85ce3-152">Congratulations, you have enabled a public CDN in your Office 365 tenant and taken advantage of it from your solution!</span></span>
