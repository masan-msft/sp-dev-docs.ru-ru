# <a name="create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-content-type"></a><span data-ttu-id="11dbb-101">Создание надстроек с размещением у поставщика, которые включают пользовательский список SharePoint и тип контента</span><span class="sxs-lookup"><span data-stu-id="11dbb-101">Create a provider-hosted add-in that includes a custom SharePoint list and content type</span></span>
<span data-ttu-id="11dbb-p101">Узнайте, как создать надстройку SharePoint, которая объединяет веб-приложение, размещенное в облаке, с размещенными в SharePoint пользовательскими шаблонами списков, экземплярами списков и пользовательскими типами контента, с помощью Инструментов разработчика Office для Visual Studio 2012. Узнайте, как взаимодействовать с сайтами надстроек SharePoint с помощью веб-службы REST/OData и как реализовать OAuth в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p101">Create an SharePoint Add-in that combines a cloud-hosted web application with custom SharePoint-hosted list templates, list instances, and custom content types by using the Office Developer Tools for Visual Studio 2012. Learn how to interact with SharePoint app webs by using the REST/OData web service, and how to implement OAuth in an SharePoint Add-in.</span></span>
 

 <span data-ttu-id="11dbb-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="11dbb-p103">Большинство классических компонентов SharePoint, например настраиваемые типы контента, пользовательские определения списков и рабочие процессы, можно включить в надстройку SharePoint, размещенную в облаке. Простой пример, приведенный в этой статье, включает следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="11dbb-p103">Most classic SharePoint components, such as custom content types, custom list definitions, and workflows, can be included in a cloud-hosted spappsing. The simple example in this article contains the following:</span></span>
 

- <span data-ttu-id="11dbb-109">Сайт надстройки с</span><span class="sxs-lookup"><span data-stu-id="11dbb-109">An add-in web with</span></span>
    
      - <span data-ttu-id="11dbb-110">рядом настраиваемых столбцов веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="11dbb-110">some custom site columns</span></span>
    
 
  - <span data-ttu-id="11dbb-111">типом пользовательского контента, использующим настраиваемые столбцы</span><span class="sxs-lookup"><span data-stu-id="11dbb-111">a custom content type that uses the custom columns</span></span>
    
 
  - <span data-ttu-id="11dbb-112">шаблоном настраиваемых списков, в котором используется данный тип пользовательского контента</span><span class="sxs-lookup"><span data-stu-id="11dbb-112">a custom list template that uses the custom content type</span></span>
    
 
  - <span data-ttu-id="11dbb-113">экземпляром списка, основанным на пользовательском определении списка</span><span class="sxs-lookup"><span data-stu-id="11dbb-113">a list instance based on the custom list definition</span></span>
    
 
- <span data-ttu-id="11dbb-114">Веб-приложение ASP.NET, считывающее данные из экземпляра списка</span><span class="sxs-lookup"><span data-stu-id="11dbb-114">An ASP.NET web application that reads data from the list instance</span></span>
    
 

## <a name="prerequisites-for-creating-this-sharepoint-add-in"></a><span data-ttu-id="11dbb-115">Необходимые условия для создания этой надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-115">Prerequisites for creating this SharePoint Add-in</span></span>
<span data-ttu-id="11dbb-116"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="11dbb-116"></span></span>


