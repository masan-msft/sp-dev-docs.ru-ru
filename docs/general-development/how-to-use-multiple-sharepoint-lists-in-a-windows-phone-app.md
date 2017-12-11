---
title: "Использование нескольких списков SharePoint в приложении Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5251d35a-d659-49b3-8e0d-dfd4a7faee6b
ms.openlocfilehash: 675a42d7de04467d780aa170183ce3c9d309d94a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-multiple-sharepoint-lists-in-a-windows-phone-app"></a>Использование нескольких списков SharePoint в приложении Windows Phone
Создайте приложения Windows Phone, использующие данные из нескольких списков SharePoint. Можно использовать несколько списков SharePoint в приложении несколькими способами. При создании приложения Windows Phone, на основе шаблона приложения списка SharePoint для Windows Phone, укажите единого целевого списка SharePoint, но архитектура результирующий проект расширяемой, чтобы учесть интеграции нескольких списков.
  
    
    


> **Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express. За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7. > Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md). 
  
    
    


## <a name="create-a-solution-involving-sharepoint-lists-based-on-the-same-schema"></a>Создание решения, включающие использование списков SharePoint на основе же схемы
<a name="BKMK_SameSchemaProject"> </a>

Если у вас есть два списка SharePoint, на основе же схемы, можно воспользоваться преимуществами классы, реализованный шаблона приложения списка SharePoint для Windows Phone и создание объектов классов для каждого списка.
  
    
    
Предположим, что у вас есть два списка SharePoint, на основе шаблона списка контактов. Один список, с именем, например, группа маркетинга, содержит члены группы маркетинга в вашей организации, а списке другие команды разработчиков участники инженерной группы. При создании проекта с помощью шаблона приложения списка SharePoint для Windows Phone и указать группы маркетинга списка в качестве целевого списка на основе которого нужно создать проект экземпляр класса **ListDataProvider** создается в реализация класса **App** в файл App.xaml.cs в проекте (именованные **DataProvider** по умолчанию). Этот объект представляет список список (то есть, группа маркетинга) как источник данных для приложения, предоставляя операции для доступа и работа с элементами в списке. Для списка, лежащие в основе приложения также создается экземпляр класса **ListViewModel**. Этот объект содержит свойство участником (который также быть с именем **DataProvider**), который может иметь значение данного экземпляра класса **ListDataProvider** установление источник данных для экземпляра класса **ListViewModel**.
  
    
    
Можно создать дополнительные экземпляр класса **ListDataProvider** в проект в качестве источника данных для второго списка (командой разработчиков) в файл App.xaml.cs. В следующем коде объект называется **SecondaryDataProvider**.
  
    
    



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

Затем можно создайте другой объекта класса **ListViewModel** (с именем, например, **SecondaryViewModel**) и назначить его свойство **DataProvider**, как в следующем коде объект **SecondaryDataProvider**.
  
    
    



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

Если же полей и представлений для двух списков применимость для ваших целей (и, снова, если приведены два иметь одинаковые столбцы и поля), внесите изменения в реализации класс **ListDataProvider** (в файле ListDataProvider.cs) не требуется.
  
    
    
Для просмотра или изменения данных во втором в вашем проекте, необходимо добавить представление формы в проект, который привязан к и настроен для этой **SecondaryViewModel**. К примеру вы добавьте папку с именем «SecondaryViews» проект и добавьте файл SecondaryList.xaml в этой папке разметку следующий файл List.xaml по умолчанию, созданной с помощью шаблона для основного списка в проекте. Обратите внимание на то, следует различать дополнительного формы списка из основной формы списка в приложении, указав отличительные значение для атрибута **x:Class** элемента **PhoneApplicationPage** в файле SecondaryList.xaml.
  
    
    



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

В файле выделенным кодом SecondaryList.xaml.cs, замените все ссылки на "App.MainViewModel" со ссылками на «App.SecondaryViewModel». Например конструктор в файле должен иметь следующий вид.
  
    
    



```cs

public ListForm()
    {
        InitializeComponent();
        this.DataContext = App.SecondaryViewModel;
    }
```

