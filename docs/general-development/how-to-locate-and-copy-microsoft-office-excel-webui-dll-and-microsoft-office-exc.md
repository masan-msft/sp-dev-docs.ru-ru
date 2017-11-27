---
title: "Найдите и скопируйте Microsoft.Office.Excel.WebUI.dll и Microsoft.Office.Excel.WebUI.Internal.dll"
ms.date: 09/25/2017
keywords: how to,howdoi,howto,WebUI DLL
f1_keywords: how to,howdoi,howto,WebUI DLL
ms.prod: sharepoint
ms.assetid: 09ad5d5e-1678-45e4-8159-23ef56f84215
ms.openlocfilehash: 07089089b39fec2e6c7bd804f7188b5e0b666859
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="locate-and-copy-microsoftofficeexcelwebuidll-and-microsoftofficeexcelwebuiinternaldll"></a><span data-ttu-id="d84a9-103">Найдите и скопируйте Microsoft.Office.Excel.WebUI.dll и Microsoft.Office.Excel.WebUI.Internal.dll</span><span class="sxs-lookup"><span data-stu-id="d84a9-103">Locate and copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll</span></span>

<span data-ttu-id="d84a9-p101">If you want to programmatically add an Веб-клиент Excel Web Part to a SharePoint page and programmatically change the Веб-клиент Excel Web Part, you must add a reference to the required SharePoint DLLs. For example:</span><span class="sxs-lookup"><span data-stu-id="d84a9-p101">If you want to programmatically add an Excel Web Access Web Part to a SharePoint page and programmatically change the Excel Web Access Web Part, you must add a reference to the required SharePoint DLLs. For example:</span></span> 
  
    
    


- <span data-ttu-id="d84a9-106">Microsoft.Office.Excel.WebUI.dll</span><span class="sxs-lookup"><span data-stu-id="d84a9-106">Microsoft.Office.Excel.WebUI.dll</span></span>
    
  
- <span data-ttu-id="d84a9-107">Microsoft.Office.Excel.WebUI.Internal.dll</span><span class="sxs-lookup"><span data-stu-id="d84a9-107">Microsoft.Office.Excel.WebUI.Internal.dll</span></span>
    
  
- <span data-ttu-id="d84a9-108">Microsoft.SharePoint.dll</span><span class="sxs-lookup"><span data-stu-id="d84a9-108">Microsoft.SharePoint.dll</span></span>
    
  

<span data-ttu-id="d84a9-p102">On the computer running Microsoft SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll in the global assembly cache. Before you can add a reference to Microsoft.Office.Excel.WebUI.dll by using the **Add Reference** dialog box in Microsoft Visual Studio, you must first copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll from the global assembly cache to a folder. Then, you can use the **Browse** tab in the **Add Reference** dialog box to browse to the folder that contains the copy of Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll.</span><span class="sxs-lookup"><span data-stu-id="d84a9-p102">On the computer running Microsoft SharePoint Server 2010, you can find a copy of Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll in the global assembly cache. Before you can add a reference to Microsoft.Office.Excel.WebUI.dll by using the **Add Reference** dialog box in Microsoft Visual Studio, you must first copy Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll from the global assembly cache to a folder. Then, you can use the **Browse** tab in the **Add Reference** dialog box to browse to the folder that contains the copy of Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll.</span></span>
  
    
    

<span data-ttu-id="d84a9-112">The following steps show how to:</span><span class="sxs-lookup"><span data-stu-id="d84a9-112">The following steps show how to:</span></span> 
- <span data-ttu-id="d84a9-113">Locate Microsoft.Office.Excel.WebUI.dll.</span><span class="sxs-lookup"><span data-stu-id="d84a9-113">Locate Microsoft.Office.Excel.WebUI.dll.</span></span> 
    
  
- <span data-ttu-id="d84a9-114">Copy Microsoft.Office.Excel.WebUI.dll from the global assembly cache to a folder of your choice.</span><span class="sxs-lookup"><span data-stu-id="d84a9-114">Copy Microsoft.Office.Excel.WebUI.dll from the global assembly cache to a folder of your choice.</span></span>
    
  

