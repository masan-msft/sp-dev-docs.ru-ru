---
title: "Библиотека базовых и PnP модуля подготовки"
ms.date: 11/03/2017
ms.openlocfilehash: 274c9796be400d3ae305358ff93d9dd6d28fa8bf
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="pnp-provisioning-engine-and-the-core-library"></a>Библиотека базовых и PnP модуля подготовки

Высокоуровневая рассмотрим удаленного процесс подготовки, включая подробное рассмотрение библиотеки OfficeDevPnP.Core.

PnP модуль подготовки — это основа подготовки framework и в его foundation — библиотека OfficeDevPnP.Core. Модуль подготовки является частью основной библиотеки и в ней используются расширения основные библиотеки в реализации задачи подготовки. Включает в себя методы расширения в объектной модели SharePoint CSOM и REST, Библиотека базовых позволяет подготовки задач, таких как перечисление и начало подготовки шаблонов, а также хранения и применения шаблонов для новых и существующих сайтов. Он также позволяет автоматизировать задачи подготовки и добавлять закодированного логику в подготовки процедуры.

**Примечание:**  Чтобы просмотреть видеозапись с пошаговой создания и сохранения и применение шаблона подготовки, перейдите к [Приступая к работе с PnP модуля подготовки](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).

## <a name="pnp-provisioning-engine"></a>PnP модуля подготовки

PnP модуль подготовки — структурированных реализация классов в библиотеке ядра в для выполнения и автоматизация удаленных задач подготовки. В новый Microsoft альбомную модели, компоненты надстройки SharePoint, подготовки решения для SharePoint Online, SharePoint 2013 и Office 365 теперь использовать клиентской объектной модели (CSOM) и платформа подготовки к подготовке артефактов сайта.

PnP модуля подготовки позволяет модель разработки столбцы сайта, типов контента, определений списков, вариантов оформления и страниц. Вы можете разработать этих функций и значительная более, с указанием существующих компонентов оформления сайта, с создания проекта руку, или используя сочетание оба подхода. Затем можно при необходимости сохранения разработка как подготовки шаблон, который можно сохранить и повторного использования.

Можно использовать один из двух подходов для извлечения как подготовки шаблона проекта веб-узла. Используйте CSOM/REST код, реализующий методы расширения, автор сценариев (SharePointPnP.PowerShell) Библиотека базовых (OfficeDevPnP.Core) или использовать Windows PowerShell.

### <a name="using-windows-powershell-scripting-to-extract-a-provisioning-template"></a>С помощью Windows PowerShell, сценарии для извлечения подготовки шаблона

