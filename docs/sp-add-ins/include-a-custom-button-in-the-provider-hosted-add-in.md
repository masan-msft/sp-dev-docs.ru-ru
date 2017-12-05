---
title: "Добавление собственной кнопки в надстройку с размещением у поставщика"
description: "Создание специального списка на хост-сайте, добавление специальной кнопки, запрашивание разрешений на чтение, запуск надстройки и тестирование кнопки."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 62dce66d9f2c0cd1a33f505659bafe065e5a9f99
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="include-a-custom-button-in-the-provider-hosted-add-in"></a><span data-ttu-id="364ad-103">Добавление специальной кнопки в надстройку, размещаемую у поставщика</span><span class="sxs-lookup"><span data-stu-id="364ad-103">Include a custom button in the provider-hosted add-in</span></span>

<span data-ttu-id="364ad-104">Это третья часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии:</span><span class="sxs-lookup"><span data-stu-id="364ad-104">This is the third in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  <span data-ttu-id="364ad-105">[Знакомство с созданием надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md);</span><span class="sxs-lookup"><span data-stu-id="364ad-105">[Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md)</span></span>
-  <span data-ttu-id="364ad-106">[Настройка внешнего вида надстройки SharePoint, размещаемой у поставщика](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md).</span><span class="sxs-lookup"><span data-stu-id="364ad-106">[Give your provider-hosted add-in the SharePoint look-and-feel](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)</span></span>
    