> <span data-ttu-id="d84a9-115">**Примечание:** Повторите действия, чтобы скопировать в папку Microsoft.Office.Excel.WebUI.Internal.dll из глобального кэша сборок.</span><span class="sxs-lookup"><span data-stu-id="d84a9-115">**Note:** Repeat the steps to copy Microsoft.Office.Excel.WebUI.Internal.dll from the global assembly cache to a folder.</span></span> 
  
    
    


### <a name="to-locate-microsoftofficeexcelwebuidll"></a><span data-ttu-id="d84a9-116">To locate Microsoft.Office.Excel.WebUI.dll</span><span class="sxs-lookup"><span data-stu-id="d84a9-116">To locate Microsoft.Office.Excel.WebUI.dll</span></span>


1. <span data-ttu-id="d84a9-117">To start the command-prompt console, click **Start**, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="d84a9-117">To start the command-prompt console, click **Start**, and then click **Run**.</span></span> 
    
  
2. <span data-ttu-id="d84a9-118">In the **Open** field text box, typecmd.</span><span class="sxs-lookup"><span data-stu-id="d84a9-118">In the **Open** field text box, typecmd.</span></span> 
    
    <span data-ttu-id="d84a9-119">The command-prompt console appears.</span><span class="sxs-lookup"><span data-stu-id="d84a9-119">The command-prompt console appears.</span></span>
    
  
3. <span data-ttu-id="d84a9-120">Use the **cd** command to navigate to the "C:\\Windows\\assembly" directory:</span><span class="sxs-lookup"><span data-stu-id="d84a9-120">Use the **cd** command to navigate to the "C:\\Windows\\assembly" directory:</span></span>
    
    > <span data-ttu-id="d84a9-121">**Примечание:** Структура каталогов на вашем компьютере может немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="d84a9-121">**Note:** The directory structure on your computer might be slightly different.</span></span> <span data-ttu-id="d84a9-122">В этом примере используется компьютер с Windows Server 2008 установлены.</span><span class="sxs-lookup"><span data-stu-id="d84a9-122">This example uses a computer that has Windows Server 2008 installed.</span></span> 

```
  
cd C:\\Windows\\assembly
```

4. <span data-ttu-id="d84a9-123">Use the **dir** command to display the contents of the "C:\\Windows\\assembly" directory:</span><span class="sxs-lookup"><span data-stu-id="d84a9-123">Use the **dir** command to display the contents of the "C:\\Windows\\assembly" directory:</span></span>
    
```
  C:\\Windows\\assembly>dir
```


    You will see contents similar to the following:
    


```
  Volume in drive C has no label.
 
 Directory of C:\\Windows\\assembly

02/20/2010  09:22 AM    <DIR>          GAC
02/20/2010  09:39 AM    <DIR>          GAC_32
02/20/2010  09:32 AM    <DIR>          GAC_64
02/22/2010  05:05 PM    <DIR>          GAC_MSIL
02/22/2010  05:35 PM    <DIR>          NativeImages_v2.0.50727_32
02/22/2010  04:33 PM    <DIR>          NativeImages_v2.0.50727_64
02/20/2010  10:34 AM    <DIR>          NativeImages_v4.0.30219_32
02/20/2010  10:35 AM    <DIR>          NativeImages_v4.0.30219_64
02/22/2010  05:04 PM    <DIR>          temp
02/22/2010  05:05 PM    <DIR>          tmp
               0 File(s)              0 bytes
              10 Dir(s)  104,032,665,600 bytes free
```

5. <span data-ttu-id="d84a9-124">Use the **cd** command again to change the directory and navigate to the gac_msil directory:</span><span class="sxs-lookup"><span data-stu-id="d84a9-124">Use the **cd** command again to change the directory and navigate to the gac_msil directory:</span></span>
    
