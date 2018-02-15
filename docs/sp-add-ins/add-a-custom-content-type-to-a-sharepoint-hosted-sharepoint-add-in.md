---
title: "Добавление настраиваемого типа контента в надстройку с размещением в SharePoint"
description: "Создание настраиваемого типа контента, запуск и тестирование надстройки."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: c6171e06ba9e3db26d043b9f31b2536967142184
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="a3544-103">Добавление собственного типа контента в надстройку с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a3544-103">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="a3544-104">Это четвертая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="a3544-104">This is the fourth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 
    
> [!NOTE]
> <span data-ttu-id="a3544-105">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="a3544-105">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="a3544-106">Вы можете также скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeContentType.sln.</span><span class="sxs-lookup"><span data-stu-id="a3544-106">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeContentType.sln file.</span></span>

<span data-ttu-id="a3544-107">В этой статье описано, как добавить настраиваемый тип контента в надстройку SharePoint Employee Orientation (Адаптация сотрудников).</span><span class="sxs-lookup"><span data-stu-id="a3544-107">In this article, you add a custom content type to the Employee Orientation SharePoint Add-in.</span></span>
 

## <a name="create-the-custom-content-type"></a><span data-ttu-id="a3544-108">Создание настраиваемого типа контента</span><span class="sxs-lookup"><span data-stu-id="a3544-108">Create the custom content type</span></span>

1. <span data-ttu-id="a3544-109">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="a3544-109">In **Solution Explorer**, right-click the project and select **Add** > **New Folder**.</span></span> <span data-ttu-id="a3544-110">Присвойте папке имя **Content Types** (Типы контента).</span><span class="sxs-lookup"><span data-stu-id="a3544-110">Name the folder **Content Types**.</span></span>
     
2. <span data-ttu-id="a3544-111">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="a3544-111">Right-click the new folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="a3544-112">В узле **Office/SharePoint** откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="a3544-112">The **Add New Item** dialog box opens to the **Office/SharePoint** node.</span></span>
     
3. <span data-ttu-id="a3544-113">Выберите **Тип контента** и присвойте ему имя **NewEmployee**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3544-113">Select **Content Type** and give it the name **NewEmployee**, and then select **Add**.</span></span> <span data-ttu-id="a3544-114">При запросе мастера выбрать базовый тип содержимого щелкните **Элемент**, и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="a3544-114">When prompted by the wizard to select the base content type, select **Item**, and then select **Finish**.</span></span>   
 
4. <span data-ttu-id="a3544-115">Если конструктор типов контента не открылся автоматически, откройте его самостоятельно, выбрав тип контента **NewEmployee** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="a3544-115">If the content type designer does not automatically open, select the **NewEmployee** content type in **Solution Explorer** to open it.</span></span>
    
5. <span data-ttu-id="a3544-116">В конструкторе откройте вкладку **Тип контента** и заполните текстовые поля так:</span><span class="sxs-lookup"><span data-stu-id="a3544-116">Open the **Content Type** tab in the designer, and fill in the text boxes as follows:</span></span>
    
   -  <span data-ttu-id="a3544-117">**Имя типа контента**: NewEmployee</span><span class="sxs-lookup"><span data-stu-id="a3544-117">**Content Type Name**: NewEmployee</span></span>
   -  <span data-ttu-id="a3544-118">**Описание**: "Представляет нового сотрудника"</span><span class="sxs-lookup"><span data-stu-id="a3544-118">**Description**: Represents a new employee</span></span>
   -  <span data-ttu-id="a3544-119">**Имя группы**: "Адаптация сотрудников"</span><span class="sxs-lookup"><span data-stu-id="a3544-119">**Group Name**: Employee Orientation</span></span>
 
