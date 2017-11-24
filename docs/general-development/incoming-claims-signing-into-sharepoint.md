---
title: "Входящая подписывание на основе утверждений в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 08c687aa-e485-4269-aea8-4333da3588a5
ms.openlocfilehash: 982b9d2b6f65c73223ed4c317e631b017d87c980
ms.sourcegitcommit: d68d6cf927d69696a3561f7d8ffe9a3ed9dbd03c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="incoming-claims-signing-into-sharepoint"></a>Входящих утверждений: вход в SharePoint

## <a name="signing-in-to-sharepoint"></a>Вход в SharePoint

При входе пользователя в систему SharePoint Server, маркер пользователя проверка и затем используется для входа в SharePoint. Маркер пользователя  это маркер безопасности, выданный поставщика утверждений.
  
    
    

> **Примечание:** Сведения о проверки подлинности для одной фермы SharePoint и проверки подлинности утверждений между фермами SharePoint можно [планирование проверки подлинности на основе утверждений](http://technet.microsoft.com/en-us/library/cc262350.aspx) на сайте TechNet.
  
    
    


### <a name="windows-claims-mode-sign-in"></a>Режим входа на основе утверждений Windows

В Windows утверждений режим входа на основе входа в происходит на запрос проверки подлинности встроенная проверка подлинности Windows с помощью согласование (NTLM/Kerberos). Однако после создания объекта  [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) (который представляет пользователя Windows), SharePoint Server преобразует объект [WindowsIdentity](https://msdn.microsoft.com/library/System.Security.Principal.WindowsIdentity.aspx) в объект [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) (который представляет представление на основе утверждений для пользователя).
  
    
    
затем SharePoint Server делает расширения утверждений и обрабатывает получившийся маркер, который был создан с SharePoint Server. Это означает, что некоторые функции (например, одним экземпляром поддержка для приложения-службы и пользовательских поставщиков утверждений) в SharePoint Server работы, даже если клиенты считаете, SharePoint Server в основном режиме входа в систему Windows. Интерфейс входа в режим утверждений Windows является встроенной по умолчанию для SharePoint Server. 
  
    
    
Все типы входа в утверждений используют пассивный вход. Пассивный вход происходит с помощью Windows задачей, но со страницы отдельный вход, поступает через 302 перенаправления. Этот режим полезен, когда более одного способа включена, а пользователь должен выбрать между поставщиками утверждений, поддерживаемых. Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office. Некоторые клиенты Office выполните другой протокол.
  
    
    

### <a name="saml-passive-sign-in-mode"></a>режим пассивного входа SAML;

В разметке языка SAML (Security Assertion) пассивный вход, при входе пользователя в, клиента (это может быть веб-страницы) перенаправляется поставщика утверждений назначенного (например, Windows Live ID поставщика утверждений). После поставщика утверждений выполняет проверку подлинности пользователя, SharePoint Server принимает SAML маркеров доклад поставщика утверждений, обрабатывает маркер SAML, а затем дополняет утверждений.
  
    
    
Для поставщиков на основе SAML-утверждений поставщика утверждений как федерации Active Directory Services (ADFS) и поставщика утверждений Windows Live ID, вход с помощью SAML пассивный режим входа является единственным способом. SAML пассивный вход является модель SharePoint online удостоверения.
  
    
    

> **Примечание:** SAML пассивный вход описывает процесс входа. Когда вход для веб-приложения настроен на прием маркеров из поставщика доверенных входа в систему, этот тип входа называется SAML пассивный вход. Поставщика доверенных входа в систему — это внешние (то есть, внешними по отношению к SharePoint) служба маркеров безопасности (STS), доверяющей SharePoint. 
  
    
    

Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office.
  
    
    

### <a name="aspnet-membership-and-role-passive-sign-in"></a>пассивный вход с помощью членства ASP.NET и роли;

В ASP.NET членства и ролей пассивный вход входа в происходит путем перенаправления клиента на веб-страницу, где размещены элементы управления ASP.NET в журнал. После создания объекта идентификатор, представляющий идентификатор пользователя, SharePoint Server преобразует его в объект  [ClaimsIdentity](https://msdn.microsoft.com/library/Microsoft.IdentityModel.Claims.ClaimsIdentity.aspx) (который представляет представление на основе утверждений для пользователя).
  
    
    
SharePoint Server то выполняет расширения утверждений. Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office.
  
    
    

### <a name="windows-classic-mode-sign-in"></a>Классический режим входа Windows

Учетное классического режима Windows поддерживается в этой версии. В Windows классический режим входа на основе входа в происходит с запросом встроенная проверка подлинности с помощью согласование (NTLM/Kerberos). Выполняется без расширения утверждений, поэтому некоторые функции (например, одним экземпляром поддержка для приложения-службы и пользовательских поставщиков утверждений) не работают при входе пользователя в в этом режиме.
  
    
    
Некоторые приложения-службы может также потребоваться режим утверждений для некоторых функций. 
  
    
    

### <a name="anonymous-access"></a>анонимный доступ;

Можно включить анонимный доступ для веб-приложения. Администраторы сайтов в веб-приложении можно разрешить анонимный доступ. Если анонимные пользователи требуется получить доступ к защищенным ресурсам, они нажмите кнопку входа в систему, чтобы предоставить учетные данные. 
  
    
    
SharePoint Server то выполняет расширения утверждений. Клиенты Win32 должна поддерживать проверку подлинности на основе форм, реализованные в клиентах Office.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Удостоверение, основанное на основе утверждений в SharePoint](claims-based-identity-in-sharepoint.md)
    
  
-  [Поставщик утверждений в SharePoint](claims-provider-in-sharepoint.md)
    
  
-  [Как: создать поставщик утверждений в SharePoint](how-to-create-a-claims-provider-in-sharepoint.md)
    
  
-  [Как: развернуть поставщик утверждений в SharePoint](how-to-deploy-a-claims-provider-in-sharepoint.md)
    
  
