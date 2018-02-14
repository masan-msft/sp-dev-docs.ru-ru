---
title: "SharePoint Framework: известные проблемы и часто задаваемые вопросы"
description: "Здесь вы найдете ответы на проблемы и часто задаваемые вопросы, связанные с SharePoint Framework."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 79b580fd263636ccab392f99f11983c24ac08e8b
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-known-issues-and-frequently-asked-questions"></a><span data-ttu-id="3338b-103">SharePoint Framework: известные проблемы и часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3338b-103">SharePoint Framework known issues and frequently asked questions</span></span>

<span data-ttu-id="3338b-104">На этой странице представлены известные проблемы и ответы на часто задаваемые вопросы о SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="3338b-104">This page is for listing any known issues or to answer any frequently asked questions around SharePoint Framework.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="3338b-105">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="3338b-105">Known issues</span></span>

### <a name="dev-certificate-issue-with-chrome-v58-"></a><span data-ttu-id="3338b-106">Проблема с сертификатом разработчика в Chrome (версии 58 и новее)</span><span class="sxs-lookup"><span data-stu-id="3338b-106">Dev certificate issue with Chrome (v58-)</span></span>

- <span data-ttu-id="3338b-107">*Дата: 28 апреля 2017 г.*</span><span class="sxs-lookup"><span data-stu-id="3338b-107">*Date - April 28, 2017*</span></span>
- <span data-ttu-id="3338b-108">*Обновлено: 2 мая 2017 г.*</span><span class="sxs-lookup"><span data-stu-id="3338b-108">*Updated - May 2, 2017*</span></span>

<span data-ttu-id="3338b-109">Если вы используете браузер Chrome для разработки, у вас могут возникнуть проблемы с сертификатом разработчика независимо от того, выполняется ли команда `gulp trust-dev-cert`.</span><span class="sxs-lookup"><span data-stu-id="3338b-109">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing `gulp trust-dev-cert` command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span> <span data-ttu-id="3338b-110">В Chrome версии 58 и более новых изменилась модель проверки сертификатов, и во время доступа к локальной рабочей области может появиться такое сообщение: "Ваше подключение не защищено".</span><span class="sxs-lookup"><span data-stu-id="3338b-110">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing  command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span>

<span data-ttu-id="3338b-111">Следует обновить пакеты шаблонов Yeoman.</span><span class="sxs-lookup"><span data-stu-id="3338b-111">You should update your Yeoman template packages.</span></span> <span data-ttu-id="3338b-112">Мы обновили логику создания сертификатов в пакете [*@microsoft/gulp-core-build-serve*](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve).</span><span class="sxs-lookup"><span data-stu-id="3338b-112">We have updated certification creation logic in the [*@microsoft/gulp-core-build-serve* package](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve).</span></span> 

<span data-ttu-id="3338b-113">Для существующих решений вы можете просто удалить эту папку и запустить `npm install`, чтобы получить обновленный пакет.</span><span class="sxs-lookup"><span data-stu-id="3338b-113">In existing solutions, you can simply delete this folder and run `npm install` to get the updated package.</span></span> <span data-ttu-id="3338b-114">Кроме того, необходимо выполнить команды `untrust-dev-cert` и `trust-dev-cert` на компьютере, чтобы устранить проблему с логикой создания сертификатов.</span><span class="sxs-lookup"><span data-stu-id="3338b-114">You also need to execute `untrust-dev-cert` and `trust-dev-cert` commands on your machine to address the certification creation logic issue.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="3338b-115">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3338b-115">Frequently asked questions</span></span>

### <a name="when-will-custom-actions-and-jslink-be-available-in-the-sharepoint-framework"></a><span data-ttu-id="3338b-116">Когда в SharePoint Framework будут доступны дополнительные действия и JSLink?</span><span class="sxs-lookup"><span data-stu-id="3338b-116">When will custom actions and JSLink be available in the SharePoint Framework?</span></span>

- <span data-ttu-id="3338b-117">*Дата: 6 июня 2017 г.*</span><span class="sxs-lookup"><span data-stu-id="3338b-117">*Date - June 6, 2017*</span></span>

<span data-ttu-id="3338b-118">Расширения SharePoint Framework с дополнительными возможностями настройки теперь доступны в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="3338b-118">SharePoint Framework Extensions with additional customizations capabilities is now available in SharePoint Online.</span></span> <span data-ttu-id="3338b-119">Дополнительные сведения о расширениях SharePoint Framework можно найти в нашей документации:</span><span class="sxs-lookup"><span data-stu-id="3338b-119">You can find more information about SharePoint Framework Extensions from our documentation:</span></span>

- [<span data-ttu-id="3338b-120">Обзор расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="3338b-120">SharePoint Framework Extensions Overview</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="3338b-121">Руководства по расширениям SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="3338b-121">SharePoint Framework Extensions Tutorials</span></span>](./extensions/get-started/build-a-hello-world-extension.md)

### <a name="will-sharepoint-framework-be-available-in-on-premises"></a><span data-ttu-id="3338b-122">Будет ли платформа SharePoint Framework доступна локально?</span><span class="sxs-lookup"><span data-stu-id="3338b-122">Will SharePoint Framework be available in on-premises?</span></span>

- <span data-ttu-id="3338b-123">*Дата: 6 июня 2017 г.*</span><span class="sxs-lookup"><span data-stu-id="3338b-123">*Date - June 6, 2017*</span></span>

<span data-ttu-id="3338b-124">Клиентские веб-части SharePoint Framework на классических страницах выпущены для SharePoint 2016 в составе пакета дополнительных компонентов 2 (FP2).</span><span class="sxs-lookup"><span data-stu-id="3338b-124">SharePoint Framework client-side web parts on classic pages were released to SharePoint 2016 as part of the Feature Pack 2 (FP2).</span></span> <span data-ttu-id="3338b-125">Мы пока не планируем добавлять возможности SharePoint Framework в SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="3338b-125">There are no plans currently to provide SharePoint Framework capabilities to SharePoint 2013.</span></span> <span data-ttu-id="3338b-126">Полного списка возможностей SharePoint Framework, которые будут включены в выпуск SharePoint 2019, нет.</span><span class="sxs-lookup"><span data-stu-id="3338b-126">There's no specific list of SharePoint Framework capabilities which will be included in the SharePoint 2019 release.</span></span>

## <a name="see-also"></a><span data-ttu-id="3338b-127">См. также</span><span class="sxs-lookup"><span data-stu-id="3338b-127">See also</span></span>

<span data-ttu-id="3338b-128">Используйте указанные ниже ресурсы, чтобы отправлять отзывы, комментарии и вопросы, касающиеся разработки решений для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3338b-128">Please use following resources to provide feedback, comments and questions towards SharePoint engineering.</span></span> 

- [<span data-ttu-id="3338b-129">Проблемы с sp-dev-docs на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="3338b-129">GitHub sp-dev-docs issues</span></span>](https://github.com/SharePoint/sp-dev-docs/issues)
- [<span data-ttu-id="3338b-130">Пространство в сообществе технических специалистов Майкрософт, в котором участвуют разработчики решений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="3338b-130">SharePoint Developer MS Tech Community space</span></span>](https://aka.ms/sppnp-community)

