---
title: "Использование удаленных приемников событий в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d6c2026aa9ae377601a42662fa5aebbb688011a7
ms.sourcegitcommit: 895d31071e73aa23e62593c9ffa46b38701ba801
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2018
---
# <a name="use-remote-event-receivers-in-sharepoint"></a>Использование удаленных приемников событий в SharePoint

Использование удаленных приемников событий для обработки событий в объектная модель SharePoint. Используйте для установки или удаления объектов SharePoint и другие приемников событий, добавьте в необходимые события AppInstalled и AppUninstalling.

_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_

>**Важные** По состоянию на январь 2017 SharePoint Online поддерживает webhooks списка, который можно использовать вместо «-ed» удаленные приемники событий. Извлечение [webhooks Общие сведения о SharePoint](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) для получения дополнительных сведений о webhooks. Обратите внимание, что несколько примеров webhook доступны из репозитория репозиториев [sp dev примеры](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) .

Пример [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) показано, как использовать размещение у поставщика в надстройке с удаленного приемника событий для обработки событий AppInstalled и AppUninstalling. События AppInstalled и AppUninstalling Установка и удаление объектов SharePoint, которые используются надстройки при запуске. Кроме того обработчик событий AppInstalled добавляет обработчик событий ItemAdded со списком. Если вы хотите используйте этого решения:

- Настройка надстройки на, сначала запустите с помощью события AppInstalled для настройки различных объектов SharePoint или приемников событий, надстройка для работы с.
    
- Замените приемников событий создана с использованием решения с полным доверием кодом. В полностью доверенной кода решения можно запустить приемников событий на сервере SharePoint. В новой надстройки модели SharePoint так как не удается запустить приемник событий на сервере SharePoint необходимо реализовать удаленного приемника событий на веб-сервере.
    
- Получайте уведомления о отмену изменения в SharePoint. К примеру при добавлении нового элемента в список, которую необходимо выполнить задачи.

- Дополнение решения журнала изменений. С использованием шаблона приемника удаленных событий с шаблоном журнал изменений содержит более надежная архитектура для обработки всех изменений баз данных контента, семейств веб-сайтов, сайтов или списков SharePoint. Принудительное выполнение удаленных приемников событий, но поскольку они выполняются на удаленном сервере, могут возникать ошибка связи. Шаблон журнала изменений гарантирует, что все изменения, доступны для обработки, но обычно обработки изменений приложение запускается по расписанию (например, задания таймера). Это означает, что изменения не обрабатываются немедленно. При совместном использовании этих двух шаблонов убедитесь, что использовать механизм для предотвращения обработки такое же изменение дважды. Для получения дополнительных сведений см [SharePoint запрос изменения журнала с ChangeQuery и маркер изменения](query-sharepoint-change-log-with-changequery-and-changeToken.md).

