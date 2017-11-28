---
title: "Вызов веб-служб из рабочих процессов SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d3ee350dde2f5c9978c6d875518f57e828f35dbc
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="call-web-services-from-sharepoint-workflows"></a><span data-ttu-id="14d95-102">Вызов веб-служб из рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="14d95-102">Call web services from SharePoint workflows</span></span>

<span data-ttu-id="14d95-103">Развертывание рабочего процесса SharePoint 2013 на хост-сайт из надстройки для SharePoint и вызов веб-служб из рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-103">Deploy a SharePoint 2013 workflow to the host web from an add-in for SharePoint, and call web services from SharePoint workflows.</span></span>

<span data-ttu-id="14d95-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="14d95-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="14d95-105">Модель SharePoint 2013 надстройки можно использовать для создания и развертывания рабочих процессов, которые запускаются на добавление в веб-сайта или веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="14d95-105">You can use the SharePoint 2013 add-in model to create and deploy workflows that run on either the add-in web or the host web.</span></span> <span data-ttu-id="14d95-106">Эти рабочие процессы могут взаимодействовать с удаленными части размещением у поставщика надстроек. Рабочие процессы можно также вызвать удаленного веб-служб, которые содержат важные бизнес-данных в одном из двух способов:</span><span class="sxs-lookup"><span data-stu-id="14d95-106">These workflows can interact with the remotely hosted portions of provider-hosted add-ins. The workflows can also call remote web services that contain important business data in one of two ways:</span></span> 

- <span data-ttu-id="14d95-107">С помощью передачи данных запроса удаленно размещенной часть надстройки.</span><span class="sxs-lookup"><span data-stu-id="14d95-107">By passing query information to the remotely hosted portion of the add-in.</span></span> <span data-ttu-id="14d95-108">Удаленное веб-приложение затем вызывает веб-службы и передает данные обратно в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-108">The remote web application then calls the web service and passes the information back to SharePoint.</span></span>
    
- <span data-ttu-id="14d95-109">С помощью запроса веб-службы с помощью SharePoint 2013 веб-прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="14d95-109">By querying the web service by using the SharePoint 2013 web proxy.</span></span> <span data-ttu-id="14d95-110">Рабочий процесс передает результаты запроса удаленно размещенной часть надстройки, который затем передает данные в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-110">The workflow passes the results of the query to the remotely hosted portion of the add-in, which then passes the information to SharePoint.</span></span>
    
<span data-ttu-id="14d95-111">Данные, полученные из веб-службы могут храниться в списках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-111">The information retrieved from the web service can be stored in SharePoint lists.</span></span> <span data-ttu-id="14d95-112">В этой статье описываются три примеров кода, показывающие, как для вызова веб-служб из рабочих процессов, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="14d95-112">This article describes three code samples that show you how to call web services from workflows, as listed in the following table.</span></span> <span data-ttu-id="14d95-113">В первых двух примеры рабочих процессов и списки развертываются на-сайт при установке надстройки.</span><span class="sxs-lookup"><span data-stu-id="14d95-113">In the first two samples, the workflows and the lists are deployed to the add-in web when the add-in installs.</span></span> <span data-ttu-id="14d95-114">Последний пример содержит основные оболочки рабочего процесса и инструкции по его развертывание на хост-сайт и связать его со списком на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="14d95-114">The last sample provides the basic shell of a workflow and instructions for how to deploy it to the host web and associate it with a list on the host web.</span></span> 

<span data-ttu-id="14d95-115">**Задачи рабочего процесса и связанные примеры**</span><span class="sxs-lookup"><span data-stu-id="14d95-115">**Workflow tasks and associated samples**</span></span>

|<span data-ttu-id="14d95-116">**Задача**</span><span class="sxs-lookup"><span data-stu-id="14d95-116">**Task**</span></span>|<span data-ttu-id="14d95-117">**Пример**</span><span class="sxs-lookup"><span data-stu-id="14d95-117">**Sample**</span></span>|
|:-----|:-----|
|<span data-ttu-id="14d95-118">Вызов пользовательских веб-служб из рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="14d95-118">Call custom web services from a workflow</span></span>|[<span data-ttu-id="14d95-119">Workflow.CallCustomService</span><span class="sxs-lookup"><span data-stu-id="14d95-119">Workflow.CallCustomService</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)|
|<span data-ttu-id="14d95-120">Вызов пользовательской веб-службы из рабочего процесса и обновление SharePoint с помощью SharePoint веб-прокси</span><span class="sxs-lookup"><span data-stu-id="14d95-120">Call a custom web service from a workflow and update SharePoint by using the SharePoint web proxy</span></span>|[<span data-ttu-id="14d95-121">Workflow.CallServiceUpdateSPViaProxy</span><span class="sxs-lookup"><span data-stu-id="14d95-121">Workflow.CallServiceUpdateSPViaProxy</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)|
|<span data-ttu-id="14d95-122">Сопоставление рабочего процесса с веб-узла</span><span class="sxs-lookup"><span data-stu-id="14d95-122">Associate a workflow with the host web</span></span>|[<span data-ttu-id="14d95-123">Workflow.AssociateToHostWeb</span><span class="sxs-lookup"><span data-stu-id="14d95-123">Workflow.AssociateToHostWeb</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)|

## <a name="call-custom-web-services-from-a-workflow"></a><span data-ttu-id="14d95-124">Вызов пользовательских веб-служб из рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="14d95-124">Call custom web services from a workflow</span></span>
<span data-ttu-id="14d95-125"><a name="bk1"> </a></span><span class="sxs-lookup"><span data-stu-id="14d95-125"></span></span>

<span data-ttu-id="14d95-126">Пример [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) демонстрируется создание рабочего процесса, который вызывает настраиваемой веб-службы, который обновляет данные списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-126">The  [Workflow.CallCustomService ](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) sample shows you how to create a workflow that calls a custom web service that updates SharePoint list data.</span></span> <span data-ttu-id="14d95-127">Он также показано, как для разработки надстройки размещением у поставщика, чтобы при выполнении запроса к веб-службе с помощью удаленного веб-приложения, которое выполняет развертывание с помощью надстройки.</span><span class="sxs-lookup"><span data-stu-id="14d95-127">It also shows you how to design a provider-hosted add-in so that it queries a web service by using the remotely hosted web application that deploys with the add-in.</span></span> <span data-ttu-id="14d95-128">В этом примере полезен, если необходимо использовать все взаимодействия с веб-службы будут обрабатываться удаленно размещенной часть надстройка размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="14d95-128">This sample is useful when you want all the interactions with the web service to be handled by the remotely hosted portion of your provider-hosted add-in.</span></span>

