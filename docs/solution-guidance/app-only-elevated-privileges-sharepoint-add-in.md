---
title: "Права только для приложений и с повышенными привилегиями в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 9bcdbe3f5bb31e0c01fac300bb237bf0134c84a1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
<a name="app-only-and-elevated-privileges-in-the-sharepoint-add-in-model"></a>Права только для приложений и с повышенными привилегиями в объектная модель SharePoint
===============================================================

<a name="summary"></a>Summary
-------

Подхода, можно повысить уровень привилегий в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы, RunWithElevatedPrivileges API используется с код на сервере объектной модели SharePoint и развернуты с помощью решений фермы.

В SharePoint надстройки модели сценарий, AllowAppOnlyPolicy разрешений или учетную запись службы используется для разрешения текущего пользователя для выполнения операций, они не авторизации для выполнения.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для повышения привилегий в коде.

- AllowAppOnlyPolicy не работает с 
    + Поиск — Если целевой объект локальная версия SharePoint. SharePoint Online поддержка добавлена ([запись в блоге](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))
    + Операции CSOM профиля пользователя, за исключением того, что можно использовать API обновления массового профилей пользователей с разрешениями только для приложений
    + Обновление записей службы таксономии (запись) — чтение works
    
    > [!NOTE] 
    > В следующих ситуациях необходимо использовать учетную запись службы.

- AllowAppOnlyPolicy аналогично RunWithElevatedPrivileges, но не точно так же.
    + AllowAppOnlyPolicy выполняет код на основании разрешения, предоставленные для SharePoint надстройки, не от имени другого пользователя, который имеет соответствующие разрешения на выполнение операции.

Ниже приведен пример возвращает маркер политики приложения и использовать его для создания объекта контекста.

    Uri siteUrl = new Uri(ConfigurationManager.AppSettings["MySiteUrl"]);
    try
    {
        //Connect to the give site using App Only token
        string realm = TokenHelper.GetRealmFromTargetUrl(siteUrl);
        var token = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUrl.Authority, realm).AccessToken;

        using (var ctx = TokenHelper.GetClientContextWithAccessToken(siteUrl.ToString(), token))
        {
            // Perform operations using the app only token access. 
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error in execution: " + ex.Message);
    }

- При использовании AllowAppOnlyPolicy, помните о работает только в размещенном у поставщика SharePoint надстройки.
- AllowAppOnlyPolicy не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.
- Учетные записи служб, определяются в SharePoint.
    + В клиента Office 365 в зависимости от функциональных возможностей у требований к коду, учетные записи служб может потребоваться лицензии Office 365, назначенные им.
    + Можно создать учетные записи служб на отдельных основы надстройки SharePoint или использование одной учетной записи для всех SharePoint надстройки.
    + Создание понятными и описательными имен для учетных записей служб, можно легко отслеживать операций, выполняемых ими.
    
    Например: Если надстройки SharePoint изменяет элементы списков, столбец Автор изменений для элементов списка отображается имя учетной записи службы, связанной с помощью надстройки SharePoint.

