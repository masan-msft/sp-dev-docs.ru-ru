---
title: "Создание надстроек SharePoint в Visual Studio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ef06e1e32cbdafb36b2ff074dacd0d528f6a656f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-sharepoint-add-ins-in-visual-studio"></a><span data-ttu-id="04242-102">Создание надстроек SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="04242-102">Create SharePoint Add-ins in Visual Studio</span></span>
<span data-ttu-id="04242-103">Узнайте, как разрабатывать надстройки SharePoint, используя шаблоны проектов и элементов проектов в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04242-103">Learn to develop SharePoint Add-ins by using templates for projects and project items in Visual Studio.</span></span>
 

 <span data-ttu-id="04242-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="04242-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="04242-107">Вы можете разрабатывать надстройки SharePoint, используя новые шаблоны проектов и элементов проектов в **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="04242-107">You can develop SharePoint Add-ins by using new templates for projects and project items in  **vsnv**.</span></span> 
 

## <a name="project-templates"></a><span data-ttu-id="04242-108">Шаблоны проектов</span><span class="sxs-lookup"><span data-stu-id="04242-108">Project templates</span></span>
<span data-ttu-id="04242-109"><a name="SP15Projecttemplates_templates"> </a></span><span class="sxs-lookup"><span data-stu-id="04242-109"></span></span>

