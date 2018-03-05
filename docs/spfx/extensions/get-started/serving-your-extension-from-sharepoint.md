---
title: "Развертывание расширения в SharePoint (Hello World, часть 3)"
description: "Разверните настройщик заполнителей SharePoint Framework в SharePoint и проверьте, работает ли он на современных страницах SharePoint."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: be5d91493d9425f158755364947b84b02dbfb487
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="deploy-your-extension-to-sharepoint-hello-world-part-3"></a><span data-ttu-id="58349-103">Развертывание расширения в SharePoint (Hello World, часть 3)</span><span class="sxs-lookup"><span data-stu-id="58349-103">Deploy your extension to SharePoint (Hello World part 3)</span></span>

<span data-ttu-id="58349-104">В этой статье рассказывается, как развернуть настройщик заполнителей SharePoint Framework в SharePoint и проверить, работает ли он на современных страницах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="58349-104">This article describes how to deploy your SharePoint Framework Application Customizer to SharePoint and see it working on modern SharePoint pages.</span></span> 

<span data-ttu-id="58349-105">Перед началом работы необходимо выполнить процедуры, описанные в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="58349-105">Be sure you have completed the procedures in the following articles before you begin:</span></span>

* [<span data-ttu-id="58349-106">Создание первого расширения SharePoint Framework (Hello World, часть 1)</span><span class="sxs-lookup"><span data-stu-id="58349-106">Build your first SharePoint Framework Extension (Hello World part 1)</span></span>](./build-a-hello-world-extension.md)
* [<span data-ttu-id="58349-107">Использование заполнителей страниц из настройщика заполнителей (Hello World, часть 2)</span><span class="sxs-lookup"><span data-stu-id="58349-107">Use page placeholders from Application Customizer (Hello World part 2)</span></span>](./using-page-placeholder-with-extensions.md)

