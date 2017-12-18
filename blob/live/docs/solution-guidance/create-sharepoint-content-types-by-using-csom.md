---
title: "Создание типов контента SharePoint с помощью CSOM"
ms.date: 11/03/2017
ms.openlocfilehash: 05d32f9c1ec1d48a128216116515eb106c221274
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-sharepoint-content-types-by-using-csom"></a><span data-ttu-id="c2e09-102">Создание типов контента SharePoint с помощью CSOM</span><span class="sxs-lookup"><span data-stu-id="c2e09-102">Create SharePoint content types by using CSOM</span></span>

<span data-ttu-id="c2e09-103">Создание типов контента SharePoint с помощью CSOM и внесение изменений локализации с помощью возможности, представленные в SharePoint 2013 с пакетом обновления 1.</span><span class="sxs-lookup"><span data-stu-id="c2e09-103">Create SharePoint content types by using CSOM, and make localization changes by using features introduced in SharePoint 2013 SP1.</span></span>

<span data-ttu-id="c2e09-104">_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="c2e09-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="c2e09-105">Пример [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) можно использовать для программного создания сайта столбцов и типов контента и их связи.</span><span class="sxs-lookup"><span data-stu-id="c2e09-105">You can use the [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) sample to programmatically create site columns and content types and link them together.</span></span> <span data-ttu-id="c2e09-106">Можно использовать API CSOM SharePoint 2013 с пакетом обновления 1, доступные в [Пакет SDK для SharePoint Server 2013 клиентских компонентов](http://www.microsoft.com/en-us/download/details.aspx?id=35585), чтобы добавить идентификатор определенного типа контента и локализация типов контента, списки и заголовков узла.</span><span class="sxs-lookup"><span data-stu-id="c2e09-106">You can also use the SharePoint 2013 SP1 CSOM APIs, available in the [SharePoint Server 2013 Client Components SDK](http://www.microsoft.com/en-us/download/details.aspx?id=35585), to add a specific content type identifier, and localize content types, lists, and site titles.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c2e09-107">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c2e09-107">Before you begin</span></span>

