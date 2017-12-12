---
title: "Настройка страницы SharePoint с помощью удаленного подготовки и CSS"
ms.date: 11/03/2017
ms.openlocfilehash: 6cf2eb2044af5a8659e19fea94e009824e7ec9d2
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="customize-a-sharepoint-page-by-using-remote-provisioning-and-css"></a><span data-ttu-id="35b7e-102">Настройка страницы SharePoint с помощью удаленного подготовки и CSS</span><span class="sxs-lookup"><span data-stu-id="35b7e-102">Customize a SharePoint page by using remote provisioning and CSS</span></span>

<span data-ttu-id="35b7e-103">Использование CSS для настройки SharePoint поля форматированного текста и зоны веб-частей.</span><span class="sxs-lookup"><span data-stu-id="35b7e-103">Use CSS to customize SharePoint rich text fields and Web Part Zones.</span></span>

<span data-ttu-id="35b7e-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="35b7e-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="35b7e-105">Каскадные таблицы стилей (CSS) можно использовать для настройки SharePoint поля форматированного текста и зоны веб-частей.</span><span class="sxs-lookup"><span data-stu-id="35b7e-105">You can use cascading style sheets (CSS) to customize SharePoint rich text fields and Web Part Zones.</span></span> <span data-ttu-id="35b7e-106">Чтобы настроить поля форматированного текста, это можно сделать это право на странице, которую требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="35b7e-106">To customize rich text fields, you can do this right in the page you're editing.</span></span> <span data-ttu-id="35b7e-107">Для зоны веб-частей можно использовать веб-часть редактора скрипта для добавления HTML-код или сценарии или связать таблицу стилей CSS.</span><span class="sxs-lookup"><span data-stu-id="35b7e-107">For Web Part Zones, you can use the Script Editor Web Part to add HTML or scripts, or associate a CSS style sheet.</span></span>
<span data-ttu-id="35b7e-108">Пример кода, который связан с этой статьей содержатся в разделе [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) в [Office 365 для разработчиков шаблоны и рекомендации](https://github.com/SharePoint/PnP) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="35b7e-108">For a code sample that is associated with this article, see  [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) in [Office 365 Developer Patterns and Practices](https://github.com/SharePoint/PnP) on GitHub.</span></span>

## <a name="customize-rich-text-fields"></a><span data-ttu-id="35b7e-109">Настройка поля форматированного текста</span><span class="sxs-lookup"><span data-stu-id="35b7e-109">Customize rich text fields</span></span>
<span data-ttu-id="35b7e-110"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="35b7e-110"></span></span>

<span data-ttu-id="35b7e-111">Поля форматированного текста можно настроить с помощью CSS вправо в редакторе страниц:</span><span class="sxs-lookup"><span data-stu-id="35b7e-111">You can customize rich text fields by using CSS right in the page editor:</span></span>

1. <span data-ttu-id="35b7e-112">На странице SharePoint нажмите кнопку **Изменить** , чтобы открыть редактор страниц.</span><span class="sxs-lookup"><span data-stu-id="35b7e-112">In your SharePoint page, choose  **Edit** to open the page editor.</span></span>
    
2. <span data-ttu-id="35b7e-113">На ленте выберите команду **Вставить** > **Внедрение кода**.</span><span class="sxs-lookup"><span data-stu-id="35b7e-113">From the ribbon, choose  **Insert** > **Embed Code**.</span></span>
    
<span data-ttu-id="35b7e-114">Теперь вы можете добавить или изменить элементы CSS для поля форматированного текста.</span><span class="sxs-lookup"><span data-stu-id="35b7e-114">You can now add or modify CSS elements for a rich text field.</span></span>

## <a name="customize-web-part-zones"></a><span data-ttu-id="35b7e-115">Настройка зоны веб-частей</span><span class="sxs-lookup"><span data-stu-id="35b7e-115">Customize Web Part Zones</span></span>
<span data-ttu-id="35b7e-116"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="35b7e-116"></span></span>

<span data-ttu-id="35b7e-117">Настройка зоны веб-частей с помощью CSS, используйте редактор сценариев веб-части.</span><span class="sxs-lookup"><span data-stu-id="35b7e-117">To customize Web Part Zones by using CSS, you use the Script Editor Web Part.</span></span> <span data-ttu-id="35b7e-118">Для получения дополнительных сведений см. [как использовать редактор сценариев веб-части в SharePoint 2013](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx).</span><span class="sxs-lookup"><span data-stu-id="35b7e-118">For more information, see  [How to Use the Script Editor Web Part in SharePoint 2013](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx).</span></span>

> [!NOTE] 
> <span data-ttu-id="35b7e-119">При использовании SharePoint Online и функцию NoScript веб-часть редактора скриптов отключена.</span><span class="sxs-lookup"><span data-stu-id="35b7e-119">If you are using SharePoint Online and the NoScript feature, the Script Editor Web Part is disabled.</span></span> 

<span data-ttu-id="35b7e-120">В следующем примере кода отправляет настраиваемого CSS в библиотеку активов, применяется ссылку на URL-адрес CSS с настраиваемым действием и затем создается настраиваемое действие для построения ссылка на файл CSS.</span><span class="sxs-lookup"><span data-stu-id="35b7e-120">The following code example uploads custom CSS to the Asset Library, applies a reference to the CSS URL with a custom action, and then creates a custom action to build a link to the new CSS file.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="35b7e-121">См. также</span><span class="sxs-lookup"><span data-stu-id="35b7e-121">See also</span></span>
<span data-ttu-id="35b7e-122"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="35b7e-122"></span></span>

-  [<span data-ttu-id="35b7e-123">Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="35b7e-123">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="35b7e-124">Как использовать редактор сценариев веб-части в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="35b7e-124">How to Use the Script Editor Web Part in SharePoint 2013</span></span>](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx)
    
-  [<span data-ttu-id="35b7e-125">Класс ScriptEditorWebPart</span><span class="sxs-lookup"><span data-stu-id="35b7e-125">ScriptEditorWebPart class</span></span>](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.webpartpages.scripteditorwebpart.aspx)
