---
title: "Подготовка ресурсов SharePoint с пакетом решения"
description: "Цепочка инструментов SharePoint Framework позволяет упаковывать и развертывать элементы SharePoint с пакетом клиентского решения. Подготовка этих элементов затем выполняется при установке клиентского решения на сайте."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: 03d69afdc7f66a9c1e95a4832b4f591a79b998aa
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="provision-sharepoint-assets-with-your-solution-package"></a><span data-ttu-id="5101e-104">Подготовка ресурсов SharePoint с пакетом решения</span><span class="sxs-lookup"><span data-stu-id="5101e-104">Provision SharePoint assets with your solution package</span></span>

<span data-ttu-id="5101e-105">Иногда требуется подготовить список или библиотеку документов SharePoint вместе с пакетом клиентского решения, чтобы они были доступны клиентским компонентам, таким как веб-части.</span><span class="sxs-lookup"><span data-stu-id="5101e-105">At times, you may need to provision a SharePoint list or a document library along with your client-side solution package so that that list or library is available for your client-side components, such as web parts. SharePoint Framework toolchain allows you to package and deploy SharePoint items with your client-side solution package. These items are then provisioned when the client-side solution is installed on a site.</span></span> <span data-ttu-id="5101e-106">Цепочка инструментов SharePoint Framework позволяет упаковывать и развертывать элементы SharePoint с пакетом клиентского решения.</span><span class="sxs-lookup"><span data-stu-id="5101e-106">SharePoint Framework toolchain allows you to package and deploy SharePoint items with your client-side solution package.</span></span> <span data-ttu-id="5101e-107">Подготовка этих элементов затем выполняется при установке клиентского решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="5101e-107">These items are then provisioned when the client-side solution is installed on a site.</span></span> 

<span data-ttu-id="5101e-108">Узнать больше о возможностях подготовки ресурсов можно из веб-трансляции на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS).</span><span class="sxs-lookup"><span data-stu-id="5101e-108">You can also find details on the provisioning options from a SharePoint PnP webcast available from [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS).</span></span> 

<a href="https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS">
<img src="../../images/spfx-webcast-youtube-provision-feature-elements.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="provision-items-using-javascript-code"></a><span data-ttu-id="5101e-109">Подготовка элементов с помощью кода JavaScript</span><span class="sxs-lookup"><span data-stu-id="5101e-109">Provisioning items using JavaScript code</span></span>

<span data-ttu-id="5101e-110">Хотя элементы SharePoint можно создавать в компоненте (например, веб-части) с помощью кода JavaScript, эта возможность ограничена контекстом текущего пользователя компонента.</span><span class="sxs-lookup"><span data-stu-id="5101e-110">While it is possible to create SharePoint items using JavaScript code in your component, such as web parts, it is limited to the context of the current user using that component.</span></span> <span data-ttu-id="5101e-111">Если у пользователя нет разрешений на создание или изменение элементов SharePoint, код JavaScript не подготовит эти элементы.</span><span class="sxs-lookup"><span data-stu-id="5101e-111">If the user doesn't have sufficient permissions to create or modify SharePoint items, the JavaScript code does not provision those items.</span></span> <span data-ttu-id="5101e-112">В таких случаях для подготовки в контексте c повышенными привилегиями элементы SharePoint необходимо упаковать и развернуть с пакетом решения.</span><span class="sxs-lookup"><span data-stu-id="5101e-112">In such cases, when you want to provision SharePoint items in an elevated context, you must package and deploy the items along with your solution package.</span></span>

## <a name="provision-sharepoint-items-in-your-solution"></a><span data-ttu-id="5101e-113">Подготовка элементов SharePoint в решении</span><span class="sxs-lookup"><span data-stu-id="5101e-113">Create SharePoint items in your solution</span></span>

<span data-ttu-id="5101e-114">С клиентским пакетом решения можно подготовить к работе следующие ресурсы SharePoint:</span><span class="sxs-lookup"><span data-stu-id="5101e-114">The following SharePoint assets can be provisioned along with your client-side solution package:</span></span>

* <span data-ttu-id="5101e-115">поля;</span><span class="sxs-lookup"><span data-stu-id="5101e-115">Fields</span></span>
* <span data-ttu-id="5101e-116">типы контента;</span><span class="sxs-lookup"><span data-stu-id="5101e-116">Content types</span></span>
* <span data-ttu-id="5101e-117">экземпляры списков;</span><span class="sxs-lookup"><span data-stu-id="5101e-117">List instances</span></span>
* <span data-ttu-id="5101e-118">экземпляры списков со специальной схемой.</span><span class="sxs-lookup"><span data-stu-id="5101e-118">List instances with custom schema</span></span>

### <a name="fields"></a><span data-ttu-id="5101e-119">Поля</span><span class="sxs-lookup"><span data-stu-id="5101e-119">Fields</span></span>

