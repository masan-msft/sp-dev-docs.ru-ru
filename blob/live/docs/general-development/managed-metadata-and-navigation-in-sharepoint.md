---
title: "Управляемые метаданные и навигация в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e
ms.openlocfilehash: e4b5453894cf03a93758157b5caa2e2f92208646
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="managed-metadata-and-navigation-in-sharepoint"></a><span data-ttu-id="b7a2e-102">Управляемые метаданные и навигация в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b7a2e-102">Managed metadata and navigation in SharePoint</span></span>

  
    
    
![Раздел концептуального обзора](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="b7a2e-104">Сведения о корпоративных управляемых метаданных (EMM) и возможности навигации в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-104">Learn about enterprise managed metadata (EMM) and navigation features in SharePoint.</span></span>
## <a name="managed-metadata-feature-enhancements-in-sharepoint-for-developers"></a><span data-ttu-id="b7a2e-105">Управляемые метаданные усовершенствований в SharePoint для разработчиков (en)</span><span class="sxs-lookup"><span data-stu-id="b7a2e-105">Managed metadata feature enhancements in SharePoint for developers</span></span>
<span data-ttu-id="b7a2e-106"><a name="SP15_ManagedMetadataAndNav_ManagedMetadataFeatureEnhancements"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-106"></span></span>

<span data-ttu-id="b7a2e-107">Управляемые метаданные можно использовать для создания тегов стратегии, которые соответствуют подробные бизнес-требованиям и таксономии.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-107">You can use managed metadata to build taxonomies and tagging strategies that meet specific, detailed business needs.</span></span> <span data-ttu-id="b7a2e-108">В SharePoint набор основных управляемых метаданных API были развернуты и предоставляет дополнительные возможности и сценарии поддержки.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-108">In SharePoint, the basic managed metadata API set is expanded and enhanced to provide more capabilities and scenario support.</span></span>
  
    
    

## <a name="net-client-object-model-csom-support-for-managed-metadata-apis"></a><span data-ttu-id="b7a2e-109">Поддержка .NET клиентской объектной модели (CSOM) для управляемых метаданных API-интерфейсы</span><span class="sxs-lookup"><span data-stu-id="b7a2e-109">.NET client object model (CSOM) support for managed metadata APIs</span></span>
<span data-ttu-id="b7a2e-110"><a name="SP15_ManagedMetadataAndNav_CSOMSupport"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-110"></span></span>

<span data-ttu-id="b7a2e-111">SharePoint CSOM поддерживает настройки таксономии и разработки.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-111">The SharePoint CSOM supports taxonomy customization and development.</span></span> <span data-ttu-id="b7a2e-112">Таксономия доступна в клиент .NET (CSOM), Silverlight и JavaScript, модели программирования.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-112">Taxonomy is available in .NET client (CSOM), Silverlight, and JavaScript programming models.</span></span> <span data-ttu-id="b7a2e-113">Разработка с помощью его логически похожа на разработку с помощью модели программирования .NET server.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-113">Developing with it is logically similar to developing with the .NET server programming model.</span></span> <span data-ttu-id="b7a2e-114">Может быть полезно для разработки решений CSOM для поддержки сценариев, где чтение содержимого — это чаще, чем разработки или администрирование его.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-114">You may find it useful to develop CSOM solutions to support scenarios where reading content is more common than authoring or administering it.</span></span> <span data-ttu-id="b7a2e-115">Чтобы разрешить использование таксономии в облаке сценарий, как SharePoint Online или для подмножества сценариев, доступных на локальном необходимо CSOM.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-115">You need to use CSOM to enable taxonomy use in a cloud scenario like SharePoint Online or for a subset of scenarios that are available on premises.</span></span>
  
    
    
<span data-ttu-id="b7a2e-116">Создание нового CSOM проекта в Visual Studio, использующего функциональные возможности таксономии, необходимо задайте следующие ссылки:</span><span class="sxs-lookup"><span data-stu-id="b7a2e-116">When you want to create a new CSOM project in Visual Studio that uses taxonomy functionality, set the following references:</span></span>
  
    
    

- <span data-ttu-id="b7a2e-117">Microsoft.SharePoint.Client.dll</span><span class="sxs-lookup"><span data-stu-id="b7a2e-117">Microsoft.SharePoint.Client.dll</span></span>
    
  
- <span data-ttu-id="b7a2e-118">Microsoft.SharePoint.Client.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="b7a2e-118">Microsoft.SharePoint.Client.Runtime.dll</span></span>
    
  
- <span data-ttu-id="b7a2e-119">Microsoft.SharePoint.Client.Taxonomy.dll</span><span class="sxs-lookup"><span data-stu-id="b7a2e-119">Microsoft.SharePoint.Client.Taxonomy.dll</span></span>
    
  
<span data-ttu-id="b7a2e-120">Разработка настроек с помощью CSOM очень похоже на разработке .NET server таксономии решений: получите ссылку на объект **TaxonomySession** и **TermStore** объектов, **Group** объекты, объекты **TermSet** и **Term** объекты, необходимые для сеанса.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-120">Developing customizations with CSOM is very similar to developing .NET server taxonomy solutions: get a reference to the **TaxonomySession** object and the **TermStore** object, **Group** objects, **TermSet** objects, and **Term** objects required for the session.</span></span>
  
    
    

### <a name="code-examples-basic-operations-with-the-taxonomy-csom"></a><span data-ttu-id="b7a2e-121">Примеры кода: Основные операции с CSOM таксономии</span><span class="sxs-lookup"><span data-stu-id="b7a2e-121">Code Examples: Basic operations with the Taxonomy CSOM</span></span>
<span data-ttu-id="b7a2e-122"><a name="SP15_ManagedMetadataAndNav_ExampleBasicOperations"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-122"></span></span>

<span data-ttu-id="b7a2e-p103">В следующих примерах кода можно использовать для выполнения базовых операций с таксономии CSOM. В первом примере создается объект **Group**, **TermSet** и **Term** объекты. Во втором примере выполняется итерация для объекта **Group** и записывает его содержимого.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-p103">You can use the following code examples to complete basic operations with the taxonomy CSOM. The first example creates a **Group** object, a **TermSet** object, and **Term** objects. The second example iterates on a **Group** object and writes its contents.</span></span>
  
    
    

```cs

       private void CreateColorsTermSet(string siteUrl)
        {
           ClientContext clientContext = new ClientContext(siteUrl);
 
           TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(clientContext);
            clientContext.Load(taxonomySession,
                ts => ts.TermStores.Include(
                    store => store.Name,
                    store => store.Groups.Include(
                        group => group.Name
                        )
                    )
                );
            clientContext.ExecuteQuery();
 
           if( taxonomySession != null )
            {
               TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
               if (termStore != null)
                {
                   //
                   //  Create group, termset, and terms.
                   //
                   TermGroup myGroup = termStore.CreateGroup("MyGroup",Guid.NewGuid());
                   TermSet myTermSet = myGroup.CreateTermSet("Color",Guid.NewGuid(), 1033);
                    myTermSet.CreateTerm("Red", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Orange", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Yellow", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Green", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Blue", 1033,Guid.NewGuid());
                    myTermSet.CreateTerm("Purple", 1033,Guid.NewGuid());
 
                    clientContext.ExecuteQuery();
                }
            }
        }
 
       private void DumpTaxonomyItems(string siteUrl)
        {
           ClientContext clientContext = new ClientContext(siteUrl);
 
           //
           // Load up the taxonomy item names.
           //
            TaxonomySession taxonomySession =TaxonomySession.GetTaxonomySession(clientContext);
           TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
            clientContext.Load(termStore,
                    store => store.Name,
                    store => store.Groups.Include(
                        group => group.Name,
                        group => group.TermSets.Include(
                            termSet => termSet.Name,
                            termSet => termSet.Terms.Include(
                                term => term.Name)
                        )
                    )
            );
            clientContext.ExecuteQuery();
 
 
           //
           //Writes the taxonomy item names.
           //
           if( taxonomySession != null )
            {
               if (termStore != null)
                {
                   foreach( TermGroup groupin termStore.Groups)
                    {
                       Console.WriteLine("Group " + group.Name);
 
                       foreach( TermSet termSetin group.TermSets )
                        {
                           Console.WriteLine("TermSet " + termSet.Name);
 
                            foreach(Term term in termSet.Terms)
                            {
                               //Writes root-level terms only.
                               Console.WriteLine("Term " + term.Name);
                            }
                        }
                    }
                }
            }
 
        }

```


  
    
    

## <a name="pinning"></a><span data-ttu-id="b7a2e-126">Закрепление</span><span class="sxs-lookup"><span data-stu-id="b7a2e-126">Pinning</span></span>
<span data-ttu-id="b7a2e-127"><a name="SP15_ManagedMetadataAndNav_Pinning"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-127"></span></span>

<span data-ttu-id="b7a2e-128">В Microsoft SharePoint Server 2010 пользователи могли бы повторно использовать условия (и всех вложенных в повторно используемую условия) в другие расположения в иерархии терминов.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-128">In Microsoft SharePoint Server 2010, users could reuse terms (and all terms nested under the reused terms) in other locations in the term hierarchy.</span></span> <span data-ttu-id="b7a2e-129">После того как эти термины, которые использовались повторно, они могут быть изменены и изменения будут видны везде термины, которые использовались повторно.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-129">After these terms were reused, they could be modified and changes would be seen everywhere the terms were reused.</span></span> <span data-ttu-id="b7a2e-130">SharePoint представляется фиксации терминов.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-130">SharePoint introduces term pinning.</span></span> <span data-ttu-id="b7a2e-131">Закрепленные терминов — так же, как условие, которое используется повторно, за исключением того, как он доступен только для чтения и не может изменяться в местах, где повторно использовать термин.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-131">A pinned term is just like a term that is reused, except it is read only and cannot be changed in the locations where the term is reused.</span></span> <span data-ttu-id="b7a2e-132">Пример приведен [как: задает использовать код с условиями ПИН-кода для терминов навигации в SharePoint](how-to-use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="b7a2e-132">For an example, see  [How to: Use code to pin terms to navigation term sets in SharePoint](how-to-use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint.md).</span></span>
  
    
    

  
    
    

## <a name="datasheet-view-support-for-managed-metadata-column-types"></a><span data-ttu-id="b7a2e-133">Поддержка представление таблицы данных для управляемых метаданных приведены типы столбцов</span><span class="sxs-lookup"><span data-stu-id="b7a2e-133">Datasheet view support for managed metadata column types</span></span>
<span data-ttu-id="b7a2e-134"><a name="SP15_ManagedMetadataAndNav_DatasheetViewSupport"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-134"></span></span>

<span data-ttu-id="b7a2e-135">В SharePoint была изменена функций представления таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-135">In SharePoint, the datasheet view functionality has changed.</span></span> <span data-ttu-id="b7a2e-136">Теперь таблицы использует дважды щелкните действие для открытия стандартного представления для редактирования сетки.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-136">Now, the datasheet uses a double-click action to open standard view for grid editing.</span></span> <span data-ttu-id="b7a2e-137">Теперь можно изменить столбцы метаданных с помощью функции, доступные при изменении отдельных элементов.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-137">You can now edit metadata columns using the same features that are available when you edit individual items.</span></span> <span data-ttu-id="b7a2e-138">Этот компонент включает доступ в набор терминов, который находится за столбец.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-138">This includes access to the term set that is behind the column.</span></span> <span data-ttu-id="b7a2e-139">Этот компонент предназначен для объединения метаданных изменения функциональные возможности, доступные при изменении отдельного элемента в режим редактирования таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-139">This feature is all about bringing the metadata modification functionality available when editing an individual item to datasheet editing.</span></span>
  
    
    

## <a name="managed-navigation"></a><span data-ttu-id="b7a2e-140">Управляемая навигация</span><span class="sxs-lookup"><span data-stu-id="b7a2e-140">Managed navigation</span></span>
<span data-ttu-id="b7a2e-141"><a name="SP15_ManagedMetadataAndNav_ManagedNav"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-141"></span></span>

<span data-ttu-id="b7a2e-142">Управляемая Навигация использует управляемых метаданных функции, такие как возможность элементы тега с условиями терминов и управление ими в банке терминов для обеспечения настраиваемых навигации.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-142">Managed navigation uses managed metadata features, such as the ability to tag items with terms and manage terms in a term store, to provide highly customized site navigation.</span></span> <span data-ttu-id="b7a2e-143">Структурированная навигация, который зависит от инфраструктуры SharePoint по-прежнему также доступен в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-143">The structured navigation that depends on the SharePoint infrastructure is also still available in SharePoint.</span></span>
  
    
    

## <a name="friendly-urls"></a><span data-ttu-id="b7a2e-144">Понятные URL-адреса</span><span class="sxs-lookup"><span data-stu-id="b7a2e-144">Friendly URLs</span></span>
<span data-ttu-id="b7a2e-145"><a name="SP15_ManagedMetadataAndNav_FriendlyURLs"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-145"></span></span>

<span data-ttu-id="b7a2e-p107">Понятные URL-адреса  это короткий формат URL-адреса, отображаемые в адресной строке большинство публикации страницы, включая начальная страница сайта SharePoint. Они являются Оптимизированных для поисковых систем и отображаться в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-p107">Friendly URLs are a shorter URL format displayed in the address bar of most SharePoint publishing pages, including the Welcome Page of your site. They are SEO-friendly and appear in search results.</span></span> 
  
    
    

## <a name="support-for-new-scenarios"></a><span data-ttu-id="b7a2e-148">Поддержка новые сценарии</span><span class="sxs-lookup"><span data-stu-id="b7a2e-148">Support for new scenarios</span></span>
<span data-ttu-id="b7a2e-149"><a name="SP15_ManagedMetadataAndNav_SupportForNewScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-149"></span></span>

<span data-ttu-id="b7a2e-150">Диспетчер банка терминов можно повысить уровень и разверните узел терминов модели использования на основании более гибкой и мощные функциональные возможности управляемых метаданных в :</span><span class="sxs-lookup"><span data-stu-id="b7a2e-150">A term store manager can enhance and expand term usage models based on more flexible and powerful managed metadata functionality in :</span></span>
  
    
    

- <span data-ttu-id="b7a2e-p108">Ссылка на другой семейства сайтов и просмотр терминов других пользователей. Если вы хотите сделать наборе доступными для других семейств веб-сайтов, подключенных к службе управляемых метаданных, создайте **global term set**. Если вы хотите создать закрытый терминов, доступен только для определенного семейства сайтов, сохраненное в службе управляемых метаданных, создайте **local term set**.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-p108">Link to another site collection and view others' terms. If you want to make your term set available to other site collections connected to the managed metadata service, create a **global term set**. If you want to create a private term set that is available only to a specific site collection when it is stored in the managed metadata service, create a **local term set**.</span></span> 
    
  
- <span data-ttu-id="b7a2e-154">Запретить пользователям использовать ключевые слова за пределами набор определенных терминов.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-154">Block users from using keywords outside of a specific term set.</span></span>
    
  
- <span data-ttu-id="b7a2e-155">Получить дополнительные многоязыковой поддержки, включая поддержку автоматического перевода и гибкие LCID.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-155">Gain additional multilingual support, including support for automated translation and flexible LCIDs.</span></span> 
    
  

## <a name="unsupported-scenarios-for-working-with-custom-site-definitions"></a><span data-ttu-id="b7a2e-156">Неподдерживаемые сценарии для работы с пользовательских определений сайтов</span><span class="sxs-lookup"><span data-stu-id="b7a2e-156">Unsupported scenarios for working with custom site definitions</span></span>
<span data-ttu-id="b7a2e-157"><a name="SP15_ManagedMetadataAndNav_UnsupportedScenarios"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-157"></span></span>


- <span data-ttu-id="b7a2e-158">SharePoint не поддерживает создание таксономии поля (столбцы сайта управляемые метаданные) декларативно путем получения XML-определение.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-158">SharePoint does not support creating taxonomy fields (managed metadata site columns) declaratively by way of XML definition.</span></span>
    
  
- <span data-ttu-id="b7a2e-159">SharePoint не поддерживает использование таксономии поля (столбцы управляемых метаданных сайта) в шаблоны сайтов.</span><span class="sxs-lookup"><span data-stu-id="b7a2e-159">SharePoint does not support the use of taxonomy fields (managed metadata site columns) in site templates.</span></span>
    
  
- <span data-ttu-id="b7a2e-160">Для получения дополнительных сведений см Microsoft поддержки статье #898631:  [поддерживаемые и неподдерживаемые сценарии](http://support2.microsoft.com/default.aspx?scid=kb;EN-US;898631
)</span><span class="sxs-lookup"><span data-stu-id="b7a2e-160">For more information, see Microsoft Support Article #898631:  [Supported and unsupported scenarios](http://support2.microsoft.com/default.aspx?scid=kb;EN-US;898631
)</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="b7a2e-161">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b7a2e-161">Additional resources</span></span>
<span data-ttu-id="b7a2e-162"><a name="SP15_ManagedMetadataAndNav_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="b7a2e-162"></span></span>


-  [<span data-ttu-id="b7a2e-163">Управляемой навигации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b7a2e-163">Managed navigation in SharePoint</span></span>](managed-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b7a2e-164">Веб-часть поиска контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b7a2e-164">Content Search Web Part in SharePoint</span></span>](content-search-web-part-in-sharepoint.md)
    
  

