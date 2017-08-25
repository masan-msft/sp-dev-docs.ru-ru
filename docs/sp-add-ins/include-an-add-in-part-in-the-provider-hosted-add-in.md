
# <a name="include-an-add-in-part-in-the-provider-hosted-add-in"></a><span data-ttu-id="8c629-101">Добавление веб-части надстройки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="8c629-101">Include an add-in part in the provider-hosted add-in</span></span>
<span data-ttu-id="8c629-102">Узнайте, как настроить внешний вид удаленной веб-формы на странице SharePoint в надстройке SharePoint, размещаемой у поставщика.</span><span class="sxs-lookup"><span data-stu-id="8c629-102">Learn how to surface a remote web form in a SharePoint page in a provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="8c629-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="8c629-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="8c629-p102">Это шестая часть серии статей, посвященной основам разработки надстроек, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="8c629-p102">Learn how to surface a remote web form in a SharePoint page in a provider-hosted SharePoint Add-in. This is the sixth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="8c629-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="8c629-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="8c629-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="8c629-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [<span data-ttu-id="8c629-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="8c629-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="8c629-111">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="8c629-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [<span data-ttu-id="8c629-112">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="8c629-112">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 

 <span data-ttu-id="8c629-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeAdd-inPart.sln.</span><span class="sxs-lookup"><span data-stu-id="8c629-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeAdd-inPart.sln file.</span></span>
 

<span data-ttu-id="8c629-p104">В данной статье вы добавите особую веб-часть, называемую веб-частью надстройки, в Надстройка SharePoint. Веб-часть надстройки позволяет использовать форму заказа надстройки на странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8c629-p104">In this article, you add a special kind of Web Part, called an add-in part to the SharePoint Add-in. The add-in part exposes the add-in's order form on a SharePoint page.</span></span>
 

## <a name="create-the-add-in-part"></a><span data-ttu-id="8c629-117">Создание веб-части надстройки</span><span class="sxs-lookup"><span data-stu-id="8c629-117">Create the add-in part</span></span>


 

 

 <span data-ttu-id="8c629-p105">**Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений** и выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="8c629-p105">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
 


1. <span data-ttu-id="8c629-121">В **обозревателе решений** щелкните правой кнопкой мыши проект **ChainStore** и выберите **Добавить | Создать элемент**.</span><span class="sxs-lookup"><span data-stu-id="8c629-121">In **Solution Explorer**, right-click the **ChainStore** project and select **Add | New Item**.</span></span>
    
 
2. <span data-ttu-id="8c629-p106">Выберите тип **Клиентская веб-часть (хост-сайт)**, присвойте ей имя Place Order (Размещение заказа), а затем нажмите кнопку **Добавить** ("клиентская веб-часть" — это еще одно название веб-части надстройки).</span><span class="sxs-lookup"><span data-stu-id="8c629-p106">Select **Client Web Part (Host Web)**, give it the name Place Order, and then press **Add**. ("Client Web Part" is another name for "add-in part".)</span></span>
    
 
3. <span data-ttu-id="8c629-124">На следующей странице мастера выберите второй переключатель **Выберите или введите URL-адрес существующей веб-страницы для контента клиентской веб-части**.</span><span class="sxs-lookup"><span data-stu-id="8c629-124">On the next page of the wizard, select the second radio button: **Select or enter the URL of an existing web page for the client web part content**.</span></span>
    
 
4. <span data-ttu-id="8c629-125">В раскрывающемся списке выберите URL-адрес для страницы **OrderForm.aspx**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="8c629-125">In the drop down list, select the URL for the **OrderForm.aspx** page, and then press **Finish**.</span></span>
    
    <span data-ttu-id="8c629-126">К проекту будет добавлен файл elements.xml, в котором определяется веб-часть надстройки, который затем откроется.</span><span class="sxs-lookup"><span data-stu-id="8c629-126">An elements.xml file that defines the add-in part is added to the project and opened.</span></span>
    
 
5. <span data-ttu-id="8c629-127">В элементе **ClientWebPart** замените перечисленные ниже атрибуты на указанные значения.</span><span class="sxs-lookup"><span data-stu-id="8c629-127">In the **ClientWebPart** element, change the following attributes to these values:</span></span>
    

|<span data-ttu-id="8c629-128">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="8c629-128">**Attribute**</span></span>|<span data-ttu-id="8c629-129">**Значение**</span><span class="sxs-lookup"><span data-stu-id="8c629-129">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="8c629-130">Название</span><span class="sxs-lookup"><span data-stu-id="8c629-130">Title</span></span>|<span data-ttu-id="8c629-131">Разместить заказ</span><span class="sxs-lookup"><span data-stu-id="8c629-131">Place Order</span></span>|
|<span data-ttu-id="8c629-132">Описание</span><span class="sxs-lookup"><span data-stu-id="8c629-132">Description</span></span>|<span data-ttu-id="8c629-133">Форма размещения заказа</span><span class="sxs-lookup"><span data-stu-id="8c629-133">Form to place an order</span></span>|
|<span data-ttu-id="8c629-134">DefaultHeight (Высота, используемая по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="8c629-134">DefaultHeight</span></span>|<span data-ttu-id="8c629-135">320</span><span class="sxs-lookup"><span data-stu-id="8c629-135">320</span></span>|

    Leave all the other attributes with their defaults and save the file.
    
 

## <a name="run-the-add-in-and-test-the-add-in-part"></a><span data-ttu-id="8c629-136">Запуск надстройки и тестирование веб-части надстройки</span><span class="sxs-lookup"><span data-stu-id="8c629-136">Run the add-in and test the add-in part</span></span>


 

 

1. <span data-ttu-id="8c629-p107">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="8c629-p107">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span>
    
 
2. <span data-ttu-id="8c629-p108">Когда откроется начальная страница надстройки, сама надстройка уже будет развернута, а пользователи смогут добавлять веб-часть надстройки **Place Order** (Размещение заказа) в любую область веб-частей на любой странице SharePoint веб-сайта магазина в Гонконге. Чтобы добавить ее на начальную страницу, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="8c629-p108">When the add-in's start page opens, the add-in has been deployed and the **Place Order** add-in part is available to for users to add to any Web Part area on any SharePoint page in the Hong Kong store's website. Follow these steps to add it to the home page.</span></span>
    
      1. <span data-ttu-id="8c629-143">На расположенном в верхней части начальной страницы элементе управления хрома нажмите кнопку **Вернуться на сайт**. Откроется домашняя страница магазина в Гонконге.</span><span class="sxs-lookup"><span data-stu-id="8c629-143">Press **Back to Site** on the chrome control at the top of the start page to open the home page of the Hong Kong store.</span></span>
    
 
  2. <span data-ttu-id="8c629-144">На ленте откройте вкладку **Страница** и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="8c629-144">On the ribbon, open the **Page** tab and press the **Edit** button.</span></span>
    
 
  3. <span data-ttu-id="8c629-p109">После перевода страницы в режим правки откройте вкладку **Вставка** на ленте и нажмите кнопку **Веб-часть надстройки** (она может по-прежнему называться **Веб-часть приложения**).</span><span class="sxs-lookup"><span data-stu-id="8c629-p109">After the page is in edit mode, open the **Insert** tab on the ribbon, and the press the **Add-in Part** button. (The button may still be called **App Part**.)</span></span>
    
 
  4. <span data-ttu-id="8c629-p110">В открывшемся элементе управления вставкой веб-части выберите веб-часть надстройки **Размещение заказа**. Элемент управления будет выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8c629-p110">On the Web Part insertion control that opens, select the **Place Order** add-in part. The control will look similar to the following.</span></span>
    
  ![Элемент управления вставкой веб-части SharePoint. Выделена веб-часть под названием "Размещение заказа". Ее имя и описание отображаются в поле справа.](../../images/aae61f89-2e9e-4808-8b0c-2439dad7c701.PNG)
 

 

 
  5. <span data-ttu-id="8c629-p112">Щелкните какую-нибудь из зон веб-части на форме. Это необходимо, чтобы задать расположение для веб-части надстройки.</span><span class="sxs-lookup"><span data-stu-id="8c629-p112">Click somewhere in one of the Web Part zones of the form. This is to set the location where the add-in part will go.</span></span> 
    
 
  6. <span data-ttu-id="8c629-p113">Нажмите кнопку **Добавить** на элементе управления вставкой веб-части. Веб-часть надстройки **Размещение заказа** будет добавлена в выбранную зону веб-частей.</span><span class="sxs-lookup"><span data-stu-id="8c629-p113">Click **Add** on the Web Part insertion control. The **Place Order** add-in part will be added to the Web Part zone.</span></span>
    
 
  7. <span data-ttu-id="8c629-156">На ленте нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8c629-156">On the ribbon press **Save**.</span></span>
    
 
3. <span data-ttu-id="8c629-p114">Теперь форма заказа отобразится на странице. У нее будет такие же внешний вид и удобство использования, как и у остальной части страницы. Она должна выглядеть указанным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="8c629-p114">The order form now appears on the page and it has the look-and-feel of the rest of the page. It should look like the following:</span></span> 
    
  ![Веб-часть надстройки "Размещение заказа" на странице с текстовыми полями "Продукт", "Поставщик" и "Количество", а также кнопкой "Разместить заказ".](../../images/beae2e3c-c1f4-4334-8ab8-0c42252cb2a2.PNG)
 

 

 
4. <span data-ttu-id="8c629-p116">Введите значения полей **Поставщик**, **Продукт** и **Количество**, а затем нажмите кнопку **Разместить заказ**. На первый взгляд ничего не произойдет, но при этом в корпоративную базу данных будет добавлен заказ. Кроме того, вы можете очистить поля веб-части надстройки, обновив страницу.</span><span class="sxs-lookup"><span data-stu-id="8c629-p116">Enter values for **Supplier**, **Product**, and **Quantity** and press **Place Order**. Nothing will appear to happen, but an order is entered in the corporate database. Optionally, you can empty the fields of the add-in part by refreshing the page.</span></span>
    
 
5. <span data-ttu-id="8c629-p117">Нажимайте кнопку "Назад" в браузере, пока не вернетесь на начальную страницу надстройки "Сеть магазинов", а затем нажмите кнопку **Показать заказы**. В списке вы увидите ваш новый заказ.</span><span class="sxs-lookup"><span data-stu-id="8c629-p117">Use the browser's back button until you are back at the Chain Store add-in's start page; and then press **Show Orders**. Your new order is listed.</span></span>
    
 
6. <span data-ttu-id="8c629-p118">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="8c629-p118">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
7. <span data-ttu-id="8c629-p119">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="8c629-p119">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="8c629-170"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="8c629-170"></span></span>

 <span data-ttu-id="8c629-p120">Надстройка зависит от двух списков, которые вы создали вручную. Но мы не хотим, чтобы пользователи тоже вводили списки вручную. В следующей статье вы начнете работу над процессом автоматического создания этих списков. Первый основной этап создание настраиваемых обработчиков события установки надстройки: [Обработка событий надстройки в надстройке, размещаемой у поставщика](handle-add-in-events-in-the-provider-hosted-add-in)</span><span class="sxs-lookup"><span data-stu-id="8c629-p120">The add-in depends on two lists that you created manually. You don't want your users to have to do that. In the next article you begin the process of automatically creating these lists. The first major step is to create custom handlers for the event of installing an add-in: [Handle add-in events in the provider-hosted add-in](handle-add-in-events-in-the-provider-hosted-add-in)</span></span>
 

 

