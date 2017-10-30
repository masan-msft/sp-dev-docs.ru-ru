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
# <a name="managed-metadata-and-navigation-in-sharepoint"></a>Управляемые метаданные и навигация в SharePoint

  
    
    
![Раздел концептуального обзора](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
Сведения о корпоративных управляемых метаданных (EMM) и возможности навигации в SharePoint.
## <a name="managed-metadata-feature-enhancements-in-sharepoint-for-developers"></a>Управляемые метаданные усовершенствований в SharePoint для разработчиков (en)
<a name="SP15_ManagedMetadataAndNav_ManagedMetadataFeatureEnhancements"> </a>

Управляемые метаданные можно использовать для создания тегов стратегии, которые соответствуют подробные бизнес-требованиям и таксономии. В SharePoint набор основных управляемых метаданных API были развернуты и предоставляет дополнительные возможности и сценарии поддержки.
  
    
    

## <a name="net-client-object-model-csom-support-for-managed-metadata-apis"></a>Поддержка .NET клиентской объектной модели (CSOM) для управляемых метаданных API-интерфейсы
<a name="SP15_ManagedMetadataAndNav_CSOMSupport"> </a>

SharePoint CSOM поддерживает настройки таксономии и разработки. Таксономия доступна в клиент .NET (CSOM), Silverlight и JavaScript, модели программирования. Разработка с помощью его логически похожа на разработку с помощью модели программирования .NET server. Может быть полезно для разработки решений CSOM для поддержки сценариев, где чтение содержимого — это чаще, чем разработки или администрирование его. Чтобы разрешить использование таксономии в облаке сценарий, как SharePoint Online или для подмножества сценариев, доступных на локальном необходимо CSOM.
  
    
    
Создание нового CSOM проекта в Visual Studio, использующего функциональные возможности таксономии, необходимо задайте следующие ссылки:
  
    
    

- Microsoft.SharePoint.Client.dll
    
  
- Microsoft.SharePoint.Client.Runtime.dll
    
  
- Microsoft.SharePoint.Client.Taxonomy.dll
    
  
Разработка настроек с помощью CSOM очень похоже на разработке .NET server таксономии решений: получите ссылку на объект **TaxonomySession** и **TermStore** объектов, **Group** объекты, объекты **TermSet** и **Term** объекты, необходимые для сеанса.
  
    
    

### <a name="code-examples-basic-operations-with-the-taxonomy-csom"></a>Примеры кода: Основные операции с CSOM таксономии
<a name="SP15_ManagedMetadataAndNav_ExampleBasicOperations"> </a>

В следующих примерах кода можно использовать для выполнения базовых операций с таксономии CSOM. В первом примере создается объект **Group**, **TermSet** и **Term** объекты. Во втором примере выполняется итерация для объекта **Group** и записывает его содержимого.
  
    
    

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


  
    
    

## <a name="pinning"></a>Закрепление
<a name="SP15_ManagedMetadataAndNav_Pinning"> </a>

В Microsoft SharePoint Server 2010 пользователи могли бы повторно использовать условия (и всех вложенных в повторно используемую условия) в другие расположения в иерархии терминов. После того как эти термины, которые использовались повторно, они могут быть изменены и изменения будут видны везде термины, которые использовались повторно. SharePoint представляется фиксации терминов. Закрепленные терминов — так же, как условие, которое используется повторно, за исключением того, как он доступен только для чтения и не может изменяться в местах, где повторно использовать термин. Пример приведен [как: задает использовать код с условиями ПИН-кода для терминов навигации в SharePoint](how-to-use-code-to-pin-terms-to-navigation-term-sets-in-sharepoint.md).
  
    
    

  
    
    

## <a name="datasheet-view-support-for-managed-metadata-column-types"></a>Поддержка представление таблицы данных для управляемых метаданных приведены типы столбцов
<a name="SP15_ManagedMetadataAndNav_DatasheetViewSupport"> </a>

В SharePoint была изменена функций представления таблицы данных. Теперь таблицы использует дважды щелкните действие для открытия стандартного представления для редактирования сетки. Теперь можно изменить столбцы метаданных с помощью функции, доступные при изменении отдельных элементов. Этот компонент включает доступ в набор терминов, который находится за столбец. Этот компонент предназначен для объединения метаданных изменения функциональные возможности, доступные при изменении отдельного элемента в режим редактирования таблицы данных.
  
    
    

## <a name="managed-navigation"></a>Управляемая навигация
<a name="SP15_ManagedMetadataAndNav_ManagedNav"> </a>

Управляемая Навигация использует управляемых метаданных функции, такие как возможность элементы тега с условиями терминов и управление ими в банке терминов для обеспечения настраиваемых навигации. Структурированная навигация, который зависит от инфраструктуры SharePoint по-прежнему также доступен в SharePoint.
  
    
    

## <a name="friendly-urls"></a>Понятные URL-адреса
<a name="SP15_ManagedMetadataAndNav_FriendlyURLs"> </a>

Понятные URL-адреса  это короткий формат URL-адреса, отображаемые в адресной строке большинство публикации страницы, включая начальная страница сайта SharePoint. Они являются Оптимизированных для поисковых систем и отображаться в результатах поиска. 
  
    
    

## <a name="support-for-new-scenarios"></a>Поддержка новые сценарии
<a name="SP15_ManagedMetadataAndNav_SupportForNewScenarios"> </a>

Диспетчер банка терминов можно повысить уровень и разверните узел терминов модели использования на основании более гибкой и мощные функциональные возможности управляемых метаданных в :
  
    
    

- Ссылка на другой семейства сайтов и просмотр терминов других пользователей. Если вы хотите сделать наборе доступными для других семейств веб-сайтов, подключенных к службе управляемых метаданных, создайте **global term set**. Если вы хотите создать закрытый терминов, доступен только для определенного семейства сайтов, сохраненное в службе управляемых метаданных, создайте **local term set**. 
    
  
- Запретить пользователям использовать ключевые слова за пределами набор определенных терминов.
    
  
- Получить дополнительные многоязыковой поддержки, включая поддержку автоматического перевода и гибкие LCID. 
    
  

## <a name="unsupported-scenarios-for-working-with-custom-site-definitions"></a>Неподдерживаемые сценарии для работы с пользовательских определений сайтов
<a name="SP15_ManagedMetadataAndNav_UnsupportedScenarios"> </a>


- SharePoint не поддерживает создание таксономии поля (столбцы сайта управляемые метаданные) декларативно путем получения XML-определение.
    
  
- SharePoint не поддерживает использование таксономии поля (столбцы управляемых метаданных сайта) в шаблоны сайтов.
    
  
- Для получения дополнительных сведений см Microsoft поддержки статье #898631:  [поддерживаемые и неподдерживаемые сценарии](http://support2.microsoft.com/default.aspx?scid=kb;EN-US;898631
)
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_ManagedMetadataAndNav_AdditionalResources"> </a>


-  [Управляемой навигации в SharePoint](managed-navigation-in-sharepoint.md)
    
  
-  [Веб-часть поиска контента в SharePoint](content-search-web-part-in-sharepoint.md)
    
  

