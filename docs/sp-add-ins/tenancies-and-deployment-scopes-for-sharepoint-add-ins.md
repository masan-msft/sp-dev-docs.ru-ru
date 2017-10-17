---
title: "Области клиентов и области развертывания для надстроек SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9a2114067ed7782188a4efd91bfe26c709b0777e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="tenancies-and-deployment-scopes-for-sharepoint-add-ins"></a><span data-ttu-id="76cc3-102">Области клиентов и области развертывания для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="76cc3-102">Tenancies and deployment scopes for SharePoint Add-ins</span></span>
 <span data-ttu-id="76cc3-103">В этой статье рассказывается о концепции тенантностей и различиях между развертыванием надстроек SharePoint в области клиента и в веб-области.</span><span class="sxs-lookup"><span data-stu-id="76cc3-103">Learn about the concept of tenancies and the differences between deploying SharePoint Add-ins at tenant scope and web scope.</span></span>
 

 <span data-ttu-id="76cc3-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="76cc3-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="tenancies-and-add-in-scope"></a><span data-ttu-id="76cc3-107">Тенантности и область надстройки</span><span class="sxs-lookup"><span data-stu-id="76cc3-107">Tenancies and add-in scope</span></span>
<span data-ttu-id="76cc3-108"><a name="AppScope"> </a></span><span class="sxs-lookup"><span data-stu-id="76cc3-108"></span></span>

