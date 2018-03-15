---
title: "Добавление веб-части на веб-страницу сайта надстройки"
description: "Добавьте готовую веб-часть на страницу сайта надстройки SharePoint."
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 6c30611332182bc1ab5e831fab220ad8c1fb4d60
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="include-a-web-part-on-a-webpage-in-the-add-in-web"></a><span data-ttu-id="bcd2c-103">Добавление веб-части на веб-страницу сайта надстройки</span><span class="sxs-lookup"><span data-stu-id="bcd2c-103">Include a Web Part in a webpage on the add-in web</span></span>

<span data-ttu-id="bcd2c-104">Вы можете добавить готовую веб-часть на страницу сайта надстройки SharePoint, но важно делать это так, чтобы не возникало проблем с обновлением надстройки.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-104">You can include an out-of-the-box Web Part in a page in the add-in web of a SharePoint Add-in, but it is important that you do this in a way that won't cause problems if you ever need to update the add-in.</span></span>
 
<span data-ttu-id="bcd2c-105">Пример кода, иллюстрирующий представленные в этой статье рекомендации: [OfficeDev/Core.WebPartOnAppWebPage](https://github.com/SharePoint/PnP/tree/master/Samples/Core.WebPartOnAppWebPage).</span><span class="sxs-lookup"><span data-stu-id="bcd2c-105">A code sample that illustrates the guidance of this topic is at:  [OfficeDev/Core.WebPartOnAppWebPage](https://github.com/SharePoint/PnP/tree/master/Samples/Core.WebPartOnAppWebPage)</span></span>

## <a name="add-a-web-part-to-a-page"></a><span data-ttu-id="bcd2c-106">Добавление веб-части на страницу</span><span class="sxs-lookup"><span data-stu-id="bcd2c-106">Add a Web Part to a page</span></span>

1. <span data-ttu-id="bcd2c-107">Создайте в Visual Studio проект надстройки SharePoint с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-107">Create a SharePoint Add-in project in Visual Studio</span></span> <span data-ttu-id="bcd2c-108">Дополнительные сведения см. в статье [Создание надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2c-108">For the prerequisites, see  [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span></span>

2. <span data-ttu-id="bcd2c-109">Откройте ASPX-файл, в который вы хотите добавить веб-часть.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-109">Open the aspx file to which you want to add a Web Part. This topic uses Default.aspx as an example.</span></span> <span data-ttu-id="bcd2c-110">В этой статье в качестве примера используется файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-110">This topic uses Default.aspx as an example.</span></span> 
    
3. <span data-ttu-id="bcd2c-111">Добавьте класс **WebPartZone** в элемент `<asp:Content>`, в котором нужно указать веб-часть.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-111">Add a **WebPartZone** to the `<asp:Content>` element where you want the Web Part with markup.</span></span> <span data-ttu-id="bcd2c-112">Обычно его добавляют в элемент `<asp:Content>`, свойство `ContentPlaceHolderId` которого имеет значение `PlaceHolderMain`.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-112">Typically, you want to add it to the `<asp:Content>` whose `ContentPlaceHolderId` is `PlaceHolderMain`.</span></span> <span data-ttu-id="bcd2c-113">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-113">The following is an example.</span></span>
    
    ```XML
      <asp:Content ContentPlaceHolderId="PlaceHolderMain" runat="server">
        <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
          ID="HomePage1" Title="loc:full" />
      </asp:Content>
    ```

    > [!WARNING] 
    > <span data-ttu-id="bcd2c-114">В качестве дочернего элемента **WebPartZone** можно добавить элемент веб-части, такой как **<WebPartPages:XsltListViewWebPart>**.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-114">It is possible to add a Web Part element, such as **<WebPartPages:XsltListViewWebPart>** as a child of the **WebPartZone**.</span></span> <span data-ttu-id="bcd2c-115">Но мы не рекомендуем это делать в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-115">But this is generally a bad practice in a SharePoint Add-in.</span></span> <span data-ttu-id="bcd2c-116">Элемент веб-части, вставленный в ASPX-файл, может привести к сбою некоторых сценариев обновления. При этом отображается сообщение: "Веб-часть с таким идентификатором уже добавлена на эту страницу".</span><span class="sxs-lookup"><span data-stu-id="bcd2c-116">Caution It is possible to add a Web Part element, such as <WebPartPages:XsltListViewWebPart> as a child of the WebPartZone. But this is generally a bad practice in a SharePoint Add-in. If the add-in ever needs to be updated, a Web Part element inserted in the aspx file can cause the update to fail in some scenarios with the message "A web part with this ID has already been added to this page." We recommend that you add web parts to the elements manifest for the page as described later of this procedure.</span></span> <span data-ttu-id="bcd2c-117">Рекомендуем добавлять веб-части в манифест элементов для страницы, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-117">We recommend that you add web parts to the elements manifest for the page as described later in this procedure.</span></span>

4. <span data-ttu-id="bcd2c-118">Откройте файл манифеста элементов для страницы.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-118">Open the element manifest file for the page.</span></span> <span data-ttu-id="bcd2c-119">Обычно он называется elements.xml и находится в той же папке проекта, что и ASPX-файл.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-119">Open the element manifest file for the page. This is usually called elements.xml and is located in the same project folder as the aspx file.</span></span>
    
5. <span data-ttu-id="bcd2c-120">В элементе **File** для страницы добавьте дочерний элемент **AllUsersWebPart** и задайте для его атрибута **WebPartZoneID** значение зоны веб-частей, созданной на странице. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-120">In the  **File** element for the page, add a child **AllUsersWebPart** element and set its **WebPartZoneID** to the value of the Web Part zone that you created on the page as this example shows.</span></span>
    
    ```XML
      <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
        <Module Name="Pages">
          <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
            <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

            </AllUsersWebPart>
          </File>
        </Module>
      </Elements>
    ```

6. <span data-ttu-id="bcd2c-121">Добавьте дочерний элемент **CDATA** в элемент **AllUsersWebPart**, а затем добавьте дочерний элемент **webParts** в элемент **CDATA**. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-121">Add a  **CDATA** element as a child of the **AllUsersWebPart**, then add a  **webParts** element as a child of the **CDATA**, as shown in this example.</span></span> 
    
    ```XML
      <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
        <![CDATA[
          <webParts>

          </webParts>
        ]]>
      </AllUsersWebPart>
    ```

7. <span data-ttu-id="bcd2c-122">Добавьте разметку **webPart** в качестве дочернего элемента для элемента **webParts**.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-122">Add the following **webPart** markup as a child of the **webParts** element.</span></span> <span data-ttu-id="bcd2c-123">В приведенном ниже примере добавляется веб-часть **XsltListViewWebPart**.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-123">The following is an example that adds an **XsltListViewWebPart**.</span></span> <span data-ttu-id="bcd2c-124">Предполагается, что пользовательский список "Test List" входит в состав того же проекта надстройки.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-124">It assumes that a custom list called "Test List" is part of the same add-in project.</span></span> <span data-ttu-id="bcd2c-125">Информацию о том, как добавить пользовательский список на сайт надстройки, см. в статье [Создание надстройки с размещением у поставщика, которая включает в себя настраиваемый список SharePoint и тип контента](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span><span class="sxs-lookup"><span data-stu-id="bcd2c-125">Add  webPart markup as a child of the webParts element. The following is an example that adds an XsltListViewWebPart. It assumes that a custom list called "Test List" is part of the same add-in project. For information about how to add a custom list to an add-in web, see  [Create a provider-hosted add-in that includes a custom SharePoint list and content type](create-a-provider-hosted-add-in-that-includes-a-custom-sharepoint-list-and-conte.md).</span></span> 
    
    > [!NOTE] 
    > <span data-ttu-id="bcd2c-126">Обратите внимание на то, что у веб-части нет свойства ID.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-126">Note that the Web Part does not have an ID property.</span></span> <span data-ttu-id="bcd2c-127">Рекомендуем включать явный идентификатор веб-части только в двух случаях, когда это действительно необходимо. Включайте его, когда веб-часть добавляется на вики-страницу SharePoint или</span><span class="sxs-lookup"><span data-stu-id="bcd2c-127">Note   Note that the Web Part does not have an ID property. It is a best practice to include an explicit ID for the Web Part only in the two cases where it is really required: The Web Part is being added to a SharePoint wiki page. The Web Part is one of two or more Web Parts that will be connected.</span></span> <span data-ttu-id="bcd2c-128">является одной из нескольких связанных веб-частей.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-128">The Web Part is one of two or more Web Parts that will be connected.</span></span>

    ```XML
      <webParts>
      <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
        <metaData>
          <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                      Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                      PublicKeyToken=71e9bce111e9429c" />
        </metaData>
        <data>
          <properties>
            <property name="ListUrl">Lists/{TestList}</property>
            <property name="IsIncluded">True</property>
            <property name="NoDefaultStyle">True</property>
            <property name="Title">{Test List}</property>
            <property name="PageType">PAGE_NORMALVIEW</property>
            <property name="Default">False</property>
            <property name="ViewContentTypeId">0x</property>
          </properties>
        </data>
      </webPart>
    </webParts>
    ```

8. <span data-ttu-id="bcd2c-129">Нажмите клавишу F5 для отладки надстройки.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-129">Select F5 to debug the add-in.</span></span> <span data-ttu-id="bcd2c-130">Веб-часть должна появиться на странице.</span><span class="sxs-lookup"><span data-stu-id="bcd2c-130">Press F5 to debug the add-in. You should see the Web Part on the page.</span></span>
    
 
## <a name="see-also"></a><span data-ttu-id="bcd2c-131">См. также</span><span class="sxs-lookup"><span data-stu-id="bcd2c-131">See also</span></span>
<span data-ttu-id="bcd2c-132"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bcd2c-132"></span></span>

-  [<span data-ttu-id="bcd2c-133">Создание компонентов взаимодействия с пользователем в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bcd2c-133">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
