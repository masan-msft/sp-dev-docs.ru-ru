---
title: "Виртуальные каталоги в решениях SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c26c4160-31be-4358-89cf-082b8a1e6a6c
ms.openlocfilehash: 93be71d76718e12439ea7d9d359639a139dfb89d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="virtual-directories-in-sharepoint-solutions"></a>Виртуальные каталоги в решениях SharePoint
Сведения о влиянии изменения в систему виртуального каталога на создание решений фермы SharePoint.
## <a name="make-your-solutions-compatible-with-the-new-ui-mode-system"></a>Сделать решений совместимым с новой системы режим пользовательского интерфейса

Когда с помощью Microsoft SharePoint 2010 Software Development Kit (SDK), но разработки для SharePoint, изменяется в системе виртуального каталога, который необходимо учитывать при работе. Изменение является побочные эффекты компонента SharePoint, которая позволяет семейства веб-сайтов в SharePoint 2010 или режиме SharePoint. Режимы иногда называются orUI уровни совместимости версий. Поиск файлов в виртуальные папки `_layouts` или `_controltemplates`, SharePoint необходимо использовать версию файлов в папке % ProgramFiles %\\общие файлы\\Microsoft Shared\\веб-серверных расширений\\15\\ (иногда называемую кусте 15) или в соответствующем 14 кусте, в зависимости от режима семейства веб-сайтов. Добавляет SharePoint «/ 15» в виртуальном каталоге сразу после имя виртуального каталога, чтобы сообщить, что следует использовать файлы SharePoint. Отсутствие дополнительные строки указывает, следует ли использовать файлы SharePoint 2010.
  
    
    
В этом новой системы влияет на вам при разработке решений SharePoint и приложения, особенно при использовании пакета SDK SharePoint 2010. В любой SharePoint Add-in (который выполнить только в режиме SharePoint) и в любой решение SharePoint, которые только будут использоваться в семейств веб-сайтов, на которых выполняется в режиме SharePoint, необходимо добавить «/ 15» выберите вариант все `_layouts` и `_controltemplates` виртуального пути можно создать e решения или приложения. (если только с указанием пути ASPX-файла), даже если эта строка не отображается в любой инструкции, чтение в пакет SDK для SharePoint 2010. Например, если пакет SDK для SharePoint 2010, этот параметр можно воспользоваться `~/_layouts/images/myimage.png`, следует использовать `~/_layouts/15/images/myimage.png` при разработке для SharePoint.
  
    
    
Если вам потребуется сделать совместимым с семейств веб-сайтов из любого из режима решения, ветвление логику для определения режима в текущем семействе сайтов и создать виртуальный путь к соответствующим образом. Свойство  [CompatibilityLevel](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPSite.CompatibilityLevel.aspx) , которое возможности также доступны на всех клиентских объектных моделей SharePoint и интерфейс REST,  одну позицию, где код можно проверить, для режима. Класс [SPUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPUtility.aspx) также имеет несколько новых свойств для помощи в управлении уровень совместимости имеющихся. Они не доступны в клиентской объектной модели. И, наконец существует несколько элементов управления в SharePoint, которые предоставляют свойство **UIVersion**, которое кода можно также использовать для поиска текущий уровень совместимости.
  
    
    

> **Примечание:** Если файл виртуальный путь *.aspx, SharePoint автоматическое определение режим в текущем семействе сайтов и возврата файла из соответствующего куста. Поэтому необходимо вставить «/ 15» в виртуальный путь. 
  
    
    


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Создавайте решения фермы в SharePoint](build-farm-solutions-in-sharepoint.md)
    
  
-  [Планирование развертывания решений фермы для SharePoint](http://blogs.technet.com/b/mspfe/archive/2013/02/04/planning-deployment-of-farm-solutions-for-sharepoint.aspx)
    
  
-  [SPUtility properties](http://msdn.microsoft.com/library/Properties.T:Microsoft.SharePoint.Utilities.SPUtility.aspx)
    
  

