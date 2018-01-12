---
title: "Создание полноценного макета сайта SharePoint с помощью модуля подготовки PnP"
description: "Создание полноценного макета сайта SharePoint с помощью модуля подготовки PnP"
ms.date: 12/14/2017
ms.openlocfilehash: 303aca9f0103634e247ec75a0323321a77709113
ms.sourcegitcommit: 28690b54f1ef7c811d64393d2eaaff0a8635cc72
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a><span data-ttu-id="e47b4-103">Вызов модуля подготовки PnP из скрипта на сайте</span><span class="sxs-lookup"><span data-stu-id="e47b4-103">Calling the PnP Provisioning Engine from a Site Script</span></span>

> [!NOTE]
> <span data-ttu-id="e47b4-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="e47b4-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="e47b4-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="e47b4-105">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="e47b4-106">Макеты сайтов — удобный способ стандартизации внешнего вида и функций семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="e47b4-106">Site Designs offer a great way to standardize the look and feel of your site collections.</span></span> <span data-ttu-id="e47b4-107">Но если вы захотите сделать больше (например, добавить на каждую страницу нижний колонтитул), то заметите, что макеты сайтов не предоставляют такой возможности.</span><span class="sxs-lookup"><span data-stu-id="e47b4-107">But if you want to take this one step further, by for instance adding a footer to every page, you might notice that Site Designs do not offer you that option.</span></span> <span data-ttu-id="e47b4-108">С помощью модуля подготовки PnP вы можете создать шаблон, позволяющий подготовить настройщик приложений для сайта.</span><span class="sxs-lookup"><span data-stu-id="e47b4-108">With the PnP Provisioning engine you can hover create a template which allows you to provision an application customizer to a site.</span></span> <span data-ttu-id="e47b4-109">Затем этот настройщик приложений может зарегистрировать нижний колонтитул на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="e47b4-109">This application customizer then can register a footer on every page.</span></span> <span data-ttu-id="e47b4-110">Из этой статьи вы узнаете, как создать макет сайта, применяющий к сайту шаблон подготовки PnP, который добавит настройщик приложений для отрисовки нижнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="e47b4-110">In this article you will learn how to create a site design that applies a PnP Provisioning Template to a site which in turn will add an application customizer to render a footer.</span></span>

<span data-ttu-id="e47b4-111">При настройке мы используем следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="e47b4-111">We use the following components in our setup:</span></span>

1. <span data-ttu-id="e47b4-112">макет и скрипт сайта;</span><span class="sxs-lookup"><span data-stu-id="e47b4-112">A Site Design and a Site Script</span></span>
1. <span data-ttu-id="e47b4-113">поток Microsoft Flow;</span><span class="sxs-lookup"><span data-stu-id="e47b4-113">A Microsoft Flow</span></span>
1. <span data-ttu-id="e47b4-114">очередь службы хранилища Azure;</span><span class="sxs-lookup"><span data-stu-id="e47b4-114">An Azure Storage Queue</span></span>
1. <span data-ttu-id="e47b4-115">функция Azure;</span><span class="sxs-lookup"><span data-stu-id="e47b4-115">An Azure Function</span></span>
1. <span data-ttu-id="e47b4-116">решение SPFX;</span><span class="sxs-lookup"><span data-stu-id="e47b4-116">An SPFX Solution</span></span>
1. <span data-ttu-id="e47b4-117">шаблон подготовки PnP;</span><span class="sxs-lookup"><span data-stu-id="e47b4-117">A PnP Provisioning Template</span></span>
1. <span data-ttu-id="e47b4-118">скрипт PnP PowerShell;</span><span class="sxs-lookup"><span data-stu-id="e47b4-118">A PnP PowerShell Script</span></span>
1. <span data-ttu-id="e47b4-119">AppId и AppSecret с правами администратора для клиента.</span><span class="sxs-lookup"><span data-stu-id="e47b4-119">An AppId and AppSecret with administration rights on your tenant.</span></span>

<span data-ttu-id="e47b4-120">Все эти компоненты необходимы, чтобы вызвать код подготовки PnP контролируемым образом сразу после создания сайта и применения макета.</span><span class="sxs-lookup"><span data-stu-id="e47b4-120">We need all these component so we can trigger the PnP Provisioning code in a controller manner right after the site has been created and the Site Design is being applied.</span></span>

## <a name="setting-up-app-only-access-to-your-tenant"></a><span data-ttu-id="e47b4-121">Настройка доступа к клиенту только для приложений</span><span class="sxs-lookup"><span data-stu-id="e47b4-121">Setting up App Only Access to your tenant</span></span>

<span data-ttu-id="e47b4-122">Для этого необходимо открыть в клиенте 2 разные страницы (на обычном сайте и на сайте администрирования SharePoint).</span><span class="sxs-lookup"><span data-stu-id="e47b4-122">This requires that you open 2 different pages on your tenant, one located in a normal site, the other located in your SharePoint Administration site.</span></span>

