---
title: "Журнал изменений запросов SharePoint с ChangeQuery и маркер изменения"
ms.date: 11/03/2017
ms.openlocfilehash: b255a298743e00c4616b691d4671ec5bea7c4463
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="query-sharepoint-change-log-with-changequery-and-changetoken"></a><span data-ttu-id="1b144-102">Журнал изменений запросов SharePoint с ChangeQuery и маркер изменения</span><span class="sxs-lookup"><span data-stu-id="1b144-102">Query SharePoint change log with ChangeQuery and ChangeToken</span></span>

<span data-ttu-id="1b144-103">Используйте **ChangeQuery** и **маркер изменения** для запроса журнал изменений SharePoint для изменения, внесенные в базу данных контента SharePoint, семейства веб-сайтов, сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="1b144-103">Use  **ChangeQuery** and **ChangeToken** to query the SharePoint change log for changes made to a SharePoint content database, site collection, site, or list.</span></span>

<span data-ttu-id="1b144-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="1b144-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="1b144-105">Журнал изменений SharePoint могут обращаться с помощью [ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery.aspx) и [маркер изменения](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.changetoken.aspx) для поиска и процесс изменения, выполненные для базы данных контента SharePoint, семейства веб-сайтов, сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="1b144-105">You can query the SharePoint change log by using [ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery.aspx) and [ChangeToken](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.changetoken.aspx) to find and process changes made on a SharePoint content database, site collection, site, or list.</span></span>

<span data-ttu-id="1b144-106">Пример кода [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) показано, как использовать журнал изменений SharePoint для поиска и обработки изменений, внесенных в списке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1b144-106">The [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) code sample shows you how to use SharePoint's change log to find and process changes made on a SharePoint list.</span></span> <span data-ttu-id="1b144-107">Используйте этот пример кода:</span><span class="sxs-lookup"><span data-stu-id="1b144-107">Use this code sample to:</span></span>

- <span data-ttu-id="1b144-108">Отслеживать изменения на список, сайт, семейства веб-сайтов или базы данных контента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1b144-108">Monitor SharePoint for changes on a list, site, site collection, or content database.</span></span>
    
- <span data-ttu-id="1b144-109">Запустите бизнес-процесс, после изменения элемента в список.</span><span class="sxs-lookup"><span data-stu-id="1b144-109">Start a business process after a change is made to an item in a list.</span></span>
    
- <span data-ttu-id="1b144-110">Дополнение к удаленного приемника событий.</span><span class="sxs-lookup"><span data-stu-id="1b144-110">Complement your remote event receiver.</span></span> <span data-ttu-id="1b144-111">С помощью шаблона журнала изменений с шаблон приемник удаленных событий предоставляет более надежная архитектура для обработки всех изменений баз данных контента, семейств веб-сайтов, сайтов или списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1b144-111">Using the change log pattern with a remote event receiver pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span></span> <span data-ttu-id="1b144-112">Принудительное выполнение удаленных приемников событий, но поскольку они выполняются на удаленном сервере, могут возникать ошибка связи.</span><span class="sxs-lookup"><span data-stu-id="1b144-112">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span></span> <span data-ttu-id="1b144-113">Шаблон журнала изменений гарантирует, что все изменения, доступны для обработки, но обычно обработки изменений приложение запускается по расписанию (например, задания таймера).</span><span class="sxs-lookup"><span data-stu-id="1b144-113">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span></span> <span data-ttu-id="1b144-114">Это означает, что изменения не обрабатываются немедленно.</span><span class="sxs-lookup"><span data-stu-id="1b144-114">This means that changes are not processed immediately.</span></span> <span data-ttu-id="1b144-115">При совместном использовании этих двух шаблонов убедитесь, что использовать механизм для предотвращения обработки такое же изменение дважды.</span><span class="sxs-lookup"><span data-stu-id="1b144-115">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span></span> <span data-ttu-id="1b144-116">Дополнительные сведения можно [использовать удаленные приемники событий в SharePoint](Use-remote-event-receivers-in-SharePoint.md).</span><span class="sxs-lookup"><span data-stu-id="1b144-116">For more information, see [Use remote event receivers in SharePoint](Use-remote-event-receivers-in-SharePoint.md).</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="1b144-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1b144-117">Before you begin</span></span>

