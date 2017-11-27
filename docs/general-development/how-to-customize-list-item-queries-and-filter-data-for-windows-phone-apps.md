---
title: "Настройка запросов элементов списка и фильтрация данных для приложений Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 32f89b97-8274-4cb0-9164-7898735a18aa
ms.openlocfilehash: c7347e36ce052f8b8f341689a633ac9a6850247f
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="customize-list-item-queries-and-filter-data-for-windows-phone-apps"></a><span data-ttu-id="5e4b4-102">Настройка запросов элементов списка и фильтрация данных для приложений Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5e4b4-102">Customize list item queries and filter data for Windows Phone apps</span></span>

<span data-ttu-id="5e4b4-p101">Настройте запросы данных, на которых основаны представления в приложении Windows Phone. С помощью проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone разработчики могут использовать преимущества шаблона разработки, реализованных в шаблон, который позволяет им настроить компонентов на уровне данных для приложения Windows Phone. Представление списка SharePoint в приложении Windows Phone можно настраивать в Microsoft SharePoint Server и включенных в приложение на телефоне или можно создать настраиваемое представление для приложения.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p101">Customize the data queries on which the views in a Windows Phone app are based. With projects created from the Windows Phone SharePoint List Application template, developers can take advantage of a design pattern implemented in the template that allows them to customize parts of the data layer for a Windows Phone app. A view of a SharePoint list in a Windows Phone app can be configured in Microsoft SharePoint Server and included as is in the app on the phone, or a custom view can be created for the app.</span></span>
  
    
    


> <span data-ttu-id="5e4b4-106">**Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-106">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="5e4b4-107">За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-107">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="5e4b4-108">> Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-108">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="configure-list-views-on-the-server-for-use-in-windows-phone-apps"></a><span data-ttu-id="5e4b4-109">Настройка представлений списка на сервере для использования в приложениях Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5e4b4-109">Configure list views on the server for use in Windows Phone apps</span></span>
<span data-ttu-id="5e4b4-110"><a name="BKMK_ConfiguringLists"> </a></span><span class="sxs-lookup"><span data-stu-id="5e4b4-110"><a name="BKMK_ConfiguringLists"> </a></span></span>

<span data-ttu-id="5e4b4-p103">При создании приложения списка SharePoint для Windows Phone с использованием шаблона приложения списка SharePoint для Windows Phone, можно включить в свое приложение все существующие представления, которые связаны с целевого списка SharePoint. Одним из способов для фильтрации элементов в списке SharePoint как список будет отображаться на телефоне, затем, является настройка отфильтрованные представления для списка на сервере, а затем выберите нужное должны быть включены в приложении Windows Phone. Мастер шаблона приложения списка SharePoint для Windows Phone создает запрос Язык CAML для выбранного представления, которая включает в себя условия фильтрации, настроенных для представления на сервере. Возможно например, имеется список на сервере, на основе шаблона списка задач. Можно создать представления для списка, с именем «Праздников стороны», которая включает в себя только элементы, связанные с, например, Планирование праздников у компании пользователя, добавив условия фильтра для отображения элементов списка, только если в поле Описание содержит слова «праздников» или «субъект». В приложении Windows Phone разметки CAML, созданных для представления будет выглядеть следующим образом (в зависимости от поля, выбранные для включения в свое приложение).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p103">When you create a SharePoint list app for a Windows Phone by using the Windows Phone SharePoint List Application template, you can choose to include in your app any existing views that are associated with the target SharePoint list. One of the ways to filter items in a SharePoint list as the list appears on the phone, then, is to configure a filtered view for the list on the server and then to select that view to be included in your Windows Phone app. The Windows Phone SharePoint List Application template wizard generates a Collaborative Application Markup Language (CAML) query for the selected view that includes the filtering conditions configured for the view on the server. You might, for example, have a list on the server that is based on the Tasks list template. You can create a view for the list named "Holiday Party" that includes only items related to, for example, planning a company holiday party by adding a filter condition to show list items only when the Description field contains the words "holiday" or "party". In the Windows Phone app, the CAML markup generated for the view would resemble the following (depending on the fields chosen to be included in your app).</span></span>
  
    
    

```XML

<View>
    <Query>
        <Where>
            <Or>
                <Contains>
                    <FieldRef Name='Body' />
                    <Value Type='Note'>holiday</Value>
                </Contains>
                <Contains>
                    <FieldRef Name='Body' />
                    <Value Type='Note'>party</Value>
                </Contains>
            </Or>
        </Where>
    </Query>
    <RowLimit>30</RowLimit>
    <ViewFields>
        <FieldRef Name='Title'/>
        <FieldRef Name='Body'/>
        <FieldRef Name='AssignedTo'/>
        <FieldRef Name='Status'/>
        <FieldRef Name='PercentComplete'/>
        <FieldRef Name='StartDate'/>
        <FieldRef Name='DueDate'/>
        <FieldRef Name='Checkmark'/>
    </ViewFields>
</View>
```

