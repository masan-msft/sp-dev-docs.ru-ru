
# <a name="troubleshooting-document-libraries"></a><span data-ttu-id="22672-101">Устранение неполадок библиотек документов</span><span class="sxs-lookup"><span data-stu-id="22672-101">Troubleshooting document libraries</span></span>
<span data-ttu-id="22672-102">В этой статье описываются проблемы, которые могут возникнуть при доступе к библиотеке документов SharePoint из облачной бизнес-надстройки, а также способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="22672-102">In this topic, you can learn about problems that may occur when you access a SharePoint document library from a cloud business add-in and the techniques that you can use to resolve those problems.</span></span>
 

 <span data-ttu-id="22672-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="22672-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


 

## <a name="error-this-add-in-does-not-support-uploading-documents-from-your-current-browser"></a><span data-ttu-id="22672-106">Ошибка: эта надстройка не поддерживает отправку документов из текущего браузера</span><span class="sxs-lookup"><span data-stu-id="22672-106">Error: This add-in does not support uploading documents from your current browser</span></span>

<span data-ttu-id="22672-p102">При попытке отправить документ в связанную библиотеку документов из облачной бизнес-надстройки, отображается сообщение об ошибке "Эта надстройка не поддерживает отправку документов из текущего браузера. Используйте последнюю версию". Эта проблема возникает только в определенных старых браузерах, которые не поддерживают API-интерфейс FileReader HTML5. Чтобы ее устранить, добавьте в проект пакет NuGet и повторно разверните надстройку.</span><span class="sxs-lookup"><span data-stu-id="22672-p102">When attempting to upload a document to an associated document library in a cloud business add-in, the upload fails with the error message "This add-in does not support uploading documents from your current browser. Please use the latest version". This issue only occurs on certain older browsers that don't support the HTML5 FileReader API. It can be fixed by adding a NuGet package to your project and redeploying the add-in.</span></span>
 

 

### <a name="to-prevent-the-error"></a><span data-ttu-id="22672-111">Как избежать этой ошибки</span><span class="sxs-lookup"><span data-stu-id="22672-111">To prevent the error</span></span>


1. <span data-ttu-id="22672-112">В **обозревателе решений** откройте контекстное меню проекта **Сервер** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="22672-112">In **Solution Explorer**, open the shortcut menu for the **Server** project and choose **Manage NuGet Packages**.</span></span>
    
 
2. <span data-ttu-id="22672-113">В диалоговом окне **Управление пакетами NuGet** разверните узел **В сети**, а затем в поле **Поиск в сети** укажите веб-страницы, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="22672-113">In the **Manage NuGet Packages** dialog box, expand the **Online** node, and then in the **Search Online** box enter web pages, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="22672-114">**Рисунок 1. Параметры, выбранные в диалоговом окне "Управление пакетами NuGet"**</span><span class="sxs-lookup"><span data-stu-id="22672-114">**Figure 1. Selections in the Manage NuGet Packages dialog box**</span></span>

 

  ![Параметры, выбранные в диалоговом окне "Управление пакетами NuGet"](../../images/NuGet.PNG)
 

 

 
3. <span data-ttu-id="22672-116">В списке результатов выберите **Веб-страницы Microsoft ASP.NET**, а затем нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="22672-116">In the list of results, choose **Microsoft ASP.NET Web Pages**, and then choose the **Install** button.</span></span>
    
    <span data-ttu-id="22672-117">Откроется диалоговое окно **Согласие с условиями лицензионного соглашения**.</span><span class="sxs-lookup"><span data-stu-id="22672-117">The **License Acceptance** dialog box opens.</span></span>
    
 
4. <span data-ttu-id="22672-118">В диалоговом окне **Согласие с условиями лицензионного соглашения** изучите условия лицензионного соглашения и нажмите кнопку **Принимаю**, если вы принимаете их.</span><span class="sxs-lookup"><span data-stu-id="22672-118">In the **License Acceptance** dialog box, review the license terms, and if you agree to the terms choose the **I Accept** button.</span></span>
    
 
5. <span data-ttu-id="22672-119">По завершении установки пакета нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="22672-119">When the package finishes installing, choose the **Close** button.</span></span>
    
 
6. <span data-ttu-id="22672-120">Опубликуйте обновленную надстройку на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="22672-120">Publish the updated add-in to your SharePoint site.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="22672-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="22672-121">Additional resources</span></span>
<span data-ttu-id="22672-122"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="22672-122"></span></span>


-  [<span data-ttu-id="22672-123">Сопоставление библиотеки документов с объектом</span><span class="sxs-lookup"><span data-stu-id="22672-123">Associate a document library with an entity</span></span>](associate-a-document-library-with-an-entity)
    
 