<span data-ttu-id="14d95-129">Пример работает, запустив рабочего процесса из удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="14d95-129">The sample works by starting a workflow from a remote web application.</span></span> <span data-ttu-id="14d95-130">Этот рабочий процесс передает сведения о запросов, отправленных пользователем, для удаленного веб-приложения, который затем использует эти сведения для создания запроса к веб-службе Northwind OData.</span><span class="sxs-lookup"><span data-stu-id="14d95-130">This workflow passes query information submitted by the user to the remote web application, which then uses that information to construct a query to the Northwind OData web service.</span></span> <span data-ttu-id="14d95-131">Запрос возвращает поставщики продукта данной страны.</span><span class="sxs-lookup"><span data-stu-id="14d95-131">The query returns the product suppliers for a given country.</span></span> <span data-ttu-id="14d95-132">После получения этой информации, удаленное веб-приложение обновляет список поставщиков продуктов, надстройка развернут на-сайт.</span><span class="sxs-lookup"><span data-stu-id="14d95-132">After it receives that information, the remote web application updates a product suppliers list that the add-in has deployed to the add-in web.</span></span>

<span data-ttu-id="14d95-133">**Примечание**  Пример страницы [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) содержит инструкции по развертыванию эта надстройка.</span><span class="sxs-lookup"><span data-stu-id="14d95-133">**Note**  The  [Workflow.CallCustomService ](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) sample page contains instructions for deploying this add-in.</span></span> <span data-ttu-id="14d95-134">Можно также развертывание и тестирование с помощью F5 отладки в Visual Studio, следуя инструкциям, представленным в записи блога [SharePoint 2013 отладки рабочих процессов с помощью Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).</span><span class="sxs-lookup"><span data-stu-id="14d95-134">You can also deploy and test with F5 debugging in Visual Studio if you follow the instructions in the blog post [Debugging SharePoint 2013 workflows using Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).</span></span>

<span data-ttu-id="14d95-135">Начальная страница этого приложения включает в себя раскрывающееся меню, в котором можно выбрать страны, для которого требуется создать список поставщиков продукта (рис. 1).</span><span class="sxs-lookup"><span data-stu-id="14d95-135">This app's start page includes a drop-down menu from which you can select a country for which you want to create a product suppliers list (Figure 1).</span></span> 

<span data-ttu-id="14d95-136">**На рисунке 1. Workflow.CallCustomService пример добавления в начало страницы**</span><span class="sxs-lookup"><span data-stu-id="14d95-136">**Figure 1. Workflow.CallCustomService sample add-in start page**</span></span>

![Снимок экрана, показывающий начальной странице примера приложения](media/b2def940-9c82-458b-8f57-7ea92548ea71.png)

<span data-ttu-id="14d95-138">Кнопку **Создать** на экране вызывает метод **Create** в файле Controllers\PartSuppliersController.cs, который создает новую запись в списке поставщиков часть добавить в Интернете.</span><span class="sxs-lookup"><span data-stu-id="14d95-138">The  **Create** button on the screen calls a **Create** method in the Controllers\PartSuppliersController.cs file that creates a new entry in the Part Suppliers list on the add-in web.</span></span> <span data-ttu-id="14d95-139">Метод **Create** затем вызывает метод **Add** , определенных в файле Services\PartSuppliersService.cs.</span><span class="sxs-lookup"><span data-stu-id="14d95-139">The **Create** method then calls the **Add** method that is defined in the Services\PartSuppliersService.cs file.</span></span> <span data-ttu-id="14d95-140">В следующих примерах кода показана последовательность.</span><span class="sxs-lookup"><span data-stu-id="14d95-140">The sequence is shown in the following two code examples.</span></span>

<span data-ttu-id="14d95-141">**Создайте метод**</span><span class="sxs-lookup"><span data-stu-id="14d95-141">**Create method**</span></span>

```
public ActionResult Create(string country, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);
            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                var id = service.GetIdByCountry(country);
                if (id == null)
                {
                    id = service.Add(country);
                    TempData["Message"] = "Part Supplier Successfully Created!";
                }
                else
                    TempData["ErrorMessage"] = string.Format("Failed to Create The Part Supplier: There's already a Part Supplier who's country is {0}.", country);

                return RedirectToAction("Details", new { id = id.Value, SPHostUrl = spHostUrl });
            }
        }

```

<span data-ttu-id="14d95-142">**Метод Add**</span><span class="sxs-lookup"><span data-stu-id="14d95-142">**Add method**</span></span>

```
public int Add(string country)
        {
            var item = list.AddItem(new ListItemCreationInformation());
            item["Country"] = country;
            item.Update();
            clientContext.ExecuteQuery();
            return item.Id;
        }

```

<span data-ttu-id="14d95-143">После создания этого нового элемента списка, надстройка представляет кнопку, которая запускает рабочий процесс утверждения, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="14d95-143">After creating that new list item, the add-in presents a button that starts the approval workflow, as shown in Figure 2.</span></span>

<span data-ttu-id="14d95-144">**На рисунке 2. Запуск рабочего процесса кнопки в примере приложения**</span><span class="sxs-lookup"><span data-stu-id="14d95-144">**Figure 2. Start Workflow button in the sample app**</span></span>

![Снимок экрана, показывающий страницы запуска рабочего процесса в примере приложения](media/1d5fc6a1-79fe-4767-b8d8-905a10354565.png)

<span data-ttu-id="14d95-146">Нажав кнопку **Запустить рабочий процесс** вызывает метод **StartWorkflow** , определенный в файле Controllers\PartSuppliersController.cs.</span><span class="sxs-lookup"><span data-stu-id="14d95-146">Choosing the  **Start Workflow** button triggers the **StartWorkflow** method that is defined in the Controllers\PartSuppliersController.cs file.</span></span> <span data-ttu-id="14d95-147">Этот метод пакеты надстройки URL-адрес, URL-адрес службы web (для удаленного веб-приложения, не для веб-службы "Борей") и значения маркер контекста и передает их в метод **StartWorkflow** .</span><span class="sxs-lookup"><span data-stu-id="14d95-147">This method packages the add-in web URL, the web service URL (for your remotely hosted web application, not for the Northwind web service), and the context token values, and passes them to the **StartWorkflow** method.</span></span> <span data-ttu-id="14d95-148">Метод **PartSuppliersService** потребуется маркер контекста для взаимодействия с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-148">The **PartSuppliersService** method will need the context token to interact with SharePoint.</span></span>

```
public ActionResult StartWorkflow(int id, Guid workflowSubscriptionId, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext) as SharePointAcsContext;

            var webServiceUrl = Url.RouteUrl("DefaultApi", new { httproute = "", controller = "Data" }, Request.Url.Scheme);
            var payload = new Dictionary<string, object>
                {
                    { "appWebUrl", spContext.SPAppWebUrl.ToString() },
                    { "webServiceUrl", webServiceUrl },
                    { "contextToken",  spContext.ContextToken }
                };

            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                service.StartWorkflow(workflowSubscriptionId, id, payload);
            }

            TempData["Message"] = "Workflow Successfully Started!";
            return RedirectToAction("Details", new { id = id, SPHostUrl = spHostUrl });
        }

```

