---
title: "Составные бизнес-приложений для SharePoint 2013 и SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 73bd4b9fd9d37cd72271cdce38320c8fdb3c67eb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="composite-business-apps-for-sharepoint-2013-and-sharepoint-online"></a>Составные бизнес-приложений для SharePoint 2013 и SharePoint Online

Использование составных бизнес-приложений для интеграции решений SharePoint с бизнес-процессами и технологиями. Решите, следует ли размещенных в SharePoint или размещением у поставщика надстройки с правильным выбором для решения.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Составные бизнес-приложений, приложений, полная интеграция с бизнес-процессов и технологий бизнес (LOB) (например, базы данных и веб-служб). Эти приложения обычно включают количество сложного взаимодействия с пользователями и с другими технологиями.
Пример составного бизнес-приложений, описанных в данном разделе предоставляют стандартные блоки, которые можно использовать для интеграции технологии и процессы, используемые с объектная модель SharePoint 2013.

## <a name="sharepoint-hosted-vs-provider-hosted-add-ins"></a>Размещение в SharePoint или размещением у поставщика надстройки
<a name="sectionSection0"> </a>

Перед созданием составного бизнес-приложений, необходимо сначала определить размещение приложений. Размещение в SharePoint надстроек лучше работают при из области действия требований к реализации одним сайтом, которые можно обрабатывать с помощью JavaScript. Размещение у поставщика надстроек подходят для более сложных бизнес-требований.

В следующей таблице перечислены факторы, которые необходимо учитывать при выборе места для размещения приложений.

|**Размещение в SharePoint надстроек**|**Размещение у поставщика надстроек**|
|:-----|:-----|
|Это можно сделать все, что необходимо сделать с помощью JavaScript.|Необходимо использовать языках, отличных от JavaScript.|
|Надстройка не нужно работать на нескольких сайтах; к примеру группы календаря приложения и основные новости rotators.|Надстройки требуется доступ к информации и работать в более чем одного сайта. Например веб-сайтов семейства подготовки приложения.|
|Содержимое конфиденциальных и должно быть в курсе безопасно и полностью в SharePoint.|Надстройки необходимо интегрировать с другими бизнес-технологиями.|
||Надстройки требуется повышенным уровнем разрешений, которые возможно с помощью политики только для приложений.|
||Надстройки требуется настраиваемых пользовательского интерфейса.|

## <a name="in-this-section"></a>В этом разделе:
<a name="sectionSection1"> </a>

|**Статья**|**Пример**|**Показано, как для...**|
|:-----|:-----|:-----|
|[Перенос форм InfoPath в SharePoint 2013](Migrate-InfoPath-forms-to-SharePoint.md) ||Перенос форм InfoPath 2013 для других поддерживаемых технологий.|
|[Варианты хранения данных в SharePoint Online](Data-storage-options-in-SharePoint-Online.md) |[Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) |Использование различных типов моделей хранилища для хранения данных SharePoint Online.|
|[Корпоративный события надстройки интеграции с SharePoint](Corporate-app-event-registration-with-SharePoint.md)|[BusinessApps.CorporateEventsApp](https://github.com/SharePoint/PnP/tree/master/Solutions/BusinessApps.CorporateEventsApp)|Используйте размещение у поставщика в надстройке для реализации сложных бизнес-задач.|
|[Вызов веб-служб из рабочих процессов SharePoint](Call-web-services-from-SharePoint-workflows.md)|<p>[Workflow.CallCustomService](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)</p><p>[Workflow.CallServiceUpdateSPViaProxy](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)</p><p>[Workflow.AssociateToHostWeb](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.AssociateToHostWeb)</p>|Используйте автоматически размещаемых приложениях для вызова удаленной веб-служб, которые содержат бизнес-данных.|

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Шаблоны и рекомендации по разработке решений для Office 365 на сайте GitHub](https://github.com/SharePoint/PnP)