<span data-ttu-id="58349-108">Эти действия также показаны в видео на [канале SharePoint PnP на YouTube](https://www.youtube.com/watch?v=P_yWI0WVQIg&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span><span class="sxs-lookup"><span data-stu-id="58349-108">You can also follow these steps by watching the video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=P_yWI0WVQIg&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV).</span></span> 

<a href="https://www.youtube.com/watch?v=DzHdVxLA3Pc">
<img src="../../../images/spfx-ext-youtube-tutorial3.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="package-the-hello-world-application-customizer"></a><span data-ttu-id="58349-109">Упаковка настройщика заполнителей Hello World</span><span class="sxs-lookup"><span data-stu-id="58349-109">Package the Hello World Application Customizer</span></span>

1. <span data-ttu-id="58349-110">В окне консоли перейдите в каталог проекта расширения, созданного при работе со статьей [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./build-a-hello-world-extension.md).</span><span class="sxs-lookup"><span data-stu-id="58349-110">In the console window, go to the extension project directory created in [Build your first SharePoint Framework Extension (Hello World part 1)](./build-a-hello-world-extension.md).</span></span>

  ```
  cd app-extension
  ```

2. <span data-ttu-id="58349-111">Если команда gulp serve все еще выполняется, остановите ее, нажав клавиши CTRL+C.</span><span class="sxs-lookup"><span data-stu-id="58349-111">If gulp serve is still running, stop it from running by selecting Ctrl+C.</span></span>

  <span data-ttu-id="58349-112">В отличие от работы в режиме **отладки**, чтобы использовать расширение на современных серверных страницах SharePoint, вам потребуется развернуть и зарегистрировать расширение в SharePoint в области `Site collection`, `Site` или `List`.</span><span class="sxs-lookup"><span data-stu-id="58349-112">Unlike in **Debug** mode, to use an extension on modern SharePoint server-side pages, you need to deploy and register the extension with SharePoint in `Site collection`, `Site`, or `List` scope.</span></span> <span data-ttu-id="58349-113">Место и способ активации настройщика определяются областью.</span><span class="sxs-lookup"><span data-stu-id="58349-113">The scope defines where and how the Application Customizer is active.</span></span> <span data-ttu-id="58349-114">В данном сценарии мы зарегистрируем настройщик заполнителей, используя область `Site collection`.</span><span class="sxs-lookup"><span data-stu-id="58349-114">In this particular scenario, we'll register the Application Customizer by using the `Site collection` scope.</span></span> 

  <span data-ttu-id="58349-115">Прежде чем упаковать решение, нам необходимо включить код для автоматизации активации решения при установке его на сайте.</span><span class="sxs-lookup"><span data-stu-id="58349-115">Before we package our solution, we want to include the code needed to automate the extension activation within the site whenever the solution is installed on the site.</span></span> <span data-ttu-id="58349-116">В данном случае мы воспользуемся элементами платформы компонентов, чтобы выполнить эти действия прямо в пакете решения, но вы, например, можете связать настройщик заполнителей с сайтом SharePoint, используя REST или CSOM при подготовке сайта к работе.</span><span class="sxs-lookup"><span data-stu-id="58349-116">In this case, we'll use feature framework elements to perform these actions directly in the solution package, but you could also associate the Application Customizer to a SharePoint site by using REST or CSOM as part of the site provisioning, for example.</span></span>

3. <span data-ttu-id="58349-117">Установите пакет решения на нужном сайте, чтобы манифест расширения попал в список разрешенных для запуска.</span><span class="sxs-lookup"><span data-stu-id="58349-117">Install the solution package to the site where it should be installed so that the extension manifest is being white listed for execution.</span></span>

4. <span data-ttu-id="58349-118">Свяжите настройщик заполнителей с запланированной областью.</span><span class="sxs-lookup"><span data-stu-id="58349-118">Associate the Application Customizer to the planned scope.</span></span> <span data-ttu-id="58349-119">Это можно сделать с помощью кода (CSOM/REST) или с помощью платформы компонентов в пакете решения SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="58349-119">This can be performed programmatically (CSOM/REST) or by using the feature framework inside of the SharePoint Framework solution package.</span></span> <span data-ttu-id="58349-120">Указанные ниже свойства необходимо сопоставить в объекте `UserCustomAction` на уровне семейства веб-сайтов, сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="58349-120">You need to associate the following properties in the `UserCustomAction` object at the site collection, site, or list level.</span></span>
  
  * <span data-ttu-id="58349-121">**ClientSideComponentId**</span><span class="sxs-lookup"><span data-stu-id="58349-121">**ClientSideComponentId**.</span></span> <span data-ttu-id="58349-122">— идентификатор (GUID) настройщика полей, установленный в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="58349-122">This is the identifier (GUID) of the Field Customizer, which has been installed in the App Catalog.</span></span> 
  * <span data-ttu-id="58349-123">**ClientSideComponentProperties**</span><span class="sxs-lookup"><span data-stu-id="58349-123">**ClientSideComponentProperties**.</span></span> <span data-ttu-id="58349-124">— необязательный параметр, с помощью которого можно указать свойства для экземпляра настройщика полей.</span><span class="sxs-lookup"><span data-stu-id="58349-124">This is an optional parameter, which can be used to provide properties for the Field Customizer instance.</span></span>
   
  <span data-ttu-id="58349-125">Обратите внимание, что вы можете требовать добавления вашего расширения на сайт, используя параметр `skipFeatureDeployment` в файле **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="58349-125">Note that you can control the requirement to add a solution containing your extension to the site by using the `skipFeatureDeployment` setting in **package-solution.json**.</span></span> <span data-ttu-id="58349-126">Даже если вы не требуете установки решения на сайте, вам нужно связать идентификатор **ClientSideComponentId** с конкретными объектами, чтобы расширение было видимым.</span><span class="sxs-lookup"><span data-stu-id="58349-126">Even though you would not require the solution to be installed on the site, you need to associate **ClientSideComponentId** to specific objects for the extension to be visible.</span></span> 
   
  <span data-ttu-id="58349-127">На следующих этапах мы рассмотрим определение `CustomAction`, которое было автоматически создано для решения при формировании шаблонов для включения решения при его установке на сайте.</span><span class="sxs-lookup"><span data-stu-id="58349-127">In the following steps, we'll review the `CustomAction` definition, which was automatically created for the solution as part of the scaffolding for enabling the solution on a site when it's being installed.</span></span> 
   
5. <span data-ttu-id="58349-128">Вернитесь к пакету решения в Visual Studio Code (или другом редакторе, который вы используете).</span><span class="sxs-lookup"><span data-stu-id="58349-128">Return to your solution package in Visual Studio Code (or to your preferred editor).</span></span>

6. <span data-ttu-id="58349-129">Разверните папку **sharepoint** и вложенную папку **assets** в корневой папке решения. Отобразится существующий файл **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="58349-129">Extend the **sharepoint** folder and **assets** subfolder in the root of the solution to see the existing **elements.xml** file.</span></span> 

   ![Папка assets в структуре решения](../../../images/ext-app-assets-folder.png)

<br/>

### <a name="review-the-existing-elementsxml-file-for-sharepoint-definitions"></a><span data-ttu-id="58349-131">Проверка наличия определений SharePoint в существующем файле elements.xml</span><span class="sxs-lookup"><span data-stu-id="58349-131">Review the existing elements.xml file for SharePoint definitions</span></span>

<span data-ttu-id="58349-132">Проверьте существующую XML-структуру в файле **elements.xml**.</span><span class="sxs-lookup"><span data-stu-id="58349-132">Review the existing XML structure in the **elements.xml** file.</span></span> <span data-ttu-id="58349-133">Обратите внимание, что свойство **ClientSideComponentId** было автоматически обновлено на основании уникального идентификатора вашего настройщика заполнителей, доступного в файле **HelloWorldApplicationCustomizer.manifest.json** в папке **src\extensions\helloWorld**.</span><span class="sxs-lookup"><span data-stu-id="58349-133">Note that the **ClientSideComponentId** property has been automatically updated based on the unique ID of your Application Customizer available in the **HelloWorldApplicationCustomizer.manifest.json** file in the **src\extensions\helloWorld** folder.</span></span>

<span data-ttu-id="58349-134">Кроме того, для параметра **ClientSideComponentProperties** этого экземпляра расширения были автоматически заданы структура, используемая по умолчанию, и свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="58349-134">**ClientSideComponentProperties** has also been automatically set with the default structure and JSON properties for this extension instance.</span></span> <span data-ttu-id="58349-135">Запомните, как выполняется выход из объекта JSON, чтобы мы могли правильно настроить его в XML-атрибуте.</span><span class="sxs-lookup"><span data-stu-id="58349-135">Note how the JSON is escaped so that we can set it properly within an XML attribute.</span></span> 

<span data-ttu-id="58349-136">Для определения настройщика заполнителей в конфигурации используется конкретное расположение объекта `ClientSideExtension.ApplicationCustomizer`.</span><span class="sxs-lookup"><span data-stu-id="58349-136">The configuration uses the specific location of `ClientSideExtension.ApplicationCustomizer` to define that this is an Application Customizer.</span></span> <span data-ttu-id="58349-137">Так как по умолчанию этот файл **elements.xml** сопоставлен с компонентом с областью *Интернет*, это действие `CustomAction` будет автоматически добавлено в коллекцию `Web.UserCustomAction` на сайте, на котором устанавливается решение.</span><span class="sxs-lookup"><span data-stu-id="58349-137">Because this **elements.xml** is associated to a *Web* scoped feature by default, this `CustomAction` is automatically added to the `Web.UserCustomAction` collection in the site where the solution is being installed.</span></span>

<span data-ttu-id="58349-138">Чтобы конфигурация соответствовала обновлениям, выполненным в настройщике заполнителей, измените параметр **ClientSideComponentProperties**, как показано в XML-структуре ниже.</span><span class="sxs-lookup"><span data-stu-id="58349-138">To ensure that the configuration matches updates performed in the Application Customizer, update the **ClientSideComponentProperties** as in the following XML structure.</span></span> <span data-ttu-id="58349-139">Учтите, что вам не следует копировать всю структуру, так как это приведет к расхождению с идентификатором **ClientSideComponentId**.</span><span class="sxs-lookup"><span data-stu-id="58349-139">Note that you should not copy the whole structure because it would cause a mismatch with your **ClientSideComponentId**.</span></span>


```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">

    <CustomAction 
        Title="SPFxApplicationCustomizer"
        Location="ClientSideExtension.ApplicationCustomizer"
        ClientSideComponentId="46606aa6-5dd8-4792-b017-1555ec0a43a4"
        ClientSideComponentProperties="{&quot;Top&quot;:&quot;Top area of the page&quot;,&quot;Bottom&quot;:&quot;Bottom area in the page&quot;}">

    </CustomAction>

</Elements>
```

<br/>

### <a name="ensure-that-definitions-are-taken-into-account-within-the-build-pipeline"></a><span data-ttu-id="58349-140">Сделайте так, чтобы определения учитывались при упаковке</span><span class="sxs-lookup"><span data-stu-id="58349-140">Ensure that definitions are taken into account within the build pipeline</span></span>

<span data-ttu-id="58349-141">Откройте файл **package-solution.json** в папке **config**.</span><span class="sxs-lookup"><span data-stu-id="58349-141">Open **package-solution.json** from the **config** folder.</span></span> <span data-ttu-id="58349-142">В файле **package-solution.json** определяются метаданные пакета, как показано в следующем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="58349-142">The **package-solution.json** file defines the package metadata as shown in the following code.</span></span> <span data-ttu-id="58349-143">Чтобы при упаковке решения учитывался файл **element.xml**, функция формирования шаблонов, используемая по умолчанию, добавляет необходимую конфигурацию, чтобы создать определение компонента платформы компонентов для пакета решения.</span><span class="sxs-lookup"><span data-stu-id="58349-143">To ensure that the **element.xml** file is taken into account while the solution is being packaged, default scaffolding adds needed configuration to define a feature framework feature definition for the solution package.</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx-build/package-solution.schema.json",
  "solution": {
    "name": "app-extension-client-side-solution",
    "id": "98a9fe4f-175c-48c1-adee-63fb927faa70",
    "version": "1.0.0.0",
    "features": [
      {
        "title": "Application Extension - Deployment of custom action.",
        "description": "Deploys a custom action with ClientSideComponentId association",
        "id": "4678966b-de68-445f-a74e-e553a7b937ab",
        "version": "1.0.0.0",
        "assets": {
          "elementManifests": [
            "elements.xml"
          ]
        }
      }
    ]
  },
  "paths": {
    "zippedPackage": "solution/app-extension.sppkg"
  }
}


