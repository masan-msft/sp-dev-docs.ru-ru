---
title: "Как создать приложение списка SharePoint для Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3e40c475-f4c1-4a4f-a3e5-1a55f814d272
ms.openlocfilehash: 79c763ceaa201007d9a43047c7e71ab0682a4e04
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-windows-phone-sharepoint-list-app"></a><span data-ttu-id="e5d64-102">Как: Создание приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="e5d64-102">How to: Create a Windows Phone SharePoint list app</span></span>
<span data-ttu-id="e5d64-p101">Создайте приложение Windows Phone в Visual Studio на основе шаблона приложения списка SharePoint для Windows Phone. Установка пакета SDK Windows Phone SharePoint предоставляет два шаблона приложения SharePoint для Windows Phone в Visual Studio 2010 или Visual Studio 2010 Express для Windows Phone. (  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)см). На основе шаблона приложения списка SharePoint для Windows Phone, можно следуйте указаниям мастера для создания функциональные приложения Windows Phone, которые можно получить доступ к и работы с данными в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p101">Create a Windows Phone app in Visual Studio based on the Windows Phone SharePoint List Application template. Installing the Windows Phone SharePoint SDK makes two Windows Phone SharePoint Application templates available to you in Visual Studio 2010 or Visual Studio 2010 Express for Windows Phone. (See  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).) Using the Windows Phone SharePoint List Application template, you can follow the steps of a wizard to create a functional Windows Phone app that can access and manipulate data in a SharePoint list.</span></span>


> <span data-ttu-id="e5d64-106">**Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="e5d64-106">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="e5d64-107">За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="e5d64-107">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="e5d64-108">> Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e5d64-108">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 


## <a name="create-the-windows-phone-sharepoint-list-application"></a><span data-ttu-id="e5d64-109">Создание приложения списка Windows Phone SharePoint</span><span class="sxs-lookup"><span data-stu-id="e5d64-109">Create the Windows Phone SharePoint list application</span></span>
<span data-ttu-id="e5d64-110"><a name="BKMK_CreatingSPListApplication"> </a></span><span class="sxs-lookup"><span data-stu-id="e5d64-110"></span></span>

<span data-ttu-id="e5d64-111">В приложении Windows Phone SharePoint списка можно получить доступ к большая часть списков, доступных в Надстройки SharePoint. Для целей, поставленных в этом примере приложения Windows Phone мы используем списков SharePoint с образцами данных из для вымышленной компании Contoso, Ltd. Для действия, чтобы создать первый итерации этого приложения списка SharePoint мы используем в список контактов SharePoint, который содержит сведения о членах группы маркетинга в компании Contoso, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="e5d64-111">In your Windows Phone SharePoint list app, you can access most of the lists that are available in SharePoint Add-ins. For the purposes of this sample Windows Phone app, we use SharePoint lists with sample data from a fictitious company named Contoso, Ltd. For the steps to create the first iteration of this SharePoint list app, we use a SharePoint Contacts list that contains information about members of a marketing team at Contoso, as shown in Figure 1.</span></span>
  
    
    

<span data-ttu-id="e5d64-112">**На рисунке 1. Список контактов для отдела маркетинга Contoso**</span><span class="sxs-lookup"><span data-stu-id="e5d64-112">**Figure 1. Contacts list for Contoso marketing team**</span></span>

  
    
    

  
    
    
![Список контактов для отдела маркетинга Contoso](../images/8d56d824-d96a-4f1e-9040-ce1da9a734d8.gif)
  
    
    

### <a name="to-create-a-windows-phone-sharepoint-list-app"></a><span data-ttu-id="e5d64-114">Создание приложения списка Windows Phone SharePoint</span><span class="sxs-lookup"><span data-stu-id="e5d64-114">To create a Windows Phone SharePoint list app</span></span>


