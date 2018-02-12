---
title: "Использование одних данных в разных веб-частях с применением глобальной переменной (руководство)"
description: "Пошаговые инструкции по использованию одних данных в разных клиентских веб-частях SharePoint."
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: edc0ee05ebdc92c540b7b8bb64b29dae04718dd5
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="share-data-between-web-parts-by-using-a-global-variable-tutorial"></a><span data-ttu-id="b63c5-103">Использование одних данных в разных веб-частях с применением глобальной переменной (руководство)</span><span class="sxs-lookup"><span data-stu-id="b63c5-103">Share data between web parts by using a global variable (tutorial)</span></span>

<span data-ttu-id="b63c5-104">При создании клиентских веб-частей можно загрузить данные один раз и использовать их в разных веб-частях. Это ускоряет загрузку страниц и уменьшает нагрузку на сеть.</span><span class="sxs-lookup"><span data-stu-id="b63c5-104">When building client-side web parts, loading data once and reusing it across different web parts helps improve the performance of your pages and decrease the load on your network.</span></span> 

> [!NOTE] 
> <span data-ttu-id="b63c5-105">Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки для создания клиентских веб-частей SharePoint](../../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="b63c5-105">Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment.md).</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="b63c5-106">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="b63c5-106">Create a new project</span></span>

1. <span data-ttu-id="b63c5-107">С помощью командной строки создайте папку для проекта:</span><span class="sxs-lookup"><span data-stu-id="b63c5-107">Using a command prompt, create a new folder for your project:</span></span>

  ```sh
  md react-recentdocuments
  ```

2. <span data-ttu-id="b63c5-108">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="b63c5-108">Go into the project folder:</span></span>

  ```sh
  cd react-recentdocuments
  ```

3. <span data-ttu-id="b63c5-109">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="b63c5-109">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

4. <span data-ttu-id="b63c5-110">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b63c5-110">When prompted, use the following values:</span></span>

  - <span data-ttu-id="b63c5-111">**WebPart** в качестве типа создаваемого клиентского компонента;</span><span class="sxs-lookup"><span data-stu-id="b63c5-111">**WebPart** as the type of client-side component to create.</span></span>
  - <span data-ttu-id="b63c5-112">**react-recentdocuments** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="b63c5-112">**react-recentdocuments** as your solution name.</span></span>
  - <span data-ttu-id="b63c5-113">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="b63c5-113">**Use the current folder** for the location to place the files.</span></span>
  - <span data-ttu-id="b63c5-114">**Recent documents** (Последние документы) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="b63c5-114">**Recent documents** as your web part name.</span></span>
  - <span data-ttu-id="b63c5-115">**Shows recently modified documents** (Показывает недавно измененные документы) в качестве описания веб-части;</span><span class="sxs-lookup"><span data-stu-id="b63c5-115">**Shows recently modified documents** as your web part description.</span></span>
  - <span data-ttu-id="b63c5-116">**React** в качестве используемой платформы.</span><span class="sxs-lookup"><span data-stu-id="b63c5-116">**React** as the framework to use.</span></span>

  ![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../images/tutorial-sharingdata-yo-sharepoint-recent-documents.png)

5. <span data-ttu-id="b63c5-118">После завершения скаффолдинга заблокируйте версию зависимостей проекта, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b63c5-118">After the scaffolding completes, lock down the version of the project dependencies by running the following command:</span></span>

  ```sh
  npm shrinkwrap
  ```

6. <span data-ttu-id="b63c5-119">Откройте папку проекта в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="b63c5-119">Open your project folder in your code editor.</span></span> <span data-ttu-id="b63c5-120">В этой статье в инструкциях и на снимках экрана используется Visual Studio Code, но вы можете использовать любой другой редактор.</span><span class="sxs-lookup"><span data-stu-id="b63c5-120">This article uses Visual Studio Code in the steps and screenshots, but you can use any editor that you prefer.</span></span>

  ![Проект SharePoint Framework, открытый в Visual Studio Code](../../../images/tutorial-sharingdata-vscode.png)

  <br/>

## <a name="show-the-recently-modified-documents"></a><span data-ttu-id="b63c5-122">Отображение недавно измененных документов</span><span class="sxs-lookup"><span data-stu-id="b63c5-122">Show the recently modified documents</span></span>

<span data-ttu-id="b63c5-123">Веб-часть Recent Documents (Последние документы) показывает сведения о последних измененных документах в виде карточек, используя Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="b63c5-123">The Recent Documents web part shows information about the most recently modified documents displayed as cards by using Office UI Fabric.</span></span>

![Веб-часть Recent Documents (Последние документы) с тремя небольшими карточками документов, представляющими три последних измененных документа](../../../images/tutorial-sharingdata-recent-documents.png)

<br/>

### <a name="remove-the-standard-description-property"></a><span data-ttu-id="b63c5-125">Удаление стандартного свойства _description_</span><span class="sxs-lookup"><span data-stu-id="b63c5-125">Remove the standard _description_ property</span></span>

1. <span data-ttu-id="b63c5-126">Удалите стандартное свойство `description` из интерфейса `IRecentDocumentsWebPartProps`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-126">Remove the standard `description` property from the `IRecentDocumentsWebPartProps` interface.</span></span> <span data-ttu-id="b63c5-127">В редакторе кода откройте файл **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-127">In the code editor, open the **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts** file, and paste the following code:</span></span>

  ```typescript
  export interface IRecentDocumentsWebPartProps {
  }
  ```

2. <span data-ttu-id="b63c5-p103">Удалите стандартное свойство `description` из манифеста веб-части. Откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json** и удалите из свойства `properties` свойство `description`:</span><span class="sxs-lookup"><span data-stu-id="b63c5-p103">Remove the standard `description` property from the web part manifest. Open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json** file, and from the `properties` property, remove the `description` property:</span></span>

  ```json
  {
    "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

    "id": "7a7e3aa9-5d8a-4155-936b-0b0e06e9ca11",
    "alias": "RecentDocumentsWebPart",
    "componentType": "WebPart",
    "version": "0.0.1",
    "manifestVersion": 2,

    "preconfiguredEntries": [{
      "groupId": "7a7e3aa9-5d8a-4155-936b-0b0e06e9ca11",
      "group": { "default": "Under Development" },
      "title": { "default": "Recent documents" },
      "description": { "default": "Shows recently modified documents" },
      "officeFabricIconFontName": "Page",
      "properties": {
      }
    }]
  }
  ```

