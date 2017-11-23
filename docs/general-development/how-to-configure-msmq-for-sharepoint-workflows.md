---
title: "Как настроить MSMQ для рабочих процессов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c0e130f6-c210-44ea-83ed-b327f04551d6
ms.openlocfilehash: 40ad8b9b742a19a24e0e2dfa648efeda623a892a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-configure-msmq-for-sharepoint-workflows"></a><span data-ttu-id="f6542-102">Как: Настройка MSMQ для рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6542-102">How to: Configure MSMQ for SharePoint workflows</span></span>
<span data-ttu-id="f6542-103">Сведения о настройке очередей сообщений Microsoft (MSMQ) в SharePoint для поддержки асинхронные события системы обмена сообщениями в рабочих процессах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f6542-103">Learn how to configure Microsoft Message Queuing (MSMQ) in SharePoint to support asynchronous event messaging in SharePoint workflows.</span></span> 
## <a name="enabling-msmq"></a><span data-ttu-id="f6542-104">Включение MSMQ</span><span class="sxs-lookup"><span data-stu-id="f6542-104">Enabling MSMQ</span></span>

<span data-ttu-id="f6542-p101">MSMQ  это компонент Windows Server, которые можно включить на компьютере SharePoint Server, чтобы разрешить асинхронные события системы обмена сообщениями в рабочих процессах SharePoint. Чтобы обеспечить поддержку асинхронные события системы обмена сообщениями, необходимо включить MSMQ на компьютере SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="f6542-p101">MSMQ is a Windows Server feature that you can enable on your SharePoint Server computer to allow asynchronous event messaging in SharePoint workflows. To support asynchronous event messaging, you must enable MSMQ on your SharePoint Server computer.</span></span>
  
    
    
<span data-ttu-id="f6542-p102">MSMQ предоставляется как «Функция» в Windows Server. Чтобы включить MSMQ, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f6542-p102">MSMQ is provided as a "Feature" in Windows Server. To enable MSMQ, do the following:</span></span>
  
    
    

> <span data-ttu-id="f6542-109">**Важные:** Снимки экрана, включены приходятся на Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="f6542-109">**Important:** The screen shots included here are from Windows Server 2008 R2.</span></span> <span data-ttu-id="f6542-110">Пользовательский Интерфейс может отличаться от эта функция включена в Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="f6542-110">The UI may change for enabling this feature in Windows Server 2012.</span></span> 
  
    
    


1. <span data-ttu-id="f6542-111">На компьютере SharePoint Server откройте **Диспетчер сервера**.</span><span class="sxs-lookup"><span data-stu-id="f6542-111">On your SharePoint Server computer, open **Server Manager**.</span></span>
    
  
2. <span data-ttu-id="f6542-112">В левой области выберите значок **функции**, а затем выберите **Добавить компоненты**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="f6542-112">Select the **Features** icon in the left pane, then select **Add Features**, as depicted in Figure 1.</span></span>
    
   <span data-ttu-id="f6542-113">**Рис. 1. Добавление функции очереди сообщений.**</span><span class="sxs-lookup"><span data-stu-id="f6542-113">**Figure 1. Adding the Message Queuing feature.**</span></span>

  

  ![Рис. 1. Добавление функции очереди сообщений.](../images/ng_MsmqFeature.png)
  

  

  
3. <span data-ttu-id="f6542-p105">В окне **Мастер добавления компонентов**, который отображается выберите **Очередь сообщений**. Оставьте значения по умолчанию и затем нажмите кнопку **Далее**, а затем нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="f6542-p105">In the **Add Features Wizard** that appears, select **Message Queuing**. Accept the default selections and then click **Next**, then click **Install**.</span></span>
    
  
4. <span data-ttu-id="f6542-118">Теперь необходимо перезагрузить компьютер.</span><span class="sxs-lookup"><span data-stu-id="f6542-118">You must now restart your computer.</span></span>
    
  
5. <span data-ttu-id="f6542-p106">После перезапуска, откройте **Диспетчер сервера**, а затем откройте значок " **Очередь сообщений** " в панели слева. Обратите внимание на то, что она теперь содержит **Очереди сообщений** папки и вложенные папки, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="f6542-p106">Once restarted, open **Server Manager** and then open **Message Queuing** icon in the left pane. Notice that it now contains a **Message Queuing** folder and subdirectories, as depicted in Figure 2.</span></span>
    
    > <span data-ttu-id="f6542-121">**Примечание:** В Windows Server 2012 очереди не содержатся в **Диспетчер сервера**.</span><span class="sxs-lookup"><span data-stu-id="f6542-121">**Note:** In Windows Server 2012 you will not find the queues in **Server Manager**.</span></span> <span data-ttu-id="f6542-122">Вместо этого перейдите в раздел **Управление компьютером**, а затем выберите **службы и приложения**.</span><span class="sxs-lookup"><span data-stu-id="f6542-122">Instead, go to **Computer Management**, then select **Services and applications**.</span></span> 
