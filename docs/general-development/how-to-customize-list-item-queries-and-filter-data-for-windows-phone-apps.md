---
title: "Настройка запросов на обработку элементов списков и фильтрация данных для приложений Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 32f89b97-8274-4cb0-9164-7898735a18aa
ms.openlocfilehash: 07e87f7dfef948adb11a13607fdabcb4cb0053a1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="customize-list-item-queries-and-filter-data-for-windows-phone-apps"></a>Настройка запросов на обработку элементов списков и фильтрация данных для приложений Windows Phone

Настройте запросы данных, на которых основаны представления в приложении Windows Phone. С помощью проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone разработчики могут использовать преимущества шаблона разработки, реализованных в шаблон, который позволяет им настроить компонентов на уровне данных для приложения Windows Phone. Представление списка SharePoint в приложении Windows Phone можно настраивать в Microsoft SharePoint Server и включенных в приложение на телефоне или можно создать настраиваемое представление для приложения.
  
    
    


> **Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express. За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7. > Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md). 
  
    
    


## <a name="configure-list-views-on-the-server-for-use-in-windows-phone-apps"></a>Настройка представлений списка на сервере для использования в приложениях Windows Phone
<a name="BKMK_ConfiguringLists"> </a>

При создании приложения списка SharePoint для Windows Phone с использованием шаблона приложения списка SharePoint для Windows Phone, можно включить в свое приложение все существующие представления, которые связаны с целевого списка SharePoint. Одним из способов для фильтрации элементов в списке SharePoint как список будет отображаться на телефоне, затем, является настройка отфильтрованные представления для списка на сервере, а затем выберите нужное должны быть включены в приложении Windows Phone. Мастер шаблона приложения списка SharePoint для Windows Phone создает запрос Язык CAML для выбранного представления, которая включает в себя условия фильтрации, настроенных для представления на сервере. Возможно например, имеется список на сервере, на основе шаблона списка задач. Можно создать представления для списка, с именем «Праздников стороны», которая включает в себя только элементы, связанные с, например, Планирование праздников у компании пользователя, добавив условия фильтра для отображения элементов списка, только если в поле Описание содержит слова «праздников» или «субъект». В приложении Windows Phone разметки CAML, созданных для представления будет выглядеть следующим образом (в зависимости от поля, выбранные для включения в свое приложение).
  
    
    

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

Как и в другие существующие представления для списка задач, которое нужно включить в свое приложение Windows Phone, при создании проекта **PivotItem** управления, соответствующий выбранного представления добавляется элемент управления **Pivot**, который представляет элемент основного пользовательского интерфейса (UI) в приложении.
  
    
    

## <a name="customize-list-view-queries-in-the-windows-phone-app"></a>Настройка запросов представления списка в приложении Windows Phone
<a name="BKMK_CustomizingLists"> </a>

Для той или иной причине может быть невозможно или разумные для настройки представления, в которых не отвечает вашим требованиям проектирования для заданного списка на сервере. В проекте Microsoft Visual Studio, созданных на основе шаблона приложения списка SharePoint для Windows Phone аспекты называемых уровень данных становятся доступными для разработчиков (en), в основном через файл ListDataProvider.cs в проекте. Можно изменить CAML, определенных для существующего представления, или можно добавить запросы CAML для новых представлений в файле ListDataProvider.cs.
  
    
    

### <a name="the-listdataprovidercs-file"></a>Файл ListDataProvider.cs

В проекте на основе шаблона приложения списка SharePoint для Windows Phone файл ListDataProvider.cs определяет объекты, которые обеспечивают доступ к и настройки списка SharePoint в качестве источника данных для представлений в приложении Windows Phone. В файл List.xaml, который определяет страницу основного приложения для приложения, элемент управления **Pivot** (непосредственно содержащий **PivotItem** дочерних элементов управления) объявлен с обработчиком событий, назначенные к событию **LoadedPivotItem**. Метод **LoadDataFromServer** в файле ListDataProvider.cs в конечном счете вызывается при загрузке элемента управления **PivotItem** (который используется в качестве контейнера отображения для элементов списка в приложении Windows Phone) на странице главному приложению приложения.
  
    
    

1. **PivotItem**, связанный с представлением списка загружается в пользовательском Интерфейсе.
    
  
2. В файле List.xaml.cs обработчик для события **LoadedPivotItem** вызывает метод **LoadData** в файле ListViewModel.cs, передав имя элемента управления **PivotItem**, после завершения загрузки. (В разработки проектов на основе шаблона приложения списка SharePoint для Windows Phone, имя элемента управления данного **PivotItem** имеет значение же значение ключа для строки запроса CAML для представления, связанного с этим элементом управления в типе **Dictionary** **ViewXmls**, определенном в классе **CamlQueryBuilder** в ListViewModel.cs).
    
  
3. С помощью метода **LoadData** в ListViewModel.cs вызывает метод **LoadData** в файле ListDataProvider.cs.
    
  
4. Метод **LoadData** в ListDataProvider.cs вызывает метод **LoadDataFromServer**, также реализована в тот же файл. Метод **LoadDataFromServer** затем выполняет следующее.
    
