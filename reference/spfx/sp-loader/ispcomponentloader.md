<span data-ttu-id="713e2-p101">Интерфейс для загрузчика модулей. Разрешает загружать модули и скрипты (через SystemJS) и CSS на странице. Разрешает также доступ к манифестам, имеющимся на странице.</span><span class="sxs-lookup"><span data-stu-id="713e2-p101">Interface for the module loader. It allows to load modules and scripts (through SystemJS) and CSS on the page. Also allows access to the manifests that exist in the page.</span></span>







Интерфейс для загрузчика модулей. Разрешает загружать модули и скрипты (через SystemJS) и CSS на странице. Разрешает также доступ к манифестам, имеющимся на странице.







## <a name="methods"></a><span data-ttu-id="713e2-105">Методы</span><span class="sxs-lookup"><span data-stu-id="713e2-105">Methods</span></span>

| <span data-ttu-id="713e2-106">Метод</span><span class="sxs-lookup"><span data-stu-id="713e2-106">Method</span></span>       |  <span data-ttu-id="713e2-107">Что возвращается</span><span class="sxs-lookup"><span data-stu-id="713e2-107">Returns</span></span>   | <span data-ttu-id="713e2-108">Описание</span><span class="sxs-lookup"><span data-stu-id="713e2-108">Description</span></span>|
|:-------------|:-------|:-----------|
|[`loadComponent(manifest)`](loadcomponent-ispcomponentloader.md)      | `Promise<TComponent>` | <span data-ttu-id="713e2-109">Загружает компонент из манифеста.</span><span class="sxs-lookup"><span data-stu-id="713e2-109">Loads a component from a manifest.</span></span> |
|[`loadCss(url)`](loadcss-ispcomponentloader.md)      | `void` | <span data-ttu-id="713e2-110">Вставляет тег <link ... /> для таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="713e2-110">Inserts a <link ... /> tag for a stylesheet.</span></span> |
|[`loadScript(url,options)`](loadscript-ispcomponentloader.md)      | `Promise<TModule>` | <span data-ttu-id="713e2-111">Если дан URL-адрес, загружает скрипт.</span><span class="sxs-lookup"><span data-stu-id="713e2-111">Given a URL, load a script.</span></span> |




