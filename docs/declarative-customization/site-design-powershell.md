---
title: "Командлеты PowerShell для макетов и скриптов сайтов SharePoint"
description: "Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell."
ms.date: 12/14/2017
ms.openlocfilehash: e6f9f0324cb0879317d04aa9873ad168072073cc
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a>Командлеты PowerShell для макетов и скриптов сайтов SharePoint

> [!NOTE]
> Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены. Сейчас они не поддерживаются для использования в рабочих средах.

Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell.

## <a name="getting-started"></a>Начало работы

Чтобы использовать командлеты PowerShell, выполните указанные ниже действия.

1. Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588). Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.
1. Подключитесь к клиенту SharePoint, следуя инструкциям в статье [Подключение к PowerShell в SharePoint Online]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx)).

Чтобы проверить настройки, попробуйте выполнить командлет **Get-SPOSiteScript**, считывающий текущий список скриптов сайта. Если командлет выполнится без ошибок, то можно двигаться дальше.

## <a name="site-design-cmdlets"></a>Командлеты для макетов сайтов

Для управления макетами и скриптами сайтов в PowerShell доступны следующие командлеты:

- **Add-SPOSiteDesign**
- **Add-SPOSiteScript**
- **Get-SPOSiteDesign**
- **Get-SPOSiteDesignRights**
- **Get-SPOSiteScript**
- **Grant-SPOSiteDesignRights**
- **Remove-SPOSiteDesign**
- **Remove-SPOSiteScript**
- **Revoke-SPOSiteDesignRights**

<!--
- **Set-SPOSiteDesign**
- **Set-SPOSiteScript**
-->

<!-- TBD document pipe bind parameters -->

## <a name="add-spositedesign"></a>Add-SPOSiteDesign

Создает макет сайта, доступный пользователям при создании сайта на домашней странице SharePoint.

```powershell
Add-SPOSiteDesign
  -Title <string>
  -WebTemplate <string>
  -SiteScripts <SPOSiteScriptPipeBind[]>
  [-Description <string>]
  [-PreviewImageUrl <string>]
  [-PreviewImageAltText <string>]
  [-IsDefault]
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр  | Описание  |
|-----------|--------------|
|-Title                 | Отображаемое имя макета сайта. |
|-WebTemplate           | Указывает, к какому базовому шаблону будет добавлен макет. Значение **64** обозначает шаблон сайта группы, а значение **68** — шаблон сайта для общения. |
|-SiteScripts           | Массив из одного или нескольких скриптов сайта. Каждый из них определяется по идентификатору. Скрипты будут выполняться в указанном порядке. |
|[-Description]         | Отображаемое описание макета сайта. |
|[-PreviewImageUrl]     | URL-адрес изображения для предварительного просмотра. Если он не указан, в SharePoint будет использоваться стандартное изображение. |
|[-PreviewImageAltText] | Замещающий текст с описанием изображения для специальных возможностей. |
|[-IsDefault]           | Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию. Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md) |

Ниже представлен пример создания макета сайта.

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview"
```

## <a name="add-spositescript"></a>**Add-SPOSiteScript**

Отправляет новый скрипт сайта для использования напрямую или в макете сайта.

```powershell
Add-SPOSiteScript
  -Title <string>
  -Content <string>
  [-Description <string>]
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| -Title       | Отображаемое имя макета сайта. |
| -Content     | Значение JSON, описывающее скрипт. Дополнительные сведения см. в [справочнике по JSON](site-design-json-schema.md).|
| -Description | Описание скрипта. |

Ниже приведен пример добавления сайта из приведенного ниже скрипта в файле.

```json
{
  "verb": "setSiteLogo",
  "url": "https://contoso.sharepoint.com/SiteAssets/company-logo.png"
},
```

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' -Raw | Add-SPOSiteScript -Title "Customer logo" -Description "Applies customer logo for customer sites"
```

## <a name="get-spositedesign"></a>Get-SPOSiteDesign

Получает сведения о макетах сайтов, находящихся в клиенте SharePoint. Вы можете указать ИД макета сайта, который требуется получить. Если параметры не указаны, отображаются сведения обо всех макетах сайтов.

```powershell
Get-SPOSiteDesign
  [[-Identity] <SPOSiteDesignPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | ИД макета сайта, который требуется получить. |

Ниже приведены пример получения сведений о макете сайта и образец отклика.

```powershell
PS C:\> Get-SPOSiteDesign 44252d09-62c4-4913-9eb0-a2a8b8d7f863

