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
# <a name="call-the-microsoft-graph-api-using-oauth-from-your-web-part"></a><span data-ttu-id="b8981-102">Вызов API Microsoft Graph из веб-части с помощью OAuth</span><span class="sxs-lookup"><span data-stu-id="b8981-102">Call the Microsoft Graph API using OAuth from your web part</span></span>

<span data-ttu-id="b8981-p101">Благодаря интеграции с Microsoft Graph ваша веб-часть может работать с электронной почтой, документами, календарем и многими другими функциями. Для вызова API Microsoft Graph нужно использовать средство Active Directory Authentication Library (ADAL) для библиотеки JavaScript и аутентификацию с помощью потока OAuth. Для правильного и безопасного использования ADAL JS и вызова API Microsoft Graph необходимо учитывать некоторые особенности разработки и изменить код веб-части.</span><span class="sxs-lookup"><span data-stu-id="b8981-p101">You can add lots of great functionality such as email, documents, and calendar to your web part by integrating with the Microsoft Graph. To call APIs on Microsoft Graph you will need to use the Active Directory Authentication Library (ADAL) for JavaScript library and authenticate using the OAuth flow. There are some design considerations and code modifications to make for your web part to use ADAL JS and call Microsoft Graph APIs correctly and securely.</span></span>

## <a name="azure-active-directory-authorization-flows"></a><span data-ttu-id="b8981-106">Потоки авторизации на основе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8981-106">Azure Active Directory authorization flows</span></span>

<span data-ttu-id="b8981-p102">Office 365 использует Azure Active Directory (Azure AD) для защиты API, доступных через Microsoft Graph. В Azure AD используется протокол авторизации OAuth. После авторизации OAuth приложение получает временный токен доступа. Токен обеспечивает доступ к определенным ресурсам от имени пользователя, используя разрешения, которые этот пользователь предоставил приложению.</span><span class="sxs-lookup"><span data-stu-id="b8981-p102">Office 365 uses Azure Active Directory (Azure AD) to secure its APIs, which are accessed through the Microsoft Graph. Azure AD uses OAuth as the authorization protocol. When an application completes the OAuth authorization flow it gets a temporary access token. The token provides access to specific resources on behalf of the user by using permissions granted to the application by that user.</span></span>

<span data-ttu-id="b8981-p103">Тип потока OAuth зависит от типа приложения. Веб-приложения используют поток OAuth, при котором Azure AD перенаправляет пользователей на URL-адрес приложения. Перенаправление — это дополнительная мера безопасности для проверки подлинности этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b8981-p103">There are different types of OAuth flows depending on the kind of application. Web applications use an OAuth flow where Azure AD redirects to the URL where the application is hosted. The redirect is an additional security measure to verify the authenticity of that application.</span></span>

<span data-ttu-id="b8981-p104">У клиентских приложений, например Android и iOS, нет URL-адреса, поэтому поток OAuth в них выполняется без перенаправления. Как клиентские, так и веб-приложения используют общедоступный идентификатор клиента и частный секрет клиента, известный только Azure AD и приложению.</span><span class="sxs-lookup"><span data-stu-id="b8981-p104">Client applications, such as Android and iOS apps, do not have a URL and cannot use a redirect. So they complete the OAuth flow without the redirect. Both web applications and client applications use a publicly known client ID and a privately held client secret known only to Azure AD and the application.</span></span>

