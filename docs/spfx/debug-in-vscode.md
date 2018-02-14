---
title: "Отладка решений SharePoint Framework в Visual Studio Code"
description: "Требования и инструкции по настройке Visual Studio Code для отладки решений SharePoint Framework."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 3e5687a6fe0a617d5eeb999ff00e376f948cb177
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="debug-sharepoint-framework-solutions-in-visual-studio-code"></a>Отладка решений SharePoint Framework в Visual Studio Code

Visual Studio Code — это популярный редактор кода, часто используемый для создания решений SharePoint Framework. Настроив отладку решения SharePoint Framework в Visual Studio Code, вы можете эффективнее пошагово выполнять код и исправлять ошибки. 

Шаги по включению отладки в Visual Studio Code также приведены в видео [на канале SharePoint PnP на YouTube](https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG). 

<a href="https://www.youtube.com/watch?v=oNChcluMrm8&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/spfx-debug-youtube.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="prerequisites"></a>Предварительные условия

Настроить Visual Studio Code для отладки решений SharePoint Framework проще всего с помощью Google Chrome и расширения Debugger for Chrome. Начиная с генератора Yeoman для SharePoint Framework версии 1.3.4, шаблоны проекта (веб-частей и расширений) по умолчанию поставляются с предварительно установленными необходимыми компонентами и требуют установку нужных расширений Visual Studio Code. В этом случае вам будет предложено установить отладчик для расширения Visual Studio Code для Chrome.

