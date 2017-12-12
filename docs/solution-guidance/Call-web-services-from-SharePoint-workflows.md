---
title: "Вызов веб-служб из рабочих процессов SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e7644ca38ef29c564c8d1ac627cef6d527d5c5d9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="call-web-services-from-sharepoint-workflows"></a>Вызов веб-служб из рабочих процессов SharePoint

Развертывание рабочего процесса SharePoint 2013 на хост-сайт из надстройки для SharePoint и вызов веб-служб из рабочих процессов SharePoint.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Модель SharePoint 2013 надстройки можно использовать для создания и развертывания рабочих процессов, которые запускаются на добавление в веб-сайта или веб-сайт. Эти рабочие процессы могут взаимодействовать с удаленными части размещением у поставщика надстроек. Рабочие процессы можно также вызвать удаленного веб-служб, которые содержат важные бизнес-данных в одном из двух способов: 

- С помощью передачи данных запроса удаленно размещенной часть надстройки. Удаленное веб-приложение затем вызывает веб-службы и передает данные обратно в SharePoint.
    
- С помощью запроса веб-службы с помощью SharePoint 2013 веб-прокси-сервера. Рабочий процесс передает результаты запроса удаленно размещенной часть надстройки, который затем передает данные в SharePoint.
    
Данные, полученные из веб-службы могут храниться в списках SharePoint. В этой статье описываются три примеров кода, показывающие, как для вызова веб-служб из рабочих процессов, как показано в следующей таблице. В первых двух примеры рабочих процессов и списки развертываются на-сайт при установке надстройки. Последний пример содержит основные оболочки рабочего процесса и инструкции по его развертывание на хост-сайт и связать его со списком на хост-сайта. 

**Задачи рабочего процесса и связанные примеры**

|**Задача**|**Пример**|
|:-----|:-----|
|Вызов пользовательских веб-служб из рабочего процесса|[Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)|
|Вызов пользовательской веб-службы из рабочего процесса и обновление SharePoint с помощью SharePoint веб-прокси|[Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)|
|Сопоставление рабочего процесса с веб-узла|[Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)|

## <a name="call-custom-web-services-from-a-workflow"></a>Вызов пользовательских веб-служб из рабочего процесса
<a name="bk1"> </a>

Пример [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) демонстрируется создание рабочего процесса, который вызывает настраиваемой веб-службы, который обновляет данные списка SharePoint. Он также показано, как для разработки надстройки размещением у поставщика, чтобы при выполнении запроса к веб-службе с помощью удаленного веб-приложения, которое выполняет развертывание с помощью надстройки. В этом примере полезен, если необходимо использовать все взаимодействия с веб-службы будут обрабатываться удаленно размещенной часть надстройка размещением у поставщика.

Пример работает, запустив рабочего процесса из удаленного веб-приложения. Этот рабочий процесс передает сведения о запросов, отправленных пользователем, для удаленного веб-приложения, который затем использует эти сведения для создания запроса к веб-службе Northwind OData. Запрос возвращает поставщики продукта данной страны. После получения этой информации, удаленное веб-приложение обновляет список поставщиков продуктов, надстройка развернут на-сайт.

> [!NOTE] 
> Пример страницы [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) содержит инструкции по развертыванию эта надстройка. Можно также развертывание и тестирование с помощью F5 отладки в Visual Studio, следуя инструкциям, представленным в записи блога [SharePoint 2013 отладки рабочих процессов с помощью Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).

Начальная страница этого приложения включает в себя раскрывающееся меню, в котором можно выбрать страны, для которого требуется создать список поставщиков продукта (рис. 1). 

**На рисунке 1. Workflow.CallCustomService пример добавления в начало страницы**

![Снимок экрана, показывающий начальной странице примера приложения](media/b2def940-9c82-458b-8f57-7ea92548ea71.png)

Кнопку **Создать** на экране вызывает метод **Create** в файле Controllers\PartSuppliersController.cs, который создает новую запись в списке поставщиков часть добавить в Интернете. Метод **Create** затем вызывает метод **Add** , определенных в файле Services\PartSuppliersService.cs. В следующих примерах кода показана последовательность.

**Создайте метод**

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

**Метод Add**

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

