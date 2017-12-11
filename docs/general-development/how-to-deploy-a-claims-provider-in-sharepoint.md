---
title: "Развертывание поставщика утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3a5fcedc-aa9a-4ff4-95c0-0e0a7dea9d1f
ms.openlocfilehash: 06b647062eaa4fcd29442e02dce5e67e02943213
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="deploy-a-claims-provider-in-sharepoint"></a>Развертывание поставщика утверждений в SharePoint

Узнайте, как развернуть поставщика утверждений SharePoint с использованием инфраструктуры функций и созданием класса, наследуемого из  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) .

## <a name="deploying-a-claims-provider-as-part-of-a-setup"></a>Развертывание поставщика утверждений как часть процесса установки
<a name="SP15_HowToDeployClaimsProvider_DeployingClaimsSetup"> </a>

С помощью инфраструктуру функций  это самый простой способ развертывания поставщика утверждений. Для этого сначала определения компонента и приемника компонента, который является производным от класса  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) и переопределяют базовые свойства.
  
    
    
Ниже приведен пример того, как это сделать.
  
    
    



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


## <a name="deploying-a-claims-provider-using-the-feature-infrastructure"></a>Развертывание с помощью инфраструктуры компонента поставщика утверждений
<a name="SP15_HowToDeployClaimsProvider_DeployingClaimsFeature"> </a>

Ниже приведен пример, в котором показано, как для определения компонента и приемника компонента, который является производным от  [SPClaimProviderFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.Administration.Claims.SPClaimProviderFeatureReceiver.aspx) и переопределяют базовые свойства.
  
    
    

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


## <a name="see-also"></a>См. также
<a name="SP15_HowToDeployClaimsProvider_AdditionalResources"> </a>


-  [Удостоверение, основанное на основе утверждений в SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Входящих утверждений: вход в SharePoint](incoming-claims-signing-into-sharepoint.md)
    
  
-  [Поставщик утверждений в SharePoint](claims-provider-in-sharepoint.md)
    
  
-  [Как: создать поставщик утверждений в SharePoint](how-to-create-a-claims-provider-in-sharepoint.md)
    
  

