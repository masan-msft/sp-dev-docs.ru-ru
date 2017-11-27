---
title: "Используйте несколько списков SharePoint в приложении Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5251d35a-d659-49b3-8e0d-dfd4a7faee6b
ms.openlocfilehash: 08638a14c0cd602dfb4cb1288fbe089ccace16fc
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="use-multiple-sharepoint-lists-in-a-windows-phone-app"></a><span data-ttu-id="93b21-102">Используйте несколько списков SharePoint в приложении Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93b21-102">Use multiple SharePoint lists in a Windows Phone app</span></span>
<span data-ttu-id="93b21-p101">Создайте приложения Windows Phone, использующие данные из нескольких списков SharePoint. Можно использовать несколько списков SharePoint в приложении несколькими способами. При создании приложения Windows Phone, на основе шаблона приложения списка SharePoint для Windows Phone, укажите единого целевого списка SharePoint, но архитектура результирующий проект расширяемой, чтобы учесть интеграции нескольких списков.</span><span class="sxs-lookup"><span data-stu-id="93b21-p101">Create Windows Phone apps that use data from multiple SharePoint lists. You can use multiple SharePoint lists in your app in several ways. When you create a Windows Phone app based on the Windows Phone SharePoint List Application template, you specify a single target SharePoint list, but the architecture of the resulting project is extensible enough to accommodate the integration of multiple lists.</span></span>
  
    
    


> <span data-ttu-id="93b21-106">**Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="93b21-106">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="93b21-107">За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="93b21-107">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="93b21-108">> Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="93b21-108">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="create-a-solution-involving-sharepoint-lists-based-on-the-same-schema"></a><span data-ttu-id="93b21-109">Создание решения, включающие использование списков SharePoint на основе же схемы</span><span class="sxs-lookup"><span data-stu-id="93b21-109">Create a solution involving SharePoint lists based on the same schema</span></span>
<span data-ttu-id="93b21-110"><a name="BKMK_SameSchemaProject"> </a></span><span class="sxs-lookup"><span data-stu-id="93b21-110"></span></span>

<span data-ttu-id="93b21-111">Если у вас есть два списка SharePoint, на основе же схемы, можно воспользоваться преимуществами классы, реализованный шаблона приложения списка SharePoint для Windows Phone и создание объектов классов для каждого списка.</span><span class="sxs-lookup"><span data-stu-id="93b21-111">If you have two SharePoint lists based on the same schema, you can take advantage of the classes implemented by the Windows Phone SharePoint List Application template and create objects of those classes specific to each list.</span></span>
  
    
    
<span data-ttu-id="93b21-p103">Предположим, что у вас есть два списка SharePoint, на основе шаблона списка контактов. Один список, с именем, например, группа маркетинга, содержит члены группы маркетинга в вашей организации, а списке другие команды разработчиков участники инженерной группы. При создании проекта с помощью шаблона приложения списка SharePoint для Windows Phone и указать группы маркетинга списка в качестве целевого списка на основе которого нужно создать проект экземпляр класса **ListDataProvider** создается в реализация класса **App** в файл App.xaml.cs в проекте (именованные **DataProvider** по умолчанию). Этот объект представляет список список (то есть, группа маркетинга) как источник данных для приложения, предоставляя операции для доступа и работа с элементами в списке. Для списка, лежащие в основе приложения также создается экземпляр класса **ListViewModel**. Этот объект содержит свойство участником (который также быть с именем **DataProvider**), который может иметь значение данного экземпляра класса **ListDataProvider** установление источник данных для экземпляра класса **ListViewModel**.</span><span class="sxs-lookup"><span data-stu-id="93b21-p103">Suppose you have two SharePoint lists based on the Contacts list template. One list, named, for instance, Marketing Team, contains members of a marketing team at your organization, and the other list, Engineering Team, contains members of an engineering team. If you create a project using the Windows Phone SharePoint List Application template and specify the Marketing Team list as the target list on which to base the project, an instance of the **ListDataProvider** class is created (named **DataProvider** by default) in the implementation of the **App** class in the App.xaml.cs file in the project. This object represents the list (that is, the Marketing Team) list as a data source for the app, providing operations to access and manipulate items in the list. An instance of the **ListViewModel** class is also created for the list on which the app is based. This object has a property member (which also happens to be named **DataProvider**) that can be set to a given instance of the **ListDataProvider** class, establishing the data source for the **ListViewModel** class instance.</span></span>
  
    
    
<span data-ttu-id="93b21-p104">Можно создать дополнительные экземпляр класса **ListDataProvider** в проект в качестве источника данных для второго списка (командой разработчиков) в файл App.xaml.cs. В следующем коде объект называется **SecondaryDataProvider**.</span><span class="sxs-lookup"><span data-stu-id="93b21-p104">You can create an additional instance of the **ListDataProvider** class in the project to serve as the data source for the second list (Engineering Team) in the App.xaml.cs file. The object is called **SecondaryDataProvider** in the following code.</span></span>
  
    
    



```cs

private static ListDataProvider m_SecondaryDataProvider;

public static ListDataProvider SecondaryDataProvider
{
    get
    {
        if (m_SecondaryDataProvider != null)
            return m_SecondaryDataProvider;

        m_SecondaryDataProvider = new ListDataProvider();
        m_SecondaryDataProvider.ListTitle = "Engineering Team";
        m_SecondaryDataProvider.SiteUrl = new Uri("http://contoso:2012/sites/samplesite/");

        return m_SecondaryDataProvider;
    }
}
```

<span data-ttu-id="93b21-120">Затем можно создайте другой объекта класса **ListViewModel** (с именем, например, **SecondaryViewModel**) и назначить его свойство **DataProvider**, как в следующем коде объект **SecondaryDataProvider**.</span><span class="sxs-lookup"><span data-stu-id="93b21-120">Then you can instantiate another object of the **ListViewModel** class (named, for instance, **SecondaryViewModel**) and assign the **SecondaryDataProvider** object to its **DataProvider** property, as in the following code.</span></span>
  
    
    



```cs

private static ListViewModel m_SecondaryViewModel;

public static ListViewModel SecondaryViewModel
{
    get
    {
        if (m_SecondaryViewModel == null)
            m_SecondaryViewModel = new ListViewModel { DataProvider = App.SecondaryDataProvider };

        return m_SecondaryViewModel;
    }
    set
    {
        m_SecondaryViewModel = value;
    }
}
```

<span data-ttu-id="93b21-121">Если же полей и представлений для двух списков применимость для ваших целей (и, снова, если приведены два иметь одинаковые столбцы и поля), внесите изменения в реализации класс **ListDataProvider** (в файле ListDataProvider.cs) не требуется.</span><span class="sxs-lookup"><span data-stu-id="93b21-121">If the same fields and views for the two lists are suitable for your purposes (and, again, if the two lists have the same columns and fields), you don't need to make any changes in the implementation of the **ListDataProvider** class (in the ListDataProvider.cs file).</span></span>
  
    
    
<span data-ttu-id="93b21-p105">Для просмотра или изменения данных во втором в вашем проекте, необходимо добавить представление формы в проект, который привязан к и настроен для этой **SecondaryViewModel**. К примеру вы добавьте папку с именем «SecondaryViews» проект и добавьте файл SecondaryList.xaml в этой папке разметку следующий файл List.xaml по умолчанию, созданной с помощью шаблона для основного списка в проекте. Обратите внимание на то, следует различать дополнительного формы списка из основной формы списка в приложении, указав отличительные значение для атрибута **x:Class** элемента **PhoneApplicationPage** в файле SecondaryList.xaml.</span><span class="sxs-lookup"><span data-stu-id="93b21-p105">To display or modify the data from the second list in your project, however, you need to add view forms to your project that are bound to and configured for this **SecondaryViewModel**. For example, you could add a folder to your project named "SecondaryViews" and add a SecondaryList.xaml file to that folder with markup similar to that of the default List.xaml file generated by the template for the primary list in the project. Note that you should distinguish your secondary List form from the primary List form in the app by specifying a distinguishing value for the **x:Class** attribute of the **PhoneApplicationPage** element in the SecondaryList.xaml file.</span></span>
  
    
    



```

<phone:PhoneApplicationPage
    x:Class="MultipleSPListApp.SecondaryViews.ListForm"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:phone="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone"
    xmlns:shell="clr-namespace:Microsoft.Phone.Shell;assembly=Microsoft.Phone"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d" d:DesignWidth="480" d:DesignHeight="696"
    FontFamily="{StaticResource PhoneFontFamilyNormal}"
    FontSize="{StaticResource PhoneFontSizeNormal}"
    Foreground="{StaticResource PhoneForegroundBrush}"
    SupportedOrientations="PortraitOrLandscape" Orientation="Portrait"
    shell:SystemTray.IsVisible="True" x:Name = "ListViewPage">
...
</phone:PhoneApplicationPage>
```

