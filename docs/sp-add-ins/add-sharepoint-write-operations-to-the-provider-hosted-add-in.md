# <a name="add-sharepoint-write-operations-to-the-provider-hosted-add-in"></a><span data-ttu-id="fb8dd-101">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="fb8dd-101">Add SharePoint write operations to the provider-hosted add-in</span></span>
<span data-ttu-id="fb8dd-102">Узнайте, как записывать данные в SharePoint в надстройке SharePoint, размещаемой у поставщика.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-102">Learn how to write data to SharePoint in a provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="fb8dd-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="fb8dd-p102">Это пятая часть серии статей, посвященных основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p102">Learn how to write data to SharePoint in a provider-hosted SharePoint Add-in. This is the fifthin a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="fb8dd-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="fb8dd-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="fb8dd-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="fb8dd-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [<span data-ttu-id="fb8dd-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="fb8dd-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="fb8dd-111">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="fb8dd-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model)
    
 

 <span data-ttu-id="fb8dd-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий на странице [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeSharePointWriteOps.sln.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeSharePointWriteOps.sln file.</span></span>
 

<span data-ttu-id="fb8dd-114">В этой статье мы вернемся к написанию кода и добавим несколько функций, которые записывают данные в надстройку SharePoint Chain Store.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-114">In this article we get back to coding by adding some functions that write data to the Chain Store SharePoint Add-in.</span></span>
 

## <a name="change-a-column-value-on-a-sharepoint-list-item"></a><span data-ttu-id="fb8dd-115">Изменение значения столбца в элементе списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="fb8dd-115">Change a column value on a SharePoint list item</span></span>

<span data-ttu-id="fb8dd-p104">В нашей надстройке имеется настраиваемая кнопка ленты, которая добавляет в корпоративную базу данных сотрудника из списка **Local Employees** магазина в Гонконге. Тем не менее пользователю приходится вручную изменять значение поля **Added to Corporate DB** на "Yes". Давайте добавим код, который будет делать это автоматически.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p104">Our add-in has a custom ribbon button that adds an employee from the Hong Kong store's **Local Employees** list to the corporate database. But the user has to remember to manually change the value of the **Added to Corporate DB** field toYes. Let's add code to do that automatically.</span></span>
 

 

 <span data-ttu-id="fb8dd-p105">**Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений**, выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p105">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
 


1. <span data-ttu-id="fb8dd-122">В **обозревателе решений** откройте файл EmployeeAdder.cs.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-122">In **Solution Explorer**, open the EmployeeAdder.cs file.</span></span>
    
 
2. <span data-ttu-id="fb8dd-p106">Добавьте указанную ниже строку в метод **Page_Load** между вызовами метода `AddLocalEmployeeToCorpDB` и метода **Response.Redirect**. Вы создадите метод `SetLocalEmployeeSyncStatus` на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p106">Add the following line to the **Page_Load** methodbetween the call of `AddLocalEmployeeToCorpDB` and the call of **Response.Redirect**. You will create the  `SetLocalEmployeeSyncStatus` method in the next step.</span></span>
    
```C#
  // Write to SharePoint 
SetLocalEmployeeSyncStatus();
```

