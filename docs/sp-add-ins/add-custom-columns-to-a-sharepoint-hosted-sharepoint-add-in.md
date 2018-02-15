---
title: "Добавление настраиваемых столбцов в надстройку SharePoint, размещаемую в SharePoint"
description: "Создание настраиваемых типов столбцов, запуск надстройки и тестирование столбцов."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: d2ac6a7455aaceb0490c74efbcb3cb47e2099d36
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="d9b11-103">Добавление собственных столбцов в надстройки с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d9b11-103">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="d9b11-104">Это третья часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="d9b11-104">This is the third in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 
    
> [!NOTE]
> <span data-ttu-id="d9b11-105">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="d9b11-105">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="d9b11-106">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeColumns.sln.</span><span class="sxs-lookup"><span data-stu-id="d9b11-106">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>

<span data-ttu-id="d9b11-107">В этой статье мы вернемся к программированию и добавим несколько столбцов сайта в надстройку SharePoint Employee Orientation (Адаптация сотрудников).</span><span class="sxs-lookup"><span data-stu-id="d9b11-107">In this article, we get back to coding by adding some site columns to the Employee Orientation SharePoint Add-in.</span></span>
 
## <a name="create-custom-column-types"></a><span data-ttu-id="d9b11-108">Создание настраиваемых типов столбцов</span><span class="sxs-lookup"><span data-stu-id="d9b11-108">Create custom column types</span></span>

1. <span data-ttu-id="d9b11-109">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-109">In **Solution Explorer**, right-click the project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="d9b11-110">Присвойте папке имя **Site Columns** (Столбцы сайта).</span><span class="sxs-lookup"><span data-stu-id="d9b11-110">Name the folder **Site Columns**.</span></span>    
 
2. <span data-ttu-id="d9b11-111">Щелкните правой кнопкой мыши новую папку и выберите пункты **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-111">Right-click the new folder, and select **Add** > **New Item**.</span></span> <span data-ttu-id="d9b11-112">В узле **Office/SharePoint** откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-112">The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
     
3. <span data-ttu-id="d9b11-113">Выберите пункт **Site Column** (Столбец сайта), присвойте столбцу имя **Division** (Подразделение) и нажмите кнопку**Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-113">Select **Site Column**, give it the name **Division**, and then select **Add**.</span></span>
    
4. <span data-ttu-id="d9b11-114">В файле elements.xml нового столбца сайта измените элемент **Field** так, чтобы он содержал атрибуты и значения, указанные в примере ниже. ***Не** следует изменять идентификатор GUID* атрибута **ID** (т. е удалять значение, созданное Visual Studio), *поэтому будьте внимательны при копировании и вставке*.</span><span class="sxs-lookup"><span data-stu-id="d9b11-114">In the elements.xml file for the new site column, edit the **Field** element so that it has the attributes and values shown in the following example, except that *you should **not** change the GUID* for the **ID** attribute from the value that Visual Studio generated for it, *so be careful if you are using copy-and-paste*.</span></span>
    
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
    
    <br/>

5. <span data-ttu-id="d9b11-115">Добавьте другой **столбец сайта** с именем **OrientationStage** (Этап адаптации) в ту же папку.</span><span class="sxs-lookup"><span data-stu-id="d9b11-115">Add another **Site Column** named **OrientationStage** to the same folder .</span></span>
    
6. <span data-ttu-id="d9b11-116">В файле elements.xml нового столбца сайта измените элемент **Field** так, чтобы он содержал атрибуты и значения, указанные в примере ниже, однако не меняйте GUID атрибута **ID**. Оставьте для него значение, созданное Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9b11-116">In the elements.xml file for the new site column, edit the **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value that Visual Studio generated for it.</span></span>
    
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
    
    <br/>

