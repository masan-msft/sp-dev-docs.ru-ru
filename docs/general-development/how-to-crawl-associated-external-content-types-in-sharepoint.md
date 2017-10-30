---
title: "Выполнение обхода связанных внешних типов контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 187ec42e-f749-4e22-abef-1df604143063
ms.openlocfilehash: 492c481703b7bb16a4c709d65f1698a06e024ded
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-crawl-associated-external-content-types-in-sharepoint"></a>Как: обход связанных внешних типов контента в SharePoint
В этой статье описывается использование свойств, имеющих отношение к поиску, в модели метаданных Служба подключения к бизнес-данным (BDC) для обхода связей, а также различные взаимодействия с пользователем, которые можно задействовать.
## <a name="crawling-the-associated-external-content-type"></a>Обход связанного внешнего типа контента
<a name="HowToCrawlAssociations_CrawlingAssociatedExternalTypes"> </a>

Службы Microsoft Business Connectivity Services (BCS) позволяет связать два связанных внешних типов контента, который затем позволяет извлечь связанные внешнего контента. Например внешнее содержимое можно извлечь из двух SQL Server базы данных на основе таблицы внешних типов контента, основанных на внешних ключей. Эта концепция компоновки два связанных внешних типов контента, называется  *связь*  . Дополнительные сведения о сопоставлениях [Добавление связей между внешними типами контента](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx)см. 
  
    
    
В контексте инфраструктурой соединителя Поиск внешнего типа контента источника ассоциации называется родительский тип внешнего контента. Программа-обходчик Поиск может выполнять обход внешних типов контента, связанные с родительской двумя способами: как вложения или дочерние элементы. Эти связей между типами внешнего контента повлиять на следующее:
  
    
    

- Взаимодействие с пользователем
    
  
- Добавочные обходы контента
    
  
- Обработка удалений обхода контента
    
  

### <a name="user-experience-effects-from-external-content-type-associations"></a>Влияние связей внешнего типа контента на взаимодействие с пользователем

Дочерний внешний тип контента имеет собственный URL-адрес страницы результатов поиска и страницу профиля (если она создана). URL-адрес страницы результатов поиска  это URL-адрес, который отображается, если пользователь выполняет поиск термина в данных дочернего внешнего типа контента. 
  
    
    
Внешний тип контента для вложения не имеет собственного URL-адреса страницы результатов поиска. Поэтому, если пользователь выполняет поиск термина во внешнем элементе вложения, отображается URL-адрес родительского внешнего типа контента. Этот URL-адрес можно задать для URL-адреса страницы профиля родительского типа. Страница профиля родительского внешнего типа контента будет отображать все поля из внешнего типа контента вложения, предоставленные навигатором связей.
  
    
    

### <a name="incremental-crawl-effects-from-external-content-type-associations"></a>Влияние связей внешнего типа контента на добавочный обход контента

Дочерних внешних элементов повторный обход и обновляются на основе временных меток добавочных обходов, при изменении отметки времени родительского внешнего элемента. 
  
    
    
Для внешних типов контента вложения отметка времени родительского внешнего элемента интерпретируется как отметка времени внешнего элемента вложения. Это значит, что изменения во внешнем элементе вложения собираются добавочным обходом контента только при изменении отметки времени родительского внешнего элемента.
  
    
    

### <a name="processing-crawl-deletions-effects-from-external-content-type-associations"></a>Влияние связей внешнего типа контента на обработку удалений обхода контента

При обработке удалений обхода контента, если родительский тип внешнего контента удаляется из индекса, программа-обходчик Поиск удаляет вложения связанных внешних типов контента и дочерние внешние типы контента из индекса.
  
    
    

## <a name="crawling-associated-external-content-type-attachments"></a>Обход вложений связанного внешнего типа контента
<a name="HowToCrawlAssociations_CrawlingAttachments"> </a>

Чтобы отметить связь для обхода в качестве вложения, добавьте свойство **AttachmentAccessor** в экземпляр метода **Association**, как показано ниже.
  
    
    

```XML

<Association Name="AttachmentsNavigate Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="ForeignFieldMappings" Type="System.String">....... </Property>
        <Property Name="AttachmentAccessor" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="AttachmentExternalContentType" Name="Attachment External Content Type" />
</Association>
```


> **Примечание:** Можно задать любое значение для свойства **AttachmentAccessor** ; Поиск не проверяет это значение.
  
    
    


## <a name="crawling-associated-external-content-types-as-child-external-content-types"></a>Обход связанных внешних типов контента в качестве дочерних внешних типов контента
<a name="HowToCrawlAssociations_CrawlingChildExternalTypes"> </a>

Чтобы отметить связь для обхода в качестве дочернего внешнего типа контента, добавьте свойство **DirectoryLink** в экземпляр метода **Association**, как показано ниже.
  
    
    

```XML

<Association Name="ChildrenNavigator Association" Type="AssociationNavigator" ...>
    <Properties>
        <Property Name="DirectoryLink" Type="System.String">x</Property>
    </Properties>
    <SourceEntity Namespace="ParentExternalContentType" Name="Parent" />
    <DestinationEntity Namespace="ChildExternalContentType" Name="Child External Content Type" />
</Association>
```


> **Примечание:** Можно задать любое значение для свойства **DirectoryLink** . Поиск не проверяет это значение.
  
    
    


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15crawlects_addlresources"> </a>


-  [Инфраструктура соединителей поиска в SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Добавление связей между внешними типами контента](http://msdn.microsoft.com/library/791e95ab-9b3c-413b-be12-bd0e59962c93%28Office.15%29.aspx)
    
  
-  [Элемент Association в элементе MethodInstances (схемы BDCMetadata)](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)
    
  
-  [Step 4 (Optional): Define Associations](http://msdn.microsoft.com/library/6bc55f46-459a-4986-8744-8c6c5f45097b%28Office.15%29.aspx)
    
  

