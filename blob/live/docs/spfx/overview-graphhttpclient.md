# <a name="overview-of-the-graphhttpclient-class-preview"></a><span data-ttu-id="896bd-101">Общие сведения о классе GraphHttpClient (ознакомительная версия)</span><span class="sxs-lookup"><span data-stu-id="896bd-101">Overview of the GraphHttpClient class (preview)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="896bd-102">Класс **GraphHttpClient** находится на этапе тестирования, и в него могут быть внесены изменения.</span><span class="sxs-lookup"><span data-stu-id="896bd-102">The **GraphHttpClient** is currently in preview and is subject to change.</span></span> <span data-ttu-id="896bd-103">Сейчас он не поддерживается для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="896bd-103">It is not currently supported for use in production environments.</span></span>

<span data-ttu-id="896bd-104">Вы можете использовать Microsoft Graph для создания решений с широкими возможностями, получающих доступ к данным в Office 365 и других службах Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="896bd-104">You can use Microsoft Graph to build powerful solutions that access data from Office 365 and other Microsoft services.</span></span> <span data-ttu-id="896bd-105">Чтобы подключить решения SharePoint Framework (SPFx) к Microsoft Graph, вам необходимо зарегистрировать приложение Azure Active Directory (Azure AD) и выполнить поток авторизации.</span><span class="sxs-lookup"><span data-stu-id="896bd-105">To connect SharePoint Framework (SPFx) solutions to Microsoft Graph, you have to register an Azure Active Directory (Azure AD) application and complete the authorization flow.</span></span> <span data-ttu-id="896bd-106">Чтобы упростить этот процесс, вы можете использовать класс SPFx **GraphHttpClient** для непосредственного вызова Microsoft Graph без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="896bd-106">To make this easier, you can use the SPFx **GraphHttpClient** class to call Microsoft Graph directly, without any additional setup.</span></span>

## <a name="what-is-the-graphhttpclient-class"></a><span data-ttu-id="896bd-107">Что представляет собой класс GraphHttpClient?</span><span class="sxs-lookup"><span data-stu-id="896bd-107">What is the GraphHttpClient class?</span></span>

<span data-ttu-id="896bd-108">Класс **GraphHttpClient** входит в состав SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="896bd-108">The **GraphHttpClient** class is included as part of the SharePoint Framework.</span></span> <span data-ttu-id="896bd-109">Он работает аналогично классу HttpClient, который вы можете использовать для взаимодействия с API сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="896bd-109">It works in a similar way to the HttpClient that you can use to communicate with third-party APIs.</span></span> <span data-ttu-id="896bd-110">Класс **GraphHttpClient** автоматически обеспечивает допустимый маркер доступа носителя и необходимые заголовки в вашем запросе к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="896bd-110">The **GraphHttpClient** class automatically ensures that your request to Microsoft Graph has a valid bearer access token and the required headers.</span></span> <span data-ttu-id="896bd-111">При совершении запроса GET или POST класс **GraphHttpClient** проверяет, есть ли в запросе допустимый маркер доступа, и если его нет, класс автоматически получает маркер доступа из внутреннего API и сохраняет его для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="896bd-111">When you issue a GET or a POST request, **GraphHttpClient** verifies that it has a valid access token, and if it doesn't, it automatically retrieves one from an internal API and stores it for subsequent requests.</span></span>

<span data-ttu-id="896bd-112">В примере ниже показан запрос к Microsoft Graph, в котором используется класс **GraphHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="896bd-112">The following example shows a request to Microsoft Graph that uses the **GraphHttpClient** class.</span></span>

