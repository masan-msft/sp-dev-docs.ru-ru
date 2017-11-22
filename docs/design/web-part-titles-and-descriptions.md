---
title: "Заголовки и описания веб-частей SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: e559b4c0cb4798919e51d870e6efb463d1caed34
ms.sourcegitcommit: 1b295a186814ca6ab13dda1a17e34dc69a61d81e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="titles-and-descriptions-for-sharepoint-web-parts"></a><span data-ttu-id="0a208-102">Заголовки и описания веб-частей SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a208-102">Titles and descriptions for SharePoint web parts</span></span>

<span data-ttu-id="0a208-103">Вы можете добавлять заголовки и описания к веб-частям, чтобы пользователям было легче понять их назначение.</span><span class="sxs-lookup"><span data-stu-id="0a208-103">You can add titles and descriptions to web parts to help users understand their purpose.</span></span> <span data-ttu-id="0a208-104">Это полезно в тех случаях, когда страница содержит множество различных веб-частей.</span><span class="sxs-lookup"><span data-stu-id="0a208-104">This is helpful when a page contains a range of web parts.</span></span> <span data-ttu-id="0a208-105">Некоторым веб-частям (например, веб-частям изображений) заголовок может быть не нужен, но до или после области контента может потребоваться описание.</span><span class="sxs-lookup"><span data-stu-id="0a208-105">Some web parts (like image web parts) might not need a title, but might need a description before or after the content area.</span></span> <span data-ttu-id="0a208-106">Не рассчитывайте, что пользователи поймут контекст веб-части без заголовка или описания либо добавят их самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="0a208-106">Don't assume that users will understand the context of the web part without either a title or a description, and don't assume that users will include titles or descriptions themselves.</span></span> 
 
<span data-ttu-id="0a208-107">Один из вариантов — подключить заголовок и описание к свойствам конфигурации веб-части.</span><span class="sxs-lookup"><span data-stu-id="0a208-107">One option is to connect the title and description to the configuration properties of your web part.</span></span> <span data-ttu-id="0a208-108">Благодаря этому веб-части будут изначально заполнены контентом, соответствующим конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0a208-108">This ensures that your web parts are prepopulated with content that makes the most sense based on the configuration.</span></span> 
 
<span data-ttu-id="0a208-109">Например, если у вас есть веб-часть, запрашивающая библиотеку документов с учетом недавно добавленных элементов, то по умолчанию можно использовать заголовок "Последние документы".</span><span class="sxs-lookup"><span data-stu-id="0a208-109">For example, if you have a web part that queries a document library based on recently added items, you might want to use "Recent documents" for the default title.</span></span>

![Веб-часть с выделенными заголовком и описанием](../images/design-web-part-title-01.png)


<span data-ttu-id="0a208-111">Как для заголовка, так и для описания автор страницы может переопределять стандартный замещающий текст и настраивать отображение в соответствии с создаваемой страницей.</span><span class="sxs-lookup"><span data-stu-id="0a208-111">For both the title and description, the author of the page can override the default placeholder text and customize them based on what makes the most sense for the page they're creating.</span></span> 

![Пользовательский текст в полях заголовка и описания веб-части](../images/design-web-part-title-02.png)