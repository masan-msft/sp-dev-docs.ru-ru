# <a name="isphttpclientcommonconfiguration-interface"></a>Интерфейс ISPHttpClientCommonConfiguration







Интерфейс флажков для SPHttpClientCommonConfiguration




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`jsonRequest`      | `boolean` | Когда этому параметру присвоено значение true, выполняется указанное далее действие. Если заголовок "Content-Type" не был явно добавлен для запроса, SPHttpClient добавит его, при условии, что запрос представляет собой операцию записи (т. е. метод HTTP, отличный от GET, HEAD или OPTIONS). Для OData 3.0 значение следующее: "application/json;odata=verbose;charset=utf-8". Для OData 4.0 значение следующее: "application/json;charset=utf-8". |
|`jsonResponse`      | `boolean` | Когда этому параметру присвоено значение true, выполняется указанное далее действие. Если заголовок "Accept" не был явно добавлен для запроса, SPHttpClient его добавит. Для OData 3.0 значение следующее: "application/json". Для OData 4.0 значение следующее: "application/json;odata.metadata=minimal". |






