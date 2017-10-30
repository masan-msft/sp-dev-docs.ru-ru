---
title: "Добавление столбца географического расположения в список программными средствами в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f31a3594-c328-4731-b8eb-5da6b85103ad
ms.openlocfilehash: b38685e7f5ae5bd54c68a07ad73e65b9466d7bfa
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint"></a><span data-ttu-id="8412f-102">Как: Добавление столбца географического расположения списка программными средствами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8412f-102">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>
<span data-ttu-id="8412f-103">Узнайте, как для программного добавления столбца географического расположения в список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8412f-103">Learn how to programmatically add a Geolocation column to a list in SharePoint.</span></span> <span data-ttu-id="8412f-104">Интегрируйте сведения о местоположении и карт в списки SharePoint и зависимостью от расположения веб-сайтов с помощью нового поля географического расположения, создание собственного типа поля на основе географического расположения.</span><span class="sxs-lookup"><span data-stu-id="8412f-104">Integrate location information and maps in SharePoint lists and location-based websites by using the new Geolocation field creating your own Geolocation-based field type.</span></span>
<span data-ttu-id="8412f-105">SharePoint представлен новый тип поля с именем географического расположения, которая позволяет добавлять комментарии к списки SharePoint, содержащие сведения о расположении.</span><span class="sxs-lookup"><span data-stu-id="8412f-105">SharePoint introduces a new field type named Geolocation that enables you to annotate SharePoint lists with location information.</span></span> <span data-ttu-id="8412f-106">В столбцах типа географического расположения можно ввести сведения о расположении в виде пары Широта и долгота координат в десятичное градусов или получить координаты текущее расположение пользователя в браузере, если он реализует интерфейс API географического расположения W3C.</span><span class="sxs-lookup"><span data-stu-id="8412f-106">In columns of type Geolocation, you can enter location information as a pair of latitude and longitude coordinates in decimal degrees or retrieve the coordinates of the user's current location from the browser if it implements the W3C Geolocation API.</span></span> <span data-ttu-id="8412f-107">Дополнительные сведения о столбце географического расположения можно [интегрирование расположение и карты функциональные возможности в SharePoint](integrating-location-and-map-functionality-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="8412f-107">For more information about the Geolocation column, see [Integrating location and map functionality in SharePoint](integrating-location-and-map-functionality-in-sharepoint.md).</span></span> <span data-ttu-id="8412f-108">В столбце географического расположения недоступен в списки SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8412f-108">The Geolocation column is not available by default in SharePoint lists.</span></span> <span data-ttu-id="8412f-109">Чтобы добавить столбец к списку SharePoint, необходимо написать код.</span><span class="sxs-lookup"><span data-stu-id="8412f-109">To add the column to a SharePoint list, you have to write code.</span></span> <span data-ttu-id="8412f-110">В этой статье процедура добавления поля географического расположения в список программным путем с помощью клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8412f-110">In this article, learn how to add the Geolocation field to a list programmatically by using the SharePoint client object model.</span></span>
  
    
    