После создания этого нового элемента списка, надстройка представляет кнопку, которая запускает рабочий процесс утверждения, как показано на рисунке 2.

**На рисунке 2. Запуск рабочего процесса кнопки в примере приложения**

![Снимок экрана, показывающий страницы запуска рабочего процесса в примере приложения](media/1d5fc6a1-79fe-4767-b8d8-905a10354565.png)

Нажав кнопку **Запустить рабочий процесс** вызывает метод **StartWorkflow** , определенный в файле Controllers\PartSuppliersController.cs. Этот метод пакеты надстройки URL-адрес, URL-адрес службы web (для удаленного веб-приложения, не для веб-службы "Борей") и значения маркер контекста и передает их в метод **StartWorkflow** . Метод **PartSuppliersService** потребуется маркер контекста для взаимодействия с SharePoint.

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

Метод **StartWorkflow** затем создает экземпляр рабочего процесса и передает три значения (appWebUrl, webServiceUrl, contextToken), хранящиеся в переменной полезных данных в рабочий процесс.

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

После запуска рабочего процесса, он отправляет запрос **POST HTTP** для удаленного веб-приложения. Этот запрос сообщает веб-приложение для обновления списка поставщиков с поставщиками для страны, который был только что добавлен. Файл Controllers\DataController.cs содержит метод **POST** , которая получает содержимое этого запроса.

```
public void Post([FromBody]string country)
        {
            var supplierNames = GetSupplierNames(country);
            UpdateSuppliers(country, supplierNames);
        }

```

Метод **GetSupplierNames** (в файле Controllers\DataController.cs) создает и выполняет запрос LINQ для веб-службы "Борей" OData для всех поставщиков, связанных с выбранной страны. Метод **UpdateSuppliers** затем обновляет поле theSuppliers только что добавленный список элемента, как показано в следующих примерах.

**Запрос данных "Борей"**

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

**Обновление списка поставщиков**

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

Если вы откроете в представление конструирования файла workflow.xaml в каталоге утверждать поставщики проекта приложения, вы увидите (, выбрав вкладку **аргументы** в нижней левой части в представление конструирования), что рабочий процесс сохраняет три значения в переменной thepayload передаваемого ему в качестве аргументов рабочего процесса (на рисунке 3).

**На рисунке 3. Полезные данные аргументов, передаваемых в рабочий процесс**

![Снимок экрана, которая отображает экран для ввода полезных данных аргументов, передаваемых в рабочий процесс](media/4bd5cbde-d505-4d35-9fe6-50ea79f63263.png)

Действие **HttpSend** возникает перед рабочего процесса утверждения. Это действие отправляет запрос **POST** в удаленных веб-приложение, которое срабатывает вызова веб-службы "Борей" и затем обновление элемента списка (с помощью списка поставщиков). Это действие настроена для отправки запроса thewebServiceUrl значение, которое передается в качестве аргумента рабочего процесса (на рисунке 4).

**На рисунке 4. Действие HttpSend значение Uri**

![Снимок экрана, показывающий текстовое поле для ввода URL-адрес службы web отправки HTTP](media/7f8c1f8c-b045-4b35-9435-5fcf1be12835.png)

Запрос **POST** также передает значение страны, которая хранится в элементе списка, на котором рабочий процесс работает (на рисунке 5).

**На рисунке 5. Сетка свойств для действия HttpSend**

![Снимок экрана, показывающий сетки свойств для действия отправки HTTP](media/7a241a29-5b3b-4c82-b86b-67159685dd02.png)

Рабочий процесс отправляет appWebUrl andcontextToken значения в веб-приложение через заголовки запроса (на рисунке 6). Заголовки также необходимо задать типы контента для отправки и приема запросов.

**На рисунке 6. Заголовки для действия HttpSend запросов**

![Снимок экрана, показывающий таблица для добавления HTTP отправки заголовков запроса активности](media/1c019be6-f509-4ff3-83af-e1ecb1f7fbe5.png)

Если рабочий процесс утверждения, он изменяется значение поля isApproved элемента списка значение **true**.

## <a name="call-a-custom-web-service-from-a-workflow-and-update-sharepoint-by-using-the-sharepoint-web-proxy"></a>Вызов пользовательской веб-службы из рабочего процесса и обновление SharePoint с помощью SharePoint веб-прокси
<a name="bk2"> </a>

