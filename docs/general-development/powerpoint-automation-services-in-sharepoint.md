---
title: "Службы автоматизации PowerPoint в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 168c7dc0-fbdc-41a2-84db-65d211d3d673
ms.openlocfilehash: dd7ec35694d14d34fa58b3ec78591b8648063826
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="powerpoint-automation-services-in-sharepoint"></a>Службы автоматизации PowerPoint в SharePoint
Изучите использование Службы автоматизации Microsoft PowerPoint для выполнения преобразования на сервере презентации в и различные форматы файлов. 

## <a name="introduction"></a>Введение
<a name="PAS_Intro"> </a>

Многие компании, крупных и мелких, используют их библиотеки Microsoft SharePoint Server в качестве хранилища для презентаций Microsoft PowerPoint. Все эти предприятия имеют собственные конкретных нужд для хранения, распространение и обновление свои презентации. Microsoft PowerPoint Automation Services — это новая возможность Microsoft SharePoint, которые могут помочь предприятия для управления свои презентации. Это общая служба, которая предоставляет выполнять на сервере преобразование презентации в других форматах. Он был разработан с самого начала работы на серверах и могут быть обработаны много файлов презентации в виде надежного и предсказуемым.
  
    
    
С помощью Службы автоматизации PowerPoint, можно преобразовать из формата двоичного файла PowerPoint (.ppt) и в PowerPoint формат файлов Open XML (PPTX-файл) в других форматах. Например может потребоваться обновление пакета PowerPoint 97 - 2003 файлов для файлов презентация Open XML. Можно также создать дополнительное действие в меню **Правка**, чтобы разрешить пользователям создавать версию PDF презентаций по запросу.
  
> [!NOTE]
> Службы автоматизации PowerPoint использует средства SharePoint и — новым компонентом. Необходимо иметь SharePoint для использования службы автоматизации PowerPoint. При использовании SharePoint в ферме серверов, необходимо явно включить PowerPoint Automation Services. 
  
    
    


## <a name="powerpoint-automation-services-scenarios"></a>Сценарии PowerPoint Automation Services
<a name="PAS_Scenarios"> </a>

Ниже описаны несколько способов, Службы автоматизации PowerPoint можно использовать для автоматизации обработки презентаций на сервере:
  
    
    

- Большое предприятие хранятся все их годовая прибыль презентаций в одну библиотеку документов на сайте интрасети. Библиотека содержит большое число презентаций, собранные за несколько лет. Как ИТ-отдел, где требуется реализовать для обновления всех файлов презентации в PowerPoint формате двоичных файлов 97 - 2003 (.ppt) в формат файлов презентация Open XML (PPTX-файл). Разработчик, используемая для выполнения преобразования решает развернуть решение на сервере, который будет выполнять итерацию по каждому из файлов в библиотеке, проверьте, является ли файл в формате .ppt и преобразование каждого PPT-файл в формате PPTX-файл.
    
  
- Региональные отдела продаж предоставляет настраиваемые службы оценок для каждого из клиентов. Каждого продавца дается обзор их квот с клиентами в собрании, в лицо или online. После собрания, менеджер по продажам содержит копию предложения с расценками для клиента в виде PDF-файла. Отдел заключает соглашения поставщика для создания пользовательской команды в меню " **Правка** " для файлов PowerPoint, хранящиеся в библиотеке документов в их экстрасети. При выборе команды сервера запускает программу, который преобразует файл PowerPoint PDF-ФАЙЛ, расположенный в одной библиотеке.
    
  

### <a name="supported-source-presentation-formats"></a>Поддерживаемый источник форматов представления

Доступны следующие форматы презентации поддерживаемый источник для преобразования:
  
    
    

- Презентация форматов Open XML формат файлов (PPTX-файл)
    
  
- Презентация PowerPoint 97 - 2003 (.ppt)
    
  

### <a name="supported-destination-document-formats"></a>Поддерживаемые целевые форматы документов

Поддерживаемые целевые форматы документов включают все поддерживаемые форматы исходных документов и следующее:
  
    
    

- PPTX-файл (в формате презентации формат файлов open XML)
    
  
- PDF-файл
    
  
- расширением XPS (open XML Paper Specification)
    
  
- .jpg
    
  
- Рисунок в формате Portable Network Graphics
    
  

