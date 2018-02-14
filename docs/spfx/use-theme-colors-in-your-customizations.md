---
title: "Использование цветов темы в настройках SharePoint Framework"
description: "Используйте цвета темы, чтобы ваши настройки сочетались с дизайном сайта, с помощью ссылки на цвета темы контекстного сайта в вашем решении SharePoint Framework."
ms.date: 01/24/2018
ms.prod: sharepoint
ms.openlocfilehash: 1fa72a0304eeb3ed93328e5040f9ca1a580a3b82
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="use-theme-colors-in-your-sharepoint-framework-customizations"></a><span data-ttu-id="4dc30-103">Использование цветов темы в настройках SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="4dc30-103">Use theme colors in your SharePoint Framework customizations</span></span>

<span data-ttu-id="4dc30-104">При создании настроек SharePoint Framework следует использовать цвета темы, чтобы настройки сочетались с дизайном сайта.</span><span class="sxs-lookup"><span data-stu-id="4dc30-104">When building SharePoint Framework customizations you should use theme colors, so that your customizations looks like a part of the site. This article explains how can you refer to the theme colors of the context site in your SharePoint Framework solution.</span></span> <span data-ttu-id="4dc30-105">В этой статье показано, как ссылаться на цвета темы контекстного сайта в решении SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="4dc30-105">When building SharePoint Framework customizations you should use theme colors, so that your customizations looks like a part of the site. This article explains how can you refer to the theme colors of the context site in your SharePoint Framework solution.</span></span>

> [!NOTE] 
> <span data-ttu-id="4dc30-106">В этой статье в качестве примера используется клиентская веб-часть SharePoint Framework, но описанные способы применимы ко всем типам настроек SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="4dc30-106">Although this article uses SharePoint Framework client-side web part as example, the described techniques apply to all types of SharePoint Framework customizations.</span></span>

## <a name="fixed-colors-vs-theme-colors"></a><span data-ttu-id="4dc30-107">Фиксированные цвета или цвета темы?</span><span class="sxs-lookup"><span data-stu-id="4dc30-107">Fixed colors vs. theme colors</span></span>

<span data-ttu-id="4dc30-108">При формировании шаблонов новой клиентской веб-части SharePoint Framework используется фиксированная синяя палитра.</span><span class="sxs-lookup"><span data-stu-id="4dc30-108">When you scaffold a new SharePoint Framework client-side web part, by default, it uses the fixed blue palette. Following steps describe the necessary adjustments to have the web part use theme colors instead.</span></span> <span data-ttu-id="4dc30-109">Если добавить такую веб-часть на современный сайт с другой цветовой схемой, она будет выделяться и выглядеть неорганично.</span><span class="sxs-lookup"><span data-stu-id="4dc30-109">When you scaffold a new SharePoint Framework client-side web part, it uses a fixed blue palette. When you add such web part on a modern site, using a different color scheme, it stands out and doesn't look like a part of the site.</span></span>

![Клиентская веб-часть SharePoint Framework, использующая синюю цветовую схему, на современном сайте группы с красной темой](../images/themed-styles-blue-web-part-red-site.png)

<span data-ttu-id="4dc30-111">Используя фиксированные цвета, вы заранее определяете, какие цвета хотите использовать для каких элементов.</span><span class="sxs-lookup"><span data-stu-id="4dc30-111">When using fixed colors, you decide upfront which colors you want to use for which elements.</span></span> <span data-ttu-id="4dc30-112">Это может привести к ситуации, когда, отображаясь на красном сайте группы, синяя веб-часть выделяется и выглядит неуместно.</span><span class="sxs-lookup"><span data-stu-id="4dc30-112">This can lead to a situation like the one just illustrated, where a blue web part is displayed on a red team site, standing out unnecessarily.</span></span> <span data-ttu-id="4dc30-113">В большинстве случаев лучше использовать цвета темы контекстного сайта, чтобы решение не выделялось, а сочеталось с сайтом.</span><span class="sxs-lookup"><span data-stu-id="4dc30-113">When using fixed colors, you decide upfront which colors you want to use for which elements. This can lead to a situation like the one just illustrated, where a blue web part is displayed on a red team site, standing out unnecessarily. In most cases, you should strive to leverage the theme colors of the context site, so that your solution doesn't stand out but looks like a part of the site.</span></span>

