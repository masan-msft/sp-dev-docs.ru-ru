---
title: "Примечания к упаковке решений"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 10bc8317561516a03ab1c212f66f34aeb7f509ff
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="notes-on-solution-packaging"></a><span data-ttu-id="364ef-102">Примечания к упаковке решений</span><span class="sxs-lookup"><span data-stu-id="364ef-102">Notes on solution packaging</span></span>

<span data-ttu-id="364ef-103">Задача gulp **package-solution** проверяет файл **/config/package-solution.json** на наличие различных сведений конфигурации, включая некоторые универсальные пути к файлам и определения связей между компонентами (_WebParts_ и _Applications_) в пакете.</span><span class="sxs-lookup"><span data-stu-id="364ef-103">The **package-solution** gulp task looks at **/config/package-solution.json** for various configuration details, including some generic filepaths, as well as defining the relationship between components (_WebParts_ and _Applications_) in a package.</span></span>

## <a name="configuration-file"></a><span data-ttu-id="364ef-104">Файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="364ef-104">Configuration File</span></span>

<span data-ttu-id="364ef-105">Схема файла конфигурации выглядит так:</span><span class="sxs-lookup"><span data-stu-id="364ef-105">The schema for the configuration file is as follows:</span></span>

```ts
interface IPackageSolutionTaskConfig {
    paths?: {
        packageDir?: string;
        debugDir?: string;
        zippedPackage?: string;
        featureXmlDir?: string;
        manifestsMatch?: string;
        manifestDir?: string;
        sharepointAssetDir?: string;
    };
    solution?: ISolution;
}
```

<span data-ttu-id="364ef-p101">Каждый файл конфигурации пакета содержит необязательные параметры, с помощью которых можно переопределить места, в которых задача будет искать различные исходные файлы и манифесты, а также определить расположение для записи пакета. Кроме того, такие файлы содержат обязательное определение решения, которое сообщает упаковщику о связях между различными компонентами.</span><span class="sxs-lookup"><span data-stu-id="364ef-p101">Each package configuration file has some optional settings to override the places where the task will look for various source files and manifests, as well as defining the location to write the package. Additionally, it has a required solution definition, which instructs the packager on the relationships of various components.</span></span>

### <a name="solution-definition-isolution"></a><span data-ttu-id="364ef-108">Определение решения (_ISolution_)</span><span class="sxs-lookup"><span data-stu-id="364ef-108">Solution definition (_ISolution_)</span></span>

```ts
interface ISolution {
    name: string;
    id: string;
    title?: string;
    supportedLocales?: string[];
    version?: string;
    features?: IFeature[];
    iconPath?: string;
    skipFeatureDeployment?: boolean;
}
```

<span data-ttu-id="364ef-p102">Каждый файл решения должен содержать свойство **name**, идентифицирующее пакет в пользовательском интерфейсе SharePoint. Кроме того, каждый пакет должен содержать глобальный уникальный идентификатор (**id**), который используется в SharePoint. При необходимости вы также можете указать номер версии (**version**) в формате X.X.X.X, который используется для идентификации различных версий пакета при обновлении.</span><span class="sxs-lookup"><span data-stu-id="364ef-p102">Each solution file must have a **name**, which identifies the package in the SharePoint UI. Additionally, each package must contain a globally unique identifier (**id**), which is used internally by SharePoint. Optionally, you may also specify a **version** number in the format "X.X.X.X", which is used to identify various versions of the package when upgrading.</span></span>

<span data-ttu-id="364ef-112">Кроме того, определение решения может включать список определений компонентов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="364ef-112">The solution definition also optionally contains a list of SharePoint Feature definitions.</span></span>

> [!NOTE] 
> <span data-ttu-id="364ef-113">Если он отсутствует или пуст, задача создает по одному компоненту для каждого элемента (сопоставление 1:1).</span><span class="sxs-lookup"><span data-stu-id="364ef-113">Note: If this is omitted or empty, the task will create a single Feature for every component (a 1:1 mapping).</span></span>

