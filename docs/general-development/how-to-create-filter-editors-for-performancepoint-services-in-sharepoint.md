---
title: "Создание редакторов фильтра для PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f4d9584f81f607714e5d06bcfb445fe76e7531f5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-filter-editors-for-performancepoint-services-in-sharepoint"></a>Как: создать фильтр редакторы для служб PerformancePoint Services в SharePoint
Узнайте, как создать компонент редактора для модуля пользовательских фильтров для Службы PerformancePoint Services.
## <a name="what-are-custom-filter-editors-for-performancepoint-services"></a>Что такое редакторы настраиваемых фильтров для Службы PerformancePoint Services ?
<a name="bk_intro"> </a>

В Службы PerformancePoint Services редакторы настраиваемых фильтров позволяют пользователям задания свойств настраиваемых фильтров. Редакторы фильтров также должны инициализировать в фильтре  [BeginPoints](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.BeginPoints.aspx) свойство, которое определяет начальную точку фильтра, где содержатся значения параметров для потребителей показателей и отчетов. Дополнительные сведения о требованиях к редактора и функциональные возможности можно [Редакторы нестандартных объектов PerformancePoint Services](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
  
    
    
Следующие процедуры и примеры основаны на класс **SampleFilterEditor** из [настраиваемых объектов](http://msdn.microsoft.com/library/af021d52-7562-4e7a-9de4-e1fc5784a59d%28Office.15%29.aspx). Редактор — тонкие веб-приложения, которое позволяет пользователям изменять имя и описание фильтра панели и выберите в источнике данных. Полный код для класса, в разделе [пример кода: создание, извлечение и обновление настраиваемых фильтров PerformancePoint Services в SharePoint](#bk_example).
  
    
    
Мы рекомендуем использовать редактор образец как шаблон. В примере демонстрируется как вызов объектов в Службы PerformancePoint Services API, предоставляет вспомогательные объекты, которые упрощают вызывает для репозитория операций (например, создание и обновление объектов) и демонстрируются советы и рекомендации по разработке Службы PerformancePoint Services.
  
    
    

## <a name="create-and-configure-the-editor-class-for-custom-performancepoint-services-filters"></a>Создание и настройка класса редактора для настраиваемых Службы PerformancePoint Services фильтров
<a name="bk_intro"> </a>


  
    
    

1. Установка Службы PerformancePoint Services или копирование библиотеки DLL, которые использует расширения (см. шаг 3) на своем компьютере. Для получения дополнительных сведений см  [Библиотеки DLL служб PerformancePoint, используемые в сценариях развертывания](http://msdn.microsoft.com/library/41e92619-8253-481d-82f9-35b6a6abc477%28Office.15%29.aspx).
    
  
2. В Visual Studio создания библиотеки классов C#. Если вы создали библиотека классов для расширения, добавьте новый класс C#.
    
    DLL-библиотеку необходимо подписать строгим именем. Кроме того, убедитесь, что все сборки, на которые ссылается DLL-библиотека, имеют строгие имена. Процедура подписывания сборки строгим именем и создания пары из открытого и закрытого ключа рассматривается в разделе  [How to: Create a public/private key pair](http://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114.aspx).
    
  
3. Добавьте в проект в качестве ссылок на сборки следующие библиотеки DLL:
    
  - Файл Microsoft.PerformancePoint.Scorecards.Client.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.ServerCommon.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.ServerRendering.dll
    
  
  - Microsoft.PerformancePoint.Scorecards.Store.dll (используется в вспомогательных классах)
    
  
  - Microsoft.SharePoint.dll (используется в вспомогательных классах)
    
  

    Образец редактора также содержит ссылки на сборки System.Web.dll и System.Web.Services.dll. В зависимости от функциональности расширения могут потребоваться другие ссылки в проекте.
    
  
4. Добавьте следующие классы из примера в проект. Редактор использует эти вспомогательные классы для взаимодействия с репозитория Службы PerformancePoint Services:
    
  - DataSourceConsumerHelper.cs
    
  
  - ExtensionRepositoryHelper.cs
    
  
  - FilterRepositoryHelper.cs
    
  
  - IDataSourceConsumer.cs
    
  
5. В классе редактора добавьте директивы **using** для следующих пространств имен Службы PerformancePoint Services.
    
  - **Microsoft.PerformancePoint.Scorecards**
    
  
  - **Microsoft.PerformancePoint.Scorecards.ServerCommon**
    
  
  - **Microsoft.PerformancePoint.Scorecards.ServerRendering**
    
  

    В зависимости от функционального диапазона расширения, могут потребоваться другие директивы **using**.
    
  
6. Определите класс, наследующий базовому классу, поддерживающему данную реализацию редактора. Поскольку образец редактора фильтров является веб-приложением, он наследует классу  [Page](https://msdn.microsoft.com/library/System.Web.UI.Page.aspx) . В других реализациях могут использоваться классы, производные от таких базовых классов, как [UserControl](https://msdn.microsoft.com/library/System.Windows.Forms.UserControl.aspx) или [WebPart](https://msdn.microsoft.com/library/System.Web.UI.WebControls.WebParts.WebPart.aspx) .
    
  
7. Определите элементы управления для доступа к свойствам, которые пользователи смогут просматривать или изменять. В образце редактора фильтров сначала объявляются переменные для серверных веб-элементов управления, определенных в компоненте пользовательского интерфейса, представляющем собой страницу ASPX. В образце редактора также определяется элемент управления "Кнопка", позволяющий пользователям отправлять изменения. Затем в редакторе вызывается метод  [CreateChildControls()](https://msdn.microsoft.com/library/System.Web.UI.Control.CreateChildControls.aspx) , чтобы сделать элементы управления доступными на странице.
    
    > **Примечание:** Редактор определяет логику программирования отдельно от пользовательского интерфейса. Инструкции по созданию компонентов пользовательского интерфейса редактора выходят за рамки данной документации. 

    Редактор фильтров пример выполняет шаги с 8 по 12 в методе **Page_Load**. **Page_Load** также используется для инициализации и проверка переменными и элементами управления, заполнения элементов управления и сохранить сведения о состоянии для настраиваемого фильтра и вспомогательные объекты.
    
  
8. Присвойте свойству  [AllowUnsafeUpdates](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ServerCommon.ServerUtils.AllowUnsafeUpdates.aspx) значение **true**. Это позволит редактору фильтров записывать данные в репозиторий без помощи операций POST формы.
    
  
9. Получите параметры из строки запроса и присвойте их значения локальным переменным, как показано в примере кода ниже.
    
```cs
  
// The URL of the site collection that contains the PerformancePoint Services repository.
string server = Request.QueryString[ClickOnceLaunchKeys.SiteCollectionUrl];

// The location of the filter in the repository.
string itemLocation = Request.QueryString[ClickOnceLaunchKeys.ItemLocation];

// The operation to perform: OpenItem or CreateItem.
string action = Request.QueryString[ClickOnceLaunchKeys.LaunchOperation];
```


```VB.net
  
' The URL of the site collection that contains the PerformancePoint Services repository.
Dim server As String = Request.QueryString(ClickOnceLaunchKeys.SiteCollectionUrl)

' The location of the filter in the repository.
Dim itemLocation As String = Request.QueryString(ClickOnceLaunchKeys.ItemLocation)

' The operation to perform: OpenItem or CreateItem.
Dim action As String = Request.QueryString(ClickOnceLaunchKeys.LaunchOperation)
```


    For information about query string parameters, see  [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx).
    
  
10. Извлеките объект **FilterRepositoryHelper**, который используется для отправки вызовов в репозиторий, как показано в следующем примере кода.
    
```cs
  
filterRepositoryHelper = new FilterRepositoryHelper();
```


```VB.net
  filterRepositoryHelper = New FilterRepositoryHelper()
```

11. Задайте расположение фильтра, используя параметр строки запроса, как показано в следующем примере кода.
    
```cs
  RepositoryLocation repositoryFilterLocation = RepositoryLocation.CreateFromUriString(itemLocation);
```


```VB.net
  Dim repositoryFilterLocation As RepositoryLocation = RepositoryLocation.CreateFromUriString(itemLocation)
```

12. Извлеките из строки запроса выполняемую операцию ( _OpenItem_ или _CreateItem_) и извлечения или создайте настраиваемый фильтр.
    
  - Для извлечения настраиваемого фильтра используйте метод **FilterRepositoryHelper.Get**.
    
  
  - Чтобы создать настраиваемый фильтр, используйте конструктор **Filter()** и определите свойства [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.RendererClassName.aspx) и [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.SubTypeId.aspx) фильтра. [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.SubTypeId.aspx)  уникальный идентификатор для фильтра, а его должен соответствовать атрибуту **subType**, указанная для фильтра в файле web.config Службы PerformancePoint Services. [RendererClassName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.RendererClassName.aspx)  это полное имя класса, который определяет веб-сервер визуализации элемента управления. Если он не определен в редакторе, это значение по умолчанию класса визуализации, которая указана в файле web.config.
    
  

```cs
  if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
{

                // Use the repository-helper object to retrieve the filter.
                filter = filterRepositoryHelper.Get(repositoryFilterLocation);
                if (filter == null)
                {
                    displayError("Could not retrieve the filter for editing.");
                    return;
                }
 }
else if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
{
                filter = new Filter
                {
                    RendererClassName = typeof(MultiSelectTreeViewControl).AssemblyQualifiedName,
                    SubTypeId = "SampleFilter"
                };
}
```


```VB.net
  
If ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase) Then

' Use the repository-helper object to retrieve the filter.
      filter = filterRepositoryHelper.Get(repositoryFilterLocation)
      If filter Is Nothing Then
           displayError("Could not retrieve the filter for editing.")
           Return
      End If

ElseIf ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase) Then
      filter = New Filter With {.RendererClassName = GetType(MultiSelectTreeViewControl).AssemblyQualifiedName, .SubTypeId = "SampleFilter"}
End If
```


    > **Note:**
      > By default, users can create custom objects from PerformancePoint Dashboard Designer only. To enable users to create a custom object outside of Dashboard Designer, you must add a menu item that sends a  _CreateItem_ request to your editor from the content type in the repository. For more information, see [Editors for Custom PerformancePoint Services Objects](http://msdn.microsoft.com/library/7c5924f1-91f3-436a-9d94-2e0dc454c8cc%28Office.15%29.aspx). 
13. Извлеките из репозитория базовый источник данных фильтра. В данном образце редактора фильтров используется свойство **FilterRepositoryHelper.DataSourceHelper** для вызова метода **DataSourceConsumerHelper.GetDataSource**, позволяющего найти источник данных по его расположению в репозитории. Это показано в следующем примере кода.
    
```cs
  
if (!string.IsNullOrEmpty(filter.DataSourceLocation.ItemUrl))
    {
        RepositoryLocation repositoryDatasourceLocation =
        RepositoryLocation.CreateFromUriString(filter.DataSourceLocation.ItemUrl);
        datasource =
        filterRepositoryHelper.DataSourceHelper.GetDataSource(repositoryDatasourceLocation);
    }
```


```VB.net
  
If Not String.IsNullOrEmpty(filter.DataSourceLocation.ItemUrl) Then
      Dim repositoryDatasourceLocation As RepositoryLocation = RepositoryLocation.CreateFromUriString(filter.DataSourceLocation.ItemUrl)
      datasource = filterRepositoryHelper.DataSourceHelper.GetDataSource(repositoryDatasourceLocation)
End If
```

14. Чтобы разрешить пользователям Выбор источника данных для фильтра, заполнения элемента управления выбора с источниками данных Службы PerformancePoint Services. Метод **PopulateDataSourceDropDown** в редакторе фильтров пример вызывает метод **DataSourceConsumerHelper.GetDataSourcesBySourceNames** для получения источников данных. Это показано в следующем примере кода.
    
```cs
  
// The parameter contains the default server-relative URL to the PerformancePoint Data Connections Library.
// Edit this value if you are not using the default path. A leading forward slash may not be needed.
ICollection dataSourceCollection =
    
filterRepositoryHelper.DataSourceHelper.GetDataSourcesBySourceNames
    ("/BICenter/Data%20Connections%20for%20PerformancePoint/",
         new[] { "WSTabularDataSource", DataSourceNames.ExcelWorkbook });
```


```VB.net
  
' The parameter contains the default server-relative URL to the PerformancePoint Data Connections Library.
' Edit this value if you are not using the default path. A leading forward slash may not be needed.
Dim dataSourceCollection As ICollection = filterRepositoryHelper.DataSourceHelper.GetDataSourcesBySourceNames ("("/BICenter/Data%20Connections%20for%20PerformancePoint/", { "WSTabularDataSource", DataSourceNames.ExcelWorkbook })
```


    The sample filter editor retrieves only two types of data source, but you can modify this method to support other data source types or to prompt the user for the type of data source to retrieve. To reference a native data source of a particular type, use the  [SourceName](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SourceName.aspx) property, which returns a field from the [DataSourceNames](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSourceNames.aspx) class. To reference a custom data source, use the [SubTypeId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.SubTypeId.aspx) property of the data source, which is the same value as the **subType** attribute that is registered in the PerformancePoint Services web.config file for the data source extension.
    
    If you modify this method, you must make the corresponding change in the  [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) method in the sample filter's data provider.
    
  
15. Определите начальную точку фильтра, представленную свойством  [BeginPoints](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.BeginPoints.aspx) . Она определяет источник значений фильтра и необходима для того, чтобы иметь возможность отправлять данные из фильтра в системы показателей и отчеты.
    
1. Создайте объект  [ParameterDefinition](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinition.aspx) . Свойство [BeginPoints](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.BeginPoints.aspx) возвращает объект [ParameterDefinitionCollection](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinitionCollection.aspx) , содержащий ровно один объект [ParameterDefinition](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinition.aspx) .
    
  
2. Для задания поставщика данных фильтра установите в качестве значения свойства  [ParameterProviderId](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinition.ParameterProviderId.aspx) уникальный идентификатор поставщика. Он должен соответствовать значению, возвращаемому методом [GetId()](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetId.aspx) поставщика данных.
    
  
3. Чтобы указать источник идентификаторов ключей для значений фильтра, установите в качестве значения свойства  [KeyColumn](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinition.KeyColumn.aspx) столбец таблицы отображаемых данных, содержащий идентификаторы ключей. В данном образце редактора фильтров это свойство определяется как столбец Symbol.
    
  
4. Чтобы указать источник отображаемых значений для элемента управления фильтром, установите в качестве значения свойства  [DisplayColumn](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinition.DisplayColumn.aspx) столбец таблицы отображаемых данных, содержащий отображаемые значения. В данном образце редактора фильтров это свойство определяется как столбец Symbol.
    
  

    > **Примечание:** В таблице данных отображения возвращается свойством [DisplayValues](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ParameterDefinition.DisplayValues.aspx) и инициализации при поставщика данных фильтра вызывает метод [GetDisplayDataInternal](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Server.Extensions.CustomParameterDataProvider.GetDisplayDataInternal.aspx) . Если в таблице данных содержит другие столбцы, можно определить другие сопоставления столбцов для предоставления дополнительных функциональных возможностей.

```cs
  
if (0 == filter.BeginPoints.Count)
{
    ParameterDefinition paramDef = new ParameterDefinition();

    // Reference the data provider.
    paramDef.ParameterProviderId = "SampleFilterDataProvider";
    paramDef.DefaultPostFormula = string.Empty;

    // Specify the column that contains the key identifiers and the column
    // that contains the display values. The sample uses the same column
    // for both purposes.
    // These values must match the structure of the data table that is
    // returned by the ParameterDefinition.DisplayValues property.

    paramDef.KeyColumn = "Symbol";
    paramDef.DisplayColumn = "Symbol";

    // You can use this property to store custom information for this filter.
    paramDef.CustomDefinition = string.Empty;
    
    filter.BeginPoints.Add(paramDef);
}
```


```VB.net
  
If 0 = filter.BeginPoints.Count Then
        Dim paramDef As New ParameterDefinition()

        ' Reference the data provider.
      paramDef.ParameterProviderId = "SampleFilterDataProvider"
      paramDef.DefaultPostFormula = String.Empty

        ' Specify the column that contains the key identifiers and the column
        ' that contains the display values. The sample uses the same column
        ' for both purposes.
        ' These values must match the structure of the data table that is
        ' returned by the ParameterDefinition.DisplayValues property.

      paramDef.KeyColumn = "Symbol"
      paramDef.DisplayColumn = "Symbol"

        ' You can use this property to store custom information for this filter.
      paramDef.CustomDefinition = String.Empty

      filter.BeginPoints.Add(paramDef)
End If
```


    The sample editor defines its beginpoint in the **VerifyFilter** method. It also uses **VerifyFilter** to verify that required properties are set and to define the selection mode, which is an optional property.
    
  
16. Инициализируйте фильтр, выполнив запрос фильтра и получив данные из источника данных. Метод **buttonOK_Click** в данном образце редактора фильтров вызывает метод **FilterRepositoryHelper.GetParameterDisplayData** для инициализации фильтра.
    
    > **Примечание:** **Filterrepositoryhelper.getparameterdisplaydata должен по крайней мере один раз перед обновлением объекта фильтра.**
17. Обновите фильтр, применив изменения, определенные пользователем. Метод **buttonOK_Click** в образце редактора фильтров вызывает метод **FilterRepositoryHelper.Update** для обновления свойств [Name](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Description](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) и [DataSourceLocation](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.DataSourceLocation.aspx) данного фильтра в репозитории. Кроме того, с помощью метода **buttonOK_Click** проверяется содержимое элементов управления и извлекается информация о состоянии настраиваемого фильтра и вспомогательного объекта.
    
    > **Примечание:** Пользователи могут задать [имя](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Name.aspx) , [Описание](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Description.aspx) и свойства [Owner](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Element.Owner.aspx) ( **Ответственное лицо**) настраиваемого объекта и удалять настраиваемые объекты непосредственно из конструктора панели мониторинга и репозитория служб PerformancePoint Services. 

## <a name="code-example-create-retrieve-and-update-custom-performancepoint-services-filters-in-sharepoint"></a>Пример кода: создание, извлечение и обновление настраиваемых фильтров PerformancePoint Services в SharePoint
<a name="bk_example"> </a>

В следующем примере кода создается, извлекаются и обновление настраиваемых фильтров. Этот код  от класса редактор кода, который содержит логику программирования для элементов управления, определенных на ASPX-странице.
  
    
    
Перед компиляцией этого примера кода необходимо настроить среду разработки, как описано в статье  [Создание и настройка класса редактора для редактор фильтров в PerformancePoint Services](#bk_intro).
  
    
    



```cs

using System;
using System.Collections;
using System.Collections.Generic;
using System.Data;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.PerformancePoint.Scorecards; 
using Microsoft.PerformancePoint.Scorecards.ServerCommon;
using Microsoft.PerformancePoint.Scorecards.ServerRendering;

namespace Microsoft.PerformancePoint.SDK.Samples.SampleFilter
{

    // Represents the class that defines the sample filter editor.
    public class SampleFilterEditor : Page
    {

        // Declare private variables for the ASP.NET controls defined in the user interface.
        // The sample's user interface is an ASPX page that defines the controls in HTML.
        private TextBox textboxName;
        private TextBox textboxDescription;
        private Label labelErrorMessage;
        private DropDownList dropdownlistDataSource;
        private Button buttonOK;
        private ListBox listboxStocks;

        // Make the controls available to this class.
        protected override void CreateChildControls()
        {
            base.CreateChildControls();

            if (null == textboxName) 
                textboxName = FindControl("textboxName") as TextBox;
            if (null == textboxDescription) 
                textboxDescription = FindControl("textboxDescription") as TextBox;
            if (null == dropdownlistDataSource) 
                dropdownlistDataSource = FindControl("dropdownlistDataSource") as DropDownList;
            if (null == labelErrorMessage)
                labelErrorMessage = FindControl("labelErrorMessage") as Label;
            if (null==buttonOK)
                buttonOK = FindControl("buttonOK") as Button;
            if (null==listboxStocks)
                listboxStocks = FindControl("listboxStocks") as ListBox;
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
                FilterRepositoryHelper filterRepositoryHelper = null;
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
                    filterRepositoryHelper =
                        new FilterRepositoryHelper();

                    // Set the filter location.
                    RepositoryLocation repositoryFilterLocation = RepositoryLocation.CreateFromUriString(itemLocation);

                    Filter filter;
                    DataSource datasource = null;

                    // Retrieve or create the filter object, depending on the operation
                    // passed in the query string (OpenItem or CreateItem).
                    if (ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {

                        // Retrieve the filter object by using the repository-helper object.
                        filter = filterRepositoryHelper.Get(repositoryFilterLocation);
                        if (filter == null)
                        {
                            displayError("Could not retrieve the filter for editing.");
                            return;
                        }

                    }
                    else if (ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase))
                    {

                        // Create a filter.
                        // CreateItem requests can be sent from a SharePoint list, but
                        // you must create a custom menu item to send the request.
                        // Dashboard Designer can send edit requests only.
                        filter = new Filter
                            {

                                // Specify the class that defines the renderer
                                // web server control. The sample filter uses a native
                                // PerformancePoint Services renderer.
                                // Defaults to the value specified in the web.config file
                                RendererClassName = typeof(MultiSelectTreeViewControl).AssemblyQualifiedName,

                                // Specify the unique identifier for the filter.
                                // The SubTypeId property must match the
                                // subType attribute in the web.config file.
                                SubTypeId = "SampleFilter"
                            };
                    }
                    else
                    {
                        displayError("Invalid Action.");
                        return;
                    }

                    VerifyFilter(filter);

                    // Retrieve filter's underlying data source.
                    if (!string.IsNullOrEmpty(filter.DataSourceLocation.ItemUrl))
                    {
                        RepositoryLocation repositoryDatasourceLocation =
                            RepositoryLocation.CreateFromUriString(filter.DataSourceLocation.ItemUrl);
                        datasource =

                            // Gets a PerformancePoint Services data source by using the
                            // DataSourceHelper property to call the
                            // DataSourceConsumerHelper.GetDataSource method. 
                            filterRepositoryHelper.DataSourceHelper.GetDataSource(repositoryDatasourceLocation);
                    }

                    // Save the original filter and helper objects across page postbacks.
                    ViewState["action"] = action;
                    ViewState["filter"] = filter;
                    ViewState["filterrepositoryhelper"] = filterRepositoryHelper;
                    ViewState["itemlocation"] = itemLocation;

                    // Populate the child controls.
                    textboxName.Text = filter.Name.ToString();
                    textboxDescription.Text = filter.Description.ToString();

                    // Populate the dropdownlistDataSource control with data sources of specific
                    // types from the PerformancePoint Services repository.
                    // This method looks up the passed data source in the data sources
                    // that are registered in the web.config file. 
                    // Although the sample retrieves data sources of two specific types,
                    // you can modify it to prompt the user for a data source type.
                    PopulateDataSourceDropDown(datasource);

                    // Call the SelectedIndexChanged event directly to populate the 
                    // listbox control with preview data.
                    dropdownlistDataSource_SelectedIndexChanged(null, null);
                }
                catch (Exception ex)
                {
                    displayError("An error has occurred. Please contact your administrator for more information.");
                    if (filterRepositoryHelper != null)
                    {
                        // Add the exception detail to the server event log.
                        filterRepositoryHelper.HandleException(ex);
                    }
                }
            }
        }

        // Handles the SelectedIndexChanged event of the dropdownlistDataSource control.
        protected void dropdownlistDataSource_SelectedIndexChanged(object sender, EventArgs e)
        {
            EnsureChildControls();

            // Check if a valid data source is selected.
            if (null != dropdownlistDataSource.SelectedItem &amp;&amp;
                !string.IsNullOrEmpty(dropdownlistDataSource.SelectedItem.Text))
            {
                // Retrieve the data source object.
                FilterRepositoryHelper filterRepositoryHelper =
                    (FilterRepositoryHelper)ViewState["filterrepositoryhelper"];
                string selectedDataSourceItemUrl = dropdownlistDataSource.SelectedItem.Value;

                RepositoryLocation repositoryDatasourceLocation =
                    RepositoryLocation.CreateFromUriString(selectedDataSourceItemUrl);
                DataSource datasource = filterRepositoryHelper.DataSourceHelper.GetDataSource(repositoryDatasourceLocation);
                ViewState["datasource"] = datasource;

                // Populate the listboxStocks control with the preview data for the selected
                // data source.
                PopulateListBoxData(datasource);
            }
            else
            {
                ClearStocksListBox();
            }
        }

        // Clears the listboxStocks control.
        // The sample filter works with a web service that provides stock information.
        private void ClearStocksListBox()
        {
            listboxStocks.DataSource = null;
            listboxStocks.DataBind();
            listboxStocks.Items.Clear();
        }

        // Handles the Click event of the buttonOK control.
        protected void buttonOK_Click(object sender, EventArgs e)
        {
            EnsureChildControls();

            // Verify that the controls contain values.
            if (string.IsNullOrEmpty(textboxName.Text))
            {
                labelErrorMessage.Text = "A filter name is required.";
                return;
            }
            if (dropdownlistDataSource.SelectedIndex == 0)
            {
                labelErrorMessage.Text = "A data source is required.";
                return;
            }

            // Clear any pre-existing error message.
            labelErrorMessage.Text = string.Empty;

            // Retrieve the filter, data source, and helper objects from view state.
            string action = (string)ViewState["action"];
            string itemLocation = (string) ViewState["itemlocation"];
            Filter filter = (Filter)ViewState["filter"];
            DataSource datasource = (DataSource)ViewState["datasource"];
            FilterRepositoryHelper filterRepositoryHelper = (FilterRepositoryHelper)ViewState["filterrepositoryhelper"];

            // Update the filter object with form changes.
            filter.Name.Text = textboxName.Text;
            filter.Description.Text = textboxDescription.Text;
            filter.DataSourceLocation = datasource.Location;
            foreach (ParameterDefinition parameterDefinition in filter.BeginPoints)
            {
                parameterDefinition.DisplayName = filter.Name.Text;
            }

            // Initialize the filter. This method runs the filter's query and retrieves preview data.
            filterRepositoryHelper.GetParameterDisplayData(ref filter);

            // Save the filter object to the PerformancePoint Services repository.
            try
            {
                filter.Validate();

                if (ClickOnceLaunchValues.CreateItem.Equals(action,StringComparison.OrdinalIgnoreCase))
                {
                    Filter newFilter = filterRepositoryHelper.Create(
                        string.IsNullOrEmpty(filter.Location.ItemUrl) ? itemLocation : filter.Location.ItemUrl, filter);
                    ViewState["filter"] = newFilter;
                    ViewState["action"] = ClickOnceLaunchValues.OpenItem;
                }
                else
                {
                    filterRepositoryHelper.Update(filter);
                }
            }
            catch (Exception ex)
            {
                displayError("An error has occurred. Please contact your administrator for more information.");
                if (filterRepositoryHelper != null)
                {

                    // Add the exception detail to the server event log.
                    filterRepositoryHelper.HandleException(ex);
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

        // Verifies that the properties for the filter object are set.
        static void VerifyFilter(Filter filter)
        {

            if (null != filter)
            {

                // Verify that all required properties are set.
                if (string.IsNullOrEmpty(filter.SubTypeId)) 
                {

                    // This value must match the subType attribute specified
                    // in the web.config file.
                    filter.SubTypeId = "SampleFilter";
                }

                if (string.IsNullOrEmpty(filter.RendererClassName)) 
                {
                    filter.RendererClassName = typeof (MultiSelectTreeViewControl).AssemblyQualifiedName; 
                }

                // Define the BeginPoints property so the filter can send a parameter value to
                // scorecards and reports.
                // The value must be from the KeyColumn of the display
                // DataTable object, which is defined in the data provider. The data table is
                // returned by the FilterRepositoryHelper.GetParameterDisplayData method.
                // A filter has one beginpoint only, and it is represented by a
                // ParameterDefinition object. The ParameterDefinition object defines how
                // the filter accesses the data.
                if (0 == filter.BeginPoints.Count)
                {
                    ParameterDefinition paramDef = new ParameterDefinition
                                                       {
                                                           // This value must match the value returned 
                                                           // by the data provider's GetId method.
                                                           ParameterProviderId = "SampleFilterDataProvider",

                                                           // Reference the data provider.
                                                           DefaultPostFormula = string.Empty,

                                                           // Specify the column that contains
                                                           // the key identifiers and the column
                                                           // that contains the display values.
                                                           // The sample uses the same column
                                                           // for both purposes.
                                                           // These values must match the structure
                                                           // of the data table that is returned
                                                           // by the ParameterDefinition.DisplayValues property.
                                                           KeyColumn = "Symbol",
                                                           DisplayColumn = "Symbol",

                                                           // You can use this property to store
                                                           // extra information for this filter.
                                                           CustomDefinition = string.Empty
                                                       };
                    filter.BeginPoints.Add(paramDef);
                }

                // Set optional properties. The renderer can return multiple values. 
                filter.SelectionMode = FilterSelectionMode.MultiSelect;
            }
        }

        // Populates the dropdownlistDataSource control.
        void PopulateDataSourceDropDown(DataSource filterDataSource)
        {
            EnsureChildControls();
            
            FilterRepositoryHelper filterRepositoryHelper =
                (FilterRepositoryHelper)ViewState["filterrepositoryhelper"];

            // Retrieve data sources from the repository by using the DataSourceHelper
            // property to call the DataSourceConsumerHelper object.
            // If you modify the types of data source to retrieve, you must make the corresponding
            // change in the filter's data provider.
            // The parameter contains the default server-relative URL to the PerformancePoint Data Connections Library.
            // Edit this value if you are not using the default path. A leading forward slash may not be needed.
            ICollection dataSourceCollection = filterRepositoryHelper.DataSourceHelper.GetDataSourcesBySourceNames("/BICenter/Data%20Connections%20for%20PerformancePoint/",
                new[] { "WSTabularDataSource", DataSourceNames.ExcelWorkbook });
            if (null == dataSourceCollection)
            {
                displayError("No available data sources were found.");
                return;
            }

            // Create a list of name/value pairs for the dropdownlistDataSource control.
            var dataSources = new List<KeyValuePair<string, string>>();
            int selectedIndex = 0;
            int i = 1;
            dataSources.Add(new KeyValuePair<string, string>(string.Empty, string.Empty));

            foreach (DataSource ds in dataSourceCollection)
            {
                dataSources.Add(new KeyValuePair<string, string>(ds.Name.Text, ds.Location.ItemUrl));

                // Check if the entry is the originally selected data source.
                if ((filterDataSource != null) &amp;&amp;
                    (string.Compare(ds.Name.Text, filterDataSource.Name.Text) == 0))
                {
                    selectedIndex = i;
                }
                ++i;
            }

            dropdownlistDataSource.DataSource = dataSources;
            dropdownlistDataSource.DataTextField = "Key";
            dropdownlistDataSource.DataValueField = "Value";
            dropdownlistDataSource.DataBind();
            dropdownlistDataSource.SelectedIndex = selectedIndex;
        }


        // Populate the list box data.
        void PopulateListBoxData(DataSource datasource)
        {
            EnsureChildControls();
            
            ClearStocksListBox();
            
            FilterRepositoryHelper filterRepositoryHelper =
                (FilterRepositoryHelper)ViewState["filterrepositoryhelper"];

            // Retrieve the first 100 rows of the preview data from the data source
            DataSet dataSet = filterRepositoryHelper.DataSourceHelper.GetDataSet(100, datasource);

            if (null != dataSet &amp;&amp; null != dataSet.Tables[0])
            {
                listboxStocks.DataTextField = "Symbol";
                listboxStocks.DataValueField = "Value";
                listboxStocks.DataSource = dataSet.Tables[0];
                listboxStocks.DataBind();
            }
        }
    }
}
```




```VB.net

'INSTANT VB NOTE: This code snippet uses implicit typing. You will need to set 'Option Infer On' in the VB file or set 'Option Infer' at the project level:

Imports System
Imports System.Collections
Imports System.Collections.Generic
Imports System.Data
Imports System.Web.UI
Imports System.Web.UI.WebControls
Imports Microsoft.PerformancePoint.Scorecards
Imports Microsoft.PerformancePoint.Scorecards.ServerCommon
Imports Microsoft.PerformancePoint.Scorecards.ServerRendering

Namespace Microsoft.PerformancePoint.SDK.Samples.SampleFilter

    ' Represents the class that defines the sample filter editor.
    Public Class SampleFilterEditor
        Inherits Page

        ' Declare private variables for the ASP.NET controls defined in the user interface.
        ' The sample's user interface is an ASPX page that defines the controls in HTML.
        Private textboxName As TextBox
        Private textboxDescription As TextBox
        Private labelErrorMessage As Label
        Private dropdownlistDataSource As DropDownList
        Private buttonOK As Button
        Private listboxStocks As ListBox

        ' Make the controls available to this class.
        Protected Overrides Sub CreateChildControls()
            MyBase.CreateChildControls()

            If Nothing Is textboxName Then
                textboxName = TryCast(FindControl("textboxName"), TextBox)
            End If
            If Nothing Is textboxDescription Then
                textboxDescription = TryCast(FindControl("textboxDescription"), TextBox)
            End If
            If Nothing Is dropdownlistDataSource Then
                dropdownlistDataSource = TryCast(FindControl("dropdownlistDataSource"), DropDownList)
            End If
            If Nothing Is labelErrorMessage Then
                labelErrorMessage = TryCast(FindControl("labelErrorMessage"), Label)
            End If
            If Nothing Is buttonOK Then
                buttonOK = TryCast(FindControl("buttonOK"), Button)
            End If
            If Nothing Is listboxStocks Then
                listboxStocks = TryCast(FindControl("listboxStocks"), ListBox)
            End If
        End Sub

        ' Handles the Load event of the Page control.
        ' Methods that use a control variable should call the Control.EnsureChildControls
        ' method before accessing the variable for the first time.
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs)

            ' Required to enable custom report and filter editors to
            ' write data to the repository.
            ServerUtils.AllowUnsafeUpdates = True

            ' Initialize controls the first time the page loads only.
            If Not IsPostBack Then
                EnsureChildControls()
                Dim filterRepositoryHelper As FilterRepositoryHelper = Nothing
                Try

                    ' Get information from the query string parameters.
                    Dim server As String = Request.QueryString(ClickOnceLaunchKeys.SiteCollectionUrl)
                    Dim itemLocation As String = Request.QueryString(ClickOnceLaunchKeys.ItemLocation)
                    Dim action As String = Request.QueryString(ClickOnceLaunchKeys.LaunchOperation)

                    ' Validate the query string parameters.
                    If String.IsNullOrEmpty(server) OrElse String.IsNullOrEmpty(itemLocation) OrElse String.IsNullOrEmpty(action) Then
                        displayError("Invalid URL.")
                        Return
                    End If

                    ' Retrieve the repository-helper object.
                    filterRepositoryHelper = New FilterRepositoryHelper()

                    ' Set the filter location.
                    Dim repositoryFilterLocation As RepositoryLocation = RepositoryLocation.CreateFromUriString(itemLocation)

                    Dim filter As Filter
                    Dim datasource As DataSource = Nothing

                    ' Retrieve or create the filter object, depending on the operation
                    ' passed in the query string (OpenItem or CreateItem).
                    If ClickOnceLaunchValues.OpenItem.Equals(action, StringComparison.OrdinalIgnoreCase) Then

                        ' Retrieve the filter object by using the repository-helper object.
                        filter = filterRepositoryHelper.Get(repositoryFilterLocation)
                        If filter Is Nothing Then
                            displayError("Could not retrieve the filter for editing.")
                            Return
                        End If

                    ElseIf ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase) Then

                        ' Create a filter.
                        ' CreateItem requests can be sent from a SharePoint list, but
                        ' you must create a custom menu item to send the request.
                        ' Dashboard Designer can send edit requests only.
                        filter = New Filter With {.RendererClassName = GetType(MultiSelectTreeViewControl).AssemblyQualifiedName, .SubTypeId = "SampleFilter"}
                        ' Specify the class that defines the renderer
                        ' web server control. The sample filter uses a native
                        ' PerformancePoint Services renderer.
                        ' Defaults to the value specified in the web.config file
                        ' Specify the unique identifier for the filter.
                        ' The SubTypeId property must match the
                        ' subType attribute in the web.config file.
                    Else
                        displayError("Invalid Action.")
                        Return
                    End If

                    VerifyFilter(filter)

                    ' Retrieve filter's underlying data source.
                    If Not String.IsNullOrEmpty(filter.DataSourceLocation.ItemUrl) Then
                        Dim repositoryDatasourceLocation As RepositoryLocation = RepositoryLocation.CreateFromUriString(filter.DataSourceLocation.ItemUrl)
                        ' Gets a PerformancePoint Services data source by using the
                        ' DataSourceHelper property to call the
                        ' DataSourceConsumerHelper.GetDataSource method. 
                        datasource = filterRepositoryHelper.DataSourceHelper.GetDataSource(repositoryDatasourceLocation)
                    End If

                    ' Save the original filter and helper objects across page postbacks.
                    ViewState("action") = action
                    ViewState("filter") = filter
                    ViewState("filterrepositoryhelper") = filterRepositoryHelper
                    ViewState("itemlocation") = itemLocation

                    ' Populate the child controls.
                    textboxName.Text = filter.Name.ToString()
                    textboxDescription.Text = filter.Description.ToString()

                    ' Populate the dropdownlistDataSource control with data sources of specific
                    ' types from the PerformancePoint Services repository.
                    ' This method looks up the passed data source in the data sources
                    ' that are registered in the web.config file. 
                    ' Although the sample retrieves data sources of two specific types,
                    ' you can modify it to prompt the user for a data source type.
                    PopulateDataSourceDropDown(datasource)

                    ' Call the SelectedIndexChanged event directly to populate the 
                    ' listbox control with preview data.
                    dropdownlistDataSource_SelectedIndexChanged(Nothing, Nothing)
                Catch ex As Exception
                    displayError("An error has occurred. Please contact your administrator for more information.")
                    If filterRepositoryHelper IsNot Nothing Then
                        ' Add the exception detail to the server event log.
                        filterRepositoryHelper.HandleException(ex)
                    End If
                End Try
            End If
        End Sub

        ' Handles the SelectedIndexChanged event of the dropdownlistDataSource control.
        Protected Sub dropdownlistDataSource_SelectedIndexChanged(ByVal sender As Object, ByVal e As EventArgs)
            EnsureChildControls()

            ' Check if a valid data source is selected.
            If Nothing IsNot dropdownlistDataSource.SelectedItem AndAlso (Not String.IsNullOrEmpty(dropdownlistDataSource.SelectedItem.Text)) Then
                ' Retrieve the data source object.
                Dim filterRepositoryHelper As FilterRepositoryHelper = CType(ViewState("filterrepositoryhelper"), FilterRepositoryHelper)
                Dim selectedDataSourceItemUrl As String = dropdownlistDataSource.SelectedItem.Value

                Dim repositoryDatasourceLocation As RepositoryLocation = RepositoryLocation.CreateFromUriString(selectedDataSourceItemUrl)
                Dim datasource As DataSource = filterRepositoryHelper.DataSourceHelper.GetDataSource(repositoryDatasourceLocation)
                ViewState("datasource") = datasource

                ' Populate the listboxStocks control with the preview data for the selected
                ' data source.
                PopulateListBoxData(datasource)
            Else
                ClearStocksListBox()
            End If
        End Sub

        ' Clears the listboxStocks control.
        ' The sample filter works with a web service that provides stock information.
        Private Sub ClearStocksListBox()
            listboxStocks.DataSource = Nothing
            listboxStocks.DataBind()
            listboxStocks.Items.Clear()
        End Sub

        ' Handles the Click event of the buttonOK control.
        Protected Sub buttonOK_Click(ByVal sender As Object, ByVal e As EventArgs)
            EnsureChildControls()

            ' Verify that the controls contain values.
            If String.IsNullOrEmpty(textboxName.Text) Then
                labelErrorMessage.Text = "A filter name is required."
                Return
            End If
            If dropdownlistDataSource.SelectedIndex = 0 Then
                labelErrorMessage.Text = "A data source is required."
                Return
            End If

            ' Clear any pre-existing error message.
            labelErrorMessage.Text = String.Empty

            ' Retrieve the filter, data source, and helper objects from view state.
            Dim action As String = CStr(ViewState("action"))
            Dim itemLocation As String = CStr(ViewState("itemlocation"))
            Dim filter As Filter = CType(ViewState("filter"), Filter)
            Dim datasource As DataSource = CType(ViewState("datasource"), DataSource)
            Dim filterRepositoryHelper As FilterRepositoryHelper = CType(ViewState("filterrepositoryhelper"), FilterRepositoryHelper)

            ' Update the filter object with form changes.
            filter.Name.Text = textboxName.Text
            filter.Description.Text = textboxDescription.Text
            filter.DataSourceLocation = datasource.Location
            For Each parameterDefinition As ParameterDefinition In filter.BeginPoints
                parameterDefinition.DisplayName = filter.Name.Text
            Next parameterDefinition

            ' Initialize the filter. This method runs the filter's query and retrieves preview data.
            filterRepositoryHelper.GetParameterDisplayData(filter)

            ' Save the filter object to the PerformancePoint Services repository.
            Try
                filter.Validate()

                If ClickOnceLaunchValues.CreateItem.Equals(action, StringComparison.OrdinalIgnoreCase) Then
                    Dim newFilter As Filter = filterRepositoryHelper.Create(If(String.IsNullOrEmpty(filter.Location.ItemUrl), itemLocation, filter.Location.ItemUrl), filter)
                    ViewState("filter") = newFilter
                    ViewState("action") = ClickOnceLaunchValues.OpenItem
                Else
                    filterRepositoryHelper.Update(filter)
                End If
            Catch ex As Exception
                displayError("An error has occurred. Please contact your administrator for more information.")
                If filterRepositoryHelper IsNot Nothing Then

                    ' Add the exception detail to the server event log.
                    filterRepositoryHelper.HandleException(ex)
                End If
            End Try
        End Sub

        ' Displays the error string in the labelErrorMessage label.
        Private Sub displayError(ByVal msg As String)
            EnsureChildControls()

            labelErrorMessage.Text = msg

            ' Disable the OK button because the page is in an error state.
            buttonOK.Enabled = False
            Return
        End Sub

        ' Verifies that the properties for the filter object are set.
        Private Shared Sub VerifyFilter(ByVal filter As Filter)

            If Nothing IsNot filter Then

                ' Verify that all required properties are set.
                If String.IsNullOrEmpty(filter.SubTypeId) Then

                    ' This value must match the subType attribute specified
                    ' in the web.config file.
                    filter.SubTypeId = "SampleFilter"
                End If

                If String.IsNullOrEmpty(filter.RendererClassName) Then
                    filter.RendererClassName = GetType(MultiSelectTreeViewControl).AssemblyQualifiedName
                End If

                ' Define the BeginPoints property so the filter can send a parameter value to
                ' scorecards and reports.
                ' The value must be from the KeyColumn of the display
                ' DataTable object, which is defined in the data provider. The data table is
                ' returned by the FilterRepositoryHelper.GetParameterDisplayData method.
                ' A filter has one beginpoint only, and it is represented by a
                ' ParameterDefinition object. The ParameterDefinition object defines how
                ' the filter accesses the data.
                If 0 = filter.BeginPoints.Count Then
                    Dim paramDef As ParameterDefinition = New ParameterDefinition With {.ParameterProviderId = "SampleFilterDataProvider", .DefaultPostFormula = String.Empty, .KeyColumn = "Symbol", .DisplayColumn = "Symbol", .CustomDefinition = String.Empty}
                    ' This value must match the value returned 
                    ' by the data provider's GetId method.
                    ' Reference the data provider.
                    ' Specify the column that contains
                    ' the key identifiers and the column
                    ' that contains the display values.
                    ' The sample uses the same column
                    ' for both purposes.
                    ' These values must match the structure
                    ' of the data table that is returned
                    ' by the ParameterDefinition.DisplayValues property.
                    ' You can use this property to store
                    ' extra information for this filter.
                    filter.BeginPoints.Add(paramDef)
                End If

                ' Set optional properties. The renderer can return multiple values. 
                filter.SelectionMode = FilterSelectionMode.MultiSelect
            End If
        End Sub

        ' Populates the dropdownlistDataSource control.
        Private Sub PopulateDataSourceDropDown(ByVal filterDataSource As DataSource)
            EnsureChildControls()

            Dim filterRepositoryHelper As FilterRepositoryHelper = CType(ViewState("filterrepositoryhelper"), FilterRepositoryHelper)

            ' Retrieve data sources from the repository by using the DataSourceHelper
            ' property to call the DataSourceConsumerHelper object.
            ' If you modify the types of data source to retrieve, you must make the corresponding
            ' change in the filter's data provider.
            ' The parameter contains the default server-relative URL to the PerformancePoint Data Connections Library.
            ' Edit this value if you are not using the default path. A leading forward slash may not be needed.
            Dim dataSourceCollection As ICollection = filterRepositoryHelper.DataSourceHelper.GetDataSourcesBySourceNames("/BICenter/Data%20Connections%20for%20PerformancePoint/", {"WSTabularDataSource", DataSourceNames.ExcelWorkbook})
            If Nothing Is dataSourceCollection Then
                displayError("No available data sources were found.")
                Return
            End If

            ' Create a list of name/value pairs for the dropdownlistDataSource control.
            Dim dataSources = New List(Of KeyValuePair(Of String, String))()
            Dim selectedIndex As Integer = 0
            Dim i As Integer = 1
            dataSources.Add(New KeyValuePair(Of String, String)(String.Empty, String.Empty))

            For Each ds As DataSource In dataSourceCollection
                dataSources.Add(New KeyValuePair(Of String, String)(ds.Name.Text, ds.Location.ItemUrl))

                ' Check if the entry is the originally selected data source.
                If (filterDataSource IsNot Nothing) AndAlso (String.Compare(ds.Name.Text, filterDataSource.Name.Text) = 0) Then
                    selectedIndex = i
                End If
                i += 1
            Next ds

            dropdownlistDataSource.DataSource = dataSources
            dropdownlistDataSource.DataTextField = "Key"
            dropdownlistDataSource.DataValueField = "Value"
            dropdownlistDataSource.DataBind()
            dropdownlistDataSource.SelectedIndex = selectedIndex
        End Sub


        ' Populate the list box data.
        Private Sub PopulateListBoxData(ByVal datasource As DataSource)
            EnsureChildControls()

            ClearStocksListBox()

            Dim filterRepositoryHelper As FilterRepositoryHelper = CType(ViewState("filterrepositoryhelper"), FilterRepositoryHelper)

            ' Retrieve the first 100 rows of the preview data from the data source
            Dim dataSet As DataSet = filterRepositoryHelper.DataSourceHelper.GetDataSet(100, datasource)

            If Nothing IsNot dataSet AndAlso Nothing IsNot dataSet.Tables(0) Then
                listboxStocks.DataTextField = "Symbol"
                listboxStocks.DataValueField = "Value"
                listboxStocks.DataSource = dataSet.Tables(0)
                listboxStocks.DataBind()
            End If
        End Sub
    End Class
End Namespace
```


## <a name="next-steps"></a>Дальнейшие действия
<a name="bk_example"> </a>

После создания в редакторе фильтров (включая его пользовательского интерфейса, при необходимости) и поставщика данных, как описано в  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx)развертывания расширения.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addResources"> </a>


-  [Как: создать фильтр поставщиков данных для служб PerformancePoint Services в SharePoint](https://msdn.microsoft.com/en-us/library/office/cc159445.aspx)
    
  
-  [PerformancePoint Services в SharePoint](https://msdn.microsoft.com/en-us/library/office/ee559635.aspx)
    
  

