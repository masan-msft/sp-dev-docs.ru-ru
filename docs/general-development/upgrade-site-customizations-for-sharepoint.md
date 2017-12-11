---
title: "Обновление настроек сайта для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4b515860-69ae-4af8-8013-cd071c0ddca6
ms.openlocfilehash: 4ce3bab5fc777bd7ec2237ecfbfe2ae0d92a89d4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upgrade-site-customizations-for-sharepoint"></a><span data-ttu-id="f954b-102">Обновление настроек сайта для SharePoint</span><span class="sxs-lookup"><span data-stu-id="f954b-102">Upgrade site customizations for SharePoint</span></span>
<span data-ttu-id="f954b-103">Узнайте о возможных проблемах и получить рекомендации по обновлению настройки сайта SharePoint 2010 до SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f954b-103">Learn about potential issues and get recommendations for upgrading your SharePoint 2010 site customizations to SharePoint.</span></span>
<span data-ttu-id="f954b-104">SharePoint вводятся существенные изменения для пользовательского интерфейса (UI), который позволяет вам настроить сайты, использующие быстрее, более гибкой компонентов.</span><span class="sxs-lookup"><span data-stu-id="f954b-104">SharePoint introduces significant changes to the user interface (UI) that let you customize sites using faster, more agile components.</span></span> <span data-ttu-id="f954b-105">Однако при обновлении с SharePoint 2010 могут возникнуть некоторые проблемы, связанные с новых компонентов, созданных в SharePoint для обработки усовершенствования в пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="f954b-105">But when you upgrade from SharePoint 2010, you might encounter some issues with the new components that have been built into SharePoint to handle the improvements to the UI.</span></span>
  
    
    

<span data-ttu-id="f954b-106">В этой статье представлены сведения о SharePoint для разработчиков и те отвечает за администрирование из SharePoint 2010 процесс обновления для выявления потенциальных проблем после обновления.</span><span class="sxs-lookup"><span data-stu-id="f954b-106">This article will help SharePoint developers and those responsible for administering the upgrade process from SharePoint 2010 to identify potential problems after upgrading.</span></span>
## <a name="general-recommendations-for-upgrading"></a><span data-ttu-id="f954b-107">Общие рекомендации по обновлению</span><span class="sxs-lookup"><span data-stu-id="f954b-107">General recommendations for upgrading</span></span>

<span data-ttu-id="f954b-108">В общем случае рекомендуется создать новый сайт «оценки», где проверки настроек и измените их в среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f954b-108">In general, we recommend that you create a new "evaluation" site where you can test your customizations and redesign them for a SharePoint environment.</span></span> <span data-ttu-id="f954b-109">Дополнительные сведения о создании семейство сайтов для оценки можно [обновления семейства веб-сайтов](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/upgrade-a-site-collection-HA102865473.aspx?CTT=5&amp;origin=HA104034491).</span><span class="sxs-lookup"><span data-stu-id="f954b-109">For more information about creating an evaluation site collection, see  [Upgrade a site collection](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/upgrade-a-site-collection-HA102865473.aspx?CTT=5&amp;origin=HA104034491).</span></span>
  
    
    

### <a name="upgrading-custom-components"></a><span data-ttu-id="f954b-110">Обновление настраиваемых компонентов</span><span class="sxs-lookup"><span data-stu-id="f954b-110">Upgrading custom components</span></span>

<span data-ttu-id="f954b-111">В таблице 1 перечислены возможные после обновления проблем для настраиваемых компонентов и сведения о способах их устранения.</span><span class="sxs-lookup"><span data-stu-id="f954b-111">Table 1 lists the possible after-upgrade problems for custom components and information about how to address them.</span></span>
  
    
    

<span data-ttu-id="f954b-112">**В таблице 1. Настраиваемые компоненты, при обновлении в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="f954b-112">**Table 1. Custom components affected by upgrading to SharePoint**</span></span>