<span data-ttu-id="b8981-117">Клиентские веб-приложения похожи на веб-приложения, но реализованы с помощью JavaScript и запускаются в контексте браузера.</span><span class="sxs-lookup"><span data-stu-id="b8981-117">Client-side web applications are similar to web applications but are implemented using JavaScript and run in the context of a browser.</span></span> <span data-ttu-id="b8981-118">Эти приложения не могут использовать секрет клиента, не сообщая его пользователям.</span><span class="sxs-lookup"><span data-stu-id="b8981-118">These applications are incapable of using a client secret without revealing it to users.</span></span> <span data-ttu-id="b8981-119">Поэтому для доступа к ресурсам, защищенным с помощью Azure AD, эти приложения используют неявный поток OAuth.</span><span class="sxs-lookup"><span data-stu-id="b8981-119">Therefore these applications use an authorization flow called OAuth implicit flow to access resources secured with Azure AD.</span></span> <span data-ttu-id="b8981-120">В этом потоке контракт между приложением и Azure AD устанавливается на основе общедоступного идентификатора клиента и URL-адреса приложения.</span><span class="sxs-lookup"><span data-stu-id="b8981-120">In this flow the contract between the application and Azure AD is established based on the publicly-known client ID and the URL where the application is hosted.</span></span> <span data-ttu-id="b8981-121">Именно этот поток должны использовать клиентские веб-части SharePoint Framework для подключения к ресурсам, защищенным с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8981-121">This is the flow that SharePoint Framework client-side web parts must use in order to connect to resources secured with Azure AD.</span></span> <span data-ttu-id="b8981-122">Чтобы реализовать в веб-части аутентификацию и авторизацию на основе Azure AD, можно использовать средство [Active Directory Authentication Library (ADAL) для JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b8981-122">To implement Azure AD-based authentication and authorization in your web part, you can use the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js) provided by Microsoft.</span></span>

## <a name="difference-between-client-side-applications-and-sharepoint-framework-web-parts"></a><span data-ttu-id="b8981-123">Разница между клиентскими приложениями и веб-частями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b8981-123">Difference between client-side applications and SharePoint Framework web parts</span></span>

<span data-ttu-id="b8981-p106">Типичное клиентское веб-приложение занимает всю страницу и является единственным ресурсом, доступным по URL-адресу приложения. Все элементы страницы определяются на этапе разработки, и пользователи, работающие с приложением, не могут динамически добавлять новые элементы. Несмотря на то что клиентское веб-приложение может состоять из нескольких представлений, работать с внешними данными и иметь настраиваемые параметры, эти особенности продумываются разработчиками при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="b8981-p106">A typical client-side web application owns the whole page and is the only resource available at the application's URL. All elements of the page are determined during development and users working with the application cannot dynamically add new elements. Even though a client-side web application might consist of several views, work with external data, and offer a certain degree of configuration, these aspects are considered by developers while building the application.</span></span>

<span data-ttu-id="b8981-p107">При работе с SharePoint пользователи создают страницы, добавляя и настраивая веб-части. Одна веб-часть — это всего лишь небольшая часть страницы. Разработчики веб-части не знают заранее, будут ли размещаться на этой странице другие веб-части и какие ресурсы они будут использовать. В отличие от надстроек SharePoint, веб-части являются частью страницы. Все веб-части могут получить доступ к модели DOM страницы, и ресурсы, загруженные одной веб-частью, доступны для других веб-частей.</span><span class="sxs-lookup"><span data-stu-id="b8981-p107">When working with SharePoint, users compose pages by adding and configuring web parts. A single web part is only a small part of the whole page. Developers building a web part cannot know up front if other web parts will be placed on the same page, and if so, which resources those web parts will use. Unlike SharePoint Add-ins, web parts are a part of the page. All web parts can access the page's DOM, and resources loaded by one web part are available to other web parts.</span></span>

## <a name="limitations-when-using-adal-js-with-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="b8981-132">Ограничения при использовании ADAL JS с клиентскими веб-частями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b8981-132">Limitations when using ADAL JS with SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="b8981-p108">Библиотека ADAL JS значительно упрощает внедрение потока OAuth для Azure AD в клиентских веб-приложениях. Но при использовании с клиентскими веб-частями SharePoint Framework действует ряд ограничений. Они связаны с тем, что ADAL JS предназначен для использования клиентскими веб-приложениями, которые занимают целую страницу и не делят ее с другими приложениями.</span><span class="sxs-lookup"><span data-stu-id="b8981-p108">The ADAL JS library significantly simplifies implementing the OAuth flow for Azure AD in client-side web applications. But it has a number of limitations when used with SharePoint Framework client-side web parts. These limitations are due to the fact that ADAL JS is designed to be used by client-side web applications that own the whole page and do not share the page with other applications.</span></span>

### <a name="shared-storage"></a><span data-ttu-id="b8981-136">Общее хранилище</span><span class="sxs-lookup"><span data-stu-id="b8981-136">Shared storage</span></span>

