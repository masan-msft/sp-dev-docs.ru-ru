---
title: "Общие сведения о действия словаря в SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 73df233e-bad8-4ea1-b05d-61ecab597924
ms.openlocfilehash: 521a83199046ba17636ae41fc8834989d2a7cb91
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-dictionary-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="7a182-102">Общие сведения о действия словаря в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="7a182-102">Understanding Dictionary actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="7a182-103">Тип переменной словаря — это новый тип переменной в платформы рабочих процессов SharePoint, которые можно использовать с помощью SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="7a182-103">The Dictionary variable type is a new variable type in the SharePoint Workflow platform that you can use with SharePoint Designer 2013.</span></span> 

   

## <a name="understanding-the-dictionary-variable-type"></a><span data-ttu-id="7a182-104">Общие сведения о переменных тип словаря</span><span class="sxs-lookup"><span data-stu-id="7a182-104">Understanding the Dictionary variable type</span></span>
<span data-ttu-id="7a182-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="7a182-105"></span></span>

<span data-ttu-id="7a182-p101">Рабочий процесс  это последовательность действий, которые выполняют желаемый результат. При построении рабочего процесса, часто требуется сохранить значения в переменной (контейнер хранения) для использования в других частей рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="7a182-p101">A workflow is a series of actions that perform a desired outcome. As you build a workflow you often need to save values in a variable (storage container) to use in other parts of the workflow.</span></span>
  
    
    
<span data-ttu-id="7a182-p102">При создании переменной необходимо указать обработчик workflow типа данных будет содержится в переменной. Например может потребоваться сохранить имени сотрудника в переменной. Имя сотрудника  это строка символов, поэтому необходимо создать переменную типа **String**. Рабочий процесс может храниться имя сотрудника, например "Иван Петров", в переменной.</span><span class="sxs-lookup"><span data-stu-id="7a182-p102">When you create a variable you need to tell the workflow engine what type of data will be contained in the variable. For example, you might want to save the name of an employee in a variable. The name of an employee is a string of characters so you would create a variable of type **String**. The workflow could then store the name of the employee, such as "John Doe," in the variable.</span></span> 
  
    
    

<span data-ttu-id="7a182-112">**Рисунок: Строковой переменной**</span><span class="sxs-lookup"><span data-stu-id="7a182-112">**Figure: A String variable**</span></span>

  
    
    

  
    
    
![Переменная строки](../images/SPD-Dictionary-1a.png)
  
    
    
<span data-ttu-id="7a182-p103">SharePoint Designer 2013 имеет новый тип переменной с именем **словаря**. Тип переменной **словаря** является контейнером, предназначенный для хранения коллекцию других переменных. Например рабочего процесса может потребоваться больше, чем просто имя сотрудника. Он может потребоваться для хранения даты свой адрес и рождения. Если вы не используете переменная **словаря** необходимо создать несколько изолированный переменных. Это можно быстро стать неудобен для организации и их для работы в логику рабочего процесса. Переменная **словаря** позволяет сохранять несколько точек данных в одной переменной.</span><span class="sxs-lookup"><span data-stu-id="7a182-p103">SharePoint Designer 2013 has a new variable type called **Dictionary**. The **Dictionary** variable type is a container designed to hold a collection of other variables. For example, your workflow might need to store more than just the name of the employee. It might also need to store his address and birth date. If you do not use the **Dictionary** variable you will have to create multiple stand-alone variables. This can quickly become difficult to organize and difficult to work with in the logic of the workflow. A **Dictionary** variable allows you to store multiple data points in a single variable.</span></span>
  
    
    
<span data-ttu-id="7a182-121">Эта концепция показана на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="7a182-121">The figure illustrates the concept.</span></span>
  
    
    

<span data-ttu-id="7a182-122">**Рисунок: Переменная словаря**</span><span class="sxs-lookup"><span data-stu-id="7a182-122">**Figure: A Dictionary variable**</span></span>

  
    
    

  
    
    
![Переменная словаря](../images/SPD15-Dictionary-1b.png)
  
    
    

  
    
    

  
    
    

