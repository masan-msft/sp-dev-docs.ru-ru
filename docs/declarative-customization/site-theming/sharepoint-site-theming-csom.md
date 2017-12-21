# <a name="sharepoint-site-theming-csom-development"></a><span data-ttu-id="6d02e-101">Настройка тем сайтов SharePoint: разработка с использованием CSOM</span><span class="sxs-lookup"><span data-stu-id="6d02e-101">SharePoint site theming: CSOM development</span></span>

<span data-ttu-id="6d02e-102">Клиентская объектная модель (CSOM) SharePoint предоставляет доступ к объектной модели SharePoint из кода, выполняемого локально или на сервере, отличном от SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6d02e-102">The SharePoint client-side object model (CSOM) provides access to the SharePoint object model from code that is running locally or on a different server than SharePoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6d02e-103">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6d02e-103">Prerequisites</span></span>
<span data-ttu-id="6d02e-104">Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="6d02e-104">Before you get started, make sure that you're familiar with the following:</span></span>
- [<span data-ttu-id="6d02e-105">Использование клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="6d02e-105">Using the Client Object Model</span></span>](https://msdn.microsoft.com/ru-RU/library/ff798388.aspx)
- [<span data-ttu-id="6d02e-106">Общие задачи программирования</span><span class="sxs-lookup"><span data-stu-id="6d02e-106">Common Programming Tasks in the Managed Client Object Model</span></span>](https://msdn.microsoft.com/ru-RU/library/ee537013.aspx)

<span data-ttu-id="6d02e-107">Вам также потребуется добавить ссылку на пакет NuGet [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/) (версия 16.1.6906.1200 или более поздняя).</span><span class="sxs-lookup"><span data-stu-id="6d02e-107">You will also need to reference the [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/) NuGet package (version 16.1.6906.1200 or later).</span></span>

## <a name="csom-code-example"></a><span data-ttu-id="6d02e-108">Пример кода CSOM</span><span class="sxs-lookup"><span data-stu-id="6d02e-108">CSOM code example</span></span>

<span data-ttu-id="6d02e-109">В приведенном ниже примере показано, как создать объект __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ и вызвать метод __GetAllTenantThemes__, чтобы вернуть список тем.</span><span class="sxs-lookup"><span data-stu-id="6d02e-109">The following example shows how to create a __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ object and call the __GetAllTenantThemes__ method to return a list of themes.</span></span> 

> [!NOTE]
> * <span data-ttu-id="6d02e-110">URL-адрес, используемый для создания объекта контекста, включает суффикс _-admin_, так как методы **TenantAdministration** работают с сайтом администрирования.</span><span class="sxs-lookup"><span data-stu-id="6d02e-110">The URL used to create the context object includes the _-admin_ suffix, because **TenantAdministration** methods work with the admin site.</span></span>
> * <span data-ttu-id="6d02e-111">Создайте экземпляр объекта __Tenant__ с помощью [конструктора Tenant](https://msdn.microsoft.com/ru-RU/library/dn174852.aspx), а затем вызывайте методы в этом экземпляре.</span><span class="sxs-lookup"><span data-stu-id="6d02e-111">Create a __Tenant__ instance with the [Tenant constructor](https://msdn.microsoft.com/ru-RU/library/dn174852.aspx), and then call the methods on that instance.</span></span>
> * <span data-ttu-id="6d02e-112">Вы можете использовать тот же подход для вызова других методов управления темами.</span><span class="sxs-lookup"><span data-stu-id="6d02e-112">You can use the same approach to call other theme management methods.</span></span>

```C#
using System.Security;
using Microsoft.SharePoint.Client;
using Microsoft.Online.SharePoint.TenantAdministration;
using Microsoft.Online.SharePoint.TenantManagement;

...

ClientContext ctx = new ClientContext("https://mysite-admin.sharepoint.com/");
var pwd = "mypassword";
var passWord = new SecureString();
foreach (char c in pwd.ToCharArray()) passWord.AppendChar(c);
ctx.Credentials = new SharePointOnlineCredentials("admin@mydomain.com", passWord);
Tenant tenant = new Tenant(ctx);
ClientObjectList<ThemeProperties> themes = tenant.GetAllTenantThemes();
```

## <a name="theme-definition-example"></a><span data-ttu-id="6d02e-113">Пример определения темы</span><span class="sxs-lookup"><span data-stu-id="6d02e-113">Theme definition example</span></span>

<span data-ttu-id="6d02e-114">Для методов, принимающих тему в качестве аргумента, приведенный ниже код определяет класс __SPOTheme__, используемый для создания настраиваемых тем.</span><span class="sxs-lookup"><span data-stu-id="6d02e-114">For methods that take a theme argument, the following code defines an __SPOTheme__ class that you can use to create custom themes.</span></span>

```C#
/// <summary> 
/// Properties defining a theme in SharePoint Online. 
/// </summary> 
public class SPOTheme 
{ 
    /// <summary> 
    /// Specifies the name of the theme. This must uniquely identify the theme. 
    /// </summary> 
    public string Name 
    { 
        get; private set; 
    } 
    /// <summary> 
    /// Specifies the palette of colors in the theme, as a dictionary of theme slot values. 
    /// </summary> 
    public IDictionary<String, String> Palette 
    { 
        get; private set; 
    } 
    /// <summary> 
    /// Specifies whether the theme is inverted, with a dark background and a light foreground. 
    /// </summary> 
    public bool IsInverted 
    { 
        get; private set; 
    } 
} 
```

## <a name="applying-a-theme"></a><span data-ttu-id="6d02e-115">Применение темы</span><span class="sxs-lookup"><span data-stu-id="6d02e-115">Applying a theme</span></span>

<span data-ttu-id="6d02e-116">В настоящее время нет поддерживаемых API, позволяющих программным способом применить тему к определенному сайту.</span><span class="sxs-lookup"><span data-stu-id="6d02e-116">There's currently no supported API to programmatically apply a theme to specific site.</span></span>

## <a name="methodsproperties-of-the-microsoftonlinesharepointtenantadministrationtenant-class"></a><span data-ttu-id="6d02e-117">Методы и свойства класса Microsoft.Online.SharePoint.TenantAdministration.Tenant</span><span class="sxs-lookup"><span data-stu-id="6d02e-117">Methods/properties of the Microsoft.Online.SharePoint.TenantAdministration.Tenant class</span></span>

<span data-ttu-id="6d02e-118">С помощью приведенных ниже методов можно настраивать доступные темы для сайта администрирования клиента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6d02e-118">Use the following methods to customize the set of available themes for a SharePoint tenant administration site.</span></span> <span data-ttu-id="6d02e-119">Вы можете добавить новую настраиваемую тему, обновить или удалить существующую либо получить определенную тему или все темы.</span><span class="sxs-lookup"><span data-stu-id="6d02e-119">You can add a new custom theme, update an existing theme, or delete a theme, and you can retrieve a specific theme or all themes.</span></span> <span data-ttu-id="6d02e-120">Вы также можете скрывать и восстанавливать стандартные темы, входящие в состав SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6d02e-120">You can also hide or restore the default themes that come with SharePoint.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="6d02e-121">Общедоступный метод AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-121">AddTenantTheme public method</span></span>
<span data-ttu-id="6d02e-122">Добавляет тему к клиенту.</span><span class="sxs-lookup"><span data-stu-id="6d02e-122">Add a theme to the tenant.</span></span>

<span data-ttu-id="6d02e-123">__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-123">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="6d02e-124">__Параметры:__ string name, string themeJson.</span><span class="sxs-lookup"><span data-stu-id="6d02e-124">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="6d02e-125">__Тип возвращаемых данных:__ ClientResult<bool>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-125">__Return type:__ ClientResult<bool></span></span>

### <a name="deletetenanttheme-public-method"></a><span data-ttu-id="6d02e-126">Общедоступный метод DeleteTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-126">DeleteTenantTheme public method</span></span>
<span data-ttu-id="6d02e-127">Удаляет тему из клиента.</span><span class="sxs-lookup"><span data-stu-id="6d02e-127">Delete a theme from the tenant.</span></span>

<span data-ttu-id="6d02e-128">__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-128">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="6d02e-129">__Параметры:__ string name.</span><span class="sxs-lookup"><span data-stu-id="6d02e-129">__Parameters:__ string name</span></span><br/>
<span data-ttu-id="6d02e-130">__Тип возвращаемых данных:__ void.</span><span class="sxs-lookup"><span data-stu-id="6d02e-130">__Return type:__ void</span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="6d02e-131">Общедоступный метод GetAllTenantThemes</span><span class="sxs-lookup"><span data-stu-id="6d02e-131">GetAllTenantThemes public method</span></span>
<span data-ttu-id="6d02e-132">Получает все темы, доступные в клиенте на данный момент, в том числе все добавленные настраиваемые темы.</span><span class="sxs-lookup"><span data-stu-id="6d02e-132">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="6d02e-133">Стандартные темы включаются, только если свойству __HideDefaultThemes__ задано значение __false__ (оно используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="6d02e-133">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="6d02e-134">__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-134">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="6d02e-135">__Параметры:__ нет.</span><span class="sxs-lookup"><span data-stu-id="6d02e-135">__Parameters:__ none</span></span><br/>
<span data-ttu-id="6d02e-136">__Тип возвращаемых данных:__ ClientObjectList<ThemeProperties>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-136">__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="6d02e-137">Общедоступный метод GetTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-137">GetTenantTheme public method</span></span>
<span data-ttu-id="6d02e-138">Получает тему по имени.</span><span class="sxs-lookup"><span data-stu-id="6d02e-138">Retrieve a theme by name.</span></span>

<span data-ttu-id="6d02e-139">__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-139">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="6d02e-140">__Параметры:__ string name.</span><span class="sxs-lookup"><span data-stu-id="6d02e-140">__Parameters:__ string name</span></span><br/>
<span data-ttu-id="6d02e-141">__Тип возвращаемых данных:__ ThemeProperties.</span><span class="sxs-lookup"><span data-stu-id="6d02e-141">__Return type:__ ThemeProperties</span></span>

### <a name="hidedefaultthemes-public-property"></a><span data-ttu-id="6d02e-142">Общедоступное свойство HideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="6d02e-142">HideDefaultThemes public property</span></span>
<span data-ttu-id="6d02e-143">Это свойство указывает, доступны ли стандартные темы в пользовательском интерфейсе выбора тем.</span><span class="sxs-lookup"><span data-stu-id="6d02e-143">This property indicates whether the default themes are available in the theme picker UI.</span></span> <span data-ttu-id="6d02e-144">По умолчанию задано значение __false__ (стандартные темы доступны), но вы можете задать для этого свойства значение __true__ после определения настраиваемых тем, чтобы разрешить использование только определенных тем.</span><span class="sxs-lookup"><span data-stu-id="6d02e-144">The default setting is __false__ (the default themes are available), but you might want to set this property to __true__ after you define custom themes, to allow only specific themes to be used.</span></span>

<span data-ttu-id="6d02e-145">__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-145">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="6d02e-146">__Тип:__ Boolean.</span><span class="sxs-lookup"><span data-stu-id="6d02e-146">__Type:__ Boolean</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="6d02e-147">Общедоступный метод UpdateTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-147">UpdateTenantTheme public method</span></span>
<span data-ttu-id="6d02e-148">Обновляет параметры имеющейся темы.</span><span class="sxs-lookup"><span data-stu-id="6d02e-148">Update the settings for an existing theme.</span></span>

<span data-ttu-id="6d02e-149">__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-149">__Namespace:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant</span></span><br/>
<span data-ttu-id="6d02e-150">__Параметры:__ string name, string themeJson.</span><span class="sxs-lookup"><span data-stu-id="6d02e-150">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="6d02e-151">__Тип возвращаемых данных:__ ClientResult<bool>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-151">__Return type:__ ClientResult<bool></span></span>

## <a name="methods-of-the-microsoftonlinesharepointtenantmanagementtenant-class"></a><span data-ttu-id="6d02e-152">Методы класса Microsoft.Online.SharePoint.TenantManagement.Tenant</span><span class="sxs-lookup"><span data-stu-id="6d02e-152">Methods of the Microsoft.Online.SharePoint.TenantManagement.Tenant class</span></span>

<span data-ttu-id="6d02e-153">Это альтернативные API для управления темами на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="6d02e-153">These are alternative APIs to manage your themes in tenant level.</span></span>

### <a name="addtenanttheme-public-method"></a><span data-ttu-id="6d02e-154">Общедоступный метод AddTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-154">AddTenantTheme public method</span></span>
<span data-ttu-id="6d02e-155">Добавляет тему к клиенту.</span><span class="sxs-lookup"><span data-stu-id="6d02e-155">Add a theme to the tenant.</span></span>

<span data-ttu-id="6d02e-156">__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-156">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="6d02e-157">__Параметры:__ string name, string themeJson.</span><span class="sxs-lookup"><span data-stu-id="6d02e-157">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="6d02e-158">__Тип возвращаемых данных:__ ClientResult<bool>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-158">__Return type:__ ClientResult<bool></span></span>

### <a name="getalltenantthemes-public-method"></a><span data-ttu-id="6d02e-159">Общедоступный метод GetAllTenantThemes</span><span class="sxs-lookup"><span data-stu-id="6d02e-159">GetAllTenantThemes public method</span></span>
<span data-ttu-id="6d02e-160">Получает все темы, доступные в клиенте на данный момент, в том числе все добавленные настраиваемые темы.</span><span class="sxs-lookup"><span data-stu-id="6d02e-160">Retrieve all the themes that are currently available in the tenant, including any custom themes that have been added.</span></span> <span data-ttu-id="6d02e-161">Стандартные темы включаются, только если свойству __HideDefaultThemes__ задано значение __false__ (оно используется по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="6d02e-161">Default themes are only included if the __HideDefaultThemes__ property is __false__ (the default value).</span></span>

<span data-ttu-id="6d02e-162">__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-162">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="6d02e-163">__Параметры:__ нет.</span><span class="sxs-lookup"><span data-stu-id="6d02e-163">__Parameters:__ none</span></span><br/>
<span data-ttu-id="6d02e-164">__Тип возвращаемых данных:__ ClientObjectList<ThemeProperties>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-164">__Return type:__ ClientObjectList<ThemeProperties></span></span>

### <a name="gethidedefaultthemes-public-method"></a><span data-ttu-id="6d02e-165">Общедоступный метод GetHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="6d02e-165">GetHideDefaultThemes public method</span></span>
<span data-ttu-id="6d02e-166">Считывает текущее значение параметра для скрытия стандартных тем в пользовательском интерфейсе выбора темы.</span><span class="sxs-lookup"><span data-stu-id="6d02e-166">Read the current setting for whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="6d02e-167">__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-167">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="6d02e-168">__Параметры:__ нет.</span><span class="sxs-lookup"><span data-stu-id="6d02e-168">__Parameters:__ none</span></span><br/>
<span data-ttu-id="6d02e-169">__Тип возвращаемых данных:__ ClientResult<bool>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-169">__Return type:__ ClientResult<bool></span></span>

### <a name="gettenanttheme-public-method"></a><span data-ttu-id="6d02e-170">Общедоступный метод GetTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-170">GetTenantTheme public method</span></span>
<span data-ttu-id="6d02e-171">Получает тему по имени.</span><span class="sxs-lookup"><span data-stu-id="6d02e-171">Retrieve a theme by name.</span></span>

<span data-ttu-id="6d02e-172">__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-172">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="6d02e-173">__Параметры:__ string name.</span><span class="sxs-lookup"><span data-stu-id="6d02e-173">__Parameters:__ string name</span></span><br/>
<span data-ttu-id="6d02e-174">__Тип возвращаемых данных:__ ThemeProperties.</span><span class="sxs-lookup"><span data-stu-id="6d02e-174">__Return type:__ ThemeProperties</span></span>

### <a name="sethidedefaultthemes-public-method"></a><span data-ttu-id="6d02e-175">Общедоступный метод SetHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="6d02e-175">SetHideDefaultThemes public method</span></span>
<span data-ttu-id="6d02e-176">Указывает, следует ли скрывать стандартные темы в пользовательском интерфейсе выбора тем.</span><span class="sxs-lookup"><span data-stu-id="6d02e-176">Specify whether to hide default themes in the theme picker UI.</span></span>

<span data-ttu-id="6d02e-177">__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-177">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="6d02e-178">__Параметры:__ Boolean.</span><span class="sxs-lookup"><span data-stu-id="6d02e-178">__Parameters:__ Boolean</span></span><br/>
<span data-ttu-id="6d02e-179">__Тип возвращаемых данных:__ void.</span><span class="sxs-lookup"><span data-stu-id="6d02e-179">__Return type:__ void</span></span>

### <a name="updatetenanttheme-public-method"></a><span data-ttu-id="6d02e-180">Общедоступный метод UpdateTenantTheme</span><span class="sxs-lookup"><span data-stu-id="6d02e-180">UpdateTenantTheme public method</span></span>
<span data-ttu-id="6d02e-181">Обновляет параметры имеющейся темы.</span><span class="sxs-lookup"><span data-stu-id="6d02e-181">Update the settings for an existing theme.</span></span>

<span data-ttu-id="6d02e-182">__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.</span><span class="sxs-lookup"><span data-stu-id="6d02e-182">__Namespace:__ Microsoft.Online.SharePoint.TenantManagement.Tenant</span></span><br/>
<span data-ttu-id="6d02e-183">__Параметры:__ string name, string themeJson.</span><span class="sxs-lookup"><span data-stu-id="6d02e-183">__Parameters:__ string name, string themeJson</span></span><br/>
<span data-ttu-id="6d02e-184">__Тип возвращаемых данных:__ ClientResult<bool>.</span><span class="sxs-lookup"><span data-stu-id="6d02e-184">__Return type:__ ClientResult<bool></span></span>

## <a name="see-also"></a><span data-ttu-id="6d02e-185">См. также</span><span class="sxs-lookup"><span data-stu-id="6d02e-185">See also</span></span>

* [<span data-ttu-id="6d02e-186">Настройка тем для сайтов SharePoint: обзор</span><span class="sxs-lookup"><span data-stu-id="6d02e-186">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="6d02e-187">Настройка тем для сайтов SharePoint: схема JSON</span><span class="sxs-lookup"><span data-stu-id="6d02e-187">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="6d02e-188">Настройка тем для сайтов SharePoint: командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d02e-188">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="6d02e-189">Настройка тем для сайтов SharePoint: REST API</span><span class="sxs-lookup"><span data-stu-id="6d02e-189">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
* [<span data-ttu-id="6d02e-190">Использование клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="6d02e-190">Using the Client Object Model</span></span>](https://msdn.microsoft.com/ru-RU/library/ff798388.aspx)
* [<span data-ttu-id="6d02e-191">Общие задачи программирования</span><span class="sxs-lookup"><span data-stu-id="6d02e-191">Common Programming Tasks in the Managed Client Object Model</span></span>](https://msdn.microsoft.com/ru-RU/library/ee537013.aspx)
