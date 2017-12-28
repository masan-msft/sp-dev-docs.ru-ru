# <a name="sharepoint-site-theming-csom-development"></a>Настройка тем сайтов SharePoint: разработка с использованием CSOM

Клиентская объектная модель (CSOM) SharePoint предоставляет доступ к объектной модели SharePoint из кода, выполняемого локально или на сервере, отличном от SharePoint.    

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступить к работе, убедитесь, что вы знакомы с понятиями, описанными в следующих статьях:
- [Использование клиентской объектной модели](https://msdn.microsoft.com/ru-RU/library/ff798388.aspx)
- [Общие задачи программирования](https://msdn.microsoft.com/ru-RU/library/ee537013.aspx)

Вам также потребуется добавить ссылку на пакет NuGet [Microsoft.SharePointOnline.CSOM](https://www.nuget.org/packages/Microsoft.SharePointOnline.CSOM/) (версия 16.1.6906.1200 или более поздняя).

## <a name="csom-code-example"></a>Пример кода CSOM

В приведенном ниже примере показано, как создать объект __Microsoft.Online.SharePoint.TenantAdministration.Tenant__ и вызвать метод __GetAllTenantThemes__, чтобы вернуть список тем. 

> [!NOTE]
> * URL-адрес, используемый для создания объекта контекста, включает суффикс _-admin_, так как методы **TenantAdministration** работают с сайтом администрирования.
> * Создайте экземпляр объекта __Tenant__ с помощью [конструктора Tenant](https://msdn.microsoft.com/ru-RU/library/dn174852.aspx), а затем вызывайте методы в этом экземпляре.
> * Вы можете использовать тот же подход для вызова других методов управления темами.

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

## <a name="theme-definition-example"></a>Пример определения темы

Для методов, принимающих тему в качестве аргумента, приведенный ниже код определяет класс __SPOTheme__, используемый для создания настраиваемых тем.

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

## <a name="applying-a-theme"></a>Применение темы

В настоящее время нет поддерживаемых API, позволяющих программным способом применить тему к определенному сайту.

## <a name="methodsproperties-of-the-microsoftonlinesharepointtenantadministrationtenant-class"></a>Методы и свойства класса Microsoft.Online.SharePoint.TenantAdministration.Tenant

С помощью приведенных ниже методов можно настраивать доступные темы для сайта администрирования клиента SharePoint. Вы можете добавить новую настраиваемую тему, обновить или удалить существующую либо получить определенную тему или все темы. Вы также можете скрывать и восстанавливать стандартные темы, входящие в состав SharePoint.

### <a name="addtenanttheme-public-method"></a>Общедоступный метод AddTenantTheme
Добавляет тему к клиенту.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.<br/>
__Параметры:__ string name, string themeJson.<br/>
__Тип возвращаемых данных:__ ClientResult<bool>.

### <a name="deletetenanttheme-public-method"></a>Общедоступный метод DeleteTenantTheme
Удаляет тему из клиента.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.<br/>
__Параметры:__ string name.<br/>
__Тип возвращаемых данных:__ void.

### <a name="getalltenantthemes-public-method"></a>Общедоступный метод GetAllTenantThemes
Получает все темы, доступные в клиенте на данный момент, в том числе все добавленные настраиваемые темы. Стандартные темы включаются, только если свойству __HideDefaultThemes__ задано значение __false__ (оно используется по умолчанию).

__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.<br/>
__Параметры:__ нет.<br/>
__Тип возвращаемых данных:__ ClientObjectList<ThemeProperties>.

### <a name="gettenanttheme-public-method"></a>Общедоступный метод GetTenantTheme
Получает тему по имени.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.<br/>
__Параметры:__ string name.<br/>
__Тип возвращаемых данных:__ ThemeProperties.

### <a name="hidedefaultthemes-public-property"></a>Общедоступное свойство HideDefaultThemes
Это свойство указывает, доступны ли стандартные темы в пользовательском интерфейсе выбора тем. По умолчанию задано значение __false__ (стандартные темы доступны), но вы можете задать для этого свойства значение __true__ после определения настраиваемых тем, чтобы разрешить использование только определенных тем.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.<br/>
__Тип:__ Boolean.

### <a name="updatetenanttheme-public-method"></a>Общедоступный метод UpdateTenantTheme
Обновляет параметры имеющейся темы.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantAdministration.Tenant.<br/>
__Параметры:__ string name, string themeJson.<br/>
__Тип возвращаемых данных:__ ClientResult<bool>.

## <a name="methods-of-the-microsoftonlinesharepointtenantmanagementtenant-class"></a>Методы класса Microsoft.Online.SharePoint.TenantManagement.Tenant

Это альтернативные API для управления темами на уровне клиента.

### <a name="addtenanttheme-public-method"></a>Общедоступный метод AddTenantTheme
Добавляет тему к клиенту.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.<br/>
__Параметры:__ string name, string themeJson.<br/>
__Тип возвращаемых данных:__ ClientResult<bool>.

### <a name="getalltenantthemes-public-method"></a>Общедоступный метод GetAllTenantThemes
Получает все темы, доступные в клиенте на данный момент, в том числе все добавленные настраиваемые темы. Стандартные темы включаются, только если свойству __HideDefaultThemes__ задано значение __false__ (оно используется по умолчанию).

__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.<br/>
__Параметры:__ нет.<br/>
__Тип возвращаемых данных:__ ClientObjectList<ThemeProperties>.

### <a name="gethidedefaultthemes-public-method"></a>Общедоступный метод GetHideDefaultThemes
Считывает текущее значение параметра для скрытия стандартных тем в пользовательском интерфейсе выбора темы.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.<br/>
__Параметры:__ нет.<br/>
__Тип возвращаемых данных:__ ClientResult<bool>.

### <a name="gettenanttheme-public-method"></a>Общедоступный метод GetTenantTheme
Получает тему по имени.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.<br/>
__Параметры:__ string name.<br/>
__Тип возвращаемых данных:__ ThemeProperties.

### <a name="sethidedefaultthemes-public-method"></a>Общедоступный метод SetHideDefaultThemes
Указывает, следует ли скрывать стандартные темы в пользовательском интерфейсе выбора тем.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.<br/>
__Параметры:__ Boolean.<br/>
__Тип возвращаемых данных:__ void.

### <a name="updatetenanttheme-public-method"></a>Общедоступный метод UpdateTenantTheme
Обновляет параметры имеющейся темы.

__Пространство имен:__ Microsoft.Online.SharePoint.TenantManagement.Tenant.<br/>
__Параметры:__ string name, string themeJson.<br/>
__Тип возвращаемых данных:__ ClientResult<bool>.

## <a name="see-also"></a>См. также

* [Настройка тем для сайтов SharePoint: обзор](sharepoint-site-theming-overview.md)
* [Настройка тем для сайтов SharePoint: схема JSON](sharepoint-site-theming-json-schema.md)
* [Настройка тем для сайтов SharePoint: командлеты PowerShell](sharepoint-site-theming-powershell.md)
* [Настройка тем для сайтов SharePoint: REST API](sharepoint-site-theming-rest-api.md)
* [Использование клиентской объектной модели](https://msdn.microsoft.com/ru-RU/library/ff798388.aspx)
* [Общие задачи программирования](https://msdn.microsoft.com/ru-RU/library/ee537013.aspx)
