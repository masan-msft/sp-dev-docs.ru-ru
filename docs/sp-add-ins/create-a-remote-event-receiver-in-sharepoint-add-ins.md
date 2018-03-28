---
title: Создание удаленного приемника событий в надстройках SharePoint
description: Создание удаленного приемника событий (RER), обрабатывающего события списка и элементы списка в надстройке SharePoint.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: db34b2390f04bdcc4d7ca61f926288a3b2fb3c80
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="create-a-remote-event-receiver-in-sharepoint-add-ins"></a>Создание удаленного приемника событий в надстройках SharePoint

Для начала желательно иметь представление о надстройках SharePoint с размещением у поставщика, а также разработать несколько надстроек, которые были бы хоть немного сложнее уровня "Hello World". См. статью [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).

Кроме того, следует ознакомиться со статьей [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md). 
 

<a name="MakeRER"> </a>

## <a name="create-a-remote-event-receiver"></a>Создание удаленного приемника событий

В этой статье показано, как усовершенствовать надстройку SharePoint, добавив удаленный приемник событий (RER), который обрабатывает событие ItemAdded для пользовательского списка на сайте надстройки. Удаленный приемник событий регистрируется на сайте надстройки с помощью декларативной разметки. Удаленные приемники событий регистрируются с помощью *хост-сайта* программно. Соответствующий пример кода см. на странице [SharePoint/PnP/Samples/Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers).
 
Удаленный приемник событий должен быть веб-службой SOAP. В этом примере он реализован в виде службы Windows Communication Foundation (WCF). Но его можно реализовать в стеке не от Майкрософт.
 
Чтобы следовать приведенным здесь указаниям и ввести код самостоятельно, скачайте пример из репозитория  [SharePoint-Add-in-CSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-CSOM-BasicDataOperations), а затем откройте его в Visual Studio.
 
> [!NOTE] 
> Этот пример использует файл TokenHelper.cs, созданный в Инструментах разработчика Office для Visual Studio. На момент создания примера это была последняя версия, но на момент чтения этой статьи она могла устареть. Тем не менее этот пример отлично подходит для создания первого удаленного приемника событий. Когда вы будете готовы двигаться дальше, ознакомьтесь с примерами в разделе "Дополнительные ресурсы" ниже. Скорее всего, они останутся актуальными.

### <a name="to-register-a-remote-event-receiver"></a>Регистрация удаленного приемника событий

1. Откройте проект надстройки SharePoint в Visual Studio. 

2. В **обозревателе решений** выберите узел проекта надстройки.

3. В строке меню выберите **Проект** > **Добавить новый элемент**.

4. На панели **Установленные шаблоны** выберите узел **Office/SharePoint**.

5. На панели **Шаблоны** выберите шаблон **Удаленный приемник событий**.

6. В поле **Имя** оставьте имя, указанное по умолчанию (RemoteEventReceiver1), и нажмите **Добавить**.

7. В списке **Тип приемника событий** выберите **События элемента списка**.

8. В списке **Элемент, который должен быть источником событий** выберите **Настраиваемый список**.
    
    В данном примере используется настраиваемый общий список. Тем не менее, приемник удаленных событий также может обрабатывать события, которые возникают в стандартных списках SharePoint, например **Объявления** или **Контакты**.
    
9. В списке **Обработать следующие события** выберите **Добавляется элемент** и нажмите **Готово**.
    
    В веб-приложение будет добавлена веб-служба для обработки указанного удаленного события. В надстройку SharePoint будет добавлен удаленный приемник событий, а в файл Elements.xml приемника, который хранится в компоненте сайта надстройки, будет добавлена ссылка на элемент списка.

### <a name="to-create-the-list"></a>Создание списка

1. В **обозревателе решений** выберите узел проекта надстройки.

2. В строке меню выберите **Проект** > **Добавить новый элемент**.

3. На панели **Установленные шаблоны** выберите узел **Office/SharePoint**.

4. На панели **Шаблоны** выберите шаблон **Список**.

5. В поле **Имя** оставьте имя, указанное по умолчанию (List1), и нажмите **Добавить**.

6. Выберите **Создать экземпляр списка на основе существующего шаблона списка** > **Настраиваемый список** и нажмите **Готово**.

### <a name="to-add-functionality-to-the-remote-event-receiver"></a>Добавление функций в удаленный приемник событий

