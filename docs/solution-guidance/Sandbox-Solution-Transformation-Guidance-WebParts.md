---
title: "Изолированная преобразования руководство по решениям для-веб-частей"
ms.date: 11/03/2017
ms.openlocfilehash: 3c93765118827db986e0830dba870aee6002eeb1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="sandbox-solution-transformation-guidance---web-parts"></a>Изолированная преобразования руководство по решениям для-веб-частей
Преобразования или преобразования на основе кода изолированных решений в объектная модель SharePoint. Сведения о стратегии преобразования существующей функциональности объектная модель SharePoint или альтернативных решений и параметры.

_**Применимо к:** Add-ins for SharePoint | SharePoint 2013 | SharePoint 2016 | SharePoint Online_


## <a name="summary"></a>Summary

Одной из причин, многие разработчики выполнять на основе кода изолированных решений является желание использовать визуальных веб-частей. Это обеспечивает отличный способ для отделения кода из макета, а также использовать элементы управления ASP.net. Конечно, могут продолжить использовать визуальных веб-частей в надстройке размещением у поставщика с помощью клиента веб-частей. Это отличный способ, предоставляет способ прямой миграции для многих приложений.

Другой способ — обновленной версии веб-части, как решение со стороны клиента. Это будет включать в себя модернизация решения для использования JavaScript, фрагментов HTML и один или несколько вспомогательных платформы. Хотя это net новый рабочий имеет дополнительную настройку решения легко интегрировать в предстоящие среды SharePoint. Это отлично подходит для простого отображения или ввода данных веб-части, можно вертикальное масштабирование целую страницу клиентских приложений.


## <a name="options-for-replacing-web-parts"></a>Параметры для замены веб-частей
<a name="sectionSection2"> </a>

|**Подход**|**Дополнительные сведения**|
|:-----|:-----|
|Веб-часть клиента надстройки размещением у поставщика|<ul><li>[Знакомство с созданием надстроек SharePoint с размещением у поставщика](https://msdn.microsoft.com/en-us/library/office/fp142381.aspx)</li><li>[Создание веб-частей надстройки для установки совместно с надстройкой для SharePoint](https://msdn.microsoft.com/en-us/library/a2664289-6c56-4cb1-987a-22367fad55eb)</li><li>[Схема определения части Web клиента](https://msdn.microsoft.com/en-us/library/office/dn481208.aspx)</li><li>[Настройка локальной среды разработки надстроек SharePoint](https://msdn.microsoft.com/en-us/library/office/fp179923.aspx)</li></ul>|
|Решение со стороны клиента|<ul><li>[Пример простой также реагирование формы](https://github.com/SharePoint/PnP/tree/dev/Samples/SharePoint.React.SupportTicket)</li><li>[Примеры внедрения JavaScript](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScript)[*](#actionsupportnote)</li><li>[Основные JS шаблоны и рекомендации](https://github.com/SharePoint/PnP-JS-Core/)</li></ul>|


## <a name="design-considerations"></a>Рекомендации по проектированию

### <a name="provider-hosted-add-in"></a>Надстройка размещением у поставщика

<ul>
<li>Требует инфраструктуры размещения.</li>
<li>Инфраструктура размещения должен быть высокой доступности</li>
<li>Клиентская часть отображается в iframe ограничения связи с остальной части страницы</li>
<li>Необходимо использовать API удаленного или с помощью REST или CSOM</li>
</ul>

### <a name="client-side-solution"></a>Решение со стороны клиента

<ul>
<li>
<a name="actionsupportnote"></a>Обратите внимание, что возможность внедрения JavaScript, как предписанный (за счет UserCustomAction) не работает в данный момент за пределами классический качества. В этих случаях можно связать файлы с помощью веб-части редактора скрипта.</li>
<li>Не удается повысить уровень разрешений, вместо этого используйте micro-service с только разрешения</li>
<li>Ограничивается объемом разрешения текущего пользователя</li>
</ul>


## <a name="removing-your-sandbox-code-from-your-site"></a>Удаление изолированного кода с веб-узла
<a name="sectionSection3"></a> При отключении существующего изолированного решения из сайтов любого активы или файлы, развернутые с помощью декларативных параметров, удаляется тем не менее, функции в изолированном решении будут автоматически отключены и будут приемника событий удалены.


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>
-  [Удаление на основе кода изолированных решений в SharePoint Online](http://dev.office.com/blogs/removing-code-based-sandbox-solutions-in-sharepoint-online)
-  [Руководство по преобразованию изолированных решений](https://msdn.microsoft.com/en-us/pnp_articles/sandbox-solution-transformation-guidance)
-  [Удалить ссылку на сборку в решении изолированной среды, созданных в Visual Studio](https://support.microsoft.com/en-us/kb/3183084)
-  [Создание надстроек для SharePoint](https://msdn.microsoft.com/library/office/fp179930.aspx)
-  [Разработка для Office 365 и руководства решения SharePoint шаблоны и рекомендации](https://msdn.microsoft.com/en-us/pnp_articles/office-365-development-patterns-and-practices-solution-guidance)
