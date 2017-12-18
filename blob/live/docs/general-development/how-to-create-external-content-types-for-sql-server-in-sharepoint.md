---
title: "Создание внешних типов контента для SQL Server в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7fe2fbf0-546b-4a16-b02e-a0960bfb3842
ms.openlocfilehash: df39aa0e0f31f8252756b63b4d9ec2f2fcc83bc3
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-external-content-types-for-sql-server-in-sharepoint"></a><span data-ttu-id="9fb4e-102">Создание внешних типов контента для SQL Server в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fb4e-102">How to: Create external content types for SQL Server in SharePoint</span></span>

<span data-ttu-id="9fb4e-103">Узнайте, как создать внешний тип контента для SQL Server в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-103">Learn how to create an external content type for SQL Server in SharePoint.</span></span>

<span data-ttu-id="9fb4e-p101">Создание внешнего типа контента — это ключевая задача при работе с внешними данными. Внешний тип контента содержит важную информацию о подключениях, доступе, методах операции, столбцах, фильтрах и других метаданных, которые используются для получения данных из внешнего источника данных.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p101">Creating an external content type is a pivotal task when you are working with external data. An external content type contains important information about connections, access, methods of operation, columns, filters, and other metadata that is used to retrieve the data from the external data source.</span></span>
  
    
    


## <a name="before-you-begin"></a><span data-ttu-id="9fb4e-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9fb4e-106">Before you begin</span></span>
<span data-ttu-id="9fb4e-107"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-107"><a name="section1"> </a></span></span>

<span data-ttu-id="9fb4e-p102">Работа с внешними данными требует выполнения нескольких предварительных задач, которые обеспечивают безопасный доступ к данным. Следующая информация поможет вам спланировать ваши дальнейшие действия. Кроме того, при возникновении проблем во время работы с внешними данными, эта информация поможет вам определить проблему. Чтобы получить доступ к внешним данным, вам или администратору необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p102">Working with external data requires several prerequisite tasks to enable secure access to the data. The following information can help you plan your next steps. Also, if you have problems trying to work with external data, this information can help you identify the issue. To access external data, you or an administrator must do the following:</span></span>
  
    
    
 <span data-ttu-id="9fb4e-p103">**Подготовить SQL Server**. Администратор базы данных должен предоставить разрешения, чтобы убедиться, что доступ к данным предоставлен нужным пользователям и данные не попадут в чужие руки. Также он должен создать учетную запись SQL Server, которая имеет разрешения db_owner. Кроме того, администратор базы данных может создать специальные таблицы, представления, запросы, псевдонимы столбцов и так далее, чтобы ограничить результаты до необходимых и повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p103">**Prepare SQL Server** A database administrator needs to provide permissions to make sure that that the right people have access to the data and that the data does not end up in the wrong hands. The database administrator must also create a SQL Server account that has db_owner permission. The database administrator might also want to create specific tables, views, queries, column aliases, and so on to limit the results to just what is needed and to help improve performance.</span></span>
  
    
    
 <span data-ttu-id="9fb4e-115">**Настроить службы SharePoint**. Администратор должен активировать Службы Business Connectivity Services (BCS) и Служба Secure Store.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-115">**Configure SharePoint services** An administrator must activate Business Connectivity Services (BCS) and the Secure Store Service.</span></span>
  
    
    
 <span data-ttu-id="9fb4e-116">**Настроить службу Secure Store**. Администратор должен определить наилучший режим доступа для внешнего источника данных, создать конечное приложение и задать учетные данные для конечного приложения.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-116">**Configure the Secure Store service** An administrator must determine the best access mode for the external data source, create a target application, and set the credentials for the target application.</span></span>
  
    
    
 <span data-ttu-id="9fb4e-117">**Настроить службу подключения к бизнес-данным**. Администратор должен убедиться, что пользователь, создающий внешний тип данных, имеет разрешение на хранилище метаданных подключения к бизнес-данным (BDC) и что соответствующие пользователи имеют доступ к внешнему типу контента, на котором основан внешний список.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-117">**Configure Business Data Connectivity Services** An administrator must make sure that the user who creates the external content type has permission to the Business Data Connectivity (BDC) metadata store and that appropriate users have access to the external content type on which the external list is based.</span></span>
  
    
    
 <span data-ttu-id="9fb4e-p104">**Убедиться, что Office 2013 готов к использованию.** Чтобы синхронизировать внешние данные с продуктами Office 2013, вы должны использовать Windows 7 или более поздние версии и убедиться, что параметр установки Office для Службы Business Connectivity Services (BCS) включен (по умолчанию). Этот параметр устанавливает Среда выполнения клиента Business Connectivity Services, который выполняет следующие действия: кэширует и синхронизирует внешние данные, сопоставляет бизнес-данные с внешними типами контента, отображает средство выбора внешних элементов в продуктах Office и запускает пользовательские решения внутри продуктов Office. Кроме того, на каждом клиентском компьютере должны быть установлены SQL Server Compact 4.0, .NET Framework 4 и службы данных WCF 5.0 для OData V3 (при необходимости вам автоматически будет предложено скачать программное обеспечение).</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p104">**Be sure Office 2013 is ready to use** To synchronize external data with Office 2013 products, you must use Windows 7 or a later version, and make sure that the Office installation option for Business Connectivity Services (BCS) is enabled (this is the default). This option installs the Business Connectivity Services Client Runtime which does the following: caches and synchronizes with external data, maps business data to external content types, displays the external item picker in Office products, and runs custom solutions inside Office products. You must also have SQL Server Compact 4.0, .NET Framework 4, and WCF Data Services 5.0 for OData V3 on each client computer (If necessary, you are automatically prompted to download the software).</span></span>
  
    
    

## <a name="define-general-information"></a><span data-ttu-id="9fb4e-121">Определение общих сведений</span><span class="sxs-lookup"><span data-stu-id="9fb4e-121">Define general information</span></span>
<span data-ttu-id="9fb4e-122"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-122"><a name="section2"> </a></span></span>


