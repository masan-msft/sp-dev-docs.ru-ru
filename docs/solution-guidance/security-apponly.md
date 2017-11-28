# <a name="accessing-sharepoint-using-an-application-context-also-known-as-app-only"></a>Доступ к SharePoint, используя контекст приложения, также известной как доступный только для приложений

Существует два подхода для этого только для приложений для SharePoint. 
 - С помощью **приложения Azure AD**: этот метод является предпочтительным при использовании SharePoint Online, так как вы также можете предоставить разрешения на другие службы Office 365 (при необходимости) + был добавлен пользовательский интерфейс (портала управления Azure) для поддержки участников вашего приложения.
 - С помощью **участника только для приложений SharePoint**: этот метод работе старых и только для доступа к SharePoint, но по-прежнему относится. Этот метод также является рекомендованной моделью при по-прежнему работе в SharePoint в локальной с момента работает эту модель в SharePoint в локальной как SharePoint Online.

Оба метода подробно рассмотрены в следующих статьях: 
 - [Предоставление доступа с помощью Azure AD только для приложений](security-apponly-azuread.md)
 - [Предоставление доступа с помощью SharePoint только для приложений](security-apponly-azureacs.md)

## <a name="what-are-the-limitations-when-using-app-only"></a>Какие существуют ограничения при использовании только приложения
Только для приложений, не работает в следующих случаях:
 - Обновление записей службы таксономии (запись) — чтение works
 - Создание веб-сайтов групп современных не поддерживает только когда [использовать SharePoint API](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Sites/SiteCollection.cs) для него. При создании веб-сайтов современных групп [с помощью Microsoft Graph](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Framework/Graph/UnifiedGroupsUtility.cs) нажмите Создать группу только для приложений является Поддерживаемые сценарии
 - Создание связи сайтов в настоящее время не поддерживает только для приложений [с помощью SharePoint API](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Sites/SiteCollection.cs)
 - Поиск при использовании SharePoint локально. SharePoint Online поддержка добавлена ([запись в блоге](https://blogs.msdn.microsoft.com/vesku/2016/03/07/using-add-in-only-app-only-permissions-with-search-queries-in-sharepoint-online/))
 - Операции CSOM профиля пользователя, за исключением того, что можно использовать API обновления массового профилей пользователей с разрешениями только для приложений
 - Управление файлами с помощью протокола WebDav и CSOM (с помощью `File.SaveBinaryDirect`) не работает с только для приложений

> [!IMPORTANT]
> Если выше сценариев критически важные для вас рекомендуется для определения учетной записи службы, предоставить его разрешения и затем использовать его в приложении. В разделе Пример [Governance.EnsurePolicy](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.EnsurePolicy) для получения дополнительных сведений о как предоставить широкий разрешения для учетной записи службы клиента. Статьи о том, используется [альтернативный модель для политик web app в SharePoint Online](security-webapppolicies.md) содержать много информации по этой теме.



