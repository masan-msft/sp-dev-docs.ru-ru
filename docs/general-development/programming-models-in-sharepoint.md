---
title: "Модели программирования в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 061985ec-6129-4e91-991b-a72488ce1d34
ms.openlocfilehash: 1c699feb8890d3d171d1c5e251c4417347f3a313
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="programming-models-in-sharepoint"></a>Модели программирования в SharePoint

Вы можете создавать приложения для платформы SharePoint разными способами. Приложения можно разделить на следующие группы в зависимости от средств, используемых для их создания, моделей программирования, методов упаковки и развертывания, а также устройств, на которых они работают.
  
    
    


- Надстройки SharePoint
    
  
- Сайты публикации SharePoint
    
  
- Решения фермы SharePoint
    
  
- Мобильные надстройки для SharePoint
    
  
- Повторно используемые компоненты для SharePoint
    
  
Эти категории  *не*  взаимоисключающие. Например, сайт публикации можно создать как Надстройка SharePoint. В следующих разделах описываются эти категории и представлены сведения о документации для каждой из них.
## <a name="add-ins-for-sharepoint"></a>Надстройки для SharePoint
<a name="Apps"> </a>

Надстройка SharePoint аналогично надстройкам на мобильном устройстве. Это решение для автономной работы, которое выполняет относительно небольшое количество связанных задач, легко устанавливается и удаляется без ошибок. Пользователи могут найти и скачать Надстройки SharePoint из магазина надстроек SharePoint или из корпоративного каталога надстроек своей организации. Надстройка SharePoint может содержать классические компоненты SharePoint, такие как списки, настраиваемые страницы веб-сайта, веб-части, рабочие процессы и типы контента. Но Надстройка SharePoint также может предоставлять доступ к удаленному веб-приложению и удаленным данным в SharePoint. Кроме того, в Надстройка SharePoint могут использоваться компоненты SharePoint и удаленные компоненты. Надстройки SharePoint  это очень надежные приложения, их настраиваемая логика всегда перемещается "вверх" в облако или "вниз" на клиентские компьютеры. Они никогда не выполняются на серверах SharePoint.
  
    
    
Общие сведения о Модель для надстроек SharePoint см. в статье  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx). Дополнительные сведения см. в статьях  [Сравнение надстроек SharePoint с решениями SharePoint](sharepoint-add-ins-compared-with-sharepoint-solutions.md) и [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md).
  
    
    

## <a name="sharepoint-publishing-sites"></a>Сайты публикации SharePoint
<a name="ECM"> </a>

Сайты публикации SharePoint предоставляют удобные возможности публикации контента с высоким уровнем поддержки и соблюдения требований. Они также обеспечивают управление документами, записями, таксономией и типами контента. Дополнительные сведения см. в статье  [Создание сайтов для SharePoint](build-sites-for-sharepoint.md).
  
    
    

## <a name="sharepoint-farm-solutions"></a>Решения фермы SharePoint
<a name="Solutions"> </a>

решения ферм SharePoint  это доверенные расширения SharePoint, настраиваемая логика которых вызывает серверную объектную модель SharePoint и выполняется с полным доверием на серверах SharePoint. Эти решения, в основном, предназначены для специальных расширений администрирования SharePoint, таких как задания таймера, настраиваемые команды Windows PowerShell и расширения центра администрирования. Решения фермы распространяются как пакеты решений SharePoint. Администраторы фермы загружают их в общее хранилище, из которого их можно развернуть. Компоненты решения ферм может работать на уровне фермы, веб-приложения, семейства веб-сайтов или веб-сайта. Дополнительные сведения см. в статье  [Создавайте решения фермы в SharePoint](build-farm-solutions-in-sharepoint.md).
  
    
    

## <a name="mobile-add-ins-for-sharepoint"></a>Мобильные надстройки для SharePoint
<a name="Mobile"> </a>

Приложения для Windows Phone и приложения на базе сторонних мобильных платформ могут получать доступ к веб-сайтам и данным SharePoint. Средства для создания приложений Windows Phone, которые взаимодействуют с SharePoint, доступны для установки в Visual Studio 2010 и Visual Studio 2012. Управляемый API клиента SharePoint доступен только для устройств с Windows Phone. Мобильные устройства, в том числе сторонних производителей, также могут получить доступ к данным SharePoint через конечные точки SharePoint REST или OData. Дополнительные сведения см. в статье  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md).
  
    
    

## <a name="reusable-components-for-sharepoint"></a>Повторно используемые компоненты для SharePoint
<a name="Reuse"> </a>

Платформа SharePoint и Visual Studio 2012 обеспечивают инкапсуляцию и повторное использование элементов приложения, в том числе элементов, созданных с помощью кода, скриптов и XML-разметки. Дополнительные сведения см. в статье  [Создание повторно используемых компонентов для SharePoint](build-reusable-components-for-sharepoint.md).
  
    
    

## <a name="in-this-section"></a>В этом разделе:
<a name="Reuse"> </a>


-  [Создание сайтов для SharePoint](build-sites-for-sharepoint.md)
    
  
-  [Создавайте решения фермы в SharePoint](build-farm-solutions-in-sharepoint.md)
    
  
-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Создание повторно используемых компонентов для SharePoint](build-reusable-components-for-sharepoint.md)
    
  

## <a name="see-also"></a>См. также
<a name="SP15devinSP_addlresources"> </a>


-  [Настройка общей среды разработки для SharePoint](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [Добавление возможностей SharePoint](add-sharepoint-capabilities.md)
    
  
-  [Специальные возможности в SharePoint](accessibility-in-sharepoint.md)
    
  