```

<br/>

## <a name="deploy-the-extension-to-sharepoint-online-and-host-javascript-from-local-host"></a><span data-ttu-id="58349-144">Развертывание расширения в SharePoint Online и размещение кода JavaScript в локальном узле</span><span class="sxs-lookup"><span data-stu-id="58349-144">Deploy the extension to SharePoint Online and host JavaScript from local host</span></span>

<span data-ttu-id="58349-145">Теперь мы готовы развернуть решение на сайте SharePoint и автоматически сопоставить действие `CustomAction` на уровне сайта.</span><span class="sxs-lookup"><span data-stu-id="58349-145">Now you are ready to deploy the solution to a SharePoint site and have the `CustomAction` automatically associated on the site level.</span></span>

1. <span data-ttu-id="58349-146">Чтобы упаковать клиентское решение, содержащее расширение, и получить базовую структуру, готовую к упаковке, в окне консоли введите указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="58349-146">In the console window, enter the following command to package your client-side solution that contains the extension so that we get the basic structure ready for packaging:</span></span>

   ```
   gulp bundle
   ```

2. <span data-ttu-id="58349-147">Затем выполните следующую команду, чтобы создать пакет решения:</span><span class="sxs-lookup"><span data-stu-id="58349-147">Execute the following command so that the solution package is created:</span></span>

   ```
   gulp package-solution
   ```

   <span data-ttu-id="58349-148">Эта команда создает пакет в папке **sharepoint/solution**:</span><span class="sxs-lookup"><span data-stu-id="58349-148">The command creates the package in the **sharepoint/solution** folder:</span></span>

   ```
   app-extension.sppkg
   ```

3. <span data-ttu-id="58349-149">Теперь необходимо развернуть пакет, созданный в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="58349-149">You now need to deploy the package that was generated to the App Catalog.</span></span> <span data-ttu-id="58349-150">Для этого перейдите в **каталог приложений** клиента и откройте библиотеку **Приложения для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="58349-150">To do this, go to your tenant's **App Catalog** and open the **Apps for SharePoint** library.</span></span>

4. <span data-ttu-id="58349-151">Отправьте или перетащите файл `app-extension.sppkg` из папки **sharepoint/solution** в каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="58349-151">Upload or drag and drop the `app-extension.sppkg` located in the **sharepoint/solution** folder to the App Catalog.</span></span> <span data-ttu-id="58349-152">В SharePoint откроется диалоговое окно с запросом на подтверждение доверия клиентскому решению.</span><span class="sxs-lookup"><span data-stu-id="58349-152">SharePoint displays a dialog and asks you to trust the client-side solution.</span></span>

   <span data-ttu-id="58349-153">Обратите внимание, что мы не изменяли URL-адреса для размещения решения в этом развертывании, поэтому по-прежнему используется URL-адрес `https://localhost:4321`.</span><span class="sxs-lookup"><span data-stu-id="58349-153">Note that we did not update the URLs for hosting the solution for this deployment, so the URL is still pointing to `https://localhost:4321`.</span></span> 
   