<span data-ttu-id="b8981-p109">В зависимости от настроек проекта, библиотека ADAL JS хранит данные в локальном хранилище браузера или хранилище сеанса. В любом случае эти данные доступны для всех компонентов на странице. Например, если одна веб-часть получает токен доступа для Microsoft Graph, другая веб-часть на той же странице может использовать этот токен и вызвать Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b8981-p109">Depending on how you configured the ADAL JS library in your project, it will store its data either in the browser's local storage or in the session storage. Either way, the information stored by ADAL JS is accessible to any component on the same page. For example, if one web part retrieves an access token for Microsoft Graph, then any other web part on the same page can reuse that token and call the Microsoft Graph.</span></span>

### <a name="adal-js-as-a-singleton"></a><span data-ttu-id="b8981-140">ADAL JS как одиночный объект</span><span class="sxs-lookup"><span data-stu-id="b8981-140">ADAL JS as a singleton</span></span>

<span data-ttu-id="b8981-p110">ADAL JS работает как служба-одиночный объект, зарегистрированный в глобальном контексте страницы. При обработке обратных вызовов потока OAuth в окнах IFrame код ADAL JS использует ссылку на зарегистрированный одиночный объект из главного окна, чтобы разрешить поток токена. Так как все веб-части зарегистрированы в разных приложениях Azure AD, использование одного экземпляра ADAL JS приводит к нежелательным результатам, когда все веб-части используют конфигурацию, зарегистрированную первой веб-частью, загруженной на странице.</span><span class="sxs-lookup"><span data-stu-id="b8981-p110">ADAL JS is designed to work as a singleton service registered in the global scope of the page. When processing OAuth flow callbacks in IFrames, ADAL JS code uses the registered singleton reference from the main window to resolve the token flow. Since each web part is registered with a different Azure AD application, reusing the same instance of ADAL JS leads to undesirable results where every web part uses the same configuration as the one registered by the first web part loaded on the page.</span></span>

### <a name="resource-based-storage"></a><span data-ttu-id="b8981-144">Ресурсно-ориентированное хранение</span><span class="sxs-lookup"><span data-stu-id="b8981-144">Resource-based storage</span></span>

<span data-ttu-id="b8981-p111">По умолчанию библиотека ADAL JS хранит данные, такие как текущий токен доступа и его срок действия, в наборе ключей, связанных с определенным ресурсом, например Microsoft Graph или SharePoint. Если несколько компонентов на одной странице обращаются к одному ресурсу с разными разрешениями, все компоненты получат от ADAL JS первый токен. Если разным компонентам нужен доступ к одному ресурсу, может возникнуть ошибка. Чтобы проиллюстрировать это ограничение, рассмотрим приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="b8981-p111">By default, the ADAL JS library stores information such as the current access token or its expiration time in a set of keys associated with the particular resource, for example Microsoft Graph or SharePoint. If there are multiple components on one page accessing the same resource with different permissions, then the first retrieved token will be served by ADAL JS to all components. If different components require access to the same resource, then they might fail. To illustrate this limitation, consider the following example.</span></span>

<span data-ttu-id="b8981-p112">Предположим, что на странице две веб-части: одна отображает предстоящие собрания, а другая создает новые. Чтобы получить сведения о предстоящих собраниях, веб-часть использует токен доступа Microsoft Graph с разрешениями на чтение календарей пользователя. С другой стороны, веб-части, которая создает собрания, нужен токен доступа Microsoft Graph с разрешениями на запись в календарях пользователя. Если сначала загружается веб-часть предстоящих собраний, ADAL JS получает только разрешение на чтение. Затем веб-часть, которая создает собрания, получит от ADAL JS тот же токен. Как видите, когда веб-часть попытается создать собрание, возникнет ошибка "Отказано в доступе". Из-за ресурсно-ориентированного хранения ADAL JS не получит новый токен для Microsoft Graph, пока не истечет срок действия полученного ранее токена.</span><span class="sxs-lookup"><span data-stu-id="b8981-p112">Imagine that there are two web parts on the page: one that lists upcoming meetings, and one that creates a new meeting. To get upcoming meetings, the upcoming meetings web part uses a Microsoft Graph access token with permissions to read user's calendars. The web part that creates new meetings on the other hand, requires a Microsoft Graph access token with permissions to write to user's calendars. If the upcoming meetings web part loads first then ADAL JS retrieves its token with only the read permission. The same token is then served by ADAL JS to the web part creating new meetings. As you can see, when the web part attempts to create a new meeting the web part will fail with an access denied error. Because of the resource-based storage, ADAL JS wouldn't retrieve a new token for Microsoft Graph until the previously retrieved token expired.</span></span>

