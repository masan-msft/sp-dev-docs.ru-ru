---
title: "Настройка среды для разработки мобильных приложений для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: acaf556d-e20d-478d-8c59-2efd8efb9dcb
ms.openlocfilehash: 9c18eb3fa355abd5f96b2620bd0ee8aed825cdb4
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="set-up-an-environment-for-developing-mobile-apps-for-sharepoint"></a>Настройка среды для разработки мобильных приложений для SharePoint

Узнайте о требованиях к системе и настройке среды разработки для мобильных проектов SharePoint.
Минимальная Настройка для работы с SharePoint мобильности проектов требуются сервере под управлением SharePoint (или SharePoint Online учетной записи) и в среде разработки на отдельной клиентской операционной системы. Установка SharePoint на клиентские операционные системы (например, Windows 7) не поддерживается, и установка средства, необходимые для разработки приложений Windows Phone, не поддерживается в операционных системах сервера (например, Windows Server 2008).
  
    
    


## <a name="windows-phone-development-projects-and-sharepoint-server"></a>Проектов разработки для Windows Phone и SharePoint Server
<a name="SP15Setupmobile_winphone"> </a>

Для создания и тестирования приложений Windows Phone, которые взаимодействуют с SharePoint, необходим доступ к серверу под управлением SharePoint или SharePoint Online учетной записи, и требуется достаточные разрешения для сайтов и списков, которые будут использоваться в ваших решений. Мы рекомендуем использовать установки SharePoint Server, предназначенный для тестирования и разработки в качестве целевого сервера при разработке проектов. Используйте SharePoint Server в рабочей среде как целевой сервер только после разработанных решения претерпел достаточно тестирования.
  
    
    
