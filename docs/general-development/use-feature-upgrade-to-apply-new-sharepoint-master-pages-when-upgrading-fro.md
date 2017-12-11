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
# <a name="use-feature-upgrade-to-apply-new-sharepoint-master-pages-when-upgrading-from-sharepoint-2010"></a><span data-ttu-id="a27e6-102">Использование обновления компонентов для применения новых эталонных страниц SharePoint при обновлении SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="a27e6-102">Use Feature upgrade to apply new SharePoint master pages when upgrading from SharePoint 2010</span></span>
<span data-ttu-id="a27e6-103">Узнайте, как очистить настраиваемой главной страницы во время `FeatureUpgrading` событий при обновлении сайта SharePoint 2010 в режиме совместимости 2013.</span><span class="sxs-lookup"><span data-stu-id="a27e6-103">Learn how to reset a custom master page during the  `FeatureUpgrading` event when you're upgrading a SharePoint site from the 2010 to the 2013 compatibility mode.</span></span>
<span data-ttu-id="a27e6-104">При обновлении настройки SharePoint 2010 до SharePoint ссылки на настраиваемых главных страниц, созданному вами переключитесь обратно на странице default.master.</span><span class="sxs-lookup"><span data-stu-id="a27e6-104">When you upgrade your SharePoint 2010 customizations to SharePoint, any references to custom master pages you've created switch back to the default.master page.</span></span> <span data-ttu-id="a27e6-105">Если развернута функциональная возможность, которая содержит одно или несколько настраиваемых главных страниц для обновленных семейства сайтов SharePoint, на котором работает в режиме совместимости SharePoint 2010 необходимо сбросить главных страниц SharePoint при обновлении до совместимость 2013 режим.</span><span class="sxs-lookup"><span data-stu-id="a27e6-105">If you've deployed a feature that contains one or more custom master pages to an upgraded SharePoint site collection that is running in SharePoint 2010 compatibility mode you'll need to reset your SharePoint master pages when you upgrade to the 2013 compatibility mode.</span></span> <span data-ttu-id="a27e6-106">В этом разделе описывается использование приемника компонента, чтобы убедиться в том, что перезапуска настраиваемой главной страницы SharePoint при обновлении с SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="a27e6-106">This topic explains how to use a feature receiver to make sure that your SharePoint custom master pages get reset when you upgrade from SharePoint 2010.</span></span> 
  
    
    


## <a name="use-custom-upgrade-code-to-reset-a-master-page"></a><span data-ttu-id="a27e6-107">Use custom upgrade code to reset a master page</span><span class="sxs-lookup"><span data-stu-id="a27e6-107">Use custom upgrade code to reset a master page</span></span>

