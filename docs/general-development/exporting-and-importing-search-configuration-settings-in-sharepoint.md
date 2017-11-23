---
title: "Экспорт и импорт параметров конфигурации поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d00679a3-ffa2-4281-ad8b-70fc2c4a14e2
ms.openlocfilehash: 2b742f7676a7252a45609d92da05dd670f34b5d4
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="exporting-and-importing-search-configuration-settings-in-sharepoint"></a><span data-ttu-id="c4c0f-102">Экспорт и импорт параметров конфигурации поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4c0f-102">Exporting and importing search configuration settings in SharePoint</span></span>
<span data-ttu-id="c4c0f-p101">Получение примеров кода, которые показывают, как для экспорта и импорта параметров конфигурации настраиваемого поиска. Эти параметры включают все правила настраиваемых запросов, источники результатов, типы результатов, моделей ранжирования и параметры поиска для сайтов. SharePoint предоставляет эту функцию через пространство имен  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) .Можно также экспорт параметров конфигурации настраиваемого поиска из приложения-службы поиска (SSA) и импорта параметров для сайтов и семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-p101">Get code examples that show you how to export and import customized search configuration settings. These settings include all customized query rules, result sources, result types, ranking models, and site search settings. SharePoint exposes this functionality through the  [Microsoft.Office.Server.Search.Portability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.aspx) namespace.You can also export customized search configuration settings from a Search service application (SSA) and import the settings to site collections and sites.</span></span> 
> <span data-ttu-id="c4c0f-106">**Примечание:** Не удается Импорт параметров конфигурации настраиваемого поиска SSA или экспорт параметров конфигурации поиска по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-106">**Note:** You can't import customized search configuration settings to an SSA, or export the default search configuration settings.</span></span> 
  
    
    


## <a name="export-search-configuration-settings"></a><span data-ttu-id="c4c0f-107">Экспорт параметров конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="c4c0f-107">Export search configuration settings</span></span>
<span data-ttu-id="c4c0f-108"><a name="SP15_exporting_search_configuration"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0f-108"></span></span>

<span data-ttu-id="c4c0f-109">Приведенный ниже код показано, как использовать [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) для экспорта параметров конфигурации поиска веб-узла.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-109">The following code shows how to use  [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) to export your site's search configuration settings.</span></span> <span data-ttu-id="c4c0f-110">Код использует на сайте пример `http://yoursite/sites/publishing1`, которого вы замените собственного узла.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-110">The code uses an example site `http://yoursite/sites/publishing1`, which you'd replace with your own site.</span></span>  <span data-ttu-id="c4c0f-111">_имя файла_ содержит ссылку на файл, где хранятся параметры конфигурации поиска; _владелец_ указывает уровень [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) , по которому можно получить параметры конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-111">_fileName_ refers to the file where the search configuration settings are stored; _owner_ specifies the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) level at which the search configuration settings are obtained.</span></span>
  
    
    

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


## <a name="import-search-configuration-settings"></a><span data-ttu-id="c4c0f-112">Импорт параметров конфигурации поиска</span><span class="sxs-lookup"><span data-stu-id="c4c0f-112">Import search configuration settings</span></span>
<span data-ttu-id="c4c0f-113"><a name="SP15_importing_search_configuration"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0f-113"></span></span>

<span data-ttu-id="c4c0f-114">Приведенный ниже код показывает, как для импорта параметров конфигурации поиска из файла с помощью [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) и замены существующих параметров поиска на указанном узле `http://yoursite/sites/publishing1`.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-114">The following code shows how to import search configuration settings from a file by using  [SearchConfigurationPortability](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Portability.SearchConfigurationPortability.aspx) and replace the existing search settings on a specified site, `http://yoursite/sites/publishing1`.</span></span>  <span data-ttu-id="c4c0f-115">_имя файла_ содержит ссылку на файл, где хранятся параметры конфигурации поиска; _владелец_ указывает уровень [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) , по которому можно получить параметры конфигурации поиска.</span><span class="sxs-lookup"><span data-stu-id="c4c0f-115">_fileName_ refers to the file where the search configuration settings are stored; _owner_ specifies the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) level at which the search configuration settings are obtained.</span></span>
  
    
    

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


## <a name="additional-resources"></a><span data-ttu-id="c4c0f-116">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c4c0f-116">Additional resources</span></span>
<span data-ttu-id="c4c0f-117"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c4c0f-117"></span></span>


-  [<span data-ttu-id="c4c0f-118">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4c0f-118">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c4c0f-119">Импорт и экспорт параметров конфигурации настраиваемого поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4c0f-119">Export and import customized search configuration settings in SharePoint</span></span>](http://technet.microsoft.com/ru-ru/library/jj871675.aspx)
    
  

  
    
    

