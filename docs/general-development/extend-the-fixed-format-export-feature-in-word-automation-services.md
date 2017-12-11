---
title: "Расширение функции экспорта в неизменяемом формате в службы Word Automation Services"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d8375505-432e-438e-971b-221a1d9bb601
ms.openlocfilehash: aad6cd52499a1599b15625d245e48eb46a7862be
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="extend-the-fixed-format-export-feature-in-word-automation-services"></a><span data-ttu-id="477c8-102">Расширение функции экспорта в неизменяемом формате в службы Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="477c8-102">Extend the fixed-format export feature in Word Automation Services</span></span>
<span data-ttu-id="477c8-103">Расширение Word Automation Services в Microsoft Office 2013 для замены библиотеки, используемой функции экспорта в неизменяемом формате.</span><span class="sxs-lookup"><span data-stu-id="477c8-103">Extend Word Automation Services in Microsoft Office 2013 to replace the library used by the fixed-format export feature.</span></span>
## <a name="introduction-to-the-word-file-conversion-service-fixed-format-export-feature"></a><span data-ttu-id="477c8-104">Общие сведения о Word conversion службы фиксированной форматов файлов экспорта компонента</span><span class="sxs-lookup"><span data-stu-id="477c8-104">Introduction to the Word file conversion service fixed-format export feature</span></span>

