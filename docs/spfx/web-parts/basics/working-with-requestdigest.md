# <a name="working-with-the-original-requestdigest"></a>Работа с исходным __RequestDigest

Есть много программных кодов, созданных для работы с классическими страницами SharePoint, которые можно использовать с платформой SharePoint Framework, но иногда бывает, что не удается найти определенные компоненты или переменные. Например, поле формы `__REQUESTDIGEST`. В идеале вам не нужно использовать глобальную переменную для доступа к дайджесту. Достаточно обновленного объекта `HttpRequest` для вызовов SharePoint, и он сам будет обрабатывать всю логику дайджеста и проверки подлинности (например, маркеры с истекшим сроком действия). Как это сделать, можно узнать из статьи [Подключение клиентской веб-части к SharePoint ("Здравствуй, мир!", часть 2)](https://dev.office.com/sharepoint/docs/spfx/web-parts/get-started/connect-to-sharepoint).

Тем не менее, если в существующем коде использованы более старые конструкции, с помощью клиентского кода и работы с DOM их довольно легко добавить обратно на страницу. Для этого нужно задействовать метод `onInit` в базовом классе веб-частей и запросить нужный элемент создания DOM. Вот пример создания элемента формы `__REQUESTDIGEST`.

```JavaScript
    public onInit<T>(): Promise<T>
    {
    // does the digest exist?
    if ( !document.getElementById('__REQUESTDIGEST') )
    {
      // OK, the request digest does not exist. Let's create it.
      // first, grab the digest value out of the contextWebInfo object (if it exists).
      var digestValue: string;
      try{
        digestValue = (window as any)._spClientSidePageContext.contextWebInfo.FormDigestValue;
      }
      catch (exception){
        // there is no digest on this page, so just return. This can easily happen on the local workbench
        return Promise.resolve();
      }

      if (digestValue){
        // OK, now lets create the digest input form. It looks like this:
        // <input type="hidden" name="__REQUESTDIGEST" id="__REQUESTDIGEST" value="blahblahblahblahblahblah, July23 -0000 or something like that">
        const requestDigestInput: Element = document.createElement('input');
        requestDigestInput.setAttribute('type', 'hidden');
        requestDigestInput.setAttribute('name', '__REQUESTDIGEST');
        requestDigestInput.setAttribute('id', '__REQUESTDIGEST');
        requestDigestInput.setAttribute('value', digestValue);

        // lastly, add the digest to the page
        document.body.appendChild(requestDigestInput);
      }
    }

    // no promise to return
    return Promise.resolve();
    }
```

>**Примечание.** Есть лучший способ получить текущее значение дайджеста, обрабатывающего все события кэширования, истечения времени, повторной выборки и т. д. Попробуйте его. Вам потребуется импортировать `digestCacheServiceKey` и `IDigestCache` из **sp-client-base**.

```JavaScript
    var digestCache:IDigestCache = this.context.serviceScope.consume(digestCacheServiceKey);
    digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string) => {
      // Do Something with the digest
      console.log(digest);
    });
```
