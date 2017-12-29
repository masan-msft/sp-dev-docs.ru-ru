---
title: "Обновление пакетов SharePoint Framework"
ms.date: 11/29/2017
ms.prod: sharepoint
ms.openlocfilehash: 665c22ffea27a8b62d433cfb4932625664638e0a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="update-sharepoint-framework-packages"></a>Обновление пакетов SharePoint Framework

Средства клиентской разработки для SharePoint управляют зависимостями и другими необходимыми вспомогательными элементами JavaScript с помощью диспетчера пакетов [npm](https://www.npmjs.com/). Этот диспетчер обычно устанавливается вместе с Node.js.

При создании нового клиентского решения генератор Yeoman для SharePoint получает последние версии необходимых для проекта пакетов SharePoint Framework. По мере работы над проектом пакеты могут устаревать. Изучив [заметки о выпуске](https://aka.ms/spfx-release-notes), касающиеся определенного выпуска или последней версии пакета, вы можете решить обновить пакеты SharePoint Framework, используемые в проекте. Пакеты SharePoint Framework включают установленные в проекте пакеты npm, например [@microsoft/sp-core-library](https://www.npmjs.com/package/@microsoft/sp-core-library), и глобально установленные пакеты npm, например [@microsoft/generator-sharepoint](https://www.npmjs.com/package/@microsoft/generator-sharepoint). 

> [!TIP]
> Рекомендуем время от времени обновлять пакеты SharePoint Framework, чтобы получать доступ к последним изменениям и исправлениям.

## <a name="find-outdated-packages-in-your-project"></a>Поиск устаревших пакетов в проекте

Чтобы найти устаревшие пакеты, в том числе пакеты SharePoint Framework и другие пакеты, от которых зависит проект, перейдите в каталог проекта и выполните в нем следующую команду. 

```sh
npm outdated
```

На основе файла `package.json`, расположенного в корневом каталоге проекта, и реестра npm будут выведены следующие сведения о пакетах:

* версия, установленная в проекте;
* версия, запрашиваемая проектом (указана в файле `package.json`);
* последняя доступная версия.

![Устаревшие пакеты NPM](../../images/npm-outdated-packages-list.png)

Имена пакетов SharePoint Framework начинаются с такого идентификатора области npm и префикса:

```text
@microsoft/sp-
```

Помимо пакетов Framework вам также может понадобиться обновить пакеты `react` и `office-ui-fabric-react`. Обязательно ознакомьтесь с [заметками о конкретном выпуске](https://aka.ms/spfx-release-notes), чтобы определить, какие пакеты нужно обновить, и запланируйте обновление.

### <a name="using-npm-outdated-with-project-targeting-sharepoint-2016"></a>Использование npm предыдущей версии в проекте для SharePoint 2016

Начиная с пакета дополнительных компонентов 2, SharePoint 2016 поддерживает решения SharePoint Framework. SharePoint 2016 использует версию SharePoint Framework, выпущенную раньше той, которая доступна в SharePoint Online. При скаффолдинге новых проектов генератор Yeoman для SharePoint Framework предложит указать, какую версию должно использовать решение. Если оно будет использовать последнюю версию SharePoint Framework, оно будет работать только в SharePoint Online, если более старую — оно будет работать в SharePoint 2016 и SharePoint Online.

Когда вы выполните команду `npm outdated` в проекте для SharePoint Online и SharePoint 2016, отобразятся последние версии пакетов SharePoint Framework. Эти версии работают только в SharePoint Online. Если вы обновите свое решение так, чтобы оно использовало эти последние пакеты, оно перестанет работать в SharePoint 2016.

Работая с решениями SharePoint Framework, совместимыми с локальной средой SharePoint, всегда проверяйте, какой уровень исправления у целевой фермы SharePoint и какую версию SharePoint Framework она поддерживает.

### <a name="update-packages"></a>Обновление пакетов

При обновлении версий пакетов всегда используйте диспетчер пакетов (npm или Yarn). Не следует редактировать файл `package.json` вручную. Если вы будете следовать рекомендациям по использованию файла блокировки, изменения, внесенные в файл `package.json`, будут проигнорированы.

Начните с определения того, какие пакеты нужно обновить и какие новые версии хотите использовать. Обратите внимание на то, что не всегда возможно использовать последнюю версию определенного пакета, так как она может быть несовместима с другими зависимостями SharePoint Framework, такими как TypeScript.

Для каждого пакета, который нужно обновить, выполните следующую команду:

```sh
npm install mypackage@newversion --save
```

Например, если вы используете AngularJS версии 1.5.9 и хотите выполнить обновление до версии 1.6.5, нужно выполнить такую команду:

```sh
npm install angular@1.6.5 --save
```

При обновлении пакета с помощью npm установится указанная версия пакета в проекте, а также обновится номер версии в зависимостях файла package.json и файл блокировки, используемый в проекте.

После установки пакетов выполните следующую команду, чтобы очистить артефакты старой сборки:

```sh
gulp clean
```

### <a name="update-your-code"></a>Обновление кода

В зависимости от того, насколько существенно изменен API, может потребоваться обновить существующий код и файлы конфигурации проекта. О существенных изменениях и модификациях, которые нужно внести в существующий код, можно узнать из [заметок о выпуске](https://aka.ms/spfx-release-notes). Внесите необходимые исправления в код.

Вы всегда можете выполнить сборку проекта, чтобы посмотреть, есть ли ошибки и предупреждения, выполнив команду в консоли в каталоге проекта:

```sh
gulp build
```

## <a name="update-yeoman-generator-for-sharepoint"></a>Обновление генератора Yeoman для SharePoint

Если вы установили генератор Yeoman для SharePoint Framework глобально, вы можете проверить, нужно ли его обновлять, выполнив следующую команду:

```sh
npm outdated -g
```

На основе версий, установленных на компьютере, и реестра npm будут выведены следующие сведения о глобально установленных на компьютере пакетах:

* текущая версия, глобально установленная на компьютере;
* версия, которую вы запросили при установке;
* последняя доступная версия.

![Устаревшие глобальные пакеты NPM](../../images/npm-outdated-global-packages-list.png)

Имя пакета генератора выглядит следующим образом:

```sh
@microsoft/generator-sharepoint
```

### <a name="update-generator-package"></a>Обновление пакета генератора

Чтобы обновить генератор до последней опубликованной версии, откройте любую консоль и выполните следующую команду:

```sh
npm install @microsoft/generator-sharepoint@latest -g
```

Команда обновит генератор Yeoman для SharePoint и его зависимости до последней опубликованной версии. Для проверки выполните в консоли следующую команду:

```sh
npm ls @microsoft/generator-sharepoint -g --depth=0
```

## <a name="see-also"></a>См. также

* [Обновление проектов SharePoint Framework (руководство для команды разработчиков)](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/team-based-development-on-sharepoint-framework#upgrading-sharepoint-framework-projects)
* [Обновление элементов SharePoint (Подготовка ресурсов SharePoint)](https://docs.microsoft.com/ru-RU/sharepoint/dev/spfx/toolchain/provision-sharepoint-assets#upgrade-sharepoint-items)