---
title: "Добавить фрагмент Trim безопасности в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4beaab08-760b-408a-b768-906312779379
ms.openlocfilehash: e238143422a472ff25922a2b409980176710a439
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-security-trim-snippet-in-sharepoint"></a><span data-ttu-id="d452c-102">Добавить фрагмент Trim безопасности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d452c-102">Add a Security Trim snippet in SharePoint</span></span>

<span data-ttu-id="d452c-103">Вы можете использовать фрагмент фильтрации по ролям безопасности, чтобы отображать контент только для указанных пользователей, имеющих специальное разрешение и прошедших или не прошедших (анонимные пользователи) проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d452c-103">You can use a Security Trim snippet to display content only to specific users, based on a specific permission that those users must have and whether the users are authenticated or anonymous.</span></span>

## <a name="introduction-to-the-security-trim-snippet"></a><span data-ttu-id="d452c-104">Общие сведения о фрагменте Trim безопасности</span><span class="sxs-lookup"><span data-stu-id="d452c-104">Introduction to the Security Trim snippet</span></span>
<span data-ttu-id="d452c-105"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="d452c-105"></span></span>

<span data-ttu-id="d452c-p101">Фрагмент Trim безопасности можно использовать для отображения содержимого только для конкретных пользователей, на основании конкретные разрешения, эти пользователи должны иметь, и являются ли тех пользователей, прошедших проверку подлинности или анонимного. Панель Trim безопасности можно добавить к главной странице или макету страницы. Панель Trim безопасности является контейнером, который может содержать другие компоненты или в дополнение к статического содержимого фрагменты кода, например веб-части.</span><span class="sxs-lookup"><span data-stu-id="d452c-p101">You can use a Security Trim snippet to display content only to specific users, based on a specific permission that those users must have, and whether those users are authenticated or anonymous. You can add a Security Trim panel to a master page or page layout. A Security Trim panel is a container that can include other components or snippets, such as Web Parts, in addition to static content.</span></span>
  
    
    
<span data-ttu-id="d452c-109">К примеру можно использовать панель Trim безопасности должно отображаться следующее содержимое для конкретных пользователей:</span><span class="sxs-lookup"><span data-stu-id="d452c-109">For example, you can use a Security Trim panel to display the following content to specific users:</span></span>
  
    
    

- <span data-ttu-id="d452c-110">Контент по веб-части поиска, которое отображает документы пользователя с разрешением в настоящее время работает в.</span><span class="sxs-lookup"><span data-stu-id="d452c-110">A Content by Search Web Part that displays which documents an authenticated user is currently working on.</span></span>
    
  
- <span data-ttu-id="d452c-111">Недавно измененные документов представления списка, таким образом, прошедшего проверку подлинности пользователи могут просматривать новые возможности на сайте.</span><span class="sxs-lookup"><span data-stu-id="d452c-111">A list view of recently modified documents so that authenticated users can see what's new on the site.</span></span>
    
  
- <span data-ttu-id="d452c-p102">Контент по веб-части поиска, который отображает список посетителей без проверки подлинности рекомендуется ссылок на основании текущей статьи. Список рекомендаций по использованию может быть помех для прошедшего проверку подлинности контента авторов, работающих на сайте, но не важно для посетителей, не прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d452c-p102">A Content by Search Web Part that displays to non-authenticated visitors a list of recommended links based on the current article. Such a list of recommendations might be noise to authenticated content authors working in the site, but it's important for non-authenticated visitors.</span></span>
    
  
- <span data-ttu-id="d452c-114">Вход ссылка отдельно от ленты, не прошедшим проверку подлинности или пользователей, которые еще не проходить проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d452c-114">A sign-in link separate from the ribbon, for non-authenticated users or users who have yet to be authenticated.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d452c-115">В этом ссылку входа автоматически вставляется в главную страницу, которая создается с помощью Дизайнера, но его можно удалить, если не требуется.</span><span class="sxs-lookup"><span data-stu-id="d452c-115">This sign-in link is inserted automatically into a master page that is created by using Design Manager, but you can delete it if it's not needed.</span></span> 

<span data-ttu-id="d452c-116">Панель Trim безопасности имеет два важных свойств: для проверки подлинности и для разрешения (или авторизации).</span><span class="sxs-lookup"><span data-stu-id="d452c-116">A Security Trim panel has two important property settings, one for authentication and one for permissions (or authorization).</span></span> <span data-ttu-id="d452c-117">К примеру можно использовать панель Trim безопасности должно отображаться следующее содержимое для конкретных пользователей:</span><span class="sxs-lookup"><span data-stu-id="d452c-117">For example, you can use a Security Trim panel to display the following content to specific users:</span></span>
  
    
    

