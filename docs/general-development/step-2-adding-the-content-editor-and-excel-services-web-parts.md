---
title: "Шаг 2 Добавление редактор содержимого и Excel Services веб-частей"
ms.prod: OFFICE365
ms.assetid: c9c66843-fd77-4a0d-a512-d936d15d4429
ms.openlocfilehash: 7ac9f535ad153693214a84ace404f26a631dbac5
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2017
---
# <a name="step-2-adding-the-content-editor-and-excel-services-web-parts"></a>Шаг 2: Добавление редактор содержимого и Excel Services веб-частей

После создания текстового файла в ECMAScript (JavaScript, JScript) и сохраните текстовый файл в надежном расположении следующим шагом является создание страницы веб-частей и добавьте веб-часть редактора содержимого и Службы Excel веб-части на страницу. 
  
    
    

Затем откройте книгу с помощью Службы Excel веб-части, который добавлен на страницу. 
### <a name="to-add-the-content-editor-web-part-and-the-excel-services-web-part"></a>Чтобы добавить веб-часть редактора содержимого и веб-части служб Excel


1. Создание новой страницы веб-частей. 
    
  
2. Добавление веб-части редактора контента на страницу веб-частей, который вы только что создали.
    
  
3. Веб-канал URL-адрес для текстовый файл, созданный в  [Этап 1: Создание ECMAScript текстового файла](step-1-creating-a-ecmascript-text-file) в веб-часть редактора содержимого. Это делается путем добавления URL-адрес для текстового файла, который загрузил библиотеку надежных документов в [Этап 1: Создание ECMAScript текстового файла](step-1-creating-a-ecmascript-text-file). 
    
    Например: 
    
     `http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`
    
  
4. Добавьте Службы Excel веб-части на страницу.
    
  

### <a name="to-run-the-ecmascript-sample"></a>Чтобы запустить образец ECMAScript


1. Отправка книги в библиотеке надежным документом. Использование меню **Изменить общую веб-часть** для отображения области задач Службы Excel веб-части. В разделе **Отображение книги** в поле **книги** введите URL-адрес, который будет Службы Excel веб-части для загрузки и отображения книги. Например:
    
     `http://` _myserver_ `/Docs/Documents/WorkbookToDisplay.xlsx`
    
  
2. Щелкните различные ячейки и выводятся в редактор контента **div**установлено значение ячейки. 
    
  

