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
# <a name="create-a-handler-for-the-update-event-in-sharepoint-add-ins"></a><span data-ttu-id="07d87-103">Создание обработчика для события обновления надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="07d87-103">Create a handler for the update event in SharePoint Add-ins</span></span>

<span data-ttu-id="07d87-104">Прежде чем начать, ознакомьтесь с разделом [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) и статьей [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), в том числе с перечисленными в них предварительными требованиями и основными понятиями.</span><span class="sxs-lookup"><span data-stu-id="07d87-104">Be thoroughly familiar with both  [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) and [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in them.</span></span>

> [!NOTE]
> <span data-ttu-id="07d87-105">**Система нумерации версий.** В этой статье предполагается, что версии надстройки имеют следующую нумерацию: 1.0.0.0, 2.0.0.0, 3.0.0.0 и т. д.</span><span class="sxs-lookup"><span data-stu-id="07d87-105">**NoteVersion numbering system:** For consistency, this topic assumes that the add-in version numbers are 1.0.0.0, 2.0.0.0, 3.0.0.0, and so on. However, the logic and guidance applies no matter what your numbering system is.</span></span> <span data-ttu-id="07d87-106">Однако логика и инструкции не зависят от системы нумерации.</span><span class="sxs-lookup"><span data-stu-id="07d87-106">However, the logic and guidance applies no matter what your numbering system is.</span></span>

<span data-ttu-id="07d87-107"><a name="UpgradedEventEndpoint"> </a></span><span class="sxs-lookup"><span data-stu-id="07d87-107"></span></span>
## <a name="create-an-upgradedeventendpoint-receiver"></a><span data-ttu-id="07d87-108">Создание приемника UpgradedEventEndpoint</span><span class="sxs-lookup"><span data-stu-id="07d87-108">Create an UpgradedEventEndpoint receiver</span></span>

<span data-ttu-id="07d87-109">Для пользовательской логики обновления можно создать приемник удаленных событий SharePoint, который обрабатывает событие обновления надстройки.</span><span class="sxs-lookup"><span data-stu-id="07d87-109">For custom update logic, you can create a SharePoint remote event receiver that handles the add-in updated event.</span></span> <span data-ttu-id="07d87-110">Этот метод следует применять осторожно.</span><span class="sxs-lookup"><span data-stu-id="07d87-110">You should be conservative in using this technique.</span></span> <span data-ttu-id="07d87-111">Используйте его только для действий, которые нельзя выполнить по-другому.</span><span class="sxs-lookup"><span data-stu-id="07d87-111">Use it only for updating steps that can't be done any other way.</span></span> <span data-ttu-id="07d87-112">Кроме того, инструкции из раздела [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) применимы к событию обновления надстройки так же, как и к событиям ее установки и удаления.</span><span class="sxs-lookup"><span data-stu-id="07d87-112">Also, the guidance found in [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) applies for the add-in updated event as much as the add-in installed and add-in uninstalling events.</span></span> <span data-ttu-id="07d87-113">В частности:</span><span class="sxs-lookup"><span data-stu-id="07d87-113">This includes co-owners.</span></span>

- <span data-ttu-id="07d87-114">Обработчик должен завершить работу и вернуть в SharePoint состояние отмены или продолжения в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="07d87-114">Your handler has to complete and return either a cancel or a continue status to SharePoint in 30 seconds. If it does not, SharePoint will re-call the handler, up to three more times.</span></span> <span data-ttu-id="07d87-115">В противном случае SharePoint вызовет обработчик повторно (до трех раз).</span><span class="sxs-lookup"><span data-stu-id="07d87-115">If it does not, SharePoint calls the handler again up to three more times.</span></span>

- <span data-ttu-id="07d87-116">Если обработчик вернет состояние отмены, SharePoint выполнит еще три попытки.</span><span class="sxs-lookup"><span data-stu-id="07d87-116">If your handler returns a cancel status, SharePoint will retry up to three more times.</span></span> 

- <span data-ttu-id="07d87-117">Как правило, следует включать в обработчик логику отката и проверки выполненных действий.</span><span class="sxs-lookup"><span data-stu-id="07d87-117">You usually need to include rollback and "already done" logic in your handler.</span></span>

<span data-ttu-id="07d87-p104">Один из сценариев, при котором удобно использовать обработчик **UpgradedEventEndpoint**, когда в удаленную базу данных добавляется вычисляемое поле. Предположим, добавляется столбец "Город" и его значение вычисляется из уже существующего столбца "Почтовый индекс". Ваш код в обработчике **UpgradedEventEndpoint** может итеративно перебирать существующие элементы в базе данных и вставлять значения в новые поля "Город" на основе значений в полях "Почтовый индекс" и внешнего источника данных, который сопоставляет индексы с городами. Изменения самой схемы базы данных лучше вносить за пределами обработчика **UpgradedEventEndpoint**, используя лучшие методики для определенной платформы базы данных.</span><span class="sxs-lookup"><span data-stu-id="07d87-p104">One scenario in which an **UpgradedEventEndpoint** handler is useful is when a computed field is added to a remote database. Suppose a City column is added, and its value is computed from an already existing Postal Code column. Your code in an **UpgradedEventEndpoint** handler could iterate through existing items in the database and fill in the value for the new City field based on the value of the Postal Code field and some external data source that maps postal codes onto cities. The change to the database schema itself is best done outside the **UpgradedEventEndpoint** handler by using the best practices of the database platform.</span></span>

<span data-ttu-id="07d87-122">Инструкции по создании обработчика для события надстройки см. в статьях [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md) и [Создание приемника событий надстройки в надстройках для SharePoint](create-an-add-in-event-receiver-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="07d87-122">For more details about how to create a handler for the add-in event, see  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md) and [Create an add-in event receiver in SharePoint Add-ins](create-an-add-in-event-receiver-in-sharepoint-add-ins.md). The following procedure assumes that you have added the add-in event receiver item to your SharePoint Add-in project in Visual Studio.</span></span> 

<span data-ttu-id="07d87-123">В приведенной ниже процедуре предполагается, что вы добавили приемник удаленных событий в свой проект надстройки SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07d87-123">For more details about how to create a handler for the add-in event, see  Handle events in SharePoint Add-ins and Create an add-in event receiver in SharePoint Add-ins. The following procedure assumes that you have added the add-in event receiver item to your SharePoint Add-in project in Visual Studio.</span></span> 

### <a name="to-handle-the-add-in-updated-event-the-first-time"></a><span data-ttu-id="07d87-124">Обработка первого события обновления надстройки</span><span class="sxs-lookup"><span data-stu-id="07d87-124">To handle the add-in updated event the first time</span></span>

1. <span data-ttu-id="07d87-125">Откройте файл AppEventReceiver.svc.cs и добавьте в метод **ProcessEvent** условную структуру, проверяющую, является ли событие, которое вызвало обработчик, событием обновления.</span><span class="sxs-lookup"><span data-stu-id="07d87-125">Open the AppEventReceiver.svc.cs file, and add a conditional structure to the **ProcessEvent** method that tests whether the event that invoked the handler is the updated event.</span></span> <span data-ttu-id="07d87-126">Код обновления добавляется внутрь этой структуры.</span><span class="sxs-lookup"><span data-stu-id="07d87-126">Your updating code goes inside this structure.</span></span> <span data-ttu-id="07d87-127">Если коду требуется доступ к SharePoint, можете использовать клиентскую объектную модель (CSOM) для управляемого кода SharePoint или интерфейс REST.</span><span class="sxs-lookup"><span data-stu-id="07d87-127">If your code needs to access SharePoint, you can use the SharePoint managed code client object model (CSOM) or Representational State Transfer (REST) interface.</span></span> 

   <span data-ttu-id="07d87-128">Расположение условной структуры зависит от структуры другого кода в методе.</span><span class="sxs-lookup"><span data-stu-id="07d87-128">Where the conditional structure is located in the method depends on how you have structured the other code in the method.</span></span> <span data-ttu-id="07d87-129">Обычно она находится рядом со аналогичными условными структурами, проверяющими события установки и удаления надстройки.</span><span class="sxs-lookup"><span data-stu-id="07d87-129">Typically, it is a peer of similar conditional structures that test for the add-in installed and add-in uninstalling events.</span></span> <span data-ttu-id="07d87-130">Она может находиться в условной структуре, которая проверяет определенные свойства или подсвойства объекта **SPRemoteEventProperties**, который передается в метод **ProcessEvent** при значениях **Null** или других недопустимых значениях.</span><span class="sxs-lookup"><span data-stu-id="07d87-130">It may be within a conditional structure that tests certain properties or subproperties of the **SPRemoteEventProperties** object that is passed to **ProcessEvent** for **null** values or other invalid values.</span></span> <span data-ttu-id="07d87-131">Она также может находиться в блоке **try**.</span><span class="sxs-lookup"><span data-stu-id="07d87-131">It may also be within a **try** block.</span></span> 
   
   <span data-ttu-id="07d87-132">Ниже представлен пример структуры.</span><span class="sxs-lookup"><span data-stu-id="07d87-132">The following is an example of calling the script:</span></span> <span data-ttu-id="07d87-133">Объект _properties_ — это объект **SPRemoteEventProperties**.</span><span class="sxs-lookup"><span data-stu-id="07d87-133">The _properties_ object is an **SPRemoteEventProperties** object.</span></span>
    
    ```C#
       if (properties.EventType == SPRemoteEventType.AppUpgraded)
     {
     }

    ```

2. <span data-ttu-id="07d87-134">Чтобы использовать CSOM в обработчике, добавьте (внутри условного блока) блок **using**, который получает объект **ClientContext**, вызывая метод **TokenHelper.CreateAppEventClientContext**.</span><span class="sxs-lookup"><span data-stu-id="07d87-134">To use CSOM in the handler, add (within the conditional block) a  **using** block that gets a **ClientContext** object by calling the **TokenHelper.CreateAppEventClientContext** method. Specify true for the second parameter to access the add-in web. Specify false to access the host web. If you need to access both, you will need two different client context objects.</span></span> <span data-ttu-id="07d87-135">Для доступа к сайту надстройки задайте для второго параметра значение **true**.</span><span class="sxs-lookup"><span data-stu-id="07d87-135">Specify **true** for the second parameter to access the add-in web.</span></span> <span data-ttu-id="07d87-136">Для доступа к хост-сайту задайте значение **false**.</span><span class="sxs-lookup"><span data-stu-id="07d87-136">Specify **false** to access the host web.</span></span> <span data-ttu-id="07d87-137">Для доступа к обоим сайтам требуются два отдельных контекста клиента.</span><span class="sxs-lookup"><span data-stu-id="07d87-137">If you need to access both, you need two different client context objects.</span></span>

3. <span data-ttu-id="07d87-p109">Если обработчику нужен доступ к компонентам, расположенным не в SharePoint, поместите этот код за пределами всех блоков контекста клиента. Код должен иметь следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="07d87-p109">If your handler needs to access non-SharePoint components, put that code outside any client context blocks. Your code should be structured similarly to the following:</span></span>
    
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

4. <span data-ttu-id="07d87-p110">Для использования интерфейса REST ваш код с помощью других методов в классе **TokenHelper** получает маркер доступа, который потом включается в запросы, отправляемые им SharePoint. Подробнее см. в статье [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md). Код должен иметь следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="07d87-p110">To use the REST interface, your code uses other methods in the **TokenHelper** class to get an access token, which is then included in the requests it makes to SharePoint. For more information, see [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md). Your code should be structured similarly to the following.</span></span>
    
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

5. <span data-ttu-id="07d87-143">Для доступа к SharePoint в коде REST также необходимо указать URL-адрес хост-сайта или сайта надстройки (или и того, и другого).</span><span class="sxs-lookup"><span data-stu-id="07d87-143">To access SharePoint, your REST code also needs to know the URL of the host web or add-in web or both. These URLs are both subproperties of the  SPRemoteEventProperties object that is passed to the ProcessEvent method. The following code shows how to get them.</span></span> <span data-ttu-id="07d87-144">Эти URL-адреса являются подсвойствами объекта **SPRemoteEventProperties**, передаваемого методу **ProcessEvent**.</span><span class="sxs-lookup"><span data-stu-id="07d87-144">These URLs are both subproperties of the **SPRemoteEventProperties** object that is passed to the **ProcessEvent** method.</span></span> <span data-ttu-id="07d87-145">Вот код, который позволяет их получить:</span><span class="sxs-lookup"><span data-stu-id="07d87-145">The following code shows how to get the lab editor.</span></span>
    
    ```C#
       Uri hostWebURL = properties.AppEventProperties.HostWebFullUrl;
       Uri appWebURL = properties.AppEventProperties.AppWebFullUrl;
    ```

<span data-ttu-id="07d87-p112">Когда вы обновляете надстройку во второй (или третий и т. д.) раз, может потребоваться сделать так, чтобы логика обновления не выполнялась много раз на одном и том же экземпляре надстройки. Ниже приведена процедура, позволяющая это сделать.</span><span class="sxs-lookup"><span data-stu-id="07d87-p112">When you update an add-in for the second (or third, and so on) time, you may need to ensure that some update logic does not run multiple times on the same add-in instance. The following procedure shows you how.</span></span>

### <a name="to-handle-the-add-in-updated-event-on-subsequent-updates"></a><span data-ttu-id="07d87-148">Обработка события обновления надстройки при последующих обновлениях</span><span class="sxs-lookup"><span data-stu-id="07d87-148">To handle the add-in updated event on subsequent updates</span></span>

1. <span data-ttu-id="07d87-149">Откройте файл AppEventReceiver.svc.cs и найдите код первого обновления (с версии 1.0.0.0</span><span class="sxs-lookup"><span data-stu-id="07d87-149">Open the AppEventReceiver.svc.cs file, and find the code that implemented update actions in the first update (from 1.0.0.0.</span></span> <span data-ttu-id="07d87-150">до версии 2.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="07d87-150">to 2.0.0.0).</span></span> <span data-ttu-id="07d87-151">Назовем его кодом предыдущего обновления.</span><span class="sxs-lookup"><span data-stu-id="07d87-151">Let's call this the previous update code.</span></span> <span data-ttu-id="07d87-152">(Этот код обычно расположен после кода авторизации, который получает контекст клиента или маркеры доступа.) При обновлении с версии 2.0.0.0 до версии 3.0.0.0 в коде предыдущего обновления, скорее всего, будут действия, которые не нужно выполнять снова для того же экземпляра надстройки, но нужно выполнять для экземпляра надстройки, не обновленной до версии 2.0.0.0 (в таком случае экземпляр обновляется с версии 1.0.0.0</span><span class="sxs-lookup"><span data-stu-id="07d87-152">Open the AppEventReceiver.svc.cs file, and find the code that implemented update actions in the first update (from 1.0.0.0. to 2.0.0.0). Let's call this the previous update code. (This code is generally located after the authorization code that gets client context or access tokens.) Now that you are updating again (from 2.0.0.0 to 3.0.0.0), there will typically be actions in the previous update code here that you don't want to run again on the same add-in instance, but you do want it to run on a add-in instance that was never updated to 2.0.0.0 (in which case, the instance is now being updated all the way from 1.0.0.0. to 3.0.0.0).</span></span> <span data-ttu-id="07d87-153">до версии 3.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="07d87-153">to 3.0.0.0).</span></span>

2. <span data-ttu-id="07d87-154">Поместите код предыдущего обновления в условную структуру, которая проверяет предыдущую версию экземпляра надстройки и выполняется, только если код в структуре еще не запускался для этого экземпляра надстройки.</span><span class="sxs-lookup"><span data-stu-id="07d87-154">Wrap the previous update code in a conditional structure that tests for the previous version of the add-in instance and executes only if the code in the structure has not run before on this add-in instance. The previous version of the instance is stored in the  PreviousVersion subproperty of the SPRemoteEventProperties object.</span></span> <span data-ttu-id="07d87-155">Предыдущая версия экземпляра хранится в подсвойстве **PreviousVersion** объекта **SPRemoteEventProperties**.</span><span class="sxs-lookup"><span data-stu-id="07d87-155">The previous version of the instance is stored in the **PreviousVersion** subproperty of the **SPRemoteEventProperties** object.</span></span>

3. <span data-ttu-id="07d87-156">Добавьте новую логику обновления (для обновления с версии 2.0.0.0 до версии 3.0.0.0) после этой структуры.</span><span class="sxs-lookup"><span data-stu-id="07d87-156">Add your new update logic (for the update from 2.0.0.0 to 3.0.0.0) below this structure. The following is an example.</span></span> <span data-ttu-id="07d87-157">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="07d87-157">The following is an example.</span></span>
    
    ```C#
       Version ver2OOO = new Version("2.0.0.0");
     if (properties.AppEventProperties.PreviousVersion < ver2OOO)
     {
         // Code to update from 1.0.0.0 to 2.0.0.0 (previous update code) is here.
     }
     // Code to update from 2.0.0.0 to 3.0.0.0 is here.

    ```

4. <span data-ttu-id="07d87-p116">Повторите эти действия для каждого последующего обновления. Ниже представлена структура кода для обновления с версии 3.0.0.0 до версии 4.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="07d87-p116">For each subsequent update, repeat these steps. For the update from 3.0.0.0 to 4.0.0.0, your code should have the following structure.</span></span>
    
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
> <span data-ttu-id="07d87-160">Если вы добавляете компонент в надстройку в обработчике **UpgradedEventEndpoint**, обязательно добавьте такой же код в обработчик **InstalledEventEndpoint**, чтобы этот компонент имелся и в заново установленной настройке.</span><span class="sxs-lookup"><span data-stu-id="07d87-160">If you add a component to an add-in in an **UpgradedEventEndpoint** handler, be sure to add the same code to an **InstalledEventEndpoint** handler because you want that component included in the add-in on a brand new installation as well.</span></span> <span data-ttu-id="07d87-161">Кроме того, необходимо добавить (или изменить) обработчик [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx), чтобы надстройка удалила компонент.</span><span class="sxs-lookup"><span data-stu-id="07d87-161">Also, you should add an [UninstallingEventEndpoint](http://msdn.microsoft.com/library/4194e44b-f2af-1db4-aad5-9b7b511b4348%28Office.15%29.aspx) (or revise it) for the add-in to remove the component.</span></span> 

> <span data-ttu-id="07d87-162">Все добавления и изменения, внесенные обработчиком **InstalledEventEndpoint**, должны отменяться или удаляться обработчиком **UninstallingEventEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="07d87-162">For the most part, anything that was added or changed by the **InstalledEventEndpoint** should be reversed or deleted by the **UninstallingEventEndpoint**.</span></span> <span data-ttu-id="07d87-163">Не следует удалять только данные, которые понадобятся после удаления надстройки со второго уровня корзины.</span><span class="sxs-lookup"><span data-stu-id="07d87-163">One exception is that data that will remain useful after the add-in is removed from the second-stage recycle bin should not be deleted.</span></span> <span data-ttu-id="07d87-164">(Данными также считаются созданные надстройкой веб-сайты, за исключением сайта надстройки.)</span><span class="sxs-lookup"><span data-stu-id="07d87-164">(Websites, other than the add-in web, that are created by the add-in should be considered data.)</span></span>

<span data-ttu-id="07d87-165"><a name="AddRollbackLogic"> </a></span><span class="sxs-lookup"><span data-stu-id="07d87-165"></span></span>
## <a name="add-rollback-logic-to-the-handler"></a><span data-ttu-id="07d87-166">Добавление логики отката в обработчик</span><span class="sxs-lookup"><span data-stu-id="07d87-166">Add rollback logic to the handler</span></span>

<span data-ttu-id="07d87-167">Если при обновлении надстройки возникает ошибка, инфраструктура SharePoint останавливает процесс и откатывает экземпляр надстройки и все его компоненты до предыдущей версии.</span><span class="sxs-lookup"><span data-stu-id="07d87-167">If an error occurs when an add-in is being updated, the SharePoint infrastructure stops the update process and rolls back the add-in instance and all its components to the previous version of the add-in instance.</span></span> <span data-ttu-id="07d87-168">Но инфраструктура не знает, какие действия выполняет обработчик **UpgradedEventEndpoint**, поэтому не всегда может их отменить.</span><span class="sxs-lookup"><span data-stu-id="07d87-168">But the infrastructure has no way of knowing what your **UpgradedEventEndpoint** handler logic does, so it can't always undo it.</span></span> <span data-ttu-id="07d87-169">Необработанное исключение при выполнении обработчика **UpgradedEventEndpoint** почти всегда означает, что необходимо откатить все обновление надстройки. Но этого не происходит, потому что инфраструктура не знает, как отменить некоторые действия, выполненные кодом обработчика **UpgradedEventEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="07d87-169">An unhandled exception thrown while your **UpgradedEventEndpoint** handler is executing almost certainly indicates that the entire add-in update process should be rolled back, but it won't be because the infrastructure doesn't know how to undo some things that your **UpgradedEventEndpoint** code might have done.</span></span> <span data-ttu-id="07d87-170">Поэтому код **UpgradedEventEndpoint** должен:</span><span class="sxs-lookup"><span data-stu-id="07d87-170">For this reason, the **UpgradedEventEndpoint** code must:</span></span>

- <span data-ttu-id="07d87-171">перехватывать все исключения;</span><span class="sxs-lookup"><span data-stu-id="07d87-171">Catch all exceptions.</span></span>
    
- <span data-ttu-id="07d87-172">передавать управление пользовательскому коду отката для отмены всех выполненных действий;</span><span class="sxs-lookup"><span data-stu-id="07d87-172">Branch to custom rollback code to undo what it has been done to that point.</span></span>
    
- <span data-ttu-id="07d87-173">сообщать инфраструктуре SharePoint, что необходимо откатить все обновление надстройки;</span><span class="sxs-lookup"><span data-stu-id="07d87-173">Signal to the SharePoint infrastructure that the entire add-in update should be rolled back.</span></span>
    
- <span data-ttu-id="07d87-174">передавать инфраструктуре сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="07d87-174">Pass on an error message to the infrastructure.</span></span>

<span data-ttu-id="07d87-175">Не все действия, выполняемые обработчиком **UpgradedEventEndpoint**, необходимо явно отменять в обработчике.</span><span class="sxs-lookup"><span data-stu-id="07d87-175">Not everything your **UpgradedEventEndpoint** does needs to be explicitly reversed inside the handler.</span></span> <span data-ttu-id="07d87-176">Сайт надстройки откатывается инфраструктурой, поэтому вашему коду не нужно отменять внесенные в него изменения.</span><span class="sxs-lookup"><span data-stu-id="07d87-176">The add-in web is going to be rolled back by the infrastructure, so your code does not have to undo changes to the add-in web.</span></span> <span data-ttu-id="07d87-177">Но обработчик **UpgradedEventEndpoint**, как правило, должен отменять изменения, внесенные им в хост-сайт или другие внешние компоненты.</span><span class="sxs-lookup"><span data-stu-id="07d87-177">But the **UpgradedEventEndpoint** handler usually does have to reverse the changes it has made to the host web or other components that are external to the SharePoint Add-in.</span></span>

<span data-ttu-id="07d87-p121">При втором (или третьем и т. д.) обновлении ваша логика обработки обновлений должна учитывать, что обновляемый экземпляр надстройки не обязательно является непосредственно предыдущей версией. Если это не так, может понадобиться два или больше блоков кода обновления, которые нужно обратить. Для этого требуется условная логика, основанная на номере предыдущей версии. Ниже приведен пример логики отката для обновления до версии 4.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="07d87-p121">On the second (or third, and so on) update, your exception handing logic has to take account of the fact that the add-in instance that is being updated is not necessarily the immediately previous version. If it isn't, there may be two or more blocks of update code that need to be reversed. For this reason, you need conditional logic that is based on the number of the previous version. The following is an example of the rollback logic for an update to version 4.0.0.0.</span></span>

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

<span data-ttu-id="07d87-182">На последнем этапе обработки ошибки необходимо назначить сообщение об ошибке и состояние отмены объекту **SPRemoteEventResult**, который метод **ProcessEvent** возвращает инфраструктуре обновления SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07d87-182">The last things your error handling should do is assign an error message and a cancel status to the  **SPRemoteEventResult** object that the **ProcessEvent** method returns to the SharePoint update infrastructure. The following is an example. In this code, result is an SPRemoteEventResult object that has been declared earlier in the ProcessEvent method.</span></span> <span data-ttu-id="07d87-183">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="07d87-183">The following is an example.</span></span> <span data-ttu-id="07d87-184">В этом коде _result_ представляет собой объект **SPRemoteEventResult**, ранее объявленный в методе **ProcessEvent**.</span><span class="sxs-lookup"><span data-stu-id="07d87-184">In this code, _result_ is an **SPRemoteEventResult** object that has been declared earlier in the **ProcessEvent** method.</span></span>

```C#
catch (Exception e)
{     
    result.ErrorMessage = "custom message " + e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;

     // Rollback logic from the preceding code snippet  is here. 

}
```

> [!IMPORTANT]
> <span data-ttu-id="07d87-185">Очень важно назначить **SPRemoteEventServiceStatus.CancelWithError** (или **SPRemoteEventServiceStatus.CancelNoError**) свойству **Status**.</span><span class="sxs-lookup"><span data-stu-id="07d87-185">Assigning **SPRemoteEventServiceStatus.CancelWithError** (or **SPRemoteEventServiceStatus.CancelNoError**) to the **Status** property is crucial.</span></span> <span data-ttu-id="07d87-186">Это свойство сообщает инфраструктуре, что нужно откатить обновление.</span><span class="sxs-lookup"><span data-stu-id="07d87-186">This property is what signals the infrastructure to roll back the update.</span></span> <span data-ttu-id="07d87-187">Но до отката SharePoint еще трижды попытается запустить обработчик.</span><span class="sxs-lookup"><span data-stu-id="07d87-187">But SharePoint will retry your handler three times before it rolls back the update.</span></span>

### <a name="use-the-handler-delegation-strategy"></a><span data-ttu-id="07d87-188">Использование стратегии делегирования обработчиков</span><span class="sxs-lookup"><span data-stu-id="07d87-188">Use the handler delegation strategy</span></span>

<span data-ttu-id="07d87-189">Стратегию делегирования обработчиков, описанную в разделе [Обработка событий надстройки](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents), можно использовать и в **UpdatedEventHandler**.</span><span class="sxs-lookup"><span data-stu-id="07d87-189">The handler delegation strategy that is described in [Handling add-in events](handle-events-in-sharepoint-add-ins.md#HandlingAppEvents) can be used in an **UpdatedEventHandler** too.</span></span> <span data-ttu-id="07d87-190">На удаленном компьютере выполняется не только логика отката вместе с логикой проверки выполненных действий, но и логика управления версиями.</span><span class="sxs-lookup"><span data-stu-id="07d87-190">Not only is your rollback and "already done" logic bundled and run on the remote component, but your versioning logic is too.</span></span> <span data-ttu-id="07d87-191">Ограничения применяются и здесь: как правило, эту стратегию нельзя использовать для обновления нескольких удаленных систем.</span><span class="sxs-lookup"><span data-stu-id="07d87-191">The limitations of the strategy apply here too; you usually can't use it to update more than one remote system.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07d87-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07d87-192">Next steps</span></span>

<span data-ttu-id="07d87-193">Вернитесь к разделу [Основные шаги по обновлению надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из указанных ниже статей, чтобы узнать, как обновить компоненты надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07d87-193">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>

-  [<span data-ttu-id="07d87-194">Обновление компонентов сайта надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="07d87-194">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
-  [<span data-ttu-id="07d87-195">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="07d87-195">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
-  <span data-ttu-id="07d87-196">[Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins.md) </span><span class="sxs-lookup"><span data-stu-id="07d87-196">[Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07d87-197">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="07d87-197">Additional resources</span></span>

-  [<span data-ttu-id="07d87-198">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="07d87-198">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
-  [<span data-ttu-id="07d87-199">Элемент UpgradedEventEndpoint (PropertiesDefinition complexType, манифест надстройки SharePoint)</span><span class="sxs-lookup"><span data-stu-id="07d87-199">UpgradedEventEndpoint element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)</span></span>](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx)
-  [<span data-ttu-id="07d87-200">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="07d87-200">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
-  [<span data-ttu-id="07d87-201">Создание удаленного приемника событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="07d87-201">Create an add-in event receiver in SharePoint Add-ins</span></span>](create-an-add-in-event-receiver-in-sharepoint-add-ins.md)
    
 

