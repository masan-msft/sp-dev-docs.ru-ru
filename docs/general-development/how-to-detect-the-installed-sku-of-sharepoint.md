---
title: "Определение установленных SKU SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d5d84d6f-6a8e-4ead-9296-7025baf1e154
ms.openlocfilehash: 94036f746306de05ef6be5abc17a5d1898824ac7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="detect-the-installed-sku-of-sharepoint"></a><span data-ttu-id="76956-102">Определение установленных SKU SharePoint</span><span class="sxs-lookup"><span data-stu-id="76956-102">Detect the installed SKU of SharePoint</span></span>

<span data-ttu-id="76956-103">Если поведение решений зависит от установленных локально SKU SharePoint или Project Server 2013, используйте в примере кода в этой статье для поиска нужной информации SKU.</span><span class="sxs-lookup"><span data-stu-id="76956-103">If the behavior of your solutions depends on the locally installed SKU of SharePoint or Project Server 2013, use the code example in this article to find the SKU information you need.</span></span>

## <a name="detect-the-installed-sku-of-sharepoint-or-project-server-2013-by-using-code"></a><span data-ttu-id="76956-104">Определение установленных SKU SharePoint или Project Server 2013 с помощью кода</span><span class="sxs-lookup"><span data-stu-id="76956-104">Detect the installed SKU of SharePoint or Project Server 2013 by using code</span></span>
<span data-ttu-id="76956-105"><a name="SP15DetectSKU_detect"> </a></span><span class="sxs-lookup"><span data-stu-id="76956-105"></span></span>

<span data-ttu-id="76956-106">В следующем примере кода показано, как получить раздел реестра установленного SKU SharePoint, Microsoft Project Server 2013 и другие серверные продукты Office, а также в соответствии с SKU с хэш-таблицы, который хранит имена и ключи для все известные Номера SKU этих продуктов.</span><span class="sxs-lookup"><span data-stu-id="76956-106">The following code example demonstrates how to retrieve the registry key of the installed SKU of SharePoint, Microsoft Project Server 2013, and other Office server products, and how to match the SKU with a hash table that stores the names and keys for all of the known SKUs of these products.</span></span> <span data-ttu-id="76956-107">Вывод консоли отображается имя установленного SKU.</span><span class="sxs-lookup"><span data-stu-id="76956-107">The console output displays the name of the installed SKU.</span></span>
  
    
    

```cs

using System;
using System.Collections;
using Microsoft.Win32;


namespace GetInstalledSharePointSku
{
    class Program
    {
        internal static Hashtable _products;

        public static Hashtable SharePointProducts
        {
            get 
            {
                if (_products == null)
                {
                    _products = new Hashtable();

                    _products.Add("35466B1A-B17B-4DFB-A703-F74E2A1F5F5E", "Project Server 2013");
                    _products.Add("BC7BAF08-4D97-462C-8411-341052402E71", " Project Server 2013 Preview");

                    _products.Add("C5D855EE-F32B-4A1C-97A8-F0A28CE02F9C", "SharePoint");
                    _products.Add("CBF97833-C73A-4BAF-9ED3-D47B3CFF51BE", "SharePoint Preview");
                    _products.Add("B7D84C2B-0754-49E4-B7BE-7EE321DCE0A9", "SharePoint Enterprise");
                    _products.Add("298A586A-E3C1-42F0-AFE0-4BCFDC2E7CD0", "SharePoint Enterprise Preview");

                    _products.Add("D6B57A0D-AE69-4A3E-B031-1F993EE52EDC ", "Microsoft Office Online");
                    _products.Add("9FF54EBC-8C12-47D7-854F-3865D4BE8118", "SharePoint Foundation 2013");
                }
                
                return _products;
            }
        }

        private const String SharePointProductsRegistryPath = @"SOFTWARE\\Microsoft\\Shared Tools\\Web Server Extensions\\15.0\\WSS\\InstalledProducts\\";

        static void Main(string[] args)
        {
            try
            {
                //Open the registry key in read-only mode.
                using (RegistryKey key = Registry.LocalMachine.OpenSubKey(SharePointProductsRegistryPath, false))
                {
                    //Get all of the installed product code/SKUId pairs.
                    foreach (String value in key.GetValueNames())
                    {
                        try
                        {
                            //Get the SKUId and see whether it is a known product.
                            String SKUId = key.GetValue(value) as String;

                            if (SharePointProducts[SKUId] != null)
                            {
                                Console.WriteLine("Product Installed: {0}", SharePointProducts[SKUId]);
                            }
                            else
                            {
                                Console.WriteLine("Unknown Product: {0}", SKUId);
                            }
                        }
                        catch (Exception e)
                        {
                            Console.WriteLine("Could not read key exception was {0}", e.Message);
                        }
                    }
                }
            }
            catch (Exception e)
            {
                Console.WriteLine("Could not open key exception was {0}", e.Message);
            }
            Console.Read();
        }
    }
}
```


## <a name="see-also"></a><span data-ttu-id="76956-108">См. также</span><span class="sxs-lookup"><span data-stu-id="76956-108">See also</span></span>
<span data-ttu-id="76956-109"><a name="bk_SP15DetectSKUaddresources"> </a></span><span class="sxs-lookup"><span data-stu-id="76956-109"></span></span>


-  [<span data-ttu-id="76956-110">Обзор разработки решений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="76956-110">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  
-  [<span data-ttu-id="76956-111">Новые возможности для разработчиков в SharePoint</span><span class="sxs-lookup"><span data-stu-id="76956-111">What's new for developers in SharePoint</span></span>](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [<span data-ttu-id="76956-112">Блог разработчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="76956-112">SharePoint Developer Blog</span></span>](http://blogs.msdn.com/b/sharepointdev/)
    
  
-  [<span data-ttu-id="76956-113">Обмен стека для SharePoint</span><span class="sxs-lookup"><span data-stu-id="76956-113">SharePoint Stack Exchange</span></span>](http://sharepoint.stackexchange.com/)
    
  

