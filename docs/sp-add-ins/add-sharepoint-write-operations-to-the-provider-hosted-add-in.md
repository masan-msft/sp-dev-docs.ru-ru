---
title: "Добавление операций записи SharePoint в надстройку с размещением у поставщика"
description: "Запись данных в SharePoint в надстройке SharePoint, размещаемой у поставщика: изменение значения столбца в элементе списка, запрос разрешения на запись, создание настраиваемого списка и вставка элемента в список, а также проверка на наличие удаленных компонентов."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: cfbba658bcb297c3ae07b55246c9fe06b994c6ba
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-sharepoint-write-operations-to-the-provider-hosted-add-in"></a><span data-ttu-id="55ac2-103">Добавление операций записи SharePoint в надстройку с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="55ac2-103">Add SharePoint write operations to the provider-hosted add-in</span></span>

<span data-ttu-id="55ac2-104">Это пятая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md#SP15createprovider_nextsteps).</span><span class="sxs-lookup"><span data-stu-id="55ac2-104">This is the fifth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 

> [!NOTE]
> <span data-ttu-id="55ac2-105">Если вы изучали предыдущие статьи этой серии о размещаемых у поставщика надстройках, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей.</span><span class="sxs-lookup"><span data-stu-id="55ac2-105">If you have been working through this series about provider-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="55ac2-106">Кроме того, вы можете скачать репозиторий [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeSharePointWriteOps.sln.</span><span class="sxs-lookup"><span data-stu-id="55ac2-106">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeSharePointWriteOps.sln file.</span></span>

<span data-ttu-id="55ac2-107">В этой статье мы вернемся к написанию кода и добавим несколько функций, которые записывают данные в надстройку SharePoint Chain Store.</span><span class="sxs-lookup"><span data-stu-id="55ac2-107">In this article, we get back to coding by adding some functions that write data to the Chain Store SharePoint Add-in.</span></span>

## <a name="change-a-column-value-on-a-sharepoint-list-item"></a><span data-ttu-id="55ac2-108">Изменение значения столбца в элементе списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="55ac2-108">Change a column value on a SharePoint list item</span></span>

<span data-ttu-id="55ac2-109">В нашей надстройке есть настраиваемая кнопка ленты, добавляющая сотрудника из списка **Local Employees** (Местные сотрудники) магазина в Гонконге в корпоративную базу данных.</span><span class="sxs-lookup"><span data-stu-id="55ac2-109">Our add-in has a custom ribbon button that adds an employee from the Hong Kong store's **Local Employees** list to the corporate database.</span></span> <span data-ttu-id="55ac2-110">Тем не менее пользователю приходится вручную изменять значение поля **Added to Corporate DB** (Добавлен в корпоративную базу данных) на **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="55ac2-110">But the user has to remember to manually change the value of the **Added to Corporate DB** field to **Yes**.</span></span> <span data-ttu-id="55ac2-111">Давайте добавим код, который будет делать это автоматически.</span><span class="sxs-lookup"><span data-stu-id="55ac2-111">Let's add code to do that automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="55ac2-112">Когда решение открывается повторно, для параметров раздела "Запускаемые проекты" в Visual Studio обычно возвращаются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="55ac2-112">The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened.</span></span> <span data-ttu-id="55ac2-113">После повторного открытия примера решения, который рассматривается в этой серии статей, всегда выполняйте указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="55ac2-113">Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 

> 1. <span data-ttu-id="55ac2-114">В верхней части **обозревателя решений** щелкните узел решения правой кнопкой мыши и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-114">Right-click the solution node at the top of **Solution Explorer**, and then select **Set startup projects**.</span></span>  
> 2. <span data-ttu-id="55ac2-115">Убедитесь, что в столбце **Действие** для всех трех проектов указано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-115">Ensure that all three projects are set to **Start** in the **Action** column.</span></span>

1. <span data-ttu-id="55ac2-116">В **обозревателе решений** откройте файл EmployeeAdder.cs.</span><span class="sxs-lookup"><span data-stu-id="55ac2-116">In **Solution Explorer**, open the EmployeeAdder.cs file.</span></span>

2. <span data-ttu-id="55ac2-117">Добавьте указанную ниже строку в метод **Page_Load** между вызовами методов `AddLocalEmployeeToCorpDB` и `Response.Redirect`.</span><span class="sxs-lookup"><span data-stu-id="55ac2-117">Add the following line to the **Page_Load** method between the call of `AddLocalEmployeeToCorpDB` and the call of `Response.Redirect`.</span></span> <span data-ttu-id="55ac2-118">Вы создадите метод **SetLocalEmployeeSyncStatus** на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="55ac2-118">In the next step, you create the **SetLocalEmployeeSyncStatus** method.</span></span>
    
    ```C#
       // Write to SharePoint 
     SetLocalEmployeeSyncStatus();
    ```

3. <span data-ttu-id="55ac2-119">Добавьте указанный ниже новый метод в класс `EmployeeAdder`.</span><span class="sxs-lookup"><span data-stu-id="55ac2-119">Add the following new method to the `EmployeeAdder` class.</span></span> 

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

   <span data-ttu-id="55ac2-120">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="55ac2-120">Note the following about this code:</span></span>
    
   - <span data-ttu-id="55ac2-p105">Внутреннее имя поля **Added to Corporate DB** (Добавлен в корпоративную базу данных) выглядит довольно странно. Это связано с тем, что внутренние имена полей не должны содержать пробелы. Когда пользователь создает поле с пробелами в отображаемом имени, при задании внутреннего имени SharePoint заменяет каждый пробел строкой _x0020_. Из-за этого строка Added to Employee DB превратилась в строку Added_x0020_to_x0020_Corporate_x0020_DB. Длина внутренних имен не должна превышать 32 символов, поэтому имя усечено до строки Added_x0020_to_x0020_Corporate_x.</span><span class="sxs-lookup"><span data-stu-id="55ac2-p105">The internal name for the **Added to Corporate DB** field is odd-looking. Internal field names cannot contain spaces, so when a user creates a field with spaces in its display name, SharePoint substitutes the string "_x0020_" for each space when it sets the internal name. This turns "Added to Employee DB" into "Added_x0020_to_x0020_Corporate_x0020_DB". Internal names cannot be more than 32 characters, so the name is truncated to just "Added_x0020_to_x0020_Corporate_x".</span></span>

   - <span data-ttu-id="55ac2-125">Хотя в пользовательском интерфейсе SharePoint столбец **Added to Corporate DB** (Добавлен в корпоративную базу данных) называется полем **Yes/No** (Да или нет), на самом деле он имеет логический тип, поэтому его значение — **true**, а не **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="55ac2-125">Although the **Added to Corporate DB** column is called a **Yes/No** field in the SharePoint UI, it is really a boolean, so its value is set to **true**, not **Yes**.</span></span>

   - <span data-ttu-id="55ac2-p106">Для фиксации изменений в базе данных контента SharePoint доложен вызвать метод **Update** класса **ListItem**. Существует общее, но не совсем универсальное правило, согласно которому при изменении значения свойства объекта, хранящегося в базах данных SharePoint, необходимо вызвать метод **Update** объекта.</span><span class="sxs-lookup"><span data-stu-id="55ac2-p106">The **Update** method of the **ListItem** class must be called to commit the changes to SharePoint's content database. It is a general, but not quite universal, rule that when you change a property value of an object that is stored in the SharePoint databases, you must call the object's **Update** method.</span></span>

## <a name="request-permission-to-write-to-the-host-web-list"></a><span data-ttu-id="55ac2-128">Запрос разрешения на запись в список хост-сайта</span><span class="sxs-lookup"><span data-stu-id="55ac2-128">Request permission to write to the host web list</span></span>

<span data-ttu-id="55ac2-129">Так как теперь надстройка не только считывает данные из списка, но и записывает их туда, нам необходимо расширить разрешения для надстройки с "Чтение" до "Запись".</span><span class="sxs-lookup"><span data-stu-id="55ac2-129">Because the add-in is now writing to the list as well as reading it, we need to escalate the permissions that the add-in requests from Read to Write.</span></span> <span data-ttu-id="55ac2-130">Сделайте вот что:</span><span class="sxs-lookup"><span data-stu-id="55ac2-130">Follow these steps.</span></span>

1. <span data-ttu-id="55ac2-131">В **обозревателе решений** в проекте **ChainStore** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="55ac2-131">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>

2. <span data-ttu-id="55ac2-132">Откройте вкладку **Разрешения** и в поле **Разрешение** в раскрывающемся списке выберите **Запись**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-132">Open the **Permissions** tab, and in the **Permission** field, select **Write** from the drop-down.</span></span>

3. <span data-ttu-id="55ac2-133">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="55ac2-133">Save the file.</span></span> 

## <a name="run-the-add-in-and-test-the-button"></a><span data-ttu-id="55ac2-134">Запуск надстройки и тестирование кнопки</span><span class="sxs-lookup"><span data-stu-id="55ac2-134">Run the add-in and test the button</span></span>

1. <span data-ttu-id="55ac2-135">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="55ac2-135">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="55ac2-136">Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express.</span><span class="sxs-lookup"><span data-stu-id="55ac2-136">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="55ac2-137">Кроме того, он выполняет временную установку надстройки на вашем тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="55ac2-137">It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="55ac2-138">Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="55ac2-138">You are prompted to grant permissions to the add-in before its start page opens.</span></span> 

2. <span data-ttu-id="55ac2-139">В форме разрешений выберите в списке пункт **Local Employees** (Локальные сотрудники), а затем щелкните **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-139">On the permission form, select **Local Employees** from the list, and then select **Trust it**.</span></span>

3. <span data-ttu-id="55ac2-140">Когда откроется начальная страница, на размещенном в верхней части элементе управления хрома нажмите кнопку **Вернуться на сайт**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-140">When the add-in's start page opens, click **Back to Site** on the chrome control at the top.</span></span>

4. <span data-ttu-id="55ac2-141">На домашней странице веб-сайта выберите **Site Contents**(Содержание сайта) > **Local Employees** (Местные сотрудники).</span><span class="sxs-lookup"><span data-stu-id="55ac2-141">From the website's home page, go to **Site Contents** > **Local Employees**.</span></span> <span data-ttu-id="55ac2-142">Откроется страница представления списка.</span><span class="sxs-lookup"><span data-stu-id="55ac2-142">The list view page opens.</span></span>

5. <span data-ttu-id="55ac2-143">Если в списке нет сотрудников, для которых в столбце **Added to Corporate DB** (Добавлен в корпоративную базу данных) указано значение **No** (Нет), добавьте в список еще одного сотрудника и *не устанавливайте флажок __Added to Corporate DB__ (Добавлен в корпоративную базу данных).*</span><span class="sxs-lookup"><span data-stu-id="55ac2-143">If there are no employees on the list with **No** in the **Added to Corporate DB** column, add an employee to the list, and *do not select the __Added to Corporate DB__ check box.*</span></span> 

6. <span data-ttu-id="55ac2-144">На ленте откройте вкладку **Элементы**. В разделе **Действия** вкладки есть специальная кнопка **Add to Corporate DB** (Добавить в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="55ac2-144">On the ribbon, open the **Items** tab. In the **Actions** section of the tab is the custom button **Add to Corporate DB**.</span></span>

7. <span data-ttu-id="55ac2-145">В списке выберите сотрудника, для которого в столбце **Added to Corporate DB** (Добавлен в корпоративную базу данных) задано значение **No** (Нет).</span><span class="sxs-lookup"><span data-stu-id="55ac2-145">Select an employee on the list that has **No** in the **Added to Corporate DB** column.</span></span>

8. <span data-ttu-id="55ac2-146">Нажмите кнопку **Add to Corporate DB** (Добавить в корпоративную базу данных).</span><span class="sxs-lookup"><span data-stu-id="55ac2-146">Select the **Add to Corporate DB** button.</span></span> <span data-ttu-id="55ac2-147">(Сначала необходимо выбрать элемент.)</span><span class="sxs-lookup"><span data-stu-id="55ac2-147">(You must select an item first.)</span></span>

9. <span data-ttu-id="55ac2-148">Вам покажется, что страница перезагружается, так как метод **Page_Load** страницы EmployeeAdder выполняет перенаправление на нее.</span><span class="sxs-lookup"><span data-stu-id="55ac2-148">The page seems to reload because the **Page_Load** method of the EmployeeAdder page redirects back to it.</span></span> <span data-ttu-id="55ac2-149">В итоге значение поля **Added to Corporate DB** (Добавлен в корпоративную базу данных) для сотрудника изменится на **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="55ac2-149">The value of the **Added to Corporate DB** field for the employee changes to **Yes**.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="55ac2-150">Что-нибудь мешает пользователю вручную изменить значение поля **Added to Corporate DB** (Добавлен в корпоративную базу данных) и рассогласовать данные в списке и корпоративной базе данных?</span><span class="sxs-lookup"><span data-stu-id="55ac2-150">What prevents a user from manually changing the value **Added to Corporate DB** in a way that makes the list and the corporate database inconsistent?</span></span> <span data-ttu-id="55ac2-151">Нет.</span><span class="sxs-lookup"><span data-stu-id="55ac2-151">Nothing does at the moment.</span></span> <span data-ttu-id="55ac2-152">Мы решим эту проблему в одной из следующих статей серии.</span><span class="sxs-lookup"><span data-stu-id="55ac2-152">You'll get the solution to this problem in a later article of this series.</span></span>

10. <span data-ttu-id="55ac2-153">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55ac2-153">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="55ac2-154">При каждом нажатии клавиши F5 Visual Studio отзывает предыдущую версию надстройки и устанавливает ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="55ac2-154">Each time you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

11. <span data-ttu-id="55ac2-155">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-155">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="create-a-new-custom-list-on-the-host-website"></a><span data-ttu-id="55ac2-156">Создание настраиваемого списка на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="55ac2-156">Create a new custom list on the host website</span></span>

<span data-ttu-id="55ac2-157">Теперь нам необходимо усовершенствовать надстройку Chain Store — сделать так, чтобы можно было создавать элементы, а не просто изменять поля существующих элементов.</span><span class="sxs-lookup"><span data-stu-id="55ac2-157">The next improvement to the Chain Store add-in is to create new items in a list, instead of merely changing a field in an existing item.</span></span> <span data-ttu-id="55ac2-158">В частности, при размещении нового заказа на корпоративном уровне в списке SharePoint должен автоматически создаваться элемент, который предупредит местных сотрудников о предстоящей отгрузке.</span><span class="sxs-lookup"><span data-stu-id="55ac2-158">Specifically, when a new order is placed at the corporate level, an item is automatically created in a SharePoint list that alerts local employees to expect a shipment.</span></span> <span data-ttu-id="55ac2-159">Этот список называется **Expected Shipments** (Ожидаемые отгрузки). Вы создадите его, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="55ac2-159">The list is called **Expected Shipments** and you create it with the following steps.</span></span> <span data-ttu-id="55ac2-160">В одной из следующих статей этой серии вы узнаете, как программным способом добавить настраиваемый список на хост-сайт, но сейчас вы добавите его вручную.</span><span class="sxs-lookup"><span data-stu-id="55ac2-160">In a later article in this series, you'll learn how to programmatically add a custom list to a host website, but for now you'll add this one manually.</span></span>

1. <span data-ttu-id="55ac2-161">На начальной странице магазина Fabrikam в Гонконге выберите пункты **Site Contents**(Содержание сайта) > **Add an add-in**(Добавить надстройку) > **Custom List** (Настраиваемый список).</span><span class="sxs-lookup"><span data-stu-id="55ac2-161">From the home page of the Fabrikam Hong Kong Store, go to **Site Contents** > **Add an add-in** > **Custom List**.</span></span> 

2. <span data-ttu-id="55ac2-162">В диалоговом окне **Добавление настраиваемого списка** укажите имя **Expected Shipments** (Ожидаемые отгрузки) и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-162">In the **Adding Custom List** dialog, specify **Expected Shipments** as the name, and then select **Create**.</span></span> 

3. <span data-ttu-id="55ac2-163">На странице **Site Contents** (Содержание сайта) откройте список **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="55ac2-163">On the **Site Contents** page, open the **Expected Shipments** list.</span></span>

4. <span data-ttu-id="55ac2-164">Откройте вкладку **Список** на ленте, а затем нажмите кнопку **Параметры списка**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-164">On the **List** tab on the ribbon, select **List Settings**.</span></span>

5. <span data-ttu-id="55ac2-165">В разделе **Столбцы** на странице **Параметры списка** выберите столбец **Название**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-165">In the **Columns** section of the **List Settings** page, select the **Title** column.</span></span>

6. <span data-ttu-id="55ac2-166">Откроется форма **Изменение столбца**. В поле **Имя столбца** измените значение с **Title** (Название) на **Product** (Продукт), а затем нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-166">In the **Edit Column** form, change the **Column name** from **Title** to **Product**, and then select **OK**.</span></span>

7. <span data-ttu-id="55ac2-167">На странице **Параметры** выберите команду **Создать столбец**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-167">On the **Settings** page, select **Create column**.</span></span>

8. <span data-ttu-id="55ac2-p115">В предыдущей статье этой серии вы узнали, как создавать настраиваемые столбцы для списка. Добавьте четыре столбца для списка **Expected Shipments** (Ожидаемые отгрузки), используя значения из указанной ниже таблицы. Для всех остальных параметров оставьте значения, используемые по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="55ac2-p115">In a previous article of this series, you learned how to create custom columns for a list. For the **Expected Shipments** list, add four columns, using the values in the following table. Leave all other settings at their defaults.</span></span>

   |<span data-ttu-id="55ac2-171">**Имя столбца**</span><span class="sxs-lookup"><span data-stu-id="55ac2-171">**Column name**</span></span>|<span data-ttu-id="55ac2-172">**Тип**</span><span class="sxs-lookup"><span data-stu-id="55ac2-172">**Type**</span></span>|<span data-ttu-id="55ac2-173">**Обязательный?**</span><span class="sxs-lookup"><span data-stu-id="55ac2-173">**Required?**</span></span>|<span data-ttu-id="55ac2-174">**Значение, используемое по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="55ac2-174">**Default value**</span></span>|
   |:-----|:-----|:-----|:-----|
   |<span data-ttu-id="55ac2-175">"Supplier" (Поставщик)</span><span class="sxs-lookup"><span data-stu-id="55ac2-175">Supplier</span></span>|<span data-ttu-id="55ac2-176">**Однострочный текст**</span><span class="sxs-lookup"><span data-stu-id="55ac2-176">**Single line of text**</span></span>|<span data-ttu-id="55ac2-177">Не требуется</span><span class="sxs-lookup"><span data-stu-id="55ac2-177">Not required</span></span>|<span data-ttu-id="55ac2-178">Нет</span><span class="sxs-lookup"><span data-stu-id="55ac2-178">None</span></span>|
   |<span data-ttu-id="55ac2-179">"Quantity" (Количество)</span><span class="sxs-lookup"><span data-stu-id="55ac2-179">Quantity</span></span>|<span data-ttu-id="55ac2-180">**Число**</span><span class="sxs-lookup"><span data-stu-id="55ac2-180">**Number**</span></span>|<span data-ttu-id="55ac2-181">Обязательный</span><span class="sxs-lookup"><span data-stu-id="55ac2-181">Required</span></span>|<span data-ttu-id="55ac2-182">1</span><span class="sxs-lookup"><span data-stu-id="55ac2-182">1</span></span>|
   |<span data-ttu-id="55ac2-183">"Arrived" (Доставлено)</span><span class="sxs-lookup"><span data-stu-id="55ac2-183">Arrived</span></span>|<span data-ttu-id="55ac2-184">**Yes/No** (Да или нет)</span><span class="sxs-lookup"><span data-stu-id="55ac2-184">**Yes/No**</span></span>|<span data-ttu-id="55ac2-185">Не требуется</span><span class="sxs-lookup"><span data-stu-id="55ac2-185">Not required</span></span>|<span data-ttu-id="55ac2-186">No (Нет)</span><span class="sxs-lookup"><span data-stu-id="55ac2-186">No</span></span>|
   |<span data-ttu-id="55ac2-187">"Added to Inventory" (Добавлено в инвентарь)</span><span class="sxs-lookup"><span data-stu-id="55ac2-187">Added to Inventory</span></span>|<span data-ttu-id="55ac2-188">**Yes/No** (Да или нет)</span><span class="sxs-lookup"><span data-stu-id="55ac2-188">**Yes/No**</span></span>|<span data-ttu-id="55ac2-189">Не требуется</span><span class="sxs-lookup"><span data-stu-id="55ac2-189">Not required</span></span>|<span data-ttu-id="55ac2-190">No (Нет)</span><span class="sxs-lookup"><span data-stu-id="55ac2-190">No</span></span>|

9. <span data-ttu-id="55ac2-191">После создания столбцов на странице параметров списка выберите **Site Contents** (Содержание сайта). Откроется страница **Site Contents** (Содержание сайта).</span><span class="sxs-lookup"><span data-stu-id="55ac2-191">After you have created the columns, on the list settings page, select **Site Contents** to open the **Site Contents** page.</span></span> <span data-ttu-id="55ac2-192">Откройте список **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="55ac2-192">Open the **Expected Shipments** list.</span></span>

10. <span data-ttu-id="55ac2-193">Нажмите кнопку **Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-193">Select **new item**.</span></span> <span data-ttu-id="55ac2-194">Форма создания элемента должна иметь точно такой же вид, как показано ниже, включая две звездочки, обозначающие обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="55ac2-194">The item creation form should look exactly like the following, including the two asterisks that indicate required fields.</span></span>

   <span data-ttu-id="55ac2-195">*Рис. 1. Форма создания элемента для списка Expected Shipments (Ожидаемые отгрузки)*</span><span class="sxs-lookup"><span data-stu-id="55ac2-195">*Figure 1. Item creation form for the Expected Shipments list*</span></span>

   ![Форма создания элемента для списка "Ожидаемые поставки" с полями "Продукт", "Поставщик", "Количество", "Поступил" и "Добавлен в перечень". Звездочки рядом с заголовками "Продукт" и "Количество" и значение по умолчанию 1 (один) для поля "Количество".](../images/e552b5c9-8baa-4e53-9295-4d85a79d7734.PNG)

11. <span data-ttu-id="55ac2-199">Мы не будем создавать элементы этого списка вручную, поэтому нажмите кнопку **Отмена**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-199">We don't want to manually create items in this list, so click **Cancel**.</span></span>

## <a name="insert-an-item-into-a-sharepoint-list"></a><span data-ttu-id="55ac2-200">Вставка элемента в список SharePoint</span><span class="sxs-lookup"><span data-stu-id="55ac2-200">Insert an item into a SharePoint list</span></span>

<span data-ttu-id="55ac2-201">Теперь добавьте в надстройку функцию, которая при размещении заказа для магазина в Гонконге на корпоративном уровне создает элемент в списке **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="55ac2-201">Now you add a function to the add-in that creates an item in the **Expected Shipments** list whenever an order for the Hong Kong store is placed at the corporate level.</span></span>

1. <span data-ttu-id="55ac2-202">В **обозревателе решений** откройте файл OrderForm.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="55ac2-202">In **Solution Explorer**, open the OrderForm.aspx.cs file.</span></span>

2. <span data-ttu-id="55ac2-203">В начало файла добавьте оператор **using** для **Microsoft.SharePoint.Client**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-203">Add a **using** statement for **Microsoft.SharePoint.Client** to the top of the file.</span></span>

3. <span data-ttu-id="55ac2-204">В методе **btnCreateOrder_Click** добавьте указанную ниже строку сразу же после вызова `CreateOrder`.</span><span class="sxs-lookup"><span data-stu-id="55ac2-204">In the **btnCreateOrder_Click** method, add the following line just under the call to `CreateOrder`.</span></span> <span data-ttu-id="55ac2-205">Вы создадите метод **CreateExpectedShipment** на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="55ac2-205">You'll create the **CreateExpectedShipment** method in the next step.</span></span>
    
    ```C#
      CreateExpectedShipment(txtBoxSupplier.Text, txtBoxItemName.Text, quantity);
    ```

4. <span data-ttu-id="55ac2-206">Добавьте указанный ниже метод в класс `OrderForm`.</span><span class="sxs-lookup"><span data-stu-id="55ac2-206">Add the following method to the `OrderForm` class.</span></span> 

    ```C#
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

   <span data-ttu-id="55ac2-207">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="55ac2-207">Note the following about this code:</span></span>

   - <span data-ttu-id="55ac2-208">Для создания объекта **ListItem** не используется конструктор.</span><span class="sxs-lookup"><span data-stu-id="55ac2-208">A  **ListItem** object is not created with a constructor.</span></span> <span data-ttu-id="55ac2-209">Это связано с соображениями производительности.</span><span class="sxs-lookup"><span data-stu-id="55ac2-209">This is for performance reasons.</span></span> <span data-ttu-id="55ac2-210">Объект **ListItem** имеет ряд свойств (со значениями по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="55ac2-210">A **ListItem** object has many properties (with default values).</span></span> <span data-ttu-id="55ac2-211">Если используется конструктор, весь объект будет включен в сообщение XML, которое метод **ExecuteQuery** отправляет на сервер.</span><span class="sxs-lookup"><span data-stu-id="55ac2-211">If a constructor is used, the entire object would be included in the XML message that the **ExecuteQuery** method sends to the server.</span></span> 
   
   - <span data-ttu-id="55ac2-212">**ListItemCreationInformation** — это "легковесный" объект, содержащий только минимальное количество значений, не используемых по умолчанию, которые необходимы серверу для создания объекта **ListItem**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-212">The **ListItemCreationInformation** object is a lightweight object that only contains the minimal non-default values that the server needs to create a **ListItem** object.</span></span> <span data-ttu-id="55ac2-213">Кроме того, может присутствовать строка, которая создает объект **ListItem**, но при вызове этой строки происходит только добавление XML-разметки в сообщение, отправляемое на сервер.</span><span class="sxs-lookup"><span data-stu-id="55ac2-213">It may appear that there is a line that creates a **ListItem** object, but recall that this line only adds some XML markup to a message that is sent to the server.</span></span> <span data-ttu-id="55ac2-214">Объект **ListItem** создается на сервере.</span><span class="sxs-lookup"><span data-stu-id="55ac2-214">The **ListItem** object is created there on the server.</span></span>

   - <span data-ttu-id="55ac2-215">Нет необходимости отправлять объект **ListItem** обратно клиенту, поэтому метод **ClientContext.Load** не вызывается.</span><span class="sxs-lookup"><span data-stu-id="55ac2-215">There is no need to bring the **ListItem** object back down to the client, so there is no call to the **ClientContext.Load** method.</span></span>

   - <span data-ttu-id="55ac2-216">В коде не нужно явно задавать значения полей **Arrived** (Прибыл) или **Added to Inventory** (Добавлен в запасы), так как им присвоено значение **No** (Нет), используемое по умолчанию, то есть именно то, что нам нужно.</span><span class="sxs-lookup"><span data-stu-id="55ac2-216">The code does not need to explicitly set the **Arrived** or **Added to Inventory** fields because they have default values of **No**, which is what we want.</span></span>

## <a name="check-for-deleted-components"></a><span data-ttu-id="55ac2-217">Проверка на наличие удаленных компонентов</span><span class="sxs-lookup"><span data-stu-id="55ac2-217">Check for deleted components</span></span>

<span data-ttu-id="55ac2-p122">Любой пользователь с привилегиями владельца списка SharePoint может удалить этот список. Если список развернут надстройкой на хост-сайте, то его может удалить и владелец хост-сайта. Это может случиться, если владелец решит, что ему не нужна функциональность, предоставляемая списком. (Если затем владелец изменит свое решение, то можно будет восстановить список из корзины SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="55ac2-p122">Anyone with list owner privileges for a SharePoint list can delete the list. And if the list is deployed to the host web by an add-in, the website owner of the host web can delete it. That may happen if the owner decides to do without the functionality provided by the list. (It can be restored from the SharePoint Recycle Bin if the owner changes his mind.)</span></span> 

<span data-ttu-id="55ac2-222">Работа метода **CreateExpectedShipment** зависит от того, существует ли список **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="55ac2-222">The **CreateExpectedShipment** method depends on the existence of the **Expected Shipments** list.</span></span> <span data-ttu-id="55ac2-223">Предположим, что владелец веб-сайта решил удалить список.</span><span class="sxs-lookup"><span data-stu-id="55ac2-223">Suppose a website owner decided to delete the list.</span></span> <span data-ttu-id="55ac2-224">Позже, при добавлении заказа с помощью **формы заказа** надстройки, вызывается метод **CreateExpectedShipment**, который создаст исключение с сообщением о том, что на веб-сайте SharePoint нет списка **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="55ac2-224">Later, when an order is added with the add-in's **Order Form**, the **CreateExpectedShipment** method is called and throws an exception whose message says that there's no **Expected Shipments** list on the SharePoint website.</span></span>

<span data-ttu-id="55ac2-225">Вам может потребоваться, чтобы перед какими-либо действиями со списком `expectedShipmentsList` метод проверял, не пуст ли он.</span><span class="sxs-lookup"><span data-stu-id="55ac2-225">You might want the method to check the `expectedShipmentsList` for nullity before it does anything with it.</span></span> <span data-ttu-id="55ac2-226">Когда вы работаете с CSOM, вам *не* удастся выполнить эту проверку с помощью простой структуры, например вот такой:</span><span class="sxs-lookup"><span data-stu-id="55ac2-226">When you are working with CSOM, you can *not*  make this check with a simple structure like this:</span></span>

`if (expectedShipmentsList != null) { ... }`
 
<span data-ttu-id="55ac2-227">Вместо этого вам придется использовать особый класс CSOM, который называется **ConditionalScope**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-227">Instead, you need to use a special CSOM class called **ConditionalScope**.</span></span> <span data-ttu-id="55ac2-228">Причины этого связаны с системой пакетной обработки CSOM, о которой мы упоминали в предыдущей статье этой серии (см. раздел [Среда выполнения и пакетная обработка в клиенте](get-a-quick-overview-of-the-sharepoint-object-model.md#CSOMBatching)).</span><span class="sxs-lookup"><span data-stu-id="55ac2-228">The reasons for this are connected to CSOM's batching system, which was mentioned in the previous article in this series (see [Client-side runtime and batching](get-a-quick-overview-of-the-sharepoint-object-model.md#CSOMBatching)).</span></span> <span data-ttu-id="55ac2-229">**ConditionalScope** и система пакетной обработки — это более сложные темы, которые выходят за рамки данной серии статей для начинающих, но после изучения этой серии вам следует ознакомиться с документацией MSDN по этим темам.</span><span class="sxs-lookup"><span data-stu-id="55ac2-229">**ConditionalScope** and the batching system are advanced topics that are outside the scope of this getting started series, but you should see MSDN's documentation about them after you have completed this series of tutorials.</span></span>

<span data-ttu-id="55ac2-230">Наличие списка можно проверить по-другому: вместо получения ссылки на список с помощью метода **GetByTitle** вы можете проверить, имеется ли список с указанным именем в "списке списков" веб-сайта. Это можно сделать с помощью кода, аналогичного указанному ниже.</span><span class="sxs-lookup"><span data-stu-id="55ac2-230">An alternative way to check for the existence of a list is as follows: instead of using the **GetByTitle** method to get a reference to the list, you can check to see if a list with the specified name is in the website's "list of lists" with code like the following.</span></span>

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

<span data-ttu-id="55ac2-231">Предыдущий код имеет одно преимущество: он позволяет вам не усложнять класс **ConditionalScope**. Мы будем использовать этот код во всех статьях этой серии.</span><span class="sxs-lookup"><span data-stu-id="55ac2-231">The preceding code has the advantage of allowing you to avoid the complications of the **ConditionalScope** class, and we use exactly this code elsewhere in this series of articles.</span></span> <span data-ttu-id="55ac2-232">Но есть и недостаток: для этого кода необходим дополнительный вызов **ExecuteQuery**, только чтобы получить значение, которое вы хотите проверить в операторе **if**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-232">But there is a disadvantage too: this code requires an extra call of **ExecuteQuery** solely to get the value you want to check in the **if** statement.</span></span> 

<span data-ttu-id="55ac2-233">Если мы используем этот способ в методе **CreateExpectedShipment**, чтобы проверить наличие списка, то этот метод получит два вызова **ExecuteQuery**, каждый из которых выполняет HTTP-запрос с удаленного веб-сервера в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="55ac2-233">If we use this technique in the **CreateExpectedShipment** method to check for the existence of the list, that method will have two calls of **ExecuteQuery**, each of which makes an HTTP request from the remote web server to SharePoint.</span></span> <span data-ttu-id="55ac2-234">Эти запросы потребляют большую часть времени в любом методе CSOM, поэтому их рекомендуется использовать как можно реже.</span><span class="sxs-lookup"><span data-stu-id="55ac2-234">These requests are the most time-consuming part of any CSOM method, so it is generally a good practice to minimize them.</span></span>

<span data-ttu-id="55ac2-235">Мы не будем изменять метод **CreateExpectedShipment**, но при разработке надстройки для рабочей среды вам придется обдумать, что должен делать ваш код, если компонент, на который он ссылается, удален.</span><span class="sxs-lookup"><span data-stu-id="55ac2-235">We will leave the **CreateExpectedShipment** method as is, but in a production add-in, you need to think about how your code is going to work if a component that it references is deleted.</span></span> <span data-ttu-id="55ac2-236">Один из вариантов — программное восстановление списка из корзины, но это будет раздражать пользователей, которые удалили список намеренно.</span><span class="sxs-lookup"><span data-stu-id="55ac2-236">Programmatically restoring the list from the Recycle Bin is one option, but that would annoy users who intentionally decided to delete the list.</span></span> 

<span data-ttu-id="55ac2-237">Кроме того, может оказаться, что лучший вариант — это ничего не делать для предотвращения исключения.</span><span class="sxs-lookup"><span data-stu-id="55ac2-237">You should also consider that doing nothing at all to prevent the exception might be the best choice.</span></span> <span data-ttu-id="55ac2-238">Исключение, полученное из SharePoint, будет предупреждать пользователей, что удаление списка нарушило работу части надстройки, причем пользователь, удаливший список, может и не осознавать этого.</span><span class="sxs-lookup"><span data-stu-id="55ac2-238">An exception from SharePoint would alert users that the deletion of the list has broken part of the add-in, which is something the person who deleted it might not have realized.</span></span> <span data-ttu-id="55ac2-239">После этого пользователь может попытаться восстановить список из корзины или продолжить работу без некоторых функций надстройки, которые больше не работают.</span><span class="sxs-lookup"><span data-stu-id="55ac2-239">A user can then decide whether to restore the list from the Recycle Bin or do without the part of the add-in functionality that no longer works.</span></span>

## <a name="request-permission-to-manage-the-website"></a><span data-ttu-id="55ac2-240">Запрос разрешения на управление веб-сайтом</span><span class="sxs-lookup"><span data-stu-id="55ac2-240">Request permission to manage the website</span></span>

<span data-ttu-id="55ac2-241">Вспомним, что когда надстройка запрашивает разрешение "Чтение" или "Запись" с областью "Список", SharePoint предлагает пользователю сделать надстройку доверенной. При этом диалоговое окно содержит раскрывающийся список, в котором пользователь может выбрать список, доступ к которому следует предоставить надстройке.</span><span class="sxs-lookup"><span data-stu-id="55ac2-241">Recall that when an add-in requests Read or Write permission with the scope of List, SharePoint prompts the user to trust the add-in, and the dialog contains a drop-down list where the user selects the list to which the add-in should have access.</span></span> <span data-ttu-id="55ac2-242">Можно выбрать только один список.</span><span class="sxs-lookup"><span data-stu-id="55ac2-242">Only one list can be selected.</span></span> <span data-ttu-id="55ac2-243">Но сейчас надстройка Chain Store записывает данные в два разных списка.</span><span class="sxs-lookup"><span data-stu-id="55ac2-243">But the Chain Store add-in now writes to two different lists.</span></span> <span data-ttu-id="55ac2-244">Чтобы получить доступ к нескольким спискам, надстройке необходимо запросить разрешение с областью "Интернет".</span><span class="sxs-lookup"><span data-stu-id="55ac2-244">To gain access to multiple lists, the add-in has to request permission with the scope of Web.</span></span> <span data-ttu-id="55ac2-245">Сделайте вот что:</span><span class="sxs-lookup"><span data-stu-id="55ac2-245">Follow these steps:</span></span>

1. <span data-ttu-id="55ac2-246">В **обозревателе решений** в проекте **ChainStore** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="55ac2-246">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>

2. <span data-ttu-id="55ac2-247">Откройте вкладку **Разрешения** и в поле **Область** в раскрывающемся списке выберите **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-247">Open the **Permissions** tab, and in the **Scope** field, select **Web** from the drop-down.</span></span>

3. <span data-ttu-id="55ac2-248">В поле **Разрешение** в раскрывающемся списке выберите пункт **Запись**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-248">In the **Permission** field, select **Write** from the drop-down.</span></span>

4. <span data-ttu-id="55ac2-249">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="55ac2-249">Save the file.</span></span> 

## <a name="run-the-add-in-and-test-the-item-creation"></a><span data-ttu-id="55ac2-250">Запуск надстройки и тестирование функции создания элемента</span><span class="sxs-lookup"><span data-stu-id="55ac2-250">Run the add-in and test the item creation</span></span>

1. <span data-ttu-id="55ac2-251">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="55ac2-251">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="55ac2-252">Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express.</span><span class="sxs-lookup"><span data-stu-id="55ac2-252">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="55ac2-253">Кроме того, он выполняет временную установку надстройки на вашем тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="55ac2-253">It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="55ac2-254">Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="55ac2-254">You are prompted to grant permissions to the add-in before its start page opens.</span></span> 

2. <span data-ttu-id="55ac2-255">Когда откроется начальная страница надстройки, в нижней части страницы щелкните ссылку **Order Form** (Форма заказа).</span><span class="sxs-lookup"><span data-stu-id="55ac2-255">When the add-in's start page opens, select the **Order Form** link at the bottom of the page.</span></span>

3. <span data-ttu-id="55ac2-256">Введите необходимые значения в форму и нажмите кнопку **Place Order** (Разместить заказ).</span><span class="sxs-lookup"><span data-stu-id="55ac2-256">Enter some values in the form, and then select **Place Order**.</span></span>

4. <span data-ttu-id="55ac2-257">С помощью кнопки "Назад" в браузере вернитесь на начальную страницу, а затем вверху на элементе управления хрома щелкните **Вернуться на сайт**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-257">Use the browser's back button to go back to the start page, and then select **Back to Site** on the chrome control at the top.</span></span>

5. <span data-ttu-id="55ac2-258">На начальной странице магазина в Гонконге выберите **Site Contents** (Содержание сайта) и откройте список **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="55ac2-258">From the home page of the Hong Kong store, go to **Site Contents** and open the **Expected Shipments** list.</span></span> <span data-ttu-id="55ac2-259">Теперь в списке есть элемент, соответствующий заказу.</span><span class="sxs-lookup"><span data-stu-id="55ac2-259">There is now an item on the list corresponding to the order.</span></span> <span data-ttu-id="55ac2-260">Ниже показан снимок экрана с примером.</span><span class="sxs-lookup"><span data-stu-id="55ac2-260">The following screenshot is an example.</span></span>
  
   <span data-ttu-id="55ac2-261">*Рис. 2. Список Expected Shipments (Ожидаемые отгрузки) с одним элементом*</span><span class="sxs-lookup"><span data-stu-id="55ac2-261">*Figure 2. Expected Shipments list with a single item*</span></span>

   ![Список Expected Shipments (Ожидаемые отгрузки) с одним элементом.](../images/e4285084-d31e-4e79-a469-ddebbc7dfb18.PNG)

6. <span data-ttu-id="55ac2-266">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55ac2-266">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="55ac2-267">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="55ac2-267">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

7. <span data-ttu-id="55ac2-268">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="55ac2-268">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55ac2-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55ac2-269">Next steps</span></span>
<span data-ttu-id="55ac2-270"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="55ac2-270"></span></span>

<span data-ttu-id="55ac2-271">В следующей статье вы узнаете, как придать удаленной форме заказа вид веб-части на странице SharePoint: [Добавление веб-части надстройки в надстройку, размещаемую у поставщика](include-an-add-in-part-in-the-provider-hosted-add-in.md)</span><span class="sxs-lookup"><span data-stu-id="55ac2-271">In the next article, you'll learn how to surface the remote Order Form as a Web Part on a SharePoint page: [Include an add-in part in the provider-hosted add-in](include-an-add-in-part-in-the-provider-hosted-add-in.md).</span></span>
 

 

