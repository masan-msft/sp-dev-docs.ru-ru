# <a name="sharepoint-online-tenant-properties"></a><span data-ttu-id="7efdb-101">Свойства клиента SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7efdb-101">SharePoint Online Tenant Properties</span></span>

<span data-ttu-id="7efdb-102">Свойства клиента позволяют администраторам добавлять свойства в каталог приложений для различных компонентов SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="7efdb-102">Tenant Properties allow tenant administrators to add properties in the app catalog that can be read by various SharePoint Framework components.</span></span> <span data-ttu-id="7efdb-103">Для управления свойствами клиента администраторы клиента используют [командную консоль Microsoft SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx). Это модуль PowerShell для управления подпиской SharePoint Online в Office 365.</span><span class="sxs-lookup"><span data-stu-id="7efdb-103">The Tenant Properties are managed by tenant administrators using the [Microsoft SharePoint Online Management Shell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) which is a PowerShell module to manage your SharePoint Online subscription in the Office 365.</span></span>

## <a name="manage-tenant-properties"></a><span data-ttu-id="7efdb-104">Управление свойствами клиента</span><span class="sxs-lookup"><span data-stu-id="7efdb-104">Manage tenant properties</span></span>

<span data-ttu-id="7efdb-105">С помощью командной консоли Microsoft SharePoint Online администраторы клиента могут добавлять и удалять свойства клиента через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7efdb-105">Using the Microsoft SharePoint Online Management Shell, tenant administrators can add and remove tenant properties using PowerShell.</span></span> 

> <span data-ttu-id="7efdb-106">Скачайте командную консоль Microsoft SharePoint Online [отсюда](https://www.microsoft.com/en-us/download/details.aspx?id=35588)</span><span class="sxs-lookup"><span data-stu-id="7efdb-106">Download the Microsoft SharePoint Online Management Shell [here](https://www.microsoft.com/en-us/download/details.aspx?id=35588)</span></span>

<span data-ttu-id="7efdb-107">Эти командлеты PowerShell доступны для управления свойствами клиента:</span><span class="sxs-lookup"><span data-stu-id="7efdb-107">The following PowerShell cmdlets are available to manage the tenant properties:</span></span>

<span data-ttu-id="7efdb-108">Так как свойства клиента хранятся в каталоге приложений клиента, в командлетах ниже нужно будет указать URL-адрес семейства веб-сайтов каталога приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="7efdb-108">Since tenant properties are stored in the tenant app catalog, you will need to provide the tenant app catalog site collection URL in the cmdlets below.</span></span>

### <a name="get-spostorageentity"></a><span data-ttu-id="7efdb-109">Get-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="7efdb-109">Get-SPOStorageEntity</span></span>
<span data-ttu-id="7efdb-110">Область применения: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7efdb-110">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="7efdb-111">Синтаксис Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="7efdb-111">Syntax Get-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

### <a name="set-spostorageentity"></a><span data-ttu-id="7efdb-112">Set-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="7efdb-112">Set-SPOStorageEntity</span></span>
<span data-ttu-id="7efdb-113">Область применения: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7efdb-113">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="7efdb-114">Синтаксис Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span><span class="sxs-lookup"><span data-stu-id="7efdb-114">Syntax Set-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String> [-Value] <String> [-Description] <String> [-Comments] <String></span></span>

### <a name="remove-spostorageentity"></a><span data-ttu-id="7efdb-115">Remove-SPOStorageEntity</span><span class="sxs-lookup"><span data-stu-id="7efdb-115">Remove-SPOStorageEntity</span></span>
<span data-ttu-id="7efdb-116">Область применения: Office 365, SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7efdb-116">Applies to: Office 365, SharePoint Online</span></span>

<span data-ttu-id="7efdb-117">Синтаксис Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span><span class="sxs-lookup"><span data-stu-id="7efdb-117">Syntax Remove-SPOStorageEntity [-Site] <AppCatalogSiteURL> [-Key] <String></span></span>

## <a name="reading-tenant-properties"></a><span data-ttu-id="7efdb-118">Считывание свойств клиента</span><span class="sxs-lookup"><span data-stu-id="7efdb-118">Reading tenant properties</span></span>

<span data-ttu-id="7efdb-119">Разработчики могут считывать свойства клиента с помощью интерфейсов API REST SharePoint и использовать их в компонентах SharePoint Framework, таких как веб-части и расширения.</span><span class="sxs-lookup"><span data-stu-id="7efdb-119">Developers can read tenant properties using the SharePoint REST APIs and use them in SharePoint Framework components such as web parts and extensions.</span></span>

## <a name="http-request"></a><span data-ttu-id="7efdb-120">Запрос HTTP</span><span class="sxs-lookup"><span data-stu-id="7efdb-120">HTTP request</span></span>

### <a name="get-a-tenant-property"></a><span data-ttu-id="7efdb-121">Получение свойства клиента</span><span class="sxs-lookup"><span data-stu-id="7efdb-121">Get a tenant property</span></span>

```text
GET _api/web/GetStorageEntity('key')
```

#### <a name="example"></a><span data-ttu-id="7efdb-122">Пример</span><span class="sxs-lookup"><span data-stu-id="7efdb-122">Example</span></span>

```text
GET _api/web/GetStorageEntity('AnalyticsKey')
```

#### <a name="request-body"></a><span data-ttu-id="7efdb-123">Текст запроса</span><span class="sxs-lookup"><span data-stu-id="7efdb-123">Request body</span></span>

<span data-ttu-id="7efdb-124">Не указывайте тело запроса для этого метода.</span><span class="sxs-lookup"><span data-stu-id="7efdb-124">Do not supply a request body for this method.</span></span>

#### <a name="response"></a><span data-ttu-id="7efdb-125">Отклик</span><span class="sxs-lookup"><span data-stu-id="7efdb-125">Response</span></span>

<span data-ttu-id="7efdb-126">Возвращает сведения об объекте хранилища для указанного ключа.</span><span class="sxs-lookup"><span data-stu-id="7efdb-126">This returns the storage entity information for the given key.</span></span>

```text
HTTP/1.1 200 OK
Content-Type: application/json
{
    "Comment":"Tenant property comment.",
    "Description":"Tenant property description",
    "Value":"Tenant property key value"
}
```
