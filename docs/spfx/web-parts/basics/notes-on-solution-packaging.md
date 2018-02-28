---
title: "Упаковка решения SharePoint"
description: "Задача gulp package-solution ищет сведения о конфигурации SharePoint Framework, в том числе определения ISolution и IFeature, в файле /config/package-solution.json."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: ced627fb96373acb21c2d83f91b82c4db28d2f3d
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="sharepoint-solution-packaging"></a><span data-ttu-id="0cf5a-103">Упаковка решения SharePoint</span><span class="sxs-lookup"><span data-stu-id="0cf5a-103">SharePoint solution packaging</span></span>

<span data-ttu-id="0cf5a-104">Задача gulp **package-solution** проверяет файл **/config/package-solution.json** на наличие различных сведений конфигурации, включая некоторые универсальные пути к файлам и определения связей между компонентами (_WebParts_ и _Applications_) в пакете.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-104">The **package-solution** gulp task looks at **/config/package-solution.json** for various configuration details, including some generic filepaths, as well as defining the relationship between components (_WebParts_ and _Applications_) in a package.</span></span>

<span data-ttu-id="0cf5a-105">Схема файла конфигурации выглядит так:</span><span class="sxs-lookup"><span data-stu-id="0cf5a-105">The schema for the configuration file is as follows:</span></span>

```typescript
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

<span data-ttu-id="0cf5a-p101">Каждый файл конфигурации пакета содержит необязательные параметры, с помощью которых можно переопределить места, в которых задача ищет исходные файлы и манифесты, а также определить место для записи пакета. Кроме того, такие файлы содержат обязательное определение решения, которое сообщает упаковщику о связях между различными компонентами.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-p101">Each package configuration file has some optional settings to override the places where the task will look for various source files and manifests, as well as defining the location to write the package. Additionally, it has a required solution definition, which instructs the packager on the relationships of various components.</span></span>

## <a name="solution-definition-isolution"></a><span data-ttu-id="0cf5a-108">Определение решения (ISolution)</span><span class="sxs-lookup"><span data-stu-id="0cf5a-108">Solution definition (ISolution)</span></span>

```typescript
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

<span data-ttu-id="0cf5a-p102">Каждый файл решения должен содержать свойство **name**, идентифицирующее пакет в пользовательском интерфейсе SharePoint. Кроме того, каждый пакет должен содержать глобальный уникальный идентификатор (**id**), который используется в SharePoint. При необходимости вы также можете указать номер версии (**version**) в формате X.X.X.X, который используется для идентификации различных версий пакета при обновлении.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-p102">Each solution file must have a **name**, which identifies the package in the SharePoint UI. Additionally, each package must contain a globally unique identifier (**id**), which is used internally by SharePoint. Optionally, you may also specify a **version** number in the format "X.X.X.X", which is used to identify various versions of the package when upgrading.</span></span>

<span data-ttu-id="0cf5a-112">Кроме того, определение решения может включать список определений компонентов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-112">The solution definition also optionally contains a list of SharePoint Feature definitions.</span></span>

> [!NOTE] 
> <span data-ttu-id="0cf5a-113">Если он отсутствует или пуст, задача создает по одному компоненту для каждого элемента (сопоставление 1:1).</span><span class="sxs-lookup"><span data-stu-id="0cf5a-113">If this is omitted or empty, the task will create a single Feature for every component (a 1:1 mapping).</span></span>

## <a name="feature-definition-ifeature"></a><span data-ttu-id="0cf5a-114">Определение компонента (IFeature)</span><span class="sxs-lookup"><span data-stu-id="0cf5a-114">Feature definition (IFeature)</span></span>

```typescript
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

<span data-ttu-id="0cf5a-p103">Важно помнить, что это определение для создания компонента SharePoint, и некоторые из этих параметров доступны в пользовательском интерфейсе. Как и у решений, у каждого компонента есть обязательные свойства **title**, **description**, **id** и **version** (в формате X.X.X.X). Обратите внимание, что свойство **id** компонента должно быть глобальным уникальным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-p103">It's important to note that this is a definition for creating a SharePoint Feature, and that some of these options will be exposed in the UI. Similarly to the solution, each Feature has a mandatory **title**, **description**, **id**, and **version** number (in the X.X.X.X format). Please note that the Feature **id** should also be a globally unique identifier.</span></span>

<span data-ttu-id="0cf5a-p104">Каждый компонент также может содержать любое количество элементов, которые активируются вместе с этим компонентом. Они определяются в списке **componentIds** — глобальных уникальных идентификаторов, которые *должны* совпадать со свойством **ID** в файле манифеста элемента. Если этот список не определен или пуст, упаковщик включает в компонент *все* элементы.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-p104">Each feature can also contain any number of components, which will be activated when the feature is activated. This is defined via a list of **componentIds**, which are globally unique identifiers that *MUST* match the **ID** in the component's Manifest file. If this list is undefined or empty the packager will include *every* component in the feature.</span></span>

## <a name="file-paths"></a><span data-ttu-id="0cf5a-121">Пути к файлу</span><span class="sxs-lookup"><span data-stu-id="0cf5a-121">File paths</span></span>

```typescript
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

