---
title: "Варианты хранения данных в SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 0e9264de4cb19e4f32939e02786611580d41c82d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="data-storage-options-in-sharepoint-online"></a>Варианты хранения данных в SharePoint Online

При разработке SharePoint Online надстроек, у вас есть несколько различных параметров для хранения данных. Ознакомьтесь с различиями между каждого варианта и сведения о преимущества использования удаленного хранилища, можно использовать образец кода, приведенный в данной статье. 

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

В этой статье описывается [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) примера приложения, в котором отображается каждого из следующие варианты хранения данных, а также их преимущества и недостатки каждого из них:

- Список SharePoint на хост-сайта
    
- Список SharePoint на сайте приложения
    
- Базы данных SQL Azure
    
- Хранилище Azure очередей
    
- Хранение таблицы Azure
    
- Внешние веб-службы
    
В примере приложения [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) — это размещение у поставщика приложений, написанных на языке C# и JavaScript, который развертывает несколько артефактов SharePoint (списки, веб-часть приложения, веб-части) на хост-сайта и сайта приложения. Взаимодействует со списками SharePoint на веб-приложения и веб-сайт, а также выполняет вызовы базы данных SQL Azure, очереди и таблицы хранилища Azure и удаленного веб-службы, который реализует OData. В этом примере используется шаблон Model-View-Controller (MVC).
В примере приложения [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) применяется каждого варианта хранилища данных определенные функции, для которого параметр отлично подходят, как описано в следующей таблице.

|Дополнительные варианты хранения примера приложения|Используется для|
|:--|:--|
|Веб-приложения списка SharePoint|Клиент notes|
|Веб-сайт для списка SharePoint|Поддержка случаев|
|Службы данных "Борей" OData|Клиенты|
|Хранение таблицы Azure|Оценки по обслуживанию Клиентов|
|Хранилище Azure очередей|Вызов очереди|
|Базы данных SQL Azure Northwind|Заказов, сведения о заказе продуктов|

Приложение реализует панель мониторинга обслуживания клиентов и соответствующие интерфейсы, которые отображают последних заказов, рейтинги пример опроса клиента, notes клиента, поддержка, а также очереди представитель звонков с клиента. Первые два сценария позволяют получить данные с помощью довольно просто кода объектной модели клиента или запросов REST, но ограничивается пороговые значения списка запросов. Следующие четыре сценарии используются различные типы удаленного хранилища. 

**На рисунке 1. Отображает запрос данных хранилища моделей начальная страница для развертывания компонентов SharePoint**

![Снимок экрана примера приложения пользовательского интерфейса](media/bb3b58ca-b983-4ec4-b36d-18a911edb5d5.png)

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Прежде чем использовать этот образец, убедитесь в том, что у вас есть следующие:

- Учетную запись Microsoft Azure можно развернуть базу данных SQL Azure и создать учетную запись хранилища Azure. 
    
- SharePoint для разработчиков веб-сайтов, чтобы можно развернуть образец из Visual Studio 2013.
    
Кроме того необходимо развернуть базы данных Northwind Microsoft Azure.

### <a name="to-deploy-the-northwind-database"></a>Развертывание базы данных "Борей"

1. Войдите в систему портала управления Azure и выбор **Базы данных SQL**> **серверов**.
    
2. Нажмите кнопку **Создать базу данных сервера SQL Server**.
    
3. В форме **Создания сервера** введите значения для **Имени для входа**, **Пароль для входа**и **области**, как показано на рисунке 2.
    
    **На рисунке 2. Параметры сервера базы данных SQL**

    ![Показывает параметры сервера базы данных SQL](media/7ae059fa-eecc-4446-8171-294e44acb189.png)

4. Нажмите кнопку флажок, чтобы закончить и создания сервера.
    
5. Теперь, когда вы создали базу данных, выберите имя сервера, который был создан, как показано на рисунке 3.
    
    **На рисунке 3. Имя сервера, на странице "серверы"**

    ![Отображает список баз данных SQL](media/a6b097e4-5ad2-47df-9e31-ac0d699efd76.png)

6. Выберите команду **НАСТРОИТЬ**и нажмите стрелку в нижнем правом углу, чтобы завершить настройку и выберите команду **Сохранить**.
    
