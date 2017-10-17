---
title: "Сопоставление библиотеки документов с объектом"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 770b85777e274ca3e1a633d6d018d3ba114ce031
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="associate-a-document-library-with-an-entity"></a><span data-ttu-id="c7fc5-102">Сопоставление библиотеки документов с объектом</span><span class="sxs-lookup"><span data-stu-id="c7fc5-102">Associate a document library with an entity</span></span>
<span data-ttu-id="c7fc5-p101">Используя библиотеки документов в SharePoint, можно создавать и загружать документы, связанные с определенными элементами списка или объекта. Например, в библиотеке можно хранить литературу по продажам и руководства по использованию для каждого продукта в списке. В облачной бизнес-надстройке библиотеку документов можно связать с объектом, создав отношение.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p101">By using the document library feature in SharePoint, you can create or upload documents associated with individual items in a list or entity. For example, you might use a document library to store sales literature and product manuals for each product in a list. In a Cloud Business Add-in, you can associate a document library with an entity by creating a relationship.</span></span>
 

 <span data-ttu-id="c7fc5-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="associating-a-document-library"></a><span data-ttu-id="c7fc5-109">Сопоставление библиотеки документов</span><span class="sxs-lookup"><span data-stu-id="c7fc5-109">Associating a Document Library</span></span>

<span data-ttu-id="c7fc5-110">Процесс привязки библиотеки документов с объектом состоит из трех этапов:</span><span class="sxs-lookup"><span data-stu-id="c7fc5-110">The process of associating a document library with an entity involves three steps:</span></span>
 

 

1. <span data-ttu-id="c7fc5-111">Добавьте библиотеку документов SharePoint в свой проект в качестве источника данных.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-111">Add a SharePoint document library to your project as a data source.</span></span>
    
     <span data-ttu-id="c7fc5-p103">**Важно!** Сначала вам потребуется создать библиотеку документов на своем сайте SharePoint. Она должна содержать настраиваемый столбец, сопоставленный с уникальным полем в объекте.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p103">**Important**  You must first create a document library on your SharePoint site. It must contain a custom column that maps to a unique field in your entity.</span></span>
2. <span data-ttu-id="c7fc5-114">Создание отношения между библиотекой документов и объектом.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-114">Create a relationship between the document library and an entity.</span></span>
    
 
3. <span data-ttu-id="c7fc5-p104">Добавить библиотеку документов на экран. Процесс зависит от того, создается ли новый экран или добавляется ли библиотека документов на существующий экран.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p104">Add the document library to a screen. The process differs depending on whether you're creating a new screen or adding it to an existing screen.</span></span>
    
 

### <a name="to-add-a-document-library"></a><span data-ttu-id="c7fc5-117">Добавление библиотеки документов</span><span class="sxs-lookup"><span data-stu-id="c7fc5-117">To add a document library</span></span>


