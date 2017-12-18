---
title: "Синхронизация терминов групп образец надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 4d78f316ad42639db4e8932515c574d867d421fc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="synchronize-term-groups-sample-add-in-for-sharepoint"></a><span data-ttu-id="b9428-102">Синхронизация терминов групп образец надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9428-102">Synchronize term groups sample add-in for SharePoint</span></span>

<span data-ttu-id="b9428-103">В рамках стратегии Enterprise Content Management (ECM) можно синхронизировать групп терминов через несколько банков терминов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b9428-103">As part of your Enterprise Content Management (ECM) strategy, you can synchronize term groups across multiple SharePoint term stores.</span></span>
    
<span data-ttu-id="b9428-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="b9428-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="b9428-105">Пример [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) показано, как использовать размещение у поставщика в надстройке для синхронизации исходной и целевой таксономии.</span><span class="sxs-lookup"><span data-stu-id="b9428-105">The [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) sample shows you how to use a provider-hosted add-in to synchronize a source and target taxonomy.</span></span> <span data-ttu-id="b9428-106">Эта надстройка синхронизирует двух банков терминов в службе управляемых метаданных - источника и конечного хранилище терминов.</span><span class="sxs-lookup"><span data-stu-id="b9428-106">This add-in synchronizes two term stores in the managed metadata service - a source and a target term store.</span></span> <span data-ttu-id="b9428-107">Синхронизация групп терминов используются следующие объекты:</span><span class="sxs-lookup"><span data-stu-id="b9428-107">The following objects are used to synchronize term groups:</span></span>

- <span data-ttu-id="b9428-108">**Банка терминов**</span><span class="sxs-lookup"><span data-stu-id="b9428-108">**TermStore**</span></span> 

- <span data-ttu-id="b9428-109">**ChangeInformation**</span><span class="sxs-lookup"><span data-stu-id="b9428-109">**ChangeInformation**</span></span> 

<span data-ttu-id="b9428-110">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="b9428-110">Use this solution if you want to:</span></span>

- <span data-ttu-id="b9428-111">Синхронизируйте две таксономии.</span><span class="sxs-lookup"><span data-stu-id="b9428-111">Synchronize two taxonomies.</span></span> <span data-ttu-id="b9428-112">Например SharePoint Online и SharePoint Server 2013 в локальной можно использовать для различных наборов данных, но они используют же таксономии.</span><span class="sxs-lookup"><span data-stu-id="b9428-112">For example, you might use both SharePoint Online and SharePoint Server 2013 on-premises for different sets of data, but they use the same taxonomy.</span></span>
    
- <span data-ttu-id="b9428-113">Синхронизация изменений, внесенных в определенные термина группу.</span><span class="sxs-lookup"><span data-stu-id="b9428-113">Synchronize changes made to a specific term group only.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b9428-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b9428-114">Before you begin</span></span>
<span data-ttu-id="b9428-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="b9428-115"></span></span>

