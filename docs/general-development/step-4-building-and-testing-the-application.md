---
title: "Этап 4. Построение и тестирование приложения"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f2feeecb-1b4c-4049-be4e-11d414f13d9f
ms.openlocfilehash: fd80f3fabb19e74e04afb60b544c81785e7af19f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="step-4-building-and-testing-the-application"></a><span data-ttu-id="bc381-102">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="bc381-102">Step 4: Building and Testing the Application</span></span>

<span data-ttu-id="bc381-p101">На этом этапе выполняется построение и тестирование приложения. Visual Studio обеспечивает различные способы создания и запуска консольного приложения из интегрированной среды разработки, например команды:</span><span class="sxs-lookup"><span data-stu-id="bc381-p101">In this step, you will build and test your application. Visual Studio offers several methods to build and run a console application from the IDE, such as:</span></span>
  
    
    


- <span data-ttu-id="bc381-105">Запуск без отладки ( **CTRL + F5**),</span><span class="sxs-lookup"><span data-stu-id="bc381-105">Start Without Debugging ( **CTRL + F5**)</span></span>
    
  
- <span data-ttu-id="bc381-106">Запуск ( **F5**).</span><span class="sxs-lookup"><span data-stu-id="bc381-106">Start ( **F5**)</span></span>
    
  

## <a name="build-run-and-debug-the-application"></a><span data-ttu-id="bc381-107">Построение, запуск и отладка приложения</span><span class="sxs-lookup"><span data-stu-id="bc381-107">Build, Run, and Debug the Application</span></span>


### <a name="to-build-and-run-the-application"></a><span data-ttu-id="bc381-108">Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="bc381-108">To build and run the application</span></span>


1. <span data-ttu-id="bc381-p102">В меню **Отладка** выберите пункт **Запуск без отладки** или нажмите клавиши **CTRL + F5**. Эта команда позволяет сохранить окно консоли открытым после завершения выполнения программы.</span><span class="sxs-lookup"><span data-stu-id="bc381-p102">On the **Debug** menu, click **Start Without Debugging** or press **CTRL + F5**. This ensures that the console window remains open after the program has finished executing.</span></span> 
    
  
2. <span data-ttu-id="bc381-111">В консоли приложение выведет следующие данные:</span><span class="sxs-lookup"><span data-stu-id="bc381-111">The application prints the following output to the console.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="bc381-112">[!Примечание] Эти значения могут различаться в зависимости от значений в книге, кода сеанса и т. д.</span><span class="sxs-lookup"><span data-stu-id="bc381-112">These values vary depending on the values you have in your workbook, session ID, and so on.</span></span> 

    ```
    The Credential is: System.Net.SystemNetworkCredential
    Total rows in range: 18
    Value in range is: 4245.955129
    ```

3. <span data-ttu-id="bc381-113">Нажмите любую клавишу, чтобы закрыть программу SampleApplication.exe.</span><span class="sxs-lookup"><span data-stu-id="bc381-113">Press any key to close SampleApplication.exe.</span></span>
    
### <a name="file-not-found-exception"></a><span data-ttu-id="bc381-114">Исключение "Файл не найден"</span><span class="sxs-lookup"><span data-stu-id="bc381-114">File Not Found Exception</span></span>


1. <span data-ttu-id="bc381-115">Если предоставлен неверный путь к книге, будет выдано исключение "Файл не найден", перехватываемое следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="bc381-115">If the path to the workbook you provided is wrong, you will get a "file not found" exception, which is caught by the following code:</span></span>
    
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

2. <span data-ttu-id="bc381-116">В консоли приложение выведет следующие данные об исключении SOAP:</span><span class="sxs-lookup"><span data-stu-id="bc381-116">The application prints the following SOAP exception output to the console:</span></span>
    
```
  
SOAP Exception Message: The file you selected could not be found. Check the spelling of the file name and verify that the location is correct.

```


### <a name="index-out-of-range-exception"></a><span data-ttu-id="bc381-117">Исключение "Индекс вне диапазона"</span><span class="sxs-lookup"><span data-stu-id="bc381-117">Index Out Of Range Exception</span></span>


1. <span data-ttu-id="bc381-p103">При попытке получить значение, которое находится за пределами диапазона, будет выдано исключение **System.IndexOutOfRangeException**. В консоли приложение выведет следующие данные:</span><span class="sxs-lookup"><span data-stu-id="bc381-p103">If you try to get a value from outside the range, you will get a **System.IndexOutOfRangeException** exception. The application prints the following output to the console:</span></span>
    
```
  
The Credential is: System.Net.SystemNetworkCredential
The sessionID is : 64.28e58e90-b757-4658-b1c4-890ad68ef6cbRmqR4IINXfkMeOJRG8Iq0Y
27tVk=110.33d3R6fqv7tr2jPyYiPwRu|!@en-US|en-US|+0480#0000-10-00-05T02:00:00:0000
#+0000#0000-04-00-01T02:00:00:0000#-0060
Total rows in range: 18
```

2. <span data-ttu-id="bc381-120">Затем будет выведено следующее необработанное исключение:</span><span class="sxs-lookup"><span data-stu-id="bc381-120">Then you will get an unhandled exception that says:</span></span>
    
```
  
An unhandled exception of type 'System.IndexOutOfRangeException' occurred in SampleApplication.exe
Additional information: Index was outside the bounds of the array.
```

3. <span data-ttu-id="bc381-121">Обработать это необработанное исключение можно путем добавления еще одного блока **catch** для перехвата исключения, следующего за блоком **catch** исключения SOAP, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="bc381-121">You can handle the above unhandled exception by adding another **catch** block to catch the exception after the SOAP exception **catch** block as shown here:</span></span>
    
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


### <a name="to-run-the-application-using-f5"></a><span data-ttu-id="bc381-122">Запуск приложения с помощью клавиши F5</span><span class="sxs-lookup"><span data-stu-id="bc381-122">To run the application using F5</span></span>


1. <span data-ttu-id="bc381-p104">Запустить приложение можно, выбрав в меню **Отладка** пункт **Запуск** или нажав клавишу **F5**. Чтобы окно консоли оставалось открытым после завершения выполнения программы, можно добавить следующую строку в конец кода (после блока **catch**):</span><span class="sxs-lookup"><span data-stu-id="bc381-p104">You can run your application by clicking **Start** on the **Debug** menu, or by pressing **F5**. To ensure that the console window remains open after the program has finished executing, you could add the following line of code at the end of your code (after the **catch** block):</span></span>
    
```cs
  
Console.ReadLine();
```


```VB.net
  Console.ReadLine()
```

2. <span data-ttu-id="bc381-125">Нажмите любую клавишу, чтобы закрыть программу SampleApplication.exe.</span><span class="sxs-lookup"><span data-stu-id="bc381-125">Press any key to close SampleApplication.exe.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="bc381-126">См. также</span><span class="sxs-lookup"><span data-stu-id="bc381-126">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="bc381-127">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="bc381-127">Concepts</span></span>


  
    
    
 [<span data-ttu-id="bc381-128">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="bc381-128">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
#### <a name="other-resources"></a><span data-ttu-id="bc381-129">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="bc381-129">Other resources</span></span>


  
    
    
 [<span data-ttu-id="bc381-130">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="bc381-130">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="bc381-131">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="bc381-131">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="bc381-132">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="bc381-132">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="bc381-133">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="bc381-133">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
  
    
    
 [<span data-ttu-id="bc381-134">How to: Trust Workbook Locations Using Script</span><span class="sxs-lookup"><span data-stu-id="bc381-134">How to: Trust Workbook Locations Using Script</span></span>](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)