3. <span data-ttu-id="fb8dd-p107">Добавьте указанный ниже новый метод в класс `EmployeeAdder`. Обратите внимание на указанные ниже особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p107">Add the following new method to the  `EmployeeAdder` class. Note the following about this code:</span></span>
    
      - <span data-ttu-id="fb8dd-p108">Внутреннее имя поля **Added to Corporate DB** (Добавлено в корпоративную базу данных) выглядит довольно странно. Это связано с тем, что внутренние имена полей не должны содержать пробелы. Когда пользователь создает поле с пробелами в отображаемом имени, при задании внутреннего имени SharePoint заменяет каждый пробел строкой _x0020_. Из-за этого строка "Added to Employee DB" (Добавлено в базу данных сотрудников) превратилась в строку "Added_x0020_to_x0020_Corporate_x0020_DB". Длина внутренних имен не должна превышать 32 символов, поэтому имя усечено до строки "Added_x0020_to_x0020_Corporate_x".</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p108">The internal name for the **Added to Corporate DB** field is odd-looking. Internal field names cannot contain spaces, so when a user creates a field with spaces in its display name, SharePoint substitutes the string "_x0020_" for each space when it sets the internal name. This turns "Added to Employee DB" into "Added_x0020_to_x0020_Corporate_x0020_DB". Internal names cannot be more than 32 characters, so the name is truncated to just "Added_x0020_to_x0020_Corporate_x".</span></span>
    
 
  - <span data-ttu-id="fb8dd-131">Несмотря на то что в пользовательском интерфейсе SharePoint столбец **Added to Corporate DB** (Добавлено в корпоративную базу данных) называется полем "Yes/No" (Да или нет), на самом деле он имеет логический тип, поэтому его значение — **true**, а не "Yes" (Да).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-131">Although the **Added to Corporate DB** column is called a "Yes/No" field in the SharePoint UI, it is really a boolean, so its value is set to **true**, not "Yes".</span></span>
    
 
  - <span data-ttu-id="fb8dd-p109">Для фиксации изменений в базе данных контента SharePoint должен вызвать метод **Update** класса **ListItem**. Существует общее, но не совсем универсальное правило, согласно которому при изменении значения свойства объекта, хранящегося в базах данных SharePoint, необходимо вызвать метод **Update** объекта.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p109">The **Update** method of the **ListItem** class must be called to commit the changes to SharePoint's content database. It is a general, but not quite universal, rule that when you change a property value of an object that is stored in the SharePoint databases, you must call the object's **Update** method.</span></span>
    
 

```C#
  private void SetLocalEmployeeSyncStatus()
{
    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
        ListItem selectedLocalEmployee = localEmployeesList.GetItemById(listItemID);
        selectedLocalEmployee["Added_x0020_to_x0020_Corporate_x"] = true;
        selectedLocalEmployee.Update();
        clientContext.ExecuteQuery();
    }
}
```


## <a name="request-permission-to-write-to-the-host-web-list"></a><span data-ttu-id="fb8dd-134">Запрос разрешения на запись в список хост-сайта</span><span class="sxs-lookup"><span data-stu-id="fb8dd-134">Request permission to write to the host web list</span></span>

<span data-ttu-id="fb8dd-p110">Так как теперь надстройка не только считывает данные из списка, но и записывает их туда, нам необходимо расширить разрешения для надстройки с "Чтение" до "Запись". Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p110">Since the add-in is now writing to the list as well as reading it, we need to escalate the permissions that the add-in requests from Read to Write. Follow these steps.</span></span>
 

 

1. <span data-ttu-id="fb8dd-137">В **обозревателе решений** откройте файл AppManifest.xml проекта **ChainStore**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-137">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>
    
 
2. <span data-ttu-id="fb8dd-138">Откройте вкладку **Разрешения** и в поле **Разрешение** в раскрывающемся списке выберите **Запись**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-138">Open the **Permissions** tab and in the **Permission** field, select **Write** from the drop down.</span></span>
    
 
3. <span data-ttu-id="fb8dd-139">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-139">Save the file.</span></span> 
    
 

## <a name="run-the-add-in-and-test-the-button"></a><span data-ttu-id="fb8dd-140">Запуск надстройки и тестирование кнопки</span><span class="sxs-lookup"><span data-stu-id="fb8dd-140">Run the add-in and test the button</span></span>


 

 

