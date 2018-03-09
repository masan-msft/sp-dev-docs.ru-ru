---
title: "Свойства клиента SharePoint Online"
description: "Управляйте свойствами клиента, которые позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 3ef0906645da5479fcac8e5f2f188063283300ee
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="sharepoint-online-tenant-properties"></a>Свойства клиента SharePoint Online

Свойства клиента позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework. Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской на SharePoint Online в Office 365.

Для управления свойствами клиента также можно использовать [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties). Office 365 CLI — это межплатформенный интерфейс командной строки, который можно использовать на любой платформе, в том числе Windows, MacOS и Linux.

## <a name="manage-tenant-properties"></a>Управление свойствами клиента

С помощью [командной консоли Microsoft SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588) администраторы клиента могут добавлять и удалять свойства клиента через PowerShell. 

Ниже приведены командлеты PowerShell для управления свойствами клиента. Так как свойства клиента хранятся в каталоге приложений клиента, в приведенных ниже командлетах нужно указать URL-адрес семейства веб-сайтов с каталогом приложений клиента.

Прежде чем запускать приведенный ниже скрипт, подключитесь к клиенту SharePoint Online, используя командлет `Connect-SPOService` в SharePoint Online PowerShell.

### <a name="get-spostorageentity"></a>Get-SPOStorageEntity

- **Область применения:** Office 365, SharePoint Online

- **Синтаксис** Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String>

### <a name="set-spostorageentity"></a>Set-SPOStorageEntity

- **Область применения:** Office 365, SharePoint Online

- **Синтаксис** Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String>

### <a name="remove-spostorageentity"></a>Remove-SPOStorageEntity

- **Область применения:** Office 365, SharePoint Online

- **Синтаксис** Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String>

## <a name="office-365-cli-commands-to-get-set-remove-and-list-tenant-properties-cross-platform"></a>Команды Office 365 CLI для получения, задания, удаления и отображения свойств клиента на любой платформе

Используя [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties), администраторы клиента могут управлять свойствами клиента с помощью команд оболочки.

Прежде чем использовать команды, подключитесь к сайту SharePoint Online с помощью команды `spo connect`.

### <a name="get-details-for-the-specified-tenant-property"></a>Получение сведений об указанном свойстве клиента

Команду [spo storageentity get](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-get/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для получения сведений о свойстве клиента Office 365 или SharePoint Online.

```shell
spo storageentity get --key <key>
```

### <a name="list-tenant-properties-stored-on-the-specified-sharepoint-online-app-catalog"></a>Отображение свойств клиента, хранящихся в указанном каталоге приложений SharePoint Online

Команду [spo storageentity list](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-list/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для отображения всех свойств клиента.

```shell
spo storageentity list --appCatalogUrl <appCatalogUrl>
```

### <a name="set-tenant-property-on-a-specified-sharepoint-online-app-catalog"></a>Задание свойства клиента в указанном каталоге приложений SharePoint Online

Команду [spo storageentity set](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-set/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для задания свойства клиента.

```shell
spo storageentity set --appCatalogUrl <appCatalogUrl> --key <key> --value <value>
```

### <a name="remove-tenant-property-stored-on-the-specified-sharepoint-online-app-catalog"></a>Удаление свойства клиента, хранящегося в указанном каталоге приложений SharePoint Online

Команду [spo storageentity remove](https://sharepoint.github.io/office365-cli/cmd/spo/storageentity/storageentity-remove/?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties) можно использовать для удаления свойства клиента.

```shell
spo storageentity remove --appCatalogUrl <appCatalogUrl> --key <key>
```

### <a name="remarks-when-using-the-office-365-cli-set-and-remove-commands"></a>Что нужно учитывать при задании и удалении свойств с помощью команд Office 365 CLI

Чтобы задать или удалить свойство клиента, сначала нужно подключиться к сайту администрирования клиента, используя команду spo connect, например spo connect https://contoso-admin.sharepoint.com. Если вы подключены к другому сайту, вы не сможете управлять свойствами клиента.

Свойства клиента хранятся на сайте каталога приложений, связанном с этим клиентом. Чтобы задать или удалить свойство, необходимо указать абсолютный URL-адрес сайта каталога приложений. Если вы укажете URL-адрес сайта, отличный от каталога приложений, вам будет отказано в доступе.

## <a name="read-tenant-properties"></a>Считывание свойств клиента

Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.

## <a name="http-request"></a>HTTP-запрос

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

## <a name="see-also"></a>См. также

- [Обзор SharePoint Framework](sharepoint-framework-overview.md)
- [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Use+SharePoint+Online+tenant+properties)