1. <span data-ttu-id="e5d64-115">Запустите Visual Studio 2010 с параметром **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="e5d64-115">Start Visual Studio 2010 by using the **Run as Administrator** option.</span></span>
    
  
2. <span data-ttu-id="e5d64-116">Выберите **Файл**, **Создать**, **Проект**.</span><span class="sxs-lookup"><span data-stu-id="e5d64-116">Choose **File**, **New**, **Project**.</span></span> 
    
    <span data-ttu-id="e5d64-117">Отобразится диалоговое окно **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="e5d64-117">The **New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="e5d64-p103">В диалоговом окне **Новый проект** разверните узел **Visual C#** и затем выберите узел **Silverlight для окна телефона**. (Убедитесь, что требуемой версии .NET Framework 4.)</span><span class="sxs-lookup"><span data-stu-id="e5d64-p103">In the **New Project** dialog box, expand the **Visual C#** node, and then choose the **Silverlight for Window Phone** node. (Ensure that the target .NET Framework version is set to 4.)</span></span>
    
    > <span data-ttu-id="e5d64-120">**Примечание:** Шаблоны, установленные пакет SDK для Windows Phone SharePoint работает только в проектах C#.</span><span class="sxs-lookup"><span data-stu-id="e5d64-120">**Note:** The templates installed by the Windows Phone SharePoint SDK work only in C# projects.</span></span> <span data-ttu-id="e5d64-121">Шаблоны недоступны для проектов Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="e5d64-121">The templates are not available for Visual Basic projects.</span></span> 
4. <span data-ttu-id="e5d64-122">В области **Шаблоны** выберите шаблон **Приложения списка SharePoint для Windows Phone** и назначьте проекту имя, напримерContosoSPListApp.</span><span class="sxs-lookup"><span data-stu-id="e5d64-122">In the **Templates** pane, choose the **Windows Phone SharePoint List Application** template and give the project a name, such asContosoSPListApp.</span></span>
    
  
5. <span data-ttu-id="e5d64-p105">При запуске **Мастера приложений для телефона SharePoint**, может возникнуть ошибка, показано на рисунке 2. Эта ошибка происходит, когда учетная запись разработчик использует во время выполнения **Мастера приложений для телефона SharePoint** не имеет разрешений.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p105">While running the **SharePoint Phone Application Wizard**, the error shown in Figure 2 can occur. This error occurs because the account the developer is using while running the **SharePoint Phone Application Wizard** has insufficient permissions.</span></span>
    
   <span data-ttu-id="e5d64-125">**На рисунке 2. Сообщение об ошибке мастера SPList**</span><span class="sxs-lookup"><span data-stu-id="e5d64-125">**Figure 2. SPList wizard error message**</span></span>

  

  ![Ошибка мастера SPList](../images/SP15Con_CreateSharePointListAppsForWindowsPhoneFig3.png)
  

    <span data-ttu-id="e5d64-p106">Можно устранить эту ошибку, предоставляя ее недостаточно прав для учетной записи, с которым он работает мастера SPList. Повторно запустите **Мастер Splist** после присваивается достаточных прав.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p106">You can resolve this error by giving sufficient privileges to the account with which the developer is running the SPList wizard. Rerun **Splist wizard** after sufficient rights are given.</span></span>
    
  
