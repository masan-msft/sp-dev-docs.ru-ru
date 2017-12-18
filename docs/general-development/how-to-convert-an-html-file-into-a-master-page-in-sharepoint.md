---
title: "Преобразование HTML-файла в эталонную страницу SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a76ab289-3256-45de-ac63-d5112a74e3c7
ms.openlocfilehash: df93a6b57fc719e83f337b061e575b7caa97eba6
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="convert-an-html-file-into-a-master-page-in-sharepoint"></a><span data-ttu-id="b8aca-102">Преобразование HTML-файла в эталонную страницу SharePoint</span><span class="sxs-lookup"><span data-stu-id="b8aca-102">How to: Convert an HTML file into a master page in SharePoint</span></span>

<span data-ttu-id="b8aca-p101">Благодаря Дизайнеру вы можете конвертировать HTML-файл в эталонную страницу SharePoint  MASTER-файл. После преобразования HTML-файл и эталонная страница будут связаны, чтобы при редактировании и сохранении HTML-файла эти изменения синхронизировались со связанной эталонной страницей.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p101">With Design Manager, you can convert an .html file into a SharePoint master page, a .master file. After the conversion, the HTML file and master page are associated, so that when you edit and save the HTML file, the changes are synced to the associated master page.</span></span>

## <a name="introduction-to-converting-a-master-page"></a><span data-ttu-id="b8aca-105">Общие сведения о преобразовании эталонной страницы</span><span class="sxs-lookup"><span data-stu-id="b8aca-105">Introduction to converting a master page</span></span>
<span data-ttu-id="b8aca-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="b8aca-106"><a name="Introduction"> </a></span></span>

 <span data-ttu-id="b8aca-107">С помощью компонента "Дизайнер" вы можете преобразовать HTML-файл в эталонную страницу SharePoint — MASTER-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-107">With Design Manager, you can convert an.html file into a SharePoint master page, a .master file.</span></span> <span data-ttu-id="b8aca-108">После преобразования HTML-файл и эталонная страница будут связаны, чтобы при редактировании и сохранении HTML-файла эти изменения синхронизировались со связанной эталонной страницей.</span><span class="sxs-lookup"><span data-stu-id="b8aca-108">After the conversion, the HTML file and master page are associated, so that when you edit and save the HTML file, the changes are synced to the associated master page.</span></span>
  
    
    
<span data-ttu-id="b8aca-109">Зачем преобразовывать HTML-файл, а не создавать MASTER-файл с нуля?</span><span class="sxs-lookup"><span data-stu-id="b8aca-109">Why do you want to convert an HTML file, instead of creating a .master file from scratch?</span></span> <span data-ttu-id="b8aca-110">В SharePoint эталонные страницы работают точно так же, как в ASP.NET, но в SharePoint для корректного отображения эталонной страницы также необходимо, чтобы на странице присутствовали определенные элементы, например элементы управления и заполнители контента, относящиеся к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8aca-110">In SharePoint, master pages work exactly as they do in ASP.NET, but SharePoint also requires that certain elements, such as controls and content placeholders that are specific to SharePoint, must be present on the page for SharePoint to correctly render that master page.</span></span> <span data-ttu-id="b8aca-111">Если вы используете "Дизайнер" для преобразования HTML-файла в полноценную эталонную страницу SharePoint, то вам не потребуется знание разметки ASP.NET или SharePoint. Вместо этого вы можете сосредоточиться на разработке сайта с помощью HTML, CSS и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b8aca-111">By using Design Manager to convert an HTML file into a fully functioning SharePoint master page, you don't have to know about ASP.NET or the SharePoint-specific markup; instead, you can focus on designing your site in HTML, CSS, and JavaScript.</span></span>
  
    
    
<span data-ttu-id="b8aca-112">При преобразовании HTML-файла в эталонную страницу происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="b8aca-112">When you convert an HTML file into a master page:</span></span>
  
    
    

- <span data-ttu-id="b8aca-113">В коллекции эталонных страниц создается MASTER-файл с таким же именем, как у HTML-файла.</span><span class="sxs-lookup"><span data-stu-id="b8aca-113">A .master file with the same name as your HTML file is created in the Master Page Gallery.</span></span>
    
  
- <span data-ttu-id="b8aca-114">В MASTER-файл добавляется вся разметка, необходимая SharePoint, поэтому эталонная страница отображается правильно.</span><span class="sxs-lookup"><span data-stu-id="b8aca-114">All markup required by SharePoint is added to the .master file so that the master page renders correctly.</span></span>
    
  
- <span data-ttu-id="b8aca-115">В исходный HTML-файл добавляется разметка, например комментарии, теги **\<div\>**, фрагменты кода и заполнители контента.</span><span class="sxs-lookup"><span data-stu-id="b8aca-115">Markup such as comments, **\<div\>** tags, snippets, and content placeholders are added to your original HTML file.</span></span>
    
  
- <span data-ttu-id="b8aca-116">HTML-файл и эталонная страница связываются, поэтому в дальнейшем при сохранении внесенных в HTML-файл изменений, этот файл будет синхронизирован с MASTER-файлом.</span><span class="sxs-lookup"><span data-stu-id="b8aca-116">The HTML file and master page are associated, so that any later edits to the HTML file are synced to the .master file when the HTML file is saved.</span></span>
    
  

