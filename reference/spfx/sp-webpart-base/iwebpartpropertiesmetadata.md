<span data-ttu-id="154dc-p101">Используйте эту структуру, чтобы определить метаданные для свойств веб-части как сопоставление строки с IWebPartPropertyMetadata. Ключ — это путь json к свойству в свойствах веб-части. Путь json поддерживает следующие операторы: – точка "." для выбора элементов объекта, например person.name – квадратные скобки "[]" для выбора элементов массива, например person.photoURLs[0] – звездочка в квадратных скобках "[*]" в качестве подстановочного знака элементов массива, например person.websites[*]. Эти операторы можно сочетать, например person.websites[*].url. Важное примечание. Поддерживается только один подстановочный знак на путь. Пример. Предположим, что у нас есть веб-часть со свойствами, которые имеют следующую схему: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Мы можем определить метаданные для нужных свойств следующим образом: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } В результате серверы SharePoint узнают о содержимом свойств и смогут выполнять индексирование поиска, корректировку ссылок и другую обработку данных. Если любое из значений необходимо обновить с помощью этих служб, например корректировка ссылок, контейнер свойств веб части обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="154dc-p101">This structure is used to define metadata for web part propeties as a map of string to IWebPartPropertyMetadata The key should be a json path to the property in web part propeties. The json path supports the following operators: - Dot . for selecting object members e.g. person.name - Brackets [] for selecting array items e.g. person.photoURLs[0] - Bracketed asterisk [*] for array elements wildcard e.g. person.websites[*]. You can make combinations of these operators e.g. person.websites[*].url Important Note: Only one wildcard per path is supported. Example: Let's assume we have a web part with properties that have the following schema: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } We can define the metadata for the desired properties as following: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } This will make SharePoint servers aware of the content of your properties and run services such as search indexing, link fix-up, etc on the data. In case any of the values needs to update by these services, e.g link fix-up, the web part property bag is automatically updated.</span></span>







Используйте эту структуру, чтобы определить метаданные для свойств веб-части как сопоставление строки с IWebPartPropertyMetadata. Ключ — это путь json к свойству в свойствах веб-части. Путь json поддерживает следующие операторы: – точка "." для выбора элементов объекта, например person.name – квадратные скобки "[]" для выбора элементов массива, например person.photoURLs[0] – звездочка в квадратных скобках "[*]" в качестве подстановочного знака элементов массива, например person.websites[*]. Эти операторы можно сочетать, например person.websites[*].url. Важное примечание. Поддерживается только один подстановочный знак на путь. Пример. Предположим, что у нас есть веб-часть со свойствами, которые имеют следующую схему: { title: string; person: { name: string; bio: string; photoURLs: string[]; websites: { title: string; url: string; }[] } } Мы можем определить метаданные для нужных свойств следующим образом: { 'person.bio': { isRichContent: true }, 'person.photoURLs[*]': { isImageSource: true }, 'person.websites[*].url': { isLink: true } } В результате серверы SharePoint узнают о содержимом свойств и смогут выполнять индексирование поиска, корректировку ссылок и другую обработку данных. Если любое из значений необходимо обновить с помощью этих служб, например корректировка ссылок, контейнер свойств веб части обновляется автоматически.







## <a name="methods"></a><span data-ttu-id="154dc-107">Методы</span><span class="sxs-lookup"><span data-stu-id="154dc-107">Methods</span></span>

| <span data-ttu-id="154dc-108">Метод</span><span class="sxs-lookup"><span data-stu-id="154dc-108">Method</span></span>       |  <span data-ttu-id="154dc-109">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="154dc-109">Returns</span></span>   | <span data-ttu-id="154dc-110">Описание</span><span class="sxs-lookup"><span data-stu-id="154dc-110">Description</span></span>|
|:-------------|:-------|:-----------|
|[`index()`](__index-iwebpartpropertiesmetadata.md)      | `IWebPartPropertyMetadata` |  |




