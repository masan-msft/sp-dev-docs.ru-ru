---
title: "Краткий справочник по условиям рабочего процесса (платформа рабочих процессов SharePoint 2010)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 71fab25b-d4f3-4871-b9ad-08d3537098fc
ms.openlocfilehash: e850ccfa11014f1032e298196ebaf0212afa3019
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-conditions-quick-reference-sharepoint-2010-workflow-platform"></a><span data-ttu-id="4b693-102">Краткий справочник по условиям рабочего процесса (платформа рабочих процессов SharePoint 2010)</span><span class="sxs-lookup"><span data-stu-id="4b693-102">Workflow conditions quick reference (SharePoint 2010 Workflow platform)</span></span>
<span data-ttu-id="4b693-103">Узнайте о условий рабочих процессов, доступных в SharePoint 2010 платформы рабочих процессов в Microsoft SharePoint Designer 2013.Use этой статьи *только* при работе в SharePoint Designer 2013, но продолжить использовать SharePoint 2010 Platform.If рабочего процесса требуется использование платформы рабочих процессов SharePoint, [действия рабочего процесса и справочник по действий для SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)и других статей, перечисленных в разделе «Дополнительные ресурсы», которые описаны новые функции, которые являются доступно в новой платформе. Чтобы приступить к созданию рабочего процесса с помощью платформы рабочих процессов 2010, выберите **Рабочий процесс SharePoint 2010** в поле **Тип платформы** в диалоговом окне **Создать рабочий процесс** .</span><span class="sxs-lookup"><span data-stu-id="4b693-103">Learn about the workflow conditions that are available in the SharePoint 2010 Workflow Platform in Microsoft SharePoint Designer 2013.Use this article  *only*  if you are working in SharePoint Designer 2013, but want to continue to use the SharePoint 2010 Workflow Platform.If instead you want to use the SharePoint Workflow Platform, see  [Workflow actions and activities reference for SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md), and other articles listed in the "Additional resources" section, which describe new features that are available in the newer platform.To begin creating a workflow by using the 2010 Workflow Platform, select **SharePoint 2010 Workflow** in the **Platform Type** box in the **Create Workflow** dialog box.</span></span>
## <a name="where-to-find-the-workflow-conditions"></a><span data-ttu-id="4b693-104">Где можно найти условий рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="4b693-104">Where to find the workflow conditions</span></span>
<span data-ttu-id="4b693-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="4b693-105"><a name="section1"> </a></span></span>

<span data-ttu-id="4b693-106">Существует два способа для доступа к меню условий рабочих процессов недоступны.</span><span class="sxs-lookup"><span data-stu-id="4b693-106">There are two ways to access the menu of available workflow conditions.</span></span>
  
    
    
<span data-ttu-id="4b693-107">При редактировании в шаге рабочего процесса выполните одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="4b693-107">While you are editing inside a workflow step, do one of the following:</span></span>
  
    
    

- <span data-ttu-id="4b693-108">На вкладке **рабочего процесса** в группе **Вставка** выберите **условия**, чтобы открыть список действий рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="4b693-108">On the **Workflow** tab, in the **Insert** group, click **Conditions** to open the list of workflow actions.</span></span>
    
  
- <span data-ttu-id="4b693-p101">Дважды щелкните внутри шаг рабочего процесса. В поле поиска введите текст, который отображается листа условие, которое требуется, например, "Создать" и нажмите клавишу ВВОД. Действия и условия, которые содержат текст, введенный появляется через текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="4b693-p101">Double-click inside a workflow step. In the search box that appears, type text that appears in the name of the condition that you want, such as "created", and then press Enter. Actions and conditions that contain the text you typed appear after the text box.</span></span>
    
  

  
    
    
![Введите ключевые слова, чтобы просмотреть список связанных условий.](../images/spd15-wf-step1a.JPG)
  
    
    
<span data-ttu-id="4b693-p102">Какие условия доступны при создании или изменение рабочего процесса зависит от точного контекста, которой вы работаете. В разделе ниже для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="4b693-p102">Which conditions are available to you while you are creating or modifying a workflow depends on the precise context that you are working in. See the following illustration for more information.</span></span>
  
    
    

  
    
    
![Доступные условия в SharePoint Designer 2013](../images/spd15-.JPG)
  
    
    
 <span data-ttu-id="4b693-116">Общие условия **1** в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="4b693-116">**1** General conditions in SharePoint Designer 2013.</span></span>
  
    
    
 <span data-ttu-id="4b693-117">**2** **Проверьте разрешения для элемента списка точное** и **разрешения для элемента списка**, доступны только в пределах шаг олицетворения.</span><span class="sxs-lookup"><span data-stu-id="4b693-117">**2** **Check exact list item permissions** and **Check list item permissions** are available only inside an impersonation step.</span></span>
  
    
    
 <span data-ttu-id="4b693-118">**3** **Размер файла находится в конкретном диапазоне Кбайт** и **Тип файла имеет конкретный тип** доступны только в рабочий процесс, связанный с типом контента документа, дочерний тип контента документа или библиотеке.</span><span class="sxs-lookup"><span data-stu-id="4b693-118">**3** **The file size is a specific range kilobytes** and **The file type is a specific type** are available only in a workflow that is associated with the Document content type, a child of the Document content type, or a library.</span></span>
  
    
    
 <span data-ttu-id="4b693-119">**4** **Если любое значение равно указанному значению** и **пользователь является допустимым пользователем SharePoint** являются единственным условий, доступных для создания рабочего процесса сайта.</span><span class="sxs-lookup"><span data-stu-id="4b693-119">**4** **If any value equals value** and **Person is a valid SharePoint user** are the only conditions available when you create a site workflow.</span></span>
  
    
    