<span data-ttu-id="14d95-149">Метод **StartWorkflow** затем создает экземпляр рабочего процесса и передает три значения (appWebUrl, webServiceUrl, contextToken), хранящиеся в переменной полезных данных в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="14d95-149">The  **StartWorkflow** method then creates a workflow instance and passes the three values (appWebUrl, webServiceUrl, contextToken) stored in the payload variable to the workflow.</span></span>

```
 {
            var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);

            var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
            var subscription = subscriptionService.GetSubscription(subscriptionId);

            var instanceService = workflowServicesManager.GetWorkflowInstanceService();
            instanceService.StartWorkflowOnListItem(subscription, itemId, payload);
            clientContext.ExecuteQuery();
        }

```

<span data-ttu-id="14d95-150">После запуска рабочего процесса, он отправляет запрос **POST HTTP** для удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="14d95-150">After the workflow starts, it makes a  **POST HTTP** request to the remotely hosted web application.</span></span> <span data-ttu-id="14d95-151">Этот запрос сообщает веб-приложение для обновления списка поставщиков с поставщиками для страны, который был только что добавлен.</span><span class="sxs-lookup"><span data-stu-id="14d95-151">This request tells the web application to update the suppliers list with the suppliers for the country that the user has just added.</span></span> <span data-ttu-id="14d95-152">Файл Controllers\DataController.cs содержит метод **POST** , которая получает содержимое этого запроса.</span><span class="sxs-lookup"><span data-stu-id="14d95-152">The Controllers\DataController.cs file contains a **POST** method that receives the contents of this request.</span></span>

```
public void Post([FromBody]string country)
        {
            var supplierNames = GetSupplierNames(country);
            UpdateSuppliers(country, supplierNames);
        }

```

<span data-ttu-id="14d95-153">Метод **GetSupplierNames** (в файле Controllers\DataController.cs) создает и выполняет запрос LINQ для веб-службы "Борей" OData для всех поставщиков, связанных с выбранной страны.</span><span class="sxs-lookup"><span data-stu-id="14d95-153">The  **GetSupplierNames** method (in the Controllers\DataController.cs file) constructs and executes a LINQ query to the Northwind OData web service for all the suppliers associated with the selected country.</span></span> <span data-ttu-id="14d95-154">Метод **UpdateSuppliers** затем обновляет поле theSuppliers только что добавленный список элемента, как показано в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="14d95-154">The **UpdateSuppliers** method then updates theSuppliers field of the newly added list item, as shown in the following two code examples.</span></span>

<span data-ttu-id="14d95-155">**Запрос данных "Борей"**</span><span class="sxs-lookup"><span data-stu-id="14d95-155">**Query Northwind**</span></span>

```
private string[] GetSupplierNames(string country)
        {
            Uri uri = new Uri("http://services.odata.org/V3/Northwind/Northwind.svc");
            var entities = new NorthwindEntities(uri);
            var names = entities.Suppliers
                .Where(s => s.Country == country)
                .AsEnumerable()
                .Select(s => s.CompanyName)
                .ToArray();
            return names;
        }

```

<span data-ttu-id="14d95-156">**Обновление списка поставщиков**</span><span class="sxs-lookup"><span data-stu-id="14d95-156">**Update suppliers list**</span></span>

```
private void UpdateSuppliers(string country, string[] supplierNames)
        {
            var request = HttpContext.Current.Request;
            var authority = request.Url.Authority;
            var spAppWebUrl = request.Headers["SPAppWebUrl"];
            var contextToken = request.Headers["SPContextToken"];

            using (var clientContext = TokenHelper.GetClientContextWithContextToken(
                spAppWebUrl, contextToken, authority))
            {
                var service = new PartSuppliersService(clientContext);
                service.UpdateSuppliers(country, supplierNames);
            }
        }

```

<span data-ttu-id="14d95-157">Если вы откроете в представление конструирования файла workflow.xaml в каталоге утверждать поставщики проекта приложения, вы увидите (, выбрав вкладку **аргументы** в нижней левой части в представление конструирования), что рабочий процесс сохраняет три значения в переменной thepayload передаваемого ему в качестве аргументов рабочего процесса (на рисунке 3).</span><span class="sxs-lookup"><span data-stu-id="14d95-157">If you look at the design view of the workflow.xaml file in the Approve Suppliers directory of the app project, you'll see (by choosing the  **Arguments** tab at the bottom left of the design view) that the workflow stores the three values in thepayload variable that is passed to it as workflow arguments (Figure 3).</span></span>

<span data-ttu-id="14d95-158">**На рисунке 3. Полезные данные аргументов, передаваемых в рабочий процесс**</span><span class="sxs-lookup"><span data-stu-id="14d95-158">**Figure 3. Payload arguments passed to the workflow**</span></span>

![Снимок экрана, которая отображает экран для ввода полезных данных аргументов, передаваемых в рабочий процесс](media/4bd5cbde-d505-4d35-9fe6-50ea79f63263.png)

<span data-ttu-id="14d95-160">Действие **HttpSend** возникает перед рабочего процесса утверждения.</span><span class="sxs-lookup"><span data-stu-id="14d95-160">The  **HttpSend** activity occurs before workflow approval.</span></span> <span data-ttu-id="14d95-161">Это действие отправляет запрос **POST** в удаленных веб-приложение, которое срабатывает вызова веб-службы "Борей" и затем обновление элемента списка (с помощью списка поставщиков).</span><span class="sxs-lookup"><span data-stu-id="14d95-161">This activity sends the **POST** query to your remote web application that triggers the call to the Northwind web service and then the list item update (with the suppliers list).</span></span> <span data-ttu-id="14d95-162">Это действие настроена для отправки запроса thewebServiceUrl значение, которое передается в качестве аргумента рабочего процесса (на рисунке 4).</span><span class="sxs-lookup"><span data-stu-id="14d95-162">This activity is configured to send the request to thewebServiceUrl value that was passed as a workflow argument (Figure 4).</span></span>

<span data-ttu-id="14d95-163">**На рисунке 4. Действие HttpSend значение Uri**</span><span class="sxs-lookup"><span data-stu-id="14d95-163">**Figure 4. HttpSend activity Uri value**</span></span>

![Снимок экрана, показывающий текстовое поле для ввода URL-адрес службы web отправки HTTP](media/7f8c1f8c-b045-4b35-9435-5fcf1be12835.png)

<span data-ttu-id="14d95-165">Запрос **POST** также передает значение страны, которая хранится в элементе списка, на котором рабочий процесс работает (на рисунке 5).</span><span class="sxs-lookup"><span data-stu-id="14d95-165">The  **POST** request also passes the country value that is stored in the list item on which the workflow is operating (Figure 5).</span></span>

<span data-ttu-id="14d95-166">**На рисунке 5. Сетка свойств для действия HttpSend**</span><span class="sxs-lookup"><span data-stu-id="14d95-166">**Figure 5. Property grid for the HttpSend activity**</span></span>