1. <span data-ttu-id="e47b4-123">Перейдите по следующему URL-адресу в клиенте: https://[ваш_клиент].sharepoint.com/_layouts/appregnew.aspx (вы можете перейти на любой сайт, но пока что выберите корневой).</span><span class="sxs-lookup"><span data-stu-id="e47b4-123">Navigate to following URL in your tenant: https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx (you can navigate to any site, but for now pick the root site)</span></span>
1. <span data-ttu-id="e47b4-124">Нажмите обе кнопки **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-124">Click both **Generate** buttons</span></span>
1. <span data-ttu-id="e47b4-125">Укажите название приложения, например "Подготовка сайта".</span><span class="sxs-lookup"><span data-stu-id="e47b4-125">Enter a title for your App, for instance "Site Provisioning"</span></span>
1. <span data-ttu-id="e47b4-126">В поле "Домен приложения" введите **localhost**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-126">Enter **localhost** as the App Domain</span></span>
1. <span data-ttu-id="e47b4-127">В поле "URI перенаправления" введите **https://localhost**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-127">Enter **http://localhost:3000/token** as the Redirect URI.</span></span>

    ![Создание приложения](images/pnpprovisioning-createapponly.png)

1. <span data-ttu-id="e47b4-129">Нажмите кнопку **Создать** и скопируйте значения из полей **Идентификатор клиента** и **Секрет клиента**, так как они потребуются позже.</span><span class="sxs-lookup"><span data-stu-id="e47b4-129">Click **Create** and copy the values for **Client Id** and **Client Secret** as you will need them later</span></span>

<span data-ttu-id="e47b4-130">Теперь мы предоставим этому приложению надлежащий уровень доступа к клиенту.</span><span class="sxs-lookup"><span data-stu-id="e47b4-130">Now we will trust this app to have the appropriate access to your tenant:</span></span>
1. <span data-ttu-id="e47b4-131">Перейдите на страницу https://[ваш_клиент]-admin.sharepoint.com/_layouts/appinv.aspx (обратите внимание на строку "-admin" в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="e47b4-131">Navigate to https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx (notice the -admin in the URL)</span></span>
1. <span data-ttu-id="e47b4-132">Вставьте скопированный ранее идентификатор клиента в поле **Код приложения** и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-132">Paste in the Client Id you copied above into the **App Id** field and select **Lookup**</span></span>
1. <span data-ttu-id="e47b4-133">Вставьте следующий код XML в поле **XML-запрос разрешения**:</span><span class="sxs-lookup"><span data-stu-id="e47b4-133">Paste the following XML in the **Permission Request XML** field:</span></span>

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. <span data-ttu-id="e47b4-134">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-134">Select **Create**</span></span>
1. <span data-ttu-id="e47b4-135">Вам будет предложено доверять приложению.</span><span class="sxs-lookup"><span data-stu-id="e47b4-135">You will receive a question if you want to trust this app.</span></span> <span data-ttu-id="e47b4-136">Дайте согласие, нажав кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-136">Confirm this by selecting **Trust It**</span></span>


## <a name="creating-the-azure-storage-queue"></a><span data-ttu-id="e47b4-137">Создание очереди службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="e47b4-137">Creating the Azure Storage Queue</span></span>

<span data-ttu-id="e47b4-138">В этом случае мы будем использовать очередь службы хранилища Azure, чтобы получать сообщения от Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="e47b4-138">In this scenario we will use an Azure Storage Queue to receive messages from a Microsoft Flow.</span></span> <span data-ttu-id="e47b4-139">Каждый раз, когда в очереди хранилища появляется сообщение, вызывается функция Azure для выполнения скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e47b4-139">Every time a message shows up in the Storage Queue an Azure Function will get triggered to execute a PowerShell script.</span></span> <span data-ttu-id="e47b4-140">Но для начала настроим очередь хранилища.</span><span class="sxs-lookup"><span data-stu-id="e47b4-140">But let us set up the Storage Queue first:</span></span>

