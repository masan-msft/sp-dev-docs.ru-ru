---
title: "Командлеты PowerShell для макетов и скриптов сайтов SharePoint"
description: "Узнайте, как создавать, получать и удалять макеты и скрипты сайтов с помощью командлетов PowerShell."
ms.date: 01/08/2018
ms.openlocfilehash: 24c49a9b7e6ae19cd6118573d11720803adc4c94
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="powershell-cmdlets-for-sharepoint-site-designs-and-site-scripts"></a>Командлеты PowerShell для макетов и скриптов сайтов SharePoint

> [!NOTE]
> Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться. В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.

Создавайте, получайте, обновляйте и удаляйте макеты и скрипты сайтов, используя командлеты PowerShell.

## <a name="getting-started"></a>Начало работы

Чтобы использовать командлеты PowerShell, выполните указанные ниже действия.

1. Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588). Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.
1. Подключитесь к клиенту SharePoint, следуя инструкциям в статье [Подключение к PowerShell в SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx).

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
- **Set-SPOSiteDesign**
- **Set-SPOSiteScript**

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
|[-IsDefault]           | Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию. Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md). |

Приведенный ниже код создает макет сайта.

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "<ID>" `
  -Description "Tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview"
```

## <a name="add-spositescript"></a>Add-SPOSiteScript

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

Приведенный ниже пример кода добавляет новый сайт из приведенного ниже скрипта в файле.

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

В примерах кода и отклика, приведенных ниже, показано получение сведений о макете сайта.

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

Приведенный ниже пример кода обеспечивает получение прав для макета сайта.

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

Приведенный ниже пример кода получает сведения о скрипте для определенного идентификатора скрипта.

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

Приведенный ниже пример кода предоставляет пользователю Nestor права на просмотр макета сайта (на вымышленном сайте Contoso).

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

Приведенный ниже пример кода удаляет макет сайта.

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

В приведенном ниже примере показано, как отозвать права на доступ к макету сайта для пользователя Nestor.

```powershell
PS C:\> Revoke-SPOSiteDesignRights 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
   -Principals "nestorw@contoso.onmicrosoft.com"
```

<!--
## Set-SPOSiteDesign (TBD)
Updates a previously uploaded site design.
## Set-SPOSiteScript (TBD)
Updates a previously uploaded site script.
-->

## <a name="set-spositedesign"></a>Set-SPOSiteDesign

Обновляет загруженный ранее макет сайта. 

```powershell
Set-SPOSiteDesign
  -Identity <SPOSiteDesignPipeBind[]>
  [-Title <string>]
  [-WebTemplate <string>]
  [-SiteScripts <SPOSiteScriptPipeBind[]>]
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
|[-IsDefault]           | Если указан этот параметр, макет сайта применяется к шаблону сайта по умолчанию. Дополнительные сведения см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md). |

Приведенный ниже код обновляет созданный ранее макет сайта.

```powershell
C:\> Set-SPOSiteDesign `
  -Title "Contoso customer tracking - version 2" `
  -WebTemplate "68" `
  -Description "Updated site design for list schema that tracks key customer data in a list" `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/site-preview.png" `
  -PreviewImageAltText "site preview - version 2"
```
## <a name="set-spositescript"></a>Set-SPOSiteScript

Обновляет загруженный ранее скрипт сайта.

```powershell
Set-SPOSiteScript
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

Приведенный ниже код обновляет созданный ранее скрипт сайта. Все макеты сайтов с ним будут выполнять обновленный скрипт. 

```json
{
    "$schema": "schema.json",
        "actions": [
            {
                "verb": "addNavLink",
                "url": "/Custom Library",
                "displayName": "Custom Library Updated",
                "isWebRelative": true
            },
            {
                "verb": "addNavLink",
                "url": "/Lists/Custom List",
                "displayName": "Custom List Updated",
                "isWebRelative": true
            },
            {
                "verb": "applyTheme",
                themeName: "Contoso Explorers"
            }
        ],
            "bindata": { },
    "version": 2
}
```
Скопируйте в буфер

```powershell
C:\> $script = Get-Clipboard -Raw
C:\> Set-SPOSiteScript -Identity 7647d3d6-1046-41fe-a798-4ff66b099d12 -Content $script -Description "Update site script to change links and apply Contoso Explorers theme"
```

## <a name="see-also"></a>См. также

- [Справочные материалы по схеме JSON](site-design-json-schema.md)
- [REST API](site-design-rest-api.md)
- [Применение области к макету сайта](site-design-scoping.md)
