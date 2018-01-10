---
title: "Общие сведения о макетах и скриптах сайтов SharePoint"
description: "Узнайте, как автоматизировать подготовку новых сайтов SharePoint с пользовательскими конфигурациями, используя скрипты и макеты сайтов SharePoint."
ms.date: 12/14/2017
ms.openlocfilehash: 5821c4a48ecccbfc23ff5eaaf1c7941c6026d06e
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="sharepoint-site-design-and-site-script-overview"></a>Общие сведения о макетах и скриптах сайтов SharePoint

> [!NOTE]
> Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены. Сейчас они не поддерживаются для использования в рабочих средах.

Узнайте, как автоматизировать подготовку новых сайтов SharePoint с собственными конфигурациями, используя макеты и скрипты сайтов. Когда пользователи в организации создают сайты SharePoint, часто требуется обеспечить некоторый уровень согласованности. Например, к каждому новому сайту может потребоваться применять надлежащий фирменный стиль и темы. Вы также можете использовать подробные скрипты подготовки сайтов (например, модуль подготовки PnP), которые должны применяться при создании каждого сайта. В этой статье описывается использование макетов и скриптов сайтов для создания пользовательских конфигураций, применяемых при создании сайтов.

## <a name="how-site-designs-work"></a>Как работают макеты сайтов

Макеты сайтов подобны шаблонам. Их можно использовать при создании сайтов, чтобы выполнять с ними одну и ту же последовательность действий. Как правило, большинство действий (например, установка темы или создание списков) влияет на сам сайт. Однако макет сайта также может включать другие действия, такие как запись URL-адреса нового сайта в журнал или отправка твита.

Вы можете создавать макеты сайтов и регистрировать их в SharePoint, используя один из современных шаблонов сайтов: сайт группы или сайт для общения. Ниже описывается, как это сделать.

1. Перейдите на домашнюю страницу SharePoint в клиенте разработчика.
1. Нажмите **Создать сайт**.

    Вы увидите два современных шаблона сайтов: **Сайт группы** и **Сайт для общения**.

1. Выберите **Сайт для общения**.

    На сайте общения есть поле **Выберите оформление**, где по умолчанию доступны следующие три макета:

    - "Статья";
    - "Демонстрация";
    - "Пустой".

Это стандартные макеты сайтов. У каждого макета сайта есть заголовок, описание и изображение.

![Стандартные заголовок, описание и изображение макета в шаблоне сайта для общения](images/site-designs-listed-on-communication-site-template.png)

Шаблон сайта группы содержит только один стандартный макет с именем **Сайт группы**. Дополнительные сведения о том, как можно изменить стандартные макеты сайта, см. в статье [Настройка стандартного макета сайта](customize-default-site-design.md).

После выбора макета сайта SharePoint создает новый сайт и выполняет скрипты для его макета. В скриптах сайта описываются такие задачи, как создание списков или применение темы. После выполнения действий из скриптов SharePoint выводит подробные сведения о результатах этих действий в области выполнения.

![Область выполнения со списком завершенных действий из макета сайта](images/progress-pane.png)

## <a name="anatomy-of-a-site-script"></a>Структура скрипта сайта

Скрипты сайтов — это JSON-файлы, в которых указывается упорядоченный список действий, выполняемых при создании сайта. Действия выполняются в указанном порядке. Ниже приведен пример скрипта с двумя действиями верхнего уровня. Сначала он применяет ранее созданную тему с именем **Contoso Explorers**. Затем он создает список **Customer Tracking**.

```json
{
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
}
```

Каждое действие в скрипте сайта задается с помощью значения **verb** в JSON. В предыдущем скрипте первое действие указывается с помощью команды **applyTheme**. Затем команда **createSPList** создает список. Обратите внимание, что команда **createSPList** содержит собственный набор команд, выполняющих дополнительные действия только со списком.

Доступны следующие действия:

- создание списка;
- применение темы;
- создание страницы;
- установка логотипа сайта;
- добавление навигации;
- запуск потока Microsoft Flow.

Скрипты сайта можно повторно запускать на том же сайте после подготовки. Это можно делать только программным способом. Скрипты сайтов являются неразрушающими, то есть при повторном запуске они гарантируют, что сайт соответствует конфигурации из скрипта. Например, если на сайте уже есть список с таким же именем, как у создаваемого скриптом, то скрипт только добавит недостающие поля в имеющийся список.

## <a name="using-powershell-or-rest-to-work-with-site-designs-and-site-scripts"></a>Работа с макетами и скриптами сайтов с помощью PowerShell или REST

Вы можете создавать макеты и скрипты сайтов с помощью PowerShell или REST API. В приведенном ниже примере создаются скрипт сайта и макет, использующий этот скрипт. <!-- The PowerShell example loads the script from a file, while the REST example has the script inline. -->

```powershell
C:\> Get-Content 'c:\scripts\site-script.json' `
     -Raw | `
     Add-SPOSiteScript `
    -Title "Contoso theme and list"

Id          : 2756067f-d818-4933-a514-2a2b2c50fb06
Title       : Contoso theme and list
Description :
Content     :
Version     : 0

C:\> Add-SPOSiteDesign `
  -Title "Contoso customer tracking" `
  -WebTemplate "64" `
  -SiteScripts "2756067f-d818-4933-a514-2a2b2c50fb06" `
  -Description "Creates customer list and applies standard theme"
