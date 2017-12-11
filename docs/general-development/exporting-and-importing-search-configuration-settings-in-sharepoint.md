---
title: "Экспорт и импорт параметров конфигурации поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d00679a3-ffa2-4281-ad8b-70fc2c4a14e2
ms.openlocfilehash: 517e7e941ef0f4b45d77c77581ddf50a8b38311f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="exporting-and-importing-search-configuration-settings-in-sharepoint"></a>Экспорт и импорт параметров конфигурации поиска в SharePoint
Получение примеров кода, которые показывают, как для экспорта и импорта параметров конфигурации настраиваемого поиска. Эти параметры включают все правила настраиваемых запросов, источники результатов, типы результатов, моделей ранжирования и параметры поиска для сайтов. SharePoint предоставляет эту функцию через пространство имен  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) .Можно также экспорт параметров конфигурации настраиваемого поиска из приложения-службы поиска (SSA) и импорта параметров для сайтов и семейств веб-сайтов. 

> [!NOTE]
> [!Примечание] Не удается Импорт параметров конфигурации настраиваемого поиска SSA или экспорт параметров конфигурации поиска по умолчанию. 
  
    
    


## <a name="export-search-configuration-settings"></a>Экспорт параметров конфигурации поиска
<a name="SP15_exporting_search_configuration"> </a>

Приведенный ниже код показано, как использовать [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) для экспорта параметров конфигурации поиска веб-узла. Код использует на сайте пример `http://yoursite/sites/publishing1`, которого вы замените собственного узла.  _имя файла_ содержит ссылку на файл, где хранятся параметры конфигурации поиска; _владелец_ указывает уровень [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) , по которому можно получить параметры конфигурации поиска.
  
    
    

```

private static void Export(string fileName)
{
    SPSite site = new SPSite("http://yoursite/sites/publishing1");
    SearchConfigurationPortability conf = new SearchConfigurationPortability(site);
    SearchObjectOwner owner = new SearchObjectOwner(SearchObjectLevel.SPWeb, site.OpenWeb());
    var buff = conf.ExportSearchConfiguration(owner);
    File.WriteAllText(fileName, buff);
    site.Close();
}
```


## <a name="import-search-configuration-settings"></a>Импорт параметров конфигурации поиска
<a name="SP15_importing_search_configuration"> </a>

Приведенный ниже код показывает, как для импорта параметров конфигурации поиска из файла с помощью [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) и замены существующих параметров поиска на указанном узле `http://yoursite/sites/publishing1`.  _имя файла_ содержит ссылку на файл, где хранятся параметры конфигурации поиска; _владелец_ указывает уровень [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) , по которому можно получить параметры конфигурации поиска.
  
    
    

```cs

private static void Import(string fileName)
{
    SPSite site = new SPSite("http://yoursite/sites/publishing1");
    SearchConfigurationPortability conf = new SearchConfigurationPortability(site);
    SearchObjectOwner owner = new SearchObjectOwner(SearchObjectLevel.SPWeb, site.OpenWeb());
    conf.ImportSearchConfiguration(owner, File.ReadAllText(fileName));
    site.Close();
}

```


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Поиск в SharePoint](search-in-sharepoint.md)
    
  
-  [Импорт и экспорт параметров конфигурации настраиваемого поиска в SharePoint](http://technet.microsoft.com/en-us/library/jj871675.aspx)
    
  

  
    
    

