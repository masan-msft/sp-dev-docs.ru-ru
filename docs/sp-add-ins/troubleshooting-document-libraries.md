---
title: "Устранение неполадок библиотек документов"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1629b514a8fa4a84d7d916214d89501f24d6a25b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="troubleshooting-document-libraries"></a><span data-ttu-id="b7d61-102">Устранение неполадок библиотек документов</span><span class="sxs-lookup"><span data-stu-id="b7d61-102">Troubleshooting document libraries</span></span>
<span data-ttu-id="b7d61-103">В этой статье описываются проблемы, которые могут возникнуть при доступе к библиотеке документов SharePoint из облачной бизнес-надстройки, а также способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="b7d61-103">In this topic, you can learn about problems that may occur when you access a SharePoint document library from a cloud business add-in and the techniques that you can use to resolve those problems.</span></span>
 

 <span data-ttu-id="b7d61-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b7d61-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 

## <a name="error-this-add-in-does-not-support-uploading-documents-from-your-current-browser"></a><span data-ttu-id="b7d61-107">Ошибка: эта надстройка не поддерживает отправку документов из текущего браузера</span><span class="sxs-lookup"><span data-stu-id="b7d61-107">Error: This add-in does not support uploading documents from your current browser</span></span>

<span data-ttu-id="b7d61-p102">При попытке отправить документ в связанную библиотеку документов из облачной бизнес-надстройки, отображается сообщение об ошибке "Эта надстройка не поддерживает отправку документов из текущего браузера. Используйте последнюю версию". Эта проблема возникает только в определенных старых браузерах, которые не поддерживают API-интерфейс FileReader HTML5. Чтобы ее устранить, добавьте в проект пакет NuGet и повторно разверните надстройку.</span><span class="sxs-lookup"><span data-stu-id="b7d61-p102">When attempting to upload a document to an associated document library in a cloud business add-in, the upload fails with the error message "This add-in does not support uploading documents from your current browser. Please use the latest version". This issue only occurs on certain older browsers that don't support the HTML5 FileReader API. It can be fixed by adding a NuGet package to your project and redeploying the add-in.</span></span>
 

 

### <a name="to-prevent-the-error"></a><span data-ttu-id="b7d61-112">Как избежать этой ошибки</span><span class="sxs-lookup"><span data-stu-id="b7d61-112">To prevent the error</span></span>


1. <span data-ttu-id="b7d61-113">В **обозревателе решений** откройте контекстное меню проекта **Сервер** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b7d61-113">In  **Solution Explorer**, open the shortcut menu for the  **Server** project and choose **Manage NuGet Packages**.</span></span>
    
 
2. <span data-ttu-id="b7d61-114">В диалоговом окне **Управление пакетами NuGet** разверните узел **В сети**, а затем в поле **Поиск в сети** укажите веб-страницы, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="b7d61-114">In the  **Manage NuGet Packages** dialog box, expand the **Online** node, and then in the **Search Online** box enter web pages, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="b7d61-115">**Рисунок 1. Параметры, выбранные в диалоговом окне "Управление пакетами NuGet"**</span><span class="sxs-lookup"><span data-stu-id="b7d61-115">**Figure 1. Selections in the Manage NuGet Packages dialog box**</span></span>

 

  ![Параметры, выбранные в диалоговом окне "Управление пакетами NuGet"](../images/NuGet.PNG)
 

 

 
3. <span data-ttu-id="b7d61-117">В списке результатов выберите **Веб-страницы Microsoft ASP.NET**, а затем нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b7d61-117">In the list of results, choose  **Microsoft ASP.NET Web Pages**, and then choose the  **Install** button.</span></span>
    
    <span data-ttu-id="b7d61-118">Откроется диалоговое окно **Согласие с условиями лицензионного соглашения**.</span><span class="sxs-lookup"><span data-stu-id="b7d61-118">The  **License Acceptance** dialog box opens.</span></span>
    
 
4. <span data-ttu-id="b7d61-119">В диалоговом окне **Согласие с условиями лицензионного соглашения** изучите условия лицензионного соглашения и нажмите кнопку **Принимаю**, если вы принимаете их.</span><span class="sxs-lookup"><span data-stu-id="b7d61-119">In the  **License Acceptance** dialog box, review the license terms, and if you agree to the terms choose the **I Accept** button.</span></span>
    
 
5. <span data-ttu-id="b7d61-120">По завершении установки пакета нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="b7d61-120">When the package finishes installing, choose the  **Close** button.</span></span>
    
 
6. <span data-ttu-id="b7d61-121">Опубликуйте обновленную надстройку на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b7d61-121">Publish the updated add-in to your SharePoint site.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="b7d61-122">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b7d61-122">Additional resources</span></span>
<span data-ttu-id="b7d61-123"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b7d61-123"></span></span>


-  [<span data-ttu-id="b7d61-124">Сопоставление библиотеки документов с объектом</span><span class="sxs-lookup"><span data-stu-id="b7d61-124">Associate a document library with an entity</span></span>](associate-a-document-library-with-an-entity.md)
    
 