![Снимок экрана, показывающий сетки свойств для действия отправки HTTP](media/7a241a29-5b3b-4c82-b86b-67159685dd02.png)

<span data-ttu-id="14d95-168">Рабочий процесс отправляет appWebUrl andcontextToken значения в веб-приложение через заголовки запроса (на рисунке 6).</span><span class="sxs-lookup"><span data-stu-id="14d95-168">The workflow sends the appWebUrl andcontextToken values to the web application through the request headers (Figure 6).</span></span> <span data-ttu-id="14d95-169">Заголовки также необходимо задать типы контента для отправки и приема запросов.</span><span class="sxs-lookup"><span data-stu-id="14d95-169">The headers also set the content types for sending and accepting requests.</span></span>

<span data-ttu-id="14d95-170">**На рисунке 6. Заголовки для действия HttpSend запросов**</span><span class="sxs-lookup"><span data-stu-id="14d95-170">**Figure 6. Request headers for the HttpSend activity**</span></span>

![Снимок экрана, показывающий таблица для добавления HTTP отправки заголовков запроса активности](media/1c019be6-f509-4ff3-83af-e1ecb1f7fbe5.png)

<span data-ttu-id="14d95-172">Если рабочий процесс утверждения, он изменяется значение поля isApproved элемента списка значение **true**.</span><span class="sxs-lookup"><span data-stu-id="14d95-172">If the workflow is approved, it changes the value of the isApproved field of the list item to **true**.</span></span>

## <a name="call-a-custom-web-service-from-a-workflow-and-update-sharepoint-by-using-the-sharepoint-web-proxy"></a><span data-ttu-id="14d95-173">Вызов пользовательской веб-службы из рабочего процесса и обновление SharePoint с помощью SharePoint веб-прокси</span><span class="sxs-lookup"><span data-stu-id="14d95-173">Call a custom web service from a workflow and update SharePoint by using the SharePoint web proxy</span></span>
<span data-ttu-id="14d95-174"><a name="bk2"> </a></span><span class="sxs-lookup"><span data-stu-id="14d95-174"></span></span>

<span data-ttu-id="14d95-175">Пример [Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) показано, как для разработки у поставщика надстройки для запроса веб-службе, а затем передать эти сведения в список SharePoint с помощью веб-прокси SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="14d95-175">The  [Workflow.CallServiceUpdateSPViaProxy ](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) sample shows how to design a provider-hosted add-in to query a web service and then pass that information to a SharePoint list via the SharePoint 2013 web proxy.</span></span>

<span data-ttu-id="14d95-176">В примере показано задание, которое используется при инкапсуляции все взаимодействия с веб-службы, чтобы они обрабатываются рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="14d95-176">The sample shows a task that is useful when you want to encapsulate all the interactions with a web service so that they are handled directly by the workflow.</span></span> <span data-ttu-id="14d95-177">С помощью веб-прокси упрощает обновление удаленного сайта логики приложения без необходимости обновления экземпляра рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="14d95-177">Using the web proxy makes it easier to update the remote web application logic without having to update the workflow instance.</span></span> <span data-ttu-id="14d95-178">Если вы не используете прокси-сервер и чтобы обновить логики в веб-приложении, необходимо удалить существующие экземпляры рабочих процессов, а затем снова развернуть надстройки.</span><span class="sxs-lookup"><span data-stu-id="14d95-178">If you're not using the proxy and you have to update the logic in your web application, you'll have to remove the existing workflow instances and then redeploy the add-in.</span></span> <span data-ttu-id="14d95-179">По этой причине корпорация Майкрософт рекомендует этот конструктор при необходимости для вызова удаленной веб-службы.</span><span class="sxs-lookup"><span data-stu-id="14d95-179">For this reason, we recommend this design when you need to call a remote web service.</span></span> 

<span data-ttu-id="14d95-180">**Примечание**  Пример страницы [Workflow.CallCustomServiceUpdateViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) содержит инструкции по развертыванию эта надстройка.</span><span class="sxs-lookup"><span data-stu-id="14d95-180">**Note**  The  [Workflow.CallCustomServiceUpdateViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) sample page contains instructions for deploying this add-in.</span></span> <span data-ttu-id="14d95-181">Кроме того, можно развернуть и проверки надстройки с помощью **F5** отладки в Visual Studio, следуя инструкциям, представленным в записи блога [SharePoint 2013 отладки рабочих процессов с помощью Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).</span><span class="sxs-lookup"><span data-stu-id="14d95-181">You can also deploy and test the add-in by using **F5** debugging in Visual Studio if you follow the instructions in the blog post [Debugging SharePoint 2013 workflows using Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).</span></span>

<span data-ttu-id="14d95-182">Рабочий процесс запуска примера из удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="14d95-182">The sample starts a workflow from a remote web application.</span></span> <span data-ttu-id="14d95-183">Этот рабочий процесс передает сведения о запросов, отправленных пользователем с помощью веб-службы "Борей" OData.</span><span class="sxs-lookup"><span data-stu-id="14d95-183">This workflow passes query information submitted by the user to the Northwind OData web service.</span></span> <span data-ttu-id="14d95-184">Запрос возвращает поставщики продукта данной страны.</span><span class="sxs-lookup"><span data-stu-id="14d95-184">The query returns the product suppliers for a given country.</span></span> <span data-ttu-id="14d95-185">После получения ответа веб-службы, рабочий процесс передает сведения из ответа для удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="14d95-185">After it receives the web service response, the workflow passes the information from the response to the remote web application.</span></span> <span data-ttu-id="14d95-186">Удаленное веб-приложение выберите обновляет список поставщиков продуктов, надстройка развернут на-сайт.</span><span class="sxs-lookup"><span data-stu-id="14d95-186">The remote web application then updates a product suppliers list that the add-in has deployed to the add-in web.</span></span>

<span data-ttu-id="14d95-187">При запуске приложения, начальная страница включает в себя раскрывающееся меню, в котором можно выбрать страны, для которого требуется создать список поставщиков продукта (на рисунке 7).</span><span class="sxs-lookup"><span data-stu-id="14d95-187">When you start the app, the start page includes a drop-down menu from which you can select a country for which you want to create a product suppliers list (Figure 7).</span></span>

<span data-ttu-id="14d95-188">**На рисунке 7. Workflow.CallServiceUpdateSPViaProxy пример добавления в начало страницы**</span><span class="sxs-lookup"><span data-stu-id="14d95-188">**Figure 7. Workflow.CallServiceUpdateSPViaProxy sample add-in start page**</span></span>

![Снимок экрана, показывающий начальной страницы для примера надстройки с пакетом обновления для приложения рабочего процесса, прокси-сервера](media/29a447b3-f17d-441f-b428-dd2a34285bb6.png)

