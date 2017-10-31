---
title: "Краткий обзор объектной модели SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: c703d0edf04b77313d6a7276df4e444dee2250cf
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-a-quick-overview-of-the-sharepoint-object-model"></a><span data-ttu-id="d5a4b-102">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5a4b-102">Get a quick overview of the SharePoint object model</span></span>
<span data-ttu-id="d5a4b-103">Краткое описание некоторых основных классов в объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-103">Get a quick introduction to some of the major classes in the SharePoint object model.</span></span>
 

 <span data-ttu-id="d5a4b-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="d5a4b-107">Это четвертая часть серии статей, посвященной основам разработки надстроек, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-107">This is the fourth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="d5a4b-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="d5a4b-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="d5a4b-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="d5a4b-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
    
 
-  [<span data-ttu-id="d5a4b-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="d5a4b-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in.md)
    
 

 <span data-ttu-id="d5a4b-p102">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeSharePointWriteOps.sln.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p102">**Note**  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeSharePointWriteOps.sln file.</span></span>
 

<span data-ttu-id="d5a4b-p103">В данной статье мы немного отвлечемся от программирования и кратко рассмотрим клиентскую объектную модель (CSOM) SharePoint. Это большая модель. Она хорошо задокументирована на MSDN в виде справочных статей, инструкций и примеров кода. В этой статье мы предоставим вам только самые поверхностные сведения. Тем не менее благодаря даже такому краткому рассказу большая часть кода, с которым вы столкнетесь в этой серии статей, станет намного понятнее.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p103">In this article you'll take a brief break from coding to get a quick overview of the SharePoint Client-side Object Model (CSOM). This model is large and well-documented in MSDN with reference topics, "how to"s, and code samples. In this article, we can only provide the tip of the tip of the tip of the iceberg. But even a very short introduction will make much of the code you will see in this series a lot less mysterious.</span></span> 
 

## <a name="content-hierarchy"></a><span data-ttu-id="d5a4b-117">Иерархия содержимого</span><span class="sxs-lookup"><span data-stu-id="d5a4b-117">Content Hierarchy</span></span>

<span data-ttu-id="d5a4b-p104">В таблице ниже показана иерархия содержимого в SharePoint, а также представляющие его классы CSOM. У каждого из этих объектов имеется дочерний объект указанного непосредственно под ним типа.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p104">The table below shows the hierarchy of content in SharePoint and the CSOM classes that represent them. Each of these entities has children of the type just below it.</span></span>
 