Пример [Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) показано, как для разработки у поставщика надстройки для запроса веб-службе, а затем передать эти сведения в список SharePoint с помощью веб-прокси SharePoint 2013.

В примере показано задание, которое используется при инкапсуляции все взаимодействия с веб-службы, чтобы они обрабатываются рабочим процессом. С помощью веб-прокси упрощает обновление удаленного сайта логики приложения без необходимости обновления экземпляра рабочего процесса. Если вы не используете прокси-сервер и чтобы обновить логики в веб-приложении, необходимо удалить существующие экземпляры рабочих процессов, а затем снова развернуть надстройки. По этой причине корпорация Майкрософт рекомендует этот конструктор при необходимости для вызова удаленной веб-службы. 

> [!NOTE] 
> Пример страницы [Workflow.CallCustomServiceUpdateViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) содержит инструкции по развертыванию эта надстройка. Кроме того, можно развернуть и проверки надстройки с помощью **F5** отладки в Visual Studio, следуя инструкциям, представленным в записи блога [SharePoint 2013 отладки рабочих процессов с помощью Visual Studio 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx).

Рабочий процесс запуска примера из удаленного веб-приложения. Этот рабочий процесс передает сведения о запросов, отправленных пользователем с помощью веб-службы "Борей" OData. Запрос возвращает поставщики продукта данной страны. После получения ответа веб-службы, рабочий процесс передает сведения из ответа для удаленного веб-приложения. Удаленное веб-приложение выберите обновляет список поставщиков продуктов, надстройка развернут на-сайт.

При запуске приложения, начальная страница включает в себя раскрывающееся меню, в котором можно выбрать страны, для которого требуется создать список поставщиков продукта (на рисунке 7).

**На рисунке 7. Workflow.CallServiceUpdateSPViaProxy пример добавления в начало страницы**

![Снимок экрана, показывающий начальной страницы для примера надстройки с пакетом обновления для приложения рабочего процесса, прокси-сервера](media/29a447b3-f17d-441f-b428-dd2a34285bb6.png)

Эта кнопка вызывает метод в файле Controllers\PartSuppliersController.cs, который создает новую запись в списке **Поставщиков часть** добавить в Интернете. Метод **Create** в этом файле вызывает метод **Add** , определенных в файле Services\PartSuppliersService.cs. В следующих примерах показаны оба.

**Создайте метод**

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

**Метод Add**

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

После создания этого нового элемента списка, надстройка представляет кнопку, которая запускает рабочий процесс утверждения (на рисунке 8).

**На рисунке 8. Кнопка «Пуск» рабочего процесса**

![Снимок экрана, на которой отображаются страницы запуска рабочего процесса в настраиваемой веб-службы](media/69576609-f4c1-4160-9f82-3099e0a07d58.png)

Кнопки **Запустить рабочий процесс** вызывает метод **StartWorkflow** в файле Controllers\PartSuppliersController.cs. Этот метод пакеты URL-адрес веб-надстройки и URL-адрес службы web (для удаленного веб-приложения, не для веб-службы "Борей") и передает их в метод **StartWorkflow** в файле Services\PartSuppliersService.cs. Рабочий процесс будет обмениваться данными с удаленного веб-приложения с помощью веб-прокси и веб-прокси добавляется маркер доступа в заголовок запроса. Вот почему рабочего процесса не передает маркер контекста в метод **StartWorkflow** в этом примере. В следующем примере показан пример кода.

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

Метод **StartWorkflow** создает экземпляр рабочего процесса и передает два значения (appWebUrl andwebServiceUrl), хранящиеся в переменной полезных данных в рабочий процесс.

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

После запуска рабочего процесса и перед ее утверждения, рабочий процесс выполняет запрос к веб-службы "Борей" для получения списка поставщиков для страны, что выбранный. Это осуществляется с помощью **HTTPSend** действие, которое отправляет запрос OData этой конечной точки: `"http://services.odata.org/V3/Northwind/Northwind.svc/Suppliers/?$filter=Country eq '" + country.Replace("'", "''") + "'&amp;$select=CompanyName"`. Действие **HttpSend** должен быть настроен как с помощью заголовков **Accept** , указывающее JSON без метаданных запроса **GET** : ` application/json;odata=nometadata` (цифры 9 и 10).

