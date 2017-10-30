---
title: "Обзор шаблонов приложений Windows Phone SharePoint в Visual Studio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6ae27957-fa41-4e6f-92e3-db11dae1f6c2
ms.openlocfilehash: c1cd9e144b5fa71d64b0a3bac46420bcc86c8b85
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="overview-of-windows-phone-sharepoint-application-templates-in-visual-studio"></a><span data-ttu-id="93353-102">Обзор шаблонов приложений Windows Phone SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93353-102">Overview of Windows Phone SharePoint application templates in Visual Studio</span></span>
<span data-ttu-id="93353-103">Узнайте о шаблонах Visual Studio, установленных с помощью пакета SDK SharePoint для Windows Phone для разработки мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="93353-103">Learn about the Visual Studio templates installed by the Windows Phone SharePoint Software Development Kit for mobile app development.</span></span>
## <a name="templates-installed-by-the-windows-phone-sharepoint-software-development-kit"></a><span data-ttu-id="93353-104">Шаблоны, установленные с средств разработки программного обеспечения для Windows Phone SharePoint</span><span class="sxs-lookup"><span data-stu-id="93353-104">Templates installed by the Windows Phone SharePoint Software Development Kit</span></span>
<span data-ttu-id="93353-105"><a name="BKMK_TemplatesInstalled"> </a></span><span class="sxs-lookup"><span data-stu-id="93353-105"></span></span>

<span data-ttu-id="93353-106">После того как настроить среду разработки и установить Windows Phone SharePoint Software Development Kit (SDK) две дополнительные шаблоны Silverlight для Windows Phone, доступны для проектов:</span><span class="sxs-lookup"><span data-stu-id="93353-106">After you set up your development environment and install the Windows Phone SharePoint Software Development Kit (SDK), two additional Silverlight for Windows Phone templates are available for projects:</span></span>
  
    
    

- <span data-ttu-id="93353-107">Шаблон приложения пустой SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93353-107">The Windows Phone Empty SharePoint Application template</span></span>
    
  
- <span data-ttu-id="93353-108">Шаблон приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93353-108">The Windows Phone SharePoint List Application template</span></span>
    
  
<span data-ttu-id="93353-p101">На данный момент эти шаблоны предназначены для использования только в проектах C#. Они недоступны для Visual Basic проектов. Тем не менее, для использования в Visual Studio 2012 и Visual Studio Express 2012 для Windows Phone 8 и Visual Studio 2010 и Visual Studio 2010, экспресс-выпуск для Windows Phone 7 доступны шаблоны.</span><span class="sxs-lookup"><span data-stu-id="93353-p101">Currently, these templates are designed to be used only in C# projects. They are not available for Visual Basic projects. The templates are available, however, for use in Visual Studio 2012 and Visual Studio Express 2012 for Windows Phone 8 and in Visual Studio 2010 and Visual Studio 2010 Express for Windows Phone 7.</span></span>
  
    
    

> <span data-ttu-id="93353-112">**Примечание:** Шаблоны Windows Phone SharePoint не отображаются в меню **Создать проект** Expression Blend.</span><span class="sxs-lookup"><span data-stu-id="93353-112">**Note:** Windows Phone SharePoint templates don't appear in the **New Project** menu of Expression Blend.</span></span> <span data-ttu-id="93353-113">Тем не менее можно изменить проект в Expression Blend, выбрав команду **Открыть в выражении Blend** контекстное меню в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93353-113">However, you can edit a project in Expression Blend by choosing **Open in Expression Blend** from a shortcut menu in Visual Studio.</span></span>
  
    
    

<span data-ttu-id="93353-114">При создании проекта, основанного на один из этих шаблонов, пользователь не получает выбрать целевой платформы Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="93353-114">When you create a project based on either one of these templates, you are not given the option of choosing a target Windows Phone platform.</span></span> <span data-ttu-id="93353-115">Как для проектов, созданных в Visual Studio Express 2012 с помощью конечных Windows Phone 8 эти шаблоны приложений с SharePoint; И ОС Windows Phone 7.1 версии по умолчанию, предназначенных для проектов, созданных в Visual Studio 2010 Express с помощью этих шаблонов, атрибут **AppPlatformVersion** элемента **развертывания** в файле WMAppManifest.xml имеет значение 7.1.</span><span class="sxs-lookup"><span data-stu-id="93353-115">As for projects created from Visual Studio Express 2012 using these templates target Windows Phone 8 applications against SharePoint ; And projects created from Visual Studio 2010 Express using these templates target Windows Phone OS version 7.1 by default That is, the **AppPlatformVersion** attribute of the **Deployment** element in the WMAppManifest.xml file has a value of 7.1.</span></span>
  
    
    



