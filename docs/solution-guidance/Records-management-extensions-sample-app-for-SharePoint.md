---
title: "Расширения управления записями пример приложения для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 34184d4f1b7f2c75c7167d86cc1cf90e1a40323e
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="records-management-extensions-sample-app-for-sharepoint"></a><span data-ttu-id="20a27-102">Расширения управления записями пример приложения для SharePoint</span><span class="sxs-lookup"><span data-stu-id="20a27-102">Records management extensions sample app for SharePoint</span></span>

<span data-ttu-id="20a27-103">В рамках стратегии Enterprise Content Management (ECM) можно включить и изменить параметры управления записями на месте на сайтах SharePoint и списков.</span><span class="sxs-lookup"><span data-stu-id="20a27-103">As part of your Enterprise Content Management (ECM) strategy, you can enable and change in-place records management settings on your SharePoint sites and lists.</span></span>

<span data-ttu-id="20a27-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="20a27-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="20a27-105">[ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) примере показано, как использовать приложения SharePoint с размещением у поставщика для управления параметрами управления записями на месте для сайта или списка.</span><span class="sxs-lookup"><span data-stu-id="20a27-105">The [ECM.RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) sample shows you how to use a provider-hosted SharePoint app to control the in-place records management settings for a site or list.</span></span>    

<span data-ttu-id="20a27-106">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="20a27-106">Use this solution if you want to:</span></span>

- <span data-ttu-id="20a27-107">Настройка параметров управления записями на месте во время настраиваемой процедуры подготовки сайта.</span><span class="sxs-lookup"><span data-stu-id="20a27-107">Configure in-place records management settings during your custom site provisioning process.</span></span>
 
## <a name="before-you-begin"></a><span data-ttu-id="20a27-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="20a27-108">Before you begin</span></span>
<span data-ttu-id="20a27-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="20a27-109"></span></span>

<span data-ttu-id="20a27-110">Чтобы начать работу, загрузите [ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) пример приложения из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="20a27-110">To get started, download the  [ECM.RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) sample app from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="20a27-111">Перед запуском этого приложения:</span><span class="sxs-lookup"><span data-stu-id="20a27-111">Before you run this app:</span></span>

- <span data-ttu-id="20a27-112">Активация компонента управления записями на месте в коллекции веб-сайтов, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="20a27-112">Activate the In-Place Records Management feature on the site collection, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="20a27-113">**На рисунке 1. Активация управления записями на месте в семействе веб-сайтов**</span><span class="sxs-lookup"><span data-stu-id="20a27-113">**Figure 1. Activating In-Place Records Management on your site collection**</span></span>

    ![Снимок экрана, на странице возможности семейства веб-сайтов с помощью активированные функции управления записи на месте с выделением.](media/d99269ae-b8fc-445b-a1b8-1612b16dcba6.png)

- <span data-ttu-id="20a27-115">В параметрах сайта убедитесь, что отображаются **Параметры объявление записи** в **Администрирование семейства веб-сайтов**, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="20a27-115">In site settings, verify that you see  **Record declaration settings** in **Site Collection Administration**, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="20a27-116">**На рисунке 2. Параметры объявления записей в настройках сайта**</span><span class="sxs-lookup"><span data-stu-id="20a27-116">**Figure 2. Record declaration settings in Site Settings**</span></span>

    ![Снимок экрана на странице Параметры сайта с параметрами объявление записи с выделением.](media/13a6a490-68cd-4f70-8714-cd6222325890.png)

## <a name="using-the-ecmrecordsmanagement-sample-app"></a><span data-ttu-id="20a27-118">С помощью ECM. Пример приложения RecordsManagement</span><span class="sxs-lookup"><span data-stu-id="20a27-118">Using the ECM.RecordsManagement sample app</span></span>
<span data-ttu-id="20a27-119"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="20a27-119"></span></span>

 <span data-ttu-id="20a27-120">При запуске приложения, начальная страница отображает два сценария, которые доступны:</span><span class="sxs-lookup"><span data-stu-id="20a27-120">When you start the app, the start page displays the two scenarios that are available:</span></span>

- <span data-ttu-id="20a27-121">Включение управления записями на месте для сайтов</span><span class="sxs-lookup"><span data-stu-id="20a27-121">Enabling in-place records management for sites</span></span>
    
- <span data-ttu-id="20a27-122">Включение управления записями на месте для списков</span><span class="sxs-lookup"><span data-stu-id="20a27-122">Enabling in-place records management for lists</span></span>

