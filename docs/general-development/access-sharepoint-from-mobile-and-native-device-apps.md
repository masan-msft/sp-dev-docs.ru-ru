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
# <a name="access-sharepoint-from-mobile-and-native-device-apps"></a><span data-ttu-id="e4013-102">SharePoint доступа с мобильных устройств и собственные устройства приложений</span><span class="sxs-lookup"><span data-stu-id="e4013-102">Access SharePoint from mobile and native device apps</span></span>
<span data-ttu-id="e4013-p101">Узнайте, как получить доступ к SharePoint из мобильных приложений и других приложений собственные устройства и из внешних веб-приложений. Надстройки SharePoint, решения ферм и "без кода" изолированные решения являются все выполнять в SharePoint, но приложения на другие платформы можно также получить доступ к клиентские интерфейсы API SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e4013-p101">Learn how to access SharePoint from mobile apps and other native device apps, and from external web applications. SharePoint Add-ins, farm solutions, and "no code" sandboxed solutions are all run from within SharePoint, but apps on other platforms can also access SharePoint client APIs.</span></span>
  
    
    


> [!IMPORTANT]
> <span data-ttu-id="e4013-p102">[!Важно!] To test and debug on any platform, you need a **developer account on Office 365**. More info: [Настройка среды для разработки надстроек SharePoint в Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) or [Создание сайта разработчика с использованием актуальной подписки на Office 365](http://msdn.microsoft.com/library/2ec857d5-dc6f-4cf6-ba45-adc845ef2a25%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4013-p102">To test and debug on any platform, you need a **developer account on Office 365**. More info: [Set up a development environment for SharePoint Add-ins on Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54%28Office.15%29.aspx) or [Create a developer site on an existing Office 365 subscription](http://msdn.microsoft.com/library/2ec857d5-dc6f-4cf6-ba45-adc845ef2a25%28Office.15%29.aspx).</span></span> 
  
    
    


## <a name="non-microsoft-mobile-and-native-device-apps"></a><span data-ttu-id="e4013-107">Приложения сторонних разработчиков мобильных устройств и собственные устройства</span><span class="sxs-lookup"><span data-stu-id="e4013-107">Non-Microsoft mobile and native device apps</span></span>

<span data-ttu-id="e4013-108">Приложений других производителей устройств, включая мобильные приложения, **использования API REST/OData SharePoint для операций с данными SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="e4013-108">Non-Microsoft device apps, including mobile apps, **use SharePoint REST/OData APIs for CRUD operations on SharePoint data**.</span></span>
  
    
    

- <span data-ttu-id="e4013-109">[Узнайте о службе SharePoint REST](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) в разделе Основы.</span><span class="sxs-lookup"><span data-stu-id="e4013-109">See  [Get to know the SharePoint REST service](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) for the basics.</span></span>
    
  
- <span data-ttu-id="e4013-110">[Справочник по интерфейсу API службы REST для SharePoint](http://msdn.microsoft.com/library/3514e753-19f9-4b41-a1ae-f35c5ffc17d2%28Office.15%29.aspx) в разделе полный справочник.</span><span class="sxs-lookup"><span data-stu-id="e4013-110">See  [REST API reference for SharePoint](http://msdn.microsoft.com/library/3514e753-19f9-4b41-a1ae-f35c5ffc17d2%28Office.15%29.aspx) for a complete reference.</span></span>
    
  
<span data-ttu-id="e4013-111">Дополнительные сведения о создании мобильного приложения для любой платформы можно [Создание мобильных приложений для других платформ с помощью SharePoint](build-mobile-apps-for-other-platforms-using-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e4013-111">For more information about how to create mobile apps for any platform, see  [Build mobile apps for other platforms using SharePoint](build-mobile-apps-for-other-platforms-using-sharepoint.md).</span></span>
  
    
    

## <a name="windows-phone-apps-that-access-sharepoint"></a><span data-ttu-id="e4013-112">Приложения для Windows Phone, обращающимися к SharePoint</span><span class="sxs-lookup"><span data-stu-id="e4013-112">Windows Phone apps that access SharePoint</span></span>
<span data-ttu-id="e4013-113"><a name="WinPhone"> </a></span><span class="sxs-lookup"><span data-stu-id="e4013-113"><a name="WinPhone"> </a></span></span>

<span data-ttu-id="e4013-114">Приложения для Windows Phone можно использовать один из следующих:</span><span class="sxs-lookup"><span data-stu-id="e4013-114">Windows Phone apps can use one of the following:</span></span>
  
    
    

- <span data-ttu-id="e4013-115">.NET SharePoint клиентской объектной модели (CSOM) версию специально для устройств Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="e4013-115">The .NET SharePoint client-side object model (CSOM) version specifically for Windows Phone devices.</span></span>
    
  
- <span data-ttu-id="e4013-116">API-интерфейсы SharePoint REST/OData.</span><span class="sxs-lookup"><span data-stu-id="e4013-116">The SharePoint REST/OData APIs.</span></span>
    
  
 <span data-ttu-id="e4013-117">Эти мобильных приложений можно воспользоваться преимуществами поддержки в SharePoint для службы Push-уведомления Майкрософт и новый тип поля географического расположения.</span><span class="sxs-lookup"><span data-stu-id="e4013-117">These mobile apps can take advantage of the support in SharePoint for the Microsoft Push Notification service and a new geolocation field type.</span></span>
  
    
    
<span data-ttu-id="e4013-118">Дополнительные сведения о создании приложений Windows Phone, обращающимися к SharePoint в разделе [Windows Phone построения приложений, доступ к SharePoint](build-windows-phone-apps-that-access-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e4013-118">For more about creating Windows Phone apps that access SharePoint, see  [Build Windows Phone apps that access SharePoint](build-windows-phone-apps-that-access-sharepoint.md).</span></span>
  
    
    

## <a name="web-applications-that-dont-start-from-sharepoint"></a><span data-ttu-id="e4013-119">Веб-приложений, которые не начинаются с SharePoint</span><span class="sxs-lookup"><span data-stu-id="e4013-119">Web applications that don't start from SharePoint</span></span>
<span data-ttu-id="e4013-120"><a name="WinPhone"> </a></span><span class="sxs-lookup"><span data-stu-id="e4013-120"><a name="WinPhone"> </a></span></span>

<span data-ttu-id="e4013-121">Веб-приложений, которые не начинаются с SharePoint не строго "Надстройки SharePoint ", несмотря на то, что в некоторых случаях вы учитывается в качестве Надстройки SharePoint в MSDN и другие документы. Эти приложения включают среди других пользователей, запустите из службы запуска приложения Office 365 и Надстройки Office, а также любого веб-приложения, на которых выполняется непосредственно из браузера.</span><span class="sxs-lookup"><span data-stu-id="e4013-121">Web applications that don't start from SharePoint are not strictly "SharePoint Add-ins," although they're sometimes counted as SharePoint Add-ins in MSDN and other docs. These apps include, among others, ones that run from the Office 365 app launcher and Office Add-ins, as well as any web applications that are run directly from a browser.</span></span>
  
    
    
<span data-ttu-id="e4013-p103">Можно создавать эти приложения на платформу ASP.NET или стек не Майкрософт. При создании веб-приложения в стеке не корпорации Майкрософт, это делается операций CRUD с помощью интерфейсов API REST/OData, так же, как приложение от стороннего устройства. При построении на ASP.NET его **можно использовать SharePoint CSOM или API REST/OData**.</span><span class="sxs-lookup"><span data-stu-id="e4013-p103">You can build these apps on the ASP.NET platform or a non-Microsoft stack. If you build your web application on a non-Microsoft stack, it does CRUD operations with the REST/OData APIs, just as a non-Microsoft device app. If you build it on ASP.NET it **can use the SharePoint CSOM or the REST/OData APIs**.</span></span>
  
    
    
<span data-ttu-id="e4013-p104">These apps **gain authorized access to SharePoint data by using access tokens** that are issued by the Azure Control Service (ACS) in compliance with the OAuth Authentication Code flow. For more, see [Поток кода аутентификации OAuth для надстроек в SharePoint](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4013-p104">These apps **gain authorized access to SharePoint data by using access tokens** that are issued by the Azure Control Service (ACS) in compliance with the OAuth Authentication Code flow. For more, see [Authorization Code OAuth flow for SharePoint Add-ins](http://msdn.microsoft.com/library/e89e91c7-ea39-49b9-af5a-7f047a7e2ab7%28Office.15%29.aspx).</span></span>
  
    
    

