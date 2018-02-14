---
title: "Формирование шаблонов проектов с помощью генератора Yeoman для SharePoint"
description: "Генератор Yeoman для SharePoint позволяет формировать шаблоны новых проектов клиентских решений, чтобы создавать, упаковывать и развертывать решения SharePoint."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: ac69ce5030289fefce1563fb03b6b0fb1466d470
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="scaffold-projects-by-using-yeoman-sharepoint-generator"></a>Формирование шаблонов проектов с помощью генератора Yeoman для SharePoint

[Yeoman](http://yeoman.io/) помогает эффективно запускать новые проекты благодаря соответствующим рекомендациям и инструментам. С помощью генератора Yeoman для SharePoint разработчики могут формировать шаблоны новых проектов клиентских решений, чтобы создавать, упаковывать и развертывать решения SharePoint. Генератор предоставляет стандартные инструменты сборки, а также стандартные код и веб-сайт для тестирования веб-частей.

## <a name="install-the-yeoman-sharepoint-generator"></a>Установка генератора Yeoman для SharePoint

Генератор Yeoman для SharePoint доступен в составе платформы как [пакет npm](https://www.npmjs.com/package/@microsoft/generator-sharepoint). Чтобы установить генератор, выполните следующую команду в консоли:

```
npm install @microsoft/generator-sharepoint -g
```

> [!NOTE] 
> Генератор Yeoman для SharePoint должен развертываться глобально с первой общедоступной версией. При его локальной установке в проекте могут возникать определенные проблемы, которые будут устранены в одной из следующих версий.

Рекомендуем воспользоваться [этими инструкциями по настройке](../set-up-your-development-environment.md), чтобы установить на компьютер полный набор инструментов разработчика, в том числе генератор Yeoman для SharePoint. 

## <a name="use-the-yeoman-sharepoint-generator"></a>Использование генератора Yeoman для SharePoint

Чтобы вызвать генератор после установки, просто введите в консоли следующую команду:

```
yo
```

Появится список всех генераторов, доступных на вашем компьютере. Выберите `@microsoft/sharepoint`, чтобы вызвать генератор SharePoint, и следуйте инструкциям, чтобы создать клиентское решение:

![Генератор Yeoman для SharePoint](../../images/yeoman-sp-generator.png)


## <a name="use-available-command-line-options-for-the-generator"></a>Использование доступных параметров командной строки для генератора

Параметры командной строки, доступные генератору Yeoman для SharePoint, позволяют не следовать отображаемым на экране инструкциям, а формировать шаблоны проектов с помощью одной команды. Выполните следующую команду, чтобы просмотреть список параметров командной строки, доступных генератору Yeoman для SharePoint:

```
yo @microsoft/generator-sharepoint --help
```

<br/>

![Параметры командной строки, доступные генератору Yeoman для SharePoint](../../images/yeoman-sp-cmdline-options.png)

<br/>

**Параметры командной строки**

Параметр | Описание 
-----|------
--help|Печать сведений об использовании генератора и его параметров.
--skip-cache|Ответы на запросы не сохраняются. По умолчанию: *false*.
--skip-install|Зависимости не устанавливаются автоматически. По умолчанию: *false*.
--componentType|Тип компонента. Сейчас поддерживаются WebPart и Extension (то есть веб-часть и расширение).
--componentDescription|Описание компонента.
--componentName|Имя компонента.
--framework|Платформа, которую необходимо использовать для решения: React, Knockout или платформа, отличная от JavaScript.
--extensionType|Тип расширения. Сейчас поддерживаются ApplicationCustomizer, FieldCustomizer, ListViewCommandSet.
--solutionName|Имя клиентского решения, а также имя папки.
--environment|Целевая среда для решения: локальная (onprem) или SharePoint Online (spo).

<br/>

**Доступные аргументы**

Аргумент | Описание | Тип | Обязательный |
-- | -- | -- | -- |
skipFeatureDeployment | Если указан, позволяет администратору клиента сделать так, что развертывание компонентов на всех сайтах будет выполнено сразу. В этом случае администратору не нужно будет запускать развертывание компонентов и добавлять приложения на сайтах. | Boolean | false | 

<br/>

Ниже приведен пример команды, которая создает решение hello-world со следующими параметрами:
- включает веб-часть HelloWorld; 
- используется платформа React, предназначенная только для SharePoint Online; 
- предусмотрена возможность развертывания на уровне клиента.

Обратите внимание на то, что некоторые параметры связаны зависимостями. Например, невозможно создать расширение с параметром локальной среды.

```
yo @microsoft/sharepoint 
--solutionName "hello-world" 
--framework "react" 
--componentType "webpart" 
--componentName "HelloWorld" 
--componentDescription "HelloWorld web part" 
--skip-install 
--environment "spo" skipFeatureDeployment true
```

<br/>

> [!NOTE]
> Команда `--skip-install` позволяет сформировать шаблоны проекта, не устанавливая зависимости. Для успешной сборки проекта вам потребуется установить зависимости позже, после формирования шаблонов проекта. 

> Если вы попытаетесь выполнить сборку проекта без установки зависимостей, возникнет указанная ниже ошибка. Она означает, что вам нужно установить зависимости перед сборкой проекта.

> ```
> Local gulp not found in ~/<project-name>
> Try running: npm install gulp
> ```

> Вы можете выполнить следующую команду, чтобы установить зависимости:

> ```
> npm install
> ```


## <a name="see-also"></a>См. также

- [Цепочка инструментов SharePoint Framework](sharepoint-framework-toolchain.md)
- [Средства разработки и библиотеки платформы SharePoint Framework](../tools-and-libraries.md)
- [Обзор SharePoint Framework](../sharepoint-framework-overview.md)
