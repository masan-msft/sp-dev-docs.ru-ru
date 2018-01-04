---
title: "API управления жизненным циклом приложений (ALM)"
ms.date: 12/19/2017
ms.prod: sharepoint
ms.assetid: fdf7ecb2-8851-425b-b058-3285fba77b68
ms.openlocfilehash: 6baa3e3aa2f29df62c20b30e8e2a392af5f278a7
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="application-lifecycle-management-alm-apis"></a>API управления жизненным циклом приложений (ALM)  

API управления жизненным циклом приложений — простые API-интерфейсы для управления развертыванием решений и надстроек SharePoint Framework в клиенте. Эти API поддерживают приведенные ниже возможности.

- Добавление решения SharePoint Framework или надстройки SharePoint в каталог приложений клиента.
- Обеспечение доступности решения SharePoint Framework или надстройки SharePoint для установки в каталоге приложений клиента.
- Отключение возможности установки решения SharePoint Framework или надстройки SharePoint в каталоге приложений клиента.
- Установка решения SharePoint Framework или надстройки SharePoint из каталога приложений клиента на сайте.
- Обновление решения SharePoint Framework или надстройки SharePoint для использования на сайте с более поздней версией, доступной в каталоге приложений клиента.
- Удаление решения SharePoint Framework или надстройки SharePoint с сайта.

API управления жизненным циклом приложений можно использовать для выполнения тех же операций, которые доступны для пользовательского интерфейса. При использовании этих API выполняются все типичные действия. Ниже описаны некоторые характеристики API ALM.

- При выполнении соответствующих операций происходят события установки и удаления надстроек, размещаемых у поставщика.
- API ALM поддерживают операции только для приложений.

API ALM изначально предоставляются с использованием REST API, но есть дополнительные расширения CSOM и командлеты PowerShell, доступные благодаря SharePoint PnP.

> [!NOTE] 
> API управления жизненным циклом приложений для [каталога приложений семейства сайтов](../general-development/site-collection-app-catalog.md) в настоящее время не поддерживаются. Поддержка будет добавлена в начале 2018 г.

## <a name="rest-api"></a>API REST

### <a name="add-solution-package-to-tenant-app-catalog"></a>Добавление пакета решения в каталог приложений клиента 

Добавление решения в каталог приложений клиента. Этот API разработан для выполнения в контексте сайта каталога приложений клиента.

```
/_api/web/tenantappcatalog/Add(overwrite=true, url='test.txt')";
method: POST
binaryStringRequestBody: true
body: 'byte array of the file'
```

### <a name="deploy-solution-package-in-tenant-app-catalog"></a>Развертывание пакета решения в каталоге приложений клиента

Обеспечение возможности установить решение на определенных сайтах. Этот API разработан для выполнения в контексте сайта каталога приложений клиента.

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Deploy";
```

> [!NOTE]
> Эта операция должна быть завершена после добавления, прежде чем вы сможете устанавливать пакеты на определенные сайты. 

### <a name="retract-solution-package-in-the-tenant-app-catalog"></a>Отзыв пакета решения в каталоге приложений клиента

Отзыв решения для отмены его доступности на сайтах. Этот API разработан для выполнения в контексте сайта каталога приложений клиента.

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Retract";
```

> [!NOTE]
> Если вы запустите эту операцию уже после установки решений на сайте, они перестанут работать, так как на уровне клиента решения отключены.

### <a name="remove-solution-package-from-tenant-app-catalog"></a>Удаление пакета решения из каталога приложений клиента

Удаляет пакет решения из каталога приложений клиента. Этот API разработан для выполнения в контексте сайта каталога приложений клиента.

```
/_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Remove";
```

> [!NOTE]
> Решение также будет автоматически отозвано, если эта операция не была выполнена до операции удаления.

### <a name="list-available-packages-from-tenant-app-catalog"></a>Перечисление доступных пакетов из каталога приложений клиента

