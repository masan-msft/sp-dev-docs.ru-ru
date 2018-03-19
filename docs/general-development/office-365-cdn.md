---
title: "Использование сети доставки содержимого Office 365"
ms.date: 1/11/2018
ms.prod: sharepoint
ms.assetid: 21ac1941-6a8b-4f33-8408-0c1f36295893
ms.openlocfilehash: 3bf18c0687084713997a0bc169df4024e461b23a
ms.sourcegitcommit: bd167bbbcae67b7f1c6a40366183781a80337bc2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2018
---
# <a name="use-the-office-365-content-delivery-network-cdn"></a>Использование сети доставки содержимого (CDN) Office 365

_**Область применения:** Office 365_.

Вы можете размещать статические ресурсы в сети доставки содержимого (CDN) Office 365, чтобы повысить производительность своих страниц SharePoint Online. Статические ресурсы — это файлы, которые редко меняются, например изображения, видео и звуковые файлы, таблицы стилей, шрифты и файлы JavaScript. Сеть CDN работает как географически распределенный прокси-сервер кэширования. Она кэширует статические архивы ближе к браузерам, которые их запрашивают.

## <a name="office-365-cdn-basics"></a>Основные сведения о сети CDN Office 365

Сеть CDN Office 365 входит в состав подписки на SharePoint Online. За нее не нужно доплачивать. Office 365 поддерживает как открытый, так и закрытый доступ. Кроме того, вы можете размещать статические ресурсы во множестве расположений, или источников. Сеть CDN Office 365 — это не то же самое, что Azure CDN. Дополнительные сведения о том, зачем использовать сеть CDN, и об общих понятиях, связанных с такими сетями, см. в статье [Сети доставки содержимого](https://support.office.com/ru-RU/article/Content-delivery-networks-0140f704-6614-49bb-aa6c-89b75dcd7f1f).

## <a name="office-365-cdn-types"></a>Типы сетей CDN Office 365

В Office 365 доступно два типа сетей CDN: частные и общедоступные. Оба варианта повышают производительность, но у каждого есть свои уникальные атрибуты и преимущества.

### <a name="office-365-public-cdn"></a>Общедоступная сеть CDN Office 365

![Схема, иллюстрирующая использование общедоступной сети CDN Office 365](../images/o365-cdn-public-logical.png)

1. Администратор включает общедоступную сеть CDN Office 365 для клиента.
1. Статические ресурсы, предоставляемые из сети CDN, отправляются в библиотеки SharePoint, включенные в качестве общедоступных источников CDN.
1. Ресурсы из настроенных библиотек и папок передаются в службу CDN.
1. URL-адреса, указывающие на расположение сети CDN, доступны для использования на сайтах SharePoint и в модификациях, работающих на страницах SharePoint.

> [!NOTE]
> Никогда не следует помещать конфиденциальные ресурсы организации в библиотеку документов, настроенную в качестве общедоступного источника CDN.

#### <a name="office-365-public-cdn-attributes-and-advantages"></a>Атрибуты и преимущества общедоступной сети CDN Office 365

- Ресурсы, предоставляемые из общедоступного источника, доступны всем анонимно.
- Если удалить ресурс из общедоступного источника, он может оставаться доступным в кэше до 30 дней. Однако ссылки на ресурс в сети CDN станут недействительными в течение 15 минут.
- При размещении таблиц стилей (CSS-файлов) в общедоступном источнике можно использовать в коде относительные пути и URI. Это означает, что вы можете ссылаться на расположение фоновых изображений и других объектов относительно расположения ресурса, который вызывает его.
- Вы можете жестко задать URL-адрес общедоступного источника, но это не рекомендуется. Это связано с тем, что если сеть CDN станет недоступна, то URL-адрес не будет автоматически указывать на вашу организацию в SharePoint Online, что может привести к неработоспособности ссылок и другим ошибкам. Следовательно, рекомендуем использовать URL-адреса SharePoint, чтобы среда SharePoint автоматически заменяла их на URL-адрес общедоступной сети CDN, если она включена.
- По умолчанию для общедоступных источников включены типы файлов CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF. Вы можете указывать дополнительные типы файлов, меняя [конфигурацию сети CDN](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnpolicy?view=sharepoint-ps).
- При желании вы можете настроить политику, которая исключает ресурсы, определенные в заданных вами классификациях сайтов. Например, вы можете исключать все ресурсы, отмеченные как "конфиденциальные" или "с ограниченным доступом", даже если они относятся к разрешенным типам файлов и находятся в общедоступном источнике.

### <a name="office-365-private-cdn"></a>Частная сеть CDN Office 365

![Схема, иллюстрирующая использование частной сети CDN Office 365](../images/o365-cdn-private-logical.png)

1. Администратор включает частную сеть CDN Office 365 для клиента.
1. Статические ресурсы, предоставляемые из сети CDN, отправляются в библиотеки SharePoint, включенные в качестве частных источников CDN.
1. Ресурсы из назначенных частных источников CDN передаются в службу CDN.
1. Когда пользователи запрашивают страницы с использованием ресурсов, хранящихся в каком-либо из источников CDN, SharePoint автоматически меняет адрес, чтобы он указывал на сеть CDN, а ресурсы предоставлялись из нее.
1. Во время замены URL-адреса для ресурсов, предоставляемых из сети CDN, должна быть опубликована основная версия, а у пользователей должны быть разрешения на доступ к этим ресурсам.

#### <a name="office-365-private-cdn-attributes-and-advantages"></a>Атрибуты и преимущества частной сети CDN Office 365

- Ресурсы из частного источника доступны только тем пользователям, у которых есть соответствующие разрешения. Анонимный доступ к таким ресурсам запрещен.
- Если удалить ресурс из частного источника, он может оставаться доступным в кэше до одного часа. Однако ссылки на ресурс в сети CDN станут недействительными в течение 15 минут.
- По умолчанию для частных источников включены типы файлов GIF, ICO, JPEG, JPG, JS и PNG. Вы можете указывать дополнительные типы файлов, меняя [конфигурацию сети CDN](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnpolicy?view=sharepoint-ps).
- Как в случае общедоступных источников, вы можете настроить политику, исключающую ресурсы, которые определены в заданных вами классификациях сайтов, даже если вы используете подстановочные знаки, чтобы включить все ресурсы в папке или библиотеке сайта.

### <a name="publishing-feature-auto-rewriting-to-cdn-urls"></a>Автоматическая замена URL-адресов на URL-адреса CDN, которую выполняет функция публикации

Чтобы помочь организациям пользоваться возможностями сетей CDN Office 365, не обновляя имеющиеся порталы, мы обновили функцию публикации в SharePoint, чтобы автоматически заменять URL-адреса ресурсов, хранящихся в источниках CDN, на их эквиваленты в сети CDN, чтобы ресурсы предоставлялись из службы CDN, а не из SharePoint.

Ниже представлен обзор ссылок, которые автоматически заменяет функция публикации в SharePoint.

- URL-адреса IMG-, LINK- и CSS-файлов в HTML-откликах классической страницы публикации.
  - Это относится и к изображениям, добавленным авторами в HTML-содержимом страницы.
  - Расширяя страницы, вы можете временно отключать автоматическую замену URL-адресов на странице. Для этого сделайте следующее:
    - извлеките страницу;
    - укажите параметр `?NoAutoReWrites=true` строки запроса.
- Ресурсы веб-части "Контент по поиску".
  - Файлы JavaScript шаблонов отображения.
  - Изображения в результатах запросов. Автоматически заменяются URL-адреса в следующих стандартных управляемых свойствах: _PictureUrl_, _PictureThumbnailUrl_, _PublishingImage_.
- URL-адреса изображений в веб-части "Слайд-шоу библиотеки рисунков".
- Поля изображений в результатах работы REST API SPList (RenderListDataAsStream).
  - Используйте новое свойство ImageFieldsToTryRewriteToCdnUrls, чтобы создать разделенный запятыми список полей.
  - Поддерживаются поля Hyperlink (Picture или Link) и PublishingImage.
- Редакции изображений в SharePoint.

## <a name="set-up-and-configure-the-office-365-cdn"></a>Установка и настройка сети CDN Office 365

Вы можете установить и настроить сеть CDN Office 365 в своем клиенте с помощью командной консоли SharePoint Online или интерфейса командной строки Office 365.

### <a name="set-up-and-configure-the-office-365-cdn-using-the-sharepoint-online-management-shell"></a>Установка и настройка сети CDN Office 365 с помощью командной консоли SharePoint Online

> [!NOTE]
> Чтобы управлять каталогами приложений в клиенте, установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588). Затем подключитесь к клиенту SharePoint Online с помощью командлета `Connect-SPOService`.

