---
title: "Обзор расширений SharePoint Framework (SPFx)"
description: "Используйте расширения SPFx, чтобы настроить области уведомлений, панели инструментов, представления данных списков и другие аспекты SharePoint."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: ad06c2cda5bd6b3ad21049164a58b70cc9dbf93d
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="overview-of-sharepoint-framework-extensions"></a><span data-ttu-id="45ff6-103">Обзор расширений SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="45ff6-103">Overview of SharePoint Framework Extensions</span></span>

<span data-ttu-id="45ff6-104">Используя расширения SharePoint Framework (SPFx), можно сделать SharePoint удобнее для пользователей.</span><span class="sxs-lookup"><span data-stu-id="45ff6-104">You can use SharePoint Framework (SPFx) Extensions to extend the SharePoint user experience.</span></span> <span data-ttu-id="45ff6-105">Используя расширения SharePoint Framework, можно настроить области уведомлений, панели инструментов, представления данных списков и другие аспекты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="45ff6-105">With SharePoint Framework Extensions, you can customize more facets of the SharePoint experience, including notification areas, toolbars, and list data views.</span></span> <span data-ttu-id="45ff6-106">Расширения SharePoint Framework доступны во всех клиентах Office 365 для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="45ff6-106">SharePoint Framework Extensions are available in all Office 365 tenants for production usage.</span></span> 

