---
title: "API управления жизненным циклом приложений (ALM)"
description: "API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: a0980afd0679398c60e3f5e9ef8ae158d5b719ee
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="application-lifecycle-management-alm-apis"></a>API управления жизненным циклом приложений (ALM)  

API ALM представляют собой простые API для управления развертыванием решений и надстроек SharePoint Framework в клиенте. Эти API поддерживают указанные ниже возможности.

- Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.
- Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.
- Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.
- Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.
- Обновление решения SharePoint Framework или надстройки SharePoint на сайте до более поздней версии, доступной в каталоге приложений клиента.
- Удаление решения SharePoint Framework или надстройки SharePoint с сайта.

С помощью API ALM можно выполнять те же операции, что и в пользовательском интерфейсе. При использовании этих API выполняются все типичные действия. Ниже описаны некоторые характеристики API ALM.

- События `Install` и `UnInstall` вызываются для надстроек с размещением у поставщика при выполнении соответствующих операций.
- API ALM поддерживают операции только для приложений.

API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM и командлеты PowerShell, доступные благодаря SharePoint PnP.

> [!NOTE] 
> API управления жизненным циклом приложений для [каталога приложений семейства сайтов](../general-development/site-collection-app-catalog.md) в настоящее время не поддерживаются. Поддержка будет добавлена в начале 2018 г.

## <a name="rest-api"></a>REST API

### <a name="add-solution-packages-to-the-tenant-app-catalog"></a>Добавление пакетов решений в каталог приложений клиента 

Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-packages-in-the-tenant-app-catalog"></a>Развертывание пакетов решений в каталоге приложений клиента

Это позволяет устанавливать решение на определенных сайтах. Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy
```

> [!NOTE]
> Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты. 

### <a name="retract-solution-packages-in-the-tenant-app-catalog"></a>Отзыв пакетов решений в каталоге приложений клиента

При этом решение становится недоступно на сайтах. Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract
```

> [!NOTE]
> Если выполнить эту операцию после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.

### <a name="remove-solution-packages-from-the-tenant-app-catalog"></a>Удаление пакетов решений из каталога приложений клиента

Этот API разработан для выполнения в контексте каталога приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove
```

> [!NOTE]
> Если не отозвать решение перед его удалением, то решение будет отозвано автоматически.

### <a name="list-available-packages-from-the-tenant-app-catalog"></a>Перечисление доступных пакетов из каталога приложений клиента

С помощью этого REST API можно получить список доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-about-individual-solution-packages-in-the-tenant-app-catalog"></a>Сведения об отдельных пакетах решений в каталоге приложений клиента

С помощью этого REST API можно получать сведения об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-the-tenant-app-catalog-to-a-sharepoint-site"></a>Установка пакета решения из каталога приложений клиента на сайте SharePoint

Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте на основе контекста URL-адреса. Этот вызов REST может выполняться в контексте сайта, на котором запланирована установка.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install
method: POST
```

### <a name="upgrade-solution-packages-on-the-sharepoint-site"></a>Обновление пакета решения на сайте SharePoint

Обновите пакет решения на сайте до более новой версии, доступной в каталоге приложений клиента. Этот вызов REST может выполняться в контексте сайта, на котором запланировано обновление.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade
method: POST
```

### <a name="uninstall-solution-packages-from-the-sharepoint-site"></a>Удаление пакетов решений с сайта SharePoint

Этот вызов REST может выполняться в контексте сайта, на котором запланировано удаление.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall
method: POST
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

Добавив приложение, следует опубликовать его. Так оно будет доступно пользователям вашего клиента. Ниже на примере командлета PnP PowerShell показано, как это можно сделать.

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

## <a name="see-also"></a>См. также

- [Знакомство со службой REST в SharePoint](../sp-add-ins/get-to-know-the-sharepoint-rest-service.md)