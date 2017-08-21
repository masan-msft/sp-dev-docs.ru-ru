
# <a name="provide-a-template-for-a-document-library-in-a-cloud-business-add-in"></a><span data-ttu-id="ab1d8-101">Предоставление шаблона для библиотеки документов в облачной бизнес-надстройке</span><span class="sxs-lookup"><span data-stu-id="ab1d8-101">Provide a template for a document library in a cloud business add-in</span></span>
<span data-ttu-id="ab1d8-p101">Кроме шаблонов Office, которые доступны при добавлении документа в библиотеку документов SharePoint, вы можете предоставлять собственные шаблоны. Например, у вас может быть собственный шаблон предложения о продаже, который вы хотите использовать при добавлении новых заказов.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-p101">In addition to the Office templates that are available when you add a document to a SharePoint document library, you can provide your own templates. For example, you might have your own sales quote template that you want to use when new orders are added.</span></span>
 

 <span data-ttu-id="ab1d8-p102">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="ab1d8-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## 

<span data-ttu-id="ab1d8-p103">Если вы еще не сделали этого, сопоставьте библиотеку документов с облачной бизнес-надстройкой. См. статью [Сопоставление библиотеки документов с объектом](associate-a-document-library-with-an-entity).</span><span class="sxs-lookup"><span data-stu-id="ab1d8-p103">If you haven't already done so, associate a document library with your cloud business add-in. See  [Associate a document library with an entity](associate-a-document-library-with-an-entity).</span></span>
 

 

### <a name="to-add-a-template"></a><span data-ttu-id="ab1d8-109">Добавление шаблона</span><span class="sxs-lookup"><span data-stu-id="ab1d8-109">To add a template</span></span>


1. <span data-ttu-id="ab1d8-110">Перейдите на свой сайт разработчика SharePoint и на странице **Разработчик** выберите **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-110">Go to your SharePoint developer site and on the **Developer** page, choose **Site Contents**.</span></span>
    
 
2. <span data-ttu-id="ab1d8-111">На странице **Содержимое сайта** выберите **Параметры**, как показано на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-111">On the **Site Contents** page, choose **Settings**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="ab1d8-112">**Рис. 1. Ссылка "Параметры"**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-112">**Figure 1. The Settings link**</span></span>

 

  ![Ссылка "Параметры сайта"](../../images/CBA_IM_8b.PNG)
 

 

 
3. <span data-ttu-id="ab1d8-114">На странице **Параметры сайта** выберите в списке **Коллекции веб-дизайнера** пункт **Типы контента сайта**, как показано на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-114">On the **Site Settings** page, in the **Web Designer Galleries** list, choose **Site content types**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="ab1d8-115">**Рис. 2. Ссылка "Типы контента сайта"**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-115">**Figure 2. The Site content types link**</span></span>

 

  ![Ссылка "Типы контента сайта"](../../images/CBA_IM_26.PNG)
 

 

 
4. <span data-ttu-id="ab1d8-117">На странице **Типы контента сайта** нажмите **Создать**, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-117">On the **Site Content Types** page, choose **Create**, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="ab1d8-118">**Рис. 3. Ссылка "Создать"**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-118">**Figure 3. The Create link**</span></span>

 

  ![Ссылка "Создать"](../../images/CBA_IM_27.PNG)
 

 

 
5. <span data-ttu-id="ab1d8-p104">На странице **Создание типа контента сайта** укажите имя и описание шаблона. В поле **Родительский тип контента** выберите **Типы контента документа** и **Документ**, как показано на рис. 4.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-p104">On the **New Site Content Type** page, enter a name and description for your template. For the **Parent Content Type**, choose **Document Content Types** and **Document**, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="ab1d8-122">**Рис. 4. Выбор родительского типа контента**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-122">**Figure 4. Parent content type selections**</span></span>

 

  ![Выбор родительского типа контента](../../images/CBA_IM_28.PNG)
 

 

 
6. <span data-ttu-id="ab1d8-124">В разделе **Группа** выберите в списке **Существующая группа** пункт **Типы контента документа**, как показано на рис. 5, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-124">In the **Group** section, in the **Existing group** list, choose **Document Content Types** as shown in Figure 5, and then choose **OK**.</span></span>
    
    <span data-ttu-id="ab1d8-125">**Рис. 5. Параметр группы**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-125">**Figure 5. Group setting**</span></span>

 

  ![Параметр группы](../../images/CBA_IM_28a.PNG)
 

 

 
7. <span data-ttu-id="ab1d8-127">На странице **Тип контента сайта** выберите **Дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-127">On the **Site Content Type** page, choose **Advanced settings**.</span></span>
    
 
8. <span data-ttu-id="ab1d8-128">На странице **Дополнительные параметры** введите URL-адрес существующего шаблона документа или отправьте новый шаблон документа, как показано на рис. 6, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-128">On the **Advanced Settings** page, either enter the URL of an existing document template or upload a new document template as shown in Figure 6, and then choose **OK**.</span></span>
    
    <span data-ttu-id="ab1d8-129">**Рис. 6. Указание шаблона документа**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-129">**Figure 6. Specify the document template**</span></span>

 

  ![Указание шаблона документа](../../images/CBA_IM_29.PNG)
 

 

 
9. <span data-ttu-id="ab1d8-131">Перейдите на страницу **Содержимое сайта** и выберите библиотеку документов, а затем перейдите на страницу **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-131">Go to the **Site Contents** page and choose your document library, and then go to the **Settings** page.</span></span>
    
 
10. <span data-ttu-id="ab1d8-132">На странице **Параметры** выберите команду **Добавить из существующих типов контента сайта**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-132">On the **Settings** page, choose **Add from existing site content types**.</span></span>
    
 
11. <span data-ttu-id="ab1d8-133">На странице **Добавление типов конвента** добавьте свой шаблон, как показано на рис. 7, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-133">On the **Add Content Types** page, add your template as shown in Figure 7, and then choose **OK**.</span></span>
    
    <span data-ttu-id="ab1d8-134">**Рис. 7. Добавление шаблона**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-134">**Figure 7. Adding the template**</span></span>

 

  ![Добавление шаблона](../../images/CBA_IM_29a.PNG)
 

 

 
12. <span data-ttu-id="ab1d8-p105">Запустите надстройку и добавьте документ. Он должен появиться в диалоговом окне **Создание нового файла**, как показано на рис. 8.</span><span class="sxs-lookup"><span data-stu-id="ab1d8-p105">Run your add-in and add a document. You should see your template in the **Create a new file** dialog box, as shown in Figure 8.</span></span>
    
    <span data-ttu-id="ab1d8-138">**Рис. 8. Диалоговое окно создания файла с новым шаблоном**</span><span class="sxs-lookup"><span data-stu-id="ab1d8-138">**Figure 8. The Create a new file dialog box with the new template**</span></span>

 

  ![Диалоговое окно создания файла с новым шаблоном](../../images/CBA_IM_30.PNG)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="ab1d8-140">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ab1d8-140">Additional resources</span></span>
<span data-ttu-id="ab1d8-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ab1d8-141"></span></span>


-  [<span data-ttu-id="ab1d8-142">Разработка облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="ab1d8-142">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins)
    
 
-  [<span data-ttu-id="ab1d8-143">Сопоставление библиотеки документов с объектом</span><span class="sxs-lookup"><span data-stu-id="ab1d8-143">Associate a document library with an entity</span></span>](associate-a-document-library-with-an-entity)
    
 