> [!NOTE] 
> Размещение в SharePoint надстройки не поддерживают удаленных приемников событий. Чтобы использовать удаленные приемники событий, необходимо использовать размещение у поставщика в надстройке. Не следует использовать удаленных приемников событий для синхронизации или долго выполняющихся процессов. Дополнительные сведения можно [как: Создание приемника событий надстройка](https://msdn.microsoft.com/library/office/jj220052.aspx).

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать эта надстройка, сделайте следующее:

1. В свойства проекта Core.EventReceivers убедитесь, что **Управление установленными приложениями** и **Обработка удаляемого приложения** имеет значение **True**. Установка **Управление установленными приложениями** и **Обработка удаляемого приложения** **значения True** создает службы WCF, который определяет обработчик событий для события **AppInstalled** и **AppUninstalling** . В Core.EventReceivers откройте контекстное меню (щелкните правой кнопкой мыши) на файл AppManifest.xml и выберите **Свойства**. **InstalledEventEndpoint** и **UninstallingEventEndpoint** указывают на удаленный приемник событий, который обрабатывает события **AppInstalled** и **AppUninstalling** .
    
2. Присоединение удаленного приемника событий для объекта на хост-сайте обычно требуется разрешение **Управление** для только этот объект. Например при присоединении приемника событий в существующий список, надстройки требуется разрешение **Управление** в **список** только. В этом примере кода требуются разрешения **Управление** **Web** , так как он добавляется список и активирует компонент на хост-сайта. Чтобы задать управление разрешениями в Интернете:
    
    1. Дважды щелкните Core.EventReceivers\AppManifest.xml.
    
    2. Выберите **разрешения**.
    
    3. Убедитесь, что **область** имеет значение **Web**и набор **разрешений** на **Управление**.
    
3. Для запуска этого примера кода требуется Azure подписки. Чтобы подписаться на пробную версию, обратитесь к разделу [Бесплатная пробная версия на один месяц](http://azure.microsoft.com/en-us/pricing/free-trial/).
    
4. Создайте пространство имен шины Azure службы.
    
    1. Выполните инструкции в разделе [Создание пространство имен служебной шины](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-create-namespace-portal).

    2. Скопируйте **Основной строку подключения** с только что созданный пространства имен шины обслуживания
    
    3. Вернуться в Visual Studio.
    
    4. Щелкните правой кнопкой мыши Core.EventReceivers > **Свойства** > **SharePoint**.
    
    5. Установите флажок **Включить отладку через шину службы Microsoft Azure**.
    
    6. В поле **Строка подключения шины службы Microsoft Azure**вставьте строку подключения.
    
    7. Выберите команду **Сохранить**.
    
5. Выполнение примера кода и выполните следующие дополнительные действия:
    
    - Нажмите кнопку **Доверять** в окне **Предоставление разрешений для приложения** .
    
    - Закройте окно **Предоставление разрешений для приложения** .
    
    - После завершения установки надстройки и службы WCF, откроется браузер.
    
    - Вход на сайт Office 365. Откроется страница start надстройки Core.EventReceivers.

## <a name="use-the-coreeventreceivers-add-in"></a>Использовать надстройки Core.EventReceivers
<a name="sectionSection1"> </a>

Чтобы просмотреть демонстрационный пример кода Core.EventReceivers:

1. Запуск образца и на странице "Запуск" выберите **веб-узел**.
    
2. Выберите **элементы контент сайта**.
    
3. Выберите **задания приемника удаленных событий**.
    
4. Выберите **новый элемент**.
    
5. В поле **Название**введите **Contoso**и в **поле Описание** введите **Contoso тестирования**.
    
6. Вернуться к списку и обновить страницу.
    
7. Убедитесь, что описание добавляемого элемента была обновлены для **тестирования Contoso обновлен с ReR 192336**, где **192336** — отметку времени.
    
Services/AppEventReceiver.cs **AppEventReceiver** реализует интерфейс **IRemoteEventService** . В этом примере кода предоставляет реализацию **методе ProcessEvent** , так как они используют синхронные события. Если вы используете асинхронные события, необходимо предоставить реализацию метода **ProcessOneWayEvent** .

**ProcessEvent** обрабатывает следующие **SPRemoteEventType** удаленных событий.

-  События **AppInstalled** при установке надстройки. При возникновении события **AppInstalled** **ProcessEvent** вызовов **HandleAppInstalled**.
    
-  События **AppUninstalling** при удалении надстройки. При возникновении события **AppUninstalling** **ProcessEvent** вызовов **HandleAppUninstalling**. Событие **AppUninstalling** выполняется только в том случае, когда пользователь полностью удаляет надстройку, удалив надстройки из корзины сайта (для конечных пользователей) или удаления надстройку из списка **тестирование приложений** (для разработчиков).
    
-  Событий **ItemAdded** при добавлении элемента в список. Когда возникает событие **ItemAdded** вызовы **ProcessEvent** **HandleItemAdded**.

> [!NOTE] 
> В окне Свойства проекта Core.EventReceiver доступны только свойства, **Управление установленными приложениями** и **Обработка удаляемого приложения** . В этом примере кода показано, как добавить обработчик событий **ItemAdded** для списка на веб-сайт с помощью события **AppInstalled** во время установки надстройки.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {

            SPRemoteEventResult result = new SPRemoteEventResult();

            switch (properties.EventType)
            {
                case SPRemoteEventType.AppInstalled:
                    HandleAppInstalled(properties);
                    break;
                case SPRemoteEventType.AppUninstalling:
                    HandleAppUninstalling(properties);
                    break;
                case SPRemoteEventType.ItemAdded:
                    HandleItemAdded(properties);
                    break;
            }


            return result;
        }
```

**HandleAppInstalled** вызывает **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** RemoteEventReceiverManager.cs.

```C#
 private void HandleAppInstalled(SPRemoteEventProperties properties)
        {
            using (ClientContext clientContext =
                TokenHelper.CreateAppEventClientContext(properties, false))
            {
                if (clientContext != null)
                {
                    new RemoteEventReceiverManager().AssociateRemoteEventsToHostWeb(clientContext);
                }
            }
        }
```

**AssociateRemoteEventsToHostWeb** создает или позволяет различных объектов SharePoint, используемые надстройкой Core.EventReceivers. Ваши требования могут отличаться. **AssociateRemoteEventsToHostWeb** выполняет следующие действия:

- Включает Push-уведомлений с помощью **Web.Features.Add**.
    
- Использует объект **clientContext** для поиска для списка. Если список не существует, **CreateJobsList** создает список. Если список существует, **List.EventReceivers** используется для поиска существующего получателя событий, имя которого является **ItemAddedEvent**.
    
- Если не существует **ItemAddedEvent** приемника событий:
    
    - Создает новый объект **EventReceiverDefinitionCreationInformation** для создания нового приемника удаленных событий. Тип приемника событий **ItemAdded** добавляется **EventReceiverDefinitionCreationInformation.EventType**.
    
    - Задает **EventReceiverDefinitionCreationInformation.ReceiverURL** URL-адрес в **AppInstalled** удаленный приемник событий.
    
    - Добавляет новый приемника событий в список с помощью **List.EventReceivers.Add**.

```C#
public void AssociateRemoteEventsToHostWeb(ClientContext clientContext)
        {
            // Add Push Notification feature to host web.
            // Not required but it is included here to show you
            // how to activate features.
            clientContext.Web.Features.Add(
                     new Guid("41e1d4bf-b1a2-47f7-ab80-d5d6cbba3092"),
                     true, FeatureDefinitionScope.None);


            // Get the Title and EventReceivers lists.
            clientContext.Load(clientContext.Web.Lists,
                lists => lists.Include(
                    list => list.Title,
                    list => list.EventReceivers).Where
                        (list => list.Title == LIST_TITLE));

            clientContext.ExecuteQuery();

            List jobsList = clientContext.Web.Lists.FirstOrDefault();

            bool rerExists = false;
            if (null == jobsList)
            {
                // List does not exist, create it. 
                jobsList = CreateJobsList(clientContext);

            }
            else
            {
                foreach (var rer in jobsList.EventReceivers)
                {
                    if (rer.ReceiverName == RECEIVER_NAME)
                    {
                        rerExists = true;
                        System.Diagnostics.Trace.WriteLine("Found existing ItemAdded receiver at "
                            + rer.ReceiverUrl);
                    }
                }
            }

            if (!rerExists)
            {
                EventReceiverDefinitionCreationInformation receiver =
                    new EventReceiverDefinitionCreationInformation();
                receiver.EventType = EventReceiverType.ItemAdded;
                
                // Get WCF URL where this message was handled.
                OperationContext op = OperationContext.Current;
                Message msg = op.RequestContext.RequestMessage;
                receiver.ReceiverUrl = msg.Headers.To.ToString();

                receiver.ReceiverName = RECEIVER_NAME;
                receiver.Synchronization = EventReceiverSynchronization.Synchronous;

                // Add the new event receiver to a list in the host web.
                jobsList.EventReceivers.Add(receiver);
                clientContext.ExecuteQuery();

                System.Diagnostics.Trace.WriteLine("Added ItemAdded receiver at " + receiver.ReceiverUrl);
            }
        }
```

При добавлении элемента в список **Заданий приемника удаленных событий** **ProcessEvent** в AppEventReceiver.svc.cs обрабатывает событие **ItemAdded** , а затем вызывает **HandleItemAdded**.  **HandleItemAdded** вызывает **RemoteEventReceiverManager.ItemAddedToListEventHandler**.  **ItemAddedToListEventHandler** выбирает элемент списка, который был добавлен и добавляет строку **обновлен с ReR** описание элемента списка.

```C#
 public void ItemAddedToListEventHandler(ClientContext clientContext, Guid listId, int listItemId)
        {
            try
            {
                List photos = clientContext.Web.Lists.GetById(listId);
                ListItem item = photos.GetItemById(listItemId);
                clientContext.Load(item);
                clientContext.ExecuteQuery();

                item["Description"] += "\nUpdated by RER " +
                    System.DateTime.Now.ToLongTimeString();
                item.Update();
                clientContext.ExecuteQuery();
            }
            catch (Exception oops)
            {
                System.Diagnostics.Trace.WriteLine(oops.Message);
            }

        }
```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Core.AppEvents.HandlerDelegation](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    
