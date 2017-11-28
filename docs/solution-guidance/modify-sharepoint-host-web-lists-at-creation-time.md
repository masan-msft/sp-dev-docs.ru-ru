---
title: "Изменение списков web узла SharePoint во время создания"
ms.date: 11/03/2017
ms.openlocfilehash: fd4849672053fe1a368cb7f05814575a055f15c5
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="modify-sharepoint-host-web-lists-at-creation-time"></a><span data-ttu-id="4c5d3-102">Изменение списков web узла SharePoint во время создания</span><span class="sxs-lookup"><span data-stu-id="4c5d3-102">Modify SharePoint host web lists at creation time</span></span>

<span data-ttu-id="4c5d3-103">Изменение списка SharePoint, созданных в веб-узла во время создания списка.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-103">Modify a SharePoint list created in the host web at list creation time.</span></span>

<span data-ttu-id="4c5d3-104">_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="4c5d3-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="4c5d3-105">При создании нового списка на хост- **ListAdded** удаленного приемника событий можно использовать для изменения этого списка.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-105">When you create a new list in the host web, you can use a **ListAdded** remote event receiver to modify that list.</span></span> <span data-ttu-id="4c5d3-106">Например можно включить управление версиями, или добавить тип контента в список или внести все изменения, реализованные с клиентской объектной модели (CSOM).</span><span class="sxs-lookup"><span data-stu-id="4c5d3-106">For example, you can enable versioning, or add a content type to the list, or make any other changes implemented by the client object model (CSOM).</span></span>

<span data-ttu-id="4c5d3-107">При добавлении списка веб-сайт, необходимо программным путем присоединения приемника событий.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-107">When the list is added to the host web, you need to programmatically attach the event receiver.</span></span> <span data-ttu-id="4c5d3-108">Пример [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) показано, как использовать размещение у поставщика в надстройке для этого.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-108">The [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) sample shows you how to use a provider-hosted add-in to do this.</span></span> <span data-ttu-id="4c5d3-109">При установке надстройки происходит событие **AppInstalled** и использовать это событие для присоединения событий **ListAdded** .</span><span class="sxs-lookup"><span data-stu-id="4c5d3-109">When the add-in is installed, an **AppInstalled** event occurs, and you use this event to attach the **ListAdded** event.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4c5d3-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4c5d3-110">Before you begin</span></span>