5. <span data-ttu-id="58349-154">Нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="58349-154">Select the **Deploy** button.</span></span>

   ![Операция доверия при отправке в каталог приложений](../../../images/ext-app-sppkg-deploy-trust.png)

6. <span data-ttu-id="58349-p114">Вернитесь к консоли и убедитесь, что решение запущено. Если это не так, выполните в папке решения следующую команду:</span><span class="sxs-lookup"><span data-stu-id="58349-p114">Move back to your console and ensure that the solution is running. If it's not running, execute the following command in the solution folder:</span></span>
   
   ```
   gulp serve --nobrowser
   ```
   
7. <span data-ttu-id="58349-p115">Перейдите на тот сайт, где требуется проверить подготовку ресурсов SharePoint. Это может быть любое семейство веб-сайтов в клиенте, где развернут пакет решения.</span><span class="sxs-lookup"><span data-stu-id="58349-p115">Go to the site where you want to test SharePoint asset provisioning. This could be any site collection in the tenant where you deployed this solution package.</span></span>

8. <span data-ttu-id="58349-160">Щелкните значок с изображением шестеренки на верхней панели навигации справа и выберите команду **Добавить приложение**. Откроется страница "Приложения".</span><span class="sxs-lookup"><span data-stu-id="58349-160">Select the gear icon on the top navigation bar on the right, and then select **Add an app** to go to your Apps page.</span></span>

