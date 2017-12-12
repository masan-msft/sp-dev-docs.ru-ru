---
title: "Изменение списков web узла SharePoint во время создания"
ms.date: 11/03/2017
ms.openlocfilehash: f9febeb90286fd49a28ff543692de62fb10f611a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-host-web-lists-at-creation-time"></a>Изменение списков web узла SharePoint во время создания

Изменение списка SharePoint, созданных в веб-узла во время создания списка.

_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

При создании нового списка на хост- **ListAdded** удаленного приемника событий можно использовать для изменения этого списка. Например можно включить управление версиями, или добавить тип контента в список или внести все изменения, реализованные с клиентской объектной модели (CSOM).

При добавлении списка веб-сайт, необходимо программным путем присоединения приемника событий. Пример [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) показано, как использовать размещение у поставщика в надстройке для этого. При установке надстройки происходит событие **AppInstalled** и использовать это событие для присоединения событий **ListAdded** .

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="attach-the-listadded-event"></a>Событие ListAdded с подключением

Реализация обработчиков событий для надстройки, отображения свойств для проекта SharePoint и задать **дескриптор надстройка установлена** и **Удаление надстройки дескриптор** значение **True**.

В следующем примере кода показано, как изменить приемник событий **AppInstalled** присоединение приемника событий **ListAdded** .

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

## <a name="customize-the-added-lists"></a>Настройка добавлены списков

Если срабатывания обработчика событий **ListAdded** выполняется следующий код.

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

## <a name="uninstalling-the-event-receiver"></a>Удаление приемника событий

При удалении надстройки необходимо также удалить приемника событий. Этой функции необходимо выполнение во время отладки, перейдите в библиотеку **надстроек в тестирования** и нажмите кнопку **Удалить** на надстройки. Это вызывает событие **AppUninstalling** с соответствующими разрешениями, чтобы удалить созданный удаленный обработчик событий. Если вы только что закройте окно браузера, или удалить надстройку из **содержимого сайта**, никогда не включении приемника событий или приемника событий **AppUninstalling** выполняется с недостаточно прав для удаления **ListAdded** приемника событий. Это время, когда он со стороны загруженных, который делает Visual Studio при нажатии клавиши F5 надстроек развертываются по-разному.

> [!NOTE] 
> Рекомендуется проверить в этом примере в сайте чистой разработчика.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Решения по подготовке сайтов SharePoint](sharepoint-site-provisioning-solutions.md)
    
- [Пример Core.EventReceiversBasedModifications](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.EventReceiversBasedModifications)
