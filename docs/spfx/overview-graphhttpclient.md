# <a name="overview-of-the-graphhttpclient-class-preview"></a>Общие сведения о классе GraphHttpClient (ознакомительная версия)

> [!IMPORTANT]
> Класс **GraphHttpClient** находится на этапе тестирования, и в него могут быть внесены изменения. Сейчас он не поддерживается для использования в рабочих средах.

Вы можете использовать Microsoft Graph для создания решений с широкими возможностями, получающих доступ к данным в Office 365 и других службах Майкрософт. Чтобы подключить решения SharePoint Framework (SPFx) к Microsoft Graph, вам необходимо зарегистрировать приложение Azure Active Directory (Azure AD) и выполнить поток авторизации. Чтобы упростить этот процесс, вы можете использовать класс SPFx **GraphHttpClient** для непосредственного вызова Microsoft Graph без дополнительной настройки.

## <a name="what-is-the-graphhttpclient-class"></a>Что представляет собой класс GraphHttpClient?

Класс **GraphHttpClient** входит в состав SharePoint Framework. Он работает аналогично классу HttpClient, который вы можете использовать для взаимодействия с API сторонних разработчиков. Класс **GraphHttpClient** автоматически обеспечивает допустимый маркер доступа носителя и необходимые заголовки в вашем запросе к Microsoft Graph. При совершении запроса GET или POST класс **GraphHttpClient** проверяет, есть ли в запросе допустимый маркер доступа, и если его нет, класс автоматически получает маркер доступа из внутреннего API и сохраняет его для последующих запросов.

В примере ниже показан запрос к Microsoft Graph, в котором используется класс **GraphHttpClient**.

```ts
// ...
import { GraphHttpClient, GraphHttpClientResponse } from '@microsoft/sp-http';

export default class MyApplicationCustomizer
  extends BaseApplicationCustomizer<IMyApplicationCustomizerProperties> {

  // ...

  @override
  public onRender(): void {
    this.context.graphHttpClient.get("v1.0/groups?$select=displayName", GraphHttpClient.configurations.v1)
      .then((response: GraphHttpClientResponse): Promise<any> => {
        return response.json();
      })
      .then((data: any): void => {
        // ...
      });
  }
}
```

Чтобы совершить запрос к Microsoft Graph, выполните указанные ниже действия.

- Импортируйте класс **GraphHttpClient** и модули **GraphHttpClientResponse** из пакета **@microsoft/sp-http**.
- Используйте экземпляр класса **GraphHttpClient**, доступный в свойстве `this.context.graphHttpClient`, чтобы создать запрос GET или POST к Microsoft Graph.
- В качестве параметров укажите API Microsoft Graph, который вы хотите вызвать (начните работу с версии API без ведущей косой черты `/`), а затем укажите конфигурацию **GraphHttpClient**.
- При необходимости вы можете указать дополнительные заголовки запроса, которые будут объединены с заголовками, используемыми по умолчанию и заданными классом **GraphHttpClient** (`'Accept': 'application/json'`, `'Authorization': 'Bearer [token]'` и `'Content-Type': 'application/json; charset=utf-8'`).

## <a name="considerations-for-using-the-graphhttpclient-class"></a>Вопросы, связанные с использованием класса **GraphHttpClient**

Класс **GraphHttpClient** обеспечивает удобный способ взаимодействия с Microsoft Graph, так как он абстрагирует поток авторизации и управление маркерами доступа. Так как на данный момент класс **GraphHttpClient** находится на этапе тестирования и представлен в виде ознакомительной версии для разработчиков, имеется ряд моментов, которые необходимо учесть перед его использованием.

### <a name="use-for-microsoft-graph-access-only"></a>Использование только для доступа к Microsoft Graph

Используйте класс **GraphHttpClient** только для доступа к Microsoft Graph. URL-адрес, указанный в запросе, должен начинаться с версии API Microsoft Graph (**v1.0** или **beta**), за которым должна следовать операция API. При использовании любого другого URL-адреса будет возвращена ошибка.

### <a name="permissions"></a>Разрешения

Класс GraphHttpClient использует приложение Azure AD для SharePoint Online в Office 365, чтобы получать допустимые маркеры доступа для Microsoft Graph от имени текущего пользователя. Полученный маркер доступа содержит два указанных ниже разрешения.

- Чтение из всех групп и запись во все группы (ознакомительная версия) (`Group.ReadWrite.All`)
- Чтение всех отчетов об использовании (`Reports.Read.All`)

Это только те разрешения, которые доступны, когда вы используете класс **GraphHttpClient**. Если для вашего решения необходимы другие разрешения, вы можете использовать [ADAL JS с неявным потоком OAuth](web-parts/guidance/call-microsoft-graph-from-your-web-part.md).

### <a name="tokens-are-retrieved-using-an-internal-api"></a>Получение маркеров с помощью внутреннего API

Чтобы получить допустимый маркер доступа, класс **GraphHttpClient** создает веб-запрос к конечной точке `/_api/SP.OAuth.Token/Acquire`. Этот API предназначен для внутреннего использования. В ваших решениях не следует взаимодействовать непосредственно с этим API.

## <a name="see-also"></a>См. также

- [Класс GraphClient настройщика приложений из примера современного сайта группы](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/js-application-graph-client).
- [Вызов Microsoft Graph с помощью клиента GraphHttpClient на платформе SharePoint Framework](call-microsoft-graph-using-graphhttpclient.md)
- [Центр разработки для Microsoft Graph](https://developer.microsoft.com/ru-RU/graph/)
