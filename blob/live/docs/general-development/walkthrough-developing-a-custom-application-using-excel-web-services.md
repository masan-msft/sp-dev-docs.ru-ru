---
title: "Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2f9bf243-281a-4d70-917e-9eaf0b867631
ms.openlocfilehash: 96cbe71ced7143b9888645b3b455c3738f0030a6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="walkthrough-developing-a-custom-application-using-excel-web-services"></a><span data-ttu-id="3cd2b-102">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="3cd2b-102">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>

<span data-ttu-id="3cd2b-103">В этом разделе представлено пошаговое руководство, в котором описывается порядок доступа к веб-службам Веб-службы Excel из приложения, созданного с помощью Microsoft Visual C#.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-103">The walkthrough in this section describes the process for accessing Excel Web Services from an application created with Microsoft Visual C#.</span></span>
  
    
    

<span data-ttu-id="3cd2b-104">В этом пошаговом руководстве рассматривается порядок выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="3cd2b-104">During this walkthrough, you will learn how to:</span></span>
- <span data-ttu-id="3cd2b-105">Создание клиентского приложения с использованием шаблона проекта консольного приложения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-105">Create a client application using the Visual Studio Console Application project template.</span></span>
    
  
- <span data-ttu-id="3cd2b-106">Добавление веб-ссылки для веб-служб Веб-службы Excel.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-106">Add a Web reference for Excel Web Services.</span></span>
    
  
- <span data-ttu-id="3cd2b-p101">Написание кода для доступа к веб-службе. В этом разделе приведены инструкции по открытию рабочей книги, получению идентификатора сеанса, передаче учетных данных по умолчанию, получению сведений о версии веб-службы, определению объекта координат диапазона, получению диапазона, в котором используется объект координат, а также по закрытию рабочей книги и перехвату исключения SOAP.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-p101">Write code to access the Web service. You will learn how to open a workbook, get the session ID, pass in the default credentials, get Web service version information, define the range coordinate object, get the range that uses the range coordinate object, close the workbook, and catch the SOAP exception.</span></span>
    
  
- <span data-ttu-id="3cd2b-109">Тестирование и запуск консольного приложения в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-109">Test and run the console application in debug mode.</span></span>
    
  
<span data-ttu-id="3cd2b-p102">Клиентское консольное приложение  это всего лишь один из возможных способов доступа к веб-службе. Гораздо чаще для этих целей используются серверные приложения, например приложения Microsoft ASP.NET. В этом пошаговом руководстве для большего удобства используется пример консольного приложения, основное внимание в котором уделяется вопросам использования API-интерфейса веб-службы Веб-службы Excel.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-p102">A client console application is just one way to access the Web service. A more common way would be to use server applications, such as Microsoft ASP.NET applications. This walkthrough uses a console application example for simplicity, to focus on the Excel Web Services API aspects.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="3cd2b-113">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="3cd2b-113">Prerequisites</span></span>

<span data-ttu-id="3cd2b-114">Для выполнения этой процедуры требуется установить следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="3cd2b-114">In order to complete this walkthrough, you will need:</span></span> 
  
    
    

- <span data-ttu-id="3cd2b-115">Microsoft SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-115">Microsoft SharePoint Server 2010.</span></span>
    
  
- <span data-ttu-id="3cd2b-116">Visual Studio или аналогичное средство разработки, совместимое с Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-116">Visual Studio or a similar Microsoft .NET Framework-compatible development tool.</span></span>
    
  
- <span data-ttu-id="3cd2b-117">Достаточные разрешения (как минимум разрешения на просмотр) для доступа к веб-службам Веб-службы Excel на компьютере, на котором располагаются SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-117">Sufficient permissions (at the very least, "view" permissions) to be able to access Excel Web Services on the computer where SharePoint Server 2010 is located.</span></span> 
    
    > <span data-ttu-id="3cd2b-118">**Примечание:** Дополнительные сведения о разрешениях книги в следующем разделе, книги» разрешения «.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-118">**Note:** For more information about workbook permissions, see the following section, "Workbook Permissions."</span></span> 