**На рисунке 9. Конфигурация HttpSend активности**

![Снимок экрана, показывающий сетка активности отправки HTTP, настроенных как запрос GET](media/8f6c5d61-4d09-4a68-9745-3548d7353d73.png)

**На рисунке 10. Заголовки запроса HttpSend активности**

![Снимок экрана, показывающий сетки заголовки запроса для действия отправки HTTP](media/5cac4a52-cb8e-432a-bf72-6d0fa100f3fd.png)

Если пользователь выбрал Канада для нового элемента списка поставщиков, например, как показано в следующем примере будет ответа формате JSON.

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

После запуска рабочего процесса, он отправляет запрос **POST HTTP** , в котором перечислены поставщики удаленного веб-приложению с помощью прокси-сервера. Это осуществляется с помощью действия **HttpSend** , которая запрашивает URL-адрес прокси-сервера: `appWebUrl + "/_api/SP.WebProxy.invoke"`. Рабочий процесс затем передает список поставщика, полученных от службы данных "Борей" путем создания и передачи полезных настраиваемые службы. **Создания полезных данных службы настраиваемых** свойств действия содержат список поставщиков и код для страны поставщика, как показано на рисунке 11.

**На рисунке 11. Создание полезной нагрузки службы настраиваемого действия**

![Снимок экрана, показывающая сетки свойства и значения для активности полезных данных службы web настраиваемых](media/7a155105-e6d5-456a-8985-eab03d6dfad9.png)

** Создание WebProxy полезных данных ** активности создает полезных данных, который передает содержимое этой полезной нагрузки в веб-URL прокси-сервера (на рисунке 12).

**На рисунке 12. Создание конфигурации WebProxy полезных данных**

![Снимок экрана, которая отображает диалоговое окно создания полезных данных WebProxy активности](media/0f016d2c-8e90-4d23-aea3-095ad6bf288a.png)

Свойства для этой операции укажите URL-адрес веб-надстройки, длина содержимого запроса POST и тип и приемки тип запроса с помощью заголовков запроса (на рисунке 13).

**На рисунке 13. Сетка свойств действия WebProxy полезных данных**

![Снимок экрана, показывающий сетки свойств для действия WebProxy полезных данных](media/0b335b2d-7bb3-43ec-ab96-019b493533a3.png)

После создания рабочего процесса в полезных данных и запрос, он передает запрос веб-прокси с помощью действия **HttpSend** , настроенный как запрос POST для URL-адрес прокси-сервера. Заголовки запроса укажите OData в формате JSON в заголовках **Content-Type** и **принять** (рисунок 14).

**На рисунке 14. Свойства действия HttpSend**

![Снимок экрана, которая отображает диалоговое окно запроса заголовки для действия отправки HTTP](media/01ce82fb-4690-4226-874a-c4734a17d9a4.png)

Метод **Post** в файле Controllers\DataController.cs принимает содержимое запроса, которое отправляет рабочего процесса через веб-прокси. С помощью метода **Post** в предыдущем примере вызывается метод для получения списка из данных "Борей", а также другая — для обновления списка SharePoint, соответствующего поставщика. Поскольку рабочего процесса в этом примере уже запрос службы Northwind, эта версия метода необходимо только обновить список SharePoint. Он также передает URL-адрес веб-надстройки и маркер доступа (которая передается по веб-прокси) в метод **UpdateSuppliers** в файле Services\PartSuppliersService.cs, как показано в следующем примере кода.

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

Метод **UpdateSuppliers** в файле PartSuppliers.cs обновляет поле theSuppliers элемента только что созданный списка.

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

Если рабочий процесс утверждения, он изменяется значение поля isApproved элемента списка значение true.

## <a name="associate-a-workflow-with-the-host-web"></a>Сопоставление рабочего процесса с веб-узла
<a name="bk3"> </a>

В примере [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) показано, как развертывание рабочего процесса к хост-сети и свяжите его со списком на хост-сайта с помощью средств в Visual Studio 2013. Инструкции по в этом примере показано, как создание рабочего процесса в Visual Studio, развертывание хост-сети и свяжите его со списком на хост-сайта.

