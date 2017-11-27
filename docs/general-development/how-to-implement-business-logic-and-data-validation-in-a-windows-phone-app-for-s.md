---
title: "Реализация бизнес-логики и данных проверок в приложении Windows Phone для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fbbedc38-9651-4cd6-b523-d93cbf1cd39d
ms.openlocfilehash: 1d122bef142048a6175d3e6c6a9a83bb34f702be
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="implement-business-logic-and-data-validation-in-a-windows-phone-app-for-sharepoint"></a><span data-ttu-id="18431-102">Реализация бизнес-логики и данных проверок в приложении Windows Phone для SharePoint</span><span class="sxs-lookup"><span data-stu-id="18431-102">Implement business logic and data validation in a Windows Phone app for SharePoint</span></span>

<span data-ttu-id="18431-p101">Реализуйте проверку данных в приложении Windows Phone, созданном с помощью шаблона приложения списка SharePoint для Windows Phone. В приложении Windows Phone, предназначенного для рабочей среды, скорее всего, потребуется проверить данные, введенные пользователями для, например, для применения бизнес-логики, предназначенных для вашей конкретной ситуации для обеспечения соответствующий формат значений, введенных или просто для перехвата ошибок перед сохранением значения в список SharePoint. Проекты на основе шаблона приложения списка SharePoint для Windows Phone содержат логику проверки данных по умолчанию, но таких проектов также предоставляют механизм для разработчиков для реализации проверки пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="18431-p101">Implement data validation in a Windows Phone app created by using the Windows Phone SharePoint List Application template. In a Windows Phone app intended for production use, you likely need to validate data entered by users to, for example, enforce business logic relevant to your particular circumstances, or to ensure appropriate formatting of entered values, or simply to catch mistakes before saving values to a SharePoint list. Projects based on the Windows Phone SharePoint List Application template include default data validation logic, but such projects also provide a mechanism for developers to implement custom data validation.</span></span>
  
    
    


