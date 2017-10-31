---
title: "Обновление компонентов хост-сайта с надстройкой в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 24d1752c1618551b85fa63fbab7ef747a4873bc6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-host-web-components-in-sharepoint"></a><span data-ttu-id="d8e68-102">Обновление компонентов хост-сайта с надстройкой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e68-102">Update host web components in SharePoint</span></span>
<span data-ttu-id="d8e68-103">Обновление веб-частей надстроек и дополнительных действий на хост-сайте надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d8e68-103">Update add-in parts and custom actions in the host web of a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="d8e68-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="d8e68-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites-for-updating-host-web-components"></a><span data-ttu-id="d8e68-107">Необходимые условия для обновления компонентов хост-сайта</span><span class="sxs-lookup"><span data-stu-id="d8e68-107">Prerequisites for updating host web components</span></span>
<span data-ttu-id="d8e68-108"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-108"><a name="Prerequisites"> </a></span></span>

<span data-ttu-id="d8e68-109">Ознакомьтесь со статьей [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), в том числе с перечисленными в ней предварительными требованиями и основными понятиями.</span><span class="sxs-lookup"><span data-stu-id="d8e68-109">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in it.</span></span>
 

 

## <a name="update-host-web-components"></a><span data-ttu-id="d8e68-110">Обновление компонентов хост-сайта</span><span class="sxs-lookup"><span data-stu-id="d8e68-110">Update host web components</span></span>
<span data-ttu-id="d8e68-111"><a name="UpdateHostWeb"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-111"><a name="UpdateHostWeb"> </a></span></span>

<span data-ttu-id="d8e68-p102">Ваша надстройка может установить на хост-сайте два вида компонентов с описательной разметкой в надстройке SharePoint: настраиваемые действия ивеб-части надстройки. Обновление этих компонентов гораздо легче на хост-сайте, чем на сайте надстройки. Вам не требуется какое-либо обновление семантики. Просто добавьте или измените настраиваемые действия и веб-части надстройки. Когда Надстройка SharePoint обновлена, SharePoint всегда применяет любые новые файлы манифеста элементов и повторно применяет любые измененные файлы манифеста элементов с самой последней версией. Это совершенно безвредно при повторном применении. Например, кнопка ленты для настраиваемого действия не добавляется несколько раз на ленту.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p102">Your add-in can install two kinds of components on a host web with descriptive markup in the SharePoint Add-in: custom actions andadd-in parts. Updating these components is easier in the host web than in the add-in web. You don't need any update semantics. Just add/change the custom actions and add-in parts. When the SharePoint Add-in is updated, SharePoint always applies any new element manifest files and reapplies any changed element manifest files with the most recent version. No harm is done in reapplying; for example, a ribbon button for a custom action will not be added multiple times to the ribbon.</span></span>
 

 
<span data-ttu-id="d8e68-p103">Когда вы обновляете веб-часть надстройки, SharePoint заменяет старую версию на новую в коллекции веб-частей. Обязательно измените свойство **Name** объекта **ClientWebPart** при обновлении веб-части надстройки. Это гарантирует, что SharePoint после обновления надстройки удалит старую версию ее веб-части (которая больше не входит в состав надстройки) со всех страниц, на которые она была добавлена. Пользователям потребуется самостоятельно добавить на страницы новую версию.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p103">When you update an add-in part, SharePoint replaces the old version with the new version in the Web Part gallery. Be sure to change the  **Name** property of the **ClientWebPart** object when you update an add-in part. Doing this ensures that, when the add-in is updated, SharePoint will remove the old version of the add-in part (which is no longer part of the app) from all pages to which it was added. Users will need to re-add the new version to pages.</span></span>
 

 
<span data-ttu-id="d8e68-p104">Если вы оставите свойство **Name** без изменений, то старая версия останется на тех страницах, где она была добавлена, поэтому пользователи, скорее всего, не узнают о том, что доступна новая версия веб-части надстройки. Кроме того, при добавлении веб-части надстройки на другие страницы добавляется новая версия, так что одна и та же версия надстройки SharePoint будет использовать разные веб-части на разных страницах.</span><span class="sxs-lookup"><span data-stu-id="d8e68-p104">If you leave the  **Name** property unchanged, the old version remains on pages where it was added, which makes it unlikely that users will be aware that a new version of the add-in part is available. Also, when the add-in part is added to other pages, it is the new version that is added, so the same version of a SharePoint Add-in would have different add-in parts on different pages.</span></span>
 

 
<span data-ttu-id="d8e68-p105">Вы можете развернуть другие виды компонентов хост-сайта программно, используя удаленный приемник событий, который вы регистрируете в манифесте надстройки с помощью элемента  [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx). Вам нужно использовать приемник  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) для обновления компонентов, которые были первоначально развернуты с помощью приемника **InstalledEventEndpoint**. Приемники  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) описаны в [Создание обработчика для события обновления в надстройках для SharePoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="d8e68-p105">You can deploy other kinds of host web components programmatically using a remote event receiver that you register in the add-in manifest with an  [InstalledEventEndpoint](http://msdn.microsoft.com/library/af9f83d8-8325-3ede-d7b0-bb82c0445eb9%28Office.15%29.aspx) element. You should use an [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) receiver to update components that were originally deployed with an **InstalledEventEndpoint** receiver. [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) receivers are described in [Create a handler for the update event in SharePoint Add-ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="d8e68-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8e68-127">Next steps</span></span>
<span data-ttu-id="d8e68-128"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-128"><a name="Next"> </a></span></span>

<span data-ttu-id="d8e68-129">Перейдите в раздел  [Основные действия при обновлении надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или непосредственно перейдите к одной из следующих статей, чтобы узнать, как обновить очередной основной компонент надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d8e68-129">Go to  [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="d8e68-130">Обновление компонентов сайта надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e68-130">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="d8e68-131">Создание обработчика событий обновления для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e68-131">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 
-  <span data-ttu-id="d8e68-132">[Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins.md) </span><span class="sxs-lookup"><span data-stu-id="d8e68-132">[Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins.md)</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="d8e68-133">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d8e68-133">Additional resources</span></span>
<span data-ttu-id="d8e68-134"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d8e68-134"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="d8e68-135">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e68-135">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="d8e68-136">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d8e68-136">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)
    
 