3. <span data-ttu-id="b63c5-130">Удалите стандартное свойство `description` из веб-части.</span><span class="sxs-lookup"><span data-stu-id="b63c5-130">Remove the standard `description` property from the web part.</span></span> <span data-ttu-id="b63c5-131">В редакторе кода откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** и замените метод `render` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-131">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file, and replace its `render` method with the following code:</span></span>

  ```typescript
  export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IRecentDocumentsProps > = React.createElement(
        RecentDocuments,
        {
        }
      );

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

4. <span data-ttu-id="b63c5-132">Замените метод `getPropertyPaneConfiguration` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-132">Replace its `getPropertyPaneConfiguration` method with the following code:</span></span>

  ```typescript
  export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
    // ...

    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.BasicGroupName,
                groupFields: []
              }
            ]
          }
        ]
      };
    }
  }
  ```

### <a name="create-the-idocumentactivity-interface"></a><span data-ttu-id="b63c5-133">Создание интерфейса IDocumentActivity</span><span class="sxs-lookup"><span data-stu-id="b63c5-133">Create the IDocumentActivity interface</span></span>

<span data-ttu-id="b63c5-134">Этот интерфейс используется для отображения сведений о действиях с определенным документом на карточке.</span><span class="sxs-lookup"><span data-stu-id="b63c5-134">Use this interface to display the activity information of a particular document on a card.</span></span>

<span data-ttu-id="b63c5-135">В папке **./src/webparts/recentDocuments** создайте файл с именем **IDocumentActivity.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-135">In the **./src/webparts/recentDocuments** folder, create a new file named **IDocumentActivity.ts**, and paste the following code:</span></span>

```typescript
export interface IDocumentActivity {
    title: string;
    actorName: string;
    actorImageUrl: string;
}
```

### <a name="create-the-idocument-interface"></a><span data-ttu-id="b63c5-136">Создание интерфейса IDocument</span><span class="sxs-lookup"><span data-stu-id="b63c5-136">Create the IDocument interface</span></span>

<span data-ttu-id="b63c5-137">Этот интерфейс представляет документ со всеми необходимыми сведениями для отображения документа в качестве карточки.</span><span class="sxs-lookup"><span data-stu-id="b63c5-137">This interface represents a document with all the information necessary to display the document as a card.</span></span>

<span data-ttu-id="b63c5-138">В папке **./src/webparts/recentDocuments** создайте файл с именем **IDocument.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-138">In the **./src/webparts/recentDocuments** folder, create a new file named **IDocument.ts**, and paste the following code:</span></span>

```typescript
import { IDocumentActivity } from './IDocumentActivity';

