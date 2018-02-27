---
title: "Общие сведения о классе GraphHttpClient (предварительная версия)\n"
description: "Используйте Microsoft Graph для создания решений с широкими возможностями, получающих доступ к данным в Office 365 и других службах Майкрософт."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 5698ccfefd4f9beff5d14947190f9269f73b0bf8
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="overview-of-the-graphhttpclient-class-preview"></a><span data-ttu-id="1713b-103">Общие сведения о классе GraphHttpClient (предварительная версия)
</span><span class="sxs-lookup"><span data-stu-id="1713b-103">Overview of the GraphHttpClient class (preview)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1713b-104">Класс **GraphHttpClient** находится на этапе тестирования, и в него могут быть внесены изменения.</span><span class="sxs-lookup"><span data-stu-id="1713b-104">The **GraphHttpClient** is currently in preview and is subject to change.</span></span> <span data-ttu-id="1713b-105">Сейчас он не поддерживается для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="1713b-105">It is not currently supported for use in production environments.</span></span>

<span data-ttu-id="1713b-106">Вы можете использовать Microsoft Graph для создания решений с широкими возможностями, получающих доступ к данным в Office 365 и других службах Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1713b-106">You can use Microsoft Graph to build powerful solutions that access data from Office 365 and other Microsoft services.</span></span> <span data-ttu-id="1713b-107">Чтобы подключить решения SharePoint Framework (SPFx) к Microsoft Graph, вам необходимо зарегистрировать приложение Azure Active Directory (Azure AD) и выполнить поток авторизации.</span><span class="sxs-lookup"><span data-stu-id="1713b-107">To connect SharePoint Framework (SPFx) solutions to Microsoft Graph, you have to register an Azure Active Directory (Azure AD) application and complete the authorization flow.</span></span> <span data-ttu-id="1713b-108">Чтобы упростить этот процесс, вы можете использовать класс SPFx **GraphHttpClient** для непосредственного вызова Microsoft Graph без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="1713b-108">To make this easier, you can use the SPFx **GraphHttpClient** class to call Microsoft Graph directly, without any additional setup.</span></span>

## <a name="what-is-the-graphhttpclient-class"></a><span data-ttu-id="1713b-109">Что представляет собой класс GraphHttpClient?</span><span class="sxs-lookup"><span data-stu-id="1713b-109">What is the GraphHttpClient class?</span></span>

<span data-ttu-id="1713b-110">Класс **GraphHttpClient** входит в состав SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="1713b-110">The **GraphHttpClient** class is included as part of the SharePoint Framework.</span></span> <span data-ttu-id="1713b-111">Он работает аналогично классу HttpClient, который вы можете использовать для взаимодействия с API сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="1713b-111">It works in a similar way to the HttpClient that you can use to communicate with third-party APIs.</span></span> <span data-ttu-id="1713b-112">Класс **GraphHttpClient** автоматически обеспечивает допустимый маркер доступа носителя и необходимые заголовки в вашем запросе к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1713b-112">The **GraphHttpClient** class automatically ensures that your request to Microsoft Graph has a valid bearer access token and the required headers.</span></span> 

<span data-ttu-id="1713b-113">При совершении запроса GET или POST класс **GraphHttpClient** проверяет, есть ли в запросе допустимый маркер доступа, и если его нет, класс автоматически получает маркер доступа из внутреннего API и сохраняет его для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="1713b-113">When you issue a GET or a POST request, **GraphHttpClient** verifies that it has a valid access token, and if it doesn't, it automatically retrieves one from an internal API and stores it for subsequent requests.</span></span>

<span data-ttu-id="1713b-114">В примере ниже показан запрос к Microsoft Graph, в котором используется класс **GraphHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="1713b-114">The following example shows a request to Microsoft Graph that uses the **GraphHttpClient** class.</span></span>

