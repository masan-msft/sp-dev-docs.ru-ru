---
title: "Изолированная преобразования руководство по решениям для-приемников событий"
ms.date: 11/03/2017
ms.openlocfilehash: 1e49fa9b9afdb06eb9ea4ec09a866eccf703cbf7
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---event-receivers"></a>Изолированная преобразования руководство по решениям для-приемников событий 
Эта статья поможет вам определить параметры и стратегии на замена существующих приемников событий из изолированных решений.

_**Применимо к:** Add-ins for SharePoint | SharePoint 2013 | SharePoint 2016 | SharePoint Online_

SharePoint online и изолированной среды на основе кода решения, [рекомендуется использовать](https://blogs.msdn.microsoft.com/sharepointdev/2014/01/14/deprecation-of-custom-code-in-sandboxed-solutions/) обратно в 2014 г запущен процесс, чтобы полностью удалить эту возможность. На основе кода изолированных решений также являются устаревшими в SharePoint 2013 и в SharePoint 2016.

## <a name="summary"></a>Summary

Подхода, можно обрабатывать события в SharePoint немного отличаться в объектная модель SharePoint, от полного доверия кодом или в закодированные изолированные решения. В типичные предыдущей решения приемники событий были созданы с помощью объектной модели SharePoint Server со стороны и развернуты с помощью пакетов решений, который выполняет код на серверах SharePoint. Надстройки модели SharePoint; Тем не менее выполняет реализацию приемника событий на веб-сервере, на котором размещен приемника событий, и они называются удаленных приемников событий (RER). Приемники событий можно во многих случаях заменить реализацию приемника удаленных событий. В этой статье описываются различные аспекты, параметры и оформление.


## <a name="options-for-replacing-event-receivers"></a>Параметры для замены приемники событий
<a name="sectionSection2"> </a>

|**Подход**|**Дополнительные сведения**|
|:-----|:-----|
|Удаленный приемник событий|</p><lu><li>[Использование удаленных приемников событий в SharePoint](https://msdn.microsoft.com/en-us/pnp_articles/use-remote-event-receivers-in-sharepoint)</li><li>[Как использовать удаленные приемники событий для надстройки SharePoint](https://channel9.msdn.com/blogs/OfficeDevPnP/How-to-use-remote-event-receivers-for-your-SharePoint-add-ins)</li><li>[Приемники событий и приемников событий списка в объектная модель SharePoint](https://msdn.microsoft.com/en-us/pnp_articles/event-receiver-and-list-event-receiver-sharepoint-add-in)</li></lu><li>[Автоматическое тегов пример надстройки для SharePoint](https://msdn.microsoft.com/en-us/pnp_articles/autotagging-sample-app-for-sharepoint)</li><li>[Обработка событий в надстройках SharePoint](https://msdn.microsoft.com/en-us/library/office/jj220048.aspx)</li></lu></p>|
|WebHooks|<p>WebHooks для SharePoint стадии разработки и скоро будет доступен для предварительного просмотра.<lu><li>[Краткие сведения о SharePoint WebHooks](http://dev.office.com/blogs/introducing-sharepoint-webhooks)</li></p>
|Удаленные задания таймера для отслеживания изменений|<p>Используйте объект **ChangeQuery** мониторинг сайта или списка для изменения. Этот шаблон является альтернативой удаленных приемников событий<lu><li>[Монитор изменений элементов списка SharePoint](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ListItemChangeMonitor)</li><li>[Шаблон задания таймера удаленного](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)</p>|

## <a name="design-considerations"></a>Рекомендации по проектированию
### <a name="remote-event-receivers"></a>Удаленные приемники событий
- Требует инфраструктуры размещения.
- Инфраструктура размещения должен быть высокой доступности
- Конечная точка службы, на котором размещается в удаленный приемник событий должен быть настроен для анонимной проверки подлинности
- Требует доверенных сторонних производителей по сертификатам при использовании SharePoint Online
- Не предназначены для long выполнение операций 
- Удаленные приемники событий, присоединенные исходящей стороны контексте надстройки, присоединенные с помощью консольного приложения или PowerShell; не получит маркер контекста SharePoint при вызове и должны отличаться разрешения только для приложений или используйте класс SharePointOnlineCredentials
- Нельзя повторить 

### <a name="webhooks"></a>WebHooks
- Требует инфраструктуры размещения.
- Инфраструктура размещения должен быть высокой доступности
- Не поддерживает синхронные события
- Процесс изменения после возникновения события
- Общедоступный preview, недоступны в лето 2016 по SharePoint Online
- Недоступно в SharePoint в локальной построена на данный момент.

### <a name="remote-timer-job"></a>Задание таймера удаленного
- Требует инфраструктуры размещения.
- Процесс изменения после возникновения события
- Использовать механизм опроса для обработки изменений

## <a name="removing-your-sandbox-code-from-your-site"></a>Удаление изолированного кода с веб-узла
<a name="sectionSection3"></a>При отключении существующего изолированного решения из сайтов любого активы или файлы, развернутые с помощью декларативных параметров, удаляется тем не менее, функции в изолированном решении будут автоматически отключены и receiver(s) события будут удалены . 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>
-  [Удаление на основе кода изолированных решений в SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [Руководство по преобразованию изолированных решений](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [Удалить ссылку на сборку в решении изолированной среды, созданных в Visual Studio](https://support.microsoft.com/en-us/kb/3183084)
-  [Создание надстроек для SharePoint](https://msdn.microsoft.com/library/office/fp179930.aspx)
-  [Разработка для Office 365 и руководства решения SharePoint шаблоны и рекомендации](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance)