6. <span data-ttu-id="a3544-120">Убедитесь, что на вкладке не установлен *ни один* флажок.</span><span class="sxs-lookup"><span data-stu-id="a3544-120">Verify that *none* of the check boxes on the tab are selected.</span></span> <span data-ttu-id="a3544-121">Флажок **Наследует столбцы родительского типа содержимого** может быть установлен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a3544-121">The check box for **Inherits the columns from the parent Content Type** may be selected by default.</span></span> <span data-ttu-id="a3544-122">*Обязательно снимите его.*</span><span class="sxs-lookup"><span data-stu-id="a3544-122">*Be sure to clear it.*</span></span>  <span data-ttu-id="a3544-123">Теперь вкладка должна выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a3544-123">The tab should now look like the following:</span></span>
    
    <span data-ttu-id="a3544-124">*Рис. 1. Вкладка "Тип контента"*</span><span class="sxs-lookup"><span data-stu-id="a3544-124">*Figure 1. Content Type Tab*</span></span>

    ![Конструктор типов контента, в котором отображаются имя типа NewEmployee, описание "Представляет нового сотрудника" и группа "Адаптация сотрудников".](../images/8a9768f4-315d-45c0-88d7-687dbf84495c.PNG)
 
7. <span data-ttu-id="a3544-126">Откройте вкладку конструктора **Столбцы**.</span><span class="sxs-lookup"><span data-stu-id="a3544-126">Open the **Columns** tab in the designer.</span></span>
     
8. <span data-ttu-id="a3544-127">В таблице выберите **Щелкните здесь, чтобы добавить столбец** и добавьте столбец **Подразделение**.</span><span class="sxs-lookup"><span data-stu-id="a3544-127">In the grid, select **Click here to add a column** to open a drop-down list of columns, and add the **Division** column.</span></span> <span data-ttu-id="a3544-128">Для этого выберите пункт **Подразделение** в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="a3544-128">It is listed in the drop-down list by its display name **Division**.</span></span> <span data-ttu-id="a3544-129">Так же добавьте столбец **Этап адаптации**.</span><span class="sxs-lookup"><span data-stu-id="a3544-129">Do the same for the **Orientation Stage** column.</span></span> <span data-ttu-id="a3544-130">(Если этих пунктов нет в списке, это значит, что вы используете неправильное решение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3544-130">(If they are not listed, you may not have started with the correct Visual Studio solution.</span></span> <span data-ttu-id="a3544-131">Начните с файла BeforeContentType.sln.) По завершении таблица должна выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a3544-131">Start with BeforeContentType.sln.) When you are finished, the grid should look like the following:</span></span>
    
    <span data-ttu-id="a3544-132">*Рис. 2. Вкладка "Столбцы"*</span><span class="sxs-lookup"><span data-stu-id="a3544-132">*Figure 2. Columns Tab*</span></span>

    ![Вкладка "Столбцы" конструктора типов контента со столбцами "Сотрудник", "Подразделение" и "Этап адаптации" в таблице.](../images/835e78b3-a073-45b2-b4ee-3f9be9d88495.PNG)

9. <span data-ttu-id="a3544-134">Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="a3544-134">Save the file and close the designer.</span></span>

### <a name="modify-the-elementsxml-file"></a><span data-ttu-id="a3544-135">Изменение файла elements.xml</span><span class="sxs-lookup"><span data-stu-id="a3544-135">Modify the elements.xml file</span></span>

1. <span data-ttu-id="a3544-136">На следующем этапе вам потребуется работать непосредственно с необработанным кодом XML типа контента, поэтому в **обозревателе решений** необходимо выбрать дочерний файл elements.xml типа контента **NewEmployee**.</span><span class="sxs-lookup"><span data-stu-id="a3544-136">The next step requires that you work directly in the raw XML for the content type, so in **Solution Explorer**, select the elements.xml file child of the **NewEmployee** content type.</span></span>
    