### <a name="limitations-of-powerpoint-automation-services"></a>Ограничения для службы автоматизации PowerPoint

Службы автоматизации PowerPoint не включает возможности для печати документов. Тем не менее он не вызывает затруднений для преобразования файлов PowerPoint презентации (PPT и PPTX-файл) в файл PDF или XPS и очереди их к принтеру.
  
    
    

## <a name="powerpoint-automation-services-api"></a>API-Интерфейс служб автоматизации PowerPoint
<a name="PAS_APIs"> </a>

Для использования службы автоматизации PowerPoint, используйте его API-интерфейс для отправки запросов на преобразование на сервере SharePoint. Для каждого преобразования запроса необходимо указать, какие файлы, которое требуется преобразовать и выходной формат задания преобразования. Для некоторых запросов на преобразование, также можно указать что преобразования типов контента, включая комментарии, скрытые слайды или свойств документа.
  
    
    
Службы автоматизации PowerPoint использует метод асинхронной модели для отправки и получения запросов на преобразование. Таким образом можно написать код, который продолжает выполняться после отправки запросов на преобразование. Если требуется отправлять уведомления для пользователей после завершения запросов на преобразование, можно указать делегата, который ссылается на метод обратного вызова для выполнения после завершения операции. 
  
> [!NOTE]
> [!Примечание] Дополнительные сведения о работе с помощью асинхронного шаблона разработки можно  [Асинхронного программирования Обзор](http://msdn.microsoft.com/en-us/library/ms228963.aspx). 
  
    
    

В следующих разделах содержат ограниченный список классов, которые необходимы для отправки и получения запросами преобразования. Все эти классы содержатся в пространстве имен **Microsoft.Office.Server.PowerPoint.Conversion**.
  
    
    

### <a name="request-base-class"></a>Базовый класс запроса

Класс **Request** является основных классов в пространстве имен **Microsoft.Office.Server.PowerPoint.Conversion**. Все другие типызапроса  **PresentationRequest**, **PictureRequest**, **PdfRequest**и **XpsRequest** от него. 
  
    
    

**В таблице 1. Запрос членов базового класса**


|**Имя элемента**|**Описание**|
|:-----|:-----|
|метод **BeginConvert(Microsoft.SharePoint.SPServiceContext, System.AsyncCallback, System.Object)** <br/> |Начинает операцию преобразования. Первым параметром  _serviceContext_указывает контекста сайта SharePoint, где находится файл для преобразования. Параметр  _callback_ используется для задания делегата, который ссылается на метода, выполняемого после завершения операции. Если нужно передать любые дополнительные сведения из кода, вызывающего метод обратного вызова, используйте параметр _state_. <br/> Возвращает объект  [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) . <br/> |
|метод **EndConvert(IAsyncResult)** <br/> |Завершает операцию преобразования. Параметр  _result_ ожидает результирующего объекта [IAsyncResult](https://msdn.microsoft.com/library/System.IAsyncResult.aspx) , которое возвращает соответствующего запроса **BeginConvert** преобразования. Если этот запрос не был завершен при вызове **EndConvert**, вызывающий поток блокируется до завершения операции преобразования. <br/> Не возвращает значение.  <br/> |
   

### <a name="presentationrequest-class"></a>Класс PresentationRequest

Класс **PresentationRequest**, который наследует от класса **Request**, преобразует файл PowerPoint 97 - 2003 (.ppt) или презентаций формат файлов Open XML (PPTX-файл) в другой формат презентации. В первом случае уже было сказано этот класс используется для преобразования старые файлы презентаций в библиотеке документов в формате презентаций формат файлов Open XML.
  
    
    
Метод-конструктор для класса **PresentationRequest** содержит три требуемые параметры:
  
    
    

-  _input_ файл, который требуется выполнить преобразование как объект  [Stream](https://msdn.microsoft.com/library/System.IO.Stream.aspx) .
    
  
-  _extension_ строка, указывающая расширение файла преобразуемого файла.
    
  
-  _output_ объект  [SPFileStream](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfilestream.aspx) , указывающий, где будут храниться выходные данные.
    
  
Класс **PresentationRequest** имеет один перегрузки для метода конструктора, добавляющий параметр _settings_. Параметр _settings_ объект **PresentationSettings** принимает в качестве аргумента.
  
    
    

> **Совет:** При преобразовании выходные данные [потока](https://msdn.microsoft.com/library/System.IO.Stream.aspx) объекта обратно на объект [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) проверьте, что данное расширение имени файла, присвоенное созданный файл сопоставляет расширение типа файлов, которое (PPT или PPTX-файл).
  
    
    


### <a name="pdfrequest-class"></a>Класс PdfRequest

Класс **PdfRequest**, который наследуется от класса **Request**, преобразует файл PowerPoint 97 - 2003 (.ppt) или презентаций формат файлов Open XML (PPTX-файл) в файл a.pdf. Во втором сценарии уже было сказано этот класс используется для преобразования в PDF-файлов презентаций.
  
    
    
Метод-конструктор для класса **PdfRequest** также содержит три параметра требуется  _input_,  _extension_и  _output_ следующий класс **PresentationRequest**.
  
    
    
Класс **PdfRequest** также имеет один перегрузки для метода конструктора, добавляющий параметр _settings_. Параметр _settings_ объект **FixedFormatSettings** принимает в качестве аргумента.
  
    
    

> **Совет:** При преобразовании выходные данные [потока](https://msdn.microsoft.com/library/System.IO.Stream.aspx) объекта обратно на объект [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) проверьте, что данное расширение имени файла, присвоенное созданный файл сопоставляет расширение типа файлов, которые должны (PDF-файл).
  
    
    


### <a name="picturerequest-class"></a>Класс PictureRequest

Класс **PictureRequest**, который наследуется от класса **Request**, преобразует PowerPoint 97 - 2003 файла (.ppt) или презентаций формат файлов Open XML (PPTX-файл) в коллекцию файлы изображений в формате the.jpg или PNG.
  
    
    
Метод-конструктор для класса **PictureRequest** также имеет четыре требуемые параметры. Параметры _input_,  _extension_и  _output_ похожи на параметры для конструктора класса **PresentationRequest**. Метод-конструктор для класса **PictureRequest** также имеет параметр необходимые _format_, должна быть константа из перечисления **PictureFormat**.
  
    
    
Класс **PictureRequest** имеет любой перегрузки метода конструктора.
  
    
    

> **Совет:** Класс **PictureRequest** возвращает поток, содержащий пакет файлы изображений. При преобразовании выходные данные [потока](https://msdn.microsoft.com/library/System.IO.Stream.aspx) объекта обратно в объект [SPFile](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfile.aspx) , убедитесь, что данное расширение имени файла, присвоенное созданный файл .zip.
  
    
    


## <a name="building-a-powerpoint-automation-services-application"></a>Создание приложения PowerPoint Automation Services
<a name="PAS_Build"> </a>

Это самый простой способ показано, как писать код, использующий Службы автоматизации PowerPoint является создание консольного приложения. Необходимо построение и запуск консольного приложения на SharePoint Server, а не на клиентском компьютере. Для запуска запросов на преобразование тот же ли код запроса преобразования является частью веб-части, рабочего процесса или обработчик событий. С помощью Службы автоматизации PowerPoint консольного приложения, следующей процедуре показано, как использовать API без добавления сложности веб-части, обработчик событий или рабочего процесса.
  
> [!NOTE]
> Так как PowerPoint Automation Services — это служба SharePoint, его можно использовать только в приложении, на котором выполняется непосредственно на сервере SharePoint Server. Необходимо создать приложение, как решение фермы. Нельзя использовать PowerPoint Automation Services из изолированного решения. 
  
    
    


### <a name="to-build-the-application"></a>Построение приложения


1. Запустите приложение Microsoft Visual Studio 2012.
    
  
2. В меню **файл** выберите команду **Создать** и затем выберите **проект**. 
    
  
3. В диалоговом окне **Новый проект** в разделе **Установленные** **Шаблоны**, разверните узел **Visual C#** и выберите **Windows**.
    
  
4. В списке шаблонов проектов выберите пункт **Консольное приложение**.
    
  
5. Убедитесь, что проект в Visual Studio предназначен для .NET Framework 4.
    
    > [!NOTE]
    > [!Примечание] Предыдущие версии SharePoint Server требуется, предназначенных для .NET Framework 3.5. Теперь библиотек Microsoft.SharePoint ссылок на сборки в .NET Framework 4. Убедиться в том, что проект предназначен для полного .NET Framework 4 и не .NET Framework 4 профиля клиента. 

6. В поле **имя** введите имя, которое вы хотите использовать для проекта, например PAS_Sample.
    
  
7. В поле **Расположение** укажите место для сохранения проекта.
    
  
8. Нажмите кнопку **ОК**, чтобы создать решение.
    
  
9. По умолчанию Visual Studio 2012 создаются проекты, процессоров x 86, но создавать SharePoint Server приложения, следует задать любой Процессор.
    
    При создании приложения Microsoft Visual C#, в **Окне Обозреватель решений** щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.
    
  - В окне **свойств** проекта щелкните **Построить**.
    
  
  - Укажите на список **конфигурации** и выберите пункт **Все конфигурации**.
    
  
  - Укажите на список **Целевая платформа** и выберите **Любой ЦП**.
    
  

    
    
    При создании Microsoft Visual Basic приложения .NET Framework, в окне **Свойства** щелкните **Компиляция**.
    
  - Щелкните **Дополнительные параметры компиляции**.
    
  
  - Укажите на список **конфигурации**, а затем выберите **Все конфигурации**.
    
  
  - Укажите на список **Целевая платформа** и выберите **Любой ЦП**.
    
  

    
    
  
10. В меню **Проект** выберите команду **Добавить ссылку**. Откроется диалоговое окно **Добавление ссылки**.
    
  
11. Разверните узел **сборки**, а затем выполните следующее:
    
  - Разверните узел **Framework**, а затем добавьте ссылку на System.Web.
    
  
  - Разверните узел **расширения**, а затем добавьте ссылку на Microsoft.SharePoint.
    
  
12. Также в диалоговом окне **Добавление ссылки** нажмите кнопку **Обзор**, перейдите в расположение для Microsoft.Office.Server.PowerPoint.dll, (C:\\Windows\\Microsoft.NET\\assembly\\GAC_MSIL\\Microsoft.Office.Server.PowerPoint\\v4.0_15.0.0.0__71e9bce111e9429c  это местоположение по умолчанию), выберите сборку и нажмите кнопку **Добавить**. 
    
  
В следующих примерах C# и Visual Basic показано это приложение простого Службы автоматизации PowerPoint, преобразует PowerPoint файла 97 - 2003 (.ppt) в папке общих документов на сайте SharePoint для файла PowerPoint Open XML (PPTX-файл) в той же папке.
  
    
    



```cs

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Web;
using Microsoft.SharePoint;
using Microsoft.Office.Server.PowerPoint.Conversion;

namespace PAS_Sample
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                string siteURL = "http://localhost";
                using (SPSite site = new SPSite(siteURL))
                {
                    using (SPWeb web = site.OpenWeb())
                    {
                        Console.WriteLine("Begin conversion");

                        // Get a reference to the "Shared Documents" library 
                        // and the presentation file to be converted.
                        SPFolder docs = web.Folders[siteURL + 
                            "/Shared Documents"];
                        SPFile file = docs.Files[siteURL + 
                            "/Shared Documents/Pres1.ppt"];

                        // Convert the file to a stream and create an
                        // SPFileStream object for the conversion output.
                        Stream fStream = file.OpenBinaryStream();
                        SPFileStream stream = new SPFileStream(web, 0x1000);

                        // Create the presentation conversion request.
                        PresentationRequest request = new PresentationRequest(
                            fStream,
                            ".ppt",
                            stream);

                        // Send the request synchronously, passing
                        // in a 'null' value for the callback parameter, 
                        // and capturing the response in the result object.
                        IAsyncResult result = request.BeginConvert(
                            SPServiceContext.GetContext(site),
                            null,
                            null);

                        // Use the EndConvert method to get the result. 
                        request.EndConvert(result);

                        // Add the converted file to the document library.
                        SPFile newFile = docs.Files.Add(
                            "newPres1.pptx", 
                            stream, 
                            true);
                        Console.WriteLine("Output: {0}", newFile.Url);

                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error: " + ex.Message);
            }
            finally
            {
                Console.WriteLine("Complete");
                Console.ReadKey();
            }
        }
    }
}
```




```VB.net

Imports System
Imports System.Collections.Generic
Imports System.IO
Imports System.Linq
Imports System.Text
Imports System.Web
Imports Microsoft.SharePoint
Imports Microsoft.Office.Server.PowerPoint.Conversion

Namespace PAS_Sample
    Class Program
        Private Shared Sub Main(args As String())
            Try
                Dim siteURL As String = "http://localhost"
                Using site As New SPSite(siteURL)
                    Using web As SPWeb = site.OpenWeb()
                        Console.WriteLine("Begin conversion")

                        ' Get a reference to the "Shared Documents" library 
                        ' and the presentation file to be converted.
                        Dim docs As SPFolder = web.Folders(siteURL + _
                            "/Shared Documents")
                        Dim file As SPFile = docs.Files(siteURL + _
                            "/Shared Documents/Pres1.ppt")

                        ' Convert the file to a stream and create an
                        ' SPFileStream object for the conversion output.
                        Dim fStream As Stream = file.OpenBinaryStream()
                        Dim stream As New SPFileStream(web, &amp;H1000)

                        ' Create the presentation conversion request.
                        Dim request As New PresentationRequest(fStream, _
                            ".ppt", 
                            stream)

                        ' Send the request synchronously, passing
                        ' in a Nothing value for the callback parameter, 
                        ' and capturing the response in the result object.
                        Dim result As IAsyncResult = request.BeginConvert(_
                            SPServiceContext.GetContext(site), _
                            Nothing, _
                            Nothing)

                        ' Use the EndConvert method to get the result. 
                        request.EndConvert(result)

                        ' Add the converted file to the document library.
                        Dim newFile As SPFile = docs.Files.Add(_
                            "newPres1.pptx", _
                            stream, _
                            True)

                        Console.WriteLine("Output: {0}", newFile.Url)
                    End Using
                End Using
            Catch ex As Exception
                Console.WriteLine("Error: " + ex.Message)
            Finally
                Console.WriteLine("Complete")
                Console.ReadKey()
            End Try
        End Sub
    End Class
End Namespace

```


### <a name="to-build-and-run-the-example"></a>Построение и запуск примера


1. Добавьте документ PowerPoint с именем Pres1.ppt в папку общих документов на сайте SharePoint.
    
  
2. Постройте и запустите пример.
    
  
3. Истечении одной минуты для запуска процесса преобразования, перейдите в папку "Общие документы" на сайте SharePoint и обновить страницу. Библиотека документов теперь содержит новый документ PowerPoint, Pres1.pptx.
    
  
Службы автоматизации PowerPoint на SharePoint предоставляет бизнеса с расширенными возможностями для управления их файлы презентаций. В этом решении высокой производительности позволяет управлять презентации масштабируемый, на сервере, формирования, как пакет или по запросу. 
  
> [!NOTE]
> Прежде чем выполнять пример, убедитесь в том, что службы автоматизации PowerPoint была включена в консоли центра администрирования SharePoint.<br/>  Чтобы убедиться, что включен PowerPoint Automation Services, выполните следующие действия. <ul><li>В консоли центра администрирования в разделе **Параметры системы**выберите **Управление службами на сервере**и убедитесь в том, что **Службы преобразования PowerPoint** установлено значение **запущено**. </li><li>Также в консоли центра администрирования в разделе **Управление приложениями**выберите **Управление приложениями-службами**, а затем убедитесь, что **Приложение службы преобразования PowerPoint** и **службы преобразования PowerPoint Прокси-сервер приложения** установлено значение запущено.</li></ul>
  
    
    


## <a name="conclusion"></a>Заключение
<a name="PAS_Conclusion"> </a>

Службы автоматизации PowerPoint на SharePoint предоставляет бизнеса с расширенными возможностями для управления их файлы презентаций. В этом решении высокой производительности позволяет управлять презентации масштабируемый, на сервере, формирования, как пакет или по запросу. 
  
    
    

## <a name="see-also"></a>См. также
<a name="PAS_Additional"> </a>


-  [Разработка с помощью SharePoint 2010 Word Automation Services](http://msdn.microsoft.com/en-us/library/ff742315.aspx)
    
  
-  [Центр разработчиков PowerPoint](http://msdn.microsoft.com/en-us/office/aa905465)
    
  
-  [Центр по разработке для SharePoint](http://msdn.microsoft.com/en-us/sharepoint/default.aspx)
    
  

