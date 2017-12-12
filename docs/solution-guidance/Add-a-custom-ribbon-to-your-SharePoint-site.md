---
title: "Добавление настраиваемой ленты на сайт SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3f7d212ca1b263d61f17e26092618753c9daa70e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-custom-ribbon-to-your-sharepoint-site"></a>Добавление настраиваемой ленты на сайт SharePoint

Добавление или удаление настраиваемой ленты на сайте SharePoint. Добавление обработчиков событий JavaScript, с помощью JavaScript метод embed для обработки событий настраиваемой ленты.

_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_

Пример кода [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) показано, как для добавления настраиваемой ленты на сайте SharePoint. Если вы хотите используйте этого решения:

- Добавление настраиваемой ленты, группы или кнопка для сайта SharePoint или список.
    
- Отображение настраиваемой ленты для определенных типов контента сайтов и списков.

> [!NOTE] 
> В этом примере кода показано, как вызывать функции JavaScript, которые обрабатывают события, вызванные кнопок на ленте. В этом примере не предоставляет реализацию функций обработчика событий JavaScript для кнопок на ленте. Для реализации функции обработчика событий JavaScript, используйте embed технология JavaScript для внедрения функции обработчика событий JavaScript на всех страницах место, где отображается настраиваемая лента. Дополнительные сведения о внедрении JavaScript содержатся в разделе [Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.RibbonCommands](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RibbonCommands) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="using-the-coreribboncommands-app"></a>С помощью приложения Core.RibbonCommands
<a name="sectionSection1"> </a>

При запуске в этом примере кода на начальной странице в **регистрации ленты**выберите **Добавление ленты**. При обновлении страницы просмотра настраиваемой ленты, выбрав **документы** > **Пользовательской вкладки**.

В этом примере кода определяется настраиваемая лента с помощью Models\RibbonCommands.xml. RibbonCommands.xml определяет настраиваемая лента групп, кнопок и обработчики событий интерфейса пользователя для ленты. Для получения дополнительных сведений см. [Настройка и расширение ленты сервера SharePoint 2010](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx) и [XML-ленты сервера](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx).

Настраиваемая лента отображается на всех сайтах и списков на хост-сайта, так как **RegistrationId = «0x01»** и **RegistrationType = «ContentType»**.  **RegistrationId = «0x01»** и **RegistrationType = «ContentType»** указать, что ленты будут отображаться для всех типов в контента, наследующие от типа **«0x01»**, а находящиеся типы контента, наследующие от класса **элемента** . Чтобы применить к ленте настраиваемого типа контента, замените «0x01» с идентификатором настраиваемого типа контента элемента. Чтобы применить на ленте списка, измените значение RegistrationType в **список**. 

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

> [!NOTE] 
> Если вы используете embed технология JavaScript для реализации обработки для кнопок на ленту событий, файл JavaScript необходимо реализовать методы, определенные в элементах **CommandUIHandler** . Например вашей внедренного файла JavaScript следует реализовать функции, такие как **GetCurrentItem** и **AddNewCustom**.

**InitializeButton_Click** в Default.aspx выполняет следующие задачи:

1. Вызывает **GetCustomActionXmlNode** для чтения XML-файла и возвращает объект **CustomAction** , определенный в RibbonCommands.xml. Объект **CustomAction** содержит разметку для настройки ленты.
    
2. Считывает несколько значений атрибутов и элементов из объекта **настраиваемое действие** .
    
3. Преобразует в строку с именем **xmlContent**элемент **CommandUIExtension** (определяющего группы ленты, кнопок и обработчики событий интерфейса пользователя).
    
4.  Создание нового настраиваемого действия с помощью **clientContext.Web.UserCustomActions.Add**.
    
5. Добавление разметки настройки ленты (в **xmlContent**) на сайте SharePoint, с помощью **CustomAction.CommandUIExtension**.
    
6. Регистрация настраиваемой ленты путем установки для параметра **CustomAction.RegistrationId** и **CustomAction.RegistrationType** значения атрибутов объекта **CustomAction** , ознакомьтесь с разделом в шаге 2.

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
    
-  [Настройка и расширение ленты сервера SharePoint 2010](https://msdn.microsoft.com/library/office/gg552606%28v=office.14%29.aspx)
    
-  [XML-кодом ленты сервера](https://msdn.microsoft.com/library/office/ff407290%28v=office.14%29.aspx)
    
