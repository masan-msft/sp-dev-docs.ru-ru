---
title: "Развертывание решений SharePoint Framework на уровне клиента"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 2340e4f5ee0bdc48c5bd4dd6dc85f9c63e3b2697
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a><span data-ttu-id="f18b9-102">Развертывание решений SharePoint Framework на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="f18b9-102">Tenant-Scoped solution deployment for SharePoint Framework solutions</span></span>

<span data-ttu-id="f18b9-p101">Вы можете настроить компоненты SharePoint Framework так, чтобы они были доступны в клиенте сразу после установки пакета решения в каталоге приложений клиента. Это можно сделать с помощью атрибута **skipFeatureDeployment** в файле **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p101">You can configure your SharePoint Framework components to be immediately available cross the tenant when solution package is installed to tenant app catalog. This can be configured by using **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span>

<span data-ttu-id="f18b9-105">Если в решении включен этот атрибут, администратор клиента может сделать решение доступным во всех семействах веб-сайтов и на всех сайтах в клиенте сразу после установки пакета решения в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="f18b9-105">When solution has this attribute enabled, tenant administrator will be provided option to enable the solution to be available automatically cross all site collections and sites in tenant, when the solution package is installed to the tenant app catalog.</span></span> 

<span data-ttu-id="f18b9-106">Развертывание на уровне клиента также демонстрируется в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=pemHOZCSwZI).</span><span class="sxs-lookup"><span data-stu-id="f18b9-106">You can also see the tenant-wide deployment option demonstrated by watching following video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=pemHOZCSwZI).</span></span>

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> <span data-ttu-id="f18b9-p102">Обратите внимание, что для использования этой возможности необходимо обновить шаблон Yeoman для SharePoint Framework до последней версии. Вы можете обновить глобальную установку с помощью команды `npm install -g @microsoft/generator-sharepoint`.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p102">Notice. You have to update to latest SharePoint Framework Yeoman template version to be able to use this capability. You can update your global installation by executing `npm install -g @microsoft/generator-sharepoint`.</span></span> 

## <a name="solution-specific-requirements"></a><span data-ttu-id="f18b9-110">Специальные требования для решений</span><span class="sxs-lookup"><span data-stu-id="f18b9-110">Solution specific requirements</span></span>

<span data-ttu-id="f18b9-p103">При использовании этот параметра игнорируются все определения платформы компонентов в решении SharePoint Framework. Если решение содержит определения платформы компонентов, например для создания настраиваемого списка, то не следует использовать этот специальный параметр решения.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p103">When this option is used, any feature framework definitions in the SharePoint Framework solution will be ignored. If solution contains Feature Framework definitions, for example for creating a custom list, you should not use this solution specific option.</span></span>

