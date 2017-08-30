
# <a name="programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in"></a><span data-ttu-id="cf6af-101">Программное развертывание настраиваемой кнопки в надстройке, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-101">Programmatically deploy a custom button in the provider-hosted add-in</span></span>
<span data-ttu-id="cf6af-102">Узнайте, как программным путем зарегистрировать настраиваемую кнопку ленты с настраиваемым списком в одной надстройке SharePoint, размещенной у поставщика.</span><span class="sxs-lookup"><span data-stu-id="cf6af-102">Learn how to programmatically register a custom ribbon button with a custom list in the same provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="cf6af-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="cf6af-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="cf6af-p102">Это девятая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p102">Add custom ribbon button commands to the host web of a SharePoint Add-in. This is the ninth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="cf6af-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="cf6af-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [<span data-ttu-id="cf6af-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="cf6af-111">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="cf6af-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [<span data-ttu-id="cf6af-112">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-112">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="cf6af-113">Добавление веб-части надстройки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-113">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="cf6af-114">Обработка событий надстройки, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-114">Handle add-in events in the provider-hosted add-in</span></span>](handle-add-in-events-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="cf6af-115">Добавление логики, выполняемой при первом запуске, в надстройку, размещаемую у поставщика</span><span class="sxs-lookup"><span data-stu-id="cf6af-115">Add first-run logic to the provider-hosted add-in</span></span>](add-first-run-logic-to-the-provider-hosted-add-in)
    
 

 <span data-ttu-id="cf6af-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeProgrammaticButton.sln.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeProgrammaticButton.sln file.</span></span>
 

<span data-ttu-id="cf6af-118">Из данной статьи вы узнаете, как включать настраиваемую кнопку ленты в Надстройка SharePoint, когда список, лента которого получает кнопку, также развертывается программным способом в той же самой надстройке.</span><span class="sxs-lookup"><span data-stu-id="cf6af-118">In this article you will learn how to include a custom ribbon button in the a SharePoint Add-in when the list whose ribbon gets the button is itself being programmatically deployed in the very same add-in.</span></span>
 

## <a name="re-add-the-custom-button-to-the-project"></a><span data-ttu-id="cf6af-119">Повторное добавление настраиваемой кнопки в проект</span><span class="sxs-lookup"><span data-stu-id="cf6af-119">Re-add the custom button to the project</span></span>


 <span data-ttu-id="cf6af-p104">**Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений** и выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p104">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
 

<span data-ttu-id="cf6af-p105">В предыдущей статье описывалось удаление настраиваемой кнопки ленты **AddEmployeeToCorpDB** из проекта. Чтобы добавить ее обратно, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p105">In the previous article you removed the custom **AddEmployeeToCorpDB** ribbon button from the project. Add it back in with these steps below.</span></span>
 

 

1. <span data-ttu-id="cf6af-125">Откройте **обозреватель решений** и на небольшой панели инструментов в верхней его части нажмите кнопку **Показать все файлы**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-125">In **Solution Explorer**, press the **Show All Files** button on the small toolbar at the top of **Solution Explorer**.</span></span>
    
  ![Панель инструментов обозревателя решений с рамкой вокруг кнопки "Показать все файлы".](../../images/f6b035f5-1aa7-452a-8f59-9dd44b062d06.PNG)
 

 

 
2. <span data-ttu-id="cf6af-127">В проекте **ChainStore** щелкните правой кнопкой мыши элемент **AddEmployeeToCorpDB** и выберите пункт **Включить в проект**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-127">In the **ChainStore** project, right-click **AddEmployeeToCorpDB** and select **Include in Project**.</span></span>
    
 
3. <span data-ttu-id="cf6af-128">Еще раз нажмите кнопку **Показать все файлы**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-128">Press the **Show All Files** button again.</span></span>
    
 
4. <span data-ttu-id="cf6af-129">В проекте **ChainStore** разверните узел **AddEmployeeToCorpDB**, а затем откройте файл elements.xml.</span><span class="sxs-lookup"><span data-stu-id="cf6af-129">In the **ChainStore** project, expand **AddEmployeeToCorpDB** and then open the elements.xml file.</span></span>
    
 

