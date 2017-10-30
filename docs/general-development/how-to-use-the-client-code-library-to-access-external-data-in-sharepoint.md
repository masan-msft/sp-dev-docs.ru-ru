---
title: "Как использовать клиентскую библиотеку кода для доступа к внешним данным в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c280ae92-c52b-4658-b0f3-805fb215ef8e
ms.openlocfilehash: 33d7be96c78828dc657331876ff03fb72f02c044
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-the-client-code-library-to-access-external-data-in-sharepoint"></a>Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint
Сведения об использовании клиентской объектной модели SharePoint для работы с объектами Business Connectivity Services (BCS) в SharePoint с использованием сценариев на основе браузера.
В этой статье показано, как настроить внешний список, который получает данные из источника Open Data protocol (OData) с помощью клиентской объектной модели в SharePoint.
  
    
    


## <a name="prerequisites-for-accessing-external-data-using-the-sharepoint-client-object-model"></a>Необходимые условия для доступа к внешним данным с помощью клиентской объектной модели SharePoint
<a name="bkmk_Prerequisites"> </a>

Ниже приведены требования к возможности разработки приложений с использованием клиентской объектной модели SharePoint.
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
- Работает среды разработки SharePoint надстройки: следуйте инструкциям в [настроить среду разработки, общие для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
    
  
- Доступ к общедоступной поставщики OData.org
    
  

### <a name="core-concepts-to-know-when-accessing-external-data-with-the-sharepoint-client-object-model"></a>Основные понятия, которые необходимо знать при доступе к внешним данным с помощью клиентской объектной модели SharePoint

Клиентская объектная модель SharePoint предоставляет способ доступа к внешним данным с помощью клиентских вызовов, которые копируют интерфейсов API на сервере. Чтобы понять, как это работает и как его использовать, обратитесь к статьям в таблице 1.
  
    
    

**В таблице 1. Основные понятия, которые по использованию клиентской объектной модели**


|**Статья**|**Описание**|
|:-----|:-----|
| [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |Узнайте, как писать код выполните основные операции с клиента SharePoint .NET Framework объектной модели (CSOM).  <br/> |
   

## <a name="create-an-sharepoint-add-in-to-access-external-data-using-the-client-object-model"></a>Создание Надстройка SharePoint для доступа к внешним данным с помощью клиентской объектной модели
<a name="bkmk_CreateApp"> </a>

Следующих процедурах показано, как настроить Надстройка SharePoint и настройка веб-страницы мог выполнять запросы, с помощью метода объектной модели клиента и объектов для извлечения данных из внешнего источника данных.
  
    
    

### <a name="to-create-an-sharepoint-add-in"></a>Создание Надстройка SharePoint


1. Откройте Visual Studio 2012.
    
  
2. Создайте проект **приложения для SharePoint** .
    
  
3. Укажите параметры приложения, включая имя приложения, URL-адрес сайта для отладки приложения, и как будут размещены приложения (автоматическим размещением, размещением у поставщика, размещенных в SharePoint). Дополнительные сведения о параметры размещения можно  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx).
    
  
4. Нажмите кнопку **Готово** для создания приложения.
    
  

### <a name="to-generate-the-external-content-type"></a>Для создания внешнего типа контента


1. В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.
    
  
2. В мастере **Укажите источника OData** введите URL-адрес службы OData, чтобы подключиться к. В этом случае будет использоваться источника Northwind OData, опубликованные в [http://www.odata.org/ecosystem](http://www.odata.org/ecosystem). Задать URL-адрес для службы OData  `http://services.odata.org/Northwind/Northwind.svc/`
    
    Укажите имя для источника данных и нажмите кнопку **Далее**.
    
  
3. Появится список сущностей, предоставляемые интерфейсом службы OData. Выберите сущности **клиентов**. Убедитесь, что установлен флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**.
    
  
4. Нажмите кнопку **Готово**.
    
  

## <a name="code-example-add-scripts-and-html-to-the-defaultaspx-page"></a>Пример кода: Добавление скриптов и HTML-код на страницу Default.aspx
<a name="bkmk_AddUIelements"> </a>

На этом этапе у вас есть внешнего типа контента и внешний список, который отображает данные из источника Netflix OData. 
  
    
    
Далее цель  это изменение страницы default.aspx, созданный при создании приложения. Добавить контейнер, который будет использоваться для хранения результатов запроса, который выполняется с помощью загрузки страницы. Выполнение сценариев на события загрузки страницы, позволяет гарантировать, что скрипт будет выполняться каждый раз при просмотре страницы, а полученные вызовы объектной модели клиента будет создан источник Netflix OData для добавления записей на страницу. 
  
    
    

### <a name="to-add-the-container-to-the-defaultaspx-page"></a>Чтобы добавить в контейнер на страницу Default.aspx


1. В **Обозревателе решений** откройте страницу Default.aspx, расположенной в модуле **страниц**.
    
  
2. Добавьте следующий элемент **div** на страницу:
    
```HTML
  
<div id="displayDiv"></div>
```

3. Сохраните страницу.
    
  
И, наконец добавьте код в файл App.js, который выполняется при загрузке страницы.
  
    
    

### <a name="to-modify-the-appjs-file-to-make-client-object-model-calls"></a>Чтобы изменить файл App.js для облегчения клиента вызывает объектной модели


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
<a name="bkmk_Addresources"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [BCS клиента Справочник по объектной модели для SharePoint](bcs-client-object-model-reference-for-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  

