# <a name="team-based-development-on-the-sharepoint-framework"></a>Командная разработка на SharePoint Framework

SharePoint Framework — это новая модель разработки настроек SharePoint. В отличие от других доступных на сегодняшний день моделей, SharePoint Framework связана с клиентской разработкой и создана на основе таких популярных инструментов с открытым кодом, как gulp и webpack. Важным преимуществом этого изменения является то, что настройки SharePoint могут создавать разработчики на любой платформе.

SharePoint Framework — это модель разработки и, несмотря на различия в основной технологии, к ней применяются те же понятия, что и к другим моделям разработки SharePoint, использовавшимся в прошлом. Разработчики создают и проверяют решения с помощью цепочки инструментов SharePoint Framework, а затем сдают пакет решения, который развертывается на клиенте SharePoint для дополнительной проверки и выпуска.

SharePoint Framework состоит из нескольких пакетов. Эти пакеты, каждый из которых находится на собственной стадии разработки, составляют выпуск SharePoint Framework. Например, общедоступная версия SharePoint Framework состоит из следующих пакетов:

- @microsoft/sp-client-base 1.0.0
- @microsoft/sp-core-library 1.0.0
- @microsoft/sp-webpart-base 1.0.0
- @microsoft/sp-build-web 1.0.0
- @microsoft/sp-module-interfaces 1.0.0
- @microsoft/sp-webpart-workbench 1.0.0

Проект, предназначений для определенного выпуска SharePoint Framework, должен ссылаться на правильные версии пакетов. При создании новых проектов генератор Yeoman автоматически добавляет необходимые ссылки на пакет из соответствующего выпуска SharePoint Framework. Но при переносе проекта на новую версию SharePoint Framework разработчики должны правильно обновить номера версий пакетов SharePoint Framework.

## <a name="preparing-the-development-environment"></a>Подготовка среды разработки

Для создания решений SharePoint Framework нужны специальные средства на компьютерах разработки. В отличие от других моделей разработки SharePoint, SharePoint Framework не ограничивает разработчиков в выборе средств и операционной системы.

Разработчики могут настроить среду разработки несколькими способами. Каждый из них имеет свои преимущества, и важно, чтобы команды разработчиков были знакомы со всеми вариантами.

### <a name="sharepoint-framework-toolchain"></a>Цепочка инструментов SharePoint Framework

При создании решений SharePoint Framework необходимо использовать определенный набор инструментов. Ниже представлен основной набор инструментов, обязательный для всех сред разработки SharePoint Framework.

#### <a name="nodejs"></a>Node.js

На компьютере разработчика должна быть установлена платформа Node.js. Node.js используется как среда выполнения для средств разработки и упаковки проекта. Платформа Node.js устанавливается на компьютере разработчика глобально, и при необходимости несколько версий Node.js могут работать одновременно.