1. <span data-ttu-id="9fb4e-123">Запустите Microsoft SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-123">Start Microsoft SharePoint Designer 2013.</span></span>
    
  
2. <span data-ttu-id="9fb4e-124">Щелкните кнопку **Открыть сайт** и затем введите соответствующее имя сайта.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-124">Click **Open Site**, and then enter the appropriate site name.</span></span>
    
  
3. <span data-ttu-id="9fb4e-125">В области **Навигация** выберите в разделе **Объекты сайта** элемент **Внешние типы контента**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-125">In the **Navigation** pane, under **Site Objects**, select **External Content Types**.</span></span>
    
    > <span data-ttu-id="9fb4e-126">**Примечание.** SharePoint Designer 2013 группирует внешние типы контента по пространству имен в начальном окне конструктора внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-126">**Note:** SharePoint Designer 2013 groups external content types by the namespace in the initial window of the External Content Type Designer.</span></span> 
4. <span data-ttu-id="9fb4e-127">Чтобы открыть конструктор внешних типов контента, выберите на ленте **Внешний тип контента**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-127">To open the External Content Type Designer, on the ribbon, click **External Content Type**.</span></span>
    
  
5. <span data-ttu-id="9fb4e-128">На странице **Новый внешний тип контента** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-128">On the **New External Content Type** page, do the following:</span></span>
    
  - <span data-ttu-id="9fb4e-129">Радом с пунктом **Имя** щелкните пункт **Новый внешний тип контента**, а затем введите уникальное имя для этого внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-129">Next to **Name**, click **New external content type**, and then enter a unique name for the external content type.</span></span>
    
  
  - <span data-ttu-id="9fb4e-130">Рядом с пунктом **Отображаемое имя** можете указать другое, более понятное имя.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-130">Next to **Display Name**, enter a different name if you want a more descriptive display name.</span></span>
    
  

## <a name="define-general-and-office-behaviors"></a><span data-ttu-id="9fb4e-131">Определение общих параметров и параметров Office</span><span class="sxs-lookup"><span data-stu-id="9fb4e-131">Define general and Office behaviors</span></span>
<span data-ttu-id="9fb4e-132"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-132"><a name="section3"> </a></span></span>


1. <span data-ttu-id="9fb4e-133">В выпадающем списке **Тип элемента Microsoft Office** один из следующих типов:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-133">In the **Office Item Type** drop-down list, select one of the following:</span></span>
    
  - <span data-ttu-id="9fb4e-134">**Универсальный список**. Выберите этот параметр для любого типа списка.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-134">**Generic List** Select this option for any type of list.</span></span>
    
  
  - <span data-ttu-id="9fb4e-p105">**Встреча, контакт, публикация или задача**. Выберите этот параметр, если вы создаете список, который ведет себя как элемент контакта, задачи, встречи или публикации для Outlook. Выбранный вами тип элемента Office определяет поведение Outlook, которое вы хотите прикрепить к внешнему типу контента. Например, внешний тип контента "Клиент" ведет себя так же, как собственный элемент "Контакт" в Outlook.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p105">**Appointment, Contact, Task, or Post** Select this option if you are creating a list that behaves like an Outlook Contact, Task, Appointment, or Post item. The Office item type that you select here determines the Outlook behavior that you want to attach to the external content type. For example, a Customer external content type behaves as a native Contact Item in Outlook.</span></span>
    
  
2. <span data-ttu-id="9fb4e-138">Убедитесь, что для параметра **Автономная синхронизация для внешнего списка** выбрано значение **Включено**, заданное по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-138">In the **Offline Sync for External List** check box, make sure **Enabled** is selected, which is the default.</span></span>
    
    > <span data-ttu-id="9fb4e-139">**Примечание.** Если отключить этот параметр, команда SharePoint **Подключиться к Outlook** будет недоступна для внешнего списка.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-139">**Note:** If you disable this option, then the **SharePoint Connect to Outlook** command is not available for an external list.</span></span>

> <span data-ttu-id="9fb4e-140">**Примечание.** Функция ферм и сайтов **Автономная синхронизация для внешних списков** также должна быть активна.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-140">**Note:** The Farm and Site feature, **Offline Synchronization for External Lists**, must also be active.</span></span> <span data-ttu-id="9fb4e-141">По умолчанию эта функция включена на уровне фермы, но отключена на уровне сайта.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-141">This feature is active by default at the Farm level, but not active by default at the site level.</span></span> 
  
    
    


## <a name="create-a-connection-to-the-external-data"></a><span data-ttu-id="9fb4e-142">Создание подключения к внешним данным</span><span class="sxs-lookup"><span data-stu-id="9fb4e-142">Create a connection to the external data</span></span>
<span data-ttu-id="9fb4e-143"><a name="section4"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-143"><a name="section4"> </a></span></span>


1. <span data-ttu-id="9fb4e-144">Чтобы указать базу данных SQL Server для внешнего типа контента, нажмите пункт **Щелкните здесь для обнаружения внешних источников данных и определения операций**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-144">To specify the SQL Server database for the external content type, click **Click here to discover external data sources and define operations**.</span></span>
    
  
2. <span data-ttu-id="9fb4e-145">Щелкните **Добавить подключение**, выберите пункт **SQL Server** в диалоговом окне **Выбор типа внешнего источника данных**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-145">Click **Add Connection**, select **SQL Server** in **the External Data Source Type Selection** dialog box, and then click **OK**.</span></span>
    
  
3. <span data-ttu-id="9fb4e-146">В диалоговом окне **Подключение к серверу SQL Server** введите имя сервера, имя базы данных, описание (необязательно) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-146">In the **SQL Server Connection** dialog box, enter the name of the server, the database name, an optional description, and then click **OK**.</span></span>
    
  
4. <span data-ttu-id="9fb4e-147">Чтобы выбрать режим проверки подлинности, укажите один из следующих пунктов:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-147">To choose an authentication mode, select one of the following:</span></span>
    
  - <span data-ttu-id="9fb4e-148">**Подключиться с удостоверением пользователя**. Используется режим сквозной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-148">**Connect with User's Identity** Uses the Pass-through authentication mode.</span></span>
    
  
  - <span data-ttu-id="9fb4e-149">**Подключиться с олицетворенным удостоверением Windows**. Используется режим проверки подлинности учетных данных Windows.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-149">**Connect with Impersonated Windows Identity** Uses the WindowsCredentials authentication mode.</span></span>
    
  
  - <span data-ttu-id="9fb4e-150">**Подключиться с олицетворенным настраиваемым удостоверением**. Используется режим проверки подлинности учетных данных RDB.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-150">**Connect with Impersonated Custom Identity** Uses the RDBCredentials authentication mode.</span></span>
    
  
