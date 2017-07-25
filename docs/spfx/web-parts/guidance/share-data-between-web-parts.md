<span data-ttu-id="042fe-p120">Даже если несколько веб-частей на странице будут ссылаться на одну и ту же службу, ее пакет будет скачан только один раз, и SharePoint Framework создаст только один экземпляр этой службы на странице. Это удобный механизм для централизации обработки и хранения данных на странице. Хотя работа со службами SharePoint Framework сложнее, чем описанные ранее методы, у нее есть огромное преимущество: изоляция данных от компонентов на странице и поддержание их целостности.</span><span class="sxs-lookup"><span data-stu-id="042fe-p120">Even if there are multiple web parts on the page referencing the same service, its bundle will be downloaded only once and SharePoint Framework will create only one instance of the service on the page. This offers you a convenient mechanism for centralizing processing and storing data on a page. While working with SharePoint Framework services is more complex than the previously described approaches, it offers you a great benefit of isolating the data from other components on the page and better handling of its integrity.</span></span>

```ts
// ...
import { DocumentsService, IDocumentsService, IDocument } from 'react-recentdocuments-service';
import { ServiceScope } from '@microsoft/sp-core-library';

export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {
  private documentsService: IDocumentsService;

  protected onInit(): Promise<void> {
    return new Promise<void>((resolve: () => void, reject: (error: any) => void): void => {
      const serviceScope: ServiceScope = this.context.serviceScope.getParent();
      serviceScope.whenFinished((): void => {
        this.documentsService = serviceScope.consume(DocumentsService.serviceKey as any) as IDocumentsService;
        resolve();
      });
    });
  }

  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    this.documentsService.getRecentDocuments(this.properties.startFrom)
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

Даже если несколько веб-частей на странице будут ссылаться на одну и ту же службу, ее пакет будет скачан только один раз, и SharePoint Framework создаст только один экземпляр этой службы на странице. Это удобный механизм для централизации обработки и хранения данных на странице. Хотя работа со службами SharePoint Framework сложнее, чем описанные ранее методы, у нее есть огромное преимущество: изоляция данных от компонентов на странице и поддержание их целостности.