<span data-ttu-id="14d95-190">Эта кнопка вызывает метод в файле Controllers\PartSuppliersController.cs, который создает новую запись в списке **Поставщиков часть** добавить в Интернете.</span><span class="sxs-lookup"><span data-stu-id="14d95-190">That button calls a method in the Controllers\PartSuppliersController.cs file that creates a new entry in the  **Part Suppliers** list on the add-in web.</span></span> <span data-ttu-id="14d95-191">Метод **Create** в этом файле вызывает метод **Add** , определенных в файле Services\PartSuppliersService.cs.</span><span class="sxs-lookup"><span data-stu-id="14d95-191">The **Create** method in that file calls the **Add** method that is defined in the Services\PartSuppliersService.cs file.</span></span> <span data-ttu-id="14d95-192">В следующих примерах показаны оба.</span><span class="sxs-lookup"><span data-stu-id="14d95-192">Both are shown in the following two code examples.</span></span>

<span data-ttu-id="14d95-193">**Создайте метод**</span><span class="sxs-lookup"><span data-stu-id="14d95-193">**Create method**</span></span>

```
public ActionResult Create(string country, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);
            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                var id = service.GetIdByCountry(country);
                if (id == null)
                {
                    id = service.Add(country);
                    TempData["Message"] = "Part Supplier Successfully Created!";
                }
                else
                    TempData["ErrorMessage"] = string.Format("Failed to Create The Part Supplier: There's already a Part Supplier who's country is {0}.", country);

                return RedirectToAction("Details", new { id = id.Value, SPHostUrl = spHostUrl });
            }
        }

```

<span data-ttu-id="14d95-194">**Метод Add**</span><span class="sxs-lookup"><span data-stu-id="14d95-194">**Add method**</span></span>

```
public int Add(string country)
        {
            var item = list.AddItem(new ListItemCreationInformation());
            item["Country"] = country;
            item.Update();
            clientContext.ExecuteQuery();
            return item.Id;
        }

```

<span data-ttu-id="14d95-195">После создания этого нового элемента списка, надстройка представляет кнопку, которая запускает рабочий процесс утверждения (на рисунке 8).</span><span class="sxs-lookup"><span data-stu-id="14d95-195">After it creates that new list item, the add-in presents a button that starts the approval workflow (Figure 8).</span></span>

<span data-ttu-id="14d95-196">**На рисунке 8. Кнопка «Пуск» рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="14d95-196">**Figure 8. Start Workflow button**</span></span>

![Снимок экрана, на которой отображаются страницы запуска рабочего процесса в настраиваемой веб-службы](media/69576609-f4c1-4160-9f82-3099e0a07d58.png)

<span data-ttu-id="14d95-198">Кнопки **Запустить рабочий процесс** вызывает метод **StartWorkflow** в файле Controllers\PartSuppliersController.cs.</span><span class="sxs-lookup"><span data-stu-id="14d95-198">Choosing the  **Start Workflow** button triggers the **StartWorkflow** method in the Controllers\PartSuppliersController.cs file.</span></span> <span data-ttu-id="14d95-199">Этот метод пакеты URL-адрес веб-надстройки и URL-адрес службы web (для удаленного веб-приложения, не для веб-службы "Борей") и передает их в метод **StartWorkflow** в файле Services\PartSuppliersService.cs.</span><span class="sxs-lookup"><span data-stu-id="14d95-199">This method packages the add-in web URL and the web service URL (for your remotely hosted web application, not for the Northwind web service) and passes them to the **StartWorkflow** method in the Services\PartSuppliersService.cs file.</span></span> <span data-ttu-id="14d95-200">Рабочий процесс будет обмениваться данными с удаленного веб-приложения с помощью веб-прокси и веб-прокси добавляется маркер доступа в заголовок запроса.</span><span class="sxs-lookup"><span data-stu-id="14d95-200">The workflow is going to communicate with the remote web application via the web proxy, and the web proxy will add the access token in a request header.</span></span> <span data-ttu-id="14d95-201">Вот почему рабочего процесса не передает маркер контекста в метод **StartWorkflow** в этом примере.</span><span class="sxs-lookup"><span data-stu-id="14d95-201">This is why the workflow doesn't pass a context token to the **StartWorkflow** method in this sample.</span></span> <span data-ttu-id="14d95-202">В следующем примере показан пример кода.</span><span class="sxs-lookup"><span data-stu-id="14d95-202">The code is shown in the following example.</span></span>

```
public ActionResult StartWorkflow(int id, Guid workflowSubscriptionId, string spHostUrl)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(HttpContext);

            var webServiceUrl = Url.RouteUrl("DefaultApi", new { httproute = "", controller = "Data" }, Request.Url.Scheme);
            var payload = new Dictionary<string, object>
                {
                    { "appWebUrl", spContext.SPAppWebUrl.ToString() },
                    { "webServiceUrl", webServiceUrl }
                };

            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                var service = new PartSuppliersService(clientContext);
                service.StartWorkflow(workflowSubscriptionId, id, payload);
            }

            TempData["Message"] = "Workflow Successfully Started!";
            return RedirectToAction("Details", new { id = id, SPHostUrl = spHostUrl });
        }

```

<span data-ttu-id="14d95-203">Метод **StartWorkflow** создает экземпляр рабочего процесса и передает два значения (appWebUrl andwebServiceUrl), хранящиеся в переменной полезных данных в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="14d95-203">The  **StartWorkflow** method creates a workflow instance and passes the two values (appWebUrl andwebServiceUrl) stored in the payload variable to the workflow.</span></span>

```
public void StartWorkflow(Guid subscriptionId, int itemId, Dictionary<string, object> payload)
        {
            var workflowServicesManager = new WorkflowServicesManager(clientContext, clientContext.Web);

            var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
            var subscription = subscriptionService.GetSubscription(subscriptionId);

            var instanceService = workflowServicesManager.GetWorkflowInstanceService();
            instanceService.StartWorkflowOnListItem(subscription, itemId, payload);
            clientContext.ExecuteQuery();
        }

```

<span data-ttu-id="14d95-204">После запуска рабочего процесса и перед ее утверждения, рабочий процесс выполняет запрос к веб-службы "Борей" для получения списка поставщиков для страны, что выбранный.</span><span class="sxs-lookup"><span data-stu-id="14d95-204">After the workflow starts, and before it is approved, the workflow makes a query to the Northwind web service to retrieve the suppliers list for the country that you selected.</span></span> <span data-ttu-id="14d95-205">Это осуществляется с помощью **HTTPSend** действие, которое отправляет запрос OData этой конечной точки: `"http://services.odata.org/V3/Northwind/Northwind.svc/Suppliers/?$filter=Country eq '" + country.Replace("'", "''") + "'&amp;$select=CompanyName"`.</span><span class="sxs-lookup"><span data-stu-id="14d95-205">It does this by using an  **HTTPSend** activity that sends an OData query to this endpoint: `"http://services.odata.org/V3/Northwind/Northwind.svc/Suppliers/?$filter=Country eq '" + country.Replace("'", "''") + "'&amp;$select=CompanyName"`.</span></span> <span data-ttu-id="14d95-206">Действие **HttpSend** должен быть настроен как с помощью заголовков **Accept** , указывающее JSON без метаданных запроса **GET** : ` application/json;odata=nometadata` (цифры 9 и 10).</span><span class="sxs-lookup"><span data-stu-id="14d95-206">The  **HttpSend** activity should be configured as a **GET** request with an **Accept** header that specifies JSON with no metadata: ` application/json;odata=nometadata` (Figures 9 and 10).</span></span>