6. <span data-ttu-id="e5d64-p107">Нажмите кнопку « **ОК** ». Откроется **Мастер приложений SharePoint телефона**. Используйте этот мастер для выбора списка SharePoint и настройка свойств этого списка, чтобы определить, как оно отображается в приложении Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p107">Choose the **OK** button. The **SharePoint Phone Application Wizard** appears. You use this wizard to choose a SharePoint list and configure properties of that list to determine how it appears in your Windows Phone app.</span></span>
    
  
7. <span data-ttu-id="e5d64-132">Укажите URL-адрес конечного сайта SharePoint в сети (то есть для локальной установки SharePoint Server ).</span><span class="sxs-lookup"><span data-stu-id="e5d64-132">Specify the URL of a target SharePoint site on your network (that is, an on-premises installation of SharePoint Server).</span></span>
    
  
8. <span data-ttu-id="e5d64-p108">Выберите **Поиск списков**. Если учетная запись, под которой выполняются Visual Studio имеет доступ к сайту указанный целевой, **Мастера приложений для телефона SharePoint** отображаются списки, доступные на этом узле.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p108">Choose **Find Lists**. If the account under which you are running Visual Studio has access to the specified target site, the **SharePoint Phone Application Wizard** displays the lists that are available on that site.</span></span>
    
  
9. <span data-ttu-id="e5d64-135">Выберите один из доступных списков, например, в список контактов (как показано с демонстрационными данными в настраиваемое представление на рис. 1).</span><span class="sxs-lookup"><span data-stu-id="e5d64-135">Select one of the available lists, such as a Contacts list (shown with sample data in a customized view in Figure 1).</span></span>
    
  
10. <span data-ttu-id="e5d64-p109">Нажмите кнопку **Далее**. Мастер отображает доступные представления, связанного с выбранного списка.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p109">Choose **Next**. The wizard displays the available views associated with the selected list.</span></span>
    
    <span data-ttu-id="e5d64-p110">Представления, отображаемые в мастере  эти представления, которые были созданы пользователями (или подготовить к работе с SharePoint Server ) и его связи с указанной списка на сервере. Некоторые списки SharePoint, имеют только один Просмотр, связанные с ними по умолчанию. В список контактов по умолчанию, связанного с представлением всех контактов. Список извещений, по умолчанию, связанного с представлением всех элементов. Списки задач, по умолчанию связан с шесть представления, включая все задачи представление и представление активных задач. Для каждого представления, выбранного на этом этапе в мастере элемент управления **PivotItem**, которая добавляется в элемент управления **Pivot** в XAML, определяющий пользовательский Интерфейс приложения Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p110">The views displayed by the wizard are those views that have been created by users (or provisioned by SharePoint Server) and associated with a given list on the server. Some SharePoint lists have only one view associated with them by default. A Contacts list, by default, is associated with an All Contacts view. An Announcements list, by default, is associated with an All Items view. A Tasks lists, by default, is associated with six views, including an All Tasks view and an Active Tasks view. For each view that you select at this stage in the wizard, a **PivotItem** control is created and added to the **Pivot** control in the XAML that defines the UI of the Windows Phone app.</span></span>
    
  
11. <span data-ttu-id="e5d64-144">Установите флажок рядом с каждым представлением, которое вы хотите включить в свое приложение Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e5d64-144">Select the check box next to each view you want to include in your Windows Phone app.</span></span>
    
  
12. <span data-ttu-id="e5d64-p111">Нажмите кнопку **Далее**. Мастер отображает доступные действия для выбранного списка в приложении Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p111">Choose **Next**. The wizard displays the available actions for the selected list in your Windows Phone app.</span></span>
    
    <span data-ttu-id="e5d64-p112">Доступны **New**, **отображаемое**, **Изменение** и **Удаление**. Если необходимо иметь возможность изменения и удаления элементов списка в приложении, необходимо выбрать операции **отображения** на этом этапе в мастере. (Флажки для операций, **Изменение** и **Удаление** отключены, если не выбран операции **отображения** ).</span><span class="sxs-lookup"><span data-stu-id="e5d64-p112">The choices are **New**, **Display**, **Edit**, and **Delete**. If you want to be able to edit or delete list items in your app, you must choose the **Display** operation at this stage in the wizard. (The check boxes for the **Edit** and **Delete** operations are disabled unless the **Display** operation is selected.)</span></span>
    
  
13. <span data-ttu-id="e5d64-150">Установите флажок рядом с каждой действие, которое должно иметь недоступны для выбранного списка в приложении Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e5d64-150">Select the check box next to each action you want to have available for the selected list in your Windows Phone app.</span></span>
    
  
14. <span data-ttu-id="e5d64-p113">Нажмите кнопку **Далее**. Мастер отображает поля, связанные с выбранного списка на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p113">Choose **Next**. The wizard displays the fields associated with the selected list on the SharePoint site.</span></span>
    
    > <span data-ttu-id="e5d64-153">**Примечание:** Настраиваемое поле не будет доступно для выбора из мастера создания списка SharePoint для мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="e5d64-153">**Note:** A custom field will not be available to select from the SharePoint List wizard for mobile devices.</span></span> <span data-ttu-id="e5d64-154">Тем не менее можно написать пользовательский код для доступа к любого настраиваемого поля.</span><span class="sxs-lookup"><span data-stu-id="e5d64-154">However, you can write custom code to access any custom field.</span></span> <span data-ttu-id="e5d64-155">Поле не может быть связана с типом контента.</span><span class="sxs-lookup"><span data-stu-id="e5d64-155">A field cannot be associated with its content type.</span></span> <span data-ttu-id="e5d64-156">Тем не менее если различные типы контента включены для списка, все поля будут доступны для разработчиков для использования в своих приложениях телефона.</span><span class="sxs-lookup"><span data-stu-id="e5d64-156">However if multiple content types are enabled for the list, all the fields will be available for developers to consume in their phone apps.</span></span> 
