---
title: "Средства и среды для разработки надстроек SharePoint"
description: "Узнайте, как создать среду разработки надстроек SharePoint на сайте SharePoint Online или в локальной ферме."
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 22c5a3cdff4d7d829a401edd1b170aafd6ca577d
ms.sourcegitcommit: 074f3a7983a7b253f56f8c670a0290c27bb7734b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a><span data-ttu-id="ecbf1-103">Средства и среды для разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="ecbf1-103">Tools and environments for developing SharePoint Add-ins</span></span>

<span data-ttu-id="ecbf1-104">Существует два основных шаблона сред для разработки надстроек SharePoint. Веб-сайт SharePoint для тестирования и разработки может находиться:</span><span class="sxs-lookup"><span data-stu-id="ecbf1-104">There are two basic patterns for development environments for SharePoint Add-ins. The test and debugging SharePoint website can be on:</span></span>

-  <span data-ttu-id="ecbf1-105">**на веб-сайте SharePoint Online в подписке Office 365.**</span><span class="sxs-lookup"><span data-stu-id="ecbf1-105">**A SharePoint Online website in an Office 365 subscription.**</span></span> <span data-ttu-id="ecbf1-106">Как правило, среда Visual Studio устанавливается на локальном компьютере, но ее также можно развернуть в облаке;</span><span class="sxs-lookup"><span data-stu-id="ecbf1-106">The test and debugging SharePoint website is in a SharePoint Online website in an Office 365 subscription. Typically, Visual Studio is installed to a local computer, but a cloud-based Visual Studio is also an option.</span></span>

-  <span data-ttu-id="ecbf1-107">**в локальной ферме SharePoint с одним сервером.**</span><span class="sxs-lookup"><span data-stu-id="ecbf1-107">**An on-premises, one-server SharePoint farm.**</span></span> <span data-ttu-id="ecbf1-108">Visual Studio устанавливается на том же компьютере.</span><span class="sxs-lookup"><span data-stu-id="ecbf1-108">Visual Studio is installed on the same computer.</span></span>
 
<span data-ttu-id="ecbf1-109">Примите во внимание следующее:</span><span class="sxs-lookup"><span data-stu-id="ecbf1-109">Consider the following:</span></span>

- <span data-ttu-id="ecbf1-110">Практически любую создаваемую надстройку можно развернуть в SharePoint Online или локальных фермах SharePoint независимо от типа используемой среды.</span><span class="sxs-lookup"><span data-stu-id="ecbf1-110">Almost any add-in that you create can be deployed to either SharePoint Online or to on-premises SharePoint farms, regardless of which type of environment you use.</span></span> <span data-ttu-id="ecbf1-111">В целом, надстройки, которые невозможно развернуть в SharePoint Online, также невозможно разрабатывать с помощью этой среды. Например, это относится к надстройкам, требующим [разрешения уровня "Полный доступ"](add-in-permissions-in-sharepoint.md) и использующим [систему авторизации с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf1-111">Almost any add-in you create can be deployed to either SharePoint Online or to on-premise SharePoint farms, regardless of which type of environment you use. As a general rule, add-ins that cannot be deployed to SharePoint Online also cannot be developed with it. Examples: add-ins that require  [Full Control permissions](add-in-permissions-in-sharepoint.md) and add-ins that use the [high-trust authorization system](creating-sharepoint-add-ins-that-use-high-trust-authorization.md).</span></span>

- <span data-ttu-id="ecbf1-112">Вы можете разрабатывать надстройки, размещаемые как в SharePoint, так и у поставщика, независимо от типа используемой среды.</span><span class="sxs-lookup"><span data-stu-id="ecbf1-112">You can develop both SharePoint-hosted and provider-hosted SharePoint Add-ins, regardless of which type of environment you use.</span></span>

- <span data-ttu-id="ecbf1-113">У вас могут быть как локальные тестовые сайты, так и тестовые сайты SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="ecbf1-113">You can have both on-premise and SharePoint Online test sites.</span></span>

- <span data-ttu-id="ecbf1-114">Учитывая все вышеизложенное, можно считать оба варианта одинаково простыми в настройке.</span><span class="sxs-lookup"><span data-stu-id="ecbf1-114">All things considered, the two options are equally easy to set up.</span></span>
    
<span data-ttu-id="ecbf1-115">**Руководство по созданию среды SharePoint Online** с помощью подписки SharePoint Online, которую можно использовать для разработки, см. в статье [Создание сайта разработчика с использованием имеющейся подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf1-115">**To create the SharePoint Online environment** using an SharePoint Online subscription that you can use for development, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span>
 
<span data-ttu-id="ecbf1-116">**Руководство по созданию локальной среды** см. в статье [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf1-116">**To create the on-premise environment**, see [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).</span></span>
 
> [!NOTE]
> <span data-ttu-id="ecbf1-117">В этой статье рассматриваются только среды для разработки надстроек SharePoint. Если планируется разрабатывать решения для ферм, см. статью [Настройка общей среды разработки для SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecbf1-117">Note  This topic is only concerned with environments for developing SharePoint Add-ins. If you plan to develop farm solutions, see  Set up a general development environment for SharePoint. If you plan to do both kinds of development, start with the latter article, and then see  Set up an on-premises development environment for SharePoint Add-ins for additional steps you need to develop SharePoint Add-ins.</span></span> 

> <span data-ttu-id="ecbf1-118">Если планируется разрабатывать решения обоих типов, начните с последней статьи, а затем ознакомьтесь со статьей [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md), где представлены дополнительные инструкции по разработке надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ecbf1-118">Note  This topic is only concerned with environments for developing SharePoint Add-ins. If you plan to develop farm solutions, see  Set up a general development environment for SharePoint. If you plan to do both kinds of development, start with the latter article, and then see  [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md) for additional steps you need to develop SharePoint Add-ins.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="ecbf1-119">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ecbf1-119">Additional resources</span></span>
<span data-ttu-id="ecbf1-120"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ecbf1-120"></span></span>

- [<span data-ttu-id="ecbf1-121">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="ecbf1-121">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
- [<span data-ttu-id="ecbf1-122">Создание надстроек SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ecbf1-122">Create SharePoint Add-ins in Visual Studio</span></span>](create-sharepoint-add-ins-in-visual-studio.md)
    
 

