---
title: "Как создать внешний список с помощью источника данных OData в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 601fbfce-a0c6-43dd-8398-540d094c083c
ms.openlocfilehash: c0fe48ca9061d22f5aade9b3afbf15ba306f0ae0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint"></a>Как: Создание внешнего списка с помощью источника данных OData в SharePoint
Узнайте, как программно создать внешний список и привязать его к внешнему типу контента на основе OData в SharePoint.
Несмотря на то, что опытный пользователь или администратор SharePoint скорее всего будет создать внешний список с помощью SharePoint Designer 2013, разработчик будет интересовать возможность создания внешних списков с помощью средств их торговые разработчика Office и Visual Studio 2012 Средства Visual Studio 2012. Это обеспечивает большую гибкость для добавления функций и Упакуйте решение, которое включает функции Business Connectivity Services (BCS) для последующего развертывания в одну или многие размещения сред.
  
    
    


## <a name="prerequisites-for-creating-an-external-list"></a>Необходимые условия для создания внешнего списка
<a name="bkmk_Prereqs"> </a>

Создание внешнего списка из источника OData необходимы следующие компоненты:
  
    
    

- Visual Studio 2012
    
  
- SharePoint
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- A опубликовано внешнего типа контента на основе источника OData: сведения содержатся в разделе [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).
    
  
Сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="core-concepts-for-creating-external-lists"></a>Основные понятия, которые для создания внешних списков

В следующих статьях представлены сведения о Надстройки SharePoint и прочие сведения для создания внешних списков.
  
    
    

**В таблице 1. Основные понятия, которые для внешних списков**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md) <br/> |Сведения о службах Business Connectivity Services и того, как предоставлять внешних данных в SharePoint.  <br/> |
| [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Узнайте о новой модели приложения в SharePoint, которое позволяет создавать приложения, представляющие собой небольшие, простые в использовании решения для конечных пользователей.  <br/> |
| [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx) <br/> |Информация о различных способах размещения Надстройки SharePoint.  <br/> |
   

## <a name="create-a-new-external-list"></a>Создание нового внешнего списка
<a name="bkmk_CreateNewVList"> </a>

Ниже показано, как создать новый внешний список, привязки на основе внешнего типа контента и публикация в SharePoint с помощью Visual Studio 2012.
  
    
    

> **Примечание:** Первый шаг предполагается, что вы создали внешнего типа контента, как описано в статье [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md). 
  
    
    


### <a name="to-add-an-external-list-automatically"></a>Чтобы автоматически добавлять внешнего списка


1. Если требуется добавить простой список в проект, который отражает в внешний тип контента, можно использовать средства Автоматическое формирование Visual Studio 2012. Список создается при создании внешнего типа контента. При установите флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**, обнаруженных в второй этап процесса автоматическое формирование (Выбор шаг сущности данных), мастер создает XML-объявления и добавлять новые внешние типы контента для каждого элемента, который вы выбрали.
    
  
2. Нажмите клавишу F5, чтобы развернуть проект и новый список также развернуть.
    
  
В целях тестирования, может потребоваться изменить файл AppManifest.xml таким образом, чтобы начальная страница приложения  это список, который вы только что создали. 
  
    
    

### <a name="to-modify-the-appmanifestxml-file"></a>Изменение файла AppManifest.xml


1. Откройте файл AppManifest.xml, с помощью XML-редактора.
    
  
2. Найдите \<StartPage\> тег.
    
  
3. Измените значение на  `~appWebUrl/Lists/Employees`.
    
  
4. Сохраните изменения.
    
  

### <a name="to-publish-the-project"></a>Публикация проекта


- Нажмите клавишу F5, чтобы развернуть проект и внешнего списка. 
    
    Откройте веб-браузер и перейдите в созданный новый список.
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_AdditionalResources"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Инструкции. Создание базового приложения с автоматическим размещением для SharePoint](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)
    
  
-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  