1. Если тестовая ферма SharePoint и Visual Studio работают на разных компьютерах (или в качестве тестового сайта SharePoint используется область клиентов SharePoint Online), настройте проект для отладки с помощью служебной шины Microsoft Azure. Дополнительные сведения см. в статье [Устранение неполадок и отладка удаленного приемника событий в надстройке SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md). 
    
2. Замените содержимое файла кода для службы удаленного приемника событий (то есть в файле RemoteEventReceiver1.svc.cs) указанным ниже кодом. Этот код выполняет следующие задачи:
    
    - Возвращает допустимый объект контекста клиента. 
    
    - Если список под названием **EventLog** еще не существует, он создается и заполняется именами удаленных событий.
        
    - Добавляет запись в список для события, включая метку даты и времени.
        
    > [!NOTE] 
    > На время написания этой статьи Инструменты разработчика Office для Visual Studio содержали ссылки на все сборки, необходимые при создании получателя. В более поздних версиях пакета они могут отсутствовать. При получении ошибки компилятора просто добавьте отсутствующие ссылки. Например, может потребоваться добавить ссылки на System.ServiceModel или System.ComponentModel.DataAnnotations.

    ```C#
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Text;
    using Microsoft.SharePoint.Client;
    using Microsoft.SharePoint.Client.EventReceivers;
    using System.Runtime.Serialization;
    using System.ServiceModel;
    using System.ServiceModel.Channels;

    namespace BasicDataOperationsWeb.Services
    {
        public class RemoteEventReceiver1 : IRemoteEventService
        {
            public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
            {
                // When a "before" event occurs (such as ItemAdding), call the event 
                // receiver code.
                ListRemoteEventReceiver(properties);
                return new SPRemoteEventResult();
            }

            public void ProcessOneWayEvent(SPRemoteEventProperties properties)
            {
                // When an "after" event occurs (such as ItemAdded), call the event 
                // receiver code.            
            }

            public static void ListRemoteEventReceiver(SPRemoteEventProperties properties)
            {
                string logListTitle = "EventLog";

                // Return if the event is from the EventLog list itself. Otherwise, it may go into
                // an infinite loop.
                if (string.Equals(properties.ItemEventProperties.ListTitle, logListTitle, 
                    StringComparison.OrdinalIgnoreCase))
                    return;

                // Get the token from the request header.
                HttpRequestMessageProperty requestProperty = 
                    (HttpRequestMessageProperty)OperationContext
                    .Current.IncomingMessageProperties[HttpRequestMessageProperty.Name];
                string contextTokenString = requestProperty.Headers["X-SP-ContextToken"];

                // If there is a valid token, continue.
                if (contextTokenString != null)
                {
                    SharePointContextToken contextToken =
                        TokenHelper.ReadAndValidateContextToken(contextTokenString, 
                            requestProperty.Headers[HttpRequestHeader.Host]);

                    Uri sharepointUrl = new Uri(properties.ItemEventProperties.WebUrl);
                    string accessToken = TokenHelper.GetAccessToken(contextToken, 
                                                        sharepointUrl.Authority).AccessToken;
                    bool exists = false;

                    // Retrieve the log list "EventLog" and add the name of the event that occurred
                    // to it with a date/time stamp.
                    using (ClientContext clientContext = 
                        TokenHelper.GetClientContextWithAccessToken(sharepointUrl.ToString(), 
                                                                                                            accessToken))
                    {
                        clientContext.Load(clientContext.Web);
                        clientContext.ExecuteQuery();
                        List logList = clientContext.Web.Lists.GetByTitle(logListTitle);

                        try
                        {
                            clientContext.Load(logList);
                            clientContext.ExecuteQuery();
                            exists = true;
                        }

                        catch (Microsoft.SharePoint.Client.ServerUnauthorizedAccessException)
                        {
                            // If the user doesn't have permissions to access the server that's 
                            // running SharePoint, return.
                            return;
                        }

                        catch (Microsoft.SharePoint.Client.ServerException)
                        {
                            // If an error occurs on the server that's running SharePoint, return.
                            exists = false;
                        }

                        // Create a log list called "EventLog" if it doesn't already exist.
                        if (!exists)
                        {
                            ListCreationInformation listInfo = new ListCreationInformation();
                            listInfo.Title = logListTitle;
                            // Create a generic custom list.
                            listInfo.TemplateType = 100;
                            clientContext.Web.Lists.Add(listInfo);
                            clientContext.Web.Context.ExecuteQuery();
                        }

                        // Add the event entry to the EventLog list.
                        string itemTitle = "Event: " + properties.EventType.ToString() + 
                            " occurred on: " + 
                            DateTime.Now.ToString(" yyyy/MM/dd/HH:mm:ss:fffffff");
                        ListCollection lists = clientContext.Web.Lists;
                        List selectedList = lists.GetByTitle(logListTitle);
                        clientContext.Load<ListCollection>(lists);
                        clientContext.Load<List>(selectedList);
                        ListItemCreationInformation listItemCreationInfo = 
                            new ListItemCreationInformation();
                        var listItem = selectedList.AddItem(listItemCreationInfo);
                        listItem["Title"] = itemTitle;
                        listItem.Update();
                        clientContext.ExecuteQuery();
                    }
                }
            }
        }
    }
    ```

