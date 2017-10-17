---
title: "Обновление компонентов сайта с надстройкой в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ad72f237e3c6ddb9d45c723a65c6225b02119314
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-add-in-web-components-in-sharepoint"></a><span data-ttu-id="42a1d-102">Обновление компонентов сайта с надстройкой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="42a1d-102">Update add-in web components in SharePoint</span></span>
<span data-ttu-id="42a1d-103">В этой статье рассказывается, как обновлять страницы, списки, типы контента и другие компоненты сайта надстройки в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="42a1d-103">Update pages, lists, content types, and other add-in web components in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="42a1d-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="42a1d-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites-for-updating-the-add-in-web-components"></a><span data-ttu-id="42a1d-107">Компоненты, необходимые для обновления компонентов сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-107">Prerequisites for updating the add-in web components</span></span>
<span data-ttu-id="42a1d-108"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="42a1d-108"></span></span>

<span data-ttu-id="42a1d-109">Изучите статью [Обновление надстроек SharePoint](update-sharepoint-add-ins.md) и ознакомьтесь со списком необходимых компонентов и основными понятиями, описанными в этой статье.</span><span class="sxs-lookup"><span data-stu-id="42a1d-109">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts included in it.</span></span>
 

 
<span data-ttu-id="42a1d-110">В этом разделе предполагается, что вы разработали и протестировали последнюю версию надстройки, как это описано в статье  [Создание и отладка новой версии в качестве новой надстройки](update-sharepoint-add-ins.md#DebugFirst).</span><span class="sxs-lookup"><span data-stu-id="42a1d-110">This topic assumes that you have developed and tested the latest version of the add-in as described in the  [Create and debug the new version as if it were a brand new add-in](update-sharepoint-add-ins.md#DebugFirst).</span></span>
 

 

## <a name="update-sharepoint-components-in-the-add-in-web"></a><span data-ttu-id="42a1d-111">Обновление компонентов SharePoint на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-111">Update SharePoint components in the add-in web</span></span>
<span data-ttu-id="42a1d-112"><a name="UpdatingAppWeb"> </a></span><span class="sxs-lookup"><span data-stu-id="42a1d-112"></span></span>

<span data-ttu-id="42a1d-p102">Все элементы SharePoint, развернутые на сайте надстройки, содержатся в компонентах области **Web** (Интернет) в пакете надстройки, поэтому для обновления этих элементов необходимо обновить один или несколько компонентов. Этот процесс не изменился со времени выпуска SharePoint 2010 и описан в статье [Практическое руководство. Добавление элементов к существующему компоненту](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) в пакете SDK для SharePoint 2010. Другие статьи, указанные в узле [Обновление компонентов](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx), также могут пригодиться, но учтите, что надстройки не должны включать пользовательский код на сервере SharePoint, поэтому некоторые аспекты обновления компонентов в SharePoint 2010 не относятся к обновлению надстроек. Например, вам не удастся использовать элемент [CustomUpgradeAction](http://msdn.microsoft.com/library/16a2182e-80aa-4184-8071-8f717ee5c572%28Office.15%29.aspx) при обновлении компонента надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p102">All of the SharePoint components that are deployed to the add-in web are contained in  **Web**-scoped Features in the add-in package. For that reason, updating these components is a matter of updating one or more of the Features. This process has not changed since SharePoint 2010 and is documented in  [How to: Add Elements to an Existing Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) in the SharePoint 2010 SDK. Other articles in the [Upgrading Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) node may be helpful also, but consider that add-ins must not include custom code on the SharePoint server, so some aspects of Feature upgrading in SharePoint 2010 are not relevant to updating add-ins. For example, you can't use the [CustomUpgradeAction](http://msdn.microsoft.com/library/16a2182e-80aa-4184-8071-8f717ee5c572%28Office.15%29.aspx) element when you upgrade the Feature of a SharePoint Add-in.</span></span>
 

 

### <a name="what-can-and-cannot-be-done-declaratively"></a><span data-ttu-id="42a1d-117">Действия, которые можно и которые нельзя выполнить декларативно</span><span class="sxs-lookup"><span data-stu-id="42a1d-117">What can and cannot be done declaratively</span></span>

<span data-ttu-id="42a1d-p103">В случае обновления надстройки, размещенной в SharePoint, можно использовать только разметку XML. При этом возможности декларативного изменения надстройки будут ограничены. Для надстройки, размещенной на стороне поставщика, можно реализовать  [обработчик UpdatedEventEndpoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md), чтобы выполнить действия, которые невозможно сделать декларативно.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p103">With a SharePoint-hosted add-in, you can only use XML markup to update an add-in and there are some limits on how you can declaratively change an add-in in an update. In a provider-hosted add-in, you can implement a  [UpdatedEventEndpoint handler](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md) to do things that can't be done declaratively.</span></span>
 

 
<span data-ttu-id="42a1d-p104">Добавлять компоненты в надстройку просто. Любой компонент, который можно включить в надстройку, можно добавить также в обновление. (Дополнительные сведения о компонентах, которые могут входить в надстройку, можно найти в статье  [Типы компонентов SharePoint, которые могут находиться в надстройке для SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).) Но если вы хотите изменить существующий компонент декларативно, учтите указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p104">Adding components to an add-in is easy. Any component that is eligible to be included in an add-in can also be added in an update. (For details about what components can be in an add-in, see  [Types of SharePoint components that can be in a SharePoint Add-in](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps). ) But when you want to modify an existing component declaratively, consider the following points.</span></span> 
 

 

- <span data-ttu-id="42a1d-p105">Тип данных поля (столбца) списка или типа контента в любом случае невозможно изменить после первоначального развертывания. В частности, не меняйте этот тип данных при обновлении надстройки ( *даже программно*  ). В качестве альтернативного решения вы можете добавить новое поле. Если надстройка содержит пользовательские формы для создания, редактирования или просмотра элементов, не забудьте внести в них соответствующие изменения. Например, добавьте элемент пользовательского интерфейса для нового поля и удалите его для старого. (В надстройке, размещенной на стороне поставщика, можно программным путем переместить данные из старого поля в новое, а затем удалить старое.)</span><span class="sxs-lookup"><span data-stu-id="42a1d-p105">The data type of a list or content type field (column) cannot be changed after its initial deployment in any circumstance. In particular, do not change the data type of a field as part of an add-in update ( *not even programmatically*  ). As an alternative, you can add a new field. If the add-in includes custom item create, edit, or view forms; be sure to make corresponding changes in these forms. For example, add UI for the new field and remove UI for the old one. (In a provider-hosted add-in, you can programmatically move data from the old field to the new one and then delete the old. )</span></span>
    
 
- <span data-ttu-id="42a1d-131">Вам не удастся удалить списки, экземпляры списков, типы контента или поля в разметке обновления.</span><span class="sxs-lookup"><span data-stu-id="42a1d-131">Lists, list instances, content types, or fields cannot be deleted in the update markup.</span></span>
    
 
- <span data-ttu-id="42a1d-p106">Вам не удастся удалить файлы с сайта надстройки в разметке обновления. Тем не менее вы можете изменить содержимое любого файла.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p106">Files cannot be deleted from the add-in web in update markup. However, you can change the contents of any file.</span></span>
    
 
- <span data-ttu-id="42a1d-134">Вам не удастся использовать элементы **CustomUpgradeAction** и **MapFile** при обновлении надстройки SharePoint, хотя они могут быть доступными в IntelliSense для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42a1d-134">The  **CustomUpgradeAction** and **MapFile** elements cannot be used when updating a SharePoint Add-in, although they may appear available in Visual Studio intellisense.</span></span>
    
 

### <a name="update-the-add-in-web-for-the-first-time"></a><span data-ttu-id="42a1d-135">Первое обновление сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-135">Update the add-in web for the first time</span></span>

<span data-ttu-id="42a1d-p107">В этом разделе описано, как добавлять или обновлять типы контента, списки, файлы и другие компоненты SharePoint на сайте надстройки. Чтобы было проще, предполагается, что все компоненты входят в один компонент на сайте надстройки. Но этот сайт может иметь несколько таких компонентов, и за один раз можно обновить несколько таких компонентов.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p107">The procedures in this section explain how to add or update content types, lists, files, and other SharePoint components in the add-in web. For simplicity, we assume that all the components are part of a single Feature in the add-in web, but add-in webs can have multiple Features and you can update more than one in the same update.</span></span>
 

 
<span data-ttu-id="42a1d-p108">Инструменты разработчика Microsoft Office для Visual Studio ориентированы на создание надстроек, поэтому поведение этих средств, заданное по умолчанию, не всегда оптимально при обновлении надстройки. Для большего контроля над процессом сначала отключите конструктор компонентов, выполнив описанные ниже действия, чтобы можно было непосредственно изменять неотформатированный XML компонента.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p108">The Microsoft Office Developer Tools for Visual Studio are oriented to creating new add-ins and the default behavior of the tools is sometimes not optimal when you are updating an add-in. To get more control over the process, you should begin by disabling the Feature Designer using the following procedure, so that you can directly edit the raw feature XML.</span></span> 
 

 

### <a name="to-edit-the-feature-xml"></a><span data-ttu-id="42a1d-140">Изменение XML компонента</span><span class="sxs-lookup"><span data-stu-id="42a1d-140">To edit the Feature XML</span></span>


1. <span data-ttu-id="42a1d-p109">В **обозревателе решений** откройте файл _{Имя_Компонента}_.features. Он откроется в редакторе компонентов.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p109">In  **Solution Explorer**, open the  _{FeatureName}_.features file. It opens in the Feature designer.</span></span>
    
 
2. <span data-ttu-id="42a1d-143">Откройте вкладку **Манифест** и разверните пункт **Параметры правки**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-143">Open the  **Manifest** tab and expand **Edit Options**.</span></span>
    
 
3. <span data-ttu-id="42a1d-144">Выберите пункт **Перезаписать созданный XML и редактировать манифест в редакторе XML**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-144">Choose  **Overwrite generated XML and edit manifest in the XML editor**.</span></span>
    
 
4. <span data-ttu-id="42a1d-145">Когда отобразится соответствующий запрос, нажмите кнопку **Да**, чтобы отключить конструктор.</span><span class="sxs-lookup"><span data-stu-id="42a1d-145">Choose  **Yes** to the prompt to disable the designer.</span></span>
    
 
5. <span data-ttu-id="42a1d-p110">В открывшемся представлении выберите пункт **Редактирование манифеста в XML-редакторе**. Откроется файл _{Имя_Компонента}_.Template.xml.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p110">On the view that opens, choose  **Edit manifest in the XML editor**. The  _{FeatureName}_.Template.xml file opens.</span></span> 
    
    <span data-ttu-id="42a1d-148">**Открытие XML-редактора компонентов**</span><span class="sxs-lookup"><span data-stu-id="42a1d-148">**Opening the Feature XML editor**</span></span>

 

  ![Действия, которые необходимо выполнить, чтобы открыть XML-редактор компонентов](../images/UpdateAppOpenFeatureXML.png)
 

 

 

 <span data-ttu-id="42a1d-p111">**Внимание!** Не добавляйте комментарии "<!-- -->" в файл _{Имя_Компонента}_.features. Комментарии не поддерживаются инфраструктурой обновления, и вам не удастся выполнить обновление, если в файле есть комментарии. Комментарии используются в примерах разметки в этой статье, только чтобы показать вам, куда следует поместить разметку.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p111">**Caution**  Do not add "<!-- -->" comments to the  _{FeatureName}_.features file. Comments are not supported by the upgrade infrastructure and the upgrade will fail if comments are in the file. They are used in the markup examples of this article only to indicate to you where your markup should go.</span></span>
 

<span data-ttu-id="42a1d-153">Чтобы обновить компонент сайта надстройки, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="42a1d-153">Use the following steps to update the add-in web Feature.</span></span>
 

 

### <a name="to-update-the-add-in-web-feature-the-first-time"></a><span data-ttu-id="42a1d-154">Первое обновление компонента сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-154">To update the add-in web Feature the first time</span></span>


1. <span data-ttu-id="42a1d-p112">Увеличьте на единицу значение атрибута **Version** (Версия) для элемента [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) (Компонент), если пакет Инструменты разработчика Office для Visual Studio еще не сделал это при увеличении номера версии в манифесте надстройки. (Пакет Инструменты разработчика Office для Visual Studio делает это не в каждом сценарии, поэтому необходимо выполнять соответствующую проверку.) Вам следует использовать тот же номер версии, что и для надстройки. Вам даже следует рассмотреть вопрос об увеличении версии компонента при обновлении других компонентов надстройки, но не самого компонента сайта надстройки. Логикой элемента [VersionRange](http://msdn.microsoft.com/library/cd715e38-6ec3-43b2-8007-6d0ed8865d91%28Office.15%29.aspx) (который рассматривается в разделе [Последующие обновления сайта надстройки](#SubsequentUpgrades)) легче управлять, если версия надстройки и версия компонента всегда одинаковы.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p112">Increment the  **Version** attribute of the [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) element, if the Office Developer Tools for Visual Studio did not already do so when you incremented the version number in the add-in manifest. (The tools don't do this in every scenario, so you need to verify.) You should use the same version number that you use for the add-in. You should even consider raising the Feature version when other components of the add-in are being updated, but not the add-in web Feature itself. The logic of the [VersionRange](http://msdn.microsoft.com/library/cd715e38-6ec3-43b2-8007-6d0ed8865d91%28Office.15%29.aspx) element (which is discussed in the section [Subsequent updates of the add-in web](#SubsequentUpgrades)) is easier to manage when the add-in version and the Feature version are always the same.</span></span> 
    
 
2. <span data-ttu-id="42a1d-p113">Никогда и ничего не удаляйте в разделе [ElementManifests](http://msdn.microsoft.com/library/d8d4db7e-2bc2-40c6-958b-d5683bdee87a%28Office.15%29.aspx) файла.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p113">Don't delete anything in the  [ElementManifests](http://msdn.microsoft.com/library/d8d4db7e-2bc2-40c6-958b-d5683bdee87a%28Office.15%29.aspx) section of the file. Nothing is ever deleted from this section.</span></span>
    
 
3. <span data-ttu-id="42a1d-161">Добавьте указанные ниже элементы в файл (если они еще не добавлены).</span><span class="sxs-lookup"><span data-stu-id="42a1d-161">If they are not already present, add the following elements to the file:</span></span> 
    
      - <span data-ttu-id="42a1d-p114">Дочерний элемент  [UpgradeActions](http://msdn.microsoft.com/library/5af24ac1-a290-454d-b32b-bc7f7a4634f0%28Office.15%29.aspx) в элемент **Feature**.  *Не*  добавляйте атрибуты **ReceiverAssembly** или **ReceiverClass** в элемент. Они не используются при обновлении надстройки SharePoint. Эти атрибуты ссылаются на настраиваемую сборку, неподдерживаемую в надстройках SharePoint. Если вы включите настраиваемую сборку в надстройку, SharePoint ее не установит.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p114">An  [UpgradeActions](http://msdn.microsoft.com/library/5af24ac1-a290-454d-b32b-bc7f7a4634f0%28Office.15%29.aspx) child element in the **Feature** element. Do *not*  add **ReceiverAssembly** or **ReceiverClass** attributes to the element. These have no use when you are updating a SharePoint Add-in. (These attributes refer to a custom assembly, which is not supported in SharePoint Add-ins. If you include a custom assembly in an add-in, SharePoint will not install the add-in.)</span></span>
    
 
  - <span data-ttu-id="42a1d-p115">Дочерний элемент **VersionRange** в элементе **UpgradedActions**. Не добавляйте атрибуты **BeginVersion** или **EndVersion** в элемент. Это бесполезно, когда надстройка обновляется впервые. Об использовании этих элементов будет рассказано в разделе [Последующие обновления сайта надстройки](#SubsequentUpgrades).</span><span class="sxs-lookup"><span data-stu-id="42a1d-p115">A  **VersionRange** child element in the **UpgradedActions** element. Do not add **BeginVersion** or **EndVersion** attributes to the element. These serve no purpose when an add-in is being updated for the first time. Their use is discussed in the section [Subsequent updates of the add-in web](#SubsequentUpgrades).</span></span>
    
 
  - <span data-ttu-id="42a1d-170">Дочерний элемент [ApplyElementManifests](http://msdn.microsoft.com/library/c087a0c3-1e27-4034-b4da-e025991454d6%28Office.15%29.aspx) в элементе **VersionRange**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-170">An  [ApplyElementManifests](http://msdn.microsoft.com/library/c087a0c3-1e27-4034-b4da-e025991454d6%28Office.15%29.aspx) child element in the **VersionRange** element.</span></span>
    
 

    <span data-ttu-id="42a1d-171">На данный момент файл должен выглядеть приблизительно так, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="42a1d-171">At this point the file should resemble the following example.</span></span>
    
     <span data-ttu-id="42a1d-p116">**Важно!** Возможно, в качестве примера пакет Инструменты разработчика Office для Visual Studio уже добавил указанную выше разметку и скопировал некоторые элементы из раздела **ElementManifests** в раздел **ApplyElementManifests**. *Удалите их*. Не исключено, что вам придется в дальнейшем возвращать некоторые из них обратно. Но намного легче и безопаснее начать работу с пустого раздела **ApplyElementManifests**. Лишние записи для компонентов, которые не изменялись, могут иметь плохие последствия. Например, длительность процесса обновления может увеличиться настолько, что будет превышено время ожидания, и обновление завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p116">**Important**  The Office Developer Tools for Visual Studio may have already added the above markup and copied some elements from the  **ElementManifests** section to the **ApplyElementManifests** section as an illustration. *Delete these.*  Although you may end up putting some of them back in later steps, it is easier and safer to start with an empty **ApplyElementManifests** section. Redundant entries for components that have not changed can have bad consequences, including possibly lengthening the update process enough that it times-out and fails.</span></span>



```XML
  <Feature <!-- Some attributes omitted --> 
               Version="2.0.0.0">
  <ElementManifests>
    <!-- ElementManifest elements omitted -->
  </ElementManifests>
  <UpgradeActions>
   <VersionRange>
     <ApplyElementManifests>
       
     </ApplyElementManifests>
   </VersionRange>
  </UpgradeActions>
</Feature>
```


### <a name="to-add-components-to-the-add-in"></a><span data-ttu-id="42a1d-176">Добавление элементов в надстройку</span><span class="sxs-lookup"><span data-stu-id="42a1d-176">To add components to the add-in</span></span>


1. <span data-ttu-id="42a1d-177">Добавьте все новые элементы в компонент точно так же, как при создании проекта надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="42a1d-177">Add any new components to the Feature exactly as you would if you were creating a new SharePoint Add-in project.</span></span>
    
 
2. <span data-ttu-id="42a1d-p117">Когда вы добавляете компонент типа, который отсутствовал в предыдущей версии надстройки (например, добавляете в надстройку список, которого раньше не было), пакет Инструменты разработчика Office для Visual Studio добавляет файл elements.xml в проект. Это манифест элементов для компонента. К этому файлу следует добавить номер новой версии надстройки (например, elements.2.0.0.0.xml). Это может быть удобно при устранении неполадок. Не забудьте внести изменения в **обозревателе решений**, чтобы ссылки на файл (например, в CSPROJ-файле и XML компонента) тоже изменились.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p117">When you add a component of a type that wasn't in the previous verison of the add-in, such as adding a list to an add-in that did not previously have a list, the Office Developer Tools for Visual Studio will add an elements.xml file to the project. This is the elements manifest for the component. You should add the new version number of the add-in to this file (for example, elements.2.0.0.0.xml). This can be helpful in troubleshooting. Be sure to make the change in  **Solution Explorer** to ensure that references to the file, such as in the csproj file and the feature XML, are changed accordingly.</span></span>
    
 
3. <span data-ttu-id="42a1d-p118">Для каждого нового манифеста элементов добавьте дочерний элемент  [ElementManifest](http://msdn.microsoft.com/library/5a6a2865-5d31-45a2-a402-6da6e0f5567a%28Office.15%29.aspx) в элементы **ElementManifests** и **ApplyElementManifests** XML компонента. (Тот же элемент **ElementManifest** в обоих случаях.) Атрибут **Location** должен указывать на относительный путь к файлу elements.2.0.0.0.xml. Например, если вы добавили список с именем MyCustomList, элемент **ElementManifest** будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p118">For each new element manifest, add an  [ElementManifest](http://msdn.microsoft.com/library/5a6a2865-5d31-45a2-a402-6da6e0f5567a%28Office.15%29.aspx) element as a child to both the **ElementManifests** and the **ApplyElementManifests** elements of the feature xml. (The exact same **ElementManifest** element in both places.) The **Location** attribute of the element should point to the relative path of the elements.2.0.0.0.xml file. For example, if you added a list named MyCustomList, the **ElementManifest** element would look like the following.</span></span>
    
```XML
  <ElementManifest Location="MyCustomList\elements.2.0.0.0.xml" />
```

4. <span data-ttu-id="42a1d-p119">Некоторые виды компонентов добавляют к проекту файлы. Например, при добавлении списка создается файл schema.xml. А когда вы добавляете страницу, создается файл подкачки. Добавьте дочерний элемент  [ElementFile](http://msdn.microsoft.com/library/bd43638e-8f18-4a0d-b122-1c055f97aa71%28Office.15%29.aspx) в элемент **ElementManifests** для каждого такого файла. (Не добавляйте его в элемент **ApplyElementManifests**.) Атрибут **Location** должен указывать на относительный путь файла. Например, если вы добавили список, элемент **ElementFile** файла schema.xml будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p119">Some kinds of components add files to the project. For example, a schema.xml file is created when you add a list; and when you add a page, a page file is created. For each such file, add an  [ElementFile](http://msdn.microsoft.com/library/bd43638e-8f18-4a0d-b122-1c055f97aa71%28Office.15%29.aspx) element as a child to the **ElementManifests** element. (Do not add it to the **ApplyElementManifests** element.) The **Location** attribute should point to the relative path of the file. For example, if you added a list, the **ElementFile** element for the schema.xml would look like the following.</span></span>
    
```XML
  <ElementFile Location="MyCustomList\Schema.xml" />
```

5. <span data-ttu-id="42a1d-p120">При добавлении другого элемента типа, который уже использовался в предыдущей версии надстройки, пакет Инструменты разработчика Office для Visual Studio может добавить ссылку на новый элемент в существующий манифест элементов, а не создавать новый. Например, чтобы добавить страницу на сайт надстройки, обычно нужно щелкнуть правой кнопкой мыши узел **Страницы** в **обозревателе решений**, а затем последовательно выбрать пункты **Добавить | Новый элемент | Страница | Добавить**. Вместо того чтобы создавать новый манифест элементов, пакет Инструменты разработчика Office для Visual Studio добавит новый элемент **File** (Файл) в модуль **Pages** (Страницы) в существующий файл манифеста элементов (обычно он называется elements.xml).</span><span class="sxs-lookup"><span data-stu-id="42a1d-p120">When you add another item of a type that was already in the previous version of the add-in, the Office Developer Tools for Visual Studio may add a reference to the new item to an existing elements manifest instead of creating a new one. For example, the standard way to add a page to an add-in web is to right-click the  **Pages** node in **Solution Explorer** and then navigate through **Add | New Item | Page | Add**. The Office Developer Tools for Visual Studio will add a new  **File** element to the **Pages** module in the existing elements manifest file (usually called elements.xml) rather than create a new element manifest.</span></span>
    
    <span data-ttu-id="42a1d-p121">Это нежелательное действие. По возможности при обновлении надстройки не изменяйте существующие файлы манифеста элементов для предыдущих версий надстройки. Как правило, новые элементы должны находиться в новых файлах манифеста элементов (на которые ссылается элемент **ApplyElementManifests** XML компонента). (Есть несколько исключений, и они описаны ниже.) Например, чтобы добавить новую страницу, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p121">This is not desirable. The best practice is to avoid, when possible, editing any existing element manifest files when updating an add-in (that is, any element manifests from previous versions of the add-in). In general, new items should be in new element manifest files (which are themselves referenced in the  **ApplyElementManifests** element of the Feature XML). (A few of exceptions to this practice are described later.) For example, to add a new page, take these steps:</span></span>
    
      1. <span data-ttu-id="42a1d-198">Создайте модуль с именем Pages.2.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="42a1d-198">Create a new module named Pages.2.0.0.0</span></span>
    
 
  2. <span data-ttu-id="42a1d-199">Удалите из него файл sample.txt, который Инструменты разработчика Office для Visual Studio добавляют автоматически.</span><span class="sxs-lookup"><span data-stu-id="42a1d-199">Remove the sample.txt file from it that theOffice Developer Tools for Visual Studio add automatically.</span></span>
    
 
  3. <span data-ttu-id="42a1d-200">Переименуйте манифесты элементов в новом модуле на elements.2.0.0.0.xml.</span><span class="sxs-lookup"><span data-stu-id="42a1d-200">Rename the elements manifest in the new module to elements.2.0.0.0.xml.</span></span>
    
 
  4. <span data-ttu-id="42a1d-p122">Щелкните правой кнопкой мыши модуль **Pages.2.0.0.0** и последовательно выберите пункты **Добавить | Новый элемент | Страница | Добавить**. Будет создана страница, на которую будет ссылаться манифест элементов для модуля **Pages.2.0.0.0**, а не **Pages**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p122">Right-click the  **Pages.2.0.0.0** module and then navigate through **Add | New Item | Page | Add**. The new page is created and it is referenced in the elements manifest for  **Pages.2.0.0.0** instead of **Pages**.</span></span>
    
 
  5. <span data-ttu-id="42a1d-203">Убедитесь, что имеется элемент **ElementsFile** для новой страницы в элементе **ElementManifests** XML компонента и элемент **ElementManifest** для файла elements.2.0.0.0.xml в разделах **ElementManifests** и **ApplyElementManifests**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-203">Ensure that there is an  **ElementsFile** element for the new page in the **ElementManifests** element of the feature XML, and ensure that there is an **ElementManifest** element for the elements.2.0.0.0.xml file in both the **ElementManifests** and **ApplyElementManifests** sections.</span></span>
    
 

    <span data-ttu-id="42a1d-p123">В любой ситуации, когда пакет Инструменты разработчика Office для Visual Studio изменил существующий манифест элементов, можно использовать еще один вариант: вручную создать файл elements.2.0.0.0.xml и переместить в него разметку, добавленную в старый манифест. (При желании вы можете поместить новый манифест в тот же узел в **обозревателе решений**, в котором находится старый манифест.)</span><span class="sxs-lookup"><span data-stu-id="42a1d-p123">Another option in any situation in which Office Developer Tools for Visual Studio has changed an existing elements manifest, is to manually create a new elements.2.0.0.0.xml and move the markup that was added to the old manifest to your new one. (You can put the new one in the same  **Solution Explorer** node as the old one if you want.)</span></span>
    
 
6. <span data-ttu-id="42a1d-p124">Если вы добавляете поле в тип контента компонента, добавьте элемент  [AddContentTypeField](http://msdn.microsoft.com/library/cb04a3ac-f41a-4ffe-aaa1-d4bf3fb6347d%28Office.15%29.aspx) в раздел **VersionRange**. Убедитесь, что вы присвоили правильные значения атрибутам **ContentTypeId** и **FieldId**. С помощью атрибута **PushDown** укажите, будет ли добавлено новое поле в какой-либо производный тип контента (необязательно). Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p124">If you add a field to a content type in the Feature, add an  [AddContentTypeField](http://msdn.microsoft.com/library/cb04a3ac-f41a-4ffe-aaa1-d4bf3fb6347d%28Office.15%29.aspx) element to the **VersionRange** section. Be sure to assign the correct values to the **ContentTypeId** and **FieldId** attributes. Optionally, use the **PushDown** attribute to specify whether the new field should be added to any derived content types. The following is an example.</span></span>
    
```XML
  <VersionRange>
  <AddContentTypeField 
    ContentTypeId="0x0101000728167cd9c94899925ba69c4af6743e"
    FieldId="{CCDD361F-A3FB-40D8-A272-3A3C858F4116}"
    PushDown="TRUE" />
  <!-- Other child elements of VersionRange -->
</VersionRange>
```


### <a name="to-modify-existing-components-of-the-add-in"></a><span data-ttu-id="42a1d-210">Изменение существующих компонентов надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-210">To modify existing components of the add-in</span></span>


1. <span data-ttu-id="42a1d-p125">Если вы изменили файл, на который имеется ссылка в файле манифеста элементов (например, файл Default.aspx), вам вообще не нужно изменять элемент **ElementFile** для файла. Тем не менее необходимо сообщить инфраструктуре обновления, что следует заменить старую версию файла на новую. Это можно сделать, добавив элемент **ElementManifest** для модуля в раздел **ApplyElementManifests**. Так как в разделе **ElementManifests** уже существует такой элемент, иногда можно просто скопировать (а не переместить) его в **ApplyElementManifests**. Это рекомендуется делать, только если были изменены все файлы, на которые ссылается манифест. Обычно не нужно заменять неизмененный файл его копией, так как в ряде сценариев это может иметь плохие последствия. Например, если страница настроена так, что пользователи могут изменять ее, то в результате замены внесенные изменения могут быть удалены. Если вы изменили страницу, вам придется учитывать эти последствия, но не нужно без веской причины доставлять неудобства пользователям.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p125">If you have changed a file that is referenced in an elements manifest file, such as a Default.aspx file, you do not have to change the  **ElementFile** element for the file at all. But you do have to tell the update infrastructure to replace the old version of the file with the new one. You do this by adding an **ElementManifest** element for the module to the **ApplyElementManifests** section. Since there is already such an element in the **ElementManifests** section, simply copying (not moving) it to the **ApplyElementManifests** is sometimes an option, but this is only advisable if every file that is referenced in the manifest has been changed. As a general practice, you shouldn't replace an unchanged file with a copy of itself. In some scenarios this can have bad effects. For example, if the page has been configured to allow users to customize it, replacing it can cause the customizations to be removed. (If you had changed the page, then you'd have to accept this consequence, but you don't want to impose this inconvenience on your customers pointlessly.)</span></span>
    
    <span data-ttu-id="42a1d-219">Чтобы удостовериться, что заменены только измененные файлы модуля, создайте еще один манифест элементов для модуля, который будет ссылаться только на измененные файлы, и примените второй манифест в **ApplyElementManifests**, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="42a1d-219">To ensure that only the changed files in the module are replaced, create a second element manifest for the module that only references the changed files and apply the second manifest in the  **ApplyElementManifests** by following these steps.</span></span>
    
      1. <span data-ttu-id="42a1d-220">Щелкните правой кнопкой мыши узел модуля в **обозревателе решений** и добавьте XML-файл (не страницу) с именем elements.2.0.0.0.xml.</span><span class="sxs-lookup"><span data-stu-id="42a1d-220">Right-click the module's node in  **Solution Explorer** and add an XML file (not a page) named elements.2.0.0.0.xml.</span></span>
    
 
  2.  <span data-ttu-id="42a1d-p126">Выберите новый файл в области **Обозреватель решений**, чтобы его область свойств стала видимой, и измените свойство **Deployment Type** на **ElementManifest**. Это обязательно нужно сделать, чтобы обработка файла с помощью Инструменты разработчика Office для Visual Studio выполнялась должным образом.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p126">Select the new file in **Solution Explorer** to make its property pane visible and change the **Deployment Type** property to **ElementManifest**. This is important to ensure that the Office Developer Tools for Visual Studio handle the file properly.</span></span>
    
 
  3. <span data-ttu-id="42a1d-223">Скопируйте содержимое исходного манифеста в новый и удалите из нового манифеста все элементы меню  [Файл](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx), соответствующие **неизмененным** файлам.</span><span class="sxs-lookup"><span data-stu-id="42a1d-223">Copy the contents of the original manifest to the new one, and then delete from the new manifest all the  [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx) elements that correspond to files that have **not** changed.</span></span>
    
 
  4. <span data-ttu-id="42a1d-224">Добавьте элемент **ElementManifest** в раздел **ApplyElementManifests**, который ссылается на новый файл манифеста, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="42a1d-224">Add an  **ElementManifest** element to the **ApplyElementManifests** section that references the new manifest file such as in this example.</span></span>
    
```XML
  <ElementManifest Location="Pages\elements.2.0.0.0.xml" />
```


     **Note**   Do not delete the original manifest. The Feature XML is using both of the old and new ones. Do not copy any **ElementFile** elements from the **ElementManifests** section to the **ApplyElementManifests** section even if the file that is referenced in the **ElementFile** has been changed.
2. <span data-ttu-id="42a1d-p127">Откройте каждый файл манифеста элементов, на который имеются ссылки в разделе **ApplyElementManifests**, и удостоверьтесь, что у всех элементов [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx) (Файл) есть атрибут **ReplaceContents** со значением **TRUE** (Истина). Ниже приведен пример. Возможно, пакет Инструменты разработчика Office для Visual Studio уже сделал это, но вам следует убедиться в этом. Проверьте даже манифесты элементов для предыдущих версий надстройки. Это один из хороших способов изменения существующего файла манифеста элементов.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p127">Open every element manifest file that is referenced in the  **ApplyElementManifests** section and ensure that any [File](http://msdn.microsoft.com/library/c270e4ce-8110-4da7-b0e7-c223604bfce7%28Office.15%29.aspx) elements have a **ReplaceContents** attribute and that it is set to **TRUE**. The following is an example. The Office Developer Tools for Visual Studio may have done this already, but you should verify it. Do this even for the element manifests from previous versions of the add-in. This is one of the few ways in which it is a good practice to edit an existing element manifest file.</span></span>
    
```XML
  <Module Name="Pages">
  <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" />
</Module>
```

3. <span data-ttu-id="42a1d-p128">В страницы могут быть встроены веб-части, как описано в статье [Добавление веб-части на страницу сайта надстройки](include-a-web-part-in-a-webpage-on-the-add-in-web.md). Если вы изменяете страницу со встроенной веб-частью (или изменяете свойства веб-части), потребуется выполнить дополнительное действие: добавить на страницу указанную ниже разметку, чтобы служба SharePoint не добавила вторую копию веб-части на страницу. Разметку необходимо добавить к элементу **asp:Content** с идентификатором `PlaceHolderAdditionalPageHead`. (Возможно, при создании страницы пакет Инструменты разработчика Office для Visual Studio уже добавил ее, но вам нужно убедиться в этом.)</span><span class="sxs-lookup"><span data-stu-id="42a1d-p128">Pages can have Web Parts embedded in them as explained in  [Include a Web Part in a webpage on the add-in web](include-a-web-part-in-a-webpage-on-the-add-in-web.md). If you change a page that has a Web Part on it (or change the properties of the Web Part), then there is an additional step: you have to add the following markup to the page to prevent the SharePoint from adding a second copy of the Web Part onto the page. The markup should be added to the  **asp:Content** element with the ID `PlaceHolderAdditionalPageHead`. (The Office Developer Tools for Visual Studio may have already added it when the page was first created, but you should verify that it is there.)</span></span>
    
```XML
  <meta name="WebPartPageExpansion" content="full" />
```


     **Note**   If the page was configured to allow users to customize it, then this markup has the side effect of removing those customizations. Users will have to repeat them. If the Web Part was added to the page following the guidance in [Include a Web Part in a webpage on the add-in web](include-a-web-part-in-a-webpage-on-the-add-in-web.md), then the Web Part markup is in the elements manifest, so changing the Web Part's properties is an exception to the general rule that you should not edit an element manifest file as part of an add-in update. 
4. <span data-ttu-id="42a1d-234">Вместо того чтобы изменять страницу, вы можете использовать перенаправление на новую страницу, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="42a1d-234">As an alternative to changing a page, you also have the option of using redirection to a new page using the following steps.</span></span> 
    
      1. <span data-ttu-id="42a1d-235">Создайте страницу и настройте для нее разметку обновления, как описано выше в разделе **Добавление компонентов в надстройку**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-235">Create the new page and configure its update markup as described in the procedure  **To add components to the add-in** above.</span></span>
    
 
  2. <span data-ttu-id="42a1d-236">Откройте старую страницу и удалите всю разметку из элемента **asp:Content** с идентификатором `PlaceHolderAdditionalPageHead`.</span><span class="sxs-lookup"><span data-stu-id="42a1d-236">Open the old page and remove all markup from the  **asp:Content** element with the ID `PlaceHolderAdditionalPageHead`.</span></span> 
    
 
  3. <span data-ttu-id="42a1d-p129">Добавьте указанную ниже разметку в элемент **asp:Content** и замените путь _{RelativePathToNewPageFile}_ на новый путь и имя файла. Этот сценарий перенаправит браузер на новую страницу и укажет параметры запроса. Кроме того, он исключит старую страницу из истории браузера.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p129">Add the following markup to the  **asp:Content** element, and then replace _{RelativePathToNewPageFile}_ with the new path and filename. This script will redirect the browser to the new page and include the query parameters. It will also keep the old page out of the browser history.</span></span>
    
```
  <script type="text/javascript">
        var queryString = window.location.search.substring(1);
        window.location.replace("{RelativePathToNewPageFile}" + "?" + queryString);
</script>
```

  4. <span data-ttu-id="42a1d-240">Удалите все остальные элементы **asp:Content** на странице.</span><span class="sxs-lookup"><span data-stu-id="42a1d-240">Delete any other  **asp:Content** elements on the page.</span></span>
    
 
  5. <span data-ttu-id="42a1d-241">Если вы заменяете начальную страницу надстройки, то измените элемент **StartPage** манифеста надстройки так, чтобы он указывал на новую страницу.</span><span class="sxs-lookup"><span data-stu-id="42a1d-241">If the page you are replacing is the start page for the add-in, change the  **StartPage** element in the add-in manifest to point to the new page.</span></span>
    
 
5. <span data-ttu-id="42a1d-p130">Если сайт надстройки содержит компонент **CustomAction** или **ClientWebPart**, и вы изменяете его при обновлении, тогда вам потребуется изменить манифест элементов, так как в нем определены эти компоненты. Это исключение из общего правила, которое не разрешает изменять манифест элементов предыдущей версии надстройки при ее обновлении. Кроме того, необходимо скопировать (не переместить) элемент **ElementManifest** из раздела **ElementManifests** в раздел **ApplyElementManifests**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p130">If the add-in web of the add-in contains a  **CustomAction** or a **ClientWebPart**, and you modify it as part of an update, then you must modify the element manifest since that is where these components are defined. (This is an exception to the general practice that you should not edit an element manifest from a previous version of the add-in when updating the add-in.) You also have to copy (not move) the  **ElementManifest** element from the **ElementManifests** section to the **ApplyElementManifests** section.</span></span>
    
 

#### <a name="example-of-feature-xml-for-upgrading-an-add-in-the-first-time"></a><span data-ttu-id="42a1d-244">Пример XML компонента для первого обновления надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-244">Example of Feature XML for upgrading an add-in the first time</span></span>

<span data-ttu-id="42a1d-p131">Ниже показан пример полного файла _{Имя_Компонента}_.Template.xml для первого обновления надстройки. В этом примере обновленная надстройка включает измененный файл Default.aspx, на который имеются ссылки в файле `Pages\Elements.xml`, и она развертывает три новых файла jQuery, на каждый из которых есть ссылка в файле `Scripts\Elements.xml`. Обратите внимание, что все элементы **ElementFile** перемещаются в раздел **ElementManifests**. Кроме того, обратите внимание, каким образом выполняется копирование (не перенос) `<ElementManifest Location="Pages\Elements.xml" />` из раздела **ElementManifests** в раздел **ApplyElementManifests**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p131">The following is an example of a complete  _{FeatureName}_.Template.xml file for a first time update of an add-in. The updated add-in in this example includes a modified Default.aspx file that is referenced in the  `Pages\Elements.xml` file, and it deploys three new jQuery files, each of which is referenced in the `Scripts\Elements.xml` file. Note that all **ElementFile**s go in the  **ElementManifests** section and note how `<ElementManifest Location="Pages\Elements.xml" />` has been copied (not moved) from the **ElementManifests** section to the **ApplyElementManifests** section.</span></span>
 

 

```XML
<Feature xmlns="http://schemas.microsoft.com/sharepoint/" Title="MyApp Feature1" 
      Description="SharePoint Add-in Feature" Id="85d309a8-107e-4a7d-b3a2-51341d3b11ff" 
      Scope="Web" Version="2.0.0.0">
  <ElementManifests>
    <ElementFile Location="Pages\Default.aspx" />
    <ElementManifest Location="Pages\Elements.xml" />
    <ElementFile Location="Content\App.css" />
    <ElementManifest Location="Content\Elements.xml" />
    <ElementFile Location="Images\AppIcon.png" />
    <ElementManifest Location="Images\Elements.xml" />
    <ElementFile Location="Scripts\jquery-3.0.0.intellisense.js" />
    <ElementFile Location="Scripts\jquery-3.0.0.js" />
    <ElementFile Location="Scripts\jquery-3.0.0.min.js" />
  </ElementManifests> 
  <UpgradeActions>
      <VersionRange>      
        <ApplyElementManifests>
          <ElementManifest Location="Pages\Elements.xml" />
          <ElementManifest Location="Scripts\elements.2.0.0.0.xml" />
        </ApplyElementManifests>
      </VersionRange>
  </UpgradeActions>
</Feature>

```


### <a name="subsequent-updates-of-the-add-in-web"></a><span data-ttu-id="42a1d-248">Последующие обновления сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-248">Subsequent updates of the add-in web</span></span>
<span data-ttu-id="42a1d-249"><a name="SubsequentUpgrades"> </a></span><span class="sxs-lookup"><span data-stu-id="42a1d-249"></span></span>

<span data-ttu-id="42a1d-p132">Когда вы обновляете надстройку SharePoint второй (или третий и т. д.) раз, следует учитывать, что некоторые из ваших клиентов, возможно, не установили предыдущие обновления. Таким образом, если пользователь отвечает на сообщение "доступно обновление" после развертывания вашего последнего обновления в каталоге надстроек организации или в Магазине Office, экземпляр надстройки пользователя можно обновить с использованием нескольких версий в рамках единого процесса обновления. По большей части это именно то, что нужно: выполнить обновление каждой более ранней версии надстройки до последней версии. Тем не менее вам не всегда нужно, чтобы каждое действие обновления компонента сайта надстройки повторялось для каждого экземпляра надстройки. Существует ряд действий обновления, которые не должны происходить несколько раз в конкретном экземпляре надстройки. Например, если вы добавляете поле к типу контента в одном обновлении, вам не нужно добавлять его снова в следующем обновлении. В процедуре ниже показано, как использовать элемент **VersionRange** для управления действиями обновления в зависимости от версии обновляемого компонента.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p132">When you update a SharePoint Add-in for the second (or third, and so on) time, you have to consider that some of your customers may not have made the previous updates. So if a user responds to the "update is available" prompt after your latest update is deployed to the organization's add-in catalog or to the Office Store, their instance of the add-in may be updated through multiple versions in a single update process. For the most part, this is exactly what should occur: you want every earlier version of the add-in updated to the latest version. But you do not always want every update action for the add-in web Feature to reoccur for every instance of the add-in. There are some update actions that should not occur multiple times on a given add-in instance. For example, if you add a field to a content type in one update, you do not want that field added again in the next update. The following procedure shows how to use the  **VersionRange** element to control which update actions occur based on the version of the Feature that is being updated.</span></span>
 

 

### <a name="to-change-the-add-in-web-feature-on-later-updates"></a><span data-ttu-id="42a1d-257">Изменение компонента сайта надстройки в более поздних обновлениях</span><span class="sxs-lookup"><span data-stu-id="42a1d-257">To change the add-in web Feature on later updates</span></span>


1. <span data-ttu-id="42a1d-p133">Откройте файл _Имя_Компонента_.Template.xml для редактирования, как описано в разделе **Изменение XML компонента** ранее в этой статье, и увеличьте на единицу значение атрибута **Version** (Версия) элемента [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) (Компонент). Для компонента следует использовать тот же номер версии, что и для надстройки.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p133">Open the  _FeatureName_.Template.xml file for editing as described in the procedure  **To edit the Feature XML** earlier in this article, and increment the **Version** attribute of the [Feature](http://msdn.microsoft.com/library/265cd648-1a7e-410f-a1d7-0da8c64b4006%28Office.15%29.aspx) element. You should use the same version number for the Feature as you used for the add-in.</span></span>
    
    <span data-ttu-id="42a1d-p134">В рамках данного примера предположим, что вы ранее обновили надстройку с версии 1.0.0.0 до версии 2.0.0.0, и теперь обновляете ее до версии 3.0.0.0. Для этого присвойте атрибуту **Version** (Версия) значение 3.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p134">For purposes of a continuing example, let's suppose that you previously updated the add-in from version 1.0.0.0 to version 2.0.0.0, and now you are updating it to version 3.0.0.0. So set the  **Version** attribute to 3.0.0.0.</span></span>
    
 
2. <span data-ttu-id="42a1d-p135">Добавьте новый элемент **VersionRange** под всеми существующими элементами **VersionRange**. *Не* добавляйте атрибут **BeginVersion** или **EndVersion** в этот элемент.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p135">Add a new  **VersionRange** element under all existing **VersionRange** elements. Do *not*  add a **BeginVersion** or **EndVersion** attribute to this element.</span></span>
    
 
3. <span data-ttu-id="42a1d-p136">Присвойте элементу **VersionRange** необходимое значение, как описано в разделе **Первое обновление компонента сайта надстройки** этой статьи, чтобы учесть изменения обновленной версии компонента. При этом считайте, что используется не раздел **ApplyElementManifests**, а дочерний элемент **ApplyElementManifests** недавно добавленного элемента **VersionRange**, т. е. *самый нижний* элемент в XML-файле компонента.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p136">Populate the  **VersionRange** element as described in the procedure **To update the add-in web Feature the first time** earlier in this article to account for the changes that you have made in this updated version of the Feature. Whenever that procedure refers to the **ApplyElementManifests** section, treat this as referring to the **ApplyElementManifests** element that is a child of the **VersionRange** element that you just added; that is, the *lowest*  one in the Feature XML file.</span></span>
    
 
4. <span data-ttu-id="42a1d-p137">Перейдите к предыдущему элементу **VersionRange**, который вы добавили при последнем обновлении надстройки (с версии 1.0.0.0 до версии 2.0.0.0 в данном примере). Добавьте к этому элементу атрибут **EndVersion**. Вам нужно, чтобы обновления в этом элементе **VersionRange** были применены к любым версиям надстройки, к которым они еще не были применены (версия 1.0.0.0). При этом важно не применять такие обновления повторно к версиям, к которым они уже были применены (версия 2.0.0.0). Значение **EndVersion** — *исключительное*, поэтому задайте его для самой ранней версии, к которой вы *не* хотите применять обновления. В данном примере вы зададите для этого параметра значение 2.0.0.0. Теперь ваш файл должен выглядеть приблизительно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p137">Go to the previous  **VersionRange** element???the one you added the last time you updated the add-in (from 1.0.0.0 to 2.0.0.0 in the continuing example)???and add an **EndVersion** attribute to it. You want the upgrade actions in this **VersionRange** to be applied to any versions of the add-in to which they haven't already been applied (version 1.0.0.0), but you don't want them to be reapplied to versions to which they were already applied (version 2.0.0.0). The **EndVersion** value is *exclusive*  , so you set it to the lowest version to which you do *not*  want the upgrade actions applied. In the continuing example, you set it to 2.0.0.0. Your file should now resemble the following.</span></span>
    
```XML
  <Feature <!-- Some attributes omitted --> 
               Version="3.0.0.0">
  <ElementManifests>
    <!-- ElementManifest elements omitted -->
  </ElementManifests>
  <UpgradeActions>
    <VersionRange EndVersion="2.0.0.0">
      <!--  Child elements for upgrade from 1.0.0.0 to 2.0.0.0 go here. -->
    </VersionRange>
   <VersionRange>
      <!--  Child elements for upgrade from 2.0.0.0 to 3.0.0.0 go here. -->
   </VersionRange>
  </UpgradeActions>
</Feature>
```


    Each time that you upgrade the Feature, follow the same pattern. Add a new  **VersionRange** for the latest update actions. Then add an **EndVersion** element to the *previous*  **VersionRange** element and set it to the previous version number. In the continuing example, the file would resemble the following for the update from 3.0.0.0 to 4.0.0.0.
    


```XML
  <Feature <!-- Some attributes omitted --> 
               Version="4.0.0.0">
  <ElementManifests>
    <!-- Child elements omitted -->
  </ElementManifests>
  <UpgradeActions>
    <VersionRange EndVersion="2.0.0.0">
       <!-- Child elements for upgrade from 1.0.0.0 to 2.0.0.0 go here. -->
    </VersionRange>
    <VersionRange EndVersion="3.0.0.0">
       <!-- Child elements for upgrade from 2.0.0.0 to 3.0.0.0 go here. -->
    </VersionRange>
    <VersionRange>
       <!-- Child elements for upgrade from 3.0.0.0 to 4.0.0.0 go here. -->
    </VersionRange>
  </UpgradeActions>
</Feature>
```


    Notice that the most recent  **VersionRange** element has no **BeginVersion** or **EndVersion** attributes. This ensures that the upgrade actions that go into this **VersionRange** element are applied to all previous versions of the Feature, which is what you want because all the latest changes are referenced in this **VersionRange**, and none of them have already occurred for any instance of the Feature.
    
    Notice also that the  **BeginVersion** attribute is not used in any of the **VersionRange**s. This is because the default value for the  **BeginVersion** attribute is 0.0.0.0, and that is the value that you want because you want all upgrade actions applied to every instance of the add-in that is earlier than the version that is specified in the **EndVersion** attribute.
    
     **Important**   The **VersionRange** element determines only which versions of the Feature the upgrades are applied to. It does not determine which versions of the add-in get a notification that an update is available???the notification is triggered only by the add-in version number. Within 24 hours of a new version of the add-in being available in the organization's add-in catalog or the Office Store, every installed instance of the add-in, regardless of version, has the notification that an update is available appear on its tile in the **Site Contents** page. The **VersionRange** does not affect the new version number of the newly upgraded Feature or the newly updated add-in. Those two numbers are always changed to the latest version number, regardless of what version range the Feature was in before the upgrade. This provides another good reason to avoid using a **BeginVersion** attribute. The **BeginVersion** attribute can be used to block some upgrade actions from ever occurring on some add-in instances. But it cannot block the Feature or add-in versions from being raised to the latest version. So the use of a **BeginVersion** attribute could create a situation in which two instances of your add-in could have the same add-in version number and the same add-in web Feature version number, but have different components in their add-in webs.

## <a name="verify-deployment-of-add-in-web-components"></a><span data-ttu-id="42a1d-271">Проверка развертывания веб-компонентов надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-271">Verify deployment of add-in web components</span></span>
<span data-ttu-id="42a1d-272"><a name="VerifyDeployAppWebComp"> </a></span><span class="sxs-lookup"><span data-stu-id="42a1d-272"></span></span>

<span data-ttu-id="42a1d-273">Выполните указанные ниже действия, чтобы проверить развертывание компонента сайта надстройки и его элементов.</span><span class="sxs-lookup"><span data-stu-id="42a1d-273">Follow these steps to verify the deployment of the add-in web Feature and its components.</span></span>
 

 

### <a name="to-verify-the-provisioning-of-the-add-in-web"></a><span data-ttu-id="42a1d-274">Проверка подготовки сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="42a1d-274">To verify the provisioning of the add-in web</span></span>


1. <span data-ttu-id="42a1d-p138">Откройте страницу **Параметры сайта** на хост-сайте. В разделе **Администрирование семейства веб-сайтов** выберите ссылку **Иерархия сайтов**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p138">Open the  **Site Settings** page of the host web. In the **Site Collection Administration** section, choose the **Site hierarchy** link.</span></span>
    
 
2. <span data-ttu-id="42a1d-p139">На странице **Иерархия сайтов** в списке отобразится URL-адрес сайта надстройки. Не запускайте его. Вместо этого скопируйте URL-адрес и используйте его при выполнении дальнейших действий.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p139">On the  **Site Hierarchy** page, you see your add-in web listed by its URL. Do not start it. Instead, copy the URL, and use the URL in the remaining steps.</span></span>
    
 
3. <span data-ttu-id="42a1d-280">Перейдите по адресу _URL-адрес_веб-приложения_/_layouts/15/ManageFeatures.aspx и когда откроется страница **Компоненты сайта**, убедитесь, что компонент присутствует в упорядоченном по алфавиту списке компонентов и имеет состояние **Активен**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-280">Navigate to  _URL_of_app_web_/_layouts/15/ManageFeatures.aspx and, on the  **Site Features** page that opens, verify that the Feature is a member of the alphabetical list of Features and that its status is **Active**.</span></span> 
    
 
4. <span data-ttu-id="42a1d-281">Если компонент сайта надстройки включает настраиваемые столбцы сайта, перейдите по адресу _URL-адрес_веб-приложения_/_layouts/15/mngfield.aspx и на открывшейся странице **Столбцы сайта** убедитесь, что новые настраиваемые столбцы сайта включены в список.</span><span class="sxs-lookup"><span data-stu-id="42a1d-281">If your add-in web Feature includes custom site columns, open  _URL_of_app_web_/_layouts/15/mngfield.aspx and, on the  **Site Columns** page that opens, verify that your new custom site columns are listed.</span></span>
    
 
5. <span data-ttu-id="42a1d-282">Если в компонент сайта надстройки включены какие-либо настраиваемые типы контента, перейдите по адресу _URL-адрес_веб-приложения_/_layouts/15/mngctype.aspx и на открывшейся странице **Типы контента сайта** убедитесь, что новые типы контента включены в список.</span><span class="sxs-lookup"><span data-stu-id="42a1d-282">If your add-in web Feature includes any custom content types, open  _URL_of_app_web_/_layouts/15/mngctype.aspx and, on the  **Site Content Types** page that opens, verify that your new content types are listed.</span></span>
    
 
6. <span data-ttu-id="42a1d-p140">Для каждого настраиваемого типа контента и каждого типа контента, в который вы добавили столбец, щелкните ссылку для данного типа. На открывшейся странице **Тип контента сайта** убедитесь, что в типе контента есть необходимые столбцы сайта.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p140">For each custom content type, and each content type to which you have added a column, choose the link to the content type. On the  **Site Content Type** page that opens, verify that the content type has the site columns it should have.</span></span>
    
 
7. <span data-ttu-id="42a1d-285">Если в компонент сайта надстройки включены какие-либо экземпляры списка, перейдите по адресу _URL-адрес_веб-приложения_/layouts/15/mcontent.aspx и на открывшейся странице **Библиотеки и списки сайта** убедитесь в наличии ссылки **Настроить <имя_списка>** для каждого настраиваемого экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="42a1d-285">If your add-in web Feature includes any list instances, open  _URL_of_app_web_/_layouts/15/mcontent.aspx and, on the  **Site Libraries and Lists** page that opens, verify that there is a **Customize "name_of_list"** link for each custom list instance.</span></span>
    
 
8. <span data-ttu-id="42a1d-286">Для каждого из этих настраиваемых экземпляров списка щелкните ссылку **Настроить <имя_списка>** и на странице параметров списка убедитесь, что в списке есть необходимые типы контента и столбцы.</span><span class="sxs-lookup"><span data-stu-id="42a1d-286">For each of these custom list instances, choose the  **Customize "name_of_list "** link, and verify on the list settings page that the list has the expected content types and columns.</span></span>
    
     <span data-ttu-id="42a1d-p141">**Примечание.** Если на странице нет раздела **Типы контента**, вам необходимо включить управление типами контента. Щелкните ссылку **Дополнительные параметры** и на странице дополнительных параметров включите управление типами контента, а затем нажмите кнопку **ОК**. Вы вернетесь на предыдущую страницу, на которой теперь будет отображаться список раздела **Типы контента**.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p141">**Note**  If there is no  **Content Types** section on the page, you must enable management of content types. Choose the **Advanced Settings** link and, on the Advanced Settings page, enable management of content types, and then choose **OK**. You are returned to the previous page, and there is now a list of  **Content Types** section.</span></span>
9. <span data-ttu-id="42a1d-p142">В верхней части страницы находится **веб-адрес** списка. Если вы включили примеры элементов в свое определение экземпляров списка, скопируйте адрес и вставьте его в адресную строку браузера, а затем перейдите к списку. Убедитесь, что в списке присутствуют созданные вами примеры элементов.</span><span class="sxs-lookup"><span data-stu-id="42a1d-p142">Near the top of the page is the  **web address** of the list. If you included sample items in your list instance definition, copy the address and paste it into the address bar of your browser, and then navigate to the list. Verify that the list has the sample items that you created.</span></span>
    
 

## <a name="next-steps"></a><span data-ttu-id="42a1d-293">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42a1d-293">Next steps</span></span>
<span data-ttu-id="42a1d-294"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="42a1d-294"></span></span>

<span data-ttu-id="42a1d-295">Вернитесь к разделу  [Основные действия при обновлении надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из следующих статей, чтобы узнать, как обновить следующий важный компонент надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="42a1d-295">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="42a1d-296">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="42a1d-296">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="42a1d-297">Создание обработчика событий обновления в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="42a1d-297">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 
-  <span data-ttu-id="42a1d-298">[Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins.md) </span><span class="sxs-lookup"><span data-stu-id="42a1d-298">[Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins.md)</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="42a1d-299">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="42a1d-299">Additional resources</span></span>
<span data-ttu-id="42a1d-300"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="42a1d-300"></span></span>


-  [<span data-ttu-id="42a1d-301">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="42a1d-301">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
    
 
-  <span data-ttu-id="42a1d-302">[Практическое руководство. Добавление элементов к существующему компоненту](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) в пакете средств разработки программного обеспечения (SDK) Microsoft SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="42a1d-302">[How to: Add Elements to an Existing Feature](http://msdn.microsoft.com/library/b007f419-e0d6-4e3a-a3ae-b8e448656d02%28Office.15%29.aspx) in the Microsoft SharePoint 2010 Software Development Kit (SDK).</span></span>
    
 
-  <span data-ttu-id="42a1d-303">[Обновление компонентов](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) в пакете средств разработки программного обеспечения (SDK) Microsoft SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="42a1d-303">[Upgrading Features](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx) in the Microsoft SharePoint 2010 Software Development Kit (SDK).</span></span>
    
 

