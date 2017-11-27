---
title: "Настройка безопасности на уровне элементов в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ffd730f2-e7b7-4707-b677-d073da7df7d7
ms.openlocfilehash: ce2ece9f7f4f35fa3235d26ab384dc3783b333c7
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="configure-item-level-security-in-sharepoint"></a>Настройка безопасности на уровне элементов в SharePoint

Узнайте, как настроить безопасность уровня элементов при обходе внешних данных с помощью соединителей индексации BCS в SharePoint.

## <a name="external-systems-with-ntlm-authentication"></a>Внешние системы с проверкой подлинности NTLM
<a name="ItemLevelSecurity_NTLMAuth"> </a>

Для внешних систем, поддерживающих проверку подлинности NTLM, дескриптор безопасности для каждого экземпляра внешнего типа контента можно получить во время обхода контента и сохранить его в индексе контента. Во время выполнения запроса дескриптор безопасности пользователя, отправляющего поисковый запрос, сопоставляется с сохраненным дескриптором безопасности, что позволяет определить наличие у пользователя прав доступа к элементу. Это самый быстрый способ выполнения фильтрации по ролям безопасности для набора результатов. Модель метаданных для внешней системы должна содержать указание на расположение, где дескриптор безопасности размещен как поле или метод внешнего типа контента.
  
    
    

### <a name="external-content-type-field"></a>Поле внешнего типа контента
<a name="ItemLevelSecurity_ExtTypeField"> </a>

Microsoft SharePoint сохраняет дескриптор безопасности, если поле внешнего типа контента, содержащее дескриптор, помечено посредством использования свойства **WindowsSecurityDescriptorField** , как показано в следующем примере.
  
    
    

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


> **Примечание:** Если вы вернетесь дескриптор безопасности в поле внешний тип контента, нельзя использовать кэширования клиентов. Это так, как кэшированные элементы ограничены определенного размера, можно легко превысить какие списки управления доступом (ACL). Таким образом инфраструктура соединителей поиска игнорирует запросы к элементам кэша, если они содержат поля дескриптор безопасности. 
  
    
    


### <a name="external-content-type-method"></a>Метод внешнего типа контента
<a name="ItemLevelSecurity_ExtTypeMethod"> </a>

При наличии метода, определенного в модели метаданных, возвращающей дескриптор безопасности для элемента в зависимости от его идентификатора, можно использовать стереотип метода **BinarySecurityDescriptorAccessor**, как показано в следующем примере.
  
    
    

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

Следующий код представляет собой подпись метода для метода, заданного в предыдущем примере.
  
    
    



```cs

Public static Byte[]GetItemSecurity (string  id)
{

}
```


## <a name="external-systems-with-authentication-schemes-that-can-be-mapped-to-ntlm-authentication"></a>Внешние системы, содержащие схемы проверки подлинности, которые могут сопоставляться с проверкой подлинности NTLM
<a name="ItemLevelSecurity_MappedToNTLM"> </a>

Если внешние системы не поддерживают проверку подлинности NTLM, но при этом пользователи внешней системы могут быть сопоставлены пользователям Windows посредством таблицы сопоставления, можно использовать подход, описанный в двух предыдущих примерах кода, в целях обеспечения безопасности на уровне элемента. В целях обеспечения работоспособности этой схемы веб-служба или служба Windows Communication Foundation (WCF), представленная внешней системой, должна включать метод, который выполняет внутреннее преобразование пользователей внешней системы в пользователей Windows, после чего возвращает дескриптор безопасности Windows для каждого URL-адреса. В следующем примере рассматривается создание кода такого метода. 
  
    
    

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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Itemlevelsec_addlresources"> </a>


-  [Инфраструктура соединителей поиска в SharePoint](search-connector-framework-in-sharepoint.md)
    
  
-  [Реализация метода BinarySecurityDescriptorAccessor](http://msdn.microsoft.com/library/6cf70490-dd3c-49cd-bb13-ed33e938435d%28Office.15%29.aspx)
    
  
-  [Улучшение файла модели BDC для поиска в SharePoint](enhancing-the-bdc-model-file-for-search-in-sharepoint.md)
    
  

