---
title: "Создание типов контента SharePoint с помощью CSOM"
ms.date: 11/03/2017
ms.openlocfilehash: 6a0e7eff44bffbc6b2de3cc181fe9b2d09df1117
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="create-sharepoint-content-types-by-using-csom"></a>Создание типов контента SharePoint с помощью CSOM

Создание типов контента SharePoint с помощью CSOM и внесение изменений локализации с помощью возможности, представленные в SharePoint 2013 с пакетом обновления 1.

_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Пример [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) можно использовать для программного создания сайта столбцов и типов контента и их связи. Можно использовать API CSOM SharePoint 2013 с пакетом обновления 1, доступные в [Пакет SDK для SharePoint Server 2013 клиентских компонентов](http://www.microsoft.com/en-us/download/details.aspx?id=35585), чтобы добавить идентификатор определенного типа контента и локализация типов контента, списки и заголовков узла. 

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите образец [Core.SPD](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.SPD) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="create-content-types-and-site-columns"></a>Создание типов контента и столбцы сайта

В следующем примере кода показано, как создать тип контента с помощью класса **ContentTypeCreationInformation** , включая установку с идентификатором.

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

Ссылка поля в типе контента с помощью классов **FieldLinkCollection** и **FieldLinkCreationInformation** .

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

## <a name="localize-content-types-list-and-site-titles"></a>Локализация типов контента, списков и сайтов заголовков

Локализация сайта заголовок и описание сайта, используйте следующий код.

```C#
web.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
web.DescriptionResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnetty saitti");

```

Список используйте такой же подход как для сайта.

```C#
list.TitleResource.SetValueForUICulture("fi-FI", "KielikÃ¤Ã¤nnÃ¤ minut");
list.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ esimerkki nÃ¤yttÃ¤Ã¤ miten voit kielikÃ¤Ã¤ntÃ¤Ã¤ listoja.");

```

Для типов контента вы можете для локализации имя и описание. для полей можно локализовать название и описание значения.

```C#
myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Dokumentti");
myContentType.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤mÃ¤ on geneerinen Contoso dokumentti.");

fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso Teksti");
fld.DescriptionResource.SetValueForUICulture("fi-FI", "TÃ¤Ã¤ on niiku Contoso metadatalle.");

```

## <a name="create-document-content-types-and-site-columns"></a>Создание типов контента документов и столбцы сайта

Следующем примере показано, как создавать типы контента документов и затем связать шаблон документа с типом контента. 

В этом примере добавляется новый тип контента, называется «Contoso документа» для семейства веб-сайтов. Этот тип контента имеет настраиваемый шаблон, связанные с ним при создании нового документа.

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

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Решения по подготовке сайтов SharePoint](sharepoint-site-provisioning-solutions.md)
    
- [FTC для КАМЕРУ - Создание типов контента с определенными идентификаторами, с помощью CSO](http://blogs.msdn.com/b/vesku/archive/2014/02/28/ftc-to-cam-create-content-types-with-specific-ids-using-csom.aspx)
    
- [Пакет SDK для SharePoint Server 2013 клиентских компонентов](http://www.microsoft.com/en-us/download/details.aspx?id=35585)
