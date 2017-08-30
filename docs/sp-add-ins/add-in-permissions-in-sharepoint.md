# <a name="add-in-permissions-in-sharepoint"></a><span data-ttu-id="9b79b-101">Разрешения для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-101">Add-in permissions in SharePoint</span></span>
<span data-ttu-id="9b79b-p101">Сведения о разрешениях для надстроек SharePoint, в том числе о типах разрешений, областях запросов и управлении разрешениями. В этой статье также рассматриваются отличия между правами для надстроек, пользователей и приложений Магазина Office.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p101">Learn about add-in permissions in SharePoint, including types of add-in permissions, permission request scopes, and managing permissions. This article also discusses the differences in add-in permission rights, user rights, and Office Store app rights. You should first be familiar with the topic  Authorization and authentication of SharePoint Add-ins before you read this article.</span></span>
 

 <span data-ttu-id="9b79b-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="9b79b-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="9b79b-107">Прежде чем читать эту статью, необходимо ознакомиться со статьей [Авторизация и проверка подлинности надстроек SharePoint](authorization-and-authentication-of-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="9b79b-107">You should first be familiar with the topic [Authorization and authentication for apps in SharePoint 2013](authorization-and-authentication-of-sharepoint-add-ins) before you read this article.</span></span> 

## <a name="get-an-overview-of-add-in-permissions-in-sharepoint"></a><span data-ttu-id="9b79b-108">Общие сведения о разрешениях для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-108">Get an overview of add-in permissions in SharePoint</span></span>
<span data-ttu-id="9b79b-109"><a name="Perm_intro"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-109"></span></span>

<span data-ttu-id="9b79b-p103">Надстройка SharePoint запрашивает разрешения, необходимые во время установки, у пользователя, который выполняет установку. Разработчик надстройки должен запрашивать разрешения, которые нужны надстройке для запуска, с помощью файла манифеста. Пользователь, запускающий надстройку, должен предоставить разрешения устройствам и веб-приложениям, которые получают доступ к SharePoint, но не установлены на веб-сайтах SharePoint, в среде выполнения. Дополнительные сведения можно узнать в статье  [Общие сведения о надстройках, запрашивающих разрешение на доступ из SharePoint во время выполнения](authorization-code-oauth-flow-for-sharepoint-add-ins#Overview). Пользователи могут предоставлять только те разрешения, которыми обладают. Пользователь может предоставить надстройке либо все необходимые разрешения, либо никаких. Выборочное предоставление разрешений невозможно. Если надстройка запрашивает разрешения в ходе выполнения, ее может запускать только пользователь с разрешениями уровня "Управление" на ресурсы SharePoint, даже если надстройке требуются разрешения более низкого уровня, например "Чтение".</span><span class="sxs-lookup"><span data-stu-id="9b79b-p103">a SharePoint Add-in requests the permissions that it needs during installation from the user who is installing it. The developer of an add-in must request, through the add-in manifest file, the permissions that the particular add-in needs to be able to run. (Device and web apps that access SharePoint, but are not installed to SharePoint websites must be granted permissions at runtime by the user who is executing the add-in. For more information, see  [Get an overview of add-ins that request access permission from SharePoint on the fly](authorization-code-oauth-flow-for-sharepoint-add-ins#Overview).) Users can grant only the permissions that they have. The user must grant all the permissions that an add-in requests or not grant any permission. Selective grants are not possible. (For add-ins that request permissions on the fly, only a user with Manage permissions to the SharePoint resources that the add-in seeks to access can run the add-in, even if the add-in is asking only for lesser permissions, such as Read.)</span></span>
 

 
<span data-ttu-id="9b79b-p104">Предоставленные надстройке разрешения также хранятся в базе данных контента для фермы SharePoint или области клиента SharePoint Online. Они не хранятся в службе токенов безопасности, например Служба контроля доступа Microsoft Azure (ACS). Когда пользователь впервые предоставляет надстройке разрешения, SharePoint получает сведения о надстройке из службы контроля доступа. Затем SharePoint сохраняет основные сведения о надстройке и ее разрешения в службе управления надстройками и базе данных контента. Дополнительные сведения о службе контроля доступа можно узнать в статье  [Создание надстроек для SharePoint, которые используют авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization).</span><span class="sxs-lookup"><span data-stu-id="9b79b-p104">The permissions that the add-in has been granted are also stored in the content database of the SharePoint farm or SharePoint Online tenancy. They are not stored with a secure token service, such as Microsoft Azure Access Control Service (ACS). When a user first grants an add-in permissions, SharePoint obtains information about the add-in from ACS. SharePoint then stores the basic information about the add-in in the add-in management service and the content database along with the add-in's permissions. For more information about ACS, see  [Creating SharePoint Add-ins that use low-trust authorization](creating-sharepoint-add-ins-that-use-low-trust-authorization).</span></span>
 

 
<span data-ttu-id="9b79b-p105">Если объект, на доступ к которому надстройке было предоставлено разрешение, удаляется, соответствующее разрешение также удаляется. Если же такой объект помещается в корзину, SharePoint не изменяет соответствующее разрешение. Это нужно для того, чтобы в случае восстановления объекта из корзины разрешение сохранилось.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p105">If an object to which an add-in was granted permission is deleted, the corresponding grants are deleted also. When an object to which an add-in was granted permission is recycled, SharePoint does not modify the corresponding grant. This is so that if the object is restored from the Recycle Bin, the grant is still intact.</span></span>
 

 
<span data-ttu-id="9b79b-p106">При удалении надстройки отзываются все разрешения, предоставленные ей для области, из которой она удаляется. Это необходимо для того, чтобы надстройка не могла использовать свои учетные данные для удаленного доступа к защищенным ресурсам SharePoint после того, как пользователь удалит ее из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p106">When an add-in is removed, all the permissions granted to that add-in at the scope from which it was removed are revoked. This is to ensure that the add-in can't use its credentials to continue accessing protected SharePoint resources remotely after a user removes the add-in from SharePoint.</span></span>
 

 

## <a name="understand-the-types-of-add-in-permissions-and-permission-scopes"></a><span data-ttu-id="9b79b-127">Основные сведения о типах и областях разрешений надстройки</span><span class="sxs-lookup"><span data-stu-id="9b79b-127">Understand the types of add-in permissions and permission scopes</span></span>
<span data-ttu-id="9b79b-128"><a name="Perm_types"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-128"></span></span>

<span data-ttu-id="9b79b-p107">С помощью запросов Надстройка SharePoint получает разрешения, необходимые для ее правильной работы. В запросах разрешений указываются как права, требуемые надстройке, так и область их действия. Разрешения запрашиваются в рамках манифеста надстройки.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p107">A SharePoint Add-in uses permission requests to specify the permissions that it needs to function correctly. The permission requests specify both the rights that an add-in needs and the scope at which it needs the rights. These permissions are requested as part of the add-in manifest.</span></span>
 

 

 <span data-ttu-id="9b79b-p108">**Примечание.** Области, описываемые в этом разделе, применимы к только содержимому списков и библиотек. Сведения об областях для других компонентов см. в разделе [Основные сведения о типах и областях разрешений надстройки](#Perm_types) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p108">**Note** The scopes described in this section apply to list content and library content only. For information about scopes for other features, see the  [Understand the types of add-in permissions and permission scopes](#Perm_types) section in this article.</span></span>
 

<span data-ttu-id="9b79b-134">Области запросов разрешений указывают расположение в иерархии SharePoint, на которое распространяется запрос разрешений.</span><span class="sxs-lookup"><span data-stu-id="9b79b-134">Permission request scopes indicate the location in the SharePoint hierarchy where a permission request applies.</span></span>
 

 

 <span data-ttu-id="9b79b-p109">**Примечание.** Надстройка SharePoint обладает собственным удостоверением и является субъектом безопасности, который называется субъектом надстройки. Аналогично пользователям и группам, субъект надстройки располагает определенными разрешениями или правами. У него есть права на полный доступ к сайту надстройки, поэтому ему требуется запрашивать разрешения на доступ к ресурсам SharePoint только на хост-сайте и в других расположениях вне сайта надстройки. Дополнительные сведения о сайте надстройки см. в статьях [Важные аспекты разработки и архитектуры для надстроек SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape) и [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="9b79b-p109">**Note** A SharePoint Add-in has its own identity and is a security principal, called an add-in principal. Like users and groups, an add-in principal has certain permissions or rights. The add-in principal has full control rights to the add-in web so it only needs to request permissions to SharePoint resources in the host web or other locations outside the add-in web. For more information about add-in web, see  [Important aspects of the SharePoint Add-in architecture and development landscape](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape) and [Host webs, add-in webs, and SharePoint components in SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013).</span></span>
 

<span data-ttu-id="9b79b-p110">SharePoint поддерживает четыре различных области разрешений для базы данных контента и области клиента, как показано в таблице 1. Названия областей разрешений совпадают с кодами URI, включая префикс http:, но они не являются URL-адресами и не содержат заполнителей. Области разрешений, перечисленные в этих статье и таблице, строки литералов.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p110">SharePoint supports four different permission scopes within the content database and tenancy, as shown in Table 1. Permission scopes are named with URIs, including a "http:" prefix, but they are not URLs and they contain no placeholders. The permission scopes in this table and this article are literal strings.</span></span>
 

 

<span data-ttu-id="9b79b-142">**Таблица 1. URI и описания областей запросов разрешений для надстроек SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9b79b-142">**Table 1. SharePoint add-in permission request scope URIs and descriptions**</span></span>

|<span data-ttu-id="9b79b-143">**Область**</span><span class="sxs-lookup"><span data-stu-id="9b79b-143">**Scope**</span></span>|<span data-ttu-id="9b79b-144">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-144">**Scope URI**</span></span>|<span data-ttu-id="9b79b-145">**Описание**</span><span class="sxs-lookup"><span data-stu-id="9b79b-145">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="9b79b-146">Клиент</span><span class="sxs-lookup"><span data-stu-id="9b79b-146">tenancy</span></span>| <span data-ttu-id="9b79b-147">http://sharepoint/content/tenant</span><span class="sxs-lookup"><span data-stu-id="9b79b-147">http://sharepoint/content/tenant</span></span>|<span data-ttu-id="9b79b-p111">Клиент, в котором установлена надстройка. Включает все дочерние элементы этой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p111">The tenancy where the add-in is installed. Includes all children of this scope.</span></span>|
|<span data-ttu-id="9b79b-150">Семейство веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="9b79b-150">Site Collection</span></span>| <span data-ttu-id="9b79b-151">http://sharepoint/content/sitecollection</span><span class="sxs-lookup"><span data-stu-id="9b79b-151">http://sharepoint/content/sitecollection</span></span>|<span data-ttu-id="9b79b-p112">Семейство веб-сайтов, в котором установлена надстройка. Включает все дочерние элементы этой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p112">The site collection where the add-in is installed. Includes all children of this scope.</span></span>|
|<span data-ttu-id="9b79b-154">Веб-сайт</span><span class="sxs-lookup"><span data-stu-id="9b79b-154">Website</span></span>| <span data-ttu-id="9b79b-155">http://sharepoint/content/sitecollection/web</span><span class="sxs-lookup"><span data-stu-id="9b79b-155">http://sharepoint/content/sitecollection/web</span></span>|<span data-ttu-id="9b79b-p113">Веб-сайт, на котором установлена надстройка. Включает все дочерние элементы этой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p113">The website where the add-in is installed. Includes all children of this scope.</span></span>|
|<span data-ttu-id="9b79b-158">Список</span><span class="sxs-lookup"><span data-stu-id="9b79b-158">List</span></span>| <span data-ttu-id="9b79b-159">http://sharepoint/content/sitecollection/web/list</span><span class="sxs-lookup"><span data-stu-id="9b79b-159">http://sharepoint/content/sitecollection/web/list</span></span>|<span data-ttu-id="9b79b-p114">Представляет собой единый список веб-сайта, на котором установлена надстройка. Когда пользователю, который устанавливает надстройку, предлагается предоставить разрешения, в диалоговом окне он может выбрать один список, для которого надстройке предоставляются разрешения. Если надстройка требует разрешения более чем для одного списка, необходимо запрашивать разрешение для веб-области. Поскольку у разработчиков нет возможности контролировать выбор списков пользователями, равно как и сообщать последним, какой список следует выбрать, необходимо использовать веб-область, если есть такой список, для которого у вашей надстройки  *должно*  быть разрешение. (Тем не менее, существует возможность ограничить выбор пользователей определенными подмножествами списков. См. раздел [Область запроса разрешений со связанными свойствами](#AssociatedProperties) ниже.) </span><span class="sxs-lookup"><span data-stu-id="9b79b-p114">A single list in the website where the add-in is installed. When the user who installs the add-in is prompted to grant permissions, the dialog enables the user to select one list to which the add-in is granted permissions. If the add-in needs permission to more than one list, it must request permission to web scope. Also, since you, the developer, have no way to control which list the user chooses or to tell the user which one to choose, you must use web scope if there is a list to which your add-in  *must*  have permission. (But there is a way to narrow the user's choice to certain subsets of lists. See [Permission request scope with associated properties](#AssociatedProperties) below.)</span></span>|

<span data-ttu-id="9b79b-p115">Если надстройке предоставлено разрешение на одну из областей, оно применяется ко всем дочерним элементам в этой области. Например, если надстройке предоставлено разрешение на доступ к веб-сайту, ей также предоставляется разрешение на доступ ко всем спискам на веб-сайте и всем элементам этих списков.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p115">If an add-in is granted permission to one of the scopes, the permission applies to all children of the scope. For example, if an add-in is granted permission to a website, the add-in is also granted permission to each list that is contained in the website, and all list items that are in each list.</span></span>
 

 
<span data-ttu-id="9b79b-p116">Поскольку запросы разрешений выполняются безотносительно к топологии семейства веб-сайтов, в котором установлена надстройка, область указывается как тип, а не как URL-адрес определенного экземпляра. Эти типы областей выражаются в виде универсальных кодов ресурсов (URI). Разрешения для ресурсов, которые хранятся в базе данных контента SharePoint, упорядочены по следующему URI:  `http://sharepoint/content`.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p116">Because permission requests are made without information about the topology of the site collection where the add-in is installed, the scope is expressed as a type instead of as the URL of a specific instance. These scope types are expressed as URIs. Permissions to resources that are stored in the SharePoint content database are organized under the following URI:  `http://sharepoint/content`.</span></span>
 

 

## <a name="understand-the-differences-between-add-in-permission-rights-and-user-rights"></a><span data-ttu-id="9b79b-171">Различия между правами, связанными с разрешениями надстройки, и правами пользователя</span><span class="sxs-lookup"><span data-stu-id="9b79b-171">Understand the differences between add-in permission rights and user rights</span></span>
<span data-ttu-id="9b79b-172"><a name="Perm_diff"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-172"></span></span>

<span data-ttu-id="9b79b-p117">Разрешения определяют действия, которые надстройке разрешено выполнять в рамках данной области. SharePoint поддерживает четыре уровня прав на доступ к базе данных контента. В каждой области надстройка может иметь следующие права:</span><span class="sxs-lookup"><span data-stu-id="9b79b-p117">Permissions indicate the activities that an add-in is permitted to do within the requested scope. SharePoint supports four rights levels in the content database. For each scope, an add-in can have the following rights:</span></span>
 

 

- <span data-ttu-id="9b79b-176">Чтение</span><span class="sxs-lookup"><span data-stu-id="9b79b-176">Read</span></span>
    
 
- <span data-ttu-id="9b79b-177">Запись</span><span class="sxs-lookup"><span data-stu-id="9b79b-177">Write</span></span>
    
 
- <span data-ttu-id="9b79b-178">Управление</span><span class="sxs-lookup"><span data-stu-id="9b79b-178">Manage</span></span>
    
 
- <span data-ttu-id="9b79b-179">FullControl</span><span class="sxs-lookup"><span data-stu-id="9b79b-179">Full-control</span></span>
    
 

 <span data-ttu-id="9b79b-180">**Примечание.** Дополнительные сведения о составе прав Read, Write, Manage и FullControl см. в статье [Планирование управления разрешениями надстроек](http://technet.microsoft.com/en-us/library/jj219576%28office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b79b-180">**Note** For more information about what Read, Write, Manage, and FullControl rights include, see  [Plan add-in permissions management](http://technet.microsoft.com/en-us/library/jj219576%28office.15%29.aspx).</span></span>
 


 <span data-ttu-id="9b79b-p118">**Примечание.** Эти права соответствуют стандартным уровням разрешений для пользователей SharePoint: "Читатель", "Участник", "Разработчик" и "Полный доступ". Дополнительные сведения об уровнях разрешений для пользователей см. в статье [Разрешения и уровни разрешений для пользователей](http://technet.microsoft.com/en-us/library/cc288074.aspx). Имена прав для надстроек не совпадают с названиями прав для ролей пользователей SharePoint, чтобы их невозможно было перепутать друг с другом. Настройка разрешений, связанных с ролями пользователей SharePoint, не влияет на уровни разрешений для надстроек, поэтому имена прав для надстроек не совпадают с названиями соответствующих ролей пользователей SharePoint (за исключением разрешения "Полный доступ", которое невозможно настраивать с помощью пользовательского интерфейса управления разрешениями).</span><span class="sxs-lookup"><span data-stu-id="9b79b-p118">**Note**  These rights correspond to the default user permission levels of SharePoint: Reader, Contributor, Designer, and Full Control. For more information about user permission levels, see  [User permissions and permission levels](http://technet.microsoft.com/en-us/library/cc288074.aspx).The add-ins rights names do not match SharePoint user roles rights names, to avoid confusion between user roles rights and add-in rights. Because customizing the permissions that are associated with SharePoint user roles does not affect add-in permission request levels, the add-in rights names do not match the corresponding SharePoint user roles, except Full Control, which can't be customized through the permissions management user interface.</span></span>
 

<span data-ttu-id="9b79b-184">Кроме того:</span><span class="sxs-lookup"><span data-stu-id="9b79b-184">In addition:</span></span>
 

 

- <span data-ttu-id="9b79b-185">Надстройка может иметь право на выполнение запросов только в области поиска.</span><span class="sxs-lookup"><span data-stu-id="9b79b-185">For Search only, an add-in can have the Query right.</span></span>
    
 
- <span data-ttu-id="9b79b-p119">Для некоторых областей Microsoft Project Server 2013 также имеются права на отправку состояния и повышение прав. Для большинства областей Project Server 2013 доступны только права на чтение и запись. Подробнее можно узнать в разделе  [Основные сведения о типах и областях разрешений надстройки](#Perm_types) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p119">For some Microsoft Project Server 2013 scopes, there is also the SubmitStatus right or the Elevate right. For most scopes for Project Server 2013, only Read and Write are available. For more information, see the  [Understand the types of add-in permissions and permission scopes](#Perm_types) section in this article.</span></span>
    
 
- <span data-ttu-id="9b79b-189">Для таксономии доступны только права на чтение и запись.</span><span class="sxs-lookup"><span data-stu-id="9b79b-189">For taxonomy, only rights for Read and Write are available.</span></span>
    
 

 <span data-ttu-id="9b79b-p120">**Примечание.** В отношении прав, которые могут запрашивать надстройки из Магазина Office, действуют некоторые ограничения. Дополнительные сведения см. в разделе [Основные сведения о типах и областях разрешений надстройки](#Perm_types) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p120">**Note** Office Store apps have some restrictions as to what type of rights an add-in can request. For more information, see the  [Understand the types of add-in permissions and permission scopes](#Perm_types) section in this article.</span></span>
 

<span data-ttu-id="9b79b-p121">В отличие от ролей пользователей SharePoint, эти уровни прав недоступны для настройки. Это позволяет гарантировать, что если надстройка запрашивает разрешения, ей предоставляется предсказуемый набор возможностей. При этом надстройке не нужно учитывать возможность того, что ей будет предоставлен более низкий уровень разрешений, чем требуется.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p121">Unlike SharePoint user roles, these rights levels are not customizable. This is to ensure that when an add-in is granted a permission request, the add-in is guaranteed a predictable set of capabilities, and it does not have to account for the possibility of being granted less permission than it expects.</span></span>
 

 
<span data-ttu-id="9b79b-p122">Пользователь не может предоставить надстройке разрешения, которых у него нет. При попытке установить надстройку, которой требуется больше разрешений, чем есть у пользователя, отображается соответствующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p122">A user cannot grant an add-in permissions that the user himself or herself does not have. If a user attempts to install an add-in that requests more permissions than the user has, an error message displays to the user informing them that they don't have sufficient permissions to grant the add-in its request.</span></span>
 

 
<span data-ttu-id="9b79b-p123">Разрешения, которые неизвестны системе SharePoint, игнорируются. Это означает, что если надстройка запрашивает разрешение, которое не распознается системой SharePoint, эту надстройку можно установить, но она не запрашивает разрешение у пользователя и не получает его.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p123">Permissions that are not known to SharePoint are ignored. This means that, if an add-in requests a permission that SharePoint does not recognize, the add-in can still be installed, but the user is not prompted to grant the permission, and the permission is not granted to the add-in.</span></span>
 

 

## <a name="learn-about-the-available-scopes-and-permissions-and-about-the-restrictions-on-office-store-apps-permissions"></a><span data-ttu-id="9b79b-198">Сведения о доступных областях и разрешениях, а также ограничениях, связанных с разрешениями надстроек Магазин Office</span><span class="sxs-lookup"><span data-stu-id="9b79b-198">Learn about the available scopes and permissions, and about the restrictions on Office Store apps permissions</span></span>
<span data-ttu-id="9b79b-199"><a name="Perm_rightlist"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-199"></span></span>

<span data-ttu-id="9b79b-p124">Различные области имеют разные наборы прав, которые может запросить надстройка. В этом разделе описываются наборы прав, доступные для каждой области. В нем также рассматриваются ограничения на Надстройки SharePoint, которые продаются через Магазин Office.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p124">Different scopes have different sets of rights that are available for an add-in to request. This section describes the sets of rights that are available for each scope. Also, it highlights the restrictions for SharePoint Add-ins that are sold through the Office Store.</span></span>
 

 

### <a name="office-store-apps-rights"></a><span data-ttu-id="9b79b-203">Права надстроек Магазин Office</span><span class="sxs-lookup"><span data-stu-id="9b79b-203">Office Store apps' rights</span></span>

<span data-ttu-id="9b79b-p125">Для надстроек из Магазин Office доступны только права на чтение, запись и управление. Если вы попытаетесь отправить в Магазин Office надстройку, требующую права на полный доступ, отправка будет заблокирована. Поскольку блокировка происходит в процессе отправки в Магазин Office, надстройки, которые запрашивают уровень разрешений выше, чем "Управление", можно развертывать через каталог надстроек.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p125">Only Read, Write, and Manage rights are allowed for Office Store apps. If you try to submit an app to the Office Store that requires FullControl rights, your app is blocked from submission. Because the block is in the Office Store submission pipeline, apps that request more than Manage permissions can still be deployed through the add-in catalog.</span></span>
 

 

### <a name="permission-request-scopes-for-list-content-and-library-content"></a><span data-ttu-id="9b79b-207">Области запроса разрешений для содержимого списков и библиотек</span><span class="sxs-lookup"><span data-stu-id="9b79b-207">Permission request scopes for list content and library content</span></span>
<span data-ttu-id="9b79b-208"><a name="PermissionsForLists"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-208"></span></span>

<span data-ttu-id="9b79b-p126">В таблице 2 показаны области запроса разрешений для содержимого списков и библиотек. В ней также перечислены права, которые можно указать для универсального кода ресурса (URI) каждой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p126">Table 2 shows the permission request scope for list and library content. It also lists the rights that can be specified for each scope URI.</span></span>
 

 

 <span data-ttu-id="9b79b-211">**Примечание.** URI, используемые в таблице 2, являются литералами.</span><span class="sxs-lookup"><span data-stu-id="9b79b-211">**Note** The URIs used in Table 2 are literal values.</span></span>
 


<span data-ttu-id="9b79b-212">**Таблица 2. URI областей разрешений для надстроек SharePoint и доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-212">**Table 2. SharePoint add-in permission scope URIs and available rights**</span></span>

|<span data-ttu-id="9b79b-213">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-213">**Scope URI**</span></span>|<span data-ttu-id="9b79b-214">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-214">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9b79b-215">http://sharepoint/content/sitecollection</span><span class="sxs-lookup"><span data-stu-id="9b79b-215">http://sharepoint/content/sitecollection</span></span>|<span data-ttu-id="9b79b-216">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="9b79b-216">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="9b79b-217">http://sharepoint/content/sitecollection/web</span><span class="sxs-lookup"><span data-stu-id="9b79b-217">http://sharepoint/content/sitecollection/web</span></span>|<span data-ttu-id="9b79b-218">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="9b79b-218">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="9b79b-219">http://sharepoint/content/sitecollection/web/list</span><span class="sxs-lookup"><span data-stu-id="9b79b-219">http://sharepoint/content/sitecollection/web/list</span></span>|<span data-ttu-id="9b79b-220">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="9b79b-220">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="9b79b-221">http://sharepoint/content/tenant</span><span class="sxs-lookup"><span data-stu-id="9b79b-221">http://sharepoint/content/tenant</span></span>|<span data-ttu-id="9b79b-222">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="9b79b-222">Read, Write, Manage, FullControl</span></span>|
<span data-ttu-id="9b79b-p127">В следующем фрагменте кода демонстрируется использование областей разрешений и прав в файле AppManifest.xml. В первом примере надстройка запрашивает разрешение на чтение для области списка.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p127">The following code shows how you use permission scopes and rights in the AppManifest.xml file. In the first example, an add-in is asking for Write access to the list scope.</span></span>
 

 



```XML
<?xml version="1.0" encoding="utf-8" ?>
<App xmlns="http://schemas.microsoft.com/sharepoint/2012/app/manifest"
     ProductID="{4a07f3bd-803d-45f2-a710-b9e944c3396e}"
     Version="1.0.0.0"
     SharePointMinVersion="15.0.0.0"
     Name="MySampleAddIn"
>
  <Properties>
    <Title>My Sample Add-in</Title>
    <StartPage>~remoteAppUrl/Home.aspx?{StandardTokens}</StartPage>
  </Properties>

  <AppPrincipal>
    <RemoteWebApplication ClientId="1ee82b34-7c1b-471b-b27e-ff272accd564" />
  </AppPrincipal>

  <AppPermissionRequests>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write"/>
  </AppPermissionRequests>
</App>
```

<span data-ttu-id="9b79b-225">В следующем фрагменте кода надстройка запрашивает разрешение на чтение для области сайта и разрешение на запись для области списка.</span><span class="sxs-lookup"><span data-stu-id="9b79b-225">The following code shows an add-in that is asking for Read access to the web scope and Write access to the list scope.</span></span>
 

 



```XML
<?xml version="1.0" encoding="utf-8" ?>
<App xmlns="http://schemas.microsoft.com/sharepoint/2012/app/manifest"
     ProductID="{4a07f3bd-803d-45f2-a710-b9e944c3396e}"
     Version="1.0.0.0"
     SharePointMinVersion="15.0.0.0"
     Name="MySampleAddIn"
>
  <Properties>
    <Title>My Sample Add-in</Title>
    <StartPage>~remoteAppUrl/Home.aspx?{StandardTokens}</StartPage>
  </Properties>

  <AppPrincipal>
    <RemoteWebApplication ClientId="6daebfdd-6516-4506-a7a9-168862921986" />
  </AppPrincipal>

  <AppPermissionRequests>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="Read"/>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write"/>
  </AppPermissionRequests>
</App>
```


### <a name="permission-request-scopes-for-other-sharepoint-features"></a><span data-ttu-id="9b79b-226">Области запроса разрешений для других компонентов SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-226">Permission request scopes for other SharePoint features</span></span>
<span data-ttu-id="9b79b-227"><a name="PermissionsForLists"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-227"></span></span>

<span data-ttu-id="9b79b-228">В приведенных ниже таблицах перечислены области разрешений для других компонентов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9b79b-228">The permission request scope for other SharePoint features are listed in the following tables.</span></span> 
 

 

 <span data-ttu-id="9b79b-229">**Примечание.** URI в этих таблицах являются литералами.</span><span class="sxs-lookup"><span data-stu-id="9b79b-229">**Note** The URIs used in the tables are literal values.</span></span>
 

<span data-ttu-id="9b79b-p128">В таблице 3 показана область запроса разрешений для Службы Business Connectivity Services (BCS). В ней также перечислены права, которые можно указать для универсального кода ресурса (URI) этой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p128">Table 3 shows the permission request scope for Business Connectivity Services (BCS) . It also lists the rights that can be specified for that scope URI.</span></span>
 

 

<span data-ttu-id="9b79b-232">**Таблица 3. Коды URI области запроса разрешений надстройки для Business Connectivity Services и доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-232">**Table 3. BCS add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="9b79b-233">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-233">**Scope URI**</span></span>|<span data-ttu-id="9b79b-234">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-234">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9b79b-235">http://sharepoint/bcs/connection</span><span class="sxs-lookup"><span data-stu-id="9b79b-235">http://sharepoint/bcs/connection</span></span>|<span data-ttu-id="9b79b-236">Чтение</span><span class="sxs-lookup"><span data-stu-id="9b79b-236">Read</span></span>|

 <span data-ttu-id="9b79b-237">**Примечание.** Дополнительные сведения об области разрешений служб BCS для надстроек см. в статье [Business Connectivity Services в SharePoint](http://msdn.microsoft.com/library/64b7d032-4b83-4e9e-bc08-f0a161af5457%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b79b-237">**Note** For more information about the BCS add-in permission request scope, see  [Business Connectivity Services in SharePoint](http://msdn.microsoft.com/library/64b7d032-4b83-4e9e-bc08-f0a161af5457%28Office.15%29.aspx).</span></span>
 


 

 
<span data-ttu-id="9b79b-p129">В таблице 4 показана область разрешений для службы поиска. В ней также перечислены права, которые можно задать для этого URI области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p129">Table 4 shows the permission request scope for Search. It also lists the rights that can be specified for that scope URI.</span></span>
 

 

<span data-ttu-id="9b79b-240">**Таблица 4. Коды URI области запроса разрешений надстройки для поиска и доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-240">**Table 4. Search add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="9b79b-241">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-241">**Scope URI**</span></span>|<span data-ttu-id="9b79b-242">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-242">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9b79b-243">http://sharepoint/search</span><span class="sxs-lookup"><span data-stu-id="9b79b-243">http://sharepoint/search</span></span>|<span data-ttu-id="9b79b-244">QueryAsUserIgnoreAppPrincipal</span><span class="sxs-lookup"><span data-stu-id="9b79b-244">QueryAsUserIgnoreAppPrincipal</span></span>|

 <span data-ttu-id="9b79b-245">**Примечание.** Дополнительные сведения об области разрешений службы поиска для надстроек см. в статье [Поиск в SharePoint](http://msdn.microsoft.com/library/59220f81-0e5e-4945-8056-cf0a116446cb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b79b-245">**Note** For more information about the Search add-in permission request scope, see  [Search in SharePoint](http://msdn.microsoft.com/library/59220f81-0e5e-4945-8056-cf0a116446cb%28Office.15%29.aspx).</span></span>
 


 

 
<span data-ttu-id="9b79b-p130">В таблице 5 показана область запроса разрешений для Project Server 2013. В ней также перечислены права, которые можно указать для универсального кода ресурса (URI) каждой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p130">Table 5 shows the permission request scope for Project Server 2013. It also lists the rights that can be specified for each scope URI.</span></span>
 

 

 <span data-ttu-id="9b79b-p131">**Примечание.** Надстройку с использованием компонентов и служб Project Server 2013 следует тестировать в среде, содержащей необходимые компоненты и службы Project Server. Сборка поставщика разрешений Project Server 2013, включающая сведения об областях разрешений Project Server 2013, не устанавливается в SharePoint Server по умолчанию. Дополнительные сведения см. в документации по Project Server 2013 для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p131">**Note** An add-in that uses Project Server 2013 features and services should be tested in an environment that has the required Project Server features and services. The Project Server 2013 permission provider assembly that knows about Project Server 2013 permission scopes is not installed by default with SharePoint Server. For more information, see the Project Server 2013 developer documentation.</span></span>
 


<span data-ttu-id="9b79b-251">**Таблица 5. URI областей разрешений и доступные права для надстроек Project Server**</span><span class="sxs-lookup"><span data-stu-id="9b79b-251">**Table 5. Project Server add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="9b79b-252">**Область**</span><span class="sxs-lookup"><span data-stu-id="9b79b-252">**Scope**</span></span>|<span data-ttu-id="9b79b-253">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-253">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9b79b-254">http://sharepoint/projectserver</span><span class="sxs-lookup"><span data-stu-id="9b79b-254">http://sharepoint/projectserver</span></span>|<span data-ttu-id="9b79b-255">Управление</span><span class="sxs-lookup"><span data-stu-id="9b79b-255">Manage</span></span>|
|<span data-ttu-id="9b79b-256">http://sharepoint/projectserver/projects</span><span class="sxs-lookup"><span data-stu-id="9b79b-256">http://sharepoint/projectserver/projects</span></span>|<span data-ttu-id="9b79b-257">Чтение, запись</span><span class="sxs-lookup"><span data-stu-id="9b79b-257">Read, Write</span></span>|
|<span data-ttu-id="9b79b-258">http://sharepoint/projectserver/projects/project</span><span class="sxs-lookup"><span data-stu-id="9b79b-258">http://sharepoint/projectserver/projects/project</span></span>|<span data-ttu-id="9b79b-259">Чтение, запись</span><span class="sxs-lookup"><span data-stu-id="9b79b-259">Read, Write</span></span>|
|<span data-ttu-id="9b79b-260">http://sharepoint/projectserver/enterpriseresources</span><span class="sxs-lookup"><span data-stu-id="9b79b-260">http://sharepoint/projectserver/enterpriseresources</span></span>|<span data-ttu-id="9b79b-261">Чтение, запись</span><span class="sxs-lookup"><span data-stu-id="9b79b-261">Read, Write</span></span>|
|<span data-ttu-id="9b79b-262">http://sharepoint/projectserver/statusing</span><span class="sxs-lookup"><span data-stu-id="9b79b-262">http://sharepoint/projectserver/statusing</span></span>|<span data-ttu-id="9b79b-263">SubmitStatus</span><span class="sxs-lookup"><span data-stu-id="9b79b-263">SubmitStatus</span></span>|
|<span data-ttu-id="9b79b-264">http://sharepoint/projectserver/reporting</span><span class="sxs-lookup"><span data-stu-id="9b79b-264">http://sharepoint/projectserver/reporting</span></span>|<span data-ttu-id="9b79b-265">Чтение</span><span class="sxs-lookup"><span data-stu-id="9b79b-265">Read</span></span>|
|<span data-ttu-id="9b79b-266">http://sharepoint/projectserver/workflow</span><span class="sxs-lookup"><span data-stu-id="9b79b-266">http://sharepoint/projectserver/workflow</span></span>|<span data-ttu-id="9b79b-267">Повышение прав</span><span class="sxs-lookup"><span data-stu-id="9b79b-267">Elevate</span></span>|

 

 
<span data-ttu-id="9b79b-p132">В таблице 6 показана область запроса разрешений для социальных функций. В ней также перечислены права, которые можно указать для универсального кода ресурса (URI) каждой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p132">Table 6 shows the permission request scope for social features. It also lists the rights that can be specified for each scope URI.</span></span>
 

 

<span data-ttu-id="9b79b-270">**Таблица 6. Коды URI области запроса разрешений надстройки для социальных функций и доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-270">**Table 6. Social features add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="9b79b-271">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-271">**Scope URI**</span></span>|<span data-ttu-id="9b79b-272">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-272">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9b79b-273">http://sharepoint/social/tenant</span><span class="sxs-lookup"><span data-stu-id="9b79b-273">http://sharepoint/social/tenant</span></span>|<span data-ttu-id="9b79b-274">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="9b79b-274">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="9b79b-275">http://sharepoint/social/core</span><span class="sxs-lookup"><span data-stu-id="9b79b-275">http://sharepoint/social/core</span></span>|<span data-ttu-id="9b79b-276">Чтение, запись, управление, полный доступ</span><span class="sxs-lookup"><span data-stu-id="9b79b-276">Read, Write, Manage, FullControl</span></span>|
|<span data-ttu-id="9b79b-277">http://sharepoint/social/microfeed</span><span class="sxs-lookup"><span data-stu-id="9b79b-277">http://sharepoint/social/microfeed</span></span>|<span data-ttu-id="9b79b-278">Read, Write, Manage, FullControl</span><span class="sxs-lookup"><span data-stu-id="9b79b-278">Read, Write, Manage, FullControl</span></span>|

 <span data-ttu-id="9b79b-279">**Примечание.** Дополнительные сведения об области запроса разрешений надстройки для социальных функций см. в разделе [Добавление разрешений надстроек для доступа к социальным функциям](http://msdn.microsoft.com/library/8852ce36-8309-45a7-a141-2e10ac17a123%28Office.15%29.aspx#bkmk_AppPerms).</span><span class="sxs-lookup"><span data-stu-id="9b79b-279">**Note** For more information about social features add-in permission request scope, see  [Add-in permission requests for accessing social features](http://msdn.microsoft.com/library/8852ce36-8309-45a7-a141-2e10ac17a123%28Office.15%29.aspx#bkmk_AppPerms).</span></span>
 


 

 
<span data-ttu-id="9b79b-p133">В таблице 7 показана область разрешений для таксономии. В ней также перечислены права, которые можно задать для этого URI области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p133">Table 7 shows the permission request scope for taxonomy. It also lists the rights that can be specified for that scope URI.</span></span>
 

 

<span data-ttu-id="9b79b-282">**Таблица 7. Коды URI области запроса разрешений надстройки для таксономии и доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-282">**Table 7. Taxonomy add-in permission request scope URIs and available rights**</span></span>

|<span data-ttu-id="9b79b-283">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-283">**Scope URI**</span></span>|<span data-ttu-id="9b79b-284">**Доступные права**</span><span class="sxs-lookup"><span data-stu-id="9b79b-284">**Available Rights**</span></span>|
|:-----|:-----|
|<span data-ttu-id="9b79b-285">http://sharepoint/taxonomy</span><span class="sxs-lookup"><span data-stu-id="9b79b-285">http://sharepoint/taxonomy</span></span>|<span data-ttu-id="9b79b-286">Read, Write</span><span class="sxs-lookup"><span data-stu-id="9b79b-286">Read, Write</span></span>|

 <span data-ttu-id="9b79b-287">**Примечание.** Дополнительные сведения об области разрешений надстроек для таксономии см. в статье [Добавление возможностей SharePoint](http://msdn.microsoft.com/library/11ecb65e-6dc5-4cf1-80ca-3c16418697b6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b79b-287">**Note** For more information about the taxonomy add-in permission request scope, see  [Add SharePoint capabilities](http://msdn.microsoft.com/library/11ecb65e-6dc5-4cf1-80ca-3c16418697b6%28Office.15%29.aspx).</span></span>
 


### <a name="permission-request-scope-with-associated-properties"></a><span data-ttu-id="9b79b-288">Область запроса разрешений с соответствующими свойствами</span><span class="sxs-lookup"><span data-stu-id="9b79b-288">Permission request scope with associated properties</span></span>
<span data-ttu-id="9b79b-289"><a name="AssociatedProperties"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-289"></span></span>

<span data-ttu-id="9b79b-p134">Область запроса разрешений для списков содержит дополнительное необязательное свойство. Для области списка может быть определено свойство с именем **BaseTemplateId** и целочисленным значением, соответствующим базовому шаблону списка, как показано в приведенном ниже примере части кода. Если оно не задано, пользователь, устанавливающий надстройку, может предоставить разрешение для *одного из списков* на сайте. Если задать идентификатор базового шаблона, пользователю будет доступен только набор списков, соответствующих значению свойства **BaseTemplateId**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p134">The list permission request scope has an additional optional property. The list scope can take a property with the name **BaseTemplateId**, and an integer value corresponding with a list base template, as shown in the markup sample below. Without a base template ID, the user who installs the add-in has the choice of granting it permission to *one list*  from among all lists in the web. Specifying a base template ID limits the user's choice to the set of lists that match what is specified by the **BaseTemplateId** property.</span></span>
 

 
<span data-ttu-id="9b79b-p135">Свойство **BaseTemplateId** — это дочерний элемент, а не атрибут элемента **AppPermissionRequest**. В приведенном ниже коде демонстрируется использование свойства **BaseTemplateId**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p135">The **BaseTemplateId** property is a child element, not an attribute of the **AppPermissionRequest** element. The following code shows how to use the **BaseTemplateId** property.</span></span>
 

 



```XML
<AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write">
  <Property Name="BaseTemplateId" Value="101"/>
</AppPermissionRequest>
```


<span data-ttu-id="9b79b-296">**Таблица 7. Область запроса разрешений с соответствующими свойствами**</span><span class="sxs-lookup"><span data-stu-id="9b79b-296">**Table 7. Permission request scope with associated properties**</span></span>

|<span data-ttu-id="9b79b-297">**URI области**</span><span class="sxs-lookup"><span data-stu-id="9b79b-297">**Scope URI**</span></span>|<span data-ttu-id="9b79b-298">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="9b79b-298">**Property**</span></span>|<span data-ttu-id="9b79b-299">**Тип**</span><span class="sxs-lookup"><span data-stu-id="9b79b-299">**Type**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="9b79b-300">http://sharepoint/content/sitecollection/web/list</span><span class="sxs-lookup"><span data-stu-id="9b79b-300">http://sharepoint/content/sitecollection/web/list</span></span>|<span data-ttu-id="9b79b-301">**BaseTemplateId**</span><span class="sxs-lookup"><span data-stu-id="9b79b-301">**BaseTemplateId**</span></span>|<span data-ttu-id="9b79b-302">Целое число. **Примечание.** Дополнительные сведения о свойстве **BaseTemplateId** и соответствующем целочисленном значении для базового шаблона списка см. в описании атрибута **Type** [элемента List](http://msdn.microsoft.com/library/b2b26fee-eb45-48ac-99f1-65f725da293f%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b79b-302">For more information about **BaseTemplateId** and the corresponding integer value for the list base template, see the **Type** attribute of the [List Element (List)](http://msdn.microsoft.com/library/b2b26fee-eb45-48ac-99f1-65f725da293f%28Office.15%29.aspx).</span></span> |

## <a name="manage-and-troubleshoot-add-in-permissions"></a><span data-ttu-id="9b79b-303">Управление разрешениями для надстроек и устранение связанных с ними неполадок</span><span class="sxs-lookup"><span data-stu-id="9b79b-303">Manage and troubleshoot add-in permissions</span></span>
<span data-ttu-id="9b79b-304"><a name="Perm_manage"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-304"></span></span>

<span data-ttu-id="9b79b-p136">Надстройки SharePoint, установленные в SharePoint, получают разрешения во время своей установки. Надстройки, установленные на других платформах, но запрашивающие доступ к SharePoint, получают разрешения в ходе выполнения от пользователя, запустившего надстройку. Иногда надстройки первого типа могут терять разрешения. Чтобы повторно предоставить им разрешения, необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p136">SharePoint Add-ins that are installed to SharePoint are granted permissions when they are installed. Add-ins that are installed on other platforms but access SharePoint, are granted permissions at runtime, by the user who is running the add-in. Occasionally, the first kind of add-in may lose its permissions. Add-ins can be regranted its permissions with the following steps:</span></span>
 

 

1. <span data-ttu-id="9b79b-p137">На веб-сайте, где надстройка могла потерять разрешения, откройте страницу **Содержимое сайта** и нажмите кнопку **???** на плитке надстройки. Откроется выноска с еще одной кнопкой **???** или со ссылкой **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p137">On the **Site Contents** page of the website where the add-in seems to have lost permissions, click the **…** button on the add-in's tile. This will open a callout with either a **PERMISSIONS** link or another **…** button.</span></span>
    
 
2. <span data-ttu-id="9b79b-p138">Если ссылка **Разрешения** отображается, перейдите по ней и пропустите следующий этап. В противном случае нажмите кнопку **???**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p138">Click the **PERMISSIONS** link if it is there and skip the next step, or click the **…** button.</span></span>
    
 
3. <span data-ttu-id="9b79b-315">Перейдите по ссылке **Разрешения**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-315">Click the **Permissions** link.</span></span>
    
 
4. <span data-ttu-id="9b79b-p139">На открывшейся странице перейдите по ссылке **здесь** в последнем предложении. Надстройке будут заново назначены ее разрешения, и снова откроется страница **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p139">On the page that opens, click **here** link in the last sentence. This will regrant the add-in its permissions and redirect the browser back to the **Site Contents** page.</span></span>
    
 

 
![Повторное предоставление разрешений приложению](../../images/RegrantPermissionsToAnApp.png)
 
<span data-ttu-id="9b79b-p140">Иногда во время разработки надстройки или устранения неполадок в ней требуется изменить или повторно предоставить разрешения уже установленной надстройке. Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p140">When you are developing an add-in or troubleshooting an add-in, there may be occasions when you want to change, or regrant, the permissions of an add-in that has already been installed. You can do so with these steps:</span></span>
 

 

 

1. <span data-ttu-id="9b79b-p141">Перейдите по адресу `http://<SharePointWebSite>/_layouts/15/AppInv.aspx`, где _<SharePointWebSite>_ — это URL-адрес веб-сайта, где установлена надстройка. Не добавляйте к URL-адресу никаких параметров запроса. Нужная форма отображается на странице только при переходе по указанному выше URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p141">Navigate to  `http://<SharePointWebSite>/_layouts/15/AppInv.aspx`, where  _<SharePointWebSite>SharePointWebSite_ is the URL of the website where the add-in is installed. Be careful not to add any query parameters on the URL. The form you need only appears on this page if the URL is exactly as shown.</span></span>
    
 
2. <span data-ttu-id="9b79b-p142">Введите идентификатор надстройки (другое название — идентификатор клиента) в поле **ИД надстройки** и нажмите кнопку **Просмотр**. Остальные поля формы заполнятся сведениями о приложении.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p142">Enter the add-in's ID, also called the client ID, in the **Add-in Id** box and click **Lookup**. The other boxes on the form are then populated with information about the add-in.</span></span>
    
 
3. <span data-ttu-id="9b79b-p143">В поле **XML-запрос разрешения** укажите запросы разрешений в том же виде, что и в манифесте надстройки. Примеры можно найти выше в разделе [Области запроса разрешений для содержимого списков и библиотек](#PermissionsForLists). Полные сведения о синтаксисе см. в статье [Элемент AppPermissionRequest](http://msdn.microsoft.com/library/4ad90fb0-33b2-aee5-69c2-5b97ca5334f8%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b79b-p143">Fill the **Permission Request XML** box with permission requests exactly as you would enter them in an add-in manifest. For examples, see [Permission request scopes for list content and library content](#PermissionsForLists) above. For complete syntax information see [AppPermissionRequest Element](http://msdn.microsoft.com/library/4ad90fb0-33b2-aee5-69c2-5b97ca5334f8%28Office.15%29.aspx).</span></span>
    
 
4. <span data-ttu-id="9b79b-329">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9b79b-329">Click **Create**.</span></span> 
    
 
<span data-ttu-id="9b79b-330">При удалении надстройки из определенной области отзываются ее разрешения для этой области.</span><span class="sxs-lookup"><span data-stu-id="9b79b-330">An add-in's permissions for a specific scope are revoked when it is removed from that scope.</span></span>
 

 

## <a name="learn-why-add-ins-cannot-be-hidden-from-users"></a><span data-ttu-id="9b79b-331">Узнайте, почему надстройки невозможно скрывать от пользователей</span><span class="sxs-lookup"><span data-stu-id="9b79b-331">Learn why add-ins cannot be hidden from users</span></span>
<span data-ttu-id="9b79b-332"><a name="CannotBeHidden"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-332"></span></span>

<span data-ttu-id="9b79b-p144">Любой пользователь, имеющий права на просмотр веб-сайта SharePoint, может запустить любую надстройку SharePoint, установленную на этом сайте. Действия, которые пользователь может выполнять с надстройкой, зависят от других его разрешений и  [типа политики авторизации](add-in-authorization-policy-types-in-sharepoint-2013), которая используется надстройкой. Если пользователь попытается выполнить с помощью надстройки действие, разрешения на которое у него нет, а при вызове SharePoint будет использоваться политика "пользователь + надстройка", отправить вызов не удастся.</span><span class="sxs-lookup"><span data-stu-id="9b79b-p144">Any user with browse rights to a SharePoint website can launch any SharePoint Add-in installed on the site. Whether the user can do anything with the add-in will depend on the user's other permissions and what  [authorization policy type](add-in-authorization-policy-types-in-sharepoint-2013) is being used by the add-in. If the user tries to do something with the add-in that the user does not have permission to do, and the call to SharePoint is using the user+add-in policy, then the call will fail.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="9b79b-336">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9b79b-336">Additional resources</span></span>
<span data-ttu-id="9b79b-337"><a name="Filename_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="9b79b-337"></span></span>


-  [<span data-ttu-id="9b79b-338">Авторизация и проверка подлинности для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-338">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9b79b-339">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-339">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9b79b-340">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-340">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9b79b-341">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="9b79b-341">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="9b79b-342">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b79b-342">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 
