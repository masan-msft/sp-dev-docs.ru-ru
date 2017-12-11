---
title: "Настройка среды разработки для BCS в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d83c8a43-49dd-47eb-94d4-23aa2cf71a9a
ms.openlocfilehash: 33956da39dedd23fa5f81ce131d84e22eca9d60f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="setting-up-a-development-environment-for-bcs-in-sharepoint"></a>Настройка среды разработки для BCS в SharePoint
Сведения о настройке среды разработки для разработки решений SharePoint и надстройки SharePoint с помощью Business Connectivity Services (BCS).
Решения SharePoint и надстройки SharePoint можно создать с помощью службы BCS на клиентском компьютере или на компьютере сервера, в зависимости от типа решения, которое создается.
  
    
    


## <a name="building-server-based-solutions-and-sharepoint-add-ins"></a>Разработка решений на стороне сервера и Надстройки SharePoint
<a name="SP15SettingupdevenvBCS_server"> </a>

Как правило большинство решений BCS и приложения будет размещаться в среде сервера. Эти решения сервера и приложения предоставляют наибольшую гибкость со всеми компонентами BCS в SharePoint.
  
    
    
Для решения на основе сервера как правило, лучше разрабатывать решения на локальном компьютере, где установлен SharePoint и, когда решение построения и тестирования, его развертывание на рабочем сервере. Среда разработки можно установить на любом узла рабочей станции или на один или несколько виртуальных компьютеров, работающих под управлением Windows Server 2008 с пакетом обновления 2.
  
    
    

### <a name="setting-up-an-environment-to-build-sharepoint-add-ins"></a>Настройка среды для построения Надстройки SharePoint

Среда, используемая для разработки приложений с BCS  это то же, как для разработки любого Надстройка SharePoint. 
  
    
    
В этой статье описывается установка компонентов разработки среды, включая операционной системы, SharePoint, Visual Studio 2012 и инструменты разработчика Office для Visual Studio 2012, следуйте инструкциям в [Set up общие среды разработки для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="building-client-based-solutions"></a>Разработка решений на базе клиента
<a name="SP15SettingupdevenvBCS_client"> </a>

Решения на основе клиентских включить клиентские приложения Office 2013 для доступа к от внешних данных, решения SharePoint или добавить в SharePoint можно. Это можно сделать при помощи кода с помощью кэш клиента BCS. Клиентские компоненты общаться с BCS через код на стороне клиента и кэш клиента. Благодаря этому сотрудники клиентские приложения Office с большого объема данных, которые доступны через внешние типы контента SharePoint.
  
    
    
Так как эти решения не требуют кода, можно использовать SharePoint Designer 2013 и Office 2013.
  
    
    

## <a name="see-also"></a>См. также
<a name="SP15SettingupdevenvBCS_addresources"> </a>


-  [Настройка локальной среды разработки надстроек SharePoint](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Обзор разработки решений для SharePoint](sharepoint-development-overview.md)
    
  

