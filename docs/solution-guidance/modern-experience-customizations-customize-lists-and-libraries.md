---
title: "Настройка «современный» списки и библиотеки"
description: "Получите быстрее, интуитивно и быстро SharePoint Online взаимодействия с настройки списков и библиотек «современный» работы, с помощью пользовательских дополнительных действий и настраиваемый фирменный стиль."
ms.date: 11/09/2017
ms.openlocfilehash: 2d888eecadd410bb64baf9d01d888253f25d656a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="customizing-modern-lists-and-libraries"></a>Настройка «современный» списки и библиотеки

В 2016 группы SharePoint Online выпущен «современный» документ списки и библиотеки, которые свести удобство работы пользователей, быстрее, интуитивно и быстро. **«Современный» каждый раз имеют много преимуществ, и мы настоятельно рекомендуем их использования**. Если текущих настроек еще не работают с «современный» качества, будет вернуться к этой теме те, поэтому пользователи могут воспользоваться преимуществами следующие усовершенствования:

 - «Современный» библиотеки документов имеют обновленный пользовательский интерфейс, который предоставляет обеспечения взаимодействия, аналогичную OneDrive, чтобы сделать его более интуитивного, чтобы создать новую папку и загрузки файлов в браузере.
 
 - Вы можете выбрать **ПИН-код в начало** Добавление документов «выше за рамкой окна» в любом представлении, на экране.
 
 - Копирование не новый, но жесты копирование и перемещение intelligent об отображении информационной архитектуры и предоставляя возможность создавать новые папки во время выполнения.
 
 - Не может потребоваться больше делать столько копий. Библиотеки документов, intelligent запомнить другие файлы, которые использовались в SharePoint, поэтому можно импортировать другие файлы из других библиотек как ссылки, без необходимости для копирования файлов между несколькими сайтами.
 
 - Новые библиотеки документов позволяют группировать файлы непосредственно в главной странице без выбора отдельных admin экрана. Также можно перетащить изменить размер столбцов, а также сортировка, фильтр и группы из любой заголовок столбца.
 
 - Браузеры мобильных устройств имеют те же функции, как рабочий стол, что SharePoint производительность пользователей для каждого пользователя взаимодействием с помощью мыши, клавиатуры, сенсорного ввода или чтения с экрана.
 
 - Теперь можно редактировать метаданные непосредственно из основного представления в области сведений о документах. Не более, щелкнув в несколько экранов для применения обновления к!
 
 - Благодаря интеграции с Office Online можно перейти preview весь документ в верхней части области сведений о документах. Панель предлагает метаданные, включая журнал последнее действие обновляет в файл, а кто полученных совместный доступ к файлу.

Эта статья посвящена вариантов расширения «современный» библиотеки и списка среды взаимодействия с пользователем. Тем не менее если вы хотите узнать больше о функциональных возможностей, предоставляемых «современный» каждый раз, можно найти в следующих ресурсах:

- [Современный библиотек в SharePoint](https://blogs.office.com/2016/06/07/modern-document-libraries-in-sharepoint)
- [Здесь вы современных списки SharePoint, включая интеграцию с Microsoft потока и PowerApps](https://blogs.office.com/2016/07/25/modern-sharepoint-lists-are-here-including-integration-with-microsoft-flow-and-powerapps)
- [Различия между каждый раз новые и классический для списков и библиотек](https://support.office.com/en-us/article/Differences-between-classic-and-new-experiences-for-lists-and-document-libraries-30e1aab0-a5cc-4363-b7f2-09e2ae07d4dc?ui=en-US&rs=en-US&ad=US)

В оставшейся части этой статьи мы будем использовать «современный» для нового пользовательского интерфейса и «классический» для прежних версий пользовательского интерфейса. 

> [!IMPORTANT]
> Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».


<a name="customizationoptions"> </a>
## <a name="overview-of-customization-options"></a>Обзор параметров настройки

«Современный» списки и библиотеки не поддерживают столько параметры настройки в качестве «классический» списки и библиотеки. В этой статье предоставляются сведения и примеры поддерживаемые параметры. Группы разработчиков SharePoint работает на другие варианты технической поддержки в будущем. В следующем списке приведено краткий обзор поддерживаемые возможности для «современный» списков и библиотек:
 
 - Подмножество пользовательских дополнительных действий
 - Настраиваемый фирменный стиль
 - Интеграция с PowerApps и поток

Эти настройки в настоящее время не поддерживается для «современный» списков и библиотек:
 
 - Настройки на основе JSLink поля (Примечание на *Расширения Framework SharePoint*)
 - Представление на основе JSLink настроек (Примечание на *Расширения Framework SharePoint*)
 - Настраиваемые CSS с помощью свойства web AlternateCSSUrl
 - Настраиваемый JavaScript, внедренные с помощью пользовательских дополнительных действий (Примечание на *Расширения Framework SharePoint*)
 - Настраиваемые главные страницы (расширенный фирменной символики будет поддерживаться более поздней версии с помощью альтернативных параметров)
 - Настройка с помощью InfoPath
 - Стратегия минимальной загрузки (MDS)
 - Публикация SharePoint server

> [!NOTE]
> В 2017 июня [расширения Framework SharePoint занялся preview для разработчиков](https://dev.office.com/blogs/announcing-availability-of-sharepoint-framework-extensions-developer-preview). Использование этих расширений Framework SharePoint, можно управлять визуализации поля с помощью пользовательского кода и создание пользователя настраиваемых действий, выполняемых пользовательского кода. Для получения дополнительных сведений см [Overview of Framework расширения SharePoint](http://aka.ms/spfx-extensions). 

<a name="supportedcustomactions"> </a>
## <a name="user-custom-actions"></a>Настраиваемые действия пользователя

Разрешить определенные пользователя настраиваемые действия, доступные в новый пользовательский интерфейс «современный» каждый раз, но не все конфигурации действие пользователя, поддерживаемых приложением «классический» режим поддерживаются «современный» сайтами. В следующей таблице приведено подробное описание расположений поддерживаемые пользовательских действий и способы их в случае предоставления в пользовательском Интерфейсе «современный»:

|**Расположение дополнительного действия пользователя**|**Видимы в «новый» пользовательский Интерфейс**|
|:-----|:-----|
| `EditControlBlock` | Да, эти записи отображаться в качестве настраиваемых элементов меню.|
| `CommandUI.Ribbon` | Да, эти записи отображаются как элементы панели инструментов. |
| Все другие расположения (например `scriptlink`) | К сожалению, настраиваемые действия пользователя, не будут работать. |

> [!NOTE]
> Эти настраиваемые действия отображаются в «современный» списки и библиотеки только в том случае, если пользователь находится в «классический» сайты с поддержкой «новый» пользовательский Интерфейс. По умолчанию они не отображаются на «современный» веб-сайтах, так как невозможно добавить настраиваемые действия пользователя «современный» сайты, поскольку они имеют включен параметр NoScript. Тем не менее можно отключить NoScript на «современный» веб-сайтах для достижения это поведение для «современный» списков и библиотек между сайтами «классический» и «современный».

<a name="editcontrolblockcustomactions"> </a>
### <a name="editcontrolblock-user-custom-actions"></a>EditControlBlock пользовательских дополнительных действий 

Добавление пользовательских ссылок в контекстном меню можно выполнить с помощью `EditControlBlock` по для дополнительного действия. Следующий PnP подготовки XML-код создает два настраиваемых записей. 

```XML
<pnp:ProvisioningTemplate ID="EditControlBlockSamples" Version="1" xmlns:pnp="http://schemas.dev.office.com/PnP/2015/12/ProvisioningSchema">
  <pnp:CustomActions>
    <pnp:SiteCustomActions>
      <pnp:CustomAction Name="CA_1" Description="ca 1" Location="EditControlBlock" RegistrationType="List" RegistrationId="101" Title="CA 1 Title" Sequence="3000" Url="https://contoso.azurewebsites.net/pages/index.aspx" Enabled="true"/>
      <pnp:CustomAction Name="CA_2" Description="ca 2" Location="EditControlBlock" RegistrationType="ContentType" RegistrationId="0x0101" Title="CA 2 Title" Sequence="4000" Url="https://contoso.azurewebsites.net/pages/index.aspx" Enabled="true"/>
    </pnp:SiteCustomActions>
  </pnp:CustomActions>
</pnp:ProvisioningTemplate>
```

Можно применить этот [PnP подготовки шаблона](https://msdn.microsoft.com/en-us/pnp_articles/pnp-provisioning-engine-and-the-core-library) на сайт с помощью PnP основной библиотеки или [PnP PowerShell](http://aka.ms/sppnp-powershell). Мы удалили Показать подход PowerShell в данной статье. Первым шагом является [Установка модуля PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell). После этого сохраните PnP подготовки XML в файл и две простой строки PnP PowerShell являются достаточно, чтобы применить шаблон:

```PowerShell

# Connect to a previously created Modern Site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Apply the PnP provisioning template
Apply-PnPProvisioningTemplate -Path c:\customaction_modern_editcontrolblock.xml -Handlers CustomActions

```

Если обновить представление «современный» библиотеки документов на сайте, вы увидите новых записей отображаются.

*На рисунке 1. Настраиваемые действия EditControlBlock, отображается в меню*

<img src="media/modern-experiences/custom-editcontrolblock-actions.png" alt="Custom EditControlBlock actions visible in the menu" width="700">


> [!NOTE]
> - Если вы пытаетесь на [сайт группы «современный»](modern-experience-customizations-customize-sites.md) , где вы отключили параметр NoScript, используйте апрель, 2017 или более поздней версии из PnP PowerShell. Кроме того используйте текущую версию разработчиков.
> - Если вы хотите использовать в этом примере для списка, необходимо задать `RegistrationId` атрибут до 100.

<a name="ribboncustomactions"> </a>
### <a name="commanduiribbon-user-custom-actions"></a>Значение CommandUI.Ribbon пользовательских дополнительных действий 

Если необходимо расширить панели инструментов «современный» каждый раз списков и библиотек, вы можете Добавление пользовательского настраиваемого действия целевого расположения значение CommandUI.Ribbon, как показано в этом PnP подготовки образец XML.

```XML
<pnp:ProvisioningTemplate ID="CommandUIRibbonSamples" Version="1" xmlns:pnp="http://schemas.dev.office.com/PnP/2015/12/ProvisioningSchema">
  <pnp:CustomActions>
    <pnp:SiteCustomActions>
      <pnp:CustomAction Name="CA_4" Description="ca 4" Location="CommandUI.Ribbon" RegistrationType="List" RegistrationId="101" Title="CA 4 Title" Sequence="6000" Enabled="true">
        <pnp:CommandUIExtension>
          <CommandUIDefinitions>
            <CommandUIDefinition Location="Ribbon.Documents.Copies.Controls._children">
              <Button
                Id="Ribbon.Documents.Copies.OfficeDevPnPDownloadAll"
                Command="OfficeDevPnP.Cmd.DownloadAll"
                Image16by16="/_layouts/15/images/sharepointfoundation16.png"
                LabelText="Download All"
                Description="Download all files separately"
                ToolTipTitle="Download All"
                ToolTipDescription="Download all files separately"
                TemplateAlias="o1"
                Sequence="15"/>
            </CommandUIDefinition>
          </CommandUIDefinitions>
          <CommandUIHandlers>
            <CommandUIHandler
              Command="OfficeDevPnP.Cmd.DownloadAll"
              CommandAction="https://contoso.azurewebsites.net/pages/index.aspx" />
          </CommandUIHandlers>
        </pnp:CommandUIExtension>
      </pnp:CustomAction>
      <pnp:CustomAction Name="CA_6" Description="ca 6" Location="CommandUI.Ribbon" RegistrationType="ContentType" RegistrationId="0x0101" Title="CA 6 Title" Sequence="5000" Enabled="true">
        <pnp:CommandUIExtension>
            <CommandUIDefinitions>
              <CommandUIDefinition Location="Ribbon.Tabs._children">
                <Tab Id="Custom Tab" Title="Custom Tab" Description="Custom Tab">
                  <Scaling Id="Custom Tab.Scaling">
                    <MaxSize Id="Custom Group.Scaling.MaxSize" GroupId="Custom Group" Size="TwoLarge" />
                    <MaxSize Id="Custom Group 2.Scaling.MaxSize" GroupId="Custom Group 2" Size="OneLarge" />
                    <Scale Id="Custom Group.Scaling.Scale" GroupId="Custom Group" Size="TwoLarge" />
                    <Scale Id="Custom Group 2.Scaling.Scale" GroupId="Custom Group 2" Size="OneLarge" />
                  </Scaling>
                  <Groups Id="Custom Tab.Groups">
                    <Group Id="Custom Group 2" Title="Custom Group 2" Description="Custom Group 2" Sequence="7888" Template="Ribbon.Templates.OneLarge">
                      <Controls Id="Custom Group 2.Controls">
                        <Button Id="CustomButton3" LabelText="Custom Button 3" Image16by16="/_layouts/15/images/attach16.png" Image32by32="/_layouts/15/images/attach16.png" ToolTipTitle="Custom Button 3" ToolTipDescription="Custom Button 3" Command="CustomButton3.Command" TemplateAlias="c3" />
                      </Controls>
                    </Group>
                    <Group Id="Custom Group" Title="Custom Group 1" Description="Custom Group 1" Sequence="10000" Template="Ribbon.Templates.TwoLarge">
                      <Controls Id="Custom Group 1.Controls">
                        <Button Id="CustomButton1" LabelText="Custom Button 1" Image16by16="/_layouts/15/images/itslidelibrary.png" Image32by32="/_layouts/15/images/itslidelibrary.png" ToolTipTitle="Custom Button 1" ToolTipDescription="Custom Button 1" Command="CustomButton1.Command" TemplateAlias="c1" />
                        <Button Id="CustomButton2" LabelText="Custom Button 2" Image16by16="/_layouts/15/images/dldsln16.png" Image32by32="/_layouts/15/images/dldsln16.png" ToolTipTitle="Custom Button 2" ToolTipDescription="Custom Button 2" Command="CustomButton2.Command" TemplateAlias="c2" />
                      </Controls>
                    </Group>
                  </Groups>
                </Tab>
              </CommandUIDefinition>
              <CommandUIDefinition Location="Ribbon.Templates._children">
                <GroupTemplate Id="Ribbon.Templates.TwoLarge">
                  <Layout Title="TwoLarge" LayoutTitle="TwoLarge"> 
                    <Section Alignment="Top" Type="OneRow"> 
                      <Row> 
                        <ControlRef DisplayMode="Large" TemplateAlias="c1" /> 
                        <ControlRef DisplayMode="Large" TemplateAlias="c2" /> 
                      </Row> 
                    </Section> 
                  </Layout> 
                </GroupTemplate>
              </CommandUIDefinition>
              <CommandUIDefinition Location="Ribbon.Templates._children">
                <GroupTemplate Id="Ribbon.Templates.OneLarge">
                  <Layout Title="OneLarge" LayoutTitle="OneLarge"> 
                    <Section Alignment="Top" Type="OneRow"> 
                      <Row> 
                        <ControlRef DisplayMode="Large" TemplateAlias="c3" /> 
                      </Row> 
                    </Section> 
                  </Layout> 
                </GroupTemplate>
              </CommandUIDefinition>
            </CommandUIDefinitions>
            <CommandUIHandlers>
              <CommandUIHandler Command="CustomButton1.Command" CommandAction="https://contoso.azurewebsites.net/pages/index.aspx" />
              <CommandUIHandler Command="CustomButton2.Command" CommandAction="http://www.bing.com" />
              <CommandUIHandler Command="CustomButton3.Command" CommandAction="http://dev.office.com/sharepoint" />
            </CommandUIHandlers>
        </pnp:CommandUIExtension>
      </pnp:CustomAction>
    </pnp:SiteCustomActions>
  </pnp:CustomActions>
</pnp:ProvisioningTemplate>
```

<br/>

После добавления этих пользовательских дополнительных действий, чтобы увидеть их на панели инструментов. Обратите внимание на то, что пользовательские вкладки преобразуются в раскрывающемся меню.

*На рисунке 2. Настраиваемое действие отображается на панели инструментов*

![Настраиваемое действие отображается на панели инструментов](media/modern-experiences/custom-actions-toolbar.png)

<br/>

> [!NOTE]
> - Если вы пытаетесь на [сайт группы «современный»](modern-experience-customizations-customize-sites.md) , где вы отключили параметр NoScript, используйте апрель, 2017 или более поздней версии из PnP PowerShell. Или же используйте текущую версию разработчиков.
> - Если вы хотите использовать в этом примере для списка, необходимо задать `RegistrationId` атрибуты 100 и используйте следующий XML-код настраиваемого действия пользователя CA_4.
>
   ```XML
    <CommandUIDefinition Location="Ribbon.Templates._children">
      <Button
        Id="Ribbon.Templates.OfficeDevPnPDownloadAll"
        Command="OfficeDevPnP.Cmd.DownloadAll"
        Image16by16="/_layouts/15/images/sharepointfoundation16.png"
        LabelText="Download All"
        Description="Download all files separately"
        ToolTipTitle="Download All"
        ToolTipDescription="Download all files separately"
        TemplateAlias="o1"
        Sequence="15"/>
    </CommandUIDefinition>
   ```

<a name="customactionlimitations"> </a>
### <a name="user-custom-action-limitations"></a>Ограничения дополнительного действия пользователя 

При разработке пользовательских дополнительных действий, которые необходимы для работы в «современный» каждый раз, необходимо учитывайте следующие ограничения:
 
 - Вы не можете определять полностью порядке, в котором пользовательских дополнительных действий отображаться; Настраиваемые действия пользователя добавляются в том порядке, `_api/web/Lists(guid'listid')/CustomActionElements` возвращает пользовательских дополнительных действий, а в настоящее время этот интерфейс API не учитывать последовательность атрибутов. Кнопки, определенного в пользовательской вкладки могут быть упорядочены путем добавления их в правильном порядке в XML-коде CommandUIDefinition. Наш пример отображается кнопка 3 как первый и, из-за порядок, в XML-код.
 
 - Группирования пользовательских дополнительных действий внутри настраиваемой вкладки определяется наличие `Button` элементов при наличии любого из нескольких `Tab` или `Group` элементов в элемент xml возвращенные пользователя дополнительного действия.
 
 - Команда действия не может содержать JavaScript. Например, с помощью `CommandAction="javascript:alert('My custom Action');"` означает, что настраиваемое действие пользователя не будет отображаться.
 
 - С помощью `ScriptLink` или `ScriptBlock` свойства невозможен, так как они могут использоваться только с расположение дополнительного действия пользователя `ScriptLink`, который не поддерживается.
 
 - С помощью гиперкарты (например, `Image16by16="/_layouts/15/1033/images/formatmap16x16.png?rev=33" Image16by16Left="-144" Image16by16Top="-107"`) не работает; необходимо указать отдельные изображения. Обратите внимание, что относятся только 16 x 16 изображений.

<a name="themingimpact"> </a>
## <a name="custom-branding"></a>Настраиваемый фирменный стиль

Если использовать пользовательскую тему веб-узла, учитываемые этой пользовательской темы в списке «современный» и библиотека процедуры, как показано в следующем примере.

*На рисунке 3. Современный список с настраиваемой фирменной настройки поступающих от пользовательской темы*

<img src="media/modern-experiences/modern-list-with-custom-theme.png" alt="Modern list with custom branding coming from custom theme" width="700">

<a name="configuremodernlibrariesandlists"> </a>
## <a name="configure-the-end-user-experience"></a>Настройка конечных пользователей

Имеется несколько возможностей для элемента управления «современный» или «классический» библиотеки и списка работу в используется ли. 

### <a name="tenant-level-configuration"></a>Конфигурирование на уровне клиента
Если необходимо полностью отключить «современный» качества, рекомендуется использовать параметр базы данных для клиента. Перейдите в центр администрирования клиента (например, contoso-admin.sharepoint.com), перейдите в раздел Параметры и выберите «классический» качества.

*На рисунке 4. Списки и библиотеки SharePoint взаимодействия параметры в пользовательском Интерфейсе администрирования SharePoint*

![Списки и библиотеки SharePoint взаимодействия параметры в пользовательском Интерфейсе администрирования SharePoint](media/modern-experiences/lists-libraries-tenant-settings.png)

> [!NOTE]
> - При переключении между **новой версии интерфейса (автоматическое обнаружение)** и **классическом взаимодействия**, изменения не видны непосредственно.
> - При выборе **новой версии интерфейса (автоматическое обнаружение)**, параметр **вернуться к классической SharePoint** всегда отображается. Это предусмотрено при проектировании, реализации сегодня не все функциональные возможности «классический» списков и библиотек «современный» списков и библиотек. Нет, невозможно изменить это поведение.

### <a name="siteweb-level-configuration"></a>Конфигурации уровня сайта и веб-
Вы можете запретить семейства веб-сайтов или веб-использования «современный» интерфейса посредством включения компонента:

- Для управления семейства сайтов используйте функцию семейства одним сайта с Идентификатором **E3540C7D-6BEA-403C-A224-1A12EAFEE4C4**. 
- Для веб-элемент управления используйте функцию уровня веб-сайта с Идентификатором **52E14B6F-B1BB-4969-B89B-C4FAA56745EF**. 

Чтобы включить или отключить необходимых компонентов с помощью следующих [PnP PowerShell](http://aka.ms/sppnp-powershell) :

```PowerShell
# Connect to a site
$cred = Get-Credential
Connect-PnPOnline -Url https://[tenant].sharepoint.com/sites/siteurl -Credentials $cred

# Prevent modern lists and libraries at site collection level
Enable-PnPFeature -Identity E3540C7D-6BEA-403C-A224-1A12EAFEE4C4 -Scope Site 
# And again enable modern lists and libraries at site collection level
#Disable-PnPFeature -Identity E3540C7D-6BEA-403C-A224-1A12EAFEE4C4 -Scope Site 

# Prevent modern lists and libraries at web level
#Enable-PnPFeature -Identity 52E14B6F-B1BB-4969-B89B-C4FAA56745EF  -Scope Web 
# And again enable modern lists and libraries at web
#Disable-PnPFeature -Identity 52E14B6F-B1BB-4969-B89B-C4FAA56745EF  -Scope Web 
```

### <a name="listlibrary-configuration"></a>Конфигурация списка/библиотеки
Если вы хотите управлять интерфейса на уровне библиотеки, вы сможете **Параметры списка** > **Дополнительные параметры**и изменить поведение.

*На рисунке 5. Конфигурация качества списка параметров уровня клиента SharePoint в пользовательский Интерфейс администрирования*

![Конфигурация качества списка параметров уровня клиента SharePoint в пользовательский Интерфейс администрирования](media/modern-experiences/list-experience-setting.png)

То же самое можно выполнить с помощью CSOM, как показано в этом фрагменте:

```C#
// Load the list you want to update
var list = context.Web.Lists.GetByTitle(title);
context.Load(list);
context.ExecuteQuery();

// Possible options are Auto (= what it's defined at tenant level), NewExperience (= "modern") and ClassicExperience
list.ListExperienceOptions = ListExperience.ClassicExperience;

// Persist the changes
list.Update();
context.ExecuteQuery();
```

> [!NOTE]
> - Параметры библиотеки на уровне *переопределить* параметры на уровне клиента, сайта или web. Это также означает, что может пилотный проект «современный» качества списков и библиотек на дочерний сайт сайтов благодаря использованию «современный» качества отключено на уровне клиента, но включен на уровне списка на пилотных сайтов.
> - Когда вы вручную выбрал «классический» (то есть не из-за списка, веб-сайтов, веб-сайта или клиентов «классический» принудительное применение), вы увидите, **Exit классический качества** связи, отображаемым в поле левой панели навигации (по состоянию на июля 2017). Выбор этого приводит «современный» качества.
> - Если вы не приобретать «современный» интерфейса должна отображаться, проверьте файлы cookie, переданного в SharePoint, так как по-прежнему остается, что явного масштабирование файла cookie «современный» каждый раз (splnu с установлено значение 0). Очистка файлов cookie браузера необходимо устранить эту неполадку.

<a name="autodetect"> </a>
## <a name="when-does-the-built-in-auto-detect-automatically-switch-rendering-back-to-classic"></a>Когда встроенных auto определит, автоматически визуализации переключатель обратно в «классический»?

SharePoint использует автоматическое обнаружение системы для автоматического перехода с отображением списка «Классическая», при условии, что вы не отключайте «современный» взаимодействия для списка с помощью сайта, web или областью действия списка переопределений описано в предыдущем разделе. Это автоматическое обнаружение, система автоматически вы перейдет в режим «классический» каждый раз, когда SharePoint обнаруживает, что список функции (еще не) поддерживается в «современный».

Ниже перечислены параметры, которые будут оцениваться как часть Автовыбор системы, а какие сделать список воспроизведения в режиме «классический»:

- Если страница формы запрошенный список содержит ноль или более одного веб-части.

- (**До июля 2017**) Если веб-сайта, областью действия компонента «Навигация и фильтрация метаданных» включено. Мы [развертывание управляемых метаданных навигации поддержка «современный» списки и библиотеки](https://techcommunity.microsoft.com/t5/SharePoint-Blog/SharePoint-filters-pane-updates-filtering-and-metadata/ba-p/74162).

- Если доступные веб-часть будет **XSLTListViewWebPart** (вариант по умолчанию для отображения в списке) и:
    - Существует нестандартный набор JSLink или XslLink значение для свойства веб-части.
    - Страница будет отображена в диалоговом окне (IsDlg = 1).
    - Список не основан на одном из следующих типов: документов библиотеки (101), библиотеки (109) изображения, библиотеки веб-страниц (119) или общий список (100). **По состоянию на август 2017**, извещений (104), а затем ссылки (103) выполните отображения с помощью «новый» пользовательский Интерфейс.
    - Свойство JSLink устанавливается для одного из полей для отображения.
    - Одно из полей для отображения типу **BCS внешних данных**, **географическое положение** **OutcomeChoice**или один из этих публикации поля типов **изображения**, **Html**или **Сводные ссылки**.
    - Существует областью действия список пользовательских дополнительных действий, которые их ScriptSrc свойство должно быть указано.

- Если доступные веб-часть будет **ListFormWebPart** и: 
    - Страница будет отображена в диалоговом окне (IsDlg = 1). 
    - Это страница формы «Новый» для библиотеки документов.  
    - Поля для отображения не любого из следующих поддерживаемых типов: **вложения**, **TaxonomyField**, **Boolean**, **Выбор**, **валюты**, **даты и времени**, **файла**, **подстановки**, **MultiChoice** **MultiLine **за исключением при Append с управлением версиями на, **число**, **текст**, **пользователя**или **URL-адрес**.

### <a name="programmatically-detect-if-your-librarylist-will-be-shown-using-modern-or-classic"></a>Программная обнаруживать если библиотеки или списка будут отображаться с помощью «современный» или «классический» 

Предыдущем разделе описано в статье также приводится обоснование наших Автовыбор механизм, но к счастью существует простой способ для вас как разработчику понять, как будут отображаться библиотеки или списка. Получение сведений о этот сложнее, как получение значения свойства файла **PageRenderType** , который можно получить с помощью REST или CSOM. Следующие примеры показывают, как загрузить страницу, отображение списка, а затем **PageRenderType**:

#### <a name="csom-sample"></a>Пример CSOM

```C#
using (var cc = new ClientContext(siteUrl))
{
    cc.Credentials = new SharePointOnlineCredentials(userName, password);
    
    // Load the AllItems.aspx file from the list
    File file = cc.Web.GetFileByServerRelativeUrl("/sites/dev/ECMTest/Forms/AllItems.aspx");
    cc.Load(file, f => f.PageRenderType);
    cc.ExecuteQuery();

    // Check page render type
    Console.WriteLine($"Status = {file.PageRenderType}");
}
```

<br/>

> [!NOTE]
> Свойство PageRenderType была введена в [2017 января CSOM выпуска (16.1.6112.1200)](https://dev.office.com/blogs/new-sharepoint-csom-version-released-for-Office-365-january-2017).

<br/>

#### <a name="rest-request"></a>Запрос REST

```Html
GET _api/web/getfilebyserverrelativeurl('/sites/dev/ECMTest/Forms/AllItems.aspx')/pageRenderType
```

Вызовов REST возвращает целое значение, которое описывается в следующей таблице.

Значение | Причина
:------:|-------
0 | Значение undefined = 0, (не достаточно сведений, чтобы знать режима отображения)
1 | MultipeWePart
2 | JSLinkCustomization
3 | XslLinkCustomization
4 | NoSPList
5 | HasBusinessDataField
6 | HasTaskOutcomeField
7 | HasPublishingField
8 | HasGeolocationField
9 | HasCustomActionWithCode
10 | HasMetadataNavFeature 
11 | SpecialViewType
12 | ListTypeNoSupportForModernMode
13 | Анонимных пользователей
14 | ListSettingOff
15 | SiteSettingOff
16 | WebSettingOff
17 | TenantSettingOff
18 | CustomizedForm
19 | DocLibNewForm
20 | UnsupportedFieldTypeInForm
21 | InvalidFieldTypeInForm 
22 | InvalidControModeInForm
23 | CustomizedPage
24 | ListTemplateNotSupported
100 | Современный


## <a name="additional-considerations"></a>Дополнительные сведения о выполнении

Постепенно описываются дополнительные параметры настройки для «современный» списка и библиотеки среды взаимодействия с пользователем. Эти способ выравнивания в выпуске дополнительные возможности среды SharePoint. На данный момент нет расписание не точное, но при выпуске новых возможностей взаимодействия «современный» статьи будут обновляться.

## <a name="see-also"></a>См. также

- [Настройка "современных" интерфейсов в SharePoint Online](modern-experience-customizations.md)
- [Переключение интерфейса по умолчанию для списков или библиотек документов из новых или классический](https://support.office.com/en-us/article/Switch-the-default-experience-for-lists-or-document-libraries-from-new-or-classic-66dac24b-4177-4775-bf50-3d267318caa9)
- [Современный библиотек в SharePoint](https://blogs.office.com/2016/06/07/modern-document-libraries-in-sharepoint)
- [Здесь вы современных списки SharePoint, включая интеграцию с Microsoft потока и PowerApps](https://blogs.office.com/2016/07/25/modern-sharepoint-lists-are-here-including-integration-with-microsoft-flow-and-powerapps) 
- [Различия между каждый раз новые и классический для списков и библиотек](https://support.office.com/en-us/article/Differences-between-the-new-and-classic-experiences-for-lists-and-libraries-30e1aab0-a5cc-4363-b7f2-09e2ae07d4dc?ui=en-US&rs=en-US&ad=US)