1. <span data-ttu-id="e47b4-141">Откройте портал Azure по адресу https://portal.azure.com и войдите.</span><span class="sxs-lookup"><span data-stu-id="e47b4-141">Navigate to the Azure portal at https://portal.azure.com and log in.</span></span>
1. <span data-ttu-id="e47b4-142">Нажмите кнопку **+ Создать**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-142">Choose **+ New**</span></span>
1. <span data-ttu-id="e47b4-143">Выберите **Хранение** в списках Azure Marketplace, а затем выберите элемент **Учетная запись хранения — BLOB-объект, файл, таблица, очередь** в столбце "Популярные".</span><span class="sxs-lookup"><span data-stu-id="e47b4-143">Select **Storage** from the Azure Marketplace listings and select **Storage account - blob, file, table, queue** in the Featured column</span></span>
1. <span data-ttu-id="e47b4-144">Укажите значения в обязательных полях.</span><span class="sxs-lookup"><span data-stu-id="e47b4-144">Provide values for the required fields as requested.</span></span> <span data-ttu-id="e47b4-145">Установите флажок **Закрепить на панели мониторинга**, чтобы учетную запись было легко найти позже, и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-145">Make sure to select **Pin to dashboard** for easy location later and click **Create**.</span></span> <span data-ttu-id="e47b4-146">Начнется создание учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e47b4-146">The storage account is being created.</span></span> <span data-ttu-id="e47b4-147">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="e47b4-147">This might take a few minutes.</span></span>
1. <span data-ttu-id="e47b4-148">Откройте учетную запись хранения после ее создания и перейдите к разделу **Очереди** в области навигации.</span><span class="sxs-lookup"><span data-stu-id="e47b4-148">Open the Storage Account after it has been created and navigate to **Queues** in the navigation</span></span>
1. <span data-ttu-id="e47b4-149">Нажмите кнопку **+ Очередь** в верхней части основной области экрана.</span><span class="sxs-lookup"><span data-stu-id="e47b4-149">Choose **+ Queue** at the top of the main area of the screen.</span></span>
1. <span data-ttu-id="e47b4-150">Введите имя **pnpprovisioningqueue** или другое имя, соответствующее действующему стандарту именования.</span><span class="sxs-lookup"><span data-stu-id="e47b4-150">Enter **pnpprovisioningqueue** as the name or enter your own following the naming standard that is enforced.</span></span> <span data-ttu-id="e47b4-151">Запишите имя очереди, так как оно потребуется позже, при создании функции Azure.</span><span class="sxs-lookup"><span data-stu-id="e47b4-151">Make a note of the queue name as you need this value later when creating the Azure Function.</span></span>
1. <span data-ttu-id="e47b4-152">Перейдите к разделу **Ключи доступа** и запишите **имя учетной записи хранения** и **значение ключа key1**. Они потребуются на следующем этапе — при создании потока.</span><span class="sxs-lookup"><span data-stu-id="e47b4-152">Navigate to **Access Keys** and make note of the **Storage Account Name** and the **key1 Key value**, you will need those values in the next step where you create the flow.</span></span>


## <a name="the-flow"></a><span data-ttu-id="e47b4-153">Поток</span><span class="sxs-lookup"><span data-stu-id="e47b4-153">The Flow</span></span>

<span data-ttu-id="e47b4-154">Чтобы поместить сообщение в очередь, необходимо создать поток.</span><span class="sxs-lookup"><span data-stu-id="e47b4-154">In order to put a message on the queue we have to create a flow.</span></span> 

1. <span data-ttu-id="e47b4-155">Перейдите на сайт **https://flow.microsoft.com**, войдите и создайте поток, выбрав команду **Создать с нуля** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e47b4-155">Navigate to **https://flow.microsoft.com**, log in and create a new flow by clicking **Create from Blank** at the top.</span></span>
1. <span data-ttu-id="e47b4-156">Нажмите **Поиск среди сотен соединителей и триггеров**, чтобы выбрать триггер.</span><span class="sxs-lookup"><span data-stu-id="e47b4-156">Click **Search hundreds of connectors and triggers** to select your trigger</span></span>
1. <span data-ttu-id="e47b4-157">Введите слово **Запрос** и выберите **Запрос: при получении HTTP-запроса**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-157">Search for **Request** and select **Request - When a HTTP Request is received**</span></span>
1. <span data-ttu-id="e47b4-158">Введите следующий код JSON в теле запроса:</span><span class="sxs-lookup"><span data-stu-id="e47b4-158">Enter the following JSON as your request body:</span></span>

    ```json
    {
        "type": "object",
        "properties": {
            "webUrl": {
                "type": "string"
            },
            "parameters": {
                "type": "object",
                "properties": {
                    "event": {
                        "type": "string"
                    },
                    "product": {
                        "type": "string"
                    }
                }
            }
        }
    }
    ``` 

