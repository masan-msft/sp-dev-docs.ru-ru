---
title: "Использование рабочего процесса SAP в Duet Enterprise 2.0"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 816e28ed-8cea-4e33-98e5-d3d27136e2e6
ms.openlocfilehash: 77e613f09c0d51da7d7c00c7be76b3cd8028a0b7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-sap-workflow-with-duet-enterprise-20"></a><span data-ttu-id="0c0e7-102">Использование рабочего процесса SAP в Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="0c0e7-102">Use SAP workflow with Duet Enterprise 2.0</span></span>

## <a name="introduction"></a><span data-ttu-id="0c0e7-103">Введение</span><span class="sxs-lookup"><span data-stu-id="0c0e7-103">Introduction</span></span>
<span data-ttu-id="0c0e7-104"><a name="bkmk_Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-104"><a name="bkmk_Introduction"> </a></span></span>

<span data-ttu-id="0c0e7-105">Рабочий процесс SAP Business предоставляет способ для автоматизации бизнес-процессов и с Duet Enterprise 2.0 эти рабочие процессы можно интегрировать в пределах Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-105">SAP Business Workflow provides a way to automate business processes, and with Duet Enterprise 2.0, those workflows can be integrated within an SharePoint Add-in.</span></span>
  
    
    
<span data-ttu-id="0c0e7-106">Далее показано, как создать приложение, настроить его, а затем способ отображения данные извлекаются из рабочих процессов SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-106">The following steps show how to create an app, configure it, and then how to display the information retrieved from the SAP workflows.</span></span>
  
    
    

## <a name="create-an-app-for-sharepoint-and-duet-enterprise-20"></a><span data-ttu-id="0c0e7-107">Создание приложения для SharePoint и Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="0c0e7-107">Create an app for SharePoint and Duet Enterprise 2.0</span></span>
<span data-ttu-id="0c0e7-108"><a name="bkmk_CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-108"><a name="bkmk_CreateApp"> </a></span></span>

<span data-ttu-id="0c0e7-109">Первым шагом является создание Надстройка SharePoint, которая будет содержать данные для подключения с помощью внешнего типа контента для Службы Business Connectivity Services (BCS), с помощью внешних списков и все настройки, вы можете использовать для представления данных.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-109">The first step is to create an SharePoint Add-in that will contain the connection information using an external content type for Business Connectivity Services (BCS), external lists and any customizations you might want to use to present the data.</span></span>
  
    
    

### <a name="to-create-an-app-for-sharepoint"></a><span data-ttu-id="0c0e7-110">Создание приложения для SharePoint:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-110">To create an app for SharePoint:</span></span>


1. <span data-ttu-id="0c0e7-111">Запустите Visual Studio 2012 от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-111">Start Visual Studio 2012 as an administrator.</span></span>
    
  
2. <span data-ttu-id="0c0e7-112">Выберите **файл**, **новый**, **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-112">Choose **File**, **New**, **New Project**.</span></span>
    
  
3. <span data-ttu-id="0c0e7-113">В диалоговом окне **Новый проект** разверните узел **Visual C#**, разверните узел **Office/SharePoint** и затем выберите узел **приложения**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-113">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then choose the **Apps** node.</span></span>
    
  
4. <span data-ttu-id="0c0e7-114">Выберите **приложение для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-114">Choose **App for SharePoint**.</span></span>
    
  
5. <span data-ttu-id="0c0e7-115">Назовите проект и нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-115">Name the project and click **OK**.</span></span>
    
  
6. <span data-ttu-id="0c0e7-p101">В диалоговом окне **Укажите приложение для настройки SharePoint** первого имя приложения и выберите **Размещение в SharePoint** в списке **как разместить приложение для SharePoint**. Также укажите URL-адрес **сайта рабочего процесса Duet** требуется отладки в списке **какой сайт SharePoint использовать для отладки приложения** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p101">In the first **Specify the App for SharePoint Settings** dialog box, name your app and choose **SharePoint-hosted** under **How do you want to host your app for SharePoint**. Also specify the URL of the **Duet Workflow site** you want to debug against under **What SharePoint site do you want to use for debugging your app** and choose **Finish**.</span></span>
    
  
7. <span data-ttu-id="0c0e7-118">В меню Построение выберите команду **Развернуть** * \<имя вашего приложения\> * .</span><span class="sxs-lookup"><span data-stu-id="0c0e7-118">On the Build menu, choose **Deploy** *\<your app name\>*  .</span></span>
    
  
<span data-ttu-id="0c0e7-119">После развертывания приложения Visual Studio запустит страницу по умолчанию для приложения.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-119">After the app is deployed, Visual Studio will launch the default page for the app.</span></span>
  
    
    

