---
title: "Как задать ключ карт Bing на уровне веб-серверы и фермы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 507ed9de-c349-44b5-b182-e838795dd862
ms.openlocfilehash: f433e66bf82336b2450382bef1a3e34df5feeb62
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint"></a>Как: задать ключ карт Bing на уровне веб-серверы и фермы в SharePoint

  
    
    
![Раздел "Инструкции"](../images/mod_icon_howto.png)
  
    
    

  
    
    

  
    
    
Узнайте, как программно задать ключ Карт Bing на веб-уровне и уровне фермы с помощью клиентской объектной модели SharePoint и Windows PowerShell, чтобы включить функционал Карт Bing в списке SharePoint, а также в веб-приложениях и мобильных приложениях на основе местоположения.

  
    
    


## <a name="prerequisites-for-setting-the-bing-maps-key"></a>Необходимые условия для установки ключ Bing Maps
<a name="SP15Bing_prereq"> </a>

Для выполнения действия, описанные в этом примере, необходимо иметь следующее:
  
    
    

- SharePoint с правами администратора.
    
  
- Действительный ключ Bing Maps, который можно получить из  [Центр учетных записей карт Bing](https://www.bingmapsportal.com/).
    
    > **Важные:** Обратите внимание, что вы несете ответственность за соблюдение сроками и условиями, которые применяются к использованию ключ Bing Maps и все необходимые условия для пользователей приложения о данных, передаваемых службы Bing Maps. 

## <a name="code-example-set-the-bing-maps-key-at-the-farm-or-web-level"></a>Пример кода: задать ключ карт Bing на уровне фермы или веб-узел
<a name="SP15Setbing_farm"> </a>

Можно задать ключ карт Bing на уровне фермы или веб. Чтобы задать ключ карт Bing на уровне фермы, необходимы права администратора на сервере. Затем можно добавить ключ с помощью консоли управления SharePoint. Чтобы задать ключ карт Bing на уровне веб-, запишите консольного приложения, использующего клиентской объектной модели SharePoint.
  
    
    

> **Совет:** Установка на уровне веб-ключ Bing Maps имеет высокий приоритет, чем ключ карт Bing на уровне фермы. 
  
    
    


### <a name="to-set-the-bing-maps-key-at-the-farm-level-using-windows-powershell"></a>Чтобы задать ключ карт Bing на уровне фермы, с помощью Windows PowerShell


1. Выполните вход на сервер SharePoint с правами администратора и откройте командную консоль SharePoint.
    
  
2. Выполните следующую команду: 
    
     `Set-SPBingMapsKey -BingKey "<Enter a valid Bing Maps key>"`
    
    Ключ Bing Maps теперь имеет значение на уровне фермы в SharePoint. 
    
    > **Примечание:** При использовании Windows PowerShell, ключ Bing Maps можно задать только на уровне фермы. Если вы хотите задать ключ карт Bing на уровне веб-, можно установить ключ программно, как показано в следующем разделе. 

### <a name="to-set-the-bing-maps-key-at-the-farm-or-web-level-using-the-client-object-model"></a>Чтобы задать ключ карт Bing на уровне фермы или веб-клиента с помощью объектной модели


1. Запустите Visual Studio.
    
  
2. В строке меню щелкните **файл**, **Создать проект**. Откроется диалоговое окно **Новый проект**.
    
  
3. В диалоговом окне **Создать проект** выберите пункт **C#** в поле **Установленные шаблоны** и затем выберите шаблон **Консольное приложение**.
    
  
4. Назовите проект и затем нажмите кнопку **ОК**.
    
  
5. Visual Studio создает проект. Добавление ссылки на следующие сборки и нажмите **кнопку ОК**.
    
  - Microsoft.SharePoint.Client.dll
    
  
  - Microsoft.SharePoint.Client.Runtime.dll
    
  
6. В файле .cs по умолчанию добавьте директиву **using** следующим образом.
    
     `using Microsoft.SharePoint.Client;`
    
  
7. Добавьте следующий код в метод Main в CS-файл.
    
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

8. Замените <Site Url> и _<Valid Bing Maps Key>_ с допустимыми значениями.
    
  
9. Требуемая версия .NET framework, заданные в свойствах проекта как .NET Framework 4.0 и запустите пример.
    
  
10. Ключ необходимо задать теперь на уровне веб. 
    
  

## <a name="next-steps"></a>Дальнейшие действия
<a name="SP15Bing_nextsteps"> </a>

Для получения дополнительных сведений о работе с расположение и карты функциональные возможности в SharePoint, см.:
  
    
    

-  [Как: Добавление столбца географического расположения списка программными средствами в SharePoint](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md)
    
  
-  [Как: расширение типа поля географического расположения, с использованием обработки на стороне клиента](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  