Чтобы использовать сценарии Windows PowerShell с помощью модуля подготовки, сначала необходимо загрузить и установить командлеты PnP PowerShell. Все, что необходимо для запуска Windows PowerShell, включая файл для загрузки и инструкции по установке, а также документация по командам Windows PowerShell будет доступна в репозиторий [SharePointPnP.PowerShell команды](https://github.com/SharePoint/PnP-PowerShell) на репозиториев.

**Примечание:**  Репозиторий команды SharePointPnP.PowerShell содержит три версии MSI команд Windows PowerShell. Два являются для локального использования (по одному для SharePoint 2013), а другое для SharePoint 2016, а третье — для SharePoint Online.

Репозиторий команды SharePointPnP.PowerShell содержит содержимое, которые позволяют создавать библиотеку команд Windows PowerShell, ориентированных на SharePoint Online. Команды используется CSOM и может работать в обоих SharePoint Online и SharePoint в локальной, в зависимости от того, какие MSI-пакет установки.

Кроме того, существует короткое видео [канала 9](https://channel9.msdn.com/) &mdash;Общие сведения о [Командлетах PnP PowerShell](https://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-PnP-PowerShell-Cmdlets)&mdash;, который обсуждается установки пакета Windows PowerShell и подключение к сайту Office 365. Помимо действий по установке и подключения видео рассматривается другие полезные сведения об использовании Windows PowerShell для удаленных подготовки.

### <a name="using-csom-code-to-extract-a-provisioning-template"></a>С помощью CSOM код для извлечения подготовки шаблона

Использовать код CSOM/REST для извлечения подготовки шаблона, просто Создание проекта разработки с помощью Visual Studio или другой среды разработки. Создание любого типа проекта&mdash;, например консоли или приложение Windows или надстройки SharePoint. После создания проекта разработки, необходимо установить основной библиотеки, которое входит в виде пакета NuGet.

**Примечание:**  Инструкции для поиска и установка основного пакета NuGet библиотеки и пошаговое руководство для удаленных подготовки образец консольного приложения, доступны в [Пример подготовки консольного приложения](provisioning-console-application-sample.md). Обратите внимание, что библиотека базовых поставляется как две версии: один предназначен для SharePoint Online, SharePoint 2013 и Office 365; и один предназначен для SharePoint 2013 в локальной.

Хотя подробные инструкции по использованию CSOM в [Пример подготовки консольного приложения](provisioning-console-application-sample.md), общий обзор — это следующим образом:

1. Создание подключения к Office 365.
    
2. Создайте экземпляр **ClientContext** и получить ссылку на объект **Web** .
    
3. Библиотека базовых расширение метод **GetProvisioningTemplate**используется для извлечения объекта **ProvisioningTemplate** .
    
4. Сохранение подготовки экземпляра шаблона в выбранное местоположение файла с помощью шаблона поставщика и сериализации форматирования данных.
    
    **Примечание:**  Так как можно настроить поставщика шаблона и объекты форматирования данных сериализации, можно реализовать любые сохраняемость хранилища и сериализации форматирование вы хотите. Стандартной, PnP модуля подготовки поддерживает файловой системы, SharePoint и Azure больших двоичных объектов поставщиков шаблон хранилища. Он также поддерживает форматирования данных сериализации XML и JSON.

Можно просмотреть пример выходных данных сериализации XML и Дополнительные сведения о сериализации XML-схему в статье [PnP подготовки схемы](pnp-provisioning-schema.md) . Вы также можете получить схемы и документация на репозиториев:[SharePoint/PnP-подготовки-схемы](https://github.com/SharePoint/PnP-Provisioning-Schema/). Кроме того, видео [канала 9](https://channel9.msdn.com/) &mdash;[глубокое погружение в PnP подготовки схемы модуля](https://channel9.msdn.com/blogs/OfficeDevPnP/Deep-dive-to-PnP-provisioning-engine-schema)&mdash;, который содержит описание и обсуждение схемы.

Тем не менее, что модуль подготовки поддерживает модель домена сериализации зависящий от формата важно. На самом деле модуль подготовки полностью несвязанные из любой формат сериализации. Это можно вручную определить экземпляр **ProvisioningTemplate** . Либо выберите узел бизнес-моделей или создания XML-документа, которое проверяет PnP подготовки схемы или писать код .NET и создания иерархия объектов. Можно даже смешивать этих подходов. Также можно создать подготовки шаблона, с помощью узла бизнес-моделей и затем сохраните его в XML-файл и выполните ряд настроек в памяти при обработке экземпляра **ProvisioningTemplate** в коде.

#### <a name="example-code-to-extract-a-template-using-getprovisioningtemplate"></a>Пример кода для извлечения шаблона с помощью GetProvisioningTemplate

В статье [Пример консольного приложения подготовки](provisioning-console-application-sample.md) демонстрируются с помощью метода **GetProvisioningTemplate** . В образце процесса экспорта подготовки шаблон выполняется в следующем блоке кода.

```
ProvisioningTemplateCreationInformation ptci = new ProvisioningTemplateCreationInformation(ctx.Web);

// Create FileSystemConnector, so that we can store composed files somewhere temporarily 
ptci.FileConnector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
ptci.PersistComposedLookFiles = true;
ptci.ProgressDelegate = delegate (String message, Int32 progress, Int32 total)
{

// Use this to simply output progress to the console application UI
Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
};

// Execute actual extraction of the tepmplate
ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);
```

### <a name="apply-the-provisioning-template"></a>Применение подготовки шаблона

Как и с извлечении подготовки шаблона можно применить настраиваемого экземпляра объекта **ProvisioningTemplate** с помощью кода CSOM/REST или команд Windows PowerShell. [Команды SharePointPnP.PowerShell](https://github.com/SharePoint/PnP-PowerShell) можно загрузить из репозитория на репозиториев.

Если применение подготовки шаблона с помощью методов расширения из основной библиотеки, у вас есть похоже на пример блока кода ниже. В примере шаблон применяется к целевого сайта с помощью метода расширения **ApplyProvisioningTemplate** типа **Web** .

```
using (var context = new ClientContext(destinationUrl))
{
  context.Credentials = new SharePointOnlineCredentials(userName, password);
  Web web = context.Web;
  context.Load(web, w => w.Title);
  context.ExecuteQueryRetry();

  // Configure the XML file system provider
  XMLTemplateProvider provider =
  new XMLFileSystemTemplateProvider(
    String.Format(@"{0}\..\..\",
    AppDomain.CurrentDomain.BaseDirectory),
    "");

  // Load the template from the XML stored copy
  ProvisioningTemplate template = provider.GetTemplate(
    "<template name>.xml");

  // Apply the template to another site
  Console.WriteLine("Start: {0:hh.mm.ss}", DateTime.Now);

  // We can also use Apply-PnPProvisioningTemplate
  web.ApplyProvisioningTemplate(template);

  Console.WriteLine("End: {0:hh.mm.ss}", DateTime.Now);
}
```

После создания подключения к SharePoint Online с помощью команды Windows PowerShell использовать командлет **Применить PnPProvisioningTemple** , как показано ниже.

```
Apply-PnProvisioningTemplate -Path "PnP-Provisioning-File.xml"
```

Обратите внимание, что `-Path` аргумент указывает путь к файлу для подготовки файл шаблона, в которой сохраняется в файловую систему. В блоке кода выше сохраненный файл находится в XML-файл, но эти файлы шаблонов могут быть сохранены в любой сериализованных формат, который вы хотите.

## <a name="pnp-core-library"></a>Библиотека PnP основных компонентов

Библиотека базовых (OfficeDevPnP.Core) — это объектная модель CSOM/REST, поддерживающем платформу PnP подготовки и позволяющая PnP модуля подготовки. Он состоит из нескольких пространств имен, включая набор [методов](https://msdn.microsoft.com/en-us/library/bb383977.aspx). Эти методы расширения объектной модели SharePoint для поддержки удаленного подготовки, а также объекты для обработки сущностей, задания таймера, подготовки шаблонов и полностью подготовки framework. В таблице 1 перечислены пространства имен в основной библиотеки.

**В таблице 1. Пространства имен в библиотеке OfficeDevPnP.Core**

|**Пространство имен**|**Описание**|
|:-----|:-----|
|OfficeDevPnP.Core||
|OfficeDevPnP.Core.AppModelExtensions|Классы .NET, расширение существующего типа с помощью дополнительных методов.|
|OfficeDevPnP.Core.Entities|Классы, используемые для предоставления и получения более сложных объектов с помощью методов расширения в AppModelExtensions.|
|OfficeDevPnP.Core.Enums|Набор перечислений, которые поддерживают операции подготовки.|
|OfficeDevPnP.Core.Extensions|Методы расширения, которые не являются SharePoint, связанных с, такие как методы, позволяющие со строками.|
|OfficeDevPnP.Core.Framework.ObjectHandlers.TokenDefinitions|Маркеры, используемые для замены определенных контента сайта в объекте шаблона.|
|OfficeDevPnP.Core.Framework.Provisioning.Connectors|Соединители используются для подключения различных источников данных места хранения шаблонов и средств.|
|OfficeDevPnP.Core.Framework.Provisioning.Extensibility|Расширяемость поставщика кода. Поставщики расширяемости можно использовать для добавления функций, который изначально не поддерживается обработчиком.|
|OfficeDevPnP.Core.Framework.Provisioning.Model|Объекты модели данных шаблона. Шаблоны извлечены или отзыва сериализованным фактический код C#. Это пространство имен содержит классы для эту структуру.|
|OfficeDevPnP.Core.Framework.Provisioning.ObjectHandlers|Обработчики для поддержки извлечения шаблона и создания элементов SharePoint.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers|Пространство имен для базового шаблона поставщика. Поставщики шаблона используются для сериализации или отмены сериализации на основе кода модели для определенных форматов.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Json|Поставщик шаблон JSON для сериализации или отзыва сериализации шаблоны на основе кода или из формате JSON.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml|Поставщик шаблон XML для сериализации или отзыва сериализации шаблоны на основе кода или из формата XML.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml.V201503|Автоматически созданные файлы схемы для v201503 версии схемы.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml.V201505|Автоматически созданные файлы схемы для v201505 версии схемы.|
|OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml.V201508|Автоматически созданные файлы схемы для v201508 версии схемы.|

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Подготовка пример консольного приложения](provisioning-console-application-sample.md)
    
- [Команды SharePointPnP.PowerShell](https://github.com/SharePoint/PnP-PowerShell)
    
- [Подготовка пример консольного приложения](provisioning-console-application-sample.md)
    
- [SharePoint/PnP подготовки схемы](https://github.com/SharePoint/Pnp-Provisioning-Schema/)
    
- [Методы расширения](https://msdn.microsoft.com/en-us/library/bb383977.aspx)
