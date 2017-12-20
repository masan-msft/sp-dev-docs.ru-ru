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
# <a name="notes-on-solution-packaging"></a>Примечания к упаковке решений

Задача gulp **package-solution** проверяет файл **/config/package-solution.json** на наличие различных сведений конфигурации, включая некоторые универсальные пути к файлам и определения связей между компонентами (_WebParts_ и _Applications_) в пакете.

## <a name="configuration-file"></a>Файл конфигурации

Схема файла конфигурации выглядит так:

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

Каждый файл конфигурации пакета содержит необязательные параметры, с помощью которых можно переопределить места, в которых задача будет искать различные исходные файлы и манифесты, а также определить расположение для записи пакета. Кроме того, такие файлы содержат обязательное определение решения, которое сообщает упаковщику о связях между различными компонентами.

### <a name="solution-definition-isolution"></a>Определение решения (_ISolution_)

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

Каждый файл решения должен содержать свойство **name**, идентифицирующее пакет в пользовательском интерфейсе SharePoint. Кроме того, каждый пакет должен содержать глобальный уникальный идентификатор (**id**), который используется в SharePoint. При необходимости вы также можете указать номер версии (**version**) в формате X.X.X.X, который используется для идентификации различных версий пакета при обновлении.

Кроме того, определение решения может включать список определений компонентов SharePoint.

> [!NOTE] 
> Если он отсутствует или пуст, задача создает по одному компоненту для каждого элемента (сопоставление 1:1).

### <a name="feature-definition-ifeature"></a>Определение компонента (_IFeature_)

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

Важно помнить, что это определение для создания компонента SharePoint, и некоторые из этих параметров будут отображаться в пользовательском интерфейсе. Как и у решений, у каждого компонента есть обязательные свойства **title**, **description**, **id** и **version** (в формате X.X.X.X). Обратите внимание, что свойство **id** компонента должно быть глобальным уникальным идентификатором.

Каждый компонент также может содержать любое количество элементов, которые будут активироваться вместе с этим компонентом. Они определяются в списке **componentIds** — глобальных уникальных идентификаторов, которые **ДОЛЖНЫ** совпадать со свойством **ID** в файле манифеста элемента. Если этот список не определен или пуст, упаковщик включит в компонент **все** элементы.

### <a name="file-paths"></a>Пути к файлу

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

* **packageDir** — упаковка корневой папки. Значение по умолчанию "./sharepoint". Все остальные пути относятся к этой папке.
* **debugDir** — папка для записи необработанного пакета на диск для отладки. Значение по умолчанию "solution/debug".
* **zippedPackage** — имя файла sppkg для создания (включая расширение). Значение по умолчанию "ClientSolution.sppkg".
* **featureXmlDir** — папка, содержащая настраиваемый компонент XML для импорта в пакет. Значение по умолчанию "feature_xml".
  > **Важно.** Обратите внимание, что все файлы в этой папке будут включены в SPPKG; тем не менее, необходимо создать RELS-файл для вашего настраиваемого компонента, который будет включаться в манифест пакета.
* **manifestsMatch** — glob для поиска файлов манифеста. Выполняет поиск в папке **dist/** в обычном режиме, а в рабочем режиме — в папке **deploy/**.
* **manifestDir** — путь к папке, где хранятся манифесты. Значение по умолчанию "buildConfig.distFolder".
* **sharepointAssetDir** каталог, содержащий ресурсы SharePoint (такие как элементы компонента, манифесты элементов и действия по обновлению), которые будут автоматически включены в пакет SharePoint. Значение по умолчанию "assets".

### <a name="examples"></a>Примеры

#### <a name="default-configuration"></a>Конфигурация по умолчанию

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

### <a name="custom-featurexml"></a>Пользовательский файл Feature.xml

Чтобы обеспечить поддержку подготовки различных ресурсов SharePoint (например, шаблонов списков, страниц или типов контента), в пакет можно внедрить пользовательский XML-файл компонента. Он используется для подготовки ресурсов, необходимых приложениям, но его также можно использовать для веб-частей. Документация по XML-файлам компонентов представлена [в этой статье](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).

По умолчанию задача упаковки ищет пользовательский XML-файл компонента в папке **./sharepoint/feature_xml**. Каждый файл из этой папки будет включен в окончательный пакет приложения. Однако задача использует содержимое папки **_rels/**, чтобы выяснить, какие пользовательские компоненты определены. В сущности, она предполагает, что каждый файл **.xml.rels** связан с одноименным файлом feature.xml на верхнем уровне папки **feature_xml/**, и добавляет связь с файлом **AppManifest.xml.rels**, включая этот компонент в пакет.