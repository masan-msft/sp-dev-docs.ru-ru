<span data-ttu-id="762fc-p123">Этот проект просто записывает сведения в журнал трассировки. Однако в вашем приемнике эти сведения будут отправляться в таблицу или очередь, которая может обрабатывать полученные данные для получения сведений из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="762fc-p123">This project just writes the information to the trace log. However, in your receiver, you will send this information into a table or a queue that can process the received data to get information from SharePoint.</span></span>

    ```
    iisexpress.exe Information: 0 : Message='Resource: c34420f9-2a67-4e54-94c9-b6770892299b'
    iisexpress.exe Information: 0 : Message='SubscriptionId: 32b95ad9-4d20-4a17-bfa3-2957cb38ead8'
    iisexpress.exe Information: 0 : Message='TenantId: 7a17cb7d-6898-423f-8839-45f363076f06'
    iisexpress.exe Information: 0 : Message='SiteUrl: /'
    iisexpress.exe Information: 0 : Message='WebId: 62b80e0b-f889-4974-a519-cc138413be40'
    iisexpress.exe Information: 0 : Message='ExpirationDateTime: 2016-10-27T16:17:57.0000000Z'
    ```

Этот проект просто записывает сведения в журнал трассировки. Однако в вашем приемнике эти сведения будут отправляться в таблицу или очередь, которая может обрабатывать полученные данные для получения сведений из SharePoint. 

<span data-ttu-id="762fc-282">С помощью этих данных вы можете составить URL-адрес и использовать API [GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges) для просмотра последних изменений.</span><span class="sxs-lookup"><span data-stu-id="762fc-282">With this data, you can construct the URL and use the [GetChanges](https://msdn.microsoft.com/EN-US/library/office/dn531433.aspx#bk_ListGetChanges) API to get the latest changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="762fc-283">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="762fc-283">Next steps</span></span>

<span data-ttu-id="762fc-284">В этой статье мы использовали клиент Postman и простой веб-API для создания подписки и получения уведомлений веб-перехватчиков из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="762fc-284">In this article, you used Postman client and a simple web API to subscribe and receive webhook notifications from SharePoint.</span></span>

<span data-ttu-id="762fc-285">Теперь ознакомьтесь с [базовой реализацией веб-перехватчиков SharePoint](./webhooks-reference-implementation), в которой для обработки сведений, получения изменений из SharePoint и их обратной передачи в список SharePoint используются Очереди хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="762fc-285">Next, take a look at [SharePoint webhooks sample reference implementation](./webhooks-reference-implementation), which shows an end-to-end sample that uses Azure Storage Queues to process the information, get changes from SharePoint, and push those changes back into a SharePoint list.</span></span>
