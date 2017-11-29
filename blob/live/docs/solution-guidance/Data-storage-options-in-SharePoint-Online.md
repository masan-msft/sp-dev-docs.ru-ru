---
title: "Варианты хранения данных в SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 0e9264de4cb19e4f32939e02786611580d41c82d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="data-storage-options-in-sharepoint-online"></a><span data-ttu-id="7d719-102">Варианты хранения данных в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7d719-102">Data storage options in SharePoint Online</span></span>

<span data-ttu-id="7d719-103">При разработке SharePoint Online надстроек, у вас есть несколько различных параметров для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-103">When you develop SharePoint Online add-ins, you have a number of different options for data storage.</span></span> <span data-ttu-id="7d719-104">Ознакомьтесь с различиями между каждого варианта и сведения о преимущества использования удаленного хранилища, можно использовать образец кода, приведенный в данной статье.</span><span class="sxs-lookup"><span data-stu-id="7d719-104">You can use the sample described in this article to explore the differences between each option, and to learn about the advantages to using remote data storage.</span></span> 

<span data-ttu-id="7d719-105">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="7d719-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="7d719-106">В этой статье описывается [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) примера приложения, в котором отображается каждого из следующие варианты хранения данных, а также их преимущества и недостатки каждого из них:</span><span class="sxs-lookup"><span data-stu-id="7d719-106">This article describes the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app, which shows you each of the following data storage options and the advantages and disadvantages of each:</span></span>

- <span data-ttu-id="7d719-107">Список SharePoint на хост-сайта</span><span class="sxs-lookup"><span data-stu-id="7d719-107">SharePoint list on the host web</span></span>
    
- <span data-ttu-id="7d719-108">Список SharePoint на сайте приложения</span><span class="sxs-lookup"><span data-stu-id="7d719-108">SharePoint list on the app web</span></span>
    
- <span data-ttu-id="7d719-109">Базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7d719-109">SQL Azure database</span></span>
    
- <span data-ttu-id="7d719-110">Хранилище Azure очередей</span><span class="sxs-lookup"><span data-stu-id="7d719-110">Azure queue storage</span></span>
    
- <span data-ttu-id="7d719-111">Хранение таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="7d719-111">Azure table storage</span></span>
    
- <span data-ttu-id="7d719-112">Внешние веб-службы</span><span class="sxs-lookup"><span data-stu-id="7d719-112">External web service</span></span>
    
<span data-ttu-id="7d719-113">В примере приложения [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) — это размещение у поставщика приложений, написанных на языке C# и JavaScript, который развертывает несколько артефактов SharePoint (списки, веб-часть приложения, веб-части) на хост-сайта и сайта приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-113">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app is a provider-hosted app written in C# and JavaScript that deploys a number of SharePoint artifacts (lists, app part, web part) to both the host web and the app web.</span></span> <span data-ttu-id="7d719-114">Взаимодействует со списками SharePoint на веб-приложения и веб-сайт, а также выполняет вызовы базы данных SQL Azure, очереди и таблицы хранилища Azure и удаленного веб-службы, который реализует OData.</span><span class="sxs-lookup"><span data-stu-id="7d719-114">It interacts with SharePoint lists on the app web and host web, and also makes calls to a SQL Azure database, an Azure queue and table storage, and a remote web service that implements OData.</span></span> <span data-ttu-id="7d719-115">В этом примере используется шаблон Model-View-Controller (MVC).</span><span class="sxs-lookup"><span data-stu-id="7d719-115">This sample uses the Model-View-Controller (MVC) pattern.</span></span>
<span data-ttu-id="7d719-116">В примере приложения [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) применяется каждого варианта хранилища данных определенные функции, для которого параметр отлично подходят, как описано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="7d719-116">The  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample app applies each data storage option to a specific function for which the option is well suited, as described in the following table.</span></span>

|<span data-ttu-id="7d719-117">Дополнительные варианты хранения примера приложения</span><span class="sxs-lookup"><span data-stu-id="7d719-117">Sample app storage option</span></span>|<span data-ttu-id="7d719-118">Используется для</span><span class="sxs-lookup"><span data-stu-id="7d719-118">Used for</span></span>|
|:--|:--|
|<span data-ttu-id="7d719-119">Веб-приложения списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d719-119">SharePoint list app web</span></span>|<span data-ttu-id="7d719-120">Клиент notes</span><span class="sxs-lookup"><span data-stu-id="7d719-120">Customer notes</span></span>|
|<span data-ttu-id="7d719-121">Веб-сайт для списка SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d719-121">SharePoint list host web</span></span>|<span data-ttu-id="7d719-122">Поддержка случаев</span><span class="sxs-lookup"><span data-stu-id="7d719-122">Support cases</span></span>|
|<span data-ttu-id="7d719-123">Службы данных "Борей" OData</span><span class="sxs-lookup"><span data-stu-id="7d719-123">Northwind OData service</span></span>|<span data-ttu-id="7d719-124">Клиенты</span><span class="sxs-lookup"><span data-stu-id="7d719-124">Customers</span></span>|
|<span data-ttu-id="7d719-125">Хранение таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="7d719-125">Azure table storage</span></span>|<span data-ttu-id="7d719-126">Оценки по обслуживанию Клиентов</span><span class="sxs-lookup"><span data-stu-id="7d719-126">CSR ratings</span></span>|
|<span data-ttu-id="7d719-127">Хранилище Azure очередей</span><span class="sxs-lookup"><span data-stu-id="7d719-127">Azure queue storage</span></span>|<span data-ttu-id="7d719-128">Вызов очереди</span><span class="sxs-lookup"><span data-stu-id="7d719-128">Call queue</span></span>|
|<span data-ttu-id="7d719-129">Базы данных SQL Azure Northwind</span><span class="sxs-lookup"><span data-stu-id="7d719-129">SQL Azure Northwind database</span></span>|<span data-ttu-id="7d719-130">Заказов, сведения о заказе продуктов</span><span class="sxs-lookup"><span data-stu-id="7d719-130">Orders, order details, products</span></span>|

<span data-ttu-id="7d719-131">Приложение реализует панель мониторинга обслуживания клиентов и соответствующие интерфейсы, которые отображают последних заказов, рейтинги пример опроса клиента, notes клиента, поддержка, а также очереди представитель звонков с клиента.</span><span class="sxs-lookup"><span data-stu-id="7d719-131">The app implements a customer service dashboard and related interfaces that show recent orders, customer representative survey ratings, customer notes, support cases, and a customer representative call queue.</span></span> <span data-ttu-id="7d719-132">Первые два сценария позволяют получить данные с помощью довольно просто кода объектной модели клиента или запросов REST, но ограничивается пороговые значения списка запросов.</span><span class="sxs-lookup"><span data-stu-id="7d719-132">The first two scenarios let you retrieve data by using relatively simply client object model code or REST queries, but are limited by list query thresholds.</span></span> <span data-ttu-id="7d719-133">Следующие четыре сценарии используются различные типы удаленного хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d719-133">The next four scenarios uses different types of remote storage.</span></span> 

<span data-ttu-id="7d719-134">**На рисунке 1. Отображает запрос данных хранилища моделей начальная страница для развертывания компонентов SharePoint**</span><span class="sxs-lookup"><span data-stu-id="7d719-134">**Figure 1. Data storage models start page prompts you to deploy SharePoint components**</span></span>

![Снимок экрана примера приложения пользовательского интерфейса](media/bb3b58ca-b983-4ec4-b36d-18a911edb5d5.png)

## <a name="before-you-begin"></a><span data-ttu-id="7d719-136">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7d719-136">Before you begin</span></span>
<span data-ttu-id="7d719-137"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-137"></span></span>

<span data-ttu-id="7d719-138">Прежде чем использовать этот образец, убедитесь в том, что у вас есть следующие:</span><span class="sxs-lookup"><span data-stu-id="7d719-138">Before you use this sample, make sure that you have the following:</span></span>

- <span data-ttu-id="7d719-139">Учетную запись Microsoft Azure можно развернуть базу данных SQL Azure и создать учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7d719-139">A Microsoft Azure account where you can deploy a SQL Azure database and create an Azure storage account.</span></span> 
    
- <span data-ttu-id="7d719-140">SharePoint для разработчиков веб-сайтов, чтобы можно развернуть образец из Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7d719-140">A SharePoint developer site so that you can deploy the sample from Visual Studio 2013.</span></span>
    
<span data-ttu-id="7d719-141">Кроме того необходимо развернуть базы данных Northwind Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d719-141">Also, you need to deploy the Northwind database to Microsoft Azure.</span></span>

### <a name="to-deploy-the-northwind-database"></a><span data-ttu-id="7d719-142">Развертывание базы данных "Борей"</span><span class="sxs-lookup"><span data-stu-id="7d719-142">To deploy the Northwind database</span></span>

