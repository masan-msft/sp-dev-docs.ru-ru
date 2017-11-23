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
# <a name="how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server"></a><span data-ttu-id="a49bf-102">Как: используйте вызов повышения качества контента веб-службы для SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="a49bf-102">How to: Use the Content Enrichment web service callout for SharePoint Server</span></span>
<span data-ttu-id="a49bf-103">Узнайте, как реализовать повышения качества контента веб-службы в SharePoint для изменения управляемого свойства для обхода элементов перед их индексации.</span><span class="sxs-lookup"><span data-stu-id="a49bf-103">Learn how to implement the Content Enrichment web service in SharePoint to modify the managed properties of crawled items before they are indexed.</span></span>
<span data-ttu-id="a49bf-104">Поиск в SharePoint позволяет разработчикам Добавление настраиваемого шага для обработки изменение управляемого свойства для обхода элементов перед их индексации контента.</span><span class="sxs-lookup"><span data-stu-id="a49bf-104">Search in SharePoint enables developers to add a custom step to content processing to modify the managed properties of crawled items before they are indexed.</span></span> <span data-ttu-id="a49bf-105">Этот шаг настраиваемого необходимо реализовать внешние веб-службы — веб-служба повышения качества контента--можно расширить управляемых свойств элементов, обрабатываемых; и затем Настройка системы, чтобы вызвать этот внешний веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a49bf-105">This custom step requires the implementation of an external web service--the Content Enrichment web service--that can enrich managed properties of items being processed; and then configuring the system to call this external web service.</span></span>
  
    
    

