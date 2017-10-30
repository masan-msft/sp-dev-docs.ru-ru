---
title: "Шаг 1. Создание проекта клиента веб-службы"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1f0fc9fc-0db4-47bb-8204-a06777b84e76
ms.openlocfilehash: 4224c42b2ffbb1cf037e59fac927811510441970
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="step-1-creating-the-web-service-client-project"></a><span data-ttu-id="0b901-102">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="0b901-102">Step 1: Creating the Web Service Client Project</span></span>

<span data-ttu-id="0b901-p101">В этом пошаговом руководстве описывается создание нового проекта и простого консольного приложения, осуществляющего доступ к веб-службам Веб-службы Excel. В этом пошаговом руководстве описывается разработка в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b901-p101">For this walkthrough, you will create a new project and a simple console application that accesses Excel Web Services. This walkthrough assumes you are developing in Visual Studio.</span></span> 
  
    
    


## <a name="creating-the-project"></a><span data-ttu-id="0b901-105">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="0b901-105">Creating the Project</span></span>

<span data-ttu-id="0b901-106">В описываемом проекте используется среда Microsoft Visual Studio 2003.</span><span class="sxs-lookup"><span data-stu-id="0b901-106">The following project uses Microsoft Visual Studio 2003.</span></span>
  
    
    

> <span data-ttu-id="0b901-107">**Примечание:** Если вы используете Microsoft Visual Studio 2005 или Microsoft Visual Studio 2008, процесс создания нового проекта отличается в зависимости от того, какие параметры использовать в среде разработки Visual Studio (IDE).</span><span class="sxs-lookup"><span data-stu-id="0b901-107">**Note:** If you are using Microsoft Visual Studio 2005 or Microsoft Visual Studio 2008, the process to create a new project is slightly different depending on which settings you use in the Visual Studio integrated development environment (IDE).</span></span>
  
    
    


### <a name="to-create-a-new-project"></a><span data-ttu-id="0b901-108">Создание нового проекта</span><span class="sxs-lookup"><span data-stu-id="0b901-108">To create a new project</span></span>


1. <span data-ttu-id="0b901-109">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0b901-109">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="0b901-p102">В меню **Файл** выберите пункт **Создать** и затем пункт **Проект**. Открывается диалоговое окно **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="0b901-p102">On the **File** menu, point to **New**, and then click **Project**. The **New Project** dialog box appears.</span></span>
    
  
3. <span data-ttu-id="0b901-112">В области **Тип проекта** выберите пункт **Проекты Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="0b901-112">In the **Project Type** pane, select **Visual C# Projects**.</span></span>
    
  
4. <span data-ttu-id="0b901-113">В области **Шаблоны** выберите пункт **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="0b901-113">In the **Templates** pane, click **Console Application**.</span></span>
    
  
5. <span data-ttu-id="0b901-114">В поле **Имя** введите **SampleApplication**.</span><span class="sxs-lookup"><span data-stu-id="0b901-114">In the **Name** box, type **SampleApplication**.</span></span>
    
  
6. <span data-ttu-id="0b901-115">В поле **Расположение** введите путь к папке, в которой требуется сохранить проект, или нажмите кнопку **Обзор** и перейдите к нужной папке.</span><span class="sxs-lookup"><span data-stu-id="0b901-115">In the **Location** box, enter the path where you want to save your project, or click **Browse** to navigate to the folder.</span></span>
    
  
7. <span data-ttu-id="0b901-p103">Нажмите кнопку **ОК**. Созданный проект отображается в окне **Обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="0b901-p103">Click **OK**. Your newly created project appears in **Solution Explorer**.</span></span> 
  
    
    
<span data-ttu-id="0b901-118">В окне **Обозреватель решений** в проект добавлен файл с установленным по умолчанию именем Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="0b901-118">In **Solution Explorer**, a file with the default name of Class1.cs has been added to your project.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="0b901-119">См. также</span><span class="sxs-lookup"><span data-stu-id="0b901-119">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="0b901-120">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="0b901-120">Concepts</span></span>


  
    
    
 [<span data-ttu-id="0b901-121">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="0b901-121">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
  
    
    
 [<span data-ttu-id="0b901-122">Excel Services Alerts</span><span class="sxs-lookup"><span data-stu-id="0b901-122">Excel Services Alerts</span></span>](excel-services-alerts.md)
  
    
    
 [<span data-ttu-id="0b901-123">Excel Services Known Issues and Tips</span><span class="sxs-lookup"><span data-stu-id="0b901-123">Excel Services Known Issues and Tips</span></span>](excel-services-known-issues-and-tips.md)
#### <a name="other-resources"></a><span data-ttu-id="0b901-124">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="0b901-124">Other resources</span></span>


  
    
    
 [<span data-ttu-id="0b901-125">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="0b901-125">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="0b901-126">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="0b901-126">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="0b901-127">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="0b901-127">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="0b901-128">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="0b901-128">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