Также заменить все ссылки в файл фонового кода «App.DataProvider» со ссылками на «App.SecondaryDataProvider» и обновить любые пути навигации для указания на соответствующие дополнительные страницы XAML. При добавлении дополнительных новая форма для проекта (с именем, например, SecondaryNewForm.xaml в папке SecondaryViews проекта), обработчика в файле SecondaryList.xaml.cs для события **OnNewButtonClick** будет выглядеть следующим образом.
  
    
    



```cs

private void OnNewButtonClick(object sender, EventArgs e)
    {
        // Instantiate a new instance of NewItemViewModel and go to NewForm.
        App.SecondaryViewModel.CreateItemViewModelInstance = new NewItemViewModel { DataProvider = App.SecondaryDataProvider };
        NavigationService.Navigate(new Uri("/SecondaryViews/SecondaryNewForm.xaml", UriKind.Relative));
    }
```

И, наконец можно добавить кнопку для **ApplicationBar** в файле List.xaml для отображения страницы SecondaryList.xaml.
  
    
    



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

В файле выделенным кодом List.xaml.cs, добавьте обработчик для события **OnSecondaryListButtonClick**, указанной в файле List.xaml.
  
    
    



```cs

private void OnSecondaryListButtonClick(object sender, EventArgs e)
{
    NavigationService.Navigate(new Uri("/SecondaryViews/SecondaryList.xaml", UriKind.Relative));
}
```

Пользователи вашего приложения могут перейти от команды разработчиков и списка группа маркетинга. Так как основной схемы списков совпадают, по умолчанию **DataProvider** и **MainViewModel** объекты созданный шаблон, а также добавлена обрабатывать объекты **SecondaryDataProvider** и **SecondaryViewModel** всех транзакций данных без необходимости каких-либо изменений в файл ListDataProvider.cs.
  
    
    

## <a name="create-a-solution-involving-sharepoint-lists-based-on-different-schemas"></a>Создание решения, включающие использование списков SharePoint на основе различных схем
<a name="BKMK_DifferentSchemasProject"> </a>

Подход в предыдущем разделе works до его переход (которые, для списков SharePoint на основе одинаковую схему), но класс **ListDataProvider** в шаблон доступен для разработчиков для настройки для обработки нескольких списков SharePoint, которые не могут быть основаны на той же схеме или не включать же столбцов и полей приложения списка SharePoint Windows Phone.
  
    
    
Предположим, что, как и в предыдущем разделе, наличие списка SharePoint, группа маркетинга (на основе шаблона списка контактов), содержащий члены группы маркетинга. Имеется также второй список, с именем заказы (на основе настраиваемого списка шаблона), содержащий столбцы и типы полей, показано в таблице 1.
  
    
    

**В таблице 1. Столбцов и полей для списка заказов**


|**Столбец**|**Тип поля**|**Обязательный**|
|:-----|:-----|:-----|
|Продукт (например, заголовок)  <br/> |Однострочный текст (Текст)  <br/> |Да  <br/> |
|Цена  <br/> |Денежный  <br/> |Да  <br/> |
|Количество  <br/> |Number (числовое значение);  <br/> |Нет (по умолчанию присваивается значение 0)  <br/> |
|Значение заказа  <br/> |Вычисляется (цена * количество)  <br/> |Нет  <br/> |
|Дата заказа  <br/> |Дата и время (Datetime)  <br/> |Нет  <br/> |
|Статус заказа  <br/> |Варианты  <br/> |Нет  <br/> |
|Клиент  <br/> |Однострочный текст (Текст)  <br/> |Нет  <br/> |
   
Как показано в примере в предыдущем разделе можно создать экземпляр объекта отдельные **ListDataProvider** и другой объект **ListViewModel** для управления списка заказов. Предполагается, что объект инициализированный **ListDataProvider** с именем **OrdersListDataProvider**, как показано в следующем примере кода.
  
    
    



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

Предполагается, что объект инициализированный **ListViewModel** для списка заказов с именем **OrdersListViewModel**, как показано в следующем примере кода.
  
    
    



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

