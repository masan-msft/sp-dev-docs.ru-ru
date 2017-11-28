---
title: "Приемники событий и приемников событий списка в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: db3b316f7505805a1d8237477056419535cea89c
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="event-receivers-and-list-event-receivers-in-the-sharepoint-add-in-model"></a>Приемники событий и приемников событий списка в объектная модель SharePoint
=======================================================================

<a name="summary"></a>Summary
-------

Подхода, можно обрабатывать события в SharePoint будет разным в новой модели надстройки SharePoint не был с кодом полного доверия.  
В типичных полного доверия кода (FTC) / сценарий решения фермы, приемники событий и приемников событий списка были созданы с помощью объектной модели SharePoint Server со стороны кода и развернуты через решений.  В этом сценарии код приемника событий работает на сервере SharePoint.

В SharePoint надстройки модели сценарии приемники событий создаются за пределами SharePoint внутри веб-службы и зарегистрирован в SharePoint.  
Они называются как *Recivers удаленных событий (RER)*. В этом сценарии код приемника событий выполняется на веб-сервере где размещен веб-службы.

>**Важные** По состоянию на январь 2017 SharePoint Online поддерживает webhooks списка, который можно использовать вместо «-ed» удаленные приемники событий. Извлечение [webhooks Общие сведения о SharePoint](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) для получения дополнительных сведений о webhooks. Обратите внимание, что несколько примеров webhook доступны из репозитория репозиториев [sp dev примеры](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) .

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для создания приемников событий.

- Конечная точка службы, реализующего приемник событий должны быть доступны анонимным пользователям.
- Приемники событий добавлен к-сети можно восстановить маркер доступа.
- Приемники событий добавлен к хост-сети возвращает маркер доступа, если они применяются из контекста приложения с помощью маркера доступа приложения и операций на хост-сайте конечного пользователя, управляемых с помощью (ItemAdded и т.д.)
- Событие AppInstalled необходимо выполнить в течение 30 секунд или SharePoint будет считать, что не удалось выполнить. SharePoint будет повторно выполнить событие 3 раза и после выполнения четвертый SharePoint будут использоваться произошел сбой установки надстройки
- Обычный события как ItemAdded также имеют время ожидания 30 секунд, но нельзя повторить
- Приемники событий добавлен к веб-узла без контекста приложения, например с SharePointOnlineCredentials или другим способом не возвращает маркер доступа и вам придется для доступа к веб-сайт с маркером доступа только для приложений
- Добавление приемников событий к хост-сети поддерживается.
    + Только это можно сделать с помощью API-интерфейсы CSOM/REST, не с помощью мастеров Visual Studio.
- SharePoint абсолютно вызывает событие приемника конечных точек, настроенных для данного события.  Тем не менее нет гарантии, который будет выполняться код в конечные точки приемника событий, так как код не выполняется на сервере SharePoint.
    
    Например:
    
    Если URL-адрес конечной точки для приемника событий недоступен не будет выполняться код приемника событий.  URL-адрес может быть недоступна из-за ряду причин.  Перечислены некоторые из наиболее распространенных причин неправильной настройкой при завершении конечную точку регистрации URL-адрес, DNS проблемы при попытке сопоставить URL-адрес или веб-сайта, размещение конечную точку вниз или в состоянии из строя.

    Кроме того при наличии ошибки в код приемника событий плохо написанного нет возможности для уведомления SharePoint возникновения ошибки и события, которые должны выполняться еще раз.  Можно обойти это для определенной с приемниками событий, подключенного к спискам SharePoint.  Ниже приведены дополнительные сведения о такой подход.  