5. <span data-ttu-id="9fb4e-151">В поле **Идентификатор приложения Secure Store** введите имя идентификатора конечного приложения, созданного в Служба Secure Store.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-151">In the **Secure Store Application ID** box, enter the target application ID name created in the Secure Store Service.</span></span>
    
  
6. <span data-ttu-id="9fb4e-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-152">Click **OK**.</span></span>
    
  
<span data-ttu-id="9fb4e-p107">SharePoint Designer 2013 проверяет и тестирует сведения о подключении. Если появятся сообщения, то для продолжения вам необходимо будет их устранить.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p107">SharePoint Designer 2013 validates and tests the connection information. If you see messages, you must resolve them before you continue.</span></span>
  
    
    

## <a name="select-a-table-view-or-routine"></a><span data-ttu-id="9fb4e-155">Выбор таблицы, представления или процедуры</span><span class="sxs-lookup"><span data-stu-id="9fb4e-155">Select a table, view, or routine</span></span>
<span data-ttu-id="9fb4e-156"><a name="section5"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-156"><a name="section5"> </a></span></span>


1. <span data-ttu-id="9fb4e-157">В проводнике источника данных разверните узел базы данных, чтобы просмотреть содержащиеся там таблицы, представления и процедуры.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-157">In the Data Source Explorer, expand the database to view the tables, views, and routines that it contains.</span></span>
    
  
2. <span data-ttu-id="9fb4e-158">Выберите таблицу, представление или процедуру.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-158">Select a table, view, or routine.</span></span>
    
  

## <a name="define-operations"></a><span data-ttu-id="9fb4e-159">Определение операций</span><span class="sxs-lookup"><span data-stu-id="9fb4e-159">Define operations</span></span>
<span data-ttu-id="9fb4e-160"><a name="section6"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-160"><a name="section6"> </a></span></span>


1. <span data-ttu-id="9fb4e-161">В проводнике источника данных щелкните правой кнопкой мыши таблицу, представление или процедуру, а затем выберите одну из следующих команд:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-161">In the Data Source Explorer, right-click the table, view, or routine, and then select one of the following:</span></span>
    
  - <span data-ttu-id="9fb4e-162">**Создать все операции**. Определяет операции создания, удаления и чтения элемента, чтения списка и обновления элемента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-162">**Create All Operations** Defines a create item, delete item, read item, read list, and update item operation.</span></span>
    
    > <span data-ttu-id="9fb4e-163">**Примечание.**
      > Команда **Создать все операции** доступна только для таблиц и представлений.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-163">**Note:**
**Create All Operations** is available only for tables and views.</span></span> <span data-ttu-id="9fb4e-164">Процедурам необходимы определенные операции.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-164">Routines require specific operations.</span></span>
  - <span data-ttu-id="9fb4e-165">**Новая операция чтения элемента**. Определяет операцию чтения элемента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-165">**New Read Item Operation** Defines a read item operation.</span></span>
    
  
  - <span data-ttu-id="9fb4e-166">**Новая операция чтения списка**. Определяет операцию чтения списка.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-166">**New Read List Operation** Defines a read list operation.</span></span>
    
  
  - <span data-ttu-id="9fb4e-167">**Новая операция обновления**. Определяет операцию обновления элемента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-167">**New Update Operation** Defines an update item operation.</span></span>
    
  
  - <span data-ttu-id="9fb4e-168">**Новая операция удаления прочитанного**. Определяет операцию удаления элемента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-168">**New Delete Read** Defines a delete item operation.</span></span>
    
  
  - <span data-ttu-id="9fb4e-169">**Обновить**. Обновляет список таблиц, представление и процедур в проводнике источника данных.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-169">**Refresh** Refreshes the list of tables, views, and routines in the Data Source Explorer.</span></span>
    
  
2. <span data-ttu-id="9fb4e-170">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-170">Click **Next**.</span></span>
    
  
 <span data-ttu-id="9fb4e-171">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-171">**Notes**</span></span>
  
    
    

- <span data-ttu-id="9fb4e-p109">В представлениях, которые охватывают несколько таблиц, убедитесь, что поддерживаются операции записи. В противном случае в командах **Создать все операции** или **Новая операция обновления** может произойти сбой.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p109">On views that span multiple tables, make sure that that write operations are supported. Otherwise, **Create All Operations** or **New Update Operation** might fail.</span></span>
    
  
- <span data-ttu-id="9fb4e-174">Всегда определяйте как минимум команды **Новая операция чтения элемента** и **Новая операция чтения списка**, так как функции SharePoint, например внешние списки, зависят от них.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-174">Always define at least a **New Read Item Operation** and **New Read List Operation** because SharePoint features, such as external lists, rely on these operations.</span></span>
    
  
- <span data-ttu-id="9fb4e-175">Если таблица или представление не поддерживают некоторые операции, выберите конкретные операции вместо команды **Создать все операции**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-175">Choose specific operations, instead of **Create All Operations**, when the table or view does not support certain operations.</span></span>
    
  

## <a name="add-columns"></a><span data-ttu-id="9fb4e-176">Добавление столбцов</span><span class="sxs-lookup"><span data-stu-id="9fb4e-176">Add columns</span></span>
<span data-ttu-id="9fb4e-177"><a name="section7"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-177"><a name="section7"> </a></span></span>


