# <a name="sharepoint-site-theming-json-schema"></a><span data-ttu-id="ac3f4-101">Настройка тем для сайтов SharePoint: схема JSON</span><span class="sxs-lookup"><span data-stu-id="ac3f4-101">SharePoint site theming: JSON schema</span></span>

<span data-ttu-id="ac3f4-102">В случае новых функций, позволяющих [настроить темы сайтов SharePoint](sharepoint-site-theming-overview.md), используется схема JSON для хранения параметров цветов и других сведений о каждой теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-102">The new [SharePoint site theming](sharepoint-site-theming-overview.md) features use a JSON schema to store color settings and other information about each theme.</span></span> <span data-ttu-id="ac3f4-103">Параметры темы хранятся в объекте JSON, содержащем перечисленные ниже ключи.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-103">Theme settings are stored in a JSON object that contains the following keys:</span></span>

* <span data-ttu-id="ac3f4-104">__name__ &mdash; имя темы, которое отображается в пользовательском интерфейсе для выбора тем, а также используется администраторами и разработчиками для обращения к теме в командлетах PowerShell или при вызовах REST API для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-104">__name__ &mdash; The name of the theme, which appears in the theme picker UI and is also used by administrators and developers to refer to the theme in PowerShell cmdlets or calls to the SharePoint REST API.</span></span>
* <span data-ttu-id="ac3f4-105">__isInverted__ &mdash; ключ, у которого должно быть значение false для светлых тем и значение true для темных. Указывает, какие цвета темы SharePoint будет использовать для отрисовки текста на цветном фоне (темные или светлые).</span><span class="sxs-lookup"><span data-stu-id="ac3f4-105">__isInverted__ &mdash; This value should be false for light themes and true for dark themes; it controls whether SharePoint will use dark or light theme colors to render text on colored backgrounds.</span></span>
* <span data-ttu-id="ac3f4-106">__backgroundImageUril__ &mdash; универсальный код ресурса (URI) необязательного фонового изображения темы (значение может быть пустым, если фоновое изображение отсутствует).</span><span class="sxs-lookup"><span data-stu-id="ac3f4-106">__backgroundImageUril__ &mdash; The URI of an optional background image for the theme (value can be blank if no background image).</span></span>
* <span data-ttu-id="ac3f4-107">__theme__ &mdash; параметры цветов темы в формате RGB, хранящиеся в виде вложенного объекта JSON со следующими ключами:</span><span class="sxs-lookup"><span data-stu-id="ac3f4-107">__theme__ &mdash; The RGB color settings for the theme, stored as a nested JSON object with the following keys:</span></span>
    * <span data-ttu-id="ac3f4-108">themePrimary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-108">themePrimary</span></span>
    * <span data-ttu-id="ac3f4-109">themeLighterAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-109">themeLighterAlt</span></span>
    * <span data-ttu-id="ac3f4-110">themeLighter</span><span class="sxs-lookup"><span data-stu-id="ac3f4-110">themeLighter</span></span>
    * <span data-ttu-id="ac3f4-111">themeLight</span><span class="sxs-lookup"><span data-stu-id="ac3f4-111">themeLight</span></span>
    * <span data-ttu-id="ac3f4-112">themeTertiary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-112">themeTertiary</span></span>
    * <span data-ttu-id="ac3f4-113">themeSecondary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-113">themeSecondary</span></span>
    * <span data-ttu-id="ac3f4-114">themeDarkAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-114">themeDarkAlt</span></span>
    * <span data-ttu-id="ac3f4-115">themeDark</span><span class="sxs-lookup"><span data-stu-id="ac3f4-115">themeDark</span></span>
    * <span data-ttu-id="ac3f4-116">themeDarker</span><span class="sxs-lookup"><span data-stu-id="ac3f4-116">themeDarker</span></span>
    * <span data-ttu-id="ac3f4-117">neutralLighterAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-117">neutralLighterAlt</span></span>
    * <span data-ttu-id="ac3f4-118">neutralLighter</span><span class="sxs-lookup"><span data-stu-id="ac3f4-118">neutralLighter</span></span>
    * <span data-ttu-id="ac3f4-119">neutralLight</span><span class="sxs-lookup"><span data-stu-id="ac3f4-119">neutralLight</span></span>
    * <span data-ttu-id="ac3f4-120">neutralQuaternaryAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-120">neutralQuaternaryAlt</span></span>
    * <span data-ttu-id="ac3f4-121">neutralQuaternary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-121">neutralQuaternary</span></span>
    * <span data-ttu-id="ac3f4-122">neutralTertiaryAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-122">neutralTertiaryAlt</span></span>
    * <span data-ttu-id="ac3f4-123">neutralTertiary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-123">neutralTertiary</span></span>
    * <span data-ttu-id="ac3f4-124">neutralSecondaryAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-124">neutralSecondaryAlt</span></span>
    * <span data-ttu-id="ac3f4-125">neutralSecondary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-125">neutralSecondary</span></span>
    * <span data-ttu-id="ac3f4-126">neutralPrimaryAlt</span><span class="sxs-lookup"><span data-stu-id="ac3f4-126">neutralPrimaryAlt</span></span>
    * <span data-ttu-id="ac3f4-127">neutralPrimary</span><span class="sxs-lookup"><span data-stu-id="ac3f4-127">neutralPrimary</span></span>
    * <span data-ttu-id="ac3f4-128">neutralDark</span><span class="sxs-lookup"><span data-stu-id="ac3f4-128">neutralDark</span></span>
    * <span data-ttu-id="ac3f4-129">black</span><span class="sxs-lookup"><span data-stu-id="ac3f4-129">black</span></span>
    * <span data-ttu-id="ac3f4-130">white</span><span class="sxs-lookup"><span data-stu-id="ac3f4-130">white</span></span>
    * <span data-ttu-id="ac3f4-131">primaryBackground</span><span class="sxs-lookup"><span data-stu-id="ac3f4-131">primaryBackground</span></span>
    * <span data-ttu-id="ac3f4-132">primaryText</span><span class="sxs-lookup"><span data-stu-id="ac3f4-132">primaryText</span></span>
    * <span data-ttu-id="ac3f4-133">error</span><span class="sxs-lookup"><span data-stu-id="ac3f4-133">error</span></span>

<span data-ttu-id="ac3f4-134">Цвета элемента _theme_ указываются в виде 6- или 3-значных шестнадцатеричных строковых значений RGB.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-134">The colors in the _theme_ element are specified as 6-digit or 3-digit hexadecimal RGB string values.</span></span>

