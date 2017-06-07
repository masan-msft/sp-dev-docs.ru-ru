# <a name="iserializedserverprocesseddata-interface"></a>Интерфейс ISerializedServerProcessedData







Содержит наборы данных, которые могут обрабатываться серверными службами, например службами индексирования поиска и корректировки ссылок.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`htmlStrings`      | `{ [key: string]: string }` | Карта "ключ-значение", где ключи — это идентификаторы строк, а значения — текст в формате HTML. Серверы SharePoint расценивают значения как HTML-контент и выполняют проверку безопасности, индексирование поиска и корректировку ссылок. Пример: { 'myRichDescription': '<div>Стандартный <b>HTML-контент</b><a href='http://somelink'>Ссылка</a></div>' 'anotherRichText': <div class='aClass'><span style='color:red'>Красный текст</div> } |
|`imageSources`      | `{ [key: string]: string }` | Карта "ключ-значение", где ключи — это идентификаторы строк, а значения — источники изображений. Серверы SharePoint расценивают значения как источники изображений и выполняют индексирование поиска и корректировку ссылок. Пример: { 'myImage1': 'http://res.contoso.com/path/to/file' 'myImage2': 'https://res.contoso.com/someName.jpg' } |
|`links`      | `{ [key: string]: string }` | Карта "ключ-значение", где ключи — это идентификаторы строк, а значения — ссылки. Серверы SharePoint расценивают значения как ссылки и выполняют корректировку ссылок. Пример: { 'myWebURL': 'http://contoso.com' 'myFileLink': 'https://res.contoso.com/file.docx' } |






