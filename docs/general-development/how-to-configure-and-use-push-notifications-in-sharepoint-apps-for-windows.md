---
title: "Настройка и использование push-уведомлений в приложениях SharePoint для Windows Phone"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 68fa2138-86d9-4e35-9c7c-5cd292087b80
ms.openlocfilehash: b9e6c480be922250a62a524a703ea2cd0925b548
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="configure-and-use-push-notifications-in-sharepoint-apps-for-windows-phone"></a>Настройка и использование push-уведомлений в приложениях SharePoint для Windows Phone

Создайте в SharePoint Server решение для отправки push-уведомлений и разработайте приложение Windows Phone для получения этих уведомлений. Использование службы Push-уведомления Майкрософт (MPNS), приложения для Windows Phone могут получать уведомления по Интернету событий, которые запускаются на Microsoft SharePoint Server. Приложение телефон не опроса сервера для изменения, например, элементов в виде списка, лежащие в основе приложение телефон. Приложения могут быть зарегистрированы на получение уведомлений с сервера, а приемника событий можно инициировать уведомление и отправьте его в получающей приложение для обработки. Ретрансляция push-уведомлений для устройств Windows Phone с MPNS.
  
    
    

Windows Phone 7 не поддерживает выполнение нескольких приложений одновременно. Кроме компонентов операционной системы Windows Phone () самой ОС только одно приложение может быть запущено на телефоне за раз. Событие, предназначенных для заданного телефона приложения могут возникать (например, например, для элемента списка добавленные в список), если приложение не запущены на переднем плане по телефону (то есть, когда приложение захороненные или закрытой). Можно разработать службы фона на телефоне с помощью периодических задач, который может проверить для изменения списка на сервере, но этот подход, потребляют ресурсы (например, пропускной способности и батарей мощность сети) на телефоне. С MPNS и компоненты, поддерживающие уведомлений, встроенные в ОС Windows Phone 7 телефона самого может получать уведомления, связанные с содержимым для данного приложения, даже если это приложение не запущены  и пользователь может предоставляется возможность запуска соответствующего приложения в ответ на уведомление. (Дополнительные сведения о push-уведомлений, см.  [Обзор Push уведомления для Windows Phone](http://msdn.microsoft.com/en-us/library/ff402558%28VS.92%29.aspx) в библиотеке MSDN.) В этом разделе создайте решение на сервере для отправки push-уведомлений в приложении phone на основании изменений в списке  это приложение на основе. Затем создается приложение телефона для получения этих уведомлений.
  
    
    


## <a name="create-a-server-side-solution-to-send-push-notifications-based-on-a-list-item-event"></a>Создание решения на сервере для отправки push-уведомления на основании события элемента списка
<a name="BKMK_ServerSideSolution"> </a>

Решение на сервере может быть развернут в объекте изолированной **SPWeb** приложение SharePoint или решение фермы SharePoint, представлена в виде пакета решения SharePoint (то есть, WSP-файл), содержащий компонент веб сайтов. В процедур, описанных в этом разделе будет разрабатываться простое решение SharePoint, который создает целевого списка для использования в приложении Windows Phone и, которая активирует механизм извещения уведомления на сервере. В разделе последующие будет разрабатывать приложения Windows Phone для получения уведомлений в решение на сервере.
  
    
    

### <a name="to-create-the-server-side-project"></a>Создание проекта на сервере


1. Запустите Visual Studio 2012 с параметром **Запуск от имени администратора**.
    
  
2. Выберите **Файл**, **Создать**, **Проект**.
    
    Отобразится диалоговое окно **Новый проект**.
    
  
3. В диалоговом окне **Новый проект** разверните узел **SharePoint** в разделе **Visual C#** и затем выберите узел **15**.
    
  
4. В области **Шаблоны** выберите **Проект SharePoint** и укажите имя проекта, такие asPushNotificationsList.
    
  
5. Нажмите кнопку « **ОК** ». Откроется мастер настройки SharePoint. Мастер позволяет выбрать целевого объекта для разработки и отладки проекта и уровень доверия решения.
    
  
6. Укажите URL-адрес сайта SharePoint Server. Выберите узел, который можно использовать в разработке приложения списка SharePoint для Windows Phone.
    
  
7. Выберите **Развернуть как решение фермы** и нажмите кнопку **Готово**, чтобы создать проект.
    
  
Затем добавьте файл класса в проект и создать несколько классов для инкапсуляции и управление push-уведомлений.
  
    
    

### <a name="to-create-the-classes-for-managing-push-notifications"></a>Создание классов для управления push-уведомлениями


1. В **Обозревателе решений** выберите узел, представляющий проект (с именемPushNotificationsList , если вы следуете соглашению об именовании, которое используется в данном разделе).
    
  
2. В меню **Проект** выберите **Добавить класс**. Отобразится диалоговое окно **Добавление нового элемента** с выбранным шаблоном **Класс** C#.
    
  
3. Укажите PushNotification.cs в качестве имени файла и нажмите кнопку **Добавить**. Файл класса добавляется в решение и открывается для редактирования.
    
  
4. Замените содержимое файла следующим кодом.
    
```cs
  
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net;
using System.Text;
using Microsoft.SharePoint;

namespace PushNotificationsList
{
    internal static class WP7Constants
    {
        internal static readonly string[] WP_RESPONSE_HEADERS = 
            {
                "X-MessageID",
                "X-DeviceConnectionStatus",
                "X-SubscriptionStatus",
                "X-NotificationStatus"
            };
    }

    public enum TileIntervalValuesEnum
    {
        ImmediateTile = 1,
        Delay450SecondsTile = 11,
        Delay900SecondsTile = 21,
    }

    public enum ToastIntervalValuesEnum
    {
        ImmediateToast = 2,
        Delay450SecondsToast = 12,
        Delay900SecondsToast = 22,
    }

    public enum RawIntervalValuesEnum
    {
        ImmediateRaw = 3,
        Delay450SecondsRaw = 13,
        Delay900SecondsRaw = 23
    }

    public enum NotificationTypeEnum
    {
        Tile = 1,
        Toast = 2,
        Raw = 3
    }

    class PushNotification
    {
        public PushNotificationResponse PushToast(SPPushNotificationSubscriber subscriber, string toastTitle, string toastMessage, string toastParam, ToastIntervalValuesEnum intervalValue)
        {
            // Construct toast notification message from parameter values.
            string toastNotification = "<?xml version=\\"1.0\\" encoding=\\"utf-8\\"?>" +
            "<wp:Notification xmlns:wp=\\"WPNotification\\">" +
               "<wp:Toast>" +
                    "<wp:Text1>" + toastTitle + "</wp:Text1>" +
                    "<wp:Text2>" + toastMessage + "</wp:Text2>" +
                    "<wp:Param>" + toastParam + "</wp:Param>" +
               "</wp:Toast> " +
            "</wp:Notification>";

            return SendPushNotification(NotificationTypeEnum.Toast, subscriber, toastNotification, (int)intervalValue);
        }

        public PushNotificationResponse PushRaw(SPPushNotificationSubscriber subscriber, string rawMessage, RawIntervalValuesEnum intervalValue)
        {
            return SendPushNotification(NotificationTypeEnum.Raw, subscriber, rawMessage, (int)intervalValue);
        }

        private PushNotificationResponse SendPushNotification(NotificationTypeEnum notificationType, SPPushNotificationSubscriber subscriber, string message, int intervalValue)
        {
            // Create HTTP Web Request object.
            string subscriptionUri = subscriber.ServiceToken;
            HttpWebRequest sendNotificationRequest = (HttpWebRequest)WebRequest.Create(subscriptionUri);

            // MPNS expects a byte array, so convert message accordingly.
            byte[] notificationMessage = Encoding.Default.GetBytes(message);
            
            // Set the notification request properties.
            sendNotificationRequest.Method = WebRequestMethods.Http.Post;
            sendNotificationRequest.ContentLength = notificationMessage.Length;
            sendNotificationRequest.ContentType = "text/xml";
            sendNotificationRequest.Headers.Add("X-MessageID", Guid.NewGuid().ToString());

            switch (notificationType)
            {
                case NotificationTypeEnum.Tile:
                    sendNotificationRequest.Headers.Add("X-WindowsPhone-Target", "token");
                    break;
                case NotificationTypeEnum.Toast:
                    sendNotificationRequest.Headers.Add("X-WindowsPhone-Target", "toast");
                    break;
                case NotificationTypeEnum.Raw:
                    // A value for the X-WindowsPhone-Target header is not specified for raw notifications.
                    break;
            }            

            sendNotificationRequest.Headers.Add("X-NotificationClass", intervalValue.ToString());

            // Merge byte array payload with headers.
            using (Stream requestStream = sendNotificationRequest.GetRequestStream())
            {
                requestStream.Write(notificationMessage, 0, notificationMessage.Length);
            }

            string statCode = string.Empty;
            PushNotificationResponse notificationResponse;

            try
            {
                // Send the notification and get the response.
                HttpWebResponse response = (HttpWebResponse)sendNotificationRequest.GetResponse();
                statCode = Enum.GetName(typeof(HttpStatusCode), response.StatusCode);

                // Create PushNotificationResponse object.
                notificationResponse = new PushNotificationResponse((int)intervalValue, subscriber.ServiceToken);
                notificationResponse.StatusCode = statCode;
                foreach (string header in WP7Constants.WP_RESPONSE_HEADERS)
                {
                    notificationResponse.Properties[header] = response.Headers[header];
                }                
            }
            catch (Exception ex)
            {
                statCode = ex.Message;
                notificationResponse = new PushNotificationResponse((int)intervalValue, subscriber.ServiceToken);
                notificationResponse.StatusCode = statCode;
            }

            return notificationResponse;
        }
    }     

    /// <summary>
    /// Object used for returning notification request results.
    /// </summary>
    class PushNotificationResponse
    {
        private DateTime timestamp;
        private int notificationIntervalValue;
        private string statusCode = string.Empty;
        private string serviceToken;
        private Dictionary<string, string> properties;

        public PushNotificationResponse(int numericalIntervalValue, string srvcToken)
        {
            timestamp = DateTime.UtcNow;
            notificationIntervalValue = numericalIntervalValue;
            serviceToken = srvcToken;
            properties = new Dictionary<string, string>();
        }

        public DateTime TimeStamp
        {
            get { return timestamp; }
        }

        public int NotificationIntervalValue
        {
            get { return notificationIntervalValue; }
        }

        public string StatusCode
        {
            get { return statusCode; }
            set { statusCode = value; }
        }

        public string ServiceToken
        {
            get { return serviceToken; }
        }

        public Dictionary<string, string> Properties
        {
            get { return properties; }
        }
    }
}
```

5. Сохраните файл.
    
  
В этом коде методы **PushToast** и **PushRaw** принимать аргументы параметра, подходящую для заданного типа уведомлений для отправки, обработки этих аргументов и затем вызвать метод **SendPushNotification**, который не отправки уведомлений, с помощью службы Push-уведомления Майкрософт. (В этом примере кода метод для отправки уведомлений заголовков не реализован.) Класс **PushNotificationResponse** является просто механизм инкапсуляции результатов, полученных от запрос уведомления. Здесь класс добавляет некоторые данные на объект (приведения как объект **HttpWebResponse** ), возвращенный методом **GetResponse** объекта **HttpWebRequest**. Приемник событий, создаваемые в следующей процедуре использует этот класс **PushNotificationResponse** обновить список результатов уведомления на сервере.
  
    
    
Теперь создайте класс приемника событий, который будет отправлять push-уведомлений для устройств, которые зарегистрированы в качестве получателей их. (Привязка этот приемника событий в список заданий, созданный во время следующей процедуры будет.)
  
    
    

### <a name="to-create-the-event-receiver-class-for-a-list"></a>Чтобы создать класс приемника событий для списка


1. В **Обозревателе решений** выберите узел, представляющий проект.
    
  
2. В меню **проект** выберите пункт **Добавление класса**. Откроется диалоговое окно **Добавление нового элемента** с шаблоном C# **класс** уже выбраны.
    
  
3. Укажите ListItemEventReceiver.cs в качестве имени файла и нажмите кнопку **Добавить**. Файл класса добавляется в решение и открывается для редактирования.
    
  
4. Замените содержимое файла следующим кодом.
    
```cs
  
using System;
using System.Security.Permissions;
using System.Text;
using Microsoft.SharePoint;
using Microsoft.SharePoint.Utilities;

namespace PushNotificationsList
{
    /// <summary>
    /// List Item Events
    /// </summary>
    public class ListItemEventReceiver : SPItemEventReceiver
    {
        internal static string ResultsList = "Push Notification Results";

        /// <summary>
        /// An item was added.
        /// </summary>
        public override void ItemAdded(SPItemEventProperties properties)
        {
            SPWeb spWeb = properties.Web;
            SPPushNotificationSubscriberCollection pushSubscribers = spWeb.PushNotificationSubscribers;
            PushNotification pushNotification = new PushNotification();

            SPListItem listItem = properties.ListItem;

            string jobAssignment = "[Unassigned]";

            // This event receiver is intended to be associated with a specific list,
            // but the list may not have an "AssignedTo" field, so using try/catch here.
            try
            {
                jobAssignment = listItem["AssignedTo"].ToString();
            }
            catch { }

            PushNotificationResponse pushResponse = null;

            foreach (SPPushNotificationSubscriber ps in pushSubscribers)
            {
                // Send a toast notification to be displayed on subscribed phones on which the app is not running.
                pushResponse = pushNotification.PushToast(ps, "New job for:", jobAssignment, string.Empty, ToastIntervalValuesEnum.ImmediateToast);
                UpdateNotificationResultsList(spWeb, ps.User.Name, pushResponse);

                // Also send a raw notification to be displayed on subscribed phones on which the app is running when the item is added.
                pushResponse = pushNotification.PushRaw(ps, string.Format("New job for: {0}", jobAssignment), RawIntervalValuesEnum.ImmediateRaw);
                UpdateNotificationResultsList(spWeb, ps.User.Name, pushResponse);
            }

            base.ItemAdded(properties);
        }

        private void UpdateNotificationResultsList(SPWeb spWeb, string subscriberName, PushNotificationResponse pushResponse)
        {
            SPList resultsList = spWeb.Lists.TryGetList(ResultsList);

            if (resultsList == null)
                return;

            try
            {
                SPListItem resultItem = resultsList.Items.Add();
                resultItem["Title"] = subscriberName;
                resultItem["Notification Time"] = pushResponse.TimeStamp;
                resultItem["Status Code"] = pushResponse.StatusCode;
                resultItem["Service Token"] = pushResponse.ServiceToken;

                StringBuilder builder = new StringBuilder();
                foreach (string key in pushResponse.Properties.Keys)
                {
                    builder.AppendFormat("{0}: {1}; ", key, pushResponse.Properties[key]);
                }
                resultItem["Headers"] = builder.ToString();

                resultItem["Interval Value"] = pushResponse.NotificationIntervalValue;
                resultItem.Update();
            }
            catch
            {
                // Could log to ULS here if adding list item fails.
            }
        }
    }
}
```

5. Сохраните файл.
    
  
В этом коде после добавления элемента в список, к которому сделана привязка приемника событий, push-уведомления отправляются подписчикам, зарегистрированные для получения уведомлений. Значение поля Кому назначено из элемента добавлен список включен в сообщение уведомления отправляются подписчикам. Всплывающее уведомление для значения параметра **toastTitle** (для метода **PushToast**, определенных в предыдущей процедуре) и параметр **toastMessage** устанавливаются. Эти значения соответствуют свойства **Text1** и **Text2** в XML-схему, определяющую всплывающим уведомлений.
  
    
    
Пустая строка просто передается в качестве значения параметра **toastParam**, которой соответствует свойству **Param** в XML-схему для уведомлений всплывающего уведомления. Этот параметр может использоваться для указания, например, на страницу приложения phone следует открыть при нажатии кнопки уведомлений на телефоне. В примере приложения телефона, разработанных далее в этом разделе для получения этих уведомлений с сервера свойство **Param** не используется. Форма списка (List.xaml) в приложении просто открывается при нажатии кнопки уведомления.
  
    
    

> **Примечание:** Свойства **параметров** для уведомлений всплывающим поддерживается только в ОС Windows Phone 7.1 или более поздней версии.
  
    
    

Для необработанного уведомления в этом примере передается строка, содержащее значение поля Кому назначено из элемента добавлен список.
  
    
    
Обратите внимание, что всплывающее уведомление будет отображаться на на рассылку телефоны (если не работает приложение телефон, для которого предназначено уведомления) и будет усечено сообщение, отображаемое при более приблизительно 41 символов. Необработанные уведомлений в MPNS не более 1024 байта (1 КБ). (Точное число знаков, которые могут быть отправлены зависит от типа кодировки, применяемой, такие как UTF-8). Плитка уведомления также могут быть ограничения на размер. Не удается отправить больших объемов данных с помощью любого из типов уведомлений. Рекомендации по использованию этих уведомлений не как механизм для передачи данных, но как способ отправки короткий на рассылку телефоны, таким образом, могут быть выполнены определенные действия на телефоне. Эти действия, такие как обновление списка на телефоне с данными на сервере, может включать в себя большие объемы данных, в зависимости от структуры приложения Windows Phone.
  
    
    
Объект **PushNotificationResponse**, которое возвращается из запрос уведомления передается методу **UpdateNotificationResultsList**. Этот метод добавляет сведения о запросе в список SharePoint с именем результаты Push-уведомлений (если существует списка). Это просто демонстрационный одним из способов использования возвращенного объекта. Для более сложных используется в производственной решения можно размещать возвращенного объекта. К примеру, может изучить возвращенного объекта для определенного состояния коды при отправке уведомления для определенного пользователя (например, пользователь, предназначенный для назначения в поле Кому назначено) и выполните необходимые действия. В реальном приложении вероятно, не сохраните эти данные в виде списка на сервере. Данные, хранятся здесь помогут вам понять свойства, связанные с MPNS уведомления.
  
    
    
Создайте простой список SharePoint, с именем задания, содержащее категории заданий, описание задания и лицо, которому назначена задания. Кроме того создайте дополнительный список, с именем результаты Push-уведомления для хранения сведений о запросах уведомления отправляются подписчикам телефоны.
  
    
    
В следующей процедуре создайте класс, **ListCreator**, включающий метод **CreateJobsList** для создания и настройки в списке заданий при активации решения на сервере. Класс также добавляет приемника событий **ItemAdded** (созданный ранее в класс **ListItemEventReceiver** ) в коллекцию **EventReceivers**, связанный со списком. Класс **ListCreator** также включает метод для создания списка Push-уведомлений результаты SharePoint.
  
    
    

### <a name="to-create-a-class-for-adding-and-configuring-the-lists"></a>Создание класса для добавления и настройки списков


1. В **Обозревателе решений** выберите узел, представляющий проект (еще раз, именованныеPushNotificationsList Если вы следуете соглашению об именовании, которое используется в данном разделе).
    
  
2. В меню **проект** выберите пункт **Добавление класса**. Откроется диалоговое окно **Добавление нового элемента** с шаблоном C# **класс** уже выбраны.
    
  
3. Укажите ListCreator.cs в качестве имени файла и нажмите кнопку **Добавить**. Файл класса добавляется в решение и открывается для редактирования.
    
  
4. Замените содержимое файла следующим кодом.
    
```cs
  
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Xml;
using Microsoft.SharePoint;

namespace PushNotificationsList
{
    class ListCreator
    {
        internal void CreateJobsList(SPWeb spWeb)
        {
            string listTitle = "Jobs";
            string listDescription = "List of jobs and assignments.";
            Dictionary<string, SPFieldType> columns = new Dictionary<string, SPFieldType>();

            // The "Title" column will be added based on the GenericList template. That field
            // will be used as the category name for the job (e.g., Shopping), so only need to add
            // the remaining fields.
            columns.Add("Description", SPFieldType.Text);
            columns.Add("AssignedTo", SPFieldType.Text);

            // Creating list (or retrieving GUID for list if it already exists).
            Guid listId = CreateCustomList(spWeb, listTitle, listDescription, columns, false);
            if (listId.Equals(Guid.Empty))
                return;

            SPList list = spWeb.Lists[listId];

            // Add event receiver (if the current Jobs list is not already associated with the receiver).
            bool ReceiverExists = false;
            string receiverClassName = "PushNotificationsList.ListItemEventReceiver";

            for (int i = 0; i < list.EventReceivers.Count; i++)
            {
                SPEventReceiverDefinition rd = list.EventReceivers[i];
                if (rd.Class == receiverClassName &amp;&amp; rd.Type == SPEventReceiverType.ItemAdded)
                {
                    ReceiverExists = true;
                    break;
                }
            }

            if (ReceiverExists == false)
            {
                SPEventReceiverDefinition eventReceiver = list.EventReceivers.Add();
                // Must specify information here for this specific assembly.
                eventReceiver.Assembly = "PushNotificationsList,
                    Version=1.0.0.0, Culture=Neutral,
                    PublicKeyToken=[YOUR TOKEN VALUE HERE]";
                eventReceiver.Class = receiverClassName;
                eventReceiver.Name = "ItemAdded Event";
                eventReceiver.Type = SPEventReceiverType.ItemAdded;
                eventReceiver.SequenceNumber = 10000;
                eventReceiver.Synchronization = SPEventReceiverSynchronization.Synchronous;
                eventReceiver.Update();
            }
        }

        internal void CreateNotificationResultsList(SPWeb spWeb)
        {
            string listTitle = "Push Notification Results";
            string listDescription = "List for results from push notification operations.";

            Dictionary<string, SPFieldType> columns = new Dictionary<string, SPFieldType>();
            columns.Add("Notification Time", SPFieldType.Text);
            columns.Add("Status Code", SPFieldType.Text);
            columns.Add("Service Token", SPFieldType.Text);
            columns.Add("Headers", SPFieldType.Text);
            columns.Add("Interval Value", SPFieldType.Integer);

            // Creating the list for storing notification results.
            CreateCustomList(spWeb, listTitle, listDescription, columns, true);
        }

        /// <summary>
        /// Creates a SharePoint list (based on the Generic List template).
        /// </summary>
        /// <param name="spWeb">The target Web site for the list.</param>
        /// <param name="listTitle">The title of the list.</param>
        /// <param name="listDescription">A description for the list.</param>
        /// <param name="columns">A Dictionary object containing field names and types.</param>
        /// <param name="replaceExistingList">Indicates whether to overwrite an existing list of the same name on the site.</param>
        /// <returns>A GUID for the created (or existing) list.</returns>
        internal Guid CreateCustomList(SPWeb spWeb, string listTitle, string listDescription, Dictionary<string, SPFieldType> columns, bool replaceExistingList)
        {
            SPList list = spWeb.Lists.TryGetList(listTitle);

            if (list != null)
            {
                if (replaceExistingList == true)
                {
                    try
                    {
                        list.Delete();
                    }
                    catch
                    {
                        return Guid.Empty;
                    }
                }
                else
                {
                    return list.ID;
                }
            }

            try
            {
                Guid listId = spWeb.Lists.Add(listTitle, listDescription, SPListTemplateType.GenericList);
                list = spWeb.Lists[listId];
                SPView view = list.DefaultView;

                foreach (string key in columns.Keys)
                {
                    list.Fields.Add(key, columns[key], false);
                    view.ViewFields.Add(key);
                }
                
                list.Update();
                view.Update();

                return listId;
            }
            catch
            {
                return Guid.Empty;
            }
        }
    }
}
```


    Be sure to specify the appropriate Public Key Token value for particular your assembly. To add a tool to Visual Studio for getting the Public Key Token value for your assembly, see  [How to: Create a Tool to Get the Public Key of an Assembly](http://msdn.microsoft.com/en-us/library/ee539398.aspx) in the MSDN Library. Note that you will have to compile your project at least once to be able to get the Public Key Token value for your output assembly.
    
  
5. Сохраните файл.
    
  
В этом примере кода метод **CreateJobsList** класса **ListCreator** создает список (или получает список, если он существует на сервере) и связывает приемника событий, созданные в предыдущей процедуре, в список, добавив в класс **EventReceivers**, связанный со списком. Метод **CreateNotificationResultsList** создает список результатов Push-уведомлений.
  
    
    
Рассмотрим добавления компонента в проект для выполнения операций инициализации на сервере при развертывании и активации решения. Добавление класса приемника событий в компонент для обработки событий, **FeatureActivated** и **FeatureDeactivating**.
  
    
    

### <a name="to-add-a-feature-to-your-project"></a>Добавление компонента в проект


1. В Visual Studio 2012, в меню **Вид** выберите **Другие окна** и выберите **Обозреватель пакетов**.
    
  
2. В окне **Обозреватель пакетов**, щелкните правой кнопкой мыши узел, представляющий проект и выберите команду **Добавить компонент**. Новая функция (с именем "Feature1" по умолчанию) добавляется в проект под узлом **функции** (в **Окне Обозреватель решений** ).
    
  
3. Теперь в **Обозревателе решений** разверните узел **компоненты** и щелкните правой кнопкой мыши только что добавленный компонент (то есть, **Feature1** ) и нажмите кнопку **Добавить приемник событий**. Файл класса приемника событий (Feature1.EventReceiver.cs) добавляется в компонент и открывается для редактирования.
    
  
4. В реализации (обозначенного открывающих и закрывающих скобок) класса **Feature1EventReceiver** добавьте следующий код.
    
```cs
  
internal const string PushNotificationFeatureId = "41E1D4BF-B1A2-47F7-AB80-D5D6CBBA3092";
```


    This string variable stores the identifier for the Push Notification Feature on the server.
    
    > **Tip:**
      > You can obtain a list of unique identifiers for the Features on a SharePoint Server by executing the following Windows PowerShell cmdlet: >  `Get-SPFeature | Sort -Property DisplayName`> The Push Notification Feature appears as "PhonePNSubscriber" in the results returned by this cmdlet. 
5. Файл класса приемника событий создается с некоторые объявления метода по умолчанию для обработки событий компонента. Изначально объявления метода в файле закомментированы. Замените метод **FeatureActivated** в файл следующий код.
    
```cs
  public override void FeatureActivated(SPFeatureReceiverProperties properties)
{
    base.FeatureActivated(properties);
    SPWeb spWeb = (SPWeb)properties.Feature.Parent;

    ListCreator listCreator = new ListCreator();
    listCreator.CreateJobsList(spWeb);
    listCreator.CreateNotificationResultsList(spWeb);

    // Then activate the Push Notification Feature on the server.
    // The Push Notification Feature is not activated by default in a SharePoint Server installation.
    spWeb.Features.Add(new Guid(PushNotificationFeatureId), false);
}
```

6. Замените метод **FeatureDeactivating** в файл следующий код.
    
```cs
  
public override void FeatureDeactivating(SPFeatureReceiverProperties properties)
{
    base.FeatureDeactivating(properties);
    SPWeb spWeb = (SPWeb)properties.Feature.Parent;

    // Deactivate the Push Notification Feature on the server
    // when the PushNotificationsList Feature is deactivated.
    spWeb.Features.Remove(new Guid(PushNotificationFeatureId), false);
}
```

7. Сохраните файл.
    
  
В реализации обработчик события **FeatureActivated** создается экземпляр класса **ListCreator** и его **CreateJobsList** и **CreateNotificationResultsList** методы вызываются с помощью **SPWeb**, где развернуть и активировать компонент как расположение, в котором будут создаваться списков. Кроме того поскольку push notification функциональность не включена по умолчанию в стандартной установке SharePoint Server, обработчика событий Активация компонента Push-уведомлений на сервере. В обработчике событий **FeatureDeactivating** функциональные возможности push notification деактивирован, когда приложения были отключены. Нет необходимости обрабатывать это событие. Может или не может потребоваться отключение push-уведомлений на сервере при отключении приложения, в зависимости от условиях установки и ли других приложений в целевом веб-сайтов сделать используйте push-уведомлений.
  
    
    

## <a name="create-a-windows-phone-sharepoint-list-app-to-receive-push-notifications"></a>Создание приложения списка SharePoint для Windows Phone для приема push-уведомлений
<a name="BKMK_NotificationPhoneApp"> </a>

В этом разделе создается приложение Windows Phone на основе шаблона приложения списка SharePoint для Windows Phone, указание список SharePoint, созданный в предыдущем разделе как целевого списка для приложения. Затем разрабатывать класс **Notifications** для подписки на push-уведомления, реализация обработчики для событий уведомления и хранения данных, связанных с уведомления на телефоне. Также добавьте XAML-страницы в приложении с помощью элементов управления, чтобы разрешить пользователям регистрации или отмены регистрации push-уведомлений.
  
    
    
Для выполнения процедур, описанных в этом разделе, сначала выполните действия, описанные в процедуре, описанной в [как: Создание приложения списка SharePoint для Windows Phone](how-to-create-a-windows-phone-sharepoint-list-app.md) для создания проекта Visual Studio с помощью шаблона приложения списка SharePoint для Windows Phone с помощью заданий список, созданный в предыдущем разделе в качестве целевого списка SharePoint для проекта. В целях процедур, описанных в этом разделе предполагается, что имя, определенное для isSPListAppForNotifications проекта.
  
    
    

### <a name="to-create-the-class-for-managing-subscriptions-and-received-notifications"></a>Создание класса для управления подписками и принимаемыми уведомлениями


1. В **Обозревателе решений** выберите узел, представляющий проект (с именемSPListAppForNotifications).
    
  
2. В меню **проект** выберите пункт **Добавление класса**. Откроется диалоговое окно **Добавление нового элемента** с шаблоном C# **класс** уже выбраны.
    
  
3. Укажите «Notifications.cs» в качестве имени файла и нажмите кнопку **Добавить**. Файл класса добавляется в решение и открывается для редактирования.
    
  
4. Замените содержимое файла следующим кодом.
    
```cs
  
using System;
using System.Linq;
using System.Net;
using System.Windows;
using Microsoft.Phone.Notification;
using Microsoft.SharePoint.Client;
using System.Diagnostics;
using System.Collections.Generic;
using Microsoft.Phone.Shell;
using System.IO;
using System.IO.IsolatedStorage;

namespace SPListAppForNotifications
{
    public class Notifications
    {
        static HttpNotificationChannel httpChannel;
        private const string RegStatusKey = "RegistrationStatus";
        public static string DeviceAppIdKey = "DeviceAppInstanceId";
        public static string ChannelName = "JobsListNotificationChannel";
        public static ClientContext Context { get; set; }

        public static void OpenNotificationChannel(bool isInitialRegistration)
        {
            try
            {
                // Get channel if it was created in a previous session of the app.
                httpChannel = HttpNotificationChannel.Find(ChannelName);

                // If channel is not found, create one.
                if (httpChannel == null)
                {
                    httpChannel = new HttpNotificationChannel(ChannelName);

                    // Add event handlers. When the Open method is called, the ChannelUriUpdated event will fire.
                    // A call is made to the SubscribeToService method in the ChannelUriUpdated event handler.                    
                    AddChannelEventHandlers();
                    httpChannel.Open();
                }
                else
                {
                    // The channel exists and is already open. Add handlers for channel events.
                    // The ChannelUriUpdated event won't fire in this case.
                    AddChannelEventHandlers();

                    // If app instance is registering for first time
                    // (instead of just starting up again), then call SubscribeToService.
                    if (isInitialRegistration)
                    {
                        SubscribeToService();
                    }
                }
            }
            catch (Exception ex)
            {                
                ShowMessage(ex.Message, "Error Opening Channel");
                CloseChannel();
            }
        }

        private static void AddChannelEventHandlers()
        {
            httpChannel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(httpChannel_ChannelUriUpdated);
            httpChannel.ErrorOccurred += new EventHandler<NotificationChannelErrorEventArgs>(httpChannel_ExceptionOccurred);
            httpChannel.ShellToastNotificationReceived += new EventHandler<NotificationEventArgs>(httpChannel_ShellToastNotificationReceived);
            httpChannel.HttpNotificationReceived += new EventHandler<HttpNotificationEventArgs>(httpChannel_HttpNotificationReceived);
        }

        private static void httpChannel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            UpdateChannelUriOnServer();
            SubscribeToService();
        }

        private static void httpChannel_ExceptionOccurred(object sender, NotificationChannelErrorEventArgs e)
        {
            // Simply showing the exception error.
            ShowMessage(e.Message, "Channel Event Error");
        }

        static void httpChannel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            if (e.Collection != null)
            {
                Dictionary<string, string> collection = (Dictionary<string, string>)e.Collection;
                ShellToast toast = new ShellToast();
                toast.Title = collection["wp:Text1"];
                toast.Content = collection["wp:Text2"];

                // Note that the Show method for a toast notification won't
                // display the notification in the UI of the phone when the app
                // that calls the method is running (as the foreground app on the phone).
                // toast.Show();
               //Toast and Raw notification will be displayed if user is running the app. Be default only Toast notification
               // will be displayed when the app is tombstoned                                               

                // Showing the toast notification with the ShowMessage method.
                ShowMessage(string.Format("Title: {0}\\r\\nContent: {1}", toast.Title, toast.Content), "Toast Notification");
            }
        }

        static void httpChannel_HttpNotificationReceived(object sender, HttpNotificationEventArgs e)
        {
            Stream messageStream = e.Notification.Body;
            string message = string.Empty;

            // Replacing NULL characters in stream.
            using (var reader = new StreamReader(messageStream))
            {
                message = reader.ReadToEnd().Replace('\\0', ' ');
            }

            // Simply displaying the raw notification.
            ShowMessage(message, "Raw Notification");
        }

        private static void SubscribeToService()
        {
            Guid deviceAppInstanceId = GetSettingValue<Guid>(DeviceAppIdKey, false);

            Context.Load(Context.Web, w => w.Title, w => w.Description);

            PushNotificationSubscriber pushSubscriber = Context.Web.RegisterPushNotificationSubscriber(deviceAppInstanceId, httpChannel.ChannelUri.AbsoluteUri);

            Context.Load(pushSubscriber);

            Context.ExecuteQueryAsync
                (
                    (object sender, ClientRequestSucceededEventArgs args) =>
                        {
                            SetRegistrationStatus(true);

                            // Indicate that tile and toast notifications can be
                            // received by phone shell when phone app is not running.
                            if (!httpChannel.IsShellTileBound)
                                httpChannel.BindToShellTile();

                            if (!httpChannel.IsShellToastBound)
                                httpChannel.BindToShellToast();

                            ShowMessage(
                                string.Format("Subscriber successfully registered: {0}", pushSubscriber.User.LoginName),
                                "Success");
                        },
                    (object sender, ClientRequestFailedEventArgs args) =>
                        {
                            ShowMessage(args.Exception.Message, "Error Subscribing");
                        });
        }

        private static void UpdateChannelUriOnServer()
        {
            Guid deviceAppInstanceId = GetSettingValue<Guid>(DeviceAppIdKey, false);

            Context.Load(Context.Web, w => w.Title, w => w.Description);            

            PushNotificationSubscriber subscriber = Context.Web.GetPushNotificationSubscriber(deviceAppInstanceId);

            Context.Load(subscriber);

            Context.ExecuteQueryAsync(
                    (object sender1, ClientRequestSucceededEventArgs args1) =>
                    {
                        subscriber.ServiceToken = httpChannel.ChannelUri.AbsolutePath;
                        subscriber.Update();
                        Context.ExecuteQueryAsync(
                            (object sender2, ClientRequestSucceededEventArgs args2) =>
                                {
                                    ShowMessage("Channel URI updated on server.", "Success");
                                },
                            (object sender2, ClientRequestFailedEventArgs args2) =>
                                {
                                    ShowMessage(args2.Exception.Message, "Error Upating Channel URI");
                                });
                    },
                   (object sender1, ClientRequestFailedEventArgs args1) =>
                   {
                       // This condition can be ignored. Getting to this point means the subscriber
                       // doesn't yet exist on the server, so updating the Channel URI is unnecessary.
                       //ShowMessage("Subscriber doesn't exist on server.", "DEBUG");
                   });
        }

        public static void UnSubscribe()
        {
            Context.Load(Context.Web, w => w.Title, w => w.Description);
            Guid deviceAppInstanceId = GetSettingValue<Guid>(DeviceAppIdKey, false);

            Context.Web.UnregisterPushNotificationSubscriber(deviceAppInstanceId);

            Context.ExecuteQueryAsync
                (
                    (object sender, ClientRequestSucceededEventArgs args) =>
                    {
                        CloseChannel();
                        SetRegistrationStatus(false);
                        //SetInitializationStatus(false);
                        ShowMessage("Subscriber successfully unregistered.", "Success");
                    },
                    (object sender, ClientRequestFailedEventArgs args) =>
                    {
                        ShowMessage(args.Exception.Message, "Error Unsubscribing");
                    });
        }

        public static void ClearSubscriptionStore()
        {
            Context.Load(Context.Web, w => w.Title, w => w.Description);
            List subscriptionStore = Context.Web.Lists.GetByTitle("Push Notification Subscription Store");
            Context.Load(subscriptionStore);
            ListItemCollection listItems = subscriptionStore.GetItems(new CamlQuery());
            Context.Load(listItems);

            Context.ExecuteQueryAsync
                (
                    (object sender1, ClientRequestSucceededEventArgs args1) =>
                    {
                        foreach (ListItem listItem in listItems.ToList())
                        {
                            listItem.DeleteObject();                            
                        }                        
                        Context.ExecuteQueryAsync(
                                (object sender2, ClientRequestSucceededEventArgs args2) =>
                                {
                                    // Close channel if open and set registration status for current app instance.
                                    CloseChannel();
                                    SetRegistrationStatus(false);

                                    ShowMessage("Subscriber store cleared.", "Success");
                                },
                                (object sender2, ClientRequestFailedEventArgs args2) =>
                                {
                                    ShowMessage(args2.Exception.Message, "Error Deleting Subscribers");
                                });
                    },
                    (object sender1, ClientRequestFailedEventArgs args1) =>
                    {
                        ShowMessage(args1.Exception.Message, "Error Loading Subscribers List");
                    });
        }

        private static void CloseChannel()
        {
            if (httpChannel == null) return;
            try
            {
                httpChannel.UnbindToShellTile();
                httpChannel.UnbindToShellToast();
                httpChannel.Close();
            }
            catch (Exception ex)
            {
                ShowMessage(ex.Message, "Error Closing Channel");
            }
        }

        public static void SaveDeviceAppIdToStorage()
        {
            if (!IsolatedStorageSettings.ApplicationSettings.Contains(DeviceAppIdKey))
            {
                Guid DeviceAppId = Guid.NewGuid();
                SetSettingValue<Guid>(DeviceAppIdKey, DeviceAppId, false);
            }
        }

        public static bool GetRegistrationStatus()
        {
            bool status = GetSettingValue<bool>(RegStatusKey, false);
            return status;
        }

        private static void SetRegistrationStatus(bool isRegistered)
        {
            SetSettingValue<bool>(RegStatusKey, isRegistered, false);
        }

        private static T GetSettingValue<T>(string key, bool fromTransientStorage)
        {
            if (fromTransientStorage == false)
            {
                if (IsolatedStorageSettings.ApplicationSettings.Contains(key))
                    return (T)IsolatedStorageSettings.ApplicationSettings[key];
                return default(T);
            }

            if (PhoneApplicationService.Current.State.ContainsKey(key))
                return (T)PhoneApplicationService.Current.State[key];
            return default(T);
        }

        private static void SetSettingValue<T>(string key, T value, bool toTransientStorage)
        {
            if (toTransientStorage == false)
            {
                if (IsolatedStorageSettings.ApplicationSettings.Contains(key))
                    IsolatedStorageSettings.ApplicationSettings[key] = value;
                else
                    IsolatedStorageSettings.ApplicationSettings.Add(key, value);

                IsolatedStorageSettings.ApplicationSettings.Save();
            }
            else
            {
                if (PhoneApplicationService.Current.State.ContainsKey(key))
                    PhoneApplicationService.Current.State[key] = value;
                else
                    PhoneApplicationService.Current.State.Add(key, value);
            }
        }

        // Method for showing messages on UI thread coming from a different originating thread.
        private static void ShowMessage(string message, string caption)
        {
            Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show(message, caption, MessageBoxButton.OK);
            });
        }
    }
}
```

5. Сохраните файл.
    
  
В этом примере кода **OpenNotificationChannel** создает уведомления для получения уведомлений в MPNS. Обработчики событий подключены к объекту канала реагирования на события уведомления, а затем открытия канала. В этом примере реализуется события **HttpNotificationReceived** (для получения уведомлений о необработанных). Необработанные уведомления могут быть получены только при запуске приложения телефона. Обработчик для события **ShellToastNotificationReceived** (для получения уведомлений об всплывающего уведомления) также реализован здесь его применения. Плитка уведомления могут быть получены только при подписки приложение телефон не выполняется, поэтому нет необходимости для реализации обработчика событий в приложении для получения уведомлений об заголовков.
  
    
    
Метод **SubscribeToService** выполняет метод **RegisterPushNotificationSubscriber** объекта **SPWeb** асинхронно (передачи значение, определяющее приложение телефон и значение URI связан с канала уведомлений) для регистрации в SharePoint Server для приема push-уведомлений. При успешном регистрации Windows Phone, имеет значение командной консоли для получения (и отображения) всплывающих и уведомления по каналу уведомление, зарегистрированных в SharePoint Server при самом приложении телефон не работает на плитке.
  
    
    
Метод **UnSubscribe** в этот код вызывает метод **UnregisterPushNotificationSubscriber** объекта SPWeb. Рекомендации по разработке приложений Windows Phone рекомендуем пользователям разрешено запрос для подписки на push-уведомления или нет. Во время следующей процедуры будет добавлен механизм пользователя для регистрации или отмены регистрации для уведомлений и текущем состоянии регистрации сохраняются между сеансами приложения, устраняя необходимость попросите для регистрации каждый раз при запуске приложения. Метод **GetRegistrationStatus** можно сделать доступной, чтобы приложение телефон можно определить ли пользователь был зарегистрирован (во время предыдущего сеанса) для приема push-уведомлений и впоследствии открытия канала уведомлений. **SaveDeviceAppIdToStorage** сохраняет идентификатор (представляются как код GUID) для экземпляра приложения на указанной Windows Phone для изолированного хранения.
  
    
    
Метод **ClearSubscriptionStore** включен здесь в качестве демонстрации одним из способов очистки подписчики из хранилища подписок на SharePoint Server. Подписчики на push-уведомлений, хранятся в список SharePoint с именем «Хранилища подписок Push Notification». Кнопка для вызова этого метода в класс **Notifications** добавляется на страницу параметров уведомлений, добавлены в приложение во время следующей процедуры.
  
    
    
Обратите внимание на то, что операций на доступ к SharePoint Server для настройки параметров или подготовки уведомления (например, метод **RegisterPushNotificationSubscriber** ) может потребоваться времени в зависимости от условий сети и доступности сервера. Эти операции таким образом, выполняются асинхронно (в частности, с помощью метода **ExecuteQueryAsync** объекта **ClientContext** ) чтобы разрешить приложение для продолжения других процессов и поддержания пользовательского интерфейса реагирует на пользователя.
  
    
    
Теперь добавьте страницу приложения с элементами управления, которые позволяют пользователю зарегистрировать или отменить регистрацию в push-уведомлений с сервера.
  
    
    

### <a name="to-add-a-notification-settings-page-to-the-app"></a>Для добавления на страницу Параметры уведомлений для приложения


1. В **Обозревателе решений** выберите узел, представляющий проект (с именемSPListAppForNotifications , если вы следуете соглашение об именовании в этих процедурах).
    
  
2. В меню **проект** выберите команду **Добавить новый элемент**. Откроется диалоговое окно **Добавление нового элемента**.
    
  
3. В области **Шаблоны** выберите шаблон **Страницы Книжная Windows Phone**. Укажите Settings.xaml в качестве имени файла для этой страницы и нажмите кнопку **Добавить**. Страница будет добавлен в проект и открыт для редактирования.
    
  
4. В представлении XAML для страницы замените содержимое между закрывающая скобка тега XML, который определяет элемент **PhoneApplicationPage** и закрывающего тега элемента ( `</phone:PhoneApplicationPage>`) следующую разметку.
    
```
  
<Grid x:Name="LayoutRoot" Background="Transparent">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*"/>
    </Grid.RowDefinitions>

    <!--TitlePanel contains the name of the application and page title-->
    <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
        <TextBlock x:Name="ApplicationTitle" Text="JOBS LIST" Style="{StaticResource PhoneTextNormalStyle}"/>
        <TextBlock x:Name="PageTitle" Text="Settings" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
    </StackPanel>

    <!--ContentPanel - place additional content here-->
    <Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
        <StackPanel Margin="0,5,0,5">
            <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                <TextBlock TextWrapping="Wrap" HorizontalAlignment="Center" Style="{StaticResource PhoneTextTitle2Style}">Notification Registration</TextBlock>
                <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                    <TextBlock x:Name="txtRegistrationStatus" TextWrapping="Wrap" HorizontalAlignment="Center" Text="Registered: No" Style="{StaticResource PhoneTextAccentStyle}" Foreground="{StaticResource PhoneAccentBrush}" />
                    <Button x:Name="btnRegister" Content="Register" Height="71" Width="260" Click="OnRegisterButtonClick" />
                    <Button x:Name="btnUnregister" Content="Unregister" Height="71" Width="260" Click="OnUnregisterButtonClick" />
                </StackPanel>
            </StackPanel>
            <StackPanel Orientation="Vertical" Margin="0,5,0,5">
                <TextBlock TextWrapping="Wrap" HorizontalAlignment="Center" Style="{StaticResource PhoneTextTitle2Style}">Subscriber Management</TextBlock>
                <Button x:Name="btnDeleteSubscribers" Content="Delete Subscribers" Height="71" Width="260" Click="OnDeleteSubscribersButtonClick" />
            </StackPanel>
        </StackPanel>
    </Grid>
</Grid>
 
<!--Sample code showing usage of ApplicationBar-->
<phone:PhoneApplicationPage.ApplicationBar>
    <shell:ApplicationBar IsVisible="True" IsMenuEnabled="False">
        <shell:ApplicationBarIconButton x:Name="btnOK" IconUri="/Images/appbar.check.rest.png" Text="OK" Click="OnOKButtonClick" />
    </shell:ApplicationBar>
</phone:PhoneApplicationPage.ApplicationBar>
```

5. С помощью файла Settings.xaml, выбранного в **Обозревателе решений** нажмите клавишуF7Чтобы открыть файл его выделенным кодом Settings.xaml.cs, для редактирования.
    
  
6. Замените содержимое файла кода следующим кодом.
    
```cs
  
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using Microsoft.Phone.Controls;
using Microsoft.SharePoint.Client;

namespace SPListAppForNotifications
{
    public partial class Settings : PhoneApplicationPage
    {
        private const string RegisteredYesText = "Registered: Yes";
        private const string RegisteredNoText = "Registered: No";

        public Settings()
        {
            InitializeComponent();
        }

        protected override void OnNavigatedTo(System.Windows.Navigation.NavigationEventArgs e)
        {
            this.txtRegistrationStatus.Text = (Notifications.GetRegistrationStatus()) ? RegisteredYesText : RegisteredNoText;
        }

        private void OnOKButtonClick(object sender, EventArgs e)
        {
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }

        private void OnRegisterButtonClick(object sender, RoutedEventArgs e)
        {
            Notifications.OpenNotificationChannel(true);
            // Navigating back to List form. User will be notified when process is complete.
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }

        private void OnUnregisterButtonClick(object sender, RoutedEventArgs e)
        {
            Notifications.UnSubscribe();
            // Navigating back to List form. User will be notified when process is complete.
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }

        private void OnDeleteSubscribersButtonClick(object sender, RoutedEventArgs e)
        {            
            Notifications.ClearSubscriptionStore();
            // Navigating back to List form. User will be notified when process is complete.
            NavigationService.Navigate(new Uri("/Views/List.xaml", UriKind.Relative));
        }
    }
}
```

7. Сохраните файл.
    
  
8. Чтобы добавить в проект файл значка (appbar.check.rest.png) для кнопки **ApplicationBar** (btnOK) указанной в файле Settings.xaml, выберите узел папки изображений в **Окне Обозреватель решений**.
    
  
9. В меню **проект** выберите пункт **Добавить существующий элемент**. Откроется окно **Браузера файла**.
    
  
10. Перейдите к папке, в котором были установлены стандартные изображения значка Windows Phone по Windows Phone SDK 7.1.
    
    > **Примечание:** Изображения с быстрое переднего плана и темный фон находятся в %PROGRAMFILES%(x86)\\пакеты SDK для Microsoft\\Windows Phone\\v7.1\\значки\\темный при установке пакета SDK. 
11. Выберите файл изображения, с именем appbar.check.rest.png и нажмите кнопку **Добавить**. Добавить изображение добавляется в проект в узле изображений.
    
  
12. В **Обозревателе решений** выберите файл изображения только что добавлен и в **Окно "Свойства"** для файла, задайте для свойства **Действие при построении** для файла изображения, "Содержимого" и задайте для свойства значение "Копировать, если новее" **Копировать в выходной каталог**.
    
  
Теперь добавьте кнопку в форму списка (List.xaml) в проекте и реализации обработчика событий **Click** кнопки для перехода к странице параметров, созданных на предыдущем шаге. Также измените обработчик событий **OnViewModelInitialization** для открытия канала уведомлений (если пользователь выбрал для подписки на push-уведомлений).
  
    
    

### <a name="to-modify-the-list-form"></a>Для изменения формы списка


1. В **Обозревателе решений** выберите узел **представления**, дважды щелкните файл List.xaml. Файл открыт для редактирования.
    
  
2. Добавьте разметку, чтобы объявить дополнительные кнопки в элемент **ApplicationBar** в файле, как показано в следующем примере.
    
```
  
...
    <phone:PhoneApplicationPage.ApplicationBar>
        <shell:ApplicationBar IsVisible="True" IsMenuEnabled="True">
            <shell:ApplicationBarIconButton x:Name="btnNew" 
                   IconUri="/Images/appbar.new.rest.png" Text="New" 
                    Click="OnNewButtonClick" />
            <shell:ApplicationBarIconButton x:Name="btnRefresh" 
                    IconUri="/Images/appbar.refresh.rest.png" Text="Refresh" IsEnabled="True" 
                    Click="OnRefreshButtonClick" />
            <shell:ApplicationBarIconButton x:Name="btnSettings" IconUri="/Images/appbar.feature.settings.rest.png" Text="Settings" IsEnabled="True" Click="OnSettingsButtonClick" />
        </shell:ApplicationBar>
    </phone:PhoneApplicationPage.ApplicationBar>
...
```

3. С помощью файла List.xaml, выбранного в **Обозревателе решений** нажмите клавишуF7Чтобы открыть файл его выделенным кодом List.xaml.cs, для редактирования.
    
  
4. В блоке кода (обозначенного открывающих и закрывающих скобок), который реализует разделяемый класс **ListForm** добавьте следующий обработчик событий в файл.
    
```cs
  
private void OnSettingsButtonClick(object sender, EventArgs e)
{
    NavigationService.Navigate(new Uri("/Settings.xaml", UriKind.Relative));
}
```

5. Найдите в файле List.xaml.cs **OnViewModelInitialization** и добавьте вызов метода **OpenNotificationChannel** класса **Notifications**, созданной ранее. Измененные реализации обработчика должен выглядеть следующим образом.
    
```cs
  
private void OnViewModelInitialization(object sender, InitializationCompletedEventArgs e)
{
    this.Dispatcher.BeginInvoke(() =>
    {
        //If initialization has failed, show error message and return
        if (e.Error != null)
        {
            MessageBox.Show(e.Error.Message, e.Error.GetType().Name, MessageBoxButton.OK);
            return;
        }

        App.MainViewModel.LoadData(((PivotItem)Views.SelectedItem).Name);
        this.DataContext = (sender as ListViewModel);
    });

    // Open notification channel here if user has chosen to subscribe to notifications.
    if (Notifications.GetRegistrationStatus() == true)
        Notifications.OpenNotificationChannel(false);
}
```

6. Сохраните файл.
    
  
7. Чтобы добавить в проект файл значка (appbar.feature.settings.rest.png) для кнопки **ApplicationBar** (btnSettings) указанной в файле List.xaml, выберите узел папки изображений в **Окне Обозреватель решений**.
    
  
8. В меню **проект** выберите пункт **Добавить существующий элемент**. Откроется окно **Браузера файла**.
    
  
9. Перейдите к папке, в котором были установлены стандартные изображения значка Windows Phone по Windows Phone SDK 7.1. (Примечание в предыдущей процедуре для расположения файлы изображений в стандартной установке пакета SDK.)
    
  
10. Выберите файл изображения, с именем appbar.feature.settings.rest.png и нажмите кнопку **Добавить**. Добавить изображение добавляется в проект в узле изображений.
    
  
11. В **Обозревателе решений** выберите файл изображения только что добавлен и в **Окно "Свойства"** для файла, задайте для свойства **Действие при построении** для файла изображения, "Содержимого" и задайте для свойства значение "Копировать, если новее" **Копировать в выходной каталог**.
    
  
И, наконец добавьте код в обработчик событий **Application_Launching** в файл App.xaml.cs, чтобы подготовить приложение для приема push-уведомлений, с помощью свойств и методов класса **Notifications**, созданной ранее.
  
    
    

### <a name="to-add-code-to-the-appxamlcs-file"></a>Добавление кода в файл App.xaml.cs


1. В **Обозревателе решений** выберите в разделе узел, представляющий проект, выберите файл App.xaml.
    
  
2. КлавишиF7Чтобы открыть файл его выделенным кодом App.xaml.cs, для редактирования.
    
  
3. Найдите в файле **Application_Launching** обработчик событий. (Для новых проектов, созданных на основе шаблона приложения списка SharePoint для Windows Phone, входит в подписи для метода, который обрабатывает событие **Application_Launching** но не логика реализована в методе).
    
  
4. Замените обработчик событий **Application_Launching** следующий код.
    
```cs
  
private void Application_Launching(object sender, LaunchingEventArgs e)
{
    // Get set up for notifications.
    Notifications.Context = App.DataProvider.Context;
    Notifications.SaveDeviceAppIdToStorage();
}
```

5. Сохраните файл.
    
  
Если выполните компиляцию проекта и развертывание приложения в эмуляторе Windows Phone для ее выполнения можно нажмите кнопку **Параметры** в **Строке приложения** для отображения страницы, из которого можно регистрировать push-уведомлений (рис. 1).
  
    
    

**На рисунке 1. Страница параметров для регистрации уведомлений**

  
    
    

  
    
    
![Страница параметров для регистрации уведомлений](../images/bee8bbc5-a93d-4695-927b-c10e0e63ddf9.gif)
  
    
    
Если развернуть и активировать решение PushNotificationsList (разработанных в разделе [Создание решения на сервере для отправки push-уведомления на основании события элемента списка](#BKMK_ServerSideSolution) ранее в этом разделе) для вашей целевой SharePoint Server и регистрации с телефона для уведомлений прошла успешно, можно добавить элемент в список заданий на сервере и должно появиться обоих всплывающее уведомление (на рисунке 2) и , если приложение работает на телефоне при добавлении элемента в список необработанное уведомление (рис. 3).
  
    
    

**На рисунке 2. Всплывающее уведомление (приложение выполняется)**

  
    
    

  
    
    
![Всплывающее уведомление (работает приложение)](../images/19b38f1b-8f98-4e91-8384-ba0e2d3da744.gif)
  
    
    
Сообщение, отображаемое при ваше приложение получено всплывающее уведомление о ходе выполнения зависит от того, как обработчик событий **ShellToastNotificationReceived** реализован в вашем приложении. В классе **Notifications** этот образец заголовка и содержимого сообщения просто отображаются для пользователя.
  
    
    

**На рисунке 3. Необработанное уведомление**

  
    
    

  
    
    
![Необработанное уведомление](../images/2e5dc58a-55d2-48c6-a162-974199ff5e5c.gif)
  
    
    
Если приложение не работает, когда элемент добавляется в список, телефон по-прежнему должны отображать всплывающее уведомление (на рисунке 4).
  
    
    

**На рисунке 4. Всплывающее уведомление (приложение не выполняется)**

  
    
    

  
    
    
![Всплывающее уведомление (приложение не работает)](../images/c046bc5c-1e31-4ac6-9cba-05482cc36915.gif)
  
    
    
При добавлении элемента в список SharePoint заданий, код в приемник, связанный со списком пытается отправлять уведомления, используя MPNS для событий подписка телефоны, но в зависимости от того, в сети и других факторов, заданным уведомление может не будет приниматься телефон. На сервере, особенно значений столбцов код состояния и заголовки, чтобы определить состояние и результаты, связанные с отдельными уведомлений, можно найти в списке результатов Push-уведомлений.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Configurepushnot_addlresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Push-уведомлений Обзор для Windows Phone](http://msdn.microsoft.com/en-us/library/ff402558%28VS.92%29.aspx)
    
  
-  [Как: Настройка среды разработки мобильных приложений для SharePoint](how-to-set-up-an-environment-for-developing-mobile-apps-for-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