7. <span data-ttu-id="d9b11-117">Так как это поле является полем выбора (Choice), необходимо указать возможные варианты и порядок их отображения в раскрывающемся списке перед пользователем, который должен сделать выбор.</span><span class="sxs-lookup"><span data-stu-id="d9b11-117">Because this is a Choice field, you must specify the possible choices and the order in which they should appear in the drop-down list when a user is making a choice.</span></span> <span data-ttu-id="d9b11-118">Так как это поле обязательно для заполнения, необходимо указать значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d9b11-118">Because it is a required field, you must specify a default value.</span></span> <span data-ttu-id="d9b11-119">Добавьте приведенную ниже дочернюю разметку в элемент **Field**, а затем сохраните все файлы.</span><span class="sxs-lookup"><span data-stu-id="d9b11-119">Add the following child markup to the **Field** element, and then save all the files.</span></span>
    
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

    </br>
    
## <a name="run-the-add-in-and-test-the-columns"></a><span data-ttu-id="d9b11-120">Запуск надстройки и тестирование столбцов</span><span class="sxs-lookup"><span data-stu-id="d9b11-120">Run the add-in and test the columns</span></span>

1. <span data-ttu-id="d9b11-p105">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="d9b11-p105">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span>  
 
2. <span data-ttu-id="d9b11-123">Когда откроется страница надстройки по умолчанию, щелкните ссылку **New Employees in Seattle** (Новые сотрудники в Сиэтле), чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="d9b11-123">When the add-in's default page opens, select the **New Employees in Seattle** link to open the custom list instance.</span></span>
 
3. <span data-ttu-id="d9b11-124">Откройте страницу **Параметры** списка и добавьте в него два столбца, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d9b11-124">Open the list's **Settings** page and add the two columns to it with these steps:</span></span>
    
    1. <span data-ttu-id="d9b11-125">Нажмите кнопку выноски **· · ·** сразу над списком и выберите пункт **Создать представление**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-125">Select the callout button, **· · ·** just above the list, and then select **Create View**.</span></span>
    2. <span data-ttu-id="d9b11-126">Откроется страница **Тип представления** со структурой строки навигации **Параметры > Тип представления** рядом с верхней границей страницы.</span><span class="sxs-lookup"><span data-stu-id="d9b11-126">The **View Type** page opens, with the breadcrumb structure **Settings > View Type** near the top.</span></span> <span data-ttu-id="d9b11-127">Выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-127">Select the **Settings** breadcrumb.</span></span>
    
        <span data-ttu-id="d9b11-128">*Рис. 1. Открытие страницы параметров списка*</span><span class="sxs-lookup"><span data-stu-id="d9b11-128">*Figure 1. Steps to open the list settings page*</span></span>

        ![Список новых сотрудников в Сиэтле с кнопкой выноски и элементом создания представления, выделенным как первый шаг. Еще указана стрелка на страницу создания представления с выделенной строкой навигации "Параметры".](../images/6c119cae-adf8-42ff-9890-f3aa1e11719d.png)
 
    3. <span data-ttu-id="d9b11-131">На странице **Параметры** щелкните ссылку **Добавить из существующих столбцов сайта** слева, примерно посередине страницы.</span><span class="sxs-lookup"><span data-stu-id="d9b11-131">On the **Settings** page, open the **Add from existing site columns** link on the left about halfway down the page.</span></span>
    
        <span data-ttu-id="d9b11-132">*Рис. 2. Страница "Параметры списка"*</span><span class="sxs-lookup"><span data-stu-id="d9b11-132">*Figure 2. List settings page*</span></span>

        ![Страница параметров экземпляра списка с выделенной ссылкой "Добавление столбцов из столбцов сайта".](../images/a8698b77-b9d2-40f6-89f6-ccc3c6e06073.png)

    4. <span data-ttu-id="d9b11-134">На странице **Добавление столбцов из столбцов веб-сайта** в раскрывающемся списке **Выбрать столбцы сайта из** щелкните **Employee Orientation** (Адаптация сотрудников).</span><span class="sxs-lookup"><span data-stu-id="d9b11-134">On the **Add Columns from Site Columns** page, select **Employee Orientation** on the **Select site columns from** drop-down list.</span></span>
    
        <span data-ttu-id="d9b11-135">*Рис. 3. Добавление столбцов из столбцов веб-сайта*</span><span class="sxs-lookup"><span data-stu-id="d9b11-135">*Figure 3. Add Columns from Site Columns page*</span></span>

        ![Элемент управления для выбора столбцов SharePoint. В раскрывающемся списке "Выбрать столбцы сайта" выбран пункт Employee Orientation (Адаптация сотрудников).](../images/3b33c622-c52a-45fd-8ea1-d7f307539753.png)

    5. <span data-ttu-id="d9b11-137">Добавьте столбцы **Division** (Подразделение) и **OrientationStage** (Этап адаптации) в поле **Столбцы для добавления**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-137">Add the **Division** and **OrientationStage** columns to the **Columns to add** box.</span></span>

    6. <span data-ttu-id="d9b11-138">Нажмите кнопку **ОК**, чтобы вернуться на страницу **Параметры**, а затем щелкните **New Employees in Seattle** (Новые сотрудники в Сиэтле) в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d9b11-138">Select **OK** to return to the **Settings** page, and then select the **New Employees in Seattle** breadcrumb near the top of the page.</span></span>
    
