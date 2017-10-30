---
title: "Новые возможности в Access"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 625bc1d0-55db-4420-a02e-aee04028b215
ms.openlocfilehash: df9d6abbc550bf070968d479e5639c5f7fba08df
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-in-access"></a><span data-ttu-id="3e509-102">Новые возможности в Access</span><span class="sxs-lookup"><span data-stu-id="3e509-102">What's new in Access</span></span>
<span data-ttu-id="3e509-103">Сведения о возможностях Access 2013 делает его упрощает создание, развертывание и управление совместной работы веб-приложений локально или в облаке.</span><span class="sxs-lookup"><span data-stu-id="3e509-103">Learn about the features in Access 2013 makes it easy to create, deploy, and manage collaborative web-based applications on premise or in the cloud.</span></span>
## <a name="introduction"></a><span data-ttu-id="3e509-104">Введение</span><span class="sxs-lookup"><span data-stu-id="3e509-104">Introduction</span></span>
<span data-ttu-id="3e509-105"><a name="SP15_access15overview_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="3e509-105"><a name="SP15_access15overview_Introduction"> </a></span></span>

<span data-ttu-id="3e509-106">Функции Access 2013, то есть модель новое приложение предназначено для одного purpose―to упростить веб-разработке так же, как более ранних версиях Access по разработке для Windows.</span><span class="sxs-lookup"><span data-stu-id="3e509-106">Access 2013 features a new application model that is designed for one purpose―to simplify web development much like earlier versions of Access with Windows development.</span></span> <span data-ttu-id="3e509-107">Access 2013 позволяет быстро создавать приложения, которое может использоваться для выполнения своих организаций экспертами по данному вопросу.</span><span class="sxs-lookup"><span data-stu-id="3e509-107">Access 2013 enables subject matter experts to quickly create an application that can be used to run their business.</span></span> <span data-ttu-id="3e509-108">С помощью Microsoft SharePoint для размещения переднего плана приложения и Microsoft SQL Server 2012, как его технологии хранения данных, Access 2013 значительно улучшает эффективность управляемости и масштабируемости доступа к приложениям.</span><span class="sxs-lookup"><span data-stu-id="3e509-108">By using Microsoft SharePoint to host the front end of the app and Microsoft SQL Server 2012 as its data storage technology, Access 2013 significantly improves the manageability and scalability of Access applications.</span></span> <span data-ttu-id="3e509-109">Совместимость с Office 365 и SQL Azure значительно разверните reach получать доступ к приложениям.</span><span class="sxs-lookup"><span data-stu-id="3e509-109">Compatibility with Office 365 and SQL Azure significantly expand the reach of Access applications.</span></span>
  
    
    

## <a name="architecture"></a><span data-ttu-id="3e509-110">Архитектура</span><span class="sxs-lookup"><span data-stu-id="3e509-110">Architecture</span></span>
<span data-ttu-id="3e509-111"><a name="SP15_access15overview_Architecture"> </a></span><span class="sxs-lookup"><span data-stu-id="3e509-111"><a name="SP15_access15overview_Architecture"> </a></span></span>

<span data-ttu-id="3e509-112">В локальной среде Access 2013 приложений, размещенных SharePoint во время хранения данных в SQL Server 2012.</span><span class="sxs-lookup"><span data-stu-id="3e509-112">In an on-premise environment, Access 2013 apps are hosted by SharePoint while the data is stored in SQL Server 2012.</span></span> <span data-ttu-id="3e509-113">SharePoint предоставляет проверки подлинности, авторизация и безопасность для приложений Access 2013.</span><span class="sxs-lookup"><span data-stu-id="3e509-113">SharePoint provides authentication, authorization, and security for Access 2013 apps.</span></span> <span data-ttu-id="3e509-114">Серверные таблицы, представления, макросов и запросов хранятся в базе данных SQL Server 2012.</span><span class="sxs-lookup"><span data-stu-id="3e509-114">The back-end tables, views, macros, and queries are stored in an SQL Server 2012 database.</span></span>
  
    
    
<span data-ttu-id="3e509-115">Access 2013, через службы Office 365 и SQL Azure предоставляет метод для развертывания приложения Access в облако.</span><span class="sxs-lookup"><span data-stu-id="3e509-115">Access 2013, through the Office 365 and SQL Azure services, provides a method to deploy an Access app to the cloud.</span></span>
  
    
    
