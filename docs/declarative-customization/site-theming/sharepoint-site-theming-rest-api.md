# <a name="sharepoint-site-theming-rest-api"></a>Настройка тем для сайтов SharePoint: REST API

С помощью интерфейса REST SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с темами сайтов.

Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch. Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis).

## <a name="prerequisites"></a>Необходимые условия
Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:
- [Знакомство со службой REST в SharePoint](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service) 
- [Выполнение базовых операций с использованием конечных точек REST SharePoint](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints)

## <a name="rest-commands-for-site-themes"></a>Команды REST для тем сайтов

Для работы с темами сайтов доступны следующие команды REST:

* __AddTenantTheme__ &mdash; создание темы, аналогична командлету Add-SPOTheme SharePoint;
* __RemoveTenantTheme__ &mdash; удаление темы из хранилища тем, аналогична командлету PowerShell Remove-SPOTheme;
* __GetTenantThemingOptions__ &mdash; чтение параметров тем.

URL-адреса этих команд начинаются с _api/thememanager (без учета прификса), например:

* http://<site url>/_api/thememanager/AddTenantTheme
* http://<site url>/_api/thememanager/RemoveTenantTheme
* http://<site url>/_api/thememanager/GetTenantThemingOptions

## <a name="addtenanttheme"></a>AddTenantTheme

Ниже показано, как добавить новую тему для клиента.

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
        {
            if (req.readyState != 4) // Loaded
                return;
            console.log(req.responseText);
        };
  req.open("POST",url,true); 
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
RestRequest("/_api/thememanager/GetTenantThemingOptions");

var pal = {
    "palette" : {
        "themePrimary": "#1BF242",
        "themeLighterAlt": "#0d0b00",
        "themeLighter": "#0b35bc",
        "themeLight": "#322d00",
        "themeTertiary": "#6a5f00",
       "themeSecondary": "#1B22F2",
        "themeDarkAlt": "#ffe817",
        "themeDark": "#ffed4b",
        "themeDarker": "#fff171",
        "neutralLighterAlt": "#252525",
        "neutralLighter": "#282828",
        "neutralLight": "#313131",
        "neutralQuaternaryAlt": "#3f3f3f",
        "neutralQuaternary": "#484848",
        "neutralTertiaryAlt": "#4f4f4f",
        "neutralTertiary": "#c8c8c8",
        "neutralSecondaryAlt": "#d0d0d0",
        "neutralSecondary": "#dadada",
        "neutralPrimary": "#ffffff",
        "neutralDark": "#eaeaea",
        "black": "#f8f8f8",
        "white": "#1f1f1f",
        "primaryBackground": "#1f1f1f",
        "primaryText": "#ffffff",
        "error": "#ff5f5f"
    }
}
RestRequest("/_api/thememanager/AddTenantTheme", {name:"Sounders Rave Green", themeJson: JSON.stringify(pal)});
```
## <a name="removetenanttheme"></a>RemoveTenantTheme
Ниже показано, как удалить тему.

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
        {
            if (req.readyState != 4) // Loaded
                return;
            console.log(req.responseText);
        };
  req.open("POST",url,true);
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
 
RestRequest("/_api/thememanager/DeleteTenantTheme", { name:"themeName.DarkYellow" });
 
RestRequest("/_api/thememanager/UpdateTenantTheme", { name:"themeName",
     themeJson:""});
```

## <a name="gettenantthemingoptions"></a>GetTenantThemingOptions
Ниже показано, как считать параметры темы.

```javascript
function RestRequest(url,params) {
  var req = new XMLHttpRequest();
  req.onreadystatechange = function ()
        {
            if (req.readyState != 4) // Loaded
                return;
            console.log(req.responseText);
        };
  req.open("POST",url,true);
  req.setRequestHeader("Content-Type", "application/json;charset=utf-8");
  req.setRequestHeader("ACCEPT", "application/json; odata.metadata=minimal");
  req.setRequestHeader("x-requestdigest", _spPageContextInfo.formDigestValue);
  req.setRequestHeader("ODATA-VERSION","4.0");
  req.send(params ? JSON.stringify(params) : void 0);
}
 
RestRequest("/_api/thememanager/GetTenantThemingOptions");
```

## <a name="see-also"></a>См. также

* [Настройка тем для сайтов SharePoint: обзор](sharepoint-site-theming-overview.md)
* [Настройка тем для сайтов SharePoint: схема JSON](sharepoint-site-theming-json-schema.md)
* [Настройка тем для сайтов SharePoint: командлеты PowerShell](sharepoint-site-theming-powershell.md)
* [Настройка тем для сайтов SharePoint: CSOM](sharepoint-site-theming-csom.md)
* [Выполнение базовых операций с использованием конечных точек REST SharePoint](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints)
* [Выполнение вызовов REST при помощи C# и JavaScript для SharePoint 2013](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&from=mscomsdc&VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)