### <a name="processing-authorization-callbacks"></a><span data-ttu-id="b8981-156">Обработка обратных вызовов авторизации</span><span class="sxs-lookup"><span data-stu-id="b8981-156">Processing authorization callbacks</span></span>

<span data-ttu-id="b8981-p113">Неявный поток OAuth основан на перенаправлениях между Azure AD и приложением, участвующим в потоке. После запуска аутентификации приложение перенаправляет вас на страницу входа в Azure AD. После аутентификации Azure AD перенаправляет вас в приложение и отправляет токен идентификации в хэш URL-адреса для обработки в приложении. С точки зрения веб-части на странице SharePoint, это имеет два недостатка.</span><span class="sxs-lookup"><span data-stu-id="b8981-p113">OAuth implicit flow is based on redirects between Azure AD and the application participating in the flow. When the authentication process starts, the application redirects you to the Azure AD sign-in page. Once the authentication completes, Azure AD redirects you back to the application, and sends the identity token in the URL hash for the application to process. From the perspective of a web part placed on a SharePoint page this behavior has two drawbacks.</span></span>

<span data-ttu-id="b8981-p114">Несмотря на то что вы вошли в SharePoint, чтобы веб-часть получила доступ к ресурсам, защищенным с помощью Azure AD, нужно выполнить отдельную аутентификацию с помощью Azure AD. Веб-часть — это небольшая часть страницы, но чтобы выполнить аутентификацию, нужно покинуть страницу. Это неудобно для пользователей.</span><span class="sxs-lookup"><span data-stu-id="b8981-p114">Even though you are signed in to SharePoint, you need to separately authenticate with Azure AD in order for your web part to be able to access resources secured with Azure AD. The web part is a small part of the overall page, but in order to complete the authentication process, you would need to leave the whole page which is a poor user experience.</span></span>

<span data-ttu-id="b8981-p115">После аутентификации служба Azure AD перенаправляет вас обратно в приложение. В хэш URL-адреса она включает токен, который приложение должно обработать. К сожалению, так как токен не содержит сведений об источнике, если на одной странице несколько веб-частей, все они будут пытаться обработать токен идентификации из URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="b8981-p115">After the authentication completes, Azure AD redirects you back to your application. In the URL hash it includes the identity token that your application needs to process. Unfortunately, as the identity token doesn't contain any information about its origin, if you had multiple web parts on one page, all of them would try to process the identity token from the URL.</span></span>

## <a name="use-adal-js-with-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="b8981-166">Использование ADAL JS с клиентскими веб-частями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b8981-166">Use ADAL JS with SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="b8981-167">Ограничения ADAL JS можно обойти, чтобы успешно реализовать OAuth в клиентской веб-части SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="b8981-167">You can overcome the limitations in ADAL JS to implement OAuth successfully in your SharePoint Framework client-side web part.</span></span>

> <span data-ttu-id="b8981-168">**Важно!** Приведенные ниже инструкции предполагают использование ADAL JS версии 1.0.12.</span><span class="sxs-lookup"><span data-stu-id="b8981-168">**Important:** The following guidance is based on ADAL JS v1.0.12.</span></span> <span data-ttu-id="b8981-169">Добавляя ADAL JS к проектам SharePoint Framework, устанавливайте ADAL JS версии 1.0.12. В противном случае выполнение представленных в этой статье инструкций не приведет к нужному результату.</span><span class="sxs-lookup"><span data-stu-id="b8981-169">Important: The following guidance is based on ADAL JS v1.0.12. When adding ADAL JS to your SharePoint Framework projects, ensure that you're installing ADAL JS v1.0.12 or the guidance mentioned in this article will not work as expected.</span></span>

