# <a name="iodatalist-interface"></a>Интерфейс IODataList







Представляет объект OData SP.List. Дополнительные сведения об этом объекте см. в документации MSDN на странице https://msdn.microsoft.com/ru-ru/library/office/jj860569.aspx.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`BaseTemplate`      | `number` | Тип определения списка, на котором основан список. |
|`Created`      | `string` | Пример: "/Date(1453294804000)/". |
|`CurrentChangeToken`      | [`IODataChangeToken`](../sp-odata-types/iodatachangetoken.md) | Токен изменений, который будет использоваться при регистрации следующего изменения в списке. |
|`Description`      | `string` | Описание списка. |
|`EntityTypeName`      | `string` | Пример: "MyListTitleList". |
|`Hidden`      | `boolean` | Скрытый список не отображается на странице "Документы и списки", панели быстрого запуска, странице "Изменение контента сайта" или странице "Добавление столбца" в качестве параметра для полей подстановки. |
|`Id`      | `string` | Пример: "/Guid(9fb9199b-65f2-4a4a-b597-11d1a44422c1)/". |
|`LastItemDeletedDate`      | `string` | Пример: "/Date(1453294809000)/". |
|`LastItemModifiedDate`      | `string` | Пример: "/Date(1453294809000)/". |
|`ListItemEntityTypeFullName`      | `string` | Пример: "SP.Data.MyListTitleListItem". |
|`ParentWebUrl`      | `string` | Пример: "/sites/PubSite". |
|`TemplateFeatureId`      | `string` | Пример: "/Guid(22a9ef51-737b-4ff2-9346-694633fe4416)/". |
|`Title`      | `string` | Пример: "Pages". |






