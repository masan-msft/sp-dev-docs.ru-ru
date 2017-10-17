---
title: "Шаг 2 Добавление редактор содержимого и Excel Services веб-частей"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c9c66843-fd77-4a0d-a512-d936d15d4429
ms.openlocfilehash: cad2e53b4a7284fc0a5de7205635e26b01c0bcd3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-2-adding-the-content-editor-and-excel-services-web-parts"></a><span data-ttu-id="5616c-102">Шаг 2: Добавление редактор содержимого и Excel Services веб-частей</span><span class="sxs-lookup"><span data-stu-id="5616c-102">Step 2: Adding the Content Editor and Excel Services Web Parts</span></span>

<span data-ttu-id="5616c-103">После создания текстового файла в ECMAScript (JavaScript, JScript) и сохраните текстовый файл в надежном расположении следующим шагом является создание страницы веб-частей и добавьте веб-часть редактора содержимого и Службы Excel веб-части на страницу.</span><span class="sxs-lookup"><span data-stu-id="5616c-103">After you create an ECMAScript (JavaScript, JScript) text file and save the text file in a trusted location, the next step is to create a Web Parts Page and add the Content Editor Web Part and the Excel Services Web Part to the page.</span></span> 
  
    
    

<span data-ttu-id="5616c-104">Затем откройте книгу с помощью Службы Excel веб-части, который добавлен на страницу.</span><span class="sxs-lookup"><span data-stu-id="5616c-104">Next, display a workbook by using the Excel Services Web Part that you added to the page.</span></span> 
### <a name="to-add-the-content-editor-web-part-and-the-excel-services-web-part"></a><span data-ttu-id="5616c-105">Чтобы добавить веб-часть редактора содержимого и веб-части служб Excel</span><span class="sxs-lookup"><span data-stu-id="5616c-105">To add the Content Editor Web Part and the Excel Services Web Part</span></span>


1. <span data-ttu-id="5616c-106">Создание новой страницы веб-частей.</span><span class="sxs-lookup"><span data-stu-id="5616c-106">Create a new Web Parts Page.</span></span> 
    
  
2. <span data-ttu-id="5616c-107">Добавление веб-части редактора контента на страницу веб-частей, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="5616c-107">Add a Content Editor Web Part to the Web Parts Page that you just created.</span></span>
    
  
3. <span data-ttu-id="5616c-p101">Веб-канал URL-адрес для текстовый файл, созданный в  [Этап 1: Создание ECMAScript текстового файла](step-1-creating-a-ecmascript-text-file.md) в веб-часть редактора содержимого. Это делается путем добавления URL-адрес для текстового файла, который загрузил библиотеку надежных документов в [Этап 1: Создание ECMAScript текстового файла](step-1-creating-a-ecmascript-text-file.md).</span><span class="sxs-lookup"><span data-stu-id="5616c-p101">Feed the URL for the text file that you created in  [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file.md) to the Content Editor Web Part. You do this by adding the URL for the text file that you uploaded to a trusted document library in [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file.md).</span></span> 
    
    <span data-ttu-id="5616c-110">Например:</span><span class="sxs-lookup"><span data-stu-id="5616c-110">For example:</span></span> 
    
     <span data-ttu-id="5616c-111">`http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span><span class="sxs-lookup"><span data-stu-id="5616c-111">`http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span></span>
    
  
4. <span data-ttu-id="5616c-112">Добавьте Службы Excel веб-части на страницу.</span><span class="sxs-lookup"><span data-stu-id="5616c-112">Add an Excel Services Web Part to the page.</span></span>
    
  

### <a name="to-run-the-ecmascript-sample"></a><span data-ttu-id="5616c-113">Чтобы запустить образец ECMAScript</span><span class="sxs-lookup"><span data-stu-id="5616c-113">To run the ECMAScript sample</span></span>


1. <span data-ttu-id="5616c-p102">Отправка книги в библиотеке надежным документом. Использование меню **Изменить общую веб-часть** для отображения области задач Службы Excel веб-части. В разделе **Отображение книги** в поле **книги** введите URL-адрес, который будет Службы Excel веб-части для загрузки и отображения книги. Например:</span><span class="sxs-lookup"><span data-stu-id="5616c-p102">Upload a workbook to a trusted document library. Use the **Modify Shared Web Part** menu to display the Excel Services Web Part task pane. In the **Workbook Display** section, in the **Workbook** field, type the URL to the workbook that you want the Excel Services Web Part to load and display. For example:</span></span>
    
     <span data-ttu-id="5616c-118">`http://` _myserver_ `/Docs/Documents/WorkbookToDisplay.xlsx`</span><span class="sxs-lookup"><span data-stu-id="5616c-118">`http://` _myserver_ `/Docs/Documents/WorkbookToDisplay.xlsx`</span></span>
    
  
2. <span data-ttu-id="5616c-119">Щелкните различные ячейки и выводятся в редактор контента **div**установлено значение ячейки.</span><span class="sxs-lookup"><span data-stu-id="5616c-119">Try clicking different cells and observe the cell value populated in the Content Editor **div**.</span></span> 
    
  

