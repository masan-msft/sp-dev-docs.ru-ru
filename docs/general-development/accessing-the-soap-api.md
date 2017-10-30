---
title: "Доступ к API SOAP"
ms.date: 09/25/2017
keywords: soap
f1_keywords: soap
ms.prod: sharepoint
ms.assetid: 36e8e3d5-83ac-4bd3-b556-1af132add3eb
ms.openlocfilehash: 41b6656034d9e67fedca44684444bfb73d667e02
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="accessing-the-soap-api"></a>Доступ к API SOAP

Веб-службы Excel использует Simple Object Access Protocol (SOAP) по протоколу HTTP и действует как интерфейс связи между клиентских программ и Службы Excel. Веб-службы состоит из набора сложный тип объектов, которые можно использовать для доступа к всех функциональных возможностей Веб-службы Excel и методов. Для вызова службы, должен ссылаться Веб-службы Excel языка описания веб-служб (WSDL).
  
    
    


## <a name="referencing-the-wsdl"></a>Создание ссылок на WSDL

Для успешного вызова веб-службы, необходимо знать, как получить доступ к службе, какие операции службы поддерживает, какие параметры службы ожидает и возвращает какие службы. WSDL предоставляет эти сведения в XML-документ, чтение или обработки компьютером.
  
    
    
WSDL для конечной точки Веб-службы Excel доступен через  `ExcelServices.asmx?wsdl`. WSDL можно размещать на наборы средств разработки, которые поддерживают SOAP и веб-службы, такие как Microsoft .NET Framework SDK.
  
    
    
В следующем примере показано формат URL-адрес для WSDL-файла Веб-службы Excel:
  
    
    
 `http://<server>/<customsite>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
Если специализированный сайт отсутствует, можно использовать следующий URL-адрес временно:
  
    
    
 `http://<server>/_vti_bin/excelservice.asmx?WSDL`
  
    
    
Рекомендуется создать настраиваемые сайта и затем использовать URL-адрес, который содержит настраиваемого веб-сайта в формат URL-адреса.
  
    
    
В следующей таблице описываются каждый элемент в URL-адрес.
  
    
    


|**URL-адрес элемента**|**Description**|
|:-----|:-----|
| _server_ <br/> |Имя сервера, на котором развернут Microsoft SharePoint Server 2010.  <br/> |
| _customsite_ <br/> |Сайт настраиваемых SharePoint Server 2010, администратор сервера создает.  <br/> |
| _<endpointname>.asmx_ <br/> |Имя конечной точки веб-службы. Для Веб-службы Excel это  `ExcelService.asmx`.<br/> |
   
Дополнительные сведения о формате WSDL см WSDL веб Consortium (W3C) http://www.w3.org/TR/wsdl.
  
    
    

## <a name="see-also"></a>См. также


#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Шаг 1. Создание проекта клиента веб-службы](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Этап 2. Добавление веб-ссылки](step-2-adding-a-web-reference.md)
  
    
    
 [Этап 3. Получение доступа к веб-службе](step-3-accessing-the-web-service.md)
  
    
    
 [Этап 4. Построение и тестирование приложения](step-4-building-and-testing-the-application.md)
  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
