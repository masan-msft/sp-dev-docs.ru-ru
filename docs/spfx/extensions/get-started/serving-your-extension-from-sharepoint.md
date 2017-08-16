
# <a name="deploy-your-extension-to-sharepoint-hello-world-part-3"></a><span data-ttu-id="723db-101">Развертывание расширения в SharePoint (Hello World, часть 3)</span><span class="sxs-lookup"><span data-stu-id="723db-101">Deploy your extension to SharePoint (Hello world part 3)</span></span>

><span data-ttu-id="723db-p101">**Примечание.** Расширения для платформы SharePoint Framework находятся на этапе тестирования и могут меняться. В настоящее время расширения SharePoint Framework невозможно использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="723db-p101">**Note:** The SharePoint Framework Extensions are currently in preview and are subject to change. SharePoint Framework Extensions are not currently supported for use in production environments.</span></span>

<span data-ttu-id="723db-p102">Из этой статьи вы узнаете, как развернуть настройщик приложений SharePoint Framework в SharePoint и использовать его на современных страницах SharePoint. Это продолжение статьи о создании расширения Hello World: [Использование заполнителей страниц в настройщике приложений (Hello World, часть 2)](./using-page-placeholder-with-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="723db-p102">In this article, you will learn how to deploy your SharePoint Framework Application Customizer to SharePoint and see it working on modern SharePoint pages. This article continues with the hello world extension built in the previous article [Using page placeholders from Application Customizer (Hello World part 2)](./using-page-placeholder-with-extensions.md).</span></span>

<span data-ttu-id="723db-106">Перед началом работы убедитесь, что вы выполнили процедуры, описанные в предыдущих статьях:</span><span class="sxs-lookup"><span data-stu-id="723db-106">Be sure you have completed the procedures in the following articles before you begin:</span></span>

* [<span data-ttu-id="723db-107">Создание первого расширения SharePoint Framework (Hello World, часть 1)</span><span class="sxs-lookup"><span data-stu-id="723db-107">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="723db-108">Использование заполнителей страниц в настройщике приложений (Hello World, часть 2)</span><span class="sxs-lookup"><span data-stu-id="723db-108">Using page placeholders from Application Customizer (Hello World part 2)</span></span>](./using-page-placeholder-with-extensions.md)

## <a name="package-the-helloworld-application-customizer"></a><span data-ttu-id="723db-109">Упаковка настройщика приложений helloWorld</span><span class="sxs-lookup"><span data-stu-id="723db-109">Package the helloWorld Application Customizer</span></span>
<span data-ttu-id="723db-110">В окне консоли перейдите к каталогу проекта расширения, создание которого описывается в статье [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./build-a-hello-world-extension.md).</span><span class="sxs-lookup"><span data-stu-id="723db-110">In the console window, go to the extension project directory created in [Build your first SharePoint Framework Extension (Hello World part 1)](./build-a-hello-world-extension.md)</span></span>

```
cd app-extension
```
<span data-ttu-id="723db-111">Если команда gulp serve все еще выполняется, остановите ее с помощью клавиш `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="723db-111">If gulp serve is still running, stop it from running by pressing `Ctrl+C`.</span></span>

<span data-ttu-id="723db-p103">В отличие от режима **Отладка**, для использования расширения на современных серверных страницах SharePoint необходимо развернуть и зарегистрировать расширение для SharePoint в области `Site collection`, `Site` или `List`. Область определяет, где и как будет активироваться настройщик приложений. В этом конкретном случае мы зарегистрируем настройщик приложений в области `Site Collection`.</span><span class="sxs-lookup"><span data-stu-id="723db-p103">Unlike in **Debug** mode, in order to use an extension on modern SharePoint server-side pages, you need to deploy and register the extension with SharePoint in either `Site collection`, `Site`, or `List` scope. The scope defines where and how the Application Customizer will be active. In this particular scenario, we'll register the Application Customizer using the `Site Collection` scope.</span></span> 

<span data-ttu-id="723db-p104">Прежде чем упаковывать решение, нам нужно добавить необходимый для автоматической активации расширений на сайте код, который выполняется во время установки решения на сайте. В данном случае мы будем использовать элементы платформы компонентов для выполнения этих действий непосредственно в пакете решения, но вы также можете связать настройщик приложений с сайтом SharePoint с помощью REST или CSOM (например, во время подготовки сайта).</span><span class="sxs-lookup"><span data-stu-id="723db-p104">Before we package our solution, we want to include the code needed to automate the extension activation within the site, whenever the solution is installed on the site. In this case, we'll use feature framework elements to perform these actions directly in the solution package, but you could also associate the application customizer to a SharePoint site using REST or CSOM as part of the site provisioning, for example.</span></span>

1. <span data-ttu-id="723db-117">Установите пакет решения на нужном сайте, чтобы манифест расширения попал в список разрешенных для запуска.</span><span class="sxs-lookup"><span data-stu-id="723db-117">Install the solution package to the site where it should be installed, so that extension manifest is being white listed for execution</span></span>
2. <span data-ttu-id="723db-p105">Свяжите настройщик приложений с нужной областью. Это можно сделать программным способом (CSOM/REST) или с помощью платформы компонентов в пакете решения SharePoint Framework. Ниже перечислены свойства, которые необходимо связать с объектом `UserCustomAction` на уровне семейства веб-сайтов, сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="723db-p105">Associate the Application Customizer to the planned scope. This can be performed programmatically (CSOM/REST) or by using the feature framework inside of the SharePoint Framework solution package. You'll need to associate the following properties in the `UserCustomAction` object at the site collection, site or list level.</span></span>
    * <span data-ttu-id="723db-121">**ClientSiteComponentId:** — это идентификатор (GUID) настройщика приложений, установленного в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="723db-121">**ClientSiteComponentId:** This is the identifier (GUID) of the Field Customizer, which has been installed in the app catalog.</span></span> 
    * <span data-ttu-id="723db-122">**ClientSideComponentProperties:** — это необязательный параметр, с помощью которого можно предоставлять свойства для экземпляра настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="723db-122">**ClientSideComponentProperties:** This is an optional parameter, which can be used to provide properties for the Field Customizer instance</span></span>

> <span data-ttu-id="723db-p106">Обратите внимание, что в настоящее время необходимо явно устанавливать пакеты решений на сайтах, чтобы расширения выполнялись должным образом. В будущем появятся альтернативные способы достижения этой цели без отдельного развертывания на каждом сайте.</span><span class="sxs-lookup"><span data-stu-id="723db-p106">Notice. Currently you'll need to install solution packages explicitly to sites to ensure the extension is being properly executed. There will be alternative ways to achieve this in the future without site-by-site deployment.</span></span> 

<span data-ttu-id="723db-126">На следующих этапах мы создадим определение объекта `CustomAction`, которое затем будет автоматически развернуто с необходимыми параметрами при установке пакета решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="723db-126">In the following steps, we'll create a new `CustomAction` definition, which will then be automatically deployed with the needed configurations when the solution package is installed on a site.</span></span> 

<span data-ttu-id="723db-127">Вернитесь к пакету решения в Visual Studio Code (или другом редакторе, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="723db-127">Return to your solution package in Visual Studio Code (or to your preferred editor).</span></span>

<span data-ttu-id="723db-128">Для начала необходимо создать папку **assets**, в которую мы поместим все ресурсы платформы компонентов, используемые для подготовки структур SharePoint при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="723db-128">We'll first need to create an **assets** folder where we will place all feature framework assets used to provision SharePoint structures when the package is installed.</span></span>

* <span data-ttu-id="723db-129">Создайте папку **sharepoint** в корневой папке решения.</span><span class="sxs-lookup"><span data-stu-id="723db-129">Create a folder named **sharepoint** in the root of the solution</span></span>
* <span data-ttu-id="723db-130">Создайте папку **assets** в только что созданной папке **sharepoint**.</span><span class="sxs-lookup"><span data-stu-id="723db-130">Create a folder named **assets** as a sub folder of the just created **sharepoint** folder</span></span>

<span data-ttu-id="723db-131">Структура решения должна быть примерно такой, как на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="723db-131">Your solution structure should look similar to the following picture:</span></span>

![Папка assets в структуре решения](../../../../images/ext-app-assets-folder.png)

### <a name="add-an-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="723db-133">Добавление файла element.xml для определений SharePoint</span><span class="sxs-lookup"><span data-stu-id="723db-133">Add an elements.xml file for SharePoint definitions</span></span>

<span data-ttu-id="723db-134">Создайте в папке **sharepoint\assets** файл **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="723db-134">Create a new file inside the **sharepoint\assets** folder named **elements.xml**</span></span>

<span data-ttu-id="723db-p107">Скопируйте приведенную ниже структуру XML в файл **elements.xml**. Обязательно замените значение свойства **ClientSideComponentId** на уникальный идентификатор настройщика приложений, указанный в файле **HelloWorldApplicationCustomizer.manifest.json** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="723db-p107">Copy the following xml structure into **elements.xml**. Be sure to update the **ClientSideComponentId** property to the unique Id of your Application Customizer available in the **HelloWorldApplicationCustomizer.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="723db-p108">Мы также задаем **ClientSideComponentProperties** и передаем свойства JSON для этого экземпляра расширения. Обратите внимание, что JSON отменяется, чтобы мы могли задать его должным образом в атрибуте XML.</span><span class="sxs-lookup"><span data-stu-id="723db-p108">We also set the **ClientSideComponentProperties** and pass JSON properties for this extension instance. Notice how the JSON is escaped so that we can set it properly within an XML attribute.</span></span> 

<span data-ttu-id="723db-p109">Кроме того, обратите внимание, что мы используем расположение `ClientSideExtension.ApplicationCustomizer`, чтобы определить решение как настройщик приложений. По умолчанию этот файл **elements.xml** будет связан с компонентом уровня *Web*, поэтому объект `CustomAction` будет автоматически добавлен в коллекцию `Web.UserCustomAction` на сайте, где устанавливается решение.</span><span class="sxs-lookup"><span data-stu-id="723db-p109">Notice also that we use the specific location of `ClientSideExtension.ApplicationCustomizer` to define that this is an Application Customizer. Since by default this **elements.xml** will be associated to a *Web* scoped feature, this `CustomAction` will be automatically added to the `Web.UserCustomAction` collection in the site where the solution is being installed.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxApplicationCustomizer"
        Location="ClientSideExtension.ApplicationCustomizer"
        ClientSideComponentId="46606aa6-5dd8-4792-b017-1555ec0a43a4"
        ClientSideComponentProperties="{&quot;Header&quot;:&quot;Header area of the page&quot;,&quot;Footer&quot;:&quot;Footer area in the page&quot;}">

    </CustomAction>

</Elements>
```

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="723db-141">Проверка учета определений в конвейере сборки</span><span class="sxs-lookup"><span data-stu-id="723db-141">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="723db-p110">Откройте файл **package-solution.json** из папки **config**. В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода:</span><span class="sxs-lookup"><span data-stu-id="723db-p110">Open **package-solution.json** from the **config** folder. The **package-solution.json** file defines the package metadata as shown in the following code:</span></span>

```json
{
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "02d35a3e-5896-4664-874f-9fe9fdfe8408",
    "version": "1.0.0.0"
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}

```

<span data-ttu-id="723db-p111">Чтобы убедиться, что новый файл **element.xml** учитывается при упаковке решения, необходимо включить определение из платформы компонентов для пакета решения. Добавим определение JSON для нужного компонента в структуру решения, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="723db-p111">To ensure that our newly added **element.xml** file is taken into account while the solution is being packaged, we'll need to include a Feature Framework feature definition for the solution package. Let's include a JSON definition for the needed feature inside of the solution structure as demonstrated below.</span></span>

```json
{
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "02d35a3e-5896-4664-874f-9fe9fdfe8408",
    "version": "1.0.0.0",
    "features": [{
      "title": "Application Extension - Deployment of custom action.",
      "description": "Deploys a custom action with ClientSideComponentId association",
      "id": "456da147-ced2-3036-b564-8dad5c1c2e34",
      "version": "1.0.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ]
      }
    }]
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}

```

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="723db-146">Развертывание расширения в SharePoint Online и размещение кода JavaScript с локального узла</span><span class="sxs-lookup"><span data-stu-id="723db-146">Deploy the extension to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="723db-147">Теперь все готово для развертывания решения на сайте SharePoint и автоматического связывания с объектом `CustomAction` на уровне сайта.</span><span class="sxs-lookup"><span data-stu-id="723db-147">Now you are ready to deploy the solution to a SharePoint site and to have the `CustomAction` automatically associated on the site level.</span></span>

<span data-ttu-id="723db-148">Чтобы упаковать клиентское решение, содержащее расширение, и получить базовую структуру, готовую к упаковке, введите в окне консоли приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="723db-148">In the console window, enter the following command to package your client-side solution that contains the extension, so that we get the basic structure ready for packaging:</span></span>

```
gulp bundle
```

<span data-ttu-id="723db-149">Затем выполните следующую команду, чтобы создать пакет решения:</span><span class="sxs-lookup"><span data-stu-id="723db-149">Next, execute the following command so that the solution package is created:</span></span>

```
gulp package-solution
```

<span data-ttu-id="723db-150">Эта команда создаст пакет в папке **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="723db-150">The command will create the package in the **sharepoint/solution** folder:</span></span>

```
app-extension.sppkg
```

<span data-ttu-id="723db-151">Далее вам потребуется развернуть созданный пакет в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="723db-151">Next you need to deploy the package that was generated to the App Catalog.</span></span>

<span data-ttu-id="723db-152">Перейдите к **каталогу приложений** вашего клиента и откройте библиотеку **Приложения для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="723db-152">Go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

<span data-ttu-id="723db-p112">Отправьте или перетащите файл `app-extension.sppkg` из папки **sharepoint/solution** в каталог приложений. В SharePoint откроется диалоговое окно с предложением доверять клиентскому решению.</span><span class="sxs-lookup"><span data-stu-id="723db-p112">Upload or drag and drop the `app-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog. SharePoint will display a dialog and ask you to trust the client-side solution.</span></span>

<span data-ttu-id="723db-p113">Обратите внимание, что мы не обновляли URL-адреса для размещения решения в этом развертывании, чтобы URL-адрес по-прежнему указывал на `https://localhost:4321`. Нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="723db-p113">Notice that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to `https://localhost:4321`. Click the **Deploy** button.</span></span>

![Операция доверия при отправке в каталог приложений](../../../../images/ext-app-sppkg-deploy-trust.png)

<span data-ttu-id="723db-p114">Вернитесь к консоли и убедитесь, что решение запущено. Если это не так, выполните в папке решения следующую команду:</span><span class="sxs-lookup"><span data-stu-id="723db-p114">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>

```
gulp serve --nobrowser
```

<span data-ttu-id="723db-p115">Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения.</span><span class="sxs-lookup"><span data-stu-id="723db-p115">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

<span data-ttu-id="723db-162">Нажмите значок шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**, чтобы перейти к странице "Приложения".</span><span class="sxs-lookup"><span data-stu-id="723db-162">Choose the gear icon on the top navigation bar on the right and choose **Add an app** to go to your Apps page.</span></span>

<span data-ttu-id="723db-163">В поле **Поиск** введите **app** и нажмите клавишу *ВВОД*, чтобы отфильтровать приложения.</span><span class="sxs-lookup"><span data-stu-id="723db-163">In the **Search** box, enter '**app**' and press *Enter* to filter your apps.</span></span>

![Установка настройщика полей на сайте](../../../../images/ext-app-install-solution-to-site.png)

<span data-ttu-id="723db-p116">Выберите приложение **app-extension-client-side-solution**, чтобы установить его на сайте. По завершении установки обновите страницу, нажав клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="723db-p116">Choose the **app-extension-client-side-solution** app to install the solution on the site. When the installation is completed, refresh the page by pressing **F5**.</span></span>

<span data-ttu-id="723db-167">После успешной установки приложения верхний и нижний колонтитулы будут отрисовываться так же, как и при использовании параметров запроса отладки.</span><span class="sxs-lookup"><span data-stu-id="723db-167">When the application has been successfully installed, you can see the header and footer being rendered just like with the debug query parameters.</span></span>

![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a><span data-ttu-id="723db-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="723db-169">Next steps</span></span>

<span data-ttu-id="723db-p117">Поздравляем! Вы развернули расширение на современной странице SharePoint из каталога приложений! Вы можете продолжить создание расширения Hello World в следующей статье — [Размещение расширения из сети доставки содержимого Office 365 (Hello World, часть 4)](./hosting-extension-from-office365-cdn.md). Из нее вы узнаете, как развертывать ресурсы расширения в сети CDN, а не localhost, и загружать их из нее.</span><span class="sxs-lookup"><span data-stu-id="723db-p117">Congratulations, you have deployed an extension to a modern SharePoint page from the app catalog! You can continue building out your Hello World extension in the next topic, [Hosting extension from Office 365 CDN (Hello world part 4)](./hosting-extension-from-office365-cdn.md), where you will learn how to deploy and load the extension assets from a CDN instead of localhost.</span></span>
