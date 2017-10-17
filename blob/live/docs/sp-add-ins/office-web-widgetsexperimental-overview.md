---
title: "Обзор экспериментальных мини-приложений Office для веб-страниц"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 40770129baa7606b7e3ebf6fb7d99cefabf51df7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="office-web-widgets---experimental-overview"></a><span data-ttu-id="91fc8-102">Обзор экспериментальных мини-приложений Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="91fc8-102">Office Web Widgets - Experimental overview</span></span>
<span data-ttu-id="91fc8-103">Сведения об экспериментальных мини-приложениях Office для веб-страниц, которые можно использовать в надстройках Office и SharePoint, а также на веб-сайтах.</span><span class="sxs-lookup"><span data-stu-id="91fc8-103">Learn about the Office Web Widgets - Experimental that you can use in Office Add-ins, SharePoint Add-ins, and websites.</span></span>
 

 <span data-ttu-id="91fc8-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="91fc8-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="91fc8-p102">**Внимание!** Экспериментальные мини-приложения Office для веб-страниц предоставляются только в целях исследований и обратной связи. Не следует использовать их в производственных сценариях. Режим работы мини-приложений Office для веб-страниц может существенно измениться в будущих выпусках. Ознакомьтесь с [условиями лицензии на экспериментальные мини-приложения Office для веб-страниц](office-web-widgetsexperimental-license-terms.md).</span><span class="sxs-lookup"><span data-stu-id="91fc8-p102">**Caution**  The Office Web Widgets - Experimental are only provided for research and feedback purposes. Do not use in production scenarios. The Office Web Widgets behavior may change significantly in future releases. Read and review the  [Office Web Widgets - Experimental License Terms](office-web-widgetsexperimental-license-terms.md).</span></span>
 


<span data-ttu-id="91fc8-111">Клиентские элементы управления, такие как экспериментальная версия веб-виджетов Office, могут значительно ускорить разработку надстроек, а также повысить их качество. Для этого мы должны быть уверены, что виджеты отвечают определенным критериям:</span><span class="sxs-lookup"><span data-stu-id="91fc8-111">Client controls, such as the Office Web Widgets - Experimental, can greatly reduce the amount of time required to build add-ins, and at the same time, increase the quality of the add-ins. For this to be true, we have to be sure the widgets meet certain criteria:</span></span>
 


- <span data-ttu-id="91fc8-112">предназначены для использования на любой веб-странице, даже если она не указана в SharePoint;</span><span class="sxs-lookup"><span data-stu-id="91fc8-112">Widgets must be designed to be used in any webpage, even if the page is not hosted on SharePoint.</span></span>
    
 
- <span data-ttu-id="91fc8-p103">работают в среде выполнения элементов управления Office. Это позволяет нам предоставлять общий набор требований и согласованный синтаксис для использования виджетов;</span><span class="sxs-lookup"><span data-stu-id="91fc8-p103">Widgets work within the Office controls runtime. This lets us to provide a common set of requirements and a consistent syntax to use the widgets.</span></span>
    
 
- <span data-ttu-id="91fc8-p104">виджеты, которые обращаются к SharePoint, используют междоменную библиотеку. Виджеты не зависят от определенной платформы или технологии на стороне сервера. Вы можете использовать виджеты независимо от того, какая у вас серверная технология;</span><span class="sxs-lookup"><span data-stu-id="91fc8-p104">Widgets that communicate back to SharePoint use the cross-domain library. The widgets don't have a dependency on a particular server-side platform or technology. You can use the widgets regardless of your choice of server technology.</span></span>
    
 
- <span data-ttu-id="91fc8-p105">должны сосуществовать с другими элементами на странице. Добавление виджета на страницу не должно изменять другие ее элементы;</span><span class="sxs-lookup"><span data-stu-id="91fc8-p105">Widgets must coexist with other elements in the page. The inclusion of the widget to a page should not modify other elements in it.</span></span>
    
 
- <span data-ttu-id="91fc8-p106">должны хорошо работать со всеми существующими платформами. Мы хотим, чтобы вы по-прежнему могли использовать привычные инструменты и технологии.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p106">Play nice with existing frameworks. We want to be sure you can still use the tools and technologies that you are used to.</span></span>
    
 

