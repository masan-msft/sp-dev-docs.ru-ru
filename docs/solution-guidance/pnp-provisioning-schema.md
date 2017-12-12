---
title: "PnP подготовки схемы"
ms.date: 11/03/2017
ms.openlocfilehash: e2bb1c364aca836bb6f38b487c88d1e4eeb879c8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="pnp-provisioning-schema"></a>PnP подготовки схемы

Как было рассмотрено в нашем [PnP подготовки framework](pnp-provisioning-framework.md) и в другом месте, формат для подготовки шаблонов была отделена от формате сохранения, можно использовать любой формат, который вы предпочитаете. Тем не менее так как с помощью подготовки схемы XML для сохранения шаблонов распространенного сценария, мы предлагаем некоторые дополнительные сведения об использовании схемы XML для сериализации и сохраните подготовки шаблонов.

**Важные:** Во время подготовки схемы очевидно, что поддерживает XML-сериализации подготовки шаблонов, он также предоставляет структуру для сериализации в формате JSON. Как правило схема предоставляет модель для определения подготовки структур.

## <a name="provisioning-schema-resources"></a>Подготовка схемы ресурсы

Можно получить подготовки схемы вместе с его вспомогательные файлы на репозиториев: [PnP-подготовки-схемы](https://github.com/SharePoint/PnP-Provisioning-Schema)

Существует видео Channel 9 20 минут, в котором обсуждаются подготовки схемы: [глубокое погружение в PnP подготовки схемы модуля](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).

Пример схемы доступны на: [репозиториев в PnP-подготовки-схеме и примеры](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).

В блоке кода отображает корневой элемент схемы и прямая дочерние элементы из корневого каталога. Документация по подготовки схемы можно найти на репозиториев: [PnP подготовки схемы](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).

```
<pnp:ProvisioningTemplate
           xmlns:pnp="http://schemas.dev.office.com/PnP/2015/08/ProvisioningSchema"
           ID="xsd:ID"
           Version="xsd:decimal"
           ImagePreviewUrl="xsd:string"
           DisplayName="xsd:string"
           Description="xsd:string">
   <pnp:Properties />
   <pnp:SitePolicy />
   <pnp:RegionalSettings />
   <pnp:SupportedUILanguages />
   <pnp:AuditSettings />
   <pnp:PropertyBagEntries />
   <pnp:Security />
   <pnp:SiteFields />
   <pnp:ContentTypes />
   <pnp:Lists />
   <pnp:Features />
   <pnp:CustomActions />
   <pnp:Files />
   <pnp:Pages />
   <pnp:TermGroups />
   <pnp:ComposedLook />
   <pnp:Workflows />
   <pnp:SearchSettings />
   <pnp:Publishing />
   <pnp:AddIns />
   <pnp:Providers />
</pnp:ProvisioningTemplate>
```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Глубокое погружение PnP схеме модуля подготовки](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
    
- [PnP подготовки схемы](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md)
    
- [Репозиториев в PnP подготовки схеме и примеры](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples)