<span data-ttu-id="04242-p102">При использовании шаблона проекта Visual Studio создает решение, которое содержит элементы проекта и файлы, необходимые для определенного типа проекта. Следующие шаблоны проекта отображаются в диалоговом окне **Новый проект**, если развернуть узел **Office/SharePoint**, а затем — узел **Надстройки**. Сведения о шаблонах проектов в узле **Решения SharePoint** см. в статье [Шаблоны проектов и элементов проектов SharePoint](http://go.microsoft.com/fwlink/?LinkId=255306).</span><span class="sxs-lookup"><span data-stu-id="04242-p102">When you use a project template in Visual Studio, it creates a solution that contains the project items and files that the project type requires. The following project templates appear in the  **New Project** dialog box if you expand the **Office/SharePoint** node and then you choose the **Add-ins** node. For information about the project templates under the **SharePoint Solutions** node, see [SharePoint Project and Project Item Templates](http://go.microsoft.com/fwlink/?LinkId=255306).</span></span> 
 

 

### <a name="office-add-in"></a><span data-ttu-id="04242-113">Надстройка Office</span><span class="sxs-lookup"><span data-stu-id="04242-113">Office Add-in</span></span>

<span data-ttu-id="04242-p103">Создает веб-страницы, которые размещаются в приложениях Office, таких как Excel или Outlook. Надстройка Office предоставляет дополнительное содержимое и функциональность для документа или элемента Outlook. Подробнее об этом:  [Обзор платформы надстроек Office](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="04242-p103">Creates a webpage that's hosted inside an Office application, such as Excel or Outlook. An Office Add-in provides additional content and functionality in a document or Outlook item. For more information, see  [Office Add-ins platform overview](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span></span>
 

 

### <a name="sharepoint-add-in"></a><span data-ttu-id="04242-117">Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="04242-117">SharePoint Add-in</span></span>

<span data-ttu-id="04242-p104">Создает Надстройка SharePoint на основе информации, которую вы указываете в мастере настройки. Эта информация включает в себя следующие данные:</span><span class="sxs-lookup"><span data-stu-id="04242-p104">Creates a SharePoint Add-in based on the information that you specify in a wizard. This information includes the following data.</span></span>
 

 

- <span data-ttu-id="04242-120">Имя надстройки.</span><span class="sxs-lookup"><span data-stu-id="04242-120">The name of the add-in.</span></span>
    
 
- <span data-ttu-id="04242-121">Локальный или удаленный сайт SharePoint, используемый для отладки надстройки.</span><span class="sxs-lookup"><span data-stu-id="04242-121">The local or remote SharePoint site to use for debugging your add-in.</span></span>
    
 
- <span data-ttu-id="04242-122">Тип надстройки: с размещением у поставщика или с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="04242-122">The type of add-in that you want to create: provider-hosted or SharePoint-hosted.</span></span> 
    
 
<span data-ttu-id="04242-123">Дополнительные сведения см. в статье [Надстройки SharePoint](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="04242-123">For more information, see  [SharePoint Add-ins](sharepoint-add-ins.md).</span></span>
 

 

### <a name="cloud-business-add-in"></a><span data-ttu-id="04242-124">Облачное бизнес-приложение</span><span class="sxs-lookup"><span data-stu-id="04242-124">Cloud Business Add-in</span></span>

<span data-ttu-id="04242-p105">Используя шаблон **Облачная бизнес-надстройка** в Visual Studio, вы можете создать надстройку с размещением в SharePoint для просмотра, добавления и обновления данных из удаленных источников с современных сенсорных устройств, таких как телефоны и планшеты. Дополнительные сведения см. в статье [Создание облачных бизнес-надстроек](create-cloud-business-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="04242-p105">By using the  **Cloud Business Add-in** template in Visual Studio, you can create a SharePoint-hosted add-in in which mobile users can view, add, and update data from remote locations by using modern, touch-oriented devices such as phones and tablets. For more information, see [Create cloud business add-ins](create-cloud-business-add-ins.md).</span></span>
 

 

## <a name="project-item-templates"></a><span data-ttu-id="04242-127">Шаблоны элементов проектов</span><span class="sxs-lookup"><span data-stu-id="04242-127">Project item templates</span></span>
<span data-ttu-id="04242-128"><a name="SP15Projecttemplates_items"> </a></span><span class="sxs-lookup"><span data-stu-id="04242-128"></span></span>

<span data-ttu-id="04242-129">После создания решения SharePoint вы можете добавить в него элементы проекта, используя следующие шаблоны, которые отображаются в диалоговом окне **Добавление нового элемента** в узле **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="04242-129">After you create a SharePoint solution, you can add project items to it by using the following templates, which appear in the  **Add New Item** dialog box under the **Office/SharePoint** node.</span></span>
 

 

### <a name="office-add-in"></a><span data-ttu-id="04242-130">Надстройка Office</span><span class="sxs-lookup"><span data-stu-id="04242-130">Office Add-in</span></span>

<span data-ttu-id="04242-p106">Добавляет Надстройка Office в Надстройка SharePoint. Вы можете добавить надстройку панели задач, контентную или почтовую надстройку. Дополнительные сведения см. в статье  [Обзор платформы надстроек Office](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="04242-p106">Adds an Office Add-in to your SharePoint Add-in. You can add a task pane add-in, a content add-in, or a mail add-in. For more information, see  [Office Add-ins platform overview](http://msdn.microsoft.com/library/e64de870-ce22-4331-92e7-76d35279bf91%28Office.15%29.aspx).</span></span>
 

 

### <a name="client-web-part-host-web"></a><span data-ttu-id="04242-134">Клиентская веб-часть (хост-сайт)</span><span class="sxs-lookup"><span data-stu-id="04242-134">Client Web Part (Host Web)</span></span>

<span data-ttu-id="04242-p107">Добавляет клиентскую веб-часть в Надстройка SharePoint. Добавив клиентскую веб-часть, вы сможете отображать надстройки на страницах хост-сайта. Этот шаблон содержит один файл Elements.xml, свойства которого определяют следующие элементы клиентской веб-части.</span><span class="sxs-lookup"><span data-stu-id="04242-p107">Adds a client web part to your SharePoint Add-in. By adding a client web part, you can display add-ins on the pages of a host site. This template contains a single Elements.xml file, whose properties define the following elements of the client web part.</span></span>
 

 


|<span data-ttu-id="04242-138">**Имя свойства**</span><span class="sxs-lookup"><span data-stu-id="04242-138">**Property Name**</span></span>|<span data-ttu-id="04242-139">**Описание**</span><span class="sxs-lookup"><span data-stu-id="04242-139">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="04242-140">ClientWebPart</span><span class="sxs-lookup"><span data-stu-id="04242-140">ClientWebPart</span></span>|<span data-ttu-id="04242-141">Определяет имя, заголовок, описание и размеры клиентской веб-части.</span><span class="sxs-lookup"><span data-stu-id="04242-141">Specifies the name, the title, the description, and the dimensions of the client web part.</span></span>|
|<span data-ttu-id="04242-142">Контент</span><span class="sxs-lookup"><span data-stu-id="04242-142">Content</span></span>|<span data-ttu-id="04242-p108">Определяет местоположение страницы, которая отображается в клиентской веб-части. У этого элемента два свойства: `Type` и `Src`. `Type` определяет тип создаваемой веб-части, например HTML. `Src` определяет расположение страницы, которая будет отображаться в клиентской веб-части. Шаблон ссылается на свойства в строке запроса, используя шаблон _PropertyName_, например `Src="~addinWebUrl/Pages/ClientWebPart1.aspx?Property1=_property1_"`. Дополнительные сведения см. в статье [Создание частей надстройки для установки совместно с надстройкой SharePoint](create-add-in-parts-to-install-with-your-sharepoint-add-in.md)</span><span class="sxs-lookup"><span data-stu-id="04242-p108">Defines the location of the page that renders inside the client web part. This element has two properties:  `Type` and `Src`.  `Type` specifies the type of web part that you're creating, such as HTML. `Src` defines the location of the page that will render inside the client web part. The template references properties on the query string by using the pattern _ _PropertyName__, such as  `Src="~addinWebUrl/Pages/ClientWebPart1.aspx?Property1=_property1_"`For more information, see  [Create add-in parts to install with your SharePoint Add-in](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span></span>|

### <a name="content-type"></a><span data-ttu-id="04242-148">Тип контента</span><span class="sxs-lookup"><span data-stu-id="04242-148">Content Type</span></span>

<span data-ttu-id="04242-p109">Добавляет тип контента в надстройку SharePoint (схожие типа контента использовались в предыдущих версиях SharePoint). Тип контента — это набор метаданных, рабочих процессов и поведения для категории элементов в списке или библиотеке SharePoint. Например, элемент — один тип контента "список". К другим типам относятся объявления, контакты и задачи, они наследуются от типа контента "элемент". Тип контента "контакт" содержит столбцы, такие как **Имя**, **Фамилия** и **Должность**.</span><span class="sxs-lookup"><span data-stu-id="04242-p109">Adds a content type to your SharePoint Add-in, similar to content types that were used in previous versions of SharePoint. A content type is a set of metadata, workflows, and behavior for a category of items in a SharePoint list or library. For example, an item is one type of list content. Other types of list content include announcements, contacts, and tasks, and they inherit from the item content type. The contact content type contains columns such as  **First Name**,  **Last Name**, and  **Job Title**.</span></span>
 

 
<span data-ttu-id="04242-p110">При добавлении типа контента в надстройку SharePoint указывается базовый тип контента. Например, новый тип контента может наследоваться от объявления, контакта, документа или элемента. Затем используется конструктор **Тип контента** для настройки столбцов и других свойств типа контента, например имени и описания. Выбранные значения добавляются в элементы `ContentType` и `FieldRef` в файле Elements.xml. Дополнительные сведения см. в статье [Стандартный блок: типы контента SharePoint 2010](http://msdn.microsoft.com/library/277dfc42-d9a8-4fae-9ae1-0d202b14674f%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="04242-p110">When you add a content type to your SharePoint Add-in, you specify the base content type from which the new content type inherits. For example, it can inherit from an announcement, a contact, a document, or an item content type. You then use the  **Content Type** designer to configure the columns for the content type and its other properties, such as its name and its description. The values that you choose are added to the `ContentType` and `FieldRef` elements in the Elements.xml file. For more information, see [Building Block: SharePoint 2010 Content Types](http://msdn.microsoft.com/library/277dfc42-d9a8-4fae-9ae1-0d202b14674f%28Office.15%29.aspx).</span></span>
 

 

### <a name="empty-element"></a><span data-ttu-id="04242-159">Пустой элемент</span><span class="sxs-lookup"><span data-stu-id="04242-159">Empty Element</span></span>

<span data-ttu-id="04242-p111">Добавляет в Надстройка SharePoint элемент проекта для пустого элемента. Этот элемент проекта содержит один файл, Elements.xml, в котором вы определяете свойства элементов. Как правило, пустой элемент используется, чтобы определить компонент, для которого в Visual Studio нет шаблона.</span><span class="sxs-lookup"><span data-stu-id="04242-p111">Adds a project item for an empty element to your SharePoint Add-in. This project item contains a single file, Elements.xml, where you define the properties of the element. You typically use an empty element to define an item for which Visual Studio doesn't provide a template.</span></span>
 

 

### <a name="list"></a><span data-ttu-id="04242-163">Список</span><span class="sxs-lookup"><span data-stu-id="04242-163">List</span></span>

<span data-ttu-id="04242-p112">Добавляет два элемента в надстройку SharePoint: определение списка и экземпляр списка. При добавлении списка в надстройку указывается его имя и тип (пустой или основанный на существующем типе списка). Кроме того, указывается, можно ли настраивать список. Затем используется **конструктор списка** для настройки столбцов и представлений списка и других свойств, например имени и описания. Подробнее о свойствах списка: [Элемент ListTemplate (List Template)](http://msdn.microsoft.com/library/e565ead9-adcb-4a90-97e3-04850719420a%28Office.15%29.aspx) и [Элемент ListInstance (List Instance)](http://msdn.microsoft.com/library/cfefe8e5-2656-4d71-bb4e-5f991a800598%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="04242-p112">Adds two project items to your SharePoint Add-in: a list definition and an instance of the list. When you add a list to your add-in, you specify what to name the list and whether to create either a blank list or a list that's based on an existing list type. You also specify whether the list can be customized. Then you use the  **List Designer** to configure the columns and views for the list and other properties, such as the list's name and description. For more information about list properties, see [ListTemplate Element (List Template)](http://msdn.microsoft.com/library/e565ead9-adcb-4a90-97e3-04850719420a%28Office.15%29.aspx) and [ListInstance Element (List Instance)](http://msdn.microsoft.com/library/cfefe8e5-2656-4d71-bb4e-5f991a800598%28Office.15%29.aspx).</span></span>
 

 

### <a name="menu-item-custom-action"></a><span data-ttu-id="04242-169">Дополнительное действие в меню</span><span class="sxs-lookup"><span data-stu-id="04242-169">Menu Item Custom Action</span></span>

<span data-ttu-id="04242-p113">Добавляет элемент проекта, который расширяет интерфейс хост-сайта путем добавления действия к меню списка. Настраиваемое действие для меню содержит файл Elements.xml, который определяет свойства действия. Подробнее об этом:  [Выполнение пользовательских действий для развертывания надстроек для SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="04242-p113">Adds a project item that extends the UI of its host site by adding an action to a list menu. The menu custom action contains an Elements.xml file, which you use to define the properties of the action. For more information, see  [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
 

 

### <a name="module"></a><span data-ttu-id="04242-173">Модуль</span><span class="sxs-lookup"><span data-stu-id="04242-173">Module</span></span>

<span data-ttu-id="04242-p114">Добавляет модуль в надстройку SharePoint. Модули — это, по сути, контейнеры, которые можно использовать для добавления других файлов при развертывании надстройки SharePoint. Для добавления файл копируется в модуль в **обозревателе решений**. В файл Elements.xml для модуля автоматически добавляется ссылка на файл, которая указывает путь к новому файлу и его URL-адрес. Вы можете удалить файл Sample.txt, который включен в модуль, так как он приведен только для примера.</span><span class="sxs-lookup"><span data-stu-id="04242-p114">Adds a module project item to your SharePoint Add-in. Modules are basically containers that you can use to include other files when you deploy your SharePoint Add-in. To add a file, you copy it into the project under the module in  **Solution Explorer**. A reference to the file is automatically added to the Elements.xml file for the module, and the reference specifies the path and URL of the new file. You can delete the Sample.txt file that's included with the module because it's included only for example purposes.</span></span>
 

 

### <a name="remote-event-receiver"></a><span data-ttu-id="04242-179">Удаленный приемник событий</span><span class="sxs-lookup"><span data-stu-id="04242-179">Remote Event Receiver</span></span>

<span data-ttu-id="04242-p115">Добавляет в решение элемент проекта для удаленной приемник событий в Надстройка SharePoint и проекта веб-приложения, если такой проект еще не создан. Веб-приложение содержит веб-службу, связанную с удаленным приемником событий в Надстройка SharePoint. Веб-служба содержит файл кода Visual Basic или Visual C#, который выполняется, если в Надстройка SharePoint возникает событие списка, элемента списка или веб-элемента. Если веб-приложение присутствует, оно связывается с Надстройка SharePoint, после чего веб-служба добавляется к этому приложению. Подробнее об этом:  [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="04242-p115">Adds a project item for a remote event receiver to your SharePoint Add-in and a web application project to your solution, if such a project isn't already present. The web application contains a web service that's associated with the remote event receiver in your SharePoint Add-in. The web service contains a Visual Basic or Visual C# code file whose code executes when a list, a list item, or a web item event occurs in the SharePoint Add-in. If a web application is present, it's associated with the SharePoint Add-in, and the web service is added to that application. For more information, see  [Handle events in SharePoint Add-ins](handle-events-in-sharepoint-add-ins.md).</span></span>
 

 

### <a name="ribbon-custom-action"></a><span data-ttu-id="04242-185">Дополнительное действие на ленте</span><span class="sxs-lookup"><span data-stu-id="04242-185">Ribbon Custom Action</span></span>

<span data-ttu-id="04242-p116">Добавляет элемент проекта, который расширяет интерфейс хост-сайта путем добавления действия к ленте. Настраиваемое действие для ленты содержит файл Elements.xml, который определяет свойства действия. Подробнее об этом:  [Выполнение пользовательских действий для развертывания надстроек для SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="04242-p116">Adds a project item that extends the UI of its host site by adding an action to a ribbon. The ribbon custom action contains an Elements.xml file, which defines the properties of the action. For more information, see  [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
 

 

### <a name="search-configuration"></a><span data-ttu-id="04242-189">Конфигурация поиска</span><span class="sxs-lookup"><span data-stu-id="04242-189">Search Configuration</span></span>

<span data-ttu-id="04242-190">Добавляет элемент проекта, который позволяет импортировать пользовательские параметры конфигурации поиска, экспортированные с сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="04242-190">Adds a project item that enables you to import custom search configuration settings that have been exported from a SharePoint site.</span></span>
 

 

### <a name="site-column"></a><span data-ttu-id="04242-191">Столбец сайта</span><span class="sxs-lookup"><span data-stu-id="04242-191">Site Column</span></span>

<span data-ttu-id="04242-p117">Добавляет элемент проекта для столбца сайта в Надстройка SharePoint. Столбец сайта содержит файл Elements.xml, который определяет свойства  `Field` столбца сайта, включая следующие данные.</span><span class="sxs-lookup"><span data-stu-id="04242-p117">Adds a project item for a site column to your SharePoint Add-in. The site column contains an Elements.xml file that defines the  `Field` properties of the site column, including the following data.</span></span>
 

 


|<span data-ttu-id="04242-194">**Имя свойства**</span><span class="sxs-lookup"><span data-stu-id="04242-194">**Property Name**</span></span>|<span data-ttu-id="04242-195">**Описание**</span><span class="sxs-lookup"><span data-stu-id="04242-195">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="04242-196">ID</span><span class="sxs-lookup"><span data-stu-id="04242-196">ID</span></span>|<span data-ttu-id="04242-197">Уникальный идентификатор GUID для столбца сайта.</span><span class="sxs-lookup"><span data-stu-id="04242-197">A unique GUID value for the site column.</span></span>|
|<span data-ttu-id="04242-198">Name</span><span class="sxs-lookup"><span data-stu-id="04242-198">Name</span></span>|<span data-ttu-id="04242-199">Уникальное имя, которое используется для обращения к столбцу сайта.</span><span class="sxs-lookup"><span data-stu-id="04242-199">A unique name that's used to reference the site column.</span></span>|
|<span data-ttu-id="04242-200">DisplayName</span><span class="sxs-lookup"><span data-stu-id="04242-200">DisplayName</span></span>|<span data-ttu-id="04242-201">Понятное имя, которое отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="04242-201">A friendly name that appears in the UI.</span></span>|
|<span data-ttu-id="04242-202">Type</span><span class="sxs-lookup"><span data-stu-id="04242-202">Type</span></span>|<span data-ttu-id="04242-203">Тип данных столбца сайта на основе **SPFieldType**, например логический, подстановка или текст.</span><span class="sxs-lookup"><span data-stu-id="04242-203">The data type of the site column based on  **SPFieldType**, such as Boolean, lookup, or text.</span></span>|
|<span data-ttu-id="04242-204">Required</span><span class="sxs-lookup"><span data-stu-id="04242-204">Required</span></span>|<span data-ttu-id="04242-205">Если столбец является обязательным, свойству присваивается значение **True**; в противном случае — значение **False**.</span><span class="sxs-lookup"><span data-stu-id="04242-205">If the column is required, the property is set to  **True**; otherwise, the property is set to  **False**.</span></span>|
|<span data-ttu-id="04242-206">Group</span><span class="sxs-lookup"><span data-stu-id="04242-206">Group</span></span>|<span data-ttu-id="04242-p118">Указывает имя группы, которой назначен столбец сайта. Значение по умолчанию для этого свойства — **Настраиваемые столбцы сайта**.</span><span class="sxs-lookup"><span data-stu-id="04242-p118">Specifies the name of the group to which the site column is assigned. The default value for this property is  **Custom Site Columns**.</span></span>|
<span data-ttu-id="04242-209">Дополнительные сведения см. в статье [Базовый элемент разработки: типы столбцов и полей](http://msdn.microsoft.com/library/58548ade-e439-4931-82a2-fa29bd5afdb7%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="04242-209">For more information, see  [Building Block: Columns and Field Types](http://msdn.microsoft.com/library/58548ade-e439-4931-82a2-fa29bd5afdb7%28Office.15%29.aspx).</span></span>
 

 

### <a name="workflow"></a><span data-ttu-id="04242-210">Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="04242-210">Workflow</span></span>

<span data-ttu-id="04242-p119">Добавляет элемент проекта для рабочего процесса Microsoft Azure в Надстройка SharePoint. Дополнительные сведения см. в статье  [Рабочие процессы в SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx). При добавлении этого типа элемента необходимо указать имя рабочего процесса, а также то, применяется ли этот рабочий процесс к списку или сайту. Как можно понять из имени этого типа, рабочий процесс списка работает только со списками, а рабочий процесс сайта только с сайтами SharePoint. При создании рабочего процесса вы также указываете, следует ли автоматически привязывать процесс к спискам и библиотекам, и, если это так, то к каким. Для каждой добавленной вами связи в проект рабочего процесса добавляется файл. Рабочий процесс содержит следующие файлы.</span><span class="sxs-lookup"><span data-stu-id="04242-p119">Adds a project item for a Microsoft Azure workflow to your SharePoint Add-in. For more information, see  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx). When you add this type of item, you specify a name for the workflow and whether it's a list or site workflow. As the names suggest, a list workflow works only with a list, and a site workflow works only with the SharePoint site. When you're creating the workflow, you also specify whether to automatically associate the workflow with lists and libraries, and if so, which ones. For every association that you add, a file for it is added to the workflow project. A workflow contains the following files.</span></span>
 

 


|<span data-ttu-id="04242-218">**Имя файла**</span><span class="sxs-lookup"><span data-stu-id="04242-218">**File Name**</span></span>|<span data-ttu-id="04242-219">**Описание**</span><span class="sxs-lookup"><span data-stu-id="04242-219">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="04242-220">Elements.xml</span><span class="sxs-lookup"><span data-stu-id="04242-220">Elements.xml</span></span>|<span data-ttu-id="04242-p120">Определяет конфигурацию рабочего процесса и содержащиеся в нем файлы (workflow.xaml и файлы связи), а также свойства каждого файла (URL-адрес, тип и путь). Для каждого файла, добавляемого в проект рабочего процесса, в файл Elements.xml добавляется соответствующий раздел. Для файлов связи в рабочих процессах списка требуется список, чтобы у них была ссылка на маркер. В рабочих процессах сайта для сайта добавляется GUID. **Внимание!** Так как Visual Studio хранит элементы в файле Elements.xml, рекомендуем не изменять его, не зная о последствиях.</span><span class="sxs-lookup"><span data-stu-id="04242-p120">Specifies the configuration of the workflow and the files that it contains, such as the workflow.xaml file and association files, and the properties of each file, such as its URL, its type, and its path. For each file that's added to the workflow project, a corresponding section is added to the Elements.xml file for the workflow. Association files in list workflows require a list, so they have a reference to the list token. In a site workflow, a GUID is added for the site. **Caution**  Because Visual Studio maintains the items in the Elements.xml file, we recommend against changing it unless you're familiar with the impact of the changes.</span></span> |
|<span data-ttu-id="04242-226">Workflow.xaml</span><span class="sxs-lookup"><span data-stu-id="04242-226">Workflow.xaml</span></span>|<span data-ttu-id="04242-p121">Представляет конструктор рабочего процесса. В этом файле вы добавляете в рабочий процесс действия, указываете их код и свойства.</span><span class="sxs-lookup"><span data-stu-id="04242-p121">Represents the designer for the workflow. In this file, you add actions to the workflow and set their code and properties.</span></span>|
|<span data-ttu-id="04242-229">WorkflowStartAssociation</span><span class="sxs-lookup"><span data-stu-id="04242-229">WorkflowStartAssociation</span></span>|<span data-ttu-id="04242-p122">Вручную запускает рабочий процесс в SharePoint. Этот файл добавляется в проект рабочего процесса при установке флажка **Пользователь запускает рабочий процесс вручную** в мастере настройки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="04242-p122">Manually starts the workflow on SharePoint. This file is added to the workflow project if you select the  **A user manually starts the workflow** check box in the workflow wizard.</span></span>|
|<span data-ttu-id="04242-232">ItemAddedAssociation</span><span class="sxs-lookup"><span data-stu-id="04242-232">ItemAddedAssociation</span></span>|<span data-ttu-id="04242-p123">Запускает рабочий процесс автоматически, когда пользователь создает элемент на сайте или в списке (в зависимости от типа рабочего процесса). Этот файл добавляется в проект рабочего процесса при выборе флажка **Рабочий процесс запускается автоматически при добавлении элемента** в мастере настройке рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="04242-p123">Starts the workflow automatically if one is present when a user creates an item in the site or list (depending on the workflow type). This file is added to the workflow project if you select the  **The workflow starts automatically when an item is added** check box in the workflow wizard.</span></span>|
|<span data-ttu-id="04242-235">ItemUpdatedAssociation</span><span class="sxs-lookup"><span data-stu-id="04242-235">ItemUpdatedAssociation</span></span>|<span data-ttu-id="04242-p124">Запускает рабочий процесс автоматически, когда пользователь изменяет элемент на сайте или в списке (в зависимости от типа рабочего процесса). Этот файл добавляется в проект рабочего процесса при выборе флажка **Рабочий процесс запускается автоматически при изменении элемента** в мастере настройки рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="04242-p124">Starts the workflow automatically, if one is present when a user changes an item in the site or list (depending on the workflow type). This file is added to the workflow project if you select the  **The workflow starts automatically when an item is changed** check box in the workflow wizard.</span></span>|
|<span data-ttu-id="04242-238">WorkflowHistoryList</span><span class="sxs-lookup"><span data-stu-id="04242-238">WorkflowHistoryList</span></span>|<span data-ttu-id="04242-239">Представляет файл, который добавляется в рабочий проект, если вы создаете список журнала для рабочего процесса в мастере создания рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="04242-239">Represents the file that's added to the workflow project if you create a history list for the workflow in the workflow wizard.</span></span>|
|<span data-ttu-id="04242-240">WorkflowTaskList</span><span class="sxs-lookup"><span data-stu-id="04242-240">WorkflowTaskList</span></span>|<span data-ttu-id="04242-241">Представляет файл, который добавляется в рабочий проект, если вы создаете список задач для рабочего процесса в мастере создания рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="04242-241">Represents the file that's added to the workflow project if you create a task list for the workflow in the workflow wizard.</span></span>|

### <a name="workflow-custom-activity"></a><span data-ttu-id="04242-242">Дополнительное действие рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="04242-242">Workflow Custom Activity</span></span>

<span data-ttu-id="04242-p125">Добавляет элемент проекта для настраиваемой активности рабочего процесса в Надстройка SharePoint. Добавив такую активность, вы сможете создавать дополнительные действия в рабочем процессе, которые затем можно импортировать как дополнительные действия в SharePoint Designer 2013. Настраиваемая активность содержит файл Elements.xml, который определяет свойства действия, и XAML-файл для конструктора рабочих процессов. Подробнее об этом:  [Рабочие процессы в SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="04242-p125">Adds a project item for a workflow custom activity to your SharePoint Add-in. By adding a workflow custom activity, you can create additional workflow actions that you can then import as custom actions in SharePoint Designer 2013. The workflow custom activity contains an Elements.xml file, which defines the properties of the action, and a .xaml file for the workflow designer. For more information, see  [Workflows in SharePoint](http://msdn.microsoft.com/library/e0602371-ae22-44be-8a7e-9e47e9f046d6%28Office.15%29.aspx).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="04242-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="04242-247">Additional resources</span></span>
<span data-ttu-id="04242-248"><a name="SP15Projecttemplates_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="04242-248"></span></span>


-  [<span data-ttu-id="04242-249">Средства и среды для разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="04242-249">Tools and environments for developing SharePoint Add-ins</span></span>](tools-and-environments-for-developing-sharepoint-add-ins.md)
    
 
