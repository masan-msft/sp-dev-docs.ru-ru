---
title: "Добавить фрагмент панели каналов устройств в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 612780a8-6267-49f6-a32d-33600bb5f6b4
ms.openlocfilehash: 8a86abb4f4166da8b63d1ad3c4ec8431ce1ae8fa
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="add-a-device-channel-panel-snippet-in-sharepoint"></a><span data-ttu-id="a49d0-102">Добавить фрагмент панели каналов устройств в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49d0-102">Add a Device Channel Panel snippet in SharePoint</span></span>

<span data-ttu-id="a49d0-p101">Панель канала устройств  это фрагмент, который можно добавить на эталонную страницу или макет страницы, чтобы управлять контентом, который отображается для каждого созданного канала. Основная цель панели канала устройств  это выборочное отображение полей различных страниц на различных каналах из одного макета шаблона.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p101">A Device Channel Panel is a snippet that you can add to a master page or page layout to control what content is rendered for each channel that you create. The primary purpose of a Device Channel Panel is to selectively display different page fields on different channels from a single page layout.</span></span>

## <a name="introduction-to-the-device-channel-panel-snippet"></a><span data-ttu-id="a49d0-105">Общие сведения о фрагменте панели каналов устройств</span><span class="sxs-lookup"><span data-stu-id="a49d0-105">Introduction to the Device Channel Panel snippet</span></span>
<span data-ttu-id="a49d0-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="a49d0-106"></span></span>

<span data-ttu-id="a49d0-p102">На панели каналов устройств представляет собой элемент управления, которые можно добавлять на главной странице или макету страницы для управления, какое содержимое отображается в каждом канале, создаваемого. На панели каналов устройств является контейнером, указывает одного или нескольких каналов; Если один или несколько из этих каналов активны при отображении страницы, отображаются также все содержимое панели каналов устройств. На панели каналов устройств может включать почти любой тип контента, включая ссылку на файл CSS или JS-файла. Это простой способ включения определенного содержимого для определенных каналов.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p102">A Device Channel Panel is a control that you can add to a master page or page layout to control what content is rendered in each channel that you create. A Device Channel Panel is a container that specifies one or more channels; if one or more of those channels are active when the page is rendered, all of the contents of the Device Channel Panel are also rendered. A Device Channel Panel can include almost any type of content, including a link to a CSS file or a .js file. It is an easy way to include specific content for specific channels.</span></span>
  
    
    
<span data-ttu-id="a49d0-p103">Возможно наиболее распространенные сценарии для использования каналов устройств будет выборочно включают части макета страницы для конкретных каналов. Например имеется макет страницы с отдельных текстовых полей для длинный приветственное сообщение и короткий приветствие. Размещая поля страниц внутри каналов устройств, вы можете отобразить короткий приветствие только для телефонов и много приветствие только к рабочему столу. Содержимое панели каналов устройств не отображается на каналы не включены  на самом деле содержимое не отображается, что не позволяет байт переход по сети. По этой причине использование каналов устройств  это лучший способ отображения содержимого на конкретные каналы, чем использование CSS-класс с  `Display:None` , так как каналов устройств позволяют снизить вес страницы для конкретного канала.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p103">Perhaps the most common scenario for using Device Channel Panels is to selectively include parts of a page layout for specific channels. For example, you may have a page layout with separate text fields for a long greeting and a short greeting. By placing the page fields inside Device Channel Panels, you can display the short greeting only to phones and the long greeting only to the desktop. The content of a Device Channel Panel is not displayed on non-included channels—in fact, the content is not rendered at all, which prevents bytes from going across the wire. For this reason, using Device Channel Panels is a better way to display content on specific channels than using a CSS class with  `Display:None` because Device Channel Panels help to reduce the page weight for a specific channel.</span></span>
  
    
    