## <a name="general-conditions"></a><span data-ttu-id="4b693-120">Общие условия</span><span class="sxs-lookup"><span data-stu-id="4b693-120">General conditions</span></span>
<span data-ttu-id="4b693-121"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="4b693-121"><a name="section2"> </a></span></span>

<span data-ttu-id="4b693-122">В этом разделе описываются условия, которые доступны в SharePoint Designer 2013 для списков и рабочих процессов для повторного использования списков, независимо от того, какой тип списка или типа контента, чтобы сопоставлен рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="4b693-122">This section describes the conditions that are available in SharePoint Designer 2013 for list and reusable list workflows, no matter what list type or content type the workflow is associated to.</span></span>
  
    
    

### <a name="if-any-value-equals-value"></a><span data-ttu-id="4b693-123">Если любое значение равно указанному значению</span><span class="sxs-lookup"><span data-stu-id="4b693-123">If any value equals value</span></span>

<span data-ttu-id="4b693-p103">Это условие сначала отображается в действии рабочего процесса как **Если любое значение равно указанному значению**. Это условие используется для сравнения одно значение с другим значением. Каждое значение может быть статический текст, динамическую строку или подстановки переменной, сведения о контексте или поля SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4b693-p103">This condition is initially displayed in a workflow step as **If any value equals value**. Use this condition when you want to compare one value with another value. Each value can be static text, a dynamic string, or a lookup to a variable, to context information, or to a SharePoint field.</span></span>
  
    
    
<span data-ttu-id="4b693-p104">Можно выбрать из большое число операторов в условие, такие как **содержит** и **больше, чем**. Для этого необходимо установить первое **значение** в условии и затем щелкните **равно**. Операторы, доступные зависят от первого **значение** в условие имеет значение. Например при использовании диалогового окна поиска для первого присваивается **значение** в условии тип данных даты и времени, такие как **Created** **оператор** не из доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="4b693-p104">You can select from a wide range of operators in your condition, such as **contains** and **is greater than**. To do so, you must set the first **value** in the condition and then click **equals**. The operators that are available depend on what the first **value** in the condition is set to. For example, if you used the lookup dialog to set the first **value** in the condition to a Date and Time data type, such as **Created**, the **Contains** operator is not among the available options.</span></span>
  
    
    
<span data-ttu-id="4b693-131">Существует два варианта **равняется** и **содержит** операторы.</span><span class="sxs-lookup"><span data-stu-id="4b693-131">There are two variations of the **equals** and **contains** operators:</span></span>
  
    
    

- <span data-ttu-id="4b693-132">Операторы **равенства** и **содержит** операции присваивания являются с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="4b693-132">The **equals** and **contains** operators are both case-sensitive.</span></span>
    
  
- <span data-ttu-id="4b693-133">Операторы **равенства (без учета регистра)** и **содержит (без учета регистра букв)** не учитывают регистр.</span><span class="sxs-lookup"><span data-stu-id="4b693-133">The **equals (ignoring case)** and **contains (ignoring case)** operators are not case-sensitive.</span></span>
    
  
<span data-ttu-id="4b693-p105">Параметр, выбранный для второе **значение** в условии также зависит от в некоторой степени что первое **значение** задано значение. Предположим, что первое **значение** равно **создано** и затем поиске второе **значение** с помощью переменной, которая является строка, например, **Последние 10 символов**. Возможно, следует возвращать строку **Как даты и времени**, таким образом, сравнение с **Created** возвращал предсказуемые результаты.</span><span class="sxs-lookup"><span data-stu-id="4b693-p105">The option that you choose for the second **value** in the condition also depends to some extent on what the first **value** is set to. For example, suppose that you set the first **value** to **Created**, and then you look up the second **value** by using a variable that is a string, such as **Last 10 Characters**. You would probably want to return the string **As Date/Time**, so that the comparison with **Created** will return predictable results.</span></span>
  
    
    

> <span data-ttu-id="4b693-137">**Примечание:** Можно использовать логические операторы, такие как**||**(или) или ** &amp; ** (и) в условии.</span><span class="sxs-lookup"><span data-stu-id="4b693-137">**Note:** You can use logical operators such as**||**(or) or **&amp;&amp;** (and) in the condition.</span></span>
  
    
    