## <a name="understand-a-dilemma-and-its-solution"></a><span data-ttu-id="cf6af-130">Описание проблемы и ее решение</span><span class="sxs-lookup"><span data-stu-id="cf6af-130">Understand a dilemma and its solution</span></span>

<span data-ttu-id="cf6af-p106">В файле elements.xml атрибут **RegistrationId** элемента **CustomAction** служит для идентификации списка, на ленту которого добавляется кнопка: `{$ListId:Lists/Local Employees;}`. Этого было достаточно, когда список уже был добавлен на хост-сайт вручную. Но теперь, когда список развертывается с помощью кода, выполняемого при первом запуске, SharePoint устанавливает надстройку и пытается развернуть кнопку, но списка еще не существует. В этом случае установка надстройки может привести к возникновению исключения и завершиться со сбоем.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p106">In the elements.xml file, the **RegistrationId** attribute of the **CustomAction** element identifies the list on whose ribbon the button is added: `{$ListId:Lists/Local Employees;}`. This worked fine when the list had already been added to the host web manually. But now that we are deploying the list programmatically in first-run logic, the list doesn't exist when SharePoint installs the add-in and tries to deploy the button. The installation of the add-in would throw an exception and fail.</span></span>
 

 
<span data-ttu-id="cf6af-135">Развертывание списка в обработчике событий установки, а не в коде, выполняемом при первом запуске, не решит эту проблему. Это связано с тем, что SharePoint развертывает описанные настраиваемые компоненты, например настраиваемую кнопку (и веб-часть надстройки **Размещение заказа**), *перед тем как* запустить настраиваемый обработчик, поэтому когда SharePoint пытается развернуть кнопку, списка еще не существует.</span><span class="sxs-lookup"><span data-stu-id="cf6af-135">Deploying the list in the installation event handler, instead of first-run logic, won't solve the dilemma because SharePoint deploys custom descriptively-defined components, such as the custom button (and the **Place Order** add-in part), *before*  it runs the custom handler, so the list won't exist when SharePoint tries to deploy the button.</span></span>
 

 
<span data-ttu-id="cf6af-p107">Создание настраиваемой кнопки полностью программным способом непрактично по причинам, которые слишком сложны, чтобы обсуждать их здесь. К счастью, это не нужно. Существует относительно безболезненный способ полупрограммного создания настраиваемой кнопки и назначения ее настраиваемому списку. Ниже перечислены необходимые для этого основные действия.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p107">Creating a custom button entirely programmatically is not practical for reasons that are too advanced to discuss here. Fortunately, it is not necessary. There is a relatively painless way to semi-programmatically create a custom button and assign it to a custom list. The following are the basic steps:</span></span>
 

 

1. <span data-ttu-id="cf6af-140">Оставьте описательно определенную кнопку в проекте, но назначьте ее ленте какого-либо приложения, которое всегда имеется на сайтах SharePoint, а не ленте списка, который развертывается программным способом с помощью той же надстройки.</span><span class="sxs-lookup"><span data-stu-id="cf6af-140">Keep the descriptively defined button in the project, but assign it to the ribbon of something that always exists on SharePoint sites, instead of to a list that's programmatically deployed with the same add-in.</span></span> 
    
 
2. <span data-ttu-id="cf6af-141">В коде, выполняемом при первом запуске, после программного создания списка добавьте неопределенную кнопку на ленту списка.</span><span class="sxs-lookup"><span data-stu-id="cf6af-141">In the first-run logic, after the list is programmatically created, programmatically add an undefined button to the ribbon of the list.</span></span>
    
 
3. <span data-ttu-id="cf6af-p108">Инициализируйте свойства новой кнопки, используя значения свойств исходной кнопки. Итак, на данный момент у нас имеются две идентичные кнопки. Вторая кнопка назначена ленте списка **Местные сотрудники**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p108">Initialize the properties of the new button with the values of the original button. At this point there are two identical buttons. The second of them is assigned to the ribbon of the **Local Employees** list.</span></span>
    
 
4. <span data-ttu-id="cf6af-145">Удалите исходную кнопку программным способом.</span><span class="sxs-lookup"><span data-stu-id="cf6af-145">Programmatically delete the original button.</span></span>
    
 

## <a name="programmatically-register-the-custom-button"></a><span data-ttu-id="cf6af-146">Регистрация настраиваемой кнопки программным способом</span><span class="sxs-lookup"><span data-stu-id="cf6af-146">Programmatically register the custom button</span></span>