7. Откройте SQL Server Management Studio на компьютере локального разработки и создать базу данных с именем **"Борей"**.
    
8. В **Обозревателе объектов**выберите базу данных **"Борей"** и выберите **Создать запрос**.
    
9. В текстовом редакторе почтой откройте скрипт SQL northwind.sql, предоставляемая с примером [Core.DataStorageModels](https://github.com/SharePoint/PnP/tree/master/Samples/Core.DataStorageModels) .
    
10. Скопируйте текст в файл northwind.sql и вставьте его в **окно запроса SQL** в SQL Server Management Studio и затем выберите команду **выполнить**.
    
11. В **Обозревателе объектов**откройте контекстное меню для базы данных **Northwind** (щелкните правой кнопкой), выберите **задачи**и выберите **Развернуть базу данных в SQL Azure**.
    
12. На экране **Введение** нажмите кнопку **Далее**.
    
13. Выберите **подключение...** и введите **имя сервера** для сервера базы данных SQL Azure, вы только что создали.
    
14. В раскрывающемся списке **Проверка подлинности** выберите **Проверка подлинности SQL Server**.
    
15. Введите имя пользователя и пароль, использованный при создания базы данных Azure SQL server и нажмите кнопку **Подключить**.
    
16. Нажмите кнопку **Далее**, затем нажмите кнопку **Готово**и подождите, пока не будет создана база данных. После создания, нажмите кнопку **Закрыть** , чтобы закрыть мастер.
    
17. Вернитесь на портале управления Azure ( [https://manage.windowsazure.com/](https://manage.windowsazure.com/)), чтобы проверить, успешно создана база данных Northwind. Вы должны увидеть, что оно указано на экране баз данных sql, как показано на рисунке 4.
    
    **На рисунке 4. Список элементов базы данных SQL Server**

    ![Отображает список всех баз данных SQL, в том числе Northwind](media/036b4252-f57b-4f39-9f60-ddaa30daf23c.png)

18. Выберите базу данных "Борей" и выберите **строки подключения базы данных SQL представления**.
    
19. Скопируйте строку подключения и вставьте его в текстовый файл и сохраните его локально. Эта строка подключения понадобится позднее. Закройте диалоговое окно **Строки подключения** .
    
20. Перейдите по ссылке **настроить правила брандмауэра Windows Azure для этого IP-адреса** и добавьте IP-адрес правила брандмауэра для доступа к базе данных.
    
21. Откройте проект Core.DataStorageModels.sln в Visual Studio 2013.
    
22. В **Окне Обозреватель решений**Visual Studio найдите файл Web.config.
    
23. В файле Web.config найдите добавить `name="NorthWindEntities"` и замените существующий connectionString значение с строку подключения, который был сохранен локально на шаге 19. 
    
    ```XML
      <add name="NorthWindEntities" connectionString="metadata=res://*/Northwind.csdl|res://*/Northwind.ssdl|res://*/Northwind.msl;provider=System.Data.SqlClient;provider connection string=&amp;quot;data source=<Your Server Here>.database.windows.net;initial catalog=NorthWind;user id=<Your Username Here>@<Your Server Here>;password=<Your Password Here>;MultipleActiveResultSets=True;App=EntityFramework&amp;quot;" providerName="System.Data.EntityClient" />
    ```
24. Сохраните файл Web.config.

## <a name="sharepoint-list-on-the-app-web-notes-scenario"></a>Список SharePoint на сайте приложения (сценарий заметки)
<a name="sectionSection1"> </a>

Сценарии списка заметки на сайте приложения с помощью списка SharePoint, показано, как выполнить списками в веб-приложения SharePoint. В веб-приложения с помощью поля Название и описание создается список заметок. API-Интерфейс REST SharePoint запрашивает список заметок и возвращает все заметки по идентификатору клиента.

С помощью списков в веб-приложение имеет важных преимуществ других решений хранения данных: можно использовать простой вызовов API-Интерфейс SharePoint REST для запроса данных. Однако есть некоторые недостатки:

- Чтобы обновить список метаданных, необходимо обновить и снова развернуть приложение.
    
- Чтобы обновить структуру данных, необходимо переписать логики приложения для хранения и обновления данных.
    
- Данные, хранящиеся в списке не могут быть легко доступны другие надстройки.
    
- Не удается найти данные в SharePoint.
    
- Объем данных, которые могут храниться в списках и размер наборы результатов запроса ограничены.
    
Код, лежащий в основе разделе Notes панель мониторинга клиентов использует запросы REST для извлечения данных из списка, разворачиваемое на сайте приложения. Этот список содержит поля для заголовков, авторов, идентификаторы клиента и описания. Интерфейс приложения можно использовать для добавления и извлечения примечания для указанного клиента, как показано на рисунке 5.

**На рисунке 5. Пользовательский интерфейс для приложения заметки**

![Снимок экрана, которая отображает пользовательский Интерфейс для модели хранения данных Notes](media/d98ce2cf-5022-4f2b-ad3e-da4eea52dfb2.png)

Ссылку **Просмотреть список заметок в веб-приложение** обеспечивает представление данных списков «по умолчанию».

Это приложение использует шаблон Model-View-Controller (MVC). Можно просмотреть код для сценария примечания в файле Views/CustomerDashboard/Notes.cshtml. Простой вызовов REST используется для добавления и извлечения данных. Следующий код получает заметки в списке заметки для указанного клиента.

```C#
function getNotesAndShow() {
    var executor = new SP.RequestExecutor(appWebUrl);
    executor.executeAsync(
       {
           url: appWebUrl + "/_api/web/lists/getByTitle('Notes')/items/" +
                "?$select=FTCAM_Description,Modified,Title,Author/ID,Author/Title" +
                "&amp;$expand=Author/ID,Author/Title" +
                "&amp;$filter=(Title eq '" + customerID + "')",
           type: "GET",
           dataType: 'json',
           headers: { "accept": "application/json;odata=verbose" },
           success: function (data) {
               var value = JSON.parse(data.body);
               showNotes(value.d.results);
           },
           error: function (error) { console.log(JSON.stringify(error)) }
       }

    );
}
```

Следующий код добавляет Примечание для данного клиента в список заметок.

```C#
function addNoteToList(note, customerID) {
    var executor = new SP.RequestExecutor(appWebUrl);
    var bodyProps = {
        '__metadata': { 'type': 'SP.Data.NotesListItem' },
        'Title': customerID,
        'FTCAM_Description': note
    };
    executor.executeAsync({
        url: appWebUrl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('Notes')/items?@target='" + appWebUrl + "'",
        contentType: "application/json;odata=verbose",
        method: "POST",
        headers: {
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        body: JSON.stringify(bodyProps),
        success: getNotesAndShow,
        error: addNoteFailed
    });
}
```

5000 элементов можно добавить в список, чтобы показать, что список запросов, получения результата набор 5000 или большего числа элементов будет выполняться и сбора данных для пороговое значение для списка. Также можно добавить столько данных в список на сайте приложения, превышает ограничение хранилища для семейства веб-сайтов (которого зависит от того, как объем памяти вы выделенный к нему). Эти сценарии демонстрируют два из наиболее важные ограничения этот подход: списка ограничения на размер запроса и ограничения пространства для хранения данных. Если организации требуется требуется при работе с большими наборами данных и наборы результатов запроса, этот подход не работает.

### <a name="list-query-threshold"></a>Пороговое значение для списка
<a name="bk_listquerythreshold"> </a>

Для загрузки достаточно данных превышает пороговое значение ограничения запроса списка:


1. В левой панели выберите **Пример домашней страницы**.
    
2. В разделе **Пороговые значения запросов списка** выберите **Добавить элементы списка в список заметок в веб-приложения**.
    
3. Следуя инструкциям, которые отображаются над кнопкой эта операция 10 раз.
    
    При обновлении списка заметок в верхней части страницы, которое указывает, сколько элементов списка (примечания), вы добавили появится сообщение и сколько остаются для добавления.
    
    **Примечание**  Около одной минуты выполняется операция каждый раз, когда нажмите кнопку Запуск. Конечный результат выполнения операции 10 раз показано на рисунке 6.
4. После добавления 5,001 элементов в список, выберите в меню слева заметки. При загрузке страницы, появится сообщение об ошибке, показано на рисунке 6, для которого извлекаются из интерфейса API REST SharePoint.
    
    **На рисунке 6. Список запроса thresold превысила сообщение об ошибке**

    ![Снимок экрана, которая отображает сообщение об ошибке о том, что операция превысила threshol представления списка.](media/90202b64-4b14-4764-9a4c-8fb236f8d10b.png)

5. Выберите **Список заметок в веб-приложения** и прокрутите список, чтобы увидеть, что она включает 500 строк. Обратите внимание, что несмотря на то, что представлений списка SharePoint можно обеспечить просмотр этого большого количества операций, API-Интерфейс REST не удается выполнить из-за регулировки порогового значения списка запросов.
    
### <a name="data-storage-limit"></a>Ограничение хранилища данных
<a name="bk_listquerythreshold"> </a>

Для загрузки достаточно данных превышает ограничение хранилища данных:

1. В левой панели выберите **Пример домашней страницы**.
    
2. В разделе порогового значения данных должны **заполнить список заметок Web App с 1 ГБ данных**.
    
3. Следуя инструкциям, которые отображаются над кнопкой **заполнить список заметок Web App с 1 ГБ данных** эта операция 11 раз.
    
    При обновлении списка заметок в верхней части страницы, которое указывает, сколько элементов списка (примечания), вы добавили появится сообщение и сколько остаются для добавления.
    
    **Примечание**  Около одной минуты выполняется операция каждый раз, когда нажмите кнопку Запуск. Конечный результат выполнения операции 11 раз показано на рисунке 7.
4. После выполнения операции 11 раз, появится сообщение об ошибке при нажатии кнопки, как показано на рисунке 7.
    
    **На рисунке 7. Сообщение об ошибке Превышен хранилища данных**

    ![Снимок экрана, которая отображает сообщение об ошибке, выполняемое при превышении ограничений хранилища данных](media/0bc55483-0ee1-487a-ba34-e827ec47aadd.png)

5. После превышает ограничение хранилища данных, нажмите кнопку возврата в веб-браузере и затем выберите ссылку **заметки** в меню слева.
    
6. Выберите **список заметок в веб-приложения**.
    
    При загрузке страницы, сообщение об ошибке отображается в верхней части страницы, которое указывает, что сайт недостаточно дискового пространства.

## <a name="sharepoint-list-on-the-host-web-support-cases-scenario"></a>Список SharePoint на хост-сайта (поддержка случаев сценария)
<a name="sectionSection2"> </a>

В сценарии поддержки случаев отображает данные, которые хранятся в списке SharePoint на хост-сайте. В этом сценарии используются два различных шаблона для доступа и взаимодействия с данными. Первый шаблон включает в себя службы поиска SharePoint и применения содержимого с веб-части поиска с помощью настраиваемого шаблона для отображения. Второй шаблон содержит часть приложения (веб-часть клиента), который отображается представление MVC, который использует **SP. RequestExecutor** вызов API-Интерфейс SharePoint REST.

Существует несколько преимуществ использования этого подхода:

- Можно выполнить запрос данных с помощью простых запросов REST или код объектной модели клиента.
    
- Можно выполнить поиск данных в SharePoint.
    
- Можно обновлять метаданные списка и создавать новые представления для списка без обновления и повторное развертывание приложения. Эти изменения не влияет на поведение приложения.
    
- Списки на веб-сайт не удаляются при удалении приложения, если приложение не использует события **AppUninstalled** Чтобы удалить список и/или удалить данные.
    
Смещения эти преимущества являются следующие недостатки:

- Веб-сайт ограничивает объем данных, которые можно хранить в списках и размера результатов запроса. Если организации требуется для хранения и/или запрос больших наборов данных, это не рекомендуется.
    
- Для сложных запросов а также баз данных выполните списков.
    
- Для резервного копирования и восстановления данных, а также баз данных выполните списков.
    
В списке SharePoint, развертывать на хост-сайта хранятся данные для этого сценария. Данные извлекаются и отображаются с помощью следующих: 

- [Веб-часть поиска контента](https://msdn.microsoft.com/en-us/library/office/jj163789%28v=office.15%29.aspx).
    
- Часть приложения, реализованные в виде model-view-controller представления. 
    
Код в этом представлении используется запросов REST для получения сведений из списка, а веб-часть поиска контента службы поиска SharePoint для извлечения данных. Два подхода Демонстрация значительные преимущества этого параметра: служба поиска и интерфейсы API REST или CSOM можно использовать для получения сведений из списка на веб-сайт.

Если выбрать клиента из раскрывающегося списка вариантов поддержки вы увидите данные вариантов поддержки для клиента отображаются в веб-частей и веб-части приложения (на рисунке 8). Веб-части могут возвращает содержимое сразу, так как он может занять до 24 часов для службы поиска SharePoint для индексации данных. Вы также можете ссылку **Список вариантов поддержки представления в веб-сайт** , чтобы увидеть обычное представление данных списков.

**На рисунке 8. Пользовательский интерфейс для поддержки сценарий**

![Снимок экрана, которая отображает пользовательский Интерфейс для взаимодействия со сценарием вариантов поддержки](media/eac41f5c-90b7-4fe3-b47e-0d65b79cbf1c.png)

Веб-часть поиска контента, развертывания с помощью этого приложения с помощью шаблона для отображения настраиваемых. На рисунке 9 показан, где в каталоге **средств** веб-проекта можно найти в веб-части и связанный шаблон.

**На рисунке 9. Содержимое каталога средств веб-проекта**

![Снимок экрана в каталоге активов](media/95db9118-9e56-4e39-84b1-271e54447792.png)

Приведенный ниже код JavaScript, который можно найти в файле Views/SupportCaseAppPart\Index.cshtml использует междоменную библиотеку для вызова запросов REST в списке SharePoint на хост-сайта. 

```C#
function execCrossDomainRequest() {
var executor = new SP.RequestExecutor(appWebUrl);

executor.executeAsync(
   {
        url: appWebUrl + "/_api/SP.AppContextSite(@@target)" +
                "/web/lists/getbytitle('Support Cases')/items" +
              "?$filter=(FTCAM_CustomerID eq '" + customerID + "')" +
            "&amp;$top=30" +
                    "&amp;$select=Id,Title,FTCAM_Status,FTCAM_CSR" +
                    "&amp;@@target='" + hostWebUrl + "'",
method: "GET",
              headers: { "Accept": "application/json; odata=verbose" },
              success: successHandler,
              error: errorHandler
   }
);
}
```

5000 элементов можно добавить в список, чтобы показать, что список запросов, получения результата набор 5000 или большего числа элементов будет выполняться и сбора данных для пороговое значение для списка. В данном сценарии показано одно из наиболее важные ограничения этот подход: список ограничения на размер запроса. Если бизнеса требуется требуется работать с большим объемом данных и наборы результатов запроса, этот подход не работает. Для получения дополнительных сведений см [пороговое значение для списка](#bk_listquerythreshold) ранее в этой статье.

## <a name="northwind-odata-web-service-customer-dashboard-scenario"></a>Веб-службе Northwind OData (панель мониторинга клиентов сценария)
<a name="sectionSection3"> </a>

Сценарий панели мониторинга клиентов использует JQuery AJAX для запуска службы NorthWind OData, чтобы получить сведения о клиенте. Приложение хранит данные в веб-службе, а затем получать его с помощью [OData](http://www.odata.org/) .

Ниже приведены преимущества использования этого подхода.

- Данной веб-службы может поддерживать несколько надстроек.
    
- Вы можете обновить веб-службы без необходимости обновите и повторно разверните вашего приложения.
    
- Установок SharePoint и веб-службы не влияют на друг с другом.
    
- Размещение служб, таких как Microsoft Azure позволяют масштабирования веб-служб.
    
- Можно резервное копирование и восстановление сведений на веб-служб отдельно из сайта SharePoint.
    
- Не потерять данные при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.
    
Сценарий панели мониторинга клиентов хранит данные в веб-службы, который реализует стандарта OData для извлечения данных. В интерфейсе клиента панели мониторинга выбрать клиента из раскрывающегося меню и отображает сведения о клиента в области **Сведения о клиенте** .

На этой странице пользовательского интерфейса — это представление Model-View-Controller. Отображение определяется в файле Views/CustomerDashboard\Home.cshtml. Базовый код содержится в файле Scripts/CustomerDashboard.js. Код JavaScript использует AJAX для запроса веб-службе "Борей". Так как это службе OData, веб-службы запросов состоит из аргументы строки запроса, подключенного к URL-адрес, указывающий на конечную веб-службы. Служба возвращает сведения о пользователе в формате JSON.

Приведенный ниже код запускается при выборе ссылки **Панель мониторинга клиентов** . Он получает все идентификаторы и имена клиентов для заполнения в раскрывающемся меню.

```C#
var getCustomerIDsUrl = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json&amp;$select=CustomerID";
    $.get(getCustomerIDsUrl).done(getCustomerIDsDone)
        .error(function (jqXHR, textStatus, errorThrown) {
            $('#topErrorMessage').text('Can\'t get customers. An error occurred: ' + jqXHR.statusText);
        });
```

Приведенный ниже код выполняется, когда имя клиента выберите в раскрывающемся меню. Аргумент **$filter** OData используется для указания идентификатора клиента и другие аргументы строки запроса для получения сведений, связанных с этим клиентом.

```C#
var url = "https://odatasampleservices.azurewebsites.net/V3/Northwind/Northwind.svc/Customers?$format=json" +  "&amp;$select=CustomerID,CompanyName,ContactName,ContactTitle,Address,City,Country,Phone,Fax" + "&amp;$filter=CustomerID eq '" + customerID + "'";

$.get(url).done(getCustomersDone)
   .error(function (jqXHR, textStatus, errorThrown) {
          alert('Can\'t get customer ' + customerID + '. An error occurred: ' + 
                 jqXHR.statusText);
});
```

## <a name="azure-table-storage-customer-service-survey-scenario"></a>Хранение таблицы Azure (сценарий опроса службы клиента)
<a name="sectionSection4"> </a>

Сценарий опроса службы клиента позволяет представителю службы для просмотра их оценки, опросы клиентов на основе клиента и использует хранилища Azure таблицы и Microsoft.WindowsAzure.Storage.Table.CloudTable API для хранения и взаимодействия с данными.

Ниже приведены преимущества использования этого подхода.

- Таблицы Azure хранилища поддерживает более одного приложения.
    
- Можно обновить таблиц Azure хранения без необходимости обновите и повторно разверните вашего приложения.
    
- Установки SharePoint и таблиц Azure хранения не оказывают влияния на производительность друг друга.
    
- Хранилище Azure легко таблиц масштабирования.
    
- Можно резервное копирование и восстановление хранилища Azure таблиц отдельно от сайта SharePoint.
    
- Не потерять данные при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.
    
Интерфейс приложения отображается оценка опроса текущего пользователя на странице центра. Если таблицы Azure хранилища пустое, приложение добавьте некоторые данные в таблицу до его отображения.

Следующий код из CSRInfoController.cs определяет метод **Домашняя страница** , который извлекает пользователя **nameId**.

```C#
[SharePointContextFilter]
public ActionResult Home()
{
    var context = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);
    var sharePointService = new SharePointService(context);
    var currentUser = sharePointService.GetCurrentUser();
    ViewBag.UserName = currentUser.Title;

    var surveyRatingsService = new SurveyRatingsService();
    ViewBag.Score = surveyRatingsService.GetUserScore(currentUser.UserId.NameId);

    return View();
}
```

Следующий код из файла SurveyRatingService.cs определяет конструктор **SurveyRatingsService** , который выполняет настройку подключения к учетной записи хранилища Azure.

```C#
public SurveyRatingsService(string storageConnectionStringConfigName = 
        "StorageConnectionString")
{
    var connectionString = Util.GetConfigSetting("StorageConnectionString");
    var storageAccount = CloudStorageAccount.Parse(connectionString);

    this.tableClient = storageAccount.CreateCloudTableClient();
    this.surveyRatingsTable = this.tableClient.GetTableReference("SurveyRatings");
    this.surveyRatingsTable.CreateIfNotExists();
}
```

Следующий код из одного файла определяет метод **GetUserScore** , который получает показатель опроса пользователя из таблицы Azure хранилища.

```C#
public float GetUserScore(string userName)
{
    var query = new TableQuery<Models.Customer>()
    .Select(new List<string> { "Score" })
    .Where(TableQuery.GenerateFilterCondition("Name", 
    QueryComparisons.Equal, userName));

    var items = surveyRatingsTable
         .ExecuteQuery(query)
             .ToArray();

    if (items.Length == 0)           
    return AddSurveyRatings(userName);

    return (float)items.Average(c => c.Score);
}
```

Если в таблице не содержит все данные опроса, связанные с текущим пользователем, метод **AddSurveyRating** случайным образом назначает счета для пользователя.

```C#
private float AddSurveyRatings(string userName)
{
    float sum = 0;
    int count = 4;
    var random = new Random();

    for (int i = 0; i < count; i++)
    {
    var score = random.Next(80, 100);
    var customer = new Models.Customer(Guid.NewGuid(), userName, score);

    var insertOperation = TableOperation.Insert(customer);
    surveyRatingsTable.Execute(insertOperation);

    sum += score;
    }
    return sum / count;
}
```

## <a name="azure-queue-storage-customer-call-queue-scenario"></a>Хранилище Azure очереди (сценарий очереди вызовов клиента)
<a name="sectionSection5"> </a>

Сценарий очередь звонков клиентов перечислены звонящих в очередь поддержки и моделирует получают звонки. В сценарии Azure хранения очередей используется для хранения данных и **Microsoft.WindowsAzure.Storage.Queue.CloudQueue** API с Model-View-Controller.

Ниже приведены преимущества использования этого подхода.

- Очереди Azure хранилища поддерживает более одного приложения.
    
- Очереди Azure хранилища можно обновлять без необходимости обновите и повторно разверните вашего приложения.
    
- Установки SharePoint и хранилища Azure очереди не оказывают влияния на производительность друг друга.
    
- Легко масштабировать очереди Azure хранилища.
    
- Можно резервное копирование и восстановление вашей очереди Azure хранилища отдельно от сайта SharePoint.
    
- Не потерять данные при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.
    
Интерфейс приложения отображается очередь вызова поддержки в центральной области при выборе ссылки **Вызова очереди** . Получение вызовов (Добавление вызова в очередь) можно смоделировать, выбрав **Моделирования звонки**и, выбрав **Принять вызов** действие, связанное с в конкретном вызове моделирования работы с наиболее старых вызова (с удалением звонка из очереди).

На этой странице — это представление Model-View-Controller, определенных в файле Views\CallQueue\Home.cshmtl. Файл Controllers\CallQueueController.cs определяет класс **CallQueueController** , который содержит методы для получения всех звонков в очереди, добавление вызова в очередь (моделирование звонка) и их удаление звонка из очереди (с помощью вызова). Каждый из этих методов вызывает методов, определенных в файле Services\CallQueueService.cs, который используется очереди Azure хранилища API для получения базовых сведений в очереди хранилища.

```C#
public class CallQueueController : Controller
{
    public CallQueueService CallQueueService { get; private set; }

    public CallQueueController()
    {
        CallQueueService = new CallQueueService();
    }

    // GET: CallQueue
    public ActionResult Home(UInt16 displayCount = 10)
    {
        var calls = CallQueueService.PeekCalls(displayCount);
        ViewBag.DisplayCount = displayCount;
        ViewBag.TotalCallCount = CallQueueService.GetCallCount();
        return View(calls);
    }

    [HttpPost]
    public ActionResult SimulateCalls(string spHostUrl)
    {
        int count = CallQueueService.SimulateCalls();
        TempData["Message"] = string.Format("Successfully simulated {0} calls and added them to the call queue.", count);
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }

    [HttpPost]
    public ActionResult TakeCall(string spHostUrl)
    {
        CallQueueService.DequeueCall();
        TempData["Message"] = "Call taken successfully and removed from the call queue!";
        return RedirectToAction("Index", new { SPHostUrl = spHostUrl });
    }
}
```

Файл CallQueueService.cs определяет класс **CallQueueService** , который устанавливает подключение к очереди Azure хранилища. Этот класс также содержит методы для добавления, удаления (извлечения) и извлечение вызовов из очереди.

```C#
public class CallQueueService
{
    private CloudQueueClient queueClient;

    private CloudQueue queue;

    public CallQueueService(string storageConnectionStringConfigName = "StorageConnectionString")
    {
        var connectionString = CloudConfigurationManager.GetSetting(storageConnectionStringConfigName);
        var storageAccount = CloudStorageAccount.Parse(connectionString);

        this.queueClient = storageAccount.CreateCloudQueueClient();
        this.queue = queueClient.GetQueueReference("calls");
        this.queue.CreateIfNotExists();
        }

        public int? GetCallCount()
        {
        queue.FetchAttributes();
        return queue.ApproximateMessageCount;
    }

    public IEnumerable<Call> PeekCalls(UInt16 count)
    {
        var messages = queue.PeekMessages(count);

        var serializer = new JavaScriptSerializer();
        foreach (var message in messages)
        {
        Call call = null;
        try
        {
        call = serializer.Deserialize<Call>(message.AsString);
        }
        catch { }

        if (call != null) yield return call;
        }
    }

    public void AddCall(Call call)
    {
        var serializer = new JavaScriptSerializer();
        var content = serializer.Serialize(call);
        var message = new CloudQueueMessage(content);
        queue.AddMessage(message);
    }

    public void DequeueCall()
    {
        var message = queue.GetMessage();
        queue.DeleteMessage(message);
    }

    public int SimulateCalls()
    {
        Random random = new Random();
        int count = random.Next(1, 6);
        for (int i = 0; i < count; i++)
        {
        int phoneNumber = random.Next();
        var call = new Call
        {
        ReceivedDate = DateTime.Now,
        PhoneNumber = phoneNumber.ToString("+1-000-000-0000")
        };
        AddCall(call);

        return count;
    }
}
```

## <a name="sql-azure-database-recent-orders-scenario"></a>Базы данных SQL Azure (последние заказы сценария)
<a name="sectionSection6"> </a>

Сценарий последние заказы прямой вызов к базе данных Northwind SQL Azure используется для возврата всех заказов для указанного клиента.

Ниже приведены преимущества использования этого подхода.

- Базы данных может поддерживать более одного приложения.
    
- Можно обновить схему базы данных без необходимости обновите и повторно разверните вашего приложения, до тех пор, пока изменения схемы не влияют на запросы в вашем приложении.
    
- Реляционные базы данных можно поддерживают отношения "многие ко многим" и таким образом поддерживать более сложных бизнес-сценарии.
    
- Средства разработки баз данных можно использовать для оптимизации проекта базы данных.
    
- Реляционные базы данных обеспечивают лучшую производительность, чем другие параметры, при необходимости выполнять сложные операции в запросах, таких как вычисления и соединений.
    
- Базы данных SQL Azure позволяет импортировать и экспортировать данные, чтобы упростить управление и перемещение данных.
    
- Все данные не потеряны при удалении приложения, если приложение не использует события **AppUninstalled** для удаления данных.
    
Последние заказы интерфейс работает как в интерфейсе клиента панели мониторинга. Выберите ссылку **Последних заказов** в левом столбце и затем выберите клиента из раскрывающегося меню в верхней части центральной панели. Список заказов из клиента отображаются в центральной панели.

На этой странице — это представление Model-View-Controller, определенных в файле Views\CustomerDashboard\Orders.cshtml. Код в файле Controllers\CustomerDashboardController.cs использует [Entity Framework](https://msdn.microsoft.com/en-us/data/ef.aspx) для запроса к таблице **Orders** в базе данных SQL Azure. Идентификатор клиента передается с помощью параметра строки запроса в URL-адрес, который передается, когда пользователь выбирает клиента в раскрывающемся меню. Запрос создает соединение таблицы **клиентов**, **сотрудников**и **отправителя** . Результат запроса затем передается в Model-View-Controller представление, отображающее результаты.

Следующий код из файла CustomerDashboardController.cs выполняет запрос к базе данных и возвращает данные в представление.

```C#
public ActionResult Orders(string customerId)
{            
    Order[] orders;
    using (var db = new NorthWindEntities())
    {
            orders = db.Orders
                  .Include(o => o.Customer)
                  .Include(o => o.Employee)
                  .Include(o => o.Shipper)
                  .Where(c => c.CustomerID == customerId)
                  .ToArray();
    }

    ViewBag.SharePointContext = 
        SharePointContextProvider.Current.GetSharePointContext(HttpContext);

    return View(orders);
}
```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online](Composite-buisness-apps-for-SharePoint.md)
    
-  [Шаблоны и рекомендации по разработке решений для Office 365 на сайте GitHub](https://github.com/SharePoint/PnP)