> [!NOTE] 
> <span data-ttu-id="45ff6-107">Вы можете получить подписку разработчиков приложений для Office 365, приняв участие в [программе для разработчиков приложений для Office 365](http://dev.office.com/devprogram).</span><span class="sxs-lookup"><span data-stu-id="45ff6-107">You can get a free Office 365 developer tenant when you subscribe to the [Office 365 Developer Program](http://dev.office.com/devprogram).</span></span>

<span data-ttu-id="45ff6-p102">Расширения SharePoint Framework позволяют дополнять пользовательский интерфейс SharePoint на современных страницах и в библиотеках документов, используя знакомые библиотеки и средства SharePoint Framework для клиентской разработки. SharePoint Framework включает три новых типа расширений:</span><span class="sxs-lookup"><span data-stu-id="45ff6-p102">SharePoint Framework Extensions enable you to extend the SharePoint user experience within modern pages and document libraries, while using the familiar SharePoint Framework tools and libraries for client-side development. Specifically, the SharePoint Framework includes three new extension types:</span></span>

- <span data-ttu-id="45ff6-110">**Настройщики заполнителей**.</span><span class="sxs-lookup"><span data-stu-id="45ff6-110">**Application Customizers**.</span></span> <span data-ttu-id="45ff6-111">Позволяют добавлять скрипты на страницу, а также изменять стандартные заполнители, добавляя собственные элементы HTML.</span><span class="sxs-lookup"><span data-stu-id="45ff6-111">Adds scripts to the page, and accesses well-known HTML element placeholders and extends them with custom renderings.</span></span>
- <span data-ttu-id="45ff6-112">**Настройщики полей**.</span><span class="sxs-lookup"><span data-stu-id="45ff6-112">**Field Customizers**.</span></span> <span data-ttu-id="45ff6-113">Позволяют настраивать отображение данных в полях списка.</span><span class="sxs-lookup"><span data-stu-id="45ff6-113">Provides modified views to data for fields within a list.</span></span>
- <span data-ttu-id="45ff6-114">**Наборы команд**.</span><span class="sxs-lookup"><span data-stu-id="45ff6-114">**Command Sets**.</span></span> <span data-ttu-id="45ff6-115">Позволяют добавлять действия на панели команд SharePoint, а также внедрять действия с помощью встроенного клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="45ff6-115">Extends the SharePoint command surfaces to add new actions, and provides client-side code that you can use to implement behaviors.</span></span>

<span data-ttu-id="45ff6-p106">Помимо проектов plainJS, вы можете создавать расширения на таких распространенных платформах создания скриптов, как AngularJS и React. Например, вы можете использовать React вместе с компонентами из Office UI Fabric React, чтобы создавать решения на основе тех же компонентов, которые используются в Office 365.</span><span class="sxs-lookup"><span data-stu-id="45ff6-p106">You can build extensions alongside common scripting frameworks, such as AngularJS and React, in addition to plain JavaScript projects. For example, you can use React along with components from Office UI Fabric React to create experiences based on the same components used in Office 365.</span></span>

> [!NOTE]
> <span data-ttu-id="45ff6-118">Мы знаем о проблеме с поддержкой расширений библиотеки и списков на классических страницах.</span><span class="sxs-lookup"><span data-stu-id="45ff6-118">There is a known bug with list and library extension support in the classic experiences.</span></span> <span data-ttu-id="45ff6-119">Сейчас их можно использовать только в контексте современных сайтов группы.</span><span class="sxs-lookup"><span data-stu-id="45ff6-119">These only work currently in context of modern team sites, also known as group associated team sites.</span></span> <span data-ttu-id="45ff6-120">Мы работаем над устранением этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="45ff6-120">Work is being done to address this issue.</span></span> 

## <a name="get-started"></a><span data-ttu-id="45ff6-121">Начало работы</span><span class="sxs-lookup"><span data-stu-id="45ff6-121">Get started</span></span>

1. <span data-ttu-id="45ff6-122">Если вы не устанавливали SharePoint Framework, выполните действия [по настройке среды разработки](../set-up-your-development-environment.md).</span><span class="sxs-lookup"><span data-stu-id="45ff6-122">If you haven't installed the SharePoint Framework, follow the steps to [Set up your development environment](../set-up-your-development-environment.md).</span></span>

2. <span data-ttu-id="45ff6-123">Когда установите SharePoint Framework, выполните следующую команду, чтобы обновить шаблоны Yeoman до последней версии:</span><span class="sxs-lookup"><span data-stu-id="45ff6-123">After you install the SharePoint Framework, run the following command to update your Yeoman templates with the latest version:</span></span>

    ```
    npm install -g @microsoft/generator-sharepoint
    ```

3. <span data-ttu-id="45ff6-124">Далее вы можете [создать свое первое расширение SharePoint Framework (Hello World, часть 1)](get-started/build-a-hello-world-extension.md).</span><span class="sxs-lookup"><span data-stu-id="45ff6-124">Next, you can [Build your first SharePoint Framework Extension (Hello World part 1)](get-started/build-a-hello-world-extension.md).</span></span>

## <a name="stay-up-to-date"></a><span data-ttu-id="45ff6-125">Своевременное обновление</span><span class="sxs-lookup"><span data-stu-id="45ff6-125">Stay up to date</span></span>
<span data-ttu-id="45ff6-126">Чтобы следить за улучшениями SharePoint Framework, в том числе за обновлением расширений, используйте следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="45ff6-126">To keep track of improvements to the SharePoint Framework, including updates to extensions, see the following:</span></span>

* <span data-ttu-id="45ff6-127">[@SharePoint](https://twitter.com/sharepoint) и [@OfficeDev](https://twitter.com/officedev) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="45ff6-127">[@SharePoint](https://twitter.com/sharepoint) and [@OfficeDev](https://twitter.com/officedev) on Twitter</span></span>
* <span data-ttu-id="45ff6-128">[Блог для разработчиков решений для Office](http://dev.office.com/blogs).</span><span class="sxs-lookup"><span data-stu-id="45ff6-128">[Office Developer Blog](http://dev.office.com/blogs)</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="45ff6-129">Предоставление отзывов</span><span class="sxs-lookup"><span data-stu-id="45ff6-129">Provide feedback</span></span> 
<span data-ttu-id="45ff6-130">Предлагаем отправить отзывы об общедоступном выпуске SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="45ff6-130">We invite you to give us your feedback on the SharePoint Framework General Availability release.</span></span> <span data-ttu-id="45ff6-131">Отправить отзывы непосредственно команде разработчиков SharePoint можно с помощью таких ресурсов:</span><span class="sxs-lookup"><span data-stu-id="45ff6-131">You can use the following resources to provide feedback directly to the SharePoint engineering team:</span></span>

- <span data-ttu-id="45ff6-132">[Список проблем, касающихся репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues) (вопросы, проблемы и комментарии).</span><span class="sxs-lookup"><span data-stu-id="45ff6-132">[sp-dev-docs repository issue list](https://github.com/SharePoint/sp-dev-docs/issues) - Questions, issues, and comments.</span></span>
* <span data-ttu-id="45ff6-133">[SharePoint StackExchange](http://sharepoint.stackexchange.com/) (используйте теги [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) и [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/)).</span><span class="sxs-lookup"><span data-stu-id="45ff6-133">[SharePoint StackExchange](http://sharepoint.stackexchange.com/) - Tag with [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/), and [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/).</span></span>
* <span data-ttu-id="45ff6-134">[SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev) (группа в сообществе технических специалистов Майкрософт, в которой участвуют разработчики решений для SharePoint).</span><span class="sxs-lookup"><span data-stu-id="45ff6-134">[SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev) - Microsoft Tech Community group.</span></span>
* <span data-ttu-id="45ff6-135">[UserVoice разработчиков SharePoint](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform) (здесь можно предложить добавить новые возможности и функции).</span><span class="sxs-lookup"><span data-stu-id="45ff6-135">[SharePoint Developer UserVoice](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform) - Request new capabilities and features.</span></span>


## <a name="see-also"></a><span data-ttu-id="45ff6-136">См. также</span><span class="sxs-lookup"><span data-stu-id="45ff6-136">See also</span></span>

- [<span data-ttu-id="45ff6-137">Обзор платформы SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="45ff6-137">Overview of the SharePoint Framework</span></span>](../sharepoint-framework-overview.md)
- [<span data-ttu-id="45ff6-138">Средства разработки и библиотеки платформы SharePoint Framework</span><span class="sxs-lookup"><span data-stu-id="45ff6-138">SharePoint Framework development tools and libraries</span></span>](../tools-and-libraries.md)