<span data-ttu-id="5101e-p104">Поле (столбец сайта) представляет атрибут, или фрагмент метаданных, который пользователь применяет в управлении списком или типом контента, к которому добавил этот столбец. Это определение столбца, или шаблон, которое вы можете назначить нескольким спискам для нескольких сайтов SharePoint. Столбцы сайтов избавляют от лишней работы и помогают обеспечить согласованность метаданных на сайтах и в списках.</span><span class="sxs-lookup"><span data-stu-id="5101e-p104">A field or a site column represents an attribute, or piece of metadata, that the user wants to manage for the items in the list or content type to which they added the column. It is a reusable column definition, or template, that you can assign to multiple lists across multiple SharePoint sites. Site columns decrease rework and help you ensure consistency of metadata across sites and lists.</span></span> 

<span data-ttu-id="5101e-123">Допустим, вы определили столбец сайта под названием "Клиент".</span><span class="sxs-lookup"><span data-stu-id="5101e-123">For example, suppose you define a site column named Customer.</span></span> <span data-ttu-id="5101e-124">Пользователи могут добавлять этот столбец к своим спискам и ссылаться на него в своих типах контента.</span><span class="sxs-lookup"><span data-stu-id="5101e-124">Users can add that column to their lists and reference it in their content types.</span></span> <span data-ttu-id="5101e-125">Это гарантирует, что у столбца всегда будут одни и те же атрибуты (хотя бы вначале), где бы он ни находился.</span><span class="sxs-lookup"><span data-stu-id="5101e-125">This ensures that the column has the same attributes—at least to start with—wherever it appears.</span></span>

