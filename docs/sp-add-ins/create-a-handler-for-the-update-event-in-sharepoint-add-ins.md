---
title: "Создание обработчика для события обновления надстройки SharePoint"
description: "Узнайте, как создать и использовать обработчик и применить логику отката для события обновления надстройки SharePoint."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 52d88501ca0918a676588115b81807df4a61bc9b
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a>Создание обработчика для события обновления надстройки SharePoint

Прежде чем начать, ознакомьтесь с разделом [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) и статьей [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), в том числе с перечисленными в них предварительными требованиями и основными понятиями.

> [!NOTE]
> **Система нумерации версий.** В этой статье предполагается, что версии надстройки имеют следующую нумерацию: 1.0.0.0, 2.0.0.0, 3.0.0.0 и т. д. Однако логика и инструкции не зависят от системы нумерации.

<a name="UpgradedEventEndpoint"> </a>
## <a name="create-an-upgradedeventendpoint-receiver"></a>Создание приемника UpgradedEventEndpoint

Для пользовательской логики обновления можно создать приемник удаленных событий SharePoint, который обрабатывает событие обновления надстройки. Этот метод следует применять осторожно. Используйте его только для действий, которые нельзя выполнить по-другому. Кроме того, инструкции из раздела [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) применимы к событию обновления надстройки так же, как и к событиям ее установки и удаления. В частности:

- Обработчик должен завершить работу и вернуть в SharePoint состояние отмены или продолжения в течение 30 секунд. В противном случае SharePoint вызовет обработчик повторно (до трех раз).

- Если обработчик вернет состояние отмены, SharePoint выполнит еще три попытки. 

- Как правило, следует включать в обработчик логику отката и проверки выполненных действий.

Один из сценариев, при котором удобно использовать обработчик **UpgradedEventEndpoint**, когда в удаленную базу данных добавляется вычисляемое поле. Предположим, добавляется столбец "Город" и его значение вычисляется из уже существующего столбца "Почтовый индекс". Ваш код в обработчике **UpgradedEventEndpoint** может итеративно перебирать существующие элементы в базе данных и вставлять значения в новые поля "Город" на основе значений в полях "Почтовый индекс" и внешнего источника данных, который сопоставляет индексы с городами. Изменения самой схемы базы данных лучше вносить за пределами обработчика **UpgradedEventEndpoint**, используя лучшие методики для определенной платформы базы данных.

Инструкции по создании обработчика для события надстройки см. в статьях [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md) и [Создание приемника событий надстройки в надстройках для SharePoint](create-an-add-in-event-receiver-in-sharepoint-add-ins.md). 

В приведенной ниже процедуре предполагается, что вы добавили приемник удаленных событий в свой проект надстройки SharePoint в Visual Studio. 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a>Обработка первого события обновления надстройки

1. Откройте файл AppEventReceiver.svc.cs и добавьте в метод **ProcessEvent** условную структуру, проверяющую, является ли событие, которое вызвало обработчик, событием обновления. Код обновления добавляется внутрь этой структуры. Если коду требуется доступ к SharePoint, можете использовать клиентскую объектную модель (CSOM) для управляемого кода SharePoint или интерфейс REST. 

   Расположение условной структуры зависит от структуры другого кода в методе. Обычно она находится рядом со аналогичными условными структурами, проверяющими события установки и удаления надстройки. Она может находиться в условной структуре, которая проверяет определенные свойства или подсвойства объекта **SPRemoteEventProperties**, который передается в метод **ProcessEvent** при значениях **Null** или других недопустимых значениях. Она также может находиться в блоке **try**. 
   
   Ниже представлен пример структуры. Объект _properties_ — это объект **SPRemoteEventProperties**.
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
     }

    ```

2. Чтобы использовать CSOM в обработчике, добавьте (внутри условного блока) блок **using**, который получает объект **ClientContext**, вызывая метод **TokenHelper.CreateAppEventClientContext**. Для доступа к сайту надстройки задайте для второго параметра значение **true**. Для доступа к хост-сайту задайте значение **false**. Для доступа к обоим сайтам требуются два отдельных контекста клиента.

3. Если обработчику нужен доступ к компонентам, расположенным не в SharePoint, поместите этот код за пределами всех блоков контекста клиента. Код должен иметь следующую структуру:
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
         using (ClientContext cc = TokenHelper.CreateAppEventClientContext(properties, true))
         {
             // CSOM code that accesses the add-in web
         }
         using (ClientContext cc = TokenHelper.CreateAppEventClientContext(properties, false))
         {
             // CSOM code that accesses the host web
         }
         // Other update code
     }

    ```