1. <span data-ttu-id="e47b4-159">Нажмите кнопку **+ Новый этап** и выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-159">Select **+ New Step** and select **Add an action**</span></span>
1. <span data-ttu-id="e47b4-160">Выполните поиск по запросу **Очереди Azure** и выберите **Очереди Azure: поместить сообщение в очередь**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-160">Search for **Azure Queues** and select **Azure Queues - Put a message on a queue**</span></span>
1. <span data-ttu-id="e47b4-161">Введите имя подключения. Это может быть любое описательное название.</span><span class="sxs-lookup"><span data-stu-id="e47b4-161">Enter a name for the connection, this can be anything descriptive</span></span>
1. <span data-ttu-id="e47b4-162">Введите имя учетной записи хранения, скопированное из предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="e47b4-162">Enter the storage account name you copied in the previous section</span></span>
1. <span data-ttu-id="e47b4-163">Введите открытый ключ хранилища, представляющий собой **значение ключа Key1** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e47b4-163">Enter the storage shared key, which is the value of the **Key1 key value** of your storage account.</span></span>
1. <span data-ttu-id="e47b4-164">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-164">Click  **Create**.</span></span>
1. <span data-ttu-id="e47b4-165">Выберите имя очереди **pnpprovisioningqueue**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-165">Select **pnpprovisioningqueue** as the Queue Name.</span></span>
1. <span data-ttu-id="e47b4-166">В тексте для этапа 4 мы указали входящий параметр с именем webUrl.</span><span class="sxs-lookup"><span data-stu-id="e47b4-166">In the body specified in step 4 we specified an incoming parameter called webUrl.</span></span> <span data-ttu-id="e47b4-167">Мы поместим значение этого параметра в очередь.</span><span class="sxs-lookup"><span data-stu-id="e47b4-167">We will put the value of that parameter on the queue.</span></span> <span data-ttu-id="e47b4-168">Щелкните поле **Сообщение** и выберите **webUrl** в средстве выбора динамического контента.</span><span class="sxs-lookup"><span data-stu-id="e47b4-168">Click in the **message** field and select **webUrl** from the Dynamic Content picker.</span></span>
1. <span data-ttu-id="e47b4-169">Нажмите кнопку **Сохранить поток**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-169">Click **Save Flow**.</span></span> <span data-ttu-id="e47b4-170">При этом будет создан URL-адрес, который мы скопируем на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="e47b4-170">This will generate the URL we will copy in the next step.</span></span>
1. <span data-ttu-id="e47b4-171">Щелкните первый этап потока ("При получении HTTP-запроса") и скопируйте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e47b4-171">Click on the first step in your flow ('When an HTTP request is received') and copy the URL.</span></span> <span data-ttu-id="e47b4-172">Он потребуется нам для тестирования потока и создания макета сайта.</span><span class="sxs-lookup"><span data-stu-id="e47b4-172">We will need that to test and later on in our Site Design.</span></span>
1. <span data-ttu-id="e47b4-173">Сохраните поток.</span><span class="sxs-lookup"><span data-stu-id="e47b4-173">Save your flow.</span></span>

<span data-ttu-id="e47b4-174">Он должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="e47b4-174">Your registry should look like this: </span></span>

![Поток](images/pnpprovisioning-flow-overview.png)

## <a name="testing-the-flow"></a><span data-ttu-id="e47b4-176">Тестирование потока</span><span class="sxs-lookup"><span data-stu-id="e47b4-176">Testing the flow</span></span>

<span data-ttu-id="e47b4-177">Чтобы тестировать поток, необходимо отправить POST-запрос.</span><span class="sxs-lookup"><span data-stu-id="e47b4-177">In order to test your flow you have will have to make a post request.</span></span> <span data-ttu-id="e47b4-178">На компьютере с Windows это проще всего сделать с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e47b4-178">The easiest for that, if you are on a Windows PC, is to use PowerShell:</span></span>

