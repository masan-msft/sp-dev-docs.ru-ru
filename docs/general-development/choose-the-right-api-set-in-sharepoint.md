---
title: "Выбор правильного набора API в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f36645da-77c5-47f1-a2ca-13d4b62b320d
ms.openlocfilehash: 2cfe9766b0a765fc3ca2abedfa91c92f6db7b9b1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="choose-the-right-api-set-in-sharepoint"></a>Выбор правильного набора API в SharePoint
Сведения о нескольких наборах API, включенных в SharePoint, в том числе для серверной объектной модели, различных клиентских объектных моделей и веб-службы REST или OData.
    
    

## <a name="factors-that-determine-which-api-set-to-use"></a>Факторы, определяющие, какой набор API нужно использовать
<a name="Factors"> </a>

Доступ к платформе SharePoint можно получить с помощью нескольких наборов интерфейсов API. Какой из них использовать, зависит от следующих факторов:
  
    
    

- **Тип приложения.** Можно использовать, помимо прочего, следующие не взаимоисключающие типы: Надстройка SharePoint, веб-часть на странице SharePoint, приложение Silverlight, которое запускается на клиентском компьютере или клиентском мобильном устройстве, приложение ASP.NET, которое представлено в SharePoint благодаря IFrame, код JavaScript, который выполняется на странице веб-сайта SharePoint, страница приложения SharePoint, приложение Microsoft .NET Framework, которое выполняется на клиентском компьютере, сценарий Windows PowerShell и задание таймера, которое выполняется на сервере SharePoint.
    
  
- **Ваши навыки.** Вы удивитесь, но в SharePoint можно создавать приложения, не вникая особо в программирование для SharePoint. Можно сразу приступить к разработке приложений для SharePoint, имея опыт работы с одной из следующих моделей программирования:
    
  - JavaScript
    
  
  - ASP.NET
    
  
  - REST или OData
    
  
  - .NET Framework
    
  
  - Windows Phone
    
  
  - Silverlight
    
  
  - Windows PowerShell
    
  
- **Устройство, на котором выполняется код.** Можно использовать сервер фермы SharePoint, внешний сервер (например, облачный сервер), клиентский компьютер и мобильное устройство.
    
  
В этом разделе предлагается обзор различных наборов интерфейсов API, предоставляемых в SharePoint. На рисунке 1 показано, какие наборы интерфейсов API можно использовать для разработки каждого из 13 стандартных приложений для SharePoint. В большинстве случаев для этого доступны несколько интерфейсов API.
  
    
    

**Рисунок 1. Выбранные типы расширений SharePoint и наборы интерфейсов API для SharePoint**

  
    
    

  
    
    
![Диаграмма Венна наборов API и типов приложений SharePoint](../images/SharePointAPIsetsandselectedSharePointextensions.png)
  
    
    

  
    
    
В таблице ниже представлены рекомендации о том, какой набор API использовать для списка выбранных стандартных проектов расширений SharePoint. В оставшихся разделах статьи описаны различные наборы интерфейсов API.
  
    
    


