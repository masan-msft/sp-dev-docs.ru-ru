<span data-ttu-id="79d00-p103">Когда этому параметру присвоено значение true, выполняется указанное далее действие. Если заголовок "X-RequestDigest" не был явно добавлен для запроса, SPHttpClient добавит его, если запрос представляет собой операцию записи (т. е. метод HTTP, отличный от GET, HEAD или OPTIONS). Дайджестом запроса управляет служба DigestCache. В случае промаха кэша может быть выполнен дополнительный сетевой запрос.</span><span class="sxs-lookup"><span data-stu-id="79d00-p103">When this switch is true: If the 'X-RequestDigest' header was not explicitly added for the request, then SPHttpClient will add it if the request is a write operation (i.e. an HTTP method other than 'GET', 'HEAD', or 'OPTIONS'). The request digest is managed by the DigestCache service. In the case of a cache miss, an additional network request may be performed.</span></span> |
|`requestDigest`      | `boolean` | Когда этому параметру присвоено значение true, выполняется указанное далее действие. Если заголовок "X-RequestDigest" не был явно добавлен для запроса, SPHttpClient добавит его, если запрос представляет собой операцию записи (т. е. метод HTTP, отличный от GET, HEAD или OPTIONS). Дайджестом запроса управляет служба DigestCache. В случае промаха кэша может быть выполнен дополнительный сетевой запрос. |