## <a name="workflow-actions-that-use-the-dictionary-variable-type"></a><span data-ttu-id="7a182-124">Действия рабочего процесса, использующие типа переменной словаря</span><span class="sxs-lookup"><span data-stu-id="7a182-124">Workflow actions that use the Dictionary variable type</span></span>
<span data-ttu-id="7a182-125"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="7a182-125"></span></span>

<span data-ttu-id="7a182-p104">Рабочий процесс состоит из нескольких действий, выполняемых при обработке рабочего процесса. SharePoint Designer 2013 содержит множество различных действий. Например  это действие для отправки сообщения электронной почты, создание элемента списка и записывать сообщения в журнал рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="7a182-p104">A workflow consists of multiple actions that are executed as the workflow is processed. SharePoint Designer 2013 contains many different actions. For example, there is an action to send an email message, create a list item, and log messages to workflow history.</span></span>
  
    
    
<span data-ttu-id="7a182-129">Ниже приведены три действия, специально предназначенный для типа переменной **словаря**.</span><span class="sxs-lookup"><span data-stu-id="7a182-129">The following are the three actions specifically designed for the **Dictionary** variable type.</span></span>
  
    
    

- <span data-ttu-id="7a182-130">**Создание словаря**</span><span class="sxs-lookup"><span data-stu-id="7a182-130">**Build Dictionary**</span></span>
    
  
- <span data-ttu-id="7a182-131">**Посчитать число элементов в словаре**</span><span class="sxs-lookup"><span data-stu-id="7a182-131">**Count Items in a Dictionary**</span></span>
    
  
- <span data-ttu-id="7a182-132">**Получение элемента из словаря.**</span><span class="sxs-lookup"><span data-stu-id="7a182-132">**Get an Item from a Dictionary**</span></span>
    
  
<span data-ttu-id="7a182-133">Действия рабочего процесса дляОбласть задачТип переменной можно найти в раскрывающемся списке **Действие**, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="7a182-133">The workflow actions for the Dictionary variable type can be found on the **Action** drop-down list, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="7a182-134">**На рисунке: Действия словаря**</span><span class="sxs-lookup"><span data-stu-id="7a182-134">**Figure: Dictionary actions**</span></span>

  
    
    

  
    
    
![Действия словаря](../images/SPD15-Dictionary-2.png)
  
    
    

### <a name="create-variables-with-the-build-dictionary-action"></a><span data-ttu-id="7a182-136">Создайте переменные с действием «Создание словаря»</span><span class="sxs-lookup"><span data-stu-id="7a182-136">Create variables with the "Build Dictionary" action</span></span>

<span data-ttu-id="7a182-p105">Чтобы создать переменную типа **словаря** используйте действие **Построения словаря**. Введите содержимое словаря и укажите имя словаря, в списке переменных.</span><span class="sxs-lookup"><span data-stu-id="7a182-p105">You use the **Build Dictionary** action to create a variable of type **Dictionary**. You enter the contents of the dictionary and then specify the name of the dictionary in the variable list.</span></span>
  
    
    
<span data-ttu-id="7a182-p106">На рисунке показано диалоговое окно **Создание словаря**. Обратите внимание на то, что три переменные были добавлены в словарь: строка, целого числа и даты и времени.</span><span class="sxs-lookup"><span data-stu-id="7a182-p106">The figure shows the **Build a Dictionary** dialog box. Notice that three variables have been added to the dictionary: a string, an integer, and a date/time.</span></span>
  
    
    

<span data-ttu-id="7a182-141">**Рисунок: Поле диалоговое окно «Создание словаря»**</span><span class="sxs-lookup"><span data-stu-id="7a182-141">**Figure: The "Build a Dictionary" dialog box**</span></span>

  
    
    

  
    
    
![Построение диалогового окна "Словарь"](../images/SPD15-BuildADictionaryDialog.png)
  
    
    