6. <span data-ttu-id="f6542-p108">Выберите подкаталог **Частные очереди**. Это каталог, в котором хранятся сообщения события рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="f6542-p108">Select the subdirectory named **Private Queues**. This is the directory in which your workflow event messages are stored.</span></span>
    
   <span data-ttu-id="f6542-125">**На рисунке 2. Очередь сообщений компонент, добавленный в диспетчер сервера.**</span><span class="sxs-lookup"><span data-stu-id="f6542-125">**Figure 2. The Message Queuing feature added to Server Manager.**</span></span>

  

  ![Рис. 2. Функция очереди сообщений добавлен в Ser](../images/ng_MsmqQueues.png)
  

    
    
    
    > <span data-ttu-id="f6542-128">**Примечание:** При первом добавлении средства **Очередей сообщений** , **Частные очереди** папка пуста.</span><span class="sxs-lookup"><span data-stu-id="f6542-128">**Note:** When you first add the **Message Queuing** feature, the **Private Queues** folder is empty.</span></span> <span data-ttu-id="f6542-129">Тем не менее после запуска рабочего процесса, активируется по событию (или активировать по SharePoint, выполняется событие контента изменения рабочего процесса) выполняется заполнение папку **Частные очереди** , как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="f6542-129">However, after a workflow runs that fires an event (or a workflow triggered by a SharePoint content change event runs), the **Private Queues** folder is populated as shown in Figure 2.</span></span>
7. <span data-ttu-id="f6542-p111">Чтобы завершить установку, необходимо установить свойство **SPWorkflowServiceApplicationProxy.AllowQueue** для **true** с помощью сценария Windows PowerShell. В **командной консоли администрирования SharePoint**, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f6542-p111">To complete the installation, you must set the **SPWorkflowServiceApplicationProxy.AllowQueue** property to **true** using a Windows PowerShell script. In the **SharePoint Administration shell**, run the following:</span></span>
    
```
  
$proxy = Get-SPWorkflowServiceApplicationProxy
$proxy.AllowQueue = $true;
$proxy.Update();

```


## <a name="troubleshooting-msmq"></a><span data-ttu-id="f6542-132">Устранение неполадок MSMQ</span><span class="sxs-lookup"><span data-stu-id="f6542-132">Troubleshooting MSMQ</span></span>

<span data-ttu-id="f6542-p112">Центр разработчиков Windows предоставляет подробную документацию MSMQ. Ниже перечислены некоторые полезные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f6542-p112">The Windows Developer Center provides extensive documentation of MSMQ. Following are some useful resources:</span></span>
  
    
    

-  [<span data-ttu-id="f6542-135">Об очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="f6542-135">About Message Queuing</span></span>](http://msdn.microsoft.com/ru-ru/library/windows/desktop/ms706032%28v=vs.85%29.aspx)
    
  
-  [<span data-ttu-id="f6542-136">Справочник по очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="f6542-136">Message Queuing Reference</span></span>](http://msdn.microsoft.com/ru-ru/library/windows/desktop/ms700112%28v=vs.85%29.aspx)
    
  
-  [<span data-ttu-id="f6542-137">Очередь сообщений об ошибках и коды информации</span><span class="sxs-lookup"><span data-stu-id="f6542-137">Message Queuing Error and Information Codes</span></span>](http://msdn.microsoft.com/ru-ru/library/windows/desktop/ms700106%28v=vs.85%29.aspx)
    
  

## <a name="additional-resources"></a><span data-ttu-id="f6542-138">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f6542-138">Additional resources</span></span>
<span data-ttu-id="f6542-139"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f6542-139"></span></span>


-  [<span data-ttu-id="f6542-140">Очередь сообщений (MSMQ)</span><span class="sxs-lookup"><span data-stu-id="f6542-140">Message Queuing (MSMQ)</span></span>](http://msdn.microsoft.com/ru-ru/library/windows/desktop/ms711472%28v=vs.85%29.aspx)
    
  

  
    
    