Также понадобится браузер Google Chrome. [Скачайте и установите последнюю версию Google Chrome](https://www.google.com/chrome/browser/desktop/index.html).

Если вы используете генератор Yeoman для SharePoint Framework более старой версии, чем 1.3.4, то можете [установить расширение отладчика для Chrome для Visual Studio Code из магазина Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome).

## <a name="debug-configurations"></a>Конфигурации отладки

Конфигурация отладки находится в файле launch.json в папке рабочей области Visual Studio Code:

```
project-name\.vscode
```

Launch.json содержит две конфигурации отладки:
* Конфигурация локальной рабочей области
* Конфигурация размещенной рабочей области

## <a name="debug-solution-using-local-workbench"></a>Отладка решения с помощью локальной рабочей области

Вы можете использовать локальную рабочую область, чтобы проверить, корректно ли работает веб-часть. Локальная рабочая область хорошо подходит для тестирования всех сценариев, не требующих связи с SharePoint, а также для автономной разработки.

Настроив Visual Studio Code для отладки решений SharePoint Framework с помощью Google Chrome и локальной рабочей области, вы можете проверить, правильно ли все работает.

### <a name="configure-a-breakpoint"></a>Настройка точки останова

1. В Visual Studio Code откройте основной исходный файл веб-части и добавьте точку останова в первой строке метода **render**. Для этого выберите поле слева от номера строки или выделите строку кода в редакторе и нажмите клавишу F9.

    ![Точка останова в клиентской веб-части SharePoint Framework в Visual Studio Code](../images/vscode-debugging-breakpoint-configured.png)

2. В Visual Studio Code откройте меню **Вид** и выберите пункт **Интегрированный терминал** или нажмите клавиши **CTRL+`**. 

3. В терминале выполните следующую команду:

    ```sh
    gulp serve --nobrowser
    ```

    При этом будет выполнена сборка решения SharePoint Framework и запустится локальный веб-сервер для предоставления выходных файлов. Так как отладчик запускает собственный экземпляр браузера, мы используем аргумент **--nobrowser**, чтобы задача **serve** не открывала окно браузера.

    ![Команда gulp serve в интегрированном терминале Visual Studio Code](../images/vscode-debugging-gulp-serve.png)

### <a name="start-debugging-in-visual-studio-code"></a>Начало отладки с помощью Visual Studio Code

Когда задача gulp будет выполнена, переместите курсор в область кода Visual Studio Code и нажмите клавишу F5 (или выберите в меню **Отладка** пункт **Запустить отладку**). 

Будет запущен режим отладки Visual Studio Code: цвет строки состояния изменится на оранжевый, а также откроется новое окно Google Chrome с локальной версией рабочей области SharePoint.

> [!NOTE] 
> В этот момент точка останова отключена, так как код веб-части еще не загружен. SharePoint Framework загружает веб-части по запросу только после их добавления на страницу.

![Visual Studio Code в режиме отладки рядом с браузером Google Chrome, в котором отображается локальная версия рабочей области SharePoint](../images/vscode-debugging-chrome-started.png)


### <a name="add-a-web-part-to-the-canvas"></a>Добавление веб-части на холст

Чтобы убедиться, что отладка работает, добавьте веб-часть на холст в рабочей области.

![Панель элементов веб-части в рабочей области SharePoint](../images/vscode-debugging-adding-web-part-to-canvas.png)

<br/>

Обратите внимание, что после загрузки кода на страницу индикатор точки останова изменился на активный.

![Активная точка останова после добавления веб-части на холст](../images/vscode-debugging-breakpoint-active.png)

<br/>

Если теперь обновить страницу, в Visual Studio Code будет достигнута точка останова, и вы сможете проверить все свойства и пошагово выполнить код.

![Достигнутая точка останова в Visual Studio Code](../images/vscode-debugging-breakpoint-hit.png)

## <a name="debug-solution-using-hosted-workbench"></a>Отладка решения с помощью размещенной рабочей области

Чтобы проверить взаимодействие решения с SharePoint, можно использовать размещенную версию рабочей области SharePoint, доступную в каждом клиенте Office 365 по адресу `https://yourtenant.sharepoint.com/_layouts/workbench.aspx`. 

При создании решений SharePoint Framework вы будете регулярно выполнять такие проверки, поэтому рекомендуем создать отдельную конфигурацию отладки для размещенной версии рабочей области SharePoint.

### <a name="debug-solution-using-hosted-workbench"></a>Отладка решения с помощью размещенной рабочей области

1. Откройте файл launch.json и измените свойство `url` в конфигурации *размещенной рабочей области* на URL-адрес вашего сайта SharePoint.

    ```json
    "url": "https://enter-your-SharePoint-site/_layouts/workbench.aspx",
    ```

2. В Visual Studio Code откройте панель **Отладка** и в списке **Конфигурации** выберите новую конфигурацию **Размещенная рабочая область**.

    ![Конфигурация размещенной рабочей области, выбранная в раскрывающемся списке конфигураций отладки в Visual Studio Code](../images/vscode-debugging-debugging-hosted-workbench.png)

3. Запустите отладку, нажав клавишу F5 или выбрав в меню **Отладка** пункт **Запустить отладку**. Visual Studio Code переключится в режим отладки (это будет видно по оранжевой строке состояния), а расширение Debugger for Chrome откроет новое окно Google Chrome со страницей входа в Office 365.

    ![Страница входа в Office 365, открытая в Google Chrome после запуска отладки в размещенной рабочей области](../images/vscode-debugging-o365-login.png)

4. После входа добавьте веб-часть на холст и обновите рабочую область, как и в случае с локальной рабочей областью. В Visual Studio Code будет достигнута точка останова, а вы сможете проверить переменные и пошагово выполнить код.

    ![Достигнута точка останова в Visual Studio Code при отладке клиентской веб-части SharePoint Framework в размещенной рабочей области](../images/vscode-debugging-breakpoint-hit-o365.png)

## <a name="for-older-projects"></a>Для более ранних проектов

Если вы используете более раннюю версию генератора Yeoman для SharePoint Framework, следуйте инструкциям ниже, чтобы создать файл launch.json вручную.

### <a name="create-debug-configuration-for-local-workbench"></a>Создание конфигурации отладки для локальной рабочей области

1. Откройте в Visual Studio Code панель **Отладка**.

    ![Панель отладки в Visual Studio Code](../images/vscode-debugging-vscode-debug.png)

2. В верхней части панели откройте список **Конфигурации** и выберите пункт **Добавить конфигурацию**.

    ![Пункт "Добавить конфигурацию" в раскрывающемся списке конфигураций отладки](../images/vscode-debugging-add-debug-configuration.png)

3. Выберите **Chrome** в списке сред отладки.

    ![Браузер Chrome выбран в качестве среды отладки для новой конфигурации](../images/vscode-debugging-chrome-debug-environment.png)

4. Замените содержимое созданного файла **launch.json** на следующее:

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Local workbench",
                "type": "chrome",
                "request": "launch",
                "url": "https://localhost:4321/temp/workbench.html",
                "webRoot": "${workspaceRoot}",
                "sourceMaps": true,
                "sourceMapPathOverrides": {
                    "webpack:///../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../../src/*": "${webRoot}/src/*"
                },
                "runtimeArgs": [
                    "--remote-debugging-port=9222"
                ]
            }
        ]
    }
    ```

    В этой конфигурации используется отладчик **Chrome**, который входит в состав расширения **Debugger for Chrome**. Он указывает на URL-адрес локальной рабочей области в качестве отправной точки. При отладке кода TypeScript важна конфигурация, с помощью которой отладчик сопоставляет код JavaScript, выполняемый в браузере, с исходным кодом TypeScript.

### <a name="create-debug-configuration-for-hosted-workbench"></a>Создание конфигурации отладки для размещенной рабочей области

1. В Visual Studio Code откройте файл **./.vscode/launch.json**. 

2. Скопируйте имеющуюся конфигурацию отладки и укажите URL-адрес размещенной рабочей области:

    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "Local workbench",
                "type": "chrome",
                "request": "launch",
                "url": "https://localhost:4321/temp/workbench.html",
                "webRoot": "${workspaceRoot}",
                "sourceMaps": true,
                "sourceMapPathOverrides": {
                    "webpack:///../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../../src/*": "${webRoot}/src/*"
                },
                "runtimeArgs": [
                    "--remote-debugging-port=9222"
                ]
            },
            {
                "name": "Hosted workbench",
                "type": "chrome",
                "request": "launch",
                "url": "https://contoso.sharepoint.com/_layouts/workbench.aspx",
                "webRoot": "${workspaceRoot}",
                "sourceMaps": true,
                "sourceMapPathOverrides": {
                    "webpack:///../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../src/*": "${webRoot}/src/*",
                    "webpack:///../../../../../src/*": "${webRoot}/src/*"
                },
                "runtimeArgs": [
                    "--remote-debugging-port=9222"
                ]
            }
        ]
    }
    ```

## <a name="see-also"></a>См. также

- [Отладка веб-части SharePoint Framework (Элио Струйф)](https://www.eliostruyf.com/how-to-debug-your-sharepoint-framework-web-part/)
- [Отладка веб-части SPFx React с помощью Visual Studio Code (Велин Георгиев)](https://blog.velingeorgiev.com/how-debug-sharepoint-framework-webpart-visual-studio-code)
- [Скаффолдинг проектов с помощью генератора Yeoman для SharePoint](toolchain/scaffolding-projects-using-yeoman-sharepoint-generator.md)
- [Обзор SharePoint Framework](sharepoint-framework-overview.md)