<span data-ttu-id="a49d0-p104">Можно также использовать каналов устройств на главных страницах. Например при наличии главной страницы, который может принимать два разных устройства (или две различных браузерах) с помощью только минимальными изменениями каналов устройств можно использовать Чтобы удерживать содержимое на главную страницу, относящуюся к любой из этих устройств.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p104">You can also use Device Channel Panels on master pages. For example, if you have a master page that can accommodate two different devices (or two different browsers) with only minimal changes, you can use Device Channel Panels to hold the content on the master page that is specific to either of those devices.</span></span>
  
    
    
<span data-ttu-id="a49d0-118">Существует два ограничения с использованием панели каналов устройств.</span><span class="sxs-lookup"><span data-stu-id="a49d0-118">There are two limitations to using a Device Channel Panel:</span></span>
  
    
    

- <span data-ttu-id="a49d0-p105">**Шаблоны отображения** Так как шаблоны для отображения могут отображаться на стороне клиента и запустить каналов устройств на стороне сервера, нельзя использовать панели каналов устройств в шаблона для отображения. Вместо этого следует использовать два разных контента веб-частей поиска в пределах каналов устройств на макет страницы или использовать переменную JavaScript для запуска в шаблоне отображения самого желаемое поведение.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p105">**Display templates** Because display templates are rendered on the client side and Device Channel Panels run on the server side, you cannot use a Device Channel Panel within a display template. Instead, you should use two different Content Search Web Parts within Device Channel Panels on your page layout, or use the JavaScript variable to trigger the behavior you want within the display template itself.</span></span>
    
  
- <span data-ttu-id="a49d0-p106">**Зоны веб-частей** Не удается вставить зону веб-частей на панели каналов устройств. Если необходимо разрешить авторам для добавления веб-части на страницу, и если вы не беспокоит вес страницы для мобильных устройств, можно добавить поле страницы редактора форматированного текста в панели каналов устройств и Проинструктируйте авторам для добавления веб-частей существует. Можно добавить веб-части непосредственно к панели каналов устройств (без зону веб-частей).</span><span class="sxs-lookup"><span data-stu-id="a49d0-p106">**Web Part zones** You cannot insert a Web Part zone inside a Device Channel Panel. If you want to allow authors to add Web Parts to a page, and if you are not concerned about the page weight for mobile devices, you can add a Rich Text Editor page field to a Device Channel Panel, and then instruct authors to add Web Parts there. You can add Web Parts directly to a Device Channel Panel (without a Web Part zone).</span></span>
    
  

## <a name="inserting-a-device-channel-panel-snippet"></a><span data-ttu-id="a49d0-124">Вставка фрагмента панели каналов устройств</span><span class="sxs-lookup"><span data-stu-id="a49d0-124">Inserting a Device Channel Panel snippet</span></span>
<span data-ttu-id="a49d0-125"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="a49d0-125"></span></span>

<span data-ttu-id="a49d0-p107">Как и все фрагменты кода добавьте фрагмент панели каналов устройств из коллекция фрагментов кода. Чтобы перейти к коллекция фрагментов кода, сначала нужно выбрать главную страницу или макет страницы для редактирования.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p107">Like all snippets, you add a Device Channel Panel snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-a-device-channel-panel-snippet"></a><span data-ttu-id="a49d0-128">Чтобы вставить фрагмент панели каналов устройств</span><span class="sxs-lookup"><span data-stu-id="a49d0-128">To insert a Device Channel Panel snippet</span></span>