### <a name="load-adal-js-in-your-web-part"></a><span data-ttu-id="b8981-170">Загрузка ADAL JS в веб-части</span><span class="sxs-lookup"><span data-stu-id="b8981-170">Load ADAL JS in your web part</span></span>

<span data-ttu-id="b8981-p117">Веб-части создаются на основе TypeScript и распространяются как модули AMD. Их модульная архитектура позволяет изолировать различные ресурсы, используемые веб-частью. ADAL JS регистрируется в глобальном контексте, но ее можно загрузить в веб-части, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="b8981-p117">Web parts are built using TypeScript and distributed as AMD modules. Their modular architecture allows you to isolate the different resources used by the web part. ADAL JS is designed to register itself in the global scope, but you can load it in a web part by using the following code:</span></span>

```ts
import * as AuthenticationContext from 'adal-angular';
```

<span data-ttu-id="b8981-174">Этот оператор импортирует класс `AuthenticationContext`, который позволяет использовать функциональность ADAL JS в веб-частях.</span><span class="sxs-lookup"><span data-stu-id="b8981-174">This statement imports the `AuthenticationContext` class that exposes the ADAL JS functionality for use in web parts. Despite the name of the module, the  class works with every JavaScript library.</span></span> <span data-ttu-id="b8981-175">Несмотря на имя модуля, класс `AuthenticationContext` работает со всеми библиотеками JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b8981-175">This statement imports the  class that exposes the ADAL JS functionality for use in web parts. Despite the name of the module, the `AuthenticationContext` class works with every JavaScript library.</span></span>

### <a name="make-adal-js-suitable-for-use-with-sharepoint-framework-web-parts"></a><span data-ttu-id="b8981-176">Как использовать ADAL JS с веб-частями SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b8981-176">Make ADAL JS suitable for use with SharePoint Framework web parts</span></span>

<span data-ttu-id="b8981-p119">Текущую функциональность ADAL JS нельзя использовать в веб-частях. Используйте приведенное ниже исправление.</span><span class="sxs-lookup"><span data-stu-id="b8981-p119">The current ADAL JS functionality is unsuitable for use in web parts. Use the following patch to make ADAL JS work in your web part.</span></span>

<span data-ttu-id="b8981-179">**WebPartAuthenticationContext.js:**</span><span class="sxs-lookup"><span data-stu-id="b8981-179">**WebPartAuthenticationContext.js:**</span></span>
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

<span data-ttu-id="b8981-180">После исправления в ADAL JS происходят следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="b8981-180">The patch applies the following changes to of ADAL JS:</span></span>
- <span data-ttu-id="b8981-181">вся информация хранится в ключе веб-части (см. переопределение функций `_getItem` и `_saveItem`);</span><span class="sxs-lookup"><span data-stu-id="b8981-181">All information is stored in key specific to the web part (see the override of the `_getItem` and `_saveItem` functions)</span></span>
- <span data-ttu-id="b8981-182">обратные вызовы обрабатываются только веб-частями, которые их инициировали (см. переопределение функции `handleWindowCallback`);</span><span class="sxs-lookup"><span data-stu-id="b8981-182">Callbacks are processed only by web parts that initiated them (see the override of the `handleWindowCallback` function)</span></span>
- <span data-ttu-id="b8981-183">при проверке данных из обратных вызовов используется не одиночный объект, зарегистрированный в глобальном контексте, а экземпляр класса `AuthenticationContext` определенной веб-части (см. `_renewToken`, `getRequestInfo` и пустую регистрацию функции `window.AuthenticationContext`).</span><span class="sxs-lookup"><span data-stu-id="b8981-183">When verifying data from callbacks, the instance of the `AuthenticationContext` class of the specific web part is used instead of the globally registered singleton (see `_renewToken`, `getRequestInfo` and the empty registration of the `window.AuthenticationContext` function)</span></span>

### <a name="use-the-adal-js-patch-in-sharepoint-framework-web-parts"></a><span data-ttu-id="b8981-184">Использование исправления ADAL JS в веб-частях SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b8981-184">Use the ADAL JS patch in SharePoint Framework web parts</span></span>

