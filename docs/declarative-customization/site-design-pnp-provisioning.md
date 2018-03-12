---
title: "Создание полноценного макета сайта SharePoint с помощью модуля подготовки PnP"
description: "Создание полноценного макета сайта SharePoint с помощью модуля подготовки PnP"
ms.date: 01/08/2018
ms.openlocfilehash: 5257881730ea69f0a897962edc125fe065029fe0
ms.sourcegitcommit: 860b40b91f01c5b781517e3cd4057b971ce90b6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2018
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a><span data-ttu-id="20394-103">Вызов модуля подготовки PnP из скрипта на сайте</span><span class="sxs-lookup"><span data-stu-id="20394-103">Calling the PnP provisioning engine from a site script</span></span>

<span data-ttu-id="20394-104">Макеты сайтов — удобный способ стандартизации внешнего вида семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="20394-104">Site designs offer a great way to standardize the look and feel of your site collections.</span></span> <span data-ttu-id="20394-105">Однако они не поддерживают некоторые задачи, например, не позволяют добавить нижний колонтитул на каждую страницу.</span><span class="sxs-lookup"><span data-stu-id="20394-105">You can't do some things with site designs, however, like add a footer to every page.</span></span> <span data-ttu-id="20394-106">Вы можете подготовить настройщик заполнителей сайта на основе шаблона, созданного с помощью модуля подготовки PnP.</span><span class="sxs-lookup"><span data-stu-id="20394-106">You can use the PnP provisioning engine to create a template that you can use to provision an Application Customizer to a site.</span></span> <span data-ttu-id="20394-107">Этот настройщик затем может обновить макет страницы, например, чтобы зарегистрировать нижний колонтитул на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="20394-107">This Application Customizer can then update your page design, for example to register a footer on every page.</span></span> 

<span data-ttu-id="20394-108">В этой статье описано, как создать макет сайта, который применяет шаблон подготовки PnP к сайту.</span><span class="sxs-lookup"><span data-stu-id="20394-108">This article describes how to create a site design that applies a PnP provisioning template to a site.</span></span> <span data-ttu-id="20394-109">Шаблон добавит настройщик заполнителей для отображения нижнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="20394-109">The template will add an Application Customizer to render a footer.</span></span>

<span data-ttu-id="20394-110">В этой статье используются следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="20394-110">The steps in this article use the following components:</span></span>

- <span data-ttu-id="20394-111">макет и скрипт сайта;</span><span class="sxs-lookup"><span data-stu-id="20394-111">A site design and a site script</span></span>
- <span data-ttu-id="20394-112">поток Microsoft Flow;</span><span class="sxs-lookup"><span data-stu-id="20394-112">Microsoft Flow</span></span>
- <span data-ttu-id="20394-113">хранилище очередей Azure</span><span class="sxs-lookup"><span data-stu-id="20394-113">Azure Queue storage</span></span>
- <span data-ttu-id="20394-114">функция Azure;</span><span class="sxs-lookup"><span data-stu-id="20394-114">An Azure Function</span></span>
- <span data-ttu-id="20394-115">решение SharePoint Framework (SPFx);</span><span class="sxs-lookup"><span data-stu-id="20394-115">A SharePoint Framework (SPFx) solution</span></span>
- <span data-ttu-id="20394-116">шаблон подготовки PnP;</span><span class="sxs-lookup"><span data-stu-id="20394-116">A PnP provisioning template</span></span>
- <span data-ttu-id="20394-117">скрипт PnP PowerShell;</span><span class="sxs-lookup"><span data-stu-id="20394-117">A PnP PowerShell script</span></span>
- <span data-ttu-id="20394-118">идентификатор и секрет приложения с правами администратора для клиента.</span><span class="sxs-lookup"><span data-stu-id="20394-118">An app ID and app secret with administrative rights on your tenant</span></span>

<span data-ttu-id="20394-119">Эти компоненты используются для активации кода подготовки PnP после создания сайта и применения макета.</span><span class="sxs-lookup"><span data-stu-id="20394-119">You'll use these components to trigger the PnP provisioning code after you create the site and apply the site design.</span></span>

## <a name="set-up-app-only-access-to-your-tenant"></a><span data-ttu-id="20394-120">Настройка доступа к клиенту на уровне приложения</span><span class="sxs-lookup"><span data-stu-id="20394-120">Set up app-only access to your tenant</span></span>

