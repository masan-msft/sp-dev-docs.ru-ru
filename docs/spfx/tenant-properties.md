# <a name="sharepoint-online-tenant-properties"></a>Свойства клиента SharePoint Online

Свойства клиента позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework. Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской SharePoint Online в Office 365.

## <a name="manage-tenant-properties"></a>Управление свойствами клиента

С помощью командной консоли Microsoft SharePoint Online администраторы клиента могут добавлять и удалять свойства клиента через PowerShell. 

> Скачайте командную консоль Microsoft SharePoint Online [отсюда](https://www.microsoft.com/en-us/download/details.aspx?id=35588)

Эти командлеты PowerShell доступны для управления свойствами клиента:

Так как свойства клиента хранятся в каталоге приложений клиента, в командлетах ниже нужно будет указать URL-адрес семейства веб-сайтов каталога приложений клиента.

### <a name="get-spostorageentity"></a>Get-SPOStorageEntity
Область применения: Office 365, SharePoint Online

Синтаксис Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String>

### <a name="set-spostorageentity"></a>Set-SPOStorageEntity
Область применения: Office 365, SharePoint Online

Синтаксис Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String>

### <a name="remove-spostorageentity"></a>Remove-SPOStorageEntity
Область применения: Office 365, SharePoint Online

Синтаксис Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String>

## <a name="reading-tenant-properties"></a>Считывание свойств клиента

Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.

## <a name="http-request"></a>Запрос HTTP

### <a name="get-a-tenant-property"></a>Получение свойства клиента

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a>Пример

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a>Текст запроса

Не указывайте тело запроса для этого метода.

#### <a name="response"></a>Отклик

Возвращает сведения об объекте хранилища для указанного ключа.

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```