<span data-ttu-id="14d95-207">**На рисунке 9. Конфигурация HttpSend активности**</span><span class="sxs-lookup"><span data-stu-id="14d95-207">**Figure 9. HttpSend activity configuration**</span></span>

![Снимок экрана, показывающий сетка активности отправки HTTP, настроенных как запрос GET](media/8f6c5d61-4d09-4a68-9745-3548d7353d73.png)

<span data-ttu-id="14d95-209">**На рисунке 10. Заголовки запроса HttpSend активности**</span><span class="sxs-lookup"><span data-stu-id="14d95-209">**Figure 10. HttpSend activity request headers**</span></span>

![Снимок экрана, показывающий сетки заголовки запроса для действия отправки HTTP](media/5cac4a52-cb8e-432a-bf72-6d0fa100f3fd.png)

<span data-ttu-id="14d95-211">Если пользователь выбрал Канада для нового элемента списка поставщиков, например, как показано в следующем примере будет ответа формате JSON.</span><span class="sxs-lookup"><span data-stu-id="14d95-211">If the user selected Canada for the new supplier list item, for example, the JSON-formatted response will be as shown in the following example.</span></span>

```
{
    value: [
        {
            CompanyName: "Ma Maison"
        },
        {
            CompanyName: "Forêts d'érables"
        }
    ]
}

```

<span data-ttu-id="14d95-212">После запуска рабочего процесса, он отправляет запрос **POST HTTP** , в котором перечислены поставщики удаленного веб-приложению с помощью прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="14d95-212">After the workflow starts, it makes a  **POST HTTP** request that contains the suppliers list to the remotely hosted web application via the proxy.</span></span> <span data-ttu-id="14d95-213">Это осуществляется с помощью действия **HttpSend** , которая запрашивает URL-адрес прокси-сервера: `appWebUrl + "/_api/SP.WebProxy.invoke"`.</span><span class="sxs-lookup"><span data-stu-id="14d95-213">It does this via an **HttpSend** activity that queries the web proxy URL: `appWebUrl + "/_api/SP.WebProxy.invoke"`.</span></span> <span data-ttu-id="14d95-214">Рабочий процесс затем передает список поставщика, полученных от службы данных "Борей" путем создания и передачи полезных настраиваемые службы.</span><span class="sxs-lookup"><span data-stu-id="14d95-214">The workflow then passes the supplier list that it has received from the Northwind service by building and passing a custom service payload.</span></span> <span data-ttu-id="14d95-215">**Создания полезных данных службы настраиваемых** свойств действия содержат список поставщиков и код для страны поставщика, как показано на рисунке 11.</span><span class="sxs-lookup"><span data-stu-id="14d95-215">The  **Create Custom Service Payload** activity properties contain the supplier list and the ID for the supplier country, as shown in Figure 11.</span></span>

<span data-ttu-id="14d95-216">**На рисунке 11. Создание полезной нагрузки службы настраиваемого действия**</span><span class="sxs-lookup"><span data-stu-id="14d95-216">**Figure 11. Create Custom Service Payload activity**</span></span>

![Снимок экрана, показывающая сетки свойства и значения для активности полезных данных службы web настраиваемых](media/7a155105-e6d5-456a-8985-eab03d6dfad9.png)

<span data-ttu-id="14d95-218">** Создание WebProxy полезных данных ** активности создает полезных данных, который передает содержимое этой полезной нагрузки в веб-URL прокси-сервера (на рисунке 12).</span><span class="sxs-lookup"><span data-stu-id="14d95-218">The ** Create WebProxy Payload** activity constructs a payload that passes the contents of this payload to the web proxy URL (Figure 12).</span></span>

<span data-ttu-id="14d95-219">**На рисунке 12. Создание конфигурации WebProxy полезных данных**</span><span class="sxs-lookup"><span data-stu-id="14d95-219">**Figure 12. Create WebProxy Payload configuration**</span></span>

![Снимок экрана, которая отображает диалоговое окно создания полезных данных WebProxy активности](media/0f016d2c-8e90-4d23-aea3-095ad6bf288a.png)

<span data-ttu-id="14d95-221">Свойства для этой операции укажите URL-адрес веб-надстройки, длина содержимого запроса POST и тип и приемки тип запроса с помощью заголовков запроса (на рисунке 13).</span><span class="sxs-lookup"><span data-stu-id="14d95-221">The properties for this activity specify the add-in web URL, the POST request content length and type, and the request acceptance type via request headers (Figure 13).</span></span>

<span data-ttu-id="14d95-222">**На рисунке 13. Сетка свойств действия WebProxy полезных данных**</span><span class="sxs-lookup"><span data-stu-id="14d95-222">**Figure 13. WebProxy Payload activity properties grid**</span></span>

![Снимок экрана, показывающий сетки свойств для действия WebProxy полезных данных](media/0b335b2d-7bb3-43ec-ab96-019b493533a3.png)

<span data-ttu-id="14d95-224">После создания рабочего процесса в полезных данных и запрос, он передает запрос веб-прокси с помощью действия **HttpSend** , настроенный как запрос POST для URL-адрес прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="14d95-224">After the workflow has constructed the payload and the request, it passes the request to the web proxy by using an  **HttpSend** activity that's configured as a POST request to the web proxy URL.</span></span> <span data-ttu-id="14d95-225">Заголовки запроса укажите OData в формате JSON в заголовках **Content-Type** и **принять** (рисунок 14).</span><span class="sxs-lookup"><span data-stu-id="14d95-225">The request headers specify JSON-formatted OData in the **Content-Type** and **Accept** headers (Figure 14).</span></span>

<span data-ttu-id="14d95-226">**На рисунке 14. Свойства действия HttpSend**</span><span class="sxs-lookup"><span data-stu-id="14d95-226">**Figure 14. Properties for the HttpSend activity**</span></span>

![Снимок экрана, которая отображает диалоговое окно запроса заголовки для действия отправки HTTP](media/01ce82fb-4690-4226-874a-c4734a17d9a4.png)