|**Что нужно сделать**|**Какой интерфейс API подойдет**|
|:-----|:-----|
|Создать веб-приложение ASP.NET, выполняющее операции создания, чтения, обновления и удаления (CRUD) данных SharePoint или внешних данных, подключаемых в SharePoint через внешний тип контента Службы Microsoft Business Connectivity Services (BCS), с использованием брандмауэра.  <br/> |Клиентская объектная модель JavaScript.  <br/> |
|Создать веб-приложение ASP.NET, выполняющее операции CRUD с данными SharePoint или внешними данными, подключаемыми в SharePoint с использованием внешнего типа контента BCS, не вызывая SharePoint через брандмауэр.  <br/> |Клиентская объектная модель .NET Framework или Silverlight, а также конечные точки REST или OData.  <br/> |
|Создать веб-приложение LAMP, выполняющее операции CRUD с данными SharePoint или внешними данными, подключаемыми в SharePoint с использованием внешнего типа контента BCS.  <br/> |Конечные точки REST или OData.  <br/> |
|Создать приложение для Windows Phone, выполняющее операции CRUD с данными SharePoint.  <br/> |Клиентская объектная модель для мобильных устройств.  <br/> |
|Создать приложение для Windows Phone, использующее службу push-уведомлений (Майкрософт), чтобы оповещать мобильное устройство о событиях в SharePoint.  <br/> |Клиентская объектная модель для мобильных устройств и серверная объектная модель.  <br/> |
|Создать приложение для iOS или Android, выполняющее операции CRUD с данными SharePoint.  <br/> |конечные точки REST и OData;  <br/> |
|Создать приложение .NET Framework, выполняющее операции CRUD с данными SharePoint.  <br/> |Клиентская объектная модель .NET Framework.  <br/> |
|Создать приложение Silverlight, выполняющее операции CRUD с данными SharePoint.  <br/> |Клиентская объектная модель Silverlight  <br/> |
|Создать приложение HTML или JavaScript, выполняющее операции CRUD с данными SharePoint.  <br/> |Клиентская объектная модель JavaScript.  <br/> |
|Создать Надстройка Office, совместимое с SharePoint.  <br/> |Клиентская объектная модель JavaScript.  <br/> |
|Создать пользовательскую команду Windows PowerShell.  <br/> |Объектная модель сервера  <br/> |
|Создать задание таймера.  <br/> |Серверная объектная модель.  <br/> |
|Создать расширение центра администрирования.  <br/> |Серверная объектная модель.  <br/> |
|Создать единую фирменную символику для всей ферме SharePoint.  <br/> |Объектная модель сервера  <br/> |
|Создать пользовательскую веб-часть, страницу приложения или пользовательский элемент управления ASP.NET.  <br/> |Серверная объектная модель  <br/> **Важно!** Если функции, которые вы планируете предложить клиентам, не рассчитаны на администрирование с помощью SharePoint за пределами семейства веб-сайтов, то вместо использования серверной объектной модели рекомендуем создать надстройку SharePoint, включающую удаленное веб-приложение ASP.NET с необходимыми настраиваемыми веб-частями и пользовательскими элементами управления. Обратите внимание на первые две строки этой таблицы.           |
   

## <a name="server-object-model"></a>Серверная объектная модель
<a name="ServerOM"> </a>