- <span data-ttu-id="3cd2b-119">Пример рабочей книги, установленный на локальном диске или в локальной библиотеке документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-119">A sample workbook installed on a local drive or local SharePoint document library.</span></span> 
    
  
- <span data-ttu-id="3cd2b-p103">Надежное расположение для хранения рабочих книг, доступ к которым будет осуществляться с помощью веб-служб Веб-службы Excel. Если рабочие книги хранятся не в надежном расположении, вызовы веб-служб Веб-службы Excel для открытия таких книг завершаются сбоем. В этом пошаговом руководстве подразумевается, что рабочая книга размещается на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-p103">A trusted location to store the workbooks that you want to access using Excel Web Services. If the workbooks are not stored in a trusted location, the Excel Web Services calls to open the workbook will fail. This walkthrough assumes the workbook is present on the local computer.</span></span> 
    
    > <span data-ttu-id="3cd2b-123">**Примечание:** Сведения о том, как надежного расположения можно [как: надежного расположения](how-to-trust-a-location.md) и [как: доверия Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cd2b-123">**Note:** For information about how to trust a location, see  [How to: Trust a Location](how-to-trust-a-location.md) and [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span></span> 
- <span data-ttu-id="3cd2b-124">Возможность создания книги с помощью Excel.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-124">To create the workbook using Excel.</span></span>
    
  
- <span data-ttu-id="3cd2b-125">Сохранение рабочей книги в формате XLSX или XLSB.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-125">To save the workbook as .xlsx or .xlsb files.</span></span>
    
  
<span data-ttu-id="3cd2b-p104">В рабочей книге, используемой в этом примере, представлен лист "Sheet1", в котором содержатся 11 столбцов и 19 строк. В каждой ячейке в диапазоне от A1 до K19 содержится числовое значение, например, 4245,955, 6960,673 и т. д.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-p104">The workbook used in this example has a worksheet named "Sheet1". The worksheet has 11 columns and 19 rows. Each cell from A1 to K19 contains a numeric value—for example, 4245.955, 6960.673, and so on.</span></span>
  
    
    

## <a name="workbook-permissions"></a><span data-ttu-id="3cd2b-129">Разрешения рабочих книг</span><span class="sxs-lookup"><span data-stu-id="3cd2b-129">Workbook Permissions</span></span>


- <span data-ttu-id="3cd2b-130">Для получения рабочей книги целиком (например, с помощью метода **GetWorkbook**) вызывающий объект должен обладать разрешениями на ее открытие.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-130">To get the entire workbook (for example, by calling the **GetWorkbook** method), the caller needs "open" permission fr the workbook.</span></span>
    
  
- <span data-ttu-id="3cd2b-131">Для вызова метода **GetApiVersion** не требуется никаких разрешений.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-131">To call the **GetApiVersion** method, no permission is necessary.</span></span>
    
  
- <span data-ttu-id="3cd2b-132">Для остальных методов веб-служб Веб-службы Excel вызывающему объекту требуются разрешения на просмотр (в Microsoft SharePoint Foundation) или чтение (на общем файловом ресурсе) рабочей книги.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-132">For the rest of the Excel Web Services methods, the caller needs "view" permission (in Microsoft SharePoint Foundation) or "read" permission (on a file share) for the workbook.</span></span>
    
    > <span data-ttu-id="3cd2b-133">**Примечание:** Дополнительные сведения о настройке разрешений обратитесь к документации SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="3cd2b-133">**Note:** For more information about setting permissions, see the SharePoint Foundation documentation.</span></span> 

## <a name="see-also"></a><span data-ttu-id="3cd2b-134">См. также</span><span class="sxs-lookup"><span data-stu-id="3cd2b-134">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="3cd2b-135">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="3cd2b-135">Concepts</span></span>


  
    
    
 [<span data-ttu-id="3cd2b-136">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="3cd2b-136">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="3cd2b-137">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="3cd2b-137">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="3cd2b-138">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="3cd2b-138">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
  
    
    
 [<span data-ttu-id="3cd2b-139">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="3cd2b-139">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
#### <a name="other-resources"></a><span data-ttu-id="3cd2b-140">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="3cd2b-140">Other resources</span></span>


  
    
    
 [<span data-ttu-id="3cd2b-141">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="3cd2b-141">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="3cd2b-142">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="3cd2b-142">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="3cd2b-143">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="3cd2b-143">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="3cd2b-144">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="3cd2b-144">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
