<span data-ttu-id="d8ce8-p147">Многие клиентские модификации используют библиотеку jQuery для выполнения запросов AJAX из-за ее простоты и совместимости с разными браузерами. Если вы используете jQuery только из-за этого, вы можете совершать вызовы AJAX с помощью стандартного клиента HTTP, входящего в состав SharePoint Framework. В SharePoint Framework есть два клиента HTTP: [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient), предназначенный для отправки запросов REST API SharePoint, и [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient), предназначенный для отправки веб-запросов других REST API. Вот как выполнить вызов с помощью SPHttpClient для получения заголовка текущего сайта SharePoint:</span><span class="sxs-lookup"><span data-stu-id="d8ce8-p147">Many client-side customizations use jQuery for executing AJAX requests for its simplicity and cross-browser compatibility. If this is all that you're using jQuery for, you can execute the AJAX calls using the standard HTTP client provided with the SharePoint Framework. SharePoint Framework offers you two types of HTTP client: the [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient), meant for executing requests to the SharePoint REST API, and the [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient) designed for issuing web requests to other REST APIs. Here is how you would execute a call using the SPHttpClient to get the title of the current SharePoint site:</span></span>

Многие клиентские модификации используют библиотеку jQuery для выполнения запросов AJAX из-за ее простоты и совместимости с разными браузерами. Если вы используете jQuery только из-за этого, вы можете совершать вызовы AJAX с помощью стандартного клиента HTTP, входящего в состав SharePoint Framework. В SharePoint Framework есть два клиента HTTP: [SPHttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/sphttpclient), предназначенный для отправки запросов REST API SharePoint, и [HttpClient](https://dev.office.com/sharepoint/reference/spfx/sp-http/httpclient), предназначенный для отправки веб-запросов других REST API. Вот как выполнить вызов с помощью SPHttpClient для получения заголовка текущего сайта SharePoint:

```ts
this.context.spHttpClient.get(`${this.context.pageContext.web.absoluteUrl}/_api/web?$select=Title`,
SPHttpClient.configurations.v1,
{
  headers: {
    'Accept': 'application/json;odata=nometadata',
    'odata-version': ''
  }
})
.then((response: SPHttpClientResponse): Promise<{Title: string}> => {
  return response.json();
})
.then((web: {Title: string}): void => {
  // web.Title
}, (error: any): void => {
  // error
});
```

## <a name="more-information"></a><span data-ttu-id="d8ce8-271">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="d8ce8-271">More information</span></span>

- [<span data-ttu-id="d8ce8-272">Перенос модификаций SharePoint с использованием JavaScript в SharePoint Framework: ссылки на функции из файлов сценариев</span><span class="sxs-lookup"><span data-stu-id="d8ce8-272">Migrate SharePoint JavaScript customizations to SharePoint Framework - reference functions from script files</span></span>](https://blog.mastykarz.nl/migrate-sharepoint-javascript-customizations-sharepoint-framework-reference-functions/)
- [<span data-ttu-id="d8ce8-273">Перенос модификаций SharePoint на JavaScript в SharePoint Framework: вызовы AJAX и отображение данных с помощью jQuery</span><span class="sxs-lookup"><span data-stu-id="d8ce8-273">Migrate SharePoint JavaScript customizations to SharePoint Framework – jQuery AJAX calls and showing data</span></span>](https://rencore.com/blog/migrate-sharepoint-javascript-customizations-to-sharepoint-framework-jquery-ajax-calls-and-showing-data/)
