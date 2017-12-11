---
title: "Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2f9bf243-281a-4d70-917e-9eaf0b867631
ms.openlocfilehash: 57f6eb6d15510b1147b82fdce53436dded5fa47a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="walkthrough-developing-a-custom-application-using-excel-web-services"></a><span data-ttu-id="40547-102">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="40547-102">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>

<span data-ttu-id="40547-103">В этом разделе представлено пошаговое руководство, в котором описывается порядок доступа к веб-службам Веб-службы Excel из приложения, созданного с помощью Microsoft Visual C#.</span><span class="sxs-lookup"><span data-stu-id="40547-103">The walkthrough in this section describes the process for accessing Excel Web Services from an application created with Microsoft Visual C#.</span></span>
  
    
    

<span data-ttu-id="40547-104">В этом пошаговом руководстве рассматривается порядок выполнения следующих действий:</span><span class="sxs-lookup"><span data-stu-id="40547-104">During this walkthrough, you will learn how to:</span></span>
- <span data-ttu-id="40547-105">Создание клиентского приложения с использованием шаблона проекта консольного приложения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40547-105">Create a client application using the Visual Studio Console Application project template.</span></span>
    
  
- <span data-ttu-id="40547-106">Добавление веб-ссылки для веб-служб Веб-службы Excel.</span><span class="sxs-lookup"><span data-stu-id="40547-106">Add a Web reference for Excel Web Services.</span></span>
    
  
- <span data-ttu-id="40547-p101">Написание кода для доступа к веб-службе. В этом разделе приведены инструкции по открытию рабочей книги, получению идентификатора сеанса, передаче учетных данных по умолчанию, получению сведений о версии веб-службы, определению объекта координат диапазона, получению диапазона, в котором используется объект координат, а также по закрытию рабочей книги и перехвату исключения SOAP.</span><span class="sxs-lookup"><span data-stu-id="40547-p101">Write code to access the Web service. You will learn how to open a workbook, get the session ID, pass in the default credentials, get Web service version information, define the range coordinate object, get the range that uses the range coordinate object, close the workbook, and catch the SOAP exception.</span></span>
    
  
- <span data-ttu-id="40547-109">Тестирование и запуск консольного приложения в режиме отладки.</span><span class="sxs-lookup"><span data-stu-id="40547-109">Test and run the console application in debug mode.</span></span>
    
  
<span data-ttu-id="40547-p102">Клиентское консольное приложение  это всего лишь один из возможных способов доступа к веб-службе. Гораздо чаще для этих целей используются серверные приложения, например приложения Microsoft ASP.NET. В этом пошаговом руководстве для большего удобства используется пример консольного приложения, основное внимание в котором уделяется вопросам использования API-интерфейса веб-службы Веб-службы Excel.</span><span class="sxs-lookup"><span data-stu-id="40547-p102">A client console application is just one way to access the Web service. A more common way would be to use server applications, such as Microsoft ASP.NET applications. This walkthrough uses a console application example for simplicity, to focus on the Excel Web Services API aspects.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="40547-113">Необходимые требования</span><span class="sxs-lookup"><span data-stu-id="40547-113">Prerequisites</span></span>

<span data-ttu-id="40547-114">Для выполнения этой процедуры требуется установить следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="40547-114">In order to complete this walkthrough, you will need:</span></span> 
  
    
    

- <span data-ttu-id="40547-115">Microsoft SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="40547-115">Microsoft SharePoint Server 2010.</span></span>
    
  
- <span data-ttu-id="40547-116">Visual Studio или аналогичное средство разработки, совместимое с Microsoft .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="40547-116">Visual Studio or a similar Microsoft .NET Framework-compatible development tool.</span></span>
    
  
- <span data-ttu-id="40547-117">Достаточные разрешения (как минимум разрешения на просмотр) для доступа к веб-службам Веб-службы Excel на компьютере, на котором располагаются SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="40547-117">Sufficient permissions (at the very least, "view" permissions) to be able to access Excel Web Services on the computer where SharePoint Server 2010 is located.</span></span> 
    
    > [!NOTE] 
    > <span data-ttu-id="40547-118">[!Примечание] Дополнительные сведения о разрешениях рабочих книг см. в следующем разделе "Разрешения рабочих книг".</span><span class="sxs-lookup"><span data-stu-id="40547-118">For more information about workbook permissions, see the following section, "Workbook Permissions."</span></span> 

