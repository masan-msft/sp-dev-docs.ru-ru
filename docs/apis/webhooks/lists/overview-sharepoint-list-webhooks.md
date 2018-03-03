---
title: "Веб-перехватчики для списков SharePoint"
description: "Веб-перехватчики списков обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 085ff54834ea0c9e1e40c25001586b35970d69cf
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="sharepoint-list-webhooks"></a>Веб-перехватчики для списков SharePoint

Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.

## <a name="tasks"></a>Задачи

| Задача                                                | Метод HTTP                                            |     
|-----------------------------------------------------|--------------------------------------------------------|
| [Создание подписки](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions` |
| [Получение подписок](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`   |
| [Удаление подписки](./delete-subscription.md)   | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`|
| [Обновление подписки](./update-subscription.md)   | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`|

## <a name="list-event-types"></a>Типы событий в списках
Приложению будут отправляться уведомления о следующих асинхронных событиях в элементах списков в SharePoint:

* ItemAdded
* ItemUpdated
* ItemDeleted
* ItemCheckedOut
* ItemCheckedIn
* ItemUncheckedOut
* ItemAttachmentAdded
* ItemAttachmentDeleted
* ItemFileMoved
* ItemVersionDeleted
* ItemFileConverted

Веб-перехватчики не поддерживают синхронные события.

## <a name="see-also"></a>См. также

* [Обзор веб-перехватчиков SharePoint](../overview-sharepoint-webhooks.md)