Id                  : 44252d09-62c4-4913-9eb0-a2a8b8d7f863
Title               : Contoso - Team Project
WebTemplate         : 64
SiteScriptIds       : {1306913c-8463-42ca-bd63-efad0fcdbba4}
Description         : Use this design to apply Contoso theme and create
                      custom lists and add to nav
```

## <a name="get-spositedesignrights"></a>Get-SPOSiteDesignRights

Выводит список субъектов и их прав на использование макета сайта. С его помощью можно определить область действия макета сайта для пользователей клиента.

```powershell
Get-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | ИД макета сайта для получения сведений об области. |

Ниже приведен пример получения сведений о правах для макета сайта.

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1

DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="get-spositescript"></a>Get-SPOSiteScript

Выводит сведения об имеющихся скриптах сайтов. Если параметры не указаны, этот командлет возвращает свойства **Id**, **Title**, **Description** и **Version** каждого скрипта сайта. Если указан ИД скрипта, этот командлет также возвращает свойство **Content**, содержащее код JSON скрипта сайта.

```powershell
Get-SPOSiteScript
  [[-Identity] <SPOSiteScriptPipeBind>]
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | Идентификатор скрипта сайта, сведения о котором требуется получить. |

В примере ниже показано, как получить сведения о скрипте для определенного идентификатора скрипта.

```powershell
PS C:\scripts> Get-SPOSiteScript 07702c07-0485-426f-b710-4704241caad9

Id          : 07702c07-0485-426f-b710-4704241caad9
Title       : Contoso theme
Description :
Content     : {
                  "$schema": "schema.json",
                      "actions": [
                          {
                             "verb": "applyTheme",
                             "themeName": "Custom Cyan"
                          }
                      ],
                          "bindata": { },
                  "version": 1
              }
Version     : 1
```

## <a name="grant-spositedesignrights"></a>Grant-SPOSiteDesignRights

Используется для применения разрешений к набору пользователей или группе безопасности. Определяет область видимости макета сайта в пользовательском интерфейсе. По умолчанию макеты являются общедоступными. Однако после установки разрешений доступ к ним смогут получать только те группы и пользователи, у которых есть разрешения.

```powershell
Grant-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  -Rights {View}
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | ИД макета сайта для получения сведений об области. |
| -Principals  | Один или несколько субъектов, для которых добавляются разрешения. |
| -Rights      | Всегда задано значение **View**. Любой пользователь и любая группа с разрешениями на просмотр могут просматривать и использовать макет сайта. |

В приведенном ниже примере показано, как предоставить права для макета сайта пользователю Nestor (пользователю на вымышленном сайте Contoso).

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="remove-spositedesign"></a>Remove-SPOSiteDesign

Удаляет макет сайта. Он больше не будет отображаться в пользовательском интерфейсе создания сайта.

```powershell
  Remove-SPOSiteDesign
  [-Identity] <SPOSiteDesignPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | Идентификатор макета сайта, который требуется удалить. |

Ниже приведен пример удаления макета сайта.

```powershell

```

## <a name="remove-spositescript"></a>Remove-SPOSiteScript

Удаляет скрипт сайта. <!-- TBD how is dependency problem handled so you don't delete a script that a design depends on. this currently creates an error when running the design.) -->

```powershell
Remove-SPOSiteScript
  [-Identity] <SPOSiteScriptPipeBind>
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | ИД скрипта сайта, который требуется удалить. |

```powershell
C:\> Remove-SPOSiteDesign 21209d88-38de-4844-9823-f1f600a1179a
```

## <a name="revoke-spositedesignrights"></a>Revoke-SPOSiteDesignRights

Отзывает права доступа к макету сайта для указанных субъектов.

```powershell
Revoke-SPOSiteDesignRights
  [-Identity] <SPOSiteDesignPipeBind>
  -Principals <string[]>
  [<CommonParameters>]
```

### <a name="parameters"></a>Параметры

|Параметр     | Описание  |
|--------------|--------------|
| [-Identity]  | ИД макета сайта, для которого требуется отозвать права. |
| -Principals  | Один или несколько субъектов, для которых требуется отозвать права доступа к указанному макету сайта. |

В примере ниже показано, как отозвать права на макет сайта для пользователя Nestor.

```powershell
PS C:\> Revoke-SPOSiteDesignRights 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
   -Principals "nestorw@contoso.onmicrosoft.com"
```

<!--
## Set-SPOSiteDesign (TBD)

## Set-SPOSiteScript (TBD)
-->

## <a name="see-also"></a>См. также

- [Справочные материалы по схеме JSON](site-design-json-schema.md)
- [REST API](site-design-rest-api.md)Применение области к макету сайта](site-design-scoping.md)
