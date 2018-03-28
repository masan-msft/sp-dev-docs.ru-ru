---
title: Начало работы с веб-перехватчиками SharePoint
description: Узнайте, как создать приложение, которое добавляет и обрабатывает запросы веб-перехватчиков SharePoint.
ms.date: 03/14/2018
ms.prod: sharepoint
ms.openlocfilehash: 915ce825d017c08f6a1af4ef54e776951b7a5eed
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="get-started-with-sharepoint-webhooks"></a><span data-ttu-id="1caab-103">Начало работы с веб-перехватчиками SharePoint</span><span class="sxs-lookup"><span data-stu-id="1caab-103">Get started with SharePoint webhooks</span></span>

<span data-ttu-id="1caab-104">В этой статье описывается создание приложения, которое добавляет и обрабатывает запросы веб-перехватчиков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1caab-104">This article describes how to build an application that adds and handles SharePoint webhook requests.</span></span> <span data-ttu-id="1caab-105">Вы научитесь быстро составлять и выполнять запросы веб-перехватчиков SharePoint с помощью [клиента Postman](https://www.getpostman.com/), используя простой веб-API ASP.NET в качестве приемника веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="1caab-105">You will learn how to use [Postman client](https://www.getpostman.com/) to construct and execute SharePoint webhook requests quickly while interacting with a simple ASP.NET Web API as the webhook receiver.</span></span>

<span data-ttu-id="1caab-106">Мы будем использовать простые HTTP-запросы, чтобы вам было легче понять принцип работы веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="1caab-106">You will use plain HTTP requests, which is useful for helping you to understand how webhooks work.</span></span>  

<span data-ttu-id="1caab-107">Чтобы выполнить представленные в этой статье пошаговые инструкции, скачайте и установите следующие средства:</span><span class="sxs-lookup"><span data-stu-id="1caab-107">To complete the step-by-step instructions in this article, download and install the following tools:</span></span>

