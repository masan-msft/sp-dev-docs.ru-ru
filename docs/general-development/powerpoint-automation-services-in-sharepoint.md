---
title: "PowerPoint Automation Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 168c7dc0-fbdc-41a2-84db-65d211d3d673
ms.openlocfilehash: 38aaa276eb79da8e7ad6a63e4b043c762535923a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="powerpoint-automation-services-in-sharepoint"></a><span data-ttu-id="be407-102">PowerPoint Automation Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="be407-102">PowerPoint Automation Services in SharePoint</span></span>
<span data-ttu-id="be407-103">Изучите использование Службы автоматизации Microsoft PowerPoint для выполнения преобразования на сервере презентации в и различные форматы файлов.</span><span class="sxs-lookup"><span data-stu-id="be407-103">Learn to use Microsoft PowerPoint Automation Services to do server-side presentation conversions to and from a variety of file formats.</span></span> 

## <a name="introduction"></a><span data-ttu-id="be407-104">Введение</span><span class="sxs-lookup"><span data-stu-id="be407-104">Introduction</span></span>
<span data-ttu-id="be407-105"><a name="PAS_Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="be407-105"></span></span>

<span data-ttu-id="be407-106">Многие компании, крупных и мелких, используют их библиотеки Microsoft SharePoint Server в качестве хранилища для презентаций Microsoft PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="be407-106">Many businesses, large and small, use their Microsoft SharePoint Server libraries as a repository for Microsoft PowerPoint presentations.</span></span> <span data-ttu-id="be407-107">Все эти предприятия имеют собственные конкретных нужд для хранения, распространение и обновление свои презентации.</span><span class="sxs-lookup"><span data-stu-id="be407-107">These businesses all have their own particular needs for storing, distributing, and updating their presentations.</span></span> <span data-ttu-id="be407-108">Microsoft PowerPoint Automation Services — это новая возможность Microsoft SharePoint, которые могут помочь предприятия для управления свои презентации.</span><span class="sxs-lookup"><span data-stu-id="be407-108">Microsoft PowerPoint Automation Services is a new feature of Microsoft SharePoint that can help enterprises to manage their presentations.</span></span> <span data-ttu-id="be407-109">Это общая служба, которая предоставляет выполнять на сервере преобразование презентации в других форматах.</span><span class="sxs-lookup"><span data-stu-id="be407-109">It is a shared service that provides unattended, server-side conversion of presentations into other formats.</span></span> <span data-ttu-id="be407-110">Он был разработан с самого начала работы на серверах и могут быть обработаны много файлов презентации в виде надежного и предсказуемым.</span><span class="sxs-lookup"><span data-stu-id="be407-110">It was designed from the outset to work on servers and can process many presentation files in a reliable and predictable manner.</span></span>
  
    
    
<span data-ttu-id="be407-p102">С помощью Службы автоматизации PowerPoint, можно преобразовать из формата двоичного файла PowerPoint (.ppt) и в PowerPoint формат файлов Open XML (PPTX-файл) в других форматах. Например может потребоваться обновление пакета PowerPoint 97 - 2003 файлов для файлов презентация Open XML. Можно также создать дополнительное действие в меню **Правка**, чтобы разрешить пользователям создавать версию PDF презентаций по запросу.</span><span class="sxs-lookup"><span data-stu-id="be407-p102">Using PowerPoint Automation Services, you can convert from the PowerPoint binary file format (.ppt) and the PowerPoint Open XML file format (.pptx) to other formats. For example, you may want to upgrade a batch of PowerPoint 97-2003 files to Open XML presentation files. You could also create a custom action in the **Edit** menu to allow users to create a PDF version of presentations on demand.</span></span>
  
    
    

> <span data-ttu-id="be407-114">**Примечание:** Службы автоматизации PowerPoint использует средства SharePoint и — новым компонентом.</span><span class="sxs-lookup"><span data-stu-id="be407-114">**Note:** PowerPoint Automation Services takes advantage of facilities of SharePoint and is a feature of it.</span></span> <span data-ttu-id="be407-115">Необходимо иметь SharePoint для использования службы автоматизации PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="be407-115">You must have SharePoint installed to use PowerPoint Automation Services.</span></span> <span data-ttu-id="be407-116">При использовании SharePoint в ферме серверов, необходимо явно включить PowerPoint Automation Services.</span><span class="sxs-lookup"><span data-stu-id="be407-116">If you are using SharePoint in a server farm, you must explicitly enable PowerPoint Automation Services.</span></span> 
  
    
    


## <a name="powerpoint-automation-services-scenarios"></a><span data-ttu-id="be407-117">Сценарии PowerPoint Automation Services</span><span class="sxs-lookup"><span data-stu-id="be407-117">PowerPoint Automation Services scenarios</span></span>
<span data-ttu-id="be407-118"><a name="PAS_Scenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="be407-118"></span></span>

<span data-ttu-id="be407-119">Ниже описаны несколько способов, Службы автоматизации PowerPoint можно использовать для автоматизации обработки презентаций на сервере:</span><span class="sxs-lookup"><span data-stu-id="be407-119">The following scenarios describe a couple of ways that you can use PowerPoint Automation Services to automate processing presentations on a server:</span></span>
  
    
    

