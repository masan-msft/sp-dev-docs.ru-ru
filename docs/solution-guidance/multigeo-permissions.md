---
title: "Модель разрешений в OneDrive и SharePoint Online Preview несколькими географически"
ms.date: 11/03/2017
ms.openlocfilehash: 3f0d47ce0f791dd41dce8ca95e877e2e64a35c06
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="permission-model-in-onedrive-and-sharepoint-online-multi-geo-preview"></a><span data-ttu-id="e4895-102">Модель разрешений в OneDrive и SharePoint Online Preview несколькими географически</span><span class="sxs-lookup"><span data-stu-id="e4895-102">Permission model in OneDrive and SharePoint Online Multi-Geo Preview</span></span>

> <span data-ttu-id="e4895-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="e4895-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="e4895-104">Модель разрешений в OneDrive и SharePoint Online Preview несколькими географически клиентов совпадает с, для одного географически клиента.</span><span class="sxs-lookup"><span data-stu-id="e4895-104">The permission model in a OneDrive and SharePoint Online Multi-Geo Preview tenant is the same as that for a single geo tenant.</span></span>

<span data-ttu-id="e4895-105">Ферма с несколькими географически клиент имеет один распределены по всем все географического расположения среды Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4895-105">A Multi-Geo tenant has a single Azure AD environment distributed across all all geo locations.</span></span> <span data-ttu-id="e4895-106">Эта среда Azure AD включает в себя:</span><span class="sxs-lookup"><span data-stu-id="e4895-106">This Azure AD environment includes:</span></span> 

- <span data-ttu-id="e4895-107">Всех пользователей и групп — если предоставить разрешения пользователя или группы, эти разрешения применяются, чтобы все географического расположения.</span><span class="sxs-lookup"><span data-stu-id="e4895-107">All users and groups - If you grant a user or group permissions, these permissions apply to all geo locations.</span></span>
- <span data-ttu-id="e4895-108">Все участники безопасности - ли вы регистрируете приложение в Azure AD, с помощью одного из порталов Azure, а через службы управления доступом Azure (appregnew.aspx в SharePoint), предоставлены разрешения применяются к все географического расположения.</span><span class="sxs-lookup"><span data-stu-id="e4895-108">All security principals - Whether you register your application in Azure AD using one of the Azure Portals, or via Azure Access Control Services (appregnew.aspx in SharePoint), the permissions granted apply to all geo locations.</span></span>

<span data-ttu-id="e4895-109">На следующем рисунке показана ферма с несколькими географически клиента с:</span><span class="sxs-lookup"><span data-stu-id="e4895-109">The following image shows a Multi-Geo tenant with:</span></span>

- <span data-ttu-id="e4895-110">Расположение по умолчанию geo в Северной Америке</span><span class="sxs-lookup"><span data-stu-id="e4895-110">A default geo location in North America</span></span>
- <span data-ttu-id="e4895-111">Расположение вспомогательных geo в Европе</span><span class="sxs-lookup"><span data-stu-id="e4895-111">A satellite geo location in Europe</span></span>
- <span data-ttu-id="e4895-112">Расположение вспомогательных географически в Азии</span><span class="sxs-lookup"><span data-stu-id="e4895-112">A satellite geo location in Asia</span></span>

<span data-ttu-id="e4895-113">Этот клиент имеет один распределенной среде Azure Active Directory (Azure AD), который включает в себя всех пользователей, групп и разрешений.</span><span class="sxs-lookup"><span data-stu-id="e4895-113">This tenant has one distributed Azure Active Directory (Azure AD) environment that includes all the users, groups, and permissions.</span></span> <span data-ttu-id="e4895-114">Центральная экземпляра Azure AD, распространяется на все географического расположения.</span><span class="sxs-lookup"><span data-stu-id="e4895-114">The central Azure AD instance is distributed to all the geo locations.</span></span> 

![Карта мира, отображение географического расположения по умолчанию в Северной Америке и вспомогательные географически расположений в Европе и Азии, с помощью учетных записей пользователей и групп, хранящиеся в AAD](media/multigeo/multigeopermissions_intro.png)

<span data-ttu-id="e4895-116">Настройка приложений для клиентов несколькими географически в Azure AD, в статье [Set up несколькими географически примера приложения](multigeo-sampleapplicationsetup.md).</span><span class="sxs-lookup"><span data-stu-id="e4895-116">To configure your applications for Multi-Geo tenants in Azure AD, see [Set up a Multi-Geo sample application](multigeo-sampleapplicationsetup.md).</span></span>

