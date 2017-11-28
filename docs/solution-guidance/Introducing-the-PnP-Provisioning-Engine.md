---
title: "Краткие сведения о PnP модуля подготовки"
ms.date: 11/03/2017
ms.openlocfilehash: 5f27bf0ad8eb45d8af78f1be0bc46a99858c9254
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="introducing-the-pnp-provisioning-engine"></a>Краткие сведения о PnP модуля подготовки

**Автор:** Paolo Pialorsi - [www.piasys.com](http://www.piasys.com/) - [@PaoloPia](https://www.twitter.com/PaoloPia/)

_**Применимо к:** SharePoint 2013 | SharePoint Online | Office 365_

Этот технический документ короткий представляется PnP подготовки модуля, которая была выпущена в 2015 апреля в рамках проекта [PnP разработчик офисных решений](http://aka.ms/officedevpnp) и которого будут обновлены в месяц в выравнивание с график выпуска Office Dev PnP основной библиотеки. Что вы увидите здесь — это благодаря работе, некоторые из членов группы Office Dev PnP Core ([(Vesa juvonen)](https://twitter.com/vesajuvonen), [Jansen Бертом](https://twitter.com/O365Bert), [Фрэнк Marasco](https://twitter.com/frank_marasco), [Hunen van Эрвин](https://twitter.com/erwinvanhunen)и [me](https://twitter/paolopia)), а также всей сообщества PnP разработчик офисных решений .

<a name="thegoal"> </a>
## <a name="the-goal"></a>Цель

Давайте начнем из основной целью необходимости подготовки модуля. Вследствие внедрения Microsoft Office 365 и Microsoft SharePoint Online сталкиваются разработчики новая надстройка модель облачных (также называемого КАМЕРУ) как новый способ создания пользовательских программных решений для Microsoft SharePoint 2013, Microsoft SharePoint Online и Microsoft Office 365 в целом. Тем не менее, во время в последние разработчиков подготовленных настраиваемых артефакты в основе XML CAML функции framework, либо с помощью решения с кодом полного доверия (также называемого FTC) или изолированные решения с помощью подготовки артефактов в новой модели КАМЕРУ должен быть выполнен с помощью удаленного « метод подготовки». Тем не менее что означает для выполнения «удаленного обеспечения»? Это означает, с помощью модели объекта со стороны клиента (CSOM) для подготовки артефакты, вместо использования структура компонентов.

Что делать, если вы хотите модели и подготовка артефакты, с помощью тестовой и производственной среде, или что делать, если требуется автоматизировать подготовки артефактов, только то, что вы хотите продать свои настройки для нескольких клиентов? Аналогичным образом что делать, если нужно определить настраиваемый шаблон сайта, которое можно повторно использовать нескольких экземпляров сайтов, такой как сайты, ориентированные на клиента или project ориентированного сайты?

С помощью новых PnP модуля подготовки, чтобы смоделировать сайта, настроив разработки столбцы сайта, типов контента, определения списков и экземпляры, вариантов оформления страниц (страницы веб-части или вики-страницы) и многое другое, с помощью веб-браузера. После завершения разработки можно экспортировать, что вы выполнили в сохраняемого подготовки формат шаблона (XML, JSON или усмотрение) и как многие целевого сайтов, как можно применить шаблона, чтобы.

Если звуки интересных... продолжайте читать и давайте Узнайте, как это сделать.

<a name="creatingtemplate"> </a>
## <a name="creating-a-provisioning-template"></a>Создание шаблона подготовки

Как уже упоминалось, — это самый простой способ создания настраиваемого шаблона подготовки для создания новой нового семейства веб-сайтов в Microsoft SharePoint Online, настройка вашего артефактов (состоит выглядеть, столбцы сайта, типы содержимого, экземпляры списков, страницы, файлы, и т.д.) и Сохраните результат в качестве шаблона подготовки.

Таким образом, давайте предположим, определения сайтов пример с пользовательским выглядеть (настраиваемые цвета темы, настраиваемый логотип, настраиваемые фонового изображения). Можно просмотреть итоговый домашней страницы на следующем рисунке.

![Домашней странице шаблона сайта](./media/Introducing-the-PnP-Provisioning-Engine/Figure-1-SiteTemplate01.png)

Кроме того вы определили несколько столбцов сайта, тип контента и библиотека накладных с настраиваемым представлением. В двух следующих рисунках можно увидеть результат.

![Библиотека накладных с настраиваемого типа контента](./media/Introducing-the-PnP-Provisioning-Engine/Figure-2-SiteTemplate02.png)

![На странице Параметры библиотеки счетов](./media/Introducing-the-PnP-Provisioning-Engine/Figure-3-SiteTemplate03.png)

Чтобы экспортировать этого сайта в качестве шаблона подготовки, можно либо использовать PowerShell (благодаря усилия [Эрвин](https://twitter.com/erwinvanhunen)!) или CSOM к коду с некоторые методы расширения, которые предоставляются PnP Библиотека базовых разработчик офисных решений. 

Чтобы использовать расширения PowerShell, можно просто просмотреть правильный URL-адрес ([http://aka.ms/officedevpnpcmdlets16](http://aka.ms/officedevpnpcmdlets16) для Microsoft SharePoint Online) или [http://aka.ms/officedevpnpcmdlets15](http://aka.ms/officedevpnpcmdlets15) для Microsoft SharePoint 2013 и установка расширения PnP основных PowerShell разработчик офисных решений. После подключения среды PowerShell для Microsoft Office 365 с помощью командлета *Connect-SPOnline* , можно использовать следующий командлет PowerShell:

*Get-SPOProvisioningTemplate-выходной параметр «PnP подготовки File.xml»*

*– Выходной параметр* аргумент, то предписывает командлету о том, куда требуется сохранить шаблон подготовки.

С другой стороны, для использования расширений CSOM может просто создание любого типа (консоли Windows, SharePoint надстройки, независимо от вы хотите) проекта программного обеспечения .NET и добавьте пакет PnP NuGet разработчик офисных решений. Доступен пакет NuGet двух видов: PnP основных V15 разработчик офисных решений, который предназначен для Microsoft SharePoint 2013 в локальной, и разработчик офисных решений PnP процессор, который предназначен для Microsoft SharePoint Online.

Давайте предназначенных для Microsoft SharePoint Online, который более было протестировано и является основной целью усилия PnP основных групп. Просто необходимо подключение к Microsoft Office 365, создайте экземпляр *ClientContext* и получить ссылку на объект *Web* . Благодаря новый метод расширения с именем *GetProvisioningTemplate*вы сможете получить объект *ProvisioningTemplate* , которые могут быть сохранены с помощью шаблона поставщика и форматирования сериализации. Поставщик шаблонов и объекты форматирования данных сериализации можно настраивать, так, чтобы реализовать любые сохраняемость хранилища и сериализации форматирование вы хотите. По умолчанию PnP модуля подготовки предоставляет поддержку для поставщиков шаблон файловой системы, SharePoint и Azure хранилища больших двоичных объектов, а также для форматирования данных сериализации XML и JSON. На следующем рисунке (кредитов для [Vesa](https://twitter.com/vesajuvonen)) могут видеть контур в общей архитектуре PnP модуля подготовки.

![Архитектура PnP платформы модуля подготовки](./media/Introducing-the-PnP-Provisioning-Engine/Figure-4-PnP-Provisioning-Framework-Outline.png)

В результате извлечение и сохранение объект экземпляра *ProvisioningTemplate* будет для экземпляра XML-файла, как показано в следующем фрагменте кода XML:
    
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
    

Как вы видите, XML-элементы, названию. XML-схемы, используемые в этом примере ссылается на 201505 версию PnP подготовки схемы (пространство имен XML: *http://schemas.dev.office.com/PnP/2015/05/ProvisioningSchema*), который был определен вместе с сообществом PnP разработчик офисных решений и что можно найти на репозиториев по следующему URL-АДРЕСУ: [https://github.com/SharePoint/Pnp-Provisioning-Schema/](https://github.com/SharePoint/Pnp-Provisioning-Schema/). В одном репозитории находятся наценки (MD) автоматически созданный документ с описываются основные элементы, типы и атрибуты, доступные для вручную определить шаблон подготовки XML.

Тем не менее в реальных степень этот модуль подготовки — это доступности высокого уровня, формат сериализации, вне зависимости от модели домена. На самом деле во внутренней сети PnP модуля подготовки полностью отделены от любого типа формат сериализации и всей engine просто обрабатывает экземпляры типа *ProvisioningTemplate* . Например на следующем рисунке видно окно «Контрольное значение» Microsoft Visual Studio 2013 отображение экземпляр объекта ProvisioningTemplate.

![Структура - в рамках отслеживания отладчика - объекта ProvisioningTemplate](./media/Introducing-the-PnP-Provisioning-Engine/Figure-5-Domain-Model.png)

Вы можете определить *ProvisioningTemplate* вручную, с помощью узла бизнес-моделей, или путем создания XML-документа, которое проверяет PnP подготовки схемы XSD или путем написания кода .NET и создав иерархия объектов это. Можно даже выполнить сочетание этих подходов: проектирование подготовки шаблона, с помощью узла бизнес-моделей, сохраните его в XML-файл и выполните ряд настроек в памяти при обработке экземпляра *ProvisioningTemplate* в коде.

<a name="applyingtemplate"> </a>
## <a name="applying-a-provisioning-template"></a>Применение шаблона подготовки

Теперь, когда вы узнали, что шаблон подготовки и как извлечь домена модели объектов из существующего веб-сайтов, можно приступать к его применения к целевого сайта. Давайте предположим, что другой новым нового семейства сайтов в Microsoft SharePoint Online, которая была создана на основе шаблона сайта группы, как показано на следующем рисунке.
 
![SharePoint Online страницы для создания нового семейства веб-сайтов](./media/Introducing-the-PnP-Provisioning-Engine/Figure-6-Target-Site-Creation.png)

По умолчанию сайт будет выглядеть как на следующем рисунке, являющийся макета по умолчанию сайта SharePoint Online.

![На домашней странице новым новой цели](./media/Introducing-the-PnP-Provisioning-Engine/Figure-7-Target-Site-Created.png)

Теперь можно применить настраиваемого экземпляра объекта *ProvisioningTemplate* за счет использования PowerShell или путем написания кода .NET. Если вы хотите использовать PowerShell, в следующем фрагменте демонстрируется, как можно использовать командлет *SPOProvisioningTemplate применить* .

*Применение SPOProvisioningTemplate-Path «PnP подготовки File.xml»*

*– Путь* аргумент ссылается на файл шаблона источника командлета автоматически применяется к сайту подключенных (подразумевается командлета *Connect-SPOnline* ). На следующем рисунке видно конечный результат.

![Домашней страницы конечного сайта, основанного на подготовки шаблона](./media/Introducing-the-PnP-Provisioning-Engine/Figure-8-Target-Site-Provisioned.png)

Как вы видите, имеет внешний вид как исходного шаблона сайта, а также библиотеки счетов, все же базовую структуру и конфигурации (столбцы сайта, типов контента, и т.д.).

Как насчет с использованием кода .NET? Здесь приведен фрагмент по использованию CSOM и разработчик офисных решений PnP Библиотека базовых методов расширения для применения этого шаблона.

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
    
Чтобы начать, необходимо создать экземпляр объекта шаблона поставщика, в зависимости от того, какой тип сохраняемость, который будет использоваться для сохранения и загрузите шаблон.  Затем загрузите шаблон из репозитория исходного с помощью метода *GetTemplate* . И, наконец шаблон будет применяться для целевого сайта с помощью метода расширения *ApplyProvisioningTemplate* типа Web.

В среднем библиотеке может занять несколько минут, чтобы применить шаблон, независимо от того, является ли вы используете код PowerShell или .NET. При желании можно регистрировать делегат для наблюдения за весь процесс подготовки во время выполнения. Мы по-прежнему повышается производительность ядра и на данный момент мы шла внимание на возможностях и функциях.

<a name="advancedtopics"> </a>
## <a name="advanced-topics"></a>Дополнительные разделы

Это просто вводную статью в ближайшем будущем будет рассмотрения глубокого вокруг некоторые дополнительные разделы. Тем не менее, важно понимать, что с помощью новых PnP модуля подготовки, вы может также подготовить таксономии, а также использовать переменные и маркеры, которые можно заменить во время выполнения, в зависимости от того, что подготовки (идентификаторы список параметров, идентификаторы терминов, и т.д.). Можно вызвать модуля подготовки из служб задания таймера, размещением у поставщика надстроек, внешние сайты и др. И, наконец можно использовать PnP модуля подготовки для переноса артефактов из тестовой/промежуточной среды в производственную среду.

Кроме того на Channel 9 имеется [раздел выделенный PnP разработчик офисных решений](http://aka.ms/OfficeDevPnPVideos), где посмотреть некоторые видеоматериалы по PnP модуля подготовки и PnP расширения PowerShell:

- [Приступая к работе с PnP модуля подготовки](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine)
- [Глубокое погружение PnP схеме модуля подготовки](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
- [Общие сведения о PnP командлеты PowerShell](https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets)

<a name="wrapup"> </a>
## <a name="requirements-and-wrap-up"></a>Требования и Wrap копирования ##

Для воспроизведения с PnP модуля подготовки локальной вы должны иметь по крайней мере SharePoint 2013 марта 2015 накопительный пакет обновления установлен, как ядро использует некоторых [новых возможностей](http://blogs.msdn.com/b/vesku/archive/2015/04/10/new-sharepoint-csom-version-released-for-office-365.aspx) объектной модели со стороны клиента которых не доступны в предыдущие версии продукта. При использовании Microsoft SharePoint Online, требования автоматически удовлетворяются благодаря программное обеспечение как модель службы.

Пожалуйста Поэкспериментируйте с PnP модуля подготовки, отзыв и находят истинное наслаждение будущее модели надстройки SharePoint и удаленных подготовки!

<a name="bk_addresources"> </a>
## <a name="additional-resources"></a>Дополнительные ресурсы

-  [Шаблоны разработки Office 365 и рекомендации на репозиториев](https://github.com/SharePoint/PnP/)
-  [Группы разработчиков SharePoint](http://aka.ms/sppnp-community) в Microsoft Tech сообщества