<span data-ttu-id="7a182-143">**Словарь** может содержать любого типа переменной, доступные в платформы рабочих процессов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7a182-143">A **Dictionary** can contain any type of variable available in the SharePoint Workflow platform.</span></span> <span data-ttu-id="7a182-144">В следующем списке определяются типы переменных:</span><span class="sxs-lookup"><span data-stu-id="7a182-144">The following list defines the variable types available:</span></span>
  
    
    

- <span data-ttu-id="7a182-145">**Логическое**: значение Да или нет</span><span class="sxs-lookup"><span data-stu-id="7a182-145">**Boolean**: A Yes or No value</span></span>
    
  
- <span data-ttu-id="7a182-146">**Даты и времени**: Дата и время</span><span class="sxs-lookup"><span data-stu-id="7a182-146">**Date/Time**: A date and time</span></span>
    
  
- <span data-ttu-id="7a182-147">**Словарь**: коллекцию переменных</span><span class="sxs-lookup"><span data-stu-id="7a182-147">**Dictionary**: A collection of variables</span></span>
    
  
- <span data-ttu-id="7a182-148">**Идентификатор GUID**: глобальный уникальный идентификатор (GUID)</span><span class="sxs-lookup"><span data-stu-id="7a182-148">**Guid**: A Globally Unique Identifier (GUID)</span></span>
    
  
- <span data-ttu-id="7a182-149">**Целое число**: целое число без десятичных знаков</span><span class="sxs-lookup"><span data-stu-id="7a182-149">**Integer**: A whole number without decimals</span></span>
    
  
- <span data-ttu-id="7a182-150">**Номера**: номер, который может содержать дробными разрядами</span><span class="sxs-lookup"><span data-stu-id="7a182-150">**Number**: A number that can contain decimals</span></span>
    
  
- <span data-ttu-id="7a182-151">**Строка**: строка символов</span><span class="sxs-lookup"><span data-stu-id="7a182-151">**String**: A string of characters</span></span>
    
  

    
> <span data-ttu-id="7a182-152">**Важные:** Тип переменной **словаря** крайне важна, когда вы используете действие **Вызова веб-службы HTTP** .</span><span class="sxs-lookup"><span data-stu-id="7a182-152">**Important:** The **Dictionary** variable type is critical when you are using the **Call HTTP Web Service** action.</span></span>
  
    
    


    
> <span data-ttu-id="7a182-153">**Осторожность:** Использование в поле **имя** в качестве подстановки поддерживается только при указании значения в словаре.</span><span class="sxs-lookup"><span data-stu-id="7a182-153">**Caution:** Using the **Name** field as a lookup is only supported when you are setting a value in a dictionary.</span></span> <span data-ttu-id="7a182-154">Использование в поле **имя** в качестве подстановки не поддерживается при построении словаря.</span><span class="sxs-lookup"><span data-stu-id="7a182-154">Using the **Name** field as a lookup is not supported when you are building a dictionary.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="7a182-p109">[!Примечание] Переменная **словаря** может содержать переменную типа **словаря**. Возможность хранить переменные **словаря** **Dictionary** предоставляет ряд преимуществ. Например можно создать **словарь** для хранения сведений о сотрудниках. В рамках **словаря** можно создать еще одну запись **словаря** для каждого сотрудника. При построении рабочего процесса можно использовать переменную **словаря** вместо постоянно создания новой автономной переменные для каждого элемента данных о каждого сотрудника. Как показано в этом примере, **словарь** можно использовать для организации сложных данных в рамках рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="7a182-p109">A **Dictionary** variable can contain a variable of type **Dictionary**. The ability to store **Dictionary** variables within a **Dictionary** provides a number of benefits. For example, you might create a **Dictionary** to store information about employees. Within the **Dictionary** you might create another **Dictionary** entry for each employee. As you build the workflow you can use the **Dictionary** variable instead of constantly creating new stand-alone variables for each piece of information about each employee. As this example shows, a **Dictionary** can be used to organize complex information within the workflow.</span></span>
  
    
    


