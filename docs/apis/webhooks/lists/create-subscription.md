---
title: "Создание подписки"
description: "Создает подписку на веб-перехватчики в списке SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 8a93bdd5c7891ac275e18c1c9f50620c44b760af
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="create-a-new-subscription"></a>Создание подписки 

Создает подписку на веб-перехватчики в списке SharePoint. 

## <a name="permissions"></a>Разрешения

У приложения должно быть разрешение на изменение списка SharePoint, в котором создается подписка.

### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a>Если приложение является приложением Microsoft Azure Active Directory (AD)

Приложению Azure AD необходимо предоставить разрешения, указанные в следующей таблице:

Приложение | Разрешение 
------------|------------
SharePoint Online в Office 365|Чтение и запись элементов и списков во всех семействах веб-сайтов.

### <a name="if-your-application-is-a-sharepoint-add-in"></a>Если приложение является надстройкой SharePoint

Надстройке SharePoint необходимо предоставить по крайней мере следующие разрешения:

Область | Разрешения 
------|------------
Список|Управление

## <a name="http-request"></a>HTTP-запрос

```
POST /_api/web/lists('list-id')/subscriptions
```

## <a name="request-body"></a>Текст запроса

Включите в запрос указанные ниже свойства.

Имя | Тип | Описание 
-----|------|------------
resource|строка|URL-адрес списка для получения уведомлений.
notificationUrl|строка|URL-адрес службы для отправки уведомлений.
expirationDateTime|дата|Срок хранения уведомления.
client-clientState|строка|Необязательный. Непрозрачная строка, которая передается клиенту со всеми уведомлениями.<br/>Ее можно использовать для проверки уведомлений или маркировки различных подписок.


### <a name="example"></a>Пример

```http
POST /_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
Accept: application/json
Content-Type: application/json

{
  "resource": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')",
  "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
  "expirationDateTime": "2016-04-27T16:17:57+00:00"
}
```

## <a name="response"></a>Ответ

Если подписка добавлена, возвращается ответ `201 Created`, который содержит новый объект подписки.

### <a name="example"></a>Пример

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
    "expirationDateTime": "2016-04-27T16:17:57Z",    
    "notificationUrl": "https://91e383a5.ngrok.io/api/webhook/handlerequest",
    "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

## <a name="url-validation"></a>Проверка URL-адреса

Перед созданием подписки SharePoint отправляет запрос с токеном проверки на указанный URL-адрес службы. Служба должна ответить на него, вернув токен проверки.

В противном случае подписка не создается.

## <a name="see-also"></a>См. также

- [Веб-перехватчики для списков SharePoint](overview-sharepoint-list-webhooks.md)
- [Обзор веб-перехватчиков SharePoint](../overview-sharepoint-webhooks.md)