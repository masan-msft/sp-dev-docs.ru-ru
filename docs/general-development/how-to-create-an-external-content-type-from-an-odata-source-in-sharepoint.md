---
title: "Создание внешнего типа контента из источника OData в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bc60ea49-c44e-4531-af62-06b8cf77d35d
ms.openlocfilehash: 9ddf00811e05fcca25b4c4f406ac22ce5de9aca0
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-an-external-content-type-from-an-odata-source-in-sharepoint"></a>Создание внешнего типа контента из источника OData в SharePoint

Узнайте, как использовать Visual Studio 2012 для обнаружения опубликованного источника OData и создать для повторного использования внешний тип контента для использования в Business Connectivity Services (BCS) в SharePoint.

## <a name="prerequisites-for-creating-odata-based-external-content-types"></a>Необходимые условия для создания на основе OData внешних типов контента
<a name="bkmk_Prerequisites"> </a>

Чтобы создать внешний тип контента из источника Open Data protocol (OData), необходимо следующее:
  
    
    

- Экземпляр SharePoint
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- Опубликованные службы OData, доступные через Интернет
    
  
Сведения о настройке среды разработки SharePoint см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

> **Примечание:** SharePoint Designer 2013 не может использоваться для моделей BDC автоматически заполнять из источника OData. Вместо этого можно использовать Visual Studio 2012. 
  
    
    


### <a name="core-concepts-for-working-with-odata-external-content-types"></a>Основные понятия, которые для работы с внешними типами контента OData

В следующих статьях представлены общие сведения о OData и соединитель OData в SharePoint.
  
    
    

**В таблице 1. Основные понятия, которые OData внешних типов контента**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |Начало работы с Создание внешних типов контента на основе источников OData и узнайте, как использовать эти данные в SharePoint или Office компонентов.  <br/> |
| [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md) <br/> |Сведения о внешних типов контента службы BCS и что необходимо для их создания в SharePoint.  <br/> |
   

## <a name="create-an-odata-based-external-content-type"></a>Создание на основе OData внешнего типа контента
<a name="bkmk_CreatingODataECT"> </a>

Далее показано, как использовать Visual Studio 2012 для создания внешнего типа контента на основе источника OData.
  
    
    

### <a name="to-create-a-new-sharepoint-add-in"></a>Чтобы создать новый Надстройка SharePoint


1. В Visual Studio 2012 создайте новый проект **приложения для SharePoint,** расположенный в узле **шаблона SharePoint** .
    
  
2. Назовите проект и нажмите **кнопку ОК**.
    
  
3. Чтобы настроить параметры SharePoint, введите имя для вашего приложения и URL-адрес сервера SharePoint, которые вам будет находиться в режиме отладки от.
    
  
4. Нажмите кнопку **Готово**.
    
  
После создания проекта можно использовать новые автоматическое формирование, создание для источников OData и добавьте модели BDC для источника OData для вашего приложения.
  
    
    

### <a name="to-add-a-new-bdc-model"></a>Добавление новой модели BDC


1. В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.
    
    Будет запущен мастер, который поможет обнаружить выбранного источника данных и создать модель BDC.
    
  
2. Первая страница мастера используется для сбора URL-адрес службы данных. На странице **Укажите источника OData** введите URL-адрес, который вы хотите подключиться к службы OData. URL-адрес должен выглядеть следующим образом: `http://services.odata.org/Northwind/Northwind.svc/`.
    
    > **Примечание:** Службы данных "Борей", который доступен в списке производители, найденные на [веб-сайт Open Data Protocol](http://www.odata.org/ecosystem#liveservices)будут отображаться. 
3. Выберите имя для источника OData и нажмите кнопку **Далее**.
    
  
4. Появится список сущностей данные, предоставляемые интерфейсом службы OData. Выберите один или несколько сущностей и нажмите кнопку **Готово**.
    
  

### <a name="to-view-the-structure-of-the-entities"></a>Чтобы просмотреть структуру сущностей


- Обратите внимание, что Visual Studio, создать новую папку с именем внешних типов контента. В этой папке можно найти вложенную папку с именем новый источник данных. При дальнейшей развернуть это, появится элемент, представляющий объект, который вы выбрали. Чтобы просмотреть графический список сущностей и их типы, откройте файл **внешнего типа контента**, который требуется просмотреть.
    
    XML-код сущности, можно также просмотреть, открыв файлы внешнего типа контента в редакторе XML.
    
  

## <a name="use-a-stream-accessor-for-the-odata-source"></a>Использование доступа к данным потока для источника OData
<a name="bkmk_UseStreamAccessor"> </a>

Путем добавления следующего кода можно получить доступ к потоку данных, можно использовать соединитель OData.
  
    
    

```cs

/*Invoke  Stream Accessor Method */
        internal void ExecuteStreamAccessorMethod(IEntityInstance entityInstance, string streamAccessorName)
        {
            this.Log.Comment("ExecuteStreamAccessorMethod enter");
            this.Log.Comment("streamAccesor method" + streamAccessorName);
            IStreamableField isf = entityInstance.GetStreamableField(streamAccessorName);
            Stream resStream = isf.GetData();
            using (BinaryReader reader = new BinaryReader(resStream))
            {
                using (FileStream fs = File.Create(@"C:\\" + entityInstance.GetIdentity().GetIdentifierValues()[0] + ".jpg"))
                {
                    int bytesRead = 0;
                    do
                    {
                        int nrBytes = 80 * 1000 * 1000;
                        byte[] streamData = new byte[nrBytes];
                        bytesRead = reader.Read(streamData, 0, nrBytes);
                        this.Log.Comment("Total Bytes Read - " + bytesRead);
                        if (bytesRead > 0)
                        {
                            fs.Write(streamData, 0, bytesRead);
                        }
                    } while (bytesRead > 0);
                }
            }
            isf.Dispose();
            this.Log.Comment("ExecuteStreamAccessorMethod Exit" );
        }
```


## <a name="next-steps"></a>Дальнейшие действия
<a name="bkmk_Next"> </a>

После создания внешнего типа контента его можно использовать на предоставление данных в SharePoint с помощью встроенных объектов (внешние списки, веб-части Business данных или пользовательский код).
  
    
    
Дополнительные сведения можно [как: Создание внешнего списка с помощью источника данных OData в SharePoint](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_Addres"> </a>


-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  

