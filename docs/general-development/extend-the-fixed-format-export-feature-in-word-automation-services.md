---
title: "Расширение функции экспорта в неизменяемом формате в службы Word Automation Services"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d8375505-432e-438e-971b-221a1d9bb601
ms.openlocfilehash: de50843d70b07089a27ac8601fc76377717fd135
ms.sourcegitcommit: 61f26b4fe41d3cd80622d9950d8f6599df48f26f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2017
---
# <a name="extend-the-fixed-format-export-feature-in-word-automation-services"></a>Расширение функции экспорта в неизменяемом формате в службы Word Automation Services
Расширение Word Automation Services в Microsoft Office 2013 для замены библиотеки, используемой функции экспорта в неизменяемом формате.
## <a name="introduction-to-the-word-file-conversion-service-fixed-format-export-feature"></a>Общие сведения о Word conversion службы фиксированной форматов файлов экспорта компонента

В этой статье описывается расширение функции экспорта в неизменяемом формате Word Automation Services для использования различных экспорта в неизменяемом формате библиотеки DLL, сторонние разработчики могут заменить те, предоставляемым корпорацией Майкрософт. Этот механизм требует и расширяет интерфейс COM расширяемость фиксированного формата в клиенте Office. Для получения дополнительных сведений см  [расширение функции экспорта фиксированный формат Office 2007](http://msdn.microsoft.com/en-us/library/aa338206.aspx).
  
    
    

## <a name="discovery"></a>Обнаружение

Word Automation Services позволяет сторонних разработчиков заменить выходные данные фиксированного формата поддерживается:
  
    
    

- PDF
    
  
- XPS
    
  
Чтобы заменить каждого формата, библиотеки DLL должны быть расположены в одном каталоге с основной библиотеки (Sword.dll) для службы Word Automation Services (путь установки: \< \<Установка корневой\>\>\\веб-службы\\ConversionService\\ Ячейка\\конвертера\\) и должен иметь имя файла, указанного в таблице 1.
  
    
    

**В таблице 1. Имена файлов для фиксированного формата экспорта библиотеки DLL**


|**Формат**|**Имя файла**|
|:-----|:-----|
|PDF  <br/> |Renderpdf.dll  <br/> |
|XPS  <br/> |Renderxps.dll  <br/> |
   

## <a name="initialization"></a>Инициализация

Библиотеки DLL необходимо экспортировать в метод с указанной ниже сигнатурой.
  
    
    

```

HRESULT HrGetDocExporter (
IMsoDocExporter **ppimde,
IMsoServerFileManagerSite *psfms,
PFNKeepAlive pfnKeepAlive
)
```

Функции требуется DLL двух интерфейсов и указатель метода, описанных в следующем разделе.
  
    
    
Если функция возвращает сбоя службы не вернуться к экспорта предоставленные корпорацией Майкрософт. Вместо этого службы сообщает преобразования как ошибочный.
  
    
    

## <a name="imsodocexporter"></a>IMsoDocExporter

Интерфейс **IMsoDocExporter** идентична существующего интерфейса, задокументированные в MSDN. Для получения дополнительных сведений см [расширение функции экспорта фиксированный формат Office 2007](http://msdn.microsoft.com/en-us/library/aa338206.aspx). При предыдущем методом успешно, этот интерфейс выполняет преобразование.
  
    
    
За пределы требованиям, описанным в упомянутой выше статье разработчики экспорта в неизменяемом формате библиотеки DLL необходимо иметь представление вызова службы отмеченными **IMsoDocExporter** на другой поток, на котором служба вызывается **HrGetDocExporter**. Библиотеки DLL должен быть способен обрабатывать это без упаковки вызова потока, который называется **HrGetDocExporter**, так как служба не запускается обработки сообщений и упакованные вызова никогда не будет через (приведет к зависание и последующих сбоя).
  
    
    

## <a name="imsoserverfilemanagersite"></a>IMsoServerFileManagerSite

Интерфейс IMsoServerFileManagerSite определяется следующим образом.
  
    
    

```

#undef  INTERFACE
#define INTERFACE  IMsoServerFileManagerSite
DECLARE_INTERFACE(IMsoServerFileManagerSite)
{
STDMETHOD_(BOOL, FGetHandle) (const WCHAR *pwzFileName, HANDLE *phFile, BOOL fRead, BOOL fWrite) PURE;
STDMETHOD_(BOOL, FCloseHandle) (HANDLE hFile) PURE;
};
```

Этот интерфейс предоставляет следующие методы.
  
    
    

**В таблице 2. Методы, предоставляемые интерфейсом IMsoServerFileManagerSite**

|||
|:-----|:-----|
|Метод  <br/> |Описание  <br/> |
|**FGetHandle** <br/> |Получает дескриптор файла.  <br/> |
|**FCloseHandle** <br/> |Освобождает дескриптор файла.  <br/> |
   
Этот интерфейс не наследует от **IUnknown**. Соответственно экспорта в неизменяемом формате DLL-Библиотека может хранить ссылки на нее в течение времени его существования.
  
    
    

### <a name="fgethandle"></a>FGetHandle

Фиксированного формата экспорта библиотеки DLL вызывает эту функцию для получения дескрипторов файла для записи. Он должен не пытайтесь открывать файлы каким-либо другим способом, так как служба выполняется в среде сильно ограниченных без доступа в большинстве ситуаций в файловой системе.
  
    
    

```

BOOL FGetHandle (
const WCHAR *pwzFile,
HANDLE *phFile,
BOOL fRead,
BOOL fWrite
)
```


**В таблице 3. Параметры FGetHandle**

|||
|:-----|:-----|
|Параметр  <br/> |Описание  <br/> |
|**pwzFile** <br/> |Указывает имя файла, фиксированного формата экспорта DLL пытается открыть. Это не должно быть полный путь к файлу, его необходимо указать только имя файла (например, Output.pdf).  <br/> |
|**phFile** <br/> |Задает дескриптор в указанный файл, если файл открыт успешно. Экспорта в неизменяемом формате DLL можно использовать этот МАРКЕР в обычных операций до его закрывает путем вызова метода **FCloseHandle**.<br/> |
|**fRead** <br/> |Указывает, будет ли файл открыт для чтения.  <br/> |
|**fWrite** <br/> |Указывает, является ли файл открыт для записи. Эта функция возвращает значение TRUE для обозначения успешности и FALSE при сбое.  <br/> |
   

### <a name="fclosehandle"></a>FCloseHandle

Экспорта в неизменяемом формате DLL вызывает эту функцию, чтобы закрыть получить с помощью вызова метода **FGetHandle** дескрипторов файлов.
  
    
    

```

BOOL FCloseHandle (
HANDLE phFile,
)
```

Параметр  *phFile*  задает дескриптор файла закрывается. Если значение, возвращаемое этим методом равно 0, операция завершилась неудачно. Все остальные значения  обозначения успешности.
  
    
    

## <a name="pfnkeepalive"></a>PFNKeepAlive

После экспорта в неизменяемом формате DLL-Библиотека является активным, его необходимо вызвать функцию **проверки активности** через регулярные интервалы времени (настраивается администратором) для предотвращения службы, если предполагается, что экспорта в неизменяемом формате DLL не отвечать на запросы и таким образом завершение процесс.
  
    
    
 `typedef void (*PFNKeepAlive)(void)`
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

Дополнительные сведения см. в следующих документах:
  
    
    

-  [Расширение функции экспорта в неизменяемом формате Office 2007](http://msdn.microsoft.com/en-us/library/office/aa338206%28v=office.12%29.aspx)
    
  