Серверная объектная модель управляемых классов содержит самый большой набор интерфейсов API. На уровне SharePoint Foundation 2013 в ее состав входят классы и элементы, обеспечивающие программный способ управления базовым сайтом, и структура списка SharePoint Foundation. Большая часть этих классов находится в пространстве имен  [Microsoft.SharePoint](https://msdn.microsoft.com/library/Microsoft.SharePoint.aspx) . Кроме того, с помощью серверной объектной модели можно расширить возможности практически каждого компонента SharePoint Foundation, в том числе рабочих процессов, оповещений, веб-частей, базового поиска и Службы Microsoft Business Connectivity Services (BCS). Серверная объектная модель также содержит расширенный набор интерфейсов API, чтобы обеспечить расширение возможностей системы администрирования и безопасности SharePoint Foundation, в том числе резервного копирования, диагностики работоспособности фермы, ведения журнала, управления веб-приложениями и фермой, обновления версии, развертывания, кэширования и настройки Windows PowerShell.
  
    
    
На уровне SharePoint добавляется намного больше классов для программирования управления корпоративным информационным содержимым (ECM), профилей пользователей, таксономии, расширенного поиска и других функций SharePoint.
  
    
    
Можно использовать  [LINQ to Objects](http://msdn.microsoft.com/en-us/library/bb397919.aspx), чтобы отправлять запросы к любой коллекции **IEnumerable**, но  [Поставщик LINQ to SharePoint](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx) позволяет отправлять прямые запросы к спискам в базах данных контента SharePoint. Строго говоря, этот поставщик недоступен в случае любого другого набора интерфейсов API, упомянутого в этой статье. Но использование синтаксиса LINQ возможно с большинством других наборов.
  
    
    
Сборки, определяющие встроенные серверные классы, устанавливаются в глобальный кэш сборок каждого сервера при установке SharePoint. Когда программирование выполняется для серверной объектной модели, сборки устанавливаются как решения ферм в глобальный кэш сборок.
  
    
    

> **Примечание.** Вместо новых изолированных решений в SharePoint теперь рекомендуется разрабатывать надстройки SharePoint, но изолированные решения все еще можно устанавливать в семействах веб-сайтов в SharePoint. Сборки этих решений остаются в пакете, пока они не используются. При использовании они временно устанавливаются в папке на сервере. Дополнительные сведения см. в статье [Где развертываются сборки изолированных решений?](http://msdn.microsoft.com/library/dadbb20b-1bf7-442c-9eeb-bd9f01dbda45%28Office.15%29.aspx). 
  
    
    


### <a name="limitations-on-when-you-can-use-the-server-object-model"></a>Ограничения на использование серверной объектной модели

Настраиваемая логика Надстройки SharePoint всегда распространяется "вниз" (к клиенту), "вверх" (в облако) или "через" (к определенному серверу, не входящему в ферму SharePoint). Во всех этих моделях распространения необходимо использовать одну из клиентских объектных моделей либо конечные точки REST или OData. (Вы не можете использовать серверную объектную модель в Надстройка SharePoint.) Например, если приложение содержит страницы с размещением в SharePoint, они могут получать доступ к данным SharePoint с помощью клиентской объектной модели JavaScript. На таких страницах также могут быть представлены приложения Silverlight, использующие клиентскую объектную модель Silverlight SharePoint. Дополнительные сведения о Надстройки SharePoint см. в статье  [Важные аспекты архитектуры и разработки надстройки SharePoint](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx).
  
    
    

## <a name="client-object-models-for-managed-code"></a>Клиентские объектные модели для управляемого кода
<a name="ClientManagedOM"> </a>

В SharePoint используются три клиентские объектные модели для управляемого кода: Silverlight, .NET и модель для мобильных устройств.
  
    
    

### <a name="net-client-object-model"></a>Клиентская объектная модель .NET

Объектная модель SharePoint для .NET Framework используется в приложениях .NET Framework, которые работают с клиентом Windows, отличном от телефона. Таким клиентом можно считать любое из следующих устройств:
  
    
    

- компьютер пользователя;
    
  
- сервер, не входящий в ферму SharePoint;
    
  
- веб-роль или рабочая роль в Microsoft Azure;
    
  
Практически каждому классу на основном сайте и в объектной модели сервера списков соответствует класс в клиентской объектной модели .NET Framework. Кроме того, клиентская объектная модель .NET Framework предоставляет полный набор API для расширения других компонентов, включая некоторые функции SharePoint, например ECM, таксономию, профили пользователей, расширенный поиск, аналитика, службы BCS и другие.
  
    
    
Для повышения производительности строки кода, написанные с помощью клиентской объектной модели .NET Framework, отправляются на сервер SharePoint в виде пакетов. Там эти строки преобразовываются в серверный код, который выполняется. Затем запрашиваемые результаты и информация о новом состоянии всех переменных возвращаются клиенту. Как разработчик вы определяете, будет ли код пакета выполняться синхронно или асинхронно. (В случае синхронного выполнения приложение .NET Framework сначала подождет, пока будут возвращены результаты с сервера. При асинхронном выполнении сразу же продолжится обработка на стороне клиента, а пользовательский интерфейс не перестанет отвечать.)
  
    
    
Чтобы запрашивать любой объект **IEnumerable**, в том числе объекты SharePoint, которые реализуют **IEnumerable**, вы можете использовать синтаксис запросов LINQ в клиентском коде. Но для этого необходимо использовать  [LINQ to Objects](http://msdn.microsoft.com/en-us/library/bb397919.aspx), а не  [поставщик LINQ to SharePoint](http://msdn.microsoft.com/library/3fa2dc5f-d308-4337-aefd-191a5df8dbbe%28Office.15%29.aspx), так как документация последнего не подходит для клиентского кода.
  
    
    
Сборки для клиентской объектной модели .NET Framework должны устанавливаться на клиенте. Они входят в состав распространяемого пакета, который можно получить на странице  [Клиентские компоненты SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35585).
  
    
    
Примеры использования объектной модели .NET Framework см. в статье [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx).
  
    
    

> **Примечание.** Вы также можете использовать конечные точки SharePoint REST или OData в приложении .NET Framework. Сравнение клиентской объектной модели .NET Framework с конечными точками SharePoint REST и OData представлено в разделе [Конечные точки REST и OData](#RESTOData) далее в этой статье.
  
    
    


### <a name="silverlight-client-object-model"></a>Клиентская объектная модель Silverlight

Объектная модель SharePoint для Silverlight используется в приложениях Silverlight независимо от места сохранения компилированного XAP-файла. Это может быть библиотека на веб-сайте SharePoint, на клиентском компьютере, в облачном хранилище или на внешнем сервере. Обычно приложение Silverlight подключается в SharePoint в объекте  [SilverlightWebPart](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebPartPages.SilverlightWebPart.aspx) . Клиентская объектная модель Silverlight в SharePoint практически идентична клиентской объектной модели .NET Framework и предусматривает поддержку тех же областей расширений. Главное отличие состоит в том, что в версии Silverlight все пакеты команд отправляются на сервер асинхронно, чтобы элементы пользовательского интерфейса приложения оставались активны.
  
    
    
Сборки для клиентской объектной модели Silverlight сохраняются на каждом сервере SharePoint в папке %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. Их не нужно устанавливать на компьютер, на котором установлено приложение Silverlight, хотя это предусмотрено. Кроме того, вы их можете сохранить в XAP-файл приложения.
  
    
    
XAP-файлы Silverlight можно включить в Надстройки SharePoint, в том числе в приложения с размещением в SharePoint. В последнем случае выполняется развертывание XAP-файла в библиотеке на сайте приложения. (Дополнительные сведения о сайтах приложения см в статье  [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).) Поэтому благодаря приложению Silverlight можно включить настраиваемый код SharePoint в состав любого приложения, так как настраиваемый серверный код недопустим в Надстройки SharePoint. Это также позволяет разработчикам Silverlight использовать свои навыки для создания приложений SharePoint, почти не тратя время на обучение.
  
    
    

> **Примечание.** Вы также можете использовать конечные точки SharePoint REST или OData в приложении Silverlight. Сравнение клиентской объектной модели Silverlight с конечными точками SharePoint REST и OData представлено в разделе [Конечные точки REST и OData](#RESTOData) далее в этой статье.
  
    
    


### <a name="mobile-object-model"></a>Объектная модель для мобильных устройств

Специальная версия клиентской объектной модели Silverlight доступна для устройств Windows Phone. Она содержит дополнительные интерфейсы API, которые подходят только для телефонов. Например, интерфейсы API, позволяющие регистрацию телефона для получения сообщений службы push-уведомлений (Майкрософт). Эта модель поддерживает все основные функции SharePoint. Но поддержка не распространяется на дополнительные расширения, которые поддерживаются двумя другими клиентскими объектными моделями для управляемого кода. Для доступа к этим дополнительным функциям используйте конечные точки REST или OData SharePoint в мобильном приложении. См. раздел  [Конечные точки REST или OData](#RESTOData) далее в этой статье.
  
    
    
Сборки для объектной модели для мобильных устройств сохраняются на каждом сервере SharePoint в папке %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\ClientBin. Их необходимо поместить в XAP-файл приложения для Windows Phone.
  
    
    

## <a name="javascript-object-model"></a>Объектная модель JavaScript
<a name="JavaScriptOM"> </a>

В SharePoint предоставлена объектная модель JavaScript, которую можно использовать во встроенном сценарии или отдельных JS-файлах. В ней предусмотрены те же функции, что и в клиентских объектных моделях .NET Framework и Silverlight. Как и клиентская объектная модель Silverlight, объектная модель JavaScript позволяет включить настраиваемый код SharePoint в состав любого приложения, так как настраиваемый код недопустим в Надстройки SharePoint. Это также позволяет веб-разработчикам использовать свои навыки работы с JavaScript, чтобы создавать приложения для SharePoint, почти не тратя время на обучение.
  
    
    
Как и клиентские объектные модели для управляемого кода, инфраструктура JavaScript для SharePoint взаимодействует с серверами фермы с помощью пакетов с кодом, который всегда выполняется асинхронно. Кроме того, сейчас возможно получать доступ к данным SharePoint на разных доменах с помощью JavaScript (но только к данным одного и того же родительского семейства веб-сайтов), что было недопустимо в предыдущих версиях SharePoint. Дополнительные сведения см. в статье  [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx). Данные возвращаются с сервера с помощью Нотация объектов JavaScript (JSON).
  
    
    
Объектная модель JavaScript определяется в наборе JS-файлов, размещенных в папке %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS на каждом сервере.
  
    
    
Примеры использования объектной модели .NET Framework см. в статье [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx).
  
    
    

> **Примечание.** Вы также можете использовать конечные точки SharePoint REST или OData в приложении JavaScript. Сравнение клиентской объектной модели JavaScript с конечными точками REST и OData в SharePoint представлено в следующем разделе, [Конечные точки REST и OData](#RESTOData). 
  
    
    


## <a name="restodata-endpoints"></a>Конечные точки REST и OData
<a name="RESTOData"> </a>

В случае сценариев, при которых необходимо получить доступ к объектам SharePoint со стороны клиентских технологий, которые не используют JavaScript и не созданы на платформах .NET Framework или Silverlight, SharePoint обеспечивает реализацию веб-службы передачи репрезентативного состояния (REST), использующей  [протокол ODatal](http://www.odata.org/) для выполнения операций CRUD с данными списков SharePoint. Кроме того, почти каждый интерфейс API клиентской объектной модели имеет соответствующую конечную точку REST. Это позволяет коду напрямую взаимодействовать с артефактами SharePoint с помощью любой технологии, поддерживающей стандартные HTTP-запросы и отклики. Чтобы использовать возможности REST, встроенные в SharePoint, код создает запрос RESTful HTTP для конечной точки, соответствующей необходимому интерфейсу API клиентской объектной модели. Веб-служба client.svc обрабатывает HTTP-запрос и направляет отклик в формате Atom или JSON.
  
    
    
Дополнительные сведения об использовании веб-службы REST или OData см. в статье  [Программирование с использованием службы SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx), примеры  в статье  [Выполнение базовых операций с использованием конечных точек SharePoint REST](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx).
  
    
    

### <a name="comparing-restodata-programming-with-client-object-model-programming"></a>Сравнение программирования с помощью REST или OData с программированием с помощью клиентской объектной модели

В некоторых случаях, возможно, лучше использовать конечные точки REST даже в приложениях, для которых доступна объектная модель SharePoint. Это в первую очередь касается разработчиков, не имеющих опыта разработки для Windows. В таблице ниже сравниваются основные функции этих типов программирования при создании приложения на платформе Windows или платформе, поддерживающей JavaScript.
  
    
    


|**Функция**|**Объектная модель .NET Framework или Silverlight**|**Объектная модель JavaScript**|**Конечные точки REST или OData, вызываемые с помощью платформы Windows или JavaScript**|
|:-----|:-----|:-----|:-----|
|Объектно-ориентированное программирование  <br/> |Да  <br/> |Да  <br/> |Нет  <br/> |
|Пакетная обработка  <br/> |Да  <br/> |Да  <br/> |Да  <br/> |
|Интерфейсы API для условной обработки и обработки исключений  <br/> |Да  <br/> |Нет  <br/> |Нет  <br/> |
|Доступность синтаксиса LINQ  <br/> |Да  <br/> |Нет  <br/> |Нет  <br/> |
|Объединение данных списков из различных веб-приложений SharePoint  <br/> |Да  <br/> |Нет  <br/> |Да  <br/> |
|Знание разработчиками, использующим REST или OData  <br/> |Нет  <br/> |Нет  <br/> |Да  <br/> |
|Сходство с программированием не для Windows или с помощью JavaScript  <br/> |Нет  <br/> |Да  <br/> |Да  <br/> |
|Строгая типизация полей элементов списка  <br/> |Нет (если не использовать LINQ)  <br/> |Нет  <br/> |Да (в случае платформы Windows)          Нет (в случае JavaScript)  <br/> |
|Использование jQuery, Knockout и других библиотек JavaScript  <br/> |Нет  <br/> |Да  <br/> |Нет (в случае платформы Windows)          Да (в случае JavaScript)  <br/> |
   

## <a name="wcf-data-services-framework"></a>Платформа WCF Data Services
<a name="WCFDataServices"> </a>

Предпочитаете использовать синтаксис LINQ в клиентских приложениях .NET Framework или Silverlight? SharePoint поддерживает  [WCF Data Services](http://msdn.microsoft.com/en-us/library/cc668792.aspx) как поставщика LINQ. Можно ориентироваться на файл listdata.svc для доступа к данным списка, как в ранних версиях SharePoint Foundation, или на тот же файл client.svc, который поддерживает интерфейс OData, чтобы получить доступ ко всем объектам SharePoint (в дополнение к данным списка). Дополнительные сведения см. в статье [Запрос SharePoint Foundation с помощью служб данных ADO.NET](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx).
  
    
    
На рисунке 2 показаны отношения между различными клиентскими интерфейсами API, клиентскими приложениями и SharePoint. URL-адреса _api*  URL-адреса конечных точек REST, связанные с фермой. Дополнительные сведения см. в статье  [Дополнительные сведения о службе REST в SharePoint 15](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx#bk_learnmore).
  
    
    

**Рисунок 2. Клиентские приложения и интерфейсы API в SharePoint**

  
    
    

  
    
    
![Модель программирования для приложений для SharePoint](../images/Sp15_app_.png)
  
    
    

  
    
    

  
    
    

## <a name="deprecated-api-sets"></a>Нерекомендуемые наборы интерфейсов API
<a name="DeprecatedAPIs"> </a>

Платформа SharePoint до сих пор поддерживает обратную совместимость двух наборов API, но мы не рекомендуем их использовать в новых проектах. Эти наборы относятся к  [веб-службам ASP.NET (asmx)](http://msdn.microsoft.com/library/c587ee90-1f88-43f3-b1a7-5f3072d038f8%28Office.15%29.aspx) и [прямым RPC-вызовам файла owssvr.dll](http://msdn.microsoft.com/library/4aa5c82b-90fb-4be5-b30c-d35ecae42a81%28Office.15%29.aspx).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Обзор разработки решений с помощью SharePoint](sharepoint-development-overview.md)
    
  
-  [Модели программирования в SharePoint](programming-models-in-sharepoint.md)
    
  
-  [Сравнение надстроек SharePoint с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md)
    
  
-  [Программирование с использованием службы SharePoint REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [Запрос SharePoint Foundation с помощью служб данных ADO.NET](http://msdn.microsoft.com/library/3e3e16f7-620a-4710-a3f3-19d0236f4b4a%28Office.15%29.aspx)
    
  

  
    
    