<span data-ttu-id="cf6af-147">Ниже описывается реализация этой стратегии.</span><span class="sxs-lookup"><span data-stu-id="cf6af-147">The following procedure shows how to implement this strategy.</span></span>
 

 

1. <span data-ttu-id="cf6af-p109">В проекте **ChainStore** разверните узел **AddEmployeeToCorpDB**, откройте файл elements.xml, а затем измените значение атрибута **RegistrationId** элемента **CustomAction** на "100". Это идентификатор типа списка. Даже если на веб-сайте нет экземпляров списков этого типа, сам *тип* списка имеется на всех веб-сайтах SharePoint. Теперь атрибут должен выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p109">In the **ChainStore** project, expand **AddEmployeeToCorpDB** and then open the elements.xml file, and then change the value of the **RegistrationId** attribute of the **CustomAction** element to "100". This is the ID of a type of list. Even if there are no instances of lists of this type on the website, the list *type* is on every SharePoint website. The attribute should now look like the following.</span></span>
    
```XML
  RegistrationId="100"
```

2. <span data-ttu-id="cf6af-p110">В файле SharePointComponentDeployer.cs добавьте указанную ниже строку в метод  `DeployChainStoreComponentsToHostWeb` сразу же после строки, в которой вызывается метод `CreateLocalEmployeesList`. Вы создадите этот метод на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p110">In the file SharePointComponentDeployer.cs, add the following line to the  `DeployChainStoreComponentsToHostWeb` method, just below the line that calls `CreateLocalEmployeesList`. You will create this method in the next step.</span></span>
    
```C#
  ChangeCustomActionRegistration();
```

3. <span data-ttu-id="cf6af-p111">Добавьте приведенный ниже метод в класс `SharePointComponentDeployer`. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p111">Add the following method to the  `SharePointComponentDeployer` class. Note the following about this code:</span></span>
    
      - <span data-ttu-id="cf6af-p112">Так как дополнительное действие, то есть настраиваемая кнопка, было зарегистрировано на ленте для  *типа*  списка, область его действия распространяется на весь веб-сайт и находится в коллекции дополнительных действий веб-сайта. Таким образом, код получает его из этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p112">Because the custom action; that is, the custom button; was registered with the ribbon of a list  *type*  , it is scoped to the entire website and is in the website's collection of custom actions. So the code retrieves it from that collection.</span></span>
    
 
  - <span data-ttu-id="cf6af-158">Значение свойства `action.Name` поступает из атрибута **ID** элемента **CustomAction** в файле element.xml из узла **AddEmployeeToCorpDB**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-158">The value of the  `action.Name` comes from the **ID** attribute of the **CustomAction** element in the element.xml file in **AddEmployeeToCorpDB**.</span></span>
    
     <span data-ttu-id="cf6af-p113">**Важно!****Вам необходимо изменить значение `action.Name` в коде ниже, чтобы оно совпадало со значением в файле elements.xml.** Часть имени с идентификатором GUID будет другой. Обратите внимание, что GUID отделен точкой от остальной части имени. Ниже приведен пример строки. `where action.Name == "4a926a42-3577-4e02-9d06-fef78586b1bc.AddEmployeeToCorpDB"`</span><span class="sxs-lookup"><span data-stu-id="cf6af-p113">**Important**   **You must change the  `action.Name` value in the code below to match the value in your elements.xml file.** The GUID part of the name will be different. Note that there is a "." character between the GUID and the rest of the name. The following is an example of the line.</span></span>

```C#
  private static void ChangeCustomActionRegistration()
{
    using (var clientContext = sPContext.CreateUserClientContextForSPHost())
    {
         var query = from action in clientContext.Web.UserCustomActions
                     where action.Name == "{button_GUID} .AddEmployeeToCorpDB"
                     select action;
          IEnumerable<UserCustomAction> matchingActions = clientContext.LoadQuery(query);          
             clientContext.ExecuteQuery();
    
          UserCustomAction webScopedEmployeeAction = matchingActions.Single();

         // TODO8: Get a reference to the (empty) collection of custom actions 
         // that are registered with the custom list.

         // TODO9: Add a blank custom action to the list's collection.

         // TODO10: Copy property values from the descriptively deployed
         // custom action to the new custom action

        // TODO11: Delete the original custom action.         

          clientContext.ExecuteQuery();
    }
}
```

