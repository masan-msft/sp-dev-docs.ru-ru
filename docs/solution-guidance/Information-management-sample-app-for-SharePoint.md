---
title: "Сведения о управления пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c5e81e55cff89d6bf311c3fb6c7f40e0b0c87ee9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="information-management-sample-add-in-for-sharepoint"></a>Сведения о управления пример надстройки для SharePoint
В рамках стратегии Enterprise Content Management (ECM) можно получить или задать политики сайта для управления жизненным циклом сайта SharePoint.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Пример [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) показано, как использовать ASP.NET размещением у поставщика SharePoint надстройке для получения и задания политики сайта для сайта. Если вы хотите используйте этого решения:

- Применение настроек политики настраиваемой процедуры подготовки сайта. 
    
- Создание новой или изменение существующей политики сайта.
    
- Создайте Настраиваемая формула истечения действия. 
    
## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.InformationManagement](https://github.com/SharePoint/PnP/tree/master/Samples/Core.InformationManagement) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Мы рекомендуем создать политику по крайней мере один сайт и назначьте его на свой сайт перед запуском этой надстройки. В противном случае надстройка будет запущен без отображения образца данных. Для получения дополнительных сведений см [Обзор политик сайта в SharePoint 2013](http://technet.microsoft.com/en-US/library/jj219569%28v=office.15%29.aspx).

## <a name="using-the-coreinformationmanagement-sample-app"></a>Использование примера приложения Core.InformationManagement
<a name="sectionSection1"> </a>

При запуске приложения на начальной странице отображаются следующие сведения, как показано на рисунке 1:

- Сайт закрытия даты окончания срока действия. Эти даты относятся к сайту и основаны на параметрах конфигурации применяемой политики сайта.
    
- Все политики сайта, которые можно применять к сайту.
    
- В настоящее время применяемой политики сайта.
    
- Поле для выбора и применение новой политики сайта к сайту.

**На рисунке 1. Надстройка начальная страница управления сведения**

![Снимок экрана с помощью надстройки в начало страницы, с помощью значения закрытия и срока действия политики сайта, политики доступны и применяемые сайта и другие политики, применяемые выделенными.](media/8c5f39f7-700d-4300-bcc4-9ed9edf0e155.png)

Из сайта SharePoint, можно перейти к приложения, который выполняется на удаленном узле, выбрав **последние** > **Core.InformationManagement**. Чтобы вернуться на сайт SharePoint, выберите **сайта**.

Файл Pages\Default.aspx.cs в проекте Core.InformationManagementWeb содержит код для страницы, отображаемой на рисунке 1. 

Следующий код в метод **Page_Load** страницы Default.aspx.cs извлекает и отображает даты закрытия и истечение срока действия сайта, на основе политики применен сайта. Этот код вызывает методы расширения **GetSiteExpirationDate** и **GetSiteCloseDate** OfficeDevPnP.Core проекта.
    
> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
// Get site expiration and closure dates.
if (cc.Web.HasSitePolicyApplied())
{
        lblSiteExpiration.Text = String.Format("The expiration date for the site is {0}", cc.Web.GetSiteExpirationDate());
        lblSiteClosure.Text = String.Format("The closure date for the site is {0}", cc.Web.GetSiteCloseDate());
}

```

Следующий код в метод **Page_Load** страницы Default.aspx.cs имена всех политик сайтов, которые применимы к сайту (в том числе политики в настоящее время примененных сайта). Этот код вызывает метод расширения **GetSitePolicies** OfficeDevPnP.Core проекта.

```C#
// List the defined policies.
List<SitePolicyEntity> policies = cc.Web.GetSitePolicies();
string policiesString = "";
foreach (var policy in policies)
                    {
                        policiesString += String.Format("{0} ({1}) <BR />", policy.Name, policy.Description);
                    }
lblSitePolicies.Text = policiesString;
            };

```

Следующий код в метод **Page_Load** страницы Default.aspx.cs имя политики сайта, в настоящее время применяется к сайту. Это вызывает метод расширения **GetAppliedSitePolicy** OfficeDevPnP.Core проекта.

```C#
// Show the assigned policy.
SitePolicyEntity appliedPolicy = cc.Web.GetAppliedSitePolicy();
if (appliedPolicy != null)
            {
            lblAppliedPolicy.Text = String.Format("{0} ({1})", appliedPolicy.Name, appliedPolicy.Description);
            }
else
            {
            lblAppliedPolicy.Text = "No policy has been applied";
            }

```

Следующий код в метод **Page_Load** страницы Default.aspx.cs заполняет раскрывающегося списка с помощью политики сайта, которые доступны, за исключением политики сайта, назначенном на сайт.

```C#
// Fill the policies combo.
foreach (var policy in policies)
{
if (appliedPolicy == null || !policy.Name.Equals(appliedPolicy.Name, StringComparison.InvariantCultureIgnoreCase))
{
                            drlPolicies.Items.Add(policy.Name);
           }
}
btnApplyPolicy.Enabled = drlPolicies.Items.Count > 0;

```

Следующий код в файле Default.aspx.cs страницы применяется политика выбранного сайта на сайт. Политики в исходный сайт заменяется новой политики сайта. 

```C#
protected void btnApplyPolicy_Click(object sender, EventArgs e)
{
if (drlPolicies.SelectedItem != null)
            {
                cc.Web.ApplySitePolicy(drlPolicies.SelectedItem.Text);
                Page.Response.Redirect(Page.Request.Url.ToString(), true);
            }
}

```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Пример OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
    
-  [Пример Core.SiteClassification](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SiteClassification)
    
-  [ECM. Пример приложения AutoTagging](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.AutoTagging)
    
-  [ECM. Пример приложения DocumentLibraries](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
    
-  [ECM. Пример приложения RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement)