```typescript
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

<span data-ttu-id="1713b-115">Чтобы совершить запрос к Microsoft Graph, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="1713b-115">To make a request to Microsoft Graph:</span></span>

1. <span data-ttu-id="1713b-116">Импортируйте класс **GraphHttpClient** и модули **GraphHttpClientResponse** из пакета **@microsoft/sp-http**.</span><span class="sxs-lookup"><span data-stu-id="1713b-116">Import the **GraphHttpClient** and **GraphHttpClientResponse** modules from the **@microsoft/sp-http** package.</span></span>

2. <span data-ttu-id="1713b-117">Используйте экземпляр класса **GraphHttpClient**, доступный в свойстве `this.context.graphHttpClient`, чтобы создать запрос GET или POST к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1713b-117">Use the instance of **GraphHttpClient** that's available on the `this.context.graphHttpClient` property to issue a GET or POST request to Microsoft Graph.</span></span>

3. <span data-ttu-id="1713b-118">В качестве параметров укажите API Microsoft Graph, который вы хотите вызвать (начните работу с версии API без ведущей косой черты `/`), а затем укажите конфигурацию **GraphHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="1713b-118">As parameters, specify the Microsoft Graph API that you want to call (start with the API version without a leading `/` - slash), followed by the **GraphHttpClient** configuration.</span></span>

4. <span data-ttu-id="1713b-119">При необходимости вы можете указать дополнительные заголовки запроса, которые будут объединены с заголовками, используемыми по умолчанию и заданными классом **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` и `'Content-Type': 'application/json; charset=utf-8'`).</span><span class="sxs-lookup"><span data-stu-id="1713b-119">Optionally, you can specify additional request headers that will be merged with the default headers set by **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` and `'Content-Type': 'application/json; charset=utf-8'`).</span></span>

## <a name="considerations-for-using-the-graphhttpclient-class"></a><span data-ttu-id="1713b-120">Вопросы, связанные с использованием класса **GraphHttpClient**</span><span class="sxs-lookup"><span data-stu-id="1713b-120">Considerations for using the **GraphHttpClient** class</span></span>

<span data-ttu-id="1713b-121">Класс **GraphHttpClient** обеспечивает удобный способ взаимодействия с Microsoft Graph, так как он абстрагирует поток авторизации и управление маркерами доступа.</span><span class="sxs-lookup"><span data-stu-id="1713b-121">The **GraphHttpClient** class provides a convenient way to communicate with Microsoft Graph because it abstracts the authorization flow and management of access tokens.</span></span> <span data-ttu-id="1713b-122">Так как на данный момент класс **GraphHttpClient** находится на этапе тестирования и представлен в виде ознакомительной версии для разработчиков, имеется ряд моментов, которые необходимо учесть перед его использованием.</span><span class="sxs-lookup"><span data-stu-id="1713b-122">Because **GraphHttpClient** is currently in developer preview, there are some considerations that you should take into account before using it.</span></span>

### <a name="use-for-microsoft-graph-access-only"></a><span data-ttu-id="1713b-123">Использование только для доступа к Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1713b-123">Use for Microsoft Graph access only</span></span>

<span data-ttu-id="1713b-124">Используйте класс **GraphHttpClient** только для доступа к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1713b-124">Use the **GraphHttpClient** class only to access Microsoft Graph.</span></span> <span data-ttu-id="1713b-125">URL-адрес, указанный в запросе, должен начинаться с версии API Microsoft Graph (**v1.0** или **beta**), за которым должна следовать операция API.</span><span class="sxs-lookup"><span data-stu-id="1713b-125">The URL specified in the request must begin with the version of the Microsoft Graph API (either **v1.0** or **beta**), followed by the API operation.</span></span> <span data-ttu-id="1713b-126">При использовании любого другого URL-адреса будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="1713b-126">Any other URL will return an error.</span></span>

### <a name="permissions"></a><span data-ttu-id="1713b-127">Разрешения</span><span class="sxs-lookup"><span data-stu-id="1713b-127">Permissions</span></span>

<span data-ttu-id="1713b-128">Класс GraphHttpClient использует приложение Azure AD для SharePoint Online в Office 365, чтобы получать допустимые маркеры доступа для Microsoft Graph от имени текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="1713b-128">The GraphHttpClient uses the Office 365 SharePoint Online Azure AD application to retrieve a valid access token to Microsoft Graph on behalf of the current user.</span></span> <span data-ttu-id="1713b-129">Полученный маркер доступа содержит два указанных ниже разрешения.</span><span class="sxs-lookup"><span data-stu-id="1713b-129">The retrieved access token contains two permissions:</span></span>

- <span data-ttu-id="1713b-130">Чтение из всех групп и запись во все группы (ознакомительная версия) (`Group.ReadWrite.All`)</span><span class="sxs-lookup"><span data-stu-id="1713b-130">Read and write all groups (preview) (`Group.ReadWrite.All`)</span></span>
- <span data-ttu-id="1713b-131">Чтение всех отчетов об использовании (`Reports.Read.All`)</span><span class="sxs-lookup"><span data-stu-id="1713b-131">Read all usage reports (`Reports.Read.All`)</span></span>

<span data-ttu-id="1713b-132">Это единственные разрешения, которые доступны при использовании класса **GraphHttpClient**.</span><span class="sxs-lookup"><span data-stu-id="1713b-132">These are the only permissions that are available when you use **GraphHttpClient**.</span></span> <span data-ttu-id="1713b-133">Если для вашего решения необходимы другие разрешения, вы можете использовать [ADAL JS с неявным потоком OAuth](web-parts/guidance/call-microsoft-graph-from-your-web-part.md).</span><span class="sxs-lookup"><span data-stu-id="1713b-133">If you need other permissions for your solution, you can use [ADAL JS with implicit OAuth flow](web-parts/guidance/call-microsoft-graph-from-your-web-part.md) instead.</span></span>

### <a name="tokens-are-retrieved-using-an-internal-api"></a><span data-ttu-id="1713b-134">Получение маркеров с помощью внутреннего API</span><span class="sxs-lookup"><span data-stu-id="1713b-134">Tokens are retrieved using an internal API</span></span>

<span data-ttu-id="1713b-135">Чтобы получить допустимый маркер доступа, класс **GraphHttpClient** создает веб-запрос к конечной точке `/_api/SP.OAuth.Token/Acquire`.</span><span class="sxs-lookup"><span data-stu-id="1713b-135">To acquire a valid access token, **GraphHttpClient** issues a web request to the `/_api/SP.OAuth.Token/Acquire` endpoint.</span></span> <span data-ttu-id="1713b-136">Этот API предназначен для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="1713b-136">This API is intended for internal use.</span></span> <span data-ttu-id="1713b-137">В ваших решениях не следует взаимодействовать непосредственно с этим API.</span><span class="sxs-lookup"><span data-stu-id="1713b-137">You should not communicate with it directly in your solutions.</span></span>

## <a name="see-also"></a><span data-ttu-id="1713b-138">См. также</span><span class="sxs-lookup"><span data-stu-id="1713b-138">See also</span></span>

- [<span data-ttu-id="1713b-139">Вызов Microsoft Graph с помощью клиента GraphHttpClient на платформе SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="1713b-139">Use GraphHttpClient to call Microsoft Graph</span></span>](call-microsoft-graph-using-graphhttpclient.md)
- <span data-ttu-id="1713b-140">[Класс GraphClient настройщика приложений из примера современного сайта группы](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span><span class="sxs-lookup"><span data-stu-id="1713b-140">[Application Customizer GraphClient from Modern Teamsite sample](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).</span></span>
- [<span data-ttu-id="1713b-141">Центр разработки для Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1713b-141">Microsoft Graph Dev Center</span></span>](https://developer.microsoft.com/ru-RU/graph/)
- [<span data-ttu-id="1713b-142">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="1713b-142">SharePoint Framework Overview</span></span>](sharepoint-framework-overview.md)