<span data-ttu-id="8412f-111">Пакет MSI с именем SQLSysClrTypes.msi необходимо установить на каждый интерфейсный веб-сервер SharePoint для просмотра значения поля географического расположения или данных в виде списка.</span><span class="sxs-lookup"><span data-stu-id="8412f-111">An MSI package named SQLSysClrTypes.msi must be installed on every SharePoint front-end web server to view the geolocation field value or data in a list.</span></span> <span data-ttu-id="8412f-112">Этот пакет устанавливает компоненты, которые реализуют новые типы идентификатор геометрии, geography и иерархии в SQL Server 2008.</span><span class="sxs-lookup"><span data-stu-id="8412f-112">This package installs components that implement the new geometry, geography, and hierarchy ID types in SQL Server 2008.</span></span> <span data-ttu-id="8412f-113">По умолчанию этот файл установлен для SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8412f-113">By default, this file is installed for SharePoint Online.</span></span> <span data-ttu-id="8412f-114">Тем не менее он не является локальных развертываний SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8412f-114">However, it is not for an on-premises deployment of SharePoint.</span></span> <span data-ttu-id="8412f-115">Необходимо быть членом группы администраторов фермы для выполнения этой операции.</span><span class="sxs-lookup"><span data-stu-id="8412f-115">You must be a member of the Farm Administrators group to perform this operation.</span></span> <span data-ttu-id="8412f-116">Загрузить SQLSysClrTypes.msi, можно в статье [Microsoft SQL Server 2008 R2 пакета дополнительных компонентов SP1](http://www.microsoft.com/en-us/download/details.aspx?id=26728) для SQL Server 2008 или [Пакета дополнительных компонентов Microsoft SQL Server 2012](http://www.microsoft.com/en-us/download/details.aspx?id=29065)для SQL Server 2012 в центре загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8412f-116">To download SQLSysClrTypes.msi, see  [Microsoft SQL Server 2008 R2 SP1 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=26728) for SQL Server 2008, or [Microsoft SQL Server 2012 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=29065)for SQL Server 2012 in the Microsoft Download Center.</span></span>
## <a name="prerequisites-for-adding-a-geolocation-column"></a><span data-ttu-id="8412f-117">Необходимые условия для добавления столбца географического расположения</span><span class="sxs-lookup"><span data-stu-id="8412f-117">Prerequisites for adding a Geolocation column</span></span>
<span data-ttu-id="8412f-118"><a name="SP15addgeo_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="8412f-118"></span></span>


  
    
    

- <span data-ttu-id="8412f-119">Доступ к списку SharePoint, имеющего достаточные права для добавления столбца.</span><span class="sxs-lookup"><span data-stu-id="8412f-119">Access to a SharePoint list, with sufficient privileges to add a column.</span></span>
    
  
- <span data-ttu-id="8412f-120">Действительный ключ карт Bing на уровне фермы или веб-, который можно получить из  [Центр учетных записей карт Bing](https://www.bingmapsportal.com/).</span><span class="sxs-lookup"><span data-stu-id="8412f-120">A valid Bing Maps key set at the farm or web level, which can be obtained from the  [Bing Maps Account Center](https://www.bingmapsportal.com/).</span></span>
    
    > <span data-ttu-id="8412f-121">**Важные:** Обратите внимание, что вы несете ответственность за соблюдение сроками и условиями, которые применяются к использованию ключ Bing Maps и все необходимые условия для пользователей приложения о данных, передаваемых службы Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="8412f-121">**Important:** Please note that you are responsible for compliance with terms and conditions applicable to your use of the Bing Maps key, and any necessary disclosures to users of your application regarding data passed to the Bing Maps service.</span></span> 
- <span data-ttu-id="8412f-122">Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="8412f-122">Visual Studio 2010.</span></span>
    
  

## <a name="code-example-add-a-geolocation-column-to-a-list-programmatically"></a><span data-ttu-id="8412f-123">Пример кода: Добавление столбца географического расположения в список программным путем</span><span class="sxs-lookup"><span data-stu-id="8412f-123">Code example: Add a Geolocation column to a list programmatically</span></span>
<span data-ttu-id="8412f-124"><a name="SP15addgeo_addcolumn"> </a></span><span class="sxs-lookup"><span data-stu-id="8412f-124"></span></span>

<span data-ttu-id="8412f-125">Выполните следующие действия для добавления столбца географического расположения в список с помощью клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8412f-125">Follow these steps to add the Geolocation column to a list using the SharePoint client object model.</span></span>
  
    
    

### <a name="to-add-the-geolocation-column-to-a-list-using-the-client-object-model"></a><span data-ttu-id="8412f-126">Для добавления столбца географического расположения в список с помощью клиентской объектной модели</span><span class="sxs-lookup"><span data-stu-id="8412f-126">To add the Geolocation column to a list using the client object model</span></span>


1. <span data-ttu-id="8412f-127">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8412f-127">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="8412f-p103">В строке меню выберите пункты **файл, создать проект**. Откроется диалоговое окно **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="8412f-p103">On the menu bar, choose **File, New Project**. The **New Project** dialog box opens.</span></span>
    
  
3. <span data-ttu-id="8412f-130">В диалоговом окне **Создать проект** выберите пункт **C#** в поле **Установленные шаблоны** и затем выберите шаблон **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="8412f-130">In the **New Project** dialog box, choose **C#** in the **Installed Templates** box, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="8412f-131">Назовите проект и затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8412f-131">Give the project a name, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="8412f-p104">Visual Studio создает проект. Добавление ссылки на следующие сборки и нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="8412f-p104">Visual Studio creates the project. Add a reference to the following assemblies, and choose **OK**.</span></span>
    
    <span data-ttu-id="8412f-134">Microsoft.SharePoint.Client.dll</span><span class="sxs-lookup"><span data-stu-id="8412f-134">Microsoft.SharePoint.Client.dll</span></span>
    
    <span data-ttu-id="8412f-135">Microsoft.SharePoint.Client.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="8412f-135">Microsoft.SharePoint.Client.Runtime.dll</span></span>
    
  
6. <span data-ttu-id="8412f-136">В файле .cs по умолчанию добавьте директиву **using** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8412f-136">In the default .cs file, add a **using** directive as follows.</span></span>
    
     `using Microsoft.SharePoint.Client;`
    
  
7. <span data-ttu-id="8412f-137">Добавьте следующий код в метод **Main** в CS-файл.</span><span class="sxs-lookup"><span data-stu-id="8412f-137">Add the following code to the **Main** method in the .cs file.</span></span>
    
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

8. <span data-ttu-id="8412f-138">Замените \<URL-адрес сайта\> и \<заголовок списка\> с допустимыми значениями.</span><span class="sxs-lookup"><span data-stu-id="8412f-138">Replace \<Site Url\> and \<List Title\> with valid values.</span></span>
    
  
9.  <span data-ttu-id="8412f-139">Установка версии .NET framework в свойствах проекта по .NET Framework 4.0 или 3.5 и запустите пример.</span><span class="sxs-lookup"><span data-stu-id="8412f-139">Set the target framework in Project Properties as .NET Framework 4.0 or 3.5, and run the example.</span></span>
    
  
10. <span data-ttu-id="8412f-p105">Перейдите к списку. Можно видеть столбец с именем **расположение** типа географического расположения в списке. Теперь можно ввести несколько значений и Испытайте программу в действии. На рисунке 1 показано расположение по умолчанию и функции сопоставления, будут видеть в списке.</span><span class="sxs-lookup"><span data-stu-id="8412f-p105">Navigate to the list. You should be able to see a column named **Location** of type Geolocation in the list. You can now enter some values and see it in action. Figure 1 shows the default location and map features that you can expect to see in your list.</span></span>
    
   <span data-ttu-id="8412f-144">**На рисунке 1. Обобщенное представление по умолчанию расположение и функции сопоставления**</span><span class="sxs-lookup"><span data-stu-id="8412f-144">**Figure 1. Summarized view of the default location and map features**</span></span>

  

  ![Географическое положение по умолчанию и функция сопоставления](../images/SP15Con_HowToAddGeolocationColumnUpdated_Fig1.png)
  

  

  

## <a name="add-a-list-item-with-the-geolocation-field-value-to-a-sharepoint-list-programmatically"></a><span data-ttu-id="8412f-146">Добавление элемента списка со значением поля географического расположения в список SharePoint программными средствами</span><span class="sxs-lookup"><span data-stu-id="8412f-146">Add a list item with the Geolocation field value to a SharePoint list programmatically</span></span>
<span data-ttu-id="8412f-147"><a name="SP15addgeo_addlistitem"> </a></span><span class="sxs-lookup"><span data-stu-id="8412f-147"></span></span>

<span data-ttu-id="8412f-p106">После географического расположения добавляется поле со списком SharePoint, разработчик может добавить элемент списка в список программными средствами. Существует два способа для программного добавления элемента списка:, передав объект **FieldGeolocationValue** для поля географического расположения, а также с передачей **Начальное значение** для поля географического расположения.</span><span class="sxs-lookup"><span data-stu-id="8412f-p106">After the Geolocation field is added to a SharePoint list, the developer can add the list item to the list programmatically. There are two ways to add the list item programmatically: by passing the **FieldGeolocationValue** object to the Geolocation field, and by passing **Raw Value** to the Geolocation field.</span></span>
  
    
    

### <a name="method-a-pass-the-fieldgeolocationvalue-object-to-the-geolocation-field"></a><span data-ttu-id="8412f-150">Метод A: передайте этот объект FieldGeolocationValue поля географического расположения</span><span class="sxs-lookup"><span data-stu-id="8412f-150">Method A: Pass the FieldGeolocationValue object to the Geolocation field</span></span>


- <span data-ttu-id="8412f-151">Следующий метод добавляет элемент списка, передав значение географическое положение как объект.</span><span class="sxs-lookup"><span data-stu-id="8412f-151">The following method adds a list item by passing the Geolocation value as an object.</span></span>
    
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


### <a name="method-b-pass-a-raw-value-to-the-geolocation-field"></a><span data-ttu-id="8412f-152">Метод B: передайте начальное значение для поля географического расположения</span><span class="sxs-lookup"><span data-stu-id="8412f-152">Method B: Pass a raw value to the Geolocation field</span></span>


- <span data-ttu-id="8412f-153">Следующий метод добавляет элемент списка в список SharePoint, передавая необработанные значения поля географического расположения.</span><span class="sxs-lookup"><span data-stu-id="8412f-153">The following method adds a list item to the SharePoint list by passing raw values to the Geolocation field.</span></span>
    
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


## <a name="additional-resources"></a><span data-ttu-id="8412f-154">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8412f-154">Additional resources</span></span>
<span data-ttu-id="8412f-155"><a name="SP15addgeo_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8412f-155"></span></span>


-  [<span data-ttu-id="8412f-156">Интеграция расположение и карты функциональные возможности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8412f-156">Integrating location and map functionality in SharePoint</span></span>](integrating-location-and-map-functionality-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8412f-157">Как: задать ключ карт Bing на уровне веб-серверы и фермы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8412f-157">How to: Set the Bing Maps key at the web and farm level in SharePoint</span></span>](how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8412f-158">Как: расширение типа поля географического расположения, с использованием обработки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="8412f-158">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  
-  [<span data-ttu-id="8412f-159">Создание представления карты для поля географического расположения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8412f-159">Create a map view for the Geolocation field in SharePoint</span></span>](create-a-map-view-for-the-geolocation-field-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8412f-160">Как: интеграция карт с помощью приложения для Windows Phone и списки SharePoint</span><span class="sxs-lookup"><span data-stu-id="8412f-160">How to: Integrate maps with Windows Phone apps and SharePoint lists</span></span>](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [<span data-ttu-id="8412f-161">Использование типа поля расположения SharePoint в мобильных приложениях</span><span class="sxs-lookup"><span data-stu-id="8412f-161">Use the SharePoint location field type in mobile applications</span></span>](http://technet.microsoft.com/en-us/library/fp161355%28v=office.15%29.aspx)
    
  