<span data-ttu-id="ac3f4-135">Ниже представлен пример объекта JSON, определяющего тему.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-135">The following is an example of a JSON object that defines a theme.</span></span>
```json
{ 
    name: 'Blue', 
    isInverted: true, 
    backgroundImageUri: '', 
    theme: { 
        themePrimary: "#00bcf2", 
        themeLighterAlt: "#00090c", 
        themeLighter: "#001318", 
        themeLight: "#002630", 
        themeTertiary: "#005066", 
        themeSecondary: "#00abda", 
        themeDarkAlt: "#0ecbff", 
        themeDark: "#44d6ff", 
        themeDarker: "#6cdfff", 
        neutralLighterAlt: "#2e3340", 
        neutralLighter: "#353a49", 
        neutralLight: "#404759", 
        neutralQuaternaryAlt: "#474e62", 
        neutralQuaternary: "#4c546a", 
        neutralTertiaryAlt: "#646e8a", 
        neutralTertiary: "#c8c8c8", 
        neutralSecondaryAlt: "#d0d0d0", 
        neutralSecondary: "#dadada", 
        neutralPrimaryAlt: "#eaeaea", 
        neutralPrimary: "#ffffff", 
        neutralDark: "#f4f4f4", 
        black: "#f8f8f8", 
        white: "#262a35", 
        primaryBackground: "#262a35", 
        primaryText: "#ffffff", 
        error: "#ff5f5f" 
    } 
} 
```

<span data-ttu-id="ac3f4-136">Платформа SharePoint Framework включает восемь встроенных тем: шесть со светлым фоном и две с темным.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-136">The SharePoint Framework includes eight built-in themes: six on light backgrounds, and two on dark backgrounds.</span></span> <span data-ttu-id="ac3f4-137">Возможно, вам будет удобнее создать собственную тему, начав с одной из встроенных тем и настроив ее в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-137">You might find it useful to create a custom theme by starting from one of the built-in themes and adjusting it to suit your needs.</span></span>