<span data-ttu-id="14d95-228">Метод **Post** в файле Controllers\DataController.cs принимает содержимое запроса, которое отправляет рабочего процесса через веб-прокси.</span><span class="sxs-lookup"><span data-stu-id="14d95-228">The  **Post** method inside the Controllers\DataController.cs file accepts the contents of the request that the workflow sends through the web proxy.</span></span> <span data-ttu-id="14d95-229">С помощью метода **Post** в предыдущем примере вызывается метод для получения списка из данных "Борей", а также другая — для обновления списка SharePoint, соответствующего поставщика.</span><span class="sxs-lookup"><span data-stu-id="14d95-229">The **Post** method in the previous sample called a method for retrieving the supplier list from Northwind as well as one for updating the corresponding SharePoint supplier list.</span></span> <span data-ttu-id="14d95-230">Поскольку рабочего процесса в этом примере уже запрос службы Northwind, эта версия метода необходимо только обновить список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-230">Since the workflow in this sample has already queried the Northwind service, this version of the method needs only to update the SharePoint list.</span></span> <span data-ttu-id="14d95-231">Он также передает URL-адрес веб-надстройки и маркер доступа (которая передается по веб-прокси) в метод **UpdateSuppliers** в файле Services\PartSuppliersService.cs, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="14d95-231">It also passes the add-in web URL and the access token (which is passed by the web proxy) to the **UpdateSuppliers** method in the Services\PartSuppliersService.cs file, as shown in the following code example.</span></span>

```
public void Post(UpdatePartSupplierModel model)
        {
            var request = HttpContext.Current.Request;
            var authority = request.Url.Authority;
            var spAppWebUrl = request.Headers["SPAppWebUrl"];
            var accessToken = request.Headers["X-SP-AccessToken"];

            using (var clientContext = TokenHelper.GetClientContextWithContextToken(spAppWebUrl, accessToken, authority))
            {
                var service = new PartSuppliersService(clientContext);
                service.UpdateSuppliers(model.Id, model.Suppliers.Select(s => s.CompanyName));
            }
        }

```

<span data-ttu-id="14d95-232">Метод **UpdateSuppliers** в файле PartSuppliers.cs обновляет поле theSuppliers элемента только что созданный списка.</span><span class="sxs-lookup"><span data-stu-id="14d95-232">The  **UpdateSuppliers** method in the PartSuppliers.cs file updates theSuppliers field of the newly created list item.</span></span>

```
public void UpdateSuppliers(int id, IEnumerable<string> supplierNames)
        {
            var item = list.GetItemById(id);
            clientContext.Load(item);
            clientContext.ExecuteQuery();

            string commaSeparatedList = String.Join(",", supplierNames);
            item["Suppliers"] = commaSeparatedList;
            item.Update();
            clientContext.ExecuteQuery();
        }

```

<span data-ttu-id="14d95-233">Если рабочий процесс утверждения, он изменяется значение поля isApproved элемента списка значение true.</span><span class="sxs-lookup"><span data-stu-id="14d95-233">If the workflow is approved, it changes the value of the isApproved field of the list item to true.</span></span>

## <a name="associate-a-workflow-with-the-host-web"></a><span data-ttu-id="14d95-234">Сопоставление рабочего процесса с веб-узла</span><span class="sxs-lookup"><span data-stu-id="14d95-234">Associate a workflow with the host web</span></span>
<span data-ttu-id="14d95-235"><a name="bk3"> </a></span><span class="sxs-lookup"><span data-stu-id="14d95-235"></span></span>

<span data-ttu-id="14d95-236">В примере [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) показано, как развертывание рабочего процесса к хост-сети и свяжите его со списком на хост-сайта с помощью средств в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="14d95-236">The  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) sample shows you how to deploy a workflow to the host web and associate it with a list on the host web by using tools in Visual Studio 2013.</span></span> <span data-ttu-id="14d95-237">Инструкции по в этом примере показано, как создание рабочего процесса в Visual Studio, развертывание хост-сети и свяжите его со списком на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="14d95-237">The instructions for this sample show you how to create a workflow in Visual Studio, deploy it to the host web, and associate it with a list on the host web.</span></span>

<span data-ttu-id="14d95-238">Данный пример содержит простой рабочий процесс, который может быть связано с любого списка.</span><span class="sxs-lookup"><span data-stu-id="14d95-238">The sample contains a simple workflow that can be associated with any list.</span></span> <span data-ttu-id="14d95-239">Инструкции по развертыванию этот рабочий процесс показано, как устранить текущего ограничения инструментов рабочего процесса Visual Studio упаковка приложения, открыв его и изменения файла конфигурации и затем распаковка его вручную перед развертыванием в узле Web.</span><span class="sxs-lookup"><span data-stu-id="14d95-239">The instructions for deploying this workflow show you how to work around the current limitations of the Visual Studio workflow tools by packaging the app, opening it up and editing a configuration file, and then repackaging it manually before deploying it to the host web.</span></span>

<span data-ttu-id="14d95-240">При открытии этого проекта в Visual Studio, вы увидите, что это простой универсальный рабочего процесса, которая предназначена для работы с любым списком SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14d95-240">When you open this project in Visual Studio, you'll see that it is a simple, generic workflow that is designed to work with any SharePoint list.</span></span> <span data-ttu-id="14d95-241">Отличный от списка задач рабочего процесса он не развертывание любого списка, с которым могут быть связаны.</span><span class="sxs-lookup"><span data-stu-id="14d95-241">Other than the workflow task list, it doesn't deploy any list with which it can be associated.</span></span>

<span data-ttu-id="14d95-242">**Примечание**  Не удается выполнить задачу, показанную в этом примере с помощью Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="14d95-242">**Note**  You cannot perform the task shown in this sample by using Visual Studio 2013.</span></span> <span data-ttu-id="14d95-243">В этом примере предоставляет полезные обходной путь.</span><span class="sxs-lookup"><span data-stu-id="14d95-243">This sample provides a useful workaround.</span></span> <span data-ttu-id="14d95-244">Если в будущем обновляются набора средств Visual Studio, не может потребоваться использовать этот способ.</span><span class="sxs-lookup"><span data-stu-id="14d95-244">If the Visual Studio tools are updated in the future, you might not need to use this workaround.</span></span>

### <a name="deploy-a-workflow-to-the-host-web"></a><span data-ttu-id="14d95-245">Развертывание рабочего процесса на веб-сайт</span><span class="sxs-lookup"><span data-stu-id="14d95-245">Deploy a workflow to the host web</span></span>

1. <span data-ttu-id="14d95-246">Откройте контекстное меню (щелкните правой кнопкой мыши) в [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) проект в обозревателе проектов и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="14d95-246">Open the shortcut menu (right-click) for the  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) add-in project in the project explorer, and select **Publish**.</span></span> <span data-ttu-id="14d95-247">Появится окно, содержащее кнопки **пакета приложения** , как показано на рис.</span><span class="sxs-lookup"><span data-stu-id="14d95-247">You'll see a window that contains a  **Package the app** button, as shown in Figure 15.</span></span>
    
    <span data-ttu-id="14d95-248">**На рисунке 15. Публикация экрана надстройки**</span><span class="sxs-lookup"><span data-stu-id="14d95-248">**Figure 15. Publish your add-in screen**</span></span>
    
    ![Снимок экрана, показывающий опубликовать страницу приложения для публикации в примере приложения](media/b003cc8b-90dc-4d49-8cb7-8b563f25f056.png)

