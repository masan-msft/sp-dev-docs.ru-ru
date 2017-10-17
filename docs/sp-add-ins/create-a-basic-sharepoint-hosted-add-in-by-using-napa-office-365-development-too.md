---
title: "Создание простой надстройки для SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1551c0a7d5cb453a5093563298c9afb9225f7997
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools"></a><span data-ttu-id="82572-102">Создание простой надстройки для SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365</span><span class="sxs-lookup"><span data-stu-id="82572-102">Create a basic SharePoint-hosted add-in by using Napa Office 365 Development Tools</span></span>
<span data-ttu-id="82572-103">Узнайте, как создать простую надстройку SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365.</span><span class="sxs-lookup"><span data-stu-id="82572-103">Learn how to create a basic SharePoint-hosted SharePoint Add-in by using Napa Office 365 Development Tools.</span></span>
 

 
![Кнопка "Запустить"](../images/Apps_NAPA_Run_Button.png)
 
 [<span data-ttu-id="82572-105">Запустить этот пример сейчас!</span><span class="sxs-lookup"><span data-stu-id="82572-105">Run this sample now!</span></span>](http://go.microsoft.com/fwlink/?LinkId=313212)
 

 <span data-ttu-id="82572-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="82572-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="82572-p102">Napa — это средство, с помощью которого можно создавать надстройки SharePoint с размещением в SharePoint. Средство Napa само по себе представлено в виде надстройки SharePoint (с размещением у поставщика), которую можно установить на веб-сайтах SharePoint Online, созданных с помощью шаблона **Сайт разработчика**. На домашней странице сайтов разработчиков SharePoint находится библиотека **Тестируемые надстройки**. Инструкции по созданию сайта разработчика и установке Napa приводятся далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="82572-p102">Napa is a tool that you can use to create SharePoint-hosted SharePoint Add-ins. Napa is itself implemented as a (provider-hosted) SharePoint Add-in that can be installed on SharePoint Online websites that are created with the  **Developer Site** template. SharePoint developer sites have a library called **Add-ins in Testing** on the home page. Instructions for creating a developer site and installing Napa are later in this article.</span></span>
 

 <span data-ttu-id="82572-112">**Примечание.** Мы не поддерживаем установку средства Napa в локальной системе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82572-112">**Note**  We do not support installing Napa to on-premises SharePoint.</span></span>
 

<span data-ttu-id="82572-p103">С помощью Napa можно создавать собственные Надстройки SharePoint в браузере, а не в Visual Studio. В случае более сложных сценариев можно в любое время скачать свой проект и открыть его в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82572-p103">By using Napa, you can create your SharePoint Add-ins inside your browser instead of in Visual Studio. At any time, you can download your project and open it in Visual Studio for more advanced scenarios.</span></span>
 
<span data-ttu-id="82572-p104">В этой статье можно узнать, как создать простую Надстройка SharePoint с размещением в SharePoint, используя Napa. Созданная надстройка будет содержать элементы управления и код для управления списками и элементами списка.</span><span class="sxs-lookup"><span data-stu-id="82572-p104">By following this article, you can learn how to create a simple SharePoint-hosted SharePoint Add-in by using Napa. The add-in that you'll create includes controls and code for managing lists and list items.</span></span> 
 

 <span data-ttu-id="82572-p105">**Примечание.** С помощью средства Napa можно создать надстройку SharePoint, которая размещается только в SharePoint, но не у поставщика. Различия между этими типами надстроек см. в статье [Надстройки SharePoint](sharepoint-add-ins.md). Средство Napa не поддерживает обновленную семантику надстроек SharePoint, которая описана в статье [Обновление веб-компонентов надстройки в SharePoint](update-add-in-web-components-in-sharepoint.md). Поэтому, чтобы обновить надстройку, созданную в Napa, необходимо сначала экспортировать ее в Visual Studio. Соответствующие инструкции приведены далее в этой статье. Вы также можете создать надстройку SharePoint с помощью Visual Studio. Дополнительные сведения см. в статье [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="82572-p105">**Note**  You can create only SharePoint-hosted SharePoint Add-ins with Napa, not provider-hosted. For information on the differences, see  [SharePoint Add-ins](sharepoint-add-ins.md).You cannot use SharePoint's add-in updating semantics, which is described in  [Update add-in web components in SharePoint](update-add-in-web-components-in-sharepoint.md), in Napa. So if you need to update an add-in created in Napa, you first have to export it to Visual Studio. Instructions for doing so are later in this article.You can also create a SharePoint Add-in by using Visual Studio. For more information, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span></span>
 


## <a name="optionally-get-an-office-365-developer-site"></a><span data-ttu-id="82572-122">Получение сайта разработчика Office 365 (необязательно)</span><span class="sxs-lookup"><span data-stu-id="82572-122">Optionally, get an Office 365 Developer Site</span></span>
<span data-ttu-id="82572-123"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-123"><a name="Prerequisites"> </a></span></span>

<span data-ttu-id="82572-p106">Если у вас еще нет подписки на SharePoint Online, которую можно использовать для разработки, ознакомьтесь со сведениями о ее получении в этом разделе. Если же она у вас есть, перейдите сразу к разделу  [Установка Napa](#Overview).</span><span class="sxs-lookup"><span data-stu-id="82572-p106">If you don't already have a SharePoint Online subscription that you can use for development, use this section to get one. Otherwise, skip to  [Install Napa](#Overview).</span></span>
 

 

 <span data-ttu-id="82572-p107">**Примечание.** Возможно, у вас уже есть доступ к сайту разработчика для Office 365. **Вы являетесь подписчиком MSDN?** Visual Studio Ultimate и Visual Studio Premium с подпиской на MSDN включают бесплатную подписку разработчика приложений для Office 365. [Воспользуйтесь этим преимуществом прямо сегодня.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **У вас есть один из указанных ниже планов подписки на Office 365?** **В этом случае администратор подписки на Office 365 может создать сайт разработчика, ** используя [Центр администрирования Office 365](https://portal.microsoftonline.com/admin/default.aspx). Дополнительные сведения см. в статье [Создание сайта разработчика для существующей подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="82572-p107">**Note**   You might already have access to an Office 365 Developer Site: **Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Do you have one of the following Office 365 subscription plans?** **If so, an administrator of the Office 365 subscription can create a Developer Site** by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx). For more information, see  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 
 

<span data-ttu-id="82572-132">Получить план Office 365 можно двумя способами:</span><span class="sxs-lookup"><span data-stu-id="82572-132">Two ways to get an Office 365 plan.</span></span> 
 

 

- <span data-ttu-id="82572-133">Начните с [бесплатной 30-дневной пробной версии](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) с лицензией для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="82572-133">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>
    
 
- <span data-ttu-id="82572-134">Приобретите [подписку разработчика приложений для Office 365](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="82572-134">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 
    
 

 <span data-ttu-id="82572-135">**Подсказка.** При выборе каждой из этих ссылок откроется новое окно или вкладка, чтобы указанные ниже инструкции оставались под рукой.</span><span class="sxs-lookup"><span data-stu-id="82572-135">**Tip**  Each of these links will open in another window or tab in order to keep the following instructions handy.</span></span>
 


<span data-ttu-id="82572-136">**Рис. 1. Доменное имя сайта разработчика Office 365**</span><span class="sxs-lookup"><span data-stu-id="82572-136">**Figure 1. Office 365 Developer Site domain name**</span></span>

 

 
![Страница 2 регистрационной формы для учетной записи Office 365](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. <span data-ttu-id="82572-p108">Первая страница (не показана) регистрационной формы не требует объяснений. Просто введите запрашиваемую информацию о себе и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82572-p108">The first page (not shown) of the signup form is self-explanatory. Just supply the information about yourself that is requested and choose  **Next**.</span></span>
    
 
2. <span data-ttu-id="82572-140">На второй странице (рис. 1) укажите ИД администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="82572-140">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
 
3. <span data-ttu-id="82572-141">Создайте поддомен **.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="82572-141">Create a subdomain of  **.onmicrosoft.com**.</span></span> 
    
    <span data-ttu-id="82572-p109">После регистрации необходимо использовать полученные учетные данные (в формате _ИД_пользователя_@ _ваш_домен_.onmicrosoft.com) для входа на сайт портала Office 365, где можно управлять вашей учетной записью. Ваш сайт разработчика для SharePoint Online подготавливается к работе на новом домене: **http:// _ваш_домен_.sharepoint.com**.</span><span class="sxs-lookup"><span data-stu-id="82572-p109">After signup, you have to use the resulting credentials (in the format  _UserID_@ _yourdomain_.onmicrosoft.com) to sign in to your Office 365 portal site where you administer your account. Your SharePoint Online Developer Site is provisioned at your new domain:  **http:// _yourdomain_.sharepoint.com**.</span></span>
    
 
4. <span data-ttu-id="82572-p110">Нажмите кнопку **Далее** и заполните последнюю страницу формы. Если вы хотите указать номер телефона, чтобы получить код подтверждения, можно ввести номер мобильного или стационарного телефона, но *не* номер VoIP.</span><span class="sxs-lookup"><span data-stu-id="82572-p110">Choose  **Next** and fill out the final page of the form. If you choose to provide a telephone number to obtain a confirmation code, you can provide a mobile or land line telephone number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
 

    
 <span data-ttu-id="82572-p111">**Примечание.** Если при попытке зарегистрировать учетную запись разработчика выполнен вход в другую учетную запись Майкрософт, может отобразиться следующее сообщение: "Введенный ИД пользователя неверный. Возможно, он недействителен. Убедитесь, что вы вводите свой ИД пользователя, назначенный вам организацией. Он должен выглядеть так: *proverka@example.com* или *proverka@example.onmicrosoft.com*". Если появляется такое сообщение, выйдите из используемой учетной записи Майкрософт и повторите попытку. Если сообщение продолжает отображаться, очистите кэш браузера или выберите режим **Просмотр InPrivate**, а затем заполните форму.</span><span class="sxs-lookup"><span data-stu-id="82572-p111">**Note**  If you're logged on to another Microsoft account when you try to sign up for a developer account, you might get this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  *someone@example.com*  or *someone@example.onmicrosoft.com*  ."If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to  **InPrivate Browsing** and then fill out the form.</span></span>
 

<span data-ttu-id="82572-p112">По завершении регистрации в браузере откроется страница установки Office 365. Щелкните значок администратора, чтобы открыть страницу Центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="82572-p112">After you finish the signup process, your browser will opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span>
 

 

<span data-ttu-id="82572-153">**Рис. 2. Страница Центра администрирования Office 365**</span><span class="sxs-lookup"><span data-stu-id="82572-153">**Figure 2. Office 365 admin center page**</span></span>

 

 
![Снимок экрана с изображением Центра администрирования Office 365.](../images/SP15_Office365AdminInset_border.png)
 

 

1. <span data-ttu-id="82572-p113">Дождитесь, когда завершится подготовка к работе сайта разработчика. После этого обновите страницу Центра администрирования в браузере.</span><span class="sxs-lookup"><span data-stu-id="82572-p113">You'll have to wait for your Developer Site to finish provisioning. After provisioning is complete, refresh the admin center page in your browser.</span></span>
    
 
2. <span data-ttu-id="82572-p114">Пройдите по ссылке **Создание надстроек** в верхнем левом углу страницы, чтобы открыть сайт разработчиков. Должен открыться сайт, который выглядит так, как показано на рис. 3. На странице размещен список **Тестируемые надстройки**. Это подтверждает, что веб-сайт был создан с помощью шаблона сайта разработчика SharePoint. Если вместо него вы видите обычный сайт группы, подождите несколько минут и перезапустите сайт.</span><span class="sxs-lookup"><span data-stu-id="82572-p114">Then, choose the  **Build Add-ins** link in the upper left corner of the page to open your Developer Site. You should see a site that looks like the one in Figure 3. There is an **Add-ins in Testing** list on the page. This confirms that the website was made with SharePoint's Developer Site template. If you see a regular team site instead, wait a few minutes and launch your site again.</span></span>
    
 
3. <span data-ttu-id="82572-p115">Обратите внимание на URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82572-p115">Make a note of the URL of the site. It is used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
 

<span data-ttu-id="82572-164">**Рис. 3. Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**</span><span class="sxs-lookup"><span data-stu-id="82572-164">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

 

 
![Снимок экрана с изображением домашней страницы сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="install-napa"></a><span data-ttu-id="82572-166">Установка Napa</span><span class="sxs-lookup"><span data-stu-id="82572-166">Install Napa</span></span>
<span data-ttu-id="82572-167"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-167"><a name="Overview"> </a></span></span>

<span data-ttu-id="82572-p116">Если ваша подписка на не была изначально создана как Сайт разработчиков Office 365, тогда необходимо создать Сайт разработчика в пользовательском интерфейсе администратора подписки на и установить на нем средства Napa. Инструкции по созданию сайта приводятся в статье  [Создание сайта разработчика с использованием актуальной подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="82572-p116">If your subscription was not originally created as a Office 365 Developer Site, then you have to create a Developer Site in the Administration UI of the subscription and then install Napa in it. Instructions for creating the site are in  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span>
 

 
<span data-ttu-id="82572-p117">Чтобы установить средства Napa, откройте сайт разработчика и последовательно выберите элементы **Контент сайта** > **Добавление надстройки** > **Магазин SharePoint**. В магазине найдите средства Napa, а затем установите их. (Если у вас есть сайт разработчиков Office 365, возможно, средства Napa уже были установлены при создании сайта. В этом случае они будут отображаться на странице **Контент сайта**.)</span><span class="sxs-lookup"><span data-stu-id="82572-p117">To install Napa, open your Developer Site and choose  **Site Contents** > **add an add-in** > **SharePoint Store**. In the store, search for Napa and install it. (If you have a Office 365 Developer Site, Napa may have already been installed when the site was created and you will see it on the **Site Contents** page.)</span></span>
 

 

## <a name="create-a-sharepoint-add-in-project"></a><span data-ttu-id="82572-173">Создание проекта для надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="82572-173">Create a SharePoint Add-in project</span></span>
<span data-ttu-id="82572-174"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-174"><a name="Create"> </a></span></span>


1. <span data-ttu-id="82572-175">Откройте надстройку Napa на странице Office 365.</span><span class="sxs-lookup"><span data-stu-id="82572-175">Open the Napa add-in on the Office 365 page.</span></span>
    
 
2. <span data-ttu-id="82572-176">Выберите плитку **Add New Project** (Добавить новый проект), а затем — плитку **Add-in for SharePoint** (Надстройка для SharePoint).</span><span class="sxs-lookup"><span data-stu-id="82572-176">Choose the  **Add New Project** tile, and then choose the **Add-in for SharePoint** tile.</span></span>
    
 
3. <span data-ttu-id="82572-177">Назовите проект "Test SharePoint Add-in" (Тестовая надстройка SharePoint) и нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="82572-177">Name the project Test SharePoint Add-in, and then choose the  **Create** button.</span></span>
    
    <span data-ttu-id="82572-178">Откроется редактор кода с веб-страницей по умолчанию, содержащей пример кода, который можно запустить без внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="82572-178">The code editor opens and shows the default webpage, which already contains some sample code that you can run without doing anything else.</span></span>
    
 

## <a name="add-controls-to-the-home-page"></a><span data-ttu-id="82572-179">Добавление элементов управления на начальную страницу</span><span class="sxs-lookup"><span data-stu-id="82572-179">Add controls to the home page</span></span>
<span data-ttu-id="82572-180"><a name="AddControls1"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-180"><a name="AddControls1"> </a></span></span>

<span data-ttu-id="82572-p118">В Надстройка SharePoint добавьте на начальную страницу по умолчанию элементы управления для создания и удаления универсальных списков SharePoint, а также получения текущего числа списка на сайте Надстройка SharePoint. Код этих элементов будет добавлен позже.</span><span class="sxs-lookup"><span data-stu-id="82572-p118">In the SharePoint Add-in, add controls to the default home page for creating and deleting a generic SharePoint list and getting the current number of lists in the web of the SharePoint Add-in. You'll add code for the controls later.</span></span>
 

 

### <a name="to-add-controls-to-the-home-page"></a><span data-ttu-id="82572-183">Добавление элементов управления на начальную страницу</span><span class="sxs-lookup"><span data-stu-id="82572-183">To add controls to the home page</span></span>


1. <span data-ttu-id="82572-184">В папке **Pages** (Страницы) в левой части страницы выберите страницу **Default.aspx**, если она еще не выбрана.</span><span class="sxs-lookup"><span data-stu-id="82572-184">On the left side of the page under the  **Pages** folder, choose the **Default.aspx** page if it isn't already selected.</span></span>
    
    <span data-ttu-id="82572-185">Страница Default.aspx появится в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="82572-185">The Default.aspx webpage appears in the code editor.</span></span> 
    
 
2. <span data-ttu-id="82572-186">В разделе `PlaceHolderMain` добавьте следующий код под имеющимся HTML-кодом:</span><span class="sxs-lookup"><span data-stu-id="82572-186">In the  `PlaceHolderMain` section, add this code under the existing HTML</span></span>
    
```HTML
  <br />
<div>
    <button id="getListCount">Get count of lists in web</button>
</div>
<br />
<div id="starter">
    <input type="text" value="List name here" id="createlistbox"/><button id="createlistbutton">Create List</button>
    <p>
    Lists
    <br />
    <select id="selectlistbox" ></select><button id="deletelistbutton">Delete Selected List</button>
    </p>
</div>
```


    The HTML creates these controls.
    
      - A button that gets the number of lists in the web of the SharePoint Add-in.
    
 
  - <span data-ttu-id="82572-187">Кнопка для создания и удаления универсальных списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82572-187">A button for creating a generic SharePoint list and another button for deleting the list.</span></span>
    
 
  - <span data-ttu-id="82572-188">список списков, доступных в надстройке.</span><span class="sxs-lookup"><span data-stu-id="82572-188">A list of lists that are available within the add-in.</span></span>
    
 

## <a name="add-code-for-creating-and-deleting-lists"></a><span data-ttu-id="82572-189">Добавление кода для создания и удаления списков</span><span class="sxs-lookup"><span data-stu-id="82572-189">Add code for creating and deleting lists</span></span>
<span data-ttu-id="82572-190"><a name="AddCode1"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-190"><a name="AddCode1"> </a></span></span>

<span data-ttu-id="82572-191">В этой процедуре добавляется код JavaScript, позволяющий создавать и удалять списки в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82572-191">In this procedure, you'll add some JavaScript code so that users can create and delete lists in the SharePoint Add-in.</span></span>
 

 

### <a name="to-add-code-for-creating-and-deleting-lists"></a><span data-ttu-id="82572-192">Добавление кода для создания и удаления списков</span><span class="sxs-lookup"><span data-stu-id="82572-192">To add code for creating and deleting lists</span></span>


1. <span data-ttu-id="82572-193">Выберите папку **Scripts** и щелкните ссылку **App.js**.</span><span class="sxs-lookup"><span data-stu-id="82572-193">Choose the  **Scripts** folder, and then choose the **App.js** link.</span></span>
    
    <span data-ttu-id="82572-p119">В редакторе будет открыт файл кода JavaScript из шаблона проекта. Этот файл содержит код, который использует надстройка SharePoint. Вы можете добавить другой JS-файл и добавить код в него, а не в существующий файл, но в этом примере добавьте код в готовый файл **App.js**.</span><span class="sxs-lookup"><span data-stu-id="82572-p119">The default JavaScript code file from the project template opens for editing. This file contains the code that's used in your SharePoint Add-in. You could add another .js file and add code to it instead of to the existing file. But, for this example, add it to the  **App.js** file that's provided.</span></span>
    
    <span data-ttu-id="82572-198">На следующем этапе определяются функции для элементов управления, созданных в предыдущей процедуре.</span><span class="sxs-lookup"><span data-stu-id="82572-198">In the next step, you'll define the functions for the controls that you created in the previous procedure.</span></span>
    

|<span data-ttu-id="82572-199">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="82572-199">**Function Name**</span></span>|<span data-ttu-id="82572-200">**Описание**</span><span class="sxs-lookup"><span data-stu-id="82572-200">**Description**</span></span>|
|:-----|:-----|
| `getWebProperties()`|<span data-ttu-id="82572-201">Когда подключена к элементу управления **getListCount**, извлекает число списков на сайте.</span><span class="sxs-lookup"><span data-stu-id="82572-201">Connected to the  **getListCount** control???retrieves the number of lists in the web.</span></span>|
| `createlist()`|<span data-ttu-id="82572-202">Когда подключена к элементу управления **createListButton**, создает универсальный список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82572-202">Connected to the  **createListButton** control???creates a generic SharePoint list.</span></span>|
| `deletelist()`|<span data-ttu-id="82572-203">Когда подключена к элементу управления **deletelistbutton**, удаляет список, выбранный пользователем в списке доступных.</span><span class="sxs-lookup"><span data-stu-id="82572-203">Connected to the  **deletelistbutton** control???deletes the list that the user chose from the list of available lists.</span></span>|

    You'll also call the  `welcome()` and `displayLists()` functions, which this walkthrough will describe later.
    
 
2. <span data-ttu-id="82572-204">В файле **App.js** к двум переменным по умолчанию добавьте переменные `web`, `lists` и `listItemcollection`, затем измените код в функции `$(document).ready()` в соответствии с указанным ниже примером.</span><span class="sxs-lookup"><span data-stu-id="82572-204">In the  **App.js** file, add the `web`,  `lists`, and  `listItemcollection` variables to the two default variables, and change the code in the `$(document).ready()` function to the following example.</span></span>
    
     <span data-ttu-id="82572-p120">**Примечание.** В коде появятся подчеркивания, указывающие на ошибки. Позже они пропадут.</span><span class="sxs-lookup"><span data-stu-id="82572-p120">**Note**  Error squiggles will appear in this code. They'll disappear in later steps.</span></span>

```
  'use strict';

var context = SP.ClientContext.get_current();
var user = context.get_web().get_currentUser();
var web = context.get_web();
var lists = web.get_lists();
var listItemCollection;  // This variable is used later when you add list items.

(function () {

// This code runs when the DOM is ready and creates a context object which is 
// needed to use the SharePoint object model.
$(document).ready(function () {
    getUserName();
    $("#getListCount").click(function (event) {
        getWebProperties();
        event.preventDefault();
    });

    $("#createlistbutton").click(function (event) {
        createlist();
        event.preventDefault();
    });

    $("#deletelistbutton").click(function (event) {
        deletelist();
        event.preventDefault();
    });
        displayLists();
    });

```


    In the next step, you'll add JavaScript functions for the definitions. Each function in the code is executed by calling  `executeQueryAsync()`, which executes the current pending request asynchronously on the server by using the client-side object model (CSOM) for SharePoint. When a function executes asynchronously, your script continues to run without waiting for the server to respond. Each  `executeQueryAsync()` call includes two event handlers. One handler responds if the function runs successfully, and the other handler responds if the function fails. This table describes the main functions.
    

|<span data-ttu-id="82572-207">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="82572-207">**Function name**</span></span>|<span data-ttu-id="82572-208">**Описание**</span><span class="sxs-lookup"><span data-stu-id="82572-208">**Description**</span></span>|
|:-----|:-----|
| `welcome()`|<span data-ttu-id="82572-209">Получает ссылку на текущий контекст сайта, а затем использует ее, чтобы задать информацию о текущем пользователе в этом контексте.</span><span class="sxs-lookup"><span data-stu-id="82572-209">Gets the current web context reference, and then uses it to set the current user information into the context.</span></span>|
| `getWebProperties()`|<span data-ttu-id="82572-210">Получает коллекцию списков на текущем сайте и возвращает их число.</span><span class="sxs-lookup"><span data-stu-id="82572-210">Gets the collection of lists in the current web and then returns the number of lists.</span></span>|
| `displaylists()`|<span data-ttu-id="82572-p121">Получает текущую коллекцию списков на сайте. В случае успеха функция добавляет их имена в коллекцию в списке доступных списков.</span><span class="sxs-lookup"><span data-stu-id="82572-p121">Gets the current collection of lists in this web. If successful, this function adds the name of each list in the collection to the list of available lists.</span></span>|
| `createlist()`|<span data-ttu-id="82572-p122">Создает универсальный список SharePoint (типа шаблона списка **genericList**) и дает ему имя, указанное пользователем в элементе управления **createlistbox**. Можно создать списки других типов. Дополнительные сведения о типах списков см. в статье [Перечисление SPListTemplateType](http://go.microsoft.com/fwlink/?LinkId=256687).</span><span class="sxs-lookup"><span data-stu-id="82572-p122">Creates a generic SharePoint list (list template type  **genericList**) and gives it the name that the user specifies in the  **createlistbox** control. You can create other types of lists. For more information about list types, see [SPListTemplateType Enumeration](http://go.microsoft.com/fwlink/?LinkId=256687).</span></span>|
| `deletelist()`|<span data-ttu-id="82572-216">Удаляет список, выбранный пользователем в списке доступных.</span><span class="sxs-lookup"><span data-stu-id="82572-216">Deletes the list that the user chose from the list of available lists.</span></span>|
3. <span data-ttu-id="82572-217">Добавьте указанный ниже код в конец функции `onGetUserNameFail()` в файле **App.js**.</span><span class="sxs-lookup"><span data-stu-id="82572-217">Add the following code after the  `onGetUserNameFail()` function in **App.js**.</span></span>
    
```
  function getWebProperties() {
        // Get the number of lists in the current web.
        context.load(lists);
        context.executeQueryAsync(onWebPropsSuccess, onWebPropsFail);
    }

    function onWebPropsSuccess(sender, args) {
        alert('Number of lists in web: ' + lists.get_count());
    }

    function onWebPropsFail(sender, args) {
        alert('Failed to get list. Error: ' + args.get_message());
    }

    function displayLists() {
        // Get the available SharePoint lists, and then set them into 
        // the context.
        lists = web.get_lists();
        context.load(lists);
        context.executeQueryAsync(onGetListsSuccess, onGetListsFail);
    }

    function onGetListsSuccess(sender, args) {
        // Success getting the lists. Set references to the list 
        // elements and the list of available lists.
        var listEnumerator = lists.getEnumerator();
        var selectListBox = document.getElementById("selectlistbox");
        if (selectListBox.hasChildNodes()) {
            while (selectListBox.childNodes.length >= 1) {
                selectListBox.removeChild(selectListBox.firstChild);
            }
        }
        // Traverse the elements of the collection, and load the name of    
        // each list into the dropdown list box.
        while (listEnumerator.moveNext()) {
            var selectOption = document.createElement("option");
            selectOption.value = listEnumerator.get_current().get_title();
            selectOption.innerHTML = listEnumerator.get_current().get_title();
            selectListBox.appendChild(selectOption);
        }
    }

    function onGetListsFail(sender, args) {
        // Lists couldn't be loaded - display error.
        alert('Failed to get list. Error: ' + args.get_message());
    }

function createlist() {
        // Create a generic SharePoint list with the name that the user specifies.
        var listCreationInfo = new SP.ListCreationInformation();
        var listTitle = document.getElementById("createlistbox").value;
        listCreationInfo.set_title(listTitle);
        listCreationInfo.set_templateType(SP.ListTemplateType.genericList);
        lists = web.get_lists();
        var newList = lists.add(listCreationInfo);
        context.load(newList);
        context.executeQueryAsync(onListCreationSuccess, onListCreationFail);
    }

    function onListCreationSuccess() {
        displayLists();
    }

    function onListCreationFail(sender, args) {
        alert('Failed to create the list. ' + args.get_message());
    }

    function deletelist() {
        // Delete the list that the user specifies.
        var selectListBox = document.getElementById("selectlistbox");
        var selectedListTitle = selectListBox.value;
        var selectedList = web.get_lists().getByTitle(selectedListTitle);
        selectedList.deleteObject();
        context.executeQueryAsync(onDeleteListSuccess, onDeleteListFail);
    }

    function onDeleteListSuccess() {
        displayLists();
    }

    function onDeleteListFail(sender, args) {
        alert('Failed to delete the list. ' + args.get_message());
    }
```


## <a name="run-it"></a><span data-ttu-id="82572-218">Запуск</span><span class="sxs-lookup"><span data-stu-id="82572-218">Run it!</span></span>
<span data-ttu-id="82572-219"><a name="Run1"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-219"><a name="Run1"> </a></span></span>

<span data-ttu-id="82572-220">Первая часть интерфейса и кода готова, поэтому запустите надстройку, чтобы проверить ее работу.</span><span class="sxs-lookup"><span data-stu-id="82572-220">The first part of the UI and code is in place, so go ahead and run the add-in to verify whether it works.</span></span>
 

 

### <a name="to-run-the-add-in"></a><span data-ttu-id="82572-221">Порядок запуска надстройки</span><span class="sxs-lookup"><span data-stu-id="82572-221">To run the add-in</span></span>


1. <span data-ttu-id="82572-222">Внизу страницы нажмите кнопку запуска (</span><span class="sxs-lookup"><span data-stu-id="82572-222">At the bottom of the page, choose the run (</span></span>
 
![Кнопка "Запустить"](../images/Apps_NAPA_Run_Button.png)
 
<span data-ttu-id="82572-224">).</span><span class="sxs-lookup"><span data-stu-id="82572-224">) button.</span></span>
    
    The add-in is packaged, deployed, and installed on your Office 365 Developer Site.
    
    After installation, the SharePoint Add-in starts. If the add-in doesn't start automatically because, for example, a popup blocker is enabled, choose the add-in link to start the add-in.
    
 
2. <span data-ttu-id="82572-225">Нажмите ссылку **Щелкните здесь, чтобы запустить надстройку в новом окне**.</span><span class="sxs-lookup"><span data-stu-id="82572-225">Choose the  **Click here to launch your add-in in a new window** link.</span></span>
    
    <span data-ttu-id="82572-226">Появится окно для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="82572-226">The screen for the SharePoint Add-in appears.</span></span>
    
 
3. <span data-ttu-id="82572-227">Нажмите кнопку **Get count of lists in web** (Получить количество списков на веб-сайте).</span><span class="sxs-lookup"><span data-stu-id="82572-227">Choose the  **Get count of lists in web** button.</span></span>
    
    <span data-ttu-id="82572-p123">В диалоговом окне будет указано, что сайт текущей надстройки SharePoint содержит два списка. По умолчанию сайт содержит списки "Библиотека макетов" и "Коллекция главных страниц".</span><span class="sxs-lookup"><span data-stu-id="82572-p123">A dialog box specifies that the web for the current SharePoint Add-in contains two lists. (The web contains the Design Gallery and Master Page Gallery lists by default.)</span></span>
    
 
4. <span data-ttu-id="82572-230">В поле **List name here** (Укажите имя здесь) введите "Test List" (Тестовый список) и нажмите кнопку **Create List** (Создать список).</span><span class="sxs-lookup"><span data-stu-id="82572-230">In the  **List name here** box, enterTest List, and then choose the  **Create List** button.</span></span>
    
 
5. <span data-ttu-id="82572-231">Откройте список **Lists** (Списки), чтобы убедиться, что в нем есть новый список.</span><span class="sxs-lookup"><span data-stu-id="82572-231">Open the  **Lists** list to verify that the new list appears in it.</span></span>
    
 
6. <span data-ttu-id="82572-232">Снова нажмите кнопку **Get count of lists in web** (Получить количество списков на веб-сайте).</span><span class="sxs-lookup"><span data-stu-id="82572-232">Choose the  **Get count of lists in web** button again.</span></span>
    
    <span data-ttu-id="82572-233">Теперь на веб-странице содержится три списка, включая только что созданный.</span><span class="sxs-lookup"><span data-stu-id="82572-233">The web now contains three lists, including the list that you just created.</span></span>
    
 
7. <span data-ttu-id="82572-234">В списке **Lists** (Списки) выберите **Test List** (Тестовый список), а затем нажмите кнопку **Delete Selected List** (Удалить выбранный список).</span><span class="sxs-lookup"><span data-stu-id="82572-234">In the  **Lists** list, choose **Test List**, and then choose the  **Delete Selected List** button.</span></span>
    
     <span data-ttu-id="82572-235">**Test List** (Тестовый список) исчезнет из списка доступных списков.</span><span class="sxs-lookup"><span data-stu-id="82572-235">**Test List** disappears from the list of available lists.</span></span>
    
 
8. <span data-ttu-id="82572-236">По завершении работы закройте окно браузера, а затем нажмите кнопку **Закрыть** в окне **Запуск надстройки**, чтобы вернуться к редактируемому проекту.</span><span class="sxs-lookup"><span data-stu-id="82572-236">When you finish, close the browser window, and then choose the  **Close** button in **Launch Add-in** window to return to the project that you were editing.</span></span>
    
 

## <a name="add-code-and-controls-for-adding-and-deleting-list-items"></a><span data-ttu-id="82572-237">Добавление кода и элементов управления для добавления и удаления элементов списков</span><span class="sxs-lookup"><span data-stu-id="82572-237">Add code and controls for adding and deleting list items</span></span>
<span data-ttu-id="82572-238"><a name="AddControls2"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-238"><a name="AddControls2"> </a></span></span>

<span data-ttu-id="82572-239">Теперь пользователи могут создавать и удалять списки, поэтому вы можете выполнить следующие действия, чтобы они могли добавлять и удалять элементы списков.</span><span class="sxs-lookup"><span data-stu-id="82572-239">Now that users can create and delete lists, you can perform the following steps to enable them to add and delete list items.</span></span>
 

 

### <a name="to-add-code-and-controls-for-adding-and-deleting-list-items"></a><span data-ttu-id="82572-240">Добавление кода и элементов управления для добавления и удаления элементов списков</span><span class="sxs-lookup"><span data-stu-id="82572-240">To add code and controls for adding and deleting list items</span></span>


1. <span data-ttu-id="82572-241">Откройте файл Default.aspx для редактирования.</span><span class="sxs-lookup"><span data-stu-id="82572-241">Choose the Default.aspx file to edit it.</span></span>
    
 
2. <span data-ttu-id="82572-242">В элементе `selectlistbox` добавьте указанный ниже код.</span><span class="sxs-lookup"><span data-stu-id="82572-242">Under the  `selectlistbox` element, add this code.</span></span>
    
```XML
      <p>
    Items
    <br />
    <input type="text" value="item name here" id="createitembox"/><button id="createitembutton">Create Item</button>
    </p>
    <p>
    <select id="selectitembox"></select> <button id="deleteitembutton">Delete Selected Item</button>
    </p>
```


    This code adds an input box where users can specify the name of an item, a button to add the item to the list, and a button to delete the item from the list.
    
 
3. <span data-ttu-id="82572-243">Выберите файл **App.js** для редактирования.</span><span class="sxs-lookup"><span data-stu-id="82572-243">Choose the  **App.js** file to edit it.</span></span>
    
 
4. <span data-ttu-id="82572-p124">В функции `$(document).ready()` добавьте определения функций, вызываемых при нажатии кнопок **Создать элемент** и **Удалить выбранный элемент**. Кроме того, добавьте обработчик событий jQuery для списка **Списки**, чтобы гарантировать, что элементы списка будут обновляться при выборе нового списка.</span><span class="sxs-lookup"><span data-stu-id="82572-p124">In the  `$(document).ready()` function, add definitions for functions that are called when the user chooses the **Create Item** and **Delete Selected Item** buttons. Also, add a jQuery event handler for the **Lists** list box to ensure the list items get updated when you select a new list.</span></span>
    
```
  $("#createitembutton").click(function (event) {
            createitem();
            event.preventDefault();
        });

        $("#deleteitembutton").click(function (event) {
            deleteitem();
            event.preventDefault();
        });
    
        // Update the list items dropdown when a new list
        // is selected in the Lists dropdown.
        $("#selectlistbox").change(function (event) {
            getitems();
            event.preventDefault();
        });
```


     **Note**  If the list items aren't displaying when you run the add-in, be sure that the  `displayLists();` statement comes after the previous code.

    In the next step, you'll add JavaScript functions for the new definitions and a support function ( `getItems()`). This table describes what the main functions do.
    

|<span data-ttu-id="82572-246">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="82572-246">**Function name**</span></span>|<span data-ttu-id="82572-247">**Описание**</span><span class="sxs-lookup"><span data-stu-id="82572-247">**Description**</span></span>|
|:-----|:-----|
| `createItem()`|<span data-ttu-id="82572-248">Добавляет элемент в выбранный список и дает ему имя из поля **Items** (Элементы).</span><span class="sxs-lookup"><span data-stu-id="82572-248">Adds an item to the list that the user chooses, and gives that item the name that the user specifies in the  **Items** box.</span></span>|
| `deleteItem()`|<span data-ttu-id="82572-249">Удаляет элемент, который пользователь выбрал из списка.</span><span class="sxs-lookup"><span data-stu-id="82572-249">Deletes the item that the user chooses from the list.</span></span>|
| `getItems()`|<span data-ttu-id="82572-250">Извлекает коллекцию элементов (и их дочерних элементов) из списка, выбранного пользователем.</span><span class="sxs-lookup"><span data-stu-id="82572-250">Retrieves the collection of items (and its children) in the list that the user chooses.</span></span>|
5. <span data-ttu-id="82572-251">Добавьте следующий код в конец файла **App.js** после функции `onDeleteListFail()`.</span><span class="sxs-lookup"><span data-stu-id="82572-251">Add this code to bottom of  **App.js**, after the  `onDeleteListFail()` function.</span></span>
    
```
  function createitem() {
    // Retrieve the list that the user chose, and add an item to it.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedListTitle = selectListBox.value;
    var selectedList = web.get_lists().getByTitle(selectedListTitle);

    var listItemCreationInfo = new SP.ListItemCreationInformation();
    var newItem = selectedList.addItem(listItemCreationInfo);
    var listItemTitle = document.getElementById("createitembox").value;
    newItem.set_item('Title', listItemTitle);
    newItem.update();
    context.load(newItem);
    context.executeQueryAsync(onItemCreationSuccess, onItemCreationFail);
}

function onItemCreationSuccess() {
    // Refresh the list of items.
    getitems();
}

function onItemCreationFail(sender, args) {
    // The item couldn't be created - display an error message.
    alert('Failed to create the item. ' + args.get_message());
}

function deleteitem() {
    // Delete the item that the user chose.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedListTitle = selectListBox.value;
    var selectedList = web.get_lists().getByTitle(selectedListTitle);
    var selectItemBox = document.getElementById("selectitembox");
    var selectedItemID = selectItemBox.value;
    var selectedItem = selectedList.getItemById(selectedItemID);
    selectedItem.deleteObject();
    selectedList.update();
    context.load(selectedList);
    context.executeQueryAsync(onDeleteItemSuccess, onDeleteItemFail);
}

function onDeleteItemSuccess() {
    // Refresh the list of items.
    getitems();
}

function onDeleteItemFail(sender, args) {
    // The item couldn't be deleted - display an error message.
    alert('Failed to delete the item. ' + args.get_message());
}

function getitems() {
    // Using a CAML query, get the items in the list that the user chose, and 
    // set the context to the collection of list items.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedList = selectListBox.value;
    var selectedListTitle = web.get_lists().getByTitle(selectedList);  
    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml("<View><ViewFields>" +
        "<FieldRef Name='ID' />" +
        "<FieldRef Name='Title' />" +
        "</ViewFields></View>')");
    listItemCollection = selectedListTitle.getItems(camlQuery);
    context.load(listItemCollection, "Include(Title, ID)");
    context.executeQueryAsync(onGetItemsSuccess, onGetItemsFail);
}

function onGetItemsSuccess(sender, args) {
    // The list items were retrieved.
    // Show all child nodes.
    var listItemEnumerator = listItemCollection.getEnumerator();
    var selectItemBox = document.getElementById("selectitembox");
    if (selectItemBox.hasChildNodes()) {
        while (selectItemBox.childNodes.length >= 1) {
     selectItemBox.removeChild(selectItemBox.firstChild);
        }
    }
        while (listItemEnumerator.moveNext()) {
            var selectOption = document.createElement("option");
            selectOption.value = listItemEnumerator.get_current().get_item('ID');
            selectOption.innerHTML = listItemEnumerator.get_current().get_item('Title');
            selectItemBox.appendChild(selectOption);
        }
}

function onGetItemsFail(sender, args) {
    // The list items couldn't be retrieved - display an error message.
    alert('Failed to get items. Error: ' + args.get_message());
}
```


## <a name="run-the-revised-sharepoint-add-in"></a><span data-ttu-id="82572-252">Запуск измененной надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="82572-252">Run the revised SharePoint Add-in!</span></span>
<span data-ttu-id="82572-253"><a name="Run2"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-253"><a name="Run2"> </a></span></span>

<span data-ttu-id="82572-254">Интерфейс и код готовы, поэтому запустите надстройку, чтобы проверить ее работу.</span><span class="sxs-lookup"><span data-stu-id="82572-254">All of the UI and code is in place, so go ahead and run the add-in to be sure it works.</span></span>
 

 

### <a name="to-run-the-revised-sharepoint-add-in"></a><span data-ttu-id="82572-255">Запуск измененной надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="82572-255">To run the revised SharePoint Add-in</span></span>


1. <span data-ttu-id="82572-256">Внизу страницы нажмите кнопку **Запустить** еще раз.</span><span class="sxs-lookup"><span data-stu-id="82572-256">At the bottom of the page, choose the  **Run** button again.</span></span>
    
 
2. <span data-ttu-id="82572-257">В поле **List name here** (Укажите имя здесь) введите "New Test List" (Новый тестовый список) и нажмите кнопку **Create List** (Создать список).</span><span class="sxs-lookup"><span data-stu-id="82572-257">In the  **List name here** box, enterNew Test List, and then choose the  **Create List** button.</span></span>
    
    <span data-ttu-id="82572-258">Новый список добавится в столбец **Lists** (Списки).</span><span class="sxs-lookup"><span data-stu-id="82572-258">The new list is added to the  **Lists** list.</span></span>
    
 
3. <span data-ttu-id="82572-259">В столбце **Lists** (Списки) выберите **New Test List** (Новый тестовый список).</span><span class="sxs-lookup"><span data-stu-id="82572-259">In the  **Lists** list, choose **New Test List**.</span></span>
    
 
4. <span data-ttu-id="82572-260">В поле **Item name here** (Укажите имя элемента) введите "Item 1" (Элемент 1) и нажмите кнопку **Create Item** (Создать элемент).</span><span class="sxs-lookup"><span data-stu-id="82572-260">In the  **Item name here** box, enterItem 1, and then choose the  **Create Item** button.</span></span>
    
    <span data-ttu-id="82572-261">Новый элемент списка появится в столбце **Items** (Элементы).</span><span class="sxs-lookup"><span data-stu-id="82572-261">The new list item appears in the  **Items** list.</span></span>
    
 
5. <span data-ttu-id="82572-262">Повторите предыдущие действия, чтобы добавить элементы "Item 2" (Элемент 2) и "Item 3" (Элемент 3).</span><span class="sxs-lookup"><span data-stu-id="82572-262">Repeat the previous step to add Item 2 andItem 3.</span></span>
    
 
6. <span data-ttu-id="82572-263">В списке элементов выберите **Item 2** (Элемент 2), а затем нажмите кнопку **Delete Selected Item** (Удалить выбранный элемент).</span><span class="sxs-lookup"><span data-stu-id="82572-263">In the list of items, choose  **Item 2**, and then choose the  **Delete Selected Item** button.</span></span>
    
     <span data-ttu-id="82572-264">**Item 2** (Элемент 2) исчезнет из списка элементов.</span><span class="sxs-lookup"><span data-stu-id="82572-264">**Item 2** disappears from the list of items.</span></span>
    
 
7. <span data-ttu-id="82572-265">По окончании работы закройте окно браузера.</span><span class="sxs-lookup"><span data-stu-id="82572-265">When you finish, close the browser window.</span></span>
    
 

## <a name="export-the-project-to-visual-studio"></a><span data-ttu-id="82572-266">Экспорт проекта в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82572-266">Export the project to Visual Studio</span></span>
<span data-ttu-id="82572-267"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-267"><a name="NextSteps"> </a></span></span>

<span data-ttu-id="82572-p125">Откройте свой проект в Visual Studio, нажав кнопку **Открыть в Visual Studio**, как показано на рисунке 3. Napa автоматически установит требуемые средства и откроет проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82572-p125">Open your project in Visual Studio by choosing the  **Open in Visual Studio** button, as shown in Figure 3. Napa automatically installs the necessary tools and opens your project in Visual Studio.</span></span>
 

 

<span data-ttu-id="82572-270">**Рис. 3. Кнопка "Открыть в Visual Studio"**</span><span class="sxs-lookup"><span data-stu-id="82572-270">**Figure 3. The Open in Visual Studio button**</span></span>

 

 
![Кнопка "Открыть в Visual Studio"](../images/Apps_Napa_OpenInVS.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="82572-272">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="82572-272">Additional resources</span></span>
<span data-ttu-id="82572-273"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="82572-273"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="82572-274">Обзор платформы разработки SharePoint</span><span class="sxs-lookup"><span data-stu-id="82572-274">SharePoint development overview</span></span>](http://msdn.microsoft.com/library/f86e2695-4d7a-4fc5-bc23-689de96c4b06%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="82572-275">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="82572-275">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 

