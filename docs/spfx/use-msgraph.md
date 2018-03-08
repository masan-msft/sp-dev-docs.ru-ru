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
# <a name="use-the-msgraphclient-to-connect-to-microsoft-graph"></a>Использование MSGraphClient для подключения к Microsoft Graph

При создании решений SharePoint Framework вы можете легко подключаться к Microsoft Graph с помощью класса **MSGraphClient**.

> [!IMPORTANT]
> В настоящее время `AadHttpClient` и `MSGraphClient` предоставляются в ознакомительных целях и могут меняться. Не следует использовать эти возможности в рабочей среде. Кроме того, обратите внимание, что использование свойств `webApiPermissionRequests` в `package-solution.json` не поддерживается для обычных клиентов.

## <a name="what-is-msgraphclient"></a>Что такое MSGraphClient?

**MSGraphClient** — это новый HTTP-клиент, появившийся в SharePoint Framework версии 1.4.1, который упрощает подключение к Microsoft Graph в решениях SharePoint Framework. **MSGraphClient** является оболочкой для всей [клиентской библиотеки JavaScript Microsoft Graph](https://www.npmjs.com/package/@microsoft/microsoft-graph-client), предоставляя разработчикам такие же возможности, как и при использовании клиентской библиотеки в других клиентских решениях. Несмотря на то что вы можете напрямую использовать в решении клиентскую библиотеку JavaScript для Microsoft Graph, при использовании класса **MSGraphClient** проверка подлинности в Microsoft Graph выполняется автоматически, что позволяет сосредоточиться на разработке решения.

## <a name="use-the-msgraphclient-in-your-solution"></a>Использование класса MSGraphClient в решении

> [!NOTE]
> Класс **MSGraphClient** доступен только в проектах, созданных с помощью SharePoint Framework 1.4.1 и более поздних версий. В этой статье демонстрируется использование класса **MSGraphClient** в клиентской веб-части, но его можно с таким же успехом использовать в расширениях SharePoint Framework.

Чтобы использовать объект **MSGraphClient** в решении SharePoint Framework, добавьте выражение `import` в основной файл веб-части.

```ts
import { MSGraphClient } from '@microsoft/sp-client-preview';
```

**MSGraphClient** предоставляется в качестве службы, которую необходимо использовать из соответствующей области, чтобы получить ссылку на нее. Для этого добавьте следующий код:

```ts
export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  public render(): void {
    // ...

    const client: MSGraphClient = this.context.serviceScope.consume(MSGraphClient.serviceKey);
  }

  // ...
}
```

Получив ссылку на экземпляр **MSGraphClient**, вы можете установить связь с Microsoft Graph, используя синтаксис клиентской библиотеки JavaScript:

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

### <a name="use-the-microsoft-graph-typescript-types"></a>Использование типов TypeScript для Microsoft Graph

При работе с Microsoft Graph и TypeScript вы можете использовать типы TypeScript для Microsoft Graph, которые помогут вам быстрее обнаруживать ошибки в коде. Типы TypeScript для Microsoft Graph предоставляются в виде отдельного пакета, который можно установить с помощью следующей команды:

```sh
npm install @microsoft/microsoft-graph-types --save-dev
```

Установив пакет в проекте, импортируйте его в файле веб-части с помощью следующей команды:

```ts
import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
```

Теперь вы можете задавать типы для объектов, полученных из Microsoft Graph, например:

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

Дополнительные сведения о работе с клиентской библиотекой JavaScript для Microsoft Graph см. на странице [https://www.npmjs.com/package/@microsoft/microsoft-graph-client](https://www.npmjs.com/package/@microsoft/microsoft-graph-client)

## <a name="available-permission-scopes"></a>Доступные области разрешений

По умолчанию субъекту-службе не назначены явные разрешения на доступ к Microsoft Graph. Однако, запросив маркер доступа для Microsoft Graph, вы получите маркер с областью разрешений `user_impersonation`, с помощью которой можно считывать сведения о пользователях (т. е. `User.Read.All`). Разработчики могут запрашивать дополнительные области разрешений, а администраторы клиентов — предоставлять их. Дополнительные сведения см. в справочной [статье, посвященной использованию AadHttpClient](./use-aadhttpclient.md).

> [!IMPORTANT]
> Вышеописанное поведение с областью разрешений `user_impersonation` может измениться перед выпуском общедоступной версии этой функции. Не рекомендуем добавлять зависимость от этих стандартных разрешений.

## <a name="see-also"></a>См. также

- [Microsoft Graph](https://graph.microsoft.com)
- [Клиентская библиотека JavaScript для Microsoft Graph](https://www.npmjs.com/package/@microsoft/microsoft-graph-client)
- [Примеры с использованием клиентской библиотеки JavaScript для Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript/tree/master/samples)
- [Типы TypeScript для Microsoft Graph](https://www.npmjs.com/package/@microsoft/microsoft-graph-types)