<span data-ttu-id="76cc3-p102">SharePoint Клиент это набор семейств веб-сайтов либо в ферме SharePoint, либо в SharePoint Online. В SharePoint Online семейства веб-сайтов относятся к отдельной учетной записи клиента. В ферме SharePoint в качестве семейств веб-сайтов могут выступать все семейства сайтов в веб-приложении SharePoint или их подмножество. Семейства сайтов могут также представлять собой набор семейств сайтов из различных веб-приложений в ферме. У клиента, как и у веб-приложения SharePoint, может быть каталог Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p102">A SharePoint tenancy is a set of site collections in either a SharePoint farm or in SharePoint Online. In SharePoint Online, the site collections belong to a single customer account. In a SharePoint farm, the site collections can be all the site collections in a SharePoint web application or a subset of them, or it can be a set of site collections from across multiple web applications in the farm. A tenancy can have a SharePoint Add-in add-in catalog just as a SharePoint web application can.</span></span>
 

 
<span data-ttu-id="76cc3-p103">Надстройка SharePoint имеет уровень надстройки. Два возможных уровня надстроек: уровень веб-сайтов иуровень клиента. Это различие не обусловлено внутренними свойствами надстройки, и вам, как разработчику, не нужно выбирать уровень установки надстройки. Решение принимается администраторами клиента и является побочным эффектом выбора способа установки. После отправки надстройки в каталог надстроек клиента она незамедлительно становится доступной для установки на каждом отдельном веб-сайте в рамках клиента. Надстройки, которые устанавливаются подобным образом, относятся к уровню веб-сайтов. Однако администраторы клиента могут выбрать другой вариант. Они могут выбрать пакетную установку надстройки в подмножестве веб-сайтов в рамках клиента. Надстройки, которые устанавливаются подобным образом, относятся к уровню клиента. Администратор клиента может указать, на какие веб-сайты устанавливается надстройка, с помощью списка управляемых путей, списка шаблонов сайтов или списка семейств веб-сайтов. Установленные пакетным способом надстройки может удалить только администратор клиента. Когда администратор клиента удаляет надстройку, она удаляется с каждого веб-сайта на уровне клиента. Пользователи не могут удалять надстройки, установленные пакетным способом, на отдельных веб-сайтах. Такой же принцип применяется и к обновлению такого надстройки: это может сделать только администратор клиента одновременно на всех веб-сайтах на уровне клиента, на которых установлена надстройка.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p103">A SharePoint Add-in has an add-in scope. The two possible add-in scopes are web scope ortenant scope. The difference is not an intrinsic property of the add-in, and you, the developer, do not decide what the scope of your add-in is. The decision is made by tenant administrators as a side effect of how the add-in is installed. After an add-in is uploaded to the add-in catalog of a tenancy, it is immediately available to be installed on websites within the tenancy on a website-by-website basis. Add-ins that are installed this way have web scope. Tenant administrators have another option, however. They can choose to batch install the add-in to a subset of websites within the tenancy. Add-ins that are installed in this way have tenant scope. The tenant admin can specify which websites the add-in is installed to by means of a list of managed paths, a list of site templates, or a list of site collections. An add-in that has been batch-installed can only be uninstalled by a tenant administrator. When the tenant admin uninstalls the add-in, it is uninstalled from every website in the tenancy. Users can't uninstall a batch-installed add-in on a website-by-website basis. The same principle applies to updating a batch-installed add-in: only a tenant administrator can do it, and it is batch-updated on every website in the tenancy where it is installed.</span></span>
 

 
<span data-ttu-id="76cc3-p104">Если надстройка, включающая сайт надстройки, устанавливается пакетным способом, создается только один сайт надстройки, совместно используемый всеми хост-сайтами, на которые устанавливается надстройка. Сайт надстройки размещается в семействе веб-сайтов каталога надстроек организации.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p104">If an add-in that includes an add-in web is batch-installed, only one add-in web is created and it is shared by all the host websites on which the add-in is installed. The add-in web is located in the site collection of the organization's add-in catalog.</span></span>
 

 
<span data-ttu-id="76cc3-129">При создании семейств веб-сайтов в тенантности надстройки, которые были установлены ранее в пакетном режиме, будут автоматически установлены в новом семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="76cc3-129">When new site collections are created in the tenancy, add-ins that were previously batch-installed are automatically installed on the new site collection.</span></span>
 

 

 <span data-ttu-id="76cc3-p105">**Примечание.** Не следует путать область надстройки с областью компонента. Область компонента определяет, где следует развертывать элементы в компоненте. Возможные варианты: **Farm** (Ферма), **WebApplication** (Веб-приложение), **Site** (Сайт, то есть семейство веб-сайтов) и **Web** (Интернет). Для компонентов (и для компонентов хост-сайта, и для компонентов в WSP-файле в пакете надстройки) в надстройках SharePoint разрешен только вариант **Web** (Интернет). Кроме того, не следует путать область надстройки с уровнями разрешений надстроек. Надстройки SharePoint могут запрашивать разрешения для всех или выбранных частей контента SharePoint на уровнях списка, Интернета, семейства веб-сайтов и тенантности. При установке надстройки с использованием области клиента надстройке не будут предоставлены разрешения, которые она не получила бы в другом случае. Кроме того, при этом не будут отменены ключевые положения модели безопасности SharePoint. Сведения о разрешениях для надстроек см. в статье [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="76cc3-p105">**Note**  Add-in scope should not be confused with Feature scope. Feature scope determines where the elements in a Feature are deployed. The possibilities include  **Farm**,  **WebApplication**,  **Site** (that is, site collection), and **Web**. Only  **Web** is permitted for Features in SharePoint Add-ins (both host web Features and Features inside a .wsp in an add-in package).Add-in scope should also not be confused with add-in permission levels. SharePoint Add-ins can request permissions to all or selected parts of SharePoint content at the levels of list, web, site collection, and tenancy. Installing an add-in with tenant scope does not give it permissions that it would not otherwise have, nor does it cancel key provisions of the SharePoint security model. For more information about add-in permissions, see  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
 


## <a name="limitations-of-tenant-scoped-add-ins"></a><span data-ttu-id="76cc3-137">Ограничения для надстроек области клиента</span><span class="sxs-lookup"><span data-stu-id="76cc3-137">Limitations of tenant-scoped add-ins</span></span>
<span data-ttu-id="76cc3-138"><a name="Tenant"> </a></span><span class="sxs-lookup"><span data-stu-id="76cc3-138"></span></span>

<span data-ttu-id="76cc3-139">Вам не удастся установить надстройки указанных ниже типов в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="76cc3-139">The following kinds of add-ins cannot be batch-installed:</span></span>
 

 

- <span data-ttu-id="76cc3-p106">Надстройки, которые содержат настраиваемое действие для ленты. (Разрешены настраиваемые действия, которые развертываются как пункты меню.)</span><span class="sxs-lookup"><span data-stu-id="76cc3-p106">Add-ins that contain a custom action for the ribbon. (Custom actions that are deployed as menu items are allowed.)</span></span>
    
 
- <span data-ttu-id="76cc3-142">Надстройки, которые содержат веб-часть надстройки.</span><span class="sxs-lookup"><span data-stu-id="76cc3-142">Add-ins that contain an add-in part.</span></span> 
    
 
<span data-ttu-id="76cc3-143">Кроме того, учтите, что установка на уровне клиента не поддерживается в версии SharePoint Online в Office 365 для малого бизнеса расширенный.</span><span class="sxs-lookup"><span data-stu-id="76cc3-143">In addition, note again that installation with tenant scope is not possible in the Office 365 Small Business Premium version of SharePoint Online.</span></span>
 

 

## <a name="how-to-install-uninstall-and-update-an-add-in-on-multiple-websites-in-a-tenancy"></a><span data-ttu-id="76cc3-144">Установка, удаление и обновление надстройки на нескольких веб-сайтах в тенантности</span><span class="sxs-lookup"><span data-stu-id="76cc3-144">How to install, uninstall, and update an add-in on multiple websites in a tenancy</span></span>
<span data-ttu-id="76cc3-145"><a name="Web"> </a></span><span class="sxs-lookup"><span data-stu-id="76cc3-145"></span></span>

<span data-ttu-id="76cc3-146">Независимо от того, устанавливается ли надстройка из Магазин Office или из каталога надстроек, администраторы клиента могут установить ее на нескольких веб-сайтах клиента, а также удалить и обновить ее с помощью следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="76cc3-146">Regardless of whether an add-in is installed from the Office Store or from an add-in catalog, tenant admins can install it to multiple websites in a tenancy, uninstall it, and update it by using the following procedures.</span></span>
 

 

### <a name="to-install-a-sharepoint-add-in-to-multiple-websites"></a><span data-ttu-id="76cc3-147">Установка надстройки SharePoint на нескольких веб-сайтах</span><span class="sxs-lookup"><span data-stu-id="76cc3-147">To install a SharePoint Add-in to multiple websites</span></span>


1. <span data-ttu-id="76cc3-148">Перейдите на страницу **Содержимое сайта** веб-сайта корпоративного каталога.</span><span class="sxs-lookup"><span data-stu-id="76cc3-148">Navigate to the  **Site Contents** page of the corporate catalog website.</span></span>
    
 
2. <span data-ttu-id="76cc3-149">Щелкните **Добавить надстройку** и установите надстройку так же, как и на любом другом веб-сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="76cc3-149">Select  **Add an add-in** and install the add-in just as you would on any other SharePoint website.</span></span>
    
 
3. <span data-ttu-id="76cc3-p107">После установки надстройки наведите указатель мыши на ссылку надстройки на странице **Содержимое сайта**. Отобразится ссылка **…**.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p107">After the add-in is installed, hover over the link to the add-in in the  **Site Contents** page. A " **...**" link appears.</span></span>
    
 
4. <span data-ttu-id="76cc3-152">Щелкните ссылку. Отобразится выноска.</span><span class="sxs-lookup"><span data-stu-id="76cc3-152">Select the link, and a callout appears.</span></span>
    
 
5. <span data-ttu-id="76cc3-153">В меню выберите пункт **Развертывание**.</span><span class="sxs-lookup"><span data-stu-id="76cc3-153">Select  **Deployment** on the menu.</span></span>
    
 
6. <span data-ttu-id="76cc3-p108">Используйте открывшийся интерфейс развертывания для указания семейств веб-сайтов, в которых необходимо установить надстройку. Можно выполнять фильтрацию по управляемым путям, шаблонам сайтов и URL-адресам. Для фильтров действует логическое отношение "ИЛИ": надстройка устанавливается во всех семействах веб-сайтов, которые проходят один или больше фильтров.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p108">Use the deployment UI that opens to specify the site collections to which you want the add-in installed. You can filter by managed paths, site templates, or URLs. The filters have a logical "OR" relationship: the add-in is installed to the union of all the site collections that pass any one or more of the filters.</span></span>
    
 
7. <span data-ttu-id="76cc3-157">Нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="76cc3-157">Select  **OK**.</span></span>
    
 

### <a name="to-uninstall-a-batch-installed-sharepoint-add-in"></a><span data-ttu-id="76cc3-158">Удаление надстройки SharePoint, установленной в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="76cc3-158">To uninstall a batch-installed SharePoint Add-in</span></span>


1. <span data-ttu-id="76cc3-159">Перейдите на страницу **Содержимое сайта** веб-сайта корпоративного каталога.</span><span class="sxs-lookup"><span data-stu-id="76cc3-159">Navigate to the  **Site Contents** page of the corporate catalog website.</span></span>
    
 
2. <span data-ttu-id="76cc3-p109">Наведите указатель мыши на ссылку надстройки на странице **Содержимое сайта**. Отобразится ссылка **…**.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p109">Hover over the link to the add-in in the  **Site Contents** page. A " **...**" link appears.</span></span>
    
 
3. <span data-ttu-id="76cc3-162">Щелкните ссылку. Отобразится выноска.</span><span class="sxs-lookup"><span data-stu-id="76cc3-162">Select the link, and a callout appears.</span></span>
    
 
4. <span data-ttu-id="76cc3-163">В выноске нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="76cc3-163">Select  **Remove** on the callout.</span></span>
    
 

### <a name="to-update-a-batch-installed-sharepoint-add-in"></a><span data-ttu-id="76cc3-164">Обновление надстройки SharePoint, установленной в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="76cc3-164">To update a batch-installed SharePoint Add-in</span></span>


1. <span data-ttu-id="76cc3-p110">Перейдите на страницу **Содержимое сайта** веб-сайта корпоративного каталога. Если для надстройки доступно обновление, возле нее появится сообщение с соответствующей ссылкой.</span><span class="sxs-lookup"><span data-stu-id="76cc3-p110">Navigate to the  **Site Contents** page of the corporate catalog website. If there is an update available for an add-in, a message appears beside the add-in. There will be a link to update the add-in.</span></span>
    
 
2. <span data-ttu-id="76cc3-168">Щелкните ссылку, чтобы обновить надстройку.</span><span class="sxs-lookup"><span data-stu-id="76cc3-168">Click the link to update the add-in.</span></span>
    
 
3. <span data-ttu-id="76cc3-169">Когда вам будет предложено утвердить запросы на разрешения для надстройки, щелкните **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="76cc3-169">When you are prompted to approve the permission requests of the add-in, choose  **Trust It**.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="76cc3-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="76cc3-170">Additional resources</span></span>
<span data-ttu-id="76cc3-171"><a name="SP15tenancies_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="76cc3-171"></span></span>


-  [<span data-ttu-id="76cc3-172">Публикация надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="76cc3-172">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="76cc3-173">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="76cc3-173">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 
-  [<span data-ttu-id="76cc3-174">Развертывание и установка надстроек SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="76cc3-174">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options.md)
    
 
-  [<span data-ttu-id="76cc3-175">Процесс обновления надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="76cc3-175">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process.md)
    
 

