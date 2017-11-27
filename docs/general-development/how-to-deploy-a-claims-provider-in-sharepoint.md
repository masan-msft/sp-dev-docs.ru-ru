---
title: "Развертывание поставщика утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3a5fcedc-aa9a-4ff4-95c0-0e0a7dea9d1f
ms.openlocfilehash: ef8377ceea402d2cc0573fbd5443974284f8ee7f
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="deploy-a-claims-provider-in-sharepoint"></a><span data-ttu-id="7c748-102">Развертывание поставщика утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7c748-102">Deploy a claims provider in SharePoint</span></span>

<span data-ttu-id="7c748-103">Узнайте, как развернуть поставщика утверждений SharePoint с использованием инфраструктуры функций и созданием класса, наследуемого из  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7c748-103">Learn how to deploy a SharePoint claims provider by using the features infrastructure and creating a class that inherits from  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) .</span></span>

## <a name="deploying-a-claims-provider-as-part-of-a-setup"></a><span data-ttu-id="7c748-104">Развертывание поставщика утверждений как часть процесса установки</span><span class="sxs-lookup"><span data-stu-id="7c748-104">Deploying a claims provider as part of a setup</span></span>
<span data-ttu-id="7c748-105"><a name="SP15_HowToDeployClaimsProvider_DeployingClaimsSetup"> </a></span><span class="sxs-lookup"><span data-stu-id="7c748-105"></span></span>

<span data-ttu-id="7c748-p101">С помощью инфраструктуру функций  это самый простой способ развертывания поставщика утверждений. Для этого сначала определения компонента и приемника компонента, который является производным от класса  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) и переопределяют базовые свойства.</span><span class="sxs-lookup"><span data-stu-id="7c748-p101">The easiest way to deploy a claims provider is by using the features infrastructure. To do this, first define a feature and a feature receiver that derives from the  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) class, and override the base properties.</span></span>
  
    
    
<span data-ttu-id="7c748-108">Ниже приведен пример того, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="7c748-108">The following is an example of how to do this.</span></span>
  
    
    



```cs

public class MyClaimProviderFeatureReceiver : SPClaimProviderFeatureReceiver
    {
        public override string ClaimProviderAssembly { get { return typeof(MyClaimProvider).Assembly.FullName; } }
        public override string ClaimProviderType { get { return typeof(MyClaimProvider).FullName; } }
        public override string ClaimProviderDisplayName
        {
            get
            {
                return StringResourceManager.GetString(MyLocalizedClaimProviderName);
            }
        }
        public override string ClaimProviderDescription
        {
            get
            {
                return StringResourceManager.GetString(MyLocalizedClaimProviderDescription);
            }
            }
    }
```


## <a name="deploying-a-claims-provider-using-the-feature-infrastructure"></a><span data-ttu-id="7c748-109">Развертывание с помощью инфраструктуры компонента поставщика утверждений</span><span class="sxs-lookup"><span data-stu-id="7c748-109">Deploying a claims provider using the feature infrastructure</span></span>
<span data-ttu-id="7c748-110"><a name="SP15_HowToDeployClaimsProvider_DeployingClaimsFeature"> </a></span><span class="sxs-lookup"><span data-stu-id="7c748-110"></span></span>

<span data-ttu-id="7c748-111">Ниже приведен пример, в котором показано, как для определения компонента и приемника компонента, который является производным от  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) и переопределяют базовые свойства.</span><span class="sxs-lookup"><span data-stu-id="7c748-111">The following is a sample that demonstrates how to define a feature and a feature receiver that derives from  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) and override the base properties.</span></span>
  
    
    

```cs

// Sample claims provider feature receiver class through which
// the sample claims provider registers itself 
// with the Microsoft.SharePoint.Administration.Claims.SPClaimProviderManager class.

using System;
using Microsoft.SharePoint.Administration;
using Microsoft.SharePoint.Administration.Claims;

namespace MySample.Sample.Server.SampleClaimsProvider
{
    /// <summary>
    /// The NameIdentifierClaimProviderFeatureReceiver class is a feature receiver class
    /// that registers the claims provider with the claims provider manager.
    /// </summary>
    
    [Microsoft.SharePoint.Security.SharePointPermission(System.Security.Permissions.SecurityAction.Demand, ObjectModel = true)]
    public sealed class NameIdentifierClaimProviderFeatureReceiver : SPClaimProviderFeatureReceiver
    {
        #region Private Methods
        /// <summary>
        /// Because use of base keyword can lead to unverifiable code inside a lambda expression, 
        /// this function is created as a wrapper for the base.FeatureActivated function.
        /// This function gets called in the following lambda expression.
        /// </summary>
        
        /// <param name="properties">Represents the properties of a feature activation.</param>
        /// <returns> void </returns>

        private void ExecBaseFeatureActivated(Microsoft.SharePoint.SPFeatureReceiverProperties properties)
        {
            base.FeatureActivated(properties);
        }
        #endregion Private Methods

        #region Public Method\\Properties
        /// <summary>
        /// Gets the fully qualified name of the MySample.Sample.Server.SampleClaimsProvider assembly.
        /// </summary>
        
        /// <returns>String representing fully qualified name of the MySample.Sample.Server.SampleClaimsProvider
        /// assembly.</returns>
        public override string ClaimProviderAssembly
        {
            get{ return typeof(SampleNameIdClaimProvider).Assembly.FullName; }
        }

        /// <summary>
        /// Gets the fully qualified name of the claims provider type, including the namespace of the type. 
        /// </summary>
        /// <returns>String representing the fully qualified name of the 
        ///SampleNameIdClaimProvider class.</returns>
        public override string ClaimProviderType
        {
            get{ return typeof(NameIdentifierClaimProvider).FullName; }
        }

        /// <summary>
        /// Gets the display name of the claims provider.
        /// </summary>
        
        /// <returns>String representing display name of the claim provider.</returns>
        public override string ClaimProviderDisplayName
        {
            get{ return "Sample NameId Claim Provider"; }
        }

        /// <summary>
        /// Gets the description about the claims provider. 
        /// </summary>
        
        /// <returns>String representing the description about the SampleClaimProvider.</returns>
        public override string ClaimProviderDescription
        {
            get
            {
                return "This feature adds SampleNameId claim type in the SAML token created by the STS.";
            }
        }

        /// <summary>
        /// This methods gets called after the activation of the feature.
        /// </summary>
        
        /// <param name="properties">Represents the properties of a feature activation<./param>
        /// <returns>void.</returns>
        public override void FeatureActivated(Microsoft.SharePoint.SPFeatureReceiverProperties properties)
        {     
            {
                ExecBaseFeatureActivated(properties);
            }            
        }
        #endregion Public Method\\Properties
    }
}

```


## <a name="additional-resources"></a><span data-ttu-id="7c748-112">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7c748-112">Additional resources</span></span>
<span data-ttu-id="7c748-113"><a name="SP15_HowToDeployClaimsProvider_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="7c748-113"></span></span>


-  [<span data-ttu-id="7c748-114">Удостоверение, основанное на основе утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7c748-114">Claims-based identity in SharePoint</span></span>](claims-based-identity-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7c748-115">Входящих утверждений: вход в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7c748-115">Incoming claims: Signing into SharePoint</span></span>](incoming-claims-signing-into-sharepoint.md)
    
  
-  [<span data-ttu-id="7c748-116">Поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7c748-116">Claims provider in SharePoint</span></span>](claims-provider-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7c748-117">Как: создать поставщик утверждений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7c748-117">How to: Create a claims provider in SharePoint</span></span>](how-to-create-a-claims-provider-in-sharepoint.md)
    
  

