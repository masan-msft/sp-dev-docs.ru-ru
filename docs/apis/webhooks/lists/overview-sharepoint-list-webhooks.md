---
title: "Веб-перехватчики для списков SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2b3543885de7fcce75694d368667f17dd690592f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-list-webhooks"></a>Веб-перехватчики для списков SharePoint

Веб-перехватчики списков SharePoint обрабатывают события, связанные с изменением элементов в списках или библиотеках документов SharePoint. Веб-перехватчики SharePoint предоставляют простой канал уведомлений, чтобы приложение узнавало об изменениях списка SharePoint, не выполняя опрос службы.

## <a name="tasks"></a>Задачи
| Задача                                                | Метод HTTP                                                  |
|-----------------------------------------------------|--------------------------------------------------------------|
| [Создание подписки](./create-subscription.md) | `POST    /_api/web/lists('list-guid')/subscriptions`         |
| [Получение подписок](./get-subscription.md)          | `GET     /_api/web/lists('list-guid')/subscriptions`         |
| [Удаление подписки](./delete-subscription.md)       | `DELETE  /_api/web/lists('list-guid')/subscriptions('id')`   |
| [Обновление подписки](./update-subscription.md)     | `PATCH   /_api/web/lists('list-guid')/subscriptions('id')`   |

## <a name="list-event-types"></a>Типы событий списков
Приложению будут отправляться уведомления о следующих асинхронных событиях с элементами списков в SharePoint:

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
