---
title: "Расширения управления записями пример приложения для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: cfc4269c4510b5bb9207e45458affcd99a9a2eab
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="records-management-extensions-sample-app-for-sharepoint"></a>Расширения управления записями пример приложения для SharePoint

В рамках стратегии Enterprise Content Management (ECM) можно включить и изменить параметры управления записями на месте на сайтах SharePoint и списков.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

[ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) примере показано, как использовать приложения SharePoint с размещением у поставщика для управления параметрами управления записями на месте для сайта или списка.    

Если вы хотите используйте этого решения:

- Настройка параметров управления записями на месте во время настраиваемой процедуры подготовки сайта.
 
## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите [ECM. RecordsManagement](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.RecordsManagement) пример приложения из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Перед запуском этого приложения:

- Активация компонента управления записями на месте в коллекции веб-сайтов, как показано на рисунке 1.
    
    **На рисунке 1. Активация управления записями на месте в семействе веб-сайтов**

    ![Снимок экрана, на странице возможности семейства веб-сайтов с помощью активированные функции управления записи на месте с выделением.](media/d99269ae-b8fc-445b-a1b8-1612b16dcba6.png)

- В параметрах сайта убедитесь, что отображаются **Параметры объявление записи** в **Администрирование семейства веб-сайтов**, как показано на рисунке 2.
    
    **На рисунке 2. Параметры объявления записей в настройках сайта**

    ![Снимок экрана на странице Параметры сайта с параметрами объявление записи с выделением.](media/13a6a490-68cd-4f70-8714-cd6222325890.png)

## <a name="using-the-ecmrecordsmanagement-sample-app"></a>С помощью ECM. Пример приложения RecordsManagement
<a name="sectionSection1"> </a>

 При запуске приложения, начальная страница отображает два сценария, которые доступны:

- Включение управления записями на месте для сайтов
    
- Включение управления записями на месте для списков

**На рисунке 3. ECM. Начальная страница приложения RecordsManagement**

![Снимок экрана приложения начальная страница, отображается в двух сценариях.](media/a5fb2d86-2365-4d39-b41e-29719ab88287.png) 

Сценарий 1 можно использовать для создания пользовательского интерфейса для управления параметрами управления записями на семействе веб-сайтов. Пользовательский Интерфейс в этом приложении похож на пользовательский Интерфейс, обнаруженных в **Параметры объявления записей** в **Настройках сайта** (см). Также можно активировать или деактивировать компонент управления записями на месте в семействе веб-сайтов.

Сценарий 2 можно использовать для создания пользовательского интерфейса для управления параметрами управления записями на списки. Пользовательский Интерфейс в этом приложении похож на пользовательский Интерфейс, обнаруженных в **параметрах объявления записей** в параметры библиотеки в список.

**На рисунке 4. Объявление параметров записи в списке.**

![Снимок экрана на странице Параметры объявления записей библиотеки.](media/2522e4b0-5d5c-40bc-829d-f13d96a2b233.png)
### <a name="scenaro-1"></a>Scenaro 1

Сценарий 1 решает функций управления записями на месте и параметров для сайтов. Пользовательский Интерфейс приложения отображается кнопка **Деактивировать** (или **активировать**), как показано на рисунке 5. Выбрав эту кнопку деактивирует (или активирует) компонента управления записями на месте в коллекции веб-сайтов. 

**На рисунке 5. Отключение кнопки для функции управления записями на месте**

![Снимок экрана, которая отображает деактивировать и активировать кнопку для управления записями на месте.](media/b1a29cad-4239-4f49-a3e8-ca4e8ca99667.png)

Приведенный ниже код активирует или деактивирует компонента управления записями на месте в коллекции веб-сайтов. Методы **DisableInPlaceRecordsManagementFeature** и **EnableSiteForInPlaceRecordsManagement** являются частью файла AppModelExtensions\RecordsManagementExtensions.cs в [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).
    
> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

OfficeDevPnP.Core включает в себя методы расширения для получения и задания параметров управления записями на месте всех веб сайтов. Следующий код в метод **EnableSiteForInPlaceRecordsManagement** показано, как использовать эти методы для установки ограничений и укажите пользователей, которые можно объявить или отменить объявление записи на вашем сайте.

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

Когда пользователь изменяет свои параметры управления записями на месте и выбирает кнопки **Сохранить изменения** , выполняется следующий код в метод **btnSaveSiteScopedIPRSettings_Click** .

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

В предыдущем примере кода выполняется вызов метода **SetRecordRestrictions** в RecordsManagementExtensions.cs. Метод **SetRecordRestrictions** в следующем примере показано, как для установки ограничений на записи.

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

### <a name="scenario-2"></a>Сценарий 2

Сценарий 2 показано, как взаимодействовать с записями на месте параметры управления для списков. При установке приложения, он создает библиотеки документов, называется IPRTest. При использовании этого приложения для изменения и сохранения параметров управления записями на месте, эти изменения применяются к IPRTest. 

> [!NOTE] 
> Чтобы использовать параметры управления записями на месте для списка, необходимо активировать компонент управления записями на месте в семействе веб-сайтов, как показано на рисунке 1 ранее в этой статье. 

Следующий код в файле Default.aspx.cs выполняется, если пользователь выбирает кнопку **Сохранить изменения** .

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

Код в файле RecordsManagementExtensions.cs OfficeDevPnP.Core вызывает следующие два метода:

-  **SetListManualRecordDeclaration** - задает параметр объявления записей вручную для этого списка.
    
-  **SetListAutoRecordDeclaration** - автоматически объявляет элементов, добавленных в этот список как записи. Если записей объявление устанавливается автоматически в этом списке, параметры объявления записей вручную в списке больше не будут применяться. Приемники событий добавляются в список для запуска определенных записей управления действия при возникновении событий.

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Пример OfficeDevPnP.Core](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core)