- <span data-ttu-id="be407-p104">Большое предприятие хранятся все их годовая прибыль презентаций в одну библиотеку документов на сайте интрасети. Библиотека содержит большое число презентаций, собранные за несколько лет. Как ИТ-отдел, где требуется реализовать для обновления всех файлов презентации в PowerPoint формате двоичных файлов 97 - 2003 (.ppt) в формат файлов презентация Open XML (PPTX-файл). Разработчик, используемая для выполнения преобразования решает развернуть решение на сервере, который будет выполнять итерацию по каждому из файлов в библиотеке, проверьте, является ли файл в формате .ppt и преобразование каждого PPT-файл в формате PPTX-файл.</span><span class="sxs-lookup"><span data-stu-id="be407-p104">A large enterprise stores all of their yearly earnings presentations in a single document library on a corporate intranet site. The library contains a large number of presentations that have accumulated over the years. The IT department wants to upgrade all of the presentation files in the PowerPoint 97-2003 binary file format (.ppt) to the Open XML presentation file format (.pptx). The developer who is performing the conversion decides to deploy a solution to the server that will iterate through each of the files in the library, check to see whether the file is in the .ppt format, and convert each .ppt file to the .pptx file format.</span></span>
    
  
- <span data-ttu-id="be407-p105">Региональные отдела продаж предоставляет настраиваемые службы оценок для каждого из клиентов. Каждого продавца дается обзор их квот с клиентами в собрании, в лицо или online. После собрания, менеджер по продажам содержит копию предложения с расценками для клиента в виде PDF-файла. Отдел заключает соглашения поставщика для создания пользовательской команды в меню " **Правка** " для файлов PowerPoint, хранящиеся в библиотеке документов в их экстрасети. При выборе команды сервера запускает программу, который преобразует файл PowerPoint PDF-ФАЙЛ, расположенный в одной библиотеке.</span><span class="sxs-lookup"><span data-stu-id="be407-p105">A regional sales department provides custom service estimates to each of their clients. Each salesperson reviews their quotes with clients in a meeting, either in-person or online. After the meeting, the salesperson provides a copy of the quote to the customer in the form of a PDF. The department hires a vendor to create a custom verb in the **Edit** menu for PowerPoint files stored in a document library in their extranet. When the verb is clicked, the server runs a program that converts the PowerPoint file to a PDF located in the same library.</span></span>
    
  

### <a name="supported-source-presentation-formats"></a><span data-ttu-id="be407-129">Поддерживаемый источник форматов представления</span><span class="sxs-lookup"><span data-stu-id="be407-129">Supported source presentation formats</span></span>

<span data-ttu-id="be407-130">Доступны следующие форматы презентации поддерживаемый источник для преобразования:</span><span class="sxs-lookup"><span data-stu-id="be407-130">The supported source presentation formats for conversion are as follows:</span></span>
  
    
    

- <span data-ttu-id="be407-131">Презентация форматов Open XML формат файлов (PPTX-файл)</span><span class="sxs-lookup"><span data-stu-id="be407-131">Open XML File Format presentation format (.pptx)</span></span>
    
  
- <span data-ttu-id="be407-132">Презентация PowerPoint 97 - 2003 (.ppt)</span><span class="sxs-lookup"><span data-stu-id="be407-132">PowerPoint 97-2003 presentation (.ppt)</span></span>
    
  

### <a name="supported-destination-document-formats"></a><span data-ttu-id="be407-133">Поддерживаемые целевые форматы документов</span><span class="sxs-lookup"><span data-stu-id="be407-133">Supported destination document formats</span></span>

<span data-ttu-id="be407-134">Поддерживаемые целевые форматы документов включают все поддерживаемые форматы исходных документов и следующее:</span><span class="sxs-lookup"><span data-stu-id="be407-134">The supported destination document formats include all of the supported source document formats and the following:</span></span>
  
    
    

- <span data-ttu-id="be407-135">PPTX-файл (в формате презентации формат файлов open XML)</span><span class="sxs-lookup"><span data-stu-id="be407-135">.pptx (Open XML File Format presentation format)</span></span>
    
  
- <span data-ttu-id="be407-136">PDF-файл</span><span class="sxs-lookup"><span data-stu-id="be407-136">.pdf</span></span>
    
  
- <span data-ttu-id="be407-137">расширением XPS (open XML Paper Specification)</span><span class="sxs-lookup"><span data-stu-id="be407-137">.xps (Open XML Paper Specification)</span></span>
    
  
- <span data-ttu-id="be407-138">.jpg</span><span class="sxs-lookup"><span data-stu-id="be407-138">.jpg</span></span>
    
  
- <span data-ttu-id="be407-139">Рисунок в формате Portable Network Graphics</span><span class="sxs-lookup"><span data-stu-id="be407-139">.png (Portable Network Graphics Format)</span></span>
    
  

### <a name="limitations-of-powerpoint-automation-services"></a><span data-ttu-id="be407-140">Ограничения для службы автоматизации PowerPoint</span><span class="sxs-lookup"><span data-stu-id="be407-140">Limitations of PowerPoint Automation Services</span></span>

<span data-ttu-id="be407-p106">Службы автоматизации PowerPoint не включает возможности для печати документов. Тем не менее он не вызывает затруднений для преобразования файлов PowerPoint презентации (PPT и PPTX-файл) в файл PDF или XPS и очереди их к принтеру.</span><span class="sxs-lookup"><span data-stu-id="be407-p106">PowerPoint Automation Services does not include capabilities for printing documents. However, it is straightforward to convert PowerPoint presentation files (.ppt and .pptx) to PDF or XPS and spool them to a printer.</span></span>
  
    
    

## <a name="powerpoint-automation-services-api"></a><span data-ttu-id="be407-143">API-Интерфейс служб автоматизации PowerPoint</span><span class="sxs-lookup"><span data-stu-id="be407-143">PowerPoint Automation Services API</span></span>
<span data-ttu-id="be407-144"><a name="PAS_APIs"> </a></span><span class="sxs-lookup"><span data-stu-id="be407-144"></span></span>

