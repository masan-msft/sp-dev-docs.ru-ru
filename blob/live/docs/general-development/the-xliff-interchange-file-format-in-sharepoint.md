---
title: "Формат файла обмена XLIFF в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 660c0f07-7030-4576-957e-b9f2cd0fa895
ms.openlocfilehash: fb3a0454d972fa54a99bff693b97a716ec3f95ce
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="the-xliff-interchange-file-format-in-sharepoint"></a><span data-ttu-id="3b7de-102">Формат файла обмена XLIFF в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b7de-102">The XLIFF interchange file format in SharePoint</span></span>
<span data-ttu-id="3b7de-103">Получение сведений о реализации SharePoint XLIFF формат файла обмена, включая схемы справочную информацию и пример кода XML.</span><span class="sxs-lookup"><span data-stu-id="3b7de-103">Get information about the SharePoint implementation of the XLIFF interchange file format, including schema reference information and an XML example.</span></span>
## <a name="the-xliff-interchange-file-format-implementation-in-sharepoint"></a><span data-ttu-id="3b7de-104">Файл формат XLIFF обмена реализации в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b7de-104">The XLIFF interchange file format implementation in SharePoint</span></span>

<span data-ttu-id="3b7de-105">SharePoint поддерживает формат файла Interchange XML локализации (XLIFF) приложения варианты и функции служб перевода.</span><span class="sxs-lookup"><span data-stu-id="3b7de-105">SharePoint provides XML Localization Interchange File Format (XLIFF) application support for the Variations feature and the Translation Services feature.</span></span> <span data-ttu-id="3b7de-106">SharePoint Server используется XLIFF для передачи информации о файле и ее содержимое из SharePoint Server для человеческого преобразования в формат, который можно легко понять (en).</span><span class="sxs-lookup"><span data-stu-id="3b7de-106">SharePoint Server uses XLIFF to transport information about a file and its contents from SharePoint Server to a human translator in a format that the translator can easily understand.</span></span>
  
    
    
<span data-ttu-id="3b7de-107">[Руководство по представление XLIFF 1.2 для HTML-код](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l) , опубликованный OASIS извлечении SharePoint Server HTML-страниц в формат XLIFF соответствующий SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3b7de-107">SharePoint adheres to the  [XLIFF 1.2 representation guide for HTML](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l) published by OASIS when SharePoint Server HTML pages are extracted to XLIFF format.</span></span> <span data-ttu-id="3b7de-108">Для устранения сочетание переводимые элементы и элементы кода, которые будут отображаться в XLIFF пакетов, если необходимо переместить немодифицированного контент SharePoint Server CDATA SharePoint доставляется возможность создания полностью спецификации XLIFF XLIFF документов интегрированное с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3b7de-108">To eliminate the mix of translatable elements and code elements that would appear in XLIFF packages if unmodified SharePoint Server CDATA content were to be transported, SharePoint is delivered with the ability to produce fully XLIFF-compliant XLIFF documents that are also well-integrated with SharePoint.</span></span> <span data-ttu-id="3b7de-109">При экспорте XML-файлы в формате XLIFF из `sharepointservernv`, данных, которая получает человеческого translator чистой и готова для перевода.</span><span class="sxs-lookup"><span data-stu-id="3b7de-109">When exporting XML files in XLIFF format from `sharepointservernv`, the data that the human translator receives is clean and ready to translate.</span></span>
  
    
    