export interface IDocument {
    title: string;
    url: string;
    imageUrl: string;
    iconUrl: string;
    activity: IDocumentActivity;
}
```

### <a name="show-recent-documents-in-the-recentdocuments-react-component"></a><span data-ttu-id="b63c5-139">Отображение последних документов в компоненте React RecentDocuments</span><span class="sxs-lookup"><span data-stu-id="b63c5-139">Show recent documents in the RecentDocuments React component</span></span>

1. <span data-ttu-id="b63c5-p105">Добавьте свойство **documents** к интерфейсу **IRecentDocumentsProps**. В редакторе кода откройте файл **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-p105">Add the **documents** property to the **IRecentDocumentsProps** interface. In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file, and paste the following code:</span></span>

  ```typescript
  import { IDocument } from '../IDocument';

  export interface IRecentDocumentsProps {
    documents: IDocument[];
  }
  ```

2. <span data-ttu-id="b63c5-142">В редакторе кода откройте файл **./src/webparts/recentDocuments/components/RecentDocuments.tsx** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-142">In the code editor, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file, and paste the following code:</span></span>

  ```tsx
  import * as React from 'react';
  import {
    DocumentCard,
    DocumentCardType,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity
  } from 'office-ui-fabric-react';
  import { IDocument } from '../IDocument';
  import styles from './RecentDocuments.module.scss';
  import { IRecentDocumentsProps } from './IRecentDocumentsProps';

  export default class RecentDocuments extends React.Component<IRecentDocumentsProps, void> {
    public render(): React.ReactElement<IRecentDocumentsProps> {
      const documents: JSX.Element[] = this.props.documents.map((document: IDocument, index: number, array: IDocument[]): JSX.Element => {
        return (
          <DocumentCard type={DocumentCardType.compact} onClickHref={document.url} accentColor='#ce4b1f' key={index}>
            <DocumentCardPreview previewImages={[{
              name: document.title,
              url: document.url,
              previewImageSrc: document.imageUrl,
              iconSrc: document.iconUrl,
              width: 144
            }]} />
            <div className='ms-DocumentCard-details'>
              <DocumentCardTitle
                title={document.title}
                shouldTruncate={true} />
              <DocumentCardActivity
                activity={document.activity.title}
                people={
                  [
                    { name: document.activity.actorName, profileImageSrc: document.activity.actorImageUrl }
                  ]
                }
                />
            </div>
          </DocumentCard>
        );
      });
      return (
        <div className={styles.helloWorld}>
          {documents}
        </div>
      );
    }
  }
  ```

<br/>

<span data-ttu-id="b63c5-143">Для начала компонент просматривает документы, переданные с помощью свойства `documents`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-143">First, the component iterates through the documents passed by using its `documents` property.</span></span> <span data-ttu-id="b63c5-144">Для каждого документа он создает [карточку документа Office UI Fabric](https://developer.microsoft.com/ru-RU/fabric#/components/documentcard), заполняя ее свойства соответствующими сведениями о конкретном документе.</span><span class="sxs-lookup"><span data-stu-id="b63c5-144">For each document, it builds an [Office UI Fabric DocumentCard](https://developer.microsoft.com/ru-RU/fabric#/components/documentcard), filling its properties with the relevant information about that particular document.</span></span> <span data-ttu-id="b63c5-145">После создания карточек для всех документов компонент добавляет их в основной текст и возвращает полную разметку.</span><span class="sxs-lookup"><span data-stu-id="b63c5-145">Finally, when cards for all documents have been built, the component adds them to its body and returns the complete markup.</span></span>

### <a name="load-the-information-about-the-recent-documents"></a><span data-ttu-id="b63c5-146">Загрузка сведений о последних документах</span><span class="sxs-lookup"><span data-stu-id="b63c5-146">Load the information about the recent documents</span></span>

<span data-ttu-id="b63c5-p107">В этом примере сведения о недавно измененных документах загружаются из статического набора данных. Однако вы легко можете изменить эту реализацию, чтобы данные загружались из библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b63c5-p107">In this example, the information about the recently modified documents is loaded from a static data set. You could, however, easily change this implementation to load the data from a SharePoint document library instead.</span></span>

1. <span data-ttu-id="b63c5-149">Откройте в редакторе кода файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="b63c5-149">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file.</span></span> <span data-ttu-id="b63c5-150">Добавьте оператор импорта для интерфейса `IDocument` под другими операторами импорта в начале файла, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-150">Add an import statement for the `IDocument` interface under the other import statements at the top of the file by using the following code:</span></span>

  ```typescript
  import { IDocument } from './IDocument';
  ```

2. <span data-ttu-id="b63c5-151">В классе `RecentDocumentsWebPart` добавьте новую частную переменную с именем `documents`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-151">In the `RecentDocumentsWebPart` class, add a new private variable named `documents` by using the following code:</span></span>

  ```typescript
  export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
      private static documents: IDocument[] = [
          {
              title: 'Proposal for Jacksonville Expansion Ad Campaign',
              url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 25 2017',
                  actorName: 'Miriam Graham',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'Customer Feedback for ZT1000',
              url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&file=Customer%20Feedback%20for%20ZT1000.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&docId=17592968714930&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 23 2017',
                  actorName: 'Miriam Graham',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'Asia Q3 Marketing Overview',
              url: 'https://contoso-my.sharepoint.com/personal/alexw_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&file=Asia%20Q3%20Marketing%20Overview%20Beta.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=18231116-2bf0-474c-93ee-eb362681b293&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&docId=17592969984791&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 23 2017',
                  actorName: 'Alex Wilber',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'Trey Research Business Development Plan',
              url: 'https://contoso.sharepoint.com/sites/contoso/Resources/Document%20Center/_layouts/15/WopiFrame.aspx?sourcedoc=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&file=Trey%20Research%20Business%20Development%20Plan.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=923a6ce1-7b67-4bd0-a59f-89d37f233804&guidWeb=c12486eb-661c-46c7-baba-073a8a45b610&guidFile=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&docId=265998788&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 15 2017',
                  actorName: 'Alex Wilber',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'XT1000 Marketing Analysis',
              url: 'https://contoso-my.sharepoint.com/personal/henriettam_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&file=XT1000%20Marketing%20Analysis.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=b187e1dd-7687-49e0-87ff-6250e61e56ac&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&docId=17592963604695&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, December 15 2016',
                  actorName: 'Henrietta Mueller',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=henriettam@contoso.onmicrosoft.com&size=L'
              }
          }
      ];

      // ...
  }
  ```

  <br/>

3. <span data-ttu-id="b63c5-152">Измените метод `render`, чтобы он загружал и отображал сведения о недавно измененных документах:</span><span class="sxs-lookup"><span data-stu-id="b63c5-152">Change the `render` method to load and render the information about the recently modified documents:</span></span>

  ```typescript
  export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
    // ...
    public render(): void {
      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

      window.setTimeout((): void => {
        const element: React.ReactElement<IRecentDocumentsProps> = React.createElement(
          RecentDocuments,
          {
            documents: RecentDocumentsWebPart.documents.slice(0, 3)
          }
        );

        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        ReactDom.render(element, this.domElement);
      }, 300);
    }
    // ...
  }
  ```

4. <span data-ttu-id="b63c5-153">Убедитесь, что веб-часть работает надлежащим образом и отображает сведения о трех последних измененных документах. Для этого с помощью командной строки выполните в каталоге проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b63c5-153">Verify that the web part is working correctly and shows information about the three most recently modified documents by running the following command from a command prompt in your project directory:</span></span>

  ```sh
  gulp serve
  ```

5. <span data-ttu-id="b63c5-154">Добавьте веб-часть Recent Documents (Последние документы) на холст SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="b63c5-154">In the SharePoint Workbench, add the Recent Documents web part to the canvas.</span></span>

  ![Веб-часть Recent Documents (Последние документы) с тремя недавно измененными документами в виде карточек документов](../../../images/tutorial-sharingdata-recent-documents.png)

## <a name="show-the-most-recently-modified-document"></a><span data-ttu-id="b63c5-156">Отображение последнего измененного документа</span><span class="sxs-lookup"><span data-stu-id="b63c5-156">Show the most recently modified document</span></span>

<span data-ttu-id="b63c5-157">В веб-части Recent Document (Последний документ) отображаются сведения о последнем измененном документе.</span><span class="sxs-lookup"><span data-stu-id="b63c5-157">The Recent Document web part shows information about the most recently modified document.</span></span>

![Веб-часть Recent Document (Последний документ) с одной большой карточкой документа, содержащей сведения о последнем измененном документе](../../../images/tutorial-sharingdata-recent-document.png)

### <a name="add-the-second-web-part"></a><span data-ttu-id="b63c5-159">Добавление второй веб-части</span><span class="sxs-lookup"><span data-stu-id="b63c5-159">Add the second web part</span></span>

<span data-ttu-id="b63c5-160">Чтобы продемонстрировать совместное использование данных разными веб-частями, добавьте к проекту вторую веб-часть.</span><span class="sxs-lookup"><span data-stu-id="b63c5-160">To illustrate sharing data between web parts, add a second web part to the project.</span></span>

1. <span data-ttu-id="b63c5-161">С помощью командной строки запустите в папке проекта генератор Yeoman для SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b63c5-161">Using a command prompt in the project folder, run the SharePoint Framework Yeoman generator.</span></span>

  ```sh
  yo @microsoft/sharepoint
  ```

2. <span data-ttu-id="b63c5-162">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b63c5-162">When prompted, enter the following values:</span></span>

  - <span data-ttu-id="b63c5-163">**WebPart** в качестве типа создаваемого клиентского компонента;</span><span class="sxs-lookup"><span data-stu-id="b63c5-163">**WebPart** as the type of client-side component to create.</span></span>
  - <span data-ttu-id="b63c5-164">**Recent document** (Последний документ) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="b63c5-164">**Recent document** as your web part name.</span></span>
  - <span data-ttu-id="b63c5-165">**Shows information about the most recently modified document** (Показывает сведения о последнем измененном документе) в качестве описания веб-части.</span><span class="sxs-lookup"><span data-stu-id="b63c5-165">**Shows information about the most recently modified document** as your web part description.</span></span>

  ![Генератор Yeoman для SharePoint Framework со сведениями для формирования второй веб-части](../../../images/tutorial-sharingdata-yo-sharepoint-recent-document.png)

### <a name="remove-the-standard-description-property"></a><span data-ttu-id="b63c5-167">Удаление стандартного свойства _description_</span><span class="sxs-lookup"><span data-stu-id="b63c5-167">Remove the standard _description_ property</span></span>

1. <span data-ttu-id="b63c5-168">Удалите свойство `description` из интерфейса `IRecentDocumentWebPartProps`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-168">Remove the `description` property from the `IRecentDocumentWebPartProps` interface.</span></span> <span data-ttu-id="b63c5-169">В редакторе кода откройте файл **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-169">In the code editor, open the **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts** file, and paste the following code:</span></span>

  ```typescript
  export interface IRecentDocumentWebPartProps {
  }
  ```

2. <span data-ttu-id="b63c5-p110">Удалите стандартное свойство `description` из манифеста веб-части. Откройте файл **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json** и удалите из свойства `properties` свойство `description`:</span><span class="sxs-lookup"><span data-stu-id="b63c5-p110">Remove the standard `description` property from the web part manifest. Open the **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json** file, and from the `properties` property, remove the `description` property:</span></span>

  ```json
  {
    "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

    "id": "71a6f643-1ac1-47ee-a9f1-502ef52f26d4",
    "alias": "RecentDocumentWebPart",
    "componentType": "WebPart",
    "version": "0.0.1",
    "manifestVersion": 2,

    "preconfiguredEntries": [{
      "groupId": "71a6f643-1ac1-47ee-a9f1-502ef52f26d4",
      "group": { "default": "Under Development" },
      "title": { "default": "Recent document" },
      "description": { "default": "Shows information about the most recently modified document" },
      "officeFabricIconFontName": "Page",
      "properties": {
      }
    }]
  }
  ```

3. <span data-ttu-id="b63c5-172">Удалите стандартное свойство `description` из области свойств веб-части.</span><span class="sxs-lookup"><span data-stu-id="b63c5-172">Remove the standard `description` property from the web part property pane.</span></span> <span data-ttu-id="b63c5-173">В редакторе кода откройте файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts** и замените метод `render` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-173">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file, and replace its `render` method with the following code:</span></span>

  ```typescript
  export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
    // ...
    public render(): void {
      const element: React.ReactElement<IRecentDocumentProps> = React.createElement(
        RecentDocument,
        {
        }
      );

      ReactDom.render(element, this.domElement);
    }
    // ...
  }
  ```

4. <span data-ttu-id="b63c5-174">Замените метод `getPropertyPaneConfiguration` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-174">Replace its `getPropertyPaneConfiguration` method with the following code:</span></span>

  ```typescript
  export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
    // ...

    protected getPropertyPaneConfiguration(): IPropertyPaneConfiguration {
      return {
        pages: [
          {
            header: {
              description: strings.PropertyPaneDescription
            },
            groups: [
              {
                groupName: strings.BasicGroupName,
                groupFields: []
              }
            ]
          }
        ]
      };
    }
  }
  ```

### <a name="reuse-the-idocument-and-idocumentactivity-interfaces"></a><span data-ttu-id="b63c5-175">Повторное использование интерфейсов _IDocument_ и _IDocumentActivity_</span><span class="sxs-lookup"><span data-stu-id="b63c5-175">Reuse the _IDocument_ and _IDocumentActivity_ interfaces</span></span>

<span data-ttu-id="b63c5-176">Веб-части "Recent Document" (Последний документ) и "Recent Documents" (Последние документы) отображают сведения о последнем измененном документе по-разному, но они используют одну и ту же структуру данных, представляющую документ.</span><span class="sxs-lookup"><span data-stu-id="b63c5-176">The Recent Document web part displays information about the most recently modified document in a different way than the Recent Documents web part, but both web parts use the same data structure representing a document.</span></span> <span data-ttu-id="b63c5-177">Вместо того чтобы дублировать интерфейсы `IDocument` и `IDocumentActivity`, вы можете использовать их в обеих веб-частях.</span><span class="sxs-lookup"><span data-stu-id="b63c5-177">Instead of duplicating the `IDocument` and `IDocumentActivity` interfaces, you can reuse them across both web parts.</span></span>

1. <span data-ttu-id="b63c5-178">В Visual Studio Code откройте область обозревателя и в папке **./src/webparts/recentDocuments** переместите файлы **IDocument.ts** и **IDocumentActivity.ts** на один уровень выше, в папку **./src/webparts**.</span><span class="sxs-lookup"><span data-stu-id="b63c5-178">In Visual Studio Code, activate the Explorer pane, and from the **./src/webparts/recentDocuments** folder, move the **IDocument.ts** and **IDocumentActivity.ts** files one level up, to the **./src/webparts** folder.</span></span>

  ![Область обозревателя Visual Studio Code с выделенными файлами IDocument.ts и IDocumentActivity.ts](../../../images/tutorial-sharingdata-interfaces.png)

  <br/>

  <span data-ttu-id="b63c5-180">Переместив файлы в другую папку проекта, необходимо обновить пути в ссылках на них.</span><span class="sxs-lookup"><span data-stu-id="b63c5-180">Having moved the files to another location in your project, you need to update the paths where they're referenced.</span></span>

2. <span data-ttu-id="b63c5-181">В редакторе кода откройте файл **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** и измените код в нем на следующий:</span><span class="sxs-lookup"><span data-stu-id="b63c5-181">In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file, and change its code to:</span></span>

  ```typescript
  import { IDocument } from '../../IDocument';

  export interface IRecentDocumentsProps {
    documents: IDocument[];
  }
  ```

3. <span data-ttu-id="b63c5-182">Откройте файл **./src/webparts/recentDocuments/components/RecentDocuments.tsx** и замените оператор `import` в интерфейсе `IDocument` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-182">Open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file, and update the `import` statement of the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument } from '../../IDocument';
  ```