1. <span data-ttu-id="c7fc5-118">В **обозревателе решений** откройте контекстное меню узла **Источники данных** и выберите пункт **Добавить источник данных**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-118">In  **Solution Explorer**, open the shortcut menu for the  **Data Sources** node and choose **Add Data Source**.</span></span>
    
 
2. <span data-ttu-id="c7fc5-119">В **мастере подключения к источнику данных** щелкните значок **SharePoint** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-119">In the  **Attach Data Source Wizard**, choose the  **SharePoint** icon, and then choose the **Next** button.</span></span>
    
 
3. <span data-ttu-id="c7fc5-120">На странице **Ввод сведений для подключения** в текстовом поле **Укажите адрес сайта SharePoint** введите URL-адрес сайта разработчика SharePoint и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-120">On the  **Enter Connection Information** page, in the **Specify the SharePoint site address** text box, enter the URL for your SharePoint developer site, and then choose the **Next** button.</span></span>
    
 
4. <span data-ttu-id="c7fc5-121">На странице **Выбор элементов SharePoint** в левой области выберите элемент списка **Библиотеки документов**, а в правой области установите флажок для библиотеки документов, как показано на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-121">On the  **Choose your SharePoint Items** page, in the left pane, choose the **Document Libraries** list item, and in the right pane, select the checkbox for your document library as shown in Figure 1.</span></span>
    
    <span data-ttu-id="c7fc5-122">**Рис. 1. Выбор библиотеки документов**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-122">**Figure 1. Selecting the document library**</span></span>

 

  ![Выбор библиотеки документов](../images/CBADocLibrary.PNG)
 

    <span data-ttu-id="c7fc5-124">На рис. 2 показана библиотека документов на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-124">Figure 2 shows the document library on the SharePoint site.</span></span>
    

    <span data-ttu-id="c7fc5-125">**Рис. 2. Обратите внимание на настраиваемый столбец ProductName (Название продукта)**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-125">**Figure 2. Note the custom ProductName column**</span></span>

 

  ![Библиотека документов с настраиваемым столбцом ProductName (Название продукта)](../images/CBADocLibrary2.PNG)
 

    
     <span data-ttu-id="c7fc5-127">**Важно!** Библиотека документов должна уже существовать и содержать настраиваемый столбец, сопоставленный с уникальным полем в вашем объекте.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-127">**Important**  The document library must already exist and must contain a custom column that maps to a unique field in your entity.</span></span>
5. <span data-ttu-id="c7fc5-128">Введите имя в поле **Укажите имя источника данных** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-128">In the  **Specify the name of the data source**, enter a name, and then choose the  **Finish** button.</span></span>
    
 

### <a name="to-create-a-relationship"></a><span data-ttu-id="c7fc5-129">Создание отношения</span><span class="sxs-lookup"><span data-stu-id="c7fc5-129">To create a relationship</span></span>


1. <span data-ttu-id="c7fc5-130">В **обозревателе решений** откройте объект библиотеки документов и на панели **Перспектива** откройте вкладку **Сервер**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-130">In  **Solution Explorer**, open the document library entity, and then on the  **Perspective** bar, choose the **Server** tab.</span></span>
    
 
2. <span data-ttu-id="c7fc5-131">На панели инструментов щелкните **Отношение**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-131">On the toolbar, choose  **Relationship**.</span></span>
    
 
3. <span data-ttu-id="c7fc5-132">В диалоговом окне **Добавление нового отношения** в раскрывающемся списке **К:** выберите объект, с которым нужно создать отношение, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-132">In the  **Add New Relationship** dialog box, in the **To** dropdown list, choose the entity that you want to associate, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="c7fc5-133">**Рис. 3. Создание отношения**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-133">**Figure 3. Creating a relationship.**</span></span>

 

  ![Создание отношения](../images/CBARelationship.PNG)
 

 

 
4. <span data-ttu-id="c7fc5-135">В раскрывающемся списке **Внешний ключ** выберите настраиваемый столбец в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-135">In the  **Foreign** key dropdown list, choose the custom column from your document library.</span></span>
    
 
5. <span data-ttu-id="c7fc5-p105">В раскрывающемся списке **Первичный ключ** выберите поле объекта, которое необходимо сопоставить с настраиваемым столбцом в библиотеке документов, а затем нажмите кнопку **ОК**. Например, для настраиваемого столбца ProductName (Название продукта) выберите поле ProductName (Название продукта), как показано на рис. 4.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p105">In the  **Primary** key dropdown list, choose the field from your entity that maps to the custom column in the document library, and then choose the **OK** button. For example, for a ProductName custom column, choose the ProductName field, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="c7fc5-138">**Рис. 4. Связанные внешний и первичный ключи**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-138">**Figure 4. Related foreign and primary keys**</span></span>

 

  ![Задание связанных свойств](../images/CBARelationship2.PNG)
 

    
     <span data-ttu-id="c7fc5-140">**Примечание.** Поле должно иметь такой же тип данных, что и поле **Внешний ключ**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-140">**Note**  The field must be of the same data type as the  **Foreign** key field.</span></span>

