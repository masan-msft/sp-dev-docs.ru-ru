---
title: "Совместное использование данных клиентскими веб-частями"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 0b6f64de7f4edb04fd5e91ba1821f122704265f9
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="share-data-between-client-side-web-parts"></a><span data-ttu-id="e162c-102">Совместное использование данных клиентскими веб-частями</span><span class="sxs-lookup"><span data-stu-id="e162c-102">Share Data Between Client-Side Web Parts</span></span>

> <span data-ttu-id="e162c-103">**Примечание.**</span><span class="sxs-lookup"><span data-stu-id="e162c-103">**Note:**</span></span> <span data-ttu-id="e162c-104">Эта статья еще не была проверена на общедоступной версии SPFx, поэтому у вас могут возникнуть трудности при использовании последнего выпуска.</span><span class="sxs-lookup"><span data-stu-id="e162c-104">Note. This article has not yet been verified with the SPFx GA version, so you might have challenges making this work as described using the latest release.</span></span>

<span data-ttu-id="e162c-p102">При создании клиентских веб-частей можно загрузить данные один раз и повторно использовать их в разных веб-частях. Это улучшит отображение страниц и уменьшит нагрузку на сеть. В статье описан ряд подходов, позволяющий обеспечить совместное использование данных разными веб-частями.</span><span class="sxs-lookup"><span data-stu-id="e162c-p102">When building client-side web parts, loading data once and reusing it across different web parts will help you improve the performance of your pages and decrease the load on your network. This article describes a number of approaches that you can use to share data across multiple web parts.</span></span>

## <a name="why-share-data-between-web-parts"></a><span data-ttu-id="e162c-107">Зачем разным веб-частям использовать одни и те же данные</span><span class="sxs-lookup"><span data-stu-id="e162c-107">Why Share Data Between Web Parts</span></span>

<span data-ttu-id="e162c-p103">Многие создаваемые веб-части используются вместе на одной странице. Если рассматривать каждую веб-часть как отдельный фрагмент страницы, придется многократно загружать похожие или даже одинаковые наборы данных на одной странице. При этом безо всякой необходимости замедлится загрузка страницы, а сетевой трафик увеличится.</span><span class="sxs-lookup"><span data-stu-id="e162c-p103">Often, when building web parts, a number of them will be used together on one page. If you consider each web part as a standalone part of the page, then you may end up in a situation where you are loading a similar or even the same set of data multiple times on the same page. This will unnecessarily slow down the loading of the page and increase traffic on your network.</span></span>

![Две веб-части на одной странице, загружающие похожие наборы данных по отдельности](../../../images/guidance-sharingdata-loading-data-separately.png)

<span data-ttu-id="e162c-112">Служба, отвечающая за загрузку данных, может выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="e162c-112">A sample service responsible for loading the data could look like the following:</span></span>

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

<span data-ttu-id="e162c-113">Клиентские веб-части SharePoint Framework используют эту службу с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="e162c-113">SharePoint Framework client-side web parts would consume this service using the following code:</span></span>

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

<span data-ttu-id="e162c-p104">Чтобы сократить время загрузки страницы и уменьшить сетевой трафик, можно создать веб-части таким образом, чтобы данные загружались только один раз. Каждый раз, когда одна их веб-частей на странице запрашивает определенный набор данных, при возможности она будет использовать ранее загруженные данные.</span><span class="sxs-lookup"><span data-stu-id="e162c-p104">To improve the loading time of the page and decrease the traffic on your network, you can build your web parts in such a way that they will load the data only once. Whenever one of the web parts on the page requests a specific set of data, it will reuse data loaded previously if possible.</span></span>

## <a name="store-the-retrieved-data-in-a-globally-scoped-variable"></a><span data-ttu-id="e162c-116">Хранение полученных данных в глобальной переменной</span><span class="sxs-lookup"><span data-stu-id="e162c-116">Store the Retrieved Data in a Globally-Scoped Variable</span></span>

> <span data-ttu-id="e162c-p105">Примечание. Как правило, не рекомендуется использовать глобальные переменные. Однако в целях демонстрации и простоты мы используем их в нашем примере кода. Решить эту проблему можно множеством способов, в том числе путем импорта и экспорта модулей с помощью понятий TypeScript.</span><span class="sxs-lookup"><span data-stu-id="e162c-p105">Note, globally-scoped variables are generally a bad idea. However, for illustration and simplicity purposes we are using them here as "demo code". There are many patterns around this issue, including importing/exporting modules using TypeScript concepts.</span></span>

