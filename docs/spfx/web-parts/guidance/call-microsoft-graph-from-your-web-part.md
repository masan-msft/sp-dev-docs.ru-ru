---
title: "Вызов API Microsoft Graph из веб-части с помощью OAuth"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 0fa5d369358ace2c3e13f279d4f1fcf0f20aef90
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="call-the-microsoft-graph-api-using-oauth-from-your-web-part"></a>Вызов API Microsoft Graph из веб-части с помощью OAuth

Благодаря интеграции с Microsoft Graph ваша веб-часть может работать с электронной почтой, документами, календарем и многими другими функциями. Для вызова API Microsoft Graph нужно использовать средство Active Directory Authentication Library (ADAL) для библиотеки JavaScript и аутентификацию с помощью потока OAuth. Для правильного и безопасного использования ADAL JS и вызова API Microsoft Graph необходимо учитывать некоторые особенности разработки и изменить код веб-части.

## <a name="azure-active-directory-authorization-flows"></a>Потоки авторизации на основе Azure Active Directory

Office 365 использует Azure Active Directory (Azure AD) для защиты API, доступных через Microsoft Graph. В Azure AD используется протокол авторизации OAuth. После авторизации OAuth приложение получает временный токен доступа. Токен обеспечивает доступ к определенным ресурсам от имени пользователя, используя разрешения, которые этот пользователь предоставил приложению.

Тип потока OAuth зависит от типа приложения. Веб-приложения используют поток OAuth, при котором Azure AD перенаправляет пользователей на URL-адрес приложения. Перенаправление — это дополнительная мера безопасности для проверки подлинности этого приложения.

У клиентских приложений, например Android и iOS, нет URL-адреса, поэтому поток OAuth в них выполняется без перенаправления. Как клиентские, так и веб-приложения используют общедоступный идентификатор клиента и частный секрет клиента, известный только Azure AD и приложению.

Клиентские веб-приложения похожи на веб-приложения, но реализованы с помощью JavaScript и запускаются в контексте браузера. Эти приложения не могут использовать секрет клиента, не сообщая его пользователям. Поэтому для доступа к ресурсам, защищенным с помощью Azure AD, эти приложения используют неявный поток OAuth. В этом потоке контракт между приложением и Azure AD устанавливается на основе общедоступного идентификатора клиента и URL-адреса приложения. Именно этот поток должны использовать клиентские веб-части SharePoint Framework для подключения к ресурсам, защищенным с помощью Azure AD. Чтобы реализовать в веб-части аутентификацию и авторизацию на основе Azure AD, можно использовать средство [Active Directory Authentication Library (ADAL) для JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) от корпорации Майкрософт.

## <a name="difference-between-client-side-applications-and-sharepoint-framework-web-parts"></a>Разница между клиентскими приложениями и веб-частями SharePoint Framework

Типичное клиентское веб-приложение занимает всю страницу и является единственным ресурсом, доступным по URL-адресу приложения. Все элементы страницы определяются на этапе разработки, и пользователи, работающие с приложением, не могут динамически добавлять новые элементы. Несмотря на то что клиентское веб-приложение может состоять из нескольких представлений, работать с внешними данными и иметь настраиваемые параметры, эти особенности продумываются разработчиками при создании приложения.

При работе с SharePoint пользователи создают страницы, добавляя и настраивая веб-части. Одна веб-часть — это всего лишь небольшая часть страницы. Разработчики веб-части не знают заранее, будут ли размещаться на этой странице другие веб-части и какие ресурсы они будут использовать. В отличие от надстроек SharePoint, веб-части являются частью страницы. Все веб-части могут получить доступ к модели DOM страницы, и ресурсы, загруженные одной веб-частью, доступны для других веб-частей.

## <a name="limitations-when-using-adal-js-with-sharepoint-framework-client-side-web-parts"></a>Ограничения при использовании ADAL JS с клиентскими веб-частями SharePoint Framework

