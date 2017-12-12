---
title: "Задайте внешний общий доступ через семейств веб-сайтов в Office 365"
ms.date: 11/03/2017
ms.openlocfilehash: d98140a1502efce34ebe60112dfc201aa3336785
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="set-external-sharing-on-site-collections-in-office-365"></a>Задайте внешний общий доступ через семейств веб-сайтов в Office 365

Можно управлять внешний общий доступ параметров в семействе сайтов SharePoint в Office 365, что позволяет внешним пользователям (пользователям, у которых нет учетной записи организации в подписки Office 365) доступ к семейству веб-сайтов.

_**Применимо к:** надстройки для SharePoint | SharePoint Online | Office 365_

Пример кода [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) показано, как управлять внешние параметры общего доступа в семействе сайтов SharePoint. Используйте для этого решения:

- Элемент управления внешние параметры общего доступа во время процесса подготовки сайта.
    
- Подготовка семейства веб-сайтов для общего доступа с внешними пользователями.

> [!NOTE] 
> Параметры внешнего совместного доступа доступны только в Office 365.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-coreexternalsharing-app"></a>С помощью приложения Core.ExternalSharing
<a name="sectionSection1"> </a>

Убедитесь в том, что подписка Office 365 позволяет внешний общий доступ. Для этого сделайте следующее.

1. Откройте созданный вами **Центр администрирования Office 365**.
    
2. В меню навигации слева нажмите кнопку **Внешний общий доступ**.
    
3. Нажмите кнопку **общий доступ к Обзор**.
    
4. На **сайтах**убедитесь, что **позволяет внешний доступ к сайтам** **на**.
    
Проверьте параметры внешних сайтов в семействе веб-сайтов SharePoint. Для этого сделайте следующее.

1. Откройте созданный вами **Центр администрирования Office 365**.
    
2. В меню навигации слева нажмите кнопку **SharePoint** , чтобы открыть в **центре администрирования SharePoint**.
    
3. Установите флажок рядом с URL-адрес семейства сайтов, чтобы проверить параметры внешнего совместного доступа на.
    
4. На ленте выберите **общий доступ**.
    
5. Просмотрите внешние параметры общего доступа в диалоговом окне **общий доступ** . После запуска этого примера кода, вернуться в диалоговое окно **общего доступа к** , чтобы убедиться, что изменены внешние параметры общего доступа.
    
При запуске в этом примере кода **Main** в файле Program.cs выполняет следующие задачи:

- Получает URL-адрес центра администрирования Office 365.
    
- Получает URL-адрес семейства сайтов для настройки параметров внешнего совместного доступа на.
    
- Получает учетные данные администратора Office 365.
    
- Вызывает **GetInputSharing**, который выдает запрос пользователю выбрать внешний общего доступа ( [SharingCapabilities](https://msdn.microsoft.com/library/office/microsoft.online.sharepoint.tenantmanagement.sharingcapabilities.aspx)) необходимо применить параметр настройки для семейства веб-сайтов. Следующие внешние параметры параметры общего доступа:
    
    -  **Отключено**, которая отключает внешний общий доступ на сайте.
    
    -  **ExternalUserAndGuestSharing**, что позволит внешних пользователей и гостевой общего доступа на сайте.
    
    -  **ExternalUserSharingOnly**, которое позволяет внешних пользователей только общий доступ.
    
- Вызывает **SetSiteSharing**.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
 static void Main(string[] args)
        {
           
            /* Prompt for your Office 365 admin center URL*/
            Console.WriteLine("Enter your Tenant Admin URL for your Office 365 subscription:");
            string tenantAdminURL = GetSite();

            /* End Program if no Office 365 admin center URL is supplied*/
            if (string.IsNullOrEmpty(tenantAdminURL))
            {
                Console.WriteLine("Hmm, i tried to work on it but you didn't supply your admin tenant url:");
                return;
            }
               
            // Prompt the user for an Office365 site collection 
            Console.WriteLine("Enter your Office 365 Site Collection URL:");
            string siteUrl = GetSite();

            /* Prompt for Credentials */
            Console.WriteLine("Enter Credentials for your Office 365 Site Collection {0}:", siteUrl);

            string userName = GetUserName();
            SecureString pwd = GetPassword();

            /* End program if no credentials are entered */
            if (string.IsNullOrEmpty(userName) || (pwd == null))
            {
                Console.WriteLine("Hmm, i tried to work on it but you didn't supply your credentials:");
                return;
            }

            try 
            {
                SharingCapabilities _sharingSettingToApply = GetInputSharing(siteUrl);
                using (ClientContext cc = new ClientContext(tenantAdminURL))
                { 
                    cc.AuthenticationMode = ClientAuthenticationMode.Default;
                    cc.Credentials = new SharePointOnlineCredentials(userName, pwd);
                    SetSiteSharing(cc, siteUrl, _sharingSettingToApply);
                }
            }
            catch(Exception ex)
            {
                Console.WriteLine("Oops, Mistakes can happen to anyone. An Error occured : {0}", ex.Message);
               
            }

            Console.WriteLine("Hit Enter to exit.");
            Console.Read();

        
        }
```

**SetSiteSharing** выполняет следующие действия:

-  **Tenant.GetSitePropertiesByUrl** используется для получения **SiteProperties** в семействе веб-сайтов.
    
- Используется **Tenant.SharingCapability** , чтобы определить, включена ли внешний общий доступ на подписки Office 365.
    
-  Если общий доступ к включен в подписки Office 365, задается **SiteProperties.SharingCapability** параметры внешнего совместного доступа, введенные пользователем.

```C#
public static void SetSiteSharing(ClientContext adminCC, string siteCollectionURl, SharingCapabilities shareSettings)
        {
            var _tenantAdmin = new Tenant(adminCC);
            SiteProperties _siteprops = _tenantAdmin.GetSitePropertiesByUrl(siteCollectionURl, true);
            adminCC.Load(_tenantAdmin);
            adminCC.Load(_siteprops);
            adminCC.ExecuteQuery();

            SharingCapabilities _tenantSharing = _tenantAdmin.SharingCapability;
            var _currentShareSettings = _siteprops.SharingCapability;
            bool _isUpdatable = false;

            if(_tenantSharing == SharingCapabilities.Disabled)
            {
                Console.WriteLine("Sharing is currently disabled in your tenant! I am unable to work on it.");
            }
            else
            {  
                if(shareSettings == SharingCapabilities.Disabled)
                { _isUpdatable = true; }
                else if(shareSettings == SharingCapabilities.ExternalUserSharingOnly)
                {
                    _isUpdatable = true;   
                }
                else if (shareSettings == SharingCapabilities.ExternalUserAndGuestSharing)
                {
                    if (_tenantSharing == SharingCapabilities.ExternalUserAndGuestSharing)
                    {
                        _isUpdatable = true;
                    }
                    else
                    {
                        Console.WriteLine("ExternalUserAndGuestSharing is currently disabled in your tenant! I am unable to work on it.");
                    }
                }
            }
            if (_currentShareSettings != shareSettings &amp;&amp; _isUpdatable)
            {
                _siteprops.SharingCapability = shareSettings;
                _siteprops.Update();
                adminCC.ExecuteQuery();
                Console.WriteLine("Set Sharing on site {0} to {1}.", siteCollectionURl, shareSettings);
            }
        }
```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Управление внешний общий доступ для среды SharePoint Online](https://support.office.com/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85)