<span data-ttu-id="91fc8-122">**Рис. 1. Надстройка, использующая экспериментальные мини-приложения Office для веб-страниц**</span><span class="sxs-lookup"><span data-stu-id="91fc8-122">**Figure 1. An add-in using Office Web Widgets - Experimental**</span></span>

 

 
![Мини-приложения Office для веб-страниц — экспериментальная демоверсия](../images/OfficeWebWidgetsOverview_demo.png)
 
<span data-ttu-id="91fc8-p107">Мини-приложения можно использовать, установив пакет NuGet **Экспериментальные мини-приложения Office для веб-страниц** из Visual Studio. Дополнительные сведения см. в статье [Управление пакетами NuGet с помощью диалогового окна](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). Кроме того, просмотрите [страницу коллекции NuGet](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="91fc8-p107">You can use the widgets by installing the  **Office Web Widgets - Experimental** NuGet package from Visual Studio For more information, see [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog). You can also browse the  [NuGet gallery page](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>
 
<span data-ttu-id="91fc8-p108">Ваши отзывы и комментарии помогли нам решить, какие мини-приложения необходимы. Как показано на рисунке 1, вы уже можете испытать мини-приложения (1) "Выбор людей" и (2) "Представление списка на рабочем столе", а также поэкспериментировать с ними. Отправляйте свои отзывы на [сайт Office Developer Platform UserVoice](http://officespdev.uservoice.com/)</span><span class="sxs-lookup"><span data-stu-id="91fc8-p108">Your feedback and comments helped us decide what widgets to provide. As you can see in Figure 1, the (1) People Picker and (2) Desktop List View widgets are ready for you to try and experiment. Please keep the feedback coming at the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/)</span></span>
 
<span data-ttu-id="91fc8-129">Кроме того, можно ознакомиться с примером кода [экспериментальной демоверсии мини-приложений Office для веб-страниц](http://code.msdn.microsoft.com/SharePoint-Office-Web-6d44aa9e).</span><span class="sxs-lookup"><span data-stu-id="91fc8-129">You can also see the widgets in action in the  [Office Web Widgets - Experimental Demo](http://code.msdn.microsoft.com/SharePoint-Office-Web-6d44aa9e) code sample.</span></span>
 

## <a name="people-picker-widget"></a><span data-ttu-id="91fc8-130">Мини-приложение "Выбор людей"</span><span class="sxs-lookup"><span data-stu-id="91fc8-130">People Picker widget</span></span>

<span data-ttu-id="91fc8-p109">Используя в надстройках экспериментальный виджет "Выбор людей", вы можете помочь пользователям находить и выбирать людей и группы в клиенте. Когда пользователь вводит текст в текстовом поле, виджет загружает контакты, чьи имена или адреса электронной почты соответствуют запросу.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p109">You can use the experimental People Picker widget in add-ins to help your users find and select people and groups in a tenant. Users can start typing in the text box and the widget retrieves the people whose name or e-mail matches the text.</span></span>
 

 

<span data-ttu-id="91fc8-133">**Рис. 2. Обработка запроса мини-приложением "Выбор людей"**</span><span class="sxs-lookup"><span data-stu-id="91fc8-133">**Figure 2. People Picker widget solving a query**</span></span>

 

 
![Экспериментальный элемент управления "Выбор людей" на странице](../images/PeoplePicker_basic.png)
 
<span data-ttu-id="91fc8-p110">Вы можете объявить мини-приложение в разметке HTML или программным путем, используя JavaScript. В любом случае необходимо использовать элемент **div** в качестве заполнителя для мини-приложения. Вы можете также установить для мини-приложения "Выбор людей" свойства и обработчики событий. В таблице ниже показаны свойства и события доступные в мини-приложении "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="91fc8-p110">You can declare the widget in the HTML markup or programmatically using JavaScript. In either case, you use a  **div** element as a placeholder for the widget. You can also set properties and event handlers for the People Picker widget. The following table shows the available properties and events in the People Picker widget.</span></span>
 

 


|<span data-ttu-id="91fc8-139">**Свойство/Событие**</span><span class="sxs-lookup"><span data-stu-id="91fc8-139">**Property/Event**</span></span>|<span data-ttu-id="91fc8-140">**Тип**</span><span class="sxs-lookup"><span data-stu-id="91fc8-140">**Type**</span></span>|<span data-ttu-id="91fc8-141">**Описание**</span><span class="sxs-lookup"><span data-stu-id="91fc8-141">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="91fc8-142">**objectType**</span><span class="sxs-lookup"><span data-stu-id="91fc8-142">**objectType**</span></span>|<span data-ttu-id="91fc8-143">Объект JSON (список строк)</span><span class="sxs-lookup"><span data-stu-id="91fc8-143">JSON Object (list of strings)</span></span>| <span data-ttu-id="91fc8-p111">Тип элементов, сопоставляемых мини-приложением. Параметры: только "Группа пользователя по умолчанию" и "Пользователь".</span><span class="sxs-lookup"><span data-stu-id="91fc8-p111">Type of items the widget will resolve. Options: User Group Default to user only.</span></span>|
|<span data-ttu-id="91fc8-146">**allowMultipleSelections**</span><span class="sxs-lookup"><span data-stu-id="91fc8-146">**allowMultipleSelections**</span></span>|<span data-ttu-id="91fc8-147">Логический</span><span class="sxs-lookup"><span data-stu-id="91fc8-147">Boolean</span></span>|<span data-ttu-id="91fc8-p112">Истина/Ложь. Если задано значение "Ложь", мини-приложение позволяет выбирать только один элемент за раз. По умолчанию выбрано значение "Ложь".</span><span class="sxs-lookup"><span data-stu-id="91fc8-p112">True/False. If False, the widget should allow selecting only one item at the time.  Default=False.</span></span>|
|<span data-ttu-id="91fc8-151">**rootGroupName**</span><span class="sxs-lookup"><span data-stu-id="91fc8-151">**rootGroupName**</span></span>|<span data-ttu-id="91fc8-152">Строка</span><span class="sxs-lookup"><span data-stu-id="91fc8-152">string</span></span>|<span data-ttu-id="91fc8-p113">Если значение указано, мини-приложение будет выбирать элементы только из этой группы. В противном случае будут отправляться запросы объектам в рамках всего клиента.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p113">If provided, the widget will limit the selection to items in this group.  If not provided, the widget will query objects from the whole tenancy.</span></span>|
|<span data-ttu-id="91fc8-155">**selectedItems**</span><span class="sxs-lookup"><span data-stu-id="91fc8-155">**selectedItems**</span></span>|<span data-ttu-id="91fc8-156">Массив JSON</span><span class="sxs-lookup"><span data-stu-id="91fc8-156">JSON array</span></span>|<span data-ttu-id="91fc8-p114">Список выбранных элементов. Каждый элемент возвращает объект, представляющий пользователя или группу.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p114">List of items selected. Each item will return an object representing a user or group.</span></span>|
|<span data-ttu-id="91fc8-159">**onAdded**</span><span class="sxs-lookup"><span data-stu-id="91fc8-159">**onAdded**</span></span>|<span data-ttu-id="91fc8-160">Функция</span><span class="sxs-lookup"><span data-stu-id="91fc8-160">Function</span></span>|<span data-ttu-id="91fc8-p115">Событие, которое запускается при добавлении объекта к выделенному фрагменту. Функция обработчика получает добавленный объект.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p115">Event that fires when a new object is added to the selection. The handler function received the object added.</span></span>|
|<span data-ttu-id="91fc8-163">**onRemoved**</span><span class="sxs-lookup"><span data-stu-id="91fc8-163">**onRemoved**</span></span>|<span data-ttu-id="91fc8-164">Функция</span><span class="sxs-lookup"><span data-stu-id="91fc8-164">Function</span></span>|<span data-ttu-id="91fc8-p116">Событие, которое запускается при удалении объекта из выделенного фрагмента. Функция обработчика получает удаленный объект.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p116">Event that fires when a new object is removed from the selection. The handler function received the object removed.</span></span>|
|<span data-ttu-id="91fc8-167">**onChange**</span><span class="sxs-lookup"><span data-stu-id="91fc8-167">**onChange**</span></span>|<span data-ttu-id="91fc8-168">Функция</span><span class="sxs-lookup"><span data-stu-id="91fc8-168">Function</span></span>|<span data-ttu-id="91fc8-p117">Это событие вызывается как при добавлении, так и при удалении объектов. В функцию обработчика параметры не передаются.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p117">Either adding or removing objects triggers this event. No parameters are passed to the handler function.</span></span>|
|<span data-ttu-id="91fc8-171">**validationErrors**</span><span class="sxs-lookup"><span data-stu-id="91fc8-171">**validationErrors**</span></span>|<span data-ttu-id="91fc8-172">Массив</span><span class="sxs-lookup"><span data-stu-id="91fc8-172">Array</span></span>| <span data-ttu-id="91fc8-173">Массив возможных ошибок проверки: пустое значение unresolvedItem, tooManyItems</span><span class="sxs-lookup"><span data-stu-id="91fc8-173">Array of possible validation errors: empty unresolvedItem tooManyItems</span></span>|
|<span data-ttu-id="91fc8-174">**autoShowValidationMessage**</span><span class="sxs-lookup"><span data-stu-id="91fc8-174">**autoShowValidationMessage**</span></span>|<span data-ttu-id="91fc8-175">Логический</span><span class="sxs-lookup"><span data-stu-id="91fc8-175">Boolean</span></span>|<span data-ttu-id="91fc8-176">Значение "Истина" указывает, что сообщение о проверке отображается, а значение "Ложь" — не отображается</span><span class="sxs-lookup"><span data-stu-id="91fc8-176">True=Show False=Don't show</span></span>|
|<span data-ttu-id="91fc8-177">**hasErrors**</span><span class="sxs-lookup"><span data-stu-id="91fc8-177">**hasErrors**</span></span>|<span data-ttu-id="91fc8-178">Логический</span><span class="sxs-lookup"><span data-stu-id="91fc8-178">Boolean</span></span>|<span data-ttu-id="91fc8-179">Значение "Истина" указывает, что имеется одна или несколько ошибок проверки. Значение "Ложь" — ошибки проверки отсутствуют</span><span class="sxs-lookup"><span data-stu-id="91fc8-179">True= There are 1 or more validation errors False=There are no validation errors</span></span>|
|<span data-ttu-id="91fc8-180">**errors**</span><span class="sxs-lookup"><span data-stu-id="91fc8-180">**errors**</span></span>|<span data-ttu-id="91fc8-181">Массив</span><span class="sxs-lookup"><span data-stu-id="91fc8-181">Array</span></span>| <span data-ttu-id="91fc8-182">Массив возможных ошибок проверки: пустое значение unresolvedItem, tooManyItems</span><span class="sxs-lookup"><span data-stu-id="91fc8-182">Array of possible validation errors: empty unresolvedItem tooManyItems</span></span>|
|<span data-ttu-id="91fc8-183">**displayErrors**</span><span class="sxs-lookup"><span data-stu-id="91fc8-183">**displayErrors**</span></span>|<span data-ttu-id="91fc8-184">Логический</span><span class="sxs-lookup"><span data-stu-id="91fc8-184">Boolean</span></span>|<span data-ttu-id="91fc8-185">Значение "Истина" указывает, что ошибки отображаются, значение "Ложь" — ошибки не отображаются</span><span class="sxs-lookup"><span data-stu-id="91fc8-185">True=Display the errors False=Don't display the errors</span></span>|
<span data-ttu-id="91fc8-p118">Классы CSS для мини-приложения "Выбор людей" определены в таблице стилей **Office.Controls.css**. Вы можете переопределить классы и настроить стиль мини-приложения для своей надстройки.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p118">The CSS classes for the People Picker widget are defined in the  **Office.Controls.css** style sheet. You can override the classes and style the widget for your add-in.</span></span>
 

 
<span data-ttu-id="91fc8-188">Дополнительные сведения см. в статье  [Использование экспериментального мини-приложения "Выбор людей" в надстройках для SharePoint](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md) и примере кода [Использование экспериментального виджета "Выбор людей" в надстройке](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85.md).</span><span class="sxs-lookup"><span data-stu-id="91fc8-188">For more information, see  [Use the experimental People Picker widget in SharePoint Add-ins](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md) and [Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85.md) code sample.</span></span>
 

 

## <a name="desktop-list-view-widget"></a><span data-ttu-id="91fc8-189">Мини-приложение "Представление списка на рабочем столе"</span><span class="sxs-lookup"><span data-stu-id="91fc8-189">Desktop List View widget</span></span>

<span data-ttu-id="91fc8-190">Пользователи получают все преимущества виджета "Представление списка" и могут представлять данные в списке, как в обычном виджете "Представление списка". Но вы можете использовать его в даже в тех надстройках, которые не размещены в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="91fc8-190">Your users can benefit from the List View widget and display the data in a list just like the regular List View widget, but you can use it in your add-ins that are not necessarily hosted in SharePoint.</span></span>
 

 

<span data-ttu-id="91fc8-191">**Рис. 3. Мини-приложение "Представление списка на рабочем столе", отображающее данные в виде списка**</span><span class="sxs-lookup"><span data-stu-id="91fc8-191">**Figure 3. Desktop List View widget displaying the data in a list**</span></span>

 

 
![Экспериментальный элемент управления "Представление списка на рабочем столе"](../images/DesktopListView_basic.png)
 
<span data-ttu-id="91fc8-193">Вы можете указать существующее представление в списке, мини-приложение обрабатывает поля в том порядке, в котором они отображаются в представлении.</span><span class="sxs-lookup"><span data-stu-id="91fc8-193">You can specify an existing view on the list, the widget renders the fields in the order that they appear in the view.</span></span>
 

 

    
 <span data-ttu-id="91fc8-p119">**Примечание.** На данный момент мини-приложение "Представление списка на рабочем столе" отображает только данные. Оно не предлагает возможности редактирования.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p119">**Note**  At this moment, the Desktop List View widget only displays the data. It doesn't offer editing capabilities.</span></span>
 

<span data-ttu-id="91fc8-p120">Вы можете вставить для мини-приложения заполнитель, используя элемент **div**. Мини-приложение можно использовать программно или декларативно.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p120">You can provide a placeholder for the widget using a  **div** element. You can programmatically or declaratively use the widget.</span></span>
 

 
<span data-ttu-id="91fc8-p121">Вы также можете указать свойства или обработчики событий для виджета "Представление списка на рабочем столе". В следующей таблице показаны доступные свойства и события в виджете "Представление списка на рабочем столе".</span><span class="sxs-lookup"><span data-stu-id="91fc8-p121">You also can set properties or event handlers for the Desktop List View widget. The following table shows the available properties and events in the Desktop List View widget.</span></span>
 

 


|<span data-ttu-id="91fc8-200">**Свойство/Событие**</span><span class="sxs-lookup"><span data-stu-id="91fc8-200">**Property/Event**</span></span>|<span data-ttu-id="91fc8-201">**Тип**</span><span class="sxs-lookup"><span data-stu-id="91fc8-201">**Type**</span></span>|<span data-ttu-id="91fc8-202">**Описание**</span><span class="sxs-lookup"><span data-stu-id="91fc8-202">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="91fc8-203">**listUrl**</span><span class="sxs-lookup"><span data-stu-id="91fc8-203">**listUrl**</span></span>|<span data-ttu-id="91fc8-204">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="91fc8-204">URL</span></span>|<span data-ttu-id="91fc8-p122">URL-адрес списка, из которого необходимо получать элементы. Это может быть относительный URL-адрес (в таком случае он будет считаться расположенным на самом сайте надстройки) или абсолютный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p122">URL of the list view to draw items from. It can be a relative URL in which case it will be assumed to be located on the add-in web itself or an absolute URL.</span></span>|
|<span data-ttu-id="91fc8-207">**viewName**</span><span class="sxs-lookup"><span data-stu-id="91fc8-207">**viewName**</span></span>|<span data-ttu-id="91fc8-208">Строка</span><span class="sxs-lookup"><span data-stu-id="91fc8-208">string</span></span>|<span data-ttu-id="91fc8-p123">Имя представления, которое необходимо отобразить. Это программное, а не отображаемое, имя представления.</span><span class="sxs-lookup"><span data-stu-id="91fc8-p123">Name of the view to show. This is the programmatic name of the view (not its display name).</span></span>|
|<span data-ttu-id="91fc8-211">**onItemSelected**</span><span class="sxs-lookup"><span data-stu-id="91fc8-211">**onItemSelected**</span></span>|<span data-ttu-id="91fc8-212">Функция</span><span class="sxs-lookup"><span data-stu-id="91fc8-212">Function</span></span>|<span data-ttu-id="91fc8-213">Событие, возникающее при выборе элемента из списка.</span><span class="sxs-lookup"><span data-stu-id="91fc8-213">Event that fires when an item is selected on the list.</span></span>|
|<span data-ttu-id="91fc8-214">**onItemAdded**</span><span class="sxs-lookup"><span data-stu-id="91fc8-214">**onItemAdded**</span></span>|<span data-ttu-id="91fc8-215">Функция</span><span class="sxs-lookup"><span data-stu-id="91fc8-215">Function</span></span>|<span data-ttu-id="91fc8-216">Событие, возникающее при добавлении элемента в список.</span><span class="sxs-lookup"><span data-stu-id="91fc8-216">Event that fires when a new item is added to the list.</span></span>|
|<span data-ttu-id="91fc8-217">**onItemRemoved**</span><span class="sxs-lookup"><span data-stu-id="91fc8-217">**onItemRemoved**</span></span>|<span data-ttu-id="91fc8-218">Функция</span><span class="sxs-lookup"><span data-stu-id="91fc8-218">Function</span></span>|<span data-ttu-id="91fc8-219">Событие, возникающее при удалении элемента из списка.</span><span class="sxs-lookup"><span data-stu-id="91fc8-219">Event that fires when an item is removed from the list.</span></span>|
|<span data-ttu-id="91fc8-220">**selectedItems**</span><span class="sxs-lookup"><span data-stu-id="91fc8-220">**selectedItems**</span></span>|<span data-ttu-id="91fc8-221">Массив</span><span class="sxs-lookup"><span data-stu-id="91fc8-221">Array</span></span>|<span data-ttu-id="91fc8-222">Список выбранных элементов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="91fc8-222">List of Selected items in JSON format.</span></span>|
<span data-ttu-id="91fc8-p124">Для виджета требуется таблица стилей веб-сайта SharePoint. Вы можете непосредственно указать ссылку на таблицу стилей SharePoint или использовать виджет хрома. Подробнее о таблице стилей см. в статьях  [Использование таблицы стилей веб-сайта SharePoint в надстройках для SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md) и [Использование клиентского элемента управления хрома в надстройках для SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="91fc8-p124">The widget requires the SharePoint website style sheet. You can reference the SharePoint style sheet directly or use the chrome widget. For more information about the style sheet, see  [Use a SharePoint website's style sheet in SharePoint Add-ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md) and [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span> 
 

 
<span data-ttu-id="91fc8-p125">Чтобы увидеть виджет "Представление списка" в действии, см. пример кода  [Использование экспериментального виджета "Представление списка на рабочем столе" в надстройке](http://code.msdn.microsoft.com/SharePoint-Use-the-c3edb076). См. также  [Использование экспериментального мини-приложения "Просмотр списка на рабочем столе" в надстройках для SharePoint](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="91fc8-p125">To see the List View widget in action, see the  [Use the Desktop List View experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-c3edb076) code sample. Also see [Use the experimental Desktop List View widget in SharePoint Add-ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="conclusion"></a><span data-ttu-id="91fc8-228">Заключение</span><span class="sxs-lookup"><span data-stu-id="91fc8-228">Conclusion</span></span>

<span data-ttu-id="91fc8-229">Виджеты могут помочь ускорить процесс разработки, а также сократить затраты на ваши надстройки и время их выхода на рынок. Вы можете использовать экспериментальные веб-виджеты Office в некоммерческих надстройках. Отправляйте свои отзывы и комментарии на  [сайт Office Developer Platform UserVoice](http://officespdev.uservoice.com/).</span><span class="sxs-lookup"><span data-stu-id="91fc8-229">Widgets can help to speed up the development process and reduce the cost and time-to-market of your add-ins. Office Web Widgets - Experimental provide widgets that you can use in your non-production add-ins. Your feedback and comments are welcome in the  [Office Developer Platform UserVoice site](http://officespdev.uservoice.com/).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="91fc8-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="91fc8-230">Additional resources</span></span>
<span data-ttu-id="91fc8-231"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="91fc8-231"></span></span>


-  [<span data-ttu-id="91fc8-232">Условия лицензии на экспериментальные мини-приложения Office для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="91fc8-232">Office Web Widgets - Experimental License Terms</span></span>](office-web-widgetsexperimental-license-terms.md)
    
 
-  [<span data-ttu-id="91fc8-233">Страница коллекции NuGet "Экспериментальные мини-приложения Office для веб-страниц"</span><span class="sxs-lookup"><span data-stu-id="91fc8-233">Office Web Widgets - Experimental NuGet gallery page</span></span>](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/)
    
 
-  [<span data-ttu-id="91fc8-234">Использование экспериментального мини-приложения "Выбор людей" в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="91fc8-234">Use the experimental People Picker widget in SharePoint Add-ins</span></span>](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="91fc8-235">Пример кода. Мини-приложения Office для веб-страниц — экспериментальная демоверсия</span><span class="sxs-lookup"><span data-stu-id="91fc8-235">Code sample: Office Web Widgets - Experimental Demo</span></span>](http://code.msdn.microsoft.com/SharePoint-Office-Web-6d44aa9e)
    
 
-  <span data-ttu-id="91fc8-236">[Использование экспериментального мини-приложения "Представление списка на рабочем столе" в надстройках для SharePoint](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="91fc8-236">[Use the experimental Desktop List View widget in SharePoint Add-ins](use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins.md)</span></span>
    
 
-  <span data-ttu-id="91fc8-237">[Пример кода. Использование экспериментального мини-приложения "Выбор людей" в надстройке](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85).</span><span class="sxs-lookup"><span data-stu-id="91fc8-237">[Code sample: Use the People Picker experimental widget in an add-in](http://code.msdn.microsoft.com/SharePoint-Use-the-57859f85)</span></span>
    
 
-  [<span data-ttu-id="91fc8-238">Пример кода. Использование экспериментального мини-приложения "Представление списка на рабочем столе"в надстройке</span><span class="sxs-lookup"><span data-stu-id="91fc8-238">Code sample: Use the Desktop List View experimental widget in an add-in</span></span>](http://code.msdn.microsoft.com/SharePoint-Use-the-c3edb076)
    
 
