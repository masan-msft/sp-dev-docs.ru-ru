<span data-ttu-id="c50d0-p109">Во избежание несанкционированного использования функции Azure при ее вызове необходимо указывать код. Этот код можно получить на экране **Управление**:</span><span class="sxs-lookup"><span data-stu-id="c50d0-p109">To avoid unathorized usage of your Azure Function the caller will need to specify a code when calling your function. This code can be retreived via the **Manage** screen:</span></span>](../../../images/webhook-azure-function8.png)

Во избежание несанкционированного использования функции Azure при ее вызове необходимо указывать код. Этот код можно получить на экране **Управление**:

![URL-адрес веб-перехватчика функции Azure](../../../images/webhook-azure-function7.png)

<span data-ttu-id="c50d0-142">Поэтому в нашем случае будет использоваться следующий URL-адрес веб-перехватчика: `https://pnp-functions.azurewebsites.net/api/spwebhookfunction?code=wyx9iAxp3o7fdGFZTbnp9Kfc5o2UhlzwgSOT/XGGM6QZcdYYa/o9aw==`</span><span class="sxs-lookup"><span data-stu-id="c50d0-142">So in our case the webhook URL to use is the following: `https://pnp-functions.azurewebsites.net/api/spwebhookfunction?code=wyx9iAxp3o7fdGFZTbnp9Kfc5o2UhlzwgSOT/XGGM6QZcdYYa/o9aw==`</span></span>



