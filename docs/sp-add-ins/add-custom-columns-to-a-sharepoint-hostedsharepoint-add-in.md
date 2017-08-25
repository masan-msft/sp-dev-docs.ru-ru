# <a name="add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in"></a><span data-ttu-id="83e6b-101">Добавление настраиваемых столбцов в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83e6b-101">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>
<span data-ttu-id="83e6b-102">В этой статье рассказывается, как добавить настраиваемый столбец в надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="83e6b-102">Learn how to include custom columns in an spappplural.</span></span>
 

 <span data-ttu-id="83e6b-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="83e6b-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="83e6b-p102">Это третья часть серии статей, посвященной основам разработки надстроек, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p102">This is the third in a series of articles about the basics of developing SharePoint-hosted spappplural. You should first be familiar with SharePoint Add-ins and the pervious articles in this series:</span></span>
 

-  [<span data-ttu-id="83e6b-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83e6b-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="83e6b-109">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83e6b-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 

 <span data-ttu-id="83e6b-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeColumns.sln.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>
 

<span data-ttu-id="83e6b-112">В этой статье мы вернемся к программированию и добавим несколько столбцов сайта в надстройку SharePoint Employee Orientation (Вводное обучение для сотрудников).</span><span class="sxs-lookup"><span data-stu-id="83e6b-112">In this article we get back to coding by adding some site columns to the Employee Orientation spappsing.</span></span>
 

## <a name="create-custom-column-types"></a><span data-ttu-id="83e6b-113">Создание настраиваемых типов столбцов</span><span class="sxs-lookup"><span data-stu-id="83e6b-113">Create custom column types</span></span>


 

 

1. <span data-ttu-id="83e6b-p104">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**. Присвойте папке имя Site Columns (Столбцы сайта).</span><span class="sxs-lookup"><span data-stu-id="83e6b-p104">In  **Solution Explorer**, right-click the project and choose  **Add** > **New Folder**. Name the folder Site Columns.</span></span>
    
 
2. <span data-ttu-id="83e6b-p105">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Новый элемент**. Откроется диалоговое окно **Добавление нового элемента** (узел **Office SharePoint**).</span><span class="sxs-lookup"><span data-stu-id="83e6b-p105">Right-click the new folder and choose **Add** > **New Item**. The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
    
 
3. <span data-ttu-id="83e6b-118">Выберите пункт **Site Column** (Столбец сайта), присвойте столбцу имя Division (Подразделение) и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83e6b-118">Choose Site Column, give it the name Division, and choose Add.</span></span>
    
 
4. <span data-ttu-id="83e6b-119">В файле elements.xml для нового столбца сайта измените элемент **Field** так, чтобы он содержал атрибуты и значения, указанные в следующем примере. ***Не** изменяйте GUID* атрибута **ID** (не удаляйте значение атрибута, созданное Visual Studio), *соответственно будьте осторожны при копировании и вставке*.</span><span class="sxs-lookup"><span data-stu-id="83e6b-119">In the elements.xml file for the new site column, edit the Field element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the ID attribute from the value that vsnv generated for it, so be careful if you are using copy-and-paste.</span></span>
    
```
  <Field ID="{generated GUID}" 
       Name="Division" 
       Title="Division" 
       DisplayName="Division" 
       Description="The division of the company where the employee works." 
       Group="Employee Orientation" 
       Type="Text" 
       Required ="FALSE">
</Field>
```

5. <span data-ttu-id="83e6b-120">Добавьте еще один **столбец сайта** c именем OrientationStage (Этап вводного обучения) в ту же папку.</span><span class="sxs-lookup"><span data-stu-id="83e6b-120">Add another Site Column to the same folder named OrientationStage.</span></span>
    
 
6. <span data-ttu-id="83e6b-121">В файле elements.xml нового столбца сайта измените элемент **Field** так, чтобы он содержал атрибуты и значения, указанные в примере ниже, однако не меняйте GUID атрибута **ID**. Оставьте для него значение, созданное Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83e6b-121">In the elements.xml file for the new site column, edit the **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value Visual Studio 2012 generated for it.</span></span>
    
```
  <Field ID="{generated GUID}" 
       Name="OrientationStage" 
       Title="OrientationStage"
       DisplayName="Orientation Stage" 
       Group="Employee Orientation" 
       Description="The current orientation stage of the employee." 
       Type="Choice"
       Required ="TRUE">
</Field>
```

7. <span data-ttu-id="83e6b-p106">Так как это поле является полем выбора, необходимо указать возможные варианты, порядок их отображения в раскрывающемся списке для пользователя, который должен сделать выбор. Так как это обязательное поле, необходимо указать значение, используемое по умолчанию. Добавьте указанную ниже дочернюю разметку в элемент **Field**.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p106">Because this is a Choice field, you must specify the possible choices and the order in which they should appear in the drop-down list when a user is making a choice. And because it is a required field, you must specify a default value. Add the following child markup to the **Field** element.</span></span>
    
```
  <CHOICES>
      <CHOICE>Not Started</CHOICE>
      <CHOICE>Tour of building</CHOICE>
      <CHOICE>HR paperwork</CHOICE>
      <CHOICE>Corporate network access</CHOICE>
      <CHOICE>Completed</CHOICE>
</CHOICES>
<MAPPINGS>
      <MAPPING Value="1">Not Started</MAPPING>
      <MAPPING Value="2">Tour of building</MAPPING>
      <MAPPING Value="3">HR paperwork</MAPPING>
      <MAPPING Value="4">Corp network access</MAPPING>
      <MAPPING Value="5">Completed</MAPPING>
</MAPPINGS>
<Default>Not Started</Default>
```

8. <span data-ttu-id="83e6b-125">Сохраните все файлы.</span><span class="sxs-lookup"><span data-stu-id="83e6b-125">Save all files.</span></span>
    
 

## <a name="run-the-add-in-and-test-the-columns"></a><span data-ttu-id="83e6b-126">Запуск надстройки и тестирование столбцов</span><span class="sxs-lookup"><span data-stu-id="83e6b-126">Run the add-in and test the columns</span></span>


 

 

1. <span data-ttu-id="83e6b-p107">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p107">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
2. <span data-ttu-id="83e6b-129">Когда откроется страница надстройки, используемая по умолчанию, щелкните ссылку **Новые сотрудники в Москве**, чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="83e6b-129">When the add-in's default page opens, choose the **New Employees in Seattle** link to open the custom list instance.</span></span>
    
 
3. <span data-ttu-id="83e6b-130">Откройте страницу **Параметры** списка и добавьте в него два столбца, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="83e6b-130">Open the list's **Settings** page and add the two columns to it with these steps.</span></span>
    
      1. <span data-ttu-id="83e6b-131">Нажмите кнопку выноски **· · ·** сразу над списком, а затем щелкните **Создать представление**.</span><span class="sxs-lookup"><span data-stu-id="83e6b-131">Click the callout button, **· · ·**, just above the list, and then choose **Create View**.</span></span>
    
 
  2. <span data-ttu-id="83e6b-p108">Откроется страница **Тип представления** со структурой строки навигации **Параметры > Тип представления** рядом с верхней границей страницы. Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p108">The **View Type** page opens, with the breadcrumb structure **Settings > View Type** near the top. Click the **Settings** breadcrumb.</span></span>
    
    <span data-ttu-id="83e6b-134">**Действия, которые необходимо выполнить, чтобы открыть страницу параметров списка**</span><span class="sxs-lookup"><span data-stu-id="83e6b-134">**Steps to open the list settings page**</span></span>

 

  ![Список новых сотрудников в Сиэтле с кнопкой выноски и элементом создания представления, выделенным как первый шаг. Еще указана стрелка на страницу создания представления с выделенной строкой навигации "Параметры".](../../images/6c119cae-adf8-42ff-9890-f3aa1e11719d.png)
 

    
    
 
  3. <span data-ttu-id="83e6b-137">На странице **Параметры** щелкните ссылку **Добавить из существующих столбцов сайта** слева, примерно посередине страницы.</span><span class="sxs-lookup"><span data-stu-id="83e6b-137">On the **Settings** page, open the **Add from existing site columns**  link on the left about halfway down the page.</span></span>
    
    <span data-ttu-id="83e6b-138">**Страница "Параметры списка"**</span><span class="sxs-lookup"><span data-stu-id="83e6b-138">**List settings page**</span></span>

 

  ![Страница параметров экземпляра списка с выделенной ссылкой "Добавление столбцов из столбцов веб-сайта".](../../images/a8698b77-b9d2-40f6-89f6-ccc3c6e06073.png)
 

    
    
 
  4. <span data-ttu-id="83e6b-140">На странице **Добавление столбцов из столбцов веб-сайта** в раскрывающемся списке **Выбрать столбцы сайта из** щелкните **Employee Orientation** (Вводное обучение для сотрудника).</span><span class="sxs-lookup"><span data-stu-id="83e6b-140">On the **Add Columns from Site Columns** page, choose **Employee Orientation** on the **Select site columns from** drop down list.</span></span>
    
    <span data-ttu-id="83e6b-141">**Добавление столбцов на странице столбцов сайта**</span><span class="sxs-lookup"><span data-stu-id="83e6b-141">**Add Columsn from Site Columns page**</span></span>

 

  ![Элемент управления для выбора столбцов SharePoint. В раскрывающемся списке "Выбрать столбцы сайта" выбран пункт Employee Orientation (Вводное обучение для сотрудника).](../../images/3b33c622-c52a-45fd-8ea1-d7f307539753.png)
 

    
    
 
  5. <span data-ttu-id="83e6b-143">В поле **Столбцы для добавления** добавьте столбцы **Division** (Подразделение) и **OrientationStage** (Этап вводного обучения).</span><span class="sxs-lookup"><span data-stu-id="83e6b-143">Add the **Division** and **OrientationStage** columns to the **Columns to add** box.</span></span>
    
 
  6. <span data-ttu-id="83e6b-144">Нажмите кнопку **ОК**, чтобы вернуться на страницу **Параметры**, а затем щелкните **New Employees in Seattle** (Новые сотрудники в Сиэтле) в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="83e6b-144">Choose **OK** to return to the **Settings** page, and then click the **New Employees in Seattle** breadcrumb near the top of the page.</span></span>
    
 
4. <span data-ttu-id="83e6b-p110">Теперь новые столбцы включены в список. Добавьте новый элемент в список. На форме для редактирования поле **Orientation Stage** (Этап вводного обучения) уже будет содержать значение Not Started (Не начат), используемое по умолчанию. (Существующие элементы в этом поле будут пустыми, так как они были созданы до добавления поля в список.)</span><span class="sxs-lookup"><span data-stu-id="83e6b-p110">The new columns are now on the list. Add a new item to the list. On the edit form, the Orientation Stage field will already have the default value Not Started. (The existing items will be blank in this field because they were created before the field was on the list.)</span></span>
    
    <span data-ttu-id="83e6b-149">**Список с новыми столбцами**</span><span class="sxs-lookup"><span data-stu-id="83e6b-149">**The list with new columns**</span></span>

 

  ![Список с новыми столбцами Division (Подразделение) и Orientation Stage (Этап вводного обучения).](../../images/d4e17424-c06b-4635-aab8-4912cee5fe35.png)
 

    
    
 
5. <span data-ttu-id="83e6b-p111">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p111">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
6. <span data-ttu-id="83e6b-p112">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="83e6b-p112">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="83e6b-155"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="83e6b-155"></span></span>

<span data-ttu-id="83e6b-156">На самом деле пользователям будет не очень удобно вручную добавлять настраиваемые столбцы в список, поэтому в следующей статье ([Добавление настраиваемого типа контента в надстройку, размещаемую в SharePoint](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)) этой серии вы создадите настраиваемый тип контента, который включает в себя настраиваемые столбцы и автоматически сопоставляется с шаблоном списка New Employees (Новые сотрудники).</span><span class="sxs-lookup"><span data-stu-id="83e6b-156">You don't really want your users to have to manually add the custom columns to the list, so in the next article in this series, you'll create a custom content type that includes the custom columns and is automatically associated with the New Employees list template: [Add a custom content type to a SharePoint-hosted add-in](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in).</span></span> 
 

 

