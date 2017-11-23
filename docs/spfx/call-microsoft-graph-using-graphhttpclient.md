# <a name="call-microsoft-graph-using-the-sharepoint-framework-graphhttpclient"></a><span data-ttu-id="82330-101">Вызов Microsoft Graph с помощью клиента GraphHttpClient на платформе SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="82330-101">Call Microsoft Graph using the SharePoint Framework GraphHttpClient</span></span>

<span data-ttu-id="82330-p101">С помощью Microsoft Graph вы можете создавать функциональные решения, использующие данные из различных служб, входящих в состав Office 365. В прошлом подключать решения SharePoint Framework к Microsoft Graph было сложно, так как для этого требовалось зарегистрировать приложение Azure Active Directory и выполнить поток авторизации. Благодаря клиенту GraphHttpClient на платформе SharePoint Framework вы можете вызывать Microsoft Graph напрямую без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="82330-p101">Using the Microsoft Graph you can build powerful solutions that use data from the different services that are a part of Office 365. In the past, connecting SharePoint Framework solutions to the Microsoft Graph was challenging, as it required you to register an Azure Active Directory application and complete the authorization flow. With the SharePoint Framework GraphHttpClient you can directly call the Microsoft Graph, without any additional setup.</span></span>

> <span data-ttu-id="82330-105">**Важно!** В настоящее время GraphHttpClient находится на этапе тестирования разработчиками. Его не следует использовать в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="82330-105">**Important:** The GraphHttpClient is currently in developer preview and should not be used in production.</span></span>

## <a name="what-is-graphhttpclient"></a><span data-ttu-id="82330-106">Что такое GraphHttpClient</span><span class="sxs-lookup"><span data-stu-id="82330-106">What is GraphHttpClient</span></span>

<span data-ttu-id="82330-p102">GraphHttpClient — это специальный HTTP-клиент, входящий в состав SharePoint Framework. Он работает аналогично клиенту HttpClient, используемому для связи со сторонними API. Этот клиент, основанный на HttpClient, автоматически обеспечивает наличие действительного маркера доступа носителя и необходимых заголовков в запросе к Microsoft Graph. Когда вы отправляете запрос GET или POST, GraphHttpClient проверяет наличие действительного маркера доступа и, в случае его отсутствия, автоматически получает маркер из внутреннего API и сохраняет его для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="82330-p102">GraphHttpClient is a specialized HTTP client provided as a part of the SharePoint Framework. It works similarly to the HttpClient that you can use to communicate with third party APIs. On top of the HttpClient, the GraphHttpClient automatically ensures that your request to the Microsoft Graph has a valid bearer access token and required headers. Whenever you issue a GET or a POST request, the GraphHttpClient verifies that it has a valid access token, and if it doesn't, it automatically retrieves one from an internal API and stores it for subsequent requests.</span></span>

<span data-ttu-id="82330-111">Ниже представлен пример запроса к Microsoft Graph с использованием GraphHttpClient.</span><span class="sxs-lookup"><span data-stu-id="82330-111">A sample request to the Microsoft Graph using the GraphHttpClient looks as follows:</span></span>

