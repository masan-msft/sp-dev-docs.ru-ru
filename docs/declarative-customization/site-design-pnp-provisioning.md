---
title: "Создание полноценного макета сайта SharePoint с помощью модуля подготовки PnP"
description: "Создание полноценного макета сайта SharePoint с помощью модуля подготовки PnP"
ms.date: 12/14/2017
ms.openlocfilehash: 028a028822c234dcbbbad290c642ec03dd4b6392
ms.sourcegitcommit: d9372f6009de1c1e48e272fd3629a99aed7fef9f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/09/2018
---
# <a name="calling-the-pnp-provisioning-engine-from-a-site-script"></a>Вызов модуля подготовки PnP из скрипта на сайте

> [!NOTE]
> Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться. В настоящее время их нельзя использовать в рабочих средах.

Макеты сайтов — удобный способ стандартизации внешнего вида семейств веб-сайтов. Однако они не поддерживают некоторые задачи, например, не позволяют добавить нижний колонтитул на каждую страницу. С помощью модуля подготовки PnP вы можете создать шаблон, позволяющий подготовить настройщик для сайта. Этот настройщик затем может обновить макет страницы, например, чтобы зарегистрировать нижний колонтитул на каждой странице. 

В этой статье описано, как создать макет сайта, который применяет шаблон подготовки PnP к сайту. Шаблон добавит настройщик для отображения нижнего колонтитула.

В этой статье используются следующие компоненты:

- макет и скрипт сайта;
- поток Microsoft Flow;
- хранилище очередей Azure
- функция Azure;
- решение SharePoint Framework (SPFx);
- шаблон подготовки PnP;
- скрипт PnP PowerShell;
- идентификатор и секрет приложения с правами администратора для клиента.

Эти компоненты используются для активации кода подготовки PnP после создания сайта и применения макета.

## <a name="set-up-app-only-access-to-your-tenant"></a>Настройка доступа к клиенту на уровне приложения

Чтобы настроить доступ на уровне приложения, нужны две страницы: одна — на обычном сайте, а другая — на сайте администрирования SharePoint.

1. Перейдите по следующему URL-адресу в своем клиенте: `https://[yourtenant].sharepoint.com/_layouts/appregnew.aspx` (вы можете перейти на любой сайт, но пока лучше использовать корневой).
1. Нажмите кнопку **Создать** рядом с полями **Идентификатор клиента** и **Секрет клиента**.
1. Введите название приложения, например "Подготовка сайта".
1. В поле **Домен приложения** введите **localhost**.
1. В поле **URI перенаправления** введите **https://localhost**.

    ![Страница создания приложения с полями "Идентификатор клиента", "Секрет клиента", "Название", "Домен приложения" и "URI перенаправления"](images/pnpprovisioning-createapponly.png)

1. Нажмите кнопку **Создать**. 
1. Скопируйте значения из полей **Идентификатор клиента** и **Секрет клиента** — они понадобятся вам позже.

После этого подтвердите, что вы доверяете приложению, чтобы предоставить ему доступ к вашему клиенту:

1. Перейдите по адресу `https://[yourtenant]-admin.sharepoint.com/_layouts/appinv.aspx` (обратите внимание на оператор `-admin` в URL-адресе).
1. В поле **Идентификатор приложения** вставьте скопированный **идентификатор клиента** и нажмите кнопку **Поиск**.
1. Вставьте следующий код XML в поле **XML-запрос разрешения**:

    ```xml
    <AppPermissionRequests AllowAppOnlyPolicy="true" >
        <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
    </AppPermissionRequests>
    ```

1. Нажмите кнопку **Создать**.
1. Чтобы подтвердить, что вы доверяете этому приложению, нажмите кнопку **Доверять**.


## <a name="create-the-azure-queue-storage"></a>Создание хранилища очередей Azure

В этом разделе показано, как получить сообщения из Microsoft Flow, используя хранилище очередей Azure. Каждый раз, когда в хранилище очередей появляется сообщение, вызывается функция Azure для выполнения скрипта PowerShell. 

Чтобы настроить хранилище очередей Azure:

1. Перейдите на [портал Azure](https://portal.azure.com) и войдите.
1. Нажмите **+ Создать**.
1. Выберите **Storage** в списке решений Azure Marketplace, а затем выберите **Учетная запись хранения — BLOB-объект, файл, таблица, очередь** в столбце "Рекомендованные".
1. Укажите значения в обязательных полях. Выберите **Закрепить на панели мониторинга** и нажмите **Создать**. Создание учетной записи хранения может занять несколько минут.
1. Откройте учетную запись хранения и перейдите в раздел **Очереди**.
1. Выберите **+ Очередь** в верхней части экрана.
1. Введите имя **pnpprovisioningqueue** или собственное значение, соответствующее стандарту именования. Запишите имя очереди; это значение понадобится вам при создании функции Azure.
1. Перейдите в раздел **Ключи доступа** и запишите **имя учетной записи хранения** и значение ключа **key1**. Эти значения понадобятся вам при создании потока.


## <a name="create-the-flow"></a>Создание потока

Чтобы поместить сообщение в очередь, необходимо создать поток. 

1. Перейдите на сайт [Microsoft Flow](https://flow.microsoft.com), войдите и выберите **Создать с нуля** в верхней части страницы.
1. Нажмите **Поиск среди сотен соединителей и триггеров**, чтобы выбрать триггер.
1. Введите слово **Запрос** и выберите **Запрос - При получении HTTP-запроса**.
1. Введите следующий код JSON в теле запроса:

    ```json
    {
        "type": "object",
        "properties": {
            "webUrl": {
                "type": "string"
            },
            "parameters": {
                "type": "object",
                "properties": {
                    "event": {
                        "type": "string"
                    },
                    "product": {
                        "type": "string"
                    }
                }
            }
        }
    }
    ``` 

1. Нажмите **+ Новый шаг** и выберите **Добавить действие**.
1. Выполните поиск по запросу **Очереди Azure** и выберите **Очереди Azure - Поместить сообщение в очередь**.
1. Введите описательное имя подключения.
1. Введите имя учетной записи хранения, скопированное в предыдущем разделе.
1. Введите открытый ключ хранилища, представляющий собой значение ключа **Key1** для учетной записи хранения.
1. Нажмите кнопку **Создать**.
1. Выберите имя очереди **pnpprovisioningqueue**.
1. В теле запроса вы указали входящий параметр *webUrl*. Чтобы поместить значение этого поля в очередь, щелкните поле **Сообщение** и выберите **webUrl** в средстве выбора динамического контента.
1. Нажмите **Сохранить поток**. При этом будет создан URL-адрес, который вы скопируете на следующем шаге.
1. Выберите первый шаг потока ("При получении HTTP-запроса") и скопируйте URL-адрес.
1. Сохраните поток.

Поток должен выглядеть следующим образом.

![Снимок экрана: поток "При получении HTTP-запроса" с URL-адресом и телом запроса, а также поля "Имя очереди" и "Сообщение"](images/pnpprovisioning-flow-overview.png)

## <a name="test-the-flow"></a>Проверка потока

Чтобы проверить поток, необходимо отправить POST-запрос. Это можно сделать через PowerShell, как показано в следующем примере.

```powershell
$uri = "[the URI you copied in step 14 when creating the flow]"
$body = "{webUrl:'somesiteurl'}
Invoke-RestMethod -Uri $uri -Method Post -ContentType "application/json" -Body $body
```

После перехода на главный экран потока вы увидите журнал выполнения. Состояние `Succeeded` означает, что поток выполнен успешно.
Теперь перейдите к новой очереди Azure и нажмите кнопку **Обновить**. Должна появиться запись о правильном вызове потока.

## <a name="provision-the-spfx-solution"></a>Подготовка решения SPFx

В этом разделе вы будете использовать существующее решение SPFx [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer). Выполните инструкции из файла [Readme](https://github.com/SharePoint/sp-dev-fx-extensions/blob/master/samples/react-application-regions-footer/README.md) в репозитории примера, чтобы создать и подготовить решение.

## <a name="create-a-pnp-provisioning-template"></a>Создание шаблона подготовки PnP

Скопируйте следующий шаблон подготовки XML в новый файл и сохраните его с именем FlowDemoTemplate.xml.

```xml
<?xml version="1.0"?>
<pnp:Provisioning xmlns:pnp="http://schemas.dev.office.com/PnP/2017/05/ProvisioningSchema">
  <pnp:Preferences Generator="OfficeDevPnP.Core, Version=2.20.1711.0, Culture=neutral, PublicKeyToken=3751622786b357c2" />
  <pnp:Templates ID="CONTAINER-FLOWDEMO">
    <pnp:ProvisioningTemplate ID="TEMPLATE-FLOWDEMO" Version="1" BaseSiteTemplate="GROUP#0" Scope="RootSite">
      <pnp:CustomActions>
        <pnp:WebCustomActions>
          <pnp:CustomAction Name="spfx-react-app-customizer" Description="Custom action for Application Customizer" Location="ClientSideExtension.ApplicationCustomizer" Title="spfx-react-app-customizer" Sequence="0" Rights="" RegistrationType="None" ClientSideComponentId="67fd1d01-84e8-4fbf-85bd-4b80768c6080" ClientSideComponentProperties="{&quot;SourceTermSetName&quot;:&quot;Regions&quot;}" />
        </pnp:WebCustomActions>
      </pnp:CustomActions>
    </pnp:ProvisioningTemplate>
  </pnp:Templates>
</pnp:Provisioning>
```

> [!NOTE]
> Шаблон подготовки добавляет в решение дополнительное действие. Идентификатор **ClientSideComponentId** связан с подготовленным ранее решением [Regions Footer Application Customizer](https://github.com/SharePoint/sp-dev-fx-extensions/tree/master/samples/react-application-regions-footer). Чтобы запустить эту демонстрацию с собственным решением SPFx, измените значения атрибутов **ClientSideComponentId** и (необязательно) **ClientSideComponentProperties** в XML-файле.

## <a name="create-the-azure-function"></a>Создание функции Azure

1. Перейдите на [портал Azure](https://portal.azure.com).
1. Выполните поиск по запросу **Приложение-функция** и создайте приложение-функцию. В поле **Хранение** выберите **Использовать имеющееся**, а затем укажите созданную ранее учетную запись хранения. При необходимости задайте другие значения.
1. Откройте приложение-функцию и выберите **Функции** > **Новая функция**.

    ![Снимок экрана: портал Azure с выделенной командой "Новая функция"](images/pnpprovisioning-create-function.png)

1. В раскрывающемся списке "Язык" выберите **PowerShell**.
1. Выберите **QueueTrigger — PowerShell**.
1. Назовите функцию **ApplyPnPProvisioningTemplate**. 
1. Введите имя созданной ранее очереди.
1. Нажмите кнопку **Создать**. Откроется редактор, в котором можно вводить командлеты PowerShell. 

Ниже описано, как загрузить модуль PowerShell PnP, чтобы использовать его в функции Azure.

## <a name="upload-the-pnp-powershell-module-for-your-azure-function"></a>Загрузка модуля PowerShell PnP для функции Azure

Чтобы загрузить модуль PnP PowerShell для функции Azure, его сначала нужно скачать.

1. Создайте временную папку на своем компьютере.
1. Запустите PowerShell и введите следующую команду:
    ```powershell
    Save-Module -Name SharePointPnPPowerShellOnline -Path [pathtoyourfolder]
    ```
Файлы модуля PowerShell скачаются в папку в созданной папке. 

После этого загрузите файлы, чтобы функция Azure могла использовать модуль.

1. Перейдите на главную страницу приложения-функции и выберите **Функции платформы**.

    ![Снимок экрана: приложение-функция с выделенным пунктом "Функции платформы"](images/pnpprovisioning-platform-features.png)

1. Выберите **Дополнительные инструменты (Kudu)**.

    ![Снимок экрана: средства разработки с выделенным пунктом "Дополнительные инструменты (Kudu)"](images/pnpprovisioning-select-kudu.png)

1. На главной странице Kudu нажмите **Консоль отладки** и выберите **CMD** или **PowerShell**.
1. Выберите проводник в верхней части страницы и перейдите в раздел **site\wwwroot\\[nameofyourazurefunction]**.
1. Создайте папку **modules**.
    
    ![Снимок экрана: выделенная команда "Создать папку"](images/pnpprovisioning-kudu-create-folder.png)

1. В папке modules создайте еще одну папку с именем **SharePointPnPPowerShellOnline** и перейдите в нее.
1. В проводнике на компьютере перейдите в папку, в которую вы скачали файлы модуля PowerShell PnP. Откройте папку **SharePointPnPPowerShellOnline\2.20.1711.0** (обратите внимание, что номер версии может отличаться).
1. Перетащите все файлы из этой папки в папку в Kudu.

   ![Снимок экрана: папка Kudu с 40 добавленными файлами](images/pnpprovisioning-module-files-uploaded.png)

## <a name="finish-the-azure-function"></a>Завершение создания функции Azure

1. Вернитесь к функции Azure и разверните вкладку файлов справа.

    ![Снимок экрана: вкладка "Просмотр файлов"](images/pnpprovisioning-view-files.png)

1. Нажмите **Отправить** и загрузите созданный ранее файл шаблона подготовки.
1. Замените скрипт PowerShell следующим кодом:

    ```powershell
    $in = Get-Content $triggerInput -Raw
    Write-Output "Incoming request for '$in'"
    Connect-PnPOnline -AppId $env:SPO_AppId -AppSecret $env:SPO_AppSecret -Url $in
    Write-Output "Connected to site"
    Apply-PnPProvisioningTemplate -Path D:\home\site\wwwroot\ApplyPnPProvisioningTemplate\FlowDemoTemplate.xml
    ```

Обратите внимание, что здесь используются две переменные среды: ```SPO_AppId``` и ```SPO_AppSecret```. Чтобы задать эти переменные, перейдите на страницу приложения-функции на портале Azure, выберите **Параметры приложения** и добавьте два новых параметра приложения:

1. ```SPO_AppId```. Укажите в качестве значения идентификатор клиента, скопированный на первом шаге при создании приложения в клиенте.
2. ```SPO_AppSecret```. Укажите в качестве значения секрет клиента, скопированный на первом шаге при создании приложения в клиенте.

## <a name="create-the-site-design"></a>Создание макета сайта

Откройте PowerShell и убедитесь, что установлена консоль управления Microsoft Office 365.

Подключитесь к клиенту, используя командлет **Connect-SPOService**.

```powershell
Connect-SPOService -Url https://[yourtenant]-admin.sharepoint.com
```

Теперь вы можете получить имеющиеся макеты сайта. 

```powershell
Get-SPOSiteDesign
```

Чтобы создать макет сайта, необходимо создать скрипт сайта. Макет сайта — это контейнер, который ссылается на один или несколько скриптов.

1. Скопируйте приведенный ниже код JSON в буфер обмена и измените его. Задайте для свойства **url** значение, скопированное при создании потока. URL-адрес будет выглядеть примерно так, как показано ниже.

    `https://prod-27.westus.logic.azure.com:443/workflows/ef7434cf0d704dd48ef5fb6...oke?api-version=2016-06-01&sp=%2Ftriggers%2Fmanual%2Frun`

        ```json
        {
            "$schema": "schema.json",
            "actions": [
            {
                    "verb": "triggerFlow",
                    "url": "[paste the workflow trigger URL here]",
                    "name": "Apply Template",
                    "parameters": {
                        "event":"",
                        "product":""
                    }
            }
            ],
            "bindata": {},
            "version": 1
        }
        ```

1. Еще раз выделите JSON и скопируйте его в буфер обмена.
1. Откройте консоль PowerShell и введите следующую команду, чтобы скопировать скрипт в переменную и создать скрипт сайта:

    ```powershell
    $script = Get-Clipboard -Raw
    Add-SPOSiteScript -Title "Apply PnP Provisioning Template" -Content $script
    Get-SPOSiteScript
    ```

1. Появится список из одного или нескольких скриптов сайта, включая только что созданный. Выделите идентификатор созданного скрипта сайта и скопируйте его в буфер обмена.
1. Создайте макет сайта, используя следующую команду:

    ```powershell
    Add-SPOSiteDesign -Title "Site with footer" -SiteScripts [Paste the ID of the Site Script here] -WebTemplate "64"
    ```

Командлет **Add-SPOSiteDesign** связывает макет с сайтом группы. Чтобы связать макет с сайтом для общения, используйте значение 68.

## <a name="verify-the-results"></a>Проверка результатов

После создания хранилища очередей Azure вы создали идентификатор приложения для доступа на уровне приложения, функцию Azure и макет сайта. После этого вы активировали поток Microsoft Flow из макета сайта. 

Чтобы проверить результаты, создайте новый сайт. В клиенте SharePoint выберите **SharePoint** > **Создать сайт** > **Сайт группы**. Новый макет сайта должен появиться в списке доступных макетов. Обратите внимание, что макет сайта применяется после создания сайта. Если поток настроен правильно, он будет активирован. Вы можете проверить работу потока, просмотрев журнал выполнения. Обратите внимание, что нижний колонтитул может появиться не сразу; если вы его не видите, подождите минуту и перезагрузите сайт.


