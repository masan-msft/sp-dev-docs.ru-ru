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
# <a name="tenant-scoped-solution-deployment-for-sharepoint-framework-solutions"></a><span data-ttu-id="159c4-103">Развертывание решений SharePoint Framework на уровне клиента</span><span class="sxs-lookup"><span data-stu-id="159c4-103">Tenant-Scoped solution deployment for SharePoint Framework solutions</span></span>

<span data-ttu-id="159c4-104">Вы можете сделать свои компоненты SharePoint Framework доступными во всем клиенте сразу после установки пакета решения в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="159c4-104">You can configure your SharePoint Framework components to be immediately available across the tenant when the solution package is installed to the tenant App Catalog.</span></span> <span data-ttu-id="159c4-105">Для этого используется атрибут **skipFeatureDeployment** в файле **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="159c4-105">This can be configured by using the **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span>

<span data-ttu-id="159c4-106">Если в решении включен этот атрибут, администратор клиента может сделать решение доступным во всех семействах веб-сайтов и на всех сайтах в клиенте сразу после установки пакета решения в каталоге приложений клиента.</span><span class="sxs-lookup"><span data-stu-id="159c4-106">When solution has this attribute enabled, tenant administrator will be provided option to enable the solution to be available automatically cross all site collections and sites in tenant, when the solution package is installed to the tenant app catalog.</span></span> 