<span data-ttu-id="5e4b4-117">Как и в другие существующие представления для списка задач, которое нужно включить в свое приложение Windows Phone, при создании проекта **PivotItem** управления, соответствующий выбранного представления добавляется элемент управления **Pivot**, который представляет элемент основного пользовательского интерфейса (UI) в приложении.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-117">As with other existing views for the Tasks list that you choose to include in your Windows Phone app when you create your project, a **PivotItem** control corresponding to the chosen view is added to the **Pivot** control that constitutes the main user interface (UI) element in the app.</span></span>
  
    
    

## <a name="customize-list-view-queries-in-the-windows-phone-app"></a><span data-ttu-id="5e4b4-118">Настройка запросов представления списка в приложении Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5e4b4-118">Customize list view queries in the Windows Phone app</span></span>
<span data-ttu-id="5e4b4-119"><a name="BKMK_CustomizingLists"> </a></span><span class="sxs-lookup"><span data-stu-id="5e4b4-119"><a name="BKMK_CustomizingLists"> </a></span></span>

<span data-ttu-id="5e4b4-p104">Для той или иной причине может быть невозможно или разумные для настройки представления, в которых не отвечает вашим требованиям проектирования для заданного списка на сервере. В проекте Microsoft Visual Studio, созданных на основе шаблона приложения списка SharePoint для Windows Phone аспекты называемых уровень данных становятся доступными для разработчиков (en), в основном через файл ListDataProvider.cs в проекте. Можно изменить CAML, определенных для существующего представления, или можно добавить запросы CAML для новых представлений в файле ListDataProvider.cs.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p104">For one reason or another, it may not be possible or reasonable to configure views that meet all of your design needs for a given list on the server. In a Microsoft Visual Studio project created from the Windows Phone SharePoint List Application template, aspects of what may be called the data layer are made available to developers, primarily through the ListDataProvider.cs file in the project. You can modify the CAML defined for an existing view, or you can add CAML queries for new views in the ListDataProvider.cs file.</span></span>
  
    
    

### <a name="the-listdataprovidercs-file"></a><span data-ttu-id="5e4b4-123">Файл ListDataProvider.cs</span><span class="sxs-lookup"><span data-stu-id="5e4b4-123">The ListDataProvider.cs file</span></span>

<span data-ttu-id="5e4b4-p105">В проекте на основе шаблона приложения списка SharePoint для Windows Phone файл ListDataProvider.cs определяет объекты, которые обеспечивают доступ к и настройки списка SharePoint в качестве источника данных для представлений в приложении Windows Phone. В файл List.xaml, который определяет страницу основного приложения для приложения, элемент управления **Pivot** (непосредственно содержащий **PivotItem** дочерних элементов управления) объявлен с обработчиком событий, назначенные к событию **LoadedPivotItem**. Метод **LoadDataFromServer** в файле ListDataProvider.cs в конечном счете вызывается при загрузке элемента управления **PivotItem** (который используется в качестве контейнера отображения для элементов списка в приложении Windows Phone) на странице главному приложению приложения.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p105">In a project based on the Windows Phone SharePoint List Application template, the ListDataProvider.cs file defines objects that provide for accessing and configuring a SharePoint list as a data source for the views in the Windows Phone app. In the List.xaml file, which defines the main application page for the app, a **Pivot** control (itself containing the child **PivotItem** controls) is declared with an event handler assigned to its **LoadedPivotItem** event. The **LoadDataFromServer** method in the ListDataProvider.cs file is ultimately called when a **PivotItem** control (which is used as the rendering container for list items in the Windows Phone app) is loaded on the main application page of the app.</span></span>
  
    
    

