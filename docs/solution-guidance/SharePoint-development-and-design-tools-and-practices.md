---
title: "Средства разработки и проектирования SharePoint и рекомендации"
ms.date: 11/03/2017
ms.openlocfilehash: 155558fb24f4be14919e83b881e70db7950ef26a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="sharepoint-development-and-design-tools-and-practices"></a>Средства разработки и проектирования SharePoint и рекомендации

Средства проектирования и разработки SharePoint можно использовать для применения фирменной символики для сайтов SharePoint.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

В этой статье представлены сведения о параметрах проектирования и разработки, доступных в SharePoint. Кроме того, можно найти сведения об использовании удаленного подготовки шаблон для применения фирменной настройки средств на сайте SharePoint.

## <a name="key-sharepoint-development-and-design-terms-and-concepts"></a>Клавиша SharePoint разработки и проектирования термины и концепции
<a name="sectionSection0"> </a>

|**Концепция или термин**|**Определение**|**Дополнительные сведения**|
|:-----|:-----|:-----|
|Дизайнер|Функциональная возможность, активировано в публикации сайтов или сайтов группы с поддержкой публикации SharePoint, который используется для импорта и управление сайтом фирменной символики активы и экспортировать их в пакете разработки.|Используйте диспетчер структуры для импорта фирменной настройки средств, созданного в другие средства, такие как Adobe PhotoShop или Adobe DreamWeaver в SharePoint.<br/>SharePoint Designer не доступно для использования со службой OneDrive для бизнеса или SharePoint Team сайтов, где публикации не включено.|
|Пакет разработки|Предназначен для использования с помощью сайтов публикации SharePoint 2013, содержит фирменной настройки средств, которые хранятся в диспетчере оформления.| [Пакеты разработки дизайнер SharePoint 2013](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)|
|Удаленный подготовки|Модель, которая включает в себя подготовки сайтов с помощью шаблонов и кода, работающего под управлением SharePoint за пределы организации надстройки размещением у поставщика.| [Веб-сайтов подготовки методик и удаленных подготовки в SharePoint 2013](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)<br/>[Подготовка самостоятельного создания сайтов с использованием приложений в SharePoint 2013](http://blogs.msdn.com/b/richard_dizeregas_blog/archive/2013/04/04/self-service-site-provisioning-using-apps-for-sharepoint-2013.aspx)|
|Корневой веб-узел|Первый веб-сайта в семействе сайтов. Корневого веб-узла иногда называется корня веб-приложения.||
|Изолированные решения|WSP-файлов, содержащих сборки, других компонентов не компилируются и XML-файл манифеста. Изолированные решения с помощью кода с частичным доверием.| [Изолированные решения](https://msdn.microsoft.com/en-us/library/ff798382.aspx)|
|SharePoint Designer 2013|HTML-код конструктора и разработки средства управления средством управления фирменной настройки элементов в SharePoint. В SharePoint 2013 SharePoint Designer главным образом поддерживает настраиваемых рабочих процессов.| [Изменения в SharePoint Designer 2013?](https://msdn.microsoft.com/en-us/library/office/jj728659.aspx)<br/>[Новые возможности разработки сайтов SharePoint 2013?](https://msdn.microsoft.com/en-us/library/office/jj163942.aspx)|
|WSP-файла|Файл решения SharePoint. WSP-файл находится в CAB-файле, относящие ресурсах сайта и упорядочивает их с помощью файла manifest.xml.| [Обзор решений](https://msdn.microsoft.com/en-us/library/office/aa543214%28v=office.14%29.aspx)|

## <a name="development-options"></a>Параметры разработки
<a name="sectionSection1"> </a>

При использовании SharePoint 2013 в качестве платформы разработки, вам потребуются для создания среды для разработки, тестирования, построения и развертывания контента. Сведения о параметрах для разработки см в статье [Управление жизненным циклом приложений SharePoint Server 2013](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx) [аспекты среды разработки](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx#DevEnvironment) . В таблице 2 приведены сведения о выполнении для различных вариантов разработки. 

**Параметры для разработки SharePoint, тестирования и приемки**

|**Вариант**|**Сведения о выполнении**|
|:-----|:-----|
|Сервера Team foundation server|-Находится в Visual Studio Online для быстрого доступа.<br/>-Включает в себя систему централизованного исходного кода и жизненного цикла управления.|
|Облако сред тестирования и приемки|-Используйте отдельные клиента для приемочного тестирования.<br/>-Отдельные тестовой среды для локальной проверки.|
|Локальные среды тестирования и приемки|-Используется для локального развертывания SharePoint.<br/>-Hosted клиента в локальной или в Microsoft Azure.|
 
В большинстве случаев потребуется по крайней мере следующие клиенты, однако может изменяться в зависимости от требований.

-  **Клиент разработчика**. Рекомендуется подготовки и использования сайта разработчика. Таким образом, чтобы избежать совместное использование данных в рабочей среде. Для регистрации и Подготовка сайта разработчика, видеть [Подписка на сайте разработчика Office 365](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx#o365_signup) в статье [Подписка на подписку разработчика Office 365 и настройте свои инструменты и среду](http://msdn.microsoft.com/library/b22ce52a-ae9e-4831-9b68-c9210af6dc54.aspx).
    
-  **Интеграция и тестирование клиента**. Используйте этот сайт для убедитесь в том, что новые приложения и функциональные возможности работы через более одного семейства веб-сайтов и от служб и данных в рабочей среде. Настройка среды для включения возможности, доступные в режиме предварительного просмотра. (Для этого в консоль администрирования клиента, выберите **Параметры службы**и выберите в разделе параметра **обновление** **Первого выпуска**.) Интернет-версия Visual Studio можно использовать для запуска автоматического тестирования и любые другие тестирование непрерывной интеграции.
    
-  **Рабочий клиент**. Выпуск проверен, обслуживаемые и утвержденных приложений для клиента. На этом клиента для разработки и тестирования приложений, которые находятся небольшие в область или обнаружили воздействия можно создать на сайте разработчика. Следует Избегайте, совместное использование вашей разработки и рабочей среды.
    
## <a name="design-tools"></a>Средства разработки
<a name="sectionSection2"> </a>

Используйте стандартные средства веб-проектирования и разработки, таких как HTML, изображений, CSS-файлы и файлы JavaScript для создания сайта SharePoint, фирменная символика активов. Например Adobe DreamWeaver и Adobe PhotoShop можно использовать для разработки HTML, CSS, JavaScript и файлы изображений, которые будут использоваться для фирменной символики на сайтах SharePoint. Кроме того можно использовать SharePoint Designer 2013 для создания, управления и Настройка фирменной настройки средств или создание настраиваемых решений в Visual Studio 2013.

### <a name="sharepoint-design-packages-and-wsp-files"></a>Пакеты разработки SharePoint и WSP-файлов

Пакеты разработки — WSP-файлы, созданные с дизайнер, соответствующие правилам прогнозируемый для упаковки средств разработки. Это, по сути, изолированных решений. Если вы используете еще одно средство, пакет фирменной символики активами в WSP-файл, фирменной настройки средств будет находиться в состоянии менее основных и предсказуемым.

Пакет разработки включает все файлы, которые были настроены. Например при создании макета страницы, которая использует пользовательский тип содержимого, пакет разработки включает макет страницы, настраиваемого типа контента, которые он использует и все настраиваемые столбцы сайта. Пакет разработки также включает несколько файлов, связанных с вариантов оформления, примененные к сайту SharePoint, включая файлы, загруженные в следующих местоположениях:

- Библиотеки материалы сайта
    
- Библиотека стилей
    
- Коллекция главных страниц
    
Если вариантов оформления применяется к сайту, перед применением настраиваемый фирменный стиль, пакет разработки будут включены файлы с расширениями .themedcss и .themedpng. Для применения фирменной настройки средств в пакете разработки на сайте SharePoint, Экспорт пакета проектирования и использование удаленного подготовки шаблон для применения содержимое пакета конструктора.

SharePoint 2013 включает в себя API-интерфейсы, которые можно использовать для работы с помощью конструктора пакетов. Если вы используете SSOM, CSOM или JSOM, можно использовать классы [DesignPackage](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.aspx) или [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) .

#### <a name="using-the-design-package-csom-to-apply-the-contents-of-design-packages-to-a-sharepoint-site"></a>С помощью пакета проектирования CSOM для применения содержимое пакетов проекта на сайте SharePoint

Следующем примере показано, как использовать API пакета проектирования в шаблоне удаленного подготовки для применения содержимое пакетов проекта на сайте SharePoint.

Этот код был разработан для использования с сайтами публикации. Несмотря на то, что можно использовать API пакетов разработки для применения фирменной символики для сайтов групп, которые имеют публикации функция включена, это может вызвать проблемы долгосрочного поддержки.

**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```
using Microsoft.SharePoint.Client;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.SharePoint.Client.Publishing;
namespace ProviderSharePointAppWeb
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_PreInit(object sender, EventArgs e)
        {
            Uri redirectUrl;
            switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
            {
                case RedirectionStatus.Ok:
                    return;
                case RedirectionStatus.ShouldRedirect:
                    Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                    break;
                case RedirectionStatus.CanNotRedirect:
                    Response.Write("An error occurred while processing your request.");
                    Response.End();
                    break;
            }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            // Use TokenHelper to get the client context and Title property.
            // To access other properties, the add-in might need to request permissions
            // on the host web.
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            
            // Publishing feature GUID to use the infrastructure for publishing. 
            Guid PublishingFeature = Guid.Parse("f6924d36-2fa8-4f0b-b16d-06b7250180fa");

            // The site-relative URL of the design package to install.
            // This sandbox design package should be uploaded to a document library.
            // For practical purposes, this can be a configuration setting in web.config.
            string fileRelativePath = @"/sites/devsite/brand/Dev.wsp";

            //string fileUrl = @"https://SPXXXXX.com/sites/devsite/brand/Dev.wsp";
            
        
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Load the site context explicitly or while installing the API, the path for
// the package will not be resolved.
                // If the package cannot be found, an exception is thrown. 
                var site = clientContext.Site;
                clientContext.Load(site);
                clientContext.ExecuteQuery();
              
                // Validate whether the Publishing feature is active. 
                if (IsSiteFeatureActivated(clientContext,PublishingFeature))
                {
                    DesignPackageInfo info = new DesignPackageInfo()
                    {
                        PackageGuid = Guid.Empty,
                        MajorVersion = 1,
                        MinorVersion = 1,
                        PackageName = "Dev"
                    };
                    Console.WriteLine("Installing design package ");
                    
                    DesignPackage.Install(clientContext, clientContext.Site, info, fileRelativePath);
                    clientContext.ExecuteQuery();

                    Console.WriteLine("Applying design package");
                    DesignPackage.Apply(clientContext, clientContext.Site, info);
                    clientContext.ExecuteQuery();
                }
            }
        }
        public  bool IsSiteFeatureActivated( ClientContext context, Guid guid)
        {
            var features = context.Site.Features;
            context.Load(features);
            context.ExecuteQuery();

            foreach (var f in features)
            {
                if (f.DefinitionId.Equals(guid))
                    return true;
            }
            return false;
        }
 
    }
}
```

#### <a name="using-filecreationinformation-to-upload-branding-assets-and-a-master-page-to-a-team-site"></a>С помощью FileCreationInformation Отправка фирменной настройки активов и Главная страница сайта группы

Установка и удаление конструктора пакетов и экспорт конструктора пакетов в сайты SharePoint Online, можно использовать функциональные возможности SharePoint 2013 CSOM. Например используйте [SP. Метод Publishing.DesignPackage.install (sp.publishing)](http://msdn.microsoft.com/library/26500127-210f-6c52-c0de-cf2894939a91.aspx) для установки пакета разработки на сайте, как показано в следующем примере.

```
public static void Install(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info,
        string path
)
```

Класс [DesignPackageInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.publishing.designpackageinfo.aspx) указывает метаданные, которые описывают содержимое пакета проектирования для установки. Метод [Uninstall](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.uninstall.aspx) для удаления пакета конструктора с сайта, как показано в следующем примере.

```
public static void UnInstall(
        ClientRuntimeContext context,
        Site site,
        DesignPackageInfo info
)
```

Если вам потребуется фирменной символики сайта группы с публикацией в функциях включено, или публикации на сайт, на SharePoint Online, можно использовать метод [ExportSmallBusiness](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportsmallbusiness.aspx) или [ExportEnterprise](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.designpackage.exportenterprise.aspx) экспорт пакетов разработки для шаблонов сайтов в решение Коллекция. Использование метода **ExportSmallBusiness** с шаблона сайта для малого бизнеса и используйте метод **ExportEnterprise** для всех шаблонов сайта, как показано в следующем примере. В примере thatpackageName Примечание — это строка, представляющая имя пакета конструктора.

```
public static ClientResult<DesignPackageInfo> ExportEnterprise(
        ClientRuntimeContext context,
        Site site,
        bool includeSearchConfiguration
)
```

При использовании этого метода можно включить конфигурацию поиска в пакете разработки, как показано в следующем примере. Обратите внимание на то, что все методы пакета проектирования работают на уровне семейства веб-сайтов.

```
public static ClientResult<DesignPackageInfo> ExportSmallBusiness(
        ClientRuntimeContext context,
        Site site,
        string packageName,
        bool includeSearchConfiguration
)
```

## <a name="design-tool-options-for-sharepoint-online"></a>Параметры средства разработки для SharePoint Online
<a name="sectionSection3"> </a>

Средства, которые можно использовать для фирменной символики сайта SharePoint Online зависят от SharePoint Online edition и тип сайта, который требуется построить. Выпуск для малого бизнеса, например, включает одного сайта рабочих групп и один общедоступный сайт. Не включает публикации сайта. Можно использовать надстройки построитель сайта в SharePoint Online для настройки общедоступного сайта фирменной символики.

Enterprise edition включает в себя семейства сайтов групп в корневой веб-приложение для домена, который не включает публикации. Он не включает общедоступный сайт. Управление SharePoint с помощью конструктора диспетчера фирменной настройки элементами сайтов для публикации сайта в SharePoint Online Enterprise edition.

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
-  [Управление жизненным циклом приложений SharePoint Server 2013](http://msdn.microsoft.com/library/caaf9a09-2e6a-49e3-a8d6-aaf7f93a842a.aspx)
    
-  [Изолированные решения](https://msdn.microsoft.com/en-us/library/ff798382.aspx)
    
-  [Веб-сайтов подготовки методик и удаленных подготовки в SharePoint 2013](http://blogs.msdn.com/b/vesku/archive/2013/08/23/site-provisioning-techniques-and-remote-provisioning-in-sharepoint-2013.aspx)
    
-  [Пакеты разработки дизайнер SharePoint 2013](http://msdn.microsoft.com/library/85ad1993-4d75-4806-9097-b934865a899a.aspx)
