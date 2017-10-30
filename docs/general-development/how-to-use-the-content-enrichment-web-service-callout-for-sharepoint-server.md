---
title: "Как используйте вызов повышения качества контента веб-службы для SharePoint Server"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d4e44498-9a3d-4f2f-b5ba-6ebef9971dcb
ms.openlocfilehash: cd0c56acb2b806bcaf2718f0702729d005711f78
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server"></a>Как: используйте вызов повышения качества контента веб-службы для SharePoint Server
Узнайте, как реализовать повышения качества контента веб-службы в SharePoint для изменения управляемого свойства для обхода элементов перед их индексации.
Поиск в SharePoint позволяет разработчикам Добавление настраиваемого шага для обработки изменение управляемого свойства для обхода элементов перед их индексации контента. Этот шаг настраиваемого необходимо реализовать внешние веб-службы — веб-служба повышения качества контента--можно расширить управляемых свойств элементов, обрабатываемых; и затем Настройка системы, чтобы вызвать этот внешний веб-службы.
  
    
    

Реализация веб-службы, повышения качества внешнего контента зависит от интерфейсов в пространстве имен  [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) .
## <a name="windows-powershell-cmdlets-to-use-with-the-content-enrichment-web-service"></a>Командлеты Windows PowerShell для использования в веб-службу повышения качества контента
<a name="SP15_PowerShell_Cmdlets_Content_Enrichment"> </a>

Функциональные возможности повышения качества контента настроить и включить с помощью следующих командлетов Windows PowerShell:
  
    
    

-  [Get-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219783%28office.15%29.aspx)
    
  
-  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219659%28office.15%29.aspx)
    
  
-  [Remove-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219742%28office.15%29.aspx)
    
  
-  [Новый SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219502%28office.15%29.aspx)
    
  
Эти командлеты Windows PowerShell включить администратор может настроить следующие параметры:
  
    
    

