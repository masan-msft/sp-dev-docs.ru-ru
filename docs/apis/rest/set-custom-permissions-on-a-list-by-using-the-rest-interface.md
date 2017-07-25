<span data-ttu-id="82712-p109">Прежде чем запускать код, замените заполнители фактическими значениями. Если вы используете другой язык или другую среду, вам потребуется добавить или изменить некоторые компоненты запросов. Дополнительные сведения см. в статье [Отличия между запросами REST в разных средах](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer).</span><span class="sxs-lookup"><span data-stu-id="82712-p109">Before you run the code, replace the placeholder values with actual values. If you're using a different language or environment, you'll need to add or change some request components. See  [How REST requests differ by environment](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer) for more information.</span></span>
 
Прежде чем запускать код, замените заполнители фактическими значениями. Если вы используете другой язык или другую среду, вам потребуется добавить или изменить некоторые компоненты запросов. Дополнительные сведения см. в статье [Отличия между запросами REST в разных средах](complete-basic-operations-using-sharepoint-2013-rest-endpoints.md#bk_HowRequestsDiffer).
 
 <span data-ttu-id="82712-134">**Пример 1. Запросы междоменной библиотеки**</span><span class="sxs-lookup"><span data-stu-id="82712-134">**Example 1: Cross-domain library requests**</span></span>
 
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

 <span data-ttu-id="82712-135">**Пример 2. Запросы jQuery AJAX**</span><span class="sxs-lookup"><span data-stu-id="82712-135">**Example 2: jQuery AJAX requests**</span></span>
 
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


## <a name="additional-resources"></a><span data-ttu-id="82712-136">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="82712-136">Additional resources</span></span>
<span data-ttu-id="82712-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="82712-137"></span></span>

-  [<span data-ttu-id="82712-138">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="82712-138">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md) 
-  [<span data-ttu-id="82712-139">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="82712-139">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [<span data-ttu-id="82712-140">Работа со списками и элементами списков в интерфейсе REST</span><span class="sxs-lookup"><span data-stu-id="82712-140">Working with lists and list items with REST</span></span>](working-with-lists-and-list-items-with-rest.md)

- <span data-ttu-id="82712-141">Ресурсы REST:</span><span class="sxs-lookup"><span data-stu-id="82712-141">REST resources:</span></span>
     - [<span data-ttu-id="82712-142">Ресурс GroupCollection</span><span class="sxs-lookup"><span data-stu-id="82712-142">GroupCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_GroupCollection)
     - [<span data-ttu-id="82712-143">Ресурс Group</span><span class="sxs-lookup"><span data-stu-id="82712-143">Group resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_Group) 
     - [<span data-ttu-id="82712-144">Ресурс RoleAssignmentCollection</span><span class="sxs-lookup"><span data-stu-id="82712-144">RoleAssignmentCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignmentCollection)
     - [<span data-ttu-id="82712-145">Ресурс RoleAssignment</span><span class="sxs-lookup"><span data-stu-id="82712-145">RoleAssignment resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleAssignment)
     - [<span data-ttu-id="82712-146">Ресурс RoleDefinitionCollection</span><span class="sxs-lookup"><span data-stu-id="82712-146">RoleDefinitionCollection resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinitionCollection)
     - [<span data-ttu-id="82712-147">Ресурс RoleDefinition</span><span class="sxs-lookup"><span data-stu-id="82712-147">RoleDefinition resource</span></span>](http://msdn.microsoft.com/library/c5e49290-78d4-4167-b4de-da32376bbf90%28Office.15%29.aspx#bk_RoleDefinition)
    
 
- <span data-ttu-id="82712-148">Статьи TechNet:</span><span class="sxs-lookup"><span data-stu-id="82712-148">TechNet articles:</span></span>
     - [<span data-ttu-id="82712-149">Справочник по детальным разрешениям для SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="82712-149">Fine-grained permission reference for SharePoint Server 2013</span></span>](http://technet.microsoft.com/en-us/library/dn169567.aspx)
     - [<span data-ttu-id="82712-150">Рекомендации по использованию детальных разрешений в SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="82712-150">Best practices for using fine-grained permissions in SharePoint Server 2013</span></span>](http://technet.microsoft.com/en-us/library/gg128955.aspx)
     - [<span data-ttu-id="82712-151">Разрешения пользователей и уровни разрешений в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="82712-151">User permissions and permission levels in SharePoint 2013</span></span>](http://technet.microsoft.com/en-us/library/cc721640.aspx)
    
 

