---
title: "Средства и среды для разработки надстроек SharePoint"
description: "Узнайте, как создать среду разработки надстроек SharePoint на сайте SharePoint Online или в локальной ферме."
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 62690d8c3e0949129dd09b57e772911333aa99fd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a>Средства и среды для разработки надстроек SharePoint

Существует два основных шаблона сред для разработки надстроек SharePoint. Веб-сайт SharePoint для тестирования и разработки может находиться:

-  **на веб-сайте SharePoint Online в подписке Office 365.** Как правило, среда Visual Studio устанавливается на локальном компьютере, но ее также можно развернуть в облаке;

-  **в локальной ферме SharePoint с одним сервером.** Visual Studio устанавливается на том же компьютере.
 
Примите во внимание следующее:

- Практически любую создаваемую надстройку можно развернуть в SharePoint Online или локальных фермах SharePoint независимо от типа используемой среды. В целом, надстройки, которые невозможно развернуть в SharePoint Online, также невозможно разрабатывать с помощью этой среды. Например, это относится к надстройкам, требующим [разрешения уровня "Полный доступ"](add-in-permissions-in-sharepoint.md) и использующим [систему авторизации с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization.md).

- Вы можете разрабатывать надстройки, размещаемые как в SharePoint, так и у поставщика, независимо от типа используемой среды.

- У вас могут быть как локальные тестовые сайты, так и тестовые сайты SharePoint Online.

- Учитывая все вышеизложенное, можно считать оба варианта одинаково простыми в настройке.
    
**Руководство по созданию среды SharePoint Online** с помощью подписки SharePoint Online, которую можно использовать для разработки, см. в статье [Создание сайта разработчика с использованием имеющейся подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).
 
**Руководство по созданию локальной среды** см. в статье [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md).
 
> [!NOTE]
> В этой статье рассматриваются только среды для разработки надстроек SharePoint. Если планируется разрабатывать решения для ферм, см. статью [Настройка общей среды разработки для SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). 

> Если планируется разрабатывать решения обоих типов, начните с последней статьи, а затем ознакомьтесь со статьей [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md), где представлены дополнительные инструкции по разработке надстроек SharePoint.


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Надстройки SharePoint](sharepoint-add-ins.md)
- [Создание надстроек SharePoint в Visual Studio](create-sharepoint-add-ins-in-visual-studio.md)
    
 