## <a name="add-the-external-content-type-and-external-lists-to-the-app"></a><span data-ttu-id="0c0e7-120">Добавление внешнего типа контента и внешних списков для приложения</span><span class="sxs-lookup"><span data-stu-id="0c0e7-120">Add the external content type and external lists to the app</span></span>
<span data-ttu-id="0c0e7-121"><a name="bkmk_AddECT"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-121"><a name="bkmk_AddECT"> </a></span></span>

<span data-ttu-id="0c0e7-p102">BCS должна состоять принять во внимание к внешнему источнику данных. Это делается с помощью внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p102">BCS must be made aware of the external data source. This is done using an external content type.</span></span>
  
    
    

### <a name="to-add-an-external-content-type"></a><span data-ttu-id="0c0e7-124">Чтобы добавить внешний тип контента:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-124">To add an external content type:</span></span>


1. <span data-ttu-id="0c0e7-125">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-125">In the **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
  
2. <span data-ttu-id="0c0e7-p103">На странице **Укажите источника OData** введите URL-адрес службы рабочих процессов Duet Enterprise. Ниже приведен пример URL-адрес службы Duet:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p103">On the **Specify OData Source** page, enter the URL of the Duet Enterprise Workflow Service. The following is an example of a Duet service URL:</span></span>
    
     <span data-ttu-id="0c0e7-128">*https://\<\<DUETGATEWAY\>\>:\<\<ПОРТ\>\>/sap/opu/odata/IWWRK/DUET_WORKFLOW_CORE, режим, c = SHAREPOINT_DE*</span><span class="sxs-lookup"><span data-stu-id="0c0e7-128">*https://\<\<DUETGATEWAY\>\>:\<\<PORT\>\>/sap/opu/odata/IWWRK/DUET_WORKFLOW_CORE;mo;c=SHAREPOINT_DE*</span></span> 
    
  
3. <span data-ttu-id="0c0e7-129">Выберите имя для источника ODATA, например, SAPWorkflows и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-129">Choose a name for your ODATA source, for example, SAPWorkflows, and then choose **Next**.</span></span>
    
  
4. <span data-ttu-id="0c0e7-130">Укажите имя пользователя SAP и пароль для подключения к службе метаданных.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-130">Specify the SAP username and password to connect to the service metadata.</span></span>
    
  
5. <span data-ttu-id="0c0e7-p104">Появится список сущностей данные, предоставляемые интерфейсом службы OData. Выбор сущностей, которые вы хотите включить в внешнего типа контента. В этом примере с помощью служб рабочих процессов SAP выполните одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p104">A list of data entities that are being exposed by the OData Service appears. Select the entities you wish to include in the external content type. In this example, using the SAP workflow services, select from the following:</span></span>
    
  - <span data-ttu-id="0c0e7-134">**AttachmentCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-134">**AttachmentCollection**</span></span>
    
  
  - <span data-ttu-id="0c0e7-135">**CommentCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-135">**CommentCollection**</span></span>
    
  
  - <span data-ttu-id="0c0e7-136">**DecisionOptionCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-136">**DecisionOptionCollection**</span></span>
    
  
  - <span data-ttu-id="0c0e7-137">**ExtensibleElementCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-137">**ExtensibleElementCollection**</span></span>
    
  
  - <span data-ttu-id="0c0e7-138">**ParticipantCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-138">**ParticipantCollection**</span></span>
    
  
  - <span data-ttu-id="0c0e7-139">**ServiceOperations**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-139">**ServiceOperations**</span></span>
    
  
  - <span data-ttu-id="0c0e7-140">**TaskDescriptionCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-140">**TaskDescriptionCollection**</span></span>
    
  
  - <span data-ttu-id="0c0e7-141">**WorkflowTaskCollection**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-141">**WorkflowTaskCollection**</span></span>
    
  
