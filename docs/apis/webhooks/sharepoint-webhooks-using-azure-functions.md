---
title: "Использование решения \"Функции Azure\" с веб-перехватчиками SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ea3ed94dd41c6da41b2cbeb6b5291211804c4dfc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="using-azure-functions-with-sharepoint-webhooks"></a><span data-ttu-id="0c949-102">Использование решения "Функции Azure" с веб-перехватчиками SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c949-102">Using Azure Functions with SharePoint webhooks</span></span>
<span data-ttu-id="0c949-103">Благодаря решению [Функции Azure](https://docs.microsoft.com/ru-RU/azure/azure-functions/functions-overview) доступен удобный способ размещать веб-перехватчики SharePoint. Достаточно добавить код веб-перехватчика на языке C# или JavaScript через браузер, и Azure займется размещением и масштабированием функции.</span><span class="sxs-lookup"><span data-stu-id="0c949-103">[Azure functions](https://docs.microsoft.com/ru-RU/azure/azure-functions/functions-overview) offer an easy way to host your SharePoint webhooks: you can simply add your webhook C# or Javascript code via the browser and Azure will take care of the hosting and scaling of your function!</span></span> <span data-ttu-id="0c949-104">В этом руководстве показано, как настроить и использовать функции Azure для веб-перехватчиков.</span><span class="sxs-lookup"><span data-stu-id="0c949-104">This guide shows how to setup and use Azure Functions for your webhooks.</span></span>

## <a name="create-a-an-azure-function-app"></a><span data-ttu-id="0c949-105">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="0c949-105">Create a an Azure Function App</span></span>
<span data-ttu-id="0c949-106">Для начала необходимо создать приложение-функцию Azure — специальный вид веб-приложений Azure, предназначенный для размещения функций в Azure.</span><span class="sxs-lookup"><span data-stu-id="0c949-106">The first step you'll need to do is creating an Azure Function App, which is a special kind of Azure Web App focused on hosting Azure Functions.</span></span> <span data-ttu-id="0c949-107">Перейдите на сайт [https://portal.azure.com](https://portal.azure.com), нажмите "Создать" и найдите элемент "Приложение-функция".</span><span class="sxs-lookup"><span data-stu-id="0c949-107">Navigate to [https://portal.azure.com](https://portal.azure.com), click on the "New" and search for "Function app":</span></span>

![Создание приложения-функции Azure](../../images/webhook-azure-function0.png)

<span data-ttu-id="0c949-109">Выберите элемент "Приложение-функция" и укажите сведения, необходимые для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="0c949-109">Select "Function App" and complete the information needed to create the Function App:</span></span>

![Ввод сведений о приложении-функции Azure](../../images/webhook-azure-function1.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="0c949-111">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="0c949-111">Create an Azure Function</span></span>
<span data-ttu-id="0c949-112">Теперь, когда мы подготовили приложение для размещения функций, вы можете создать первую функцию Azure с помощью ссылки "Новая функция".</span><span class="sxs-lookup"><span data-stu-id="0c949-112">Now that the app to host the functions is ready you can continue with creating your first Azure Function by clicking on the "New Function" link:</span></span>

![Добавление функции Azure](../../images/webhook-azure-function2.png)

<span data-ttu-id="0c949-114">Вам будет предложено создать функцию на основе шаблона. В случае веб-перехватчиков SharePoint нам потребуется функция, активируемая с помощью HTTP. В нашем примере мы будем писать код на C#, поэтому воспользуемся шаблоном функции **HttpTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="0c949-114">This will offer you to start your function from a template, in the case of SharePoint webhooks we will need a HTTP triggered function and since we'll be writing C# code in our sample this means we're using the **HttpTrigger-CSharp** function template.</span></span> <span data-ttu-id="0c949-115">Учитывая, что службы веб-перехватчиков SharePoint должны поддерживать анонимный вызов, важно изменить значение параметра **Уровень авторизации** на **Анонимный**.</span><span class="sxs-lookup"><span data-stu-id="0c949-115">Given that SharePoint webhook services need to be anonymously callable it's important to switch the **Authorization level** to **Anonymous**.</span></span>

![Выбор шаблона функции Azure](../../images/webhook-azure-function3.png)

> [!NOTE]
> - <span data-ttu-id="0c949-117">В настоящее время шаблон **GenericWebHook** не работает с веб-перехватчиками SharePoint, но команда разработчиков SharePoint знает об этой проблеме и исправит ее.</span><span class="sxs-lookup"><span data-stu-id="0c949-117">Using the **GenericWebHook** template currently does not yet work for SharePoint webhooks but the SharePoint product team is aware of this problem and will address it.</span></span>
> - <span data-ttu-id="0c949-118">Если при использовании веб-перехватчика на основе функции Azure возникают ошибки "Не удалось проверить URL-адрес уведомления", установите уровень авторизации **Функция** и настройте анонимный доступ для функции.</span><span class="sxs-lookup"><span data-stu-id="0c949-118">If you get "Failed to validate the notification URL" errors when using your Azure function based webhook you might be able to resolve this by setting the Authorization level to **Function** and define your function for anonymous access</span></span>

<span data-ttu-id="0c949-119">В результате получится "стандартная" функция Azure на C#. ![Стандартная функция Azure](../../images/webhook-azure-function4.png)</span><span class="sxs-lookup"><span data-stu-id="0c949-119">The result will be a "default" Azure Function written in C# ![The default Azure Function](../../images/webhook-azure-function4.png)</span></span>

<span data-ttu-id="0c949-120">В нашем случае эта функция Azure должна работать как служба веб-перехватчиков SharePoint, поэтому нам потребуется реализовать на C# следующие операции:</span><span class="sxs-lookup"><span data-stu-id="0c949-120">In our case we want this Azure Function to behave as a SharePoint webhook service, so we'll need to implement the following in C#:</span></span>
- <span data-ttu-id="0c949-121">1. Возвращение параметра validationtoken, если он указан в качестве параметра URL-адреса в вызове.</span><span class="sxs-lookup"><span data-stu-id="0c949-121">Return the validationtoken if specified as URL parameter to the call.</span></span> <span data-ttu-id="0c949-122">Необходимость этого описана [здесь](./lists/create-subscription.md), а SharePoint ожидает ответ в течение 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="0c949-122">This is needed as described [here](./lists/create-subscription.md) and SharePoint expects the reply to happen within 5 seconds.</span></span> 
- <span data-ttu-id="0c949-p105">2. Обработка уведомления веб-перехватчика JSON. В приведенном ниже примере мы решили сохранять код JSON в очереди хранилища, чтобы веб-задание Azure могло обрабатывать его асинхронно. В зависимости от ваших потребностей вы также можете обеспечить обработку уведомления непосредственно в службе веб-перехватчиков, но помните, что все вызовы службы веб-перехватчиков должны завершаться в течение 5 секунд, поэтому рекомендуем использовать асинхронную модель.</span><span class="sxs-lookup"><span data-stu-id="0c949-p105">Process the JSON webhook notification. In below sample we've opted to store the JSON in a storage queue so that an Azure Web Job can pick it up and process it asynchronously. Depending on your needs you could also process the notification directly in your webhook service, but keep in mind that all webhook service calls need to complete in 5 seconds, hence using an asynchronous model is recommended</span></span>

<span data-ttu-id="0c949-126">Вы можете добиться этого, заменив код по умолчанию следующим кодом (укажите свою строку подключения для учетной записи хранения и измените имя очереди, если вы используете другую):</span><span class="sxs-lookup"><span data-stu-id="0c949-126">You can achieve above by replacing the default code by below code (please enter your storage account connection string and update the queue name if you're using a different one):</span></span>

```
#r "Newtonsoft.Json"
#r "Microsoft.WindowsAzure.Storage"

using System;
using System.Net;
using Newtonsoft.Json;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"Webhook was triggered!");

    // Grab the validationToken URL parameter
    string validationToken = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "validationtoken", true) == 0)
        .Value;
    
    // If a validation token is present, we need to respond within 5 seconds by  
    // returning the given validation token. This only happens when a new 
    // web hook is being added
    if (validationToken != null)
    {
      log.Info($"Validation token {validationToken} received");
      var response = req.CreateResponse(HttpStatusCode.OK);
      response.Content = new StringContent(validationToken);
      return response;
    }

    log.Info($"SharePoint triggered our webhook...great :-)");
    var content = await req.Content.ReadAsStringAsync();
    log.Info($"Received following payload: {content}");

    var notifications = JsonConvert.DeserializeObject<ResponseModel<NotificationModel>>(content).Value;
    log.Info($"Found {notifications.Count} notifications");

    if (notifications.Count > 0)
    {
        log.Info($"Processing notifications...");
        foreach(var notification in notifications)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("<YOUR STORAGE ACCOUNT>");
            // Get queue... create if does not exist.
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
            CloudQueue queue = queueClient.GetQueueReference("sharepointlistwebhookeventazuread");
            queue.CreateIfNotExists();

            // add message to the queue
            string message = JsonConvert.SerializeObject(notification);
            log.Info($"Before adding a message to the queue. Message content: {message}");
            queue.AddMessage(new CloudQueueMessage(message));
            log.Info($"Message added :-)");
        }
    }

    // if we get here we assume the request was well received
    return new HttpResponseMessage(HttpStatusCode.OK);
}


// supporting classes
public class ResponseModel<T>
{
    [JsonProperty(PropertyName = "value")]
    public List<T> Value { get; set; }
}

public class NotificationModel
{
    [JsonProperty(PropertyName = "subscriptionId")]
    public string SubscriptionId { get; set; }

    [JsonProperty(PropertyName = "clientState")]
    public string ClientState { get; set; }

    [JsonProperty(PropertyName = "expirationDateTime")]
    public DateTime ExpirationDateTime { get; set; }

    [JsonProperty(PropertyName = "resource")]
    public string Resource { get; set; }

    [JsonProperty(PropertyName = "tenantId")]
    public string TenantId { get; set; }

    [JsonProperty(PropertyName = "siteUrl")]
    public string SiteUrl { get; set; }

    [JsonProperty(PropertyName = "webId")]
    public string WebId { get; set; }
}

public class SubscriptionModel
{
    [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
    public string Id { get; set; }

    [JsonProperty(PropertyName = "clientState", NullValueHandling = NullValueHandling.Ignore)]
    public string ClientState { get; set; }

    [JsonProperty(PropertyName = "expirationDateTime")]
    public DateTime ExpirationDateTime { get; set; }

    [JsonProperty(PropertyName = "notificationUrl")]
    public string NotificationUrl {get;set;}

    [JsonProperty(PropertyName = "resource", NullValueHandling = NullValueHandling.Ignore)]
    public string Resource { get; set; }
}
```

## <a name="configure-your-azure-function"></a><span data-ttu-id="0c949-127">Настройка функции Azure</span><span class="sxs-lookup"><span data-stu-id="0c949-127">Configure your Azure Function</span></span>
<span data-ttu-id="0c949-128">Так как мы выбрали правильный шаблон, наша конфигурация почти готова. Остается только изменить значение параметра **Разрешенные методы HTTP** на **Выбранные методы**, а затем разрешить только метод HTTP **POST**.</span><span class="sxs-lookup"><span data-stu-id="0c949-128">Since we've chosen the correct template to start from our configuration is almost complete, the only thing you need to still do is to switch the **Allowed HTTP methods** to **Selected methods** and then only allow the **POST** HTTP method.</span></span> <span data-ttu-id="0c949-129">Кроме того, убедитесь, что для параметра **Режим** задано значение **Стандартный**, а для параметра **Уровень авторизации** — **Анонимный**.</span><span class="sxs-lookup"><span data-stu-id="0c949-129">Also cross check that **Mode** is equal to **Standard** and **Authorization level** is set to **Anonymous**.</span></span>

![Параметры функции Azure](../../images/webhook-azure-function5.png)

## <a name="test-your-azure-function"></a><span data-ttu-id="0c949-131">Тестирование функции Azure</span><span class="sxs-lookup"><span data-stu-id="0c949-131">Test your Azure Function</span></span>
<span data-ttu-id="0c949-132">Все готово к тестированию вашей первой функции Azure. Откройте экран **Разработка**.</span><span class="sxs-lookup"><span data-stu-id="0c949-132">You're now all set for your first Azure Function test: navigate to the **Develop** screen.</span></span> <span data-ttu-id="0c949-133">Нажмите значок **Тестирование**, чтобы открыть панель тестирования в правой части экрана, и добавьте параметр URL-адреса validationtoken со случайной строкой в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="0c949-133">Click on the **Test** icon to pop-up the test pane at the right side, add a URL parameter "validationtoken" with a random string as value.</span></span> <span data-ttu-id="0c949-134">Так мы имитируем то, как SharePoint вызывает службу веб-перехватчиков при проверке добавления веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="0c949-134">Using this setup we're mimicking the behavior of SharePoint calling your web hook service when validating a new webhook addition.</span></span> <span data-ttu-id="0c949-135">Нажмите **Запустить**, чтобы начать тестирование. Если все пройдет без проблем, вы увидите в разделе журналов, что служба была вызвана и вернула переданное значение с ответом HTTP 200:</span><span class="sxs-lookup"><span data-stu-id="0c949-135">Click on **Run** to test...if everything goes well you'll see in the logs section that your service was called and that it returned the passed value with a HTTP 200 response:</span></span>

![Тестирование функции Azure](../../images/webhook-azure-function6.png)

## <a name="grab-the-webhook-url-to-use-in-your-implementation"></a><span data-ttu-id="0c949-137">Выбор URL-адреса веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="0c949-137">Grab the webhook URL to use in your implementation</span></span>
<span data-ttu-id="0c949-p108">Теперь нам необходимо сообщить SharePoint, какой URL-адрес веб-перехватчика мы используем. Для начала скопируем URL-адрес функции Azure:</span><span class="sxs-lookup"><span data-stu-id="0c949-p108">We'll need to let SharePoint now what webhook URL we're using. To so let's start by copying the Azure Function URL:</span></span>

![Коды авторизации функций Azure](../../images/webhook-azure-function8.png)

<span data-ttu-id="0c949-141">Во избежание несанкционированного использования функции Azure при ее вызове необходимо указывать код.</span><span class="sxs-lookup"><span data-stu-id="0c949-141">To avoid unathorized usage of your Azure Function the caller will need to specify a code when calling your function.</span></span> <span data-ttu-id="0c949-142">Этот код можно получить на экране **Управление**:</span><span class="sxs-lookup"><span data-stu-id="0c949-142">This code can be retreived via the **Manage** screen:</span></span>

![URL-адрес веб-перехватчика функции Azure](../../images/webhook-azure-function7.png)

<span data-ttu-id="0c949-144">Поэтому в нашем случае будет использоваться следующий URL-адрес веб-перехватчика: `https://pnp-functions.azurewebsites.net/api/spwebhookfunction?code=wyx9iAxp3o7fdGFZTbnp9Kfc5o2UhlzwgSOT/XGGM6QZcdYYa/o9aw==`</span><span class="sxs-lookup"><span data-stu-id="0c949-144">So in our case the webhook URL to use is the following: `https://pnp-functions.azurewebsites.net/api/spwebhookfunction?code=wyx9iAxp3o7fdGFZTbnp9Kfc5o2UhlzwgSOT/XGGM6QZcdYYa/o9aw==`</span></span>



