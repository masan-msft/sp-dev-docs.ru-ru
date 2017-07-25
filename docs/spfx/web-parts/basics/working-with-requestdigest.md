<span data-ttu-id="95b7d-p103">**Примечание.** Есть лучший способ получить текущее значение дайджеста, обрабатывающего все события кэширования, истечения времени, повторной выборки и т. д.  Попробуйте его.  Вам потребуется импортировать digestCacheServiceKey и IDigestCache из sp-client-base</span><span class="sxs-lookup"><span data-stu-id="95b7d-p103">**Note:** There is a better way to get the current digest value that will handle all of the caching / expiring / refetching / etc.  Give this a try.  You'll need to import digestCacheServiceKey and IDigestCache from sp-client-base</span></span>

```JavaScript
    public onInit<T>(): Promise<T>
    {
    // does the digest exist?
    if ( !document.getElementById('__REQUESTDIGEST') )
    {
      // OK, the request digest does not exist.  Let's create it.
      // first, grab the digest value out of the contextWebInfo object (if it exists).
      var digestValue: string;
      try{
        digestValue = (window as any)._spClientSidePageContext.contextWebInfo.FormDigestValue;
      }
      catch (exception){
        // there is no digest on this page, so just return.  This can easily happen on the local workbench
        return Promise.resolve();
      }

      if (digestValue){
        // OK, now lets create the digest input form.  It looks like this -
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

>**Примечание.** Есть лучший способ получить текущее значение дайджеста, обрабатывающего все события кэширования, истечения времени, повторной выборки и т. д.  Попробуйте его.  Вам потребуется импортировать digestCacheServiceKey и IDigestCache из sp-client-base

```JavaScript
    var digestCache:IDigestCache = this.context.serviceScope.consume(digestCacheServiceKey);
    digestCache.fetchDigest(this.context.pageContext.web.serverRelativeUrl).then((digest: string) => {
      // Do Something with the digest
      console.log(digest);
    });
```