---
title: "SharePoint доступа с мобильных устройств и собственные устройства приложений"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 42014171-5ee5-421d-9cde-413efc3aecef
ms.openlocfilehash: 5376b4f3f0b629669d6965d7d37c63e12eded769
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="access-sharepoint-from-mobile-and-native-device-apps"></a>SharePoint доступа с мобильных устройств и собственные устройства приложений
Узнайте, как получить доступ к SharePoint из мобильных приложений и других приложений собственные устройства и из внешних веб-приложений. Надстройки SharePoint, решения ферм и "без кода" изолированные решения являются все выполнять в SharePoint, но приложения на другие платформы можно также получить доступ к клиентские интерфейсы API SharePoint.
  
    
    


> [!IMPORTANT]
> [!Важно!] To test and debug on any platform, you need a **developer account on Office 365**. More info: [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) or [Создание сайта разработчика с использованием актуальной подписки на Office 365](http://msdn.microsoft.com/library/2ec857d5-dc6f-4cf6-ba45-adc845ef2a25%28Office.15%29.aspx). 
  
    
    


## <a name="non-microsoft-mobile-and-native-device-apps"></a>Приложения сторонних разработчиков мобильных устройств и собственные устройства

Приложений других производителей устройств, включая мобильные приложения, **использования API REST/OData SharePoint для операций с данными SharePoint**.
  
    
    

- [Узнайте о службе SharePoint REST](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) в разделе Основы.
    
  
- [Справочник по интерфейсу API службы REST для SharePoint](http://msdn.microsoft.com/library/3514e753-19f9-4b41-a1ae-f35c5ffc17d2%28Office.15%29.aspx) в разделе полный справочник.
    
  
Дополнительные сведения о создании мобильного приложения для любой платформы можно [Создание мобильных приложений для других платформ с помощью SharePoint](build-mobile-apps-for-other-platforms-using-sharepoint.md).
  
    
    

## <a name="windows-phone-apps-that-access-sharepoint"></a>Приложения для Windows Phone, обращающимися к SharePoint
<a name="WinPhone"> </a>

Приложения для Windows Phone можно использовать один из следующих:
  
    
    

- .NET SharePoint клиентской объектной модели (CSOM) версию специально для устройств Windows Phone.
    
  
- API-интерфейсы SharePoint REST/OData.
    
  
 Эти мобильных приложений можно воспользоваться преимуществами поддержки в SharePoint для службы Push-уведомления Майкрософт и новый тип поля географического расположения.
  
    
    
Дополнительные сведения о создании приложений Windows Phone, обращающимися к SharePoint в разделе [Windows Phone построения приложений, доступ к SharePoint](build-windows-phone-apps-that-access-sharepoint.md).
  
    
    

## <a name="web-applications-that-dont-start-from-sharepoint"></a>Веб-приложений, которые не начинаются с SharePoint
<a name="WinPhone"> </a>

Веб-приложений, которые не начинаются с SharePoint не строго "Надстройки SharePoint ", несмотря на то, что в некоторых случаях вы учитывается в качестве Надстройки SharePoint в MSDN и другие документы. Эти приложения включают среди других пользователей, запустите из службы запуска приложения Office 365 и Надстройки Office, а также любого веб-приложения, на которых выполняется непосредственно из браузера.
  
    
    
Можно создавать эти приложения на платформу ASP.NET или стек не Майкрософт. При создании веб-приложения в стеке не корпорации Майкрософт, это делается операций CRUD с помощью интерфейсов API REST/OData, так же, как приложение от стороннего устройства. При построении на ASP.NET его **можно использовать SharePoint CSOM или API REST/OData**.
  
    
    
These apps **gain authorized access to SharePoint data by using access tokens** that are issued by the Azure Control Service (ACS) in compliance with the OAuth Authentication Code flow. For more, see [Поток кода аутентификации OAuth для надстроек в SharePoint](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).
  
    
    