> <span data-ttu-id="b8aca-117">**Примечание.** Синхронизация выполняется только в одном направлении.</span><span class="sxs-lookup"><span data-stu-id="b8aca-117">**Note:** The syncing goes in one direction only.</span></span> <span data-ttu-id="b8aca-118">Изменения эталонной страницы HTML будут синхронизированы со связанным MASTER-файлом, однако если вы редактируете непосредственно MASTER-файл, внесенные изменения не будут синхронизированы с HTML-файлом.</span><span class="sxs-lookup"><span data-stu-id="b8aca-118">Changes to the HTML master page are synced to the associated .master file, but if you choose to edit the .master file directly the changes are not synced to the HTML file.</span></span> <span data-ttu-id="b8aca-119">У каждой эталонной страницы HTML (и каждого макета HTML-страницы) есть свойство **Связанный файл**, для которого по умолчанию задано значение **True**, что обеспечивает связь и синхронизацию между файлами.</span><span class="sxs-lookup"><span data-stu-id="b8aca-119">Every HTML master page (and every HTML page layout) has a property named **Associated File** that is set to **True** by default, which creates the association and syncing between files.</span></span>
  
    
    

<span data-ttu-id="b8aca-p105">Если у вас есть пара связанных файлов (HTML и MASTER) и вы изменяете MASTER-файл, не нарушая связь, внесенные изменения будут сохранены, но вы не сможете отметить или опубликовать этот файл, то есть по большому счету эти изменения не сохраняются. Любые изменения в файле HTML перезаписывают MASTER-файл. Если вы отметите или опубликуете HTML-файл, то его изменения перезапишут любые изменения, которые были сделаны в MASTER-файле. Изменения, внесенные в MASTER-файл, будут изменены.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p105">If you have a pair of associated files (HTML and .master) and you edit the .master file without breaking the association, the changes to the .master file will be saved, but you can't check in or publish the .master file, so those changes are not saved in a meaningful way. Any changes to the HTML file override the .master file. If you check in or publish the HTML file, the HTML file changes override any changes that were made to the .master file. The changes to the .master file are lost.</span></span>
  
    
    
<span data-ttu-id="b8aca-124">Если вы разработчик, обладающий опытом работы с ASP.NET, то вы можете работать с MASTER-файлом отдельно, нарушив связь между файлами.</span><span class="sxs-lookup"><span data-stu-id="b8aca-124">If you're a developer comfortable working with ASP.NET, you can choose to work only with the .master file by breaking the association between the files.</span></span> <span data-ttu-id="b8aca-125">Чтобы отменить связь между HTML-файлом и MASTER-файлом, в компоненте "Дизайнер" нажмите **Изменить свойства** для HTML-файла, а затем снимите флажок **Связанный файл**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-125">To break the association between the HTML file and the .master file, in Design Manager, choose **Edit Properties** for the HTML file, and then clear the **Associated File** check box.</span></span> <span data-ttu-id="b8aca-126">Позже вы можете заново связать файлы, изменив свойства и установив этот флажок. В этом случае HTML-файл снова заменит MASTER-файл, а изменения, внесенные в MASTER-файл, будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="b8aca-126">You can later re-associate the files by editing the properties and selecting this check box, in which case the HTML file will again overwrite the .master file, and changes made to the .master file will be lost.</span></span>
  
    
    

## <a name="prepare-the-html-file-for-conversion"></a><span data-ttu-id="b8aca-127">Подготовка HTML-файла к преобразованию</span><span class="sxs-lookup"><span data-stu-id="b8aca-127">Prepare the HTML file for conversion</span></span>
<span data-ttu-id="b8aca-128"><a name="Prepare"> </a></span><span class="sxs-lookup"><span data-stu-id="b8aca-128"><a name="Prepare"> </a></span></span>

<span data-ttu-id="b8aca-129">Прежде чем преобразовывать HTML-файл, ознакомьтесь с приведенными ниже советами и рекомендациями.</span><span class="sxs-lookup"><span data-stu-id="b8aca-129">Before you convert your HTML file, here are some best practices and guidance to consider:</span></span>
  
    
    