> [!NOTE]
> <span data-ttu-id="364ad-107">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, значит у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей.</span><span class="sxs-lookup"><span data-stu-id="364ad-107">Note  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_Provider-hosted_Add-Ins_Tutorials and open the BeforeRibbonButton.sln file.</span></span> <span data-ttu-id="364ad-108">Кроме того, вы можете скачать репозиторий [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeRibbonButton.sln.</span><span class="sxs-lookup"><span data-stu-id="364ad-108">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeRibbonButton.sln file.</span></span>

<span data-ttu-id="364ad-109">Надстройка SharePoint может включать дополнительные действия, представляющие собой термин SharePoint для специальных элементов меню или кнопок ленты.</span><span class="sxs-lookup"><span data-stu-id="364ad-109">A SharePoint Add-in can include custom actions, which is the SharePoint term for a custom menu items or ribbon buttons. In this article you'll learn how to create a custom button that synchronizes a SharePoint list with a remote database.</span></span> <span data-ttu-id="364ad-110">В этой статье рассказано, как создать специальную кнопку, которая синхронизирует список SharePoint с удаленной базой данных.</span><span class="sxs-lookup"><span data-stu-id="364ad-110">A spappsing can include custom actions, which is the SharePoint term for a custom menu items or ribbon buttons. In this article you'll learn how to create a custom button that synchronizes a SharePoint list with a remote database.</span></span>
 
## <a name="create-a-custom-list-on-the-host-website"></a><span data-ttu-id="364ad-111">Создание специального списка на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="364ad-111">Create a custom list on the host website</span></span>

<span data-ttu-id="364ad-p103">Предполагается, что настраиваемая кнопка будет размещена на ленте определенного списка, в котором записаны сведения о сотрудниках местного магазина. В одной из следующих статей этой серии вы узнаете, как программным способом добавить настраиваемый список на хост-сайт, а при изучении данной статьи вы добавите такой список вручную.</span><span class="sxs-lookup"><span data-stu-id="364ad-p103">The custom button is going to be on the ribbon of a specific list that records the employees of the local store. In a later article in this series, you'll learn how to programmatically add a custom list to a host website, but for now you'll add one manually.</span></span> 

1. <span data-ttu-id="364ad-114">На домашней странице магазина Fabrikam Hong Kong выберите пункты **Содержимое сайта** > **Добавить надстройку** > **Настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="364ad-114">From the home page of the Fabrikam Hong Kong Store, navigate to  Site Contents | add an add-in | Custom List.</span></span> 

2. <span data-ttu-id="364ad-115">В диалоговом окне **Настраиваемый список — добавление** укажите имя **Local Employees** (Местные сотрудники) и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="364ad-115">In the Adding Custom List dialog, specifyLocal Employees as the name and press Create.</span></span> 

3. <span data-ttu-id="364ad-116">На странице **Содержимое сайта** откройте список **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="364ad-116">On the **Site Contents** page, open the **Local Employees** list.</span></span>

4. <span data-ttu-id="364ad-117">Откройте вкладку **Список** на ленте, а затем нажмите кнопку **Параметры списка**.</span><span class="sxs-lookup"><span data-stu-id="364ad-117">On the **List** tab on the ribbon, select **List Settings**.</span></span>

5. <span data-ttu-id="364ad-118">В разделе **Столбцы** на странице **Параметры списка** выберите столбец **Название**.</span><span class="sxs-lookup"><span data-stu-id="364ad-118">In the  **Columns** section of the **List Settings** page, click the **Title** column.</span></span>

6. <span data-ttu-id="364ad-119">Откроется форма **Изменение столбца**. Замените значение **Название** в поле **Имя столбца** на **Имя**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="364ad-119">In the  Edit Column form, change the Column name from Title toProduct; and then click  OK.</span></span>

7. <span data-ttu-id="364ad-120">На странице **Параметры** выберите команду **Создать столбец**.</span><span class="sxs-lookup"><span data-stu-id="364ad-120">On the **Settings** page, click **Create column**.</span></span>

8. <span data-ttu-id="364ad-121">В форме **Создание столбца** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="364ad-121">In the **Create Column** form, do the following:</span></span>
    
   1. <span data-ttu-id="364ad-122">В поле **Имя столбца** введите **Added to Corporate DB** (Добавлено в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="364ad-122">For **Column name**, enter **Added to Corporate DB**.</span></span>
   2. <span data-ttu-id="364ad-123">В качестве **типа** укажите **Да/Нет (флажок)**.</span><span class="sxs-lookup"><span data-stu-id="364ad-123">Set the type to  Yes/No (check box).</span></span>
   3. <span data-ttu-id="364ad-124">В поле **Значение по умолчанию** укажите значение **Нет**.</span><span class="sxs-lookup"><span data-stu-id="364ad-124">Set the  **Default value** to **No**.</span></span>
   4. <span data-ttu-id="364ad-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="364ad-125">Select **OK**.</span></span> <span data-ttu-id="364ad-126">Снова откроется страница **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="364ad-126">Press  OK. You are taken back to the  **Settings** page.</span></span>
    
9. <span data-ttu-id="364ad-127">Выберите **Содержимое сайта**, чтобы открыть страницу **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="364ad-127">Select **Site Contents** to open the **Site Contents** page.</span></span> <span data-ttu-id="364ad-128">На ней отобразится плитка для нового списка.</span><span class="sxs-lookup"><span data-stu-id="364ad-128">Click  Site Contents to open the Site Contents page. The tile for the new list is there. Open it.</span></span> <span data-ttu-id="364ad-129">Откройте ее.</span><span class="sxs-lookup"><span data-stu-id="364ad-129">Open it.</span></span>
    
10. <span data-ttu-id="364ad-130">Щелкните **Создайте элемент** и в форме создания элемента введите имя, но *не* устанавливайте флажок **Added to Corporate DB** (Добавлено в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="364ad-130">Click  **new item** and on the create item form, enter a name, but do *not*  check **Added to Corporate DB**. Then click  Save. The list should look similar to the following:</span></span> <span data-ttu-id="364ad-131">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="364ad-131">Select **Save**.</span></span> <span data-ttu-id="364ad-132">Список должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="364ad-132">The calendar should look similar to the following:</span></span>

    <span data-ttu-id="364ad-133">*Рис. 1. Список местных сотрудников с одним элементом*</span><span class="sxs-lookup"><span data-stu-id="364ad-133">*Figure 1. Local Employees list with a single item*</span></span>

    ![Список местных сотрудников с одним элементом. Имя — Григорий Иванов. В столбце "Added to Corporate DB" (Добавлено в корпоративную базу данных) указано значение "Нет".](../images/a3371859-e42f-49ea-8f17-48d8a248b075.PNG)

## <a name="add-the-custom-button"></a><span data-ttu-id="364ad-137">Добавление специальной кнопки</span><span class="sxs-lookup"><span data-stu-id="364ad-137">Add the custom button</span></span>

<span data-ttu-id="364ad-138">В этом разделе показано, как добавить в надстройку часть кода, которая будет развертывать кнопку на ленте списка.</span><span class="sxs-lookup"><span data-stu-id="364ad-138">In this section, you include markup in the add-in that deploys a button to the list's ribbon.</span></span> <span data-ttu-id="364ad-139">Когда пользователь выделяет сотрудника в списке и нажимает кнопку, имя сотрудника добавляется в корпоративную базу данных, а в поле **Added to Corporate DB** (Добавлено в корпоративную базу данных) для этого сотрудника значение **Нет** заменяется на **Да**.</span><span class="sxs-lookup"><span data-stu-id="364ad-139">In this section, you include markup in the add-in that will deploy a button to the list's ribbon. When a user highlights an employee on the list and clicks the button, the employee's name will be added to the corporate database and the  Added to Corporate DB field for the employee will be switched from No to Yes.</span></span>

1.  <span data-ttu-id="364ad-140">Если открыт редактор Visual Studio, вам необходимо будет закрыть его и повторно открыть решение Chain Store, чтобы Visual Studio обнаружил новый список. (Запустите Visual Studio от имени администратора.)</span><span class="sxs-lookup"><span data-stu-id="364ad-140">If Visual Studio is open, you have to close it  and reopen the Chain Store solution so that Visual Studio can discover your new list. (Run Visual Studio as an administrator.)</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="364ad-141">Когда решение открывается повторно, для параметров раздела "Startup Projects" (Запускаемые проекты) в Visual Studio обычно возвращаются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="364ad-141">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> <span data-ttu-id="364ad-142">Сразу же после повторного открытия примера решения согласно инструкциям из этой серии статей всегда выполняйте указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="364ad-142">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 

   > 1. <span data-ttu-id="364ad-143">В верхней части **обозревателя решений** щелкните правой кнопкой мыши узел решения и выберите **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="364ad-143">Right-click the solution node at the top of  **Solution Explorer** and select **Set startup projects**.</span></span>  
   > 2. <span data-ttu-id="364ad-144">Убедитесь, что в столбце **Действие** для всех трех проектов указано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="364ad-144">Make sure all three projects are set to  **Start** in the **Action** column.</span></span>

2. <span data-ttu-id="364ad-145">В **обозревателе решений** щелкните правой кнопкой мыши проект **ChainStore** и выберите пункты **Добавить** > **Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="364ad-145">Right-click the **ChainStore** project in **Solution Explorer**, and then select **Add** > **New Item**.</span></span> 
    
3. <span data-ttu-id="364ad-146">В диалоговом окне **Добавить новый элемент** выберите **Настраиваемое действие ленты**, укажите имя **AddEmployeeToCorpDB**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="364ad-146">In the  **Add New Item** dialog, select **Ribbon Custom Action**, give it the name AddEmployeeToCorpDB, and then click  **Add**.</span></span>

4. <span data-ttu-id="364ad-p110">Откроется диалоговое окно с тремя вопросами. Выберите следующие ответы:</span><span class="sxs-lookup"><span data-stu-id="364ad-p110">The dialog that opens asks three questions. Give the following answers:</span></span>

   |<span data-ttu-id="364ad-149">**Вопрос**</span><span class="sxs-lookup"><span data-stu-id="364ad-149">**Question**</span></span>|<span data-ttu-id="364ad-150">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="364ad-150">**Give this answer:**</span></span>|
   |:-----|:-----|
   |<span data-ttu-id="364ad-151">**Где требуется предоставить настраиваемое действие?**</span><span class="sxs-lookup"><span data-stu-id="364ad-151">**Where do you want to expose the custom action?**</span></span>|<span data-ttu-id="364ad-152">Хост-сайт</span><span class="sxs-lookup"><span data-stu-id="364ad-152">Host Web</span></span>|
   |<span data-ttu-id="364ad-153">**К какой области относится настраиваемое действие?**</span><span class="sxs-lookup"><span data-stu-id="364ad-153">**Where is the custom action scoped to?**</span></span>|<span data-ttu-id="364ad-154">Экземпляр списка</span><span class="sxs-lookup"><span data-stu-id="364ad-154">List Instance</span></span>|
   |<span data-ttu-id="364ad-155">**Каким конкретным элементом ограничена область настраиваемого действия?**</span><span class="sxs-lookup"><span data-stu-id="364ad-155">**Which particular item is the custom action scoped to?**</span></span>|<span data-ttu-id="364ad-156">Local Employees</span><span class="sxs-lookup"><span data-stu-id="364ad-156">Local Employees</span></span>|

5. <span data-ttu-id="364ad-157">Нажмите кнопку **Далее**. Появятся еще три вопроса.</span><span class="sxs-lookup"><span data-stu-id="364ad-157">Click  **Next** and you get three more questions:</span></span>

   |<span data-ttu-id="364ad-158">**Вопрос**</span><span class="sxs-lookup"><span data-stu-id="364ad-158">**Question**</span></span>|<span data-ttu-id="364ad-159">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="364ad-159">**Give this answer:**</span></span>|
   |:-----|:-----|
   |<span data-ttu-id="364ad-160">**Где расположен этот элемент управления?**</span><span class="sxs-lookup"><span data-stu-id="364ad-160">**Where is the control located?**</span></span>|<span data-ttu-id="364ad-161">Ribbon.ListItem.Actions</span><span class="sxs-lookup"><span data-stu-id="364ad-161">Ribbon.ListItem.Actions</span></span>|
   |<span data-ttu-id="364ad-162">**Какой текст должен отображаться на подписи этой кнопки?**</span><span class="sxs-lookup"><span data-stu-id="364ad-162">**What is the label text for the button control?**</span></span>|<span data-ttu-id="364ad-163">Add To Corporate DB</span><span class="sxs-lookup"><span data-stu-id="364ad-163">Add to Corporate DB</span></span>|
   |<span data-ttu-id="364ad-164">**Куда ведет элемент управления "Кнопка"?**</span><span class="sxs-lookup"><span data-stu-id="364ad-164">**Where does the button control navigate to?**</span></span>|<span data-ttu-id="364ad-165">ChainStoreWeb\Pages\EmployeeAdder.aspx</span><span class="sxs-lookup"><span data-stu-id="364ad-165">ChainStoreWeb\Pages\EmployeeAdder.aspx</span></span><br/><span data-ttu-id="364ad-166">(это страница, код программной части которой будет добавлять сотрудника в базу данных)</span><span class="sxs-lookup"><span data-stu-id="364ad-166">ChainStoreWeb\Pages\EmployeeAdder.aspx (This is a page whose code behind is going to add the employee to the database.)</span></span>|

6. <span data-ttu-id="364ad-167">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="364ad-167">Click  **Finish**.</span></span>
    
   <span data-ttu-id="364ad-168">Файл elements.xml, который определяет дополнительное действие, будет добавлен в проект и открыт.</span><span class="sxs-lookup"><span data-stu-id="364ad-168">An elements.xml file that defines the add-in part is added to the project and opened.</span></span> <span data-ttu-id="364ad-169">Вы можете обращаться с этим файлом как с "черным ящиком". Вам не потребуется вносить в него изменения до знакомства со следующими статьями этой серии.</span><span class="sxs-lookup"><span data-stu-id="364ad-169">An elements.xml file that defines the custom action is added to the project and opened. For the most part, you can treat this file as a black box, and you won't need to make any changes in it untill a later article in this series. For now, note only the following:</span></span> <span data-ttu-id="364ad-170">А сейчас обратите внимание на указанные ниже моменты.</span><span class="sxs-lookup"><span data-stu-id="364ad-170">For now, note only the following:</span></span>

   - <span data-ttu-id="364ad-171">Атрибут **Location** элемента **CommandUIDefinition** имеет значение `Ribbon.ListItem.Actions.Controls_children`.</span><span class="sxs-lookup"><span data-stu-id="364ad-171">The  **Location** attribute of the **CommandUIDefinition** element has the value `Ribbon.ListItem.Actions.Controls_children`.</span></span> <span data-ttu-id="364ad-172">Его вторая часть (`ListItem`) идентифицирует *вкладку* на ленте, на которую будет помещена кнопка (но это может и не быть точным отображаемым именем вкладки).</span><span class="sxs-lookup"><span data-stu-id="364ad-172">The  Location attribute of the *CommandUIDefinition* element has the value . The second part of this,  `ListItem`, identifies the tab on the ribbon where the button will be placed (but that may not be the exact display name of the tab) and the third part,  , is the name of the section of the ribbon where the button will be placed.</span></span> <span data-ttu-id="364ad-173">Третья часть (`Actions`) — это имя *раздела* ленты, в который будет помещена кнопка.</span><span class="sxs-lookup"><span data-stu-id="364ad-173">The third part, `Actions`, is the name of the *section* of the ribbon where the button will be placed.</span></span>

   - <span data-ttu-id="364ad-p113">Атрибут **CommandAction** элемента **CommandUIHandler** начинается с заполнителя `~remoteAppUrl`. При развертывании кнопки он будет заменен на URL-адрес удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="364ad-p113">The  **CommandAction** attribute of the **CommandUIHandler** element begins with the placeholder `~remoteAppUrl`. This will be replaced with the URL of the remote web application when the button is deployed.</span></span>

   - <span data-ttu-id="364ad-176">В значение **CommandAction** с использованием значений заполнителей в фигурных скобках "{ }" добавлены несколько параметров запроса.</span><span class="sxs-lookup"><span data-stu-id="364ad-176">A few query parameters have been added to the **CommandAction** value with placeholder values in braces "{ }".</span></span> <span data-ttu-id="364ad-177">Эти заполнители разрешаются в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="364ad-177">These placeholders are resolved at runtime.</span></span> <span data-ttu-id="364ad-178">Обратите внимание, что один из них — идентификатор элемента списка, выбранного пользователем перед нажатием специальной кнопки на ленте.</span><span class="sxs-lookup"><span data-stu-id="364ad-178">A few query parameters have been added to the  CommandAction value with placeholder values in braces "{ }". These placeholders are resolved at runtime. Note that one of them is the ID of the list item that is selected by the user before she presses the custom button on the ribbon.</span></span>

7. <span data-ttu-id="364ad-179">В проекте **ChainStoreWeb** откройте файл **Pages/EmployeeAdder.aspx**.</span><span class="sxs-lookup"><span data-stu-id="364ad-179">In the **ChainStoreWeb** project, open the **Pages/EmployeeAdder.aspx** file.</span></span> <span data-ttu-id="364ad-180">Обратите внимание на то, что в нем нет пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="364ad-180">Notice that it doesn't have any UI.</span></span> <span data-ttu-id="364ad-181">Предполагается, что надстройка будет использовать эту страницу в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="364ad-181">The add-in is going to use this page as a kind of web service.</span></span> <span data-ttu-id="364ad-182">Это возможно, так как класс ASP.NET **System.Web.UI.Page** реализует **System.Web.IHttpHandler** и при запрашивании страницы автоматически выполняется событие **Page\_Load**.</span><span class="sxs-lookup"><span data-stu-id="364ad-182">In the  ChainStoreWeb project, open the Pages/EmployeeAdder.aspx file. Notice that it doesn't have any UI. The add-in is going to use this page as a kind of web service. This is possible because the ASP.NET **System.Web.UI.Page** class implements **System.Web.IHttpHandler** and because the **Page\_Load** event runs automatically when the page is requested.</span></span>  
 
8. <span data-ttu-id="364ad-183">Откройте файл с кодом программной части **Pages/EmployeeAdder.aspx.cs**.</span><span class="sxs-lookup"><span data-stu-id="364ad-183">Open the code-behind file **Pages/EmployeeAdder.aspx.cs**.</span></span> <span data-ttu-id="364ad-184">В нем уже есть метод, который добавляет сотрудника в удаленную базу данных `AddLocalEmployeeToCorpDB`.</span><span class="sxs-lookup"><span data-stu-id="364ad-184">The method that adds the employee to the remote database, `AddLocalEmployeeToCorpDB`, is already present.</span></span> <span data-ttu-id="364ad-185">Он использует объект **SharePointContext** для получения URL-адреса хост-сайта, который надстройка использует в качестве своего дискриминатора клиента.</span><span class="sxs-lookup"><span data-stu-id="364ad-185">It uses the **SharePointContext** object to get the host web's URL, which the add-in uses as its tenant discriminator.</span></span> <span data-ttu-id="364ad-186">Первое, что должен сделать метод **Page_Load**, — инициализировать этот объект.</span><span class="sxs-lookup"><span data-stu-id="364ad-186">The first thing the **Page_Load** method needs to do is initialize this object.</span></span> <span data-ttu-id="364ad-187">Объект создается и помещается в кэш в сеансе, когда загружается начальная страница надстройки, поэтому добавьте указанный ниже код в метод **Page_Load**.</span><span class="sxs-lookup"><span data-stu-id="364ad-187">The object is created and cached in the Session when the add-in's start page loads, so add the following code to the **Page_Load** method.</span></span> <span data-ttu-id="364ad-188">(Объект **SharePointContext** определен в файле SharePointContext.cs, который пакет "Инструменты разработчика Office для Visual Studio" создает при создании решения надстройки.)</span><span class="sxs-lookup"><span data-stu-id="364ad-188">(The **SharePointContext** object is defined in the SharePointContext.cs file that the Office Developer Tools for Visual Studio generates when the add-in solution is created.)</span></span>
    
    ```C#
      spContext = Session["SPContext"] as SharePointContext;
    ```

9. <span data-ttu-id="364ad-189">Метод `AddLocalEmployeeToCorpDB` использует имя сотрудника в качестве параметра, поэтому добавьте указанную ниже строку в метод **Page_Load**.</span><span class="sxs-lookup"><span data-stu-id="364ad-189">The  `AddLocalEmployeeToCorpDB` method takes the employee's name as a parameter, so add the following line to the **Page_Load** method. You'll create the  method in a later step.</span></span> <span data-ttu-id="364ad-190">Вы создадите метод `GetLocalEmployeeName` на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="364ad-190">You will create the  `GetLocalEmployeeName` object and  method in a later step.</span></span>
    
    ```C#
      // Read from SharePoint 
    string employeeName = GetLocalEmployeeName();
    ```

10. <span data-ttu-id="364ad-191">После этой строки добавьте вызов метода `AddLocalEmployeeToCorpDB`.</span><span class="sxs-lookup"><span data-stu-id="364ad-191">Below this line, add the call to the  `AddLocalEmployeeToCorpDB` method.</span></span>
    
    ```C#
      // Write to remote database 
    AddLocalEmployeeToCorpDB(employeeName);
    ```

11. <span data-ttu-id="364ad-p118">Добавьте в файл оператор **using** для пространства имен `Microsoft.SharePoint.Client`. (При создании проекта **ChainStoreWeb**Инструменты разработчика Office для Visual Studio включил в него сборку Microsoft.SharePoint.Client.)</span><span class="sxs-lookup"><span data-stu-id="364ad-p118">Add a **using** statement to file for the namespace `Microsoft.SharePoint.Client`. (The Office Developer Tools for Visual Studio included the Microsoft.SharePoint.Client assembly in the **ChainStoreWeb** project when it was created.)</span></span>
    
12. <span data-ttu-id="364ad-194">Теперь добавьте указанный ниже метод в класс `EmployeeAdder`.</span><span class="sxs-lookup"><span data-stu-id="364ad-194">Add the following method to the  `EmployeeAdder` class.</span></span> <span data-ttu-id="364ad-195">Клиентская объектная модель (CSOM) .NET для SharePoint подробно задокументирована на MSDN. Рекомендуем изучить ее по завершении работы с этой серией статей.</span><span class="sxs-lookup"><span data-stu-id="364ad-195">The SharePoint .NET Client-side Object Model (CSOM) is documented in detail elsewhere on MSDN, and we encourage you to explore it when you are finished with this series of articles.</span></span> <span data-ttu-id="364ad-196">Обратите внимание на то, что класс **ListItem** представляет элемент в списке SharePoint и что на значение поля в элементе можно сослаться с помощью синтаксиса "индексатора".</span><span class="sxs-lookup"><span data-stu-id="364ad-196">For this article, note that the **ListItem** class represents an item in a SharePoint list, and that the value of a field in the item can be referenced with "indexer" syntax.</span></span> <span data-ttu-id="364ad-197">Кроме того, учтите, что код ссылается на поле, используя имя **Название**, даже если вы заменили его на **Имя**.</span><span class="sxs-lookup"><span data-stu-id="364ad-197">Also notice that the code refers to the field as **Title** even though you changed the field name to **Name**.</span></span> <span data-ttu-id="364ad-198">Это происходит из-за того, что в коде необходимо ссылаться на поля, используя их *внутренние*, а не отображаемые имена.</span><span class="sxs-lookup"><span data-stu-id="364ad-198">This is because fields are always referred to in code by their *internal* name, not their display name.</span></span> <span data-ttu-id="364ad-199">Внутреннее имя поля указывается при создании поля, и его невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="364ad-199">The internal name of a field is set when the field is created and can never change.</span></span> <span data-ttu-id="364ad-200">Вы выполните `TODO1` на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="364ad-200">You will create the  `TODO1` object and  method in a later step.</span></span>
    
    ```C#
      private string GetLocalEmployeeName()
    {
        ListItem localEmployee;

        // TODO1: Initialize the localEmployee object by getting  
        // the item from SharePoint.

        return localEmployee["Title"].ToString();
    }
    ```

13. <span data-ttu-id="364ad-201">Чтобы наш код смог получить элемент списка из SharePoint, ему потребуется идентификатор этого элемента.</span><span class="sxs-lookup"><span data-stu-id="364ad-201">Our code will need the list item's ID before it can retrieve it from SharePoint. Add the following declaration to the   class just below the declaration for the  object.</span></span> <span data-ttu-id="364ad-202">Добавьте указанное ниже объявление в класс `EmployeeAdder` сразу же после объявления для объекта `spContext`.</span><span class="sxs-lookup"><span data-stu-id="364ad-202">Add the following declaration to the `EmployeeAdder` class just under the declaration for the `spContext` object.</span></span>
    
    ```C#
      private int listItemID;
    ```

14. <span data-ttu-id="364ad-203">Теперь добавьте указанный ниже метод в класс `EmployeeAdder`, чтобы получить идентификатор элемента списка из параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="364ad-203">Now add the following method to the  `EmployeeAdder` class to get the list item's ID from the query parameter.</span></span>
    
    ```C#
      private int GetListItemIDFromQueryParameter()
    {
        int result;
        Int32.TryParse(Request.QueryString["SPListItemId"], out result);
        return result;
    }
    ```

15. <span data-ttu-id="364ad-204">Чтобы инициализировать переменную `listItemID`, добавьте указанную ниже строку в метод **Page_Load** сразу же за строкой, в которой выполняется инициализация переменной `spContext`.</span><span class="sxs-lookup"><span data-stu-id="364ad-204">To initialize the  `listItemID` variable, add the following line to the **Page_Load** method just below the line that initializes the `spContext` variable.</span></span>
    
    ```C#
      listItemID = GetListItemIDFromQueryParameter();
    ```

16. <span data-ttu-id="364ad-205">В `GetLocalEmployeeName` замените `TODO1` указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="364ad-205">In the TasksCalendarWebPart class replace the displayTasks and updateTask methods with the following code:</span></span> <span data-ttu-id="364ad-206">На данный момент относитесь к этому коду как к "черному ящику", потому что сейчас нас интересует то, как заставить работать специальную кнопку.</span><span class="sxs-lookup"><span data-stu-id="364ad-206">For the time being, just treat this code as a black box while we concentrate on getting the custom button working.</span></span> <span data-ttu-id="364ad-207">Мы более подробно рассмотрим этот код в следующей статье серии, которая будет целиком посвящена клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="364ad-207">In the  , replace the   with the following code. For the time being, just treat this code as a black box while we concentrate on getting the custom button working. We'll learn more about this code in the next article in this series, which is all about the SharePoint client-side object model.</span></span>
    
    ```C#
      using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
        localEmployee = localEmployeesList.GetItemById(listItemID);
        clientContext.Load(localEmployee);
        clientContext.ExecuteQuery();
    }

    ```

   <span data-ttu-id="364ad-208">Теперь весь метод должен выглядеть, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="364ad-208">The entire method should now look like the following.</span></span>

    ```C#
      private string GetLocalEmployeeName()
     {
         ListItem localEmployee;

         using (var clientContext = spContext.CreateUserClientContextForSPHost())
         {
             List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
             selectedLocalEmployee = localEmployeesList.GetItemById(listItemID);
             clientContext.Load(selectedLocalEmployee);
             clientContext.ExecuteQuery();
         }
         return localEmployee["Title"].ToString();
     }
     ```

17. <span data-ttu-id="364ad-209">Страница EmployeeAdder не должна отрисовываться, поэтому добавьте указанный ниже код в метод **Page_Load** в качестве последней строки.</span><span class="sxs-lookup"><span data-stu-id="364ad-209">The EmployeeAdder page should not actually render, so add the following as the last line in the  **Page_Load** method. This will redirect the browser back to the list view page for the Local Employees list.</span></span> <span data-ttu-id="364ad-210">Она будет перенаправлять браузер обратно на страницу представления списка для списка **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="364ad-210">This redirects the browser back to the list view page for the **Local Employees** list.</span></span>
    
    ```C#
      // Go back to the Local Employees page
    Response.Redirect(spContext.SPHostUrl.ToString() + "Lists/LocalEmployees/AllItems.aspx", true);

    ```

   <span data-ttu-id="364ad-211">Теперь весь метод **Page_Load** должен выглядеть, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="364ad-211">The whole **Page_Load** method should now look like the following.</span></span>

    ```C#
          protected void Page_Load(object sender, EventArgs e)
        {
            spContext = Session["SPContext"] as SharePointContext;
            listItemID = GetListItemIDFromQueryParameter();

            // Read from SharePoint
            string employeeName = GetLocalEmployeeName();

            // Write to remote database
            AddLocalEmployeeToCorpDB(employeeName);

            // Go back to the preceding page
            Response.Redirect(spContext.SPHostUrl.ToString() + "Lists/LocalEmployees/AllItems.aspx", true);
        }
    ```


## <a name="request-permission-to-read-the-host-web-list"></a><span data-ttu-id="364ad-212">Запрашивание разрешения на чтение списка на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="364ad-212">Request permission to read the host web list</span></span>

<span data-ttu-id="364ad-213">Как вы уже видели, при установке надстройки SharePoint предлагает предоставить ей разрешения на доступ к хост-сайту.</span><span class="sxs-lookup"><span data-stu-id="364ad-213">As you have seen, SharePoint prompts you to grant the add-in permissions to the host web when it is installed.</span></span> <span data-ttu-id="364ad-214">Каждый раз, когда вы нажимали клавишу F5, выполнялась переустановка надстройки.</span><span class="sxs-lookup"><span data-stu-id="364ad-214">You have been re-installing the add-in every time you select F5.</span></span> <span data-ttu-id="364ad-215">До настоящего момента у надстройки были только минимально необходимые разрешения, но методу `GetLocalEmployeeName` необходимо разрешение на чтение списков хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="364ad-215">So far, the add-in has only needed minimal permissions, but the `GetLocalEmployeeName` method requires permission to read the lists of the host website.</span></span> <span data-ttu-id="364ad-216">Надстройка использует свой манифест, чтобы сообщить SharePoint, какие разрешения ей необходимы.</span><span class="sxs-lookup"><span data-stu-id="364ad-216">The add-in uses its add-in manifest to tell SharePoint what permissions it needs.</span></span> <span data-ttu-id="364ad-217">Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="364ad-217">Follow these steps.</span></span>

1. <span data-ttu-id="364ad-218">В **обозревателе решений** откройте файл AppManifest.xml в проекте **ChainStore** (файл называется AppManifest и в нем использовано слово App, потому что ранее надстройки назывались приложениями).</span><span class="sxs-lookup"><span data-stu-id="364ad-218">In  **Solution Explorer**, open the AppManifest.xml file in the  **ChainStore** project. (The file is called AppManifest because add-ins used to be called "apps".) The manifest designer opens.</span></span> <span data-ttu-id="364ad-219">Откроется конструктор манифестов.</span><span class="sxs-lookup"><span data-stu-id="364ad-219">The application designer opens.</span></span>

2. <span data-ttu-id="364ad-220">Откройте вкладку **Разрешения** и щелкните пустую ячейку в столбце **Область**. Затем в раскрывающемся списке выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="364ad-220">Open the  **Permissions** tab and click the empty cell under the **Scope** column; and then select **List** from the drop down.</span></span>

3. <span data-ttu-id="364ad-221">Щелкнув пустую ячейку в столбце **Разрешение**, в раскрывающемся списке выберите **Read**.</span><span class="sxs-lookup"><span data-stu-id="364ad-221">In the  **Permission** field, select **Read** from the drop down.</span></span>

4. <span data-ttu-id="364ad-222">Оставьте столбец **Свойства** пустым и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="364ad-222">Leave the  **Properties** field empty and save the file. The Permission tab should look similar to the following:</span></span> <span data-ttu-id="364ad-223">Вкладка **Разрешения** должна иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="364ad-223">Choose  OK. The  **Permissions** tab should now look similar to the following:</span></span>

   <span data-ttu-id="364ad-224">*Рис. 2. Вкладка "Разрешения"*</span><span class="sxs-lookup"><span data-stu-id="364ad-224">*Figure 2. Permissions tab*</span></span>

   ![Вкладка "Разрешения" конструктора манифеста надстройки, где в качестве области задан список, а в качестве разрешения — Read.](../images/8dd2a25f-103a-42af-aa88-c8ec796315db.PNG)


## <a name="run-the-add-in-and-test-the-button"></a><span data-ttu-id="364ad-226">Запуск надстройки и тестирование кнопки</span><span class="sxs-lookup"><span data-stu-id="364ad-226">Run the add-in and test the button</span></span>

1. <span data-ttu-id="364ad-227">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="364ad-227">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="364ad-228">Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express.</span><span class="sxs-lookup"><span data-stu-id="364ad-228">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="364ad-229">Кроме того, он выполняет временную установку надстройки на вашем тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="364ad-229">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="364ad-230">Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="364ad-230">You are prompted to grant permissions to the add-in before its start page opens.</span></span> <span data-ttu-id="364ad-231">В этот раз будет отображен раскрывающийся список, в котором вы можете выбрать список, данные из которого необходимо считывать приложению, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="364ad-231">This time the prompt has a drop-down where you select the list that the app needs to read as seen in the following screenshot.</span></span> 
  
   <span data-ttu-id="364ad-232">*Рис. 3. Запрос на предоставление разрешения надстройке SharePoint*</span><span class="sxs-lookup"><span data-stu-id="364ad-232">*Figure 3. SharePoint add-in permission prompt*</span></span>

   ![Запрос на предоставление разрешения надстройке SharePoint со списком "Local Employees" (Местные сотрудники), выбранным в раскрывающемся списке "Разрешить читать элементы в списке"](../images/84e8b42c-4800-4947-acbd-21c6f096f4ea.PNG)

2. <span data-ttu-id="364ad-234">В списке выберите пункт **Local Employees** (Местные сотрудники), а затем нажмите кнопку **Сделать доверенным**.</span><span class="sxs-lookup"><span data-stu-id="364ad-234">Choose  **Local Employees** from the list and then click **Trust it**.</span></span>

3. <span data-ttu-id="364ad-235">Когда откроется начальная страница надстройки, выберите **Вернуться на сайт** на размещенном в верхней части элементе управления хрома.</span><span class="sxs-lookup"><span data-stu-id="364ad-235">When the add-in's start page opens, select the  **Back to Site** link on the chrome control at the top.</span></span>

4. <span data-ttu-id="364ad-236">На домашней странице веб-сайта выберите **Содержимое сайта** > **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="364ad-236">From the website's home page, go to **Site Contents** > **Local Employees**.</span></span> <span data-ttu-id="364ad-237">Откроется страница представления списка.</span><span class="sxs-lookup"><span data-stu-id="364ad-237">The list view page opens.</span></span>

5. <span data-ttu-id="364ad-238">Добавьте несколько сотрудников в список.</span><span class="sxs-lookup"><span data-stu-id="364ad-238">Add a few employees to the list.  Do not check the  Added to Corporate DB checkbox.</span></span> <span data-ttu-id="364ad-239">*Не устанавливайте флажок __Added to Corporate DB__ (Добавлено в корпоративную базу данных).*</span><span class="sxs-lookup"><span data-stu-id="364ad-239">*Do not select the __Added to Corporate DB__ check box.*</span></span> 

6. <span data-ttu-id="364ad-240">На ленте откройте вкладку **Элементы**. В разделе **Действия** вкладки есть специальная кнопка **Add to Corporate DB** (Добавить в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="364ad-240">On the ribbon, open the  **Items** tab. In the **Actions** section of the tab, is the custom button **Add to Corporate DB**.</span></span>

7. <span data-ttu-id="364ad-241">Выберите элемент в списке.</span><span class="sxs-lookup"><span data-stu-id="364ad-241">Select an item from the list box.</span></span> <span data-ttu-id="364ad-242">Страница и лента должны иметь примерно следующий вид:</span><span class="sxs-lookup"><span data-stu-id="364ad-242">Select an item on the list. The page and ribbon should look similar to the following:</span></span>

   <span data-ttu-id="364ad-243">*Рис. 4. Список местных сотрудников*</span><span class="sxs-lookup"><span data-stu-id="364ad-243">*Figure 4. Local Employees list*</span></span>  

   ![Список местных сотрудников.](../images/797a5ceb-7291-4b62-8075-2bb6a1b8e8a1.PNG)

8. <span data-ttu-id="364ad-247">Выбрав элемент в списке, нажмите кнопку **Add To Corporate DB** (Добавить в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="364ad-247">After selecting an item in the list, select **Add to Corporate DB**.</span></span> 

9. <span data-ttu-id="364ad-248">Вам покажется, что страница перезагружается, так как метод **Page_Load** страницы EmployeeAdder выполняет перенаправление на нее.</span><span class="sxs-lookup"><span data-stu-id="364ad-248">The page will seem to reload because the  **Page_Load** method of the EmployeeAdder page redirects back to it.</span></span>

10. <span data-ttu-id="364ad-249">Дважды нажмите кнопку "Назад" в браузере, чтобы вернуться на начальную страницу надстройки.</span><span class="sxs-lookup"><span data-stu-id="364ad-249">Use the browser's back button twice to go back to the add-in's start page.</span></span> 

11. <span data-ttu-id="364ad-250">Нажмите кнопку **Show Employees** (Показать сотрудников), после чего список сотрудников будет заполнен добавленными вами сотрудниками.</span><span class="sxs-lookup"><span data-stu-id="364ad-250">Click  **Show Employees** and the list of employees will be populated with the employee that you added. It should look similar to the following:</span></span> <span data-ttu-id="364ad-251">Он должен выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="364ad-251">The calendar should look similar to the following:</span></span>

   <span data-ttu-id="364ad-252">*Рис. 5. Список сотрудников организации на начальной странице надстройки*</span><span class="sxs-lookup"><span data-stu-id="364ad-252">*Figure 5. Corporate employees list on the add-in start page*</span></span> 

   ![Список сотрудников организации на начальной странице надстройки, где отображается сотрудник, выбранный на предыдущем этапе.](../images/4a300a4e-f479-4f63-b536-6315c5d9ba4d.PNG)

12. <span data-ttu-id="364ad-254">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="364ad-254">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="364ad-255">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="364ad-255">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

13. <span data-ttu-id="364ad-256">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="364ad-256">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="364ad-257">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="364ad-257">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="364ad-258">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="364ad-258">Next steps</span></span>
<span data-ttu-id="364ad-259"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="364ad-259"></span></span>

<span data-ttu-id="364ad-260">В следующей статье мы немного отвлечемся от программирования и [ознакомимся с клиентской объектной моделью SharePoint](get-a-quick-overview-of-the-sharepoint-object-model.md).</span><span class="sxs-lookup"><span data-stu-id="364ad-260">In the next article, we'll take a brief break from coding for an overview of the SharePoint client-side object model: [Get a quick overview of the SharePoint object model](get-a-quick-overview-of-the-sharepoint-object-model.md).</span></span>
 

 