2. <span data-ttu-id="a3544-137">В файле двух добавленных вами столбцов уже есть элементы **FieldRef**.</span><span class="sxs-lookup"><span data-stu-id="a3544-137">There are already **FieldRef** elements in the file for the two columns that you added.</span></span> <span data-ttu-id="a3544-138">Добавьте элементы **FieldRef** для двух встроенных столбцов SharePoint, которые будут равнозначны двум уже имеющимся.</span><span class="sxs-lookup"><span data-stu-id="a3544-138">Add **FieldRef** elements for two built-in SharePoint columns as peers of the two that are already there.</span></span> <span data-ttu-id="a3544-139">Ниже приведена разметка для элементов.</span><span class="sxs-lookup"><span data-stu-id="a3544-139">The following is the markup for the elements.</span></span> <span data-ttu-id="a3544-140">*Необходимо использовать эти же идентификаторы GUID для атрибута ID, так как это встроенные типы полей с фиксированными ID.*</span><span class="sxs-lookup"><span data-stu-id="a3544-140">*You must use these same GUIDs for the ID attribute because these are built-in field types with fixed IDs.*</span></span> <span data-ttu-id="a3544-141">Добавьте их *над* двумя элементами **FieldRef** настраиваемых столбцов сайта.</span><span class="sxs-lookup"><span data-stu-id="a3544-141">Add these *above* the two **FieldRef** elements for the custom site columns.</span></span> <span data-ttu-id="a3544-142">Обратите внимание, что этим полям присвоено отображаемое имя **Сотрудник**.</span><span class="sxs-lookup"><span data-stu-id="a3544-142">Note that we have given these fields the custom display name **Employee**.</span></span>
    
    ```
      <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
    ```
 
3. <span data-ttu-id="a3544-143">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="a3544-143">Save and close the file.</span></span>
 
###  <a name="modify-content-type-settings"></a><span data-ttu-id="a3544-144">Изменение параметров типа контента</span><span class="sxs-lookup"><span data-stu-id="a3544-144">Modify Content Type settings</span></span>

1. <span data-ttu-id="a3544-145">Разверните узел **Lists** (Списки) в **обозревателе решений** и выберите список **NewEmployeeOrientation**, чтобы открыть конструктор типов списка.</span><span class="sxs-lookup"><span data-stu-id="a3544-145">Expand the **Lists** node in **Solution Explorer**, and select **NewEmployeeOrientation** to open the list type designer.</span></span>
    
2. <span data-ttu-id="a3544-146">Откройте вкладку **Столбцы** конструктора и нажмите кнопку **Типы контента**.</span><span class="sxs-lookup"><span data-stu-id="a3544-146">Open the **Columns** tab in the designer, and then select the **Content Types** button.</span></span>
    
3. <span data-ttu-id="a3544-147">В диалоговом окне **Параметры типа контента** добавьте тип контента **NewEmployee**.</span><span class="sxs-lookup"><span data-stu-id="a3544-147">In the **Content Type Settings** dialog box, add the **NewEmployee** content type.</span></span>
    
4. <span data-ttu-id="a3544-148">Выберите тип контента **NewEmployee** в списке типов контента, а затем нажмите кнопку **По умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="a3544-148">Select the **NewEmployee** content type in the list of types, and then select the **Set as Default** button.</span></span>
 
5. <span data-ttu-id="a3544-149">Выберите тип контента **Item**, щелкните правой кнопкой мыши маленькую стрелку слева от имени типа контента и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="a3544-149">Select the **Item** content type, right-click the small arrowhead that appears to the left of the content type name, and then select **Delete**.</span></span>
    
6. <span data-ttu-id="a3544-150">Повторите предыдущий этап для типа контента **Folder**, чтобы в списке остался только тип контента **NewEmployee**.</span><span class="sxs-lookup"><span data-stu-id="a3544-150">Repeat the preceding step for the **Folder** content type, so that **NewEmployee** is the only content type listed.</span></span> <span data-ttu-id="a3544-151">Диалоговое окно должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a3544-151">The dialog box should now look like the following:</span></span>
    
    <span data-ttu-id="a3544-152">*Рис. 3. Диалоговое окно "Параметры типа контента"*</span><span class="sxs-lookup"><span data-stu-id="a3544-152">*Figure 3. Content Type Settings dialog box*</span></span>

    ![Диалоговое окно параметров типа контента только с типом контента NewEmployee.](../images/b90699f4-40de-4f50-ad47-3e8773d0eb92.PNG)
 