```
  
C:\\Windows\\assembly>cd gac_msil
```

6. <span data-ttu-id="d84a9-125">Use the **dir** command to display the content of the "C:\\Windows\\assembly\\GAC_MSIL" directory:</span><span class="sxs-lookup"><span data-stu-id="d84a9-125">Use the **dir** command to display the content of the "C:\\Windows\\assembly\\GAC_MSIL" directory:</span></span>
    
```
  C:\\Windows\\assembly\\GAC_MSIL>dir
```


    You will see contents similar to the following:
    


```
  Volume in drive C has no label.
Directory of C:\\Windows\\assembly\\GAC_MSIL
...
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.Udf
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.WebServices

02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI.Internal
...
02/20/2010  07:57 AM    <DIR>          Microsoft.SharePoint
...
0 File(s)              0 bytes
             739 Dir(s)  100,594,409,472 bytes free
```

7. <span data-ttu-id="d84a9-126">Now that you have located Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll, you can copy them to a folder of your choice.</span><span class="sxs-lookup"><span data-stu-id="d84a9-126">Now that you have located Microsoft.Office.Excel.WebUI.dll and Microsoft.Office.Excel.WebUI.Internal.dll, you can copy them to a folder of your choice.</span></span>
    
  

### <a name="to-copy-microsoftofficeexcelwebuidll"></a><span data-ttu-id="d84a9-127">To copy Microsoft.Office.Excel.WebUI.dll</span><span class="sxs-lookup"><span data-stu-id="d84a9-127">To copy Microsoft.Office.Excel.WebUI.dll</span></span>


1. <span data-ttu-id="d84a9-128">Use the **cd** command again to change the directory to "Microsoft.Office.Excel.WebUI":</span><span class="sxs-lookup"><span data-stu-id="d84a9-128">Use the **cd** command again to change the directory to "Microsoft.Office.Excel.WebUI":</span></span>
    
```
  
C:\\Windows\\assembly\\GAC_MSIL>cd Microsoft.Office.Excel.WebUI 
```

2. <span data-ttu-id="d84a9-129">Use the **dir** command to display the contents:</span><span class="sxs-lookup"><span data-stu-id="d84a9-129">Use the **dir** command to display the contents:</span></span>
    
```
  C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>dir
```


    You will see contents similar to the following:
    


```
  Volume in drive C has no label.
Directory of C:\\Windows\\assembly\\GAC_MSIL\Microsoft.Office.Excel.WebUI

02/20/2010  07:57 AM    <DIR>          .
02/20/2010  07:57 AM    <DIR>          ..
02/20/2010  07:57 AM    <DIR>          14.0.0.0__71e9bce111e9429c
               0 File(s)              0 bytes
               3 Dir(s)  104,006,115,328 bytes free
```

3. <span data-ttu-id="d84a9-130">Use the **cd** command again to change the directory:</span><span class="sxs-lookup"><span data-stu-id="d84a9-130">Use the **cd** command again to change the directory:</span></span>
    
```
  
C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>cd 14.0.0.0__71e9bce111e9429c
```

4. <span data-ttu-id="d84a9-131">Use the **copy** command to copy Microsoft.Office.Excel.WebUI.dll to a folder of your choice.</span><span class="sxs-lookup"><span data-stu-id="d84a9-131">Use the **copy** command to copy Microsoft.Office.Excel.WebUI.dll to a folder of your choice.</span></span>
    
    <span data-ttu-id="d84a9-132">In the following example, Microsoft.Office.Excel.WebUI.dll is copied to "C:\\WebUIAssembly", where "C:\\WebUIAssembly" is a folder that you created previously:</span><span class="sxs-lookup"><span data-stu-id="d84a9-132">In the following example, Microsoft.Office.Excel.WebUI.dll is copied to "C:\\WebUIAssembly", where "C:\\WebUIAssembly" is a folder that you created previously:</span></span>
    