<span data-ttu-id="b8981-185">Чтобы средство ADAL JS работало правильно в веб-частях SharePoint Framework, его необходимо определенным образом настроить.</span><span class="sxs-lookup"><span data-stu-id="b8981-185">For ADAL JS to work correctly in SharePoint Framework web parts, you have to configure it in a specific way. To do that, you first need to define a custom interface that extends the standard ADAL JS  interface to expose additional properties on the configuration object.</span></span> <span data-ttu-id="b8981-186">Для этого сначала необходимо определить пользовательский интерфейс, который расширяет стандартный интерфейс ADAL JS `Config`, чтобы предоставить объекту конфигурации дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="b8981-186">For ADAL JS to work correctly in SharePoint Framework web parts, you have to configure it in a specific way. To do that, you first need to define a custom interface that extends the standard ADAL JS `Config` interface to expose additional properties on the configuration object.</span></span>

```ts
export interface IAdalConfig extends adal.Config {
  popUp?: boolean;
  callback?: (error: any, token: string) => void;
  webPartId?: string;
}
```

<span data-ttu-id="b8981-187">Свойство `popUp` и функция `callback` уже реализованы в ADAL JS, но не доступны в определениях типа TypeScript стандартного интерфейса Config.</span><span class="sxs-lookup"><span data-stu-id="b8981-187">The `popUp` property and the `callback` function are both already implemented in ADAL JS but are not exposed in the TypeScript typings of the standard Config interface. You need them in order to allow users to sign in to your web parts using a pop-up window instead of redirecting to the Azure AD sign-in page.</span></span> <span data-ttu-id="b8981-188">Они нужны, чтобы пользователи могли входить в веб-части, используя всплывающее окно, а не перенаправление на страницу входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8981-188">The  property and the  function are both already implemented in ADAL JS but are not exposed in the TypeScript typings of the standard Config interface. You need them in order to allow users to sign in to your web parts using a pop-up window instead of redirecting to the Azure AD sign-in page.</span></span>

<span data-ttu-id="b8981-189">Далее загрузите исправление ADAL JS, пользовательский интерфейс конфигурации и объект конфигурации в основной компонент веб-части.</span><span class="sxs-lookup"><span data-stu-id="b8981-189">Next load the ADAL JS patch, the custom configuration interface, and your configuration object into the main component of your web part.</span></span>

```tsx
import * as AuthenticationContext from 'adal-angular';
import adalConfig from '../AdalConfig';
import { IAdalConfig } from '../../IAdalConfig';
import '../../WebPartAuthenticationContext';
```

<span data-ttu-id="b8981-190">В конструкторе компонента дополните конфигурацию ADAL JS и используйте ее для создания нового экземпляра класса `AuthenticationContext`.</span><span class="sxs-lookup"><span data-stu-id="b8981-190">In the constructor of your component, extend the ADAL JS configuration with additional properties and use it to create a new instance of the `AuthenticationContext` class.</span></span>

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

<span data-ttu-id="b8981-191">Сначала код извлекает стандартный объект конфигурации ADAL JS и приводит его к типу нового интерфейса конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b8981-191">The code first retrieves the standard ADAL JS configuration object and casts it to the type of the newly defined configuration interface.</span></span> <span data-ttu-id="b8981-192">Затем он передает идентификатор экземпляра веб-части, чтобы все значения ADAL JS могли храниться, не конфликтуя с другими веб-частями на странице.</span><span class="sxs-lookup"><span data-stu-id="b8981-192">Then it passes the ID of the web part instance so that all ADAL JS values can be stored in a way that they won't collide with other web parts on the page.</span></span> <span data-ttu-id="b8981-193">Далее он включает аутентификацию с помощью всплывающего окна и определяет функцию обратного вызова, которая запускается после аутентификации для обновления компонента.</span><span class="sxs-lookup"><span data-stu-id="b8981-193">Next it enables the pop-up-based authentication and defines a callback function that runs when authentication completes to update the component.</span></span> <span data-ttu-id="b8981-194">Наконец, он создает новый экземпляр класса `AuthenticationContext` и сбрасывает набор `_singletonInstance` в конструкторе класса `AuthenticationContext`.</span><span class="sxs-lookup"><span data-stu-id="b8981-194">Finally it creates a new instance of the `AuthenticationContext` class and resets the `_singletonInstance`  set in the constructor of the `AuthenticationContext` class.</span></span> <span data-ttu-id="b8981-195">Это необходимо, чтобы каждая веб-часть могла использовать собственную версию контекста аутентификации ADAL JS.</span><span class="sxs-lookup"><span data-stu-id="b8981-195">This is required in order to allow every web part to use its own version of the ADAL JS authentication context.</span></span>

