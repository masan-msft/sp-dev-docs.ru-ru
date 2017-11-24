# <a name="sharepoint-site-theming-rest-api"></a><span data-ttu-id="83f2c-101">Настройка тем для сайтов SharePoint: REST API</span><span class="sxs-lookup"><span data-stu-id="83f2c-101">SharePoint site theming: REST API</span></span>

<span data-ttu-id="83f2c-102">С помощью интерфейса REST SharePoint можно выполнять операции CRUD (создание, чтение, обновление и удаление) с темами сайтов.</span><span class="sxs-lookup"><span data-stu-id="83f2c-102">You can use the the SharePoint REST interface to perform basic create, read, update, and delete (CRUD) operations on site themes.</span></span>

<span data-ttu-id="83f2c-103">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData $batch.</span><span class="sxs-lookup"><span data-stu-id="83f2c-103">Tip  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData   query option. For details and links to code samples, see Make batch requests with the REST APIs.</span></span> <span data-ttu-id="83f2c-104">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="83f2c-104">For details and links to code samples, see [Make batch requests with the REST APIs](https://dev.office.com/sharepoint/docs/apis/rest/make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83f2c-105">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="83f2c-105">Prerequisites</span></span>
<span data-ttu-id="83f2c-106">Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="83f2c-106">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="83f2c-107">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f2c-107">Get to know the SharePoint REST service</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/get-to-know-the-sharepoint-rest-service.md) 
- [<span data-ttu-id="83f2c-108">Выполнение базовых операций с использованием конечных точек REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f2c-108">Complete basic operations using SharePoint REST endpoints</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)

## <a name="rest-commands-for-site-themes"></a><span data-ttu-id="83f2c-109">Команды REST для тем сайтов</span><span class="sxs-lookup"><span data-stu-id="83f2c-109">REST commands for site themes</span></span>

<span data-ttu-id="83f2c-110">Для работы с темами сайтов доступны следующие команды REST:</span><span class="sxs-lookup"><span data-stu-id="83f2c-110">The following REST commands are available for working with site themes:</span></span>

* <span data-ttu-id="83f2c-111">__AddTenantTheme__ &mdash; создание темы, аналогична командлету Add-SPOTheme SharePoint;</span><span class="sxs-lookup"><span data-stu-id="83f2c-111">__AddTenantTheme__ &mdash; create a new theme; similar to the Add-SPOTheme SharePoint cmdlet</span></span>
* <span data-ttu-id="83f2c-112">__RemoveTenantTheme__ &mdash; удаление темы из хранилища тем, аналогична командлету PowerShell Remove-SPOTheme;</span><span class="sxs-lookup"><span data-stu-id="83f2c-112">__RemoveTenantTheme__ &mdash; remove a theme from the tenant store; similar to the Remove-SPOTheme PowerShell cmdlet</span></span>
* <span data-ttu-id="83f2c-113">__GetTenantThemingOptions__ &mdash; чтение параметров тем.</span><span class="sxs-lookup"><span data-stu-id="83f2c-113">__GetTenantThemingOptions__ &mdash; read theme settings</span></span>

<span data-ttu-id="83f2c-114">URL-адреса этих команд начинаются с _api/thememanager (без учета прификса),</span><span class="sxs-lookup"><span data-stu-id="83f2c-114">The URL for theme management REST commands is based on _api/thememanager.</span></span> <span data-ttu-id="83f2c-115">например:</span><span class="sxs-lookup"><span data-stu-id="83f2c-115">For example, the following are the endpoints for the commands:</span></span>

* <span data-ttu-id="83f2c-116">http://<site url>/_api/thememanager/AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="83f2c-116">http://<site url>/_api/thememanager/AddTenantTheme</span></span>
* <span data-ttu-id="83f2c-117">http://<site url>/_api/thememanager/RemoveTenantTheme</span><span class="sxs-lookup"><span data-stu-id="83f2c-117">http://<site url>/_api/thememanager/RemoveTenantTheme</span></span>
* <span data-ttu-id="83f2c-118">http://<site url>/_api/thememanager/GetTenantThemingOptions</span><span class="sxs-lookup"><span data-stu-id="83f2c-118">http://<site url>/_api/thememanager/GetTenantThemingOptions</span></span>

## <a name="addtenanttheme"></a><span data-ttu-id="83f2c-119">AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="83f2c-119">AddTenantTheme</span></span>

<span data-ttu-id="83f2c-120">Ниже показано, как добавить новую тему для клиента.</span><span class="sxs-lookup"><span data-stu-id="83f2c-120">The following JavaScript sample code shows how to add a new theme to a tenant.</span></span>

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
## <a name="removetenanttheme"></a><span data-ttu-id="83f2c-121">RemoveTenantTheme</span><span class="sxs-lookup"><span data-stu-id="83f2c-121">RemoveTenantTheme</span></span>
<span data-ttu-id="83f2c-122">Ниже показано, как удалить тему.</span><span class="sxs-lookup"><span data-stu-id="83f2c-122">The following JavaScript sample code shows how to remove a theme.</span></span>

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

## <a name="gettenantthemingoptions"></a><span data-ttu-id="83f2c-123">GetTenantThemingOptions</span><span class="sxs-lookup"><span data-stu-id="83f2c-123">GetTenantThemingOptions</span></span>
<span data-ttu-id="83f2c-124">Ниже показано, как считать параметры темы.</span><span class="sxs-lookup"><span data-stu-id="83f2c-124">The following JavaScript sample code shows how to read theme settings.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="83f2c-125">См. также</span><span class="sxs-lookup"><span data-stu-id="83f2c-125">See also</span></span>

* [<span data-ttu-id="83f2c-126">Настройка тем для сайтов SharePoint: обзор</span><span class="sxs-lookup"><span data-stu-id="83f2c-126">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="83f2c-127">Настройка тем для сайтов SharePoint: схема JSON</span><span class="sxs-lookup"><span data-stu-id="83f2c-127">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="83f2c-128">Настройка тем для сайтов SharePoint: командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="83f2c-128">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="83f2c-129">Настройка тем для сайтов SharePoint: CSOM</span><span class="sxs-lookup"><span data-stu-id="83f2c-129">SharePoint site theming: CSOM</span></span>](sharepoint-site-theming-csom.md)
* [<span data-ttu-id="83f2c-130">Выполнение базовых операций с использованием конечных точек REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="83f2c-130">Complete basic operations using SharePoint REST endpoints</span></span>](https://dev.office.com/sharepoint/docs/apis/rest/complete-basic-operations-using-sharepoint-rest-endpoints.md)
* [<span data-ttu-id="83f2c-131">Выполнение вызовов REST при помощи C# и JavaScript для SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="83f2c-131">Making REST calls with C# and JavaScript for SharePoint 2013</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&from=mscomsdc&VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)

