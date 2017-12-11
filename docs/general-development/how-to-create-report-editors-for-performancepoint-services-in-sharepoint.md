---
title: "Создание отчета редакторы для служб PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 8c48ffd7d0029309e9cb816c64e45c5f9caf5a84
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-report-editors-for-performancepoint-services-in-sharepoint"></a>Создание отчета редакторы для служб PerformancePoint Services в SharePoint

Узнайте, как создать компонент редактора для модуля пользовательских отчетов для Службы PerformancePoint Services.

## <a name="what-are-custom-report-editors-for-performancepoint-services"></a>Что такое редакторы настраиваемых отчетов по Службы PerformancePoint Services ?
<a name="bi_intro"> </a>

В Службы PerformancePoint Services редакторы настраиваемых отчетов позволяют пользователям задания свойств настраиваемых отчетов. Редакторы отчетов также инициализировать конечную точку отчета, который получает значения параметров от системы показателей и поставщиков фильтров. Дополнительные сведения о требованиях к редактора и функциональные возможности можно  [Редакторы нестандартных объектов PerformancePoint Services](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
  
    
    
Следующие процедуры и примеры основаны на класс **SampleReportViewEditor** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Редактор — тонкие веб-приложения, которое позволяет пользователям изменять имя и описание отчета. Полный код для класса, в разделе [пример кода: создание, извлечение и обновление настраиваемых отчетов служб PerformancePoint Services в SharePoint](#bk_example).
  
    
    
Мы рекомендуем использовать редактор образец как шаблон. В примере демонстрируется как вызов объектов в Службы PerformancePoint Services API, предоставляет вспомогательные объекты, которые упрощают вызывает для репозитория операций (например, создание и обновление объектов) и демонстрируются советы и рекомендации по разработке Службы PerformancePoint Services.
  
    
    

## <a name="create-editors-for-custom-performancepoint-services-reports"></a>Создание редакторов настраиваемых Службы PerformancePoint Services отчетов
<a name="BKMK_ConfigREditor"> </a>


  
    
    

1. Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (перечисленных в шаге 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. В Visual Studio создайте библиотеку классов C#. Если библиотека классов для расширения уже создана, добавьте новый класс C#.
    
    DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Добавьте в проект в качестве ссылок на сборки следующие библиотеки DLL:
    
  - Файл Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.ServerCommon.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Store.dll (используется в вспомогательных классах)
    
  
  - Microsoft.SharePoint.dll (используется в вспомогательных классах)
    
  

    Образец редактора также содержит ссылки на сборки System.Web.dll и System.Web.Services.dll. В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.
    
  
4. Добавьте следующие классы из примера в проект. Редактор использует эти вспомогательные классы для взаимодействия с репозитория Службы PerformancePoint Services:
    
  - DataSourceConsumerHelper.cs
    
  
  - ExtensionRepositoryHelper.cs
    
  
  - ReportViewRepositoryHelper.cs
    
  
  - IDataSourceConsumer.cs
    
  > [!NOTE]
    > Пример отчета получает данные из фильтра, поэтому он не использует **DataSourceConsumerHelper** или **IDataSourceConsumer** объектов. Тем не менее, если отчет получает данные из источника данных PerformancePoint Services, можно использовать методы, предоставляемые классом **DataSourceConsumerHelper** для получения источников данных, как описано в [как для: создание редакторов для фильтра PerformancePoint Services в SharePoint](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/how-to-create-report-editors-for-performancepoint-services-in-sharepoint). 

5. В классе редактора добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.
    
  - **Microsoft.PerformancePoint.Scorecards**
    
  
  - **Microsoft.PerformancePoint.Scorecards.ServerCommon**
    
  

    В зависимости от функциональности расширения могут потребоваться другие директивы **using**.
    
  
6. Унаследуйте класс от базового класса, который поддерживает реализацию редактора. Так как образец редактора отчетов  это веб-приложение, он наследуется от класса  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) . Другие реализации могут быть производными от базовых классов, таких как [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) или [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) .
    
  
7. Объявите переменные для элементов управления, предоставляющих свойства, которые пользователи должны просматривать или редактировать. Образец редактора отчетов сначала объявляет переменные для элементов управления веб-сервера, заданных в компоненте пользовательского интерфейса, который является ASPX-страницей. В образце редактора также определяется элемент управления кнопки, который позволяет пользователям передавать изменения. Затем редактор вызывает метод  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) для размещения элементов управления на странице.
    
    > [!NOTE]
    > [!Примечание] В редакторе программная логика определяется отдельно от пользовательского интерфейса. Инструкции по созданию компонента пользовательского интерфейса не входят в данную документации. 

    Редактор отчетов пример выполняет шаги с 8 по 12 в методе **Page_Load**. **Page_Load** также используется для инициализации и проверка переменными и элементами управления, заполнения элементов управления и сохранить сведения о состоянии для настраиваемых отчетов и вспомогательные объекты.
    
  
8. Присвойте свойству  [AllowUnsafeUpdates](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.ServerUtils.AllowUnsafeUpdates.aspx) значение **true**. Это позволяет редактор отчетов для записи данных в репозитории без использования операций **POST** формы.
    
  
9. Получите параметры из строки запроса и присвойте их значения локальным переменным, как показано в примере кода ниже.
    
```cs
  
// The URL of the site collection that contains the PerformancePoint Services repository.
string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];

// The location of the report in the repository.
string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];

// The operation to perform: OpenItem or CreateItem.
string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];
```


    For information about the query string parameters, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
    
  
10. Извлеките объект **ReportViewRepositoryHelper**, который используется для направления вызовов к репозиторию, как показано в следующем примере кода.
    
```cs
  
reportviewRepositoryHelper = new ReportViewRepositoryHelper();
```

11. Задайте расположение отчета на основе параметра строки запроса, как показано в следующем примере кода.
    
```cs
  RepositoryLocation repositoryReportViewLocation = RepositoryLocation.CreateFromUriString(itemLocation);
```

12. Извлеките из строки запроса выполняемую операцию ( _OpenItem_ или _CreateItem_) и извлечения или создайте настраиваемый отчет.
    
  - Чтобы извлечь настраиваемый отчет, воспользуйтесь методом **ReportViewRepositoryHelper.Get**.
    
  
  - Чтобы создать настраиваемый отчет, воспользуйтесь конструктором **ReportView()** и затем определите свойства [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx) и [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx) объекта.
    
     [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.SubTypeId.aspx)  уникальный идентификатор для отчета, и его должен соответствовать атрибуту **subType**, указанная для настраиваемого отчета в файле web.config Службы PerformancePoint Services. [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.RendererClassName.aspx)  это полное имя класса, который определяет веб-сервер визуализации элемента управления. Если не определен в редакторе, это значение по умолчанию класса визуализации, указанное в файле web.config.
    
  

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


    > [!NOTE]
    > By default, users can create custom objects from PerformancePoint Dashboard Designer only. To enable users to create a custom object outside of Dashboard Designer, you must add a menu item that sends a  _CreateItem_ request to your editor from the content type in the repository. For more information, see [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx). 

13. Определите конечную точку отчета, которая позволяет отчету получать данные из фильтров и систем показателей. В образце редактора отчетов определяются обязательные свойства конечной точки, как показано в следующем примере кода.
    
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
    
  
14. Обновите отчет в соответствии с изменениями, внесенными пользователем. Метод **buttonOK_Click** в образце редактора отчетов вызывает метод **ReportViewRepositoryHelper.Update** для обновления свойств [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) и [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) отчета в репозитории. **buttonOK_Click** также используется для проверки содержимого элементов управления и извлечения сведений о состоянии для настраиваемого отчета и вспомогательного объекта.
    
    > [!NOTE]
    > [!Примечание] Пользователи могут изменять  [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) и свойства [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx) ( **Ответственное лицо** ) пользовательского объекта и удалять настраиваемые объекты непосредственно из репозитория Службы PerformancePoint Services и Конструктор панели мониторинга. 

## <a name="code-example-create-retrieve-and-update-custom-performancepoint-services-reports-in-sharepoint"></a>Пример кода: создание, извлечение и обновление настраиваемых отчетов служб PerformancePoint Services в SharePoint
<a name="bk_example"> </a>

В следующем примере кода создается, извлекаются и обновляются настраиваемые отчеты. Этот код  от класса редактор кода, который содержит логику программирования для элементов управления, определенных на ASPX-странице.
  
    
    
Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в статье  [Создание редакторов настраиваемых Службы PerformancePoint Services отчетов](#BKMK_ConfigREditor).
  
    
    



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


## <a name="next-steps"></a>Дальнейшие шаги
<a name="bk_next"> </a>

После создания отчета редактора, (включая его пользовательского интерфейса, при необходимости) и модуль подготовки отчетов, развертывание данное расширение имени файла, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addResources"> </a>


-  [Как: создание средств отображения отчетов для PerformancePoint Services в SharePoint](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [PerformancePoint Services в SharePoint](performancepoint-services-in-sharepoint.md)
    
  