* [<span data-ttu-id="1caab-108">Браузер Google Chrome</span><span class="sxs-lookup"><span data-stu-id="1caab-108">Google Chrome Browser</span></span>](http://google.com/chrome)
* [<span data-ttu-id="1caab-109">Postman</span><span class="sxs-lookup"><span data-stu-id="1caab-109">Postman</span></span>](https://www.getpostman.com/)
* [<span data-ttu-id="1caab-110">Visual Studio Community Edition</span><span class="sxs-lookup"><span data-stu-id="1caab-110">Visual Studio Community Edition</span></span>](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)
* <span data-ttu-id="1caab-111">[ngrok](https://ngrok.com/) ([файл для скачивания и инструкции по установке](https://ngrok.com/download)).</span><span class="sxs-lookup"><span data-stu-id="1caab-111">[ngrok](https://ngrok.com/) (to install ngrok, see [Download and Installation](https://ngrok.com/download))</span></span>
* <span data-ttu-id="1caab-112">Подписка разработчика Office 365 с SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1caab-112">An Office 365 subscription with SharePoint Online.</span></span> <span data-ttu-id="1caab-113">Если вы только начинаете работу с Office 365, вы также можете [получить подписку по программе для разработчиков Office 365](https://developer.microsoft.com/ru-RU/office/dev-program).</span><span class="sxs-lookup"><span data-stu-id="1caab-113">If you are new to Office 365, you can also [sign up for an Office 365 developer account](https://developer.microsoft.com/ru-RU/office/dev-program).</span></span> <span data-ttu-id="1caab-114">Пошаговые инструкции по регистрации и настройке подписки см. в [документации по программе для разработчиков Office 365](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="1caab-114">See the [Office 365 Developer Program documentation](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program) for step-by-step instructions about how to join the Office 365 Developer Program and sign up and configure your subscription.</span></span>

## <a name="step-1-register-an-azure-ad-application-for-postman-client"></a><span data-ttu-id="1caab-115">Шаг 1. Регистрация приложения Azure AD для клиента Postman</span><span class="sxs-lookup"><span data-stu-id="1caab-115">Step 1: Register an Azure AD application for Postman client</span></span>

<span data-ttu-id="1caab-116">Чтобы клиент Postman мог взаимодействовать с SharePoint, необходимо зарегистрировать приложение Microsoft Azure Active Directory (Azure AD) в клиенте Azure AD, связанном с клиентом Office 365.</span><span class="sxs-lookup"><span data-stu-id="1caab-116">In order for the Postman client to communicate with SharePoint, you need to register a Microsoft Azure Active Directory (Azure AD) app in your Azure AD tenant associated with your Office 365 tenant.</span></span> 

1. <span data-ttu-id="1caab-117">Зарегистрируйте приложение как **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="1caab-117">Ensure that you register the application as a **Web Application**.</span></span>

2. <span data-ttu-id="1caab-118">Для доступа к SharePoint Online важно предоставить приложению Azure AD разрешения на доступ к приложению **Office 365 SharePoint Online** и выбрать разрешение **Чтение и запись элементов и списков во всех семействах веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="1caab-118">To access SharePoint Online, it's important to grant the Azure AD app permissions to the **Office 365 SharePoint Online** application and select the **read and write items and lists in all site collections** permission.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1caab-119">Дополнительные сведения о добавлении приложения Azure AD и предоставлении разрешений приложениям см. в разделе [Добавление приложения](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application).</span><span class="sxs-lookup"><span data-stu-id="1caab-119">For more information about adding an Azure AD application and granting permissions to applications, see [Adding an application](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application).</span></span> 

3. <span data-ttu-id="1caab-p103">Введите указанную ниже конечную точку в качестве URL-адреса ответа (перенаправления) для приложения. Это конечная точка, на которую Azure AD будет отправлять ответ на запрос аутентификации, в том числе маркер доступа при успешной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="1caab-p103">Enter the following endpoint as the Reply (Redirect) URL for the app. This is the endpoint to which Azure AD will send the authentication response, including the access token, if authentication was successful.</span></span>

    ```html
    https://www.getpostman.com/oauth2/callback
    ```

4. <span data-ttu-id="1caab-122">Создайте **Ключ**, который будет секретом клиента.</span><span class="sxs-lookup"><span data-stu-id="1caab-122">Generate a **Key**, which will be the client secret.</span></span>

5. <span data-ttu-id="1caab-123">Указанные ниже свойства пригодятся вам позже, поэтому скопируйте их в безопасное место.</span><span class="sxs-lookup"><span data-stu-id="1caab-123">The following properties are required in later steps, so copy them to a safe place:</span></span>

    * <span data-ttu-id="1caab-124">Идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="1caab-124">Client Id</span></span>
    * <span data-ttu-id="1caab-125">Client Secret</span><span class="sxs-lookup"><span data-stu-id="1caab-125">Client Secret</span></span> 

## <a name="step-2-build-a-webhook-receiver"></a><span data-ttu-id="1caab-126">Шаг 2. Создание приемника веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1caab-126">Step 2: Build a webhook receiver</span></span>

<span data-ttu-id="1caab-127">Чтобы создать для этого проекта приемник веб-перехватчиков, используйте проект веб-API Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-127">For this project, use the Visual Studio Web API project to build the webhook receiver.</span></span>

### <a name="create-a-new-aspnet-web-api-project"></a><span data-ttu-id="1caab-128">Создание проекта веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1caab-128">Create a new ASP.NET Web API project</span></span>

1. <span data-ttu-id="1caab-129">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-129">Open Visual Studio.</span></span>

2. <span data-ttu-id="1caab-130">Выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="1caab-130">Select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="1caab-131">В области **Шаблоны** выберите **Установленные шаблоны** и разверните узел **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="1caab-131">In the **Templates** pane, select **Installed Templates**, and expand the **Visual C#** node.</span></span> 

4. <span data-ttu-id="1caab-132">В разделе **Visual C#** выберите **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="1caab-132">Under **Visual C#**, select **Web**.</span></span> 

5. <span data-ttu-id="1caab-133">В списке шаблонов проектов выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="1caab-133">In the list of project templates, select **ASP.NET Web Application**.</span></span> 

6. <span data-ttu-id="1caab-134">Назовите проект **SPWebhooksReceiver** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1caab-134">Name the project **SPWebhooksReceiver**, and select **OK**.</span></span>

7. <span data-ttu-id="1caab-135">В диалоговом окне **Новый проект ASP.NET** выберите шаблон **Веб-API** в группе **ASP.NET 4.5.**</span><span class="sxs-lookup"><span data-stu-id="1caab-135">In the **New ASP.NET Project** dialog, select the **Web API** template from the **ASP.NET 4.5.**</span></span> <span data-ttu-id="1caab-136">.</span><span class="sxs-lookup"><span data-stu-id="1caab-136">group.</span></span> 

8. <span data-ttu-id="1caab-137">Нажмите кнопку **Изменить способ проверки подлинности** и выберите **Без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="1caab-137">Change the authentication to **No Authentication** by selecting the **Change Authentication** button.</span></span>

9. <span data-ttu-id="1caab-138">Нажмите кнопку **ОК**, чтобы создать проект веб-API.</span><span class="sxs-lookup"><span data-stu-id="1caab-138">Select **OK** to create the Web API project.</span></span>

> [!NOTE]
> <span data-ttu-id="1caab-139">Вы можете снять флажок **Разместить в облаке**, так как этот проект не будет развертываться в облаке.</span><span class="sxs-lookup"><span data-stu-id="1caab-139">You can clear the **Host in the cloud** check box because this project will not be deployed to the cloud.</span></span>

<span data-ttu-id="1caab-140">Visual Studio создаст ваш проект.</span><span class="sxs-lookup"><span data-stu-id="1caab-140">Visual Studio creates your project.</span></span>

### <a name="build-the-webhook-receiver"></a><span data-ttu-id="1caab-141">Сборка приемника веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1caab-141">Build the webhook receiver</span></span>

#### <a name="install-nuget-packages"></a><span data-ttu-id="1caab-142">Установка пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="1caab-142">Install NuGet packages</span></span>

<span data-ttu-id="1caab-143">Для ведения журнала запросов, поступающих от SharePoint, используется трассировка веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1caab-143">Use ASP.NET Web API Tracing to log the requests coming from SharePoint.</span></span> <span data-ttu-id="1caab-144">Чтобы установить пакет трассировки, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1caab-144">The following steps install the tracing package:</span></span>

1. <span data-ttu-id="1caab-145">Откройте **обозреватель решений** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-145">Go to **Solution Explorer** in Visual Studio.</span></span>

2. <span data-ttu-id="1caab-146">Откройте контекстное меню проекта и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1caab-146">Open the context menu (right-click) for the project, and select **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="1caab-147">В поле поиска введите **Microsoft.AspNet.WebApi.Tracing**.</span><span class="sxs-lookup"><span data-stu-id="1caab-147">In the search box, enter **Microsoft.AspNet.WebApi.Tracing**.</span></span>

4. <span data-ttu-id="1caab-148">В результатах поиска выберите пакет **Microsoft.AspNet.WebApi.Tracing** и нажмите кнопку **Установить**, чтобы установить пакет.</span><span class="sxs-lookup"><span data-stu-id="1caab-148">In the search results, select the **Microsoft.AspNet.WebApi.Tracing** package, and then select **Install** to install the package.</span></span>

#### <a name="build-spwebhooknotification-model"></a><span data-ttu-id="1caab-149">Сборка модели SPWebhookNotification</span><span class="sxs-lookup"><span data-stu-id="1caab-149">Build SPWebhookNotification model</span></span>

<span data-ttu-id="1caab-150">Каждое уведомление, созданное службой, сериализуется в экземпляр **webhookNotification**.</span><span class="sxs-lookup"><span data-stu-id="1caab-150">Each notification generated by the service is serialized into a **webhookNotification** instance.</span></span> <span data-ttu-id="1caab-151">Вам нужно создать простую модель, которая представляет этот экземпляр уведомления.</span><span class="sxs-lookup"><span data-stu-id="1caab-151">You need to build a simple model that represents this notification instance.</span></span>

1. <span data-ttu-id="1caab-152">Откройте **обозреватель решений** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-152">Go to **Solution Explorer** in Visual Studio.</span></span>

2. <span data-ttu-id="1caab-153">Откройте контекстное меню папки **Модели** и выберите **Добавить** > **Класс**.</span><span class="sxs-lookup"><span data-stu-id="1caab-153">Open the context menu (right-click) for the **Models** folder, and select **Add** > **Class**.</span></span>

3. <span data-ttu-id="1caab-154">Введите имя класса **SPWebhookNotification** и нажмите кнопку **Добавить**, чтобы добавить класс в проект.</span><span class="sxs-lookup"><span data-stu-id="1caab-154">Enter **SPWebhookNotification** as the class name and select **Add** to add the class to your project.</span></span>

4. <span data-ttu-id="1caab-155">Добавьте следующий код в текст класса **SPWebhookNotification**:</span><span class="sxs-lookup"><span data-stu-id="1caab-155">Add the following code to the body of the **SPWebhookNotification** class:</span></span>

    ```cs
    public string SubscriptionId { get; set; }

    public string ClientState { get; set; }

    public string ExpirationDateTime { get; set; }

    public string Resource { get; set; }

    public string TenantId { get; set; }

    public string SiteUrl { get; set; }

    public string WebId { get; set; }
    ```

#### <a name="build-spwebhookcontent-model"></a><span data-ttu-id="1caab-156">Сборка модели SPWebhookContent</span><span class="sxs-lookup"><span data-stu-id="1caab-156">Build SPWebhookContent model</span></span>

<span data-ttu-id="1caab-p107">Так как в одном запросе приемнику веб-перехватчиков могут отправляться несколько уведомлений, они объединяются в объект со значением единого массива. Создайте простую модель, представляющую массив.</span><span class="sxs-lookup"><span data-stu-id="1caab-p107">Because multiple notifications can be submitted to your webhook receiver in a single request, they are combined together in an object with a single array value. Build a simple model that represents the array.</span></span>

1. <span data-ttu-id="1caab-159">Откройте **обозреватель решений** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-159">Go to **Solution Explorer** in Visual Studio.</span></span>

2. <span data-ttu-id="1caab-160">Откройте контекстное меню папки **Модели** и выберите **Добавить** > **Класс**.</span><span class="sxs-lookup"><span data-stu-id="1caab-160">Open the context menu (right-click) for the **Models** folder, and select **Add** > **Class**.</span></span>

3. <span data-ttu-id="1caab-161">Введите имя класса **SPWebhookContent** и нажмите кнопку **Добавить**, чтобы добавить класс в проект.</span><span class="sxs-lookup"><span data-stu-id="1caab-161">Enter **SPWebhookContent** as the class name, and select **Add** to add the class to your project.</span></span>

4. <span data-ttu-id="1caab-162">Добавьте следующий код в текст класса **SPWebhookContent**:</span><span class="sxs-lookup"><span data-stu-id="1caab-162">Add the following code to the body of the **SPWebhookContent** class:</span></span>

    ```cs
     public List<SPWebhookNotification> Value { get; set; }
    ```

#### <a name="add-sharepoint-webhook-client-state"></a><span data-ttu-id="1caab-163">Добавление состояния клиента веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="1caab-163">Add SharePoint webhook client state</span></span>

<span data-ttu-id="1caab-p108">Веб-перехватчики позволяют использовать необязательное строковое значение, возвращаемое в уведомлении для подписки. С его помощью можно проверить, действительно ли запрос поступает из доверенного источника (в данном случае — SharePoint).</span><span class="sxs-lookup"><span data-stu-id="1caab-p108">Webhooks provide the ability to use an optional string value that is passed back in the notification message for your subscription. This can be used to verify that the request is indeed coming from the source you trust, which in this case is SharePoint.</span></span> 

<span data-ttu-id="1caab-166">Добавьте значение состояния клиента, с помощью которого приложение может проверять входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="1caab-166">Add a client state value with which the application can verify the incoming requests.</span></span>

1. <span data-ttu-id="1caab-167">Откройте **обозреватель решений** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-167">Go to **Solution Explorer** in Visual Studio.</span></span>

2. <span data-ttu-id="1caab-168">Откройте файл **web.config** и добавьте следующий ключ состояния клиента в раздел `<appSettings>`:</span><span class="sxs-lookup"><span data-stu-id="1caab-168">Open the **web.config** file, and add the following key as the client state to the `<appSettings>` section:</span></span>

    ```xml
    <add key="webhookclientstate" value="A0A354EC-97D4-4D83-9DDB-144077ADB449"/>
    ```

#### <a name="enable-tracing"></a><span data-ttu-id="1caab-169">Включение трассировки</span><span class="sxs-lookup"><span data-stu-id="1caab-169">Enable tracing</span></span>

<span data-ttu-id="1caab-170">Включите трассировку в файле **web.config**, добавив следующий код в элемент `<system.web>` в разделе `<configuration>`:</span><span class="sxs-lookup"><span data-stu-id="1caab-170">In the **web.config** file, enable tracing by adding the following key inside the `<system.web>` element in the `<configuration>` section:</span></span>

```xml
<trace enabled="true"/>
```

<span data-ttu-id="1caab-171">Вам потребуется средство записи трассировки, поэтому его следует добавить в конфигурацию контроллера (в данном случае используйте конфигурацию из **System.Diagnostics**).</span><span class="sxs-lookup"><span data-stu-id="1caab-171">A trace writer is required, so you must add a trace writer to the controller configuration (in this case use the one from **System.Diagnostics**).</span></span>

1. <span data-ttu-id="1caab-172">Откройте **обозреватель решений** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-172">Go to **Solution Explorer** in Visual Studio.</span></span>

2. <span data-ttu-id="1caab-173">Откройте файл **WebApiConfig.cs** в папке **App_Start**.</span><span class="sxs-lookup"><span data-stu-id="1caab-173">Open **WebApiConfig.cs** in the **App_Start** folder.</span></span>

3. <span data-ttu-id="1caab-174">Добавьте следующую строку в метод **Register**:</span><span class="sxs-lookup"><span data-stu-id="1caab-174">Add the following line inside the **Register** method:</span></span>

    ```cs
    config.EnableSystemDiagnosticsTracing();
    ```

#### <a name="build-sharepoint-webhook-controller"></a><span data-ttu-id="1caab-175">Создание контроллера веб-перехватчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="1caab-175">Build SharePoint webhook controller</span></span>

<span data-ttu-id="1caab-176">Теперь создайте контроллер приемника веб-перехватчиков, который обрабатывает входящие запросы из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1caab-176">Now build the webhook receiver controller that handles the incoming requests from SharePoint and take action accordingly.</span></span>

1. <span data-ttu-id="1caab-177">Откройте **обозреватель решений** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-177">Go to **Solution Explorer** in Visual Studio.</span></span>

2. <span data-ttu-id="1caab-178">Откройте контекстное меню папки **Контроллеры** и выберите **Добавить** > **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="1caab-178">Open the context menu (right-click) for the **Controllers** folder, and select **Add** > **Controller**.</span></span>

3. <span data-ttu-id="1caab-179">В диалоговом окне **Добавление шаблона** выберите **Контроллер Web API 2 – пустой**.</span><span class="sxs-lookup"><span data-stu-id="1caab-179">In the **Add Scaffold** dialog, select **Web API 2 Controller - Empty**.</span></span>

4. <span data-ttu-id="1caab-180">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1caab-180">Select **Add**.</span></span>

5. <span data-ttu-id="1caab-181">Назовите контроллер **SPWebhookController** и нажмите кнопку **Добавить**, чтобы добавить контроллер API в проект.</span><span class="sxs-lookup"><span data-stu-id="1caab-181">Name the controller **SPWebhookController**, and select **Add** to add the API controller to your project.</span></span>

6. <span data-ttu-id="1caab-182">Замените операторы `using` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="1caab-182">Replace the `using` statements with the following code:</span></span>

    ```cs
    using Newtonsoft.Json;
    using SPWebhooksReceiver.Models;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web;
    using System.Web.Http;
    using System.Web.Http.Tracing;
    ```

7. <span data-ttu-id="1caab-183">Замените код класса **SPWebhookController** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="1caab-183">Replace the code in the **SPWebhookController** class with the following code:</span></span>

    ```cs
    [HttpPost]
    public HttpResponseMessage HandleRequest()
    {
        HttpResponseMessage httpResponse = new HttpResponseMessage(HttpStatusCode.BadRequest);
        var traceWriter = Configuration.Services.GetTraceWriter();
        string validationToken = string.Empty;
        IEnumerable<string> clientStateHeader = new List<string>();
        string webhookClientState = ConfigurationManager.AppSettings["webhookclientstate"].ToString();

        if (Request.Headers.TryGetValues("ClientState", out clientStateHeader))
        {
            string clientStateHeaderValue = clientStateHeader.FirstOrDefault() ?? string.Empty;

            if (!string.IsNullOrEmpty(clientStateHeaderValue) && clientStateHeaderValue.Equals(webhookClientState))
            {
                traceWriter.Trace(Request, "SPWebhooks", 
                    TraceLevel.Info, 
                    string.Format("Received client state: {0}", clientStateHeaderValue));

                var queryStringParams = HttpUtility.ParseQueryString(Request.RequestUri.Query);

                if (queryStringParams.AllKeys.Contains("validationtoken"))
                {
                    httpResponse = new HttpResponseMessage(HttpStatusCode.OK);
                    validationToken = queryStringParams.GetValues("validationtoken")[0].ToString();
                    httpResponse.Content = new StringContent(validationToken);

                    traceWriter.Trace(Request, "SPWebhooks", 
                        TraceLevel.Info, 
                        string.Format("Received validation token: {0}", validationToken));                        
                    return httpResponse;
                }
                else
                {
                    var requestContent = Request.Content.ReadAsStringAsync().Result;

                    if (!string.IsNullOrEmpty(requestContent))
                    {
                        SPWebhookNotification notification = null;

                        try
                        {
                            var objNotification = JsonConvert.DeserializeObject<SPWebhookContent>(requestContent);
                            notification = objNotification.Value[0];
                        }
                        catch (JsonException ex)
                        {
                            traceWriter.Trace(Request, "SPWebhooks", 
                                TraceLevel.Error, 
                                string.Format("JSON deserialization error: {0}", ex.InnerException));
                            return httpResponse;
                        }

                        if (notification != null)
                        {
                            Task.Factory.StartNew(() =>
                            {
                                 //handle the notification here
                                 //you can send this to an Azure queue to be processed later
                                //for this sample, we just log to the trace

                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("Resource: {0}", notification.Resource));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("SubscriptionId: {0}", notification.SubscriptionId));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("TenantId: {0}", notification.TenantId));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("SiteUrl: {0}", notification.SiteUrl));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("WebId: {0}", notification.WebId));
                                traceWriter.Trace(Request, "SPWebhook Notification", 
                                    TraceLevel.Info, string.Format("ExpirationDateTime: {0}", notification.ExpirationDateTime));

                            });

                            httpResponse = new HttpResponseMessage(HttpStatusCode.OK);
                        }
                    }
                }
            }
            else
            {
                httpResponse = new HttpResponseMessage(HttpStatusCode.Forbidden);
            }
        }

        return httpResponse;
    }
    ```

8. <span data-ttu-id="1caab-184">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="1caab-184">Save the file.</span></span>

## <a name="step-3-debug-the-webhook-receiver"></a><span data-ttu-id="1caab-185">Шаг 3. Отладка приемника веб-перехватчиков</span><span class="sxs-lookup"><span data-stu-id="1caab-185">Step 3: Debug the webhook receiver</span></span>

1. <span data-ttu-id="1caab-186">Нажмите клавишу **F5** для отладки приемника веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="1caab-186">Select **F5** to debug the webhook receiver.</span></span>

2. <span data-ttu-id="1caab-187">Скопируйте номер порта из адресной строки браузера.</span><span class="sxs-lookup"><span data-stu-id="1caab-187">When you have the browser open, copy the port number from the address bar.</span></span> <span data-ttu-id="1caab-188">Пример: `http://localhost:<_port-number_>`</span><span class="sxs-lookup"><span data-stu-id="1caab-188">For example: `http://localhost:<_port-number_>`</span></span>

## <a name="step-4-run-ngrok-proxy"></a><span data-ttu-id="1caab-189">Шаг 4. Запуск прокси-сервера ngrok</span><span class="sxs-lookup"><span data-stu-id="1caab-189">Step 4: Run ngrok proxy</span></span>

1. <span data-ttu-id="1caab-190">Откройте терминал консоли.</span><span class="sxs-lookup"><span data-stu-id="1caab-190">Open a console terminal.</span></span>

2. <span data-ttu-id="1caab-191">Перейдите к папке, в которую вы распаковали ngrok.</span><span class="sxs-lookup"><span data-stu-id="1caab-191">Go to the extracted ngrok folder.</span></span>

3. <span data-ttu-id="1caab-192">Чтобы запустить ngrok, введите следующую команду с номером порта, скопированным на предыдущем шаге:</span><span class="sxs-lookup"><span data-stu-id="1caab-192">Enter the following with the port number URL from the previous step to start ngrok:</span></span>

    ```
    ./ngrok http port-number --host-header=localhost:port-number
    ```

    <span data-ttu-id="1caab-193">Должен запуститься ngrok.</span><span class="sxs-lookup"><span data-stu-id="1caab-193">You should see ngrok running.</span></span>

4. <span data-ttu-id="1caab-194">Скопируйте HTTPS-адрес **переадресации**.</span><span class="sxs-lookup"><span data-stu-id="1caab-194">Copy the **Forwarding** HTTPS address.</span></span> <span data-ttu-id="1caab-195">Этот адрес будет использоваться в качестве прокси-сервера службы для отправки запросов из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1caab-195">You will use this address as the service proxy for SharePoint to send requests.</span></span> 

## <a name="step-5-add-webhook-subscription-using-postman"></a><span data-ttu-id="1caab-196">Этап 5. Добавление подписки на веб-перехватчик с помощью Postman</span><span class="sxs-lookup"><span data-stu-id="1caab-196">Step 5: Add webhook subscription using Postman</span></span>

### <a name="get-new-access-token"></a><span data-ttu-id="1caab-197">Получение нового маркера доступа</span><span class="sxs-lookup"><span data-stu-id="1caab-197">Get new access token</span></span>

<span data-ttu-id="1caab-p111">Postman значительно упрощает работу с API. Для начала настройте аутентификацию Postman с помощью Azure AD, чтобы отправлять запросы API в SharePoint. Вы будете использовать приложение Azure AD, зарегистрированное на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="1caab-p111">Postman makes it really simple to work with APIs. The first step is to configure Postman to authenticate with Azure AD so you can send API requests to SharePoint. You will use the Azure AD app that you registered in Step 1.</span></span>

1. <span data-ttu-id="1caab-201">Откройте Postman.</span><span class="sxs-lookup"><span data-stu-id="1caab-201">Open Postman.</span></span> <span data-ttu-id="1caab-202">Вы увидите **боковую панель** и **редактор запросов**.</span><span class="sxs-lookup"><span data-stu-id="1caab-202">You are presented with a **Sidebar** and **Request Editor**.</span></span>

2. <span data-ttu-id="1caab-203">Выберите вкладку **Authorization** (Авторизация) в **редакторе запросов**.</span><span class="sxs-lookup"><span data-stu-id="1caab-203">Select the **Authorization** tab in the **Request Editor**.</span></span>

3. <span data-ttu-id="1caab-204">Выберите **OAuth 2.0** в списке **Type** (Тип).</span><span class="sxs-lookup"><span data-stu-id="1caab-204">Select **OAuth 2.0** in the **Type** list.</span></span>

4. <span data-ttu-id="1caab-205">Нажмите кнопку **Get New Access Token** (Получить новый маркер доступа).</span><span class="sxs-lookup"><span data-stu-id="1caab-205">Select the **Get New Access Token** button.</span></span>

5. <span data-ttu-id="1caab-206">В диалоговом окне введите следующее:</span><span class="sxs-lookup"><span data-stu-id="1caab-206">In the dialog window, enter the following:</span></span> 
    * <span data-ttu-id="1caab-207">**Auth URL**:</span><span class="sxs-lookup"><span data-stu-id="1caab-207">**Auth URL**:</span></span> 
       * `https://login.microsoftonline.com/common/oauth2/authorize?resource=https%3A%2F%2F<_your-sharepoint-tenant-url-without-https_>`
       * <span data-ttu-id="1caab-208">замените `your-sharepoint-tenant-url-without-https` URL-адресом клиента без префикса **https**.</span><span class="sxs-lookup"><span data-stu-id="1caab-208">Replace `your-sharepoint-tenant-url-without-https` with your tenant url without the **https** prefix.</span></span>
    * <span data-ttu-id="1caab-209">**Access Token URL**: `https://login.microsoftonline.com/common/oauth2/token`</span><span class="sxs-lookup"><span data-stu-id="1caab-209">**Access Token URL**: `https://login.microsoftonline.com/common/oauth2/token`</span></span>
    * <span data-ttu-id="1caab-210">**Client Id**: идентификатор клиента для приложения, зарегистрированного на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="1caab-210">**Client Id**: Client Id of the app you registered previously in Step one.</span></span>
    * <span data-ttu-id="1caab-211">**Client Secret**: секрет клиента для приложения, зарегистрированного на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="1caab-211">**Client Secret**: Client Secret of the app you registered previously in Step one.</span></span>
    * <span data-ttu-id="1caab-212">**Token name**: sp_webhooks_token</span><span class="sxs-lookup"><span data-stu-id="1caab-212">**Token name**: sp_webhooks_token</span></span>
    * <span data-ttu-id="1caab-213">**Grant type**: Authorization Code</span><span class="sxs-lookup"><span data-stu-id="1caab-213">**Grant type**: Authorization Code</span></span>

6. <span data-ttu-id="1caab-214">Нажмите **Request Token** (Запросить маркер), чтобы войти, предоставить разрешения и получить маркер для сеанса.</span><span class="sxs-lookup"><span data-stu-id="1caab-214">Select the **Request Token** to sign in, consent, and get the token for the session.</span></span>

7. <span data-ttu-id="1caab-215">После успешного получения маркера на вкладке **Authorization** (Авторизация) должна появиться переменная **access\_token**.</span><span class="sxs-lookup"><span data-stu-id="1caab-215">When the token is successfully retrieved, you should see **access\_token** variable added to the **Authorization** tab.</span></span>

8. <span data-ttu-id="1caab-216">Нажмите **Add token to header** (Добавить маркер к заголовку).</span><span class="sxs-lookup"><span data-stu-id="1caab-216">Select the option to **Add token to header**.</span></span>

9. <span data-ttu-id="1caab-217">Дважды щелкните переменную **access\_token**, чтобы добавить маркер к заголовку запроса.</span><span class="sxs-lookup"><span data-stu-id="1caab-217">Double-click the **access\_token** variable to add the token to the header for the request.</span></span>

    ![Получение нового маркера доступа в Postman](../../images/postman-get-new-access-token.png)

### <a name="get-documents-list-id"></a><span data-ttu-id="1caab-219">Получение идентификатора списка документов</span><span class="sxs-lookup"><span data-stu-id="1caab-219">Get Documents list Id</span></span>

<span data-ttu-id="1caab-220">Вам необходимо управлять веб-перехватчиками для стандартной библиотеки документов **Документы**, подготовленной в семействе веб-сайтов по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1caab-220">You need to manage webhooks for the default document library, which is provisioned in your default site collection under the name **Documents**.</span></span> <span data-ttu-id="1caab-221">Чтобы получить идентификатор этого списка, отправьте запрос **GET**:</span><span class="sxs-lookup"><span data-stu-id="1caab-221">Get the Id of this list by issuing a **GET** request:</span></span>

1. <span data-ttu-id="1caab-222">Введите следующий URL-адрес запроса:</span><span class="sxs-lookup"><span data-stu-id="1caab-222">Enter the following request URL:</span></span>

    ```
    https://site-collection/_api/web/lists/getbytitle('Documents')?$select=Title,Id
    ```

2. <span data-ttu-id="1caab-223">Замените _site-collection_ именем своего семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="1caab-223">Replace _site-collection_ with your site collection.</span></span>
    
    <span data-ttu-id="1caab-224">Postman выполнит запрос. В случае успешного выполнения появится результат.</span><span class="sxs-lookup"><span data-stu-id="1caab-224">Postman executes your request and if successful, you should see the result.</span></span>

3. <span data-ttu-id="1caab-225">Скопируйте значение **Id** из результатов.</span><span class="sxs-lookup"><span data-stu-id="1caab-225">Copy the **Id** from the results.</span></span> <span data-ttu-id="1caab-226">Это значение **Id** потребуется позже для отправки запросов к веб-перехватчикам.</span><span class="sxs-lookup"><span data-stu-id="1caab-226">Later you will use the **Id** to make webhook requests.</span></span>   

### <a name="add-webhook-subscription"></a><span data-ttu-id="1caab-227">Добавление подписки на веб-перехватчик</span><span class="sxs-lookup"><span data-stu-id="1caab-227">Add webhook subscription</span></span>

<span data-ttu-id="1caab-p115">Теперь, когда у вас есть необходимые сведения, составьте запрос на добавление подписки на веб-перехватчик. С помощью редактора запросов сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="1caab-p115">Now that you have the required information, construct the query and the request to add a webhook subscription. Use the request editor for the following steps:</span></span>

1. <span data-ttu-id="1caab-230">Замените запрос **GET** на запрос **POST**.</span><span class="sxs-lookup"><span data-stu-id="1caab-230">Change the request to **POST** from **GET**.</span></span>

2. <span data-ttu-id="1caab-231">Введите следующий URL-адрес запроса:</span><span class="sxs-lookup"><span data-stu-id="1caab-231">Enter the following as the request URL:</span></span>

    ```
    https://site-collection/_api/web/lists('list-id')/subscriptions
    ```

3. <span data-ttu-id="1caab-232">Замените _site-collection_ на имя вашего семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="1caab-232">Replace _site-collection_ with your site collection.</span></span>

4. <span data-ttu-id="1caab-233">Перейдите на вкладку **Headers** (Запросы).</span><span class="sxs-lookup"><span data-stu-id="1caab-233">Go to the **Headers** tab.</span></span>

5. <span data-ttu-id="1caab-234">Убедитесь, что у вас по-прежнему есть заголовок **Authorization**.</span><span class="sxs-lookup"><span data-stu-id="1caab-234">Make sure you still have the **Authorization** header.</span></span> <span data-ttu-id="1caab-235">В противном случае необходимо запросить новый маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="1caab-235">If not, you need to request a new access token.</span></span>

6. <span data-ttu-id="1caab-236">Добавьте следующие пары **ключ** > **значение** для заголовка:</span><span class="sxs-lookup"><span data-stu-id="1caab-236">Add the following header **key** > **value** pairs:</span></span>
    * <span data-ttu-id="1caab-237">Accept > application/json;odata=nometadata</span><span class="sxs-lookup"><span data-stu-id="1caab-237">Accept > application/json;odata=nometadata</span></span>
    * <span data-ttu-id="1caab-238">Content-Type > application/json</span><span class="sxs-lookup"><span data-stu-id="1caab-238">Content-Type > application/json</span></span>

7. <span data-ttu-id="1caab-239">Перейдите на вкладку **Body** (Текст) и выберите формат **raw**.</span><span class="sxs-lookup"><span data-stu-id="1caab-239">Go to the **Body** tab and select **raw** format.</span></span>

8. <span data-ttu-id="1caab-240">Вставьте в качестве текста следующий код JSON:</span><span class="sxs-lookup"><span data-stu-id="1caab-240">Paste the following JSON as the body:</span></span>

    ```json
    {
      "resource": "https://site-collection/_api/web/lists('list-id')",
      "notificationUrl": "https://ngrok-forwarding-address/api/spwebhook/handlerequest",
      "expirationDateTime": "2016-10-27T16:17:57+00:00",
      "clientState": "A0A354EC-97D4-4D83-9DDB-144077ADB449"
    }
    ```

    <br/>

    ![Добавление текста веб-перехватчика в Postman](../../images/postman-add-webhook-body.png)

9. <span data-ttu-id="1caab-242">Убедитесь, что значение **expirationDateTime** превышает текущую дату не более чем на 6 месяцев.</span><span class="sxs-lookup"><span data-stu-id="1caab-242">Make sure the **expirationDateTime** is at most 6 months from today.</span></span> 

10. <span data-ttu-id="1caab-243">Убедитесь, что отладка веб-перехватчика выполняется так же, как на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="1caab-243">Make sure you are debugging the webhook receiver as in Step 4.</span></span>

11. <span data-ttu-id="1caab-244">Нажмите кнопку **Send** (Отправить), чтобы выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="1caab-244">Select **Send** to execute the request.</span></span>

    <span data-ttu-id="1caab-p117">Если запрос будет выполнен, появится ответ от SharePoint со сведениями о подписке. В следующем примере показан ответ для новой подписки:</span><span class="sxs-lookup"><span data-stu-id="1caab-p117">If the request is successful, you should see the response from SharePoint that provides the subscription details. The following example shows a response for a newly created subscription:</span></span>

    ```json
    {
      "clientState": "A0A354EC-97D4-4D83-9DDB-144077ADB449",
      "expirationDateTime": "2016-10-27T16:17:57Z",
      "id": "32b95d9-4d20-4a17-bfa3-2957cb38ead8",
      "notificationUrl": "https://85557d4b.ngrok.io/api/spwebhook/handlerequest",
      "resource": "c34420f9-2ad7-4e54-94c9-b67798d2299b"
    }
    ```

12. <span data-ttu-id="1caab-247">Скопируйте значение **id** подписки. Оно потребуется для следующего набора запросов.</span><span class="sxs-lookup"><span data-stu-id="1caab-247">Copy the subscription **id**. You will need it for the next set of requests.</span></span>

13. <span data-ttu-id="1caab-248">Перейдите к проекту приемника веб-перехватчиков в Visual Studio и просмотрите окно **Вывод**.</span><span class="sxs-lookup"><span data-stu-id="1caab-248">Go to the webhook receiver project in Visual Studio and examine the **Output** window.</span></span> <span data-ttu-id="1caab-249">В нем (наряду с другими сообщениями) должны отображаться журналы трассировки, подобные следующему:</span><span class="sxs-lookup"><span data-stu-id="1caab-249">You should see the trace logs that look similar to the following trace, along with other messages:</span></span>

    ```
    iisexpress.exe Information: 0 : Message='Received client state: A0A354EC-97D4-4D83-9DDB-144077ADB449'
    iisexpress.exe Information: 0 : Message='Received validation token: daf2803c-43cf-44c7-8dff-7066eaa40f13'
    ```

    <span data-ttu-id="1caab-p119">Трассировка указывает, что веб-перехватчик получил запрос на проверку. Изучив этот код, вы заметите, что он сразу возвращает маркер проверки, чтобы SharePoint мог проверить запрос:</span><span class="sxs-lookup"><span data-stu-id="1caab-p119">The trace indicates that the webhook received initially received a validation request. If you look at the code, you'll see that it returns the validation token immediately so that SharePoint can validate the request:</span></span>

    ```cs
    if (queryStringParams.AllKeys.Contains("validationtoken"))
    {
        httpResponse = new HttpResponseMessage(HttpStatusCode.OK);
        validationToken = queryStringParams.GetValues("validationtoken")[0].ToString();
        httpResponse.Content = new StringContent(validationToken);

        traceWriter.Trace(Request, "SPWebhooks", 
            TraceLevel.Info, 
            string.Format("Received validation token: {0}", validationToken));                        
        return httpResponse;
    }
    ```

## <a name="step-6-get-subscription-details"></a><span data-ttu-id="1caab-252">Шаг 6. Получение сведений о подписке</span><span class="sxs-lookup"><span data-stu-id="1caab-252">Step 6: Get subscription details</span></span>

<span data-ttu-id="1caab-253">Теперь мы выполним запросы на получение сведений о подписке в Postman.</span><span class="sxs-lookup"><span data-stu-id="1caab-253">Now you'll run queries in Postman to get the subscription details.</span></span>

1. <span data-ttu-id="1caab-254">Откройте клиент Postman.</span><span class="sxs-lookup"><span data-stu-id="1caab-254">Open the Postman client.</span></span>

2. <span data-ttu-id="1caab-255">Замените запрос **POST** на запрос **GET**.</span><span class="sxs-lookup"><span data-stu-id="1caab-255">Change the request to **GET** from **POST**.</span></span>

3. <span data-ttu-id="1caab-256">Введите следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="1caab-256">Enter the following as the request:</span></span>

    ```
    https://site-collection/_api/web/lists('list-id')/subscriptions
    ```

4. <span data-ttu-id="1caab-257">Замените _site-collection_ именем своего семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="1caab-257">Replace _site-collection_ with your site collection.</span></span>

5. <span data-ttu-id="1caab-258">Нажмите кнопку **Send** (Отправить), чтобы выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="1caab-258">Select **Send** to execute the request.</span></span>

    <span data-ttu-id="1caab-p120">Если запрос будет выполнен, SharePoint вернет подписки для этого ресурса списка. Так как мы только что добавили подписку, должна появиться хотя бы одна подписка. В следующем примере показан ответ с одной подпиской:</span><span class="sxs-lookup"><span data-stu-id="1caab-p120">If successful, you should see SharePoint return the subscriptions for this list resource. Because we just added one, you should at least see one subscription returned. The following example shows a response with one subscription:</span></span>

    ```json
    {
      "value": [
        {
          "clientState": "A0A354EC-97D4-4D83-9DDB-144077ADB449",
          "expirationDateTime": "2016-10-27T16:17:57Z",
          "id": "32b95add-4d20-4a17-bfa3-2957cb38ead8",
          "notificationUrl": "https://85557d4b.ngrok.io/api/spwebhook/handlerequest",
          "resource": "c34420f9-2a67-4e54-94c9-b67798229f9b"
        }
      ]
    }
    ```

6. <span data-ttu-id="1caab-262">Выполните следующий запрос, чтобы получить сведения о подписке:</span><span class="sxs-lookup"><span data-stu-id="1caab-262">Run the following query to get details of the specific subscription:</span></span>

    ```
    https://site-collection/_api/web/lists('list-id')/subscriptions('subscription-id')
    ```

7. <span data-ttu-id="1caab-263">Замените `subscription-id` идентификатором подписки.</span><span class="sxs-lookup"><span data-stu-id="1caab-263">Replace `subscription-id` with your subscription id.</span></span> 

## <a name="step-7-test-webhook-notification"></a><span data-ttu-id="1caab-264">Шаг 7. Тестирование уведомления веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="1caab-264">Step 7: Test webhook notification</span></span>

<span data-ttu-id="1caab-265">Теперь добавьте файл в библиотеку документов и проверьте, приходит ли уведомление из SharePoint в приемник веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="1caab-265">Now add a file to the Documents library and test if you get a notification from SharePoint in the webhook receiver.</span></span>

1. <span data-ttu-id="1caab-266">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1caab-266">Go to Visual Studio.</span></span>

2. <span data-ttu-id="1caab-267">В элементе **SPWebhookController** добавьте точку останова на следующей строке кода:</span><span class="sxs-lookup"><span data-stu-id="1caab-267">In the **SPWebhookController**, place a breakpoint on the following line of code:</span></span>

    ```cs
    var requestContent = Request.Content.ReadAsStringAsync().Result;
    ```

3. <span data-ttu-id="1caab-268">Перейдите к библиотеке **Документы**.</span><span class="sxs-lookup"><span data-stu-id="1caab-268">Go to the **Documents** library.</span></span> <span data-ttu-id="1caab-269">В семействе веб-сайтов по умолчанию она называется **Общие документы**.</span><span class="sxs-lookup"><span data-stu-id="1caab-269">It is named **Shared Documents** library in your default site collection.</span></span>

4. <span data-ttu-id="1caab-270">Добавьте новый файл.</span><span class="sxs-lookup"><span data-stu-id="1caab-270">Add a new file.</span></span>

5. <span data-ttu-id="1caab-271">Откройте Visual Studio и подождите, пока не будет достигнута точка останова.</span><span class="sxs-lookup"><span data-stu-id="1caab-271">Go to Visual Studio and wait for the breakpoint to be hit.</span></span>

    <span data-ttu-id="1caab-272">Это может занять от нескольких секунд до пяти минут.</span><span class="sxs-lookup"><span data-stu-id="1caab-272">The wait time may vary from a few seconds to up to five minutes.</span></span> <span data-ttu-id="1caab-273">Когда будет достигнута точка останова, это означает, что приемник веб-перехватчиков только что получил уведомление от SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1caab-273">When the breakpoint is hit, the webhook receiver has just received a notification from SharePoint.</span></span>

6. <span data-ttu-id="1caab-274">Нажмите клавишу **F5**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="1caab-274">Select **F5** to continue.</span></span>

7. <span data-ttu-id="1caab-275">Чтобы увидеть данные уведомления, найдите следующие записи в окне **Выходные данные**, так как вы добавили данные уведомления в журнал трассировки:</span><span class="sxs-lookup"><span data-stu-id="1caab-275">To see the notification data, look in the **Output** window for the following entries, since you added the notification data into the trace log:</span></span>

    ```
    iisexpress.exe Information: 0 : Message='Resource: c34420f9-2a67-4e54-94c9-b6770892299b'
    iisexpress.exe Information: 0 : Message='SubscriptionId: 32b95ad9-4d20-4a17-bfa3-2957cb38ead8'
    iisexpress.exe Information: 0 : Message='TenantId: 7a17cb7d-6898-423f-8839-45f363076f06'
    iisexpress.exe Information: 0 : Message='SiteUrl: /'
    iisexpress.exe Information: 0 : Message='WebId: 62b80e0b-f889-4974-a519-cc138413be40'
    iisexpress.exe Information: 0 : Message='ExpirationDateTime: 2016-10-27T16:17:57.0000000Z'
    ```

<span data-ttu-id="1caab-276">Этот проект просто записывает сведения в журнал трассировки.</span><span class="sxs-lookup"><span data-stu-id="1caab-276">This project only writes the information to the trace log.</span></span> <span data-ttu-id="1caab-277">Однако в нашем приемнике эти сведения отправляются в таблицу или очередь, которая может обрабатывать полученные данные для получения сведений из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1caab-277">However, in your receiver, you send this information into a table or a queue that can process the received data to get information from SharePoint.</span></span> 

<span data-ttu-id="1caab-278">С помощью этих данных вы можете составить URL-адрес и использовать API [GetChanges](https://msdn.microsoft.com/ru-RU/library/office/dn531433.aspx#bk_ListGetChanges) для просмотра последних изменений.</span><span class="sxs-lookup"><span data-stu-id="1caab-278">With this data, you can construct the URL and use the [GetChanges](https://msdn.microsoft.com/ru-RU/library/office/dn531433.aspx#bk_ListGetChanges) API to get the latest changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1caab-279">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1caab-279">Next steps</span></span>

<span data-ttu-id="1caab-280">В этой статье мы использовали клиент Postman и простой веб-API для создания подписки и получения уведомлений веб-перехватчиков из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1caab-280">In this article, you used Postman client and a simple web API to subscribe and receive webhook notifications from SharePoint.</span></span>

<span data-ttu-id="1caab-281">Теперь ознакомьтесь с [базовой реализацией веб-перехватчиков SharePoint](./webhooks-reference-implementation.md), в которой для обработки сведений, получения изменений из SharePoint и их обратной передачи в список SharePoint используются Очереди хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1caab-281">Next, take a look at [SharePoint webhooks sample reference implementation](./webhooks-reference-implementation.md), which shows an end-to-end sample that uses Azure Storage Queues to process the information, get changes from SharePoint, and push those changes back into a SharePoint list.</span></span>
