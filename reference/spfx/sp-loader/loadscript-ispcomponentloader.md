# <a name="loadscripturloptions"></a>loadScript(url,options)




Загружает сценарий с указанного URL-адреса.

**Подпись:** _loadScript < TModule >(url: string, options?: [ILoadScriptOptions](../sp-loader/iloadscriptoptions.md)): Promise<TModule>;_

**Что возвращается**: `Promise<TModule>`



Обещание, содержащее загруженный модуль.

#### <a name="parameters"></a>Параметры


| Параметр    | Тип    | Описание |
|:-------------|:---------------|:------------|
| `url`    | `string` | URL-адрес скрипта. |
| `options`    | [`ILoadScriptOptions`](../sp-loader/iloadscriptoptions.md) | __Дополнительно.__ globalExportsName. Если скрипт не является модулем AMD и загружает глобальный элемент на странице, укажите имя этого глобального элемента. |