<span data-ttu-id="93b21-p106">В файле выделенным кодом SecondaryList.xaml.cs, замените все ссылки на "App.MainViewModel" со ссылками на «App.SecondaryViewModel». Например конструктор в файле должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p106">In the associated code-behind file, SecondaryList.xaml.cs, replace all references to "App.MainViewModel" with references to "App.SecondaryViewModel". For example, the constructor in the file should be as follows.</span></span>
  
    
    



```cs

public ListForm()
    {
        InitializeComponent();
        this.DataContext = App.SecondaryViewModel;
    }
```

<span data-ttu-id="93b21-p107">Также заменить все ссылки в файл фонового кода «App.DataProvider» со ссылками на «App.SecondaryDataProvider» и обновить любые пути навигации для указания на соответствующие дополнительные страницы XAML. При добавлении дополнительных новая форма для проекта (с именем, например, SecondaryNewForm.xaml в папке SecondaryViews проекта), обработчика в файле SecondaryList.xaml.cs для события **OnNewButtonClick** будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="93b21-p107">Also replace all references in the code-behind file to "App.DataProvider" with references to "App.SecondaryDataProvider" and update any navigation paths to point to the appropriate secondary XAML pages. If you also add a secondary New form to your project (named, for example, SecondaryNewForm.xaml in the SecondaryViews folder of your project), the handler in the SecondaryList.xaml.cs file for the **OnNewButtonClick** event would resemble the following code.</span></span>
  
    
    



```cs

private void OnNewButtonClick(object sender, EventArgs e)
    {
        // Instantiate a new instance of NewItemViewModel and go to NewForm.
        App.SecondaryViewModel.CreateItemViewModelInstance = new NewItemViewModel { DataProvider = App.SecondaryDataProvider };
        NavigationService.Navigate(new Uri("/SecondaryViews/SecondaryNewForm.xaml", UriKind.Relative));
    }
```

<span data-ttu-id="93b21-129">И, наконец можно добавить кнопку для **ApplicationBar** в файле List.xaml для отображения страницы SecondaryList.xaml.</span><span class="sxs-lookup"><span data-stu-id="93b21-129">Finally, you can add a button to the **ApplicationBar** in the List.xaml file to display the SecondaryList.xaml page.</span></span>
  
    
    



```

...
    <phone:PhoneApplicationPage.ApplicationBar>
        <shell:ApplicationBar IsVisible="True" IsMenuEnabled="True">
            <shell:ApplicationBarIconButton x:Name="btnNew" IconUri="/Images/appbar.new.rest.png" Text="New" Click="OnNewButtonClick"/>
            <shell:ApplicationBarIconButton x:Name="btnRefresh" IconUri="/Images/appbar.refresh.rest.png" Text="Refresh" IsEnabled="True" Click="OnRefreshButtonClick"/>
            <!--Add the following button to navigate to the secondary list (Engineering Team).-->
            <shell:ApplicationBarIconButton x:Name="btnSecondaryList" IconUri="/Images/appbar.upload.rest.png" Text="Engineering" IsEnabled="True" Click="OnSecondaryListButtonClick"/>
        </shell:ApplicationBar>
    </phone:PhoneApplicationPage.ApplicationBar>
...
```

<span data-ttu-id="93b21-130">В файле выделенным кодом List.xaml.cs, добавьте обработчик для события **OnSecondaryListButtonClick**, указанной в файле List.xaml.</span><span class="sxs-lookup"><span data-stu-id="93b21-130">In the associated code-behind file, List.xaml.cs, add a handler for the **OnSecondaryListButtonClick** event declared in the List.xaml file.</span></span>
  
    
    



```cs

private void OnSecondaryListButtonClick(object sender, EventArgs e)
{
    NavigationService.Navigate(new Uri("/SecondaryViews/SecondaryList.xaml", UriKind.Relative));
}
```

<span data-ttu-id="93b21-p108">Пользователи вашего приложения могут перейти от команды разработчиков и списка группа маркетинга. Так как основной схемы списков совпадают, по умолчанию **DataProvider** и **MainViewModel** объекты созданный шаблон, а также добавлена обрабатывать объекты **SecondaryDataProvider** и **SecondaryViewModel** всех транзакций данных без необходимости каких-либо изменений в файл ListDataProvider.cs.</span><span class="sxs-lookup"><span data-stu-id="93b21-p108">Users of your app can then navigate between the Marketing Team list and the Engineering Team list. Because the underlying list schemas are the same, the default **DataProvider** and **MainViewModel** objects generated by the template and the added **SecondaryDataProvider** and **SecondaryViewModel** objects handle all the data transactions without requiring any modifications to the ListDataProvider.cs file.</span></span>
  
    
    

## <a name="create-a-solution-involving-sharepoint-lists-based-on-different-schemas"></a><span data-ttu-id="93b21-133">Создание решения, включающие использование списков SharePoint на основе различных схем</span><span class="sxs-lookup"><span data-stu-id="93b21-133">Create a solution involving SharePoint lists based on different schemas</span></span>
<span data-ttu-id="93b21-134"><a name="BKMK_DifferentSchemasProject"> </a></span><span class="sxs-lookup"><span data-stu-id="93b21-134"></span></span>

<span data-ttu-id="93b21-135">Подход в предыдущем разделе works до его переход (которые, для списков SharePoint на основе одинаковую схему), но класс **ListDataProvider** в шаблон доступен для разработчиков для настройки для обработки нескольких списков SharePoint, которые не могут быть основаны на той же схеме или не включать же столбцов и полей приложения списка SharePoint Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="93b21-135">The approach in the preceding section works as far as it goes (that is, for SharePoint lists based on the same schema) but the **ListDataProvider** class in the Windows Phone SharePoint List Application template is available to developers for customization to handle multiple SharePoint lists that may not be based on the same schema or may not include the same columns and fields.</span></span>
  
    
    
<span data-ttu-id="93b21-p109">Предположим, что, как и в предыдущем разделе, наличие списка SharePoint, группа маркетинга (на основе шаблона списка контактов), содержащий члены группы маркетинга. Имеется также второй список, с именем заказы (на основе настраиваемого списка шаблона), содержащий столбцы и типы полей, показано в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="93b21-p109">Suppose, as in the preceding section, that you have a SharePoint list, Marketing Team (based on the Contacts list template), containing members of a marketing team. Suppose also that you have a second list, named Orders (based on the Custom list template), containing the columns and field types shown in Table 1.</span></span>
  
    
    

<span data-ttu-id="93b21-138">**В таблице 1. Столбцов и полей для списка заказов**</span><span class="sxs-lookup"><span data-stu-id="93b21-138">**Table 1. Columns and fields for Orders list**</span></span>


|<span data-ttu-id="93b21-139">**Столбец**</span><span class="sxs-lookup"><span data-stu-id="93b21-139">**Column**</span></span>|<span data-ttu-id="93b21-140">**Тип поля**</span><span class="sxs-lookup"><span data-stu-id="93b21-140">**Field Type**</span></span>|<span data-ttu-id="93b21-141">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="93b21-141">**Required**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="93b21-142">Продукт (например, заголовок)</span><span class="sxs-lookup"><span data-stu-id="93b21-142">Product (i.e., Title)</span></span>  <br/> |<span data-ttu-id="93b21-143">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="93b21-143">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="93b21-144">Да</span><span class="sxs-lookup"><span data-stu-id="93b21-144">Yes</span></span>  <br/> |
|<span data-ttu-id="93b21-145">Цена</span><span class="sxs-lookup"><span data-stu-id="93b21-145">Unit Price</span></span>  <br/> |<span data-ttu-id="93b21-146">Денежный</span><span class="sxs-lookup"><span data-stu-id="93b21-146">Currency</span></span>  <br/> |<span data-ttu-id="93b21-147">Да</span><span class="sxs-lookup"><span data-stu-id="93b21-147">Yes</span></span>  <br/> |
|<span data-ttu-id="93b21-148">Количество</span><span class="sxs-lookup"><span data-stu-id="93b21-148">Quantity</span></span>  <br/> |<span data-ttu-id="93b21-149">Number (числовое значение);</span><span class="sxs-lookup"><span data-stu-id="93b21-149">Number</span></span>  <br/> |<span data-ttu-id="93b21-150">Нет (по умолчанию присваивается значение 0)</span><span class="sxs-lookup"><span data-stu-id="93b21-150">No (defaults to zero)</span></span>  <br/> |
|<span data-ttu-id="93b21-151">Значение заказа</span><span class="sxs-lookup"><span data-stu-id="93b21-151">Order Value</span></span>  <br/> |<span data-ttu-id="93b21-152">Вычисляется (цена * количество)</span><span class="sxs-lookup"><span data-stu-id="93b21-152">Calculated (Unit Price * Quantity)</span></span>  <br/> |<span data-ttu-id="93b21-153">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-153">No</span></span>  <br/> |
|<span data-ttu-id="93b21-154">Дата заказа</span><span class="sxs-lookup"><span data-stu-id="93b21-154">Order Date</span></span>  <br/> |<span data-ttu-id="93b21-155">Дата и время (Datetime)</span><span class="sxs-lookup"><span data-stu-id="93b21-155">Date and Time (Datetime)</span></span>  <br/> |<span data-ttu-id="93b21-156">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-156">No</span></span>  <br/> |
|<span data-ttu-id="93b21-157">Статус заказа</span><span class="sxs-lookup"><span data-stu-id="93b21-157">Order Status</span></span>  <br/> |<span data-ttu-id="93b21-158">Варианты</span><span class="sxs-lookup"><span data-stu-id="93b21-158">Choice</span></span>  <br/> |<span data-ttu-id="93b21-159">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-159">No</span></span>  <br/> |
|<span data-ttu-id="93b21-160">Клиент</span><span class="sxs-lookup"><span data-stu-id="93b21-160">Customer</span></span>  <br/> |<span data-ttu-id="93b21-161">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="93b21-161">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="93b21-162">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-162">No</span></span>  <br/> |
   