<span data-ttu-id="b9428-116">Чтобы начать работу, загрузите пример надстройки [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="b9428-116">To get started, download the  [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="b9428-117">Перед запуском этой надстройки необходимо разрешение на доступ к хранилищу терминов в службе управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="b9428-117">Before you run this add-in, you'll need permission to access the term store in the managed metadata service.</span></span> <span data-ttu-id="b9428-118">На рисунке 1 показано центра администрирования Office 365, в которых назначаются разрешения.</span><span class="sxs-lookup"><span data-stu-id="b9428-118">Figure 1 shows the Office 365 admin center where these permissions are assigned.</span></span>

<span data-ttu-id="b9428-119">**На рисунке 1. Предоставление разрешений на термин хранения в центре администрирования SharePoint**</span><span class="sxs-lookup"><span data-stu-id="b9428-119">**Figure 1. Assigning permissions to the term store in the SharePoint admin center**</span></span>

![Снимок экрана, показывающий администрирования SharePoint центра обработки, с хранилищем терминов поле поиска хранилища терминов таксономии и полях администраторов хранилища терминов с выделением.](media/93a19898-6ae2-4176-b030-2546f4c86c5c.png)

<span data-ttu-id="b9428-121">Назначение разрешений для хранилища терминов:</span><span class="sxs-lookup"><span data-stu-id="b9428-121">To assign permissions to the term store:</span></span>

1. <span data-ttu-id="b9428-122">В центре администрирования Office 365 выберите команду **хранилища терминов**.</span><span class="sxs-lookup"><span data-stu-id="b9428-122">From the Office 365 admin center, choose  **term store**.</span></span>
    
2. <span data-ttu-id="b9428-123">В **Банк ТЕРМИНОВ ТАКСОНОМИИ**выберите набор терминов, что необходимо назначить администратору.</span><span class="sxs-lookup"><span data-stu-id="b9428-123">In  **TAXONOMY TERM STORE**, choose the term set that you want to assign an administrator to.</span></span>
    
3. <span data-ttu-id="b9428-124">В группе **Администраторов хранилища терминов**введите учетная запись организации, который требует разрешений администратора для хранилища терминов.</span><span class="sxs-lookup"><span data-stu-id="b9428-124">In  **Term Store Administrators**, enter the organizational account that requires term store administrator permissions.</span></span>

## <a name="using-the-coremmssync-sample-app"></a><span data-ttu-id="b9428-125">Использование примера приложения Core.MMSSync</span><span class="sxs-lookup"><span data-stu-id="b9428-125">Using the Core.MMSSync sample app</span></span>
<span data-ttu-id="b9428-126"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="b9428-126"></span></span>

<span data-ttu-id="b9428-127">При запуске надстройки появится консольное приложение, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="b9428-127">When you start the add-in, you see a console application, as shown in Figure 2.</span></span> <span data-ttu-id="b9428-128">Будет предложено ввести следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="b9428-128">You are prompted to enter the following information:</span></span>

- <span data-ttu-id="b9428-129">URL-адрес центра администрирования Office 365, которая содержит банк терминов источника (это URL-адрес службы метаданных управляемого источника).</span><span class="sxs-lookup"><span data-stu-id="b9428-129">The URL of the Office 365 admin center that contains the source term store (this is the URL of the source managed metadata service).</span></span> <span data-ttu-id="b9428-130">Например можно ввести https://contososource-admin.sharepoint.com.</span><span class="sxs-lookup"><span data-stu-id="b9428-130">For example, you might enter https://contososource-admin.sharepoint.com.</span></span>
    
- <span data-ttu-id="b9428-131">Имя пользователя и пароль администратора банка терминов в качестве источника служба управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="b9428-131">The user name and password of a term store administrator on your source managed metadata service.</span></span>
    
- <span data-ttu-id="b9428-132">URL-адрес центра администрирования theOffice 365, которая содержит банк терминов конечного (это URL-адрес конечного MMS).</span><span class="sxs-lookup"><span data-stu-id="b9428-132">The URL of theOffice 365 admin center that contains the target term store (this is the URL of the target MMS).</span></span> <span data-ttu-id="b9428-133">Например можно ввести https://contosotarget-admin.sharepoint.com.</span><span class="sxs-lookup"><span data-stu-id="b9428-133">For example, you might enter https://contosotarget-admin.sharepoint.com.</span></span>
    
- <span data-ttu-id="b9428-134">Имя пользователя и пароль администратора банка терминов в целевую служба управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="b9428-134">The user name and password of a term store administrator on your target managed metadata service.</span></span>
    
- <span data-ttu-id="b9428-135">Тип операции, которую необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="b9428-135">The type of operation you want to perform.</span></span> <span data-ttu-id="b9428-136">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="b9428-136">You can either:</span></span>
    
    - <span data-ttu-id="b9428-137">Переместите группу терминов (сценарий 1) с помощью объекта **банка терминов** .</span><span class="sxs-lookup"><span data-stu-id="b9428-137">Move a term group (scenario 1) by using the  **TermStore** object.</span></span>
    
    - <span data-ttu-id="b9428-138">Процесс изменения (сценарий 2) с помощью объекта **ChangeInformation** .</span><span class="sxs-lookup"><span data-stu-id="b9428-138">Process changes (scenario 2) by using the  **ChangeInformation** object.</span></span>

<span data-ttu-id="b9428-139">**Важные**  Этот пример надстройки для работы с обоих SharePoint Online и SharePoint Server 2013 локально.</span><span class="sxs-lookup"><span data-stu-id="b9428-139">**Important**  This sample add-in works with both SharePoint Online and SharePoint Server 2013 on-premises.</span></span>

<span data-ttu-id="b9428-140">**На рисунке 2. Core.MMSSync консольного приложения**</span><span class="sxs-lookup"><span data-stu-id="b9428-140">**Figure 2. Core.MMSSync console application**</span></span>

![Снимок экрана консоли приложения запроса на ввод информации для ввода.](media/1ef0e4f4-6f79-46b0-83d3-bdf9d87ccad9.png)

<span data-ttu-id="b9428-142">После выбора сценария введите имя группы терминов, которые необходимо синхронизировать из источника к службе конечного управляемых метаданных, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="b9428-142">After you select your scenario, enter the name of the term group you want to synchronize from your source to your target managed metadata service, as shown in Figure 3.</span></span> <span data-ttu-id="b9428-143">Например можно ввести Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b9428-143">For example, you might enter Enterprise.</span></span>

<span data-ttu-id="b9428-144">**На рисунке 3. Термин групп в службе управляемых метаданных**</span><span class="sxs-lookup"><span data-stu-id="b9428-144">**Figure 3. Term groups in the managed metadata service**</span></span>

![Снимок экрана из списка раскрывающегося списка хранилища терминов таксономии.](media/5202fd88-4f2f-4b68-8083-165e6702bc86.png)
### <a name="scenario-1---move-term-group"></a><span data-ttu-id="b9428-146">Сценарий 1 — переместить группу терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-146">Scenario 1 - Move term group</span></span>

<span data-ttu-id="b9428-147">При выборе **Перемещение группы терминов**, необходимо ввести группу терминов, чтобы синхронизировать надстройки и затем вызывает метод **CopyNewTermGroups** в MMSSyncManager.cs.</span><span class="sxs-lookup"><span data-stu-id="b9428-147">When you select  **Move Term Group**, the add-in prompts you to enter a term group to synchronize and then calls the  **CopyNewTermGroups** method in MMSSyncManager.cs.</span></span> <span data-ttu-id="b9428-148">Затем **CopyNewTermGroups** производит следующие действия для копирования группы терминов из хранилища терминов источника для банка терминов конечного:</span><span class="sxs-lookup"><span data-stu-id="b9428-148">**CopyNewTermGroups** then does the following to copy a term group from the source term store to the target term store:</span></span>

1. <span data-ttu-id="b9428-149">Получает терминов исходного и конечного хранилища объектов.</span><span class="sxs-lookup"><span data-stu-id="b9428-149">Retrieves the source and target term store objects.</span></span>
    
2. <span data-ttu-id="b9428-150">Проверяет, что языки терминов исходной и целевой сохраняет совпадение.</span><span class="sxs-lookup"><span data-stu-id="b9428-150">Verifies that the languages of the source and target term stores match.</span></span> 
    
3. <span data-ttu-id="b9428-151">Проверяет, не существует в банке терминов целевой группе Источник терминов и копирует группе Источник терминов банк терминов целевой с помощью **CreateNewTargetTermGroup**.</span><span class="sxs-lookup"><span data-stu-id="b9428-151">Verifies that the source term group doesn't exist in the target term store, and then copies the source term group to the target term store by using  **CreateNewTargetTermGroup**.</span></span> 
    
<span data-ttu-id="b9428-152">Можно задать параметры _TermGroupExclusions_, _TermGroupToCopy_и _TermSetInclusions_ для фильтрации, будут обработаны, какие слова.</span><span class="sxs-lookup"><span data-stu-id="b9428-152">You can set the  _TermGroupExclusions_,  _TermGroupToCopy_, and  _TermSetInclusions_ parameters to filter which terms get processed.</span></span>

<span data-ttu-id="b9428-153">В следующем коде показан методы **CopyNewTermGroups** и **CreateNewTargetTermGroup** в MMSSyncManager.cs.</span><span class="sxs-lookup"><span data-stu-id="b9428-153">The following code shows the  **CopyNewTermGroups** and **CreateNewTargetTermGroup** methods in MMSSyncManager.cs.</span></span>

> [!NOTE] 
> <span data-ttu-id="b9428-154">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="b9428-154">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public bool CopyNewTermGroups(ClientContext sourceContext, ClientContext targetContext, List<string> termGroupExclusions = null, string termGroupToCopy = null)
        {
            TermStore sourceTermStore = GetTermStoreObject(sourceContext);
            TermStore targetTermStore = GetTermStoreObject(targetContext);

            
            List<int> languagesToProcess = null;
            if (!ValidTermStoreLanguages(sourceTermStore, targetTermStore, out languagesToProcess))
            {
                Log.Internal.TraceError((int)EventId.LanguageMismatch, "The target termstore default language is not available as language in the source term store, syncing cannot proceed.");
                return false;
            }

            // Get a list of term groups to process. Exclude site collection-scoped groups and system groups.
            IEnumerable<TermGroup> termGroups = sourceContext.LoadQuery(sourceTermStore.Groups.Include(g => g.Name,
                                                                                                       g => g.Id,
                                                                                                       g => g.IsSiteCollectionGroup,
                                                                                                       g => g.IsSystemGroup))
                                                                                              .Where(g => g.IsSystemGroup == false &amp;&amp; g.IsSiteCollectionGroup == false);
            sourceContext.ExecuteQuery();

            foreach (TermGroup termGroup in termGroups)
            {
                // Skip term group if you only want to copy one particular term group.
                if (!String.IsNullOrEmpty(termGroupToCopy))
                {
                    if (!termGroup.Name.Equals(termGroupToCopy, StringComparison.InvariantCultureIgnoreCase))
                    {
                        continue;
                    }
                }

                // Skip term groups that you do not want to copy.
                if (termGroupExclusions != null &amp;&amp; termGroupExclusions.Contains(termGroup.Name, StringComparer.InvariantCultureIgnoreCase))
                {
                    Log.Internal.TraceInformation((int)EventId.CopyTermGroup_Skip, "Skipping {0} as this is a system termgroup", termGroup.Name);
                    continue;
                }

                // About to start copying a term group.
                TermGroup sourceTermGroup = GetTermGroup(sourceContext, sourceTermStore, termGroup.Name);
                TermGroup targetTermGroup = GetTermGroup(targetContext, targetTermStore, termGroup.Name);

                if (sourceTermGroup == null)
                {
                    continue;
                }
                if (targetTermGroup != null)
                {
                    if (sourceTermGroup.Id != targetTermGroup.Id)
                    {
                        // Term group exists with a different ID, unable to sync.
                        Log.Internal.TraceWarning((int)EventId.CopyTermGroup_IDMismatch, "The term groups have different ID's. I don't know how to work it.");
                    }
                    else
                    {
                        // Do nothing as this term group was previously copied. Term group changes need to be 
                        // picked up by the change log processing.
                        Log.Internal.TraceInformation((int)EventId.CopyTermGroup_AlreadyCopied, "Termgroup {0} was already copied...changes to it will need to come from changelog processing.", termGroup.Name);
                    }
                }
                else
                {
                    Log.Internal.TraceInformation((int)EventId.CopyTermGroup_Copying, "Copying termgroup {0}...", termGroup.Name);
                    this.CreateNewTargetTermGroup(sourceContext, targetContext, sourceTermGroup, targetTermStore, languagesToProcess);
                }
            }

            return true;
        }



private void CreateNewTargetTermGroup(ClientContext sourceClientContext, ClientContext targetClientContext, TermGroup sourceTermGroup, TermStore targetTermStore, List<int> languagesToProcess)
        {
            TermGroup destinationTermGroup = targetTermStore.CreateGroup(sourceTermGroup.Name, sourceTermGroup.Id);
            if (!string.IsNullOrEmpty(sourceTermGroup.Description))
            {
                destinationTermGroup.Description = sourceTermGroup.Description;
            }

            TermSetCollection sourceTermSetCollection = sourceTermGroup.TermSets;
            if (sourceTermSetCollection.Count > 0)
            {
                foreach (TermSet sourceTermSet in sourceTermSetCollection)
                {
                    sourceClientContext.Load(sourceTermSet,
                                              set => set.Name,
                                              set => set.Description,
                                              set => set.Id,
                                              set => set.Contact,
                                              set => set.CustomProperties,
                                              set => set.IsAvailableForTagging,
                                              set => set.IsOpenForTermCreation,
                                              set => set.CustomProperties,
                                              set => set.Terms.Include(
                                                        term => term.Name,
                                                        term => term.Description,
                                                        term => term.Id,
                                                        term => term.IsAvailableForTagging,
                                                        term => term.LocalCustomProperties,
                                                        term => term.CustomProperties,
                                                        term => term.IsDeprecated,
                                                        term => term.Labels.Include(label => label.Value, label => label.Language, label => label.IsDefaultForLanguage)));

                    sourceClientContext.ExecuteQuery();

                    TermSet targetTermSet = destinationTermGroup.CreateTermSet(sourceTermSet.Name, sourceTermSet.Id, targetTermStore.DefaultLanguage);
                    targetClientContext.Load(targetTermSet, set => set.CustomProperties);
                    targetClientContext.ExecuteQuery();
                    UpdateTermSet(sourceClientContext, targetClientContext, sourceTermSet, targetTermSet);

                    foreach (Term sourceTerm in sourceTermSet.Terms)
                    {
                        Term reusedTerm = targetTermStore.GetTerm(sourceTerm.Id);
                        targetClientContext.Load(reusedTerm);
                        targetClientContext.ExecuteQuery();

                        Term targetTerm;
                        if (reusedTerm.ServerObjectIsNull.Value)
                        {
                            try
                            {
                                targetTerm = targetTermSet.CreateTerm(sourceTerm.Name, targetTermStore.DefaultLanguage, sourceTerm.Id);
                                targetClientContext.Load(targetTerm, term => term.IsDeprecated,
                                                                     term => term.CustomProperties,
                                                                     term => term.LocalCustomProperties);
                                targetClientContext.ExecuteQuery();
                                UpdateTerm(sourceClientContext, targetClientContext, sourceTerm, targetTerm, languagesToProcess);
                            }
                            catch (ServerException ex)
                            {
                                if (ex.Message.IndexOf("Failed to read from or write to database. Refresh and try again.") > -1)
                                {
                                    // This exception was due to caching issues and generally is thrown when terms are reused across groups.
                                    targetTerm = targetTermSet.ReuseTerm(reusedTerm, false);
                                }
                                else
                                {
                                    throw ex;
                                }
                            }
                        }
                        else
                        {
                            targetTerm = targetTermSet.ReuseTerm(reusedTerm, false);
                        }

                        targetClientContext.Load(targetTerm);
                        targetClientContext.ExecuteQuery();

                        targetTermStore.UpdateCache();

                        // Refresh session and term store references to force reload of the term just added. You need 
                        // to do this because there can be an update change event following next, and if you don't,
                        // the newly created term set cannot be obtained from the server.
                        targetTermStore = GetTermStoreObject(targetClientContext);

                        // Recursively add the other terms.
                        ProcessSubTerms(sourceClientContext, targetClientContext, targetTermSet, targetTerm, sourceTerm, languagesToProcess, targetTermStore.DefaultLanguage);
                    }
                }
            }
            targetClientContext.ExecuteQuery();
        }

```

### <a name="scenario-2---process-changes"></a><span data-ttu-id="b9428-155">Сценарий 2 — процесс изменения</span><span class="sxs-lookup"><span data-stu-id="b9428-155">Scenario 2 - Process changes</span></span>

<span data-ttu-id="b9428-156">При выборе **Изменения процесса**надстройки предлагается ввести группу терминов для синхронизации, а затем вызывает метод **ProcessChanges** в MMSSyncManager.cs.</span><span class="sxs-lookup"><span data-stu-id="b9428-156">When you select  **Process Changes**, the add-in prompts you to enter a Term Group to synchronize, and then calls the  **ProcessChanges** method in MMSSyncManager.cs.</span></span> <span data-ttu-id="b9428-157">**ProcessChanges** используется метод **GetChanges** класса **ChangedInformation** для получения все изменения, внесенные в группы, наборы терминов и термины в службе источника управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="b9428-157">**ProcessChanges** uses the **GetChanges** method of the **ChangedInformation** class to retrieve all changes made to groups, term sets, and terms in the source managed metadata service.</span></span> <span data-ttu-id="b9428-158">Затем изменения применяются к службе конечного управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="b9428-158">Changes are then applied to the target managed metadata service.</span></span>

> [!NOTE] 
> <span data-ttu-id="b9428-159">Этот документ содержит только некоторые части метод **ProcessChanges** .</span><span class="sxs-lookup"><span data-stu-id="b9428-159">This document includes only some parts of the  **ProcessChanges** method.</span></span> <span data-ttu-id="b9428-160">Чтобы просмотреть весь метод, откройте решение Core.MMSSync в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9428-160">To review the entire method, open the Core.MMSSync solution in Visual Studio.</span></span>

<span data-ttu-id="b9428-161">Метод **ProcessChanges** начинается с создания объект **TaxonomySession** .</span><span class="sxs-lookup"><span data-stu-id="b9428-161">The  **ProcessChanges** method starts by creating a **TaxonomySession** object.</span></span>

```C#
Log.Internal.TraceInformation((int)EventId.TaxonomySession_Open, "Opening the taxonomy session");
            TaxonomySession sourceTaxonomySession = TaxonomySession.GetTaxonomySession(sourceClientContext);
            TermStore sourceTermStore = sourceTaxonomySession.GetDefaultKeywordsTermStore();
            sourceClientContext.Load(sourceTermStore,
                                            store => store.Name,
                                            store => store.DefaultLanguage,
                                            store => store.Languages,
                                            store => store.Groups.Include(group => group.Name, group => group.Id));
            sourceClientContext.ExecuteQuery();

```

<span data-ttu-id="b9428-162">После этого он получает изменения, с помощью объекта **ChangeInformation** и установки дату начала объекта **ChangeInformation** .</span><span class="sxs-lookup"><span data-stu-id="b9428-162">Next, it retrieves changes by using the  **ChangeInformation** object, and setting the start date on the **ChangeInformation** object.</span></span> <span data-ttu-id="b9428-163">В этом примере извлекаются все изменения, внесенные в прошлом году.</span><span class="sxs-lookup"><span data-stu-id="b9428-163">This example retrieves all changes that were made within the last year.</span></span>

```C#
Log.Internal.TraceInformation((int)EventId.TermStore_GetChangeLog, "Reading the changes");
            ChangeInformation changeInformation = new ChangeInformation(sourceClientContext);
            changeInformation.StartTime = startFrom;
            ChangedItemCollection termStoreChanges = sourceTermStore.GetChanges(changeInformation);
            sourceClientContext.Load(termStoreChanges);
            sourceClientContext.ExecuteQuery();

```

<span data-ttu-id="b9428-164">Метод **GetChanges** возвращает **ChangedItemCollection**, который перечисляет все изменения, происходящие в банке терминов, как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="b9428-164">The  **GetChanges** method returns a **ChangedItemCollection**, which enumerates all changes occurring in the term store, as shown in the following code example.</span></span> <span data-ttu-id="b9428-165">Последней строке примера проверяет, была ли **ChangedItem** группа терминов.</span><span class="sxs-lookup"><span data-stu-id="b9428-165">The last line of the example checks to determine whether the  **ChangedItem** was a term group.</span></span> <span data-ttu-id="b9428-166">**ProcessChanges** включает код для выполнения следующего проверок на **ChangedItem** для наборов терминов и термины.</span><span class="sxs-lookup"><span data-stu-id="b9428-166">**ProcessChanges** includes code to perform similar checks on the **ChangedItem** for term sets and terms.</span></span>

```C#
foreach (ChangedItem _changeItem in termStoreChanges)
                {
                    
                    if (_changeItem.ChangedTime < startFrom)
                    {
                        Log.Internal.TraceVerbose((int)EventId.TermStore_SkipChangeLogEntry, "Skipping item {1} changed at {0}", _changeItem.ChangedTime, _changeItem.Id);
                        continue;
                    }

                    Log.Internal.TraceVerbose((int)EventId.TermStore_ProcessChangeLogEntry, "Processing item {1} changed at {0}. Operation = {2}, ItemType = {3}", _changeItem.ChangedTime, _changeItem.Id, _changeItem.Operation, _changeItem.ItemType);

                    #region Group changes
                    if (_changeItem.ItemType == ChangedItemType.Group)

```

<span data-ttu-id="b9428-167">Тип измененный элемент может быть группа терминов, набор терминов или терминов.</span><span class="sxs-lookup"><span data-stu-id="b9428-167">The changed item type might be a term group, term set, or term.</span></span> <span data-ttu-id="b9428-168">Каждый тип измененный элемент имеет разные операции, которые можно выполнить над ним.</span><span class="sxs-lookup"><span data-stu-id="b9428-168">Each changed item type has different operations you can perform on it.</span></span> <span data-ttu-id="b9428-169">В следующей таблице перечислены операции, которые можно выполнить для каждого типа измененный элемент.</span><span class="sxs-lookup"><span data-stu-id="b9428-169">The following table lists the operations that you can perform on each changed item type.</span></span> 

|<span data-ttu-id="b9428-170">Что изменилось?</span><span class="sxs-lookup"><span data-stu-id="b9428-170">What changed?</span></span> <span data-ttu-id="b9428-171">(ChangedItemType)</span><span class="sxs-lookup"><span data-stu-id="b9428-171">(ChangedItemType)</span></span> | <span data-ttu-id="b9428-172">Операции можно выполнить на тип измененный элемент (ChangedOperationType)</span><span class="sxs-lookup"><span data-stu-id="b9428-172">Operations you can perform on changed item type (ChangedOperationType)</span></span>|
|---|---|
|<span data-ttu-id="b9428-173">Group</span><span class="sxs-lookup"><span data-stu-id="b9428-173">Group</span></span>|<p><span data-ttu-id="b9428-174">Удаление группы</span><span class="sxs-lookup"><span data-stu-id="b9428-174">Delete group</span></span></p><p><span data-ttu-id="b9428-175">Добавление группы</span><span class="sxs-lookup"><span data-stu-id="b9428-175">Add group</span></span></p><p><span data-ttu-id="b9428-176">Изменение группы</span><span class="sxs-lookup"><span data-stu-id="b9428-176">Edit group</span></span>|
|<span data-ttu-id="b9428-177">TermSet</span><span class="sxs-lookup"><span data-stu-id="b9428-177">TermSet</span></span>|</p><span data-ttu-id="b9428-178">Удаление набора терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-178">Delete term set</span></span></p><p><span data-ttu-id="b9428-179">Переместить набор терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-179">Move term set</span></span></p><p><span data-ttu-id="b9428-180">Скопируйте набор терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-180">Copy term set</span></span></p><p><span data-ttu-id="b9428-181">Добавление набора терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-181">Add term set</span></span></p><p><span data-ttu-id="b9428-182">Изменение набора терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-182">Edit term set</span></span><p>|
|<span data-ttu-id="b9428-183">Термин</span><span class="sxs-lookup"><span data-stu-id="b9428-183">Term</span></span>|</p><span data-ttu-id="b9428-184">Удаление термина</span><span class="sxs-lookup"><span data-stu-id="b9428-184">Delete term</span></span></p><p><span data-ttu-id="b9428-185">Перемещение термина</span><span class="sxs-lookup"><span data-stu-id="b9428-185">Move term</span></span></p><p><span data-ttu-id="b9428-186">Скопируйте терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-186">Copy term</span></span></p><p><span data-ttu-id="b9428-187">Изменение пути терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-187">Path change term</span></span></p><p><span data-ttu-id="b9428-188">Объединение терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-188">Merge term</span></span></p><p><span data-ttu-id="b9428-189">Добавление терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-189">Add term</span></span></p><p><span data-ttu-id="b9428-190">Изменение терминов</span><span class="sxs-lookup"><span data-stu-id="b9428-190">Edit term</span></span><p>|

<span data-ttu-id="b9428-191">Следующий код демонстрирует операции удаления группы терминов был удален в службе источника управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="b9428-191">The following code shows how to perform a delete operation when a term group was deleted in the source managed metadata service.</span></span>

```C#
#region Delete group
                        if (_changeItem.Operation == ChangedOperationType.DeleteObject)
                        {
                            TermGroup targetTermGroup = targetTermStore.GetGroup(_changeItem.Id);
                            targetClientContext.Load(targetTermGroup, group => group.Name);
                            targetClientContext.ExecuteQuery();

                            if (!targetTermGroup.ServerObjectIsNull.Value)
                            {
                                if (termGroupExclusions == null || !termGroupExclusions.Contains(targetTermGroup.Name, StringComparer.InvariantCultureIgnoreCase))
                                {
                                    Log.Internal.TraceInformation((int)EventId.TermGroup_Delete, "Deleting group: {0}", targetTermGroup.Name);
                                    targetTermGroup.DeleteObject();
                                    targetClientContext.ExecuteQuery();
                                }
                            }
                        }
                        #endregion

```

## <a name="see-also"></a><span data-ttu-id="b9428-192">См. также</span><span class="sxs-lookup"><span data-stu-id="b9428-192">See also</span></span>
<span data-ttu-id="b9428-193"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b9428-193"></span></span>

-  [<span data-ttu-id="b9428-194">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="b9428-194">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="b9428-195">Пример OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="b9428-195">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
    
-  [<span data-ttu-id="b9428-196">Пример Core.MMS</span><span class="sxs-lookup"><span data-stu-id="b9428-196">Core.MMS sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
