---
title: "Описывается поддержка и преобразования типов поля SharePoint для приложений Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 301e6e58-5153-4ca9-a419-8ae0535ebbed
ms.openlocfilehash: 50e7405ed9390000f3152dfd06c3103b1b42d037
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-support-and-convert-sharepoint-field-types-for-windows-phone-apps"></a>Как: поддержка и convert SharePoint поля типов приложений Windows Phone
Реализуйте логику преобразования данных для поддержки типов полей SharePoint в приложениях Windows Phone. В проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone данные множество типов поля SharePoint обрабатываются и координированное логикой преобразования по умолчанию для подходит для отображения и управление ими в пользовательском интерфейсе Silverlight Windows Phone, но разработчики также могут реализовать собственные пользовательские данные процедур обработки.
  
    
    


> **Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express. За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7. > Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md). 
  
    
    


## <a name="sharepoint-field-types-in-windows-phone-apps"></a>Типы полей SharePoint в приложениях Windows Phone
<a name="BKMK_SharePointFieldTypes"> </a>

Списки SharePoint обеспечить достаточный с поля данных (в виде столбцов), и данное поле предназначена для хранения данных определенного типа (то есть, данные структурированы определенным образом). Эти типы вызываются типов полей. (Такие типы называется также типы столбцов, так как при добавлении столбца к списку SharePoint добавляется столбец полей, связанного с типом данных.) Эти поля определены схемы XML. Схема для поля, называется «Дата заказа» с типом данных **DateTime** (представленные в виде поля даты и времени в пользовательском интерфейсе Microsoft SharePoint Server ) может выглядеть следующим образом.
  
    
    

```XML

<Field Type="DateTime" DisplayName="Order Date" Required="FALSE"
 EnforceUniqueValues="FALSE" Indexed="FALSE" Format="DateOnly"
 FriendlyDisplayFormat="Disabled" Name="Order_x0020_Date">
  <Default>[today]</Default>
  <DefaultFormulaValue>2012-01-10T00:00:00Z</DefaultFormulaValue>
</Field>
```

Обратите внимание, в частности значение атрибута **Type** элемента **Field** в этой схеме, указанный здесь в качестве даты-времени". Список полей, созданной для хранения данных структурирован другими способами может определенных **Type** значение, например, "Вариант" или "Text" или "Boolean".
  
    
    
Типов поля SharePoint не может быть связан непосредственно к элементам управления Silverlight в приложении Windows Phone. Данные как в списке SharePoint необходимо быть подготовлен или обработки определенным образом (или в Стандартные термины привязки данных Silverlight, преобразованы) для привязанных к элементам управления в приложении и этой подготовки и координация обрабатывается ViewModels в проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone. Проекты на основе этого шаблона предназначены для включения логику преобразования по умолчанию для поддержки привязки и отображение данных SharePoint в приложении Windows Phone для некоторых стандартных типов поля SharePoint (или для настраиваемых полей, основанного на один из следующих стандартных типов). В таблице 1 перечислены типы полей, поддерживающих логику преобразования по умолчанию.
  
    
    

**В таблице 1. Типы полей с подготавливает преобразования по умолчанию**


|**Тип поля SharePoint**|**Тип данных Silverlight**|
|:-----|:-----|
|Вложения  <br/> |Файл  <br/> |
|Логический  <br/> |Логический  <br/> |
|Вычисляется (только для отображения)  <br/> |String  <br/> |
|Варианты  <br/> |Строка  <br/> |
|Денежный  <br/> |Numeric  <br/> |
|DateTime  <br/> |Дата (представлено в соответствии с языковой стандарт по телефону)  <br/> |
|URL-адрес  <br/> |Ссылка  <br/> |
|Целое число  <br/> |Numeric  <br/> |
|Расположение  <br/> |GeoCoordinate  <br/> |
|Подстановка  <br/> |Строка  <br/> |
|MultiChoice  <br/> |Строка  <br/> |
|Примечание  <br/> |Строка  <br/> |
|Число  <br/> |Numeric  <br/> |
|OutcomeChoice  <br/> |Строка  <br/> |
|Рисунок  <br/> |Ссылка  <br/> |
|Text  <br/> |Строка  <br/> |
|User  <br/> |Строка  <br/> |
   
