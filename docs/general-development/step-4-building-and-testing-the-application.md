---
title: "Этап 4. Построение и тестирование приложения"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f2feeecb-1b4c-4049-be4e-11d414f13d9f
ms.openlocfilehash: 344c1fff77662184f13d9f4397b1c7e1f6b065e1
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-4-building-and-testing-the-application"></a>Этап 4. Построение и тестирование приложения

На этом этапе выполняется построение и тестирование приложения. Visual Studio обеспечивает различные способы создания и запуска консольного приложения из интегрированной среды разработки, например команды:
  
    
    


- Запуск без отладки ( **CTRL + F5**),
    
  
- Запуск ( **F5**).
    
  

## <a name="build-run-and-debug-the-application"></a>Построение, запуск и отладка приложения


### <a name="to-build-and-run-the-application"></a>Построение и запуск приложения


1. В меню **Отладка** выберите пункт **Запуск без отладки** или нажмите клавиши **CTRL + F5**. Эта команда позволяет сохранить окно консоли открытым после завершения выполнения программы. 
    
  
2. В консоли приложение выведет следующие данные:
    
    > **Примечание:** Эти значения зависят от значения, которые имеют в книге, идентификатор сеанса и т. д. 

```
  
The Credential is: System.Net.SystemNetworkCredential
Total rows in range: 18
Value in range is: 4245.955129
```

3. Нажмите любую клавишу, чтобы закрыть программу SampleApplication.exe.
    
  

### <a name="file-not-found-exception"></a>Исключение "Файл не найден"


1. Если предоставлен неверный путь к книге, будет выдано исключение "Файл не найден", перехватываемое следующим кодом:
    
```cs
  
catch (SoapException e)
{
    Console.WriteLine("SOAP Exception Message: {0}", e.Message);
}
```


```VB.net
  
Catch e As SoapException
Console.WriteLine("SOAP Exception Message: {0}", e.Message)
End Try
```

2. В консоли приложение выведет следующие данные об исключении SOAP:
    
```
  
SOAP Exception Message: The file you selected could not be found. Check the spelling of the file name and verify that the location is correct.

```


### <a name="index-out-of-range-exception"></a>Исключение "Индекс вне диапазона"


1. При попытке получить значение, которое находится за пределами диапазона, будет выдано исключение **System.IndexOutOfRangeException**. В консоли приложение выведет следующие данные:
    
```
  
The Credential is: System.Net.SystemNetworkCredential
The sessionID is : 64.28e58e90-b757-4658-b1c4-890ad68ef6cbRmqR4IINXfkMeOJRG8Iq0Y
27tVk=110.33d3R6fqv7tr2jPyYiPwRu|!@en-US|en-US|+0480#0000-10-00-05T02:00:00:0000
#+0000#0000-04-00-01T02:00:00:0000#-0060
Total rows in range: 18
```

2. Затем будет выведено следующее необработанное исключение:
    
```
  
An unhandled exception of type 'System.IndexOutOfRangeException' occurred in SampleApplication.exe
Additional information: Index was outside the bounds of the array.
```

3. Обработать это необработанное исключение можно путем добавления еще одного блока **catch** для перехвата исключения, следующего за блоком **catch** исключения SOAP, как показано ниже:
    
```cs
  
catch (Exception e)
{
    Console.WriteLine("Exception Message: {0}", e.Message);
}
```


```VB.net
  
Catch e As Exception
Console.WriteLine("Exception Message: {0}", e.Message)
End Try
```


### <a name="to-run-the-application-using-f5"></a>Запуск приложения с помощью клавиши F5


1. Запустить приложение можно, выбрав в меню **Отладка** пункт **Запуск** или нажав клавишу **F5**. Чтобы окно консоли оставалось открытым после завершения выполнения программы, можно добавить следующую строку в конец кода (после блока **catch**):
    
```cs
  
Console.ReadLine();
```


```VB.net
  Console.ReadLine()
```

2. Нажмите любую клавишу, чтобы закрыть программу SampleApplication.exe.
    
  

## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Основные понятия


  
    
    
 [Доступ к API SOAP](accessing-the-soap-api.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Шаг 1. Создание проекта клиента веб-службы](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Этап 2. Добавление веб-ссылки](step-2-adding-a-web-reference.md)
  
    
    
 [Этап 3. Получение доступа к веб-службе](step-3-accessing-the-web-service.md)
  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
  
    
    
 [How to: Trust Workbook Locations Using Script](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)
