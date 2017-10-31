---
title: "Важные аспекты разработки и архитектуры для надстроек SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: bdc7c2f6954931f3af8cc8e539b973a1ba238bb6
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape"></a><span data-ttu-id="def32-102">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-102">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>
<span data-ttu-id="def32-p101">Изучите аспекты архитектуры Надстройки SharePoint и Модель для надстроек SharePoint, включая варианты размещения надстроек, параметры пользовательского интерфейса, систему развертывания, систему безопасности и жизненный цикл. В этой статье содержатся сведения, дополняющие статью  [Надстройки SharePoint](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p101">Learn about aspects of the architecture of SharePoint Add-ins and the model for SharePoint Add-ins, including the add-in hosting options, user interface options, deployment system, security system, and lifecycle. This article supplements the information in the article  [SharePoint Add-ins](sharepoint-add-ins.md).</span></span>
 

 <span data-ttu-id="def32-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="def32-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="sharepoint-add-ins-hosting-options"></a><span data-ttu-id="def32-108">Варианты размещения для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-108">SharePoint Add-ins hosting options</span></span>
<span data-ttu-id="def32-109"><a name="SPAppModelArch_SPCenteredVsCloudCentered"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-109"><a name="SPAppModelArch_SPCenteredVsCloudCentered"> </a></span></span>

<span data-ttu-id="def32-110">Модель надстроек SharePoint предусматривает следующие способы для размещения компонентов надстройки:</span><span class="sxs-lookup"><span data-stu-id="def32-110">The SharePoint add-in model provides the following ways to host the components of a SharePoint Add-in:</span></span> 
 

 

-  <span data-ttu-id="def32-p103">**Размещение у поставщика.** Надстройки, которые содержат по крайней мере один удаленный компонент и могут содержать компоненты SharePoint, разворачиваются в соответствии с вашей логикой на вашем оборудовании или в учетной записи облака, либо разворачиваются на оборудовании клиента или в его учетной записи облака с помощью предоставленных вами программ установки и инструкций.</span><span class="sxs-lookup"><span data-stu-id="def32-p103">**Provider-hosted:** Add-ins that include at least one remote component and may also include SharePoint components. The non-SharePoint components are deployed by your logic on your hardware or cloud account, or deployed on the customer's hardware or cloud account using installation programs and instructions that you provide.</span></span>
    
 
-  <span data-ttu-id="def32-113">**Размещение в SharePoint.** Надстройки, содержащие только компоненты SharePoint и логику, которая выполняется на клиенте.</span><span class="sxs-lookup"><span data-stu-id="def32-113">**SharePoint-hosted:** Add-ins that include only SharePoint components and logic that runs on the client.</span></span>
    
 
<span data-ttu-id="def32-114">Дополнительные сведения о вариантах размещения и некоторые рекомендации по их выбору см. в статье  [Выбор шаблонов для разработки и размещения надстройки SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="def32-114">For more detailed information about hosting options and some guidance for how to choose between them, see  [Choose patterns for developing and hosting your SharePoint Add-in](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md).</span></span>
 

 

## <a name="add-in-webs-host-webs-features-and-sharepoint-components-in-add-ins"></a><span data-ttu-id="def32-115">Сайты надстроек, хост-сайты, функции и компоненты SharePoint в надстройках</span><span class="sxs-lookup"><span data-stu-id="def32-115">Add-in webs, host webs, Features, and SharePoint components in add-ins</span></span>
<span data-ttu-id="def32-116"><a name="SPComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-116"><a name="SPComponents"> </a></span></span>

<span data-ttu-id="def32-p104">Веб-сайт, на котором устанавливается надстройка SharePoint, называется хост-сайтом. Однако некоторые важные части надстройки SharePoint (будь то компоненты SharePoint или внешние компоненты) не разворачиваются на хост-сайте. Внешние веб-части разворачиваются на внешних серверах или в облачных учетных записях. Компоненты SharePoint разворачиваются на специальном веб-сайте в его собственном домене. Он называется сайтом надстройки. На хост-сайте разворачивается только ограниченный набор элементов пользовательского интерфейса, которые предоставляют пользователям доступ к другим компонентам надстройки, развернутым на хост-сайте. Эти компоненты пользовательского интерфейса на хост-сайте разворачиваются как часть компонента хост-сайта — компонента, который свободно располагается в пакете надстройки, а не в WSP-файле. Компоненты, которые разворачиваются на сайте надстройки, всегда являются компонентами, входящими в WSP-файл. Оба типа компонентов должны иметь область **Web**. Другие области невозможны для компонентов в надстройках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="def32-p104">The website to which a SharePoint Add-in is installed is called the host web. However, the significant parts of the SharePoint Add-in, whether they are SharePoint components or external components, are not deployed to the host web. External parts are deployed to external servers or cloud accounts. SharePoint components are deployed to a special website with its own domain. This is called the add-in web. Only a limited set of UI elements that give users access to the add-in's other components are deployed to the host web. These UI components in the host web are deployed as part of a host web Feature — a Feature that is loose in the add-in package instead of inside a .wsp file. The components that are deployed to the add-in web are always in Features that are inside a .wsp file. Both kinds of Features must have  **Web** scope. No other scope is possible for Features in SharePoint Add-ins.</span></span>
 

 
<span data-ttu-id="def32-p105">Как правило, любой компонент SharePoint, не включающий пользовательский код, который работает на серверах SharePoint, можно включать в Надстройка SharePoint (и разворачивать на сайте надстройки). Однако имеются некоторые исключения и нюансы того, как и где разворачиваются компоненты. Дополнительные сведения об этих нюансах, а также о хост-сайтах, изолированных сайтах надстройки и компонентах в надстройках см. в статье  [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p105">As a general rule, any SharePoint component that does not include custom code that runs on the SharePoint servers can be included in a SharePoint Add-in (and be deployed to the add-in web). There are, however, some exceptions and some nuances to how and where the components are deployed. For more information about these nuances and about host webs, the isolated add-in webs, and Features in add-ins, see  [Host webs, add-in webs, and SharePoint components in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md).</span></span>
 

 

## <a name="accessing-the-add-in-from-the-ui"></a><span data-ttu-id="def32-130">Доступ к надстройке из пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="def32-130">Accessing the add-in from the UI</span></span>
<span data-ttu-id="def32-131"><a name="AccessingApp"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-131"><a name="AccessingApp"> </a></span></span>

<span data-ttu-id="def32-p106">Когда надстройка SharePoint устанавливается на веб-сайте, эта надстройка указывается на странице **содержания** хост-сайта. Пользователи могут запускать надстройку с этой страницы. При таком запуске надстройка открывается в полноэкранном режиме.</span><span class="sxs-lookup"><span data-stu-id="def32-p106">When a SharePoint Add-in is installed on a website, the add-in is listed on the  **Site Contents** page of the host web. Users can start the add-in from that page. When opened in this way, the add-in runs in full-screen mode.</span></span>
 

 
<span data-ttu-id="def32-p107">Можно также вызвать надстройку SharePoint в веб-части надстройки. Веб-часть такого типа представлена классом **ClientWebPart** и, в сущности, является оболочкой для IFrame, где будет размещаться страница надстройки. В самом простом случае единственным существенным свойством этой веб-части является URL-адрес, который указывает на страницу. Но веб-части могут иметь настраиваемые свойства, которые пользователи могут устанавливать в инструментальной части. Эти свойства можно использовать, например, для установки сведений о контексте, таких как почтовый индекс пользователя. Чтобы включить такую веб-часть в надстройку, следует создать в надстройке компонент хост-сайта и добавить декларативную разметку веб-части. Как и другие веб-части, она появляется в пользовательском интерфейсе SharePoint, из которого пользователи добавляют веб-части. Если требуется еще большая степень изменчивости, то можно развернуть в надстройке несколько веб-частей надстройки. Например, надстройка со сводкой погоды может иметь одну веб-часть, в которой показывается текущая погода, и вторую веб-часть для недельного прогноза. Эти две части могут иметь разные размеры и функциональность.</span><span class="sxs-lookup"><span data-stu-id="def32-p107">Another way that a SharePoint Add-in can be surfaced is through an add-in part, a type of Web Part that is represented by the  **ClientWebPart** class. This kind of Web Part is essentially a wrapper for an IFrame that would host a page of the add-in. In the simplest case, the only significant property of the Web Part is a URL that points to the page. But Web Parts can have custom properties that users can set in a Tool Part. Such properties could be used, for example, to set context information such as the user's ZIP Code or Postal Code. To include such an add-in part in your add-in, you create a host web Feature in the add-in and add declarative Web Part markup. Like any other Web Part, it appears in the SharePoint UI from which users add Web Parts. You can have more than one add-in part deployed with your add-in if you need even more variability. For example, a weather add-in can have an add-in part that shows current weather and a second add-in part that shows a weekly forecast. The two parts can have different sizes and functionality.</span></span>
 

 

 <span data-ttu-id="def32-p108">**Примечание.** Веб-части надстройки можно также разворачивать на сайте надстройки. Для этого разметка веб-части должна быть частью компонента в WSP-файле пакета надстройки, а не компонента хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="def32-p108">**Note**  You can also deploy add-in parts to the add-in web. To implement this, the markup for the Web Part would be part of a Feature inside a .wsp file in the add-in package, not in the host web Feature.</span></span>
 

<span data-ttu-id="def32-p109">Рекомендуется стараться придавать своим надстройкам внешний вид SharePoint, насколько это возможно, хотя это необязательно, и не всегда будет лучшим вариантом. Дополнительные сведения о рекомендациях по взаимодействию с пользователем см. в статье  [Проектирование пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p109">We recommend that you try to give your add-ins a SharePoint appearance to the extent possible, although that is not mandatory and may not always be the best choice. For more information about the user experience guidelines, see  [UX design for SharePoint Add-ins](ux-design-for-sharepoint-add-ins.md).</span></span> 
 

 
<span data-ttu-id="def32-p110">Например, существует специальная главная страница с именем app.master. Она оптимизирована для использования страницами надстроек. Страница app.master является частью нового определения сайта, включенного в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="def32-p110">There is, for example, a special master page called app.master. This page is optimized for use by the pages of add-ins. The app.master page is part of a new site definition that is included in SharePoint.</span></span> 
 

 
<span data-ttu-id="def32-p111">Другим средством, которое можно использовать для поддержания целостного с SharePoint внешнего вида надстроек, является элемент управления хрома, который поставляется с SharePoint. Этот элемент управления позволяет добавлять область верхнего колонтитула с элементами навигации SharePoint на страницы надстройки, включая страницы с внешним размещением. Дополнительные сведения по проектированию взаимодействия с пользователями в Надстройки SharePoint см. в статье  [Проектирование пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins.md). Подробнее об элементе управления хрома можно узнать в статье  [Использование клиентского элемента управления хрома в надстройках для SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p111">Another tool you can use to help your add-ins maintain a consistent look and feel with SharePoint is the chrome control that ships with SharePoint. This control enables you to add the SharePoint navigation header area to your add-in pages, including pages hosted externally. For more information about UX design in SharePoint Add-ins, see  [UX design for SharePoint Add-ins](ux-design-for-sharepoint-add-ins.md). For more information about the chrome control, see  [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="add-in-package-structure"></a><span data-ttu-id="def32-154">Структура пакета надстройки</span><span class="sxs-lookup"><span data-stu-id="def32-154">Add-in package structure</span></span>
<span data-ttu-id="def32-155"><a name="SPAppModelArch_Package"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-155"><a name="SPAppModelArch_Package"> </a></span></span>

<span data-ttu-id="def32-p112">Пакет Надстройка SharePoint это файл с расширением APP, который соответствует  [новому стандарту упаковки данных (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx). (Чтобы открыть этот файл, следует добавить к его имени дополнительное расширение ZIP, а затем открыть его в проводнике.) Он содержит манифест надстройки, указывающий разные свойства надстройки инструкции для инфраструктуры установки SharePoint. Дополнительные сведения о манифесте и пакете надстройки см. в статье  [Изучите структуру манифеста надстройки и пакет надстройки для SharePoint](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p112">A SharePoint Add-in package is a file that has an ".app" extension and that complies with the  [Open Packaging Conventions (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx). (You can open the file by adding ".zip" as an extra extension on the filename and then opening it in Windows Explorer.) It contains an add-in manifest that specifies certain properties of the add-in and instructions to the SharePoint installation infrastructure. For more information about the add-in manifest and package, see  [Explore the app manifest structure and the package of a SharePoint Add-in](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).</span></span>
 

 

## <a name="permissions-authentication-and-authorization-for-sharepoint-add-ins"></a><span data-ttu-id="def32-159">Разрешения, аутентификация и авторизация для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-159">Permissions, authentication, and authorization for SharePoint add-ins</span></span>
<span data-ttu-id="def32-160"><a name="SPAppModelArch_Running"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-160"><a name="SPAppModelArch_Running"> </a></span></span>

<span data-ttu-id="def32-161">В SharePoint используется новая система безопасности и разрешений для надстроек.</span><span class="sxs-lookup"><span data-stu-id="def32-161">SharePoint introduces a new add-in permissions and security system.</span></span>
 

 

### <a name="add-in-permissions"></a><span data-ttu-id="def32-162">Разрешения для надстроек</span><span class="sxs-lookup"><span data-stu-id="def32-162">Add-in permissions</span></span>
<span data-ttu-id="def32-163"><a name="AppPermissions"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-163"><a name="AppPermissions"> </a></span></span>

<span data-ttu-id="def32-p113">Надстройки SharePoint имеют разрешения, как пользователи и группы. Это позволяет надстройке иметь набор разрешений, отличных от разрешений пользователя, который выполняет надстройку.</span><span class="sxs-lookup"><span data-stu-id="def32-p113">SharePoint Add-ins have permissions just as users and groups do. This enables an add-in to have a set of permissions that are different from the permissions of the user who is executing the add-in.</span></span> 
 

 
<span data-ttu-id="def32-p114">В файле манифеста надстройки необходимо запрашивать разрешения, которые требуются надстройке для запуска. Пользователь, который добавляет надстройку, должен удовлетворить эти запросы, и он может предоставить только те разрешения, которые имеет сам как пользователь. Предоставление должно быть для всех запрошенных разрешений или ни для одного из них, чтобы упростить управление разрешениями для пользователей и разработчиков. (Субъект надстройки всегда имеет права полного доступа на сайте надстройки, так что ему достаточно запросить разрешения для ресурсов SharePoint на хост-сайте или в других расположениях вне сайта надстройки.)</span><span class="sxs-lookup"><span data-stu-id="def32-p114">You must request, in the add-in manifest file, the permissions that an add-in needs to run. The user who adds the add-in must grant these requests, and the user can only grant permissions that he or she has as a user. The grant must be for all the requested permissions or none of them to simplify the management of permissions for users and developers. (The add-in principal always has full control rights to the add-in web, so it only needs to request permissions to SharePoint resources in the host web or other locations outside the add-in web.)</span></span>
 

 
<span data-ttu-id="def32-170">Подробнее см. в статье [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="def32-170">For more information about add-in permissions, see  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
 

 

### <a name="selective-delegation-and-authorization"></a><span data-ttu-id="def32-171">Выборочное делегирование и авторизация</span><span class="sxs-lookup"><span data-stu-id="def32-171">Selective delegation and authorization</span></span>
<span data-ttu-id="def32-172"><a name="SelectiveAuthorization"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-172"><a name="SelectiveAuthorization"> </a></span></span>

<span data-ttu-id="def32-p115">Ни пользователям, запускающим надстройку, ни владельцам ресурсов, предоставляющим надстройке разрешения для доступа к ресурсам, не требуется предоставлять надстройке свои учетные данные или пароль. Вместо этого SharePoint дает пользователям и владельцам ресурсов возможность предоставлять только конкретные разрешения, которые запрашивает надстройка. Это возможно благодаря использованию SharePoint протокола транзакций  [OAuth 2.0](http://tools.ietf.org/html/draft-ietf-oauth-v2-22). Дополнительные сведения о протоколе OAuth в SharePoint см. в статье  [Поток маркеров контекста OAuth для надстроек в SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p115">Neither users who are launching an add-in, nor resource owners who are granting an add-in permission to access a resource, need to provide the add-in their credentials or password. Instead, SharePoint enables users and resource owners to grant only the specific permissions that the add-in requests. What makes this possible is the use by SharePoint of the transaction protocol  [OAuth 2.0](http://tools.ietf.org/html/draft-ietf-oauth-v2-22). For more information about OAuth in SharePoint, see  [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins.md).</span></span>
 

 

### <a name="cross-domain-access"></a><span data-ttu-id="def32-177">Междоменный доступ</span><span class="sxs-lookup"><span data-stu-id="def32-177">Cross-domain access</span></span>
<span data-ttu-id="def32-178"><a name="SelectiveAuthorization"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-178"><a name="SelectiveAuthorization"> </a></span></span>

<span data-ttu-id="def32-p116">Надстройка SharePoint, включающее удаленное веб-приложение, которое использует JavaScript в своей логике доступа к данным, может использовать междоменную библиотеку JavaScript для получения авторизованного доступа к данным SharePoint в пределах арендованной области, в которой установлена надстройка. Дополнительные сведения см. в статье  [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p116">A SharePoint Add-in that includes a remote web application that uses JavaScript for its data access logic can use a JavaScript cross domain library to get authorized access to SharePoint data within the tenancy where the add-in is installed. For more information, see  [Access SharePoint data from add-ins using the cross-domain library](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).</span></span>
 

 

## <a name="add-in-lifecycle"></a><span data-ttu-id="def32-181">Жизненный цикл надстроек</span><span class="sxs-lookup"><span data-stu-id="def32-181">Add-in lifecycle</span></span>
<span data-ttu-id="def32-182"><a name="SPAppModelArch_Lifecycle"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-182"><a name="SPAppModelArch_Lifecycle"> </a></span></span>

<span data-ttu-id="def32-p117">Жизненный цикл Надстройка SharePoint включает публикацию, установку, обновление и удаление. Дополнительные сведения по этим темам см. в статьях  [Публикация надстроек для SharePoint](publish-sharepoint-add-ins.md),  [Развертывание и установка надстроек для SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) и [Процедура обновления надстроек для SharePoint](sharepoint-add-ins-update-process.md). Кроме того, следует отметить, что имеется механизм, с помощью которого администраторы клиента могут выполнять пакетную установку Надстройка SharePoint на несколько веб-сайтов. Дополнительные сведения см. в статье  [Сроки аренды и области развертывания надстроек для SharePoint](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p117">The lifecycle for a SharePoint Add-in includes publishing, installing, upgrading, and uninstalling. For more information about these subjects, see  [Publish SharePoint Add-ins](publish-sharepoint-add-ins.md),  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md) and [SharePoint Add-ins update process](sharepoint-add-ins-update-process.md). Note also that there is a mechanism by which tenant administrators can batch install a SharePoint Add-in to multiple websites. For more information, see  [Tenancies and deployment scopes for SharePoint Add-ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span></span>
 

 

## <a name="data-storage-in-sharepoint-add-ins"></a><span data-ttu-id="def32-187">Хранение данных в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-187">Data storage in SharePoint Add-ins</span></span>
<span data-ttu-id="def32-188"><a name="Data"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-188"><a name="Data"> </a></span></span>

<span data-ttu-id="def32-p118">Надстройки SharePoint может создавать и получать доступ к любому типу данных, включая структурированные данные, документы и файлы мультимедиа. Эти данные могут храниться в SharePoint или во внешнем расположении.</span><span class="sxs-lookup"><span data-stu-id="def32-p118">SharePoint Add-ins can create and access any kind of data, including structured data, documents, and multimedia files. This data can be stored in SharePoint or in an external location.</span></span> 
 

 

### <a name="structured-data-storage-options"></a><span data-ttu-id="def32-191">Параметры хранилища структурированных данных</span><span class="sxs-lookup"><span data-stu-id="def32-191">Structured data storage options</span></span>
<span data-ttu-id="def32-192"><a name="StructuredData"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-192"><a name="StructuredData"> </a></span></span>

<span data-ttu-id="def32-p119">Надстройка SharePoint может использовать практически любой тип хранилища структурированных данных, как в составе решения SharePoint, так и вне его, как на платформах Майкрософт, так и на платформах других производителей. Далее представлены  *некоторые*  места хранения структурированных данных для Надстройка SharePoint:</span><span class="sxs-lookup"><span data-stu-id="def32-p119">A SharePoint Add-in can use almost any kind of structured data storage, both inside and out of SharePoint and on Microsoft and non-Microsoft platforms. The following are  *some*  locations where you can store structured data for a SharePoint Add-in:</span></span>
 

 

- <span data-ttu-id="def32-195">Списки SharePoint на сайте надстроек</span><span class="sxs-lookup"><span data-stu-id="def32-195">SharePoint lists in an add-in web</span></span>
    
 
- <span data-ttu-id="def32-196">SQL Azure</span><span class="sxs-lookup"><span data-stu-id="def32-196">SQL Azure</span></span>
    
 
- <span data-ttu-id="def32-197">Внешние источники данных, подключенные к SharePoint, со службами Службы Microsoft Business Connectivity Services (BCS)</span><span class="sxs-lookup"><span data-stu-id="def32-197">External data sources connected to SharePoint with Microsoft Business Connectivity Services (BCS)</span></span>
    
 
- <span data-ttu-id="def32-198">Облачная служба сторонних поставщиков</span><span class="sxs-lookup"><span data-stu-id="def32-198">A non-Microsoft cloud service</span></span>
    
 
- <span data-ttu-id="def32-199">База данных на собственном сервере</span><span class="sxs-lookup"><span data-stu-id="def32-199">A database on your own server</span></span>
    
 

 <span data-ttu-id="def32-p120">**Совет.** Вероятно, однажды вам понадобится обновить свою надстройку SharePoint. Если надстройка SharePoint содержит компоненты SharePoint, расположенные на сайте надстройки, в процессе обновления будет создаваться полная копия веб-приложения. Поэтому если на сайте надстройки хранятся очень большие списки SharePoint, обновление будет выполняться длительное время и потреблять много процессорной мощности сервера базы данных содержимого. Не следует помещать "большие данные" в списки SharePoint на сайте надстройки.</span><span class="sxs-lookup"><span data-stu-id="def32-p120">**Tip**  You will probably upgrade your SharePoint Add-in at some point. When a SharePoint Add-in includes SharePoint components on an add-in web, the upgrade process makes a complete copy of the add-in web. For this reason, very large SharePoint lists on the add-in web make the upgrade process time-consuming and processor intensive on the content database server. You should avoid putting "big data" in SharePoint lists on the add-in web.</span></span>
 


### <a name="unstructured-data-storage-options"></a><span data-ttu-id="def32-204">Параметры хранилища неструктурированных данных</span><span class="sxs-lookup"><span data-stu-id="def32-204">Unstructured data storage options</span></span>
<span data-ttu-id="def32-205"><a name="UnStructuredData"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-205"><a name="UnStructuredData"> </a></span></span>

<span data-ttu-id="def32-p121">Документы, изображения, видеозаписи, аудиофайлы и другие виды неструктурированных данных, которые производятся или используются Надстройка SharePoint, можно хранить в составе решения SharePoint или вне его. Библиотеки документов это прекрасный вариант для хранения документов, которые становятся доступными для поиска с помощью системы поиска SharePoint. Библиотека ресурсов сайта, как правило, отлично подходит для хранения мультимедийных файлов.</span><span class="sxs-lookup"><span data-stu-id="def32-p121">Documents, images, videos, audio files, and other kinds of unstructured data that is produced or used by a SharePoint Add-in can be stored in or outside SharePoint. Document libraries are a good choice for documents and are searchable via SharePoint search. A site asset library is often a good choice for multimedia files.</span></span> 
 

 
<span data-ttu-id="def32-p122">Другие варианты включают хранилище BLOB-объектов в учетной записи Microsoft Azure или на ваших серверах. Вы также можете хранить файлы на некоторых сторонних платформах или в сторонних облачных службах.</span><span class="sxs-lookup"><span data-stu-id="def32-p122">Other options include blob storage in your Microsoft Azure account or on your own servers. You can also store files in some non-Microsoft platforms or cloud services.</span></span>
 

 

### <a name="add-in-settings-and-other-metadata-storage-options"></a><span data-ttu-id="def32-211">Параметры надстроек и другие варианты хранения метаданных</span><span class="sxs-lookup"><span data-stu-id="def32-211">Add-in settings and other metadata storage options</span></span>
<span data-ttu-id="def32-212"><a name="AppMetadata"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-212"><a name="AppMetadata"> </a></span></span>

<span data-ttu-id="def32-p123">Метаданные для Надстройка SharePoint, например предпочтения пользователей, сведения о расположении и другие настройки, можно хранить в различных местах. Иногда для этого отлично подходит скрытый список SharePoint. Вы также можете использовать контейнер свойств сайта надстройки. Другой вариант, доступный для надстройки с размещением у поставщика, использование табличного хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="def32-p123">Metadata for a SharePoint Add-in, such as user preferences, location information, and other settings can be stored in several places. A hidden SharePoint list is sometimes a good choice. You can also use the property bag of the add-in web. Another option, for a provider-hosted add-in, is to use Microsoft Azure Table storage.</span></span> 
 

 

### <a name="secure-data-access-options"></a><span data-ttu-id="def32-217">Варианты безопасного доступа к данным</span><span class="sxs-lookup"><span data-stu-id="def32-217">Secure data access options</span></span>
<span data-ttu-id="def32-218"><a name="DataAccess"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-218"><a name="DataAccess"> </a></span></span>

<span data-ttu-id="def32-p124">Варианты безопасного доступа к данным, конечно же, зависят от выбранного вами хранилища. Поиск данных и доступ к ним рассматриваются более подробно в других разделах. Дополнительные сведения см. в статье  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="def32-p124">Your options for secure data access, of course, depend on your choice of storage. Data access and search are discussed in detail in several other articles. For more information, see  [Secure data access and client object models for SharePoint Add-ins](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).</span></span>
 

 

## <a name="managing-add-ins"></a><span data-ttu-id="def32-222">Управление надстройками</span><span class="sxs-lookup"><span data-stu-id="def32-222">Managing add-ins</span></span>
<span data-ttu-id="def32-223"><a name="SPAppModelArch_Managing"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-223"><a name="SPAppModelArch_Managing"> </a></span></span>

<span data-ttu-id="def32-p125">Администраторы семейства сайтов и администраторы клиента могут выполнять мониторинг надстроек и изменять выделенные для них ресурсы. Кроме того, персонал Microsoft магазина надстроек может помечать надстройки и отключать их.</span><span class="sxs-lookup"><span data-stu-id="def32-p125">Site collection administrators and tenant administrators can monitor add-ins and change the resources allocated to them. In addition, Microsoft personnel for the add-in store can flag add-ins and disable them.</span></span>
 

 
<span data-ttu-id="def32-226">Подробнее об управлении надстройками см. в статье [Установка надстроек SharePoint и управление ими](http://msdn.microsoft.com/en-us/library/733647a3-a5d3-475b-967d-3bb627c2a0c2) на сайте TechNet.</span><span class="sxs-lookup"><span data-stu-id="def32-226">For more information about managing add-ins, see  [Install and manage SharePoint Add-ins](http://msdn.microsoft.com/en-us/library/733647a3-a5d3-475b-967d-3bb627c2a0c2) on TechNet.</span></span>
 

 

### <a name="monitoring-add-ins"></a><span data-ttu-id="def32-227">Отслеживание надстроек</span><span class="sxs-lookup"><span data-stu-id="def32-227">Monitoring add-ins</span></span>
<span data-ttu-id="def32-228"><a name="SPAppModelArch_Monitoring"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-228"><a name="SPAppModelArch_Monitoring"> </a></span></span>

<span data-ttu-id="def32-p126">SharePoint предоставляет возможность наблюдения за работоспособностью надстроек и делает эту информацию доступной в пользовательском интерфейсе для владельцев веб-сайта, администраторов клиентов и администраторов фермы. Большая часть документации по мониторингу системы находится на веб-сайте TechNet; например,  [Мониторинг надстроек SharePoint](http://technet.microsoft.com/library/3adafdd2-f276-4a9d-8a74-e06b8916bbc2). В этом разделе даются только краткие вводные сведения, чтобы объяснить, как осуществляется мониторинг продаваемых вами надстроек.</span><span class="sxs-lookup"><span data-stu-id="def32-p126">SharePoint provides health monitoring of add-ins and makes this information available in the UI to website owners, tenant administrators, and farm administrators. Most documentation for the monitoring system is on TechNet; for example  [Monitor SharePoint Add-ins](http://technet.microsoft.com/library/3adafdd2-f276-4a9d-8a74-e06b8916bbc2). This section is just a quick introduction to explain how add-ins that you sell are monitored.</span></span>
 

 
<span data-ttu-id="def32-p127">Отчеты по одним видам данных создаются на уровне приложения, а по другим видам данных на уровне экземпляра приложения. Отчеты инфраструктуры мониторинга включают следующие основные элементы.</span><span class="sxs-lookup"><span data-stu-id="def32-p127">Some kinds of data are reported per-app and other kinds are reported per-app-instance. The primary items that the monitoring framework reports are as follows:</span></span>
 

 

- <span data-ttu-id="def32-233">Использование надстройки, например, количество ее установок (созданий нового экземпляра).</span><span class="sxs-lookup"><span data-stu-id="def32-233">Use of the add-in, such as the number of times it has been installed (creating a new instance).</span></span> 
    
 
- <span data-ttu-id="def32-234">Потребление серверных ресурсов каждым экземпляром надстройки.</span><span class="sxs-lookup"><span data-stu-id="def32-234">Server resource consumption of each add-in instance.</span></span>
    
 
- <span data-ttu-id="def32-235">Ошибки установки, обновления и времени выполнения каждого экземпляра надстройки.</span><span class="sxs-lookup"><span data-stu-id="def32-235">Installation, upgrade, and run-time errors of each add-in instance.</span></span>
    
 
- <span data-ttu-id="def32-236">Общий индикатор работоспособности каждого экземпляра надстройки, имеющий зеленый, желтый или красный цвет.</span><span class="sxs-lookup"><span data-stu-id="def32-236">An overall health indicator for each add-in instance of green, yellow, and red.</span></span>
    
 
<span data-ttu-id="def32-p128">Если в надстройке имеются компоненты Веб-сайт Azure, то инфраструктура мониторинга также проводит ежечасные опросы Microsoft Azure для сбора сведений об ошибках и сообщает данные о критически важных ошибках и квоте хранилища в пользовательском интерфейсе SharePoint. Сведения об ошибках База данных SQL Microsoft Azure не сообщаются.</span><span class="sxs-lookup"><span data-stu-id="def32-p128">If the add-in includes Azure Web Site components, the monitoring framework also polls Microsoft Azure hourly for its error data and reports critical errors and storage quota data in the SharePoint UI. Microsoft Azure SQL Database errors are not reported.</span></span>
 

 
<span data-ttu-id="def32-239">Сведения, предоставляемые инфраструктурой мониторинга, позволяют администраторам определять, насколько разумно был потрачен бюджет на приобретение надстроек, следует ли развернуть дополнительные ресурсы для надстроек, и следует ли отключить надстройку, которая работает неправильно.</span><span class="sxs-lookup"><span data-stu-id="def32-239">The information that is provided by the monitoring framework enables administrators to determine whether their add-in purchase budget is being wisely spent, whether they have to deploy more resources to add-ins, and whether they have to disable an add-in that is not working correctly.</span></span>
 

 

## <a name="registering-add-in-dependencies"></a><span data-ttu-id="def32-240">Регистрация зависимостей надстроек</span><span class="sxs-lookup"><span data-stu-id="def32-240">Registering add-in dependencies</span></span>
<span data-ttu-id="def32-241"><a name="RegisterDependency"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-241"><a name="RegisterDependency"> </a></span></span>

<span data-ttu-id="def32-p129">Если ваша Надстройка SharePoint зависит от возможности SharePoint, которая сейчас недоступна и которую нельзя включить через сайт надстройки, пользователи будут жаловаться на неправильную работу. Можно сделать так, чтобы ваша надстройка не устанавливалось там, где отсутствуют необходимые возможности и функции, регистрируя зависимости надстройки в манифесте. Инфраструктура установки Надстройки SharePoint будет проверять эти зависимости, блокируя установку надстройки при их отсутствии.</span><span class="sxs-lookup"><span data-stu-id="def32-p129">If your SharePoint Add-in depends on a SharePoint capability that is not available and cannot be made available on the add-in web, then it will not work properly and your customers will complain. You can ensure that your add-in is not installed where the requisite services and Features are not available by registering the dependencies of the add-in in add-in manifest. The installation infrastructure for SharePoint Add-ins will check for these prerequisites and it will block installation of you add-in if any of them is not available.</span></span>
 

 
<span data-ttu-id="def32-245">Для таких служб, как Excel, Access или Visio, инфраструктура будет проверять установку и наличие лицензий.</span><span class="sxs-lookup"><span data-stu-id="def32-245">For services, such as Excel, Access, or Visio services, the infrastructure will verify that the service is installed and licensed.</span></span>
 

 
<span data-ttu-id="def32-246">Для таких функций, как список задач, инфраструктура будет проверять, развернута ли функция, а также одно из двух:</span><span class="sxs-lookup"><span data-stu-id="def32-246">For Features, such as a Task list, the infrastructure will verify that the Feature is deployed and either:</span></span>
 

 
<span data-ttu-id="def32-247">— активирована ли функция в области **Farm**, **WebApplication** или **Site** (семейство веб-сайтов);</span><span class="sxs-lookup"><span data-stu-id="def32-247">-- activated at the  **Farm**,  **WebApplication**, or  **Site** (site collection) scope</span></span>
 

 
<span data-ttu-id="def32-248">или</span><span class="sxs-lookup"><span data-stu-id="def32-248">or</span></span>
 

 
<span data-ttu-id="def32-249">— возможно ли ее активировать в области **Web** на сайте надстройки, создаваемом при ее установке.</span><span class="sxs-lookup"><span data-stu-id="def32-249">-- activatible, with  **Web** scope, on the add-in web that is created when the add-in is installed.</span></span>
 

 

 <span data-ttu-id="def32-250">**Примечание.** Инфраструктура установки автоматически включает такие функции на сайте надстройки при его создании.</span><span class="sxs-lookup"><span data-stu-id="def32-250">**Note**  The add-in installation infrastructure will automatically activate such Features on the add-in web when it is created.</span></span>
 

<span data-ttu-id="def32-251">В следующих разделах описано, как зарегистрировать необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="def32-251">The following sections provide the details you need to register your prerequisites.</span></span>
 

 

### <a name="implicitly-register-dependencies-with-permission-requests"></a><span data-ttu-id="def32-252">Неявная регистрация зависимостей с запросами разрешений</span><span class="sxs-lookup"><span data-stu-id="def32-252">Implicitly register dependencies with permission requests</span></span>
<span data-ttu-id="def32-253"><a name="PermAsPreq"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-253"><a name="PermAsPreq"> </a></span></span>

<span data-ttu-id="def32-p130">Если вашей надстройке нужен доступ к компонентам SharePoint вне сайта надстройки, то она должна запросить разрешения на них в разделе **AppPermissionRequests** манифеста приложения. Эти запросы также служат для регистрации зависимостей, так как SharePoint определит по запрошенным разрешениям, какие возможности SharePoint нужны вашей надстройке. В ряде случаев SharePoint может определить все нужные возможности, и оставшиеся разделы статьи использовать не потребуется. Тем не менее, избыточность при регистрации зависимостей не повредит.</span><span class="sxs-lookup"><span data-stu-id="def32-p130">When your add-in needs access to SharePoint components outside of the add-in web, it must request permission for these resources in the  **AppPermissionRequests** section of the add-in manifest. These permission requests also serve as prerequisite registrations because SharePoint will infer from the permissions that your add-in requests that it the add-in needs certain SharePoint capabilities to be available. In many situations, SharePoint can infer all the capabilities that your add-in needs and the remaining sections of this topic are not needed. However, redundant dependency registrations are not harmful.</span></span>
 

 

### <a name="explicitly-register-dependencies-with-appprerequisites"></a><span data-ttu-id="def32-258">Явная регистрация зависимостей с помощью AppPrerequisites</span><span class="sxs-lookup"><span data-stu-id="def32-258">Explicitly register dependencies with AppPrerequisites</span></span>
<span data-ttu-id="def32-259"><a name="Explicit"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-259"><a name="Explicit"> </a></span></span>

<span data-ttu-id="def32-p131">Если ваша надстройка имеет зависимость, которая не выводится по запросам разрешений, ее следует зарегистрировать в элементе **AppPrerequisite** манифеста надстройки. У этого элемента есть три атрибута: **Type**, **ID** и (необязательный) **MinimumVersion**.</span><span class="sxs-lookup"><span data-stu-id="def32-p131">When your add-in has a dependency that is not implied by its permission requests, you register each dependency with an  **AppPrerequisite** element in the add-in manifest. There are three attributes in this element; **Type**,  **ID**, and (optionally)  **MinimumVersion**.</span></span> 
 

 
<span data-ttu-id="def32-p132">Существует три возможных значения необходимых компонентов для **Type**: `Feature`, `Capablility` и `AutoProvisioning`. Необходимый компонент Feature — это просто функция SharePoint, которая должна быть развернута и активирована на сайте надстройки или в более широкой области, включающей этот сайт. Capability — это набор связанных функций и служб, который должен быть доступен на сайте надстройки. (`AutoProvisioning` рассматривается далее.)</span><span class="sxs-lookup"><span data-stu-id="def32-p132">There are three possible prerequisite values for  **Type**;  `Feature`,  `Capablility`, and  `AutoProvisioning`. A Feature prerequisite is simply a SharePoint Feature that must be deployed and activated on the add-in web or a broader scope that includes the add-in web. A capability is a set of related Features and services that must be available on the add-in web. ( `AutoProvisioning` is discussed in the next section.)</span></span>
 

 
<span data-ttu-id="def32-p133">Необязательный атрибут **MinimumVersion** задает минимальную версию функции или возможности, необходимой надстройке, в формате n.n.n.n, например `15.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="def32-p133">The optional  **MinimumVersion** specifies the lowest version of the Feature or capability that your add-in requires. The attribute values are of the form n.n.n.n; for example `15.0.0.0`.</span></span>
 

 
<span data-ttu-id="def32-p134">**ID** указывает, какая функция или возможность необходима. Если **Type** — это `Feature`, то **ID** — это GUID функции с разделителями-дефисами в скобках, например `{151D22D9-95A8-4904-A0A3-22E4DB85D1E0}`. Если же **Type** — это `Capability`, то **ID** — это GUID возможности. Все возможности перечислены ниже. Сведения о получении GUID возможности см. в статье [Элемент AppPrerequisite (AppPrerequisiteCollection complexType) (Manifest SharePoint Add-in)](http://msdn.microsoft.com/library/791be402-981f-519e-fcde-f24cc3cb4139%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="def32-p134">The  **ID** specifies which Feature or capability is required. If **Type** is `Feature`, the  **ID** is the bracketed, hyphenated GUID of the Feature; for example `{151D22D9-95A8-4904-A0A3-22E4DB85D1E0}`. If  **Type** is `Capability`, the  **ID** is the GUID of the capability. The capabilities are listed below. To get the find the GUID of a capability see [AppPrerequisite element (AppPrerequisiteCollection complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/791be402-981f-519e-fcde-f24cc3cb4139%28Office.15%29.aspx).</span></span>
 

 

- <span data-ttu-id="def32-273">Службы Access 2010</span><span class="sxs-lookup"><span data-stu-id="def32-273">Access Services 2010</span></span>
    
 
- <span data-ttu-id="def32-274">Службы Access</span><span class="sxs-lookup"><span data-stu-id="def32-274">Access Services</span></span>
    
 
- <span data-ttu-id="def32-275">Веб-служба управляемых метаданных</span><span class="sxs-lookup"><span data-stu-id="def32-275">Managed Metadata Web Service</span></span>
    
 
- <span data-ttu-id="def32-276">Службы PowerPoint</span><span class="sxs-lookup"><span data-stu-id="def32-276">PowerPoint Services</span></span>
    
 
- <span data-ttu-id="def32-277">Службы Secure Store</span><span class="sxs-lookup"><span data-stu-id="def32-277">Secure Store Services</span></span>
    
 
- <span data-ttu-id="def32-278">Служба машинного перевода</span><span class="sxs-lookup"><span data-stu-id="def32-278">Machine Translation Service</span></span>
    
 
- <span data-ttu-id="def32-279">Служба профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="def32-279">User Profile Service</span></span>
    
 
- <span data-ttu-id="def32-280">Служба графики Visio</span><span class="sxs-lookup"><span data-stu-id="def32-280">Visio Graphics Service</span></span>
    
 
- <span data-ttu-id="def32-281">Служба управления работой</span><span class="sxs-lookup"><span data-stu-id="def32-281">Work Management Service</span></span>
    
 
- <span data-ttu-id="def32-282">Duet</span><span class="sxs-lookup"><span data-stu-id="def32-282">Duet</span></span>
    
 
- <span data-ttu-id="def32-283">Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="def32-283">Workflow</span></span>
    
 
- <span data-ttu-id="def32-284">Поиск</span><span class="sxs-lookup"><span data-stu-id="def32-284">Search</span></span>
    
 
- <span data-ttu-id="def32-285">EDU</span><span class="sxs-lookup"><span data-stu-id="def32-285">EDU</span></span>
    
 
<span data-ttu-id="def32-p135">Далее приведен пример необработанной разметки **AppPrerequisites**, в которой регистрируется возможность Workflow. Если вы используете Visual Studio, то манифест надстройки редактируется в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="def32-p135">The following is an example of raw  **AppPrerequisites** markup that registers the Workflow capability. If you are using Visual Studio, you edit the add-in manifest in a designer tool.</span></span>
 

 



```
<AppPrerequisites>
  <AppPrerequisite Type="Capability" ID="{CDD8F991-B459-4512-8048-03D5A03FF27E}" MinimumVersion="15.0.0.0" />
</ AppPrerequisites>
```


## <a name="in-this-section"></a><span data-ttu-id="def32-288">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="def32-288">In this section</span></span>
<span data-ttu-id="def32-289"><a name="RegisterDependency"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-289"><a name="RegisterDependency"> </a></span></span>


-  [<span data-ttu-id="def32-290">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-290">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="def32-291">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-291">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)
    
 

## <a name="additional-resources"></a><span data-ttu-id="def32-292">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="def32-292">Additional resources</span></span>
<span data-ttu-id="def32-293"><a name="SPAppModelArch_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="def32-293"><a name="SPAppModelArch_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="def32-294">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-294">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="def32-295">Надстройки SharePoint в сравнении с решениями для SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-295">SharePoint Add-ins compared with SharePoint solutions</span></span>](http://msdn.microsoft.com/library/0e9efadb-aaf2-4c0d-afd5-d6cf25c4e7a8%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="def32-296">Разрешения для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-296">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint.md)
    
 
-  [<span data-ttu-id="def32-297">Поток OAuth токена контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-297">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="def32-298">Разработка пользовательского интерфейса для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-298">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="def32-299">IFrame</span><span class="sxs-lookup"><span data-stu-id="def32-299">IFrame</span></span>](http://www.w3schools.com/tags/tag_iframe.asp)
    
 
-  [<span data-ttu-id="def32-300">Изучение структуры манифеста приложения и пакета надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-300">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="def32-301">Развертывание и установка надстроек SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="def32-301">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)
    
 
-  <span data-ttu-id="def32-302">[Процесс обновления надстроек SharePoint](sharepoint-add-ins-update-process.md)</span><span class="sxs-lookup"><span data-stu-id="def32-302">[SharePoint Add-ins update process](sharepoint-add-ins-update-process.md).</span></span>
    
 
-  [<span data-ttu-id="def32-303">Области клиентов и области развертывания для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="def32-303">Tenancies and deployment scopes for SharePoint Add-ins</span></span>](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md)
    
 

