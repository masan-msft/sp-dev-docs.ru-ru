---
title: "Добавление настраиваемой ленты на сайт SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 371711f55879477a62cd891c04e86e8aa2101db0
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="add-a-custom-ribbon-to-your-sharepoint-site"></a><span data-ttu-id="695a4-102">Добавление настраиваемой ленты на сайт SharePoint</span><span class="sxs-lookup"><span data-stu-id="695a4-102">Add a custom ribbon to your SharePoint site</span></span>

<span data-ttu-id="695a4-103">Добавление или удаление настраиваемой ленты на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="695a4-103">Add or remove a custom ribbon on your SharePoint site.</span></span> <span data-ttu-id="695a4-104">Добавление обработчиков событий JavaScript, с помощью JavaScript метод embed для обработки событий настраиваемой ленты.</span><span class="sxs-lookup"><span data-stu-id="695a4-104">Add JavaScript event handlers using the embed JavaScript technique to handle your custom ribbon's events.</span></span>

<span data-ttu-id="695a4-105">_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="695a4-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="695a4-106">Пример кода [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) показано, как для добавления настраиваемой ленты на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="695a4-106">The  [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) code sample shows you how to add a custom ribbon to a SharePoint site.</span></span> <span data-ttu-id="695a4-107">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="695a4-107">Use this solution if you want to:</span></span>

- <span data-ttu-id="695a4-108">Добавление настраиваемой ленты, группы или кнопка для сайта SharePoint или список.</span><span class="sxs-lookup"><span data-stu-id="695a4-108">Add a custom ribbon, group, or button to your SharePoint site or list.</span></span>
    
- <span data-ttu-id="695a4-109">Отображение настраиваемой ленты для определенных типов контента сайтов и списков.</span><span class="sxs-lookup"><span data-stu-id="695a4-109">Display a custom ribbon for specific content types, sites, or lists.</span></span>

