# <a name="sharepoint-online-tenant-properties"></a><span data-ttu-id="39409-101">Свойства клиента SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="39409-101">SharePoint Online Tenant Properties</span></span>

> [!NOTE]
> <span data-ttu-id="39409-102">Функция управления свойствами клиента доступна в первом выпуске в формате предварительной версии и может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="39409-102">Tenant Propeties capability is currently in preview in First Release and is subject to change.</span></span> <span data-ttu-id="39409-103">Сейчас она не поддерживается для рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="39409-103">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="39409-104">С помощью свойств клиента администраторы клиента могут добавлять свойства в каталог приложений для различных компонентов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="39409-104">Tenant Properties allow tenant administrators to add properties in the app catalog that can be read by various SharePoint Framework components.</span></span> <span data-ttu-id="39409-105">Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской SharePoint Online в Office 365.</span><span class="sxs-lookup"><span data-stu-id="39409-105">The Tenant Properties are managed by tenant administrators using the [Microsoft SharePoint Online Management Shell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) which is a PowerShell module to manage your SharePoint Online subscription in the Office 365.</span></span>

## <a name="manage-tenant-properties"></a><span data-ttu-id="39409-106">Управление свойствами клиента</span><span class="sxs-lookup"><span data-stu-id="39409-106">Manage tenant properties</span></span>

<span data-ttu-id="39409-107">С помощью командной консоли Microsoft SharePoint Online администраторы клиента могут добавлять и удалять свойства клиента через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39409-107">Using the Microsoft SharePoint Online Management Shell, tenant administrators can add and remove tenant properties using PowerShell.</span></span> 

> <span data-ttu-id="39409-108">Скачайте командную консоль Microsoft SharePoint Online [отсюда](https://www.microsoft.com/en-us/download/details.aspx?id=35588)</span><span class="sxs-lookup"><span data-stu-id="39409-108">Download the Microsoft SharePoint Online Management Shell [here](https://www.microsoft.com/en-us/download/details.aspx?id=35588)</span></span>

<span data-ttu-id="39409-109">Эти командлеты PowerShell доступны для управления свойствами клиента:</span><span class="sxs-lookup"><span data-stu-id="39409-109">The following PowerShell cmdlets are available to manage the tenant properties:</span></span>

<span data-ttu-id="39409-110">Так как свойства клиента хранятся в каталоге приложений клиента, в командлетах ниже нужно будет указать URL-адрес семейства веб-сайтов каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="39409-110">Since tenant properties are stored in the tenant app catalog, you will need to provide the tenant app catalog site collection URL in the cmdlets below.</span></span>

### <a name="get-spostorageentity"></a><span data-ttu-id="39409-111">Get-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="39409-111">Get-SPOStorageEntity</span></span>
<span data-ttu-id="39409-112">Область применения: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="39409-112">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="39409-113">Синтаксис Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="39409-113">Syntax Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

### <a name="set-spostorageentity"></a><span data-ttu-id="39409-114">Set-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="39409-114">Set-SPOStorageEntity</span></span>
<span data-ttu-id="39409-115">Область применения: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="39409-115">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="39409-116">Синтаксис Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span><span class="sxs-lookup"><span data-stu-id="39409-116">Syntax Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span></span>

### <a name="remove-spostorageentity"></a><span data-ttu-id="39409-117">Remove-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="39409-117">Remove-SPOStorageEntity</span></span>
<span data-ttu-id="39409-118">Область применения: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="39409-118">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="39409-119">Синтаксис Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="39409-119">Syntax Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

## <a name="reading-tenant-properties"></a><span data-ttu-id="39409-120">Считывание свойств клиента</span><span class="sxs-lookup"><span data-stu-id="39409-120">Reading tenant properties</span></span>

<span data-ttu-id="39409-121">Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.</span><span class="sxs-lookup"><span data-stu-id="39409-121">Developers can read tenant properties using the SharePoint REST APIs and use them in SharePoint Framework components such as web parts and extensions.</span></span>

## <a name="http-request"></a><span data-ttu-id="39409-122">Запрос HTTP</span><span class="sxs-lookup"><span data-stu-id="39409-122">HTTP request</span></span>

### <a name="get-a-tenant-property"></a><span data-ttu-id="39409-123">Получение свойства клиента</span><span class="sxs-lookup"><span data-stu-id="39409-123">Get a tenant property</span></span>

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a><span data-ttu-id="39409-124">Пример</span><span class="sxs-lookup"><span data-stu-id="39409-124">Example</span></span>

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a><span data-ttu-id="39409-125">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="39409-125">Request body</span></span>

<span data-ttu-id="39409-126">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="39409-126">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="39409-127">Отклик</span><span class="sxs-lookup"><span data-stu-id="39409-127">Response</span></span>

<span data-ttu-id="39409-128">Возвращает сведения об объекте хранилища для указанного ключа.</span><span class="sxs-lookup"><span data-stu-id="39409-128">This returns the storage entity information for the given key.</span></span>

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```
