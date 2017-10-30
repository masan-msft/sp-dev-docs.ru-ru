---
title: "Как создать добавить в пределах внешнего типа контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: de4b50a3-84da-48ce-9ba0-fe06571e52a8
ms.openlocfilehash: 385bec9d7904031dee03347afc83974da7c3b6a0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-an-add-in-scoped-external-content-type-in-sharepoint"></a>Как: создать добавить в пределах внешнего типа контента в SharePoint
Узнайте, как создать внешний тип контента, который можно устанавливать, защищать и использовать в Надстройка SharePoint.
## <a name="prerequisites-for-developing-add-in-scoped-external-content-types"></a>Предварительные требования для разработки добавьте в пределах внешних типов контента
<a name="bkmk_Prerequisites"> </a>

Для начала разработки добавьте в пределах внешних типов контента, необходимо следующее:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- Опубликованные службы OData, доступные через Интернет
    
  
Сведения о настройке среды разработки SharePoint видеть [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="create-an-add-in-scoped-external-content-type"></a>Создание добавить в пределах внешнего типа контента
<a name="bkmk_CreateECT"> </a>

Далее показано, как создать внешний тип контента на основе источника Open Data protocol (OData) и изменить его ограничиваться вашей Надстройка SharePoint.
  
    
    

### <a name="to-create-a-new-sharepoint-add-in"></a>Чтобы создать новый Надстройка SharePoint


1. Откройте Visual Studio 2012.
    
  
2. Создайте проект **надстройки для SharePoint** .
    
  
3. Укажите параметры надстроек, включая имя, URL-адрес сайта для отладки надстройки и способ для размещения надстройки (автоматическим размещением, размещением у поставщика или размещением в SharePoint). Для получения дополнительных сведений см  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
    
  
4. Нажмите кнопку **Готово**, чтобы создать приложение.
    
  
Для завершения действия по созданию Надстройки SharePoint см.:
  
    
    

-  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](http://msdn.microsoft.com/library/3038dd73-41ee-436f-8c78-ef8e6869bf7b%28Office.15%29.aspx)
    
  
-  [Инструкции. Создание базового приложения с автоматическим размещением для SharePoint](http://msdn.microsoft.com/library/0572894d-c437-4b7d-8ac6-8405496e2145%28Office.15%29.aspx)
    
  
-  [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](http://msdn.microsoft.com/library/1b992485-6efe-4ea4-a18c-221689b0b66f%28Office.15%29.aspx)
    
  

### <a name="to-generate-the-external-content-type"></a>Для создания внешнего типа контента


1. В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.
    
    Будет запущен мастер, которая поможет вам найти выбранного источника данных и создать модель BDC.
    
  
2. На странице **Настройка источника OData** введите URL-адрес, который вы хотите подключиться к службы OData. URL-адрес должен выглядеть примерно следующим образом: `http://services.odata.org/Northwind/Northwind.svc/`.
    
    Укажите имя для источника OData.
    
    > **Примечание:** В данном примере необходимо использовать службы данных "Борей", который доступен в списке производители, расположенный на [веб-сайт Open Data Protocol](http://www.odata.org). 
3. Появится список сущностей отображение данных, предоставляемые интерфейсом службы OData. Выберите один или несколько сущностей и нажмите кнопку **Готово**.
    
  

### <a name="to-deploy-the-add-in-scoped-external-content-type"></a>Чтобы развернуть добавить в пределах внешнего типа контента


- Нажмите клавишу F5, чтобы скомпилировать и передача файлов проекта SharePoint.
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Добавьте в пределах внешних типов контента в SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  

