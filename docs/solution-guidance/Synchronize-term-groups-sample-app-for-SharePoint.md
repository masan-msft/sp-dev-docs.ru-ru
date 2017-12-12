---
title: "Синхронизация терминов групп образец надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 4d78f316ad42639db4e8932515c574d867d421fc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="synchronize-term-groups-sample-add-in-for-sharepoint"></a>Синхронизация терминов групп образец надстройки для SharePoint

В рамках стратегии Enterprise Content Management (ECM) можно синхронизировать групп терминов через несколько банков терминов SharePoint.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Пример [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) показано, как использовать размещение у поставщика в надстройке для синхронизации исходной и целевой таксономии. Эта надстройка синхронизирует двух банков терминов в службе управляемых метаданных - источника и конечного хранилище терминов. Синхронизация групп терминов используются следующие объекты:

- **Банка терминов** 

- **ChangeInformation** 

Если вы хотите используйте этого решения:

- Синхронизируйте две таксономии. Например SharePoint Online и SharePoint Server 2013 в локальной можно использовать для различных наборов данных, но они используют же таксономии.
    
- Синхронизация изменений, внесенных в определенные термина группу.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Перед запуском этой надстройки необходимо разрешение на доступ к хранилищу терминов в службе управляемых метаданных. На рисунке 1 показано центра администрирования Office 365, в которых назначаются разрешения.

**На рисунке 1. Предоставление разрешений на термин хранения в центре администрирования SharePoint**

![Снимок экрана, показывающий администрирования SharePoint центра обработки, с хранилищем терминов поле поиска хранилища терминов таксономии и полях администраторов хранилища терминов с выделением.](media/93a19898-6ae2-4176-b030-2546f4c86c5c.png)

Назначение разрешений для хранилища терминов:

1. В центре администрирования Office 365 выберите команду **хранилища терминов**.
    
2. В **Банк ТЕРМИНОВ ТАКСОНОМИИ**выберите набор терминов, что необходимо назначить администратору.
    
3. В группе **Администраторов хранилища терминов**введите учетная запись организации, который требует разрешений администратора для хранилища терминов.

## <a name="using-the-coremmssync-sample-app"></a>Использование примера приложения Core.MMSSync
<a name="sectionSection1"> </a>

При запуске надстройки появится консольное приложение, как показано на рисунке 2. Будет предложено ввести следующие сведения:

- URL-адрес центра администрирования Office 365, которая содержит банк терминов источника (это URL-адрес службы метаданных управляемого источника). Например можно ввести https://contososource-admin.sharepoint.com.
    
- Имя пользователя и пароль администратора банка терминов в качестве источника служба управляемых метаданных.
    
- URL-адрес центра администрирования theOffice 365, которая содержит банк терминов конечного (это URL-адрес конечного MMS). Например можно ввести https://contosotarget-admin.sharepoint.com.
    
- Имя пользователя и пароль администратора банка терминов в целевую служба управляемых метаданных.
    
- Тип операции, которую необходимо выполнить. Вы можете:
    
    - Переместите группу терминов (сценарий 1) с помощью объекта **банка терминов** .
    
    - Процесс изменения (сценарий 2) с помощью объекта **ChangeInformation** .

**Важные**  Этот пример надстройки для работы с обоих SharePoint Online и SharePoint Server 2013 локально.

**На рисунке 2. Core.MMSSync консольного приложения**

![Снимок экрана консоли приложения запроса на ввод информации для ввода.](media/1ef0e4f4-6f79-46b0-83d3-bdf9d87ccad9.png)

После выбора сценария введите имя группы терминов, которые необходимо синхронизировать из источника к службе конечного управляемых метаданных, как показано на рисунке 3. Например можно ввести Enterprise.

**На рисунке 3. Термин групп в службе управляемых метаданных**