<span data-ttu-id="93b21-p110">Как показано в примере в предыдущем разделе можно создать экземпляр объекта отдельные **ListDataProvider** и другой объект **ListViewModel** для управления списка заказов. Предполагается, что объект инициализированный **ListDataProvider** с именем **OrdersListDataProvider**, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="93b21-p110">As in the example in the preceding section, you can instantiate a separate **ListDataProvider** object and another **ListViewModel** object to manage the Orders list. Assume that the instantiated **ListDataProvider** object is named **OrdersListDataProvider**, as in the following code.</span></span>
  
    
    



```cs

private static ListDataProvider m_OrdersListDataProvider;

public static ListDataProvider OrdersListDataProvider
{
    get
    {
        if (m_OrdersListDataProvider != null)
            return m_OrdersListDataProvider;

        m_OrdersListDataProvider = new ListDataProvider();
        m_OrdersListDataProvider.ListTitle = "Orders";
        m_OrdersListDataProvider.SiteUrl = new Uri("http://contoso:2012/sites/samplesite/"); // Specify a URL here for your server.

        return m_OrdersListDataProvider;
    }
}
```

<span data-ttu-id="93b21-165">Предполагается, что объект инициализированный **ListViewModel** для списка заказов с именем **OrdersListViewModel**, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="93b21-165">And assume that the instantiated **ListViewModel** object for the Orders list is named **OrdersListViewModel**, as in the following code.</span></span>
  
    
    



```cs

private static ListViewModel m_OrdersListViewModel;

public static ListViewModel OrdersListViewModel
{
    get
    {
        if (m_OrdersListViewModel == null)
            m_OrdersListViewModel = new ListViewModel { DataProvider = App.OrdersListDataProvider };

        return m_OrdersListViewModel;
    }
    set
    {
        m_OrdersListViewModel = value;
    }
}
```

<span data-ttu-id="93b21-p111">Схемы для списка заказов отличается от списка, группа маркетинга. Позволяет разместить различия, добавив код в файле ListDataProvider.cs специально для класса **CamlQueryBuilder**.</span><span class="sxs-lookup"><span data-stu-id="93b21-p111">The schema for the Orders list differs from that of the Marketing Team list. You can accommodate the differences by adding code to the ListDataProvider.cs file, specifically to the **CamlQueryBuilder** class.</span></span>
  
    
    



```cs

public static class CamlQueryBuilder
{
    static Dictionary<string, string> ViewXmls = new Dictionary<string, string>()
    {   
        {"View1",   @"<View><Query><OrderBy><FieldRef Name='Title' />
                    <FieldRef Name='FirstName'  /></OrderBy></Query><RowLimit>30</RowLimit><ViewFields>{0}</ViewFields></View>"},
      {"View2",   @"<View><Query><OrderBy><FieldRef Name='ID' /></OrderBy></Query><RowLimit>30</RowLimit>
     <ViewFields>{0}</ViewFields></View>"}
    };

    static string View1Fields = @"<FieldRef Name='Title'/><FieldRef Name='FirstName'/>
   <FieldRef Name='JobTitle'/><FieldRef Name='Email'/><FieldRef Name='Comments'/>";
    static string View2Fields = @"<FieldRef Name='Title'/><FieldRef Name='Unit_x0020_Price'/><FieldRef Name='Quantity'/>
            <FieldRef Name='Order_x0020_Value'/><FieldRef Name='Order_x0020_Date'/>
            <FieldRef Name='Status'/><FieldRef Name='Customer'/>";

    public static CamlQuery GetCamlQuery(string viewName)
    {
        string viewXml = ViewXmls[viewName];
        // Add ViewFields to the ViewXml depending on the view.
        switch (viewName)
        {
            case "View2":
                viewXml = string.Format(viewXml, View2Fields);
                break;
            case "View1":
            default:
                viewXml = string.Format(viewXml, View1Fields);
                break;
        }
        return new CamlQuery { ViewXml = viewXml };
    }
}
```

<span data-ttu-id="93b21-p112">Здесь вторую запись со значением ключа «View2» добавляется к объекту **Dictionary** **ViewXmls**для списка заказов. (Имейте в виду, что ключ значений для записи, добавляемые **ViewXmls** **Dictionary** в классе **CamlQueryBuilder** должны быть уникальными (в решении) для кэширования логика в шаблоне для правильной работы.) Переменные String ( **View1Fields** и **View2Fields**) используются для хранения список полей для каждого представления. Затем в зависимости от значения параметра **viewName**, переданной в метод **GetCamlQuery**, создается соответствующий запрос CAML XML-строка.</span><span class="sxs-lookup"><span data-stu-id="93b21-p112">Here, a second entry with a key value of "View2" is added to the **ViewXmls** **Dictionary** object for the Orders list. (Keep in mind that the key values for entries added to the **ViewXmls** **Dictionary** in the **CamlQueryBuilder** class must be unique (in the solution) for the caching logic in the template to operate properly.) String variables ( **View1Fields** and **View2Fields**) are used to store the list of fields for each view. Then, depending on the value of the **viewName** parameter passed to the **GetCamlQuery** method, the appropriate CAML query XML string is created.</span></span>
  
    
    
<span data-ttu-id="93b21-p113">Затем как и в предыдущем разделе, можно создавать формы представления для списка, привязанных к **OrdersListViewModel** и **OrdersListDataProvider** объекты этого времени. Например, XAML для формы списка, определенного в список заказов с именем OrdersList.xaml, аналогичную разметку в файле List.xaml создаются с помощью шаблона для основного списка в приложении, за исключением того, что будет имя элемента управления **PivotItem**, который отображает список "View2" (а не по умолчанию "Представление1") и задайте объявление **Binding** в атрибуте **ItemsSource** элемента управления **ListBox**, в котором элементы списка отображаются в "View2" как в следующем примере Разметка (где отображаются только разметка для сетки корневой страницы).</span><span class="sxs-lookup"><span data-stu-id="93b21-p113">Then, as in the preceding section, you can create view forms for the list, bound this time to the **OrdersListViewModel** and **OrdersListDataProvider** objects. As an example, the XAML for a List form specific to the Orders list, named OrdersList.xaml, would be similar to the markup in the List.xaml file generated by the template for the primary list in the app, except that you would name the **PivotItem** control that renders the list "View2" (rather than the default, "View1") and set the **Binding** declaration for the **ItemsSource** attribute of the **ListBox** control in which list items are rendered to "View2" as in the following markup (which shows only the markup for the root grid of the page).</span></span>
  
    
    



```

...
    <Grid x:Name="LayoutRoot" Background="Transparent" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:controls="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone.Controls">
        <!--Pivot Control-->
        <ProgressBar x:Name="progressBar" Opacity="1" HorizontalAlignment="Center" VerticalAlignment="Top" 
               Height="30" Width="470" IsIndeterminate="{Binding IsBusy}" Visibility="{Binding ShowIfBusy}" />
        <Grid x:Name="ContentPanel" Grid.Row="0" Width="470">
            <controls:Pivot Name="Views" Title="Orders" LoadedPivotItem="OnPivotItemLoaded">
                <!--Pivot item-->
                <controls:PivotItem Name="View2" Header="All Orders">
                    <!--Double line list with text wrapping-->
                    <ListBox x:Name="lstBox1" Margin="0,0,-12,0" SelectionChanged="OnSelectionChanged" ItemsSource="{Binding [View2]}">
                        <ListBox.ItemTemplate>
                            <DataTemplate>
                                <StackPanel Orientation="Vertical" Margin="10">
                                    <TextBlock Name="txtTitle" Text="{Binding [Title]}" TextWrapping="NoWrap" 
                                          Style="{StaticResource PhoneTextTitle2Style}" />
                                    <TextBlock Name="txtUnitPrice" Text="{Binding [Unit_x0020_Price]}" 
                                         TextWrapping="NoWrap" Style="{StaticResource PhoneTextNormalStyle}" />
                                    <TextBlock Name="txtQuantity" Text="{Binding [Quantity]}"
                                         TextWrapping="NoWrap" Style="{StaticResource PhoneTextNormalStyle}" />
                                </StackPanel>
                            </DataTemplate>
                        </ListBox.ItemTemplate>
                    </ListBox>
                </controls:PivotItem>
            </controls:Pivot>
        </Grid>
    </Grid>
...
```