```ts
// ...
import { GraphHttpClient, GraphClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

<span data-ttu-id="82330-p103">Для начала из пакета **@microsoft/sp-http** импортируются модули **GraphHttpClient** и **GraphClientResponse**. Затем с помощью экземпляра GraphHttpClient, доступного в свойстве `this.context.graphHttpClient`, запрос GET или POST отправляется в Microsoft Graph. В качестве параметров указываются вызываемый API Microsoft Graph (начиная с версии API без начального символа `/`) и конфигурация GraphHttpClient. При желании можно указать дополнительные заголовки запроса, которые будут объединены с заголовками по умолчанию, заданными клиентом GraphHttpClient (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` и `'Content-Type': 'application/json; charset=utf-8'`).</span><span class="sxs-lookup"><span data-stu-id="82330-p103">You start with importing the **GraphHttpClient** and **GraphClientResponse** modules from the **@microsoft/sp-http** package. Next, using the instance of the GraphHttpClient available on the `this.context.graphHttpClient` property, you issue a GET or a POST request to the Microsoft Graph. As the parameters, you specify the Microsoft Graph API that you want to call (starting with the API version without a leading `/` - slash), followed by the GraphHttpClient configuration. Optionally, you can specify additional request headers that will be merged with the default headers set by the GraphHttpClient (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` and `'Content-Type': 'application/json; charset=utf-8'`).</span></span>

## <a name="graphhttpclient-considerations"></a><span data-ttu-id="82330-116">Замечания касательно GraphHttpClient</span><span class="sxs-lookup"><span data-stu-id="82330-116">GraphHttpClient considerations</span></span>

<span data-ttu-id="82330-p104">Использование GraphHttpClient — очень удобный способ связи с Microsoft Graph, так как он позволяет абстрагироваться от потока авторизации и управления маркерами доступа. В настоящее время GraphHttpClient находится на этапе тестирования разработчиками, и перед его использованием следует учитывать некоторые особенности.</span><span class="sxs-lookup"><span data-stu-id="82330-p104">Using the GraphHttpClient is a very convenient way of communicating with the Microsoft Graph as it abstracts away the authorization flow and management of access tokens. The GraphHttpClient is currently in developer preview and there are some considerations that you should take into account before using it.</span></span>

### <a name="use-for-microsoft-graph-access-only"></a><span data-ttu-id="82330-119">Использование только для доступа к Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="82330-119">Use for Microsoft Graph access only</span></span>

<span data-ttu-id="82330-p105">GraphHttpClient предназначен только для доступа к Microsoft Graph. Указанный в запросе URL-адрес должен начинаться с версии API Microsoft Graph (**v1.0** или **beta**), за которой следует операция API. Все остальные URL-адреса отклоняются с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="82330-p105">The GraphHttpClient is meant to be used only for accessing the Microsoft Graph. The URL specified in the request must begin with the version of the Microsoft Graph API (either **v1.0** or **beta**) followed by the API operation. Any other URL will be rejected with an error.</span></span>

### <a name="available-permission-scopes"></a><span data-ttu-id="82330-123">Доступные области разрешений</span><span class="sxs-lookup"><span data-stu-id="82330-123">Available permission scopes</span></span>

<span data-ttu-id="82330-p106">GraphHttpClient использует приложение **Office 365 SharePoint Online** для Azure Active Directory, чтобы получить действительный маркер доступа к Microsoft Graph от имени текущего пользователя. Полученный маркер доступа содержит две области разрешений:</span><span class="sxs-lookup"><span data-stu-id="82330-p106">The GraphHttpClient uses the **Office 365 SharePoint Online** Azure Active Directory application to retrieve a valid access token to the Microsoft Graph on behalf of the current user. The retrieved access token contains two permissions scopes:</span></span> 

* <span data-ttu-id="82330-126">**Чтение и запись всех групп (предварительная версия)** (`Group.ReadWrite.All`)</span><span class="sxs-lookup"><span data-stu-id="82330-126">Read and write all groups</span></span> 
* <span data-ttu-id="82330-127">**Чтение всех отчетов об использовании** (`Reports.Read.All`)</span><span class="sxs-lookup"><span data-stu-id="82330-127">Read all usage reports</span></span> 

<span data-ttu-id="82330-p107">В настоящее время при использовании GraphHttpClient доступно только две области разрешений. Если для вашего решения необходимы другие области разрешений, следует использовать [ADAL JS с неявным потоком OAuth](web-parts/guidance/call-microsoft-graph-from-your-web-part).</span><span class="sxs-lookup"><span data-stu-id="82330-p107">At this moment these are the only two permissions available when using the GraphHttpClient. If you need other permission scopes in your solution, you have to use [ADAL JS with implicit OAuth flow](web-parts/guidance/call-microsoft-graph-from-your-web-part) instead.</span></span>

### <a name="tokens-are-retrieved-using-an-internal-api"></a><span data-ttu-id="82330-130">Извлечение маркеров с помощью внутреннего API</span><span class="sxs-lookup"><span data-stu-id="82330-130">Tokens are retrieved using an internal API</span></span>

<span data-ttu-id="82330-p108">Чтобы получить действительный маркер доступа, GraphHttpClient отправляет веб-запрос конечной точке `/_api/SP.OAuth.Token/Acquire`. Этот API предназначен для внутреннего использования, и к нему не следует обращаться напрямую в решениях.</span><span class="sxs-lookup"><span data-stu-id="82330-p108">To acquire a valid access token, the GraphHttpClient issues a web request to the `/_api/SP.OAuth.Token/Acquire` endpoint. This API is intended for internal use and you should not communicate with it directly in your solutions.</span></span>

## <a name="more-information"></a><span data-ttu-id="82330-133">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="82330-133">More information</span></span>

<span data-ttu-id="82330-134">Пример практического использования GraphHttpClient можно увидеть в образце решения на сайте GitHub по адресу [https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span><span class="sxs-lookup"><span data-stu-id="82330-134">To see how the GraphHttpClient can be used in practice, see a sample solution on GitHub at [https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span></span>

<span data-ttu-id="82330-135">Дополнительные сведения о Microsoft Graph см. на странице [https://developer.microsoft.com/ru-ru/graph/](https://developer.microsoft.com/ru-ru/graph/).</span><span class="sxs-lookup"><span data-stu-id="82330-135">For more information about the Microsoft Graph visit [https://developer.microsoft.com/ru-ru/graph/](https://developer.microsoft.com/ru-ru/graph/).</span></span>