4. <span data-ttu-id="d9b11-139">Новые столбцы теперь находятся в списке.</span><span class="sxs-lookup"><span data-stu-id="d9b11-139">The new columns are now on the list.</span></span> <span data-ttu-id="d9b11-140">Добавление нового элемента в список.</span><span class="sxs-lookup"><span data-stu-id="d9b11-140">Add a new item to the list.</span></span> <span data-ttu-id="d9b11-141">В форме редактирования поле **Этап адаптации** будет иметь значение по умолчанию **Не начато**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-141">On the edit form, the **Orientation Stage** field will already have the default value **Not Started**.</span></span> <span data-ttu-id="d9b11-142">(Существующие элементы в этом поле будут пустыми, так как они были созданы до того, как поле появилось в списке.)</span><span class="sxs-lookup"><span data-stu-id="d9b11-142">(The existing items will be blank in this field because they were created before the field was on the list.)</span></span>
    
    <span data-ttu-id="d9b11-143">*Рис. 4. Список с новыми столбцами*</span><span class="sxs-lookup"><span data-stu-id="d9b11-143">*Figure 4. The list with new columns*</span></span>

    ![Список с новыми столбцами Division (Подразделение) и Orientation Stage (Этап адаптации).](../images/d4e17424-c06b-4635-aab8-4912cee5fe35.png)
 
5. <span data-ttu-id="d9b11-145">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9b11-145">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="d9b11-146">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать последнюю.</span><span class="sxs-lookup"><span data-stu-id="d9b11-146">Each time that you select F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
6. <span data-ttu-id="d9b11-147">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуется отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="d9b11-147">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="d9b11-148">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-148">Right-click the project in **Solution Explorer**, and then select **Retract**.</span></span>
    

## <a name="next-steps"></a><span data-ttu-id="d9b11-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9b11-149">Next steps</span></span>
<span data-ttu-id="d9b11-150"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="d9b11-150"></span></span>

<span data-ttu-id="d9b11-151">На самом деле пользователям будет не очень удобно вручную добавлять настраиваемые столбцы в список, поэтому в следующей статье ([Добавление настраиваемого типа контента в надстройку, размещаемую в SharePoint](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)) этой серии описано, как создать настраиваемый тип контента, который включает в себя настраиваемые столбцы и автоматически сопоставляется с шаблоном списка New Employees (Новые сотрудники).</span><span class="sxs-lookup"><span data-stu-id="d9b11-151">You don't really want your users to have to manually add the custom columns to the list, so in the next article in this series, you'll create a custom content type that includes the custom columns and is automatically associated with the New Employees list template: [Add a custom content type to a SharePoint-hosted SharePoint Add-in](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span> 
 

 

