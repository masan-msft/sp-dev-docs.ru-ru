# <a name="provision-sharepoint-assets-with-your-solution-package"></a>Подготовка ресурсов SharePoint с пакетом решения

Иногда требуется подготовить к работе список или библиотеку документов SharePoint вместе с клиентским пакетом решения, чтобы сделать их доступными клиентским решениям, таким как веб-части. Цепочка инструментов SharePoint Framework позволяет упаковывать и развертывать элементы SharePoint с клиентским пакетом решения. Затем эти элементы подготавливаются к работе при установке клиентского решения на сайте. 

Подробнее о возможностях подготовки ресурсов можно узнать из веб-трансляции на [YouTube-канале SharePoint PnP](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS). 

<a href="https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS">
<img src="../../../images/spfx-webcast-youtube-provision-feature-elements.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>


## <a name="provisioning-items-using-javascript-code"></a>Подготовка элементов с помощью кода JavaScript

Хотя можно создавать элементы SharePoint в решении (например, веб-части) с помощью кода JavaScript, эта возможность ограничена контекстом текущего пользователя решения. Если у пользователя нет разрешений для создания или изменения элементов SharePoint, код JavaScript не подготовит эти элементы к работе. В таких случаях, если требуется подготовить элементы SharePoint в контексте c повышенными привилегиями, вам потребуется упаковать и развернуть элементы с пакетом решения.

## <a name="create-and-provision-sharepoint-items-in-your-solution"></a>Создание и подготовка элементов SharePoint в решении

### <a name="sharepoint-items"></a>Элементы SharePoint

С клиентским пакетом решения можно подготовить к работе такие ресурсы SharePoint:

* поля;
* типы контента;
* экземпляры списков;
* экземпляры списков с настраиваемой схемой.

#### <a name="fields"></a>Поля

Поле (столбец сайта) представляет атрибут, или фрагмент метаданных, который пользователь применяет в управлении списком или типом контента, к которому добавил этот столбец. Это определение столбца, или шаблон, которое вы можете назначить нескольким спискам для нескольких сайтов SharePoint. Столбцы сайтов избавляют от лишней работы и помогают обеспечить согласованность метаданных на сайтах и в списках. 

Допустим, вы определили столбец сайта под названием "Клиент". Пользователи могут добавлять этот столбец к своим спискам и ссылаться на него в своих типах контента. Это гарантирует, что у столбца всегда будут одни и те же атрибуты (хотя бы вначале), где бы он ни находился.