<span data-ttu-id="3e509-116">На рисунке 1 содержит сведения об архитектуре Access 2013.</span><span class="sxs-lookup"><span data-stu-id="3e509-116">Figure 1 provides an overview of Access 2013 architecture.</span></span>
  
    
    

<span data-ttu-id="3e509-117">**На рисунке 1. Архитектура Access 2013**</span><span class="sxs-lookup"><span data-stu-id="3e509-117">**Figure 1. Access 2013 architecture**</span></span>

  
    
    

  
    
    
![Архитектура Access 2013](../images/odc_Office15_Access15OverviewDK2_Figure07.jpg)
  
    
    
<span data-ttu-id="3e509-119">При создании нового приложения Access, службы Access в SharePoint создает новую базу данных приложения, в которой хранятся данные, представления, запросов и макросов, которые содержатся в приложении.</span><span class="sxs-lookup"><span data-stu-id="3e509-119">When a new Access application is created, Access Services in SharePoint creates a new Application database that stores the data, view, queries and macros contained in the app.</span></span> <span data-ttu-id="3e509-120">База данных Access Services 2013 системы можно настроить для создания новых приложений баз данных на отдельном сервере SQL Server 2012.</span><span class="sxs-lookup"><span data-stu-id="3e509-120">The Access Services 2013 System database can be configured to create new Application databases on a separate SQL Server 2012 server.</span></span>
  
    
    
<span data-ttu-id="3e509-p104">Использование SQL Server 2012 для хранения данных обеспечивает управляемости и масштабируемости, ранее неизвестные Access приложениям. Прошли дни, когда приложение Access придется переработана и воссозданы в среде с более эффективны.</span><span class="sxs-lookup"><span data-stu-id="3e509-p104">Using SQL Server 2012 to store data provides manageability and scalability previously unknown to Access applications. Gone are the days when an Access application would have to be redesigned and reimplemented in a more powerful environment.</span></span>
  
    
    
<span data-ttu-id="3e509-p105">Приложение Access 2013 online тогда, когда он будет создан. Можно совместно использовать приложения с другими людьми, развертывание в частном каталоге организации или развертывание в Магазин Office.</span><span class="sxs-lookup"><span data-stu-id="3e509-p105">An Access 2013 app is online the moment it's created. You can decide to share the app with other people, deploy to the private corporate catalog, or deploy to the Office Store.</span></span>
  
    
    

## <a name="developing-access-apps"></a><span data-ttu-id="3e509-125">Разработка приложений Access</span><span class="sxs-lookup"><span data-stu-id="3e509-125">Developing Access apps</span></span>
<span data-ttu-id="3e509-126"><a name="SP15_access15overview_DevelopingAccessapps"> </a></span><span class="sxs-lookup"><span data-stu-id="3e509-126"><a name="SP15_access15overview_DevelopingAccessapps"> </a></span></span>

<span data-ttu-id="3e509-127">В отличие от служб SharePointapplication Access Services 2013 не предоставляют доступ к API, который можно использовать при разработке приложения Access в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3e509-127">Unlike many of the SharePointapplication services, Access Services 2013 doesn't expose an API that you can use to develop Access apps in Visual Studio.</span></span> <span data-ttu-id="3e509-128">Access 2013 — это среда, которая используется для разработки приложений Access 2013.</span><span class="sxs-lookup"><span data-stu-id="3e509-128">Access 2013 is the environment that you use to develop Access 2013 apps.</span></span>
  
    
    
<span data-ttu-id="3e509-129">Дополнительные сведения о разработке приложений Access 2013 можно  [How to: Create and customize a web app in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="3e509-129">For more information about how to develop Access 2013 apps, see  [How to: Create and customize a web app in Access](http://msdn.microsoft.com/library/628745f4-82e9-4838-9726-6f3e506a654f%28Office.15%29.aspx)</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="3e509-130">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3e509-130">Additional Resources</span></span>
<span data-ttu-id="3e509-131"><a name="SP15_access15overview_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="3e509-131"><a name="SP15_access15overview_addres"> </a></span></span>


-  [<span data-ttu-id="3e509-132">New in Access for developers</span><span class="sxs-lookup"><span data-stu-id="3e509-132">New in Access for developers</span></span>](http://msdn.microsoft.com/library/df778f51-d65e-4c30-b618-65003ceb39b3%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="3e509-133">Access custom web app reference</span><span class="sxs-lookup"><span data-stu-id="3e509-133">Access custom web app reference</span></span>](http://msdn.microsoft.com/library/8d696fa4-a6f2-4fb1-8662-a313bf0b5989%28Office.15%29.aspx)
    
  

