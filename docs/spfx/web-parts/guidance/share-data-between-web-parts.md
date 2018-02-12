---
title: "Совместное использование данных клиентскими веб-частями"
description: "Узнайте, какие подходы можно использовать для совместного использования и хранения полученных данных в нескольких веб-частях SharePoint."
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: a9b423c5bf55ebe14f1b7c77c92b2c532750707e
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="share-data-between-client-side-web-parts"></a><span data-ttu-id="d1a73-103">Совместное использование данных клиентскими веб-частями</span><span class="sxs-lookup"><span data-stu-id="d1a73-103">Share data between client-side web parts</span></span>

<span data-ttu-id="d1a73-p101">При создании клиентских веб-частей можно загрузить данные один раз и повторно использовать их в разных веб-частях. Это улучшит отображение страниц и уменьшит нагрузку на сеть. В этой статье описан ряд подходов, с помощью которых можно обеспечить совместное использование данных разными веб-частями.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p101">When building client-side web parts, loading data once and reusing it across different web parts helps you improve the performance of your pages and decrease the load on your network. This article describes a number of approaches that you can use to share data across multiple web parts.</span></span>

## <a name="why-share-data-between-web-parts"></a><span data-ttu-id="d1a73-106">Зачем разным веб-частям использовать одни и те же данные</span><span class="sxs-lookup"><span data-stu-id="d1a73-106">Why share data between web parts</span></span>

<span data-ttu-id="d1a73-p102">При создании веб-частей часто приходится использовать несколько таких решений на одной странице. Если рассматривать каждую веб-часть как отдельный фрагмент страницы, придется многократно загружать похожие или даже одинаковые наборы данных на одной странице. При этом безо всякой необходимости замедлится загрузка страницы, а сетевой трафик увеличится.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p102">Often, when building web parts, a number of them are used together on one page. If you consider each web part as a standalone part of the page, you may end up in a situation where you are loading a similar or even the same set of data multiple times on the same page. This unnecessarily slows down the loading of the page and increases traffic on your network.</span></span>

![Две веб-части на одной странице, загружающие похожие наборы данных по отдельности](../../../images/guidance-sharingdata-loading-data-separately.png)

<br/>

<span data-ttu-id="d1a73-111">Служба, отвечающая за загрузку данных, может выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="d1a73-111">A sample service responsible for loading the data could look like the following:</span></span>

```typescript
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

<br/>

<span data-ttu-id="d1a73-112">Клиентские веб-части SharePoint Framework используют эту службу с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="d1a73-112">SharePoint Framework client-side web parts would consume this service by using the following code:</span></span>

```typescript
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

<br/>

<span data-ttu-id="d1a73-p103">Чтобы сократить время загрузки страницы и уменьшить сетевой трафик, можно создать веб-части таким образом, чтобы данные загружались только один раз. Каждый раз, когда одна их веб-частей на странице запрашивает определенный набор данных, по мере возможности она будет использовать ранее загруженные данные.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p103">To improve the loading time of the page and decrease the traffic on your network, you can build your web parts in such a way that they load the data only once. Whenever one of the web parts on the page requests a specific set of data, it reuses data loaded previously if possible.</span></span>

## <a name="store-the-retrieved-data-in-a-globally-scoped-variable"></a><span data-ttu-id="d1a73-115">Хранение полученных данных в глобальной переменной</span><span class="sxs-lookup"><span data-stu-id="d1a73-115">Store the retrieved data in a globally-scoped variable</span></span>

> [!NOTE] 
> <span data-ttu-id="d1a73-p104">Как правило, не рекомендуется использовать глобальные переменные. Однако в целях наглядности и простоты мы используем их в нашем примере кода. Решить эту проблему можно множеством способов, в том числе путем импорта и экспорта модулей с помощью понятий TypeScript.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p104">Globally-scoped variables are generally a bad idea. However, for illustration and simplicity purposes, we are using them here as "demo code." There are many patterns around this issue, including importing/exporting modules by using TypeScript concepts.</span></span>