## <a name="considerations-when-using-oauth-implicit-flow-in-sharepoint-framework-client-side-web-parts"></a><span data-ttu-id="b8981-196">Что нужно учитывать при использовании неявного потока OAuth в клиентских веб-частях SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="b8981-196">Considerations when using OAuth implicit flow in SharePoint Framework client-side web parts</span></span>

<span data-ttu-id="b8981-p123">При создании клиентских веб-частей SharePoint Framework, которые взаимодействуют с ресурсами, защищенными Azure AD, следует учитывать некоторые ограничения. Приведенная ниже информация поможет вам определить, подходит ли авторизация OAuth для вашей веб-части и организации.</span><span class="sxs-lookup"><span data-stu-id="b8981-p123">Before you build SharePoint Framework client-side web parts that communicate with resources secured by Azure AD, there are some constraints that you should consider. The following information will help you determine when OAuth authorization in web parts is the right choice for your solution and organization.</span></span>

### <a name="sharepoint-framework-web-parts-are-highly-trusted"></a><span data-ttu-id="b8981-199">Веб-части SharePoint Framework с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="b8981-199">SharePoint Framework web parts are highly trusted</span></span>

<span data-ttu-id="b8981-p124">В отличие от надстроек SharePoint, веб-части получают те же разрешения, что и текущий пользователь. Они могут выполнять любые действия, доступные пользователю. Поэтому веб-части могут устанавливать и развертывать только администраторы клиента. Они должны убедиться, что веб-части получены из надежного источника и утверждены для использования в клиенте.</span><span class="sxs-lookup"><span data-stu-id="b8981-p124">Unlike SharePoint Add-ins, web parts run with the same permissions as the current user. Whatever the user can do, the web part can do as well. This is why web parts can be installed and deployed only by tenant administrators The tenant administrator should verify that web parts they are deploying come from a trusted source, and were approved for use in the tenant.</span></span>

<span data-ttu-id="b8981-p125">Веб-части входят в состав страницы и, в отличие от надстроек SharePoint, используют модель DOM и ресурсы совместно с другими элементами на странице. Токены, которые предоставляют доступ к ресурсам, защищенным с помощью Azure AD, извлекаются через обратный вызов, посылаемый на страницу веб-части. Этот обратный вызов может быть обработан любым элементом на странице. Кроме того, после обработки токены доступа хранятся в локальном хранилище браузера или хранилище сеанса, из которого их может получить любой компонент на странице. Вредоносная веб-часть может прочитать токен и предоставить его или полученные с его помощью данные внешней службе.</span><span class="sxs-lookup"><span data-stu-id="b8981-p125">Web parts are a part of the page and, unlike SharePoint Add-ins, share DOM and resources with other elements on the page. Access tokens that grant access to resources secured with Azure AD, are retrieved through a callback to the same page where the web part is located. That callback can be processed by any element on the page. Also, once access tokens are processed from callbacks, they are stored in the browser's local storage or session storage from where they can be retrieved by any component on the page. A malicious web part could read the token and either expose the token or the data it retrieved using that token to an external service.</span></span>

### <a name="url-is-a-part-of-the-oauth-implicit-flow-contract"></a><span data-ttu-id="b8981-208">URL-адрес — это часть контракта неявного потока OAuth</span><span class="sxs-lookup"><span data-stu-id="b8981-208">URL is a part of the OAuth implicit flow contract</span></span>