<span data-ttu-id="3b7de-p103">В этом статье документы определенного SharePoint Server реализации XLIFF элементы и атрибуты, которые определены как правило в версии 1.2 XLIFF open стандартный документ издательством OASIS. Дополнительные сведения о конкретных XLIFF элементы и атрибуты  [XLIFF 1.2 спецификация](http://docs.oasis-open.org/xliff/xliff-core/xliff-corel)см.</span><span class="sxs-lookup"><span data-stu-id="3b7de-p103">This article documents specific SharePoint Server implementations of XLIFF elements and attributes that are defined more generally in version 1.2 of the XLIFF open standard document published by OASIS. For more information about specific XLIFF elements and attributes, see the  [XLIFF 1.2 Specification](http://docs.oasis-open.org/xliff/xliff-core/xliff-corel).</span></span>
  
    
    

  
    
    

<span data-ttu-id="3b7de-112">**В таблице 1. Важные XLIFF элементы и атрибуты в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="3b7de-112">**Table 1. Notable XLIFF elements and attributes in SharePoint**</span></span>


|<span data-ttu-id="3b7de-113">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="3b7de-113">**Element**</span></span>|<span data-ttu-id="3b7de-114">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="3b7de-114">**Attributes**</span></span>|<span data-ttu-id="3b7de-115">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="3b7de-115">**Notes**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="3b7de-116">Xml</span><span class="sxs-lookup"><span data-stu-id="3b7de-116">Xml</span></span>  <br/> | `version` <br/>  `encoding` <br/> |<span data-ttu-id="3b7de-117">Объявляет версии XML и кодировки.</span><span class="sxs-lookup"><span data-stu-id="3b7de-117">Declares the XML version and encoding.</span></span>  <br/> |
|<span data-ttu-id="3b7de-118">XLIFF</span><span class="sxs-lookup"><span data-stu-id="3b7de-118">Xliff</span></span>  <br/> | `version` <br/>  `xmlns` <br/> |<span data-ttu-id="3b7de-119">Содержит атрибут  `version` и механизм проверки схемы.</span><span class="sxs-lookup"><span data-stu-id="3b7de-119">Contains the  `version` attribute and the schema validation mechanism.</span></span> <br/> |
|<span data-ttu-id="3b7de-120">Файл</span><span class="sxs-lookup"><span data-stu-id="3b7de-120">File</span></span>  <br/> | `original` <br/>  `source-language` <br/>  `target-language` <br/>  `datatype` <br/>  `tool-id` <br/> |<span data-ttu-id="3b7de-121">Соответствующий исходный файл, являющийся в одну страницу GUID из вариантов компонент, который включает в себя исходный и целевой языки ( `source-language` и `target-language`), которые будут использоваться средства машинного перевода и средства human перевода.</span><span class="sxs-lookup"><span data-stu-id="3b7de-121">Corresponds to the original source file, which in is one page GUID from the Variations feature that includes the source and target languages ( `source-language` and `target-language`) that are used by both machine-translation tools and human-translation tools.</span></span>  <br/> <span data-ttu-id="3b7de-p104">Атрибут  `original` содержит идентификатор GUID, используемый для идентификации исходного источника контента. Это значение всегда должно быть static для обеспечения успешного импорта.</span><span class="sxs-lookup"><span data-stu-id="3b7de-p104">The  `original` attribute contains a GUID that is used to identify the original source content. This value should remain static to help ensure a successful import. </span></span><br/> <span data-ttu-id="3b7de-124">Атрибут  `datatype` также хранится в элементе **File** для всех страниц SharePoint в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="3b7de-124">The  `datatype` attribute is also stored in the **File** element in HTML format for all SharePoint pages.</span></span> <br/> <span data-ttu-id="3b7de-125">Атрибут  `tool-id`  это идентификатор GUID, определяющий средство, создавшего файл XLIFF.</span><span class="sxs-lookup"><span data-stu-id="3b7de-125">The  `tool-id` attribute is the GUID that identifies the tool that generated the XLIFF file.</span></span> <br/> |
|<span data-ttu-id="3b7de-126">Header</span><span class="sxs-lookup"><span data-stu-id="3b7de-126">Header</span></span>  <br/> |||
|<span data-ttu-id="3b7de-127">Средство</span><span class="sxs-lookup"><span data-stu-id="3b7de-127">Tool</span></span>  <br/> | `tool-id` <br/>  `tool-name` <br/> |<span data-ttu-id="3b7de-128">Указывает, создавшего файл XLIFF инструмент.</span><span class="sxs-lookup"><span data-stu-id="3b7de-128">Identifies the tool that generated the XLIFF file.</span></span>  <br/> |
|<span data-ttu-id="3b7de-129">Примечание</span><span class="sxs-lookup"><span data-stu-id="3b7de-129">Note</span></span>  <br/> ||<span data-ttu-id="3b7de-130">Содержит сведения, которые могут оказаться полезны для локализатора, разработчик или пользователями, имеющими обработки файла XLIFF.</span><span class="sxs-lookup"><span data-stu-id="3b7de-130">Contains information that may be useful to the localizer, developer, or others who process the XLIFF file.</span></span>  <br/>  <span data-ttu-id="3b7de-p105">значения элементов  `note` создаются . атрибуты `note` содержат идентификаторы GUID, чтобы указать расположение и типов контента для предоставления контекста. </span><span class="sxs-lookup"><span data-stu-id="3b7de-p105">`note` element values are generated by . `note` attributes contain GUIDs that identify location and types of content to provide context. </span></span><br/> |
|<span data-ttu-id="3b7de-133">Основной текст</span><span class="sxs-lookup"><span data-stu-id="3b7de-133">Body</span></span>  <br/> |||
|<span data-ttu-id="3b7de-134">Единица передачи</span><span class="sxs-lookup"><span data-stu-id="3b7de-134">Trans-unit</span></span>  <br/> | `id` <br/>  `datatype` <br/> |<span data-ttu-id="3b7de-135">Атрибут  `id` содержит идентификатор GUID, определяющий расположение импорта.</span><span class="sxs-lookup"><span data-stu-id="3b7de-135">The  `id` attribute contains a GUID that identifies the location of the import.</span></span> <br/> <span data-ttu-id="3b7de-p106">Атрибут  `datatype` определяет тип данных, содержащихся в элементе **trans-unit**. Список доступных `datatype` значений атрибутов открытом документе стандартных XLIFF см. </span><span class="sxs-lookup"><span data-stu-id="3b7de-p106">The  `datatype` attribute defines the type of data contained in the **trans-unit** element. For a list of available `datatype` attribute values, see the XLIFF open standard document. </span></span><br/> |
|<span data-ttu-id="3b7de-138">Источник</span><span class="sxs-lookup"><span data-stu-id="3b7de-138">Source</span></span>  <br/> ||<span data-ttu-id="3b7de-139">HTML-контент часто содержит разметки, которые сохранены.</span><span class="sxs-lookup"><span data-stu-id="3b7de-139">HTML content often contains markup that has to be preserved.</span></span> <span data-ttu-id="3b7de-140">По этой причине SharePoint является оболочкой разметки в HTML-контент с тегами, которые определены в [руководство по представление XLIFF 1.2 для HTML-код](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).</span><span class="sxs-lookup"><span data-stu-id="3b7de-140">For this reason, SharePoint wraps markup in HTML content with tags that are defined in the  [XLIFF 1.2 representation guide for HTML](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).</span></span>  <br/> |
|<span data-ttu-id="3b7de-141">Целевой объект</span><span class="sxs-lookup"><span data-stu-id="3b7de-141">Target</span></span>  <br/> |<span data-ttu-id="3b7de-142">фазы (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3b7de-142">ph (optional)</span></span>  <br/> <span data-ttu-id="3b7de-143">BPT (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3b7de-143">bpt (optional)</span></span>  <br/> <span data-ttu-id="3b7de-144">(необязательно) типа корпоративного проекта</span><span class="sxs-lookup"><span data-stu-id="3b7de-144">ept (optional)</span></span>  <br/> <span data-ttu-id="3b7de-145">Sub (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3b7de-145">sub (optional)</span></span>  <br/> |<span data-ttu-id="3b7de-146">HTML-контент часто содержит разметки, которые сохранены.</span><span class="sxs-lookup"><span data-stu-id="3b7de-146">HTML content often contains markup that has to be preserved.</span></span> <span data-ttu-id="3b7de-147">По этой причине SharePoint является оболочкой разметки в HTML-контент с тегами, которые определены в [руководство по представление XLIFF 1.2 для HTML-код](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).</span><span class="sxs-lookup"><span data-stu-id="3b7de-147">For this reason, SharePoint wraps markup in HTML content with tags that are defined in the  [XLIFF 1.2 representation guide for HTML](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).</span></span>  <br/> |
|<span data-ttu-id="3b7de-148">Ячейки единицы</span><span class="sxs-lookup"><span data-stu-id="3b7de-148">Bin-unit</span></span>  <br/> ||<span data-ttu-id="3b7de-149">Файлы, хранящиеся в SharePoint могут быть отправлены для локализации с помощью XLIFF по элементам **ячейки единицы** .</span><span class="sxs-lookup"><span data-stu-id="3b7de-149">Files stored in SharePoint can be sent for localization via XLIFF through the **bin-unit** elements.</span></span> <span data-ttu-id="3b7de-150">Извлечение файла обратно в исходном формате файла с помощью [SharePoint: извлечение и вставка элементов корзины подразделения в файлах XLIFF](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878) пример кода.</span><span class="sxs-lookup"><span data-stu-id="3b7de-150">The file can be extracted back into its original file format by using the [SharePoint: Extract and insert bin-unit elements in XLIFF files](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878) code sample.</span></span> <br/> |
|<span data-ttu-id="3b7de-151">Источник корзины</span><span class="sxs-lookup"><span data-stu-id="3b7de-151">Bin-source</span></span>  <br/> |||
|<span data-ttu-id="3b7de-152">Целевой ячейки</span><span class="sxs-lookup"><span data-stu-id="3b7de-152">Bin-target</span></span>  <br/> |||
|<span data-ttu-id="3b7de-153">Внутренний файл</span><span class="sxs-lookup"><span data-stu-id="3b7de-153">Internalfile</span></span>  <br/> |<span data-ttu-id="3b7de-154">форма</span><span class="sxs-lookup"><span data-stu-id="3b7de-154">form</span></span>  <br/> ||
   

## <a name="example-xliff-markup-from-sharepoint"></a><span data-ttu-id="3b7de-155">Пример: XLIFF разметки из SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b7de-155">Example: XLIFF markup from SharePoint</span></span>

<span data-ttu-id="3b7de-156">В следующем примере XML-документ в формате файла обмена XLIFF показано, как SharePoint реализует некоторые элементы и атрибуты, определенные в стандарте.</span><span class="sxs-lookup"><span data-stu-id="3b7de-156">The following example of an XML document in XLIFF interchange file format demonstrates how SharePoint implements some of the elements and attributes defined in the standard.</span></span> 
  
    
    

```XML

<?xml version="1.0" encoding="utf-8"?>
<xliff version="1.2" xmlns="urn:oasis:names:tc:xliff:document:1.2">
  <file original="ce2b8e40-b802-4196-b6cb-93e63eb4bb42" source-language="en-US" target-language="fr-CA" datatype="html">
    <header>
      <note>type=ListItem</note>
      <note>translatorType=Vendor</note>
      <note>packageGroupId=fb98837d-c4e0-48f1-9e59-874b61802cda</note>
      <note>webId=1c013046-821b-40d7-a1e0-689dd920f37d</note>
      <note>listId=58b11f3f-6549-47c5-bf13-a2dc4dfa03b3</note>
      <note>url=Pages/Type-or-edit-text-in-a-different-language.aspx</note>
      <note>sourceVersion=2</note>
    </header>
<body>
      <trans-unit id="fa564e0f-0c70-4ab9-b863-0177e6ddd247" datatype="plaintext">
        <source>Type or edit text in a different language</source>
        <note>fieldTitle=Title</note>
      </trans-unit>
      <trans-unit id="f55c4d88-1f2e-4ad9-aaa8-819af4ee7ee8" datatype="html">
        <source>
          <bpt id="1">&amp;lt;strong&amp;gt;</bpt>When you want to type documents in different languages, you can change your keyboard layout language--the language-specific characters typed when keyboard keys are pressed--so that you can type the special characters for each language. 
  <ept id="1">&amp;lt;/strong&amp;gt;</ept>
        </source>
        <note>fieldTitle=Page Content</note>
      </trans-unit>
    </body>
  </file>

```


  
    
    

## <a name="additional-resources"></a><span data-ttu-id="3b7de-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3b7de-157">Additional resources</span></span>
<span data-ttu-id="3b7de-158"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3b7de-158"></span></span>


-  [<span data-ttu-id="3b7de-159">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b7de-159">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
- <span data-ttu-id="3b7de-160">Пример кода: [SharePoint: извлечение и вставка элементов корзины подразделения в файлах XLIFF](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878)</span><span class="sxs-lookup"><span data-stu-id="3b7de-160">Code sample:  [SharePoint: Extract and insert bin-unit elements in XLIFF files](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878)</span></span>
    
  
-  [<span data-ttu-id="3b7de-161">Службы машинного перевода в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3b7de-161">Machine Translation Services in SharePoint</span></span>](machine-translation-services-in-sharepoint.md)
    
  

  
    
    