Схемы для списка заказов отличается от списка, группа маркетинга. Позволяет разместить различия, добавив код в файле ListDataProvider.cs специально для класса **CamlQueryBuilder**.
  
    
    



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

Здесь вторую запись со значением ключа «View2» добавляется к объекту **Dictionary** **ViewXmls**для списка заказов. (Имейте в виду, что ключ значений для записи, добавляемые **ViewXmls** **Dictionary** в классе **CamlQueryBuilder** должны быть уникальными (в решении) для кэширования логика в шаблоне для правильной работы.) Переменные String ( **View1Fields** и **View2Fields**) используются для хранения список полей для каждого представления. Затем в зависимости от значения параметра **viewName**, переданной в метод **GetCamlQuery**, создается соответствующий запрос CAML XML-строка.
  
    
    
Затем как и в предыдущем разделе, можно создавать формы представления для списка, привязанных к **OrdersListViewModel** и **OrdersListDataProvider** объекты этого времени. Например, XAML для формы списка, определенного в список заказов с именем OrdersList.xaml, аналогичную разметку в файле List.xaml создаются с помощью шаблона для основного списка в приложении, за исключением того, что будет имя элемента управления **PivotItem**, который отображает список "View2" (а не по умолчанию "Представление1") и задайте объявление **Binding** в атрибуте **ItemsSource** элемента управления **ListBox**, в котором элементы списка отображаются в "View2" как в следующем примере Разметка (где отображаются только разметка для сетки корневой страницы).
  
    
    



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

 Это удобный способ создания подходящего разметки XAML для использования шаблона приложения списка SharePoint для Windows Phone для создания отдельного проекта на основе списка заказов и затем скопируйте созданный код XAML из этого проекта в проект с помощью нескольких списков, с учетом изменить имя элемента управления **PivotItem** (значение по умолчанию "Представление1") на "View2" и измените объявление **Binding** элемента управления **ListBox**, как показано ниже. Необходимо также изменить все ссылки в файле выделенным кодом для формы для указания соответствующих объектов **ListViewModel** и **DataProvider** (как, например, **OrdersListViewModel** и **OrdersListDataProvider**).
  
    
    
Такой подход работает, так как в файле выделенным кодом (с именем, в данном случае OrdersList.xaml.cs), управлять различных обработчиков событий, которые могут вызывать методы объекта **ListDataProvider** (в данном случае  **OrdersListDataProvider**) для доступа к списка используйте имя **PivotItem**, чтобы указать соответствующие представления для использования. Например, для обработчика событий **OnPivotItemLoaded** вызывает метод **LoadData** **OrdersListViewModel** объект, созданный из класса **ListViewModel** (и в свою очередь, этот метод вызывает метод **LoadData** объекта **OrdersListDataProvider** ), передающая свое имя элемента управления **PivotItem** (здесь "View2") в качестве значения параметра **ViewName** методу. В конечном счете это же значение передается (в качестве значения параметра **viewName** ) в метод **GetCamlQuery** показано выше в измененные реализация класса **CamlQueryBuilder**.
  
    
    

## <a name="an-alternative-approach-for-a-solution-involving-sharepoint-lists-based-on-different-schemas"></a>Альтернативный подход для решения, включающие использование списков SharePoint на основе различных схем
<a name="BKMK_DifferentSchemasAlternative"> </a>

В качестве альтернативы подхода в предыдущем разделе можно использовать шаблон приложения списка SharePoint для Windows Phone для создания Windows Phone проекта приложения в Microsoft Visual Studio 2010 решения на основе заданного списка SharePoint, а затем добавьте проекты построена на основе других списков для этого же решения. Такой подход позволяет воспользоваться преимуществами шаблон для создания форм для каждого списка SharePoint. Затем можно настроить решение по мере необходимости для управления взаимодействия пользователей с помощью списков. В этом разделе описано этого подхода.
  
    
    
Для выполнения следующих процедур предполагается наличие списка SharePoint с именем Orders (на основе настраиваемого списка шаблона), с помощью столбцов и типов полей, как показано в таблице 1 в предыдущем разделе. Кроме того, предположим, у вас есть другой список SharePoint (еще раз, на основе шаблона списка Custom), с именем клиентов, и столбцов и типов полей, приведенных в таблице 2.
  
    
    