<span data-ttu-id="a49bf-106">Реализация веб-службы, повышения качества внешнего контента зависит от интерфейсов в пространстве имен  [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a49bf-106">Implementation of the external content enrichment web service relies on interfaces under the  [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) namespace.</span></span>
## <a name="windows-powershell-cmdlets-to-use-with-the-content-enrichment-web-service"></a><span data-ttu-id="a49bf-107">Командлеты Windows PowerShell для использования в веб-службу повышения качества контента</span><span class="sxs-lookup"><span data-stu-id="a49bf-107">Windows PowerShell Cmdlets to use with the Content Enrichment web service</span></span>
<span data-ttu-id="a49bf-108"><a name="SP15_PowerShell_Cmdlets_Content_Enrichment"> </a></span><span class="sxs-lookup"><span data-stu-id="a49bf-108"><a name="SP15_PowerShell_Cmdlets_Content_Enrichment"> </a></span></span>

<span data-ttu-id="a49bf-109">Функциональные возможности повышения качества контента настроить и включить с помощью следующих командлетов Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a49bf-109">The Content Enrichment functionality is configured and enabled with the following Windows PowerShell cmdlets:</span></span>
  
    
    

-  [<span data-ttu-id="a49bf-110">Get-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="a49bf-110">Get-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/ru-ru/library/jj219783%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="a49bf-111">Set-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="a49bf-111">Set-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/ru-ru/library/jj219659%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="a49bf-112">Remove-SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="a49bf-112">Remove-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/ru-ru/library/jj219742%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="a49bf-113">Новый SPEnterpriseSearchContentEnrichmentConfiguration</span><span class="sxs-lookup"><span data-stu-id="a49bf-113">New-SPEnterpriseSearchContentEnrichmentConfiguration</span></span>](http://technet.microsoft.com/ru-ru/library/jj219502%28office.15%29.aspx)
    
  
<span data-ttu-id="a49bf-114">Эти командлеты Windows PowerShell включить администратор может настроить следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a49bf-114">These Windows PowerShell cmdlets enable an administrator to configure the following:</span></span>
  
    
    

- <span data-ttu-id="a49bf-115">Пользовательский набор управляемых свойств для отправки внешних веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a49bf-115">A custom set of managed properties to be sent to the external web service.</span></span>
    
  
- <span data-ttu-id="a49bf-116">Пользовательский набор управляемых свойств должно быть возвращено внешних веб-службой.</span><span class="sxs-lookup"><span data-stu-id="a49bf-116">A custom set of managed properties to be returned by the external web service.</span></span>
    
  
- <span data-ttu-id="a49bf-p102">Условие триггер, который представляет предикат на выполнение для всех элементов, обрабатываемых. Если используется условие запуска внешних веб-службы вызывается только в том случае, если триггер **true**. При использовании без условие запуска всех элементов, передаются в внешние веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p102">A trigger condition, that represents a predicate to execute for every item being processed. If a trigger condition is used, the external web service is called only when the trigger evaluates to **true**. If no trigger condition is used, all items are sent to the external web service.</span></span>
    
  
- <span data-ttu-id="a49bf-p103">**FailureMode**, которая позволяет веб-служба, либо не удается элементов, которые не удается обработать на этапе повышения качества контента или передайте эти элементы через без внесения изменений. Если не удалось выполнить элементы, не индексируются и предупреждения, записывается в журнал ULS.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p103">A **FailureMode** that enables the web service to either fail items that cannot be processed during the content enrichment step or pass these items through without any modification. If the items are failed, they are not indexed and a warning is written to the ULS log.</span></span>
    
  
- <span data-ttu-id="a49bf-p104">**DebugMode**, обеспечивающий быстрого создания прототипов внешние веб-службы. При включении этого параметра внешних веб-служба получает все доступные управляемого свойства. В **DebugMode**условие запуска игнорируется и вывод управляемых свойств веб-службой, также игнорируются.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p104">A **DebugMode**, that enables rapid prototyping of the external web service. When enabled, the external web service receives all available managed properties. In **DebugMode**, the trigger condition is ignored and any managed properties output by the web service are also ignored.</span></span>
    
  
- <span data-ttu-id="a49bf-p105">Переключатель **SendRawData**, которое отправляет необработанные данные элемента в двоичном формате. Это полезно, когда требуется больше метаданных чем что можно извлечь из проанализированного версии элемента.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p105">A **SendRawData** switch that sends the raw data of an item in binary form. This is useful when more metadata is required than what can be retrieved from the parsed version of the item.</span></span>
    
  
<span data-ttu-id="a49bf-p106">Кроме того существует возможность указать ограничения на размер и время ожидания. В разделе  [Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"](custom-content-processing-with-the-content-enrichment-web-service-callout.md) полный список настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p106">In addition, there are options for specifying size limits and timeouts. See  [Custom content processing with the Content Enrichment web service callout](custom-content-processing-with-the-content-enrichment-web-service-callout.md) for a full list of configurable properties.</span></span>
  
    
    

## <a name="prerequisites-for-using-the-content-enrichment-web-service-callout-for-sharepoint"></a><span data-ttu-id="a49bf-129">Необходимые условия для использования вызов повышения качества контента веб-службы для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49bf-129">Prerequisites for using the Content Enrichment web service callout for SharePoint</span></span>
<span data-ttu-id="a49bf-130"><a name="SP15ContentEnrich_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="a49bf-130"><a name="SP15ContentEnrich_prereq"> </a></span></span>

<span data-ttu-id="a49bf-131">Для выполнения этой инструкции, необходимо установить следующие компоненты в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="a49bf-131">To complete this how-to, you must have the following installed in your development environment:</span></span>
  
    
    

- <span data-ttu-id="a49bf-132">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49bf-132">Search in SharePoint</span></span>
    
  
- <span data-ttu-id="a49bf-133">Visual Studio 2010 или аналогичную .NET Framework - средство совместимые разработки</span><span class="sxs-lookup"><span data-stu-id="a49bf-133">Visual Studio 2010 or similar .NET Framework-compatible development tool</span></span>
    
  
- <span data-ttu-id="a49bf-134">Права администратора на установку SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49bf-134">Administrator privileges on your SharePoint installation</span></span>
    
  
- <span data-ttu-id="a49bf-135">Сервер, на котором вы можете размещать службы с помощью служб IIS</span><span class="sxs-lookup"><span data-stu-id="a49bf-135">A server on which you can host the service with IIS</span></span>
    
  
<span data-ttu-id="a49bf-136">Также необходимо знать, как создать сайт в службах IIS и развертывание службы</span><span class="sxs-lookup"><span data-stu-id="a49bf-136">You must also know how to create a site in IIS and deploy a service to it</span></span>
  
    
    

## <a name="set-up-a-content-enrichment-service-project"></a><span data-ttu-id="a49bf-137">Настройка проекта службы повышения качества контента</span><span class="sxs-lookup"><span data-stu-id="a49bf-137">Set up a content enrichment service project</span></span>
<span data-ttu-id="a49bf-138"><a name="SP15ContentEnrich_setup"> </a></span><span class="sxs-lookup"><span data-stu-id="a49bf-138"><a name="SP15ContentEnrich_setup"> </a></span></span>

<span data-ttu-id="a49bf-139">На этом этапе будет создать проект реализации службы и добавьте необходимые ссылки в проект.</span><span class="sxs-lookup"><span data-stu-id="a49bf-139">In this step, you will create the service implementation project and then add the required references to the project.</span></span>
  
    
    

### <a name="to-create-the-project-for-a-content-enrichment-service"></a><span data-ttu-id="a49bf-140">Создание проекта для повышения качества контента службы</span><span class="sxs-lookup"><span data-stu-id="a49bf-140">To create the project for a content enrichment service</span></span>


1. <span data-ttu-id="a49bf-141">В Visual Studio в строке меню щелкните **файл**, **Создать**, **проект**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-141">In Visual Studio, on the menu bar choose **File**, **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="a49bf-142">В окне **типы проектов** в разделе Visual C# выберите **WCF**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-142">In **Project types**, under Visual C#, choose **WCF**.</span></span>
    
  
3. <span data-ttu-id="a49bf-p107">В области **Шаблоны** выберите **Приложение-службу WCF**. В поле **имя** введите **ContentProcessingEnrichmentService** и затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p107">Under **Templates**, choose **WCF Service Application**. In the **Name** field, type **ContentProcessingEnrichmentService**, and then choose the **OK** button.</span></span>
    
  
4. <span data-ttu-id="a49bf-145">Удалите автоматически созданный **Service1** класс и **Service1** интерфейс.</span><span class="sxs-lookup"><span data-stu-id="a49bf-145">Delete the automatically generated **Service1** class and **Service1** interface.</span></span>
    
  

### <a name="to-add-references-to-the-content-enrichment-service-project"></a><span data-ttu-id="a49bf-146">Добавление ссылок в проект службы повышения качества контента</span><span class="sxs-lookup"><span data-stu-id="a49bf-146">To add references to the content enrichment service project</span></span>


1. <span data-ttu-id="a49bf-147">В меню **проект** выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-147">On the **Project** menu, choose **Add Reference**.</span></span>
    
  
2. <span data-ttu-id="a49bf-148">Нажмите кнопку **Обзор** и найдите сборку **Microsoft.Office.Server.Search.ContentProcessingEnrichment** в папке установки SharePoint в разделе _Installation Path_\\Microsoft Office Servers\\15.0\\Search\\Applications\\External.</span><span class="sxs-lookup"><span data-stu-id="a49bf-148">Choose **Browse** and locate the **Microsoft.Office.Server.Search.ContentProcessingEnrichment** assembly in your SharePoint installation folder under _Installation Path_\\Microsoft Office Servers\\15.0\\Search\\Applications\\External.</span></span> 
    
    > <span data-ttu-id="a49bf-149">**Примечание:** Если на компьютере, используемом для разработки компьютере установлена служба SharePoint, скопируйте сборку на компьютере для разработки и ссылаться на нее из.</span><span class="sxs-lookup"><span data-stu-id="a49bf-149">**Note:** If SharePoint is installed on a machine other than your development machine, copy the assembly over to your development machine and reference it from there.</span></span> 

## <a name="create-a-content-enrichment-service"></a><span data-ttu-id="a49bf-150">Создание службы повышения качества контента</span><span class="sxs-lookup"><span data-stu-id="a49bf-150">Create a content enrichment service</span></span>
<span data-ttu-id="a49bf-151"><a name="SP15ContentEnrich_createservice"> </a></span><span class="sxs-lookup"><span data-stu-id="a49bf-151"><a name="SP15ContentEnrich_createservice"> </a></span></span>

<span data-ttu-id="a49bf-p108">Обработка службы повышения качества контента должна реализовать интерфейс **IContentProcessingEnrichmentService** из пространства имен [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) . В примере кода в этом разделе представлена базовая реализацию этого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p108">Your content processing enrichment service must implement the **IContentProcessingEnrichmentService** interface from the [Microsoft.Office.Server.Search.ContentProcessingEnrichment](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.ContentProcessingEnrichment.aspx) namespace. The code example in this section is a basic implementation of this interface.</span></span>
  
    
    
<span data-ttu-id="a49bf-p109">Реализация требует наличия двух управляемых свойств для каждого элемента, получаемые с помощью внешних веб-службы: **Author** и **Filename**. **Author**  это список объектов **String** и **Filename**  это объект **String**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p109">The implementation requires two managed properties for each item received via the external web service: **Author** and **Filename**. The **Author** is a list of **String** objects and the **Filename** is a **String** object.</span></span>
  
    
    
<span data-ttu-id="a49bf-p110">Реализация **IContentProcessingEnrichmentService** записывает необработанные двоичные данные во временной папке на диске с **Filename** в качестве имени файла. Затем новое имя добавлено в список авторов и возвращается к компоненту обработки контента.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p110">The **IContentProcessingEnrichmentService** implementation writes the raw binary data to a temporary location on disk, with **Filename** as the name of the file. Then, a new name is added to the list of authors and returned to the content processing component.</span></span>
  
    
    

### <a name="to-create-the-class-file-for-the-content-enrichment-service"></a><span data-ttu-id="a49bf-158">Чтобы создать файл класса для повышения качества контента службы</span><span class="sxs-lookup"><span data-stu-id="a49bf-158">To create the class file for the content enrichment service</span></span>


1. <span data-ttu-id="a49bf-159">В меню **ПРОЕКТ** выберите пункт **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-159">On the **Project** menu, choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="a49bf-160">В разделе **Visual C#** в разделе **Установленные шаблоны** выберите строку **Web** и выберите **Службы WCF**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-160">Under **Visual C#** in **Installed Templates**, choose **Web**, and then choose **WCF Service**.</span></span>
    
  
3. <span data-ttu-id="a49bf-161">Введите **ContentProcessingEnrichmentService.svc** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-161">Type **ContentProcessingEnrichmentService.svc**, and then choose **Add**.</span></span>
    
  
4. <span data-ttu-id="a49bf-162">Удаление интерфейса **IContentProcessingEnrichmentService.cs**, которая создается.</span><span class="sxs-lookup"><span data-stu-id="a49bf-162">Delete the **IContentProcessingEnrichmentService.cs** interface that is created.</span></span>
    
  

### <a name="to-modify-the-default-code-in-the-contentprocessingenrichmentservice-class"></a><span data-ttu-id="a49bf-163">Изменение кода по умолчанию в классе ContentProcessingEnrichmentService</span><span class="sxs-lookup"><span data-stu-id="a49bf-163">To modify the default code in the ContentProcessingEnrichmentService class</span></span>


1. <span data-ttu-id="a49bf-164">Замените существующий директивы **using** следующие директивы **using** в начале класса.</span><span class="sxs-lookup"><span data-stu-id="a49bf-164">Replace the existing **using** directives with the following **using** directives at the beginning of the class.</span></span>
    
```cs
  
using System;
using System.Collections.Generic;
using System.IO;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment;
using Microsoft.Office.Server.Search.ContentProcessingEnrichment.PropertyTypes;

```

2. <span data-ttu-id="a49bf-165">Метод **DoWork** DELETE.</span><span class="sxs-lookup"><span data-stu-id="a49bf-165">Delete the **DoWork** method.</span></span>
    
  

### <a name="to-implement-the-icontentprocessingenrichmentservice-interface-method"></a><span data-ttu-id="a49bf-166">Чтобы реализовать метод интерфейса IContentProcessingEnrichmentService</span><span class="sxs-lookup"><span data-stu-id="a49bf-166">To implement the IContentProcessingEnrichmentService interface method</span></span>


1. <span data-ttu-id="a49bf-167">Добавьте следующий код внутри класса, чтобы определить необходимые константы и его элементы.</span><span class="sxs-lookup"><span data-stu-id="a49bf-167">Add the following code inside the class to define the required constants and members.</span></span>
    
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

2. <span data-ttu-id="a49bf-168">Добавьте следующий код для объявления метода **ProcessItem**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-168">Add the following code for the **ProcessItem** method.</span></span>
    
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

3. <span data-ttu-id="a49bf-169">Изменение **web.config** принимать сообщения до 8 МБ и настройка **readerQuotas** до такой степени, значением.</span><span class="sxs-lookup"><span data-stu-id="a49bf-169">Modify **web.config** to accept messages up to 8 MB, and configure **readerQuotas** to be a sufficiently large value.</span></span>
    
  
4. <span data-ttu-id="a49bf-170">Добавьте следующий код внутри **<system.serviceModel>**.</span><span class="sxs-lookup"><span data-stu-id="a49bf-170">Add the following inside **<system.serviceModel>**.</span></span>
    
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

<span data-ttu-id="a49bf-171">Выполните построение проекта и его развертывание на свой сайт служб IIS.</span><span class="sxs-lookup"><span data-stu-id="a49bf-171">Build the project and deploy it to your IIS site.</span></span>
  
    
    

## <a name="configure-sharepoint"></a><span data-ttu-id="a49bf-172">Настройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49bf-172">Configure SharePoint</span></span>
<span data-ttu-id="a49bf-173"><a name="SP15ContentEnrich_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="a49bf-173"><a name="SP15ContentEnrich_configure"> </a></span></span>

<span data-ttu-id="a49bf-174">Откройте Командная консоль SharePoint и введите следующую последовательность Windows PowerShell командлетов.</span><span class="sxs-lookup"><span data-stu-id="a49bf-174">Open the SharePoint Management Shell, and enter the following sequence of Windows PowerShell cmdlets.</span></span>
  
    
    

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

<span data-ttu-id="a49bf-p111">Последовательность Windows PowerShell командлеты позволяют сначала создайте объект конфигурации с помощью командлета  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/ru-ru/library/jj219502%28office.15%29.aspx) . Объект конфигурации нажмите указывает к реализации службы; Рекомендуется используйте `http://localhost:808` для _Site_URL_.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p111">The sequence of Windows PowerShell cmdlets help you to first create a configuration object by using the  [New-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/ru-ru/library/jj219502%28office.15%29.aspx) cmdlet. The configuration object is then pointed toward your service implementation; as a best practice, use `http://localhost:808` for _Site_URL_.</span></span>
  
    
    
<span data-ttu-id="a49bf-p112">Управляемые свойства **Author** и **Filename**, передаются в службе для каждого элемента, который обрабатывается. Кроме того Проинформируйте клиента веб-службы, что службы будут выведены управляемое свойство **Author**. В дополнительных управляемых свойств клиента веб-службы настроена для отправки необработанные данные элемента с ограничением на размер данных. И, наконец командлет  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/ru-ru/library/jj219659%28office.15%29.aspx)используется для хранения всей конфигурации. После этот командлет возвращает, конфигурации активен, и компонент обхода контента с помощью этой конфигурации его следующий процесс обхода контента.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p112">The managed properties **Author** and **Filename** are sent to your service for every item that is being processed. In addition, you have informed the web service client that the service will output a single managed property, **Author**. In additional to managed properties, the web service client is configured to send the raw data of the item with a limitation on the size of the data. Finally, the  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/ru-ru/library/jj219659%28office.15%29.aspx)cmdlet is used to store the entire configuration. After this cmdlet returns, the configuration is active and the crawl component uses this configuration for its next crawl process.</span></span>
  
    
    
<span data-ttu-id="a49bf-p113">После завершения этой работы, можно начать полный обход контента сайта. Если служба работает правильно, можно отслеживать временная папка на сервере, где размещается сайт для документы, написанные на диске.</span><span class="sxs-lookup"><span data-stu-id="a49bf-p113">After this is finished, you can start a full crawl of your site. If the service is working correctly, you should be able to monitor the temporary folder on the server hosting your site for the documents written to disk.</span></span>
  
    
    
<span data-ttu-id="a49bf-184">Можно удалить конфигурацию более поздней версии с помощью следующего командлета Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a49bf-184">You can remove the configuration later by using the following Windows PowerShell cmdlet.</span></span>
  
    
    



```

Remove-SPEnterpriseSearchContentEnrichmentConfiguration -SearchApplication $ssa
```


## <a name="additional-resources"></a><span data-ttu-id="a49bf-185">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a49bf-185">Additional resources</span></span>
<span data-ttu-id="a49bf-186"><a name="SP15ContentEnrich_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a49bf-186"><a name="SP15ContentEnrich_addresources"> </a></span></span>


-  [<span data-ttu-id="a49bf-187">Запустить, приостановить, возобновить или остановить обход контента</span><span class="sxs-lookup"><span data-stu-id="a49bf-187">Start, pause, resume, or stop a crawl</span></span>](http://technet.microsoft.com/ru-ru/library/jj219814%28office.15%29.aspx)
    
  
-  [<span data-ttu-id="a49bf-188">Настройка службы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a49bf-188">Configure search in SharePoint</span></span>](configure-search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="a49bf-189">Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"</span><span class="sxs-lookup"><span data-stu-id="a49bf-189">Custom content processing with the Content Enrichment web service callout</span></span>](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  