### <a name="feature-definition-ifeature"></a><span data-ttu-id="364ef-114">Определение компонента (_IFeature_)</span><span class="sxs-lookup"><span data-stu-id="364ef-114">Feature definition (_IFeature_)</span></span>

```ts
interface IFeature {
    title: string;
    description: string;
    id: string;
    version?: string;
    componentIds?: string[];
    components: IComponent[];
    assets: ISharepointAssets<string>;
}
```

<span data-ttu-id="364ef-p103">Важно помнить, что это определение для создания компонента SharePoint, и некоторые из этих параметров будут отображаться в пользовательском интерфейсе. Как и у решений, у каждого компонента есть обязательные свойства **title**, **description**, **id** и **version** (в формате X.X.X.X). Обратите внимание, что свойство **id** компонента должно быть глобальным уникальным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="364ef-p103">It's important to note that this is a definition for creating a SharePoint Feature, and that some of these options will be exposed in the UI. Similarly to the solution, each Feature has a mandatory **title**, **description**, **id**, and **version** number (in the X.X.X.X format). Please note that the Feature **id** should also be a globally unique identifier.</span></span>

<span data-ttu-id="364ef-p104">Каждый компонент также может содержать любое количество элементов, которые будут активироваться вместе с этим компонентом. Они определяются в списке **componentIds** — глобальных уникальных идентификаторов, которые **ДОЛЖНЫ** совпадать со свойством **ID** в файле манифеста элемента. Если этот список не определен или пуст, упаковщик включит в компонент **все** элементы.</span><span class="sxs-lookup"><span data-stu-id="364ef-p104">Each feature can also contain any number of components, which will be activated when the feature is activated. This is defined via a list of **componentIds**, which are globally unique identifiers that **MUST** match the **ID** in the component's Manifest file. If this list is undefined or empty the packager will include **every** component in the feature.</span></span>

### <a name="file-paths"></a><span data-ttu-id="364ef-121">Пути к файлу</span><span class="sxs-lookup"><span data-stu-id="364ef-121">File paths</span></span>

```ts
interface IPackageSolutionTaskConfig {
    paths?: {
        packageDir?: string;
        debugDir?: string;
        zippedPackage?: string;
        featureXmlDir?: string;
        manifestsMatch?: string;
        manifestDir?: string;
        sharepointAssetDir?: string;
    };
    solution?: ISolution;
}
```

* <span data-ttu-id="364ef-p105">**packageDir** — упаковка корневой папки. Значение по умолчанию "./sharepoint". Все остальные пути относятся к этой папке.</span><span class="sxs-lookup"><span data-stu-id="364ef-p105">**packageDir**: packaging root folder. Defaults to './sharepoint'. All other paths are relative to this folder</span></span>
* <span data-ttu-id="364ef-p106">**debugDir** — папка для записи необработанного пакета на диск для отладки. Значение по умолчанию "solution/debug".</span><span class="sxs-lookup"><span data-stu-id="364ef-p106">**debugDir**: folder to write the raw package to disk for debugging. Defaults to 'solution/debug'</span></span>
* <span data-ttu-id="364ef-127">**zippedPackage** — имя файла sppkg для создания (включая расширение). Значение по умолчанию "ClientSolution.sppkg".</span><span class="sxs-lookup"><span data-stu-id="364ef-127">**zippedPackage**: name of the sppkg file to create (including extension) Defaults to 'ClientSolution.sppkg'</span></span>
* <span data-ttu-id="364ef-p107">**featureXmlDir** — папка, содержащая настраиваемый компонент XML для импорта в пакет. Значение по умолчанию "feature_xml".</span><span class="sxs-lookup"><span data-stu-id="364ef-p107">**featureXmlDir**: folder containing the custom feature xml to import into the package. Defaults to 'feature_xml'.</span></span>
  > <span data-ttu-id="364ef-130">**Важно.** Обратите внимание, что все файлы в этой папке будут включены в SPPKG; тем не менее, необходимо создать RELS-файл для вашего настраиваемого компонента, который будет включаться в манифест пакета.</span><span class="sxs-lookup"><span data-stu-id="364ef-130">**Important:** Note that all files in this folder will be included in the SPPKG, however, you must create a .rels file for your custom feature for it to be included in the package manifest.</span></span>
