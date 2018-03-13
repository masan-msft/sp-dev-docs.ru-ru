---
title: "Совместное использование данных клиентскими веб-частями"
description: "Узнайте, какие подходы можно использовать для совместного использования и хранения полученных данных в нескольких веб-частях SharePoint."
ms.date: 01/10/2018
ms.prod: sharepoint
ms.openlocfilehash: e556ec482a9721cd759dac3b3fe32a6f266ab149
ms.sourcegitcommit: 249f0fbce4df81fbe65848f1d26a4ebcad7aa89c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2018
---
# <a name="share-data-between-client-side-web-parts"></a>Совместное использование данных клиентскими веб-частями

При создании клиентских веб-частей можно загрузить данные один раз и повторно использовать их в разных веб-частях. Это улучшит отображение страниц и уменьшит нагрузку на сеть. В этой статье описан ряд подходов, с помощью которых можно обеспечить совместное использование данных разными веб-частями.

## <a name="why-share-data-between-web-parts"></a>Зачем разным веб-частям использовать одни и те же данные

При создании веб-частей часто приходится использовать несколько таких решений на одной странице. Если рассматривать каждую веб-часть как отдельный фрагмент страницы, придется многократно загружать похожие или даже одинаковые наборы данных на одной странице. При этом безо всякой необходимости замедлится загрузка страницы, а сетевой трафик увеличится.

![Две веб-части на одной странице, загружающие похожие наборы данных по отдельности](../../../images/guidance-sharingdata-loading-data-separately.png)

<br/>

Служба, отвечающая за загрузку данных, может выглядеть примерно так:

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

Клиентские веб-части SharePoint Framework используют эту службу с помощью следующего кода:

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

Чтобы сократить время загрузки страницы и уменьшить сетевой трафик, можно создать веб-части таким образом, чтобы данные загружались только один раз. Каждый раз, когда одна их веб-частей на странице запрашивает определенный набор данных, по мере возможности она будет использовать ранее загруженные данные.

## <a name="store-the-retrieved-data-in-a-globally-scoped-variable"></a>Хранение полученных данных в глобальной переменной

> [!NOTE] 
> Как правило, не рекомендуется использовать глобальные переменные. Однако в целях наглядности и простоты мы используем их в нашем примере кода. Решить эту проблему можно множеством способов, в том числе путем импорта и экспорта модулей с помощью понятий TypeScript.

Веб-части, созданные с помощью SharePoint Framework, изолированы в отдельных модулях. Поэтому одна веб-часть не может напрямую получить доступ к данным и свойствам, сохраненным другой веб-частью. Один из способов обойти такую особенность избежать такой проблемы и сделать данные, загруженные одной веб-частью, доступными для других веб-частей на странице — назначить полученные данные глобальной переменной.

Представленную выше службу доступа к данным можно изменить следующим образом:

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

Обратите внимание, что теперь для загрузки данных вместо специальных методов используется метод `ensureRecentDocuments`. Если данные уже были загружены, этот метод разрешает обещание и немедленно возвращает ранее загруженные документы. Если в это время выполняется загрузка данных, метод ожидает в течение 100 мс и пытается разрешить обещание снова.

Взглянув на журнал в средствах разработчика, можно заметить, что удаленный API теперь был вызван только один раз.

![Один оператор журнала, указывающий на загрузку данных для обеих веб-частей](../../../images/guidance-sharingdata-reusing-data-global-variable-loading-message.png)

<br/>

Из информационных сообщений видно следующее: при попытке загрузить данные вторая веб-часть обнаруживает, что данные уже загружаются. После загрузки данных веб-часть использует имеющиеся данные, а не загружает их самостоятельно.

![В информационном сообщении журнала показано, что вторая веб-часть ожидает, пока загрузятся данные](../../../images/guidance-sharingdata-reusing-data-global-variable-waiting-message.png)

<br/>

Использование глобальной переменной — самый легкий способ обеспечить использование данных разными веб-частями на странице. Один из недостатков такого подхода заключается в том, что данные видны не только веб-частям, но и всем остальным элементам на странице. Из-за этого возникает риск того, что элементы страницы, использующие для сохранения своих данных ту же переменную, в итоге перепишут ваши данные.

## <a name="store-the-retrieved-data-in-a-cookie"></a>Сохранение полученных данных в файле cookie

