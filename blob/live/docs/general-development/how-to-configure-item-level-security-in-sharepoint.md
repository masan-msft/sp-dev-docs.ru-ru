---
title: "Настройка безопасности на уровне элементов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ffd730f2-e7b7-4707-b677-d073da7df7d7
ms.openlocfilehash: 4513b317f79dfe5a5382e162d931db9bd980a32f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-configure-item-level-security-in-sharepoint"></a><span data-ttu-id="3d3ab-102">Как: настройка безопасности на уровне элементов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d3ab-102">How to: Configure item-level security in SharePoint</span></span>
<span data-ttu-id="3d3ab-103">Узнайте, как настроить безопасность уровня элементов при обходе внешних данных с помощью соединителей индексации BCS в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-103">Learn how to configure item level security when crawling external data with BCS indexing connectors in SharePoint.</span></span>
## <a name="external-systems-with-ntlm-authentication"></a><span data-ttu-id="3d3ab-104">Внешние системы с проверкой подлинности NTLM</span><span class="sxs-lookup"><span data-stu-id="3d3ab-104">External systems with NTLM authentication</span></span>
<span data-ttu-id="3d3ab-105"><a name="ItemLevelSecurity_NTLMAuth"> </a></span><span class="sxs-lookup"><span data-stu-id="3d3ab-105"></span></span>

<span data-ttu-id="3d3ab-p101">Для внешних систем, поддерживающих проверку подлинности NTLM, дескриптор безопасности для каждого экземпляра внешнего типа контента можно получить во время обхода контента и сохранить его в индексе контента. Во время выполнения запроса дескриптор безопасности пользователя, отправляющего поисковый запрос, сопоставляется с сохраненным дескриптором безопасности, что позволяет определить наличие у пользователя прав доступа к элементу. Это самый быстрый способ выполнения фильтрации по ролям безопасности для набора результатов. Модель метаданных для внешней системы должна содержать указание на расположение, где дескриптор безопасности размещен как поле или метод внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-p101">For external systems that support NTLM authentication, the security descriptor can be obtained for each instance of the external content type at crawl time and stored in the content index. During query time, the security descriptor of the user who is submitting the search query is compared to the stored security descriptor to determine whether the user has access to the item. This is the fastest way to perform security trimming on the result set. The metadata model for the external system must indicate where the security descriptor can be found as an external content type field or method.</span></span>
  
    
    

### <a name="external-content-type-field"></a><span data-ttu-id="3d3ab-110">Поле внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="3d3ab-110">External content type field</span></span>
<span data-ttu-id="3d3ab-111"><a name="ItemLevelSecurity_ExtTypeField"> </a></span><span class="sxs-lookup"><span data-stu-id="3d3ab-111"></span></span>

<span data-ttu-id="3d3ab-112">Microsoft SharePoint сохраняет дескриптор безопасности, если поле внешнего типа контента, содержащее дескриптор, помечено посредством использования свойства **WindowsSecurityDescriptorField** , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-112">Microsoft SharePoint stores the security descriptor if the field of the external content type that contains the descriptor is marked by using the **WindowsSecurityDescriptorField** property, as shown in the following example.</span></span>
  
    
    