-  <span data-ttu-id="11dbb-117">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="11dbb-117">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) or later.</span></span>
    
 
-  <span data-ttu-id="11dbb-118">[Office Developer Tools](https://msdn.microsoft.com/en-us/office/aa905340.aspx).</span><span class="sxs-lookup"><span data-stu-id="11dbb-118">[Office Developer Tools](https://msdn.microsoft.com/en-us/office/aa905340.aspx)</span></span>
    
 
- <span data-ttu-id="11dbb-119">Установка SharePoint для тестирования и отладки</span><span class="sxs-lookup"><span data-stu-id="11dbb-119">A SharePoint 2013 installation for testing and debugging</span></span>
    
      - <span data-ttu-id="11dbb-p104">Это можно сделать на том же компьютере, который используется для разработки. Для разработки также можно использовать удаленную установку SharePoint. Если вы работаете с удаленной установкой, необходимо установить распространяемую клиентскую объектную модель для целевой установки. Она доступна в качестве распространяемого пакета в Центре загрузки Майкрософт. Выполните поиск по словам "пакет SDK для клиентских компонентов SharePoint Server 2013" или "пакет SDK для клиентских компонентов SharePoint Online".</span><span class="sxs-lookup"><span data-stu-id="11dbb-p104">This can be on the same computer as your development computer, or you can develop with a remote SharePoint 2013 installation. If you work with a remote installation, you need to install the client object model redistributable on the target installation. It is available as a redistributable package on the Microsoft Download Center. Search for "SharePoint Server 2013 Client Components SDK" or "SharePoint Online Client Components SDK".</span></span> 
    
 
  - <span data-ttu-id="11dbb-124">Тестовый веб-сайт SharePoint необходимо создать на основе определения **Сайт разработчика** (его можно создать в Центре администрирования).</span><span class="sxs-lookup"><span data-stu-id="11dbb-124">The test SharePoint website must be created from the **Developer Site** site definition (which you can create in Central Administration).</span></span>
    
 
  - <span data-ttu-id="11dbb-p105">Для обмена данными с сайтом надстройки ваше удаленное приложение использует либо JavaScript и [междоменную библиотеку](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library), либо [OAuth](authorization-and-authentication-of-sharepoint-add-ins). При использовании OAuth, как демонстрирует пример в данной статье, необходимо настроить установку SharePoint для работы с OAuth.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p105">Your remote web application communicates with the add-in web by using either JavaScript and the  [cross-domain library](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library) or [OAuth](authorization-and-authentication-of-sharepoint-add-ins). If OAuth is used, as it is in the continuing example of this article, the SharePoint 2013 installation must be configured to use OAuth.</span></span>
    
 

 <span data-ttu-id="11dbb-127">**Примечание.** Рекомендации по настройке среды разработки, соответствующей вашим потребностям, вы найдете в разделе [Разработка решений Office](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span><span class="sxs-lookup"><span data-stu-id="11dbb-127">**NOTE** For guidance on how to setup a development environment that fits your needs, see  [Start building Office and SharePoint Add-ins](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span></span>
 


### <a name="core-concepts-to-know-for-creating-an-add-in"></a><span data-ttu-id="11dbb-128">Ключевые понятия, которые необходимо знать при создании надстройки</span><span class="sxs-lookup"><span data-stu-id="11dbb-128">Core concepts to know for creating an add-in</span></span>

<span data-ttu-id="11dbb-p106">Перед созданием первой надстройки необходимо иметь базовое представление о том, что такое Надстройки SharePoint, и о различиях между размещением надстроек SharePoint в SharePoint и в облаке. Такие сведения имеются в статьях, перечисленных в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p106">Before you create your first add-in, you should have a basic understanding of what SharePoint Add-ins are and the differences between SharePoint-hosted and cloud-hosted SharePoint Add-ins. The articles in Table 1 should give you that understanding.</span></span>
 

 

<span data-ttu-id="11dbb-131">**Таблица 1. Ключевые понятия для создания надстройки**</span><span class="sxs-lookup"><span data-stu-id="11dbb-131">**Table 1. Core concepts for creating an add-in**</span></span>


|<span data-ttu-id="11dbb-132">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="11dbb-132">**Article title**</span></span>|<span data-ttu-id="11dbb-133">**Описание**</span><span class="sxs-lookup"><span data-stu-id="11dbb-133">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="11dbb-134">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-134">SharePoint Add-ins</span></span>](sharepoint-add-ins)|<span data-ttu-id="11dbb-135">Изучите новую модель надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.</span><span class="sxs-lookup"><span data-stu-id="11dbb-135">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="11dbb-136">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-136">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)|<span data-ttu-id="11dbb-137">Изучите аспекты архитектуры надстроек SharePoint и Модель для надстроек SharePoint, в том числе параметры размещения надстроек и пользовательского интерфейса, систему развертывания, систему безопасности и жизненный цикл.</span><span class="sxs-lookup"><span data-stu-id="11dbb-137">Learn about aspects of the architecture of SharePoint Add-ins and the model for SharePoint Add-ins, including the add-in hosting options, user interface (UI) options, deployment system, security system, and life cycle.</span></span>|
| [<span data-ttu-id="11dbb-138">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-138">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in)|<span data-ttu-id="11dbb-139">Узнайте о различных способах размещения надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="11dbb-139">Learn about the various ways that you can host SharePoint Add-ins.</span></span>|

## <a name="develop-the-sharepoint-add-in"></a><span data-ttu-id="11dbb-140">Разработка надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-140">Develop the SharePoint Add-in</span></span>
<span data-ttu-id="11dbb-141"><a name="Develop"> </a></span><span class="sxs-lookup"><span data-stu-id="11dbb-141"></span></span>

 <span data-ttu-id="11dbb-142">С помощью процедур в данном разделе на своем компьютере для разработки вы сможете создать надстройку SharePoint, включающую сайт надстройки с компонентами SharePoint и удаленное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="11dbb-142">In the procedures of this section, you create a SharePoint Add-in that includes an add-in web with SharePoint components and a remote web application on your development machine.</span></span>
 

 

### <a name="to-set-up-the-visual-studio-2012-solution-and-its-elements"></a><span data-ttu-id="11dbb-143">Настройка решения Visual Studio 2012 и его элементов</span><span class="sxs-lookup"><span data-stu-id="11dbb-143">To set up the Visual Studio 2012 solution and its elements</span></span>


1. <span data-ttu-id="11dbb-p107">В Visual Studio 2012 создайте проект на основе шаблона **Надстройка для SharePoint** из узла **Office SharePoint | Надстройки** (либо на **C#**, либо на **Visual Basic**) в дереве шаблонов мастера **создания проектов**. Выберите вариант **Размещено у поставщика**. В примере, рассматриваемом в этой статье, выбран язык C# и указано имя проекта LocalTheater.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p107">In Visual Studio 2012, create an **Add-in for SharePoint 2013** project from the **Office SharePoint | Add-ins** node (under either **C#** or **Visual Basic**) in the templates tree of the **New Project** wizard. Choose the **Provider-hosted** hosting option. In the continuing example of this article, C# is used as the language andLocalTheater is the project name.</span></span>
    
 
2. <span data-ttu-id="11dbb-147">Нажмите в мастере кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-147">Choose **Finish** in the wizard.</span></span>
    
 
3. <span data-ttu-id="11dbb-p108">Откройте файл AppManifest.xml в конструкторе манифеста. По умолчанию в качестве значения элемента **Title** используется имя проекта. Замените его на более понятное имя, так как именно это название надстройки будет отображаться в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p108">Open the AppManifest.xml file in the manifest designer. The **Title** element has the project name as its default value. Replace it with something more friendly because this is the name of the add-in that users see in the UI.</span></span>
    
 
4. <span data-ttu-id="11dbb-p109">Укажите значение параметра **Name** для надстройки. Это внутреннее имя, в котором можно использовать только символы ASCII без пробелов. Пример: LocalTheater.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p109">Specify a **Name** for the add-in. This is an internal name that must contain only ASCII characters and must contain no spaces; for example,LocalTheater.</span></span>
    
 
5. <span data-ttu-id="11dbb-153">Откройте файл Web.config в проекте веб-приложения и добавьте элемент `<customErrors mode="Off"/>` к элементу **system.web**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-153">Open the Web.config file in the web application project and add the element  `<customErrors mode="Off"/>` to the **system.web** element.</span></span>
    
 
6. <span data-ttu-id="11dbb-p110">Проверьте, находятся ли ссылки на следующие сборки в проекте веб-приложения. (Если ваша версия Visual Studio 2012 не добавила ссылки автоматически, добавьте их.)</span><span class="sxs-lookup"><span data-stu-id="11dbb-p110">Check to see that references to the following assemblies are in the web application project. (If your edition of Visual Studio 2012 did not add the references automatically, then add them now.)</span></span>
    
      -  <span data-ttu-id="11dbb-p111">**Microsoft.IdentityModel.dll** Данная сборка устанавливается в глобальном кэше сборки посредством Windows Identity Foundation (WIF). Так как данная сборка является сборкой.NET Framework 3.5, она отфильтровывается из узла **Framework** в диалоговом окне **Добавить ссылку** по умолчанию. Вы можете добавить к ней ссылку, переместившись непосредственно в папку `C:\Program Files\Reference Assemblies\Microsoft\Windows Identity Foundation\v3.5` вашего компьютера, используемого для разработки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p111">**Microsoft.IdentityModel.dll** This assembly is installed into the global assembly cache with Windows Identity Foundation (WIF). Because this is a .NET Framework 3.5 assembly, it is filtered out of the **Framework** node of the **Add Reference** dialog box by default. You can add a reference to it by browsing directly to the `C:\Program Files\Reference Assemblies\Microsoft\Windows Identity Foundation\v3.5` directory of your development computer.</span></span>
    
 
  -  <span data-ttu-id="11dbb-159">**Microsoft.IdentityModel.Extensions.dll** Вы можете добавить ссылку на эту библиотеку. Для этого перейдите непосредственно к папке `C:\Program Files\Reference Assemblies\Microsoft\Microsoft Identity Extensions\1.0` на компьютере, используемом для разработки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-159">**Microsoft.IdentityModel.Extensions.dll** You can add a reference to it by browsing directly to the `C:\Program Files\Reference Assemblies\Microsoft\Microsoft Identity Extensions\1.0` folder of your development computer.</span></span>
    
 
  -  <span data-ttu-id="11dbb-160">**System.IdentityModel.dll** Данная сборка является частью .NET Framework 4, и она появляется в узле **Assemblies | Framework** диалогового окна **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-160">**System.IdentityModel.dll** This assembly is part of the .NET Framework 4, and it appears on the **Assemblies | Framework** node of the **Add Reference** dialog box.</span></span>
    
 
7. <span data-ttu-id="11dbb-p112">Если удаленное веб-приложение получает доступ к данным на хост-сайте и на сайте надстройки, то необходимо добавить элемент **AppPermissionRequests** (с одним или несколькими дочерними элементами **AppPermissionRequest**) в файл AppManifest.xml. Веб-приложение в нашем примере получает доступ только к сайту надстройки. Субъекты надстроек автоматически получают все разрешения, необходимые для сайта надстройки, поэтому в файле AppManifest.xml из этого примера нет элемента **AppPermissionRequests**. Дополнительные сведения о запросах разрешений для надстроек и о том, как добавлять их, см. в статье [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p112">If your remote web application accesses information in the host web as well as the add-in web, you must add an **AppPermissionRequests** element, with one or more child **AppPermissionRequest** elements, to the AppManifest.xml file. (The web application in the continuing example of this article accesses only the add-in web. Add-in principals automatically have all permissions needed to the add-in web, so the AppManifest.xml in the example does not have an **AppPermissionRequests** element.) For more information about add-in permission requests and how to add them, see [Add-in permissions in SharePoint 2013](add-in-permissions-in-sharepoint-2013).</span></span>
    
 

### <a name="to-add-the-sharepoint-components"></a><span data-ttu-id="11dbb-164">Добавление компонентов SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-164">To add the SharePoint components</span></span>


1. <span data-ttu-id="11dbb-p113">Вы можете добавлять компоненты SharePoint в надстройку точно так же, как и в классическое решение фермы. Тем не менее, не каждый тип компонентов SharePoint можно включить в надстройку SharePoint. Цели, для которых служат этих компоненты, Надстройки SharePoint достигают другими способами. Подробные сведения о том, какие типы компонентов SharePoint можно включить в надстройку SharePoint, и о том, как включить их в проект, см. в разделах  [Типы компонентов SharePoint, которые могут находиться в надстройке для SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#TypesOfSPComponentsInApps).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p113">You add SharePoint components to an add-in exactly as you would add them to a classic farm solution. However, not every kind of SharePoint component can be included in a SharePoint Add-in. The purposes these components serve are accomplished in other ways in SharePoint Add-ins. For detailed information about what kinds of SharePoint components can be included in a SharePoint Add-in and how to include them in a project, see  [Types of SharePoint components that can be in a SharePoint Add-in](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#TypesOfSPComponentsInApps).</span></span>
    
    <span data-ttu-id="11dbb-p114">Для примера используйте указанные ниже процедуры. В них имеются примеры использования Visual Studio 2012, с помощью которых можно добавить настраиваемые столбцы, типы содержимого, шаблоны списков и экземпляры списков в надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p114">For purposes of the continuing example, use the following procedures. These will provide examples of using Visual Studio 2012 to add custom columns, content types, list templates, and list instances to a SharePoint Add-in.</span></span>
    
### <a name="to-create-the-custom-column-types"></a><span data-ttu-id="11dbb-171">Создание пользовательских типов столбцов</span><span class="sxs-lookup"><span data-stu-id="11dbb-171">To create the custom column types</span></span>


1. <span data-ttu-id="11dbb-172">В **обозревателе решений** добавьте в проект надстройки SharePoint элемент **Столбец сайта** с именем Actor.</span><span class="sxs-lookup"><span data-stu-id="11dbb-172">In **Solution Explorer**, add a SharePoint **Site Column** item to the SharePoint Add-in project with the nameActor.</span></span>
    
 
2. <span data-ttu-id="11dbb-p115">В файле elements.xml для нового столбца сайта отредактируйте элемент **Field**, указав атрибуты и значения, приведенные в следующем примере, но не меняйте GUID в атрибуте **ID**, оставив значение, созданное средой Visual Studio 2012. Не забудьте добавить фигурные скобки: {}.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p115">In the elements.xml file for the new site column, edit the **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value Visual Studio 2012 generated for it. Don't forget the framing braces "{}".</span></span>
    
```
  <Field ID="{generated GUID}" 
       Name="Actor" 
       Title="Actor" 
       DisplayName="Actor/Actress" 
       Group="Theater and Movies" 
       Description="The person cast, perhaps tentatively, in the role" 
       Type="Text" 
/>
```

3. <span data-ttu-id="11dbb-175">Добавьте в проект еще один элемент **Столбец сайта** с именем CastingStatus.</span><span class="sxs-lookup"><span data-stu-id="11dbb-175">Add another **Site Column** to the project namedCastingStatus.</span></span>
    
 
4. <span data-ttu-id="11dbb-176">В файле elements.xml для нового столбца сайта отредактируйте элемент **Field**, указав атрибуты и значения, приведенные в следующем примере, но не меняйте GUID в атрибуте **ID**, оставив значение, созданное средой Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="11dbb-176">In the elements.xml file for the new site column, edit the **Field** element so that it has the attributes and values shown in the following example, except that you should not change the GUID for the **ID** attribute from the value Visual Studio 2012 generated for it.</span></span>
    
```
  <Field ID="{generated GUID}" 
       Name="CastingStatus" 
       Title="CastingStatus"
       DisplayName="Casting Status" 
       Group="Theater and Movies" 
       Description="The current casting status of the role" 
       Type="Choice">
</Field>
```

5. <span data-ttu-id="11dbb-p116">Так как это поле является полем выбора, необходимо указать возможные варианты, порядок их отображения в раскрывающемся списке и вариант, выбранный по умолчанию. Добавьте следующую дочернюю маркировку к элементу **Field**:</span><span class="sxs-lookup"><span data-stu-id="11dbb-p116">Because this is a Choice field, you must specify the possible choices, the order in which they should appear in the drop-down list when a user is making a choice, and the default choice. Add the following child markup to the **Field** element.</span></span>
    
```
  <CHOICES>
      <CHOICE>Not Started</CHOICE>
      <CHOICE>Audition Scheduled</CHOICE>
      <CHOICE>Auditioned</CHOICE>
      <CHOICE>Role Offered</CHOICE>
      <CHOICE>Committed to Role</CHOICE>
</CHOICES>
<MAPPINGS>
      <MAPPING Value="1">Not Started</MAPPING>
      <MAPPING Value="2">Audition Scheduled</MAPPING>
      <MAPPING Value="3">Auditioned</MAPPING>
      <MAPPING Value="4">Role Offered</MAPPING>
      <MAPPING Value="5">Committed to Role</MAPPING>
</MAPPINGS>
<Default>Not Started</Default>
```


### <a name="to-create-the-custom-content-type"></a><span data-ttu-id="11dbb-179">Создание пользовательского типа контента</span><span class="sxs-lookup"><span data-stu-id="11dbb-179">To create the custom content type</span></span>


1. <span data-ttu-id="11dbb-p117">В **обозревателе решений** добавьте в проект надстройки SharePoint элемент **Тип контента** с именем ActingRole. Когда мастер предложит выбрать базовый тип контента, выберите **Элемент**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p117">In **Solution Explorer**, add a SharePoint **Content Type** item to the SharePoint Add-in project with the nameActingRole. When prompted by the wizard to select the base content type, choose **Item**, and then choose **Finish**.</span></span>
    
 
2. <span data-ttu-id="11dbb-182">Если конструктор типа контента не откроется автоматически, выберите тип контента **ActingRole** в **обозревателе решений**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="11dbb-182">If the content type designer does not automatically open, choose the **ActingRole** content type in **Solution Explorer** to open it.</span></span>
    
 
3. <span data-ttu-id="11dbb-183">Откройте вкладку **Тип контента** в конструкторе и заполните текстовые поля следующим образом:</span><span class="sxs-lookup"><span data-stu-id="11dbb-183">Open the **Content Type** tab in the designer and fill the text boxes as follows:</span></span>
    
      -  <span data-ttu-id="11dbb-184">**Имя типа контента**: ActingRole</span><span class="sxs-lookup"><span data-stu-id="11dbb-184">**Content Type Name**: ActingRole</span></span>
    
 
  -  <span data-ttu-id="11dbb-185">**Описание**: "Соответствует роли в пьесе или фильме"</span><span class="sxs-lookup"><span data-stu-id="11dbb-185">**Description**: Represents a role in a play or movie.</span></span>
    
 
  -  <span data-ttu-id="11dbb-186">**Имя группы**: "Театр и кино"</span><span class="sxs-lookup"><span data-stu-id="11dbb-186">**Group Name**: Theater and Movies</span></span>
    
 
4. <span data-ttu-id="11dbb-p118">Убедитесь, что ни один из флажков, находящихся во вкладке, не выбран ( *None*  ). Флажок **Наследует столбцы из родительского Типа контента** может быть выбран по умолчанию. *Обязательно очистите его.*</span><span class="sxs-lookup"><span data-stu-id="11dbb-p118">Verify that  *none*  of the check boxes on the tab are selected. The check box for **Inherits the columns from the parent Content Type** may be selected by default. *Be sure to clear it.*</span></span> 
    
 
5. <span data-ttu-id="11dbb-190">Откройте вкладку **Столбцы** конструктора.</span><span class="sxs-lookup"><span data-stu-id="11dbb-190">Open the **Columns** tab in the designer.</span></span>
    
 
6. <span data-ttu-id="11dbb-p119">Добавьте эти два столбца сайта к типу контента, используя сетку. Они располагаются в раскрывающемся списке по отображаемым именам: **Actor/Actress** и **CastingStatus**. Если они отсутствуют в списке, возможно, вы не сохранили проект после добавления настраиваемых столбцов сайтов. Нажмите **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p119">Use the grid to add the two site columns to the content type. They are listed in the drop-down list by their display names: **Actor/Actress** and **CastingStatus**. (If they are not listed, you may not have saved the project since adding the custom site columns. Choose **Save all**.)</span></span>
    
 
7. <span data-ttu-id="11dbb-195">Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="11dbb-195">Save the file and close the designer.</span></span>
    
 
8. <span data-ttu-id="11dbb-196">На следующем этапе вам потребуется работать непосредственно с необработанным кодом XML типа контента, поэтому в **обозревателе решений** необходимо выбрать дочерний файл elements.xml типа контента **ActingRole**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-196">The next step requires that you work directly in the raw XML for the content type, so in **Solution Explorer**, choose the elements.xml file child of the **ActingRole** content type.</span></span>
    
 
9. <span data-ttu-id="11dbb-p120">Для двух добавленных вами столбцов в файле уже есть элементы **FieldRef**. Добавьте аналогичные им элементы **FieldRef** для двух встроенных столбцов SharePoint. Ниже представлена маркировка элементов. *Для атрибута ID необходимо использовать те же идентификаторы GUID, так как это встроенные типы полей с фиксированными идентификаторами.* Добавьте их *над* двумя имеющимися элементами **FieldRef** для настраиваемых столбцов сайтов.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p120">There are already **FieldRef** elements in the file for the two columns that you added. Add **FieldRef** elements for two built-in SharePoint 2013 columns as peers of the two that are already there. The following is the markup for the elements. *You must use these same GUIDs for the ID attribute because these are built-in field types with fixed IDs.*  Add these *above*  the two **FieldRef** elements for the custom site columns.</span></span>
    
```
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Character" />
<FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Character" />
```


    Note that we have given these fields a custom display name:  **Character**, in the sense of a character in a play or movie.
    
 

### <a name="to-create-the-custom-list-template-and-a-list-instance"></a><span data-ttu-id="11dbb-202">Создание пользовательского шаблона и экземпляра списка</span><span class="sxs-lookup"><span data-stu-id="11dbb-202">To create the custom list template and a list instance</span></span>


1. <span data-ttu-id="11dbb-p121">Добавьте в проект надстройки SharePoint элемент **Список** с именем CharactersInShow. На странице **Выберите параметры списка** в **мастере настроек SharePoint** оставьте заданное по умолчанию отображаемое имя списка (**CharactersInShow**), нажмите кнопку **Создать настраиваемый список на основе**, а затем выберите элемент **По умолчанию (пусто)** в раскрывающемся списке. Затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p121">Add a SharePoint **List** item to the SharePoint Add-in project with the nameCharactersInShow. On the **Choose List Settings** page of the **SharePoint Customization Wizard**, leave the list display name at the default **CharactersInShow**, choose the **Create a customizable list based on** option button, and choose **Default (Blank)** on the drop-down list. Then choose **Finish**.</span></span>
    
 
2. <span data-ttu-id="11dbb-p122">По завершении работы мастера будет создан шаблон списка **CharactersInShow** с дочерним экземпляром списка под названием **CharactersInShowInstance**. По умолчанию может открыться конструктор списка. Он понадобится на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p122">When you complete the wizard, a **CharactersInShow** list template is created with a child list instance named **CharactersInShowInstance**. A list designer may have opened by default. It is used in a later step.</span></span>
    
 
3. <span data-ttu-id="11dbb-209">Откройте дочерний файл elements.xml шаблона списка **CharactersInShow** (*не* дочерний файл elements.xml, относящийся к списку **CharactersInShowInstance**).</span><span class="sxs-lookup"><span data-stu-id="11dbb-209">Open the elements.xml child of the **CharactersInShow** list template ( *not*  the elements.xml child of the **CharactersInShowInstance**).</span></span>
    
 
4. <span data-ttu-id="11dbb-210">Измените значение атрибута **DisplayName** на более понятное: "Герои представления".</span><span class="sxs-lookup"><span data-stu-id="11dbb-210">Add spaces to the **DisplayName** attribute to make it friendlier:"Characters In Show".</span></span>
    
 
5. <span data-ttu-id="11dbb-211">Для атрибута **Description** задайте значение "Персонажи пьесы или фильма".</span><span class="sxs-lookup"><span data-stu-id="11dbb-211">Set the **Description** attribute to"The characters in a play or movie."</span></span>
    
 
6. <span data-ttu-id="11dbb-212">Оставьте для других атрибутов значения по умолчанию, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="11dbb-212">Leave all other attributes at their default, save the file and close it.</span></span>
    
 
7. <span data-ttu-id="11dbb-213">Если конструктор списка не открыт, выберите узел **CharactersInShow** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-213">If the list designer is not open, choose the **CharactersInShow** node in **Solution Explorer**.</span></span>
    
 
8. <span data-ttu-id="11dbb-214">Откройте вкладку **Столбцы** конструктора и нажмите кнопку **Типы контента**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-214">Open the **Columns** tab in the designer, and then choose the **Content Types** button.</span></span>
    
 
9. <span data-ttu-id="11dbb-215">В диалоговом окне **Параметры типов содержимого** добавьте тип контента **ActingRole**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-215">In the **Content Type Settings** dialog, add the **ActingRole** content type.</span></span>
    
 
10. <span data-ttu-id="11dbb-216">Выберите тип контента **ActingRole** в списке типов контента, а затем нажмите кнопку **По умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-216">Choose the **ActingRole** content type in the list of types, and choose the **Set as Default** button.</span></span>
    
    <span data-ttu-id="11dbb-217">Выберите тип контента **Элемент**, щелкните правой кнопкой мыши маленькую стрелку слева от имени типа контента и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-217">Choose the **Item** content type, right-click the small arrowhead that appears to the left of the content type name, and then choose **Delete**.</span></span>
    
 
11. <span data-ttu-id="11dbb-p123">Повторите предыдущий этап для типа контента **Папка**, чтобы в списке остался только тип контента **ActingRole**. Чтобы закрыть диалоговое окно, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p123">Repeat the preceding step for the **Folder** content type, so **ActingRole** is the only content type listed. Choose **OK** to close the dialog.</span></span>
    
 
12. <span data-ttu-id="11dbb-p124">Теперь в списке столбцов отображается три столбца. Выберите **Название**, щелкните правой кнопкой мыши маленькую стрелку слева от имени типа контента и выберите пункт **Удалить**. Теперь должно остаться только два столбца: **Актер или актриса** и **Статус кастинга**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p124">Three columns are now on the list of columns. Choose **Title**, right-click the small arrowhead that appears to the left of the content type name, and then choose **Delete**. Only two columns should now be listed, **Actor/Actress** and **Casting Status**.</span></span>
    
 
13. <span data-ttu-id="11dbb-p125">Откройте вкладку **Список** конструктора. Эта вкладка используется для настройки определенных значений для *экземпляра*, а не *шаблона* списка.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p125">Open the **List** tab of the designer. This tab is used to set certain values for the list *instance*  , not the list *template*  .</span></span>
    
 
14. <span data-ttu-id="11dbb-225">Замените значения на этой вкладке следующими:</span><span class="sxs-lookup"><span data-stu-id="11dbb-225">Change the values on this tab to the following:</span></span>
    
      -  <span data-ttu-id="11dbb-226">**Заголовок**: "Герои пьесы «Гамлет»"</span><span class="sxs-lookup"><span data-stu-id="11dbb-226">**Title**: Characters in Hamlet</span></span>
    
 
  -  <span data-ttu-id="11dbb-227">**URL-адрес списка**: Lists/CharactersInHamlet</span><span class="sxs-lookup"><span data-stu-id="11dbb-227">**List URL**: Lists/CharactersInHamlet</span></span>
    
 
  -  <span data-ttu-id="11dbb-228">**Описание**: "Герои пьесы «Гамлет» и сведения о кастинге".</span><span class="sxs-lookup"><span data-stu-id="11dbb-228">**Description**: The characters in Hamlet and casting information.</span></span>
    
 

     <span data-ttu-id="11dbb-229">Оставьте установленные по умолчанию флажки и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="11dbb-229">Leave the check boxes at their default status, save the file, and close the designer.</span></span>
    
 
15. <span data-ttu-id="11dbb-p126">В **обозревателе решений** может отображаться старое имя экземпляра списка. В этом случае откройте контекстное меню элемента **CharactersInShowInstance**, выберите пункт **Переименовать** и измените имя на CharactersInHamlet.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p126">The list instance may have its old name in **Solution Explorer**. If so, open the shortcut menu for **CharactersInShowInstance**, choose **Rename**, and change the name to CharactersInHamlet.</span></span>
    
 
16. <span data-ttu-id="11dbb-232">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="11dbb-232">Open the schema.xml file.</span></span>
    
 
17. <span data-ttu-id="11dbb-p127">Файл может содержать два элемента **ContentType**: один со значением ActingRole для атрибута **Name**, другой с именем **ListFieldsContentType**. Нас интересует только элемент ActingRole, поэтому следует удалить остальные элементы **ContentType**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p127">There may be two **ContentType** elements in the file, one with the **Name** attribute value ofActingRole and another called **ListFieldsContentType**. Only the one called ActingRole belongs, so delete any other **ContentType** elements.</span></span>
    
     <span data-ttu-id="11dbb-p128">**Примечание.** Между элементами **ContentType** может не быть разрывов строк, вследствие чего может показаться, что отображается только один элемент. Прокрутите представление вправо и внимательно проверьте наличие остальных элементов.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p128">**NOTE** There may not be line breaks between the **ContentType** elements, in which case it may appear at first that there is only one. Scroll to the right and check carefully for others.</span></span>
18. <span data-ttu-id="11dbb-p129">Элемент **Fields** должен содержать два элемента **Field** (в одной строке, если между ними нет разрыва строки). Один из них должен быть точной копией элемента **Field** из файла elements.xml столбца сайта **Actor**, а другой — точной копией элемента **Field** из файла elements.xml столбца сайта **CastingStatus**. Если между ними нет полного совпадения (включая все дочерние элементы, например **CHOICES** и **MAPPINGS**), скопируйте элемент **Field** из файла elements.xml столбца сайта и вставьте его вместо несоответствующего элемента **Field** в файле schema.xml.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p129">The **Fields** element should have two **Field** elements (which are on a single line if there is no line break between them). One should exactly duplicate the **Field** element in the **Actor** site column elements.xml and the other should exactly duplicate the **Field** element from the **CastingStatus** site column elements.xml. If there is not an exact match, including all child elements (such as the **CHOICES** and **MAPPINGS** elements), copy the **Field** element from the site column elements.xml file and paste it in place of the mismatched **Field** element in the schema.xml file.</span></span>
    
 
19. <span data-ttu-id="11dbb-p130">Не закрывая файл schema.xml, в элементе **View**, значение BaseViewID которого равно 0, замените элемент **ViewFields** на приведенную ниже разметку. Используйте именно этот GUID для параметра **FieldRef** с именем `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p130">Still in the schema.xml file, in the **View** element whose BaseViewID value is "0", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
```
  <ViewFields>
  <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Character" />
  <FieldRef Name="Actor" ID="{GUID from the site column elements.xml}" />
  <FieldRef Name="CastingStatus" ID="{GUID from the site column elements.xml}" />
</ViewFields>
```

20. <span data-ttu-id="11dbb-p131">Замените два отсутствующих значения атрибута ID на идентификаторы GUID в соответствующих файлах elements.xml столбцов сайтов. Не забудьте добавить фигурные скобки: {}.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p131">Replace the two missing ID attribute values with the GUIDs in the respective site column elements.xml files. Don't forget the framing braces "{}".</span></span> 
    
 
21. <span data-ttu-id="11dbb-p132">Не закрывая файл schema.xml, в элементе **View**, значение BaseViewID которого равно 1, замените имеющийся элемент **ViewFields** на приведенную ниже разметку. Используйте именно этот GUID для параметра **FieldRef** с именем `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p132">Still in the schema.xml file, in the **View** element whose BaseViewID value is "1", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
```
  <ViewFields>
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Character" />
</ViewFields>
```

22. <span data-ttu-id="11dbb-246">Скопируйте два элемента **FieldRef** столбцов `Actor` и `CastingStatus`, которые вы добавили в предыдущее представление, в этот элемент **ViewFields** на одном уровне с элементом **FieldRef** для `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="11dbb-246">Copy the two **FieldRef** elements for `Actor` and `CastingStatus` that you added to the previous view to this **ViewFields** element as siblings of the `LinkTitle` **FieldRef**.</span></span>
    
 
23. <span data-ttu-id="11dbb-247">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="11dbb-247">Save and close the schema.xml file.</span></span>
    
 
24. <span data-ttu-id="11dbb-248">Откройте файл elements.xml, являющийся дочерним объектом экземпляра списка **CharactersInHamlet**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-248">Open the elements.xml file that is a child of the list instance **CharactersInHamlet**.</span></span>
    
 
25. <span data-ttu-id="11dbb-249">Заполните список какими-либо начальными данными, добавив приведенную ниже разметку в качестве дочернего объекта элемента **ListInstance**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-249">Populate the list with some initial data by adding the following markup as a child of the **ListInstance** element.</span></span>
    
```
  <Data>
  <Rows>
    <Row>
      <Field Name="Title">Hamlet</Field>
      <Field Name="Actor">Tom Higginbotham</Field>
      <Field Name="CastingStatus">Committed to Role</Field>
    </Row>
    <Row>
      <Field Name="Title">Claudius</Field>
      <Field Name="Actor"></Field>
      <Field Name="CastingStatus">Not Started</Field>
    </Row>
    <Row>
      <Field Name="Title">Gertrude</Field>
      <Field Name="Actor">Satomi Hayakawa</Field>
      <Field Name="CastingStatus">Auditioned</Field>
    </Row>
    <Row>
      <Field Name="Title">Ophelia</Field>
      <Field Name="Actor">Cassi Hicks</Field>
      <Field Name="CastingStatus">Committed to Role</Field>
    </Row>
    <Row>
      <Field Name="Title">The ghost</Field>
      <Field Name="Actor">Lertchai Treetawatchaiwong</Field>
      <Field Name="CastingStatus">Role Offered</Field>
    </Row>
  </Rows>
</Data>
```

2. <span data-ttu-id="11dbb-p133">В **обозревателе решений** выберите элемент **Feature1**, чтобы открыть конструктор возможностей. В конструкторе задайте для поля **Заголовок** значение "Компоненты данных театра и кино", а для поля **Описание** — "Столбцы сайтов, типы контента и экземпляры списков для данных о театре и кино". Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p133">In **Solution Explorer**, choose **Feature1** to open the Feature designer. In the designer, set the **Title** toTheater and Movie Data Components and set the **Description** toSite columns, content types, and list instances for data about theater and movies.. Save the file, and close the designer.</span></span>
    
 
3. <span data-ttu-id="11dbb-253">Если элемент **Feature1** в **обозревателе решений** не был переименован, откройте его контекстное меню, выберите пункт **Переименовать** и укажите имя TheaterAndMovieDataComponents.</span><span class="sxs-lookup"><span data-stu-id="11dbb-253">If the **Feature1** in **Solution Explorer** has not been renamed, open its shortcut menu, choose **Rename**, and rename it TheaterAndMovieDataComponents.</span></span>
    
 

### <a name="to-code-the-remote-web-application-project"></a><span data-ttu-id="11dbb-254">Написание кода проекта удаленного веб-приложения</span><span class="sxs-lookup"><span data-stu-id="11dbb-254">To code the remote web application project</span></span>


- <span data-ttu-id="11dbb-p134">Создайте веб-приложение так же, как и любое другое веб-приложение для выбранного вами комплекса платформ. Что касается платформ корпорации Майкрософт, вы можете использовать либо веб-службу REST/OData, либо одну из клиентских объектных моделей в SharePoint. При работе с другими платформами вы можете использовать конечные точки REST/OData в SharePoint для выполнения операций CRUD (создания, чтения, обновления и удаления данных) на сайте надстройки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p134">Develop the web application as you would any other web application for your preferred platform stack. For a Microsoft stack, you can use either the REST/OData web service or one of the client object models in SharePoint 2013. For a non-Microsoft stack, you can use the REST/OData endpoints in SharePoint 2013 to perform create/read/update/delete (CRUD) operations on data in the add-in web.</span></span>
    
     <span data-ttu-id="11dbb-p135">**Примечание.** При добавлении ссылки на сборку для проекта веб-приложения в Visual Studio задайте для свойства **Копировать локально** этой сборки значение **True**, если вы не уверены, установлена ли сборка на веб-сервере и сможете ли вы обеспечить ее установку перед развертыванием надстройки. Платформа .NET Framework устанавливается в веб-ролях Microsoft Azure и на веб-сайтах Azure. Тем не менее клиентские сборки для SharePoint, а также различные расширения и основы для управляемого кода Майкрософт не устанавливаются. Инструменты разработчика Office для Visual Studio 2012 автоматически добавляют ссылки на некоторые сборки, часто используемые надстройками SharePoint, и задают свойство **Копировать локально**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p135">**NOTE** When you add a reference to an assembly to your web application project in Visual Studio, set the **Copy Local** property of the assembly to **True**, unless you know that the assembly is already installed on the web server, or you can ensure that it is installed before you deploy your add-in. The .NET Framework is installed on Microsoft Azure Web Roles and Azure Web Sites. But the SharePoint 2013 client assemblies and the various Microsoft managed code extensions and foundations are not installed. Office Developer Tools for Visual Studio 2012 automatically adds references to some assemblies commonly used in SharePoint Add-ins and sets the **Copy Local** property.</span></span>

    <span data-ttu-id="11dbb-p136">В нашем примере создается веб-приложение ASP.NET. Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p136">For the continuing example, you develop an ASP.NET web application. Take the following steps.</span></span>
    
      1. <span data-ttu-id="11dbb-p137">Откройте файл Default.aspx и замените основной элемент файла на приведенную ниже разметку. Она добавляет кнопку **Get the Cast** (Получить состав актеров), при нажатии которой данные из списка **Герои пьесы "Гамлет"** на сайте приложения отображаются в элементе управления [GridView](http://msdn2.microsoft.com/EN-US/library/4w7ya1ts), появляющемся только после нажатия кнопки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p137">Open the Default.aspx file and replace the body element of the file with the following markup. The markup adds a **Get the Cast** button that, when chosen, reads the **Characters in Hamlet** list that is in the add-in web and presents its data in a [GridView](http://msdn2.microsoft.com/EN-US/library/4w7ya1ts) control that appears only after the button is pressed.</span></span>
    
```HTML
  <body >
    <form id="form1" runat="server">
    <div>
    <h2>Local Theater</h2>
    </div>
    <asp:Literal ID="Literal1" runat="server"><br /><br /></asp:Literal>

    <asp:Button ID="Button1" runat="server" OnClick="Button1_Click" Text="Get the Cast"/>

    <asp:Literal ID="Literal2" runat="server"><br /><br /></asp:Literal>

    <asp:GridView ID="GridView1" runat="server" Caption="The Cast" ></asp:GridView>
    </form>
</body>
```

  2. <span data-ttu-id="11dbb-266">Откройте файл Default.aspx.cs и добавьте в него приведенные ниже операторы **using**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-266">Open the Default.aspx.cs file and add the following **using** statements to it.</span></span>
    
```C#
  using Microsoft.SharePoint.Client;
using Microsoft.IdentityModel.S2S.Tokens;
using System.Net;
using System.IO;
using System.Xml;
using System.Data;
using System.Xml.Linq;
using System.Xml.XPath;
using Microsoft.SharePoint.Samples;
```


    The last of these statements refers to the namespace that is declared in the TokenHelper.cs file.
    
 
  3. <span data-ttu-id="11dbb-267">Добавьте приведенные ниже поля в класс **Default**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-267">Add the following fields to the **Default** class.</span></span>
    
```C#
  SharePointContextToken contextToken;
string accessToken;
Uri sharepointUrl;
```

  4. <span data-ttu-id="11dbb-p138">Замените метод **Page_Load** на приведенный ниже код, который использует класс **TokenHelper** для получения маркеров с защищенного сервера маркеров, совместимого с OAuth. Затем маркер доступа сохраняется в свойстве [CommandArgument](http://msdn2.microsoft.com/EN-US/library/hykdabtx) кнопки для дальнейшего вызова обработчиком события при нажатии кнопки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p138">Replace the **Page_Load** method with the following code that uses the **TokenHelper** class to obtain tokens from the OAuth-compliant secure token server. The access token is then stored in the [CommandArgument](http://msdn2.microsoft.com/EN-US/library/hykdabtx) property of the button for later retrieval by the button's click event handler.</span></span>
    
```C#
  protected void Page_Load(object sender, EventArgs e)
{
    TokenHelper.TrustAllCertificates();
    string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

    if (contextTokenString != null)
    {
        // Get context token
        contextToken = TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

        // Get access token
        sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);
        accessToken = TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority).AccessToken;
        
        // Pass the access token to the button event handler.
        Button1.CommandArgument = accessToken;
    }
}
```

  5. <span data-ttu-id="11dbb-p139">Добавьте к классу **Default** приведенный ниже обработчик событий. Сначала обработчик получает маркер доступа, который был сохранен в свойстве [CommandArgument](http://msdn2.microsoft.com/EN-US/library/hykdabtx) кнопки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p139">Add the following event handler to the **Default** class. The handler begins by retrieving the access token that was stored in the button's [CommandArgument](http://msdn2.microsoft.com/EN-US/library/hykdabtx) property.</span></span>
    
```C#
  protected void Button1_Click(object sender, EventArgs e)
{
    // Retrieve the access token that the Page_Load method stored
    // in the button's command argument.
    string accessToken = ((Button)sender).CommandArgument;
}
```

  6. <span data-ttu-id="11dbb-272">Обработчику требуется заново получить измененный URL-адрес сайта надстройки при обратной передаче, поэтому следует добавить приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="11dbb-272">The handler needs to reacquire the modified add-in web URL on postbacks, so add the following code.</span></span>
    
```C#
  if (IsPostBack)
{
    sharepointUrl = new Uri(Request.QueryString["SPAppWebUrl"]);
}
```

  7. <span data-ttu-id="11dbb-p140">Для получения данных списка добавьте приведенную ниже строку, в которой используется одна из конечных точек SharePoint REST/OData. В этом примере код считывает список **Герои пьесы "Гамлет"**, развернутый на сайте надстройки. Благодаря API для этой службы достаточно одной строки кода, чтобы выбрать список и указать три возвращаемых поля. Обратите внимание, что в URL-адресе OData необходимо использовать внутренние имена полей (столбцов), а не отображаемые имена, поэтому в коде используются значения `Title`, `Actor` и `CastingStatus`, а не `Character`, `Actor/Actress` и `Casting Status.`. Дополнительные сведения о веб-службе REST/OData см. в статье [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p140">Add the following line that uses one of the SharePoint 2013 REST/OData endpoints to obtain list data. In this example, the code reads the **Characters in Hamlet** list that is deployed to the add-in web. The APIs for this service make it easy, in a single line of code, to select a list and specify three fields from the list to return. Note that in the OData URL you must use the internal names of the fields (columns) rather than the display names, so the code uses `Title`,  `Actor`, and  `CastingStatus` rather than `Character`,  `Actor/Actress`, and  `Casting Status.` For more information about the REST/OData web service, see [Use OData query operations in SharePoint REST requests](use-odata-query-operations-in-sharepoint-rest-requests).</span></span>
    
```C#
  // REST/OData URL section
 string oDataUrl = "/_api/Web/lists/getbytitle('Characters In Hamlet')/items?$select=Title,Actor,CastingStatus";
```

  8. <span data-ttu-id="11dbb-277">Добавьте приведенный ниже код, создающий объекты HTTP-запроса и отклика с помощью классов [HttpWebRequest](http://msdn2.microsoft.com/EN-US/library/8y7x3zz2) и [HttpWebResponse](http://msdn2.microsoft.com/EN-US/library/ww5755y6) из пространства имен [System.Net](http://msdn2.microsoft.com/EN-US/library/btdf6a7e).</span><span class="sxs-lookup"><span data-stu-id="11dbb-277">Add the following code that uses the  [HttpWebRequest](http://msdn2.microsoft.com/EN-US/library/8y7x3zz2) and [HttpWebResponse](http://msdn2.microsoft.com/EN-US/library/ww5755y6) classes of the [System.Net](http://msdn2.microsoft.com/EN-US/library/btdf6a7e) namespace to construct the HTTP request and response objects.</span></span>
    
```C#
  // HTTP Request and Response construction section
HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + oDataUrl);
request.Method = "GET";
request.Accept = "application/atom+xml";
request.ContentType = "application/atom+xml;type=entry";
request.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

  9. <span data-ttu-id="11dbb-p141">Для выполнения синтаксического анализа XML-ответа в формате ATOM добавьте следующий код. Он использует классы области имен  [System.Xml.Linq](http://msdn2.microsoft.com/EN-US/library/bb299195) для синтаксического анализа возвращенных данных и создания [List<T>](http://msdn2.microsoft.com/EN-US/library/6sh2ey19) элементов из списка SharePoint. (Вы также могли бы использовать классы области имен [System.Xml](http://msdn2.microsoft.com/EN-US/library/y3y47afh) .) Обратите внимание, что в XML-файле, возвращаемом SharePoint, дочерние элементы элемента **entry** содержат метаданные об элементе списка. Фактические данные строк элемента списка SharePoint размещаются двумя уровнями ниже в элементе **properties**. По этой причине для отфильтровывания верхних уровней дважды используется метод расширения  [Elements<T>](http://msdn2.microsoft.com/EN-US/library/bb348465)</span><span class="sxs-lookup"><span data-stu-id="11dbb-p141">Add the following code to parse the ATOM-formatted response XML. It uses the classes of the  [System.Xml.Linq](http://msdn2.microsoft.com/EN-US/library/bb299195) namespace to parse the data that is returned and construct a [List<T>](http://msdn2.microsoft.com/EN-US/library/6sh2ey19) of the items from the SharePoint list. (You could also use the classes of the [System.Xml](http://msdn2.microsoft.com/EN-US/library/y3y47afh) namespace.) Note that, in the XML that SharePoint returns, the child elements of the **entry** element hold metadata about the list item. The actual row data of a SharePoint list item is nested two layers down in the **properties** element. For that reason the [Elements<T>](http://msdn2.microsoft.com/EN-US/library/bb348465) extension method is used twice to filter out the higher levels.</span></span>
    
```C#
  // Response markup parsing section
XDocument oDataXML = XDocument.Load(response.GetResponseStream(), LoadOptions.None);
XNamespace atom = "http://www.w3.org/2005/Atom";
XNamespace d = "http://schemas.microsoft.com/ado/2007/08/dataservices";
XNamespace m = "http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"; 

List<XElement> entries = oDataXML.Descendants(atom + "entry")
                         .Elements(atom + "content")
                         .Elements(m + "properties")
                         .ToList();
```

  10. <span data-ttu-id="11dbb-p142">Добавьте приведенный ниже запрос LINQ, чтобы создать коллекцию [IEnumerable<T>](http://msdn2.microsoft.com/EN-US/library/9eekhta0) анонимного типа, включающего только необходимые нам свойства. Обратите внимание: несмотря на то что код должен ссылаться на поле имени элемента по его внутреннему имени (`Title`), в качестве имени свойства в анонимном типе, которому назначается значение, можно указать значение `Character`. В результате после привязки коллекции к элементу управления сетки на странице будет отображаться более понятное название — **Персонаж**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p142">Add the following LINQ query to construct an  [IEnumerable<T>](http://msdn2.microsoft.com/EN-US/library/9eekhta0) collection of an anonymous type that has just the properties you need and no others. Note that although the code must refer to the item title field by its internal name `Title`, the property name in the anonymous type, to which the value is assigned, can be named  `Character`. One effect of this is that when the collection is bound to a grid control, the more appropriate name **Character** appears on the page.</span></span>
    
```C#
  var entryFieldValues = from entry in entries
                       select new { Character=entry.Element(d + "Title").Value, 
                                    Actor=entry.Element(d + "Actor").Value, 
                                    CastingStatus=entry.Element(d + "CastingStatus").Value };

```

  11. <span data-ttu-id="11dbb-p143">Завершите настройку обработчика следующим кодом, привязывающим данные к элементу контроля  [GridView](http://msdn2.microsoft.com/EN-US/library/4w7ya1ts) на странице. Заголовкам столбцов в сетке по умолчанию присваиваются имена свойств анонимного типа: `Character`,  `Actor` и `CastingStatus`. Элемент управления  [GridView](http://msdn2.microsoft.com/EN-US/library/4w7ya1ts) имеет свойства, позволяющие управлять именем и форматировать заголовки колонок, поэтому вы можете сделать так, чтобы имена **Actor/Actress** (Актер/актриса) и **Casting Status** (Статус кастинга) совпадали с заголовками колонок в SharePoint. Чтобы избежать сложностей, эти методы здесь не описываются. (Вы можете также использовать элемент управления [DataGrid](http://msdn2.microsoft.com/EN-US/library/e1zk1ey1) .)</span><span class="sxs-lookup"><span data-stu-id="11dbb-p143">Finish the handler with the following code to bind the data to a  [GridView](http://msdn2.microsoft.com/EN-US/library/4w7ya1ts) control on the page. The column headers in the grid default to the property names of the anonymous type: `Character`,  `Actor`, and  `CastingStatus`. The  [GridView](http://msdn2.microsoft.com/EN-US/library/4w7ya1ts) control has properties that enable you to control the name and formatting column headers, so you could have **Actor/Actress** and **Casting Status** to match the column headers in SharePoint. For simplicity, these techniques are not described here. (You could also use a [DataGrid](http://msdn2.microsoft.com/EN-US/library/e1zk1ey1) control.)</span></span>
    
```C#
  GridView1.DataSource = entryFieldValues;
GridView1.DataBind();

```

  12. <span data-ttu-id="11dbb-291">Сохраните все файлы.</span><span class="sxs-lookup"><span data-stu-id="11dbb-291">Save all files.</span></span>
    
 

### <a name="to-test-and-debug-the-sharepoint-add-in"></a><span data-ttu-id="11dbb-292">Тестирование и отладка надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-292">To test and debug the SharePoint Add-in</span></span>


1. <span data-ttu-id="11dbb-p144">Чтобы протестировать надстройку SharePoint и ее удаленное веб-приложение, в Visual Studio 2012 нажмите клавишу F5. Веб-приложение будет развернуто в IIS Express в localhost. Надстройка SharePoint будет установлена на целевом веб-сайте SharePoint. (В нашем примере удаленная надстройка *не* пытается взаимодействовать с *хост*-сайтом, и субъект надстройки автоматически получает разрешения для доступа к сайту *надстройки*, поэтому для вас *не* отображается предложение предоставить разрешения.) Откроется страница **Содержимое сайта** целевого веб-сайта SharePoint, на которой отобразится новая надстройка.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p144">To test the SharePoint Add-in and its remote web application, choose the F5 key in Visual Studio 2012. The web application is deployed to IIS Express at localhost. The SharePoint Add-in will is installed to the target SharePoint website. (In the continuing example, the remote add-in does  *not*  try to interact with the *host*  web and the add-in principal automatically has permissions to the *add-in*  web, so you are *not*  prompted to grant permissions.) The **Site Contents** page of your target SharePoint website opens, and you see the new add-in listed there.</span></span>
    
 
2. <span data-ttu-id="11dbb-p145">Выберите надстройку SharePoint, и удаленное веб-приложение откроется на странице, указанной в элементе **StartPage** файла AppManifest.xml. Откройте приложение и проверьте его работоспособность. В нашем примере достаточно нажать кнопку. После этого будет создана таблица, заполненная элементами списка **Герои пьесы "Гамлет"** с сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p145">Choose the SharePoint Add-in, and the remote web application opens to the page you specified in the **StartPage** element in the AppManifest.xml file. Use the web application as needed to verify that it is working. In the continuing example of this topic, just choose the button. Doing so creates a grid and populates it with the **Characters in Hamlet** list of the add-in web.</span></span>
    
 

## <a name="publishing-the-sharepoint-add-in"></a><span data-ttu-id="11dbb-301">Публикация надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-301">Publishing the SharePoint Add-in</span></span>
<span data-ttu-id="11dbb-302"><a name="Publish"> </a></span><span class="sxs-lookup"><span data-stu-id="11dbb-302"></span></span>

<span data-ttu-id="11dbb-p146">Чтобы опубликовать вашу надстройку SharePoint, отправьте пакет надстройки в корпоративный каталог надстроек или в магазин надстроек Office. Дополнительные сведения см. в разделах  [Публикация в Магазин Office или каталоге надстроек организации](deploying-and-installing-sharepoint-add-ins-methods-and-options#MarketOrCatalog) и [Публикация надстроек для SharePoint](publish-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p146">To publish your SharePoint Add-in, upload the add-in package to a corporate add-in catalog or to the Office add-in store. For more information, see  [Publishing to the Office Store or an organization's add-in catalog](deploying-and-installing-sharepoint-add-ins-methods-and-options#MarketOrCatalog) and [Publish SharePoint Add-ins](publish-sharepoint-add-ins).</span></span>
 

 

## <a name="troubleshooting"></a><span data-ttu-id="11dbb-305">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="11dbb-305">Troubleshooting</span></span>
<span data-ttu-id="11dbb-306"><a name="Troubleshooting"> </a></span><span class="sxs-lookup"><span data-stu-id="11dbb-306"></span></span>

<span data-ttu-id="11dbb-p147">Если надстройка не работает, рекомендуется проверить, не является ли это следствием ошибки разметки CAML, блокирующей развертывание компонентов SharePoint. Чтобы проверить развертывание, используйте процедуру, аналогичную описанной ниже.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p147">If the add-in is not working, you should consider whether a mistake in the CAML markup is blocking deployment of the SharePoint components. Use a procedure similar to the following, which is based on the continuing example, to verify the deployment.</span></span>
 

 

### <a name="to-test-the-provisioning-of-the-add-in-web"></a><span data-ttu-id="11dbb-309">Проверка подготовки сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="11dbb-309">To test the provisioning of the add-in web</span></span>


1. <span data-ttu-id="11dbb-p148">Откройте страницу **Параметры сайта** на хост-сайте. В разделе **Администрирование семейства веб-сайтов** выберите ссылку **Иерархия сайтов**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p148">Open the **Site Settings** page of the host web. In the **Site Collection Administration** section, choose the **Site hierarchy** link.</span></span>
    
 
2. <span data-ttu-id="11dbb-p149">На странице **Иерархия сайтов** вы увидите свою надстройку, указанную по URL-адресу. Не запускайте ее. Вместо этого скопируйте URL-адрес и используйте его URL на оставшихся этапах.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p149">On the **Site Hierarchy** page, you see your add-in listed by its URL. Do not launch it. Instead, copy the URL and use the URL in the remaining steps.</span></span>
    
 
3. <span data-ttu-id="11dbb-315">Перейдите по адресу _URL-адрес_сайта_приложения_/_layouts/15/ManageFeatures.aspx и на открывшейся странице **Возможности сайта** убедитесь, что возможность **Компоненты данных театра и кино** указана в алфавитном списке возможностей вашей надстройки SharePoint, а ее состояние — **Активна**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-315">Navigate to URL_of_app_web/_layouts/15/ManageFeatures.aspx and, on the Site Features page that opens, verify that Theater and Movie Data Components is on the alphabetical list of Features in your spappsing and that its status is Active.</span></span>
    
 
4. <span data-ttu-id="11dbb-316">Перейдите по адресу _URL-адрес_сайта_приложения_/_layouts/15/mngfield.aspx и на открывшейся странице **Столбцы сайта** убедитесь, что группа **Театр и кино** отображается в списке столбцов сайта и содержит новые настраиваемые столбцы сайта: **Актер или актриса** и **Статус кастинга**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-316">Navigate to _URL_of_app_web_/_layouts/15/mngfield.aspx and, on the **Site Columns** page that opens, verify that a **Theater and Movies** group is in the list of site columns and that it contains your new custom site columns, **Actor/Actress** and **Casting Status**.</span></span>
    
 
5. <span data-ttu-id="11dbb-317">Перейдите по адресу _URL-адрес_сайта_приложения_/_layouts/15/mngctype.aspx и на открывшейся странице **Типы контента сайта** убедитесь, что группа **Театр и кино** указана в списке типов контента и содержит новый тип контента — **ActingRole**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-317">Navigate to _URL_of_app_web_/_layouts/15/mngctype.aspx and, on the **Site Content Types** page that opens, verify that a **Theater and Movies** group is in the list of content types and that it contains your new **ActingRole** content type.</span></span>
    
 
6. <span data-ttu-id="11dbb-p150">Перейдите по ссылке на тип контента **ActingRole**. На открывшейся странице **Тип контента сайта** убедитесь, что тип контента содержит два новых типа столбцов сайта, **Актер или актриса** и **Статус кастинга**, а в поле названия элемента указано заданное вами отображаемое имя: **Персонаж**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p150">Choose the link to the **ActingRole** content type. On the **Site Content Type** page that opens, verify that the content type has the two new site column types, **Actor/Actress** and **Casting Status**, and that the item title field has been given your custom display name: **Character**.</span></span>
    
 
7. <span data-ttu-id="11dbb-320">Перейдите по адресу _URL-адрес_сайта_приложения_/_layouts/15/mcontent.aspx и на открывшейся странице **Списки и библиотеки сайта** проверьте наличие ссылки **Настроить "Герои пьесы «Гамлет»"**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-320">Navigate to _URL_of_app_web_/_layouts/15/mcontent.aspx and, on the **Site Libraries and Lists** page that opens, verify that there is a **Customize "Characters in Hamlet"** link.</span></span>
    
 
8. <span data-ttu-id="11dbb-p151">Перейдите по ссылке **Настроить "Герои пьесы «Гамлет»"** и убедитесь, что на странице параметров списка единственный тип контента для списка — это **ActingRole**, а два новых столбца сайта, **Актер или актриса** и **Статус кастинга** указаны в разделе **Столбцы**. Столбец заголовка может быть обозначен внутренним именем **Title**, а не присвоенным вами отображаемым именем **Персонаж**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p151">Choose the **Customize "Characters in Hamlet"** link and verify on the list settings page that the only content type for the list is your custom **ActingRole** content type and that your two new site columns, **Actor/Actress** and **Casting Status** are listed in the **Columns** section. (The Title column may appear with its internal name **Title**, instead of the display name **Character** that you gave it.)</span></span>
    
     <span data-ttu-id="11dbb-p152">**Примечание.** Если на этой странице отсутствует раздел **Типы контента**, необходимо включить управление типами контента. Перейдите по ссылке **Дополнительные параметры**, а затем на странице **Дополнительные параметры** включите управление типами контента и нажмите кнопку **ОК**. Снова откроется предыдущая страница, которая теперь содержит раздел **Типы контента**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p152">**NOTE** If there is no **Content Types** section on the page, you must enable management of content types. Click the **Advanced Settings** link and on the **Advanced Settings** page, enable management of content types and click **OK**. You are returned to the previous page and there is now a list of **Content Types** section.</span></span>
9. <span data-ttu-id="11dbb-p153">В верхней части страницы указан **веб-адрес** списка. Скопируйте его и вставьте в адресной строке вашего браузера, а затем перейдите к списку. Убедитесь, что список содержит элементы, созданные вами качестве образцов. Столбец заголовка может появиться на экране с внутренним именем **Title** вместо присвоенного вами отображаемого имени **Персонаж**.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p153">Near the top of the page is the **Web Address** of the list. Copy this and paste it into the address bar of your browser, and then navigate to the list. Verify that the list has the sample items that you created. (The Title column may appear with its internal name **Title**, instead of the display name **Character** that you gave it.)</span></span>
    
 

## <a name="next-steps"></a><span data-ttu-id="11dbb-330">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11dbb-330">Next steps</span></span>
<span data-ttu-id="11dbb-331"><a name="NextSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="11dbb-331"></span></span>

<span data-ttu-id="11dbb-p154">В данной статье показано, как создать несложную комбинацию надстройки SharePoint с удаленным веб-приложением. Ниже указаны некоторые действия, которые вы можете предпринять дальше.</span><span class="sxs-lookup"><span data-stu-id="11dbb-p154">This article demonstrated how to create a simple hybrid SharePoint Add-in with a remote web application. As next steps, consider the following:</span></span>
 

 

- <span data-ttu-id="11dbb-p155">Добавление в надстройку всех функций CRUD с помощью конечных точек REST/OData или с помощью одной из клиентских объектных моделей. Дополнительные сведения см. в статье [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests) и [Выполнение базовых операций с помощью кода клиентской библиотеки SharePoint](complete-basic-operations-using-sharepoint-2013-client-library-code).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p155">Adding full CRUD functionality to the add-in with either the REST/OData endpoints or one of the client object models. For more information, see  [Use OData query operations in SharePoint REST requests](use-odata-query-operations-in-sharepoint-rest-requests) and [Complete basic operations using SharePoint 2013 client library code](complete-basic-operations-using-sharepoint-2013-client-library-code).</span></span>
    
 
- <span data-ttu-id="11dbb-p156">Локализация надстройки SharePoint для других языков. Дополнительные сведения см. в статье [Локализация надстроек SharePoint](localize-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p156">Localizing your SharePoint Add-in for other cultures. For more information, see  [Localize SharePoint Add-ins](localize-sharepoint-add-ins).</span></span>
    
 
- <span data-ttu-id="11dbb-p157">Создание надстройки-компаньона для Windows Phone, которая дублирует функции удаленного веб-приложения. Дополнительные сведения см. в разделе  [Создание мобильных надстроек для SharePoint 2013](http://msdn.microsoft.com/en-us/library/office/jj163228.aspx).</span><span class="sxs-lookup"><span data-stu-id="11dbb-p157">Creating a Windows Phone companion add-in that duplicates the functionality of the remote web application. For more information, see  [Build mobile SharePoint Add-ins 2013](http://msdn.microsoft.com/en-us/library/office/jj163228.aspx).</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="11dbb-340">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="11dbb-340">Additional resources</span></span>
<span data-ttu-id="11dbb-341"><a name="SP15createcloud_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="11dbb-341"></span></span>


-  [<span data-ttu-id="11dbb-342">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="11dbb-342">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="11dbb-343">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="11dbb-343">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

