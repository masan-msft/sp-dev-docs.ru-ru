# <a name="servicekey-t-class"></a>Класс ServiceKey <T>



_Параметры типов: `<T>`_



ServiceKey — это ключ поиска, используемый при вызове метода ServiceScope.consume() для получения зависимости. Кроме того, этот ключ определяет версию зависимости по умолчанию, которую автоматически создает корневая область, если зависимость не найдена. Указав версию по умолчанию, вы сможете безопасно добавлять новые зависимости, не нарушая работу компонентов, загруженных старым основным приложением (которое не предоставляет новую зависимость).


## <a name="constructor"></a>constructor
ЧАСТНЫЙ — не вызывайте его из своего кода.

**Подпись:** _constructor(id: string, name: string, defaultCreator: ServiceCreator<T>);_

**Возвращаемое значение**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`defaultCreator`     | `public` | `ServiceCreator<T>` |  |
|`id`     | `public` | `string` |  |
|`name`     | `public` | `string` |  |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`create(name,serviceClass)`](create-servicekey.md)     | `public, static` | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Создает новый объект ServiceKey, версией по умолчанию которого будет новый экземпляр класса TypeScript, принимающий стандартный параметр конструктора. Чтобы указать пользовательские параметры конструктора, используйте метод createCustom(). |
|[`createCustom(name,defaultCreator)`](createcustom-servicekey.md)     | `public, static` | [`ServiceKey`](../sp-core-library/servicekey.md)<T> | Создает новый объект ServiceKey, реализацию по умолчанию для которого можно получить с помощью указанного метода обратного вызова. |




