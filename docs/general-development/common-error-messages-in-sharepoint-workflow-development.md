---
title: "Распространенные сообщения об ошибках при разработке рабочих процессов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e9bf6878-c722-4b1f-b5b5-b302ae0ea4da
ms.openlocfilehash: b838b41869ab9f8ff44309fe34b3b3b7ba72c052
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="common-error-messages-in-sharepoint-workflow-development"></a><span data-ttu-id="826ed-102">Распространенные сообщения об ошибках при разработке рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="826ed-102">Common error messages in SharePoint workflow development</span></span>
<span data-ttu-id="826ed-103">Список распространенных сообщений об ошибках, которые могут возникнуть при разработке рабочих процессов SharePoint, и указания по устранению исходной проблемы.</span><span class="sxs-lookup"><span data-stu-id="826ed-103">A listing of common error messages that you might encounter while developing SharePoint workflows and guidance for solving the underlying problem.</span></span>
## <a name="common-sharepoint-workflow-errors"></a><span data-ttu-id="826ed-104">Распространенные ошибки рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="826ed-104">Common SharePoint workflow errors</span></span>

<span data-ttu-id="826ed-105">Хотя этот список включает не все возможные ошибки, которые могут возникнуть при разработке рабочих процессов SharePoint, в нем представлены те, которые наиболее вероятны.</span><span class="sxs-lookup"><span data-stu-id="826ed-105">Although this list doesn't cover every possible error you may encounter when developing SharePoint workflows, it does cover those that you are most likely to face.</span></span>
  
    
    