1. <span data-ttu-id="a49d0-129">Откройте свой сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="a49d0-129">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="a49d0-130">Нажмите значок шестеренки "Параметры" в правом верхнем углу страницы, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="a49d0-130">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="a49d0-131">В диспетчере оформления на левой панели навигации слева выберите **Изменить главную страницу** или **Изменение макетов страниц**, в зависимости от того, какой тип файла требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="a49d0-131">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="a49d0-132">Выберите имя главной страницы или макет страницы, который вы хотите добавить фрагмент для.</span><span class="sxs-lookup"><span data-stu-id="a49d0-132">Select the name of the master page or page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="a49d0-133">Чтобы открыть коллекцию фрагментов, выберите **Фрагменты** в правом верхнем углу страницы предварительного просмотра на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="a49d0-133">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="a49d0-134">На ленте перейдите на вкладку **Конструктор** выберите пункт **Панель канала устройств**.</span><span class="sxs-lookup"><span data-stu-id="a49d0-134">On the ribbon, on the **Design** tab, choose **Device Channel Panel**.</span></span>
    
  
7. <span data-ttu-id="a49d0-135">В разделе **Об этом компоненте** в правой части коллекции фрагментов щелкните или выберите заголовок раздела, чтобы развернуть или свернуть группу свойств, а затем настройте все нужные настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="a49d0-135">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="a49d0-p108">Раздел, с именем **важные** содержит свойства, которые являются ключом к принципы работы этого конкретного фрагмента. Для панели каналов устройств свойство **IncludedChannels** является наиболее важные. Для этого свойства введите псевдоним каждый канал устройства, который необходимо отобразить содержимое в этой панели каналов устройств. При вводе более одного псевдоним разделяйте их запятыми.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p108">The section named **Important** contains the properties that are key to how this particular snippet works. For a Device Channel Panel, the **IncludedChannels** property is the most important. For this property, enter the alias of each Device Channel that you want to display the content contained in this Device Channel Panel. If you enter more than one alias, separate each with a comma.</span></span>
    
    > <span data-ttu-id="a49d0-140">**Примечание:** При редактировании псевдоним канал в списке устройств, каналы, необходимо вручную найти и изменить то псевдоним там, где он находится в файле кода структуры, включая обновление свойства **IncludedChannels** для каждого панели канала устройств, который использует этот псевдоним</span><span class="sxs-lookup"><span data-stu-id="a49d0-140">**Note:** If you edit the alias of a channel in the Device Channels list, you must manually find and update that alias wherever it appears in your design files, including updating the **IncludedChannels** property for every Device Channel Panel that uses that alias</span></span>
8. <span data-ttu-id="a49d0-p109">После настройки других свойств выберите **обновление**. Это обновление фрагмента кода HTML в левой части страницы, чтобы разметка отражает пользовательских параметров. Всегда можно **сбросить** для возврата всех свойств к значениям по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p109">After you configure any other properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="a49d0-144">В разделе **Фрагмент HTML** в левой части коллекции фрагментов выберите команду **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="a49d0-144">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="a49d0-145">В редакторе HTML откройте сопоставленный сетевой диск на своем компьютере, а затем откройте HTML-файл для эталонной страницы или макета, к которым добавляется фрагмент.</span><span class="sxs-lookup"><span data-stu-id="a49d0-145">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
    <span data-ttu-id="a49d0-146">Дополнительные сведения см. в статье  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="a49d0-146">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
11. <span data-ttu-id="a49d0-147">Вставьте фрагмент в том месте HTML-файла, где должна отображаться разметка.</span><span class="sxs-lookup"><span data-stu-id="a49d0-147">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="a49d0-148">При добавлении фрагмента в макет страниц, убедитесь в том вставить фрагмент внутри **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="a49d0-148">If you are adding the snippet to a page layout, make sure to paste the snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="a49d0-149">Замените **<div>** в разделе `class="DefaultContentBlock"` собственным контентом.</span><span class="sxs-lookup"><span data-stu-id="a49d0-149">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content.</span></span>
    
    <span data-ttu-id="a49d0-150">Как правило при добавлении в макет страниц панели каналов устройств, замените **<div>**, скопировав поля страниц в панели.</span><span class="sxs-lookup"><span data-stu-id="a49d0-150">Typically, if you're adding a Device Channel Panel to a page layout, you replace the **<div>** by copying page fields inside the panel.</span></span>
    
  
13. <span data-ttu-id="a49d0-151">Сохраните страницу и затем обновить на сервере предварительного просмотра в диспетчере оформления, чтобы убедиться в том, что панели каналов устройств отображается должным.</span><span class="sxs-lookup"><span data-stu-id="a49d0-151">Save the page, and then refresh the server-side preview in Design Manager to make sure the Device Channel Panel appears as expected.</span></span>
    
    <span data-ttu-id="a49d0-p110">Для предварительного просмотра на разных каналах панели, можно добавить параметры строки запроса URL-адрес. К примеру можно добавить переменной строки запроса  `"DeviceChannel=YourChannelAlias"` URL-адрес любую страницу в предварительной версии на сервере.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p110">To preview the panel on different channels, you can add query string parameters to the URL. For example, you can append the query string variable  `"DeviceChannel=YourChannelAlias"` to the URL of any page in the server-side preview.</span></span>
    
  