1. <span data-ttu-id="9fb4e-178">Чтобы указать столбцы, которые нужно отобразить из таблицы или представления, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-178">To specify the columns that you want to display from the table or view, click **Next**.</span></span>
    
  
2. <span data-ttu-id="9fb4e-p110">В диалоговом окне **Параметры конфигурации** по умолчанию выбраны все столбцы (известные как **Элементы источника данных**). Чтобы удалить ненужные столбцы, снимите соответствующие флажки.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p110">In the **Parameters Configuration** dialog box, by default all columns (known as **Data Source Elements**) are selected. To remove unnecessary columns, clear the corresponding check boxes.</span></span>
    
    > <span data-ttu-id="9fb4e-181">**Примечание.** В отличие от встроенного списка SharePoint, во внешнем списке невозможно изменить имя столбца.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-181">**Note:** Unlike a native SharePoint list, you cannot change the column name of an external list.</span></span> <span data-ttu-id="9fb4e-182">Вы можете использовать псевдоним столбца SQL, чтобы указать более понятное или краткое имя.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-182">Consider using an SQL column alias to provide a more meaningful name or a shorter name.</span></span> 
3. <span data-ttu-id="9fb4e-183">Чтобы выбрать поле идентификатора, нажмите и выделите поле (как правило, с уникальным значением), а затем в разделе **Свойства** нажмите **Сопоставить с идентификатором**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-183">To select an identifier field, click and highlight a field (typically a unique-valued field), and then under **Properties**, click **Map to Identifier**.</span></span>
    
  

> <span data-ttu-id="9fb4e-184">**Важно!** Чтобы предотвратить обновление определенных полей, например поля идентификатора или первичного ключа, снимите флажок **Обязательно**, но установите флажок **Только для чтения**. Это необходимо для извлечения элементов, чтобы вы могли обновлять другие поля.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-184">**Important:** To prevent specific fields from being updated, such as an ID or primary key field, clear the **Required** check box, but select the **Read-Only** check box, which is needed to retrieve items so you can update other fields.</span></span>
  
    
    

  
    
    


> <span data-ttu-id="9fb4e-185">**Совет.** Всегда внимательно читайте сообщения в области **Ошибки и предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-185">**Tip:** Always carefully read the messages in the **Errors and Warnings** pane.</span></span> <span data-ttu-id="9fb4e-186">Они содержат полезные сведения о выполняемых действиях и возможных проблемах.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-186">They provide useful information to confirm your actions or troubleshoot any issues.</span></span> <span data-ttu-id="9fb4e-187">Периодически открывайте область **Ошибки и предупреждения**, чтобы убедиться, что ошибок и предупреждений больше нет.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-187">Periodically click the **Errors and Warnings** pane and make sure that there are no more errors or warnings.</span></span>
  
    
    


## <a name="map-outlook-fields"></a><span data-ttu-id="9fb4e-188">Сопоставление полей Outlook</span><span class="sxs-lookup"><span data-stu-id="9fb4e-188">Map Outlook fields</span></span>
<span data-ttu-id="9fb4e-189"><a name="section8"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-189"><a name="section8"> </a></span></span>

<span data-ttu-id="9fb4e-p113">Если ваш внешний тип контента соответствует типу элемента Outlook, вы должны сопоставить одно или несколько полей из своего внешнего типа контента с полями элемента Outlook. При сопоставлении внешнего типа контента, например "Клиент", с типом элемента Outlook, например "Контакт", вы должны явно сопоставить отдельные поля из внешнего типа контента, например, "Фамилия клиента", "Имя клиента", "Адрес клиента" и "Телефон клиента" с соответствующими им полями элемента Outlook, например, "Имя", "Фамилия", "Рабочий адрес" и "Рабочий телефон" контакта.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p113">If your external content type maps to an Outlook item type, you must map one or more fields from your external content type to the Outlook item fields. When you map an external content type, such as a Customer, to an Outlook item type, such as a Contact, you must explicitly map the individual fields in the external content type, such as Customer First Name, Customer Last Name, Customer Address, and Customer Phone, to their respective Outlook item type fields, such as a contact's FirstName, LastName, BusinessAddress, and BusinessPhone.</span></span>
  
    
    

- <span data-ttu-id="9fb4e-192">Для каждого поля выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-192">For the each field, do the following:</span></span>
    
1. <span data-ttu-id="9fb4e-193">Щелкните в поле, чтобы выделить его.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-193">Click and highlight the field.</span></span>
    
  
2. <span data-ttu-id="9fb4e-p114">В разделе **Свойства** нажмите стрелку вниз рядом с элементом **Свойство Office**, а затем выберите соответствующее поле.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p114">Under **Properties**, next to **Office property**, click the down arrow. and then select the appropriate matching field.</span></span> 
    
  

> <span data-ttu-id="9fb4e-196">**Примечание.** Сопоставлять все соответствующие поля необязательно.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-196">**Note:** You do not need to map all the corresponding fields.</span></span> <span data-ttu-id="9fb4e-197">Однако поля, представленные в приведенной ниже таблице, должны быть сопоставлены.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-197">However, the fields shown in the following table must be mapped.</span></span> 
  
    
    


<span data-ttu-id="9fb4e-198">**Таблица. Тип элемента Outlook, сопоставленный с полем элемента Outlook**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-198">**Table: Outlook item type mapped to Outlook item field**</span></span>


|<span data-ttu-id="9fb4e-199">**Тип элемента Outlook**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-199">**Outlook item type**</span></span>|<span data-ttu-id="9fb4e-200">**Поле элемента Outlook**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-200">**Outlook item field**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9fb4e-201">Контакт</span><span class="sxs-lookup"><span data-stu-id="9fb4e-201">Contact</span></span>  <br/> |<span data-ttu-id="9fb4e-202">LastName</span><span class="sxs-lookup"><span data-stu-id="9fb4e-202">LastName</span></span>  <br/> |
|<span data-ttu-id="9fb4e-203">Задача</span><span class="sxs-lookup"><span data-stu-id="9fb4e-203">Task</span></span>  <br/> |<span data-ttu-id="9fb4e-204">Subject</span><span class="sxs-lookup"><span data-stu-id="9fb4e-204">Subject</span></span>  <br/> |
|<span data-ttu-id="9fb4e-205">Appointment</span><span class="sxs-lookup"><span data-stu-id="9fb4e-205">Appointment</span></span>  <br/> |<span data-ttu-id="9fb4e-206">Начало, окончание и тема</span><span class="sxs-lookup"><span data-stu-id="9fb4e-206">Start, End, and Subject</span></span>  <br/> |
|<span data-ttu-id="9fb4e-207">Запись</span><span class="sxs-lookup"><span data-stu-id="9fb4e-207">Post</span></span>  <br/> |<span data-ttu-id="9fb4e-208">Subject</span><span class="sxs-lookup"><span data-stu-id="9fb4e-208">Subject</span></span>  <br/> |
   