- <span data-ttu-id="40547-119">Пример рабочей книги, установленный на локальном диске или в локальной библиотеке документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="40547-119">A sample workbook installed on a local drive or local SharePoint document library.</span></span> 
    
  
- <span data-ttu-id="40547-p103">Надежное расположение для хранения рабочих книг, доступ к которым будет осуществляться с помощью веб-служб Веб-службы Excel. Если рабочие книги хранятся не в надежном расположении, вызовы веб-служб Веб-службы Excel для открытия таких книг завершаются сбоем. В этом пошаговом руководстве подразумевается, что рабочая книга размещается на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="40547-p103">A trusted location to store the workbooks that you want to access using Excel Web Services. If the workbooks are not stored in a trusted location, the Excel Web Services calls to open the workbook will fail. This walkthrough assumes the workbook is present on the local computer.</span></span> 
    
    > [!NOTE] 
    > <span data-ttu-id="40547-123">[!Примечание] Присвоение доверия расположению рассматривается в статьях  [How to: Trust a Location](how-to-trust-a-location.md) и [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="40547-123">For information about how to trust a location, see  [How to: Trust a Location](how-to-trust-a-location.md) and [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx).</span></span> 

- <span data-ttu-id="40547-124">Возможность создания книги с помощью Excel.</span><span class="sxs-lookup"><span data-stu-id="40547-124">To create the workbook using Excel.</span></span>
    
  
- <span data-ttu-id="40547-125">Сохранение рабочей книги в формате XLSX или XLSB.</span><span class="sxs-lookup"><span data-stu-id="40547-125">To save the workbook as .xlsx or .xlsb files.</span></span>
    
  
<span data-ttu-id="40547-p104">В рабочей книге, используемой в этом примере, представлен лист "Sheet1", в котором содержатся 11 столбцов и 19 строк. В каждой ячейке в диапазоне от A1 до K19 содержится числовое значение, например, 4245,955, 6960,673 и т. д.</span><span class="sxs-lookup"><span data-stu-id="40547-p104">The workbook used in this example has a worksheet named "Sheet1". The worksheet has 11 columns and 19 rows. Each cell from A1 to K19 contains a numeric value—for example, 4245.955, 6960.673, and so on.</span></span>
  
    
    

## <a name="workbook-permissions"></a><span data-ttu-id="40547-129">Разрешения рабочих книг</span><span class="sxs-lookup"><span data-stu-id="40547-129">Workbook Permissions</span></span>


- <span data-ttu-id="40547-130">Для получения рабочей книги целиком (например, с помощью метода **GetWorkbook**) вызывающий объект должен обладать разрешениями на ее открытие.</span><span class="sxs-lookup"><span data-stu-id="40547-130">To get the entire workbook (for example, by calling the **GetWorkbook** method), the caller needs "open" permission fr the workbook.</span></span>
    
  
- <span data-ttu-id="40547-131">Для вызова метода **GetApiVersion** не требуется никаких разрешений.</span><span class="sxs-lookup"><span data-stu-id="40547-131">To call the **GetApiVersion** method, no permission is necessary.</span></span>
    
  
- <span data-ttu-id="40547-132">Для остальных методов веб-служб Веб-службы Excel вызывающему объекту требуются разрешения на просмотр (в Microsoft SharePoint Foundation) или чтение (на общем файловом ресурсе) рабочей книги.</span><span class="sxs-lookup"><span data-stu-id="40547-132">For the rest of the Excel Web Services methods, the caller needs "view" permission (in Microsoft SharePoint Foundation) or "read" permission (on a file share) for the workbook.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="40547-133">[!Примечание] Дополнительные сведения об установке разрешений см. в документации SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="40547-133">For more information about setting permissions, see the SharePoint Foundation documentation.</span></span> 

## <a name="see-also"></a><span data-ttu-id="40547-134">См. также</span><span class="sxs-lookup"><span data-stu-id="40547-134">See also</span></span>

- [<span data-ttu-id="40547-135">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="40547-135">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
- [<span data-ttu-id="40547-136">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="40547-136">Excel Services Alerts</span></span>](excel-services-alerts.md)
- [<span data-ttu-id="40547-137">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="40547-137">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
- [<span data-ttu-id="40547-138">Loop-Back SOAP Calls and Direct Linking</span><span class="sxs-lookup"><span data-stu-id="40547-138">Loop-Back SOAP Calls and Direct Linking</span></span>](loop-back-soap-calls-and-direct-linking.md)
- [<span data-ttu-id="40547-139">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="40547-139">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
- [<span data-ttu-id="40547-140">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="40547-140">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
- [<span data-ttu-id="40547-141">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="40547-141">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
- [<span data-ttu-id="40547-142">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="40547-142">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
