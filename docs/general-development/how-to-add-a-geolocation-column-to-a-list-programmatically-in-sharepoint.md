---
title: "Программный способ добавления столбца \"Географическое положение\" в список SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f31a3594-c328-4731-b8eb-5da6b85103ad
ms.openlocfilehash: 3278aba461fe9d1acbc33b5e4f24595794646e15
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-geolocation-column-to-a-list-programmatically-in-sharepoint"></a>Программный способ добавления столбца "Географическое положение" в список SharePoint
Узнайте, как для программного добавления столбца географического расположения в список SharePoint. Интегрируйте сведения о местоположении и карт в списки SharePoint и зависимостью от расположения веб-сайтов с помощью нового поля географического расположения, создание собственного типа поля на основе географического расположения.
SharePoint представлен новый тип поля с именем географического расположения, которая позволяет добавлять комментарии к списки SharePoint, содержащие сведения о расположении. В столбцах типа географического расположения можно ввести сведения о расположении в виде пары Широта и долгота координат в десятичное градусов или получить координаты текущее расположение пользователя в браузере, если он реализует интерфейс API географического расположения W3C. Дополнительные сведения о столбце географического расположения можно [интегрирование расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md). В столбце географического расположения недоступен в списки SharePoint по умолчанию. Чтобы добавить столбец к списку SharePoint, необходимо написать код. В этой статье процедура добавления поля географического расположения в список программным путем с помощью клиентской объектной модели SharePoint.
  
    
    

