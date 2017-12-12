---
title: "Сведения о управления пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c5e81e55cff89d6bf311c3fb6c7f40e0b0c87ee9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="information-management-sample-add-in-for-sharepoint"></a><span data-ttu-id="a19cf-102">Сведения о управления пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a19cf-102">Information management sample add-in for SharePoint</span></span>
<span data-ttu-id="a19cf-103">В рамках стратегии Enterprise Content Management (ECM) можно получить или задать политики сайта для управления жизненным циклом сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a19cf-103">As part of your Enterprise Content Management (ECM) strategy, you can get or set site policies to manage the lifecycle of your SharePoint site.</span></span>
    
<span data-ttu-id="a19cf-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="a19cf-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="a19cf-105">Пример [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) показано, как использовать ASP.NET размещением у поставщика SharePoint надстройке для получения и задания политики сайта для сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-105">The [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) sample shows you how to use an ASP.NET provider-hosted SharePoint add-in to get and set a site policy on a site.</span></span> <span data-ttu-id="a19cf-106">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="a19cf-106">Use this solution if you want to:</span></span>

- <span data-ttu-id="a19cf-107">Применение настроек политики настраиваемой процедуры подготовки сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-107">Apply policy settings during your custom site provisioning process.</span></span> 
    
- <span data-ttu-id="a19cf-108">Создание новой или изменение существующей политики сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-108">Create a new or modify an existing site policy.</span></span>
    
- <span data-ttu-id="a19cf-109">Создайте Настраиваемая формула истечения действия.</span><span class="sxs-lookup"><span data-stu-id="a19cf-109">Create a custom expiration formula.</span></span> 
    
## <a name="before-you-begin"></a><span data-ttu-id="a19cf-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a19cf-110">Before you begin</span></span>
<span data-ttu-id="a19cf-111"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="a19cf-111"></span></span>

