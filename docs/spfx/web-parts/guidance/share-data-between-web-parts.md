# <a name="share-data-between-client-side-web-parts"></a>Совместное использование данных клиентскими веб-частями

> Примечание. Эта статья еще не была проверена на общедоступной версии SPFx, поэтому у вас могут возникнуть трудности при использовании последнего выпуска.

При создании клиентских веб-частей можно загрузить данные один раз и повторно использовать их в разных веб-частях. Это улучшит отображение страниц и уменьшит нагрузку на сеть. В статье описан ряд подходов, позволяющий обеспечить совместное использование данных разными веб-частями.

## <a name="why-share-data-between-web-parts"></a>Зачем разным веб-частям использовать одни и те же данные

Многие создаваемые веб-части используются вместе на одной странице. Если рассматривать каждую веб-часть как отдельный фрагмент страницы, придется многократно загружать похожие или даже одинаковые наборы данных на одной странице. При этом безо всякой необходимости замедлится загрузка страницы, а сетевой трафик увеличится.

![Две веб-части на одной странице, загружающие похожие наборы данных по отдельности](../../../../images/guidance-sharingdata-loading-data-separately.png)

Служба, отвечающая за загрузку данных, может выглядеть примерно так:

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            // [...] reach out to a remote API
            resolve(recentDocument);
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            // [...] reach out to a remote API
            resolve(recentDocuments);
        });
    }
}
```

Клиентские веб-части SharePoint Framework используют эту службу с помощью следующего кода:

```ts
import { DocumentsService, IDocument } from '../../services';

export default class RecentDocumentsWebPart extends BaseClientSideWebPart<IRecentDocumentsWebPartProps> {

  public render(): void {
    this.context.statusRenderer.displayLoadingIndicator(this.domElement, 'documents');

    DocumentsService.getRecentDocuments(this.properties.startFrom)
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

Чтобы сократить время загрузки страницы и уменьшить сетевой трафик, можно создать веб-части таким образом, чтобы данные загружались только один раз. Каждый раз, когда одна их веб-частей на странице запрашивает определенный набор данных, при возможности она будет использовать ранее загруженные данные.

## <a name="store-the-retrieved-data-in-a-globally-scoped-variable"></a>Хранение полученных данных в глобальной переменной

> Примечание. Как правило, не рекомендуется использовать глобальные переменные. Однако в целях демонстрации и простоты мы используем их в нашем примере кода. Решить эту проблему можно множеством способов, в том числе путем импорта и экспорта модулей с помощью понятий TypeScript.

Веб-части, созданные с помощью SharePoint Framework, изолированы в отдельных модулях. Поэтому одна веб-часть не может напрямую получить доступ к данным и свойствам, сохраненным другой веб-частью. Один из способов обойти такую особенность избежать такой проблемы и сделать данные, загруженные одной веб-частью, доступными для других веб-частей на странице — назначить полученные данные глобальной переменной.

Представленную выше службу доступа к данным можно изменить следующим образом:

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            if ((window as any).loadedData) {
                // data already loaded so reuse
                resolve((window as any).loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded, wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                // data not loaded yet, call the remote API,
                // store the data for subsequent requests, and resolve the Promise
                (window as any).loadedData = loadedData;
                (window as any).loadingData = false;
                resolve((window as any).loadedData);
            }
        });
    }
}
```

Обратите внимание, что теперь для загрузки данных вместо специальных методов используется метод `ensureRecentDocuments`. Если данные уже были загружены, этот метод разрешает обещание и немедленно возвращает ранее загруженные документы. Если данные загружаются в настоящий момент, метод ожидает в течение 100 мс и пытается разрешить обещание снова.

Взглянув на журнал в средствах разработчика, можно заметить, что удаленный API теперь был вызван только один раз.

![Один оператор журнала, указывающий на загрузку данных для обеих веб-частей](../../../../images/guidance-sharingdata-reusing-data-global-variable-loading-message.png)

Из информационных сообщений видно следующее: при попытке загрузить данные вторая веб-часть обнаруживает, что данные уже загружаются. После загрузки данных веб-часть использует имеющиеся данные, а не загружает их самостоятельно.

![В информационном сообщении журнала показано, что вторая веб-часть ожидает, пока загрузятся данные](../../../../images/guidance-sharingdata-reusing-data-global-variable-waiting-message.png)

Использование глобальной переменной — самый легкий способ обеспечить использование данных разными веб-частями на странице. Один из недостатков такого подхода заключается в том, что данные видны не только веб-частям, но и всем остальным элементам на странице. Из-за этого возникает риск того, что элементы страницы, использующие для сохранения своих данных ту же переменную, в итоге перепишут ваши данные.

## <a name="store-the-retrieved-data-in-a-cookie"></a>Сохранение полученных данных в файле cookie

Другой способ обеспечить использование данных разными веб-частями — сохранить данные в файле cookie. Дополнительное преимущество использования файлов cookie состоит в том, что данные можно хранить дольше. Поэтому если данные меняются нечасто, можно загрузить их один раз и повторно использовать не только в разных веб-частях, но и на разных страницах.

Подход с использованием файлов cookie напоминает сохранение данных в глобальной переменной. Единственное отличие состоит в том, что фактические данные будут сохранены в файле cookie.

```ts
import { IDocument } from './IDocument';
import * as Cookies from 'js-cookie';