4. <span data-ttu-id="cf6af-163">Замените строку `TODO8` на приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="cf6af-163">Replace  `TODO8` with the following code.</span></span>
    
    <span data-ttu-id="cf6af-p114">Обратите внимание, что если вы отзовете надстройку, созданные ею компоненты не будут удалены. По завершении работы кода, выполняемого при первом запуске, в коллекции **UserCustomActions** списка появится дополнительное действие, которое не будет отозвано при следующем нажатии клавиши F5. Во избежание путаницы в последней строке этого кода метод `listActions.Clear();` очищает коллекцию.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p114">Note that when you retract an add-in, components created by the add-in are not removed. After your first-run logic executes, there will be a custom action in the list's **UserCustomActions** collection, and it will not be retracted the next time you press F5. To avoid confusion, the last line in this code `listActions.Clear();` empties the collection.</span></span>
    


```C#
  var queryForList = from list in clientContext.Web.Lists
                   where list.Title == "Local Employees"
                   select list;
IEnumerable<List> matchingLists = clientContext.LoadQuery(queryForList);
clientContext.ExecuteQuery();

List employeeList = matchingLists.First();
var listActions = employeeList.UserCustomActions;
clientContext.Load(listActions);
listActions.Clear();
```

5. <span data-ttu-id="cf6af-167">Замените строку `TODO9` на приведенную ниже строку. В список **Местные сотрудники** будет добавлено неопределенное дополнительное действие.</span><span class="sxs-lookup"><span data-stu-id="cf6af-167">Replace  `TODO9` with the following line, which adds an undefined custom action to the **Local Employees** list.</span></span>
    
```C#
  var listScopedEmployeeAction = listActions.Add();
```

6. <span data-ttu-id="cf6af-p115">Замените строку `TODO10` на приведенный ниже код. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p115">Replace  `TODO10` with the following code. Note the following about this code:</span></span>
    
      - <span data-ttu-id="cf6af-170">Он назначает значения свойств кнопки уровня веб-сайта (которая была развернута с помощью описательной разметки) соответствующим свойствам кнопки уровня списка, так что эти две кнопки становятся идентичными за исключением области их действия.</span><span class="sxs-lookup"><span data-stu-id="cf6af-170">It assigns the property values of the web-scoped button (that was deployed with descriptive markup) to the corresponding properties of the list-scoped button, so the two buttons are identical except in scope.</span></span>
    
 
  - <span data-ttu-id="cf6af-p116">Свойство **Sequence** указывает относительное положение кнопки в соответствующей области на ленте. В данном случае кнопка находится в разделе **Действия** на вкладке **Элементы** ленты. В описательной части кода это значение составляло 10001. Это достаточно большое значение, чтобы кнопка отображалась после (справа от) всех встроенных кнопок, которые SharePoint помещает в раздел **Действия**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p116">The **Sequence** property specifies the relative order that the button will appear in its area of the ribbon. In this case, the button is on the **Actions** section of the **Items** tab of the ribbon. In the descriptive markup this value was set to 10001 which is high enough to ensure that it will appear after (that is, to the right of) any in-the-box buttons that SharePoint itself puts in the **Actions** section of the ribbon.</span></span>
    
 

```C#
  listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
listScopedEmployeeAction.Update();
```

7. <span data-ttu-id="cf6af-p117">Замените  `TODO11` указанной ниже строкой, в которой выполняется удаление исходной описательным способом определенной кнопки. Если бы у нас не было этой строки, то на каждом списке на веб-сайте, для которого используется шаблон списка 100, была бы настраиваемая кнопка. Так как функциональность кнопки тесно связана со списком **Local Employees** (Местные сотрудники), то нет никакого смысла размещать эту кнопку в других списках. Кроме того, без этой строки кнопка будет *дважды*  размещена в списке **Local Employees** (Местные сотрудники), так как для этого списка используется шаблон 100.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p117">Replace  `TODO11` with the following line, which deletes the original descriptively-defined button. If we did not have this line, every list on the website that uses list template "100" would have the custom button on it. Since the button's functionality is closely tied to the **Local Employees** list, it would make no sense to have the button on any other list. Also, without this line, the button would appear *twice*  on the **Local Employees** list, because that list uses template "100".</span></span>
    
