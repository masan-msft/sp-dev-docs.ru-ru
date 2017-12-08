---
title: "Подготовка ресурсов SharePoint с пакетом решения"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9da564c257f513b40fc036b9656d11972d5dc530
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="provision-sharepoint-assets-with-your-solution-package"></a><span data-ttu-id="6437f-102">Подготовка ресурсов SharePoint с пакетом решения</span><span class="sxs-lookup"><span data-stu-id="6437f-102">Provision SharePoint assets with your solution package</span></span>

<span data-ttu-id="6437f-p101">Иногда требуется подготовить к работе список или библиотеку документов SharePoint вместе с клиентским пакетом решения, чтобы сделать их доступными клиентским решениям, таким как веб-части. Цепочка инструментов SharePoint Framework позволяет упаковывать и развертывать элементы SharePoint с клиентским пакетом решения. Затем эти элементы подготавливаются к работе при установке клиентского решения на сайте.</span><span class="sxs-lookup"><span data-stu-id="6437f-p101">At times, you may need to provision a SharePoint list or a document library along with your client-side solution package so that that list or library is available for your client-side components, such as web parts. SharePoint Framework toolchain allows you to package and deploy SharePoint items with your client-side solution package. These items are then provisioned when the client-side solution is installed on a site.</span></span> 

<span data-ttu-id="6437f-106">Подробнее о возможностях подготовки ресурсов можно узнать из веб-трансляции на [YouTube-канале SharePoint PnP](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS).</span><span class="sxs-lookup"><span data-stu-id="6437f-106">You can also find details on the provisioning options from a SharePoint PnP webcast available from [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS).</span></span> 

<a href="https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS">
<img src="../../images/spfx-webcast-youtube-provision-feature-elements.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="provisioning-items-using-javascript-code"></a><span data-ttu-id="6437f-107">Подготовка элементов с помощью кода JavaScript</span><span class="sxs-lookup"><span data-stu-id="6437f-107">Provisioning items using JavaScript code</span></span>

<span data-ttu-id="6437f-p102">Хотя можно создавать элементы SharePoint в решении (например, веб-части) с помощью кода JavaScript, эта возможность ограничена контекстом текущего пользователя решения. Если у пользователя нет разрешений для создания или изменения элементов SharePoint, код JavaScript не подготовит эти элементы к работе. В таких случаях, если требуется подготовить элементы SharePoint в контексте c повышенными привилегиями, вам потребуется упаковать и развернуть элементы с пакетом решения.</span><span class="sxs-lookup"><span data-stu-id="6437f-p102">While it is possible to create SharePoint items using JavaScript code in your component, such as web parts, it is limited to context of the current user using that component. If the user doesn't have sufficient permissions to create or modify SharePoint items, the JavaScript code will not provision those items. In such cases, when you want to provision SharePoint items in an elevated context, you will need to package and deploy the items along with your solution package.</span></span>

## <a name="create-and-provision-sharepoint-items-in-your-solution"></a><span data-ttu-id="6437f-111">Создание и подготовка элементов SharePoint в решении</span><span class="sxs-lookup"><span data-stu-id="6437f-111">Create and provision SharePoint items in your solution</span></span>

### <a name="sharepoint-items"></a><span data-ttu-id="6437f-112">Элементы SharePoint</span><span class="sxs-lookup"><span data-stu-id="6437f-112">SharePoint items</span></span>

<span data-ttu-id="6437f-113">С клиентским пакетом решения можно подготовить к работе такие ресурсы SharePoint:</span><span class="sxs-lookup"><span data-stu-id="6437f-113">The following SharePoint assets can be provisioned along with your client-side solution package:</span></span>

* <span data-ttu-id="6437f-114">поля;</span><span class="sxs-lookup"><span data-stu-id="6437f-114">Fields</span></span>
* <span data-ttu-id="6437f-115">типы контента;</span><span class="sxs-lookup"><span data-stu-id="6437f-115">Content Types</span></span>
* <span data-ttu-id="6437f-116">экземпляры списков;</span><span class="sxs-lookup"><span data-stu-id="6437f-116">List Instances</span></span>
* <span data-ttu-id="6437f-117">экземпляры списков с настраиваемой схемой.</span><span class="sxs-lookup"><span data-stu-id="6437f-117">List Instances with custom schema</span></span>

