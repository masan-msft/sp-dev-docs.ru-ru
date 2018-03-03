---
title: "Обновление подписки"
description: "Обновляет подписку на веб-перехватчики для списка SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: fe8a0960f597d50d77b22a29f14f21afec20c422
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="update-a-subscription"></a>Обновление подписки

Обновляет подписку на веб-перехватчики для списка SharePoint.

## <a name="permissions"></a>Разрешения

Приложение должно иметь по крайней мере разрешение на изменение списка SharePoint, в котором обновляется подписка.  

### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a>Если приложение является приложением Microsoft Azure Active Directory (AD)

Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно обновить только из приложения Azure AD, в котором она создана.

Приложение | Разрешение 
------------|------------
SharePoint Online в Office 365|Чтение и запись элементов и списков во всех семействах веб-сайтов. 

### <a name="if-your-application-is-a-sharepoint-add-in"></a>Если приложение является надстройкой SharePoint

Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно обновить только из надстройки SharePoint, в которой она создана.

Область | Разрешения 
------|------------
Список|Управление

## <a name="http-request"></a>HTTP-запрос

```
PATCH _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a>Пример

```http
PATCH _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
Content-Type: application/json

{
  "notificationUrl": "https://contoso.azurewebsites.net/api/v2/webhook-receiver",
  "expirationDateTime": "2016-01-03T11:23:00.000Z"
}
```

## <a name="request-body"></a>Тело запроса

Включите в запрос указанные ниже свойства.

Имя | Тип | Описание 
-----|------|------------
notificationUrl|строка|URL-адрес службы для отправки уведомлений.
expirationDateTime|дата|Срок хранения уведомления.
client-clientState|строка|Необязательный. Непрозрачная строка, которая передается клиенту со всеми уведомлениями.<br/>Ее можно использовать для проверки уведомлений или маркировки различных подписок.


## <a name="response"></a>Ответ

Если подписка найдена и успешно обновлена, возвращается ответ `204 No Content`.

### <a name="example"></a>Пример

```http
HTTP/1.1 204 No Content
```

## <a name="see-also"></a>См. также

- [Веб-перехватчики для списков SharePoint](overview-sharepoint-list-webhooks.md)
- [Обзор веб-перехватчиков SharePoint](../overview-sharepoint-webhooks.md)