<span data-ttu-id="159c4-107">Развертывание на уровне клиента также демонстрируется в видео на [канале SharePoint PnP в YouTube](https://www.youtube.com/watch?v=pemHOZCSwZI).</span><span class="sxs-lookup"><span data-stu-id="159c4-107">You can also see the tenant-wide deployment option demonstrated by watching following video on the [SharePoint PnP YouTube Channel](https://www.youtube.com/watch?v=pemHOZCSwZI).</span></span>

<a href="https://www.youtube.com/watch?v=pemHOZCSwZI&list=PLR9nK3mnD-OXZbEvTEPxzIOMGXj_aZKJG">
<img src="../images/tenant-deploy-youtube-video.png" alt="PnP Short Guidance video on tenant-wide deployment option" />
</a>

> [!NOTE] 
> <span data-ttu-id="159c4-108">Для использования этой возможности необходимо обновить шаблон Yeoman для SharePoint Framework до последней версии.</span><span class="sxs-lookup"><span data-stu-id="159c4-108">Notice. You have to update to latest SharePoint Framework Yeoman template version to be able to use this capability. You can update your global installation by executing .</span></span> <span data-ttu-id="159c4-109">Вы можете обновить глобальную установку с помощью команды `npm install -g @microsoft/generator-sharepoint`.</span><span class="sxs-lookup"><span data-stu-id="159c4-109">You can update your global installation by executing `npm install -g @microsoft/generator-sharepoint`.</span></span> 

## <a name="solution-specific-requirements"></a><span data-ttu-id="159c4-110">Требования для решений</span><span class="sxs-lookup"><span data-stu-id="159c4-110">Solution-specific requirements</span></span>

<span data-ttu-id="159c4-p103">При использовании этого параметра игнорируются все определения платформы компонентов в решении SharePoint Framework. Если решение содержит определения платформы компонентов, например для создания настраиваемого списка, то не следует использовать этот специальный параметр решения.</span><span class="sxs-lookup"><span data-stu-id="159c4-p103">When this option is used, any feature framework definitions in the SharePoint Framework solution will be ignored. If solution contains Feature Framework definitions, for example for creating a custom list, you should not use this solution specific option.</span></span>

<span data-ttu-id="159c4-113">Дополнительные сведения см. в статье [Подготовка ресурсов SharePoint с пакетом решения](./toolchain/provision-sharepoint-assets.md).</span><span class="sxs-lookup"><span data-stu-id="159c4-113">For more information, see [Provision SharePoint assets with your solution package](./toolchain/provision-sharepoint-assets.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="159c4-114">Решения, настроенные на автоматическое развертывание на уровне клиента, не отображаются при добавлении приложения на уровне сайта.</span><span class="sxs-lookup"><span data-stu-id="159c4-114">Notice. Solutions which are configured to be automatically deployed cross tenants are not visible in the add an app capability at the site level.</span></span> 

## <a name="configure-solution-to-be-available-across-the-tenant"></a><span data-ttu-id="159c4-115">Настройка решения для доступности во всем клиенте</span><span class="sxs-lookup"><span data-stu-id="159c4-115">Configure solution to be available across the tenant</span></span>

<span data-ttu-id="159c4-116">В шаблоне Yeoman для SharePoint Framework есть отдельный вопрос, связанный с этой возможностью.</span><span class="sxs-lookup"><span data-stu-id="159c4-116">The SharePoint Framework Yeoman template asks a specific question related to this option.</span></span> <span data-ttu-id="159c4-117">Ответ на этот вопрос влияет непосредственно на атрибут **skipFeatureDeployment** в файле **package-solution.json**.</span><span class="sxs-lookup"><span data-stu-id="159c4-117">This question impacts directly on the **skipFeatureDeployment** attribute in the **package-solution.json** file.</span></span> 

![Вопрос Yeoman о варианте развертывания на уровне клиента](../images/tenant-deploy-yeoman.png)

<br/>

<span data-ttu-id="159c4-119">В приведенном ниже примере конфигурации для параметра **skipFeatureDeployment** задано значение true, указывающее, что решение можно централизованно развернуть на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="159c4-119">In following example configuration, **skipFeatureDeployment** is set to true, which indicates that solution can be centrally deployed cross the tenant.</span></span> 

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

### <a name="approving-tenant-wide-deployment-in-app-catalog"></a><span data-ttu-id="159c4-120">Утверждение развертывания на уровне клиента в каталоге приложений</span><span class="sxs-lookup"><span data-stu-id="159c4-120">Approving tenant-wide deployment in App Catalog</span></span>

<span data-ttu-id="159c4-121">При развертывании решения, где для атрибута **skipFeatureDeployment** задано значение **true**, в каталоге приложений администратор может настроить решение на централизованное развертывание на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="159c4-121">When solution with **skipFeatureDeployment** attribute set to **true** is deployed to tenant app catalog, administrator is given an option to configure solution to be deployed centrally cross the tenant.</span></span>

<span data-ttu-id="159c4-122">По умолчанию флажок **Сделать это решение доступным для всех сайтов в организации** не установлен.</span><span class="sxs-lookup"><span data-stu-id="159c4-122">By default, the **Make this solution available to all sites in the organization** check box is not selected.</span></span> <span data-ttu-id="159c4-123">Если администратор установит этот флажок, компоненты решений будут автоматически видны и доступны во всем клиенте.</span><span class="sxs-lookup"><span data-stu-id="159c4-123">If the check box is selected by the administrator, components in the solutions are automatically visible and available across the tenant.</span></span> 

![Параметр "Сделать это решение доступным для всех сайтов в организации" отображается при развертывании решения в каталоге приложений](../images/tenant-deploy-app-catalog.png)

<span data-ttu-id="159c4-125">Обратите внимание: так как действия по обновлению решений и сайтов доступны только при использовании платформы компонентов, специального способа обновления централизованно развернутых решений не существует.</span><span class="sxs-lookup"><span data-stu-id="159c4-125">Notice that because the solution and site-specific upgrade actions are only available when you use the feature framework, there's no specific upgrade option for the centrally deployed solutions.</span></span> <span data-ttu-id="159c4-126">Эти решения можно обновлять путем обновления ресурсов в сети CDN и обновления пакета в каталоге приложений.</span><span class="sxs-lookup"><span data-stu-id="159c4-126">These solutions can be updated by updating the solution-specific assets in the CDN and by updating the package in the App Catalog.</span></span> <span data-ttu-id="159c4-127">При этом все существующие экземпляры компонентов автоматически начинают использовать новейшие ресурсы, такие как файлы JavaScript и обновленные CSS-файлы.</span><span class="sxs-lookup"><span data-stu-id="159c4-127">This automatically updates all existing component instances across the tenant to use the latest component assets, such as JavaScript files and updated CSS files.</span></span>

## <a name="client-side-web-part-visibility-on-sharepoint-sites"></a><span data-ttu-id="159c4-128">Видимость клиентских веб-частей на сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="159c4-128">Client-side web part visibility in SharePoint sites</span></span>

<span data-ttu-id="159c4-129">Веб-части, включенные в централизованно развернутые решения, будут автоматически видны в средстве выбора веб-частей как на классических, так и на современных страницах.</span><span class="sxs-lookup"><span data-stu-id="159c4-129">Web parts included in solutions which have been centrally deployed, will be immediately visible in the web part picker in both classic and modern pages.</span></span> 

## <a name="impact-of-skipfeaturedeployment-setting-with-extensions"></a><span data-ttu-id="159c4-130">Влияние параметра skipFeatureDeployment на расширения</span><span class="sxs-lookup"><span data-stu-id="159c4-130">Impact of skipFeatureDeployment setting with Extensions</span></span>

<span data-ttu-id="159c4-131">[Расширения SharePoint Framework](./extensions/overview-extensions.md) сразу доступны для использования на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="159c4-131">[SharePoint Framework Extensions](./extensions/overview-extensions.md) are immediately available to be used on SharePoint sites.</span></span> <span data-ttu-id="159c4-132">Это означает, что их можно сопоставлять со свойствами **ClientSideComponentId** в определенных элементах SharePoint, таких как **поля** и **дополнительные действия пользователей**.</span><span class="sxs-lookup"><span data-stu-id="159c4-132">SharePoint Framework extensions will be immediately available to be used in the SharePoint sites. This means that they can be associated to be used with **ClientSideComponentId** properties in the specific SharePoint elements, like **fields** and **user custom actions**.</span></span> 

## <a name="see-also"></a><span data-ttu-id="159c4-133">См. также</span><span class="sxs-lookup"><span data-stu-id="159c4-133">See also</span></span>

- [<span data-ttu-id="159c4-134">Обзор SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="159c4-134">Overview of the SharePoint Framework</span></span>](sharepoint-framework-overview.md)