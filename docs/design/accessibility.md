---
title: "Специальные возможности при разработке веб-части SharePoint"
ms.date: 11/21/2017
ms.openlocfilehash: f308f8d1cbe1fabc274e8c83af9cf1b6e8d43177
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
<!--Based on how rough this content is in it's current state, i'm going to pull it from this initial release so we can edit and better prepare. -->

# <a name="accessibility-in-sharepoint-web-part-design"></a><span data-ttu-id="92b3b-102">Специальные возможности при разработке веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="92b3b-102">Accessibility in SharePoint web part design</span></span>

<span data-ttu-id="92b3b-103">При разработке веб-части SharePoint важно создать одинаковые возможности для всех пользователей, в том числе для пользователей с ограничениями зрения, слуха, подвижности, речи и способности к восприятию информации.</span><span class="sxs-lookup"><span data-stu-id="92b3b-103">Developing an equal experience that meets all users' unique visual, hearing, dexterity, cognitive, and speech needs is an important component of SharePoint web part design.</span></span> <span data-ttu-id="92b3b-104">Специальные возможности нужны не только людям с ограничениями, но и в тех ситуациях, когда использование устройства затруднено.</span><span class="sxs-lookup"><span data-stu-id="92b3b-104">Accessible design applies not only to people with disabilities, but also to potential situational impairments.</span></span> <span data-ttu-id="92b3b-105">Если они обеспечены, разработка выполнена качественно.</span><span class="sxs-lookup"><span data-stu-id="92b3b-105">Accessible design is good design.</span></span>

## <a name="accessibility-guidelines"></a><span data-ttu-id="92b3b-106">Рекомендации по специальным возможностям</span><span class="sxs-lookup"><span data-stu-id="92b3b-106">Accessibility guidelines</span></span>

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
<span data-ttu-id="92b3b-107">Все продукты Майкрософт должны соответствовать требованиям, приведенным в [стандартах Майкрософт, касающихся специальных возможностей](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Ссылка на стандарты Майкрософт, касающиеся специальных возможностей").</span><span class="sxs-lookup"><span data-stu-id="92b3b-107">All Microsoft products must meet the requirements listed in the [Microsoft Accessibility Standards](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Link to Microsoft Accesssibility Standards").</span></span>  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

