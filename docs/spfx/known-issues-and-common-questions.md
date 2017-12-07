---
title: "Известные проблемы и часто задаваемые вопросы"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9621898741763ed6adf9b967e8c300932bee139a
ms.sourcegitcommit: 11d9185437fc819ab41421c0f4fe06aa300b9d28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2017
---
# <a name="known-issues-and-frequently-asked-questions"></a><span data-ttu-id="43d3c-102">Известные проблемы и часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="43d3c-102">Known issues and frequently asked questions</span></span>

<span data-ttu-id="43d3c-103">На этой странице представлены известные проблемы и ответы на часто задаваемые вопросы о SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="43d3c-103">This page is for listing any known issues or to answer any frequently asked questions around SharePoint Framework.</span></span> 

## <a name="known-issues"></a><span data-ttu-id="43d3c-104">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="43d3c-104">Known issues</span></span>

<span data-ttu-id="43d3c-105">**Проблема с сертификатом разработчика в Chrome (версии 58 и новее)**</span><span class="sxs-lookup"><span data-stu-id="43d3c-105">**Dev certificate issue with Chrome (v58-)**</span></span>

- <span data-ttu-id="43d3c-106">*Дата: 28 апреля*</span><span class="sxs-lookup"><span data-stu-id="43d3c-106">*Date - 28th of April*</span></span>
- <span data-ttu-id="43d3c-107">*Обновление: 2 мая*</span><span class="sxs-lookup"><span data-stu-id="43d3c-107">*Updated - 2nd of May*</span></span>

<span data-ttu-id="43d3c-p101">Если вы используете браузер Chrome для разработки, у вас могут возникнуть проблемы с сертификатом разработчика независимо от того, выполняется ли команда `gulp trust-dev-cert`. В Chrome 58 изменилась модель проверки сертификатов, и во время доступа к локальной рабочей области может появиться такое сообщение: "Ваше подключение не защищено".</span><span class="sxs-lookup"><span data-stu-id="43d3c-p101">If you are using Chrome as your development browser, you might have challenges with the developer certificate regardless of executing `gulp trust-dev-cert` command. Chrome has changed its model for certificate validation starting from version 58 and you might see "Your connection is not private" warning when you are accessing the local workbench.</span></span>

<span data-ttu-id="43d3c-p102">Следует обновить пакеты шаблонов Yeoman. Мы обновили логику создания сертификатов в пакете *@microsoft/gulp-core-build-serve*. Для существующих решений вы можете просто удалить эту папку и выполнить `npm install`, чтобы получить обновленный пакет. Кроме того, вам понадобится выполнить команды `untrust-dev-cert` и `trust-dev-cert` на компьютере, чтобы устранить проблему с логикой создания сертификатов.</span><span class="sxs-lookup"><span data-stu-id="43d3c-p102">You should update your Yeoman template packages. We have updated certification creation logic in the *@microsoft/gulp-core-build-serve* package. In existing solutions, you can simply delete this folder and run `npm install` to get the updated package. You will also need to execute `untrust-dev-cert` and `trust-dev-cert` commands in your machine to address the certification creation logic issue.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="43d3c-114">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="43d3c-114">Frequently asked questions</span></span>

<span data-ttu-id="43d3c-115">**Когда в SharePoint Framework будут доступны дополнительные действия и JSLink?**</span><span class="sxs-lookup"><span data-stu-id="43d3c-115">**When will custom actions and JSLink be available in the SharePoint Framework?**</span></span>

- <span data-ttu-id="43d3c-116">*Дата: 6 июня.*</span><span class="sxs-lookup"><span data-stu-id="43d3c-116">*Date - 6th of June*</span></span>

<span data-ttu-id="43d3c-117">Расширения SharePoint с дополнительными возможностями настройки для SharePoint Online теперь доступны в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="43d3c-117">SharePoint Extensions with additional customizations capabilities for the SharePoint Online is now available as Release Candiate release.</span></span> <span data-ttu-id="43d3c-118">Дополнительные сведения о расширениях SharePoint Framework можно найти в соответствующей документации.</span><span class="sxs-lookup"><span data-stu-id="43d3c-118">You can find more details on the SharePoint Framework extensions from our documentation.</span></span>

- [<span data-ttu-id="43d3c-119">Обзор расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="43d3c-119">SharePoint Framework Extensions Overview</span></span>](./extensions/overview-extensions.md)
- [<span data-ttu-id="43d3c-120">Руководство по расширениям SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="43d3c-120">SharePoint Framework Extensions Tutorials</span></span>](./extensions/get-started/build-a-hello-world-extension.md)

<span data-ttu-id="43d3c-121">**Будет ли платформа SharePoint Framework доступна локально?**</span><span class="sxs-lookup"><span data-stu-id="43d3c-121">**Will SharePoint Framework be available in on-premises?**</span></span>

- <span data-ttu-id="43d3c-122">*Дата: 6 июня.*</span><span class="sxs-lookup"><span data-stu-id="43d3c-122">*Date - 6th of June*</span></span>

<span data-ttu-id="43d3c-123">Клиентские веб-части SharePoint Framework на классических страницах выпущены для SharePoint 2016 в составе пакета дополнительных компонентов 2 (FP2).</span><span class="sxs-lookup"><span data-stu-id="43d3c-123">SharePoint Framework client-side web parts will be released to SharePoint 2016 as part of the Feature Pack 2 (FP2).</span></span> <span data-ttu-id="43d3c-124">Мы пока не планируем добавлять возможности SharePoint Framework в SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="43d3c-124">There are no plans currently to provide SharePoint Framework capabilities to SharePoint 2013.</span></span> <span data-ttu-id="43d3c-125">Готового списка возможностей SharePoint Framework, которые будут включены в выпуск SharePoint 2019, нет.</span><span class="sxs-lookup"><span data-stu-id="43d3c-125">There's no specific list of SharePoint Framework capabilities which will be included in the SharePoint 2019 release.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43d3c-126">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="43d3c-126">Additional resources</span></span>
<span data-ttu-id="43d3c-127">Используйте указанные ниже ресурсы, чтобы отправлять отзывы, комментарии и вопросы, касающиеся разработки решений для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="43d3c-127">Please use following resources to provide feedback, comments and questions towards SharePoint engineering.</span></span> 

* [<span data-ttu-id="43d3c-128">Список проблем в репозитории sp-dev-docs на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="43d3c-128">sp-dev-docs GitHub issue list</span></span>](https://github.com/SharePoint/sp-dev-docs/issues)
* [<span data-ttu-id="43d3c-129">Раздел, посвященный разработке решений для SharePoint, на сайте Microsoft Tech Community</span><span class="sxs-lookup"><span data-stu-id="43d3c-129">SharePoint Developer MS Tech Community space</span></span>](https://aka.ms/sppnp-community)