```XML

<Deployment xmlns="http://schemas.microsoft.com/windowsphone/2009/deployment" AppPlatformVersion="7.1">
```


> <span data-ttu-id="93353-116">**Примечание:** Дополнительные сведения о параметрах в файле WMAppManifest.xml видеть [Приложения манифест файла для Windows Phone](http://msdn.microsoft.com/en-us/library/ff769509.aspx).</span><span class="sxs-lookup"><span data-stu-id="93353-116">**Note:** For more information about settings in the WMAppManifest.xml file, see  [Application Manifest File for Windows Phone](http://msdn.microsoft.com/en-us/library/ff769509.aspx).</span></span> 
  
    
    


## <a name="starting-a-project-based-on-the-windows-phone-empty-sharepoint-application-template"></a><span data-ttu-id="93353-117">Запуск проекта на основе шаблона пустой SharePoint приложения Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93353-117">Starting a project based on the Windows Phone Empty SharePoint Application template</span></span>
<span data-ttu-id="93353-118"><a name="BKMK_EmptySPAppTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="93353-118"></span></span>

<span data-ttu-id="93353-119">При создании проекта Visual Studio на основе шаблона пустой SharePoint приложения Windows Phone, начала проекта похож на проект, созданный с помощью базового шаблона приложения для Windows Phone (устанавливается по Windows Phone SDK 7.1), с добавлением ссылок на библиотеки DLL, установленных с Windows Phone пакет SDK для SharePoint (Microsoft.SharePoint.Client.Phone.dll, Microsoft.SharePoint.Client.Phone.Auth.UI и Microsoft.SharePoint.Client.Phone.Runtime.dll, как показано на рисунке 1) и некоторые другие при изменении конфигурации.</span><span class="sxs-lookup"><span data-stu-id="93353-119">If you create a Visual Studio project based on the Windows Phone Empty SharePoint Application template, the starting project is similar to a project created by using the basic Windows Phone Application template (installed by the Windows Phone SDK 7.1), with the addition of references to DLLs installed by the Windows Phone SharePoint SDK (Microsoft.SharePoint.Client.Phone.dll, Microsoft.SharePoint.Client.Phone.Auth.UI, and Microsoft.SharePoint.Client.Phone.Runtime.dll as shown in Figure 1) and a few other reconfigurations.</span></span>
  
    
    

> <span data-ttu-id="93353-120">**Примечание:** Шаблоны доступны для Windows Phone 8 в Visual Studio Express 2012.</span><span class="sxs-lookup"><span data-stu-id="93353-120">**Note:** The same templates are available for Windows Phone 8 in Visual Studio Express 2012.</span></span> 
  
    
    


<span data-ttu-id="93353-121">**На рисунке 1. Файлы в Windows Phone пустой проект приложения SharePoint**</span><span class="sxs-lookup"><span data-stu-id="93353-121">**Figure 1. Files in a Windows Phone Empty SharePoint Application project**</span></span>

  
    
    

  
    
    
![Пустой проект приложения SharePoint для Windows Phone](../images/SP15_OverviewOfWinPhoneSPTemplatesInVisualStudio_fig1.PNG)
  
    
    
<span data-ttu-id="93353-p104">В проекте на основе шаблона пустой SharePoint приложения Windows Phone это стандартные файлы приложения Silverlight Windows Phone. Файл MainPage.xaml содержит объявления XAML, которые составляют пользовательского интерфейса (UI) приложения. Файл фонового кода, файл MainPage.xaml.cs, связан с файла MainPage.xaml с помощью механизма разделяемых классов, как и другие файлы кода в проекте. (  [Фонового кода и разделяемых классов](http://msdn.microsoft.com/en-us/library/cc221357.aspx)см). Файл MainPage.xaml.cs содержит процедурный код, реализующий логику для поддержки операций и события в пользовательском Интерфейсе. Файл App.xaml представляет общий приложение Windows. Файл выделенным кодом App.xaml.cs, включает в себя процедурного кода для обработки событий жизненного цикла для приложения.</span><span class="sxs-lookup"><span data-stu-id="93353-p104">The files in a project based on the Windows Phone Empty SharePoint Application template are the standard files of a Silverlight Windows Phone app. The MainPage.xaml file contains XAML declarations that constitute the user interface (UI) of the app. A code-behind file, MainPage.xaml.cs, is associated with the MainPage.xaml file by using the mechanism of partial classes, as are the other code-behind files in the project. (See  [Code-Behind and Partial Classes](http://msdn.microsoft.com/en-us/library/cc221357.aspx).) The MainPage.xaml.cs file contains procedural code to implement logic to support operations and events in the UI. The App.xaml file represents the overall Windows app. The associated code-behind file, App.xaml.cs, includes procedural code to handle life-cycle events for the app.</span></span>
  
    
    

## <a name="starting-a-project-based-on-the-windows-phone-sharepoint-list-application-template"></a><span data-ttu-id="93353-129">Запуск проекта на основе шаблона приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93353-129">Starting a project based on the Windows Phone SharePoint List Application template</span></span>
<span data-ttu-id="93353-130"><a name="BKMK_SPListAppTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="93353-130"></span></span>

<span data-ttu-id="93353-p105">Шаблон приложения списка SharePoint для Windows Phone значительно эффективнее, чем шаблон приложение Windows Phone пустой SharePoint. Этот шаблон разработан для создания приложения для Windows Phone для обработки вероятный сценарий в разработки мобильных приложений для SharePoint: доступа и управления данными в список SharePoint из Windows Phone. При создании проекта Visual Studio, основанных на этом шаблоне, мастер помогает выполнить необходимые шаги по настройке и создает файлы решения для работы приложения Windows Phone, можно работать с данными списков SharePoint. Можно создать и развернуть приложение из созданные файлы с минимальными или без изменений.</span><span class="sxs-lookup"><span data-stu-id="93353-p105">The Windows Phone SharePoint List Application template is considerably more powerful than the Windows Phone Empty SharePoint Application template. This template was designed to help you create Windows Phone apps to handle a likely scenario in mobile application development for SharePoint: accessing and manipulating data stored in a SharePoint list from a Windows Phone. When you create a Visual Studio project based on this template, a wizard guides you through the necessary configuration steps and generates solution files for a functional Windows Phone app that can work with SharePoint list data. You can build and deploy the app from the generated files with little or no modification.</span></span>
  
    
    

> <span data-ttu-id="93353-135">**Примечание:** Шаблоны доступны для Windows Phone 8 в Visual Studio Express 2012.</span><span class="sxs-lookup"><span data-stu-id="93353-135">**Note:** The same templates are available for Windows Phone 8 in Visual Studio Express 2012.</span></span> 
  
    
    


### <a name="understanding-the-solution-files-in-a-windows-phone-sharepoint-list-application-project"></a><span data-ttu-id="93353-136">Общие сведения о файлах решения в проект приложения списка SharePoint для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93353-136">Understanding the solution files in a Windows Phone SharePoint List Application project</span></span>

<span data-ttu-id="93353-p106">Файлы, созданные для Visual Studio проекта с помощью шаблона приложения списка SharePoint для Windows Phone показаны на рисунке 2. (Ссылки на другие сборки  не показано на рисунке 2  например, System.Runtime.Serialization.dll и Microsoft.Phone.Controls.dll относятся только к эти ссылки, включенные в шаблоне приложения Windows Phone пустой SharePoint. Эти дополнительные сборки поддерживает управление данным списков SharePoint и визуальные элементы управления для представления данных).</span><span class="sxs-lookup"><span data-stu-id="93353-p106">The files generated for a Visual Studio project using the Windows Phone SharePoint List Application template are shown in Figure 2. (References to other assemblies—not shown in Figure 2—such as System.Runtime.Serialization.dll and Microsoft.Phone.Controls.dll are additional to those references included by the Windows Phone Empty SharePoint Application template. These additional assemblies support the management of SharePoint list data and the visual controls to represent that data.)</span></span>
  
    
    

<span data-ttu-id="93353-140">**На рисунке 2. Файлы в проект приложения списка SharePoint для Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="93353-140">**Figure 2. Files in a Windows Phone SharePoint List Application project**</span></span>

  
    
    

  
    
    
![Проект приложения списка SharePoint для Windows Phone](../images/1a9680d3-7a96-4d82-b0b9-9a9384bf96c2.gif)
  
    
    
<span data-ttu-id="93353-142">Файлы проекта для описаны в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="93353-142">The project files for are described in Table 1.</span></span>
  
    
    

<span data-ttu-id="93353-143">**В таблице 1. Файлы проекта приложения списка SharePoint для Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="93353-143">**Table 1. Windows Phone SharePoint List Application project files**</span></span>


|<span data-ttu-id="93353-144">**Файл**</span><span class="sxs-lookup"><span data-stu-id="93353-144">**File**</span></span>|<span data-ttu-id="93353-145">**Описание**</span><span class="sxs-lookup"><span data-stu-id="93353-145">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="93353-146">App.XAML</span><span class="sxs-lookup"><span data-stu-id="93353-146">App.xaml</span></span>  <br/> |<span data-ttu-id="93353-p107">Представляет приложение Windows Phone в целом. Включает в себя объявления элементов, связанные с приложением (вместо на отдельные страницы в приложении), такие как события жизненным циклом приложения как **Application_Deactivated** и **Application_Closing**. </span><span class="sxs-lookup"><span data-stu-id="93353-p107">Represents the overall Windows Phone application. Includes declarations of elements related to the application (instead of to individual pages within the application), such as application life-cycle events like **Application_Deactivated** and **Application_Closing**.  </span></span><br/> |
|<span data-ttu-id="93353-149">App.XAML.cs</span><span class="sxs-lookup"><span data-stu-id="93353-149">App.xaml.cs</span></span>  <br/> |<span data-ttu-id="93353-p108">Файл фонового кода, связанного с App.xaml (с помощью механизма разделяемого класса, как в случае для других файлов кода в проекте). Включает в себя процедурного кода для обработки операций в событий жизненного цикла, такие как **Application_Deactivated** и **Application_Closing**. Написание кода в этот файл для управления автономной (локальный) хранилище данных. </span><span class="sxs-lookup"><span data-stu-id="93353-p108">The code-behind file associated with App.xaml (using the partial-class mechanism, as is the case for the other code-behind files in the project). Includes procedural code to handle the operations in the life-cycle events, such as **Application_Deactivated** and **Application_Closing**. You write code in this file to manage offline (local) storage of data.  </span></span><br/> |
|<span data-ttu-id="93353-153">ListDataProvider.cs</span><span class="sxs-lookup"><span data-stu-id="93353-153">ListDataProvider.cs</span></span>  <br/> |<span data-ttu-id="93353-154">Содержит код для доступа к данным на SharePoint Server и предоставляет доступ к являются различных представлений списка приложения на основе синтаксиса запроса.</span><span class="sxs-lookup"><span data-stu-id="93353-154">Contains code for accessing data on the SharePoint Server and provides access to the query syntax on which the various list views of the application are based.</span></span>  <br/> |
|<span data-ttu-id="93353-155">List.XAML</span><span class="sxs-lookup"><span data-stu-id="93353-155">List.xaml</span></span>  <br/> |<span data-ttu-id="93353-p109">Определяет элементы пользовательского интерфейса для представления формы по умолчанию в приложении телефона; аналогом всех элементов (или все задачи, все контакты или аналогичное) представления в SharePoint. Файл List.xaml содержит элемент управления **Pivot**, который представляет основной контейнер для визуальных элементов в приложении, включая элементы управления **PivotItem**, отображать представления списка, выбранного разработчиком, должны быть включены в приложении Windows Phone. </span><span class="sxs-lookup"><span data-stu-id="93353-p109">Defines the UI elements for the default view form in the phone application; analogous to the All Items (or All Tasks, All Contacts, or similar) view in SharePoint. The List.xaml file contains the **Pivot** control that constitutes the primary container for visual elements in the application, including the **PivotItem** controls that render the list views chosen by the developer to be included in the Windows Phone app. </span></span><br/> |
|<span data-ttu-id="93353-158">List.XAML.cs</span><span class="sxs-lookup"><span data-stu-id="93353-158">List.xaml.cs</span></span>  <br/> |<span data-ttu-id="93353-p110">Файл фонового кода, связанного с List.xaml. Включает в себя код, реализующий методы и обработчики для кнопок на форме, таких как **Создать** "и" **Обновить**. </span><span class="sxs-lookup"><span data-stu-id="93353-p110">The code-behind file associated with List.xaml. Includes code to implement the methods and handlers for the buttons on the form, such as **New** and **Refresh**.  </span></span><br/> |
|<span data-ttu-id="93353-161">DisplayForm.xaml</span><span class="sxs-lookup"><span data-stu-id="93353-161">DisplayForm.xaml</span></span>  <br/> |<span data-ttu-id="93353-p111">Определяет элементы пользовательского интерфейса для формы **Отображения элемента** (или страницы) в приложении; аналогом **Элемента представления** формы в SharePoint. В приложении Windows Phone с помощью элемента управления **StackPanel**, содержащийся в элементе управления **Pivot** Silverlight в вертикальном «стек» отображаются поля. </span><span class="sxs-lookup"><span data-stu-id="93353-p111">Defines the UI elements for the **Display Item** form (or page) in the application; analogous to the **View Item** form in SharePoint. In the Windows Phone app, the fields are rendered in a vertical "stack" by using a **StackPanel** control contained in a Silverlight **Pivot** control. </span></span><br/> |
|<span data-ttu-id="93353-164">Displayform.XAML.cs из</span><span class="sxs-lookup"><span data-stu-id="93353-164">DisplayForm.xaml.cs</span></span>  <br/> |<span data-ttu-id="93353-p112">Файл фонового кода, связанного с DisplayForm.xaml. Включает в себя код, реализующий методы и обработчики для кнопок на форме, например, **Изменение** и **Удаление**. </span><span class="sxs-lookup"><span data-stu-id="93353-p112">The code-behind file associated with DisplayForm.xaml. Includes code to implement the methods and handlers for the buttons on the form, such as **Edit** and **Delete**.  </span></span><br/> |
|<span data-ttu-id="93353-167">EditForm.xaml</span><span class="sxs-lookup"><span data-stu-id="93353-167">EditForm.xaml</span></span>  <br/> |<span data-ttu-id="93353-p113">Определяет элементы пользовательского интерфейса для форма **Изменения элемента** в приложении телефона; Аналогично форма **Изменения элемента** в SharePoint. Как и в форме **Отображения элемента** в элементе управления **StackPanel** отображаются поля. </span><span class="sxs-lookup"><span data-stu-id="93353-p113">Defines the UI elements for the **Edit Item** form in the phone application; analogous to the **Edit Item** form in SharePoint. As with the **Display Item** form, fields are rendered in a **StackPanel** control. </span></span><br/> |
|<span data-ttu-id="93353-170">EditForm.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="93353-170">EditForm.xaml.cs</span></span>  <br/> |<span data-ttu-id="93353-p114">Файл фонового кода, связанного с EditForm.xaml. Включает в себя код, реализующий методы и обработчики для кнопок на форме, таких как **Отправка** и **Отмена**. </span><span class="sxs-lookup"><span data-stu-id="93353-p114">The code-behind file associated with EditForm.xaml. Includes code to implement the methods and handlers for the buttons on the form, such as **Submit** and **Cancel**.  </span></span><br/> |
|<span data-ttu-id="93353-173">NewForm.xaml</span><span class="sxs-lookup"><span data-stu-id="93353-173">NewForm.xaml</span></span>  <br/> |<span data-ttu-id="93353-p115">Определяет элементы пользовательского интерфейса для формы **Нового элемента** в приложении телефона; аналог в форму **Новый элемент** в SharePoint. В элементе управления **StackPanel** отображаются поля. </span><span class="sxs-lookup"><span data-stu-id="93353-p115">Defines the UI elements for the **New Item** form in the phone application; analogous to the **New Item** form in SharePoint. Fields are rendered in a **StackPanel** control. </span></span><br/> |
|<span data-ttu-id="93353-176">NewForm.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="93353-176">NewForm.xaml.cs</span></span>  <br/> |<span data-ttu-id="93353-p116">Файл фонового кода, связанного с NewForm.xaml. Включает в себя код, реализующий методы и обработчики для кнопок на форме, таких как **Отправка** и **Отмена**. </span><span class="sxs-lookup"><span data-stu-id="93353-p116">The code-behind file associated with NewForm.xaml. Includes code to implement the methods and handlers for the buttons on the form, such as **Submit** and **Cancel**.  </span></span><br/> |
|<span data-ttu-id="93353-179">DisplayItemViewModel.cs</span><span class="sxs-lookup"><span data-stu-id="93353-179">DisplayItemViewModel.cs</span></span>  <br/> |<span data-ttu-id="93353-180">Выступает в качестве источника данных для файла DisplayForm.xaml.</span><span class="sxs-lookup"><span data-stu-id="93353-180">Serves as the data source for the DisplayForm.xaml file.</span></span>  <br/> |
|<span data-ttu-id="93353-181">EditItemViewModel.cs</span><span class="sxs-lookup"><span data-stu-id="93353-181">EditItemViewModel.cs</span></span>  <br/> |<span data-ttu-id="93353-p117">Выступает в качестве источника данных для файла EditForm.xaml. Написание кода в этот файл, чтобы проверить данные, введенные пользователями при изменении элемента списка.</span><span class="sxs-lookup"><span data-stu-id="93353-p117">Serves as the data source for the EditForm.xaml file. You write code in this file to validate data entered by users when editing a list item.</span></span>  <br/> |
|<span data-ttu-id="93353-184">ListViewModel.cs</span><span class="sxs-lookup"><span data-stu-id="93353-184">ListViewModel.cs</span></span>  <br/> |<span data-ttu-id="93353-185">Выступает в качестве источника данных для файла List.xaml.</span><span class="sxs-lookup"><span data-stu-id="93353-185">Serves as the data source for the List.xaml file.</span></span>  <br/> |
|<span data-ttu-id="93353-186">NewItemViewModel.cs</span><span class="sxs-lookup"><span data-stu-id="93353-186">NewItemViewModel.cs</span></span>  <br/> |<span data-ttu-id="93353-p118">Выступает в качестве источника данных для файла NewForm.xaml. Написание кода в этот файл, чтобы проверить данные, введенные пользователями, при добавлении нового элемента списка.</span><span class="sxs-lookup"><span data-stu-id="93353-p118">Serves as the data source for the NewForm.xaml file. You write code in this file to validate data entered by users when adding a new list item.</span></span>  <br/> |
   
<span data-ttu-id="93353-189">Подробные сведения об этапах, используемых при создании приложения Windows Phone с использованием шаблона приложения списка SharePoint для Windows Phone, в разделе [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md).</span><span class="sxs-lookup"><span data-stu-id="93353-189">For the details of the steps involved in creating a Windows Phone app by using the Windows Phone SharePoint List Application template, see  [How to: Create a Windows Phone SharePoint list app](how-to-create-a-windows-phone-sharepoint-list-app.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="93353-190">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="93353-190">Additional resources</span></span>
<span data-ttu-id="93353-191"><a name="SP15winphoneover_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="93353-191"></span></span>


-  [<span data-ttu-id="93353-192">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="93353-192">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="93353-193">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="93353-193">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="93353-194">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="93353-194">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="93353-195">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="93353-195">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="93353-196">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="93353-196">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="93353-197">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="93353-197">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  
-  [<span data-ttu-id="93353-198">Windows Phone разработки</span><span class="sxs-lookup"><span data-stu-id="93353-198">Windows Phone Development</span></span>](http://msdn.microsoft.com/en-us/library/ff402535%28v=vs.92%29.aspx)
    
  

