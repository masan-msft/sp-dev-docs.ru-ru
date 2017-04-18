# <a name="sppermission-class"></a>Класс SPPermission







Этот класс можно использовать, чтобы определить, есть ли у текущего пользователя запрашиваемый набор разрешений. Указывает встроенные разрешения, доступные в SharePoint Foundation и полученные из каталога OneDriveWeb/ODBNext/odsp-shared (https://msdn.microsoft.com/ru-ru/library/microsoft.sharepoint.spbasepermissions.aspx).


## <a name="constructor"></a>constructor


**Подпись:** _constructor(value: [IODataBasePermission](../sp-odata-types/iodatabasepermission.md));_

**Что возвращается**: 



#### <a name="parameters"></a>Параметры
Нет


## <a name="properties"></a>Свойства

| Свойство     | Модификатор доступа | Тип | Описание|
|:-------------|:----|:-------|:-----------|
|`addAndCustomizePages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Добавление, изменение или удаление HTML-страниц или страниц веб-частей, а также редактирование веб-сайта с помощью редактора, совместимого с SharePoint Foundation. |
|`addDelPrivateWebParts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Добавление и удаление личных веб-частей на странице веб-частей. |
|`addListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Добавление элементов в списки, документов — в библиотеки документов, а комментариев в веб-дискуссии — в документ. |
|`applyStyleSheets`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Применение таблицы стилей (CSS-файла) к веб-сайту. |
|`applyThemeAndBorder`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Применение темы или границ ко всему веб-сайту. |
|`approveItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Утверждение дополнительного номера версии элемента списка или документа. |
|`browseDirectories`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Нумерация файлов и папок на веб-сайте с помощью интерфейсов WebDAV и Microsoft Office SharePoint Designer 2007. |
|`browserUserInfo`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр сведений о пользователях веб-сайта. |
|`cancelCheckout`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Отмена или запись после изменения документа, который был получен для изменения другим пользователем. |
|`createAlerts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Создание предупреждений для отправки по электронной почте. |
|`createGroups`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Создание группы пользователей, которую можно применять во всем семействе веб-сайтов. |
|`createSSCSite`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Самостоятельное создание веб-сайтов. |
|`deleteListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Удаление элементов из списка, документов — из библиотеки документов, а комментариев в веб-дискуссиях — из документов. |
|`deleteVersions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Удаление предыдущих версий элемента списка или документа. |
|`editListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Редактирование элементов в списках, документов — в библиотеках документов, а комментариев в веб-дискуссиях — в документах, а также настройка страниц веб-частей в библиотеках документов. |
|`editMyUserInfo`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Разрешает пользователю изменять сведения о себе, например добавлять фотографию. |
|`emptyMask`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Не имеет разрешений на веб-сайте. Через пользовательский интерфейс недоступно. |
|`enumeratePermissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Перечисление разрешений для веб-сайта, списка, папки, документа или элемента списка. |
|`fullMask`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Имеет все разрешения на веб-сайте. Через пользовательский интерфейс недоступно. |
|`layoutsPage`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотреть страницу макетов? |
|`manageAlerts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Управление оповещениями для всех пользователей веб-сайта. |
|`manageLists`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Создание и удаление списков, добавление и удаление столбцов в списке, а также добавление и удаление общедоступных представлений списка. |
|`managePermissions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Создание и изменение уровней разрешений на веб-сайте и назначение разрешений пользователям и группам. |
|`managePersonalViews`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Создание, изменение и удаление личных представлений списков. |
|`manageSubwebs`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Создание дочерних сайтов, таких как сайты группы, веб-сайты рабочих областей для собраний и веб-сайты рабочих областей для документов. |
|`manageWeb`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Предоставляет возможность выполнить все задачи администрирования веб-сайта, а также управления контентом. Активация, деактивация и изменение свойств функций веб-сайта через объектную модель или пользовательский интерфейс. Если это разрешено на корневом веб-сайте семейства веб-сайтов, можно активировать, деактивировать и изменять свойства функций семейства веб-сайтов через объектную модель. Просматривать страницу функций семейства веб-сайтов, а также активировать или деактивировать такие функции через пользовательский интерфейс может только администратор семейства веб-сайтов. |
|`open`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Разрешает пользователям открывать веб-сайт, список или папку для доступа к элементам в этом контейнере. |
|`openItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр источника документов с помощью серверных обработчиков файлов. |
|`updatePersonalWebParts`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Обновление личных веб-частей для отображения персональных сведений. |
|`useClientIntegration`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Необходимо использовать функции запуска клиентских приложений. В противном случае пользователям придется работать с документами локально, а затем передавать изменения. |
|`useRemoteAPIs`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Использование интерфейсов SOAP, WebDAV или Microsoft Office SharePoint Designer 2007 для доступа к веб-сайту. |
|`value`     | `public` | [`IODataBasePermission`](../sp-odata-types/iodatabasepermission.md) | _Только для чтения._ Возвращает значение этого объекта SPPermission. |
|`viewFormPages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр форм, представлений и страниц приложений, а также перечисление списков. |
|`viewListItems`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр элементов в списках, а документов — в библиотеках документов, а также просмотр комментариев в веб-дискуссиях. |
|`viewPages`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр страниц веб-сайта. |
|`viewUsageData`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр отчетов об использовании веб-сайта. |
|`viewVersions`     | `public` | [`SPPermission`](../sp-page-context/sppermission.md) | Просмотр предыдущих версий элемента списка или документа. |




## <a name="methods"></a>Методы

| Метод       | Модификатор доступа | Что возвращается  | Описание|
|:-------------|:----|:-------|:-----------|
|[`hasAllPermissions(...requestedPerms)`](hasallpermissions-sppermission.md)     | `public` | `boolean` | Эта функция определяет, есть ли у заданной маски разрешений все запрашиваемые разрешения. |
|[`hasAnyPermissions(...requestedPerms)`](hasanypermissions-sppermission.md)     | `public` | `boolean` | Эта функция определяет, есть ли у заданной маски разрешений какое-либо из запрашиваемых разрешений. |
|[`hasPermission(requestedPerm)`](haspermission-sppermission.md)     | `public` | `boolean` | Эта функция проверяет, есть ли у заданной маски разрешений запрашиваемое разрешение. |