```XML

<Method Name="Item SpecificFinder ">
  <Properties>
    <Property Name="RdbCommandType" Type="System.Data.CommandType, System.Data, 
 Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">Text</Property>
    <Property Name="RdbCommandText" Type="System.String">SELECT [Identifier] , 
 [SecurityDescriptor] FROM [Test].[dbo].[Items] WHERE [Identifier] = @Identifier</Property>
    <Property Name="BackEndObjectType" Type="System.String">SqlServerTable</Property>
    <Property Name="BackEndObject" Type="System.String">Items</Property>
    <Property Name="Schema" Type="System.String">dbo</Property>
  </Properties>
  <Parameters>
    <Parameter Direction="In" Name="@Identifier">
      <TypeDescriptor TypeName="System.Int32" IdentifierName="Identifier" Name="Identifier" />
    </Parameter>
    <Parameter Direction="Return" Name="BaseItemsRead Item">
      <TypeDescriptor TypeName="System.Data.IDataReader, System.Data, Version=2.0.0.0, 
Culture=neutral, PublicKeyToken=b77a5c561934e089" IsCollection="true" Name="BaseItemsRead Item">
        <TypeDescriptors>
          <TypeDescriptor TypeName="System.Data.IDataRecord, System.Data, Version=2.0.0.0, 
Culture=neutral, PublicKeyToken=b77a5c561934e089" Name="BaseItemsRead ItemElement">
          <TypeDescriptors>
            <TypeDescriptor TypeName="System.Int32" IdentifierName="Identifier" Name="Identifier"/>
            <TypeDescriptor TypeName="System.Byte[], mscorlib, Version=2.0.0.0, 
Culture=neutral, PublicKeyToken=b77a5c561934e089" IsCollection="true" Name="SecurityDescriptor">
              <TypeDescriptors>
                <TypeDescriptor TypeName="System.Byte" Name="SecurityDescriptorElement" />
              </TypeDescriptors>
            </TypeDescriptor>
            </TypeDescriptors>
          </TypeDescriptor>
          </TypeDescriptors>
        </TypeDescriptor>
      </Parameter>
    </Parameters>
    <MethodInstances>
      <MethodInstance Type="SpecificFinder" ReturnParameterName="BaseItemsRead Item"
 ReturnTypeDescriptorName="BaseItemsRead ItemElement" Name="BaseItemsRead Item"
DefaultDisplayName="ReadSecurity">
        <Properties>
          <Property Name="WindowsSecurityDescriptorField" Type="System.String">
                SecurityDescriptor
          </Property>
        </Properties>
      </MethodInstance>
    </MethodInstances>
</Method>
```


> <span data-ttu-id="3d3ab-113">**Примечание:** Если вы вернетесь дескриптор безопасности в поле внешний тип контента, нельзя использовать кэширования клиентов.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-113">**Note:** If you return the security descriptor as a field of the external content type, you cannot use client caching.</span></span> <span data-ttu-id="3d3ab-114">Это так, как кэшированные элементы ограничены определенного размера, можно легко превысить какие списки управления доступом (ACL).</span><span class="sxs-lookup"><span data-stu-id="3d3ab-114">This is because cached items are limited to a specific size, which access control lists (ACL) can easily exceed.</span></span> <span data-ttu-id="3d3ab-115">Таким образом инфраструктура соединителей поиска игнорирует запросы к элементам кэша, если они содержат поля дескриптор безопасности.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-115">Therefore, the Search connector framework ignores requests to cache items if they contain a security descriptor field.</span></span> 
  
    
    


### <a name="external-content-type-method"></a><span data-ttu-id="3d3ab-116">Метод внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="3d3ab-116">External content type method</span></span>
<span data-ttu-id="3d3ab-117"><a name="ItemLevelSecurity_ExtTypeMethod"> </a></span><span class="sxs-lookup"><span data-stu-id="3d3ab-117"></span></span>

<span data-ttu-id="3d3ab-118">При наличии метода, определенного в модели метаданных, возвращающей дескриптор безопасности для элемента в зависимости от его идентификатора, можно использовать стереотип метода **BinarySecurityDescriptorAccessor**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-118">If you have a method defined in the metadata model that returns the security descriptor for an item based on its identifier, you can use the **BinarySecurityDescriptorAccessor** method stereotype, as shown in the following example.</span></span>
  
    
    

```XML

<Method Name="GetItemSecurity" LobName="GetItemSecurity">
  <Parameters>
    <Parameter Name="itemId" Direction="In">
      <TypeDescriptor Name="itemId" TypeName="System.Int32, mscorlib, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" 
IdentifierEntityNamespace="MS.Internal.Test.Automation.Search.Scater" 
IdentifierEntityName="Item" IdentifierName="ItemId" /> 
    </Parameter>
    <Parameter Name="Return" Direction="Return">
      <TypeDescriptor Name="SecurityDescriptor" TypeName="System.Byte[],
mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" 
IsCollection="true">
        <TypeDescriptors>
          <TypeDescriptor Name="Item" TypeName="System.Byte, mscorlib, 
Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </TypeDescriptors>
      </TypeDescriptor>
    </Parameter>
  </Parameters>
  <MethodInstances>
    <MethodInstance Name="GetItemSecurity_Instance" Type="BinarySecurityDescriptorAccessor"
 ReturnParameterName="Return" ReturnTypeDescriptorName="SecurityDescriptor" 
ReturnTypeDescriptorLevel="0">
      <Properties>
        <Property Name="WindowsSecurityDescriptorField" Type="System.String">
            SecurityDescriptor
        </Property>
      </Properties>
      <AccessControlList>
        <AccessControlEntry Principal="NT AUTHORITY\\Authenticated Users">
          <Right BdcRight="Execute" />
        </AccessControlEntry>
      </AccessControlList>
    </MethodInstance>
  </MethodInstances>
</Method>
```