![Снимок экрана из списка раскрывающегося списка хранилища терминов таксономии.](media/5202fd88-4f2f-4b68-8083-165e6702bc86.png)
### <a name="scenario-1---move-term-group"></a>Сценарий 1 — переместить группу терминов

При выборе **Перемещение группы терминов**, необходимо ввести группу терминов, чтобы синхронизировать надстройки и затем вызывает метод **CopyNewTermGroups** в MMSSyncManager.cs. Затем **CopyNewTermGroups** производит следующие действия для копирования группы терминов из хранилища терминов источника для банка терминов конечного:

1. Получает терминов исходного и конечного хранилища объектов.
    
2. Проверяет, что языки терминов исходной и целевой сохраняет совпадение. 
    
3. Проверяет, не существует в банке терминов целевой группе Источник терминов и копирует группе Источник терминов банк терминов целевой с помощью **CreateNewTargetTermGroup**. 
    
Можно задать параметры _TermGroupExclusions_, _TermGroupToCopy_и _TermSetInclusions_ для фильтрации, будут обработаны, какие слова.

В следующем коде показан методы **CopyNewTermGroups** и **CreateNewTargetTermGroup** в MMSSyncManager.cs.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

### <a name="scenario-2---process-changes"></a>Сценарий 2 — процесс изменения

При выборе **Изменения процесса**надстройки предлагается ввести группу терминов для синхронизации, а затем вызывает метод **ProcessChanges** в MMSSyncManager.cs. **ProcessChanges** используется метод **GetChanges** класса **ChangedInformation** для получения все изменения, внесенные в группы, наборы терминов и термины в службе источника управляемых метаданных. Затем изменения применяются к службе конечного управляемых метаданных.

> [!NOTE] 
> Этот документ содержит только некоторые части метод **ProcessChanges** . Чтобы просмотреть весь метод, откройте решение Core.MMSSync в Visual Studio.

Метод **ProcessChanges** начинается с создания объект **TaxonomySession** .

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

После этого он получает изменения, с помощью объекта **ChangeInformation** и установки дату начала объекта **ChangeInformation** . В этом примере извлекаются все изменения, внесенные в прошлом году.

```C#
Log.Internal.TraceInformation((int)EventId.TermStore_GetChangeLog, "Reading the changes");
            ChangeInformation changeInformation = new ChangeInformation(sourceClientContext);
            changeInformation.StartTime = startFrom;
            ChangedItemCollection termStoreChanges = sourceTermStore.GetChanges(changeInformation);
            sourceClientContext.Load(termStoreChanges);
            sourceClientContext.ExecuteQuery();

```

Метод **GetChanges** возвращает **ChangedItemCollection**, который перечисляет все изменения, происходящие в банке терминов, как показано в следующем примере кода. Последней строке примера проверяет, была ли **ChangedItem** группа терминов. **ProcessChanges** включает код для выполнения следующего проверок на **ChangedItem** для наборов терминов и термины.

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

Тип измененный элемент может быть группа терминов, набор терминов или терминов. Каждый тип измененный элемент имеет разные операции, которые можно выполнить над ним. В следующей таблице перечислены операции, которые можно выполнить для каждого типа измененный элемент. 

|Что изменилось? (ChangedItemType) | Операции можно выполнить на тип измененный элемент (ChangedOperationType)|
|---|---|
|Group|<p>Удаление группы</p><p>Добавление группы</p><p>Изменение группы|
|TermSet|</p>Удаление набора терминов</p><p>Переместить набор терминов</p><p>Скопируйте набор терминов</p><p>Добавление набора терминов</p><p>Изменение набора терминов<p>|
|Термин|</p>Удаление термина</p><p>Перемещение термина</p><p>Скопируйте терминов</p><p>Изменение пути терминов</p><p>Объединение терминов</p><p>Добавление терминов</p><p>Изменение терминов<p>|

Следующий код демонстрирует операции удаления группы терминов был удален в службе источника управляемых метаданных.

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Пример OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core)
    
-  [Пример Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
