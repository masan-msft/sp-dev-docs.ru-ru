---
title: Step 2 Creating a Managed-Code UDF
ms.date: 09/25/2017
keywords: soap
f1_keywords: soap
ms.prod: sharepoint
ms.assetid: 3c9edf82-ee2d-41f0-9d66-e88e8dc0cc69
ms.openlocfilehash: f763b1599a2fcbb1c8d70998ad02b707c79769d5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-2-creating-a-managed-code-udf"></a>Step 2: Creating a Managed-Code UDF

After you have added a reference to Microsoft.Office.Excel.Server.Udf.dll to your project, the next step is to create some custom functions and mark them with the Службы Excel user-defined function (UDF) attributes. 
  
    
    

You must mark your UDF class with the **Microsoft.Office.Excel.Server.Udf.UdfClass** attribute, and mark the UDF methods with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute. Any methods that are not marked with the **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute in the UDF assembly will be ignored, because they will not be considered UDF methods.
  
    
    

The **Microsoft.Office.Excel.Server.Udf.UdfMethod** attribute has an **IsVolatile** property. You use the **IsVolatile** property to specify a UDF method as volatile or nonvolatile. The **IsVolatile** property takes a Boolean value. The default value is **false**, which means that particular UDF method is nonvolatile. 
## <a name="creating-udfs"></a>Creating UDFs


### <a name="to-add-directives"></a>To add directives


- Типы для использования определены в пространстве имен **Microsoft.Office.Excel.Server.Udf** . Добавление **с помощью** (или **Imports**) директиву в верхней части файла Class1.cs можно использовать типы в **Microsoft.Office.Excel.Server.Udf** без необходимости полностью определить типы в пространстве имен.
    
    To add this directive, add the following code to the beginning of your code in the Class1.cs file, after  `using System.Text:`
    


```cs
  
using Microsoft.Office.Excel.Server.Udf; 
```




```VB.net
  Imports Microsoft.Office.Excel.Server.Udf
```


### <a name="to-mark-a-udf-class-and-methods"></a>To mark a UDF class and methods


1. Mark  `Class1` as a UDF class by adding the following attribute just above `public class Class1`: 
    
```cs
  [UdfClass]
```


```VB.net
  <UdfClass>_
```

2. Create a function that takes a number (of type **double**), and in the function, multiply the number by 9. The function is a UDF method that is nonvolatile. Add the following code to  `Class1`:
    
```cs
  [UdfMethod]
public double MyDouble(double d)
{
    return d * 9;
}
```


```VB.net
  
<UdfMethod> _
Public Function MyDouble(ByVal d As Double) As Double
    Return d * 9
End Function
```


    > **Note:**
      > The default value for the **IsVolatile** property is **false**, which means that particular UDF method is nonvolatile. Therefore, it is sufficient to mark a nonvolatile UDF method as  `[UdfMethod]`. It is not necessary to mark it as  `[UdfMethod(IsVolatile = false)]`. 
3. Create another function that returns the current date using the **System.DateTime.Today** property. The function is a UDF method that is volatile. Add the following code to `Class1`:
    
```cs
  
[UdfMethod(IsVolatile = true)]
public DateTime ReturnDateTimeToday()
{
    return (DateTime.Today);
}      
```


```VB.net
  
<UdfMethod(IsVolatile := True)> _
Public Function ReturnDateTimeToday() As Date
    Return (Date.Today)
End Function
```


### <a name="to-build-the-project"></a>To build the project


1. On the **Build** menu, click **Build Solution**.
    
  
2. You should find SampleUdf.dll assembly in the directory where you have saved your project. 
    
  

### <a name="complete-code"></a>Complete Code

The following code sample is the complete code in the Class1.cs example file described in the previous procedures.
  
    
    

```cs

using System;
using System.Collections.Generic;
using System.Text;
using Microsoft.Office.Excel.Server.Udf;

namespace SampleUdf
{
    [UdfClass]
    public class Class1
    {
        [UdfMethod]
        public double MyDouble(double d)
        {
            return d * 9;
        }  

        [UdfMethod(IsVolatile = true)]
        public DateTime ReturnDateTimeToday()
        {
            return (DateTime.Today);
        }
    }
}
```


```VB.net

Imports System
Imports System.Collections.Generic
Imports System.Text
Imports Microsoft.Office.Excel.Server.Udf

Namespace SampleUdf
    <UdfClass> _
    Public Class Class1
        <UdfMethod> _
        Public Function MyDouble(ByVal d As Double) As Double
            Return d * 9
        End Function

        <UdfMethod(IsVolatile := True)> _
        Public Function ReturnDateTimeToday() As Date
            Return (Date.Today)
        End Function
    End Class
End Namespace
```


## <a name="see-also"></a>См. также


#### <a name="tasks"></a>Задачи


  
    
    
 [Step 1: Creating a Project and Adding a UDF Reference](step-1-creating-a-project-and-adding-a-udf-reference.md)
  
    
    
 [Step 3: Deploying and Enabling UDFs](step-3-deploying-and-enabling-udfs.md)
  
    
    
 [Step 4: Testing and Calling UDFs from Cells](step-4-testing-and-calling-udfs-from-cells.md)
  
    
    
 [How to: Create a UDF That Calls a Web Service](how-to-create-a-udf-that-calls-a-web-service.md)
#### <a name="concepts"></a>Основные понятия


  
    
    
 [Walkthrough: Developing a Managed-Code UDF](walkthrough-developing-a-managed-code-udf.md)
  
    
    
 [Understanding Excel Services UDFs](understanding-excel-services-udfs.md)