Подробную информацию об установке и настройке SharePoint см в разделе [Продуктов SharePoint](http://technet.microsoft.com/en-us/library/ee428287.aspx) в библиотеке Microsoft TechNet. Сведения о разработке решений с помощью SharePoint Online посетите [Центр ресурсов для разработчиков SharePoint Online](http://msdn.microsoft.com/en-us/sharepoint/gg153540.aspx).
  
    
    
Примеры кода в этой документации предполагается, что разработчик, работающий с примером имеет или можно получить достаточные разрешения на сайтах SharePoint, и списков, чтобы иметь возможность добавлять, изменять и удалять данные.
  
    
    

## <a name="configure-a-client-development-environment-for-sharepoint-mobility-projects"></a>Настройка среды разработки клиента для проектов SharePoint мобильной работы
<a name="SP15Setupmobile_configure"> </a>

Чтобы разработать Надстройки SharePoint для использования на устройствах Windows Phone, необходимо настроить средств разработки на компьютере под управлением клиентской операционной системы, не в операционной системе сервера.
  
    
    

### <a name="configuring-windows-phone-sdk-80"></a>Настройка Windows Phone SDK 8.0

Чтобы разработать Надстройки SharePoint для использования на Windows Phone 8, необходимо настроить средств разработки на компьютере, работающем под управлением версиями клиентов Windows 8 64-разрядных (x 64) или Windows 8 профессиональная. Эмулятора Windows Phone 8 требует Windows 8 Профессиональная и чтобы процессором, поддерживающим преобразования адресов второго уровня (SLAT).
  
    
    

1. Установите на компьютере с поддерживаемой клиентской операционной системы,  [8.0 пакет SDK для Windows Phone](http://www.microsoft.com/en-us/download/details.aspx?id=35471). Windows Phone Software Development Kit (SDK) 8.0 предоставляет средства, необходимые для разработки приложений и игры для Windows Phone 8 и Windows Phone 7.5.
    
    8.0 пакет SDK для Windows Phone  это среда разработки полнофункциональных для создания приложения и игры для Windows Phone 8.0 и Windows Phone 7.5. Пакет SDK для Windows Phone предоставляет изолированный Visual Studio 2012, Express edition для Windows Phone или работает в качестве надстройки для Visual Studio 2012 Professional, Premium или Ultimate выпуски. С помощью пакета SDK можно использовать имеющиеся навыки программирования и кода для создания управляемого или собственного кода приложения. Кроме того пакет SDK содержит несколько эмуляторов и дополнительные средства для профилирования и тестированию приложения Windows Phone в реальных условиях.
    
    > **Примечание:** Если компьютер соответствует требованиям оборудования и требования к операционной системе, но не соответствует требованиям для эмулятора Windows Phone 8, установки и выполнения 8.0 пакет SDK для Windows Phone. Тем не менее эмулятора Windows Phone 8 не будет работать, и вы не сможете для развертывания или тестирования приложения в эмуляторе Windows Phone 8. Сведения о требованиях к системе для запуска эмулятора Windows Phone видеть [программы установки и системы-требования для эмулятора Windows Phone](http://msdn.microsoft.com/en-us/library/ff626524). 
2. Установите  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818).
    
    Пакет SDK для SharePoint для Windows Phone устанавливает два шаблоны Silverlight для Windows Phone (кроме, установленных с пакет SDK для Windows Phone): шаблон приложение Windows Phone пустой SharePoint и приложения списка SharePoint для Windows Phone. Пакет SDK также устанавливается SharePoint CSOM библиотеки, библиотеки проверки подлинности и шаблоны проектов Windows Phone и он теперь поддерживает проверку подлинности NTLM. Связанные интерфейсы API и шаблоны можно использовать для построения приложений Windows Phone 8 на основе SharePoint.
    
    Кроме того пакет SDK для SharePoint для Windows Phone устанавливает несколько вспомогательные сборки во время выполнения (в  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v8.0\\Libraries` для стандартной установки).
    
  - Microsoft.SharePoint.Client.Phone.dll
    
  
  - Microsoft.SharePoint.Client.Phone.Runtime.dll
    
  
  - Microsoft.SharePoint.Client.Phone.Auth.UI
    
  
  - Microsoft.SharePoint.Phone.Application.dll
    
  

    > **Примечание:** Шаблоны в пакете SDK SharePoint для Windows Phone в настоящее время доступны только для проектов C#. 
      > Дополнительные сведения о шаблонах в пакете SDK SharePoint для Windows Phone можно [шаблоны приложений Overview of Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).
  
    
    

### <a name="configuring-windows-phone-sdk-71"></a>Настройка Windows Phone 7.1 SDK

Чтобы разработать Надстройки SharePoint для использования на Windows Phone 7, необходимо настроить средств разработки на компьютере, на котором работает Windows 7 (32-разрядная или 64-разрядная версия) или Пакет обновления 2 для Windows Vista (32-разрядная или 64-разрядная версия). Windows Phone Software Development Kit (SDK) 7.1 не поддерживается на Windows Server 2008 или на Windows XP.
  
    
    

1. На компьютере с поддерживаемой клиентской операционной системы установите  [пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570).
    
    > **Примечание:** Более ранней версии пакета SDK Windows Phone был с именем средств разработчика Windows Phone. 

    Пакет SDK для Windows Phone устанавливает Microsoft Visual Studio 2010 Express для Windows Phone, эмулятора Windows Phone, Studio игру XNA и Blend выражений Microsoft для Windows Phone. Visual Studio 2010, экспресс-выпуск for Windows Phone  это среду разработки подходит для большинства решений для Windows Phone. Visual Studio 2010 Professional также можно использовать в качестве среды разработки предпочитаемый, но все еще необходимо установить пакет SDK для телефонов Windows, которая устанавливает необходимые надстройки Visual Studio. (Пакет SDK для Windows Phone не поддерживается в настоящее время для использования с Visual Studio 2012.)
    
    Сведения о дополнительных системных требованиях и инструкции по установке пакет SDK для Windows Phone содержатся в разделе  [Установка пакет SDK для Windows Phone](http://msdn.microsoft.com/en-us/library/ff402530). Сведения о требованиях к системе для запуска эмулятора Windows Phone  [программа установки, которая системы-требования для эмулятора телефона Windows](http://msdn.microsoft.com/en-us/library/ff626524)см.
    
  
2. Установите  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476).
    
    Пакет SDK для SharePoint для Windows Phone устанавливает два шаблоны Silverlight для Windows Phone (кроме, установленных с пакет SDK для Windows Phone): шаблон приложение Windows Phone пустой SharePoint и приложения списка SharePoint для Windows Phone.
    
    Кроме того пакет SDK для SharePoint для Windows Phone устанавливает несколько вспомогательные сборки во время выполнения (в  `%ProgramFiles(x86)%\\Microsoft SDKs\\SharePoint\\v15.0\\Phone\\v7.1\\Libraries` для стандартной установки).
    
  - Microsoft.SharePoint.Client.Phone.dll
    
  
  - Microsoft.SharePoint.Client.Phone.Runtime.dll
    
  
  - Microsoft.SharePoint.Client.Phone.Auth.UI
    
  
  - Microsoft.SharePoint.Phone.Application.dll
    
  

    > **Примечание:** Шаблоны в пакете SDK SharePoint для Windows Phone в настоящее время доступны только для проектов C#. 
      > Дополнительные сведения о шаблонах в пакете SDK SharePoint для Windows Phone можно [шаблоны приложений Overview of Windows Phone SharePoint в Visual Studio](overview-of-windows-phone-sharepoint-application-templates-in-visual-studio.md).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Setupmobile_addlresources"> </a>


-  [Построение приложений Windows Phone, обращающихся к SharePoint](build-windows-phone-apps-that-access-sharepoint.md)
    
  
-  [Windows Phone SDK 8.0](http://www.microsoft.com/en-us/download/details.aspx?id=35471)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 8](http://www.microsoft.com/en-us/download/details.aspx?id=36818)
    
  
-  [Пакет SDK для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=27570)
    
  
-  [Пакет SDK Microsoft SharePoint для Windows Phone 7.1](http://www.microsoft.com/en-us/download/details.aspx?id=30476)
    
  

