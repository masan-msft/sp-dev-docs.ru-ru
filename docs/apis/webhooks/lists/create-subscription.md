# <a name="create-a-new-subscription"></a>Создание подписки 

Создает подписку на веб-перехватчики в списке SharePoint. 

## <a name="permissions"></a>Разрешения

У приложения должно быть разрешение на изменение списка SharePoint, в котором создается подписка.

**Если приложение является приложением Microsoft Azure Active Directory (AD):**

Приложению Azure AD необходимо предоставить разрешения, указанные в следующей таблице:

Приложение | Разрешение 
------------|------------
SharePoint Online в Office 365|Чтение и запись элементов и списков во всех семействах веб-сайтов.

**Если приложение является надстройкой SharePoint:**

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
client-clientState|string|Необязательный. Непрозрачная строка, которая передаются клиенту со всеми уведомлениями. Ее можно использовать для проверки уведомлений и маркировки различных подписок.


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

Когда вы добавляете подписку, возвращается ответ `201 Created`, который включает новый объект подписки.

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

Перед созданием подписки SharePoint отправит запрос с токеном проверки на указанный URL-адрес службы. Служба должна ответить на него, вернув токен проверки.

В противном случае подписка не будет создана. Подробнее: [Обзор веб-перехватчиков SharePoint](../overview-sharepoint-webhooks).