<span data-ttu-id="20a27-123">**На рисунке 3. ECM. Начальная страница приложения RecordsManagement**</span><span class="sxs-lookup"><span data-stu-id="20a27-123">**Figure 3. ECM.RecordsManagement app start page**</span></span>

![Снимок экрана приложения начальная страница, отображается в двух сценариях.](media/a5fb2d86-2365-4d39-b41e-29719ab88287.png) 

<span data-ttu-id="20a27-125">Сценарий 1 можно использовать для создания пользовательского интерфейса для управления параметрами управления записями на семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="20a27-125">You can use scenario 1 to build a UI to control the records management settings on your site collection.</span></span> <span data-ttu-id="20a27-126">Пользовательский Интерфейс в этом приложении похож на пользовательский Интерфейс, обнаруженных в **Параметры объявления записей** в **Настройках сайта** (см).</span><span class="sxs-lookup"><span data-stu-id="20a27-126">The UI in this app is similar to the UI found in **Records declaration settings** in **Site Settings** (see Figure 2).</span></span> <span data-ttu-id="20a27-127">Также можно активировать или деактивировать компонент управления записями на месте в семействе веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="20a27-127">You can also activate or deactivate the In-Place Records Management feature on your site collection.</span></span>

<span data-ttu-id="20a27-128">Сценарий 2 можно использовать для создания пользовательского интерфейса для управления параметрами управления записями на списки.</span><span class="sxs-lookup"><span data-stu-id="20a27-128">You can use Scenario 2 to build a UI to control the records management settings on lists.</span></span> <span data-ttu-id="20a27-129">Пользовательский Интерфейс в этом приложении похож на пользовательский Интерфейс, обнаруженных в **параметрах объявления записей** в параметры библиотеки в список.</span><span class="sxs-lookup"><span data-stu-id="20a27-129">The UI in this app is similar to the UI found in  **Records declaration settings** in the library settings on your list.</span></span>

<span data-ttu-id="20a27-130">**На рисунке 4. Объявление параметров записи в списке.**</span><span class="sxs-lookup"><span data-stu-id="20a27-130">**Figure 4. Record declaration settings on a list**</span></span>

![Снимок экрана на странице Параметры объявления записей библиотеки.](media/2522e4b0-5d5c-40bc-829d-f13d96a2b233.png)
### <a name="scenaro-1"></a><span data-ttu-id="20a27-132">Scenaro 1</span><span class="sxs-lookup"><span data-stu-id="20a27-132">Scenaro 1</span></span>

<span data-ttu-id="20a27-133">Сценарий 1 решает функций управления записями на месте и параметров для сайтов.</span><span class="sxs-lookup"><span data-stu-id="20a27-133">Scenario 1 addresses in-place records management features and settings for sites.</span></span> <span data-ttu-id="20a27-134">Пользовательский Интерфейс приложения отображается кнопка **Деактивировать** (или **активировать**), как показано на рисунке 5.</span><span class="sxs-lookup"><span data-stu-id="20a27-134">The app UI includes a  **Deactivate** (or **Activate**) button, as shown in Figure 5.</span></span> <span data-ttu-id="20a27-135">Выбрав эту кнопку деактивирует (или активирует) компонента управления записями на месте в коллекции веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="20a27-135">Choosing this button deactivates (or activates) the In-Place Records Management feature on the site collection.</span></span> 

<span data-ttu-id="20a27-136">**На рисунке 5. Отключение кнопки для функции управления записями на месте**</span><span class="sxs-lookup"><span data-stu-id="20a27-136">**Figure 5. Deactivate button for the In-Place Records Management feature**</span></span>

![Снимок экрана, которая отображает деактивировать и активировать кнопку для управления записями на месте.](media/b1a29cad-4239-4f49-a3e8-ca4e8ca99667.png)

