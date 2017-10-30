---
title: "С помощью командлета связывания Register-SPWorkflowService"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 91fca6c2-60ca-4177-8560-2b310dac0e2c
ms.openlocfilehash: b04bb57d3583ea7fb4e8927ff867ab5ff3e2b264
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="using-the-pairing-cmdlet-register-spworkflowservice"></a><span data-ttu-id="07e65-102">С помощью командлета связывания Register-SPWorkflowService</span><span class="sxs-lookup"><span data-stu-id="07e65-102">Using the pairing cmdlet Register-SPWorkflowService</span></span>
<span data-ttu-id="07e65-103">Узнайте, как использовать командлет **Register-SPWorkflowService** успешно связать SharePoint с помощью диспетчера рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="07e65-103">Learn how to use the cmdlet **Register-SPWorkflowService** to successfully pair SharePoint with Workflow Manager.</span></span>
<span data-ttu-id="07e65-104">Установка и настройка Microsoft SharePoint для поддержки разработки рабочего процесса требуется «связывания» установок SharePoint и рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="07e65-104">Installing and configuring Microsoft SharePoint to support workflow development requires "pairing" your installations of SharePoint and Workflow Manager.</span></span> <span data-ttu-id="07e65-105">В большинстве случаев этот связывания легко выполняется с помощью командлета **Register-SPWorkflowService**, входящий в состав установки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07e65-105">In most scenarios, this pairing is easily done by using the cmdlet **Register-SPWorkflowService**, which is included with your SharePoint installation.</span></span>
  
    
    

