---
title: "Программное развертывание собственной кнопки в надстройке с размещением у поставщика"
description: "Регистрация программным путем настраиваемой кнопки ленты с настраиваемым списком в одной надстройке SharePoint, размещенной у поставщика."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 0fc7f5e8d4255f103413d9f49750d7d3365a2562
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in"></a>Программное развертывание собственной кнопки в надстройке с размещением у поставщика

Это девятая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии.

-  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [Настройка внешнего вида надстройки SharePoint, размещенной у поставщика](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
-  [Добавление настраиваемой кнопки в надстройку, размещенную у поставщика](include-a-custom-button-in-the-provider-hosted-add-in.md)
-  [Краткий обзор объектной модели SharePoint](get-a-quick-overview-of-the-sharepoint-object-model.md)
-  [Добавление операций записи SharePoint в надстройку, размещенную у поставщика](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
-  [Добавление веб-части надстройки в надстройку, размещенную у поставщика](include-an-add-in-part-in-the-provider-hosted-add-in.md)
-  [Обработка событий надстройки, размещенной у поставщика](handle-add-in-events-in-the-provider-hosted-add-in.md)
-  [Добавление логики, выполняемой при первом запуске, в надстройку, размещаемую у поставщика](add-first-run-logic-to-the-provider-hosted-add-in.md)

> [!NOTE]
> Если вы изучали предыдущие статьи из этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей. Кроме того, вы можете скачать репозиторий [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeProgrammaticButton.sln.

В этой статьи вы узнаете, как включать настраиваемую кнопку ленты в надстройку SharePoint, когда список, на ленте которого размещается кнопка, также развертывается программным способом в той же надстройке.

## <a name="re-add-the-custom-button-to-the-project"></a>Повторное добавление настраиваемой кнопки в проект

> [!NOTE]
> Когда решение открывается повторно, для параметров раздела "Запускаемые проекты" в Visual Studio обычно возвращаются значения по умолчанию. Сразу же после повторного открытия примера решения согласно инструкциям из этой серии статей всегда делайте вот что: 
> 1. В верхней части **обозревателя решений** щелкните узел решения правой кнопкой мыши и выберите пункт **Назначить запускаемые проекты**.  
> 2. Убедитесь, что в столбце **Действие** для всех трех проектов указано значение **Запуск**.

В предыдущей статье вы удалили настраиваемую кнопку ленты **AddEmployeeToCorpDB** из проекта. Добавьте ее обратно, сделав вот что:

1. В верхней части **обозревателя решений** на панели инструментов нажмите кнопку **Показать все файлы**.

   *Рис. 1. Панель инструментов обозревателя решений*

   ![Панель инструментов обозревателя решений с рамкой вокруг кнопки "Показать все файлы".](../images/f6b035f5-1aa7-452a-8f59-9dd44b062d06.PNG)

2. В проекте **ChainStore** щелкните правой кнопкой мыши элемент **AddEmployeeToCorpDB**, а затем выберите пункт **Включить в проект**.

3. Снова нажмите кнопку **Показать все файлы**.

4. В проекте **ChainStore** разверните узел **AddEmployeeToCorpDB**, а затем откройте файл elements.xml.

## <a name="understand-a-dilemma-and-its-solution"></a>Описание проблемы и ее решение

В файле elements.xml атрибут **RegistrationId** элемента **CustomAction** служит для идентификации списка, на ленту которого вы добавляете кнопку: `{$ListId:Lists/Local Employees;}`. Это отлично работало, когда список уже был добавлен на хост-сайт вручную. Но теперь при развертывании списка программным способом в коде, выполняемом при первом запуске, когда SharePoint устанавливает надстройку и пытается развернуть кнопку, списка еще не существует. В этом случае установка надстройки может привести к созданию исключения и завершиться со сбоем.

Развертывание списка в обработчике событий установки, а не в коде, выполняемом при первом запуске, не решит эту проблему. Это связано с тем, что SharePoint развертывает описанные настраиваемые компоненты, например настраиваемую кнопку (и веб-часть надстройки **Place Order** (Размещение заказа)), *прежде чем* запустить настраиваемый обработчик, поэтому когда SharePoint пытается развернуть кнопку, списка еще не существует.

Создание настраиваемой кнопки полностью программным способом непрактично по причинам, которые слишком сложны, чтобы обсуждать их здесь. К счастью, это не нужно. Существует относительно безболезненный способ "полупрограммного" создания настраиваемой кнопки и назначения ее настраиваемому списку. 

Для этого нужно выполнить вот какие основные действия:

1. Оставьте описательно определенную кнопку в проекте, но назначьте ее ленте какого-либо приложения, которое всегда имеется на сайтах SharePoint, а не ленте списка, который развертывается программным способом с помощью той же надстройки. 

2. В коде, выполняемом при первом запуске, после программного создания списка добавьте неопределенную кнопку на ленту списка.

3. Инициализируйте свойства новой кнопки, используя значения свойств исходной кнопки. Сейчас у нас есть две идентичные кнопки. Вторая кнопка назначена ленте списка **Local Employees** (Местные сотрудники).

4. Удалите исходную кнопку программным способом.

## <a name="programmatically-register-the-custom-button"></a>Регистрация настраиваемой кнопки программным способом

Ниже описывается реализация этой стратегии.

1. В проекте **ChainStore** разверните узел **AddEmployeeToCorpDB**, откройте файл elements.xml, а затем измените значение атрибута **RegistrationId** элемента **CustomAction** на число 100. Это идентификатор типа списка. Даже если на веб-сайте нет экземпляров списка этого типа, *тип* списка есть на всех веб-сайтах SharePoint. Теперь атрибут должен выглядеть так:
    
    ```XML
      RegistrationId="100"
    ```

2. В файле SharePointComponentDeployer.cs добавьте указанную ниже строку в метод **DeployChainStoreComponentsToHostWeb** сразу же после строки, в которой вызывается метод `CreateLocalEmployeesList`. Вы создадите этот метод на следующем этапе.
    
    ```C#
      ChangeCustomActionRegistration();
    ```

3. Добавьте указанный ниже метод в класс `SharePointComponentDeployer`. 

    ```C#
      private static void ChangeCustomActionRegistration()
    {
        using (var clientContext = sPContext.CreateUserClientContextForSPHost())
        {
         var query = from action in clientContext.Web.UserCustomActions
                 where action.Name == "{button_GUID} .AddEmployeeToCorpDB"
                 select action;
          IEnumerable<UserCustomAction> matchingActions = clientContext.LoadQuery(query);          
             clientContext.ExecuteQuery();

          UserCustomAction webScopedEmployeeAction = matchingActions.Single();

         // TODO8: Get a reference to the (empty) collection of custom actions 
         // that are registered with the custom list.

         // TODO9: Add a blank custom action to the list's collection.

         // TODO10: Copy property values from the descriptively deployed
         // custom action to the new custom action

        // TODO11: Delete the original custom action.         

          clientContext.ExecuteQuery();
        }
    }
    ```

   Обратите внимание на следующие особенности этого кода:
    
   - Так как дополнительное действие, то есть настраиваемая кнопка, зарегистрировано на ленте для *типа* списка, область его действия распространяется на весь веб-сайт и находится в коллекции дополнительных действий веб-сайта. Таким образом, код получает его из этой коллекции.
    
   - Значение свойства `action.Name` поступает из атрибута **ID** элемента **CustomAction** в файле element.xml из узла **AddEmployeeToCorpDB**.
    
   > [!IMPORTANT]
   > **Вам необходимо изменить значение `action.Name` в коде, чтобы оно совпадало со значением в файле elements.xml.** Часть GUID имени будет другой. Обратите внимание, что между GUID и остальной частью имени есть символ `"."`. Вот пример строки: 
   > 
   > `where action.Name == "4a926a42-3577-4e02-9d06-fef78586b1bc.AddEmployeeToCorpDB"`

4. Замените `TODO8` указанным ниже кодом. Обратите внимание, что если вы отзовете надстройку, созданные ею компоненты не будут удалены. По завершении работы кода, выполняемого при первом запуске, в коллекции **UserCustomActions** списка появится дополнительное действие, которое не будет отозвано при следующем нажатии клавиши F5. Чтобы избежать путаницы, в последней строке в этом коде метод `listActions.Clear();` очищает коллекцию.

    ```C#
    var queryForList = from list in clientContext.Web.Lists
               where list.Title == "Local Employees"
               select list;
    IEnumerable<List> matchingLists = clientContext.LoadQuery(queryForList);
    clientContext.ExecuteQuery();

    List employeeList = matchingLists.First();
    var listActions = employeeList.UserCustomActions;
    clientContext.Load(listActions);
    listActions.Clear();
    ```

5. Замените `TODO9` указанной ниже строкой, которая добавляет неопределенное дополнительное действие в список **Local Employees** (Местные сотрудники).
    
    ```C#
      var listScopedEmployeeAction = listActions.Add();
    ```

6. Замените `TODO10` указанным ниже кодом. 

    ```C#
    listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
    listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
    listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
    listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
    listScopedEmployeeAction.Update();
    ```

   Обратите внимание на следующие особенности этого кода:
    
   - Он назначает значения свойств кнопки уровня веб-сайта (которая была развернута с помощью описательной разметки) соответствующим свойствам кнопки уровня списка, так что эти две кнопки становятся идентичными за исключением области их действия.
    
   - В свойстве **Sequence** указывается относительный порядок, в котором кнопка будет отображена в своей области на ленте. В этом случае кнопка находится в разделе **Actions** (Действия) на вкладке **Items** (Элементы) ленты. В описательной разметке это значение было равно 10001. Это достаточно большое значение, чтобы кнопка отображалась после (т. е. справа от) всех встроенных кнопок, которые SharePoint самостоятельно помещает в раздел **Actions** (Действия) ленты.

7. Замените `TODO11` указанной ниже строкой, в которой удаляется исходная кнопка, определенная описательным способом. Если бы у нас не было этой строки, то каждый список на веб-сайте, для которого используется шаблон списка 100, включал бы настраиваемую кнопку. Так как функциональность кнопки тесно связана со списком **Local Employees** (Местные сотрудники), то нет никакого смысла размещать эту кнопку в других списках. Кроме того, без этой строки кнопка будет *дважды* размещена в списке **Local Employees** (Местные сотрудники), так как для этого списка используется шаблон 100.
    
    ```C#
      webScopedEmployeeAction.DeleteObject();
    ```
    
8. Теперь весь метод должен иметь указанный ниже вид (за исключением того, что заполнитель необходимо заменить на GUID).
    
    ```C#
      private static void ChangeCustomActionRegistration()
    {
        using (var clientContext = SPContext.CreateUserClientContextForSPHost())
        {
         var query = from action in clientContext.Web.UserCustomActions
                 where action.Name == "{button_GUID} .AddEmployeeToCorpDB"
                 select action;
          IEnumerable<UserCustomAction> matchingActions = clientContext.LoadQuery(query);          
             clientContext.ExecuteQuery();

          UserCustomAction webScopedEmployeeAction = matchingActions.Single();

         var queryForList = from list in clientContext.Web.Lists
                    where list.Title == "Local Employees"
                    select list;
         IEnumerable<List> matchingLists = clientContext.LoadQuery(queryForList);
         clientContext.ExecuteQuery();

        List employeeList = matchingLists.First();
        var listActions = employeeList.UserCustomActions;
        clientContext.Load(listActions);
        listActions.Clear();

        var listScopedEmployeeAction = listActions.Add();

        listScopedEmployeeAction.Title = webScopedEmployeeAction.Title;
        listScopedEmployeeAction.Location = webScopedEmployeeAction.Location;
        listScopedEmployeeAction.Sequence = webScopedEmployeeAction.Sequence;
        listScopedEmployeeAction.CommandUIExtension = webScopedEmployeeAction.CommandUIExtension;
        listScopedEmployeeAction.Update();

        webScopedEmployeeAction.DeleteObject();         

        clientContext.ExecuteQuery();
        }
    }
    ```


## <a name="request-full-control-of-the-host-web"></a>Запрос полного контроля над хост-сайтом

Так как теперь надстройка добавляет и удаляет дополнительные действия уровня веб-сайта, необходимо расширить разрешения для нее с уровня "Управление" до уровня "Полный контроль". Для этого сделайте вот что:

1. В **обозревателе решений** в проекте **ChainStore** откройте файл AppManifest.xml.

2. Откройте вкладку **Разрешения**. Для поля **Область** оставьте значение **Интернет**, а в поле **Разрешение** выберите из раскрывающегося списка пункт **Полный контроль**.

3. Сохраните файл.

## <a name="run-the-add-in-and-test-the-button-deployment"></a>Запуск надстройки и тестирование развертывания кнопки

1. Откройте страницу **Site Contents** (Содержание сайта) веб-сайта магазина в Гонконге и удалите список **Local Employees** (Местные сотрудники). 
    
   > [!NOTE]
   > При отзыве надстройки в Visual Studio не будут удалены созданные ею списки, поэтому вам потребуется вручную удалять их каждый раз, когда вы тестируете создающий их код.

2. Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express. Кроме того, он временно устанавливает надстройку на вашем тестовом сайте SharePoint и сразу же запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.

3. Когда откроется начальная страница надстройки, щелкните ссылку **Back to Site** (Вернуться на сайт) на размещенном в верхней части элементе управления хрома.

4. Перейдите на страницу **Site Contents** (Содержание сайта). На ней будет список **Local Employees** (Список сотрудников), так как его добавил код, выполняемый при первом запуске.
    
   > [!NOTE]
   > Если этого списка нет или у вас имеются другие свидетельства того, что код, выполняемый при первом запуске, не выполняется, возможно, при нажатии клавиши F5 таблица **Tenants** (Клиенты) не очищается. Самая распространенная причина этого заключается в том, что проект **ChainCorporateDB** больше не задан в качестве начального проекта в Visual Studio. См. [примечание в верхней части данной статьи](#re-add-the-custom-button-to-the-project) о том, как устранить эту проблему. Кроме того, убедитесь, что вы настроили базу данных так, чтобы она перестраивалась, как описано в разделе [Настройка Visual Studio для перестройки корпоративной базы данных при каждом сеансе отладки](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md#Rebuild).

5. Откройте список и добавьте элемент.

6. В представлении списка выберите этот элемент и откройте вкладку **Item** (Элемент) на ленте. 

7. На вкладке **Item** (Элемент) нажмите кнопку **Add to Corporate DB** (Добавить в корпоративную базу данных). Сотрудник будет добавлен в корпоративную базу данных, а значение поля **Added to Corporate DB** (Добавлен в корпоративную базу данных) изменится на **Yes** (Да).

8. Вернитесь на страницу **Site Contents** (Содержание сайта) и выберите **Add an add-in** (Добавить надстройку).

9. Добавьте новый **настраиваемый список**. По умолчанию он будет иметь тип Generic, которому соответствует тип списка 100. После создания списка откройте вкладку **Item** (Элемент) на ленте. Обратите внимание, что кнопки **Add to Corporate DB** (Добавить в корпоративную базу данных) *нет* на ленте. Это связано с тем, что ваш код удалил кнопку уровня веб-сайта.

10. Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.

11. Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.

## <a name="next-steps"></a>Дальнейшие действия
<a name="Nextsteps"> </a>

Для событий в списках и элементах списков также можно использовать настраиваемые обработчики в SharePoint. Чтобы узнать, как создать такой обработчик и развернуть его в коде, выполняемом при первом запуске, см. статью [Обработка событий элемента списка в надстройке, размещаемой у поставщика](handle-list-item-events-in-the-provider-hosted-add-in.md).
 

 