```powershell
$uri = "[the URI you copied in step 8 when creating the flow]"
$body = "{webUrl:'somesiteurl'}
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

<span data-ttu-id="e47b4-179">Если теперь перейти на главный экран потока, отобразится журнал запусков.</span><span class="sxs-lookup"><span data-stu-id="e47b4-179">If you now navigate to the main screen of your flow you will see a run history.</span></span> <span data-ttu-id="e47b4-180">В случае успешного выполнения должно отображаться состояние "Успешно".</span><span class="sxs-lookup"><span data-stu-id="e47b4-180">If everything went okay it should say 'Succeeded'.</span></span>
<span data-ttu-id="e47b4-181">Теперь перейдите к очереди, созданной только что в Azure, и нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-181">Now navigate to the queue you just created in Azure and click **Refresh**.</span></span> <span data-ttu-id="e47b4-182">Должна отображаться запись, указывающая, что вы успешно вызвали поток.</span><span class="sxs-lookup"><span data-stu-id="e47b4-182">There should be an entry showing that you correctly invoked the Flow.</span></span>

## <a name="provision-the-spfx-solution"></a><span data-ttu-id="e47b4-183">Подготовка решения SPFX</span><span class="sxs-lookup"><span data-stu-id="e47b4-183">Provision the SPFX Solution</span></span>

<span data-ttu-id="e47b4-184">В этом пошаговом руководстве мы будем использовать имеющееся решение SPFX, доступное по адресу https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer.</span><span class="sxs-lookup"><span data-stu-id="e47b4-184">For this walkthrough we are going to use an existing SPFX solution which is available at https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer</span></span>

<span data-ttu-id="e47b4-185">Выполните действия, описанные в файле README.MD из этого репозитория, чтобы собрать и подготовить решение.</span><span class="sxs-lookup"><span data-stu-id="e47b4-185">Follow the steps as provided in the README.MD available in that repository to build and provision your solution.</span></span>

# <a name="create-a-pnp-provisioning-template"></a><span data-ttu-id="e47b4-186">Создание шаблона подготовки PnP</span><span class="sxs-lookup"><span data-stu-id="e47b4-186">Create a PnP Provisioning Template</span></span>

<span data-ttu-id="e47b4-187">Скопируйте приведенный ниже код XML в новый файл и сохраните его с именем FlowDemoTemplate.xml.</span><span class="sxs-lookup"><span data-stu-id="e47b4-187">Copy the following XML to a new file and save the file as FlowDemoTemplate.xml</span></span>

```xml
<?xml version="1.0"?>
<pnp:Provisioning xmlns:pnp="http://schemas.dev.office.com/PnP/2017/05/ProvisioningSchema">
  <pnp:Preferences Generator="OfficeDevPnP.Core, Version=2.20.1711.0, Culture=neutral, PublicKeyToken=3751622786b357c2" />
  <pnp:Templates ID="CONTAINER-FLOWDEMO">
    <pnp:ProvisioningTemplate ID="TEMPLATE-FLOWDEMO" Version="1" BaseSiteTemplate="GROUP#0" Scope="RootSite">
      <pnp:CustomActions>
        <pnp:WebCustomActions>
          <pnp:CustomAction Name="spfx-react-app-customizer" Description="Custom action for Application Customizer" Location="ClientSideExtension.ApplicationCustomizer" Title="spfx-react-app-customizer" Sequence="0" Rights="" RegistrationType="None" ClientSideComponentId="67fd1d01-84e8-4fbf-85bd-4b80768c6080" ClientSideComponentProperties="{&quot;SourceTermSetName&quot;:&quot;Regions&quot;}" />
        </pnp:WebCustomActions>
      </pnp:CustomActions>
    </pnp:ProvisioningTemplate>
</pnp:Provisioning>
```

> [!NOTE]
> <span data-ttu-id="e47b4-188">Шаблон добавляет дополнительное действие на сайт, к которому он применяется.</span><span class="sxs-lookup"><span data-stu-id="e47b4-188">The template adds a custom action to the the web it is being applied to.</span></span> <span data-ttu-id="e47b4-189">Он ссылается на свойство ClientSideComponentId, поступающее из подготовленного ранее решения SPFX.</span><span class="sxs-lookup"><span data-stu-id="e47b4-189">It refers to ClientSideComponentId which is the one coming from the SPFX Solution you provisioned earlier.</span></span> <span data-ttu-id="e47b4-190">Чтобы запустить эту демонстрацию с собственным решением SPFX, необходимо изменить значения атрибутов ClientSideComponentId и (необязательно) ClientSideComponentProperties в XML-файле.</span><span class="sxs-lookup"><span data-stu-id="e47b4-190">If you run this demo with your own SPFX Solution you will have to change the ClientSideComponentId and optionally the ClientSideComponentProperties attribute values in the XML.</span></span>

## <a name="create-the-azure-function"></a><span data-ttu-id="e47b4-191">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="e47b4-191">Create an Azure Function</span></span>

1. <span data-ttu-id="e47b4-192">Перейдите на портал Azure по адресу https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e47b4-192">Navigate to the Azure Portal at https://portal.azure.com.</span></span>
1. <span data-ttu-id="e47b4-193">Выполните поиск по запросу "Приложение-функция" и создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="e47b4-193">Search for 'Function App' and create a new Function App.</span></span> <span data-ttu-id="e47b4-194">В поле **Хранилище** выберите **Использовать имеющееся**, а затем укажите созданную ранее учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e47b4-194">In the **Storage** field select **Use existing** and select your previously created storage account.</span></span> <span data-ttu-id="e47b4-195">При необходимости задайте другие значения.</span><span class="sxs-lookup"><span data-stu-id="e47b4-195">Set the other values as required.</span></span>
1. <span data-ttu-id="e47b4-196">После создания приложения-функции откройте его и выберите **Функции**, а затем нажмите **Создать функцию**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-196">After the function app has been created open it and select **Functions**, then select **New function**.</span></span>

  ![Создание функции](images/pnpprovisioning-create-function.png)

1. <span data-ttu-id="e47b4-198">В раскрывающемся списке "Язык" выберите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-198">From the Language drop-down, select **PowerShell**.</span></span>
1. <span data-ttu-id="e47b4-199">Выберите **QueueTrigger — PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-199">Select **QueueTrigger - PowerShell**.</span></span>
1. <span data-ttu-id="e47b4-200">Назовите функцию **ApplyPnPProvisioningTemplate**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-200">Name the function **ApplyPnPProvisioningTemplate**</span></span> 
1. <span data-ttu-id="e47b4-201">Введите имя очереди, созданной на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="e47b4-201">Enter the name of your queue you created in the previous steps.</span></span>
1. <span data-ttu-id="e47b4-202">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-202">Select **Create**</span></span>
1. <span data-ttu-id="e47b4-203">Откроется редактор, где можно вводить командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e47b4-203">You will be presented with a Editor where you can enter PowerShell Cmdlets.</span></span> <span data-ttu-id="e47b4-204">Теперь мы отправим модуль PnP для PowerShell, чтобы использовать его в функции Azure.</span><span class="sxs-lookup"><span data-stu-id="e47b4-204">We will now upload the PnP PowerShell module so we can use it in the Azure function.</span></span>

## <a name="uploading-pnp-powershell-for-your-azure-function"></a><span data-ttu-id="e47b4-205">Отправка модуля PowerShell PnP для функции Azure</span><span class="sxs-lookup"><span data-stu-id="e47b4-205">Uploading PnP PowerShell for your Azure Function</span></span>

<span data-ttu-id="e47b4-206">Для начала необходимо скачать модуль PnP для PowerShell, чтобы позже его было легко отправить.</span><span class="sxs-lookup"><span data-stu-id="e47b4-206">We first have to download the PnP PowerShell module so you can easy upload it later.</span></span>

1. <span data-ttu-id="e47b4-207">Создайте временную папку в любом расположении на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e47b4-207">Create a temporary folder somewhere on your computer</span></span>
1. <span data-ttu-id="e47b4-208">Запустите PowerShell и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e47b4-208">Launch PowerShell and enter</span></span>
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```
1. <span data-ttu-id="e47b4-209">Файлы модуля PowerShell будут загружены в папку, вложенную в только что выбранную папку.</span><span class="sxs-lookup"><span data-stu-id="e47b4-209">The PowerShell module files will be downloaded to a folder inside the folder you just selected.</span></span> 