Определяя новое поле в своем решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент поля (Field)](https://msdn.microsoft.com/ru-ru/library/aa979575(v=office.15).aspx). 

Ниже приведен пример нового поля DateTime.

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
#### <a name="content-types"></a>Типы контента

Тип контента — это многоразовая коллекция метаданных (столбцов), настроек поведения и других настроек для категории элементов в списке SharePoint или документов в библиотеке документов SharePoint. Типы контента позволяют централизованно управлять настройками для категории сведений.

Например, представьте себе бизнес-ситуацию, в которой есть три типа документов: отчеты о расхода, заказы на покупку и счета. У всех трех типов документов есть ряд общих характеристик, с одной стороны, все они являются финансовыми документами и содержат данные с денежными суммами. Но у каждого типа документов есть свои требования к данным, свой шаблон документов и свой рабочий процесс. Одним из решений этой бизнес-проблемы является создание четырех типов контента. Первый тип контента, "Финансовый документ", может инкапсулировать требования к данным, общие для всех финансовых документов в организации. Оставшиеся три, "Отчет о расходах", "Заказ на покупку" и "Счет", могут наследовать общие элементы от типа "Финансовый документ", а также определять характеристики, уникальные для каждого типа, такие как конкретный набор метаданных, шаблон документа, используемый при создании нового элемента, и конкретный рабочий процесс для обработки элемента.

Определяя новый тип контента в решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент типа контента (ContentType)](https://msdn.microsoft.com/ru-ru/library/aa544268.aspx). 

Ниже приведен пример типа контента.

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

#### <a name="lists-instances"></a>Экземпляры списков

Списки — это ключевая, базовая функция сайта SharePoint. Они помогают группам собирать и отслеживать информацию, а также делиться ею. Многие приложения используют списки, созданные на сайте, чтобы хранить данные для реализации своего поведения. Экземпляр списка — это предопределенный список SharePoint с известным идентификатором. Вы можете настраивать и добавлять элементы в этих списках, создавать дополнительные списки с помощью доступных шаблонов, а также создавать специальные списки, указывая только нужные параметры и столбцы.

В SharePoint доступны несколько шаблонов списков (например, для календаря, списка контактов или задач). С помощью этих шаблонов вы можете создавать экземпляры списков для своих веб-частей и других решений. Например, вы можете определить экземпляр списка "Финансовые документы" на основе шаблона "Библиотека документов", чтобы обеспечить хранение соответствующих документов для веб-части. 

Определяя новый экземпляр списка в решении, вы можете сверяться со схемой и атрибутами из статьи [Элемент экземпляра списка (ListInstance)](https://msdn.microsoft.com/ru-ru/library/office/ms476062.aspx).

Ниже приведен пример определения экземпляра списка.

```xml
<ListInstance 
    FeatureId="00bfea71-e717-4e80-aa17-d0c71b360101"
    Title="Finance Records" 
    Description="Finance documents"
    TemplateType="101"
    Url="Lists/FinanceRecords">
</ListInstance>
```

#### <a name="lists-instances-with-custom-schema"></a>Экземпляры списков с настраиваемой схемой

Вы можете определять поля, типы контента и представления, используемые в экземпляре списка, применяя определение настраиваемой схемы списков. Используйте атрибут `customschema` [элемента экземпляра списка](https://msdn.microsoft.com/ru-ru/library/office/ms476062.aspx#sectionSection0), чтобы ссылаться на настраиваемую схему экземпляра списка. 

Например, вы можете определить экземпляр списка "Финансовые документы" с типом контента "Финансовый документ", который может инкапсулировать требования к данным, общие для всех финансовых документов в организации. 

Ниже приведен пример определения экземпляра списка, для которого используется настраиваемая схема.

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
А так выглядит определение настраиваемой схемы, которое задает тип контента для определенного выше экземпляра списка:

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
### <a name="create-sharepoint-items-in-your-solution"></a>Создание элементов SharePoint в решении

Пакет решения использует [компоненты SharePoint](https://msdn.microsoft.com/ru-ru/library/ee537350(office.14).aspx) для упаковки элементов SharePoint и подготовки последних к работе. Компонент — это контейнер, включающий один или несколько подготавливаемых элементов SharePoint. Компонент содержит файл Feature.xml и один или несколько файлов манифеста элементов. Эти XML-файлы также называют определениями компонентов. 

Как правило, клиентский пакет решения содержит один компонент. Этот компонент активируется при установке решения на сайте. Важно отметить, что администраторы сайтов устанавливают пакет решения, а не компонент. 

Компонент, как правило, создается с помощью указанных ниже XML-файлов.

**Файл манифеста элемента**

Файл манифеста элемента содержит определения элементов SharePoint и выполняется при активации компонента. Например: XML-определения для создания экземпляров списка, поля или типа контента находятся в манифесте элемента. 

Ниже приведен пример файла манифеста элемента, в котором определяется новое поле DateTime.

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

**Файл элемента**

Любой поддерживаемый файл, сопровождающий манифест элемента, — это файл элемента. Например, схема экземпляра списка — это манифест элемента, связанный с экземпляром списка, определенным в манифесте элемента. 

Ниже приведен пример настраиваемой схемы экземпляра списка.

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

**Файл с действиями по обновлению**

Как понятно из названия, этот файл указывает действия, выполняемые при обновлении решения на сайте. Такое действие может предусматривать включение одного или нескольких манифестов элемента. Например: Если для обновления требуется добавить новое поле, то определение этого поля будет доступно в виде манифеста элемента и добавлено в файл с действиями по обновлению. 

Ниже приведен пример файла с действиями по обновлению, который применяет файл манифеста элемента во время обновления.

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

#### <a name="configure-the-sharepoint-feature"></a>Настройка компонента SharePoint 

Чтобы включить XML-файлы, необходимо сначала определить конфигурацию компонента в файле конфигурации *package-solution.json*, находящемся в папке *config* проекта. Файл *package-solution.json* содержит ключевые метаданные для клиентского пакета решения, и на него можно ссылаться при выполнении задачи gulp `package-solution`, которая упаковывает решение в файл `.sppkg`. 

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
Объект JSON `features` содержит метаданные для компонента.

Свойство | Описание 
-----|------
id|Уникальный идентификатор (GUID) компонента
title|Название компонента
description| Описание компонента
assets|Массив XML-файлов, используемых в компоненте
elementManifests|Определяется в свойстве `assets`, массив файлов манифеста элемента
elementFiles|Определяется в свойстве `assets`, массив файлов элемента
upgradeActions|Определяется в свойстве `assets`, массив файлов с действиями по обновлению

#### <a name="create-the-feature-xml-files"></a>Создание XML-файлов компонента

Цепочка инструментов ищет XML-файлы, как определено в конфигурации в специальной папке проекта клиентского решения — *sharepoint\assets*. 

![XML-файлы компонента в проекте клиентского решения](../../images/feature-provision-project-items.png)

Конфигурация, определенная в файле `package-solution.json`, сопоставляет XML-файлы с соответствующим XML-файлом компонента при выполнении задачи gulp `package-solution`.

#### <a name="package-sharepoint-items"></a>Упаковка элементов SharePoint 

Определив компонент в файле `package-solution.json` и создав соответствующие XML-файлы компонента, вы можете упаковать элементы SharePoint вместе с пакетом `.sppkg` с помощью указанной ниже задачи gulp.

```js
gulp package-solution
```

Приведенная выше команда упакует один или несколько манифестов клиентских решений, таких как веб-части, вместе с XML-файлами компонента, на которые ссылается файл конфигурации `package-solution.json`.

>**ПРИМЕЧАНИЕ.** Вы можете использовать флаг `--ship`, чтобы упаковать минимальные версии решений. 

#### <a name="upgrade-sharepoint-items"></a>Обновление элементов SharePoint

Вы можете добавлять новые элементы SharePoint или обновлять имеющиеся при обновлении клиентского решения. Для подготовки элементов SharePoint используются компоненты, поэтому определите список действий по обновлению с помощью XML-файла [действий по обновлению компонента](https://msdn.microsoft.com/ru-ru/library/office/ee537575(v=office.14).aspx).

Массив объектов JSON `upgradeActions` в файле `package-solution.json` ссылается на XML-файлы компонента, связанные с действиями по обновлению для компонента. В файле с действиями по обновлению определяется по крайней мере XML-файл манифеста элемента, который будет выполняться при обновлении компонента. 

При обновлении решения SharePoint Framework необходимо также обновить атрибуты версии как для решения, так и для компонента, где были включены действия по обновлению. Увеличение версии решения будет обозначать для SharePoint и конечных пользователей, что доступна новая версия пакета. Увеличение версии компонента обеспечит обработку задач, указанных в действиях по обновлению, в рамках обновления решения. 

Ниже приведен пример файла с действиями по обновлению, который применяет файл манифеста элемента во время обновления.

```xml
<ApplyElementManifests>
      <ElementManifest Location="9c0be970-a4d7-41bb-be21-4a683586db18\elements-v2.xml" />
</ApplyElementManifests>
```

Соответствующий файл `element-v2.xml`, в котором определяется новое поле валюты, подготавливаемое при обновлении:

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

Действия по обновлению в клиентских решениях поддерживают следующие дочерние элементы:


**AddContentTypeField**

Добавляет новое поле к имеющемуся подготовленному типу контента. Распространяет изменения, внесенные в тип контента сайта, для всех дочерних списков и типов контента на этом сайте. Например:

```xml
<AddContentTypeField 
     ContentTypeId="0x010100A6F9CE1AFE2A48f0A3E6CB5BB770B0F7" 
     FieldId="{B250DCFD-9310-4e2d-85F2-BE2DA37A57D2}" 
     PushDown="TRUE" />
```

**ApplyElementManifests**

Добавляет новый элемент к имеющемуся компоненту. При обновлении компонента подготавливаются все недекларативные элементы, на которые ссылаются указанные манифесты элементов.

**VersionRange**

Задает диапазон версий, к которым применяются указанные действия по обновлению.

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Веб-трансляция SharePoint PnP: подготовка ресурсов SharePoint для решения SPFx](https://www.youtube.com/watch?v=r-UdJhhHlEQ&list=PLR9nK3mnD-OUnJytlXlO84fQnYt50iTmS)
    
-  [Руководство: подготовка ресурсов SharePoint из клиентской веб-части SharePoint](https://dev.office.com/sharepoint/docs/spfx/web-parts/get-started/provision-sp-assets-from-package)

-  
  [Стандартный блок SharePoint: компоненты](https://msdn.microsoft.com/ru-ru/library/ee537350.aspx)

-  [Компонент Framework: использование элемента UpgradeActions](https://msdn.microsoft.com/ru-ru/library/office/ee537575.aspx)

-  [Компонент Framework: элемент Field](https://msdn.microsoft.com/ru-ru/library/aa979575.aspx)

-  [Компонент Framework: элемент ContentType](https://msdn.microsoft.com/ru-ru/library/aa544268.aspx).aspx)

-  [Компонент Framework: элемент ListInstance](https://msdn.microsoft.com/ru-ru/library/office/ms476062.aspx)