- <span data-ttu-id="d452c-118">**AuthenticationRestrictions** С помощью этого свойства можно ограничить панели прошедшего проверку подлинности либо анонимным пользователям, или выберите всех пользователей (все пользователи по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="d452c-118">**AuthenticationRestrictions** With this property, you can restrict the panel to either authenticated or anonymous users, or choose all users (all users is the default setting).</span></span>
    
  
- <span data-ttu-id="d452c-119">**Разрешения** С помощью этого свойства можно выбрать определенное разрешение, которое необходимо пользователям для просмотра содержимого панели.</span><span class="sxs-lookup"><span data-stu-id="d452c-119">**Permissions** With this property, you can select a specific permission that users must have to view the content in the panel.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="d452c-120">Вы выбираете отдельных разрешений, не уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="d452c-120">You are selecting an individual permission, not a permission level.</span></span> <span data-ttu-id="d452c-121">(Уровень разрешений — это набор предоставленных разрешений). Конечно Если проверка подлинности только анонимным пользователям, не обычно необходимо указать определенное разрешение, так как анонимные пользователи не обычно были указаны все разрешения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d452c-121">(A permission level is a set of granted permissions.) Of course, if you restrict the authentication to only anonymous users, it's typically not necessary to specify a specific permission because anonymous users have usually not been given any SharePoint permissions.</span></span> <span data-ttu-id="d452c-122">Это имеет смысл использовать разрешения только с всем пользователям или всем прошедшим проверку подлинности пользователям.</span><span class="sxs-lookup"><span data-stu-id="d452c-122">It makes sense to use permissions only with all users or with all authenticated users.</span></span>
  
    
    
<span data-ttu-id="d452c-p105">На панели безопасности Trim имеется три варианта на ленте, перечисленные в столбце слева в таблице 1. В таблице 1 показано, как эти параметры определить конкретные разрешения, необходимые для пользователей, низкий уровень разрешений по умолчанию, которая включает в себя этого определенные разрешения и группы, которая связана этот уровень разрешений по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="d452c-p105">The Security Trim panel has three options on the ribbon, listed in the left column of Table 1. Table 1 shows how these settings determine the specific permission that users are required to have, the lowest default permission level that includes that specific permission, and the group that is linked to that permission level by default.)</span></span>
  
> [!NOTE]
> <span data-ttu-id="d452c-125">[!Примечание] Далее представлены параметры по умолчанию, которые могут быть изменены для любой заданной области действия, такие как семейства веб-сайтов, сайта, списка или элемента.</span><span class="sxs-lookup"><span data-stu-id="d452c-125">These are the default settings, which can be changed for any given scope, such as a site collection, site, list, or item.</span></span> 
  
    
    

<span data-ttu-id="d452c-126">К примеру Если панель Trim безопасности для **отображения для авторов**, с содержимым по умолчанию в этой панели отображается для пользователей в группе элементы и группы "Владельцы".</span><span class="sxs-lookup"><span data-stu-id="d452c-126">For example, if you set a Security Trim panel to **Show to authors**, by default content inside that panel is visible to users in the Members group and the Owners group.</span></span>
  
    
    

<span data-ttu-id="d452c-127">**В таблице 1. Сопоставление параметры панели уровни разрешений по умолчанию и группам**</span><span class="sxs-lookup"><span data-stu-id="d452c-127">**Table 1. Mapping of panel options to default permission levels and groups**</span></span>


