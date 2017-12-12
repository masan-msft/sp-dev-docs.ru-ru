---
title: "Каким образом можно обеспечить клиента только добавить в приложение административных разрешений в SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 48104bb22245a27be487685f8f668b0de2c559b5
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
<a name="how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online"></a><span data-ttu-id="f2b97-102">Каким образом можно обеспечить клиента только добавить в приложение административных разрешений в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f2b97-102">How to provide add-in app only tenant administrative permissions in SharePoint Online</span></span>
================================================

<span data-ttu-id="f2b97-103">При разработке надстройки SharePoint зарегистрировать их с помощью модели ACS (appregnew.aspx и appinv.aspx) необходимо следовать специальный процесс, если надстройка запрашивает разрешения администратора клиента и в режиме только для приложений.</span><span class="sxs-lookup"><span data-stu-id="f2b97-103">When you are developing SharePoint add-ins and want to register them using the ACS model (appregnew.aspx and appinv.aspx), you will need to follow a special process, when an add-in is requesting tenant admin permissions and in app-only mode.</span></span> 

<span data-ttu-id="f2b97-104">Шаги для предоставления разрешений администратора для приложения клиента только надстройки:</span><span class="sxs-lookup"><span data-stu-id="f2b97-104">Steps to provide tenant admin permission for app only add-in:</span></span>

- <span data-ttu-id="f2b97-105">Зарегистрируйте идентификатор приложения для надстройки в разделе семейства обычных веб-сайтов в клиентов, где будет развертываться надстройки.</span><span class="sxs-lookup"><span data-stu-id="f2b97-105">Register app id for the add-in under normal site collection in the tenant where add-in will be deployed.</span></span> 
  - <span data-ttu-id="f2b97-106">URL-адрес: *https://[tenant].sharepoint.com/_layouts/15/appregnew.aspx*</span><span class="sxs-lookup"><span data-stu-id="f2b97-106">URL: *https://[tenant].sharepoint.com/_layouts/15/appregnew.aspx*</span></span>
- <span data-ttu-id="f2b97-107">Укажите необходимые сведения о регистрации надстройки и зарегистрировать идентификатор и секрет для надстройки</span><span class="sxs-lookup"><span data-stu-id="f2b97-107">Provide necessary details for the add-in registration and register ID and secret for your add-in</span></span>
- <span data-ttu-id="f2b97-108">Перемещение на страницу appinv.aspx в области сайта администрирования клиентов</span><span class="sxs-lookup"><span data-stu-id="f2b97-108">Move to appinv.aspx page under your tenant admin site</span></span>
  - <span data-ttu-id="f2b97-109">URL-адрес: *https://[tenant]-admin.sharepoint.com/_layouts/15/appinv.aspx*</span><span class="sxs-lookup"><span data-stu-id="f2b97-109">URL: *https://[tenant]-admin.sharepoint.com/_layouts/15/appinv.aspx*</span></span>
- <span data-ttu-id="f2b97-110">Выполните поиск для идентификатора приложения, зарегистрированные в предыдущие действия, описанные в appinv.aspx страницы</span><span class="sxs-lookup"><span data-stu-id="f2b97-110">Perform a lookup for the app id registered in previous steps in appinv.aspx page</span></span>
- <span data-ttu-id="f2b97-111">Предоставить необходимые разрешения для регистрации надстроек</span><span class="sxs-lookup"><span data-stu-id="f2b97-111">Provide needed permissions for your add-in registration</span></span>
- <span data-ttu-id="f2b97-112">Выполнение доверия для регистрации обновленные надстроек</span><span class="sxs-lookup"><span data-stu-id="f2b97-112">Perform trust for the updated add-in registration</span></span>

<span data-ttu-id="f2b97-113">Обратите внимание, что эта операция должна выполняться в разделе сайт администрирования клиентов и учетная запись, используемая для выполнения этих операций необходимо иметь права администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="f2b97-113">Notice that this operation has to be completed under the tenant administration site and account used for these operations will need to have tenant administrative permissions.</span></span> <span data-ttu-id="f2b97-114">Если нужно предоставить разрешения на нижнем уровне для надстройки, следует выполнить те, в разделе URL-адреса семейства обычный сайт с разрешениями более низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="f2b97-114">If you are providing lower level permissions for your add-in, you can complete those under normal site collection URLs with lower permissions.</span></span> 


## <a name="see-also"></a><span data-ttu-id="f2b97-115">См. также</span><span class="sxs-lookup"><span data-stu-id="f2b97-115">See also</span></span>
<span data-ttu-id="f2b97-116"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f2b97-116"></span></span>

- [<span data-ttu-id="f2b97-117">Регистрация надстроек для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f2b97-117">Register SharePoint Add-ins 2013</span></span>](https://msdn.microsoft.com/en-us/library/office/jj687469.aspx)
    
- [<span data-ttu-id="f2b97-118">Разрешения для надстроек в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="f2b97-118">Add-in permissions in SharePoint 2013</span></span>](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)