-  [<span data-ttu-id="826ed-106">Истекло время ожидания завершения запроса на выполнение изолированного кода в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="826ed-106">Timeout while waiting for sandboxed code execution request to complete within the worker process</span></span>](#bkmk_error01)
    
  
-  [<span data-ttu-id="826ed-107">Истекло время ожидания завершения запроса в изолированном домене приложения</span><span class="sxs-lookup"><span data-stu-id="826ed-107">Timeout while waiting for request to complete within the sandboxed appdomain</span></span>](#bkmk_error02)
    
  
-  [<span data-ttu-id="826ed-108">Рабочий процесс, выполняющий этот запрос, завершен из-за превышения нормы ресурса {0}</span><span class="sxs-lookup"><span data-stu-id="826ed-108">The worker process handling this request was ended because it exceeded the resource {0}</span></span>](#bkmk_error03)
    
  
-  [<span data-ttu-id="826ed-109">Не удалось запустить рабочий процесс из-за ошибки песочницы</span><span class="sxs-lookup"><span data-stu-id="826ed-109">This workflow could not run because a sandboxed solution encountered an error</span></span>](#bkmk_error04)
    
  
-  [<span data-ttu-id="826ed-110">Не удалось запустить рабочий процесс из-за ошибки песочницы: не удалось получить процесс из пула процессов</span><span class="sxs-lookup"><span data-stu-id="826ed-110">This workflow could not run because the sandbox failed: Could not get a process from the process pool</span></span>](#bkmk_error05)
    
  
-  [<span data-ttu-id="826ed-111">Не удалось запустить рабочий процесс из-за ошибки песочницы: неожиданный выход из рабочего процесса изолированного кода</span><span class="sxs-lookup"><span data-stu-id="826ed-111">This workflow could not run because the sandbox failed: The sandboxed code worker process exited unexpectedly</span></span>](#bkmk_error06)
    
  
-  [<span data-ttu-id="826ed-112">Не удается отправить сообщение электронной почты. Проверьте правильность настройки параметров исходящей электронной почты на сервере</span><span class="sxs-lookup"><span data-stu-id="826ed-112">The e-mail message cannot be sent. Make sure the outgoing e-mail settings for the server are configured correctly</span></span>](#bkmk_error07)
    
  
-  [<span data-ttu-id="826ed-113">Обновить элемент в рабочем процессе не удалось, возможно потому, что в одном или нескольких столбцах для этого элемента должны содержаться данные другого типа</span><span class="sxs-lookup"><span data-stu-id="826ed-113">The workflow could not update the item, possibly because one or more columns for the item require a different type of information</span></span>](#bkmk_error08)
    
  
-  [<span data-ttu-id="826ed-114">Операция рабочего процесса не выполнена, поскольку подстановка в рабочем процессе не позволила найти подходящий элемент</span><span class="sxs-lookup"><span data-stu-id="826ed-114">The workflow operation failed because the workflow lookup found no matching item</span></span>](#bkmk_error09)
    
  
-  [<span data-ttu-id="826ed-115">Рабочему процессу не удалось создать элемент списка, так как имя файла отсутствует или не является допустимым</span><span class="sxs-lookup"><span data-stu-id="826ed-115">The workflow could not create the list item because the file name is either missing or invalid</span></span>](#bkmk_error10)
    
  
-  [<span data-ttu-id="826ed-116">Ошибка приведения: не удалось преобразовать входные данные подстановки к запрошенному типу</span><span class="sxs-lookup"><span data-stu-id="826ed-116">Coercion Failed: Unable to transform the input lookup data into the requested type</span></span>](#bkmk_error11)
    
  
-  [<span data-ttu-id="826ed-117">Операция рабочего процесса не выполнена, поскольку данное действие требует извлечения документа</span><span class="sxs-lookup"><span data-stu-id="826ed-117">The workflow operation failed because the action requires the document to be checked out</span></span>](#bkmk_error12)
    
  
-  [<span data-ttu-id="826ed-118">При компиляции рабочего процесса были обнаружены ошибки. Файлы рабочего процесса сохранены, но не могут быть выполнены. Непредвиденная ошибка на сервере при сопоставлении с рабочим процессом</span><span class="sxs-lookup"><span data-stu-id="826ed-118">Errors were found when compiling the workflow. The workflow files were saved but cannot be run. Unexpected error on server associating the workflow</span></span>](#bkmk_error13)
    
  

### <a name="timeout-while-waiting-for-sandboxed-code-execution-request-to-complete-within-the-worker-process"></a><span data-ttu-id="826ed-119">Истекло время ожидания завершения запроса на выполнение изолированного кода в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="826ed-119">Timeout while waiting for sandboxed code execution request to complete within the worker process</span></span>
<span data-ttu-id="826ed-120"><a name="bkmk_error01"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-120"><a name="bkmk_error01"> </a></span></span>

<span data-ttu-id="826ed-121">Те же проблема и решение, что и в разделе ниже, "Истекло время ожидания завершения запроса в изолированном домене приложения".</span><span class="sxs-lookup"><span data-stu-id="826ed-121">Same issue and same solution as the item below, "Timeout while waiting for request to complete within the sandboxed appdomain".</span></span>
  
    
    

### <a name="timeout-while-waiting-for-request-to-complete-within-the-sandboxed-appdomain"></a><span data-ttu-id="826ed-122">Истекло время ожидания завершения запроса в изолированном домене приложения</span><span class="sxs-lookup"><span data-stu-id="826ed-122">Timeout while waiting for request to complete within the sandboxed appdomain</span></span>
<span data-ttu-id="826ed-123"><a name="bkmk_error02"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-123"><a name="bkmk_error02"> </a></span></span>

<span data-ttu-id="826ed-p101">Обе эти ошибки вызваны одной и той же проблемой  истечением времени ожидания по умолчанию для выполняемого действия рабочего процесса. Время ожидания по умолчанию составляет 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="826ed-p101">Both of these errors result from the same issue—exceeding the default timeout period for the workflow action to execute. The default timeout period is 30 seconds.</span></span>
  
    
    
<span data-ttu-id="826ed-p102">В локальных установках можно изменять время ожидания, а в установках SharePoint Online это невозможно. Чтобы избежать этой ошибки в установках SharePoint Online, необходимо изменить код, ограничив действия в рабочем процессе или домене приложения так, чтобы они занимали менее 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="826ed-p102">You can change the timeout value in on-premises installations, but you can't change it in SharePoint Online installations. To avoid getting this error in SharePoint Online installations, you must modify your code to limit actions in the worker process or appdomain to fewer than 30 seconds.</span></span>
  
    
    
<span data-ttu-id="826ed-p103">Чтобы изменить время ожидания в локальной установке, выполните следующую команду Windows PowerShell. Обратите внимание, что пример кода сбрасывает время ожидания до 60 секунд, но вы можете использовать другое значение.</span><span class="sxs-lookup"><span data-stu-id="826ed-p103">To modify the timeout period in your on-premises installation, execute the following Windows PowerShell command. Note that the example code resets the timeout to 60 seconds, but you can use another value.</span></span>
  
    
    



```

Add-pssnapin microsoft.sharepoint.powershell
   $userCodeSvc = [Microsoft.SharePoint.Administration.SPUserCodeService]::Local
   #change to 60 second timeout
   $userCodeSvc.WorkerProcessExecutionTimeout = 60 
   $userCodeSvc.Update()
```


### <a name="the-worker-process-handling-this-request-was-ended-because-it-exceeded-the-resource-0"></a><span data-ttu-id="826ed-130">Рабочий процесс, выполняющий этот запрос, завершен из-за превышения нормы ресурса {0}</span><span class="sxs-lookup"><span data-stu-id="826ed-130">The worker process handling this request was ended because it exceeded the resource {0}</span></span>
<span data-ttu-id="826ed-131"><a name="bkmk_error03"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-131"><a name="bkmk_error03"> </a></span></span>

<span data-ttu-id="826ed-p104">Значение  `{0}` в строке ошибки является заполнителем для конкретного ресурса, норма которого была превышена. Чтобы устранить эту проблему, необходимо изменить код так, чтобы он не превышал норму ресурса. Эти значения указаны в статье [Ограничения на использование ресурсов для изолированных решений](http://msdn.microsoft.com/ru-RU/library/gg615462%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="826ed-p104">In the error string, the value of  `{0}` is a placeholder for the specific resource whose threshold has been exceeded. To alleviate this problem, you should modify your code so that it does not exceed the resource threshold. These resource values are documented in [Resource Usage Limits on Sandboxed Solutions in SharePoint 2010](http://msdn.microsoft.com/ru-RU/library/gg615462%28v=office.14%29.aspx).</span></span>
  
    
    

### <a name="this-workflow-could-not-run-because-a-sandboxed-solution-encountered-an-error"></a><span data-ttu-id="826ed-135">Не удалось запустить рабочий процесс из-за ошибки песочницы</span><span class="sxs-lookup"><span data-stu-id="826ed-135">This workflow could not run because a sandboxed solution encountered an error</span></span>
<span data-ttu-id="826ed-136"><a name="bkmk_error04"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-136"><a name="bkmk_error04"> </a></span></span>

<span data-ttu-id="826ed-p105">В коде рабочего процесса возникло необработанное исключение. Для устранения этой ошибки необходимы отладка и изменение изолированного кода.</span><span class="sxs-lookup"><span data-stu-id="826ed-p105">The workflow code threw an unhandled exception. Resolving this error requires debugging and revising your sandboxed code.</span></span>
  
    
    

### <a name="this-workflow-could-not-run-because-the-sandbox-failed-could-not-get-a-process-from-the-process-pool"></a><span data-ttu-id="826ed-139">Не удалось запустить рабочий процесс из-за ошибки песочницы: не удалось получить процесс из пула процессов</span><span class="sxs-lookup"><span data-stu-id="826ed-139">This workflow could not run because the sandbox failed: Could not get a process from the process pool</span></span>
<span data-ttu-id="826ed-140"><a name="bkmk_error05"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-140"><a name="bkmk_error05"> </a></span></span>

<span data-ttu-id="826ed-p106">Конфигурацию песочницы содержит ошибку. Сведения о настройке изолированного решения см. в статье  [Изолированные решения в SharePoint](http://msdn.microsoft.com/ru-RU/library/ee536577%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="826ed-p106">There is an error in your sandbox configuration. For information about configuring a sandboxed solution, see  [Sandboxed Solutions in SharePoint](http://msdn.microsoft.com/ru-RU/library/ee536577%28v=office.14%29.aspx).</span></span>
  
    
    

### <a name="this-workflow-could-not-run-because-the-sandbox-failed-the-sandboxed-code-worker-process-exited-unexpectedly"></a><span data-ttu-id="826ed-143">Не удалось запустить рабочий процесс из-за ошибки песочницы: неожиданный выход из рабочего процесса изолированного кода</span><span class="sxs-lookup"><span data-stu-id="826ed-143">This workflow could not run because the sandbox failed: The sandboxed code worker process exited unexpectedly</span></span>
<span data-ttu-id="826ed-144"><a name="bkmk_error06"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-144"><a name="bkmk_error06"> </a></span></span>

<span data-ttu-id="826ed-p107">Конфигурацию песочницы содержит ошибку. Сведения о настройке изолированного решения см. в статье  [Изолированные решения в SharePoint](http://msdn.microsoft.com/ru-RU/library/ee536577%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="826ed-p107">There is an error in your sandbox configuration. For information about configuring a sandboxed solution, see  [Sandboxed Solutions in SharePoint](http://msdn.microsoft.com/ru-RU/library/ee536577%28v=office.14%29.aspx).</span></span>
  
    
    

### <a name="the-e-mail-message-cannot-be-sent-make-sure-the-outgoing-e-mail-settings-for-the-server-are-configured-correctly"></a><span data-ttu-id="826ed-p108">Не удается отправить сообщение электронной почты. Проверьте правильность настройки параметров исходящей электронной почты на сервере</span><span class="sxs-lookup"><span data-stu-id="826ed-p108">The e-mail message cannot be sent. Make sure the outgoing e-mail settings for the server are configured correctly</span></span>
<span data-ttu-id="826ed-149"><a name="bkmk_error07"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-149"><a name="bkmk_error07"> </a></span></span>

<span data-ttu-id="826ed-p109">При устранении неполадок электронной почты следует учитывать два аспекта. Как в локальных установках, так и в SharePoint Online необходимо убедиться, что все строки **Кому:** и **Копия:** являются допустимыми адресами электронной почты. В локальных установках необходимо убедиться, что на сервере правильно настроены параметры электронной почты.</span><span class="sxs-lookup"><span data-stu-id="826ed-p109">There are two issues of note to consider when troubleshooting email issues. In both on-premises and SharePoint Online installations, ensure that all addresses on the **To:** and **Cc:** lines are valid email addresses. In on-premises installations, ensure that email settings on the server are configured correctly.</span></span>
  
    
    
<span data-ttu-id="826ed-153">Ознакомьтесь с приведенными ниже статьями, чтобы убедиться в правильности настройки входящей и исходящей почты.</span><span class="sxs-lookup"><span data-stu-id="826ed-153">Review the following to ensure that you have correctly configured incoming and outgoing emails.</span></span>
  
    
    

-  [<span data-ttu-id="826ed-154">Руководство по развертыванию Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="826ed-154">Deployment guide for Microsoft SharePoint</span></span>](http://download.microsoft.com/download/1/F/6/1F6D3BE4-1174-4320-A1D1-C0E2681CCCF3/Deployment-guide-for-SharePoint.pdf)
    
  
-  [<span data-ttu-id="826ed-155">Настройка входящей и исходящей почты в SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="826ed-155">How to configure Incoming and Outgoing emails in SharePoint Server</span></span>](http://blogs.msdn.com/b/pareshg/archive/2010/04/23/how-to-configure-incoming-and-outgoing-emails-in-sharepoint-server-2010.aspx)
    
  

### <a name="the-workflow-could-not-update-the-item-possibly-because-one-or-more-columns-for-the-item-require-a-different-type-of-information"></a><span data-ttu-id="826ed-156">Обновить элемент в рабочем процессе не удалось, возможно потому, что в одном или нескольких столбцах для этого элемента должны содержаться данные другого типа</span><span class="sxs-lookup"><span data-stu-id="826ed-156">The workflow could not update the item, possibly because one or more columns for the item require a different type of information</span></span>
<span data-ttu-id="826ed-157"><a name="bkmk_error08"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-157"><a name="bkmk_error08"> </a></span></span>

<span data-ttu-id="826ed-158">Как правило, эта ошибка вызвана одной из двух ситуаций:</span><span class="sxs-lookup"><span data-stu-id="826ed-158">This error commonly results from one of two situations:</span></span>
  
    
    

- <span data-ttu-id="826ed-p110">Одно из полей списка была удалено или изменено, но рабочий процесс не был обновлен с учетом изменений и пытается задать значение старого поля. Проверьте все действия **Обновление элемента списка** в рабочем процессе и убедитесь, что они задают подходящие значения полей, а эти поля присутствуют в списке.</span><span class="sxs-lookup"><span data-stu-id="826ed-p110">One of the list fields was removed or changed, but the workflow was not updated to account for the change and is therefore trying to set a value for the old field. You should check all **Update List Item** actions in your workflow and make sure they are setting appropriate values for fields and that those fields exist on the list.</span></span>
    
  
- <span data-ttu-id="826ed-p111">Ошибка типа данных, вызванная тем, что рабочий процесс пытается задать значение поля в элементе списка с неправильным типом данных. Необходимо убедиться, что операция **Вернуть поле как** в подстановке имеет правильный тип данных.</span><span class="sxs-lookup"><span data-stu-id="826ed-p111">There is a data type error wherein the workflow is trying to set a value in a field in the list item using the wrong data type. You should confirm that the **Return Field As** operation in their lookup is of the correct data type.</span></span>
    
  

### <a name="the-workflow-operation-failed-because-the-workflow-lookup-found-no-matching-item"></a><span data-ttu-id="826ed-163">Операция рабочего процесса не выполнена, поскольку подстановка в рабочем процессе не позволила найти подходящий элемент</span><span class="sxs-lookup"><span data-stu-id="826ed-163">The workflow operation failed because the workflow lookup found no matching item</span></span>
<span data-ttu-id="826ed-164"><a name="bkmk_error09"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-164"><a name="bkmk_error09"> </a></span></span>

<span data-ttu-id="826ed-p112">Это указывает ошибку в логике рабочего процесса. Убедитесь, что в подстановке выбираются правильные список и поле.</span><span class="sxs-lookup"><span data-stu-id="826ed-p112">This indicates there is an error in the workflow logic. Check to ensure that you are selecting the correct list and field in your lookup.</span></span>
  
    
    

### <a name="the-workflow-could-not-create-the-list-item-because-the-file-name-is-either-missing-or-invalid"></a><span data-ttu-id="826ed-167">Рабочему процессу не удалось создать элемент списка, так как имя файла отсутствует или не является допустимым</span><span class="sxs-lookup"><span data-stu-id="826ed-167">The workflow could not create the list item because the file name is either missing or invalid</span></span>
<span data-ttu-id="826ed-168"><a name="bkmk_error10"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-168"><a name="bkmk_error10"> </a></span></span>

<span data-ttu-id="826ed-p113">Это указывает на ошибку в логике рабочего процесса. Убедитесь, что имя файла, указанное в поле **Путь и имя**, является допустимым. К распространенным причинам некорректности имени файла относятся отсутствующие или неправильные расширения, а также строки имени или пути, длина которых превышает допустимую.</span><span class="sxs-lookup"><span data-stu-id="826ed-p113">This indicates there is an error in the workflow logic. Ensure that the file name entered in the **Path and Name** field is a valid file name. Common reasons for a file name to be invalid include a missing or incorrect file extension or a file/path string that is too long and exceeds the allowable number of characters.</span></span>
  
    
    

### <a name="coercion-failed-unable-to-transform-the-input-lookup-data-into-the-requested-type"></a><span data-ttu-id="826ed-172">Ошибка приведения: не удалось преобразовать входные данные подстановки к запрошенному типу</span><span class="sxs-lookup"><span data-stu-id="826ed-172">Coercion Failed: Unable to transform the input lookup data into the requested type</span></span>
<span data-ttu-id="826ed-173"><a name="bkmk_error11"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-173"><a name="bkmk_error11"> </a></span></span>

<span data-ttu-id="826ed-p114">Операции не удалось преобразовать значения между несовместимыми типами данных (например, преобразовать случайную строку в значение даты и времени). Проверьте параметры операции **Вернуть поле как** в подстановке и убедитесь, что тип является допустимым для ожидаемых данных.</span><span class="sxs-lookup"><span data-stu-id="826ed-p114">The operation failed to cast values between incompatible data types (for example, converting a random string to a Date/Time value). You should check the **Return Field As** settings in your lookup to ensure that it is a valid data type for the expected data.</span></span>
  
    
    

### <a name="the-workflow-operation-failed-because-the-action-requires-the-document-to-be-checked-out"></a><span data-ttu-id="826ed-176">Операция рабочего процесса не выполнена, поскольку данное действие требует извлечения документа</span><span class="sxs-lookup"><span data-stu-id="826ed-176">The workflow operation failed because the action requires the document to be checked out</span></span>
<span data-ttu-id="826ed-177"><a name="bkmk_error12"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-177"><a name="bkmk_error12"> </a></span></span>

<span data-ttu-id="826ed-178">Необходимо извлечь элемент с помощью действия **Извлечь элемент**, прежде чем использовать действие **Обновить элемент**.</span><span class="sxs-lookup"><span data-stu-id="826ed-178">You must check out the item using the **Check Out Item** action before using the **Update Item** action.</span></span>
  
    
    

### <a name="errors-were-found-when-compiling-the-workflow-the-workflow-files-were-saved-but-cannot-be-run-unexpected-error-on-server-associating-the-workflow"></a><span data-ttu-id="826ed-p115">При компиляции рабочего процесса были обнаружены ошибки. Файлы рабочего процесса сохранены, но не могут быть выполнены. Непредвиденная ошибка на сервере при сопоставлении с рабочим процессом</span><span class="sxs-lookup"><span data-stu-id="826ed-p115">Errors were found when compiling the workflow. The workflow files were saved but cannot be run. Unexpected error on server associating the workflow</span></span>
<span data-ttu-id="826ed-182"><a name="bkmk_error13"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-182"><a name="bkmk_error13"> </a></span></span>

<span data-ttu-id="826ed-183">Дополнительные сведения см. в  [статье базы знаний службы поддержки Майкрософт с номером 2557533](http://support.microsoft.com/kb/2557533) ( `http://support.microsoft.com/kb/2557533`).</span><span class="sxs-lookup"><span data-stu-id="826ed-183">See  [Microsoft Support Knowledge Base article ID 2557533](http://support.microsoft.com/kb/2557533) ( `http://support.microsoft.com/kb/2557533`) for more information.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="826ed-184">См. также</span><span class="sxs-lookup"><span data-stu-id="826ed-184">See also</span></span>
<span data-ttu-id="826ed-185"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="826ed-185"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="826ed-186">Рекомендации по разработке рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="826ed-186">SharePoint workflow development best practices</span></span>](sharepoint-workflow-development-best-practices.md)
    
  
-  [<span data-ttu-id="826ed-187">Разработка рабочих процессов в SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="826ed-187">Develop SharePoint workflows using Visual Studio</span></span>](develop-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

