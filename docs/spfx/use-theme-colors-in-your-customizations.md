# <a name="use-theme-colors-in-your-sharepoint-framework-customizations"></a><span data-ttu-id="4c19c-101">Использование цветов темы в настройке SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="4c19c-101">Use theme colors in your SharePoint Framework customizations</span></span>

<span data-ttu-id="4c19c-p101">При создании настроек SharePoint Framework следует использовать цвета темы, чтобы настройки сочетались с дизайном сайта. Эта статья описывает, как использовать цвета темы контекстного сайта в своем решении SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p101">When building SharePoint Framework customizations you should use theme colors, so that your customizations looks like a part of the site. This article explains how can you refer to the theme colors of the context site in your SharePoint Framework solution.</span></span>

> <span data-ttu-id="4c19c-104">**Примечание.** Несмотря на то что в этой статье как пример рассматривается клиентская веб-часть SharePoint Framework, описанные способы применимы ко всем типам настроек SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="4c19c-104">**Note:** although this article uses SharePoint Framework client-side web part as example, the described techniques apply to all types of SharePoint Framework customizations.</span></span>

## <a name="fixed-colors-vs-theme-colors"></a><span data-ttu-id="4c19c-105">Фиксированные цвета или цвета темы?</span><span class="sxs-lookup"><span data-stu-id="4c19c-105">Fixed colors vs. theme colors</span></span>

<span data-ttu-id="4c19c-p102">При формировании шаблона новой клиентской веб-части SharePoint Framework используется фиксированная синяя палитра. Если добавить такую ​​веб-часть на современный сайт с другой цветовой схемой, она будет выделяться и выглядеть неорганично.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p102">When you scaffold a new SharePoint Framework client-side web part, it uses a fixed blue palette. When you add such web part on a modern site, using a different color scheme, it stands out and doesn't look like a part of the site.</span></span>

![Клиентская веб-часть SharePoint Framework, использующая синюю цветовую схему, на современном сайте группы с красной темой](../../images/themed-styles-blue-web-part-red-site.png)

<span data-ttu-id="4c19c-p103">Используя фиксированные цвета, вы заранее определяете, какие цвета вы хотите использовать для каких элементов. Это может привести к ситуации, когда, отображаясь на красном сайте группы, синяя веб-часть выделяется (а это неуместно). В большинстве случаев нужно стараться использовать цвета темы контекстного сайта, чтобы решение не выделялось, а выглядело как часть сайта.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p103">When using fixed colors, you decide upfront which colors you want to use for which elements. This can lead to a situation like the one just illustrated, where a blue web part is displayed on a red team site, standing out unnecessarily. In most cases, you should strive to leverage the theme colors of the context site, so that your solution doesn't stand out but looks like a part of the site.</span></span>

<span data-ttu-id="4c19c-p104">SharePoint Framework дает возможность использовать цвета темы контекстного сайта вместо фиксированных цветов. Если веб-часть размещена на сайте с использованием красной темы, она также будет использовать красную палитру, а если она будет помещена на сайт с использованием синей темы, то автоматически настроится на использование синей палитры. Все это происходит автоматически без каких-либо изменений кода веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p104">Instead of using fixed colors, SharePoint Framework allows you to refer to theme colors of the context site. As a result, if your web part is placed on a site using red theme, it will use the red palette as well, and if it's placed on a site using the blue theme, it will automatically adjust itself to use the blue palette. All of this is done automatically without any changes to the web part code in between.</span></span>

## <a name="using-theme-colors-in-the-sharepoint-framework"></a><span data-ttu-id="4c19c-115">Использование цветов темы в SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="4c19c-115">Using theme colors in the SharePoint Framework</span></span>

<span data-ttu-id="4c19c-116">Работая с фиксированными цветами, вы указываете их в свойствах CSS, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="4c19c-116">When working with fixed colors, you specify them in CSS properties, for example:</span></span>

