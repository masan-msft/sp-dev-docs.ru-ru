---
title: "Развертывание решений SharePoint Framework на уровне клиента"
description: "Узнайте, как сделать свои компоненты SharePoint Framework доступными во всем клиенте сразу после установки пакета решения в каталоге приложений клиента."
ms.date: 02/02/2018
ms.prod: sharepoint
ms.openlocfilehash: d48aa779602950cd589b4d5e6dbaab868b698f9e
ms.sourcegitcommit: 7a40bb847e8753810ab7f907d638f3cac022d444
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/05/2018
---
# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a>Развертывание решений SharePoint Framework на уровне клиента

Вы можете сделать свои компоненты SharePoint Framework доступными во всем клиенте сразу после установки пакета решения в каталоге приложений клиента. Для этого используется атрибут **skipFeatureDeployment** в файле **package-solution.json**.

Если в решении включен этот атрибут, администратор клиента может сделать решение доступным во всех семействах веб-сайтов и на всех сайтах в клиенте сразу после установки пакета решения в каталоге приложений клиента. 

Развертывание на уровне клиента также демонстрируется в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=pemHOZCSwZI).

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> [!NOTE] 
> Для использования этой возможности необходимо обновить шаблон Yeoman для SharePoint Framework до последней версии. Вы можете обновить глобальную установку с помощью команды `npm install -g @microsoft/generator-sharepoint`. 

## <a name="solution-specific-requirements"></a>Требования для решений

При использовании этого параметра игнорируются все определения платформы компонентов в решении SharePoint Framework. Если решение содержит определения платформы компонентов, например для создания настраиваемого списка, то не следует использовать этот специальный параметр решения.

Дополнительные сведения см. в статье [Подготовка ресурсов SharePoint с пакетом решения](./toolchain/provision-sharepoint-assets.md).

> [!NOTE] 
> Решения, настроенные на автоматическое развертывание на уровне клиента, не отображаются при добавлении приложения на уровне сайта. 

## <a name="configure-solution-to-be-available-across-the-tenant"></a>Настройка решения для доступности во всем клиенте

В шаблоне Yeoman для SharePoint Framework есть отдельный вопрос, связанный с этой возможностью. Ответ на этот вопрос влияет непосредственно на атрибут **skipFeatureDeployment** в файле **package-solution.json**. 

![Вопрос Yeoman о варианте развертывания на уровне клиента](../images/tenant-deploy-yeoman.png)

<br/>

В приведенном ниже примере конфигурации для параметра **skipFeatureDeployment** задано значение true, указывающее, что решение можно централизованно развернуть на уровне клиента. 

```json
{
  "solution": {
    "name": "tenant-deploy-client-side-solution",
    "id": "dd4feca4-6f7e-47f1-a0e2-97de8890e3fa",
    "version": "1.0.0.0",
    "skipFeatureDeployment": true
  },
  "paths": {
    "zippedPackage": "solution/tenant-deploy-true.sppkg"
  }
}

```

### <a name="approving-tenant-wide-deployment-in-app-catalog"></a>Утверждение развертывания на уровне клиента в каталоге приложений

При развертывании решения, где для атрибута **skipFeatureDeployment** задано значение **true**, в каталоге приложений администратор может настроить решение на централизованное развертывание на уровне клиента.

По умолчанию флажок **Сделать это решение доступным для всех сайтов в организации** не установлен. Если администратор установит этот флажок, компоненты решений будут автоматически видны и доступны во всем клиенте. 

![Параметр "Сделать это решение доступным для всех сайтов в организации" отображается при развертывании решения в каталоге приложений](../images/tenant-deploy-app-catalog.png)

Обратите внимание: так как действия по обновлению решений и сайтов доступны только при использовании платформы компонентов, специального способа обновления централизованно развернутых решений не существует. Эти решения можно обновлять путем обновления ресурсов в сети CDN и обновления пакета в каталоге приложений. При этом все существующие экземпляры компонентов автоматически начинают использовать новейшие ресурсы, такие как файлы JavaScript и обновленные CSS-файлы.

## <a name="client-side-web-part-visibility-on-sharepoint-sites"></a>Видимость клиентских веб-частей на сайтах SharePoint

Веб-части, включенные в централизованно развернутые решения, будут автоматически видны в средстве выбора веб-частей как на классических, так и на современных страницах. 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a>Влияние параметра skipFeatureDeployment на расширения

[Расширения SharePoint Framework](./extensions/overview-extensions.md) сразу доступны для использования на сайтах SharePoint. Это означает, что их можно сопоставлять со свойствами **ClientSideComponentId** в определенных элементах SharePoint, таких как **поля** и **дополнительные действия пользователей**. 

## <a name="see-also"></a>См. также

- [Обзор SharePoint Framework](sharepoint-framework-overview.md)