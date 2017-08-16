# <a name="working-with-the-original-requestdigest"></a><span data-ttu-id="4d681-101">Работа с исходным __RequestDigest</span><span class="sxs-lookup"><span data-stu-id="4d681-101">Working with the original __RequestDigest</span></span>

<span data-ttu-id="4d681-p101">Есть много программных кодов, созданных для работы с классическими страницами SharePoint, которые можно использовать с платформой SharePoint Framework, но иногда бывает, что не удается найти определенные компоненты или переменные. Например, поле формы `__REQUESTDIGEST`. В идеале вам не нужно использовать глобальную переменную для доступа к дайджесту. Достаточно обновленного объекта `HttpRequest` для вызовов SharePoint, и он сам будет обрабатывать всю логику дайджеста и проверки подлинности (например, маркеры с истекшим сроком действия). Как это сделать, можно узнать из статьи [Подключение клиентской веб-части к SharePoint ("Здравствуй, мир!", часть 2)](https://dev.office.com/sharepoint/docs/spfx/web-parts/get-started/connect-to-sharepoint).</span><span class="sxs-lookup"><span data-stu-id="4d681-p101">There is a lot of code written to work with the classic SharePoint pages that you can use with the SharePoint Framework, but sometimes certain components or variables aren't there. One example is the __REQUESTDIGEST form field.  In an ideal world, you wouldn't use a global variable to access the digest, you'd just use the updated HttpRequest object to make your SharePoint call, and it will handle all the digest / auth logic for you (including things like expired tokens).  The Connect your client-side web part to SharePoint (Hello world part 2) article shows you how to do this.</span></span>

<span data-ttu-id="4d681-p102">Тем не менее, если в существующем коде использованы более старые конструкции, с помощью клиентского кода и работы с DOM их довольно легко добавить обратно на страницу. Для этого нужно задействовать метод `onInit` в базовом классе веб-частей и запросить нужный элемент создания DOM. Вот пример создания элемента формы `__REQUESTDIGEST`.</span><span class="sxs-lookup"><span data-stu-id="4d681-p102">However, if your existing code uses some older constructs, through the power of client side code and DOM manipulation, it's fairly easy to add these back to a page.  The key is to hook into the onInit method in the base web part class, and pull the create the DOM element that you expect to be there.  Here's an example that creates the __REQESTDIGEST form element.</span></span>

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

><span data-ttu-id="4d681-109">**Примечание.** Есть лучший способ получить текущее значение дайджеста, обрабатывающего все события кэширования, истечения времени, повторной выборки и т. д. Попробуйте его. Вам потребуется импортировать `digestCacheServiceKey` и `IDigestCache` из **sp-client-base**.</span><span class="sxs-lookup"><span data-stu-id="4d681-109">Note: There is a better way to get the current digest value that will handle all of the caching / expiring / refetching / etc.  Give this a try.  You'll need to import digestCacheServiceKey and IDigestCache from sp-client-base</span></span>

```JavaScript
    var digestCache:IDigestCache = this.context.serviceScope.consume(digestCacheServiceKey);
    digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string) => {
      // Do Something with the digest
      console.log(digest);
    });
```