7.  <span data-ttu-id="a3544-154">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="a3544-154">Select **OK** to close the dialog box, and then save and close the file.</span></span>

### <a name="modify-the-schemaxml-file-and-elementxml-file"></a><span data-ttu-id="a3544-155">Изменение файлов schema.xml и element.xml</span><span class="sxs-lookup"><span data-stu-id="a3544-155">Modify the schema.xml file and element.xml file</span></span>

1. <span data-ttu-id="a3544-156">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-156">Open the schema.xml file.</span></span>
    
2. <span data-ttu-id="a3544-157">Найдите элемент **Fields**.</span><span class="sxs-lookup"><span data-stu-id="a3544-157">Find the **Fields** element.</span></span> <span data-ttu-id="a3544-158">В нем должны быть три элемента **Field**: **Title**, **Division** и **OrientationStage**.</span><span class="sxs-lookup"><span data-stu-id="a3544-158">It should have three **Field** elements: **Title**, **Division**, and **OrientationStage**.</span></span> <span data-ttu-id="a3544-159">(В созданном файле эти элементы могут быть в одной строке.</span><span class="sxs-lookup"><span data-stu-id="a3544-159">(These elements may be on a single line in this generated file.</span></span> <span data-ttu-id="a3544-160">Если это так, разделите их с помощью разрывов строк.)</span><span class="sxs-lookup"><span data-stu-id="a3544-160">If so, separate them with line breaks.)</span></span>
 
3. <span data-ttu-id="a3544-161">Не закрывайте файл, а затем в **обозревателе решений** разверните папку **Site Columns** (Столбцы сайта) и узел **Division**, а затем откройте файл elements.xml узла **Division**.</span><span class="sxs-lookup"><span data-stu-id="a3544-161">Leave the file open, and in **Solution Explorer**, expand the **Site Columns** folder and the **Division** node, and then open the elements.xml file for **Division**.</span></span> <span data-ttu-id="a3544-162">Элемент **Field** узла **Division** в файле schema.xml должен точно дублировать элемент **Field** узла **Division** в файле elements.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-162">The **Field** element for **Division** in schema.xml should exactly duplicate the **Field** element in the **Division** elements.xml.</span></span> <span data-ttu-id="a3544-163">Если совпадение не точное, скопируйте элемент **Field** из файла elements.xml в столбце сайта и вставьте его вместо элемента **Field** в файле schema.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-163">If there is not an exact match, copy the **Field** element from the site column elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file.</span></span> <span data-ttu-id="a3544-164">Закройте файл element.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-164">Close the element.xml file.</span></span>
    
4. <span data-ttu-id="a3544-165">Откройте файл elements.xml элемента **OrientationStage**.</span><span class="sxs-lookup"><span data-stu-id="a3544-165">Open the elements.xml file for **OrientationStage**.</span></span> <span data-ttu-id="a3544-166">При этом также должно быть точное совпадение элементов **Field** в двух файлах элемента **OrientationStage**, включая все дочерние элементы, например **CHOICES** (ВАРИАНТЫ) и **MAPPINGS** (СОПОСТАВЛЕНИЯ).</span><span class="sxs-lookup"><span data-stu-id="a3544-166">Here, too, there must be an exact match of the  **Field** elements in the two files for **OrientationStage**, including all child elements, such as the **CHOICES** and **MAPPINGS** elements.</span></span> <span data-ttu-id="a3544-167">Если совпадение не точное, скопируйте элемент **Field** из файла elements.xml в столбце сайта и вставьте его вместо элемента **Field** в файле schema.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-167">If there isn't, copy the **Field** in the elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file.</span></span> <span data-ttu-id="a3544-168">Закройте файл element.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-168">Close the element.xml file.</span></span>
 