Данный пример содержит простой рабочий процесс, который может быть связано с любого списка. Инструкции по развертыванию этот рабочий процесс показано, как устранить текущего ограничения инструментов рабочего процесса Visual Studio упаковка приложения, открыв его и изменения файла конфигурации и затем распаковка его вручную перед развертыванием в узле Web.

При открытии этого проекта в Visual Studio, вы увидите, что это простой универсальный рабочего процесса, которая предназначена для работы с любым списком SharePoint. Отличный от списка задач рабочего процесса он не развертывание любого списка, с которым могут быть связаны.

> [!NOTE] 
> Не удается выполнить задачу, показанную в этом примере с помощью Visual Studio 2013. В этом примере предоставляет полезные обходной путь. Если в будущем обновляются набора средств Visual Studio, не может потребоваться использовать этот способ.

### <a name="deploy-a-workflow-to-the-host-web"></a>Развертывание рабочего процесса на веб-сайт

1. Откройте контекстное меню (щелкните правой кнопкой мыши) в [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb) проект в обозревателе проектов и выберите **Опубликовать**. Появится окно, содержащее кнопки **пакета приложения** , как показано на рис.
    
    **На рисунке 15. Публикация экрана надстройки**
    
    ![Снимок экрана, показывающий опубликовать страницу приложения для публикации в примере приложения](media/b003cc8b-90dc-4d49-8cb7-8b563f25f056.png)

2. При выборе **пакета приложения**Visual Studio создает файл Workflow.AssociateToHostWeb.app в `bin\Debug\app.publish\1.0.0.0` каталог решения. В этом App-файл — это тип zip-файл.
    
3. Извлеките содержимое файла с помощью изменения расширения файла на ZIP. 
    
4. В каталоге, который вы извлекли найдите и откройте XML-файл с именем WorkflowManifest.xml. Файл пуст.
    
5. Добавьте следующий фрагмент XML в файл и сохраните файл.
    
    ```XML
      <SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
        <IntegratedApp>true</IntegratedApp>
      </SPIntegratedWorkflow>
    ```

6. Выберите значение все файлы в папке извлеченные, а затем откройте контекстное меню (щелкните правой кнопкой мыши) для файлов и выберите **Отправить** > **сжатый ZIP-папку**.
    
7. ZIP-файл, который вы только что создали, измените расширение файла, которое. приложение. Теперь должна появиться новый пакет Workflow.AssociateToHostWeb.app, содержащий обновленный файл WorkflowManifest.xml.
    
8. Добавьте надстройку в каталог приложения.
    
9. Установка надстройки на сайт узла.
    
10. Перейдите к списку на узле размещения и выберите **список** слева параметр редактирования в верхней части страницы. Вы увидите меню раскрывающийся список **Параметров рабочих процессов** (на рисунке 16).
    
    **На рисунке 16. Параметры рабочего процесса для списка**
    
    ![Снимок экрана, который отображает параметры рабочего процесса для списка](media/195d2d5b-091e-46aa-aefd-e1b883b1c33e.png)

11. Выберите ** Добавить рабочий процесс ** в раскрывающемся меню.
    
12. Вы увидите параметр выделения, как на рисунке на рисунке 17. Выберите приложение **Workflow.AssociateToHostWeb** в списке доступных параметров.
    
    **На рисунке 17. Добавление параметров рабочего процесса**
    
    ![Снимок экрана, показывающий добавления на страницу параметров рабочего процесса](media/08317057-4546-4ad9-b8c5-d5b33bc4350d.png)

Развертывание рабочего процесса в веб-сайт и связанный со списком на хост-сайта. Можно запуск рабочего процесса вручную или рабочих процессов в Visual Studio можно обновить, чтобы оно запускается другими способами.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online](Composite-buisness-apps-for-SharePoint.md)
    
-  [Отладка с помощью Visual Studio 2013 рабочих процессов SharePoint 2013](http://blogs.msdn.com/b/officeapps/archive/2013/10/30/debugging-sharepoint-2013-workflows-using-visual-studio-2013.aspx)
    
-  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
    
-  [Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)
    
-  [Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