```
  C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI\\14.0.0.0__71e9bce111e9429c>copy Microsoft.Office.Excel.WebUI.dll c:\\WebUIAssembly
        1 file(s) copied.
```


## <a name="example"></a><span data-ttu-id="d84a9-133">Пример</span><span class="sxs-lookup"><span data-stu-id="d84a9-133">Example</span></span>

<span data-ttu-id="d84a9-134">The following is an example of the result of using the command prompt to locate and copy Microsoft.Office.Excel.WebUI.dll to a folder.</span><span class="sxs-lookup"><span data-stu-id="d84a9-134">The following is an example of the result of using the command prompt to locate and copy Microsoft.Office.Excel.WebUI.dll to a folder.</span></span>
  
    
    

```

C:\\Windows\\assembly>dir
Volume in drive C has no label.
Directory of C:\\Windows\\assembly

02/20/2010  09:22 AM    <DIR>          GAC
02/20/2010  09:39 AM    <DIR>          GAC_32
02/20/2010  09:32 AM    <DIR>          GAC_64
02/22/2010  05:05 PM    <DIR>          GAC_MSIL
02/22/2010  05:35 PM    <DIR>          NativeImages_v2.0.50727_32
02/22/2010  04:33 PM    <DIR>          NativeImages_v2.0.50727_64
02/20/2010  10:34 AM    <DIR>          NativeImages_v4.0.30219_32
02/20/2010  10:35 AM    <DIR>          NativeImages_v4.0.30219_64
02/22/2010  05:04 PM    <DIR>          temp
02/22/2010  05:05 PM    <DIR>          tmp
               0 File(s)              0 bytes
              10 Dir(s)  104,032,665,600 bytes free
C:\\Windows\\assembly>cd gac_msil

C:\\Windows\\assembly\\GAC_MSIL>dir
 Volume in drive C has no label.
 Directory of C:\\Windows\\assembly\GAC_MSIL
...
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.Udf
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.Server.WebServices

02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI
02/20/2010  07:57 AM    <DIR>          Microsoft.Office.Excel.WebUI.Internal
...

C:\\Windows\\assembly\\GAC_MSIL>cd Microsoft.Office.Excel.WebUI

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>dir
 Volume in drive C has no label.
Directory of C:\\Windows\\assembly\\GAC_MSIL\Microsoft.Office.Excel.WebUI

02/20/2010  07:57 AM    <DIR>          .
02/20/2010  07:57 AM    <DIR>          ..
02/20/2010  07:57 AM    <DIR>          14.0.0.0__71e9bce111e9429c
               0 File(s)              0 bytes
               3 Dir(s)  104,006,115,328 bytes free

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI>cd 14.0.0.0__71e9bce111e9429c

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI\\14.0.0.0__71e9bce111e9429c>copy Microsoft.Office.Excel.WebUI.dll c:\\WebUIAssembly
        1 file(s) copied.

C:\\Windows\\assembly\\GAC_MSIL\\Microsoft.Office.Excel.WebUI\\14.0.0.0__71e9bce111e9429c>
```


## <a name="see-also"></a><span data-ttu-id="d84a9-135">См. также</span><span class="sxs-lookup"><span data-stu-id="d84a9-135">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="d84a9-136">Задачи</span><span class="sxs-lookup"><span data-stu-id="d84a9-136">Tasks</span></span>


  
    
    
 [<span data-ttu-id="d84a9-137">How to: Programmatically Add an Excel Web Access Web Part to a Page</span><span class="sxs-lookup"><span data-stu-id="d84a9-137">How to: Programmatically Add an Excel Web Access Web Part to a Page</span></span>](how-to-programmatically-add-an-excel-web-access-web-part-to-a-page.md)
  
    
    
 [<span data-ttu-id="d84a9-138">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="d84a9-138">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
#### <a name="concepts"></a><span data-ttu-id="d84a9-139">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="d84a9-139">Concepts</span></span>


  
    
    
 [<span data-ttu-id="d84a9-140">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="d84a9-140">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="d84a9-141">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="d84a9-141">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