#### <a name="fields"></a><span data-ttu-id="6437f-118">Поля</span><span class="sxs-lookup"><span data-stu-id="6437f-118">Fields</span></span>

<span data-ttu-id="6437f-p103">Поле (столбец сайта) представляет атрибут, или фрагмент метаданных, который пользователь применяет в управлении списком или типом контента, к которому добавил этот столбец. Это определение столбца, или шаблон, которое вы можете назначить нескольким спискам для нескольких сайтов SharePoint. Столбцы сайтов избавляют от лишней работы и помогают обеспечить согласованность метаданных на сайтах и в списках.</span><span class="sxs-lookup"><span data-stu-id="6437f-p103">A field or a site column represents an attribute, or piece of metadata, that the user wants to manage for the items in the list or content type to which they added the column. It is a reusable column definition, or template, that you can assign to multiple lists across multiple SharePoint sites. Site columns decrease rework and help you ensure consistency of metadata across sites and lists.</span></span> 

<span data-ttu-id="6437f-p104">Допустим, вы определили столбец сайта под названием "Клиент". Пользователи могут добавлять этот столбец к своим спискам и ссылаться на него в своих типах контента. Это гарантирует, что у столбца всегда будут одни и те же атрибуты (хотя бы вначале), где бы он ни находился.</span><span class="sxs-lookup"><span data-stu-id="6437f-p104">For example, suppose you define a site column named Customer. Users can add that column to their lists, and reference it in their content types. This ensures that the column has the same attributes—at least to start with—wherever it appears.</span></span>