- При проверке подлинности с помощью учетных записей служб, вы должны получить имя пользователя и пароль для учетной записи службы.
    + Приведенный ниже фрагмент кода иллюстрирует, используя имя пользователя и пароль для проверки подлинности.
    + Будьте внимательны для хранения и извлечения имя пользователя и пароль безопасным образом.

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {
    
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<a name="options-to-elevate-permissions"></a>Параметры, чтобы повысить уровень разрешений
------------------------------

У вас есть две возможности повышения уровня разрешений.

- OAuth (AllowAppOnlyPolicy)
    + S2S (sub вариант)
    + ACS (sub вариант)
- Учетная запись службы
    + Удаленно размещенных кода (пример: Azure WebJob)

<a name="oauth-allowapponlypolicy"></a>OAuth (AllowAppOnlyPolicy)
--------------------------
В этом параметре AllowAppOnlyPolicy задано значение true в элемент AppPermissionRequests и разрешения, заданный в манифесте добавить в SharePoint. OAuth используется для получения маркера доступа, чтобы разрешить надстройки SharePoint для выполнения операций, имеющий разрешения на выполнение.

**Параметр sub S2S**

S2S sub параметр работает только в локальной среде SharePoint.

При проверке подлинности с помощью OAuth в сценарии S2S метод **TokenHelper::GetS2SAccessTokenWithWindowsIdentity** используется для получения маркера доступа для надстройки SharePoint.  Маркер доступа позволяет надстройки SharePoint для выполнения любых операций, предоставленные надстройки SharePoint в манифесте добавить в SharePoint.

Этот параметр не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.

**Когда это подходит?**

Если вам необходимо повысить уровень привилегий в сценарии SharePoint S2S это является хорошим выбором, поскольку этот параметр, для работы с S2S и очень просто реализовать.

**Приступая к работе**

Следующей статье показано, как использовать AllowAppOnlyPolicy с S2S.

- [Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

**Параметр sub ACS**

Параметр sub ACS работать в средах Office 365 SharePoint и локальных.

При проверке подлинности с помощью OAuth в сценарии ACS **TokenHelper::GetAppOnlyAccessTokenmethod** используется для получения маркера доступа для надстройки SharePoint.  Метод **TokenHelper::GetClientContextWithAccessToken** вызывается для возвращения контекста клиента, необходимые для выполнения каких-либо надстройки SharePoint имеет разрешения на выполнение операций, основанные на разрешения, предоставленные в манифесте добавить в SharePoint.

Этот параметр не выполняет код от имени пользователя и поэтому может быть неприемлема для всех сценариев.

**Когда это подходит?**

Если вам необходимо повысить уровень привилегий в сценарии SharePoint ACS это является хорошим выбором, поскольку этот параметр, для работы с ACS и очень просто реализовать.  Этот параметр используется подходит, если у вас есть в локальной среде SharePoint, имеющей отношения доверия с ACS.  Это единственным вариантом OAuth, когда у вас есть в среде Office 365 SharePoint.

**Приступая к работе**

В следующей статье демонстрируется использование AllowAppOnlyPolicy с ACS.

- [Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)

<a name="service-account"></a>Учетная запись службы
---------------
В этом шаблоне класс SharePointOnlineCredentials используется для установки контекста пользователя, который выполняет код.

**Когда это подходит?**

Для выполнения кода от имени определенного пользователя (учетная запись службы) это является хорошим выбором, так как он выполняет действия на пользователя (учетная запись службы) и разрешений SharePoint надстройки.

**Приступая к работе**

В следующей статье описывается, как класс SharePointOnlineCredentials используется для установки контекста пользователя, который выполняет код.

- [Начало работы по построению WebJobs Azure («задания таймера») для Office 365 сайтов (раздел сведения о выполнении проверки подлинности) - статья блога Zimmergren Тобиаса](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)

<a name="related-links"></a>Ссылки по теме
=============
- [Приложения для SharePoint 2013 только политики более простой (Петров Кирк — публикация в блоге MSDN)](http://blogs.msdn.com/b/kaevans/archive/2013/02/23/sharepoint-2013-app-only-policy-made-easy.aspx)
- [Начало работы по построению WebJobs Azure («задания таймера») для Office 365 сайтов (раздел сведения о выполнении проверки подлинности) - статья блога Zimmergren Тобиаса](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites)
- [Класс SharePointOnlineCredentials (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.sharepointonlinecredentials.aspx)
- [С помощью надстройки только аудио- и только разрешения с помощью запросов поиска в SharePoint Online — на статья блога Vesa Juvonen](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Core.SimpleTimerJob (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- Примеры и содержимое в https://github.com/SharePoint/PnP

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D) *частично*
- SharePoint 2013 в локальной — *частично*

*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*
