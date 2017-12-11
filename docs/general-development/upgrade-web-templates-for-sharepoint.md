---
title: "Обновление веб-шаблоны для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 69048e4c-6d6d-4e4e-b74c-7c72ae444354
ms.openlocfilehash: efa803c32e4da5c54df61f0647c2685006512916
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upgrade-web-templates-for-sharepoint"></a>Обновление веб-шаблоны для SharePoint
Сведения об обновлении настраиваемые веб-шаблоны SharePoint 2010 для использования в SharePoint после самостоятельного обновления.
SharePoint значительно изменился базовых компонентах, которое используется для отображения внешний вид сайтов SharePoint. Эти изменения настроек, выполненных для компонентов по умолчанию в SharePoint 2010, включите стилей, макеты страниц, главные страницы и темы.
  
    
    

В этой статье представлены рекомендации по обновлению веб-шаблоны, чтобы они работали с новой платформы.
## <a name="possible-behavior-after-a-self-service-site-upgrade"></a>Возможные поведение после обновления самостоятельного создания сайтов

При обновлении сервера SharePoint 2010 до версии 2013, Администраторы семейства сайтов показаны ссылку, которая позволяет обновлять свои сайты постепенно или обновление всех сайтов в семействе сайтов за один раз. Затем пользователи могут обновления и тестирование этих сайтов, содержащих настройки. Некоторые проблемы, которые пользователи могут возникнуть после обновления include:
  
    
    

- Фирменный стиль применяется для сайтов было изменено или отсутствует вообще.
    
  
- Настраиваемые компоненты не отображаться правильно.
    
  
- Страницы не прорисовывается, а пользователи получают неизвестные ошибки из SharePoint.
    
  
- Компоненты, включаемые по умолчанию отключены после обновления.
    
  

## <a name="recommendations-for-upgrading-sites"></a>Рекомендации по обновлению сайтов

При обновлении сайты обычно рекомендуется использовать сайта для проверки установки и тестирования компонентов для обеспечения совместимости и повышения производительности.
  
    
    
В следующих разделах подробно, необходимых для обновления в веб-шаблона.
  
    
    

### <a name="update-master-page-references"></a>Обновление ссылок на главную страницу

После обновления для SharePoint ссылки настраиваемой главной страницы, которые содержит веб-шаблон будет иметь значение главную страницу по умолчанию с именем **seattle.master**. Если настройка главную страницу по умолчанию в SharePoint 2010, необходимо изменить ссылку на странице, настраиваемых в порядке для настройки отображаться.
  
    
    

### <a name="update-available-features"></a>Доступные возможности обновления

При обновлении сайта для использования SharePoint веб-шаблоны, функции, которые присоединяются к шаблону по умолчанию, удаляются. Следовательно уменьшается доступные функции обновленных веб-шаблона.
  
    
    
Чтобы добавить функциональные возможности по умолчанию шаблон, необходимо изменить файл Onet.xml для веб-шаблона, который содержит список компонентов. Чтобы добавить компоненты по умолчанию веб-шаблон, выполните следующие действия.
  
    
    

### <a name="to-add-default-features-back-to-the-web-template"></a>Чтобы добавить по умолчанию компоненты резервного веб-шаблон


1. Откройте проект Visual Studio, который содержит веб-шаблон, который требуется обновить.
    
  
2. В **Обозревателе решений** найдите файл Onet.xml в проекте.
    
  
3. Откройте файл Onet.xml в редакторе XML.
    
  
4. Убедитесь в том, что каждой из функций в таблице 1 содержатся в разделе **WebFeatures**.
    
   **В таблице 1. По умолчанию веб-шаблона функции**