#### <a name="enable-office-365-cdn"></a>Включение сети CDN Office 365

Вы можете управлять состоянием сети CDN Office 365 в клиенте с помощью командлета [Set-SPOTenantCdnEnabled](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnenabled?view=sharepoint-ps).

Чтобы включить в клиенте общедоступную сеть CDN Office 365, выполните следующую команду:

```powershell
Set-SPOTenantCdnEnabled -CdnType Public -Enable $true
```

Чтобы включить частную сеть CDN Office 365, выполните следующую команду:

```powershell
Set-SPOTenantCdnEnabled -CdnType Private -Enable $true
```

Кроме того, если вы хотите использовать сети CDN обоих типов, их можно включить с помощью следующей команды:

```powershell
Set-SPOTenantCdnEnabled -CdnType Both -Enable $true
```

Если вы не хотите использовать стандартные источники CDN, добавьте параметр `-NoDefaultOrigins`:

```powershell
Set-SPOTenantCdnEnabled -CdnType Both -Enable $true -NoDefaultOrigins
```

#### <a name="view-the-current-status-of-the-office-365-cdn"></a>Просмотр текущего состояния сети CDN Office 365

Чтобы проверить, включена ли сеть CDN Office 365 определенного типа, используйте командлет [Get-SPOTenantCdnEnabled](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnenabled?view=sharepoint-ps).

