---
title: "Как получить доступ к внешним данным с помощью REST в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 0663cc8c-a736-434d-9858-6ce12ce7f748
ms.openlocfilehash: c2043eb097ba6b8db294737f413cf91dd2e7c8ab
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-access-external-data-with-rest-in-sharepoint"></a>Как: доступ к внешним данным с помощью REST в SharePoint
Узнайте, как получить доступ к внешним данным из SharePoint с помощью представлений состояния (REST) URL-адреса Business Connectivity Services (BCS).
В этой статье показано, как настроить внешний список, который получает данные из источника Open Data protocol (OData).
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-rest"></a>Необходимые условия для доступа к внешним данным использовать REST
<a name="bkmk_Prerequisites"> </a>

Для доступа к внешним данным из SharePoint с помощью REST, вам необходимо следующее:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- Работает среды разработки SharePoint надстройки: следуйте инструкциям в [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
    
  
- Доступ к общедоступной поставщики OData.org
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-rest"></a>Основные понятия, которые необходимо знать при доступе к внешним данным с помощью REST

Службы SharePoint REST предоставляет способ доступа к внешним данным с помощью специально созданного URL-адреса. Чтобы понять, как это работает и как его использовать, обратитесь к следующим документам.
  
    
    

**В таблице 1. Основные понятия, которые REST в SharePoint**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Программирование с использованием службы SharePoint 2013 REST](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx) <br/> |Узнайте, как использовать службы SharePoint REST, содержащей REST, интерфейс сравнимые существующей клиентской объектной модели программирования.  <br/> |
| [Знакомство со службой REST в SharePoint](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx) <br/> |Основы использования службы REST в SharePoint для чтения и изменения данных в SharePoint по веб-протоколам REST и OData.  <br/> |
| [С помощью службы SharePoint REST](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx) <br/> |Узнайте, как для перемещения по структуре данных SharePoint, представленным в службе REST, выполнять распространенные CRUD (Создание, чтение, обновление и удаление) операций для элементов SharePoint с помощью службы REST синхронизация элементов SharePoint в приложениях и управления параллелизм элемента.  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-rest"></a>Создание Надстройка SharePoint для доступа к внешним данным использовать REST
<a name="bkmk_CreateApp"> </a>

Следующие процедуры рекомендации по установке Надстройка SharePoint и настройке веб-страницы мог выполнять запросы, с помощью функции REST для извлечения данных из внешнего источника данных.
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a>Создание Надстройка SharePoint


1. Откройте Visual Studio 2012.
    
  
2. Создайте проект **приложения для SharePoint** .
    
  
3. Укажите параметры приложения, включая имя приложения, URL-адрес сайта для отладки приложения, и как будут размещены приложения (автоматическим размещением, размещением у поставщика, размещенных в SharePoint). Дополнительные сведения о параметры размещения можно  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
    
  
4. Нажмите кнопку **Готово**, чтобы создать приложение.
    
  

### <a name="to-generate-the-external-content-type"></a>Для создания внешнего типа контента


1. В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **Типы контента для внешнего источника данных**.
    
  
2. На странице **Указание источника OData** введите URL-адрес службы OData, который требуется подключение к. В этом случае используйте источника Northwind OData, опубликованные в [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Значение  `http://services.odata.org/Northwind/Northwind.svc/`URL-адрес для службы OData и укажите имя для источника данных.
    
    Нажмите кнопку **Далее**.
    
  
3. Эта команда выводит список сущностей данные, предоставляемые интерфейсом службы OData. Выберите лицо, **Клиенты**. Убедитесь, что установлен флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**.
    
  
4. Нажмите кнопку **Готово**.
    
  

## <a name="code-example-add-scripts-and-html-to-the-homeaspx-page"></a>Пример кода: Добавление скриптов и HTML-код страницы Home.aspx
<a name="bkmk_AddUIelements"> </a>

На этом этапе у вас есть внешнего типа контента и внешний список, который отображает данные из источника данных "Борей" OData. 
  
    
    
Далее основная задача заключается в том, чтобы изменить страницу default.aspx, созданную при создании приложения. Добавьте контейнер для хранения результатов запроса, который выполняется с помощью загрузки страницы. Выполнение сценариев на события загрузки страницы, убедитесь, что скрипт будет выполняться каждый раз при просмотре страницы, а полученные вызовы REST выполняются в источник данных "Борей" OData для добавления записей на страницу.
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a>Чтобы добавить в контейнер на страницу Default.aspx


1. В **Обозревателе решений** откройте страницу Default.aspx в модуле **страниц**.
    
  
2. Добавьте следующий элемент **div** на страницу.
    
```HTML
  
<div id="displayDiv"></div>
```

3. Сохраните страницу.
    
  
И, наконец добавьте код в файл App.js, который выполняется при загрузке страницы.
  
    
    

### <a name="to-modify-the-appjs-file-to-make-rest-calls"></a>Чтобы изменить файл App.js для выполнения вызовов REST


1. Откройте файл App.js в модуле сценариев проекта SharePoint.
    
  
2. Вставьте следующий код в конец файла.
    
```
  $(document).ready(function () {

    // Namespace
    window.AppLevelECT = window.AppLevelECT || {};

    // Constructor
    AppLevelECT.Grid = function (hostElement, surlWeb) {
        this.hostElement = hostElement;
        if (surlWeb.length > 0 &amp;&amp; surlWeb.substring(surlWeb.length - 1, surlWeb.length) != "/")
            surlWeb += "/";
        this.surlWeb = surlWeb;
    }

    // Prototype
    AppLevelECT.Grid.prototype = {

        init: function () {

            $.ajax({
                url: this.surlWeb + "_api/lists/getbytitle('Customer')/items?$select=BdcIdentity,CustomerID,ContactName",
                headers: {
                    "accept": "application/json",
                    "X-RequestDigest": $("#__REQUESTDIGEST").val()
                },
                success: this.showItems
            });
        },

        showItems: function (data) {
            var items = [];

            items.push("<table>");
            items.push('<tr><td>Customer ID</td><td>Customer Name</td></tr>');

            $.each(data.d.results, function (key, val) {
                items.push('<tr id="' + val.BdcIdentity + '"><td>' +
                    val.CustomerID + '</td><td>' +
                    val.ContactName + '</td></tr>');
            });

            items.push("</table>");

            $("#displayDiv").html(items.join(''));
        }
    }

    ExecuteOrDelayUntilScriptLoaded(getCustomers, "sp.js");
});

function getCustomers() {
    var grid = new AppLevelECT.Grid($("#displayDiv"), _spPageContextInfo.webServerRelativeUrl);
    grid.init();
}
```

Нажмите клавишу F5, чтобы развернуть приложение для SharePoint. Перейдите на страницу Default.aspx в приложении и на странице отображается список клиентов.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_Addres"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Знакомство со службой REST в SharePoint](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590%28Office.15%29.aspx)
    
  
-  [С помощью службы SharePoint REST](http://msdn.microsoft.com/library/e1ff2979-1c16-4cb0-a57e-9168dfe20a7c.aspx)
    
  
-  [Добавьте в пределах внешних типов контента в SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

