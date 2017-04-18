# <a name="spcomponentloader-class"></a>Класс SPComponentLoader







Загрузчик компонентов. Необходима инициализация с помощью внедренного ISPComponentLoader.






## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`initialize()`](initialize-spcomponentloader.md)     | `public, static` | `void` | Инициализирует загрузчик компонентов с внедрением. Перед использованием необходимо вызвать один раз. |
|[`loadComponent()`](loadcomponent-spcomponentloader.md)     | `public, static` | `Promise<TComponent>` | {@inheritdoc ISPComponentLoader.loadComponent} |
|[`loadCss()`](loadcss-spcomponentloader.md)     | `public, static` | `void` | {@inheritdoc ISPComponentLoader.loadCss} |
|[`loadScript()`](loadscript-spcomponentloader.md)     | `public, static` | `Promise<TModule>` | {@inheritdoc ISPComponentLoader.loadScript} |





