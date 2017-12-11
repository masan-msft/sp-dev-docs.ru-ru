---
title: "Использование обновления компонентов для применения новых эталонных страниц SharePoint при обновлении SharePoint 2010"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: de3169f1-715e-4f80-bfbf-caea744e2a0b
ms.openlocfilehash: 3f370357d065ae858d0f21d8c4d59d927d55805f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-feature-upgrade-to-apply-new-sharepoint-master-pages-when-upgrading-from-sharepoint-2010"></a>Использование обновления компонентов для применения новых эталонных страниц SharePoint при обновлении SharePoint 2010
Узнайте, как очистить настраиваемой главной страницы во время `FeatureUpgrading` событий при обновлении сайта SharePoint 2010 в режиме совместимости 2013.
При обновлении настройки SharePoint 2010 до SharePoint ссылки на настраиваемых главных страниц, созданному вами переключитесь обратно на странице default.master. Если развернута функциональная возможность, которая содержит одно или несколько настраиваемых главных страниц для обновленных семейства сайтов SharePoint, на котором работает в режиме совместимости SharePoint 2010 необходимо сбросить главных страниц SharePoint при обновлении до совместимость 2013 режим. В этом разделе описывается использование приемника компонента, чтобы убедиться в том, что перезапуска настраиваемой главной страницы SharePoint при обновлении с SharePoint 2010. 
  
    
    


## <a name="use-custom-upgrade-code-to-reset-a-master-page"></a>Use custom upgrade code to reset a master page