<span data-ttu-id="1b144-118">Чтобы начать работу, загрузите пример надстройки [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="1b144-118">To get started, download the [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="1b144-119">Прежде чем запускать этот пример кода, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="1b144-119">Before you run this code sample, do the following:</span></span>

1. <span data-ttu-id="1b144-120">Вход на сайт Office 365, где необходимо создать список.</span><span class="sxs-lookup"><span data-stu-id="1b144-120">Sign in to your Office 365 site where you want to create the list.</span></span>
    
2. <span data-ttu-id="1b144-121">Выберите **элементы контент сайта**.</span><span class="sxs-lookup"><span data-stu-id="1b144-121">Choose  **Site Contents**.</span></span>
    
3. <span data-ttu-id="1b144-122">Последовательно выберите пункты **Добавить надстройку в**.</span><span class="sxs-lookup"><span data-stu-id="1b144-122">Choose  **add an add-in**.</span></span>
    
4. <span data-ttu-id="1b144-123">Выберите **Настраиваемый список**.</span><span class="sxs-lookup"><span data-stu-id="1b144-123">Choose  **Custom List**.</span></span>
    
5. <span data-ttu-id="1b144-124">В поле **имя**введите **TestList**.</span><span class="sxs-lookup"><span data-stu-id="1b144-124">In  **Name**, enter  **TestList**.</span></span>
    
6. <span data-ttu-id="1b144-125">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1b144-125">Choose  **Create**.</span></span>
    
<span data-ttu-id="1b144-126">Чтобы просмотреть демонстрационный ролик этот пример кода, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1b144-126">To see a demo of this code sample, perform the following steps:</span></span>

1. <span data-ttu-id="1b144-127">Выберите **Пуск** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b144-127">Choose  **Start** in Visual Studio.</span></span>
    
2. <span data-ttu-id="1b144-128">Введите URL-адрес сайта Office 365, имя списка (**TestList**) и учетные данные Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b144-128">Enter your Office 365 site's URL, the name of the list (**TestList**), and your Office 365 credentials.</span></span> <span data-ttu-id="1b144-129">Теперь консольное приложение ожидает вносить изменения в **TestList**.</span><span class="sxs-lookup"><span data-stu-id="1b144-129">The console application now waits for changes to be made to **TestList**.</span></span> <span data-ttu-id="1b144-130">По умолчанию консольное приложение проверяет журнал изменений и обновляет отображение каждые 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="1b144-130">By default, the console application checks the change log and updates the display every 30 seconds.</span></span>
    
3. <span data-ttu-id="1b144-131">Добавьте новый элемент **TestList**:</span><span class="sxs-lookup"><span data-stu-id="1b144-131">Add a new item to  **TestList**:</span></span>
    
    1. <span data-ttu-id="1b144-132">Откройте сайт Office 365 и перейдите к **Контент сайта** > **TestList**.</span><span class="sxs-lookup"><span data-stu-id="1b144-132">Open your Office 365 site and go to  **Site Contents** > **TestList**.</span></span>
    
    2. <span data-ttu-id="1b144-133">Выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="1b144-133">Choose  **new item**.</span></span>
    
    3. <span data-ttu-id="1b144-134">Введите **MyTitle** в поле **Название**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1b144-134">Enter  **MyTitle** in **Title**, and then choose  **Save**.</span></span>
    
4. <span data-ttu-id="1b144-135">Убедитесь, что изменения отображаются в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="1b144-135">Verify that your change appears in the console application.</span></span> <span data-ttu-id="1b144-136">Вы можете принудительно консольного приложения для чтения журнала изменений SharePoint посредством ввода данных **r** в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="1b144-136">You can force the console application to read SharePoint's change log by entering  **r** in the console application.</span></span>

## <a name="use-the-corelistitemchangemonitor-add-in"></a><span data-ttu-id="1b144-137">Использовать надстройки Core.ListItemChangeMonitor</span><span class="sxs-lookup"><span data-stu-id="1b144-137">Use the Core.ListItemChangeMonitor add-in</span></span>

<span data-ttu-id="1b144-138">В Program.cs **Main** вызывается **DoWork** для чтения и обработки журнал изменений SharePoint:</span><span class="sxs-lookup"><span data-stu-id="1b144-138">In Program.cs,  **Main** calls **DoWork** to read and process SharePoint's change log:</span></span>

1. <span data-ttu-id="1b144-139">Создайте объект **ChangeQuery** для доступа к журналу изменений в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1b144-139">Create a  **ChangeQuery** object to access SharePoint's change log.</span></span>
    
2. <span data-ttu-id="1b144-140">Использование журнала изменений для возврата изменений элементов с помощью **cq. Элемент = true**.</span><span class="sxs-lookup"><span data-stu-id="1b144-140">Use the change log to return changes to items by using  **cq.Item = true**.</span></span> <span data-ttu-id="1b144-141">Следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="1b144-141">Changes include:</span></span>
    
    - <span data-ttu-id="1b144-142">Новых элементов, добавленных с помощью **cq. Добавление = true**.</span><span class="sxs-lookup"><span data-stu-id="1b144-142">New items added by using  **cq.Add= true**.</span></span>
    
    - <span data-ttu-id="1b144-143">Удаленные элементы с помощью **cq. DeleteObject = true**.</span><span class="sxs-lookup"><span data-stu-id="1b144-143">Deleted items by using  **cq.DeleteObject = true**.</span></span>
    
    - <span data-ttu-id="1b144-144">Элементы изменены с помощью **cq. Обновление = true**.</span><span class="sxs-lookup"><span data-stu-id="1b144-144">Modified items by using  **cq.Update=true**.</span></span>
    
3. <span data-ttu-id="1b144-145">Создайте объект **маркер изменения** для чтения изменений из журнала изменений из определенного момента времени.</span><span class="sxs-lookup"><span data-stu-id="1b144-145">Create a  **ChangeToken** object to read changes from the change log from a certain point in time.</span></span>
    
4. <span data-ttu-id="1b144-146">Значение [ChangeToken.StringValue](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changetoken.stringvalue.aspx) с номером версии, изменить область, идентификатор GUID **TestList** , Дата и время изменения и значения элемента изменений в маркер изменения (initialize с значение -1).</span><span class="sxs-lookup"><span data-stu-id="1b144-146">Set [ChangeToken.StringValue](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changetoken.stringvalue.aspx) with the version number, change scope, GUID of **TestList** , date and time when changes occurred, and the change item value on the ChangeToken (initialize with a value of -1).</span></span> <span data-ttu-id="1b144-147">В этом примере кода ограничивает объем изменений, чтение из журнала изменений инициализация дату и время возникновения изменений в предыдущих двух дней с помощью **DateTime.Now.AddDays(-2). ToUniversalTime(). Ticks.ToString()**.</span><span class="sxs-lookup"><span data-stu-id="1b144-147">This code sample limits the amount of changes read from the change log by initializing the date and time when the changes occurred to the previous two days by using **DateTime.Now.AddDays(-2).ToUniversalTime().Ticks.ToString()**.</span></span>
    
5.  <span data-ttu-id="1b144-148">Чтение журнала изменений либо каждые 30 секунд (которые период ожидания по умолчанию задано с постоянным **WaitSeconds**), или когда пользователь вводит **r**.</span><span class="sxs-lookup"><span data-stu-id="1b144-148">Read the change log either every 30 seconds (which is the default waiting period set by the constant **WaitSeconds**), or when the user enters **r**.</span></span> <span data-ttu-id="1b144-149">При чтении журнала изменений, консольного приложения необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1b144-149">When reading the change log, the console application performs the following steps:</span></span>
    
    1.  <span data-ttu-id="1b144-150">Использует [List.GetChanges](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.getchanges.aspx) для возврата [ChangeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changecollection.aspx), который представляет собой коллекцию изменения, внесенные в список с момента последнего изменения времени обработки.</span><span class="sxs-lookup"><span data-stu-id="1b144-150">Uses [List.GetChanges](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.getchanges.aspx) to return the [ChangeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changecollection.aspx), which is a collection of changes made to the list since the last time changes were processed.</span></span>
    
    2. <span data-ttu-id="1b144-151">Вызывает **DisplayChanges** , чтобы отобразить изменения в объекте **ChangeCollection** .</span><span class="sxs-lookup"><span data-stu-id="1b144-151">Calls  **DisplayChanges** to display the changes in the **ChangeCollection** object.</span></span>
    
    3. <span data-ttu-id="1b144-152">Задает новую точку времени на чтение изменений из журнала изменений.</span><span class="sxs-lookup"><span data-stu-id="1b144-152">Sets the new point in time to read changes from the change log.</span></span> <span data-ttu-id="1b144-153">Если существует изменений в списке (который был возвращен в **coll**), необходимо задать **ChangeTokenStart** к последнему его изменить дату и время.</span><span class="sxs-lookup"><span data-stu-id="1b144-153">If there are changes to the list (which was returned in  **coll**), set **ChangeTokenStart** to the last change's date and time.</span></span>

> [!NOTE] 
> <span data-ttu-id="1b144-154">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="1b144-154">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
private static void DoWork()
        {
            Console.WriteLine();
            Console.WriteLine("Url: " + url);
            Console.WriteLine("User name: " + userName);
            Console.WriteLine("List name: " + listName);
            Console.WriteLine();
            try
            {

                Console.WriteLine(string.Format("Connecting to {0}", url));
                Console.WriteLine();
                ClientContext cc = new ClientContext(url);
                cc.AuthenticationMode = ClientAuthenticationMode.Default;
                cc.Credentials = new SharePointOnlineCredentials(userName, password);

                ListCollection lists = cc.Web.Lists;
                IEnumerable<List> results = cc.LoadQuery<List>(lists.Where(lst => lst.Title == listName));
                cc.ExecuteQuery();
                List list = results.FirstOrDefault();
                if (list == null)
                {

                    Console.WriteLine("A list named \"{0}\" does not exist. Press any key to exit...", listName);
                    Console.ReadKey();
                    return;
                }

                nextRunTime = DateTime.Now;

                ChangeQuery cq = new ChangeQuery(false, false);
                cq.Item = true;
                cq.DeleteObject = true;
                cq.Add = true;
                cq.Update = true;

                // Set the ChangeTokenStart to two days ago to reduce how much data is returned from the change log. Depending on your requirements, you might want to change this value. 
                // The value of the string assigned to ChangeTokenStart.StringValue is semicolon delimited, and takes the following parameters in the order listed:
                // Version number. 
                // The change scope (0 - Content Database, 1 - site collection, 2 - site, 3 - list).
                // GUID of the item the scope applies to (for example, GUID of the list). 
                // Time (in UTC) from when changes occurred.
                // Initialize the change item on the ChangeToken using a default value of -1.

                cq.ChangeTokenStart = new ChangeToken();
                cq.ChangeTokenStart.StringValue = string.Format("1;3;{0};{1};-1", list.Id.ToString(), DateTime.Now.AddDays(-2).ToUniversalTime().Ticks.ToString());

                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine(string.Format("Ctrl+c to exit. Press \"r\" key to force the console application to read the change log without waiting {0} seconds.", WaitSeconds));
                Console.WriteLine();
                Console.ResetColor();
                do
                {
                    do
                    {
                        if (Console.KeyAvailable &amp;&amp; Console.ReadKey(true).KeyChar == 'r') { break; }
                    }
                    while (nextRunTime > DateTime.Now);

                    Console.WriteLine(string.Format("Looking for items modified after {0} UTC", GetDateStringFromChangeToken(cq.ChangeTokenStart)));

                    
                    ChangeCollection coll = list.GetChanges(cq);
                    cc.Load(coll);
                    cc.ExecuteQuery();


                    DisplayChanges(coll, cq.ChangeTokenStart);
                    // If there are changes to the list (which was returned in coll), set ChangeTokenStart to the last change's date and time. This will be used as the starting point for the next read from the change log.                      
                    cq.ChangeTokenStart = coll.Count > 0 ? coll.Last().ChangeToken : cq.ChangeTokenStart;

                    nextRunTime = DateTime.Now.AddSeconds(WaitSeconds);

                } while (true);
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
                Console.WriteLine("Press any key to exit...");
                Console.ReadKey();

            }
        }
```

## <a name="see-also"></a><span data-ttu-id="1b144-155">См. также</span><span class="sxs-lookup"><span data-stu-id="1b144-155">See also</span></span>
<span data-ttu-id="1b144-156"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="1b144-156"></span></span>

- [<span data-ttu-id="1b144-157">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="1b144-157">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [<span data-ttu-id="1b144-158">Использование удаленных приемников событий в SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b144-158">Use remote event receivers in SharePoint</span></span>](Use-remote-event-receivers-in-SharePoint.md)
    
- [<span data-ttu-id="1b144-159">Члены ChangeQuery</span><span class="sxs-lookup"><span data-stu-id="1b144-159">ChangeQuery members</span></span>](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery_members.aspx)
    
- [<span data-ttu-id="1b144-160">Центр для разработчиков шаблоны и рекомендации</span><span class="sxs-lookup"><span data-stu-id="1b144-160">Patterns and Practices developer center</span></span>](http://dev.office.com/patterns-and-practices)