|<span data-ttu-id="d452c-128">**Параметр удаления панели безопасности**</span><span class="sxs-lookup"><span data-stu-id="d452c-128">**Security Trim panel option**</span></span>|<span data-ttu-id="d452c-129">**Свойство разрешения**</span><span class="sxs-lookup"><span data-stu-id="d452c-129">**Permissions property**</span></span>|<span data-ttu-id="d452c-130">**Разрешение**</span><span class="sxs-lookup"><span data-stu-id="d452c-130">**Permission**</span></span>|<span data-ttu-id="d452c-131">**Уровень разрешений**</span><span class="sxs-lookup"><span data-stu-id="d452c-131">**Permission level**</span></span>|<span data-ttu-id="d452c-132">**Группа**</span><span class="sxs-lookup"><span data-stu-id="d452c-132">**Group**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d452c-133">Показать авторов</span><span class="sxs-lookup"><span data-stu-id="d452c-133">Show to authors</span></span>  <br/> |<span data-ttu-id="d452c-134">**AddAndCustomizePages**</span><span class="sxs-lookup"><span data-stu-id="d452c-134">**AddAndCustomizePages**</span></span> <br/> |<span data-ttu-id="d452c-135">Добавление и настройка страниц</span><span class="sxs-lookup"><span data-stu-id="d452c-135">Add and Customize Pages</span></span>  <br/> |<span data-ttu-id="d452c-136">Contribute (или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="d452c-136">Contribute (or higher)</span></span>  <br/> |<span data-ttu-id="d452c-137">Элементы</span><span class="sxs-lookup"><span data-stu-id="d452c-137">Members</span></span>  <br/> |
|<span data-ttu-id="d452c-138">Отображать для пользователей, прошедших проверку</span><span class="sxs-lookup"><span data-stu-id="d452c-138">Show to Authenticated Users</span></span>  <br/> |<span data-ttu-id="d452c-139">**ViewPages**</span><span class="sxs-lookup"><span data-stu-id="d452c-139">**ViewPages**</span></span> <br/> |<span data-ttu-id="d452c-140">Просмотр страниц</span><span class="sxs-lookup"><span data-stu-id="d452c-140">View Pages</span></span>  <br/> |<span data-ttu-id="d452c-141">Read (или выше)</span><span class="sxs-lookup"><span data-stu-id="d452c-141">Read (or higher)</span></span>  <br/> |<span data-ttu-id="d452c-142">Посетители</span><span class="sxs-lookup"><span data-stu-id="d452c-142">Visitors</span></span>  <br/> |
|<span data-ttu-id="d452c-143">Показать для администраторов</span><span class="sxs-lookup"><span data-stu-id="d452c-143">Show to Administrators</span></span>  <br/> |<span data-ttu-id="d452c-144">**FullMask**</span><span class="sxs-lookup"><span data-stu-id="d452c-144">**FullMask**</span></span> <br/> |<span data-ttu-id="d452c-145">Выделить все</span><span class="sxs-lookup"><span data-stu-id="d452c-145">Select All</span></span>  <br/> |<span data-ttu-id="d452c-146">Полный доступ</span><span class="sxs-lookup"><span data-stu-id="d452c-146">Full Control</span></span>  <br/> |<span data-ttu-id="d452c-147">Владельцы</span><span class="sxs-lookup"><span data-stu-id="d452c-147">Owners</span></span>  <br/> |
   

### <a name="inserting-a-security-trim-panel"></a><span data-ttu-id="d452c-148">Вставка панели Trim безопасности</span><span class="sxs-lookup"><span data-stu-id="d452c-148">Inserting a Security Trim panel</span></span>
<span data-ttu-id="d452c-149"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="d452c-149"></span></span>

<span data-ttu-id="d452c-p106">Как все фрагменты кода добавьте фрагмент Trim безопасности из коллекция фрагментов кода. Чтобы перейти к коллекция фрагментов кода, сначала нужно выбрать главную страницу или макет страницы для редактирования.</span><span class="sxs-lookup"><span data-stu-id="d452c-p106">Like all snippets, you add the Security Trim snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-a-security-trim-panel"></a><span data-ttu-id="d452c-152">Чтобы вставить панель Trim безопасности</span><span class="sxs-lookup"><span data-stu-id="d452c-152">To insert a Security Trim panel</span></span>


1. <span data-ttu-id="d452c-153">Откройте свой сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="d452c-153">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="d452c-154">Нажмите значок шестеренки "Параметры" в правом верхнем углу страницы, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="d452c-154">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="d452c-155">В диспетчере оформления на левой панели навигации слева выберите **Изменить главную страницу** или **Изменение макетов страниц**, в зависимости от того, какой тип файла требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="d452c-155">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="d452c-156">Выберите имя главной страницы или макет страницы, который вы хотите добавить фрагмент для.</span><span class="sxs-lookup"><span data-stu-id="d452c-156">Select the name of the master page or page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="d452c-157">Чтобы открыть коллекцию фрагментов, выберите **Фрагменты** в правом верхнем углу страницы предварительного просмотра на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d452c-157">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="d452c-158">На ленте перейдите на вкладку **Конструктор** нажмите кнопку **Обрезать безопасности**.</span><span class="sxs-lookup"><span data-stu-id="d452c-158">On the ribbon, on the **Design** tab, choose **Security Trim**.</span></span>
    
    <span data-ttu-id="d452c-159">Кроме того в раскрывающемся списке на кнопке **Trim безопасности**, можно выбрать пользователей, которым будет отображаться содержимого панели или можно увидеть дополнительные параметры, настроив значения важных свойств для панели.</span><span class="sxs-lookup"><span data-stu-id="d452c-159">Optionally, in the drop-down list on the **Security Trim** button, you can select the users to whom the panel content will be visible, or you can see more options by configuring the important property values for the panel.</span></span>
    
  
7. <span data-ttu-id="d452c-160">В разделе **Об этом компоненте** в правой части коллекции фрагментов щелкните или выберите заголовок раздела, чтобы развернуть или свернуть группу свойств, а затем настройте все нужные настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="d452c-160">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
  
