---
title: "Определение установленных SKU SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d5d84d6f-6a8e-4ead-9296-7025baf1e154
ms.openlocfilehash: 4e7d8343d3151ac3fc0c4514e7bddfbf0f0ddd65
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="detect-the-installed-sku-of-sharepoint"></a>Определение установленных SKU SharePoint

Если поведение решений зависит от установленных локально SKU SharePoint или Project Server 2013, используйте в примере кода в этой статье для поиска нужной информации SKU.

## <a name="detect-the-installed-sku-of-sharepoint-or-project-server-2013-by-using-code"></a>Определение установленных SKU SharePoint или Project Server 2013 с помощью кода
<a name="SP15DetectSKU_detect"> </a>

В следующем примере кода показано, как получить раздел реестра установленного SKU SharePoint, Microsoft Project Server 2013 и другие серверные продукты Office, а также в соответствии с SKU с хэш-таблицы, который хранит имена и ключи для все известные Номера SKU этих продуктов. Вывод консоли отображается имя установленного SKU.
  
    
    

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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_SP15DetectSKUaddresources"> </a>


-  [Обзор разработки решений с помощью SharePoint](sharepoint-development-overview.md)
    
  
-  [Новые возможности для разработчиков в SharePoint](what-s-new-for-developers-in-sharepoint.md)
    
  
-  [Блог разработчиков SharePoint](http://blogs.msdn.com/b/sharepointdev/)
    
  
-  [Обмен стека для SharePoint](http://sharepoint.stackexchange.com/)
    
  