<span data-ttu-id="e162c-p106">Веб-части, созданные с помощью SharePoint Framework, изолированы в отдельных модулях. Поэтому одна веб-часть не может напрямую получить доступ к данным и свойствам, сохраненным другой веб-частью. Один из способов обойти такую особенность избежать такой проблемы и сделать данные, загруженные одной веб-частью, доступными для других веб-частей на странице — назначить полученные данные глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="e162c-p106">Web parts built using the SharePoint Framework are isolated into separate modules. This way, one web part cannot directly access data and properties stored by another web part. One way to overcome this design characteristic and make data loaded by one web part available to other web parts on the page is to assign the retrieved data to a globally-scoped variable.</span></span>

<span data-ttu-id="e162c-123">Представленную выше службу доступа к данным можно изменить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e162c-123">Using the data access service shown above, it could be changed as follows:</span></span>

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

<span data-ttu-id="e162c-p107">Обратите внимание, что теперь для загрузки данных вместо специальных методов используется метод `ensureRecentDocuments`. Если данные уже были загружены, этот метод разрешает обещание и немедленно возвращает ранее загруженные документы. Если данные загружаются в настоящий момент, метод ожидает в течение 100 мс и пытается разрешить обещание снова.</span><span class="sxs-lookup"><span data-stu-id="e162c-p107">Notice how loading the data has been moved from the specific methods to the `ensureRecentDocuments` method. If the data has been loaded previously, the method resolves the promise immediately returning the previously loaded documents. If the data is currently being loaded, the method waits for 100ms and tries resolving the promise again.</span></span>

<span data-ttu-id="e162c-127">Взглянув на журнал в средствах разработчика, можно заметить, что удаленный API теперь был вызван только один раз.</span><span class="sxs-lookup"><span data-stu-id="e162c-127">If you look at the log in the developer tools, you will notice that the remote API is now called only once.</span></span>

![Один оператор журнала, указывающий на загрузку данных для обеих веб-частей](../../../images/guidance-sharingdata-reusing-data-global-variable-loading-message.png)

<span data-ttu-id="e162c-p108">Из информационных сообщений видно следующее: при попытке загрузить данные вторая веб-часть обнаруживает, что данные уже загружаются. После загрузки данных веб-часть использует имеющиеся данные, а не загружает их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="e162c-p108">Looking at the informational messages, you can confirm that when the second web part tries to load the data it detects that the data is already being loaded. Once the data is loaded, it reuses the existing data rather than loading it itself.</span></span>

![В информационном сообщении журнала показано, что вторая веб-часть ожидает, пока загрузятся данные](../../../images/guidance-sharingdata-reusing-data-global-variable-waiting-message.png)

<span data-ttu-id="e162c-p109">Использование глобальной переменной — самый легкий способ обеспечить использование данных разными веб-частями на странице. Один из недостатков такого подхода заключается в том, что данные видны не только веб-частям, но и всем остальным элементам на странице. Из-за этого возникает риск того, что элементы страницы, использующие для сохранения своих данных ту же переменную, в итоге перепишут ваши данные.</span><span class="sxs-lookup"><span data-stu-id="e162c-p109">Using a globally-scoped variable is the easiest way to exchange data between different web parts on the page. One downside of using this approach, however, is that the data is exposed not only to web parts but also to all other elements on the page. This introduces the risk of other elements on the page using the same variable as you to store their data potentially overwriting your data.</span></span>

## <a name="store-the-retrieved-data-in-a-cookie"></a><span data-ttu-id="e162c-135">Сохранение полученных данных в файле cookie</span><span class="sxs-lookup"><span data-stu-id="e162c-135">Store the Retrieved Data in a Cookie</span></span>

<span data-ttu-id="e162c-p110">Другой способ обеспечить использование данных разными веб-частями — сохранить данные в файле cookie. Дополнительное преимущество использования файлов cookie состоит в том, что данные можно хранить дольше. Поэтому если данные меняются нечасто, можно загрузить их один раз и повторно использовать не только в разных веб-частях, но и на разных страницах.</span><span class="sxs-lookup"><span data-stu-id="e162c-p110">Another approach to exchange data across different web parts is by storing the data in a cookie. The added benefit of using cookies is that you can persist the data for longer periods of time. So in cases where the data doesn't change often, you can load the data once and reuse it not only across different web parts but also across different pages.</span></span>

