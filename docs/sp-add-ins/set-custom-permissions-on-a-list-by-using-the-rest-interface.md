---
title: "Назначение настраиваемых разрешений для списка с помощью интерфейса REST"
description: "Определение детальных настраиваемых разрешений для списка SharePoint с помощью интерфейса REST и JavaScript."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 241a27bcafa257be429787a5bbe0d9ff63cc1ec2
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="set-custom-permissions-on-a-list-by-using-the-rest-interface"></a>Назначение настраиваемых разрешений для списка с помощью интерфейса REST

Сайты, списки и элементы списков SharePoint представляют собой типы **SecurableObject**. По умолчанию защищаемый объект наследует разрешения от родительского объекта. Чтобы задать настраиваемые разрешения для объекта, необходимо прервать наследование его разрешений от родительского объекта, а затем определить новые разрешения, добавив или удалив назначения ролей.
 
> [!NOTE] 
> Ссылки на статьи о настройке детальных разрешений см. в разделе [См. также](#bk_addresources).
 
Пример кода в этой статье задает настраиваемые разрешения для списка, а затем меняет разрешения группы для него. В примере интерфейс REST используется в следующих целях.

- Чтобы получить идентификатор целевой группы. Пример использует его, чтобы получить текущие привязки ролей для группы в списке и чтобы добавить новую роль в список.

- Получить идентификатор определения роли, задающего новые разрешения для группы. Этот идентификатор используется для добавления новой роли в список. Пример применяет существующее определение для новой роли, но при необходимости вы можете создать новое определение.

- Прервите наследование ролей для списка с помощью метода `BreakRoleInheritance`. В этом примере прерывается наследование ролей, но сохраняется их текущий набор. (Вы также можете не копировать назначения ролей и добавить для текущего пользователя уровень разрешений "Управление".)

- Чтобы удалить текущее назначение ролей группы в списке, отправив запрос DELETE конечной точки назначения роли. (Если вы решили не копировать назначения ролей, пропустите этот шаг.)

- Добавьте к списку назначение роли для группы с помощью метода `AddRoleAssignment`, который привязывает группу к определению роли и добавляет роль к списку.

<a name="SP15Accessdatafromremoteapp_Prereq"> </a>

## <a name="prerequisites-for-using-the-example-in-this-article"></a>Необходимые условия для использования примеров в этой статье

Чтобы использовать пример из этой статьи, вам потребуется следующее:

- среда разработки SharePoint (для локальных сценариев необходима изоляция приложений);   
 
- Visual Studio 2012 или Visual Studio 2013 с Инструментами разработчика Office для Visual Studio 2012 или более поздней версии. 
 
Вам также потребуется задать разрешения **Full Control** надстройки в области **Web**. Только пользователи с достаточными разрешениями для изменения разрешений списка (например, владельцы сайта) могут запускать эту надстройку.

<a name="bk_example1"> </a>

## <a name="examples-set-custom-permissions-on-a-list-by-using-the-rest-interface"></a>Примеры: назначение настраиваемых разрешений для списка с помощью интерфейса REST

В приведенных ниже примерах представлено содержимое файла App.js в надстройке с размещением в SharePoint. В первом примере используется междоменная библиотека JavaScript для создания и отправки HTTP-запросов. Во втором примере используются запросы jQuery AJAX.

Прежде чем запускать код, замените заполнители действительными значениями. Если вы используете другой язык или другую среду, вам потребуется добавить или изменить некоторые компоненты запросов. Дополнительные сведения см. в статье [Отличия между запросами REST в разных средах](complete-basic-operations-using-sharepoint-rest-endpoints.md#bk_HowRequestsDiffer).

### <a name="example-1-cross-domain-library-requests"></a>Пример 1. Запросы междоменной библиотеки

```
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

<br/>

### <a name="example-2-jquery-ajax-requests"></a>Пример 2. Запросы jQuery AJAX

```
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

<br/>

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Знакомство со службой REST SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [Материалы по OData](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [Справочник по детальным разрешениям для SharePoint Server 2013](http://technet.microsoft.com/ru-RU/library/dn169567.aspx)
- [Рекомендации по использованию детальных разрешений в SharePoint Server 2013](http://technet.microsoft.com/ru-RU/library/gg128955.aspx)
- [Разрешения пользователей и уровни разрешений в SharePoint](http://technet.microsoft.com/ru-RU/library/cc721640.aspx)
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)    
 