|**DisplayName**|**Код компонента**|
|:-----|:-----|
|AccSvcAddAccessApp  <br/> |d2b9ec23-526b-42c5-87b6-852bd83e0364  <br/> |
|AnnouncementsList  <br/> |00BFEA71-D1CE-42de-9C63-A44004CE0104  <br/> |
|BaseWeb  <br/> |99fe402e-89a0-45aa-9163-85342e865dc8  <br/> |
|BizAppsListTemplates  <br/> |065c78be-5231-477e-a972-14177cc5b3c7  <br/> |
|ContactsList  <br/> |00BFEA71-7E6D-4186-9BA8-C047AC750105  <br/> |
|ContactsList  <br/> |00BFEA71-7E6D-4186-9BA8-C047AC750105  <br/> |
|CustomList  <br/> |00BFEA71-DE22-43B2-A848-C05709900100  <br/> |
|DataConnectionLibrary  <br/> |00bfea71-dbd7-4f72-b8cb-da7ac0440130  <br/> |
|DataSourceLibrary  <br/> |00BFEA71-F381-423D-B9D1-DA7A54C50110  <br/> |
|DiscussionsList  <br/> |00BFEA71-6A49-43FA-B535-D15C05500108  <br/> |
|DocumentLibrary  <br/> |00BFEA71-E717-4E80-AA17-D0C71B360101  <br/> |
|EventsList  <br/> |00BFEA71-EC85-4903-972D-EBE475780106  <br/> |
|EventsList  <br/> |00BFEA71-EC85-4903-972D-EBE475780106  <br/> |
|ExternalList  <br/> |00bfea71-9549-43f8-b978-e47e54a10600  <br/> |
|FollowingContent  <br/> |a7a2793e-67cd-4dc1-9fd0-43f61581207a  <br/> |
|GanttTasksList  <br/> |00BFEA71-513D-4CA0-96C2-6A47775C0119  <br/> |
|GettingStarted  <br/> |4aec7207-0d02-4f4f-aa07-b370199cd0c7  <br/> |
|GridList  <br/> |00BFEA71-3A1D-41D3-A0EE-651D11570120  <br/> |
|HierarchyTasksList  <br/> |f9ce21f8-f437-4f7e-8bc6-946378c850f0  <br/> |
|IPFSWebFeatures  <br/> |f9ce21f8-f437-4f7e-8bc6-946378c850f0  <br/> |
|IssuesList  <br/> |00BFEA71-5932-4F9C-AD71-1557E5751100  <br/> |
|LinksList  <br/> |00BFEA71-5932-4F9C-AD71-1557E5751100  <br/> |
|MBrowserRedirect  <br/> |d95c97f3-e528-4da2-ae9f-32b3535fbb59  <br/> |
|MDSFeature  <br/> |87294c72-f260-42f3-a41b-981a2ffce37a  <br/> |
|MobilityRedirect  <br/> |f41cc668-37e5-4743-b4a8-74d1db3fd8a4  <br/> |
|MySiteMicroBlog  <br/> |ea23650b-0340-4708-b465-441a41c37af7  <br/> |
|NoCodeWorkflowLibrary  <br/> |00BFEA71-F600-43F6-A895-40C0DE7B0117  <br/> |
|PictureLibrary  <br/> |00BFEA71-52D4-45B3-B544-B1C71B620109  <br/> |
|PremiumWeb  <br/> |0806d127-06e6-447a-980e-2e90b03101b8  <br/> |
|PromotedLinksList  <br/> |192efa95-e50c-475e-87ab-361cede5dd7f  <br/> |
|ReportListTemplate  <br/> |2510d73f-7109-4ccc-8a1c-314894deeb3a  <br/> |
|SiteFeed  <br/> |15a572c6-e545-4d32-897a-bab6f5846e18  <br/> |
|SiteFeedController  <br/> |5153156a-63af-4fac-b557-91bd8c315432  <br/> |
|SurveysList  <br/> |00BFEA71-EB8A-40B1-80C7-506BE7590102  <br/> |
|TaskListNewsFeed  <br/> |ff13819a-a9ac-46fb-8163-9d53357ef98d  <br/> |
|TasksList  <br/> |00BFEA71-A83E-497E-9BA0-7A5C597D0107  <br/> |
|TeamCollab  <br/> |00bfea71-4ea5-48d4-a4ad-7ea5c011abe5  <br/> |
|WebPageLibrary  <br/> |00BFEA71-C796-4402-9F2F-0EB9A6E71B18  <br/> |
|WikiPageHomePage  <br/> |00bfea71-d8fe-4fec-8dad-01c19a6e4053  <br/> |
|WorkflowHistoryList  <br/> |00BFEA71-4EA5-48D4-A4AD-305CF7030140  <br/> |
|workflowProcessList  <br/> |00BFEA71-2D77-4A75-9FCA-76516689E21A  <br/> |
|WorkflowServiceStore  <br/> |2c63df2b-ceab-42c6-aeff-b3968162d4b1  <br/> |
|WorkflowTask  <br/> |57311b7a-9afd-4ff0-866e-9393ad6647b1  <br/> |
|XmlFormLibrary  <br/> |00BFEA71-1E1D-4562-B56A-F05371BB0115  <br/> |
   
5. Сохраните изменения и развертывания обычным образом.
    
> [!NOTE] 
> [!Примечание] Может также потребоваться для активации этих компонентов в программе центра администрирования. 
  
## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Обновление настроек сайта для SharePoint](upgrade-site-customizations-for-sharepoint.md)
-  [SharePoint 2010 и веб-шаблоны](http://blogs.msdn.com/b/vesku/archive/2010/10/14/sharepoint-2010-and-web-templates.aspx) 
-  [Планирование обновления семейства веб-сайтов](https://technet.microsoft.com/en-us/library/ff191199.aspx)
-  [Планирование обновлений семейств сайтов в SharePoint](http://technet.microsoft.com/en-us/library/ff191199.aspx)
    
  

  
    
    