4. <span data-ttu-id="b63c5-183">Откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** и замените оператор `import` в интерфейсе `IDocument` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-183">Open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file, and update the `import` statement of the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument } from '../IDocument';
  ```

### <a name="show-the-most-recent-document-in-the-recentdocument-react-component"></a><span data-ttu-id="b63c5-184">Отображение последнего документа в компоненте React RecentDocument</span><span class="sxs-lookup"><span data-stu-id="b63c5-184">Show the most recent document in the RecentDocument React component</span></span>

1. <span data-ttu-id="b63c5-p113">Добавьте свойство `document` к интерфейсу `IRecentDocumentProps`. В редакторе кода откройте файл **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-p113">Add the `document` property to the `IRecentDocumentProps` interface. In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file, and paste the following code:</span></span>

  ```typescript
  import { IDocument } from '../../IDocument';

  export interface IRecentDocumentProps {
    document: IDocument;
  }
  ```

2. <span data-ttu-id="b63c5-187">В редакторе кода откройте файл **./src/webparts/recentDocument/components/RecentDocument.tsx** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-187">In the code editor, open the **./src/webparts/recentDocument/components/RecentDocument.tsx** file, and paste the following code:</span></span>

  ```typescriptx
  import * as React from 'react';
  import {
    DocumentCard,
    DocumentCardPreview,
    DocumentCardTitle,
    DocumentCardActivity,
    ImageFit
  } from 'office-ui-fabric-react';
  import { IDocument } from '../../IDocument';
  import styles from './RecentDocument.module.scss';
  import { IRecentDocumentProps } from './IRecentDocumentProps';

  export default class RecentDocument extends React.Component<IRecentDocumentProps, void> {
    public render(): React.ReactElement<IRecentDocumentProps> {
      const document: IDocument = this.props.document;

      return (
        <div className={styles.helloWorld}>
          <DocumentCard onClickHref={document.url}>
            <DocumentCardPreview previewImages={[{
              name: document.title,
              url: document.url,
              previewImageSrc: document.imageUrl,
              iconSrc: document.iconUrl,
              imageFit: ImageFit.cover,
              width: 318,
              height: 196,
              accentColor: '#ce4b1f'
            }]} />
            <DocumentCardTitle
              title={document.title}
              shouldTruncate={true} />
            <DocumentCardActivity
              activity={document.activity.title}
              people={
                [
                  { name: document.activity.actorName, profileImageSrc: document.activity.actorImageUrl }
                ]
              }
              />
          </DocumentCard>
        </div>
      );
    }
  }
  ```

  <br/>

<span data-ttu-id="b63c5-188">Компонент React `RecentDocument` отображает карточку документа Office UI Fabric, используя сведения о последнем измененном документе, передаваемые в свойстве `document`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-188">The `RecentDocument` React component uses the information about the most recently modified document passed in the `document` property to render an Office UI Fabric DocumentCard.</span></span>

### <a name="load-the-information-about-the-recent-document"></a><span data-ttu-id="b63c5-189">Загрузка сведений о последнем документе</span><span class="sxs-lookup"><span data-stu-id="b63c5-189">Load the information about the recent document</span></span>

<span data-ttu-id="b63c5-p114">В этом примере сведения о последнем измененном документе загружаются из статического набора данных. Однако вы легко можете изменить эту реализацию, чтобы данные загружались из библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b63c5-p114">In this example, the information about the most recently modified document is loaded from a static data set. You could, however, easily change this implementation to load the data from a SharePoint document library instead.</span></span>

1. <span data-ttu-id="b63c5-192">Откройте в редакторе кода файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts**.</span><span class="sxs-lookup"><span data-stu-id="b63c5-192">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file.</span></span> <span data-ttu-id="b63c5-193">Добавьте оператор импорта для интерфейса `IDocument` под другими операторами импорта в начале файла, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-193">Add an import statement for the `IDocument` interface under the other import statements at the top of the file by using the following code:</span></span>

  ```typescript
  import { IDocument } from '../IDocument';
  ```

2. <span data-ttu-id="b63c5-194">В классе `RecentDocumentWebPart` добавьте новую частную переменную с именем `document`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-194">In the `RecentDocumentWebPart` class, add a new private variable named `document` by using the following code:</span></span>

  ```typescript
  export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
      private static document: IDocument = {
          title: 'Proposal for Jacksonville Expansion Ad Campaign',
          url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
          imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
          iconUrl: '',
          activity: {
              title: 'Modified, January 25 2017',
              actorName: 'Miriam Graham',
              actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
          }
      };

      // ...
  }
  ```

3. <span data-ttu-id="b63c5-195">Измените метод `render`, чтобы он загружал и отображал сведения о последнем измененном документе:</span><span class="sxs-lookup"><span data-stu-id="b63c5-195">Change the `render` method to load and render the information about the most recently modified document:</span></span>

  ```typescript
  export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
    // ...
    public render(): void {
      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

      window.setTimeout((): void => {
        const element: React.ReactElement<IRecentDocumentProps> = React.createElement(
          RecentDocument,
          {
            document: RecentDocumentWebPart.document
          }
        );

        this.context.statusRenderer.clearLoadingIndicator(this.domElement);
        ReactDom.render(element, this.domElement);
      }, 300);
    }
    // ...
  }
  ```

4. <span data-ttu-id="b63c5-196">Убедитесь, что веб-часть работает надлежащим образом и отображает сведения о последнем измененном документе. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b63c5-196">Verify that the web part is working correctly and shows information about the most recently modified document by running the following command from a command prompt in your project folder:</span></span>

  ```sh
  gulp serve
  ```

5. <span data-ttu-id="b63c5-197">Добавьте веб-часть Recent Document (Последний документ) на холст SharePoint Workbench.</span><span class="sxs-lookup"><span data-stu-id="b63c5-197">In the SharePoint Workbench, add the Recent Document web part to the canvas.</span></span>

  ![Веб-часть Recent Document (Последний документ) с карточкой документа, содержащей сведения о последнем измененном документе](../../../images/tutorial-sharingdata-recent-document.png)


<br/>

<span data-ttu-id="b63c5-199">Текущая реализация — типичный пример независимой разработки двух веб-частей.</span><span class="sxs-lookup"><span data-stu-id="b63c5-199">The current implementation is a typical example of two web parts being developed independently.</span></span> <span data-ttu-id="b63c5-200">Если они обе располагаются на одной странице и загружают данные из SharePoint, то для получения похожих сведений приходится выполнять два отдельных запроса.</span><span class="sxs-lookup"><span data-stu-id="b63c5-200">If they were both placed on the same page and were loading data from SharePoint, they would execute two separate requests to retrieve similar information.</span></span> <span data-ttu-id="b63c5-201">Если в тот или иной момент вам потребуется изменить источник, из которого загружаются данные о недавно измененных документах, то придется обновлять обе веб-части.</span><span class="sxs-lookup"><span data-stu-id="b63c5-201">If, at some point, you had to change where the information about the recently modified documents is loaded from, you would have to update both web parts.</span></span> 

<span data-ttu-id="b63c5-202">Чтобы ускорить загрузку страницы и упростить работу с кодом веб-части, вы можете централизовать логику получения данных и сделать однажды полученные данные доступными обеим веб-частям.</span><span class="sxs-lookup"><span data-stu-id="b63c5-202">To improve the performance of loading the page and simplify maintaining the web part code, you can centralize the logic of retrieving the data and make the once retrieved data available to both web parts.</span></span>

## <a name="centralize-loading-data"></a><span data-ttu-id="b63c5-203">Централизованная загрузка данных</span><span class="sxs-lookup"><span data-stu-id="b63c5-203">Centralize loading data</span></span>

<span data-ttu-id="b63c5-204">Чтобы централизовать загрузку сведений о недавно измененных документах, создайте службу, на которую будут ссылаться обе веб-части.</span><span class="sxs-lookup"><span data-stu-id="b63c5-204">To centralize loading the information about recently modified documents, build a service that is referenced by both web parts.</span></span>

### <a name="move-the-data-model-interfaces"></a><span data-ttu-id="b63c5-205">Перемещение интерфейсов модели данных</span><span class="sxs-lookup"><span data-stu-id="b63c5-205">Move the data model interfaces</span></span>

1. <span data-ttu-id="b63c5-206">Создайте в папке проекта путь **./src/services/documentsService**.</span><span class="sxs-lookup"><span data-stu-id="b63c5-206">In the project folder, create the **./src/services/documentsService** folder path.</span></span> 

2. <span data-ttu-id="b63c5-207">Переместите файлы **IDocument.ts** и **IDocumentActivity.ts** из папки **./src/webparts** в папку **./src/services/documentsService**.</span><span class="sxs-lookup"><span data-stu-id="b63c5-207">From the **./src/webparts** folder, move the **IDocument.ts** and **IDocumentActivity.ts** files to the **./src/services/documentsService** folder.</span></span>

  ![Файлы IDocument.ts и IDocumentActivity.ts, выделенные в области обозревателя Visual Studio Code](../../../images/tutorial-sharingdata-interfaces-documentsservice.png)

### <a name="build-the-data-access-service"></a><span data-ttu-id="b63c5-209">Создание службы доступа к данным</span><span class="sxs-lookup"><span data-stu-id="b63c5-209">Build the data access service</span></span>

<span data-ttu-id="b63c5-210">В папке **./src/services/documentsService** создайте файл с именем **DocumentsService.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-210">In the **./src/services/documentsService** folder, create a new file named **DocumentsService.ts**, and paste the following code:</span></span>

```typescript
import { IDocument } from './IDocument';

