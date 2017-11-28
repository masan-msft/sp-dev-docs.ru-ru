---
title: "Журнал изменений запросов SharePoint с ChangeQuery и маркер изменения"
ms.date: 11/03/2017
ms.openlocfilehash: 79458791659ce0e750446d22d49564ff6998db1a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="query-sharepoint-change-log-with-changequery-and-changetoken"></a>Журнал изменений запросов SharePoint с ChangeQuery и маркер изменения

Используйте **ChangeQuery** и **маркер изменения** для запроса журнал изменений SharePoint для изменения, внесенные в базу данных контента SharePoint, семейства веб-сайтов, сайта или списка.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Журнал изменений SharePoint могут обращаться с помощью [ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery.aspx) и [маркер изменения](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.changetoken.aspx) для поиска и процесс изменения, выполненные для базы данных контента SharePoint, семейства веб-сайтов, сайта или списка.

Пример кода [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) показано, как использовать журнал изменений SharePoint для поиска и обработки изменений, внесенных в списке SharePoint. Используйте этот пример кода:

- Отслеживать изменения на список, сайт, семейства веб-сайтов или базы данных контента SharePoint.
    
- Запустите бизнес-процесс, после изменения элемента в список.
    
- Дополнение к удаленного приемника событий. С помощью шаблона журнала изменений с шаблон приемник удаленных событий предоставляет более надежная архитектура для обработки всех изменений баз данных контента, семейств веб-сайтов, сайтов или списков SharePoint. Принудительное выполнение удаленных приемников событий, но поскольку они выполняются на удаленном сервере, могут возникать ошибка связи. Шаблон журнала изменений гарантирует, что все изменения, доступны для обработки, но обычно обработки изменений приложение запускается по расписанию (например, задания таймера). Это означает, что изменения не обрабатываются немедленно. При совместном использовании этих двух шаблонов убедитесь, что использовать механизм для предотвращения обработки такое же изменение дважды. Дополнительные сведения можно [использовать удаленные приемники событий в SharePoint](Use-remote-event-receivers-in-SharePoint.md).
    
## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.ListItemChangeMonitor](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ListItemChangeMonitor) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать этот пример кода, выполните следующее:

1. Вход на сайт Office 365, где необходимо создать список.
    
2. Выберите **элементы контент сайта**.
    
3. Последовательно выберите пункты **Добавить надстройку в**.
    
4. Выберите **Настраиваемый список**.
    
5. В поле **имя**введите **TestList**.
    
6. Нажмите кнопку **Создать**.
    
Чтобы просмотреть демонстрационный ролик этот пример кода, выполните следующие действия:

1. Выберите **Пуск** в Visual Studio.
    
2. Введите URL-адрес сайта Office 365, имя списка (**TestList**) и учетные данные Office 365. Теперь консольное приложение ожидает вносить изменения в **TestList**. По умолчанию консольное приложение проверяет журнал изменений и обновляет отображение каждые 30 секунд.
    
3. Добавьте новый элемент **TestList**:
    
    1. Откройте сайт Office 365 и перейдите к **Контент сайта** > **TestList**.
    
    2. Выберите **новый элемент**.
    
    3. Введите **MyTitle** в поле **Название**и нажмите кнопку **Сохранить**.
    
4. Убедитесь, что изменения отображаются в консольное приложение. Вы можете принудительно консольного приложения для чтения журнала изменений SharePoint посредством ввода данных **r** в консольное приложение.

## <a name="use-the-corelistitemchangemonitor-add-in"></a>Использовать надстройки Core.ListItemChangeMonitor

В Program.cs **Main** вызывается **DoWork** для чтения и обработки журнал изменений SharePoint:

1. Создайте объект **ChangeQuery** для доступа к журналу изменений в SharePoint.
    
2. Использование журнала изменений для возврата изменений элементов с помощью **cq. Элемент = true**. Следующие изменения:
    
    - Новых элементов, добавленных с помощью **cq. Добавление = true**.
    
    - Удаленные элементы с помощью **cq. DeleteObject = true**.
    
    - Элементы изменены с помощью **cq. Обновление = true**.
    
3. Создайте объект **маркер изменения** для чтения изменений из журнала изменений из определенного момента времени.
    
4. Значение [ChangeToken.StringValue](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changetoken.stringvalue.aspx) с номером версии, изменить область, идентификатор GUID **TestList** , Дата и время изменения и значения элемента изменений в маркер изменения (initialize с значение -1). В этом примере кода ограничивает объем изменений, чтение из журнала изменений инициализация дату и время возникновения изменений в предыдущих двух дней с помощью **DateTime.Now.AddDays(-2). ToUniversalTime(). Ticks.ToString()**.
    
5.  Чтение журнала изменений либо каждые 30 секунд (которые период ожидания по умолчанию задано с постоянным **WaitSeconds**), или когда пользователь вводит **r**. При чтении журнала изменений, консольного приложения необходимо выполнить следующие действия:
    
    1.  Использует [List.GetChanges](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.list.getchanges.aspx) для возврата [ChangeCollection](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changecollection.aspx), который представляет собой коллекцию изменения, внесенные в список с момента последнего изменения времени обработки.
    
    2. Вызывает **DisplayChanges** , чтобы отобразить изменения в объекте **ChangeCollection** .
    
    3. Задает новую точку времени на чтение изменений из журнала изменений. Если существует изменений в списке (который был возвращен в **coll**), необходимо задать **ChangeTokenStart** к последнему его изменить дату и время.

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [Использование удаленных приемников событий в SharePoint](Use-remote-event-receivers-in-SharePoint.md)
    
- [Члены ChangeQuery](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.changequery_members.aspx)
    
- [Центр для разработчиков шаблоны и рекомендации](http://dev.office.com/patterns-and-practices)
