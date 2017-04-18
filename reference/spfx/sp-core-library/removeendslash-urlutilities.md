# <a name="removeendslashurl"></a>removeEndSlash(url)




Удаляет косую черту в конце URL-адреса. Эта функция предполагает, что входная строка уже является действительным URL-адресом (абсолютным или относительным). Примеры: removeEndSlash('http://example.com/') ---> 'http://example.com' removeEndSlash('/example') ---> '/example' removeEndSlash('/') ---> ''

**Подпись:** _public static removeEndSlash(url: string): string;_

**Возвращаемое значение**: `string`





#### <a name="parameters"></a>Параметры


| Параметр       | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | Нормализуемый URL-адрес |