<span data-ttu-id="9fb4e-209">Несопоставленные поля в зависимости от номера отображаются в виде расширенных свойств следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-209">Unmapped fields, depending on the number, are displayed as extended properties as follows:</span></span>
  
    
    

- <span data-ttu-id="9fb4e-210">**Смежное**. Прилагается к области формы в нижней части страницы по умолчанию для формы Outlook (от двух до пяти полей).</span><span class="sxs-lookup"><span data-stu-id="9fb4e-210">**Adjoining** Appended to the form region at the bottom of an Outlook form's default page (two to five fields).</span></span>
    
  
- <span data-ttu-id="9fb4e-211">**Отдельное**. Добавляется на форму Outlook в качестве новой страницы (от двух до пяти полей).</span><span class="sxs-lookup"><span data-stu-id="9fb4e-211">**Separate** Added as a new page to an Outlook form (six or more fields).</span></span>
    
  

## <a name="set-up-the-external-item-picker-control"></a><span data-ttu-id="9fb4e-212">Настройка элемента управления выбора внешних элементов</span><span class="sxs-lookup"><span data-stu-id="9fb4e-212">Set up the external item picker control</span></span>
<span data-ttu-id="9fb4e-213"><a name="section9"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-213"><a name="section9"> </a></span></span>

<span data-ttu-id="9fb4e-p116">Средство управления выбора внешних элементов позволяет пользователям выбирать поля, например поле идентификатора или поле, содержащее уникальные значения, для удобного выбора элемента. Это средство управления доступно в SharePoint и продуктах Office 2013. Например, пользователи могут использовать его, чтобы выбрать элемент из внешнего списка клиентов, а Word 2013 позволяет использовать это средство управления с элементами управления контентом, которые связаны со столбцами внешних данных. Это хороший способ выбрать определенные столбцы, которые вы хотите отобразить в средстве управления выбора внешнего элемента, так как операция для показа всех столбцов, которая используется по умолчанию, в большинстве случаев не требуется.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p116">The external item picker control allows users to select a field, such as an ID field or a field that has unique values, to conveniently choose an item. This control is available in SharePoint and Office 2013 products. For example, users can use this control to choose an item from an external list of customers and Word 2013 enables this control for use with content controls that are linked to external data columns.It's a good idea to select the specific columns you want to display in the external item picker control because the default operation is to show all the columns, which in most cases, is not necessary.</span></span>
  
    
    

1. <span data-ttu-id="9fb4e-217">Для каждого поля, которое вы хотите отобразить в средстве выбора внешнего элемента контента, щелкните и выделите поле, а затем в разделе **Свойства** поставьте флажок напротив пункта **Показать в средстве выбора**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-217">For each field that you want displayed in the external content item picker, click and highlight the field, and then under **Properties**, click the **Show in Picker** check box.</span></span>
    
  
2. <span data-ttu-id="9fb4e-218">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-218">Click **Next**.</span></span>
    
  

> <span data-ttu-id="9fb4e-219">**Примечание.** Все определенные вами фильтры отображаются в средстве выбора внешних элементов.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-219">**Note:** All filters that you define are displayed in the external item picker control.</span></span> <span data-ttu-id="9fb4e-220">Из средства выбора внешних элементов невозможно удалять определенные фильтры, но вы можете определить фильтр по умолчанию, выбрав параметр **Используется по умолчанию** в диалоговом окне **Конфигурация фильтра** при создании или изменении фильтра.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-220">Although you cannot remove specific filters from the external item picker control, you can define a default filter by clicking **Is Default** in the **Filter configuration** dialog box when you are creating or modifying the filter.</span></span>
  
    
    


## <a name="define-filters"></a><span data-ttu-id="9fb4e-221">Определение фильтров</span><span class="sxs-lookup"><span data-stu-id="9fb4e-221">Define filters</span></span>
<span data-ttu-id="9fb4e-222"><a name="section10"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-222"><a name="section10"> </a></span></span>

<span data-ttu-id="9fb4e-p118">Если вы не определили фильтр, внешний список возвратит все данные до предела регулирования Службы Business Connectivity Services (BCS) (по умолчанию это 2000 элементов) или все данные, которые определены в типе внешнего контента, если их количество меньше текущего значения предела регулирования. Кроме того, вся обработка результатов происходит в продукте SharePoint. Рекомендуется определить хотя бы один фильтр. В целом существует два типа фильтров, которые необходимо знать:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p118">If you do not define a filter, an external list returns all of the data up to the Business Connectivity Services (BCS) throttle limit (by default, 2,000 items) or all the data that is defined in the external content type, if less than the current throttle limit. In addition, the entire processing of the results occurs within the SharePoint product. It's a good idea to define at least one filter. In general, there are two types of filters that you need to be aware:</span></span>
  
    
    

- <span data-ttu-id="9fb4e-p119">**Фильтр источника данных**. Когда вы создаете фильтр типов внешнего контента, известный как фильтр источника данных, операция фильтрации происходит в пределах базы данных SQL Server. Это важно, когда вы работаете с большим количеством данных, так как вы можете разгрузить обработку из продуктов SharePoint во внешнюю базу данных и повысить производительность. После создания внешнего списка вы можете использовать фильтр источника данных, создав представление, которое определяет различные значения фильтров в разделе **Фильтр источника данных** на странице настроек **Представление списка**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p119">**Data Source Filter** When you create an external content type filter, which is known as a Data Source Filter, the filter operation occurs within the SQL Server database. This is important when you are working with lots of data because you can offload processing from SharePoint products to the external database and gain performance improvements. After you create the external list, you can use the Data Source Filter by creating a view that specifies different filter values in the **Data Source Filter** section of the **List View** settings page.</span></span>
    
  
- <span data-ttu-id="9fb4e-p120">**Фильтр SharePoint**. Пользователи по-прежнему могут фильтровать данные с помощью фильтра SharePoint, либо фильтром заголовков столбца, либо с помощью раздела **Фильтры** на странице настроек **Представление списка**. В этом случае операция фильтрации проходит в пределах продукта SharePoint, а не базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p120">**SharePoint filter** Users can still filter the data by using a SharePoint filter, either the column header filter or by using the **Filters** section in the **List View** settings page. In this case, the filter operation occurs within the SharePoint product, not within the SQL Server database.</span></span>
    
  
<span data-ttu-id="9fb4e-232">Хорошая стратегия  создать набор представлений внешних списков, основанных на определенных фильтрах источников данных, который гарантирует, что большие объемы данных сначала будут отфильтрованы во внешнем источнике данных, а затем пользователи смогут отфильтровать и уточнить результаты с помощью фильтров SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-232">A good strategy to consider is to create a set of external list views based on specific Data Source Filters that make sure that larger amounts of data are filtered first in the external data source, and then users can further filter and refine the results by using SharePoint filters.</span></span>
  
    
    
