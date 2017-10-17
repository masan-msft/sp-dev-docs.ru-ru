---
title: "Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: aa5e03efbb6af2e86f29aa10fbca0f883c0c3427
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in"></a><span data-ttu-id="bd91f-102">Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-102">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>
<span data-ttu-id="bd91f-103">В этой статье рассказывается, как добавить команды для настраиваемых кнопок ленты на хост-сайте надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bd91f-103">Add custom ribbon button commands to the host web of a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="bd91f-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="bd91f-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="bd91f-107">Это девятая часть серии статей, посвященной основам разработки надстроек, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="bd91f-107">This is the ninth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="bd91f-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="bd91f-109">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="bd91f-110">Добавление настраиваемых столбцов в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in.md)
    
 
-  [<span data-ttu-id="bd91f-111">Добавление настраиваемого типа контента в надстройки, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in.md)
    
 
-  [<span data-ttu-id="bd91f-112">Добавление веб-части на страницу в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="bd91f-113">Добавление рабочего процесса в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-113">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="bd91f-114">Добавление настраиваемой страницы и стиля для надстройки с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-114">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="bd91f-115">Добавление настраиваемой клиентской обработки в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bd91f-115">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
    
 

 <span data-ttu-id="bd91f-p102">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeRibbon.sln.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p102">**Note**  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeRibbon.sln file.</span></span>
 

<span data-ttu-id="bd91f-p103">Любую надстройку SharePoint можно запустить на странице **Содержимое сайта** хост-сайта. Для этого достаточно щелкнуть плитку необходимой надстройки. Кроме того, функциональность надстройки SharePoint можно сделать доступной на хост-сайте с помощью дополнительных действий, которые представляют собой настраиваемые кнопки ленты или настраиваемые элементы меню. В процессе изучения этой статьи вы добавите кнопку на ленту хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p103">All SharePoint Add-ins can be run from the  **Site Contents** page of the host web by clicking the add-in's tile. The functionality of a SharePoint Add-in can also be exposed on the host web through custom actions, which are custom ribbon buttons or custom menu items. In this article you add a button to the ribbon on a host web.</span></span>
 

## <a name="prepare-the-host-web"></a><span data-ttu-id="bd91f-121">Подготовка хост-сайта</span><span class="sxs-lookup"><span data-stu-id="bd91f-121">Prepare the host web</span></span>

<span data-ttu-id="bd91f-p104">Ниже показано, как добавить кнопку на ленту календаря на хост-сайте. В пользовательском интерфейсе сайта разработчика SharePoint выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p104">You will add the button to the ribbon of a calendar on the host web. Take the following steps in the UI of your SharePoint developer site.</span></span>
 

 

1. <span data-ttu-id="bd91f-124">На домашней странице сайта выберите пункты **Содержимое сайта** > **добавить надстройку** > **Календарь**.</span><span class="sxs-lookup"><span data-stu-id="bd91f-124">From the home page of the site, choose  **Site Contents** > **add and add-in** > **Calendar**.</span></span>
    
 
2. <span data-ttu-id="bd91f-125">В диалоговом окне **Добавление календаря** в поле **Имя** введите Employee Orientation Schedule (Расписание вводного обучения для сотрудников), а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bd91f-125">On the  **Adding Calendar** dialog, typeEmployee Orientation Schedule for the **Name**, and then choose  **Create**.</span></span>
    
 
3. <span data-ttu-id="bd91f-126">Когда откроется календарь, наведите указатель на любую дату, чтобы на ней появилась ссылка **Add** (Добавить), и перейдите по этой ссылке.</span><span class="sxs-lookup"><span data-stu-id="bd91f-126">When the calendar opens, put the cursor on any date until the  **Add** link appears on the date, and then click **Add**.</span></span> 
    
 
4. <span data-ttu-id="bd91f-p105">В диалоговом окне **Employee Orientation Schedule - New Item** (Расписание вводного обучения для сотрудников: новый элемент) введите "Orient Cassi Hicks" (Вводное обучение Cassi Hicks) в поле **Title** (Название). В остальных полях оставьте значения, заданные по умолчанию, а затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="bd91f-p105">On the  **Employee Orientation Schedule - New Item** dialog, typeOrient Cassi Hicks for the **Title**. Leave the other fields at their defaults and click  **Save**.</span></span>
    
    <span data-ttu-id="bd91f-129">Календарь должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="bd91f-129">The calendar should look similar to the following:</span></span>
    

    <span data-ttu-id="bd91f-130">**Настраиваемый календарь**</span><span class="sxs-lookup"><span data-stu-id="bd91f-130">**Custom calendar**</span></span>

 

  ![Календарь Employee Orientation Schedule (Расписание вводного обучения для сотрудников), где в элементе "1 июня" указано Orient Cassie Hicks (Вводное обучение для пользователя Cassi Hicks)](../images/d2066862-41c1-424d-9bfb-b6c5342bcf2c.PNG)
 

 

 

 

 

 <span data-ttu-id="bd91f-p106">**Важно!** Для выполнения следующей процедуры необходимо, чтобы календарь отображался в пользовательском интерфейсе Visual Studio. Но его не будет видно, если в момент создания календаря Visual Studio будет открыт. Прежде чем продолжить, закройте Visual Studio, окна браузера и консоли PowerShell, с помощью которых вы входили на сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p106">**Important**  The next procedure requires that the calendar be visible in the UI of Visual Studio, but it won't be if If Visual Studio was open when you created the calendar. Before you continue, close Visual Studio and also log out of any browser windows and PowerShell consoles where you are logged into your developer site.</span></span>
 


## <a name="add-a-ribbon-custom-action"></a><span data-ttu-id="bd91f-134">Добавление дополнительного действия на ленте</span><span class="sxs-lookup"><span data-stu-id="bd91f-134">Add a ribbon custom action</span></span>


1. <span data-ttu-id="bd91f-p107">В **обозревателе решений** щелкните правой кнопкой мыши проект **EmployeeOrientation** (Вводное обучение для сотрудников) и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие ленты**. Присвойте новому элементу имя RunOrientationAdd-in и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p107">In  **Solution Explorer**, right-click the  **EmployeeOrientation** project, and choose **Add** > **New Item** > **Office/SharePoint** > **Ribbon Custom Action**. Name it RunOrientationAdd-in, and then choose  **Add**.</span></span>
    
 
2. <span data-ttu-id="bd91f-p108">**Мастер настраиваемого действия для ленты** задаст вам несколько вопросов. Ответьте на них, используя таблицу ниже.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p108">The  **Create Custom Action for Ribbon** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    

|<span data-ttu-id="bd91f-139">**Вопрос для свойства**</span><span class="sxs-lookup"><span data-stu-id="bd91f-139">**Property question**</span></span>|<span data-ttu-id="bd91f-140">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bd91f-140">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bd91f-141">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="bd91f-141">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="bd91f-142">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="bd91f-142">Choose  **Host Web**.</span></span>|
|<span data-ttu-id="bd91f-143">Какова область для дополнительного действия?</span><span class="sxs-lookup"><span data-stu-id="bd91f-143">Where is the custom action scoped to?</span></span>|<span data-ttu-id="bd91f-144">Выберите вариант **Экземпляр списка** (*не* "Шаблон списка").</span><span class="sxs-lookup"><span data-stu-id="bd91f-144">Choose  **List Instance** ( *not*  List Template).</span></span>|
|<span data-ttu-id="bd91f-145">К какому элементу относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="bd91f-145">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="bd91f-146">Выберите вариант **Employee Orientation Schedule** (Расписание вводного обучения для сотрудников).</span><span class="sxs-lookup"><span data-stu-id="bd91f-146">Choose  **Employee Orientation Schedule**.</span></span>|
|<span data-ttu-id="bd91f-147">Где находится элемент управления?</span><span class="sxs-lookup"><span data-stu-id="bd91f-147">Where is the control located?</span></span>|<span data-ttu-id="bd91f-p109">Не используйте варианты из раскрывающегося списка. Вместо этого введите **Ribbon.Calendar.Events.Actions.Controls._children**. (Третья часть, **Events**, идентифицирует вкладку на ленте, а четвертая часть, **Actions**, — группу кнопок.)</span><span class="sxs-lookup"><span data-stu-id="bd91f-p109">Do not use the drop down selections. Instead, type  **Ribbon.Calendar.Events.Actions.Controls._children**. (The third part,  **Events**, identifies the tab of the ribbon, and the fourth part,  **Actions**, identifies the button group.)</span></span>|
|<span data-ttu-id="bd91f-151">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="bd91f-151">What is the text on the menu item?</span></span>|<span data-ttu-id="bd91f-152">Введите **Employee Orientation** (Вводное обучение для сотрудников).</span><span class="sxs-lookup"><span data-stu-id="bd91f-152">Type  **Employee Orientation**.</span></span>|
|<span data-ttu-id="bd91f-153">Куда будет вести дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="bd91f-153">Where does the custom action navigate to?</span></span>|<span data-ttu-id="bd91f-p110">Не используйте варианты из раскрывающегося списка. Вместо этого введите **~appWebUrl/Lists/NewEmployeesInSeattle**. Это страница представления списка, который находится на сайте надстройки, поэтому кнопка на ленте на хост-сайте открывает страницу на сайте надстройки.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p110">Do not use the drop down selections. Instead, type  **~appWebUrl/Lists/NewEmployeesInSeattle**. This is the list view page for the list, which is on the add-in web, so the ribbon button on the host web opens a page on the add-in web.</span></span>|
3. <span data-ttu-id="bd91f-157">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="bd91f-157">Choose  **Finish**.</span></span> 
    
 

## <a name="inspect-the-add-in-web-feature"></a><span data-ttu-id="bd91f-158">Проверка компонента сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="bd91f-158">Inspect the add-in web Feature</span></span>

<span data-ttu-id="bd91f-p111">В **обозревателе решений** разверните узел **Компоненты** и выберите компонент **NewEmployeeOrientationComponents**. Откроется конструктор компонентов.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p111">In  **Solution Explorer**, expand the  **Features** folder and choose the **NewEmployeeOrientationComponents** feature. The Feature designer opens.</span></span>
 

 
<span data-ttu-id="bd91f-p112">Обратите внимание, что созданное вами дополнительное действие **RunOrientationAdd-in** находится в списке **Элементы в решении**, а не в списке **Элементы в компоненте**. Это связано с тем, что компонент развернут на сайте надстройки, а ваше дополнительное действие — на хост-сайте. Когда вы создаете пакет надстройки в Visual Studio для развертывания в рабочей среде или нажимаете клавишу F5 в Visual Studio, пакет Инструменты разработчика Office для Visual Studio создает особый компонент хост-сайта, добавляет в него дополнительное действие и развертывает его на хост-сайте. Ни в коем случае не следует изменять компонент хост-сайта. Именно поэтому он не будет создан до момента формирования пакета.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p112">Notice that the custom action that you created,  **RunOrientationAdd-in**, is listed in  **Items in the solution**, but not in  **Items in the feature**. This is because the Feature is deployed to the add-in web, but your custom action is deployed to the host web. When you package the add-in in Visual Studio for deployment to production, or when you press F5 in Visual Studio, the Office Developer Tools for Visual Studio creates a special host web Feature, adds the custom action to it, and deploys it to the host web. You should never edit the host web Feature. That is why it is not created until packaging-time.</span></span>
 

 

<span data-ttu-id="bd91f-166">**Конструктор компонентов**</span><span class="sxs-lookup"><span data-stu-id="bd91f-166">**Feature designer**</span></span>

 

 
![Конструктор компонентов со столбцами "Элементы в решении" и "Элементы в компоненте". "Надстройка запуска адаптации" находится в первом, а не во втором столбце.](../images/49ea0bf0-2cfa-4070-aa65-24b4a9c5e874.PNG)
 

 

 

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="bd91f-169">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="bd91f-169">Run and test the add-in</span></span>


 

 

1. <span data-ttu-id="bd91f-p114">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p114">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
    
 
2. <span data-ttu-id="bd91f-p115">Откроется страница надстройки SharePoint, указанная по умолчанию. Перейдите на начальную страницу сайта разработчика (то есть хост-сайта). Ссылка на него расположена в левом верхнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p115">The default page of the SharePoint Add-in opens. Navigate to the home page of your developer site (which is the host web). There is a breadcrumb link to it in the upper left of the page.</span></span>
    
 
3. <span data-ttu-id="bd91f-175">На домашней странице хост-сайта щелкните **Содержимое сайта**, а затем на странице **Содержимое сайта** щелкните календарь **Employee Orientation Schedule** (Расписание вводного обучения для сотрудников). Обратите внимание, что надстройку **Employee Orientation** (Вводное обучение для сотрудников) выбирать не надо.</span><span class="sxs-lookup"><span data-stu-id="bd91f-175">On the host web's home page, choose  **Site Contents**, and on the  **Site Contents** page, click the **Employee Orientation Schedule** calendar (not the **Employee Orientation** add-in).</span></span>
    
 
4. <span data-ttu-id="bd91f-p116">Когда откроется календарь, щелкните событие **Orient Cassie Hicks** (Вводное обучение для пользователя Cassi Hicks). Если вкладка **События** на ленте не открылась автоматически, откройте ее. Она должна выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p116">When the calendar opens, click the event  **Orient Cassie Hicks**. If the  **Events** tab on the ribbon doesn't open automatically, open it. It should look similar to the following:</span></span>
    
    <span data-ttu-id="bd91f-179">**Вкладка ленты "События" с настраиваемой кнопкой**</span><span class="sxs-lookup"><span data-stu-id="bd91f-179">**Events ribbon tab with custom button**</span></span>

 

  ![Лента "События" с настраиваемой кнопкой Employee Orientation (Вводное обучение для сотрудников).](../images/916ecbba-11ff-45b6-a8e9-ba717ae6fe0b.png)
 

 

 
5. <span data-ttu-id="bd91f-p117">В группе **Действия** на ленте выберите элемент **Employee Orientation** (Вводное обучение для сотрудников). Откроется представление списка **New Employees in Seattle** (Новые сотрудники в Сиэтле).</span><span class="sxs-lookup"><span data-stu-id="bd91f-p117">In the  **Actions** group on the ribbon, click **Employee Orientation**. The list view page for  **New Employees in Seattle** opens.</span></span>
    
 
6. <span data-ttu-id="bd91f-p118">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p118">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
7. <span data-ttu-id="bd91f-p119">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="bd91f-p119">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="bd91f-187"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="bd91f-187"></span></span>

<span data-ttu-id="bd91f-188">Из следующей статьи этой серии вы узнаете, как добавить JavaScript в надстройку SharePoint и получить доступ к данным SharePoint с помощью объектной модели JavaScript для SharePoint. Название этой статьи:  [Использование API JavaScript для SharePoint для работы с данными SharePoint](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).</span><span class="sxs-lookup"><span data-stu-id="bd91f-188">In the next article in this series, you'll add JavaScript to the SharePoint Add-in and access SharePoint data with SharePoint's JavaScript object model:  [Use the SharePoint JavaScript APIs to work with SharePoint data](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).</span></span>
 

 

