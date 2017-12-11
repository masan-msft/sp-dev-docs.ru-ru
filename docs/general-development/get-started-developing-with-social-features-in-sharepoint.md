---
title: "Приступая к разработке с использованием социальных функций в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8852ce36-8309-45a7-a141-2e10ac17a123
ms.openlocfilehash: c8ecb5d92ed472137c5053dcb46e81b6d7e72f5f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-developing-with-social-features-in-sharepoint"></a>Приступая к разработке с использованием социальных функций в SharePoint
Начало работы по программированию с социальными веб-каналами SharePoint и микроблога публикации, следуя людей и содержимое (документы, сайты и теги) и работа с профилями пользователей.

    
 [как управление социальными компонентами приложений и решений в?](get-started-developing-with-social-features-in-sharepoint.md#bk_HowToUseSocialFeatures)
  
    
    
 [Параметр среды разработки](get-started-developing-with-social-features-in-sharepoint.md#DevEnvironment)
  
    
    
 [сценарии разработки для социальных компонентов](get-started-developing-with-social-features-in-sharepoint.md#DevScenarios)
  
    
    
 [руководства по программированию с использованием социальных функций](get-started-developing-with-social-features-in-sharepoint.md#bk_GetStarted)
  
    
    
 [API-интерфейсы для программирования с использованием социальных функций](get-started-developing-with-social-features-in-sharepoint.md#SocialApis)
  
    
    
 [запроса разрешений для доступа к социальные функции](get-started-developing-with-social-features-in-sharepoint.md#bkmk_AppPerms)
  
    
    
 [Дополнительные ресурсы](get-started-developing-with-social-features-in-sharepoint.md#bk_AddResources)
  
    
    


## <a name="how-can-i-use-social-features-in-sharepoint-apps-and-solutions"></a>Использование социальных функций в SharePoint приложений и решений
<a name="bk_HowToUseSocialFeatures"> </a>

Социальные функции в приложений и решений SharePoint может помочь подключиться, обмениваться данными и совместно работать друг с другом и поиска, отслеживания и совместного использования важное содержимое и сведения о. Вы можете добавить новых социальных функций или расширяющих его возможности, которые уже доступны в SharePoint. Например можно создать приложение, которое позволяет находить и подписка на людей, которые имеют общие моменты, создание настраиваемой визуализации веб-канала данных или публикации пользовательских действий в веб-канал.
  
    
    
Возможности, описанные в этой статье выравнивание для пользователей, веб-каналов и дополнительные функциональные возможности, найдите на личных сайтов и веб-сайтов групп. Модель качества и репутации форум на сайты сообщества не предоставляют доступ к определенным интерфейсам API, поэтому использовать сайт SharePoint и список API-интерфейсы непосредственно к расширить. Для получения дополнительных сведений см  [Новый веб-узел сообщества](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md#bkmk_Collab).
  
    
    
Перед началом разработки, вы должны знать, где будет выполняться код, какая среда SharePoint, его можно было запускать на и какие функциональные возможности будет предоставлять. Эти факторы помогут выбрать тип приложения для создания и какие API-интерфейса или API-интерфейсы для использования. Сведения содержатся в разделе [Choose право API в SharePoint](choose-the-right-api-set-in-sharepoint.md) и [надстройки SharePoint по сравнению с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md) , которая поможет вам решить.
  
    
    

### <a name="setting-up-your-development-environment"></a>Настройка среды разработки
<a name="DevEnvironment"> </a>

Для начала разработки с использованием социальных функций, то необходимо:
  
    
    

- SharePoint или SharePoint Online
    
- Visual Studio 2012 или Visual Studio 2013 со средствами для разработчиков Office для Visual Studio 2013 — или более поздней версии
  

  
Дополнительные инструкции в разделе [Настройка среды Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md) и [Настройка компонентов социальных сетей в SharePoint](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx).
  
    
    

### <a name="development-scenarios-for-social-features-in-sharepoint"></a>Сценарии разработки для социальных функций в SharePoint
<a name="DevScenarios"> </a>

Сценарии разработки высокого уровня для социальных компонентов относятся работа с социальными веб-каналами, подписки на людей и содержимое (документы, сайты и теги) и работа со свойствами пользователей. В таблице 1 приведены ссылки на статьи с описанием основных интерфейсы API, которая используется для доступа к функции для каждого сценария и типичные задачи программирования.
  
    
    
В следующих статьях описываются основные интерфейсы API и задачи программирования для разработки конкретного сценария:
  
    
    

-  [Работа с социальными веб-каналами в SharePoint](work-with-social-feeds-in-sharepoint.md)
    
  
-  [Подписка на людей в SharePoint](follow-people-in-sharepoint.md)
    
  
-  [Подписка на контент в SharePoint](follow-content-in-sharepoint.md)
    
  
-  [Работа с профилями пользователей в SharePoint](work-with-user-profiles-in-sharepoint.md)
    
  

### <a name="how-tos-for-programming-with-social-features-in-sharepoint"></a>Руководства по программированию с использованием социальных функций в SharePoint
<a name="bk_GetStarted"> </a>

После того как настроить среду разработки и выберите сценария можно начать работу, программирование с использованием социальных функций. В таблице 1 приведены ссылки на статьи, в которых показано, как выполнять базовые задачи программирования с использованием социальных функций.
  
    
    

**В таблице 1. Статьи с инструкциями по разработке с использованием социальных функций**


|**Функциональная область**|**Описание**|
|:-----|:-----|
| [Как: сведения для чтения и записи социальных канал, чтобы с помощью клиентской объектной модели .NET в SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-net-client-object.md)|Познакомьтесь с помощью подробные инструкции по созданию приложения, которое считывает и записывает социальных канал, чтобы с помощью клиентской объектной модели .NET.|
| [Как: сведения для чтения и записи социальных канал с помощью службы REST в SharePoint](how-to-learn-to-read-and-write-to-the-social-feed-by-using-the-rest-service-in-s.md)|Познакомьтесь с помощью подробные инструкции по созданию приложения, которое считывает и записывает социальные веб-канал с помощью службы REST.|
| [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью клиентской объектной модели .NET в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-net-cli.md)|Узнайте, как создавать и удалять и публикации в микроблога и извлечение социальных веб-каналов с помощью клиентской объектной модели .NET.|
| [Как: Создание и удаление сообщений и извлечение социальных веб-канал с помощью объектной модели JavaScript в SharePoint](how-to-create-and-delete-posts-and-retrieve-the-social-feed-by-using-the-javascr.md)|Узнайте, как создавать и удалять и публикации в микроблога и извлечение социальных веб-каналов с помощью объектной модели JavaScript.|
| [Как добавлять в записи упоминания, теги и ссылки на сайты и документы в SharePoint](how-to-include-mentions-tags-and-links-to-sites-and-documents-in-posts-in-sharep.md)|Узнайте, как добавлять объекты **SocialDataItem** микроблога публикации, которые отображаются в виде упоминания, теги и ссылок в социальных веб-каналов.|
| [Как внедрять в записи изображения, видео и документы в SharePoint](how-to-embed-images-videos-and-documents-in-posts-in-sharepoint-server.md)|Узнайте, как добавлять объекты **SocialAttachment** микроблога публикации, которые отображаются в виде внедренного изображения, видео и документами в социальных веб-каналов.|
| [Как подписываться на пользователей, используя клиентскую объектную модель .NET в SharePoint](how-to-follow-people-by-using-the-net-client-object-model-in-sharepoint.md)|Узнайте, как работа с функциями следующих пользователей с помощью клиентской объектной модели .NET.|
| [Как подписываться на пользователей, используя объектную модель JavaScript в SharePoint](how-to-follow-people-by-using-the-javascript-object-model-in-sharepoint.md)|Узнайте, как работа с функциями следующих пользователей с помощью объектной модели JavaScript.|
| [Как подписываться на документы и сайты, используя клиентскую объектную модель .NET в SharePoint](how-to-follow-documents-and-sites-by-using-the-net-client-object-model-in-sharep.md)|Узнайте, как работа с функциями следующие контента с помощью клиентской объектной модели .NET.|
| [Как подписываться на документы, сайты и теги, используя службу REST в SharePoint](how-to-follow-documents-sites-and-tags-by-using-the-rest-service-in-sharepoint-2.md)|Узнайте, как работа с функциями следующие контента с помощью службы REST.|
| [Как: получение свойств профиля пользователя с помощью клиентской объектной модели .NET в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-net-client-object-model-in.md)|Узнайте, как получение свойств профиля пользователя с помощью клиентской объектной модели .NET.|
| [Инструкции. Получение свойств профиля пользователя с помощью объектной модели JavaScript в SharePoint](how-to-retrieve-user-profile-properties-by-using-the-javascript-object-model-in.md)|Узнайте, как получение свойств профиля пользователя с помощью объектной модели JavaScript.|
| [Инструкции. Работа с профилями пользователей и организации с использованием объектной модели сервера в SharePoint](how-to-work-with-user-profiles-and-organization-profiles-by-using-the-server-obj.md)|Узнайте, как создание, получение и управление свойства и профили пользователей с помощью объектной модели сервера.|
   

### <a name="apis-for-programming-with-sharepoint-social-features"></a>API-интерфейсы для программирования с использованием социальных функций SharePoint
<a name="SocialApis"> </a>

Несмотря на то, что приложений и решений для доступа к SharePoint по-разному, после доступа к SharePoint по сути так же, как используется социальные API. В таблице 2 показаны интерфейсы API для программирования с использованием веб-канал, выполнив, и профили пользователей возможности в SharePoint и пути к исходным файлам на сервере.
  
    
    

**В таблице 2. API-интерфейсы для программирования с использованием социальных функций**


|**Имя API**|**Источник и путь**|
|:-----|:-----|
| [Клиентская объектная модель .NET](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)|Библиотеке Microsoft.SharePoint.Client.UserProfiles.dll<br/>в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ISAPI|
|Клиентская объектная модель Silverlight|Microsoft.SharePoint.Client.UserProfiles.Silverlight.dll<br/>в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ШАБЛОНА\\МАКЕТОВ\\ClientBin|
|Клиентская объектная модель для мобильных устройств.|Microsoft.SharePoint.Client.UserProfiles.Phone.dll<br/>в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ШАБЛОНА\\МАКЕТОВ\\ClientBin|
| [Объектная модель JavaScript](http://msdn.microsoft.com/library/95cb5427-8514-4e9a-8eee-7ed4b82ec01b%28Office.15%29.aspx)|SP. UserProfiles.js<br/>в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ШАБЛОНА\\МАКЕТОВ|
|Служба передачи репрезентативного состояния (REST).| [`http://<site url>/_api/social.feed`](social-feed-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/social.following`](following-people-and-content-rest-api-reference-for-sharepoint.md)<br/>[`http://<site url>/_api/SP.UserProfiles.PeopleManager`](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx.md#bk_PeopleManager)|
| [Серверная объектная модель.](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)|Microsoft.Office.Server.UserProfiles.dll<br/>в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ISAPI|
   
> [!NOTE]
> [!Примечание] Не все функциональные возможности на сервере в сборке Microsoft.Office.Server.UserProfiles доступен из клиентских API-интерфейсов. Доступные API-интерфейсы см пространства имен  [Microsoft.SharePoint.Client.Social](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Social.aspx) и пространства имен [Microsoft.SharePoint.Client.UserProfiles](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.UserProfiles.aspx) .
  
    
    


## <a name="app-permission-requests-for-accessing-social-features-in-sharepoint-add-ins"></a>Запросы разрешений приложения для доступа к социальных функций в Надстройки SharePoint
<a name="bkmk_AppPerms"> </a>

Надстройка SharePoint должен запрашивать разрешения, необходимые для доступа к ресурсам SharePoint от пользователя, который установит ее. Например приложения, которая публикует веб-канал должен запрашивать разрешение **Write** (минимум) на канал. Укажите разрешения, которые приложения должны в AppManifest.xml файлов в Visual Studio.
  
    
    
Запросы разрешений приложения распространяются среда развертывания SharePoint. В таблице 3 перечислены имена областей (с соответствующей области коды URI) и доступные права на доступ к социальных функций. Дополнительные сведения можно [Добавить разрешения в SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx), [Add-in типы политик авторизации в SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx)и [Планирование управления разрешениями приложений в SharePoint](http://technet.microsoft.com/en-us/library/jj219576%28office.15%29.aspx).
  
    
    

**В таблице 3. Приложение области разрешений и доступные права для социальных функций в SharePoint**


|**Название области**|**Описание**|**Доступные права**|
|:-----|:-----|:-----|
|Профили пользователей<br/>`http://sharepoint/social/tenant`|Область запроса разрешений для доступа к все профили пользователей. Можно изменить только изображение профиля; все другие свойства профиля пользователя доступны только для чтения для Надстройки SharePoint. Необходимо установить, администратор клиента.|Чтение, запись, управление, полный доступ|
|Ядро<br/>`http://sharepoint/social/core`|Область запроса разрешений, используемые для доступа к его отслеживаемого содержимого и общих метаданных, которую использует функции микроблогов. Область применяется только к личные сайты, которые поддерживают следующие материалы. Если приложение устанавливается на любой другой тип сайта, используйте уровне клиентов.|Чтение, запись, управление, полный доступ|
|Веб-канал новостей<br/>`http://sharepoint/social/microfeed`|Область запроса разрешений для доступа к его веб-канал или канал группы. Область применяется для личных сайтов, поддерживающих микроблогов или сайты рабочих групп, где активирован компонент **Веб-каналов сайтов**. Если приложение устанавливается на любой другой тип сайта, используйте уровне клиентов.|Чтение, запись, управление, полный доступ|
| `http://sharepoint/social/trimming`|Эта область запроса разрешений, служит для определения, следует ли отображать контент обрезать безопасности социальных веб-канала к приложениям. Если это разрешение высоким уровнем доверия не предоставлено, часть содержимого (например, действия о документах и сайты, которые приложение не имеет разрешений на) обрезать из веб-канала данных, который возвращается в приложение даже в том случае, если у пользователя есть достаточные разрешения. Это разрешение необходимо вручную добавить в файл манифеста приложения.|Чтение, запись, управление, полный доступ|
   

### <a name="what-youll-need-to-consider-when-requesting-app-permissions"></a>Что необходимо учитывать при запросе разрешений приложения

Следует иметь в виду следующие соображения при указании приложения разрешения на использование социальных компонентов:
  
    
    

- Приложения, которые задают **FullControl** правами не допускается для Магазин Office приложений. Права **Read**, **Write**и **Manage** могут Магазин Office приложений.
    
  
- Можно задать разрешения для веб-каналов и следующие функции с помощью основных, канала новостей и областей клиента ( `http://sharepoint/content/tenant`). Область клиента представляет всей аренды установки приложения, включая областей ядро и веб-канал новостей. Поэтому если ваше приложение уже указывает права, которые требуется на уровне клиента, не нужно запрашивать разрешения на уровне ядра или веб-канал новостей.
    
  
- Во время разработки, используйте уровне клиентов, если вы получаете "SocialListNotFound: социальные списка не существует на личном узле" или «Файл не найден» сообщения. Если вы хотите использовать область основных или веб-канала новостей в вашем приложении, вы можете проверить разрешения, открыв приложения из каталога приложений.
    
  
- Основные области применяется к личные сайты, которые поддерживают следующие материалы. На уровне веб-канал новостей применяется для личных сайтов, поддерживающих микроблогов или сайты рабочих групп, где активирован компонент **Веб-каналов сайтов**. Если приложение будет установлен на любой другой тип сайта, необходимо использовать уровне клиентов. В разделе  [Сроки аренды и области развертывания надстроек для SharePoint](http://msdn.microsoft.com/library/1ceb3142-a7a5-453e-920f-5f953a79401a%28Office.15%29.aspx).
    
  
- Администратор клиента должен быть установлен приложений, запрашивающих права для области профили пользователей и их нельзя установить в версии Office 365 для малого бизнеса расширенный SharePoint Online.
    
  
- Если не выполняются требования к активации лицензирования или компонент для возможности социальных вычислений и микроблогов, пользователи получают сообщение о том, что они не могут установить приложение.
    
  
- Приложения, которые запускаются за пределами SharePoint может запрашивать разрешение на динамически (за исключением **Полный доступ**). Для получения дополнительных сведений см [процесс авторизации OAuth кода для SharePoint надстройки](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).
    
  

## <a name="see-also"></a>См. также
<a name="bk_AddResources"> </a>

 **Основные статьи**
  
    
    

-  [Социальные функции и функции совместной работы в SharePoint](social-and-collaboration-features-in-sharepoint.md)
    
  
-  [Новые возможности социальных сетей и совместной работы в SharePoint для разработчиков](what-s-new-for-developers-in-social-and-collaboration-features-in-sharepoint-201.md)
    
  
-  [Планирование социальных вычислений и совместной работы в SharePoint](http://technet.microsoft.com/en-us/library/ee662531%28v=office.15%29)
    
  
-  [Настройка компонентов социальных сетей в SharePoint](http://technet.microsoft.com/en-us/library/fp161267%28v=office.15%29.aspx)
    
  
-  [Социальные терминология и концепции сетей в SharePoint](http://technet.microsoft.com/en-us/library/jj219804%28v=office.15%29.aspx)
    
  
 **Справочная документация**
  
    
    

-  [Библиотека классов клиента социальных сетей](http://msdn.microsoft.com/library/9cc3f70c-78ac-4d2d-b46e-77522ee5d937%28Office.15%29.aspx)
    
  
-  [SP. Справочник по JavaScript UserProfiles.js](http://msdn.microsoft.com/library/80cf5436-6aa2-6f11-a782-66a04f6e2fb0%28Office.15%29.aspx)
    
  
-  [Social feed REST API reference for SharePoint](social-feed-rest-api-reference-for-sharepoint.md)
    
  
-  [Following people and content REST API reference for SharePoint](following-people-and-content-rest-api-reference-for-sharepoint.md)
    
  
-  [Справочник по API REST для профилей пользователей](http://msdn.microsoft.com/library/10757ed1-6e86-474f-89e0-6dec6aa66a2b%28Office.15%29.aspx)
    
  
-  [Библиотека классов сервера SharePoint социальных сетей](http://msdn.microsoft.com/library/87c5118c-ac0e-4bd9-a75f-7452a9eb0e41%28Office.15%29.aspx)
    
  
