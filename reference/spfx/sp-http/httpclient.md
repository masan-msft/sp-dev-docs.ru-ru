<span data-ttu-id="7f943-p104">Выполняет вызов службы REST. Несмотря на то что подкласс SPHttpClient добавляет некоторые улучшения, параметры и семантика для HttpClient.fetch() фактически такие же, как и в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org).</span><span class="sxs-lookup"><span data-stu-id="7f943-p104">Performs a REST service call. Although the SPHttpClient subclass adds additional enhancements, the parameters and semantics for HttpClient.fetch() are essentially the same as the WHATWG API standard that is documented here: https://fetch.spec.whatwg.org/</span></span>|
|:-------------|:----|:-------|:-----------|
|[`fetch(url,configuration,options)`](fetch-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | Выполняет вызов службы REST. Несмотря на то что подкласс SPHttpClient добавляет некоторые улучшения, параметры и семантика для HttpClient.fetch() фактически такие же, как и в стандарте по API WHATWG (приведен здесь: https://fetch.spec.whatwg.org). |
|[`fetchCore()`](fetchcore-httpclient.md)     | `protected` | `Promise<Response>` | <span data-ttu-id="7f943-126">Все сетевые запросы маршрутизируются с помощью этого метода, вызывающего IFetchProvider.fetch().</span><span class="sxs-lookup"><span data-stu-id="7f943-126">All network requests are routed through this method, which calls the underlying IFetchProvider.fetch().</span></span> |
|[`get(url,configuration,options)`](get-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | <span data-ttu-id="7f943-127">Вызывает fetch(), но задает метод GET.</span><span class="sxs-lookup"><span data-stu-id="7f943-127">Calls fetch(), but sets the method to 'GET'.</span></span> |
|[`post(url,configuration,options)`](post-httpclient.md)     | `public` | `Promise<HttpClientResponse>` | <span data-ttu-id="7f943-128">Вызывает fetch(), но задает метод POST.</span><span class="sxs-lookup"><span data-stu-id="7f943-128">Calls fetch(), but sets the method to 'POST'.</span></span> |