1. Получает строку запроса CAML, связанный с заданным представлением.
    
```cs
  
CamlQuery query = CamlQueryBuilder.GetCamlQuery(ViewName);
```

2. Регистрирует с помощью клиентского объекта модели списка нужно вернуть.
    
```cs
  ListItemCollection items = Context.Web.Lists.GetByTitle(ListTitle).GetItems(query);
```

3. Указывает клиентской объектной модели, он должен возвращать элементов списка и поля этих элементов списка (как текстовые значения).
    
```cs
  Context.Load(items);
Context.Load(items, listItems => listItems.Include(item => item.FieldValuesAsText));
```

4. Вызывает **ExecuteQueryAsync** для отправки запросов к SharePoint Server и извлечения данных (асинхронно).
    
  

  
    
    

## <a name="add-a-custom-list-view-query-and-corresponding-ui-elements"></a>Добавьте настраиваемый список представление запроса и соответствующего пользовательского интерфейса элементов
<a name="BKMK_AddingCustomizations"> </a>

В проектах можно воспользоваться преимуществами направленной на уровне данных предназначена для добавления собственных настраиваемых строк запроса CAML и представлений списка.
  
    
    
В следующем примере кода предполагается еще раз конечного установленного сервера SharePoint Server на наличие список заказов на продукт, созданный шаблон настраиваемого списка, настроенных с полями и типы, указанные в таблице 1 в разделе [как для: реализация бизнес-логики и проверка данных в приложении Windows Phone для SharePoint](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md). Создание проекта на основе шаблона приложения списка SharePoint для Windows Phone, которое использует список как список заказов на продукт в качестве источника (как описано в статье [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md)). В целях в этом примере мы Добавьте настраиваемое представление приложения Windows Phone (не в список на server.md), отфильтрованную для отображения заказы продукта, в которых количество упорядоченные 100 или более.
  
    
    

### <a name="to-add-a-custom-query-and-view"></a>Добавление пользовательских запросов и представлений


1. В **Обозревателе решений** дважды щелкните файл ListDataProvider.cs (или выберите файл и нажмите кнопкуF7) для открытия файла для редактирования.
    
  
2. Обновление определения типа **Dictionary** **ViewXmls**в классе статический **CamlQueryBuilder** для включения дополнительных запросов CAML (en), с предложением WHERE, указав соответствующий условия фильтрации.
    
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

3. Дважды щелкните файл List.xaml, чтобы открыть файл для редактирования.
    
  
4. Добавьте разметку, чтобы определить дополнительные дочернего **PivotItem** элемента управления в элементе управления основной **Pivot**. Элемент **Grid**, объявленные элементы пользовательского интерфейса, которые определяют страницы основного приложения должен иметь следующий код:
    
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


    > [!NOTE]
    > In particular that the value of the **Name** attribute ("View2") of the **PivotItem** control is the same as the key value of the entry added to the **Dictionary** type defined in step 2. This value is used to identify the appropriate CAML query to use to retrieve the data to be displayed in the **PivotItem**. Also note that the **ListBox** declared here (named "lstBox2" simply to distinguish it from the **ListBox** for the default view) is also bound to the view.

    
    
  
При запуске проекта (нажатием клавиши F5), элемент управления **Pivot** для приложения включает два элемента управления **PivotItem** и данные, извлекаемые запросы CAML, связанные с соответствующими представлениями. Просмотр всех элементов по умолчанию отображаются все заказы, как показано на рисунке 1 (с образцами данных).
  
    
    

**На рисунке 1. Все заказы (элементы списка) в примере списка**

  
    
    

  
    
    
![Все заказы (элементы списка) в примере списка](../images/e9cf225a-7040-4545-8db2-9e6f04e7a6eb.gif)
  
    
    
И настраиваемое представление, определенных в предыдущей процедуре, отображается список отфильтрованных элементов, который включает в себя только те заказы, для которых количество 100 или более указывается, как показано на рисунке 2.
  
    
    

**На рисунке 2. Только крупные заказы**

  
    
    

  
    
    
![Только большие заказы](../images/0d28b4f9-7f81-47c0-976e-247c2b9544d4.gif)
  
    
    
Многие другие настройки можно сделать для запросы CAML, на которых основаны представлений и элементы пользовательского интерфейса, связанные с представлениями.
  
    
    

## <a name="see-also"></a>См. также
<a name="SP15Custlistitem_addlresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Введение в Collaborative Application Markup Language (CAML)](http://msdn.microsoft.com/en-us/library/ms426449.aspx)
    
  
-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