<span data-ttu-id="4dc30-114">SharePoint Framework позволяет использовать цвета темы контекстного сайта вместо фиксированных цветов.</span><span class="sxs-lookup"><span data-stu-id="4dc30-114">Instead of using fixed colors, SharePoint Framework allows you to refer to the theme colors of the context site.</span></span> <span data-ttu-id="4dc30-115">Как следствие, если веб-часть размещена на сайте с использованием красной темы, она также будет использовать красную палитру, а при помещении на сайт с использованием синей темы она будет автоматически настроена на использование синей палитры.</span><span class="sxs-lookup"><span data-stu-id="4dc30-115">As a result, if your web part is placed on a site that uses a red theme, it uses the red palette as well, and if it's placed on a site that uses the blue theme, it automatically adjusts itself to use the blue palette.</span></span> <span data-ttu-id="4dc30-116">Все это происходит автоматически без каких-либо изменений кода веб-части.</span><span class="sxs-lookup"><span data-stu-id="4dc30-116">All of this is done automatically without any changes to the web part code in between.</span></span>

## <a name="use-theme-colors-in-the-sharepoint-framework"></a><span data-ttu-id="4dc30-117">Использование цветов темы в SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="4dc30-117">Using theme colors in the SharePoint Framework</span></span>

<span data-ttu-id="4dc30-118">Работая с фиксированными цветами, вы указываете их в свойствах CSS, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="4dc30-118">When working with fixed colors, you specify them in CSS properties, for example:</span></span>

```css
.button {
    background-color: #0078d7;
}
```

<br/>

<span data-ttu-id="4dc30-119">Чтобы вместо этого использовать цвет темы, замените фиксированный цвет на маркер темы:</span><span class="sxs-lookup"><span data-stu-id="4dc30-119">To use a theme color instead, replace the fixed color with a theme token:</span></span>

```css
.button {
    background-color: "[theme: themePrimary, default: #0078d7]";
}
```

<br/>

<span data-ttu-id="4dc30-120">Когда настройка SharePoint Framework загружается на страницу, пакет **@microsoft/load-themed-styles**, являющийся частью SharePoint Framework, будет искать маркеры темы в файлах CSS и пытаться заменить их соответствующим цветом из текущей темы.</span><span class="sxs-lookup"><span data-stu-id="4dc30-120">When your SharePoint Framework customization is loading on the page, the **@microsoft/load-themed-styles** package, which is a part of the SharePoint Framework, will look for theme tokens in CSS files and try to replace them with the corresponding color from the current theme. If the value for the specified token is not available, SharePoint Framework will use the value specified using the default parameter instead, which is why it's important that you always include it.</span></span> <span data-ttu-id="4dc30-121">Если значение для указанного маркера недоступно, SharePoint Framework использует значение, указанное с помощью **стандартного** параметра, поэтому важно, чтобы оно всегда было включено.</span><span class="sxs-lookup"><span data-stu-id="4dc30-121">If the value for the specified token is not available, SharePoint Framework uses the value specified by using the **default** parameter instead, which is why it's important that you always include it.</span></span>

<span data-ttu-id="4dc30-122">Вы можете использовать следующие маркеры темы:</span><span class="sxs-lookup"><span data-stu-id="4dc30-122">Following theme tokens are available for you to use:</span></span>