* <span data-ttu-id="364ef-p108">**manifestsMatch** — glob для поиска файлов манифеста. Выполняет поиск в папке **dist/** в обычном режиме, а в рабочем режиме — в папке **deploy/**.</span><span class="sxs-lookup"><span data-stu-id="364ef-p108">**manifestsMatch**: glob to match against to find manifest files. Looks in **dist/** when running in normal, but **deploy/** for production.</span></span>
* <span data-ttu-id="364ef-p109">**manifestDir** — путь к папке, где хранятся манифесты. Значение по умолчанию "buildConfig.distFolder".</span><span class="sxs-lookup"><span data-stu-id="364ef-p109">**manifestDir**: path to the folder where manifests are stored. Defaults to 'buildConfig.distFolder'</span></span>
* <span data-ttu-id="364ef-p110">**sharepointAssetDir** каталог, содержащий ресурсы SharePoint (такие как элементы компонента, манифесты элементов и действия по обновлению), которые будут автоматически включены в пакет SharePoint. Значение по умолчанию "assets".</span><span class="sxs-lookup"><span data-stu-id="364ef-p110">**sharepointAssetDir**: directory containing SharePoint assets (such as feature elements, element manifests, and upgrade actions), which will be automatically included in the SharePoint package. Defaults to 'assets'.</span></span>

### <a name="examples"></a><span data-ttu-id="364ef-137">Примеры</span><span class="sxs-lookup"><span data-stu-id="364ef-137">Examples</span></span>

#### <a name="default-configuration"></a><span data-ttu-id="364ef-138">Конфигурация по умолчанию</span><span class="sxs-lookup"><span data-stu-id="364ef-138">Default Configuration</span></span>

```json
{
  "solution": {
    "name": "spfx-hello-world-client-side-solution",
    "id": "77fd2eed-55b0-42bf-8b4d-f66730cb0c34",
    "version": "1.0.0.0"
  },
  "paths": {
    "zippedPackage": "solution/spfx-hello-world.sppkg"
  }
}
```

### <a name="custom-featurexml"></a><span data-ttu-id="364ef-139">Пользовательский файл Feature.xml</span><span class="sxs-lookup"><span data-stu-id="364ef-139">Custom Feature.xml</span></span>

<span data-ttu-id="364ef-p111">Чтобы обеспечить поддержку подготовки различных ресурсов SharePoint (например, шаблонов списков, страниц или типов контента), в пакет можно внедрить пользовательский XML-файл компонента. Он используется для подготовки ресурсов, необходимых приложениям, но его также можно использовать для веб-частей. Документация по XML-файлам компонентов представлена [в этой статье](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="364ef-p111">In order support provisioning of various SharePoint resources (such as List Templates, Pages, or Content Types), custom Feature XML may also be injected into the package. This is used in order to provision resources necessary for applications, but may also be used for WebParts. The documentation for Feature XML is located [here](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).</span></span>

<span data-ttu-id="364ef-p112">По умолчанию задача упаковки ищет пользовательский XML-файл компонента в папке **./sharepoint/feature_xml**. Каждый файл из этой папки будет включен в окончательный пакет приложения. Однако задача использует содержимое папки **_rels/**, чтобы выяснить, какие пользовательские компоненты определены. В сущности, она предполагает, что каждый файл **.xml.rels** связан с одноименным файлом feature.xml на верхнем уровне папки **feature_xml/**, и добавляет связь с файлом **AppManifest.xml.rels**, включая этот компонент в пакет.</span><span class="sxs-lookup"><span data-stu-id="364ef-p112">By default, the packaging task looks for the custom Feature XML in **./sharepoint/feature_xml**. Every file in this folder will be included in the final application package. However, the task relies on the contents of the  **_rels/** folder to determine which custom features are defined. Essentially, it assumes that each **.xml.rels** file is related to a feature.xml of the same name at the top level of the **feature_xml/**, and will add a relationship to the **AppManifest.xml.rels** file including that Feature in the package.</span></span>