export class DocumentsService {
    private static documents: IDocument[] = [
        {
            title: 'Proposal for Jacksonville Expansion Ad Campaign',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 25 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Customer Feedback for ZT1000',
            url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&file=Customer%20Feedback%20for%20ZT1000.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&docId=17592968714930&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Miriam Graham',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Asia Q3 Marketing Overview',
            url: 'https://contoso-my.sharepoint.com/personal/alexw_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&file=Asia%20Q3%20Marketing%20Overview%20Beta.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=18231116-2bf0-474c-93ee-eb362681b293&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&docId=17592969984791&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 23 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'Trey Research Business Development Plan',
            url: 'https://contoso.sharepoint.com/sites/contoso/Resources/Document%20Center/_layouts/15/WopiFrame.aspx?sourcedoc=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&file=Trey%20Research%20Business%20Development%20Plan.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=923a6ce1-7b67-4bd0-a59f-89d37f233804&guidWeb=c12486eb-661c-46c7-baba-073a8a45b610&guidFile=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&docId=265998788&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, January 15 2017',
                actorName: 'Alex Wilber',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
            }
        },
        {
            title: 'XT1000 Marketing Analysis',
            url: 'https://contoso-my.sharepoint.com/personal/henriettam_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&file=XT1000%20Marketing%20Analysis.pptx&action=view&DefaultItemOpen=1',
            imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=b187e1dd-7687-49e0-87ff-6250e61e56ac&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&docId=17592963604695&metadataToken=&clienttype=DelveWebHomeFeed',
            iconUrl: '',
            activity: {
                title: 'Modified, December 15 2016',
                actorName: 'Henrietta Mueller',
                actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=henriettam@contoso.onmicrosoft.com&size=L'
            }
        }
    ];

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            window.setTimeout((): void => {
                resolve(DocumentsService.documents[0]);
            }, 300);
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            window.setTimeout((): void => {
                resolve(DocumentsService.documents.slice(startFrom, startFrom + 3));
            }, 300);
        });
    }
}
```

<span data-ttu-id="b63c5-p117">Класс `DocumentsService` — это пример службы, загружающей сведения о последних документах. В этом примере используется статический набор данных, но вы легко можете изменить его реализацию, чтобы данные загружались из библиотеки документов SharePoint. На этом этапе класс `DocumentsService` уже предоставляет центральную точку доступа к данным для всех веб-частей, но еще не сохраняет ранее загруженные данные. Эту возможность мы реализуем позже.</span><span class="sxs-lookup"><span data-stu-id="b63c5-p117">The `DocumentsService` class is a sample service that loads information about recent documents. In this example, it uses a static data set, but you could easily change its implementation to load its data from a SharePoint document library. At this stage, the `DocumentsService` class offers a centralized point for all web parts to access their data, but it doesn't store the previously loaded data. You will implement that later in this tutorial.</span></span>

### <a name="create-a-barrel-for-the-service-files"></a><span data-ttu-id="b63c5-215">Создание блока данных для системных файлов</span><span class="sxs-lookup"><span data-stu-id="b63c5-215">Create a barrel for the service files</span></span>

<span data-ttu-id="b63c5-216">Ссылаясь на файлы в проекте, вы указываете относительный путь.</span><span class="sxs-lookup"><span data-stu-id="b63c5-216">When referencing files in a project, you point to their relative path.</span></span> <span data-ttu-id="b63c5-217">При изменении этого пути потребуется обновить все ссылки на соответствующий файл.</span><span class="sxs-lookup"><span data-stu-id="b63c5-217">Whenever that path changes, you have to update all references to the particular file.</span></span> <span data-ttu-id="b63c5-218">Такие изменения очень вероятны в начале разработки, когда добавляются различные элементы, а окончательная структура проекта еще не определена.</span><span class="sxs-lookup"><span data-stu-id="b63c5-218">Such changes are very likely at the beginning of the project when the different elements are being added and the final project structure is unclear.</span></span> <span data-ttu-id="b63c5-219">Во избежание частых изменений ссылок на файлы в проекте вы можете использовать блоки данных.</span><span class="sxs-lookup"><span data-stu-id="b63c5-219">To avoid frequent changes to file references in a project, you can use barrels.</span></span>

<span data-ttu-id="b63c5-220">Блок данных — это контейнер, объединяющий ряд экспортированных объектов.</span><span class="sxs-lookup"><span data-stu-id="b63c5-220">A barrel is a container that combines a number of exported objects.</span></span> <span data-ttu-id="b63c5-221">С их помощью вы можете абстрагировать точное расположение файлов от других элементов проекта, использующих их.</span><span class="sxs-lookup"><span data-stu-id="b63c5-221">By using barrels, you can abstract away the exact location of files from other elements in the project that are using them.</span></span>

<span data-ttu-id="b63c5-222">В папке **./src/services/documentsService** создайте файл с именем **index.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-222">In the **./src/services/documentsService** folder, create a new file named **index.ts**, and paste the following code:</span></span>

```typescript
export { IDocument } from './IDocument';
export { IDocumentActivity } from './IDocumentActivity';
export { DocumentsService } from './DocumentsService';
```

<span data-ttu-id="b63c5-223">После определения блока данных другие элементы проекта смогут ссылаться на любой из экспортированных типов по относительному пути к папке **./src/services/documentsService**, а не точному пути к отдельному файлу.</span><span class="sxs-lookup"><span data-stu-id="b63c5-223">With this barrel defined, other elements in the project can reference any of the exported types by using the relative path to the **./src/services/documentsService** folder instead of the exact path to the individual files.</span></span> <span data-ttu-id="b63c5-224">Например, ссылка на интерфейс `IDocument` может быть такой:</span><span class="sxs-lookup"><span data-stu-id="b63c5-224">For example, the `IDocument` interface can be referenced like this:</span></span>

```typescript
import { IDocument } from '../services/documentsService';
```

<span data-ttu-id="b63c5-225">а не такой:</span><span class="sxs-lookup"><span data-stu-id="b63c5-225">instead of:</span></span>

```typescript
import { IDocument } from '../services/documentsService/IDocument.ts';
```

<span data-ttu-id="b63c5-p121">Если в тот или иной момент вы решите, что предпочтительней переместить файл **IDocument.ts** во вложенную папку или объединить несколько файлов, изменить потребуется только путь к определению блока данных (**./src/services/documentsService/index.ts**). Все элементы проекта по-прежнему могут использовать тот же относительный путь к папке **documentsService**, чтобы ссылаться на интерфейс `IDocument`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-p121">If at some point you decided that it's better to move the **IDocument.ts** file to a subfolder or merge a few files together, the only thing that you would change is the path in the barrel definition (**./src/services/documentsService/index.ts**). All elements in the project could still use the exact same relative path to the **documentsService** folder to reference the `IDocument` interface.</span></span>


### <a name="update-references-to-the-moved-files-to-use-the-barrel"></a><span data-ttu-id="b63c5-228">Обновление ссылок на перемещенные файлы для использования блока данных</span><span class="sxs-lookup"><span data-stu-id="b63c5-228">Update references to the moved files to use the barrel</span></span>

<span data-ttu-id="b63c5-229">Так как вы переместили файлы **IDocument.ts** и **IDocumentActivity.ts** в другое расположение, необходимо обновить ссылки на них.</span><span class="sxs-lookup"><span data-stu-id="b63c5-229">Because you have moved the **IDocument.ts** and **IDocumentActivity.ts** files to another location, you have to update their references.</span></span> <span data-ttu-id="b63c5-230">Благодаря блокам данных в дальнейшем вам не придется это делать.</span><span class="sxs-lookup"><span data-stu-id="b63c5-230">Thanks to the barrel, this is the last time that you have to do this.</span></span>

#### <a name="update-references-in-the-recent-documents-web-part"></a><span data-ttu-id="b63c5-231">Обновление ссылок в веб-части Recent Documents (Последние документы)</span><span class="sxs-lookup"><span data-stu-id="b63c5-231">Update references in the Recent Documents web part</span></span>

1. <span data-ttu-id="b63c5-232">В редакторе кода откройте файл **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** и измените код в нем на следующий:</span><span class="sxs-lookup"><span data-stu-id="b63c5-232">In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file, and change its code to:</span></span>

  ```typescript
  import { IDocument } from '../../../services/documentsService';

  export interface IRecentDocumentsProps {
    documents: IDocument[];
  }
  ```

2. <span data-ttu-id="b63c5-233">Откройте файл **./src/webparts/recentDocuments/components/RecentDocuments.tsx** и замените оператор `import` в интерфейсе `IDocument` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-233">Open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file, and change the `import` statement of the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument } from '../../../services/documentsService';
  ```

