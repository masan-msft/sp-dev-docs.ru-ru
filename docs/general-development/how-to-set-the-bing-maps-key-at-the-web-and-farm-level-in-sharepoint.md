---
title: "Настройка ключа службы \"Карты Bing\" в SharePoint на уровне фермы и веб-сайта"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 507ed9de-c349-44b5-b182-e838795dd862
ms.openlocfilehash: 2414eef9bc3f1781d02c33fbfeaa5824e161b5d9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint"></a><span data-ttu-id="8694f-102">Настройка ключа службы "Карты Bing" в SharePoint на уровне фермы и веб-сайта</span><span class="sxs-lookup"><span data-stu-id="8694f-102">Set the Bing Maps key at the web and farm level in SharePoint</span></span>

![Раздел "Инструкции"](../images/mod_icon_howto.png)

<span data-ttu-id="8694f-104">Узнайте, как программно задать ключ Карт Bing на веб-уровне и уровне фермы с помощью клиентской объектной модели SharePoint и Windows PowerShell, чтобы включить функционал Карт Bing в списке SharePoint, а также в веб-приложениях и мобильных приложениях на основе местоположения.</span><span class="sxs-lookup"><span data-stu-id="8694f-104">Learn how to set the Bing Maps key programmatically at the web and farm level by using the SharePoint client object model and Windows PowerShell, to enable the Bing Maps functionality in SharePoint lists and location-based web and mobile apps.</span></span>

## <a name="prerequisites-for-setting-the-bing-maps-key"></a><span data-ttu-id="8694f-105">Необходимые условия для установки ключ Bing Maps</span><span class="sxs-lookup"><span data-stu-id="8694f-105">Prerequisites for setting the Bing Maps key</span></span>
<span data-ttu-id="8694f-106"><a name="SP15Bing_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="8694f-106"></span></span>

<span data-ttu-id="8694f-107">Для выполнения действия, описанные в этом примере, необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="8694f-107">To follow the steps in this example, you should have the following:</span></span>
  
    
    