### <a name="to-add-a-document-library-to-a-new-screen-set"></a><span data-ttu-id="c7fc5-141">Добавление библиотеки документов на новый набор экранов</span><span class="sxs-lookup"><span data-stu-id="c7fc5-141">To add a document library to a new screen set</span></span>


1. <span data-ttu-id="c7fc5-142">В **обозревателе решений** откройте объект, сопоставленный с библиотекой документов, и на панели **Перспектива** откройте вкладку **HTMLClient**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-142">In  **Solution Explorer**, open the entity that is associated with a document library, and then on the  **Perspective** bar, choose the **HTMLClient** tab.</span></span>
    
 
2. <span data-ttu-id="c7fc5-143">На панели инструментов щелкните **Экран**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-143">On the toolbar, choose  **Screen**.</span></span>
    
 
3. <span data-ttu-id="c7fc5-144">В диалоговом окне **Добавление экрана** в текстовом поле **Имя набора экранов** введите имя набора экранов.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-144">In the  **Add New Screen** dialog box, in the **Screen Set Name** text box, enter a name for the screen set.</span></span>
    
 
4. <span data-ttu-id="c7fc5-145">В списке **Данные экрана** выберите ваш объект.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-145">In the  **Screen Data** list, choose your entity.</span></span>
    
 
5. <span data-ttu-id="c7fc5-146">В списке **Включить дополнительные данные** установите флажок для вашей библиотеки документов и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-146">In the  **Additional Data to Include** list, select the checkbox for your document library, and then choose the **OK** button.</span></span>
    
    <span data-ttu-id="c7fc5-147">На рис. 5 показан набор экранов для объекта Product (Продукт).</span><span class="sxs-lookup"><span data-stu-id="c7fc5-147">Figure 5 shows a screen set for a Product entity.</span></span>
    

    <span data-ttu-id="c7fc5-148">**Рис. 5. Набор экранов Product (Продукт)**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-148">**Figure 5. Products screen set**</span></span>

 

  ![Диалоговое окно "Добавление экрана"](../images/CBAScreenSet.PNG)
 

    <span data-ttu-id="c7fc5-p106">Экран **просмотра**, созданный для объекта, содержит вкладку **Documents** (Документы) и кнопку **Add Document** (Добавить документ). При ее нажатии отображается всплывающее окно для добавления или отправки документов.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p106">The  **View** screen that is created for the entity contains a **Documents** tab with an **Add Document** button. The button displays a Popup for adding or uploading documents.</span></span>
    
 

### <a name="to-add-a-document-library-to-an-existing-screen"></a><span data-ttu-id="c7fc5-152">Добавление библиотеки документов на существующий экран</span><span class="sxs-lookup"><span data-stu-id="c7fc5-152">To add a document library to an existing screen</span></span>


1. <span data-ttu-id="c7fc5-153">В **обозревателе решений** откройте контекстное меню для экрана, который вы хотите сопоставить с библиотекой документов, и нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-153">In  **Solution Explorer**, open the shortcut menu for the screen that you want to associate with a document library and choose  **Open**.</span></span>
    
 
2. <span data-ttu-id="c7fc5-154">В конструкторе экрана выберите узел **Вкладки**, как показано на рис. 6, а затем узел **Добавить вкладку**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-154">In the screen designer, choose the  **Tabs** node as shown in Figure 6, and then choose the **Add Tab** node.</span></span>
    
    <span data-ttu-id="c7fc5-155">**Рис. 6. Узел "Вкладки"**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-155">**Figure 6. The Tabs node**</span></span>

 

  ![Добавление новой вкладки](../images/CBAAddTab.PNG)
 

 

 
