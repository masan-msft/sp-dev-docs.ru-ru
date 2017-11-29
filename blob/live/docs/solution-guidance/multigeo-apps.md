---
title: "Управление приложениями в SharePoint несколькими-географически клиентов"
ms.date: 11/08/2017
ms.openlocfilehash: c6131a1bc49f6bdcf7f4131a0699fc7d62bb8459
ms.sourcegitcommit: 26a4fb9cfe1ffcd266313c16f2afabfc841fdb71
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2017
---
# <a name="managing-apps-in-a-sharepoint-multi-geo-tenant"></a><span data-ttu-id="9d5a6-102">Управление приложениями в SharePoint несколькими-географически клиентов</span><span class="sxs-lookup"><span data-stu-id="9d5a6-102">Managing apps in a SharePoint Multi-Geo tenant</span></span>

> <span data-ttu-id="9d5a6-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="9d5a6-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="9d5a6-104">В географически нескольких клиентов вам придется каталога приложений одного географического расположения, что-то, выполняемых в учетной записи, если вы хотите развернуть ваших приложений в все географически подразделениях.</span><span class="sxs-lookup"><span data-stu-id="9d5a6-104">In a Multi-Geo tenant, you'll have an app catalog per geo location which is something to take in account if you want to deploy your apps across all geo locations.</span></span>

## <a name="where-do-i-need-to-deploy-my-apps-in-a-multi-geo-tenant"></a><span data-ttu-id="9d5a6-105">Где необходимо развернуть Мои приложения в географически нескольких клиентов?</span><span class="sxs-lookup"><span data-stu-id="9d5a6-105">Where do I need to deploy my apps in a Multi-Geo tenant?</span></span>
<span data-ttu-id="9d5a6-106">Прежде чем речь идет о развертывании приложения давайте сначала определите, что подразумевается с приложениями в этой статье: все приложения, развертываемым с первого их добавление в каталог приложений вашего клиента находятся в области данное руководство так, включающий SharePoint надстройки (так .app-файлы), но также Приложения SharePoint Framework и расширения (.sppkg-файлы).</span><span class="sxs-lookup"><span data-stu-id="9d5a6-106">Before talking about deploying apps let's first define what's meant with apps in this article: all apps that you deploy by first adding them to your tenant app catalog are in scope of this guidance, so that includes SharePoint Add-In's (so .app files) but also SharePoint Framework Apps and Extensions (the .sppkg files).</span></span> <span data-ttu-id="9d5a6-107">Один сайт каталога приложений в географически нескольких клиентов придется одного географического расположения, как показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="9d5a6-107">In a Multi-Geo tenant you'll have one app catalog site per geo location as show below:</span></span>

![World карты отображение каталога приложений в Северной Америке и вспомогательные расположений в Европе и Азии, с помощью каталога приложений](media/multigeo/multigeoapps_intro.png)

<span data-ttu-id="9d5a6-109">Вследствие данной архитектуры — это, что вам потребуется развернуть приложение в **все** каталоги приложений, если вы хотите, чтобы ваше приложение, чтобы оно было доступно для всех сайтов, независимо от расположения географически сайта, размещенной в.</span><span class="sxs-lookup"><span data-stu-id="9d5a6-109">A consequence of this architecture is that you'll need to deploy your app in **all** app catalogs if you want your app to be available for all sites, regardless of the geo location the site is hosted in.</span></span> <span data-ttu-id="9d5a6-110">Чтобы реализовать это у вас есть два варианта:</span><span class="sxs-lookup"><span data-stu-id="9d5a6-110">To realize this you have 2 options:</span></span>
- <span data-ttu-id="9d5a6-111">Развертывание приложения вручную на каждом из сайтов каталога приложения</span><span class="sxs-lookup"><span data-stu-id="9d5a6-111">Deploy your app manually in each of the app catalog sites</span></span>
- <span data-ttu-id="9d5a6-112">Использование API управления жизненным циклом Приложений для автоматизации развертывания приложений: с помощью этих API можно написать код, постоянно развертывает и обновления приложений в все расположения географически несколькими географически клиента.</span><span class="sxs-lookup"><span data-stu-id="9d5a6-112">Use the ALM API's to automate the deployment of your apps: using these API's you can write code that consistently deploys/upgrades your apps in all the geo locations of your Multi-Geo tenant.</span></span>


## <a name="see-also"></a><span data-ttu-id="9d5a6-113">См. также</span><span class="sxs-lookup"><span data-stu-id="9d5a6-113">See also</span></span>

- [<span data-ttu-id="9d5a6-114">Приложения SharePoint API управления жизненным циклом Приложений</span><span class="sxs-lookup"><span data-stu-id="9d5a6-114">SharePoint Apps ALM API's</span></span>]()
- [<span data-ttu-id="9d5a6-115">Развертывание и установка надстроек для SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="9d5a6-115">Deploying and installing SharePoint Add-ins: methods and options</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/sp-add-ins/deploying-and-installing-sharepoint-add-ins-methods-and-options)
- [<span data-ttu-id="9d5a6-116">Размещение клиентских веб-части из сети CDN Office 365</span><span class="sxs-lookup"><span data-stu-id="9d5a6-116">Hosting client-side web part from Office 365 CDN</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/web-parts/get-started/hosting-webpart-from-office-365-cdn)
- [<span data-ttu-id="9d5a6-117">Расширение узла из сети CDN Office 365</span><span class="sxs-lookup"><span data-stu-id="9d5a6-117">Host extension from Office 365 CDN</span></span>](https://docs.microsoft.com/en-us/sharepoint/dev/spfx/extensions/get-started/hosting-extension-from-office365-cdn) 