Чтобы проверить, включена ли общедоступная сеть CDN Office 365, выполните следующую команду:

```powershell
Get-SPOTenantCdnEnabled -CdnType Public
```

#### <a name="view-office-365-cdn-origins"></a>Просмотр источников CDN Office 365

Чтобы просмотреть список настроенных в данный момент общедоступных источников CDN Office 365, выполните следующую команду:

```powershell
Get-SPOTenantCdnOrigins -CdnType Public
```

#### <a name="add-office-365-cdn-origin"></a>Добавление источника сети CDN Office 365

> [!NOTE]
> Никогда не следует помещать конфиденциальные ресурсы организации в библиотеку документов SharePoint, настроенную в качестве общедоступного источника CDN.

Чтобы определить источник CDN, используйте командлет [Add-SPOTenantCdnOrigin](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/add-spotenantcdnorigin?view=sharepoint-ps). Вы можете определить несколько источников. Источник — это URL-адрес, указывающий на библиотеку или папку в SharePoint, содержащую ресурсы, которые требуется размещать в сети CDN.

```powershell
Add-SPOTenantCdnOrigin -CdnType <Public | Private> -OriginUrl <path>
```

`path` — это путь к папке, содержащей ресурсы. Помимо относительных путей, можно использовать подстановочные знаки.

Чтобы включить все ресурсы в коллекции эталонных страниц на всех сайтах в качестве общедоступного источника CDN, выполните следующую команду:

```powershell
Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */masterpage
```

Чтобы настроить частный источник для определенного семейства веб-сайтов, выполните следующую команду:

```powershell
Add-SPOTenantCdnOrigin -CdnType Private -OriginUrl sites/site1/siteassets
```

> [!NOTE]
> После добавления источника CDN может понадобиться до 15 минут, чтобы получить файлы через службу CDN. Вы можете проверить, включен ли тот или иной источник, с помощью командлета [Get-SPOTenantCdnOrigins](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnorigins?view=sharepoint-ps).

#### <a name="remove-office-365-cdn-origin"></a>Удаление источника CDN Office 365

Чтобы удалить источник CDN для указанного типа CDN, используйте командлет [Remove-SPOTenantCdnOrigin](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/remove-spotenantcdnorigin?view=sharepoint-ps).

Чтобы удалить источник из конфигурации частной сети CDN, выполните следующую команду:

```powershell
Remove-SPOTenantCdnOrigin -CdnType Public -OriginUrl */masterpage
```

> [!NOTE]
> Удаление источника CDN не влияет на файлы, хранящиеся в какой-либо библиотеке документов, соответствующей этому источнику. Если на эти ресурсы ссылались по их URL-адресу в SharePoint, то среда SharePoint автоматически вернется к исходному URL-адресу, указывающему на библиотеку документов. Но если на ресурсы ссылались по URL-адресу общедоступной сети CDN, то эти ссылки станут неработоспособными, и их потребуется изменить вручную.

#### <a name="modify-office-365-cdn-origin"></a>Изменение источника CDN Office 365

Изменить имеющийся источник CDN невозможно. Вместо этого следует удалить определенный ранее источник CDN с помощью командлета `Remove-SPOTenantCdnOrigin` и добавить новый с помощью командлета `Add-SPOTenantCdnOrigin`.

#### <a name="change-the-types-of-files-to-include-in-office-365-cdn"></a>Изменение типов файлов, включаемых в сеть CDN Office 365