5. <span data-ttu-id="a3544-169">Не закрывая файл schema.xml, в элементе **View**, значение **BaseViewID** которого равно "1", найдите дочерний элемент **ViewFields**, а затем добавьте два приведенных ниже элемента **FieldRef** в качестве его дочерних объектов.</span><span class="sxs-lookup"><span data-stu-id="a3544-169">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", find the child **ViewFields** element, and then add the following two **FieldRef** elements as children of it.</span></span> <span data-ttu-id="a3544-170">Возможно, они уже существуют, но не содержат атрибута **ID**.</span><span class="sxs-lookup"><span data-stu-id="a3544-170">They may already be there but missing an **ID** attribute.</span></span> <span data-ttu-id="a3544-171">В таком случае добавьте атрибут ID.</span><span class="sxs-lookup"><span data-stu-id="a3544-171">If so, add the ID attribute.</span></span>
    
    ```
      <FieldRef Name="Division" ID="{GUID from the Field element}" />
      <FieldRef Name="OrientationStage" ID="{GUID from the Field element}" />

    ```

6. <span data-ttu-id="a3544-172">Замените заполнители значений двух атрибутов **ID** на идентификаторы GUID из соответствующих элементов **Field** в элементе **ContentType** для типа **NewEmployee**, расположенном выше в файле schema.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-172">Replace the two placeholder **ID** attribute values with the GUIDs from the corresponding **Field** elements in the **ContentType** element for **NewEmployee** that is earlier in the schema.xml file.</span></span> <span data-ttu-id="a3544-173">Не забудьте добавить фигурные скобки: {}.</span><span class="sxs-lookup"><span data-stu-id="a3544-173">Don't forget the framing braces "{}".</span></span> <span data-ttu-id="a3544-174">Ниже показано, как должен выглядеть элемент **ViewFields** для элемента **View** с идентификатором "1" (у вас могут быть другие идентификаторы GUID).</span><span class="sxs-lookup"><span data-stu-id="a3544-174">The **ViewFields** for the "1" **View** should look like the following (your GUIDs may be different):</span></span>

    ```
      <ViewFields>
        <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
        <FieldRef Name="Division" ID="{509d2d67-9a96-4596-9b3b-58449cdcc6ff}" />
        <FieldRef Name="OrientationStage" ID="{38a3b54c-acf3-4ddf-b748-55c7c28d4cc2}" />        
      </ViewFields>
    ```

7. <span data-ttu-id="a3544-175">Не закрывая файл schema.xml, найдите элемент **View**, значение **BaseViewID** которого равно "0".</span><span class="sxs-lookup"><span data-stu-id="a3544-175">Still in the schema.xml file, find the **View** element whose **BaseViewID** value is "0".</span></span> <span data-ttu-id="a3544-176">Найдите в нем элемент **ViewFields**.</span><span class="sxs-lookup"><span data-stu-id="a3544-176">Find the **ViewFields** element within it.</span></span>

8. <span data-ttu-id="a3544-177">Скопируйте весь раздел **ViewFields** элемента View "1" и вставьте его вместо раздела **ViewFields** элемента View "0".</span><span class="sxs-lookup"><span data-stu-id="a3544-177">Copy the entire **ViewFields** section from View "1" over the **ViewFields** section of View "0".</span></span> <span data-ttu-id="a3544-178">Два представления теперь должны иметь одинаковые разделы **ViewFields**.</span><span class="sxs-lookup"><span data-stu-id="a3544-178">The two views should now have identical **ViewFields** sections.</span></span>
    
9. <span data-ttu-id="a3544-179">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="a3544-179">Save and close the schema.xml file.</span></span>