3. <span data-ttu-id="b63c5-234">Откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** и замените оператор `import` в интерфейсе `IDocument` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="b63c5-234">Open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file, and change the `import` statement of the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument } from '../../services/documentsService';
  ```

#### <a name="update-references-in-the-recent-document-web-part"></a><span data-ttu-id="b63c5-235">Обновление ссылок в веб-части Recent Document (Последний документ)</span><span class="sxs-lookup"><span data-stu-id="b63c5-235">Update references in the Recent Document web part</span></span>

1. <span data-ttu-id="b63c5-236">В редакторе кода откройте файл **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="b63c5-236">In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file, and change its code to:</span></span>

  ```typescript
  import { IDocument } from '../../../services/documentsService';

  export interface IRecentDocumentProps {
    document: IDocument;
  }
  ```

2. <span data-ttu-id="b63c5-237">Откройте файл **./src/webparts/recentDocument/components/RecentDocument.tsx** и измените оператор `import` в интерфейсе `IDocument` на следующий:</span><span class="sxs-lookup"><span data-stu-id="b63c5-237">Open the **./src/webparts/recentDocument/components/RecentDocument.tsx** file, and change the `import` statement of the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument } from '../../../services/documentsService';
  ```

3. <span data-ttu-id="b63c5-238">Откройте файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts** и замените оператор `import` в интерфейсе `IDocument` на следующий:</span><span class="sxs-lookup"><span data-stu-id="b63c5-238">Open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file, and change the `import` statement of the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument } from '../../services/documentsService';
  ```

4. <span data-ttu-id="b63c5-239">Убедитесь, что ваши изменения работают надлежащим образом. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b63c5-239">Verify that your changes work as expected, by running the following command from a command prompt in your project folder:</span></span>

  ```sh
  gulp serve
  ```

  <br/>

  ![Веб-части Recent Document (Последний документ) и Recent Documents (Последние документы) с информацией о недавно измененных документах](../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="load-web-part-data-by-using-the-data-service"></a><span data-ttu-id="b63c5-241">Загрузка данных веб-частей с помощью службы данных</span><span class="sxs-lookup"><span data-stu-id="b63c5-241">Load web part data by using the data service</span></span>

<span data-ttu-id="b63c5-242">Когда служба данных будет готова, необходимо выполнить рефакторинг обеих веб-частей, чтобы они загружали свои данные с помощью службы данных.</span><span class="sxs-lookup"><span data-stu-id="b63c5-242">With the data service ready, the next step is to refactor both web parts to use the data service to load their data.</span></span>

#### <a name="load-information-about-the-recently-modified-documents"></a><span data-ttu-id="b63c5-243">Загрузка сведений о недавно измененных документах</span><span class="sxs-lookup"><span data-stu-id="b63c5-243">Load information about the recently modified documents</span></span>

1. <span data-ttu-id="b63c5-p123">Откройте в редакторе кода файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Замените оператор `import`, ссылающийся на интерфейс `IDocument`, на следующий оператор:</span><span class="sxs-lookup"><span data-stu-id="b63c5-p123">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Expand the `import` statement referencing the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument, DocumentsService } from '../../services/documentsService';
  ```