15. <span data-ttu-id="e5d64-157">Установите флажок рядом с пунктом каждого поля, которые необходимо включить в список, как оно будет отображаться в приложении Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e5d64-157">Select the check box next to each field you want to include in the list as it will appear in your Windows Phone app.</span></span>
    
    > <span data-ttu-id="e5d64-158">**Примечание:** Список полей, определенных в SharePoint Server в качестве сведения о необходимости установки выбраны уже; они не может быть снят в мастере.</span><span class="sxs-lookup"><span data-stu-id="e5d64-158">**Note:** List fields that are designated in SharePoint Server as requiring information are selected already; they can't be cleared in the wizard.</span></span> 
16. <span data-ttu-id="e5d64-p115">Нажмите кнопку **Далее**. Мастер предоставит вам возможность упорядочить выбранные ранее поля.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p115">Choose **Next**. The wizard gives you the opportunity to order the fields you selected in the previous step.</span></span>
    
  
17. <span data-ttu-id="e5d64-161">Упорядочьте поля в соответствии со своими потребностями, выбирая отдельные поля и перемещая их выше или ниже в списке с помощью стрелок.</span><span class="sxs-lookup"><span data-stu-id="e5d64-161">Order the fields according to your needs by selecting individual fields and moving them higher or lower in the order by choosing the up or down arrows.</span></span>
    
  
18. <span data-ttu-id="e5d64-p116">Нажмите кнопку **Готово**. Visual Studio создаст необходимые файлы для проекта и откроет файл List.xaml для редактирования.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p116">Choose **Finish**. Visual Studio creates the necessary files for the project and opens the List.xaml file for editing.</span></span>
    
  

## <a name="run-the-windows-phone-app-generated-by-the-sharepoint-phone-application-wizard"></a><span data-ttu-id="e5d64-164">Запустите приложение Windows Phone, созданных с помощью мастера приложений SharePoint телефона</span><span class="sxs-lookup"><span data-stu-id="e5d64-164">Run the Windows Phone app generated by the SharePoint Phone Application Wizard</span></span>
<span data-ttu-id="e5d64-165"><a name="BKMK_RunningApp"> </a></span><span class="sxs-lookup"><span data-stu-id="e5d64-165"></span></span>

<span data-ttu-id="e5d64-p117">Можно создать проект, созданный с помощью **Мастера приложений для телефона SharePoint**, как создавать простые, но функциональные приложения списка Windows Phone SharePoint. Мы можем изменить и разработка приложения дальнейшей, но, пока пользователь может коснитесь (или, в эмуляторе Windows Phone, нажмите кнопку) элемент заданного списка и приложение отображает все поля, связанный с этим элементом (поля, выбранные в мастере для включения в приложение). Пользователь также можно добавлять элементы, удаление элементов списка и изменить значения полей для элементов списка. Вход в систему несколько пользователей в одном приложении не поддерживается. Тем не менее разработчик можно написать код, завершите сеанс текущего пользователя, когда другой пользователь попытается войти в одном мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p117">The project generated by the **SharePoint Phone Application Wizard** can be built as it is to create a simple but functional Windows Phone SharePoint list app. We can modify and develop the app further, but, for now, a user can tap (or, in the Windows Phone Emulator, click) a given list item and the app displays all the fields associated with that item (those fields that you selected in the wizard to include in the app). A user can also add new list items, delete list items, and edit the field values for list items. Multiple-user logon in a single app is not supported. However, a developer can write code that logs off the current user when another user tries to log on to the same mobile app.</span></span>
  
    
    