<span data-ttu-id="93b21-p114"> Это удобный способ создания подходящего разметки XAML для использования шаблона приложения списка SharePoint для Windows Phone для создания отдельного проекта на основе списка заказов и затем скопируйте созданный код XAML из этого проекта в проект с помощью нескольких списков, с учетом изменить имя элемента управления **PivotItem** (значение по умолчанию "Представление1") на "View2" и измените объявление **Binding** элемента управления **ListBox**, как показано ниже. Необходимо также изменить все ссылки в файле выделенным кодом для формы для указания соответствующих объектов **ListViewModel** и **DataProvider** (как, например, **OrdersListViewModel** и **OrdersListDataProvider**).</span><span class="sxs-lookup"><span data-stu-id="93b21-p114">A convenient way to create suitable XAML markup is to use the Windows Phone SharePoint List Application template to generate a separate project based on the Orders list and then copy the generated XAML from that project to the project with multiple lists, taking care to change the name of the **PivotItem** control (which defaults to "View1") to "View2" and to change the **Binding** declaration of the **ListBox** control as shown here. You would also need to change all references in the associated code-behind file for the form to specify the appropriate **ListViewModel** and **DataProvider** objects (as, for example, **OrdersListViewModel** and **OrdersListDataProvider**).</span></span>
  
    
    
<span data-ttu-id="93b21-p115">Такой подход работает, так как в файле выделенным кодом (с именем, в данном случае OrdersList.xaml.cs), управлять различных обработчиков событий, которые могут вызывать методы объекта **ListDataProvider** (в данном случае  **OrdersListDataProvider**) для доступа к списка используйте имя **PivotItem**, чтобы указать соответствующие представления для использования. Например, для обработчика событий **OnPivotItemLoaded** вызывает метод **LoadData** **OrdersListViewModel** объект, созданный из класса **ListViewModel** (и в свою очередь, этот метод вызывает метод **LoadData** объекта **OrdersListDataProvider** ), передающая свое имя элемента управления **PivotItem** (здесь "View2") в качестве значения параметра **ViewName** методу. В конечном счете это же значение передается (в качестве значения параметра **viewName** ) в метод **GetCamlQuery** показано выше в измененные реализация класса **CamlQueryBuilder**.</span><span class="sxs-lookup"><span data-stu-id="93b21-p115">This approach works because in the associated code-behind file (named, in this case, OrdersList.xaml.cs), the various event handlers that call methods of the **ListDataProvider** object (here, **OrdersListDataProvider**) to access list data use the name of the **PivotItem** control as a way to specify the appropriate view to use. For example, the **OnPivotItemLoaded** event handler calls the **LoadData** method of the **OrdersListViewModel** object instantiated from the **ListViewModel** class (and this method in turn calls the **LoadData** method of the **OrdersListDataProvider** object), passing the name of the **PivotItem** control (here, "View2") as the value of the **ViewName** parameter to the method. This same value is ultimately passed (as the value of the **viewName** parameter) to the **GetCamlQuery** method shown above in the modified implementation of the **CamlQueryBuilder** class.</span></span>
  
    
    

## <a name="an-alternative-approach-for-a-solution-involving-sharepoint-lists-based-on-different-schemas"></a><span data-ttu-id="93b21-178">Альтернативный подход для решения, включающие использование списков SharePoint на основе различных схем</span><span class="sxs-lookup"><span data-stu-id="93b21-178">An alternative approach for a solution involving SharePoint lists based on different schemas</span></span>
<span data-ttu-id="93b21-179"><a name="BKMK_DifferentSchemasAlternative"> </a></span><span class="sxs-lookup"><span data-stu-id="93b21-179"></span></span>

<span data-ttu-id="93b21-p116">В качестве альтернативы подхода в предыдущем разделе можно использовать шаблон приложения списка SharePoint для Windows Phone для создания Windows Phone проекта приложения в Microsoft Visual Studio 2010 решения на основе заданного списка SharePoint, а затем добавьте проекты построена на основе других списков для этого же решения. Такой подход позволяет воспользоваться преимуществами шаблон для создания форм для каждого списка SharePoint. Затем можно настроить решение по мере необходимости для управления взаимодействия пользователей с помощью списков. В этом разделе описано этого подхода.</span><span class="sxs-lookup"><span data-stu-id="93b21-p116">As an alternative to the approach in the preceding section, you can use the Windows Phone SharePoint List Application template to create a Windows Phone app project in a Microsoft Visual Studio 2010 solution based on a given SharePoint list and then add projects built based on other lists to that same solution. This approach allows you to take advantage of the template for generating forms specific to each SharePoint list. You can then customize the solution according to your needs to control how users interact with the lists. The procedures in this section demonstrate that approach.</span></span>
  
    
    
<span data-ttu-id="93b21-p117">Для выполнения следующих процедур предполагается наличие списка SharePoint с именем Orders (на основе настраиваемого списка шаблона), с помощью столбцов и типов полей, как показано в таблице 1 в предыдущем разделе. Кроме того, предположим, у вас есть другой список SharePoint (еще раз, на основе шаблона списка Custom), с именем клиентов, и столбцов и типов полей, приведенных в таблице 2.</span><span class="sxs-lookup"><span data-stu-id="93b21-p117">Assume for the following procedures that you have a SharePoint list named Orders (based on the Custom list template), with the columns and field types as shown in Table 1 in the preceding section. In addition, assume you have another SharePoint list (again, based on the Custom list template), named Customers, with the columns and field types shown in Table 2.</span></span>
  
    
    

<span data-ttu-id="93b21-186">**В таблице 2. Столбцов и полей для списка клиентов**</span><span class="sxs-lookup"><span data-stu-id="93b21-186">**Table 2. Columns and fields for Customers list**</span></span>


|<span data-ttu-id="93b21-187">**Столбец**</span><span class="sxs-lookup"><span data-stu-id="93b21-187">**Column**</span></span>|<span data-ttu-id="93b21-188">**Тип поля**</span><span class="sxs-lookup"><span data-stu-id="93b21-188">**Field Type**</span></span>|<span data-ttu-id="93b21-189">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="93b21-189">**Required**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="93b21-190">Имя пользователя (например, заголовок)</span><span class="sxs-lookup"><span data-stu-id="93b21-190">Customer Name (i.e., Title)</span></span>  <br/> |<span data-ttu-id="93b21-191">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="93b21-191">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="93b21-192">Да</span><span class="sxs-lookup"><span data-stu-id="93b21-192">Yes</span></span>  <br/> |
|<span data-ttu-id="93b21-193">Номер контакта</span><span class="sxs-lookup"><span data-stu-id="93b21-193">Contact Number</span></span>  <br/> |<span data-ttu-id="93b21-194">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="93b21-194">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="93b21-195">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-195">No</span></span>  <br/> |
|<span data-ttu-id="93b21-196">Адрес электронной почты</span><span class="sxs-lookup"><span data-stu-id="93b21-196">E-mail Address</span></span>  <br/> |<span data-ttu-id="93b21-197">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="93b21-197">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="93b21-198">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-198">No</span></span>  <br/> |
|<span data-ttu-id="93b21-199">Компания</span><span class="sxs-lookup"><span data-stu-id="93b21-199">Company</span></span>  <br/> |<span data-ttu-id="93b21-200">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="93b21-200">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="93b21-201">Нет</span><span class="sxs-lookup"><span data-stu-id="93b21-201">No</span></span>  <br/> |
   
<span data-ttu-id="93b21-p118">В следующих процедурах Создание приложения Windows Phone, которое использует оба эти списки. Основной список в приложение, список клиентов. При просмотре сведений для данного клиента в форме отображения кнопки включен на форме, которая позволяет пользователям отображать все заказы (из списка заказов) относящиеся к этому клиенту.</span><span class="sxs-lookup"><span data-stu-id="93b21-p118">In the following procedures, you create a Windows Phone app that uses both of these lists. The primary list in the app is the Customers list. When you display the details for a given customer in the Display form, a button is included on the form that allows users to display all the orders (from the Orders list) associated with that customer.</span></span>
  
    
    

### <a name="to-create-the-component-projects-for-the-solution"></a><span data-ttu-id="93b21-205">Для создания проектов компонент для решения</span><span class="sxs-lookup"><span data-stu-id="93b21-205">To create the component projects for the solution</span></span>