2. <span data-ttu-id="b63c5-246">Обновите метод `render`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-246">Update the `render` method by using the following code:</span></span>

  ```typescript
  export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
    // ...
    public render(): void {
      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

      DocumentsService.getRecentDocuments()
        .then((documents: IDocument[]): void => {
          const element: React.ReactElement<IRecentDocumentsProps> = React.createElement(
            RecentDocuments,
            {
              documents: documents
            }
          );

          this.context.statusRenderer.clearLoadingIndicator(this.domElement);
          ReactDom.render(element, this.domElement);
        });
    }
    // ...
  }
  ```

#### <a name="load-information-about-the-most-recently-modified-document"></a><span data-ttu-id="b63c5-247">Загрузка сведений о последнем измененном документе</span><span class="sxs-lookup"><span data-stu-id="b63c5-247">Load information about the most recently modified document</span></span>

1. <span data-ttu-id="b63c5-p124">Откройте в редакторе кода файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Замените оператор `import`, ссылающийся на интерфейс `IDocument`, на следующий оператор:</span><span class="sxs-lookup"><span data-stu-id="b63c5-p124">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Expand the `import` statement referencing the `IDocument` interface to:</span></span>

  ```typescript
  import { IDocument, DocumentsService } from '../../services/documentsService';
  ```

2. <span data-ttu-id="b63c5-250">Обновите метод `render`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-250">Update the `render` method by using the following code:</span></span>

  ```typescript
  export default class RecentDocumentWebPart extends BaseClientSideWebPart<IRecentDocumentWebPartProps> {
    // ...
    public render(): void {
      this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'document');

      DocumentsService.getRecentDocument()
        .then((document: IDocument): void => {
          const element: React.ReactElement<IRecentDocumentProps> = React.createElement(
            RecentDocument,
            {
              document: document
            }
          );

          this.context.statusRenderer.clearLoadingIndicator(this.domElement);
          ReactDom.render(element, this.domElement);
        });
    }
    // ...
  }
  ```