<span data-ttu-id="be407-145">Для использования службы автоматизации PowerPoint, используйте его API-интерфейс для отправки запросов на преобразование на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be407-145">To use PowerPoint Automation Services, you use its programming interface to send a conversion request to the SharePoint server.</span></span> <span data-ttu-id="be407-146">Для каждого преобразования запроса необходимо указать, какие файлы, которое требуется преобразовать и выходной формат задания преобразования.</span><span class="sxs-lookup"><span data-stu-id="be407-146">For each conversion request, you specify which files you want to convert and the output format of the conversion job.</span></span> <span data-ttu-id="be407-147">Для некоторых запросов на преобразование, также можно указать что преобразования типов контента, включая комментарии, скрытые слайды или свойств документа.</span><span class="sxs-lookup"><span data-stu-id="be407-147">For some conversion requests, you can also specify what types of content is converted, including comments, hidden slides, or document properties.</span></span>
  
    
    
<span data-ttu-id="be407-p108">Службы автоматизации PowerPoint использует метод асинхронной модели для отправки и получения запросов на преобразование. Таким образом можно написать код, который продолжает выполняться после отправки запросов на преобразование. Если требуется отправлять уведомления для пользователей после завершения запросов на преобразование, можно указать делегата, который ссылается на метод обратного вызова для выполнения после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="be407-p108">PowerPoint Automation Services uses the asynchronous pattern method for sending and receiving conversion requests. Thus, you can write code that continues to execute after a conversion request has been sent. If you need to provide notification to users after a conversion request has been completed, you can specify a delegate that references a callback method to execute when the operation completes.</span></span> 
  
    
    

> <span data-ttu-id="be407-151">**Примечание:** Дополнительные сведения о работе с шаблоном асинхронного видеть [Обзор асинхронного программирования](http://msdn.microsoft.com/en-us/library/ms228963.aspx).</span><span class="sxs-lookup"><span data-stu-id="be407-151">**Note:** For more information about how to work with the asynchronous design pattern, see the  [Asynchronous Programming Overview](http://msdn.microsoft.com/en-us/library/ms228963.aspx).</span></span> 
  
    
    

<span data-ttu-id="be407-p109">В следующих разделах содержат ограниченный список классов, которые необходимы для отправки и получения запросами преобразования. Все эти классы содержатся в пространстве имен **Microsoft.Office.Server.PowerPoint.Conversion**.</span><span class="sxs-lookup"><span data-stu-id="be407-p109">The sections below contain a limited list of the classes that are necessary for sending and receiving a conversion requests. All of these classes are contained in the **Microsoft.Office.Server.PowerPoint.Conversion** namespace.</span></span>
  
    
    

### <a name="request-base-class"></a><span data-ttu-id="be407-154">Базовый класс запроса</span><span class="sxs-lookup"><span data-stu-id="be407-154">Request Base Class</span></span>

<span data-ttu-id="be407-p110">Класс **Request** является основных классов в пространстве имен **Microsoft.Office.Server.PowerPoint.Conversion**. Все другие типызапроса  **PresentationRequest**, **PictureRequest**, **PdfRequest**и **XpsRequest** от него.</span><span class="sxs-lookup"><span data-stu-id="be407-p110">The **Request** class is the most fundamental class within the **Microsoft.Office.Server.PowerPoint.Conversion** namespace. All of the otherrequest types— **PresentationRequest**, **PictureRequest**, **PdfRequest**, and **XpsRequest**—inherit from it.</span></span> 
  
    
    

<span data-ttu-id="be407-157">**В таблице 1. Запрос членов базового класса**</span><span class="sxs-lookup"><span data-stu-id="be407-157">**Table 1. Request base class members**</span></span>


|<span data-ttu-id="be407-158">**Имя элемента**</span><span class="sxs-lookup"><span data-stu-id="be407-158">**Member name**</span></span>|<span data-ttu-id="be407-159">**Описание**</span><span class="sxs-lookup"><span data-stu-id="be407-159">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="be407-160">метод **BeginConvert(Microsoft.SharePoint.SPServiceContext, System.AsyncCallback, System.Object)**</span><span class="sxs-lookup"><span data-stu-id="be407-160">**BeginConvert(Microsoft.SharePoint.SPServiceContext, System.AsyncCallback, System.Object)** method</span></span> <br/> |<span data-ttu-id="be407-p111">Начинает операцию преобразования. Первым параметром  _serviceContext_указывает контекста сайта SharePoint, где находится файл для преобразования. Параметр  _callback_ используется для задания делегата, который ссылается на метода, выполняемого после завершения операции. Если нужно передать любые дополнительные сведения из кода, вызывающего метод обратного вызова, используйте параметр _state_. </span><span class="sxs-lookup"><span data-stu-id="be407-p111">Begins the conversion operation. The first parameter,  _serviceContext_, specifies the context of the SharePoint site where the file to be converted is located. Use the  _callback_ parameter to specify a delegate that references a method to execute once the operation has completed. Use the _state_ parameter if you need to pass any additional information from the calling code to the callback method. </span></span><br/> <span data-ttu-id="be407-165">Возвращает объект  [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) .</span><span class="sxs-lookup"><span data-stu-id="be407-165">Returns an  [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) object.</span></span> <br/> |
|<span data-ttu-id="be407-166">метод **EndConvert(IAsyncResult)**</span><span class="sxs-lookup"><span data-stu-id="be407-166">**EndConvert(IAsyncResult)** method</span></span> <br/> |<span data-ttu-id="be407-p112">Завершает операцию преобразования. Параметр  _result_ ожидает результирующего объекта [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) , которое возвращает соответствующего запроса **BeginConvert** преобразования. Если этот запрос не был завершен при вызове **EndConvert**, вызывающий поток блокируется до завершения операции преобразования. </span><span class="sxs-lookup"><span data-stu-id="be407-p112">Ends the conversion operation. The  _result_ parameter expects the resulting [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) object that the corresponding **BeginConvert** conversion request returns. If that request has not been completed when **EndConvert** is called, the calling thread is blocked until the conversion operation is complete. </span></span><br/> <span data-ttu-id="be407-170">Не возвращает значение.</span><span class="sxs-lookup"><span data-stu-id="be407-170">Does not return a value.</span></span>  <br/> |
   

### <a name="presentationrequest-class"></a><span data-ttu-id="be407-171">Класс PresentationRequest</span><span class="sxs-lookup"><span data-stu-id="be407-171">PresentationRequest class</span></span>

<span data-ttu-id="be407-p113">Класс **PresentationRequest**, который наследует от класса **Request**, преобразует файл PowerPoint 97 - 2003 (.ppt) или презентаций формат файлов Open XML (PPTX-файл) в другой формат презентации. В первом случае уже было сказано этот класс используется для преобразования старые файлы презентаций в библиотеке документов в формате презентаций формат файлов Open XML.</span><span class="sxs-lookup"><span data-stu-id="be407-p113">The **PresentationRequest** class, which inherits from the **Request** class, converts a PowerPoint 97-2003 file (.ppt) or Open XML File Format presentation (.pptx) to another presentation file format. In the first scenario mentioned above, you use this class to convert older presentation files in a document library to the Open XML File Format presentation format.</span></span>
  
    
    
<span data-ttu-id="be407-174">Метод-конструктор для класса **PresentationRequest** содержит три требуемые параметры:</span><span class="sxs-lookup"><span data-stu-id="be407-174">The constructor method for the **PresentationRequest** class has three required parameters:</span></span>
  
    
    

-  <span data-ttu-id="be407-175">_input_ файл, который требуется выполнить преобразование как объект  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) .</span><span class="sxs-lookup"><span data-stu-id="be407-175">_input_—Takes the file that you want to convert as a  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object.</span></span>
    
  
-  <span data-ttu-id="be407-176">_extension_ строка, указывающая расширение файла преобразуемого файла.</span><span class="sxs-lookup"><span data-stu-id="be407-176">_extension_—A string that specifies the file extension of the file being converted.</span></span>
    
  
-  <span data-ttu-id="be407-177">_output_ объект  [SPFileStream](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfilestream.aspx) , указывающий, где будут храниться выходные данные.</span><span class="sxs-lookup"><span data-stu-id="be407-177">_output_—An  [SPFileStream](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfilestream.aspx) object that specifies where the output will be stored.</span></span>
    
  
<span data-ttu-id="be407-p114">Класс **PresentationRequest** имеет один перегрузки для метода конструктора, добавляющий параметр _settings_. Параметр _settings_ объект **PresentationSettings** принимает в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="be407-p114">The **PresentationRequest** class has a single overload for its constructor method that adds a _settings_ parameter. The _settings_ parameter accepts a **PresentationSettings** object as an argument.</span></span>
  
    
    