Пакет MSI с именем SQLSysClrTypes.msi необходимо установить на каждый интерфейсный веб-сервер SharePoint для просмотра значения поля географического расположения или данных в виде списка. Этот пакет устанавливает компоненты, которые реализуют новые типы идентификатор геометрии, geography и иерархии в SQL Server 2008. По умолчанию этот файл установлен для SharePoint Online. Тем не менее он не является локальных развертываний SharePoint. Необходимо быть членом группы администраторов фермы для выполнения этой операции. Загрузить SQLSysClrTypes.msi, можно в статье [Microsoft SQL Server 2008 R2 пакета дополнительных компонентов SP1](http://www.microsoft.com/en-us/download/details.aspx?id=26728) для SQL Server 2008 или [Пакета дополнительных компонентов Microsoft SQL Server 2012](http://www.microsoft.com/en-us/download/details.aspx?id=29065)для SQL Server 2012 в центре загрузки Майкрософт.
## <a name="prerequisites-for-adding-a-geolocation-column"></a>Необходимые условия для добавления столбца географического расположения
<a name="SP15addgeo_prereq"> </a>


  
    
    

- Доступ к списку SharePoint, имеющего достаточные права для добавления столбца.
    
  
- Действительный ключ карт Bing на уровне фермы или веб-, который можно получить из  [Центр учетных записей карт Bing](https://www.bingmapsportal.com/).
    
    > **Важные:** Обратите внимание, что вы несете ответственность за соблюдение сроками и условиями, которые применяются к использованию ключ Bing Maps и все необходимые условия для пользователей приложения о данных, передаваемых службы Bing Maps. 
- Visual Studio 2010.
    
  

## <a name="code-example-add-a-geolocation-column-to-a-list-programmatically"></a>Пример кода: Добавление столбца географического расположения в список программным путем
<a name="SP15addgeo_addcolumn"> </a>

Выполните следующие действия для добавления столбца географического расположения в список с помощью клиентской объектной модели SharePoint.
  
    
    

### <a name="to-add-the-geolocation-column-to-a-list-using-the-client-object-model"></a>Для добавления столбца географического расположения в список с помощью клиентской объектной модели


1. Запустите Visual Studio.
    
  
2. В строке меню выберите пункты **файл, создать проект**. Откроется диалоговое окно **Новый проект**.
    
  
3. В диалоговом окне **Создать проект** выберите пункт **C#** в поле **Установленные шаблоны** и затем выберите шаблон **Консольное приложение**.
    
  
4. Назовите проект и затем нажмите кнопку **ОК**.
    
  
5. Visual Studio создает проект. Добавление ссылки на следующие сборки и нажмите **кнопку ОК**.
    
    Microsoft.SharePoint.Client.dll
    
    Microsoft.SharePoint.Client.Runtime.dll
    
  
6. В файле .cs по умолчанию добавьте директиву **using** следующим образом.
    
     `using Microsoft.SharePoint.Client;`
    
  
7. Добавьте следующий код в метод **Main** в CS-файл.
    
```cs
  
class Program
    {
        static void Main(string[] args)
        {
            AddGeolocationField();
            Console.WriteLine("Location field added successfully");
        }
        private static void AddGeolocationField()
        { 
         // Replace site URL and List Title with Valid values.
            ClientContext context = new ClientContext("<Site Url>"); 
            List oList = context.Web.Lists.GetByTitle("<List Title>");
            oList.Fields.AddFieldAsXml("<Field Type='Geolocation' DisplayName='Location'/>",true, AddFieldOptions.AddToAllContentTypes);                                        
            oList.Update();
            context.ExecuteQuery();
        } 
    }
```

8. Замените \<URL-адрес сайта\> и \<заголовок списка\> с допустимыми значениями.
    
  
9.  Установка версии .NET framework в свойствах проекта по .NET Framework 4.0 или 3.5 и запустите пример.
    
  
10. Перейдите к списку. Можно видеть столбец с именем **расположение** типа географического расположения в списке. Теперь можно ввести несколько значений и Испытайте программу в действии. На рисунке 1 показано расположение по умолчанию и функции сопоставления, будут видеть в списке.
    
   **На рисунке 1. Обобщенное представление по умолчанию расположение и функции сопоставления**

  

  ![Географическое положение по умолчанию и функция сопоставления](../images/SP15Con_HowToAddGeolocationColumnUpdated_Fig1.png)
  

  

  

## <a name="add-a-list-item-with-the-geolocation-field-value-to-a-sharepoint-list-programmatically"></a>Добавление элемента списка со значением поля географического расположения в список SharePoint программными средствами
<a name="SP15addgeo_addlistitem"> </a>

После географического расположения добавляется поле со списком SharePoint, разработчик может добавить элемент списка в список программными средствами. Существует два способа для программного добавления элемента списка:, передав объект **FieldGeolocationValue** для поля географического расположения, а также с передачей **Начальное значение** для поля географического расположения.
  
    
    

### <a name="method-a-pass-the-fieldgeolocationvalue-object-to-the-geolocation-field"></a>Метод A: передайте этот объект FieldGeolocationValue поля географического расположения


- Следующий метод добавляет элемент списка, передав значение географическое положение как объект.
    
```cs
  
private void AddListItem()
        {   // Replace site URL and List Title with Valid values.
            ClientContext context = new ClientContext("<Site Url>");
            List oList = context.Web.Lists.GetByTitle("<List Name>");

            ListItemCreationInformation itemCreationInfo = new ListItemCreationInformation();
            ListItem oListItem = oList.AddItem(itemCreationInfo);

            oListItem["Title"] = "New Title";

            FieldGeolocationValue oGeolocationValue = new FieldGeolocationValue();
            oGeolocationValue.Latitude = (double)17.4;
            oGeolocationValue.Longitude = (double)78.4;
            oListItem["location"] = oGeolocationValue;

            oListItem.Update();
            context.ExecuteQuery();
        }

```


### <a name="method-b-pass-a-raw-value-to-the-geolocation-field"></a>Метод B: передайте начальное значение для поля географического расположения


- Следующий метод добавляет элемент списка в список SharePoint, передавая необработанные значения поля географического расположения.
    
```cs
  
private void AddListItem()
        {   // Replace site URL and List Title with Valid values.
            ClientContext context = new ClientContext("<Site Url>");
            List oList = context.Web.Lists.GetByTitle("<List Name>");

            ListItemCreationInformation itemCreationInfo = new ListItemCreationInformation();
            ListItem oListItem = oList.AddItem(itemCreationInfo);

            oListItem["Title"] = "New Title";
             // Data in WKT (World Known Text) format.
            oListItem["location"] = "POINT (78.4 17.4)" ; 

            oListItem.Update();
            context.ExecuteQuery();
        }

```


## <a name="see-also"></a>См. также
<a name="SP15addgeo_addlresources"> </a>


-  [Интеграция расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [Как: задать ключ карт Bing на уровне веб-серверы и фермы в SharePoint](how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint.md)
    
  
-  [Как: расширение типа поля географического расположения, с использованием обработки на стороне клиента](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  
-  [Создание представления карты для поля географического расположения в SharePoint](create-a-map-view-for-the-geolocation-field-in-sharepoint.md)
    
  
-  [Как: интеграция карт с помощью приложения для Windows Phone и списки SharePoint](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [Использование типа поля расположения SharePoint в мобильных приложениях](http://technet.microsoft.com/en-us/library/fp161355%28v=office.15%29.aspx)
    
  