|<span data-ttu-id="f954b-113">**Если вы настроили.**</span><span class="sxs-lookup"><span data-stu-id="f954b-113">**If you have customized**</span></span>|<span data-ttu-id="f954b-114">**Могут возникать**</span><span class="sxs-lookup"><span data-stu-id="f954b-114">**You might encounter**</span></span>|
|:-----|:-----|
|<span data-ttu-id="f954b-115">Стили CSS</span><span class="sxs-lookup"><span data-stu-id="f954b-115">CSS styles</span></span>  <br/> |<span data-ttu-id="f954b-p103">Во время обновления веб-узла будет восстановлено файлы CSS, которые ссылаются на странице default.master. В результате будет изменить все настройки, внесенные во внешний вид страниц и страниц будут отображаться со стилями по умолчанию, обнаруженных в установки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f954b-p103">During upgrade, your site will revert to the CSS files referred to in the default.master page. As a result, any customizations you have made to the appearance of your pages will change, and pages will render with the default styles found in a default installation.</span></span>  <br/> |
|<span data-ttu-id="f954b-118">Темы</span><span class="sxs-lookup"><span data-stu-id="f954b-118">Themes</span></span>  <br/> |<span data-ttu-id="f954b-p104">Для SharePoint 2010 может создавать пользовательские темы, которые определяют фирменной символики для всего сайта. Можно создать как .thmx файлы, которые можно было выгрузить в коллекции веб-сайтов и применяется администратором.</span><span class="sxs-lookup"><span data-stu-id="f954b-p104">For SharePoint 2010, you may have created custom themes that define a corporate branding for an entire site. You create these as .thmx files that can be uploaded to the site collection and applied by the administrator.</span></span>  <br/> <span data-ttu-id="f954b-121">В SharePoint модуль темы была полностью переработана для более гибкая и мощная и обеспечения для упрощения будущих обновлений.</span><span class="sxs-lookup"><span data-stu-id="f954b-121">In SharePoint, the theming engine has been completely redesigned to be more flexible and powerful and to provide for easier future upgrades.</span></span> <span data-ttu-id="f954b-122">Изменение топологии корпоративного поиска, из-за обновление с SharePoint 2010 для тем SharePoint не поддерживается и будет необходимо повторно создать их для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f954b-122">As a result of this redesign, upgrading from SharePoint 2010 to SharePoint themes is not supported and will require you to re-create them for SharePoint.</span></span>  <br/> |
|<span data-ttu-id="f954b-123">шаблоны веб-сайта;</span><span class="sxs-lookup"><span data-stu-id="f954b-123">Web templates</span></span>  <br/> |<span data-ttu-id="f954b-p106">Веб-шаблоны были представлены в SharePoint 2010 предоставляет способ для пакета компонентов, макеты, стили и других компонентов, которые затем можно использовать для создания нового веб-сайтов. Они являются аналогично Создание определений сайта, но с веб-шаблоны можно добавить компоненты публикации.</span><span class="sxs-lookup"><span data-stu-id="f954b-p106">Web templates were introduced in SharePoint 2010 to provide a way to package features, layouts, styles, and other components that you can then use to create new webs. They are similar in function to creating site definitions, but with web templates, you can add publishing features.  </span></span><br/> <span data-ttu-id="f954b-126">Из-за изменений, внесенных в SharePoint к настраиваемой веб-шаблонов не будет работать сразу же после обновления.</span><span class="sxs-lookup"><span data-stu-id="f954b-126">Due to the changes made in SharePoint, your customized web templates will not work immediately after upgrade.</span></span>  <br/> <span data-ttu-id="f954b-127">Чтобы просмотреть изменения, которые были внесены в веб-шаблоны и устранить проблемы, связанные с этим можно в статье [обновления веб-шаблоны для SharePoint](upgrade-web-templates-for-sharepoint.md) для рекомендации и полезные советы.</span><span class="sxs-lookup"><span data-stu-id="f954b-127">To see what changes have been made to web templates and to fix issues resulting from this, see  [Upgrade web templates for SharePoint](upgrade-web-templates-for-sharepoint.md) for recommendations and best practices.</span></span> <br/> |
|<span data-ttu-id="f954b-128">Эталонные страницы.</span><span class="sxs-lookup"><span data-stu-id="f954b-128">Master pages</span></span>  <br/> |<span data-ttu-id="f954b-p107">Во время обновления вернуться к странице default.master отменяются все ссылки на настраиваемых главных страниц, которые были созданы. Это может стать причиной ошибок в SharePoint из-за ссылки на настраиваемую страницу на отсутствующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="f954b-p107">During upgrade, any references to custom master pages you have created are reverted back to the default.master page. This may cause errors in SharePoint due to references on the custom page to missing components.</span></span>  <br/> <span data-ttu-id="f954b-131">Чтобы устранить эту проблему, необходимо изменить ссылки на настраиваемой главной страницы.</span><span class="sxs-lookup"><span data-stu-id="f954b-131">To fix this, you have to change the references to any custom master pages.</span></span>  <br/> |
   

## <a name="see-also"></a><span data-ttu-id="f954b-132">См. также</span><span class="sxs-lookup"><span data-stu-id="f954b-132">See also</span></span>
<span data-ttu-id="f954b-133"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f954b-133"></span></span>


-  [<span data-ttu-id="f954b-134">Планирование обновления семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f954b-134">Plan to upgrade a site collection</span></span>](https://technet.microsoft.com/en-us/library/ff191199.aspx)
    
  
-  [<span data-ttu-id="f954b-135">Проблемы с конфигурацией продукта, могут возникнуть при обновлении в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f954b-135">Branding issues that may occur when upgrading to SharePoint</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/branding-issues-that-may-occur-when-upgrading-to-sharepoint-HA104052656.aspx?CTT=5&amp;origin=HA104034491)
    
  
-  [<span data-ttu-id="f954b-136">Обновление семейства сайтов</span><span class="sxs-lookup"><span data-stu-id="f954b-136">Upgrade a site collection</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/upgrade-a-site-collection-HA102865473.aspx?CTT=5&amp;origin=HA104034491)
    
  
-  [<span data-ttu-id="f954b-137">Вопросы устранения неполадок обновления семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f954b-137">Troubleshoot site collection upgrade issues</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/troubleshoot-site-collection-upgrade-issues-HA104037311.aspx?CTT=5&amp;origin=HA104034491)
    
  