<span data-ttu-id="20394-121">Чтобы настроить доступ на уровне приложения, нужны две страницы: одна — на обычном сайте, а другая — на сайте администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="20394-121">To set up app-only access, you need to have two different pages on your tenant - one on the regular site, and the other on your SharePoint administration site.</span></span>

1. <span data-ttu-id="20394-122">Перейдите по следующему URL-адресу в своем клиенте: `https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx` (вы можете перейти на любой сайт, но пока лучше использовать корневой).</span><span class="sxs-lookup"><span data-stu-id="20394-122">Go to following URL in your tenant: `https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx` (you can go to any site, but for now pick the root site).</span></span>
1. <span data-ttu-id="20394-123">Нажмите кнопку **Создать** рядом с полями **Идентификатор клиента** и **Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="20394-123">Choose the **Generate** button next to the **Client Id** and **Client Secret** fields.</span></span>
1. <span data-ttu-id="20394-124">Введите название приложения, например "Подготовка сайта".</span><span class="sxs-lookup"><span data-stu-id="20394-124">Enter a title for your app, such as "Site Provisioning".</span></span>
1. <span data-ttu-id="20394-125">В поле **Домен приложения** введите **localhost**.</span><span class="sxs-lookup"><span data-stu-id="20394-125">In the **App Domain** box, enter **localhost**.</span></span>
1. <span data-ttu-id="20394-126">В поле **URI перенаправления** введите **https://localhost**.</span><span class="sxs-lookup"><span data-stu-id="20394-126">In the **Redirect URI** box, enter **https://localhost**.</span></span>

    ![Страница создания приложения с полями "Идентификатор клиента", "Секрет клиента", "Название", "Домен приложения" и "URI перенаправления"](images/pnpprovisioning-createapponly.png)

1. <span data-ttu-id="20394-128">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="20394-128">Choose **Create**.</span></span> 
1. <span data-ttu-id="20394-129">Скопируйте значения из полей **Идентификатор клиента** и **Секрет клиента** — они понадобятся вам позже.</span><span class="sxs-lookup"><span data-stu-id="20394-129">Copy the values for **Client Id** and **Client Secret** - you will need them later.</span></span>

<span data-ttu-id="20394-130">После этого подтвердите, что вы доверяете приложению, чтобы предоставить ему доступ к вашему клиенту:</span><span class="sxs-lookup"><span data-stu-id="20394-130">Next, trust the app, so that it has the appropriate access to your tenant:</span></span>

1. <span data-ttu-id="20394-131">Перейдите по адресу `https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx` (обратите внимание на оператор `-admin` в URL-адресе).</span><span class="sxs-lookup"><span data-stu-id="20394-131">Go to `https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx` (notice the `-admin` in the URL).</span></span>
1. <span data-ttu-id="20394-132">В поле **Идентификатор приложения** вставьте скопированный **идентификатор клиента** и нажмите кнопку **Поиск**.</span><span class="sxs-lookup"><span data-stu-id="20394-132">In the **App Id** field, paste the **Client ID** that you copied, and choose **Lookup**.</span></span>
1. <span data-ttu-id="20394-133">Вставьте следующий код XML в поле **XML-запрос разрешения**:</span><span class="sxs-lookup"><span data-stu-id="20394-133">In the **Permission Request XML** field, paste the following XML:</span></span>

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. <span data-ttu-id="20394-134">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="20394-134">Choose **Create**.</span></span>
1. <span data-ttu-id="20394-135">Чтобы подтвердить, что вы доверяете этому приложению, нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="20394-135">To confirm that you want to trust this app, choose **Trust It**.</span></span>


## <a name="create-the-azure-queue-storage"></a><span data-ttu-id="20394-136">Создание хранилища очередей Azure</span><span class="sxs-lookup"><span data-stu-id="20394-136">Create the Azure Queue storage</span></span>

<span data-ttu-id="20394-137">В этом разделе показано, как получить сообщения из Microsoft Flow, используя хранилище очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="20394-137">In this section, you will use Azure Queue storage to receive messages from Microsoft Flow.</span></span> <span data-ttu-id="20394-138">Каждый раз, когда в хранилище очередей появляется сообщение, вызывается функция Azure для выполнения скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20394-138">Every time a message shows up in the Queue storage, an Azure function is triggered to run a PowerShell script.</span></span> 

<span data-ttu-id="20394-139">Чтобы настроить хранилище очередей Azure:</span><span class="sxs-lookup"><span data-stu-id="20394-139">To set up the Azure Queue storage:</span></span>