<span data-ttu-id="5101e-126">Определяя новое поле в своем решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент Field (поле)](https://msdn.microsoft.com/en-us/library/aa979575(v=office.15).aspx).</span><span class="sxs-lookup"><span data-stu-id="5101e-126">You can refer to the schema and attributes in the [Field Element](https://msdn.microsoft.com/en-us/library/aa979575(v=office.15).aspx) documentation to define a new field in your solution.</span></span> 

<span data-ttu-id="5101e-127">Ниже приведен пример нового поля DateTime.</span><span class="sxs-lookup"><span data-stu-id="5101e-127">Below is an example of a new DateTime field:</span></span>

```xml
<Field ID="{1511BF28-A787-4061-B2E1-71F64CC93FD5}"
            Name="DateOpened"
            DisplayName="Date Opened"
            Type="DateTime"
            Format="DateOnly"
            Required="FALSE"
            Group="Financial Columns">
        <Default>[today]</Default>
    </Field>
```

### <a name="content-types"></a><span data-ttu-id="5101e-128">Типы контента</span><span class="sxs-lookup"><span data-stu-id="5101e-128">Content types</span></span>

<span data-ttu-id="5101e-p106">Тип контента — это многоразовая коллекция метаданных (столбцов), настроек поведения и других настроек для категории элементов в списке SharePoint или документов в библиотеке документов SharePoint. Типы контента позволяют централизованно управлять настройками для категории сведений.</span><span class="sxs-lookup"><span data-stu-id="5101e-p106">A content type is a reusable collection of metadata (columns), behavior, and other settings for a category of items or documents in a SharePoint list or document library. Content types enable you to manage the settings for a category of information in a centralized, reusable way.</span></span>

<span data-ttu-id="5101e-131">Представьте себе, что у вас есть три типа документов: авансовые отчеты, заказы на поставку и счета-фактуры.</span><span class="sxs-lookup"><span data-stu-id="5101e-131">For example, imagine a business situation in which you have three different types of documents: expense reports, purchase orders, and invoices.</span></span> <span data-ttu-id="5101e-132">Все три типа схожи тем, что представляют собой финансовые документы и содержат данные с денежными значениями.</span><span class="sxs-lookup"><span data-stu-id="5101e-132">All three types of documents have some characteristics in common; for one thing, they are all financial documents and contain data with values in currency.</span></span> <span data-ttu-id="5101e-133">Однако каждый из них имеет собственные требования к данным, шаблон и рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="5101e-133">Yet each type of document has its own data requirements, its own document template, and its own workflow.</span></span> 

<span data-ttu-id="5101e-134">Один из способов решения этой проблемы — создание четырех типов контента.</span><span class="sxs-lookup"><span data-stu-id="5101e-134">One solution to this business problem is to create four content types.</span></span> <span data-ttu-id="5101e-135">Первый тип контента, "Финансовый документ", может включать требования к данным, общие для всех финансовых документов в организации.</span><span class="sxs-lookup"><span data-stu-id="5101e-135">For example, you can define a list instance Finance Documents with a content type Financial Document that could encapsulate data requirements that are common to all financial documents in the organization.</span></span> <span data-ttu-id="5101e-136">Остальные три — "Авансовый отчет", "Заказ на покупку" и "Счет-фактура" — могут наследовать общие элементы от типа "Финансовый документ".</span><span class="sxs-lookup"><span data-stu-id="5101e-136">The remaining three, Expense Report, Purchase Order, and Invoice, could inherit common elements from Financial Document.</span></span> <span data-ttu-id="5101e-137">Кроме того, они могут определять отличительные особенности каждого типа, например особый набор метаданных, шаблон документа, используемый при создании элемента, и особую схему его обработки.</span><span class="sxs-lookup"><span data-stu-id="5101e-137">In addition, they could define characteristics that are unique to each type, such as a particular set of metadata, a document template to be used in creating a new item, and a specific workflow for processing an item.</span></span>

<span data-ttu-id="5101e-138">Определяя новый тип контента в решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент ContentType (тип контента)](https://msdn.microsoft.com/ru-RU/library/aa544268.aspx).</span><span class="sxs-lookup"><span data-stu-id="5101e-138">You can refer to the schema and attributes in the [Content Type Element](https://msdn.microsoft.com/ru-RU/library/aa544268.aspx) documentation to define a new content type in your solution.</span></span> 

<span data-ttu-id="5101e-139">Ниже приведен пример типа контента.</span><span class="sxs-lookup"><span data-stu-id="5101e-139">Below is an example of a content type:</span></span>

```xml
<ContentType ID="0x010042D0C1C200A14B6887742B6344675C8B" 
    Name="Cost Center" 
    Group="Financial Content Types" 
    Description="Financial Content Type">
    <FieldRefs>
        <FieldRef ID="{1511BF28-A787-4061-B2E1-71F64CC93FD5}" />
        <FieldRef ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}" /> 
    </FieldRefs>
</ContentType> 
```

### <a name="list-instances"></a><span data-ttu-id="5101e-140">Экземпляры списков</span><span class="sxs-lookup"><span data-stu-id="5101e-140">List instances</span></span>

<span data-ttu-id="5101e-p109">Списки — это ключевая, базовая функция сайта SharePoint. Они помогают группам собирать и отслеживать информацию, а также делиться ею. Многие приложения используют списки, созданные на сайте, чтобы хранить данные для реализации своего поведения. Экземпляр списка — это предопределенный список SharePoint с известным идентификатором. Вы можете настраивать и добавлять элементы в этих списках, создавать дополнительные списки с помощью доступных шаблонов, а также создавать специальные списки, указывая только нужные параметры и столбцы.</span><span class="sxs-lookup"><span data-stu-id="5101e-p109">Lists are a key, underlying feature of a SharePoint site. They enable teams to gather, track, and share information. Many applications rely on lists created at the site for data storage to implement their behaviors. A list instance is a predefined SharePoint list that has a well-known identifier. You can customize and add items to these lists, create additional lists from the list templates that are already available, and create custom lists with just the settings and columns that you choose.</span></span>

<span data-ttu-id="5101e-146">В SharePoint доступно несколько шаблонов списков (например, для календаря, списка контактов или задач).</span><span class="sxs-lookup"><span data-stu-id="5101e-146">SharePoint provides several list templates such as contact list, calendar, task list, and more.</span></span> <span data-ttu-id="5101e-147">С помощью этих шаблонов вы можете создавать экземпляры списков для своих веб-частей и других решений.</span><span class="sxs-lookup"><span data-stu-id="5101e-147">You can use these templates to create new list instances for your web parts or other components.</span></span> <span data-ttu-id="5101e-148">Например, вы можете определить экземпляр списка "Финансовые документы" на основе шаблона "Библиотека документов", чтобы обеспечить хранение соответствующих документов для веб-части.</span><span class="sxs-lookup"><span data-stu-id="5101e-148">SharePoint provides several list templates such as contact list, calendar, task list and more. You can use these templates to create new list instances for your web parts or other components. For example, you can define a list instance Finance Documents based on the Document Library template to store associated documents with your web part.</span></span> 

<span data-ttu-id="5101e-149">Определяя новый экземпляр списка в решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент ListInstance (экземпляр списка)](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx).</span><span class="sxs-lookup"><span data-stu-id="5101e-149">You can refer to the schema and attributes in the [List Instance Element](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx) documentation to define a list instance in your solution.</span></span>

<span data-ttu-id="5101e-150">Ниже приведен пример определения экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="5101e-150">Below is an example of a list instance definition:</span></span>

```xml
<ListInstance 
    FeatureId="00bfea71-e717-4e80-aa17-d0c71b360101"
    Title="Finance Records" 
    Description="Finance documents"
    TemplateType="101"
    Url="Lists/FinanceRecords">
</ListInstance>
```

### <a name="list-instances-with-custom-schema"></a><span data-ttu-id="5101e-151">экземпляры списков со специальной схемой.</span><span class="sxs-lookup"><span data-stu-id="5101e-151">List instances with custom schema</span></span>