<span data-ttu-id="4c5d3-111">Чтобы начать работу, загрузите пример надстройки [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-111">To get started, download the [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="attach-the-listadded-event"></a><span data-ttu-id="4c5d3-112">Событие ListAdded с подключением</span><span class="sxs-lookup"><span data-stu-id="4c5d3-112">Attach the ListAdded event</span></span>

<span data-ttu-id="4c5d3-113">Реализация обработчиков событий для надстройки, отображения свойств для проекта SharePoint и задать **дескриптор надстройка установлена** и **Удаление надстройки дескриптор** значение **True**.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-113">To implement the event handlers for the add-in, display the properties for the SharePoint project, and set both  **Handle Add-in Installed** and **Handle Add-in Uninstalling** to **True**.</span></span>

<span data-ttu-id="4c5d3-114">В следующем примере кода показано, как изменить приемник событий **AppInstalled** присоединение приемника событий **ListAdded** .</span><span class="sxs-lookup"><span data-stu-id="4c5d3-114">The following code example shows how the  **AppInstalled** event receiver is modified to attach the **ListAdded** event receiver.</span></span>

<span data-ttu-id="4c5d3-115">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-115">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
bool rerExists = false;
cc.Load(cc.Web.EventReceivers);
cc.ExecuteQuery();

foreach (var rer in cc.Web.EventReceivers)
{
  if (rer.ReceiverName == RECEIVER_NAME)
  {
    rerExists = true;
  }
}

if (!rerExists)
{
  EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
  receiver.EventType = EventReceiverType.ListAdded;

  // Get WCF URL where this message was handled.
  OperationContext op = OperationContext.Current;
  Message msg = op.RequestContext.RequestMessage;
  receiver.ReceiverUrl = msg.Headers.To.ToString();
  receiver.ReceiverName = RECEIVER_NAME;
  receiver.Synchronization = EventReceiverSynchronization.Synchronous;
  cc.Web.EventReceivers.Add(receiver);
  cc.ExecuteQuery();
}
```

## <a name="customize-the-added-lists"></a><span data-ttu-id="4c5d3-116">Настройка добавлены списков</span><span class="sxs-lookup"><span data-stu-id="4c5d3-116">Customize the added lists</span></span>

<span data-ttu-id="4c5d3-117">Если срабатывания обработчика событий **ListAdded** выполняется следующий код.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-117">When the  **ListAdded** event handler is firing, the following code runs.</span></span>

```C#
private void HandleListAdded(SPRemoteEventProperties properties)
{
  using (ClientContext cc = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
  {
    if (cc != null)
    {
      try
        {
          if (properties.ListEventProperties.TemplateId == (int)ListTemplateType.DocumentLibrary)
          {
          //set versioning 
   cc.Web.GetListByTitle(properties.ListEventProperties.ListTitle).UpdateListVersioning(true, true);
          }
        }
         catch (Exception ex)
         {
           System.Diagnostics.Trace.WriteLine(ex.Message);
         }
       }
    }
  }
}
```

## <a name="uninstalling-the-event-receiver"></a><span data-ttu-id="4c5d3-118">Удаление приемника событий</span><span class="sxs-lookup"><span data-stu-id="4c5d3-118">Uninstalling the event receiver</span></span>

<span data-ttu-id="4c5d3-119">При удалении надстройки необходимо также удалить приемника событий.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-119">When the add-in is uninstalled, the event receiver should also be removed.</span></span> <span data-ttu-id="4c5d3-120">Этой функции необходимо выполнение во время отладки, перейдите в библиотеку **надстроек в тестирования** и нажмите кнопку **Удалить** на надстройки.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-120">To make this work during debugging, go to the  **Add-ins in testing** library and use the **remove** option on the add-in.</span></span> <span data-ttu-id="4c5d3-121">Это вызывает событие **AppUninstalling** с соответствующими разрешениями, чтобы удалить созданный удаленный обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-121">This triggers the **AppUninstalling** event with the proper permissions to remove the created remote event handler.</span></span> <span data-ttu-id="4c5d3-122">Если вы только что закройте окно браузера, или удалить надстройку из **содержимого сайта**, никогда не включении приемника событий или приемника событий **AppUninstalling** выполняется с недостаточно прав для удаления **ListAdded** приемника событий.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-122">If you just close the browser or uninstall the add-in from **site contents**, either the event receiver never fires or the **AppUninstalling** event receiver runs with insufficient permissions to remove the **ListAdded** event receiver.</span></span> <span data-ttu-id="4c5d3-123">Это время, когда он со стороны загруженных, который делает Visual Studio при нажатии клавиши F5 надстроек развертываются по-разному.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-123">This is because add-ins are deployed differently when they are side loaded, which is what Visual Studio does when you press F5.</span></span>

<span data-ttu-id="4c5d3-124">**Примечание:**  Рекомендуется проверить в этом примере в сайте чистой разработчика.</span><span class="sxs-lookup"><span data-stu-id="4c5d3-124">**Note:**  We recommend that you test this sample in a clean developer site.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c5d3-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4c5d3-125">Additional resources</span></span>
<span data-ttu-id="4c5d3-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4c5d3-126"></span></span>

- [<span data-ttu-id="4c5d3-127">Решения по подготовке сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c5d3-127">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="4c5d3-128">Пример Core.EventReceiversBasedModifications</span><span class="sxs-lookup"><span data-stu-id="4c5d3-128">Core.EventReceiversBasedModifications sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications)
