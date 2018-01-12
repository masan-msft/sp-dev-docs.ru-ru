---
title: "Назначение настраиваемых разрешений для списка с помощью интерфейса REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2fe15a33964aadcae0c1aa3495251a2475335c3f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="set-custom-permissions-on-a-list-by-using-the-rest-interface"></a><span data-ttu-id="2e48e-102">Назначение настраиваемых разрешений для списка с помощью интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="2e48e-102">Set custom permissions on a list by using the REST interface</span></span>
<span data-ttu-id="2e48e-103">Узнайте, как определять детальные настраиваемые разрешения для списка SharePoint с помощью интерфейса REST и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2e48e-103">Learn how to define custom, fine-grained permissions on a SharePoint list by using the REST interface and JavaScript.</span></span>

<span data-ttu-id="2e48e-p101">Сайты, списки и элементы списков SharePoint относятся к типу **SecurableObject**. По умолчанию защищаемый объект наследует разрешения от родительского объекта. Чтобы задать настраиваемые разрешения для объекта, необходимо прервать его наследование, чтобы он перестал наследовать разрешения от родительского объекта, а затем определить новые разрешения, добавив или удалив назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="2e48e-p101">SharePoint sites, lists, and list items are types of  **SecurableObject**. By default, a securable object inherits the permissions of its parent. To set custom permissions for an object, you need to break its inheritance so that it stops inheriting permissions from its parent, and then define new permissions by adding or removing role assignments.</span></span>
 