<span data-ttu-id="695a4-110">**Примечание**  В этом примере кода показано, как вызывать функции JavaScript, которые обрабатывают события, вызванные кнопок на ленте.</span><span class="sxs-lookup"><span data-stu-id="695a4-110">**Note**  This code sample shows how to call the JavaScript functions that handle events raised by the ribbon's buttons.</span></span> <span data-ttu-id="695a4-111">В этом примере не предоставляет реализацию функций обработчика событий JavaScript для кнопок на ленте.</span><span class="sxs-lookup"><span data-stu-id="695a4-111">This code sample does not provide the implementation of the JavaScript event handler functions for the ribbon's buttons.</span></span> <span data-ttu-id="695a4-112">Для реализации функции обработчика событий JavaScript, используйте embed технология JavaScript для внедрения функции обработчика событий JavaScript на всех страницах место, где отображается настраиваемая лента.</span><span class="sxs-lookup"><span data-stu-id="695a4-112">To implement the JavaScript event handler functions, use the embed JavaScript technique to embed the JavaScript event handler functions on all pages where your custom ribbon appears.</span></span> <span data-ttu-id="695a4-113">Дополнительные сведения о внедрении JavaScript содержатся в разделе [Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span><span class="sxs-lookup"><span data-stu-id="695a4-113">For more information about embedding JavaScript, see  [Customize your SharePoint site UI by using JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="695a4-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="695a4-114">Before you begin</span></span>
<span data-ttu-id="695a4-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="695a4-115"></span></span>

<span data-ttu-id="695a4-116">Чтобы начать работу, загрузите пример надстройки [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="695a4-116">To get started, download the  [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-coreribboncommands-app"></a><span data-ttu-id="695a4-117">С помощью приложения Core.RibbonCommands</span><span class="sxs-lookup"><span data-stu-id="695a4-117">Using the Core.RibbonCommands app</span></span>
<span data-ttu-id="695a4-118"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="695a4-118"></span></span>

<span data-ttu-id="695a4-119">При запуске в этом примере кода на начальной странице в **регистрации ленты**выберите **Добавление ленты**.</span><span class="sxs-lookup"><span data-stu-id="695a4-119">When you run this code sample, on the start page in  **Register the ribbon**, choose  **Add Ribbon**.</span></span> <span data-ttu-id="695a4-120">При обновлении страницы просмотра настраиваемой ленты, выбрав **документы** > **Пользовательской вкладки**.</span><span class="sxs-lookup"><span data-stu-id="695a4-120">When the page refreshes, view the custom ribbon by choosing  **Documents** > **Custom Tab**.</span></span>

<span data-ttu-id="695a4-121">В этом примере кода определяется настраиваемая лента с помощью Models\RibbonCommands.xml.</span><span class="sxs-lookup"><span data-stu-id="695a4-121">This code sample defines a custom ribbon by using Models\RibbonCommands.xml.</span></span> <span data-ttu-id="695a4-122">RibbonCommands.xml определяет настраиваемая лента групп, кнопок и обработчики событий интерфейса пользователя для ленты.</span><span class="sxs-lookup"><span data-stu-id="695a4-122">RibbonCommands.xml defines custom ribbon groups, buttons, and UI event handlers for the ribbon.</span></span> <span data-ttu-id="695a4-123">Для получения дополнительных сведений см. [Настройка и расширение ленты сервера SharePoint 2010](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx) и [XML-ленты сервера](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="695a4-123">For more information, see [Customizing and Extending the SharePoint 2010 Server Ribbon](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx) and [Server Ribbon XML](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx).</span></span>

<span data-ttu-id="695a4-124">Настраиваемая лента отображается на всех сайтах и списков на хост-сайта, так как **RegistrationId = «0x01»** и **RegistrationType = «ContentType»**.</span><span class="sxs-lookup"><span data-stu-id="695a4-124">The custom ribbon displays on all sites and lists on the host web because  **RegistrationId="0x01"** and **RegistrationType="ContentType"**.</span></span>  <span data-ttu-id="695a4-125">**RegistrationId = «0x01»** и **RegistrationType = «ContentType»** указать, что ленты будут отображаться для всех типов в контента, наследующие от типа **«0x01»**, а находящиеся типы контента, наследующие от класса **элемента** .</span><span class="sxs-lookup"><span data-stu-id="695a4-125">**RegistrationId="0x01"** and **RegistrationType="ContentType"** specify that the ribbon will appear for all content types that inherit from type **"0x01"**, which are content types that inherit from the  **Item** class.</span></span> <span data-ttu-id="695a4-126">Чтобы применить к ленте настраиваемого типа контента, замените «0x01» с идентификатором настраиваемого типа контента элемента.</span><span class="sxs-lookup"><span data-stu-id="695a4-126">To apply your ribbon to a custom content type, replace "0x01" with your custom content type's ID.</span></span> <span data-ttu-id="695a4-127">Чтобы применить на ленте списка, измените значение RegistrationType в **список**.</span><span class="sxs-lookup"><span data-stu-id="695a4-127">To apply your ribbon to a list, change the value of RegistrationType to **List**.</span></span> 

<span data-ttu-id="695a4-128">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="695a4-128">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```XML
<?xml version="1.0" encoding="utf-8" ?>
<Elements xmlns="http://schemas.microsoft.com/sharepoint/">
  <CustomAction
    Id="CustomCustomRibbonTab"
    Location="CommandUI.Ribbon.ListView"
    RegistrationId="0x01"
    RegistrationType="ContentType"
    Sequence="100"
    >
    <CommandUIExtension>
      <CommandUIDefinitions>
        <CommandUIDefinition
          Location="Ribbon.Tabs._children">
          <Tab
            Id="Ribbon.CustomRibbonTab"
            Title="Custom Tab"
            Description="Custom Tab Description"
            Sequence="501">
            <Scaling
              Id="Ribbon.CustomRibbonTab.Scaling">
              <MaxSize
                Id="Ribbon.CustomRibbonTab.MaxSize"
                GroupId="Ribbon.CustomRibbonTab.ManageCustomGroup"
                Size="OneLargeTwoMedium"/>
              <MaxSize
                Id="Ribbon.CustomRibbonTab.TabTwoMaxSize"
                GroupId="Ribbon.CustomRibbonTab.NewOpenCustomGroup"
                Size="TwoLarge" />
              <Scale
                Id="Ribbon.CustomRibbonTab.Scaling.CustomTabScaling"
                GroupId="Ribbon.CustomRibbonTab.ManageCustomGroup"
                Size="OneLargeTwoMedium" />
              <Scale
                Id="Ribbon.CustomRibbonTab.Scaling.CustomSecondTabScaling"
                GroupId="Ribbon.CustomRibbonTab.NewOpenCustomGroup"
                Size="TwoLarge" />
            </Scaling>
            <Groups Id="Ribbon.CustomRibbonTab.Groups">
              <Group
                Id="Ribbon.CustomRibbonTab.ManageCustomGroup"
                Description="Group to Custom Functions"
                Title="Manage Item"
                Sequence="52"
                Template="Ribbon.Templates.CustomTemplate">
                <Controls Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Controls">
                  <Button
                    Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Accept"
                    Command="CustomRibbonTab.AcceptCustomCommand"
                    Sequence="15"
                    Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                    Image32by32Top="-68"
                    Image32by32Left="-272"
                    Description="Accept Item"
                    LabelText="Accept"
                    TemplateAlias="AWR" />
                  <Button
                    Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Reject"
                    Command="CustomRibbonTab.RejectCustomCommand"
                    Sequence="17"
                    Image16by16="{SiteUrl}/_layouts/15/1033/Images/formatmap16x16.png?rev=23"
                    Image16by16Top="-216"
                    Image16by16Left="-290"
                    Description="Reject Item"
                    LabelText="Reject"
                    TemplateAlias="RWR"/>
                  <Button
                    Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Verify"
                    Command="CustomRibbonTab.VerifyCustomCommand"
                    Sequence="19"
                    Image16by16="{SiteUrl}/_layouts/15/1033/Images/formatmap16x16.png?rev=23"
                    Image16by16Top="-126"
                    Image16by16Left="-144"
                    Description="Verify Item"
                    LabelText="Verify"
                    TemplateAlias="ACWR"/>
                  <Button
                   Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Close"
                   Command="CustomRibbonTab.CloseCustomCommand"
                   Sequence="19"
                   Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                   Image32by32Top="-0"
                   Image32by32Left="-34"
                   Description="Close Item"
                   LabelText="Close"
                   TemplateAlias="CWR"/>
                  <Button
                   Id="Ribbon.CustomRibbonTab.ManageCustomGroup.Copy"
                   Command="CustomRibbonTab.CopyCustomCommand"
                   Sequence="19"
                   Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                   Image32by32Top="-442"
                   Image32by32Left="-67"
                   Description="Copy Item"
                   LabelText="Copy"
                   TemplateAlias="CPWR"/>
                </Controls>
              </Group>
              <Group
                Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup"
                Description="Group to manage item"
                Title="New &amp;amp; Open"
                Sequence="53"
                Template="Ribbon.Templates.CustomTemplate">
                <Controls Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup.Controls">
                  <Button
                    Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup.New"
                    Command="CustomRibbonTab.NewCustomCommand"
                    Sequence="15"
                    Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                    Image32by32Top="-33"
                    Image32by32Left="-66"
                    Description="New Item"
                    LabelText="New"
                    TemplateAlias="LOR"/>
                  <Button
                   Id="Ribbon.CustomRibbonTab.NewOpenCustomGroup.Open"
                   Command="CustomRibbonTab.OpenCustomCommand"
                   Sequence="15"
                   Image32by32="{SiteUrl}/_layouts/15/1033/Images/formatmap32x32.png?rev=23"
                   Image32by32Top="-170"
                   Image32by32Left="-138"
                   Description="Open Item"
                   LabelText="Open"
                   TemplateAlias="LORS"/>
                </Controls>
              </Group>
            </Groups>
          </Tab>
        </CommandUIDefinition>
        <CommandUIDefinition Location="Ribbon.Templates._children">
          <GroupTemplate Id="Ribbon.Templates.CustomTemplate">
            <Layout
              Title="OneLargeTwoMedium"
              LayoutTitle="OneLargeTwoMedium">
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="AWR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="TwoRow">
                <Row>
                  <ControlRef DisplayMode="Medium" TemplateAlias="RWR" />
                </Row>
                <Row>
                  <ControlRef DisplayMode="Medium" TemplateAlias="ACWR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="CWR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="CPWR" />
                </Row>
              </Section>
            </Layout>
            <Layout
             Title="TwoLarge"
             LayoutTitle="TwoLarge">
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="LOR" />
                </Row>
              </Section>
              <Section Alignment="Top" Type="OneRow">
                <Row>
                  <ControlRef DisplayMode="Large" TemplateAlias="LORS" />
                </Row>
              </Section>
            </Layout>
          </GroupTemplate>
        </CommandUIDefinition>
      </CommandUIDefinitions>
      <CommandUIHandlers>
        <CommandUIHandler
          Command="CustomRibbonTab.AcceptCustomCommand"
          CommandAction="javascript:GetCurrentItem('AP');"/>
        <CommandUIHandler
          Command="CustomRibbonTab.RejectCustomCommand"
          CommandAction="javascript:GetCurrentItem('RJ');"/>
        <CommandUIHandler
          Command="CustomRibbonTab.VerifyCustomCommand"
          CommandAction="javascript:GetCurrentItem('AK');"/>
        <CommandUIHandler
          Command="CustomRibbonTab.NewCustomCommand"
          CommandAction="javascript:AddNewCustom();"/>
        <CommandUIHandler
          Command="CustomRibbonTab.OpenCustomCommand"
          CommandAction="javascript:OpenExistingCustom();"/>
        <CommandUIHandler
          Command="CustomRibbonTab.CloseCustomCommand"
          CommandAction="javascript:CloseExistingCustom();"/>
        <CommandUIHandler
          Command ="CustomRibbonTab.CopyCustomCommand"
          CommandAction="Javascript:CopyCustom();"/>
      </CommandUIHandlers>
    </CommandUIExtension>
  </CustomAction>
</Elements>
```

<span data-ttu-id="695a4-129">**Примечание**  Если вы используете embed технология JavaScript для реализации обработки для кнопок на ленту событий, файл JavaScript необходимо реализовать методы, определенные в элементах **CommandUIHandler** .</span><span class="sxs-lookup"><span data-stu-id="695a4-129">**Note**  If you use the embed JavaScript technique to implement event handling for your ribbons' buttons, your JavaScript file must implement the methods defined in the  **CommandUIHandler** elements.</span></span> <span data-ttu-id="695a4-130">Например вашей внедренного файла JavaScript следует реализовать функции, такие как **GetCurrentItem** и **AddNewCustom**.</span><span class="sxs-lookup"><span data-stu-id="695a4-130">For example, your embedded JavaScript file should implement functions like **GetCurrentItem** and **AddNewCustom**.</span></span>

<span data-ttu-id="695a4-131">**InitializeButton_Click** в Default.aspx выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="695a4-131">**InitializeButton_Click** in Default.aspx performs the following tasks:</span></span>

1. <span data-ttu-id="695a4-132">Вызывает **GetCustomActionXmlNode** для чтения XML-файла и возвращает объект **CustomAction** , определенный в RibbonCommands.xml.</span><span class="sxs-lookup"><span data-stu-id="695a4-132">Calls  **GetCustomActionXmlNode** to read the XML file and return the **CustomAction** object defined in RibbonCommands.xml.</span></span> <span data-ttu-id="695a4-133">Объект **CustomAction** содержит разметку для настройки ленты.</span><span class="sxs-lookup"><span data-stu-id="695a4-133">The **CustomAction** object contains the ribbon customization markup.</span></span>
    
2. <span data-ttu-id="695a4-134">Считывает несколько значений атрибутов и элементов из объекта **настраиваемое действие** .</span><span class="sxs-lookup"><span data-stu-id="695a4-134">Reads several elements and attribute values from the  **CustomAction** object.</span></span>
    
3. <span data-ttu-id="695a4-135">Преобразует в строку с именем **xmlContent**элемент **CommandUIExtension** (определяющего группы ленты, кнопок и обработчики событий интерфейса пользователя).</span><span class="sxs-lookup"><span data-stu-id="695a4-135">Converts the  **CommandUIExtension** element (which defines the ribbon groups, buttons, and UI event handlers) to a string called **xmlContent**.</span></span>
    
4.  <span data-ttu-id="695a4-136">Создание нового настраиваемого действия с помощью **clientContext.Web.UserCustomActions.Add**.</span><span class="sxs-lookup"><span data-stu-id="695a4-136">Creates a new custom action by using **clientContext.Web.UserCustomActions.Add**.</span></span>
    
5. <span data-ttu-id="695a4-137">Добавление разметки настройки ленты (в **xmlContent**) на сайте SharePoint, с помощью **CustomAction.CommandUIExtension**.</span><span class="sxs-lookup"><span data-stu-id="695a4-137">Adds the ribbon customization markup (in  **xmlContent**) to the SharePoint site using the  **CustomAction.CommandUIExtension**.</span></span>
    
6. <span data-ttu-id="695a4-138">Регистрация настраиваемой ленты путем установки для параметра **CustomAction.RegistrationId** и **CustomAction.RegistrationType** значения атрибутов объекта **CustomAction** , ознакомьтесь с разделом в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="695a4-138">Registers the custom ribbon by setting the  **CustomAction.RegistrationId** and **CustomAction.RegistrationType** to the attribute values of the **CustomAction** object read in step 2.</span></span>

```C#
 protected void InitializeButton_Click(object sender, EventArgs e) {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost()) {
                clientContext.Load(clientContext.Web, web => web.UserCustomActions);
                clientContext.ExecuteQuery();

                // Get the XML elements file and get the CommandUIExtension node.
                var customActionNode = GetCustomActionXmlNode();
                var customActionName = customActionNode.Attribute("Id").Value;
                var commandUIExtensionNode = customActionNode.Element(ns + "CommandUIExtension");
                var xmlContent = commandUIExtensionNode.ToString();
                var location = customActionNode.Attribute("Location").Value;
                var registrationId = customActionNode.Attribute("RegistrationId").Value;
                var registrationTypeString = customActionNode.Attribute("RegistrationType").Value;
                var registrationType = (UserCustomActionRegistrationType)Enum.Parse(typeof(UserCustomActionRegistrationType), registrationTypeString);

                var sequence = 1000;
                if (customActionNode.Attribute(ns + "Sequence") != null) {
                    sequence = Convert.ToInt32(customActionNode.Attribute(ns + "Sequence").Value);
                }

                // Determine if the custom action exists already.
                var customAction = clientContext.Web.UserCustomActions.FirstOrDefault(uca => uca.Name == customActionName);

                // If the custom action does not exist, create it.
                if (customAction == null) {
                    // create the ribbon.
                    customAction = clientContext.Web.UserCustomActions.Add();
                    customAction.Name = customActionName;
                }

                // Set custom action properties.
                customAction.Location = location;
                customAction.CommandUIExtension = xmlContent; // CommandUIExtension xml
                customAction.RegistrationId = registrationId;
                customAction.RegistrationType = registrationType;
                customAction.Sequence = sequence;

                customAction.Update();
                clientContext.Load(customAction);
                clientContext.ExecuteQuery();
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="695a4-139">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="695a4-139">Additional resources</span></span>
<span data-ttu-id="695a4-140"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="695a4-140"></span></span>

-  [<span data-ttu-id="695a4-141">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="695a4-141">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="695a4-142">Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript</span><span class="sxs-lookup"><span data-stu-id="695a4-142">Customize your SharePoint site UI by using JavaScript</span></span>](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
    
-  [<span data-ttu-id="695a4-143">Настройка и расширение ленты сервера SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="695a4-143">Customizing and Extending the SharePoint 2010 Server Ribbon</span></span>](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx)
    
-  [<span data-ttu-id="695a4-144">XML-кодом ленты сервера</span><span class="sxs-lookup"><span data-stu-id="695a4-144">Server Ribbon XML</span></span>](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx)
    
