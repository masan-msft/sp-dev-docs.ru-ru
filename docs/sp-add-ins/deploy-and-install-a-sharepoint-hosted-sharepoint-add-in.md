# <a name="deploy-and-install-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="161f6-101">Развертывание и установка надстроек, размещенных в SharePoint</span><span class="sxs-lookup"><span data-stu-id="161f6-101">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="161f6-102">Узнайте, как выполняются развертывание и установка надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="161f6-102">Learn how spappplural are deployed and installed.</span></span>
 

 <span data-ttu-id="161f6-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="161f6-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="161f6-p102">Это вторая часть серии статей об основах разработки надстроек, размещаемых в SharePoint. Сначала вам необходимо ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями этой серии:</span><span class="sxs-lookup"><span data-stu-id="161f6-p102">Learn how SharePoint Add-ins are deployed and installed. This is the second in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with the topic  [SharePoint Add-ins](sharepoint-add-ins) and the preceding topics in the series:</span></span>
 

-  [<span data-ttu-id="161f6-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="161f6-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

 <span data-ttu-id="161f6-p103">**Примечание.** Если вы уже изучали предыдущие статьи серии о надстройках с размещением в SharePoint, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей. Вы также можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeColumns.sln.</span><span class="sxs-lookup"><span data-stu-id="161f6-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>
 

<span data-ttu-id="161f6-p104">Размещаемые в SharePoint Надстройки SharePoint будет намного проще разрабатывать, зная, как пользователи развертывают и устанавливают надстройки. Поэтому в этой статье мы отвлечемся от кода, чтобы создать и использовать каталог надстроек, а затем установим надстройку, над которой вы работали.</span><span class="sxs-lookup"><span data-stu-id="161f6-p104">You'll find it a lot easier to develop SharePoint-hosted SharePoint Add-ins if you are familiar with how users deploy and install your add-ins. So, in this article, we'll take a brief break from coding to create and use an add-in catalog, and then install the add-in you've been working on.</span></span>
 

## <a name="create-an-add-in-catalog"></a><span data-ttu-id="161f6-113">Создание каталога надстроек</span><span class="sxs-lookup"><span data-stu-id="161f6-113">Create an add-in catalog</span></span>


 

 

1. <span data-ttu-id="161f6-p105">Войдите в свою подписку Office 365 от имени администратора. Нажмите значок средства запуска надстроек и выберите надстройку **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="161f6-p105">Login to your Office 365 subscription as an administrator. Choose the add-in launcher icon, and then choose the  **Admin** add-in.</span></span>
    
    <span data-ttu-id="161f6-116">**Средство запуска надстроек Office 365**</span><span class="sxs-lookup"><span data-stu-id="161f6-116">**Office 365 add-in launcher**</span></span>

 

  ![Средство запуска приложений Office 365](../../images/ec60797c-d329-4922-a811-70c64598f4d5.PNG)
 

    
    
 
2. <span data-ttu-id="161f6-118">В **Центре администрирования** разверните узел **Администратор** в области задачи и выберите **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="161f6-118">In the  **Admin Center**, expand the  **Admin** node in the task pane and then choose **SharePoint**.</span></span>
    
 
3. <span data-ttu-id="161f6-119">В **Центре администрирования SharePoint** выберите **Надстройки** в области задач.</span><span class="sxs-lookup"><span data-stu-id="161f6-119">In the  **SharePoint Admin Center**, choose  **add-ins** in the task pane.</span></span>
    
 
4. <span data-ttu-id="161f6-p106">На странице **надстройки** выберите пункт **Каталог надстроек**. (Если в подписке уже есть семейство веб-сайтов каталога надстроек, он откроется, а вам ничего делать не придется. Невозможно создать несколько каталогов в одной подписке.)</span><span class="sxs-lookup"><span data-stu-id="161f6-p106">On the  **add-ins** page, choose **Add-in Catalog**. (If there is already an add-in catalog site collection in the subscription, it will open and you are done. You cannot create more than one add-in catalog in a subscription.)</span></span>
    
 
5. <span data-ttu-id="161f6-123">На странице **Сайт каталога надстроек** нажмите кнопку **ОК**, чтобы принять параметр по умолчанию и создать сайт каталога надстроек.</span><span class="sxs-lookup"><span data-stu-id="161f6-123">On the  **Add-in Catalog Site** page, choose **OK** to accept the default option and create a new add-in catalog site.</span></span>
    
 
6. <span data-ttu-id="161f6-p107">В диалоговом окне **Создание семейства веб-сайтов каталога надстроек** укажите название и адрес сайта каталога надстроек. Рекомендуется добавить в название слово "каталог" и ввести URL-адрес, чтобы сделать его запоминающимся и отличающимся в **Центре администрирования SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="161f6-p107">On the  **Create Add-in Catalog Site Collection** dialog, specify the title and web site address of your add-in catalog site. We recommend that you include "catalog" in the title and URL to make it memorable and distinguishable in the **SharePoint Admin Center**.</span></span>
    
 
7. <span data-ttu-id="161f6-126">Укажите **часовой пояс** и назначьте себя **администратором**.</span><span class="sxs-lookup"><span data-stu-id="161f6-126">Specify a  **Time Zone** and set yourself as the **Administrator**.</span></span>
    
 
8. <span data-ttu-id="161f6-127">Выберите минимально возможную **квоту хранилища** (в настоящее время это 110, но значение можно изменить), потому что пакеты надстроек, которые будут передаваться в это семейство веб-сайтов, совсем небольшие.</span><span class="sxs-lookup"><span data-stu-id="161f6-127">Set the  **Storage Quota** to the lowest possible value (currently 110, but that can change), because the add-in packages you upload to this site collection are very small.</span></span>
    
 
9. <span data-ttu-id="161f6-p108">Задайте для параметра **Квота ресурсов сервера** значение 0 (ноль) и нажмите **ОК**. (Квота ресурсов сервера связана с регулированием изолированные решения с низкой производительностью, но на сайте каталога надстроек не будут устанавливаться изолированные решения.)</span><span class="sxs-lookup"><span data-stu-id="161f6-p108">Set the  **Server Resource Quota** to 0 (zero), and then choose **OK**. (The server resource quota is related to throttling poorly performing sandboxed solutions, but you won't be installing any sandboxed solutions on your add-in catalog site.)</span></span>
    
 
<span data-ttu-id="161f6-p109">При создании семейства веб-сайтов SharePoint возвращает вас в **Центр администрирования SharePoint**. Через несколько минут вы увидите, что коллекция создана.</span><span class="sxs-lookup"><span data-stu-id="161f6-p109">As the site collection is being created, SharePoint takes you back to the  **SharePoint Admin Center**. After a few minutes, you'll see that the collection has been created.</span></span>
 

## <a name="package-the-add-in-and-upload-it-to-the-catalog"></a><span data-ttu-id="161f6-132">Упаковка надстройки и ее отправка в каталог</span><span class="sxs-lookup"><span data-stu-id="161f6-132">Package the add-in and upload it to the catalog</span></span>


 

 

1. <span data-ttu-id="161f6-p110">Откройте решение в Visual Studio, а затем дважды щелкните узел проекта в **обозревателе решений**. Нажмите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="161f6-p110">Open the Visual Studio solution, and then right-click the project node in  **Solution Explorer**. Choose  **Publish**.</span></span>
    
 
2. <span data-ttu-id="161f6-p111">В области **Публикация** выберите команду **Упаковать надстройку**. Надстройка будет упакована и сохранена как APP-файл в папке \bin\debug\web.publish\1.0.0.0 решения.</span><span class="sxs-lookup"><span data-stu-id="161f6-p111">In the **Publish** pane, choose **Package the add-in**. The add-in is packaged and saved as an *.app file in the solution's \bin\debug\web.publish\1.0.0.0 folder.</span></span>
    
 
3. <span data-ttu-id="161f6-137">Откройте сайт каталога приложений в браузере и выберите **Надстройки SharePoint** на панели навигации.</span><span class="sxs-lookup"><span data-stu-id="161f6-137">Open your add-in catalog site in a browser and choose  **SharePoint Add-ins** in the navigation bar.</span></span>
    
 
4. <span data-ttu-id="161f6-p112">**Каталог Надстройки SharePoint** это стандартная библиотека ресурсов SharePoint. Отправьте в него пакет надстройки с помощью любых из методов передачи файлов в библиотеки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="161f6-p112">The  **SharePoint Add-ins** catalog is a standard SharePoint asset library. Upload the add-in package to it using any of the methods of uploading files to SharePoint libraries.</span></span>
    
 

## <a name="install-the-add-in-as-end-users-do"></a><span data-ttu-id="161f6-140">Способ установки надстройки, который доступен пользователям</span><span class="sxs-lookup"><span data-stu-id="161f6-140">Install the add-in as end users do</span></span>


1. <span data-ttu-id="161f6-141">Перейдите на любой веб-сайт в подписке SharePoint Online и откройте страницу **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="161f6-141">Navigate to any website in the SharePoint Online subscription and open the  **Site Contents** page.</span></span>
    
 
2. <span data-ttu-id="161f6-142">Выберите команду **Добавить надстройку**, чтобы открыть страницу **Ваши надстройки**.</span><span class="sxs-lookup"><span data-stu-id="161f6-142">Choose  **add an add-in** to open the **Your Add-ins** page.</span></span>
    
 
3. <span data-ttu-id="161f6-143">Найдите надстройку **Employee Orientation** (Обучение сотрудников) в разделе **Надстройки, которые можно добавить** и нажмите ее плитку.</span><span class="sxs-lookup"><span data-stu-id="161f6-143">Find the  **Employee Orientation** add-in in the **Add-ins you can add** section and click its tile.</span></span>
    
 
4. <span data-ttu-id="161f6-p113">Выберите **Доверять** в диалоговом окне запроса согласия. Автоматически откроется страница **Контент сайта**, и появится надстройка с сообщением об установке. После завершения установки пользователи могут выбрать плитку, чтобы запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="161f6-p113">Choose  **Trust It** on the consent dialog. The **Site Contents** page automatically opens and the add-in appears with a notation that it is installing. After it installs, users can choose the tile to run the add-in.</span></span>
    
 

## <a name="remove-the-add-in"></a><span data-ttu-id="161f6-147">Удаление надстройки</span><span class="sxs-lookup"><span data-stu-id="161f6-147">Remove the add-in</span></span>

<span data-ttu-id="161f6-148">Чтобы продолжить совершенствовать надстройку SharePoint в Visual Studio (см. раздел [Дальнейшие действия](#Nextsteps)), удалите ее, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="161f6-148">In order to continue enhancing the same SharePoint Add-in in Visual Studio (see  [Next steps](#Nextsteps)), remove the add-in with these steps:</span></span>
 

 

1. <span data-ttu-id="161f6-149">На странице **Содержимое сайта** наведите указатель мыши на надстройку, чтобы появилась кнопка выноски **…**</span><span class="sxs-lookup"><span data-stu-id="161f6-149">In the  **Site Contents** page, move the cursor over the add-in so that the callout button **...** appears.</span></span>
    
 
2. <span data-ttu-id="161f6-150">Нажмите кнопку выноски и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="161f6-150">Choose the callout button and then choose  **REMOVE** on the callout.</span></span>
    
 
3. <span data-ttu-id="161f6-151">Вернитесь к сайту каталога надстроек и выберите **Надстройки SharePoint** на панели навигации.</span><span class="sxs-lookup"><span data-stu-id="161f6-151">Navigate back to your add-in catalog site and choose  **SharePoint Add-ins** in the navigation bar.</span></span>
    
 
4. <span data-ttu-id="161f6-152">Выделите надстройку и выберите команду **Управление** в области задач над списком, а затем нажмите **Удалить** в меню управления.</span><span class="sxs-lookup"><span data-stu-id="161f6-152">Highlight the add-in and choose  **manage** on the task bar just above the list, and then choose **Delete** on the manage menu.</span></span>
    
 

## 

<span data-ttu-id="161f6-p114">Настоятельно рекомендуем продолжить изучение этой серии статей о надстройках с размещением в SharePoint, прежде чем переходить к более сложным темам. В следующей статье  [Добавление настраиваемых столбцов в надстройку с размещением в SharePoint](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in) мы вернемся к программированию.</span><span class="sxs-lookup"><span data-stu-id="161f6-p114">We strongly recommend that you continue with this series about SharePoint-hosted add-ins before you go on to the more advanced topics. Next we get back to coding in  [Add custom columns to a SharePoint-hostedSharePoint Add-in](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in).</span></span>
 

 