<span data-ttu-id="d1a73-p105">Веб-части, созданные с помощью SharePoint Framework, изолированы в отдельных модулях. Поэтому одна веб-часть не может напрямую получить доступ к данным и свойствам, сохраненным другой веб-частью. Один из способов обойти такую особенность избежать такой проблемы и сделать данные, загруженные одной веб-частью, доступными для других веб-частей на странице — назначить полученные данные глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p105">Web parts built using the SharePoint Framework are isolated into separate modules. This way, one web part cannot directly access data and properties stored by another web part. One way to overcome this design characteristic and make data loaded by one web part available to other web parts on the page is to assign the retrieved data to a globally-scoped variable.</span></span>

<span data-ttu-id="d1a73-122">Представленную выше службу доступа к данным можно изменить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d1a73-122">Using the data access service shown earlier, it could be changed as follows:</span></span>

```typescript
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

<br/>

<span data-ttu-id="d1a73-p106">Обратите внимание, что теперь для загрузки данных вместо специальных методов используется метод `ensureRecentDocuments`. Если данные уже были загружены, этот метод разрешает обещание и немедленно возвращает ранее загруженные документы. Если в это время выполняется загрузка данных, метод ожидает в течение 100 мс и пытается разрешить обещание снова.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p106">Notice how loading the data has been moved from the specific methods to the `ensureRecentDocuments` method. If the data has been loaded previously, the method resolves the promise immediately by returning the previously loaded documents. If the data is currently being loaded, the method waits for 100 ms and tries resolving the promise again.</span></span>

<span data-ttu-id="d1a73-126">Взглянув на журнал в средствах разработчика, можно заметить, что удаленный API теперь был вызван только один раз.</span><span class="sxs-lookup"><span data-stu-id="d1a73-126">If you look at the log in the developer tools, you notice that the remote API is now called only once.</span></span>

![Один оператор журнала, указывающий на загрузку данных для обеих веб-частей](../../../images/guidance-sharingdata-reusing-data-global-variable-loading-message.png)

<br/>

<span data-ttu-id="d1a73-p107">Из информационных сообщений видно следующее: при попытке загрузить данные вторая веб-часть обнаруживает, что данные уже загружаются. После загрузки данных веб-часть использует имеющиеся данные, а не загружает их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p107">Looking at the informational messages, you can confirm that when the second web part tries to load the data, it detects that the data is already being loaded. After the data is loaded, it reuses the existing data rather than loading it itself.</span></span>

![В информационном сообщении журнала показано, что вторая веб-часть ожидает, пока загрузятся данные](../../../images/guidance-sharingdata-reusing-data-global-variable-waiting-message.png)

<br/>

<span data-ttu-id="d1a73-p108">Использование глобальной переменной — самый легкий способ обеспечить использование данных разными веб-частями на странице. Один из недостатков такого подхода заключается в том, что данные видны не только веб-частям, но и всем остальным элементам на странице. Из-за этого возникает риск того, что элементы страницы, использующие для сохранения своих данных ту же переменную, в итоге перепишут ваши данные.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p108">Using a globally-scoped variable is the easiest way to exchange data between different web parts on the page. One downside of using this approach, however, is that the data is exposed not only to web parts but also to all other elements on the page. This introduces the risk of other elements on the page using the same variable as you to store their data, potentially overwriting your data.</span></span>

## <a name="store-the-retrieved-data-in-a-cookie"></a><span data-ttu-id="d1a73-134">Сохранение полученных данных в файле cookie</span><span class="sxs-lookup"><span data-stu-id="d1a73-134">Store the retrieved data in a cookie</span></span>

<span data-ttu-id="d1a73-p109">Другой способ обеспечить использование данных разными веб-частями — сохранить данные в файле cookie. Дополнительное преимущество использования файлов cookie состоит в том, что данные можно хранить дольше. Поэтому если данные меняются нечасто, можно загрузить их один раз и повторно использовать не только в разных веб-частях, но и на разных страницах.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p109">Another approach to exchange data across different web parts is by storing the data in a cookie. The added benefit of using cookies is that you can persist the data for longer periods of time. So in cases where the data doesn't change often, you can load the data once and reuse it not only across different web parts but also across different pages.</span></span>

<span data-ttu-id="d1a73-p110">Подход с использованием файлов cookie напоминает сохранение данных в глобальной переменной. Единственное отличие состоит в том, что фактические данные будут сохранены в файле cookie.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p110">The implementation that uses cookies is very similar to how you store data in a globally-scoped variable. The only difference is that the actual data would be stored in a cookie.</span></span>

```typescript
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

