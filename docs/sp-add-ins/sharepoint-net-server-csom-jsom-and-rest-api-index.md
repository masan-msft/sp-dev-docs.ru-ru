
# <a name="sharepoint-net-server-csom-jsom-and-rest-api-index"></a>Сервер .NET, CSOM, JSOM и индекс REST API для SharePoint

 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 


## <a name="sharepoint-api-index"></a>Индекс API SharePoint

Используйте индекс API для поиска наиболее часто используемых типов и объектов, реализованных в серверной объектной модели .NET и, по крайней мере, в одной клиентской модели программирования: клиентская объектная модель .NET, объектная модель JavaScript и REST.
 

 
В таблице 1 приведены наиболее часто используемые основные API, которые в большинстве случаев основаны на типах реализации сервера .NET. В некоторых случаях типы являются уникальными для клиентской модели SharePoint без эквивалентного типа серверной модели .NET. Для некоторых типов существуют клиентские реализации модели программирования определенного типа.
 

 
 *Табл. 1. Часто используемые основные API* 
 

||||
|:-----|:-----|:-----|
|**API**|**SP.Object/Enumeration (sp.js)**|**Конечная точка REST**|
|**AttachmentCollection** **SPAttachmentCollection**| [SP.AttachmentCollection](http://msdn.microsoft.com/library/28247ba7-eeaf-e1fc-0609-fb4c39b5d53c%28Office.15%29.aspx)| `…/_api/web/lists('<list id>')/items(<item id>)/attachmentfiles`|
|**BasePermissions** **SPBasePermissions**| [Объект SP.BasePermissions](http://msdn.microsoft.com/library/40349d51-1068-08c6-8ba4-b23ee58396c4%28Office.15%29.aspx)|Н/Д|
|**CalendarType** **SPCalendarType**| [Перечисление SP.CalendarType](http://msdn.microsoft.com/library/33242ef7-1300-b534-6e8e-c5df1a3df85b%28Office.15%29.aspx)|Н/Д|
|**ChangeCollection** **SPChangeCollection**| [Объект SP.ChangeCollection](http://msdn.microsoft.com/library/528b8776-f295-77ff-5403-a3556b4f3081%28Office.15%29.aspx)| `…/_api/web/getchanges(changequery)`|
|**ChangeSite** **SPChangeSite**| [Перечисление SP.ChangeSite](http://msdn.microsoft.com/library/fab86803-f106-97d0-6e97-696c91f210cd%28Office.15%29.aspx)|Н/Д|
|**ClientContext**| [Объект SP.ClientContext](http://msdn.microsoft.com/library/662619d3-60b9-92a8-5da7-b481c9b73c79%28Office.15%29.aspx)| `…/_api/contextinfo`|
|**ContentType** **SPContentType**| [Объект SP.ContentType](http://msdn.microsoft.com/library/5418f5ad-8a47-3bf7-a8ac-99b10ba04294%28Office.15%29.aspx)| `…/_api/web/contenttypes('<content type id>')`|
|**ContentTypeCollection** **SPContentTypeCollection**| [Объект SP.ContentTypeCollection](http://msdn.microsoft.com/library/e89cc14d-40ea-5e7a-c3db-efe7e6697445%28Office.15%29.aspx)| `…/_api/web/contenttypes`|
|**SPContext**| [Объект SP.RequestContext](http://msdn.microsoft.com/library/7bf846f5-e049-ca89-14b7-cf9fed8a82f1%28Office.15%29.aspx)|Н/Д|
|**EventReceiverDefinition** **SPEventReceiverDefinition**| [Объект SP.EventReceiverDefinition](http://msdn.microsoft.com/library/7d78e562-fb0e-2e87-aa47-022aa0c5848c%28Office.15%29.aspx)| `…/_api/web/eventreceivers`|
|**EventReceiverDefinitionCollection** **SPEventReceiverDefinitionCollection**| [Объект SP.EventReceiverDefinitionCollection](http://msdn.microsoft.com/library/1a495e76-00ab-4e20-e824-c3612458448d%28Office.15%29.aspx)| `…/_api/web/eventreceivers(eventreceiverid)`|
|**EventReceiverDefinitionCreationInformation** **SPEventReceiverDefinitionCreationInformation**| [Объект SP.EventReceiverDefinitionCreationInformation](http://msdn.microsoft.com/library/38382946-d098-b658-306f-019ee4d0e15e%28Office.15%29.aspx)|Н/Д|
|**EventReceiverType** **SPEventReceiverType**| [Перечисление SP.EventReceiverType](http://msdn.microsoft.com/library/8b4db240-9814-052c-fb67-1e840b610969%28Office.15%29.aspx)|Н/Д|
|**Feature** **SPFeature**| [Объект SP.Feature](http://msdn.microsoft.com/library/e998df87-9250-17d1-737d-a37092f36ec8%28Office.15%29.aspx)| `…/_api/web/features(featureid)`|
|**FeatureCollection** **SPFeatureCollection**| [Объект SP.FeatureCollection](http://msdn.microsoft.com/library/ab02330d-3102-8342-5641-a9a4f6a48772%28Office.15%29.aspx)| `…/_api/web/features`|
|**FeatureDefinitionScope** **SPFeatureDefinitionScope**| [Перечисление SP.FeatureDefinitionScope](http://msdn.microsoft.com/library/574f7613-5707-d0ad-dc72-02d639a299ff%28Office.15%29.aspx)|Н/Д|
|**Field** **SPField**| [Объект SP.Field](http://msdn.microsoft.com/library/d1e50cda-8d5e-47aa-8c78-23b1707dca04%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_Field)|
|**FieldCalculated** **SPFieldCalculated**| [Объект SP.FieldCalculated](http://msdn.microsoft.com/library/40a5b764-f1be-482b-7779-88e9bbb3f70a%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldCalculated)|
|**FieldChoice** **SPFieldChoice**| [Объект SP.FieldChoice](http://msdn.microsoft.com/library/4521054f-8b98-892a-1e4f-016684e2872f%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldMultiChoice)|
|**FieldCollection** **SPFieldCollection**| [Объект SP.FieldCollection](http://msdn.microsoft.com/library/db532e07-a4e8-d2f8-4ac8-c14de4adc761%28Office.15%29.aspx)| […/_api/web/fields](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldCollection)|
|**FieldComputed** **SPFieldComputed**| [Объект SP.FieldComputed](http://msdn.microsoft.com/library/c00fcb21-1aab-6aff-cc9c-a7b1c9cd70f6%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldComputed)|
|**FieldCurrency** **SPFieldCurrency**| [Объект SP.FieldCurrency](http://msdn.microsoft.com/library/aef1c982-fb34-3c5c-a6dc-659fd16b32e7%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldNumber)|
|**FieldLink** **SPFieldLink**| [Объект SP.FieldLink](http://msdn.microsoft.com/library/5dc71a19-3260-20fa-73ed-3de3cde37825%28Office.15%29.aspx)| `…/_api/web/contenttypes('<content type id>')/fieldlinks('<field link id>')`|
|**FieldLookupValue** **SPFieldLookupValue**| [Объект SP.FieldLookup](http://msdn.microsoft.com/library/275b256e-1192-75f5-b604-ec002448be02%28Office.15%29.aspx)|Н/Д|
|**FieldMultiChoice** **SPFieldMultiChoice**| [Объект SP.FieldMultiChoice](http://msdn.microsoft.com/library/a9546014-715a-ed57-993f-bbe237f92880%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldMultiChoice)|
|**FieldMultiLineText** **SPFieldMultiLineText**| [Объект SP.FieldMultiLineText](http://msdn.microsoft.com/library/52d130f2-6858-3aa1-88ce-d5b73eccd150%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldMultiLineText)|
|**FieldNumber** **SPFieldNumber**| [Объект SP.FieldNumber](http://msdn.microsoft.com/library/1c3d179f-21a7-66cc-ea16-3341ea50f395%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldNumber)|
|**FieldText** **SPFieldText**| [Объект SP.FieldText](http://msdn.microsoft.com/library/ba9a623c-b387-862d-eb1b-eb9d7fd9e04e%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldText)|
|**FieldUrl** **SPFieldUrl**| [Объект SP.FieldUrl](http://msdn.microsoft.com/library/4eeff596-fa18-d21e-8cc0-fd8463fb5351%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldUrl)|
|**FieldUrlValue** **SPFieldUrlValue**| [Объект SP.FieldUrlValue](http://msdn.microsoft.com/library/3866f4a6-8fda-586a-ecdc-0c7e7d7ad44b%28Office.15%29.aspx)|Н/Д|
|**FieldUser** **SPFieldUser**| [Объект SP.FieldUser](http://msdn.microsoft.com/library/9058425f-b35a-b8a3-d5d1-b2abdbf08576%28Office.15%29.aspx)| […/_api/web/fields('<field id>')](http://msdn.microsoft.com/library/fields-rest-api-reference%28Office.15%29.aspx#bk_FieldLookup)|
|**File** **SPFile**| [Объект SP.File](http://msdn.microsoft.com/library/860609d0-d317-41ca-9164-159e522d07cb%28Office.15%29.aspx)| […/_api/web/getfilebyserverrelativeurl('/<folder name>/<file name>')](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx#bk_File)|
|**FileCollection** **SPFileCollection**| [Объект SP.FieldCollection](http://msdn.microsoft.com/library/db532e07-a4e8-d2f8-4ac8-c14de4adc761%28Office.15%29.aspx)| […/_api/web/getfolderbyserverrelativeurl('/<folder name>')/files](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx#bk_FileCollection)|
|**Folder** **SPFolder**| [Объект SP.Folder](http://msdn.microsoft.com/library/60117e9d-6e9c-8aa9-be9f-a287bc1f547f%28Office.15%29.aspx)| […/_api/web/getfolderbyserverrelativeurl('/<folder name>')](http://msdn.microsoft.com/library/files-and-folders-rest-api-reference%28Office.15%29.aspx#bk_Folder)|
|**Form** **SPForm**| [Объект SP.Form](http://msdn.microsoft.com/library/8d5429c4-c218-a17e-51ee-1d34914d5550%28Office.15%29.aspx)| `…/_api/web/lists(guid'<list id>')/forms('<form id>')`|
|**Group** **SPGroup**| [Объект SP.Group](http://msdn.microsoft.com/library/763a2172-1d66-cf41-4121-d26902e6f42a%28Office.15%29.aspx)| […/_api/web/sitegroups(<group id>)](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_Group)|
|**GroupCollection** **SPGroupCollection**| [Объект SP.GroupCollection](http://msdn.microsoft.com/library/c20fa978-7e6c-e9f6-b169-852872b982e6%28Office.15%29.aspx)| […/_api/web/sitegroups](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_GroupCollection)|
|**Language** **SPLanguage**| [Объект SP.Language](http://msdn.microsoft.com/library/072936e7-a23f-f4ea-9c6d-c484b3ba1d25%28Office.15%29.aspx)|Н/Д|
|**List** **SPList**| [Объект SP.List](http://msdn.microsoft.com/library/6d4b1a5d-0600-87d3-757d-360679d937dc%28Office.15%29.aspx)| […/_api/web/lists(guid'<list id>')](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_List)|
|**ListCollection** **SPListCollection**| [Объект SP.ListCollection](http://msdn.microsoft.com/library/abc4fe81-3b0f-dffb-dba5-638c3f58268a%28Office.15%29.aspx)| […/_api/web/lists](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_ListCollection)|
|**ListDataSource** **SPListDataSource**| [Объект SP.ListDataSource](http://msdn.microsoft.com/library/099059ae-2261-e3f5-d8f2-7dbcbadeff21%28Office.15%29.aspx)|Н/Д|
|**ListItem** **SPListItem**| [Объект SP.ListItem](http://msdn.microsoft.com/library/3ea127c9-6cba-fe11-2193-ff2dc5c02fbf%28Office.15%29.aspx)| […/_api/web/lists(guid'<list id>')/items(<item id>)](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_ListItem)|
|**ListItemCollection** **SPListItemCollection**| [Объект SP.ListItemCollection](http://msdn.microsoft.com/library/05107bcd-32d5-b2a5-05d2-12152441c1fc%28Office.15%29.aspx)| […/_api/web/lists(guid'<list id>')/items](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_ListItemCollection)|
|**ListTemplateType** **SPListTemplateType**| [Объект SP.ListTemplateType](http://msdn.microsoft.com/library/1ccbd999-9415-8449-6b38-aadb9549f384%28Office.15%29.aspx)|Н/Д|
|**Navigation** **SPNavigation**| [Объект SP.Navigation](http://msdn.microsoft.com/library/22777706-0bf1-ae70-0d99-529e643a2f31%28Office.15%29.aspx)| `…/_api/web/navigation`|
|**NavigationNode** **SPNavigationNode**| [Объект SP.NavigationNode](http://msdn.microsoft.com/library/ec8a4fe0-6996-dba3-f565-4333c5046311%28Office.15%29.aspx)|Н/Д|
|**Principal** **SPPrincipal**| [Объект SP.Principal](http://msdn.microsoft.com/library/2d89b994-f692-7b2c-0cd0-be586586d70a%28Office.15%29.aspx)|Н/Д|
|**SPQuery**||Н/Д|
|**RecycleBinItem** **SPRecycleBinItem**| [Объект SP.RecycleBinItem](http://msdn.microsoft.com/library/4109c8f7-2dbe-95db-a0b2-064da24f4ed9%28Office.15%29.aspx)| `…/_api/web/RecycleBin(recyclebinitemid)`|
|**RecycleBinItemCollection** **SPRecycleBinItemCollection**| [Объект SP.RecycleBinItemCollection](http://msdn.microsoft.com/library/e182d87a-b0be-dc3e-ba9e-69f9148e9366%28Office.15%29.aspx)| `…/_api/web/RecycleBin`|
|**RegionalSettings** **SPRegionalSettings**| [Объект SP.RegionalSettings](http://msdn.microsoft.com/library/fcf7b8c8-c595-8646-6d60-7ae27084848d%28Office.15%29.aspx)| `…/_api/web/RegionalSettings`|
|**RoleAssignment** **SPRoleAssignment**| [Объект SP.RoleAssignment](http://msdn.microsoft.com/library/5dd76bb3-c0a0-a3b8-8263-723fe3d542f8%28Office.15%29.aspx)| […/_api/web/roleassignments(<principal id>)](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_RoleAssignment)|
|**RoleAssignmentCollection** **SPRoleAssignmentCollection**| [Объект SP.RoleAssignmentCollection](http://msdn.microsoft.com/library/ec84c668-9eca-45e8-40ae-8d9ac283d3b1%28Office.15%29.aspx)| […/_api/web/roleassignments](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_RoleAssignmentCollection)|
|**RoleDefinition** **SPRoleDefinition**| [Объект SP.RoleDefinition](http://msdn.microsoft.com/library/a7871c97-07d9-b63f-bdb8-6812adb82be8%28Office.15%29.aspx)| […/_api/web/roledefinitions(<role definition id>)](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_RoleDefinition)|
|**RoleType** **SPRoleType**| [Перечисление SP.RoleType](http://msdn.microsoft.com/library/c2c0149f-6b90-9cd5-73d8-5ee3ab9c2ca9%28Office.15%29.aspx)|Н/Д|
|**SecurableObject** **SPSecurableObject**| [Объект SP.SecurableObject](http://msdn.microsoft.com/library/6b9c310e-2a80-9bff-540b-28d54b37c841%28Office.15%29.aspx)|Н/Д|
|**Site** **SPSite**| [Объект SP.Site](http://msdn.microsoft.com/library/d3169eb6-882f-180a-2159-34301f66746a%28Office.15%29.aspx)| `…/_api/site`|
|**TimeZone** **SPTimeZone**| [Объект SP.TimeZone](http://msdn.microsoft.com/library/5bef51e2-c86c-1821-0462-0749e77f9be3%28Office.15%29.aspx)| `…/_api/web/RegionalSettings/TimeZones(timzoneid)`|
|**TimeZoneCollection** **SPTimeZoneCollection**| [Объект SP.TimeZoneCollection](http://msdn.microsoft.com/library/95b45caa-c88f-2f53-c99e-738859d7bb93%28Office.15%29.aspx)| `…/_api/web/RegionalSettings/TimeZones`|
|**User** **SPUser**| [Объект SP.User](http://msdn.microsoft.com/library/d36be210-3c1d-c589-e703-1ad66156dc18%28Office.15%29.aspx)| […/_api/web/siteusers(@v)?@v='<login name>'](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_User)|
|**UserCollection** **SPUserCollection**| [Объект SP.UserCollection](http://msdn.microsoft.com/library/1bb7bd28-4f19-a8a7-762f-3887c2b8ef7d%28Office.15%29.aspx)| […/_api/web/sitegroups(<group id>)/users](http://msdn.microsoft.com/library/users-groups-and-roles-rest-api-reference%28Office.15%29.aspx#bk_UserCollection)|
|**Utility** **SPUtility**| [Объект SP.Utilities.Utility (sp.js)](http://msdn.microsoft.com/library/57148667-64ff-7fed-8665-03226e70a96b%28Office.15%29.aspx)|Н/Д|
|**View** **SPView**| [Объект SP.View (sp.js)](http://msdn.microsoft.com/library/7b97ecb8-47cc-5c76-231f-81fa4ccae30a%28Office.15%29.aspx)| […/_api/web/lists(guid'<list id>')/views('<view id>')](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_View)|
|**ViewCollection** **SPViewCollection**| [Объект SP.ViewCollection](http://msdn.microsoft.com/library/3b0214c7-17b3-152c-78fa-a7a01e8b679a%28Office.15%29.aspx)| […/_api/web/lists(guid'<list id>')/views](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_ViewCollection)|
|**ViewFieldCollection** **SPViewFieldCollection**| [Объект SP.ViewFieldCollection](http://msdn.microsoft.com/library/05cab807-0609-5881-4119-bea2623eb01d%28Office.15%29.aspx)| […/_api/web/lists(guid'<list id>')/views('<view id>')/fields](http://msdn.microsoft.com/library/lists-and-list-items-rest-api-reference%28Office.15%29.aspx#bk_ViewFieldCollection)|
|**Web** **SPWeb**| [Объект SP.Web](http://msdn.microsoft.com/library/3685fd38-a11d-f07c-c042-13efc6473ba5%28Office.15%29.aspx)| […/_api/web](http://msdn.microsoft.com/library/webs-rest-api-reference%28Office.15%29.aspx#bk_Web)|
|**WebCollection** **SPWebCollection**| [Объект SP.WebCollection](http://msdn.microsoft.com/library/fa790853-9ced-0e79-4ce4-9228c336d770%28Office.15%29.aspx)| […/_api/web/webs](http://msdn.microsoft.com/library/webs-rest-api-reference%28Office.15%29.aspx#bk_WebCollection)|
|**WebInformation** **SPWebInfo**| [Объект SP.WebInformation](http://msdn.microsoft.com/library/006ca57d-50c2-9605-c4ef-fee212aacd54%28Office.15%29.aspx)| `…/_api/web/webinfos('<web information id>')`|
|**WebTemplate** **SPWebTemplate**| [Объект SP.WebTemplate](http://msdn.microsoft.com/library/cd670582-20a3-30b7-20f5-758be6d838da%28Office.15%29.aspx)| `…/_api/web/GetAvailableWebTemplates(languageid,includecrosslanguage)/getbyname(templatename)`|
|**WebTemplateCollection** **SPWebTemplateCollection**| [Объект SP.WebTemplateCollection](http://msdn.microsoft.com/library/c6e8b2c8-4f0f-bfda-2626-49c59ef92844%28Office.15%29.aspx)| `…/_api/web/GetAvailableWebTemplates(languageid,includecrosslanguage)`|

 **Примечание.** Перед использованием URI конечной точки REST, указанного в таблице, замените сокращение `…` на путь к вашему сайту SharePoint, например `http://<site collection>/<site>/_api/web/lists`.
 


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint](complete-basic-operations-using-sharepoint-2013-client-library-code)
    
 
-  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 
-  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint-2013)
    
 