1. <span data-ttu-id="20394-140">Перейдите на [портал Azure](https://portal.azure.com) и войдите.</span><span class="sxs-lookup"><span data-stu-id="20394-140">Go to the [Azure portal](https://portal.azure.com) and sign in.</span></span>
1. <span data-ttu-id="20394-141">Нажмите **+ Создать**.</span><span class="sxs-lookup"><span data-stu-id="20394-141">Choose **+ New**.</span></span>
1. <span data-ttu-id="20394-142">Выберите **Storage** в списке решений Azure Marketplace, а затем выберите **Учетная запись хранения — BLOB-объект, файл, таблица, очередь** в столбце "Рекомендованные".</span><span class="sxs-lookup"><span data-stu-id="20394-142">From the Azure Marketplace listings, select **Storage**, and in the Featured column, choose **Storage account - blob, file, table, queue**.</span></span>
1. <span data-ttu-id="20394-143">Укажите значения в обязательных полях.</span><span class="sxs-lookup"><span data-stu-id="20394-143">Provide values for the required fields.</span></span> <span data-ttu-id="20394-144">Выберите **Закрепить на панели мониторинга** и нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="20394-144">Select **Pin to dashboard**, and choose **Create**.</span></span> <span data-ttu-id="20394-145">Создание учетной записи хранения может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="20394-145">It can take a few minutes for the storage account to be created.</span></span>
1. <span data-ttu-id="20394-146">Откройте учетную запись хранения и перейдите в раздел **Очереди**.</span><span class="sxs-lookup"><span data-stu-id="20394-146">Open the storage account and go to **Queues**.</span></span>
1. <span data-ttu-id="20394-147">Выберите **+ Очередь** в верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="20394-147">Choose **+ Queue** at the top of the screen.</span></span>
1. <span data-ttu-id="20394-148">Введите имя **pnpprovisioningqueue** или собственное значение, соответствующее стандарту именования.</span><span class="sxs-lookup"><span data-stu-id="20394-148">Enter **pnpprovisioningqueue** for the name, or enter your own value; be sure to follow the naming standard.</span></span> <span data-ttu-id="20394-149">Запишите имя очереди; это значение понадобится вам при создании функции Azure.</span><span class="sxs-lookup"><span data-stu-id="20394-149">Make note of the queue name; you will need this value when you create the Azure Function.</span></span>
1. <span data-ttu-id="20394-150">Перейдите в раздел **Ключи доступа** и запишите **имя учетной записи хранения** и значение ключа **key1**.</span><span class="sxs-lookup"><span data-stu-id="20394-150">Go to **Access Keys** and note the **Storage Account Name** and the **key1 Key value**.</span></span> <span data-ttu-id="20394-151">Эти значения понадобятся вам при создании потока.</span><span class="sxs-lookup"><span data-stu-id="20394-151">You will need these values when you create the flow.</span></span>


## <a name="create-the-flow"></a><span data-ttu-id="20394-152">Создание потока</span><span class="sxs-lookup"><span data-stu-id="20394-152">Create the flow</span></span>

<span data-ttu-id="20394-153">Чтобы поместить сообщение в очередь, необходимо создать поток.</span><span class="sxs-lookup"><span data-stu-id="20394-153">To put a message in the queue, you need to create a flow.</span></span> 

1. <span data-ttu-id="20394-154">Перейдите на сайт [Microsoft Flow](https://flow.microsoft.com), войдите и выберите **Создать с нуля** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="20394-154">Go to the [Microsoft Flow](https://flow.microsoft.com) site, sign in, and choose **Create from Blank** at the top of the page.</span></span>
1. <span data-ttu-id="20394-155">Нажмите **Поиск среди сотен соединителей и триггеров**, чтобы выбрать триггер.</span><span class="sxs-lookup"><span data-stu-id="20394-155">Choose **Search hundreds of connectors and triggers** to select your trigger.</span></span>
1. <span data-ttu-id="20394-156">Введите слово **Запрос** и выберите **Запрос - При получении HTTP-запроса**.</span><span class="sxs-lookup"><span data-stu-id="20394-156">Search for **Request**, and select **Request - When a HTTP Request is received**.</span></span>
1. <span data-ttu-id="20394-157">Введите следующий код JSON в теле запроса:</span><span class="sxs-lookup"><span data-stu-id="20394-157">Enter the following JSON as your request body:</span></span>

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

1. <span data-ttu-id="20394-158">Нажмите **+ Новый шаг** и выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="20394-158">Select **+ New Step** and choose **Add an action**.</span></span>
1. <span data-ttu-id="20394-159">Выполните поиск по запросу **Очереди Azure** и выберите **Очереди Azure - Поместить сообщение в очередь**.</span><span class="sxs-lookup"><span data-stu-id="20394-159">Search for **Azure Queues** and select **Azure Queues - Put a message on a queue**.</span></span>
1. <span data-ttu-id="20394-160">Введите описательное имя подключения.</span><span class="sxs-lookup"><span data-stu-id="20394-160">Enter a descriptive name for the connection.</span></span>
1. <span data-ttu-id="20394-161">Введите имя учетной записи хранения, скопированное в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="20394-161">Enter the storage account name that you copied in the previous section.</span></span>
1. <span data-ttu-id="20394-162">Введите открытый ключ хранилища, представляющий собой значение ключа **Key1** для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="20394-162">Enter the storage shared key, which is the value of the **Key1 key value** field of your storage account.</span></span>
1. <span data-ttu-id="20394-163">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="20394-163">Choose **Create**.</span></span>
1. <span data-ttu-id="20394-164">Выберите имя очереди **pnpprovisioningqueue**.</span><span class="sxs-lookup"><span data-stu-id="20394-164">Select **pnpprovisioningqueue** for the queue name.</span></span>
1. <span data-ttu-id="20394-165">В теле запроса вы указали входящий параметр *webUrl*.</span><span class="sxs-lookup"><span data-stu-id="20394-165">In the request body, you specified an incoming parameter called *webUrl*.</span></span> <span data-ttu-id="20394-166">Чтобы поместить значение этого поля в очередь, щелкните поле **Сообщение** и выберите **webUrl** в средстве выбора динамического контента.</span><span class="sxs-lookup"><span data-stu-id="20394-166">To put the value of that field in the queue, click in the **message** field and select **webUrl** from the Dynamic Content picker.</span></span>
1. <span data-ttu-id="20394-167">Нажмите **Сохранить поток**.</span><span class="sxs-lookup"><span data-stu-id="20394-167">Choose **Save Flow**.</span></span> <span data-ttu-id="20394-168">При этом будет создан URL-адрес, который вы скопируете на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="20394-168">This will generate the URL that you will copy in the next step.</span></span>
1. <span data-ttu-id="20394-169">Выберите первый шаг потока ("При получении HTTP-запроса") и скопируйте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="20394-169">Choose the first step in your flow ('When an HTTP request is received') and copy the URL.</span></span>
1. <span data-ttu-id="20394-170">Сохраните поток.</span><span class="sxs-lookup"><span data-stu-id="20394-170">Save your flow.</span></span>

<span data-ttu-id="20394-171">Поток должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="20394-171">Your flow should look like the following.</span></span>

![Снимок экрана: поток "При получении HTTP-запроса" с URL-адресом и телом запроса, а также поля "Имя очереди" и "Сообщение"](images/pnpprovisioning-flow-overview.png)

## <a name="test-the-flow"></a><span data-ttu-id="20394-173">Проверка потока</span><span class="sxs-lookup"><span data-stu-id="20394-173">Test the flow</span></span>

<span data-ttu-id="20394-174">Чтобы проверить поток, необходимо отправить POST-запрос.</span><span class="sxs-lookup"><span data-stu-id="20394-174">To test your flow, you have to make a POST request.</span></span> <span data-ttu-id="20394-175">Это можно сделать через PowerShell, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="20394-175">You can do this via PowerShell, as shown in the following example.</span></span>

```powershell
$uri = "[the URI you copied in step 14 when creating the flow]"
$body = "{webUrl:'somesiteurl'}"
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

<span data-ttu-id="20394-176">После перехода на главный экран потока вы увидите журнал выполнения.</span><span class="sxs-lookup"><span data-stu-id="20394-176">When you go to the main screen of your flow, you will see a run history.</span></span> <span data-ttu-id="20394-177">Состояние `Succeeded` означает, что поток выполнен успешно.</span><span class="sxs-lookup"><span data-stu-id="20394-177">If your flow worked correctly, it will show `Succeeded`.</span></span>
<span data-ttu-id="20394-178">Теперь перейдите к новой очереди Azure и нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="20394-178">Now go to the queue you just created in Azure and choose **Refresh**.</span></span> <span data-ttu-id="20394-179">Должна появиться запись о правильном вызове потока.</span><span class="sxs-lookup"><span data-stu-id="20394-179">You should see an entry that shows that you correctly invoked the flow.</span></span>

## <a name="provision-the-spfx-solution"></a><span data-ttu-id="20394-180">Подготовка решения SPFx</span><span class="sxs-lookup"><span data-stu-id="20394-180">Provision the SPFx solution</span></span>

<span data-ttu-id="20394-181">В этом разделе вы будете использовать существующее решение SPFx [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer).</span><span class="sxs-lookup"><span data-stu-id="20394-181">In this section, you'll use an existing SPFx solution, the [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer).</span></span> <span data-ttu-id="20394-182">Выполните инструкции из файла [Readme](https://github.com/SharePoint/sp-dev-fx-extensions/blob/master/samples/react-application-regions-footer/README.md) в репозитории примера, чтобы создать и подготовить решение.</span><span class="sxs-lookup"><span data-stu-id="20394-182">Follow the steps in the [Readme](https://github.com/SharePoint/sp-dev-fx-extensions/blob/master/samples/react-application-regions-footer/README.md) file in the sample repo to build and provision the solution.</span></span>

## <a name="create-a-pnp-provisioning-template"></a><span data-ttu-id="20394-183">Создание шаблона подготовки PnP</span><span class="sxs-lookup"><span data-stu-id="20394-183">Create a PnP provisioning template</span></span>

<span data-ttu-id="20394-184">Скопируйте следующий шаблон подготовки XML в новый файл и сохраните его с именем FlowDemoTemplate.xml.</span><span class="sxs-lookup"><span data-stu-id="20394-184">Copy the following provisioning template XML to a new file and save the file as FlowDemoTemplate.xml.</span></span>

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
  </pnp:Templates>
</pnp:Provisioning>
```

> [!NOTE]
> <span data-ttu-id="20394-185">Шаблон подготовки добавляет в решение дополнительное действие.</span><span class="sxs-lookup"><span data-stu-id="20394-185">The provisioning template adds a custom action to a solution.</span></span> <span data-ttu-id="20394-186">Идентификатор **ClientSideComponentId** связан с подготовленным ранее решением [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer).</span><span class="sxs-lookup"><span data-stu-id="20394-186">The **ClientSideComponentId** is associated with the [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer) that you provisioned earlier.</span></span> <span data-ttu-id="20394-187">Чтобы запустить эту демонстрацию с собственным решением SPFx, измените значения атрибутов **ClientSideComponentId** и (необязательно) **ClientSideComponentProperties** в XML-файле.</span><span class="sxs-lookup"><span data-stu-id="20394-187">If you run this demo with your own SPFx solution, change the **ClientSideComponentId** and optionally the **ClientSideComponentProperties** attribute values in the XML.</span></span>

## <a name="create-the-azure-function"></a><span data-ttu-id="20394-188">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="20394-188">Create the Azure Function</span></span>

1. <span data-ttu-id="20394-189">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20394-189">Go to the [Azure Portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="20394-190">Выполните поиск по запросу **Приложение-функция** и создайте приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="20394-190">Search for **Function App** and create a new function app.</span></span> <span data-ttu-id="20394-191">В поле **Хранение** выберите **Использовать имеющееся**, а затем укажите созданную ранее учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="20394-191">In the **Storage** field, select **Use existing**, and select the storage account that you created earlier.</span></span> <span data-ttu-id="20394-192">При необходимости задайте другие значения.</span><span class="sxs-lookup"><span data-stu-id="20394-192">Set the other values as required.</span></span>
1. <span data-ttu-id="20394-193">Откройте приложение-функцию и выберите **Функции** > **Новая функция**.</span><span class="sxs-lookup"><span data-stu-id="20394-193">Open the Function app and select **Functions** > **New function**.</span></span>

    ![Снимок экрана: портал Azure с выделенной командой "Новая функция"](images/pnpprovisioning-create-function.png)

1. <span data-ttu-id="20394-195">В раскрывающемся списке "Язык" выберите **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="20394-195">From the Language drop-down box, select **PowerShell**.</span></span>
1. <span data-ttu-id="20394-196">Выберите **QueueTrigger — PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="20394-196">Select **QueueTrigger - PowerShell**.</span></span>
1. <span data-ttu-id="20394-197">Назовите функцию **ApplyPnPProvisioningTemplate**.</span><span class="sxs-lookup"><span data-stu-id="20394-197">Name the function **ApplyPnPProvisioningTemplate**.</span></span> 
1. <span data-ttu-id="20394-198">Введите имя созданной ранее очереди.</span><span class="sxs-lookup"><span data-stu-id="20394-198">Enter the name of the queue you created earlier.</span></span>
1. <span data-ttu-id="20394-199">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="20394-199">Choose **Create**.</span></span> <span data-ttu-id="20394-200">Откроется редактор, в котором можно вводить командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20394-200">An editor where you can enter PowerShell cmdlets will open.</span></span> 

<span data-ttu-id="20394-201">Ниже описано, как загрузить модуль PowerShell PnP, чтобы использовать его в функции Azure.</span><span class="sxs-lookup"><span data-stu-id="20394-201">Next, you'll upload the PnP PowerShell module so that you can use it in the Azure Function.</span></span>

## <a name="upload-the-pnp-powershell-module-for-your-azure-function"></a><span data-ttu-id="20394-202">Загрузка модуля PowerShell PnP для функции Azure</span><span class="sxs-lookup"><span data-stu-id="20394-202">Upload the PnP PowerShell module for your Azure Function</span></span>

<span data-ttu-id="20394-203">Чтобы загрузить модуль PnP PowerShell для функции Azure, его сначала нужно скачать.</span><span class="sxs-lookup"><span data-stu-id="20394-203">You'll need to download the PnP PowerShell module so that you can upload it for your Azure Function.</span></span>

1. <span data-ttu-id="20394-204">Создайте временную папку на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="20394-204">Create a temporary folder on your computer.</span></span>
1. <span data-ttu-id="20394-205">Запустите PowerShell и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="20394-205">Launch PowerShell and enter the following:</span></span>
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```

<span data-ttu-id="20394-206">Файлы модуля PowerShell скачаются в папку в созданной папке.</span><span class="sxs-lookup"><span data-stu-id="20394-206">The PowerShell module files will download to a folder within the folder that you created.</span></span> 

<span data-ttu-id="20394-207">После этого загрузите файлы, чтобы функция Azure могла использовать модуль.</span><span class="sxs-lookup"><span data-stu-id="20394-207">Next, upload the files so that your Azure Function can use the module.</span></span>

1. <span data-ttu-id="20394-208">Перейдите на главную страницу приложения-функции и выберите **Функции платформы**.</span><span class="sxs-lookup"><span data-stu-id="20394-208">Go to the main page of your Function App and select **Platform Features**.</span></span>

    ![Снимок экрана: приложение-функция с выделенным пунктом "Функции платформы"](images/pnpprovisioning-platform-features.png)

1. <span data-ttu-id="20394-210">Выберите **Дополнительные инструменты (Kudu)**.</span><span class="sxs-lookup"><span data-stu-id="20394-210">Select **Advanced tools (Kudu)**.</span></span>

    ![Снимок экрана: средства разработки с выделенным пунктом "Дополнительные инструменты (Kudu)"](images/pnpprovisioning-select-kudu.png)

1. <span data-ttu-id="20394-212">На главной странице Kudu нажмите **Консоль отладки** и выберите **CMD** или **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="20394-212">On the main Kudu page, select **Debug Console** and pick either **CMD** or **PowerShell**.</span></span>
1. <span data-ttu-id="20394-213">Выберите проводник в верхней части страницы и перейдите в раздел **site\wwwroot\\[nameofyourazurefunction]**.</span><span class="sxs-lookup"><span data-stu-id="20394-213">Choose the file explorer on the upper part of the page, and go to **site\wwwroot\\[nameofyourazurefunction]**.</span></span>
1. <span data-ttu-id="20394-214">Создайте папку **modules**.</span><span class="sxs-lookup"><span data-stu-id="20394-214">Create a new folder named **modules**.</span></span>
    
    ![Снимок экрана: выделенная команда "Создать папку"](images/pnpprovisioning-kudu-create-folder.png)

1. <span data-ttu-id="20394-216">В папке modules создайте еще одну папку с именем **SharePointPnPPowerShellOnline** и перейдите в нее.</span><span class="sxs-lookup"><span data-stu-id="20394-216">In the modules folder, create another folder called **SharePointPnPPowerShellOnline** and go to that folder.</span></span>
1. <span data-ttu-id="20394-217">В проводнике на компьютере перейдите в папку, в которую вы скачали файлы модуля PowerShell PnP.</span><span class="sxs-lookup"><span data-stu-id="20394-217">In File Explorer on your computer, go to the folder where you downloaded the PnP PowerShell module files.</span></span> <span data-ttu-id="20394-218">Откройте папку **SharePointPnPPowerShellOnline\2.20.1711.0** (обратите внимание, что номер версии может отличаться).</span><span class="sxs-lookup"><span data-stu-id="20394-218">Open the **SharePointPnPPowerShellOnline\2.20.1711.0** folder (notice that the version number might be different).</span></span>
1. <span data-ttu-id="20394-219">Перетащите все файлы из этой папки в папку в Kudu.</span><span class="sxs-lookup"><span data-stu-id="20394-219">Drag and drop all the files from this folder into the folder in Kudu to upload them.</span></span>

   ![Снимок экрана: папка Kudu с 40 добавленными файлами](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finish-the-azure-function"></a><span data-ttu-id="20394-221">Завершение создания функции Azure</span><span class="sxs-lookup"><span data-stu-id="20394-221">Finish the Azure Function</span></span>

1. <span data-ttu-id="20394-222">Вернитесь к функции Azure и разверните вкладку файлов справа.</span><span class="sxs-lookup"><span data-stu-id="20394-222">Go back to your Azure Function and expand the files tab to the right.</span></span>

    ![Снимок экрана: вкладка "Просмотр файлов"](images/pnpprovisioning-view-files.png)

1. <span data-ttu-id="20394-224">Нажмите **Отправить** и загрузите созданный ранее файл шаблона подготовки.</span><span class="sxs-lookup"><span data-stu-id="20394-224">Select **Upload** and upload the provisioning template file that you created earlier.</span></span>
1. <span data-ttu-id="20394-225">Замените скрипт PowerShell следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="20394-225">Replace the PowerShell script with the following:</span></span>

    ```powershell
    $in = Get-Content $triggerInput -Raw
    Write-Output "Incoming request for '$in'"
    Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
    Write-Output "Connected to site"
    Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
    ```

<span data-ttu-id="20394-226">Обратите внимание, что здесь используются две переменные среды: ```SPO_AppId``` и ```SPO_AppSecret```.</span><span class="sxs-lookup"><span data-stu-id="20394-226">Notice that you're using two environment variables: ```SPO_AppId```and ```SPO_AppSecret```.</span></span> <span data-ttu-id="20394-227">Чтобы задать эти переменные, перейдите на страницу приложения-функции на портале Azure, выберите **Параметры приложения** и добавьте два новых параметра приложения:</span><span class="sxs-lookup"><span data-stu-id="20394-227">To set those variables, go to the main Function App page in the Azure Portal, select **Application Settings**, and add two new application settings:</span></span>

1. <span data-ttu-id="20394-228">```SPO_AppId```. Укажите в качестве значения идентификатор клиента, скопированный на первом шаге при создании приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="20394-228">```SPO_AppId``` - Set the value to the Client ID you copied in the first step when you created your app on your tenant.</span></span>
2. <span data-ttu-id="20394-229">```SPO_AppSecret```. Укажите в качестве значения секрет клиента, скопированный на первом шаге при создании приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="20394-229">```SPO_AppSecret``` - Set the value to the Client Secret that you copied in the first step when you created your app on your tenant.</span></span>

## <a name="create-the-site-design"></a><span data-ttu-id="20394-230">Создание макета сайта</span><span class="sxs-lookup"><span data-stu-id="20394-230">Create the site design</span></span>

<span data-ttu-id="20394-231">Откройте PowerShell и убедитесь, что установлена [консоль управления SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="20394-231">Open PowerShell and make sure that you have the Microsoft Office 365 Management Shell installed.</span></span>

<span data-ttu-id="20394-232">Подключитесь к клиенту, используя командлет **Connect-SPOService**.</span><span class="sxs-lookup"><span data-stu-id="20394-232">Connect to your tenant using **Connect-SPOService**.</span></span>

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

<span data-ttu-id="20394-233">Теперь вы можете получить имеющиеся макеты сайта.</span><span class="sxs-lookup"><span data-stu-id="20394-233">Now you can get the existing site designs.</span></span> 

```powershell
Get-SPOSiteDesign
```

<span data-ttu-id="20394-234">Чтобы создать макет сайта, необходимо создать скрипт сайта.</span><span class="sxs-lookup"><span data-stu-id="20394-234">To create a site design, you first need to create a site script.</span></span> <span data-ttu-id="20394-235">Макет сайта — это контейнер, который ссылается на один или несколько скриптов.</span><span class="sxs-lookup"><span data-stu-id="20394-235">A site design is a container that refers to one or more site scripts.</span></span>

1. <span data-ttu-id="20394-236">Скопируйте приведенный ниже код JSON в буфер обмена и измените его.</span><span class="sxs-lookup"><span data-stu-id="20394-236">Copy the following JSON code to your clipboard and modify it.</span></span> <span data-ttu-id="20394-237">Задайте для свойства **url** значение, скопированное при создании потока.</span><span class="sxs-lookup"><span data-stu-id="20394-237">Set the **url** property to the value you copied when you created the flow.</span></span> <span data-ttu-id="20394-238">URL-адрес будет выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="20394-238">The URL looks similar to the following:</span></span>

    `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`

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

1. <span data-ttu-id="20394-239">Еще раз выделите JSON и скопируйте его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="20394-239">Select the JSON again and copy it again to your clipboard.</span></span>
1. <span data-ttu-id="20394-240">Откройте консоль PowerShell и введите следующую команду, чтобы скопировать скрипт в переменную и создать скрипт сайта:</span><span class="sxs-lookup"><span data-stu-id="20394-240">Open PowerShell and enter the following to copy the script into a variable and create the site script:</span></span>

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. <span data-ttu-id="20394-241">Появится список из одного или нескольких скриптов сайта, включая только что созданный.</span><span class="sxs-lookup"><span data-stu-id="20394-241">You will see a list of one or more site scripts, including the site script you just created.</span></span> <span data-ttu-id="20394-242">Выделите идентификатор созданного скрипта сайта и скопируйте его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="20394-242">Select the ID of the site script that you created and copy it to the clipboard.</span></span>
1. <span data-ttu-id="20394-243">Создайте макет сайта, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="20394-243">Use the following command to create the site design:</span></span>

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

<span data-ttu-id="20394-244">Командлет **Add-SPOSiteDesign** связывает макет с сайтом группы.</span><span class="sxs-lookup"><span data-stu-id="20394-244">The **Add-SPOSiteDesign** cmdlet associates the site design with the team site.</span></span> <span data-ttu-id="20394-245">Чтобы связать макет с сайтом для общения, используйте значение 68.</span><span class="sxs-lookup"><span data-stu-id="20394-245">If you want to associate the design with a communication site, use the value "68".</span></span>

## <a name="verify-the-results"></a><span data-ttu-id="20394-246">Проверка результатов</span><span class="sxs-lookup"><span data-stu-id="20394-246">Verify the results</span></span>

<span data-ttu-id="20394-247">После создания хранилища очередей Azure вы создали идентификатор приложения для доступа на уровне приложения, функцию Azure и макет сайта.</span><span class="sxs-lookup"><span data-stu-id="20394-247">After you created your Azure Queue storage, you created the app ID for app-only access, the Azure Function, and the site design.</span></span> <span data-ttu-id="20394-248">После этого вы активировали поток Microsoft Flow из макета сайта.</span><span class="sxs-lookup"><span data-stu-id="20394-248">You then triggered the Microsoft Flow from the site design.</span></span> 

<span data-ttu-id="20394-249">Чтобы проверить результаты, создайте новый сайт.</span><span class="sxs-lookup"><span data-stu-id="20394-249">To test the results, create a new site.</span></span> <span data-ttu-id="20394-250">В клиенте SharePoint выберите **SharePoint** > **Создать сайт** > **Сайт группы**.</span><span class="sxs-lookup"><span data-stu-id="20394-250">In your SharePoint tenant, select **SharePoint** > **Create Site** > **Team Site**.</span></span> <span data-ttu-id="20394-251">Новый макет сайта должен появиться в списке доступных макетов.</span><span class="sxs-lookup"><span data-stu-id="20394-251">Your new site design should show up as a design option.</span></span> <span data-ttu-id="20394-252">Обратите внимание, что макет сайта применяется после создания сайта.</span><span class="sxs-lookup"><span data-stu-id="20394-252">Notice that the site design is applied after the site is created.</span></span> <span data-ttu-id="20394-253">Если поток настроен правильно, он будет активирован.</span><span class="sxs-lookup"><span data-stu-id="20394-253">If you configured it correctly, your flow will be triggered.</span></span> <span data-ttu-id="20394-254">Вы можете проверить работу потока, просмотрев журнал выполнения.</span><span class="sxs-lookup"><span data-stu-id="20394-254">You can check the run history of the flow to verify that it ran correctly.</span></span> <span data-ttu-id="20394-255">Обратите внимание, что нижний колонтитул может появиться не сразу; если вы его не видите, подождите минуту и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="20394-255">Note that the footer might not show up immediately; if you don't see it, wait a minute and reload your site to check again.</span></span>