<span data-ttu-id="5101e-152">Определять поля, типы контента и представления, используемые в экземпляре списка, можно с помощью специальной схемы.</span><span class="sxs-lookup"><span data-stu-id="5101e-152">You can use a custom list schema definition to define your fields, content types and views used in your list instance.</span></span> <span data-ttu-id="5101e-153">Ссылаться на специальную схему можно с помощью атрибута [CustomSchema](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx#sectionSection0) в элементе ListInstance.</span><span class="sxs-lookup"><span data-stu-id="5101e-153">You will use the  attribute in the list instance element to reference a custom schema for the list instance.</span></span> 

<span data-ttu-id="5101e-154">Например, вы можете определить тип экземпляра списка **Финансовые документы** как **Финансовый документ**, который может включать требования к данным, общие для всех финансовых документов в организации.</span><span class="sxs-lookup"><span data-stu-id="5101e-154">For example, you can define a list instance Finance Documents with a content type Financial Document that could encapsulate data requirements that are common to all financial documents in the organization.</span></span> 

<span data-ttu-id="5101e-155">Ниже приведен пример экземпляра списка, для определения которого используется специальная схема.</span><span class="sxs-lookup"><span data-stu-id="5101e-155">Below is an example of a list instance definition that uses a custom schema:</span></span>

```xml
<ListInstance 
    CustomSchema="schema.xml"
    FeatureId="00bfea71-de22-43b2-a848-c05709900100"
    Title="Cost Centers" 
    Description="Cost Centers"
    TemplateType="100"
    Url="Lists/CostCenters">
</ListInstance>
```

<br/>

<span data-ttu-id="5101e-156">А так выглядит специальная схема, которая определяет тип контента для определенного выше экземпляра списка:</span><span class="sxs-lookup"><span data-stu-id="5101e-156">And the custom schema definition that defines a content type for the list instance defined above:</span></span>

```xml
<List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE" Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
  <MetaData>
    <ContentTypes>
      <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
    </ContentTypes>
    <Fields></Fields>
    <Views>
      <View BaseViewID="1" Type="HTML" WebPartZoneID="Main" DisplayName="$Resources:core,objectiv_schema_mwsidcamlidC24;" DefaultView="TRUE" MobileView="TRUE" MobileDefaultView="TRUE" SetupPath="pages\viewpage.aspx" ImageUrl="/_layouts/images/generic.png" Url="AllItems.aspx">
        <XslLink Default="TRUE">main.xsl</XslLink>
        <JSLink>clienttemplates.js</JSLink>
        <RowLimit Paged="TRUE">30</RowLimit>
        <Toolbar Type="Standard" />
        <ViewFields>
          <FieldRef Name="LinkTitle"></FieldRef>
          <FieldRef Name="SPFxAmount"></FieldRef>
          <FieldRef Name="SPFxCostCenter"></FieldRef>
        </ViewFields>
        <Query>
          <OrderBy>
            <FieldRef Name="ID" />
          </OrderBy>
        </Query>
      </View>
    </Views>
    <Forms>
      <Form Type="DisplayForm" Url="DispForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      <Form Type="EditForm" Url="EditForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
      <Form Type="NewForm" Url="NewForm.aspx" SetupPath="pages\form.aspx" WebPartZoneID="Main" />
    </Forms>
  </MetaData>
</List>
```

## <a name="create-sharepoint-items-in-your-solution"></a><span data-ttu-id="5101e-157">Создание элементов SharePoint в решении</span><span class="sxs-lookup"><span data-stu-id="5101e-157">Create SharePoint items in your solution</span></span>

<span data-ttu-id="5101e-158">В пакете решения для подготовки и упаковки элементов SharePoint используются [компоненты SharePoint](https://msdn.microsoft.com/en-us/library/ee537350(office.14).aspx).</span><span class="sxs-lookup"><span data-stu-id="5101e-158">The solution package uses [SharePoint Features](https://msdn.microsoft.com/en-us/library/ee537350(office.14).aspx) to package and provision the SharePoint items.</span></span> <span data-ttu-id="5101e-159">Компонент — это контейнер, включающий один или несколько элементов SharePoint для подготовки.</span><span class="sxs-lookup"><span data-stu-id="5101e-159">A Feature is a container that includes one or more SharePoint items to provision.</span></span> <span data-ttu-id="5101e-160">Компонент содержит файл Feature.xml и один или несколько файлов манифеста элементов.</span><span class="sxs-lookup"><span data-stu-id="5101e-160">A Feature contains a Feature.xml file and one or more element manifest files.</span></span> <span data-ttu-id="5101e-161">Эти XML-файлы также называют определениями компонентов.</span><span class="sxs-lookup"><span data-stu-id="5101e-161">These XML files are also known as Feature definitions.</span></span> 

<span data-ttu-id="5101e-162">Как правило, пакет клиентского решения содержит один компонент.</span><span class="sxs-lookup"><span data-stu-id="5101e-162">Typically, a client-side solution package contains one feature.</span></span> <span data-ttu-id="5101e-163">Этот компонент активируется при установке решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="5101e-163">This feature is activated when the solution is installed on a site.</span></span> <span data-ttu-id="5101e-164">Важно отметить, что администраторы сайтов устанавливают пакет решения, а не компонент.</span><span class="sxs-lookup"><span data-stu-id="5101e-164">Typically, a client-side solution package contains one feature. This feature is activated when the solution is installed in a site. It is important to note that the site administrators install your solution package and not the feature.</span></span> 

<span data-ttu-id="5101e-165">Как правило, при создании компонентов используются указанные ниже XML-файлы.</span><span class="sxs-lookup"><span data-stu-id="5101e-165">A feature is primarily constructed by using the following XML files:</span></span>

### <a name="element-manifest-file"></a><span data-ttu-id="5101e-166">Файл манифеста элементов</span><span class="sxs-lookup"><span data-stu-id="5101e-166">Element Manifest File</span></span>

<span data-ttu-id="5101e-167">Файл манифеста элементов содержит определения элементов SharePoint и выполняется при активации компонента.</span><span class="sxs-lookup"><span data-stu-id="5101e-167">The element manifest file contains the SharePoint item definitions and is executed when the feature is activated.</span></span> <span data-ttu-id="5101e-168">Например, в манифесте элементов могут находиться XML-определения для создания поля, типа контента или экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="5101e-168">For example, the XML definitions to create a new field, content type, or list instance is in the element manifest.</span></span> 

<span data-ttu-id="5101e-169">Ниже приведен пример файла манифеста элемента, который определяет новое поле DateTime.</span><span class="sxs-lookup"><span data-stu-id="5101e-169">Below is an example of an element manifest file that defines a new DateTime field.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Field ID="{1511BF28-A787-4061-B2E1-71F64CC93FD5}"
            Name="DateOpened"
            DisplayName="Date Opened"
            Type="DateTime"
            Format="DateOnly"
            Required="FALSE"
            Group="Financial Columns">
        <Default>[today]</Default>
    </Field>
  </Elements>
```

### <a name="element-file"></a><span data-ttu-id="5101e-170">Файл элемента</span><span class="sxs-lookup"><span data-stu-id="5101e-170">Element File</span></span>

<span data-ttu-id="5101e-171">Файлы элементов — это все поддерживаемые файлы, сопровождающие манифест элемента.</span><span class="sxs-lookup"><span data-stu-id="5101e-171">Any supported files that accompany the element manifest are element files.</span></span> <span data-ttu-id="5101e-172">Например, схема экземпляра списка — это файл элемента, связанный с экземпляром списка, определенным в манифесте элемента.</span><span class="sxs-lookup"><span data-stu-id="5101e-172">Any supported files that accompany the element manifest will be an element file. For example, the list instance schema is an element manifest that is associated with a list instance that is defined in an element manifest.</span></span> 

<span data-ttu-id="5101e-173">Ниже приведен пример специальной схемы экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="5101e-173">Below is an example of a custom list instance schema:</span></span>

```xml
<List xmlns:ows="Microsoft SharePoint" Title="Basic List" EnableContentTypes="TRUE" FolderCreation="FALSE"
      Direction="$Resources:Direction;" Url="Lists/Basic List" BaseType="0" xmlns="http://schemas.microsoft.com/sharepoint/">
  <MetaData>
    <ContentTypes>
      <ContentTypeRef ID="0x010042D0C1C200A14B6887742B6344675C8B" />
    </ContentTypes>    
  </MetaData>
</List>
```

### <a name="upgrade-actions-file"></a><span data-ttu-id="5101e-174">Файл с действиями по обновлению</span><span class="sxs-lookup"><span data-stu-id="5101e-174">Upgrade Actions File</span></span>

<span data-ttu-id="5101e-175">Как понятно из названия, этот файл указывает действия, выполняемые при обновлении решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="5101e-175">As its name suggests, this is the file that includes any upgrade actions when the solution is updated on the site.</span></span> <span data-ttu-id="5101e-176">Такое действие может сопровождаться одним или несколькими манифестами элементов.</span><span class="sxs-lookup"><span data-stu-id="5101e-176">As part of the upgrade actions, the action could specify to include one or more element manifests as well.</span></span> <span data-ttu-id="5101e-177">Например, если обновление предусматривает добавление нового поля, то определение этого поля доступно в виде манифеста элемента и сопоставлено в файле с действиями по обновлению.</span><span class="sxs-lookup"><span data-stu-id="5101e-177">For example, if the upgrade requires a new field to be added, the field definition is available as an element manifest and is associated in the upgrade actions file.</span></span> 

<span data-ttu-id="5101e-178">Ниже приведен пример файла с действиями по обновлению, который применяет файл манифеста элемента во время обновления.</span><span class="sxs-lookup"><span data-stu-id="5101e-178">Below is an example of an upgrade action file that applies an element manifest file during the upgrade:</span></span>

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

## <a name="configure-the-sharepoint-feature"></a><span data-ttu-id="5101e-179">Настройка компонента SharePoint</span><span class="sxs-lookup"><span data-stu-id="5101e-179">Configure the SharePoint feature</span></span> 

<span data-ttu-id="5101e-180">Чтобы включить XML-файлы, необходимо сначала определить конфигурацию компонента в файле конфигурации *package-solution.json*, находящемся в папке *config* проекта.</span><span class="sxs-lookup"><span data-stu-id="5101e-180">In order to include the XML files, you will need to first define the feature configuration in the *package-solution.json* configuration file underneath the *config* folder in your project.</span></span> <span data-ttu-id="5101e-181">Файл *package-solution.json* содержит ключевые метаданные для пакета клиентского решения, и на него можно ссылаться при выполнении задачи gulp `package-solution`, которая упаковывает решение в файл `.sppkg`.</span><span class="sxs-lookup"><span data-stu-id="5101e-181">The *package-solution.json* contains the key metadata information about your client-side solution package and is referenced when you run the `package-solution` gulp task which packages your solution into a `.sppkg` file.</span></span> 

```json
{
  "solution": {
    "name": "hello-world-client-side-solution",
    "id": "26364618-3056-4b45-98c1-39450adc5723",
    "version": "1.1.0.0",
    "features": [{
      "title": "hello-world-client-side-solution",
      "description": "hello-world-client-side-solution",
      "id": "d46cd9d6-87fc-473b-a4c0-db9ad9162b64",
      "version": "1.1.0.0",
      "assets": {        
        "elementManifests": [
          "elements.xml"
        ],
        "elementFiles":[
          "schema.xml"
        ],
        "upgradeActions":[
            "upgrade-actions-v1.xml"
        ]
      }
    }]
  },  
  "paths": {
    "zippedPackage": "solution/hello-world.sppkg"
  }
}
``` 

<br/>

<span data-ttu-id="5101e-182">Объект JSON `features` содержит метаданные для компонента, как показано в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="5101e-182">The `features` JSON object contains the metadata about the feature, as shown in the following table.</span></span>

<span data-ttu-id="5101e-183">Свойство</span><span class="sxs-lookup"><span data-stu-id="5101e-183">Property</span></span> | <span data-ttu-id="5101e-184">Описание</span><span class="sxs-lookup"><span data-stu-id="5101e-184">Description</span></span> 
-----|------
<span data-ttu-id="5101e-185">id</span><span class="sxs-lookup"><span data-stu-id="5101e-185">id</span></span>|<span data-ttu-id="5101e-186">Уникальный идентификатор (GUID) компонента</span><span class="sxs-lookup"><span data-stu-id="5101e-186">Unique identifier (GUID) of the feature</span></span>
<span data-ttu-id="5101e-187">title</span><span class="sxs-lookup"><span data-stu-id="5101e-187">title</span></span>|<span data-ttu-id="5101e-188">Название компонента</span><span class="sxs-lookup"><span data-stu-id="5101e-188">Title of the feature</span></span>
<span data-ttu-id="5101e-189">description</span><span class="sxs-lookup"><span data-stu-id="5101e-189">description</span></span>| <span data-ttu-id="5101e-190">Описание компонента</span><span class="sxs-lookup"><span data-stu-id="5101e-190">Description of the feature</span></span>
<span data-ttu-id="5101e-191">assets</span><span class="sxs-lookup"><span data-stu-id="5101e-191">assets</span></span>|<span data-ttu-id="5101e-192">Массив XML-файлов, используемых в компоненте</span><span class="sxs-lookup"><span data-stu-id="5101e-192">An array of XML files used in the feature</span></span>
<span data-ttu-id="5101e-193">elementManifests</span><span class="sxs-lookup"><span data-stu-id="5101e-193">elementManifests</span></span>|<span data-ttu-id="5101e-194">Определяется в свойстве `assets`, массив файлов манифеста элемента</span><span class="sxs-lookup"><span data-stu-id="5101e-194">Defined within the `assets` property, an array of element manifest files</span></span>
<span data-ttu-id="5101e-195">elementFiles</span><span class="sxs-lookup"><span data-stu-id="5101e-195">elementFiles</span></span>|<span data-ttu-id="5101e-196">Определяется в свойстве `assets`, массив файлов элемента</span><span class="sxs-lookup"><span data-stu-id="5101e-196">Defined within the `assets` property, an array of element files</span></span>
<span data-ttu-id="5101e-197">upgradeActions</span><span class="sxs-lookup"><span data-stu-id="5101e-197">upgradeActions</span></span>|<span data-ttu-id="5101e-198">Определяется в свойстве `assets`, массив файлов с действиями по обновлению</span><span class="sxs-lookup"><span data-stu-id="5101e-198">Defined within the `assets` property, an array of upgrade action files</span></span>

### <a name="create-the-feature-xml-files"></a><span data-ttu-id="5101e-199">Создание XML-файлов компонента</span><span class="sxs-lookup"><span data-stu-id="5101e-199">Create the feature XML files</span></span>

<span data-ttu-id="5101e-200">Цепочка инструментов ищет XML-файлы, определенные в конфигурации в специальной папке проекта клиентского решения — *sharepoint\assets*.</span><span class="sxs-lookup"><span data-stu-id="5101e-200">The toolchain looks for the XML files as defined in the configuration underneath a special folder - *sharepoint\assets* - in your client-side solution project.</span></span> 

![XML-файлы компонента в проекте клиентского решения](../../images/feature-provision-project-items.png)

<span data-ttu-id="5101e-202">Конфигурация, определенная в файле `package-solution.json`, сопоставляет XML-файлы с соответствующим XML-файлом компонента при выполнении задачи gulp `package-solution`.</span><span class="sxs-lookup"><span data-stu-id="5101e-202">The configurations defined in the `package-solution.json` is what maps the XML files here to its appropriate feature XML file when the `package-solution` gulp task is executed.</span></span>

## <a name="package-sharepoint-items"></a><span data-ttu-id="5101e-203">Упаковка элементов SharePoint</span><span class="sxs-lookup"><span data-stu-id="5101e-203">Package SharePoint items</span></span> 

<span data-ttu-id="5101e-204">Определив компонент в файле `package-solution.json` и создав соответствующие XML-файлы компонента, вы можете упаковать элементы SharePoint вместе с пакетом `.sppkg` при помощи приведенной ниже команды gulp.</span><span class="sxs-lookup"><span data-stu-id="5101e-204">Once you have defined your feature in the `package-solution.json` and created the respective feature XML files, you can use the following gulp task to package the SharePoint items along with your `.sppkg` package.</span></span>

```js
gulp package-solution
```

<span data-ttu-id="5101e-205">Эта команда упаковывает один или несколько манифестов клиентских компонентов, таких как веб-части, вместе с XML-файлами, на которые ссылается файл конфигурации `package-solution.json`.</span><span class="sxs-lookup"><span data-stu-id="5101e-205">The command above will package one or more client-side component manifests, such as web parts, along with the feature XML files referenced in the `package-solution.json` configuration file.</span></span>

> [!NOTE] 
> <span data-ttu-id="5101e-206">Вы можете упаковывать сжатые версии компонентов, используя флаг `--ship`.</span><span class="sxs-lookup"><span data-stu-id="5101e-206">You can use the `--ship` flag to package minified versions of your components.</span></span> 

## <a name="upgrade-sharepoint-items"></a><span data-ttu-id="5101e-207">Обновление элементов SharePoint</span><span class="sxs-lookup"><span data-stu-id="5101e-207">Upgrade SharePoint items</span></span>

<span data-ttu-id="5101e-208">Обновляя клиентское решение, можно добавлять новые элементы SharePoint или обновлять уже имеющиеся.</span><span class="sxs-lookup"><span data-stu-id="5101e-208">You may include new SharePoint items or update existing SharePoint items when you upgrade your client-side solution.</span></span> <span data-ttu-id="5101e-209">Для подготовки элементов SharePoint используются компоненты, поэтому определите список действий по обновлению с помощью XML-файла [UpgradeActions](https://msdn.microsoft.com/en-us/library/office/ee537575(v=office.14).aspx).</span><span class="sxs-lookup"><span data-stu-id="5101e-209">Since provisioning SharePoint items uses features, you will be using the [feature upgrade actions](https://msdn.microsoft.com/en-us/library/office/ee537575(v=office.14).aspx) XML file to define a list of upgrade actions.</span></span>

<span data-ttu-id="5101e-210">Массив объектов JSON `upgradeActions` в файле `package-solution.json` ссылается на XML-файлы, связанные с действиями по обновлению для компонента.</span><span class="sxs-lookup"><span data-stu-id="5101e-210">The `upgradeActions` JSON object array in the `package-solution.json` references the feature XML file(s) associated with the upgrade actions for your feature.</span></span> <span data-ttu-id="5101e-211">В файле с действиями по обновлению определяется по крайней мере XML-файл манифеста элемента, выполняющийся при обновлении компонента.</span><span class="sxs-lookup"><span data-stu-id="5101e-211">At the least, an upgrade action file will define the element manifest XML file that will be executed when upgrading the feature.</span></span> 

<span data-ttu-id="5101e-212">При обновлении решения SharePoint Framework необходимо также обновить атрибуты версии как для решения, так и для компонента, в который были включены действия по обновлению.</span><span class="sxs-lookup"><span data-stu-id="5101e-212">When you are upgrading a SharePoint Framework solution, you must also update version attributes for both the solution and the feature where the upgrade actions have been included.</span></span> <span data-ttu-id="5101e-213">По увеличению версии решения пользователи SharePoint поймут, что доступна новая версия пакета.</span><span class="sxs-lookup"><span data-stu-id="5101e-213">A solution version increase indicates to SharePoint end users that there is a new version of the package available.</span></span> <span data-ttu-id="5101e-214">Увеличение версии компонента обеспечивает обработку задач, указанных в действиях по обновлению, при обновлении решения.</span><span class="sxs-lookup"><span data-stu-id="5101e-214">A feature element version increase ensures that the tasks defined in the upgrade actions are being processed as part of the solution upgrade.</span></span> 

<span data-ttu-id="5101e-215">Ниже приведен пример файла с действиями по обновлению, который применяет файл манифеста элемента во время обновления.</span><span class="sxs-lookup"><span data-stu-id="5101e-215">Below is an example of an upgrade action file that applies an element manifest file during the upgrade:</span></span>

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

<br/>

<span data-ttu-id="5101e-216">Это соответствующий файл `element-v2.xml`, который определяет новое денежное поле, подготавливаемое при обновлении:</span><span class="sxs-lookup"><span data-stu-id="5101e-216">And the corresponding `element-v2.xml` which defines a new Currency Field to be provisioned during the upgrade:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <Field ID="{060E50AC-E9C1-4D3C-B1F9-DE0BCAC300F6}"
            Name="Amount"
            DisplayName="Amount"
            Type="Currency"
            Decimals="2"
            Min="0"
            Required="FALSE"
            Group="Financial Columns" />
</Elements>
```

<br/>

### <a name="sub-elements"></a><span data-ttu-id="5101e-217">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="5101e-217">Sub-elements</span></span>

<span data-ttu-id="5101e-218">Действия по обновлению в клиентских решениях поддерживают следующие дочерние элементы:</span><span class="sxs-lookup"><span data-stu-id="5101e-218">Upgrade actions in client-side solutions support the following sub elements:</span></span>

#### <a name="addcontenttypefield"></a><span data-ttu-id="5101e-219">AddContentTypeField</span><span class="sxs-lookup"><span data-stu-id="5101e-219">AddContentTypeField</span></span>

<span data-ttu-id="5101e-p121">Добавляет новое поле к имеющемуся подготовленному типу контента. Распространяет изменения, внесенные в тип контента сайта, для всех дочерних списков и типов контента на этом сайте. Например:</span><span class="sxs-lookup"><span data-stu-id="5101e-p121">Adds a new field to an existing provisioned content type. Propagates the change from the site content type to all child lists and content types within the site. For example:</span></span>

```xml
<AddContentTypeField 
     ContentTypeId="0x010100A6F9CE1AFE2A48f0A3E6CB5BB770B0F7" 
     FieldId="{B250DCFD-9310-4e2d-85F2-BE2DA37A57D2}" 
     PushDown="TRUE" />
```

#### <a name="applyelementmanifests"></a><span data-ttu-id="5101e-223">ApplyElementManifests</span><span class="sxs-lookup"><span data-stu-id="5101e-223">ApplyElementManifests</span></span>

<span data-ttu-id="5101e-224">Добавляет новый элемент к уже имеющемуся компоненту.</span><span class="sxs-lookup"><span data-stu-id="5101e-224">Add a new element to an existing feature</span></span> <span data-ttu-id="5101e-225">При обновлении компонента подготавливаются все недекларативные элементы, на которые ссылаются указанные манифесты элементов.</span><span class="sxs-lookup"><span data-stu-id="5101e-225">Adds a new element to an existing Feature. When a Feature is upgraded, provisions all non-declarative elements that are referenced in the specified element manifests.</span></span>

#### <a name="versionrange"></a><span data-ttu-id="5101e-226">VersionRange</span><span class="sxs-lookup"><span data-stu-id="5101e-226">VersionRange</span></span>

<span data-ttu-id="5101e-227">Задает диапазон версий, к которым применяются указанные действия по обновлению.</span><span class="sxs-lookup"><span data-stu-id="5101e-227">Specifies a version range to which specified upgrade actions apply.</span></span>


## <a name="see-also"></a><span data-ttu-id="5101e-228">См. также</span><span class="sxs-lookup"><span data-stu-id="5101e-228">See also</span></span>
 
- [<span data-ttu-id="5101e-229">Руководство: подготовка ресурсов SharePoint из клиентской веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="5101e-229">Tutorial - Provisioning SharePoint assets from your SharePoint client-side web part</span></span>](../web-parts/get-started/provision-sp-assets-from-package.md)
- [<span data-ttu-id="5101e-230">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="5101e-230">SharePoint Framework Overview</span></span>](../sharepoint-framework-overview.md)