|<span data-ttu-id="d5a4b-120">**Объект**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-120">**Entity**</span></span>|<span data-ttu-id="d5a4b-121">**Класс**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-121">**Class**</span></span>|<span data-ttu-id="d5a4b-122">**Замечания**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-122">**Remarks**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="d5a4b-123">Локальная ферма SharePoint или подписка на SharePoint Online (также называемая клиентом)</span><span class="sxs-lookup"><span data-stu-id="d5a4b-123">SharePoint on-premises farm or SharePoint Online subscription (also called a tenant)</span></span>||<span data-ttu-id="d5a4b-p105">К этому уровню CSOM можно получить только ограниченный программный доступ. Например, нет классов Farm, Subscription или Tenant. (в серверной объектной модели SharePoint, которую невозможно использовать в надстройках, имеется программный доступ к этим объектам.)</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p105">There is only limited programmatic access to this level in CSOM. There is no Farm or Subscription or Tenant class, for example. (SharePoint's server-side object model, which cannot be used in add-ins, enables programmatic access to these entities.)</span></span>|
|<span data-ttu-id="d5a4b-127">семейство веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="d5a4b-127">site collection</span></span>|<span data-ttu-id="d5a4b-128">**Site**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-128">**Site**</span></span>|<span data-ttu-id="d5a4b-p106">Семейство веб-сайтов, сгруппированных вместе большей частью по причинам, связанным с администрированием, а также для того чтобы в нем содержались компоненты SharePoint, например эталонные страницы с фирменным оформлением или настраиваемые группы безопасности, которые можно применить ко всем дочерним веб-сайтам. Все веб-сайты принадлежат каким-либо семействам веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p106">A collection of websites that are grouped together for mainly administrative reasons and to house SharePoint components, such as branded master pages, or custom security groups, that can be applied to all the child websites. All websites belong to some site collection.</span></span>|
|<span data-ttu-id="d5a4b-131">веб-сайт</span><span class="sxs-lookup"><span data-stu-id="d5a4b-131">website</span></span>|<span data-ttu-id="d5a4b-132">**Web**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-132">**Web**</span></span>|<span data-ttu-id="d5a4b-p107">Набор страниц и компонентов SharePoint. Может включать дочерние веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p107">A set of pages and SharePoint components. Can have subwebsites.</span></span>|
|<span data-ttu-id="d5a4b-135">список</span><span class="sxs-lookup"><span data-stu-id="d5a4b-135">list</span></span>|<span data-ttu-id="d5a4b-136">**List**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-136">**List**</span></span>|<span data-ttu-id="d5a4b-p108">На этом уровне также находятся библиотеки документов и другие библиотеки файлов. Библиотека документов — это особый тип списка, в котором каждая строка содержит вложенный документ, а в других столбцах содержатся данные об этом документе, например сведения об авторе, дате и времени последнего изменения документа и о том, кто последним извлекал его.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p108">Document libraries and other kinds of file libraries are also at this level. A document library is a special kind of list in which each row includes an attached document, and the other columns are data about the document, such as its author, when it was last edited, and who has it checked out.</span></span> |
|<span data-ttu-id="d5a4b-139">элемент списка</span><span class="sxs-lookup"><span data-stu-id="d5a4b-139">list item</span></span>|<span data-ttu-id="d5a4b-140">**ListItem**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-140">**ListItem**</span></span>|<span data-ttu-id="d5a4b-p109">Строка в списке (то есть элемент списка), в полях которой записаны определенные значения. Тоже имеет тип. См. следующую строку.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p109">A row in a list—that is, a list item—with particular values in the fields of the row. Also has a type. See next row.</span></span> |
|<span data-ttu-id="d5a4b-144">элемент списка</span><span class="sxs-lookup"><span data-stu-id="d5a4b-144">list item</span></span>|<span data-ttu-id="d5a4b-145">**Тип контента**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-145">**Content Type**</span></span>|<span data-ttu-id="d5a4b-p110">Тип элемента списка. Представлен классом **ContentType**. По сути каждый тип элемента списка представляет собой набор столбцов и метаданных. Самый простой их них — встроенный тип контента **Item**. Все другие типы контента являются производными от типа **Item**. В SharePoint имеется много встроенных типов контента, например Event и Announcement.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p110">The type of a list item. These are represented by the  **ContentType** class. Each is basically a set of columns and metadata. The simplest is the built-in **Item** content type. All other content types are derived from **Item**. SharePoint includes many built-in content types, such as Event and Announcement.</span></span> |
|<span data-ttu-id="d5a4b-152">столбец</span><span class="sxs-lookup"><span data-stu-id="d5a4b-152">column</span></span>|<span data-ttu-id="d5a4b-153">**Поле**</span><span class="sxs-lookup"><span data-stu-id="d5a4b-153">**Field**</span></span>|<span data-ttu-id="d5a4b-154">Объект **Field** включает не только данные о базовом типе данных, но и сведения о том, каким образом форматировать и отображать данные в формах, например в формах создания, отображения и изменения элементов списка.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-154">A  **Field** object includes not only information about the underlying data type, but also information about how the data is formatted and rendered on forms, such as the forms for creating, displaying, and editing specific list items.</span></span>|

 

 
<span data-ttu-id="d5a4b-155">Вы можете программным способом создавать настраиваемые списки, типы контента, типы столбцов и элементы списков.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-155">You can programmatically create custom lists, content types, column types, and list items.</span></span> 
 

 
<span data-ttu-id="d5a4b-156">Помимо доступа к содержимому CSOM предоставляет доступ к пользователям, группам, ролям и разрешениям, таксономии, поиску и многому другому.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-156">In addition to content, the CSOM gives you access to users, groups, roles &amp; permissions, taxonomy, search, and more.</span></span>
 

 

## <a name="client-side-runtime-and-batching"></a><span data-ttu-id="d5a4b-157">Клиентская среда выполнения и пакетная обработка</span><span class="sxs-lookup"><span data-stu-id="d5a4b-157">Client-side runtime and batching</span></span>
<span data-ttu-id="d5a4b-158"><a name="CSOMBatching"> </a></span><span class="sxs-lookup"><span data-stu-id="d5a4b-158"><a name="CSOMBatching"> </a></span></span>

<span data-ttu-id="d5a4b-p111">В CSOM используется система пакетной обработки. Система преобразовывает блоки управляемого кода в XML и отправляет их на сервер в одном HTTP-запросе. Для каждой команды система совершает вызов соответствующей серверной объектной модели, а сервер возвращает клиенту отклик в формате нотации объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p111">CSOM uses a batching system. Chunks of managed code is converted into XML and sent to the server in a single HTTP request. For every command, a corresponding server object model call is made, and the server returns a response to the client in JavaScript Object Notation (JSON) format.</span></span> 
 

 
<span data-ttu-id="d5a4b-p112">Код SharePoint на клиенте начинается с получения клиентом объекта контекста, представляющего текущий контекст запроса, который включает идентификатор веб-сайта SharePoint (и его родительского семейства веб-сайтов). С помощью этого контекста вы можете получить доступ к объектам CSOM. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p112">SharePoint code on a client begins by retrieving a client context object that represents the current request context, including the identity of the SharePoint website (and its parent site collection) and through this context you can obtain access to CSOM objects. The following is the basic structure that you will see again and again. Note the following about this code:</span></span>
 

 

- <span data-ttu-id="d5a4b-p113">Объект  `spContext` имеет тип **SharePointContext** и определен в файле SharePointContext.cs (или в файле SharePointContext.vb), который создается Инструменты разработчика Office для Visual Studio. Вы можете изменять этот файл, но не так часто, как хотелось бы. Для многих проектов надстройки SharePoint этот файл и файл TokenHelper.cs (или файл TokenHelper.vb), который также создается с помощью средств, эффективно работает в качестве расширений CSOM.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p113">The  `spContext` object is of the type **SharePointContext** and is defined in a the SharePointContext.cs (or .vb) file that is generated by the Office Developer Tools for Visual Studio. This file can be modified, but it is not often that you need to do so. For most SharePoint Add-in projects, this file, and the TokenHelper.cs (or .vb) file that is also generated by the tools, effectively function as extensions of CSOM itself.</span></span>
    
 
- <span data-ttu-id="d5a4b-168">Объект `clientContext` относится к типу **ClientContext** модели CSOM.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-168">The  `clientContext` object is the CSOM type **ClientContext**.</span></span>
    
 
- <span data-ttu-id="d5a4b-p114">Метод **ExecuteQuery** объединяет код операции CRUD в XML-сообщение, которое затем отправляет на сервер SharePoint. Там оно преобразуется в эквивалентный код серверной объектной модели, а затем выполняется.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p114">The  **ExecuteQuery** method bundles up the CRUD operation code in and XML message that it sends to the SharePoint server. There it is translated into equivalent server-side object model code and executed.</span></span>
    
 



```C#
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    // CRUD operation or query code goes here.

    clientContext.ExecuteQuery();
}
```

<span data-ttu-id="d5a4b-p115">В одной из предыдущих статей этой серии был пример этого шаблона (в показанном ниже методе  `GetLocalEmployeeName`). Обратите внимание на указанные ниже особенности этого метода.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p115">There was an example of this pattern in the previous article of this series, in the  `GetLocalEmployeeName` method shown below. Note the following about this method:</span></span>
 

 

- <span data-ttu-id="d5a4b-p116">Первые две строки в блоке **using** получают ссылки на список и объект элемента списка. Но на самом деле, когда эти строки выполняются в клиентской среде выполнения SharePoint, они просто преобразовываются в формат XML. Метод **ExecuteQuery** отправляет полученный код XML на сервер.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p116">The first two lines in the  **using** block appear to get references to the list and the list item object. But actually when these lines execute in the SharePoint client-side runtime, they are simply translated into an XML format. The **ExecuteQuery** method sends that XML to the server.</span></span>
    
 
-  <span data-ttu-id="d5a4b-p117">Метод **Load** добавляет дополнительную информацию в сообщение: он сообщает серверу, что необходимо отправить указанный объект на клиент. Метод **ExecuteQuery** получает этот объект (в виде JSON) и использует его для инициализации переменной `selectedLocalEmployee` в клиенте. Последующий код клиентской части затем ссылается на этот объект **ListItem** и его члены. Как вы видите, следующая строка ссылается на значение поля Title (Название) элемента. Если не был вызван метод **Load**, то эта срока приведет к исключению, так как чтобы этот объект появился в клиентской части, необходимо загрузить его.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-p117">The **Load** method adds something extra to the message: it tells the server to send the specified object down to the client. The **ExecuteQuery** method receives this object (as JSON) and uses it to initialize the client-side `selectedLocalEmployee` variable. Subsequent client-side code and then reference that **ListItem** object and its members. As you can see, the next line references the value of the item's "Title" field. This line would have thrown an exception if the **Load** method had not been called because the object doesn't really exist on the client-side until its loaded.</span></span>
    
 



```C#
private string GetLocalEmployeeName()
{
    ListItem localEmployee;

    using (var clientContext = spContext.CreateUserClientContextForSPHost())
    {
        List localEmployeesList = clientContext.Web.Lists.GetByTitle("Local Employees");
        selectedLocalEmployee = localEmployeesList.GetItemById(listItemID);
        clientContext.Load(selectedLocalEmployee);
        clientContext.ExecuteQuery();
    }
    return localEmployee["Title"].ToString();
}
```


## 
<span data-ttu-id="d5a4b-181"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="d5a4b-181"><a name="Nextsteps"> </a></span></span>

 <span data-ttu-id="d5a4b-182">В следующей статье [Добавление операций записи SharePoint в надстройку, размещаемую у поставщика](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md) мы вернемся к программированию и узнаем, как записывать данные в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d5a4b-182">In the next article, we get back to coding and learn how to write data to SharePoint: [Add SharePoint write operations to the provider-hosted add-in](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)</span></span>
 

 

