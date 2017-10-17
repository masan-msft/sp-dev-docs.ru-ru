---
title: "Обновление удаленных компонентов в надстройках SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a15890881bb4269ef21e5a2f22865509e9834750
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-remote-components-in-sharepoint-add-ins"></a>Обновление удаленных компонентов в надстройках SharePoint
Узнайте, как обновлять удаленные веб-приложения и базы данных в надстройках SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="prerequisites-for-updating-the-remote-components-of-a-sharepoint-add-in"></a>Необходимые условия для обновления удаленных компонентов надстройки SharePoint
<a name="Prerequistes"> </a>

Ознакомьтесь со статьей [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), в том числе с перечисленными в ней предварительными требованиями и основными понятиями.
 

 

## <a name="update-remote-components"></a>Обновление удаленных компонентов
<a name="UpdateRemote"> </a>

В связи с большим количеством различий между платформами и клиентскими системами в целом можно предоставить только очень общие рекомендации по обновлению удаленных компонентов. В следующих двух разделах приведены некоторые инструкции.
 

 

### <a name="update-remote-components-in-a-provider-hosted-add-in"></a>Обновление удаленных компонентов в надстройке, размещаемой у поставщика
<a name="UpdateProviderHosted"> </a>

Для обновления удаленных компонентов надстройки SharePoint с размещением у поставщика следует использовать лучшие процедуры обновления платформы, на которой размещены компоненты. Точно так же как удаленные компоненты надстройки с размещением у поставщика установлены отдельно от самой надстройки SharePoint, обновляются они тоже отдельно. При этом необходимо помнить о следующем.
 

 

- Обновленные удаленные компоненты должны продолжать функционировать со всеми предыдущими версиями надстройки SharePoint.
    
 
- Если для своих удаленных компонентов вы внедрили систему обособления клиента, помните, что различные клиенты могут использовать несколько версий надстройки, а для отдельных клиентов даже могут быть установлены различные версии на различных веб-сайтах SharePoint.
    
 
В случае надстройки SharePoint с размещением у поставщика, которая использует База данных SQL Microsoft Azure или SQL Server, существует несколько методов обновления базы данных. Для начала см. статью  [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).
 

 

## <a name="next-steps"></a>Дальнейшие действия
<a name="Next"> </a>

Вернитесь к разделу  [Основные действия при обновлении надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из следующих статей, чтобы узнать, как обновить следующий важный компонент надстройки SharePoint.
 

 

-  [Обновление компонентов сайта надстройки в SharePoint](update-add-in-web-components-in-sharepoint.md)
    
 
-  [Обновление компонентов хост-сайта в SharePoint](update-host-web-components-in-sharepoint.md)
    
 
-  [Создание обработчика событий обновления для надстроек SharePoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Обновление надстроек SharePoint](update-sharepoint-add-ins.md)
    
 
-  [Процесс обновления надстроек SharePoint](sharepoint-add-ins-update-process.md)
    
 