1. <span data-ttu-id="93b21-206">Создание приложения Windows Phone с использованием шаблона приложения списка SharePoint для Windows Phone, указание список SharePoint, заданных на основе столбцов и типов полей, приведенных в таблице 2.</span><span class="sxs-lookup"><span data-stu-id="93b21-206">Create a Windows Phone app by using the Windows Phone SharePoint List Application template, specifying a SharePoint list defined based on the columns and field types shown in Table 2.</span></span> <span data-ttu-id="93b21-207">В процедур, описанных в этом разделе предполагается, что имя списка в проекте является «Клиенты» и «CustomersSPListApp» — это имя проекта.</span><span class="sxs-lookup"><span data-stu-id="93b21-207">In the procedures in this section, it is assumed that the name of the list in the project is "Customers" and the name of the project is "CustomersSPListApp".</span></span> <span data-ttu-id="93b21-208">(Увидеть [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md) сведения о создании приложения на основе шаблона приложения списка SharePoint для Windows Phone.. MD)</span><span class="sxs-lookup"><span data-stu-id="93b21-208">(See  [How to: Create a Windows Phone SharePoint list app](how-to-create-a-windows-phone-sharepoint-list-app.md) for information about creating an app based on the Windows Phone SharePoint List Application template..md)</span></span>
    
  
2. <span data-ttu-id="93b21-209">Выберите **файл**, **Добавить** **Новый проект** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93b21-209">In Visual Studio, choose **File**, **Add**, **New Project**.</span></span> 
    
    <span data-ttu-id="93b21-210">Откроется диалоговое окно **Добавление нового проекта**.</span><span class="sxs-lookup"><span data-stu-id="93b21-210">The **Add New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="93b21-211">В диалоговом окне **Добавить новый проект** разверните узел **Visual C#** и выберите узел **Silverlight для Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="93b21-211">In the **Add New Project** dialog box, under the **Visual C#** node, choose the **Silverlight for Windows Phone** node.</span></span>
    
  
4. <span data-ttu-id="93b21-212">В области **Шаблоны** выберите шаблон приложения списка SharePoint для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="93b21-212">In the **Templates** pane, choose the Windows Phone SharePoint List Application template.</span></span>
    
  
5. <span data-ttu-id="93b21-213">Имя приложения, например, OrdersSPListAppи нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="93b21-213">Name the app, for example, OrdersSPListApp, and then choose **OK**.</span></span>
    
  
6. <span data-ttu-id="93b21-214">Выполните процедуру, описанную в [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md) для создания другого проекта приложения Windows Phone, определяющее список SharePoint, заданных на основе столбцов и Показать типов полей в таблице 1 как целевого списка для проекта.</span><span class="sxs-lookup"><span data-stu-id="93b21-214">Follow the procedure described in  [How to: Create a Windows Phone SharePoint list app](how-to-create-a-windows-phone-sharepoint-list-app.md) to create another Windows Phone app project, specifying a SharePoint list defined based on the columns and field types show in Table 1 as the target list for the project.</span></span> <span data-ttu-id="93b21-215">Теперь вы должны два проекта в решении с именем «CustomersSPListApp» и «OrdersSPListApp» (при использовании соглашения о наименовании в этой процедуре).</span><span class="sxs-lookup"><span data-stu-id="93b21-215">You should now have two projects in your solution, named "CustomersSPListApp" and "OrdersSPListApp" (if you are following the naming conventions in this procedure).</span></span>
    
  
7. <span data-ttu-id="93b21-216">В **Обозревателе решений** выберите узел проекта CustomerSPListApp.</span><span class="sxs-lookup"><span data-stu-id="93b21-216">In **Solution Explorer**, choose the CustomerSPListApp project node.</span></span>
    
  
8. <span data-ttu-id="93b21-217">В меню **проект** выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="93b21-217">On the **Project** menu, choose **Add Reference**.</span></span> 
    
    <span data-ttu-id="93b21-218">Откроется диалоговое окно **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="93b21-218">The **Add Reference** dialog box appears.</span></span>
    
  
9. <span data-ttu-id="93b21-p121">На вкладке **проекты** выберите проект OrdersSPListApp в решение и затем нажмите кнопку **ОК**. Проект будет добавлен в узле **ссылки** проекта CustomersSPListApp.</span><span class="sxs-lookup"><span data-stu-id="93b21-p121">On the **Projects** tab, choose the OrdersSPListApp project in the solution, and then choose the **OK** button. The project is added under the **References** node of the CustomersSPListApp project.</span></span>
    
  
<span data-ttu-id="93b21-p122">Далее настройте два проекта в решение. По сути настройки проекта OrdersSPListApp (основан на список заказов) для работы в качестве «поиск» проекта для проекта CustomerSPListApp (основан на список клиентов).</span><span class="sxs-lookup"><span data-stu-id="93b21-p122">Next, configure the two projects in the solution. You essentially configure the OrdersSPListApp project (based on the Orders list) to operate as a "look-up" project for the CustomerSPListApp project (based on the Customers List).</span></span>
  
    
    

### <a name="to-configure-the-orderssplistapp-project"></a><span data-ttu-id="93b21-223">Настройка проекта OrdersSPListApp</span><span class="sxs-lookup"><span data-stu-id="93b21-223">To configure the OrdersSPListApp project</span></span>


1. <span data-ttu-id="93b21-p123">Изменение пути перехода в формах представление проекта OrdersSPListApp для включения основного пространства имен проекта ("OrdersSPListApp") и обозначение «компонент». В обработчике для события OnNewButtonClick в файле List.xaml.cs OrdersSPListApp проекта, измените, например, вызов метода навигатор объекта NavigationService из этого:</span><span class="sxs-lookup"><span data-stu-id="93b21-p123">Change the navigation paths in the view forms of the OrdersSPListApp project to include the primary namespace of the project ("OrdersSPListApp") and the "component" designation. For example, in the handler for the OnNewButtonClick event in the List.xaml.cs file of the OrdersSPListApp project, change the call to the Navigate method of the NavigationService object from this:</span></span>
    
     `NavigationService.Navigate(new Uri("/Views/NewForm.xaml", UriKind.Relative));`
    
    <span data-ttu-id="93b21-226">на строку следующего вида:</span><span class="sxs-lookup"><span data-stu-id="93b21-226">To this:</span></span>
    
     `NavigationService.Navigate(new Uri("/OrdersSPListApp;component/Views/NewForm.xaml", UriKind.Relative));`
    
    <span data-ttu-id="93b21-227">Чтобы выполнить эти изменения проще всего использовать команду **Быстрая замена** в проекте OrdersSPListApp.</span><span class="sxs-lookup"><span data-stu-id="93b21-227">The easiest way to make these changes is to use the **Quick Replace** command in the OrdersSPListApp project.</span></span>
    