<span data-ttu-id="6437f-125">Определяя новое поле в своем решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент поля (Field)](https://msdn.microsoft.com/en-us/library/aa979575(v=office.15).aspx).</span><span class="sxs-lookup"><span data-stu-id="6437f-125">You can refer to the schema and attributes in the [Field Element](https://msdn.microsoft.com/en-us/library/aa979575(v=office.15).aspx) documentation to define a new field in your solution.</span></span> 

<span data-ttu-id="6437f-126">Ниже приведен пример нового поля DateTime.</span><span class="sxs-lookup"><span data-stu-id="6437f-126">Below is an example of a new DateTime field:</span></span>

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
#### <a name="content-types"></a><span data-ttu-id="6437f-127">Типы контента</span><span class="sxs-lookup"><span data-stu-id="6437f-127">Content Types</span></span>

<span data-ttu-id="6437f-p105">Тип контента — это многоразовая коллекция метаданных (столбцов), настроек поведения и других настроек для категории элементов в списке SharePoint или документов в библиотеке документов SharePoint. Типы контента позволяют централизованно управлять настройками для категории сведений.</span><span class="sxs-lookup"><span data-stu-id="6437f-p105">A content type is a reusable collection of metadata (columns), behavior, and other settings for a category of items or documents in a SharePoint list or document library. Content types enable you to manage the settings for a category of information in a centralized, reusable way.</span></span>

<span data-ttu-id="6437f-p106">Например, представьте себе бизнес-ситуацию, в которой есть три типа документов: отчеты о расхода, заказы на покупку и счета. У всех трех типов документов есть ряд общих характеристик, с одной стороны, все они являются финансовыми документами и содержат данные с денежными суммами. Но у каждого типа документов есть свои требования к данным, свой шаблон документов и свой рабочий процесс. Одним из решений этой бизнес-проблемы является создание четырех типов контента. Первый тип контента, "Финансовый документ", может инкапсулировать требования к данным, общие для всех финансовых документов в организации. Оставшиеся три, "Отчет о расходах", "Заказ на покупку" и "Счет", могут наследовать общие элементы от типа "Финансовый документ", а также определять характеристики, уникальные для каждого типа, такие как конкретный набор метаданных, шаблон документа, используемый при создании нового элемента, и конкретный рабочий процесс для обработки элемента.</span><span class="sxs-lookup"><span data-stu-id="6437f-p106">For example, imagine a business situation in which you have three different types of documents: expense reports, purchase orders, and invoices. All three types of documents have some characteristics in common; for one thing, they are all financial documents and contain data with values in currency. Yet each type of document has its own data requirements, its own document template, and its own workflow. One solution to this business problem is to create four content types. The first content type, Financial Document, could encapsulate data requirements that are common to all financial documents in the organization. The remaining three, Expense Report, Purchase Order, and Invoice, could inherit common elements from Financial Document. In addition, they could define characteristics that are unique to each type, such as a particular set of metadata, a document template to be used in creating a new item, and a specific workflow for processing an item.</span></span>

<span data-ttu-id="6437f-137">Определяя новый тип контента в решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент типа контента (ContentType)](https://msdn.microsoft.com/ru-RU/library/aa544268.aspx).</span><span class="sxs-lookup"><span data-stu-id="6437f-137">You can refer to the schema and attributes in the [Content Type Element](https://msdn.microsoft.com/ru-RU/library/aa544268.aspx) documentation to define a new content type in your solution.</span></span> 

<span data-ttu-id="6437f-138">Ниже приведен пример типа контента.</span><span class="sxs-lookup"><span data-stu-id="6437f-138">Below is an example of a content type:</span></span>

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

#### <a name="lists-instances"></a><span data-ttu-id="6437f-139">Экземпляры списков</span><span class="sxs-lookup"><span data-stu-id="6437f-139">Lists Instances</span></span>

<span data-ttu-id="6437f-p107">Списки — это ключевая, базовая функция сайта SharePoint. Они помогают группам собирать и отслеживать информацию, а также делиться ею. Многие приложения используют списки, созданные на сайте, чтобы хранить данные для реализации своего поведения. Экземпляр списка — это предопределенный список SharePoint с известным идентификатором. Вы можете настраивать и добавлять элементы в этих списках, создавать дополнительные списки с помощью доступных шаблонов, а также создавать специальные списки, указывая только нужные параметры и столбцы.</span><span class="sxs-lookup"><span data-stu-id="6437f-p107">Lists are a key, underlying feature of a SharePoint site. They enable teams to gather, track, and share information. Many applications rely on lists created at the site for data storage to implement their behaviors. A list instance is a predefined SharePoint list that has a well-known identifier. You can customize and add items to these lists, create additional lists from the list templates that are already available, and create custom lists with just the settings and columns that you choose.</span></span>

<span data-ttu-id="6437f-p108">В SharePoint доступны несколько шаблонов списков (например, для календаря, списка контактов или задач). С помощью этих шаблонов вы можете создавать экземпляры списков для своих веб-частей и других решений. Например, вы можете определить экземпляр списка "Финансовые документы" на основе шаблона "Библиотека документов", чтобы обеспечить хранение соответствующих документов для веб-части.</span><span class="sxs-lookup"><span data-stu-id="6437f-p108">SharePoint provides several list templates such as contact list, calendar, task list and more. You can use these templates to create new list instances for your web parts or other components. For example, you can define a list instance Finance Documents based on the Document Library template to store associated documents with your web part.</span></span> 

<span data-ttu-id="6437f-148">Определяя новый экземпляр списка в решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент экземпляра списка (ListInstance)](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx).</span><span class="sxs-lookup"><span data-stu-id="6437f-148">You can refer to the schema and attributes in the [List Instance Element](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx) documentation to define a list instance in your solution.</span></span>

<span data-ttu-id="6437f-149">Ниже приведен пример определения экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="6437f-149">Below is an example of a list instance definition:</span></span>

```xml
<ListInstance 
    FeatureId="00bfea71-e717-4e80-aa17-d0c71b360101"
    Title="Finance Records" 
    Description="Finance documents"
    TemplateType="101"
    Url="Lists/FinanceRecords">
</ListInstance>
```

#### <a name="lists-instances-with-custom-schema"></a><span data-ttu-id="6437f-150">Экземпляры списков с настраиваемой схемой</span><span class="sxs-lookup"><span data-stu-id="6437f-150">Lists Instances with custom schema</span></span>