- Можно использовать при выполнении значительного объема кода приемника событий асинхронной модели.
    + В разделе следующие MSDN, блоге Дополнительные сведения об этом шаблоне. [С помощью хранилища Azure очереди и WebJobs для асинхронного действия в Office 365 (публикация в блоге MSDN)](http://blogs.msdn.com/b/vesku/archive/2015/03/02/using-azure-storage-queues-and-webjobs-for-async-actions-in-office-365.aspx)
    + В следующей статье MSDN Дополнительные сведения о времени ожидания в приемниках событий.  (Поиск времени ожидания в статье).  [Обработка событий в надстройках для SharePoint (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/jj220048.aspx)
- Когда приемников событий работают в списках SharePoint рекомендуется использовать определенные исправлений механизм, а также приемника событий для обеспечения высокого качества обработки.
    + В разделе O365 PnP следующий код Дополнительные сведения об этом шаблоне и его применение.  [Core.ListItemChangeMonitor (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ListItemChangeMonitor)


<a name="debugging-event-receivers"></a>Отладка приемников событий
-------------------------
Чтобы выполнить отладку приемников событий, необходимо настроить несколько различных аспектов в Azure и Visual Studio.  В следующих статьях предоставляются пошаговые инструкции и Дополнительные сведения, связанные с отладкой. 
- [Отладка и устранение неполадок удаленного приемника событий в надстройку для записи блога SharePoint MSDN)](https://msdn.microsoft.com/en-us/library/office/dn275975.aspx) 
- [Отладка удаленных приемников событий с помощью Visual Studio (публикация в блоге MSDN)](http://blogs.msdn.com/b/officeapps/archive/2013/01/03/debugging-remote-event-receivers-with-visual-studio.aspx)
- [Обновление для отладки удаленных событий SharePoint 2013 с помощью Visual Studio 2012 (публикация в блоге MSDN)](http://blogs.msdn.com/b/officeapps/archive/2013/03/21/update-to-debugging-sharepoint-2013-remote-events-using-visual-studio-2012.aspx)
- [Создание и отладки удаленного приемника событий «Установщик приложений» в SharePoint Online (Scott Хиллиер)](http://www.itunity.com/article/create-debug-remote-event-receiver-installer-apps-sharepoint-online-775)

<a name="more-examples"></a>Дополнительные примеры
-------------
- [Core.EventReceivers (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
    + Это пример hows как надстройки SharePoint установлено приложение событие используется для выполнения дополнительных работ в хост-сайта, например, присоединение приемников событий в списки на хост-сайте.
    + В разделе следующие MSDN, блоге Дополнительные сведения об этом шаблоне. [Прикрепление удаленных приемников событий в списки на хост-сайте (публикация в блоге MSDN)](http://blogs.msdn.com/b/kaevans/archive/2014/02/26/attaching-remote-event-receivers-to-lists-in-the-host-web.aspx)
- [Core.AppEvents.HandlerDelegation (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    + В этом примере показано, как реализовать обработчики для событий AppInstalled и AppUninstalling, который:
        1. Внедрение логики отката, если обработчик возникает ошибка.
        2. Внедрение логики «уже done» для учета того факта, что SharePoint повторов обработчик до трех раз если он не отвечает или занимает более 30 секунд.
        3. Используйте стратегию делегирования обработчик для минимизации вызовов из обработчика веб-службы в SharePoint.
        4. Использование классов CSOM ExceptionHandlingScope и ConditionalScope.
- [Core.AppEvents (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents)
    + В этом примере показано, как реализовать обработчики для событий AppInstalled и AppUninstalling, который:
        1. Внедрение логики отката, если обработчик возникает ошибка.
        2. Внедрение логики «уже done» для учета того факта, что SharePoint повторов обработчик до трех раз если он не отвечает или занимает более 30 секунд.

<a name="related-links"></a>Ссылки по теме
=============
- [Удаленные приемники событий в SharePoint 2013 вопросы и ответы (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn456315.aspx)
- [Создание удаленного приемника событий в надстройках для SharePoint (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/jj220043.aspx)
- [Создание приемника событий приложения в SharePoint 2013 (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/jj220052.aspx)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Core.ListItemChangeMonitor (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ListItemChangeMonitor)
- [Core.EventReceivers (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
- [Core.AppEvents.HandlerDelegation (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
- [Core.AppEvents (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents)
- Примеры и содержимое в https://github.com/SharePoint/PnP

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D) 
- SharePoint 2013 в локальной