<span data-ttu-id="ac3f4-138">Кроме того, для создания пользовательской темы можно использовать [инструмент создания тем](https://developer.microsoft.com/ru-RU/fabric#/styles/themegenerator).</span><span class="sxs-lookup"><span data-stu-id="ac3f4-138">Another option is to use the [Theme Generator tool](https://developer.microsoft.com/ru-RU/fabric#/styles/themegenerator) to build a custom theme.</span></span> <span data-ttu-id="ac3f4-139">Вам потребуется выбрать цвета будущей темы с помощью интерактивного пользовательского интерфейса. Затем определения JSON, SASS и PowerShell для вашей темы будут созданы автоматически.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-139">It provides an interactive UI for selecting theme colors, and automatically generates the JSON, SASS, and PowerShell definitions for your custom theme:</span></span>

![Инструмент создания тем](../../images/theme-generator-tool.png)

<span data-ttu-id="ac3f4-141">Ниже представлена сводка встроенных тем, включая определения JSON для их цветов, которые можно использовать в качестве отправной точки для настройки.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-141">The following is a summary of the built-in themes, including JSON definitions for the theme colors that you can use as a starting point for customization.</span></span>

## <a name="red-theme"></a><span data-ttu-id="ac3f4-142">Красная тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-142">Red theme</span></span>

<span data-ttu-id="ac3f4-143">В приведенной ниже таблице представлена цветовая палитра, используемая в красной теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-143">The following table shows the color palette used by the Red theme.</span></span>

<table><tr><td style="color:white; background-color:#751b1e"><span data-ttu-id="ac3f4-144">themeDarker: #751b1e</span><span class="sxs-lookup"><span data-stu-id="ac3f4-144">themeDarker: #751b1e</span></span></td><td style="color:white; background-color:#000000"><span data-ttu-id="ac3f4-145">black: #000000</span><span class="sxs-lookup"><span data-stu-id="ac3f4-145">black: #000000</span></span></td></tr><tr><td style="color:white; background-color:#952226"><span data-ttu-id="ac3f4-146">themeDark: #952226</span><span class="sxs-lookup"><span data-stu-id="ac3f4-146">themeDark: #952226</span></span></td><td style="color:white; background-color:#212121"><span data-ttu-id="ac3f4-147">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="ac3f4-147">neutralDark: #212121</span></span></td></tr><tr><td style="color:white; background-color:#c02b30"><span data-ttu-id="ac3f4-148">themeDarkAlt: #c02b30</span><span class="sxs-lookup"><span data-stu-id="ac3f4-148">themeDarkAlt: #c02b30</span></span></td><td style="color:white; background-color:#333"><span data-ttu-id="ac3f4-149">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="ac3f4-149">neutralPrimary: #333</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#d13438"></td><td style="color:white; background-color:#3c3c3c"><span data-ttu-id="ac3f4-150">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-150">neutralPrimaryAlt: #3c3c3c</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#d13438"><span data-ttu-id="ac3f4-151">themePrimary: #d13438</span><span class="sxs-lookup"><span data-stu-id="ac3f4-151">themePrimary: #d13438</span></span></td><td style="color:white; background-color:#666666"><span data-ttu-id="ac3f4-152">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="ac3f4-152">neutralSecondary: #666666</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#d13438"></td><td style="color:black; background-color:#a6a6a6"><span data-ttu-id="ac3f4-153">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-153">neutralTertiary: #a6a6a6</span></span></td></tr><tr><td style="color:white; background-color:#d6494d"><span data-ttu-id="ac3f4-154">themeSecondary: #d6494d</span><span class="sxs-lookup"><span data-stu-id="ac3f4-154">themeSecondary: #d6494d</span></span></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-155">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-155">neutralTertiaryAlt: #c8c8c8</span></span></td></tr><tr><td style="color:black; background-color:#ecaaac"><span data-ttu-id="ac3f4-156">themeTertiary: #ecaaac</span><span class="sxs-lookup"><span data-stu-id="ac3f4-156">themeTertiary: #ecaaac</span></span></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-157">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-157">neutralLight: #eaeaea</span></span></td></tr><tr><td style="color:black; background-color:#f6d6d8"><span data-ttu-id="ac3f4-158">themeLight: #f6d6d8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-158">themeLight: #f6d6d8</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-159">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-159">neutralLighter: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#faebeb"><span data-ttu-id="ac3f4-160">themeLighter: #faebeb</span><span class="sxs-lookup"><span data-stu-id="ac3f4-160">themeLighter: #faebeb</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-161">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-161">neutralLighterAlt: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#fdf5f5"><span data-ttu-id="ac3f4-162">themeLighterAlt: #fdf5f5</span><span class="sxs-lookup"><span data-stu-id="ac3f4-162">themeLighterAlt: #fdf5f5</span></span></td><td style="color:black; background-color:#fff"><span data-ttu-id="ac3f4-163">white: #fff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-163">white: #fff</span></span></td></tr></table>

<span data-ttu-id="ac3f4-164">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры красной темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-164">The following code shows how to define a dictionary in PowerShell for the Red theme's color palette.</span></span>
```powershell
{ 
    themeDarker: '#751b1e', 
    themeDark: '#952226', 
    themeDarkAlt: '#c02b30', 
    themePrimary: '#d13438', 
    themeSecondary: '#d6494d', 
    themeTertiary: '#ecaaac', 
    themeLight: '#f6d6d8', 
    themeLighter: '#faebeb', 
    themeLighterAlt: '#fdf5f5', 
    black: '#000000', 
    neutralDark: '#212121', 
    neutralPrimary: '#333', 
    neutralPrimaryAlt: '#3c3c3c', 
    neutralSecondary: '#666666', 
    neutralTertiary: '#a6a6a6', 
    neutralTertiaryAlt: '#c8c8c8', 
    neutralLight: '#eaeaea', 
    neutralLighter: '#f4f4f4', 
    neutralLighterAlt: '#f8f8f8', 
    white: '#fff', 
    neutralQuaternaryAlt: '#dadada', 
    neutralQuaternary: '#d0d0d0', 
    neutralSecondaryAlt: '#767676', 
    primaryBackground: '#fff', 
    primaryText: '#333' 
}
```
## <a name="orange-theme"></a><span data-ttu-id="ac3f4-165">Оранжевая тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-165">Orange theme</span></span>

<span data-ttu-id="ac3f4-166">В приведенной ниже таблице представлена цветовая палитра, используемая в оранжевой теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-166">The following table shows the color palette used by the Orange theme.</span></span>

<table><tr><td style="color:white; background-color:#6f2d09"><span data-ttu-id="ac3f4-167">themeDarker: #6f2d09</span><span class="sxs-lookup"><span data-stu-id="ac3f4-167">themeDarker: #6f2d09</span></span></td><td style="color:white; background-color:#000000"><span data-ttu-id="ac3f4-168">black: #000000</span><span class="sxs-lookup"><span data-stu-id="ac3f4-168">black: #000000</span></span></td></tr><tr><td style="color:white; background-color:#8d390b"><span data-ttu-id="ac3f4-169">themeDark: #8d390b</span><span class="sxs-lookup"><span data-stu-id="ac3f4-169">themeDark: #8d390b</span></span></td><td style="color:white; background-color:#212121"><span data-ttu-id="ac3f4-170">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="ac3f4-170">neutralDark: #212121</span></span></td></tr><tr><td style="color:white; background-color:#b5490f"><span data-ttu-id="ac3f4-171">themeDarkAlt: #b5490f</span><span class="sxs-lookup"><span data-stu-id="ac3f4-171">themeDarkAlt: #b5490f</span></span></td><td style="color:white; background-color:#333"><span data-ttu-id="ac3f4-172">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="ac3f4-172">neutralPrimary: #333</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#ca5010"></td><td style="color:white; background-color:#3c3c3c"><span data-ttu-id="ac3f4-173">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-173">neutralPrimaryAlt: #3c3c3c</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#ca5010"><span data-ttu-id="ac3f4-174">themePrimary: #ca5010</span><span class="sxs-lookup"><span data-stu-id="ac3f4-174">themePrimary: #ca5010</span></span></td><td style="color:white; background-color:#666666"><span data-ttu-id="ac3f4-175">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="ac3f4-175">neutralSecondary: #666666</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#ca5010"></td><td style="color:black; background-color:#a6a6a6"><span data-ttu-id="ac3f4-176">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-176">neutralTertiary: #a6a6a6</span></span></td></tr><tr><td style="color:white; background-color:#e55c12"><span data-ttu-id="ac3f4-177">themeSecondary: #e55c12</span><span class="sxs-lookup"><span data-stu-id="ac3f4-177">themeSecondary: #e55c12</span></span></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-178">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-178">neutralTertiaryAlt: #c8c8c8</span></span></td></tr><tr><td style="color:black; background-color:#f6b28d"><span data-ttu-id="ac3f4-179">themeTertiary: #f6b28d</span><span class="sxs-lookup"><span data-stu-id="ac3f4-179">themeTertiary: #f6b28d</span></span></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-180">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-180">neutralLight: #eaeaea</span></span></td></tr><tr><td style="color:black; background-color:#fbdac9"><span data-ttu-id="ac3f4-181">themeLight: #fbdac9</span><span class="sxs-lookup"><span data-stu-id="ac3f4-181">themeLight: #fbdac9</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-182">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-182">neutralLighter: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#fdede4"><span data-ttu-id="ac3f4-183">themeLighter: #fdede4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-183">themeLighter: #fdede4</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-184">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-184">neutralLighterAlt: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#fef6f1"><span data-ttu-id="ac3f4-185">themeLighterAlt: #fef6f1</span><span class="sxs-lookup"><span data-stu-id="ac3f4-185">themeLighterAlt: #fef6f1</span></span></td><td style="color:black; background-color:#fff"><span data-ttu-id="ac3f4-186">white: #fff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-186">white: #fff</span></span></td></tr></table>

<span data-ttu-id="ac3f4-187">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры оранжевой темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-187">The following code shows how to define a dictionary in PowerShell for the Orange theme's color palette.</span></span>

```powershell
{ 
    themeDarker: '#6f2d09', 
    themeDark: '#8d390b', 
    themeDarkAlt: '#b5490f', 
    themePrimary: '#ca5010', 
    themeSecondary: '#e55c12', 
    themeTertiary: '#f6b28d', 
    themeLight: '#fbdac9', 
    themeLighter: '#fdede4', 
    themeLighterAlt: '#fef6f1', 
    black: '#000000', 
    neutralDark: '#212121', 
    neutralPrimary: '#333', 
    neutralPrimaryAlt: '#3c3c3c', 
    neutralSecondary: '#666666', 
    neutralTertiary: '#a6a6a6', 
    neutralTertiaryAlt: '#c8c8c8', 
    neutralLight: '#eaeaea', 
    neutralLighter: '#f4f4f4', 
    neutralLighterAlt: '#f8f8f8', 
    white: '#fff', 
    neutralQuaternaryAlt: '#dadada', 
    neutralQuaternary: '#d0d0d0', 
    neutralSecondaryAlt: '#767676', 
    primaryBackground: '#fff', 
    primaryText: '#333' 
}
```
## <a name="green-theme"></a><span data-ttu-id="ac3f4-188">Зеленая тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-188">Green theme</span></span>

<span data-ttu-id="ac3f4-189">В приведенной ниже таблице представлена цветовая палитра, используемая в зеленой теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-189">The following table shows the color palette used by the Green theme.</span></span>

<table><tr><td style="color:white; background-color:#094c23"><span data-ttu-id="ac3f4-190">themeDarker: #094c23</span><span class="sxs-lookup"><span data-stu-id="ac3f4-190">themeDarker: #094c23</span></span></td><td style="color:white; background-color:#000000"><span data-ttu-id="ac3f4-191">black: #000000</span><span class="sxs-lookup"><span data-stu-id="ac3f4-191">black: #000000</span></span></td></tr><tr><td style="color:white; background-color:#0c602c"><span data-ttu-id="ac3f4-192">themeDark: #0c602c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-192">themeDark: #0c602c</span></span></td><td style="color:white; background-color:#212121"><span data-ttu-id="ac3f4-193">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="ac3f4-193">neutralDark: #212121</span></span></td></tr><tr><td style="color:white; background-color:#0f7c39"><span data-ttu-id="ac3f4-194">themeDarkAlt: #0f7c39</span><span class="sxs-lookup"><span data-stu-id="ac3f4-194">themeDarkAlt: #0f7c39</span></span></td><td style="color:white; background-color:#333"><span data-ttu-id="ac3f4-195">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="ac3f4-195">neutralPrimary: #333</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#10893e"></td><td style="color:white; background-color:#3c3c3c"><span data-ttu-id="ac3f4-196">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-196">neutralPrimaryAlt: #3c3c3c</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#10893e"><span data-ttu-id="ac3f4-197">themePrimary: #10893e</span><span class="sxs-lookup"><span data-stu-id="ac3f4-197">themePrimary: #10893e</span></span></td><td style="color:white; background-color:#666666"><span data-ttu-id="ac3f4-198">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="ac3f4-198">neutralSecondary: #666666</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#10893e"></td><td style="color:black; background-color:#a6a6a6"><span data-ttu-id="ac3f4-199">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-199">neutralTertiary: #a6a6a6</span></span></td></tr><tr><td style="color:white; background-color:#14a94e"><span data-ttu-id="ac3f4-200">themeSecondary: #14a94e</span><span class="sxs-lookup"><span data-stu-id="ac3f4-200">themeSecondary: #14a94e</span></span></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-201">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-201">neutralTertiaryAlt: #c8c8c8</span></span></td></tr><tr><td style="color:black; background-color:#7aefa7"><span data-ttu-id="ac3f4-202">themeTertiary: #7aefa7</span><span class="sxs-lookup"><span data-stu-id="ac3f4-202">themeTertiary: #7aefa7</span></span></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-203">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-203">neutralLight: #eaeaea</span></span></td></tr><tr><td style="color:black; background-color:#bff7d5"><span data-ttu-id="ac3f4-204">themeLight: #bff7d5</span><span class="sxs-lookup"><span data-stu-id="ac3f4-204">themeLight: #bff7d5</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-205">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-205">neutralLighter: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#dffbea"><span data-ttu-id="ac3f4-206">themeLighter: #dffbea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-206">themeLighter: #dffbea</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-207">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-207">neutralLighterAlt: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#effdf4"><span data-ttu-id="ac3f4-208">themeLighterAlt: #effdf4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-208">themeLighterAlt: #effdf4</span></span></td><td style="color:black; background-color:#fff"><span data-ttu-id="ac3f4-209">white: #fff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-209">white: #fff</span></span></td></tr></table>

<span data-ttu-id="ac3f4-210">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры зеленой темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-210">The following code shows how to define a dictionary in PowerShell for the Green theme's color palette.</span></span>

```powershell
{ 
    themePrimary: '#10893e', 
    themeLighterAlt: '#effdf4', 
    themeLighter: '#dffbea', 
    themeLight: '#bff7d5', 
    themeTertiary: '#7aefa7', 
    themeSecondary: '#14a94e', 
    themeDarkAlt: '#0f7c39', 
    themeDark: '#0c602c', 
    themeDarker: '#094c23', 
    neutralLighterAlt: '#f8f8f8', 
    neutralLighter: '#f4f4f4', 
    neutralLight: '#eaeaea', 
    neutralQuaternaryAlt: '#dadada', 
    neutralQuaternary: '#d0d0d0', 
    neutralTertiaryAlt: '#c8c8c8', 
    neutralTertiary: '#a6a6a6', 
    neutralSecondaryAlt: '#767676', 
    neutralSecondary: '#666666', 
    neutralPrimary: '#333', 
    neutralPrimaryAlt: '#3c3c3c', 
    neutralDark: '#212121', 
    black: '#000000', 
    white: '#fff', 
    primaryBackground: '#fff', 
    primaryText: '#333' 
}
```
## <a name="blue-theme"></a><span data-ttu-id="ac3f4-211">Синяя тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-211">Blue theme</span></span>

<span data-ttu-id="ac3f4-212">В приведенной ниже таблице представлена цветовая палитра, используемая в синей теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-212">The following table shows the color palette used by the Blue theme.</span></span>

<table><tr><td style="color:white; background-color:#004578"><span data-ttu-id="ac3f4-213">themeDarker: #004578</span><span class="sxs-lookup"><span data-stu-id="ac3f4-213">themeDarker: #004578</span></span></td><td style="color:white; background-color:#000000"><span data-ttu-id="ac3f4-214">black: #000000</span><span class="sxs-lookup"><span data-stu-id="ac3f4-214">black: #000000</span></span></td></tr><tr><td style="color:white; background-color:#005a9e"><span data-ttu-id="ac3f4-215">themeDark: #005a9e</span><span class="sxs-lookup"><span data-stu-id="ac3f4-215">themeDark: #005a9e</span></span></td><td style="color:white; background-color:#212121"><span data-ttu-id="ac3f4-216">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="ac3f4-216">neutralDark: #212121</span></span></td></tr><tr><td style="color:white; background-color:#106ebe"><span data-ttu-id="ac3f4-217">themeDarkAlt: #106ebe</span><span class="sxs-lookup"><span data-stu-id="ac3f4-217">themeDarkAlt: #106ebe</span></span></td><td style="color:white; background-color:#333"><span data-ttu-id="ac3f4-218">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="ac3f4-218">neutralPrimary: #333</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#0078d7"></td><td style="color:white; background-color:#3c3c3c"><span data-ttu-id="ac3f4-219">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-219">neutralPrimaryAlt: #3c3c3c</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#0078d7"><span data-ttu-id="ac3f4-220">themePrimary: #0078d7</span><span class="sxs-lookup"><span data-stu-id="ac3f4-220">themePrimary: #0078d7</span></span></td><td style="color:white; background-color:#666666"><span data-ttu-id="ac3f4-221">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="ac3f4-221">neutralSecondary: #666666</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#0078d7"></td><td style="color:black; background-color:#a6a6a6"><span data-ttu-id="ac3f4-222">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-222">neutralTertiary: #a6a6a6</span></span></td></tr><tr><td style="color:white; background-color:#2b88d8"><span data-ttu-id="ac3f4-223">themeSecondary: #2b88d8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-223">themeSecondary: #2b88d8</span></span></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-224">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-224">neutralTertiaryAlt: #c8c8c8</span></span></td></tr><tr><td style="color:black; background-color:#71afe5"><span data-ttu-id="ac3f4-225">themeTertiary: #71afe5</span><span class="sxs-lookup"><span data-stu-id="ac3f4-225">themeTertiary: #71afe5</span></span></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-226">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-226">neutralLight: #eaeaea</span></span></td></tr><tr><td style="color:black; background-color:#c7e0f4"><span data-ttu-id="ac3f4-227">themeLight: #c7e0f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-227">themeLight: #c7e0f4</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-228">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-228">neutralLighter: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#deecf9"><span data-ttu-id="ac3f4-229">themeLighter: #deecf9</span><span class="sxs-lookup"><span data-stu-id="ac3f4-229">themeLighter: #deecf9</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-230">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-230">neutralLighterAlt: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#eff6fc"><span data-ttu-id="ac3f4-231">themeLighterAlt: #eff6fc</span><span class="sxs-lookup"><span data-stu-id="ac3f4-231">themeLighterAlt: #eff6fc</span></span></td><td style="color:black; background-color:#fff"><span data-ttu-id="ac3f4-232">white: #fff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-232">white: #fff</span></span></td></tr></table>

<span data-ttu-id="ac3f4-233">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры синей темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-233">The following code shows how to define a dictionary in PowerShell for the Blue theme's color palette.</span></span>

```powershell
{ 
    themePrimary: '#0078d7', 
    themeLighterAlt: '#eff6fc', 
    themeLighter: '#deecf9', 
    themeLight: '#c7e0f4', 
    themeTertiary: '#71afe5', 
    themeSecondary: '#2b88d8', 
    themeDarkAlt: '#106ebe', 
    themeDark: '#005a9e', 
    themeDarker: '#004578', 
    neutralLighterAlt: '#f8f8f8', 
    neutralLighter: '#f4f4f4', 
    neutralLight: '#eaeaea', 
    neutralQuaternaryAlt: '#dadada', 
    neutralQuaternary: '#d0d0d0', 
    neutralTertiaryAlt: '#c8c8c8', 
    neutralTertiary: '#a6a6a6', 
    neutralSecondaryAlt: '#767676', 
    neutralSecondary: '#666666', 
    neutralPrimary: '#333', 
    neutralPrimaryAlt: '#3c3c3c', 
    neutralDark: '#212121', 
    black: '#000000', 
    white: '#fff', 
    primaryBackground: '#fff', 
    primaryText: '#333' 
}
```
## <a name="purple-theme"></a><span data-ttu-id="ac3f4-234">Сиреневая тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-234">Purple theme</span></span>

<span data-ttu-id="ac3f4-235">В приведенной ниже таблице представлена цветовая палитра, используемая в сиреневой теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-235">The following table shows the color palette used by the Purple theme.</span></span>

<table><tr><td style="color:white; background-color:#27268a"><span data-ttu-id="ac3f4-236">themeDarker: #27268a</span><span class="sxs-lookup"><span data-stu-id="ac3f4-236">themeDarker: #27268a</span></span></td><td style="color:white; background-color:#000000"><span data-ttu-id="ac3f4-237">black: #000000</span><span class="sxs-lookup"><span data-stu-id="ac3f4-237">black: #000000</span></span></td></tr><tr><td style="color:white; background-color:#3230b0"><span data-ttu-id="ac3f4-238">themeDark: #3230b0</span><span class="sxs-lookup"><span data-stu-id="ac3f4-238">themeDark: #3230b0</span></span></td><td style="color:white; background-color:#212121"><span data-ttu-id="ac3f4-239">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="ac3f4-239">neutralDark: #212121</span></span></td></tr><tr><td style="color:white; background-color:#5250cf"><span data-ttu-id="ac3f4-240">themeDarkAlt: #5250cf</span><span class="sxs-lookup"><span data-stu-id="ac3f4-240">themeDarkAlt: #5250cf</span></span></td><td style="color:white; background-color:#333"><span data-ttu-id="ac3f4-241">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="ac3f4-241">neutralPrimary: #333</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#6b69d6"></td><td style="color:white; background-color:#3c3c3c"><span data-ttu-id="ac3f4-242">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-242">neutralPrimaryAlt: #3c3c3c</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#6b69d6"><span data-ttu-id="ac3f4-243">themePrimary: #6b69d6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-243">themePrimary: #6b69d6</span></span></td><td style="color:white; background-color:#666666"><span data-ttu-id="ac3f4-244">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="ac3f4-244">neutralSecondary: #666666</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#6b69d6"></td><td style="color:black; background-color:#a6a6a6"><span data-ttu-id="ac3f4-245">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-245">neutralTertiary: #a6a6a6</span></span></td></tr><tr><td style="color:white; background-color:#7a78da"><span data-ttu-id="ac3f4-246">themeSecondary: #7a78da</span><span class="sxs-lookup"><span data-stu-id="ac3f4-246">themeSecondary: #7a78da</span></span></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-247">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-247">neutralTertiaryAlt: #c8c8c8</span></span></td></tr><tr><td style="color:black; background-color:#c1c0ee"><span data-ttu-id="ac3f4-248">themeTertiary: #c1c0ee</span><span class="sxs-lookup"><span data-stu-id="ac3f4-248">themeTertiary: #c1c0ee</span></span></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-249">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-249">neutralLight: #eaeaea</span></span></td></tr><tr><td style="color:black; background-color:#e1e1f7"><span data-ttu-id="ac3f4-250">themeLight: #e1e1f7</span><span class="sxs-lookup"><span data-stu-id="ac3f4-250">themeLight: #e1e1f7</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-251">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-251">neutralLighter: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#f0f0fb"><span data-ttu-id="ac3f4-252">themeLighter: #f0f0fb</span><span class="sxs-lookup"><span data-stu-id="ac3f4-252">themeLighter: #f0f0fb</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-253">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-253">neutralLighterAlt: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#f8f7fd"><span data-ttu-id="ac3f4-254">themeLighterAlt: #f8f7fd</span><span class="sxs-lookup"><span data-stu-id="ac3f4-254">themeLighterAlt: #f8f7fd</span></span></td><td style="color:black; background-color:#fff"><span data-ttu-id="ac3f4-255">white: #fff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-255">white: #fff</span></span></td></tr></table>

<span data-ttu-id="ac3f4-256">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры сиреневой темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-256">The following code shows how to define a dictionary in PowerShell for the Purple theme's color palette.</span></span>

```powershell
{ 
    themePrimary: '#6b69d6', 
    themeLighterAlt: '#f8f7fd', 
    themeLighter: '#f0f0fb', 
    themeLight: '#e1e1f7', 
    themeTertiary: '#c1c0ee', 
    themeSecondary: '#7a78da', 
    themeDarkAlt: '#5250cf', 
    themeDark: '#3230b0', 
    themeDarker: '#27268a', 
    neutralLighterAlt: '#f8f8f8', 
    neutralLighter: '#f4f4f4', 
    neutralLight: '#eaeaea', 
    neutralQuaternaryAlt: '#dadada', 
    neutralQuaternary: '#d0d0d0', 
    neutralTertiaryAlt: '#c8c8c8', 
    neutralTertiary: '#a6a6a6', 
    neutralSecondaryAlt: '#767676', 
    neutralSecondary: '#666666', 
    neutralPrimary: '#333', 
    neutralPrimaryAlt: '#3c3c3c', 
    neutralDark: '#212121', 
    black: '#000000', 
    white: '#fff', 
    primaryBackground: '#fff', 
    primaryText: '#333' 
}
```
## <a name="gray-theme"></a><span data-ttu-id="ac3f4-257">Серая тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-257">Gray theme</span></span>

<span data-ttu-id="ac3f4-258">В приведенной ниже таблице представлена цветовая палитра, используемая в серой теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-258">The following table shows the color palette used by the Gray theme.</span></span>

<table><tr><td style="color:white; background-color:#323130"><span data-ttu-id="ac3f4-259">themeDarker: #323130</span><span class="sxs-lookup"><span data-stu-id="ac3f4-259">themeDarker: #323130</span></span></td><td style="color:white; background-color:#000000"><span data-ttu-id="ac3f4-260">black: #000000</span><span class="sxs-lookup"><span data-stu-id="ac3f4-260">black: #000000</span></span></td></tr><tr><td style="color:white; background-color:#403e3d"><span data-ttu-id="ac3f4-261">themeDark: #403e3d</span><span class="sxs-lookup"><span data-stu-id="ac3f4-261">themeDark: #403e3d</span></span></td><td style="color:white; background-color:#212121"><span data-ttu-id="ac3f4-262">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="ac3f4-262">neutralDark: #212121</span></span></td></tr><tr><td style="color:white; background-color:#53504e"><span data-ttu-id="ac3f4-263">themeDarkAlt: #53504e</span><span class="sxs-lookup"><span data-stu-id="ac3f4-263">themeDarkAlt: #53504e</span></span></td><td style="color:white; background-color:#333"><span data-ttu-id="ac3f4-264">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="ac3f4-264">neutralPrimary: #333</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#5d5a58"></td><td style="color:white; background-color:#3c3c3c"><span data-ttu-id="ac3f4-265">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-265">neutralPrimaryAlt: #3c3c3c</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#5d5a58"><span data-ttu-id="ac3f4-266">themePrimary: #5d5a58</span><span class="sxs-lookup"><span data-stu-id="ac3f4-266">themePrimary: #5d5a58</span></span></td><td style="color:white; background-color:#666666"><span data-ttu-id="ac3f4-267">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="ac3f4-267">neutralSecondary: #666666</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#5d5a58"></td><td style="color:black; background-color:#a6a6a6"><span data-ttu-id="ac3f4-268">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="ac3f4-268">neutralTertiary: #a6a6a6</span></span></td></tr><tr><td style="color:white; background-color:#6d6a67"><span data-ttu-id="ac3f4-269">themeSecondary: #6d6a67</span><span class="sxs-lookup"><span data-stu-id="ac3f4-269">themeSecondary: #6d6a67</span></span></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-270">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-270">neutralTertiaryAlt: #c8c8c8</span></span></td></tr><tr><td style="color:black; background-color:#bbb9b8"><span data-ttu-id="ac3f4-271">themeTertiary: #bbb9b8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-271">themeTertiary: #bbb9b8</span></span></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-272">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-272">neutralLight: #eaeaea</span></span></td></tr><tr><td style="color:black; background-color:#dfdedd"><span data-ttu-id="ac3f4-273">themeLight: #dfdedd</span><span class="sxs-lookup"><span data-stu-id="ac3f4-273">themeLight: #dfdedd</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-274">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-274">neutralLighter: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#efeeee"><span data-ttu-id="ac3f4-275">themeLighter: #efeeee</span><span class="sxs-lookup"><span data-stu-id="ac3f4-275">themeLighter: #efeeee</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-276">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-276">neutralLighterAlt: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#f7f7f7"><span data-ttu-id="ac3f4-277">themeLighterAlt: #f7f7f7</span><span class="sxs-lookup"><span data-stu-id="ac3f4-277">themeLighterAlt: #f7f7f7</span></span></td><td style="color:black; background-color:#fff"><span data-ttu-id="ac3f4-278">white: #fff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-278">white: #fff</span></span></td></tr></table>

<span data-ttu-id="ac3f4-279">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры серой темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-279">The following code shows how to define a dictionary in PowerShell for the Gray theme's color palette.</span></span>

```powershell
{ 
    themePrimary: '#5d5a58', 
    themeLighterAlt: '#f7f7f7', 
    themeLighter: '#efeeee', 
    themeLight: '#dfdedd', 
    themeTertiary: '#bbb9b8', 
    themeSecondary: '#6d6a67', 
    themeDarkAlt: '#53504e', 
    themeDark: '#403e3d', 
    themeDarker: '#323130', 
    neutralLighterAlt: '#f8f8f8', 
    neutralLighter: '#f4f4f4', 
    neutralLight: '#eaeaea', 
    neutralQuaternaryAlt: '#dadada', 
    neutralQuaternary: '#d0d0d0', 
    neutralTertiaryAlt: '#c8c8c8', 
    neutralTertiary: '#a6a6a6', 
    neutralSecondaryAlt: '#767676', 
    neutralSecondary: '#666666', 
    neutralPrimary: '#333', 
    neutralPrimaryAlt: '#3c3c3c', 
    neutralDark: '#212121', 
    black: '#000000', 
    white: '#fff', 
    primaryBackground: '#fff', 
    primaryText: '#333' 
}
```
## <a name="dark-yellow-theme"></a><span data-ttu-id="ac3f4-280">Темно-желтая тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-280">Dark Yellow theme</span></span>

<span data-ttu-id="ac3f4-281">В приведенной ниже таблице представлена цветовая палитра, используемая в темно-желтой теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-281">The following table shows the color palette used by the Dark Yellow theme.</span></span>

<table><tr><td style="color:black; background-color:#fff171"><span data-ttu-id="ac3f4-282">themeDarker: #fff171</span><span class="sxs-lookup"><span data-stu-id="ac3f4-282">themeDarker: #fff171</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-283">black: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-283">black: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#ffed4b"><span data-ttu-id="ac3f4-284">themeDark: #ffed4b</span><span class="sxs-lookup"><span data-stu-id="ac3f4-284">themeDark: #ffed4b</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-285">neutralDark: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-285">neutralDark: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#ffe817"><span data-ttu-id="ac3f4-286">themeDarkAlt: #ffe817</span><span class="sxs-lookup"><span data-stu-id="ac3f4-286">themeDarkAlt: #ffe817</span></span></td><td style="color:black; background-color:#ffffff"><span data-ttu-id="ac3f4-287">neutralPrimary: #ffffff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-287">neutralPrimary: #ffffff</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#fce100"></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-288">neutralPrimaryAlt: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-288">neutralPrimaryAlt: #eaeaea</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#fce100"><span data-ttu-id="ac3f4-289">themePrimary: #fce100</span><span class="sxs-lookup"><span data-stu-id="ac3f4-289">themePrimary: #fce100</span></span></td><td style="color:black; background-color:#dadada"><span data-ttu-id="ac3f4-290">neutralSecondary: #dadada</span><span class="sxs-lookup"><span data-stu-id="ac3f4-290">neutralSecondary: #dadada</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#fce100"></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-291">neutralTertiary: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-291">neutralTertiary: #c8c8c8</span></span></td></tr><tr><td style="color:white; background-color:#e3cc00"><span data-ttu-id="ac3f4-292">themeSecondary: #e3cc00</span><span class="sxs-lookup"><span data-stu-id="ac3f4-292">themeSecondary: #e3cc00</span></span></td><td style="color:white; background-color:#6d6d6d"><span data-ttu-id="ac3f4-293">neutralTertiaryAlt: #6d6d6d</span><span class="sxs-lookup"><span data-stu-id="ac3f4-293">neutralTertiaryAlt: #6d6d6d</span></span></td></tr><tr><td style="color:white; background-color:#6a5f00"><span data-ttu-id="ac3f4-294">themeTertiary: #6a5f00</span><span class="sxs-lookup"><span data-stu-id="ac3f4-294">themeTertiary: #6a5f00</span></span></td><td style="color:white; background-color:#3f3f3f"><span data-ttu-id="ac3f4-295">neutralLight: #3f3f3f</span><span class="sxs-lookup"><span data-stu-id="ac3f4-295">neutralLight: #3f3f3f</span></span></td></tr><tr><td style="color:white; background-color:#322d00"><span data-ttu-id="ac3f4-296">themeLight: #322d00</span><span class="sxs-lookup"><span data-stu-id="ac3f4-296">themeLight: #322d00</span></span></td><td style="color:white; background-color:#313131"><span data-ttu-id="ac3f4-297">neutralLighter: #313131</span><span class="sxs-lookup"><span data-stu-id="ac3f4-297">neutralLighter: #313131</span></span></td></tr><tr><td style="color:white; background-color:#191700"><span data-ttu-id="ac3f4-298">themeLighter: #191700</span><span class="sxs-lookup"><span data-stu-id="ac3f4-298">themeLighter: #191700</span></span></td><td style="color:white; background-color:#282828"><span data-ttu-id="ac3f4-299">neutralLighterAlt: #282828</span><span class="sxs-lookup"><span data-stu-id="ac3f4-299">neutralLighterAlt: #282828</span></span></td></tr><tr><td style="color:white; background-color:#0d0b00"><span data-ttu-id="ac3f4-300">themeLighterAlt: #0d0b00</span><span class="sxs-lookup"><span data-stu-id="ac3f4-300">themeLighterAlt: #0d0b00</span></span></td><td style="color:white; background-color:#1f1f1f"><span data-ttu-id="ac3f4-301">white: #1f1f1f</span><span class="sxs-lookup"><span data-stu-id="ac3f4-301">white: #1f1f1f</span></span></td></tr></table>

<span data-ttu-id="ac3f4-302">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры темно-желтой темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-302">The following code shows how to define a dictionary in PowerShell for the Dark Yellow theme's color palette.</span></span>

```powershell
{ 
    themePrimary: '#fce100', 
    themeLighterAlt: '#0d0b00', 
    themeLighter: '#191700', 
    themeLight: '#322d00', 
    themeTertiary: '#6a5f00', 
    themeSecondary: '#e3cc00', 
    themeDarkAlt: '#ffe817', 
    themeDark: '#ffed4b', 
    themeDarker: '#fff171', 
    neutralLighterAlt: '#282828', 
    neutralLighter: '#313131', 
    neutralLight: '#3f3f3f', 
    neutralQuaternaryAlt: '#484848', 
    neutralQuaternary: '#4f4f4f', 
    neutralTertiaryAlt: '#6d6d6d', 
    neutralTertiary: '#c8c8c8', 
    neutralSecondaryAlt: '#d0d0d0', 
    neutralSecondary: '#dadada', 
    neutralPrimaryAlt: '#eaeaea', 
    neutralPrimary: '#ffffff', 
    neutralDark: '#f4f4f4', 
    black: '#f8f8f8', 
    white: '#1f1f1f', 
    primaryBackground: '#1f1f1f', 
    primaryText: '#ffffff', 
    error: '#ff5f5f' 
}
```
## <a name="dark-blue-theme"></a><span data-ttu-id="ac3f4-303">Темно-синяя тема</span><span class="sxs-lookup"><span data-stu-id="ac3f4-303">Dark Blue theme</span></span>

<span data-ttu-id="ac3f4-304">В приведенной ниже таблице представлена цветовая палитра, используемая в темно-синей теме.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-304">The following table shows the color palette used by the Dark Blue theme.</span></span>

<table><tr><td style="color:black; background-color:#6cdfff"><span data-ttu-id="ac3f4-305">themeDarker: #6cdfff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-305">themeDarker: #6cdfff</span></span></td><td style="color:black; background-color:#f8f8f8"><span data-ttu-id="ac3f4-306">black: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-306">black: #f8f8f8</span></span></td></tr><tr><td style="color:black; background-color:#44d6ff"><span data-ttu-id="ac3f4-307">themeDark: #44d6ff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-307">themeDark: #44d6ff</span></span></td><td style="color:black; background-color:#f4f4f4"><span data-ttu-id="ac3f4-308">neutralDark: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="ac3f4-308">neutralDark: #f4f4f4</span></span></td></tr><tr><td style="color:black; background-color:#0ecbff"><span data-ttu-id="ac3f4-309">themeDarkAlt: #0ecbff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-309">themeDarkAlt: #0ecbff</span></span></td><td style="color:black; background-color:#ffffff"><span data-ttu-id="ac3f4-310">neutralPrimary: #ffffff</span><span class="sxs-lookup"><span data-stu-id="ac3f4-310">neutralPrimary: #ffffff</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#00bcf2"></td><td style="color:black; background-color:#eaeaea"><span data-ttu-id="ac3f4-311">neutralPrimaryAlt: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="ac3f4-311">neutralPrimaryAlt: #eaeaea</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#00bcf2"><span data-ttu-id="ac3f4-312">themePrimary: #00bcf2</span><span class="sxs-lookup"><span data-stu-id="ac3f4-312">themePrimary: #00bcf2</span></span></td><td style="color:black; background-color:#dadada"><span data-ttu-id="ac3f4-313">neutralSecondary: #dadada</span><span class="sxs-lookup"><span data-stu-id="ac3f4-313">neutralSecondary: #dadada</span></span></td></tr><tr><td style="font-weight:bold; color:white; background-color:#00bcf2"></td><td style="color:black; background-color:#c8c8c8"><span data-ttu-id="ac3f4-314">neutralTertiary: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="ac3f4-314">neutralTertiary: #c8c8c8</span></span></td></tr><tr><td style="color:white; background-color:#00abda"><span data-ttu-id="ac3f4-315">themeSecondary: #00abda</span><span class="sxs-lookup"><span data-stu-id="ac3f4-315">themeSecondary: #00abda</span></span></td><td style="color:white; background-color:#646e8a"><span data-ttu-id="ac3f4-316">neutralTertiaryAlt: #646e8a</span><span class="sxs-lookup"><span data-stu-id="ac3f4-316">neutralTertiaryAlt: #646e8a</span></span></td></tr><tr><td style="color:white; background-color:#005066"><span data-ttu-id="ac3f4-317">themeTertiary: #005066</span><span class="sxs-lookup"><span data-stu-id="ac3f4-317">themeTertiary: #005066</span></span></td><td style="color:white; background-color:#404759"><span data-ttu-id="ac3f4-318">neutralLight: #404759</span><span class="sxs-lookup"><span data-stu-id="ac3f4-318">neutralLight: #404759</span></span></td></tr><tr><td style="color:white; background-color:#002630"><span data-ttu-id="ac3f4-319">themeLight: #002630</span><span class="sxs-lookup"><span data-stu-id="ac3f4-319">themeLight: #002630</span></span></td><td style="color:white; background-color:#353a49"><span data-ttu-id="ac3f4-320">neutralLighter: #353a49</span><span class="sxs-lookup"><span data-stu-id="ac3f4-320">neutralLighter: #353a49</span></span></td></tr><tr><td style="color:white; background-color:#001318"><span data-ttu-id="ac3f4-321">themeLighter: #001318</span><span class="sxs-lookup"><span data-stu-id="ac3f4-321">themeLighter: #001318</span></span></td><td style="color:white; background-color:#2e3340"><span data-ttu-id="ac3f4-322">neutralLighterAlt: #2e3340</span><span class="sxs-lookup"><span data-stu-id="ac3f4-322">neutralLighterAlt: #2e3340</span></span></td></tr><tr><td style="color:white; background-color:#00090c"><span data-ttu-id="ac3f4-323">themeLighterAlt: #00090c</span><span class="sxs-lookup"><span data-stu-id="ac3f4-323">themeLighterAlt: #00090c</span></span></td><td style="color:white; background-color:#262a35"><span data-ttu-id="ac3f4-324">white: #262a35</span><span class="sxs-lookup"><span data-stu-id="ac3f4-324">white: #262a35</span></span></td></tr></table>

<span data-ttu-id="ac3f4-325">Приведенный ниже код иллюстрирует определение словаря в PowerShell для цветовой палитры темно-синей темы.</span><span class="sxs-lookup"><span data-stu-id="ac3f4-325">The following code shows how to define a dictionary in PowerShell for the Dark Blue theme's color palette.</span></span>

```powershell
{ 
    themePrimary: '#00bcf2', 
    themeLighterAlt: '#00090c', 
    themeLighter: '#001318', 
    themeLight: '#002630', 
    themeTertiary: '#005066', 
    themeSecondary: '#00abda', 
    themeDarkAlt: '#0ecbff', 
    themeDark: '#44d6ff', 
    themeDarker: '#6cdfff', 
    neutralLighterAlt: '#2e3340', 
    neutralLighter: '#353a49', 
    neutralLight: '#404759', 
    neutralQuaternaryAlt: '#474e62', 
    neutralQuaternary: '#4c546a', 
    neutralTertiaryAlt: '#646e8a', 
    neutralTertiary: '#c8c8c8', 
    neutralSecondaryAlt: '#d0d0d0', 
    neutralSecondary: '#dadada', 
    neutralPrimaryAlt: '#eaeaea', 
    neutralPrimary: '#ffffff', 
    neutralDark: '#f4f4f4', 
    black: '#f8f8f8', 
    white: '#262a35', 
    primaryBackground: '#262a35', 
    primaryText: '#ffffff', 
    error: '#ff5f5f' 
}
```
## <a name="see-also"></a><span data-ttu-id="ac3f4-326">См. также</span><span class="sxs-lookup"><span data-stu-id="ac3f4-326">See also</span></span>

* [<span data-ttu-id="ac3f4-327">Обзор настройки тем для сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac3f4-327">SharePoint site theming overview</span></span>](sharepoint-site-theming-overview.md)
* [<span data-ttu-id="ac3f4-328">Настройка тем для сайтов SharePoint: командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac3f4-328">SharePoint site theming: PowerShell cmdlets</span></span>](sharepoint-site-theming-powershell.md)
* [<span data-ttu-id="ac3f4-329">Настройка тем для сайтов SharePoint: CSOM</span><span class="sxs-lookup"><span data-stu-id="ac3f4-329">SharePoint site theming: CSOM</span></span>](sharepoint-site-theming-csom.md)
* [<span data-ttu-id="ac3f4-330">Настройка тем для сайтов SharePoint: REST API</span><span class="sxs-lookup"><span data-stu-id="ac3f4-330">SharePoint site theming: REST API</span></span>](sharepoint-site-theming-rest-api.md)