> [!Note]
> <span data-ttu-id="2e48e-107">Ссылки на статьи о детальных разрешениях см. разделе [Дополнительные ресурсы](set-custom-permissions-on-a-list-by-using-the-rest-interface.md#bk_addresources).</span><span class="sxs-lookup"><span data-stu-id="2e48e-107">See [Additional resources](set-custom-permissions-on-a-list-by-using-the-rest-interface.md#bk_addresources) for links to articles about setting fine-grained permissions.</span></span>
 
<span data-ttu-id="2e48e-p102">Пример кода в этой статье задает настраиваемые разрешения для списка, а затем меняет разрешения группы для него. В примере интерфейс REST используется в следующих целях.</span><span class="sxs-lookup"><span data-stu-id="2e48e-p102">The code example in this article sets custom permissions on a list, and then changes a group's permissions to it. The example uses the REST interface to:</span></span>
 

- <span data-ttu-id="2e48e-p103">Чтобы получить идентификатор целевой группы. Пример использует его, чтобы получить текущие привязки ролей для группы в списке и чтобы добавить новую роль в список.</span><span class="sxs-lookup"><span data-stu-id="2e48e-p103">Get the ID of the target group. The example uses the group ID to get the current role bindings for the group on the list and to add the new role to the list.</span></span>

- <span data-ttu-id="2e48e-p104">Получить идентификатор определения роли, задающего новые разрешения для группы. Этот идентификатор используется для добавления новой роли в список. Пример применяет существующее определение для новой роли, но при необходимости вы можете создать новое определение.</span><span class="sxs-lookup"><span data-stu-id="2e48e-p104">Get the ID of the role definition that defines the new permissions for the group. The ID is used to add the new role to the list. This example uses an existing role definition for the new role, but you can optionally create a new role definition.</span></span>
 
- <span data-ttu-id="2e48e-p105">Прервите наследование ролей для списка с помощью метода `BreakRoleInheritance`. В этом примере прерывается наследование ролей, но сохраняется их текущий набор. (Вы также можете не копировать назначения ролей и добавить для текущего пользователя уровень разрешений "Управление".)</span><span class="sxs-lookup"><span data-stu-id="2e48e-p105">Break role inheritance on the list by using the  `BreakRoleInheritance` method. The example breaks role inheritance but keeps the current set of roles. (Alternatively, you can choose not to copy any role assignments and to add the current user to the Manage permission level.)</span></span>
 
- <span data-ttu-id="2e48e-p106">Чтобы удалить текущее назначение ролей группы в списке, отправив запрос DELETE конечной точки назначения роли. (Если вы решили не копировать назначения ролей, пропустите этот шаг.)</span><span class="sxs-lookup"><span data-stu-id="2e48e-p106">Remove the group's current role assignment on the list by sending a DELETE request to the role assignment endpoint. (If you choose not to copy any role assignments, you would skip this step.)</span></span>
 
- <span data-ttu-id="2e48e-120">Добавьте к списку назначение роли для группы с помощью метода `AddRoleAssignment`, который привязывает группу к определению роли и добавляет роль к списку.</span><span class="sxs-lookup"><span data-stu-id="2e48e-120">Add a role assignment for the group to the list by using the  `AddRoleAssignment` method, which binds the group to the role definition and adds the role to the list.</span></span>
    
## <a name="prerequisites-for-using-the-example-in-this-article"></a><span data-ttu-id="2e48e-121">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="2e48e-121">Prerequisites for using the example in this article</span></span>
<span data-ttu-id="2e48e-122"><a name="SP15Accessdatafromremoteapp_Prereq"> </a> Для использования примеров, представленных в этой статье, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="2e48e-122"><a name="SP15Accessdatafromremoteapp_Prereq"> </a> To use the example in this article, you'll need:</span></span>

- <span data-ttu-id="2e48e-123">Среда разработки SharePoint (для локальных сценариев необходима изоляция приложений).</span><span class="sxs-lookup"><span data-stu-id="2e48e-123">A SharePoint development environment (app isolation required for on-premises scenarios)</span></span>
- <span data-ttu-id="2e48e-124">Visual Studio 2013 с Office Developer Tools или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2e48e-124">Visual Studio 2013 with Office Developer Tools or newer</span></span>
    
<span data-ttu-id="2e48e-p107">Вам также потребуется задать для надстройки разрешения **Полный доступ** в области **Интернет**. Запускать эту надстройку могут только те пользователи, у которых есть разрешения на изменение разрешений списка (например, владельцы сайта).</span><span class="sxs-lookup"><span data-stu-id="2e48e-p107">You'll also need to set  **Full Control** add-in permissions at the **Web** scope. Only users who have sufficient permissions to change list permissions (such as site owners) can run this add-in.</span></span>

## <a name="example-set-custom-permissions-on-a-list-by-using-the-rest-interface"></a><span data-ttu-id="2e48e-127">Пример: Назначение настраиваемых разрешений для списка с помощью интерфейса REST</span><span class="sxs-lookup"><span data-stu-id="2e48e-127">Example: Set custom permissions on a list by using the REST interface</span></span>
<span data-ttu-id="2e48e-128"><a name="bk_example1"> </a></span><span class="sxs-lookup"><span data-stu-id="2e48e-128"></span></span>

<span data-ttu-id="2e48e-p108">В приведенных ниже примерах представлено содержимое файла App.js в надстройке с размещением в SharePoint. В первом примере используется междоменная библиотека JavaScript для создания и отправки HTTP-запросов. Во втором примере используются запросы jQuery AJAX.</span><span class="sxs-lookup"><span data-stu-id="2e48e-p108">The following examples represent the contents of the App.js file in a SharePoint-hosted add-in. The first example uses the JavaScript cross-domain library to build and send HTTP requests. The second example uses jQuery AJAX requests.</span></span>
 
<span data-ttu-id="2e48e-p109">Прежде чем запускать код, замените заполнители фактическими значениями. Если вы используете другой язык или другую среду, вам потребуется добавить или изменить некоторые компоненты запросов. Дополнительные сведения см. в статье [Отличия между запросами REST в разных средах](complete-basic-operations-using-sharepoint-rest-endpoints.md#bk_HowRequestsDiffer).</span><span class="sxs-lookup"><span data-stu-id="2e48e-p109">Before you run the code, replace the placeholder values with actual values. If you're using a different language or environment, you'll need to add or change some request components. See  [How REST requests differ by environment](complete-basic-operations-using-sharepoint-rest-endpoints.md#bk_HowRequestsDiffer) for more information.</span></span>
 
 <span data-ttu-id="2e48e-135">**Пример 1. Запросы междоменной библиотеки**</span><span class="sxs-lookup"><span data-stu-id="2e48e-135">**Example 1: Cross-domain library requests**</span></span>
 
```javascript
'use strict';

// Change placeholder values before you run this code.
var listTitle = 'List 1';
var groupName = 'Group A';
var targetRoleDefinitionName = 'Contribute';
var appweburl;
var hostweburl;
var executor;
var groupId;
var targetRoleDefinitionId;

$(document).ready( function() {

    //Get the URI decoded URLs.
    hostweburl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
    appweburl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));

    // Load the cross-domain library file and continue to the custom code.
    var scriptbase = hostweburl + "/_layouts/15/";
    $.getScript(scriptbase + "SP.RequestExecutor.js", getTargetGroupId);
});

// Get the ID of the target group.
function getTargetGroupId() {
    executor = new SP.RequestExecutor(appweburl);
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/sitegroups/getbyname('";
    endpointUri += groupName + "')/id" + "?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            var jsonObject = JSON.parse(responseData.body);
            groupId = jsonObject.d.Id;
            getTargetRoleDefinitionId();
        },
        error: errorHandler
   });
}

// Get the ID of the role definition that defines the permissions
// you want to assign to the group.
function getTargetRoleDefinitionId() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/roledefinitions/getbyname('";
    endpointUri += targetRoleDefinitionName + "')/id" + "?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            var jsonObject = JSON.parse(responseData.body)
            targetRoleDefinitionId = jsonObject.d.Id;
            breakRoleInheritanceOfList();
        },
        error: errorHandler
    });
}

// Break role inheritance on the list.
function breakRoleInheritanceOfList() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('";
    endpointUri += listTitle + "')/breakroleinheritance(true)?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: deleteCurrentRoleForGroup,
        error: errorHandler
    });
}

// Remove the current role assignment for the group on the list.
function deleteCurrentRoleForGroup() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('";
    endpointUri += listTitle + "')/roleassignments/getbyprincipalid('" + groupId + "')?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'POST',
        headers: { 
            'X-RequestDigest':$('#__REQUESTDIGEST').val(),
            'X-HTTP-Method':'DELETE'
        },
        success: setNewPermissionsForGroup,
        error: errorHandler
    });
}

// Add the new role assignment for the group on the list.
function setNewPermissionsForGroup() {
    var endpointUri = appweburl + "/_api/SP.AppContextSite(@target)/web/lists/getbytitle('";
    endpointUri += listTitle + "')/roleassignments/addroleassignment(principalid=" + groupId;
    endpointUri += ",roledefid=" + targetRoleDefinitionId + ")?@target='" + hostweburl + "'";

    executor.executeAsync({
        url: endpointUri,
        method: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: successHandler,
        error: errorHandler
    });
}

// Get parameters from the query string.
// For production purposes you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
    var params = document.URL.split("?")[1].split("&amp;");
    for (var i = 0; i < params.length; i = i + 1) {
        var singleParam = params[i].split("=");
        if (singleParam[0] == paramToRetrieve) return singleParam[1];
    }
}

function successHandler() {
    alert('Request succeeded.');
} 

function errorHandler(xhr, ajaxOptions, thrownError) {
    alert('Request failed: ' + xhr.status + '\n' + thrownError + '\n' + xhr.responseText);
}
```

 <span data-ttu-id="2e48e-136">**Пример 2. Запросы jQuery AJAX**</span><span class="sxs-lookup"><span data-stu-id="2e48e-136">**Example 2: jQuery AJAX requests**</span></span>
 
```javascript
// Change placeholder values before you run this code.
var siteUrl = 'http://server/site';
var listTitle = 'List 1';
var groupName = 'Group A';
var targetRoleDefinitionName = 'Contribute';
var groupId;
var targetRoleDefinitionId;

$(document).ready( function() {
    getTargetGroupId();
});

// Get the ID of the target group.
function getTargetGroupId() {
    $.ajax({
        url: siteUrl + '/_api/web/sitegroups/getbyname(\'' + groupName + '\')/id',
        type: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            groupId = responseData.d.Id;
            getTargetRoleDefinitionId();
        },
        error: errorHandler
   });
}

// Get the ID of the role definition that defines the permissions
// you want to assign to the group.
function getTargetRoleDefinitionId() {
    $.ajax({
        url: siteUrl + '/_api/web/roledefinitions/getbyname(\''
            + targetRoleDefinitionName + '\')/id',
        type: 'GET',
        headers: { 'accept':'application/json;odata=verbose' },
        success: function(responseData) {
            targetRoleDefinitionId = responseData.d.Id;
            breakRoleInheritanceOfList();
        },
        error: errorHandler
    });
}

// Break role inheritance on the list.
function breakRoleInheritanceOfList() {
    $.ajax({
        url: siteUrl + '/_api/web/lists/getbytitle(\'' + listTitle
            + '\')/breakroleinheritance(true)',
        type: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: deleteCurrentRoleForGroup,
        error: errorHandler
    });
}

// Remove the current role assignment for the group on the list.
function deleteCurrentRoleForGroup() {
    $.ajax({
        url: siteUrl + '/_api/web/lists/getbytitle(\'' + listTitle
            + '\')/roleassignments/getbyprincipalid(' + groupId + ')',
        type: 'POST',
        headers: { 
            'X-RequestDigest':$('#__REQUESTDIGEST').val(),
            'X-HTTP-Method':'DELETE'
        },
        success: setNewPermissionsForGroup,
        error: errorHandler
    });
}

// Add the new role assignment for the group on the list.
function setNewPermissionsForGroup() {
    $.ajax({
        url: siteUrl + '/_api/web/lists/getbytitle(\'' + listTitle
            + '\')/roleassignments/addroleassignment(principalid='
            + groupId + ',roledefid=' + targetRoleDefinitionId + ')',
        type: 'POST',
        headers: { 'X-RequestDigest':$('#__REQUESTDIGEST').val() },
        success: successHandler,
        error: errorHandler
    });
}

function successHandler() {
    alert('Request succeeded.');
} 

function errorHandler(xhr, ajaxOptions, thrownError) {
    alert('Request failed: ' + xhr.status + '\n' + thrownError + '\n' + xhr.responseText);
}
```


## <a name="see-also"></a><span data-ttu-id="2e48e-137">См. также</span><span class="sxs-lookup"><span data-stu-id="2e48e-137">See also</span></span>
<span data-ttu-id="2e48e-138"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2e48e-138"></span></span>

-  [<span data-ttu-id="2e48e-139">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e48e-139">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md) 
-  [<span data-ttu-id="2e48e-140">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="2e48e-140">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="2e48e-141">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="2e48e-141">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)

- <span data-ttu-id="2e48e-142">Ресурсы REST:</span><span class="sxs-lookup"><span data-stu-id="2e48e-142">REST resources:</span></span>
     - [<span data-ttu-id="2e48e-143">Ресурс GroupCollection</span><span class="sxs-lookup"><span data-stu-id="2e48e-143">GroupCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_GroupCollection)
     - [<span data-ttu-id="2e48e-144">Ресурс Group</span><span class="sxs-lookup"><span data-stu-id="2e48e-144">Group resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_Group) 
     - [<span data-ttu-id="2e48e-145">Ресурс RoleAssignmentCollection</span><span class="sxs-lookup"><span data-stu-id="2e48e-145">RoleAssignmentCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignmentCollection)
     - [<span data-ttu-id="2e48e-146">Ресурс RoleAssignment</span><span class="sxs-lookup"><span data-stu-id="2e48e-146">RoleAssignment resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignment)
     - [<span data-ttu-id="2e48e-147">Ресурс RoleDefinitionCollection</span><span class="sxs-lookup"><span data-stu-id="2e48e-147">RoleDefinitionCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinitionCollection)
     - [<span data-ttu-id="2e48e-148">Ресурс RoleDefinition</span><span class="sxs-lookup"><span data-stu-id="2e48e-148">RoleDefinition resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinition)
    
 
- <span data-ttu-id="2e48e-149">Статьи TechNet:</span><span class="sxs-lookup"><span data-stu-id="2e48e-149">TechNet articles:</span></span>
     - [<span data-ttu-id="2e48e-150">Справочник по детальным разрешениям для SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="2e48e-150">Fine-grained permission reference for SharePoint Server 2013</span></span>](http://technet.microsoft.com/ru-RU/library/dn169567.aspx)
     - [<span data-ttu-id="2e48e-151">Рекомендации по использованию детальных разрешений в SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="2e48e-151">Best practices for using fine-grained permissions in SharePoint Server 2013</span></span>](http://technet.microsoft.com/ru-RU/library/gg128955.aspx)
     - [<span data-ttu-id="2e48e-152">Разрешения пользователей и уровни разрешений в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="2e48e-152">User permissions and permission levels in SharePoint 2013</span></span>](http://technet.microsoft.com/ru-RU/library/cc721640.aspx)
    
 