<span data-ttu-id="20a27-138">Приведенный ниже код активирует или деактивирует компонента управления записями на месте в коллекции веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="20a27-138">The following code activates or deactivates the In-Place Records Management feature on the site collection.</span></span> <span data-ttu-id="20a27-139">Методы **DisableInPlaceRecordsManagementFeature** и **EnableSiteForInPlaceRecordsManagement** являются частью файла AppModelExtensions\RecordsManagementExtensions.cs в [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span><span class="sxs-lookup"><span data-stu-id="20a27-139">The  **DisableInPlaceRecordsManagementFeature** and **EnableSiteForInPlaceRecordsManagement** methods are part of the AppModelExtensions\RecordsManagementExtensions.cs file in the [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span></span>
    
<span data-ttu-id="20a27-140">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="20a27-140">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
protected void btnToggleIPRStatus_Click(object sender, EventArgs e)
        {
            if (cc.Site.IsInPlaceRecordsManagementActive())
            {
                cc.Site.DisableInPlaceRecordsManagementFeature();
                IPRStatusUpdate(false);
            }
            else
            {
                cc.Site.EnableSiteForInPlaceRecordsManagement();
                IPRStatusUpdate(true);
            }
        }
```

<span data-ttu-id="20a27-141">OfficeDevPnP.Core включает в себя методы расширения для получения и задания параметров управления записями на месте всех веб сайтов.</span><span class="sxs-lookup"><span data-stu-id="20a27-141">OfficeDevPnP.Core includes extension methods to get and set all site-scoped in-place records management settings.</span></span> <span data-ttu-id="20a27-142">Следующий код в метод **EnableSiteForInPlaceRecordsManagement** показано, как использовать эти методы для установки ограничений и укажите пользователей, которые можно объявить или отменить объявление записи на вашем сайте.</span><span class="sxs-lookup"><span data-stu-id="20a27-142">The following code from the  **EnableSiteForInPlaceRecordsManagement** method shows how to use these extension methods to set restrictions, and specify who can declare or undeclare records on your site.</span></span>

```C#
public static void EnableSiteForInPlaceRecordsManagement(this Site site)
        {
            // Activate the In-Place Records Management feature if not yet enabled.
            if (!site.IsFeatureActive(new Guid(INPLACE_RECORDS_MANAGEMENT_FEATURE_ID)))
            {
                // Note: this also sets the ECM_SITE_RECORD_RESTRICTIONS value to "BlockDelete, BlockEdit".
                site.ActivateInPlaceRecordsManagementFeature();
            }

            // Enable in-place records management in all locations.
            site.SetManualRecordDeclarationInAllLocations(true);

            // Set restrictions to default values after enablement (this is also done at feature activation).
            EcmSiteRecordRestrictions restrictions = EcmSiteRecordRestrictions.BlockDelete | EcmSiteRecordRestrictions.BlockEdit;
            site.SetRecordRestrictions(restrictions);

            // Set record declaration to default value.
            site.SetRecordDeclarationBy(EcmRecordDeclarationBy.AllListContributors);

            // Set record undeclaration to default value.
            site.SetRecordUnDeclarationBy(EcmRecordDeclarationBy.OnlyAdmins);

        }
```

<span data-ttu-id="20a27-143">Когда пользователь изменяет свои параметры управления записями на месте и выбирает кнопки **Сохранить изменения** , выполняется следующий код в метод **btnSaveSiteScopedIPRSettings_Click** .</span><span class="sxs-lookup"><span data-stu-id="20a27-143">When the user changes their in-place records management settings and chooses the  **Save changes** button, the following code in the **btnSaveSiteScopedIPRSettings_Click** method runs.</span></span>

```C#
protected void btnSaveSiteScopedIPRSettings_Click(object sender, EventArgs e)
        {
            EcmSiteRecordRestrictions restrictions = (EcmSiteRecordRestrictions)Convert.ToInt32(rdRestrictions.SelectedValue);
            cc.Site.SetRecordRestrictions(restrictions);
            cc.Site.SetManualRecordDeclarationInAllLocations(Convert.ToBoolean(rdAvailability.SelectedValue));
            EcmRecordDeclarationBy declareBy = (EcmRecordDeclarationBy)Convert.ToInt32(rdDeclarationBy.SelectedValue);
            cc.Site.SetRecordDeclarationBy(declareBy);
            EcmRecordDeclarationBy unDeclareBy = (EcmRecordDeclarationBy)Convert.ToInt32(rdUndeclarationBy.SelectedValue);
            cc.Site.SetRecordUnDeclarationBy(unDeclareBy);
        }
```

<span data-ttu-id="20a27-144">В предыдущем примере кода выполняется вызов метода **SetRecordRestrictions** в RecordsManagementExtensions.cs.</span><span class="sxs-lookup"><span data-stu-id="20a27-144">In the previous code, a call is made to the  **SetRecordRestrictions** method in RecordsManagementExtensions.cs.</span></span> <span data-ttu-id="20a27-145">Метод **SetRecordRestrictions** в следующем примере показано, как для установки ограничений на записи.</span><span class="sxs-lookup"><span data-stu-id="20a27-145">The **SetRecordRestrictions** method in the next example shows how to set restrictions on the records.</span></span>

```C#
public static void SetRecordRestrictions(this Site site, EcmSiteRecordRestrictions restrictions)
        {
            string restrictionsProperty = "";

            if (restrictions.Has(EcmSiteRecordRestrictions.None))
            {
                restrictionsProperty = EcmSiteRecordRestrictions.None.ToString();
            }
            else if (restrictions.Has(EcmSiteRecordRestrictions.BlockEdit))
            {
                // BlockEdit is always used in conjunction with BlockDelete.
                restrictionsProperty = EcmSiteRecordRestrictions.BlockDelete.ToString() + ", " + EcmSiteRecordRestrictions.BlockEdit.ToString();
            }
            else if (restrictions.Has(EcmSiteRecordRestrictions.BlockDelete))
            {
                restrictionsProperty = EcmSiteRecordRestrictions.BlockDelete.ToString();
            }

            // Set property bag entry.
            site.RootWeb.SetPropertyBagValue(ECM_SITE_RECORD_RESTRICTIONS, restrictionsProperty);
        }
```

### <a name="scenario-2"></a><span data-ttu-id="20a27-146">Сценарий 2</span><span class="sxs-lookup"><span data-stu-id="20a27-146">Scenario 2</span></span>

<span data-ttu-id="20a27-147">Сценарий 2 показано, как взаимодействовать с записями на месте параметры управления для списков.</span><span class="sxs-lookup"><span data-stu-id="20a27-147">Scenario 2 shows how to interact with in-place records management settings for lists.</span></span> <span data-ttu-id="20a27-148">При установке приложения, он создает библиотеки документов, называется IPRTest.</span><span class="sxs-lookup"><span data-stu-id="20a27-148">When the app installs, it creates a document library called IPRTest.</span></span> <span data-ttu-id="20a27-149">При использовании этого приложения для изменения и сохранения параметров управления записями на месте, эти изменения применяются к IPRTest.</span><span class="sxs-lookup"><span data-stu-id="20a27-149">When you use this app to change and save the in-place records management settings, the changes are applied to IPRTest.</span></span> 

<span data-ttu-id="20a27-150">**Примечание**  Чтобы использовать параметры управления записями на месте для списка, необходимо активировать компонент управления записями на месте в семействе веб-сайтов, как показано на рисунке 1 ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="20a27-150">**Note**  To use in-place records management settings on a list, you must activate the In-place Records Management feature on your site collection, as shown in Figure 1 earlier in this article.</span></span> 

<span data-ttu-id="20a27-151">Следующий код в файле Default.aspx.cs выполняется, если пользователь выбирает кнопку **Сохранить изменения** .</span><span class="sxs-lookup"><span data-stu-id="20a27-151">The following code in Default.aspx.cs runs when a user chooses the  **Save Changes** button.</span></span>

```C#
protected void btnSaveListScopedIPRSettings_Click(object sender, EventArgs e)
        {
            List ipr = cc.Web.GetListByTitle(IPR_LIBRARY);
            EcmListManualRecordDeclaration listManual = (EcmListManualRecordDeclaration)Convert.ToInt32(rdListAvailability.SelectedValue);
            ipr.SetListManualRecordDeclaration(listManual);
            ipr.SetListAutoRecordDeclaration(chbAutoDeclare.Checked);

            // Refresh the settings as AutoDeclare changes the manual settings.
            if (ipr.IsListRecordSettingDefined())
            {
                rdListAvailability.SelectedValue = Convert.ToString((int)ipr.GetListManualRecordDeclaration());
                chbAutoDeclare.Checked = ipr.GetListAutoRecordDeclaration();
                rdListAvailability.Enabled = !chbAutoDeclare.Checked;
            }

        }
```

<span data-ttu-id="20a27-152">Код в файле RecordsManagementExtensions.cs OfficeDevPnP.Core вызывает следующие два метода:</span><span class="sxs-lookup"><span data-stu-id="20a27-152">The code calls the following two methods in the RecordsManagementExtensions.cs file of OfficeDevPnP.Core:</span></span>

-  <span data-ttu-id="20a27-153">**SetListManualRecordDeclaration** - задает параметр объявления записей вручную для этого списка.</span><span class="sxs-lookup"><span data-stu-id="20a27-153">**SetListManualRecordDeclaration** - Defines the manual records declaration setting for this list.</span></span>
    
-  <span data-ttu-id="20a27-154">**SetListAutoRecordDeclaration** - автоматически объявляет элементов, добавленных в этот список как записи.</span><span class="sxs-lookup"><span data-stu-id="20a27-154">**SetListAutoRecordDeclaration** - Automatically declares items added to this list as a record.</span></span> <span data-ttu-id="20a27-155">Если записей объявление устанавливается автоматически в этом списке, параметры объявления записей вручную в списке больше не будут применяться.</span><span class="sxs-lookup"><span data-stu-id="20a27-155">If records declaration is set to automatic on this list, the manual records declaration settings on the list no longer apply.</span></span> <span data-ttu-id="20a27-156">Приемники событий добавляются в список для запуска определенных записей управления действия при возникновении событий.</span><span class="sxs-lookup"><span data-stu-id="20a27-156">Event receivers are added to the list to start specific records management actions when events occur.</span></span>

```C#
public static void SetListManualRecordDeclaration(this List list, EcmListManualRecordDeclaration settings)
        {
            if (settings == EcmListManualRecordDeclaration.UseSiteCollectionDefaults)
            {
                // If you set list record declaration back to the default values, you also need to 
                // turn off auto record declaration. Other property bag values are left as is; when 
                // settings are changed again these properties are also again usable.
                if (list.PropertyBagContainsKey(ECM_AUTO_DECLARE_RECORDS))
                {
                    list.SetListAutoRecordDeclaration(false);
                }
                // Set the property that dictates custom list record settings to false.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, false.ToString());
            }
            else if (settings == EcmListManualRecordDeclaration.AlwaysAllowManualDeclaration)
            {
                list.SetPropertyBagValue(ECM_ALLOW_MANUAL_DECLARATION, true.ToString());
                // Set the property that dictates custom list record settings to true.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, true.ToString());
            } 
            else if (settings == EcmListManualRecordDeclaration.NeverAllowManualDeclaration)
            {
                list.SetPropertyBagValue(ECM_ALLOW_MANUAL_DECLARATION, false.ToString());
                // Set the property that dictates custom list record settings to true.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, true.ToString());
            }
            else
            {
                throw new ArgumentOutOfRangeException("settings");
            }
        }

public static void SetListAutoRecordDeclaration(this List list, bool autoDeclareRecords)
        {
            // Determine the SharePoint version based on the loaded CSOM library.
            Assembly asm = Assembly.GetAssembly(typeof(Microsoft.SharePoint.Client.Site));
            int sharePointVersion = asm.GetName().Version.Major;

            if (autoDeclareRecords)
            {
                // Set the property that dictates custom list record settings to true.
                list.SetPropertyBagValue(ECM_IPR_LIST_USE_LIST_SPECIFIC, true.ToString());
                // Prevent manual declaration.
                list.SetPropertyBagValue(ECM_ALLOW_MANUAL_DECLARATION, false.ToString());

                // Hook up the needed event handlers.
                list.Context.Load(list.EventReceivers);
                list.Context.ExecuteQuery();

                List<EventReceiverDefinition> currentEventReceivers = new List<EventReceiverDefinition>(list.EventReceivers.Count);
                currentEventReceivers.AddRange(list.EventReceivers);

                // Track changes to see if a list.Update is needed.
                bool eventReceiverAdded = false;
                
                // ItemUpdating receiver.
                EventReceiverDefinitionCreationInformation newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemUpdating, 1000, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemDeleting receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemDeleting, 1000, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemFileMoving receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemFileMoving, 1000, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemAdded receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemAdded, 1005, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemUpdated receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemUpdated, 1007, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                // ItemCheckedIn receiver.
                newEventReceiver = CreateECMRecordEventReceiverDefinition(EventReceiverType.ItemCheckedIn, 1006, sharePointVersion);
                if (!ContainsECMRecordEventReceiver(newEventReceiver, currentEventReceivers))
                {
                    list.EventReceivers.Add(newEventReceiver);
                    eventReceiverAdded = true;
                }
                                
                if (eventReceiverAdded)
                {
                    list.Update();
                    list.Context.ExecuteQuery();
                }

                // Set the property that dictates the autodeclaration.
                list.SetPropertyBagValue(ECM_AUTO_DECLARE_RECORDS, autoDeclareRecords.ToString());
            }
            else
            {
                // Set the property that dictates the autodeclaration.
                list.SetPropertyBagValue(ECM_AUTO_DECLARE_RECORDS, autoDeclareRecords.ToString());
                //Note: Existing list event handlers will just stay as they are, no need to remove them.
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="20a27-157">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="20a27-157">Additional resources</span></span>
<span data-ttu-id="20a27-158"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="20a27-158"></span></span>

-  [<span data-ttu-id="20a27-159">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="20a27-159">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="20a27-160">Пример OfficeDevPnP.Core</span><span class="sxs-lookup"><span data-stu-id="20a27-160">OfficeDevPnP.Core sample</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