- <span data-ttu-id="b8aca-130">Рассмотрим модель страниц в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8aca-130">Consider the SharePoint page model.</span></span> <span data-ttu-id="b8aca-131">Дополнительные сведения см. в статье [Обзор модели страниц в SharePoint](overview-of-the-sharepoint-page-model.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-131">For more information, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model.md).</span></span> <span data-ttu-id="b8aca-132">При создании HTML-макетов для сайта у вас наверняка будет несколько HTML-файлов для разных типов страниц, например статьи или страницы категории, содержащей веб-части, в которых отображаются элементы определенной категории из каталога.</span><span class="sxs-lookup"><span data-stu-id="b8aca-132">As you design the HTML mockups of your site, you'll probably have several HTML files for different types of pages, such as an article page or a category page that contains Web Parts that display a category of items from a catalog.</span></span> <span data-ttu-id="b8aca-133">Однако только один HTML-файл будет преобразован в эталонную страницу.</span><span class="sxs-lookup"><span data-stu-id="b8aca-133">But, only one HTML file will be converted into the master page.</span></span> <span data-ttu-id="b8aca-134">HTML-файл можно преобразовать в эталонную страницу, но невозможно преобразовать непосредственно в макет страницы, так как для этого необходимы поля страницы.</span><span class="sxs-lookup"><span data-stu-id="b8aca-134">An HTML file can be converted into a master page, but an HTML file can't be converted directly into a page layout because a page layout requires page fields.</span></span>
    
  
- <span data-ttu-id="b8aca-135">Убедитесь, что HTML-файл совместим с форматом XML.</span><span class="sxs-lookup"><span data-stu-id="b8aca-135">Make sure your HTML file is XML-compliant.</span></span> <span data-ttu-id="b8aca-136">Для успешного преобразования HTML-файл должен быть совместимым с XML.</span><span class="sxs-lookup"><span data-stu-id="b8aca-136">For the conversion to work, the HTML file must be XML-compliant.</span></span> <span data-ttu-id="b8aca-137">К сожалению, это требование переопределяет некоторые стандарты HTML 5. Например, в HTML 5 можно указать значение **doctype** в нижнем регистре, но в XML значение **doctype** следует указывать прописными буквами.</span><span class="sxs-lookup"><span data-stu-id="b8aca-137">Unfortunately, this requirement overrides some HTML 5 standards—for example, in HTML 5 you can specify the **doctype** in lowercase, but in XML the **doctype** must be uppercase.</span></span> <span data-ttu-id="b8aca-138">Кроме того, из HTML-файла следует удалить теги **\<form\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-138">Also, you should remove any **\<form\>** tags from your HTML file.</span></span> <span data-ttu-id="b8aca-139">Вы можете пропустить HTML-файл через внешнее средство проверки XML, чтобы обнаружить ошибки XML перед преобразованием.</span><span class="sxs-lookup"><span data-stu-id="b8aca-139">Consider running your HTML file through an external XML validator to identify XML errors before conversion.</span></span>
    
  
- <span data-ttu-id="b8aca-140">Ниже представлены важные рекомендации, связанные со ссылками CSS.</span><span class="sxs-lookup"><span data-stu-id="b8aca-140">Consider these important guidelines for your CSS references:</span></span>
    
  - <span data-ttu-id="b8aca-141">Не помещайте блоки **\<style\>** в тег **\<head\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-141">Don't put **\<style\>** blocks in the **\<head\>** tag.</span></span> <span data-ttu-id="b8aca-142">Эти стили удаляются во время преобразования.</span><span class="sxs-lookup"><span data-stu-id="b8aca-142">These styles are removed during conversion.</span></span> <span data-ttu-id="b8aca-143">Вместо этого ссылайтесь в HTML-файле на внешний CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-143">Instead, link from your HTML file to an external CSS file.</span></span>
    
  
  - <span data-ttu-id="b8aca-144">Добавьте параметр `ms-design-css-conversion="no"` в тег **\<CSS link\>**, если вы используете веб-шрифт.</span><span class="sxs-lookup"><span data-stu-id="b8aca-144">Add  `ms-design-css-conversion="no"` to the **\<CSS link\>** tag if you're using a web font.</span></span>
    
  
  - <span data-ttu-id="b8aca-145">Будьте осторожны, применяя стили к общим HTML-тегам, например **\<body\>**, **\<div\>** и **\<img\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-145">Be cautious about applying styles to general HTML tags like **\<body\>**, **\<div\>**, and **\<img\>**.</span></span> <span data-ttu-id="b8aca-146">Все содержимое оформления SharePoint, включая ленту, находится внутри тега **\<body\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-146">Everything within your SharePoint design, including the ribbon, is within the **\<body\>** tag.</span></span> <span data-ttu-id="b8aca-147">Стили, которые обычно применялись бы к тегу **\<body\>**, следует применять к тегу **\<div id="s4-bodyContainer"\>**, который SharePoint использует для основного текста страницы.</span><span class="sxs-lookup"><span data-stu-id="b8aca-147">For styles that you would usually apply to the **\<body\>** tag, consider applying them instead to **\<div id="s4-bodyContainer"\>**, which is a tag that SharePoint uses for the main body of the page.</span></span> <span data-ttu-id="b8aca-148">Кроме того, SharePoint использует множество изображений, на которые влияют стили, применяемые к тегу **\<img\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-148">Also, SharePoint uses many images that are affected by whatever styles you apply to the **\<img\>** tag.</span></span>
    
  
  - <span data-ttu-id="b8aca-149">Многие дизайнеры настраивают стиль навигации, применяя классы к элементам **\<ul\>** и **\<li\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-149">Many designers style the navigation by applying classes to **\<ul\>** and **\<li\>** elements.</span></span> <span data-ttu-id="b8aca-150">Однако в SharePoint используется динамический элемент навигации, который можно добавить на эталонную страницу из коллекции фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="b8aca-150">But, SharePoint uses a dynamic navigation control, which you can add to your master page from the Snippet Gallery.</span></span> <span data-ttu-id="b8aca-151">По умолчанию к элементам навигации SharePoint применены стили, которые необходимо переопределять.</span><span class="sxs-lookup"><span data-stu-id="b8aca-151">SharePoint navigation controls have styles applied by default that you have to override.</span></span>
    
  