```

<!-- 
```javascript
var site_script = {
  "$schema": "schema.json",
  "actions": [
    {
      "verb": "applyTheme",
      "themeName": "Contoso Explorers"
    },
    {
      "verb": "createSPList",
      "listName": "Customer Tracking",
      "templateType": 100,
      "subactions": [
        {
          "verb": "SetDescription",
          "description": "List of Customers and Orders"
        },
        {
          "verb": "addSPField",
          "fieldType": "Text",
          "displayName": "Customer Name",
          "isRequired": false,
          "addToDefaultView": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Number",
          "displayName": "Requisition Total",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "User",
          "displayName": "Contact",
          "addToDefaultView": true,
          "isRequired": true
        },
        {
          "verb": "addSPField",
          "fieldType": "Note",
          "displayName": "Meeting Notes",
          "isRequired": false
        }
      ]
    }
  ],
  "bindata": { },
  "version": 1
};

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteScript(Title=@title)?@title='Contoso theme and list'", site_script);

RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign",{
  info:{
    Title:"Contoso customer tracking", Description:"Creates customer list and applies standard theme",  SiteScriptIds:["607aed52-6d61-490a-b692-c0f58a6981a1"],  WebTemplate:"64"
   }
  });
```
-->

В предыдущем примере командлет **Add-SPOSiteScript** или REST API **CreateSiteScript** возвращает ИД скрипта сайта. Он используется для параметра **SiteScripts** в последующем вызове командлета **Add-SPO-SiteDesign** или REST API **CreateSiteDesign**.

Параметр **WebTemplate** со значением 64 указывает, что макет сайта регистрируется с шаблоном сайта группы. Значение 68 указывает на шаблон сайта для общения. Параметры **Title** и **Description** отображаются, когда пользователь просматривает макеты сайтов во время создания сайта группы.

> [!NOTE]
> Макет сайта может выполнять множество скриптов. Их идентификаторы передаются в массиве, а скрипты выполняются в указанном порядке.

Пошаговые инструкции по созданию макета сайта см. в статье [Начало создания макетов сайтов](get-started-create-site-design.md).

## <a name="pnp-provisioning-and-customization-using-microsoft-flow"></a>Подготовка PnP и настройка с помощью Microsoft Flow

Возможности скриптов сайтов включают вызов потока Microsoft Flow. Благодаря этому вы можете указать любое дополнительное действие помимо доступных по умолчанию.

Если для автоматизации создания сайта используется модуль подготовки PnP, то вы можете использовать поток Microsoft Flow для интеграции с макетами сайтов. С помощью этой методики вы можете сохранить все имеющиеся скрипты подготовки, а также создавать новые.

![процесс вызова потока Microsoft Flow](images/process-for-triggering-a-custom-flow.png)

Этот процесс описывается ниже.

1. Скрипт создает экземпляр потока Microsoft Flow, используя URL-адрес с дополнительными сведениями.
1. Поток отправляет сообщение в настроенную вами очередь службы хранилища Azure.
1. Сообщение вызывает настроенную вами функцию Azure.
1. Функция Azure выполняет пользовательский скрипт (например, модуль подготовки PnP), чтобы подготовить пользовательские конфигурации.

Пошаговое руководстве по настройке потока Microsoft Flow с помощью модуля подготовки PnP см. в статье [Создание полноценного макета сайта с помощью модуля подготовки PnP](site-design-pnp-provisioning.md).

## <a name="scoping"></a>Определение области

Вы можете настраивать макеты сайтов, чтобы они отображались только для определенных групп пользователей в организации. Это гарантирует, что пользователям видны только те макеты сайтов, которые для них предназначены. Например, отделу бухгалтерии будут доступны только соответствующие макеты. С другой стороны, макеты сайтов для бухгалтерии не понадобятся другим пользователям.

После создания макета сайта он по умолчанию виден всем пользователям. Области применяются с помощью командлета **Grant-SPOSiteDesignRights** или REST API **GrantSiteDesignRights**.  В качестве области можно указывать пользователей или группы безопасности, поддерживающие почту. В приведенном ниже примере показано, как добавить к макету сайта права просмотра для пользователя Nestor (на вымышленном сайте Contoso).

> [!div class="tabbedCodeSnippets"]
```powershell
Grant-SPOSiteDesignRights `
  -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
  -Principals "nestorw@contoso.onmicrosoft.com" `
  -Rights View
```

<!--
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.GrantSiteDesignRights", {id:"44252d09-62c4-4913-9eb0-a2a8b8d7f863", principalNames:["nestorw@contoso.onmicrosoft.com”], grantedRights:1});
```
-->
Дополнительные сведения о работе с областями см. в статье [Определение области доступа к макетами сайтов](site-design-scoping.md).

## <a name="see-also"></a>См. также

- [Приступая к созданию макетов сайтов](get-started-create-site-design.md)
- [Применение области к макету сайта](site-design-scoping.md)
- [Схема JSON для макета сайта](site-design-json-schema.md)
- [Командлеты PowerShell для макетов и скриптов сайтов SharePoint](site-design-powershell.md)
- [REST API макетов и скриптов сайтов](site-design-rest-api.md)
- [Примеры макетов сайта]((https://github.com/SharePoint/sp-dev-site-scripts))