1. <span data-ttu-id="5e4b4-127">**PivotItem**, связанный с представлением списка загружается в пользовательском Интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-127">The **PivotItem** associated with a given list view is loaded in the UI.</span></span>
    
  
2. <span data-ttu-id="5e4b4-p106">В файле List.xaml.cs обработчик для события **LoadedPivotItem** вызывает метод **LoadData** в файле ListViewModel.cs, передав имя элемента управления **PivotItem**, после завершения загрузки. (В разработки проектов на основе шаблона приложения списка SharePoint для Windows Phone, имя элемента управления данного **PivotItem** имеет значение же значение ключа для строки запроса CAML для представления, связанного с этим элементом управления в типе **Dictionary** **ViewXmls**, определенном в классе **CamlQueryBuilder** в ListViewModel.cs).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p106">In the List.xaml.cs file, the handler for the **LoadedPivotItem** event calls the **LoadData** method implemented in the ListViewModel.cs file, passing the name of the **PivotItem** control that has finished loading. (In the design of projects based on the Windows Phone SharePoint List Application template, the name of a given **PivotItem** control is set to be the same as the key value for the CAML query string for the view associated with that control in the **ViewXmls** **Dictionary** type defined in the **CamlQueryBuilder** class in ListViewModel.cs.)</span></span>
    
  
3. <span data-ttu-id="5e4b4-130">С помощью метода **LoadData** в ListViewModel.cs вызывает метод **LoadData** в файле ListDataProvider.cs.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-130">The **LoadData** method in ListViewModel.cs calls the **LoadData** method implemented in the ListDataProvider.cs file.</span></span>
    
  
4. <span data-ttu-id="5e4b4-p107">Метод **LoadData** в ListDataProvider.cs вызывает метод **LoadDataFromServer**, также реализована в тот же файл. Метод **LoadDataFromServer** затем выполняет следующее.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p107">The **LoadData** method in ListDataProvider.cs calls the **LoadDataFromServer** method also implemented in that same file. The **LoadDataFromServer** method then does the following:</span></span>
    
1. <span data-ttu-id="5e4b4-133">Получает строку запроса CAML, связанный с заданным представлением.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-133">Gets the CAML query string associated with a given view.</span></span>
    
```cs
  
CamlQuery query = CamlQueryBuilder.GetCamlQuery(ViewName);
```

2. <span data-ttu-id="5e4b4-134">Регистрирует с помощью клиентского объекта модели списка нужно вернуть.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-134">Registers with the client object model the list to be retrieved.</span></span>
    
```cs
  ListItemCollection items = Context.Web.Lists.GetByTitle(ListTitle).GetItems(query);
```

3. <span data-ttu-id="5e4b4-135">Указывает клиентской объектной модели, он должен возвращать элементов списка и поля этих элементов списка (как текстовые значения).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-135">Indicates to the client object model that it should return the list items and the fields of those list items (as text values).</span></span>
    
```cs
  Context.Load(items);
Context.Load(items, listItems => listItems.Include(item => item.FieldValuesAsText));
```

4. <span data-ttu-id="5e4b4-136">Вызывает **ExecuteQueryAsync** для отправки запросов к SharePoint Server и извлечения данных (асинхронно).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-136">Calls **ExecuteQueryAsync** to send the requests to SharePoint Server and retrieve the data (asynchronously).</span></span>
    
  

  
    
    

## <a name="add-a-custom-list-view-query-and-corresponding-ui-elements"></a><span data-ttu-id="5e4b4-137">Добавьте настраиваемый список представление запроса и соответствующего пользовательского интерфейса элементов</span><span class="sxs-lookup"><span data-stu-id="5e4b4-137">Add a custom list view query and corresponding UI elements</span></span>
<span data-ttu-id="5e4b4-138"><a name="BKMK_AddingCustomizations"> </a></span><span class="sxs-lookup"><span data-stu-id="5e4b4-138"><a name="BKMK_AddingCustomizations"> </a></span></span>

<span data-ttu-id="5e4b4-139">В проектах можно воспользоваться преимуществами направленной на уровне данных предназначена для добавления собственных настраиваемых строк запроса CAML и представлений списка.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-139">In your own projects, you can take advantage of the way the data layer is designed to add your own custom CAML query strings and list views.</span></span>
  
    
    
