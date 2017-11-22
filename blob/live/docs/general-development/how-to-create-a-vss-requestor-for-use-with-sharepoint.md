---
title: "Создание опросчика VSS для использования с SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 63b3145b-ece2-4acf-b58a-fd8b50303030
ms.openlocfilehash: f2dbb3c94cc8196f24cbbb48862116854cc47044
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-a-vss-requestor-for-use-with-sharepoint"></a><span data-ttu-id="5ec4f-102">Как: создание опросчика VSS для использования с SharePoint</span><span class="sxs-lookup"><span data-stu-id="5ec4f-102">How to: Create a VSS requestor for use with SharePoint</span></span>
 <span data-ttu-id="5ec4f-103">**Сводка:** Сведения о создании запросившей для использования с помощью модуля записи службы теневого копирования томов (VSS) для Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5ec4f-103">**Summary:** Learn about how to create a requestor for use with the Volume Shadow Copy Service (VSS) writer for Microsoft SharePoint.</span></span>
## <a name="writing-a-requestor"></a><span data-ttu-id="5ec4f-104">Создание опросчика</span><span class="sxs-lookup"><span data-stu-id="5ec4f-104">Writing a requestor</span></span>

<span data-ttu-id="5ec4f-p101">Процесс создания опросчика для резервного копирования и восстановления SharePoint Foundation с помощью службы теневого копирования ТОМОВ это же, как для написания опросчика для любого другого основе приложения как Microsoft SQL Server или Microsoft Exchange Server. Разработчики приложений резервного копирования следует выполните действия, описанные в  [Тома теневого копирования службы обзор](http://msdn.microsoft.com/en-us/library/aa384649%28VS.85%29.aspx) и [Справка по API тома теневой копии](http://msdn.microsoft.com/en-us/library/aa384648%28VS.85%29.aspx) для создания приложений, которые могут правильно резервного копирования и восстановления данных SharePoint Foundation .</span><span class="sxs-lookup"><span data-stu-id="5ec4f-p101">The process of writing a requestor for backing up and restoring SharePoint Foundation by using VSS is the same as that for writing a requestor for any other Windows-based application such as Microsoft SQL Server or Microsoft Exchange Server. Developers of backup applications should follow the procedures outlined in the  [Volume Shadow Copy Service Overview](http://msdn.microsoft.com/en-us/library/aa384649%28VS.85%29.aspx) and [Volume Shadow Copy API Reference](http://msdn.microsoft.com/en-us/library/aa384648%28VS.85%29.aspx) to build applications that can properly back up and restore SharePoint Foundation data.</span></span>
  
    
    

## <a name="next-steps"></a><span data-ttu-id="5ec4f-107">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ec4f-107">Next steps</span></span>
<span data-ttu-id="5ec4f-108"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="5ec4f-108"></span></span>

<span data-ttu-id="5ec4f-109">Узнайте, как использовать для резервного копирования и восстановления SharePoint и приложений поиска и индексов инициатора запроса:</span><span class="sxs-lookup"><span data-stu-id="5ec4f-109">Learn how to use the requestor to back up and restore SharePoint and search applications and indexes:</span></span>
  
    
    

-  [<span data-ttu-id="5ec4f-110">Как: резервное копирование и восстановление SharePoint с использованием модуля запросов VSS</span><span class="sxs-lookup"><span data-stu-id="5ec4f-110">How to: Back up and restore SharePoint using a VSS requestor</span></span>](how-to-back-up-and-restore-sharepoint-using-a-vss-requestor.md)
    
  
-  [<span data-ttu-id="5ec4f-111">Как: резервное копирование и восстановление приложения-службы поиска в SharePoint с использованием служба теневого копирования ТОМОВ</span><span class="sxs-lookup"><span data-stu-id="5ec4f-111">How to: Back up and restore a search service application in SharePoint using VSS</span></span>](how-to-back-up-and-restore-a-search-service-application-in-sharepoint-using.md)
    
  

## <a name="additional-resources"></a><span data-ttu-id="5ec4f-112">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ec4f-112">Additional resources</span></span>
<span data-ttu-id="5ec4f-113"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5ec4f-113"></span></span>


-  [<span data-ttu-id="5ec4f-114">Общие сведения о SharePoint и службы теневого копирования томов</span><span class="sxs-lookup"><span data-stu-id="5ec4f-114">Overview of SharePoint and the Volume Shadow Copy Service</span></span>](overview-of-sharepoint-and-the-volume-shadow-copy-service.md)
    
  
