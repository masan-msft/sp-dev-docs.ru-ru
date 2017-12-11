---
title: "С помощью командлета связывания Register-SPWorkflowService"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 91fca6c2-60ca-4177-8560-2b310dac0e2c
ms.openlocfilehash: 93941c54931812e0333c2297705d5196dff164a6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="using-the-pairing-cmdlet-register-spworkflowservice"></a>С помощью командлета связывания Register-SPWorkflowService
Узнайте, как использовать командлет **Register-SPWorkflowService** успешно связать SharePoint с помощью диспетчера рабочих процессов.
Установка и настройка Microsoft SharePoint для поддержки разработки рабочего процесса требуется «связывания» установок SharePoint и рабочих процессов. В большинстве случаев этот связывания легко выполняется с помощью командлета **Register-SPWorkflowService**, входящий в состав установки SharePoint.
  
    
    

Важно этот командлет не полезен для каждой пары сценария. **Register-SPWorkflowService** можно использовать только в следующих сценариях связывания:
- Ферма серверов один компьютер, где SharePoint и рабочих процессов совместное размещение на сервере.
    
  
- Ферма серверов три компьютера, где SharePoint и рабочих процессов совместное размещение на всех трех компьютерах. (Добавить четвертый компьютер потребностей поиска должна находиться на отдельном компьютере и высокой ДОСТУПНОСТИ диспетчера рабочих процессов является обязательным. Если второй является обязательным, его следует установить на всех трех компьютерах.
    
  
- Три компьютера фермы SharePoint в сочетании с фермы серверов не находится уведомлений диспетчера рабочих процессов.
    
  
Также Обратите внимание, что этот **Register-SPWorkflowService** используются учетные данные текущего пользователя.
## <a name="cmdlet-design"></a>Командлет разработки





|**Данные**|**Описание**|
|:-----|:-----|
|Глагол  <br/> |Регистрация  <br/> |
|Существительное  <br/> |SPWorkflowService  <br/> |
|Описание  <br/> |Работает в ферме sps15short с Workflow Manager фермы. Этот командлет необходимо выполнить один раз на каждой ферме. Перед запуском командлета, необходимо установить сертификат корневого центра сертификации в хранилище сертификатов компьютера и хранилища сертификатов SharePoint. Чтобы сделать это, используйте командлет **New-SPTrustedRootAuthority**. (См. инструкции ниже).<br/> |
|Тип вывода  <br/> |Нет.  <br/> |
|Синтаксис  <br/> | `Register-SPWorkflowService -SPSite <URI or GUID representing an SPSite object> -WorkflowHostUri <workflow service endpoint URL> -ScopeName <string> [-PartitionMode] [-AllowOAuthHttp] [-Force]` <br/> |
   

## <a name="cmdlet-parameters"></a>Параметры командлета



|**Параметр**|**Тип**|**Описание**|
|:-----|:-----|:-----|
|SPSite          (обязательный)  <br/> |**SPSitePipeBind** <br/> |URL-адрес семейства веб-сайтов в ферме SharePoint Server, который выступает в качестве конечной точке связывания длительный. Сведения для связывания выводится из этот URL-адрес.  <br/> |
|WorkflowHostUri          (Required)  <br/> |Строка  <br/> |URL-адрес конечной точки Workflow Manager для связывания. Предоставляет узла рабочего процесса URI и номер порта.  <br/> |
|ScopeName  <br/> |Строка  <br/> |Имя для использования службы рабочих процессов для идентификации парного SharePoint Server фермы. Значение по умолчанию  «SharePoint». Необходимо указать этот параметр, если связь нескольких фермах SharePoint в ферму Workflow Manager.  <br/> |
|PartitionMode  <br/> |SwitchParameter  <br/> |Этот параметр используется только для фермы SharePoint несколькими клиентами. В режиме секционирования указан для службы SharePoint. Обратите внимание на то, что одним экземпляром нескольких клиентов можно создать в ферме SharePoint после выполнения этого командлета; Таким образом командлет не может вывести значение этого параметра неявно из существующих состояний в ферме SharePoint.  <br/> |
|AllowOAuthHttp  <br/> |SwitchParameter  <br/> |Позволяет OAuth и метаданные exchange по протоколу HTTP. Эта функция особенно полезна при тестировании, но не в рабочий режим. Этот параметр используется только в том случае, если SharePoint настроен для поддержки HTTP. Нет необходимости настроить Workflow Manager на использование протокола HTTP.  <br/> |
|Force  <br/> |SwitchParameter  <br/> |Обеспечивает создание области с использованием параметра  _ScopeName_ или обновляет соответствующие же _ScopeName_существующей области. Если не указан, а область с таким же именем существует, командлета возникает ошибка. <br/> |
   

## <a name="example"></a>Пример


```

PS> Register-SPWorkflowService -SPSite "https://myserver/mysitecollection" -WorkflowHostUri "http://workflow.example.com:12291" -ScopeName "SharePoint2" -PartitionMode -AllowOAuthHttp  -Force
```


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Установка и настройка рабочих процессов для SharePoint](http://technet.microsoft.com/en-us/library/jj658588.aspx)
    
  
-  [Серия: Установка и настройка рабочего процесса в SharePoint](http://technet.microsoft.com/en-us/library/dn201724.aspx)
    
  
-  [Диспетчер рабочих процессов версии 1.0](http://msdn.microsoft.com/en-us/library/jj193528%28Azure.10%29)
    
  