<span data-ttu-id="e47b4-210">Теперь следует отправить эти файлы, чтобы функция Azure могла использовать модуль:</span><span class="sxs-lookup"><span data-stu-id="e47b4-210">Now it is time to upload those files so your Azure Function can make use of the module:</span></span>

1. <span data-ttu-id="e47b4-211">Перейдите на главную страницу приложения-функции и выберите **Функции платформы**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-211">Navigate to the main page of your Function App and select **Platform Features**</span></span>

    ![Перейдите к разделу "Функции платформы".](images/pnpprovisioning-platform-features.png)

1. <span data-ttu-id="e47b4-213">Выберите **Дополнительные инструменты (Kudu)**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-213">Select **Advanced tools (Kudu)**</span></span>

    ![Выберите "Дополнительные инструменты (Kudu)".](images/pnpprovisioning-select-kudu.png)

1. <span data-ttu-id="e47b4-215">На главной странице Kudu нажмите **Консоль отладки** и выберите **CMD** или **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-215">On the main Kudu page, select **Debug Console** and pick either **CMD** or **PowerShell**</span></span>
1. <span data-ttu-id="e47b4-216">В верхней части страницы откроется проводник.</span><span class="sxs-lookup"><span data-stu-id="e47b4-216">In the upper part of the page you see a file explorer.</span></span> <span data-ttu-id="e47b4-217">Перейдите к папке **site\wwwroot\\[имя_функции_azure]**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-217">Navigate to **site\wwwroot\\[nameofyourazurefunction]**</span></span>
1. <span data-ttu-id="e47b4-218">Создайте папку и назовите ее **modules**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-218">Create a new folder and call that folder **modules**</span></span>
    
    ![Создание папки](images/pnpprovisioning-kudu-create-folder.png)

