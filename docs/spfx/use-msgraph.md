---
title: "Использование MSGraphClient для подключения к Microsoft Graph"
description: "Узнайте, как использовать класс MSGraphClient для вызова REST API Microsoft Graph."
ms.date: 02/15/2018
ms.prod: sharepoint
ms.openlocfilehash: 95e7fc8ffd5c1be022e14f3fd66449148f2e1b8d
ms.sourcegitcommit: b4110530e7dcb42282023a562073e5aebd20db19
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/21/2018
---
# <a name="use-the-msgraphclient-to-connect-to-microsoft-graph"></a><span data-ttu-id="d539d-103">Использование MSGraphClient для подключения к Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d539d-103">Use the MSGraphClient to connect to Microsoft Graph</span></span>

<span data-ttu-id="d539d-104">При создании решений SharePoint Framework вы можете легко подключаться к Microsoft Graph с помощью класса **MSGraphClient**.</span><span class="sxs-lookup"><span data-stu-id="d539d-104">When building SharePoint Framework solutions, you can easily connect to the Microsoft Graph using the **MSGraphClient**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d539d-105">В настоящее время `AadHttpClient` и `MSGraphClient` предоставляются в ознакомительных целях и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="d539d-105">Usage of `AadHttpClient` and `MSGraphClient` is currently in preview status and subject to change.</span></span> <span data-ttu-id="d539d-106">Не следует использовать эти возможности в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d539d-106">You should not use these capabilities in production environment.</span></span> <span data-ttu-id="d539d-107">Кроме того, обратите внимание, что использование свойств `webApiPermissionRequests` в `package-solution.json` не поддерживается для обычных клиентов.</span><span class="sxs-lookup"><span data-stu-id="d539d-107">Notice also that usage of `webApiPermissionRequests` properties in `package-solution.json` is not supported in normal tenants.</span></span>

## <a name="what-is-msgraphclient"></a><span data-ttu-id="d539d-108">Что такое MSGraphClient?</span><span class="sxs-lookup"><span data-stu-id="d539d-108">What is MSGraphClient</span></span>