- Пользовательский набор управляемых свойств для отправки внешних веб-службы.
    
  
- Пользовательский набор управляемых свойств должно быть возвращено внешних веб-службой.
    
  
- Условие триггер, который представляет предикат на выполнение для всех элементов, обрабатываемых. Если используется условие запуска внешних веб-службы вызывается только в том случае, если триггер **true**. При использовании без условие запуска всех элементов, передаются в внешние веб-службы.
    
  
- **FailureMode**, которая позволяет веб-служба, либо не удается элементов, которые не удается обработать на этапе повышения качества контента или передайте эти элементы через без внесения изменений. Если не удалось выполнить элементы, не индексируются и предупреждения, записывается в журнал ULS.
    
  
- **DebugMode**, обеспечивающий быстрого создания прототипов внешние веб-службы. При включении этого параметра внешних веб-служба получает все доступные управляемого свойства. В **DebugMode**условие запуска игнорируется и вывод управляемых свойств веб-службой, также игнорируются.
    
  
- Переключатель **SendRawData**, которое отправляет необработанные данные элемента в двоичном формате. Это полезно, когда требуется больше метаданных чем что можно извлечь из проанализированного версии элемента.
    
  
Кроме того существует возможность указать ограничения на размер и время ожидания. В разделе  [Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"](custom-content-processing-with-the-content-enrichment-web-service-callout.md) полный список настраиваемых свойств.
  
    
    

## <a name="prerequisites-for-using-the-content-enrichment-web-service-callout-for-sharepoint"></a>Необходимые условия для использования вызов повышения качества контента веб-службы для SharePoint
<a name="SP15ContentEnrich_prereq"> </a>

Для выполнения этой инструкции, необходимо установить следующие компоненты в среде разработки:
  
    
    

- Поиск в SharePoint
    
  
- Visual Studio 2010 или аналогичную .NET Framework - средство совместимые разработки
    
  
- Права администратора на установку SharePoint
    
  
- Сервер, на котором вы можете размещать службы с помощью служб IIS
    
  
Также необходимо знать, как создать сайт в службах IIS и развертывание службы
  
    
    

## <a name="set-up-a-content-enrichment-service-project"></a>Настройка проекта службы повышения качества контента
<a name="SP15ContentEnrich_setup"> </a>

На этом этапе будет создать проект реализации службы и добавьте необходимые ссылки в проект.
  
    
    

### <a name="to-create-the-project-for-a-content-enrichment-service"></a>Создание проекта для повышения качества контента службы


1. В Visual Studio в строке меню щелкните **файл**, **Создать**, **проект**.
    
  
2. В окне **типы проектов** в разделе Visual C# выберите **WCF**.
    
  
3. В области **Шаблоны** выберите **Приложение-службу WCF**. В поле **имя** введите **ContentProcessingEnrichmentService** и затем нажмите кнопку **ОК**.
    
  
4. Удалите автоматически созданный **Service1** класс и **Service1** интерфейс.
    
  

### <a name="to-add-references-to-the-content-enrichment-service-project"></a>Добавление ссылок в проект службы повышения качества контента


1. В меню **проект** выберите команду **Добавить ссылку**.
    
  
2. Нажмите кнопку **Обзор** и найдите сборку **Microsoft.Office.Server.Search.ContentProcessingEnrichment** в папке установки SharePoint в разделе _Installation Path_\\Microsoft Office Servers\\15.0\\Search\\Applications\\External. 
    
    > **Примечание:** Если на компьютере, используемом для разработки компьютере установлена служба SharePoint, скопируйте сборку на компьютере для разработки и ссылаться на нее из. 

## <a name="create-a-content-enrichment-service"></a>Создание службы повышения качества контента
<a name="SP15ContentEnrich_createservice"> </a>

Обработка службы повышения качества контента должна реализовать интерфейс **IContentProcessingEnrichmentService** из пространства имен [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) . В примере кода в этом разделе представлена базовая реализацию этого интерфейса.
  
    
    
Реализация требует наличия двух управляемых свойств для каждого элемента, получаемые с помощью внешних веб-службы: **Author** и **Filename**. **Author**  это список объектов **String** и **Filename**  это объект **String**.
  
    
    
Реализация **IContentProcessingEnrichmentService** записывает необработанные двоичные данные во временной папке на диске с **Filename** в качестве имени файла. Затем новое имя добавлено в список авторов и возвращается к компоненту обработки контента.
  
    
    

### <a name="to-create-the-class-file-for-the-content-enrichment-service"></a>Чтобы создать файл класса для повышения качества контента службы


1. В меню **ПРОЕКТ** выберите пункт **Добавить новый элемент**.
    
  
2. В разделе **Visual C#** в разделе **Установленные шаблоны** выберите строку **Web** и выберите **Службы WCF**.
    
  
3. Введите **ContentProcessingEnrichmentService.svc** и нажмите кнопку **Добавить**.
    
  
4. Удаление интерфейса **IContentProcessingEnrichmentService.cs**, которая создается.
    
  

### <a name="to-modify-the-default-code-in-the-contentprocessingenrichmentservice-class"></a>Изменение кода по умолчанию в классе ContentProcessingEnrichmentService


1. Замените существующий директивы **using** следующие директивы **using** в начале класса.
    
```cs
  
using System;
using System.Collections.Generic;
using System.IO;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment.PropertyTypes;

```

2. Метод **DoWork** DELETE.
    
  

### <a name="to-implement-the-icontentprocessingenrichmentservice-interface-method"></a>Чтобы реализовать метод интерфейса IContentProcessingEnrichmentService


1. Добавьте следующий код внутри класса, чтобы определить необходимые константы и его элементы.
    
```cs
  
// Defines the name of the managed property 'Filename'.
private const string FileNameProperty = "Filename";

// Defines the name of the managed property 'Author'
private const string AuthorProperty = "Author";

// Defines the temporary directory where binary data will be stored.
private const string TempDirectory = @"C:\\Temp";

// Defines the error code for managed properties with an unexpected type.
private const int UnexpectedType = 1;

// Defines the error code for encountering unexpected exceptions.
private const int UnexpectedError = 2;

private readonly ProcessedItem processedItemHolder = new ProcessedItem
{ 
   ItemProperties = new List<AbstractProperty>()
};
```

2. Добавьте следующий код для объявления метода **ProcessItem**.
    
```cs
  
public ProcessedItem ProcessItem(Item item)
{
   processedItemHolder.ErrorCode = 0;
   processedItemHolder.ItemProperties.Clear();
   try
   {
      // Iterate over each property received and locate the two properties we
      // configured the system to send.
      foreach (var property in item.ItemProperties)
      {
         // Check if this is the author property.
         if (property.Name.Equals(AuthorProperty, StringComparison.Ordinal))
         {
            var author = property as Property<List<string>>;
            if (author == null)
            {
               // The author property was not of the expected type.
               // Update the error code and return. 
                  processedItemHolder.ErrorCode = UnexpectedType;
                  return processedItemHolder;
            }
               // Adding a new author to the list so it will become searchable.      
                  author.Value.Add("ExampleService");
                  processedItemHolder.ItemProperties.Add(author);
         }
         else if (property.Name.Equals(FileNameProperty, StringComparison.Ordinal))
         {
            var filename = property as Property<string>;
            if (filename == null)
            {
               // The file name property was not of the expected type.
               // Update error code and return.
                  processedItemHolder.ErrorCode = UnexpectedType;
                  return processedItemHolder;
            }
            if (!string.IsNullOrEmpty(filename.Value))
            {
               var fullFilePath = string.Join(char.ToString(Path.DirectorySeparatorChar), TempDirectory, filename.Value);
               if (item.RawData != null)
               {   
                  var outputFile = File.Create(fullFilePath);
                  using (var writer = new BinaryWriter(outputFile))
                  {
                     writer.Write(item.RawData);
                  }
               }
            }
         }
      }
   }
   catch (Exception)
   { 
      processedItemHolder.ErrorCode = UnexpectedError;
   } return processedItemHolder;
}
```

3. Изменение **web.config** принимать сообщения до 8 МБ и настройка **readerQuotas** до такой степени, значением.
    
  
4. Добавьте следующий код внутри **<system.serviceModel>**.
    
```XML
  
<bindings>
   <basicHttpBinding>
   <!-- The service will accept a maximum blob of 8 MB. -->
      <binding maxReceivedMessageSize = "8388608">
         <readerQuotas maxDepth="32"
          maxStringContentLength="2147483647"
          maxArrayLength="2147483647"   
          maxBytesPerRead="2147483647"   
          maxNameTableCharCount="2147483647" />  
             <security mode="None" />
      </binding>
   </basicHttpBinding>
</bindings>
```

Выполните построение проекта и его развертывание на свой сайт служб IIS.
  
    
    

## <a name="configure-sharepoint"></a>Настройка SharePoint
<a name="SP15ContentEnrich_configure"> </a>

Откройте Командная консоль SharePoint и введите следующую последовательность Windows PowerShell командлетов.
  
    
    

```

$ssa = Get-SPEnterpriseSearchServiceApplication
$config = New-SPEnterpriseSearchContentEnrichmentConfiguration
$config.Endpoint = http://Site_URL/ContentEnrichmentService.svc
$config.InputProperties = "Author", "Filename"
$config.OutputProperties = "Author"
$config.SendRawData = $True
$config.MaxRawDataSize = 8192
Set-SPEnterpriseSearchContentEnrichmentConfiguration -SearchApplication
$ssa -ContentEnrichmentConfiguration $config
```

Последовательность Windows PowerShell командлеты позволяют сначала создайте объект конфигурации с помощью командлета  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219502%28office.15%29.aspx) . Объект конфигурации нажмите указывает к реализации службы; Рекомендуется используйте `http://localhost:808` для _Site_URL_.
  
    
    
