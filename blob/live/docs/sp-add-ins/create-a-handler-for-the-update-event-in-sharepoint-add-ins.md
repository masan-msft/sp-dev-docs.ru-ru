---
title: "Создание обработчика событий обновления для надстроек SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d647c85975b0b94e6265e60ee8463cbadf57df57
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a><span data-ttu-id="b5204-102">Создание обработчика событий обновления для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5204-102">Create a handler for the update event in SharePoint Add-ins</span></span>
<span data-ttu-id="b5204-103">Узнайте, как создать и использовать обработчик событий обновления для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b5204-103">Create and use a handler for the update event of a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="b5204-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b5204-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites-for-creating-a-handler-for-the-add-in-update-event"></a><span data-ttu-id="b5204-107">Необходимые условия для создания обработчика событий обновления в надстройке</span><span class="sxs-lookup"><span data-stu-id="b5204-107">Prerequisites for creating a handler for the add-in update event</span></span>
<span data-ttu-id="b5204-108"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="b5204-108"><a name="Prerequisites"> </a></span></span>

<span data-ttu-id="b5204-109">Ознакомьтесь с разделом [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) и статье [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), а том числе с перечисленными в них предварительными требованиями и основными понятиями.</span><span class="sxs-lookup"><span data-stu-id="b5204-109">Be thoroughly familiar with both  [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) and [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in them.</span></span>
 

 

## <a name="create-an-upgradedeventendpoint-receiver"></a><span data-ttu-id="b5204-110">Создание приемника UpgradedEventEndpoint</span><span class="sxs-lookup"><span data-stu-id="b5204-110">Create an UpgradedEventEndpoint receiver</span></span>
<span data-ttu-id="b5204-111"><a name="UpgradedEventEndpoint"> </a></span><span class="sxs-lookup"><span data-stu-id="b5204-111"><a name="UpgradedEventEndpoint"> </a></span></span>


 <span data-ttu-id="b5204-p102">**Примечание**   **Система нумерации версий.** Для согласованности в этом разделе предполагается, что версии надстройки имеют следующую нумерацию: 1.0.0.0, 2.0.0.0, 3.0.0.0 и т. д. Однако логика и инструкции применяются независимо от системы нумерации.</span><span class="sxs-lookup"><span data-stu-id="b5204-p102">**Note**   **Version numbering system:** For consistency, this topic assumes that the add-in version numbers are 1.0.0.0, 2.0.0.0, 3.0.0.0, and so on. However, the logic and guidance applies no matter what your numbering system is.</span></span>
 

<span data-ttu-id="b5204-p103">Для настраиваемой логики обновления можно создать приемник удаленных событий SharePoint, который обрабатывает событие обновления надстройки. Этот метод следует применять осторожно. Используйте его только для тех этапов обновления, которые невозможно обработать другим способом. Кроме того, инструкции из раздела  [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) применимы к событию обновления надстройки так же, как и к событиям установки и удаления. В частности:</span><span class="sxs-lookup"><span data-stu-id="b5204-p103">For custom update logic, you can create a SharePoint remote event receiver that handles the add-in updated event. You should be conservative in using this technique. Use it only for updating steps that can't be done any other way. Also, the guidance found in  [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) applies for the add-in updated event as much as the add-in installed and add-in uninstalling events. This includes:</span></span>
 

 

- <span data-ttu-id="b5204-p104">после выполнения обработчик должен возвращать в SharePoint состояние отмены или продолжения в течение 30 секунд. Если этого не произойдет, SharePoint будет повторно вызывать обработчик (до трех раз);</span><span class="sxs-lookup"><span data-stu-id="b5204-p104">Your handler has to complete and return either a cancel or a continue status to SharePoint in 30 seconds. If it does not, SharePoint will call the handler again, up to three more times.</span></span>
    
 
- <span data-ttu-id="b5204-121">если обработчик возвращает состояние отмены, SharePoint повторяет попытку до трех раз;</span><span class="sxs-lookup"><span data-stu-id="b5204-121">If your handler returns a cancel status, SharePoint will retry up to three more times.</span></span> 
    
 
- <span data-ttu-id="b5204-122">Как правило, следует включать в обработчик логику отката и проверки выполненных действий.</span><span class="sxs-lookup"><span data-stu-id="b5204-122">You usually need to include rollback and "already done" logic in your handler.</span></span>
    
 
<span data-ttu-id="b5204-p105">К примеру, использовать обработчик **UpgradedEventEndpoint** удобно, когда в удаленную базу данных добавляется вычисляемое поле. Предположим, добавляется столбец "Город" и его значение вычисляется из уже существующего столбца "Почтовый индекс". Код в обработчике **UpgradedEventEndpoint** может просматривать существующие элементы в базе данных и вставлять значения в новые поля "Город" на основе значений в полях "Почтовый индекс" и внешнего источника данных, который сопоставляет индексы с городами. Изменения самой схемы базы данных лучше вносить за пределами обработчика **UpgradedEventEndpoint**, используя лучшие методики для определенной платформы базы данных.</span><span class="sxs-lookup"><span data-stu-id="b5204-p105">One scenario in which an  **UpgradedEventEndpoint** handler is useful is when a computed field is added to a remote database. Suppose a City column is added, and its value is computed from an already existing Postal Code column. Your code in an **UpgradedEventEndpoint** handler could iterate through existing items in the database and fill in the value for the new City field based on the value of the Postal Code field and some external data source that maps postal codes onto cities. The change to the database schema itself is best done outside the **UpgradedEventEndpoint** handler by using the best practices of the database platform.</span></span>
 

 
<span data-ttu-id="b5204-127">Подробнее о создании обработчика для события надстройки можно узнать в статьях  [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md) и [Создание приемника событий надстройки в надстройках для SharePoint](create-an-add-in-event-receiver-in-sharepoint-add-ins.md). В следующей процедуре предполагается, что вы добавили элемент приемника удаленных событий надстройки в свой проект Надстройка SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5204-127">For more details about how to create a handler for the add-in event, see  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md) and [Create an add-in event receiver in SharePoint Add-ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md). The following procedure assumes that you have added the add-in event receiver item to your SharePoint Add-in project in Visual Studio.</span></span> 
 

 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a><span data-ttu-id="b5204-128">Обработка первого события обновления надстройки</span><span class="sxs-lookup"><span data-stu-id="b5204-128">To handle the add-in updated event the first time</span></span>


1. <span data-ttu-id="b5204-p106">Откройте файл AppEventReceiver.svc.cs и добавьте в метод  **ProcessEvent** условную структуру, проверяющую, является ли событие, вызвавшее обработчик, событием обновления. Ваш код обновления добавляется внутрь этой структуры. Если коду нужно получать доступ к SharePoint, вы можете использовать интерфейс клиентской объектной модели управляемого кода SharePoint (CSOM) или REST. Место размещения условной структуры в методе зависит от того, как в нем структурирован другой код. Обычно оно сходно с аналогичными условными структурами, проверяющими события установки и удаления надстройки. Оно может находиться внутри условной структуры, которая проверяет определенные свойства или подсвойства объекта **SPRemoteEventProperties** , который передается в **ProcessEvent** для значений **null** или других значений, обозначающих недопустимые состояния, или внутри блока **try**. Ниже представлен пример структуры. Объект  _properties_ это объект **SPRemoteEventProperties** .</span><span class="sxs-lookup"><span data-stu-id="b5204-p106">Open the AppEventReceiver.svc.cs file and add a conditional structure to the  **ProcessEvent** method that tests whether the event that invoked the handler is the updated event. Your updating code goes inside this structure. If your code needs to access SharePoint, you can use the SharePoint managed code client object model (CSOM) or Representational State Transfer (REST) interface. Where the conditional structure is located in the method depends on how you have structured the other code in the method. Typically, it is a peer of similar conditional structures that test for the add-in installed and add-in uninstalling events. It may be within a conditional structure that tests certain properties or subproperties of the **SPRemoteEventProperties** object that is passed to **ProcessEvent** for **null** values or other invalid values. It may also be within a **try** block. The following is an example of the structure. The _properties_ object is an **SPRemoteEventProperties** object.</span></span>
    
```C#
  if (properties.EventType == SPRemoteEventType.AppUpgraded)
{
}

```

2. <span data-ttu-id="b5204-p107">Чтобы использовать CSOM в обработчике, добавьте (внутри условного блока) блок **using**, который получает объект **ClientContext**, вызывая метод **TokenHelper.CreateAppEventClientContext**. Чтобы получить доступ к сайту надстройки, задайте для второго параметра значение **true**. Для доступа к хост-сайту задайте значение **false**. Чтобы одновременно использовать оба варианта доступа, необходимо два отдельных объекта контекста клиента.</span><span class="sxs-lookup"><span data-stu-id="b5204-p107">To use CSOM in the handler, add (within the conditional block) a  **using** block that gets a **ClientContext** object by calling the **TokenHelper.CreateAppEventClientContext** method. Specify **true** for the second parameter to access the add-in web. Specify **false** to access the host web. If you need to access both, you will need two different client context objects.</span></span>
    
 
3. <span data-ttu-id="b5204-p108">Если обработчику нужен доступ к компонентам, расположенным не в SharePoint, поместите этот код за пределами всех блоков контекста клиента. Код должен иметь следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="b5204-p108">If your handler needs to access non-SharePoint components, put that code outside any client context blocks. Your code should be structured similarly to the following:</span></span>
    
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

4. <span data-ttu-id="b5204-p109">Для использования интерфейса REST ваш код с помощью других методов класса **TokenHelper** получает маркер доступа, который затем включается в запросы, отправляемые им среде SharePoint. Дополнительные сведения см. в статье [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md). Код должен иметь следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="b5204-p109">To use the REST interface, your code uses other methods in the  **TokenHelper** class to get an access token, which is then included in the requests it makes to SharePoint. For more information, see [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md). Your code should be structured similarly to the following.</span></span>
    
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

5. <span data-ttu-id="b5204-p110">Для доступа к SharePoint вашему коду REST также должен передаваться URL-адрес хост-сайта, сайта надстройки или обоих этих сайтов. Эти URL-адреса являются подсвойствами объекта  **SPRemoteEventProperties** , передаваемого методу **ProcessEvent** . Ниже показан код, который позволяет их получить.</span><span class="sxs-lookup"><span data-stu-id="b5204-p110">To access SharePoint, your REST code also needs to know the URL of the host web or add-in web or both. These URLs are both subproperties of the  **SPRemoteEventProperties** object that is passed to the **ProcessEvent** method. The following code shows how to get them.</span></span>
    
```C#
  Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
```

<span data-ttu-id="b5204-p111">Когда вы обновляете надстройку во второй (или третий и т. д.) раз, может потребоваться сделать так, чтобы логика обновления не выполнялась много раз на одном и том же экземпляре надстройки. Ниже приведена процедура, позволяющая это сделать.</span><span class="sxs-lookup"><span data-stu-id="b5204-p111">When you update an add-in for the second (or third, and so on) time, you may need to ensure that some update logic does not run multiple times on the same add-in instance. The following procedure shows you how.</span></span>
 

 

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a><span data-ttu-id="b5204-152">Обработка события обновления надстройки при последующих обновлениях</span><span class="sxs-lookup"><span data-stu-id="b5204-152">To handle the add-in updated event on subsequent updates</span></span>


1. <span data-ttu-id="b5204-p112">Откройте файл AppEventReceiver.svc.cs, с помощью которого были реализованы действия по обновлению в первом обновлении (с 1.0.0.0. до 2.0.0.0). Назовем его кодом предыдущего обновления. Этот код обычно расположен после кода авторизации, который получает контекст клиента или маркеры доступа. Теперь при новом обновлении (с 2.0.0.0 до 3.0.0.0) в предыдущем коде, скорее всего, будут содержаться действия, которые не нужно запускать снова на том же экземпляре надстройки, но нужно запустить на экземпляре надстройки, не обновленной до версии 2.0.0.0 (в таком случае экземпляр сейчас обновляется с 1.0.0.0. до 3.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="b5204-p112">Open the AppEventReceiver.svc.cs file, and find the code that implemented update actions in the first update (from 1.0.0.0. to 2.0.0.0). Let's call this the previous update code. (This code is generally located after the authorization code that gets client context or access tokens.) Now that you are updating again (from 2.0.0.0 to 3.0.0.0), there will typically be actions in the previous update code here that you don't want to run again on the same add-in instance, but you do want it to run on a add-in instance that was never updated to 2.0.0.0 (in which case, the instance is now being updated all the way from 1.0.0.0. to 3.0.0.0).</span></span>
    
 
2. <span data-ttu-id="b5204-p113">Поместите код предыдущего обновления в условную структуру, которая проверяет предыдущую версию экземпляра надстройки и выполняется, только если код в структуре еще не запускался для этого экземпляра надстройки. Предыдущая версия экземпляра хранится в подсвойстве  **PreviousVersion** объекта **SPRemoteEventProperties** .</span><span class="sxs-lookup"><span data-stu-id="b5204-p113">Wrap the previous update code in a conditional structure that tests for the previous version of the add-in instance and executes only if the code in the structure has not run before on this add-in instance. The previous version of the instance is stored in the  **PreviousVersion** subproperty of the **SPRemoteEventProperties** object.</span></span>
    
 
3. <span data-ttu-id="b5204-p114">Добавьте новую логику обновления (для обновления с версии 2.0.0.0 до версии 3.0.0.0) после этой структуры. Ниже представлен пример.</span><span class="sxs-lookup"><span data-stu-id="b5204-p114">Add your new update logic (for the update from 2.0.0.0 to 3.0.0.0) below this structure. The following is an example.</span></span>
    
```C#
  Version ver2OOO = new Version("2.0.0.0");
if (properties.AppEventProperties.PreviousVersion < ver2OOO)
{
    // Code to update from 1.0.0.0 to 2.0.0.0 (previous update code) is here.
}
// Code to update from 2.0.0.0 to 3.0.0.0 is here.

```

4. <span data-ttu-id="b5204-p115">Повторите эти действия для каждого последующего обновления. Ниже представлена структура кода для обновления с версии 3.0.0.0 до версии 4.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5204-p115">For each subsequent update, repeat these steps. For the update from 3.0.0.0 to 4.0.0.0, your code should have the following structure.</span></span>
    
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


 <span data-ttu-id="b5204-p116">**Важно!** Если вы добавляете компонент в надстройку в обработчике **UpgradedEventEndpoint**, обязательно добавьте такой же код в обработчик **InstalledEventEndpoint**, потому что этот компонент также нужно включить в надстройку в новой установке. Кроме того, необходимо добавить обработчик [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) (или изменить его), чтобы надстройка удалила компонент. По большей части, все добавления и изменения, внесенные обработчиком **InstalledEventEndpoint**, отменяются или удаляются с помощью обработчика **UninstallingEventEndpoint**. Единственное исключение состоит в том, что данные, которые будут необходимы после удаления надстройки со второго уровня корзины, не должны быть удалены. Данными также считаются созданные надстройкой веб-сайты, за исключением сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="b5204-p116">**Important**  If you add a component to an add-in in an  **UpgradedEventEndpoint** handler, be sure to add the same code to an **InstalledEventEndpoint** handler because you want that component included in the add-in on a brand new installation as well. Also, you should add an [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) (or revise it) for the add-in to remove the component. For the most part, anything that was added or changed by the **InstalledEventEndpoint** should be reversed or deleted by the **UninstallingEventEndpoint**. One exception is that data that will remain useful after the add-in is removed from the second-stage recycle bin should not be deleted. (Websites, other than the add-in web, that are created by the add-in should be considered data.)</span></span>
 


## <a name="add-rollback-logic-to-the-handler"></a><span data-ttu-id="b5204-169">Добавление логики отката в обработчик</span><span class="sxs-lookup"><span data-stu-id="b5204-169">Add rollback logic to the handler</span></span>
<span data-ttu-id="b5204-170"><a name="AddRollbackLogic"> </a></span><span class="sxs-lookup"><span data-stu-id="b5204-170"><a name="AddRollbackLogic"> </a></span></span>

<span data-ttu-id="b5204-p117">В случае возникновения ошибки при обновлении надстройки инфраструктура SharePoint останавливает процесс обновления и выполняет откат экземпляра надстройки вместе со всеми его компонентами до предыдущей версии. Но инфраструктура не получает сведений о действиях логики обработчика **UpgradedEventEndpoint**, поэтому не всегда может их отменить. Необработанное исключение при выполнении обработчика **UpgradedEventEndpoint** почти всегда означает, что необходимо сделать откат всего процесса обновления надстройки. Но этого не происходит, потому что инфраструктура не имеет возможности отменить некоторые действия, выполненные кодом обработчика **UpgradedEventEndpoint**. По этой причине код **UpgradedEventEndpoint** должен:</span><span class="sxs-lookup"><span data-stu-id="b5204-p117">If an error occurs when an add-in is being updated, the SharePoint infrastructure stops the update process and rolls back the add-in instance and all its components to the previous version of the add-in instance. But the infrastructure has no way of knowing what your  **UpgradedEventEndpoint** handler logic does, so it can't always undo it. An unhandled exception thrown while your **UpgradedEventEndpoint** handler is executing almost certainly indicates that the entire add-in update process should be rolled back, but it won't be because the infrastructure doesn't know how to undo some things your **UpgradedEventEndpoint** code might have done. For this reason, the **UpgradedEventEndpoint** code must:</span></span>
 

 

1. <span data-ttu-id="b5204-175">перехватывать все исключения;</span><span class="sxs-lookup"><span data-stu-id="b5204-175">Catch all exceptions.</span></span>
    
 
2. <span data-ttu-id="b5204-176">переходить к выполнению настроенного кода отката для отмены всех действий, выполненных до текущего момента;</span><span class="sxs-lookup"><span data-stu-id="b5204-176">Branch to custom rollback code to undo what it has been done to that point.</span></span>
    
 
3. <span data-ttu-id="b5204-177">сообщать инфраструктуре SharePoint, что необходимо сделать откат всего обновления надстройки;</span><span class="sxs-lookup"><span data-stu-id="b5204-177">Signal to the SharePoint infrastructure that the entire add-in update should be rolled back.</span></span>
    
 
4. <span data-ttu-id="b5204-178">передавать инфраструктуре сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b5204-178">Pass on an error message to the infrastructure.</span></span>
    
 
<span data-ttu-id="b5204-p118">Не все действия, выполняемые обработчиком **UpgradedEventEndpoint**, необходимо явно отменять внутри обработчика. Откат сайта надстройки будет выполнен инфраструктурой, поэтому вашему коду не нужно отменять изменения в нем. Но обработчик **UpgradedEventEndpoint**, как правило, должен обратить изменения, внесенные им на хост-сайте или в других компонентах, которые находятся вне надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b5204-p118">Not everything your  **UpgradedEventEndpoint** does needs to be explicitly reversed inside the handler. The add-in web is going to be rolled back by the infrastructure, so your code does not have to undo changes to the add-in web. But the **UpgradedEventEndpoint** handler usually does have to reverse changes it has made to the host web or other components that are external to the SharePoint Add-in.</span></span>
 

 
<span data-ttu-id="b5204-p119">При втором (или третьем и т. д.) обновлении ваша логика обработки обновлений должна учитывать, что обновляемый экземпляр надстройки не обязательно является непосредственно предыдущей версией. Если это не так, может понадобиться два или больше блоков кода обновления, которые нужно обратить. Для этого требуется условная логика, основанная на номере предыдущей версии. Ниже приведен пример логики отката для обновления до версии 4.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="b5204-p119">On the second (or third, and so on) update, your exception handing logic has to take account of the fact that the add-in instance that is being updated is not necessarily the immediately previous version. If it isn't, there may be two or more blocks of update code that need to be reversed. For this reason, you need conditional logic that is based on the number of the previous version. The following is an example of the rollback logic for an update to version 4.0.0.0.</span></span>
 

 



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

<span data-ttu-id="b5204-p120">На последнем этапе обработки ошибки необходимо назначить сообщение об ошибке и состояние отмены объекту  **SPRemoteEventResult** , который возвращается методом **ProcessEvent** инфраструктуре обновления SharePoint. Ниже приведен пример. В данном коде _result_ это объект **SPRemoteEventResult**, который был объявлен ранее в методе **ProcessEvent**.</span><span class="sxs-lookup"><span data-stu-id="b5204-p120">The last things your error handling should do is assign an error message and a cancel status to the  **SPRemoteEventResult** object that the **ProcessEvent** method returns to the SharePoint update infrastructure. The following is an example. In this code, _result_ is an **SPRemoteEventResult** object that has been declared earlier in the **ProcessEvent** method.</span></span>
 

 



```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```


 <span data-ttu-id="b5204-p121">**Важно!** Очень важно назначить **SPRemoteEventServiceStatus.CancelWithError** (или **SPRemoteEventServiceStatus.CancelNoError**) свойству **Status**. Это свойство сообщает инфраструктуре, что нужно выполнить откат обновления. Однако SharePoint повторит попытку запуска обработчика еще три раза, прежде чем выполнять откат.</span><span class="sxs-lookup"><span data-stu-id="b5204-p121">**Important**  Assigning  **SPRemoteEventServiceStatus.CancelWithError** (or **SPRemoteEventServiceStatus.CancelNoError**) to the  **Status** property is crucial. This property is what signals the infrastructure to roll back the update. But SharePoint will retry your handler three times before it rolls back the update.</span></span>
 


### <a name="use-the-handler-delegation-strategy"></a><span data-ttu-id="b5204-192">Использование стратегии делегирования обработчиков</span><span class="sxs-lookup"><span data-stu-id="b5204-192">Use the handler delegation strategy</span></span>

<span data-ttu-id="b5204-p122">Стратегию делегирования обработчиков, описанную в разделе  [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents), можно применять и в **UpdatedEventHandler**. На удаленном компьютере пакетно выполняются не только логика отката и логика проверки выполненных действий, но и логика управления версиями. Ограничения для стратегий применяются и здесь: как правило, эту логику невозможно использовать для обновления нескольких удаленных систем.</span><span class="sxs-lookup"><span data-stu-id="b5204-p122">The handler delegation strategy that is described in  [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) can be used in an **UpdatedEventHandler** too. Not only is your rollback and "already done" logic bundled and run on the remote component, but your versioning logic is too. The limitations of the strategy apply here too: you usually can't use it to update more than one remote system.</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="b5204-196">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5204-196">Next steps</span></span>
<span data-ttu-id="b5204-197"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="b5204-197"><a name="Next"> </a></span></span>

<span data-ttu-id="b5204-198">Вернитесь к разделу  [Основные действия при обновлении надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из следующих статей, чтобы узнать, как обновить следующий важный компонент надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b5204-198">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="b5204-199">Обновление компонентов сайта надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5204-199">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="b5204-200">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5204-200">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
    
 
-  <span data-ttu-id="b5204-201">[Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins.md) </span><span class="sxs-lookup"><span data-stu-id="b5204-201">[Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins.md)</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="b5204-202">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b5204-202">Additional resources</span></span>
<span data-ttu-id="b5204-203"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b5204-203"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="b5204-204">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5204-204">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="b5204-205">Элемент UpgradedEventEndpoint (PropertiesDefinition complexType, манифест надстройки SharePoint)</span><span class="sxs-lookup"><span data-stu-id="b5204-205">UpgradedEventEndpoint element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)</span></span>](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="b5204-206">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5204-206">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="b5204-207">Создание удаленного приемника событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="b5204-207">Create an add-in event receiver in SharePoint Add-ins</span></span>](create-an-add-in-event-receiver-in-sharepoint-add-ins.md)
    
 