3. <span data-ttu-id="c7fc5-157">В окне **Свойства** выберите свойство **Отображаемое имя** и введите понятное имя для добавленной вкладки. Например, Documents (Документы).</span><span class="sxs-lookup"><span data-stu-id="c7fc5-157">In the  **Properties** window, choose the **Display Name** property and enter a meaningful name for the newly added tab. For example,Documents.</span></span>
    
 
4. <span data-ttu-id="c7fc5-158">В левой области конструктора экрана щелкните ссылку **Add** _DocumentLibraryName_ (Добавить имя библиотеки документов), как показано на рис. 7, где _DocumentLibraryName_ — имя вашей библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-158">In the left pane of the screen designer, choose the  **Add** _DocumentLibraryName_ link as shown in Figure 7, where _DocumentLibraryName_ is the name of your document library.</span></span>
    
    <span data-ttu-id="c7fc5-159">**Рис. 7. Ссылка Add ProductDocuments (Добавить документы, связанные с продуктом)**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-159">**Figure 7. The Add ProductDocuments link**</span></span>

 

  ![Добавление объекта Documents (Документы)](../images/CBAAddDoc.PNG)
 

 

 
5. <span data-ttu-id="c7fc5-161">В центральной области выберите узел новой вкладки, раскройте список **Добавить** и выберите _DocumentLibraryName_ (Имя библиотеки документов).</span><span class="sxs-lookup"><span data-stu-id="c7fc5-161">In the center pane, choose the node for the new tab, expand the  **Add** list, and then choose _DocumentLibraryName_.</span></span>
    
 
6. <span data-ttu-id="c7fc5-162">Разверните узел **Панель команд** для новой вкладки, как показано на рис. 8, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-162">Expand the  **Command Bar** node for the new tab as shown in Figure 8 and choose **Add**.</span></span>
    
    <span data-ttu-id="c7fc5-163">**Рис. 8. Узел "Панель команд"**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-163">**Figure 8. The Command Bar node**</span></span>

 

  ![Добавление кнопки](../images/CBAAddButton.PNG)
 

 

 
7. <span data-ttu-id="c7fc5-165">В диалоговом окне **Добавление кнопки** примите настройки, используемые по умолчанию, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-165">In the  **Add Button** dialog box, accept the default choices and choose the **OK** button.</span></span>
    
    <span data-ttu-id="c7fc5-166">На рис. 9 показано диалоговое окно **Добавление кнопки** с методом **createOrUploadDocument**, используемым по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-166">Figure 9 shows the  **Add Button** dialog box with the default method, **createOrUploadDocument**.</span></span>
    

    <span data-ttu-id="c7fc5-167">**Рис. 9. Диалоговое окно "Добавление кнопки"**</span><span class="sxs-lookup"><span data-stu-id="c7fc5-167">**Figure 9. The Add Button dialog box**</span></span>

 

  ![Диалоговое окно "Добавление кнопки"](../images/CBAAddDialog.PNG)
 

 

 
8. <span data-ttu-id="c7fc5-p107">В окне **Свойства** выберите свойство **Отображаемое имя** и введите понятное имя кнопки, например Add Document (Добавить документ).</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p107">In the  **Properties** window, choose the **Display Name** property and enter a meaningful name for the button. For example,Add Document.</span></span>
    
    <span data-ttu-id="c7fc5-p108">Теперь на экране есть вкладка **Documents** (Документы) с кнопкой на панели команд. При нажатии кнопки отображается всплывающее окно для добавления или отправки документов.</span><span class="sxs-lookup"><span data-stu-id="c7fc5-p108">The screen now contains a  **Documents** tab with a button on the command bar. The button displays a Popup for adding or uploading documents.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="c7fc5-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c7fc5-173">Additional resources</span></span>
<span data-ttu-id="c7fc5-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c7fc5-174"></span></span>


-  [<span data-ttu-id="c7fc5-175">Разработка облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="c7fc5-175">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins.md)
    
 
-  [<span data-ttu-id="c7fc5-176">Диспетчер инцидентов: руководство по созданию облачной бизнес-надстройки</span><span class="sxs-lookup"><span data-stu-id="c7fc5-176">Incident manager: A cloud business add-in tutorial</span></span>](incident-manager-a-cloud-business-add-in-tutorial.md)
    
 

