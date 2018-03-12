---
title: "API управления жизненным циклом приложений (ALM)"
description: "API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: 3e3b9aa836bf6242bf2fe2ef4f1b3fdc5d2bcb62
ms.sourcegitcommit: 860b40b91f01c5b781517e3cd4057b971ce90b6e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2018
---
# <a name="application-lifecycle-management-alm-apis"></a>API управления жизненным циклом приложений (ALM)

API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте. Эти API поддерживают указанные ниже возможности.

- Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.
- Удаление решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента.
- Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.
- Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.
- Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.
- Обновление решения SharePoint Framework или надстройки SharePoint на сайте до более поздней версии, доступной в каталоге приложений клиента.
- Удаление решения SharePoint Framework или надстройки SharePoint с сайта.
- Перечисление и получение всех сведений о решениях SharePoint Framework или надстройках SharePoint в каталоге приложений клиента.

С помощью API ALM можно выполнять те же операции, что и в пользовательском интерфейсе. При использовании этих API выполняются все типичные действия. Ниже описаны некоторые характеристики API ALM.

- События `Install` и `UnInstall` вызываются для надстроек с размещением у поставщика при выполнении соответствующих операций.
- API ALM поддерживают операции только для приложений.

API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM, командлеты PowerShell и межплатформенный интерфейс командной строки Office 365, доступные благодаря SharePoint PnP.

> [!NOTE] 
> API управления жизненным циклом приложений для [каталога приложений семейства сайтов](../general-development/site-collection-app-catalog.md) в настоящее время не поддерживаются. Поддержка будет добавлена в начале 2018 г.

## <a name="rest-api"></a>REST API

### <a name="add-solution-package-to-the-tenant-app-catalog"></a>Добавление пакета решений в каталог приложений клиента

Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-packages-in-the-tenant-app-catalog"></a>Развертывание пакетов решений в каталоге приложений клиента

Это позволяет устанавливать решение на определенных сайтах. Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
Content-Type: 'application/json;odata=nometadata;charset=utf-8'
```

> [!NOTE]
> Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты. 

### <a name="retract-solution-packages-in-the-tenant-app-catalog"></a>Отзыв пакетов решений в каталоге приложений клиента

При этом решение становится недоступно на сайтах. Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```

> [!NOTE]
> Если выполнить эту операцию после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.

### <a name="remove-solution-packages-from-the-tenant-app-catalog"></a>Удаление пакетов решений из каталога приложений клиента

Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove
method: POST
Authorization: Bearer <access token>
Accept: 'application/json;odata=nometadata'
```

> [!NOTE]
> Если не отозвать решение перед его удалением, то решение будет отозвано автоматически.

### <a name="list-available-packages-from-the-tenant-app-catalog"></a>Перечисление доступных пакетов из каталога приложений клиента

С помощью этого REST API можно получить список доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
Authorization: Bearer <access token>
Accept: 'application/json;odata=nometadata'
```

### <a name="get-details-about-individual-solution-packages-in-the-tenant-app-catalog"></a>Получение сведений об отдельных пакетах решений в каталоге приложений клиента

С помощью этого REST API можно получать сведения об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
Authorization: Bearer <access token>
Accept: 'application/json;odata=nometadata'
```

### <a name="install-solution-package-from-the-tenant-app-catalog-to-a-sharepoint-site"></a>Установка пакета решения из каталога приложений клиента на сайте SharePoint

Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте на основе контекста URL-адреса. Этот вызов REST может выполняться в контексте сайта, на котором запланирована установка.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```

### <a name="upgrade-solution-packages-on-the-sharepoint-site"></a>Обновление пакета решения на сайте SharePoint

Обновите пакет решения на сайте до более новой версии, доступной в каталоге приложений клиента. Этот вызов REST может выполняться в контексте сайта, на котором запланировано обновление.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```

### <a name="uninstall-solution-packages-from-the-sharepoint-site"></a>Удаление пакетов решений с сайта SharePoint

Этот вызов REST может выполняться в контексте сайта, на котором запланировано удаление.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall
method: POST
Authorization: Bearer <access token>
X-RequestDigest: <form digest>
Accept: 'application/json;odata=nometadata'
```
> [!NOTE]
> При удалении пакета решения с сайта с помощью REST API он не перемещается в корзину.


## <a name="sharepoint-pnp-powershell-cmdlets"></a>Командлеты PowerShell в SharePoint PnP 