REST API для получения списка доступных надстроек или решений SharePoint Framework в каталоге приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps
method: GET
```

### <a name="details-on-individual-solution-package-from-tenant-app-catalog"></a>Сведения об отдельном пакете решения из каталога приложений клиента

REST API для получения сведений об отдельных надстройках или решениях SharePoint Framework, которые доступны в каталоге приложений клиента.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')
method: GET
```

### <a name="install-solution-package-from-tenant-app-catalog-to-sharepoint-site"></a>Установка пакета решения из каталога приложений клиента на сайте SharePoint

Установка пакета решения с определенным идентификатором из каталога приложений клиента на сайте с учетом контекста URL-адреса. Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция установки.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Install";
method: POST
```

### <a name="upgrade-solution-package-in-sharepoint-site"></a>Обновление пакета решения на сайте SharePoint

Обновление пакета решения с сайта до более новой версии, доступной в каталоге приложений клиента. Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция обновления.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Upgrade";
method: POST
```

### <a name="uninstall-solution-package-from-sharepoint-site"></a>Удаление пакета решения с сайта SharePoint

Удаление пакета решения с сайта. Вызов REST может быть выполнен в контексте сайта, на котором должна выполняться операция удаления.

```
url: /_api/web/tenantappcatalog/AvailableApps/GetById('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx')/Uninstall";
method: POST
```
> [!NOTE]
> Когда вы используете REST API для удаления пакета решения с сайта, он не перемещается в корзину.


## <a name="sharepoint-pnp-powershell-cmdlets-to-programmatically-add-and-deploy-sharepoint-apps"></a>Командлеты PnP PowerShell SharePoint для добавления и развертывания приложений SharePoint программным способом

При помощи [PnP PowerShell]((https://msdn.microsoft.com/ru-RU/pnp_powershell/pnp-powershell-overview)) вы можете автоматизировать развертывание, публикацию, установку, обновление и отзыв приложений. Дополнительные сведения об этих командлетах вы найдете в приведенном ниже разделе.

### <a name="adding-and-publishing-your-app-to-the-app-catalog"></a>Добавление и публикация приложения в каталоге приложений
Добавление приложения (.sppkg, .app) в каталог приложений клиента является обязательным условием для дальнейшего использования этого приложения на сайтах SharePoint. Это можно сделать с помощью приведенного ниже простого командлета.

```PowerShell
Add-PnPApp -Path ./myapp.sppkg"
```

Следующий после добавления шаг — публикация приложения. Так оно будет доступно пользователям вашего клиента. Ниже на примере командлета PnP PowerShell показано, как это можно сделать.

```PowerShell
Publish-PnPApp -Identity <app id> -SkipFeatureDeployment
```


> [!NOTE]
> Используйте флажок SkipFeatureDeployment, чтобы приложение, разработанное для развертывания на уровне клиента, было фактически доступно в этом качестве.



### <a name="removing-the-app-from-the-app-catalog"></a>Удаление приложения из каталога приложений
Вы также можете удалить ранее добавленное приложение с помощью приведенного ниже командлета.

```PowerShell
Remove-PnPApp -Identity <app id>
```


### <a name="using-apps-on-your-site"></a>Использование приложений на сайте
После добавления приложения в каталог приложений и его публикации вы можете установить это приложение на своем сайте.

```PowerShell
Install-PnPApp -Identity <app id>
```


Добавленное приложение следует обновить:

```PowerShell
Update-PnPApp -Identity <app id>
```


Затем приложение можно снова удалить с сайта:

```PowerShell
Uninstall-PnPApp -Identity <app id>
```


> [!NOTE]
> При удалении приложения с сайта оно удаляется полностью, поэтому не попадает в корзину сайта.



### <a name="knowing-which-apps-are-there-for-you-to-use"></a>Информация о доступных приложениях
При помощи приведенного ниже командлета вы получите список приложений, которые можно добавить на сайт.

```PowerShell
Get-PnPAvailableApp
```
