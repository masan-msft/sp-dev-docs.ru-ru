---
title: "Службы Visio в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ed8c5d12-e17d-4ceb-b195-601c26824370
ms.openlocfilehash: d59e3c6d447327e9ad9444f889f38c24ca21120f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="visio-services-in-sharepoint"></a><span data-ttu-id="1ed7d-102">Службы Visio в SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed7d-102">Visio Services in SharePoint</span></span>
<span data-ttu-id="1ed7d-103">Службы Visio в Microsoft SharePoint позволяет загружать, отображать и программно взаимодействовать с Visio vsdx (en), .vsdm файлы и веб-документов Visio (.vdw) на Microsoft SharePoint и Microsoft SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-103">Visio Services in Microsoft SharePoint enables you to load, display, and interact programmatically with Visio .vsdx, .vsdm files and Visio Web Drawings (.vdw) on Microsoft SharePoint and Microsoft SharePoint Online.</span></span>
## <a name="whats-new-in-visio-services-in-sharepoint"></a><span data-ttu-id="1ed7d-104">Новые возможности служб Visio в SharePoint</span><span class="sxs-lookup"><span data-stu-id="1ed7d-104">What's new in Visio Services in SharePoint</span></span>
<span data-ttu-id="1ed7d-105"><a name="visserv15_WhatsNew"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-105"></span></span>

<span data-ttu-id="1ed7d-106">Службы Visio в Microsoft SharePoint и в Microsoft SharePoint Online включает в себя ряд новых функций, включая поддержку нового формата файлов Microsoft Visio 2013, поддержки для источников данных служб Microsoft Business Connectivity Services (BCS) и программный доступ к комментариев.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-106">Visio Services in Microsoft SharePoint and in Microsoft SharePoint Online includes several new features, including support for the new Microsoft Visio 2013 file format, support for Microsoft Business Connectivity Services (BCS) data sources, and programmatic access to comments.</span></span>
  
    
    