```ts
// ...
import { GraphHttpClient, GraphHttpClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphHttpClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

<span data-ttu-id="896bd-113">Чтобы совершить запрос к Microsoft Graph, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="896bd-113">To make a request to Microsoft Graph:</span></span>

- <span data-ttu-id="896bd-114">Импортируйте класс **GraphHttpClient** и модули **GraphHttpClientResponse** из пакета **@microsoft/sp-http**.</span><span class="sxs-lookup"><span data-stu-id="896bd-114">Import the **GraphHttpClient** and **GraphHttpClientResponse** modules from the **@microsoft/sp-http** package.</span></span>
- <span data-ttu-id="896bd-115">Используйте экземпляр класса **GraphHttpClient**, доступный в свойстве `this.context.graphHttpClient`, чтобы создать запрос GET или POST к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="896bd-115">Use the instance of **GraphHttpClient** that's available on the `this.context.graphHttpClient` property to issue a GET or POST request to Microsoft Graph.</span></span>
- <span data-ttu-id="896bd-116">В качестве параметров укажите API Microsoft Graph, который вы хотите вызвать (начните работу с версии API без ведущей косой черты `/`), а затем укажите конфигурацию **GraphHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="896bd-116">As parameters, specify the Microsoft Graph API that you want to call (start with the API version without a leading `/` - slash), followed by the **GraphHttpClient** configuration.</span></span>
- <span data-ttu-id="896bd-117">При необходимости вы можете указать дополнительные заголовки запроса, которые будут объединены с заголовками, используемыми по умолчанию и заданными классом **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` и `'Content-Type': 'application/json; charset=utf-8'`).</span><span class="sxs-lookup"><span data-stu-id="896bd-117">Optionally, you can specify additional request headers that will be merged with the default headers set by **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` and `'Content-Type': 'application/json; charset=utf-8'`).</span></span>

## <a name="considerations-for-using-the-graphhttpclient-class"></a><span data-ttu-id="896bd-118">Вопросы, связанные с использованием класса **GraphHttpClient**</span><span class="sxs-lookup"><span data-stu-id="896bd-118">Considerations for using the **GraphHttpClient** class</span></span>

<span data-ttu-id="896bd-119">Класс **GraphHttpClient** обеспечивает удобный способ взаимодействия с Microsoft Graph, так как он абстрагирует поток авторизации и управление маркерами доступа.</span><span class="sxs-lookup"><span data-stu-id="896bd-119">The **GraphHttpClient** class provides a convenient way to communicate with Microsoft Graph because it abstracts the authorization flow and management of access tokens.</span></span> <span data-ttu-id="896bd-120">Так как на данный момент класс **GraphHttpClient** находится на этапе тестирования и представлен в виде ознакомительной версии для разработчиков, имеется ряд моментов, которые необходимо учесть перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="896bd-120">Because **GraphHttpClient** is currently in developer preview, there are some considerations that you should take into account before using it.</span></span>

### <a name="use-for-microsoft-graph-access-only"></a><span data-ttu-id="896bd-121">Использование только для доступа к Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="896bd-121">Use for Microsoft Graph access only</span></span>

<span data-ttu-id="896bd-122">Используйте класс **GraphHttpClient** только для доступа к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="896bd-122">Use the **GraphHttpClient** class only to access Microsoft Graph.</span></span> <span data-ttu-id="896bd-123">URL-адрес, указанный в запросе, должен начинаться с версии API Microsoft Graph (**v1.0** или **beta**), за которым должна следовать операция API.</span><span class="sxs-lookup"><span data-stu-id="896bd-123">The GraphHttpClient is meant to be used only for accessing the Microsoft Graph. The URL specified in the request must begin with the version of the Microsoft Graph API (either **v1.0** or **beta**) followed by the API operation. Any other URL will be rejected with an error.</span></span> <span data-ttu-id="896bd-124">При использовании любого другого URL-адреса будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="896bd-124">Any other URL will return an error.</span></span>

### <a name="permissions"></a><span data-ttu-id="896bd-125">Разрешения</span><span class="sxs-lookup"><span data-stu-id="896bd-125">Permissions</span></span>

<span data-ttu-id="896bd-126">Класс GraphHttpClient использует приложение Azure AD для SharePoint Online в Office 365, чтобы получать допустимые маркеры доступа для Microsoft Graph от имени текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="896bd-126">The GraphHttpClient uses the Office 365 SharePoint Online Azure Active Directory application to retrieve a valid access token to the Microsoft Graph on behalf of the current user. The retrieved access token contains two permissions scopes:</span></span> <span data-ttu-id="896bd-127">Полученный маркер доступа содержит два указанных ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="896bd-127">The retrieved access token contains two permissions:</span></span>

- <span data-ttu-id="896bd-128">Чтение из всех групп и запись во все группы (ознакомительная версия) (`Group.ReadWrite.All`)</span><span class="sxs-lookup"><span data-stu-id="896bd-128">Read and write all groups (preview) (`Group.ReadWrite.All`)</span></span>
- <span data-ttu-id="896bd-129">Чтение всех отчетов об использовании (`Reports.Read.All`)</span><span class="sxs-lookup"><span data-stu-id="896bd-129">Read all usage reports (`Reports.Read.All`)</span></span>

<span data-ttu-id="896bd-130">Это только те разрешения, которые доступны, когда вы используете класс **GraphHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="896bd-130">These are the only permissions that are available when you use **GraphHttpClient**.</span></span> <span data-ttu-id="896bd-131">Если для вашего решения необходимы другие разрешения, вы можете использовать [ADAL JS с неявным потоком OAuth](web-parts/guidance/call-microsoft-graph-from-your-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="896bd-131">If you need other permissions for your solution, you can use [ADAL JS with implicit OAuth flow](web-parts/guidance/call-microsoft-graph-from-your-web-part.md) instead.</span></span>

### <a name="tokens-are-retrieved-using-an-internal-api"></a><span data-ttu-id="896bd-132">Получение маркеров с помощью внутреннего API</span><span class="sxs-lookup"><span data-stu-id="896bd-132">Tokens are retrieved using an internal API</span></span>

<span data-ttu-id="896bd-133">Чтобы получить допустимый маркер доступа, класс **GraphHttpClient** создает веб-запрос к конечной точке `/_api/SP.OAuth.Token/Acquire`.</span><span class="sxs-lookup"><span data-stu-id="896bd-133">To acquire a valid access token, the GraphHttpClient issues a web request to the  endpoint. This API is intended for internal use and you should not communicate with it directly in your solutions.</span></span> <span data-ttu-id="896bd-134">Этот API предназначен для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="896bd-134">This API is intended for internal use.</span></span> <span data-ttu-id="896bd-135">В ваших решениях не следует взаимодействовать непосредственно с этим API.</span><span class="sxs-lookup"><span data-stu-id="896bd-135">You should not communicate with it directly in your solutions.</span></span>

## <a name="see-also"></a><span data-ttu-id="896bd-136">См. также</span><span class="sxs-lookup"><span data-stu-id="896bd-136">See also</span></span>

- <span data-ttu-id="896bd-137">[Класс GraphClient настройщика приложений из примера современного сайта группы](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span><span class="sxs-lookup"><span data-stu-id="896bd-137">[Application Customizer GraphClient from Modern Teamsite sample](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span></span>
- [<span data-ttu-id="896bd-138">Вызов Microsoft Graph с помощью клиента GraphHttpClient на платформе SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="896bd-138">Use GraphHttpClient to call Microsoft Graph</span></span>](call-microsoft-graph-using-graphhttpclient.md)
- [<span data-ttu-id="896bd-139">Центр разработки для Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="896bd-139">Microsoft Graph dev center</span></span>](https://developer.microsoft.com/ru-RU/graph/)