export class DocumentsService {
    private static cookieName: string = 'recentDocuments';

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            let loadedData: IDocument[] = Cookies.getJSON(DocumentsService.cookieName);
            if (loadedData) {
                // data already loaded so reuse
                resolve(loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded, wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                // data not loaded yet, call the remote API,
                // store the data for subsequent requests, and resolve the Promise
                Cookies.set(DocumentsService.cookieName, loadedData, {
                    expires: 1,
                    path: '/'
                });
                (window as any).loadingData = false;
                resolve(loadedData);
            }
        });
    }
}
```

В приведенном выше примере используется пакет [js-cookie](https://www.npmjs.com/package/js-cookie), чтобы упростить работу с файлами cookie. Используя параметры, переданные в метод `Cookies.set()`, можно указать, каким страницам и в течение какого времени должны быть доступны полученные данные.

При первоначальной загрузке страницы в Microsoft Edge данные будут получены один раз, а затем повторно использованы обеими веб-частями.

![Записи журнала, сообщающие об однократной загрузке данных и о том, что вторая веб-часть ожидает, пока загрузятся данные согласно первому запросу в Microsoft Edge](../../../../images/guidance-sharingdata-cookie-edge-first-request.png)

При последующих запросах веб-часть может напрямую использовать ранее загруженные данные, не вызывая удаленный API.

![Запись журнала, сообщающая о прямой загрузке данных без вызова удаленного API при последующих запросах в Microsoft Edge](../../../../images/guidance-sharingdata-cookie-edge-subsequent-request.png)

При загрузке страницы в Google Chrome видно, что данные дважды загружаются из удаленного API и вообще не кэшируются.

![Запись журнала, сообщающая о двукратной загрузке данных из удаленного API даже при использовании файлов cookie](../../../../images/guidance-sharingdata-cookie-chrome.png)

Разные веб-браузеры имеют разные ограничения на объем данных, сохраняемых в файлах cookie. В этом примере полученные данные превышают ограничение и не могут быть сохранены в файле cookie в Google Chrome. Поэтому файл cookie не создан, а данные загружены дважды.

С помощью файлов cookie можно обеспечить совместное использование данных веб-частями (если объем таких данных не слишком велик), но у такого метода есть свои недостатки. Как и в случае с глобальными переменными, файлы cookie доступны всем элементам на странице или даже портала и могут быть ими перезаписаны. Кроме того, веб-браузеры отправляют файлы cookie с исходящими запросами и получают их вместе с входящими откликами, из-за чего может замедлиться загрузка данных на портале. Следует учитывать и другой важный момент: файлы cookie хранятся в веб-браузере, поэтому они не должны содержать конфиденциальные данные.

## <a name="store-the-retrieved-data-in-session-or-local-storage"></a>Хранение полученных данных в хранилище сеанса или локальном хранилище

Альтернатива использованию файлов cookie — хранение данных в хранилище сеанса или локальном хранилище. Как и в файлах cookie, в хранилище браузера можно оставить данные не только для последующих запросов, но и для разных страниц. Преимущество использования хранилища браузера состоит в том, что сохраненные данные не отправляются с исходящими запросами, а объем этих данных может быть больше, чем в файле cookie. В отличие от файлов cookie, хранилище браузера может содержать только строковые значения, поэтому для хранения более сложных объектов сначала нужно их сериализировать. Для этого можно использовать собственный метод `JSON.stringify()`.

Если требуется сохранить данные только на время текущего сеанса, используйте хранилище сеанса. Если же данные должны храниться дольше, используйте локальное хранилище. Данные могут находиться в локальном хранилище в течение неограниченного времени, а решение об их удалении принимает пользователь.

Вышеописанный подход, предусматривающий использование службы доступа к данным и файлов cookie, можно легко откорректировать для применения локального хранилища.

```ts
import { IDocument } from './IDocument';

export class DocumentsService {
    private static storageKey: string = 'recentDocuments';

