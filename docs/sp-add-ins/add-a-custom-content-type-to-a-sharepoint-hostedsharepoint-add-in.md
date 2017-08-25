# <a name="add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="3d370-101">Добавление пользовательского типа контента в надстройку, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d370-101">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="3d370-102">В этой статье рассказывается, как добавлять пользовательские типы контента в надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d370-102">Learn how to include custom content types in an SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="3d370-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="3d370-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="3d370-p102">Эта четвертая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и другими статьями из этой серии:</span><span class="sxs-lookup"><span data-stu-id="3d370-p102">Get a quick introduction to some of the major classes in the SharePoint object model. This is the fourth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="3d370-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d370-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="3d370-109">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d370-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
    
 
-  [<span data-ttu-id="3d370-110">Добавление настраиваемых столбцов в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d370-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
    
 

 <span data-ttu-id="3d370-p103">**Примечание.** Если вы уже изучали предыдущие статьи серии о надстройках с размещением в SharePoint, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей. Вы также можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeContentType.sln.</span><span class="sxs-lookup"><span data-stu-id="3d370-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>
 

<span data-ttu-id="3d370-113">В этой статье описывается добавление пользовательского типа контента в надстройку "Обучение сотрудников".</span><span class="sxs-lookup"><span data-stu-id="3d370-113">In this article you add a custom content type to the Employee Orientation SharePoint Add-in.</span></span>
 

## <a name="create-the-custom-content-type"></a><span data-ttu-id="3d370-114">Создание пользовательского типа контента</span><span class="sxs-lookup"><span data-stu-id="3d370-114">Create a custom content type</span></span>

1. <span data-ttu-id="3d370-p104">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**. Задайте для папки имя "Столбцы сайта".</span><span class="sxs-lookup"><span data-stu-id="3d370-p104">In  **Solution Explorer**, right-click the project and choose  **Add** > **New Folder**. Name the folder Content Types.</span></span>
    
 
2. <span data-ttu-id="3d370-p105">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Создать элемент**. Откроется диалоговое окно **Добавление нового элемента** для узла **BeforeContentType**.</span><span class="sxs-lookup"><span data-stu-id="3d370-p105">Right-click the new folder and choose  **Add** > **New Item**. The  **Add New Item** dialog box opens to the **Office/SharePoint** node..</span></span>
    
 
3. <span data-ttu-id="3d370-p106">Выберите **Тип контента** и задайте для него имя NewEmployee, а затем нажмите **Добавить**. Когда мастер предложит выбрать базовый тип содержимого, выберите **Элемент**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3d370-p106">Choose  **Content Type** and give it the nameNewEmployee, and then choose  **Add**. When prompted by the wizard to select the base content type, choose  **Item**, and then choose  **Finish**.</span></span>
    
 
4. <span data-ttu-id="3d370-121">Если конструктор типа контента не откроется автоматически, выберите тип контента **NewEmployee** в **обозревателе решений**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="3d370-121">If the content type designer does not automatically open, choose the **ActingRole** content type in **Solution Explorer** to open it.</span></span>
    
 
5. <span data-ttu-id="3d370-122">Откройте вкладку **Тип контента** в конструкторе и заполните текстовые поля следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3d370-122">Open the **Content Type** tab in the designer and fill the text boxes as follows:</span></span>
    
      -  <span data-ttu-id="3d370-123">**Имя типа контента**: NewEmployee</span><span class="sxs-lookup"><span data-stu-id="3d370-123">**Content Type Name**: NewEmployee</span></span>
    
 
  -  <span data-ttu-id="3d370-124">**Описание**: "Представляет нового сотрудника".</span><span class="sxs-lookup"><span data-stu-id="3d370-124">**Description**: Represents a new employee.</span></span>
    
 
  -  <span data-ttu-id="3d370-125">**Имя группы**: "Обучение сотрудников"</span><span class="sxs-lookup"><span data-stu-id="3d370-125">**Group Name**: Employee Orientation</span></span>
    
 
6. <span data-ttu-id="3d370-p107">Убедитесь, что *ни один* из флажков на вкладке не установлен. Флажок **Наследует столбцы родительского типа содержимого** может быть установлен по умолчанию. *Обязательно снимите его.* Теперь вкладка должна выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="3d370-p107">Verify that  *none*  of the check boxes on the tab are selected. The check box for **Inherits the columns from the parent Content Type** may be selected by default. *Be sure to clear it.*</span></span>
    
    <span data-ttu-id="3d370-130">**Вкладка "Тип контента"**</span><span class="sxs-lookup"><span data-stu-id="3d370-130">**Content Type Tab**</span></span>

  ![Конструктор типов контента, в котором отображаются имя типа NewEmployee, описание "Представляет нового сотрудника" и группа "Обучение сотрудников".](../../images/8a9768f4-315d-45c0-88d7-687dbf84495c.PNG)
 
 
7. <span data-ttu-id="3d370-132">Откройте вкладку **Столбцы** конструктора.</span><span class="sxs-lookup"><span data-stu-id="3d370-132">Open the **Columns** tab in the designer.</span></span>
     
8. <span data-ttu-id="3d370-p108">В таблице нажмите надпись **Щелкните, чтобы добавить столбец**, чтобы открыть раскрывающийся список столбцов, и добавьте столбец **Division**. В раскрывающемся списке он обозначен отображаемым именем: **Подразделение**. Повторите эти действия для столбца **Этап обучения**. Если эти столбцы не отображаются, возможно, вы начали не с того решения Visual Studio. Начните с файла BeforeContentType.sln. По завершении таблица должна выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="3d370-p108">In the gird, choose  **Click here to add a column** to open a drop down list of columns, and add the **Division** column. It is listed in the drop-down list by its display name: **Division**. Do the same for the  **Orientation Stage** column. (If they are not listed, you may not have started with the correct Visual Studio solution. Start with BeforeContentType.sln.) When your are finished the grid should look like the following:</span></span>
    
    <span data-ttu-id="3d370-138">**Вкладка "Столбцы"**</span><span class="sxs-lookup"><span data-stu-id="3d370-138">**Columns Tab**</span></span>

    ![Вкладка "Столбцы" конструктора типов контента со столбцами "Сотрудник", "Подразделение" и "Этап адаптации" в таблице.](../../images/835e78b3-a073-45b2-b4ee-3f9be9d88495.PNG)
 
 
9. <span data-ttu-id="3d370-140">Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="3d370-140">Save the file and close the designer.</span></span>
    
 
10. <span data-ttu-id="3d370-141">На следующем этапе вам потребуется работать непосредственно с необработанным кодом XML типа контента, поэтому в **обозревателе решений** необходимо выбрать дочерний файл elements.xml типа контента **NewEmployee**.</span><span class="sxs-lookup"><span data-stu-id="3d370-141">The next step requires that you work directly in the raw XML for the content type, so in **Solution Explorer**, choose the elements.xml file child of the **ActingRole** content type.</span></span>
    
 
11. <span data-ttu-id="3d370-p109">Для двух добавленных вами столбцов в файле уже есть элементы **FieldRef**. Добавьте аналогичные им элементы **FieldRef** для двух встроенных столбцов SharePoint. Ниже представлена маркировка элементов. *Для атрибута ID необходимо использовать те же идентификаторы GUID, так как это встроенные типы полей с фиксированными идентификаторами.* Добавьте их *над* двумя имеющимися элементами **FieldRef** для настраиваемых столбцов сайтов.</span><span class="sxs-lookup"><span data-stu-id="3d370-p109">There are already **FieldRef** elements in the file for the two columns that you added. Add **FieldRef** elements for two built-in SharePoint 2013 columns as peers of the two that are already there. The following is the markup for the elements. *You must use these same GUIDs for the ID attribute because these are built-in field types with fixed IDs.*  Add these *above*  the two **FieldRef** elements for the custom site columns.</span></span>
    
```
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
<FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
```


    Note that we have given these fields a custom display name:  **Employee**.
    
 
12. <span data-ttu-id="3d370-147">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3d370-147">Save and close the file.</span></span>
    
 
13. <span data-ttu-id="3d370-148">Разверните узел **Списки** в **обозревателе решений** и выберите список **NewEmployeeOrientation**, чтобы открыть конструктора типа списка.</span><span class="sxs-lookup"><span data-stu-id="3d370-148">Expand the  **Lists** node in **Solution Explorer** and choose **NewEmployeeOrientation** to open the list type designer.</span></span>
    
 
14. <span data-ttu-id="3d370-149">Откройте вкладку **Столбцы** конструктора и нажмите кнопку **Типы контента**.</span><span class="sxs-lookup"><span data-stu-id="3d370-149">Open the **Columns** tab in the designer, and then choose the **Content Types** button.</span></span>
    
 
15. <span data-ttu-id="3d370-150">В диалоговом окне **Параметры типа содержимого** добавьте тип контента **NewEmployee**.</span><span class="sxs-lookup"><span data-stu-id="3d370-150">In the **Content Type Settings** dialog, add the **ActingRole** content type.</span></span>
    
 
16. <span data-ttu-id="3d370-151">Выберите тип контента **NewEmployee** в списке типов контента, а затем нажмите кнопку **По умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="3d370-151">Choose the **ActingRole** content type in the list of types, and choose the **Set as Default** button.</span></span>
    
 
17. <span data-ttu-id="3d370-152">Выберите тип контента **Элемент**, щелкните правой кнопкой мыши маленькую стрелку слева от имени типа контента и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3d370-152">Choose the **Item** content type, right-click the small arrowhead that appears to the left of the content type name, and then choose **Delete**.</span></span>
    
 
18. <span data-ttu-id="3d370-p110">Повторите предыдущий этап для типа контента **Папка**, чтобы в списке остался только тип контента **ActingRole**. Теперь диалоговое окно должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="3d370-p110">Repeat the preceding step for the  **Folder** content type, so **NewEmployee** is the only content type listed. The dialog box should now look like the following:</span></span>
    
    <span data-ttu-id="3d370-155">**Диалоговое окно "Параметры типа содержимого"**</span><span class="sxs-lookup"><span data-stu-id="3d370-155">The Choose Content Type Settings dialog box appears.</span></span>

    ![Диалоговое окно параметров типа содержимого с одним типом контента — NewEmployee.](../../images/b90699f4-40de-4f50-ad47-3e8773d0eb92.PNG)
 
19.  <span data-ttu-id="3d370-157">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3d370-157">Choose **OK** to close the dialog box, and then save and close the file.</span></span>
    
20. <span data-ttu-id="3d370-158">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="3d370-158">Open the schema.xml file.</span></span>
    
21. <span data-ttu-id="3d370-p111">Найдите элемент **Fields**. Он должен включать три элемента **Field**: **Title**, Division и OrientationStage. Эти элементы могут находиться в одной строке файла. Если это так, разделите их разрывами строки.</span><span class="sxs-lookup"><span data-stu-id="3d370-p111">Find the  **Fields** element. It should have three **Field** elements: **Title**, Division, and OrientationStage. (These elements may be on a single line in this generated file. If so, separate them with line breaks.)</span></span>
 
22. <span data-ttu-id="3d370-p112">Оставьте файл открытым и в **обозревателе решений** разверните папку **Столбцы сайта** и узел Division, а затем откройте файл elements.xml для этого столбца. Элемент **Field** для столбца Division в файле schema.xml должен в точности совпадать с элементом **Field** в файле elements.xml столбца Division. Если между ними нет точного совпадения, скопируйте элемент **Field** из файла elements.xml столбца сайта и вставьте его вместо несоответствующего элемента **Field** в файле schema.xml. Затем закройте файл element.xml.</span><span class="sxs-lookup"><span data-stu-id="3d370-p112">Leave the file open and in  **Solution Explorer**, expand the  **Site Columns** folder and theDivision node, and then open the elements.xml file forDivision. The  **Field** element forDivision in schema.xml should exactly duplicate the **Field** element in theDivision elements.xml. If there is not an exact match, copy the **Field** element from the site column elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file. Then close the element.xml file.</span></span>
    
23. <span data-ttu-id="3d370-p113">Откройте файл elements.xml для столбца OrientationStage. В этом случае элементы **Field** в двух файлах для столбца OrientationStage тоже должны полностью совпадать (включая все дочерние элементы, например **CHOICES** и **MAPPINGS**). Если они не совпадают, скопируйте элемент **Field** из файла elements.xml и вставьте его вместо несоответствующего элемента **Field** в файле schema.xml. Затем закройте файл element.xml.</span><span class="sxs-lookup"><span data-stu-id="3d370-p113">Open the elements.xml file for OrientationStage. Here, too, there must be an exact match of the  **Field** elements in the two files forOrientationStage, including all child elements, such as the  **CHOICES** and **MAPPINGS** elements. If there isn't, copy the **Field** in the elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file. Then close the element.xml file.</span></span>
 
24. <span data-ttu-id="3d370-p114">Не закрывая файл schema.xml, в элементе **View**, значение **BaseViewID** которого равно "1", найдите дочерний элемент **ViewFields**, а затем добавьте два приведенных ниже элемента **FieldRef** в качестве его дочерних объектов. Возможно, они уже существуют, но не содержат атрибута **ID**. В таком случае добавьте атрибут ID.</span><span class="sxs-lookup"><span data-stu-id="3d370-p114">Still in the schema.xml file, in the  **View** element whose **BaseViewID** value is "1", find the child **ViewFields** element and then add the following two **FieldRef** elements as children of it. They may already be there, but missing an **ID** attribute. If so, add the ID attribute.</span></span>
    
```
  <FieldRef Name="Division" ID="{GUID from the Field element}" />
<FieldRef Name="OrientationStage" ID="{GUID from the Field element}" />

```

25. <span data-ttu-id="3d370-p115">Замените заполнители значений двух атрибутов **ID** на идентификаторы GUID из соответствующих элементов **Field** в элементе **ContentType** для типа **NewEmployee**, расположенном выше в файле schema.xml. Не забудьте добавить фигурные скобки: {}.</span><span class="sxs-lookup"><span data-stu-id="3d370-p115">Replace the two placeholder  **ID** attribute values with the GUIDs from the corresponding **Field** elements in the **ContentType** element for **NewEmployee** that is earlier in the schema.xml file. Don't forget the framing braces "{}".</span></span>
    
    <span data-ttu-id="3d370-p116">Ниже показано, как должен выглядеть элемент **ViewFields** для элемента **View** с идентификатором "1" (у вас могут быть другие идентификаторы GUID).</span><span class="sxs-lookup"><span data-stu-id="3d370-p116">The  **ViewFields** for the "1" **View** should look like this. (Your GUIDs may be different.)</span></span>
    


```
  <ViewFields>
   <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
   <FieldRef Name="Division" ID="{509d2d67-9a96-4596-9b3b-58449cdcc6ff}" />
   <FieldRef Name="OrientationStage" ID="{38a3b54c-acf3-4ddf-b748-55c7c28d4cc2}" />        
</ViewFields>
```

26. <span data-ttu-id="3d370-p117">Не закрывая файл schema.xml, найдите элемент **View**, значение **BaseViewID** которого равно "0". Найдите в нем элемент **ViewFields**.</span><span class="sxs-lookup"><span data-stu-id="3d370-p117">Still in the schema.xml file, find the  **View** element whose **BaseViewID** value is "0". find the **ViewFields** element with in it.</span></span>
    
 
27. <span data-ttu-id="3d370-p118">Полностью скопируйте раздел **ViewFields** из элемента View с идентификатором "1" в раздел **ViewFields** элемента View с идентификатором "0". Разделы **ViewFields** этих двух представлений не должны быть идентичными.</span><span class="sxs-lookup"><span data-stu-id="3d370-p118">Copy the whole of the  **ViewFields** section from View "1" over the **ViewFields** section of View "0". The two views should now have identical **ViewFields** sections.</span></span>
    
 
28. <span data-ttu-id="3d370-182">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="3d370-182">Save and close the schema.xml file.</span></span>
    
 
29. <span data-ttu-id="3d370-p119">В папке **Списки** разверните узел **NewEmployeeOrientation** и его дочерний экземпляр списка **NewEmployeesInSeattle**. Разница между файлами elements.xml для шаблона и экземпляра должна быть очевидна. Откройте файл для экземпляра.</span><span class="sxs-lookup"><span data-stu-id="3d370-p119">In the  **Lists** folder, expand both the **NewEmployeeOrientation** node and its child list instance **NewEmployeesInSeattle**. You should be able to clearly see and distinguish the elements.xml for the template from the elements.xml for the instance. Open the one for the instance.</span></span> 
    
 
30. <span data-ttu-id="3d370-186">Добавьте два элемента **Field** в первый элемент **Row**, чтобы элемент **Row** выглядел, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3d370-186">Add two  **Field** elements to the first **Row** element, so that the **Row** element looks like the following.</span></span>
    
```
  
<Row>
  <Field Name="Title">Tom Higginbotham</Field>
  <Field Name="Division">Manufacturing</Field>
  <Field Name="OrientationStage">Tour of building</Field>
</Row>
   
```

31. <span data-ttu-id="3d370-187">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3d370-187">Save and close the file.</span></span>
    
 

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="3d370-188">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="3d370-188">Run and test the add-in</span></span>

1. <span data-ttu-id="3d370-p120">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="3d370-p120">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
     
2. <span data-ttu-id="3d370-191">Когда откроется страница надстройки, используемая по умолчанию, щелкните ссылку **Новые сотрудники в Москве**, чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="3d370-191">When the add-in's default page opens, choose the **New Employees in Seattle** link to open the custom list instance.</span></span>
 
3. <span data-ttu-id="3d370-p121">Откроется страница списка со столбцами Division и OrientationStage. Пользователю необязательно добавлять их вручную, так как они входят в состав типа контента списка. Верхний элемент содержит добавленные вами данные.</span><span class="sxs-lookup"><span data-stu-id="3d370-p121">The list page opens and the Division andOrientationStage columns are on it. It is not necessary for a user to add them manually because they are part of the list's content type. The top item has the data you added.</span></span>
    
    <span data-ttu-id="3d370-195">**Список "Новые сотрудники в Москве"**</span><span class="sxs-lookup"><span data-stu-id="3d370-195">**New Employees in Seattle**</span></span>

    ![Список новых сотрудников в Москве с готовыми столбцами "Подразделение" и "Этап адаптации".](../../images/b654af45-663e-425c-b7c7-b8b5524cb316.PNG) 
 
4. <span data-ttu-id="3d370-197">Попробуйте добавлять к списку новые элементы и редактировать существующие.</span><span class="sxs-lookup"><span data-stu-id="3d370-197">Try adding new items to the list and editing existing items.</span></span>
    
 
5. <span data-ttu-id="3d370-p122">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="3d370-p122">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
6. <span data-ttu-id="3d370-p123">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="3d370-p123">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>

## 
<span data-ttu-id="3d370-202"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="3d370-202"></span></span>

<span data-ttu-id="3d370-203">В следующей статье этой серии описывается добавление веб-части представления списка на страницу по умолчанию для надстройки SharePoint: [Добавление веб-части на страницу в надстройке, размещенной в SharePoint](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="3d370-203">In the next article in this series, you'll add a list view Web Part to the default page of the SharePoint Add-in:  [Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in).</span></span>