6. <span data-ttu-id="0c0e7-142">Установите флажок **создать экземпляры списков для выбранных данных сущностей (за исключением операции службы)**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-142">Select the **Create list instances for the selected data entities (except Service Operations)** check box.</span></span>
    
  
7. <span data-ttu-id="0c0e7-143">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-143">Choose **Finish**.</span></span>
    
  

> [!NOTE]
> <span data-ttu-id="0c0e7-144">[!Примечание] Убедитесь, что службы рабочих процессов SAP позволяет обычной проверки подлинности, как средства для автоматического создания BDC в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-144">Make sure SAP workflow service allows basic authentication as the BDC auto-generation tools in Visual Studio.</span></span> 
  
    
    


## <a name="add-a-custom-action-feature-to-a-duet-enterprise-20-workflow-list"></a><span data-ttu-id="0c0e7-145">Добавьте компонент дополнительного действия со списком Duet Enterprise 2.0 рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="0c0e7-145">Add a custom action feature to a Duet Enterprise 2.0 workflow list</span></span>
<span data-ttu-id="0c0e7-146"><a name="bkmk_AddCustomAction"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-146"><a name="bkmk_AddCustomAction"> </a></span></span>

<span data-ttu-id="0c0e7-147">Для предоставления позволяет пользователю работать с новыми функциональными возможностями, добавленные в список SharePoint, следующие шаги будут добавить элемент в меню Действия сайта.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-147">In order to provide a way for the user to work with the new functionality added to a SharePoint list, the following steps will add an item to the Site Actions menu.</span></span>
  
    
    

### <a name="to-add-a-custom-action"></a><span data-ttu-id="0c0e7-148">Добавление настраиваемых действий:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-148">To add a custom action:</span></span>


