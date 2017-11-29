---
title: "PnP подготовки схемы"
ms.date: 11/03/2017
ms.openlocfilehash: acc16112e79972db74f97d50e20c1b0f1f0bb4f6
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="pnp-provisioning-schema"></a><span data-ttu-id="bb143-102">PnP подготовки схемы</span><span class="sxs-lookup"><span data-stu-id="bb143-102">PnP provisioning schema</span></span>

<span data-ttu-id="bb143-103">Как было рассмотрено в нашем [PnP подготовки framework](pnp-provisioning-framework.md) и в другом месте, формат для подготовки шаблонов была отделена от формате сохранения, можно использовать любой формат, который вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="bb143-103">As you learned in our [PnP provisioning framework](pnp-provisioning-framework.md) and elsewhere, the format for provisioning templates has been decoupled from the persistence format so that you can use any format you prefer.</span></span> <span data-ttu-id="bb143-104">Тем не менее так как с помощью подготовки схемы XML для сохранения шаблонов распространенного сценария, мы предлагаем некоторые дополнительные сведения об использовании схемы XML для сериализации и сохраните подготовки шаблонов.</span><span class="sxs-lookup"><span data-stu-id="bb143-104">Nevertheless, because using the XML provisioning schema for persisting templates is such a common scenario, we're providing some additional information about how to use the XML schema to serialize and save your provisioning templates.</span></span>

<span data-ttu-id="bb143-105">**Важные:** Во время подготовки схемы очевидно, что поддерживает XML-сериализации подготовки шаблонов, он также предоставляет структуру для сериализации в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="bb143-105">**Important:** While the provisioning schema obviously supports XML serialization of provisioning templates, it also provides the structure for serialization in JSON format.</span></span> <span data-ttu-id="bb143-106">Как правило схема предоставляет модель для определения подготовки структур.</span><span class="sxs-lookup"><span data-stu-id="bb143-106">More generally, the schema provides the model for defining provisioning structures.</span></span>

## <a name="provisioning-schema-resources"></a><span data-ttu-id="bb143-107">Подготовка схемы ресурсы</span><span class="sxs-lookup"><span data-stu-id="bb143-107">Provisioning schema resources</span></span>

<span data-ttu-id="bb143-108">Можно получить подготовки схемы вместе с его вспомогательные файлы на репозиториев: [PnP-подготовки-схемы](https://github.com/SharePoint/PnP-Provisioning-Schema)</span><span class="sxs-lookup"><span data-stu-id="bb143-108">You can get the provisioning schema, along with its supporting files, on GitHub: [PnP-Provisioning-Schema](https://github.com/SharePoint/PnP-Provisioning-Schema)</span></span>

<span data-ttu-id="bb143-109">Существует видео Channel 9 20 минут, в котором обсуждаются подготовки схемы: [глубокое погружение в PnP подготовки схемы модуля](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).</span><span class="sxs-lookup"><span data-stu-id="bb143-109">There is a 20-minute Channel 9 video that discusses the provisioning schema: [Deep dive to PnP provisioning engine schema](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema).</span></span>

<span data-ttu-id="bb143-110">Пример схемы доступны на: [репозиториев в PnP-подготовки-схеме и примеры](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="bb143-110">Sample schemas are available on: [GitHub at PnP-Provisioning-Schema/Samples](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples).</span></span>

<span data-ttu-id="bb143-111">В блоке кода отображает корневой элемент схемы и прямая дочерние элементы из корневого каталога.</span><span class="sxs-lookup"><span data-stu-id="bb143-111">The code block below displays the schema's root element and direct child elements of the root.</span></span> <span data-ttu-id="bb143-112">Документация по подготовки схемы можно найти на репозиториев: [PnP подготовки схемы](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).</span><span class="sxs-lookup"><span data-stu-id="bb143-112">You can find provisioning schema documentation on GitHub: [PnP Provisioning Schema](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md).</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="bb143-113">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bb143-113">Additional resources</span></span>
<span data-ttu-id="bb143-114"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bb143-114"></span></span>

- [<span data-ttu-id="bb143-115">Глубокое погружение PnP схеме модуля подготовки</span><span class="sxs-lookup"><span data-stu-id="bb143-115">Deep dive to PnP provisioning engine schema</span></span>](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)
    
- [<span data-ttu-id="bb143-116">PnP подготовки схемы</span><span class="sxs-lookup"><span data-stu-id="bb143-116">PnP Provisioning Schema</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/Tools/OfficeDevPnP.Core.Tools.DocsGenerator/OfficeDevPnP.Core.Tools.DocsGenerator/ProvisioningSchema-2015-08.md)
    
- [<span data-ttu-id="bb143-117">Репозиториев в PnP подготовки схеме и примеры</span><span class="sxs-lookup"><span data-stu-id="bb143-117">GitHub at PnP-Provisioning-Schema/Samples</span></span>](https://github.com/SharePoint/PnP-Provisioning-Schema/tree/master/Samples)