<span data-ttu-id="9fb4e-p121">Вы можете создать несколько различных типов фильтров. Для каждого создаваемого фильтра необходимо выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p121">You can create several different types of filters. For each filter that you create, do the following:</span></span>
  
    
    

1. <span data-ttu-id="9fb4e-235">Выберите поле в разделе **Свойства** рядом с пунктом **Элемент источника данных**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-235">Under **Properties**, next to **Data Source Element**, select a field.</span></span>
    
  
2. <span data-ttu-id="9fb4e-236">В разделе **Свойства** рядом с пунктом **Фильтр** нажмите ссылку **Щелкните, чтобы добавить**, чтобы открыть диалоговое окно **Конфигурация фильтра**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-236">Under **Properties**, next to **Filter**, click **Click to Add** to display the **Filter Configuration** dialog box.</span></span>
    
  
3. <span data-ttu-id="9fb4e-237">Щелкните **Добавить параметр фильтра**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-237">Click **Add Filter Parameter**.</span></span>
    
  
4. <span data-ttu-id="9fb4e-238">В поле **Создать фильтр** введите имя фильтра.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-238">In the **New Filter** box, enter a filter name.</span></span>
    
  
5. <span data-ttu-id="9fb4e-239">В поле **Тип фильтра** выберите тип фильтра:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-239">In the **Filter Type** box, select a filter type:</span></span>
    
    
  
    
    
 <span data-ttu-id="9fb4e-240">**Сравнения**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-240">**Comparisons**</span></span>
  
    
    

    
    <span data-ttu-id="9fb4e-241">Фильтр сравнения ограничивает элементы, которые возвращаются в зависимости от условия (например, Штат = "Нью-Джерси"), и преобразуется в SQL-предложение WHERE.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-241">A Comparison filter limits what items are returned based on a condition (such as State = "New Jersey") and is converted to an SQL WHERE clause.</span></span>
    
1. <span data-ttu-id="9fb4e-242">В поле **Тип фильтра** выберите пункт **Сравнение**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-242">In the **Filter Type** box, select **Comparison**.</span></span>
    
  
2. <span data-ttu-id="9fb4e-243">В поле **Оператор** выберите операцию.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-243">In the **Operator** box, select an operation.</span></span>
    
  
3. <span data-ttu-id="9fb4e-244">Убедитесь, что в поле **Поле фильтра** выбрано необходимое для сравнения.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-244">In the **Filter Field** box, make sure that the field that you want to compare is selected.</span></span>
    
  
4. <span data-ttu-id="9fb4e-245">Если вводимые пользователем значения должны совпадать по регистру, выберите параметр **Учитывать регистр**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-245">If you want values entered by the user to match by case, click **Case Sensitive**.</span></span>
    
  
5. <span data-ttu-id="9fb4e-246">Если при наличии нескольких совпадающих элементов в средстве выбора внешних элементов должен отображаться список возможных совпадений, установите флажок **Использовать для создания списка соответствий в средстве выбора внешних элементов**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-246">If you want to display a list of possible matches ??n the external item picker control when there is more than one matching item, select **Use to create match list in external item picker**.</span></span>
    
  
6. <span data-ttu-id="9fb4e-247">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-247">Click **OK**.</span></span>
    
  
7.  <span data-ttu-id="9fb4e-p122">В разделе **Свойства** рядом с полем **Значение по умолчанию** введите начальное значение, по которому будет производиться фильтрация в случае, если пользователь не введет значение. Если вы оставите это поле пустым, внешний список не отобразит никаких элементов.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p122">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span>
    
  

    
  
    
    
 <span data-ttu-id="9fb4e-250">**Подстановочные знаки**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-250">**Wildcards**</span></span>
  
    
    

    
    <span data-ttu-id="9fb4e-251">Фильтр с подстановочными знаками ограничивает набор возвращаемых элементов в соответствии со строковым значением, которое указал пользователь (например, поле "Состояние" должно содержать значение "Новый"), и преобразуется в предложение SQL LIKE.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-251">A Wildcard filter limits what items are returned based on a user-entered string value (such as State Contains "New") and is converted to an SQL LIKE clause.</span></span> <span data-ttu-id="9fb4e-252">Допустимые подстановочные знаки SQL Server: \* (звездочка) для сопоставления любого количества символов и \_ (подчеркивание) для сопоставления только одного символа.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-252">Valid SQL Server wildcard characters are \* (asterisk) which means match any number of characters and \_ (underscore) which means match one and only one character.</span></span> 
  
    
    

    