Управляемые свойства **Author** и **Filename**, передаются в службе для каждого элемента, который обрабатывается. Кроме того Проинформируйте клиента веб-службы, что службы будут выведены управляемое свойство **Author**. В дополнительных управляемых свойств клиента веб-службы настроена для отправки необработанные данные элемента с ограничением на размер данных. И, наконец командлет  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219659%28office.15%29.aspx)используется для хранения всей конфигурации. После этот командлет возвращает, конфигурации активен, и компонент обхода контента с помощью этой конфигурации его следующий процесс обхода контента.
  
    
    
После завершения этой работы, можно начать полный обход контента сайта. Если служба работает правильно, можно отслеживать временная папка на сервере, где размещается сайт для документы, написанные на диске.
  
    
    
Можно удалить конфигурацию более поздней версии с помощью следующего командлета Windows PowerShell.
  
    
    



```

Remove-SPEnterpriseSearchContentEnrichmentConfiguration -SearchApplication $ssa
```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15ContentEnrich_addresources"> </a>


-  [Запустить, приостановить, возобновить или остановить обход контента](http://technet.microsoft.com/en-us/library/jj219814%28office.15%29.aspx)
    
  
-  [Настройка службы поиска в SharePoint](configure-search-in-sharepoint.md)
    
  
-  [Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