<span data-ttu-id="4dc30-123">Маркер</span><span class="sxs-lookup"><span data-stu-id="4dc30-123">Token</span></span>|<span data-ttu-id="4dc30-124">Значение по умолчанию на современном сайте группы с использованием красной палитры</span><span class="sxs-lookup"><span data-stu-id="4dc30-124">Default value on a modern team site using the red palette</span></span>|<span data-ttu-id="4dc30-125">Комментарии</span><span class="sxs-lookup"><span data-stu-id="4dc30-125">Remarks</span></span>
-----|--------------------------------|-----------
`backgroundImageUri`|`none`|
`themeAccent`|`#ee0410`|
`themeAccentTranslucent10`|`rgba(238, 4, 16, 0.10)`|
`themeDark`|`#b3030c`|<span data-ttu-id="4dc30-126">Используется для значков действия на панели команд, а также как цвет при наведении.</span><span class="sxs-lookup"><span data-stu-id="4dc30-126">Used for action icons in the command bar and as hover color</span></span>
`themeDarkAlt`|`#b3030c`|
`themeDarker`|`#770208`|
`themeLight`|`#fd969b`|
`themeLightAlt`|`#fd969b`|
`themeLighter`|`#fecacd`|
`themeLighterAlt`|`#fecacd`|
`themePrimary`|`#ee0410`|<span data-ttu-id="4dc30-127">Основной цвет темы.</span><span class="sxs-lookup"><span data-stu-id="4dc30-127">Primary theme color.</span></span> <span data-ttu-id="4dc30-128">Используется для значков и стандартных кнопок.</span><span class="sxs-lookup"><span data-stu-id="4dc30-128">Primary theme color. Used for icons and default buttons</span></span>
`themeSecondary`|`#fc6169`|
`themeTertiary`|`#fd969b`|
`themeTertiaryAlt`|`#fd969b`|

> [!NOTE] 
> <span data-ttu-id="4dc30-129">В SharePoint Framework зарегистрировано больше маркеров.</span><span class="sxs-lookup"><span data-stu-id="4dc30-129">There are more tokens registered with the SharePoint Framework.</span></span> <span data-ttu-id="4dc30-130">Все они имеют указанные значения на классических сайтах, но только упомянутая выше часть имеет значения на современных сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4dc30-130">While all of them have values specified on classic sites, only the subset mentioned earlier has values on modern SharePoint sites.</span></span> <span data-ttu-id="4dc30-131">Полный список доступных маркеров см. в значении свойства `window.__themeState__.theme` (используйте консоль в средствах разработчика веб-браузера).</span><span class="sxs-lookup"><span data-stu-id="4dc30-131">For the complete list of available tokens, see the value of the `window.__themeState__.theme` property by using the console in your web browser's developer tools.</span></span>

## <a name="use-theme-colors-in-your-customizations"></a><span data-ttu-id="4dc30-132">Использование цветов темы в настройках</span><span class="sxs-lookup"><span data-stu-id="4dc30-132">Use theme colors in your customizations</span></span>

<span data-ttu-id="4dc30-133">При формировании шаблонов новой клиентской веб-части SharePoint Framework по умолчанию используется фиксированная синяя палитра.</span><span class="sxs-lookup"><span data-stu-id="4dc30-133">When you scaffold a new SharePoint Framework client-side web part, by default, it uses the fixed blue palette. Following steps describe the necessary adjustments to have the web part use theme colors instead.</span></span> <span data-ttu-id="4dc30-134">Ниже приведены действия, которые необходимо выполнить, чтобы веб-часть использовала цвета темы.</span><span class="sxs-lookup"><span data-stu-id="4dc30-134">The following steps describe the necessary adjustments to have the web part use theme colors instead.</span></span>

> [!NOTE] 
> <span data-ttu-id="4dc30-135">Указанные ниже инструкции относятся к клиентской веб-части SharePoint Framework _HelloWorld_, созданной с помощью React.</span><span class="sxs-lookup"><span data-stu-id="4dc30-135">The following steps apply to a SharePoint Framework client-side web part named _HelloWorld_ built by using React.</span></span> <span data-ttu-id="4dc30-136">Для веб-частей, созданных с помощью других библиотек и типов настроек, может потребоваться соответствующая корректировка изменений.</span><span class="sxs-lookup"><span data-stu-id="4dc30-136">The following steps apply to a SharePoint Framework client-side web part named HelloWorld built using React. For web parts built using different libraries and other types of customizations, you might need to adjust the modifications accordingly.</span></span>

