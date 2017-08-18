# <a name="call-microsoft-graph-using-the-sharepoint-framework-graphhttpclient"></a>Вызов Microsoft Graph с помощью клиента GraphHttpClient на платформе SharePoint Framework

С помощью Microsoft Graph вы можете создавать функциональные решения, использующие данные из различных служб, входящих в состав Office 365. В прошлом подключать решения SharePoint Framework к Microsoft Graph было сложно, так как для этого требовалось зарегистрировать приложение Azure Active Directory и выполнить поток авторизации. Благодаря клиенту GraphHttpClient на платформе SharePoint Framework вы можете вызывать Microsoft Graph напрямую без дополнительной настройки.

> **Важно!** В настоящее время GraphHttpClient находится на этапе тестирования разработчиками. Его не следует использовать в рабочей среде.

## <a name="what-is-graphhttpclient"></a>Что такое GraphHttpClient

GraphHttpClient — это специальный HTTP-клиент, входящий в состав SharePoint Framework. Он работает аналогично клиенту HttpClient, используемому для связи со сторонними API. Этот клиент, основанный на HttpClient, автоматически обеспечивает наличие действительного маркера доступа носителя и необходимых заголовков в запросе к Microsoft Graph. Когда вы отправляете запрос GET или POST, GraphHttpClient проверяет наличие действительного маркера доступа и, в случае его отсутствия, автоматически получает маркер из внутреннего API и сохраняет его для последующих запросов.

Ниже представлен пример запроса к Microsoft Graph с использованием GraphHttpClient.

```ts
// ...
import { GraphHttpClient, GraphClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

Для начала из пакета **@microsoft/sp-http** импортируются модули **GraphHttpClient** и **GraphClientResponse**. Затем с помощью экземпляра GraphHttpClient, доступного в свойстве `this.context.graphHttpClient`, запрос GET или POST отправляется в Microsoft Graph. В качестве параметров указываются вызываемый API Microsoft Graph (начиная с версии API без начального символа `/`) и конфигурация GraphHttpClient. При желании можно указать дополнительные заголовки запроса, которые будут объединены с заголовками по умолчанию, заданными клиентом GraphHttpClient (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` и `'Content-Type': 'application/json; charset=utf-8'`).

## <a name="graphhttpclient-considerations"></a>Замечания касательно GraphHttpClient

Использование GraphHttpClient — очень удобный способ связи с Microsoft Graph, так как он позволяет абстрагироваться от потока авторизации и управления маркерами доступа. В настоящее время GraphHttpClient находится на этапе тестирования разработчиками, и перед его использованием следует учитывать некоторые особенности.

### <a name="use-for-microsoft-graph-access-only"></a>Использование только для доступа к Microsoft Graph

GraphHttpClient предназначен только для доступа к Microsoft Graph. Указанный в запросе URL-адрес должен начинаться с версии API Microsoft Graph (**v1.0** или **beta**), за которой следует операция API. Все остальные URL-адреса отклоняются с ошибкой.

### <a name="available-permission-scopes"></a>Доступные области разрешений

GraphHttpClient использует приложение **Office 365 SharePoint Online** для Azure Active Directory, чтобы получить действительный маркер доступа к Microsoft Graph от имени текущего пользователя. Полученный маркер доступа содержит две области разрешений: 

* **Чтение и запись всех групп (предварительная версия)** (`Group.ReadWrite.All`) 
* **Чтение всех отчетов об использовании** (`Reports.Read.All`) 

В настоящее время при использовании GraphHttpClient доступно только две области разрешений. Если для вашего решения необходимы другие области разрешений, следует использовать [ADAL JS с неявным потоком OAuth](web-parts/guidance/call-microsoft-graph-from-your-web-part).

### <a name="tokens-are-retrieved-using-an-internal-api"></a>Извлечение маркеров с помощью внутреннего API

Чтобы получить действительный маркер доступа, GraphHttpClient отправляет веб-запрос конечной точке `/_api/SP.OAuth.Token/Acquire`. Этот API предназначен для внутреннего использования, и к нему не следует обращаться напрямую в решениях.

## <a name="more-information"></a>Дополнительные сведения

Пример практического использования GraphHttpClient можно увидеть в образце решения на сайте GitHub по адресу [https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).

Дополнительные сведения о Microsoft Graph см. на странице [https://developer.microsoft.com/ru-ru/graph/](https://developer.microsoft.com/en-us/graph/).