---
title: "Размещение расширения из сети доставки содержимого Office 365 (Hello World, часть 4)"
description: "Разверните настройщик заполнителей SharePoint Framework в сети доставки содержимого Office 365, а затем разверните его в SharePoint для конечных пользователей."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: 998b8ae5688bfbccddb6811e4b0460625204a63d
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="host-extension-from-office-365-cdn-hello-world-part-4"></a>Размещение расширения в сети доставки содержимого Office 365 (Hello World, часть 4)

В этой статье объясняется, как развернуть настройщик заполнителей SharePoint Framework для размещения в сети доставки содержимого Office 365 и как развернуть его в SharePoint для конечных пользователей. 

Перед началом работы необходимо выполнить процедуры, описанные в следующих статьях:

* [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./build-a-hello-world-extension.md)
* [Использование заполнителей страниц из настройщика заполнителей (Hello World, часть 2)](./using-page-placeholder-with-extensions.md)
* [Развертывание расширения в SharePoint (Hello World, часть 3)](./serving-your-extension-from-sharepoint.md)

Эти действия также показаны в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=oOIHWamPr34&list=PLR9nK3mnD-OXtWO5AIIr7nCR3sWutACpV). 

<a href="https://www.youtube.com/watch?v=nh1qFArXG2Y">
<img src="../../../images/spfx-ext-youtube-tutorial4.png" alt="Screenshot of the YouTube video player for this tutorial" />
</a>

## <a name="enable-the-cdn-in-your-office-365-tenant"></a>Использование CDN в клиенте Office 365

Сеть доставки содержимого Office 365 — самый простой способ размещать решения SharePoint непосредственно из их клиента, пользуясь при этом преимуществами службы сетей доставки содержимого (CDN) для сокращения времени загрузки ресурсов.

1. Скачайте [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588), чтобы убедиться, что у вас установлена последняя версия.

2. Подключитесь к клиенту SharePoint Online с помощью PowerShell:
    
    ```powershell
    Connect-SPOService -Url https://contoso-admin.sharepoint.com
    ```
    
3. Чтобы узнать текущее состояние настроек общедоступной сети CDN для клиента, поочередно выполните указанные ниже команды. 
    
    ```powershell
    Get-SPOTenantCdnEnabled -CdnType Public
    Get-SPOTenantCdnOrigins -CdnType Public
    Get-SPOTenantCdnPolicies -CdnType Public
    ```
    
4. Включите общедоступную сеть доставки содержимого в клиенте:
    
    ```powershell
    Set-SPOTenantCdnEnabled -CdnType Public
    ```
    
    Теперь в клиенте включена общедоступная сеть доставки содержимого с использованием разрешенной конфигурации типов файлов по умолчанию. Это означает, что поддерживаются такие расширения: CSS, EOT, CSS, EOT, GIF, ICO, JPEG, JPG, JS, MAP, PNG, SVG, TTF и WOFF.

5. Откройте браузер и перейдите к семейству веб-сайтов, в котором вы хотите разместить свою библиотеку CDN. Это может быть любое семейство веб-сайтов в клиенте. Это руководство описывает создание библиотеки CDN, но вы также можете использовать отдельную папку в любой существующей библиотеке документов как конечную точку CDN.

6. В семействе веб-сайтов создайте библиотеку документов **CDN** и добавьте в нее папку **helloworld**.
    
    ![Папка helloworld-extension в библиотеке CDN](../../../images/ext-app-cdn-folder-created.png) 
    
    <br/>
    
7. В консоли PowerShell добавьте новый источник сети доставки содержимого. В этом случае мы задаем источник `*/cdn`, то есть в качестве источника сети доставки содержимого будет выступать любая относительная папка с именем **cdn**.
    
    ```powershell
    Add-SPOTenantCdnOrigin -CdnType Public -OriginUrl */cdn
    ```
    
8. Выполните указанную ниже команду, чтобы получить список источников сети доставки содержимого клиента:
    
    ```powershell
    Get-SPOTenantCdnOrigins -CdnType Public
    ```
    
    Обратите внимание, что новый источник указан как допустимый источник CDN. Окончательная настройка источника занимает приблизительно 15 минут, поэтому мы можем продолжить создавать расширение, которое будет размещено в источнике после развертывания. 

    ![Список общедоступных источников в клиенте](../../../images/ext-app-cdn-origins-pending.png)

    Если рядом с названием источника нет уведомления `(configuration pending)`, он готов к использованию в клиенте. Это указывает на выполняющуюся настройку SharePoint Online и системы CDN. 

## <a name="update-your-solution-project-for-the-cdn-urls"></a>Обновление проекта решения для URL-адресов CDN

1. Вернитесь к ранее созданному решению, чтобы изменить URL-адреса.
    
2. Обновите файл **write-manifestests.json** (в папке **config**), как показано ниже, чтобы он указывал на конечную точку CDN. Используйте `publiccdn.sharepointonline.com` в качестве префикса, а затем дополните URL-адрес фактическим путем к вашему клиенту. Формат URL-адреса для сети доставки содержимого:
    
    ```json
    https://publiccdn.sharepointonline.com/<tenant host name>/sites/site/library/folder
    ```
    
    ![Путь к конечной точке CDN в манифесте записи](../../../images/ext-app-cdn-write-manifest.png)

3. Сохраните изменения.

4. Выполните приведенные ниже задачи для упаковки решения. При этом будет выполнена сборка конечной версии проекта с использованием URL-адреса сети доставки содержимого, указанного в файле **writer-manifest.json**. Результат будет помещен в папку **./temp/deploy**. Эти файлы вам нужно будет добавить в папку SharePoint, представляющую собой конечную точку CDN. 
    
    ```
    gulp bundle --ship
    ```
    
5. Выполните указанную ниже команду, чтобы упаковать решение. Эта команда создает пакет **app-extension.sppkg** в папке **sharepoint/solution** и подготавливает ресурсы в папке **temp/deploy** к развертыванию в CDN.
    
    ```
    gulp package-solution --ship
    ```
    
6. Добавьте или перетащите новый пакет клиентского решения в каталог приложений в клиенте и нажмите кнопку **Развернуть**.

    ![Диалоговое окно подтверждения доверия в каталоге приложений со ссылкой на конечную точку CDN](../../../images/ext-app-approve-cdn-address.png)

7. Отправьте или перетащите файлы из папки **temp/deploy** в созданную ранее папку **CDN/helloworld**.

8. Установите новую версию решения на сайте и убедитесь, что она работает без файла JavaScript в домене *locahost*.

    ![Пользовательские верхний и нижний колонтитулы на странице](../../../images/ext-app-header-footer-visible.png)

<br/>

Поздравляем! Вы включили общедоступную сеть CDN в клиенте Office 365 и воспользовались ею в решении!

> [!NOTE]
> Если вы обнаружили ошибку в документации или SharePoint Framework, сообщите о ней разработчикам SharePoint, указав в [списке проблем для репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues). Заранее спасибо!

## <a name="see-also"></a>См. также

- [Создание первого набора команд ListView](./building-simple-cmdset-with-dialog-api.md)
- [Создание первого расширения для настройки полей](./building-simple-field-customizer.md)
- [Обзор расширений SharePoint Framework](../overview-extensions.md)