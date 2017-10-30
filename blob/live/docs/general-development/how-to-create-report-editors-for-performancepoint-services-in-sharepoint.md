---
title: "Создание редакторы отчетов для PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f9675950d272a1bd90efa4eb26a6772f13dd24bc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-report-editors-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="ddf35-102">Как: создать отчет редакторы для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ddf35-102">How to: Create report editors for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="ddf35-103">Узнайте, как создать компонент редактора для модуля пользовательских отчетов для Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="ddf35-103">Learn how to create the editor component of a custom report extension for PerformancePoint Services.</span></span>
## <a name="what-are-custom-report-editors-for-performancepoint-services"></a><span data-ttu-id="ddf35-104">Что такое редакторы настраиваемых отчетов по Службы PerformancePoint Services ?</span><span class="sxs-lookup"><span data-stu-id="ddf35-104">What are custom report editors for PerformancePoint Services?</span></span>
<span data-ttu-id="ddf35-105"><a name="bi_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="ddf35-105"></span></span>

<span data-ttu-id="ddf35-p101">В Службы PerformancePoint Services редакторы настраиваемых отчетов позволяют пользователям задания свойств настраиваемых отчетов. Редакторы отчетов также инициализировать конечную точку отчета, который получает значения параметров от системы показателей и поставщиков фильтров. Дополнительные сведения о требованиях к редактора и функциональные возможности можно  [Редакторы нестандартных объектов PerformancePoint Services](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddf35-p101">In PerformancePoint Services, custom report editors enable users to set properties on custom reports. Report editors also initialize the report endpoint, which receives parameter values from scorecard and filter providers. For more information about editor requirements and functionality, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="ddf35-109">Следующие процедуры и примеры основаны на класс **SampleReportViewEditor** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddf35-109">The following procedures and examples are based on the **SampleReportViewEditor** class from the [custom objects sample](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx).</span></span> <span data-ttu-id="ddf35-110">Редактор — тонкие веб-приложения, которое позволяет пользователям изменять имя и описание отчета.</span><span class="sxs-lookup"><span data-stu-id="ddf35-110">The editor is a thin web application that enables users to modify the report's name and description.</span></span> <span data-ttu-id="ddf35-111">Полный код для класса, в разделе [пример кода: создание, извлечение и обновление настраиваемых отчетов служб PerformancePoint Services в SharePoint](#bk_example).</span><span class="sxs-lookup"><span data-stu-id="ddf35-111">For the complete code for the class, see  [Code example: Create, retrieve, and update custom PerformancePoint Services reports in SharePoint](#bk_example).</span></span>
  
    
    
<span data-ttu-id="ddf35-p103">Мы рекомендуем использовать редактор образец как шаблон. В примере демонстрируется как вызов объектов в Службы PerformancePoint Services API, предоставляет вспомогательные объекты, которые упрощают вызывает для репозитория операций (например, создание и обновление объектов) и демонстрируются советы и рекомендации по разработке Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p103">We recommend that you use the sample editor as a template. The sample shows how to call objects in the PerformancePoint Services API, provides helper objects that simplify calls for repository operations (such as creating and updating objects), and demonstrates best practices for PerformancePoint Services development.</span></span>
  
    
    

## <a name="create-editors-for-custom-performancepoint-services-reports"></a><span data-ttu-id="ddf35-114">Создание редакторов настраиваемых Службы PerformancePoint Services отчетов</span><span class="sxs-lookup"><span data-stu-id="ddf35-114">Create editors for custom PerformancePoint Services reports</span></span>
<span data-ttu-id="ddf35-115"><a name="BKMK_ConfigREditor"> </a></span><span class="sxs-lookup"><span data-stu-id="ddf35-115"></span></span>


  
    
    

1. <span data-ttu-id="ddf35-p104">Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddf35-p104">Install PerformancePoint Services, or copy the DLLs that your extension uses (listed in step 3) to your computer. For more information, see  [DLLs with Class Libraries](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).</span></span>
    
  
2. <span data-ttu-id="ddf35-p105">В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p105">In Visual Studio, create a C# class library. If you have already created a class library for your extension, add a new C# class.</span></span>
    
    <span data-ttu-id="ddf35-p106">DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddf35-p106">You must sign your DLL with a strong name. In addition, ensure that all assemblies referenced by your DLL have strong names. For information about how to sign an assembly with a strong name and how to create a public/private key pair, see  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).</span></span>
    
  
3. <span data-ttu-id="ddf35-123">Добавьте в проект в качестве ссылок на сборки следующие библиотеки DLL:</span><span class="sxs-lookup"><span data-stu-id="ddf35-123">Add the following DLLs as assembly references to the project:</span></span>
    
  - <span data-ttu-id="ddf35-124">Файл Microsoft.PerformancePoint.Scorecards.Client.dll</span><span class="sxs-lookup"><span data-stu-id="ddf35-124">Microsoft.PerformancePoint.Scorecards.Client.dll</span></span>
    
  
  - <span data-ttu-id="ddf35-125">Microsoft.PerformancePoint.Scorecards.ServerCommon.dll</span><span class="sxs-lookup"><span data-stu-id="ddf35-125">Microsoft.PerformancePoint.Scorecards.ServerCommon.dll</span></span>
    
  
  - <span data-ttu-id="ddf35-126">Microsoft.PerformancePoint.Scorecards.Store.dll (используется в вспомогательных классах)</span><span class="sxs-lookup"><span data-stu-id="ddf35-126">Microsoft.PerformancePoint.Scorecards.Store.dll (used by helper classes)</span></span>
    
  
  - <span data-ttu-id="ddf35-127">Microsoft.SharePoint.dll (используется в вспомогательных классах)</span><span class="sxs-lookup"><span data-stu-id="ddf35-127">Microsoft.SharePoint.dll (used by helper classes)</span></span>
    
  

    <span data-ttu-id="ddf35-p107">Образец редактора также содержит ссылки на сборки System.Web.dll и System.Web.Services.dll. В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p107">The sample editor also contains assembly references to System.Web.dll and System.Web.Services.dll. Depending on your extension's functionality, other project references may be required.</span></span>
    
  
4. <span data-ttu-id="ddf35-p108">Добавьте следующие классы из примера в проект. Редактор использует эти вспомогательные классы для взаимодействия с репозитория Службы PerformancePoint Services:</span><span class="sxs-lookup"><span data-stu-id="ddf35-p108">Add the following classes from the sample to the project. The editor uses these helper classes to interact with the PerformancePoint Services repository:</span></span>
    
  - <span data-ttu-id="ddf35-132">DataSourceConsumerHelper.cs</span><span class="sxs-lookup"><span data-stu-id="ddf35-132">DataSourceConsumerHelper.cs</span></span>
    
  
  - <span data-ttu-id="ddf35-133">ExtensionRepositoryHelper.cs</span><span class="sxs-lookup"><span data-stu-id="ddf35-133">ExtensionRepositoryHelper.cs</span></span>
    
  
  - <span data-ttu-id="ddf35-134">ReportViewRepositoryHelper.cs</span><span class="sxs-lookup"><span data-stu-id="ddf35-134">ReportViewRepositoryHelper.cs</span></span>
    
  
  - <span data-ttu-id="ddf35-135">IDataSourceConsumer.cs</span><span class="sxs-lookup"><span data-stu-id="ddf35-135">IDataSourceConsumer.cs</span></span>
    
  

    > <span data-ttu-id="ddf35-136">**Примечание:** Пример отчета получает данные из фильтра, поэтому он не использует **DataSourceConsumerHelper** или **IDataSourceConsumer** объектов.</span><span class="sxs-lookup"><span data-stu-id="ddf35-136">**Note:** The sample report obtains data from a filter, so it does not use **DataSourceConsumerHelper** or **IDataSourceConsumer** objects.</span></span> <span data-ttu-id="ddf35-137">Тем не менее, если отчет получает данные из источника данных PerformancePoint Services, можно использовать методы, предоставляемые классом **DataSourceConsumerHelper** для получения источников данных, как описано в [как для: создание редакторов для фильтра PerformancePoint Services в SharePoint](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/how-to-create-report-editors-for-performancepoint-services-in-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="ddf35-137">However, if your report obtains data from a PerformancePoint Services data source, you can use the methods that are exposed by the **DataSourceConsumerHelper** class to retrieve data sources as described in [How to: Create filter editors for PerformancePoint Services in SharePoint](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/how-to-create-report-editors-for-performancepoint-services-in-sharepoint).</span></span> 
5. <span data-ttu-id="ddf35-138">В классе редактора добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="ddf35-138">In your editor class, add **using** directives for the following PerformancePoint Services namespaces:</span></span>
    
  - <span data-ttu-id="ddf35-139">**Microsoft.PerformancePoint.Scorecards**</span><span class="sxs-lookup"><span data-stu-id="ddf35-139">**Microsoft.PerformancePoint.Scorecards**</span></span>
    
  
  - <span data-ttu-id="ddf35-140">**Microsoft.PerformancePoint.Scorecards.ServerCommon**</span><span class="sxs-lookup"><span data-stu-id="ddf35-140">**Microsoft.PerformancePoint.Scorecards.ServerCommon**</span></span>
    
  

    <span data-ttu-id="ddf35-141">В зависимости от функциональности расширения могут потребоваться другие директивы **using**.</span><span class="sxs-lookup"><span data-stu-id="ddf35-141">Depending on your extension's functionality, other **using** directives may be required.</span></span>
    
  
6. <span data-ttu-id="ddf35-p110">Унаследуйте класс от базового класса, который поддерживает реализацию редактора. Так как образец редактора отчетов  это веб-приложение, он наследуется от класса  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) . Другие реализации могут быть производными от базовых классов, таких как [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) или [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ddf35-p110">Inherit from the base class that supports your editor implementation. Because the sample report editor is a web application, it inherits from the  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) class. Other implementations can derive from base classes such as the [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) or [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) class.</span></span>
    
  
7. <span data-ttu-id="ddf35-p111">Объявите переменные для элементов управления, предоставляющих свойства, которые пользователи должны просматривать или редактировать. Образец редактора отчетов сначала объявляет переменные для элементов управления веб-сервера, заданных в компоненте пользовательского интерфейса, который является ASPX-страницей. В образце редактора также определяется элемент управления кнопки, который позволяет пользователям передавать изменения. Затем редактор вызывает метод  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) для размещения элементов управления на странице.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p111">Declare variables for the controls that expose the properties that you want users to view or modify. The sample report editor first declares variables for the web server controls that are defined in the user interface component, which is an ASPX page. The sample editor also defines a button control that enables users to submit changes. Then, the editor calls the  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) method to make the controls available on the page.</span></span>
    
    > <span data-ttu-id="ddf35-149">**Примечание:** Редактор определяет логику программирования отдельно от пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ddf35-149">**Note:** The editor defines programming logic separately from the user interface.</span></span> <span data-ttu-id="ddf35-150">Инструкции по созданию компонентов пользовательского интерфейса редактора выходят за рамки данной документации.</span><span class="sxs-lookup"><span data-stu-id="ddf35-150">Instructions for creating the user interface component of the editor are beyond the scope of this documentation.</span></span> 

    <span data-ttu-id="ddf35-p113">Редактор отчетов пример выполняет шаги с 8 по 12 в методе **Page_Load**. **Page_Load** также используется для инициализации и проверка переменными и элементами управления, заполнения элементов управления и сохранить сведения о состоянии для настраиваемых отчетов и вспомогательные объекты.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p113">The sample report editor performs steps 8 through 12 in the **Page_Load** method. **Page_Load** is also used to initialize and validate variables and controls, populate controls, and save state information for the custom report and helper objects.</span></span>
    
  
8. <span data-ttu-id="ddf35-p114">Присвойте свойству  [AllowUnsafeUpdates](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.ServerUtils.AllowUnsafeUpdates.aspx) значение **true**. Это позволяет редактор отчетов для записи данных в репозитории без использования операций **POST** формы.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p114">Set the  [AllowUnsafeUpdates](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.ServerUtils.AllowUnsafeUpdates.aspx) property to **true**. This enables the report editor to write data to the repository without using form **POST** operations.</span></span>
    
  
9. <span data-ttu-id="ddf35-155">Получите параметры из строки запроса и присвойте их значения локальным переменным, как показано в примере кода ниже.</span><span class="sxs-lookup"><span data-stu-id="ddf35-155">Retrieve the parameters from the query string and set them as values for local variables, as shown in the following code example.</span></span>
    
```cs
  
// The URL of the site collection that contains the PerformancePoint Services repository.
string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];

// The location of the report in the repository.
string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];

// The operation to perform: OpenItem or CreateItem.
string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];
```


    For information about the query string parameters, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
    
  
10. <span data-ttu-id="ddf35-156">Извлеките объект **ReportViewRepositoryHelper**, который используется для направления вызовов к репозиторию, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="ddf35-156">Retrieve the **ReportViewRepositoryHelper** object, which is used to make calls to the repository, as shown in the following code example.</span></span>
    
```cs
  
reportviewRepositoryHelper = new ReportViewRepositoryHelper();
```

11. <span data-ttu-id="ddf35-157">Задайте расположение отчета на основе параметра строки запроса, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="ddf35-157">Set the report location based on the query string parameter, as shown in the following code example.</span></span>
    
```cs
  RepositoryLocation repositoryReportViewLocation = RepositoryLocation.CreateFromUriString(itemLocation);
```

12. <span data-ttu-id="ddf35-158">Извлеките из строки запроса выполняемую операцию ( _OpenItem_ или _CreateItem_) и извлечения или создайте настраиваемый отчет.</span><span class="sxs-lookup"><span data-stu-id="ddf35-158">Retrieve the operation to perform ( _OpenItem_ or _CreateItem_) from the query string, and then retrieve or create the custom report.</span></span>
    
  - <span data-ttu-id="ddf35-159">Чтобы извлечь настраиваемый отчет, воспользуйтесь методом **ReportViewRepositoryHelper.Get**.</span><span class="sxs-lookup"><span data-stu-id="ddf35-159">To retrieve the custom report, use the **ReportViewRepositoryHelper.Get** method.</span></span>
    
  
  - <span data-ttu-id="ddf35-160">Чтобы создать настраиваемый отчет, воспользуйтесь конструктором **ReportView()** и затем определите свойства [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) и [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) объекта.</span><span class="sxs-lookup"><span data-stu-id="ddf35-160">To create the custom report, use the **ReportView()** constructor and then define the report's [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) , and [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) properties.</span></span>
    
     <span data-ttu-id="ddf35-p115">[SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx)  уникальный идентификатор для отчета, и его должен соответствовать атрибуту **subType**, указанная для настраиваемого отчета в файле web.config Службы PerformancePoint Services. [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx)  это полное имя класса, который определяет веб-сервер визуализации элемента управления. Если не определен в редакторе, это значение по умолчанию класса визуализации, указанное в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p115">[SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) is the unique identifier for the report, and it must match the **subType** attribute that you specify for your custom report in the PerformancePoint Services web.config file. [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) is the fully qualified name of the class that defines the renderer web server control. If not defined in the editor, this value defaults to the renderer class specified in the web.config file.</span></span>
    
  

```cs
  if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
    {

        // Use the repository-helper object to retrieve the report.
        reportview = reportviewRepositoryHelper.Get(repositoryReportViewLocation);
        if (reportview == null)
        {
            displayError("Could not retrieve the report view for editing.");
            return;
        }
    }
    else if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
    {
        reportview = new ReportView
        {
            RendererClassName = typeof(SampleReportRenderer).AssemblyQualifiedName, 
            SubTypeId = "SampleReportView"
        };
    }
    else
    {
        displayError("Invalid Action.");
        return;
    }
```


    > **Note:**
      > By default, users can create custom objects from PerformancePoint Dashboard Designer only. To enable users to create a custom object outside of Dashboard Designer, you must add a menu item that sends a  _CreateItem_ request to your editor from the content type in the repository. For more information, see [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx). 
13. <span data-ttu-id="ddf35-p116">Определите конечную точку отчета, которая позволяет отчету получать данные из фильтров и систем показателей. В образце редактора отчетов определяются обязательные свойства конечной точки, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p116">Define the report's endpoint, which enables the report to receive data from filters and scorecards. The sample report editor defines the required properties for the endpoint, as shown in the following code example.</span></span>
    
```cs
  
if (0 == reportview.EndPoints.Count)
{
    EndPoint endpoint = new EndPoint
    {
        Category = EndPointCategory.None,
        UniqueName = "SampleReportView_EndPoint",

        // The display name is shown to users in Dashboard Designer.
        // It represents the endpoint that can be connected 
        // to a filter or scorecard.
        DisplayName = "Sample Report View EndPoint"
    };

    reportview.EndPoints.Add(endpoint);
}
```


    The sample editor defines the endpoint in the **VerifyReportView** method. It also uses **VerifyReportView** to verify that required properties are set and to define the optional [CustomData](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.CustomData.aspx) property, which you can use to store information for your report.
    
  
14. <span data-ttu-id="ddf35-p117">Обновите отчет в соответствии с изменениями, внесенными пользователем. Метод **buttonOK_Click** в образце редактора отчетов вызывает метод **ReportViewRepositoryHelper.Update** для обновления свойств [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) и [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) отчета в репозитории. **buttonOK_Click** также используется для проверки содержимого элементов управления и извлечения сведений о состоянии для настраиваемого отчета и вспомогательного объекта.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p117">Update the report with user-defined changes. The **buttonOK_Click** method in the sample report editor calls the **ReportViewRepositoryHelper.Update** method to update the report's [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) and [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) properties in the repository. **buttonOK_Click** is also used to validate the contents of the controls and retrieve state information for the custom report and the helper object.</span></span>
    
    > <span data-ttu-id="ddf35-169">**Примечание:** Пользователи могут изменить [имя](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Описание](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) и свойства [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx) ( **Ответственное лицо**) настраиваемого объекта и удалять настраиваемые объекты непосредственно из конструктора панели мониторинга и репозитория служб PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="ddf35-169">**Note:** Users can edit a custom object's  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) , and [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx) ( **Person Responsible**) properties and delete custom objects directly from Dashboard Designer and the PerformancePoint Services repository.</span></span> 

## <a name="code-example-create-retrieve-and-update-custom-performancepoint-services-reports-in-sharepoint"></a><span data-ttu-id="ddf35-170">Пример кода: создание, извлечение и обновление настраиваемых отчетов служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ddf35-170">Code example: Create, retrieve, and update custom PerformancePoint Services reports in SharePoint</span></span>
<span data-ttu-id="ddf35-171"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="ddf35-171"></span></span>

<span data-ttu-id="ddf35-p118">В следующем примере кода создается, извлекаются и обновляются настраиваемые отчеты. Этот код  от класса редактор кода, который содержит логику программирования для элементов управления, определенных на ASPX-странице.</span><span class="sxs-lookup"><span data-stu-id="ddf35-p118">The following code example creates, retrieves, and updates custom reports. This code is from the editor's code-behind class, which provides the programming logic for controls that are defined in an ASPX page.</span></span>
  
    
    
<span data-ttu-id="ddf35-174">Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в статье  [Создание редакторов настраиваемых Службы PerformancePoint Services отчетов](#BKMK_ConfigREditor).</span><span class="sxs-lookup"><span data-stu-id="ddf35-174">Before you can compile this code example, you must configure your development environment as described in  [Create editors for custom PerformancePoint Services reports](#BKMK_ConfigREditor).</span></span>
  
    
    



```cs

using System;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.PerformancePoint.Scorecards;
using Microsoft.PerformancePoint.Scorecards.ServerCommon;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleReport
{

    // Represents the class that defines the sample report editor. 
    public class SampleReportViewEditor : Page
    {

        // Declare private variables for the ASP.NET controls defined in the user interface.
        // The sample's user interface is an ASPX page that defines the controls in HTML.
        private TextBox textboxName;
        private TextBox textboxDescription;
        private Label labelErrorMessage;
        private Button buttonOK;

        // Make the controls available to this class.
        protected override void CreateChildControls()
        {
            base.CreateChildControls();

            if (null == textboxName)
                textboxName = FindControl("textboxName") as TextBox;
            if (null == textboxDescription)
                textboxDescription = FindControl("textboxDescription") as TextBox;
            if (null == labelErrorMessage)
                labelErrorMessage = FindControl("labelErrorMessage") as Label;
            if (null == buttonOK)
                buttonOK = FindControl("buttonOK") as Button;
        }

        // Handles the Load event of the Page control.
        // Methods that use a control variable should call the Control.EnsureChildControls
        // method before accessing the variable for the first time.
        protected void Page_Load(object sender, EventArgs e)
        {

            // Required to enable custom report and filter editors to
            // write data to the repository.
            ServerUtils.AllowUnsafeUpdates = true;

            // Initialize controls the first time the page loads only.
            if (!IsPostBack)
            {
                EnsureChildControls();
                ReportViewRepositoryHelper reportviewRepositoryHelper = null;
                try
                {

                    // Get information from the query string parameters.
                    string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];
                    string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];
                    string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];

                    // Validate the query string parameters.
                    if (string.IsNullOrEmpty(server) ||
                        string.IsNullOrEmpty(itemLocation) ||
                        string.IsNullOrEmpty(action))
                    {
                        displayError("Invalid URL.");
                        return;
                    }

                    // Retrieve the repository-helper object.
                    reportviewRepositoryHelper =
                        new ReportViewRepositoryHelper();

                    // Set the report location by using the location from the query string.
                    RepositoryLocation repositoryReportViewLocation = RepositoryLocation.CreateFromUriString(itemLocation);

                    ReportView reportview;

                    // Retrieve or create the report object, depending on the operation
                    // passed in the query string (OpenItem or CreateItem).
                    if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {

                        // Retrieve the report object by using the repository-helper object.
                        reportview = reportviewRepositoryHelper.Get(repositoryReportViewLocation);
                        if (reportview == null)
                        {
                            displayError("Could not retrieve the report view for editing.");
                            return;
                        }
                    }
                    else if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {

                        // Create a report view.
                        // CreateItem requests can be sent from a SharePoint list, but
                        // you must create a custom menu item to send the request.
                        // Dashboard Designer can send edit requests only.
                        reportview = new ReportView
                        {
                            RendererClassName = typeof(SampleReportRenderer).AssemblyQualifiedName, 
                            SubTypeId = "SampleReportView"
                        };
                    }
                    else
                    {
                        displayError("Invalid Action.");
                        return;
                    }

                    VerifyReportView(reportview);

                    // Save the original report and helper objects across page postbacks.
                    ViewState["action"] = action;
                    ViewState["reportview"] = reportview;
                    ViewState["reportviewrepositoryhelper"] = reportviewRepositoryHelper;
                    ViewState["itemlocation"] = itemLocation;

                    // Populate the child controls.
                    textboxName.Text = reportview.Name.ToString();
                    textboxDescription.Text = reportview.Description.ToString();
                }
                catch (Exception ex)
                {
                    displayError("An error has occurred. Please contact your administrator for more information.");
                    if (reportviewRepositoryHelper != null)
                    {

                        // Add the exception detail to the server event log.
                        reportviewRepositoryHelper.HandleException(ex);
                    }
                }
            }
        }

        // Handles the Click event of the buttonOK control.
        protected void buttonOK_Click(object sender, EventArgs e)
        {
            EnsureChildControls();

            // Verify that the textboxName control contains a value.
            if (string.IsNullOrEmpty(textboxName.Text))
            {
                labelErrorMessage.Text = "A report view name is required.";
                return;
            }

            // Clear any pre-existing error message.
            labelErrorMessage.Text = string.Empty;

            // Retrieve the report and helper objects from view state.
            string action = (string)ViewState["action"];
            string itemLocation = (string) ViewState["itemlocation"];
            ReportView reportview = (ReportView)ViewState["reportview"];
            ReportViewRepositoryHelper reportviewRepositoryHelper = (ReportViewRepositoryHelper)ViewState["reportviewrepositoryhelper"];

            // Update the report object with form changes.
            reportview.Name.Text = textboxName.Text;
            reportview.Description.Text = textboxDescription.Text;

            // Save the report object to the PerformancePoint Services repository.
            try
            {
                reportview.Validate();
                if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                {
                    reportview.CreatedDate = DateTime.Now;
                    ReportView newReportView = reportviewRepositoryHelper.Create(
                        string.IsNullOrEmpty(reportview.Location.ItemUrl) ? itemLocation : reportview.Location.ItemUrl, 
                        reportview);
                    ViewState["reportview"] = newReportView;
                    ViewState["action"] = ClickOnceLaunchValues.OpenItem;
                }
                else
                {
                    reportviewRepositoryHelper.Update(reportview);
                }
            }
            catch (Exception ex)
            {
                displayError("An error has occurred. Please contact your administrator for more information.");
                if (reportviewRepositoryHelper != null)
                {
                    // Add the exception detail to the server event log.
                    reportviewRepositoryHelper.HandleException(ex);
                }
            }
        }

        // Displays the error string in the labelErrorMessage label. 
        void displayError(string msg)
        {
            EnsureChildControls();

            labelErrorMessage.Text = msg;

            // Disable the OK button because the page is in an error state.
            buttonOK.Enabled = false;
            return;
        }

        // Verifies that the properties for the report object are set.
        static void VerifyReportView(ReportView reportview)
        {

            // Verify that all required properties are set. 
            if (string.IsNullOrEmpty(reportview.SubTypeId))
            {

                // This value must match the subType attribute specified
                // in the web.config file.
                reportview.SubTypeId = "SampleReportView";
            }

            if (string.IsNullOrEmpty(reportview.RendererClassName))
            {
                reportview.RendererClassName = typeof (SampleReportRenderer).AssemblyQualifiedName;
            }

            // Reports are consumers and do not use provider endpoints.
           reportview.BeginPoints.Clear();

            // If there are no consumer endpoints, create one so we can connect a filter or a scorecard to the report.
            if (0 == reportview.EndPoints.Count)
            {
                EndPoint endpoint = new EndPoint
                {
                    Category = EndPointCategory.None,
                    UniqueName = "SampleReportView_EndPoint",

                    // The display name is shown to users in Dashboard
                    // Designer to represent the endpoint that can be 
                    // connected to a filter or scorecard.
                    DisplayName = "Sample Report View EndPoint"
                };

                reportview.EndPoints.Add(endpoint);
            }
            
            // Set optional properties for reports.
            reportview.CustomData = "You can use this property to store custom information for this filter as a string or a serialized object.";
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="ddf35-175">Дальнейшие шаги</span><span class="sxs-lookup"><span data-stu-id="ddf35-175">Next steps</span></span>
<span data-ttu-id="ddf35-176"><a name="bk_next"> </a></span><span class="sxs-lookup"><span data-stu-id="ddf35-176"></span></span>

<span data-ttu-id="ddf35-177">После создания отчета редактора, (включая его пользовательского интерфейса, при необходимости) и модуль подготовки отчетов, развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddf35-177">After you create a report editor (including its user interface, if required) and a report renderer, deploy the extension as described in  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="ddf35-178">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ddf35-178">Additional resources</span></span>
<span data-ttu-id="ddf35-179"><a name="bk_addResources"> </a></span><span class="sxs-lookup"><span data-stu-id="ddf35-179"></span></span>


-  [<span data-ttu-id="ddf35-180">Как: создание средств отображения отчетов для PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ddf35-180">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ddf35-181">PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ddf35-181">PerformancePoint Services in SharePoint</span></span>](performancepoint-services-in-sharepoint.md)
    
  

