# <a name="share-data-between-web-parts-using-a-global-variable-tutorial"></a><span data-ttu-id="0037f-101">Совместное использование данных разными веб-частями с помощью глобальной переменной (руководство)</span><span class="sxs-lookup"><span data-stu-id="0037f-101">Share Data Between Web Parts Using a Global Variable (Tutorial)</span></span>

> <span data-ttu-id="0037f-102">Примечание. Эта статья еще не была проверена на общедоступной версии SPFx, поэтому у вас могут возникнуть трудности при использовании последнего выпуска.</span><span class="sxs-lookup"><span data-stu-id="0037f-102">Note: This article has not yet been verified with the SPFx GA version, so you might have challenges making this work as described using the latest release.</span></span>

<span data-ttu-id="0037f-p101">При создании клиентских веб-частей можно загрузить данные один раз и повторно использовать их в разных веб-частях. Это ускорит загрузку страниц и уменьшит нагрузку на сеть. В этом пошаговом руководстве показано, как веб-части могут совместно использовать данные с помощью глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="0037f-p101">When building client-side web parts, loading data once and reusing it across different web parts will help improve the performance of your pages and decrease the load on your network. This tutorial illustrates step-by-step how to share data between web parts using a global variable.</span></span>

> <span data-ttu-id="0037f-105">**Примечание.** Прежде чем выполнять действия, описанные в этой статье, [настройте среду разработки клиентских веб-частей для SharePoint](../../set-up-your-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0037f-105">**Note:** Before following the steps in this article, be sure to [set up your SharePoint client-side web part development environment](../../set-up-your-development-environment).</span></span>

## <a name="prepare-the-project"></a><span data-ttu-id="0037f-106">Подготовка проекта</span><span class="sxs-lookup"><span data-stu-id="0037f-106">Prepare the Project</span></span>

### <a name="create-a-new-project"></a><span data-ttu-id="0037f-107">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="0037f-107">Create a New Project</span></span>

<span data-ttu-id="0037f-108">С помощью командной строки создайте папку для проекта:</span><span class="sxs-lookup"><span data-stu-id="0037f-108">Using a command prompt, create a new folder for your project:</span></span>

```sh
md react-recentdocuments
```

<span data-ttu-id="0037f-109">Перейдите в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="0037f-109">Go into the project folder:</span></span>

```sh
cd react-recentdocuments
```

<span data-ttu-id="0037f-110">В папке проекта запустите генератор Yeoman для SharePoint Framework, чтобы сформировать шаблон проекта на платформе SharePoint Framework:</span><span class="sxs-lookup"><span data-stu-id="0037f-110">In the project folder, run the SharePoint Framework Yeoman generator to scaffold a new SharePoint Framework project:</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="0037f-111">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="0037f-111">When prompted, use the following values:</span></span>

- <span data-ttu-id="0037f-112">**WebPart** в качестве типа создаваемого клиентского компонента;</span><span class="sxs-lookup"><span data-stu-id="0037f-112">**WebPart** as the type of client-side component to create.</span></span>
- <span data-ttu-id="0037f-113">**react-recentdocuments** в качестве имени решения;</span><span class="sxs-lookup"><span data-stu-id="0037f-113">**react-recentdocuments** as your solution name.</span></span>
- <span data-ttu-id="0037f-114">**Use the current folder** (Использовать текущую папку) в качестве расположения файлов;</span><span class="sxs-lookup"><span data-stu-id="0037f-114">**Use the current folder** for the location to place the files.</span></span>
- <span data-ttu-id="0037f-115">**Recent documents** (Последние документы) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="0037f-115">**Recent documents** as your web part name.</span></span>
- <span data-ttu-id="0037f-116">**Shows recently modified documents** (Показывает недавно измененные документы) в качестве описания веб-части;</span><span class="sxs-lookup"><span data-stu-id="0037f-116">**Shows recently modified documents** as your web part description.</span></span>
- <span data-ttu-id="0037f-117">**React** в качестве используемой платформы.</span><span class="sxs-lookup"><span data-stu-id="0037f-117">**React** as the framework to use.</span></span>

![Генератор Yeoman для платформы SharePoint Framework с параметрами по умолчанию](../../../../images/tutorial-sharingdata-yo-sharepoint-recent-documents.png)

<span data-ttu-id="0037f-p102">Когда шаблон будет сформирован, откройте папку проекта в редакторе кода. В этой статье инструкции и снимки экрана основаны на Visual Studio Code, но вы можете использовать любой редактор.</span><span class="sxs-lookup"><span data-stu-id="0037f-p102">Once the scaffolding completes, open your project folder in your code editor. This article uses Visual Studio Code in the steps and screenshots, but you can use any editor you prefer.</span></span>

![Проект SharePoint Framework, открытый в Visual Studio Code](../../../../images/tutorial-sharingdata-vscode.png)

## <a name="show-the-recently-modified-documents"></a><span data-ttu-id="0037f-122">Отображение недавно измененных документов</span><span class="sxs-lookup"><span data-stu-id="0037f-122">Show the Recently Modified Documents</span></span>

<span data-ttu-id="0037f-123">Веб-часть Recent documents (Последние документы) показывает сведения о последних измененных документах в виде карточек, используя Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="0037f-123">The Recent documents web part shows information about the most recently modified documents displayed as cards using the Office UI Fabric.</span></span>

![Веб-часть Recent documents (Последние документы) с тремя небольшими карточками документов, представляющими три последних измененных документа](../../../../images/tutorial-sharingdata-recent-documents.png)

### <a name="remove-the-standard-description-property"></a><span data-ttu-id="0037f-125">Удаление стандартного свойства _description_</span><span class="sxs-lookup"><span data-stu-id="0037f-125">Remove the Standard _description_ Property</span></span>

<span data-ttu-id="0037f-p103">Для начала удалите стандартное свойство `description` из интерфейса `IRecentDocumentsWebPartProps`. В редакторе кода откройте файл **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p103">Start by removing the standard `description` property from the `IRecentDocumentsWebPartProps` interface. In the code editor, open the **./src/webparts/recentDocuments/IRecentDocumentsWebPartProps.ts** file and paste the following code:</span></span>

```ts
export interface IRecentDocumentsWebPartProps {
}
```

<span data-ttu-id="0037f-p104">Удалите стандартное свойство `description` из манифеста веб-части. Откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json** и удалите из свойства `properties` свойство `description`:</span><span class="sxs-lookup"><span data-stu-id="0037f-p104">Remove the standard `description` property from the web part manifest. Open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.manifest.json** file, and from the `properties` property, remove the `description` property:</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",

  "id": "7a7e3aa9-5d8a-4155-936b-0b0e06e9ca11",
  "alias": "RecentDocumentsWebPart",
  "componentType": "WebPart",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

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

<span data-ttu-id="0037f-p105">Наконец удалите стандартное свойство `description` из веб-части. Откройте в редакторе кода файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Замените метод `render` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p105">Finally, remove the standard `description` property from the web part. In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Replace its `render` method with the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-133">Затем замените метод `getPropertyPaneConfiguration` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-133">Then, replace its `getPropertyPaneConfiguration` method with the following code:</span></span>

```ts
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

### <a name="create-the-idocumentactivity-interface"></a><span data-ttu-id="0037f-134">Создание интерфейса IDocumentActivity</span><span class="sxs-lookup"><span data-stu-id="0037f-134">Create the IDocumentActivity Interface</span></span>

<span data-ttu-id="0037f-135">В папке **./src/webparts/recentDocuments** создайте файл с именем **IDocumentActivity.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-135">In the **./src/webparts/recentDocuments** folder, create a new file named **IDocumentActivity.ts** and paste the following code:</span></span>

```ts
export interface IDocumentActivity {
    title: string;
    actorName: string;
    actorImageUrl: string;
}
```

<span data-ttu-id="0037f-136">Этот интерфейс используется для отображения сведений о действиях с определенным документом на карточке.</span><span class="sxs-lookup"><span data-stu-id="0037f-136">This interface is used to display the activity information of a particular document on a card.</span></span>

### <a name="create-the-idocument-interface"></a><span data-ttu-id="0037f-137">Создание интерфейса IDocument</span><span class="sxs-lookup"><span data-stu-id="0037f-137">Create the IDocument Interface</span></span>

<span data-ttu-id="0037f-138">В папке **./src/webparts/recentDocuments** создайте файл с именем **IDocument.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-138">In the **./src/webparts/recentDocuments** folder, create a new file named **IDocument.ts** and paste the following code:</span></span>

```ts
import { IDocumentActivity } from './IDocumentActivity';

export interface IDocument {
    title: string;
    url: string;
    imageUrl: string;
    iconUrl: string;
    activity: IDocumentActivity;
}
```

<span data-ttu-id="0037f-139">Этот интерфейс представляет документ со всей необходимой информацией для отображения документа в качестве карточки.</span><span class="sxs-lookup"><span data-stu-id="0037f-139">This interface represents a document with all information necessary to display the document as a card.</span></span>

### <a name="show-recent-documents-in-the-recentdocuments-react-component"></a><span data-ttu-id="0037f-140">Отображение последних документов в компоненте React RecentDocuments</span><span class="sxs-lookup"><span data-stu-id="0037f-140">Show Recent Documents in the RecentDocuments React Component</span></span>

<span data-ttu-id="0037f-p106">Добавьте свойство **documents** к интерфейсу **IRecentDocumentsProps**. В редакторе кода откройте файл **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p106">Add the **documents** property to the **IRecentDocumentsProps** interface. In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file, and paste the following code:</span></span>

```ts
import { IDocument } from '../IDocument';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

<span data-ttu-id="0037f-143">В редакторе кода откройте файл **./src/webparts/recentDocuments/components/RecentDocuments.tsx** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-143">In the code editor, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and paste the following code:</span></span>

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

<span data-ttu-id="0037f-p107">Для начала компонент просматривает документы, переданные с помощью свойства `documents`. Для каждого документа он создает [карточку документа Office UI Fabric](https://dev.office.com/fabric#/components/documentcard), заполняя ее свойства соответствующими сведениями о конкретном документе. После создания карточек для всех документов компонент добавляет их в основной текст и возвращает полную разметку.</span><span class="sxs-lookup"><span data-stu-id="0037f-p107">First, the component iterates through the documents passed using its `documents` property. For each document, it builds an [Office UI Fabric Document Card](https://dev.office.com/fabric#/components/documentcard) filling its properties with the relevant information about that particular document. Finally, when cards for all documents have been built, the component adds them to its body and returns the complete markup.</span></span>

### <a name="load-the-information-about-the-recent-documents"></a><span data-ttu-id="0037f-147">Загрузка сведений о последних документах</span><span class="sxs-lookup"><span data-stu-id="0037f-147">Load the Information About the Recent Documents</span></span>

<span data-ttu-id="0037f-p108">В этом примере сведения о недавно измененных документах загружаются из статического набора данных. Однако вы легко можете изменить эту реализацию, чтобы данные загружались из библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0037f-p108">In this example, the information about the recently modified documents is loaded from a static data set. You could, however, easily change this implementation to load the data from a SharePoint document library instead.</span></span>

<span data-ttu-id="0037f-p109">В редакторе кода откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Добавьте оператор импорта для интерфейса `IDocument` после других операторов импорта в начале файла, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p109">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Add an import statement for the `IDocument` interface under the other import statements at the top of the file using the following code:</span></span>

```ts
import { IDocument } from './IDocument';
```

<span data-ttu-id="0037f-152">В классе `RecentDocumentsWebPart` добавьте новую частную переменную с именем `documents`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-152">In the `RecentDocumentsWebPart` class, add a new private variable named `documents` using the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-153">Измените метод `render`, чтобы он загружал и отображал сведения о недавно измененных документах:</span><span class="sxs-lookup"><span data-stu-id="0037f-153">Change the `render` method to load and render the information about the recently modified documents:</span></span>

```ts
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

<span data-ttu-id="0037f-154">Убедитесь, что веб-часть работает надлежащим образом и отображает сведения о трех последних измененных документах. Для этого с помощью командной строки выполните в каталоге проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0037f-154">Verify that the web part is working correctly and shows information about the three most recently modified documents by running the following command from a command prompt in your project directory:</span></span>

```sh
gulp serve
```

<span data-ttu-id="0037f-155">Добавьте веб-часть Recent Documents (Последние документы) на холст рабочего места SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0037f-155">In the SharePoint workbench add the Recent Documents web part to the canvas.</span></span>

![Веб-часть Recent Documents (Последние документы) с тремя недавно измененными документами в виде карточек документов](../../../../images/tutorial-sharingdata-recent-documents.png)

## <a name="show-the-most-recently-modified-document"></a><span data-ttu-id="0037f-157">Отображение последнего измененного документа</span><span class="sxs-lookup"><span data-stu-id="0037f-157">Show the Most Recently Modified Document</span></span>

<span data-ttu-id="0037f-158">В веб-части Recent document (Последний документ) отображаются сведения о последнем измененном документе.</span><span class="sxs-lookup"><span data-stu-id="0037f-158">The Recent document web part shows information about the most recently modified document.</span></span>

![Веб-часть Recent document (Последний документ) с одной большой карточкой документа, содержащей сведения о последнем измененном документе](../../../../images/tutorial-sharingdata-recent-document.png)

### <a name="add-the-second-web-part"></a><span data-ttu-id="0037f-160">Добавление второй веб-части</span><span class="sxs-lookup"><span data-stu-id="0037f-160">Add the Second Web Part</span></span>

<span data-ttu-id="0037f-161">Чтобы продемонстрировать совместное использование данных разными веб-частями, добавьте к проекту вторую веб-часть.</span><span class="sxs-lookup"><span data-stu-id="0037f-161">To illustrate sharing data between web parts, add a second web part to the project.</span></span>

<span data-ttu-id="0037f-162">С помощью командной строки запустите в папке проекта генератор Yeoman для SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="0037f-162">Using a command prompt in the project folder, run the SharePoint Framework Yeoman generator.</span></span>

```sh
yo @microsoft/sharepoint
```

<span data-ttu-id="0037f-163">Когда появится соответствующий запрос, укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="0037f-163">When prompted, enter the following values:</span></span>


- <span data-ttu-id="0037f-164">**WebPart** в качестве типа создаваемого клиентского компонента;</span><span class="sxs-lookup"><span data-stu-id="0037f-164">**WebPart** as the type of client-side component to create.</span></span>
- <span data-ttu-id="0037f-165">**Recent document** (Последний документ) в качестве имени веб-части;</span><span class="sxs-lookup"><span data-stu-id="0037f-165">**Recent document** as your web part name.</span></span>
- <span data-ttu-id="0037f-166">**Shows information about the most recently modified document** (Показывает сведения о последнем измененном документе) в качестве описания веб-части.</span><span class="sxs-lookup"><span data-stu-id="0037f-166">**Shows information about the most recently modified document** as your web part description.</span></span>

![Генератор Yeoman для SharePoint Framework со сведениями для формирования второй веб-части](../../../../images/tutorial-sharingdata-yo-sharepoint-recent-document.png)

### <a name="remove-the-standard-description-property"></a><span data-ttu-id="0037f-168">Удаление стандартного свойства _description_</span><span class="sxs-lookup"><span data-stu-id="0037f-168">Remove the Standard _description_ Property</span></span>

<span data-ttu-id="0037f-p110">Для начала удалите свойство `description` из интерфейса `IRecentDocumentWebPartProps`. В редакторе кода откройте файл **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p110">Start by removing the `description` property from the `IRecentDocumentWebPartProps` interface. In the code editor, open the **./src/webparts/recentDocument/IRecentDocumentWebPartProps.ts** file and paste the following code:</span></span>

```ts
export interface IRecentDocumentWebPartProps {
}
```

<span data-ttu-id="0037f-p111">Удалите стандартное свойство `description` из манифеста веб-части. Откройте файл **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json** и удалите из свойства `properties` свойство `description`:</span><span class="sxs-lookup"><span data-stu-id="0037f-p111">Remove the standard `description` property from the web part manifest. Open the **./src/webparts/recentDocument/RecentDocumentWebPart.manifest.json** file, and from the `properties` property, remove the `description` property:</span></span>

```json
{
  "$schema": "https://dev.office.com/json-schemas/spfx/client-side-web-part-manifest.schema.json",

  "id": "71a6f643-1ac1-47ee-a9f1-502ef52f26d4",
  "alias": "RecentDocumentWebPart",
  "componentType": "WebPart",

  // The "*" signifies that the version should be taken from the package.json
  "version": "*",
  "manifestVersion": 2,

  // If true, the component can only be installed on sites where Custom Script is allowed.
  // Components that allow authors to embed arbitrary script code should set this to true.
  // https://support.office.com/en-us/article/Turn-scripting-capabilities-on-or-off-1f2c515f-5d7e-448a-9fd7-835da935584f
  "requiresCustomScript": false,

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

<span data-ttu-id="0037f-p112">Наконец, удалите стандартное свойство `description` из области свойств веб-части. Откройте в редакторе кода файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Замените метод `render` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p112">Finally, remove the standard `description` property from the web part property pane. In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Replace its `render` method with the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-176">Затем замените метод `getPropertyPaneConfiguration` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-176">Next, replace its `getPropertyPaneConfiguration` method with the following code:</span></span>

```ts
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

### <a name="reuse-the-idocument-and-idocumentactivity-interfaces"></a><span data-ttu-id="0037f-177">Повторное использование интерфейсов _IDocument_ и _IDocumentActivity_</span><span class="sxs-lookup"><span data-stu-id="0037f-177">Reuse the _IDocument_ and _IDocumentActivity_ Interfaces</span></span>

<span data-ttu-id="0037f-p113">Веб-части Recent document (Последний документ) и Recent documents (Последние документы) отображают сведения о последнем измененном документе по-разному, но они используют одну и ту же структуру данных для представления документа. Вместо того чтобы дублировать интерфейсы `IDocument` и `IDocumentActivity`, вы можете использовать их в обеих веб-частях.</span><span class="sxs-lookup"><span data-stu-id="0037f-p113">The Recent document web part displays information about the most recently modified document in a different way than the Recent documents web part, but both web parts use the same data structure representing a document. Instead of duplicating the `IDocument` and `IDocumentActivity` interfaces, you can reuse them across both web parts.</span></span>

<span data-ttu-id="0037f-180">В Visual Studio Code откройте область обозревателя и в папке **./src/webparts/recentDocuments** переместите файлы **IDocument.ts** и **IDocumentActivity.ts** на один уровень выше, в папку **./src/webparts**.</span><span class="sxs-lookup"><span data-stu-id="0037f-180">In Visual Studio Code, activate the Explorer pane, and from the **./src/webparts/recentDocuments** folder, move the **IDocument.ts** and **IDocumentActivity.ts** files one level up, to the **./src/webparts** folder.</span></span>

![Область обозревателя Visual Studio Code с выделенными файлами IDocument.ts и IDocumentActivity.ts](../../../../images/tutorial-sharingdata-interfaces.png)

#### <a name="update-references-to-the-moved-files"></a><span data-ttu-id="0037f-182">Обновление ссылок на перемещенные файлы</span><span class="sxs-lookup"><span data-stu-id="0037f-182">Update References to the Moved Files</span></span>

<span data-ttu-id="0037f-183">Переместив файлы в другую папку проекта, необходимо обновить пути в ссылках на них.</span><span class="sxs-lookup"><span data-stu-id="0037f-183">Having moved the files to another location in your project, you need to update the paths where they're referenced.</span></span>

<span data-ttu-id="0037f-184">В редакторе кода откройте файл **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="0037f-184">In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file and change its code to:</span></span>

```ts
import { IDocument } from '../../IDocument';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

<span data-ttu-id="0037f-185">Затем откройте файл **./src/webparts/recentDocuments/components/RecentDocuments.tsx** и замените оператор `import` в интерфейсе `IDocument` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-185">Next, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and update the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../IDocument';
```

<span data-ttu-id="0037f-186">Наконец, откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** и замените оператор `import` в интерфейсе `IDocument` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-186">Finally, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file and update the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../IDocument';
```

### <a name="show-the-most-recent-document-in-the-recentdocument-react-component"></a><span data-ttu-id="0037f-187">Отображение последнего документа в компоненте React RecentDocument</span><span class="sxs-lookup"><span data-stu-id="0037f-187">Show the Most Recent Document in the RecentDocument React Component</span></span>

<span data-ttu-id="0037f-p114">Добавьте свойство `document` к интерфейсу `IRecentDocumentProps`. В редакторе кода откройте файл **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p114">Add the `document` property to the `IRecentDocumentProps` interface. In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file, and paste the following code:</span></span>

```ts
import { IDocument } from '../../IDocument';

export interface IRecentDocumentProps {
  document: IDocument;
}
```

<span data-ttu-id="0037f-190">В редакторе кода откройте файл **./src/webparts/recentDocument/components/RecentDocument.tsx** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-190">In the code editor, open the **./src/webparts/recentDocument/components/RecentDocument.tsx** file and paste the following code:</span></span>

```tsx
import * as React from 'react';
import {
  DocumentCard,
  DocumentCardPreview,
  DocumentCardTitle,
  DocumentCardActivity
} from 'office-ui-fabric-react/lib/DocumentCard';
import { ImageFit } from 'office-ui-fabric-react/lib/Image';
import { IDocument } from '../../IDocument';
import styles from './RecentDocument.module.scss';
import { IRecentDocumentProps } from './IRecentDocumentProps';

export default class RecentDocument extends React.Component<IRecentDocumentProps, {}> {
  public render(): React.ReactElement<IRecentDocumentProps> {
    const document: IDocument = this.props.document;

    return (
      <div className={styles.recentDocument}>
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

<span data-ttu-id="0037f-191">Компонент React `RecentDocument` использует сведения о последнем измененном документе, переданные в свойстве `document`, и отображает с их помощью карточки документа Office UI Fabric.</span><span class="sxs-lookup"><span data-stu-id="0037f-191">The `RecentDocument` React component uses the information about the most recently modified document passed in the `document` property and uses it to render an Office UI Fabric Document Card.</span></span>

### <a name="load-the-information-about-the-recent-document"></a><span data-ttu-id="0037f-192">Загрузка сведений о последнем документе</span><span class="sxs-lookup"><span data-stu-id="0037f-192">Load the Information About the Recent Document</span></span>

<span data-ttu-id="0037f-p115">В этом примере сведения о последнем измененном документе загружаются из статического набора данных. Однако вы легко можете изменить эту реализацию, чтобы данные загружались из библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0037f-p115">In this example, the information about the most recently modified document is loaded from a static data set. You could, however, easily change this implementation to load the data from a SharePoint document library instead.</span></span>

<span data-ttu-id="0037f-p116">В редакторе кода откройте файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Добавьте оператор импорта для интерфейса `IDocument` после других операторов импорта в начале файла, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-p116">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Add an import statement for the `IDocument` interface under the other import statements at the top of the file using the following code:</span></span>

```ts
import { IDocument } from '../IDocument';
```

<span data-ttu-id="0037f-197">В классе `RecentDocumentWebPart` добавьте новую частную переменную с именем `document`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-197">In the `RecentDocumentWebPart` class, add a new private variable named `document` using the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-198">Измените метод `render`, чтобы он загружал и отображал сведения о последнем измененном документе:</span><span class="sxs-lookup"><span data-stu-id="0037f-198">Change the `render` method to load and render the information about the most recently modified document:</span></span>

```ts
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

<span data-ttu-id="0037f-199">Убедитесь, что веб-часть работает надлежащим образом и отображает сведения о последнем измененном документе. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0037f-199">Verify that the web part is working correctly and shows information about the most recently modified document, by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

<span data-ttu-id="0037f-200">Добавьте веб-часть Recent document (Последний документ) на холст рабочего места SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0037f-200">In the SharePoint workbench add the Recent document web part to the canvas.</span></span>

![Веб-часть Recent document (Последний документ) с карточкой документа, содержащей сведения о последнем измененном документе](../../../../images/tutorial-sharingdata-recent-document.png)

<span data-ttu-id="0037f-p117">Текущая реализация — типичный пример независимой разработки двух веб-частей. Если они обе располагаются на одной странице и загружают данные из SharePoint, то для получения похожих сведений приходится выполнять два отдельных запроса. Если в тот или иной момент вам потребуется изменить источник, из которого загружаются данные о недавно измененных документах, то придется обновлять обе веб-части. Чтобы ускорить загрузку страницы и упростить работу с кодом веб-части, вы можете централизовать логику получения данных и сделать однажды полученные данные доступными обеим веб-частям.</span><span class="sxs-lookup"><span data-stu-id="0037f-p117">The current implementation is a typical example of two web parts being developed independently. If they were both placed on the same page and were loading data from SharePoint, they would execute two separate requests to retrieve similar information. If, at some point, you had to change where the information about the recently modified documents is loaded from, you would have to update both web parts. To improve the performance of loading the page and simplify maintaining the web part code, you can centralize the logic of retrieving the data and make the once retrieved data available to both web parts.</span></span>

## <a name="centralize-loading-data"></a><span data-ttu-id="0037f-206">Централизованная загрузка данных</span><span class="sxs-lookup"><span data-stu-id="0037f-206">Centralize Loading Data</span></span>

<span data-ttu-id="0037f-207">Чтобы централизовать загрузку сведений о недавно измененных документах, создайте службу, на которую будут ссылаться обе веб-части.</span><span class="sxs-lookup"><span data-stu-id="0037f-207">To centralize loading the information about recently modified documents, build a service that will be referenced by both web parts.</span></span>

### <a name="move-the-data-model-interfaces"></a><span data-ttu-id="0037f-208">Перемещение интерфейсов модели данных</span><span class="sxs-lookup"><span data-stu-id="0037f-208">Move the Data Model Interfaces</span></span>

<span data-ttu-id="0037f-p118">Создайте в папке проекта путь **./src/services/documentsService**. Переместите файлы **IDocument.ts** и **IDocumentActivity.ts** из папки **./src/webparts** в папку **./src/services/documentsService**.</span><span class="sxs-lookup"><span data-stu-id="0037f-p118">In the project folder create the **./src/services/documentsService** folder path. From the **./src/webparts** folder, move the **IDocument.ts** and **IDocumentActivity.ts** files to the **./src/services/documentsService** folder.</span></span>

![Файлы IDocument.ts и IDocumentActivity.ts, выделенные в области обозревателя Visual Studio Code](../../../../images/tutorial-sharingdata-interfaces-documentsservice.png)

### <a name="build-the-data-access-service"></a><span data-ttu-id="0037f-212">Создание службы доступа к данным</span><span class="sxs-lookup"><span data-stu-id="0037f-212">Build the Data Access Service</span></span>

<span data-ttu-id="0037f-213">В папке **./src/services/documentsService** создайте файл с именем **DocumentsService.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-213">In the **./src/services/documentsService** folder, create a new file named **DocumentsService.ts** and paste the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-p119">Класс `DocumentsService` — это пример службы, загружающей сведения о последних документах. В этом примере используется статический набор данных, но вы легко можете изменить его реализацию, чтобы данные загружались из библиотеки документов SharePoint. На этом этапе класс `DocumentsService` уже предоставляет центральную точку доступа к данным для всех веб-частей, но еще не сохраняет ранее загруженные данные. Эту возможность мы реализуем позже.</span><span class="sxs-lookup"><span data-stu-id="0037f-p119">The `DocumentsService` class is a sample service that loads information about recent documents. In this example, it uses a static data set, but you could easily change its implementation to load its data from a SharePoint document library. At this stage, the `DocumentsService` class offers a centralized point for all web parts to access their data, but it doesn't store the previously loaded data. You will implement that later in this tutorial.</span></span>

### <a name="create-a-barrel-for-the-service-files"></a><span data-ttu-id="0037f-218">Создание блока данных для системных файлов</span><span class="sxs-lookup"><span data-stu-id="0037f-218">Create a Barrel for the Service Files</span></span>

<span data-ttu-id="0037f-p120">Ссылаясь на файлы в проекте, вы указываете относительный путь. При изменении этого пути потребуется обновить все ссылки на соответствующий файл. Такие изменения очень вероятны на раннем этапе разработки, когда добавляются различные элементы, а окончательная структура проекта еще не определена. Во избежание частых изменений ссылок на файлы в проекте вы можете использовать блоки данных.</span><span class="sxs-lookup"><span data-stu-id="0037f-p120">When referencing files in a project you point to their relative path. Whenever that path changes, you have to update all references to the particular file. Such changes are very likely at the beginning of the project when the different elements are being added and the final project structure is unclear. To avoid frequent changes to file references in a project you can use barrels.</span></span>

<span data-ttu-id="0037f-p121">Блок данных — это контейнер, объединяющий ряд экспортированных объектов. С их помощью вы можете абстрагировать точное расположение файлов от других элементов проекта, использующих их.</span><span class="sxs-lookup"><span data-stu-id="0037f-p121">A barrel is a container that combines a number of exported objects. By using barrels you can abstract away the exact location of files from other elements in the project using them.</span></span>

<span data-ttu-id="0037f-225">В папке **./src/services/documentsService** создайте файл с именем **index.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-225">In the **./src/services/documentsService** folder create a new file named **index.ts** and paste the following code:</span></span>

```ts
export { IDocument } from './IDocument';
export { IDocumentActivity } from './IDocumentActivity';
export { DocumentsService } from './DocumentsService';
```

<span data-ttu-id="0037f-p122">После определения блока данных другие элементы проекта смогут ссылаться на любой из экспортированных типов по относительному пути к папке **./src/services/documentsService**, а не точному пути к отдельному файлу. Например, ссылка на интерфейс `IDocument` может быть такой:</span><span class="sxs-lookup"><span data-stu-id="0037f-p122">With this barrel defined, other elements in the project can reference any of the exported types using the relative path to the **./src/services/documentsService** folder instead of the exact path to the individual files. For example the `IDocument` interface can be referenced like this:</span></span>

```ts
import { IDocument } from '../services/documentsService';
```

<span data-ttu-id="0037f-228">а не такой:</span><span class="sxs-lookup"><span data-stu-id="0037f-228">instead of:</span></span>

```ts
import { IDocument } from '../services/documentsService/IDocument';
```

<span data-ttu-id="0037f-p123">Если в тот или иной момент вы решите, что предпочтительней переместить файл **IDocument.ts** во вложенную папку или объединить несколько файлов, изменить потребуется только путь к определению блока данных (**./src/services/documentsService/index.ts**). Все элементы проекта по-прежнему могут использовать тот же относительный путь к папке **documentsService**, чтобы ссылаться на интерфейс `IDocument`.</span><span class="sxs-lookup"><span data-stu-id="0037f-p123">If at some point you decided that it's better to move the **IDocument.ts** file to a subfolder or merge a few files together, the only thing that you would change is the path in the barrel definition (**./src/services/documentsService/index.ts**). All elements in the project could still use the exact same relative path to the **documentsService** folder to reference the `IDocument` interface.</span></span>

### <a name="update-references-to-the-moved-files-to-use-the-barrel"></a><span data-ttu-id="0037f-231">Обновление ссылок на перемещенные файлы для использования блока данных</span><span class="sxs-lookup"><span data-stu-id="0037f-231">Update References to the Moved Files to Use the Barrel</span></span>

<span data-ttu-id="0037f-p124">Так как вы переместили файлы **IDocument.ts** и **IDocumentActivity.ts** в другое расположение, необходимо обновить ссылки на них. Благодаря блокам данных после этого вам не придется менять эти ссылки.</span><span class="sxs-lookup"><span data-stu-id="0037f-p124">As you have moved the **IDocument.ts** and **IDocumentActivity.ts** files to another location, you have to update their references. Thanks to the barrel, this will be the last time that you will have to do this.</span></span>

#### <a name="update-references-in-the-recent-documents-web-part"></a><span data-ttu-id="0037f-234">Обновление ссылок в веб-части Recent documents (Последние документы)</span><span class="sxs-lookup"><span data-stu-id="0037f-234">Update References in the Recent Documents Web Part</span></span>

<span data-ttu-id="0037f-235">В редакторе кода откройте файл **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="0037f-235">In the code editor, open the **./src/webparts/recentDocuments/components/IRecentDocumentsProps.ts** file and change its code to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';

export interface IRecentDocumentsProps {
  documents: IDocument[];
}
```

<span data-ttu-id="0037f-236">Затем откройте файл **./src/webparts/recentDocuments/components/RecentDocuments.tsx** и замените оператор `import` в интерфейсе `IDocument` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-236">Next, open the **./src/webparts/recentDocuments/components/RecentDocuments.tsx** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';
```

<span data-ttu-id="0037f-237">Затем откройте файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** и замените оператор `import` в интерфейсе `IDocument` на следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-237">Then, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../services/documentsService';
```

#### <a name="update-references-in-the-recent-document-web-part"></a><span data-ttu-id="0037f-238">Обновление ссылок в веб-части Recent document (Последний документ)</span><span class="sxs-lookup"><span data-stu-id="0037f-238">Update References in the Recent Document Web Part</span></span>

<span data-ttu-id="0037f-239">В редакторе кода откройте файл **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** и измените его код на следующий:</span><span class="sxs-lookup"><span data-stu-id="0037f-239">In the code editor, open the **./src/webparts/recentDocument/components/IRecentDocumentProps.ts** file and change its code to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';

export interface IRecentDocumentProps {
  document: IDocument;
}
```

<span data-ttu-id="0037f-240">Затем откройте файл **./src/webparts/recentDocument/components/RecentDocument.tsx** и измените оператор `import` в интерфейсе `IDocument` на следующий:</span><span class="sxs-lookup"><span data-stu-id="0037f-240">Next, open the **./src/webparts/recentDocument/components/RecentDocument.tsx** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../../services/documentsService';
```

<span data-ttu-id="0037f-241">Затем откройте файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts** и замените оператор `import` в интерфейсе `IDocument` на следующий:</span><span class="sxs-lookup"><span data-stu-id="0037f-241">Then, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file and change the `import` statement of the `IDocument` interface to:</span></span>

```ts
import { IDocument } from '../../services/documentsService';
```

<span data-ttu-id="0037f-242">Убедитесь, что ваши изменения работают надлежащим образом. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0037f-242">Verify that your changes work as expected, by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

![Веб-части Recent document (Последний документ) и Recent documents (Последние документы) с информацией о недавно измененных документах](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="load-web-part-data-using-the-data-service"></a><span data-ttu-id="0037f-244">Загрузка данных веб-частей с помощью службы данных</span><span class="sxs-lookup"><span data-stu-id="0037f-244">Load Web Part Data Using the Data Service</span></span>

<span data-ttu-id="0037f-245">Когда служба данных будет готова, необходимо выполнить рефакторинг обеих веб-частей, чтобы они загружали свои данные с помощью службы данных.</span><span class="sxs-lookup"><span data-stu-id="0037f-245">With the data service ready, the next step is to refactor both web parts to use the data service to load their data.</span></span>

#### <a name="load-information-about-the-recently-modified-documents"></a><span data-ttu-id="0037f-246">Загрузка информации о недавно измененных документах</span><span class="sxs-lookup"><span data-stu-id="0037f-246">Load Information About the Recently Modified Documents</span></span>

<span data-ttu-id="0037f-p125">Откройте в редакторе кода файл **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts**. Замените оператор `import`, ссылающийся на интерфейс `IDocument`, на следующий оператор:</span><span class="sxs-lookup"><span data-stu-id="0037f-p125">In the code editor, open the **./src/webparts/recentDocuments/RecentDocumentsWebPart.ts** file. Expand the `import` statement referencing the `IDocument` interface to:</span></span>

```ts
import { IDocument, DocumentsService } from '../../services/documentsService';
```

<span data-ttu-id="0037f-249">Затем обновите метод `render`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-249">Next, update the `render` method using the following code:</span></span>

```ts
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

#### <a name="load-information-about-the-most-recently-modified-document"></a><span data-ttu-id="0037f-250">Загрузка информации о последних измененных документах</span><span class="sxs-lookup"><span data-stu-id="0037f-250">Load Information About the Most Recently Modified Document</span></span>

<span data-ttu-id="0037f-p126">Откройте в редакторе кода файл **./src/webparts/recentDocument/RecentDocumentWebPart.ts**. Замените оператор `import`, ссылающийся на интерфейс `IDocument`, на следующий оператор:</span><span class="sxs-lookup"><span data-stu-id="0037f-p126">In the code editor, open the **./src/webparts/recentDocument/RecentDocumentWebPart.ts** file. Expand the `import` statement referencing the `IDocument` interface to:</span></span>

```ts
import { IDocument, DocumentsService } from '../../services/documentsService';
```

<span data-ttu-id="0037f-253">Затем обновите метод `render`, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-253">Next, update the `render` method using the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-254">Убедитесь, что обе веб-части работают надлежащим образом. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0037f-254">Confirm that both web parts are working correctly by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

![Веб-части Recent document (Последний документ) и Recent documents (Последние документы) с информацией о недавно измененных документах](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

### <a name="share-data-between-web-parts"></a><span data-ttu-id="0037f-256">Совместное использование данных разными веб-частями</span><span class="sxs-lookup"><span data-stu-id="0037f-256">Share Data Between Web Parts</span></span>

<span data-ttu-id="0037f-257">Теперь, когда обе веб-части загружают свои данные с помощью службы данных, необходимо расширить службу данных так, чтобы она загружала данные только один раз и использовала их для обеих веб-частей.</span><span class="sxs-lookup"><span data-stu-id="0037f-257">Now that both web parts use the data service to load their data, the next step is to extend the data service so that it loads the data only once and reuses it for both web parts.</span></span>

<span data-ttu-id="0037f-258">Откройте в редакторе кода файл **./src/services/documentsService/DocumentsService.ts** и вставьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0037f-258">In the code editor, open the **./src/services/documentsService/DocumentsService.ts** file and paste the following code:</span></span>

```ts
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

<span data-ttu-id="0037f-p127">Когда веб-часть впервые вызывает службу данных, чтобы загрузить свои данные, служба задает для глобальной переменной `loadingData` значение `true`. Это означает, что в данный момент данные загружаются. Это необходимо, чтобы данные не загружались несколько раз, например если другая веб-часть также запросит загрузку данных, в то время как изначальный запрос на загрузку данных еще не был выполнен. В этом примере данные загружаются из статического набора данных, но вы легко можете изменить реализацию, чтобы данные загружались из библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0037f-p127">The first time a web part calls the data service to load its data, the service will set the `loadingData` global variable to `true`. This indicates that data is currently being loaded. This is required to prevent data from being loaded multiple times should, for instance, another web part request loading its data while the initial request to load data has not yet completed. In this example, the data is loaded from a static data set, but you could easily change the implementation to load the data from a SharePoint document library.</span></span>

<span data-ttu-id="0037f-p128">После загрузки данные хранятся в глобальной переменной `loadedData`. Для переменной `loadingData` задается значение `false`, а обещание разрешается с помощью полученных данных. В следующий раз, когда веб-часть запросит свои данные, служба данных вернет ранее загруженные данные, не совершая никаких дополнительных запросов к удаленным API.</span><span class="sxs-lookup"><span data-stu-id="0037f-p128">Once the data is loaded, it is stored in the `loadedData` global variable. The value of the `loadingData` variable is set to `false` and the promise is resolved with the retrieved data. The next time a web part requests its data, the data service will return the data loaded previously eliminating any additional requests to the remote APIs.</span></span>

<span data-ttu-id="0037f-266">Убедитесь, что обе веб-части работают надлежащим образом. Для этого с помощью командной строки выполните в папке проекта следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0037f-266">Confirm that both web parts are working correctly by running the following command from a command prompt in your project folder:</span></span>

```sh
gulp serve
```

![Веб-части Recent document (Последний документ) и Recent documents (Последние документы) с информацией о недавно измененных документах](../../../../images/tutorial-sharingdata-recent-document-recent-documents.png)

<span data-ttu-id="0037f-268">Если добавить операторы ведения журнала в разных частях метода `DocumentsService.ensureRecentDocuments`, вы увидите, что данные загружаются один раз, после чего используются повторно.</span><span class="sxs-lookup"><span data-stu-id="0037f-268">If you were to add logging statements in the different parts of the `DocumentsService.ensureRecentDocuments` method, you would see that the data is loaded once and reused for the second web part!</span></span>

![Консоль разработчика с различными операторами ведения журнала в Microsoft Edge](../../../../images/tutorial-sharingdata-console-log.png)

## <a name="see-also"></a><span data-ttu-id="0037f-270">См. также</span><span class="sxs-lookup"><span data-stu-id="0037f-270">See Also</span></span>

- [<span data-ttu-id="0037f-271">Совместное использование данных клиентскими веб-частями</span><span class="sxs-lookup"><span data-stu-id="0037f-271">Share Data Between Client-Side Web Parts</span></span>](./share-data-between-web-parts)
