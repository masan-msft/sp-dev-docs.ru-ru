# <a name="sharepoint-site-theming-powershell-cmdlets"></a><span data-ttu-id="e3d7c-101">Настройка тем для сайтов SharePoint: командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3d7c-101">SharePoint site theming: PowerShell cmdlets</span></span>

<span data-ttu-id="e3d7c-102">Администраторы клиента SharePoint могут создавать, получать и удалять темы сайтов с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-102">SharePoint tenant administrators can use PowerShell cmdlets to create, retrieve, and remove site themes.</span></span> <span data-ttu-id="e3d7c-103">Разработчики могут также использовать [REST API](sharepoint-site-theming-rest-api.md) SharePoint для управления темами.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-103">Developers can also use the SharePoint [REST API](sharepoint-site-theming-rest-api.md) to handle theme management tasks.</span></span>

<span data-ttu-id="e3d7c-104">Информацию об определении и сохранении тем см. в [справочнике по схеме JSON](sharepoint-site-theming-json-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e3d7c-104">For information about how themes are defined and stored, see [JSON schema reference](sharepoint-site-theming-json-schema.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="e3d7c-105">Начало работы</span><span class="sxs-lookup"><span data-stu-id="e3d7c-105">Getting started</span></span>

<span data-ttu-id="e3d7c-106">Чтобы управлять темами с помощью командлетов PowerShell, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e3d7c-106">To run the PowerShell cmdlets for theme management, you'll need to do the following:</span></span>

1. <span data-ttu-id="e3d7c-107">Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="e3d7c-107">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="e3d7c-108">Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-108">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
2. <span data-ttu-id="e3d7c-109">Подключитесь к клиенту SharePoint, следуя инструкциям в [этой статье]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e3d7c-109">Follow the instructions at [Connect to SharePoint Online PowerShell]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx)) to connect to your SharePoint tenant.</span></span>

<span data-ttu-id="e3d7c-110">Для проверки настройки нужно считывание параметра SPOHideDefaultThemes с помощью командлета **Get-SPOHideDefaultThemes**.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-110">To verify your setup, try using the **Get-HideDefaultThemes** cmdlet to read the HideDefaultThemes setting.</span></span> <span data-ttu-id="e3d7c-111">Если командлет вернет значение False без ошибок, как показано в следующем примере, можете продолжать.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-111">If the cmdlet runs and returns False with no errors, as shown in the following example, you're ready to proceed.</span></span>

```powershell
c:\> Get-SPOHideDefaultThemes
False
```
## <a name="site-theme-cmdlets"></a><span data-ttu-id="e3d7c-112">Командлеты для управления темами сайтов</span><span class="sxs-lookup"><span data-stu-id="e3d7c-112">Site theme cmdlets</span></span>

<span data-ttu-id="e3d7c-113">Для управления темами сайтов из PowerShell доступны следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="e3d7c-113">The following cmdlets are available for managing site themes from PowerShell:</span></span>

* <span data-ttu-id="e3d7c-114">**Add-SPOTheme** &mdash; создает новую пользовательскую тему или перезаписывает существующую;</span><span class="sxs-lookup"><span data-stu-id="e3d7c-114">**Add-SPOTheme** &mdash; Creates a new custom theme, or overwrites an existing theme to modify its settings.</span></span>
* <span data-ttu-id="e3d7c-115">**Get-SPOTheme** &mdash; получает параметры существующей темы;</span><span class="sxs-lookup"><span data-stu-id="e3d7c-115">**Get-SPOTheme** &mdash; Retrieves settings for an existing theme.</span></span>
* <span data-ttu-id="e3d7c-116">**Remove-SPOTheme** &mdash; удаляет тему из коллекции;</span><span class="sxs-lookup"><span data-stu-id="e3d7c-116">**Remove-SPOTheme** &mdash; Removes a theme from the theme gallery.</span></span>
* <span data-ttu-id="e3d7c-117">**Set-SPOHideDefaultThemes** &mdash; указывает, доступны ли стандартные темы;</span><span class="sxs-lookup"><span data-stu-id="e3d7c-117">**Set-HideDefaultThemes** &mdash; Specifies whether the default themes should be available.</span></span>
* <span data-ttu-id="e3d7c-118">**Get-SPOHideDefaultThemes** &mdash; запрашивает текущий параметр SPOHideDefaultThemes.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-118">**Get-SPOHideDefaultThemes** &mdash; Queries the current SPOHideDefaultThemes setting.</span></span>

## <a name="add-spotheme"></a><span data-ttu-id="e3d7c-119">Add-SPOTheme</span><span class="sxs-lookup"><span data-stu-id="e3d7c-119">Add-SPOTheme</span></span>

<span data-ttu-id="e3d7c-120">Командлет **Add-SPOTheme** создает новую тему или обновляет существующую.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-120">The **Add-SPOTheme** cmdlet creates a new theme or updates an existing theme.</span></span> <span data-ttu-id="e3d7c-121">Параметры цветовой палитры можно передавать в виде хэш-таблицы или словаря.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-121">The color pallette settings can be passed as either a hash table or a dictionary.</span></span>

<span data-ttu-id="e3d7c-122">В приведенном ниже примере создается тема Custom Cyan, цветовая палитра которой включает различные оттенки голубого.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-122">In the following example, a new theme named "Custom Cyan" is created, with color pallette settings that are various shades of cyan.</span></span> <span data-ttu-id="e3d7c-123">Обратите внимание на то, что параметры передаются в виде хэш-таблицы.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-123">Note that the settings are passed as a hash table.</span></span>

```powershell
$themepallette = @{
  "themePrimary" = "#00ffff";
  "themeLighterAlt" = "#f3fcfc";
  "themeLighter" = "#daffff";
  "themeLight" = "#affefe";
  "themeTertiary" = "#76ffff";
  "themeSecondary" = "#39ffff";
  "themeDarkAlt" = "#00c4c4";
  "themeDark" = "#009090";
  "themeDarker" = "#005252";
  "neutralLighterAlt" = "#f8f8f8";
  "neutralLighter" = "#f4f4f4";
  "neutralLight" = "#eaeaea";
  "neutralQuaternaryAlt" = "#dadada";
  "neutralQuaternary" = "#d0d0d0";
  "neutralTertiaryAlt" = "#c8c8c8";
  "neutralTertiary" = "#a6a6a6";
  "neutralSecondaryAlt" = "#767676";
  "neutralSecondary" = "#666666";
  "neutralPrimary" = "#333";
  "neutralPrimaryAlt" = "#3c3c3c";
  "neutralDark" = "#212121";
  "black" = "#000000";
  "white" = "#fff";
  "primaryBackground" = "#fff";
  "primaryText" = "#333"
 }

Add-SPOTheme -Name "Custom Cyan" -Palette $themepallette -IsInverted $false
```

> [!NOTE]
> <span data-ttu-id="e3d7c-124">В выпусках командной консоли SPO, предшествующих выпуску за декабрь 2017 года, параметры цветовой палитры нужно было передавать в командлет **Add-SPOTheme** в виде словаря.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-124">Prior to the December 2017 release of SPO Management Shell, the **Add-SPOTheme** cmdlet required that color pallette settings be passed as a dictionary.</span></span> <span data-ttu-id="e3d7c-125">Рекомендуем использовать последнюю версию командной консоли SPO, однако при необходимости хэш-таблицу можно преобразовать в словарь с помощью приведенной ниже функции ```HashToDictionary```.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-125">We recommend that you use the latest version of the SPO Management Shell, however the following ```HashToDictionary``` function can be used to convert a hash table to a dictionary if needed.</span></span>

```powershell
function HashToDictionary {
  Param ([Hashtable]$ht)
  $dictionary = New-Object "System.Collections.Generic.Dictionary``2[System.String,System.String]"
  foreach ($entry in $ht.GetEnumerator()) {
    $dictionary.Add($entry.Name, $entry.Value)
  }
  return $dictionary
}
```
<span data-ttu-id="e3d7c-126">Если вы хотите обновить существующую тему (например, изменить некоторые параметры цвета), используйте тот же синтаксис, что и ранее, но добавьте флажок *-Overwrite* в командлет **Add-SPOTheme**.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-126">If you want to update an existing theme (to modify some of its color settings, for example), use the same syntax as shown previously but add the *-Overwrite* flag to the **Add-SPOTheme** cmdlet.</span></span>

```powershell
Add-SPOTheme -Name "Custom Cyan" -Palette $themepallette -IsInverted $false -Overwrite
```
<span data-ttu-id="e3d7c-127">Новая тема не применяется к сайтам.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-127">Adding a theme does not apply the theme to any sites.</span></span> <span data-ttu-id="e3d7c-128">Она добавляется в хранилище клиента и список тем в разделе **Изменение оформления** для современных страниц.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-128">It adds the theme to your tenant store, and then the theme will be available in the list of themes under the **Change the look** option for modern pages.</span></span>

## <a name="get-spotheme"></a><span data-ttu-id="e3d7c-129">Get-SPOTheme</span><span class="sxs-lookup"><span data-stu-id="e3d7c-129">Get-SPOTheme</span></span>

<span data-ttu-id="e3d7c-130">Командлет **Get SPOTheme** возвращает параметры темы с указанным именем или параметры всех отправленных тем, если имя не указано.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-130">The **Get-SPOTheme** cmdlet returns the settings for a named existing theme, or for all uploaded themes if no name is provided.</span></span>

<span data-ttu-id="e3d7c-131">Приведенный ниже командлет **Get-SPOTheme** возвращает параметры темы Custom Cyan, созданной в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-131">For example, here's how to use the **Get-SPOTheme** cmdlet to return the settings for the "Custom Cyan" theme created in the previous example.</span></span>

```powershell
C:\> Get-SPOTheme -Name "Custom Cyan" | ConvertTo-Json
```
```json
{
    "Name":  "Custom Cyan",
    "Palette":  {
                    "themeLight":  "#affefe",
                    "themeTertiary":  "#76ffff",
                    "black":  "#000000",
                    "neutralSecondary":  "#666666",
                    "neutralTertiaryAlt":  "#c8c8c8",
                    "themeSecondary":  "#39ffff",
                    "themeDarker":  "#005252",
                    "primaryBackground":  "#fff",
                    "neutralQuaternary":  "#d0d0d0",
                    "neutralPrimaryAlt":  "#3c3c3c",
                    "neutralPrimary":  "#333",
                    "themeDark":  "#009090",
                    "themeLighter":  "#daffff",
                    "neutralTertiary":  "#a6a6a6",
                    "neutralQuaternaryAlt":  "#dadada",
                    "themeLighterAlt":  "#f3fcfc",
                    "white":  "#fff",
                    "neutralSecondaryAlt":  "#767676",
                    "neutralLighter":  "#f4f4f4",
                    "neutralLight":  "#eaeaea",
                    "neutralDark":  "#212121",
                    "themeDarkAlt":  "#00c4c4",
                    "neutralLighterAlt":  "#f8f8f8",
                    "primaryText":  "#333",
                    "themePrimary":  "#00ffff"
                },
    "IsInverted":  false
}
```
<span data-ttu-id="e3d7c-132">Обратите внимание на то, что в этом примере для отображения темы в формате JSON используется фильтр PowerShell _ConvertTo-Json_.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-132">Note that this example uses the PowerShell _ConvertTo-Json_ filter to display the theme in JSON format.</span></span>

<span data-ttu-id="e3d7c-133">Чтобы получить все отправленные темы, используйте команду **Get SPOTheme** без аргументов:</span><span class="sxs-lookup"><span data-stu-id="e3d7c-133">To return all uploaded themes, use the **Get-SPOTheme** command with no arguments:</span></span>

```powershell
C:\> Get-SPOTheme
```

<span data-ttu-id="e3d7c-134">Ниже показан пример данных, полученных с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-134">Here's an example of the output from this command:</span></span>

![Пример Get-SPOTheme](../../images/Get-SPOTheme-example.png)

## <a name="remove-spotheme"></a><span data-ttu-id="e3d7c-136">Remove-SPOTheme</span><span class="sxs-lookup"><span data-stu-id="e3d7c-136">Remove-SPOTheme</span></span>

<span data-ttu-id="e3d7c-137">Командлет **Remove-SPOTheme** удаляет тему из хранилища клиента.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-137">The **Remove-SPOTheme** cmdlet removes a theme from your tenant store.</span></span> <span data-ttu-id="e3d7c-138">Например, приведенный ниже командлет удаляет тему Custom Cyan, которая использовалась в предыдущих примерах.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-138">For example, this cmdlet removes the "Custom Cyan" theme that was used in the previous examples.</span></span>

```powershell
c:\> Remove-SPOTheme -Name "Custom Cyan"
```
## <a name="set-spohidedefaultthemes"></a><span data-ttu-id="e3d7c-139">Set-SPOHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="e3d7c-139">Set-SPOHideDefaultThemes</span></span>

> [!NOTE]
> <span data-ttu-id="e3d7c-140">В выпусках командной консоли SPO, предшествующих выпуску за декабрь 2017 года, этот командлет назывался ```Set-HideDefaultThemes```.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-140">This cmdlet was named ```Set-HideDefaultThemes``` until the December 2017 release of SPO Management Shell.</span></span> <span data-ttu-id="e3d7c-141">Рекомендуем использовать последнюю версию командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-141">We recommend that you use the latest version of the PowerShell cmdlets.</span></span>

<span data-ttu-id="e3d7c-142">Командлет **Set-SPOHideDefaultThemes** позволяет указать, следует ли включить в список выбора тем стандартные темы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-142">The **Set-HideDefaultThemes** cmdlet is used to specify whether the default themes that come with SharePoint should be included in the theme picker list.</span></span> <span data-ttu-id="e3d7c-143">Например, вам может потребоваться создать специальные темы для своих сайтов, а затем удалить стандартные темы, чтобы использовать на всех страницах только специальные темы.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-143">For example, you might want to create custom themes for your sites and then remove the default themes, to ensure that all pages will use your custom themes.</span></span>

<span data-ttu-id="e3d7c-144">Задайте для этого параметра значение _$true_, чтобы скрыть стандартные темы, или значение _$false_ (используется по умолчанию), чтобы разрешить использовать стандартные темы.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-144">Specify the setting as either _$true_ to hide the default themes, or _$false_ (the default setting) to allow use of the default themes.</span></span> <span data-ttu-id="e3d7c-145">Например, этот командлет скрывает стандартные темы.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-145">For example, this cmdlet hides the default themes.</span></span>

```powershell
Set-SPOHideDefaultThemes $true
```
<span data-ttu-id="e3d7c-146">Если после создания темы Custom Cyan скрыть стандартные темы, в списке тем в разделе **Изменение оформления** останется только одна специальная тема.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-146">After creating the "Custom Cyan" theme, hiding the default themes will leave only the one custom theme in the themes list under **Change the look**.</span></span>

<span data-ttu-id="e3d7c-147">Чтобы восстановить стандартные темы в списке выбора тем, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="e3d7c-147">To restore the default themes to the theme picker list, use the following cmdlet.</span></span>
```powershell
Set-SPOHideDefaultThemes $false
```

## <a name="get-spohidedefaultthemes"></a><span data-ttu-id="e3d7c-148">Get-SPOHideDefaultThemes</span><span class="sxs-lookup"><span data-stu-id="e3d7c-148">Get-SPOHideDefaultThemes</span></span>

> [!NOTE]
> <span data-ttu-id="e3d7c-149">В выпусках командной консоли SPO, предшествующих выпуску за декабрь 2017 года, этот командлет назывался ```Get-HideDefaultThemes```.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-149">this cmdlet was named ```Get-HideDefaultThemes``` until the December 2017 release of SPO Management Shell.</span></span> <span data-ttu-id="e3d7c-150">Рекомендуем использовать последнюю версию командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-150">We recommend that you use the latest version of the PowerShell cmdlets.</span></span>

<span data-ttu-id="e3d7c-151">Командлет **Get-SPOHideDefaultThemes** получает текущее значение параметра **Set-SPOHideDefaultThemes**.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-151">The **Get-HideDefaultThemes** cmdlet retrieves the currrent **Set-HideDefaultThemes** setting.</span></span> <span data-ttu-id="e3d7c-152">Этот командлет можно использовать в сценарии PowerShell для считывания параметра и выполнения действий в зависимости того, скрыты ли стандартные темы.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-152">You might want to use this cmdlet in a PowerShell script to read the setting and then take different actions based on whether the default themes are hidden.</span></span> <span data-ttu-id="e3d7c-153">Этот командлет не имеет параметров.</span><span class="sxs-lookup"><span data-stu-id="e3d7c-153">This cmdlet does not have any parameters.</span></span>

```powershell
c:\> Get-SPOHideDefaultThemes
False
```

## <a name="see-also"></a><span data-ttu-id="e3d7c-154">См. также</span><span class="sxs-lookup"><span data-stu-id="e3d7c-154">See also</span></span>

* [<span data-ttu-id="e3d7c-155">Настройка тем для сайтов SharePoint: обзор</span><span class="sxs-lookup"><span data-stu-id="e3d7c-155">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="e3d7c-156">Настройка тем для сайтов SharePoint: схема JSON</span><span class="sxs-lookup"><span data-stu-id="e3d7c-156">SharePoint site theming: JSON schema</span></span>](sharepoint-site-theming-json-schema.md)
* [<span data-ttu-id="e3d7c-157">Настройка тем для сайтов SharePoint: CSOM</span><span class="sxs-lookup"><span data-stu-id="e3d7c-157">SharePoint site theming: CSOM</span></span>](sharepoint-site-theming-csom.md)
* [<span data-ttu-id="e3d7c-158">Настройка тем для сайтов SharePoint: REST API</span><span class="sxs-lookup"><span data-stu-id="e3d7c-158">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
* [<span data-ttu-id="e3d7c-159">Командная консоль SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e3d7c-159">SharePoint Online Management Shell</span></span>](https://www.microsoft.com/en-us/download/details.aspx?id=35588)
* <span data-ttu-id="e3d7c-160">[Подключение к PowerShell в SharePoint Online]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx))</span><span class="sxs-lookup"><span data-stu-id="e3d7c-160">[Connect to SharePoint Online PowerShell]((https://technet.microsoft.com/ru-RU/library/fp161372.aspx))</span></span>