```C#
  webScopedEmployeeAction.DeleteObject();
```


    The entire method should now look like the following (except there should be a GUID in place of the placeholder).
    


```C#
  private static void ChangeCustomActionRegistration()
{
    using (var clientContext = SPContext.CreateUserClientContextForSPHost())
    {
         var query = from action in clientContext.Web.UserCustomActions
                     where action.Name == "{button_GUID} .AddEmployeeToCorpDB"
                     select action;
          IEnumerable<UserCustomAction> matchingActions = clientContext.LoadQuery(query);          
             clientContext.ExecuteQuery();
    
          UserCustomAction webScopedEmployeeAction = matchingActions.Single();

         var queryForList = from list in clientContext.Web.Lists
                            where list.Title == "Local Employees"
                            select list;
         IEnumerable<List> matchingLists = clientContext.LoadQuery(queryForList);
         clientContext.ExecuteQuery();

        List employeeList = matchingLists.First();
        var listActions = employeeList.UserCustomActions;
        clientContext.Load(listActions);
        listActions.Clear();

        var listScopedEmployeeAction = listActions.Add();

        listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
        listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
        listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
        listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
        listScopedEmployeeAction.Update();

        webScopedEmployeeAction.DeleteObject();         

        clientContext.ExecuteQuery();
    }
}
```


## <a name="request-full-control-of-the-host-web"></a><span data-ttu-id="cf6af-178">Запрос полного доступа к хост-сайту</span><span class="sxs-lookup"><span data-stu-id="cf6af-178">Request full control of the host web</span></span>

<span data-ttu-id="cf6af-p118">Так как теперь надстройка добавляет и удаляет дополнительные действия уровня веб-сайта, необходимо расширить разрешения для нее с уровня "Управление" до уровня "Полный контроль". Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p118">Since the add-in is now adding adding and deleting web-scoped custom actions, we need to escalate the permissions that the add-in requests from Manage to Full Control. Follow these steps.</span></span>
 

 

1. <span data-ttu-id="cf6af-181">В **обозревателе решений** откройте файл AppManifest.xml проекта **ChainStore**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-181">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>
    
 
2. <span data-ttu-id="cf6af-p119">Откройте вкладку **Разрешения**. Для поля **Область** оставьте значение **Интернет**, а в поле **Разрешение** выберите из раскрывающегося списка пункт **Полный доступ**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p119">Open the **Permissions** tab. Leave the **Scope** value at **Web**, but in the **Permission** field, select **Full Control** from the drop down.</span></span>
    
 
3. <span data-ttu-id="cf6af-184">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="cf6af-184">Save the file.</span></span>
    
 

## <a name="run-the-add-in-and-test-the-button-deployment"></a><span data-ttu-id="cf6af-185">Запуск надстройки и тестирование развертывания кнопки</span><span class="sxs-lookup"><span data-stu-id="cf6af-185">Run the add-in and test the button deployment</span></span>


 

 

1. <span data-ttu-id="cf6af-186">Откройте страницу **Содержимое сайта** для веб-сайта магазина в Гонконге *и удалите список **Местные сотрудники**.*</span><span class="sxs-lookup"><span data-stu-id="cf6af-186">Open the **Site Contents** page of the Hong Kong store's website *and remove the **Local Employees** list!*</span></span> 
    
     <span data-ttu-id="cf6af-187">**Примечание.** При отзыве надстройки в Visual Studio не будут удалены созданные ею списки, поэтому вам потребуется вручную удалять их каждый раз, когда вы тестируете создающий их код.</span><span class="sxs-lookup"><span data-stu-id="cf6af-187">**Note** Retracting an add-in in Visual Studio, does not remove lists that are created by the add-in, so you need to manually delete it any time you are testing code that creates it.</span></span>
