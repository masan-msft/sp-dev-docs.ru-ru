# <a name="ispcomponentloader-interface"></a>Интерфейс ISPComponentLoader







Интерфейс для загрузчика модулей. Разрешает загружать модули и скрипты (через SystemJS) и CSS на странице. Разрешает также доступ к манифестам, имеющимся на странице.







## <a name="methods"></a>Методы

| Метод       |  Что возвращается   | Описание|
|:-------------|:-------|:-----------|
|[`loadComponent(manifest)`](loadcomponent-ispcomponentloader.md)      | `Promise<TComponent>` | Загружает компонент из манифеста. |
|[`loadCss(url)`](loadcss-ispcomponentloader.md)      | `void` | Вставляет тег <link ... /> для таблицы стилей. |
|[`loadScript(url,options)`](loadscript-ispcomponentloader.md)      | `Promise<TModule>` | Если дан URL-адрес, загружает скрипт. |