<span data-ttu-id="e162c-p111">Подход с использованием файлов cookie напоминает сохранение данных в глобальной переменной. Единственное отличие состоит в том, что фактические данные будут сохранены в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="e162c-p111">The implementation using cookies is very similar to how you store data in a globally-scoped variable. The only difference is that the actual data would be stored in a cookie:</span></span>

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

<span data-ttu-id="e162c-p112">В приведенном выше примере используется пакет [js-cookie](https://www.npmjs.com/package/js-cookie), чтобы упростить работу с файлами cookie. Используя параметры, переданные в метод `Cookies.set()`, можно указать, каким страницам и в течение какого времени должны быть доступны полученные данные.</span><span class="sxs-lookup"><span data-stu-id="e162c-p112">In the example above the [js-cookie](https://www.npmjs.com/package/js-cookie) package is used to simplify working with cookies. Using the parameters passed into the `Cookies.set()` method you can specify to which pages and for how long the retrieved data should be available.</span></span>

<span data-ttu-id="e162c-143">При первоначальной загрузке страницы в Microsoft Edge данные будут получены один раз, а затем повторно использованы обеими веб-частями.</span><span class="sxs-lookup"><span data-stu-id="e162c-143">When you load the page in Microsoft Edge the first time, you will see that the data is retrieved once and reused by both web parts.</span></span>

![Записи журнала, сообщающие об однократной загрузке данных и о том, что вторая веб-часть ожидает, пока загрузятся данные согласно первому запросу в Microsoft Edge](../../../images/guidance-sharingdata-cookie-edge-first-request.png)

<span data-ttu-id="e162c-145">При последующих запросах веб-часть может напрямую использовать ранее загруженные данные, не вызывая удаленный API.</span><span class="sxs-lookup"><span data-stu-id="e162c-145">On subsequent requests, a web part can directly reuse the previously loaded data without calling the remote API.</span></span>

![Запись журнала, сообщающая о прямой загрузке данных без вызова удаленного API при последующих запросах в Microsoft Edge](../../../images/guidance-sharingdata-cookie-edge-subsequent-request.png)

<span data-ttu-id="e162c-147">При загрузке страницы в Google Chrome видно, что данные дважды загружаются из удаленного API и вообще не кэшируются.</span><span class="sxs-lookup"><span data-stu-id="e162c-147">When loading the page in Google Chrome, you would see that the data is loaded twice from the remote API and is not being cached at all.</span></span>

![Запись журнала, сообщающая о двукратной загрузке данных из удаленного API даже при использовании файлов cookie](../../../images/guidance-sharingdata-cookie-chrome.png)

<span data-ttu-id="e162c-p113">Разные веб-браузеры имеют разные ограничения на объем данных, сохраняемых в файлах cookie. В этом примере полученные данные превышают ограничение и не могут быть сохранены в файле cookie в Google Chrome. Поэтому файл cookie не создан, а данные загружены дважды.</span><span class="sxs-lookup"><span data-stu-id="e162c-p113">Different web browsers have different limits regarding how much data can be stored in a cookie. In this example, the retrieved data exceeds the maximum length of what can be stored in a cookie in Google Chrome. As a result, no cookie is being set and the data is loaded twice.</span></span>

<span data-ttu-id="e162c-p114">С помощью файлов cookie можно обеспечить совместное использование данных веб-частями (если объем таких данных не слишком велик), но у такого метода есть свои недостатки. Как и в случае с глобальными переменными, файлы cookie доступны всем элементам на странице или даже портала и могут быть ими перезаписаны. Кроме того, веб-браузеры отправляют файлы cookie с исходящими запросами и получают их вместе с входящими откликами, из-за чего может замедлиться загрузка данных на портале. Следует учитывать и другой важный момент: файлы cookie хранятся в веб-браузере, поэтому они не должны содержать конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="e162c-p114">While you could use cookies to share data between web parts, assuming the data that you want to share is not too large, there are some downsides to using cookies. Similar to globally-scoped variables, cookies are available to all elements on the page, or even across the whole portal and could be overwritten by them. Additionally, web browsers send cookies with outgoing requests and retrieve them with incoming responses which adds overhead to loading information in the portal. Another important thing that you should consider is that cookies are persisted in the web browser and you should never store any confidential information in them.</span></span>

## <a name="store-the-retrieved-data-in-session-or-local-storage"></a><span data-ttu-id="e162c-156">Хранение полученных данных в хранилище сеанса или локальном хранилище</span><span class="sxs-lookup"><span data-stu-id="e162c-156">Store the Retrieved Data in Session or Local Storage</span></span>

<span data-ttu-id="e162c-p115">Альтернатива использованию файлов cookie — хранение данных в хранилище сеанса или локальном хранилище. Как и в файлах cookie, в хранилище браузера можно оставить данные не только для последующих запросов, но и для разных страниц. Преимущество использования хранилища браузера состоит в том, что сохраненные данные не отправляются с исходящими запросами, а объем этих данных может быть больше, чем в файле cookie. В отличие от файлов cookie, хранилище браузера может содержать только строковые значения, поэтому для хранения более сложных объектов сначала нужно их сериализировать. Для этого можно использовать собственный метод `JSON.stringify()`.</span><span class="sxs-lookup"><span data-stu-id="e162c-p115">An alternative to using cookies is storing data in session or local storage. Similar to cookies, browser storage allows you to persist data not just for subsequent requests but also across pages. The benefits of using browser storage over using cookies are that data stored in browser storage is not sent with outgoing requests and you can store more data than in a cookie. Comparable to cookies, browser storage is capable of storing only string values. So if you need to store more complex objects, you will need to serialize them first using, for example, the native `JSON.stringify()` method.</span></span>

<span data-ttu-id="e162c-p116">Если требуется сохранить данные только на время текущего сеанса, используйте хранилище сеанса. Если же данные должны храниться дольше, используйте локальное хранилище. Данные могут находиться в локальном хранилище в течение неограниченного времени, а решение об их удалении принимает пользователь.</span><span class="sxs-lookup"><span data-stu-id="e162c-p116">If you want data to be stored only during the current session, you should use session storage. If the data should be persisted for a longer period of time you should use local storage instead. Data stored in local storage doesn't expire and it's up to you to clear it.</span></span>

<span data-ttu-id="e162c-165">Вышеописанный подход, предусматривающий использование службы доступа к данным и файлов cookie, можно легко откорректировать для применения локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="e162c-165">The previously used implementation of the data access service based on cookies can easily be adapted to use local storage instead:</span></span>

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

<span data-ttu-id="e162c-p117">Реализация такой службы очень похожа на использование файлов cookie. Однако следует учитывать один момент: пользователь может отключить хранилище браузера, поэтому нужно всегда проверять его доступность, прежде чем выполнять с ним какие-либо операции. Как и файлы cookie, локальное хранилище остается в веб-браузере, поэтому его не следует использовать для конфиденциальных данных.</span><span class="sxs-lookup"><span data-stu-id="e162c-p117">The implementation of this service is very similar to when using cookies. One thing that you should keep in mind, however, is that browser storage can be disabled by the user and you should always check for its availability before performing operations on it. Just as with cookies, local storage is persisted in the web browser and you should never use it to store any confidential information.</span></span>

## <a name="share-data-through-a-sharepoint-framework-service"></a><span data-ttu-id="e162c-169">Совместное использование данных с помощью службы SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="e162c-169">Share Data Through a SharePoint Framework Service</span></span>

<span data-ttu-id="e162c-p118">Другой подход к совместному использованию данных веб-частями — создание службы SharePoint Framework для централизованной загрузки данных и управления ими. Службы SharePoint Framework — это автономные компоненты, создаваемые отдельно от веб-частей и распространяемые как отдельные пакеты Node. Веб-части SharePoint Framework могут ссылаться на службы и использовать их для конкретных операций, поддерживаемых такими службами (например, для загрузки данных).</span><span class="sxs-lookup"><span data-stu-id="e162c-p118">Another approach to sharing data between web parts, is by building a SharePoint Framework service and using it to centrally load and manage data. SharePoint Framework services are standalone components built separately from web parts and distributed as separate Node packages. SharePoint Framework web parts can reference services and use them to perform specific operations supported by these services, such as loading data.</span></span>

> <span data-ttu-id="e162c-173">Дополнительные сведения о службах SharePoint Framework см. на странице [https://github.com/SharePoint/sp-dev-docs/wiki/Tech-Note:-ServiceScope-API](https://github.com/SharePoint/sp-dev-docs/wiki/Tech-Note:-ServiceScope-API).</span><span class="sxs-lookup"><span data-stu-id="e162c-173">For more information about SharePoint Framework services see [https://github.com/SharePoint/sp-dev-docs/wiki/Tech-Note:-ServiceScope-API](https://github.com/SharePoint/sp-dev-docs/wiki/Tech-Note:-ServiceScope-API).</span></span>

<span data-ttu-id="e162c-174">Имеющуюся службу, продемонстрированную в предыдущих примерах, можно преобразовать в службу SharePoint Framework, внеся лишь несколько изменений.</span><span class="sxs-lookup"><span data-stu-id="e162c-174">The existing service, demonstrated in previous examples, with just a few modifications can be transformed into a SharePoint Framework service.</span></span>

<span data-ttu-id="e162c-175">Во-первых, нужно реализовать интерфейс с операциями и свойствами, которые она поддерживает.</span><span class="sxs-lookup"><span data-stu-id="e162c-175">First, it needs to implement an interface that represents the operations and properties it supports:</span></span>

```ts
export interface IDocumentsService {
    getRecentDocument(): Promise<IDocument>;
    getRecentDocuments(startFrom: number): Promise<IDocument[]>;
}

export class DocumentsService implements IDocumentsService {
    // ...
}
```

<span data-ttu-id="e162c-176">Затем нужно указать [ключ службы](https://dev.office.com/sharepoint/reference/spfx/sp-core-library/servicekey), необходимый для регистрации службы в SharePoint Framework, и обеспечить его использование из веб-частей.</span><span class="sxs-lookup"><span data-stu-id="e162c-176">Next, it needs to specify a [service key](https://dev.office.com/sharepoint/reference/spfx/sp-core-library/servicekey) used to register the service with the SharePoint Framework and consume it from within web parts:</span></span>

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

<span data-ttu-id="e162c-177">В каждой службе SharePoint Framework также должен быть конструктор, принимающий в качестве параметра экземпляр класса [ServiceScope](https://dev.office.com/sharepoint/reference/spfx/sp-core-library/servicescope).</span><span class="sxs-lookup"><span data-stu-id="e162c-177">Each SharePoint Framework service must also have a constructor that accepts an instance of the [ServiceScope](https://dev.office.com/sharepoint/reference/spfx/sp-core-library/servicescope) class as a parameter.</span></span>

<span data-ttu-id="e162c-p119">Службы SharePoint Framework можно создавать с помощью той же системы создания проектов, что и для клиентских веб-частей SharePoint Framework. Как и для клиентской веб-части, для службы SharePoint Framework предусмотрен манифест. Основное отличие манифеста веб-части заключается в том, что свойству `componentType` присвоено значение `Library`.</span><span class="sxs-lookup"><span data-stu-id="e162c-p119">SharePoint Framework services can be built using the same project build system as SharePoint Framework client-side web parts. Similar to a client-side web part, a SharePoint Framework service has a manifest. The main difference with the web part manifest is that the `componentType` property is set to `Library`:</span></span>

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

<span data-ttu-id="e162c-181">Когда все будет готово, вы сможете использовать службу SharePoint Framework в веб-части с помощью ссылок на пакет службы и ключа службы.</span><span class="sxs-lookup"><span data-stu-id="e162c-181">Once ready, you can consume the SharePoint Framework service from a web part by referencing its package and retrieving the service using its key.</span></span>

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

<span data-ttu-id="e162c-p120">Даже если несколько веб-частей на странице будут ссылаться на одну и ту же службу, ее пакет будет скачан только один раз, и SharePoint Framework создаст только один экземпляр этой службы на странице. Это удобный механизм для централизации обработки и хранения данных на странице. Работать со службами SharePoint Framework сложнее, чем использовать вышеописанные методы, но у этого подхода есть огромное преимущество: изоляция данных от компонентов на странице и поддержание их целостности.</span><span class="sxs-lookup"><span data-stu-id="e162c-p120">Even if there are multiple web parts on the page referencing the same service, its bundle will be downloaded only once and the SharePoint Framework will create only one instance of the service on the page. This offers you a convenient mechanism for centralizing processing and storing data on a page. While working with SharePoint Framework services is more complex than the previously described approaches, it offers you the great benefit of isolating the data from other components on the page and better handling of its integrity.</span></span>
