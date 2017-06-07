# <a name="isphttpclientconfiguration-interface"></a>Интерфейс ISPHttpClientConfiguration







Интерфейс флажков для SPHttpClientConfiguration.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`defaultODataVersion`      | [`ODataVersion`](../sp-http/odataversion.md) | Если этот параметр указан (т. е. без значения undefined), выполняется указанное далее действие. Если заголовок "OData-Version" не был явно добавлен к запросу, SPHttpClient добавит его для определения версии, указанной с помощью defaultODataVersion. ПРИМЕЧАНИЕ. В большинстве случаев при отсутствии заголовка "OData-Version" сервер SharePoint в настоящее время указывает по умолчанию версию 3.0. Рекомендуем версию 4.0. |
|`defaultSameOriginCredentials`      | `boolean` | Когда этому параметру присвоено значение true, выполняется указанное далее действие. Если свойство RequestInit.credentials не указано явно для запроса, SPHttpClient назначит для него "same-origin". Без этого параметра разные веб-браузеры могут применять разные значения по умолчанию. Дополнительные сведения см. в спецификации по такому адресу: https://fetch.spec.whatwg.org/#cors-protocol-and-credentials. |
|`requestDigest`      | `boolean` | Когда этому параметру присвоено значение true, выполняется указанное далее действие. Если заголовок "X-RequestDigest" не был явно добавлен для запроса, SPHttpClient добавит его, если запрос представляет собой операцию записи (т. е. метод HTTP, отличный от GET, HEAD или OPTIONS). Дайджестом запроса управляет служба DigestCache. В случае промаха кэша может быть выполнен дополнительный сетевой запрос. |