<span data-ttu-id="477c8-p101">В этой статье описывается расширение функции экспорта в неизменяемом формате Word Automation Services для использования различных экспорта в неизменяемом формате библиотеки DLL, сторонние разработчики могут заменить те, предоставляемым корпорацией Майкрософт. Этот механизм требует и расширяет интерфейс COM расширяемость фиксированного формата в клиенте Office. Для получения дополнительных сведений см  [расширение функции экспорта фиксированный формат Office 2007](http://msdn.microsoft.com/en-us/library/aa338206.aspx).</span><span class="sxs-lookup"><span data-stu-id="477c8-p101">This article describes how to extend the fixed-format export feature of Word Automation Services to use different fixed-format export DLLs, so third-party developers can replace those provided by Microsoft. This mechanism requires and extends the Office client fixed-format extensibility COM interface. For more information, see  [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/en-us/library/aa338206.aspx).</span></span>
  
    
    

## <a name="discovery"></a><span data-ttu-id="477c8-108">Обнаружение</span><span class="sxs-lookup"><span data-stu-id="477c8-108">Discovery</span></span>

<span data-ttu-id="477c8-109">Word Automation Services позволяет сторонних разработчиков заменить выходные данные фиксированного формата поддерживается:</span><span class="sxs-lookup"><span data-stu-id="477c8-109">Word Automation Services allows third-party developers to replace either or both of the fixed format outputs supported:</span></span>
  
    
    

- <span data-ttu-id="477c8-110">PDF</span><span class="sxs-lookup"><span data-stu-id="477c8-110">PDF</span></span>
    
  
- <span data-ttu-id="477c8-111">XPS</span><span class="sxs-lookup"><span data-stu-id="477c8-111">XPS</span></span>
    
  
<span data-ttu-id="477c8-112">Чтобы заменить каждого формата, библиотеки DLL должны быть расположены в одном каталоге с основной библиотеки (Sword.dll) для службы Word Automation Services (путь установки: \< \<Установка корневой\>\>\\веб-службы\\ConversionService\\ Ячейка\\конвертера\\) и должен иметь имя файла, указанного в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="477c8-112">To replace each format, the DLL must be located in the same directory as the core library (Sword.dll) for Word Automation Services (install path: \<\<install root\>\>\\WebServices\\ConversionService\\Bin\\Converter\\), and must have the specific file name specified in table 1.</span></span>
  
    
    

<span data-ttu-id="477c8-113">**В таблице 1. Имена файлов для фиксированного формата экспорта библиотеки DLL**</span><span class="sxs-lookup"><span data-stu-id="477c8-113">**Table 1. File names for fixed-format export DLLs**</span></span>


|<span data-ttu-id="477c8-114">**Формат**</span><span class="sxs-lookup"><span data-stu-id="477c8-114">**Format**</span></span>|<span data-ttu-id="477c8-115">**Имя файла**</span><span class="sxs-lookup"><span data-stu-id="477c8-115">**File Name**</span></span>|
|:-----|:-----|
|<span data-ttu-id="477c8-116">PDF</span><span class="sxs-lookup"><span data-stu-id="477c8-116">PDF</span></span>  <br/> |<span data-ttu-id="477c8-117">Renderpdf.dll</span><span class="sxs-lookup"><span data-stu-id="477c8-117">Renderpdf.dll</span></span>  <br/> |
|<span data-ttu-id="477c8-118">XPS</span><span class="sxs-lookup"><span data-stu-id="477c8-118">XPS</span></span>  <br/> |<span data-ttu-id="477c8-119">Renderxps.dll</span><span class="sxs-lookup"><span data-stu-id="477c8-119">Renderxps.dll</span></span>  <br/> |
   

## <a name="initialization"></a><span data-ttu-id="477c8-120">Инициализация</span><span class="sxs-lookup"><span data-stu-id="477c8-120">Initialization</span></span>

<span data-ttu-id="477c8-121">Библиотеки DLL необходимо экспортировать в метод с указанной ниже сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="477c8-121">The DLL must export a method with the following signature.</span></span>
  
    
    

```

HRESULT HrGetDocExporter (
IMsoDocExporter **ppimde,
IMsoServerFileManagerSite *psfms,
PFNKeepAlive pfnKeepAlive
)
```

<span data-ttu-id="477c8-122">Функции требуется DLL двух интерфейсов и указатель метода, описанных в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="477c8-122">The function requires the DLL to supply two interfaces and a method pointer, described in the following section.</span></span>
  
    
    
<span data-ttu-id="477c8-p102">Если функция возвращает сбоя службы не вернуться к экспорта предоставленные корпорацией Майкрософт. Вместо этого службы сообщает преобразования как ошибочный.</span><span class="sxs-lookup"><span data-stu-id="477c8-p102">If the function returns failure the service will not fall back to the Microsoft-provided exporter. Instead, the service will report the conversion as having failed.</span></span>
  
    
    

## <a name="imsodocexporter"></a><span data-ttu-id="477c8-125">IMsoDocExporter</span><span class="sxs-lookup"><span data-stu-id="477c8-125">IMsoDocExporter</span></span>

<span data-ttu-id="477c8-p103">Интерфейс **IMsoDocExporter** идентична существующего интерфейса, задокументированные в MSDN. Для получения дополнительных сведений см [расширение функции экспорта фиксированный формат Office 2007](http://msdn.microsoft.com/en-us/library/aa338206.aspx). При предыдущем методом успешно, этот интерфейс выполняет преобразование.</span><span class="sxs-lookup"><span data-stu-id="477c8-p103">The **IMsoDocExporter** interface is identical to the existing interface documented on MSDN. For more information, see [Extending the Office 2007 Fixed-Format Export Feature](http://msdn.microsoft.com/en-us/library/aa338206.aspx). When the previous method returns success, this interface performs the conversion.</span></span>
  
    
    
<span data-ttu-id="477c8-p104">За пределы требованиям, описанным в упомянутой выше статье разработчики экспорта в неизменяемом формате библиотеки DLL необходимо иметь представление вызова службы отмеченными **IMsoDocExporter** на другой поток, на котором служба вызывается **HrGetDocExporter**. Библиотеки DLL должен быть способен обрабатывать это без упаковки вызова потока, который называется **HrGetDocExporter**, так как служба не запускается обработки сообщений и упакованные вызова никогда не будет через (приведет к зависание и последующих сбоя).</span><span class="sxs-lookup"><span data-stu-id="477c8-p104">Beyond the requirements described in the aforementioned article, developers of fixed-format export DLLs must be aware that the service can call the provided **IMsoDocExporter** on a different thread from the one on which the service called **HrGetDocExporter**. The DLL must be able to handle this without marshalling the call back to the thread that called **HrGetDocExporter**, because the service does not run a message pump and the marshaled call will never get through (resulting in a hang and subsequent failure).</span></span>
  
    
    

## <a name="imsoserverfilemanagersite"></a><span data-ttu-id="477c8-131">IMsoServerFileManagerSite</span><span class="sxs-lookup"><span data-stu-id="477c8-131">IMsoServerFileManagerSite</span></span>

<span data-ttu-id="477c8-132">Интерфейс IMsoServerFileManagerSite определяется следующим образом.</span><span class="sxs-lookup"><span data-stu-id="477c8-132">The IMsoServerFileManagerSite interface is defined as follows.</span></span>
  
    
    

```

#undef  INTERFACE
#define INTERFACE  IMsoServerFileManagerSite
DECLARE_INTERFACE(IMsoServerFileManagerSite)
{
STDMETHOD_(BOOL, FGetHandle) (const WCHAR *pwzFileName, HANDLE *phFile, BOOL fRead, BOOL fWrite) PURE;
STDMETHOD_(BOOL, FCloseHandle) (HANDLE hFile) PURE;
};
```

<span data-ttu-id="477c8-133">Этот интерфейс предоставляет следующие методы.</span><span class="sxs-lookup"><span data-stu-id="477c8-133">This interface exposes the following methods.</span></span>
  
    
    

<span data-ttu-id="477c8-134">**В таблице 2. Методы, предоставляемые интерфейсом IMsoServerFileManagerSite**</span><span class="sxs-lookup"><span data-stu-id="477c8-134">**Table 2. Methods exposed by the IMsoServerFileManagerSite interface**</span></span>

|||
|:-----|:-----|
|<span data-ttu-id="477c8-135">Метод</span><span class="sxs-lookup"><span data-stu-id="477c8-135">Method</span></span>  <br/> |<span data-ttu-id="477c8-136">Описание</span><span class="sxs-lookup"><span data-stu-id="477c8-136">Description</span></span>  <br/> |
|<span data-ttu-id="477c8-137">**FGetHandle**</span><span class="sxs-lookup"><span data-stu-id="477c8-137">**FGetHandle**</span></span> <br/> |<span data-ttu-id="477c8-138">Получает дескриптор файла.</span><span class="sxs-lookup"><span data-stu-id="477c8-138">Gets a file handle.</span></span>  <br/> |
|<span data-ttu-id="477c8-139">**FCloseHandle**</span><span class="sxs-lookup"><span data-stu-id="477c8-139">**FCloseHandle**</span></span> <br/> |<span data-ttu-id="477c8-140">Освобождает дескриптор файла.</span><span class="sxs-lookup"><span data-stu-id="477c8-140">Releases a file handle.</span></span>  <br/> |
   
<span data-ttu-id="477c8-p105">Этот интерфейс не наследует от **IUnknown**. Соответственно экспорта в неизменяемом формате DLL-Библиотека может хранить ссылки на нее в течение времени его существования.</span><span class="sxs-lookup"><span data-stu-id="477c8-p105">This interface does not inherit from **IUnknown**. Accordingly, the fixed-format export DLL is allowed to keep a reference to it for its lifetime.</span></span>
  
    
    

### <a name="fgethandle"></a><span data-ttu-id="477c8-143">FGetHandle</span><span class="sxs-lookup"><span data-stu-id="477c8-143">FGetHandle</span></span>

<span data-ttu-id="477c8-p106">Фиксированного формата экспорта библиотеки DLL вызывает эту функцию для получения дескрипторов файла для записи. Он должен не пытайтесь открывать файлы каким-либо другим способом, так как служба выполняется в среде сильно ограниченных без доступа в большинстве ситуаций в файловой системе.</span><span class="sxs-lookup"><span data-stu-id="477c8-p106">The fixed-format export DLL calls this function to get file handles to write to. It must not try to open files through any other mechanism because the service runs in a highly restricted environment without access to most places in the file system.</span></span>
  
    
    

```

BOOL FGetHandle (
const WCHAR *pwzFile,
HANDLE *phFile,
BOOL fRead,
BOOL fWrite
)
```


<span data-ttu-id="477c8-146">**В таблице 3. Параметры FGetHandle**</span><span class="sxs-lookup"><span data-stu-id="477c8-146">**Table 3. FGetHandle parameters**</span></span>

|||
|:-----|:-----|
|<span data-ttu-id="477c8-147">Параметр</span><span class="sxs-lookup"><span data-stu-id="477c8-147">Parameter</span></span>  <br/> |<span data-ttu-id="477c8-148">Описание</span><span class="sxs-lookup"><span data-stu-id="477c8-148">Description</span></span>  <br/> |
|<span data-ttu-id="477c8-149">**pwzFile**</span><span class="sxs-lookup"><span data-stu-id="477c8-149">**pwzFile**</span></span> <br/> |<span data-ttu-id="477c8-p107">Указывает имя файла, фиксированного формата экспорта DLL пытается открыть. Это не должно быть полный путь к файлу, его необходимо указать только имя файла (например, Output.pdf).</span><span class="sxs-lookup"><span data-stu-id="477c8-p107">Specifies the name of the file the fixed-format export DLL wants to open. This must not be a full file path—it must specify only a file name (for example, Output.pdf).</span></span>  <br/> |
|<span data-ttu-id="477c8-152">**phFile**</span><span class="sxs-lookup"><span data-stu-id="477c8-152">**phFile**</span></span> <br/> |<span data-ttu-id="477c8-p108">Задает дескриптор в указанный файл, если файл открыт успешно. Экспорта в неизменяемом формате DLL можно использовать этот МАРКЕР в обычных операций до его закрывает путем вызова метода **FCloseHandle**.</span><span class="sxs-lookup"><span data-stu-id="477c8-p108">Specifies the handle to the specified file, if the file is opened successfully. The fixed-format export DLL can then use this HANDLE in normal file operations until it closes it by calling the **FCloseHandle** method. </span></span><br/> |
|<span data-ttu-id="477c8-155">**fRead**</span><span class="sxs-lookup"><span data-stu-id="477c8-155">**fRead**</span></span> <br/> |<span data-ttu-id="477c8-156">Указывает, будет ли файл открыт для чтения.</span><span class="sxs-lookup"><span data-stu-id="477c8-156">Specifies whether the file is to be opened with read access.</span></span>  <br/> |
|<span data-ttu-id="477c8-157">**fWrite**</span><span class="sxs-lookup"><span data-stu-id="477c8-157">**fWrite**</span></span> <br/> |<span data-ttu-id="477c8-p109">Указывает, является ли файл открыт для записи. Эта функция возвращает значение TRUE для обозначения успешности и FALSE при сбое.</span><span class="sxs-lookup"><span data-stu-id="477c8-p109">Specifies whether the file is to be opened with write access. This function returns TRUE to indicate success and FALSE to indicate failure.</span></span>  <br/> |
   

### <a name="fclosehandle"></a><span data-ttu-id="477c8-160">FCloseHandle</span><span class="sxs-lookup"><span data-stu-id="477c8-160">FCloseHandle</span></span>

<span data-ttu-id="477c8-161">Экспорта в неизменяемом формате DLL вызывает эту функцию, чтобы закрыть получить с помощью вызова метода **FGetHandle** дескрипторов файлов.</span><span class="sxs-lookup"><span data-stu-id="477c8-161">The fixed-format export DLL calls this function to close file handles obtained through calls to the **FGetHandle** method.</span></span>
  
    
    

```

BOOL FCloseHandle (
HANDLE phFile,
)
```

<span data-ttu-id="477c8-p110">Параметр  *phFile*  задает дескриптор файла закрывается. Если значение, возвращаемое этим методом равно 0, операция завершилась неудачно. Все остальные значения  обозначения успешности.</span><span class="sxs-lookup"><span data-stu-id="477c8-p110">The  *phFile*  parameter specifies the handle to the file to be closed. If the value returned by this method is 0, the operation failed. All other values indicate success.</span></span>
  
    
    

## <a name="pfnkeepalive"></a><span data-ttu-id="477c8-165">PFNKeepAlive</span><span class="sxs-lookup"><span data-stu-id="477c8-165">PFNKeepAlive</span></span>

<span data-ttu-id="477c8-166">После экспорта в неизменяемом формате DLL-Библиотека является активным, его необходимо вызвать функцию **проверки активности** через регулярные интервалы времени (настраивается администратором) для предотвращения службы, если предполагается, что экспорта в неизменяемом формате DLL не отвечать на запросы и таким образом завершение процесс.</span><span class="sxs-lookup"><span data-stu-id="477c8-166">When the fixed-format export DLL is active, it must call the **KeepAlive** function at regular intervals (configurable by the administrator) to prevent the service from assuming that the fixed-format export DLL is not responding, and thus terminating the process.</span></span>
  
    
    
 `typedef void (*PFNKeepAlive)(void)`
  
    
    

## <a name="see-also"></a><span data-ttu-id="477c8-167">См. также</span><span class="sxs-lookup"><span data-stu-id="477c8-167">See also</span></span>
<span data-ttu-id="477c8-168"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="477c8-168"><a name="bk_addresources"> </a></span></span>

<span data-ttu-id="477c8-169">Дополнительные сведения см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="477c8-169">For more information, see the following resources:</span></span>
  
    
    

-  [<span data-ttu-id="477c8-170">Расширение функции экспорта в неизменяемом формате Office 2007</span><span class="sxs-lookup"><span data-stu-id="477c8-170">Extending the Office 2007 Fixed-Format Export Feature</span></span>](http://msdn.microsoft.com/en-us/library/office/aa338206%28v=office.12%29.aspx)
    
  

