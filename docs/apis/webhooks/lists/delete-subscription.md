---
title: "Удаление подписки"
description: "Удаляет подписку на веб-перехватчики из списка SharePoint. После удаления подписки доставка уведомлений прекращается."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 69ddbfcc4274b307bd262d72922a7651de5a2745
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="delete-a-subscription"></a>Удаление подписки

Удаляет подписку на веб-перехватчики из списка SharePoint. После удаления подписки доставка уведомлений прекращается.

## <a name="permissions"></a>Разрешения

У приложения должно быть разрешение по крайней мере на изменение списка SharePoint, из которого удаляется подписка.

### <a name="if-your-application-is-a-microsoft-azure-active-directory-azure-ad-application"></a>Если приложение является приложением Microsoft Azure Active Directory (AD)

Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно удалить только из приложения Azure AD, в котором она создана.

Приложение | Разрешение 
------------|------------
SharePoint Online в Office 365|Чтение и запись элементов и списков во всех семействах веб-сайтов.

### <a name="if-your-application-is-a-sharepoint-add-in"></a>Если приложение является надстройкой SharePoint

Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно удалить только из надстройки SharePoint, в которой она создана.

Область | Разрешения 
------|------------
Список|Управление

## <a name="http-request"></a>HTTP-запрос

```
DELETE _api/web/lists('list-id')/subscriptions('id')
```

### <a name="example"></a>Пример

```http
DELETE _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

## <a name="request-body"></a>Текст запроса

Не указывайте тело запроса для этого метода.

## <a name="response"></a>Ответ

Если подписка найдена и удалена, возвращается ответ `204 No Content`.

### <a name="example"></a>Пример

```http
HTTP/1.1 204 No Content
```

## <a name="see-also"></a>См. также

- [Веб-перехватчики для списков SharePoint](overview-sharepoint-list-webhooks.md)
- [Обзор веб-перехватчиков SharePoint](../overview-sharepoint-webhooks.md)