**В таблице 2. Столбцов и полей для списка клиентов**


|**Столбец**|**Тип поля**|**Обязательный**|
|:-----|:-----|:-----|
|Имя пользователя (например, заголовок)  <br/> |Однострочный текст (Текст)  <br/> |Да  <br/> |
|Номер контакта  <br/> |Однострочный текст (Текст)  <br/> |Нет  <br/> |
|Адрес электронной почты  <br/> |Однострочный текст (Текст)  <br/> |Нет  <br/> |
|Компания  <br/> |Однострочный текст (Текст)  <br/> |Нет  <br/> |
   
В следующих процедурах Создание приложения Windows Phone, которое использует оба эти списки. Основной список в приложение, список клиентов. При просмотре сведений для данного клиента в форме отображения кнопки включен на форме, которая позволяет пользователям отображать все заказы (из списка заказов) относящиеся к этому клиенту.
  
    
    

### <a name="to-create-the-component-projects-for-the-solution"></a>Для создания проектов компонент для решения


1. Создание приложения Windows Phone с использованием шаблона приложения списка SharePoint для Windows Phone, указание список SharePoint, заданных на основе столбцов и типов полей, приведенных в таблице 2. В процедур, описанных в этом разделе предполагается, что имя списка в проекте является «Клиенты» и «CustomersSPListApp» — это имя проекта. (Увидеть [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md) сведения о создании приложения на основе шаблона приложения списка SharePoint для Windows Phone.. MD)
    
  
2. Выберите **файл**, **Добавить** **Новый проект** в Visual Studio. 
    
    Откроется диалоговое окно **Добавление нового проекта**.
    
  
3. В диалоговом окне **Добавить новый проект** разверните узел **Visual C#** и выберите узел **Silverlight для Windows Phone**.
    
  
4. В области **Шаблоны** выберите шаблон приложения списка SharePoint для Windows Phone.
    
  
5. Имя приложения, например, OrdersSPListAppи нажмите кнопку **ОК**.
    
  
6. Выполните процедуру, описанную в [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md) для создания другого проекта приложения Windows Phone, определяющее список SharePoint, заданных на основе столбцов и Показать типов полей в таблице 1 как целевого списка для проекта. Теперь вы должны два проекта в решении с именем «CustomersSPListApp» и «OrdersSPListApp» (при использовании соглашения о наименовании в этой процедуре).
    
  
7. В **Обозревателе решений** выберите узел проекта CustomerSPListApp.
    
  
8. В меню **проект** выберите команду **Добавить ссылку**. 
    
    Откроется диалоговое окно **Добавить ссылку**.
    
  
9. На вкладке **проекты** выберите проект OrdersSPListApp в решение и затем нажмите кнопку **ОК**. Проект будет добавлен в узле **ссылки** проекта CustomersSPListApp.
    
  
Далее настройте два проекта в решение. По сути настройки проекта OrdersSPListApp (основан на список заказов) для работы в качестве «поиск» проекта для проекта CustomerSPListApp (основан на список клиентов).
  
    
    

### <a name="to-configure-the-orderssplistapp-project"></a>Настройка проекта OrdersSPListApp


1. Изменение пути перехода в формах представление проекта OrdersSPListApp для включения основного пространства имен проекта ("OrdersSPListApp") и обозначение «компонент». В обработчике для события OnNewButtonClick в файле List.xaml.cs OrdersSPListApp проекта, измените, например, вызов метода навигатор объекта NavigationService из этого:
    
     `NavigationService.Navigate(new Uri("/Views/NewForm.xaml", UriKind.Relative));`
    
    на строку следующего вида:
    
     `NavigationService.Navigate(new Uri("/OrdersSPListApp;component/Views/NewForm.xaml", UriKind.Relative));`
    
    Чтобы выполнить эти изменения проще всего использовать команду **Быстрая замена** в проекте OrdersSPListApp.
    