```css
.button {
    background-color: #0078d7;
}
```

<span data-ttu-id="4c19c-117">Чтобы вместо этого использовать цвет темы, замените фиксированный цвет на маркер темы:</span><span class="sxs-lookup"><span data-stu-id="4c19c-117">To use a theme color instead, replace the fixed color with a theme token:</span></span>

```css
.button {
    background-color: "[theme: themePrimary, default: #0078d7]";
}
```

<span data-ttu-id="4c19c-p105">Когда настройка SharePoint Framework загружается на страницу, пакет **@microsoft/load-themed-styles**, являющийся частью SharePoint Framework, будет искать маркеры темы в файлах CSS и пытаться заменить их соответствующим цветом из текущей темы. Если значение для указанного маркера недоступно, SharePoint Framework использует значение, указанное с помощью параметра **по умолчанию**, поэтому важно, чтобы оно всегда было включено.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p105">When your SharePoint Framework customization is loading on the page, the **@microsoft/load-themed-styles** package, which is a part of the SharePoint Framework, will look for theme tokens in CSS files and try to replace them with the corresponding color from the current theme. If the value for the specified token is not available, SharePoint Framework will use the value specified using the **default** parameter instead, which is why it's important that you always include it.</span></span>

<span data-ttu-id="4c19c-120">Вы можете использовать маркеры темы, представленные ниже:</span><span class="sxs-lookup"><span data-stu-id="4c19c-120">Following theme tokens are available for you to use:</span></span>

<span data-ttu-id="4c19c-121">Маркер</span><span class="sxs-lookup"><span data-stu-id="4c19c-121">Token</span></span>|<span data-ttu-id="4c19c-122">Значение по умолчанию на современном сайте группы с использованием красной палитры</span><span class="sxs-lookup"><span data-stu-id="4c19c-122">Default value on a modern team site using the red palette</span></span>|<span data-ttu-id="4c19c-123">Комментарии</span><span class="sxs-lookup"><span data-stu-id="4c19c-123">Remarks</span></span>
-----|--------------------------------|-----------
`backgroundImageUri`|`none`|
`themeAccent`|`#ee0410`|
`themeAccentTranslucent10`|`rgba(238, 4, 16, 0.10)`|
`themeDark`|`#b3030c`|<span data-ttu-id="4c19c-124">Используется для значков действия на панели команд, а также как цвет при наведении</span><span class="sxs-lookup"><span data-stu-id="4c19c-124">Used for action icons in the command bar and as hover color</span></span>
`themeDarkAlt`|`#b3030c`|
`themeDarker`|`#770208`|
`themeLight`|`#fd969b`|
`themeLightAlt`|`#fd969b`|
`themeLighter`|`#fecacd`|
`themeLighterAlt`|`#fecacd`|
`themePrimary`|`#ee0410`|<span data-ttu-id="4c19c-p106">Основной цвет темы: используется для значков и кнопок, используемых по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4c19c-p106">Primary theme color. Used for icons and default buttons</span></span>
`themeSecondary`|`#fc6169`|
`themeTertiary`|`#fd969b`|
`themeTertiaryAlt`|`#fd969b`|

> <span data-ttu-id="4c19c-p107">**Примечание.** Кроме того, существуют дополнительные маркеры, зарегистрированные в SharePoint Framework. Хотя все они имеют значения, указанные на классических сайтах, только упомянутое выше подмножество имеет значения на современных сайтах SharePoint. Полный список доступных маркеров см. в значении свойства `window.__themeState__.theme`, использующего консоль в средствах разработчика веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p107">**Note:** there are more tokens registered with the SharePoint Framework. While all of them have values specified on classic sites, only the subset mentioned earlier has values on modern SharePoint sites. For the complete list of available tokens, see the value of the `window.__themeState__.theme` property using the console in your web browser's developer tools.</span></span>