> <span data-ttu-id="18431-106">**Важные:** При разработке приложения для Windows Phone 8, должны использовать Visual Studio Express 2012 г., а не в Visual Studio 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="18431-106">**Important:** If you are developing an app for Windows Phone 8, you must use Visual Studio Express 2012 instead of Visual Studio 2010 Express.</span></span> <span data-ttu-id="18431-107">За исключением среды разработки все сведения в этой статье применимы к созданию приложений для Windows Phone 8 и Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="18431-107">Except for the development environment, all information in this article applies to creating apps for both Windows Phone 8 and Windows Phone 7.</span></span> <span data-ttu-id="18431-108">> Для получения дополнительных сведений см [как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="18431-108">> For more information, see  [How to: Set up an environment for developing mobile apps for SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md).</span></span> 
  
    
    


## <a name="default-data-validation-rules"></a><span data-ttu-id="18431-109">Правила проверки данных по умолчанию</span><span class="sxs-lookup"><span data-stu-id="18431-109">Default data validation rules</span></span>
<span data-ttu-id="18431-110"><a name="BKMK_DefaultValidation"> </a></span><span class="sxs-lookup"><span data-stu-id="18431-110"><a name="BKMK_DefaultValidation"> </a></span></span>

<span data-ttu-id="18431-p103">По умолчанию с помощью простого форматирования или выполнить проверку данных связаны некоторые типы данных для полей в списках SharePoint. Если вводится недопустимый URL-адрес для поля, по полю гиперссылки и рисунки, введите в списке SharePoint и пытается сохранить изменения, появится сообщение о том, что введенный адрес является недопустимым. Если ввести имя клиента в качестве значения для поля даты и времени тип поля, появится сообщение с указанием введите дату в допустимый диапазон для поля.</span><span class="sxs-lookup"><span data-stu-id="18431-p103">Some data types for fields in SharePoint lists are associated by default with simple formatting or data validation. If you enter an invalid URL for a field based on the Hyperlink or Picture field type in a SharePoint list and attempt to save your changes, you see a message indicating that the address you entered is invalid. If you enter a customer name as a value for a field based on the Date and Time field type, you receive a message directing you to enter a date within a valid range for the field.</span></span>
  
    
    

> <span data-ttu-id="18431-114">**Примечание:** Проверка ввода даты — по отношению к SharePoint формат даты.</span><span class="sxs-lookup"><span data-stu-id="18431-114">**Note:** Date input validation is with respect to SharePoint date format.</span></span> <span data-ttu-id="18431-115">При необходимости в формате языкового телефона, Настройка поля и добавьте проверки соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="18431-115">If the date format of the phone locale is required, customize the field and add validations accordingly.</span></span> 
  
    
    

<span data-ttu-id="18431-p105">Некоторые из этих основных правил проверки также применяется по умолчанию в приложении Windows Phone, созданных на основе шаблона приложения списка SharePoint для Windows Phone. При вводе отличное от значения даты в поля, привязанного к полю SharePoint тип даты и времени в форме редактирования приложении Windows Phone на основе списка SharePoint, появится сообщение об ошибке проверки при изменении фокуса из элемента управления **TextBox**, связанного с полем. (См.)</span><span class="sxs-lookup"><span data-stu-id="18431-p105">Some of these basic validation rules are also enforced by default in a Windows Phone app created from the Windows Phone SharePoint List Application template. If you enter anything other than a date value in a field that is bound to a SharePoint field of Date and Time type in the Edit form of a Windows Phone app based on a SharePoint list, you see a validation error message when the focus shifts from the **TextBox** control associated with the field. (See Figure 1.)</span></span>
  
    
    

<span data-ttu-id="18431-119">**На рисунке 1. Очередь ошибок проверки в приложении Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="18431-119">**Figure 1. Validation error cue in a Windows Phone app**</span></span>

  
    
    

  
    
    
![Очередь ошибок проверки в приложении Windows Phone](../images/49a93d59-6755-4afc-a703-ca8469b6fa74.gif)
  
    
    
<span data-ttu-id="18431-p106">Текстовое поле «Время начала» в форме редактирования привязан к полю даты и времени в списке SharePoint, на котором основано в этом примере приложения. Очередь ошибок проверки (текстом красного цвета) показано на рисунке 1 отображается, если недопустимую дату, введенных в текстовое поле (и текстовое поле впоследствии теряет фокус) так, как свойство **ValidatesOnNotifyDataErrors** **Binding** объекта, связанного с помощью свойства **Text** элемента управления **TextBox** **True** в объявлении XAML, который определяет **TextBox** в файле EditForm.xaml.</span><span class="sxs-lookup"><span data-stu-id="18431-p106">The text box labeled "Start Time" in the Edit form is bound to a Date and Time field in the SharePoint list on which this sample app is based. The validation error cue (in red text) shown in Figure 1 appears if an invalid date is entered in the text box (and the text box subsequently loses focus) because the **ValidatesOnNotifyDataErrors** property of the **Binding** object associated with the **Text** property of the **TextBox** control is set to **True** in the XAML declaration that defines the **TextBox** in the EditForm.xaml file.</span></span>
  
    
    



```XML

<StackPanel Orientation="Vertical" Margin="0,5,0,5">
   <TextBlock TextWrapping="Wrap" HorizontalAlignment="Left" 
                    Style="{StaticResource PhoneTextNormalStyle}">Start Time*
   </TextBlock>
   <TextBox Height="Auto" Style="{StaticResource TextValidationTemplate}"
    FontSize="{StaticResource PhoneFontSizeNormal}" Width="470" 
        HorizontalAlignment="Left" Name="txtEventDate"
    Text="{Binding [EventDate], Mode=TwoWay, ValidatesOnNotifyDataErrors=True,
                       NotifyOnValidationError=True}"
    TextWrapping="Wrap" />
   <TextBlock FontSize="16" TextWrapping="Wrap" HorizontalAlignment="Left"
    Style="{StaticResource PhoneTextSubtleStyle}" Text="{Binding DateTimeFormat}" />
</StackPanel>
```

<span data-ttu-id="18431-p107">( **ValidatesOnNotifyDataErrors** задано значение **False**, есть ли у пользователя нет сигнал о том, что введенных данных является недопустимым, пока не выбран кнопку **Сохранить**. В этот момент на экране пользователя отображается сообщение об ошибке относительно ошибок проверки, так как проверка формата даты введенных значений по-прежнему выполняемые с базовый класс, от которого наследуется класс **EditItemViewModel**.)</span><span class="sxs-lookup"><span data-stu-id="18431-p107">(If the **ValidatesOnNotifyDataErrors** property is set to **False**, the user has no indication that the entered data is invalid until the **Save** button is chosen. At that point, the user sees an error message regarding validation errors, because format validation on entered date values is still carried out by the base class from which the **EditItemViewModel** class is derived.)</span></span>
  
    
    
<span data-ttu-id="18431-p108">Однако некоторые поля могут не предоставлять все уведомления о недопустимых данных в приложении Windows Phone. И шаблоны проектов хорошо продуманного Visual Studio обязательно обобщенный для использования в качестве отправной точки для разных приложениях. Шаблона приложения списка SharePoint для Windows Phone не может включать правила проверки, предназначенных для конкретных контекстах и еще сохранять свое значение как общий шаблон. В зависимости от ваших потребностей и условиях, в которых будут использоваться определенного приложения Windows Phone скорее всего потребуется реализовать правил проверки данных.</span><span class="sxs-lookup"><span data-stu-id="18431-p108">But some fields may not provide any notification for invalid data in the Windows Phone app. And well-designed Visual Studio project templates are necessarily generalized to be used as a starting point for many different applications. The Windows Phone SharePoint List Application template can't include validation rules relevant to specific contexts and yet retain its value as a generalized template. Depending on your needs and the circumstances in which your particular Windows Phone app will be used, you likely will want to implement your own custom data-validation rules.</span></span>
  
    
    

## <a name="implement-custom-data-validation-rules"></a><span data-ttu-id="18431-129">Реализации правил проверки данных</span><span class="sxs-lookup"><span data-stu-id="18431-129">Implement custom data-validation rules</span></span>
<span data-ttu-id="18431-130"><a name="BKMK_CustomValidation"> </a></span><span class="sxs-lookup"><span data-stu-id="18431-130"><a name="BKMK_CustomValidation"> </a></span></span>

<span data-ttu-id="18431-p109">Можно проверить данные, введенные пользователями вашего приложения Windows Phone с несколькими способами. Проект, созданный с использованием шаблона приложения списка SharePoint для Windows Phone включает классы, которые используются в качестве посредников между формы (то есть, представления) данных в приложении Windows Phone (например, файл EditForm.xaml) и самих данных в списке SharePoint, на котором приложения на основе. Эти классы можно оценить как реализации компоненте ViewModel  [шаблон разработки Model-View-ViewModel](http://blogs.msdn.com/b/johngossman/archive/2005/10/08/478683.aspx) (на рисунке 2). (Дополнительные сведения о как шаблона приложения списка SharePoint для Windows Phone соответствует шаблон разработки программного обеспечения MVVM см. [Архитектура шаблона приложения списка SharePoint для Windows Phone](architecture-of-the-windows-phone-sharepoint-list-application-template.md)).</span><span class="sxs-lookup"><span data-stu-id="18431-p109">You can validate data entered by users of your Windows Phone app in several ways. A project created by using the Windows Phone SharePoint List Application template includes classes that serve as intermediaries between the forms (that is, the views) of the data in the Windows Phone app (for example, the EditForm.xaml file) and the data itself in the SharePoint list on which the app is based. These classes can be considered implementations of the ViewModel component of the  [Model-View-ViewModel design pattern](http://blogs.msdn.com/b/johngossman/archive/2005/10/08/478683.aspx) (Figure 2). (For more information about how the Windows Phone SharePoint List Application template conforms to the MVVM software design pattern, see [Architecture of the Windows Phone SharePoint List Application template](architecture-of-the-windows-phone-sharepoint-list-application-template.md).)</span></span>
  
    
    

> <span data-ttu-id="18431-135">**Примечание:** Шаблоны списков SharePoint не включать обнаруживаются по умолчанию (например, процент завершения в списке задач SharePoint post флажок для групп обсуждений списка и проверки типа decimal полей SP), но можно реализовать такой проверки.</span><span class="sxs-lookup"><span data-stu-id="18431-135">**Note:** The SharePoint list templates do not include default validations (such as percentage complete in a SharePoint task list, post check for a team discussion list, and SP decimal field type validation), but you can implement such validations.</span></span> 
  
    
    


<span data-ttu-id="18431-136">**На рисунке 2. Файлы шаблонов в компоненте ViewModel**</span><span class="sxs-lookup"><span data-stu-id="18431-136">**Figure 2. Template files in ViewModel component**</span></span>

  
    
    

  
    
    
![Файлы шаблонов в компоненте ViewModel](../images/2df9591d-a837-4130-98e4-5863d0c717e8.gif)
  
    
    
<span data-ttu-id="18431-p110">В приложениях, разработанных на основании шаблоне MVVM, проверка данных часто используется на уровне данных (то есть в компоненте модели). В проектах, созданных на основе шаблона приложения списка SharePoint для Windows Phone, было расширяемый механизм для проверки данных «передать» слой и реализации в компоненте ViewModel, чтобы упростить для разработчиков для управления проверки данных. Проекты на основе шаблона таким образом, наиболее подходящего месте пользовательского кода, который проверяет входные данные пользователя или управляет данными, в противном случае  в эти классы ViewModel. Выполнить проверку данных, класс **EditItemViewModel** и класс **NewItemViewModel** (классы, связанные с формами, скорее всего, охватывающие изменение и обновление данных списков) оба предоставить open реализацию метода проверки (с именем **Validate**), который переопределяет метод базового проверки в классе, от которого наследуются этих двух классов.</span><span class="sxs-lookup"><span data-stu-id="18431-p110">In applications designed based on the MVVM pattern, data validation is often handled in the data layer (that is, in the Model component). In projects created from the Windows Phone SharePoint List Application template, an extensible mechanism for data validation has been "pushed up" a layer and implemented in the ViewModel component, to make it easier for developers to manage data validation. In projects based on the template, therefore, the most suitable place for custom code that validates user input or otherwise manages data is in these ViewModel classes. In terms of data validation, the **EditItemViewModel** class and the **NewItemViewModel** class (the classes associated with the forms most likely to involve editing and updating list data) both provide an open implementation of a validation method (named **Validate**) that overrides the base validation method in the class from which these two classes are derived.</span></span>
  
    
    



```cs

public override void Validate(string fieldName, object value)
   {
      base.Validate(fieldName, value);
   }
```

<span data-ttu-id="18431-p111">Этот метод  это удобный для разработчика для добавления настраиваемую логику проверки, отдельные целевые значения поля. Общий подход заключается в том, чтобы проверить значение аргумента **fieldName**, переданной в метод **Validate** для идентификации поля, который необходимо связать с нестандартной проверки кода. К примеру, можно используется оператор **switch** в реализации данного метода чтобы предоставить логику проверки, относящиеся к различным полям в форме редактирования (EditForm.xaml) приложение Windows.</span><span class="sxs-lookup"><span data-stu-id="18431-p111">This method provides a convenient mechanism to the developer for adding custom validation logic that targets individual fields. The general approach is to check the value of the **fieldName** argument passed to the **Validate** method to identify the field you want to associate with your custom validation code. You can, for example, use a **switch** statement in your implementation of this method to supply validation logic specific to various fields in the Edit form (EditForm.xaml) of your Windows app.</span></span>
  
    
    
<span data-ttu-id="18431-p112">В следующем примере кода предполагается, что установка SharePoint Server содержит список заказов на продукт, созданный на основе шаблона настраиваемого списка. Список был создан с помощью типов столбцов и полей показано в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="18431-p112">For the following code example, assume that an installation of SharePoint Server has a Product Orders list created from the Custom List template. The list has been created with the columns and field types shown in Table 1.</span></span>
  
    
    

<span data-ttu-id="18431-147">**В таблице 1. Список заказов на продукт**</span><span class="sxs-lookup"><span data-stu-id="18431-147">**Table 1. Product Orders list**</span></span>


|<span data-ttu-id="18431-148">**Столбец**</span><span class="sxs-lookup"><span data-stu-id="18431-148">**Column**</span></span>|<span data-ttu-id="18431-149">**Тип**</span><span class="sxs-lookup"><span data-stu-id="18431-149">**Type**</span></span>|<span data-ttu-id="18431-150">**Required**</span><span class="sxs-lookup"><span data-stu-id="18431-150">**Required**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="18431-151">Продукт (например, заголовок)</span><span class="sxs-lookup"><span data-stu-id="18431-151">Product (i.e., Title)</span></span>  <br/> |<span data-ttu-id="18431-152">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="18431-152">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="18431-153">Да</span><span class="sxs-lookup"><span data-stu-id="18431-153">Yes</span></span>  <br/> |
|<span data-ttu-id="18431-154">Описание</span><span class="sxs-lookup"><span data-stu-id="18431-154">Description</span></span>  <br/> |<span data-ttu-id="18431-155">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="18431-155">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="18431-156">Нет</span><span class="sxs-lookup"><span data-stu-id="18431-156">No</span></span>  <br/> |
|<span data-ttu-id="18431-157">Количество</span><span class="sxs-lookup"><span data-stu-id="18431-157">Quantity</span></span>  <br/> |<span data-ttu-id="18431-158">Число</span><span class="sxs-lookup"><span data-stu-id="18431-158">Number</span></span>  <br/> |<span data-ttu-id="18431-159">Да</span><span class="sxs-lookup"><span data-stu-id="18431-159">Yes</span></span>  <br/> |
|<span data-ttu-id="18431-160">Дата заказа</span><span class="sxs-lookup"><span data-stu-id="18431-160">Order Date</span></span>  <br/> |<span data-ttu-id="18431-161">Дата и время (DateTime)</span><span class="sxs-lookup"><span data-stu-id="18431-161">Date and Time (DateTime)</span></span>  <br/> |<span data-ttu-id="18431-162">Нет</span><span class="sxs-lookup"><span data-stu-id="18431-162">No</span></span>  <br/> |
|<span data-ttu-id="18431-163">Дата выполнения</span><span class="sxs-lookup"><span data-stu-id="18431-163">Fulfillment Date</span></span>  <br/> |<span data-ttu-id="18431-164">Дата и время (DateTime)</span><span class="sxs-lookup"><span data-stu-id="18431-164">Date and Time (DateTime)</span></span>  <br/> |<span data-ttu-id="18431-165">Нет</span><span class="sxs-lookup"><span data-stu-id="18431-165">No</span></span>  <br/> |
|<span data-ttu-id="18431-166">Номер контакта</span><span class="sxs-lookup"><span data-stu-id="18431-166">Contact Number</span></span>  <br/> |<span data-ttu-id="18431-167">Однострочный текст (Текст)</span><span class="sxs-lookup"><span data-stu-id="18431-167">Single line of text (Text)</span></span>  <br/> |<span data-ttu-id="18431-168">Нет</span><span class="sxs-lookup"><span data-stu-id="18431-168">No</span></span>  <br/> |
   
<span data-ttu-id="18431-169">Опять же в целях в этом примере предполагается, что следующие правила простой проверки находятся для применения, бизнес-логики в вымышленной компании Contoso, Ltd., для данного продукта упорядочивание системы на основании:</span><span class="sxs-lookup"><span data-stu-id="18431-169">Again, for the purposes of this example, assume that the following simple validation rules are to be enforced, based on the business logic employed at the fictitious company Contoso, Ltd., for a given product ordering system:</span></span>
  
    
    

- <span data-ttu-id="18431-170">Даты выполнения заказов orders должно быть позже даты, на котором размещена порядке.</span><span class="sxs-lookup"><span data-stu-id="18431-170">Fulfillment dates for orders must be later than the date on which the order was placed.</span></span>
    
  
- <span data-ttu-id="18431-p113">Если пользователь хочет размещение заказа на продукт, с именем Нечеткое кости, кости должны быть упорядочены в пары. В соответствии с правилами символы в компании Contoso, Ltd. нет просто нет такого понятия, как Нечеткое умереть.</span><span class="sxs-lookup"><span data-stu-id="18431-p113">If a customer wants to place an order for a product named Fuzzy Dice, the dice must be ordered in pairs. According to the peculiar rules at Contoso, Ltd., there is simply no such thing as a Fuzzy Die.</span></span>
    
  
- <span data-ttu-id="18431-p114">В списке заказов продукта тип поля для телефонных номеров является «Однострочный текст» (текст), который может быть любой текст (до 255 знаков по умолчанию). В данном примере форматирования правило проверки принудительно, которому требуется введенных данных должен находиться в одном из распространенных форматов номеров телефона. Например, «(555) 555-55 55».</span><span class="sxs-lookup"><span data-stu-id="18431-p114">In the Product Orders list, the field type for phone numbers is "Single line of text" (that is, Text), which can be any text (up to 255 characters by default). For this sample, a formatting validation rule will be enforced that requires entered data to be in one of the common phone number formats; for example, "(555) 555-5555".</span></span>
    
  

### <a name="to-implement-custom-validation-rules"></a><span data-ttu-id="18431-175">Для реализации настраиваемых правил проверки</span><span class="sxs-lookup"><span data-stu-id="18431-175">To implement custom validation rules</span></span>


1. <span data-ttu-id="18431-176">Предположим, что вы создали списка SharePoint на основе шаблона настраиваемый список, который включает в себя столбцов и типов, указанных в таблице 1, создание приложения Windows Phone с использованием шаблона приложения списка SharePoint для Windows Phone в Visual Studio, выполнив действия в [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md).</span><span class="sxs-lookup"><span data-stu-id="18431-176">Assuming you have created a SharePoint list based on the Custom List template that includes the columns and types specified in Table 1, create a Windows Phone app by using the Windows Phone SharePoint List Application template in Visual Studio by following the steps detailed in  [How to: Create a Windows Phone SharePoint list app](how-to-create-a-windows-phone-sharepoint-list-app.md).</span></span>
    
  
2. <span data-ttu-id="18431-177">В **Обозревателе решений** в папке ViewModels для проекта дважды щелкните файл EditItemViewModel.cs (или выберите файл и нажмите кнопкуF7) для открытия файла для редактирования.</span><span class="sxs-lookup"><span data-stu-id="18431-177">In **Solution Explorer**, in the ViewModels folder for the project, double-click the EditItemViewModel.cs file (or choose the file and press F7) to open the file for editing.</span></span>
    
  
3. <span data-ttu-id="18431-178">Добавьте следующие директивы **using** списка директив в верхней части файла.</span><span class="sxs-lookup"><span data-stu-id="18431-178">Add the following **using** directives to the list of directives at the top of the file.</span></span>
    
```cs
  
using System.Globalization;
using System.Text.RegularExpressions;
```

4. <span data-ttu-id="18431-179">Замените реализация по умолчанию с помощью метода **Validate** в файл следующий код.</span><span class="sxs-lookup"><span data-stu-id="18431-179">Replace the default implementation of the **Validate** method in the file with the following code.</span></span>
    
```cs
  
public override void Validate(string fieldName, object value)
{
    string fieldValue = value.ToString();
    if (!string.IsNullOrEmpty(fieldValue)) //Allowing for blank fields.
    {
        bool isProperValue = false;

        switch (fieldName)
        {
            case "Quantity":
                // Enforce ordering Fuzzy Dice in pairs only.
                int quantityOrdered;
                isProperValue = Int32.TryParse(fieldValue, out quantityOrdered);
                if (isProperValue)
                {
                    if ((quantityOrdered % 2) != 0) // Odd number of product items ordered.
                    {
                        if ((string)this["Title"] == "Fuzzy Dice")
                        {
                            AddError("Item[Quantity]", "Fuzzy Dice must be ordered in pairs. 
                                                                   No such thing as a Fuzzy Die!");
                        }
                        else
                        {
                            // Restriction on ordering in pairs doesn't apply to other products.
                            RemoveAllErrors("Item[Quantity]");
                        }
                    }
                    else
                    {
                        RemoveAllErrors("Item[Quantity]");
                    }
                }
                break;
            case "Fulfillment_x0020_Date":
                // Determine whether fulfillment date is later than order date.
                DateTime fulfillmentDate;
                isProperValue = DateTime.TryParse(fieldValue, CultureInfo.CurrentCulture, 
                              DateTimeStyles.AssumeLocal, out fulfillmentDate);
                if (isProperValue)
                {
                    DateTime orderDate;
                    isProperValue = DateTime.TryParse((string)this["Order_x0020_Date"], 
                               CultureInfo.CurrentCulture, DateTimeStyles.AssumeLocal, out orderDate);

                    if (fulfillmentDate.CompareTo(orderDate) > 0)
                    {
                        RemoveAllErrors("Item[Fulfillment_x0020_Date]");
                    }
                    else
                    {
                        AddError("Item[Fulfillment_x0020_Date]", 
                                "Fulfillment Date must be later than Order Date.");
                    }
                }
                break;
            case "Contact_x0020_Number":
                // Check that contact number is in an appropriate format.
                Regex rx = new Regex(@"^\\(?([0-9]{3})\\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$");
                if (rx.IsMatch(fieldValue))
                {
                    RemoveAllErrors("Item[Contact_x0020_Number]");
                }
                else
                {
                    //Specified Contact Number is not a valid phone number.
                    AddError("Item[Contact_x0020_Number]", "Specified Contact Number is invalid.");
                }
                break;
            default:
                // Not adding custom validation for other fields.
                break;
        }
    }

    //And then proceed with default validation from base class.
    base.Validate(fieldName, value);
}
```


    Keep in mind that the field names specified in this code sample are based on properties of the sample Product Orders list specified in Table 1. (Notice that in the XML schema for list fields in SharePoint Server, spaces in the names of fields are replaced with the string "_x0020_" for the **Name** attribute of the **Field** element that defines a given field. The template uses the **Name** attribute for a **Field** element as it is defined in the XML schema on the server, not the **DisplayName** attribute.) You can identify the field names of those fields for which you want to implement validation logic by looking at the **Binding** declarations of the **Text** properties for the **TextBox** objects defined in EditForm.xaml or by examining the **ViewFields** string of the **CamlQueryBuilder** class in the ListProvider.cs file.
    
  
5. <span data-ttu-id="18431-180">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="18431-180">Save the file.</span></span>
    
  
<span data-ttu-id="18431-p115">Настраиваемая проверка кода в этом примере выполняется только в том случае, если аргумент **value**, переданной в метод **Validate** не может быть null или пустую строку. Как показано в таблице 1, поля Дата выполнения и номер контакта не требуются для хранения данных (как список определяется в целях в этом примере SharePoint Server ), поэтому его нужно разрешить эти поля как пустые. Простой проверку, чтобы определить, является ли аргумент **value** значение null, недостаточно, так как значение, переданное может быть строка нулевой длины (к которым не соответствуют нулевое значение), а для данного примера необходимо объявить недействительным пустых строк для полей, которые могут быть пустым. Логику проверки для поля Кол-во и Дата выполнения включает в себя дополнительные проверки значений, подставляемых в, чтобы убедиться в их соответствующего типа. Начальная проверка здесь (перед оператором **switch** ) подтверждено только, переданное значение, не равно null (вместо проверки на соответствие узкие условие являются строку нулевой длины), эти проверки будет по-прежнему не выполняется, если это значение было строку нулевой длины, но логики для проверки данных для **Номер контакта** поля *будет*  по-прежнему выполняется, если значение, переданное были строку нулевой длины. И в этом примере, чтобы предоставить в поле номер контакта должно быть пустым (строкой нулевой длины), особенно при запуске изменении элемента списка, открыв форма редактирования.</span><span class="sxs-lookup"><span data-stu-id="18431-p115">The custom validation code in this sample is executed only if the **value** argument passed to the **Validate** method is not a null or empty string. As indicated in Table 1, the Fulfillment Date and Contact Number fields are not required to contain data (as the list is defined for the purposes of this sample in SharePoint Server), so we want to allow these fields to be blank. A simple check to determine whether the **value** argument is null is not sufficient, because the value passed could be a zero-length string (which doesn't equate to a null value), and for this sample we don't want to invalidate zero-length strings for fields that can be blank. The validation logic for the Quantity and Fulfillment Date fields includes additional checks of the values passed in to ensure that they are of the appropriate type. If the initial check here (before the **switch** statement) confirmed only that the value passed in were not null (instead of checking against the narrower condition of being a zero-length string), those validations would still not execute if the value were a zero-length string, but the logic to validate data for the **Contact Number** field *would*  still execute if the value passed were a zero-length string. And in this sample we want to allow for the Contact Number field to be blank (a zero-length string), especially when a user starts editing a list item by opening the Edit form.</span></span>
  
    
    
<span data-ttu-id="18431-p116">Если построение проекта и его развертывание на эмулятора Windows Phone для ее выполнения можно проверить свою логику проверки, введя данные, которые нарушают бизнес-правил в поля в список в форме редактирования app. (увидеть на рисунке 3.)</span><span class="sxs-lookup"><span data-stu-id="18431-p116">If you build the project and deploy it to Windows Phone Emulator to run it, you can test your validation logic by entering data that violates your business rules into the fields of the list in the Edit form of the app. (See Figure 3.)</span></span>
  
    
    

<span data-ttu-id="18431-189">**На рисунке 3. Настраиваемые очереди проверки ошибок**</span><span class="sxs-lookup"><span data-stu-id="18431-189">**Figure 3. Custom validation error cues**</span></span>

  
    
    

  
    
    
![Настраиваемые очереди проверки ошибок](../images/fada902b-fa38-4ac8-8566-3693b736ac35.gif)
  
    
    
<span data-ttu-id="18431-p117">Код, приведенный в этом примере содержащийся в файле EditItemViewModel.cs только, применяет эти правила проверки данных, введенных пользователями только в форме редактирования. Если вы хотите добавить правила проверки обоих при пользователям  *добавлять*  новые элементы также при их изменить их, необходимо включить ту же логику проверки в метод **Validate** в NewItemViewModel.cs файл (или желательно, чтобы создать отдельный файл класса с функция, которая включает в себя этот логику проверки и звонок, то же самое функции из методов **Validate** в файле EditItemViewModel.cs и файл NewItemViewModel.cs).</span><span class="sxs-lookup"><span data-stu-id="18431-p117">The code in this sample, if it is included in the EditItemViewModel.cs file only, enforces these validation rules for data entered by users only on the Edit Form. If you want to enforce the validation rules both when users  *add*  new items as well as when they edit them, you must include the same validation logic in the **Validate** method in the NewItemViewModel.cs file (or, preferably, create a separate class file with a function that includes this validation logic and call that same function from the **Validate** methods in both the EditItemViewModel.cs file and the NewItemViewModel.cs file).</span></span>
  
    
    
<span data-ttu-id="18431-193">Логику проверки в этом примере применяет данного бизнес-правил, указывающий пользователя, что введенных данных не в формате, допускаемых правила, но не перехвачены и изменена этот код введенных данных.</span><span class="sxs-lookup"><span data-stu-id="18431-193">The validation logic in this sample enforces given business rules by indicating to the user that entered data is not in a format permitted by the rules, but the entered data is not intercepted and changed by this code.</span></span> <span data-ttu-id="18431-194">Для перехвата и, например, формат телефонных номеров в едином виде перед сохранением данных в список SharePoint, вы можете реализовать преобразование пользовательских данных для введенных номеров телефонов.</span><span class="sxs-lookup"><span data-stu-id="18431-194">To intercept and, for example, format phone numbers in a consistent way before saving the data to the SharePoint list, you can implement custom data conversion for entered phone numbers.</span></span> <span data-ttu-id="18431-195">Объяснение преобразование пользовательских данных для полей элемента списка, в разделе [как: поддержка и convert SharePoint поля типов приложений Windows Phone](how-to-support-and-convert-sharepoint-field-types-for-windows-phone-apps.md).</span><span class="sxs-lookup"><span data-stu-id="18431-195">For an explanation of custom data conversion for list item fields, see  [How to: Support and convert SharePoint field types for Windows Phone apps](how-to-support-and-convert-sharepoint-field-types-for-windows-phone-apps.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="18431-196">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="18431-196">Additional resources</span></span>
<span data-ttu-id="18431-197"><a name="SP15Implementbuslogic_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="18431-197"></span></span>


-  [<span data-ttu-id="18431-198">Построение приложений Windows Phone, обращающихся к SharePoint</span><span class="sxs-lookup"><span data-stu-id="18431-198">Build Windows Phone apps that access SharePoint</span></span>](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [<span data-ttu-id="18431-199">Привязка данных Silverlight</span><span class="sxs-lookup"><span data-stu-id="18431-199">Silverlight Data Binding</span></span>](http://msdn.microsoft.com/en-us/library/cc278072.aspx)
    
  
-  [<span data-ttu-id="18431-200">Как: Настройка среды разработки мобильных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="18431-200">How to: Set up an environment for developing mobile apps for SharePoint</span></span>](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [<span data-ttu-id="18431-201">Windows Phone SDK 8.0</span><span class="sxs-lookup"><span data-stu-id="18431-201">Windows Phone SDK 8.0</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [<span data-ttu-id="18431-202">Пакет SDK Microsoft SharePoint для Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="18431-202">Microsoft SharePoint SDK for Windows Phone 8</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [<span data-ttu-id="18431-203">Пакет SDK для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="18431-203">Windows Phone SDK 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [<span data-ttu-id="18431-204">Пакет SDK Microsoft SharePoint для Windows Phone 7.1</span><span class="sxs-lookup"><span data-stu-id="18431-204">Microsoft SharePoint SDK for Windows Phone 7.1</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