Как описывается в статье [Развертывание пользовательских функций для обновления семейств веб-сайтов в SharePoint](http://technet.microsoft.com/en-us/library/dn673579%28v=office.15%29.aspx) , при обновлении с SharePoint 2010 в SharePoint, семейства веб-сайтов в ферме серверов будут запускаться в режиме совместимости SharePoint 2010 по умолчанию. В зависимости от выбранного варианта обновления настраиваемых компонентов, которые вы извлекли будет развернута любого заданного компонента при помощи пакетов решений один или два:
  
    
    

- A single solution package that can be deployed to both the "14" and the "15" compatibility levels, either because of custom logic for the "15" compatibility level, or because the feature works without any problems in both the "14" and the "15" compatibility levels.
    
  
- Two solution packages that contain different versions of the same feature. This approach is called "feature masking."
    
  
In either case, during upgrade any custom master pages you've created will revert to the default.master page. If you don't reset these pages with logic inside your feature, you'll need to reactivate the feature (or the "15" version of the feature) to reset the master pages to your custom versions. You can reset your 2013 custom master pages by using a feature receiver that is tied to the  `FeatureUpgrading` event.
  
    
    

### <a name="to-reset-a-2013-custom-master-page-with-a-feature-receiver"></a>To reset a 2013 custom master page with a feature receiver


1. Open your solution in Visual Studio. Find your feature under the **Features** node in Solution Explorer, and open the feature.xml file for your feature.
    
  
2. Add an  `<UpgradeActions>` section to the feature.xml file and make sure that the action applies only to the version of the feature that is currently in use for the "14" compatibility level. This section specifies the name of an action to perform when the feature is upgraded. The following example specifies an upgrade when version 1.0.0.0 of the feature is in use. In the example, the action `UpgradeFeature` is passed to the implementation of the **FeatureUpgrading(SPFeatureReceiverProperties, String, IDictionary<String, String>)** method that you'll define later after you've added a feature receiver.
    
```XML
  
<UpgradeActions
    ReceiverAssembly="MyFeatureReceiver, Version=2.0.0.0, Culture=neutral, PublicKeyToken=<token>"
    ReceiverClass="MyFeature.MyFeatureEventReceiver">
  <VersionRange BeginVersion="1.0.0.0" EndVersion="1.0.0.0">
   <CustomUpgradeAction Name="UpgradeFeature"/>
<ApplyElementManifests>
<ElementManifest Location="MasterPages\\UpgradeElements.xml" />
</ApplyElementManifests>
  </VersionRange>
</UpgradeActions>

```


    You place the master page or pages in the **MasterPages** folder of the project, and any metadata related to the master page(s) in the **UpgradeElements.xml** file.
    
  
3. Add a  `<Properties>` section to the feature.xml file. This section contains key-value pairs that specify the 2013 custom master page or pages that you want to set when the site is upgraded. The following example specifies the value of the `My15MasterPage` key that you'll use in the feature receiver.
    
```
  
<Properties>
  <Property Key="My15MasterPage" Value="_catalogs/masterpage/My15MasterPage.master" />
</Properties>

```

4. In Solution Explorer, under the **Features** node, right click the name of your feature, and then choose **Add Event Receiver** to add an event receiver to the feature.
    
    This adds a code file under your feature in Solution Explorer. Figure 1 shows where a sample Feature1.EventReceiver.cs file appears under the feature in the **Features** folder.
    

   **Figure 1. The code file for an event receiver in a feature**

  

  ![После создания приемника событий для компонента под ним появляется файл кода.](../images/SP15_FeatureReceiverVS.png)
  

    This file contains a commented and empty  `FeatureUpgrading` method. You'll use this method in the following step.
    
  
5. Open the code file and uncomment the FeatureUpgrading method, which overrides the **FeatureUpgrading(SPFeatureReceiverProperties, String, IDictionary<String, String>)** method. The following example applies the `My15MasterPage` file that was specified earlier in the feature.xml file.
    
```cs
  
public override void FeatureUpgrading(SPFeatureReceiverProperties properties, string upgradeActionName, System.Collections.Generic.IDictionary<string, string> parameters)
        {
 
            try
            {
            if (upgradeActionName != "UpgradeFeature")
                return;
                //Set the master page to a value stored as a property in the feature.xml file
                string masterPage = properties.Definition.Properties[My15MasterPage].Value;
                string baseURL;
                var currentWeb = properties.Feature.Parent as SPWeb;
 
                //Checks to see that the API returns a string that ends in a "/" and if not adds it.
                if (currentWeb.ServerRelativeUrl.Substring(currentWeb.ServerRelativeUrl.Length - 1) == "/")
                {
                    baseURL = currentWeb.ServerRelativeUrl;
                }
                else
                {
                    baseURL = currentWeb.ServerRelativeUrl + "/";
                }
 
                masterPage = baseURL + masterPage;
                currentWeb.CustomMasterUrl = masterPage;
 
                currentWeb.Properties.Update();
                currentWeb.Update();
            }
            }
 
            catch (Exception ex)
            {
             //Handle exception
            }
        }

```

После завершения обновления может потребоваться будущих и долгосрочного обслуживания для функции, учитывайте следующее. Руководство по обслуживанию код с полным доверием, обратитесь к [Управление жизненным циклом приложений в SharePoint 2010](http://msdn.microsoft.com/en-us/library/office/gg604045%28v=office.14%29.aspx) . Хотя данная статья относится к SharePoint 2010 в частности, применяется одинаково для кода с полным доверием в SharePoint. Если вы не знакомы с действиями управление версиями и обновление компонента, обратитесь к разделу [модели управления жизненным циклом решений](http://msdn.microsoft.com/en-us/library/office/gg604045%28v=office.14%29.aspx#sectionSection7) этой статьи. Следует также рассмотрим [Советы и рекомендации для версий с помощью компонента](http://msdn.microsoft.com/en-us/library/office/ee535064%28v=office.14%29.aspx).
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Развертывание настраиваемых компонентов в обновленных семействах сайтов в SharePoint](http://technet.microsoft.com/en-us/library/dn673579%28v=office.15%29.aspx)
    
  
-  [Обновление настроек сайта для SharePoint](upgrade-site-customizations-for-sharepoint.md)
    
  
-  [Обновления для SharePoint](http://technet.microsoft.com/en-us/library/cc303420%28v=office.15%29.aspx)
    
  
-  [Пакет решения SharePoint и SharePoint Online для фирменной настройки и подготовки сайта](http://www.microsoft.com/en-us/download/details.aspx?id=42030)
    
  
-  [Установка и управление решениями для SharePoint](http://technet.microsoft.com/en-us/library/cc263205%28v=office.15%29.aspx)
    
  

