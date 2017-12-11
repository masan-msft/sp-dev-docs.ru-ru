---
title: "Формат файла обмена XLIFF в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 660c0f07-7030-4576-957e-b9f2cd0fa895
ms.openlocfilehash: 106110eb458cf6cd76ebc67fd8516cbcb4358a4f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="the-xliff-interchange-file-format-in-sharepoint"></a>Формат файла обмена XLIFF в SharePoint
Получение сведений о реализации SharePoint XLIFF формат файла обмена, включая схемы справочную информацию и пример кода XML.
## <a name="the-xliff-interchange-file-format-implementation-in-sharepoint"></a>Файл формат XLIFF обмена реализации в SharePoint

SharePoint поддерживает формат файла Interchange XML локализации (XLIFF) приложения варианты и функции служб перевода. SharePoint Server используется XLIFF для передачи информации о файле и ее содержимое из SharePoint Server для человеческого преобразования в формат, который можно легко понять (en).
  
    
    
[Руководство по представление XLIFF 1.2 для HTML-код](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l) , опубликованный OASIS извлечении SharePoint Server HTML-страниц в формат XLIFF соответствующий SharePoint. Для устранения сочетание переводимые элементы и элементы кода, которые будут отображаться в XLIFF пакетов, если необходимо переместить немодифицированного контент SharePoint Server CDATA SharePoint доставляется возможность создания полностью спецификации XLIFF XLIFF документов интегрированное с SharePoint. При экспорте XML-файлы в формате XLIFF из `sharepointservernv`, данных, которая получает человеческого translator чистой и готова для перевода.
  
    
    
В этом статье документы определенного SharePoint Server реализации XLIFF элементы и атрибуты, которые определены как правило в версии 1.2 XLIFF open стандартный документ издательством OASIS. Дополнительные сведения о конкретных XLIFF элементы и атрибуты  [XLIFF 1.2 спецификация](http://docs.oasis-open.org/xliff/xliff-core/xliff-corel)см.
  
    
    

  
    
    

**В таблице 1. Важные XLIFF элементы и атрибуты в SharePoint**


|**Элемент**|**Атрибуты**|**Примечания**|
|:-----|:-----|:-----|
|Xml  <br/> | `version` <br/>  `encoding` <br/> |Объявляет версии XML и кодировки.  <br/> |
|XLIFF  <br/> | `version` <br/>  `xmlns` <br/> |Содержит атрибут  `version` и механизм проверки схемы. <br/> |
|Файл  <br/> | `original` <br/>  `source-language` <br/>  `target-language` <br/>  `datatype` <br/>  `tool-id` <br/> |Соответствующий исходный файл, являющийся в одну страницу GUID из вариантов компонент, который включает в себя исходный и целевой языки ( `source-language` и `target-language`), которые будут использоваться средства машинного перевода и средства human перевода.  <br/> Атрибут  `original` содержит идентификатор GUID, используемый для идентификации исходного источника контента. Это значение всегда должно быть static для обеспечения успешного импорта.<br/> Атрибут  `datatype` также хранится в элементе **File** для всех страниц SharePoint в формате HTML. <br/> Атрибут  `tool-id`  это идентификатор GUID, определяющий средство, создавшего файл XLIFF. <br/> |
|Header  <br/> |||
|Средство  <br/> | `tool-id` <br/>  `tool-name` <br/> |Указывает, создавшего файл XLIFF инструмент.  <br/> |
|Примечание  <br/> ||Содержит сведения, которые могут оказаться полезны для локализатора, разработчик или пользователями, имеющими обработки файла XLIFF.  <br/>  значения элементов  `note` создаются . атрибуты `note` содержат идентификаторы GUID, чтобы указать расположение и типов контента для предоставления контекста. <br/> |
|Основной текст  <br/> |||
|Единица передачи  <br/> | `id` <br/>  `datatype` <br/> |Атрибут  `id` содержит идентификатор GUID, определяющий расположение импорта. <br/> Атрибут  `datatype` определяет тип данных, содержащихся в элементе **trans-unit**. Список доступных `datatype` значений атрибутов открытом документе стандартных XLIFF см. <br/> |
|Источник  <br/> ||HTML-контент часто содержит разметки, которые сохранены. По этой причине SharePoint является оболочкой разметки в HTML-контент с тегами, которые определены в [руководство по представление XLIFF 1.2 для HTML-код](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).  <br/> |
|Целевой объект  <br/> |фазы (необязательно)  <br/> BPT (необязательно)  <br/> (необязательно) типа корпоративного проекта  <br/> Sub (необязательно)  <br/> |HTML-контент часто содержит разметки, которые сохранены. По этой причине SharePoint является оболочкой разметки в HTML-контент с тегами, которые определены в [руководство по представление XLIFF 1.2 для HTML-код](http://docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02l).  <br/> |
|Ячейки единицы  <br/> ||Файлы, хранящиеся в SharePoint могут быть отправлены для локализации с помощью XLIFF по элементам **ячейки единицы** . Извлечение файла обратно в исходном формате файла с помощью [SharePoint: извлечение и вставка элементов корзины подразделения в файлах XLIFF](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878) пример кода. <br/> |
|Источник корзины  <br/> |||
|Целевой ячейки  <br/> |||
|Внутренний файл  <br/> |форма  <br/> ||
   

## <a name="example-xliff-markup-from-sharepoint"></a>Пример: XLIFF разметки из SharePoint

В следующем примере XML-документ в формате файла обмена XLIFF показано, как SharePoint реализует некоторые элементы и атрибуты, определенные в стандарте. 
  
    
    

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


  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Добавление возможностей SharePoint](add-sharepoint-capabilities.md)
    
  
- Пример кода: [SharePoint: извлечение и вставка элементов корзины подразделения в файлах XLIFF](http://code.msdn.microsoft.com/SharePoint-Extract-fe686878)
    
  
-  [Службы машинного перевода в SharePoint](machine-translation-services-in-sharepoint.md)
    
  

  
    
    

