# <a name="enable-a-newsfeed-for-a-cloud-business-add-in"></a><span data-ttu-id="673f2-101">Включение канала новостей для облачной бизнес-надстройки</span><span class="sxs-lookup"><span data-stu-id="673f2-101">Enable a newsfeed for a cloud business add-in</span></span>
<span data-ttu-id="673f2-p101">Функции социальных медиа и совместной работы в SharePoint для Office 365 позволяют пользователям следить за действиями со списком и добавлять комментарии. Вы можете легко создать канал новостей для своей облачной бизнес-надстройки, включив несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="673f2-p101">Social and collaboration features in SharePoint for Office 365 allow users to track activity on a list and add comments. You can easily create a newsfeed for your Cloud Business Add-in by enabling a couple of properties.</span></span>
 

 <span data-ttu-id="673f2-p102">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="673f2-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="673f2-107">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="673f2-107">Prerequisites</span></span>

<span data-ttu-id="673f2-108">Для размещения канала новостей вам понадобится сайт разработчика SharePoint в Office 365, который вы можете получить на странице  [Регистрация на сайте разработчиков для Office 365](http://go.microsoft.com/fwlink/?LinkId=263490).</span><span class="sxs-lookup"><span data-stu-id="673f2-108">To host the newsfeed, you'll need a SharePoint Developer site on Office 365, which you can get from  [Sign up for an Office 365 Developer Site](http://go.microsoft.com/fwlink/?LinkId=263490).</span></span>
 

 

## <a name="procedures"></a><span data-ttu-id="673f2-109">Процедуры</span><span class="sxs-lookup"><span data-stu-id="673f2-109">Procedures</span></span>


### <a name="to-enable-a-newsfeed"></a><span data-ttu-id="673f2-110">Включение канала новостей</span><span class="sxs-lookup"><span data-stu-id="673f2-110">To enable a newsfeed</span></span>


1. <span data-ttu-id="673f2-111">В обозревателе решений откройте объект, представляющий список, в который требуется добавить канал новостей, а затем в области **Перспектива** откройте вкладку **Сервер**.</span><span class="sxs-lookup"><span data-stu-id="673f2-111">In Solution Explorer, open the entity representing the list where you want to add a newsfeed, and then on the **Perspective** bar choose the **Server** tab.</span></span>
    
 
2. <span data-ttu-id="673f2-112">В окне **Свойства** установите флажки **Размещать при создании** или **Размещать при обновлении**.</span><span class="sxs-lookup"><span data-stu-id="673f2-112">In the **Properties** window, select the **Post when Created** and/or **Post when Updated** check boxes.</span></span>
    
  ![Социальные свойства](../../images/CBAsocial.PNG)
 

     <span data-ttu-id="673f2-p103">Если установлен флажок **Размещать при создании**, в канал новостей добавляется поток для каждого нового элемента списка. Если установлен флажок **Размещать при обновлении**, поток добавляется при изменении значения для элемента в списке. Триггеры записей определяют, какие поля в элементе будут активировать запись.</span><span class="sxs-lookup"><span data-stu-id="673f2-p103">**Post when Created** adds a thread to the newsfeed for each new list item. **Post when Updated** adds a thread when the value for an item in the list is changed. Post triggers determine which fields in the item will trigger a post.</span></span>
    
 
3. <span data-ttu-id="673f2-117">Перейдите по ссылке **Выбор триггеров записи**.</span><span class="sxs-lookup"><span data-stu-id="673f2-117">Choose the **Choose post triggers** link.</span></span>
    
    <span data-ttu-id="673f2-118">Откроется диалоговое окно **Выбор триггеров записи**.</span><span class="sxs-lookup"><span data-stu-id="673f2-118">The **Choose post triggers** dialog box appears.</span></span>
    
 
4. <span data-ttu-id="673f2-119">В диалоговом окне **Выбор триггеров записи** установите флажки для полей, которые должны вызывать размещение, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="673f2-119">In the **Choose post triggers** dialog box, select the check boxes for all fields that you want to trigger a post, and then choose the **OK** button.</span></span>
    
    <span data-ttu-id="673f2-120">Будет создан единый поток для всех изменений элемента независимо от того, сколько полей выбрано.</span><span class="sxs-lookup"><span data-stu-id="673f2-120">A single thread will be created for all changes in an item no matter how many fields you choose.</span></span>
    
 

### <a name="to-access-a-newsfeed"></a><span data-ttu-id="673f2-121">Доступ к каналу новостей</span><span class="sxs-lookup"><span data-stu-id="673f2-121">To access a newsfeed</span></span>


1. <span data-ttu-id="673f2-122">Чтобы запустить приложение, в строке меню выберите пункт **Отладка**, а затем — **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="673f2-122">On the menu bar, choose **Debug**, **Start Debugging** to run the application.</span></span>
    
 
2. <span data-ttu-id="673f2-p104">В запущенном приложении откройте экран просмотра для объекта, представляющего список, в который вы добавили канал новостей. Если вы включили параметр **Размещать при создании**, добавьте новый элемент. Если вы включили параметр **Размещать при обновлении**, отредактируйте поля, выбранные в диалоговом окне **Выбор триггеров записи**.</span><span class="sxs-lookup"><span data-stu-id="673f2-p104">In the running application, open the browse screen for the entity representing the list where you added a newsfeed. If you enabled **Post when Created**, add a new item. If you enabled **Post when Updated**, edit the fields that you selected in the **Choose post triggers** dialog box.</span></span>
    
 
3. <span data-ttu-id="673f2-126">На панели хрома SharePoint выберите ссылку **Канал новостей**.</span><span class="sxs-lookup"><span data-stu-id="673f2-126">On the SharePoint chrome bar, choose the **Newsfeed** link.</span></span>
    
  ![Панель хрома SharePoint](../../images/CBAnewsfeed.PNG)
 

    <span data-ttu-id="673f2-p105">В новом окне браузера откроется страница **Канал новостей** с записями для добавленных и обновленных элементов. Вы можете нажать **Мне нравится** рядом с той или иной записью или **Ответить**, чтобы добавить комментарий.</span><span class="sxs-lookup"><span data-stu-id="673f2-p105">The **Newsfeed** page opens in a new browser window with entries for the added and/or updated items. You can choose the **Like** link for a post, or you can choose the **Reply** link to add a comment.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="673f2-130">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="673f2-130">Additional resources</span></span>
<span data-ttu-id="673f2-131"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="673f2-131"></span></span>


-  [<span data-ttu-id="673f2-132">Разработка облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="673f2-132">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins)
    
 
-  [<span data-ttu-id="673f2-133">Функции социальных медиа и совместной работы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="673f2-133">Social and collaboration features in SharePoint</span></span>](http://msdn.microsoft.com/en-us/library/office/jj163280.aspx)
    
 
-  [<span data-ttu-id="673f2-134">Создание облачных бизнес-надстроек с каналом новостей для социальных служб</span><span class="sxs-lookup"><span data-stu-id="673f2-134">Create a cloud business add-in with a social newsfeed</span></span>](create-a-cloud-business-add-in-with-a-social-newsfeed)
    
 