> Дополнительные сведения об установке Node.js и поддерживаемых версиях см. на странице [https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment](https://dev.office.com/sharepoint/docs/spfx/set-up-your-development-environment).

#### <a name="npm"></a>Npm

Npm — это аналог NuGet в проектах .NET: он позволяет разработчикам приобрести и установить пакеты для использования в проектах SharePoint Framework. Npm также используется для установки цепочки инструментов SharePoint Framework. Обычно разработчики используют последнюю версию npm и устанавливают ее глобально на компьютере. Npm — это пакет Node.js, поэтому, если вы используете несколько версий Node.js одновременно, для каждой будет установлена собственная версия npm.

#### <a name="gulp"></a>gulp

gulp — это аналог MSBuild в проекте .NET и отвечает за выполнение таких задач, как сборка и упаковка проекта SharePoint Framework. gulp распространяется в виде пакета Node.js и обычно устанавливается глобально с помощью npm.

#### <a name="yeoman-and-sharepoint-framework-yeoman-generator"></a>Yeoman и генератор SharePoint Framework Yeoman

Разработчики создают проекты SharePoint Framework с помощью Yeoman и генератора SharePoint Framework Yeoman. Yeoman и генераторы распространяются в виде пакетов Node.js и обычно устанавливаются глобально с помощью npm. Преимущество глобальный установки заключается в том, что разработчики могут установить Yeoman и генераторы один раз и использовать их для создания проектов.

Генератор Yeoman связан с определенной версией SharePoint Framework. Проекты, созданные с помощью генератора, ссылаются на определенные версии пакетов SharePoint Framework, а созданные веб-части — на определенные части платформы. Генератор SharePoint Framework Yeoman используется для создания проектов, а также для добавления веб-частей в существующие проекты. Если вы установите его глобально и добавите новую веб-часть в существующий проект, она может оказаться несовместимой с остальной частью проекта, что может привести к ошибкам сборки. Это ограничение можно обойти несколькими способами, которые описаны далее в этой статье.

#### <a name="typescript"></a>TypeScript

SharePoint Framework использует TypeScript, чтобы разработчики могли работать эффективнее, оптимизируя написание кода и находя ошибки во время самой разработки. Проекты SharePoint Framework поставляются с собственной версией TypeScript, которая используется в процессе сборки и не требует отдельной установки.

### <a name="building-a-sharepoint-framework-development-environment"></a>Создание среды разработки SharePoint Framework

В прошлом в качестве среды разработки SharePoint обычно использовались виртуальные машины. Они позволяли создать решение, которое точно будет работать в среде, используемый в определенной организации. На виртуальных машинах разработчики устанавливали SharePoint и обновляли его в соответствии с рабочей средой, используемой в конкретной организации. В некоторых случаях они устанавливали дополнительное программное обеспечение, чтобы среда разработки максимально соответствовала целевой среде, в которой будет использоваться решение. Этот подход был сложным и подразумевал управление различными средами, но позволял разработчикам раньше находить ошибки, вызываемые разницей в средах.

Переход на решения разработки для облака только частично решил эти проблемы. Разработчикам больше не нужно было запускать ферму SharePoint на своих компьютерах разработки, но им приходилось учитывать способ размещения решения и взаимодействия с SharePoint Online.

Так как SharePoint Framework связан с клиентской разработкой, SharePoint больше не нужно устанавливать на компьютерах разработки. За редким исключением, все зависимости от платформы и другие пакеты указываются в проекте и содержатся в папке проекта. Так как платформа SharePoint Framework появилась из облака и постоянно эволюционирует, разработчики должны использовать правильную версию цепочки инструментов, соответствующую проекту SharePoint Framework.

#### <a name="shared-or-a-personal-development-environment"></a>Общая или личная среда разработки

Среди настроек SharePoint есть как простые сценарии, добавляемые прямо на страницу, так и сложные решения, развертываемые как пакеты решений. SharePoint Framework — это модель разработки, предназначенная для структурированной и стандартной модели развертывания настроек SharePoint. При создании решений SharePoint Framework каждый разработчик в команде использует собственную среду разработки и делится исходным кодом проекта с другими разработчиками через систему управления версиями. Таким образом разработчики могут одновременно работать над одним проектом и проверять решения, не мешая друг другу.

В прошлом многие организации не могли обеспечить разработчиков SharePoint мощными компьютерами, и иногда нескольким разработчикам приходилось использовать один компьютер и работать менее эффективно. Благодаря SharePoint Framework разработчики могут использовать стандартные компьютеры для создания настроек SharePoint.

#### <a name="developing-on-the-host"></a>Разработка на хост-компьютере

Самый простой способ настроить среду разработки для проектов SharePoint Framework — установить все средства непосредственно на хост-компьютере. Если ваша команда работает только над проектами SharePoint Framework, разработчики могут установить Node.js на своих компьютерах. Если они работают и над другими проектами Node.js, они могут использовать сторонние решения, такие как [nvm](https://github.com/creationix/nvm), для одновременного запуска нескольких версий Node.js.

После средств, необходимых для цепочки инструментов SharePoint Framework, разработчики устанавливают Yeoman и генератор SharePoint Framework Yeoman. Обычно оба эти средства устанавливаются глобально. Однако поскольку генератор SharePoint Framework Yeoman связан с определенной версией SharePoint Framework, разработчикам может потребоваться удалить генератор, а затем установить версию для проекта, над которым они работают в данный момент. Целесообразнее установить Yeoman и генератор SharePoint Framework Yeoman локально в проекте. Несмотря на определенные издержки, так разработчики могут обеспечить совместимость новых элементов с остальной частью проекта.

Преимуществом разработки на хост-компьютере является то, что разработчик может настроить компьютер по своему вкусу и использовать его для всех проектов. Кроме того, при выполнении программного обеспечения на хост-компьютере оно имеет прямой доступ к ЦП и памяти и диску, что гарантирует лучшую производительность, чем при выполнении того же программного обеспечения на виртуальной машине.

#### <a name="developing-in-a-virtual-machine"></a>Разработка на виртуальной машине

В прошлом большинство разработчиков SharePoint использовали виртуальные машины в качестве основной среды разработки для создания решений SharePoint. С помощью виртуальных машинах разработчики могли обеспечить соответствие разным требованиям к разным проектам.

При создании решений в SharePoint Framework организации получают те же преимущества, что и при создании решений SharePoint в прошлом. С помощью виртуальных машин они могут изолировать программное обеспечение разработки от операционной системы хост-компьютера, что часто требуется, особенно в больших организациях. Создав отдельную виртуальную машину для каждого проекта, разработчики могут обеспечить совместимость используемой цепочки инструментов с проектом, даже если к нему придется вернуться в будущем.

Использование виртуальных машин имеет свои недостатки. Виртуальные машины занимают много места, и для их приемлемой работы требуются достаточно мощные компьютеры. Кроме того, время от времени разработчики должны обновлять операционную систему и устанавливать все необходимые обновления для системы безопасности. Разработчики должны тратить некоторое время в начале нового проекта на настройку стандартной виртуальной машины по своему вкусу или использовать стандартные настройки и работать менее эффективно. Так как на виртуальных машинах запускается полная операционная система со всеми компонентами, гораздо труднее обеспечить совместимость всех виртуальных машин, используемых всеми разработчиками в команде. По сравнению с другими средами разработки, создание решений SharePoint Framework с помощью виртуальных машин требует больше денег и времени.

#### <a name="developing-using-docker"></a>Разработка с использованием Docker

Использование Docker — это интересный компромисс между разработкой на хост-компьютере и виртуальной машине. Docker — это технология виртуализации программного обеспечения, похожая на виртуальные машины, но имеющая несколько существенных отличий. Самые важные преимущества образов Docker над виртуальными машинами: образы Docker проще создавать, обслуживать и распространять, они занимают меньше места на диске (несколько сотен МБ по сравнению с десятками ГБ для виртуальных машинах) и позволяют разработчикам использовать средства и параметры, которые они уже установили и настроили на хост-компьютере.

Так же как на виртуальных машинах, в контейнерах Docker запускается виртуализированный экземпляр операционной системы (обычно на основе Linux). Все программное обеспечение, установленное в образе, используемом для создания контейнера, выполняется изолированно внутри этого контейнера и имеет доступ только к части файловой системы хост-компьютера. Так как все изменения, внесенные в файловую систему внутри контейнера Docker, отменяются после закрытия контейнера, разработчики используют общие папки на хост-компьютере для хранения исходного кода.

Узнайте больше об [использовании Docker для создания решений SharePoint Framework](https://rencore.com/blog/try-sharepoint-framework-without-installing).

## <a name="development-workflow-in-sharepoint-framework-projects"></a>Схема разработки проектов SharePoint Framework

Платформа SharePoint Framework основана на цепочке инструментов с открытым кодом, и использует общую схему разработки, представленную в других проектах, основанных на том же стеке. Ниже описана схема разработки типичного проекта SharePoint Framework.

### <a name="create-new-sharepoint-framework-project"></a>Создание нового проекта SharePoint Framework

При создании настроек SharePoint с помощью SharePoint Framework сначала формируется шаблон нового проекта SharePoint Framework. Для этого используется генератор SharePoint Framework Yeoman. Генератор попросит вас ответить на несколько вопросов, связанных с названием проекта или его расположением. Он также позволит вам создавать первую веб-часть. Важно помнить, что платформа, на которой создана первая веб-часть, будет автоматически использоваться для всех веб-частей, которые будут добавлены в проект позднее. Вы можете вручную изменить платформу, но мы рекомендуем использовать одну платформу в проекте SharePoint Framework.

### <a name="lock-dependencies-version"></a>Блокировка версии зависимостей

Новый проект SharePoint Framework, создании генератором Yeoman, имеет зависимости от пакетов SharePoint Framework, а также других пакетов, необходимых для его правильной работы. В ходе создания веб-частей можно добавлять зависимости, например Angular или jQuery. В проектах SharePoint Framework зависимости устанавливаются с помощью npm. Каждая зависимость — это пакет Node.js определенной версии. По умолчанию для ссылки на зависимости используется диапазон версий, чтобы разработчикам было проще их обновлять. Вследствие этого восстановление зависимостей для одного проекта в два момента времени может дать разные результаты и даже привести к нарушению работы проекта.

Чтобы избежать изменения зависимостей в проекте, основанном на цепочке инструментов с открытым кодом, заблокируйте версии всех зависимостей. При добавлении зависимости в проект разработчики могут установить зависимость определенной версии, а не диапазон версий, вызвав команду `npm install` с аргументом `--save-exact`. Однако это никак не влияет на дочерние зависимости пакета. Чтобы заблокировать версии всех зависимостей и их дочерних зависимостей в проекте, разработчики могут использовать команду `npm shrinkwrap`. Она создаст список всех зависимостей и их версий на момент выполнения и запишет его в файл **npm-shrinkwrap.json**, который необходимо включить в систему управления версиями. При восстановлении зависимостей npm будет использовать версии из этого файла, а не последнюю версию из определенного диапазона версий.

> Примечание. Если в папке **node_modules** установлены пакеты, которые не указаны как зависимости в файле **package.json** или не являются зависимостью одного из пакетов, скорее всего, при создании файла **npm-shrinkwrap.json** возникнет ошибка. В этом случае вы можете либо добавить пакеты, из-за которых возникает ошибка, в файл **package.json**, либо удалить их из папки **node_modules**, либо удалить папку **node_modules**, восстановить все зависимости, а затем создать файл shrinkwrap.

### <a name="add-the-project-to-source-control"></a>Добавление проекта в систему управления версиями

Чтобы все члены команды могли работать над одним проектом, добавьте его в систему управления версиями. Необходимые действия зависят от системы, которую использует ваша команда.

Проекты SharePoint Framework создаются с файлом **.gitignore**, в котором указывается, какие файлы следует исключить из системы управления версиями. Если ваша команда использует систему управления версиями, отличную от Git (например, систему Visual Studio Team System с репозиториями Team Foundation System), убедитесь, что в систему управления версиями включаются соответствующие файлы из проекта. Кроме того, исключение зависимостей и созданных автоматически файлов во время сборки позволяет обеспечить эффективную работу команды.

Особенно важно не включать в систему управления версиями папку **node_modules**. Эта папка содержит пакеты, от которых зависит проект и которые автоматически устанавливаются при восстановлении зависимостей с помощью команды `npm install`. Некоторые пакеты компилируются в двоичные файлы, при этом процесс компиляции зависит от операционной системы. Если команда работает в другой операционной системе, включение папки **node_modules** в систему управления версиями, скорее всего, разрушит сборку для некоторых членов команды.

### <a name="get-the-project-from-source-control"></a>Получение проекта из системы управления версиями

При первом получении проекта из системы управления версиями вы получите исходный код проекта, но не библиотеки SharePoint Framework, необходимые для его сборки. Так же, как при работе с проектами .NET и использовании пакетов NuGet, сначала необходимо восстановить зависимости. В проектах SharePoint Framework, так же как во всех проектах, основанных на Node.js, для этого необходимо выполнить команду `npm install` в командной строке. npm использует сведения из файлов **package.json** и **npm-shrinkwrap.json** и установит все пакеты.

> Примечание. Обычно для восстановления зависимостей с помощью команды `npm install` необходимо подключение к Интернету, так как пакеты скачиваются с сайта _registry.npmjs.org_. Если у вас есть проблемы с подключением к сети или реестр npmjs недоступен, выполнить сборку не удастся. Обойти это ограничение можно несколькими способами. Вы можете скачать tar-архивы всех зависимостей с помощью команды [shrinkpack](https://github.com/JamieMason/shrinkpack) и сохранить их в системе управления версиями. Shrinkpack автоматически обновляет файл npm-shrinkwrap.json для использования локальных tar-архивов, позволяя устанавливать зависимости проекта в автономном режиме.

Некоторые пакеты во время установки компилируются в двоичные файлы. Этот процесс зависит от архитектуры и операционной системы. Например, если вы восстановите зависимости в контейнере Docker под управлением Linux, а затем попробуйте выполнить сборку проекта на хост-компьютере с Windows, возникнет ошибка из-за несоответствия типа среды, используемого для сборки и выполнения двоичных файлов.

В ходе разработки решения в проект могут добавляться новые или обновленные зависимости. Если файл **package.json** изменился с момента последнего получения проекта из системы управления версиями, нужно выполнить команду `npm install` в командной строке, чтобы установить отсутствующие зависимости. Если вы не уверены, изменился ли файл **package.json**, вы можете выполнить команду `npm install` в командной строке, просто чтобы убедиться, что у вас есть последние зависимости, не нарушая работу проекта.

### <a name="add-packages-to-your-project"></a>Добавление пакетов в проект

Использование существующих пакетов для выполнения определенных задач позволяет работать более эффективно. npmjs.com — это общедоступный реестр пакетов, которые можно использовать в проекте.

> Примечание. Так как перед публикацией на сайте npmjs.com пакет не проходит проверку, перед использованием тщательно изучите его содержимое и лицензию.

Чтобы добавить пакет в проект SharePoint Framework, выполните команду `npm install <package> --save` или `npm install <package> --save-dev` в командной строке, например `npm install angular --save`. Использование аргумента `--save` или `--save-dev` гарантирует, что пакет будет добавлен в файл **package.json** и другие разработчики в команде также получат его при восстановлении зависимостей. Без него не удастся выполнить сборку проекта на другом компьютере. При добавлении пакетов, необходимых решению при запуске, например Angular или jQuery, используйте аргумент `--save`. При установке пакетов, необходимых в процессе сборки, например дополнительных задач gulp, используйте аргумент `--save-dev`.

Если не указана версия, npm устанавливает последнюю версию, доступную в реестре пакетов (npmjs.com по умолчанию). Версию пакета необходимо указать, если вы используете файл **npm-shrinkwrap.json** и хотите обновить существующий пакет до новой версии. По умолчанию npm устанавливает версию, указанную в файле **npm-shrinkwrap.json**. Если в команде `npm install` указан номер версии, например `npm install angular@1.5.9 --save`, будет установлен этот пакет и обновлен номер версии в файле **npm-shrinkwrap.json**.

## <a name="working-with-internal-packages"></a>Работа с внутренними пакетами

По мере разработки клиентских решений вы, скорее всего, соберете общие библиотеки кода, которые захотите использовать во всех проектах. Во многих случаях такие библиотеки содержат проприетарный код, доступный за пределами организации только в пакетах, развернутых в рабочей среде. Ваша команда может использовать внутренние библиотеки в своих проектах SharePoint Framework несколькими способами.

### <a name="hosting-private-package-registry"></a>Размещение частного реестра пакетов

В прошлом многие организации, создающие решения .NET, размещали частные репозитории NuGet на своих серверах, чтобы использовать систему управления пакетами NuGet для своих внутренних пакетов. Так как SharePoint Framework использует систему npm для управления пакетами, организации так же могут использовать частный реестр для своих внутренних пакетов. После публикации эти пакеты можно будет использовать во всех проектах организации.

Частный реестр пакетов можно разместить в облаке или на собственном сервере.

С помощью частного реестра пакетов организации могут централизованно управлять общим кодом, используемым в разный проектах. Составив отдельный план действий по добавлению изменений в общую базу кода, организации могут обеспечить высокое качество библиотеки и надлежащую эффектность использования для всех разработчиков.

Популярным частным реестром, размещенным в облаке, является [npm Enterprise](https://www.npmjs.com/enterprise). Организациям, которые хотят разместить реестр самостоятельно, предлагается на выбор несколько подсистем с открытым кодом, таких как [Sinopia](https://github.com/rlidwka/sinopia), [Verdaccio](https://github.com/verdaccio/verdaccio) или [Nexus](https://www.sonatype.com/nexus-repository-oss).

> Примечание. Разные подсистемы для размещения частных реестров пакетов находятся на разных стадиях разработки, и вам следует внимательно проверить, соответствует ли определенная подсистема вашим требованиям с точки зрения функций, лицензии и поддержки.

Чтобы упростить установку частного реестра пакетов и управление им, большинство подсистем предлагаются с готовыми образами Docker.

### <a name="linking-packages-using-npm-link"></a>Связывание пакетов с помощью команды npm link

Не обязательно использовать частный реестр — пакеты можно связывать. При этом не требуется настройка реестра, но требуется четкая координация действий на всех компьютерах для разработки и сервере сборки.

Сначала каждый разработчик в команде должен скачать копию общего пакета на свой компьютер для разработки. В командной строке они должны изменить рабочий каталог на каталог общего пакета, а затем выполнить команду `npm link`. Эта команда регистрирует пакет как глобальный пакет на этом компьютере для разработки. После этого разработчики должны изменить рабочий каталог на каталог проекта, в котором они хотят использовать общий пакет. Затем они должны установить пакет так же, как любой другой пакет, выполнив команду `npm install <shared_package> --save` в командной строке. Так как общий пакет установлен глобально, npm будет использовать эту версию для установки пакета. На этом этапе пакет установлен так же, как любой другой общедоступный пакет, и разработчики могут выбрать способ связывания пакета с проектом.

Связывание пакета необходимо выполнить на всех компьютерах для разработки, а также на сервере сборки. Если общий пакет не связан с помощью команды `npm link`, восстановление зависимостей проекта разрушит сборку.

Особенно полезно ссылаться на связанные пакеты в начале проекта при одновременной разработке общего пакета и проекта. Благодаря связыванию не нужно публиковать новую версию пакета в реестре, чтобы использовать последний код в проекте. Обратите внимание, что если разработчики будут ссылаться на версию общей библиотеки, измененную локально и не добавленную в систему управления версиями, это разрушит сборку для остальных членов команды.

### <a name="combining-private-package-registry-and-linking-packages"></a>Сочетание частного реестра пакетов и связывания пакетов

Связывание пакетов можно сочетать с частным реестром. Например, разработчики могут ссылаться на связанный пакет, а сервер сборки — скачивать общую библиотеку из частного реестра. С точки зрения проекта ничего не меняется: ссылку на пакет в файле **package.json** можно обработать как из связанного пакета, так и из частного реестра. Команде остается только публиковать последние изменения в общей библиотеке в частном реестре перед выполнением сборки.

Так как код общей библиотеки со временем стабилизируется и для отдельных проектов требуется меньше изменений, разработчики, скорее всего, будут просто ссылаться на опубликованный пакет из частного реестра, а не изменять его.

## <a name="ensuring-code-consistency-and-quality"></a>Обеспечение единообразия и качества кода

Часто командам разработчиков программного обеспечения тяжело обеспечить единообразие и высокое качество своих проектов. У разных разработчиков разные стили написания кода. В каждой команде есть квалифицированные специалисты и разработчики, у которых меньше опыта в определенной сфере. Кроме того, у многих организаций и отраслей есть требования, которым должно соответствовать программное обеспечение. Из-за всех этих задач разработчикам сложнее не выбиться из графика. Особенно перед сдачей проекта разработчики часто не обращают внимание на качество, что в долгосрочной перспективе оказывается хуже, чем не уложиться в сроки.

### <a name="choose-javascript-library-for-your-team-and-use-coding-standards"></a>Выберите библиотеку JavaScript для команды и используйте стандарты кодирования

Если ваша команда не впервые создает настройки SharePoint, скорее ли, у вас есть стандарты кодирования, описывающие применяемые способы, а также средства и библиотеки, используемые в проектах. Использование стандартов кодирования позволяет обезличить код, что значительно упрощает его восприятие другими членами команды. Кроме того, стандарты кодирования отражают многолетний опыт вашей команды, позволяя вам создавать настройки эффективнее и качественнее.

В отличие от других доступных на сегодняшний день моделей настройки, SharePoint Framework связана с клиентской разработкой. SharePoint Framework рекомендует использовать TypeScript, который позволяет разработчикам писать более качественный код и находить несоответствия уже в процессе сборки. Для этой же цели предназначены сотни клиентских библиотек. Если ваша команда не впервые выполняет разработку клиентских решений, вероятно, вы уже выбрали подходящую библиотеку. Если нет, советуем изучить информацию о наиболее популярных библиотеках и выбрать одну из них для команды или всей организации (рекомендуется).

Использование одной библиотеки во всех проектах позволяет легче адаптироваться новым членам команды и легче переключаться с одного проекта на другой. Опыт в разработке клиентских решений пригодится вашей организация во всех проектах. Стандартизация проектов по всей организации также сокращает срок выполнения заказов и снижает затраты на обслуживание проектов. Новые библиотеки публикуются в Интернете каждый день, и если постоянно переходить с одной на другую, вы не сможете эффективно работать и создавать качественные решения.

Стандартизация библиотек в организации также поможет оптимизировать работу решений. Так как во всей организации используется одна библиотека, пользователям нужно скачать ее всего один раз, что значительно уменьшает время загрузки решений, повышая удобство использования.

Выбор одной из наиболее популярных библиотек позволяет воспользоваться знаниями и опытом других разработчиков, которые используют эту библиотеку в течение длительного времени и уже решили многие проблемы, которые могут возникнуть у вас самих. Кроме того, для наиболее популярных библиотек доступны стандарты кодирования, что может использовать ваша команда. Используя существующие рыночные стандарты для определенной библиотеки, вашей организации будет проще расширять команду, нанимая разработчиков и помогая им быстрее адаптироваться.

Например, для создания собственных решений на платформе SharePoint корпорация Майкрософт выбрала React. Кроме того, многие другие команды в корпорации Майкрософт, такие как OneDrive или Delve, используют React в своих проектах. Это не значит, что вы также должны использовать React во всех своих проектах SharePoint Framework, но подтверждает, что важно выбрать клиентскую библиотеку, которая подходит для вашей организации. Например, если у вашей команды есть опыт работы с Angular или Knockout, эта платформа может эффективно использоваться при создании решений SharePoint Framework.

### <a name="enforce-coding-standards-and-policies-throughout-the-whole-lifecycle-of-your-solution"></a>Применение стандартов кодирования и правил на протяжении всего жизненного цикла решения

Использование стандартов кодирования дает очевидные преимущества, но одно их наличие не означает, что они активно используются на всех стадиях разработки и тестирования настройки SharePoint. Чем дольше разработчики не могут подтвердить, что решение соответствует стандартам кодирования и правилам организации и чем тяжелее вашей команде это сделать, тем дороже будет исправлять ошибки, найденные в проекте. Ниже описано несколько способов реализации плана управления для решения SharePoint в процессе разработки.

#### <a name="linting"></a>Линтинг

Линтинг — это процедура проверки кода на соответствие определенным правилам. По умолчанию проекты SharePoint Framework создаются с помощью TypeScript. При каждой сборке TSLint (анализатор кода для TypeScript) анализирует проект на соответствие стандартному набору правил и сообщает о несоответствиях. Разработчики могут выбирать активные правила и при необходимости создавать собственные.

Разработчики могут использовать линтинг не только для проверки содержимого файлов TypeScript. Анализаторы кода доступны для наиболее популярных языков, таких как CSS, JavaScript или Markdown, и если у команды есть определенные правила для этих языков, будет полезно реализовать их в анализаторе кода, чтобы они проверялись автоматически каждый раз, когда разработчик выполняет сборку проекта.

#### <a name="automated-testing"></a>Автоматическое тестирование

С помощью автоматических тестов разработчики могут легко убедиться, что после применения последних изменений в проекте все элементы продолжают работать должным образом. Чем старше проект, тем важнее автоматические тесты: чем больше кодовая база, тем больше влияние каждого изменения и риск повреждения других фрагментов кода. Автоматические тесты позволяют разработчикам проверить работу решения и найти все возможные ошибки на ранней стадии.

SharePoint Framework поддерживает средство выполнения тестов [Karma](http://karma-runner.github.io/1.0/index.html) и платформу [Mocha](http://mochajs.org), на которой разработчики могут писать тесты. При необходимости разработчики могут использовать дополнительные элементы, доступные в SharePoint Framework, такие как [PhantomJS](http://phantomjs.org), чтобы расширить сферу действия тестов. Все тесты в проектах SharePoint Framework можно выполнять с помощью стандартной задачи `gulp test`.

#### <a name="code-analysis"></a>Анализ кода

Линтинг помогает проверить синтаксис конкретного файла, но часто разработчикам нужны другие средства для проверки проекта на соответствие правилам в целом. Обычно анализаторы кода делают акцент на коде, но пропускают контекст, представленный файлом кода. В решениях SharePoint Framework у артефактов есть особые требования, например идентификатор веб-части должен быть уникальным в проекте. Кроме того, у организаций могут быть другие требования, например "не ссылаться на сценарии из сеть доставки содержимого" или "использовать только определенную версию определенной библиотеки". Обычно анализаторы кода не могут это проверить, поэтому разработчикам нужны другие средства.

[SharePoint Code Analysis Framework](http://rencore.com/spcaf) (SPCAF) — это стороннее решение, которое разработчики SharePoint, администраторы и сотрудники, ответственные за контроль качества и безопасность, часто используют для проверки настроек SharePoint на соответствие правилам организации. SPCAF интегрируется с процессом управления жизненным циклом приложений, помогая организациям снизить общую стоимость владения настройками SharePoint. SPCAF содержит набор правил, предназначенных специально для решений SharePoint Framework.

## <a name="upgrading-sharepoint-framework-projects"></a>Обновление проектов SharePoint Framework

Развертывание настройки SharePoint в рабочей среде обычно не означает конец ее жизненного цикла. Часто изменение или добавление требований приводит к изменениям в решении. Чтобы правильно обновить настройку, развернутую в рабочей среде, необходимо учитывать несколько факторов.

### <a name="semantic-versioning-semver"></a>Семантическое версионирование (SemVer)

За редким исключением, SharePoint Framework использует семантическое версионирование (SemVer) для отслеживания номеров версий. Семантическое версионирование — это модель версионирования, которая широко применяется разработчиками программного обеспечения по всему миру. Номер SemVer состоит из трех цифр ОСНОВНОЙ.ДОПОЛНИТЕЛЬНЫЙ.ИСПРАВЛЕНИЕ и необязательных меток, например 1.0.1.

> Примечание. В настоящее время в SharePoint Frameworks можно использовать только три цифры без меток.

Различные части номера SemVer увеличиваются в зависимости от того, как изменяется решение:

- ОСНОВНОЙ, если изменения не совместимы с предыдущими версиями.
- ДОПОЛНИТЕЛЬНЫЙ, если добавлены функции, совместимые с предыдущими версиями.
- ИСПРАВЛЕНИЕ, если исправлены ошибки (изменения совместимы с предыдущими версиями).

Важно помнить, что семантическое версионирование — это всего лишь соглашение. Ваша команда может следовать ему, сообщая об изменениях в последнем выпуске.

Узнать больше о семантическом версионировании можно на сайте [http://semver.org](http://semver.org).

### <a name="increase-version-number"></a>Увеличение номера версии

При обновлении решения SharePoint Framework разработчики должны увеличить номера версий изменившихся элементов, чтобы четко указать, какие элементы изменились и каковы последствия.

#### <a name="increase-package-version-in-packagejson"></a>Увеличение версии пакета в файле package.json

Пакет SharePoint Framework имеет такую же структуру, как пакет Node.js. Его зависимости и метаданные хранятся в файле **package.json** в папке проекта. Одно из свойств в файле **package.json** определяет версию всего проекта. Хотя оно имеет сугубо информационный характер и не используется развернутыми артефактами, разработчики должны увеличивать номер версии в файле **package.json** каждый раз, когда планируется новый выпуск проекта, по схеме SemVer.

#### <a name="increase-solution-package-version-in-package-solutionjson"></a>Увеличение версии пакета решения в файле package-solution.json

Решения SharePoint Framework развертываются с помощью файла **.spapp**, установленного в каталоге приложений на клиенте SharePoint. Файл **.spapp** похож на пакет надстройки SharePoint, и номера его версий увеличиваются по той же схеме. Текущая версия пакета **.spapp** определяется с помощью четырехкомпонентного номера (ОСНОВНОЙ.ДОПОЛНИТЕЛЬНЫЙ.ИСПРАВЛЕНИЕ.СБОРКА), который хранится в файле **config/package-solution.json**. Для простоты разработчикам следует синхронизировать этот номер с номером версии в файле **package.json**, так как оба номера относятся к версии проекта в целом.

> Примечание. Увеличение номера версии в файле package-solution.json между выпусками необходимо для правильного развертывания новой версии пакета в SharePoint.

#### <a name="increase-web-part-version-in-the-web-part-manifest"></a>Увеличение версии веб-части в манифесте веб-части

Каждая клиентская веб-часть, созданная на основе SharePoint Framework, содержит манифест, который содержит сведения об этой веб-части, такие как название, значок, свойства и расположение пакета кода. В манифесте, в свойстве **version**, также хранится номер версии веб-части. Свойство **version** состоит из трех цифр без метки согласно схеме SemVer. Манифест веб-части входит в состав пакета **.spapp**, который развертывается в SharePoint.

При обновлении веб-части разработчики должны изменить номер версии в соответствии с объемом внесенных изменения. Если определенная веб-часть в проекте не изменилась с предыдущего выпуска, номер ее версии менять не нужно.

### <a name="update-dependencies"></a>Обновление зависимостей

Проект SharePoint Framework может обновляться из-за изменения одной из базовых зависимостей, например выпуска новой версии Angular, в которой исправлены ошибки и повышена производительность. Если ваша команда использует npm shrinkwrap для блокировки версий зависимостей, используйте команду `npm install <package>@<version> --save`, чтобы обновить зависимость от определенной версии и проверить работу проекта. В зависимости от того, как изменения базовых зависимостей влияют на проект, обновление проекта может быть как исправлением, так и основным выпуском.

### <a name="build-and-package-project-in-release-mode"></a>Сборка и упаковка проекта в режиме выпуска

После проверки работы решения выполните сборку проекта в режиме выпуска с помощью команды `gulp bundle --ship`. После этого создайте новый пакет с помощью команды `gulp package-solution --ship`. Если не выполнена команда `gulp bundle --ship`, пакет будет содержать предыдущую версию проекта.

### <a name="deploy-new-version-of-your-solution"></a>Развертывание новой версии решения

После сборки и упаковки проекта нужно его развернуть. Сначала разверните обновленные пакеты веб-части, расположенные в проекте в папке **./temp/deploy**. Опубликуйте файлы рядом с пакетами предыдущей версии решения.

> Примечание. Не удаляйте предыдущие версии решения, пока их используют активные экземпляры веб-частей. Каждая версия пакетов имеет уникальное имя, и удаление предыдущих версий до обновления веб-частей нарушит работу этих веб-частей.

После этого разверните новый пакет решения в каталоге приложений SharePoint. Это необходимо, чтобы сообщить SharePoint о новой версии решения, которую он должен применить.