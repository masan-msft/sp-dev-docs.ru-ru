---
title: "Работа с __REQUESTDIGEST"
description: "Добавляйте действительный дайджест к каждому запросу API SharePoint, отличному от GET REST."
ms.date: 01/09/2018
ms.prod: sharepoint
ms.openlocfilehash: 8a357c2a199566dbbf24f209c18b5f4673bd8b1a
ms.sourcegitcommit: 2188f21ce207c9d62d7d8af93822bd101058ba2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="work-with-requestdigest"></a>Работа с __REQUESTDIGEST

К каждому запросу API SharePoint, отличному от GET REST, необходимо добавлять действительный дайджест. Этот дайджест доказывает, что запрос к SharePoint является действительным. Так как срок действия этого токена ограничен, необходимо убедиться, что токен действителен, прежде чем добавлять его к запросу. В противном случае запрос будет отклонен. 

На классических страницах SharePoint дайджест-токен запроса включается в скрытое поле с именем **__REQUESTDIGEST**. Часто дайджест извлекают из этого поля и добавляют к запросу, например:

```js
var digest = $('#__REQUESTDIGEST').val();
$.ajax({
    url: '/_api/web/...'
    method: "POST",
    headers: {
        "Accept": "application/json; odata=nometadata",
        "X-RequestDigest": digest
    },
    success: function (data) {
      // ...
    },
    error: function (data, errorCode, errorMessage) {
      // ...
    }
});
```

Поначалу такой запрос будет работать, но если страница будет открыта долго, срок действия дайджеста запроса на странице истечет и возникнет ошибка **403 FORBIDDEN**. По умолчанию срок действия дайджест-токена запроса составляет 30 минут, поэтому перед его использованием необходимо убедиться, что он еще действителен. В прошлом это требовалось делать вручную, сравнивая метку времени из дайджеста запроса с текущим временем. 

SharePoint Framework упрощает этот процесс, позволяя проверить, действителен ли дайджест-токен запроса одним из двух способов.

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a>Использование класса SPHttpClient для связи с REST API SharePoint

Рекомендуемый способ связи с REST API SharePoint — использование класса SPHttpClient, входящего в состав SharePoint Framework. Этот класс представляет собой оболочку для отправки запросов REST к REST API SharePoint с удобной логикой, упрощающей код. 

Например, при отправке отличного от GET запроса с помощью SPHttpClient автоматически возвращается действительный дайджест, который добавляется к запросу. Это значительно упрощает решение, так как вам не требуется писать код для управления дайджест-токенами запросов и проверять, являются ли они действительными.

При создании новых настроек на платформе SharePoint Framework следует всегда использовать класс SPHttpClient для работы с REST API SharePoint. 

Но иногда может не быть возможности использовать SPHttpClient. Например, такая проблема может возникать при переносе имеющейся настройки на платформу SharePoint Framework, если требуется сохранить как можно больше первоначального кода, или при создании настроек с помощью таких библиотек, как Angular(JS), где предусмотрены собственные службы для отправки веб-запросов. В таких случаях действительный дайджест-токен запроса можно получить из службы **DigestCache**.

## <a name="retrieve-a-valid-request-digest-by-using-the-digestcache-service"></a>Получение действительного дайджеста запроса из службы DigestCache

Если у вас нет возможности использовать класс SPHttpClient для работы с REST API SharePoint, то вы можете получить действительный дайджест-токен запроса из службы **DigestCache**, входящей в состав SharePoint Framework. 

Преимущество использования службы DigestCache по сравнению с получением действительного дайджест-токена запроса вручную заключается в том, что DigestCache автоматически проверяет, действителен ли ранее полученный дайджест запроса. Если срок его действия истек, служба DigestCache автоматически запрашивает новый дайджест-токен из SharePoint и сохраняет его для последующих запросов. Использование DigestCache упрощает код и делает решение более надежным.

### <a name="to-use-the-digestcache-service-in-your-code"></a>Использование службы DigestCache в коде

1. Импортируйте типы **DigestCache** и **IDigestCache** из пакета **@microsoft/sp-http**:

  ```ts
  // ...
  import { IDigestCache, DigestCache } from '@microsoft/sp-http';

  export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
    // ...
  }
  ```

2. Когда вам понадобится действительный дайджест-токен запроса, получите ссылку на службу DigestCache и вызовите ее метод **fetchDigest**:

  ```ts
  // ...
  import { IDigestCache, DigestCache } from '@microsoft/sp-http';

  export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
    protected onInit(): Promise<void> {
      return new Promise<void>((resolve: () => void, reject: (error: any) => void): void => {
        const digestCache: IDigestCache = this.context.serviceScope.consume(DigestCache.serviceKey);
        digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string): void => {
          // use the digest here
          resolve();
        });
      });
    }

    // ...
  }
  ```