---
title: "Обработка SharePoint Online регулирования с помощью экспоненциальное пассивный режим"
ms.date: 11/03/2017
ms.openlocfilehash: 5fe327f1d80ba38c67e82bfa82f4743c13e65510
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="handle-sharepoint-online-throttling-by-using-exponential-back-off"></a>Обработка SharePoint Online регулирования с помощью экспоненциальное пассивный режим

Узнайте, как обрабатывать регулирования в SharePoint Online с помощью метода экспоненциальное отсрочки. 
    
_**Применимо к:** Office 365 | SharePoint Online | SharePoint Server 2013_

SharePoint Online с помощью регулирования запретить пользователям чрезмерное потребление ресурсов. Когда пользователь запускает REST или CSOM код, который превышает ограничения на использование, SharePoint Online регулировки все дополнительные запросы от пользователя на определенный период времени. 
    
Пример кода [Core.Throttling](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) в [Office 365 для разработчиков шаблонов и рекомендациям репозитория](https://github.com/SharePoint/PnP) показано, как реализовать экспоненциальное пассивный способ обработки регулирования в SharePoint Online. При получения ограничением в SharePoint Online, экспоненциальное пассивный метод ожидает постепенно длительных периодов времени перед повторным выполнением кода, снижение скорости.
    
Дополнительные сведения о регулирования в SharePoint Online (например, причины, ограничения и т. п.) и описание образца кода Core.Throttling можно [как: избежать получения регулирование или заблокированные в SharePoint Online](https://msdn.microsoft.com/library/office/dn889829.aspx). 

Кроме того в образце [ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs) извлечь метод расширения ExecuteQueryImplementation. ExecuteQueryImplementation включен в [OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core).    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Пример ClientContextExtensions.cs](https://github.com/SharePoint/PnP/blob/dev/Samples/Core.Throttling/Core.Throttling/ClientContextExtensions.cs)
    
-  [Как: избежать получения регулирование или заблокированные в SharePoint Online](https://msdn.microsoft.com/library/office/dn889829.aspx)