<span data-ttu-id="a27e6-108">Как описывается в статье [Развертывание пользовательских функций для обновления семейств веб-сайтов в SharePoint](http://technet.microsoft.com/en-us/library/dn673579%28v=office.15%29.aspx) , при обновлении с SharePoint 2010 в SharePoint, семейства веб-сайтов в ферме серверов будут запускаться в режиме совместимости SharePoint 2010 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a27e6-108">As the guidance in  [Deploy custom features to upgraded site collections in SharePoint](http://technet.microsoft.com/en-us/library/dn673579%28v=office.15%29.aspx) explains, when you upgrade from SharePoint 2010 to SharePoint, the site collections in your farm will run in SharePoint 2010 compatibility mode by default.</span></span> <span data-ttu-id="a27e6-109">В зависимости от выбранного варианта обновления настраиваемых компонентов, которые вы извлекли будет развернута любого заданного компонента при помощи пакетов решений один или два:</span><span class="sxs-lookup"><span data-stu-id="a27e6-109">Depending on the approach to upgrading your custom features that you've taken, you'll have deployed any given feature by using either one or two solution packages:</span></span>
  
    
    

- <span data-ttu-id="a27e6-110">A single solution package that can be deployed to both the "14" and the "15" compatibility levels, either because of custom logic for the "15" compatibility level, or because the feature works without any problems in both the "14" and the "15" compatibility levels.</span><span class="sxs-lookup"><span data-stu-id="a27e6-110">A single solution package that can be deployed to both the "14" and the "15" compatibility levels, either because of custom logic for the "15" compatibility level, or because the feature works without any problems in both the "14" and the "15" compatibility levels.</span></span>
    
  
- <span data-ttu-id="a27e6-p103">Two solution packages that contain different versions of the same feature. This approach is called "feature masking."</span><span class="sxs-lookup"><span data-stu-id="a27e6-p103">Two solution packages that contain different versions of the same feature. This approach is called "feature masking."</span></span>
    
  
<span data-ttu-id="a27e6-p104">In either case, during upgrade any custom master pages you've created will revert to the default.master page. If you don't reset these pages with logic inside your feature, you'll need to reactivate the feature (or the "15" version of the feature) to reset the master pages to your custom versions. You can reset your 2013 custom master pages by using a feature receiver that is tied to the  `FeatureUpgrading` event.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p104">In either case, during upgrade any custom master pages you've created will revert to the default.master page. If you don't reset these pages with logic inside your feature, you'll need to reactivate the feature (or the "15" version of the feature) to reset the master pages to your custom versions. You can reset your 2013 custom master pages by using a feature receiver that is tied to the  `FeatureUpgrading` event.</span></span>
  
    
    

### <a name="to-reset-a-2013-custom-master-page-with-a-feature-receiver"></a><span data-ttu-id="a27e6-116">To reset a 2013 custom master page with a feature receiver</span><span class="sxs-lookup"><span data-stu-id="a27e6-116">To reset a 2013 custom master page with a feature receiver</span></span>


1. <span data-ttu-id="a27e6-p105">Open your solution in Visual Studio. Find your feature under the **Features** node in Solution Explorer, and open the feature.xml file for your feature.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p105">Open your solution in Visual Studio. Find your feature under the **Features** node in Solution Explorer, and open the feature.xml file for your feature.</span></span>
    
  
2. <span data-ttu-id="a27e6-p106">Add an  `<UpgradeActions>` section to the feature.xml file and make sure that the action applies only to the version of the feature that is currently in use for the "14" compatibility level. This section specifies the name of an action to perform when the feature is upgraded. The following example specifies an upgrade when version 1.0.0.0 of the feature is in use. In the example, the action `UpgradeFeature` is passed to the implementation of the **FeatureUpgrading(SPFeatureReceiverProperties, String, IDictionary<String, String>)** method that you'll define later after you've added a feature receiver.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p106">Add an  `<UpgradeActions>` section to the feature.xml file and make sure that the action applies only to the version of the feature that is currently in use for the "14" compatibility level. This section specifies the name of an action to perform when the feature is upgraded. The following example specifies an upgrade when version 1.0.0.0 of the feature is in use. In the example, the action `UpgradeFeature` is passed to the implementation of the **FeatureUpgrading(SPFeatureReceiverProperties, String, IDictionary<String, String>)** method that you'll define later after you've added a feature receiver.</span></span>
    
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
    
  
3. <span data-ttu-id="a27e6-p107">Add a  `<Properties>` section to the feature.xml file. This section contains key-value pairs that specify the 2013 custom master page or pages that you want to set when the site is upgraded. The following example specifies the value of the `My15MasterPage` key that you'll use in the feature receiver.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p107">Add a  `<Properties>` section to the feature.xml file. This section contains key-value pairs that specify the 2013 custom master page or pages that you want to set when the site is upgraded. The following example specifies the value of the `My15MasterPage` key that you'll use in the feature receiver.</span></span>
    
```
  
<Properties>
  <Property Key="My15MasterPage" Value="_catalogs/masterpage/My15MasterPage.master" />
</Properties>

```

4. <span data-ttu-id="a27e6-126">In Solution Explorer, under the **Features** node, right click the name of your feature, and then choose **Add Event Receiver** to add an event receiver to the feature.</span><span class="sxs-lookup"><span data-stu-id="a27e6-126">In Solution Explorer, under the **Features** node, right click the name of your feature, and then choose **Add Event Receiver** to add an event receiver to the feature.</span></span>
    
    <span data-ttu-id="a27e6-p108">This adds a code file under your feature in Solution Explorer. Figure 1 shows where a sample Feature1.EventReceiver.cs file appears under the feature in the **Features** folder.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p108">This adds a code file under your feature in Solution Explorer. Figure 1 shows where a sample Feature1.EventReceiver.cs file appears under the feature in the **Features** folder.</span></span>
    

   <span data-ttu-id="a27e6-129">**Figure 1. The code file for an event receiver in a feature**</span><span class="sxs-lookup"><span data-stu-id="a27e6-129">**Figure 1. The code file for an event receiver in a feature**</span></span>

  

  ![После создания приемника событий для компонента под ним появляется файл кода.](../images/SP15_FeatureReceiverVS.png)
  

    <span data-ttu-id="a27e6-p109">This file contains a commented and empty  `FeatureUpgrading` method. You'll use this method in the following step.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p109">This file contains a commented and empty  `FeatureUpgrading` method. You'll use this method in the following step.</span></span>
    
  
5. <span data-ttu-id="a27e6-p110">Open the code file and uncomment the FeatureUpgrading method, which overrides the **FeatureUpgrading(SPFeatureReceiverProperties, String, IDictionary<String, String>)** method. The following example applies the `My15MasterPage` file that was specified earlier in the feature.xml file.</span><span class="sxs-lookup"><span data-stu-id="a27e6-p110">Open the code file and uncomment the FeatureUpgrading method, which overrides the **FeatureUpgrading(SPFeatureReceiverProperties, String, IDictionary<String, String>)** method. The following example applies the `My15MasterPage` file that was specified earlier in the feature.xml file.</span></span>
    
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

<span data-ttu-id="a27e6-135">После завершения обновления может потребоваться будущих и долгосрочного обслуживания для функции, учитывайте следующее.</span><span class="sxs-lookup"><span data-stu-id="a27e6-135">Once you're done with the upgrade, you'll want to think about the future and long-term maintenance of your feature.</span></span> <span data-ttu-id="a27e6-136">Руководство по обслуживанию код с полным доверием, обратитесь к [Управление жизненным циклом приложений в SharePoint 2010](http://msdn.microsoft.com/en-us/library/office/gg604045%28v=office.14%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a27e6-136">Refer to  [Application Lifecycle Management in SharePoint 2010](http://msdn.microsoft.com/en-us/library/office/gg604045%28v=office.14%29.aspx) for guidance on maintaining full-trust code.</span></span> <span data-ttu-id="a27e6-137">Хотя данная статья относится к SharePoint 2010 в частности, применяется одинаково для кода с полным доверием в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a27e6-137">Although this article refers to SharePoint 2010 specifically, it applies equally well to full-trust code in SharePoint.</span></span> <span data-ttu-id="a27e6-138">Если вы не знакомы с действиями управление версиями и обновление компонента, обратитесь к разделу [модели управления жизненным циклом решений](http://msdn.microsoft.com/en-us/library/office/gg604045%28v=office.14%29.aspx#sectionSection7) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="a27e6-138">If you aren't familiar with feature versioning and upgrade actions, refer to the [Models for Solution Lifecycle Management](http://msdn.microsoft.com/en-us/library/office/gg604045%28v=office.14%29.aspx#sectionSection7) section of this article.</span></span> <span data-ttu-id="a27e6-139">Следует также рассмотрим [Советы и рекомендации для версий с помощью компонента](http://msdn.microsoft.com/en-us/library/office/ee535064%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a27e6-139">You should also look at [Best Practices for Using Feature Versions](http://msdn.microsoft.com/en-us/library/office/ee535064%28v=office.14%29.aspx).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="a27e6-140">См. также</span><span class="sxs-lookup"><span data-stu-id="a27e6-140">See also</span></span>
<span data-ttu-id="a27e6-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a27e6-141"></span></span>


-  [<span data-ttu-id="a27e6-142">Развертывание настраиваемых компонентов в обновленных семействах сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="a27e6-142">Deploy custom features to upgraded site collections in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/dn673579%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="a27e6-143">Обновление настроек сайта для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a27e6-143">Upgrade site customizations for SharePoint</span></span>](upgrade-site-customizations-for-sharepoint.md)
    
  
-  [<span data-ttu-id="a27e6-144">Обновления для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a27e6-144">Upgrade to SharePoint</span></span>](http://technet.microsoft.com/en-us/library/cc303420%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="a27e6-145">Пакет решения SharePoint и SharePoint Online для фирменной настройки и подготовки сайта</span><span class="sxs-lookup"><span data-stu-id="a27e6-145">SharePoint and SharePoint Online solution pack for branding and site provisioning</span></span>](http://www.microsoft.com/en-us/download/details.aspx?id=42030)
    
  
-  [<span data-ttu-id="a27e6-146">Установка и управление решениями для SharePoint</span><span class="sxs-lookup"><span data-stu-id="a27e6-146">Install and manage solutions for SharePoint</span></span>](http://technet.microsoft.com/en-us/library/cc263205%28v=office.15%29.aspx)
    
  