1. <span data-ttu-id="7d719-143">Войдите в систему портала управления Azure и выбор **Базы данных SQL**> **серверов**.</span><span class="sxs-lookup"><span data-stu-id="7d719-143">Log on to the Azure Management Portal and choose  **SQL Databases**> **Servers**.</span></span>
    
2. <span data-ttu-id="7d719-144">Нажмите кнопку **Создать базу данных сервера SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7d719-144">Choose  **Create a SQL Database Server**.</span></span>
    
3. <span data-ttu-id="7d719-145">В форме **Создания сервера** введите значения для **Имени для входа**, **Пароль для входа**и **области**, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="7d719-145">In the  **Create Server** form, enter values for **Login Name**,  **Login Password**, and  **Region**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="7d719-146">**На рисунке 2. Параметры сервера базы данных SQL**</span><span class="sxs-lookup"><span data-stu-id="7d719-146">**Figure 2. SQL database server settings**</span></span>

    ![Показывает параметры сервера базы данных SQL](media/7ae059fa-eecc-4446-8171-294e44acb189.png)

4. <span data-ttu-id="7d719-148">Нажмите кнопку флажок, чтобы закончить и создания сервера.</span><span class="sxs-lookup"><span data-stu-id="7d719-148">Choose the checkmark button to finish and create the server.</span></span>
    
5. <span data-ttu-id="7d719-149">Теперь, когда вы создали базу данных, выберите имя сервера, который был создан, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="7d719-149">Now that you've created the database, choose the server name that you created, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="7d719-150">**На рисунке 3. Имя сервера, на странице "серверы"**</span><span class="sxs-lookup"><span data-stu-id="7d719-150">**Figure 3. Server name on the Servers page**</span></span>

    ![Отображает список баз данных SQL](media/a6b097e4-5ad2-47df-9e31-ac0d699efd76.png)

6. <span data-ttu-id="7d719-152">Выберите команду **НАСТРОИТЬ**и нажмите стрелку в нижнем правом углу, чтобы завершить настройку и выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7d719-152">Choose  **CONFIGURE**, and then choose the arrow in the lower right corner to complete the configuration, and choose  **SAVE**.</span></span>
    
7. <span data-ttu-id="7d719-153">Откройте SQL Server Management Studio на компьютере локального разработки и создать базу данных с именем **"Борей"**.</span><span class="sxs-lookup"><span data-stu-id="7d719-153">Open SQL Server Management Studio on your local development computer and create a new database named  **NorthWind**.</span></span>
    
8. <span data-ttu-id="7d719-154">В **Обозревателе объектов**выберите базу данных **"Борей"** и выберите **Создать запрос**.</span><span class="sxs-lookup"><span data-stu-id="7d719-154">In the  **Object Explorer**, select the  **Northwind** database, and then choose **New Query**.</span></span>
    
9. <span data-ttu-id="7d719-155">В текстовом редакторе почтой откройте скрипт SQL northwind.sql, предоставляемая с примером [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) .</span><span class="sxs-lookup"><span data-stu-id="7d719-155">In a text editor of your choice, open the northwind.sql SQL script that is provided with the  [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) sample.</span></span>
    
10. <span data-ttu-id="7d719-156">Скопируйте текст в файл northwind.sql и вставьте его в **окно запроса SQL** в SQL Server Management Studio и затем выберите команду **выполнить**.</span><span class="sxs-lookup"><span data-stu-id="7d719-156">Copy the text in the northwind.sql file and paste it into the  **SQL Query window** in the SQL Server Management Studio, and then choose **Execute**.</span></span>
    
11. <span data-ttu-id="7d719-157">В **Обозревателе объектов**откройте контекстное меню для базы данных **Northwind** (щелкните правой кнопкой), выберите **задачи**и выберите **Развернуть базу данных в SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="7d719-157">In the  **Object Explorer**, open the shortcut menu for (right-click) the  **Northwind** database, select **Tasks**, and then select  **Deploy Database to SQL Azure**.</span></span>
    
12. <span data-ttu-id="7d719-158">На экране **Введение** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7d719-158">On the  **Introduction** screen, choose **Next**.</span></span>
    
13. <span data-ttu-id="7d719-159">Выберите **подключение...** и введите **имя сервера** для сервера базы данных SQL Azure, вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="7d719-159">Choose  **Connect ...** and enter the **Server name** for the SQL Azure Database Server you just created.</span></span>
    
14. <span data-ttu-id="7d719-160">В раскрывающемся списке **Проверка подлинности** выберите **Проверка подлинности SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7d719-160">In the  **Authentication** dropdown, select **SQL Server Authentication**.</span></span>
    
15. <span data-ttu-id="7d719-161">Введите имя пользователя и пароль, использованный при создания базы данных Azure SQL server и нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="7d719-161">Enter the user name and password you used when you created the SQL Azure Database server, then choose  **Connect**.</span></span>
    
16. <span data-ttu-id="7d719-162">Нажмите кнопку **Далее**, затем нажмите кнопку **Готово**и подождите, пока не будет создана база данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-162">Choose  **Next**, and then choose  **Finish**, and wait until the database is created.</span></span> <span data-ttu-id="7d719-163">После создания, нажмите кнопку **Закрыть** , чтобы закрыть мастер.</span><span class="sxs-lookup"><span data-stu-id="7d719-163">After it is created, choose  **Close** to close the wizard.</span></span>
    
17. <span data-ttu-id="7d719-164">Вернитесь на портале управления Azure ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)), чтобы проверить, успешно создана база данных Northwind.</span><span class="sxs-lookup"><span data-stu-id="7d719-164">Return to the Azure Management Portal ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)) to verify that the Northwind database was created successfully.</span></span> <span data-ttu-id="7d719-165">Вы должны увидеть, что оно указано на экране баз данных sql, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="7d719-165">You should see it listed on the sql databases screen, as shown in Figure 4.</span></span>
    
    <span data-ttu-id="7d719-166">**На рисунке 4. Список элементов базы данных SQL Server**</span><span class="sxs-lookup"><span data-stu-id="7d719-166">**Figure 4. Listing of SQL Server databases**</span></span>

    ![Отображает список всех баз данных SQL, в том числе Northwind](media/036b4252-f57b-4f39-9f60-ddaa30daf23c.png)

18. <span data-ttu-id="7d719-168">Выберите базу данных "Борей" и выберите **строки подключения базы данных SQL представления**.</span><span class="sxs-lookup"><span data-stu-id="7d719-168">Select the Northwind database, and then select  **View SQL Database connection strings**.</span></span>
    
19. <span data-ttu-id="7d719-169">Скопируйте строку подключения и вставьте его в текстовый файл и сохраните его локально.</span><span class="sxs-lookup"><span data-stu-id="7d719-169">Copy the connection string and paste it into a text file and save it locally.</span></span> <span data-ttu-id="7d719-170">Эта строка подключения понадобится позднее.</span><span class="sxs-lookup"><span data-stu-id="7d719-170">You will need this connection string later.</span></span> <span data-ttu-id="7d719-171">Закройте диалоговое окно **Строки подключения** .</span><span class="sxs-lookup"><span data-stu-id="7d719-171">Close the  **Connection Strings** dialog box.</span></span>
    
20. <span data-ttu-id="7d719-172">Перейдите по ссылке **настроить правила брандмауэра Windows Azure для этого IP-адреса** и добавьте IP-адрес правила брандмауэра для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-172">Choose the  **Set up Windows Azure firewall rules for this IP address** link and add your IP address to the firewall rules to allow you to access the database.</span></span>
    
21. <span data-ttu-id="7d719-173">Откройте проект Core.DataStorageModels.sln в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7d719-173">Open the Core.DataStorageModels.sln project in Visual Studio 2013.</span></span>
    
22. <span data-ttu-id="7d719-174">В **Окне Обозреватель решений**Visual Studio найдите файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="7d719-174">In the Visual Studio **Solution Explorer**, locate the Web.config file.</span></span>
    
23. <span data-ttu-id="7d719-175">В файле Web.config найдите добавить `name="NorthWindEntities"` и замените существующий connectionString значение с строку подключения, который был сохранен локально на шаге 19.</span><span class="sxs-lookup"><span data-stu-id="7d719-175">In the Web.config file, locate the add  `name="NorthWindEntities"` element and replace the existing connectionString value with the connection string information that you saved locally in step 19.</span></span> 
    
    ```XML
      <add name="NorthWindEntities" connectionString="metadata=res://*/Northwind.csdl|res://*/Northwind.ssdl|res://*/Northwind.msl;provider=System.Data.SqlClient;provider connection string=&amp;quot;data source=<Your Server Here>.database.windows.net;initial catalog=NorthWind;user id=<Your Username Here>@<Your Server Here>;password=<Your Password Here>;MultipleActiveResultSets=True;App=EntityFramework&amp;quot;" providerName="System.Data.EntityClient" />
    ```