<br/>

<span data-ttu-id="d1a73-p111">В предыдущем примере используется пакет [js-cookie](https://www.npmjs.com/package/js-cookie), упрощающий работу с файлами cookie. Используя параметры, переданные в метод `Cookies.set()`, можно указать, каким страницам и в течение какого времени должны быть доступны полученные данные.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p111">In the previous example, the [js-cookie](https://www.npmjs.com/package/js-cookie) package is used to simplify working with cookies. Using the parameters passed into the `Cookies.set()` method, you can specify to which pages and for how long the retrieved data should be available.</span></span>

<span data-ttu-id="d1a73-142">При первоначальной загрузке страницы в Microsoft Edge данные будут получены один раз, а затем повторно использованы обеими веб-частями.</span><span class="sxs-lookup"><span data-stu-id="d1a73-142">When you load the page in Microsoft Edge for the first time, you see that the data is retrieved once and reused by both web parts.</span></span>

![Записи журнала, сообщающие об однократной загрузке данных и о том, что вторая веб-часть ожидает, пока загрузятся данные согласно первому запросу в Microsoft Edge](../../../images/guidance-sharingdata-cookie-edge-first-request.png)

<br/>

<span data-ttu-id="d1a73-144">При последующих запросах веб-часть может напрямую использовать ранее загруженные данные, не вызывая удаленный API.</span><span class="sxs-lookup"><span data-stu-id="d1a73-144">On subsequent requests, a web part can directly reuse the previously loaded data without calling the remote API.</span></span>

![Запись журнала, сообщающая о прямой загрузке данных без вызова удаленного API при последующих запросах в Microsoft Edge](../../../images/guidance-sharingdata-cookie-edge-subsequent-request.png)

<br/>

<span data-ttu-id="d1a73-146">При загрузке страницы в Google Chrome видно, что данные дважды загружаются из удаленного API и вообще не кэшируются.</span><span class="sxs-lookup"><span data-stu-id="d1a73-146">When loading the page in Google Chrome, you see that the data is loaded twice from the remote API and is not being cached at all.</span></span>

![Запись журнала, сообщающая о двукратной загрузке данных из удаленного API даже при использовании файлов cookie](../../../images/guidance-sharingdata-cookie-chrome.png)

<br/>

<span data-ttu-id="d1a73-p112">Разные веб-браузеры имеют разные ограничения на объем данных, сохраняемых в файлах cookie. В этом примере полученные данные превышают ограничение и не могут быть сохранены в файле cookie в Google Chrome. Поэтому файл cookie не создан, а данные загружены дважды.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p112">Different web browsers have different limits regarding how much data can be stored in a cookie. In this example, the retrieved data exceeds the maximum length of what can be stored in a cookie in Google Chrome. As a result, no cookie is being set and the data is loaded twice.</span></span>

<span data-ttu-id="d1a73-p113">С помощью файлов cookie можно обеспечить использование одних данных разными веб-частями (если объем таких данных не слишком велик), но у такого метода есть свои недостатки. Как и в случае с глобальными переменными, файлы cookie доступны всем элементам на странице или даже на портале и могут быть ими перезаписаны. Кроме того, веб-браузеры отправляют файлы cookie с исходящими запросами и получают их вместе с входящими ответами, из-за чего может замедлиться загрузка данных на портале. Следует учитывать и другой важный момент: файлы cookie хранятся в веб-браузере, поэтому они не должны содержать конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p113">While you could use cookies to share data between web parts, assuming the data that you want to share is not too large, there are some downsides to using cookies. Similar to globally-scoped variables, cookies are available to all elements on the page, or even across the whole portal, and could be overwritten by them. Additionally, web browsers send cookies with outgoing requests and retrieve them with incoming responses, which adds overhead to loading information in the portal. Another important thing that you should consider is that cookies are persisted in the web browser, and you should never store any confidential information in them.</span></span>

## <a name="store-the-retrieved-data-in-session-or-local-storage"></a><span data-ttu-id="d1a73-155">Хранение полученных данных в хранилище сеанса или локальном хранилище</span><span class="sxs-lookup"><span data-stu-id="d1a73-155">Store the retrieved data in session or local storage</span></span>

<span data-ttu-id="d1a73-p114">Альтернатива использованию файлов cookie — хранение данных в хранилище сеанса или локальном хранилище. Как и в файлах cookie, в хранилище браузера можно оставить данные не только для последующих запросов, но и для разных страниц. Преимущество использования хранилища браузера состоит в том, что сохраненные данные не отправляются с исходящими запросами, а объем этих данных может быть больше, чем в файле cookie. В отличие от файлов cookie, хранилище браузера может содержать только строковые значения, поэтому для хранения более сложных объектов сначала нужно их сериализировать. Для этого можно использовать встроенный метод `JSON.stringify()`.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p114">An alternative to using cookies is storing data in session or local storage. Similar to cookies, browser storage allows you to persist data not only for subsequent requests but also across pages. The benefits of using browser storage over using cookies are that data stored in browser storage is not sent with outgoing requests and you can store more data than in a cookie. Comparable to cookies, browser storage is capable of storing only string values. So if you need to store more complex objects, you need to serialize them first by using, for example, the native `JSON.stringify()` method.</span></span>

<span data-ttu-id="d1a73-p115">Если требуется сохранить данные только на время текущего сеанса, используйте хранилище сеанса. Если же данные должны храниться дольше, используйте локальное хранилище. Данные могут находиться в локальном хранилище в течение неограниченного времени, а решение об их удалении остается за вами.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p115">If you want data to be stored only during the current session, you should use session storage. If the data should be persisted for a longer period of time, you should use local storage. Data stored in local storage doesn't expire and it's up to you to clear it.</span></span>

<span data-ttu-id="d1a73-164">Приведенную выше реализацию службы доступа к данным на основе файлов cookie можно легко адаптировать к использованию локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="d1a73-164">The previously used implementation of the data access service based on cookies can easily be adapted to use local storage instead.</span></span>

```typescript
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

<br/>

<span data-ttu-id="d1a73-p116">Реализация такой службы очень похожа на использование файлов cookie. Однако следует учитывать один момент: пользователь может отключить хранилище браузера, поэтому нужно всегда проверять его доступность, прежде чем выполнять с ним какие-либо операции. Как и файлы cookie, локальное хранилище остается в веб-браузере, поэтому его не следует использовать для конфиденциальных данных.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p116">The implementation of this service is very similar to when using cookies. One thing that you should keep in mind, however, is that browser storage can be disabled by the user, and you should always check for its availability before performing operations on it. Just as with cookies, local storage is persisted in the web browser and you should never use it to store any confidential information.</span></span>

## <a name="share-data-through-a-sharepoint-framework-service"></a><span data-ttu-id="d1a73-168">Общий доступ к данным через службу SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="d1a73-168">Share data through a SharePoint Framework service</span></span>

<span data-ttu-id="d1a73-p117">Централизованно загружать данные и управлять ими можно через службу SharePoint Framework. Службы SharePoint Framework — это автономные компоненты, создаваемые отдельно от веб-частей и распространяемые как отдельные пакеты Node. Веб-части SharePoint Framework могут ссылаться на службы и использовать их для конкретных операций, поддерживаемых такими службами (например, для загрузки данных).</span><span class="sxs-lookup"><span data-stu-id="d1a73-p117">Another approach to sharing data between web parts is by building a SharePoint Framework service and using it to centrally load and manage data. SharePoint Framework services are standalone components built separately from web parts and distributed as separate Node packages. SharePoint Framework web parts can reference services and use them to perform specific operations supported by these services, such as loading data.</span></span>

<span data-ttu-id="d1a73-172">Имеющуюся службу, продемонстрированную в предыдущих примерах, можно преобразовать в службу SharePoint Framework, внеся лишь несколько изменений.</span><span class="sxs-lookup"><span data-stu-id="d1a73-172">The existing service, demonstrated in previous examples, with just a few modifications, can be transformed into a SharePoint Framework service.</span></span>

<span data-ttu-id="d1a73-173">Во-первых, нужно реализовать интерфейс с операциями и свойствами, которые она поддерживает.</span><span class="sxs-lookup"><span data-stu-id="d1a73-173">First, it needs to implement an interface that represents the operations and properties it supports:</span></span>

```typescript
export interface IDocumentsService {
    getRecentDocument(): Promise<IDocument>;
    getRecentDocuments(startFrom: number): Promise<IDocument[]>;
}

export class DocumentsService implements IDocumentsService {
    // ...
}
```

<br/>

<span data-ttu-id="d1a73-174">Затем нужно указать [ключ службы](https://docs.microsoft.com/ru-RU/javascript/api/sp-core-library/servicekey), необходимый для регистрации службы в SharePoint Framework, и обеспечить его использование из веб-частей.</span><span class="sxs-lookup"><span data-stu-id="d1a73-174">Next, it needs to specify a [service key](https://docs.microsoft.com/ru-RU/javascript/api/sp-core-library/servicekey) used to register the service with the SharePoint Framework and consume it from within web parts:</span></span>

```typescript
import { ServiceScope, ServiceKey } from '@microsoft/sp-core-library';

export class DocumentsService implements IDocumentsService {
    public static readonly serviceKey: ServiceKey<IDocumentsService> = ServiceKey.create<IDocumentsService>('contoso:DocumentsService', DocumentsService);
    // ...

    constructor(serviceScope: ServiceScope) {
    }

    // ...
}
```

<br/>

<span data-ttu-id="d1a73-175">В каждой службе SharePoint Framework также должен быть конструктор, принимающий в качестве параметра экземпляр класса [ServiceScope](https://docs.microsoft.com/ru-RU/javascript/api/sp-core-library/servicescope).</span><span class="sxs-lookup"><span data-stu-id="d1a73-175">Each SharePoint Framework service must also have a constructor that accepts an instance of the [ServiceScope](https://docs.microsoft.com/ru-RU/javascript/api/sp-core-library/servicescope) class as a parameter.</span></span>

<span data-ttu-id="d1a73-p118">Службы SharePoint Framework можно создавать с помощью той же системы создания проектов, что и для клиентских веб-частей SharePoint Framework. Как и для клиентской веб-части, для службы SharePoint Framework предусмотрен манифест. Основное отличие манифеста веб-части заключается в том, что свойству `componentType` присвоено значение `Library`.</span><span class="sxs-lookup"><span data-stu-id="d1a73-p118">SharePoint Framework services can be built using the same project build system as SharePoint Framework client-side web parts. Similar to a client-side web part, a SharePoint Framework service has a manifest. The main difference with the web part manifest is that the `componentType` property is set to `Library`:</span></span>

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

<br/>

<span data-ttu-id="d1a73-179">Когда все будет готово, вы сможете использовать службу SharePoint Framework в веб-части, ссылаясь на пакет службы и обращаясь к службе по ее ключу.</span><span class="sxs-lookup"><span data-stu-id="d1a73-179">When ready, you can consume the SharePoint Framework service from a web part by referencing its package and retrieving the service using its key.</span></span>

```typescript
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

<br/>

<span data-ttu-id="d1a73-180">Даже если несколько веб-частей на странице ссылается на одну и ту же службу, ее пакет скачивается только один раз, и SharePoint Framework создает только один экземпляр этой службы на странице.</span><span class="sxs-lookup"><span data-stu-id="d1a73-180">Even if there are multiple web parts on the page referencing the same service, its bundle is downloaded only once, and the SharePoint Framework creates only one instance of the service on the page.</span></span> <span data-ttu-id="d1a73-181">Это удобный механизм для централизации обработки и хранения данных на странице.</span><span class="sxs-lookup"><span data-stu-id="d1a73-181">This offers you a convenient mechanism for centralizing processing and storing data on a page.</span></span> 

<span data-ttu-id="d1a73-182">Работать со службами SharePoint Framework сложнее, чем применять описанные выше методы, но у этого подхода есть огромное преимущество — изоляция данных от других компонентов на странице и поддержание их целостности.</span><span class="sxs-lookup"><span data-stu-id="d1a73-182">While working with SharePoint Framework services is more complex than the previously described approaches, it offers you the great benefits of isolating the data from other components on the page and better handling of its integrity.</span></span>

## <a name="see-also"></a><span data-ttu-id="d1a73-183">См. также</span><span class="sxs-lookup"><span data-stu-id="d1a73-183">See also</span></span>

- [<span data-ttu-id="d1a73-184">Руководство. Использование одних данных разными веб-частями с применением глобальной переменной</span><span class="sxs-lookup"><span data-stu-id="d1a73-184">Tutorial: Share data between web parts by using a global variable</span></span>](./tutorial-share-data-between-web-parts-global-variable.md)