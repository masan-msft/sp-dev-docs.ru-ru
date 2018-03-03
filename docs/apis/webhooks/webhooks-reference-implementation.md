---
title: "Пример реализации веб-перехватчиков SharePoint"
description: "В этой эталонной реализации PnP SharePoint показано, как использовать веб-перехватчики SharePoint в приложении."
ms.date: 02/08/2018
ms.prod: sharepoint
ms.openlocfilehash: 229dccd087e4e936034ceedc63c3ba9540458ea1
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="sharepoint-webhooks-sample-reference-implementation"></a>Пример реализации веб-перехватчиков SharePoint

Эталонная реализация PnP SharePoint демонстрирует способы использования веб-перехватчиков SharePoint в приложении. Веб-перехватчики реализованы так, что могут использоваться на предприятиях совместно с различными компонентами Microsoft Azure, такими как веб-задания Azure, SQL Server для Azure и очереди службы хранилища Azure для асинхронной обработки уведомлений о веб-заданиях.

Эталонная реализация работает только с [веб-перехватчиками для списков SharePoint](./lists/overview-sharepoint-list-webhooks.md). 

Вы также можете выполнить эти действия, посмотрев видео, добавленные в [канал SharePoint PnP на сайте YouTube](https://www.youtube.com/watch?v=j3hWCAI9R20).

<a href="https://www.youtube.com/watch?v=j3hWCAI9R20">
<img src="../../images/youtube-introducing-sharepoint-webhooks.png" alt="PnP webcast - Introducing SharePoint webhooks" />
</a>

**Относится к:** мультитенантная среда Office 365.

Microsoft Azure используется для размещения различных компонентов, необходимых для реализации веб-перехватчиков Azure.

Исходный код и другие материалы для данной эталонной реализации доступны в двух вариантах: 
- Версия приложения SharePoint с размещением у поставщика
- Приложение Azure AD для Office 365, которое представлено в [репозитории примеров для разработчиков SharePoint на сайте GitHub](https://aka.ms/sp-webhooks-sample-reference). 

## <a name="deploy-the-reference-implementation"></a>Развертывание эталонной реализации

Это приложение показывает, как управлять веб-перехватчиками для списка SharePoint. Оно также содержит эталонную реализацию конечной точки службы веб-перехватчиков, которую вы можете использовать в своих проектах. 

![Приложение с эталонной реализацией веб-перехватчиков в SharePoint](../../images/webhook-sample-application.png)

### <a name="deployment-guides"></a>Руководства по развертыванию

- [Руководстве по развертыванию эталонной реализации веб-перехватчиков в SharePoint](https://github.com/SharePoint/sp-dev-samples/blob/master/Samples/WebHooks.List/Deployment%20guide.md) содержит инструкции по развертыванию эталонной реализации с размещением у поставщика. 

- Чтобы развернуть приложение Azure AD для Office 365, выполните действия, описанные в [руководстве по развертыванию эталонной реализации веб-перехватчиков SharePoint в Azure AD](https://github.com/SharePoint/sp-dev-samples/blob/master/Samples/WebHooks.List.AzureAD/Deployment%20guide.md), где показано, как использовать функцию веб-API в качестве службы веб-перехватчиков. 

- Если вас больше интересует использование функций Azure, см. [руководство по функциям Azure](https://github.com/SharePoint/sp-dev-samples/blob/master/Samples/WebHooks.List.AzureAD/azure%20functions%20guide.md), где вы найдете дополнительные сведения о том, как использовать их в этой эталонной реализации.

### <a name="introduction-to-webhooks"></a>Общие сведения о веб-перехватчиках

Веб-перехватчики используются для оповещения приложения об изменениях в SharePoint, которые оно должно отслеживать. Таким образом, приложению не нужно регулярно запрашивать сведения об изменениях. Веб-перехватчики оповещают приложение (модель **push**) о наличии каких-либо изменений. Веб-перехватчики используются не только в решениях корпорации Майкрософт. Это универсальный веб-стандарт, который используют и другие поставщики (например, WordPress, GitHub, MailChimp и другие).

## <a name="add-a-webhook-to-your-sharepoint-list"></a>Добавление веб-перехватчика в список SharePoint

Эталонная реализация работает со списком SharePoint. Чтобы добавить веб-перехватчик в список SharePoint, приложение сначала создает подписку на веб-перехватчик, отправив запрос [`POST /_api/web/lists('list-id')/subscriptions`](./lists/create-subscription.md). Запрос включает перечисленные ниже данные.

* Полезные данные, определяющие список, для которого вы добавляете веб-перехватчик.
* URL-адрес службы веб-перехватчиков для отправки уведомлений.
* Дата окончания срока действия веб-перехватчика. 

Когда вы отправите среде SharePoint запрос на добавление веб-перехватчика, SharePoint проверит, существует ли конечная точка службы веб-перехватчиков, а затем отправит строку проверки в конечную точку службы. Предполагается, что конечная точка службы вернет строку проверки в течение 5 секунд. Если произойдет ошибка, создание веб-перехватчика будет отменено. Если служба развернута, то операция успешно выполняется, а SharePoint возвращает сообщение HTTP 201 в ответ на первоначальный запрос POST от приложения. Полученные полезные данные содержат идентификатор новой подписки на веб-перехватчик.

![Добавление веб-перехватчика](../../images/webhook-sample-add-process.png)

Ознакомившись с эталонной реализацией, вы увидите, что все операции CRUD веб-перехватчиков объединяются в класс [WebHookManager](https://github.com/SharePoint/sp-dev-samples/blob/master/Samples/WebHooks.List/SharePoint.WebHooks.Common/WebHookManager.cs) проекта **SharePoint.WebHooks.Common**. Для добавления веб-перехватчика используется метод **AddListWebHookAsync**:

```cs
/// <summary>
/// This method adds a webhook to a SharePoint list. Note that you need your webhook endpoint being passed into this method to be up and running and reachable from the internet
/// </summary>
/// <param name="siteUrl">Url of the site holding the list</param>
/// <param name="listId">Id of the list</param>
/// <param name="webHookEndPoint">Url of the webhook service endpoint (the one that will be called during an event)</param>
/// <param name="accessToken">Access token to authenticate against SharePoint</param>
/// <param name="validityInMonths">Optional webhook validity in months, defaults to 3 months, max is 6 months</param>
/// <returns>subscription ID of the new webhook</returns>
public async Task<SubscriptionModel> AddListWebHookAsync(string siteUrl, string listId, string webHookEndPoint, string accessToken, int validityInMonths = 3)
{
    // webhook add code...
}
```

<br/>

Вызывая SharePoint, необходимо указать данные для проверки подлинности. В этом случае используются заголовок **Bearer** и **маркер доступа**. Чтобы получить маркер доступа, перехватите его с помощью обработчика событий **ExecutingWebRequest**:

```cs
ClientContext cc = null;

// Create SharePoint ClientContext object...

// Add ExecutingWebRequest event handler
cc.ExecutingWebRequest += Cc_ExecutingWebRequest;

// Capture the OAuth access token since we want to reuse that one in our REST requests
private void Cc_ExecutingWebRequest(object sender, WebRequestEventArgs e)
{
    this.accessToken = e.WebRequestExecutor.RequestHeaders.Get("Authorization").Replace("Bearer ", "");
}
```

## <a name="sharepoint-calls-out-to-your-webhook-service"></a>SharePoint вызывает службу веб-перехватчиков

Когда SharePoint обнаруживает изменение в списке, для которого вы создали подписку на веб-перехватчик, SharePoint вызывает конечную точку службы. При просмотре полезных данных из SharePoint обратите внимание на следующие важные свойства:

Свойство|Описание
--------|-----------
**subscriptionId**|Идентификатор подписки на веб-перехватчик. Этот идентификатор нужен, чтобы обновить подписку на веб-перехватчик (например, в случае продления срока действия веб-перехватчика).
**resource**|Идентификатор списка, в отношении которого произошло изменение.
**siteUrl**|Относительный URL-адрес сервера сайта с ресурсом, в отношении которого произошло изменение.

> [!NOTE]
> SharePoint отправляет уведомления только о том, что произошло изменение, не указывая при этом суть изменения. Так как вы получаете сведения о веб-сайте и списке, которые были изменены, это означает, что эту же конечную точку службы можно использовать для обработки событий веб-перехватчика, касающихся нескольких сайтов и списков.

При вызове службы важно, чтобы в течение 5 секунд в ответ вернулось сообщение HTTP 200. Далее в этой статье приведены дополнительные сведения о времени ответа, но фактически для этого необходима **асинхронная** обработка уведомлений. В данной эталонной реализации она обеспечивается при помощи веб-заданий Azure и очередей службы хранилища Azure.

![SharePoint вызывает конечную точку веб-перехватчика](../../images/webhook-sample-call-webhook.png)

## <a name="grab-the-changes-your-service-needs-to-act-upon"></a>Захват изменений, на которые должна реагировать служба

На предыдущем шаге была вызвана конечная точка службы, но среда SharePoint предоставила сведения только о том, где произошло изменение, а не о том, что было изменено. Чтобы понять, что было изменено, необходимо использовать API SharePoint `GetChanges()`, как показано ниже.

![Асинхронный метод GetChanges](../../images/webhook-sample-async-getchanges.png)

Дополнительные сведения о реализации `GetChanges()` в методе **ProcessNotification** вы найдете, открыв описание класса [ChangeManager](https://github.com/SharePoint/sp-dev-samples/blob/master/Samples/WebHooks.List/SharePoint.WebHooks.Common/ChangeManager.cs) в проекте **SharePoint.WebHooks.Common**. 

Чтобы не получать уведомления об одних и тех же изменениях несколько раз, необходимо сообщить SharePoint, из какой точки вы хотите узнавать об изменениях. Это можно сделать путем передачи маркера **changeToken**, применение которого предполагает, что конечная точка службы должна хранить последний **changeToken**, чтобы его можно было использовать при следующем вызове этой конечной точки.

Ниже приведены некоторые ключевые сведения об изменениях.

- SharePoint не вызывает службу в режиме реального времени. При изменении списка, для которого предусмотрен веб-перехватчик, SharePoint поставит в очередь вызов веб-перехватчика. Один раз в минуту эта очередь считывается и вызываются соответствующие конечные точки службы. Такая пакетная обработка запросов важна. Например, если одновременно отправляется 1000 записей, то пакетная обработка не допустит, чтобы среда SharePoint вызывала конечную точку 1000 раз. Таким образом, конечная точка вызывается только один раз, но при вызове метода `GetChanges()` вы получаете 1000 событий изменения, которые необходимо обработать.

- Для обеспечения немедленного ответа важно, чтобы рабочая нагрузка конечной точки службы выполнялась асинхронно независимо от количества изменений. В данной эталонной реализации мы использовали возможности Azure: служба сериализует входящие полезные данные и хранит их в очереди службы хранилища Azure, а веб-задание Azure непрерывно проверяет наличие сообщений в очереди. Если в очереди есть сообщения, веб-задание обрабатывает их и асинхронно выполняет логику.

## <a name="complete-end-to-end-flow"></a>Полный поток

Ниже показан поток реализации веб-перехватчиков от начала до конца.

![Полный поток эталонной реализации веб-перехватчиков](../../images/webhook-sample-end-to-end-flow.png)

1. Приложение создает подписку на веб-перехватчик. После этого оно получает текущий маркер **changeToken** из списка, для которого был создан веб-перехватчик.
2. Приложение сохраняет **changeToken** в постоянном хранилище (в данном случае — SQL Azure).
3. В SharePoint происходит изменение, и SharePoint вызывает конечную точку службы.
4. Конечная точка службы сериализует запрос уведомления и помещает его в очередь хранилища.
5. Веб-задание видит сообщение в очереди и начинает выполнять логику его обработки.
6. Логика обработки сообщений получает маркер изменений, который использовался в последний раз, из постоянного хранилища.
7. Логика обработки сообщений использует API `GetChanges()`, чтобы определить суть изменения.
8. Возвращенные изменения обрабатываются, и приложение выполняет необходимые действия.
9. Наконец, приложение сохраняет последний полученный маркер **changeToken**, чтобы в дальнейшем не получать сведения об уже обработанных изменениях.

## <a name="work-with-webhook-renewal"></a>Работа с обновлением веб-перехватчиков

Срок действия подписок на веб-перехватчики по умолчанию истекает через 6 месяцев или в день, указанный во время их создания. Часто требуется, чтобы веб-перехватчик был доступен на протяжении большего периода времени. Модели, описанные в следующих разделах, подходят для продления срока действия подписки на веб-перехватчик. Первая модель довольно простая, вторая же немного сложнее и требует размещения дополнительного веб-задания.

### <a name="basic-model"></a>Базовая модель

Вместе с уведомлением служба также получает сведения о сроке действия подписки. Если он скоро истечет, вы просто продлеваете его в логике обработки уведомлений. Эта модель предусмотрена в данной эталонной реализации и подходит в большинстве случаев. Но если в списке, для которого мы создали подписку на веб-перехватчик, не происходит изменений на протяжении 6 месяцев, эта подписка не продлевается и впоследствии удаляется.

### <a name="reliable-but-more-complex-model"></a>Надежная, но более сложная модель

Создайте веб-задание, которое еженедельно будет считывать все ИД подписки из постоянного хранилища. Каждый раз поочередно расширяйте найденные подписки. 

> [!NOTE]
> Это веб-задание не входит в данную эталонную реализацию.

Обновление веб-перехватчика для списка SharePoint можно выполнить с помощью вызова REST [`PATCH /_api/web/lists('list-id')/subscriptions(‘subscriptionID’)`](./lists/update-subscription.md). 

В эталонной реализации обновление веб-перехватчиков реализуется в классе [WebHookManager](https://github.com/SharePoint/sp-dev-samples/blob/master/Samples/WebHooks.List/SharePoint.WebHooks.Common/WebHookManager.cs) проекта **SharePoint.WebHooks.Common**. 

Для обновления веб-перехватчика используется метод **UpdateListWebHookAsync**:

```csharp
/// <summary>
/// Updates the expiration datetime (and notification URL) of an existing SharePoint list webhook
/// </summary>
/// <param name="siteUrl">Url of the site holding the list</param>
/// <param name="listId">Id of the list</param>
/// <param name="subscriptionId">Id of the webhook subscription that we need to update</param>
/// <param name="webHookEndPoint">Url of the webhook service endpoint (the one that will be called during an event)</param>
/// <param name="expirationDateTime">New webhook expiration date</param>
/// <param name="accessToken">Access token to authenticate against SharePoint</param>
/// <returns>true if successful, exception in case something went wrong</returns>
public async Task<bool> UpdateListWebHookAsync(string siteUrl, string listId, string subscriptionId, string webHookEndPoint, DateTime expirationDateTime, string accessToken)
{
    // webhook update code...
}
```

## <a name="debugging-webhooks"></a>Отладка веб-перехватчиков

Так как SharePoint вызывает конечную точку службы веб-перехватчиков, эта точка должна быть доступна для SharePoint, что немного усложняет разработку и отладку. Ниже приведены некоторые стратегии, которые можно использовать для упрощения работы.

* Во время первоначальной разработки вы предоставляете сериализованные полезные данные логике обработки службы. Это позволяет полностью проверить логику обработки без развертывания конечной точки службы (и даже без настройки веб-перехватчика).

* Если у вас есть доступ к ресурсам Azure, можно развернуть конечную точку в Azure с помощью отладочной сборки, а также настроить службу приложений Azure для отладки. Это позволяет задать удаленную точку останова и выполнить удаленную отладку с помощью Visual Studio.

- Если вы не хотите развертывать службу во время разработки, необходимо использовать защищенный туннель. Идея заключается в том, что вы сообщаете SharePoint, что служба уведомлений находится в общедоступной конечной точке. Установите в клиенте компонент, который подключается к этой общедоступной службе. При каждом вызове общедоступной конечной точки этот клиентский компонент получает уведомление, после чего он передает полезные данные службе, запущенной на localhost. [ngrok](https://ngrok.com/) — реализация инструмента защищенного туннеля, который можно использовать для локальной отладки службы веб-перехватчиков.

## <a name="see-also"></a>См. также

- [Обзор веб-перехватчиков SharePoint](overview-sharepoint-webhooks.md)