9. <span data-ttu-id="58349-161">В поле **Поиск** введите **app**, а затем нажмите клавишу ВВОД, чтобы отфильтровать приложения.</span><span class="sxs-lookup"><span data-stu-id="58349-161">In the **Search** box, enter **app**, and then select Enter to filter your apps.</span></span>

   ![Установка настройщика полей на сайте](../../../images/ext-app-install-solution-to-site.png)

10. <span data-ttu-id="58349-163">Выберите приложение **app-extension-client-side-solution**, чтобы установить решение на сайте.</span><span class="sxs-lookup"><span data-stu-id="58349-163">Select the **app-extension-client-side-solution** app to install the solution on the site.</span></span> <span data-ttu-id="58349-164">После завершения установки обновите страницу, нажав клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="58349-164">When the installation is completed, refresh the page by selecting F5.</span></span>

  <span data-ttu-id="58349-165">После установки приложения верхний и нижний колонтитулы будут отрисовываться так же, как и при использовании параметров запроса отладки.</span><span class="sxs-lookup"><span data-stu-id="58349-165">When the application has been successfully installed, you can see the header and footer being rendered just like with the debug query parameters.</span></span>

  ![Пользовательские элементы верхнего и нижнего колонтитулов на странице](../../../images/ext-app-header-footer-visible.png)

## <a name="next-steps"></a><span data-ttu-id="58349-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58349-167">Next steps</span></span>

<span data-ttu-id="58349-168">Поздравляем, вы развернули расширение из каталога приложений на современной странице SharePoint!</span><span class="sxs-lookup"><span data-stu-id="58349-168">Congratulations, you have deployed an extension to a modern SharePoint page from the app catalog!</span></span> 

<span data-ttu-id="58349-169">Из следующей статьи [Размещение расширения в сети доставки содержимого Office 365 (Hello World, часть 4)](./hosting-extension-from-office365-cdn.md) вы узнаете, как развернуть ресурсы расширения в сети CDN и загружать их оттуда.</span><span class="sxs-lookup"><span data-stu-id="58349-169">You can continue building out your Hello World extension in the next topic, [Host extension from Office 365 CDN (Hello World part 4)](./hosting-extension-from-office365-cdn.md), where you learn how to deploy and load the extension assets from a CDN instead of from localhost.</span></span>

> [!NOTE]
> <span data-ttu-id="58349-170">Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="58349-170">If you find an issue in the documentation or in the SharePoint Framework, report that to SharePoint engineering by using the [issue list at the sp-dev-docs repository](https://github.com/SharePoint/sp-dev-docs/issues).</span></span> <span data-ttu-id="58349-171">Заранее спасибо!</span><span class="sxs-lookup"><span data-stu-id="58349-171">Thanks for your input in advance.</span></span>