- <span data-ttu-id="8694f-108">SharePoint с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8694f-108">SharePoint, with administrative privileges.</span></span>
    
  
- <span data-ttu-id="8694f-109">Действительный ключ Bing Maps, который можно получить из  [Центр учетных записей карт Bing](https://www.bingmapsportal.com/).</span><span class="sxs-lookup"><span data-stu-id="8694f-109">A valid Bing Maps key, which you can obtain from the  [Bing Maps Account Center](https://www.bingmapsportal.com/).</span></span>
    
    > <span data-ttu-id="8694f-110">**Важные:** Обратите внимание, что вы несете ответственность за соблюдение сроками и условиями, которые применяются к использованию ключ Bing Maps и все необходимые условия для пользователей приложения о данных, передаваемых службы Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="8694f-110">**Important:** Please note that you are responsible for compliance with terms and conditions applicable to your use of the Bing Maps key, and any necessary disclosures to users of your application regarding data passed to the Bing Maps service.</span></span> 

## <a name="code-example-set-the-bing-maps-key-at-the-farm-or-web-level"></a><span data-ttu-id="8694f-111">Пример кода: задать ключ карт Bing на уровне фермы или веб-узел</span><span class="sxs-lookup"><span data-stu-id="8694f-111">Code example: Set the Bing Maps key at the farm or web level</span></span>
<span data-ttu-id="8694f-112"><a name="SP15Setbing_farm"> </a></span><span class="sxs-lookup"><span data-stu-id="8694f-112"></span></span>

<span data-ttu-id="8694f-113">Можно задать ключ карт Bing на уровне фермы или веб.</span><span class="sxs-lookup"><span data-stu-id="8694f-113">The Bing Maps key can be set at the farm or web level.</span></span> <span data-ttu-id="8694f-114">Чтобы задать ключ карт Bing на уровне фермы, необходимы права администратора на сервере. Затем можно добавить ключ с помощью консоли управления SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8694f-114">To set the Bing Maps key at the farm level, you need administrator rights on the server; you can then add the key by using the SharePoint Management Shell.</span></span> <span data-ttu-id="8694f-115">Чтобы задать ключ карт Bing на уровне веб-, запишите консольного приложения, использующего клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8694f-115">To set the Bing Maps key at the web level, write a console application that uses the SharePoint client object model.</span></span>
  
    
    

> <span data-ttu-id="8694f-116">**Совет:** Установка на уровне веб-ключ Bing Maps имеет высокий приоритет, чем ключ карт Bing на уровне фермы.</span><span class="sxs-lookup"><span data-stu-id="8694f-116">**Tip:** The Bing Maps key set at web level has higher precedence order than the Bing Maps key set at farm level.</span></span> 
  
    
    


### <a name="to-set-the-bing-maps-key-at-the-farm-level-using-windows-powershell"></a><span data-ttu-id="8694f-117">Чтобы задать ключ карт Bing на уровне фермы, с помощью Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8694f-117">To set the Bing Maps key at the farm level using Windows PowerShell</span></span>


1. <span data-ttu-id="8694f-118">Выполните вход на сервер SharePoint с правами администратора и откройте командную консоль SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8694f-118">Log on to the SharePoint server as an administrator, and open the SharePoint Management Shell.</span></span>
    
  
2. <span data-ttu-id="8694f-119">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8694f-119">Execute the following command:</span></span> 
    
     `Set-SPBingMapsKey -BingKey "<Enter a valid Bing Maps key>"`
    
    <span data-ttu-id="8694f-120">Ключ Bing Maps теперь имеет значение на уровне фермы в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8694f-120">The Bing Maps key is now set at the farm level in SharePoint.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="8694f-p102">[!Примечание] При использовании Windows PowerShell ключ Bing Maps можно задать только на уровне фермы. Если вы хотите задать ключ карт Bing на уровне веб-, можно установить ключ программно, как показано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="8694f-p102">When you use Windows PowerShell, the Bing Maps key can be set only at the farm level. If you want to set the Bing Maps key at the web level, you can set the key programmatically, as shown in the following section.</span></span> 

### <a name="to-set-the-bing-maps-key-at-the-farm-or-web-level-using-the-client-object-model"></a><span data-ttu-id="8694f-123">Чтобы задать ключ карт Bing на уровне фермы или веб-клиента с помощью объектной модели</span><span class="sxs-lookup"><span data-stu-id="8694f-123">To set the Bing Maps key at the farm or web level using the client object model</span></span>


1. <span data-ttu-id="8694f-124">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8694f-124">Start Visual Studio.</span></span>
    
  
2. <span data-ttu-id="8694f-p103">В строке меню щелкните **файл**, **Создать проект**. Откроется диалоговое окно **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="8694f-p103">On the menu bar, choose **File**, **New Project**. The **New Project** dialog box opens.</span></span>
    
  
3. <span data-ttu-id="8694f-127">В диалоговом окне **Создать проект** выберите пункт **C#** в поле **Установленные шаблоны** и затем выберите шаблон **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="8694f-127">In the **New Project** dialog box, choose **C#** in the **Installed Templates** box, and then choose the **Console Application** template.</span></span>
    
  
4. <span data-ttu-id="8694f-128">Назовите проект и затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8694f-128">Give the project a name, and then choose the **OK** button.</span></span>
    
  
5. <span data-ttu-id="8694f-p104">Visual Studio создает проект. Добавление ссылки на следующие сборки и нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="8694f-p104">Visual Studio creates the project. Add a reference to the following assemblies, and choose **OK**.</span></span>
    
  - <span data-ttu-id="8694f-131">Microsoft.SharePoint.Client.dll</span><span class="sxs-lookup"><span data-stu-id="8694f-131">Microsoft.SharePoint.Client.dll</span></span>
    
  
  - <span data-ttu-id="8694f-132">Microsoft.SharePoint.Client.Runtime.dll</span><span class="sxs-lookup"><span data-stu-id="8694f-132">Microsoft.SharePoint.Client.Runtime.dll</span></span>
    
  
6. <span data-ttu-id="8694f-133">В файле .cs по умолчанию добавьте директиву **using** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8694f-133">In the default .cs file, add a **using** directive as follows.</span></span>
    
     `using Microsoft.SharePoint.Client;`
    
  
7. <span data-ttu-id="8694f-134">Добавьте следующий код в метод Main в CS-файл.</span><span class="sxs-lookup"><span data-stu-id="8694f-134">Add the following code to the Main method in the .cs file.</span></span>
    
```cs
  
class Program
    {
        static void Main(string[] args)
        {
            SetBingMapsKey();
            Console.WriteLine("Bing Maps set successfully");
        }
     static private void SetBingMapsKey()
        {

            ClientContext context = new ClientContext("<Site Url>");
            Web web = context.Web;
            web.AllProperties["BING_MAPS_KEY"] = "<Valid Bing Maps Key>"
            web.Update();
            context.ExecuteQuery();
        }    
    }

```

8. <span data-ttu-id="8694f-135">Замените <Site Url> и _<Valid Bing Maps Key>_ с допустимыми значениями.</span><span class="sxs-lookup"><span data-stu-id="8694f-135">Replace the <Site Url> and  _<Valid Bing Maps Key>_ with valid values.</span></span>
    
  
9. <span data-ttu-id="8694f-136">Требуемая версия .NET framework, заданные в свойствах проекта как .NET Framework 4.0 и запустите пример.</span><span class="sxs-lookup"><span data-stu-id="8694f-136">Set the target framework in Project Properties as .NET Framework 4.0, and run the example.</span></span>
    
  
10. <span data-ttu-id="8694f-137">Ключ необходимо задать теперь на уровне веб.</span><span class="sxs-lookup"><span data-stu-id="8694f-137">The key should now be set at the web level.</span></span> 
    
  

## <a name="next-steps"></a><span data-ttu-id="8694f-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8694f-138">Next steps</span></span>
<span data-ttu-id="8694f-139"><a name="SP15Bing_nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="8694f-139"></span></span>

<span data-ttu-id="8694f-140">Для получения дополнительных сведений о работе с расположение и карты функциональные возможности в SharePoint, см.:</span><span class="sxs-lookup"><span data-stu-id="8694f-140">To learn more about working with location and map functionality in SharePoint, see the following:</span></span>
  
    
    

-  [<span data-ttu-id="8694f-141">Как программно добавить столбец "Географическое расположение" в список SharePoint</span><span class="sxs-lookup"><span data-stu-id="8694f-141">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8694f-142">Как: расширение типа поля географического расположения, с использованием обработки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="8694f-142">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  