24. <span data-ttu-id="7d719-176">Сохраните файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="7d719-176">Save the Web.config file.</span></span>

## <a name="sharepoint-list-on-the-app-web-notes-scenario"></a><span data-ttu-id="7d719-177">Список SharePoint на сайте приложения (сценарий заметки)</span><span class="sxs-lookup"><span data-stu-id="7d719-177">SharePoint list on the app web (Notes scenario)</span></span>
<span data-ttu-id="7d719-178"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-178"></span></span>

<span data-ttu-id="7d719-179">Сценарии списка заметки на сайте приложения с помощью списка SharePoint, показано, как выполнить списками в веб-приложения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-179">The Notes list scenario, which uses a SharePoint list on an app web, shows how lists perform in a SharePoint app web.</span></span> <span data-ttu-id="7d719-180">В веб-приложения с помощью поля Название и описание создается список заметок.</span><span class="sxs-lookup"><span data-stu-id="7d719-180">The Notes list is created in the app web with a title and description field.</span></span> <span data-ttu-id="7d719-181">API-Интерфейс REST SharePoint запрашивает список заметок и возвращает все заметки по идентификатору клиента.</span><span class="sxs-lookup"><span data-stu-id="7d719-181">The SharePoint REST API queries the Notes list and returns all the notes based on a customer ID.</span></span>

<span data-ttu-id="7d719-182">С помощью списков в веб-приложение имеет важных преимуществ других решений хранения данных: можно использовать простой вызовов API-Интерфейс SharePoint REST для запроса данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-182">Using lists in the app web has one important advantage over other storage solutions: you can use simple SharePoint REST API calls to query data.</span></span> <span data-ttu-id="7d719-183">Однако есть некоторые недостатки:</span><span class="sxs-lookup"><span data-stu-id="7d719-183">However, there are some disadvantages:</span></span>

- <span data-ttu-id="7d719-184">Чтобы обновить список метаданных, необходимо обновить и снова развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="7d719-184">To update list metadata, you must update and redeploy the app.</span></span>
    
- <span data-ttu-id="7d719-185">Чтобы обновить структуру данных, необходимо переписать логики приложения для хранения и обновления данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-185">To update the data structure, you must rewrite application logic for storing and updating data.</span></span>
    
- <span data-ttu-id="7d719-186">Данные, хранящиеся в списке не могут быть легко доступны другие надстройки.</span><span class="sxs-lookup"><span data-stu-id="7d719-186">Information stored in the list cannot be shared easily with other add-ins.</span></span>
    
- <span data-ttu-id="7d719-187">Не удается найти данные в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-187">You cannot search for data in SharePoint.</span></span>
    
- <span data-ttu-id="7d719-188">Объем данных, которые могут храниться в списках и размер наборы результатов запроса ограничены.</span><span class="sxs-lookup"><span data-stu-id="7d719-188">The amount of data that you can store in lists and the size of query result sets are limited.</span></span>
    
<span data-ttu-id="7d719-189">Код, лежащий в основе разделе Notes панель мониторинга клиентов использует запросы REST для извлечения данных из списка, разворачиваемое на сайте приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-189">The code that underlies the Notes section of the customer dashboard uses REST queries to retrieve data from a list that is deployed to the app web.</span></span> <span data-ttu-id="7d719-190">Этот список содержит поля для заголовков, авторов, идентификаторы клиента и описания.</span><span class="sxs-lookup"><span data-stu-id="7d719-190">This list contains fields for titles, authors, customer IDs, and descriptions.</span></span> <span data-ttu-id="7d719-191">Интерфейс приложения можно использовать для добавления и извлечения примечания для указанного клиента, как показано на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="7d719-191">You can use the app's interface to add and retrieve notes for a specified customer, as shown in Figure 5.</span></span>

<span data-ttu-id="7d719-192">**На рисунке 5. Пользовательский интерфейс для приложения заметки**</span><span class="sxs-lookup"><span data-stu-id="7d719-192">**Figure 5. User interface for the Notes app**</span></span>

![Снимок экрана, которая отображает пользовательский Интерфейс для модели хранения данных Notes](media/d98ce2cf-5022-4f2b-ad3e-da4eea52dfb2.png)

<span data-ttu-id="7d719-194">Ссылку **Просмотреть список заметок в веб-приложение** обеспечивает представление данных списков «по умолчанию».</span><span class="sxs-lookup"><span data-stu-id="7d719-194">The  **View Notes List in App Web** link provides an "out of the box" view of the list data.</span></span>

<span data-ttu-id="7d719-195">Это приложение использует шаблон Model-View-Controller (MVC).</span><span class="sxs-lookup"><span data-stu-id="7d719-195">This app uses the Model-View-Controller (MVC) pattern.</span></span> <span data-ttu-id="7d719-196">Можно просмотреть код для сценария примечания в файле Views/CustomerDashboard/Notes.cshtml.</span><span class="sxs-lookup"><span data-stu-id="7d719-196">You can see the code for the notes scenario in the Views/CustomerDashboard/Notes.cshtml file.</span></span> <span data-ttu-id="7d719-197">Простой вызовов REST используется для добавления и извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-197">It uses simple REST calls to add and retrieve data.</span></span> <span data-ttu-id="7d719-198">Следующий код получает заметки в списке заметки для указанного клиента.</span><span class="sxs-lookup"><span data-stu-id="7d719-198">The following code retrieves notes from the Notes list for a specified customer.</span></span>

```C#
function getNotesAndShow() {
    var executor = new SP.RequestExecutor(appWebUrl);
    executor.executeAsync(
       {
           url: appWebUrl + "/_api/web/lists/getByTitle('Notes')/items/" +
                "?$select=FTCAM_Description,Modified,Title,Author/ID,Author/Title" +
                "&amp;$expand=Author/ID,Author/Title" +
                "&amp;$filter=(Title eq '" + customerID + "')",
           type: "GET",
           dataType: 'json',
           headers: { "accept": "application/json;odata=verbose" },
           success: function (data) {
               var value = JSON.parse(data.body);
               showNotes(value.d.results);
           },
           error: function (error) { console.log(JSON.stringify(error)) }
       }

    );
}
```

<span data-ttu-id="7d719-199">Следующий код добавляет Примечание для данного клиента в список заметок.</span><span class="sxs-lookup"><span data-stu-id="7d719-199">The following code adds a note for a given customer to the notes list.</span></span>

```C#
function addNoteToList(note, customerID) {
    var executor = new SP.RequestExecutor(appWebUrl);
    var bodyProps = {
        '__metadata': { 'type': 'SP.Data.NotesListItem' },
        'Title': customerID,
        'FTCAM_Description': note
    };
    executor.executeAsync({
        url: appWebUrl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('Notes')/items?@target='" + appWebUrl + "'",
        contentType: "application/json;odata=verbose",
        method: "POST",
        headers: {
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        body: JSON.stringify(bodyProps),
        success: getNotesAndShow,
        error: addNoteFailed
    });
}
```

