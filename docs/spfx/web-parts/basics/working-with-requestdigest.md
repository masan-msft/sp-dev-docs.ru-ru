---
title: "Работа с __REQUESTDIGEST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ae30e9d655ebaf9d99d6e72017a2ed62e2fb3aac
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-requestdigest"></a>Работа с __REQUESTDIGEST

При выполнении запросов REST к API SharePoint (всех, кроме GET) в них необходимо добавлять действительный дайджест. Он подтверждает действительность вашего запроса к SharePoint. Так как срок действия этого токена ограничен, его необходимо проверить, прежде чем добавлять в запрос, иначе возникнет ошибка. В этой статье описано, как получить действительный дайджест запроса и избежать ошибок.

## <a name="considerations-when-using-request-digest-from-the-hidden-requestdigest-field"></a>Что следует учитывать при использовании дайджеста запроса из скрытого поля __REQUESTDIGEST

На классических страницах SharePoint включает токен дайджеста запроса в скрытом поле **__REQUESTDIGEST**. Один из наиболее распространенных способов работы с дайджестом запроса — извлечение его из этого поля и добавление в запрос, например:

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

Первоначально такой запрос будет работать, но если страница будет открыта в течение долгого времени, срок действия дайджеста запроса истечет и возникнет ошибка **403 FORBIDDEN**. По умолчанию токен дайджеста запроса действителен в течение 30 минут, поэтому перед использованием его необходимо проверить. Раньше для этого нужно было сравнить метку времени из дайджеста запроса с текущим временем. SharePoint Framework упрощает этот процесс. Проверить токен дайджеста запроса можно двумя способами.

## <a name="use-the-sphttpclient-to-communicate-with-the-sharepoint-rest-api"></a>Использование SPHttpClient для связи с REST API SharePoint

Для связи с REST API SharePoint рекомендуется использовать SPHttpClient, предоставляемый вместе с SharePoint Framework. Этот класс содержит удобную логику для отправки запросов REST к API SharePoint, которая упрощает код. Например, когда вы отправляете запрос, отличный от GET, используя SPHttpClient, он автоматически получает действительный дайджест запроса и добавляет его в запрос. Это значительно упрощает решение, так как не нужно создавать код для управления токенами дайджеста запросов и их проверки.

При создании новых настроек в SharePoint Framework для связи с REST API SharePoint всегда следует использовать SPHttpClient. Однако, иногда это невозможно, например, когда вы переносите существующую настройку в SharePoint Framework и хотите сохранить как можно больше исходного кода или создаете настройку, используя библиотеку, такую как Angular(JS), с собственными службами для отправки веб-запросов. В таких случаях действительный токен дайджеста запроса можно получить из службы **DigestCache**.

## <a name="retrieve-valid-request-digest-using-the-digestcache-service"></a>Извлечение действительного дайджеста запроса с помощью службы DigestCache

Если использовать SPHttpClient для связи с REST API SharePoint невозможно, действительный токен дайджеста запроса можно получить, используя службу **DigestCache**, предоставляемую вместе с SharePoint Framework. Использовать службу DigestCache удобнее, чем получать действительный токен дайджеста запроса вручную, так как DigestCache автоматически проверяет полученный ранее дайджест запроса. Если срок его действия истек, служба DigestCache автоматически запрашивает новый токен дайджеста запроса в SharePoint и сохраняет его для последующих запросов. Использование DigestCache упрощает код и делает решение более надежным.

Чтобы использовать службу DigestCache в коде, сначала импортируйте типы **DigestCache** и **IDigestCache** из пакета **@microsoft/sp-http**:

```ts
// ...
import { IDigestCache, DigestCache } from '@microsoft/sp-http';

export default class HelloWorldWebPart extends BaseClientSideWebPart<IHelloWorldWebPartProps> {
  // ...
}
```

После этого, когда вам понадобится действительный токен дайджеста запроса, получите ссылку на службу DigestCache и вызовите ее метод **fetchDigest**:

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