<span data-ttu-id="c2e09-108">Чтобы начать работу, загрузите образец [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="c2e09-108">To get started, download the [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) sample from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="create-content-types-and-site-columns"></a><span data-ttu-id="c2e09-109">Создание типов контента и столбцы сайта</span><span class="sxs-lookup"><span data-stu-id="c2e09-109">Create content types and site columns</span></span>

<span data-ttu-id="c2e09-110">В следующем примере кода показано, как создать тип контента с помощью класса **ContentTypeCreationInformation** , включая установку с идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c2e09-110">The following code example shows how to create a content type by using the  **ContentTypeCreationInformation** class, including setting the ID.</span></span>

> [!NOTE] 
> <span data-ttu-id="c2e09-111">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="c2e09-111">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
ContentTypeCollection contentTypes = web.ContentTypes;
cc.Load(contentTypes);
cc.ExecuteQuery();

foreach (var item in contentTypes)
{
  if (item.StringId == "0x0101009189AB5D3D2647B580F011DA2F356FB2")
    return;
}

// Create a Content Type Information object.
ContentTypeCreationInformation newCt = new ContentTypeCreationInformation();
// Set the name for the content type.
newCt.Name = "Contoso Document";
// Inherit from oob document - 0x0101 and assign. 
newCt.Id = "0x0101009189AB5D3D2647B580F011DA2F356FB2";
// Set content type to be available from specific group.
newCt.Group = "Contoso Content Types";
// Create the content type.
ContentType myContentType = contentTypes.Add(newCt);
cc.ExecuteQuery();

Using AddFieldAsXml you can add fields to the FieldCollection of a site collection:
FieldCollection fields = web.Fields;
cc.Load(fields);
cc.ExecuteQuery();

string FieldAsXML = @"<Field ID='{4F34B2ED-9CFF-4900-B091-4C0033F89944}' Name='ContosoString' DisplayName='Contoso String' Type='Text' Hidden='False' Group='Contoso Site Columns' Description='Contoso Text Field' />";
Field fld = fields.AddFieldAsXml(FieldAsXML, true, AddFieldOptions.DefaultValue);
cc.Load(fields);
cc.Load(fld);
cc.ExecuteQuery();

```

<span data-ttu-id="c2e09-112">Ссылка поля в типе контента с помощью классов **FieldLinkCollection** и **FieldLinkCreationInformation** .</span><span class="sxs-lookup"><span data-stu-id="c2e09-112">Link the fields to the content type by using the  **FieldLinkCollection** and **FieldLinkCreationInformation** classes.</span></span>

```C#
FieldCollection fields = web.Fields;
Field fld = fields.GetByInternalNameOrTitle("ContosoString");
cc.Load(fields);
cc.Load(fld);
cc.ExecuteQuery();

FieldLinkCollection refFields = myContentType.FieldLinks;
cc.Load(refFields);
cc.ExecuteQuery();

foreach (var item in refFields)
{
  if (item.Name == "ContosoString")
    return;
  }

FieldLinkCreationInformation link = new FieldLinkCreationInformation();
link.Field = fld;
myContentType.FieldLinks.Add(link);
myContentType.Update(true);
cc.ExecuteQuery();

```

## <a name="localize-content-types-list-and-site-titles"></a><span data-ttu-id="c2e09-113">Локализация типов контента, списков и сайтов заголовков</span><span class="sxs-lookup"><span data-stu-id="c2e09-113">Localize content types, list, and site titles</span></span>

<span data-ttu-id="c2e09-114">Локализация сайта заголовок и описание сайта, используйте следующий код.</span><span class="sxs-lookup"><span data-stu-id="c2e09-114">Use the following code to localize the site title and site description.</span></span>

```C#
web.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
web.DescriptionResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnetty saitti");

```

<span data-ttu-id="c2e09-115">Список используйте такой же подход как для сайта.</span><span class="sxs-lookup"><span data-stu-id="c2e09-115">For a list, you use the same approach as for a site.</span></span>

```C#
list.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
list.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ esimerkki nÃ¤yttÃ¤Ã¤ miten voit kielikÃ¤Ã¤ntÃ¤Ã¤ listoja.");

```

<span data-ttu-id="c2e09-116">Для типов контента вы можете для локализации имя и описание.</span><span class="sxs-lookup"><span data-stu-id="c2e09-116">For content types, you have the option to localize the name and description.</span></span> <span data-ttu-id="c2e09-117">для полей можно локализовать название и описание значения.</span><span class="sxs-lookup"><span data-stu-id="c2e09-117">for fields, you can localize the title and description values.</span></span>

```C#
myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Dokumentti");
myContentType.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ on geneerinen Contoso dokumentti.");

fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso Teksti");
fld.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤Ã¤ on niiku Contoso metadatalle.");

```

## <a name="create-document-content-types-and-site-columns"></a><span data-ttu-id="c2e09-118">Создание типов контента документов и столбцы сайта</span><span class="sxs-lookup"><span data-stu-id="c2e09-118">Create document content types and site columns</span></span>

<span data-ttu-id="c2e09-119">Следующем примере показано, как создавать типы контента документов и затем связать шаблон документа с типом контента.</span><span class="sxs-lookup"><span data-stu-id="c2e09-119">The following example shows how to create document content types and then associate a document template with the content type.</span></span> 

<span data-ttu-id="c2e09-120">В этом примере добавляется новый тип контента, называется «Contoso документа» для семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c2e09-120">This example adds a new content type called 'Contoso Document' to the site collection.</span></span> <span data-ttu-id="c2e09-121">Этот тип контента имеет настраиваемый шаблон, связанные с ним при создании нового документа.</span><span class="sxs-lookup"><span data-stu-id="c2e09-121">This content type has a custom template associated with it when a new document is created.</span></span>

```C#
ContentType ct = web.ContentTypes.GetById("0x0101009189AB5D3D2647B580F011DA2F356FB2");
            cc.Load(ct); cc.ExecuteQuery();
            string ctFolderServerRelativeURL = "_cts/" + ct.Name;
            Folder ctFolder = web.GetFolderByServerRelativeUrl(ctFolderServerRelativeURL);
            cc.Load(ctFolder);
            cc.ExecuteQuery();

            string path = @"C:\Data\Test Documents\Doc CT File.docx";
            string fileName = System.IO.Path.GetFileName(path);
            byte[] filecontent = System.IO.File.ReadAllBytes(path);

            using (System.IO.FileStream fs = new System.IO.FileStream(path, System.IO.FileMode.Open))
            {
                FileCreationInformation newFile = new FileCreationInformation();
                newFile.Content = filecontent;
                newFile.Url = ctFolderServerRelativeURL + "/" + fileName;

                Microsoft.SharePoint.Client.File uploadedFile = ctFolder.Files.Add(newFile);
                cc.Load(uploadedFile);
                cc.ExecuteQuery();
                //Microsoft.SharePoint.Client.File.SaveBinaryDirect(clientContext, ctFolderServerRelativeURL + "/" + fileName, fs, true);

                
                cc.Load(ct); cc.ExecuteQuery();
                ct.DocumentTemplate = fileName;
                ct.Update(false);
                cc.Load(ct); cc.ExecuteQuery();
                Console.WriteLine("Content type updates");
            }

```

## <a name="see-also"></a><span data-ttu-id="c2e09-122">См. также</span><span class="sxs-lookup"><span data-stu-id="c2e09-122">See also</span></span>
<span data-ttu-id="c2e09-123"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c2e09-123"></span></span>

- [<span data-ttu-id="c2e09-124">Решения по подготовке сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="c2e09-124">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="c2e09-125">FTC для КАМЕРУ - Создание типов контента с определенными идентификаторами, с помощью CSO</span><span class="sxs-lookup"><span data-stu-id="c2e09-125">FTC to CAM - Create Content Types with specific IDs using CSO</span></span>](http://blogs.msdn.com/b/vesku/archive/2014/02/28/ftc-to-cam-create-content-types-with-specific-ids-using-csom.aspx)
    
- [<span data-ttu-id="c2e09-126">Пакет SDK для SharePoint Server 2013 клиентских компонентов</span><span class="sxs-lookup"><span data-stu-id="c2e09-126">SharePoint Server 2013 Client Components SDK</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=35585)
