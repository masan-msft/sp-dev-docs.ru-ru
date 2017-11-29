---
title: "Обработка SharePoint Online регулирования с помощью экспоненциальное пассивный режим"
ms.date: 11/03/2017
ms.openlocfilehash: 5fe327f1d80ba38c67e82bfa82f4743c13e65510
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="handle-sharepoint-online-throttling-by-using-exponential-back-off"></a><span data-ttu-id="078a5-102">Обработка SharePoint Online регулирования с помощью экспоненциальное пассивный режим</span><span class="sxs-lookup"><span data-stu-id="078a5-102">Handle SharePoint Online throttling by using exponential back off</span></span>

<span data-ttu-id="078a5-103">Узнайте, как обрабатывать регулирования в SharePoint Online с помощью метода экспоненциальное отсрочки.</span><span class="sxs-lookup"><span data-stu-id="078a5-103">Learn how to handle throttling in SharePoint Online by using the exponential back-off technique.</span></span> 
    
<span data-ttu-id="078a5-104">_**Применимо к:** Office 365 | SharePoint Online | SharePoint Server 2013_</span><span class="sxs-lookup"><span data-stu-id="078a5-104">_**Applies to:** Office 365 | SharePoint Online | SharePoint Server 2013_</span></span>

<span data-ttu-id="078a5-105">SharePoint Online с помощью регулирования запретить пользователям чрезмерное потребление ресурсов.</span><span class="sxs-lookup"><span data-stu-id="078a5-105">SharePoint Online uses throttling to prevent users from over-consuming resources.</span></span> <span data-ttu-id="078a5-106">Когда пользователь запускает REST или CSOM код, который превышает ограничения на использование, SharePoint Online регулировки все дополнительные запросы от пользователя на определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="078a5-106">When a user runs CSOM or REST code that exceeds usage limits, SharePoint Online throttles any further request from the user for a period of time.</span></span> 
    
<span data-ttu-id="078a5-107">Пример кода [Core.Throttling](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) в [Office 365 для разработчиков шаблонов и рекомендациям репозитория](https://github.com/SharePoint/PnP) показано, как реализовать экспоненциальное пассивный способ обработки регулирования в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="078a5-107">The [Core.Throttling](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) code sample in the [Office 365 Developer Patterns and Practices repository](https://github.com/SharePoint/PnP) shows how to implement the exponential back off technique to handle throttling in SharePoint Online.</span></span> <span data-ttu-id="078a5-108">При получения ограничением в SharePoint Online, экспоненциальное пассивный метод ожидает постепенно длительных периодов времени перед повторным выполнением кода, снижение скорости.</span><span class="sxs-lookup"><span data-stu-id="078a5-108">When you get throttled in SharePoint Online, the exponential back off technique waits progressively longer periods of time before retrying the code that was throttled.</span></span>
    
<span data-ttu-id="078a5-109">Дополнительные сведения о регулирования в SharePoint Online (например, причины, ограничения и т. п.) и описание образца кода Core.Throttling можно [как: избежать получения регулирование или заблокированные в SharePoint Online](https://msdn.microsoft.com/library/office/dn889829.aspx).</span><span class="sxs-lookup"><span data-stu-id="078a5-109">For more information about throttling in SharePoint Online (for example, causes, limits, and so on), and an explanation of the Core.Throttling code sample, see [How to: Avoid getting throttled or blocked in SharePoint Online](https://msdn.microsoft.com/library/office/dn889829.aspx).</span></span> 

<span data-ttu-id="078a5-110">Кроме того в образце [ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs) извлечь метод расширения ExecuteQueryImplementation.</span><span class="sxs-lookup"><span data-stu-id="078a5-110">Also, in the [ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs) sample, check out the ExecuteQueryImplementation extension method.</span></span> <span data-ttu-id="078a5-111">ExecuteQueryImplementation включен в [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core).</span><span class="sxs-lookup"><span data-stu-id="078a5-111">ExecuteQueryImplementation is included in [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core).</span></span>    

## <a name="additional-resources"></a><span data-ttu-id="078a5-112">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="078a5-112">Additional resources</span></span>
<span data-ttu-id="078a5-113"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="078a5-113"></span></span>

-  [<span data-ttu-id="078a5-114">Руководство по решениям</span><span class="sxs-lookup"><span data-stu-id="078a5-114">Solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="078a5-115">Пример ClientContextExtensions.cs</span><span class="sxs-lookup"><span data-stu-id="078a5-115">ClientContextExtensions.cs sample</span></span>](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs)
    
-  [<span data-ttu-id="078a5-116">Как: избежать получения регулирование или заблокированные в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="078a5-116">How to: Avoid getting throttled or blocked in SharePoint Online</span></span>](https://msdn.microsoft.com/library/office/dn889829.aspx)