- <span data-ttu-id="b8aca-152">Ниже указаны возможные проблемы с именованием файлов.</span><span class="sxs-lookup"><span data-stu-id="b8aca-152">Consider these potential issues about file naming:</span></span>
    
  - <span data-ttu-id="b8aca-153">Файлы Index.html и Index.htm будут иметь один и тот же MASTER-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-153">If you have Index.html and Index.htm, those files will have the same .master file.</span></span>
    
  
  - <span data-ttu-id="b8aca-p112">Файлы Design/Index.html и Design/SubDesign/Index.html будут преобразованы в отдельные MASTER-файлы, но они оба будут отображаться в списке эталонной странице в Дизайнере как Index.html. Чтобы устранить неоднозначность, щелкните каждый файл или нажмите кнопку с многоточием, чтобы увидеть полный путь.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p112">If you have Design/Index.html and Design/SubDesign/Index.html, both of those files are available for conversion into their own, separate .master files, but they'll both show up as Index.html in the master page list in Design Manager. To disambiguate them, click or select the ellipsis button for each file to see the full path.</span></span>
    
  
- <span data-ttu-id="b8aca-156">Если вы добавляете мини-приложение JavaScript, убедитесь, что открывающий тег **\<script\>** находится на отдельной строке.</span><span class="sxs-lookup"><span data-stu-id="b8aca-156">If you're adding a JavaScript widget, make sure the **\<script\>** start tag is on its own line.</span></span>
    
```
  
<script>
(function( …

```

<span data-ttu-id="b8aca-157">Не помещайте их в одну строку, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b8aca-157">Do not put them on the same line, like this.</span></span>
    


```
  
<Script> (function( …
```

- <span data-ttu-id="b8aca-158">Ссылка на библиотеку JQuery (внешняя ссылка) должна находиться перед тегом **\</head\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-158">A reference to the JQuery library (an external reference) should go before the **\</head\>** tag.</span></span>
    
  

## <a name="convert-the-html-file-into-a-master-page"></a><span data-ttu-id="b8aca-159">Преобразование HTML-файла в эталонную страницу</span><span class="sxs-lookup"><span data-stu-id="b8aca-159">Convert the HTML file into a master page</span></span>
<span data-ttu-id="b8aca-160"><a name="Convert"> </a></span><span class="sxs-lookup"><span data-stu-id="b8aca-160"><a name="Convert"> </a></span></span>

<span data-ttu-id="b8aca-161">Перед преобразованием HTML-файла необходимо отправить все файлы оформления, включая HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-161">Before you convert an HTML file, you first have to upload all of your design files, including your HTML file.</span></span> <span data-ttu-id="b8aca-162">Дополнительные сведения см. в статье [Инструкции. Сопоставление сетевого диска с коллекцией эталонных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-162">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    

### <a name="to-convert-the-html-file-into-a-master-file"></a><span data-ttu-id="b8aca-163">Преобразование HTML-файла в MASTER-файл</span><span class="sxs-lookup"><span data-stu-id="b8aca-163">To convert the HTML file into a .master file</span></span>


1. <span data-ttu-id="b8aca-164">Перейдите на сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="b8aca-164">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="b8aca-165">В правом верхнем углу страницы выберите пункт **Параметры**, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-165">In the upper-right corner of the page, choose **Settings**, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="b8aca-166">Откройте "Дизайнер" и в области навигации слева выберите команду **Изменить главные страницы**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-166">In Design Manager, in the left navigation pane, choose **Edit Master Pages**.</span></span>
    
  
4. <span data-ttu-id="b8aca-167">Выберите пункт **Преобразование HTML-файла в главную страницу SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-167">Choose **Convert an HTML file to a SharePoint master page**.</span></span>
    
  
5. <span data-ttu-id="b8aca-168">В диалоговом окне **Выбор актива** найдите и выберите преобразуемый HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-168">In the **Select an Asset** dialog box, browse to and select the HTML file that you want to convert.</span></span>
    
    > <span data-ttu-id="b8aca-169">**Примечание.** При отправке файлов оформления следует хранить все файлы, связанные с одним оформлением, в отдельной папке в коллекции эталонных страниц.</span><span class="sxs-lookup"><span data-stu-id="b8aca-169">**Note:** When you upload your design files, you should keep all files that are related to a single design in their own folder in the Master Page Gallery.</span></span> <span data-ttu-id="b8aca-170">Если скопировать папку оформления на сопоставленный сетевой диск, в коллекции эталонных страниц сохранится созданная вами структура папок.</span><span class="sxs-lookup"><span data-stu-id="b8aca-170">When you copy your design folder into the mapped network drive, the Master Page Gallery retains whatever folder structure you created.</span></span> 
6. <span data-ttu-id="b8aca-171">Нажмите кнопку **Вставить**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-171">Choose **Insert**.</span></span>
    
    <span data-ttu-id="b8aca-172">На этом этапе SharePoint преобразует HTML-файл в MASTER-файл с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="b8aca-172">At this point, SharePoint converts your HTML file into a .master file with the same name.</span></span>
    
    <span data-ttu-id="b8aca-173">Теперь в компоненте "Дизайнер" для вашего HTML-файла отображается столбец "Состояние", в котором показано одно из двух возможных состояний:</span><span class="sxs-lookup"><span data-stu-id="b8aca-173">In Design Manager, your HTML file now appears with a Status column that shows one of two possible statuses:</span></span>
    
  - <span data-ttu-id="b8aca-174">**Предупреждения и ошибки**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-174">**Warnings and Errors**</span></span>
    
  
  - <span data-ttu-id="b8aca-175">**Преобразование выполнено успешно**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-175">**Conversion successful**</span></span>
    
  