По умолчанию для общедоступной сети CDN включены следующие типы файлов: _CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF_. Если требуется включить в сеть CDN дополнительные типы файлов, вы можете изменить конфигурацию CDN с помощью командлета [Set-SPOTenantCdnPolicy](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnpolicy?view=sharepoint-ps).

> [!NOTE]
> При изменении списка типов файлов перезаписывается текущий список. Если требуется включить дополнительные типы файлов, сперва используйте командлет [Get-SPOTenantCdnPolicies](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnpolicies?view=sharepoint-ps), чтобы узнать, какие типы файлов настроены в текущий момент.

Чтобы добавить тип файла _JSON_ в стандартный список типов файлов, включенных в сеть CDN, выполните следующую команду:

```powershell
Set-SPOTenantCdnPolicy -CdnType Public -PolicyType IncludeFileExtensions -PolicyValue "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF,JSON"
```

#### <a name="change-the-list-of-site-classifications-you-want-to-exclude-from-the-office-365-cdn"></a>Изменение списка классификаций сайтов, которые требуется исключить из сети CDN Office 365

Чтобы исключить классификации сайтов, которые не должны быть доступны в сети CDN, используйте командлет [Set-SPOTenantCdnPolicy](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/set-spotenantcdnpolicy?view=sharepoint-ps). По умолчанию не исключаются никакие классификации сайтов.

> [!NOTE]
> При изменении списка исключаемых классификаций сайтов перезаписывается текущий список. Если требуется включить дополнительные классификации сайтов, сперва используйте командлет [Get-SPOTenantCdnPolicies](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/get-spotenantcdnpolicies?view=sharepoint-ps), чтобы узнать, какие классификации сайтов настроены в текущий момент.

Чтобы исключить сайты, классифицируемые как _HBI_, из частной сети CDN, выполните следующую команду:

```powershell
Set-SPOTenantCdnPolicy -CdnType Public -PolicyType ExcludeRestrictedSiteClassifications -PolicyValue "HBI"
```

#### <a name="disable-office-365-cdn"></a>Отключение сети CDN Office 365

Чтобы отключить сеть CDN Office 365, используйте командлет `Set-SPOTenantCdnEnabled`. Пример:

```powershell
Set-SPOTenantCdnEnabled -CdnType Public -Enable $false
```

### <a name="set-up-and-configure-the-office-365-cdn-using-the-office-365-cli"></a>Установка и настройка сети CDN Office 365 с помощью интерфейса командной строки Office 365:

> [!NOTE]
> Чтобы управлять каталогами приложений в клиенте, установите [интерфейс командной строки Office 365](https://aka.ms/o365cli). Затем подключитесь к клиенту SharePoint Online с помощью команды [spo connect](https://sharepoint.github.io/office365-cli/cmd/spo/connect/).

#### <a name="enable-office-365-cdn"></a>Включение сети CDN Office 365

Вы можете управлять состоянием сети CDN Office 365 в клиенте с помощью команды [spo cdn set](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-set/).

Чтобы включить в клиенте общедоступную сеть CDN Office 365, выполните следующую команду:

```sh
spo cdn set --type Public --enabled true
```

Чтобы включить частную сеть CDN Office 365, выполните следующую команду:

```sh
spo cdn set --type Private --enabled true
```

#### <a name="view-the-current-status-of-the-office-365-cdn"></a>Просмотр текущего состояния сети CDN Office 365

Чтобы проверить, включена ли сеть CDN Office 365 определенного типа, используйте команду [spo cdn get](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-get/).

Чтобы проверить, включена ли общедоступная сеть CDN Office 365, выполните следующую команду:

```sh
spo cdn get --type Public
```

#### <a name="view-office-365-cdn-origins"></a>Просмотр источников CDN Office 365

Чтобы просмотреть список настроенных в данный момент общедоступных источников CDN Office 365, выполните следующую команду:

```sh
spo cdn origin list --type Public
```

#### <a name="add-office-365-cdn-origin"></a>Добавление источника сети CDN Office 365

> [!NOTE]
> Никогда не следует помещать конфиденциальные ресурсы организации в библиотеку документов SharePoint, настроенную в качестве общедоступного источника CDN.

Чтобы определить источник CDN, используйте команду [spo cdn origin add](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-add/). Вы можете определить несколько источников. Источник — это URL-адрес, указывающий на библиотеку или папку в SharePoint, содержащую ресурсы, которые требуется размещать в сети CDN.

```sh
spo cdn origin add --type [Public | Private] --origin <path>
```

`path` — это путь к папке, содержащей ресурсы. Помимо относительных путей, можно использовать подстановочные знаки.

Чтобы включить все ресурсы в коллекции эталонных страниц на всех сайтах в качестве общедоступного источника CDN, выполните следующую команду:

```sh
spo cdn origin add --type Public --origin */masterpage
```

Чтобы настроить частный источник для определенного семейства веб-сайтов, выполните следующую команду:

```sh
spo cdn origin add --type Private --origin sites/site1/siteassets
```

> [!NOTE]
> После добавления источника CDN может понадобиться до 15 минут, чтобы получить файлы через службу CDN. Вы можете проверить, включен ли тот или иной источник, с помощью команды [spo cdn origin list](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-list/).

#### <a name="remove-office-365-cdn-origin"></a>Удаление источника CDN Office 365

Чтобы удалить источник CDN для указанного типа CDN, используйте команду [spo cdn origin remove](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-remove/).

Чтобы удалить источник из конфигурации частной сети CDN, выполните следующую команду:

```sh
spo cdn origin remove --type Public --origin */masterpage
```

> [!NOTE]
> Удаление источника CDN не влияет на файлы, хранящиеся в какой-либо библиотеке документов, соответствующей этому источнику. Если на эти ресурсы ссылались по их URL-адресу в SharePoint, то среда SharePoint автоматически вернется к исходному URL-адресу, указывающему на библиотеку документов. Но если на ресурсы ссылались по URL-адресу общедоступной сети CDN, то эти ссылки станут неработоспособными, и их потребуется изменить вручную.

#### <a name="modify-office-365-cdn-origin"></a>Изменение источника CDN Office 365

Изменить имеющийся источник CDN невозможно. Вместо этого следует удалить определенный ранее источник CDN с помощью команды `spo cdn origin remove` и добавить новый с помощью команды `spo cdn origin add`.

#### <a name="change-the-types-of-files-to-include-in-office-365-cdn"></a>Изменение типов файлов, включаемых в сеть CDN Office 365

По умолчанию для сети CDN включены следующие типы файлов: _CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF_. Если требуется включить в сеть CDN дополнительные типы файлов, вы можете изменить конфигурацию CDN с помощью команды [spo cdn policy set](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-policy-set/).

> [!NOTE]
> При изменении списка типов файлов перезаписывается текущий список. Если требуется включить дополнительные типы файлов, сперва используйте команду [spo cdn policy list](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-origin-list/), чтобы узнать, какие типы файлов настроены в текущий момент.

Чтобы добавить тип файла _JSON_ в стандартный список типов файлов, включенных в сеть CDN, выполните следующую команду:

```sh
spo cdn policy set --type Public --policy IncludeFileExtensions --value "CSS,EOT,GIF,ICO,JPEG,JPG,JS,MAP,PNG,SVG,TTF,WOFF,JSON"
```

#### <a name="change-the-list-of-site-classifications-you-want-to-exclude-from-the-office-365-cdn"></a>Изменение списка классификаций сайтов, которые требуется исключить из сети CDN Office 365

Чтобы исключить классификации сайтов, которые не должны быть доступны в сети CDN, используйте команду [spo cdn policy set](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-policy-set/). По умолчанию не исключаются никакие классификации сайтов.

> [!NOTE]
> При изменении списка исключаемых классификаций сайтов перезаписывается текущий список. Если требуется исключить дополнительные классификации сайтов, сперва используйте команду [spo cdn policy list](https://sharepoint.github.io/office365-cli/cmd/spo/cdn/cdn-policy-list/), чтобы узнать, какие классификации настроены в текущий момент.

Чтобы исключить сайты, классифицируемые как _HBI_, из частной сети CDN, выполните следующую команду:

```sh
spo cdn policy set --type Public --policy ExcludeRestrictedSiteClassifications --value "HBI"
```

#### <a name="disable-office-365-cdn"></a>Отключение сети CDN Office 365

Чтобы отключить сеть CDN Office 365, используйте команду `spo cdn set`. Пример:

```sh
spo cdn set --type Public --enabled false
```

## <a name="see-also"></a>См. также

- [Использование сети доставки содержимого Office 365 с SharePoint Online](https://support.office.com/ru-RU/article/use-the-office-365-content-delivery-network-with-sharepoint-online-bebb285f-1d54-4f79-90a5-94985afc6af8)
- [Видеоролик, посвященный началу работы с сетью CDN Office 365](https://youtu.be/2kI2LnQ-3wQ?list=PLR9nK3mnD-OWSbg0o9a7mx_E7s2u7h_o2)