1. <span data-ttu-id="fb8dd-p111">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p111">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span> 
    
 
2. <span data-ttu-id="fb8dd-145">В форме разрешений выберите из списка пункт **Local Employees** (Локальные сотрудники), а затем щелкните **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-145">On the permission form, choose **Local Employees** from the list and then click **Trust it**.</span></span>
    
 
3. <span data-ttu-id="fb8dd-146">Когда откроется начальная страница надстройки, на расположенном в верхней части элементе управления хрома нажмите кнопку **Вернуться на сайт**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-146">When the add-in's start page opens, click **Back to Site** on the chrome control at the top.</span></span>
    
 
4. <span data-ttu-id="fb8dd-p112">На домашней странице веб-сайта выберите пункты **Контент сайта | Local Employees**. Откроется страница представления списка.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p112">From the website's home page navigate to **Site Contents | Local Employees**. The list view page opens.</span></span>
    
 
5. <span data-ttu-id="fb8dd-149">Если в списке нет сотрудников, для которых в столбце **Added to Corporate DB** (Добавлено в корпоративную базу данных) указано значение **No** (Нет), добавьте в список еще одного сотрудника и *не устанавливайте флажок **Added to Corporate DB** (Добавлено в корпоративную базу данных).*</span><span class="sxs-lookup"><span data-stu-id="fb8dd-149">If there are no employees on the list with **No** in the **Added to Corporate DB** column, add an employee to the list, and *do not check the **Added to Corporate DB** checkbox.*</span></span> 
    
 
6. <span data-ttu-id="fb8dd-p113">На ленте откройте вкладку **Элементы**. В разделе **Действия** вы увидите настраиваемую кнопку **Add to Corporate DB** (Добавить в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p113">On the ribbon, open the **Items** tab. In the **Actions** section of the tab, is the custom button **Add to Corporate DB**.</span></span>
    
 
7. <span data-ttu-id="fb8dd-152">В списке выберите сотрудника, для которого в столбце **Added to Corporate DB** (Добавлено в корпоративную базу данных) задано значение **No** (Нет).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-152">Select an employee on the list that has **No** in the **Added to Corporate DB** column.</span></span>
    
 
8. <span data-ttu-id="fb8dd-p114">Нажмите кнопку **Add to Corporate DB** (Добавить в корпоративную базу данных). * **Перед этим необходимо выбрать элемент!***</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p114">Press the **Add to Corporate DB** button. * **An item must be selected first!***</span></span> 
    
 
9. <span data-ttu-id="fb8dd-p115">Страница перезагрузится, так как метод **Page_Load** страницы EmployeeAdder выполнит перенаправление на нее. В итоге значение поля **Added to Corporate DB** (Добавлено в корпоративную базу данных) для сотрудника изменится на **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p115">The page will seem to reload because the **Page_Load** method of the EmployeeAdder page redirects back to it. The value of the **Added to Corporate DB** field for the employee has changed to **Yes**.</span></span>
    
     <span data-ttu-id="fb8dd-p116">**Примечание.** Есть ли у нас какая-нибудь защита, не позволяющая пользователю вручную изменить значение поля **Added to Corporate DB** (Добавлено в корпоративную базу данных) и рассогласовать данные в списке и в корпоративной базе данных? На данный момент такой защиты нет. Мы решим эту проблему в одной из следующих статей серии.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p116">**Note** What prevents a user from manually changing the value **Added to Corporate DB** in a way that makes the list and the corporate database inconsistent? Nothing does at the moment. You'll get the solution to this problem in a later article of this series.</span></span>
10. <span data-ttu-id="fb8dd-p117">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p117">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
11. <span data-ttu-id="fb8dd-162">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-162">Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## <a name="create-a-new-custom-list-on-the-host-website"></a><span data-ttu-id="fb8dd-163">Создание настраиваемого списка на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="fb8dd-163">Create a new custom list on the host website</span></span>

<span data-ttu-id="fb8dd-p118">Теперь нам необходимо усовершенствовать надстройку Chain Store и сделать так, чтобы можно было создавать элементы, а не просто изменять поля существующих элементов. А именно, при размещении нового заказа на корпоративном уровне в список SharePoint должен автоматически добавляться элемент, который предупредит местных сотрудников о предстоящей отгрузке. Этот список называется **Expected Shipments**. Вы создадите его, выполнив указанные ниже действия. В одной из следующих статей этой серии вы узнаете, как программным способом добавить настраиваемый список на хост-сайт, но сейчас вы добавите его вручную.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p118">The next improvement to the Chain Store add-in is to create new items in a list, instead of merely changing a field in an existing item. Specifically, when a new order is placed at the corporate level, an item is automatically created in a SharePoint list that alerts local employees to expect a shipment. The list is called **Expected Shipments** and you create it with the steps below. In a later article in this series, you'll learn how to programmatically add a custom list to a host website, but for now you'll add this one manually.</span></span>
 

 

1. <span data-ttu-id="fb8dd-168">На начальной странице магазина Fabrikam в Гонконге выберите пункты **Контент сайта | Добавить надстройку | Настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-168">From the home page of the Fabrikam Hong Kong Store, navigate to **Site Contents | add an add-in | Custom List**.</span></span> 
    
 
2. <span data-ttu-id="fb8dd-169">В диалоговом окне **Добавление настраиваемого списка** укажите имя "Expected Shipments" (Ожидаемые поставки) и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-169">In the **Adding Custom List** dialog, specifyExpected Shipments as the name and press **Create**.</span></span> 
    
 
3. <span data-ttu-id="fb8dd-170">На странице **Контент сайта** откройте список **Expected Shipments** (Ожидаемые поставки).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-170">On the **Site Contents** page, open the **Expected Shipments** list.</span></span>
    
 
4. <span data-ttu-id="fb8dd-171">Откройте вкладку **Список** на ленте, а затем нажмите кнопку **Параметры списка**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-171">Open the **List** tab on the ribbon, and then click the **List Settings** button.</span></span>
    
 
5. <span data-ttu-id="fb8dd-172">В разделе **Столбцы** на странице **Параметры списка** выберите столбец **Title** (Заголовок).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-172">In the **Columns** section of the **List Settings** page, click the **Title** column.</span></span>
    
 
6. <span data-ttu-id="fb8dd-173">В форме **Изменение столбца** замените значение "Title" (Заголовок) в поле **Имя столбца** на "Product" (Продукт), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-173">In the **Edit Column** form, change the **Column name** from Title toProduct; and then click **OK**.</span></span>
    
 
7. <span data-ttu-id="fb8dd-174">На странице **Параметры** нажмите кнопку **Создать столбец**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-174">On the **Settings** page, click **Create column**.</span></span>
    
 
8. <span data-ttu-id="fb8dd-p119">В предыдущей статье этой серии вы узнали, как создавать настраиваемые столбцы для списка. Добавьте четыре столбца для списка **Expected Shipments** (Ожидаемые поставки), используя значения из указанной ниже таблицы. Для всех остальных параметров оставьте значения, используемые по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p119">In a previous article of this series, you learned how to create custom columns for a list. For the **Expected Shipments** list, add four columns, using the values in the following table. Leave all other settings at their defaults.</span></span>
    

|<span data-ttu-id="fb8dd-178">**Имя столбца**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-178">**Column name**</span></span>|<span data-ttu-id="fb8dd-179">**Тип**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-179">**Type**</span></span>|<span data-ttu-id="fb8dd-180">**Обязательный?**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-180">**Required**</span></span>|<span data-ttu-id="fb8dd-181">**Значение, используемое по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-181">**Default value**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="fb8dd-182">"Supplier" (Поставщик)</span><span class="sxs-lookup"><span data-stu-id="fb8dd-182">Supplier</span></span>|<span data-ttu-id="fb8dd-183">**Однострочный текст**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-183">**Single line of text**</span></span>|<span data-ttu-id="fb8dd-184">Необязательный</span><span class="sxs-lookup"><span data-stu-id="fb8dd-184">not required</span></span>|<span data-ttu-id="fb8dd-185">нет</span><span class="sxs-lookup"><span data-stu-id="fb8dd-185">none</span></span>|
|<span data-ttu-id="fb8dd-186">"Quantity" (Количество)</span><span class="sxs-lookup"><span data-stu-id="fb8dd-186">Quantity</span></span>|<span data-ttu-id="fb8dd-187">**Число**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-187">**Number**</span></span>|<span data-ttu-id="fb8dd-188">Обязательный</span><span class="sxs-lookup"><span data-stu-id="fb8dd-188">Required</span></span>|<span data-ttu-id="fb8dd-189">1</span><span class="sxs-lookup"><span data-stu-id="fb8dd-189">1</span></span>|
|<span data-ttu-id="fb8dd-190">"Arrived" (Доставлено)</span><span class="sxs-lookup"><span data-stu-id="fb8dd-190">Arrived</span></span>|<span data-ttu-id="fb8dd-191">**Да или нет**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-191">**Yes/No**</span></span>|<span data-ttu-id="fb8dd-192">Необязательный</span><span class="sxs-lookup"><span data-stu-id="fb8dd-192">not required</span></span>|<span data-ttu-id="fb8dd-193">Нет</span><span class="sxs-lookup"><span data-stu-id="fb8dd-193">No</span></span>|
|<span data-ttu-id="fb8dd-194">"Added to Inventory" (Добавлено в инвентарь)</span><span class="sxs-lookup"><span data-stu-id="fb8dd-194">Added to Inventory</span></span>|<span data-ttu-id="fb8dd-195">**Да или нет**</span><span class="sxs-lookup"><span data-stu-id="fb8dd-195">**Yes/No**</span></span>|<span data-ttu-id="fb8dd-196">Необязательный</span><span class="sxs-lookup"><span data-stu-id="fb8dd-196">not required</span></span>|<span data-ttu-id="fb8dd-197">Нет</span><span class="sxs-lookup"><span data-stu-id="fb8dd-197">No</span></span>|
9. <span data-ttu-id="fb8dd-p120">После создания столбцов на странице параметров списка нажмите кнопку **Контент сайта**. Откроется страница **Контент сайта**. Откройте список **Expected Shipments** (Ожидаемые поставки).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p120">After you have created the columns, on the list settings page, click **Site Contents** to open the **Site Contents** page. Open the **Expected Shipments** list.</span></span>
    
 
10. <span data-ttu-id="fb8dd-p121">Нажмите кнопку **Создать элемент**. Форма создания элемента должна иметь точно такой же вид, как показано ниже, включая две звездочки, обозначающие обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p121">Click **new item**. The item creation form should look exactly like the following, including the two asterisks that indicate required fields.:</span></span>
    
  ![Форма создания элемента для списка "Ожидаемые поставки" с полями "Продукт", "Поставщик", "Количество", "Поступил" и "Добавлен в перечень". Звездочки рядом с заголовками "Продукт" и "Количество" и значение по умолчанию 1 (один) для поля "Количество".](../../images/e552b5c9-8baa-4e53-9295-4d85a79d7734.PNG)
 

 

 
11. <span data-ttu-id="fb8dd-205">Мы не будем создавать элементы этого списка вручную, поэтому нажмите кнопку **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-205">We don't want to manually create items on this list, so click **Cancel**.</span></span>
    
 

## <a name="insert-an-item-into-a-sharepoint-list"></a><span data-ttu-id="fb8dd-206">Вставка элемента в список SharePoint</span><span class="sxs-lookup"><span data-stu-id="fb8dd-206">Insert an item into a SharePoint list</span></span>

<span data-ttu-id="fb8dd-207">Теперь добавьте в надстройку функцию, которая при размещении заказа для магазина в Гонконге на корпоративном уровне создает элемент в списке **Expected Shipments** (Ожидаемые поставки).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-207">Now you add a function to the add-in that creates an item in the **Expected Shipments** list whenever an order for the Hong Kong store is placed at the corporate level.</span></span>
 

 

1. <span data-ttu-id="fb8dd-208">В **обозревателе решений** откройте файл OrderForm.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-208">In **Solution Explorer**, open the OrderForm.aspx.cs file.</span></span>
    
 
2. <span data-ttu-id="fb8dd-209">В начало файла добавьте оператор **using** для **Microsoft.SharePoint.Client**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-209">Add a **using** statement for **Microsoft.SharePoint.Client** to the top of the file.</span></span>
    
 
3. <span data-ttu-id="fb8dd-p123">В метод `btnCreateOrder_Click`, сразу под вызовом `CreateOrder`, добавьте следующую строку. Вы создадите метод CreateExpectedShipment на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p123">In the  `btnCreateOrder_Click` method, add the following line just below the call to `CreateOrder`. You'll create the CreateExpectedShipment method in the next step.</span></span>
    
```C#
  CreateExpectedShipment(txtBoxSupplier.Text, txtBoxItemName.Text, quantity);
```

4. <span data-ttu-id="fb8dd-p124">Добавьте в класс `OrderForm` приведенный ниже метод. Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p124">Add the following method to the  `OrderForm` class. Note the following about this code:</span></span>
    
      - <span data-ttu-id="fb8dd-p125">Для создания объекта **ListItem** мы не будем использовать конструктор, исходя из соображений производительности. Объект **ListItem** имеет большое количество свойств (со значениями, используемыми по умолчанию). При использовании конструктора весь объект будет включен в сообщение XML, которое метод **ExecuteQuery** отправляет на сервер. **ListItemCreationInformation** — это "легковесный" объект, содержащий только минимальное количество значений, которые не используются по умолчанию и необходимы серверу для создания объекта **ListItem**. Может оказаться, что существует строка, которая создает объект **ListItem**, но при вызове этой строки происходит только добавление XML-разметки в сообщение, отправляемое на сервер. Объект **ListItem** создается на сервере.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p125">A **ListItem** object is not created with a constructor. This is for performance reasons. A **ListItem** object has many properties (with default values). If a constructor is used, the entire object would be included in the XML message that the **ExecuteQuery** method sends to the server. The **ListItemCreationInformation** object is a lightweight object that only contains the minimal non-default values that the server needs to create a **ListItem** object. It may appear that there is a line that creates a **ListItem** object, but recall that this line only adds some XML markup to a message that is sent to the server. The **ListItem** object is created there on the server.</span></span>
    
 
  - <span data-ttu-id="fb8dd-221">Нет необходимости отправлять объект **ListItem** обратно клиенту, поэтому метод **ClientContext.Load** не вызывается.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-221">There is no need to bring the **ListItem** object back down to the client, so there is no call to **ClientContext.Load** method.</span></span>
    
 
  - <span data-ttu-id="fb8dd-222">В коде не нужно явно задавать значения полей **Arrived** (Доставлено) или **Added to Inventory** (Добавлено в инвентарь), так как им присвоено значение "No" (Нет), используемое по умолчанию, то есть именно то, что нам нужно.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-222">The code does not need to explicitly set the **Arrived** or **Added to Inventory** fields because they have default values of "No", which is what we want.</span></span>
    
 

```
  private void CreateExpectedShipment(string supplier, string product, UInt16 quantity)
{
    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List expectedShipmentsList = clientContext.Web.Lists.GetByTitle("Expected Shipments");
        ListItemCreationInformation itemCreateInfo = new ListItemCreationInformation();
        ListItem newItem = expectedShipmentsList.AddItem(itemCreateInfo);
        newItem["Title"] = product;
        newItem["Supplier"] = supplier;
        newItem["Quantity"] = quantity;
        newItem.Update();
        clientContext.ExecuteQuery();
    }
}
```


## <a name="checking-for-deleted-components"></a><span data-ttu-id="fb8dd-223">Проверка удаленных компонентов</span><span class="sxs-lookup"><span data-stu-id="fb8dd-223">Checking for deleted components</span></span>

<span data-ttu-id="fb8dd-p126">Любой пользователь с привилегиями владельца списка SharePoint может удалить этот список. Если список развернут надстройкой на хост-сайте, то его может удалить и владелец хост-сайта. Это может случиться, если владелец решит, что ему не нужна функциональность, предоставляемая списком. (Если затем владелец изменит свое решение, то можно будет восстановить список из корзины SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p126">Anyone with list owner privileges for a SharePoint list can delete the list. And if the list is deployed to the host web by an add-in, the website owner of the host web can delete it. That may happen if the owner decides to do without the functionality provided by the list. (It can be restored from the SharePoint Recycle Bin if the owner changes his mind.)</span></span> 
 

 
<span data-ttu-id="fb8dd-p127">Работа метода  `CreateExpectedShipment` зависит от того, существует ли список **Expected Shipments** (Ожидаемые отгрузки). Предположим, что владелец веб-сайта решил удалить список. Позже, при добавлении заказа с помощью **формы заказа** надстройки вызывается метод `CreateExpectedShipment`, который создаст исключение с сообщением о том, что на веб-сайте SharePoint нет списка **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p127">The  `CreateExpectedShipment` method depends on the existence of the **Expected Shipments** list. Suppose a website owner decided to delete the list. Later, when an order is added with the add-in's **Order Form**, the  `CreateExpectedShipment` is called and will throw an exception whose message says that there's no **Expected Shipments** list on the SharePoint website.</span></span>
 

 
<span data-ttu-id="fb8dd-p128">Возможно, вы захотите, чтобы перед совершением каких-либо действий со списком  `expectedShipmentsList` метод проверял, не пуст ли этот список. Когда вы работаете с CSOM, вам *не*  удастся выполнить эту проверку с помощью простой структуры, например указанной ниже.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p128">You might want the method to check the  `expectedShipmentsList` for nullity before it does anything with it. When you are working with CSOM, you can *not*  make this check with a simple structure like this:</span></span>
 

 
 `if (expectedShipmentsList != null) { ... }`
 

 
<span data-ttu-id="fb8dd-p129">Вместо этого вам придется использовать особый класс CSOM, называемый **ConditionalScope**. Это связано с системой пакетной обработки CSOM, о которой мы упоминали в предыдущей статье этой серии. (См. раздел [Среда выполнения и пакетная обработка в клиенте](get-a-quick-overview-of-the-sharepoint-object-model#CSOMBatching)). Класс **ConditionalScope** и система пакетной обработки являются сложными темами, которые выходят за рамки данной серии статей для начинающих, но по завершении изучения этой серии вам следует ознакомиться с соответствующей документацией MSDN.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p129">Instead, you need to use a special CSOM class called **ConditionalScope**. The reasons for this are connected to CSOM's batching system, which was mentioned in the previous article in this series. (See  [Client-side runtime and batching](get-a-quick-overview-of-the-sharepoint-object-model#CSOMBatching)). **ConditionalScope** and the batching system are advanced topics that are outside the scope of this getting started series, but you should see MSDN's documentation of them after you have completed this series of tutorials.</span></span>
 

 
<span data-ttu-id="fb8dd-237">Имеется и другой способ проверить, существует ли список: вместо того чтобы использовать метод **GetByTitle** для получения ссылки на список, вы можете проверить, имеется ли список с указанным именем в "списке списков" веб-сайта. Это можно сделать с помощью кода, аналогичного указанному ниже.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-237">There is an alternative way to check for the existence of a list: instead of using the **GetByTitle** method to get a reference to the list, you can check to see if a list with the specified name is in the website's "list of lists" with code like the following.</span></span>
 

 



```C#
var query = from list in clientContext.Web.Lists 
             where list.Title == "Expected Shipments" 
             select list; 
IEnumerable<List> matchingLists = clientContext.LoadQuery(query); 
clientContext.ExecuteQuery(); 
if (matchingLists.Count() != 0) 
{ 
    List expectedShipmentsList = matchingLists.Single(); 
    // Do something with the list. 
}
clientContext.ExecuteQuery(); 
```

<span data-ttu-id="fb8dd-p130">Предыдущий код имеет одно преимущество: он позволяет избежать сложностей класса **ConditionalScope**. Мы будем использовать этот код во всех статьях этой серии. Но есть и недостаток: для этого кода необходим дополнительный вызов **ExecuteQuery** только для того, чтобы получить значение, которое вы хотите проверить в операторе **if**. Если мы используем этот способ в методе `CreateExpectedShipment`, чтобы проверить, существует ли список, то этот метод будет выполнять два вызова **ExecuteQuery**, каждый из которых делает HTTP-запрос с удаленного веб-сервера в SharePoint. Эти запросы потребляют большую часть времени в любом методе CSOM, поэтому рекомендуется свести их использование к минимуму.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p130">The preceding code has the advantage of allowing you to avoid the complications of the **ConditionalScope** class, and we use exactly this code elsewhere in this series of articles. But there is a disadvantage too: this code requires an extra call of **ExecuteQuery** solely to get the value you want to check in the **if** statement. If we use this technique in the `CreateExpectedShipment` to check for the existence of the list, then that method will have two calls of **ExecuteQuery** each of which makes an HTTP request from the remote web server to SharePoint. These requests are the most time-consuming part of any CSOM method, so it is generally a good practice to minimize them.</span></span>
 

 
<span data-ttu-id="fb8dd-p131">Мы не будем изменять метод  `CreateExpectedShipment`, но при разработке надстройки для рабочей среды вам придется обдумать, что должен делать ваш код, если компонент, на который он ссылается, удален. Один из вариантов программное восстановление списка из корзины, но это будет раздражать пользователей, которые удалили список намеренно. Кроме того, может оказаться, что лучший вариант это ничего не делать для предотвращения исключения. Исключение, полученное из SharePoint, будет предупреждать пользователей, что удаление списка нарушило работу части надстройки, причем, пользователь, удаливший список, может и не осознавать этого. После этого пользователь может попытаться восстановить список из корзины или продолжить работу без части функций надстройки, которые больше не работают.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p131">We will leave the  `CreateExpectedShipment` as it is, but in a production add-in, you need to think about how your code is going to work if a component that it references is deleted. Programmatically restoring the list from the Recycle Bin is one option, but that would annoy users who intentionally decided to delete the list. You should also consider that doing nothing at all to prevent the exception might be the best choice. An exception from SharePoint would alert users that the deletion of the list has broken part of the add-in, which is something the person who deleted it might not have realized. A user can then decide whether to restore the list from the Recycle Bin or do without the part of the add-in functionality that no longer works.</span></span>
 

 

## <a name="request-permission-to-manage-the-website"></a><span data-ttu-id="fb8dd-247">Запрос разрешения на управление веб-сайтом</span><span class="sxs-lookup"><span data-stu-id="fb8dd-247">Request permission to manage the website</span></span>

<span data-ttu-id="fb8dd-p132">Вспомним, что когда надстройка запрашивает разрешение "Чтение" или "Запись" с областью "Список", SharePoint предлагает пользователю сделать надстройку доверенной. При этом в диалоговом окне имеется раскрывающийся список, в котором пользователь может выбрать список, доступ к которому следует предоставить надстройке. Можно выбрать только один список. Но сейчас надстройка Chain Store записывает данные в два разных списка. Чтобы получить доступ к нескольким спискам, надстройке необходимо запросить разрешение с областью "Интернет". Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p132">Recall that when an add-in requests Read or Write permission with the scope of List, SharePoint prompts the user to trust the add-in and the dialog contains a drop down list where the user selects the list to which the add-in should have access. Only one list can be selected. But the Chain Store add-in now writes to two different lists. To gain access to multiple lists, the add-in has to request permission with the scope of Web. Follow these steps:</span></span>
 

 

1. <span data-ttu-id="fb8dd-253">В **обозревателе решений** откройте файл AppManifest.xml проекта **ChainStore**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-253">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>
    
 
2. <span data-ttu-id="fb8dd-254">Откройте вкладку **Разрешения** и в поле **Область** в раскрывающемся списке выберите **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-254">Open the **Permissions** tab and in the **Scope** field, select **Web** from the drop down.</span></span>
    
 
3. <span data-ttu-id="fb8dd-255">В поле **Разрешение** в раскрывающемся списке выберите пункт **Запись**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-255">In the **Permission** field, select **Write** from the drop down.</span></span>
    
 
4. <span data-ttu-id="fb8dd-256">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-256">Save the file.</span></span> 
    
 

## <a name="run-the-add-in-and-test-the-item-creation"></a><span data-ttu-id="fb8dd-257">Запуск надстройки и тестирование функции создания элемента</span><span class="sxs-lookup"><span data-stu-id="fb8dd-257">Run the add-in and test the item creation</span></span>


 

 

1. <span data-ttu-id="fb8dd-p133">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p133">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span> 
    
 
2. <span data-ttu-id="fb8dd-262">Когда откроется начальная страница надстройки, в нижней части страницы щелкните ссылку **Order Form** (Форма заказа).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-262">When the add-in's start page opens, click the **Order Form** link at the bottom of the page.</span></span>
    
 
3. <span data-ttu-id="fb8dd-263">Введите необходимые значения в форму и нажмите кнопку **Place Order** (Заказать).</span><span class="sxs-lookup"><span data-stu-id="fb8dd-263">Enter some values in the form and press **Place Order**.</span></span>
    
 
4. <span data-ttu-id="fb8dd-264">С помощью кнопки "Назад" в браузере вернитесь на начальную страницу, а затем вверху на элементе управления хрома щелкните **Вернуться на сайт**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-264">Use the browser's back button to navigate back to the start page, and then click **Back to Site** on the chrome control at the top.</span></span>
    
 
5. <span data-ttu-id="fb8dd-p134">На начальной странице магазина в Гонконге выберите **Контент сайта** и откройте список **Expected Shipments** (Ожидаемые поставки). Теперь в списке есть элемент, соответствующий заказу. Ниже показан снимок экрана с примером.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p134">From the home page of the Hong Kong store, navigate to **Site Contents** and open the **Expected Shipments** list. There is now an item on the list corresponding to the order. The following screenshot is an example.</span></span>
    
  ![Список "Ожидаемые поставки" с одним элементом. Поля "Продукт" и "Поставщик" содержат значения. Поле "Количество" содержит число. В двух полях "Да/Нет" задано значение "Нет".](../../images/e4285084-d31e-4e79-a469-ddebbc7dfb18.PNG)
 

 

 
6. <span data-ttu-id="fb8dd-p136">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-p136">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
7. <span data-ttu-id="fb8dd-274">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="fb8dd-274">Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="fb8dd-275"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="fb8dd-275"></span></span>

 <span data-ttu-id="fb8dd-276">В следующей статье вы узнаете, как придать удаленной форме заказа вид веб-части на странице SharePoint: [Включение веб-части надстройки в надстройку, размещаемую у поставщика](include-an-add-in-part-in-the-provider-hosted-add-in)</span><span class="sxs-lookup"><span data-stu-id="fb8dd-276">In the next article, you'll learn how to surface the remote Order Form as a Web Part in a SharePoint page: [Include an add-in part in the provider-hosted add-in](include-an-add-in-part-in-the-provider-hosted-add-in)</span></span>
 

 