Библиотека ADAL JS значительно упрощает внедрение потока OAuth для Azure AD в клиентских веб-приложениях. Но при использовании с клиентскими веб-частями SharePoint Framework действует ряд ограничений. Они связаны с тем, что ADAL JS предназначен для использования клиентскими веб-приложениями, которые занимают целую страницу и не делят ее с другими приложениями.

### <a name="shared-storage"></a>Общее хранилище

В зависимости от настроек проекта, библиотека ADAL JS хранит данные в локальном хранилище браузера или хранилище сеанса. В любом случае эти данные доступны для всех компонентов на странице. Например, если одна веб-часть получает токен доступа для Microsoft Graph, другая веб-часть на той же странице может использовать этот токен и вызвать Microsoft Graph.

### <a name="adal-js-as-a-singleton"></a>ADAL JS как одиночный объект

ADAL JS работает как служба-одиночный объект, зарегистрированный в глобальном контексте страницы. При обработке обратных вызовов потока OAuth в окнах IFrame код ADAL JS использует ссылку на зарегистрированный одиночный объект из главного окна, чтобы разрешить поток токена. Так как все веб-части зарегистрированы в разных приложениях Azure AD, использование одного экземпляра ADAL JS приводит к нежелательным результатам, когда все веб-части используют конфигурацию, зарегистрированную первой веб-частью, загруженной на странице.

### <a name="resource-based-storage"></a>Ресурсно-ориентированное хранение

По умолчанию библиотека ADAL JS хранит данные, такие как текущий токен доступа и его срок действия, в наборе ключей, связанных с определенным ресурсом, например Microsoft Graph или SharePoint. Если несколько компонентов на одной странице обращаются к одному ресурсу с разными разрешениями, все компоненты получат от ADAL JS первый токен. Если разным компонентам нужен доступ к одному ресурсу, может возникнуть ошибка. Чтобы проиллюстрировать это ограничение, рассмотрим приведенный ниже пример.

Предположим, что на странице две веб-части: одна отображает предстоящие собрания, а другая создает новые. Чтобы получить сведения о предстоящих собраниях, веб-часть использует токен доступа Microsoft Graph с разрешениями на чтение календарей пользователя. С другой стороны, веб-части, которая создает собрания, нужен токен доступа Microsoft Graph с разрешениями на запись в календарях пользователя. Если сначала загружается веб-часть предстоящих собраний, ADAL JS получает только разрешение на чтение. Затем веб-часть, которая создает собрания, получит от ADAL JS тот же токен. Как видите, когда веб-часть попытается создать собрание, возникнет ошибка "Отказано в доступе". Из-за ресурсно-ориентированного хранения ADAL JS не получит новый токен для Microsoft Graph, пока не истечет срок действия полученного ранее токена.

### <a name="processing-authorization-callbacks"></a>Обработка обратных вызовов авторизации

Неявный поток OAuth основан на перенаправлениях между Azure AD и приложением, участвующим в потоке. После запуска аутентификации приложение перенаправляет вас на страницу входа в Azure AD. После аутентификации Azure AD перенаправляет вас в приложение и отправляет токен идентификации в хэш URL-адреса для обработки в приложении. С точки зрения веб-части на странице SharePoint, это имеет два недостатка.

Несмотря на то что вы вошли в SharePoint, чтобы веб-часть получила доступ к ресурсам, защищенным с помощью Azure AD, нужно выполнить отдельную аутентификацию с помощью Azure AD. Веб-часть — это небольшая часть страницы, но чтобы выполнить аутентификацию, нужно покинуть страницу. Это неудобно для пользователей.

После аутентификации служба Azure AD перенаправляет вас обратно в приложение. В хэш URL-адреса она включает токен, который приложение должно обработать. К сожалению, так как токен не содержит сведений об источнике, если на одной странице несколько веб-частей, все они будут пытаться обработать токен идентификации из URL-адреса.

## <a name="use-adal-js-with-sharepoint-framework-client-side-web-parts"></a>Использование ADAL JS с клиентскими веб-частями SharePoint Framework

Ограничения ADAL JS можно обойти, чтобы успешно реализовать OAuth в клиентской веб-части SharePoint Framework.

