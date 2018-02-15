---
title: "Программное развертывание собственной кнопки в надстройке с размещением у поставщика"
description: "Регистрация программным путем настраиваемой кнопки ленты с настраиваемым списком в одной надстройке SharePoint, размещенной у поставщика."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 4bc647271a97a21da663d6e9aa55c8bb2a2f6189
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in"></a><span data-ttu-id="35ac0-103">Программное развертывание собственной кнопки в надстройке с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="35ac0-103">Programmatically deploy a custom button in the provider-hosted add-in</span></span>

<span data-ttu-id="35ac0-104">Это девятая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md#SP15createprovider_nextsteps).</span><span class="sxs-lookup"><span data-stu-id="35ac0-104">This is the ninth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 

> [!NOTE]
> <span data-ttu-id="35ac0-105">Если вы изучали предыдущие статьи этой серии о размещаемых у поставщика надстройках, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей.</span><span class="sxs-lookup"><span data-stu-id="35ac0-105">If you have been working through this series about provider-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="35ac0-106">Кроме того, вы можете скачать репозиторий [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeProgrammaticButton.sln.</span><span class="sxs-lookup"><span data-stu-id="35ac0-106">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeProgrammaticButton.sln file.</span></span>

<span data-ttu-id="35ac0-107">В этой статьи вы узнаете, как включать настраиваемую кнопку ленты в надстройку SharePoint, когда список, на ленте которого размещается кнопка, также развертывается программным способом в той же надстройке.</span><span class="sxs-lookup"><span data-stu-id="35ac0-107">In this article, you learn how to include a custom ribbon button in a SharePoint Add-in when the list whose ribbon gets the button is itself being programmatically deployed in the very same add-in.</span></span>

## <a name="re-add-the-custom-button-to-the-project"></a><span data-ttu-id="35ac0-108">Повторное добавление настраиваемой кнопки в проект</span><span class="sxs-lookup"><span data-stu-id="35ac0-108">Re-add the custom button to the project</span></span>

> [!NOTE]
> <span data-ttu-id="35ac0-109">Когда решение открывается повторно, для параметров раздела "Запускаемые проекты" в Visual Studio обычно возвращаются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="35ac0-109">The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened.</span></span> <span data-ttu-id="35ac0-110">После повторного открытия примера решения, который рассматривается в этой серии статей, всегда выполняйте указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="35ac0-110">Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 
> 1. <span data-ttu-id="35ac0-111">В верхней части **обозревателя решений** щелкните узел решения правой кнопкой мыши и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-111">Right-click the solution node at the top of **Solution Explorer**, and then select **Set startup projects**.</span></span>  
> 2. <span data-ttu-id="35ac0-112">Убедитесь, что в столбце **Действие** для всех трех проектов указано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-112">Ensure that all three projects are set to **Start** in the **Action** column.</span></span>

<span data-ttu-id="35ac0-113">В предыдущей статье вы удалили настраиваемую кнопку ленты **AddEmployeeToCorpDB** из проекта.</span><span class="sxs-lookup"><span data-stu-id="35ac0-113">In the previous article, you removed the custom **AddEmployeeToCorpDB** ribbon button from the project.</span></span> <span data-ttu-id="35ac0-114">Добавьте ее обратно, сделав вот что:</span><span class="sxs-lookup"><span data-stu-id="35ac0-114">Add it back in with the following steps.</span></span>

1. <span data-ttu-id="35ac0-115">В верхней части **обозревателя решений** на панели инструментов нажмите кнопку **Показать все файлы**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-115">On the toolbar at the top of **Solution Explorer**, select the **Show All Files** button.</span></span>

   <span data-ttu-id="35ac0-116">*Рис. 1. Панель инструментов обозревателя решений*</span><span class="sxs-lookup"><span data-stu-id="35ac0-116">*Figure 1. Solution Explorer toolbar*</span></span>

   ![Панель инструментов обозревателя решений с рамкой вокруг кнопки "Показать все файлы".](../images/f6b035f5-1aa7-452a-8f59-9dd44b062d06.PNG)

2. <span data-ttu-id="35ac0-118">В проекте **ChainStore** щелкните правой кнопкой мыши элемент **AddEmployeeToCorpDB**, а затем выберите пункт **Включить в проект**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-118">In the **ChainStore** project, right-click **AddEmployeeToCorpDB**, and then select **Include in Project**.</span></span>

3. <span data-ttu-id="35ac0-119">Снова нажмите кнопку **Показать все файлы**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-119">Select the **Show All Files** button again.</span></span>

4. <span data-ttu-id="35ac0-120">В проекте **ChainStore** разверните узел **AddEmployeeToCorpDB**, а затем откройте файл elements.xml.</span><span class="sxs-lookup"><span data-stu-id="35ac0-120">In the **ChainStore** project, expand **AddEmployeeToCorpDB**, and then open the elements.xml file.</span></span>

## <a name="understand-a-dilemma-and-its-solution"></a><span data-ttu-id="35ac0-121">Описание проблемы и ее решение</span><span class="sxs-lookup"><span data-stu-id="35ac0-121">Understand a dilemma and its solution</span></span>

<span data-ttu-id="35ac0-p104">В файле elements.xml атрибут **RegistrationId** элемента **CustomAction** служит для идентификации списка, на ленту которого вы добавляете кнопку: `{$ListId:Lists/Local Employees;}`. Это отлично работало, когда список уже был добавлен на хост-сайт вручную. Но теперь при развертывании списка программным способом в коде, выполняемом при первом запуске, когда SharePoint устанавливает надстройку и пытается развернуть кнопку, списка еще не существует. В этом случае установка надстройки может привести к созданию исключения и завершиться со сбоем.</span><span class="sxs-lookup"><span data-stu-id="35ac0-p104">In the elements.xml file, the **RegistrationId** attribute of the **CustomAction** element identifies the list on whose ribbon the button is added: `{$ListId:Lists/Local Employees;}`. This worked fine when the list had already been added to the host web manually. But now that we are deploying the list programmatically in first-run logic, the list doesn't exist when SharePoint installs the add-in and tries to deploy the button. The installation of the add-in would throw an exception and fail.</span></span>

<span data-ttu-id="35ac0-126">Развертывание списка в обработчике событий установки, а не в коде, выполняемом при первом запуске, не решит эту проблему. Это связано с тем, что SharePoint развертывает описанные настраиваемые компоненты, например настраиваемую кнопку (и веб-часть надстройки **Place Order** (Размещение заказа)), *прежде чем* запустить настраиваемый обработчик, поэтому когда SharePoint пытается развернуть кнопку, списка еще не существует.</span><span class="sxs-lookup"><span data-stu-id="35ac0-126">Deploying the list in the installation event handler, instead of first-run logic, won't solve the dilemma because SharePoint deploys custom descriptively-defined components, such as the custom button (and the **Place Order** add-in part), *before* it runs the custom handler, so the list won't exist when SharePoint tries to deploy the button.</span></span>

<span data-ttu-id="35ac0-127">Создание настраиваемой кнопки полностью программным способом непрактично по причинам, которые слишком сложны, чтобы обсуждать их здесь.</span><span class="sxs-lookup"><span data-stu-id="35ac0-127">Creating a custom button entirely programmatically is not practical for reasons that are too advanced to discuss here.</span></span> <span data-ttu-id="35ac0-128">К счастью, это не нужно.</span><span class="sxs-lookup"><span data-stu-id="35ac0-128">Fortunately, it is not necessary.</span></span> <span data-ttu-id="35ac0-129">Существует относительно безболезненный способ "полупрограммного" создания настраиваемой кнопки и назначения ее настраиваемому списку.</span><span class="sxs-lookup"><span data-stu-id="35ac0-129">There is a relatively painless way to semi-programmatically create a custom button and assign it to a custom list.</span></span> 

<span data-ttu-id="35ac0-130">Для этого нужно выполнить вот какие основные действия:</span><span class="sxs-lookup"><span data-stu-id="35ac0-130">The following are the basic steps:</span></span>

1. <span data-ttu-id="35ac0-131">Оставьте описательно определенную кнопку в проекте, но назначьте ее ленте какого-либо приложения, которое всегда имеется на сайтах SharePoint, а не ленте списка, который развертывается программным способом с помощью той же надстройки.</span><span class="sxs-lookup"><span data-stu-id="35ac0-131">Keep the descriptively defined button in the project, but assign it to the ribbon of something that always exists on SharePoint sites, instead of to a list that's programmatically deployed with the same add-in.</span></span> 

2. <span data-ttu-id="35ac0-132">В коде, выполняемом при первом запуске, после программного создания списка добавьте неопределенную кнопку на ленту списка.</span><span class="sxs-lookup"><span data-stu-id="35ac0-132">In the first-run logic, after the list is programmatically created, programmatically add an undefined button to the ribbon of the list.</span></span>

3. <span data-ttu-id="35ac0-133">Инициализируйте свойства новой кнопки, используя значения свойств исходной кнопки.</span><span class="sxs-lookup"><span data-stu-id="35ac0-133">Initialize the properties of the new button with the values of the original button.</span></span> <span data-ttu-id="35ac0-134">Сейчас у нас есть две идентичные кнопки.</span><span class="sxs-lookup"><span data-stu-id="35ac0-134">At this point there are two identical buttons.</span></span> <span data-ttu-id="35ac0-135">Вторая кнопка назначена ленте списка **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="35ac0-135">The second is assigned to the ribbon of the **Local Employees** list.</span></span>

4. <span data-ttu-id="35ac0-136">Удалите исходную кнопку программным способом.</span><span class="sxs-lookup"><span data-stu-id="35ac0-136">Programmatically delete the original button.</span></span>

## <a name="programmatically-register-the-custom-button"></a><span data-ttu-id="35ac0-137">Регистрация настраиваемой кнопки программным способом</span><span class="sxs-lookup"><span data-stu-id="35ac0-137">Programmatically register the custom button</span></span>

<span data-ttu-id="35ac0-138">Ниже описывается реализация этой стратегии.</span><span class="sxs-lookup"><span data-stu-id="35ac0-138">The following procedure shows how to implement this strategy.</span></span>

1. <span data-ttu-id="35ac0-139">В проекте **ChainStore** разверните узел **AddEmployeeToCorpDB**, откройте файл elements.xml, а затем измените значение атрибута **RegistrationId** элемента **CustomAction** на число 100.</span><span class="sxs-lookup"><span data-stu-id="35ac0-139">In the **ChainStore** project, expand **AddEmployeeToCorpDB**, open the elements.xml file, and then change the value of the **RegistrationId** attribute of the **CustomAction** element to "100".</span></span> <span data-ttu-id="35ac0-140">Это идентификатор типа списка.</span><span class="sxs-lookup"><span data-stu-id="35ac0-140">This is the ID of a type of list.</span></span> <span data-ttu-id="35ac0-141">Даже если на веб-сайте нет экземпляров списка этого типа, *тип* списка есть на всех веб-сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="35ac0-141">Even if there are no instances of lists of this type on the website, the list *type* is on every SharePoint website.</span></span> <span data-ttu-id="35ac0-142">Теперь атрибут должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="35ac0-142">The attribute should now look like the following.</span></span>
    
    ```XML
      RegistrationId="100"
    ```

2. <span data-ttu-id="35ac0-143">В файле SharePointComponentDeployer.cs добавьте указанную ниже строку в метод **DeployChainStoreComponentsToHostWeb** сразу же после строки, в которой вызывается метод `CreateLocalEmployeesList`. Вы создадите этот метод на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="35ac0-143">In the file SharePointComponentDeployer.cs, add the following line to the **DeployChainStoreComponentsToHostWeb** method, just under the line that calls `CreateLocalEmployeesList` (you create this method in the next step).</span></span>
    
    ```C#
      ChangeCustomActionRegistration();
    ```

3. <span data-ttu-id="35ac0-144">Добавьте указанный ниже метод в класс `SharePointComponentDeployer`.</span><span class="sxs-lookup"><span data-stu-id="35ac0-144">Add the following method to the `SharePointComponentDeployer` class.</span></span> 

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

   <span data-ttu-id="35ac0-145">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="35ac0-145">Note the following about this code:</span></span>
    
   - <span data-ttu-id="35ac0-146">Так как дополнительное действие, то есть настраиваемая кнопка, зарегистрировано на ленте для *типа* списка, область его действия распространяется на весь веб-сайт и находится в коллекции дополнительных действий веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="35ac0-146">Because the custom action, that is, the custom button, was registered with the ribbon of a list *type*, it is scoped to the entire website and is in the website's collection of custom actions.</span></span> <span data-ttu-id="35ac0-147">Таким образом, код получает его из этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="35ac0-147">So the code retrieves it from that collection.</span></span>
    
   - <span data-ttu-id="35ac0-148">Значение свойства `action.Name` поступает из атрибута **ID** элемента **CustomAction** в файле element.xml из узла **AddEmployeeToCorpDB**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-148">The value of the `action.Name` comes from the **ID** attribute of the **CustomAction** element in the element.xml file in **AddEmployeeToCorpDB**.</span></span>
    
   > [!IMPORTANT]
   > <span data-ttu-id="35ac0-149">**Вам необходимо изменить значение `action.Name` в коде, чтобы оно совпадало со значением в файле elements.xml.**</span><span class="sxs-lookup"><span data-stu-id="35ac0-149">**You must change the `action.Name` value in the code to match the value in your elements.xml file.**</span></span> <span data-ttu-id="35ac0-150">Часть GUID имени будет другой.</span><span class="sxs-lookup"><span data-stu-id="35ac0-150">The GUID part of the name will be different.</span></span> <span data-ttu-id="35ac0-151">Обратите внимание, что между GUID и остальной частью имени есть символ `"."`.</span><span class="sxs-lookup"><span data-stu-id="35ac0-151">Note that there is a `"."` character between the GUID and the rest of the name.</span></span> <span data-ttu-id="35ac0-152">Вот пример строки:</span><span class="sxs-lookup"><span data-stu-id="35ac0-152">The following is an example of the line:</span></span> 
   > 
   > `where action.Name == "4a926a42-3577-4e02-9d06-fef78586b1bc.AddEmployeeToCorpDB"`

4. <span data-ttu-id="35ac0-153">Замените `TODO8` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="35ac0-153">Replace `TODO8` with the following code.</span></span> <span data-ttu-id="35ac0-154">Обратите внимание, что если вы отзовете надстройку, созданные ею компоненты не будут удалены.</span><span class="sxs-lookup"><span data-stu-id="35ac0-154">Note that when you retract an add-in, components created by the add-in are not removed.</span></span> <span data-ttu-id="35ac0-155">По завершении работы кода, выполняемого при первом запуске, в коллекции **UserCustomActions** списка появится дополнительное действие, которое не будет отозвано при следующем нажатии клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="35ac0-155">After your first-run logic executes, there will be a custom action in the list's **UserCustomActions** collection, and it will not be retracted the next time you select F5.</span></span> <span data-ttu-id="35ac0-156">Чтобы избежать путаницы, в последней строке в этом коде метод `listActions.Clear();` очищает коллекцию.</span><span class="sxs-lookup"><span data-stu-id="35ac0-156">To avoid confusion, the last line in this code `listActions.Clear();` empties the collection.</span></span>

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

5. <span data-ttu-id="35ac0-157">Замените `TODO9` указанной ниже строкой, которая добавляет неопределенное дополнительное действие в список **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="35ac0-157">Replace `TODO9` with the following line, which adds an undefined custom action to the **Local Employees** list.</span></span>
    
    ```C#
      var listScopedEmployeeAction = listActions.Add();
    ```

6. <span data-ttu-id="35ac0-158">Замените `TODO10` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="35ac0-158">Replace `TODO10` with the following code.</span></span> 

    ```C#
    listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
    listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
    listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
    listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
    listScopedEmployeeAction.Update();
    ```

   <span data-ttu-id="35ac0-159">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="35ac0-159">Note the following about this code:</span></span>
    
   - <span data-ttu-id="35ac0-160">Он назначает значения свойств кнопки уровня веб-сайта (которая была развернута с помощью описательной разметки) соответствующим свойствам кнопки уровня списка, так что эти две кнопки становятся идентичными за исключением области их действия.</span><span class="sxs-lookup"><span data-stu-id="35ac0-160">It assigns the property values of the web-scoped button (that was deployed with descriptive markup) to the corresponding properties of the list-scoped button, so the two buttons are identical except in scope.</span></span>
    
   - <span data-ttu-id="35ac0-161">В свойстве **Sequence** указывается относительный порядок, в котором кнопка будет отображена в своей области на ленте.</span><span class="sxs-lookup"><span data-stu-id="35ac0-161">The **Sequence** property specifies the relative order that the button will appear in its area of the ribbon.</span></span> <span data-ttu-id="35ac0-162">В этом случае кнопка находится в разделе **Actions** (Действия) на вкладке **Items** (Элементы) ленты.</span><span class="sxs-lookup"><span data-stu-id="35ac0-162">In this case, the button is on the **Actions** section of the **Items** tab of the ribbon.</span></span> <span data-ttu-id="35ac0-163">В описательной разметке это значение было равно 10001. Это достаточно большое значение, чтобы кнопка отображалась после (т. е. справа от) всех встроенных кнопок, которые SharePoint самостоятельно помещает в раздел **Actions** (Действия) ленты.</span><span class="sxs-lookup"><span data-stu-id="35ac0-163">In the descriptive markup, this value was set to 10001, which is high enough to ensure that it will appear after (that is, to the right of) any in-the-box buttons that SharePoint itself puts in the **Actions** section of the ribbon.</span></span>

7. <span data-ttu-id="35ac0-164">Замените `TODO11` указанной ниже строкой, в которой удаляется исходная кнопка, определенная описательным способом.</span><span class="sxs-lookup"><span data-stu-id="35ac0-164">Replace `TODO11` with the following line, which deletes the original descriptively-defined button.</span></span> <span data-ttu-id="35ac0-165">Если бы у нас не было этой строки, то каждый список на веб-сайте, для которого используется шаблон списка 100, включал бы настраиваемую кнопку.</span><span class="sxs-lookup"><span data-stu-id="35ac0-165">If we did not have this line, every list on the website that uses list template "100" would have the custom button on it.</span></span> <span data-ttu-id="35ac0-166">Так как функциональность кнопки тесно связана со списком **Local Employees** (Местные сотрудники), то нет никакого смысла размещать эту кнопку в других списках.</span><span class="sxs-lookup"><span data-stu-id="35ac0-166">Because the button's functionality is closely tied to the **Local Employees** list, it would make no sense to have the button on any other list.</span></span> <span data-ttu-id="35ac0-167">Кроме того, без этой строки кнопка будет *дважды* размещена в списке **Local Employees** (Местные сотрудники), так как для этого списка используется шаблон 100.</span><span class="sxs-lookup"><span data-stu-id="35ac0-167">Also, without this line, the button would appear *twice*  on the **Local Employees** list, because that list uses template "100".</span></span>
    
    ```C#
      webScopedEmployeeAction.DeleteObject();
    ```
    
8. <span data-ttu-id="35ac0-168">Теперь весь метод должен иметь указанный ниже вид (за исключением того, что заполнитель необходимо заменить на GUID).</span><span class="sxs-lookup"><span data-stu-id="35ac0-168">The entire method should now look like the following (except there should be a GUID in place of the placeholder).</span></span>
    
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


## <a name="request-full-control-of-the-host-web"></a><span data-ttu-id="35ac0-169">Запрос полного контроля над хост-сайтом</span><span class="sxs-lookup"><span data-stu-id="35ac0-169">Request full control of the host web</span></span>

<span data-ttu-id="35ac0-170">Так как теперь надстройка добавляет и удаляет дополнительные действия уровня веб-сайта, необходимо расширить разрешения для нее с уровня "Управление" до уровня "Полный контроль". Для этого сделайте вот что:</span><span class="sxs-lookup"><span data-stu-id="35ac0-170">Because the add-in now adds and deletes web-scoped custom actions, we need to escalate the permissions that the add-in requests from Manage to Full Control:</span></span>

1. <span data-ttu-id="35ac0-171">В **обозревателе решений** в проекте **ChainStore** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="35ac0-171">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>

2. <span data-ttu-id="35ac0-172">Откройте вкладку **Разрешения**. Для поля **Область** оставьте значение **Интернет**, а в поле **Разрешение** выберите из раскрывающегося списка пункт **Полный контроль**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-172">Open the **Permissions** tab. Leave the **Scope** value at **Web**, but in the **Permission** field, select **Full Control** from the drop-down.</span></span>

3. <span data-ttu-id="35ac0-173">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="35ac0-173">Save the file.</span></span>

## <a name="run-the-add-in-and-test-the-button-deployment"></a><span data-ttu-id="35ac0-174">Запуск надстройки и тестирование развертывания кнопки</span><span class="sxs-lookup"><span data-stu-id="35ac0-174">Run the add-in and test the button deployment</span></span>

1. <span data-ttu-id="35ac0-175">Откройте страницу **Site Contents** (Содержание сайта) веб-сайта магазина в Гонконге и удалите список **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="35ac0-175">Open the **Site Contents** page of the Hong Kong store's website and remove the **Local Employees** list.</span></span> 
    
   > [!NOTE]
   > <span data-ttu-id="35ac0-176">При отзыве надстройки в Visual Studio не будут удалены созданные ею списки, поэтому вам потребуется вручную удалять их каждый раз, когда вы тестируете создающий их код.</span><span class="sxs-lookup"><span data-stu-id="35ac0-176">Retracting an add-in in Visual Studio does not remove lists that are created by the add-in, so you need to manually delete it any time you are testing code that creates it.</span></span>

2. <span data-ttu-id="35ac0-177">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="35ac0-177">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="35ac0-178">Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express.</span><span class="sxs-lookup"><span data-stu-id="35ac0-178">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="35ac0-179">Кроме того, он выполняет временную установку надстройки на вашем тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="35ac0-179">It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="35ac0-180">Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="35ac0-180">You are prompted to grant permissions to the add-in before its start page opens.</span></span>

3. <span data-ttu-id="35ac0-181">Когда откроется начальная страница надстройки, перейдите по ссылке **Вернуться на сайт** на размещенном в верхней части элементе управления хрома.</span><span class="sxs-lookup"><span data-stu-id="35ac0-181">When the add-in's start page opens, select the **Back to Site** link on the chrome control at the top.</span></span>

4. <span data-ttu-id="35ac0-182">Перейдите на страницу **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-182">Go to the **Site Contents** page.</span></span> <span data-ttu-id="35ac0-183">На ней будет список **Local Employees** (Местные сотрудники), так как его добавила логика первого запуска.</span><span class="sxs-lookup"><span data-stu-id="35ac0-183">The **Local Employees** list is present because your first-run logic added it.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="35ac0-184">Если списка там нет или имеются другие признаки того, что код первого запуска не выполняется, может быть, при нажатии клавиши F5 таблица **Клиенты** не очищается.</span><span class="sxs-lookup"><span data-stu-id="35ac0-184">If the list is not there or you have other indications that the first-run code is not executing, it may be that the **Tenants** table is not being reverted to an empty state when you select F5.</span></span> <span data-ttu-id="35ac0-185">Как правило, это связано с тем, что проект **ChainCorporateDB** больше не задан в качестве запускаемого в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35ac0-185">The most common cause of this is that the **ChainCorporateDB** project is no longer set as a startup project in Visual Studio.</span></span> <span data-ttu-id="35ac0-186">См. [примечание в верхней части данной статьи](#re-add-the-custom-button-to-the-project) о том, как устранить эту проблему.</span><span class="sxs-lookup"><span data-stu-id="35ac0-186">See the [note near the top of this article](#re-add-the-custom-button-to-the-project) for how to fix this.</span></span> <span data-ttu-id="35ac0-187">Кроме того, убедитесь, что вы настроили базу данных так, чтобы она перестраивалась, как описано в разделе [Настройка Visual Studio для перестройки корпоративной базы данных при каждом сеансе отладки](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md#Rebuild).</span><span class="sxs-lookup"><span data-stu-id="35ac0-187">Also be sure that you've configured the database to be rebuilt as described in [Configure Visual Studio to rebuild the corporate database with each debugging session](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md#Rebuild).</span></span>

5. <span data-ttu-id="35ac0-188">Откройте список и добавьте элемент.</span><span class="sxs-lookup"><span data-stu-id="35ac0-188">Open the list and add an item.</span></span>

6. <span data-ttu-id="35ac0-189">В представлении списка выберите этот элемент и откройте вкладку **Item** (Элемент) на ленте.</span><span class="sxs-lookup"><span data-stu-id="35ac0-189">In the list view, select the item, and then open the **Item** tab on the ribbon.</span></span> 

7. <span data-ttu-id="35ac0-190">На вкладке **Item** (Элемент) нажмите кнопку **Add to Corporate DB** (Добавить в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="35ac0-190">On the **Item** tab, select the **Add to Corporate DB** button.</span></span> <span data-ttu-id="35ac0-191">Сотрудник будет добавлен в корпоративную базу данных, а значение поля **Added to Corporate DB** (Добавлен в корпоративную базу данных) изменится на **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="35ac0-191">The employee is added to the corporate database, and the **Added to Corporate DB** field is changed to **Yes**.</span></span>

8. <span data-ttu-id="35ac0-192">Вернитесь на страницу **Site Contents** (Содержание сайта) и выберите **Add an add-in** (Добавить надстройку).</span><span class="sxs-lookup"><span data-stu-id="35ac0-192">Go back to the **Site Contents** page and select **Add an add-in**.</span></span>

9. <span data-ttu-id="35ac0-193">Добавьте новый **настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-193">Add a new **Custom List**.</span></span> <span data-ttu-id="35ac0-194">По умолчанию он будет иметь тип Generic, которому соответствует тип списка 100.</span><span class="sxs-lookup"><span data-stu-id="35ac0-194">By default it will be "Generic" type (Generic is list type 100).</span></span> <span data-ttu-id="35ac0-195">После создания списка откройте вкладку **Item** (Элемент) на ленте.</span><span class="sxs-lookup"><span data-stu-id="35ac0-195">After the list is created, open the **Item** tab on the ribbon.</span></span> <span data-ttu-id="35ac0-196">Обратите внимание, что кнопки **Add to Corporate DB** (Добавить в корпоративную базу данных) *нет* на ленте.</span><span class="sxs-lookup"><span data-stu-id="35ac0-196">Notice that the **Add to Corporate DB** button is *not*  on the ribbon.</span></span> <span data-ttu-id="35ac0-197">Это связано с тем, что ваш код удалил кнопку уровня веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="35ac0-197">This is because your code deleted the web-scoped button.</span></span>

10. <span data-ttu-id="35ac0-198">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35ac0-198">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="35ac0-199">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="35ac0-199">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

11. <span data-ttu-id="35ac0-200">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="35ac0-200">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="35ac0-201">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="35ac0-201">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35ac0-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35ac0-202">Next steps</span></span>
<span data-ttu-id="35ac0-203"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="35ac0-203"></span></span>

<span data-ttu-id="35ac0-204">Для событий в списках и элементах списков также можно использовать настраиваемые обработчики в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="35ac0-204">Events on lists and list items can also have custom handlers in SharePoint.</span></span> <span data-ttu-id="35ac0-205">Чтобы узнать, как создать такой обработчик и развернуть его в коде, выполняемом при первом запуске, см. статью [Обработка событий элемента списка в надстройке, размещаемой у поставщика](handle-list-item-events-in-the-provider-hosted-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="35ac0-205">You will learn how to create one and deploy it in your first-run logic in [Handle list item events in the provider-hosted add-in](handle-list-item-events-in-the-provider-hosted-add-in.md).</span></span>
 

 

