---
title: "Сведения о выполнении авторизации для клиентов, размещенных в средах Германии, Китай и правительственных \"мне Нравится\""
ms.date: 11/03/2017
ms.openlocfilehash: 537ab7cc5b7536ba977a9563639271ef5620559d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="authorization-considerations-for-tenants-hosted-in-the-germany-china-or-us-government-environments"></a>Сведения о выполнении авторизации для клиентов, размещенных в средах Германии, Китай и правительственных "мне Нравится"

Если клиент Office 365 размещено в среде, определенные как Германия, Китай или "мне Нравится" государственных среды, то нужен это в учетной записи при разработке для вашего клиента. 

_**Применимо к:** Office 365, размещенных в средах Германии, Китай и правительственных "мне Нравится"_


## <a name="introduction"></a>Введение
<a name="introduction"> </a>

Корпорация Майкрософт конкретных развертываний Office 365 в Германию, Китай и для государственных учреждений "мне Нравится" для удовлетворения соответствующих определенным правилам в тех областях. Следующие ссылки предоставляют дополнительные контекста:
- [Office 365 Германия](https://technet.microsoft.com/en-us/library/mt793278.aspx)
- [Office 365 обслуживается 21Vianet (Китай)](https://technet.microsoft.com/en-us/library/mt651782.aspx)
- [Office 365 государственных организаций США.](https://technet.microsoft.com/library/mt774581.aspx)

Если вы являетесь разработчиком целевого приложения для SharePoint Online, размещенных в этих средах then необходимо воспользоваться учетной записью, имеющей эти среды собственные выделенные конечные точки проверки подлинности Azure AD, как разработчик необходимо использовать. Ниже главы поясняется, как использовать эти выделенного конечных точек для типичного параметров настройки SharePoint Online.

## <a name="using-azure-ad-to-authorize"></a>С помощью Azure AD для авторизации
<a name="usingazureadtoauthorize"> </a>

### <a name="azure-ad-endpoints"></a>Конечные точки Azure AD
<a name="adendpoints"> </a>

Когда приложению Azure AD для авторизации необходимо использовать правильный конечной точки. Приведенной ниже таблице описаны конечных точек для использования в зависимости от того, где был определен приложения Azure AD:

|**Среда**|**Конечная точка**|
|:-----|:-----|
| Рабочая | https://Login.Windows.NET |
| Германия | https://Login.microsoftonline.de |
| Китай | https://Login.chinacloudapi.CN |
| Правительства США | https://Login-US.microsoftonline.com |

### <a name="using-pnp-to-authorize-using-azure-ad"></a>С помощью PnP для авторизации с помощью Azure AD
<a name="adpnp"> </a>

PnP [помощью класса AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) предлагает простой способ получить объект SharePoint ClientContext при использовании приложения Azure AD. Затронутые методы были расширены с помощью дополнительного `AzureEnvironment` enum

```c#
/// <summary>
/// Enum to identify the supported Office 365 hosting environments
/// </summary>
public enum AzureEnvironment
{
    Production=0,
    PPE=1,
    China=2,
    Germany=3,
    USGovernment=4
}
```

Ниже фрагменте показано только приложения на авторизации, обратите внимание на то последним параметром в `GetAzureADAppOnlyAuthenticatedContext` метод:
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "079d8797-cebc-4cda-a3e0-xxxx"; 
string pfxPassword = "my password";
ClientContext cc = new AuthenticationManager().GetAzureADAppOnlyAuthenticatedContext(siteUrl, 
            aadAppId, "contoso.onmicrosoft.de", @"C:\contoso.pfx", pfxPassword, AzureEnvironment.Germany);
```

Другой фрагмент, на котором отображается интерактивного пользователя для входа с помощью `GetAzureADNativeApplicationAuthenticatedContext` метод:

```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string aadAppId = "ff76a9f4-430b-4ee4-8602-xxxx"; 
ClientContext cc = new AuthenticationManager().GetAzureADNativeApplicationAuthenticatedContext(siteUrl, 
            aadAppId, "https://contoso.com/test", environment: AzureEnvironment.Germany);
```

## <a name="using-azure-acs-to-authorize-your-sharepoint-add-in"></a>С помощью Azure ACS для авторизации надстройки SharePoint
<a name="usingazureacs"> </a>

При создании SharePoint надстроек они будут авторизации обычно низким уровнем доверия, зависит от Azure ACS как descrived в [создании SharePoint Add-ins, использующих авторизации с низким уровнем доверия](https://msdn.microsoft.com/en-us/library/office/dn790707.aspx).


### <a name="azure-acs-endpoints"></a>Конечные точки Azure ACS
<a name="endpointsacs"> </a>


|**Среда**|**Префикс конечной точки**|**Конечная точка**|
|:-----|:-----|:-----|
| Рабочая | учетные записи | AccessControl.Windows.NET |
| Германия | для входа | microsoftonline.de |
| Китай | учетные записи | AccessControl.chinacloudapi.CN |
| Правительства США | учетные записи | AccessControl.Windows.NET |

С помощью URL-адрес конечной точки этой модели ACS отформатированное как https:// + конечной точки префикс + / + конечной точки. Поэтому URL-адрес для рабочей среды будет https://accounts.accesscontrol.windows.net, одно для Германии будет https://login.microsoftonline.de.

### <a name="updating-tokenhelpercs-in-your-applications"></a>Обновление tokenhelper.cs в приложениях
<a name="tokenhelperacs"> </a>

При необходимости выполните SharePoint надстройки авторизации с помощью Azure ACS, а затем вы используете `tokenhelper.cs` (или `tokenhelper.vb`). Класс tokenhelper по умолчанию будет иметь жестко ссылки на конечные точки Azure ACS и методы для получения конечной точки службы ACS, как показано ниже:

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.windows.net";

...
```

#### <a name="tokenhelpercs-updates-for-germany"></a>Обновления Tokenhelper.cs для Германии
Обновление статические переменные `GlobalEndPointPrefix` и `AcsHostUrl` к значениям Германия Azure ACS.

```C#
...

private static string GlobalEndPointPrefix = "login";
private static string AcsHostUrl = "microsoftonline.de";

...
```

#### <a name="tokenhelpercs-updates-for-china"></a>Обновления Tokenhelper.cs для Китая
Обновление статические переменные `GlobalEndPointPrefix` и `AcsHostUrl` для Китая Azure ACS значений:

```C#
...

private static string GlobalEndPointPrefix = "accounts";
private static string AcsHostUrl = "accesscontrol.chinacloudapi.cn";

...
```

### <a name="using-pnp-to-authorize-your-add-in-using-azure-acs"></a>С помощью PnP для авторизации надстройки с помощью Azure ACS
<a name="pnpacs"> </a>

PnP [помощью класса AuthenticationManager](https://github.com/SharePoint/PnP-Sites-Core/blob/dev/Core/OfficeDevPnP.Core/AuthenticationManager.cs) предлагает простой способ получить объект SharePoint ClientContext при работе с Azure ACS для авторизации. Затронутые методы были расширены с помощью дополнительного `AzureEnvironment` enum

```c#
/// <summary>
/// Enum to identify the supported Office 365 hosting environments
/// </summary>
public enum AzureEnvironment
{
    Production=0,
    PPE=1,
    China=2,
    Germany=3,
    USGovernment=4
}
```

Ниже фрагменте показано только приложения на авторизации, обратите внимание на то последним параметром в `GetAppOnlyAuthenticatedContext` метод:
```c#
string siteUrl = "https://contoso.sharepoint.de/sites/test";
string acsAppId = "955c10f2-7072-47f8-8bc1-xxxxx"; 
string acsAppSecret = "jgTolmGXU9DW8hUKgletoxxxxx"; 
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext(siteUrl, acsAppId, 
                acsAppSecret, AzureEnvironment.Germany);
```


### <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Ознакомьтесь с Office 365 Германия](https://support.office.com/en-US/article/Learn-about-Office-365-Germany-8a5a4bbc-667a-4cac-8769-d8ac9015db4c) 
- [Узнайте об Office 365, которой с 21Vianet (Китай)](https://support.office.com/en-us/article/Learn-about-Office-365-operated-by-21Vianet-A8AB5061-3346-4DA0-BB7C-5260822B53AE)