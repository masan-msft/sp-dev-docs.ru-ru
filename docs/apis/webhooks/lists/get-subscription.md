# <a name="get-subscriptions"></a>Получение подписок

Возвращает одну или несколько подписок на веб-перехватчики в списке SharePoint.

## <a name="permissions"></a>Разрешения

### <a name="get-a-single-subscription"></a>Получение одной подписки

У приложения должно быть разрешение на изменение списка SharePoint, из которого извлекается подписка.

**Для приложения Microsoft Azure Active Directory (AD):**

Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. Подписку можно получить только из создавшего ее приложения Azure AD. 

Приложение | Разрешение 
------------|------------
SharePoint Online в Office 365|Чтение и запись элементов и списков во всех семействах веб-сайтов.

**Для надстройки SharePoint**:

Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. Подписку можно получить только из создавшей ее надстройки SharePoint. 

Область | Разрешения 
------|------------
Список|Управление

### <a name="get-all-subscriptions"></a>Получение всех подписок

У приложения должны быть разрешения на управление списком SharePoint, из которого извлекается подписка.

**Для приложения Microsoft Azure Active Directory (AD):**

Приложению Azure AD необходимо предоставить разрешения, указанные в таблице ниже. 

Приложение | Разрешение 
------------|------------
SharePoint Online в Office 365|Полный доступ ко всем семействам веб-сайтов.

**Для надстройки SharePoint**:

Надстройке SharePoint необходимо предоставить по крайней мере указанные ниже разрешения. 

Область | Разрешения 
------|------------
Список|Полный доступ

## <a name="http-request"></a>HTTP-запрос

### <a name="get-a-single-subscription"></a>Получение одной подписки

#### <a name="list-webhook"></a>Веб-перехватчик списка
```
GET _api/web/lists('list-id')/subscriptions('id')
```

##### <a name="example"></a>Пример

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('6D77031A-2345-5GRT-BV3D-55234B56FR43')
```

#### <a name="request-body"></a>Текст запроса

Не указывайте тело запроса для этого метода.

##### <a name="response"></a>Отклик

Возвращает подписку, которую можно просмотреть в приложении, отправившем вызов.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://contoso.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions/@Element",
  "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
  "odata.id": "https://contoso.sharepoint.com/_api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "odata.editLink": "web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions('a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7')",
  "expirationDateTime": "2016-04-30T16:17:57Z",
  "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
  "notificationUrl": "https://contoso.azurewebistes.net/api/webhook/handlerequest",
  "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
}
```

### <a name="get-all-subscriptions"></a>Получение всех подписок

#### <a name="list-webhook"></a>Веб-перехватчик списка
```
GET _api/web/lists('list-id')/subscriptions
```

##### <a name="example"></a>Пример

```http
GET _api/web/lists('5C77031A-9621-4DFC-BB5D-57803A94E91D')/subscriptions
```

#### <a name="request-body"></a>Текст запроса

Не указывайте тело запроса для этого метода.

##### <a name="response"></a>Отклик

Возвращает коллекцию всех подписок в ресурсе SharePoint. 

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "odata.metadata": "https://a830edad9050849295j16032914.sharepoint.com/_api/$metadata#SP.ApiData.Subscriptions",
  "value": [
    {
      "odata.type": "Microsoft.SharePoint.Webhooks.Subscription",
      "odata.id": "https://contoso.sharepoint.com/_api/Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "odata.editLink": "Microsoft.SharePoint.Webhooks.Subscriptionc3175b9c-1491-454f-b5da-980431e36146",
      "clientState": "{A0A354EC-97D4-4D83-9DDB-144077ADB449}",
      "expirationDateTime": "2016-04-30T16:17:57Z",
      "id": "a8e6d5e6-9f7f-497a-b97f-8ffe8f559dc7",
      "notificationUrl": "https://contoso.azurewebsites.net/api/webhook/handlerequest",
      "resource": "5c77031a-9621-4dfc-bb5d-57803a94e91d"
    }
  ]
}
```