7. <span data-ttu-id="b8aca-176">Перейдите по ссылке в столбце "Состояние" для предварительного просмотра файла, а также ошибок или предупреждений, касающихся эталонной страницы.</span><span class="sxs-lookup"><span data-stu-id="b8aca-176">Follow the link in the Status column to preview the file and to view any errors or warnings about the master page.</span></span>
    
    <span data-ttu-id="b8aca-p115">Страница предварительного просмотра — это страница динамического просмотра эталонной страницы на стороне сервера. Верхняя часть области предварительного просмотра отображает предупреждения или ошибки, которые необходимо устранить, изменив HTML-файл в редакторе HTML. Для того чтобы эталонная страница правильно отображалась во время предварительного просмотра, все ошибки должны быть устранены.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p115">The preview page is a live server-side preview of your master page. The top of the preview displays any warnings or errors that you may have to resolve by editing the HTML file in an HTML editor. Errors must be fixed before the preview will display the master page correctly.</span></span>
    
    <span data-ttu-id="b8aca-180">Дополнительные сведения об устранении ошибок и предупреждений см. в статье [Инструкции. Устранение ошибок и предупреждений во время предварительного просмотра страницы в SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-180">For more information about resolving errors and warnings, see  [How to: Resolve errors and warnings when previewing a page in SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md).</span></span>
    
    <span data-ttu-id="b8aca-181">Дополнительные сведения о предварительном просмотре эталонной страницы с различными страницами см. в статье [Инструкции. Изменение страницы предварительного просмотра в компоненте "Дизайнер" SharePoint](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-181">For more information about previewing the master page with different pages, see  [How to: Change the preview page in SharePoint Design Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span></span>
    
    <span data-ttu-id="b8aca-182">На странице предварительного просмотра также есть ссылка "Фрагменты кода" в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="b8aca-182">The preview page also contains a Snippets link in the upper-right corner.</span></span> <span data-ttu-id="b8aca-183">Эта ссылка ведет к коллекции фрагментов кода, где можно начать заменять статические или временные элементы управления в оформлении на динамические элементы управления SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8aca-183">This link opens the Snippet Gallery, where you can begin replacing static or mockup controls in your design with dynamic SharePoint controls.</span></span> <span data-ttu-id="b8aca-184">Дополнительные сведения см. в статье [Фрагменты кода в компоненте "Дизайнер" SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-184">For more information, see  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  
8. <span data-ttu-id="b8aca-p117">Чтобы устранить ошибки, с помощью HTML-редактора откройте и измените HTML-файл на подключенном диске на стороне сервера. Каждый раз при сохранении HTML-файла, все изменения синхронизируется со связанным MASTER-файлом.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p117">To fix any errors, edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in the mapped drive. Each time you save the HTML file, any changes are synced to the associated .master file.</span></span>
    
  
9. <span data-ttu-id="b8aca-187">После успешного предварительного просмотра эталонной страницы в HTML-файл будет добавлен тег **\<div\>**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-187">After your master page previews successfully, you will see a **\<div\>** tag that gets added to your HTML file.</span></span> <span data-ttu-id="b8aca-188">Возможно, чтобы увидеть тег **\<div\>**, потребуется прокрутить страницу вниз.</span><span class="sxs-lookup"><span data-stu-id="b8aca-188">You may have to scroll to the bottom of the page to see the **\<div\>** tag.</span></span>
    
    <span data-ttu-id="b8aca-189">Этот тег **\<div\>** является основным блоком контента.</span><span class="sxs-lookup"><span data-stu-id="b8aca-189">This **\<div\>** is the main content block.</span></span> <span data-ttu-id="b8aca-190">Он находится в заполнителе контента с именем **ContentPlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-190">It resides inside a content placeholder named **ContentPlaceHolderMain**.</span></span> <span data-ttu-id="b8aca-191">Во время выполнения, когда посетитель просматривает ваш сайт и запрашивает страницу, в этот заполнитель добавляется контент из макета страницы для соответствующей области содержимого.</span><span class="sxs-lookup"><span data-stu-id="b8aca-191">At run time, when a visitor browses your site and requests a page, this content placeholder gets filled with content from a page layout that contains content in a matching content region.</span></span> <span data-ttu-id="b8aca-192">Этот тег **\<div\>** следует поместить там, где должны отображаться макеты страниц на эталонной странице.</span><span class="sxs-lookup"><span data-stu-id="b8aca-192">You should position this **\<div\>** where you want your page layouts to appear on the master page.</span></span>
    
    <span data-ttu-id="b8aca-193">Если HTML-файл содержит статический или временный контент в основном тексте страницы, теперь начинается процесс удаления этого статического контента с эталонной HTML-страницы и применения этих стилей к другим элементам модели страниц SharePoint, например макетам страниц, полям страниц, фрагментам кода и шаблонам отображения.</span><span class="sxs-lookup"><span data-stu-id="b8aca-193">If your HTML file contains static or mockup content in the body of the page, now you begin the process of removing that static content from the HTML master page and applying those styles to other elements of the SharePoint page model, such as page layouts, page field controls, snippets, and display templates.</span></span> <span data-ttu-id="b8aca-194">Пример вы найдете в статье [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-194">For an example, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  

## <a name="understanding-the-html-file-after-conversion"></a><span data-ttu-id="b8aca-195">Общие сведения об HTML-файле после преобразования</span><span class="sxs-lookup"><span data-stu-id="b8aca-195">Understanding the HTML file after conversion</span></span>
<span data-ttu-id="b8aca-196"><a name="Understand"> </a></span><span class="sxs-lookup"><span data-stu-id="b8aca-196"><a name="Understand"> </a></span></span>

<span data-ttu-id="b8aca-p121">После преобразования HTML-файла в эталонную страницу в этот файл будет добавлено большое количество строк разметки. Вы можете не обращать внимания на большую ее часть, так как она не будет отображаться в конечной разметке вашего сайта при просмотре источника в браузере, однако эта разметка критична для преобразования вашего HTML-файла в MASTER-файл, который фактически используется SharePoint. Каждый раз при сохранении HTML-файла эта разметка SharePoint позволяет выполнить аналогичные изменения в связанном MASTER-файле в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p121">When you convert an HTML file into a master page, many lines of markup get added to your HTML file. You can safely ignore most of this markup, and most of it will not appear in the final markup of your site when you view source in the browser, but this markup is critical for converting your HTML file into the .master file that SharePoint actually uses. Each time you save a change to your HTML file, this SharePoint markup makes it possible for that same change to be made to the associated .master file in the background.</span></span>
  
    
    
<span data-ttu-id="b8aca-200">Добавляемая разметка включает теги, расположенные до тега **\<head\>** и в нем, фрагменты кода и заполнители контента.</span><span class="sxs-lookup"><span data-stu-id="b8aca-200">The markup that gets added includes tags before and in the **\<head\>** tag, snippets, and content placeholders.</span></span> <span data-ttu-id="b8aca-201">Большая часть разметки заключена в теги комментариев. Каждый раз при сохранении изменений в HTML-файле в процессе преобразования вырезаются комментарии, чтобы можно было использовать заключенную в них разметку ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b8aca-201">Most of the markup is enclosed within comment tags: Whenever you save a change to the HTML file, the conversion process strips out the comments to use the ASP.NET markup within.</span></span>
  
    
    

### <a name="types-of-markup"></a><span data-ttu-id="b8aca-202">Типы разметки</span><span class="sxs-lookup"><span data-stu-id="b8aca-202">Types of markup</span></span>

<span data-ttu-id="b8aca-203">Ниже представлены типы разметки, которые добавляются в HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-203">The following is a breakdown of the types of markup that are added to the HTML file:</span></span>
  
    
    

- <span data-ttu-id="b8aca-204">**Свойства документа.** Тег **\<mso\>** содержит метаданные SharePoint, в том числе сведения о самом файле и некоторые свойства, необходимые для успешного преобразования в MASTER-файл.</span><span class="sxs-lookup"><span data-stu-id="b8aca-204">**Document properties** The **\<mso\>** tag contains SharePoint metadata, including information about the file itself and some properties needed for the successful conversion to the .master file.</span></span>
    
```HTML
  
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
```

- <span data-ttu-id="b8aca-205">**Регистрация пространства имен SharePoint.** Тег **\<SPM\>** ("разметка SharePoint") содержит строку, регистрирующую пространство имен SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8aca-205">**SharePoint namespace registration** The **\<SPM\>** tag ("SharePoint markup") provides a line registering a SharePoint namespace.</span></span>
    
```HTML
  
<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

- <span data-ttu-id="b8aca-206">**Комментарии.** Теги **\<CS\>** и **\<CE\>** (начало и конец комментария) игнорируются во время преобразования.</span><span class="sxs-lookup"><span data-stu-id="b8aca-206">**Comments** The **\<CS\>** and **\<CE\>** ("Comment start" and "comment end") tags are ignored during the conversion process.</span></span> <span data-ttu-id="b8aca-207">Эти теги призваны помочь вам проанализировать строки разметки.</span><span class="sxs-lookup"><span data-stu-id="b8aca-207">These tags are to help you parse the lines of markup.</span></span>
    
```HTML
  
<!--CS: Start Page Head Contents Snippet-->
…
<!--CE: End Page Head Contents Snippet-->

  <!--CS: Start Ribbon Snippet-->
…
<!--CE: End Ribbon Snippet-->

<!--CS: Start PlaceHolderMain Snippet-->
…
<!--CE: End PlaceHolderMain Snippet-->
```

- <span data-ttu-id="b8aca-208">**Фрагменты кода.** Теги **\<MS\>** и **\<ME\>** (начало и конец разметки) обозначают начало и конец элемента управления SharePoint или фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="b8aca-208">**Snippets** The **\<MS\>** and **\<ME\>** ("markup start" and "markup end") tags denote the beginning and end of a SharePoint control or a snippet.</span></span> <span data-ttu-id="b8aca-209">Фрагмент кода — это элемент управления SharePoint, добавляющий функции SharePoint на страницу.</span><span class="sxs-lookup"><span data-stu-id="b8aca-209">A snippet is a SharePoint control that adds SharePoint functionality to your page.</span></span> <span data-ttu-id="b8aca-210">Вы можете добавлять их самостоятельно с помощью коллекции фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="b8aca-210">You can add snippets yourself by using the Snippet Gallery.</span></span> <span data-ttu-id="b8aca-211">Дополнительные сведения см. в статье [Фрагменты кода в компоненте "Дизайнер" SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="b8aca-211">For more information, see [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
```HTML
  
<!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
```

- <span data-ttu-id="b8aca-212">**Блоки предварительного просмотра**. Теги **\<PS\>** и **\<PE\>** (начало и конец предварительного просмотра) окружают раздел HTML-кода, который не следует редактировать, так как этот раздел влияет только на предварительный просмотр в ходе разработки.</span><span class="sxs-lookup"><span data-stu-id="b8aca-212">**Preview blocks** The **\<PS\>** and **\<PE\>** ("Preview start" and "preview end") tags surround a section of HTML code that you shouldn't edit because this section affects only the design-time preview.</span></span> <span data-ttu-id="b8aca-213">Эти разделы представляют собой моментальный снимок элемента управления SharePoint, вставляемого фрагментом кода.</span><span class="sxs-lookup"><span data-stu-id="b8aca-213">These preview sections are a snapshot in time of the SharePoint control that snippet is inserting.</span></span> <span data-ttu-id="b8aca-214">Предварительный просмотр помогает более осознанно работать с HTML-файлом в клиентском редакторе HTML.</span><span class="sxs-lookup"><span data-stu-id="b8aca-214">A preview makes it possible for you to work more meaningfully on the HTML file in a client-side HTML editor.</span></span> <span data-ttu-id="b8aca-215">Однако изменение контента или стилей для предварительного просмотра не окажет долговременного влияния на MASTER-файл, который в конечном итоге использует SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8aca-215">But, changing the content or styling within that preview has no lasting effect on the .master file, which is what SharePoint is ultimately using.</span></span> <span data-ttu-id="b8aca-216">Чтобы применить стиль к фрагменту кода, необходимо идентифицировать и переопределить стили SharePoint в пользовательской таблице CSS.</span><span class="sxs-lookup"><span data-stu-id="b8aca-216">To style a snippet, you have to identify and override the SharePoint styles with your own custom CSS.</span></span>
    
```HTML
  
<!--PS: Start of READ-ONLY PREVIEW (do not modify) -->
<div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div>
<!--PE: End of READ-ONLY PREVIEW -->
```

- <span data-ttu-id="b8aca-217">**Идентификаторы SharePoint**. С двумя фрагментами кода, добавляемыми в HTML-файл в ходе преобразования ("Содержимое заголовка страницы" и "Лента SharePoint"), связаны идентификаторы SharePoint или SID (00 и 02 соответственно).</span><span class="sxs-lookup"><span data-stu-id="b8aca-217">**SharePoint IDs** Two of the snippets added to your HTML file during the conversion (the Page Head Contents snippet and the SharePoint Ribbon) have an associated SharePoint ID, or SID (00 and 02, respectively).</span></span> <span data-ttu-id="b8aca-218">Эти идентификаторы позволяют сократить фрагменты кода и сделать HTML-код страницы более удобочитаемым.</span><span class="sxs-lookup"><span data-stu-id="b8aca-218">These IDs make it possible to shorten the snippets and make the HTML in the page easier to read.</span></span>
    
```HTML
  
<!--SID:00 -->

<!--SID:02 {Ribbon}-->
```


### <a name="added-snippets"></a><span data-ttu-id="b8aca-219">Добавленные фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="b8aca-219">Added snippets</span></span>

<span data-ttu-id="b8aca-p127">Важно знать о двух фрагментах кода, которые будут добавлены в HTML-файл. Эти фрагменты кода добавляются автоматически во время преобразования, но они могут быть недоступны для добавления из коллекции фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="b8aca-p127">It's important to know about two of the snippets that are added to your HTML file. These snippets are added automatically during the conversion, but they're not available for you to add from the Snippet Gallery.</span></span>
  
    
    

- <span data-ttu-id="b8aca-222">**Лента**. Чтобы авторы контента могли создавать страницы и контент на сайте SharePoint, эталонной странице необходимы лента и "навигация по набору" — новая функция SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b8aca-222">**The Ribbon** For content authors to be able to create pages and author content on your SharePoint site, your master page needs the ribbon and the "suite navigation" that is new to SharePoint.</span></span> <span data-ttu-id="b8aca-223">Лента содержится во фрагменте кода для фильтрации по ролям безопасности, поэтому когда посетитель просматривает сайт, лента видна только пользователям, прошедшим проверку подлинности, и не видна анонимным пользователям.</span><span class="sxs-lookup"><span data-stu-id="b8aca-223">The ribbon is contained in a security-trimming snippet, so that when a visitor browses your site, the ribbon is displayed only to authenticated users, not anonymous users.</span></span> <span data-ttu-id="b8aca-224">Вы можете переместить ленту в другое место страницы или стиля, переопределив стандартные классы CSS, но не рекомендуем перемещать и менять местами компоненты (например, меню "Действия сайта") на ленте.</span><span class="sxs-lookup"><span data-stu-id="b8aca-224">You can move the ribbon to a different position on the page or style it by overriding the default CSS classes, but we do not recommend moving or reordering the components (such as the Site Actions menu) that are contained inside the ribbon.</span></span>
    
```HTML
  
<!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
<!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
<!--ME:</wssucw:Welcome>-->
<!--ME:</SharePoint:SPSecurityTrimmedControl>-->
```

- <span data-ttu-id="b8aca-225">**ContentPlaceHolderMain**. В конце тега **\<div id="s4-bodyContainer"\>** (перед закрывающим тегом **\</body\>**) в ходе преобразования вставляется заполнитель контента с именем **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="b8aca-225">**ContentPlaceHolderMain** At the bottom of the **\<div id="s4-bodyContainer"\>** tag, before the closing **\</body\>** tag, the conversion process inserts a content placeholder named **PlaceHolderMain**.</span></span> <span data-ttu-id="b8aca-226">Внутри этого фрагмента находится желтый тег **\<div\>** с черными границами, который отображается в представлении конструктора в редакторе HTML или в окне предварительного просмотра на сервере в компоненте "Дизайнер".</span><span class="sxs-lookup"><span data-stu-id="b8aca-226">Inside this snippet is the black-bordered, yellow **\<div\>** that appears in the design view of your HTML editor, or in the server-side preview in Design Manager.</span></span>
    
    <span data-ttu-id="b8aca-227">Этот тег **\<div\>** представляет область, в которую будет добавлен контент, заданный макетами страниц и самими страницами.</span><span class="sxs-lookup"><span data-stu-id="b8aca-227">This **\<div\>** represents the area where the content specified by your page layouts and pages will go.</span></span> <span data-ttu-id="b8aca-228">Фрагмент **PlaceHolderMain** следует переместить в ту область эталонной страницы, которую заполнят макеты страниц, — область структуры сайта, которая отличается на разных страницах сайта.</span><span class="sxs-lookup"><span data-stu-id="b8aca-228">You should move the **PlaceHolderMain** snippet to the place within your master page that will be filled by your page layouts—the area of your site design that isn't the same across all pages of your site.</span></span>
    


```HTML
  
<!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
```


## <a name="reference-examples-of-sharepoint-markup-added-to-the-html-file"></a><span data-ttu-id="b8aca-229">Справочник. Примеры разметки SharePoint, добавленной в HTML-файл</span><span class="sxs-lookup"><span data-stu-id="b8aca-229">Reference: Examples of SharePoint markup added to the HTML file</span></span>
<span data-ttu-id="b8aca-230"><a name="Reference"> </a></span><span class="sxs-lookup"><span data-stu-id="b8aca-230"><a name="Reference"> </a></span></span>

<span data-ttu-id="b8aca-231">Ниже приведен пример разметки, добавленной в HTML-файл после его преобразования в эталонную страницу.</span><span class="sxs-lookup"><span data-stu-id="b8aca-231">The following is an example of markup added to an HTML file after it is converted to a master page.</span></span>
  
    
    

### <a name="markup-added-to-the-head-tag"></a><span data-ttu-id="b8aca-232">Разметка, добавленная в тег \<head\></span><span class="sxs-lookup"><span data-stu-id="b8aca-232">Markup added to the \<head\> tag</span></span>


```HTML

<head>
        <meta http-equiv="X-UA-Compatible" content="IE=10" />
        <!--CS: Start Page Head Contents Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SID:00 -->
        <meta name="GENERATOR" content="Microsoft SharePoint" />
        <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
        <meta http-equiv="Expires" content="0" />
        <!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--CE: End Page Head Contents Snippet-->
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <!--DC:Business Solutions-->
        <link rel="stylesheet" href="css/style.css" type="text/css" charset="utf-8" />
        <!--[if lte IE 7]>
  <link rel="stylesheet" href="css/ie.css" type="text/css" charset="utf-8"/> 
 <![endif]-->
        <!--[if gte mso 9]><xml>
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
</xml><![endif]-->
    </head>

```


### <a name="markup-added-after-the-start-body-tag"></a><span data-ttu-id="b8aca-233">Разметка, добавленная после открывающего тега \<body\></span><span class="sxs-lookup"><span data-stu-id="b8aca-233">Markup added after the start \<body\> tag</span></span>


#### <a name="ribbon-snippet"></a><span data-ttu-id="b8aca-234">Фрагмент кода ленты</span><span class="sxs-lookup"><span data-stu-id="b8aca-234">Ribbon snippet</span></span>


```HTML

<!--CS: Start Ribbon Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="wssucw" TagName="Welcome" Src="~/_controltemplates/15/Welcome.ascx"%>-->
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" HideFromSearchCrawler="true" EmitDiv="true">-->
            <div id="TurnOnAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOnAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(true);UpdateAccessibilityUI();document.getElementById('linkTurnOffAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnonaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
            <div id="TurnOffAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOffAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(false);UpdateAccessibilityUI();document.getElementById('linkTurnOnAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnoffaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <div id="ms-designer-ribbon">
            <!--SID:02 {Ribbon}-->
            <!--PS: Start of READ-ONLY PREVIEW (do not modify) --><div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div><!--PE: End of READ-ONLY PREVIEW -->
        </div>
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
            <!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
            <!--ME:</wssucw:Welcome>-->
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <!--CE: End Ribbon Snippet-->

```


#### <a name="two-sharepoint-div-tags"></a><span data-ttu-id="b8aca-235">Два тега \<div\> в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b8aca-235">Two SharePoint \<div\> tags</span></span>


```HTML

<div id="s4-workspace">
            <div id="s4-bodyContainer">

```


### <a name="markup-added-before-the-closing-body-tag-and-two-closing-div-tags"></a><span data-ttu-id="b8aca-236">Разметка, добавленная перед закрывающим тегом \</body\> и двумя закрывающими тегами \</div\></span><span class="sxs-lookup"><span data-stu-id="b8aca-236">Markup added before the closing \</body\> tag and two closing \</div\> tags</span></span>


```HTML

<div data-name="ContentPlaceHolderMain">
                    <!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
                </div>

```


## <a name="additional-resources"></a><span data-ttu-id="b8aca-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b8aca-237">Additional resources</span></span>
<span data-ttu-id="b8aca-238"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="b8aca-238"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="b8aca-239">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b8aca-239">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b8aca-240">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b8aca-240">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b8aca-241">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="b8aca-241">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