## <a name="understanding-the-snippet-markup"></a><span data-ttu-id="a49d0-154">Сведения о разметке фрагментов</span><span class="sxs-lookup"><span data-stu-id="a49d0-154">Understanding the snippet markup</span></span>
<span data-ttu-id="a49d0-155"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="a49d0-155"></span></span>

<span data-ttu-id="a49d0-p111">Два наиболее важные части панели каналов устройств фрагмент, свойство **IncludedChannels** и **<div>** где `class="DefaultContentBlock"`. По умолчанию свойство **IncludedChannels** будет пустым. В разделе **важные** сетка свойств, необходимо ввести псевдонимы, разделенных запятыми, которые вы хотите отобразить контент этой панели каналов устройств.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p111">The two most important parts of a Device Channel Panel snippet are the **IncludedChannels** property and the **<div>** where `class="DefaultContentBlock"`. By default, the **IncludedChannels** property is empty. In the **Important** section of the property grid, you should enter the aliases, separated by commas, of the device channels that you want to display the content in this panel.</span></span>
  
    
    

> <span data-ttu-id="a49d0-159">**Примечание:** Чтобы изменить псевдоним в списке устройств, каналы, необходимо изменить то псевдоним там, где он находится в разметке, в том числе в свойстве **IncludedChannels** для каждой панели канала устройств, который использует этот псевдоним.</span><span class="sxs-lookup"><span data-stu-id="a49d0-159">**Note:** If you change an alias in the Device Channels list, you must also change that alias wherever it appears in your markup, including in the **IncludedChannels** property for every Device Channel Panel that uses that alias.</span></span>
  
    
    

<span data-ttu-id="a49d0-p112">**<div>**, где `class="DefaultContentBlock"` должно быть заменено независимо от определенного содержимого, вы должны отображаться включены каналов. На панели каналов устройств может включать почти любой тип контента, включая ссылку на файл CSS или JS-файла. Наиболее распространенные сценарии для использования каналов устройств  для добавления определенных параметров страницы полей из макета страницы для конкретных каналов. В этом случае необходимо скопировать разметки поля страницы, положение **<div>** внутри панели каналов устройств.</span><span class="sxs-lookup"><span data-stu-id="a49d0-p112">The **<div>** where `class="DefaultContentBlock"` should be replaced with whatever specific content you want to display for the included channels. A Device Channel Panel can include almost any type of content, including a link to a CSS file or a .js file. The most common scenario for using Device Channel Panels is to include specific page fields from a page layout for specific channels. In this case, you copy the page field markup where the **<div>** is positioned inside the Device Channel Panel.</span></span>
  
    
    



```HTML

<div data-name="DeviceChannelPanel">
    <!--CS: Start Device Channel Panel Snippet-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:DeviceChannelPanel runat="server" IncludedChannels="MyPhoneChannel, MyTabletChannel">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
       <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Device Channel Panel Properties.    
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</Publishing:DeviceChannelPanel>-->
    <!--CE: End Device Channel Panel Snippet-->
</div>

```


## <a name="additional-resources"></a><span data-ttu-id="a49d0-164">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a49d0-164">Additional resources</span></span>
<span data-ttu-id="a49d0-165"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="a49d0-165"></span></span>


-  [<span data-ttu-id="a49d0-166">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49d0-166">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="a49d0-167">Каналы устройств в компоненте "Дизайнер" SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49d0-167">SharePoint Design Manager device channels</span></span>](sharepoint-design-manager-device-channels.md)
    
  
-  [<span data-ttu-id="a49d0-168">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49d0-168">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a49d0-169">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49d0-169">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