<span data-ttu-id="3d3ab-119">Следующий код представляет собой подпись метода для метода, заданного в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-119">The following code is the method signature for the method that is specified in the previous example.</span></span>
  
    
    



```cs

Public static Byte[]GetItemSecurity (string  id)
{

}
```


## <a name="external-systems-with-authentication-schemes-that-can-be-mapped-to-ntlm-authentication"></a><span data-ttu-id="3d3ab-120">Внешние системы, содержащие схемы проверки подлинности, которые могут сопоставляться с проверкой подлинности NTLM</span><span class="sxs-lookup"><span data-stu-id="3d3ab-120">External systems with authentication schemes that can be mapped to NTLM authentication</span></span>
<span data-ttu-id="3d3ab-121"><a name="ItemLevelSecurity_MappedToNTLM"> </a></span><span class="sxs-lookup"><span data-stu-id="3d3ab-121"></span></span>

<span data-ttu-id="3d3ab-p103">Если внешние системы не поддерживают проверку подлинности NTLM, но при этом пользователи внешней системы могут быть сопоставлены пользователям Windows посредством таблицы сопоставления, можно использовать подход, описанный в двух предыдущих примерах кода, в целях обеспечения безопасности на уровне элемента. В целях обеспечения работоспособности этой схемы веб-служба или служба Windows Communication Foundation (WCF), представленная внешней системой, должна включать метод, который выполняет внутреннее преобразование пользователей внешней системы в пользователей Windows, после чего возвращает дескриптор безопасности Windows для каждого URL-адреса. В следующем примере рассматривается создание кода такого метода.</span><span class="sxs-lookup"><span data-stu-id="3d3ab-p103">If the external system does not support NTLM authentication, but the external system users can be mapped to Windows users by using a mapping table, you can use the approach described in the previous two code examples to provide item level security. For this to work, the web service or Windows Communication Foundation (WCF) service exposed by the external system must include a method that converts the external system users to Windows users internally, and then returns a Windows security descriptor for each URL. The following example shows how you could code this method.</span></span> 
  
    
    

```cs

/// Returns the security descriptor for a user.
/// </summary>
/// <param name="domain"></param>
/// <param name="username"></param>
/// <returns></returns>

private Byte[] GetSecurityDescriptor(string domain, string username)
{
   NTAccount acc = new NTAccount(domain, username);
   SecurityIdentifier sid = (SecurityIdentifier)acc.Translate(typeof(SecurityIdentifier));
   CommonSecurityDescriptor sd = new CommonSecurityDescriptor(false, false, ControlFlags.None,
sid, null, null, null);
   sd.SetDiscretionaryAclProtection(true, false);

//Deny access to all users.
   SecurityIdentifier everyone = new SecurityIdentifier(WellKnownSidType.WorldSid, null);
   sd.DiscretionaryAcl.RemoveAccess(AccessControlType.Allow, everyone, 
unchecked((int)0xffffffffL), InheritanceFlags.None, PropagationFlags.None);

//Grant full access to a specified user.
   sd.DiscretionaryAcl.AddAccess(AccessControlType.Allow, sid, 
unchecked((int)0xffffffffL), InheritanceFlags.None, PropagationFlags.None);
 
   byte[] secDes = new Byte[sd.BinaryLength];
   sd.GetBinaryForm(secDes, 0);

   return secDes;
}
```


## <a name="additional-resources"></a><span data-ttu-id="3d3ab-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3d3ab-125">Additional resources</span></span>
<span data-ttu-id="3d3ab-126"><a name="SP15Itemlevelsec_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3d3ab-126"></span></span>


-  [<span data-ttu-id="3d3ab-127">Инфраструктура соединителей поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d3ab-127">Search connector framework in SharePoint</span></span>](search-connector-framework-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3d3ab-128">Реализация метода BinarySecurityDescriptorAccessor</span><span class="sxs-lookup"><span data-stu-id="3d3ab-128">Implementing a BinarySecurityDescriptorAccessor</span></span>](http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="3d3ab-129">Улучшение файла модели BDC для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3d3ab-129">Enhancing the BDC model file for Search in SharePoint</span></span>](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  

