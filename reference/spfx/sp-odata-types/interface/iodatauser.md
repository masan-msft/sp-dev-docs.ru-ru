# <a name="iodatauser-interface"></a>Интерфейс IODataUser







Представляет объект OData SP.User. Дополнительные сведения об этом объекте см. в документации MSDN на странице https://msdn.microsoft.com/ru-ru/library/office/jj860569.aspx.




## <a name="properties"></a>Свойства

| Свойство     | Тип   | Описание|
|:-------------|:-------|:-----------|
|`Email`      | `string` | Пример: "proverka@example.com". |
|`Id`      | `number` |  |
|`IsSiteAdmin`      | `boolean` | Логическое значение, определяющее, является ли пользователь администратором семейства веб-сайтов. |
|`LoginName`      | `string` | Пример: "i:0#.w|domain\user". |
|`PrincipalType`      | `number` | Это перечисление имеет атрибут FlagsAttribute, который допускает побитовую комбинацию значений его членов. None: 0. User: 1. DistributionList: 2. SecurityGroup: 4. SharePointGroup: 8. All: 15. |
|`Title`      | `string` | Пример: "DOMAIN\user". |
|`UserId`      | `IODataUserId` | Возвращает информацию о пользователе, содержащую идентификатор имени пользователя и издателя этого идентификатора. |