* [<span data-ttu-id="f18b9-113">Подготовка ресурсов SharePoint с пакетом решения</span><span class="sxs-lookup"><span data-stu-id="f18b9-113">Provision SharePoint assets with your solution package</span></span>](#)

> <span data-ttu-id="f18b9-p104">Обратите внимание, что решения, настроенные для автоматического развертывания на уровне клиента, не отображаются при добавлении приложения на уровне сайта.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p104">Notice. Solutions which are configured to be automatically deployed cross tenants are not visible in the add an app capability at the site level.</span></span> 

## <a name="configuring-solution-to-be-available-cross-tenant"></a><span data-ttu-id="f18b9-116">Настройка решения для доступности во всем клиенте</span><span class="sxs-lookup"><span data-stu-id="f18b9-116">Configuring solution to be available cross tenant</span></span>

<span data-ttu-id="f18b9-p105">Шаблон Yeoman для SharePoint Framework задаст конкретный вопрос, связанный с этим вариантом развертывания. Это непосредственно повлияет на атрибут **skipFeatureDeployment** в файле **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p105">SharePoint Framework Yeoman template will ask a specific question related on this option. This question will impact directly on the **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span> 

![Вопрос Yeoman о варианте развертывания на уровне клиента](../images/tenant-deploy-yeoman.png)

<span data-ttu-id="f18b9-120">В приведенном ниже примере конфигурации для параметра **skipFeatureDeployment** задано значение true, указывающее, что решение можно централизованно развернуть на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="f18b9-120">In following example configuration, **skipFeatureDeployment** is set to true, which indicates that solution can be centrally deployed cross the tenant.</span></span> 

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

### <a name="approving-tenant-wide-deployment-in-app-catalog"></a><span data-ttu-id="f18b9-121">Утверждение развертывания на уровне клиента в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="f18b9-121">Approving tenant wide deployment in app catalog</span></span>

<span data-ttu-id="f18b9-122">При развертывании решения, где для атрибута **skipFeatureDeployment** задано значение **true**, в каталоге приложений администратор может настроить решение на централизованное развертывание на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="f18b9-122">When solution with **skipFeatureDeployment** attribute set to **true** is deployed to tenant app catalog, administrator is given an option to configure solution to be deployed centrally cross the tenant.</span></span>

<span data-ttu-id="f18b9-p106">По умолчанию флажок **Сделать это решение доступным всем сайтам в организации** снят. Если администратор установит этот флажок, компоненты решения будут автоматически видны и доступны на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p106">By default, "**Make this solution available to all sites in the organization**" checkbox is unchecked. If the checkbox is checked by the administrator, components in the solutions will be automatically visible and available cross the tenant.</span></span> 

![Параметр "Сделать это решение доступным всем сайтам в организации" при развертывании решения в каталоге приложений](../images/tenant-deploy-app-catalog.png)

<span data-ttu-id="f18b9-p107">Обратите внимание, что специальные действия по обновлению решений и сайтов доступны только при использовании платформы компонентов, поэтому не существует специального варианта обновления для централизованно развернутых решений. Вы можете просто обновить ресурс такого решения в сети CDN и пакет в каталоге приложений. При этом все существующие экземпляры компонентов будут автоматически обновлены для использования последних версий ресурсов компонентов, таких как файлы JavaScript и обновленные CSS-файлы.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p107">Notice that since the solution and site -specific upgrade actions are only available when you use feature framework, there's no specific upgrade option for the centrally deployed solutions. These solutions can be simply updated by updating solution specific assets in the CDN and by updating package in the app catalog. This will update automatically all existing component instances cross the tenant to use the latest component assets, like JavaScript files and updated CSS files.</span></span>

## <a name="client-side-web-part-visibility-in-sharepoint-sites"></a><span data-ttu-id="f18b9-129">Видимость клиентских веб-частей на сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="f18b9-129">Client-side web part visibility in SharePoint sites</span></span>

<span data-ttu-id="f18b9-130">Веб-части, включенные в централизованно развернутые решения, будут автоматически видны в средстве выбора веб-частей как на классических, так и на современных страницах.</span><span class="sxs-lookup"><span data-stu-id="f18b9-130">Web parts included in solutions which have been centrally deployed, will be immediately visible in the web part picker in both classic and modern pages.</span></span> 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a><span data-ttu-id="f18b9-131">Влияние параметра skipFeatureDeployment на расширения</span><span class="sxs-lookup"><span data-stu-id="f18b9-131">Impact of skipFeatureDeployment setting with Extensions</span></span>

<span data-ttu-id="f18b9-p108">Расширения SharePoint Framework будут сразу доступны для использования на сайтах SharePoint. Это означает, что их можно связывать для использования со свойствами **ClientSideComponentId** в определенных элементах SharePoint, таких как *поля* и *пользовательские дополнительные действия*.</span><span class="sxs-lookup"><span data-stu-id="f18b9-p108">SharePoint Framework extensions will be immediately available to be used in the SharePoint sites. This means that they can be associated to be used with **ClientSideComponentId** properties in the specific SharePoint elements, like *fields* and *user custom actions*.</span></span> 

