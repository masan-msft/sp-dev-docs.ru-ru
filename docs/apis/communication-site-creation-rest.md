# <a name="creating-sharepoint-communication-site-using-rest"></a>Создание сайта SharePoint для общения с помощью REST

Узнайте, как создать современный сайт SharePoint для общения и получить его состояние с помощью интерфейса REST.

## <a name="prerequisites"></a>Предварительные требования

В этой статье предполагается, что вы уже ознакомились со статьями "Знакомство со службой REST для SharePoint" и "Выполнение базовых операций с использованием конечных точек REST в SharePoint". Здесь не представлены фрагменты кода.

Ниже перечислены команды REST, доступные при создании современного сайта SharePoint для общения.

- **Create** — создание сайта SharePoint для общения.
- **Status** — получение состояния сайта SharePoint для общения.

URL-адрес для команд службы REST на сайте для общения основан на конечной точке `_api/sitepages/communicationsite`. Например, для вышеуказанных команд используются следующие конечные точки:

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
> Параметр lcid в данный момент не поддерживается для этого API. В настоящее время можно создавать только сайты на английском языке. 

В этом API появилось понятие SiteDesignID. Как и поток создания сайтов в продукте, параметр SiteDesignID сопоставляется с включенными вариантами оформления сайтов. Они указаны ниже.

- Тема: null
- Демонстрация: 6142d2a0-63a5-4ba0-aede-d9fefca2c767
- Пустой: f6cc5403-0d63-442e-96c0-285923709ffc

**Отклик**

В случае успешного выполнения этот метод возвращает код отклика 200 OK и простой объект JSON в тексте отклика с указанными ниже сведениями.

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

REST API для получения состояния современного сайта SharePoint для общения

```
url: /_api/sitepages/communicationsite/status?url='https%3A%2F%2Fcontoso.sharepoint.com%2Fsites%2Fcomm1'
method: GET
body: none
```

**Отклик**

В случае успешного выполнения этот метод возвращает код отклика 200 OK и простой объект JSON в тексте отклика с указанными ниже сведениями.
 
Если сайт существует, отклик содержит состояние и URL-адрес сайта.

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

Если сайт не существует, отклик содержит состояние сайта 0 без URL-адреса.

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