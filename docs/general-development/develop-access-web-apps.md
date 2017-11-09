---
title: "Разработка веб-приложений Access"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 41131b27-d750-4d11-b3c7-c17ad4d666e2
ms.openlocfilehash: be398709c93b4d8f86bffe6e8566349527f59126
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="develop-access-web-apps"></a><span data-ttu-id="063f5-102">Разработка веб-приложений Access</span><span class="sxs-lookup"><span data-stu-id="063f5-102">Develop Access web apps</span></span>
<span data-ttu-id="063f5-103">Узнайте, как Microsoft Access 2013 упрощает создание и развертывание веб-приложений для совместной работы в локальной среде или в облаке, а также управление ними.</span><span class="sxs-lookup"><span data-stu-id="063f5-103">Learn how Microsoft Access 2013 makes it easy to create, deploy, and manage collaborative web-based applications on premise or in the cloud.</span></span>
## <a name="introduction"></a><span data-ttu-id="063f5-104">Введение</span><span class="sxs-lookup"><span data-stu-id="063f5-104">Introduction</span></span>
<span data-ttu-id="063f5-105"><a name="dk2_DevelopingAccess15WebApps_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="063f5-105"></span></span>

<span data-ttu-id="063f5-p101">Приложение Microsoft Access 2013 позволяет упростить веб-разработку так же, как это делалось ранее в случае разработки для Windows. С помощью Access 2013 специалисты могут быстро создавать приложения для управления компанией.</span><span class="sxs-lookup"><span data-stu-id="063f5-p101">Microsoft Access 2013 is designed to simplify web development in the same manner that it did in previous eras of Windows development. Access 2013 is designed to enable subject matter experts to quickly create an application that can be used to run their business.</span></span>
  
    
    

  
    
    

## <a name="whats-new-in-access-2013"></a><span data-ttu-id="063f5-108">Что нового в Access 2013</span><span class="sxs-lookup"><span data-stu-id="063f5-108">What's new in Access 2013</span></span>
<span data-ttu-id="063f5-109"><a name="dk2_DevelopingAccess15WebApps_whatsNewInAccess15"> </a></span><span class="sxs-lookup"><span data-stu-id="063f5-109"></span></span>

<span data-ttu-id="063f5-p102">Access 2013 представляет новую модель приложения, с помощью которой можно создавать веб-приложения, ориентированные на данные. Пользователям с небольшим опытом программирования или вовсе без него часто нужно быстро создать приложение, отвечающее потребностям компании, и поделиться ним с коллегами, друзьями и членами семьи. В Access 2013 доступен интерактивный метод, позволяющий легко начать создавать таблицы и различные формы с учетом указанных условий.</span><span class="sxs-lookup"><span data-stu-id="063f5-p102">Access 2013 features a new application model that is designed to allow users to create data-centric web applications. Users with little or no programming experience often need to quickly build an application that addresses their business needs and share it with their colleagues, friends, or family. Access 2013 offers users an interactive method that can be used to get up and running quickly with by creating tables and forms that are based on the selected criteria.</span></span>
  
    
    
<span data-ttu-id="063f5-p103">Приложение Access 2013 использует Microsoft SharePoint для размещения внешнего интерфейса приложения, тогда как данные хранятся на сервере SQL Server. Access 2013 с помощью служб Office 365 и SQL Azure обеспечивает метод развертывания приложения для Access в Интернете. Предоставить доступ к приложению для Access 2013 так же просто, как отправить его URL-адрес заинтересованным пользователям.</span><span class="sxs-lookup"><span data-stu-id="063f5-p103">Access 2013 uses Microsoft SharePoint to host the front end of your application while it is using SQL Server for data storage. Access 2013, through the Office 365 and SQL Azure services, provides a method to deploy an Access application to the Internet. Sharing an Access 2013 app is as easy as sending the URL of the app to the intended users.</span></span>
  
    
    
<span data-ttu-id="063f5-116">Дополнительные сведения о новых возможностях приложений для Access 2013 см. в статье  [Новые возможности в Access](what-s-new-in-access.md)</span><span class="sxs-lookup"><span data-stu-id="063f5-116">For more information about what's new in Access 2013 apps, see  [What's new in Access](what-s-new-in-access.md)</span></span>
  
    
    

## <a name="creating-an-access-2013-application"></a><span data-ttu-id="063f5-117">Создание приложения для Access 2013</span><span class="sxs-lookup"><span data-stu-id="063f5-117">Creating an Access 2013 application</span></span>
<span data-ttu-id="063f5-118"><a name="dk2_DevelopingAccess15WebApps_CreatingAnAccess15App"> </a></span><span class="sxs-lookup"><span data-stu-id="063f5-118"></span></span>

<span data-ttu-id="063f5-119">В отличие от большинства служб приложений SharePoint, в службах Access 2013 не предоставлен API, с помощью которого можно разрабатывать приложения для Access в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="063f5-119">Unlike many of the SharePoint Server 2013application services, Access Services 2013 doesn't expose an API that you can use to develop Access apps in Visual Studio. Access 2013 is the environment that you use to develop Access 2013 apps.</span></span> <span data-ttu-id="063f5-120">Access 2013 — это среда, с помощью которой можно разрабатывать приложения для Access 2013.</span><span class="sxs-lookup"><span data-stu-id="063f5-120">Access 2013 is the environment that you use to develop Access 2013 apps.</span></span>
  
    
    
<span data-ttu-id="063f5-121">Дополнительные сведения о разработке приложений для Access 2013 см. в статье [Инструкции: создание и настройка веб-приложений в Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="063f5-121">For more information about how to develop Access 2013 apps, see  [How to: Create and customize a web app in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="063f5-122">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="063f5-122">Additional resources</span></span>
<span data-ttu-id="063f5-123"><a name="dk2_DevelopingAccess15WebApps_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="063f5-123"></span></span>


-  [<span data-ttu-id="063f5-124">Новые возможности в Access</span><span class="sxs-lookup"><span data-stu-id="063f5-124">What's new in Access</span></span>](what-s-new-in-access.md)
    
  
-  [<span data-ttu-id="063f5-125">How to: Create and customize a web app in Access</span><span class="sxs-lookup"><span data-stu-id="063f5-125">How to: Create and customize a web app in Access</span></span>](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)
    
  