<span data-ttu-id="6437f-151">Вы можете определять поля, типы контента и представления, используемые в экземпляре списка, применяя определение настраиваемой схемы списков.</span><span class="sxs-lookup"><span data-stu-id="6437f-151">You can use a custom list schema definition to define your fields, content types and views used in your list instance. You will use the  attribute in the list instance element to reference a custom schema for the list instance.</span></span> <span data-ttu-id="6437f-152">Используйте атрибут `customschema` [элемента экземпляра списка](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx#sectionSection0), чтобы ссылаться на настраиваемую схему экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="6437f-152">You can use a custom list schema definition to define your fields, content types and views used in your list instance. You will use the `customschema` attribute in the [list instance element](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx#sectionSection0) to reference a custom schema for the list instance.</span></span> 

<span data-ttu-id="6437f-153">Например, вы можете определить экземпляр списка "Финансовые документы" с типом контента "Финансовый документ", который может инкапсулировать требования к данным, общие для всех финансовых документов в организации.</span><span class="sxs-lookup"><span data-stu-id="6437f-153">For example, you can define a list instance Finance Documents with a content type Financial Document that could encapsulate data requirements that are common to all financial documents in the organization.</span></span> 

<span data-ttu-id="6437f-154">Ниже приведен пример определения экземпляра списка, для которого используется настраиваемая схема.</span><span class="sxs-lookup"><span data-stu-id="6437f-154">Below is an example of a list instance definition that uses a custom schema:</span></span>

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
<span data-ttu-id="6437f-155">А так выглядит определение настраиваемой схемы, которое задает тип контента для определенного выше экземпляра списка:</span><span class="sxs-lookup"><span data-stu-id="6437f-155">And the custom schema definition that defines a content type for the list instance defined above:</span></span>

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
### <a name="create-sharepoint-items-in-your-solution"></a><span data-ttu-id="6437f-156">Создание элементов SharePoint в решении</span><span class="sxs-lookup"><span data-stu-id="6437f-156">Create SharePoint items in your solution</span></span>

<span data-ttu-id="6437f-157">Пакет решения использует [компоненты SharePoint](https://msdn.microsoft.com/en-us/library/ee537350(office.14).aspx) для упаковки элементов SharePoint и подготовки последних к работе.</span><span class="sxs-lookup"><span data-stu-id="6437f-157">The solution package uses [SharePoint Features](https://msdn.microsoft.com/en-us/library/ee537350(office.14).aspx) to package and provision the SharePoint items.</span></span> <span data-ttu-id="6437f-158">Компонент — это контейнер, включающий один или несколько подготавливаемых элементов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6437f-158">A Feature is a container that includes one or more SharePoint items to provision.</span></span> <span data-ttu-id="6437f-159">Компонент содержит файл Feature.xml и один или несколько файлов манифеста элементов.</span><span class="sxs-lookup"><span data-stu-id="6437f-159">A Feature contains a Feature.xml file and one or more element manifest files.</span></span> <span data-ttu-id="6437f-160">Эти XML-файлы также называют определениями компонентов.</span><span class="sxs-lookup"><span data-stu-id="6437f-160">These XML files are also known as Feature definitions.</span></span> 

<span data-ttu-id="6437f-p111">Как правило, клиентский пакет решения содержит один компонент. Этот компонент активируется при установке решения на сайте. Важно отметить, что администраторы сайтов устанавливают пакет решения, а не компонент.</span><span class="sxs-lookup"><span data-stu-id="6437f-p111">Typically, a client-side solution package contains one feature. This feature is activated when the solution is installed in a site. It is important to note that the site administrators install your solution package and not the feature.</span></span> 

<span data-ttu-id="6437f-164">Компонент, как правило, создается с помощью указанных ниже XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="6437f-164">A feature is primarily constructed by using the following XML files:</span></span>

<span data-ttu-id="6437f-165">**Файл манифеста элемента**</span><span class="sxs-lookup"><span data-stu-id="6437f-165">**Element Manifest File**</span></span>

<span data-ttu-id="6437f-p112">Файл манифеста элемента содержит определения элементов SharePoint и выполняется при активации компонента. Например: XML-определения для создания экземпляров списка, поля или типа контента находятся в манифесте элемента.</span><span class="sxs-lookup"><span data-stu-id="6437f-p112">The element manifest file contains the SharePoint item definitions and will be executed when the feature is activated. For example: The XML definitions to create a new field or content type or list instance(s) will be in the element manifest.</span></span> 

<span data-ttu-id="6437f-168">Ниже приведен пример файла манифеста элемента, в котором определяется новое поле DateTime.</span><span class="sxs-lookup"><span data-stu-id="6437f-168">Below is an example of an element manifest file that defines a new DateTime field.</span></span>

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

<span data-ttu-id="6437f-169">**Файл элемента**</span><span class="sxs-lookup"><span data-stu-id="6437f-169">**Element File**</span></span>

<span data-ttu-id="6437f-p113">Любой поддерживаемый файл, сопровождающий манифест элемента, — это файл элемента. Например, схема экземпляра списка — это манифест элемента, связанный с экземпляром списка, определенным в манифесте элемента.</span><span class="sxs-lookup"><span data-stu-id="6437f-p113">Any supported files that accompany the element manifest will be an element file. For example, the list instance schema is an element manifest that is associated with a list instance that is defined in an element manifest.</span></span> 

<span data-ttu-id="6437f-172">Ниже приведен пример настраиваемой схемы экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="6437f-172">Below is an example of a custom list instance schema:</span></span>

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

<span data-ttu-id="6437f-173">**Файл с действиями по обновлению**</span><span class="sxs-lookup"><span data-stu-id="6437f-173">**Upgrade Actions File**</span></span>

<span data-ttu-id="6437f-p114">Как понятно из названия, этот файл указывает действия, выполняемые при обновлении решения на сайте. Такое действие может предусматривать включение одного или нескольких манифестов элемента. Например: Если для обновления требуется добавить новое поле, то определение этого поля будет доступно в виде манифеста элемента и добавлено в файл с действиями по обновлению.</span><span class="sxs-lookup"><span data-stu-id="6437f-p114">As it name suggests, this is the file that will include any upgrade actions when the solution is updated in the site. As part of the upgrade actions, the action could specify to include one or more element manifests as well. For example: If the upgrade requires a new field to be added, then the field definition will be available as an element manifest and associated in the upgrade actions file.</span></span> 

<span data-ttu-id="6437f-177">Ниже приведен пример файла с действиями по обновлению, который применяет файл манифеста элемента во время обновления.</span><span class="sxs-lookup"><span data-stu-id="6437f-177">Below is an example of an upgrade action file that applies an element manifest file during the upgrade:</span></span>

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

#### <a name="configure-the-sharepoint-feature"></a><span data-ttu-id="6437f-178">Настройка компонента SharePoint</span><span class="sxs-lookup"><span data-stu-id="6437f-178">Configure the SharePoint feature</span></span> 

<span data-ttu-id="6437f-179">Чтобы включить XML-файлы, необходимо сначала определить конфигурацию компонента в файле конфигурации *package-solution.json*, находящемся в папке *config* проекта.</span><span class="sxs-lookup"><span data-stu-id="6437f-179">In order to include the XML files, you will need to first define the feature configuration in the *package-solution.json* configuration file underneath the *config* folder in your project. The package-solution.json contains the key metadata information about your client-side solution package and is referenced when you run the  gulp task which packages your solution into a  file.</span></span> <span data-ttu-id="6437f-180">Файл *package-solution.json* содержит ключевые метаданные для клиентского пакета решения, и на него можно ссылаться при выполнении задачи gulp `package-solution`, которая упаковывает решение в файл `.sppkg`.</span><span class="sxs-lookup"><span data-stu-id="6437f-180">In order to include the XML files, you will need to first define the feature configuration in the package-solution.json configuration file underneath the config folder in your project. The *package-solution.json* contains the key metadata information about your client-side solution package and is referenced when you run the `package-solution` gulp task which packages your solution into a `.sppkg` file.</span></span> 

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
<span data-ttu-id="6437f-181">Объект JSON `features` содержит метаданные для компонента.</span><span class="sxs-lookup"><span data-stu-id="6437f-181">The `features` JSON object contains the metadata about the feature:</span></span>

<span data-ttu-id="6437f-182">Свойство</span><span class="sxs-lookup"><span data-stu-id="6437f-182">Property</span></span> | <span data-ttu-id="6437f-183">Описание</span><span class="sxs-lookup"><span data-stu-id="6437f-183">Description</span></span> 
-----|------
<span data-ttu-id="6437f-184">id</span><span class="sxs-lookup"><span data-stu-id="6437f-184">id</span></span>|<span data-ttu-id="6437f-185">Уникальный идентификатор (GUID) компонента</span><span class="sxs-lookup"><span data-stu-id="6437f-185">Unique identifier (GUID) of the feature</span></span>
<span data-ttu-id="6437f-186">title</span><span class="sxs-lookup"><span data-stu-id="6437f-186">title</span></span>|<span data-ttu-id="6437f-187">Название компонента</span><span class="sxs-lookup"><span data-stu-id="6437f-187">Title of the feature</span></span>
<span data-ttu-id="6437f-188">description</span><span class="sxs-lookup"><span data-stu-id="6437f-188">description</span></span>| <span data-ttu-id="6437f-189">Описание компонента</span><span class="sxs-lookup"><span data-stu-id="6437f-189">Description of the feature</span></span>
<span data-ttu-id="6437f-190">assets</span><span class="sxs-lookup"><span data-stu-id="6437f-190">assets</span></span>|<span data-ttu-id="6437f-191">Массив XML-файлов, используемых в компоненте</span><span class="sxs-lookup"><span data-stu-id="6437f-191">An array of XML files used in the feature</span></span>
<span data-ttu-id="6437f-192">elementManifests</span><span class="sxs-lookup"><span data-stu-id="6437f-192">elementManifests</span></span>|<span data-ttu-id="6437f-193">Определяется в свойстве `assets`, массив файлов манифеста элемента</span><span class="sxs-lookup"><span data-stu-id="6437f-193">Defined within the `assets` property, an array of element manifest files</span></span>
<span data-ttu-id="6437f-194">elementFiles</span><span class="sxs-lookup"><span data-stu-id="6437f-194">elementFiles</span></span>|<span data-ttu-id="6437f-195">Определяется в свойстве `assets`, массив файлов элемента</span><span class="sxs-lookup"><span data-stu-id="6437f-195">Defined within the `assets` property, an array of element files</span></span>
<span data-ttu-id="6437f-196">upgradeActions</span><span class="sxs-lookup"><span data-stu-id="6437f-196">upgradeActions</span></span>|<span data-ttu-id="6437f-197">Определяется в свойстве `assets`, массив файлов с действиями по обновлению</span><span class="sxs-lookup"><span data-stu-id="6437f-197">Defined within the `assets` property, an array of upgrade action files</span></span>

#### <a name="create-the-feature-xml-files"></a><span data-ttu-id="6437f-198">Создание XML-файлов компонента</span><span class="sxs-lookup"><span data-stu-id="6437f-198">Create the feature XML files</span></span>

<span data-ttu-id="6437f-199">Цепочка инструментов ищет XML-файлы, как определено в конфигурации в специальной папке проекта клиентского решения — *sharepoint\assets*.</span><span class="sxs-lookup"><span data-stu-id="6437f-199">The toolchain looks for the XML files as defined in the configuration underneath a special folder - *sharepoint\assets* - in your client-side solution project.</span></span> 

![XML-файлы компонента в проекте клиентского решения](../../images/feature-provision-project-items.png)

<span data-ttu-id="6437f-201">Конфигурация, определенная в файле `package-solution.json`, сопоставляет XML-файлы с соответствующим XML-файлом компонента при выполнении задачи gulp `package-solution`.</span><span class="sxs-lookup"><span data-stu-id="6437f-201">The configurations defined in the `package-solution.json` is what maps the XML files here to its appropriate feature XML file when the `package-solution` gulp task is executed.</span></span>

#### <a name="package-sharepoint-items"></a><span data-ttu-id="6437f-202">Упаковка элементов SharePoint</span><span class="sxs-lookup"><span data-stu-id="6437f-202">Package SharePoint items</span></span> 

<span data-ttu-id="6437f-203">Определив компонент в файле `package-solution.json` и создав соответствующие XML-файлы компонента, вы можете упаковать элементы SharePoint вместе с пакетом `.sppkg` с помощью указанной ниже задачи gulp.</span><span class="sxs-lookup"><span data-stu-id="6437f-203">Once you have defined your feature in the `package-solution.json` and created the respective feature XML files, you can use the following gulp task to package the SharePoint items along with your `.sppkg` package.</span></span>

```js
gulp package-solution
```

<span data-ttu-id="6437f-204">Приведенная выше команда упакует один или несколько манифестов клиентских решений, таких как веб-части, вместе с XML-файлами компонента, на которые ссылается файл конфигурации `package-solution.json`.</span><span class="sxs-lookup"><span data-stu-id="6437f-204">The command above will package one or more client-side component manifests, such as web parts, along with the feature XML files referenced in the `package-solution.json` configuration file.</span></span>

><span data-ttu-id="6437f-205">**ПРИМЕЧАНИЕ.** Вы можете использовать флаг `--ship`, чтобы упаковать минимальные версии решений.</span><span class="sxs-lookup"><span data-stu-id="6437f-205">**NOTE:** You can use the `--ship` flag to package minified versions of your components.</span></span> 

#### <a name="upgrade-sharepoint-items"></a><span data-ttu-id="6437f-206">Обновление элементов SharePoint</span><span class="sxs-lookup"><span data-stu-id="6437f-206">Upgrade SharePoint items</span></span>

<span data-ttu-id="6437f-207">Вы можете добавлять новые элементы SharePoint или обновлять имеющиеся при обновлении клиентского решения.</span><span class="sxs-lookup"><span data-stu-id="6437f-207">You may include new SharePoint items or update existing SharePoint items when you upgrade your client-side solution. Since provisioning SharePoint items uses features, you will be using the feature upgrade actions XML file to define a list of upgrade actions.</span></span> <span data-ttu-id="6437f-208">Для подготовки элементов SharePoint используются компоненты, поэтому определите список действий по обновлению с помощью XML-файла [действий по обновлению компонента](https://msdn.microsoft.com/en-us/library/office/ee537575(v=office.14).aspx).</span><span class="sxs-lookup"><span data-stu-id="6437f-208">You may include new SharePoint items or update existing SharePoint items when you upgrade your client-side solution. Since provisioning SharePoint items uses features, you will be using the [feature upgrade actions](https://msdn.microsoft.com/en-us/library/office/ee537575(v=office.14).aspx) XML file to define a list of upgrade actions.</span></span>

<span data-ttu-id="6437f-209">Массив объектов JSON `upgradeActions` в файле `package-solution.json` ссылается на XML-файлы компонента, связанные с действиями по обновлению для компонента.</span><span class="sxs-lookup"><span data-stu-id="6437f-209">The `upgradeActions` JSON object array in the `package-solution.json` references the feature XML file(s) associated with the upgrade actions for your feature. At the least, an upgrade action file will define the element manifest XML file that will be executed when upgrading the feature.</span></span> <span data-ttu-id="6437f-210">В файле с действиями по обновлению определяется по крайней мере XML-файл манифеста элемента, выполняющийся при обновлении компонента.</span><span class="sxs-lookup"><span data-stu-id="6437f-210">The  JSON object array in the  references the feature XML file(s) associated with the upgrade actions for your feature. At the least, an upgrade action file will define the element manifest XML file that will be executed when upgrading the feature.</span></span> 

<span data-ttu-id="6437f-p118">При обновлении решения SharePoint Framework необходимо также обновить атрибуты версии как для решения, так и для компонента, где были включены действия по обновлению. Увеличение версии решения будет обозначать для SharePoint и конечных пользователей, что доступна новая версия пакета. Увеличение версии компонента обеспечит обработку задач, указанных в действиях по обновлению, в рамках обновления решения.</span><span class="sxs-lookup"><span data-stu-id="6437f-p118">When you are upgrading a SharePoint Framework solution, you will need to update also version attributes for both solution and feature, where the upgrade actions have been included. Solution version increase will indicate SharePoint and end users that there is a new version of the package available. Feature element version increase will ensure that the tasks defined in the upgrade actions are being processed as part of the solution upgrade.</span></span> 

<span data-ttu-id="6437f-214">Ниже приведен пример файла с действиями по обновлению, который применяет файл манифеста элемента во время обновления.</span><span class="sxs-lookup"><span data-stu-id="6437f-214">Below is an example of an upgrade action file that applies an element manifest file during the upgrade:</span></span>

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

<span data-ttu-id="6437f-215">Соответствующий файл `element-v2.xml`, в котором определяется новое поле валюты, подготавливаемое при обновлении:</span><span class="sxs-lookup"><span data-stu-id="6437f-215">And the corresponding `element-v2.xml` which defines a new Currency Field to be provisioned during the upgrade:</span></span>

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

<span data-ttu-id="6437f-216">Действия по обновлению в клиентских решениях поддерживают следующие дочерние элементы:</span><span class="sxs-lookup"><span data-stu-id="6437f-216">Upgrade actions in client-side solutions support the following sub elements:</span></span>


<span data-ttu-id="6437f-217">**AddContentTypeField**</span><span class="sxs-lookup"><span data-stu-id="6437f-217">**AddContentTypeField**</span></span>

<span data-ttu-id="6437f-p119">Добавляет новое поле к имеющемуся подготовленному типу контента. Распространяет изменения, внесенные в тип контента сайта, для всех дочерних списков и типов контента на этом сайте. Например:</span><span class="sxs-lookup"><span data-stu-id="6437f-p119">Adds a new field to an existing provisioned content type. Propagates the change from the site content type to all child lists and content types within the site. For example:</span></span>

```xml
<AddContentTypeField 
     ContentTypeId="0x010100A6F9CE1AFE2A48f0A3E6CB5BB770B0F7" 
     FieldId="{B250DCFD-9310-4e2d-85F2-BE2DA37A57D2}" 
     PushDown="TRUE" />
```

<span data-ttu-id="6437f-221">**ApplyElementManifests**</span><span class="sxs-lookup"><span data-stu-id="6437f-221">**ApplyElementManifests**</span></span>

<span data-ttu-id="6437f-p120">Добавляет новый элемент к имеющемуся компоненту. При обновлении компонента подготавливаются все недекларативные элементы, на которые ссылаются указанные манифесты элементов.</span><span class="sxs-lookup"><span data-stu-id="6437f-p120">Adds a new element to an existing Feature. When a Feature is upgraded, provisions all non-declarative elements that are referenced in the specified element manifests.</span></span>

<span data-ttu-id="6437f-224">**VersionRange**</span><span class="sxs-lookup"><span data-stu-id="6437f-224">**VersionRange**</span></span>

<span data-ttu-id="6437f-225">Задает диапазон версий, к которым применяются указанные действия по обновлению.</span><span class="sxs-lookup"><span data-stu-id="6437f-225">Specifies a version range to which specified upgrade actions apply.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6437f-226">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6437f-226">Additional resources</span></span>
<span data-ttu-id="6437f-227"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6437f-227"></span></span>

-  [<span data-ttu-id="6437f-228">Веб-трансляция SharePoint PnP: подготовка ресурсов SharePoint для решения SPFx</span><span class="sxs-lookup"><span data-stu-id="6437f-228">SharePoint PnP Webcast - Provisioning SharePoint assets for your SPFx solution</span></span>](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS)
    
-  [<span data-ttu-id="6437f-229">Руководство: подготовка ресурсов SharePoint из клиентской веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="6437f-229">Tutorial - Provisioning SharePoint assets from your SharePoint client-side web part</span></span>](https://dev.office.com/sharepoint/docs/spfx/web-parts/get-started/provision-sp-assets-from-package)

-  <span data-ttu-id="6437f-230">
  [Стандартный блок SharePoint: компоненты](https://msdn.microsoft.com/ru-RU/library/ee537350.aspx)</span><span class="sxs-lookup"><span data-stu-id="6437f-230">[SharePoint Building Block: Features](https://msdn.microsoft.com/ru-RU/library/ee537350.aspx)</span></span>

-  [<span data-ttu-id="6437f-231">Компонент Framework: использование элемента UpgradeActions</span><span class="sxs-lookup"><span data-stu-id="6437f-231">Feature Framework - UpgradeAcctions element usage</span></span>](https://msdn.microsoft.com/ru-RU/library/office/ee537575.aspx)

-  [<span data-ttu-id="6437f-232">Компонент Framework: элемент Field</span><span class="sxs-lookup"><span data-stu-id="6437f-232">Feature Framework - Field Element</span></span>](https://msdn.microsoft.com/ru-RU/library/aa979575.aspx)

-  <span data-ttu-id="6437f-233">[Компонент Framework: элемент ContentType](https://msdn.microsoft.com/ru-RU/library/aa544268.aspx).aspx)</span><span class="sxs-lookup"><span data-stu-id="6437f-233">[Feature Framework - ContentType Element](https://msdn.microsoft.com/ru-RU/library/aa544268.aspx).aspx)</span></span>

-  [<span data-ttu-id="6437f-234">Компонент Framework: элемент ListInstance</span><span class="sxs-lookup"><span data-stu-id="6437f-234">Feature Framework - ListInstance Element</span></span>](https://msdn.microsoft.com/ru-RU/library/office/ms476062.aspx)
