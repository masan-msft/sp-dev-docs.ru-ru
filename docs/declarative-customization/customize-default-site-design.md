---
title: "Настройка стандартных дизайнов сайтов в SharePoint"
description: "Настройка стандартных дизайнов сайтов в шаблоне сайта группы или сайта для общения в SharePoint"
ms.date: 12/18/2017
ms.openlocfilehash: 8b5506877f5e7938c16ce2d2dacb928ae57e24f9
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="customize-a-default-site-design"></a>Настройка стандартного дизайна сайта

> [!NOTE]
> Дизайны и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены. Сейчас они не поддерживаются для использования в рабочих средах.

В SharePoint есть несколько дизайнов сайтов, доступных в шаблонах сайтов SharePoint Online. Это стандартные дизайны сайтов. Вы можете изменить их с помощью PowerShell или REST API для контролирования всего процесса подготовки сайта. Например, вы можете сделать так, чтобы тема организации применялась к каждому создаваемому сайту. Вы также можете обеспечить обязательное ведение журнала независимо от того, какой дизайн сайта выбран.

## <a name="apply-a-site-design-to-the-default-site-designs"></a>Применение к стандартным дизайнам сайтов другого дизайна сайта

Чтобы настроить стандартные дизайны сайтов, примените новый дизайн с помощью командлета Powershell **Add-SPOSiteDesign** или REST API **CreateSiteDesign**. Укажите параметр **IsDefault**, чтобы применить дизайн сайта в качестве стандартного.

В приведенном ниже примере показано, как с помощью параметра **IsDefault** применить тему организации Contoso к стандартным дизайнам сайта. Скрипт сайта, на который можно ссылаться по ИД, содержит скрипт JSON для применения правильной темы.

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso company theme" `
  -WebTemplate "68" `
  -SiteScripts "89516c6d-9f4d-4a57-ae79-36b0c95a817b" `
  -Description "Applies standard company theme to site" `
  -IsDefault
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"Contoso company theme", Description:"Applies standard company theme to site", SiteScriptIds:["89516c6d-9f4d-4a57-ae79-36b0c95a817b"],  WebTemplate:"68", IsDefault: true}});
```

## <a name="which-default-site-designs-are-updated"></a>Какие стандартные дизайны сайта обновляются?

В предыдущем примере значение 68 для параметра **WebTemplate** относится к шаблону сайта SharePoint Online для общения. Этот шаблон содержит следующие дизайны сайта по умолчанию:

- "Тема";
- "Демонстрация";
- "Пустой".

Применяя новый дизайн сайта, вы одновременно обновляете все три дизайна сайта, используемые по умолчанию.

Шаблон сайта группы SharePoint Online содержит только один стандартный дизайн с именем **Группа**. В этом случае при применении стандартного дизайна сайта обновляется только дизайн сайта **Группа**.

## <a name="restoring-the-default-site-designs"></a>Восстановление стандартных дизайнов сайтов

Чтобы восстановить стандартный дизайн сайта, удалите примененный дизайн сайта. Если бы в предыдущем примере у созданного дизайна сайта был ИД db752673-18fd-44db-865a-aa3e0b28698e, его можно было бы удалить так, как показано в следующем примере.

```powershell
C:\> Remove-SPOSiteDesign db752673-18fd-44db-865a-aa3e0b28698e
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"db752673-18fd-44db-865a-aa3e0b28698e"});
```

> [!NOTE]
> Если вы не знаете, какой дизайн сайта используется по умолчанию, запустите командлет **Get-SPOSiteDesign**. Он перечислит все дизайны сайтов и укажет, какие из них стандартные.