<span data-ttu-id="e5d64-p118">Цель развертывания для решения по умолчанию имеет значение эмулятора Windows Phone. Можно запустить проект в Visual Studio как есть (при нажатии клавиши F5 для запуска проекта в контексте отладчик или нажав сочетание клавиш CTRL + F5 для запуска проекта без отладки). Запуск эмулятора Windows Phone, ОС Windows Phone и развернуть в эмуляторе и работы приложения. При запуске с кодом, созданного с помощью мастера при запуске приложения списка SharePoint в эмуляторе, выводится запрос учетных данных для указанного списка SharePoint на целевом сайте. Укажите учетные данные учетной записи, имеющей достаточные разрешения для доступа к списку и выберите команду **Вход в систему** в эмуляторе. На главную страницу приложения Windows Phone (определяется с помощью файла List.xaml в проекте) отображается в эмуляторе. В зависимости от выбранных полей и порядке, в котором были введены для тех полях на предыдущих шагах вы должны увидеть элементы из указанного списка. На основе данных в список, представленный на рисунке 1, вы увидите список элементов в эмуляторе, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p118">The deployment target for the solution is set to Windows Phone Emulator by default. You can run the project in Visual Studio as it is (either by pressing F5 to start the project in the context of the debugger or by pressing CTRL+F5 to start the project without debugging). The Windows Phone Emulator is launched, the Windows Phone operating system is loaded, and your app is deployed to the emulator and started. If you start with the code as it is generated by the wizard, when your SharePoint list app runs in the emulator, you're asked for credentials for the specified SharePoint list on the target site. Provide the credentials for an account that has sufficient permissions to access the list and choose **Log On** in the emulator. The main page of the Windows Phone app (defined by the List.xaml file in the project) is displayed in the emulator. Depending on the fields you chose and the order you specified for those fields in the previous steps, you should see items from the specified list. Based on the data in the list represented by Figure 1, you would see a list of items in the emulator as shown in Figure 3.</span></span>
  
    
    

<span data-ttu-id="e5d64-179">**На рисунке 3. Элементы списка SharePoint в приложении Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="e5d64-179">**Figure 3. SharePoint list items in a Windows Phone app**</span></span>

  
    
    

  
    
    
![Элементы списка SharePoint в приложении Windows Phone](../images/9159345c-ce12-41a6-8994-fc2e9aa26fd6.gif)
  
    
    
<span data-ttu-id="e5d64-p119">При выполнении приложения Windows Phone, может возникнуть ошибка проверки подлинности, показано на рисунке 4. Это вызвано тем, что мобильного приложения SharePoint требуется **Обычная проверка подлинности форм**; Это не включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p119">While running a Windows Phone app, the authentication error shown in Figure 4 can occur. This happens because the SharePoint mobile app requires **Basic Form Authentication**; this isn't enabled by default.</span></span>
  
    
    

<span data-ttu-id="e5d64-183">**На рисунке 4. Ошибка проверки подлинности приложения Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="e5d64-183">**Figure 4. Windows Phone app authentication error**</span></span>

  
    
    

  
    
    
![Ошибка мобильного приложения](../images/SP15Con_CreateSharePointListAppsForWindowsPhoneFig4.png)
  
    
    
<span data-ttu-id="e5d64-185">Можно устранить эту ошибку, Выбор метода **проверки подлинности базовой формы** из центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="e5d64-185">You can resolve this error by choosing **Basic form authentication** from Central Administration.</span></span>
  
    
    

### <a name="to-enable-basic-form-authentication"></a><span data-ttu-id="e5d64-186">Для включения проверки подлинности базовой формы</span><span class="sxs-lookup"><span data-stu-id="e5d64-186">To enable Basic form authentication</span></span>