### <a name="new-file-format"></a><span data-ttu-id="1ed7d-107">Новый формат файла</span><span class="sxs-lookup"><span data-stu-id="1ed7d-107">New file format</span></span>
<span data-ttu-id="1ed7d-108"><a name="vis15_WhatsNew_NewFF"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-108"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-p101">Visio 2013 представлен новый формат файла (vsdx (en), на основе Open Packaging Conventions (OPC) standard (ISO 29500, часть 2) и XML-элементы из предыдущих Visio формат XML-файла (.vdx). Это формат ZIP-файл на основе XML, аналогичную форматы файлов, используемые в других приложениях .</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p101">Visio 2013 introduces a new file format (.vsdx), based on the Open Packaging Conventions (OPC) standard (ISO 29500, Part 2) and the XML elements from the previous Visio XML file format (.vdx). It is a zipped, XML-based file format similar to the file formats used in other applications.  </span></span><br/> <span data-ttu-id="1ed7d-p102">С помощью нового формата файлов можно сохранить Visio 2013 документа в библиотеке SharePoint Server или SharePoint Online без необходимости опубликуйте файл как Visio Web рисунка (.vdw). Тем не менее Службы Visio возможность чтения и отображение файлов веб-документа Visio.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p102">With the new file format, you can save a Visio 2013 drawing directly to a SharePoint Server or SharePoint Online library, without having to publish the file as a Visio Web Drawing (.vdw). Even so, Visio Services can still read and display Visio Web Drawing files.  </span></span><br/> <span data-ttu-id="1ed7d-p103">Службы Visio сохраняет возможность отображения в формат веб-документа Visio (.vdw) в браузере. Он теперь также выводит нового Visio документа (vsdx (en) и Visio макросами рисунка (.vsdm) форматы.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p103">Visio Services retains the ability to display the Visio Web Drawing (.vdw) format in the browser. It now also renders the new Visio drawing (.vsdx) and Visio macro-enabled drawing (.vsdm) formats.  </span></span><br/> <span data-ttu-id="1ed7d-p104">Объектная модельECMAScript (JavaScript, JScript)Службы Visio содержит новые API для поддержки новый формат файла:  [Vwa.VwaControl.getDiagramFileType Method](http://msdn.microsoft.com/library/fd8ca95f-a3be-4000-bce8-3aaf1f48148c%28Office.15%29.aspx). Методы возвращает значение из  [Vwa.DiagramFileType Enumeration](http://msdn.microsoft.com/library/dd2f8a5d-a54b-44bd-a458-02efdcba0201%28Office.15%29.aspx) , которое указывает, является ли имя файла, отображаемое в веб-части Visio Web Access (vsdx (en) документа Visio или Visio Web рисунка (.vdw). </span><span class="sxs-lookup"><span data-stu-id="1ed7d-p104">The Visio ServicesECMAScript (JavaScript, JScript) object model contains a new API to support the new file format: the  [Vwa.VwaControl.getDiagramFileType Method](http://msdn.microsoft.com/library/fd8ca95f-a3be-4000-bce8-3aaf1f48148c%28Office.15%29.aspx). The methods returns a value from the  [Vwa.DiagramFileType Enumeration](http://msdn.microsoft.com/library/dd2f8a5d-a54b-44bd-a458-02efdcba0201%28Office.15%29.aspx) that indicates whether the file displayed in the Visio Web Access Web Part is a Visio drawing (.vsdx) or a Visio Web Drawing (.vdw). </span></span><br/> <span data-ttu-id="1ed7d-119">Дополнительные сведения о новом формате Visio 2013 [Introduction to the Visio file format (.vsdx)](http://msdn.microsoft.com/library/69736f40-8f67-46c2-abf6-82dffecb2274%28Office.15%29.aspx)см.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-119">For more information about the new file format in Visio 2013, see  [Introduction to the Visio file format (.vsdx)](http://msdn.microsoft.com/library/69736f40-8f67-46c2-abf6-82dffecb2274%28Office.15%29.aspx).</span></span>  <br/> <span data-ttu-id="1ed7d-120">**Примечание:** Новые файлы Visio (vsdx (en) и .vsdm) отображаются только в растровом формате в Visio Services.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-120">**Note:** The new Visio files (.vsdx and .vsdm) are only displayed in raster format on Visio Services.</span></span> <span data-ttu-id="1ed7d-121">Веб-документов Visio (.vdw) по-прежнему отображаются с помощью Silverlight.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-121">Visio Web Drawings (.vdw) can still be displayed using Silverlight.</span></span>           |
   

### <a name="support-for-business-connectivity-services-bcs-data"></a><span data-ttu-id="1ed7d-122">Поддержка данных Business Connectivity Services (BCS)</span><span class="sxs-lookup"><span data-stu-id="1ed7d-122">Support for Business Connectivity Services (BCS) data</span></span>
<span data-ttu-id="1ed7d-123"><a name="vis15_WhatsNew_BCS"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-123"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-126">Схемы Visio 2013 теперь могут быть подключены к внешним спискам, созданных с помощью Microsoft Business Connectivity Services (BCS) на серверах SharePoint и в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-126">Visio 2013 diagrams can now be connected to external lists created using Microsoft Business Connectivity Services (BCS) on SharePoint servers and in SharePoint Online.</span></span> <span data-ttu-id="1ed7d-127">Службы Visio поддерживают возможность обновления схемы Visio как обновления данных.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-127">Visio Services supports the ability to refresh the Visio diagrams as the data updates.</span></span>  <br/> <span data-ttu-id="1ed7d-128">**Примечание:** Службам Visio не поддерживает SQL, SQL Azure, OLEDC, ODBC и настраиваемые поставщики данных в качестве источников данных в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-128">**Note:** Visio Services does not support SQL, SQL Azure, OLEDC, ODBC, and custom data providers as data sources in SharePoint Online.</span></span>           |
   

### <a name="commenting"></a><span data-ttu-id="1ed7d-129">Комментарии</span><span class="sxs-lookup"><span data-stu-id="1ed7d-129">Commenting</span></span>
<span data-ttu-id="1ed7d-130"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-130"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-p107">Visio 2013 включает в себя новые комментирования framework. Комментарии, теперь могут быть связаны с конкретной формы или страницы. Службы Visio включает в себя интерфейсы API JavaScript для извлечения комментариев из схемы.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p107">Visio 2013 includes a new commenting framework. Comments can now be associated with a particular shape or page. Visio Services includes JavaScript APIs to retrieve the comments from a diagram.  </span></span><br/> <span data-ttu-id="1ed7d-136">Дополнительные сведения о комментирования интерфейсы API в объектной моделиJavaScriptСлужбы Visio видеть темы  [VwaPage.getPageComments Method](http://msdn.microsoft.com/library/d1e7740c-e0fa-4823-b2b6-14551bb84c36%28Office.15%29.aspx) и [VwaShape.getComments Method](http://msdn.microsoft.com/library/fcdec9c2-a503-4315-b048-033cd5ac09dd%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ed7d-136">For more information about the commenting APIs in the Visio ServicesJavaScript object model, see the topics  [VwaPage.getPageComments Method](http://msdn.microsoft.com/library/d1e7740c-e0fa-4823-b2b6-14551bb84c36%28Office.15%29.aspx) and [VwaShape.getComments Method](http://msdn.microsoft.com/library/fcdec9c2-a503-4315-b048-033cd5ac09dd%28Office.15%29.aspx).</span></span>  <br/> |
   

### <a name="expanded-recalculation"></a><span data-ttu-id="1ed7d-137">Пересчет в развернутой</span><span class="sxs-lookup"><span data-stu-id="1ed7d-137">Expanded recalculation</span></span>
<span data-ttu-id="1ed7d-138"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-138"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-p108">Службы Visio теперь можно создать формулы в таблице свойств фигуры. Помимо обновления связанных с данными, Службы Visio можно обновить все фигуры с данными и визуальные элементы, которые зависят от данных. Большинство функций ShapeSheet поддерживаются для пересчета.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p108">Visio Services can now recalculate formulas in the ShapeSheet. In addition to refreshing Data Graphics, Visio Services can refresh all shapes with data and visuals that depend upon data. Most ShapeSheet functions are supported for recalculation.</span></span>  <br/> |
   

### <a name="improved-error-handling"></a><span data-ttu-id="1ed7d-144">Улучшенная обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="1ed7d-144">Improved error handling</span></span>
<span data-ttu-id="1ed7d-145"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-145"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-p109">При возникновении ошибки обновления данных в документе Visio, отображаемые в Службы Visio, отображение теперь будет использоваться Неподвижное изображение диаграммы. Службы Visio также предоставляет более содержательные сведения в сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p109">When a data refresh error occurs in a Visio drawing displayed in Visio Services, the display now falls back to a static image of the diagram. Visio Services also provides more actionable information in error messages.</span></span>  <br/> |
   

### <a name="secure-store-authentication"></a><span data-ttu-id="1ed7d-150">Проверка подлинности службы Secure Store</span><span class="sxs-lookup"><span data-stu-id="1ed7d-150">Secure Store Authentication</span></span>
<span data-ttu-id="1ed7d-151"><a name="vis15_WhatsNew_Commenting"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-151"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-p110">Ранее параметры проверки подлинности для внешних источников данных (базы данных SQL, например) может быть только через служебной программы в Microsoft Excel. С Visio 2013 пользователи теперь могут настраивать их подключением данных схемы непосредственно из клиент Visio, который позволяет источников данных, необходимо обновить в Службы Visio.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p110">Previously, Authentication Settings for external data sources (a SQL database, for example) could only be configured through a utility in Microsoft Excel. With Visio 2013, users can now configure their data connected diagrams directly from the Visio client, which allows data sources to be refreshed in Visio Services.</span></span>  <br/> |
   

## <a name="visio-services-javascript-object-model"></a><span data-ttu-id="1ed7d-156">Модель объектов JavaScript служб Visio</span><span class="sxs-lookup"><span data-stu-id="1ed7d-156">Visio Services JavaScript Object Model</span></span>
<span data-ttu-id="1ed7d-157"><a name="visserv15_JSOM"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-157"></span></span>


|||
|:-----|:-----|
|![Заметка в облачном режиме](../images/mod_icon_incloud.gif)           <br/> ![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-p111">[Vwa Пространства имен](http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx) в объектной моделиJavaScript в Службы Visio предоставляет программный доступ к схем Visio в веб-части Visio Web Access. С помощью объектной модели JavaScript, чтобы воспользоваться данные о схемы, страницы и фигуры. гиперссылки на фигуры; и фигуры, ограничивающих свойства поля. При этом access можно создавать гибридных веб-приложений, выделите фигуры, поместите перекрытий на диаграмме, реагировать на события схемы и мыши и изменения свойств панорамирования и масштабирования окна просмотра.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-p111">The  [Vwa namespace](http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx) in the JavaScript object model in Visio Services gives you programmatic access to Visio drawings displayed in the Visio Web Access Web Part. Using the JavaScript object model, you can access data about diagrams, pages, and shapes; shape hyperlinks; and shape bounding box properties. With this access, you can create mashups that highlight shapes, place overlays on the diagram, respond to diagram and mouse events, and change the panning and zooming properties of the viewport. </span></span><br/> <span data-ttu-id="1ed7d-163">Сведения о добавлении веб-части Visio Web Access на страницу SharePoint, а также программирование этой страницы с помощью JavaScript API-интерфейсы в Visio 2013 содержатся в разделе  [Настройка веб-документов Visio в веб-части Visio Web Access](http://msdn.microsoft.com/ru-ru/library/ff394649.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ed7d-163">For information about adding a Visio Web Access Web Part to a SharePoint page and programming that page by using the JavaScript APIs in Visio 2013, see  [Customizing Visio Web Drawings in the Visio Web Access Web Part](http://msdn.microsoft.com/ru-ru/library/ff394649.aspx).</span></span>  <br/> |
   

## <a name="visio-services-class-library"></a><span data-ttu-id="1ed7d-164">Библиотека классов служб Visio</span><span class="sxs-lookup"><span data-stu-id="1ed7d-164">Visio Services Class Library</span></span>
<span data-ttu-id="1ed7d-165"><a name="visserv15_Mref"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-165"></span></span>


|||
|:-----|:-----|
|![Заметка локального режима](../images/mod_icon_onpremises.gif)|<span data-ttu-id="1ed7d-167">Библиотека классов служб Visio, в пространство имен [Microsoft.Office.Visio.Server](https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx) можно использовать для создания настраиваемых поставщиков данных служб Visio.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-167">You can use the Visio Services class library, in the  [Microsoft.Office.Visio.Server](https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx) namespace, to build custom Visio Services data providers.</span></span> <span data-ttu-id="1ed7d-168">Поставщики данных позволяют программным путем обновления данных, полученных от источников пользовательских данных в схемы Visio 2013, размещенного на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="1ed7d-168">These data providers permit you to programmatically refresh data derived from custom data sources in Visio 2013 diagrams hosted on a SharePoint site.</span></span> <br/> <span data-ttu-id="1ed7d-169">Дополнительные сведения о создании настраиваемого поставщика данных и для работы через в единое решение начала до конца содержатся в разделе  [Создание настраиваемого поставщика данных с помощью служб Visio](http://msdn.microsoft.com/ru-ru/library/ff394595.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ed7d-169">For more information about creating a custom data provider and to work through a complete end-to-end solution, see  [Creating a Custom Data Provider with Visio Services](http://msdn.microsoft.com/ru-ru/library/ff394595.aspx).</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="1ed7d-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="1ed7d-170">Additional Resources</span></span>
<span data-ttu-id="1ed7d-171"><a name="visserv15_Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="1ed7d-171"></span></span>


-  [<span data-ttu-id="1ed7d-172">Microsoft.Office.Visio.Server</span><span class="sxs-lookup"><span data-stu-id="1ed7d-172">Microsoft.Office.Visio.Server</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Visio.Server.aspx)
    
  
-  [<span data-ttu-id="1ed7d-173">Vwa Пространства имен</span><span class="sxs-lookup"><span data-stu-id="1ed7d-173">Vwa namespace</span></span>](http://msdn.microsoft.com/library/b67939fa-d3db-41ff-8864-eabd318ba7c4%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="1ed7d-174">Создание настраиваемого поставщика данных с помощью служб Visio</span><span class="sxs-lookup"><span data-stu-id="1ed7d-174">Creating a Custom Data Provider with Visio Services</span></span>](http://msdn.microsoft.com/ru-ru/library/ff394595.aspx)
    
  
-  [<span data-ttu-id="1ed7d-175">Настройка веб-документов Visio в веб-части Visio Web Access</span><span class="sxs-lookup"><span data-stu-id="1ed7d-175">Customizing Visio Web Drawings in the Visio Web Access Web Part</span></span>](http://msdn.microsoft.com/ru-ru/library/ff394649.aspx)
    
  
-  [<span data-ttu-id="1ed7d-176">New in Visio for developers</span><span class="sxs-lookup"><span data-stu-id="1ed7d-176">New in Visio for developers</span></span>](http://msdn.microsoft.com/library/7e3fb858-0ab8-bd2e-217c-c85b10d79785%28Office.15%29.aspx)
    
  
- <span data-ttu-id="1ed7d-177">Список новых функций в vis15short для конечных пользователей в разделе  [новые возможности Visio](http://office.com/redir/HA102749364.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ed7d-177">For a list of new features in vis15short for end users, see  [What's new in Visio](http://office.com/redir/HA102749364.aspx).</span></span>
    
  