3. В файле Home.aspx.cs замените все экземпляры `SPHostUrl` на `SPAppWebUrl`.
    
    Например, следует заменить `sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);` на `sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);`. 
    
<a name="RunAndTest"> </a>
 
## <a name="run-and-test-the-event-handler"></a>Запуск и тестирование обработчика событий

Протестируйте обработчик, выполнив указанную ниже процедуру.

1. Нажмите клавишу **F5** для запуска проекта.

2. Подтвердите, что вы доверяете надстройке. Запустится ваша надстройка SharePoint. После этого появится таблица доступных списков, в которой будет список **List1**.

3. Выберите идентификатор списка **List1**. Этот идентификатор будет скопирован в поле **Получение элементов списка**.

4. Нажмите кнопку **Получить элементы списка**. Отобразится список **List1**, причем в нем не будет ни одного элемента.

5. В поле **Добавить элемент** введите **First Item** (Первый элемент), а затем нажмите кнопку **Добавить элемент**. Элемент **Первый элемент** будет добавлен в список **List1**. При этом активируется удаленный приемник событий и добавляется запись в список EventLog.

6. Нажмите кнопку **Обновить списки**, чтобы вернуться к таблице списков. В таблице появится новый список с именем **EventLog** (Журнал событий).

7. Выберите значение GUID **ListID** для **EventLog**, а затем нажмите кнопку **Получить элементы списка**. Появится таблица для списка **EventLog** с записью для события **Handle ItemAdding**, которое происходит при добавлении элемента в список **List1**.

<a name="Handle"> </a>

## <a name="add-or-remove-event-handlers-using-visual-studio"></a>Добавление и удаление обработчиков событий с помощью Visual Studio

1. В **обозревателе решений** выберите узел проекта для удаленного приемника событий.

2. На панели **Свойства** установите для свойств событий, которые нужно обрабатывать, значение **True**.
    
    Например, если вы хотите обеспечить реакцию на добавление элемента списка пользователем, задайте для свойства **Обрабатывать ItemAdding** значение **True**. Если вы не хотите обрабатывать это событие, задайте для его свойства значение **False**.
 
    **Удаленные события SharePoint в Visual Studio**

   ![Удаленные события SharePoint в Visual Studio](../images/SP_VS_Properties_Window_RemoteEvents.PNG)

3. Если вы добавили событие, включите код для его обработки в файл кода веб-службы, как и для предыдущих событий.
    
    Для обработки события другого типа добавьте в Надстройка SharePoint еще один приемник удаленных событий. Например, если приемник удаленных событий обрабатывает события, связанные с элементами списка, вы можете добавить в него еще одно такое событие. Однако если вы хотите обрабатывать событие, связанное со списками, вам нужно добавить другой приемник удаленных событий. 
    

## <a name="url-and-hosting-restrictions-for-production-remote-event-receivers"></a>URL-адрес и ограничения при размещении удаленных приемников событий в рабочей среде

Удаленный приемник событий может быть размещен в облаке или на локальном сервере, который не используется в качестве сервера SharePoint. URL-адрес производственного приемника не может использовать определенный порт. Это значит, что вам необходимо использовать порт 443 для протокола HTTPS (рекомендовано) или порт 80 для HTTP. Если вы используете HTTPS, приемник размещен локально, а надстройка находится в SharePoint Online, сервер размещения должен иметь доверенный сертификат, выданный центром сертификации. (Самозаверяющий сертификат подходит, только если надстройка расположена в локальной ферме SharePoint.)

## <a name="see-also"></a>Дополнительные ресурсы
<a name="Additional"> </a>

- [SharePoint/PnP/Samples/Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
- [SharePoint/PnP/Samples/Provisioning.ReR](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.ReR)
- [SharePoint/PnP/Samples/ECM.AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging)
- [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md)
    
 