При помощи [PnP PowerShell](https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений. 

### <a name="add-and-publish-your-app-to-the-app-catalog"></a>Добавление и публикация приложения в каталоге приложений
Добавление приложения (SPPKG, APP) в каталог приложений клиента является обязательным условием для использования этого приложения на сайтах SharePoint. Для этого можно использовать следующий командлет:

```PowerShell
Add-PnPApp -Path ./myapp.sppkg
```

Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента. Ниже на примере командлета PnP PowerShell показано, как это можно сделать.

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> Используйте флаг `SkipFeatureDeployment`, чтобы приложение, разработанное для развертывания на уровне клиента, было доступно в этом качестве.



### <a name="remove-the-app-from-the-app-catalog"></a>Удаление приложения из каталога приложений

Чтобы удалить добавленное ранее приложение, используйте следующий командлет:

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="use-apps-on-your-site"></a>Использование приложений на сайте

Добавив приложение в каталог и опубликовав его, вы можете установить приложение на своем сайте:

```PowerShell
Install-PnPApp -Identity <app id>
```


Обновление приложения:

```PowerShell
Update-PnPApp -Identity <app id>
```

Удаление приложения с сайта:

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> При удалении приложения с сайта оно удаляется полностью, не попадая в корзину сайта.



### <a name="know-which-apps-are-there-for-you-to-use"></a>Сведения о доступных приложениях

Вы можете получить список приложений, доступных для добавления на сайт, используя следующий командлет:

```PowerShell
Get-PnPApp
```

## <a name="office-365-cli-commands-to-add-deploy-and-manage-sharepoint-apps-cross-platform"></a>Команды Office 365 CLI для добавления и развертывания приложений SharePoint на нескольких платформах, а также управления ими

При помощи [Office 365 CLI](https://sharepoint.github.io/office365-cli?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений. Office 365 CLI — это межплатформенный интерфейс командной строки, который можно использовать на любой платформе, в том числе Windows, MacOS и Linux. С дополнительными сведениями об этих командах можно ознакомиться в указанных ниже разделах.

### <a name="add-and-publish-your-app-to-the-app-catalog"></a>Добавление и публикация приложения в каталоге приложений
Добавление приложения (SPPKG, APP) в каталог приложений клиента является обязательным условием для использования этого приложения на сайтах SharePoint. Для этого используйте команду [add](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-add/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):

```shell
spo app add --filePath ./spfx.sppkg
```

Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента. Опубликовать приложение можно с помощью команды [deploy](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-deploy/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):

```shell
spo app deploy --id <app id> --skipFeatureDeployment
```


> [!NOTE]
> Используйте флажок **SkipFeatureDeployment**, чтобы приложение, разработанное для развертывания на уровне клиента, было фактически доступно в этом качестве.



### <a name="remove-the-app-from-the-app-catalog"></a>Удаление приложения из каталога приложений
Вам может потребоваться удалить добавленное ранее приложение. Это можно сделать с помощью команды [remove](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-remove/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):

```shell
spo app remove --id <app id>
```


### <a name="use-apps-on-your-site"></a>Использование приложений на сайте
Добавив приложение в каталог и опубликовав его, вы можете установить приложение на своем сайте с помощью команды [install](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-install/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):

```shell
spo app install --id <app id> --siteUrl <url>
```


Для обновления приложения используйте команду [upgrade](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-upgrade/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):

```shell
spo app upgrade --id <app id> --siteUrl <url>
```


С помощью команды [uninstall](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-uninstall/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) можно удалить приложение с сайта:

```shell
spo app uninstall --id <app id> --siteUrl <url>
```


> [!NOTE]
> При этом оно удаляется полностью, поэтому не попадает в корзину сайта.


### <a name="list-and-get-apps-in-the-app-catalog"></a>Перечисление приложений в каталоге и их получение
С помощью команды [list](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-list/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs) можно узнать, какие приложения были добавлены в каталог:

```shell
spo app list
```


Чтобы получить сведения об отдельном приложении, используйте команду [get](https://sharepoint.github.io/office365-cli/cmd/spo/app/app-get/?utm_source=msft_docs&utm_medium=page&utm_campaign=Application+Lifecycle+Management+ALM+APIs):

```shell
spo app get --id <app id>
```

## <a name="see-also"></a>См. также

- [Знакомство со службой REST в SharePoint](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)
