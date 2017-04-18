# <a name="scaffold-projects-using-yeoman-sharepoint-generator"></a>Скаффолдинг проектов с помощью генератора yeoman для SharePoint

[Yeoman](http://yeoman.io/) помогает эффективно запускать новые проекты благодаря соответствующим рекомендациям и инструментам. С помощью генератора yeoman для SharePoint разработчики могут инициализировать проекты, чтобы создавать, упаковывать и развертывать решения SharePoint. Генератор предоставляет стандартные инструменты сборки, стереотипный код и стандартный веб-сайт для тестирования веб-частей.

## <a name="installing-the-yeoman-sharepoint-generator"></a>Установка генератора yeoman для SharePoint

Генератор yeoman для SharePoint доступен в составе платформы как [пакет npm](https://www.npmjs.com/package/@microsoft/generator-sharepoint). Чтобы установить генератор, выполните следующую команду в консоли:

```
npm install @microsoft/generator-sharepoint -g
```

>**Примечание.** Генератор yeoman для SharePoint должен развертываться глобально с первой общедоступной версией. Существуют известные проблемы при локальной установке в проекте, которые планируется устранить после выпуска общедоступной версии.

Рекомендуем воспользоваться [этими инструкциями](../spfx/set-up-your-development-environment.md), чтобы установить на компьютер полный набор инструментов разработчика, в том числе генератор yeoman для SharePoint. 

## <a name="using-the-yeoman-sharepoint-generator"></a>Использование генератора yeoman для SharePoint

Чтобы вызвать генератор после установки, просто введите следующую команду в консоли:

```
yo
```

Появится список всех генераторов, доступных на вашем компьютере. Выберите `@microsoft/sharepoint`, чтобы вызвать генератор SharePoint и следуйте инструкциям, чтобы создать клиентское решение:

![Генератор yeoman для SharePoint](../../images/yeoman-sp-generator.png)

## <a name="available-command-line-options-for-the-generator"></a>Доступные параметры командной строки для генератора

Вы можете использовать параметры командной строки, доступные для генератора SharePoint, чтобы не следовать инструкциям, а инициализировать проекты с помощью одной команды. Выполните следующую команду, чтобы просмотреть список параметров командной строки, доступных для генератора SharePoint:

```
yo @microsoft/generator-sharepoint --help
```

![параметры командной строки для генератора SharePoint](../../images/yeoman-sp-cmdline-options.png)

Параметр | Описание 
-----|------
--skip-install|Не устанавливать зависимости автоматически.
--solutionName|Имя клиентского решения, а также имя папки.
--framework|Платформа, которую необходимо использовать для решения: "none", "react" или "knockout".
--componentType|Тип компонента. В настоящее время поддерживается только "webpart".
--componentName|Имя компонента.
--componentDescription|Описание компонента.

Ниже приведен пример команды, которая создает решение "hello-world" с веб-частью "HelloWorld" на платформе "react":

```
yo @microsoft/sharepoint --solutionName "hello-world" --framework "react" --componentType "webpart" --componentName "HelloWorld" --componentDescription "HelloWorld web part"
```

### <a name="notes-on---skip-install"></a>Примечания по --skip-install 

Команда `--skip-install` позволяет инициализировать проект, не устанавливая зависимости. Для успешной сборки проекта вам потребуется установить зависимости позже после скаффолдинга проекта. 

При сборке проекта без установки зависимостей возникнет следующая ошибка. Она означает, что вам нужно установить зависимости перед сборкой проекта:

```
Local gulp not found in ~/<project-name>
Try running: npm install gulp
```

Вы можете выполнить следующую команду, чтобы установить зависимости:

```
npm install
```