1. <span data-ttu-id="0c0e7-149">Щелкните правой кнопкой мыши проект Надстройка SharePoint и добавьте новый элемент **UI Custom Action (Дополнительное действие пользовательского интерфейса)**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-149">Right-click the SharePoint Add-in project, and add a new **UI Custom Action** item.</span></span>
    
  
2. <span data-ttu-id="0c0e7-p105">Откройте файл **Elements.xml** компонента дополнительного действия узла web. Путем замены код в файл следующий XML-код, будет настраиваемого действия:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p105">Open the **Elements.xml** file of the custom action host web feature. By replacing the code in the file with the following XML, the custom action will:</span></span>
    
  - <span data-ttu-id="0c0e7-152">Объявите дополнительное действие ECB и его атрибуты.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-152">Declare an ECB custom action and its attributes.</span></span>
    
  
  - <span data-ttu-id="0c0e7-153">Объявите дополнительное действие ленты и его атрибуты.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-153">Declare a Ribbon custom action and its attributes.</span></span>
    
  
  - <span data-ttu-id="0c0e7-154">Объявите конечного приложения веб-страницы и значения, которые передаются в строке запроса.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-154">Declare the app webpage target and the values that are passed to it through the query string.</span></span> 
    
    <span data-ttu-id="0c0e7-p106">Элемент **UrlAction** использует несколько токенов. Для получения дополнительных сведений см [Строки URL и маркеры в надстройках для SharePoint](http://msdn.microsoft.com/library/800ec8cd-a448-46bc-b41e-d4030eeb4048%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p106">The **UrlAction** element uses several tokens. For more information, see [URL strings and tokens in SharePoint Add-ins](http://msdn.microsoft.com/library/800ec8cd-a448-46bc-b41e-d4030eeb4048%28Office.15%29.aspx).</span></span>
    
  

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

3. <span data-ttu-id="0c0e7-157">Добавление новой страницы, страницы ViewDetails.aspx в проект.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-157">Add a new page, ViewDetails.aspx page to the project.</span></span>
    
  
4. <span data-ttu-id="0c0e7-158">Нажмите клавишу **F5** для построения и развертывания приложения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-158">Press **F5** to build and deploy the SharePoint app.</span></span>
    
  
5. <span data-ttu-id="0c0e7-p107">Перейдите к списку **рабочих элементов** в веб-узла и выберите команду **Просмотр сведений** в контекстном меню. Вы будете перенаправлены на **ViewDetails.aspx**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p107">Go to the **WorkItem** list in the host web and choose **View Details** in the context menu. You will be redirected to **ViewDetails.aspx**.</span></span>
    
> [!NOTE]
> <span data-ttu-id="0c0e7-p108">[!Примечание] Убедитесь, что службы рабочих процессов SAP позволяет обычной проверки подлинности. BDC для автоматического создания средства в Visual Studio в настоящее время поддерживают только анонимных и обычная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p108">Make sure the SAP workflow service allows basic authentication. The BDC auto-generation tools in Visual Studio currently only support anonymous and basic authentication.</span></span> 
  
    
    

<span data-ttu-id="0c0e7-163">Если развертывание приложения и затем перейдите к **Спискам/WorkflowTaskCollection** внутри приложения, появится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-163">If you deploy the app and then navigate to **Lists/WorkflowTaskCollection** inside your app, you will see the following message:</span></span>
  
    
    
<span data-ttu-id="0c0e7-164">"Сообщения из внешней системы: «LobSystem (внешняя система) возвратил ошибку проверки подлинности».".</span><span class="sxs-lookup"><span data-stu-id="0c0e7-164">"Message from External System: 'LobSystem (External System) returned authentication error.'".</span></span>
  
    
    
<span data-ttu-id="0c0e7-165">Чтобы устранить эту проблему, необходимо добавить единого входа в приложение, чтобы задать учетные данные проверки подлинности для BCS и базы данных SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-165">To fix this, you will need to add single sign-on to the app to provide authentication credentials to BCS and the SAP backend.</span></span>
  
    
    

## <a name="add-single-sign-on-security-to-the-app"></a><span data-ttu-id="0c0e7-166">Добавление безопасности единого входа в приложение</span><span class="sxs-lookup"><span data-stu-id="0c0e7-166">Add single sign-on security to the app</span></span>
<span data-ttu-id="0c0e7-167"><a name="bkmk_AddSSO"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-167"><a name="bkmk_AddSSO"> </a></span></span>

<span data-ttu-id="0c0e7-168">Duet Enterprise Single Sign-On позволит пользователям проходить проверку подлинности, чтобы они получают доступ к ресурсам SharePoint и SAP сторон с одного входа в.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-168">Duet Enterprise Single Sign-On will allow users to be authenticated so that they can access resources on both the SharePoint and SAP sides with one sign in.</span></span>
  
    
    

### <a name="to-add-single-sign-on"></a><span data-ttu-id="0c0e7-169">Чтобы добавить единого входа:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-169">To add single sign-on:</span></span>


1. <span data-ttu-id="0c0e7-170">Создание подключения к OData, выполнив следующую команду в консоли управления SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-170">Create an OData connection by executing the following command on the SharePoint Management Shell.</span></span>
    
```XML
  
New-SPODataConnectionSetting -Name SAPWorkflow
-ServiceContext "http://localhost" -ExtensionProvider 
"OBA.Server.Canary.ObaOdataServerExtensionProvider, OBA.Server.SSOProvider, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" 
-AuthenticationMode passthrough -ServiceAddressURL 
"https://<<DUETGATEWAY>>:<<PORT>>/sap/opu/odata/IWWRK/
DUET_WORKFLOW_CORE;mo;c=SHAREPOINT_DE"

```

2. <span data-ttu-id="0c0e7-171">Дважды щелкните **WorkflowTaskCollection.ect**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-171">Double click on **WorkflowTaskCollection.ect**.</span></span>
    
  
3. <span data-ttu-id="0c0e7-172">В окне "Свойства" обновите значение  `ODataConnectionSettingId` *SAPWorkflow*  .</span><span class="sxs-lookup"><span data-stu-id="0c0e7-172">In the Properties window, update the value of  `ODataConnectionSettingId` to *SAPWorkflow*  .</span></span>
    
  
4. <span data-ttu-id="0c0e7-173">Разрешить приложению использовать подключение.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-173">Allow the App to use the Connection.</span></span>
    
  
5. <span data-ttu-id="0c0e7-174">Откройте **файл AppManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-174">Open the **AppManifest.xml**.</span></span>
    
  
6. <span data-ttu-id="0c0e7-175">**Запросы разрешений**, выберите **область**, **BCS** затем **разрешение** = чтения.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-175">In **Permission Requests**, select **Scope**, **BCS** then **Permission** = Read.</span></span>
    
  
7. <span data-ttu-id="0c0e7-176">Нажмите клавишу **F5**, чтобы развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-176">Press **F5** to deploy the app.</span></span>
    
  
8. <span data-ttu-id="0c0e7-177">На странице " **разрешения** " для приложения, выберите подключения OData, которые будут использоваться приложением.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-177">On the **Permissions** page for the app, select the OData connection this app will use.</span></span>
    
  
9. <span data-ttu-id="0c0e7-178">Нажмите кнопку **Trust It (Доверять)**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-178">Choose the **Trust It** button.</span></span>
    
  
10. <span data-ttu-id="0c0e7-p109">Перейдите к **... / Списки/WorkflowTaskCollection**. Вы должны увидеть задачи SAP, назначенных пользователю непосредственно из системы SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p109">Navigate to **../Lists/WorkflowTaskCollection**. You should see the SAP tasks assigned to you coming directly from the SAP system.</span></span>
    
  

## <a name="access-workflow-tasks-and-associated-items-using-jsom"></a><span data-ttu-id="0c0e7-181">Доступа к задачам рабочего процесса и связанных элементов, с помощью JSOM</span><span class="sxs-lookup"><span data-stu-id="0c0e7-181">Access workflow tasks and associated items using JSOM</span></span>
<span data-ttu-id="0c0e7-182"><a name="bkmk_UseJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-182"><a name="bkmk_UseJSOM"> </a></span></span>

<span data-ttu-id="0c0e7-183">Поскольку Надстройки SharePoint необходимо использовать клиентский код для взаимодействия с SharePoint, ниже показано, как взаимодействовать с задачами рабочего процесса SAP, с помощью объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-183">Since SharePoint Add-ins must use client code to communicate with SharePoint, the following will demonstrate how to interact with the SAP workflow tasks using the JavaScript object model.</span></span>
  
    
    

### <a name="to-create-the-code"></a><span data-ttu-id="0c0e7-184">Создание кода:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-184">To create the code:</span></span>


1. <span data-ttu-id="0c0e7-185">Щелкните правой кнопкой мыши папку **страницы** в **Окне Обозреватель решений**, добавьте на страницу .NET и присвойте ему имя **ViewDetails.aspx**</span><span class="sxs-lookup"><span data-stu-id="0c0e7-185">Right-click the **Pages** folder in the **Solution Explorer**, add a .NET page and name it **ViewDetails.aspx**</span></span>
    
  
2. <span data-ttu-id="0c0e7-p110">Вставьте следующий HTML-код в разделе  `PlaceHolderAdditionalPageHead` . Это задание ссылки на таблицы стилей, загрузки сценария и верните задач связанных с ними рабочих процессов из системы SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p110">Paste the following HTML in the  `PlaceHolderAdditionalPageHead` section. This will set the style sheet reference, load the script and then return the related workflow tasks from SAP.</span></span>
    
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

3. <span data-ttu-id="0c0e7-p111">Щелкните правой кнопкой мыши папку **скрипты** и добавьте файл JavaScript. Присвойте ему имя **ViewDetails.js**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p111">Right-click the **Scripts** folder and add a JavaScript file. Name it **ViewDetails.js**.</span></span>
    
  
4. <span data-ttu-id="0c0e7-190">Эта разметка выполняет следующие функции:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-190">This markup will do the following:</span></span>
    
  - <span data-ttu-id="0c0e7-191">Извлекает  `ClientContext` для родительского веб-узла.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-191">Retrieves the  `ClientContext` for the parent web.</span></span>
    
  
  - <span data-ttu-id="0c0e7-192">Извлекает  `TaskInstanceParentId` для выбранного рабочего процесса задач, с помощью идентификатора GUID Duet рабочий процесс списка и выбранный элемент по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-192">Retrieves the  `TaskInstanceParentId` for the selected workflow task using the Duet workflow list GUID and the selected item ID.</span></span>
    
  
  - <span data-ttu-id="0c0e7-193">Анализирует  `TaskInstanceParentId` для получения SAP Origin и идентификатор для этого рабочего процесса в SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-193">Parses the  `TaskInstanceParentId` to get SAP Origin and the ID for the workflow in SAP.</span></span>
    
  
  - <span data-ttu-id="0c0e7-194">Загружает сущности для внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-194">Loads the entities for the external content types.</span></span>
    
  
  - <span data-ttu-id="0c0e7-195">Считывает задачи определенного рабочего процесса из системы SAP, с помощью специальный метод поиска, передав SAP Origin и идентификатор задачи рабочего процесса для SAP в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-195">Reads the specific workflow task from SAP using specific finder by passing SAP Origin and the workflow task ID for SAP as parameters.</span></span>
    
  
  - <span data-ttu-id="0c0e7-196">Считывает связанных элементов для задачи рабочего процесса из системы SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-196">Reads the associated elements for the workflow task from SAP.</span></span>
    
  
5. <span data-ttu-id="0c0e7-197">Ниже приведен полный код HTML и JavaScript для страницы.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-197">The following is the complete HTML and JavaScript for the page.</span></span>
    
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

6. <span data-ttu-id="0c0e7-198">Откройте файл **AppManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-198">Open the **AppManifest.xml** file.</span></span>
    
  
7. <span data-ttu-id="0c0e7-199">**Запросы разрешений** в выберите **область**, **веб-серверы и разрешение** и установите значение для *чтения*  .</span><span class="sxs-lookup"><span data-stu-id="0c0e7-199">In **Permission Requests**, select **Scope**, **Web and Permission** and set the value to *Read*  .</span></span>
    
  
8. <span data-ttu-id="0c0e7-200">Нажмите клавишу **F5**, чтобы развернуть решение на сайте рабочего процесса duet.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-200">Press **F5** to deploy the solution to the duet workflow site.</span></span>
    
  
9. <span data-ttu-id="0c0e7-p112">Перейдите к **задачам рабочего процесса**. Выберите **Просмотр сведений** в ECB-меню или выберите задачи и нажмите **Показать сведения** на ленте. Вы будете перенаправлены на **ViewDetails.aspx**, где появится соответствующее уведомление, содержащий количество для некоторых элементов, связанный с рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p112">Go to **My Workflow Tasks**. Select **View Details** in the ECB menu or select a task and press **View Details** in the ribbon. You will be redirected to **ViewDetails.aspx** where you will see an alert containing the count for some of the elements associated to the workflow.</span></span>
    
  

## <a name="using-html-and-javascript-to-render-custom-ui"></a><span data-ttu-id="0c0e7-204">С помощью HTML и JavaScript для отображения пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0c0e7-204">Using HTML and JavaScript to render Custom UI</span></span>
<span data-ttu-id="0c0e7-205"><a name="bkmk_UseJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-205"><a name="bkmk_UseJSOM"> </a></span></span>

<span data-ttu-id="0c0e7-206">В ViewDetails.aspx замените следующий код HTML и JavaScript для отображения настраиваемого пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-206">In ViewDetails.aspx, replace the following code with your own HTML and JavaScript to render your own custom UI.</span></span>
  
    
    

```

alert("# of extensible elements: " + exElementsCollection.get_count() +
"\\n# of comments: " + commentsCollection.get_count() + 
"\\n# of decision options: " + decisionsCollection.get_count() + 
"\\n# of attachments: " + attachmentCollection.get_count() + 
"\\n# of participants: " + participantsCollection.get_count());

```


## <a name="adding-lync-control-to-your-details-page"></a><span data-ttu-id="0c0e7-207">Добавление элемента управления Lync на страницу сведений</span><span class="sxs-lookup"><span data-stu-id="0c0e7-207">Adding Lync Control to your details page</span></span>
<span data-ttu-id="0c0e7-208"><a name="bkmk_UseJSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-208"><a name="bkmk_UseJSOM"> </a></span></span>

<span data-ttu-id="0c0e7-p113">Здесь приводится один параметр для настраиваемого пользовательского интерфейса. Добавление элемента управления Lync даст возможность связи с контактами Lync с настраиваемой страницы.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-p113">Here is one option for your custom user interface. Adding a Lync control will give you the ability to communicate with your Lync contacts from the custom page.</span></span>
  
    
    

### <a name="to-add-a-lync-control"></a><span data-ttu-id="0c0e7-211">Чтобы добавить элемент Lync.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-211">To add a Lync control:</span></span>


1. <span data-ttu-id="0c0e7-212">Щелкните правой кнопкой мыши папку **скрипты** в окне Обозреватель решений, добавьте файл JavaScript и присвойте ему имя **People.js**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-212">Right-click the **Scripts** folder in solution explorer, add a JavaScript file and name it **People.js**.</span></span>
    
  
2. <span data-ttu-id="0c0e7-213">Следующая разметка выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-213">The following markup will:</span></span>
    
  - <span data-ttu-id="0c0e7-214">Добавление элемента управления сведений о присутствии для участников задачи.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-214">Add presence control for the participants of the task.</span></span>
    
  
  - <span data-ttu-id="0c0e7-215">Интеграция Lync в выноске участниками одним щелчком мыши совместной работы для задачи.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-215">Lync integration in callout for participants for one-click collaboration for the task.</span></span>
    
  

    <span data-ttu-id="0c0e7-216">Вставьте следующий код в **People.js** страницы.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-216">Paste the following code into the **People.js** page.</span></span>
    


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


> [!NOTE]
> <span data-ttu-id="0c0e7-217">[!Примечание] Имя участника в сети компании же, что и в SAP.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-217">The user name of the participant in company's network is same as that in SAP.</span></span>

3. <span data-ttu-id="0c0e7-218">Откройте страницу **AppManifest.xml**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-218">Open the **AppManifest.xml** page.</span></span>
    
  
4. <span data-ttu-id="0c0e7-219">**Запросы разрешений** в выберите **область**, **Профили пользователей и разрешений** и присвойте ей значение *чтения*  .</span><span class="sxs-lookup"><span data-stu-id="0c0e7-219">In **Permission Requests**, select **Scope**, **User Profiles and Permission** and set its value to *Read*  .</span></span>
    
  
5. <span data-ttu-id="0c0e7-220">Скопируйте следующую разметку и вставьте его в разделе  `PlaceHolderAdditionalPageHead` в **ViewDetails.aspx**.</span><span class="sxs-lookup"><span data-stu-id="0c0e7-220">Copy the following markup and paste it in the  `PlaceHolderAdditionalPageHead` section in **ViewDetails.aspx**.</span></span>
    
```HTML
  
<script src="../Scripts/People.js" type="text/javascript"></script>
```

6. <span data-ttu-id="0c0e7-221">Чтобы добавить элемент управления сведений о присутствии для участника, вызовите следующее:</span><span class="sxs-lookup"><span data-stu-id="0c0e7-221">To add the presence control for a participant, call the following:</span></span> 
    
```
  AddPeopleControl(userName);
```


## <a name="see-also"></a><span data-ttu-id="0c0e7-222">См. также</span><span class="sxs-lookup"><span data-stu-id="0c0e7-222">See also</span></span>
<span data-ttu-id="0c0e7-223"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0c0e7-223"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="0c0e7-224">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c0e7-224">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0c0e7-225">Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c0e7-225">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0c0e7-226">Общие сведения о рабочих процессов SAP Business</span><span class="sxs-lookup"><span data-stu-id="0c0e7-226">An introduction to SAP Business Workflow</span></span>](http://scn.sap.com/docs/DOC-31056)
    
  