> **Важно!** Приведенные ниже инструкции предполагают использование ADAL JS версии 1.0.12. Добавляя ADAL JS к проектам SharePoint Framework, устанавливайте ADAL JS версии 1.0.12. В противном случае выполнение представленных в этой статье инструкций не приведет к нужному результату.

### <a name="load-adal-js-in-your-web-part"></a>Загрузка ADAL JS в веб-части

Веб-части создаются на основе TypeScript и распространяются как модули AMD. Их модульная архитектура позволяет изолировать различные ресурсы, используемые веб-частью. ADAL JS регистрируется в глобальном контексте, но ее можно загрузить в веб-части, используя следующий код:

```ts
import * as AuthenticationContext from 'adal-angular';
```

Этот оператор импортирует класс `AuthenticationContext`, который позволяет использовать функциональность ADAL JS в веб-частях. Несмотря на имя модуля, класс `AuthenticationContext` работает со всеми библиотеками JavaScript.

### <a name="make-adal-js-suitable-for-use-with-sharepoint-framework-web-parts"></a>Как использовать ADAL JS с веб-частями SharePoint Framework

Текущую функциональность ADAL JS нельзя использовать в веб-частях. Используйте приведенное ниже исправление.

**WebPartAuthenticationContext.js:**
```js
const AuthenticationContext = require('adal-angular');

AuthenticationContext.prototype._getItemSuper = AuthenticationContext.prototype._getItem;
AuthenticationContext.prototype._saveItemSuper = AuthenticationContext.prototype._saveItem;
AuthenticationContext.prototype.handleWindowCallbackSuper = AuthenticationContext.prototype.handleWindowCallback;
AuthenticationContext.prototype._renewTokenSuper = AuthenticationContext.prototype._renewToken;
AuthenticationContext.prototype.getRequestInfoSuper = AuthenticationContext.prototype.getRequestInfo;
AuthenticationContext.prototype._addAdalFrameSuper = AuthenticationContext.prototype._addAdalFrame;

AuthenticationContext.prototype._getItem = function (key) {
  if (this.config.webPartId) {
    key = this.config.webPartId + '_' + key;
  }

  return this._getItemSuper(key);
};

AuthenticationContext.prototype._saveItem = function (key, object) {
  if (this.config.webPartId) {
    key = this.config.webPartId + '_' + key;
  }

  return this._saveItemSuper(key, object);
};

AuthenticationContext.prototype.handleWindowCallback = function (hash) {
  if (hash == null) {
    hash = window.location.hash;
  }

  if (!this.isCallback(hash)) {
    return;
  }

  var requestInfo = this.getRequestInfo(hash);
  if (requestInfo.requestType === this.REQUEST_TYPE.LOGIN) {
    return this.handleWindowCallbackSuper(hash);
  }

  var resource = this._getResourceFromState(requestInfo.stateResponse);
  if (!resource || resource.length === 0) {
    return;
  }

  if (this._getItem(this.CONSTANTS.STORAGE.RENEW_STATUS + resource) === this.CONSTANTS.TOKEN_RENEW_STATUS_IN_PROGRESS) {
    return this.handleWindowCallbackSuper(hash);
  }
}

AuthenticationContext.prototype._renewToken = function (resource, callback) {
  this._renewTokenSuper(resource, callback);
  var _renewStates = this._getItem('renewStates');
  if (_renewStates) {
    _renewStates = _renewStates.split(',');
  }
  else {
    _renewStates = [];
  }
  _renewStates.push(this.config.state);
  this._saveItem('renewStates', _renewStates);
}

AuthenticationContext.prototype.getRequestInfo = function (hash) {
  var requestInfo = this.getRequestInfoSuper(hash);
  var _renewStates = this._getItem('renewStates');
  if (!_renewStates) {
    return requestInfo;
  }

  _renewStates = _renewStates.split(';');
  for (var i = 0; i < _renewStates.length; i++) {
    if (_renewStates[i] === requestInfo.stateResponse) {
      requestInfo.requestType = this.REQUEST_TYPE.RENEW_TOKEN;
      requestInfo.stateMatch = true;
      break;
    }
  }

  return requestInfo;
}

AuthenticationContext.prototype._addAdalFrame = function (iframeId) {
  var adalFrame = this._addAdalFrameSuper(iframeId);
  adalFrame.style.width = adalFrame.style.height = '106px';
  return adalFrame;
}

window.AuthenticationContext = function() {
  return undefined;
}
```

