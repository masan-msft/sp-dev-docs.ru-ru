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
# <a name="sharepoint-solution-packaging"></a>Упаковка решения SharePoint

Задача gulp **package-solution** проверяет файл **/config/package-solution.json** на наличие различных сведений конфигурации, включая некоторые универсальные пути к файлам и определения связей между компонентами (_WebParts_ и _Applications_) в пакете.

Схема файла конфигурации выглядит так:

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

Каждый файл конфигурации пакета содержит необязательные параметры, с помощью которых можно переопределить места, в которых задача ищет исходные файлы и манифесты, а также определить место для записи пакета. Кроме того, такие файлы содержат обязательное определение решения, которое сообщает упаковщику о связях между различными компонентами.

## <a name="solution-definition-isolution"></a>Определение решения (ISolution)

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

Каждый файл решения должен содержать свойство **name**, идентифицирующее пакет в пользовательском интерфейсе SharePoint. Кроме того, каждый пакет должен содержать глобальный уникальный идентификатор (**id**), который используется в SharePoint. При необходимости вы также можете указать номер версии (**version**) в формате X.X.X.X, который используется для идентификации различных версий пакета при обновлении.

Кроме того, определение решения может включать список определений компонентов SharePoint.

> [!NOTE] 
> Если он отсутствует или пуст, задача создает по одному компоненту для каждого элемента (сопоставление 1:1).

## <a name="feature-definition-ifeature"></a>Определение компонента (IFeature)

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

Важно помнить, что это определение для создания компонента SharePoint, и некоторые из этих параметров доступны в пользовательском интерфейсе. Как и у решений, у каждого компонента есть обязательные свойства **title**, **description**, **id** и **version** (в формате X.X.X.X). Обратите внимание, что свойство **id** компонента должно быть глобальным уникальным идентификатором.

Каждый компонент также может содержать любое количество элементов, которые активируются вместе с этим компонентом. Они определяются в списке **componentIds** — глобальных уникальных идентификаторов, которые *должны* совпадать со свойством **ID** в файле манифеста элемента. Если этот список не определен или пуст, упаковщик включает в компонент *все* элементы.

## <a name="file-paths"></a>Пути к файлу

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

* **packageDir**: корневая папка пакета. Значение по умолчанию — `./sharepoint`. Все остальные пути указываются относительно этой папки.
* **debugDir**: папка для записи необработанного пакета на диск для отладки. Значение по умолчанию — `solution/debug`.
* **zippedPackage**: имя файла SPPKG, который следует создать (включая расширение). Значение по умолчанию — `ClientSolution.sppkg`.
* **featureXmlDir**: папка, содержащая XML-файл специального компонента, который следует импортировать в пакет. Значение по умолчанию — `feature_xml`.
  
  > [!IMPORTANT] 
  > Обратите внимание, что все файлы в этой папке включаются в файл SPPKG, но чтобы включить в манифест пакета специальный компонент, для него необходимо создать RELS-файл.

* **manifestsMatch**: стандартная маска для поиска файлов манифеста. Поиск выполняется в папке **dist/** в обычном режиме и в папке **deploy/** для рабочих версий.
* **manifestDir**: путь к папке, где хранятся манифесты. Значение по умолчанию — `buildConfig.distFolder`.
* **sharepointAssetDir** каталог, содержащий ресурсы SharePoint (элементы компонента, манифесты элементов и действия по обновлению), которые автоматически включаются в пакет SharePoint. Значение по умолчанию — `assets`.

## <a name="examples"></a>Примеры

### <a name="default-configuration"></a>Конфигурация по умолчанию

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

## <a name="custom-feature-xml"></a>XML-файл специального компонента

Чтобы подготовить определенные ресурсы SharePoint (шаблоны списков, страницы или типы контента), в пакет можно внедрить XML-файл специального компонента. Он используется для подготовки ресурсов, необходимых приложениям, но его также можно использовать для веб-частей. Документация по XML-файлам компонентов представлена [в этой статье](https://msdn.microsoft.com/en-us/library/office/ms475601.aspx?f=255&MSPPError=-2147217396).

По умолчанию задача упаковки ищет XML-файл специального компонента в папке **./sharepoint/feature\_xml**. Все файлы из этой папки включаются в конечный пакет приложения. Однако задача использует содержимое папки **\_rels/**, чтобы выяснить, какие специальные компоненты определены. 

В сущности, она предполагает, что каждый файл **.xml.rels** связан с одноименным файлом feature.xml на верхнем уровне папки **feature_xml/**, и добавляет связь с файлом **AppManifest.xml.rels**, включая этот компонент в пакет.

## <a name="see-also"></a>См. также

- [Обзор SharePoint Framework](../../sharepoint-framework-overview.md)