1. <span data-ttu-id="9fb4e-253">В поле **Тип фильтра** выберите пункт **С подстановочными знаками**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-253">In the **Filter Type** box, select **Wildcard**.</span></span>
    
  
2. <span data-ttu-id="9fb4e-254">В поле **Поле фильтра** выберите нужное.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-254">In the **Filter Field** box, select a field.</span></span>
    
  
3. <span data-ttu-id="9fb4e-255">Если вводимые пользователем значения должны совпадать по регистру, выберите параметр **Учитывать регистр**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-255">If you want values entered by the user to match by case, click **Case Sensitive**.</span></span>
    
  
4. <span data-ttu-id="9fb4e-256">Если при наличии нескольких совпадающих элементов в средстве выбора внешних элементов должен отображаться список возможных совпадений, установите флажок **Использовать для создания списка соответствий в средстве выбора внешних элементов**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-256">If you want to display a list of possible matches ??n the external item picker control when there is more than one matching item, select **Use to create match list in external item picker**.</span></span>
    
  
5. <span data-ttu-id="9fb4e-257">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-257">Click **OK**.</span></span>
    
  
6.  <span data-ttu-id="9fb4e-258">В разделе **Свойства** укажите для параметра **Значение по умолчанию** исходное значение, по которому следует фильтровать результаты, если пользователь не укажет значение.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-258">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value.</span></span> <span data-ttu-id="9fb4e-259">Если это значение не указано, во внешнем списке не будут отображаться элементы.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-259">If you do not enter a value, the external list does not display any items.</span></span> <span data-ttu-id="9fb4e-260">Рекомендуем использовать по умолчанию символ \* (звездочку).</span><span class="sxs-lookup"><span data-stu-id="9fb4e-260">It's a good idea to enter an \* (asterisk) as the default.</span></span>
    
  

    
  
    
    
 <span data-ttu-id="9fb4e-261">**Ограничение**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-261">**Limit**</span></span>
  
    
    

    
    <span data-ttu-id="9fb4e-p125">В большинстве случаев вы можете определить ограничивающий фильтр для операций чтения и чтения списка. Если вы не определите значение **Ограничения по умолчанию**, никакие данные не будут извлечены из внешнего источника данных. Убедитесь, что введенное вами значение по умолчанию для ограничивающего фильтра меньше 2000, так как регулирование Службы Business Connectivity Services (BCS) по умолчанию равно 2000 элементов. При необходимости вы можете увеличить данное значение.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p125">In most cases, you must define a Limit Filter for Read and Read List operations. If you do not define a **Default Limit** value, no data is retrieved from the external data source. Ensure that the default value that you enter for the limit filter is less than 2,000, because the default Business Connectivity Services (BCS) throttle is 2,000 items. You can increase this limit if it is necessary.</span></span>
    
1. <span data-ttu-id="9fb4e-266">В поле **Тип фильтра** выберите пункт **Ограничение**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-266">In the **Filter Type** box, select **Limit**.</span></span> 
    
  
2. <span data-ttu-id="9fb4e-267">В поле **Число** укажите число.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-267">In the **Number** box, enter a number.</span></span>
    
  
3. <span data-ttu-id="9fb4e-268">Если при наличии нескольких совпадающих элементов в средстве выбора внешних элементов должен отображаться список возможных совпадений, установите флажок **Использовать для создания списка соответствий в средстве выбора внешних элементов**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-268">If you want to display a list of possible matches ??n the external item picker control when there is more than one matching item, select **Use to create match list in external item picker**.</span></span>
    
  
4. <span data-ttu-id="9fb4e-p126">В разделе **Свойства** рядом с полем **Значение по умолчанию** введите начальное значение, по которому будет производиться фильтрация в случае, если пользователь не введет значение. Если вы оставите это поле пустым, внешний список не отобразит никаких элементов.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p126">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span>
    
  
5. <span data-ttu-id="9fb4e-271">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-271">Click **OK**.</span></span> 
  
    
    

    
  

    > <span data-ttu-id="9fb4e-272">**Примечание.** Администратор базы данных SQL Server может создать специальные таблицы, представления, индексы и оптимизированные запросы, чтобы ограничить результаты до лишь необходимых данных и повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-272">**Note:** The SQL Server database administrator might want to create specific tables, views, indexes, and optimized queries to limit the results to just what is needed and to help improve performance.</span></span> 

    
  
    
    
 <span data-ttu-id="9fb4e-273">**Номер страницы**</span><span class="sxs-lookup"><span data-stu-id="9fb4e-273">**Page Number**</span></span>
  
    
    

    
    <span data-ttu-id="9fb4e-p127">Используйте внешний тип контента "Номер страницы", чтобы заменить ограничение страниц SharePoint, определенных на странице **Представление списка** внешнего списка. Вот отличия:</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p127">Use the external content type Page Number to supersede the SharePoint page limit defined in the **List View** page of the external list. Here's the difference:</span></span>
    
  - <span data-ttu-id="9fb4e-276">Внешний тип контента "Номер страницы" сначала обрабатывает результаты в пределах базы данных SQL Server, а затем возвращает и отображает только то количество строк, которое определено значением "Размер страницы".</span><span class="sxs-lookup"><span data-stu-id="9fb4e-276">The external content type Page Number first processes the results within the SQL Server database, and then returns and displays only the number of rows determined by the Page Size value.</span></span>
    
  
  - <span data-ttu-id="9fb4e-277">Ограничение страниц SharePoint возвращает все строки в "Значение по умолчанию" из базы данных SQL Server, а затем отображает количество строк, определенное значением ограничения страниц SharePoint на странице настроек **Представление списка**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-277">The SharePoint page limit returns all the rows up to the Default Value size from the SQL Server database, and then displays the number of rows determined by the SharePoint page limit value in the **List View** settings page.</span></span>
    
  

    <span data-ttu-id="9fb4e-p128">Использование внешнего типа контента "Номер страницы" в целом более эффективно. Кроме того, значение **Порядок** помогает убедиться, что возвращено точное отображение результатов.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p128">Using the external content type Page Number is generally more efficient. In addition, the **Order** value helps make sure that an accurate display of the results returned.</span></span>
    
1. <span data-ttu-id="9fb4e-280">В поле **Тип фильтра** выберите пункт **Номер страницы**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-280">In the **Filter Type** box, select **Page Number**.</span></span> 
    
  
2. <span data-ttu-id="9fb4e-281">В поле **Размер страницы** введите число.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-281">In the **Page Size** box, enter a number.</span></span>
    
  
3. <span data-ttu-id="9fb4e-282">В поле **Порядок** выберите направление сортировки.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-282">In the **Order** box, select a sort direction.</span></span>
    
  
4. <span data-ttu-id="9fb4e-283">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-283">Click **OK**.</span></span> 
    
  
5. <span data-ttu-id="9fb4e-p129">В разделе **Свойства** рядом с полем **Значение по умолчанию** введите начальное значение, по которому будет производиться фильтрация в случае, если пользователь не введет значение. Если вы оставите это поле пустым, внешний список не отобразит никаких элементов.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p129">Under **Properties**, next to **Default Value**, enter the initial value that you want to filter by, if the user does not enter a value. If you do not enter a value, the external list does not display any items.</span></span> 
  
    
    

    
  