2. <span data-ttu-id="14d95-250">При выборе **пакета приложения**Visual Studio создает файл Workflow.AssociateToHostWeb.app в `bin\Debug\app.publish\1.0.0.0` каталог решения.</span><span class="sxs-lookup"><span data-stu-id="14d95-250">When you choose  **Package the app**, Visual Studio creates a Workflow.AssociateToHostWeb.app file in the  `bin\Debug\app.publish\1.0.0.0` directory of your solution.</span></span> <span data-ttu-id="14d95-251">В этом App-файл — это тип zip-файл.</span><span class="sxs-lookup"><span data-stu-id="14d95-251">This .app file is a type of zip file.</span></span>
    
3. <span data-ttu-id="14d95-252">Извлеките содержимое файла с помощью изменения расширения файла на ZIP.</span><span class="sxs-lookup"><span data-stu-id="14d95-252">Extract the contents of the file by first changing the file extension to .zip.</span></span> 
    
4. <span data-ttu-id="14d95-253">В каталоге, который вы извлекли найдите и откройте XML-файл с именем WorkflowManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="14d95-253">In the directory that you've extracted, locate and open the XML file named WorkflowManifest.xml.</span></span> <span data-ttu-id="14d95-254">Файл пуст.</span><span class="sxs-lookup"><span data-stu-id="14d95-254">The file is empty.</span></span>
    
5. <span data-ttu-id="14d95-255">Добавьте следующий фрагмент XML в файл и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="14d95-255">Add the following XML fragment to the file and then save the file.</span></span>
    
    ```XML
      <SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
        <IntegratedApp>true</IntegratedApp>
      </SPIntegratedWorkflow>
    ```

6. <span data-ttu-id="14d95-256">Выберите значение все файлы в папке извлеченные, а затем откройте контекстное меню (щелкните правой кнопкой мыши) для файлов и выберите **Отправить** > **сжатый ZIP-папку**.</span><span class="sxs-lookup"><span data-stu-id="14d95-256">Select all the files in the extracted folder, and then open the shortcut menu (right-click) for the files and select  **Send to** > **Compressed (zipped) folder**.</span></span>
    
7. <span data-ttu-id="14d95-257">ZIP-файл, который вы только что создали, измените расширение файла, которое. приложение.</span><span class="sxs-lookup"><span data-stu-id="14d95-257">On the zip file you just created, change the file extension to .app.</span></span> <span data-ttu-id="14d95-258">Теперь должна появиться новый пакет Workflow.AssociateToHostWeb.app, содержащий обновленный файл WorkflowManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="14d95-258">You should now have a new Workflow.AssociateToHostWeb.app package that contains the updated WorkflowManifest.xml file.</span></span>
    
8. <span data-ttu-id="14d95-259">Добавьте надстройку в каталог приложения.</span><span class="sxs-lookup"><span data-stu-id="14d95-259">Add the add-in to your app catalog.</span></span>
    
9. <span data-ttu-id="14d95-260">Установка надстройки на сайт узла.</span><span class="sxs-lookup"><span data-stu-id="14d95-260">Install the add-in to your host site.</span></span>
    
10. <span data-ttu-id="14d95-261">Перейдите к списку на узле размещения и выберите **список** слева параметр редактирования в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="14d95-261">Go to a list on your host site and select the  **List** editing option at the top left of the page.</span></span> <span data-ttu-id="14d95-262">Вы увидите меню раскрывающийся список **Параметров рабочих процессов** (на рисунке 16).</span><span class="sxs-lookup"><span data-stu-id="14d95-262">You'll see a **Workflow Settings** drop-down menu (Figure 16).</span></span>
    
    <span data-ttu-id="14d95-263">**На рисунке 16. Параметры рабочего процесса для списка**</span><span class="sxs-lookup"><span data-stu-id="14d95-263">**Figure 16. Workflow settings for a list**</span></span>
    
    ![Снимок экрана, который отображает параметры рабочего процесса для списка](media/195d2d5b-091e-46aa-aefd-e1b883b1c33e.png)

11. <span data-ttu-id="14d95-265">Выберите ** Добавить рабочий процесс ** в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="14d95-265">Select ** Add a Workflow** from the drop-down menu.</span></span>
    
12. <span data-ttu-id="14d95-266">Вы увидите параметр выделения, как на рисунке на рисунке 17.</span><span class="sxs-lookup"><span data-stu-id="14d95-266">You will now see a selection option similar to the image in Figure 17.</span></span> <span data-ttu-id="14d95-267">Выберите приложение **Workflow.AssociateToHostWeb** в списке доступных параметров.</span><span class="sxs-lookup"><span data-stu-id="14d95-267">Select the  **Workflow.AssociateToHostWeb** app from the list of available options.</span></span>
    
    <span data-ttu-id="14d95-268">**На рисунке 17. Добавление параметров рабочего процесса**</span><span class="sxs-lookup"><span data-stu-id="14d95-268">**Figure 17. Add a workflow settings**</span></span>
    
    ![Снимок экрана, показывающий добавления на страницу параметров рабочего процесса](media/08317057-4546-4ad9-b8c5-d5b33bc4350d.png)

<span data-ttu-id="14d95-270">Развертывание рабочего процесса в веб-сайт и связанный со списком на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="14d95-270">You have now deployed the workflow to the host web and associated it with a list on the host web.</span></span> <span data-ttu-id="14d95-271">Можно запуск рабочего процесса вручную или рабочих процессов в Visual Studio можно обновить, чтобы оно запускается другими способами.</span><span class="sxs-lookup"><span data-stu-id="14d95-271">You can trigger a workflow manually, or you can update the workflow in Visual Studio so that it is triggered in other ways.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14d95-272">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="14d95-272">Additional resources</span></span>
<span data-ttu-id="14d95-273"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="14d95-273"></span></span>

-  [<span data-ttu-id="14d95-274">Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="14d95-274">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="14d95-275">Отладка с помощью Visual Studio 2013 рабочих процессов SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="14d95-275">Debugging SharePoint 2013 workflows using Visual Studio 2013</span></span>](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)
    
-  [<span data-ttu-id="14d95-276">Workflow.AssociateToHostWeb</span><span class="sxs-lookup"><span data-stu-id="14d95-276">Workflow.AssociateToHostWeb</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [<span data-ttu-id="14d95-277">Workflow.CallServiceUpdateSPViaProxy</span><span class="sxs-lookup"><span data-stu-id="14d95-277">Workflow.CallServiceUpdateSPViaProxy</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
    
-  [<span data-ttu-id="14d95-278">Workflow.AssociateToHostWeb</span><span class="sxs-lookup"><span data-stu-id="14d95-278">Workflow.AssociateToHostWeb</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [<span data-ttu-id="14d95-279">Workflow.CallCustomService</span><span class="sxs-lookup"><span data-stu-id="14d95-279">Workflow.CallCustomService</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
