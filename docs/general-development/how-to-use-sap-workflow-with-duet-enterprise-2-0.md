---
title: "Способ использование SAP рабочего процесса с Duet Enterprise 2.0 (en)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 816e28ed-8cea-4e33-98e5-d3d27136e2e6
ms.openlocfilehash: 516e0ee220db2d6ebaea1db3cdff9a6dc98c346c
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-sap-workflow-with-duet-enterprise-20"></a>Способ: использование SAP рабочего процесса с Duet Enterprise 2.0 (en)

## <a name="introduction"></a>Введение
<a name="bkmk_Introduction"> </a>

Рабочий процесс SAP Business предоставляет способ для автоматизации бизнес-процессов и с Duet Enterprise 2.0 эти рабочие процессы можно интегрировать в пределах Надстройка SharePoint.
  
    
    
Далее показано, как создать приложение, настроить его, а затем способ отображения данные извлекаются из рабочих процессов SAP.
  
    
    

## <a name="create-an-app-for-sharepoint-and-duet-enterprise-20"></a>Создание приложения для SharePoint и Duet Enterprise 2.0
<a name="bkmk_CreateApp"> </a>

Первым шагом является создание Надстройка SharePoint, которая будет содержать данные для подключения с помощью внешнего типа контента для Службы Business Connectivity Services (BCS), с помощью внешних списков и все настройки, вы можете использовать для представления данных.
  
    
    

### <a name="to-create-an-app-for-sharepoint"></a>Создание приложения для SharePoint:


1. Запустите Visual Studio 2012 от имени администратора.
    
  
2. Выберите **файл**, **новый**, **Создать проект**.
    
  
3. В диалоговом окне **Новый проект** разверните узел **Visual C#**, разверните узел **Office/SharePoint** и затем выберите узел **приложения**.
    
  
4. Выберите **приложение для SharePoint**.
    
  
5. Назовите проект и нажмите **кнопку ОК**.
    
  
6. В диалоговом окне **Укажите приложение для настройки SharePoint** первого имя приложения и выберите **Размещение в SharePoint** в списке **как разместить приложение для SharePoint**. Также укажите URL-адрес **сайта рабочего процесса Duet** требуется отладки в списке **какой сайт SharePoint использовать для отладки приложения** и нажмите кнопку **Готово**.
    
  
7. В меню Построение выберите команду **Развернуть** * \<имя вашего приложения\> * .
    
  
После развертывания приложения Visual Studio запустит страницу по умолчанию для приложения.
  
    
    

## <a name="add-the-external-content-type-and-external-lists-to-the-app"></a>Добавление внешнего типа контента и внешних списков для приложения
<a name="bkmk_AddECT"> </a>

BCS должна состоять принять во внимание к внешнему источнику данных. Это делается с помощью внешнего типа контента.
  
    
    

### <a name="to-add-an-external-content-type"></a>Чтобы добавить внешний тип контента:


1. В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.
    
  
2. На странице **Укажите источника OData** введите URL-адрес службы рабочих процессов Duet Enterprise. Ниже приведен пример URL-адрес службы Duet:
    
     *https://\<\<DUETGATEWAY\>\>:\<\<ПОРТ\>\>/sap/opu/odata/IWWRK/DUET_WORKFLOW_CORE, режим, c = SHAREPOINT_DE* 
    
  
3. Выберите имя для источника ODATA, например, SAPWorkflows и нажмите кнопку **Далее**.
    
  
4. Укажите имя пользователя SAP и пароль для подключения к службе метаданных.
    
  
5. Появится список сущностей данные, предоставляемые интерфейсом службы OData. Выбор сущностей, которые вы хотите включить в внешнего типа контента. В этом примере с помощью служб рабочих процессов SAP выполните одно из следующих:
    
  - **AttachmentCollection**
    
  
  - **CommentCollection**
    
  
  - **DecisionOptionCollection**
    
  
  - **ExtensibleElementCollection**
    
  
  - **ParticipantCollection**
    
  
  - **ServiceOperations**
    
  
  - **TaskDescriptionCollection**
    
  
  - **WorkflowTaskCollection**
    
  
6. Установите флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**.
    
  
7. Нажмите кнопку **Готово**.
    
  