4. Для использования интерфейса REST ваш код с помощью других методов в классе **TokenHelper** получает маркер доступа, который потом включается в запросы, отправляемые им SharePoint. Подробнее см. в статье [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md). Код должен иметь следующую структуру:
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
         string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);
         if (contextTokenString != null)
         {
             contextToken = TokenHelper.ReadAndValidateContextToken(contextTokenString, 
                                                                                                                       Request.Url.Authority);
             accessToken = TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                                        .AccessToken;

            // REST code that accesses SharePoint
         }  
         // Other update code
     }

    ```

5. Для доступа к SharePoint в коде REST также необходимо указать URL-адрес хост-сайта или сайта надстройки (или и того, и другого). Эти URL-адреса являются подсвойствами объекта **SPRemoteEventProperties**, передаваемого методу **ProcessEvent**. Вот код, который позволяет их получить:
    
    ```C#
       Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
       Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
    ```

Когда вы обновляете надстройку во второй (или третий и т. д.) раз, может потребоваться сделать так, чтобы логика обновления не выполнялась много раз на одном и том же экземпляре надстройки. Ниже приведена процедура, позволяющая это сделать.

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a>Обработка события обновления надстройки при последующих обновлениях

1. Откройте файл AppEventReceiver.svc.cs и найдите код первого обновления (с версии 1.0.0.0 до версии 2.0.0.0). Назовем его кодом предыдущего обновления. (Этот код обычно расположен после кода авторизации, который получает контекст клиента или маркеры доступа.) При обновлении с версии 2.0.0.0 до версии 3.0.0.0 в коде предыдущего обновления, скорее всего, будут действия, которые не нужно выполнять снова для того же экземпляра надстройки, но нужно выполнять для экземпляра надстройки, не обновленной до версии 2.0.0.0 (в таком случае экземпляр обновляется с версии 1.0.0.0 до версии 3.0.0.0).

2. Поместите код предыдущего обновления в условную структуру, которая проверяет предыдущую версию экземпляра надстройки и выполняется, только если код в структуре еще не запускался для этого экземпляра надстройки. Предыдущая версия экземпляра хранится в подсвойстве **PreviousVersion** объекта **SPRemoteEventProperties**.

3. Добавьте новую логику обновления (для обновления с версии 2.0.0.0 до версии 3.0.0.0) после этой структуры. Ниже приведен пример.
    
    ```C#
       Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 (previous update code) is here.
     }
     // Code to update from 2.0.0.0 to 3.0.0.0 is here.

    ```

4. Повторите эти действия для каждого последующего обновления. Ниже представлена структура кода для обновления с версии 3.0.0.0 до версии 4.0.0.0.
    
    ```C#
     Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 is here.
     }

     Version ver3OOO = new Version("3.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver3OOO)
     {
         // Code to update from 2.0.0.0 to 3.0.0.0 (previous update code) is here.
     }
     // Code to update from 3.0.0.0 to 4.0.0.0 is here.

    ```

> [!IMPORTANT]
> Если вы добавляете компонент в надстройку в обработчике **UpgradedEventEndpoint**, обязательно добавьте такой же код в обработчик **InstalledEventEndpoint**, чтобы этот компонент имелся и в заново установленной настройке. Кроме того, необходимо добавить (или изменить) обработчик [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx), чтобы надстройка удалила компонент. 

> Все добавления и изменения, внесенные обработчиком **InstalledEventEndpoint**, должны отменяться или удаляться обработчиком **UninstallingEventEndpoint**. Не следует удалять только данные, которые понадобятся после удаления надстройки со второго уровня корзины. (Данными также считаются созданные надстройкой веб-сайты, за исключением сайта надстройки.)

<a name="AddRollbackLogic"> </a>
## <a name="add-rollback-logic-to-the-handler"></a>Добавление логики отката в обработчик

Если при обновлении надстройки возникает ошибка, инфраструктура SharePoint останавливает процесс и откатывает экземпляр надстройки и все его компоненты до предыдущей версии. Но инфраструктура не знает, какие действия выполняет обработчик **UpgradedEventEndpoint**, поэтому не всегда может их отменить. Необработанное исключение при выполнении обработчика **UpgradedEventEndpoint** почти всегда означает, что необходимо откатить все обновление надстройки. Но этого не происходит, потому что инфраструктура не знает, как отменить некоторые действия, выполненные кодом обработчика **UpgradedEventEndpoint**. Поэтому код **UpgradedEventEndpoint** должен:

- перехватывать все исключения;
    
- передавать управление пользовательскому коду отката для отмены всех выполненных действий;
    
- сообщать инфраструктуре SharePoint, что необходимо откатить все обновление надстройки;
    
- передавать инфраструктуре сообщение об ошибке.

Не все действия, выполняемые обработчиком **UpgradedEventEndpoint**, необходимо явно отменять в обработчике. Сайт надстройки откатывается инфраструктурой, поэтому вашему коду не нужно отменять внесенные в него изменения. Но обработчик **UpgradedEventEndpoint**, как правило, должен отменять изменения, внесенные им в хост-сайт или другие внешние компоненты.

При втором (или третьем и т. д.) обновлении ваша логика обработки обновлений должна учитывать, что обновляемый экземпляр надстройки не обязательно является непосредственно предыдущей версией. Если это не так, может понадобиться два или больше блоков кода обновления, которые нужно обратить. Для этого требуется условная логика, основанная на номере предыдущей версии. Ниже приведен пример логики отката для обновления до версии 4.0.0.0.

```C#
catch (Exception e)
{ 
    // Rollback of the 3.0.0.0 to 4.0.0.0 update logic goes here.

    Version ver3OOO = new Version("3.0.0.0");
    if (properties.AppEventProperties.PreviousVersion < ver3OOO)
    {
        // Rollback of the 2.0.0.0 to 3.0.0.0 update logic goes here.
    }

    Version ver2OOO = new Version("2.0.0.0");
    if (properties.AppEventProperties.PreviousVersion < ver2OOO)
    {
        // Rollback of the 1.0.0.0 to 2.0.0.0 update logic goes here.
    }
}
```

На последнем этапе обработки ошибки необходимо назначить сообщение об ошибке и состояние отмены объекту **SPRemoteEventResult**, который метод **ProcessEvent** возвращает инфраструктуре обновления SharePoint. Ниже приведен пример. В этом коде _result_ представляет собой объект **SPRemoteEventResult**, ранее объявленный в методе **ProcessEvent**.

```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```

> [!IMPORTANT]
> Очень важно назначить **SPRemoteEventServiceStatus.CancelWithError** (или **SPRemoteEventServiceStatus.CancelNoError**) свойству **Status**. Это свойство сообщает инфраструктуре, что нужно откатить обновление. Но до отката SharePoint еще трижды попытается запустить обработчик.

### <a name="use-the-handler-delegation-strategy"></a>Использование стратегии делегирования обработчиков

Стратегию делегирования обработчиков, описанную в разделе [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents), можно использовать и в **UpdatedEventHandler**. На удаленном компьютере выполняется не только логика отката вместе с логикой проверки выполненных действий, но и логика управления версиями. Ограничения применяются и здесь: как правило, эту стратегию нельзя использовать для обновления нескольких удаленных систем.

## <a name="next-steps"></a>Дальнейшие действия

Вернитесь к разделу [Основные шаги по обновлению надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из указанных ниже статей, чтобы узнать, как обновить компоненты надстройки SharePoint.

-  [Обновление компонентов сайта надстройки в SharePoint](update-add-in-web-components-in-sharepoint.md)
-  [Обновление компонентов хост-сайта в SharePoint](update-host-web-components-in-sharepoint.md)
-  [Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins.md) 

## <a name="additional-resources"></a>Дополнительные ресурсы

-  [Обновление надстроек SharePoint](update-sharepoint-add-ins.md)
-  [Элемент UpgradedEventEndpoint (PropertiesDefinition complexType, манифест надстройки SharePoint)](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
-  [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md)
-  [Создание удаленного приемника событий в надстройках SharePoint](create-an-add-in-event-receiver-in-sharepoint-add-ins.md)
    
 