<span data-ttu-id="92b3b-108">Если вы создаете диалоговое окно, средство выбора файлов или любой другой компонент [Office UI Fabric](https://dev.office.com/fabric#/components), следуйте инструкциям из этой статьи для обеспечения специальных возможностей в отношении содержимого.</span><span class="sxs-lookup"><span data-stu-id="92b3b-108">If you're building a dialog box, file picker, or any other [Office UI Fabric](https://dev.office.com/fabric#/components) component, follow the guidance in this article to ensure that your content is accessible.</span></span> 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? [v-licapu] - I agree; we shouldn't be linking to this unless it's live to external audiences; even I can't access it. I moved it to within the comment: 
[Common UI Controls](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Link to Common UI Controls") -->

## <a name="accessibility-testing"></a><span data-ttu-id="92b3b-109">Проверка специальных возможностей</span><span class="sxs-lookup"><span data-stu-id="92b3b-109">Accessibility testing</span></span>

<!-- FYI, I added links. Can we assume that our target audience uses the Edge browser? -->

<span data-ttu-id="92b3b-110">Сначала проверьте веб-часть, используя [экранный диктор](https://support.microsoft.com/ru-RU/help/22798/windows-10-narrator-get-started) и Microsoft Edge, затем — при помощи [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span><span class="sxs-lookup"><span data-stu-id="92b3b-110">Test your web part first with [Narrator](https://support.microsoft.com/ru-RU/help/22798/windows-10-narrator-get-started) and Microsoft Edge, and then verify the accessibility experience with [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).</span></span>

<span data-ttu-id="92b3b-111">Экранный диктор и Microsoft Edge соответствуют стандартам.</span><span class="sxs-lookup"><span data-stu-id="92b3b-111">Narrator and Microsoft Edge are standards compliant.</span></span> <span data-ttu-id="92b3b-112">Используя эту комбинацию инструментов, вы с большей вероятностью обнаружите проблемы. С ее помощью можно подтвердить, что сайт соответствует стандартам в отношении специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="92b3b-112">When you test with that combination, you are more likely to find issues, and you can validate that your site meets accessibility standards.</span></span> 

<span data-ttu-id="92b3b-113">JAWS — лидер рынка среди средств чтения с экрана.</span><span class="sxs-lookup"><span data-stu-id="92b3b-113">JAWS is the market leader in screen readers.</span></span> <span data-ttu-id="92b3b-114">JAWS включает компоненты, позволяющие улучшить специальные возможности некоторых веб-сайтов и недоступные в других средствах чтения с экрана.</span><span class="sxs-lookup"><span data-stu-id="92b3b-114">JAWS includes features that can improve the accessibility of some websites that aren't as accessible in other screen readers.</span></span> <span data-ttu-id="92b3b-115">Поэтому тестирование при помощи JAWS не всегда гарантирует, что сайт соответствует всем требованиям к специальным возможностям.</span><span class="sxs-lookup"><span data-stu-id="92b3b-115">Therefore testing in JAWS might not ensure that your site meets all accessibility requirements.</span></span> 
 
<span data-ttu-id="92b3b-116">Вы также можете определить сочетание браузера и средства чтения с экрана, которое охватывает наибольшую долю рынка для вашего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="92b3b-116">You might also want to test for whatever combination of browser and screen reader has the greatest market share for your website.</span></span>

<!-- Delete? This doesn't seem like text that should be in externally published docs? 
When suppliers test with JAWS, we ask them to repro identified bugs with Narrator and Edge. In the case a bug does not repro with Narrator/Edge it is sent to Mary Smith who works with VFO for a Jaws specific fix. 
-->

## <a name="keyboard-navigation"></a><span data-ttu-id="92b3b-117">Навигация с помощью клавиатуры</span><span class="sxs-lookup"><span data-stu-id="92b3b-117">Keyboard navigation</span></span>

<!-- Is this section telling people how to navigate via a keyboard, or how to design to optimize for keyboard navigation? If the former, . -->

<span data-ttu-id="92b3b-118">Для некоторых пользователей навигация по сайту с помощью клавиатуры более доступна.</span><span class="sxs-lookup"><span data-stu-id="92b3b-118">For some users, navigating a site via keyboard is more accessible.</span></span> <span data-ttu-id="92b3b-119">Опытные пользователи тоже часто обращаются к этому способу навигации.</span><span class="sxs-lookup"><span data-stu-id="92b3b-119">Power users also often rely on keyboard navigation.</span></span> <span data-ttu-id="92b3b-120">Можно использовать сочетания клавиш (например, клавишу табуляции — для открытия элементов управления на странице, а клавиши со стрелками — для перехода между ними).</span><span class="sxs-lookup"><span data-stu-id="92b3b-120">Use keyboard shortcuts such as tabs to go controls on the page, and use arrow keys to navigate inside controls.</span></span>

### <a name="navigation-between-controls"></a><span data-ttu-id="92b3b-121">Навигация между элементами управления</span><span class="sxs-lookup"><span data-stu-id="92b3b-121">Navigation between controls</span></span>

<span data-ttu-id="92b3b-122">Каждому элементу управления соответствует позиция табуляции.</span><span class="sxs-lookup"><span data-stu-id="92b3b-122">Each control is a tab stop.</span></span> <span data-ttu-id="92b3b-123">В отношении элемента управления применяются приведенные ниже правила.</span><span class="sxs-lookup"><span data-stu-id="92b3b-123">Within a control, the following rules apply:</span></span>

- <span data-ttu-id="92b3b-124">Обычно первая позиция табуляции — это верхняя левая область элемента управления,</span><span class="sxs-lookup"><span data-stu-id="92b3b-124">In general, the first tab stop is the top left area of the control.</span></span> <span data-ttu-id="92b3b-125">а последняя позиция — его нижняя правая область.</span><span class="sxs-lookup"><span data-stu-id="92b3b-125">The last tab stop is the bottom right control.</span></span>
- <span data-ttu-id="92b3b-126">На модальных поверхностях последней позицией табуляции должны быть действия фиксации.</span><span class="sxs-lookup"><span data-stu-id="92b3b-126">For modal surfaces, the last tab stop should be the commit actions.</span></span>
- <span data-ttu-id="92b3b-127">Для списков первая позиция табуляции должна быть первым элементом списка, далее должны следовать команды, а затем — элементы навигации, настройки и т. д.</span><span class="sxs-lookup"><span data-stu-id="92b3b-127">For lists, the first tab stop should be the first item in the list, the next should be the commands, and then the navigation, settings, and so on.</span></span>

<!-- We should make sure the content in the accessibility topic is accessibible. ;) Please describe the information that the image conveys; something like this (also consider making the image an actual screen shot, that might be more clear):

In the following image:
The first tab is the list item.
The second tab is the command.
The third tab is the navigation.
-->

<span data-ttu-id="92b3b-128">*Рис. 1. Позиции табуляции на странице SharePoint*</span><span class="sxs-lookup"><span data-stu-id="92b3b-128">*Figure 1. The tab stops on a SharePoint page*</span></span>

![Изображение, на котором показаны позиции табуляции на странице SharePoint](https://i.imgur.com/Vn3VosN.png)

### <a name="navigation-within-a-control"></a><span data-ttu-id="92b3b-130">Навигация в элементе управления</span><span class="sxs-lookup"><span data-stu-id="92b3b-130">Navigation within a control</span></span>

<span data-ttu-id="92b3b-131">Вы можете использовать клавиши со стрелками для перемещения между частями элемента управления (например, пунктами меню, командами на панели команд или элементами списка).</span><span class="sxs-lookup"><span data-stu-id="92b3b-131">You can use arrow keys to move to items in a control, such as choices in a menu, commands in a command bar, or items in a list.</span></span>

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

<span data-ttu-id="92b3b-132">*Рис. 2. Использование клавиш со стрелками для навигации в элементе управления*</span><span class="sxs-lookup"><span data-stu-id="92b3b-132">*Figure 2. Using arrow keys to navigate within a control*</span></span>

![Использование клавиш со стрелками для навигации в элементе управления](https://i.imgur.com/vF0Nk73.png)

### <a name="selecting-the-current-item"></a><span data-ttu-id="92b3b-134">Выбор текущего элемента</span><span class="sxs-lookup"><span data-stu-id="92b3b-134">Selecting the current item</span></span>

<span data-ttu-id="92b3b-135">Используйте клавишу пробела, чтобы выбрать или отменить выбор элемента, который в настоящее время находится в фокусе в элементе управления.</span><span class="sxs-lookup"><span data-stu-id="92b3b-135">Use the space bar to select or deselect the item currently in focus in a control.</span></span>

<span data-ttu-id="92b3b-136">*Рис. 3. Выбор элемента списка при помощи клавиши пробела*</span><span class="sxs-lookup"><span data-stu-id="92b3b-136">*Figure 3. Using the space bar to select an item in a list*</span></span>

![Выбор элемента списка при помощи клавиши пробела](https://i.imgur.com/j3fBKPl.png)

### <a name="run-a-control"></a><span data-ttu-id="92b3b-138">Запуск элемента управления</span><span class="sxs-lookup"><span data-stu-id="92b3b-138">Run a control</span></span>

<span data-ttu-id="92b3b-139">Нажмите клавишу ВВОД, чтобы запустить элемент управления.</span><span class="sxs-lookup"><span data-stu-id="92b3b-139">Select Enter or the return key to run a control.</span></span>

<span data-ttu-id="92b3b-140">*Рис. 4. Нажатие клавиши ВВОД для запуска элемента управления*</span><span class="sxs-lookup"><span data-stu-id="92b3b-140">*Figure 4. Selecting Enter to run a control*</span></span>

![Нажатие клавиши ВВОД для запуска элемента управления](https://i.imgur.com/s0nMPdT.png)

### <a name="leave-a-control"></a><span data-ttu-id="92b3b-142">Выход из элемента управления</span><span class="sxs-lookup"><span data-stu-id="92b3b-142">Leave a control</span></span>

<span data-ttu-id="92b3b-143">Нажмите клавишу **ESC**, чтобы выйти из элемента управления и вернуться к контейнеру.</span><span class="sxs-lookup"><span data-stu-id="92b3b-143">Select **Escape** to exit a control and return to the container.</span></span>

<span data-ttu-id="92b3b-144">*Рис. 5. Нажатие клавиши ESC для выхода из элемента управления и возвращения к контейнеру*</span><span class="sxs-lookup"><span data-stu-id="92b3b-144">*Figure 5. Selecting Escape to leave a control and return to the container*</span></span>

![Выход из элемента управления и возвращение к контейнеру с помощью клавиши ESC](https://i.imgur.com/uD99zIX.png)

### <a name="go-to-the-first-or-last-item"></a><span data-ttu-id="92b3b-146">Переход к первому или последнему элементу</span><span class="sxs-lookup"><span data-stu-id="92b3b-146">Go to the first or last item</span></span>

<span data-ttu-id="92b3b-147">Нажмите клавишу **HOME** или **END**, чтобы перейти сразу к первому или последнему элементу списка, меню и т. д.</span><span class="sxs-lookup"><span data-stu-id="92b3b-147">Select **Home** or **End** to go directly to the first or last item in a list, menu, and so on.</span></span>

<span data-ttu-id="92b3b-148">*Рис. 6. Переход к первому или последнему элементу списка с помощью клавиши HOME или END*</span><span class="sxs-lookup"><span data-stu-id="92b3b-148">*Figure 6. Selecting Home or End to go to the first or last item in a list*</span></span>

![Переход к первому или последнему элементу списка с помощью клавиши HOME или END](https://i.imgur.com/gGKsh74.png)


## <a name="screen-reader-navigation"></a><span data-ttu-id="92b3b-150">Навигация при помощи средства чтения с экрана</span><span class="sxs-lookup"><span data-stu-id="92b3b-150">Screen reader navigation</span></span>

<span data-ttu-id="92b3b-151">Пользователи с нарушениями зрения полагаются на средства чтения с экрана для навигации по пользовательскому интерфейсу сайта.</span><span class="sxs-lookup"><span data-stu-id="92b3b-151">Users who have vision impairments rely on screen readers to navigate the site UI.</span></span> 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

<span data-ttu-id="92b3b-152">*Рис. 7. Навигация при помощи средства чтения с экрана на странице SharePoint*</span><span class="sxs-lookup"><span data-stu-id="92b3b-152">*Figure 7. Screen reader navigation of a SharePoint page*</span></span>

![Навигация при помощи средства чтения с экрана на странице SharePoint](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a><span data-ttu-id="92b3b-154">Замещающий текст и текстовые записи</span><span class="sxs-lookup"><span data-stu-id="92b3b-154">Alt text and transcripts</span></span>

<span data-ttu-id="92b3b-155">Замещающий текст позволяет добавлять описания изображений, которые могут быть использованы средствами чтения с экрана.</span><span class="sxs-lookup"><span data-stu-id="92b3b-155">Use alt text to provide descriptions of images that can be consumed by screen readers.</span></span> <span data-ttu-id="92b3b-156">Это удобно для людей с нарушениями зрения, которые не могут получать информацию визуально.</span><span class="sxs-lookup"><span data-stu-id="92b3b-156">This is useful for vision-impaired users who cannot consume information visually.</span></span> <span data-ttu-id="92b3b-157">Проследите, чтобы замещающий текст был описательным, так как некоторые устройства для чтения получают передаваемую изображением информацию, используя средство чтения с экрана.</span><span class="sxs-lookup"><span data-stu-id="92b3b-157">Make sure that your alt text is descriptive, keeping in mind that some readers are relying on a screen reader to access the information conveyed in the image.</span></span> 

<span data-ttu-id="92b3b-158">Не полагайтесь только на цвет, чтобы передать смысл. Полагайтесь и на цвет, и на форму.</span><span class="sxs-lookup"><span data-stu-id="92b3b-158">Don't rely only on color to convey meaning; rely on both color and shape.</span></span>

<span data-ttu-id="92b3b-159">Для полного соответствия стандартам в отношении специальных возможностей добавьте на сайт замещающий текст и полную текстовую запись аудио- и видеоконтента.</span><span class="sxs-lookup"><span data-stu-id="92b3b-159">To be fully compliant with accessibility standards, include alt text and a complete transcript of audio and video content on your site.</span></span>

## <a name="minimum-readable-contrast"></a><span data-ttu-id="92b3b-160">Минимальная контрастность для читаемости</span><span class="sxs-lookup"><span data-stu-id="92b3b-160">Minimum readable contrast</span></span>

<span data-ttu-id="92b3b-161">Минимальный уровень контрастности необходим, чтобы помочь пользователям с нарушениями зрения ознакомиться с содержимым страницы.</span><span class="sxs-lookup"><span data-stu-id="92b3b-161">A minimum level of contrast is essential to help users with vision impairments consume the content on the page.</span></span> <span data-ttu-id="92b3b-162">Важно также улучшить читаемость в условиях низкой освещенности и бликов.</span><span class="sxs-lookup"><span data-stu-id="92b3b-162">It is also important to aid readability in low light and glare situations.</span></span> 

<!-- Convert this image into a table, for accessibility. ;) -->
<!-- ![Neutral, Theme, and Alert colors for minimum readable contrast](https://i.imgur.com/L7pSF1w.png)-->

![Цвета минимальной контрастности для читаемости](../images/wcag-2aa-compliance-colors.png)

### <a name="theme-colors-blue-and-neutral-colors"></a><span data-ttu-id="92b3b-164">Цвета темы (синий) и нейтральные цвета</span><span class="sxs-lookup"><span data-stu-id="92b3b-164">Theme colors (Blue) and neutral colors</span></span>

<table>
<tr>
<td style="color:white; background-color:#004578"><span data-ttu-id="92b3b-165">themeDarker: #004578</span><span class="sxs-lookup"><span data-stu-id="92b3b-165">themeDarker: #004578</span></span></td>
<td style="color:white; background-color:#000000"><span data-ttu-id="92b3b-166">black: #000000</span><span class="sxs-lookup"><span data-stu-id="92b3b-166">black: #000000</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#005a9e"><span data-ttu-id="92b3b-167">themeDark: #005a9e</span><span class="sxs-lookup"><span data-stu-id="92b3b-167">themeDark: #005a9e</span></span></td>
<td style="color:white; background-color:#212121"><span data-ttu-id="92b3b-168">neutralDark: #212121</span><span class="sxs-lookup"><span data-stu-id="92b3b-168">neutralDark: #212121</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#106ebe"><span data-ttu-id="92b3b-169">themeDarkAlt: #106ebe</span><span class="sxs-lookup"><span data-stu-id="92b3b-169">themeDarkAlt: #106ebe</span></span></td>
<td style="color:white; background-color:#333"><span data-ttu-id="92b3b-170">neutralPrimary: #333</span><span class="sxs-lookup"><span data-stu-id="92b3b-170">neutralPrimary: #333</span></span></td>
</tr>
<tr>
<td rowspan="3" style="font-weight:bold; vertical-align:middle; color:white; background-color:#0078d7"><span data-ttu-id="92b3b-171">themePrimary: #0078d7</span><span class="sxs-lookup"><span data-stu-id="92b3b-171">themePrimary: #0078d7</span></span></td>
<td style="color:white; background-color:#3c3c3c"><span data-ttu-id="92b3b-172">neutralPrimaryAlt: #3c3c3c</span><span class="sxs-lookup"><span data-stu-id="92b3b-172">neutralPrimaryAlt: #3c3c3c</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#666666"><span data-ttu-id="92b3b-173">neutralSecondary: #666666</span><span class="sxs-lookup"><span data-stu-id="92b3b-173">neutralSecondary: #666666</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#a6a6a6"><span data-ttu-id="92b3b-174">neutralTertiary: #a6a6a6</span><span class="sxs-lookup"><span data-stu-id="92b3b-174">neutralTertiary: #a6a6a6</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#2b88d8"><span data-ttu-id="92b3b-175">themeSecondary: #2b88d8</span><span class="sxs-lookup"><span data-stu-id="92b3b-175">themeSecondary: #2b88d8</span></span></td>
<td style="color:black; background-color:#c8c8c8"><span data-ttu-id="92b3b-176">neutralTertiaryAlt: #c8c8c8</span><span class="sxs-lookup"><span data-stu-id="92b3b-176">neutralTertiaryAlt: #c8c8c8</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#71afe5"><span data-ttu-id="92b3b-177">themeTertiary: #71afe5</span><span class="sxs-lookup"><span data-stu-id="92b3b-177">themeTertiary: #71afe5</span></span></td>
<td style="color:black; background-color:#eaeaea"><span data-ttu-id="92b3b-178">neutralLight: #eaeaea</span><span class="sxs-lookup"><span data-stu-id="92b3b-178">neutralLight: #eaeaea</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#c7e0f4"><span data-ttu-id="92b3b-179">themeLight: #c7e0f4</span><span class="sxs-lookup"><span data-stu-id="92b3b-179">themeLight: #c7e0f4</span></span></td>
<td style="color:black; background-color:#f4f4f4"><span data-ttu-id="92b3b-180">neutralLighter: #f4f4f4</span><span class="sxs-lookup"><span data-stu-id="92b3b-180">neutralLighter: #f4f4f4</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#deecf9"><span data-ttu-id="92b3b-181">themeLighter: #deecf9</span><span class="sxs-lookup"><span data-stu-id="92b3b-181">themeLighter: #deecf9</span></span></td>
<td style="color:black; background-color:#f8f8f8"><span data-ttu-id="92b3b-182">neutralLighterAlt: #f8f8f8</span><span class="sxs-lookup"><span data-stu-id="92b3b-182">neutralLighterAlt: #f8f8f8</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#eff6fc"><span data-ttu-id="92b3b-183">themeLighterAlt: #eff6fc</span><span class="sxs-lookup"><span data-stu-id="92b3b-183">themeLighterAlt: #eff6fc</span></span></td>
<td style="color:black; background-color:#fff"><span data-ttu-id="92b3b-184">white: #fff</span><span class="sxs-lookup"><span data-stu-id="92b3b-184">white: #fff</span></span></td>
</tr>
</table>

### <a name="alert-colors"></a><span data-ttu-id="92b3b-185">Цвета оповещений</span><span class="sxs-lookup"><span data-stu-id="92b3b-185">Alert colors</span></span>

<table>
<tr>
<td style="color:white; background-color:#952226"><span data-ttu-id="92b3b-186">themeDark: #952226</span><span class="sxs-lookup"><span data-stu-id="92b3b-186">themeDark: #952226</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#f6d6d8"><span data-ttu-id="92b3b-187">themeLight: #f6d6d8</span><span class="sxs-lookup"><span data-stu-id="92b3b-187">themeLight: #f6d6d8</span></span></td>
</tr>
<tr>
<td style="color:white; background-color:#e55c12"><span data-ttu-id="92b3b-188">themeSecondary: #e55c12</span><span class="sxs-lookup"><span data-stu-id="92b3b-188">themeSecondary: #e55c12</span></span></td>
</tr>
</table>

<br/>

<table>
<tr>
<td style="color:white; background-color:#0f7c39"><span data-ttu-id="92b3b-189">themeDarkAlt: #0f7c39</span><span class="sxs-lookup"><span data-stu-id="92b3b-189">themeDarkAlt: #0f7c39</span></span></td>
</tr>
<tr>
<td style="color:black; background-color:#bff7d5"><span data-ttu-id="92b3b-190">themeLight: #bff7d5</span><span class="sxs-lookup"><span data-stu-id="92b3b-190">themeLight: #bff7d5</span></span></td>
</tr>
</table>

## <a name="high-contrast"></a><span data-ttu-id="92b3b-191">Высокая контрастность</span><span class="sxs-lookup"><span data-stu-id="92b3b-191">High contrast</span></span>

<span data-ttu-id="92b3b-192">При выборе цвета компонентов и состояний на сайте ориентируйтесь на высококонтрастные цвета.</span><span class="sxs-lookup"><span data-stu-id="92b3b-192">Use high contrast colors as a guide for color choices for components and states on the web.</span></span> <span data-ttu-id="92b3b-193">Компьютеры с Windows могут только определить, работает ли ПК с высокой контрастностью или с высокой контрастностью белого.</span><span class="sxs-lookup"><span data-stu-id="92b3b-193">Windows computers only have the ability to detect whether a PC is running high contrast, or high contrast white.</span></span> <span data-ttu-id="92b3b-194">По этой причине используйте по умолчанию высокую контрастность черного для высококонтрастной темы любого цвета, кроме белого.</span><span class="sxs-lookup"><span data-stu-id="92b3b-194">For this reason, use the default high contrast black setting for any high contrast, non-white theme.</span></span>

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

<span data-ttu-id="92b3b-195">*Рис. 8. Параметры высококонтрастного черного и высококонтрастного белого*</span><span class="sxs-lookup"><span data-stu-id="92b3b-195">*Figure 8. High contrast black and high contrast white settings*</span></span>

![Параметры высококонтрастного черного и высококонтрастного белого](https://i.imgur.com/qvTFzd4.png)