> **Примечание:** Убедитесь, что службы рабочих процессов SAP позволяет обычной проверки подлинности, как средства для автоматического создания BDC в Visual Studio. 
  
    
    


## <a name="add-a-custom-action-feature-to-a-duet-enterprise-20-workflow-list"></a>Добавьте компонент дополнительного действия со списком Duet Enterprise 2.0 рабочего процесса
<a name="bkmk_AddCustomAction"> </a>

Для предоставления позволяет пользователю работать с новыми функциональными возможностями, добавленные в список SharePoint, следующие шаги будут добавить элемент в меню Действия сайта.
  
    
    

### <a name="to-add-a-custom-action"></a>Добавление настраиваемых действий:


1. Щелкните правой кнопкой мыши проект Надстройка SharePoint и добавьте новый элемент **UI Custom Action (Дополнительное действие пользовательского интерфейса)**.
    
  
2. Откройте файл **Elements.xml** компонента дополнительного действия узла web. Путем замены код в файл следующий XML-код, будет настраиваемого действия:
    
  - Объявите дополнительное действие ECB и его атрибуты.
    
  
  - Объявите дополнительное действие ленты и его атрибуты.
    
  
  - Объявите конечного приложения веб-страницы и значения, которые передаются в строке запроса. 
    
    Элемент **UrlAction** использует несколько токенов. Для получения дополнительных сведений см [Строки URL и маркеры в надстройках для SharePoint](http://msdn.microsoft.com/library/800ec8cd-a448-46bc-b41e-d4030eeb4048%28Office.15%29.aspx).
    
  

```XML
  
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction Id="ViewDetailsECBCustomAction"
          RegistrationType="List"
          RegistrationId="107"
          Location="EditControlBlock"
          Sequence="1"
          ImageUrl="_layouts/15/images/placeholder16x16.png"
          Title="View Details">
     <UrlAction Url="~appWebUrl/Pages/ViewDetails.aspx?
            {StandardTokens}&amp;amp;ListId={ListId}&amp;amp;ItemId={ItemId}"/>
  </CustomAction>

  <CustomAction
          Id="ViewDetailsRibbonAction"
          RegistrationId="107"
          RegistrationType="List"
          Location="CommandUI.Ribbon"
          Title="View Details"
          HostWebDialog="false"
          HostWebDialogHeight="500"
          HostWebDialogWidth="500">
    <CommandUIExtension>
      <CommandUIDefinitions>
        <CommandUIDefinition 
              Location="Ribbon.ListItem.Workflow.Controls._children">
          <Button
              Id="Ribbon.ListItem.Workflow.ViewDetails"
              Alt="View Details"
              Sequence="25"
              Command="Invoke_ViewDetailsSAPWorkflow"
              LabelText="View Details"
              TemplateAlias="o1"
              Image32by32="_layouts/15/images/placeholder32x32.png"
              Image16by16="_layouts/15/images/placeholder16x16.png"/>
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler
          Command="Invoke_ViewDetailsSAPWorkflow"
          CommandAction="~appWebUrl/Pages/ViewDetails.aspx?
           {StandardTokens}&amp;amp;ListId={ListId}&amp;amp;ItemId={SelectedItemId}"/>
      </CommandUIHandlers>
    </CommandUIExtension>
  </CustomAction>
</Elements>
```

3. Добавление новой страницы, страницы ViewDetails.aspx в проект.
    
  
4. Нажмите клавишу **F5** для построения и развертывания приложения SharePoint.
    
  
5. Перейдите к списку **рабочих элементов** в веб-узла и выберите команду **Просмотр сведений** в контекстном меню. Вы будете перенаправлены на **ViewDetails.aspx**.
    
  

> **Примечание:** Убедитесь, что службы рабочих процессов SAP позволяет обычной проверки подлинности. BDC для автоматического создания средства в Visual Studio в настоящее время поддерживают только анонимных и обычная проверка подлинности. 
  
    
    

Если развертывание приложения и затем перейдите к **Спискам/WorkflowTaskCollection** внутри приложения, появится следующее сообщение:
  
    
    
"Сообщения из внешней системы: «LobSystem (внешняя система) возвратил ошибку проверки подлинности».".
  
    
    
Чтобы устранить эту проблему, необходимо добавить единого входа в приложение, чтобы задать учетные данные проверки подлинности для BCS и базы данных SAP.
  
    
    

## <a name="add-single-sign-on-security-to-the-app"></a>Добавление безопасности единого входа в приложение
<a name="bkmk_AddSSO"> </a>

Duet Enterprise Single Sign-On позволит пользователям проходить проверку подлинности, чтобы они получают доступ к ресурсам SharePoint и SAP сторон с одного входа в.
  
    
    

### <a name="to-add-single-sign-on"></a>Чтобы добавить единого входа:


1. Создание подключения к OData, выполнив следующую команду в консоли управления SharePoint.
    
```XML
  
New-SPODataConnectionSetting -Name SAPWorkflow
-ServiceContext "http://localhost" -ExtensionProvider 
"OBA.Server.Canary.ObaOdataServerExtensionProvider, OBA.Server.SSOProvider, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" 
-AuthenticationMode passthrough -ServiceAddressURL 
"https://<<DUETGATEWAY>>:<<PORT>>/sap/opu/odata/IWWRK/
DUET_WORKFLOW_CORE;mo;c=SHAREPOINT_DE"

```

2. Дважды щелкните **WorkflowTaskCollection.ect**.
    
  
3. В окне "Свойства" обновите значение  `ODataConnectionSettingId` *SAPWorkflow*  .
    
  
4. Разрешить приложению использовать подключение.
    
  
5. Откройте **файл AppManifest.xml**.
    
  
6. **Запросы разрешений**, выберите **область**, **BCS** затем **разрешение** = чтения.
    
  
7. Нажмите клавишу **F5**, чтобы развернуть приложение.
    
  
8. На странице " **разрешения** " для приложения, выберите подключения OData, которые будут использоваться приложением.
    
  
9. Нажмите кнопку **Trust It (Доверять)**.
    
  
10. Перейдите к **... / Списки/WorkflowTaskCollection**. Вы должны увидеть задачи SAP, назначенных пользователю непосредственно из системы SAP.
    
  

## <a name="access-workflow-tasks-and-associated-items-using-jsom"></a>Доступа к задачам рабочего процесса и связанных элементов, с помощью JSOM
<a name="bkmk_UseJSOM"> </a>

Поскольку Надстройки SharePoint необходимо использовать клиентский код для взаимодействия с SharePoint, ниже показано, как взаимодействовать с задачами рабочего процесса SAP, с помощью объектной модели JavaScript.
  
    
    

### <a name="to-create-the-code"></a>Создание кода:


1. Щелкните правой кнопкой мыши папку **страницы** в **Окне Обозреватель решений**, добавьте на страницу .NET и присвойте ему имя **ViewDetails.aspx**
    
  
2. Вставьте следующий HTML-код в разделе  `PlaceHolderAdditionalPageHead` . Это задание ссылки на таблицы стилей, загрузки сценария и верните задач связанных с ними рабочих процессов из системы SAP.
    
```XML
  
<link
    rel="Stylesheet" 
    type="text/css"
    href="../Content/App.css"/>

<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script 
    src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js" 
    type="text/javascript">
</script>      
<script 
    src="../Scripts/ViewDetails.js" 
    type="text/javascript">
</script>

```

3. Щелкните правой кнопкой мыши папку **скрипты** и добавьте файл JavaScript. Присвойте ему имя **ViewDetails.js**.
    
  
4. Эта разметка выполняет следующие функции:
    
  - Извлекает  `ClientContext` для родительского веб-узла.
    
  
  - Извлекает  `TaskInstanceParentId` для выбранного рабочего процесса задач, с помощью идентификатора GUID Duet рабочий процесс списка и выбранный элемент по идентификатору.
    
  
  - Анализирует  `TaskInstanceParentId` для получения SAP Origin и идентификатор для этого рабочего процесса в SAP.
    
  
  - Загружает сущности для внешних типов контента.
    
  
  - Считывает задачи определенного рабочего процесса из системы SAP, с помощью специальный метод поиска, передав SAP Origin и идентификатор задачи рабочего процесса для SAP в качестве параметров.
    
  
  - Считывает связанных элементов для задачи рабочего процесса из системы SAP.
    
  
5. Ниже приведен полный код HTML и JavaScript для страницы.
    
```
  
// This code runs when the DOM is ready. It ensures the SharePoint
// script files are loaded and then executes execOperation().
$(document).ready(function () {
  SP.SOD.executeFunc("sp.js", "SP.ClientContext", execOperation);
});

function execOperation() {
  retrieveTaskFromList();
}

function retrieveTaskFromList() {
  // Retrieves the ClientContext of the parent web.
  var clientContext = 
  new SP.ClientContext.get_current();
  var appContextSite = 
  new SP.AppContextSite(clientContext, 
      decodeURIComponent(getQueryStringParameter("SPHostUrl")));
  var web = appContextSite.get_web();
  // Loads the selected workflow task from the duet workflow list.
  var listGuid = decodeURIComponent(getQueryStringParameter("ListId"));
  var itemId = decodeURIComponent(getQueryStringParameter("ItemId"))
  this.workflowItem = web.get_lists().getById(
      listGuid.substring(1, listGuid.length - 1)).getItemById(itemId);
  clientContext.load(workflowItem);

  clientContext.executeQueryAsync(
    Function.createDelegate(this, this.onLoadingTaskSucceeded),
    Function.createDelegate(this, this.onError)
  );
}

function onLoadingTaskSucceeded() {
  var sapParameters = parseParentTaskId(workflowItem.
      get_item("TaskInstanceParentId"));
  getDataFromSAP(sapParameters);
}

// Parses the TaskInstanceParentId 
// to get SAP Origin and the id for the workflow in SAP.
function parseParentTaskId(parentTaskId) {
  var idlength = parseInt(parentTaskId.substring(0, 2));
  var sapParameters = new Object();
  if (parentTaskId.length > (17 + idlength)) {
    sapParameters.workitemId = parentTaskId.substring(5, 5 + idlength);
    sapParameters.sapOrigin = parentTaskId.substring(17 + idlength);
  }
  return sapParameters;
}
    
// Retrieves the workflow task and associated elements from SAP.
function getDataFromSAP(sapParameters) {
  context = new SP.ClientContext.get_current();
  //Loads the entities for the external content types.
  wfEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "WorkflowTaskCollection");
  context.load(wfEntity);
  wfExtensibleElementEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "ExtensibleElementCollection");
  context.load(wfExtensibleElementEntity);
  wfCommentsEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "CommentCollection");
  context.load(wfCommentsEntity);
  wfDecisionsEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "DecisionOptionCollection");
  context.load(wfDecisionsEntity);
  wfParticipantEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "ParticipantCollection");
  context.load(wfParticipantEntity);
  wfDescriptionEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "TaskDescriptionCollection");
  context.load(wfDescriptionEntity);
  wfAttachmentEntity = context.get_web().getAppBdcCatalog().
      getEntity("DUET_WORKFLOW_CORE", "AttachmentCollection");
  context.load(wfAttachmentEntity);

  // Loads a LOB system instances.
  lobSystem = wfEntity.getLobSystem();
  lobSystemInstanceCollection = lobSystem.getLobSystemInstances();
  context.load(lobSystemInstanceCollection);

  context.executeQueryAsync(onLoadingLOBInstanceSucceeded, onError);

  function onLoadingLOBInstanceSucceeded() {
    lobSystemInstance = lobSystemInstanceCollection.get_item(0);
    // Reads the workflow task from SAP using specific finder.
    var identifierValues = [sapParameters.sapOrigin, sapParameters.workitemId];
    var entityIdentity = SP.BusinessData.Runtime.EntityIdentity.
          newObject(context, identifierValues);
    wfEntityInstance = wfEntity.findSpecific(entityIdentity, 
          "ReadSpecificWorkflowTask", lobSystemInstance);
    context.load(wfEntityInstance);

    context.executeQueryAsync(onLoadingWorkflowSucceeded, onError);
  }

  function onLoadingWorkflowSucceeded() {
    // Reads the associated elements for the workflow task.
    var exFilterCollection = wfExtensibleElementEntity.getFilters(
        "GetExtensibleElementsFromWorkflowTaskCollection");
    context.load(exFilterCollection);
    exElementsCollection = wfExtensibleElementEntity.findAssociated(
        wfEntityInstance, "GetExtensibleElementsFromWorkflowTaskCollection", 
        exFilterCollection, lobSystemInstance);
    context.load(exElementsCollection);

    var comFilterCollection = wfCommentsEntity.getFilters(
        "GetCommentsFromWorkflowTaskCollection");
    context.load(comFilterCollection);
    commentsCollection = wfCommentsEntity.findAssociated(
        wfEntityInstance, "GetCommentsFromWorkflowTaskCollection", 
        comFilterCollection, lobSystemInstance);
    context.load(commentsCollection);

    var decFilterCollection = wfDecisionsEntity.getFilters(
        "GetDecisionOptionsFromWorkflowTaskCollection");
    context.load(decFilterCollection);
    decisionsCollection = wfDecisionsEntity.findAssociated(
        wfEntityInstance, "GetDecisionOptionsFromWorkflowTaskCollection", 
        decFilterCollection, lobSystemInstance);
    context.load(decisionsCollection);

    var partFilterCollection = wfParticipantEntity.getFilters(
        "GetParticipantsFromWorkflowTaskCollection");
    context.load(partFilterCollection);
    participantsCollection = wfParticipantEntity.findAssociated(
        wfEntityInstance, "GetParticipantsFromWorkflowTaskCollection", 
        partFilterCollection, lobSystemInstance);
    context.load(participantsCollection);

    var descFilterCollection = wfDescriptionEntity.getFilters(
        "GetDescriptionFromWorkflowTaskCollection");
    context.load(descFilterCollection);
    descriptionCollection = wfDescriptionEntity.findAssociated(
        wfEntityInstance, "GetDescriptionFromWorkflowTaskCollection", 
        descFilterCollection, lobSystemInstance);
    context.load(descriptionCollection);

    var attaFilterCollection = wfAttachmentEntity.getFilters(
        "GetAttachmentsFromWorkflowTaskCollection");
    context.load(attaFilterCollection);
    attachmentCollection = wfAttachmentEntity.findAssociated(
        wfEntityInstance, "GetAttachmentsFromWorkflowTaskCollection", 
        attaFilterCollection, lobSystemInstance);
    context.load(attachmentCollection);

    context.executeQueryAsync(getUpdatedDataSucceeded, onError);
  }

  function getUpdatedDataSucceeded() {
    alert("# of extensible elements: " + exElementsCollection.get_count() + 
      "\\n# of comments: " + commentsCollection.get_count() + 
      "\\n# of decision options: " + decisionsCollection.get_count() + 
      "\\n# of attachments: " + attachmentCollection.get_count() + 
      "\\n# of participants: " + participantsCollection.get_count());
  }

  function onError(sender, e) {
    alert("Request failed. " + e.get_message() +
          "\\n" + e.get_stackTrace());
  }
}

// Retrieves a query string value.
function getQueryStringParameter(paramToRetrieve) {
  var params = document.URL.split("")[1].split("&amp;");
  var strParams = "";
  for (var i = 0; i < params.length; i = i + 1) {
    var singleParam = params[i].split("=");
    if (singleParam[0] == paramToRetrieve)
      return singleParam[1];
  }
}

```

6. Откройте файл **AppManifest.xml**.
    
  
7. **Запросы разрешений** в выберите **область**, **веб-серверы и разрешение** и установите значение для *чтения*  .
    
  
8. Нажмите клавишу **F5**, чтобы развернуть решение на сайте рабочего процесса duet.
    
  
9. Перейдите к **задачам рабочего процесса**. Выберите **Просмотр сведений** в ECB-меню или выберите задачи и нажмите **Показать сведения** на ленте. Вы будете перенаправлены на **ViewDetails.aspx**, где появится соответствующее уведомление, содержащий количество для некоторых элементов, связанный с рабочим процессом.
    
  

## <a name="using-html-and-javascript-to-render-custom-ui"></a>С помощью HTML и JavaScript для отображения пользовательского интерфейса
<a name="bkmk_UseJSOM"> </a>

В ViewDetails.aspx замените следующий код HTML и JavaScript для отображения настраиваемого пользовательского интерфейса.
  
    
    

```

alert("# of extensible elements: " + exElementsCollection.get_count() +
"\\n# of comments: " + commentsCollection.get_count() + 
"\\n# of decision options: " + decisionsCollection.get_count() + 
"\\n# of attachments: " + attachmentCollection.get_count() + 
"\\n# of participants: " + participantsCollection.get_count());

```


## <a name="adding-lync-control-to-your-details-page"></a>Добавление элемента управления Lync на страницу сведений
<a name="bkmk_UseJSOM"> </a>

Здесь приводится один параметр для настраиваемого пользовательского интерфейса. Добавление элемента управления Lync даст возможность связи с контактами Lync с настраиваемой страницы.
  
    
    

### <a name="to-add-a-lync-control"></a>Чтобы добавить элемент Lync.


1. Щелкните правой кнопкой мыши папку **скрипты** в окне Обозреватель решений, добавьте файл JavaScript и присвойте ему имя **People.js**.
    
  
2. Следующая разметка выполняет следующие действия:
    
  - Добавление элемента управления сведений о присутствии для участников задачи.
    
  
  - Интеграция Lync в выноске участниками одним щелчком мыши совместной работы для задачи.
    
  

    Вставьте следующий код в **People.js** страницы.
    


```
  
var presenceControlCount = 0;
var appWebURL = '';

function AddPeopleControl(userName) {
  var id = "pc_participants_" + presenceControlCount++;
  var prevId = null;

  return "<div id='" + id + "' ></div>" + 
    "<script>" + 
      "LoadPeopleControl('" +id+ "', '" +prevId+ "', '" +userName+ "');" + 
    "</script>";
}

function LoadPeopleControl(elemId, prevId, user) {
  var prevElement = null;
  var element = $("#" + elemId);
  user = "fareast\\\\" + user.toLowerCase();

  GetUsersInfo(user, element, prevElement);
}

function GetUsersInfo(accountName, htmlElement, waitforElement) {
  var clientContext = SP.ClientContext.get_current();
  var website = clientContext.get_web();

  clientContext.load(website);
  clientContext.executeQueryAsync(onRequestSucceeded, onRequestFailed);

  function onRequestSucceeded() {
    appWebURL = website.get_url();
    var queryURL = appWebURL + 
    "/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)?@v='"
     + accountName + "'";

    jQuery.ajax({
      url: queryURL,
      type: "GET",
      headers: {
        "ACCEPT": "application/json;odata=verbose"
      },
      success: function (data) {
        var html = [];
        var i = 0;

        var id = htmlElement[0].id + "_";

        var about_info;

        if (data.d.UserProfileProperties != null) {
          for (i = 0; i < data.d.UserProfileProperties.results.length; i++) {
            if (data.d.UserProfileProperties.results[i].Key == "AboutMe") {
              about_info = data.d.UserProfileProperties.results[i].Value;
            }
          }
        }

        var email = data.d.Email;
        var profileUrl = data.d.UserUrl;
        var pictureUrl = data.d.PictureUrl;
        var name = data.d.DisplayName;

        if (name == null) {
          name = accountName;
        }

        var isFollowed = data.d.IsFollowed;

        var html = [
          "<table>",
          "<tr>",
          "<td>",
            "<span class='ms-spimn-presenceWrapper ms-spimn-imgSize-5x48'> ",
              "<img id='imn_" + id + "_" + i++ + ",type=smtp'" ,
                "onload=\\"IMNRC('", email, "')\\" ",
                "class='ms-spimn-img ms-spimn-presence-offline-5x48x32 '", 
                "title='' name='imnmark' alt='Offline' ", 
                "src='/_layouts/15/images/spimn.png' ", 
                "sip='" + email + "' showofflinepawn='1'>",
            "</span>",
          "</td>",
          "<td>",
            "<span class='ms-imnSpan'>",
              "<a class='ms-imnlink' tabindex='-1'", 
                "onclick='IMNImageOnClick(event);return false;' href='#'>",
                "<img id='imn_" + id + "_" + i++ + ",type=smtp'",
                  "onload=\\"IMNRC('", email, "')\\"",
                  "class=' ms-hide' title='' name='imnmark' alt='Away' ",
                  "src='/_layouts/15/images/spimn.png' ",
                  "sip='" + email + "' showofflinepawn='1'>",
              "</a>",
              "<a class='ms-subtleLink ms-peopleux-imgUserLink' ",
                "onclick='GoToLinkOrDialogNewWindow(this);return false;' ",
                "href='" + profileUrl + "'>",
                "<span style='width: 48px; height: 48px;'" ,
                  "class='ms-peopleux-userImgWrapper'>",
                "<img style='cliptop: 0px; clipright: 48px;" ,
                  "clipbottom: 48px; clipleft: 0px; ",
                  "min-height: 48px; min-width: 48px; max-width: 48px;' ",
                  "class='ms-peopleux-userImg' alt='' src='" +pictureUrl+ "'>",
                "</span>",
              "</a>",
            "</span>",
          "</td>",
          "<td>",
            "<span class='ms-spimn-presenceWrapper ms-spimn-imgSize-5x48'>",
            "<img id='imn_" + id + "_" + i++ + ",type=smtp' ",
              "onload=\\"IMNRC('", email, "')\\" ",
              "class='ms-spimn-img ms-spimn-presence-offline-5x48x32' ",
              "title='' name='imnmark' alt='Offline' ",
              "src='/_layouts/15/images/spimn.png' ",
              "sip='" + email + "' showofflinepawn='1'>",
            "</span>",
          "</td>",
          "<td>",
            "<span class='ms-microfeed-userName ms-textLarge' ",
              "style='font-size: medium;'>" + name + "<br/>",
              "<div id='people_callout_" + id + "_" + i + "' ",
                "class='ms-microfeed-button ms-textSmall" + 
                "ms-secondaryCommandLink ms-microfeed-footerButton' ",
                "align='center' ",
                "style='cursor:pointer; font-size:small;' > more... </div>",
                  "<script>",
                    "RegisterCallOut(\\"people_callout_" + id + "_" + i + 
                      "\\",\\"" + name + "\\",\\"" + encodeURI(about_info) + 
                      "\\",\\"" + profileUrl + "\\",\\"" + isFollowed + "\\");",
                  "</script>",
            "</span>",
          "</td>",
          "</tr>",
          "</table>",
        ];

        htmlElement.html(html.join(''));
      }

    });
  }
  function onRequestFailed(sender, args) {
    alert('Error: ' + args.get_message());
  }

}

function RegisterCallOut(divId, displayName, aboutme, userUrl, isFollowed) {
  if (typeof CalloutManager !== "object" || typeof Callout !== "function" || typeof CalloutAction !== "function")
    return;

  var launchdiv = document.getElementById(divId);
  var calloutId = divId + "_callout";
  var html = [];

  html.push("<br/>");

  if (aboutme == "") {
    html.push("No Information Found about this person.");
  }
  else {
    html.push(decodeURI(aboutme));
  }

  html.push("<hr/>");

  if (isFollowed == true) {
    html.push("<div>You are <b>following</b> this person</div>");
  }
  else {
    html.push("<div >You are <b>not following</b> this person</div>");
  }

  var callout = CalloutManager.createNew({
    launchPoint: launchdiv,
    openOptions: {
      closeCalloutOnBlur: true,
      event: "click",
      showCloseButton: true
    },
    ID: calloutId,
    title: displayName,
    content: html.join("")
  });

  callout.addAction(new CalloutAction({
    text: "View Profile", onClickCallback: 
    function (calloutActionClickEvent, calloutAction) {
      window.open(userUrl);
    }
  }));
}

```


    > **Note:**
      > The user name of the participant in company's network is same as that in SAP. 
3. Откройте страницу **AppManifest.xml**.
    
  
4. **Запросы разрешений** в выберите **область**, **Профили пользователей и разрешений** и присвойте ей значение *чтения*  .
    
  
5. Скопируйте следующую разметку и вставьте его в разделе  `PlaceHolderAdditionalPageHead` в **ViewDetails.aspx**.
    
```HTML
  
<script src="../Scripts/People.js" type="text/javascript"></script>
```

6. Чтобы добавить элемент управления сведений о присутствии для участника, вызовите следующее: 
    
```
  AddPeopleControl(userName);
```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [Общие сведения о рабочих процессов SAP Business](http://scn.sap.com/docs/DOC-31056)
    
  