<span data-ttu-id="5e4b4-140">В следующем примере кода предполагается еще раз конечного установленного сервера SharePoint Server на наличие список заказов на продукт, созданный шаблон настраиваемого списка, настроенных с полями и типы, указанные в таблице 1 в разделе [как для: реализация бизнес-логики и проверка данных в приложении Windows Phone для SharePoint](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-140">For the following code sample, assume again that the target installation of SharePoint Server has a Product Orders list created from the Custom List template, configured with the fields and types indicated in Table 1 in the topic  [How to: Implement business logic and data validation in a Windows Phone app for SharePoint](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md).</span></span> <span data-ttu-id="5e4b4-141">Создание проекта на основе шаблона приложения списка SharePoint для Windows Phone, которое использует список как список заказов на продукт в качестве источника (как описано в статье [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md)).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-141">Create a project based on the Windows Phone SharePoint List Application template that uses a list like the Product Orders list as a source (as described in  [How to: Create a Windows Phone SharePoint list app](how-to-create-a-windows-phone-sharepoint-list-app.md)).</span></span> <span data-ttu-id="5e4b4-142">В целях в этом примере мы Добавьте настраиваемое представление приложения Windows Phone (не в список на server.md), отфильтрованную для отображения заказы продукта, в которых количество упорядоченные 100 или более.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-142">For the purposes of this example, we add a custom view to the Windows Phone app (not to the list on the server.md) that is filtered to display only those product orders in which the quantity ordered is 100 or more.</span></span>
  
    
    

### <a name="to-add-a-custom-query-and-view"></a><span data-ttu-id="5e4b4-143">Добавление пользовательских запросов и представлений</span><span class="sxs-lookup"><span data-stu-id="5e4b4-143">To add a custom query and view</span></span>


1. <span data-ttu-id="5e4b4-144">В **Обозревателе решений** дважды щелкните файл ListDataProvider.cs (или выберите файл и нажмите кнопкуF7) для открытия файла для редактирования.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-144">In **Solution Explorer**, double-click the ListDataProvider.cs file (or choose the file and press F7) to open the file for editing.</span></span>
    
  
2. <span data-ttu-id="5e4b4-145">Обновление определения типа **Dictionary** **ViewXmls**в классе статический **CamlQueryBuilder** для включения дополнительных запросов CAML (en), с предложением WHERE, указав соответствующий условия фильтрации.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-145">Update the definition of the **ViewXmls** **Dictionary** type in the static **CamlQueryBuilder** class to include an additional CAML query, with a WHERE clause stipulating the appropriate filtering condition.</span></span>
    
```cs
  
static Dictionary<string, string> ViewXmls = new Dictionary<string, string>()
{   
    {"View1",   @"<View><Query><OrderBy><FieldRef Name='ID'/>
        </OrderBy></Query><RowLimit>30</RowLimit><ViewFields>{0}</ViewFields></View>"},
    {"View2",   @"<View><Query><OrderBy><FieldRef Name='ID' /></OrderBy>
     <Where><Geq><FieldRef Name='Quantity' />
          <ValueType='Number'>100</Value>
                </Geq></Where>
             </Query><RowLimit>30</RowLimit>
               <ViewFields>{0}</ViewFields></View>"}
};
```

3. <span data-ttu-id="5e4b4-146">Дважды щелкните файл List.xaml, чтобы открыть файл для редактирования.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-146">Double-click the List.xaml file to open the file for editing.</span></span>
    
  
4. <span data-ttu-id="5e4b4-p109">Добавьте разметку, чтобы определить дополнительные дочернего **PivotItem** элемента управления в элементе управления основной **Pivot**. Элемент **Grid**, объявленные элементы пользовательского интерфейса, которые определяют страницы основного приложения должен иметь следующий код:</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p109">Add markup to define an additional child **PivotItem** control within the main **Pivot** control. The **Grid** element in which the UI elements that define the main application page are declared should resemble the following code.</span></span>
    
```XML
  
<Grid x:Name="LayoutRoot" Background="Transparent"
 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" 
 xmlns:controls="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone.Controls">
    <!--Pivot Control-->
    <ProgressBar x:Name="progressBar" Opacity="1" HorizontalAlignment="Center" 
     VerticalAlignment="Top" Height="30" Width="470" IsIndeterminate="{Binding IsBusy}" 
     Visibility="{Binding ShowIfBusy}" />
    <Grid x:Name="ContentPanel" Grid.Row="0" Width="470">
        <controls:Pivot Name="Views" Title="Product Orders" LoadedPivotItem="OnPivotItemLoaded">
            <!--Pivot item-->
            <controls:PivotItem Name="View1" Header="All Items">
                <!--Double line list with text wrapping-->
                <ListBox x:Name="lstBox1" Margin="0,0,-12,0" SelectionChanged="OnSelectionChanged" 
                 ItemsSource="{Binding [View1]}">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <StackPanel Orientation="Vertical" Margin="10">
                                <TextBlock Name="txtTitle" Text="{Binding [Title]}" 
                                 TextWrapping="NoWrap" Style="{StaticResource PhoneTextTitle2Style}" />
                                <TextBlock Name="txtDescription" Text="{Binding [Description]}" 
                                 TextWrapping="NoWrap" Style="{StaticResource PhoneTextNormalStyle}" />
                                <TextBlock Name="txtQuantity" Text="{Binding [Quantity]}" 
                                 TextWrapping="NoWrap" Style="{StaticResource PhoneTextNormalStyle}" />
                            </StackPanel>
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>                    
            </controls:PivotItem>
            
            <!--Added PivotItem control for customized view--><controls:PivotItem Name="View2" Header="Big Orders"><!--Double line list with text wrapping--><ListBox x:Name="lstBox2" Margin="0,0,-12,0" 
                 SelectionChanged="OnSelectionChanged" ItemsSource="{Binding [View2]}"><ListBox.ItemTemplate><DataTemplate><StackPanel Orientation="Vertical" Margin="10"><TextBlock Name="txtTitle" Text="{Binding [Title]}" 
                                 TextWrapping="NoWrap" Style="{StaticResource PhoneTextTitle2Style}" /><TextBlock Name="txtDescription" Text="{Binding [Description]}" 
                                 TextWrapping="NoWrap" Style="{StaticResource PhoneTextNormalStyle}" /><TextBlock Name="txtQuantity" Text="{Binding [Quantity]}" 
                                 TextWrapping="NoWrap" Style="{StaticResource PhoneTextNormalStyle}" /></StackPanel></DataTemplate></ListBox.ItemTemplate></ListBox></controls:PivotItem>

        </controls:Pivot>
    </Grid>
</Grid>
```


    > **Note:**
      >  In particular that the value of the **Name** attribute ("View2") of the **PivotItem** control is the same as the key value of the entry added to the **Dictionary** type defined in step 2. This value is used to identify the appropriate CAML query to use to retrieve the data to be displayed in the **PivotItem**. Also note that the **ListBox** declared here (named "lstBox2" simply to distinguish it from the **ListBox** for the default view) is also bound to the view.

    
    
  
<span data-ttu-id="5e4b4-p110">При запуске проекта (нажатием клавиши F5), элемент управления **Pivot** для приложения включает два элемента управления **PivotItem** и данные, извлекаемые запросы CAML, связанные с соответствующими представлениями. Просмотр всех элементов по умолчанию отображаются все заказы, как показано на рисунке 1 (с образцами данных).</span><span class="sxs-lookup"><span data-stu-id="5e4b4-p110">When you start your project (by pressing F5), the **Pivot** control for the app includes the two **PivotItem** controls and the data retrieved by the CAML queries associated with their respective views. The default All Items view displays all the orders, as shown in Figure 1 (with sample data).</span></span>
  
    
    

<span data-ttu-id="5e4b4-151">**На рисунке 1. Все заказы (элементы списка) в примере списка**</span><span class="sxs-lookup"><span data-stu-id="5e4b4-151">**Figure 1. All orders (list items) in a sample list**</span></span>

  
    
    

  
    
    
![Все заказы (элементы списка) в примере списка](../images/e9cf225a-7040-4545-8db2-9e6f04e7a6eb.gif)
  
    
    
<span data-ttu-id="5e4b4-153">И настраиваемое представление, определенных в предыдущей процедуре, отображается список отфильтрованных элементов, который включает в себя только те заказы, для которых количество 100 или более указывается, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-153">And the custom view, as defined in the preceding procedure, displays a filtered list of items that includes only those orders for which a quantity of 100 or more is specified, as shown in Figure 2.</span></span>
  
    
    

<span data-ttu-id="5e4b4-154">**На рисунке 2. Только крупные заказы**</span><span class="sxs-lookup"><span data-stu-id="5e4b4-154">**Figure 2. Only the big orders**</span></span>

  
    
    

  
    
    
![Только большие заказы](../images/0d28b4f9-7f81-47c0-976e-247c2b9544d4.gif)
  
    
    
<span data-ttu-id="5e4b4-156">Многие другие настройки можно сделать для запросы CAML, на которых основаны представлений и элементы пользовательского интерфейса, связанные с представлениями.</span><span class="sxs-lookup"><span data-stu-id="5e4b4-156">You can make many other customizations both to the CAML queries on which views are based and to the UI elements associated with views.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="5e4b4-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5e4b4-157">Additional resources</span></span>
<span data-ttu-id="5e4b4-158"><a name="SP15Custlistitem_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5e4b4-158"></span></span>


-  [<span data-ttu-id="5e4b4-159">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="5e4b4-159">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="5e4b4-160">Введение в Collaborative Application Markup Language (CAML)</span><span class="sxs-lookup"><span data-stu-id="5e4b4-160">Introduction to Collaborative Application Markup Language (CAML)</span></span>](http://msdn.microsoft.com/en-us/library/ms426449.aspx)
    
  
-  [<span data-ttu-id="5e4b4-161">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="5e4b4-161">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="5e4b4-162">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="5e4b4-162">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="5e4b4-163">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="5e4b4-163">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="5e4b4-164">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="5e4b4-164">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="5e4b4-165">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="5e4b4-165">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

