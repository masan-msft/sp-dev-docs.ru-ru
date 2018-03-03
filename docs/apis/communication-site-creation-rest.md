---
title: "Создание сайта SharePoint для общения с помощью REST"
description: "Создайте современный сайт SharePoint для общения и получите его состояние, используя интерфейс REST."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: c691bdf6a6dcdc3402eabb9b9ce198d630b23704
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="create-sharepoint-communication-site-using-rest"></a>Создание сайта SharePoint для общения с помощью REST

В этой статье предполагается, что вы уже ознакомились со следующими статьями:

- [Знакомство со службой REST в SharePoint](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)
- [Выполнение базовых операций с использованием конечных точек REST SharePoint](../sp-add-ins/complete-basic-operations-using-sharepoint-rest-endpoints.md)

В этой статье нет фрагментов кода.

Ниже перечислены команды REST для создания современного сайта SharePoint для общения.

- **Create**. Создание сайта SharePoint для общения.
- **Status**. Получение состояния сайта SharePoint для общения.

URL-адрес для команд службы REST на сайте для общения основан на конечной точке `_api/sitepages/communicationsite`. Например, для указанных выше команд REST используются следующие конечные точки:

- `http:///_api/sitepages/communicationsite/create`
- `http:///_api/sitepages/communicationsite/status`

## <a name="create-communication-site"></a>Создание сайта для общения

```
url: /_api/sitepages/communicationsite/create
method: POST
body:
{
   "request":{
      "__metadata":{
         "type":"SP.Publishing.CommunicationSiteCreationRequest"
      },
      "AllowFileSharingForGuestUsers":false,
      "Classification":"LBI",
      "Description":"Description",
      "SiteDesignId":"6142d2a0-63a5-4ba0-aede-d9fefca2c767",
      "Title":"Comm Site 1",
      "Url":"https://vesku.sharepoint.com/sites/commsite132",
      "lcid":1033
   }
}
```

> [!IMPORTANT]
> Параметр `lcid` в данный момент не поддерживается для этого API. В настоящее время можно создавать сайты только на английском языке. 

В этом API появилось понятие `SiteDesignID`. Как и поток создания сайтов в продукте, параметр `SiteDesignID` сопоставляется с включенными вариантами оформления сайтов. Они указаны ниже.

- Тема: null
- Демонстрация: 6142d2a0-63a5-4ba0-aede-d9fefca2c767
- Пустой: f6cc5403-0d63-442e-96c0-285923709ffc

### <a name="response"></a>Ответ

В случае успешного выполнения этот метод возвращает код ответа `200, OK` и простой объект JSON в тексте ответа с указанными ниже сведениями.

```
{
  "d":{
      "Create":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":2,
          "SiteUrl":"https://contoso.sharepoint.com/sites/comm1"
      }
  }
}
```


## <a name="get-communication-site-status"></a>Получение состояния сайта для общения

REST API для получения состояния современного сайта SharePoint для общения:

```
url: /_api/sitepages/communicationsite/status?url='https%3A%2F%2Fcontoso.sharepoint.com%2Fsites%2Fcomm1'
method: GET
body: none
```

### <a name="response"></a>Ответ

В случае успешного выполнения этот метод возвращает код ответа `200, OK` и простой объект JSON в тексте ответа с указанными ниже сведениями.
 
Если сайт существует, ответ содержит состояние и URL-адрес сайта.

```
{
  "d":{
      "Status":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":2,
          "SiteUrl":"https://contoso.sharepoint.com/sites/comm1"
      }
  }
}
```

Если сайт не существует, ответ содержит состояние сайта 0 без URL-адреса.

```
{
  "d":{
      "Status":{
           "__metadata":{"type":"SP.Publishing.CommunicationSiteCreationResponse"},
          "SiteStatus":0,
          "SiteUrl":
      }
  }
}
```

## <a name="see-also"></a>См. также

- [Знакомство со службой REST в SharePoint](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)