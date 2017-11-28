---
title: "Метаданных SharePoint, навигации и публикации возможности веб-сайтов"
ms.date: 11/03/2017
ms.openlocfilehash: 6917e097fd9b329d07ebfc82952150f30c63a8af
ms.sourcegitcommit: 3276e9b281b227fb2f1a131ab4ac54ae212ce5cf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/24/2017
---
# <a name="sharepoint-metadata-site-navigation-and-publishing-site-features"></a>Метаданных SharePoint, навигации и публикации возможности веб-сайтов

Использование функций управления SharePoint Online метаданных, навигации по сайту и публикации возможности веб-сайтов для поддержки сайтов публикации SharePoint.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

В этой статье описывается управление метаданными и Настройка структуры переходов сайта публикации и возможности веб-сайтов в SharePoint Online с помощью модели надстройки. В ней также рассматриваются способы работы с Общие шаблоны программирования web и библиотеки, помогут при настройке клиентов публикации фирменной символики сайта SharePoint.

## <a name="key-metadata-navigation-and-publishing-terms-and-concepts"></a>Основные метаданные, навигации и публикации термины и концепции

|**Концепция или термин**|**Описание и рекомендации**|
|:-----|:-----|
|Веб-часть поиска контента|Веб-части SharePoint, которая отображает динамический поиска контента на страницах, которые можно легко отформатировать. Для получения дополнительных сведений см. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://technet.microsoft.com/en-us/library/jj679900(v=office.15).aspx" target="_blank">Настройка веб-частей поиска в SharePoint Server 2013</a></p></li><li><p><a href="https://support.office.com/en-us/article/Configure-a-Content-Search-Web-Part-in-SharePoint-0dc16de1-dbe4-462b-babb-bf8338c36c9a?CorrelationId=5024de0f-f4f4-436a-9c4a-b578b74b4764&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Настройка веб-части поиска контента в SharePoint</a></p></li><li><p><a href="https://technet.microsoft.com/en-us/library/sharepoint-online-search-service-description.aspx" target="_blank">Функции поиска в SharePoint Online</a></p></li></ul>|
|ContentTypeId|Уникальные идентификаторы типов контента, которые предназначены для рекурсивного. Дополнительные сведения см в [класс ContentTypeId](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.contenttypeid.aspx) (CSOM).|
|Тип контента|Для повторного использования, централизованного коллекция метаданных (столбцов), рабочий процесс, поведение и других параметров для категории сведений. Сведения см. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms196085(v=office.14).aspx" target="_blank">Столбцы</a></p></li><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms460224(v=office.14).aspx" target="_blank">Создание типов контента</a></p></li><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms468437(v=office.14).aspx" target="_blank">Особые сведения в типах контента</a></p></li></ul>|
|Концентратор типов контента|Часть приложения-службы управляемых метаданных, который является центральный сайт, который публикует типов контента для других семейств веб-сайтов. Позволяет публиковать, повторная публикация и Отмена публикации типов контента из центрального расположения. Сведения см. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://support.office.com/en-us/article/Publish-a-content-type-from-a-content-publishing-hub-58081155-118d-4e7a-9cc5-d43b5dbb7d02?CorrelationId=49ebfe9f-6cf8-4f04-86a3-4d3fe23324fe&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Публикация типа контента от контента публикации сервера-концентратора</a></p></li><li><p><a href="https://support.office.com/en-us/article/View-error-logs-for-content-type-publishing-fa8bc6d4-f03e-4ce7-94de-5fd1c38fe32c?CorrelationId=3aaa4607-0888-417a-a0ff-8c1e44ce8167&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Просмотр журналов ошибок для публикации на тип контента</a></p></li></ul>|
|Каналы устройств|Метод для отображения страниц сайта публикации несколькими способами, с помощью различных разрабатывает, предназначенных для нескольких устройств. Дополнительные сведения можно [как: добавить фрагмент панели каналов устройств в SharePoint 2013](http://msdn.microsoft.com/library/612780a8-6267-49f6-a32d-33600bb5f6b4%28Office.15%29.aspx).|
|Шаблон отображения|Используется в веб-части, использующие технологии поиска отображения элемента управления шаблонами отображения результатов запросы, выполняемые в индекс поиска. Шаблоны для отображения доступны для всех веб-частей поиска. Для получения дополнительных сведений см [ссылка на шаблон отображения в SharePoint Server 2013](https://technet.microsoft.com/en-us/library/jj944947%28v=office.15%29.aspx).|
|Управляемая навигация|На базе службы управляемых метаданных (Таксономия) навигации по сайту. Используйте его для создания структуры переходов сайта, производного от таксономии управляемых метаданных. Управляемая Навигация часто хорошо работает с каталога продуктов.|
|Управляемые метаданные|Иерархическая коллекция централизованно управляемых терминов, которые можно использовать для определения и атрибут элементов в SharePoint. Управляемые метаданные можно использовать для управления публикация типов контента и для создания таксономии. В SharePoint 2013 и SharePoint Online, служба управляемых метаданных используется для создания управляемой навигации&mdash;веб-сайтов на базе таксономии навигации. Для получения дополнительных сведений см. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/bb897739(v=office.14).aspx" target="_blank">Настройка поставщиков в SharePoint Server 2010 (ECM) и элементы управления навигацией</a></p></li><li><p><a href="https://support.office.com/en-us/article/Introduction-to-managed-metadata-a180fa28-6405-4679-9ec3-81d2028c4efc?CorrelationId=2a4dbdb0-0199-40e2-ac58-568ca0a3f099&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Общие сведения об управляемых метаданных</a></p></li><li><p><a href="https://support.office.com/en-us/article/Introduction-to-managed-metadata-in-SharePoint-Server-2010-b324aebd-67ab-45a8-933d-ceedb2d909ea?CorrelationId=9152b80c-9fe4-43c5-bacc-178cc49d0e8f&amp;ui=en-US&amp;rs=en-US&amp;ad=US" target="_blank">Общие сведения об управляемых метаданных в SharePoint Server 2010</a></p></li><li><p><a href="https://technet.microsoft.com/en-us/library/ee530393(v=office.14).aspx" target="_blank">Администрирование управляемых метаданных (SharePoint Server 2010)</a></p></li><li><p><a href="http://msdn.microsoft.com/library/b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e(Office.15).aspx" target="_blank">Управляемые метаданные и навигация в SharePoint 2013</a></p></li><li><p><a href="http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02(Office.15).aspx" target="_blank">Управляемая навигация в SharePoint 2013</a></p></li><li><p><a href="https://msdn.microsoft.com/en-us/library/office/hh147179(v=office.14).aspx" target="_blank">Миграция управляемых метаданных в SharePoint Server 2010</a></p></li></ul>|
|[Пространство имен навигации](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.navigation.aspx)|Классы клиента объектной модели (CSOM), которые поддерживают структуры переходов сайта для сайтов публикации. |
|[Пространство имен таксономии](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.aspx)|Классы CSOM, которые поддерживают компоненты таксономии. Дополнительные сведения можно [синхронизировать групп терминов образец добавить в SharePoint](http://msdn.microsoft.com/library/76caa8e2-2a37-432c-8f98-9aa4acf86f79%28Office.15%29.aspx).|
|Закрепление|Как и повторное использование термина, фиксации хранит общих отношение между исходным термином и повторное использование экземпляра. Например общих отношения могут охватывать в семействах сайтов в сценарии публикации cross-site. Любое время добавляется или удаляется, термин действия обновляются по всей иерархии везде, где прикрепленных термин. Дополнительные сведения можно [как: задает использовать код с условиями ПИН-кода для терминов навигации в SharePoint 2013](http://msdn.microsoft.com/library/4a2811dc-25fd-4eb2-b0ab-1edded64c556%28Office.15%29.aspx).|
|Каталог продуктов|Чтобы получить сведения см.: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="http://msdn.microsoft.com/library/33f49e69-c1d3-4a6e-8887-5df683cba022(Office.15).aspx" target="_blank">Публикация в SharePoint 2013 на нескольких сайтах</a></p></li><li><p><a href="https://technet.microsoft.com/en-us/library/jj656774(v=office.15).aspx" target="_blank">Настройка публикации на нескольких сайтах в SharePoint Server 2013</a></p></li></ul>|
|Фрагмент кода|Фрагмент HTML функциональные возможности, которые можно добавлять к HTML-файл, созданный [Дизайнер](http://msdn.microsoft.com/library/29834b3f-3815-4347-91d3-296387663114%28Office.15%29.aspx). Например, может потребоваться добавить панели каналов устройств на страницу публикации&mdash;имеется фрагмент, которые. В следующих статьях представлены несколько примеров: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="http://msdn.microsoft.com/library/612780a8-6267-49f6-a32d-33600bb5f6b4(Office.15).aspx" target="_blank">Как: добавить фрагмент панели каналов устройств в SharePoint 2013</a></p></li><li><p><a href="http://msdn.microsoft.com/library/7583b217-200c-4569-8f88-fe975c8ebd72(Office.15).aspx" target="_blank">Как: Добавление фрагмент зоны веб-частей в SharePoint 2013</a></p></li><li><p><a href="http://msdn.microsoft.com/library/4beaab08-760b-408a-b768-906312779379(Office.15).aspx" target="_blank">Как: добавить фрагмент Trim безопасности в SharePoint 2013</a></p></li></ul>|
|Структурированная навигация|Сведения об использовании структурированная навигация можно [как: Настройка навигации в SharePoint Server 2010 (ECM)](https://msdn.microsoft.com/en-us/library/office/ms558975%28v=office.14%29.aspx)|

## <a name="prerequisites-for-using-csom-to-brand-publishing-sites"></a>Необходимые условия для использования CSOM на отображение фирменной сайтов публикации

По умолчанию веб-содержимым, опубликованной в веб-сайтов SharePoint в локальной общедоступный доступна для анонимных пользователей. По умолчанию CSOM и REST, недоступны для анонимных пользователей.

**Важные:**  Этот сценарий представлен потенциально серьезную угрозу для локальных сайтов SharePoint. Прежде чем использовать удаленный подготовки модели, описанной в [Удаленный подготовки торговых марок страницах SharePoint](Use-remote-provisioning-to-brand-SharePoint-pages.md) для подготовки фирменной символики для сайтов публикации, убедитесь, что установлены безопасности и разрешений веб-узла и безопасности последствия анонимный доступ.

В случае, если администратор сайта создает новое веб-приложение, которое включает в себя семейства веб-сайтов, которое использует публикации шаблона, а также позволяет анонимный доступ, анонимный доступ, будут доступны для каждого пользователя сайта при загрузке приложения для добавить в каталог. Так как анонимный доступ разрешен для сайта публикации SharePoint в локальной, что произойдет, если пользователь, который не проходит проверку подлинности переходит на сайт?

При создании надстройки размещенных в SharePoint и добавьте в проект клиентская часть надстройки, перейдите в **Центр администрирования** > **надстройки** > **Управление Add-in каталога** и создание каталога надстройки для веб-приложения, публикация Размещение в SharePoint надстройки с помощью Visual Studio для создания пакета надстройки, а затем загрузить пакет надстроек к каталогу надстройки. На этом этапе администратор семейства сайтов можно добавить надстройки для сайта публикации. Надстройка теперь доступен для добавления на страницу на сайте публикации.

Если изменение главной страницы сайта публикации и публикация надстройки, надстройка работает, как ожидалось. Выбор связанных заголовок надстройки загружает работу веб-страницы. Если SharePoint создает ошибку, это означает, что анонимный пользователь не имеет доступа к используется CSOM. Это имеет смысл, так как CSOM и REST, недоступны по умолчанию для анонимных пользователей.

### <a name="be-aware-that-disabling-use-remote-interfaces-permissions-can-introduce-a-security-risk"></a>Помните о том, что отключение разрешения на использование удаленных интерфейсов может привести к появлению риска безопасности

В поле **Разрешения для сайта**по умолчанию установлен флажок **требовать использование удаленных интерфейсов разрешений** . Снимите флажок **разрешений на использование удаленных интерфейсов** , чтобы разрешить анонимным пользователям доступ к используйте CSOM и REST. Это разделяет пользователям разрешения на использование удаленных интерфейсов, который предоставляет пользователю доступ к SOAP, WebDAV и CSOM. Если снять флажок удалит также и возможность использовать SharePoint Designer.

Может быть иногда требуется, чтобы запретить использование SharePoint Designer, но по-прежнему могут использовать CSOM. **Использование удаленных интерфейсов разрешение** checkbox позволяет анонимные пользователи могут использовать CSOM, не требуя их права на использование удаленных интерфейсов. Если снят флажок **разрешений на использование удаленных интерфейсов** , и выберите связанный заголовок надстройки для загрузки на взаимодействие с веб-страницы, SharePoint не вызывает ошибку. В этом случае интерпретирует код обработки ошибок Basic как анонимного пользователя.

**Предупреждение:**  
- При добавлении приложения для сайтов SharePoint общедоступный, использующих публикации шаблона, не снимите флажок **разрешения на использование удаленных интерфейсов** разрешения для сайта. Включение CSOM для анонимных пользователей представляет риску разглашения сведений. он divulges значительно больше информации, чем бы предполагается. С другой стороны, даже с доступом к полной CSOM SharePoint разрешения по-прежнему применяются. Анонимные пользователи будут только могут видеть списки или элементы, которые были явно доступны анонимным пользователям. Больше, чем значение, отображаемое на веб-страницы для анонимных пользователей с помощью CSOM и REST.
- Если не обязателен, не снимайте флажок **требовать использование удаленных интерфейсов разрешений** включены разрешения анонимного доступа на SharePoint на локальном сайт публикации. Это может привести к оба публикации и отмены публикации такого контента сайта для анонимных пользователей и может не закрывайте сайта отказ в обслуживании.

### <a name="use-the-viewformpageslockdown-feature"></a>Использовать функцию ViewFormPagesLockdown

Чтобы запретить пользователям доступ к страницам форм (например, Pages/Forms/AllItems.aspx) в общедоступный сайт SharePoint, используйте функцию **ViewFormPagesLockdown** . Он позволяет запретить пользователям просматривать сведения о Кем создан и автор изменений. Эта функция удаляется разрешение на **Просмотр страниц приложений** или **Использование удаленных интерфейсов**. Когда эта функция включена, пользователи не может перейти Pages/Forms/AllItems.aspx и просмотр элементов из этой библиотеки.

Если CSOM и REST, доступны для всех анонимных пользователей&mdash; Если снять флажок **разрешения на использование удаленных интерфейсов** &mdash;затем несмотря на то, что они по-прежнему не удается просмотреть **Кем создан** и **Автор изменений** данных в браузере, они могут Используйте REST или CSOM доступ к этим сведениям.

### <a name="security-trimming"></a>Фильтрация по ролям безопасности

Настроив анонимный доступ для веб-приложения, укажите политика анонимного доступа: _Запрещение записи&mdash;нет доступа на запись_ . Это означает, что анонимный доступ пользователей не могут выполнять запись на сайт&mdash;даже с кодом REST или CSOM. Анонимные пользователи могут видеть только сведения, которые были предоставлены им при настройке анонимный доступ к сайту.

Отменить публикацию страниц невидимы для анонимных пользователей по умолчанию. Они могут просматривать только списков, которые разрешить анонимный доступ. 

**Важные:**  Если флажок **разрешения на использование удаленных интерфейсов** используйте модель разрешений и другие меры безопасности убедитесь, что анонимные пользователи не имеют доступа к вещей, которые не должны.

### <a name="prevent-denial-of-service-attacks"></a>Предотвратить атаки

Нет, кэширование не CSOM. Это означает, что злоумышленник может запрашивать тысячи элементов из списков, одновременно, при адаптированные в разделе пороговое значение представления списка по умолчанию и сложная задача базы данных SharePoint. Это может распространение и перевести в полный отказ в обслуживании. 

### <a name="use-app-only-policy"></a>С помощью политики только для приложений

Можно использовать политики только для приложений с помощью надстройки для выполнения действий, которые текущий пользователь не прав на выполнение разрешает политики только которые запускаются добавить на размещение у поставщика. К примеру пользователь с разрешениями только для чтения, который является важным выполнить запись в список можно использовать надстройки с разрешениями только для приложений выполнить запись в список.

Для получения дополнительных сведений см [авторизации и проверки подлинности SharePoint Add-ins](http://msdn.microsoft.com/library/bde5647a-fff1-4b51-b67b-2139de79ce4a%28Office.15%29.aspx) и [Общие сведения о проверки подлинности и разрешения с помощью SharePoint надстроек и отключение](http://channel9.msdn.com/Events/Build/2013/3-603) (видео Channel 9).

### <a name="implement-ssl"></a>Реализация SSL

При использовании модели надстройки, использующих протокол Secure Sockets Layer (SSL) к управлению безопасностью передачи сообщений из Интернета. Протокол SSL работает с удаленного веб-сайт, отправка маркер доступа в заголовке HTTP Authorization со значением носителя + base64 кодировке строки (без шифрования).

**Важные:**  Протокол SSL защищает сайта публикации SharePoint от злоумышленников, чтобы получить маркер авторизации и воспользоваться доступа.

## <a name="remote-provisioning-and-publishing-sites"></a>Удаленный подготовки и веб-сайтах публикации

Можно использовать [удаленных подготовки рекомендациям](Use-remote-provisioning-to-brand-SharePoint-pages.md) для подготовки фирменной символики и другие настройки для сайтов публикации SharePoint.

Сайты публикации зависят от типов контента и **ContentTypeId**, который связывает типов контента в макеты страниц и шаблоны отображения. Настройка и Подготовка публикации содержимого страницы SharePoint зависит от эту функцию. Другие аспекты особенности, такие как службы управляемых метаданных и управляемой навигации подготовки настраиваемого сайта публикации не зависят от **ContentTypeId** и полностью поддерживаются в CSOM.

Другие публикации сайта настройки параметров, таких как каналы устройств и шаблоны для отображения, не требующие настраиваемых CSOM. Они зависят от функций дизайнер, CSS и HTML. Они являются после подготовки настроек, которые строятся с нуля и не нужно перенести.

## <a name="managed-metadata"></a>Управляемые метаданные

Функции управляемых метаданных, впервые введен в SharePoint 2010 позволяет определять пользовательские иерархии, или тегов таксономии метаданных для использования в SharePoint. Если вы хотите создать пользовательский узел навигации, можно использовать функцию управляемой навигации, которая построена на инфраструктуре управляемых метаданных.

Таксономии — это иерархическая классификации слова, метки или термины, которые сгруппированы в группы на основании сходства. Наименьший в таксономии SharePoint — это термин. Термины можно разбить на наборы терминов. Наборы терминов, сходства можно разбить на группы большего размера.

Краткое введение в таксономии в SharePoint в разделе [A Краткое введение в корпоративных управляемых метаданных в SharePoint 2010](https://msdn.microsoft.com/en-us/library/office/ee832800%28v=office.14%29.aspx) и [Общие сведения об управляемых метаданных в SharePoint 2010](https://support.office.com/en-us/article/Introduction-to-managed-metadata-in-SharePoint-Server-2010-b324aebd-67ab-45a8-933d-ceedb2d909ea?CorrelationId=2251ec3f-51ef-4924-89cc-d828b5068851&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

SharePoint 2013 представлены новые интерфейсы API и функции в набор компонентов управляемых метаданных.

### <a name="managed-metadata-programming-model"></a>Управляемая модель программирования метаданных

Для SharePoint 2013 модель программирования .NET Server для управляемых метаданных определяется в наборе следующие пространства имен: 

- [Пространство имен таксономии](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.aspx)
    
- [Пространство имен ContentTypeSync](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.contenttypesync.aspx)
    
- [Универсальный пространство имен](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.generic.aspx)
    
- [Пространство имен фонового кода](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.om.codebehind.aspx)
    
- [Обновление имен](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.upgrade.aspx)
    
- [Пространство имен веб-службы](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.webservices.aspx)
    
Эквивалентный CSOM классы, [пространства имен Client.Taxonomy](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.aspx) пространства имен.

В отличие от других областях объектной модели SharePoint, управляемых метаданных существует закрыть сходства между классы модели программирования .NET Server члены и CSOM классы и члены. Ниже приведены некоторые ключевые различия:

- CSOM не поддерживает синхронизацию типов контента.
    
- Класс **группы** , который представляет верхнем уровне организации в классе [банка терминов](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstore.aspx) , доступен только в .NET Server объектной модели. Класс [TermGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroup.aspx) является его эквивалент в CSOM.
    
- [GroupCollection класс](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.groupcollection.aspx), который представляет коллекцию объектов группы, доступен только в .NET Server объектной модели. Эквивалентное выражение на CSOM — это класс [TermGroupCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroupcollection.aspx) .
    
- CSOM включает в себя [CustomPropertyMatchInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.custompropertymatchinformation.aspx) и [LabelMatchInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.labelmatchinformation.aspx) классы, которые синхронизации настраиваемое свойство и метки данных с сервера.
    
В следующей таблице сравниваются классы в объектной модели сервера .NET и объектной модели CSOM.

|**.NET server объектной модели**|**Эквивалентный CSOM API**|
|:-----|:-----|
|[Microsoft.SharePoint.Taxonomy.ChangedGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedgroup.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedgroup.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changeditem.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeditem.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedItemCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changeditemcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedItemCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeditemcollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedItemType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changeditemtype.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedItemType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeditemtype.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedOperationType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedoperationtype.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedOperationType](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedoperationtype.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedSite](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedsite.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedSite](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedsite.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedterm.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedterm.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedTermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedtermset.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedTermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedtermset.aspx)|
|[Microsoft.SharePoint.Taxonomy.ChangedTermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.changedtermstore.aspx)|[Microsoft.SharePoint.Client.Taxonomy.ChangedTermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changedtermstore.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Taxonomy.ChangeInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.changeinformation.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Taxonomy.CustomPropertyMatchInformation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.custompropertymatchinformation.aspx)|
|[Microsoft.SharePoint.Taxonomy.FeatureIds](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.featureids.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.Group](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.group.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.HiddenListFullSyncJobDefinition](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.hiddenlistfullsyncjobdefinition.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.ImportManager](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.importmanager.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.Label](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.label.aspx)|[Microsoft.SharePoint.Client.Taxonomy.Label](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.label.aspx)|
|[Microsoft.SharePoint.Taxonomy.LabelCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.labelcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.LabelCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.labelcollection.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Taxonomy.LabelMatchInformation]()|
|[Microsoft.SharePoint.Taxonomy.MobileTaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.mobiletaxonomyfield.aspx)|[Microsoft.SharePoint.Client.Taxonomy.MobileTaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.mobiletaxonomyfield.aspx)|
|[Microsoft.SharePoint.Taxonomy.StringMatchOption](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.stringmatchoption.aspx)|[Microsoft.SharePoint.Client.Taxonomy.StringMatchOption]()|
|[Microsoft.SharePoint.Taxonomy.TaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfield.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyField](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.stringmatchoption.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldcontrol.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldEditor](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldeditor.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldValue](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldvalue.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyFieldValue](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomyfieldvalue.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyFieldValueCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyfieldvaluecollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyFieldValueCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomyfieldvaluecollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyitem.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomyItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomyitem.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyItemPicker](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyitempicker.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TaxonomyRights](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomyrights.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TaxonomySession](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomysession.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TaxonomySession](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.taxonomysession.aspx)|
|[Microsoft.SharePoint.Taxonomy.TaxonomyWebTaggingControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.taxonomywebtaggingcontrol.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.Term](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.term.aspx)|[Microsoft.SharePoint.Client.Taxonomy.Term](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.term.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termcollection.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Taxonomy.TermGroup](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroup.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Taxonomy.TermGroupCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termgroupcollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermProperty](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termproperty.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TermPropertyToolPart](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termpropertytoolpart.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termset.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termset.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermSetCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termsetcollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermSetCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termsetcollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermSetItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termsetitem.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermSetItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termsetitem.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstore.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermStore](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termstore.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermStoreCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstorecollection.aspx)|[Microsoft.SharePoint.Client.Taxonomy.TermStoreCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.taxonomy.termstorecollection.aspx)|
|[Microsoft.SharePoint.Taxonomy.TermStoreOperationException](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.termstoreoperationexception.aspx)|Примеры|
|[Microsoft.SharePoint.Taxonomy.TreeControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.taxonomy.treecontrol.aspx)|Примеры|

## <a name="page-layouts"></a>Макеты страниц

Для сайтов публикации макет страницы определяет макет страниц определенного класса. Он также определяет настраиваемых областей страницы с заполнителей контента, которые заполняются содержимого из совпадающих областей на макетах страниц. Макеты страниц обычно основаны на настраиваемого типа контента. Типы контента определите настраиваемые поля содержимого, которые требуется отобразить на странице. Как правило вы создадите настраиваемого типа контента, который включает в себя поля, которые сопоставляют макет страницы или ваша группа разработки запланировали ранее.

Настраиваемые элементы управления поля может включать текст, изображения, видео или других типов контента. SharePoint предоставляет типов контента для статьи, каталога, начальная страница и др. Доступ к типы контента макета страницы, перейдя к **Параметрам сайта** > **Типы контента сайта**. Эти макет страницы по умолчанию, контента, что типы может служить введите родительских типов контента для настраиваемого содержимого, который создается.

Все типы контента макета страницы наследовать от типа контента страницы. После создания настраиваемого типа контента SharePoint отображаются столбцы, новый тип контента наследуется от типа контента страницы. Можно добавить новые столбцы сайта для представления новых настраиваемых полей, которые необходимо отобразить в макет страницы. Указание типа для каждого столбца сайта. Тип — это значение, например, «однострочный текст» или «Полный HTML». Рассмотрите возможность факторов, как степень descriptiveness или элемент управления, пользователь должен иметь с полем при указании типа.

После создания всех полей, которые хранения содержимого в макет страницы, можно создать макет страницы в диспетчере оформления. Дополнительные сведения можно [как: создать макет страницы в SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx). После создания макета страницы, его публикация, перейдя к **Параметрам сайта** > **главные страницы и макеты страниц**. HTML-файл и ASPX-файл отсутствуют. HTML-файл является хозяином и для ее редактирования можно использовать любой редактор HTML. После сохранения файла и его публикация дизайнер включает в себя изменения и преобразует обновленный HTML-файл в формате ASPX, который использует SharePoint для отображения страницы. Чтобы опубликовать макет страницы, выберите HTML-файл и выберите пункт **Опубликовать** на ленте.

Чтобы создать на основании нового макета страницы, перейдите на **Новую страницу** > **страница** > **Макетов страниц** для просмотра нового макета страницы в списке Доступные макеты страниц. При выборе нового макета страницы, вы должны увидеть все новые поля, указанную при создании нового типа контента для нового макета страницы. При просмотре страницы и HTML-код не будет визуализации должным образом, можно изменить HTML-код и затем использовать Дизайнер Отправка обновленный файл.

## <a name="site-navigation"></a>Структуры переходов сайта

Существует четыре вида навигации по сайту. 

- Глобальная Навигация
    
- Локальный навигации
    
- Структурированная навигация
    
- Управляемая навигация
    
Глобальная Навигация ссылается на элементы навигации, которые помогают пользователям перемещение с одного сайта SharePoint. Локальный навигации относится к навигации на сайте SharePoint. Структурированные и управляемые навигации немного более сложны.

### <a name="structured-navigation"></a>Структурированная навигация

Структурированная навигация статического подход к реализации навигации на сайтах SharePoint. Обычно совпадает структуры компании, которая требует изменение структуры навигации сайта SharePoint. Реструктуризация работы часто означает, что перемещение дочерних сайтов и/или страниц и обновление ссылки для указания на новый целевых значений.

Структурированная навигация может быть достаточно для структуры сайта достаточно простую, частичного Если вашей компании структуры (и поэтому структуры сайта) является стабильным в течение длительных периодов времени. Для структуры глубокое и более сложные веб-узлов и компаний в публикации структуры навигации веб-узлов, которые необходимо расти в размерах и динамическое изменение управляемая Навигация может быть лучшим вариантом. Дополнительные сведения о структурированная навигация можно [как: Настройка навигации в SharePoint Server 2010](https://msdn.microsoft.com/en-us/library/office/ms558975%28v=office.14%29.aspx).

### <a name="managed-navigation"></a>Управляемая навигация

Управляемая Навигация построена на ядро публикации сайта и таксономии инфраструктуры. Управляемая Навигация привязан к одного семейства сайтов. Он используется для определения навигации глобальные и локальные наборы терминов и термины. К примеру можно создайте набор терминов, который определяет общий глобальной навигации и добавьте условия для этого набора терминов для определенных навигационных элементов в глобальной навигации.

Дополнительные сведения об управляемой навигации можно найти в следующих статьях:

- [Управляемая навигация в SharePoint 2013](http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02%28Office.15%29.aspx)
    
- [Обзор управляемой навигации в SharePoint Server 2013](https://technet.microsoft.com/en-us/library/dn194311%28v=office.15%29.aspx)
    
Ниже приведены некоторые ключевые моменты высокого уровня о классы, методы и свойства в модели расширения навигации SharePoint для публикации сайтов.

-  Классы **NavigationTerm** и **NavigationTermSet** добавить свойства и методы, которые специфичны для управляемой навигации. Дополнительные состояние хранится в свойстве **настраиваемые свойства** класса **NavigationTerm** .
    
-  Классы **NavigationTerm** и **NavigationTermSet** имеет два режима: редактируемого и только для чтения. В объектной модели .NET Server **NavigationTerm** объекты хранятся в кэше навигации таксономии, к которому можно получить только с помощью функций в **TaxonomyNavigation** статического класса.
    
-  **PortalSiteMapNodeProvider** объекты в объектной модели .NET Server предоставляют интерфейс между возможности перехода сайт на основе данных и источники данных карты сайта. Как правило записываются узел поставщика карты для хранения карты сайта в XML-файл или формат данных, который не поддерживается платформой SharePoint по умолчанию.
    
CSOM включает в себя некоторые уникальные классы и перечисления:

- Перечисление **NavigationLinkType** определяет тип узла навигации в дереве переходов. Можно указать узел как корневой узел, понятный URL-адрес или стандартной связи.
    
- Перечисление **StandardNavigationScheme** определяет как локальной или глобальной панели навигации.
    
- Перечисление **StandardNavigationSource** включает в себя три возможных глобальной навигации и локальной навигации. Каждый вариант представляет состояние, соответствующий конфигурации базового поставщиков.
    
- Класс **StandardNavigationSettings** управляет схемы глобальные и локальные навигации.
    
В следующей таблице перечислены публикации классы навигации в режиме объектов сервера и их эквивалентами CSOM.

|**Серверная объектная модель.**|**CSOM**|
|:-----|:-----|
|[Microsoft.SharePoint.Publishing.Navigation.CachedObjectSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.cachedobjectsitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationComparer](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationcomparer.aspx)|Примеры|
|Примеры|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationLinkType](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationlinktype.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationterm.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTerm](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.navigation.navigationterm.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermCollection](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermcollection.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTermSet](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationtermset.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermSet](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermset.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTermSetItem](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationtermsetitem.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermSetItem](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermsetitem.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.NavigationTermSetView](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.navigationtermsetview.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.NavigationTermSetView](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.navigationtermsetview.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.PortalHierarchicalDataSourceView](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalhierarchicaldatasourceview.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalHierarchicalEnumerable](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalhierarchicalenumerable.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalHierarchyData](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalhierarchydata.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalListItemSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portallistitemsitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalListSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portallistsitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalNavigation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalnavigation.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapDataSource](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalsitemapdatasource.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapDataSourceSwitch](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalsitemapdatasourceswitch.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portallistsitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalSiteMapProvider](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalsitemapprovider.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.PortalWebSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.portalwebsitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.ProxySiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.proxysitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.SiteNavigationSettings](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.sitenavigationsettings.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.SiteNavigationSettingsWriter](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.sitenavigationsettingswriter.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.SPNavigationSiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.spnavigationsitemapnode.aspx)|Примеры|
|Примеры|[Microsoft.SharePoint.Client.Publishing.Navigation.StandardNavigationSource](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.standardnavigationsource.aspx)|
|Примеры|[Microsoft.SharePoint.Client.Publishing.Navigation.StandardNavigationSettings](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.standardnavigationsettings.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigation](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigation.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.TaxonomyNavigation](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.taxonomynavigation.aspx)|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigationCacheConfig](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigationcacheconfig.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigationCacheStatistics](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigationcachestatistics.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomyNavigationContext](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomynavigationcontext.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapNode](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomysitemapnode.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.TaxonomySiteMapProvider](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.taxonomysitemapprovider.aspx)|Примеры|
|[Microsoft.SharePoint.Publishing.Navigation.WebNavigationSettings](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.navigation.webnavigationsettings.aspx)|[Microsoft.SharePoint.Client.Publishing.Navigation.WebNavigationSettings](https://msdn.microsoft.com/EN-US/library/office/microsoft.sharepoint.client.publishing.navigation.webnavigationsettings.aspx)|

## <a name="publishing-site-features"></a>Компоненты публикации сайта

SharePoint 2013 и SharePoint Online: несколько функций, которые специфичны для сайтов публикации SharePoint

- Каналы устройств позволяют для применения одного проекта сайта публикации на нескольких устройствах и браузерах.
    
- Шаблоны для отображения делают возможным фирменной символики и настроить внешний вид веб-частей, связанных с поиском.
    
- Показ изображений определить аналитики, которые используются для отображения изображений на страницы на сайтах публикации SharePoint 2013.
    
Эти компоненты можно реализовать с помощью классов в пространстве имен [публикации](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.aspx) модели программирования CSOM.

### <a name="device-channels-and-device-channel-panels"></a>Каналы устройств и панели каналов устройств

Каналы устройств и панели каналов устройств можно использовать для оптимизации сайта для телефонов и планшетные ПК. Путем создания уникальных канала для каждого устройства, которое требуется работать, можно отображать сайта публикации SharePoint в несколько способов. Можно создавать один сайт один раз, а затем сопоставить сайта и его содержимого разных главных страниц и таблиц стилей для размещения разных целевых значений.

Создание каналов с помощью [Дизайнера](http://msdn.microsoft.com/library/29834b3f-3815-4347-91d3-296387663114%28Office.15%29.aspx). После создания канала сопоставьте его мобильное устройство или браузера с строка агента пользователя входящих устройства.

Устройство может принадлежать более одного канала. В этом случае можно ранжирования каналы, в том случае, если устройство принадлежит. Например при создании канала для смартфонов и канала для настройки определенное устройство, можно ранжирования каналы, чтобы устройства с определенной конфигурации получить канала для их, а все другие смартфоны получения смартфонах канала.

Вы можете создать до 10 каналов (в том числе канала по умолчанию) в диспетчере оформления. По умолчанию канала захватывает весь трафик, не обнаружены с помощью одного из других каналов. При создании нового канала, заполните поля, перечисленные в следующей таблице.

|**Поле**|**Обязательный или необязательный?**|**Описание**|
|:-----|:-----|:-----|
|Имя|Required|Определяет канал, чтобы отличать его от других пользователей.|
|Псевдоним канала|Required|Как код, строки запроса, файлы cookie или каналов устройств различать различия между каналами.|
|Правила включения устройств|Required|Подстрок агента пользователя, направление запросов от устройств (каждый должен быть на другую строку).|
|Описание|Необязательно заполнять.|Описывает, что делает этот канал.|
|Active|Необязательно заполнять.|Если этот флажок установлен, связанные с ними ресурсы для канала каналом для направления трафика. В противном случае строки запроса `?DeviceChannel=<alias>` Предварительный просмотр сайта в канале.|
 **Каналов устройств**

После создания каналов устройств сопоставьте главной страницы каждой из них. Поскольку главная страница настроек реже, часто это главную страницу по умолчанию (seattle.master). При создании уникальных главной страницы для одного или нескольких каналов устройств можно ссылаться в другой файл CSS, чем главной страницы для канала по умолчанию. Макеты страниц, которые можно создать будет работать с каждого канала, который вы создаете. Элемент управления панели каналов устройств можно использовать для различения макетов страниц макета между каналами.

Для получения дополнительных сведений см [каналы устройств дизайнер SharePoint 2013](http://msdn.microsoft.com/library/a924bd7b-a5e3-41bf-b0a7-3e43945fa951%28Office.15%29.aspx).

Панель канала устройств является элементом управления контейнера, сопоставленную с одного или нескольких каналов. Элемент управления панели каналов устройств можно добавить в макет страниц и панели может контролировать, какие содержимое отображается в каждый канал. Когда один или несколько из этих каналов активны при отображении страницы, отображаются все содержимое панели каналов устройств. Чтобы определить, когда для включения определенного содержимого для одного или нескольких конкретных каналов с помощью панели канала устройств.

Рассмотрите возможность макет страницы, который включает в себя десяти полей. Некоторые из этих полей, доступны для всех каналов, а некоторые только должно составлять конкретные каналы. Например рассмотрим поля заголовка мобильных заголовка, который отображает только на смартфонах или большой настраиваемых боковой панели, которая отображает только на настольные ПК и планшетные ПК.

Панели каналов устройств можно также использовать для изменения стилей и размещения содержимого на страницы путем добавления CSS указанного канала. Дополнительные сведения можно [как: добавить фрагмент панели каналов устройств в SharePoint 2013](http://msdn.microsoft.com/library/612780a8-6267-49f6-a32d-33600bb5f6b4%28Office.15%29.aspx) и [как: фирменной символики фрагментов кода с помощью CSS в SharePoint 2013](http://msdn.microsoft.com/library/d18d07b6-1a6b-4589-a65c-932b67cef595%28Office.15%29.aspx).

**Строки агента пользователя и каналы устройств**

Строка агента пользователя — это небольшая строка данных, который определяет браузер. Эти сведения можно отправить на сервер, который определяет агента пользователя. Каналы устройств включить запрос в соответствующем канал устройства на основе строка агента пользователя (или подстрок) устройства (или браузера) пользователь просматривает из. Интерфейсный веб-разработчик создает и настраивает каналы для захвата трафика. Дополнительные сведения можно [что будет Windows Internet Explorer отчет в виде строки агента пользователя?](https://msdn.microsoft.com/en-us/library/cc817582.aspx)

**Приоритет разрешения для каналов устройств**

При создании нескольких каналов, они располагались в том порядке, в котором требуется их устранения. Используется первого канала, который включает в себя правило включения устройства, которое соответствует строка агента пользователя. В следующей таблице показан пример этого правила.

|**Канал**|**Порядок 1**|**Порядковый номер 2**|
|:-----|:-----|:-----|
|1|Windows Phone 8|Windows Phone|
|2|Windows Phone|Windows Phone 8|
|3|Значение по умолчанию|Значение по умолчанию|
Если порядок 1 активен, пользователя, запрашивающего страницу с телефона Windows 8, получает канал устройства 1 с меткой Windows Phone 8. Использовать каналу 2 пользователь с ОС Windows phone и все остальное будет использовать канал 3. Тем не менее с помощью порядка 2, пользователя, запрашивающего что страницы из Windows phone 8 всегда могут получать канал устройства 1 с меткой Windows Phone и никогда не использовать канал устройства, определенные для него.

После определения и упорядочивать каналы устройств разных главных страниц можно применять к каждому каналу. По умолчанию все каналы будут использовать главную страницу по умолчанию канала. 

**Примечание:**  CSOM не содержит общий программный Интерфейс для управления каналы устройств и панели каналов устройств.

### <a name="display-templates"></a>Шаблоны отображения

Сайты публикации SharePoint используйте отображения шаблоны, которые необходимо контроль того, какие управляемые свойства отображаются в результатах поиска и как они отображаются в веб-части. Поиск только шаблонов отображения для использования веб-частей; веб-части запроса содержимого не поиска веб-части и не использует шаблоны для отображения.

В следующей таблице перечислены типы шаблонов отображения, в том порядке, в котором SharePoint применяет их. 

|**Шаблон отображения**|**Примечания**|
|:-----|:-----|
|Шаблоны отображения элемента управления|Применяется к всей веб-части, поэтому он сначала применяет SharePoint и только один раз. Он содержит HTML-код, структуры общий макет для отображения результатов поиска. Например шаблон отображения элемента управления предоставить HTML-код для заголовка и начало и конец списка. Этот шаблон отображается только один раз в веб-части. |
|Шаблоны для отображения группы|Применяется во-вторых, а — это один раз на группу для веб-части результатов поиска. |
|Шаблоны отображения элемента|Применяется последнего, если не применяется шаблон отображения фильтра. Шаблоны отображения элемента, применяются для каждого элемента. Этот шаблон определяет способ отображения каждого элемента в наборе результатов в веб-части. Например он предоставляет HTML-код для элемента списка, который является обычного текста, элемента списка, который содержит изображение или элемент списка, форматов блока Дополнительные ссылки и сведения о сводном описании обеспечивает более контекст для результатов поиска. |
SharePoint сохраняет шаблоны для отображения в папке шаблонов отображения в коллекции главных страниц. Каждый шаблон отображения связан с типом контента в коллекции главных страниц. Чтобы определить тип контента для каждого файла шаблона отображения во время использования подключенный диск, используйте имя файла.

Приемники событий, преобразования и обновление главные страницы и макеты страниц из HTML-код JavaScript, которые также преобразование шаблонов отображения из HTML в JavaScript. Преобразование и синхронизация является односторонним; он не преобразует из JavaScript в формате HTML.

**Примечание:**  CSOM не содержит общий программный Интерфейс для работы с шаблонами отображения.

**Структура шаблона отображения**

Каждый шаблон отображения содержит следующие элементы: 

- Заголовок.
    
- Заголовок, который содержит настраиваемые элементы ограниченного `<mso:CustomDocumentProperties>` тег.
    
- A `<body>` тег, содержащий блок скрипта.
    
- A `<div>` тег.
    
Настраиваемые свойства документа содержат важную информацию в SharePoint о шаблон отображения. Каждый шаблон отображения связан с типом контента, который определяется `<ContenTypeId>`. Можно задать другие свойства, которые определяют, будет ли Чтобы скрыть или отобразить шаблон в списке шаблонов доступные отображения для веб-части, HTML-кода JavaScript Сопоставление управляемого свойства, контекст, в котором используется шаблон отображения, является ли JS-файла в настоящее время связанные с шаблоном отображения HTML и ли преобразование HTML-код JavaScript прошла успешно, или если предупреждения и ошибки были созданы. 

С помощью `<script>` тег, можно ссылаться на внешние файлы CSS или JavaScript за пределами файлов шаблонов HTML основной экран.

Если требуется утверждение контента в коллекции главных страниц, все CSS, JavaScript, и другие файлы ресурсов должны быть опубликованы, прежде чем их можно использовать на главные страницы и макеты страниц. Для получения дополнительных сведений см [требуется утверждение элементов в список веб-сайтов или библиотеке](https://support.office.com/en-us/article/Require-approval-of-items-in-a-site-list-or-library-cd0761c4-8c3f-4ea2-9435-13c28aa23d08?CorrelationId=4efce7db-3017-4f50-854d-1f07eaf6bc16&amp;ui=en-US&amp;rs=en-US&amp;ad=US). `<div>` Тега содержит код, совпадает с именем файла шаблона HTML-код для отображения. Место CSS или JavaScript, который необходимо включить, который настраивает способ отображения этой веб-части в `<div>` блокировки.

**Обработка шаблона отображения**

SharePoint определяет шаблоны для отображения в файлах HTML и JavaScript. Если в диспетчере оформления, измените HTML-файл, содержащий определение шаблона отображения и сохранить изменения, SharePoint компилирует изменения в файл JavaScript, с тем же именем. SharePoint использует этот файл JavaScript для отображения веб-частей на страницах.

**Важные:**  Не изменяйте файл JavaScript, который содержит определение шаблона отображения. Только обновление HTML-файл. Процесс преобразования требуется HTML-файла для соответствия стандартам XML. Например, используйте ** &lt;br&gt;**, а не ** &lt;br /&gt;**. Дополнительные сведения можно [как: преобразование HTML-файла в главную страницу в SharePoint 2013](http://msdn.microsoft.com/library/a76ab289-3256-45de-ac63-d5112a74e3c7%28Office.15%29.aspx).

**Создание новых шаблонов отображения**

— Это самый простой способ создать новый шаблон отображения для изменения существующего шаблона. Шаблоны для отображения различных изменить внешний вид различных связанных с веб-частей, включая поиск контента веб-части уточнения веб-часть, веб-части уточнения таксономии и результатов поиска в веб-части. Для получения дополнительных сведений см.

- [Шаблоны для отображения дизайнер SharePoint 2013](http://msdn.microsoft.com/library/1a782bac-48ee-4baf-8751-0f943a306e0f%28Office.15%29.aspx)
    
- [Настройка веб-частей поиска в SharePoint Server 2013](https://technet.microsoft.com/en-us/library/jj679900%28v=office.15%29.aspx)
    
- [Настройка свойств веб-части уточнения результатов поиска в SharePoint Server 2013](https://technet.microsoft.com/en-us/library/gg549985%28v=office.15%29.aspx)
    
- [Ссылка на шаблон для отображения в SharePoint Server 2013](https://technet.microsoft.com/en-us/library/jj944947%28v=office.15%29.aspx)
    
**Шаблоны отображения свойств, которые могут использоваться в**

Прежде чем начать для идентификации свойств, которые можно использовать в шаблон отображения, найдите шаблон отображения, необходимо создать из, а затем сохраните его под новым именем. Код шаблона отображения находится в пределах `<mso:ManagedPropertyMapping>` тег.

```
<mso:ManagedPropertyMapping msdt:dt="string">'Picture URL'{Picture URL}:'PublishingImage;PictureURL;PictureThumbnailURL','Link URL'{Link URL}:'Path','Line 1'{Line 1}:'Title','Line 2'{Line 2}:'Description','Line 3'{Line3}:'','SecondaryFileExtension','ContentTypeId'</mso:ManagedPropertyMapping>
```

Далее, откройте **Параметры сайта** > **Схемы поиска**и выполните поиск имени столбца в поле фильтра управляемое свойство, которое вы хотите включить в шаблон отображения. Выберите управляемое свойство, а затем изменить и скопируйте имя свойства. 

```
<mso:ManagedPropertyMapping msdt:dt="string">'Picture URL'{Picture URL}:'PublishingImage;PictureURL;PictureThumbnailURL','Link URL'{Link URL}:'Path','Line 1'{Line 1}:'Title','Line 2'{Line 2}:'Description','Line 3'{Line3}:'','owsTXTPrice','owsTXTColor'</mso:ManagedPropertyMapping>
```

**Примечание:**  В этом примере **PictureURL** сопоставляется с первого управляемого свойства, который использовался во время поиска получение результатов для **PublishingImage**, **PictureURL**или **PictureThumbnailURL**.

### <a name="image-renditions"></a>Показ изображений

Передача изображения определяет измерения, которые используются для отображения изображений на страницы на сайтах публикации SharePoint 2013. CSOM можно использовать для создания экземпляра и обработки изображений. Метаданные, такие как высота, ширина, имя и версию представление изображения можно указать с помощью класса [ImageRendition](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.imagerendition.aspx) . Можно использовать свойства и методы в классе [SiteImageRenditions](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.siteimagerenditions.aspx) для чтения и записи изображений из семейства веб-сайтов.

Дополнительные сведения см в [SharePoint 2013 дизайнер изображений](http://msdn.microsoft.com/library/d08a74c0-5674-4f26-8646-11ea1f081c85%28Office.15%29.aspx).

## <a name="sharepoint-and-common-web-programming-techniques"></a>SharePoint и общие веб-методов программирования

SharePoint дизайнеров и разработчиков часто требуется использовать стандартный web методов программирования с помощью SharePoint при разработке сайтов публикации. Можно использовать реакции разработки, адаптивный разработки или каналы устройств и взаимодействуйте разработки, совместного использования.

### <a name="responsive-design"></a>Уровень возможности реагирования у разработки

С помощью каналов устройств можно создать сайт один раз и затем предназначенных для нескольких устройств и браузеров. Сообщества разработчиков web обычно использует реакции проектирования и подход «жидкости сетка» для управления отображение макетов и разработка сайтов для правильного воспроизведения любой браузер или устройство. В структуре реакции элементов на странице изменить порядок самостоятельно в соответствии с устройством пользователя и ориентации экрана.

Уровень возможности реагирования у конструктора основано на компонент запросов мультимедиа в CSS3. Она использует медиа-запросов в соответствии с ширины экрана устройства, а затем применятся стили на стороне клиента для отображения содержимого. Медиа-запросов дают возможность конструктору конечного свойства отдельного сайта, такие как ширину экрана. Использование медиа-запросов для создания гибкой макетов и изображений и условного вызова альтернативы файл CSS.

Дополнительные сведения и примеры в разделе [Реакции пользовательского интерфейса SharePoint 2013/2016/Online](https://dev.office.com/patterns-and-practices-detail/7267), [Взаимодействуйте SharePoint](http://responsivesharepoint.codeplex.com/) и [Реализация реакции проектов в SharePoint 2013](http://blogs.msdn.com/b/sharepointdev/archive/2013/04/01/implementing-your-responsive-designs-on-sharepoint-2013.aspx). 

### <a name="adaptive-design"></a>Адаптивный разработки

Адаптивный веб-дизайн (иногда называемую доставки адаптивный web) похож на разработки быстродействующих веб-приложений. Адаптивный разработки прослушивает устройств и браузеров и выбирает оптимальный способ отображения страниц. 

Функция каналы устройств в SharePoint 2013 — это адаптивный разработки. Адаптивный макетов позволяет каждое устройство, в зависимости от макета страницы, спецификации каждый канал устройства и порядке, указанном в панели каналов устройств. 

### <a name="device-channels-and-responsive-design-together"></a>Каналы устройств и взаимодействуйте разработки вместе

Можно использовать каналы устройств и методы разработки быстродействующих веб-приложений друг с другом для построения быстро сайта публикации SharePoint общедоступный. Рассмотрите возможность создания единого настраиваемой главной страницы для устройствах, таких как телефоны и планшетные ПК, а другой для веб-браузеров и связать каждый из них с помощью канала устройств. Затем с помощью гибкой сетки, гибкие изображений и медиа-запросов CSS3 создавать удобства просмотра взаимодействия для каждого устройства и веб-браузере, веб-узла необходимые для поддержки.

## <a name="add-jquery-to-a-sharepoint-site"></a>Добавление jQuery на сайте SharePoint

JQuery можно добавить на сайт SharePoint на уровне сайта, страницы или в разделы страницы, например один из области страницы SharePoint или веб-части добавлены макет страницы.

Настраиваемое действие можно использовать для загрузки jQuery из библиотеки документов. Это необходимо сделайте в том случае, если требуется сделать доступным для всех страниц jQuery на сайте SharePoint. Данный подход гибкие, но не просто элемента управления, и это влияет на конструктор веб-сайтов и администратора. Можно хранить и поддерживать файлы JavaScript в библиотеке документов, но они могут также быть случайно изменены или удалены. По этой причине не рекомендуется этого подхода.

Также можно загрузить jQuery из корневого каталога SharePoint с помощью [ScriptLinkControl](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.webcontrols.scriptlink.aspx). Использование элемента управления для вставки сценариев, которые выполняются на удаленном сайте и изменение скриптов без изменения установки SharePoint. **ScriptLinkControl** подход имеет смысл, когда необходимо использовать jQuery на страницу приложения или в веб-части, который отображается на странице. Подготовка с помощью этого параметра медленная и влияет на производительность, так как jQuery добавляется на одну страницу за раз, развертывание файл jQuery в SharePoint правило позволяет обойти другие требования прежних версий. Это полезно, если необходимо перенести решения SharePoint 2013 код с полным доверием (FTC) CSOM и переноса включает в себя перемещение и рефакторинг пользовательских JavaScript и вариантов поведения jQuery.

И, наконец можно использовать редактор содержимого веб-части для загрузки jQuery из сети доставки содержимого (CDN). Это полезно, если необходимо добавить jQuery один или несколько страниц, включая страницы вики-сайта и веб-части. Так как вы загружаете файл jQuery из сети CDN, не требуется для хранения дополнительных файлов на сервере SharePoint, а пользователи получают преимущества распределенных, кэшированной версии файлов jQuery. SharePoint вызывает файл jQuery из сети CDN, и можно добавить код настраиваемого jQuery, вы создаете редактор контента веб-части. 

## <a name="build-sharepoint-provider-hosted-add-ins-with-aspnet-mvc-5"></a>Построение SharePoint у поставщика надстроек в ASP.NET MVC 5

Может создавать настраиваемые размещением у поставщика надстроек с помощью шаблона model-view-controller (MVC) в SharePoint. В этой модели разделяет приложение на три части подключенными друг к другу. Это отделяет внутренние представления информации от того, они видны и принятия пользователем. Модель представляет внутренней структуры программного обеспечения, представление (обычно элементы пользовательского интерфейса) и контроллера, которые являются классы, которые подключаются модели и представления. 

Можно включить содержимое ASP.NET MVC в содержимом главную страницу сайта SharePoint. На самом деле можно использовать интерфейсы API Office 365 для создания надстройки SharePoint 2013 с ASP.NET MVC 5. 

API-интерфейсы для MVC при разработке для SharePoint определяются в `Filters\SharePointContextFilterAttribute.cs` и `SharePointContext.cs`. Эти интерфейсы API перенос действия, которые легко общаться в SharePoint за один вызов, который упрощает логику, необходимую для реализации принимает веб-проект.

Атрибут фильтра контекста SharePoint выполняет дополнительную обработку для получения стандартных сведений при перенаправлении из SharePoint удаленного веб-приложения, такие как URL-адрес узла. Также определяет, требуется ли добавить в перенаправление на SharePoint для пользователя для входа (например, закладки). Этот фильтр можно применять к контроллеру или в представление. Классы контекста SharePoint инкапсулируют все данные из SharePoint таким образом, вы можете создать определенного контекста хост-сайта и добавить в веб- и связь с SharePoint.

Дополнительные сведения можно [Узнать о ASP.NET MVC](http://www.asp.net/mvc/overview) и[Краткие сведения о MVC поддерживает SharePoint Add-ins](http://blogs.msdn.com/b/officeapps/archive/2013/07/09/introducing-mvc-support-for-apps-for-sharepoint.aspx).

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
- [Как: применение стилей поля страниц в SharePoint 2013](http://msdn.microsoft.com/library/e227613d-0e4d-4312-924d-bb55e1fe4293%28Office.15%29.aspx)
    
- [Инструкции. Создание макета страницы в SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx)
    
- [Как: Настройка макетов страниц для сайтов на основе каталога в SharePoint 2013](http://msdn.microsoft.com/library/21d8db99-73b3-4429-b6cb-04e375af9f55%28Office.15%29.aspx)
    
- [Как: сопоставление сетевого диска коллекции главных страниц SharePoint 2013](http://msdn.microsoft.com/library/7d416f6e-2471-4d03-97ae-4e8d907784c6%28Office.15%29.aspx)
