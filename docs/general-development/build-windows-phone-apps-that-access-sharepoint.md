---
title: "Создание приложений Windows Phone, обращающихся к SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 36681335-f772-4499-8445-f94481bc18e7
ms.openlocfilehash: 3187d51804a96627f38b2ec5f4320f7d356c1107
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="build-windows-phone-apps-that-access-sharepoint"></a>Создание приложений Windows Phone, обращающихся к SharePoint
Сведения о создании SharePoint Add-ins, интеграции SharePoint и мобильных устройств, такие как Windows Phone 8 и Windows Phone 7.
## <a name="introduction-to-building-mobile-apps-with-sharepoint"></a>Введение в создание мобильных приложений с помощью SharePoint
<a name="SP15mobileapp_intro"> </a>

SharePoint предоставляет замечательные возможности для разработчиков для создания мобильного приложения, которые передаются с пользователями, являются интерактивные и привлекательных и доступны всякий раз, когда и где это необходимо работать с ними пользователей. Вы можете сочетать приложений Windows Phone 8 и Windows Phone 7 с локальной службы SharePoint и приложения или удаленных SharePoint services и приложений, работающих в облаке (например, те, которые используют SharePoint Online) для создания мощных приложения, расширения функциональных возможностей за пределы традиционного рабочего стола и ноутбуков и в среде действительно портативных, так и намного более доступными.
  
    
    
Новые возможности мобильности, предоставляемые SharePoint, основанные на существующих Microsoft средства и технологии, такие как SharePoint, Windows Phone, Visual Studio и Silverlight. Разработчики, имеющие опыт работы с этими технологиями и их средства будет для создания на базе SharePoint мобильных приложений для Windows Phone без некоторого обучения. В этом разделе мы изучение некоторых типов мобильных приложений на базе SharePoint, можно создать для Windows Phone 8 и Windows Phone 7 и наиболее распространенные способы настройки этих приложений. SharePoint предоставляет платформу и средства для разработчиков, шаблоны проектов Visual Studio 2010, включая создание решений для мобильных устройств, которые взаимодействуют с данными SharePoint в локальных установок SharePoint и в облаке, используя SharePoint Online. На рисунке 1 показано, как может выглядеть приложение простого списка на Windows Phone.
  
    
    

**На рисунке 1. Элементы списка SharePoint в приложении Windows Phone**

  
    
    

  
    
    
![Элементы списка SharePoint в приложении Windows Phone](../images/9159345c-ce12-41a6-8994-fc2e9aa26fd6.gif)
  
    
    

  
    
    

  
    
    

## <a name="what-skills-do-you-need-to-create-mobile-apps"></a>Какие навыки работы необходимые для создания мобильных приложений?
<a name="SP15buildmobile_needtoknow"> </a>

В этом разделе предполагается, что вы знакомы с SharePoint, .NET Framework, система разработки Visual Studio и Visual C#. Также полезно некоторые сравнению с Windows Phone 8 или Windows Phone 7 при разработке приложений с Silverlight и приводятся рекомендации по можно ознакомиться с XAML, StackPanel и Pivot элементы управления для Windows Phone и основные понятия, такие как деактивация, привязка данных Silverlight и т. д. Если вы не знакомы с помощью Silverlight при разработке приложений Windows Phone, рекомендуется ознакомиться со следующими ресурсами.
  
    
    