## <a name="use-theme-colors-in-your-customizations"></a><span data-ttu-id="4c19c-130">Использование цветов темы в настройках SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="4c19c-130">Use theme colors in your customizations</span></span>

<span data-ttu-id="4c19c-p108">При формировании шаблона новой клиентской веб-части SharePoint Framework по умолчанию используется фиксированная синяя палитра. Следующие шаги описывают корректировки, которые необходимо сделать, чтобы использовать цвета темы веб-части.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p108">When you scaffold a new SharePoint Framework client-side web part, by default, it uses the fixed blue palette. Following steps describe the necessary adjustments to have the web part use theme colors instead.</span></span>

> <span data-ttu-id="4c19c-p109">**Примечание.** Указанные ниже действия применяются для клиентской веб-части SharePoint Framework с именем _HelloWorld_, построенной с использованием React. Для веб-частей, созданных с использованием других библиотек и типов настроек, может потребоваться соответствующая корректировка изменений.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p109">**Note:** the following steps apply to a SharePoint Framework client-side web part named _HelloWorld_ built using React. For web parts built using different libraries and other types of customizations, you might need to adjust the modifications accordingly.</span></span>

<span data-ttu-id="4c19c-135">В редакторе кода откройте файл **./src/webparts/helloWorld/components/HelloWorld.tsx** и с div с классом **ms-Grid-row** удалите класс **ms-bgColor-themeDark**.</span><span class="sxs-lookup"><span data-stu-id="4c19c-135">In the code editor open the **./src/webparts/helloWorld/components/HelloWorld.tsx** file and from the div with class **ms-Grid-row** remove the **ms-bgColor-themeDark** class.</span></span>

![Класс "ms-bgColor-themeDark", выбранный в редакторе Visual Studio Code](../../images/themed-styles-ms-bgcolor-themedark-class.png)

<span data-ttu-id="4c19c-p110">Затем в той же папке откройте файл **HelloWorld.module.scss** и измените `.row` селектор на указанный ниже.</span><span class="sxs-lookup"><span data-stu-id="4c19c-p110">Next, in the same folder, open the **HelloWorld.module.scss** file. Change the `.row` selector to:</span></span>

```css
.row {
    padding: 20px;
    background-color: "[theme: themeDark, default: #005a9e]";
}
```

![Область выделения строки, дополненная цветом фона](../../images/themed-styles-row-class.png)

<span data-ttu-id="4c19c-140">В селекторе `.button` замените свойства `background-color` и `border-color` указанными ниже:</span><span class="sxs-lookup"><span data-stu-id="4c19c-140">In the `.button` selector, change the `background-color` and `border-color` properties to:</span></span>

```css
.button {
    /* ... */
    background-color: "[theme: themePrimary, default: #0078d7]";
    border-color: "[theme: themePrimary, default: #0078d7]";
    /* ... */
}
```

![Селектор .button обновлен с использованием цветов темы](../../images/themed-styles-button-class.png)

<span data-ttu-id="4c19c-142">При добавлении веб-части на сайт цвета, используемые веб-частью, будут автоматически адаптироваться к цветам темы, используемым на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="4c19c-142">When you add the web part to a site, the colors used by the web part will automatically adapt to the theme colors used by the current site.</span></span>

![Параллельное представление одной и той же веб-части, отображаемой на двух сайтах с использованием разных цветов; веб-часть соответствует цветовой схеме каждого веб-сайта](../../images/themed-styles-side-by-side.png)

## <a name="more-information"></a><span data-ttu-id="4c19c-145">Подробнее</span><span class="sxs-lookup"><span data-stu-id="4c19c-145">More information</span></span>

* [<span data-ttu-id="4c19c-146">Использование цветов темы в веб-частях SPFX</span><span class="sxs-lookup"><span data-stu-id="4c19c-146">How to use Theme Colors in SPFX Web Parts</span></span>](http://www.n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/), Стефан Бауэр (разработка для Office, MVP)