<span data-ttu-id="07e65-p102">Важно этот командлет не полезен для каждой пары сценария. **Register-SPWorkflowService** можно использовать только в следующих сценариях связывания:</span><span class="sxs-lookup"><span data-stu-id="07e65-p102">Importantly, this cmdlet is not useful for every pairing scenario. **Register-SPWorkflowService** is useful only in the following pairing scenarios:</span></span>
- <span data-ttu-id="07e65-108">Ферма серверов один компьютер, где SharePoint и рабочих процессов совместное размещение на сервере.</span><span class="sxs-lookup"><span data-stu-id="07e65-108">One-computer server farm where SharePoint and Workflow Manager are co-located on the server box.</span></span>
    
  
- <span data-ttu-id="07e65-109">Ферма серверов три компьютера, где SharePoint и рабочих процессов совместное размещение на всех трех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="07e65-109">Three-computer server farm where SharePoint and Workflow Manager are co-located on all three computers.</span></span> <span data-ttu-id="07e65-110">(Добавить четвертый компьютер потребностей поиска должна находиться на отдельном компьютере и высокой ДОСТУПНОСТИ диспетчера рабочих процессов является обязательным.</span><span class="sxs-lookup"><span data-stu-id="07e65-110">(Add a fourth computer is search needs to be on a separate computer and Workflow Manager HA is required.</span></span> <span data-ttu-id="07e65-111">Если второй является обязательным, его следует установить на всех трех компьютерах.</span><span class="sxs-lookup"><span data-stu-id="07e65-111">If the latter is required, it must be installed on all three machines.</span></span>
    
  
- <span data-ttu-id="07e65-112">Три компьютера фермы SharePoint в сочетании с фермы серверов не находится уведомлений диспетчера рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="07e65-112">Three-computer SharePoint farm paired with a non-co-located Workflow Manager server farm.</span></span>
    
  
<span data-ttu-id="07e65-113">Также Обратите внимание, что этот **Register-SPWorkflowService** используются учетные данные текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="07e65-113">Also note that **Register-SPWorkflowService** uses the credentials of the current user.</span></span>
## <a name="cmdlet-design"></a><span data-ttu-id="07e65-114">Командлет разработки</span><span class="sxs-lookup"><span data-stu-id="07e65-114">Cmdlet design</span></span>





|<span data-ttu-id="07e65-115">**Данные**</span><span class="sxs-lookup"><span data-stu-id="07e65-115">**Detail**</span></span>|<span data-ttu-id="07e65-116">**Описание**</span><span class="sxs-lookup"><span data-stu-id="07e65-116">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="07e65-117">Глагол</span><span class="sxs-lookup"><span data-stu-id="07e65-117">Verb</span></span>  <br/> |<span data-ttu-id="07e65-118">Регистрация</span><span class="sxs-lookup"><span data-stu-id="07e65-118">Register</span></span>  <br/> |
|<span data-ttu-id="07e65-119">Существительное</span><span class="sxs-lookup"><span data-stu-id="07e65-119">Noun</span></span>  <br/> |<span data-ttu-id="07e65-120">SPWorkflowService</span><span class="sxs-lookup"><span data-stu-id="07e65-120">SPWorkflowService</span></span>  <br/> |
|<span data-ttu-id="07e65-121">Описание</span><span class="sxs-lookup"><span data-stu-id="07e65-121">Description</span></span>  <br/> |<span data-ttu-id="07e65-p104">Работает в ферме sps15short с Workflow Manager фермы. Этот командлет необходимо выполнить один раз на каждой ферме. Перед запуском командлета, необходимо установить сертификат корневого центра сертификации в хранилище сертификатов компьютера и хранилища сертификатов SharePoint. Чтобы сделать это, используйте командлет **New-SPTrustedRootAuthority**. (См. инструкции ниже).</span><span class="sxs-lookup"><span data-stu-id="07e65-p104">Pairs a sps15short farm with a Workflow Manager farm. You must run this cmdlet once per farm. Before running the cmdlet, you must install root CA certificate in machine certificate store and SharePoint certificate store. To do this, use the cmdlet **New-SPTrustedRootAuthority**. (See instructions below.)  </span></span><br/> |
|<span data-ttu-id="07e65-127">Тип вывода</span><span class="sxs-lookup"><span data-stu-id="07e65-127">Output type</span></span>  <br/> |<span data-ttu-id="07e65-128">Нет.</span><span class="sxs-lookup"><span data-stu-id="07e65-128">None.</span></span>  <br/> |
|<span data-ttu-id="07e65-129">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="07e65-129">Syntax</span></span>  <br/> | `Register-SPWorkflowService -SPSite <URI or GUID representing an SPSite object> -WorkflowHostUri <workflow service endpoint URL> -ScopeName <string> [-PartitionMode] [-AllowOAuthHttp] [-Force]` <br/> |
   

## <a name="cmdlet-parameters"></a><span data-ttu-id="07e65-130">Параметры командлета</span><span class="sxs-lookup"><span data-stu-id="07e65-130">Cmdlet parameters</span></span>



|<span data-ttu-id="07e65-131">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="07e65-131">**Parameter**</span></span>|<span data-ttu-id="07e65-132">**Тип**</span><span class="sxs-lookup"><span data-stu-id="07e65-132">**Type**</span></span>|<span data-ttu-id="07e65-133">**Описание**</span><span class="sxs-lookup"><span data-stu-id="07e65-133">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="07e65-134">SPSite          (обязательный)</span><span class="sxs-lookup"><span data-stu-id="07e65-134">SPSite          (Required)</span></span>  <br/> |<span data-ttu-id="07e65-135">**SPSitePipeBind**</span><span class="sxs-lookup"><span data-stu-id="07e65-135">**SPSitePipeBind**</span></span> <br/> |<span data-ttu-id="07e65-p105">URL-адрес семейства веб-сайтов в ферме SharePoint Server, который выступает в качестве конечной точке связывания длительный. Сведения для связывания выводится из этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="07e65-p105">The URL of a long-lasting site collection on the SharePoint Server farm that serves as the pairing endpoint. Information for pairing is deduced from this URL.</span></span>  <br/> |
|<span data-ttu-id="07e65-138">WorkflowHostUri          (Required)</span><span class="sxs-lookup"><span data-stu-id="07e65-138">WorkflowHostUri          (Required)</span></span>  <br/> |<span data-ttu-id="07e65-139">Строка</span><span class="sxs-lookup"><span data-stu-id="07e65-139">String</span></span>  <br/> |<span data-ttu-id="07e65-p106">URL-адрес конечной точки Workflow Manager для связывания. Предоставляет узла рабочего процесса URI и номер порта.</span><span class="sxs-lookup"><span data-stu-id="07e65-p106">The URL of the Workflow Manager endpoint for the pairing. Provides the workflow host URI along with port number.</span></span>  <br/> |
|<span data-ttu-id="07e65-142">ScopeName</span><span class="sxs-lookup"><span data-stu-id="07e65-142">ScopeName</span></span>  <br/> |<span data-ttu-id="07e65-143">Строка</span><span class="sxs-lookup"><span data-stu-id="07e65-143">String</span></span>  <br/> |<span data-ttu-id="07e65-p107">Имя для использования службы рабочих процессов для идентификации парного SharePoint Server фермы. Значение по умолчанию  «SharePoint». Необходимо указать этот параметр, если связь нескольких фермах SharePoint в ферму Workflow Manager.</span><span class="sxs-lookup"><span data-stu-id="07e65-p107">The name to be used by the workflow service to identify the paired SharePoint Server farm. The default value is "SharePoint". You only need to specify this parameter if trying to pair multiple SharePoint farms to a Workflow Manager farm.</span></span>  <br/> |
|<span data-ttu-id="07e65-147">PartitionMode</span><span class="sxs-lookup"><span data-stu-id="07e65-147">PartitionMode</span></span>  <br/> |<span data-ttu-id="07e65-148">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="07e65-148">SwitchParameter</span></span>  <br/> |<span data-ttu-id="07e65-p108">Этот параметр используется только для фермы SharePoint несколькими клиентами. В режиме секционирования указан для службы SharePoint. Обратите внимание на то, что одним экземпляром нескольких клиентов можно создать в ферме SharePoint после выполнения этого командлета; Таким образом командлет не может вывести значение этого параметра неявно из существующих состояний в ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07e65-p108">Use this parameter only for multi-tenant SharePoint farm. The partition mode is specified per SharePoint service. Note that you can create multi-tenancy in a SharePoint farm after this cmdlet runs; therefore, the cmdlet cannot deduce this parameter value implicitly from the existing state of the SharePoint farm.</span></span>  <br/> |
|<span data-ttu-id="07e65-152">AllowOAuthHttp</span><span class="sxs-lookup"><span data-stu-id="07e65-152">AllowOAuthHttp</span></span>  <br/> |<span data-ttu-id="07e65-153">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="07e65-153">SwitchParameter</span></span>  <br/> |<span data-ttu-id="07e65-p109">Позволяет OAuth и метаданные exchange по протоколу HTTP. Эта функция особенно полезна при тестировании, но не в рабочий режим. Этот параметр используется только в том случае, если SharePoint настроен для поддержки HTTP. Нет необходимости настроить Workflow Manager на использование протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="07e65-p109">Enables OAuth and metadata exchange over HTTP. This is useful in testing, but not in production mode. Use this only when SharePoint is configured to support HTTP. It is not necessary that the Workflow Manager be configured to use HTTP.</span></span>  <br/> |
|<span data-ttu-id="07e65-158">Force</span><span class="sxs-lookup"><span data-stu-id="07e65-158">Force</span></span>  <br/> |<span data-ttu-id="07e65-159">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="07e65-159">SwitchParameter</span></span>  <br/> |<span data-ttu-id="07e65-p110">Обеспечивает создание области с использованием параметра  _ScopeName_ или обновляет соответствующие же _ScopeName_существующей области. Если не указан, а область с таким же именем существует, командлета возникает ошибка. </span><span class="sxs-lookup"><span data-stu-id="07e65-p110">Enforces the creating of scope using  _ScopeName_ parameter, or updates an existing scope corresponding to the same _ScopeName_. If not specified and scope with the same name exists, the cmdlet will throw an error.  </span></span><br/> |
   

## <a name="example"></a><span data-ttu-id="07e65-162">Пример</span><span class="sxs-lookup"><span data-stu-id="07e65-162">Example</span></span>


```

PS> Register-SPWorkflowService -SPSite "https://myserver/mysitecollection" -WorkflowHostUri "http://workflow.example.com:12291" -ScopeName "SharePoint2" -PartitionMode -AllowOAuthHttp  -Force
```


## <a name="additional-resources"></a><span data-ttu-id="07e65-163">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="07e65-163">Additional resources</span></span>
<span data-ttu-id="07e65-164"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="07e65-164"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="07e65-165">Установка и настройка рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e65-165">Install and configure workflow for SharePoint</span></span>](http://technet.microsoft.com/en-us/library/jj658588.aspx)
    
  
-  [<span data-ttu-id="07e65-166">Серия: Установка и настройка рабочего процесса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="07e65-166">Video series: Install and configure Workflow in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/dn201724.aspx)
    
  
-  [<span data-ttu-id="07e65-167">Диспетчер рабочих процессов версии 1.0</span><span class="sxs-lookup"><span data-stu-id="07e65-167">Workflow Manager 1.0</span></span>](http://msdn.microsoft.com/en-us/library/jj193528%28Azure.10%29)
    
  
