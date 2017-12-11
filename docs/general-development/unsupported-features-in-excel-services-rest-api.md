---
title: "Неподдерживаемые функции интерфейса API REST служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 4139901f-255b-4556-b8c8-3d986a07c587
ms.openlocfilehash: 1e8bf0ba8947391e0479aded0086a8c836ce38bb
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="unsupported-features-in-excel-services-rest-api"></a><span data-ttu-id="b346b-102">Неподдерживаемые функции интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="b346b-102">Unsupported Features in Excel Services REST API</span></span>

<span data-ttu-id="b346b-103">Первая версия Службы Excel API-Интерфейс REST не поддерживает все возможности Excel.</span><span class="sxs-lookup"><span data-stu-id="b346b-103">The first version of the Excel Services REST API does not support every Excel feature.</span></span> 
  
> [!NOTE] 
> <span data-ttu-id="b346b-104">API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="b346b-104">The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="b346b-105">Для учетных записей Office 365 для образования, Office 365 бизнес и Office 365 корпоративный используйте REST API Excel, входящие в состав конечной точки [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
).</span><span class="sxs-lookup"><span data-stu-id="b346b-105">For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


<span data-ttu-id="b346b-106">Ниже приведен неполный список некоторых наиболее важные функциональные возможности, которые в настоящее время не поддерживаются или работаете в Службы Excel API-Интерфейс REST:</span><span class="sxs-lookup"><span data-stu-id="b346b-106">Following is a partial list of some of the more important features that are currently not supported or working in the Excel Services REST API:</span></span>
  
    
    


- <span data-ttu-id="b346b-p102">**Плавающее диаграмм.** Если диапазон содержит диаграммы и запросить диапазон через REST, вы получаете только диапазон.</span><span class="sxs-lookup"><span data-stu-id="b346b-p102">**No floating charts.** If a range contains a chart, and you request the range through REST, you get only the range.</span></span>
    
  
- <span data-ttu-id="b346b-p103">**Не спарклайны без значков условного форматирования.** В настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b346b-p103">**No sparklines, no icon conditional formatting.** Currently not supported.</span></span>
    
  
- <span data-ttu-id="b346b-p104">**Не пиксель идеальное с EWA.** HTML-код, который создает REST очень приближается к завершению, Веб-клиент Excel HTML-код создает. Тем не менее, Службы Excel API-Интерфейс REST не удается получить доступ к всех каскадных таблиц стилей (CSS) можно получить доступ к элементам, Веб-клиент Excel. Службы Excel API-Интерфейс REST возвращает фрагмент HTML-кода. HTML-фрагмента должны быть автономными.</span><span class="sxs-lookup"><span data-stu-id="b346b-p104">**Not pixel-perfect with EWA.** The HTML that REST produces is very close to the HTML that Excel Web Access produces. However, the Excel Services REST API cannot access all the Cascading Style Sheets (CSS) elements that Excel Web Access can access. The Excel Services REST API returns an HTML fragment. The HTML fragment must be self-contained.</span></span>
    
  
- <span data-ttu-id="b346b-p105">**Нет различий в таблицах.** При запросе таблицы как Atom ли заголовок столбца, общее или общие данные, ячейки или данных нет нет различий, внесенные в таблице. То есть нет различий, который определяет, является ли ячейки или данные заголовка, всего или только общие данные. Все ячейки таблицы во всей таблицы равноценны.</span><span class="sxs-lookup"><span data-stu-id="b346b-p105">**No distinction in tables.** When a table is requested as Atom to see whether the cell or data is a column head, a total or general data, there is no distinction made in the table. That is, there is no distinction that specifies whether a cell or data is a header, a total or just general data. All table cells throughout a table are treated equally.</span></span>
    
  
- <span data-ttu-id="b346b-p106">**Ограничения на размер URL-адреса.** URL-адрес размер ограничен примерно 2000 символов. Это означает, что при наличии большое число параметров в книге вы не можно задать все из них. Это особенно, если книга находится глубоко в структуре папок.</span><span class="sxs-lookup"><span data-stu-id="b346b-p106">**URL size limits.** URL size is limited to approximately 2000 characters. This means that, if you have a large number of parameters in a workbook, you may not be able to set all of them. This is especially so if the workbook is located deep in a folder structure.</span></span>
    
  
- <span data-ttu-id="b346b-p107">**Специальные символы.** Знаки, такие как «?» и «#» не поддерживаются. Правильность ссылок на имена листов, которые содержат специальные символы, основная рекомендация «Просмотр клиента Excel» при обращении формулу для таблицы с помощью специальных символов и следуйте этого примера.</span><span class="sxs-lookup"><span data-stu-id="b346b-p107">**Special characters.** Characters like "?" and "#" are unsupported. To correctly reference sheet names that contain special characters, the basic guideline is "see what the Excel client does" when referencing a formula to a sheet with special characters and follow that example.</span></span>
    
  