1. В **Обозревателе решений** выберите узел проекта OrdersSPListApp.
    
  
2. Клавиши Ctrl + H, чтобы отобразить диалоговое окно " **Быстрая замена** ".
    
  
3. В текстовом поле **Найти** задайте следующий текст именно то, которое будет отображаться здесь:
    
    URI ("/Views/
    
  
4. В текстовом поле **Заменить** так, как оно указано здесь укажите следующий текст:
    
    URI ("/ OrdersSPListApp; компонент/представлений /
    
  
5. Убедитесь, что выбран **Текущий проект**, в раскрывающемся списке **Искать в**.
    
  
6. Нажмите кнопку **Заменить все**.
    
  
7. Сохраните все измененные файлы в проекте.
    
  
2. Добавление свойства элемента в файл App.xaml.cs OrdersSPListApp проекта. В **Обозревателе решений** выберите узел проекта OrdersSPListApp и выберите файл App.xaml.
    
  
3. КлавишиF7Чтобы открыть файл его выделенным кодом App.xaml.cs, для редактирования.
    
  
4. В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **App** добавьте следующий код.
    
```cs
  
public static string CustomerName { get; set; }
```

5. В **Обозревателе решений** выберите узел проекта OrdersSPListApp и выберите файл List.xaml.
    
  
6. КлавишиF7Чтобы открыть файл его выделенным кодом List.xaml.cs, для редактирования.
    
  
7. Измените обработчик событий **OnNavigatedTo** в файле для анализа **QueryString** свойства объекта **NavigationContext**, чтобы задать значение переменной **CustomerName**, указанному в шаге 4. Можно также установить свойство **Header** **PivotItem** элемента управления в форме списка в соответствии с именем customer, для удобства пользователей. Измененные обработчик должен иметь следующий вид.
    
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

8. Добавьте в качестве аргумента в вызове метода **LoadData** в обработчике событий **OnPivotItemLoaded** в файле List.xaml.cs **CustomerName**. Реализация обработчика событий **OnPivotItemLoaded** должен иметь следующий вид.
    
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
    
  
9. Также добавьте переменную **CustomerName** в качестве аргумента в вызове метода **LoadData** в обработчике событий **OnViewModelInitialization**. Реализация обработчика событий **OnViewModelInitialization** должен иметь следующий вид.
    
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

10. Добавьте в качестве аргумента в вызове метода **RefreshData** в обработчике событий **OnRefreshButtonClick** в файле List.xaml.cs **CustomerName**. Реализация обработчика событий **OnRefreshButtonClick** должен иметь следующий вид.
    
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
    
  
11. Когда пользователи нажмите кнопку **Создать** на формы списка для списка заказов в вашем приложении, поле клиента в форме создания уже должны содержать имя клиента, так как список заказов, отображаются для пользователя было отфильтровано, основанным на имя клиента. Новые заказы, добавленных из фильтрованного списка должен быть связан с именем customer, на котором список фильтруется. Чтобы передать значение переменной **CustomerName** новая форма, измените событие **OnNewButtonClick** для значение как строку запроса в путь перехода на новую форму, как показано в следующем коде.
    
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

12. В обработчике событий **OnNavigatedTo** новая форма Проверьте строки запроса с именем customer, если он доступен, его и назначьте поле Клиент ViewModel для формы. В **Обозревателе решений** выберите в разделе проект OrdersSPListApp, выберите файл NewForm.xaml и нажмите кнопкуF7Чтобы открыть файл его выделенным кодом NewForm.xaml.cs, для редактирования.
    
  
13. Измените обработчик событий **OnNavigatedTo** в файле в соответствии со следующим кодом.
    
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

14. В классе **CamlQueryBuilder** в файле ListDataProvider.cs в проекте OrdersSPListApp добавьте предложение **WHERE** в поле клиента в CAML запрос, используемый для получения элементов из списка заказов для фильтрации списка на основе имени данного клиента (из переменной **CustomerName** ). Добавьте параметр **GetCamlQuery** методы в классе передачи имени клиента. Класс измененные **CamlQueryBuilder** должен иметь следующий вид.
    
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

15. Измените метод **LoadDataFromServer** в файле ListDataProvider.cs для проверки в аргументе **CustomerName** и передачи аргумента в метод **GetCamlQuery**. Измененный метод должен иметь следующий вид.
    
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

16. Аналогичным образом измените метод **LoadData** в файле ListDataProvider.cs для обработки параметр **CustomerName**.
    
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

17. Добавьте кнопку **Отмена** элемент **ApplicationBar** в файле List.xaml в проекте OrdersSPListApp. В **Обозревателе решений** в узле OrdersSPListApp выберите файл List.xaml и нажмите клавишуSHIFT + F7Откройте файл для редактирования в конструкторе.
    
  
18. Добавьте XAML для объявления кнопка **Отмена** внутри тега `<phone:PhoneApplicationPage.ApplicationBar>` , как показано в следующей разметке.
    
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

19. С помощью файла List.xaml, выбранного в **Обозревателе решений** нажмите клавишуF7Чтобы открыть файл выделенным кодом List.xaml.cs, для редактирования.
    
  
20. В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **ListForm** добавьте следующий обработчик для события **OnCancelButtonClick**.
    
```cs
  
private void OnCancelButtonClick(object sender, EventArgs e)
{
    NavigationService.Navigate(new Uri("/CustomersSPListApp;component/Views/DisplayForm.xaml", UriKind.Relative));
}
```

21. Сохраните файлы в проекте.
    
  
Теперь он остается для добавления кнопки на форму просмотра в проект CustomersSPListApp, чтобы показать заказы, связанные с указанной клиентом.
  
    
    

### <a name="to-configure-the-customerssplistapp-project"></a>Настройка проекта CustomersSPListApp


1. В **Обозревателе решений** в узле проекта CustomersSPListApp, выберите файл DisplayForm.xaml.
    
  
2. КлавишиSHIFT + F7(или дважды щелкните файл) откройте файл для редактирования в конструкторе.
    
  
3. Добавьте XAML объявления элемента управления **Button** внутри другого элемента управления **StackPanel** после контейнер элемента управления окончательный **StackPanel** для последнего поля элемента списка, как показано в следующей разметке.
    
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

4. С помощью файла DisplayForm.xaml, выбранного в **Обозревателе решений** нажмите клавишуF7Чтобы открыть файл выделенным кодом displayform.XAML.cs из, для редактирования.
    
  
5. В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **DisplayForm** добавьте следующий обработчик для события **OnButtonOrdersClick**.
    
```cs
  
private void OnOrdersButtonClick(object sender, RoutedEventArgs e)
{
    this.NavigationService.Navigate(new Uri("/OrdersSPListApp;component/Views/List.xaml?CustomerName=" + 
                                                                 viewModel["Title"], UriKind.Relative));
}
```

6. Сохраните файл.
    
  
Если построить решение и его развертывание на эмулятора Windows Phone, отображается форма списка для списка клиентов. Выбор элемента в списке, чтобы показать форме отображения для данного клиента, вы увидите кнопку, чтобы получить заказы, связанные с клиента (рис. 1).
  
    
    

**На рисунке 1. Форма просмотра клиентов**

  
    
    

  
    
    
![Форма "Отображение клиентов"](../images/70d5a602-b349-4791-bf05-d61635d0fc91.gif)
  
    
    
После нажатия кнопки **Получить заказы** на этой форме отображения заказов для клиента отображаются в виде списка из проекта OrdersSPListApp в решении (на рисунке 2).
  
    
    

**На рисунке 2. Форма списка заказов**

  
    
    

  
    
    
![Форма "Список заказов"](../images/884d6dcb-c690-4b43-9bb2-d1bcaf4b7a31.gif)
  
    
    
С помощью этой формы (формы списка для списка заказов) Добавление, изменение и удаление заказов для клиента. При выборе кнопки **Отмена** открыто формы списка для списка клиентов. В приложении одного телефона можно управлять элементов списка на два списка SharePoint.
  
    
    

## <a name="see-also"></a>См. также
<a name="SP15Usemultlists_addlresources"> </a>


-  [Как: Настройка и использование push-уведомлений в SharePoint приложений для Windows Phone](how-to-configure-and-use-push-notifications-in-sharepoint-apps-for-windows.md)
    
  
-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