-  [Разработка Windows Phone приложения от начала до конца](http://msdn.microsoft.com/en-us/library/gg680270%28v=pandp.11%29.aspx)
    
  
-  [Пользовательский интерфейс для Windows Phone](http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff967556%28v=vs.105%29.aspx)
    
  
-  [Краткое руководство: Создание пользовательского интерфейса с помощью XAML для Windows Phone](http://msdn.microsoft.com/en-us/library/windowsphone/develop/jj207025%28v=vs.105%29.aspx)
    
  
-  [Архитектура управления PIVOT для Windows Phone](http://msdn.microsoft.com/en-us/library/windowsphone/develop/ff941097%28v=vs.105%29.aspx)
    
  

## <a name="development-overview-for-mobile-apps-using-sharepoint"></a>Общие сведения о разработке для мобильных приложений с помощью SharePoint
<a name="SP15buildmobile_devoverview"> </a>

Может создавать широкий спектр мобильных приложений с помощью SharePoint. В этом разделе описаны новые или измененные выпуска SharePoint, с помощью простого разработки мобильных приложений для разработчиков.
  
    
    

### <a name="windows-phone-sharepoint-application-template"></a>Шаблон приложения SharePoint для Windows Phone

Это простой тип мобильного приложения, которые вы можете создать для переноса регулярного списка на номер телефона. SharePoint предоставляет шаблон Visual Studio, чтобы обеспечить возможность быстро и легко создавать приложения списка SharePoint для Windows Phone. Например, можно создать «Список дел»-введите приложения Windows Phone, которое возвращает список задач из SharePoint в Windows Phone и позволяет использовать телефон для обновления состояния задач в дороге. Другой пример возникли каталог продуктов для список в SharePoint, доступные на телефоне для сотрудников отдела продаж. Установка пакета SDK SharePoint для Windows Phone предоставляет два шаблоны Windows Phone приложений SharePoint в Visual Studio 2010 или Visual Studio 2010 Express для Windows Phone. (Увидеть [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) На основе шаблона приложения списка SharePoint для Windows Phone, можно следуйте указаниям мастера для создания приложения Windows Phone с работы, которые можно получить доступ к и работы с данными в списке SharePoint.
  
    
    

### <a name="new-and-enhanced-mobility-object-model-in-sharepoint"></a>Новые и усовершенствованные мобильности объектная модель в SharePoint

SharePoint добавляет несколько новых классов на сервере и клиентских объектных моделей, чтобы включить сценарии мобильности SharePoint, которые мы описано ранее в этой статье.
  
    
    
Чтобы включить приложений с поддержкой местоположения, существует новые собственные класс типа поля, **SPFieldGeoLocation**вместе с несколькими связанные с ним классы для структурирования значение поля расположения и отображения их. Эти классы можно также вызвать в клиентской объектной модели SharePoint для Silverlight. Новый тип поля также есть определение добавляемого стандартных файла fldtypes.xml SharePoint и новые пользовательские элементы управления для отображения поля в формах отображения, редактирования и создания. Общие сведения в разделе [Интеграция расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md). 
  
    
    
Для включения проверки подлинности SharePoint для пользователей Windows Phone, клиентская объектная модель содержит несколько связанных классов и новый класс **проверки подлинности** . Дополнительные сведения см [Обзор объектной модели SharePoint мобильного клиента проверки подлинности](overview-of-the-sharepoint-mobile-client-authentication-object-model.md).
  
    
    
Чтобы включить автоматическое уведомлений для пользователей Windows Phone событий в ферме SharePoint, серверной объектной модели включает несколько новых классов, каждый из которых также может быть вызван из клиентской объектной модели. Эти классы содержат методы, позволяющие телефона приложений для регистрации для уведомлений об указанных типов событий приложений SharePoint server. Существуют также методы, которые используют серверные приложения для отправки уведомления о зарегистрированных подписчикам. Обзор перейдите в раздел [Create приложения списка SharePoint для Windows Phone для приема push-уведомлений](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md#BKMK_NotificationPhoneApp).
  
    
    
С помощью SharePoint можно не только для разработки мобильных приложений для Windows Phone 8 и Windows Phone 7. С программирования интерфейс и новых представлений состояния (REST) интерфейс программирования предоставлено SharePoint JavaScript можно создавать приложения для мобильных устройств, отличных от Windows Phone; могут взаимодействовать с сайтами SharePoint, используя JavaScript, который выполняется в качестве скрипты в браузере или удаленно с помощью любая технология, которая поддерживает стандартные возможности REST. Следующий раздел Обзор программных интерфейсов REST и JavaScript.
  
    
    

#### <a name="ecmascript-javascript-jscript-object-model-architecture"></a>Архитектура объектной модели ECMAScript (JavaScript, JScript)

SharePoint Foundation 2010 представлено клиентских объектных моделей, которые включены разработчиков выполнение удаленной связи с SharePoint с помощью веб-программирования технологии выбранного: .NET Framework, Silverlight и JavaScript.
  
    
    
В SharePoint Foundation 2010 клиентских объектных моделей предоставляют API, которые позволяют разработчикам взаимодействовать с сайтами SharePoint из скрипта, который выполняется в браузере, из кода (на основе .NET Framework 3.5 или более поздней версии), который выполняется в .NET Framework управляемых приложений или из кода, выполняющегося в приложении Silverlight 2.0. Прокси-сервер с расширением js и управляемых DLL-файлы, которые составляют объектные модели клиента основанные на веб-службы client.svc и обработки эффективной сериализации пакетной обработки, запросов и синтаксический анализ для ответов. На рисунке 2 показана высокоуровневая архитектура клиентских объектных моделей SharePoint.
  
    
    

**На рисунке 2. Архитектура объектной модели клиента SharePoint**

  
    
    

  
    
    
![Архитектура клиентских объектных моделей SharePoint](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig3.png)
  
    
    
Чтобы сведения об использовании клиентской объектной модели JavaScript с данными SharePoint, перейдите в раздел  [ECMAScript клиентской объектной модели](http://channel9.msdn.com/learn/courses/SharePoint2010Developer/ClientObjectModel/ECMAScriptClientObjectModel)
  
    
    

#### <a name="rest-endpoints-in-sharepoint"></a>Конечные точки REST в SharePoint

Чтобы использовать возможности REST, которые встроены в SharePoint, можно создать RESTful HTTP-запросов с использованием стандарта Open Data Protocol (OData), соответствующий API желаемую клиентской объектной модели. Веб-службы client.svc обрабатывает HTTP-запрос и обслуживает соответствующий ответ в формате Atom или JavaScript Object Notation (JSON). Затем клиентское приложение должно проанализировать этот отклик. На рисунке 3 показано высокоуровневое представление архитектуры SharePoint REST.
  
    
    

**На рисунке 3. Архитектура SharePoint REST**

  
    
    

  
    
    
![Архитектура REST SharePoint](../images/SP15Con_BuildSharePointAppsForMobileDevices_Fig2.png)
  
    
    
На данный момент службы REST в SharePoint доступен только для чтения. То есть доступны только конечные точки REST, которые представляют операции HTTP GET
  
    
    
По умолчанию ответы службы SharePoint REST форматируются с помощью протокола Atom спецификации OData. Кроме того служба REST поддерживает заголовков HTTP Accept, которые позволяют разработчикам указать, что ответ возвращается в формате JSON. Для получения дополнительных сведений о служб REST в SharePoint, видеть [операции запросов OData используется в запросах SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx).
  
    
    
Службы SharePoint REST поддерживает следующие операторы запросов OData.
  
    
    

- Фильтр
    
  
- Перевод
    
  
- expand
    
  

## <a name="start-developing-mobile-apps-for-sharepoint"></a>Начало разработки мобильных приложений для SharePoint
<a name="SP15buildmobile_start"> </a>

Следующие руководства и обзоры подробно определенные сведения, необходимые для разработки мобильных приложений:
  
    
    

-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Обзор шаблонов приложений Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md)
    
  
-  [Архитектура шаблона приложения списка SharePoint для Windows Phone](architecture-of-the-windows-phone-sharepoint-list-application-template.md)
    
  
-  [Как: Создание приложения списка Windows Phone SharePoint](how-to-create-a-windows-phone-sharepoint-list-app.md)
    
  
-  [Как: хранения и извлечения SharePoint списка элементов на ОС Windows Phone](how-to-store-and-retrieve-sharepoint-list-items-on-a-windows-phone.md)
    
  
-  [Как: реализация бизнес-логики и данных проверок в приложении Windows Phone для SharePoint](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md)
    
  
-  [Как: поддержка и convert SharePoint полей типов для приложения для Windows Phone](how-to-support-and-convert-sharepoint-field-types-for-windows-phone-apps.md)
    
  
-  [Как: Настройка запросов элементов списка и фильтрация данных для приложения для Windows Phone](how-to-customize-list-item-queries-and-filter-data-for-windows-phone-apps.md)
    
  
-  [Как: Настройка пользовательского интерфейса приложения списка SharePoint для Windows Phone](how-to-customize-the-user-interface-of-a-sharepoint-list-app-for-windows-ph.md)
    
  
-  [Способ: использование нескольких SharePoint спискам в приложении Windows Phone](how-to-use-multiple-sharepoint-lists-in-a-windows-phone-app.md)
    
  
-  [Как: Настройка и использование push-уведомлений в SharePoint приложений для Windows Phone](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [Интеграция расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [Как: Создание мобильных приложений в SharePoint, содержащую данные из внешнего источника данных](how-to-create-a-mobile-app-in-sharepoint-that-contains-data-from-an-externa.md)
    
  
-  [Как: интеграция карт с помощью приложения для Windows Phone и списки SharePoint](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [Как создавать ориентированные на поиск мобильные приложения с интерфейсами навигации и ведения журнала событий REST](how-to-build-search-driven-mobile-apps-with-the-navigation-and-event-logging-res.md)
    
  

## <a name="see-also"></a>См. также
<a name="SP15buildmobile_addlresources"> </a>


  
    
    

-  [Модели программирования в SharePoint](programming-models-in-sharepoint.md)
    
  
-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  
-  [О Expression Blend](http://msdn.microsoft.com/en-us/library/cc296376%28Expression.40%29.aspx)
    
  