После исправления в ADAL JS происходят следующие изменения:
- вся информация хранится в ключе веб-части (см. переопределение функций `_getItem` и `_saveItem`);
- обратные вызовы обрабатываются только веб-частями, которые их инициировали (см. переопределение функции `handleWindowCallback`);
- при проверке данных из обратных вызовов используется не одиночный объект, зарегистрированный в глобальном контексте, а экземпляр класса `AuthenticationContext` определенной веб-части (см. `_renewToken`, `getRequestInfo` и пустую регистрацию функции `window.AuthenticationContext`).

### <a name="use-the-adal-js-patch-in-sharepoint-framework-web-parts"></a>Использование исправления ADAL JS в веб-частях SharePoint Framework

Чтобы средство ADAL JS работало правильно в веб-частях SharePoint Framework, его необходимо определенным образом настроить. Для этого сначала необходимо определить пользовательский интерфейс, который расширяет стандартный интерфейс ADAL JS `Config`, чтобы предоставить объекту конфигурации дополнительные свойства.

```ts
export interface IAdalConfig extends adal.Config {
  popUp?: boolean;
  callback?: (error: any, token: string) => void;
  webPartId?: string;
}
```

Свойство `popUp` и функция `callback` уже реализованы в ADAL JS, но не доступны в определениях типа TypeScript стандартного интерфейса Config. Они нужны, чтобы пользователи могли входить в веб-части, используя всплывающее окно, а не перенаправление на страницу входа в Azure AD.

Далее загрузите исправление ADAL JS, пользовательский интерфейс конфигурации и объект конфигурации в основной компонент веб-части.

```tsx
import * as AuthenticationContext from 'adal-angular';
import adalConfig from '../AdalConfig';
import { IAdalConfig } from '../../IAdalConfig';
import '../../WebPartAuthenticationContext';
```

В конструкторе компонента дополните конфигурацию ADAL JS и используйте ее для создания нового экземпляра класса `AuthenticationContext`.

```tsx
export default class UpcomingMeetings extends React.Component<IUpcomingMeetingsProps, IUpcomingMeetingsState> {
  private authCtx: adal.AuthenticationContext;

  constructor(props: IUpcomingMeetingsProps, state: IUpcomingMeetingsState) {
    super(props);

    this.state = {
      loading: false,
      error: null,
      upcomingMeetings: [],
      signedIn: false
    };

    const config: IAdalConfig = adalConfig;
    config.webPartId = this.props.webPartId;
    config.popUp = true;
    config.callback = (error: any, token: string): void => {
      this.setState((previousState: IUpcomingMeetingsState, currentProps: IUpcomingMeetingsProps): IUpcomingMeetingsState => {
        previousState.error = error;
        previousState.signedIn = !(!this.authCtx.getCachedUser());
        return previousState;
      });
    };

    this.authCtx = new AuthenticationContext(config);
    AuthenticationContext.prototype._singletonInstance = undefined;
  }
}
```

Сначала код извлекает стандартный объект конфигурации ADAL JS и приводит его к типу нового интерфейса конфигурации. Затем он передает идентификатор экземпляра веб-части, чтобы все значения ADAL JS могли храниться, не конфликтуя с другими веб-частями на странице. Далее он включает аутентификацию с помощью всплывающего окна и определяет функцию обратного вызова, которая запускается после аутентификации для обновления компонента. Наконец, он создает новый экземпляр класса `AuthenticationContext` и сбрасывает набор `_singletonInstance` в конструкторе класса `AuthenticationContext`. Это необходимо, чтобы каждая веб-часть могла использовать собственную версию контекста аутентификации ADAL JS.