    public static getRecentDocument(): Promise<IDocument> {
        return new Promise<IDocument>((resolve: (document: IDocument) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments[0]);
                });
        });
    }

    public static getRecentDocuments(startFrom: number = 0): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (documents: IDocument[]) => void, reject: (error: any) => void): void => {
            this.ensureRecentDocuments()
                .then((recentDocuments: IDocument[]): void => {
                    resolve(recentDocuments.slice(startFrom, startFrom + 3));
                });
        });
    }

    private static ensureRecentDocuments(): Promise<IDocument[]> {
        return new Promise<IDocument[]>((resolve: (recentDocuments: IDocument[]) => void, reject: (error: any) => void): void => {
            let loadedData: IDocument[] = localStorage ? JSON.parse(localStorage.getItem(DocumentsService.storageKey)) : undefined;
            if (loadedData) {
                // data already loaded so reuse
                resolve(loadedData);
                return;
            }

            if ((window as any).loadingData) {
                // data is being loaded, wait a moment and try again
                window.setTimeout((): void => {
                    DocumentsService.ensureRecentDocuments()
                        .then((recentDocuments: IDocument[]): void => {
                            resolve(recentDocuments);
                        });
                }, 100);
            }
            else {
                (window as any).loadingData = true;
                // data not loaded yet, call the remote API,
                // store the data for subsequent requests, and resolve the Promise
                if (localStorage) {
                    localStorage.setItem(DocumentsService.storageKey, JSON.stringify(loadedData));
                }
                (window as any).loadingData = false;
                resolve(loadedData);
            }
        });
    }
}
```

Реализация такой службы очень похожа на использование файлов cookie. Однако следует учитывать один момент: пользователь может отключить хранилище браузера, поэтому нужно всегда проверять его доступность, прежде чем выполнять с ним какие-либо операции. Как и файлы cookie, локальное хранилище остается в веб-браузере, поэтому его не следует использовать для конфиденциальных данных.

## <a name="share-data-through-a-sharepoint-framework-service"></a>Совместное использование данных с помощью службы SharePoint Framework

Другой подход к совместному использованию данных веб-частями — создание службы SharePoint Framework для централизованной загрузки данных и управления ими. Службы SharePoint Framework — это автономные компоненты, создаваемые отдельно от веб-частей и распространяемые как отдельные пакеты Node. Веб-части SharePoint Framework могут ссылаться на службы и использовать их для конкретных операций, поддерживаемых такими службами (например, для загрузки данных).

> Дополнительные сведения о службах SharePoint Framework см. на странице [https://github.com/SharePoint/sp-dev-docs/wiki/Tech-Note:-ServiceScope-API](https://github.com/SharePoint/sp-dev-docs/wiki/Tech-Note:-ServiceScope-API).

Имеющуюся службу, продемонстрированную в предыдущих примерах, можно преобразовать в службу SharePoint Framework, внеся лишь несколько изменений.

Во-первых, нужно реализовать интерфейс с операциями и свойствами, которые она поддерживает.

```ts
export interface IDocumentsService {
    getRecentDocument(): Promise<IDocument>;
    getRecentDocuments(startFrom: number): Promise<IDocument[]>;
}

export class DocumentsService implements IDocumentsService {
    // ...
}
```

Затем нужно указать [ключ службы](https://dev.office.com/sharepoint/reference/spfx/sp-core-library/servicekey), необходимый для регистрации службы в SharePoint Framework, и обеспечить его использование из веб-частей.

```ts
import { ServiceScope, ServiceKey } from '@microsoft/sp-core-library';

export class DocumentsService implements IDocumentsService {
    public static readonly serviceKey: ServiceKey<IDocumentsService> = ServiceKey.create<IDocumentsService>('contoso:DocumentsService', DocumentsService);
    // ...

    constructor(serviceScope: ServiceScope) {
    }

    // ...
}
```

В каждой службе SharePoint Framework также должен быть конструктор, принимающий в качестве параметра экземпляр класса [ServiceScope](https://dev.office.com/sharepoint/reference/spfx/sp-core-library/servicescope).

Службы SharePoint Framework можно создавать с помощью той же системы создания проектов, что и для клиентских веб-частей SharePoint Framework. Как и для клиентской веб-части, для службы SharePoint Framework предусмотрен манифест. Основное отличие манифеста веб-части заключается в том, что свойству `componentType` присвоено значение `Library`.

```json
{
  "$schema": "../../../node_modules/@microsoft/sp-module-interfaces/lib/manifestSchemas/jsonSchemas/clientSideComponentManifestSchema.json",

  "id": "69b1aacd-68f2-4147-8433-8efb08eae331",
  "alias": "DocumentsService",
  "componentType": "Library",
  "version": "0.0.1",
  "manifestVersion": 2
}
```

Когда все будет готово, вы сможете использовать службу SharePoint Framework в веб-части с помощью ссылок на пакет службы и ключа службы.

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

Даже если несколько веб-частей на странице будут ссылаться на одну и ту же службу, ее пакет будет скачан только один раз, и SharePoint Framework создаст только один экземпляр этой службы на странице. Это удобный механизм для централизации обработки и хранения данных на странице. Работать со службами SharePoint Framework сложнее, чем использовать вышеописанные методы, но у этого подхода есть огромное преимущество: изоляция данных от компонентов на странице и поддержание их целостности.