1. <span data-ttu-id="e5d64-187">Перейдите в **Центр администрирования**; Убедитесь, что имеются права администратора на сервере.</span><span class="sxs-lookup"><span data-stu-id="e5d64-187">Navigate to **Central Administration**; ensure you have admin rights on server.</span></span>
    
  
2. <span data-ttu-id="e5d64-188">Выберите пункт **Управление веб-приложениями** в разделе **Управление приложениями**.</span><span class="sxs-lookup"><span data-stu-id="e5d64-188">Choose **Manage Web Applications** under **Application Management**.</span></span>
    
  
3. <span data-ttu-id="e5d64-189">Выберите веб-приложения (на котором имеется свой сайт SharePoint, который вы получаете доступ к мобильного приложения).</span><span class="sxs-lookup"><span data-stu-id="e5d64-189">Choose your web application (on which you have your SharePoint site, which you are accessing from your mobile app).</span></span>
    
  
4. <span data-ttu-id="e5d64-190">Выберите **Поставщики проверки подлинности** с помощью ленты.</span><span class="sxs-lookup"><span data-stu-id="e5d64-190">Choose **Authentication Providers** from the ribbon.</span></span>
    
  
5. <span data-ttu-id="e5d64-191">Выберите **Поставщики проверки подлинности** с помощью ленты.</span><span class="sxs-lookup"><span data-stu-id="e5d64-191">Choose **Authentication Providers** from the ribbon.</span></span>
    
  
6. <span data-ttu-id="e5d64-192">В диалоговом окне **Поставщика проверки подлинности** выберите команду Изменение параметров проверки подлинности **по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="e5d64-192">In the **Authentication Provider** dialog box, choose **Default** to Edit Authentication.</span></span>
    
  
7. <span data-ttu-id="e5d64-193">В окне **Изменение параметров проверки подлинности** модели выберите **Простая проверка подлинности** в разделе типы **Проверки подлинности на основе утверждений**.</span><span class="sxs-lookup"><span data-stu-id="e5d64-193">In the **Edit Authentication** model window, choose **Basic Authentication** under **Claims Authentication** types.</span></span>
    
  
<span data-ttu-id="e5d64-p120">Если вы свое приложение Windows Phone на основе данных из списка контактов, как показано на рисунке 1, можно выбрать элемент списка и приложение отображает страницу представления (определяется DisplayForm.xaml в проекте) элемента отображение всех полей, доступных для элемента в приложении, как показано на рисунке 5. (В данном примере все поля, связанные со списком контактов SharePoint были выбраны в мастере приложений SharePoint телефона и хранения по умолчанию порядка полей).</span><span class="sxs-lookup"><span data-stu-id="e5d64-p120">If you based your Windows Phone app on the data from a Contacts list, as shown in Figure 1, you can choose a particular list item and the app presents a page with a view of the item (defined by DisplayForm.xaml in the project) showing all the fields available for the item in the app, as in Figure 5. (For this example, all the fields associated with a SharePoint Contacts list were selected in the SharePoint Phone Application Wizard and the default order of those fields was retained.)</span></span>
  
    
    

<span data-ttu-id="e5d64-196">**На рисунке 5. Представление DisplayForm элемента списка контактов**</span><span class="sxs-lookup"><span data-stu-id="e5d64-196">**Figure 5. DisplayForm view of a Contacts list item**</span></span>

  
    
    

  
    
    
![Представление DisplayForm элемента списка контактов](../images/e2cf6848-bd29-416b-b397-a1d670bd2910.gif)
  
    
    
<span data-ttu-id="e5d64-p121">Обратите внимание, **Изменение** и **Удаление** кнопки на панели приложения в эту страницу приложения. Эти операции для вас реализуются методы в Microsoft.SharePoint.Phone.Application.dll (по одной из библиотек, установленных с пакет SDK для Windows Phone SharePoint). Если нажмите кнопку **Изменить**, отображается элемент управления **Page** Windows Phone (то есть объект, полученные из класса, наследуемого от класса **Microsoft.Phone.Controls.PhoneApplicationPage** ). Если изменение полей и нажмите кнопку **Отправить** на странице, в приложение выполняется метод **UpdateItem** базового класса **EditItemViewModelBase** (, в конечном счете, выполняет метод **Update** объекта **ListItem** из объектной модели клиента SharePoint Silverlight) для сохранения изменений в список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e5d64-p121">Notice the **Edit** and **Delete** buttons on the Application Bar in this page of the app. These operations are implemented for you by methods in Microsoft.SharePoint.Phone.Application.dll (which is one of the libraries installed by the Windows Phone SharePoint SDK). If you choose the **Edit** button, a Windows Phone **Page** control (that is, an object instantiated from a class that inherits from the **Microsoft.Phone.Controls.PhoneApplicationPage** class) is displayed. If you edit any of the fields and choose the **Submit** button on that page in the app, the underlying **UpdateItem** method of the **EditItemViewModelBase** class is executed (which, ultimately, executes the **Update** method of a **ListItem** object from the SharePoint Silverlight client object model) to save your changes to the SharePoint list.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="e5d64-202">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e5d64-202">Additional resources</span></span>
<span data-ttu-id="e5d64-203"><a name="SP15Createwinphoneapp_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e5d64-203"></span></span>


-  [<span data-ttu-id="e5d64-204">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="e5d64-204">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="e5d64-205">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="e5d64-205">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="e5d64-206">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="e5d64-206">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="e5d64-207">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="e5d64-207">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="e5d64-208">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="e5d64-208">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="e5d64-209">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="e5d64-209">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