2. <span data-ttu-id="cf6af-p120">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p120">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span>
    
 
3. <span data-ttu-id="cf6af-192">Когда откроется начальная страница надстройки, нажмите кнопку **Вернуться на сайт** на расположенном в верхней части элементе управления хрома.</span><span class="sxs-lookup"><span data-stu-id="cf6af-192">When the add-in's start page opens, select the **Back to Site** link on the chrome control at the top.</span></span>
    
 
4. <span data-ttu-id="cf6af-p121">Перейдите на страницу **Содержимое сайта**. Список **Местные сотрудники** отображается, потому что его добавил код, выполняемый при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p121">Navigate to the **Site Contents** page. The **Local Employees** list is present because your first-run logic added it.</span></span>
    
     <span data-ttu-id="cf6af-p122">**Примечание.** Если список не отображается или имеются другие признаки того, что код для первого запуска не выполняется, это может быть вызвано тем, что таблица **Tenants** (Клиенты) не очищается при нажатии клавиши F5. Как правило, это связано с тем, что проект **ChainCorporateDB** больше не задан в качестве запускаемого проекта в Visual Studio. В начале этой статьи есть примечание о том, как это исправить. Кроме того, убедитесь, что база данных настроена на повторное создание, как описано в разделе [Настройка Visual Studio на повторное создание корпоративной базы данных в каждом сеансе отладки](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel#Rebuild).</span><span class="sxs-lookup"><span data-stu-id="cf6af-p122">**Note** If the list is not there or you have other indications that the first-run code is not executing, it may be that the **Tenants** table is not being reverted to an empty state when you press F5. The most common cause of this is that the **ChainCorporateDB** project is no longer set as a startup project in Visual Studio. See the note near the top of this article for how to fix this. Also be sure that you've configured the database to be rebuilt as described in [Configure Visual Studio to rebuild the corporate database with each debugging session](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel#Rebuild).</span></span>
5. <span data-ttu-id="cf6af-199">Откройте список и добавьте элемент.</span><span class="sxs-lookup"><span data-stu-id="cf6af-199">Open the list and add an item.</span></span>
    
 
6. <span data-ttu-id="cf6af-p123">В представлении списка выберите этот элемент и откройте вкладку **Элемент** на ленте. На ленте имеется кнопка **Добавить в корпоративную базу данных**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p123">In the list view, select the item and open the **Item** tab on the ribbon. The **Add to Corporate DB** button is on the ribbon.</span></span>
    
 
7. <span data-ttu-id="cf6af-202">Нажмите эту кнопку. Сотрудник будет добавлен в корпоративную базу данных, а значение поля **Добавлено в корпоративную базу данных** изменится на **Да**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-202">Click the button and the employee is added to the corporate database and the **Added to Corporate DB** field is changed to **Yes**.</span></span>
    
 
8. <span data-ttu-id="cf6af-203">Вернитесь на страницу **Содержимое сайта** и нажмите **Добавить надстройку**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-203">Navigate back to the **Site Contents** page and select **add an add-in**.</span></span>
    
 
9. <span data-ttu-id="cf6af-p124">Добавьте новый **настраиваемый список**. По умолчанию он будет относиться к типу Generic (ему соответствует значение 100). После создания списка откройте вкладку **Элемент** на ленте. Обратите внимание, что кнопки **Добавить в корпоративную базу данных** *нет* на ленте. Это связано с тем, что код удалил кнопку на уровне веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p124">Add a new **Custom List**. By default it will be "Generic" type. (Generic is list type 100.) After the list is created, open the **Item** tab on the ribbon. Notice that the **Add to Corporate DB** button is *not*  on the ribbon. This because your code deleted the web-scoped button.</span></span>
    
 
10. <span data-ttu-id="cf6af-p125">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p125">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
11. <span data-ttu-id="cf6af-p126">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="cf6af-p126">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="cf6af-213"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="cf6af-213"></span></span>

 <span data-ttu-id="cf6af-p127">Для событий в списках и элементах списков также можно использовать настраиваемые обработчики в SharePoint. Сведения о том, как создать такой обработчик и развернуть его в коде, выполняемом при первом запуске, см. в статье [Обработка событий элемента списка в надстройке, размещаемой у поставщика](handle-list-item-events-in-the-provider-hosted-add-in).</span><span class="sxs-lookup"><span data-stu-id="cf6af-p127">Events on lists and list items can also have custom handlers in SharePoint. You learn how to create one and deploy it in your first-run logic in the next article: [Handle list item events in the provider-hosted add-in](handle-list-item-events-in-the-provider-hosted-add-in)</span></span>
 

 