* <span data-ttu-id="0cf5a-p105">**packageDir**: корневая папка пакета. Значение по умолчанию — `./sharepoint`. Все остальные пути указываются относительно этой папки.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-p105">packageDir: packaging root folder. Defaults to './sharepoint'. All other paths are relative to this folder</span></span>
* <span data-ttu-id="0cf5a-p106">**debugDir**: папка для записи необработанного пакета на диск для отладки. Значение по умолчанию — `solution/debug`.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-p106">debugDir: folder to write the raw package to disk for debugging. Defaults to 'solution/debug'</span></span>
* <span data-ttu-id="0cf5a-127">**zippedPackage**: имя файла SPPKG, который следует создать (включая расширение).</span><span class="sxs-lookup"><span data-stu-id="0cf5a-127">**zippedPackage**: name of the sppkg file to create (including extension) Defaults to 'ClientSolution.sppkg'</span></span> <span data-ttu-id="0cf5a-128">Значение по умолчанию — `ClientSolution.sppkg`.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-128">Defaults to `ClientSolution.sppkg`</span></span>
* <span data-ttu-id="0cf5a-129">**featureXmlDir**: папка, содержащая XML-файл специального компонента, который следует импортировать в пакет.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-129">**featureXmlDir**: folder containing the custom feature xml to import into the package. Defaults to 'feature_xml'.</span></span> <span data-ttu-id="0cf5a-130">Значение по умолчанию — `feature_xml`.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-130">Defaults to `feature_xml`</span></span>
  
  > [!IMPORTANT] 
  > <span data-ttu-id="0cf5a-131">Обратите внимание, что все файлы в этой папке включаются в файл SPPKG, но чтобы включить в манифест пакета специальный компонент, для него необходимо создать RELS-файл.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-131">Important: Note that all files in this folder will be included in the SPPKG, however, you must create a .rels file for your custom feature for it to be included in the package manifest.</span></span>

* <span data-ttu-id="0cf5a-132">**manifestsMatch**: стандартная маска для поиска файлов манифеста.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-132">**manifestsMatch**: Glob to match against to find manifest files.</span></span> <span data-ttu-id="0cf5a-133">Поиск выполняется в папке **dist/** в обычном режиме и в папке **deploy/** для рабочих версий.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-133">manifestsMatch: glob to match against to find manifest files. Looks in dist/ when running in normal, but deploy/ for production.</span></span>
* <span data-ttu-id="0cf5a-134">**manifestDir**: путь к папке, где хранятся манифесты.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-134">**manifestDir**: path to the folder where manifests are stored. Defaults to 'buildConfig.distFolder'</span></span> <span data-ttu-id="0cf5a-135">Значение по умолчанию — `buildConfig.distFolder`.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-135">Defaults to `buildConfig.distFolder`</span></span>
* <span data-ttu-id="0cf5a-136">**sharepointAssetDir** каталог, содержащий ресурсы SharePoint (элементы компонента, манифесты элементов и действия по обновлению), которые автоматически включаются в пакет SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-136">**sharepointAssetDir**: directory containing SharePoint assets (such as feature elements, element manifests, and upgrade actions), which will be automatically included in the SharePoint package. Defaults to 'assets'.</span></span> <span data-ttu-id="0cf5a-137">Значение по умолчанию — `assets`.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-137">Defaults to `assets`</span></span>

## <a name="examples"></a><span data-ttu-id="0cf5a-138">Примеры</span><span class="sxs-lookup"><span data-stu-id="0cf5a-138">Examples</span></span>

### <a name="default-configuration"></a><span data-ttu-id="0cf5a-139">Конфигурация по умолчанию</span><span class="sxs-lookup"><span data-stu-id="0cf5a-139">Default Configuration</span></span>

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

## <a name="custom-feature-xml"></a><span data-ttu-id="0cf5a-140">XML-файл специального компонента</span><span class="sxs-lookup"><span data-stu-id="0cf5a-140">Custom feature XML</span></span>

<span data-ttu-id="0cf5a-141">Чтобы подготовить определенные ресурсы SharePoint (шаблоны списков, страницы или типы контента), в пакет можно внедрить XML-файл специального компонента.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-141">To support provisioning of various SharePoint resources (such as List Templates, Pages, or Content Types), custom feature XML may also be injected into the package.</span></span> <span data-ttu-id="0cf5a-142">Он используется для подготовки ресурсов, необходимых приложениям, но его также можно использовать для веб-частей.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-142">This is used to provision resources necessary for applications, but may also be used for web parts.</span></span> <span data-ttu-id="0cf5a-143">Документация по XML-файлам компонентов представлена [в этой статье](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="0cf5a-143">The documentation for Feature XML is located at [Feature.xml Files](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).</span></span>

<span data-ttu-id="0cf5a-144">По умолчанию задача упаковки ищет XML-файл специального компонента в папке **./sharepoint/feature\_xml**.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-144">By default, the packaging task looks for the custom feature XML in **./sharepoint/feature\_xml**.</span></span> <span data-ttu-id="0cf5a-145">Все файлы из этой папки включаются в конечный пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-145">Every file in this folder is included in the final application package.</span></span> <span data-ttu-id="0cf5a-146">Однако задача использует содержимое папки **\_rels/**, чтобы выяснить, какие специальные компоненты определены.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-146">However, the task relies on the contents of the **\_rels/** folder to determine which custom features are defined.</span></span> 

<span data-ttu-id="0cf5a-147">В сущности, она предполагает, что каждый файл **.xml.rels** связан с одноименным файлом feature.xml на верхнем уровне папки **feature_xml/**, и добавляет связь с файлом **AppManifest.xml.rels**, включая этот компонент в пакет.</span><span class="sxs-lookup"><span data-stu-id="0cf5a-147">Essentially, it assumes that each **.xml.rels** file is related to a feature.xml of the same name at the top level of the **feature_xml/**, and adds a relationship to the **AppManifest.xml.rels** file that includes that feature in the package.</span></span>

## <a name="see-also"></a><span data-ttu-id="0cf5a-148">См. также</span><span class="sxs-lookup"><span data-stu-id="0cf5a-148">See also</span></span>

- [<span data-ttu-id="0cf5a-149">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="0cf5a-149">SharePoint Framework Overview</span></span>](../../sharepoint-framework-overview.md)