Другой способ обеспечить использование данных разными веб-частями — сохранить данные в файле cookie. Дополнительное преимущество использования файлов cookie состоит в том, что данные можно хранить дольше. Поэтому если данные меняются нечасто, можно загрузить их один раз и повторно использовать не только в разных веб-частях, но и на разных страницах.

Подход с использованием файлов cookie напоминает сохранение данных в глобальной переменной. Единственное отличие состоит в том, что фактические данные будут сохранены в файле cookie.

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

В предыдущем примере используется пакет [js-cookie](https://www.npmjs.com/package/js-cookie), упрощающий работу с файлами cookie. Используя параметры, переданные в метод `Cookies.set()`, можно указать, каким страницам и в течение какого времени должны быть доступны полученные данные.

При первоначальной загрузке страницы в Microsoft Edge данные будут получены один раз, а затем повторно использованы обеими веб-частями.

![Записи журнала, сообщающие об однократной загрузке данных и о том, что вторая веб-часть ожидает, пока загрузятся данные согласно первому запросу в Microsoft Edge](../../../images/guidance-sharingdata-cookie-edge-first-request.png)

<br/>

При последующих запросах веб-часть может напрямую использовать ранее загруженные данные, не вызывая удаленный API.

![Запись журнала, сообщающая о прямой загрузке данных без вызова удаленного API при последующих запросах в Microsoft Edge](../../../images/guidance-sharingdata-cookie-edge-subsequent-request.png)

<br/>

При загрузке страницы в Google Chrome видно, что данные дважды загружаются из удаленного API и вообще не кэшируются.

![Запись журнала, сообщающая о двукратной загрузке данных из удаленного API даже при использовании файлов cookie](../../../images/guidance-sharingdata-cookie-chrome.png)

<br/>

Разные веб-браузеры имеют разные ограничения на объем данных, сохраняемых в файлах cookie. В этом примере полученные данные превышают ограничение и не могут быть сохранены в файле cookie в Google Chrome. Поэтому файл cookie не создан, а данные загружены дважды.

С помощью файлов cookie можно обеспечить использование одних данных разными веб-частями (если объем таких данных не слишком велик), но у такого метода есть свои недостатки. Как и в случае с глобальными переменными, файлы cookie доступны всем элементам на странице или даже на портале и могут быть ими перезаписаны. Кроме того, веб-браузеры отправляют файлы cookie с исходящими запросами и получают их вместе с входящими ответами, из-за чего может замедлиться загрузка данных на портале. Следует учитывать и другой важный момент: файлы cookie хранятся в веб-браузере, поэтому они не должны содержать конфиденциальные данные.

## <a name="store-the-retrieved-data-in-session-or-local-storage"></a>Хранение полученных данных в хранилище сеанса или локальном хранилище

Альтернатива использованию файлов cookie — хранение данных в хранилище сеанса или локальном хранилище. Как и в файлах cookie, в хранилище браузера можно оставить данные не только для последующих запросов, но и для разных страниц. Преимущество использования хранилища браузера состоит в том, что сохраненные данные не отправляются с исходящими запросами, а объем этих данных может быть больше, чем в файле cookie. В отличие от файлов cookie, хранилище браузера может содержать только строковые значения, поэтому для хранения более сложных объектов сначала нужно их сериализировать. Для этого можно использовать встроенный метод `JSON.stringify()`.

Если требуется сохранить данные только на время текущего сеанса, используйте хранилище сеанса. Если же данные должны храниться дольше, используйте локальное хранилище. Данные могут находиться в локальном хранилище в течение неограниченного времени, а решение об их удалении остается за вами.

Приведенную выше реализацию службы доступа к данным на основе файлов cookie можно легко адаптировать к использованию локального хранилища.

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

Реализация такой службы очень похожа на использование файлов cookie. Однако следует учитывать один момент: пользователь может отключить хранилище браузера, поэтому нужно всегда проверять его доступность, прежде чем выполнять с ним какие-либо операции. Как и файлы cookie, локальное хранилище остается в веб-браузере, поэтому его не следует использовать для конфиденциальных данных.

## <a name="see-also"></a>См. также

- [Руководство. Использование одних данных разными веб-частями с применением глобальной переменной](./tutorial-share-data-between-web-parts-global-variable.md)