### <a name="to-use-theme-colors"></a><span data-ttu-id="4dc30-137">Использование цветов темы</span><span class="sxs-lookup"><span data-stu-id="4dc30-137">To use theme colors</span></span>

1. <span data-ttu-id="4dc30-138">В редакторе кода откройте файл **./src/webparts/helloWorld/components/HelloWorld.tsx** и из DIV с классом **ms-Grid-row** удалите класс **ms-bgColor-themeDark**.</span><span class="sxs-lookup"><span data-stu-id="4dc30-138">In the code editor open the **./src/webparts/helloWorld/components/HelloWorld.tsx** file and from the div with class **ms-Grid-row** remove the **ms-bgColor-themeDark** class.</span></span>

    ![Класс "ms-bgColor-themeDark", выбранный в редакторе Visual Studio Code](../images/themed-styles-ms-bgcolor-themedark-class.png)

2. <span data-ttu-id="4dc30-140">В этой же папке откройте файл **HelloWorld.module.scss**.</span><span class="sxs-lookup"><span data-stu-id="4dc30-140">Next, in the same folder, open the **HelloWorld.module.scss** file. Change the  selector to:</span></span> <span data-ttu-id="4dc30-141">Измените селектор `.row` на следующий:</span><span class="sxs-lookup"><span data-stu-id="4dc30-141">Change the URL to `.row`.</span></span>

    ```css
    .row {
        padding: 20px;
        background-color: "[theme: themeDark, default: #005a9e]";
    }
    ```

    <br/>

    ![Область выделения строки, дополненная цветом фона](../images/themed-styles-row-class.png)

3. <span data-ttu-id="4dc30-143">В селекторе `.button` замените свойства `background-color` и `border-color` указанными ниже:</span><span class="sxs-lookup"><span data-stu-id="4dc30-143">In the `.button` selector, change the `background-color` and `border-color` properties to:</span></span>

    ```css
    .button {
        /* ... */
        background-color: "[theme: themePrimary, default: #0078d7]";
        border-color: "[theme: themePrimary, default: #0078d7]";
        /* ... */
    }
    ```

    <br/>

    ![Селектор .button обновлен с использованием цветов темы](../images/themed-styles-button-class.png)

4. <span data-ttu-id="4dc30-145">При добавлении веб-части на сайт цвета, используемые веб-частью, автоматически адаптируются к цветам темы, используемым на текущем сайте.</span><span class="sxs-lookup"><span data-stu-id="4dc30-145">When you add the web part to a site, the colors used by the web part will automatically adapt to the theme colors used by the current site.</span></span>

    ![Параллельное представление одной и той же веб-части, отображаемой на двух сайтах с использованием разных цветов; веб-часть соответствует цветовой схеме каждого веб-сайта](../images/themed-styles-side-by-side.png)

## <a name="see-also"></a><span data-ttu-id="4dc30-148">См. также</span><span class="sxs-lookup"><span data-stu-id="4dc30-148">See also</span></span>

- [<span data-ttu-id="4dc30-149">Темы и цвета SharePoint</span><span class="sxs-lookup"><span data-stu-id="4dc30-149">SharePoint themes and colors</span></span>](../design/themes-colors.md)
- <span data-ttu-id="4dc30-150">[Использование цветов темы в веб-частях SPFX](https://n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/), Стефан Бауэр (разработка для Office, MVP)</span><span class="sxs-lookup"><span data-stu-id="4dc30-150">[How to use Theme Colors in SPFX Web Parts](https://n8d.at/blog/how-to-use-theme-colors-in-spfx-web-parts/) by Stefan Bauer (Office Development MVP)</span></span>
