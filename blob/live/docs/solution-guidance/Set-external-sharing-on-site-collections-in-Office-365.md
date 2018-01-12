---
title: "Задайте внешний общий доступ через семейств веб-сайтов в Office 365"
ms.date: 11/03/2017
ms.openlocfilehash: 77dcda34649a2d4d3a19e07b161c623d8db26de3
ms.sourcegitcommit: 7b6ce94b477d9b587beaa059eb9aa7cd6235efde
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="set-external-sharing-on-site-collections-in-office-365"></a><span data-ttu-id="2155d-102">Задайте внешний общий доступ через семейств веб-сайтов в Office 365</span><span class="sxs-lookup"><span data-stu-id="2155d-102">Set external sharing on site collections in Office 365</span></span>

<span data-ttu-id="2155d-103">Можно управлять внешний общий доступ параметров в семействе сайтов SharePoint в Office 365, что позволяет внешним пользователям (пользователям, у которых нет учетной записи организации в подписки Office 365) доступ к семейству веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="2155d-103">You can control external sharing settings on a SharePoint site collection in Office 365, allowing external users (users who don't have an organization account in your Office 365 subscription) access to your site collection.</span></span>

<span data-ttu-id="2155d-104">_**Применимо к:** надстройки для SharePoint | SharePoint Online | Office 365_</span><span class="sxs-lookup"><span data-stu-id="2155d-104">_**Applies to:** add-ins for SharePoint | SharePoint Online | Office 365_</span></span>

<span data-ttu-id="2155d-105">Пример кода [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) показано, как управлять внешние параметры общего доступа в семействе сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2155d-105">The  [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) code sample shows you how to control your external sharing settings on a SharePoint site collection.</span></span> <span data-ttu-id="2155d-106">Используйте для этого решения:</span><span class="sxs-lookup"><span data-stu-id="2155d-106">Use this solution to:</span></span>

- <span data-ttu-id="2155d-107">Элемент управления внешние параметры общего доступа во время процесса подготовки сайта.</span><span class="sxs-lookup"><span data-stu-id="2155d-107">Control external sharing settings during your site provisioning process.</span></span>
    
- <span data-ttu-id="2155d-108">Подготовка семейства веб-сайтов для общего доступа с внешними пользователями.</span><span class="sxs-lookup"><span data-stu-id="2155d-108">Prepare your site collection for sharing with external users.</span></span>

> [!NOTE] 
> <span data-ttu-id="2155d-109">Параметры внешнего совместного доступа доступны только в Office 365.</span><span class="sxs-lookup"><span data-stu-id="2155d-109">External sharing settings are only available in Office 365.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2155d-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2155d-110">Before you begin</span></span>
<span data-ttu-id="2155d-111"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="2155d-111"></span></span>

<span data-ttu-id="2155d-112">Чтобы начать работу, загрузите пример надстройки [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="2155d-112">To get started, download the  [Core.ExternalSharing](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ExternalSharing) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreexternalsharing-app"></a><span data-ttu-id="2155d-113">С помощью приложения Core.ExternalSharing</span><span class="sxs-lookup"><span data-stu-id="2155d-113">Using the Core.ExternalSharing app</span></span>
<span data-ttu-id="2155d-114"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="2155d-114"></span></span>

<span data-ttu-id="2155d-115">Убедитесь в том, что подписка Office 365 позволяет внешний общий доступ.</span><span class="sxs-lookup"><span data-stu-id="2155d-115">Verify that your Office 365 subscription allows external sharing.</span></span> <span data-ttu-id="2155d-116">Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2155d-116">To do this:</span></span>

1. <span data-ttu-id="2155d-117">Откройте созданный вами **Центр администрирования Office 365**.</span><span class="sxs-lookup"><span data-stu-id="2155d-117">Open your  **Office 365 admin center**.</span></span>
    
2. <span data-ttu-id="2155d-118">В меню навигации слева выберите пункт **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="2155d-118">On the left navigation menu, choose **SharePoint**.</span></span>
    
3. <span data-ttu-id="2155d-119">В меню навигации слева нажмите кнопку **общий доступ**.</span><span class="sxs-lookup"><span data-stu-id="2155d-119">On the left navigation menu, choose  **Sharing**.</span></span>
    
4. <span data-ttu-id="2155d-120">В **общий доступ за пределами вашей организации**убедитесь, что **Разрешить пользователям приглашать и обмен информацией с проверкой подлинности внешних пользователей** **на**.</span><span class="sxs-lookup"><span data-stu-id="2155d-120">In  **Sharing outside your organization**, ensure that  **Allow users to invite and share with authenticated external users** is **On**.</span></span>
    
<span data-ttu-id="2155d-121">Проверьте параметры внешних сайтов в семействе веб-сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2155d-121">Verify your external site settings on your SharePoint site collection.</span></span> <span data-ttu-id="2155d-122">Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="2155d-122">To do this:</span></span>

1. <span data-ttu-id="2155d-123">Откройте созданный вами **Центр администрирования Office 365**.</span><span class="sxs-lookup"><span data-stu-id="2155d-123">Open your  **Office 365 admin center**.</span></span>
    
2. <span data-ttu-id="2155d-124">В меню навигации слева нажмите кнопку **SharePoint** , чтобы открыть в **центре администрирования SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="2155d-124">On the left navigation menu, choose  **SharePoint** to open your **SharePoint admin center**.</span></span>
    
3. <span data-ttu-id="2155d-125">В списке семейства сайтов установите флажок рядом с URL-адрес семейства сайтов, чтобы проверить параметры внешнего совместного доступа на.</span><span class="sxs-lookup"><span data-stu-id="2155d-125">In the Site Collection List, select the check box next to the site collection URL that you want to verify your external sharing settings on.</span></span>
    
4. <span data-ttu-id="2155d-126">На ленте выберите **общий доступ**.</span><span class="sxs-lookup"><span data-stu-id="2155d-126">On the ribbon, choose  **Sharing**.</span></span>
    
5. <span data-ttu-id="2155d-127">Просмотрите внешние параметры общего доступа в диалоговом окне **общий доступ** .</span><span class="sxs-lookup"><span data-stu-id="2155d-127">Review your external sharing settings in the  **sharing** dialog.</span></span> <span data-ttu-id="2155d-128">После запуска этого примера кода, вернуться в диалоговое окно **общего доступа к** , чтобы убедиться, что изменены внешние параметры общего доступа.</span><span class="sxs-lookup"><span data-stu-id="2155d-128">After running the code sample, return to the **sharing** dialog to verify that your external sharing settings changed.</span></span>
    
<span data-ttu-id="2155d-129">При запуске в этом примере кода **Main** в файле Program.cs выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2155d-129">When you run this code sample,  **Main** in Program.cs performs the following tasks:</span></span>

- <span data-ttu-id="2155d-130">Получает URL-адрес центра администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2155d-130">Gets the SharePoint admin center URL.</span></span>
    
- <span data-ttu-id="2155d-131">Получает URL-адрес семейства сайтов для настройки параметров внешнего совместного доступа на.</span><span class="sxs-lookup"><span data-stu-id="2155d-131">Gets the site collection URL to configure external sharing settings on.</span></span>
    
- <span data-ttu-id="2155d-132">Получает учетные данные администратора Office 365.</span><span class="sxs-lookup"><span data-stu-id="2155d-132">Gets your Office 365 administrator credentials.</span></span>
    
- <span data-ttu-id="2155d-133">Вызывает **GetInputSharing**, который выдает запрос пользователю выбрать внешний общего доступа ( [SharingCapabilities](https://msdn.microsoft.com/library/office/microsoft.online.sharepoint.tenantmanagement.sharingcapabilities.aspx)) необходимо применить параметр настройки для семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="2155d-133">Calls  **GetInputSharing**, which prompts the user to choose an external sharing setting ( [SharingCapabilities](https://msdn.microsoft.com/library/office/microsoft.online.sharepoint.tenantmanagement.sharingcapabilities.aspx)) to apply to the site collection.</span></span> <span data-ttu-id="2155d-134">Следующие внешние параметры параметры общего доступа:</span><span class="sxs-lookup"><span data-stu-id="2155d-134">The external sharing settings choices include:</span></span>
    
    -  <span data-ttu-id="2155d-135">**Отключено**, которая отключает внешний общий доступ на сайте.</span><span class="sxs-lookup"><span data-stu-id="2155d-135">**Disabled**, which turns off external sharing on the site.</span></span>
    
    -  <span data-ttu-id="2155d-136">**ExternalUserAndGuestSharing**, что позволит внешних пользователей и гостевой общего доступа на сайте.</span><span class="sxs-lookup"><span data-stu-id="2155d-136">**ExternalUserAndGuestSharing**, which enables external user and guest sharing on the site.</span></span>
    
    -  <span data-ttu-id="2155d-137">**ExternalUserSharingOnly**, которое позволяет внешних пользователей только общий доступ.</span><span class="sxs-lookup"><span data-stu-id="2155d-137">**ExternalUserSharingOnly**, which enables external user sharing only.</span></span>
    
- <span data-ttu-id="2155d-138">Вызывает **SetSiteSharing**.</span><span class="sxs-lookup"><span data-stu-id="2155d-138">Calls  **SetSiteSharing**.</span></span>

> [!NOTE] 
> <span data-ttu-id="2155d-139">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="2155d-139">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="2155d-140">**SetSiteSharing** выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2155d-140">**SetSiteSharing** does the following:</span></span>

-  <span data-ttu-id="2155d-141">**Tenant.GetSitePropertiesByUrl** используется для получения **SiteProperties** в семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="2155d-141">Uses the **Tenant.GetSitePropertiesByUrl** to retrieve **SiteProperties** on your site collection.</span></span>
    
- <span data-ttu-id="2155d-142">Используется **Tenant.SharingCapability** , чтобы определить, включена ли внешний общий доступ на подписки Office 365.</span><span class="sxs-lookup"><span data-stu-id="2155d-142">Uses  **Tenant.SharingCapability** to determine whether external sharing is enabled on your Office 365 subscription.</span></span>
    
-  <span data-ttu-id="2155d-143">Если общий доступ к включен в подписки Office 365, задается **SiteProperties.SharingCapability** параметры внешнего совместного доступа, введенные пользователем.</span><span class="sxs-lookup"><span data-stu-id="2155d-143">If sharing is enabled in your Office 365 subscription, sets the **SiteProperties.SharingCapability** to the external sharing settings the user entered.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="2155d-144">См. также</span><span class="sxs-lookup"><span data-stu-id="2155d-144">See also</span></span>
<span data-ttu-id="2155d-145"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2155d-145"></span></span>

-  [<span data-ttu-id="2155d-146">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="2155d-146">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="2155d-147">Управление внешний общий доступ для среды SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2155d-147">Manage external sharing for your SharePoint Online environment</span></span>](https://support.office.com/article/Manage-external-sharing-for-your-SharePoint-Online-environment-C8A462EB-0723-4B0B-8D0A-70FEAFE4BE85)