<span data-ttu-id="7d719-200">5000 элементов можно добавить в список, чтобы показать, что список запросов, получения результата набор 5000 или большего числа элементов будет выполняться и сбора данных для пороговое значение для списка.</span><span class="sxs-lookup"><span data-stu-id="7d719-200">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span></span> <span data-ttu-id="7d719-201">Также можно добавить столько данных в список на сайте приложения, превышает ограничение хранилища для семейства веб-сайтов (которого зависит от того, как объем памяти вы выделенный к нему).</span><span class="sxs-lookup"><span data-stu-id="7d719-201">You can also add so much data to your list on the app web that you exceed the storage limit for your site collection (which depends on how much storage space you've allocated to it).</span></span> <span data-ttu-id="7d719-202">Эти сценарии демонстрируют два из наиболее важные ограничения этот подход: списка ограничения на размер запроса и ограничения пространства для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-202">These scenarios show two of the most important limitations of this approach: list query size limits and storage space limits.</span></span> <span data-ttu-id="7d719-203">Если организации требуется требуется при работе с большими наборами данных и наборы результатов запроса, этот подход не работает.</span><span class="sxs-lookup"><span data-stu-id="7d719-203">If your business needs require you to work with large data sets and query result sets, this approach won't work.</span></span>

### <a name="list-query-threshold"></a><span data-ttu-id="7d719-204">Пороговое значение для списка</span><span class="sxs-lookup"><span data-stu-id="7d719-204">List query threshold</span></span>
<span data-ttu-id="7d719-205"><a name="bk_listquerythreshold"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-205"></span></span>

<span data-ttu-id="7d719-206">Для загрузки достаточно данных превышает пороговое значение ограничения запроса списка:</span><span class="sxs-lookup"><span data-stu-id="7d719-206">To load enough data to exceed the list query threshold limit:</span></span>


1. <span data-ttu-id="7d719-207">В левой панели выберите **Пример домашней страницы**.</span><span class="sxs-lookup"><span data-stu-id="7d719-207">In the left menu, choose  **Sample Home Page**.</span></span>
    
2. <span data-ttu-id="7d719-208">В разделе **Пороговые значения запросов списка** выберите **Добавить элементы списка в список заметок в веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="7d719-208">In the  **List Query Thresholds** section, choose **Add list items to the Notes list in the App Web**.</span></span>
    
3. <span data-ttu-id="7d719-209">Следуя инструкциям, которые отображаются над кнопкой эта операция 10 раз.</span><span class="sxs-lookup"><span data-stu-id="7d719-209">Per the instructions that appear above the button, perform this operation 10 times.</span></span>
    
    <span data-ttu-id="7d719-210">При обновлении списка заметок в верхней части страницы, которое указывает, сколько элементов списка (примечания), вы добавили появится сообщение и сколько остаются для добавления.</span><span class="sxs-lookup"><span data-stu-id="7d719-210">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span></span>
    
    <span data-ttu-id="7d719-211">**Примечание**  Около одной минуты выполняется операция каждый раз, когда нажмите кнопку Запуск.</span><span class="sxs-lookup"><span data-stu-id="7d719-211">**Note**  The operation takes about one minute to run each time you choose the button.</span></span> <span data-ttu-id="7d719-212">Конечный результат выполнения операции 10 раз показано на рисунке 6.</span><span class="sxs-lookup"><span data-stu-id="7d719-212">The end result of running the operation 10 times is shown in Figure 6.</span></span>
4. <span data-ttu-id="7d719-213">После добавления 5,001 элементов в список, выберите в меню слева заметки.</span><span class="sxs-lookup"><span data-stu-id="7d719-213">After you've added 5,001 items to the list, choose Notes in the left menu.</span></span> <span data-ttu-id="7d719-214">При загрузке страницы, появится сообщение об ошибке, показано на рисунке 6, для которого извлекаются из интерфейса API REST SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-214">When the page loads, you will see the error message shown in Figure 6, which comes from the SharePoint REST API.</span></span>
    
    <span data-ttu-id="7d719-215">**На рисунке 6. Список запроса thresold превысила сообщение об ошибке**</span><span class="sxs-lookup"><span data-stu-id="7d719-215">**Figure 6. List query thresold exceeded error message**</span></span>

    ![Снимок экрана, которая отображает сообщение об ошибке о том, что операция превысила threshol представления списка.](media/90202b64-4b14-4764-9a4c-8fb236f8d10b.png)

5. <span data-ttu-id="7d719-217">Выберите **Список заметок в веб-приложения** и прокрутите список, чтобы увидеть, что она включает 500 строк.</span><span class="sxs-lookup"><span data-stu-id="7d719-217">Choose  **View Notes List in App Web** and page through the list to see that it includes 500 rows.</span></span> <span data-ttu-id="7d719-218">Обратите внимание, что несмотря на то, что представлений списка SharePoint можно обеспечить просмотр этого большого количества операций, API-Интерфейс REST не удается выполнить из-за регулировки порогового значения списка запросов.</span><span class="sxs-lookup"><span data-stu-id="7d719-218">Note that although SharePoint list views can accommodate browsing of this many entries, the REST API fails due to the list query throttling threshold.</span></span>
    
### <a name="data-storage-limit"></a><span data-ttu-id="7d719-219">Ограничение хранилища данных</span><span class="sxs-lookup"><span data-stu-id="7d719-219">Data storage limit</span></span>
<span data-ttu-id="7d719-220"><a name="bk_listquerythreshold"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-220"></span></span>

<span data-ttu-id="7d719-221">Для загрузки достаточно данных превышает ограничение хранилища данных:</span><span class="sxs-lookup"><span data-stu-id="7d719-221">To load enough data to exceed the data storage limit:</span></span>

1. <span data-ttu-id="7d719-222">В левой панели выберите **Пример домашней страницы**.</span><span class="sxs-lookup"><span data-stu-id="7d719-222">In the left menu, choose  **Sample Home Page**.</span></span>
    
2. <span data-ttu-id="7d719-223">В разделе порогового значения данных должны **заполнить список заметок Web App с 1 ГБ данных**.</span><span class="sxs-lookup"><span data-stu-id="7d719-223">In the Data Threshold section, choose  **Fill the App Web Notes list with 1GB of data**.</span></span>
    
3. <span data-ttu-id="7d719-224">Следуя инструкциям, которые отображаются над кнопкой **заполнить список заметок Web App с 1 ГБ данных** эта операция 11 раз.</span><span class="sxs-lookup"><span data-stu-id="7d719-224">Per the instructions that appear above the  **Fill the App Web Notes list with 1GB of data** button, perform this operation 11 times.</span></span>
    
    <span data-ttu-id="7d719-225">При обновлении списка заметок в верхней части страницы, которое указывает, сколько элементов списка (примечания), вы добавили появится сообщение и сколько остаются для добавления.</span><span class="sxs-lookup"><span data-stu-id="7d719-225">When the Notes list is updated, a message appears at the top of the page that indicates how many list items (Notes) you added and how many are left to add.</span></span>
    
    <span data-ttu-id="7d719-226">**Примечание**  Около одной минуты выполняется операция каждый раз, когда нажмите кнопку Запуск.</span><span class="sxs-lookup"><span data-stu-id="7d719-226">**Note**  The operation takes about one minute to run each time you choose the button.</span></span> <span data-ttu-id="7d719-227">Конечный результат выполнения операции 11 раз показано на рисунке 7.</span><span class="sxs-lookup"><span data-stu-id="7d719-227">The end result of running the operation 11 times is shown in Figure 7.</span></span>
4. <span data-ttu-id="7d719-228">После выполнения операции 11 раз, появится сообщение об ошибке при нажатии кнопки, как показано на рисунке 7.</span><span class="sxs-lookup"><span data-stu-id="7d719-228">After you perform the operation 11 times, an error message will occur when you choose the button, as shown in Figure 7.</span></span>
    
    <span data-ttu-id="7d719-229">**На рисунке 7. Сообщение об ошибке Превышен хранилища данных**</span><span class="sxs-lookup"><span data-stu-id="7d719-229">**Figure 7. Data storage threshold exceeded error message**</span></span>

    ![Снимок экрана, которая отображает сообщение об ошибке, выполняемое при превышении ограничений хранилища данных](media/0bc55483-0ee1-487a-ba34-e827ec47aadd.png)

5. <span data-ttu-id="7d719-231">После превышает ограничение хранилища данных, нажмите кнопку возврата в веб-браузере и затем выберите ссылку **заметки** в меню слева.</span><span class="sxs-lookup"><span data-stu-id="7d719-231">After you exceed the data storage limit, choose the back button in the web browser, and then choose the  **Notes** link in the left menu.</span></span>
    
6. <span data-ttu-id="7d719-232">Выберите **список заметок в веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="7d719-232">Choose  **View Notes List in App Web**.</span></span>
    
    <span data-ttu-id="7d719-233">При загрузке страницы, сообщение об ошибке отображается в верхней части страницы, которое указывает, что сайт недостаточно дискового пространства.</span><span class="sxs-lookup"><span data-stu-id="7d719-233">When the page loads, an error message appears at the top of the page that indicates that the site is out of storage space.</span></span>

## <a name="sharepoint-list-on-the-host-web-support-cases-scenario"></a><span data-ttu-id="7d719-234">Список SharePoint на хост-сайта (поддержка случаев сценария)</span><span class="sxs-lookup"><span data-stu-id="7d719-234">SharePoint list on the host web (Support Cases scenario)</span></span>
<span data-ttu-id="7d719-235"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-235"></span></span>

<span data-ttu-id="7d719-236">В сценарии поддержки случаев отображает данные, которые хранятся в списке SharePoint на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="7d719-236">The Support Cases scenario displays data that is stored in a SharePoint list in the host web.</span></span> <span data-ttu-id="7d719-237">В этом сценарии используются два различных шаблона для доступа и взаимодействия с данными.</span><span class="sxs-lookup"><span data-stu-id="7d719-237">This scenario uses two different patterns to access and interact with the data.</span></span> <span data-ttu-id="7d719-238">Первый шаблон включает в себя службы поиска SharePoint и применения содержимого с веб-части поиска с помощью настраиваемого шаблона для отображения.</span><span class="sxs-lookup"><span data-stu-id="7d719-238">The first pattern includes the SharePoint Search Service and the Content By Search Web Part with a custom Display Template applied.</span></span> <span data-ttu-id="7d719-239">Второй шаблон содержит часть приложения (веб-часть клиента), который отображается представление MVC, который использует **SP. RequestExecutor** вызов API-Интерфейс SharePoint REST.</span><span class="sxs-lookup"><span data-stu-id="7d719-239">The second pattern includes an App Part (Client Web Part) that displays an MVC view, which uses the  **SP.RequestExecutor** class to call the SharePoint REST API.</span></span>

<span data-ttu-id="7d719-240">Существует несколько преимуществ использования этого подхода:</span><span class="sxs-lookup"><span data-stu-id="7d719-240">There are several advantages to using this approach:</span></span>

- <span data-ttu-id="7d719-241">Можно выполнить запрос данных с помощью простых запросов REST или код объектной модели клиента.</span><span class="sxs-lookup"><span data-stu-id="7d719-241">You can query data easily using simple REST queries or client object model code.</span></span>
    
- <span data-ttu-id="7d719-242">Можно выполнить поиск данных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-242">You can search for data in SharePoint.</span></span>
    
- <span data-ttu-id="7d719-243">Можно обновлять метаданные списка и создавать новые представления для списка без обновления и повторное развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-243">You can update the list metadata and create new views for a list without updating and redeploying the app.</span></span> <span data-ttu-id="7d719-244">Эти изменения не влияет на поведение приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-244">These changes won't affect the behavior of your app.</span></span>
    
- <span data-ttu-id="7d719-245">Списки на веб-сайт не удаляются при удалении приложения, если приложение не использует события **AppUninstalled** Чтобы удалить список и/или удалить данные.</span><span class="sxs-lookup"><span data-stu-id="7d719-245">Lists on the host web are not deleted when you uninstall your app, unless the app uses the  **AppUninstalled** event to remove the list and/or delete the data.</span></span>
    
<span data-ttu-id="7d719-246">Смещения эти преимущества являются следующие недостатки:</span><span class="sxs-lookup"><span data-stu-id="7d719-246">Offsetting these advantages are the following disadvantages:</span></span>

- <span data-ttu-id="7d719-247">Веб-сайт ограничивает объем данных, которые можно хранить в списках и размера результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="7d719-247">The host web limits both the amount of data you can store in lists and the size of the query results.</span></span> <span data-ttu-id="7d719-248">Если организации требуется для хранения и/или запрос больших наборов данных, это не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="7d719-248">If your business needs require storing and/or querying large data sets, this is not a recommended approach.</span></span>
    
- <span data-ttu-id="7d719-249">Для сложных запросов а также баз данных выполните списков.</span><span class="sxs-lookup"><span data-stu-id="7d719-249">For complex queries, lists do not perform as well as databases.</span></span>
    
- <span data-ttu-id="7d719-250">Для резервного копирования и восстановления данных, а также баз данных выполните списков.</span><span class="sxs-lookup"><span data-stu-id="7d719-250">For backing up and restoring data, lists do not perform as well as databases.</span></span>
    
<span data-ttu-id="7d719-251">В списке SharePoint, развертывать на хост-сайта хранятся данные для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="7d719-251">The data for this scenario is stored in a SharePoint list deployed to the host web.</span></span> <span data-ttu-id="7d719-252">Данные извлекаются и отображаются с помощью следующих:</span><span class="sxs-lookup"><span data-stu-id="7d719-252">Data is retrieved and displayed by means of the following:</span></span> 

- <span data-ttu-id="7d719-253">[Веб-часть поиска контента](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d719-253">A  [Content Search Web Part](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).</span></span>
    
- <span data-ttu-id="7d719-254">Часть приложения, реализованные в виде model-view-controller представления.</span><span class="sxs-lookup"><span data-stu-id="7d719-254">An app part that's implemented as a model-view-controller view.</span></span> 
    
<span data-ttu-id="7d719-255">Код в этом представлении используется запросов REST для получения сведений из списка, а веб-часть поиска контента службы поиска SharePoint для извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-255">The code in this view uses REST queries to retrieve information from the list, while the content search web part uses the SharePoint search service to retrieve the data.</span></span> <span data-ttu-id="7d719-256">Два подхода Демонстрация значительные преимущества этого параметра: служба поиска и интерфейсы API REST или CSOM можно использовать для получения сведений из списка на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="7d719-256">The two approaches demonstrate the significant advantage of this option: you can use both the search service and the REST/CSOM APIs to retrieve information from a list on the host web.</span></span>

<span data-ttu-id="7d719-257">Если выбрать клиента из раскрывающегося списка вариантов поддержки вы увидите данные вариантов поддержки для клиента отображаются в веб-частей и веб-части приложения (на рисунке 8).</span><span class="sxs-lookup"><span data-stu-id="7d719-257">When you select a customer from the support cases drop-down, you'll see the support case data for that customer displayed in both the web part and the app part (Figure 8).</span></span> <span data-ttu-id="7d719-258">Веб-части могут возвращает содержимое сразу, так как он может занять до 24 часов для службы поиска SharePoint для индексации данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-258">The web part might not return content right away, because it can take up to 24 hours for the SharePoint search service to index the data.</span></span> <span data-ttu-id="7d719-259">Вы также можете ссылку **Список вариантов поддержки представления в веб-сайт** , чтобы увидеть обычное представление данных списков.</span><span class="sxs-lookup"><span data-stu-id="7d719-259">You can also choose the  **View Support Cases List in Host Web** link to see a conventional view of the list data.</span></span>

<span data-ttu-id="7d719-260">**На рисунке 8. Пользовательский интерфейс для поддержки сценарий**</span><span class="sxs-lookup"><span data-stu-id="7d719-260">**Figure 8. User interface for the support case scenario**</span></span>

![Снимок экрана, которая отображает пользовательский Интерфейс для взаимодействия со сценарием вариантов поддержки](media/eac41f5c-90b7-4fe3-b47e-0d65b79cbf1c.png)

<span data-ttu-id="7d719-262">Веб-часть поиска контента, развертывания с помощью этого приложения с помощью шаблона для отображения настраиваемых.</span><span class="sxs-lookup"><span data-stu-id="7d719-262">The content search web part deployed by this app uses a custom display template.</span></span> <span data-ttu-id="7d719-263">На рисунке 9 показан, где в каталоге **средств** веб-проекта можно найти в веб-части и связанный шаблон.</span><span class="sxs-lookup"><span data-stu-id="7d719-263">Figure 9 shows where in the  **Assets** directory of the web project you can find the web part and the associated template.</span></span>

<span data-ttu-id="7d719-264">**На рисунке 9. Содержимое каталога средств веб-проекта**</span><span class="sxs-lookup"><span data-stu-id="7d719-264">**Figure 9. Contents of the Assets directory of the web project**</span></span>

![Снимок экрана в каталоге активов](media/95db9118-9e56-4e39-84b1-271e54447792.png)

<span data-ttu-id="7d719-266">Приведенный ниже код JavaScript, который можно найти в файле Views/SupportCaseAppPart\Index.cshtml использует междоменную библиотеку для вызова запросов REST в списке SharePoint на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="7d719-266">The following JavaScript code that you'll find in the Views/SupportCaseAppPart\Index.cshtml file uses the cross-domain library to invoke a REST query on the SharePoint list on the host web.</span></span> 

```C#
function execCrossDomainRequest() {
var executor = new SP.RequestExecutor(appWebUrl);

executor.executeAsync(
   {
        url: appWebUrl + "/_api/SP.AppContextSite(@@target)" +
                "/web/lists/getbytitle('Support Cases')/items" +
              "?$filter=(FTCAM_CustomerID eq '" + customerID + "')" +
            "&amp;$top=30" +
                    "&amp;$select=Id,Title,FTCAM_Status,FTCAM_CSR" +
                    "&amp;@@target='" + hostWebUrl + "'",
method: "GET",
              headers: { "Accept": "application/json; odata=verbose" },
              success: successHandler,
              error: errorHandler
   }
);
}
```

<span data-ttu-id="7d719-267">5000 элементов можно добавить в список, чтобы показать, что список запросов, получения результата набор 5000 или большего числа элементов будет выполняться и сбора данных для пороговое значение для списка.</span><span class="sxs-lookup"><span data-stu-id="7d719-267">You can add 5000 items to the list to show that list queries that generate a result set of 5000 or more items will hit the list query threshold and fail.</span></span> <span data-ttu-id="7d719-268">В данном сценарии показано одно из наиболее важные ограничения этот подход: список ограничения на размер запроса.</span><span class="sxs-lookup"><span data-stu-id="7d719-268">This scenario shows one of the most important limitations of this approach: list query size limits.</span></span> <span data-ttu-id="7d719-269">Если бизнеса требуется требуется работать с большим объемом данных и наборы результатов запроса, этот подход не работает.</span><span class="sxs-lookup"><span data-stu-id="7d719-269">If your business needs require you to work with large data and query result sets, this approach won't work.</span></span> <span data-ttu-id="7d719-270">Для получения дополнительных сведений см [пороговое значение для списка](#bk_listquerythreshold) ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7d719-270">For more information, see  [List query threshold](#bk_listquerythreshold) earlier in this article.</span></span>

## <a name="northwind-odata-web-service-customer-dashboard-scenario"></a><span data-ttu-id="7d719-271">Веб-службе Northwind OData (панель мониторинга клиентов сценария)</span><span class="sxs-lookup"><span data-stu-id="7d719-271">Northwind OData web service (Customer Dashboard scenario)</span></span>
<span data-ttu-id="7d719-272"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-272"></span></span>

<span data-ttu-id="7d719-273">Сценарий панели мониторинга клиентов использует JQuery AJAX для запуска службы NorthWind OData, чтобы получить сведения о клиенте.</span><span class="sxs-lookup"><span data-stu-id="7d719-273">The Customer Dashboard scenario uses JQuery AJAX to invoke the NorthWind OData service to return customer information.</span></span> <span data-ttu-id="7d719-274">Приложение хранит данные в веб-службе, а затем получать его с помощью [OData](http://www.odata.org/) .</span><span class="sxs-lookup"><span data-stu-id="7d719-274">The app stores its data in a web service, then uses  [OData](http://www.odata.org/) to retrieve it.</span></span>

<span data-ttu-id="7d719-275">Ниже приведены преимущества использования этого подхода.</span><span class="sxs-lookup"><span data-stu-id="7d719-275">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="7d719-276">Данной веб-службы может поддерживать несколько надстроек.</span><span class="sxs-lookup"><span data-stu-id="7d719-276">A given web service can support multiple add-ins.</span></span>
    
- <span data-ttu-id="7d719-277">Вы можете обновить веб-службы без необходимости обновите и повторно разверните вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-277">You can update your web service without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="7d719-278">Установок SharePoint и веб-службы не влияют на друг с другом.</span><span class="sxs-lookup"><span data-stu-id="7d719-278">Your SharePoint and web service installations do not affect one another.</span></span>
    
- <span data-ttu-id="7d719-279">Размещение служб, таких как Microsoft Azure позволяют масштабирования веб-служб.</span><span class="sxs-lookup"><span data-stu-id="7d719-279">Hosting services such as Microsoft Azure enable you to scale your web services.</span></span>
    
- <span data-ttu-id="7d719-280">Можно резервное копирование и восстановление сведений на веб-служб отдельно из сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-280">You can back up and restore information on your web services separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="7d719-281">Не потерять данные при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-281">You don't lose data when uninstalling your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="7d719-282">Сценарий панели мониторинга клиентов хранит данные в веб-службы, который реализует стандарта OData для извлечения данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-282">The customer dashboard scenario stores its data in a web service that implements the OData standard to retrieve data.</span></span> <span data-ttu-id="7d719-283">В интерфейсе клиента панели мониторинга выбрать клиента из раскрывающегося меню и отображает сведения о клиента в области **Сведения о клиенте** .</span><span class="sxs-lookup"><span data-stu-id="7d719-283">In the customer dashboard interface, you select a customer from a drop-down menu, and customer information displays in the  **Customer Info** pane.</span></span>

<span data-ttu-id="7d719-284">На этой странице пользовательского интерфейса — это представление Model-View-Controller.</span><span class="sxs-lookup"><span data-stu-id="7d719-284">This UI page is a Model-View-Controller view.</span></span> <span data-ttu-id="7d719-285">Отображение определяется в файле Views/CustomerDashboard\Home.cshtml.</span><span class="sxs-lookup"><span data-stu-id="7d719-285">The display is defined in the Views/CustomerDashboard\Home.cshtml file.</span></span> <span data-ttu-id="7d719-286">Базовый код содержится в файле Scripts/CustomerDashboard.js.</span><span class="sxs-lookup"><span data-stu-id="7d719-286">The underlying code is in the Scripts/CustomerDashboard.js file.</span></span> <span data-ttu-id="7d719-287">Код JavaScript использует AJAX для запроса веб-службе "Борей".</span><span class="sxs-lookup"><span data-stu-id="7d719-287">The JavaScript code uses AJAX to query the Northwind web service.</span></span> <span data-ttu-id="7d719-288">Так как это службе OData, веб-службы запросов состоит из аргументы строки запроса, подключенного к URL-адрес, указывающий на конечную веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7d719-288">Because this is an OData service, the web service query consists of query string arguments attached to a URL that points to a web service endpoint.</span></span> <span data-ttu-id="7d719-289">Служба возвращает сведения о пользователе в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="7d719-289">The service returns customer information in JSON format.</span></span>

<span data-ttu-id="7d719-290">Приведенный ниже код запускается при выборе ссылки **Панель мониторинга клиентов** .</span><span class="sxs-lookup"><span data-stu-id="7d719-290">The following code runs when you choose the  **Customer Dashboard** link.</span></span> <span data-ttu-id="7d719-291">Он получает все идентификаторы и имена клиентов для заполнения в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="7d719-291">It retrieves all the customer names and IDs in order to populate the drop-down menu.</span></span>

```C#
var getCustomerIDsUrl = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json&amp;$select=CustomerID";
    $.get(getCustomerIDsUrl).done(getCustomerIDsDone)
        .error(function (jqXHR, textStatus, errorThrown) {
            $('#topErrorMessage').text('Can\'t get customers. An error occurred: ' + jqXHR.statusText);
        });
```

<span data-ttu-id="7d719-292">Приведенный ниже код выполняется, когда имя клиента выберите в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="7d719-292">The following code runs when you select a customer name from the drop-down menu.</span></span> <span data-ttu-id="7d719-293">Аргумент **$filter** OData используется для указания идентификатора клиента и другие аргументы строки запроса для получения сведений, связанных с этим клиентом.</span><span class="sxs-lookup"><span data-stu-id="7d719-293">It uses the OData  **$filter** argument to specify the customer ID and other query string arguments to retrieve information related to this customer.</span></span>

```C#
var url = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json" +  "&amp;$select=CustomerID,CompanyName,ContactName,ContactTitle,Address,City,Country,Phone,Fax" + "&amp;$filter=CustomerID eq '" + customerID + "'";

$.get(url).done(getCustomersDone)
   .error(function (jqXHR, textStatus, errorThrown) {
          alert('Can\'t get customer ' + customerID + '. An error occurred: ' + 
                 jqXHR.statusText);
});
```

## <a name="azure-table-storage-customer-service-survey-scenario"></a><span data-ttu-id="7d719-294">Хранение таблицы Azure (сценарий опроса службы клиента)</span><span class="sxs-lookup"><span data-stu-id="7d719-294">Azure table storage (Customer Service Survey scenario)</span></span>
<span data-ttu-id="7d719-295"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-295"></span></span>

<span data-ttu-id="7d719-296">Сценарий опроса службы клиента позволяет представителю службы для просмотра их оценки, опросы клиентов на основе клиента и использует хранилища Azure таблицы и Microsoft.WindowsAzure.Storage.Table.CloudTable API для хранения и взаимодействия с данными.</span><span class="sxs-lookup"><span data-stu-id="7d719-296">The Customer Service Survey scenario allows a customer service representative to see their rating based on customer surveys and uses Azure table storage and the Microsoft.WindowsAzure.Storage.Table.CloudTable API to store and interact with the data.</span></span>

<span data-ttu-id="7d719-297">Ниже приведены преимущества использования этого подхода.</span><span class="sxs-lookup"><span data-stu-id="7d719-297">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="7d719-298">Таблицы Azure хранилища поддерживает более одного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-298">Azure storage tables support more than one app.</span></span>
    
- <span data-ttu-id="7d719-299">Можно обновить таблиц Azure хранения без необходимости обновите и повторно разверните вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-299">You can update Azure storage tables without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="7d719-300">Установки SharePoint и таблиц Azure хранения не оказывают влияния на производительность друг друга.</span><span class="sxs-lookup"><span data-stu-id="7d719-300">Your SharePoint installation and Azure storage tables have no effect on each other's performance.</span></span>
    
- <span data-ttu-id="7d719-301">Хранилище Azure легко таблиц масштабирования.</span><span class="sxs-lookup"><span data-stu-id="7d719-301">Azure storage tables scale easily.</span></span>
    
- <span data-ttu-id="7d719-302">Можно резервное копирование и восстановление хранилища Azure таблиц отдельно от сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-302">You can back up and restore your Azure storage tables separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="7d719-303">Не потерять данные при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-303">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="7d719-304">Интерфейс приложения отображается оценка опроса текущего пользователя на странице центра.</span><span class="sxs-lookup"><span data-stu-id="7d719-304">The app's interface displays the current user's survey rating in the center page.</span></span> <span data-ttu-id="7d719-305">Если таблицы Azure хранилища пустое, приложение добавьте некоторые данные в таблицу до его отображения.</span><span class="sxs-lookup"><span data-stu-id="7d719-305">If that Azure storage table is empty, the app will add some information to the table before it displays it.</span></span>

<span data-ttu-id="7d719-306">Следующий код из CSRInfoController.cs определяет метод **Домашняя страница** , который извлекает пользователя **nameId**.</span><span class="sxs-lookup"><span data-stu-id="7d719-306">The following code from the CSRInfoController.cs defines the  **Home** method that retrieves the user's **nameId**.</span></span>

```C#
[SharePointContextFilter]
public ActionResult Home()
{
    var context = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);
    var sharePointService = new SharePointService(context);
    var currentUser = sharePointService.GetCurrentUser();
    ViewBag.UserName = currentUser.Title;

    var surveyRatingsService = new SurveyRatingsService();
    ViewBag.Score = surveyRatingsService.GetUserScore(currentUser.UserId.NameId);

    return View();
}
```

<span data-ttu-id="7d719-307">Следующий код из файла SurveyRatingService.cs определяет конструктор **SurveyRatingsService** , который выполняет настройку подключения к учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7d719-307">The following code from the SurveyRatingService.cs file defines the  **SurveyRatingsService** constructor, which sets up the connection to the Azure storage account.</span></span>

```C#
public SurveyRatingsService(string storageConnectionStringConfigName = 
        "StorageConnectionString")
{
    var connectionString = Util.GetConfigSetting("StorageConnectionString");
    var storageAccount = CloudStorageAccount.Parse(connectionString);

    this.tableClient = storageAccount.CreateCloudTableClient();
    this.surveyRatingsTable = this.tableClient.GetTableReference("SurveyRatings");
    this.surveyRatingsTable.CreateIfNotExists();
}
```

<span data-ttu-id="7d719-308">Следующий код из одного файла определяет метод **GetUserScore** , который получает показатель опроса пользователя из таблицы Azure хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d719-308">The following code from the same file defines the  **GetUserScore** method, which retrieves the user's survey score from the Azure storage table.</span></span>

```C#
public float GetUserScore(string userName)
{
    var query = new TableQuery<Models.Customer>()
    .Select(new List<string> { "Score" })
    .Where(TableQuery.GenerateFilterCondition("Name", 
    QueryComparisons.Equal, userName));

    var items = surveyRatingsTable
         .ExecuteQuery(query)
             .ToArray();

    if (items.Length == 0)           
    return AddSurveyRatings(userName);

    return (float)items.Average(c => c.Score);
}
```

<span data-ttu-id="7d719-309">Если в таблице не содержит все данные опроса, связанные с текущим пользователем, метод **AddSurveyRating** случайным образом назначает счета для пользователя.</span><span class="sxs-lookup"><span data-stu-id="7d719-309">If the table doesn't contain any survey data related to the current user, the  **AddSurveyRating** method randomly assigns a score for the user.</span></span>

```C#
private float AddSurveyRatings(string userName)
{
    float sum = 0;
    int count = 4;
    var random = new Random();

    for (int i = 0; i < count; i++)
    {
    var score = random.Next(80, 100);
    var customer = new Models.Customer(Guid.NewGuid(), userName, score);

    var insertOperation = TableOperation.Insert(customer);
    surveyRatingsTable.Execute(insertOperation);

    sum += score;
    }
    return sum / count;
}
```

## <a name="azure-queue-storage-customer-call-queue-scenario"></a><span data-ttu-id="7d719-310">Хранилище Azure очереди (сценарий очереди вызовов клиента)</span><span class="sxs-lookup"><span data-stu-id="7d719-310">Azure queue storage (Customer Call Queue scenario)</span></span>
<span data-ttu-id="7d719-311"><a name="sectionSection5"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-311"></span></span>

<span data-ttu-id="7d719-312">Сценарий очередь звонков клиентов перечислены звонящих в очередь поддержки и моделирует получают звонки.</span><span class="sxs-lookup"><span data-stu-id="7d719-312">The Customer Call Queue scenario lists callers in the support queue and simulates taking calls.</span></span> <span data-ttu-id="7d719-313">В сценарии Azure хранения очередей используется для хранения данных и **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API с Model-View-Controller.</span><span class="sxs-lookup"><span data-stu-id="7d719-313">The scenario uses Azure storage queues to store data and the  **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API with Model-View-Controller.</span></span>

<span data-ttu-id="7d719-314">Ниже приведены преимущества использования этого подхода.</span><span class="sxs-lookup"><span data-stu-id="7d719-314">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="7d719-315">Очереди Azure хранилища поддерживает более одного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-315">Azure storage queues support more than one app.</span></span>
    
- <span data-ttu-id="7d719-316">Очереди Azure хранилища можно обновлять без необходимости обновите и повторно разверните вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-316">You can update Azure storage queues without having to update and redeploy your app.</span></span>
    
- <span data-ttu-id="7d719-317">Установки SharePoint и хранилища Azure очереди не оказывают влияния на производительность друг друга.</span><span class="sxs-lookup"><span data-stu-id="7d719-317">Your SharePoint installation and Azure storage queues have no effect on each other's performance.</span></span>
    
- <span data-ttu-id="7d719-318">Легко масштабировать очереди Azure хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d719-318">Azure storage queues scale easily.</span></span>
    
- <span data-ttu-id="7d719-319">Можно резервное копирование и восстановление вашей очереди Azure хранилища отдельно от сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d719-319">You can back up and restore your Azure storage queues separately from your SharePoint site.</span></span>
    
- <span data-ttu-id="7d719-320">Не потерять данные при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-320">You don't lose data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="7d719-321">Интерфейс приложения отображается очередь вызова поддержки в центральной области при выборе ссылки **Вызова очереди** .</span><span class="sxs-lookup"><span data-stu-id="7d719-321">The app's interface displays a support call queue in the center pane when you choose the  **Call Queue** link.</span></span> <span data-ttu-id="7d719-322">Получение вызовов (Добавление вызова в очередь) можно смоделировать, выбрав **Моделирования звонки**и, выбрав **Принять вызов** действие, связанное с в конкретном вызове моделирования работы с наиболее старых вызова (с удалением звонка из очереди).</span><span class="sxs-lookup"><span data-stu-id="7d719-322">You can simulate receiving calls (adding a call to the queue) by choosing **Simulate Calls**, and you can simulate taking the oldest call (removing a call from the queue) by choosing the  **Take Call** action associated with a given call.</span></span>

<span data-ttu-id="7d719-323">На этой странице — это представление Model-View-Controller, определенных в файле Views\CallQueue\Home.cshmtl.</span><span class="sxs-lookup"><span data-stu-id="7d719-323">This page is a Model-View-Controller view that is defined in the Views\CallQueue\Home.cshmtl file.</span></span> <span data-ttu-id="7d719-324">Файл Controllers\CallQueueController.cs определяет класс **CallQueueController** , который содержит методы для получения всех звонков в очереди, добавление вызова в очередь (моделирование звонка) и их удаление звонка из очереди (с помощью вызова).</span><span class="sxs-lookup"><span data-stu-id="7d719-324">The Controllers\CallQueueController.cs file defines the  **CallQueueController** class, which contains methods for retrieving all calls in the queue, adding a call to the queue (simulating a call), and removing a call from the queue (taking a call).</span></span> <span data-ttu-id="7d719-325">Каждый из этих методов вызывает методов, определенных в файле Services\CallQueueService.cs, который используется очереди Azure хранилища API для получения базовых сведений в очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d719-325">Each of these methods calls methods defined in the Services\CallQueueService.cs file, which uses the Azure storage queue API to retrieve the underlying information in the storage queue.</span></span>

```C#
public class CallQueueController : Controller
{
    public CallQueueService CallQueueService { get; private set; }

    public CallQueueController()
    {
        CallQueueService = new CallQueueService();
    }

    // GET: CallQueue
    public ActionResult Home(UInt16 displayCount = 10)
    {
        var calls = CallQueueService.PeekCalls(displayCount);
        ViewBag.DisplayCount = displayCount;
        ViewBag.TotalCallCount = CallQueueService.GetCallCount();
        return View(calls);
    }

    [HttpPost]
    public ActionResult SimulateCalls(string spHostUrl)
    {
        int count = CallQueueService.SimulateCalls();
        TempData["Message"] = string.Format("Successfully simulated {0} calls and added them to the call queue.", count);
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }

    [HttpPost]
    public ActionResult TakeCall(string spHostUrl)
    {
        CallQueueService.DequeueCall();
        TempData["Message"] = "Call taken successfully and removed from the call queue!";
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }
}
```

<span data-ttu-id="7d719-326">Файл CallQueueService.cs определяет класс **CallQueueService** , который устанавливает подключение к очереди Azure хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d719-326">The CallQueueService.cs file defines the  **CallQueueService** class, which establishes the connection to the Azure storage queue.</span></span> <span data-ttu-id="7d719-327">Этот класс также содержит методы для добавления, удаления (извлечения) и извлечение вызовов из очереди.</span><span class="sxs-lookup"><span data-stu-id="7d719-327">That class also contains the methods for adding, removing (dequeuing), and retrieving the calls from the queue.</span></span>

```C#
public class CallQueueService
{
    private CloudQueueClient queueClient;

    private CloudQueue queue;

    public CallQueueService(string storageConnectionStringConfigName = "StorageConnectionString")
    {
        var connectionString = CloudConfigurationManager.GetSetting(storageConnectionStringConfigName);
        var storageAccount = CloudStorageAccount.Parse(connectionString);

        this.queueClient = storageAccount.CreateCloudQueueClient();
        this.queue = queueClient.GetQueueReference("calls");
        this.queue.CreateIfNotExists();
        }

        public int? GetCallCount()
        {
        queue.FetchAttributes();
        return queue.ApproximateMessageCount;
    }

    public IEnumerable<Call> PeekCalls(UInt16 count)
    {
        var messages = queue.PeekMessages(count);

        var serializer = new JavaScriptSerializer();
        foreach (var message in messages)
        {
        Call call = null;
        try
        {
        call = serializer.Deserialize<Call>(message.AsString);
        }
        catch { }

        if (call != null) yield return call;
        }
    }

    public void AddCall(Call call)
    {
        var serializer = new JavaScriptSerializer();
        var content = serializer.Serialize(call);
        var message = new CloudQueueMessage(content);
        queue.AddMessage(message);
    }

    public void DequeueCall()
    {
        var message = queue.GetMessage();
        queue.DeleteMessage(message);
    }

    public int SimulateCalls()
    {
        Random random = new Random();
        int count = random.Next(1, 6);
        for (int i = 0; i < count; i++)
        {
        int phoneNumber = random.Next();
        var call = new Call
        {
        ReceivedDate = DateTime.Now,
        PhoneNumber = phoneNumber.ToString("+1-000-000-0000")
        };
        AddCall(call);

        return count;
    }
}
```

## <a name="sql-azure-database-recent-orders-scenario"></a><span data-ttu-id="7d719-328">Базы данных SQL Azure (последние заказы сценария)</span><span class="sxs-lookup"><span data-stu-id="7d719-328">SQL Azure database (Recent Orders scenario)</span></span>
<span data-ttu-id="7d719-329"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-329"></span></span>

<span data-ttu-id="7d719-330">Сценарий последние заказы прямой вызов к базе данных Northwind SQL Azure используется для возврата всех заказов для указанного клиента.</span><span class="sxs-lookup"><span data-stu-id="7d719-330">The Recent Orders scenario uses a direct call to the Northwind SQL Azure database to return all the orders for a given customer.</span></span>

<span data-ttu-id="7d719-331">Ниже приведены преимущества использования этого подхода.</span><span class="sxs-lookup"><span data-stu-id="7d719-331">The following are the advantages to using this approach:</span></span>

- <span data-ttu-id="7d719-332">Базы данных может поддерживать более одного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d719-332">A database can support more than one app.</span></span>
    
- <span data-ttu-id="7d719-333">Можно обновить схему базы данных без необходимости обновите и повторно разверните вашего приложения, до тех пор, пока изменения схемы не влияют на запросы в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="7d719-333">You can update your database schema without having to update and redeploy your app, as long as the schema changes don't affect the queries in your app.</span></span>
    
- <span data-ttu-id="7d719-334">Реляционные базы данных можно поддерживают отношения "многие ко многим" и таким образом поддерживать более сложных бизнес-сценарии.</span><span class="sxs-lookup"><span data-stu-id="7d719-334">A relational database can support many-to-many relationships and thus support more complex business scenarios.</span></span>
    
- <span data-ttu-id="7d719-335">Средства разработки баз данных можно использовать для оптимизации проекта базы данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-335">You can use database design tools to optimize the design of your database.</span></span>
    
- <span data-ttu-id="7d719-336">Реляционные базы данных обеспечивают лучшую производительность, чем другие параметры, при необходимости выполнять сложные операции в запросах, таких как вычисления и соединений.</span><span class="sxs-lookup"><span data-stu-id="7d719-336">Relational databases provide better performance than the other options when you need to execute complex operations in your queries, such as calculations and joins.</span></span>
    
- <span data-ttu-id="7d719-337">Базы данных SQL Azure позволяет импортировать и экспортировать данные, чтобы упростить управление и перемещение данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-337">A SQL Azure database allows you to import and export data easily, so it's easier to manage and move your data.</span></span>
    
- <span data-ttu-id="7d719-338">Все данные не потеряны при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.</span><span class="sxs-lookup"><span data-stu-id="7d719-338">You don't lose any data when you uninstall your app, unless the app uses the  **AppUninstalled** event to delete the data.</span></span>
    
<span data-ttu-id="7d719-339">Последние заказы интерфейс работает как в интерфейсе клиента панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="7d719-339">The recent orders interface works much like the customer dashboard interface.</span></span> <span data-ttu-id="7d719-340">Выберите ссылку **Последних заказов** в левом столбце и затем выберите клиента из раскрывающегося меню в верхней части центральной панели.</span><span class="sxs-lookup"><span data-stu-id="7d719-340">You choose on the  **Recent Orders** link in the left column, and then choose a customer from the drop-down menu at the top of the center pane.</span></span> <span data-ttu-id="7d719-341">Список заказов из клиента отображаются в центральной панели.</span><span class="sxs-lookup"><span data-stu-id="7d719-341">A list of orders from that customer will appear in the center pane.</span></span>

<span data-ttu-id="7d719-342">На этой странице — это представление Model-View-Controller, определенных в файле Views\CustomerDashboard\Orders.cshtml.</span><span class="sxs-lookup"><span data-stu-id="7d719-342">This page is a Model-View-Controller view defined in the Views\CustomerDashboard\Orders.cshtml file.</span></span> <span data-ttu-id="7d719-343">Код в файле Controllers\CustomerDashboardController.cs использует [Entity Framework](https://msdn.microsoft.com/en-us/data/ef.aspx) для запроса к таблице **Orders** в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7d719-343">Code in the Controllers\CustomerDashboardController.cs file uses the  [Entity Framework ](https://msdn.microsoft.com/en-us/data/ef.aspx) to query the **Orders** table in your SQL Azure database.</span></span> <span data-ttu-id="7d719-344">Идентификатор клиента передается с помощью параметра строки запроса в URL-адрес, который передается, когда пользователь выбирает клиента в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="7d719-344">The customer ID is passed by using a query string parameter in the URL that is passed when the user selects a customer from the drop-down menu.</span></span> <span data-ttu-id="7d719-345">Запрос создает соединение таблицы **клиентов**, **сотрудников**и **отправителя** .</span><span class="sxs-lookup"><span data-stu-id="7d719-345">The query creates a join on the **Customer**,  **Employee**, and  **Shipper** tables.</span></span> <span data-ttu-id="7d719-346">Результат запроса затем передается в Model-View-Controller представление, отображающее результаты.</span><span class="sxs-lookup"><span data-stu-id="7d719-346">The query result is then passed to the Model-View-Controller view that displays the results.</span></span>

<span data-ttu-id="7d719-347">Следующий код из файла CustomerDashboardController.cs выполняет запрос к базе данных и возвращает данные в представление.</span><span class="sxs-lookup"><span data-stu-id="7d719-347">The following code from the CustomerDashboardController.cs file performs the database query and returns the data to the view.</span></span>

```C#
public ActionResult Orders(string customerId)
{            
    Order[] orders;
    using (var db = new NorthWindEntities())
    {
            orders = db.Orders
                  .Include(o => o.Customer)
                  .Include(o => o.Employee)
                  .Include(o => o.Shipper)
                  .Where(c => c.CustomerID == customerId)
                  .ToArray();
    }

    ViewBag.SharePointContext = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    return View(orders);
}
```

## <a name="additional-resources"></a><span data-ttu-id="7d719-348">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7d719-348">Additional resources</span></span>
<span data-ttu-id="7d719-349"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7d719-349"></span></span>

-  [<span data-ttu-id="7d719-350">Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7d719-350">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
    
-  [<span data-ttu-id="7d719-351">Шаблоны и рекомендации по разработке решений для Office 365 на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="7d719-351">Office 365 Development Patterns and Practices on GitHub</span></span>](https://github.com/SharePoint/PnP)