<span data-ttu-id="d539d-109">**MSGraphClient** — это новый HTTP-клиент, появившийся в SharePoint Framework версии 1.4.1, который упрощает подключение к Microsoft Graph в решениях SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="d539d-109">**MSGraphClient** is a new HTTP client introduced in SharePoint Framework v1.4.1, that simplifies connecting to the Microsoft Graph inside SharePoint Framework solutions.</span></span> <span data-ttu-id="d539d-110">**MSGraphClient** является оболочкой для всей [клиентской библиотеки JavaScript Microsoft Graph](https://www.npmjs.com/package/@microsoft/microsoft-graph-client), предоставляя разработчикам такие же возможности, как и при использовании клиентской библиотеки в других клиентских решениях.</span><span class="sxs-lookup"><span data-stu-id="d539d-110">**MSGraphClient** wraps the existing [Microsoft Graph JavaScript Client Library](https://www.npmjs.com/package/@microsoft/microsoft-graph-client) offering developers the same capabilities as when using the client library in other client-side solutions.</span></span> <span data-ttu-id="d539d-111">Несмотря на то что вы можете напрямую использовать в решении клиентскую библиотеку JavaScript для Microsoft Graph, при использовании класса **MSGraphClient** проверка подлинности в Microsoft Graph выполняется автоматически, что позволяет сосредоточиться на разработке решения.</span><span class="sxs-lookup"><span data-stu-id="d539d-111">While you could use the Microsoft Graph JavaScript Client Library in your solution directly, using the **MSGraphClient** will handle authenticating against the Microsoft Graph for you, allowing you to focus on building your solution.</span></span>

## <a name="use-the-msgraphclient-in-your-solution"></a><span data-ttu-id="d539d-112">Использование класса MSGraphClient в решении</span><span class="sxs-lookup"><span data-stu-id="d539d-112">Use the MSGraphClient in your solution</span></span>

> [!NOTE]
> <span data-ttu-id="d539d-113">Класс **MSGraphClient** доступен только в проектах, созданных с помощью SharePoint Framework 1.4.1 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="d539d-113">The **MSGraphClient** is available only in projects built using SharePoint Framework v1.4.1 and newer.</span></span> <span data-ttu-id="d539d-114">В этой статье демонстрируется использование класса **MSGraphClient** в клиентской веб-части, но его можно с таким же успехом использовать в расширениях SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="d539d-114">While using the **MSGraphClient** is explained using a client-side web part, you can use it just as well in SharePoint Framework extensions.</span></span>

<span data-ttu-id="d539d-115">Чтобы использовать объект **MSGraphClient** в решении SharePoint Framework, добавьте выражение `import` в основной файл веб-части.</span><span class="sxs-lookup"><span data-stu-id="d539d-115">To use the **MSGraphClient** in your SharePoint Framework solution, add the following `import` clause in your main web part file:</span></span>

```ts
import { MSGraphClient } from '@microsoft/sp-client-preview';
```

<span data-ttu-id="d539d-116">**MSGraphClient** предоставляется в качестве службы, которую необходимо использовать из соответствующей области, чтобы получить ссылку на нее.</span><span class="sxs-lookup"><span data-stu-id="d539d-116">**MSGraphClient** is provided as a service, which you have to consume from the service scope to get a reference to.</span></span> <span data-ttu-id="d539d-117">Для этого добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="d539d-117">To do that, in your code add:</span></span>

```ts
export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  public render(): void {
    // ...

    const client: MSGraphClient = this.context.serviceScope.consume(MSGraphClient.serviceKey);
  }

  // ...
}
```

<span data-ttu-id="d539d-118">Получив ссылку на экземпляр **MSGraphClient**, вы можете установить связь с Microsoft Graph, используя синтаксис клиентской библиотеки JavaScript:</span><span class="sxs-lookup"><span data-stu-id="d539d-118">Once you have the reference to the **MSGraphClient** instance, you can start communicating with the Microsoft Graph, using its JavaScript Client Library syntax:</span></span>

```ts
export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  public render(): void {
    // ...

    const client: MSGraphClient = this.context.serviceScope.consume(MSGraphClient.serviceKey);
    // get information about the current user from the Microsoft Graph
    client
      .api('/me')
      .get((error, response: any, rawResponse?: any) => {
        // handle the response
    });
  }

  // ...
}
```

### <a name="use-the-microsoft-graph-typescript-types"></a><span data-ttu-id="d539d-119">Использование типов TypeScript для Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d539d-119">Use the Microsoft Graph TypeScript types</span></span>

<span data-ttu-id="d539d-120">При работе с Microsoft Graph и TypeScript вы можете использовать типы TypeScript для Microsoft Graph, которые помогут вам быстрее обнаруживать ошибки в коде.</span><span class="sxs-lookup"><span data-stu-id="d539d-120">When working with the Microsoft Graph and TypeScript, you can benefit of the Microsoft Graph TypeScript types which will help you catch errors in your code faster.</span></span> <span data-ttu-id="d539d-121">Типы TypeScript для Microsoft Graph предоставляются в виде отдельного пакета, который можно установить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="d539d-121">Microsoft Graph TypeScript types are provided as a separate package, which you can install using:</span></span>

```sh
npm install @microsoft/microsoft-graph-types --save-dev
```

<span data-ttu-id="d539d-122">Установив пакет в проекте, импортируйте его в файле веб-части с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="d539d-122">After installing the package in your project, import it in your web part file using:</span></span>

```ts
import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
```

<span data-ttu-id="d539d-123">Теперь вы можете задавать типы для объектов, полученных из Microsoft Graph, например:</span><span class="sxs-lookup"><span data-stu-id="d539d-123">Now you can type the objects retrieved from the Microsoft Graph, for example:</span></span>

```ts
export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  public render(): void {
    // ...

    const client: MSGraphClient = this.context.serviceScope.consume(MSGraphClient.serviceKey);
    // get information about the current user from the Microsoft Graph
    client
      .api('/me')
      .get((error, user: MicrosoftGraph.User, rawResponse?: any) => {
        // handle the response
    });
  }

  // ...
}
```

<span data-ttu-id="d539d-124">Дополнительные сведения о работе с клиентской библиотекой JavaScript для Microsoft Graph см. на странице [https://www.npmjs.com/package/@microsoft/microsoft-graph-client](https://www.npmjs.com/package/@microsoft/microsoft-graph-client)</span><span class="sxs-lookup"><span data-stu-id="d539d-124">For more information about working with the Microsoft Graph JavaScript Client Library see [https://www.npmjs.com/package/@microsoft/microsoft-graph-client](https://www.npmjs.com/package/@microsoft/microsoft-graph-client)</span></span>

## <a name="available-permission-scopes"></a><span data-ttu-id="d539d-125">Доступные области разрешений</span><span class="sxs-lookup"><span data-stu-id="d539d-125">Available permission scopes</span></span>

<span data-ttu-id="d539d-126">По умолчанию субъекту-службе не назначены явные разрешения на доступ к Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d539d-126">By default, the service principal has no explicit permissions granted to access the Microsoft Graph.</span></span> <span data-ttu-id="d539d-127">Однако, запросив маркер доступа для Microsoft Graph, вы получите маркер с областью разрешений `user_impersonation`, с помощью которой можно считывать сведения о пользователях (т. е. `User.Read.All`).</span><span class="sxs-lookup"><span data-stu-id="d539d-127">If you would however request an access token for the Microsoft Graph, you would get a token with the `user_impersonation` permission scope, that can be used for reading information about the users (i.e. `User.Read.All`).</span></span> <span data-ttu-id="d539d-128">Разработчики могут запрашивать дополнительные области разрешений, а администраторы клиентов — предоставлять их.</span><span class="sxs-lookup"><span data-stu-id="d539d-128">Additional permission scopes can be requested by developers and granted by tenant administrators.</span></span> <span data-ttu-id="d539d-129">Дополнительные сведения см. в справочной [статье, посвященной использованию AadHttpClient](./use-aadhttpclient.md).</span><span class="sxs-lookup"><span data-stu-id="d539d-129">For more information see the guidance [article on using the AadHttpClient](./use-aadhttpclient.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d539d-130">Вышеописанное поведение с областью разрешений `user_impersonation` может измениться перед выпуском общедоступной версии этой функции. Не рекомендуем добавлять зависимость от этих стандартных разрешений.</span><span class="sxs-lookup"><span data-stu-id="d539d-130">Above behavior with  `user_impersonation` is subject to change before general availability of of the this capability.It is not recommended to take dependency on these default permissions.</span></span>

## <a name="see-also"></a><span data-ttu-id="d539d-131">См. также</span><span class="sxs-lookup"><span data-stu-id="d539d-131">See also</span></span>

- [<span data-ttu-id="d539d-132">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d539d-132">Microsoft Graph</span></span>](https://graph.microsoft.com)
- [<span data-ttu-id="d539d-133">Клиентская библиотека JavaScript для Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d539d-133">Microsoft Graph .NET Client Library</span></span>](https://www.npmjs.com/package/@microsoft/microsoft-graph-client)
- [<span data-ttu-id="d539d-134">Примеры с использованием клиентской библиотеки JavaScript для Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d539d-134">Microsoft Graph JavaScript Client Library samples</span></span>](https://github.com/microsoftgraph/msgraph-sdk-javascript/tree/master/samples)
- <span data-ttu-id="d539d-135">[Типы TypeScript для Microsoft Graph](https://www.npmjs.com/package/@microsoft/microsoft-graph-types)</span><span class="sxs-lookup"><span data-stu-id="d539d-135">Use the [Microsoft Graph TypeScript types](https://www.npmjs.com/package/@microsoft/microsoft-graph-types)</span></span>