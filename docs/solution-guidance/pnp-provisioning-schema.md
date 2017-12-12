---
title: "PnP подготовки схемы"
ms.date: 11/03/2017
ms.openlocfilehash: e2bb1c364aca836bb6f38b487c88d1e4eeb879c8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="pnp-provisioning-schema"></a><span data-ttu-id="28340-102">PnP подготовки схемы</span><span class="sxs-lookup"><span data-stu-id="28340-102">PnP provisioning schema</span></span>

<span data-ttu-id="28340-103">Как было рассмотрено в нашем [PnP подготовки framework](pnp-provisioning-framework.md) и в другом месте, формат для подготовки шаблонов была отделена от формате сохранения, можно использовать любой формат, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="28340-103">As you learned in our [PnP provisioning framework](pnp-provisioning-framework.md) and elsewhere, the format for provisioning templates has been decoupled from the persistence format so that you can use any format you prefer.</span></span> <span data-ttu-id="28340-104">Тем не менее так как с помощью подготовки схемы XML для сохранения шаблонов распространенного сценария, мы предлагаем некоторые дополнительные сведения об использовании схемы XML для сериализации и сохраните подготовки шаблонов.</span><span class="sxs-lookup"><span data-stu-id="28340-104">Nevertheless, because using the XML provisioning schema for persisting templates is such a common scenario, we're providing some additional information about how to use the XML schema to serialize and save your provisioning templates.</span></span>

<span data-ttu-id="28340-105">**Важные:** Во время подготовки схемы очевидно, что поддерживает XML-сериализации подготовки шаблонов, он также предоставляет структуру для сериализации в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="28340-105">**Important:** While the provisioning schema obviously supports XML serialization of provisioning templates, it also provides the structure for serialization in JSON format.</span></span> <span data-ttu-id="28340-106">Как правило схема предоставляет модель для определения подготовки структур.</span><span class="sxs-lookup"><span data-stu-id="28340-106">More generally, the schema provides the model for defining provisioning structures.</span></span>

## <a name="provisioning-schema-resources"></a><span data-ttu-id="28340-107">Подготовка схемы ресурсы</span><span class="sxs-lookup"><span data-stu-id="28340-107">Provisioning schema resources</span></span>

<span data-ttu-id="28340-108">Можно получить подготовки схемы вместе с его вспомогательные файлы на репозиториев: [PnP-подготовки-схемы](https://github.com/SharePoint/PnP-Provisioning-Schema)</span><span class="sxs-lookup"><span data-stu-id="28340-108">You can get the provisioning schema, along with its supporting files, on GitHub: [PnP-Provisioning-Schema](https://github.com/SharePoint/PnP-Provisioning-Schema)</span></span>

<span data-ttu-id="28340-109">Существует видео Channel 9 20 минут, в котором обсуждаются подготовки схемы: [глубокое погружение в PnP подготовки схемы модуля](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).</span><span class="sxs-lookup"><span data-stu-id="28340-109">There is a 20-minute Channel 9 video that discusses the provisioning schema: [Deep dive to PnP provisioning engine schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).</span></span>

<span data-ttu-id="28340-110">Пример схемы доступны на: [репозиториев в PnP-подготовки-схеме и примеры](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="28340-110">Sample schemas are available on: [GitHub at PnP-Provisioning-Schema/Samples](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).</span></span>

<span data-ttu-id="28340-111">В блоке кода отображает корневой элемент схемы и прямая дочерние элементы из корневого каталога.</span><span class="sxs-lookup"><span data-stu-id="28340-111">The code block below displays the schema's root element and direct child elements of the root.</span></span> <span data-ttu-id="28340-112">Документация по подготовки схемы можно найти на репозиториев: [PnP подготовки схемы](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).</span><span class="sxs-lookup"><span data-stu-id="28340-112">You can find provisioning schema documentation on GitHub: [PnP Provisioning Schema](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).</span></span>

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

## <a name="see-also"></a><span data-ttu-id="28340-113">См. также</span><span class="sxs-lookup"><span data-stu-id="28340-113">See also</span></span>
<span data-ttu-id="28340-114"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="28340-114"></span></span>

- [<span data-ttu-id="28340-115">Глубокое погружение PnP схеме модуля подготовки</span><span class="sxs-lookup"><span data-stu-id="28340-115">Deep dive to PnP provisioning engine schema</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
    
- [<span data-ttu-id="28340-116">PnP подготовки схемы</span><span class="sxs-lookup"><span data-stu-id="28340-116">PnP Provisioning Schema</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md)
    
- [<span data-ttu-id="28340-117">Репозиториев в PnP подготовки схеме и примеры</span><span class="sxs-lookup"><span data-stu-id="28340-117">GitHub at PnP-Provisioning-Schema/Samples</span></span>](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples)