<span data-ttu-id="b8981-p126">Клиентские приложения не могут хранить секрет клиента, не сообщая его пользователям. Чтобы проверить подлинность приложения, его URL-адрес включается в контракт доверия между Azure AD и приложением. В результате URL-адрес каждой страницы с веб-частями, использующими неявный поток OAuth, должен быть зарегистрирован в Azure AD. В противном случае произойдет сбой потока OAuth и веб-части будет отказано в доступе к защищенному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="b8981-p126">Client-side applications are incapable of storing a client secret without revealing it to users. In order to verify the authenticity of the particular application, the URL where the application is hosted, is used as a part of the trust contract between Azure AD and the application. The consequences of this are that the URL of every page with web parts using OAuth implicit flow must be registered with Azure AD. If a page is not registered, the OAuth flow will fail and the web part will be denied access to the secured resource.</span></span>

<span data-ttu-id="b8981-p127">Эта необходимая мера безопасности — существенное ограничение для организаций, которые разрешают пользователям добавлять веб-части на страницы. Рекомендуем ограничить количество страниц с веб-частями, которые используют неявный поток OAuth. Используйте домашнюю страницу или определенные целевые страницы и зарегистрируйте их в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8981-p127">This necessary security measure is a significant limitation for organizations that allow users to add web parts to pages. We recommend that you limit the number of locations where web parts using OAuth implicit flow are used. Use a few well known locations such as the home page or specific landing pages and have these locations registered with Azure AD.</span></span>

### <a name="internet-explorer-security-zones"></a><span data-ttu-id="b8981-216">Зоны безопасности Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b8981-216">Internet Explorer security zones</span></span>

<span data-ttu-id="b8981-p128">Браузер Internet Explorer применяет политики безопасности к посещаемым веб-сайтам, основываясь на зонах безопасности. Веб-сайты, которые относятся к разным зонам безопасности, запускаются в изолированных средах и не взаимодействуют между собой. При использовании неявного потока OAuth в клиентских веб-частях SharePoint Framework страница с веб-частями, использующими OAuth, и страница для входа в Azure AD (https://login.microsoftonline.com) должны находиться в одной зоне безопасности. В противном случае выполнить аутентификацию не удастся, и веб-часть не сможет взаимодействовать с ресурсами, защищенными с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8981-p128">Internet Explorer uses security zones to apply security policies to websites you visit. Websites assigned to different security zones run isolated and cannot cooperate. When using OAuth implicit flow in SharePoint Framework client-side web parts, the page with web parts using OAuth and the Azure AD login page (located at https://login.microsoftonline.com) must be in the same security zone. Without such configuration the authentication process will fail and web part won't be able to communicate with Azure AD-secured resources.</span></span>

### <a name="user-must-sign-in-frequently"></a><span data-ttu-id="b8981-221">Пользователь должен входить в приложение часто</span><span class="sxs-lookup"><span data-stu-id="b8981-221">User must sign in frequently</span></span>

<span data-ttu-id="b8981-p129">В обычном потоке OAuth веб-приложения и клиентские приложения получают токен доступа с коротким сроком действия и токен обновления, действительный в течение более длительного периода времени. Когда срок действия токена доступа истекает, для получения нового используется токен обновления. При таком подходе пользователи могут входить в Azure AD реже.</span><span class="sxs-lookup"><span data-stu-id="b8981-p129">When using regular OAuth flow web applications and client applications get a short-lived access token and a refresh token which is valid for a longer period of time. When the access token expires, the refresh token is used to get a new access token. This approach reduces how often users need to sign in to Azure AD.</span></span>

<span data-ttu-id="b8981-p130">Так как клиентские приложения не могут хранить секреты, а раскрытие токена обновления представляет собой серьезную угрозу безопасности, они получают токен доступа только в неявном потоке OAuth. Когда срок действия этого токена закончится, приложение запустит новый поток OAuth, и пользователю придется войти в него снова.</span><span class="sxs-lookup"><span data-stu-id="b8981-p130">Because client-side applications are incapable of securely storing secrets, and disclosing a refresh token is a serious security threat, they only receive the access token as part of the OAuth implicit flow. Once that token expires, the application must start a new OAuth flow which could require the user to sign in again.</span></span>

## <a name="more-information"></a><span data-ttu-id="b8981-227">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="b8981-227">More information</span></span>

- [<span data-ttu-id="b8981-228">Сценарии аутентификации для Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8981-228">Authentication Scenarios for Azure AD</span></span>](https://Azure.microsoft.com/ru-RU/documentation/articles/active-directory-authentication-scenarios/)