10. <span data-ttu-id="a3544-180">В папке **Lists** (Списки) разверните узел **NewEmployeeOrientation** и его дочерний экземпляр списка **NewEmployeesInSeattle**.</span><span class="sxs-lookup"><span data-stu-id="a3544-180">In the **Lists** folder, expand both the **NewEmployeeOrientation** node and its child list instance **NewEmployeesInSeattle**.</span></span> <span data-ttu-id="a3544-181">Вы должны отличить файл elements.xml шаблона от файла elements.xml экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a3544-181">You should be able to clearly see and distinguish the elements.xml for the template from the elements.xml for the instance.</span></span> <span data-ttu-id="a3544-182">Откройте файл elements.xml экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a3544-182">Open the one for the instance.</span></span> 
    
11. <span data-ttu-id="a3544-183">Добавьте два элемента **Field** в первый элемент **Row**, чтобы элемент **Row** выглядел, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a3544-183">Add two **Field** elements to the first **Row** element, so that the **Row** element looks like the following:</span></span>
    
    ``` 
    <Row>
      <Field Name="Title">Tom Higginbotham</Field>
      <Field Name="Division">Manufacturing</Field>
      <Field Name="OrientationStage">Tour of building</Field>
    </Row>
    ```

12. <span data-ttu-id="a3544-184">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="a3544-184">Save and close the file.</span></span>
    

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="a3544-185">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="a3544-185">Run and test the add-in</span></span>

1. <span data-ttu-id="a3544-p117">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="a3544-p117">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
     
2. <span data-ttu-id="a3544-188">Когда откроется страница надстройки по умолчанию, щелкните ссылку **New Employees in Seattle** (Новые сотрудники в Сиэтле), чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="a3544-188">When the add-in's default page opens, select the **New Employees in Seattle** link to open the custom list instance.</span></span>
 
3. <span data-ttu-id="a3544-189">Откроется список со столбцами **Division** и **OrientationStage**.</span><span class="sxs-lookup"><span data-stu-id="a3544-189">The list page opens and the **Division** and **OrientationStage** columns are on it.</span></span> <span data-ttu-id="a3544-190">Пользователю не обязательно добавлять их вручную, так как они являются частью типа контента списка.</span><span class="sxs-lookup"><span data-stu-id="a3544-190">It is not necessary for a user to add them manually because they are part of the list's content type.</span></span> <span data-ttu-id="a3544-191">Верхний элемент содержит добавленные вами данные.</span><span class="sxs-lookup"><span data-stu-id="a3544-191">The top item has the data you added.</span></span>
    
    <span data-ttu-id="a3544-192">*Рис. 4. Список "Новые сотрудники в Сиэтле"*</span><span class="sxs-lookup"><span data-stu-id="a3544-192">*Figure 4. New Employees in Seattle list*</span></span>

    ![Список новых сотрудников в Сиэтле с готовыми столбцами "Подразделение" и "Этап адаптации".](../images/b654af45-663e-425c-b7c7-b8b5524cb316.PNG) 
 
4. <span data-ttu-id="a3544-194">Попробуйте добавлять к списку новые элементы и редактировать существующие.</span><span class="sxs-lookup"><span data-stu-id="a3544-194">Try adding new items to the list and editing existing items.</span></span>
    
5. <span data-ttu-id="a3544-195">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3544-195">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="a3544-196">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать последнюю.</span><span class="sxs-lookup"><span data-stu-id="a3544-196">Each time that you select F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
6. <span data-ttu-id="a3544-197">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуется отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="a3544-197">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="a3544-198">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="a3544-198">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3544-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3544-199">Next steps</span></span>
<span data-ttu-id="a3544-200"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="a3544-200"></span></span>

<span data-ttu-id="a3544-201">В следующей статье этой серии описано, как [добавить веб-часть на страницу в надстройке SharePoint, размещаемой в SharePoint](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="a3544-201">In the next article in this series, you'll [add a Web Part to a page in a SharePoint-hosted SharePoint Add-in](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