Других типов поля SharePoint, такие как поля **Guid**, можно использовать в приложениях Windows Phone, но разработчикам необходимо предоставить логику пользовательского преобразования для поддержки привязки и отображение значений для этих типов полей, для которых по умолчанию предоставляется логика преобразования. (См [Логика пользовательского преобразования для подготовки типы полей не поддерживается](#BKMK_ConversionForUnsupportedFields) в этой статье).
  
    
    
В качестве иллюстрации, как шаблон предоставляет преобразование по умолчанию и поддержка для определенных типов полей, предположим, SharePoint, список содержит столбец полей с именем "Категория продуктов" назначением с типом **Choice** и связанные с несколько параметров, таких как "Создать заново" и "Culinary". Схема для поля на сервере может напоминать следующую разметку.
  
    
    



```XML

<Field Type="Choice" DisplayName="Product Category" Required="FALSE"
 EnforceUniqueValues="FALSE" Indexed="FALSE" Format="Dropdown"
 FillInChoice="TRUE" 
 Name="Product_x0020_Category">
  <Default>Recreation</Default>
  <CHOICES>
    <CHOICE>Culinary</CHOICE>
    <CHOICE>Recreation</CHOICE>
    <CHOICE>Sartorial</CHOICE>
    <CHOICE>Travel</CHOICE>
    <CHOICE>Other</CHOICE>
  </CHOICES>
</Field>
```

В этом поле **Choice** имеет обработки для подходит для отображения в интерфейсе Windows Phone. В этом случае данные в поле представлены в виде строки (например, "создать заново") в коллекции строковых значений (в частности, по одному из значений свойства **FieldValuesAsText** объекта **ListItem** ). Логика преобразования для полей **Choice** извлекает такую строку для отображения в интерфейсе пользователя телефона. Строка может привязанных к и отображаемых в элементе управления **TextBlock** в форме. Если значение предоставляется для редактирования, логику преобразования по умолчанию для поля **Choice** извлекает доступные параметры для поля ("Кулинарных", "Создать заново", "Sartorial", и т.д.) из XML-схему, которая определяет поле и представляет эти доступные параметры семейства сайтов (в частности, как тип семейства сайтов на основе класса **ObservableCollection(T)** ) определенный параметр сами включают (например объектов "Кулинарных") и ли был выбран соответствующий параметр. Эти операции обрабатываются в ViewModel уровня приложения. На уровне представления (или презентации) (который в XAML-файле создается для формы изменения шаблона приложения списка SharePoint для Windows Phone) эти параметры отображаются по умолчанию как Silverlight **RadioButton** управления в элементе управления **ListBox**.
  
    
    

## <a name="custom-conversion-for-sharepoint-field-types"></a>Настраиваемое преобразование для типов поля SharePoint
<a name="BKMK_CustomConversion"> </a>

В Visual Studio проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone механизм обработки координации и преобразования данных между SharePoint и пользовательский интерфейс Windows Phone Silverlight разработан для гибкости и расширяемости.
  
    
    
В зависимости от целями разработки для конкретного приложения необходимо предоставить логику преобразования для поддержки привязки и отображение типов поля SharePoint, которые не предоставляются вместе с логику преобразования по умолчанию или воспользуйтесь для отображения данных для поля, поддерживаемые в результате которого отличается от реализации по умолчанию.
  
    
    
Проекты на основе шаблона приложения списка SharePoint для Windows Phone реализации класса статического **Converter**, который включает в себя процедуры для регистрации методов для обработки типов данных специально для данного операций преобразования данных. Проект включает в себя и регистрирует процедуры преобразования данных для определенных типов данных по умолчанию. Механизм регистрации использует делегатов для обеспечения расширяемости. Разработчиков (en) таким образом можно написать собственные функции, чтобы предоставить логику для преобразования данных, и эти пользовательские функции могут вызываться при вызове делегаты вместо функции по умолчанию. Чтобы упорядочить для пользовательских функций для вызова для операций преобразования данных, зарегистрируйте свои функции с классом **Converter**, с помощью методов регистрации класса. Регистрация методы выглядят специально для каждого ViewModel, чтобы учесть возможность того, что требуется реализовать и зарегистрировать различные функции для обработки данных по-разному в зависимости от того, например, будет ли данные будут представлены для редактирования или для просмотра только (без изменения).
  
    
    

> **Совет:** Символ валюты, приведенные в форме отображения — от языкового стандарта SharePoint даже в том случае, если языковой стандарт Windows Phone нет в списке. Разработчики могут настраивать это поведение с помощью **конвертера** объектов.
  
    
    

Чтобы зарегистрировать функции преобразования данных для отображения форм (DisplayForm.xaml), используйте метод **RegisterDisplayFieldValueConverter** класса **Converter**. Чтобы зарегистрировать функции для формы изменения (EditForm.xaml), используйте метод **RegisterEditFieldValueConverter** и новой формы (NewForm.xaml), используйте метод **RegisterNewFieldValueConverter**.
  
    
    
Можно регистрировать функции преобразования, которые обрабатывают данные, поступающие из списка отображаться в пользовательском интерфейсе (то есть функции, определяющие способ **получить** данные) и функции, которые обрабатывают данные из пользовательского интерфейса, как его сохраненные в список на сервере можно регистрировать (функции, определяющие как **набор** данных).
  
    
    
**Получите** функции должно соответствовать подписи следующее объявление делегата в классе **Converter**.
  
    
    



```cs

public delegate object GetConvertedFieldValue(string fieldName,
  ListItem item, ConversionContext context);
```

**Настройка** функции должно соответствовать подписи следующее объявление делегата.
  
    
    



```cs

public delegate void SetConvertedFieldValue(string fieldName,
  object fieldValue, ListItem item, ConversionContext context);
```

Метод **RegisterDisplayFieldValueConverter** принимает только, функция **get**, так как класс **DisplayItemViewModel**, замыслу, предназначенного для отображения, но не изменять данные. **RegisterEditFieldValueConverter**, а также методы **RegisterNewFieldValueConverter** перегрузки для принятия функции **получить** и **задать** функции.
  
    
    
В [как: реализация бизнес-логики и данных проверок в приложении Windows Phone для SharePoint](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md), процедуру проверки был разработан для проверки формата или номерам телефонов, пользователем приложения Windows Phone. Чтобы продемонстрировать преобразование пользовательских данных, в следующем примере кода реализуется функции **получения** и **задания** для обработки данных номеров телефонов определенным образом и зарегистрировать эти функции для использования в формах редактирования и создания с **конвертера **класса.
  
    
    
Предположим, для целей в следующем примере кода, было ли создано приложение Windows Phone SharePoint списка, на основе списка заказов на продукт создан на основе шаблона настраиваемого списка на сервере. Предполагается, что список содержит поле с именем «Номер контакта» и, что это поле используется в качестве поля **Text** в списке. В конфигурации по умолчанию в качестве типа **Text** на SharePoint Server поле списка пользователь может ввести любые текстовых символов (не более 255 знаков). Шаблон предоставляет логику преобразования по умолчанию для отображения и редактирования данных из **Text** полей в SharePoint, но поле **Text** (по умолчанию) имеет структуру для применяться или отображение определенных форматирования, например, может быть традиционно применена к телефонных номеров. В приложении Windows Phone можно номера телефонов для отображения для пользователей в едином виде и, при сохранении в список на сервере, отформатированные определенным образом, даже если базовый тип поля ( **Text**) не связан с определенным правила форматирования. Для применения определенного правила форматирования, можно реализовать собственную логику преобразования пользовательских данных вместо логики по умолчанию для типа поддерживаемые поля.
  
    
    

### <a name="to-implement-custom-data-conversion"></a>Чтобы реализовать преобразование пользовательских данных


1. Если предположить, создания списка на сервере SharePoint Server, который включает в себя **текстовое** поле с именем «Номер контакта» (как образца списка заказов на продукт, используемые в [как: реализация бизнес-логики и данных проверок в приложении Windows Phone для SharePoint](how-to-implement-business-logic-and-data-validation-in-a-windows-phone-app-for-s.md)), Создание приложения Windows Phone на основе шаблона приложения списка SharePoint для Windows Phone в Visual Studio, выполнив действия, описанные в [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md).
    
  
2. В **Обозревателе решений** выберите узел, представляющий проект (с именем, например,ContosoSPListApp).
    
  
3. В меню **проект** в Visual Studio (или Visual Studio Express для Windows Phone) выберите пункт **Добавить класс**. Откроется диалоговое окно **Добавление нового элемента** с помощью C# **класс** шаблона уже.
    
  
4. Укажите имя для файла класса (например, ContosoConverter.cs) и нажмите кнопку **Добавить**. Файл класса будет добавлен в проект и открыт для редактирования.
    
  
5. Замените содержимое файла следующим кодом.
    
```cs
  
using System;
using Microsoft.SharePoint.Client;  // Added for ListItem.
using Microsoft.SharePoint.Phone.Application; // Added for ConversionContext.
using System.Text.RegularExpressions;

// Specify a namespace appropriate for your particular project.
namespace ContosoSPListApp
{
    public static class ContosoConverter
    {
        static Regex StandardNumberFormat = 
          new Regex(@"^\\(?([0-9]{3})\\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$", RegexOptions.Compiled);

        public static object GetConvertedTextFieldValue(string fieldName, 
          ListItem item, ConversionContext context)
        {
            if (item == null) return null;

            if (fieldName == "Contact_x0020_Number")
            {
                string contactNumber = string.Empty;
                try
                {
                    contactNumber = item.FieldValuesAsText[fieldName];
                }
                catch (PropertyOrFieldNotInitializedException)
                {
                    object itemValue = item[fieldName];
                    if (itemValue != null)
                    {
                        contactNumber = itemValue.ToString();
                    }
                }

                // Regularize the formatting of phone number for display in UI.
                if (StandardNumberFormat.IsMatch(contactNumber))
                {
                    // Phone number is in an acceptable format, but formatting it
                    // in a specific way for visual consistency in the UI.
                    string properlyFormattedNumber = 
                      StandardNumberFormat.Replace(contactNumber, "($1) $2-$3");
                    return properlyFormattedNumber;
                }
                else
                {
                    // Return a representation of the data adorned in such a way 
                    // as to designate its invalidity.
                    if (!contactNumber.Contains("Invalid Number"))
                    {
                        return string.Format("Invalid Number: {0}", contactNumber);
                    }
                    else
                    {
                        // Assume data is already adorned with an invalidity designation.
                        return contactNumber;
                    }
                }
            }
            else
            {
                return item[fieldName];
            }
        }

        public static void SetConvertedTextFieldValue(string fieldName, 
                             object fieldValue, ListItem item, ConversionContext context)
        {
            if (fieldValue == null) return;

            if (fieldName == "Contact_x0020_Number")
            {
                // Conventional formats (e.g., 555-555-5555) are acceptable,
                // but formatting phone numbers consistently here for storage in list on Server.
                string contactNumber = (string)fieldValue;

                if (StandardNumberFormat.IsMatch(contactNumber))
                {
                    string properlyFormattedNumber = StandardNumberFormat.Replace
                                                               (contactNumber, "($1) $2-$3");
                    item[fieldName] = properlyFormattedNumber;
                }
                else
                {
                    if (!contactNumber.Contains("Invalid Number"))
                    {
                        item[fieldName] = string.Format("Invalid Number: {0}", contactNumber);
                    }
                    else
                    {
                        // Assume data is already adorned with an invalidity designation.
                        item[fieldName] = contactNumber;
                    }                    
                }
            }
            else
            {
                // Allow values for other Text fields to be passed on to list without modification.
                item[fieldName] = fieldValue;                
            }
        }
    }
}
```

6. Сохраните файл.
    
  
Функцию **GetConvertedTextFieldValue** определяет, будет ли строка данные из поля предназначен для хранения номера телефона (с именем "Номер контакта" в данном примере) отформатированное в соответствии с стандартным соглашениям для телефонных номеров (в Северной Америке) и, если да, преобразует это число в определенный формат для отображения "(XXX) XXX-XXXX". Если данные не отформатировано как номер телефона standard, оно указывается обозначение. Эта функция не фактически изменение данных в списке. Функция **SetConvertedTextFieldValue**, с другой стороны, переходит в обратном направлении. Проверяет значение данных, предоставленных пользователю определить, соответствует ли введенные данные шаблон для стандартных телефонных номеров для поля. Если это так, предоставленное значение преобразуется в определенный формат будет сохранен в список на сервере. Если указанное значение не стандартного формата, обозначение указывается значение и затем  с префиксом значение сохранены на сервере.
  
    
    
Теперь остается зарегистрировать эти функции преобразования данных с помощью класса **конвертера** для использования в формах редактирования и создания. Конвертеры можно зарегистрировать в нескольких местах. В следующей процедуре конвертеры, регистрируются в событии **OnNavigatedTo** формы списка (List.xaml). Форма списка создается и переход, прежде чем редактирования и создания форм создаются в приложении, поэтому конвертеры, зарегистрированные в это событие в виде списка вступят в силу для текстовых полей в формах.
  
    
    

### <a name="to-register-the-data-conversion-functions"></a>Для регистрации функции преобразования данных


1. В **Окне Обозреватель решений** для одного проекта, в котором вы создали класс в предыдущей процедуре выберите файл List.xaml в разделе узел **представления**.
    
  
2. КлавишиF7Чтобы открыть файл выделенным кодом List.xaml.cs, для редактирования.
    
  
3. Добавьте следующее объявление переменной закрытого в верхнюю часть блока кода, который реализует разделяемый класс **ListForm** после открывающей скобки в блоке кода и перед конструктором `ListForm()` .
    
```cs
  
private bool _isConversionRegistered;
```

4. Добавьте следующий метод **RegisterTextFieldValueConverters**в файл в блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **ListForm**.
    
```cs
  private void RegisterTextFieldValueConverters()
{
    Converter.RegisterEditFieldValueConverter(FieldType.Text, 
                      ContosoConverter.GetConvertedTextFieldValue, 
                        ContosoConverter.SetConvertedTextFieldValue);

    Converter.RegisterNewFieldValueConverter(FieldType.Text, 
                          ContosoConverter.GetConvertedTextFieldValue, 
                          ContosoConverter.SetConvertedTextFieldValue);
}
```


    This method simply calls the appropriate registration methods of the **Converter** class. It is assumed for this code that the custom class containing the **get** and **set** functions created in the preceding procedure is named "ContosoConverter". If you specified a different name for your class, change the code here accordingly.
    
  
5. Измените реализации обработчика событий **OnNavigatedTo** в файле, добавив проверять на значение флага **_isConversionRegistered** и вызове функции **RegisterTextFieldValueConverters**, добавленные в предыдущем шаге. Измененные обработчик должен иметь следующий вид.
    
```cs
  
protected override void OnNavigatedTo(System.Windows.Navigation.NavigationEventArgs e)
{
    base.OnNavigatedTo(e);

    App.MainViewModel.ViewDataLoaded += 
      new EventHandler<ViewDataLoadedEventArgs>(OnViewDataLoaded);
    App.MainViewModel.InitializationCompleted += 
      new EventHandler<InitializationCompletedEventArgs>(OnViewModelInitialization);

    // The OnNavigatedTo event can fire more than once, but the converters only need
    // to be registered once, so checking the conversion flag first.
    if (_isConversionRegistered == false)
    {
        // Register converters.
        RegisterTextFieldValueConverters();
        _isConversionRegistered = true;
    }
}
```

6. Сохраните файл.
    
  
Обратите внимание на то, что функции преобразования данных регистрируются все поля, связанного с типом данных **Text** в формах редактирования и создания. Именно по этой причине, включение функции **получения** и **задания** реализации для **ContosoConverter** класс, созданный в предыдущей процедуре проверки условий для обработки данных для отдельного поля (с именем, в этом случае "Contact_x0020_Number"), позволяя данных "проходить через" для других полей **Text**.
  
    
    

## <a name="custom-conversion-logic-to-provision-unsupported-field-types"></a>Логика пользовательского преобразования для подготовки типы полей не поддерживается
<a name="BKMK_ConversionForUnsupportedFields"> </a>

Даже в том случае, если не предоставляет логику преобразования в вашем приложении для поля **Text**, такие поля можно по-прежнему отображения и редактирования. Предоставление собственную логику преобразования для полей, которые предоставляются вместе с логику преобразования по умолчанию уже дает большую степень контроль над форматом или структуры данных в этих полях Если логики по умолчанию не подходит для вашей целями разработки. Для полей и некоторые другие типы данных, как поля **Guid** логику преобразования не предоставляется по умолчанию, но если вы понимаете механизм (описано в предыдущем разделе), с помощью которого предоставляется логика преобразования для полей, это может быть довольно легко собственную логику преобразования для поддержки типов полей в свое приложение, которое не поддерживают логику по умолчанию для шаблона приложения списка SharePoint для Windows Phone.
  
    
    
Предположим, что вы создаете приложения Windows Phone, на основе списка SharePoint с именем идентификаторы продукта, которая содержит поле с типом данных **Guid**. В этом в следующем примере кода предполагается, что список имеет продукта (или заголовок) поле (типа **Text**) и поле идентификатора (из типа **Guid**).
  
    
    

> **Примечание:** Списки SharePoint с помощью полей **Guid** должен быть создан программным образом или из шаблона списка, включающего поля **Guid** .
  
    
    

В приложении Windows Phone создан на основе шаблона и на основе этого простого списка данные в поля **Guid** не отображается по умолчанию. (Вместо эти данные отображаются сообщения следующим образом: "Не конвертера для типа поля"Guid"не зарегистрирован.") В следующей процедуре будет включать логику преобразования для поддержки **Guid** поля для приложения Windows Phone. Добавьте класс, который содержит методы для регистрации конвертеров значение поля для отображения идентификаторов GUID и для создания новых значений GUID для добавлен список элементов.
  
    
    

### <a name="to-provide-conversion-logic-for-an-unsupported-field-type"></a>Чтобы предоставить логику преобразования для типа поля не поддерживается


1. В проект (с именем, например, SPListAppGuidConversion) из приложения списка SharePoint для Windows Phone и на основе списка идентификаторов продукта, упомянутого выше выберите узел, представляющий проект в **Обозревателе решений**.
    
  
2. В меню **Проект** выберите **Добавить класс**. Отобразится диалоговое окно **Добавление нового элемента** с выбранным шаблоном **Класс** C#.
    
  
3. Укажите GuidConversion.cs в качестве имени файла и нажмите кнопку **Добавить**. Добавлен в решение и открывается для редактирования файла класса
    
  
4. Замените содержимое файла следующим кодом.
    
```cs
  
using System;
using Microsoft.SharePoint.Phone.Application;
using Microsoft.SharePoint.Client;

namespace SPListAppGuidConversion
{
    public class GuidConversion
    {
        /// <summary>
        /// Registers a GET converter to prepare GUID values for display.
        /// </summary>
        static public void RegisterDisplayFieldGuidConverter()
        {
            // Register GET converter to display GUID values.
            Converter.RegisterDisplayFieldValueConverter(FieldType.Guid,
            getConvertedFieldValue: (string fieldName, ListItem item, ConversionContext context) =>
            {
                string guidValue = string.Empty;

                try
                {
                    guidValue = item.FieldValuesAsText[fieldName];
                }
                catch (PropertyOrFieldNotInitializedException)
                {
                    object itemValue = item[fieldName];
                    if (itemValue != null)
                    {
                        guidValue = itemValue.ToString();
                    }
                }

                if (string.IsNullOrWhiteSpace(guidValue))
                {
                    return string.Format("{{{0}}}", Guid.Empty);
                }
                else
                {
                    Guid g = new Guid();

                    if (Guid.TryParse(guidValue, out g))
                    {
                        guidValue = string.Format("{{{0}}}", g.ToString().ToUpper());
                        return guidValue;
                    }
                    else
                    {
                        return "Invalid Identifier (GUID)";
                    }
                }
            });
        }

        /// <summary>
        /// Registers GET and SET converters for GUID value of new (i.e., added) list items.
        /// </summary>
        public static void RegisterNewFieldGuidConverter()
        {
            Converter.RegisterNewFieldValueConverter(FieldType.Guid,
                getConvertedFieldValue: (string fieldName, ListItem item, 
                                 ConversionContext context) => Guid.NewGuid().ToString(),
                setConvertedFieldValue: (string fieldName, object fieldValue, 
                                ListItem item, ConversionContext context) =>
                {
                    if (fieldValue == null)
                    {
                        item[fieldName] = Guid.Empty.ToString();
                    }
                    else
                    {
                        item[fieldName] = fieldValue;
                    }
                });
        }
    }
}
```


    In this custom class, the **RegisterDisplayFieldValueConverter** and the **RegisterNewFieldValueConverter** methods of the **Converter** class are called using anonymous functions (defined by a statement lambda) to implement the **get** and **set** routines for the delegates required by the registration methods. The optional argument labels here (for example, "getConvertedFieldValue:") are included in this code only to clarify which delegates are defined.)
    
    This approach, involving lambda expressions, is an alternative to passing named functions as parameters to the converter registration functions, which was demonstrated in an earlier procedure described in this topic (in the section  [To register the data conversion functions](#BKMK_RegisterFunctions)).
    
  
5. Сохраните файл.
    
  
6. В **Обозревателе решений** выберите файл App.xaml.
    
  
7. КлавишиF7Чтобы открыть выделенным кодом файл App.xaml.cs, для редактирования.
    
  
8. Найдите реализации обработчика событий **Application_Launching** (который пуст в новый проект, созданный на основе шаблона приложения списка SharePoint для Windows Phone) и замените его следующим кодом.
    
```cs
  
private void Application_Launching(object sender, LaunchingEventArgs e)
{
    // Register converters for GUID fields. Converters can be
    // registered just once for the app.
    GuidConversion.RegisterDisplayFieldGuidConverter();
    GuidConversion.RegisterNewFieldGuidConverter();
}
```

9. Для логики конвертера для работы для новых элементов списка (то есть, чтобы создать GUID значения при добавлении элементов в список), необходимо убедиться, что поле идентификатора **NewItemViewModel** привязан к новой формы. Для этого можно путем добавления элемента управления скрытые **TextBlock** NewForm.xaml с объявлением **Binding**, для его свойства **Text** идентификатор поля. Элемент управления **TextBlock** можно добавить в контейнер **StackPanel** элемент управления, который включает в себя элемент управления **TextBox** для поля Название, как показано в следующем разделе разметку в файле NewForm.xaml.
    
```
  
...
    <Grid x:Name="LayoutRoot" Background="Transparent" 
         xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" 
                 xmlns:controls="clr-namespace:Microsoft.Phone.Controls;
                                      assembly=Microsoft.Phone.Controls">
        <StackPanel>
            <ProgressBar Background="Red" x:Name="progressBar" 
                  Opacity="1" HorizontalAlignment="Center" VerticalAlignment="Top" 
                                    Height="15" Width="470" IsIndeterminate="{Binding IsBusy}"
                                       Visibility="{Binding ShowIfBusy}" />
            <ScrollViewer HorizontalScrollBarVisibility="Auto" Height="700">
                <Grid x:Name="ContentPanel" Width="470">
                    <StackPanel Margin="0,5,0,5">
                        <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                            <TextBlock TextWrapping="Wrap" 
                           HorizontalAlignment="Left" Style="{StaticResource PhoneTextNormalStyle}">
                                        Title*</TextBlock>
                            <TextBox Style="{StaticResource TextValidationTemplate}" 
                              FontSize="{StaticResource PhoneFontSizeNormal}" Width="470" 
                                   HorizontalAlignment="Left" Name="txtTitle" Text="{Binding [Title], 
                                    Mode=TwoWay, ValidatesOnNotifyDataErrors=True, 
                                      NotifyOnValidationError=True}" TextWrapping="Wrap" />
                            <TextBlock Name="txtIdentifier" Text="{Binding [Identifier]}" Visibility="Collapsed"/>
                        </StackPanel>
                    </StackPanel>
                </Grid>
            </ScrollViewer>
        </StackPanel>
    </Grid>
...
```


    Save the file.
    
  
Если запустить проект и развертывание приложения в эмуляторе Windows Phone для ее выполнения данных в поле Идентификатор отображается в виде списка (List.xaml), если в соответствующее поле в список SharePoint содержит значение GUID. (См.)
  
    
    

**На рисунке 1. Отображение полей Guid**

  
    
    

  
    
    
![Отображение полей GUID](../images/eb20da0e-793f-43af-aa5e-67f85cdfa2df.gif)
  
    
    
В проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone элементов управления Silverlight может не добавлены в формы и привязанных к типы полей, которые не поддерживают логику преобразования по умолчанию в шаблоне. Для поля идентификаторы список идентификаторов продукта, используемый в предыдущей процедуре можно добавить разметку в файл DisplayForm.xaml, чтобы определить дополнительные элементы управления для отображения значений GUID, например управления **TextBlock** и **TextBox** в элементе управления **StackPanel**, который является самой **Grid** элемента управления пользовательского интерфейса. Разметка для элемента управления добавлены **StackPanel** может выглядеть следующим образом.
  
    
    



```

<StackPanel HorizontalAlignment="Left" Orientation="Horizontal"
                                             Margin="0,5,0,5">
    <TextBlock TextWrapping="Wrap" Width="150" HorizontalAlignment="Left" 
                      Style="{StaticResource PhoneTextNormalStyle}">Identifier:</TextBlock>
    <TextBlock Width="310" HorizontalAlignment="Left" Name="txtIdentifier" 
                 Text="{Binding [Identifier]}" TextWrapping="Wrap" Style="
                                           {StaticResource PhoneTextSubtleStyle}" />
</StackPanel>
```

Теперь в поле Идентификатор отображается в форме отображения, так и в виде списка.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Supportwinphone_addlresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