8. <span data-ttu-id="d452c-p107">Настроив свойства, нажмите **Обновить**. При этом обновляется фрагмент HTML в левой части страницы, чтобы разметка отражала настраиваемые параметры. Вы всегда можете нажать кнопку **Сбросить**, чтобы восстановить исходные значения всех свойств.</span><span class="sxs-lookup"><span data-stu-id="d452c-p107">After you configure any properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="d452c-164">В разделе **Фрагмент HTML** в левой части коллекции фрагментов выберите команду **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="d452c-164">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="d452c-165">В редакторе HTML откройте сопоставленный сетевой диск на своем компьютере, а затем откройте HTML-файл для эталонной страницы или макета, к которым добавляется фрагмент.</span><span class="sxs-lookup"><span data-stu-id="d452c-165">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
  
11. <span data-ttu-id="d452c-166">Вставьте фрагмент в том месте HTML-файла, где должна отображаться разметка.</span><span class="sxs-lookup"><span data-stu-id="d452c-166">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="d452c-167">При добавлении фрагмента в макет страниц, убедитесь в том вставить фрагмент внутри **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="d452c-167">If you are adding the snippet to a page layout, make sure to paste the snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="d452c-168">Замените **<div>** в разделе `class="DefaultContentBlock"` собственным контентом.</span><span class="sxs-lookup"><span data-stu-id="d452c-168">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content.</span></span>
    
  
13. <span data-ttu-id="d452c-169">Сохраните страницу и затем обновить на сервере предварительного просмотра в диспетчере оформления, чтобы убедиться в том, что панель безопасности сократить отображается должным.</span><span class="sxs-lookup"><span data-stu-id="d452c-169">Save the page, and then refresh the server-side preview in Design Manager to make sure the Security Trim panel appears as expected.</span></span>
    
  

## <a name="understanding-the-snippet-markup"></a><span data-ttu-id="d452c-170">Сведения о разметке фрагментов</span><span class="sxs-lookup"><span data-stu-id="d452c-170">Understanding the snippet markup</span></span>
<span data-ttu-id="d452c-171"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="d452c-171"></span></span>

<span data-ttu-id="d452c-p108">Наиболее важные части фрагмента Trim безопасности  это свойство **AuthenticationRestrictions** и свойство **Permissions** и **<div>** полужирным шрифтом ниже. **AuthenticationRestrictions** появится в разметке только в том случае, если изменено с **AllUsers**, которая используется по умолчанию. Если выбран **перезапуск** для фрагмента в коллекция фрагментов кода **AuthenticationRestrictions** удаляется из разметка, которая означает, что в фрагменте используется значение по умолчанию **AllUsers**.</span><span class="sxs-lookup"><span data-stu-id="d452c-p108">The most important parts of a Security Trim snippet are the **AuthenticationRestrictions** property and the **Permissions** property, and the **<div>** in bold below. **AuthenticationRestrictions** appears in the markup only when changed from **AllUsers**, which is the default. If you choose **Reset** for the snippet in the Snippet Gallery, **AuthenticationRestrictions** is removed from the markup, which means the snippet uses the default value, **AllUsers**.</span></span>
  
    
    
<span data-ttu-id="d452c-175">**<div>**, где `class="DefaultContentBlock"`  заменить на собственный текст, который может содержать другие фрагменты кода и элементов управления.</span><span class="sxs-lookup"><span data-stu-id="d452c-175">The **<div>** where `class="DefaultContentBlock"` is what you replace with your own content, which can include other snippets and controls.</span></span>
  
    
    



```HTML

<div data-name="SecurityTrimmedAuthors">
    <!--CS: Start Security Trim Snippet-->
    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AuthenticatedUsersOnly" Permissions="AddAndCustomizePages" PermissionContext="RootSite">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><span><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Security Trim Properties.
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--></span><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
    <!--CE: End Security Trim Snippet-->
</div>
```


## <a name="see-also"></a><span data-ttu-id="d452c-176">См. также</span><span class="sxs-lookup"><span data-stu-id="d452c-176">See also</span></span>
<span data-ttu-id="d452c-177"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="d452c-177"></span></span>


-  [<span data-ttu-id="d452c-178">Введение: управление доступом пользователей с разрешениями</span><span class="sxs-lookup"><span data-stu-id="d452c-178">Introduction: Control user access with permissions</span></span>](http://office.microsoft.com/en-us/sharepoint-foundation-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=1)
    
  
-  [<span data-ttu-id="d452c-179">Общие сведения об уровнях разрешений</span><span class="sxs-lookup"><span data-stu-id="d452c-179">Understanding permission levels</span></span>](http://office.microsoft.com/en-us/products/default-permission-levels-HA102772313.aspx?CTT=5&amp;origin=HA102771919)
    
  
-  [<span data-ttu-id="d452c-180">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="d452c-180">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="d452c-181">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d452c-181">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="d452c-182">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d452c-182">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