6. <span data-ttu-id="9fb4e-286">Если вы хотите отобразить поле, но не изменять его, щелкните и выделите это поле, а затем в разделе **Свойства** установите флажок **Только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-286">If you want to display but not modify a field, click and highlight the field, and then under **Properties**, select **Read-Only**.</span></span>
    
  
7. <span data-ttu-id="9fb4e-287">Если вы хотите убедиться, что поле всегда имеет значение созданного при его создании или изменении, щелкните и выделите это поле, а затем в разделе **Свойства** установите флажок **Обязательно**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-287">If you want to make sure that a field always has a value when it's created or modified, click and highlight the field, and then under **Properties**, select **Required**.</span></span>
    
  
8. <span data-ttu-id="9fb4e-288">Чтобы предоставить описательное имя в средстве управления выбором внешнего элемента для имени **Элемента источника данных**, которое является производным от имени столбца SQL Server, щелкните и выделите поле, а затем введите имя в разделе **Свойства** в поле **Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-288">To provide a descriptive name in the external item picker control of the **Data Source Element** name, which is derived from the SQL Server column name, click and highlight the field, and then under **Properties**, in the **Display Name** box, enter a name.</span></span>
    
  
9. <span data-ttu-id="9fb4e-p130">Чтобы определить значение по умолчанию для фильтра (которое также отображается в разделе **Фильтр источника данных** на странице настроек **Представление списка**), в разделе **Параметры фильтра** щелкните и выделите фильтр, а затем введите соответствующее значение в поле **Значение по умолчанию**. Если вы не введете значение, то при первом использовании фильтра не будут отображены никакие элементы.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p130">To define a default value for the filter (which also displays in the **Data Source Filter** section of the **List View** settings page), under **Filter Parameters**, click and highlight the filter, and then in the **Default Value** box, enter an appropriate value. If you do not enter a value, then when that filter is used for the first time, no items are displayed.</span></span>
    
  

## <a name="set-the-title-field-for-an-external-list"></a><span data-ttu-id="9fb4e-291">Настройка поля "Заголовок" для внешнего списка</span><span class="sxs-lookup"><span data-stu-id="9fb4e-291">Set the Title field for an external list</span></span>
<span data-ttu-id="9fb4e-292"><a name="section11"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-292"><a name="section11"> </a></span></span>


1. <span data-ttu-id="9fb4e-293">На ленте щелкните кнопку **Представление сводки**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-293">On the ribbon, click **Summary View**.</span></span>
    
  
2. <span data-ttu-id="9fb4e-294">В разделе **Поля** выберите поле с помощью параметра **Имя поля**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-294">In the **Fields** section, under **Field Name**, select a field.</span></span>
    
    > <span data-ttu-id="9fb4e-295">**Важно!** В общем случае рекомендуем задать для заголовка поля уникальное значение.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-295">**Important:** In general, it's a good idea to make the Title a field that has a unique value.</span></span> <span data-ttu-id="9fb4e-296">Поле "Заголовок" используется для отображения списка или форм InfoPath.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-296">The Title field is used to display list or InfoPath forms.</span></span> <span data-ttu-id="9fb4e-297">После установки значения в поле "Заголовок" его невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-297">Once you set the Title field, you cannot change it.</span></span> 
3. <span data-ttu-id="9fb4e-298">На ленте нажмите **Установить в качестве заголовка**.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-298">On the ribbon, click **Set as Title**.</span></span>
    
  

## <a name="complete-the-external-content-type"></a><span data-ttu-id="9fb4e-299">Завершение создания внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="9fb4e-299">Complete the external content type</span></span>
<span data-ttu-id="9fb4e-300"><a name="section12"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-300"><a name="section12"> </a></span></span>


- <span data-ttu-id="9fb4e-p132">На панели быстрого доступа нажмите кнопку **Сохранить**. При этом определение внешнего типа контента сохраняется в хранилище метаданных службы подключения к бизнес-данным.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-p132">On the Quick Access Toolbar, click **Save**. This stores the external content type definition in the Business Data Connectivity metadata store.</span></span>
    
  

> <span data-ttu-id="9fb4e-303">**Примечание.** Для повышения производительности служба подключения к бизнес-данным кэширует все объекты в хранилище метаданных и обновляет изменения с помощью задания таймера, выполняемого каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-303">**Note:** To provide better performance, Business Data Connectivity caches all the objects in the metadata store and updates changes by using a timer job that runs every minute.</span></span> <span data-ttu-id="9fb4e-304">Чтобы изменения распространились на всех серверах в ферме, может потребоваться до одной минуты, но на том сервере, где вносится изменение, они применяются мгновенно.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-304">It might take up to one minute for changes to propagate to all the servers in the farm, but changes are immediate on the server where you make the change.</span></span> 
  
    
    

<span data-ttu-id="9fb4e-305">Теперь в продуктах SharePoint и Office 2013 можно использовать внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="9fb4e-305">The external content type is now available for use in SharePoint and Office 2013 products.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="9fb4e-306">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9fb4e-306">Additional resources</span></span>
<span data-ttu-id="9fb4e-307"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="9fb4e-307"><a name="AR"> </a></span></span>


-  [<span data-ttu-id="9fb4e-308">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fb4e-308">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="9fb4e-309">Deploy a Business Connectivity Services on-premises solution in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fb4e-309">Deploy a Business Connectivity Services on-premises solution in SharePoint</span></span>](http://msdn.microsoft.com/library/4692ebba-90eb-4d72-ac12-e90c4d4ee7ae.aspx)
    
  
-  [<span data-ttu-id="9fb4e-310">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fb4e-310">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="9fb4e-311">Configure the Secure Store Service in SharePoint</span><span class="sxs-lookup"><span data-stu-id="9fb4e-311">Configure the Secure Store Service in SharePoint</span></span>](http://msdn.microsoft.com/library/29C0BC76-D835-401B-A2FB-ABB069E84125.aspx)
    
  