1. <span data-ttu-id="93b21-228">В **Обозревателе решений** выберите узел проекта OrdersSPListApp.</span><span class="sxs-lookup"><span data-stu-id="93b21-228">In **Solution Explorer**, choose the OrdersSPListApp project node.</span></span>
    
  
2. <span data-ttu-id="93b21-229">Клавиши Ctrl + H, чтобы отобразить диалоговое окно " **Быстрая замена** ".</span><span class="sxs-lookup"><span data-stu-id="93b21-229">Press Ctrl+H to display the **Quick Replace** dialog box.</span></span>
    
  
3. <span data-ttu-id="93b21-230">В текстовом поле **Найти** задайте следующий текст именно то, которое будет отображаться здесь:</span><span class="sxs-lookup"><span data-stu-id="93b21-230">In the **Find what** text box, specify the following text exactly as it is appears here:</span></span>
    
    <span data-ttu-id="93b21-231">URI ("/Views/</span><span class="sxs-lookup"><span data-stu-id="93b21-231">Uri("/Views/</span></span>
    
  
4. <span data-ttu-id="93b21-232">В текстовом поле **Заменить** так, как оно указано здесь укажите следующий текст:</span><span class="sxs-lookup"><span data-stu-id="93b21-232">In the **Replace with** text box, specify the following text exactly as it appears here:</span></span>
    
    <span data-ttu-id="93b21-233">URI ("/ OrdersSPListApp; компонент/представлений /</span><span class="sxs-lookup"><span data-stu-id="93b21-233">Uri("/OrdersSPListApp;component/Views/</span></span>
    
  
5. <span data-ttu-id="93b21-234">Убедитесь, что выбран **Текущий проект**, в раскрывающемся списке **Искать в**.</span><span class="sxs-lookup"><span data-stu-id="93b21-234">Ensure that **Current Project** is selected in the **Look in** drop-down list.</span></span>
    
  
6. <span data-ttu-id="93b21-235">Нажмите кнопку **Заменить все**.</span><span class="sxs-lookup"><span data-stu-id="93b21-235">Choose **Replace All**.</span></span>
    
  
7. <span data-ttu-id="93b21-236">Сохраните все измененные файлы в проекте.</span><span class="sxs-lookup"><span data-stu-id="93b21-236">Save all changed files in the project.</span></span>
    
  
2. <span data-ttu-id="93b21-p124">Добавление свойства элемента в файл App.xaml.cs OrdersSPListApp проекта. В **Обозревателе решений** выберите узел проекта OrdersSPListApp и выберите файл App.xaml.</span><span class="sxs-lookup"><span data-stu-id="93b21-p124">Add a member property to the App.xaml.cs file of the OrdersSPListApp project. In **Solution Explorer**, under the OrdersSPListApp project node, choose the App.xaml file.</span></span>
    
  
3. <span data-ttu-id="93b21-239">КлавишиF7Чтобы открыть файл его выделенным кодом App.xaml.cs, для редактирования.</span><span class="sxs-lookup"><span data-stu-id="93b21-239">Press F7 to open its associated code-behind file, App.xaml.cs, for editing.</span></span>
    
  
4. <span data-ttu-id="93b21-240">В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **App** добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="93b21-240">Within the code block (demarcated by opening and closing braces) that implements the **App** partial class, add the following code.</span></span>
    
```cs
  
public static string CustomerName { get; set; }
```

5. <span data-ttu-id="93b21-241">В **Обозревателе решений** выберите узел проекта OrdersSPListApp и выберите файл List.xaml.</span><span class="sxs-lookup"><span data-stu-id="93b21-241">In **Solution Explorer**, under the OrdersSPListApp project node, choose the List.xaml file.</span></span>
    
  
6. <span data-ttu-id="93b21-242">КлавишиF7Чтобы открыть файл его выделенным кодом List.xaml.cs, для редактирования.</span><span class="sxs-lookup"><span data-stu-id="93b21-242">Press F7 to open its associated code-behind file, List.xaml.cs, for editing.</span></span>
    
  
7. <span data-ttu-id="93b21-p125">Измените обработчик событий **OnNavigatedTo** в файле для анализа **QueryString** свойства объекта **NavigationContext**, чтобы задать значение переменной **CustomerName**, указанному в шаге 4. Можно также установить свойство **Header** **PivotItem** элемента управления в форме списка в соответствии с именем customer, для удобства пользователей. Измененные обработчик должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p125">Modify the **OnNavigatedTo** event handler in the file to parse the **QueryString** property of the **NavigationContext** object to set the value of the **CustomerName** variable declared in step 4. You can also set the **Header** property of the **PivotItem** control on the List form to match the customer name, for the convenience of your users. The modified handler should be as follows.</span></span>
    
```cs
  protected override void OnNavigatedTo(System.Windows.Navigation.NavigationEventArgs e)
{
    base.OnNavigatedTo(e);

    if (this.NavigationContext.QueryString.ContainsKey("CustomerName"))
    {
        App.CustomerName = NavigationContext.QueryString["CustomerName"];
    }

    // Also set the value of the Header property for the PivotItem to match the customer name.
    if (!string.IsNullOrWhiteSpace(App.CustomerName))
    {
        this.View1.Header = App.CustomerName;
    }

    App.MainViewModel.ViewDataLoaded += new EventHandler<ViewDataLoadedEventArgs>(OnViewDataLoaded);
    App.MainViewModel.InitializationCompleted += new EventHandler<InitializationCompletedEventArgs>(OnViewModelInitialization);
}
```

8. <span data-ttu-id="93b21-p126">Добавьте в качестве аргумента в вызове метода **LoadData** в обработчике событий **OnPivotItemLoaded** в файле List.xaml.cs **CustomerName**. Реализация обработчика событий **OnPivotItemLoaded** должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p126">Add the **CustomerName** variable as an argument in the call to the **LoadData** method in the **OnPivotItemLoaded** event handler in the List.xaml.cs file. The implementation of the **OnPivotItemLoaded** event handler should be as follows.</span></span>
    
```cs
  
private void OnPivotItemLoaded(object sender, PivotItemEventArgs e)
{
    if (!App.MainViewModel.IsInitialized)
    {
        //Initialize ViewModel and Load Data for PivotItem upon initialization.
        App.MainViewModel.Initialize();
    }
    else
    {
        //Load Data for the currently loaded PivotItem.
        App.MainViewModel.LoadData(e.Item.Name, App.CustomerName);
    }
}
```


    The **LoadData** method of the **ListViewModel** class in the template is defined such as to be able to accept optional parameters.
    
  
9. <span data-ttu-id="93b21-p127">Также добавьте переменную **CustomerName** в качестве аргумента в вызове метода **LoadData** в обработчике событий **OnViewModelInitialization**. Реализация обработчика событий **OnViewModelInitialization** должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p127">Also add the **CustomerName** variable as an argument in the call to the **LoadData** method in the **OnViewModelInitialization** event handler. The implementation of the **OnViewModelInitialization** event handler should be as follows.</span></span>
    
```cs
  
private void OnViewModelInitialization(object sender, InitializationCompletedEventArgs e)
{
    this.Dispatcher.BeginInvoke(() =>
    {
        //If initialization has failed, show error message and return.
        if (e.Error != null)
        {
            MessageBox.Show(e.Error.Message, e.Error.GetType().Name, MessageBoxButton.OK);
            return;
        }
        App.MainViewModel.LoadData(((PivotItem)Views.SelectedItem).Name, App.CustomerName);
        this.DataContext = (sender as ListViewModel);
    });
}
```

10. <span data-ttu-id="93b21-p128">Добавьте в качестве аргумента в вызове метода **RefreshData** в обработчике событий **OnRefreshButtonClick** в файле List.xaml.cs **CustomerName**. Реализация обработчика событий **OnRefreshButtonClick** должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p128">Add the **CustomerName** variable as an argument in the call to the **RefreshData** method in the **OnRefreshButtonClick** event handler in the List.xaml.cs file. The implementation of the **OnRefreshButtonClick** event handler should be as follows.</span></span>
    
```cs
  
private void OnRefreshButtonClick(object sender, EventArgs e)
{
    if (Views.SelectedItem == null)
        return;

    if (!App.MainViewModel.IsInitialized)
    {
        //Initialize ViewModel and Load Data for PivotItem upon completion.
        App.MainViewModel.Initialize();
    }
    else
    {   //Refresh Data for the currently loaded PivotItem.
        App.MainViewModel.RefreshData(((PivotItem)Views.SelectedItem).Name, App.CustomerName);
    }
}
```


    As for the **LoadData** method, the **RefreshData** method is also defined to be able to accept optional parameters. Notice that in the preceding three steps, the only change to the event handlers as generated by the template is the addition of the **CustomerName** variable as an argument in the call to the **LoadData** or **RefreshData** methods.
    
  
11. <span data-ttu-id="93b21-p129">Когда пользователи нажмите кнопку **Создать** на формы списка для списка заказов в вашем приложении, поле клиента в форме создания уже должны содержать имя клиента, так как список заказов, отображаются для пользователя было отфильтровано, основанным на имя клиента. Новые заказы, добавленных из фильтрованного списка должен быть связан с именем customer, на котором список фильтруется. Чтобы передать значение переменной **CustomerName** новая форма, измените событие **OnNewButtonClick** для значение как строку запроса в путь перехода на новую форму, как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="93b21-p129">When users choose the **New** button on the List form for the Orders list in your app, the Customer field in the New form should already contain the name of the customer, because the list of orders displayed to the user has been filtered based on the customer name. New orders added from that filtered list should be associated with the customer name on which the list is filtered. To pass the value of the **CustomerName** variable to the New form, modify the **OnNewButtonClick** event to include the value as a query string in the navigation path to the New form, as shown in the following code.</span></span>
    
```cs
  
private void OnNewButtonClick(object sender, EventArgs e)
{
    //Instantiate a new instance of NewItemViewModel and go to NewForm.
    App.MainViewModel.CreateItemViewModelInstance = new NewItemViewModel { DataProvider = App.DataProvider };
    
    if (!string.IsNullOrWhiteSpace(App.CustomerName))
    {
        NavigationService.Navigate(new Uri("/OrdersSPListApp;component/Views/NewForm.xaml?CustomerName=" + 
                                                                            App.CustomerName, UriKind.Relative));
    }
    else
    {
        NavigationService.Navigate(new Uri("/OrdersSPListApp;component/Views/NewForm.xaml", UriKind.Relative));
    }
}
```

12. <span data-ttu-id="93b21-p130">В обработчике событий **OnNavigatedTo** новая форма Проверьте строки запроса с именем customer, если он доступен, его и назначьте поле Клиент ViewModel для формы. В **Обозревателе решений** выберите в разделе проект OrdersSPListApp, выберите файл NewForm.xaml и нажмите кнопкуF7Чтобы открыть файл его выделенным кодом NewForm.xaml.cs, для редактирования.</span><span class="sxs-lookup"><span data-stu-id="93b21-p130">In the **OnNavigatedTo** event handler for the New form, check the query string for a customer name and, if it's available, assign it to the Customer field of the ViewModel for the form. In **Solution Explorer**, under the OrdersSPListApp project, choose the NewForm.xaml file and press F7 to open its associated code-behind file, NewForm.xaml.cs, for editing.</span></span>
    
  
13. <span data-ttu-id="93b21-257">Измените обработчик событий **OnNavigatedTo** в файле в соответствии со следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="93b21-257">Modify the **OnNavigatedTo** event handler in the file to match the following code.</span></span>
    
```cs
  
protected override void OnNavigatedTo(System.Windows.Navigation.NavigationEventArgs e)
{
    base.OnNavigatedTo(e);

    if (this.NavigationContext.QueryString.ContainsKey("CustomerName"))
    {
        this.viewModel["Customer"] = NavigationContext.QueryString["CustomerName"];
    }

    viewModel.ItemCreated += new EventHandler<ItemCreatedEventArgs>(OnItemCreated);
}
```

14. <span data-ttu-id="93b21-p131">В классе **CamlQueryBuilder** в файле ListDataProvider.cs в проекте OrdersSPListApp добавьте предложение **WHERE** в поле клиента в CAML запрос, используемый для получения элементов из списка заказов для фильтрации списка на основе имени данного клиента (из переменной **CustomerName** ). Добавьте параметр **GetCamlQuery** методы в классе передачи имени клиента. Класс измененные **CamlQueryBuilder** должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p131">In the **CamlQueryBuilder** class in the ListDataProvider.cs file in the OrdersSPListApp project, add a **WHERE** clause to the Customer field in the CAML query used to get items from the Orders list to filter the list based on a given customer name (from the **CustomerName** variable). Add a parameter to the **GetCamlQuery** method in the class for passing the customer name. The modified **CamlQueryBuilder** class should be as follows.</span></span>
    
```cs
  
public static class CamlQueryBuilder
{
    static Dictionary<string, string> ViewXmls = new Dictionary<string, string>()
    {   
        {"View1", @"<View><Query>{0}</Query><RowLimit>30</RowLimit><ViewFields>{1}</ViewFields></View>"}
    };

    static string ViewFields = @"<FieldRef Name='Title'/><FieldRef Name='Unit_x0020_Price'/><FieldRef Name='Quantity'/><FieldRef Name='Order_x0020_Value'/><FieldRef Name='Order_x0020_Date'/><FieldRef Name='Status'/><FieldRef Name='Customer'/>";

    public static CamlQuery GetCamlQuery(string viewName, string customerName)
    {
        string queryClause = string.Empty;

        // Create appropriate Query Clause, depending on customerName parameter.
        if (string.IsNullOrWhiteSpace(customerName))
        {
            queryClause = "<OrderBy><FieldRef Name='ID' /></OrderBy>";
        }
        else
        {
            queryClause = string.Format("<Where><Eq><FieldRef Name='Customer' /><Value Type='Text'>{0}</Value></Eq></Where>", customerName);
        }

        // Add Query Clause and ViewFields to ViewXml.
        string viewXml = ViewXmls[viewName];
        viewXml = string.Format(viewXml, queryClause, ViewFields);

        return new CamlQuery { ViewXml = viewXml };
    }
}
```

15. <span data-ttu-id="93b21-p132">Измените метод **LoadDataFromServer** в файле ListDataProvider.cs для проверки в аргументе **CustomerName** и передачи аргумента в метод **GetCamlQuery**. Измененный метод должен иметь следующий вид.</span><span class="sxs-lookup"><span data-stu-id="93b21-p132">Modify the **LoadDataFromServer** method in the ListDataProvider.cs file to check for the **CustomerName** argument and pass the argument to the **GetCamlQuery** method. The modified method should be as follows.</span></span>
    
```cs
  
private void LoadDataFromServer(string ViewName, Action<LoadViewCompletedEventArgs>
                                              loadItemCompletedCallback, params object[] filterParameters)
{
    string customerName = string.Empty;
    string cacheKey = ViewName;

    // Parse the optional parameters:
    if (filterParameters.Length > 0)
    {
        customerName = filterParameters[0].ToString();
        cacheKey += "-" + customerName;
    }

    CamlQuery query = CamlQueryBuilder.GetCamlQuery(ViewName, customerName);
    ListItemCollection items = Context.Web.Lists.GetByTitle(ListTitle).GetItems(query);
    Context.Load(items);
    Context.Load(items, listItems => listItems.Include(item => item.FieldValuesAsText));

    Context.ExecuteQueryAsync(
        delegate(object sender, ClientRequestSucceededEventArgs args)
        {
            base.CacheView(cacheKey, items);
            loadItemCompletedCallback(new LoadViewCompletedEventArgs { ViewName = ViewName, Items = base.GetCachedView(cacheKey) });
        },
        delegate(object sender, ClientRequestFailedEventArgs args)
        {
            loadItemCompletedCallback(new LoadViewCompletedEventArgs { Error = args.Exception });
        });
}
```

16. <span data-ttu-id="93b21-263">Аналогичным образом измените метод **LoadData** в файле ListDataProvider.cs для обработки параметр **CustomerName**.</span><span class="sxs-lookup"><span data-stu-id="93b21-263">Likewise, modify the **LoadData** method in the ListDataProvider.cs file to process the **CustomerName** parameter.</span></span>
    
```cs
  
public override void LoadData(string ViewName, Action<LoadViewCompletedEventArgs>
                                                           loadViewCompletedCallback, params object[] filterParameters)
{
    string customerName = string.Empty;
    string cacheKey = ViewName;

    // Parse the optional parameters:
    if (filterParameters.Length > 0)
    {
        customerName = filterParameters[0].ToString();
        cacheKey += "-" + customerName;
    }

    List<ListItem> CachedItems = GetCachedView(cacheKey);
    if (CachedItems != null)
    {
        loadViewCompletedCallback(new LoadViewCompletedEventArgs { ViewName = ViewName, Items = CachedItems });
        return;
    }

    LoadDataFromServer(ViewName, loadViewCompletedCallback, filterParameters);
}
```

17. <span data-ttu-id="93b21-p133">Добавьте кнопку **Отмена** элемент **ApplicationBar** в файле List.xaml в проекте OrdersSPListApp. В **Обозревателе решений** в узле OrdersSPListApp выберите файл List.xaml и нажмите клавишуSHIFT + F7Откройте файл для редактирования в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="93b21-p133">Add a **Cancel** button to the **ApplicationBar** element in the List.xaml file in the OrdersSPListApp project. In **Solution Explorer**, under the OrdersSPListApp node, choose the List.xaml file, and then press SHIFT+F7 to open the file for editing in the designer.</span></span>
    
  
18. <span data-ttu-id="93b21-266">Добавьте XAML для объявления кнопка **Отмена** внутри тега `<phone:PhoneApplicationPage.ApplicationBar>` , как показано в следующей разметке.</span><span class="sxs-lookup"><span data-stu-id="93b21-266">Add XAML to declare a **Cancel** button within the `<phone:PhoneApplicationPage.ApplicationBar>` tag, as shown in the following markup.</span></span>
    
```
  
<phone:PhoneApplicationPage.ApplicationBar>
    <shell:ApplicationBar IsVisible="True" IsMenuEnabled="True">
        <shell:ApplicationBarIconButton x:Name="btnNew" 
                 IconUri="/Images/appbar.new.rest.png" Text="New" Click="OnNewButtonClick"/>
        <shell:ApplicationBarIconButton x:Name="btnRefresh" IconUri="/Images/appbar.refresh.rest.png" 
                 Text="Refresh" IsEnabled="True" Click="OnRefreshButtonClick"/>
        <shell:ApplicationBarIconButton x:Name="btnCancel" IconUri="/Images/appbar.cancel.rest.png" Text="Cancel" IsEnabled="True" Click="OnCancelButtonClick" />
    </shell:ApplicationBar>
</phone:PhoneApplicationPage.ApplicationBar>
```

19. <span data-ttu-id="93b21-267">С помощью файла List.xaml, выбранного в **Обозревателе решений** нажмите клавишуF7Чтобы открыть файл выделенным кодом List.xaml.cs, для редактирования.</span><span class="sxs-lookup"><span data-stu-id="93b21-267">With the List.xaml file selected in **Solution Explorer**, press F7 to open the associated code-behind file, List.xaml.cs, for editing.</span></span>
    
  
20. <span data-ttu-id="93b21-268">В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **ListForm** добавьте следующий обработчик для события **OnCancelButtonClick**.</span><span class="sxs-lookup"><span data-stu-id="93b21-268">Within the code block (demarcated by opening and closing braces) that implements the **ListForm** partial class, add the following handler for the **OnCancelButtonClick** event.</span></span>
    
```cs
  
private void OnCancelButtonClick(object sender, EventArgs e)
{
    NavigationService.Navigate(new Uri("/CustomersSPListApp;component/Views/DisplayForm.xaml", UriKind.Relative));
}
```

21. <span data-ttu-id="93b21-269">Сохраните файлы в проекте.</span><span class="sxs-lookup"><span data-stu-id="93b21-269">Save the files in the project.</span></span>
    
  
<span data-ttu-id="93b21-270">Теперь он остается для добавления кнопки на форму просмотра в проект CustomersSPListApp, чтобы показать заказы, связанные с указанной клиентом.</span><span class="sxs-lookup"><span data-stu-id="93b21-270">Now, it remains to add a button to the Display form in the CustomersSPListApp project to show the orders associated with a given customer.</span></span>
  
    
    

### <a name="to-configure-the-customerssplistapp-project"></a><span data-ttu-id="93b21-271">Настройка проекта CustomersSPListApp</span><span class="sxs-lookup"><span data-stu-id="93b21-271">To configure the CustomersSPListApp project</span></span>


1. <span data-ttu-id="93b21-272">В **Обозревателе решений** в узле проекта CustomersSPListApp, выберите файл DisplayForm.xaml.</span><span class="sxs-lookup"><span data-stu-id="93b21-272">In **Solution Explorer**, under the node for the CustomersSPListApp project, choose the DisplayForm.xaml file.</span></span>
    
  
2. <span data-ttu-id="93b21-273">КлавишиSHIFT + F7(или дважды щелкните файл) откройте файл для редактирования в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="93b21-273">Press Shift + F7 (or double-click the file) to open the file for editing in the designer.</span></span>
    
  
3. <span data-ttu-id="93b21-274">Добавьте XAML объявления элемента управления **Button** внутри другого элемента управления **StackPanel** после контейнер элемента управления окончательный **StackPanel** для последнего поля элемента списка, как показано в следующей разметке.</span><span class="sxs-lookup"><span data-stu-id="93b21-274">Add XAML declarations for a **Button** control within a containing **StackPanel** control after the final **StackPanel** control container for the last field of the list item, as in the following markup.</span></span>
    
```
  
...
    <Grid x:Name="LayoutRoot" Background="Transparent" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:controls="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone.Controls">
        <StackPanel>
            <ProgressBar Background="Red" x:Name="progressBar" Opacity="1" HorizontalAlignment="Center" 
              VerticalAlignment="Top" Height="15" Width="470" IsIndeterminate="{Binding IsBusy}" 
               Visibility="{Binding ShowIfBusy}" />
            <ScrollViewer HorizontalScrollBarVisibility="Auto" Height="700">
                <Grid x:Name="ContentPanel" Width="470">
                    <StackPanel Margin="0,5,0,5">
                        <StackPanel HorizontalAlignment="Left" Orientation="Horizontal" Margin="0,5,0,5">
                            <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
                                           Style="{StaticResource PhoneTextNormalStyle}">Title :</TextBlock>
                            <TextBlock Width="310" HorizontalAlignment="Left" Name="txtTitle"
                                    Text="{Binding [Title]}" TextWrapping="Wrap" Style="{StaticResource PhoneTextSubtleStyle}" />
                                   </StackPanel>
                        <StackPanel HorizontalAlignment="Left" Orientation="Horizontal" Margin="0,5,0,5">
                            <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
                                       Style="{StaticResource PhoneTextNormalStyle}">Contact Number :</TextBlock>
                            <TextBlock Width="310" HorizontalAlignment="Left" Name="txtContact_x0020_Number"
                                       Text="{Binding [Contact_x0020_Number]}" TextWrapping="Wrap" 
                                       Style="{StaticResource PhoneTextSubtleStyle}" />
                        </StackPanel>
                        <StackPanel HorizontalAlignment="Left" Orientation="Horizontal" Margin="0,5,0,5">
                            <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
                                     Style="{StaticResource PhoneTextNormalStyle}">E-mail Address :</TextBlock>
                            <TextBlock Width="310" HorizontalAlignment="Left" Name="txtE_x002d_mail_x0020_Address" 
                                 Text="{Binding [E_x002d_mail_x0020_Address]}" TextWrapping="Wrap" 
                                             Style="{StaticResource PhoneTextSubtleStyle}" />
                        </StackPanel>
                        <StackPanel HorizontalAlignment="Left" Orientation="Horizontal" Margin="0,5,0,5">
                            <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
                                     Style="{StaticResource PhoneTextNormalStyle}">Company :</TextBlock>
                            <TextBlock Width="310" HorizontalAlignment="Left" Name="txtCompany" 
                                     Text="{Binding [Company]}" TextWrapping="Wrap" Style="{StaticResource PhoneTextSubtleStyle}" />
                        </StackPanel>
                        <StackPanel Margin="0,60,0,5"><Button Content="Get Orders" Height="70" Name="OrdersButton" Width="400" Click="OnButtonOrdersClick" /></StackPanel>
                    </StackPanel>
                </Grid>
            </ScrollViewer>
        </StackPanel>
    </Grid>
...
```

4. <span data-ttu-id="93b21-275">С помощью файла DisplayForm.xaml, выбранного в **Обозревателе решений** нажмите клавишуF7Чтобы открыть файл выделенным кодом displayform.XAML.cs из, для редактирования.</span><span class="sxs-lookup"><span data-stu-id="93b21-275">With the DisplayForm.xaml file selected in **Solution Explorer**, press F7 to open the associated code-behind file, DisplayForm.xaml.cs, for editing.</span></span>
    
  
5. <span data-ttu-id="93b21-276">В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **DisplayForm** добавьте следующий обработчик для события **OnButtonOrdersClick**.</span><span class="sxs-lookup"><span data-stu-id="93b21-276">Within the code block (demarcated by opening and closing braces) that implements the **DisplayForm** partial class, add the following handler for the **OnButtonOrdersClick** event.</span></span>
    
```cs
  
private void OnOrdersButtonClick(object sender, RoutedEventArgs e)
{
    this.NavigationService.Navigate(new Uri("/OrdersSPListApp;component/Views/List.xaml?CustomerName=" + 
                                                                 viewModel["Title"], UriKind.Relative));
}
```

6. <span data-ttu-id="93b21-277">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="93b21-277">Save the file.</span></span>
    
  
<span data-ttu-id="93b21-p134">Если построить решение и его развертывание на эмулятора Windows Phone, отображается форма списка для списка клиентов. Выбор элемента в списке, чтобы показать форме отображения для данного клиента, вы увидите кнопку, чтобы получить заказы, связанные с клиента (рис. 1).</span><span class="sxs-lookup"><span data-stu-id="93b21-p134">If you build the solution and deploy it to the Windows Phone Emulator, the List form for the Customers list appears. If you choose an item in the list to show the Display form for a given customer, you see a button to retrieve the orders associated with that customer (Figure 1).</span></span>
  
    
    

<span data-ttu-id="93b21-280">**На рисунке 1. Форма просмотра клиентов**</span><span class="sxs-lookup"><span data-stu-id="93b21-280">**Figure 1. Customers Display form**</span></span>

  
    
    

  
    
    
![Форма "Отображение клиентов"](../images/70d5a602-b349-4791-bf05-d61635d0fc91.gif)
  
    
    
<span data-ttu-id="93b21-282">После нажатия кнопки **Получить заказы** на этой форме отображения заказов для клиента отображаются в виде списка из проекта OrdersSPListApp в решении (на рисунке 2).</span><span class="sxs-lookup"><span data-stu-id="93b21-282">When you choose the **Get Orders** button on this Display form, the orders for the customer are displayed in the List form from the OrdersSPListApp project in the solution (Figure 2).</span></span>
  
    
    

<span data-ttu-id="93b21-283">**На рисунке 2. Форма списка заказов**</span><span class="sxs-lookup"><span data-stu-id="93b21-283">**Figure 2. Orders List form**</span></span>

  
    
    

  
    
    
![Форма "Список заказов"](../images/884d6dcb-c690-4b43-9bb2-d1bcaf4b7a31.gif)
  
    
    
<span data-ttu-id="93b21-p135">С помощью этой формы (формы списка для списка заказов) Добавление, изменение и удаление заказов для клиента. При выборе кнопки **Отмена** открыто формы списка для списка клиентов. В приложении одного телефона можно управлять элементов списка на два списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="93b21-p135">From this form (the List form for the Orders list) you can add, edit, or delete orders for a customer. If you choose the **Cancel** button, you navigate back to the List form for the Customers list. In a single phone app, you can manage the list items from two SharePoint lists.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="93b21-288">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="93b21-288">Additional resources</span></span>
<span data-ttu-id="93b21-289"><a name="SP15Usemultlists_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="93b21-289"></span></span>


-  [<span data-ttu-id="93b21-290">Как: Настройка и использование push-уведомлений в SharePoint приложений для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="93b21-290">How to: Configure and use push notifications in SharePoint apps for Windows Phone</span></span>](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [<span data-ttu-id="93b21-291">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="93b21-291">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="93b21-292">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="93b21-292">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="93b21-293">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="93b21-293">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="93b21-294">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="93b21-294">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="93b21-295">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="93b21-295">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