### <a name="count-and-store-variables-with-the-count-items-in-a-dictionary-action"></a><span data-ttu-id="7a182-161">Количество и хранения переменных с действием «Число элементов в словаре»</span><span class="sxs-lookup"><span data-stu-id="7a182-161">Count and store variables with the "Count Items in a Dictionary" action</span></span>

<span data-ttu-id="7a182-p110">Используйте действие **Число элементов в словаре** для подсчета переменные, которые содержит **словарь**, а затем сохраните этот номер в переменной типа Integer. Затем можно использовать число элементов в цикле **словаря**.</span><span class="sxs-lookup"><span data-stu-id="7a182-p110">You use the **Count Items in a Dictionary** action to count the variables that a **Dictionary** contains and then store that number in an Integer variable. You can then use the item count to loop through the **Dictionary**.</span></span>
  
    
    
<span data-ttu-id="7a182-164">На рисунке показаны действия рабочего процесса **Число элементов в словаре**.</span><span class="sxs-lookup"><span data-stu-id="7a182-164">The figure shows the **Count Items in a Dictionary** workflow action.</span></span>
  
    
    

<span data-ttu-id="7a182-165">**Рисунок: Число элементов в словаре**</span><span class="sxs-lookup"><span data-stu-id="7a182-165">**Figure: Count items in a Dictionary**</span></span>

  
    
    

  
    
    
![Счетчик элементов в словаре.](../images/SPD15-CountItemsInDictionary.png)
  
    
    

  
    
    

  
    
    

### <a name="retrieve-variables-with-the-get-an-item-from-a-dictionary-action"></a><span data-ttu-id="7a182-167">Получение переменных с действием «Получение элемента из словаря»</span><span class="sxs-lookup"><span data-stu-id="7a182-167">Retrieve variables with the "Get an Item from a Dictionary" action</span></span>

<span data-ttu-id="7a182-p111">Действие **Получение элемента из словаря** используется для получения переменной, хранящейся в **словаре** и поместить его в переменную. Это полезно при необходимости значение в словаре, хранящиеся в переменной изолированный. Можно получить значение, указав имя переменной.</span><span class="sxs-lookup"><span data-stu-id="7a182-p111">You use the **Get an Item from a Dictionary** action to retrieve a variable stored in the **Dictionary** and place it in a variable. This is valuable when you need a value in the dictionary stored in a stand-alone variable. You can retrieve a value by entering the name of the variable.</span></span>
  
    
    
<span data-ttu-id="7a182-p112">На рисунке показано **Получение элемента из словаря** действия рабочего процесса. Обратите внимание на то, что **Срок хранения** является имя переменной в **словаре** и который вывод в новую переменную **целое число**.</span><span class="sxs-lookup"><span data-stu-id="7a182-p112">The figure shows the **Get an Item from a Dictionary** workflow action. Notice that **Age** is the name of the variable in the **Dictionary** and it is being output to a new **Integer** variable.</span></span>
  
    
    

<span data-ttu-id="7a182-173">**Рисунок: Получение элемента из словаря**</span><span class="sxs-lookup"><span data-stu-id="7a182-173">**Figure: Get an item from a Dictionary**</span></span>

  
    
    

  
    
    
![Получение элемента из словаря.](../images/SPD15-GetAnItemFromDictionary.png)
  
    
    

  
    
    

  
    
    

## <a name="see-also"></a><span data-ttu-id="7a182-175">См. также</span><span class="sxs-lookup"><span data-stu-id="7a182-175">See also</span></span>
<span data-ttu-id="7a182-176"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7a182-176"></span></span>


-  [<span data-ttu-id="7a182-177">Рабочий процесс в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7a182-177">Workflow in SharePoint</span></span>](http://technet.microsoft.com/en-us/sharepoint/jj556245.aspx)
    
  
-  [<span data-ttu-id="7a182-178">Новые возможности рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="7a182-178">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="7a182-179">Начало работы с рабочими процессами SharePoint</span><span class="sxs-lookup"><span data-stu-id="7a182-179">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  

  
    
    