1. <span data-ttu-id="e47b4-220">В этой папке создайте еще одну папку с именем **SharePointPnPPowerShellOnline** и перейдите к ней.</span><span class="sxs-lookup"><span data-stu-id="e47b4-220">In that folder create another folder called **SharePointPnPPowerShellOnline** and navigate to the folder</span></span>
1. <span data-ttu-id="e47b4-221">В проводнике на компьютере перейдите к папке, в которую вы скачали все файлы модуля PnP для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e47b4-221">In your File Explorer on your computer navigate to the folder where you downloaded all the PnP PowerShell Module files.</span></span> <span data-ttu-id="e47b4-222">Откройте папку **SharePointPnPPowerShellOnline\2.20.1711.0** (обратите внимание на то, что в настоящее время номер версии может быть другим).</span><span class="sxs-lookup"><span data-stu-id="e47b4-222">Open the **SharePointPnPPowerShellOnline\2.20.1711.0** folder (notice that depending on when you follow this walkthrough the version number can be different).</span></span>
1. <span data-ttu-id="e47b4-223">Отправьте все файлы из этой папки, перетащив их в папку в Kudu.</span><span class="sxs-lookup"><span data-stu-id="e47b4-223">Upload all files in that folder by dragging and dropping all the files from this folder into the folder in Kudu.</span></span>

   ![Создание папки](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finishing-the-azure-function"></a><span data-ttu-id="e47b4-225">Завершение создания функции Azure</span><span class="sxs-lookup"><span data-stu-id="e47b4-225">Finishing the Azure Function</span></span>

1. <span data-ttu-id="e47b4-226">Вернитесь к функции Azure и разверните вкладку файлов справа.</span><span class="sxs-lookup"><span data-stu-id="e47b4-226">Navigate back to your Azure Function and expand the files tab to the right.</span></span>

    ![Просмотр файлов](images/pnpprovisioning-view-files.png)

1. <span data-ttu-id="e47b4-228">Нажмите кнопку **Отправить** и отправьте созданный ранее файл шаблона подготовки.</span><span class="sxs-lookup"><span data-stu-id="e47b4-228">Select **Upload** and upload your provisioning template file you created earlier.</span></span>
1. <span data-ttu-id="e47b4-229">Замените скрипт PowerShell на следующий код:</span><span class="sxs-lookup"><span data-stu-id="e47b4-229">Replace the PowerShell script with the following</span></span>

```powershell
$in = Get-Content $triggerInput -Raw
Write-Output "Incoming request for '$in'"
Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
Write-Output "Connected to site"
Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
```

<span data-ttu-id="e47b4-230">Обратите внимание на то, что мы используем 2 переменные среды — ```SPO_AppId``` и ```SPO_AppSecret```.</span><span class="sxs-lookup"><span data-stu-id="e47b4-230">Notice that we are using 2 environment variables, one called ```SPO_AppId```, the other ```SPO_AppSecret```.</span></span> <span data-ttu-id="e47b4-231">Чтобы задать эти переменные, перейдите на главную страницу приложения-функции на портале Azure, выберите **Параметры приложения** и добавьте два новых параметра приложения:</span><span class="sxs-lookup"><span data-stu-id="e47b4-231">In order to set those variables navigate to your main Function App page in your Azure Portal, select **Application Settings** and add two new Application Settings:</span></span>

1. <span data-ttu-id="e47b4-232">```SPO_AppId```. Укажите в качестве значения идентификатор клиента, скопированный на первом этапе во время создания приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="e47b4-232">```SPO_AppId```: set the value to the Client Id you copied in the first step when creating your app on your tenant.</span></span>
2. <span data-ttu-id="e47b4-233">```SPO_AppSecret```. Укажите в качестве значения секрет клиента, скопированный на первом этапе во время создания приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="e47b4-233">```SPO_AppSecret```: set the value to the Client Secret you copied in the first step when creating your app on your tenant.</span></span>

## <a name="creating-the-site-design"></a><span data-ttu-id="e47b4-234">Создание макета сайта</span><span class="sxs-lookup"><span data-stu-id="e47b4-234">Creating a Site Design</span></span>

<span data-ttu-id="e47b4-235">Откройте PowerShell и убедитесь, что установлена консоль управления Microsoft Office 365.</span><span class="sxs-lookup"><span data-stu-id="e47b4-235">Open PowerShell and make sure you have the Microsoft Office 365 Management Shell installed.</span></span>

<span data-ttu-id="e47b4-236">Для начала подключитесь к клиенту с помощью командлета Connect-SPOService:</span><span class="sxs-lookup"><span data-stu-id="e47b4-236">First connect to your tenant using Connect-SPOService:</span></span>

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

<span data-ttu-id="e47b4-237">Теперь вы можете получить имеющиеся макеты сайтов с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e47b4-237">Now you can retrieve the existing Site Designs using</span></span> 

```powershell
Get-SPOSiteDesign
```

<span data-ttu-id="e47b4-238">Перед созданием макета сайта необходимо создать скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="e47b4-238">In order to create a Site Design you first need to create a Site Script.</span></span> <span data-ttu-id="e47b4-239">Макет сайта можно рассматривать как контейнер, ссылающийся на один или несколько скриптов сайта.</span><span class="sxs-lookup"><span data-stu-id="e47b4-239">Think of a Site Design as a container which refers to 1 or more Site Scripts.</span></span>
1. <span data-ttu-id="e47b4-240">Скопируйте приведенный ниже код JSON в буфер обмена и измените его.</span><span class="sxs-lookup"><span data-stu-id="e47b4-240">Copy the following JSON code to your clipboard and modify it.</span></span> <span data-ttu-id="e47b4-241">Задайте для свойства url значение, скопированное при создании потока.</span><span class="sxs-lookup"><span data-stu-id="e47b4-241">Set the url property to the value you copied when creating the flow.</span></span> <span data-ttu-id="e47b4-242">URL-адрес выглядит так: `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`</span><span class="sxs-lookup"><span data-stu-id="e47b4-242">The URL looks alike    `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`</span></span>

    ```json
    {
        "$schema": "schema.json",
        "actions": [
           {
                "verb": "triggerFlow",
                "url": "[paste the workflow trigger URL here]",
                "name": "Apply Template",
                "parameters": {
                    "event":"",
                    "product":""
                }
           }
        ],
        "bindata": {},
        "version": 1
    }
    ```

1. <span data-ttu-id="e47b4-243">Когда вы измените код JSON, скопировав URL-адрес для вызова потока, выделите его и снова скопируйте в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="e47b4-243">After modifying the JSON by inserting the correct URL to trigger your flow, select it all and copy it again to your clipboard</span></span>
1. <span data-ttu-id="e47b4-244">Откройте консоль PowerShell и введите приведенную ниже команду, чтобы скопировать скрипт в переменную и создать скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="e47b4-244">Open PowerShell and enter the following to copy the script into a variable and create the site script</span></span>

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. <span data-ttu-id="e47b4-245">Должен появиться список из одного или нескольких скриптов сайта, включая только что созданный.</span><span class="sxs-lookup"><span data-stu-id="e47b4-245">You should be presented with a list of one or more site scripts, including the site script you just created</span></span>
1. <span data-ttu-id="e47b4-246">Выделите ИД только что созданного скрипта сайта и скопируйте его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="e47b4-246">Select the ID of the Site Script you just created and copy it to the clipboard</span></span>
1. <span data-ttu-id="e47b4-247">Создайте макет сайта:</span><span class="sxs-lookup"><span data-stu-id="e47b4-247">Create the Site Design:</span></span>

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

<span data-ttu-id="e47b4-248">Командлет Add-SPOSiteDesign сопоставит макет с сайтом группы.</span><span class="sxs-lookup"><span data-stu-id="e47b4-248">The Add-SPOSiteDesign will associate the site design with the Team Site.</span></span> <span data-ttu-id="e47b4-249">Чтобы сопоставить макет с сайтом для общения, используйте значение 68.</span><span class="sxs-lookup"><span data-stu-id="e47b4-249">If you want to associate the design with a Communication Site use "68".</span></span>

## <a name="conclusion"></a><span data-ttu-id="e47b4-250">Заключение</span><span class="sxs-lookup"><span data-stu-id="e47b4-250">Conclusion</span></span>

<span data-ttu-id="e47b4-251">Мы создали очередь хранилища и ИД приложения, обеспечивающий доступ только для приложений, корректно создали функцию Azure и макет сайта, а затем вызвали правильный поток Microsoft Flow из макета сайта. Теперь все готово к работе.</span><span class="sxs-lookup"><span data-stu-id="e47b4-251">After you created your Storage Queue, you created the app Id for the app only access, you correctly created the Azure Function, you created the Site Design and triggered the correct Microsoft Flow from the Site Design, you are all good to go.</span></span> 

<span data-ttu-id="e47b4-252">Чтобы создать новый сайт, перейдите к клиенту SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e47b4-252">Try creating a new site by navigating to your SharePoint Tenant.</span></span> <span data-ttu-id="e47b4-253">Выберите **SharePoint**, нажмите **Создать сайт** и выберите **Сайт группы**.</span><span class="sxs-lookup"><span data-stu-id="e47b4-253">Select **SharePoint**, select **Create Site**, Select **Team Site**.</span></span> <span data-ttu-id="e47b4-254">Новый макет сайта должен появиться в списке доступных вариантов оформления.</span><span class="sxs-lookup"><span data-stu-id="e47b4-254">Your newly created Site Design should show up as a possible design option.</span></span> <span data-ttu-id="e47b4-255">Создайте сайт и обратите внимание на то, как макет сайта применяется после его создания.</span><span class="sxs-lookup"><span data-stu-id="e47b4-255">Create your site and notice the Site Design being applied after the site has been created.</span></span> <span data-ttu-id="e47b4-256">Если все настроено надлежащим образом, должен вызываться поток.</span><span class="sxs-lookup"><span data-stu-id="e47b4-256">If you configured it all correctly you should see your flow being triggered.</span></span> <span data-ttu-id="e47b4-257">Вы можете просмотреть журнал запусков потока, чтобы проверить, был ли он запущен должным образом.</span><span class="sxs-lookup"><span data-stu-id="e47b4-257">You can check the Run History of the flow if it was executed correctly.</span></span> <span data-ttu-id="e47b4-258">Применение шаблона подготовки PnP может занять некоторое время, поэтому нижний колонтитул может появиться не сразу.</span><span class="sxs-lookup"><span data-stu-id="e47b4-258">As it can take a bit before the PnP Provisioning Template has been applied, it can be that the footer does not show up immediately.</span></span> <span data-ttu-id="e47b4-259">Подождите минуту и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="e47b4-259">Give it a minute and reload your site to check again.</span></span>


