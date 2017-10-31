---
title: "Изучение структуры манифеста приложения и пакета надстройки SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: d178c11ac3cfaa0d53f8517bfa3fa7da21a354c2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in"></a><span data-ttu-id="1b36e-102">Изучение структуры манифеста приложения и пакета надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b36e-102">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>
<span data-ttu-id="1b36e-103">В этой статье рассказывается о структуре пакета надстройки и файле манифеста для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1b36e-103">Learn about the add-in package structure and the manifest file for a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="1b36e-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="add-in-for-sharepoint-package-structure"></a><span data-ttu-id="1b36e-107">Структура пакета надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b36e-107">Add-in for SharePoint package structure</span></span>
<span data-ttu-id="1b36e-108"><a name="Package"> </a></span><span class="sxs-lookup"><span data-stu-id="1b36e-108"><a name="Package"> </a></span></span>

<span data-ttu-id="1b36e-p102">Пакет надстройки SharePoint это файл с расширением APP, который соответствует  [новому стандарту упаковки данных (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx). Пакет содержит следующие элементы.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p102">A SharePoint Add-in package is a file that has an ".app" extension and that complies with the  [Open Packaging Conventions (OPC)](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx). The package contains the following items:</span></span>
 

 

-  <span data-ttu-id="1b36e-p103">**Манифест надстройки.** Это обязательный файл с именем appmanifest.xml. Он сообщает SharePoint некоторые важные свойства надстройки, такие как название и необходимые для запуска разрешения. Дополнительные сведения о содержимом этого файла можно найти в разделе [Файл манифеста надстройки для SharePoint](#AppManifest).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p103">**Add-in manifest:** This is a required file that is named appmanifest.xml. It tells SharePoint about some important properties of the add-in, such as its title and the permissions it needs to run. For more information about the contents of this file, see [Add-in for SharePoint manifest file](#AppManifest).</span></span>
    
 
-  <span data-ttu-id="1b36e-p104">**Пакеты решений SharePoint.** Надстройка может дополнительно включать пакет решений SharePoint (WSP-файл), содержащий компоненты сайта надстройки. Эти компоненты могут включать страницы, экземпляры списков, представления, документы, компоненты на уровне **Web** и другие компоненты SharePoint. (Дополнительные сведения о том, какие компоненты SharePoint могут быть включены в надстройку SharePoint, можно найти в статье [Типы компонентов SharePoint, которые могут находиться в надстройке для SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).) WSP-файл может также содержать Надстройки Office. Компоненты из WSP-файла разворачиваются на сайте надстройки. Пример пакета надстройки, включающего пакет решений SharePoint, можно найти в статье  [Создание надстроек с размещением у поставщика, которые включают в себя пользовательский список SharePoint и тип контента](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p104">**SharePoint Solution Packages:** Optionally, the add-in may include a SharePoint solution package (.wsp file) that contains the components of the add-in web. These components may include pages, list instances, views, documents, **Web**-scoped Features, and other SharePoint components. (For more information about what SharePoint components can be included in a SharePoint Add-in, see  [Types of SharePoint components that can be in a SharePoint Add-in](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#TypesOfSPComponentsInApps).) The .wsp file may also contain Office Add-ins. The components in the .wsp file are deployed to the add-in web. For an example of an add-in package that includes a SharePoint solution package, see  [Create a provider-hosted add-in that includes a custom SharePoint list and content type](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span></span>
    
 
-  <span data-ttu-id="1b36e-p105">**Компоненты хост-сайта с дополнительными действиями или веб-частями надстройки.** В дополнение к компонентам SharePoint, которые разворачиваются на сайте надстройки, Надстройка SharePoint может также разворачивать одно или несколько дополнительных действий (элементов контекстного меню или расширений ленты) на хост-сайте. Это выполняется путем включения в пакет надстройки компонента, не входящего в WSP-файл пакета и разворачивающего компоненты, которые попадут на хост-сайт. Этот "свободный" компонент называется компонентом хост-сайта. Веб-части надстройки разворачиваются на хост-сайте таким же образом. Компонент хост-сайта состоит из стандартного файла SharePoint feature.xml и одного или нескольких связанных файлов elements.xml. Например, файл elements.xml для дополнительного действия содержит разметку **CustomAction** для этого действия. Он также может включать разметку для веб-частей надстройки. В компоненте хост-сайта могут быть только эти два вида компонентов. Такие компоненты хост-сайта не перечисляются в манифесте надстройки. Однако они являются "частями" в контексте OPC, и существует явное отношение OPC между манифестом надстройки и каждым из этих файлов. Пример пакета надстройки, в котором имеется компонент хост-сайта, можно найти в статье [Выполнение пользовательских действий для развертывания надстроек для SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p105">**Host web Features with Custom Actions or add-in parts:** In addition to the SharePoint components that are deployed to the add-in web, a SharePoint Add-in can also deploy one or more custom actions (shortcut menu items or ribbon extensions) to the host web. This is accomplished by including in the add-in package a Feature that is not inside the package's .wsp file and that deploys the components that will go to the host web. This "loose" Feature is called a host web Feature. Add-in parts are deployed to the host web in the same way. The host web Feature consists of a standard SharePoint feature.xml file and one or more associated elements.xml files. An elements.xml file for a custom action, for example, contains the **CustomAction** markup for the custom action. It can also include markup for add-in parts. Only these two kinds of components can be in the host web Feature. These host web Features are not itemized in the add-in manifest. However, they are "parts" in the OPC sense, and there is an explicit OPC relationship between the add-in manifest and each of these files. For an example of an add-in package that includes a host web Feature, see [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
    
     <span data-ttu-id="1b36e-p106">**Примечание.** Администраторы клиента могут выполнять пакетную установку надстройки SharePoint на несколько веб-сайтов. Надстройка, установленная таким образом, называется надстройкой уровня **Tenant** (Клиент). Если надстройка устанавливается не в пакетном режиме, а отдельно на каждый веб-сайт, то это надстройка уровня **Web** (Интернет). Если компонент хост-сайта включает расширения ленты или части надстройки, то при пакетной установке надстройки они не развертываются на хост-сайтах, так что только элементы контекстного меню развертываются с надстройками на уровне клиента. Уровень надстройки не должен конфликтовать с уровнем компонента. Уровень компонента определяет, где следует развертывать элементы компонента. Возможные уровни: **Farm** (Ферма), **WebApplication** (Веб-приложение), **Site** (Сайт, т. е. семейство веб-сайтов) и **Web** (Интернет). Для компонентов в надстройках SharePoint (как компонентов хост-сайта, так и компонентов в WSP-файле пакета надстройки) разрешен только вариант **Web** (Интернет). Уровень надстройки относится к уровню, на котором установлена надстройка. Возможные уровни: **Web** (Интернет), когда надстройка установлена на одном или нескольких веб-сайтах по очереди, и **Tenant** (Клиент), когда надстройка установлена в пакетном режиме на несколько веб-сайтов в тенантности пользователя. Дополнительные сведения об уровнях **Tenant** (Клиент) и **Web** (Интернет) см. в статье [Тенантности и области развертывания для надстроек SharePoint](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p106">**Note**  Tenant administrators have the option to batch-install a SharePoint Add-in to multiple websites. An add-in that has been installed in this way is said to have  **Tenant** scope. If the add-in has not been batch-installed, and is instead installed to each website separately, it has **Web** scope. If the host web Feature includes ribbon extensions or add-in parts, they are not deployed to the host webs if the add-in is batch-installed, so only shortcut menu items are deployed with Tenant-scoped add-ins. Add-in scope should not be confused with Feature scope. Feature scope determines where the elements in a Feature are deployed. The possibilities are **Farm**,  **WebApplication**,  **Site** (that is, site collection), and **Web**. Only the  **Web** option is permitted for Features in SharePoint Add-ins (both host web Features and Features inside a .wsp in an add-in package). Add-in scope refers to the scope at which an add-in is installed. The possibilities are **Web**, in which case the add-in has been installed to one or more websites site-by-site, and  **Tenant**, in which case the add-in has been batch installed to all or some subset of the websites in a customer's tenancy. For more information about  **Tenant** and **Web** scope, see [Tenancies and deployment scopes for SharePoint Add-ins](tenancies-and-deployment-scopes-for-sharepoint-add-ins.md).</span></span>
-  <span data-ttu-id="1b36e-p107">**Файлы ресурсов (RESX-файлы) для локализации.** Это составляющие манифеста надстройки для локализации, которые включают название надстройки и составляющие компонентов хост-сайта в пакете надстройки. (Отдельные части пакета надстройки, находящиеся внутри собственных пакетов, таких как WSP-файлы, пакеты Веб-сайты Azure и манифесты надстройка, имеют свои собственные процессы локализации, которые применяются точно так же, как если бы элементы, о которых идет речь, не были частью надстройки SharePoint.) Пример пакета надстройки, содержащего RESX-файлы для компонента хост-сайта, можно найти в статье [Локализация надстроек для SharePoint](localize-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p107">**Localization resource files (.resx):** These are for localizing aspects of the add-in manifest that include the add-in title and aspects of host web Features in the add-in package. (Individual parts of the add-in package that are inside their own package, such as .wsp files, Azure Web Sites packages, and add-in manifests, each have their own localization processes that are applied exactly as they would be if the items in question were not part of a SharePoint Add-in.) For an example of an add-in package that includes .resx files for a host web Feature, see [Localize SharePoint Add-ins](localize-sharepoint-add-ins.md).</span></span>
    
 
-  <span data-ttu-id="1b36e-p108">**Манифесты надстроек Office.** При необходимости в пакете может быть один или несколько манифестов надстроек Office, при этом каждый пакет Надстройка Office. Эта часть может быть включена в пакет надстройки, только если надстройку планируется отправить в корпоративный каталог надстроек SharePoint, а не в общедоступный магазин. Дополнительные сведения можно найти в статье [Публикация надстроек для SharePoint](publish-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p108">**Office Add-ins Manifests:** Optionally, there may be one or more Office Add-ins manifests that each package an Office Add-in. This part can be included in the add-in package only if the add-in is going to be uploaded to a SharePoint corporate add-in catalog, not the public marketplace. See [Publish SharePoint Add-ins](publish-sharepoint-add-ins.md) for more information.</span></span>
    
 

## <a name="add-in-for-sharepoint-manifest-file"></a><span data-ttu-id="1b36e-144">Файл манифеста надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b36e-144">Add-in for SharePoint manifest file</span></span>
<span data-ttu-id="1b36e-145"><a name="AppManifest"> </a></span><span class="sxs-lookup"><span data-stu-id="1b36e-145"><a name="AppManifest"> </a></span></span>

<span data-ttu-id="1b36e-p109">Каждая надстройка SharePoint включает файл appmanifest.xml. Файл appmanifest.xml сообщает SharePoint, что он должен знать о надстройке и задает наиболее важные свойства надстройки. Далее приводятся некоторые элементы, которые задаются в манифесте.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p109">Every SharePoint Add-in includes an appmanifest.xml file. The appmanifest.xml tells SharePoint what it must know about the add-in and defines the add-in's most important properties. The following are some of the items that are specified in the manifest:</span></span>
 

 

- <span data-ttu-id="1b36e-149">Внутреннее имя, идентификатор продукта и версия надстройки.</span><span class="sxs-lookup"><span data-stu-id="1b36e-149">The internal name, product ID, and version of the add-in.</span></span>
    
 
- <span data-ttu-id="1b36e-p110">URL-адрес начальной страницы, которая открывается при запуске надстройки. Это может быть страница на сайте надстройки, страница в облаке или страница на веб-сервере независимого поставщика ПО.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p110">The URL of the start page, which is the page that opens when the add-in is started. This can be a page in the add-in web, a cloud-based page, or a page on a web server of the ISV.</span></span>
    
     <span data-ttu-id="1b36e-p111">**Примечание.** При определенных обстоятельствах могут существовать ограничения, из-за которых в элементе **StartPage** можно указывать не все типы файлов. Дополнительные сведения см. в статье [Элемент StartPage (complexType PropertiesDefinition, манифест надстройки SharePoint)](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx). Когда вы сочетаете несколько параметров запроса в значении **StartPage**, необходимо использовать код амперсанда `&amp;amp;`, а не символ `&amp;` или точку с запятой для объединения параметров.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p111">**Note**  In certain circumstances, there may be restrictions on what type of file can be specified in the  **StartPage** element. For details, see [StartPage element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx). When you are combining more than one query parameter in the  **StartPage** value, you must use the encoded ampersand " `&amp;amp;`" rather than " `&amp;`" or a semi-colon to append them together.</span></span>
- <span data-ttu-id="1b36e-p112">Другие свойства надстройки. Сюда входит название и поддерживаемые надстройкой языки (оба параметра обязательные), URL-адреса служб, которые обрабатывают события после установки, после обновления и до удаления, и шаблон сайта, который должен использоваться при создании сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p112">Other properties of the add-in. These include title and the locales supported by the add-in (both are required), the URLs of services that handle the post-install, post-upgrade, and pre-uninstall events, and the web template to use when the add-in web is created.</span></span>
    
 
- <span data-ttu-id="1b36e-157">Запросы разрешений, необходимых надстройке для доступа к ресурсам SharePoint вне сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="1b36e-157">Requests for permissions the add-in needs to SharePoint resources outside the add-in web.</span></span>
    
 
- <span data-ttu-id="1b36e-p113">Идентификация субъекта надстройки в целях проверки подлинности и авторизации. Это субъект, который предоставляет разрешения. Для надстроек с размещением в SharePoint этот элемент не нужен.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p113">An identification, for authentication and authorization purposes, of the add-in principal. It is this principal that is granted permissions. This is not required for a SharePoint-hosted add-in.</span></span>
    
 
- <span data-ttu-id="1b36e-p114">Список обязательных компонентов (если таковые имеются), которые должны быть доступны, чтобы можно было установить надстройку. Например, может требоваться установка, лицензирование и активация определенных компонентов или служб.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p114">A list of the prerequisites, if any, that must be available to the add-in in order for the add-in to be installed. For example, certain Features may need to be installed and activated, and certain services may need to be licensed and installed.</span></span>
    
 

 <span data-ttu-id="1b36e-163">**Примечание.** Файл манифеста надстройки — единственный обязательный элемент в пакете надстройки, при этом не все элементы в списке выше должны обязательно входить в этот файл.</span><span class="sxs-lookup"><span data-stu-id="1b36e-163">**Note**  The add-in manifest file is the only required item in the add-in package, but not all of the items in the previous list are required parts of the file.</span></span> 
 

<span data-ttu-id="1b36e-p115">Дополнительные сведения о разметке манифеста надстройки можно найти в разделе  [Справочник по схеме для манифестов SharePoint Add-ins](http://msdn.microsoft.com/library/1f8c5d44-3b60-0bfe-9069-1df821220691%28Office.15%29.aspx). Эта статья не заменяет сведения из указанного раздела, в том числе сведения об обязательных элементах и атрибутах. Обратите внимание также на то, что схема манифестов надстроек SharePoint отличается от схемы манифестов надстроек Office. Дополнительные сведения можно найти в разделе  [Справка по схеме для приложений для манифестов Office (версия 1.1)](http://msdn.microsoft.com/library/7e0cadc3-f613-8eb9-57ef-9032cbb97f92%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p115">For detailed information about the add-in manifest markup, see the node  [Schema reference for manifests of SharePoint Add-ins](http://msdn.microsoft.com/library/1f8c5d44-3b60-0bfe-9069-1df821220691%28Office.15%29.aspx). This topic is not a substitute for the information in that node, including information about required elements and attributes. Also, note that SharePoint add-in manifests have a different schema from Office Add-in manifests. You can find information about the latter at  [Schema reference for Office Add-ins manifests (v1.1)](http://msdn.microsoft.com/library/7e0cadc3-f613-8eb9-57ef-9032cbb97f92%28Office.15%29.aspx).</span></span>
 

 
<span data-ttu-id="1b36e-p116">Далее приводится пример файла appmanifest.xml. Обратите внимание, что в этом примере начальной страницей надстройки является страница ASP.NET, находящаяся на удаленном сервере, а не страница сайта SharePoint. URL-адрес для этой страницы включает строку запроса, которая передает в удаленное веб-приложение URL-адрес хост-сайта. Часть "{HostUrl}" строки является маркером, который разрешается при запуске надстройки. Надстройка запрашивает разрешение на запись во все списки на хост-сайте. Субъектом надстройки, которому необходимо предоставить это разрешение, является удаленное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="1b36e-p116">The following is an example of an appmanifest.xml file. Note that in this example, the start page for the add-in is an ASP.NET page that is on a remote server, not a page on the SharePoint site. The URL for the page includes a query string that passes to the remote web application the URL of the host web. The "{HostUrl}" part of the string is a token that is resolved when the add-in is launched. The add-in is requesting Write permission to all the lists in the host web. The add-in principal that must be granted this permission is the remote web application.</span></span>
 

 
<span data-ttu-id="1b36e-p117">В манифесте надстройки вам необходимо использовать либо элемент **SupportedLocales**, либо элемент **SupportedLanguages**. Элемент **SupportedLanguages** устарел и теперь заменяется элементом **SupportedLocales**. Элемент **SupportedLanguages** будет работать даже после выпуска, однако следует воздерживаться от его использования. Дополнительные сведения об этих элементах см. в статьях [Элемент SupportedLocales (complexType PropertiesDefinition, манифест надстройки SharePoint)](http://msdn.microsoft.com/library/49bde91a-8d7a-be17-4c91-82c9c19f0f61%28Office.15%29.aspx) и [Элемент SupportedLanguages (complexType PropertiesDefinition, манифест надстройки SharePoint)](http://msdn.microsoft.com/library/7a8da886-5731-9abd-2911-5cd268bba4cf%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p117">You must use either the  **SupportedLocales** or the **SupportedLanguages** element in your add-in manifest. **SupportedLanguages** is being deprecated in favor of **SupportedLocales**. The  **SupportedLanguages** element will continue to work even after release, but you should refrain from using it. For more information about these elements see [SupportedLocales element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/49bde91a-8d7a-be17-4c91-82c9c19f0f61%28Office.15%29.aspx) and [SupportedLanguages element (PropertiesDefinition complexType) (SharePoint Add-in Manifest)](http://msdn.microsoft.com/library/7a8da886-5731-9abd-2911-5cd268bba4cf%28Office.15%29.aspx).</span></span>
 

 

 <span data-ttu-id="1b36e-p118">**Примечание** Значения атрибута **Scope** элемента **AppPermissionRequest** структурированы как URI, но фактически это строковые литералы. Ни одна часть значения **Scope** в примере ниже не является заполнителем. Дополнительные сведения о разрешениях см. в статье [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p118">**Note**  The values of the  **Scope** attribute of the **AppPermissionRequest** element are structured like URIs, but they are actually literal strings. No part of the example **Scope** value in the following example is a placeholder. For more information about permissions, see [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint.md).</span></span>
 




```XML
<?xml version="1.0" encoding="utf-8" ?>
<App xmlns="http://schemas.microsoft.com/sharepoint/2012/app/manifest"
     ProductID="{4a07f3bd-803d-45f2-a710-b9e944c3396e}"
     Version="1.0.0.0"
     SharePointMinVersion="15.0.0.0"
     Name="MySampleApp"
>
  <Properties>
    <Title>My Sample App</Title>
    <StartPage>http://MyRemoteWebApplicationServer/default.aspx/?SPHostUrl={HostUrl}</StartPage>
    <SupportedLocales>
      <SupportedLocale CultureName="en-US" />
    </SupportedLocales>        
  </Properties>

  <AppPermissionRequests>
    <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web/list" Right="Write"/>
  </AppPermissionRequests>

  <AppPrincipal>
    <RemoteWebApplication ClientId="1ee82b34-7c1b-471b-b27e-ff272accd564" />
  </AppPrincipal>
</App>

```


### <a name="url-tokens-in-the-add-in-manifest"></a><span data-ttu-id="1b36e-180">Маркеры URL-адресов в манифесте надстройки</span><span class="sxs-lookup"><span data-stu-id="1b36e-180">URL tokens in the add-in manifest</span></span>

<span data-ttu-id="1b36e-p119">В SharePoint имеется несколько маркеров, которые можно использовать в элементе **StartPage** и в других местах надстроек и их компонентов, чтобы представлять информацию, которая неизвестна до запуска надстройки. Инфраструктура SharePoint разрешает эти маркеры. Одни маркеры используются в начале URL-адреса, а другие можно использовать в URL-адресе в качестве значения параметра запроса. Эти маркеры и ряд других маркеров также можно использовать во многих контекстах разработки SharePoint. Подробные сведения обо всех этих маркерах и о том, где их можно использовать, см. в статье [Строки URL-адресов и маркеры в надстройках SharePoint](url-strings-and-tokens-in-sharepoint-add-ins.md). Общие сведения об остальных маркерах и URL-адресах в SharePoint см. в статье [URL-адреса и маркеры в SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b36e-p119">SharePoint provides several tokens that can be used in the  **StartPage** element and other places in add-ins and components of add-ins to represent information that is not known until the add-in is run. The SharePoint infrastructure resolves these tokens. Some are used at the beginning of the URL and others can be used within a URL such as the value of a query parameter. These tokens and several others can also be used in a variety of SharePoint development contexts. For detailed information about all the tokens and where they can be used, see [URL strings and tokens in SharePoint Add-ins](url-strings-and-tokens-in-sharepoint-add-ins.md). For general information about other tokens and URLs in SharePoint, see  [URLs and tokens in SharePoint](http://msdn.microsoft.com/library/161418d7-8123-4c4e-91a1-97e43c17f0e6%28Office.15%29.aspx).</span></span>
 

 

 <span data-ttu-id="1b36e-186">**Примечание.** Эти маркеры не используются в атрибуте **Scope** элемента **AppPermissionRequest**.</span><span class="sxs-lookup"><span data-stu-id="1b36e-186">**Note**  These tokens are not used in the  **Scope** attribute of an **AppPermissionRequest** element.</span></span>
 


## <a name="additional-resources"></a><span data-ttu-id="1b36e-187">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1b36e-187">Additional resources</span></span>
<span data-ttu-id="1b36e-188"><a name="SP15Exploreappmanifest_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="1b36e-188"><a name="SP15Exploreappmanifest_bk_addlresources"> </a></span></span>


-  [<span data-ttu-id="1b36e-189">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b36e-189">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="1b36e-190">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b36e-190">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 
-  [<span data-ttu-id="1b36e-191">Справочник по схеме для манифестов надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="1b36e-191">Schema reference for manifests of SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/1f8c5d44-3b60-0bfe-9069-1df821220691%28Office.15%29.aspx)
    
 
-  [<span data-ttu-id="1b36e-192">Open Packaging Conventions (OPC)</span><span class="sxs-lookup"><span data-stu-id="1b36e-192">Open Packaging Conventions (OPC)</span></span>](http://msdn.microsoft.com/en-us/magazine/cc163372.aspx)
    
 
-  [<span data-ttu-id="1b36e-193">Подключение приложения уровня данных (DAC)</span><span class="sxs-lookup"><span data-stu-id="1b36e-193">Data-Tier Application Connection (DAC)</span></span>](http://msdn.microsoft.com/en-us/library/ee210546)
    
 
-  [<span data-ttu-id="1b36e-194">Web Deploy 2.0</span><span class="sxs-lookup"><span data-stu-id="1b36e-194">Web Deploy 2.0</span></span>](http://www.iis.net/download/WebDeploy)
    
 

