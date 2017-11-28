---
title: "Настройка страницы SharePoint с помощью удаленного подготовки и CSS"
ms.date: 11/03/2017
ms.openlocfilehash: 7287c1d4375f37f1047ab299dbe04f012f0fa297
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="customize-a-sharepoint-page-by-using-remote-provisioning-and-css"></a>Настройка страницы SharePoint с помощью удаленного подготовки и CSS

Использование CSS для настройки SharePoint поля форматированного текста и зоны веб-частей.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Каскадные таблицы стилей (CSS) можно использовать для настройки SharePoint поля форматированного текста и зоны веб-частей. Чтобы настроить поля форматированного текста, это можно сделать это право на странице, которую требуется изменить. Для зоны веб-частей можно использовать веб-часть редактора скрипта для добавления HTML-код или сценарии или связать таблицу стилей CSS.
Пример кода, который связан с этой статьей содержатся в разделе [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) в [Office 365 для разработчиков шаблоны и рекомендации](https://github.com/SharePoint/PnP) на репозиториев.

## <a name="customize-rich-text-fields"></a>Настройка поля форматированного текста
<a name="sectionSection0"> </a>

Поля форматированного текста можно настроить с помощью CSS вправо в редакторе страниц:

1. На странице SharePoint нажмите кнопку **Изменить** , чтобы открыть редактор страниц.
    
2. На ленте выберите команду **Вставить** > **Внедрение кода**.
    
Теперь вы можете добавить или изменить элементы CSS для поля форматированного текста.

## <a name="customize-web-part-zones"></a>Настройка зоны веб-частей
<a name="sectionSection1"> </a>

Настройка зоны веб-частей с помощью CSS, используйте редактор сценариев веб-части. Для получения дополнительных сведений см. [как использовать редактор сценариев веб-части в SharePoint 2013](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx).

**Примечание**  При использовании SharePoint Online и функцию NoScript веб-часть редактора скриптов отключена. 

В следующем примере кода отправляет настраиваемого CSS в библиотеку активов, применяется ссылку на URL-адрес CSS с настраиваемым действием и затем создается настраиваемое действие для построения ссылка на файл CSS.

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.EventReceivers;

namespace AlternateCSSAppAutohostedWeb.Services
{
    public class AppEventReceiver : IRemoteEventService
    {
        public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {
            SPRemoteEventResult result = new SPRemoteEventResult();

            try
            {
                using (ClientContext clientContext = TokenHelper.CreateAppEventClientContext(properties, false))
                {
                    if (clientContext != null)
                    {
                        Web hostWebObj = clientContext.Web;

                        List assetLibrary = hostWebObj.Lists.GetByTitle("Site Assets");
                        clientContext.Load(assetLibrary, l => l.RootFolder);

                        // First, upload the CSS files to the Asset Library.
                        DirectoryInfo themeDir = new DirectoryInfo(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "CSS");
                        foreach (var themeFile in themeDir.EnumerateFiles())
                        {
                            FileCreationInformation newFile = new FileCreationInformation();
                            newFile.Content = System.IO.File.ReadAllBytes(themeFile.FullName);
                            newFile.Url = themeFile.Name;
                            newFile.Overwrite = true;

                            Microsoft.SharePoint.Client.File uploadAsset = assetLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(uploadAsset);
                            break;
                        }
                        
                        string actionName = "SampleCSSLink";

                        // Now, apply a reference to the CSS URL via a custom action.
                        
                        // Clean up existing actions that we may have deployed.
                        var existingActions = hostWebObj.UserCustomActions;
                        clientContext.Load(existingActions);

                        // Run uploads and initialize the existing Actions collection.
                        clientContext.ExecuteQuery();

                        // Clean up existing actions.
                        foreach (var existingAction in existingActions)
                        {
                            if(existingAction.Name.Equals(actionName, StringComparison.InvariantCultureIgnoreCase))
                                existingAction.DeleteObject();
                        }
                        clientContext.ExecuteQuery();

                        // Build a custom action to write a link to your new CSS file.
                        UserCustomAction cssAction = hostWebObj.UserCustomActions.Add();
                        cssAction.Location = "ScriptLink";
                        cssAction.Sequence = 100;
                        cssAction.ScriptBlock = @"document.write('<link rel=""stylesheet"" href=""" + assetLibrary.RootFolder.ServerRelativeUrl + @"/cs-style.css"" />');";
                        cssAction.Name = actionName;
                        
                        // Apply.
                        cssAction.Update();
                        clientContext.ExecuteQuery();
                    }
                    result.Status = SPRemoteEventServiceStatus.Continue;
                    return result;
                }
            }
            catch (Exception ex)
            {
                result.Status = SPRemoteEventServiceStatus.CancelWithError;
                result.ErrorMessage = ex.Message;
                return result;
            }
            
        }

        public void ProcessOneWayEvent(SPRemoteEventProperties properties)
        {
            // This method is not used by app events.
        }
    }
}

```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [Как использовать редактор сценариев веб-части в SharePoint 2013](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx)
    
-  [Класс ScriptEditorWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.webpartpages.scripteditorwebpart.aspx)