<span data-ttu-id="a19cf-112">Чтобы начать работу, загрузите пример надстройки [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="a19cf-112">To get started, download the  [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="a19cf-113">Мы рекомендуем создать политику по крайней мере один сайт и назначьте его на свой сайт перед запуском этой надстройки.</span><span class="sxs-lookup"><span data-stu-id="a19cf-113">We recommend that you create at least one site policy, and assign it to your site before you run this add-in.</span></span> <span data-ttu-id="a19cf-114">В противном случае надстройка будет запущен без отображения образца данных.</span><span class="sxs-lookup"><span data-stu-id="a19cf-114">Otherwise, the add-in will start without displaying sample data.</span></span> <span data-ttu-id="a19cf-115">Для получения дополнительных сведений см [Обзор политик сайта в SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a19cf-115">For more information, see  [Overview of site policies in SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).</span></span>

## <a name="using-the-coreinformationmanagement-sample-app"></a><span data-ttu-id="a19cf-116">Использование примера приложения Core.InformationManagement</span><span class="sxs-lookup"><span data-stu-id="a19cf-116">Using the Core.InformationManagement sample app</span></span>
<span data-ttu-id="a19cf-117"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="a19cf-117"></span></span>

<span data-ttu-id="a19cf-118">При запуске приложения на начальной странице отображаются следующие сведения, как показано на рисунке 1:</span><span class="sxs-lookup"><span data-stu-id="a19cf-118">When you start the app, the start page displays the following information, as shown in Figure 1:</span></span>

- <span data-ttu-id="a19cf-119">Сайт закрытия даты окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="a19cf-119">The site's closure and expiration dates.</span></span> <span data-ttu-id="a19cf-120">Эти даты относятся к сайту и основаны на параметрах конфигурации применяемой политики сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-120">These dates are specific to a site and are based on the configuration settings of the site policy that is applied.</span></span>
    
- <span data-ttu-id="a19cf-121">Все политики сайта, которые можно применять к сайту.</span><span class="sxs-lookup"><span data-stu-id="a19cf-121">All site policies that can be applied to the site.</span></span>
    
- <span data-ttu-id="a19cf-122">В настоящее время применяемой политики сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-122">The site policy that is currently applied.</span></span>
    
- <span data-ttu-id="a19cf-123">Поле для выбора и применение новой политики сайта к сайту.</span><span class="sxs-lookup"><span data-stu-id="a19cf-123">The option box to select and apply a new site policy to the site.</span></span>

<span data-ttu-id="a19cf-124">**На рисунке 1. Надстройка начальная страница управления сведения**</span><span class="sxs-lookup"><span data-stu-id="a19cf-124">**Figure 1. Information Management add-in start page**</span></span>

![Снимок экрана с помощью надстройки в начало страницы, с помощью значения закрытия и срока действия политики сайта, политики доступны и применяемые сайта и другие политики, применяемые выделенными.](media/8c5f39f7-700d-4300-bcc4-9ed9edf0e155.png)

<span data-ttu-id="a19cf-126">Из сайта SharePoint, можно перейти к приложения, который выполняется на удаленном узле, выбрав **последние** > **Core.InformationManagement**.</span><span class="sxs-lookup"><span data-stu-id="a19cf-126">From your SharePoint site, you can go to the app, which runs on the remote host, by choosing  **Recent** > **Core.InformationManagement**.</span></span> <span data-ttu-id="a19cf-127">Чтобы вернуться на сайт SharePoint, выберите **сайта**.</span><span class="sxs-lookup"><span data-stu-id="a19cf-127">To return to your SharePoint site, choose  **Back to Site**.</span></span>

<span data-ttu-id="a19cf-128">Файл Pages\Default.aspx.cs в проекте Core.InformationManagementWeb содержит код для страницы, отображаемой на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="a19cf-128">The Pages\Default.aspx.cs file in the Core.InformationManagementWeb project contains the code for the page displayed in Figure 1.</span></span> 

<span data-ttu-id="a19cf-129">Следующий код в метод **Page_Load** страницы Default.aspx.cs извлекает и отображает даты закрытия и истечение срока действия сайта, на основе политики применен сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-129">The following code in the  **Page_Load** method of the Default.aspx.cs page fetches and displays the closure and expiration dates of the site, based on the applied site policy.</span></span> <span data-ttu-id="a19cf-130">Этот код вызывает методы расширения **GetSiteExpirationDate** и **GetSiteCloseDate** OfficeDevPnP.Core проекта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-130">This code calls the **GetSiteExpirationDate** and **GetSiteCloseDate** extension methods of the OfficeDevPnP.Core project.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="a19cf-131">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="a19cf-131">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
// Get site expiration and closure dates.
if (cc.Web.HasSitePolicyApplied())
{
        lblSiteExpiration.Text = String.Format("The expiration date for the site is {0}", cc.Web.GetSiteExpirationDate());
        lblSiteClosure.Text = String.Format("The closure date for the site is {0}", cc.Web.GetSiteCloseDate());
}

```

<span data-ttu-id="a19cf-132">Следующий код в метод **Page_Load** страницы Default.aspx.cs имена всех политик сайтов, которые применимы к сайту (в том числе политики в настоящее время примененных сайта).</span><span class="sxs-lookup"><span data-stu-id="a19cf-132">The following code in the  **Page_Load** method of the Default.aspx.cs page displays the names of all site policies that can be applied to the site (including the currently applied site policy).</span></span> <span data-ttu-id="a19cf-133">Этот код вызывает метод расширения **GetSitePolicies** OfficeDevPnP.Core проекта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-133">This code calls the **GetSitePolicies** extension method of the OfficeDevPnP.Core project.</span></span>

```C#
// List the defined policies.
List<SitePolicyEntity> policies = cc.Web.GetSitePolicies();
string policiesString = "";
foreach (var policy in policies)
                    {
                        policiesString += String.Format("{0} ({1}) <BR />", policy.Name, policy.Description);
                    }
lblSitePolicies.Text = policiesString;
            };

```

<span data-ttu-id="a19cf-134">Следующий код в метод **Page_Load** страницы Default.aspx.cs имя политики сайта, в настоящее время применяется к сайту.</span><span class="sxs-lookup"><span data-stu-id="a19cf-134">The following code in the  **Page_Load** method of the Default.aspx.cs page displays the name of the site policy currently applied to the site.</span></span> <span data-ttu-id="a19cf-135">Это вызывает метод расширения **GetAppliedSitePolicy** OfficeDevPnP.Core проекта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-135">This calls the **GetAppliedSitePolicy** extension method of the OfficeDevPnP.Core project.</span></span>

```C#
// Show the assigned policy.
SitePolicyEntity appliedPolicy = cc.Web.GetAppliedSitePolicy();
if (appliedPolicy != null)
            {
            lblAppliedPolicy.Text = String.Format("{0} ({1})", appliedPolicy.Name, appliedPolicy.Description);
            }
else
            {
            lblAppliedPolicy.Text = "No policy has been applied";
            }

```

<span data-ttu-id="a19cf-136">Следующий код в метод **Page_Load** страницы Default.aspx.cs заполняет раскрывающегося списка с помощью политики сайта, которые доступны, за исключением политики сайта, назначенном на сайт.</span><span class="sxs-lookup"><span data-stu-id="a19cf-136">The following code in the  **Page_Load** method of the Default.aspx.cs page populates the drop-down list with the site policies that are available, except for the site policy that is currently assigned to the site.</span></span>

```C#
// Fill the policies combo.
foreach (var policy in policies)
{
if (appliedPolicy == null || !policy.Name.Equals(appliedPolicy.Name, StringComparison.InvariantCultureIgnoreCase))
{
                            drlPolicies.Items.Add(policy.Name);
           }
}
btnApplyPolicy.Enabled = drlPolicies.Items.Count > 0;

```

<span data-ttu-id="a19cf-137">Следующий код в файле Default.aspx.cs страницы применяется политика выбранного сайта на сайт.</span><span class="sxs-lookup"><span data-stu-id="a19cf-137">The following code in the Default.aspx.cs page applies the selected site policy to the site.</span></span> <span data-ttu-id="a19cf-138">Политики в исходный сайт заменяется новой политики сайта.</span><span class="sxs-lookup"><span data-stu-id="a19cf-138">The original site policy is replaced by the new site policy.</span></span> 

```C#
protected void btnApplyPolicy_Click(object sender, EventArgs e)
{
if (drlPolicies.SelectedItem != null)
            {
                cc.Web.ApplySitePolicy(drlPolicies.SelectedItem.Text);
                Page.Response.Redirect(Page.Request.Url.ToString(), true);
            }
}

```

## <a name="see-also"></a><span data-ttu-id="a19cf-139">См. также</span><span class="sxs-lookup"><span data-stu-id="a19cf-139">See also</span></span>
<span data-ttu-id="a19cf-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a19cf-140"></span></span>

-  [<span data-ttu-id="a19cf-141">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a19cf-141">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="a19cf-142">Пример OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="a19cf-142">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
-  [<span data-ttu-id="a19cf-143">Пример Core.SiteClassification</span><span class="sxs-lookup"><span data-stu-id="a19cf-143">Core.SiteClassification sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SiteClassification)
    
-  [<span data-ttu-id="a19cf-144">ECM. Пример приложения AutoTagging</span><span class="sxs-lookup"><span data-stu-id="a19cf-144">ECM.AutoTagging sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging)
    
-  [<span data-ttu-id="a19cf-145">ECM. Пример приложения DocumentLibraries</span><span class="sxs-lookup"><span data-stu-id="a19cf-145">ECM.DocumentLibraries sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
    
-  [<span data-ttu-id="a19cf-146">ECM. Пример приложения RecordsManagement</span><span class="sxs-lookup"><span data-stu-id="a19cf-146">ECM.RecordsManagement sample app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement)