3. <span data-ttu-id="b63c5-251">Убедитесь, что обе веб-части работают надлежащим образом. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b63c5-251">Confirm that both web parts are working correctly by running the following command from a command prompt in your project folder:</span></span>

  ```sh
  gulp serve
  ```

  <br/>

  ![Веб-части Recent Document (Последний документ) и Recent Documents (Последние документы) с информацией о недавно измененных документах](../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="share-data-between-web-parts"></a><span data-ttu-id="b63c5-253">Совместное использование данных разными веб-частями</span><span class="sxs-lookup"><span data-stu-id="b63c5-253">Share data between web parts</span></span>

<span data-ttu-id="b63c5-254">Теперь, когда обе веб-части загружают свои данные с помощью службы данных, необходимо расширить службу данных так, чтобы она загружала данные только один раз и использовала их для обеих веб-частей.</span><span class="sxs-lookup"><span data-stu-id="b63c5-254">Now that both web parts use the data service to load their data, the next step is to extend the data service so that it loads the data only once and reuses it for both web parts.</span></span>

1. <span data-ttu-id="b63c5-255">Откройте в редакторе кода файл **./src/services/documentsService/DocumentsService.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="b63c5-255">In the code editor, open the **./src/services/documentsService/DocumentsService.ts** file, and paste the following code:</span></span>

  ```typescript
  import { IDocument } from './IDocument';

  export class DocumentsService {
      private static documents: IDocument[] = [
          {
              title: 'Proposal for Jacksonville Expansion Ad Campaign',
              url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&file=Jacksonville%20Ad%20Campaign%20(draft).docx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BCBF65183-0378-485B-AB67-791E0FC81D72%7D&docId=17592965474834&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 25 2017',
                  actorName: 'Miriam Graham',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'Customer Feedback for ZT1000',
              url: 'https://contoso-my.sharepoint.com/personal/miriamg_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&file=Customer%20Feedback%20for%20ZT1000.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=ca6fa69c-347d-4c07-886c-67105dc5a357&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7B5449CE24-BFB7-442E-843D-E0C86CEB71CC%7D&docId=17592968714930&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 23 2017',
                  actorName: 'Miriam Graham',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=miriamg@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'Asia Q3 Marketing Overview',
              url: 'https://contoso-my.sharepoint.com/personal/alexw_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&file=Asia%20Q3%20Marketing%20Overview%20Beta.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=18231116-2bf0-474c-93ee-eb362681b293&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BFD077A94-AB7D-45F9-A810-36229E518A94%7D&docId=17592969984791&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 23 2017',
                  actorName: 'Alex Wilber',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'Trey Research Business Development Plan',
              url: 'https://contoso.sharepoint.com/sites/contoso/Resources/Document%20Center/_layouts/15/WopiFrame.aspx?sourcedoc=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&file=Trey%20Research%20Business%20Development%20Plan.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=923a6ce1-7b67-4bd0-a59f-89d37f233804&guidWeb=c12486eb-661c-46c7-baba-073a8a45b610&guidFile=%7B743A6C44-D3F8-4ECC-A1B7-EA9844911314%7D&docId=265998788&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, January 15 2017',
                  actorName: 'Alex Wilber',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=alexw@contoso.onmicrosoft.com&size=L'
              }
          },
          {
              title: 'XT1000 Marketing Analysis',
              url: 'https://contoso-my.sharepoint.com/personal/henriettam_contoso_onmicrosoft_com/_layouts/15/WopiFrame.aspx?sourcedoc=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&file=XT1000%20Marketing%20Analysis.pptx&action=view&DefaultItemOpen=1',
              imageUrl: 'https://contoso-my.sharepoint.com/_layouts/15/getpreview.ashx?guidSite=b187e1dd-7687-49e0-87ff-6250e61e56ac&guidWeb=237a3f3f-59a4-46e8-b0a8-6effd78bd327&guidFile=%7BA8B9F935-E5A1-47AD-B052-D5ED30E682AB%7D&docId=17592963604695&metadataToken=&clienttype=DelveWebHomeFeed',
              iconUrl: '',
              activity: {
                  title: 'Modified, December 15 2016',
                  actorName: 'Henrietta Mueller',
                  actorImageUrl: 'https://contoso-my.sharepoint.com/_vti_bin/DelveApi.ashx/people/profileimage?userId=henriettam@contoso.onmicrosoft.com&size=L'
              }
          }
      ];

      public static getRecentDocument(): Promise<IDocument> {
          return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
              DocumentsService.ensureRecentDocuments()
                  .then((recentDocuments: IDocument[]): void => {
                      resolve(recentDocuments[0]);
                  });
          });
      }

      public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
          return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
              DocumentsService.ensureRecentDocuments()
                  .then((recentDocuments: IDocument[]): void => {
                      resolve(recentDocuments.slice(startFrom, startFrom + 3));
                  });
          });
      }

      private static ensureRecentDocuments(): Promise<IDocument[]> {
          return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
              if ((window as any).loadedData) {
                  // data already loaded. reuse
                  resolve((window as any).loadedData);
                  return;
              }

              if ((window as any).loadingData) {
                  // data is being loaded. wait a moment and try again
                  window.setTimeout((): void => {
                      DocumentsService.ensureRecentDocuments()
                          .then((recentDocuments: IDocument[]): void => {
                              resolve(recentDocuments);
                          });
                  }, 100);
              }
              else {
                  (window as any).loadingData = true;
                  window.setTimeout((): void => {
                      // store the data for subsequent requests and resolve the Promise
                      (window as any).loadedData = DocumentsService.documents;
                      (window as any).loadingData = false;
                      resolve((window as any).loadedData);
                  }, 300);
              }
          });
      }
  }
  ```

  <br/>

  <span data-ttu-id="b63c5-256">Когда веб-часть впервые вызывает службу данных, чтобы загрузить свои данные, служба задает для глобальной переменной `loadingData` значение `true`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-256">The first time a web part calls the data service to load its data, the service sets the `loadingData` global variable to `true`.</span></span> <span data-ttu-id="b63c5-257">Это означает, что в данный момент данные загружаются.</span><span class="sxs-lookup"><span data-stu-id="b63c5-257">This indicates that data is currently being loaded.</span></span> <span data-ttu-id="b63c5-258">Это необходимо, чтобы данные не загружались несколько раз, например если другая веб-часть запросит загрузку данных, в то время как изначальный запрос еще не был выполнен.</span><span class="sxs-lookup"><span data-stu-id="b63c5-258">This is required to prevent data from being loaded multiple times should, for instance, another web part request loading its data while the initial request to load data has not yet completed.</span></span> <span data-ttu-id="b63c5-259">В этом примере данные загружаются из статического набора данных, но вы легко можете изменить реализацию, чтобы данные загружались из библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b63c5-259">In this example, the data is loaded from a static data set, but you could easily change the implementation to load the data from a SharePoint document library.</span></span>

  <span data-ttu-id="b63c5-260">После загрузки данные хранятся в глобальной переменной `loadedData`.</span><span class="sxs-lookup"><span data-stu-id="b63c5-260">After the data is loaded, it is stored in the `loadedData` global variable.</span></span> <span data-ttu-id="b63c5-261">Для переменной `loadingData` задается значение `false`, а обещание разрешается с помощью полученных данных.</span><span class="sxs-lookup"><span data-stu-id="b63c5-261">The value of the `loadingData` variable is set to `false` and the promise is resolved with the retrieved data.</span></span> <span data-ttu-id="b63c5-262">В следующий раз, когда веб-часть запросит свои данные, служба данных вернет ранее загруженные данные, не совершая никаких дополнительных запросов к удаленным API.</span><span class="sxs-lookup"><span data-stu-id="b63c5-262">The next time a web part requests its data, the data service returns the data loaded previously, eliminating any additional requests to the remote APIs.</span></span>

3. <span data-ttu-id="b63c5-263">Убедитесь, что обе веб-части работают надлежащим образом. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b63c5-263">Confirm that both web parts are working correctly by running the following command from a command prompt in your project folder:</span></span>

  ```sh
  gulp serve
  ```

  <br/>

  ![Веб-части Recent Document (Последний документ) и Recent Documents (Последние документы) с информацией о недавно измененных документах](../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

4. <span data-ttu-id="b63c5-265">Если добавить операторы ведения журнала в разных частях метода `DocumentsService.ensureRecentDocuments`, вы увидите, что данные загружаются один раз, после чего используются повторно.</span><span class="sxs-lookup"><span data-stu-id="b63c5-265">If you were to add logging statements in the different parts of the `DocumentsService.ensureRecentDocuments` method, you would see that the data is loaded once and reused for the second web part.</span></span>

  ![Консоль разработчика с различными операторами ведения журнала в Microsoft Edge](../../../images/tutorial-sharingdata-console-log.png)

## <a name="see-also"></a><span data-ttu-id="b63c5-267">См. также</span><span class="sxs-lookup"><span data-stu-id="b63c5-267">See also</span></span>

- [<span data-ttu-id="b63c5-268">Использование одних данных в разных клиентских веб-частях</span><span class="sxs-lookup"><span data-stu-id="b63c5-268">Share data between client-side web parts</span></span>](./share-data-between-web-parts.md)