## <a name="considerations-when-using-oauth-implicit-flow-in-sharepoint-framework-client-side-web-parts"></a>Что нужно учитывать при использовании неявного потока OAuth в клиентских веб-частях SharePoint Framework

При создании клиентских веб-частей SharePoint Framework, которые взаимодействуют с ресурсами, защищенными Azure AD, следует учитывать некоторые ограничения. Приведенная ниже информация поможет вам определить, подходит ли авторизация OAuth для вашей веб-части и организации.

### <a name="sharepoint-framework-web-parts-are-highly-trusted"></a>Веб-части SharePoint Framework с высоким уровнем доверия

В отличие от надстроек SharePoint, веб-части получают те же разрешения, что и текущий пользователь. Они могут выполнять любые действия, доступные пользователю. Поэтому веб-части могут устанавливать и развертывать только администраторы клиента. Они должны убедиться, что веб-части получены из надежного источника и утверждены для использования в клиенте.

Веб-части входят в состав страницы и, в отличие от надстроек SharePoint, используют модель DOM и ресурсы совместно с другими элементами на странице. Токены, которые предоставляют доступ к ресурсам, защищенным с помощью Azure AD, извлекаются через обратный вызов, посылаемый на страницу веб-части. Этот обратный вызов может быть обработан любым элементом на странице. Кроме того, после обработки токены доступа хранятся в локальном хранилище браузера или хранилище сеанса, из которого их может получить любой компонент на странице. Вредоносная веб-часть может прочитать токен и предоставить его или полученные с его помощью данные внешней службе.

### <a name="url-is-a-part-of-the-oauth-implicit-flow-contract"></a>URL-адрес — это часть контракта неявного потока OAuth

Клиентские приложения не могут хранить секрет клиента, не сообщая его пользователям. Чтобы проверить подлинность приложения, его URL-адрес включается в контракт доверия между Azure AD и приложением. В результате URL-адрес каждой страницы с веб-частями, использующими неявный поток OAuth, должен быть зарегистрирован в Azure AD. В противном случае произойдет сбой потока OAuth и веб-части будет отказано в доступе к защищенному ресурсу.

Эта необходимая мера безопасности — существенное ограничение для организаций, которые разрешают пользователям добавлять веб-части на страницы. Рекомендуем ограничить количество страниц с веб-частями, которые используют неявный поток OAuth. Используйте домашнюю страницу или определенные целевые страницы и зарегистрируйте их в Azure AD.

### <a name="internet-explorer-security-zones"></a>Зоны безопасности Internet Explorer

Браузер Internet Explorer применяет политики безопасности к посещаемым веб-сайтам, основываясь на зонах безопасности. Веб-сайты, которые относятся к разным зонам безопасности, запускаются в изолированных средах и не взаимодействуют между собой. При использовании неявного потока OAuth в клиентских веб-частях SharePoint Framework страница с веб-частями, использующими OAuth, и страница для входа в Azure AD (https://login.microsoftonline.com) должны находиться в одной зоне безопасности. В противном случае выполнить аутентификацию не удастся, и веб-часть не сможет взаимодействовать с ресурсами, защищенными с помощью Azure AD.

### <a name="user-must-sign-in-frequently"></a>Пользователь должен входить в приложение часто

В обычном потоке OAuth веб-приложения и клиентские приложения получают токен доступа с коротким сроком действия и токен обновления, действительный в течение более длительного периода времени. Когда срок действия токена доступа истекает, для получения нового используется токен обновления. При таком подходе пользователи могут входить в Azure AD реже.

Так как клиентские приложения не могут хранить секреты, а раскрытие токена обновления представляет собой серьезную угрозу безопасности, они получают токен доступа только в неявном потоке OAuth. Когда срок действия этого токена закончится, приложение запустит новый поток OAuth, и пользователю придется войти в него снова.

## <a name="more-information"></a>Дополнительные сведения

- [Сценарии аутентификации для Azure AD](https://Azure.microsoft.com/ru-RU/documentation/articles/active-directory-authentication-scenarios/)
