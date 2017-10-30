---
title: "Пошаговое руководство по разработке с использованием веб-части редактора контента"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0b5e74b7-405c-43c5-b2dd-1dff77280856
ms.openlocfilehash: ded8a724e95d5bc9f4c10a9d902d7f13a468baad
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="walkthrough-developing-using-the-content-editor-web-part"></a><span data-ttu-id="d7d20-102">Пошаговое руководство по разработке с использованием веб-части редактора контента</span><span class="sxs-lookup"><span data-stu-id="d7d20-102">Walkthrough: Developing Using the Content Editor Web Part</span></span>

<span data-ttu-id="d7d20-103">В этом разделе представлено пошаговое руководство описывает процесс для взаимодействия с объектной моделью ECMAScript (JavaScript, JScript) в Службы Excel с помощью веб-часть редактора содержимого.</span><span class="sxs-lookup"><span data-stu-id="d7d20-103">The walkthrough in this section describes the process for interacting with the ECMAScript (JavaScript, JScript) object model in Excel Services by using the Content Editor Web Part.</span></span>
  
    
    

<span data-ttu-id="d7d20-104">В руководстве рассматриваются следующие этапы:</span><span class="sxs-lookup"><span data-stu-id="d7d20-104">During this walkthrough, you will learn how to:</span></span>
- <span data-ttu-id="d7d20-105">Создайте текстовый файл, содержащий JavaScript и сохраните его в виде текстового файла в библиотеке надежным документом.</span><span class="sxs-lookup"><span data-stu-id="d7d20-105">Create a text file that contains JavaScript and save it as a text file to a trusted document library.</span></span> 
    
  
- <span data-ttu-id="d7d20-106">Добавление веб-части редактора контента и затем передайте URL-адрес в текстовом файле JavaScript в веб-часть редактора содержимого.</span><span class="sxs-lookup"><span data-stu-id="d7d20-106">Add a Content Editor Web Part, and then feed the URL for the JavaScript text file to the Content Editor Web Part.</span></span>
    
  
- <span data-ttu-id="d7d20-107">Отображения и взаимодействия с книги с помощью Службы Excel веб-часть, которая будет вызывать JavaScript в Службы Excel , который вы или с помощью сценария.</span><span class="sxs-lookup"><span data-stu-id="d7d20-107">Display and interact with a workbook by using the Excel Services Web Part that will call the JavaScript in Excel Services that you scripted.</span></span> 
    
  

> <span data-ttu-id="d7d20-108">**Примечание:** Сведения о том, как надежного расположения можно [как: надежного расположения](how-to-trust-a-location.md).</span><span class="sxs-lookup"><span data-stu-id="d7d20-108">**Note:** For information about how to trust a location, see  [How to: Trust a Location](how-to-trust-a-location.md).</span></span> 
  
    
    


## <a name="see-also"></a><span data-ttu-id="d7d20-109">См. также</span><span class="sxs-lookup"><span data-stu-id="d7d20-109">See also</span></span>


#### <a name="tasks"></a><span data-ttu-id="d7d20-110">Задачи</span><span class="sxs-lookup"><span data-stu-id="d7d20-110">Tasks</span></span>


  
    
    
 [<span data-ttu-id="d7d20-111">How to: Trust a Location</span><span class="sxs-lookup"><span data-stu-id="d7d20-111">How to: Trust a Location</span></span>](how-to-trust-a-location.md)
#### <a name="concepts"></a><span data-ttu-id="d7d20-112">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="d7d20-112">Concepts</span></span>


  
    
    
 [<span data-ttu-id="d7d20-113">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="d7d20-113">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="d7d20-114">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="d7d20-114">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
#### <a name="other-resources"></a><span data-ttu-id="d7d20-115">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="d7d20-115">Other resources</span></span>


  
    
    
 [<span data-ttu-id="d7d20-116">How to: Trust Workbook Locations Using Script</span><span class="sxs-lookup"><span data-stu-id="d7d20-116">How to: Trust Workbook Locations Using Script</span></span>](http://msdn.microsoft.com/library/79ab6ced-7a0c-4275-b852-bb246fc6be57%28Office.15%29.aspx)
