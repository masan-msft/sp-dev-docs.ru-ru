---
title: "Краткие сведения о PnP модуля подготовки"
ms.date: 11/03/2017
ms.openlocfilehash: 5ffce93158a74f43b6428ba9ab04143eebd68c48
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="introducing-the-pnp-provisioning-engine"></a><span data-ttu-id="efa7e-102">Краткие сведения о PnP модуля подготовки</span><span class="sxs-lookup"><span data-stu-id="efa7e-102">Introducing the PnP Provisioning Engine</span></span>

<span data-ttu-id="efa7e-103">**Автор:** Paolo Pialorsi - [www.piasys.com](http://www.piasys.com/) - [@PaoloPia](https://www.twitter.com/PaoloPia/)</span><span class="sxs-lookup"><span data-stu-id="efa7e-103">**Author:** Paolo Pialorsi - [www.piasys.com](http://www.piasys.com/) - [@PaoloPia](https://www.twitter.com/PaoloPia/)</span></span>

<span data-ttu-id="efa7e-104">_**Применимо к:** SharePoint 2013 | SharePoint Online | Office 365_</span><span class="sxs-lookup"><span data-stu-id="efa7e-104">_**Applies to:** SharePoint 2013 | SharePoint Online | Office 365_</span></span>

<span data-ttu-id="efa7e-105">Этот технический документ короткий представляется PnP подготовки модуля, которая была выпущена в 2015 апреля в рамках проекта [PnP разработчик офисных решений](http://aka.ms/officedevpnp) и которого будут обновлены в месяц в выравнивание с график выпуска Office Dev PnP основной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="efa7e-105">This short whitepaper introduces the PnP Provisioning Engine, which was released in April 2015 within the [OfficeDev PnP](http://aka.ms/officedevpnp) project, and which will be updated on a monthly basis, in alignment with the release schedule of the Office Dev PnP Core Library.</span></span> <span data-ttu-id="efa7e-106">Что вы увидите здесь — это благодаря работе, некоторые из членов группы Office Dev PnP Core ([(Vesa juvonen)](https://twitter.com/vesajuvonen), [Jansen Бертом](https://twitter.com/O365Bert), [Фрэнк Marasco](https://twitter.com/frank_marasco), [Hunen van Эрвин](https://twitter.com/erwinvanhunen)и [me](https://twitter/paolopia)), а также всей сообщества PnP разработчик офисных решений .</span><span class="sxs-lookup"><span data-stu-id="efa7e-106">What you will see here is available thanks to the efforts of some of the Office Dev PnP Core Team members ([Vesa Juvonen](https://twitter.com/vesajuvonen), [Bert Jansen](https://twitter.com/O365Bert), [Frank Marasco](https://twitter.com/frank_marasco), [Erwin van Hunen](https://twitter.com/erwinvanhunen), and [me](https://twitter/paolopia)), as well as the whole OfficeDev PnP community.</span></span>

<span data-ttu-id="efa7e-107"><a name="thegoal"> </a></span><span class="sxs-lookup"><span data-stu-id="efa7e-107"></span></span>
## <a name="the-goal"></a><span data-ttu-id="efa7e-108">Цель</span><span class="sxs-lookup"><span data-stu-id="efa7e-108">The Goal</span></span>

<span data-ttu-id="efa7e-109">Давайте начнем из основной целью необходимости подготовки модуля.</span><span class="sxs-lookup"><span data-stu-id="efa7e-109">Let’s start from the main goal of having a provisioning engine.</span></span> <span data-ttu-id="efa7e-110">Вследствие внедрения Microsoft Office 365 и Microsoft SharePoint Online сталкиваются разработчики новая надстройка модель облачных (также называемого КАМЕРУ) как новый способ создания пользовательских программных решений для Microsoft SharePoint 2013, Microsoft SharePoint Online и Microsoft Office 365 в целом.</span><span class="sxs-lookup"><span data-stu-id="efa7e-110">With the introduction of Microsoft Office 365 and Microsoft SharePoint Online, developers are facing the new Cloud Add-in Model (aka CAM) as a new way of creating custom software solutions for Microsoft SharePoint 2013, Microsoft SharePoint Online, and Microsoft Office 365 in general.</span></span> <span data-ttu-id="efa7e-111">Тем не менее, во время в последние разработчиков подготовленных настраиваемых артефакты в основе XML CAML функции framework, либо с помощью решения с кодом полного доверия (также называемого FTC) или изолированные решения с помощью подготовки артефактов в новой модели КАМЕРУ должен быть выполнен с помощью удаленного « метод подготовки».</span><span class="sxs-lookup"><span data-stu-id="efa7e-111">However, while in the past developers provisioned custom artifacts using the CAML/XML-based features framework, either with Full Trust Code (aka FTC) solutions or Sandbox Solutions, provisioning artifacts in the new CAM model should be done via the "remote provisioning" technique.</span></span> <span data-ttu-id="efa7e-112">Тем не менее что означает для выполнения «удаленного обеспечения»?</span><span class="sxs-lookup"><span data-stu-id="efa7e-112">However, what does it mean to do "remote provisioning"?</span></span> <span data-ttu-id="efa7e-113">Это означает, с помощью модели объекта со стороны клиента (CSOM) для подготовки артефакты, вместо использования структура компонентов.</span><span class="sxs-lookup"><span data-stu-id="efa7e-113">It means using the Client Side Object Model (CSOM) to provision artifacts, instead of using the feature framework.</span></span>

<span data-ttu-id="efa7e-114">Что делать, если вы хотите модели и подготовка артефакты, с помощью тестовой и производственной среде, или что делать, если требуется автоматизировать подготовки артефактов, только то, что вы хотите продать свои настройки для нескольких клиентов?</span><span class="sxs-lookup"><span data-stu-id="efa7e-114">What if you want to model and provision artifacts using a test and a production environment, or what if you want to automate provisioning of artifacts, just because you want to sell your customizations to multiple customers?</span></span> <span data-ttu-id="efa7e-115">Аналогичным образом что делать, если нужно определить настраиваемый шаблон сайта, которое можно повторно использовать нескольких экземпляров сайтов, такой как сайты, ориентированные на клиента или project ориентированного сайты?</span><span class="sxs-lookup"><span data-stu-id="efa7e-115">Likewise, what if you want to define a custom site template that you can reuse across multiple site instances, like customer-oriented sites, or project-oriented sites?</span></span>

<span data-ttu-id="efa7e-116">С помощью новых PnP модуля подготовки, чтобы смоделировать сайта, настроив разработки столбцы сайта, типов контента, определения списков и экземпляры, вариантов оформления страниц (страницы веб-части или вики-страницы) и многое другое, с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="efa7e-116">Using the new PnP Provisioning Engine, you can model a site by configuring the design of Site Columns, Content Types, List Definitions and Instances, Composed Looks, Pages (either WebPart Pages or Wiki Pages), and much more, via your web browser.</span></span> <span data-ttu-id="efa7e-117">После завершения разработки можно экспортировать, что вы выполнили в сохраняемого подготовки формат шаблона (XML, JSON или усмотрение) и как многие целевого сайтов, как можно применить шаблона, чтобы.</span><span class="sxs-lookup"><span data-stu-id="efa7e-117">When you are done with the design, you can export what you have done into a persistent provisioning template format (XML, JSON, or whatever you like), and you can apply that template to as many target sites as you would like.</span></span>

<span data-ttu-id="efa7e-118">Если звуки интересных... продолжайте читать и давайте Узнайте, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="efa7e-118">If it sounds interesting... keep reading, and let’s learn how to do it!</span></span>

<span data-ttu-id="efa7e-119"><a name="creatingtemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="efa7e-119"></span></span>
## <a name="creating-a-provisioning-template"></a><span data-ttu-id="efa7e-120">Создание шаблона подготовки</span><span class="sxs-lookup"><span data-stu-id="efa7e-120">Creating a Provisioning Template</span></span>

<span data-ttu-id="efa7e-121">Как уже упоминалось, — это самый простой способ создания настраиваемого шаблона подготовки для создания новой нового семейства веб-сайтов в Microsoft SharePoint Online, настройка вашего артефактов (состоит выглядеть, столбцы сайта, типы содержимого, экземпляры списков, страницы, файлы, и т.д.) и Сохраните результат в качестве шаблона подготовки.</span><span class="sxs-lookup"><span data-stu-id="efa7e-121">As already stated, the easiest way to create a custom provisioning template is to create a fresh new site collection in Microsoft SharePoint Online, configure your artifacts (Composed Look, Site Columns, Content Types, Lists Instances, Pages, Files, etc.) and to save the result as a Provisioning Template.</span></span>

<span data-ttu-id="efa7e-122">Таким образом, давайте предположим, определения сайтов пример с пользовательским выглядеть (настраиваемые цвета темы, настраиваемый логотип, настраиваемые фонового изображения).</span><span class="sxs-lookup"><span data-stu-id="efa7e-122">Thus, let's say you have defined a sample site with a custom look (custom color theme, custom logo, custom background image).</span></span> <span data-ttu-id="efa7e-123">Можно просмотреть итоговый домашней страницы на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="efa7e-123">You can see the resulting Home Page in the following figure.</span></span>

![Домашней странице шаблона сайта](./media/Introducing-the-PnP-Provisioning-Engine/Figure-1-SiteTemplate01.png)

<span data-ttu-id="efa7e-125">Кроме того вы определили несколько столбцов сайта, тип контента и библиотека накладных с настраиваемым представлением.</span><span class="sxs-lookup"><span data-stu-id="efa7e-125">Moreover, you have defined a couple of Site Columns, a Content Type and a Library of Invoices with a custom View.</span></span> <span data-ttu-id="efa7e-126">В двух следующих рисунках можно увидеть результат.</span><span class="sxs-lookup"><span data-stu-id="efa7e-126">In the two following figures you can see the result.</span></span>

![Библиотека накладных с настраиваемого типа контента](./media/Introducing-the-PnP-Provisioning-Engine/Figure-2-SiteTemplate02.png)

![На странице Параметры библиотеки счетов](./media/Introducing-the-PnP-Provisioning-Engine/Figure-3-SiteTemplate03.png)

<span data-ttu-id="efa7e-129">Чтобы экспортировать этого сайта в качестве шаблона подготовки, можно либо использовать PowerShell (благодаря усилия [Эрвин](https://twitter.com/erwinvanhunen)!) или CSOM к коду с некоторые методы расширения, которые предоставляются PnP Библиотека базовых разработчик офисных решений.</span><span class="sxs-lookup"><span data-stu-id="efa7e-129">In order to export that site as a Provisioning Template, you can either use PowerShell (thanks to the efforts of [Erwin](https://twitter.com/erwinvanhunen)!) or CSOM code, with some extension methods, which are provided by the OfficeDev PnP Core Library.</span></span> 

<span data-ttu-id="efa7e-130">Чтобы использовать расширения PowerShell, можно просто просмотреть правильный URL-адрес ([http://aka.ms/officedevpnpcmdlets16](http://aka.ms/officedevpnpcmdlets16) для Microsoft SharePoint Online) или [http://aka.ms/officedevpnpcmdlets15](http://aka.ms/officedevpnpcmdlets15) для Microsoft SharePoint 2013 и установка расширения PnP основных PowerShell разработчик офисных решений.</span><span class="sxs-lookup"><span data-stu-id="efa7e-130">In order to use the PowerShell extensions, you can simply browse to the proper URL ([http://aka.ms/officedevpnpcmdlets16](http://aka.ms/officedevpnpcmdlets16) for Microsoft SharePoint Online, or [http://aka.ms/officedevpnpcmdlets15](http://aka.ms/officedevpnpcmdlets15) for Microsoft SharePoint 2013) and install the OfficeDev PnP Core PowerShell extensions.</span></span> <span data-ttu-id="efa7e-131">После подключения среды PowerShell для Microsoft Office 365 с помощью командлета *Connect-SPOnline* , можно использовать следующий командлет PowerShell:</span><span class="sxs-lookup"><span data-stu-id="efa7e-131">After you have connected your PowerShell environment to Microsoft Office 365, by using the *Connect-SPOnline* cmdlet, you will be able to use the following PowerShell cmdlet:</span></span>

<span data-ttu-id="efa7e-132">*Get-SPOProvisioningTemplate-выходной параметр «PnP подготовки File.xml»*</span><span class="sxs-lookup"><span data-stu-id="efa7e-132">*Get-SPOProvisioningTemplate -Out "PnP-Provisioning-File.xml"*</span></span>

<span data-ttu-id="efa7e-133">*– Выходной параметр* аргумент, то предписывает командлету о том, куда требуется сохранить шаблон подготовки.</span><span class="sxs-lookup"><span data-stu-id="efa7e-133">The *–Out* argument instructs the cmdlet about where to save the Provisioning Template.</span></span>

<span data-ttu-id="efa7e-134">С другой стороны, для использования расширений CSOM может просто создание любого типа (консоли Windows, SharePoint надстройки, независимо от вы хотите) проекта программного обеспечения .NET и добавьте пакет PnP NuGet разработчик офисных решений.</span><span class="sxs-lookup"><span data-stu-id="efa7e-134">On the other side, in order to use the CSOM extensions, you can simply create any kind (Console, Windows, SharePoint Add-in, whatever you like) of .NET software project, and add the OfficeDev PnP NuGet Package.</span></span> <span data-ttu-id="efa7e-135">Доступен пакет NuGet двух видов: PnP основных V15 разработчик офисных решений, который предназначен для Microsoft SharePoint 2013 в локальной, и разработчик офисных решений PnP процессор, который предназначен для Microsoft SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="efa7e-135">The NuGet Package is available in two flavors: OfficeDev PnP Core V15, which targets Microsoft SharePoint 2013 on-premises, and OfficeDev PnP Core, which targets Microsoft SharePoint Online.</span></span>

<span data-ttu-id="efa7e-136">Давайте предназначенных для Microsoft SharePoint Online, который более было протестировано и является основной целью усилия PnP основных групп.</span><span class="sxs-lookup"><span data-stu-id="efa7e-136">Let's target Microsoft SharePoint Online, which has been tested more, and is the main target of the PnP Core Team efforts.</span></span> <span data-ttu-id="efa7e-137">Просто необходимо подключение к Microsoft Office 365, создайте экземпляр *ClientContext* и получить ссылку на объект *Web* .</span><span class="sxs-lookup"><span data-stu-id="efa7e-137">You will simply need to connect to Microsoft Office 365, create a *ClientContext* instance and retrieve a reference to a *Web* object.</span></span> <span data-ttu-id="efa7e-138">Благодаря новый метод расширения с именем *GetProvisioningTemplate*вы сможете получить объект *ProvisioningTemplate* , которые могут быть сохранены с помощью шаблона поставщика и форматирования сериализации.</span><span class="sxs-lookup"><span data-stu-id="efa7e-138">Thanks to a new extension method, called *GetProvisioningTemplate*, you will be able to retrieve a *ProvisioningTemplate* object that can be saved using a template provider and a serialization formatter.</span></span> <span data-ttu-id="efa7e-139">Поставщик шаблонов и объекты форматирования данных сериализации можно настраивать, так, чтобы реализовать любые сохраняемость хранилища и сериализации форматирование вы хотите.</span><span class="sxs-lookup"><span data-stu-id="efa7e-139">Both the template provider and the serialization formatter objects can be customized, so that you can implement whatever persistence storage and serialization format you like.</span></span> <span data-ttu-id="efa7e-140">По умолчанию PnP модуля подготовки предоставляет поддержку для поставщиков шаблон файловой системы, SharePoint и Azure хранилища больших двоичных объектов, а также для форматирования данных сериализации XML и JSON.</span><span class="sxs-lookup"><span data-stu-id="efa7e-140">Out of the box, the PnP Provisioning Engine provides support for File System, SharePoint, and Azure Blob Storage template providers, as well as for XML and JSON serialization formatters.</span></span> <span data-ttu-id="efa7e-141">На следующем рисунке (кредитов для [Vesa](https://twitter.com/vesajuvonen)) могут видеть контур в общей архитектуре PnP модуля подготовки.</span><span class="sxs-lookup"><span data-stu-id="efa7e-141">In the following figure (credits to [Vesa](https://twitter.com/vesajuvonen)) you can see an outline of the overall architecture of the PnP Provisioning Engine.</span></span>

![Архитектура PnP платформы модуля подготовки](./media/Introducing-the-PnP-Provisioning-Engine/Figure-4-PnP-Provisioning-Framework-Outline.png)

<span data-ttu-id="efa7e-143">В результате извлечение и сохранение объект экземпляра *ProvisioningTemplate* будет для экземпляра XML-файла, как показано в следующем фрагменте кода XML:</span><span class="sxs-lookup"><span data-stu-id="efa7e-143">The result of extracting and saving a *ProvisioningTemplate* instance object will be for instance an XML file like the one shown in the following XML code excerpt:</span></span>
    
    <?xml version="1.0"?>
    <pnp:Provisioning xmlns:pnp="http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema">
      <pnp:Preferences Generator="OfficeDevPnP.Core, Version=1.2.515.0, Culture=neutral, PublicKeyToken=null" />
      <pnp:Templates ID="CONTAINER-TEMPLATE-1D3F60898418437E8B275147BEC7B0F5">
    <pnp:ProvisioningTemplate ID="TEMPLATE-1D3F60898418437E8B275147BEC7B0F5" Version="1">
      <pnp:Security>
    <pnp:AdditionalAdministrators>
      <pnp:User Name="i:0#.f|membership|paolo@piasysdev.onmicrosoft.com" />
    </pnp:AdditionalAdministrators>
      </pnp:Security>
      <pnp:Files>
    <pnp:File Src="PnP.png" Folder="SiteAssets" Overwrite="true" />
    <pnp:File Src="STB13_Rick_01_small.png" Folder="SiteAssets" Overwrite="true" />
      </pnp:Files>
      <pnp:SiteFields>
    <Field Type="DateTime" DisplayName="Invoice Date" Required="FALSE" EnforceUniqueValues="FALSE"
        Indexed="FALSE" Format="DateOnly" Group="PnP Columns" FriendlyDisplayFormat="Disabled"
        ID="{f1c6f202-f976-4f4e-b0a3-8b984991d00d}" SourceID="{5a15b9ca-4410-4854-bc61-d7fb0ff84e56}"
        StaticName="PnPInvoiceDate" Name="PnPInvoiceDate" CalType="0">
      <Default>[today]</Default>
    </Field>
    <Field Type="Text" DisplayName="Invoice Number" Required="FALSE" 
        EnforceUniqueValues="FALSE" Indexed="FALSE" MaxLength="20" Group="PnP Columns"
        ID="{5049a822-424c-4479-9648-79c4b3214375}" SourceID="{5a15b9ca-4410-4854-bc61-d7fb0ff84e56}"
        StaticName="PnPInvoiceNumber" Name="PnPInvoiceNumber">
    </Field>
      </pnp:SiteFields>
      <pnp:ContentTypes>
    <pnp:ContentType ID="0x01010097931365769EE34E9078576A150FF52E" Name="Invoice"
        Description="" Group="PnP Content Types">
      <pnp:FieldRefs>
    <pnp:FieldRef ID="5049a822-424c-4479-9648-79c4b3214375" Name="PnPInvoiceNumber" />
    <pnp:FieldRef ID="f1c6f202-f976-4f4e-b0a3-8b984991d00d" Name="PnPInvoiceDate" />
      </pnp:FieldRefs>
    </pnp:ContentType>
      </pnp:ContentTypes>
      <pnp:Lists>
    <pnp:ListInstance Title="Invoices" Description=""
        DocumentTemplate="{site}/Invoices/Forms/template.dotx" TemplateType="101" Url="Invoices"
        EnableVersioning="true" MinorVersionLimit="0" MaxVersionLimit="500"
        TemplateFeatureID="00bfea71-e717-4e80-aa17-d0c71b360101" ContentTypesEnabled="true"
        EnableAttachments="false">
      <pnp:ContentTypeBindings>
    <pnp:ContentTypeBinding ContentTypeID="0x01010097931365769EE34E9078576A150FF52E" Default="true" />
      </pnp:ContentTypeBindings>
      <pnp:Views>
    <View Name="{3D715498-8FA2-4B80-8D35-885B2A4CCBDE}" MobileView="TRUE" MobileDefaultView="TRUE"
            Type="HTML" DisplayName="All Documents"
            Url="/sites/PnPProvisioningDemo/Invoices/Forms/AllItems.aspx" Level="1"
            BaseViewID="1" ContentTypeID="0x" ImageUrl="/_layouts/15/images/dlicon.png?rev=38">
      <Query>
    <OrderBy>
      <FieldRef Name="FileLeafRef" />
    </OrderBy>
      </Query>
      <ViewFields>
    <FieldRef Name="DocIcon" />
    <FieldRef Name="LinkFilename" />
    <FieldRef Name="Modified" />
    <FieldRef Name="Editor" />
      </ViewFields>
      <RowLimit Paged="TRUE">30</RowLimit>
      <JSLink>clienttemplates.js</JSLink>
      <XslLink Default="TRUE">main.xsl</XslLink>
      <Toolbar Type="Standard" />
    </View>
    <View Name="{D9BC935E-2154-47EE-A9E2-7C9490389007}" DefaultView="TRUE" MobileView="TRUE"
            Type="HTML" DisplayName="All Invoices"
            Url="/sites/PnPProvisioningDemo/Invoices/Forms/All Invoices.aspx" Level="1"
            BaseViewID="1" ContentTypeID="0x" ImageUrl="/_layouts/15/images/dlicon.png?rev=38">
      <Query>
    <OrderBy>
      <FieldRef Name="FileLeafRef" />
    </OrderBy>
      </Query>
      <ViewFields>
    <FieldRef Name="DocIcon" />
    <FieldRef Name="LinkFilename" />
    <FieldRef Name="Modified" />
    <FieldRef Name="Editor" />
    <FieldRef Name="PnPInvoiceDate" />
    <FieldRef Name="PnPInvoiceNumber" />
      </ViewFields>
      <RowLimit Paged="TRUE">30</RowLimit>
      <Aggregations Value="Off" />
      <JSLink>clienttemplates.js</JSLink>
      <XslLink Default="TRUE">main.xsl</XslLink>
      <Toolbar Type="Standard" />
    </View>
      </pnp:Views>
      <pnp:FieldRefs>
    <pnp:FieldRef ID="5049a822-424c-4479-9648-79c4b3214375" Name="PnPInvoiceNumber"
            DisplayName="Invoice Number" />
    <pnp:FieldRef ID="f1c6f202-f976-4f4e-b0a3-8b984991d00d" Name="PnPInvoiceDate"
            DisplayName="Invoice Date" />
      </pnp:FieldRefs>
    </pnp:ListInstance>
      </pnp:Lists>
      <pnp:Features />
      <pnp:CustomActions />
      <pnp:ComposedLook
    BackgroundFile="{sitecollection}/SiteAssets/STB13_Rick_01_small.png"
    ColorFile="{sitecollection}/_catalogs/theme/15/Palette012.spcolor"
    SiteLogo="{sitecollection}/SiteAssets/PnP.png"
    Name="RED"
    MasterPage="{sitecollection}/_catalogs/masterpage/seattle.master"
    FontFile="" />
    </pnp:ProvisioningTemplate>
      </pnp:Templates>
    </pnp:Provisioning>
    

<span data-ttu-id="efa7e-144">Как вы видите, XML-элементы, названию.</span><span class="sxs-lookup"><span data-stu-id="efa7e-144">As you can see, the XML elements are fairly self-explanatory.</span></span> <span data-ttu-id="efa7e-145">XML-схемы, используемые в этом примере ссылается на 201505 версию PnP подготовки схемы (пространство имен XML: *http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema*), который был определен вместе с сообществом PnP разработчик офисных решений и что можно найти на репозиториев по следующему URL-АДРЕСУ: [https://github.com/SharePoint/Pnp-Provisioning-Schema/](https://github.com/SharePoint/Pnp-Provisioning-Schema/).</span><span class="sxs-lookup"><span data-stu-id="efa7e-145">The XML schema used in the example references the 201505 version of the PnP Provisioning Schema (XML Namespace: *http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema*), which has been defined together with the OfficeDev PnP Community, and which can be found on GitHub at the following URL: [https://github.com/SharePoint/Pnp-Provisioning-Schema/](https://github.com/SharePoint/Pnp-Provisioning-Schema/).</span></span> <span data-ttu-id="efa7e-146">В одном репозитории находятся наценки (MD) автоматически созданный документ с описываются основные элементы, типы и атрибуты, доступные для вручную определить шаблон подготовки XML.</span><span class="sxs-lookup"><span data-stu-id="efa7e-146">Within the same repository, you will also find a markdown (MD) auto-generated document, which describes the main elements, types, and attributes available to manually define an XML provisioning template.</span></span>

<span data-ttu-id="efa7e-147">Тем не менее в реальных степень этот модуль подготовки — это доступности высокого уровня, формат сериализации, вне зависимости от модели домена.</span><span class="sxs-lookup"><span data-stu-id="efa7e-147">However, the real power of this provisioning engine is the availability of a high-level, serialization format that is independent of the Domain Model.</span></span> <span data-ttu-id="efa7e-148">На самом деле во внутренней сети PnP модуля подготовки полностью отделены от любого типа формат сериализации и всей engine просто обрабатывает экземпляры типа *ProvisioningTemplate* .</span><span class="sxs-lookup"><span data-stu-id="efa7e-148">In fact, internally the PnP Provisioning Engine is completely decoupled from any kind of serialization format, and the whole engine simply handles instances of the *ProvisioningTemplate* type.</span></span> <span data-ttu-id="efa7e-149">Например на следующем рисунке видно окно «Контрольное значение» Microsoft Visual Studio 2013 отображение экземпляр объекта ProvisioningTemplate.</span><span class="sxs-lookup"><span data-stu-id="efa7e-149">For instance, in the following figure you can see the "Quick Watch" window of Microsoft Visual Studio 2013 showing a ProvisioningTemplate object instance.</span></span>

![Структура - в рамках отслеживания отладчика - объекта ProvisioningTemplate](./media/Introducing-the-PnP-Provisioning-Engine/Figure-5-Domain-Model.png)

<span data-ttu-id="efa7e-151">Вы можете определить *ProvisioningTemplate* вручную, с помощью узла бизнес-моделей, или путем создания XML-документа, которое проверяет PnP подготовки схемы XSD или путем написания кода .NET и создав иерархия объектов это.</span><span class="sxs-lookup"><span data-stu-id="efa7e-151">It is up to you to define the *ProvisioningTemplate* manually, using a model site, or by composing an XML document that validates against the PnP Provisioning XSD Schema, or by simply writing .NET code and constructing the hierarchy of objects.</span></span> <span data-ttu-id="efa7e-152">Можно даже выполнить сочетание этих подходов: проектирование подготовки шаблона, с помощью узла бизнес-моделей, сохраните его в XML-файл и выполните ряд настроек в памяти при обработке экземпляра *ProvisioningTemplate* в коде.</span><span class="sxs-lookup"><span data-stu-id="efa7e-152">You can even do a mix of these approaches: you can design the provisioning template using a model site, save it into an XML file, and do some in-memory customizations, while handling the *ProvisioningTemplate* instance in your code.</span></span>

<span data-ttu-id="efa7e-153"><a name="applyingtemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="efa7e-153"></span></span>
## <a name="applying-a-provisioning-template"></a><span data-ttu-id="efa7e-154">Применение шаблона подготовки</span><span class="sxs-lookup"><span data-stu-id="efa7e-154">Applying a Provisioning Template</span></span>

<span data-ttu-id="efa7e-155">Теперь, когда вы узнали, что шаблон подготовки и как извлечь домена модели объектов из существующего веб-сайтов, можно приступать к его применения к целевого сайта.</span><span class="sxs-lookup"><span data-stu-id="efa7e-155">Now that you have seen what a Provisioning Template is, and how to extract the Domain Model object from an existing site, you are ready to apply it to a target site.</span></span> <span data-ttu-id="efa7e-156">Давайте предположим, что другой новым нового семейства сайтов в Microsoft SharePoint Online, которая была создана на основе шаблона сайта группы, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="efa7e-156">Let's say that you have another fresh new Site Collection in Microsoft SharePoint Online that has been created using the Team Site template, like it is shown in the following figure.</span></span>
 
![SharePoint Online страницы для создания нового семейства веб-сайтов](./media/Introducing-the-PnP-Provisioning-Engine/Figure-6-Target-Site-Creation.png)

<span data-ttu-id="efa7e-158">По умолчанию сайт будет выглядеть как на следующем рисунке, являющийся макета по умолчанию сайта SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="efa7e-158">By default, the site will look like the following figure, which is the default layout of a SharePoint Online site.</span></span>

![На домашней странице новым новой цели](./media/Introducing-the-PnP-Provisioning-Engine/Figure-7-Target-Site-Created.png)

<span data-ttu-id="efa7e-160">Теперь можно применить настраиваемого экземпляра объекта *ProvisioningTemplate* за счет использования PowerShell или путем написания кода .NET.</span><span class="sxs-lookup"><span data-stu-id="efa7e-160">You can now apply a custom *ProvisioningTemplate* instance object either by utilizing PowerShell, or by writing .NET code.</span></span> <span data-ttu-id="efa7e-161">Если вы хотите использовать PowerShell, в следующем фрагменте демонстрируется, как можно использовать командлет *SPOProvisioningTemplate применить* .</span><span class="sxs-lookup"><span data-stu-id="efa7e-161">If you want to use PowerShell, the following excerpt shows how you can utilize the *Apply-SPOProvisioningTemplate* cmdlet.</span></span>

<span data-ttu-id="efa7e-162">*Применение SPOProvisioningTemplate-Path «PnP подготовки File.xml»*</span><span class="sxs-lookup"><span data-stu-id="efa7e-162">*Apply-SPOProvisioningTemplate -Path "PnP-Provisioning-File.xml"*</span></span>

<span data-ttu-id="efa7e-163">*– Путь* аргумент ссылается на файл шаблона источника командлета автоматически применяется к сайту подключенных (подразумевается командлета *Connect-SPOnline* ).</span><span class="sxs-lookup"><span data-stu-id="efa7e-163">The *–Path* argument refers to the source template file, which the cmdlet will automatically apply to the currently connected site (implied by the *Connect-SPOnline* cmdlet).</span></span> <span data-ttu-id="efa7e-164">На следующем рисунке видно конечный результат.</span><span class="sxs-lookup"><span data-stu-id="efa7e-164">In the following figure you can see the final result.</span></span>

![Домашней страницы конечного сайта, основанного на подготовки шаблона](./media/Introducing-the-PnP-Provisioning-Engine/Figure-8-Target-Site-Provisioned.png)

<span data-ttu-id="efa7e-166">Как вы видите, имеет внешний вид как исходного шаблона сайта, а также библиотеки счетов, все же базовую структуру и конфигурации (столбцы сайта, типов контента, и т.д.).</span><span class="sxs-lookup"><span data-stu-id="efa7e-166">As you can see, the site has the same look as the original template, and it includes the Invoices library, with all of the same underlying structure and configuration (Site Columns, Content Types, etc.).</span></span>

<span data-ttu-id="efa7e-167">Как насчет с использованием кода .NET?</span><span class="sxs-lookup"><span data-stu-id="efa7e-167">What about using .NET code?</span></span> <span data-ttu-id="efa7e-168">Здесь приведен фрагмент по использованию CSOM и разработчик офисных решений PnP Библиотека базовых методов расширения для применения этого шаблона.</span><span class="sxs-lookup"><span data-stu-id="efa7e-168">Here is an excerpt on how to use CSOM and the OfficeDev PnP Core Library extension methods to apply the template.</span></span>

    using (var context = new ClientContext(destinationUrl))
    {
      context.Credentials = new SharePointOnlineCredentials(userName, password);
      Web web = context.Web;
      context.Load(web, w => w.Title);
      context.ExecuteQueryRetry();
    
      // Configure the XML file system provider
      XMLTemplateProvider provider =
      new XMLFileSystemTemplateProvider(
        String.Format(@"{0}\..\..\",
        AppDomain.CurrentDomain.BaseDirectory),
        "");
    
      // Load the template from the XML stored copy
      ProvisioningTemplate template = provider.GetTemplate(
        "PnP-Provisioning-Demo-201505-Polished.xml");
    
      // Apply the template to another site
      Console.WriteLine("Start: {0:hh.mm.ss}", DateTime.Now);
    
      // We can also use Apply-SPOProvisioningTemplate
      web.ApplyProvisioningTemplate(template);
     
      Console.WriteLine("End: {0:hh.mm.ss}", DateTime.Now);
    }
    
<span data-ttu-id="efa7e-169">Чтобы начать, необходимо создать экземпляр объекта шаблона поставщика, в зависимости от того, какой тип сохраняемость, который будет использоваться для сохранения и загрузите шаблон.</span><span class="sxs-lookup"><span data-stu-id="efa7e-169">To start, you need to create an instance of a Template Provider object, depending on what kind of persistence you will use to save and load the template.</span></span>  <span data-ttu-id="efa7e-170">Затем загрузите шаблон из репозитория исходного с помощью метода *GetTemplate* .</span><span class="sxs-lookup"><span data-stu-id="efa7e-170">Next, you load the template from the source repository, by using the *GetTemplate* method.</span></span> <span data-ttu-id="efa7e-171">И, наконец шаблон будет применяться для целевого сайта с помощью метода расширения *ApplyProvisioningTemplate* типа Web.</span><span class="sxs-lookup"><span data-stu-id="efa7e-171">Lastly, you will apply the template to the target site, using the *ApplyProvisioningTemplate* extension method of the Web type.</span></span>

<span data-ttu-id="efa7e-172">В среднем библиотеке может занять несколько минут, чтобы применить шаблон, независимо от того, является ли вы используете код PowerShell или .NET.</span><span class="sxs-lookup"><span data-stu-id="efa7e-172">On average, the library will take a couple of minutes to apply the template, regardless of whether you are utilizing PowerShell or .NET code.</span></span> <span data-ttu-id="efa7e-173">При желании можно регистрировать делегат для наблюдения за весь процесс подготовки во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="efa7e-173">If desired, you can register a delegate to monitor the overall process, while the provisioning is in progress.</span></span> <span data-ttu-id="efa7e-174">Мы по-прежнему повышается производительность ядра и на данный момент мы шла внимание на возможностях и функциях.</span><span class="sxs-lookup"><span data-stu-id="efa7e-174">We are still improving performances of the engine, and so far we have focused our attention on capabilities and functionalities.</span></span>

<span data-ttu-id="efa7e-175"><a name="advancedtopics"> </a></span><span class="sxs-lookup"><span data-stu-id="efa7e-175"></span></span>
## <a name="advanced-topics"></a><span data-ttu-id="efa7e-176">Дополнительные разделы</span><span class="sxs-lookup"><span data-stu-id="efa7e-176">Advanced Topics</span></span>

<span data-ttu-id="efa7e-177">Это просто вводную статью в ближайшем будущем будет рассмотрения глубокого вокруг некоторые дополнительные разделы.</span><span class="sxs-lookup"><span data-stu-id="efa7e-177">This is just an introductory article, as in the near future we will go deeper around some more advanced topics.</span></span> <span data-ttu-id="efa7e-178">Тем не менее, важно понимать, что с помощью новых PnP модуля подготовки, вы может также подготовить таксономии, а также использовать переменные и маркеры, которые можно заменить во время выполнения, в зависимости от того, что подготовки (идентификаторы список параметров, идентификаторы терминов, и т.д.).</span><span class="sxs-lookup"><span data-stu-id="efa7e-178">Nevertheless, it is important to understand that using the new PnP Provisioning Engine, you can also provision Taxonomies, as well as use variables and tokens, which can be replaced at runtime, based on what you are provisioning (List IDs, Parameters, Term IDs, etc.).</span></span> <span data-ttu-id="efa7e-179">Можно вызвать модуля подготовки из служб задания таймера, размещением у поставщика надстроек, внешние сайты и др.</span><span class="sxs-lookup"><span data-stu-id="efa7e-179">You can invoke the provisioning engine from timer job services, provider-hosted add-ins, external sites, and more.</span></span> <span data-ttu-id="efa7e-180">И, наконец можно использовать PnP модуля подготовки для переноса артефактов из тестовой/промежуточной среды в производственную среду.</span><span class="sxs-lookup"><span data-stu-id="efa7e-180">Lastly, you can use the PnP Provisioning Engine to move artifacts from test/staging environments to production environments.</span></span>

<span data-ttu-id="efa7e-181">Кроме того на Channel 9 имеется [раздел выделенный PnP разработчик офисных решений](http://aka.ms/OfficeDevPnPVideos), где посмотреть некоторые видеоматериалы по PnP модуля подготовки и PnP расширения PowerShell:</span><span class="sxs-lookup"><span data-stu-id="efa7e-181">Moreover, on Channel 9 there is a [section dedicated to OfficeDev PnP](http://aka.ms/OfficeDevPnPVideos), where you can watch some videos about the PnP Provisioning Engine and the PnP PowerShell Extensions:</span></span>

- [<span data-ttu-id="efa7e-182">Приступая к работе с PnP модуля подготовки</span><span class="sxs-lookup"><span data-stu-id="efa7e-182">Getting Started with PnP Provisioning Engine</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine)
- [<span data-ttu-id="efa7e-183">Глубокое погружение PnP схеме модуля подготовки</span><span class="sxs-lookup"><span data-stu-id="efa7e-183">Deep dive to PnP provisioning engine schema</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
- [<span data-ttu-id="efa7e-184">Общие сведения о PnP командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="efa7e-184">Introduction to PnP PowerShell Cmdlets</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets)

<span data-ttu-id="efa7e-185"><a name="wrapup"> </a></span><span class="sxs-lookup"><span data-stu-id="efa7e-185"></span></span>
## <a name="requirements-and-wrap-up"></a><span data-ttu-id="efa7e-186">Требования и Wrap копирования</span><span class="sxs-lookup"><span data-stu-id="efa7e-186">Requirements and Wrap Up</span></span> ##

<span data-ttu-id="efa7e-187">Для воспроизведения с PnP модуля подготовки локальной вы должны иметь по крайней мере SharePoint 2013 марта 2015 накопительный пакет обновления установлен, как ядро использует некоторых [новых возможностей](http://blogs.msdn.com/b/vesku/archive/2015/04/10/new-sharepoint-csom-version-released-for-office-365.aspx) объектной модели со стороны клиента которых не доступны в предыдущие версии продукта.</span><span class="sxs-lookup"><span data-stu-id="efa7e-187">In order to play with the PnP Provisioning Engine on-premises, you need to have at least the SharePoint 2013 March 2015 Cumulative Update installed, as the engine leverages some [new capabilities](http://blogs.msdn.com/b/vesku/archive/2015/04/10/new-sharepoint-csom-version-released-for-office-365.aspx) of the Client Side Object Model, which are not available in previous versions of the product.</span></span> <span data-ttu-id="efa7e-188">При использовании Microsoft SharePoint Online, требования автоматически удовлетворяются благодаря программное обеспечение как модель службы.</span><span class="sxs-lookup"><span data-stu-id="efa7e-188">If you target Microsoft SharePoint Online, the requirements are automatically satisfied thanks to the Software as a Service model.</span></span>

<span data-ttu-id="efa7e-189">Пожалуйста Поэкспериментируйте с PnP модуля подготовки, отзыв и находят истинное наслаждение будущее модели надстройки SharePoint и удаленных подготовки!</span><span class="sxs-lookup"><span data-stu-id="efa7e-189">Please, play with the PnP Provisioning Engine, give us feedback, and enjoy the future of the SharePoint Add-in Model and remote provisioning!</span></span>

<span data-ttu-id="efa7e-190"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="efa7e-190"></span></span>
## <a name="see-also"></a><span data-ttu-id="efa7e-191">См. также</span><span class="sxs-lookup"><span data-stu-id="efa7e-191">See also</span></span>

-  [<span data-ttu-id="efa7e-192">Шаблоны разработки Office 365 и рекомендации на репозиториев</span><span class="sxs-lookup"><span data-stu-id="efa7e-192">Office 365 Development Patterns & Practices on GitHub</span></span>](https://github.com/SharePoint/PnP/)
-  <span data-ttu-id="efa7e-193">[Группы разработчиков SharePoint](http://aka.ms/sppnp-community) в Microsoft Tech сообщества</span><span class="sxs-lookup"><span data-stu-id="efa7e-193">[SharePoint Developer Group](http://aka.ms/sppnp-community) at Microsoft Tech Community</span></span>