<span data-ttu-id="4b693-138">Ниже приведены примеры как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-138">Following are examples of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-139">Если переменной: недели от измененобольше, чемсегодня</span><span class="sxs-lookup"><span data-stu-id="4b693-139">If Variable: A week from Modifiedis greater thanToday</span></span>
    
  
- <span data-ttu-id="4b693-140">Если переменной: имя спецификациясодержит (без учета регистра букв)SharePoint Designer || SPD</span><span class="sxs-lookup"><span data-stu-id="4b693-140">If Variable: Specification Namecontains (ignoring case)SharePoint Designer || SPD</span></span>
    
  
<span data-ttu-id="4b693-p106">**Если любое значение равно указанному значению** условие  это один из двух условий, доступных при работе в рабочий процесс сайта другое  **пользователь является допустимым пользователем SharePoint**. Дополнительные сведения о рабочих процессов сайта разделе  [Условия доступны в рамках рабочего процесса сайта](workflow-conditions-quick-reference-sharepoint-2010-workflow-platform.md#section5) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b693-p106">The **If any value equals value** condition is one of only two conditions available when you are working in a site workflow, the other being **Person is a valid SharePoint user**. For more information about site workflows, see the  [Conditions available within a site workflow](workflow-conditions-quick-reference-sharepoint-2010-workflow-platform.md#section5) section of this article.</span></span>
  
    
    

### <a name="if-current-item-field-equals-value"></a><span data-ttu-id="4b693-143">Если текущее поле элемента равно значению</span><span class="sxs-lookup"><span data-stu-id="4b693-143">If current item field equals value</span></span>

<span data-ttu-id="4b693-p107">Это условие сначала отображается в действии рабочего процесса как **поля равно указанному значению**. Это условие можно используйте для сравнения значения в поле в текущем элементе (элемент, списка или для повторного использования рабочего процесса списка в настоящее время работает на) с другим значением. Значения может быть статический текст, динамической строки или поиск в переменные, сведения о контексте или другие поля SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4b693-p107">This condition is initially displayed in a workflow step as **If field equals value**. Use this condition to compare the value in a field in the current item (that is, the item that the list or reusable list workflow is currently running on) to another value. Values can be static text, dynamic strings, or lookups to variables, to context information, or to other SharePoint fields.</span></span>
  
    
    
<span data-ttu-id="4b693-p108">Щелкните **поле**, чтобы просмотреть список параметров. Доступные параметры для **поля** зависят от типа контента, списка, библиотеки или сайта, к которым связана рабочего процесса. Например рабочего процесса, который связан в библиотеке по умолчанию будут иметь параметров полей, например, **заголовок**, **создано** и **Кем создан**.</span><span class="sxs-lookup"><span data-stu-id="4b693-p108">You can click **field** to see the list of options. The available options for **field** depend on the content type, list, library, or site that the workflow is associated to. For example, a workflow that is associated to a default library will have field options such as **Title**, **Created**, and **Created By**.</span></span>
  
    
    
<span data-ttu-id="4b693-p109">Можно выбрать из диапазона операторов в условие, а также **содержит** **больше, чем**. Прежде чем устанавливать оператор, необходимо сначала выбрать значение для **поля** и нажмите кнопку **равно**. Какие операторы доступны зависит от **поля**. Например если диалоговом окне поиска используется для задания **поля** в тип данных даты и времени, например **создано**, **оператор** не указана в качестве параметр.</span><span class="sxs-lookup"><span data-stu-id="4b693-p109">You can select from a range of operators in your condition, including **contains** and **is greater than**. Before you select an operator, you must first select a value for **field**, and then click **equals**. Which operators are available depends on the **field** setting. For example, if you used the lookup dialog to set **field** to a Date and Time data type, such as **Created**, the **Contains** operator is not listed as an option.</span></span>
  
    
    
<span data-ttu-id="4b693-p110">Существует два варианта **равняется** и **содержит** операторы. Операторы **равенства** и **содержит** зависят от регистра символов, во время **равно (без учета регистра)** и **содержит (без учета регистра букв)** регистр не учитывается. Например если значение **поля** **заголовка** и затем использовать оператор **содержит** и **значение** в вашей условие являетсядокументом, затем условие имеет значение true только в том случае, если название содержит документас заглавной буквы D, а не в том случае, если он содержит только документбез капитала г. Если используется оператор **содержит (без учета регистра букв)** вместо условие имеет значение true для заголовков, содержащийдокументов идокументов либо оба.</span><span class="sxs-lookup"><span data-stu-id="4b693-p110">There are two variations of the **equals** and **contains** operators. The **equals** and **contains** operators are case-sensitive, while the **equals (ignoring case)** and **contains (ignoring case)** are not case-sensitive. For example, if you set **field** to **Title** and then use the **contains** operator, and if the **value** in your condition isDocument, then the condition is true only if the title contains Document, with a capital D, and not if it contains only document, without a capital D. If you use the **contains (ignoring case)** operator instead, then the condition is true for titles containing eitherDocument ordocument or both.</span></span>
  
    
    
<span data-ttu-id="4b693-p111">Параметр выбирается для **значения** зависит от в некоторой степени какие **поля** задано значение. Например, предположим **, что вы в поле** **создано**, и затем найдите **значение** с помощью переменной, которая является строка, например, **Последние 10 символов**. Возможно, следует возвращать строку **Как даты и времени**, таким образом, сравнение с **Created** возвращал предсказуемые результаты.</span><span class="sxs-lookup"><span data-stu-id="4b693-p111">The option that you choose for **value** also depends to some extent on what **field** is set to. For example, suppose that you set **field** to **Created**, and then you look up the **value** by using a variable that is a string, such as **Last 10 Characters**. You would probably want to return the string **As Date/Time**, so that the comparison with **Created** will return predictable results.</span></span>
  
    
    

> <span data-ttu-id="4b693-160">**Примечание:** Можно использовать логические операторы, такие как**||**(или) или ** &amp; ** (и) в условии.</span><span class="sxs-lookup"><span data-stu-id="4b693-160">**Note:** You can use logical operators such as**||**(or) or **&amp;&amp;** (and) in the condition.</span></span>
  
    
    

<span data-ttu-id="4b693-p112">Ниже приведены примеры как может выглядеть условие в действии рабочего процесса. (Обратите внимание, что в первом примере ** меньше, чем** означает «раньше, чем».)</span><span class="sxs-lookup"><span data-stu-id="4b693-p112">Following are examples of what the condition might look like in a workflow step. (Note that in the first example, **is less than** is interpreted to mean "earlier than".)</span></span>
  
    
    

- <span data-ttu-id="4b693-163">Если текущего элемента: изменить меньше, чем1/1/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="4b693-163">If Current Item:Modifiedis less than1/1/2010 12:00:00 AM</span></span>
    
  
- <span data-ttu-id="4b693-164">Если Текущий элемент: путьсодержит (без учета регистра букв)маркетинга || Общественностью</span><span class="sxs-lookup"><span data-stu-id="4b693-164">If Current Item:Pathcontains (ignoring case)Marketing || Public Relations</span></span>
    
  

### <a name="created-by-a-specific-person"></a><span data-ttu-id="4b693-165">Создан конкретным пользователем</span><span class="sxs-lookup"><span data-stu-id="4b693-165">Created by a specific person</span></span>

<span data-ttu-id="4b693-p113">Это условие сначала отображается в действии рабочего процесса как **Если создан конкретным пользователем**. Используйте это условие для обнаружения, был ли создан элемент по указанному пользователю. Можно указать либо введя их пользователя имя или адрес электронной почты вручную пользователя (например, Olivier@contoso.com) или путем выбора пользователя из числа пользователей в списке SharePoint, Exchange или Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b693-p113">This condition is initially displayed in a workflow step as **If created by specific person**. Use this condition to discover whether an item was created by a specified user. You can specify the user either by entering their user name or email address manually (for example, Olivier@contoso.com) or by selecting the user from among users already listed in SharePoint, Exchange, or Active Directory.</span></span>
  
    
    

> <span data-ttu-id="4b693-169">**Примечание:** Так как имя пользователя и адрес электронной почты с учетом регистра, рекомендуется использовать последний метод для обеспечения правильного случаев.</span><span class="sxs-lookup"><span data-stu-id="4b693-169">**Note:** Because both the user name and the e-mail address are case sensitive, it is recommended that you use the latter method to ensure correct cases.</span></span> <span data-ttu-id="4b693-170">Если необходимо ввести имя пользователя или адрес электронной почты вручную, нужно незначительно отличаться от случаев.</span><span class="sxs-lookup"><span data-stu-id="4b693-170">If you must enter a user name or e-mail address manually, be careful to match the cases precisely.</span></span> <span data-ttu-id="4b693-171">Например, условие **Если созданные contoso\\Ольга** не вычисляет значение true, если учетная запись пользователя в качестве Contoso\\Алексей.</span><span class="sxs-lookup"><span data-stu-id="4b693-171">For example, the condition **If created by contoso\\molly** does not evaluate as true if the user account is registered as Contoso\\Molly.</span></span>
  
    
    

<span data-ttu-id="4b693-172">Ниже приведен пример как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-172">Following is an example of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-173">Если создан с помощью Алексей Орехов</span><span class="sxs-lookup"><span data-stu-id="4b693-173">If created by Molly Clark</span></span>
    
  

### <a name="created-in-a-specific-date-span"></a><span data-ttu-id="4b693-174">Создан в конкретном диапазоне дат</span><span class="sxs-lookup"><span data-stu-id="4b693-174">Created in a specific date span</span></span>

<span data-ttu-id="4b693-p115">Это условие сначала отображается в действии рабочего процесса как **Если создано между датами и**. Используйте это условие для обнаружения, был ли создан элемент между двумя заданными датами. Можно использовать текущую дату, определенной даты или результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="4b693-p115">This condition is initially displayed in a workflow step as **If created between date and date**. Use this condition to discover whether an item was created between two specified dates. You can use the current date, a specified date, or the result of a lookup.</span></span>
  
    
    
<span data-ttu-id="4b693-178">Ниже приведен пример как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-178">Following is an example of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-179">Если создано между 1/1/2009 и1/1/2010 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="4b693-179">If created between 1/1/2009 and1/1/2010 12:00:00 AM</span></span>
    
  

### <a name="modified-by-a-specific-person"></a><span data-ttu-id="4b693-180">Изменено определенным человеком</span><span class="sxs-lookup"><span data-stu-id="4b693-180">Modified by a specific person</span></span>

<span data-ttu-id="4b693-p116">Это условие сначала отображается в действии рабочего процесса как **Если изменен конкретным пользователем**. Используйте это условие для обнаружения, был ли элемент изменен с указанного пользователя. Пользователь может указан как адрес электронной почты, например olivier@contoso.com, или выборе от пользователей SharePoint, Exchange и Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b693-p116">This condition is initially displayed in a workflow step as **If modified by specific person**. Use this condition to discover whether an item was modified by a specified user. The user can be specified as an e-mail address, such as olivier@contoso.com, or selected from SharePoint, Exchange, or Active Directory users.</span></span>
  
    
    

> <span data-ttu-id="4b693-184">**Примечание:** Адрес электронной почты и имя пользователя, с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="4b693-184">**Note:** The user name and e-mail address are case sensitive.</span></span> <span data-ttu-id="4b693-185">Рекомендуется выбрать пользователя имя или адрес электронной почты для убедитесь, что используется правильный регистр.</span><span class="sxs-lookup"><span data-stu-id="4b693-185">It is recommended that you select a user name or e-mail address to help ensure that you use the correct case.</span></span> <span data-ttu-id="4b693-186">При вводе пользователем имя или адрес электронной почты, должен соответствовать регистру учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4b693-186">If you type a user name or e-mail address, you must match the case of the account.</span></span> <span data-ttu-id="4b693-187">Например **Если создателем является contoso\\Ольга** не будет оценивать значение true, если учетная запись пользователя является Contoso\\Алексей.</span><span class="sxs-lookup"><span data-stu-id="4b693-187">For example, **If modified by contoso\\molly** will not evaluate as true if the user account is Contoso\\Molly.</span></span>
  
    
    

<span data-ttu-id="4b693-188">Ниже приведен пример как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-188">Following is an example of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-189">Если создателем является Алексей Орехов</span><span class="sxs-lookup"><span data-stu-id="4b693-189">If modified by Molly Clark</span></span>
    
  

### <a name="modified-in-a-specific-date-span"></a><span data-ttu-id="4b693-190">Изменено в рамках определенного диапазона дат</span><span class="sxs-lookup"><span data-stu-id="4b693-190">Modified in a specific date span</span></span>

<span data-ttu-id="4b693-p118">Это условие сначала отображается в действии рабочего процесса как **Если произошло в период с date до date**. Используйте это условие для обнаружения, был ли элемент изменен между двумя заданными датами. Для каждого из значений даты можно использовать текущую дату, определенной даты или результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="4b693-p118">This condition is initially displayed in a workflow step as **If modified between date and date**. Use this condition to discover whether an item was modified between two specified dates. For each of the date values, you can use the current date, a specified date, or the result of a lookup.</span></span>
  
    
    
<span data-ttu-id="4b693-194">Ниже приведен пример как может выглядеть условие в действии рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="4b693-194">Following is an example of what the condition might look like in a workflow step,</span></span>
  
    
    

- <span data-ttu-id="4b693-195">Если произошло в период с 1/1/2009 и1/1/2009 г., 12:00:00 AM</span><span class="sxs-lookup"><span data-stu-id="4b693-195">If modified between 1/1/2009 and1/1/2009 12:00:00 AM</span></span>
    
  

### <a name="person-is-a-valid-sharepoint-user"></a><span data-ttu-id="4b693-196">Пользователь является допустимым пользователем SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b693-196">Person is a valid SharePoint user</span></span>

<span data-ttu-id="4b693-p119">Это условие сначала отображается в действии рабочего процесса как **Если пользователь является допустимым пользователем SharePoint**. Это условие можно используйте для определения, является ли указанный пользователь членом сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4b693-p119">This condition is initially displayed in a workflow step as **If person is a valid SharePoint user**. Use this condition to discover whether the specified user is a member of the SharePoint site.</span></span>
  
    
    
<span data-ttu-id="4b693-p120">В SharePoint Designer 2013 может включать людей за пределами корпоративного домена (называемые внешних участников) в рабочих процессах. Например предположим, которым назначен задачи рабочего процесса, внешним участникам. Затем можно использовать эту операцию чтобы сделать пользователя сайта обратитесь к внешним участникам до завершения задачи.</span><span class="sxs-lookup"><span data-stu-id="4b693-p120">In SharePoint Designer 2013, you can include people outside your corporate domain (called external participants) in your workflows. For example, suppose that you have assigned tasks in your workflow to external participants. You can then use this action to make a site user follow up with the external participants until the tasks are complete.</span></span>
  
    
    
<span data-ttu-id="4b693-202">Ниже приведен пример как может выглядеть условие в действии рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="4b693-202">Following is an example of what the condition might look like in a workflow step,</span></span>
  
    
    

- <span data-ttu-id="4b693-203">Если Алексей Орехов является допустимым пользователем SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b693-203">If Molly Clark is a valid SharePoint user</span></span>
    
  
<span data-ttu-id="4b693-p121">Условие **пользователь является допустимым пользователем SharePoint**  это один из двух условий, доступных при работе в рабочий процесс сайта другое  **Если любое значение равно указанному значению**. Дополнительные сведения о рабочих процессов сайта в разделе  [Условия доступны в рамках рабочего процесса сайта](workflow-conditions-quick-reference-sharepoint-2010-workflow-platform.md#section5) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b693-p121">The **Person is a valid SharePoint user** condition is one of only two conditions available when you are working in a site workflow, the other being **If any value equals value**. For more information about site workflows, see the  [Conditions available within a site workflow](workflow-conditions-quick-reference-sharepoint-2010-workflow-platform.md#section5) section in this article.</span></span>
  
    
    

### <a name="title-field-contains-keywords"></a><span data-ttu-id="4b693-206">Поле заголовка содержит ключевые слова</span><span class="sxs-lookup"><span data-stu-id="4b693-206">Title field contains keywords</span></span>

<span data-ttu-id="4b693-p122">Это условие сначала отображается в действии рабочего процесса как **Если название содержит ключевые слова**. Используйте это условие для обнаружения, содержит ли поле **заголовка** элемента указанный текст. Можно указать текст в Построитель строк (как статические значения, как динамической строки или сочетание двух) или вставить подстановки для поля или переменной.</span><span class="sxs-lookup"><span data-stu-id="4b693-p122">This condition is initially displayed in a workflow step as **If title field contains keywords**. Use this condition to discover whether the **Title** field for an item contains specified text. You can either specify the text in the String Builder (as a static value, as a dynamic string, or as a combination of the two) or insert a lookup to a field or variable.</span></span>
  
    
    

> <span data-ttu-id="4b693-210">**Примечание:** При использовании условие **Название содержит ключевые слова** , не могут поиска для более чем одного ключевые слова.</span><span class="sxs-lookup"><span data-stu-id="4b693-210">**Note:** When using the **Title field contains keywords** condition, you cannot search for more than a single keyword text.</span></span> <span data-ttu-id="4b693-211">Для поиска нескольких, тексты альтернативный ключевое слово, можно использовать логические операторы таких как**||**(или) и ** &amp; ** (и) в одном из двух следующих условий: **Если любое значение равно указанному значению** и, **Если текущее поле элемента равно указанному значению**.</span><span class="sxs-lookup"><span data-stu-id="4b693-211">To search for multiple, alternative keyword texts, you can use logical operators such as**||**( or) and **&amp;&amp;** (and) in either of the following two conditions: **If any value equals value** and **If current item field equals value**.</span></span> <span data-ttu-id="4b693-212">(Используйте последнее условие, если нужно найти в поле **Название** только).</span><span class="sxs-lookup"><span data-stu-id="4b693-212">(Use the latter condition if you want to search in the **Title** field only).</span></span> <span data-ttu-id="4b693-213">Например, увидеть следующее изображение: ></span><span class="sxs-lookup"><span data-stu-id="4b693-213">For an example, see the following image:></span></span> 
  
    
    
![Логические операторы, используемые для поиска ключевых слов](../images/spd15-wf-logical-ops.JPG)
  
    
    

  
    
    

  
    
    

  
    
    


## <a name="conditions-available-only-within-an-impersonation-step"></a><span data-ttu-id="4b693-215">Условия доступны только в пределах шаг олицетворения</span><span class="sxs-lookup"><span data-stu-id="4b693-215">Conditions available only within an impersonation step</span></span>
<span data-ttu-id="4b693-216"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="4b693-216"><a name="section3"> </a></span></span>

<span data-ttu-id="4b693-p124">По умолчанию при запуске рабочего процесса вручную использует разрешения человека, который запускает его. Но что делать, если сотрудник, который запускает его не обладать достаточными правами для одной или нескольких операций, которые следует выполнить рабочий процесс? Например: что делать, если рабочий процесс в некоторых случаях потребуется архивирование документа в библиотеку, для которой сотрудник, который запускает рабочий процесс может иметь только чтения уровень разрешений, который не включает разрешение в архив?</span><span class="sxs-lookup"><span data-stu-id="4b693-p124">By default, when a workflow is started manually it uses the permissions of the person who starts it. But what if the person who starts it doesn't have adequate rights for one or more of the operations that the workflow will need to perform? For example: What if the workflow will sometimes need to archive a document to a library for which the person who starts the workflow might have only the Read permission level, which does not include permission to archive?</span></span> 
  
    
    
<span data-ttu-id="4b693-220">В таких случаях можно использовать один или несколько олицетворения, описанных в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="4b693-220">In such cases, you can use one or more impersonation steps in the workflow.</span></span> <span data-ttu-id="4b693-221">Шаг олицетворения использует разрешения пользователя, который последним сохранения шаблона рабочего процесса. Обычно автора шаблон, который будут иметь необходимые разрешения для всех операций рабочего процесса, в том числе в данном случае разрешений в архив документов с соответствующей библиотекой.</span><span class="sxs-lookup"><span data-stu-id="4b693-221">An impersonation step uses the permissions of the person who most recently saved the workflow template???typically the author of the template, who would typically have the needed permissions for all of the workflow's operations, including in this case permission to archive the document to the appropriate library.</span></span> 
  
    
    

> <span data-ttu-id="4b693-222">**Примечание:** Для обоих этих условий *всех* указанных пользователей и групп необходимо передать сравнения условия для принимают значение True. > для оба эти условия не имеет ли указанный разрешения были назначены * явным образом* указанного отдельным пользователям или ли разрешения удерживаемые этих отдельных пользователей только *неявно* (как члены группы, к которой назначены разрешения, например). Для указанной *группы* , с другой стороны, разрешения необходимо назначить *явным образом* и *не* наследуется от родительской группы.</span><span class="sxs-lookup"><span data-stu-id="4b693-222">**Note:** For both of these conditions, *all*  of the specified users and groups must pass the comparison in order for the condition to evaluate to True.>  For both of these conditions, it does not matter whether the specified permissions have been assigned *explicitly*  to the specified individual users or whether the permissions are held by those individual users only *implicitly*  (as members of a group to which the permissions have been assigned, for instance).For specified *groups*  , on the other hand, the permissions must have been assigned *explicitly*  and *not*  inherited from a parent group.</span></span>
  
    
    


### <a name="check-list-item-permissions"></a><span data-ttu-id="4b693-223">Проверка разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="4b693-223">Check list item permissions</span></span>

<span data-ttu-id="4b693-224">Это условие сначала отображается в шаг олицетворения как **наличие по крайней мере этих разрешений на элемент в этом списке разрешения для этих пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4b693-224">This condition is initially displayed in an impersonation step as **If permissions for these users are at least these permissions on item in this list**.</span></span> 
  
    
    
<span data-ttu-id="4b693-225">Используйте это условие для обнаружения ли, для указанного списка или библиотеки,  *отдельные разрешения*  , что каждый указанный пользователь и группа содержит включают все *отдельные разрешения*  , которые включены в уровень безопасности или уровней.</span><span class="sxs-lookup"><span data-stu-id="4b693-225">Use this condition to discover whether, for the specified list or library, the  *individual permissions*  that each specified user and group holds include all of the *individual permissions*  that are included in the specified security level or levels.</span></span>
  
    
    
 <span data-ttu-id="4b693-226">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="4b693-226">**Examples**</span></span>
  
    
    

- <span data-ttu-id="4b693-p126">Пользователь или группа имеет только уровень разрешений чтение списка, но условие указывает уровень утвердить. Уровень чтение  *не*  включают все разрешения, которые включены в уровень утвердить, поэтому в данном случае условие как False.</span><span class="sxs-lookup"><span data-stu-id="4b693-p126">A user or group has only the Read permission level for a list, but the condition specifies the Approve level. The Read level does  *not*  include all of the permissions that are included in the Approve level, so in this case the condition evaluates as False.</span></span>
    
  
- <span data-ttu-id="4b693-p127">Другой пользователь или группа, обладает уровнем разрешений полный доступ для тот же список. Полный доступ уровня  *does*  включает все разрешения, которые включены в уровень утверждение (а также другие разрешения), и поэтому этот раз условие значение true.</span><span class="sxs-lookup"><span data-stu-id="4b693-p127">Another user or group has the Full Control permission level for the same list. The Full Control level  *does*  include all of the permissions that are included in the Approve level (as well as other permissions), and so this time the condition evaluates as True.</span></span>
    
  
<span data-ttu-id="4b693-231">Ниже приведен пример как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-231">Following is an example of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-232">Если разрешения для Членов Contoso , по крайней меречтения элемента вТекущем элементов</span><span class="sxs-lookup"><span data-stu-id="4b693-232">If permissions for Contoso Members are at leastRead on item inCurrent Items</span></span>
    
  

### <a name="check-list-item-permission-levels"></a><span data-ttu-id="4b693-233">Проверка уровней разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="4b693-233">Check list item permission levels</span></span>

<span data-ttu-id="4b693-234">Это условие сначала отображается в шаг олицетворения как **наличие по крайней мере эти уровни разрешений на элемент в этом списке уровней разрешений для этих пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4b693-234">This condition is initially displayed in an impersonation step as **If permission levels for these users are at least these permission levels on item in this list**.</span></span> 
  
    
    
<span data-ttu-id="4b693-p128">Используйте это условие для обнаружения, для указанного списка или библиотеки, каждый указанный пользователь и группа была ли  *явно*  назначить разрешение *уровня или уровней*  . Разрешения предоставлены только *неявно*  (например, с помощью члена группы, назначенных разрешения), *не*  считаются, это условие, а не отдельные разрешения удерживаемые указанных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="4b693-p128">Use this condition to discover whether, for the specified list or library, each specified user and group has been  *explicitly*  assigned the specified permission *level or levels*  . Permissions held only *implicitly*  (for instance, by a member of a group to which the permissions have been assigned) are *not*  considered by this condition, and neither are the individual permissions held by the specified users and groups.</span></span>
  
    
    
 <span data-ttu-id="4b693-237">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="4b693-237">**Examples**</span></span>
  
    
    

- <span data-ttu-id="4b693-p129">Пользователь явным образом назначена только уровнем разрешений полный доступ для списка, но только на уровне чтения указывает условие. Даже если пользователь  *содержит*  все отдельные разрешения, которые включены в уровень чтение, пользователь не были *явно*  назначить уровень чтение, чтобы условие имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="4b693-p129">A user has been explicitly assigned only the Full Control permission level for a list, but the condition specifies only the Read level. Even though the user  *holds*  all of the individual permissions that are included in the Read level, the user not been *explicitly*  assigned the Read level, so the condition evaluates as False.</span></span>
    
  
- <span data-ttu-id="4b693-p130">Другой пользователь явным образом назначена только уровень разрешений проекта для другого списка, но условие указывает уровень структуры и уровень управления иерархии. Так как пользователь был назначен только один из двух уровней обязательные, условие значение false.</span><span class="sxs-lookup"><span data-stu-id="4b693-p130">A different user has been explicitly assigned only the Design permission level for a different list, but the condition specifies both the Design level and the Manage Hierarchy level. Because the user has been assigned only one of the two required levels, the condition evaluates as False.</span></span>
    
  
- <span data-ttu-id="4b693-p131">Третий список пользователь является членом группы участников и наследует разрешения этой группе. Тем не менее не уровень разрешений не  *явно*  назначенных пользователю. Условие требуются *явные назначения*  участие уровня, так как пользователь удерживает разрешения этого уровня только неявно, еще раз условие значение False.</span><span class="sxs-lookup"><span data-stu-id="4b693-p131">For a third list, a user is a member of the Members group and inherits permissions from that group. However, no permissions level has been  *explicitly*  assigned to the user. The condition requires *explicit assignment*  of the Contribute level, so because the user holds the permissions of that level only implicitly, the condition again evaluates to False.</span></span>
    
  
<span data-ttu-id="4b693-245">Ниже приведен пример как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-245">Following is an example of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-246">Если уровни разрешений для Членов Contoso , по крайней меречтения элемента вТекущем элементов</span><span class="sxs-lookup"><span data-stu-id="4b693-246">If permission levels for Contoso Members are at leastRead on item inCurrent Items</span></span>
    
  

## <a name="conditions-available-only-when-the-workflow-is-associated-to-a-library-or-the-document-content-type"></a><span data-ttu-id="4b693-247">Условия доступны только в том случае, когда рабочий процесс связан библиотеки или типа контента документа</span><span class="sxs-lookup"><span data-stu-id="4b693-247">Conditions available only when the workflow is associated to a library or the Document content type</span></span>
<span data-ttu-id="4b693-248"><a name="section4"> </a></span><span class="sxs-lookup"><span data-stu-id="4b693-248"><a name="section4"> </a></span></span>

<span data-ttu-id="4b693-249">Условия, **размер файла находится в конкретном диапазоне Кбайт** и **Тип файла имеет конкретный тип** доступны только в том случае, если рабочий процесс связан с библиотеки или типа контента документа.</span><span class="sxs-lookup"><span data-stu-id="4b693-249">The conditions **The file size is a specific range kilobytes** and **The file type is a specific type** are available only when your workflow is associated with a Library or the Document content type.</span></span>
  
    
    

### <a name="the-file-size-in-a-specific-range-of-kilobytes"></a><span data-ttu-id="4b693-250">Размер файла в конкретный диапазон КБ</span><span class="sxs-lookup"><span data-stu-id="4b693-250">The file size in a specific range of kilobytes</span></span>

<span data-ttu-id="4b693-p132">Это условие сначала отображается в действии рабочего процесса как **Если размер файла находится между size и size КБ**. Используйте это условие для обнаружения, попадает ли размер файла документа между двумя указанного размера, измеряется в килобайтах. Условие не включает указанного размера в расчет. Для каждого экземпляра **размера** можно ввести номер или использовать подстановки.</span><span class="sxs-lookup"><span data-stu-id="4b693-p132">This condition is initially displayed in a workflow step as **If the file size is between size and size kilobytes**. Use this condition to discover whether the file size of a document falls between two specified sizes measured in kilobytes. The condition does not include the specified sizes in the evaluation. For each instance of **size**, you can either enter a number or use a lookup.</span></span>
  
    
    
<span data-ttu-id="4b693-255">Ниже приведен пример как может выглядеть условие в действии рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="4b693-255">Following is an example of what the condition might look like in a workflow step,</span></span>
  
    
    

- <span data-ttu-id="4b693-256">Если размер файла находится в пределах 1023 и1048577 килобайт</span><span class="sxs-lookup"><span data-stu-id="4b693-256">If the file size is between 1023 and1048577 kilobytes</span></span>
    
  

> <span data-ttu-id="4b693-257">**Примечание:** Указанные верхние и нижние границы не включаются в определенном диапазоне.</span><span class="sxs-lookup"><span data-stu-id="4b693-257">**Note:** The specified upper and lower limits are not included in the defined range.</span></span> <span data-ttu-id="4b693-258">В приведенном ниже примере, файл размером не 1023 КБ будет интерпретируются как значение false, так как он не между 1023 и 1048577.</span><span class="sxs-lookup"><span data-stu-id="4b693-258">In the example given here, a file that is 1023 KB would evaluate as false because it is not between 1023 and 1048577.</span></span> 
  
    
    


### <a name="the-file-type-is-a-specific-type"></a><span data-ttu-id="4b693-259">Файл имеет конкретный тип</span><span class="sxs-lookup"><span data-stu-id="4b693-259">The file type is a specific type</span></span>

<span data-ttu-id="4b693-p134">Это условие изначально отображается в шаг рабочего процесса как **Если тип файла имеет значение определенного типа**. Используйте это условие для обнаружения, является ли тип файла текущего элемента указанного типа (например, docx. Можно ввести тип файла в виде строки или использовать подстановки.</span><span class="sxs-lookup"><span data-stu-id="4b693-p134">This condition initially displays in a workflow step as **If the file type is specific type**. Use this condition to discover whether the file type of the current item is the specified type, (such as docx. You can either enter the file type as a string or use a lookup.</span></span>
  
    
    
<span data-ttu-id="4b693-263">Ниже приведен пример как может выглядеть условие в действии рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="4b693-263">Following is an example of what the condition might look like in a workflow step:</span></span>
  
    
    

- <span data-ttu-id="4b693-264">Если файл относится к типу docx</span><span class="sxs-lookup"><span data-stu-id="4b693-264">If the file type is docx</span></span>
    
  

## <a name="conditions-available-within-a-site-workflow"></a><span data-ttu-id="4b693-265">Условия доступны в рамках рабочего процесса сайта</span><span class="sxs-lookup"><span data-stu-id="4b693-265">Conditions available within a site workflow</span></span>
<span data-ttu-id="4b693-266"><a name="section5"> </a></span><span class="sxs-lookup"><span data-stu-id="4b693-266"><a name="section5"> </a></span></span>

<span data-ttu-id="4b693-p135">Рабочие процессы сайта работают на уровне сайта и не связаны с элементом списка. При работе в рабочий процесс сайта доступны только следующие условия. (Все другие условия SharePoint Designer 2013 работают с элементов списка, и поэтому ни один из них работает в рабочие процессы сайта).</span><span class="sxs-lookup"><span data-stu-id="4b693-p135">Site workflows operate at the site level and are not associated with a list item. When you are working in a site workflow, only the following conditions are available. (All other conditions in SharePoint Designer 2013 operate on list items, and therefore none of them function in site workflows.)</span></span>
  
    
    

- <span data-ttu-id="4b693-270">**Если любое значение равно указанному значению**</span><span class="sxs-lookup"><span data-stu-id="4b693-270">**If any value equals value**</span></span>
    
  
- <span data-ttu-id="4b693-271">**Пользователь является допустимым пользователем SharePoint**</span><span class="sxs-lookup"><span data-stu-id="4b693-271">**Person is a valid SharePoint user**</span></span>
    
  
<span data-ttu-id="4b693-272">Изнутри олицетворение шаг в рабочий процесс сайта:</span><span class="sxs-lookup"><span data-stu-id="4b693-272">From within an impersonation step in a site workflow:</span></span>
  
    
    

- <span data-ttu-id="4b693-273">**Проверка разрешений для элемента списка**</span><span class="sxs-lookup"><span data-stu-id="4b693-273">**Check list item permissions**</span></span>
    
  
- <span data-ttu-id="4b693-274">**Проверка уровней разрешений для элемента списка**</span><span class="sxs-lookup"><span data-stu-id="4b693-274">**Check list item permission levels**</span></span>
    
  
- <span data-ttu-id="4b693-275">**Пользователь является допустимым пользователем SharePoint**</span><span class="sxs-lookup"><span data-stu-id="4b693-275">**Person is a valid SharePoint user**</span></span>
    
  
<span data-ttu-id="4b693-276">Дополнительные сведения об условиях см в разделе  [Общие условия](workflow-conditions-quick-reference-sharepoint-2010-workflow-platform.md#section2) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b693-276">For more information about conditions, see the  [General conditions](workflow-conditions-quick-reference-sharepoint-2010-workflow-platform.md#section2) section of this article.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="4b693-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4b693-277">Additional resources</span></span>
<span data-ttu-id="4b693-278"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4b693-278"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="4b693-279">Что нового в рабочих процессах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b693-279">What's new in workflows for SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [<span data-ttu-id="4b693-280">Общие сведения о рабочих процессах в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4b693-280">Get started with workflows in SharePoint</span></span>](get-started-with-workflows-in-sharepoint.md)
    
  
-  [<span data-ttu-id="4b693-281">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="4b693-281">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  

  
    
    