> <span data-ttu-id="be407-180">**Совет:** При преобразовании выходные данные [потока](https://msdn.microsoft.com/library/System.IO.Stream.aspx) объекта обратно на объект [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) проверьте, что данное расширение имени файла, присвоенное созданный файл сопоставляет расширение типа файлов, которое (PPT или PPTX-файл).</span><span class="sxs-lookup"><span data-stu-id="be407-180">**Tip:** When converting the output  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object back to an [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) object, check that the extension given to the resulting file matches the extension of the file type that you want (.ppt or .pptx).</span></span>
  
    
    


### <a name="pdfrequest-class"></a><span data-ttu-id="be407-181">Класс PdfRequest</span><span class="sxs-lookup"><span data-stu-id="be407-181">PdfRequest class</span></span>

<span data-ttu-id="be407-p115">Класс **PdfRequest**, который наследуется от класса **Request**, преобразует файл PowerPoint 97 - 2003 (.ppt) или презентаций формат файлов Open XML (PPTX-файл) в файл a.pdf. Во втором сценарии уже было сказано этот класс используется для преобразования в PDF-файлов презентаций.</span><span class="sxs-lookup"><span data-stu-id="be407-p115">The **PdfRequest** class, which also inherits from the **Request** class, converts a PowerPoint 97-2003 file (.ppt) or Open XML File Format presentation (.pptx) to a.pdf file. In the second scenario mentioned above, you use this class to convert presentations to PDF files.</span></span>
  
    
    
<span data-ttu-id="be407-184">Метод-конструктор для класса **PdfRequest** также содержит три параметра требуется  _input_,  _extension_и  _output_ следующий класс **PresentationRequest**.</span><span class="sxs-lookup"><span data-stu-id="be407-184">The constructor method for the **PdfRequest** class also has three required parameters— _input_,  _extension_, and  _output_—similar to the **PresentationRequest** class.</span></span>
  
    
    
<span data-ttu-id="be407-p116">Класс **PdfRequest** также имеет один перегрузки для метода конструктора, добавляющий параметр _settings_. Параметр _settings_ объект **FixedFormatSettings** принимает в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="be407-p116">The **PdfRequest** class also has a single overload for its constructor method that adds a _settings_ parameter. The _settings_ parameter accepts a **FixedFormatSettings** object as an argument.</span></span>
  
    
    

> <span data-ttu-id="be407-187">**Совет:** При преобразовании выходные данные [потока](https://msdn.microsoft.com/library/System.IO.Stream.aspx) объекта обратно на объект [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) проверьте, что данное расширение имени файла, присвоенное созданный файл сопоставляет расширение типа файлов, которые должны (PDF-файл).</span><span class="sxs-lookup"><span data-stu-id="be407-187">**Tip:** When converting the output  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object back to an [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) object, check that the extension given to the resulting file matches the extension of the file type that you want (.pdf).</span></span>
  
    
    


### <a name="picturerequest-class"></a><span data-ttu-id="be407-188">Класс PictureRequest</span><span class="sxs-lookup"><span data-stu-id="be407-188">PictureRequest class</span></span>

<span data-ttu-id="be407-189">Класс **PictureRequest**, который наследуется от класса **Request**, преобразует PowerPoint 97 - 2003 файла (.ppt) или презентаций формат файлов Open XML (PPTX-файл) в коллекцию файлы изображений в формате the.jpg или PNG.</span><span class="sxs-lookup"><span data-stu-id="be407-189">The **PictureRequest** class, which also inherits from the **Request** class, converts a PowerPoint 97-2003 file (.ppt) or Open XML File Format presentation (.pptx) to a collection of image files in either the.jpg or .png format.</span></span>
  
    
    
<span data-ttu-id="be407-p117">Метод-конструктор для класса **PictureRequest** также имеет четыре требуемые параметры. Параметры _input_,  _extension_и  _output_ похожи на параметры для конструктора класса **PresentationRequest**. Метод-конструктор для класса **PictureRequest** также имеет параметр необходимые _format_, должна быть константа из перечисления **PictureFormat**.</span><span class="sxs-lookup"><span data-stu-id="be407-p117">The constructor method for the **PictureRequest** class also has four required parameters. The _input_,  _extension_, and  _output_ parameters are similar to the parameters for the **PresentationRequest** class constructor. The constructor method for the **PictureRequest** class also has a required _format_ parameter, which must be a constant from the **PictureFormat** enumeration.</span></span>
  
    
    
<span data-ttu-id="be407-193">Класс **PictureRequest** имеет любой перегрузки метода конструктора.</span><span class="sxs-lookup"><span data-stu-id="be407-193">The **PictureRequest** class does not have any overloads for its constructor method.</span></span>
  
    
    

> <span data-ttu-id="be407-194">**Совет:** Класс **PictureRequest** возвращает поток, содержащий пакет файлы изображений.</span><span class="sxs-lookup"><span data-stu-id="be407-194">**Tip:** The **PictureRequest** class returns a stream that contains a package of image files.</span></span> <span data-ttu-id="be407-195">При преобразовании выходные данные [потока](https://msdn.microsoft.com/library/System.IO.Stream.aspx) объекта обратно в объект [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) , убедитесь, что данное расширение имени файла, присвоенное созданный файл .zip.</span><span class="sxs-lookup"><span data-stu-id="be407-195">When converting the output [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) object back to an [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) object, check that the extension given to the resulting file is .zip.</span></span>
  
    
    


## <a name="building-a-powerpoint-automation-services-application"></a><span data-ttu-id="be407-196">Создание приложения PowerPoint Automation Services</span><span class="sxs-lookup"><span data-stu-id="be407-196">Building a PowerPoint Automation Services application</span></span>
<span data-ttu-id="be407-197"><a name="PAS_Build"> </a></span><span class="sxs-lookup"><span data-stu-id="be407-197"></span></span>

<span data-ttu-id="be407-p119">Это самый простой способ показано, как писать код, использующий Службы автоматизации PowerPoint является создание консольного приложения. Необходимо построение и запуск консольного приложения на SharePoint Server, а не на клиентском компьютере. Для запуска запросов на преобразование тот же ли код запроса преобразования является частью веб-части, рабочего процесса или обработчик событий. С помощью Службы автоматизации PowerPoint консольного приложения, следующей процедуре показано, как использовать API без добавления сложности веб-части, обработчик событий или рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="be407-p119">The easiest way to show how to write code that uses PowerPoint Automation Services is to build a console application. You must build and run the console application on the SharePoint Server, not on a client computer. The code to start conversion requests is similar whether the conversion request code is incorporated into a Web Part, a workflow, or an event handler. By using PowerPoint Automation Services from a console application, the following procedure shows how to use the API without adding the complexities of a Web Part, an event handler, or a workflow.</span></span>
  
    
    

> <span data-ttu-id="be407-202">**Примечание:** Так как PowerPoint Automation Services — это служба SharePoint, его можно использовать только в приложении, на котором выполняется непосредственно на сервере SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="be407-202">**Note:** Because PowerPoint Automation Services is a service of SharePoint, you can use it only in an application that runs directly on a SharePoint Server.</span></span> <span data-ttu-id="be407-203">Необходимо создать приложение, как решение фермы.</span><span class="sxs-lookup"><span data-stu-id="be407-203">You must build the application as a farm solution.</span></span> <span data-ttu-id="be407-204">Нельзя использовать PowerPoint Automation Services из изолированного решения.</span><span class="sxs-lookup"><span data-stu-id="be407-204">You cannot use PowerPoint Automation Services from a sandboxed solution.</span></span> 
  
    
    


### <a name="to-build-the-application"></a><span data-ttu-id="be407-205">Построение приложения</span><span class="sxs-lookup"><span data-stu-id="be407-205">To build the application</span></span>


1. <span data-ttu-id="be407-206">Запустите приложение Microsoft Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="be407-206">Start Microsoft Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="be407-207">В меню **файл** выберите команду **Создать** и затем выберите **проект**.</span><span class="sxs-lookup"><span data-stu-id="be407-207">On the **File** menu, point to **New**, and then choose **Project**.</span></span> 
    
  
3. <span data-ttu-id="be407-208">В диалоговом окне **Новый проект** в разделе **Установленные** **Шаблоны**, разверните узел **Visual C#** и выберите **Windows**.</span><span class="sxs-lookup"><span data-stu-id="be407-208">In the **New Project** dialog box, under **Installed**, expand **Templates**, expand **Visual C#**, and then chose **Windows**.</span></span>
    
  
4. <span data-ttu-id="be407-209">В списке шаблонов проектов выберите пункт **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="be407-209">In the list of project templates, choose **Console Application**.</span></span>
    
  
5. <span data-ttu-id="be407-210">Убедитесь, что проект в Visual Studio предназначен для .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="be407-210">Be sure that the project in Visual Studio targets .NET Framework 4.</span></span>
    
    > <span data-ttu-id="be407-211">**Примечание:** Предыдущие версии SharePoint Server требуется платформы .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="be407-211">**Note:** Previous versions of SharePoint Server required that you target .NET Framework 3.5.</span></span> <span data-ttu-id="be407-212">Теперь библиотек Microsoft.SharePoint ссылок на сборки в .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="be407-212">The Microsoft.SharePoint libraries now reference assemblies in .NET Framework 4.</span></span> <span data-ttu-id="be407-213">Убедиться в том, что проект предназначен для полной платформы .NET Framework 4 и не профиль клиента для .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="be407-213">Also make sure that your project targets the full .NET Framework 4 and not the .NET Framework 4 Client Profile.</span></span> 
6. <span data-ttu-id="be407-214">В поле **имя** введите имя, которое вы хотите использовать для проекта, например PAS_Sample.</span><span class="sxs-lookup"><span data-stu-id="be407-214">In the **Name** box, type the name that you want to use for your project, such as PAS_Sample.</span></span>
    
  
7. <span data-ttu-id="be407-215">В поле **Расположение** укажите место для сохранения проекта.</span><span class="sxs-lookup"><span data-stu-id="be407-215">In the **Location** box, type the location where you want to place the project.</span></span>
    
  
8. <span data-ttu-id="be407-216">Нажмите кнопку **ОК**, чтобы создать решение.</span><span class="sxs-lookup"><span data-stu-id="be407-216">Click **OK** to create the solution.</span></span>
    
  
9. <span data-ttu-id="be407-217">По умолчанию Visual Studio 2012 создаются проекты, процессоров x 86, но создавать SharePoint Server приложения, следует задать любой Процессор.</span><span class="sxs-lookup"><span data-stu-id="be407-217">By default, Visual Studio 2012 creates projects that target x86 CPUs, but to build SharePoint Server applications, you must target any CPU.</span></span>
    
    <span data-ttu-id="be407-218">При создании приложения Microsoft Visual C#, в **Окне Обозреватель решений** щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="be407-218">If you are building a Microsoft Visual C# application, in **Solution Explorer**, right-click the project, and then click **Properties**.</span></span>
    
  - <span data-ttu-id="be407-219">В окне **свойств** проекта щелкните **Построить**.</span><span class="sxs-lookup"><span data-stu-id="be407-219">In the project **Properties** window, click **Build**.</span></span>
    
  
  - <span data-ttu-id="be407-220">Укажите на список **конфигурации** и выберите пункт **Все конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="be407-220">Point to the **Configuration** list, and select **All Configurations**.</span></span>
    
  
  - <span data-ttu-id="be407-221">Укажите на список **Целевая платформа** и выберите **Любой ЦП**.</span><span class="sxs-lookup"><span data-stu-id="be407-221">Point to the **Platform Target** list, and select **Any CPU**.</span></span>
    
  

    
    
    <span data-ttu-id="be407-222">При создании Microsoft Visual Basic приложения .NET Framework, в окне **Свойства** щелкните **Компиляция**.</span><span class="sxs-lookup"><span data-stu-id="be407-222">If you are building a Microsoft Visual Basic .NET Framework application, in the **Properties** window, click **Compile**.</span></span>
    
  - <span data-ttu-id="be407-223">Щелкните **Дополнительные параметры компиляции**.</span><span class="sxs-lookup"><span data-stu-id="be407-223">Click **Advanced Compile Options**.</span></span>
    
  
  - <span data-ttu-id="be407-224">Укажите на список **конфигурации**, а затем выберите **Все конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="be407-224">Point to the **Configuration** list, and then select **All Configurations**.</span></span>
    
  
  - <span data-ttu-id="be407-225">Укажите на список **Целевая платформа** и выберите **Любой ЦП**.</span><span class="sxs-lookup"><span data-stu-id="be407-225">Point to the **Platform Target** list, and then click **Any CPU**.</span></span>
    
  

    
    
  
10. <span data-ttu-id="be407-226">В меню **Проект** выберите команду **Добавить ссылку**. Откроется диалоговое окно **Добавление ссылки**.</span><span class="sxs-lookup"><span data-stu-id="be407-226">On the **Project** menu, click **Add Reference** to open the **Add Reference** dialog box.</span></span>
    
  
11. <span data-ttu-id="be407-227">Разверните узел **сборки**, а затем выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="be407-227">Expand **Assemblies**, and then do the following:</span></span>
    
  - <span data-ttu-id="be407-228">Разверните узел **Framework**, а затем добавьте ссылку на System.Web.</span><span class="sxs-lookup"><span data-stu-id="be407-228">Expand **Framework**, and then add a reference to System.Web.</span></span>
    
  
  - <span data-ttu-id="be407-229">Разверните узел **расширения**, а затем добавьте ссылку на Microsoft.SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be407-229">Expand **Extensions**, and then add a reference to Microsoft.SharePoint.</span></span>
    
  
12. <span data-ttu-id="be407-230">Также в диалоговом окне **Добавление ссылки** нажмите кнопку **Обзор**, перейдите в расположение для Microsoft.Office.Server.PowerPoint.dll, (C:\\Windows\\Microsoft.NET\\assembly\\GAC_MSIL\\Microsoft.Office.Server.PowerPoint\\v4.0_15.0.0.0__71e9bce111e9429c  это местоположение по умолчанию), выберите сборку и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="be407-230">Also in the **Add Reference** dialog box, choose **Browse**, navigate to the location for the Microsoft.Office.Server.PowerPoint.dll (default location is C:\\Windows\\Microsoft.NET\\assembly\\GAC_MSIL\\Microsoft.Office.Server.PowerPoint\\v4.0_15.0.0.0__71e9bce111e9429c), select the assembly, and then choose **Add**.</span></span> 
    
  
<span data-ttu-id="be407-231">В следующих примерах C# и Visual Basic показано это приложение простого Службы автоматизации PowerPoint, преобразует PowerPoint файла 97 - 2003 (.ppt) в папке общих документов на сайте SharePoint для файла PowerPoint Open XML (PPTX-файл) в той же папке.</span><span class="sxs-lookup"><span data-stu-id="be407-231">The following C# and Visual Basic examples show a simple PowerPoint Automation Services application that converts a PowerPoint 97-2003 file (.ppt) in the Shared Documents folder of a SharePoint site to a PowerPoint Open XML file (.pptx) in the same folder.</span></span>
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Web;
using Microsoft.SharePoint;
using Microsoft.Office.Server.PowerPoint.Conversion;

namespace PAS_Sample
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                string siteURL = "http://localhost";
                using (SPSite site = new SPSite(siteURL))
                {
                    using (SPWeb web = site.OpenWeb())
                    {
                        Console.WriteLine("Begin conversion");

                        // Get a reference to the "Shared Documents" library 
                        // and the presentation file to be converted.
                        SPFolder docs = web.Folders[siteURL + 
                            "/Shared Documents"];
                        SPFile file = docs.Files[siteURL + 
                            "/Shared Documents/Pres1.ppt"];

                        // Convert the file to a stream and create an
                        // SPFileStream object for the conversion output.
                        Stream fStream = file.OpenBinaryStream();
                        SPFileStream stream = new SPFileStream(web, 0x1000);

                        // Create the presentation conversion request.
                        PresentationRequest request = new PresentationRequest(
                            fStream,
                            ".ppt",
                            stream);

                        // Send the request synchronously, passing
                        // in a 'null' value for the callback parameter, 
                        // and capturing the response in the result object.
                        IAsyncResult result = request.BeginConvert(
                            SPServiceContext.GetContext(site),
                            null,
                            null);

                        // Use the EndConvert method to get the result. 
                        request.EndConvert(result);

                        // Add the converted file to the document library.
                        SPFile newFile = docs.Files.Add(
                            "newPres1.pptx", 
                            stream, 
                            true);
                        Console.WriteLine("Output: {0}", newFile.Url);

                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error: " + ex.Message);
            }
            finally
            {
                Console.WriteLine("Complete");
                Console.ReadKey();
            }
        }
    }
}
```




```VB.net

Imports System
Imports System.Collections.Generic
Imports System.IO
Imports System.Linq
Imports System.Text
Imports System.Web
Imports Microsoft.SharePoint
Imports Microsoft.Office.Server.PowerPoint.Conversion

Namespace PAS_Sample
    Class Program
        Private Shared Sub Main(args As String())
            Try
                Dim siteURL As String = "http://localhost"
                Using site As New SPSite(siteURL)
                    Using web As SPWeb = site.OpenWeb()
                        Console.WriteLine("Begin conversion")

                        ' Get a reference to the "Shared Documents" library 
                        ' and the presentation file to be converted.
                        Dim docs As SPFolder = web.Folders(siteURL + _
                            "/Shared Documents")
                        Dim file As SPFile = docs.Files(siteURL + _
                            "/Shared Documents/Pres1.ppt")

                        ' Convert the file to a stream and create an
                        ' SPFileStream object for the conversion output.
                        Dim fStream As Stream = file.OpenBinaryStream()
                        Dim stream As New SPFileStream(web, &amp;H1000)

                        ' Create the presentation conversion request.
                        Dim request As New PresentationRequest(fStream, _
                            ".ppt", 
                            stream)

                        ' Send the request synchronously, passing
                        ' in a Nothing value for the callback parameter, 
                        ' and capturing the response in the result object.
                        Dim result As IAsyncResult = request.BeginConvert(_
                            SPServiceContext.GetContext(site), _
                            Nothing, _
                            Nothing)

                        ' Use the EndConvert method to get the result. 
                        request.EndConvert(result)

                        ' Add the converted file to the document library.
                        Dim newFile As SPFile = docs.Files.Add(_
                            "newPres1.pptx", _
                            stream, _
                            True)

                        Console.WriteLine("Output: {0}", newFile.Url)
                    End Using
                End Using
            Catch ex As Exception
                Console.WriteLine("Error: " + ex.Message)
            Finally
                Console.WriteLine("Complete")
                Console.ReadKey()
            End Try
        End Sub
    End Class
End Namespace

```


### <a name="to-build-and-run-the-example"></a><span data-ttu-id="be407-232">Построение и запуск примера</span><span class="sxs-lookup"><span data-stu-id="be407-232">To build and run the example</span></span>


1. <span data-ttu-id="be407-233">Добавьте документ PowerPoint с именем Pres1.ppt в папку общих документов на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be407-233">Add a PowerPoint document named Pres1.ppt to the Shared Documents folder in the SharePoint site.</span></span>
    
  
2. <span data-ttu-id="be407-234">Постройте и запустите пример.</span><span class="sxs-lookup"><span data-stu-id="be407-234">Build and run the example.</span></span>
    
  
3. <span data-ttu-id="be407-p122">Истечении одной минуты для запуска процесса преобразования, перейдите в папку "Общие документы" на сайте SharePoint и обновить страницу. Библиотека документов теперь содержит новый документ PowerPoint, Pres1.pptx.</span><span class="sxs-lookup"><span data-stu-id="be407-p122">After waiting one minute for the conversion process to run, navigate to the Shared Documents folder in the SharePoint site, and refresh the page. The document library now contains a new PowerPoint document, Pres1.pptx.</span></span>
    
  
<span data-ttu-id="be407-237">Службы автоматизации PowerPoint на SharePoint предоставляет бизнеса с расширенными возможностями для управления их файлы презентаций.</span><span class="sxs-lookup"><span data-stu-id="be407-237">PowerPoint Automation Services on SharePoint provides businesses with advanced capabilities for managing their presentation files.</span></span> <span data-ttu-id="be407-238">В этом решении высокой производительности позволяет управлять презентации масштабируемый, на сервере, формирования, как пакет или по запросу.</span><span class="sxs-lookup"><span data-stu-id="be407-238">This high-performance solution allows scalable, server-side presentation manipulation and generation, as a batch or on-demand.</span></span> 
  
    
    

> <span data-ttu-id="be407-239">**Примечание:** Прежде чем выполнять пример, убедитесь в том, что службы автоматизации PowerPoint была включена в консоли центра администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be407-239">**Note:** Before you run the example, make sure that PowerPoint Automation Services has been enabled in the SharePoint Central Administration console.</span></span><br/>  <span data-ttu-id="be407-240">Чтобы убедиться, что включен PowerPoint Automation Services, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="be407-240">To verify that PowerPoint Automation Services is enabled, do the following:</span></span> <ul><li><span data-ttu-id="be407-241">В консоли центра администрирования в разделе **Параметры системы**выберите **Управление службами на сервере**и убедитесь в том, что **Службы преобразования PowerPoint** установлено значение **запущено**.</span><span class="sxs-lookup"><span data-stu-id="be407-241">In the Central Administration console, under **System Settings**, choose **Manage services on server**, and then make sure that the **PowerPoint Conversion Service** is set to **Started**.</span></span> </li><li><span data-ttu-id="be407-242">Также в консоли центра администрирования в разделе **Управление приложениями**выберите **Управление приложениями-службами**, а затем убедитесь, что **Приложение службы преобразования PowerPoint** и **службы преобразования PowerPoint Прокси-сервер приложения** установлено значение запущено.</span><span class="sxs-lookup"><span data-stu-id="be407-242">Also in the Central Administration console, under **Application Management**, choose **Manage service applications**, and then make sure that the **PowerPoint Conversion Service Application** and **PowerPoint Conversion Service Application Proxy** are set to Started.</span></span></li></ul>
  
    
    


## <a name="conclusion"></a><span data-ttu-id="be407-243">Заключение</span><span class="sxs-lookup"><span data-stu-id="be407-243">Conclusion</span></span>
<span data-ttu-id="be407-244"><a name="PAS_Conclusion"> </a></span><span class="sxs-lookup"><span data-stu-id="be407-244"></span></span>

<span data-ttu-id="be407-245">Службы автоматизации PowerPoint на SharePoint предоставляет бизнеса с расширенными возможностями для управления их файлы презентаций.</span><span class="sxs-lookup"><span data-stu-id="be407-245">PowerPoint Automation Services on SharePoint provides businesses with advanced capabilities for managing their presentation files.</span></span> <span data-ttu-id="be407-246">В этом решении высокой производительности позволяет управлять презентации масштабируемый, на сервере, формирования, как пакет или по запросу.</span><span class="sxs-lookup"><span data-stu-id="be407-246">This high-performance solution allows scalable, server-side presentation manipulation and generation, as a batch or on-demand.</span></span> 
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="be407-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="be407-247">Additional Resources</span></span>
<span data-ttu-id="be407-248"><a name="PAS_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="be407-248"></span></span>


-  [<span data-ttu-id="be407-249">Разработка с помощью SharePoint 2010 Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="be407-249">Developing with SharePoint 2010 Word Automation Services</span></span>](http://msdn.microsoft.com/en-us/library/ff742315.aspx)
    
  
-  [<span data-ttu-id="be407-250">Центр разработчиков PowerPoint</span><span class="sxs-lookup"><span data-stu-id="be407-250">PowerPoint Developer Center</span></span>](http://msdn.microsoft.com/en-us/office/aa905465)
    
  
-  [<span data-ttu-id="be407-251">Центр по разработке для SharePoint</span><span class="sxs-lookup"><span data-stu-id="be407-251">SharePoint Developer Center</span></span>](http://msdn.microsoft.com/en-us/sharepoint/default.aspx)
    
  

