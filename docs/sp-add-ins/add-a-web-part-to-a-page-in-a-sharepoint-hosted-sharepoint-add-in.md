---
title: "Добавление веб-части на страницу в надстройке SharePoint, размещаемой в SharePoint"
description: "Добавьте веб-часть на страницу, а затем запустите и протестируйте надстройку."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 335e68f24e7bc4ba9bd8a7777b48473542e8fc26
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="44824-103">Добавление веб-части на страницу в надстройке с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="44824-103">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="44824-104">Это пятая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="44824-104">This is the fifth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 
    
> [!NOTE]
> <span data-ttu-id="44824-105">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="44824-105">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="44824-106">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeWebPart.sln.</span><span class="sxs-lookup"><span data-stu-id="44824-106">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeWebPart.sln file.</span></span>

<span data-ttu-id="44824-107">В этой статье рассказывается, как добавить веб-часть на страницу, используемую по умолчанию, в надстройке SharePoint Employee Orientation (Обучение сотрудников).</span><span class="sxs-lookup"><span data-stu-id="44824-107">In this article, you add a Web Part to the default page of the Employee Orientation SharePoint Add-in.</span></span>

## <a name="add-a-web-part-to-a-page"></a><span data-ttu-id="44824-108">Добавление веб-части на страницу</span><span class="sxs-lookup"><span data-stu-id="44824-108">Add a Web Part to a page</span></span>

1. <span data-ttu-id="44824-109">В **обозревателе решений** откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="44824-109">In **Solution Explorer**, open the Default.aspx file.</span></span> 

2. <span data-ttu-id="44824-110">Так как мы будем добавлять веб-часть представления списка на страницу, на которой отображается список New Employees in Seattle (Новые сотрудники в Сиэтле), нам больше не нужна ссылка на страницу представления списка для списка.</span><span class="sxs-lookup"><span data-stu-id="44824-110">Because we'll be adding a list view Web Part to the page that surfaces the New Employees in Seattle list, we no longer need a link to the list view page for the list.</span></span> <span data-ttu-id="44824-111">Удалите элемент **<asp:HyperLink>** из элемента **<asp:Content>**, у которого параметр **ContentPlaceHolderId** имеет значение `PlaceHolderMain`.</span><span class="sxs-lookup"><span data-stu-id="44824-111">Remove the **<asp:HyperLink>** element from the **<asp:Content>** element whose **ContentPlaceHolderId** is `PlaceHolderMain`.</span></span> 

3. <span data-ttu-id="44824-112">Внутри того же элемента **<asp:Content>** добавьте указанный ниже элемент **WebPartZone**.</span><span class="sxs-lookup"><span data-stu-id="44824-112">Inside the same **<asp:Content>** element, add the following **WebPartZone**.</span></span> 
    
    ```XML
      <WebPartPages:WebPartZone runat="server" FrameType="TitleBarOnly" 
          ID="HomePage1" Title="loc:full" />
    ```

4. <span data-ttu-id="44824-113">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="44824-113">Save and close the file.</span></span>

5. <span data-ttu-id="44824-114">В **обозревателе решений** откройте файл elements.xml страницы в узле **Страницы**.</span><span class="sxs-lookup"><span data-stu-id="44824-114">In **Solution Explorer**, open the elements.xml file for the page in the **Pages** node.</span></span>

6. <span data-ttu-id="44824-115">Если элемент **File** — самозакрывающийся, удалите из него символ / и добавьте закрывающий тег `</File>`.</span><span class="sxs-lookup"><span data-stu-id="44824-115">If the **File** element is self-closing, remove the "/" character from it and add the end tag `</File>`.</span></span>

7. <span data-ttu-id="44824-116">В элементе **File** добавьте дочерний элемент **AllUsersWebPart**, а для его атрибута **WebPartZoneID** укажите идентификатор зоны веб-частей, созданной на странице.</span><span class="sxs-lookup"><span data-stu-id="44824-116">In the **File** element, add a child **AllUsersWebPart** element, and set its **WebPartZoneID** to the ID of the Web Part zone that you created on the page.</span></span> <span data-ttu-id="44824-117">Теперь содержимое файла должно выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="44824-117">The file's contents should now look like the following.</span></span> <span data-ttu-id="44824-118">Эта разметка сообщает SharePoint, что необходимо вставить элемент **AllUsersWebPart** в зону веб-частей с именем HomePage1 (Домашняя страница 1).</span><span class="sxs-lookup"><span data-stu-id="44824-118">This markup tells SharePoint to insert an **AllUsersWebPart** into the Web Part zone that is named "HomePage1".</span></span>
    
    ```
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Module Name="Pages">
        <File Path="Pages\Default.aspx" Url="Pages/Default.aspx" ReplaceContent="TRUE" >
          <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">

          </AllUsersWebPart>
        </File>
      </Module>
    </Elements>

    ```

8. <span data-ttu-id="44824-119">Добавьте элемент **CDATA** в качестве дочернего элемента для элемента **AllUsersWebPart**. Затем добавьте элемент **webParts** в качестве дочернего элемента для элемента **CDATA**, как показано в разметке ниже.</span><span class="sxs-lookup"><span data-stu-id="44824-119">Add a **CDATA** element as a child of the **AllUsersWebPart**, and then add a **webParts** element as a child of the **CDATA**, as shown in the following markup.</span></span> 
    
    ```
    <AllUsersWebPart WebPartZoneID="HomePage1" WebPartOrder="1">
      <![CDATA[
        <webParts>

        </webParts>
      ]]>
    </AllUsersWebPart>
    ```

9. <span data-ttu-id="44824-120">Добавьте указанную ниже разметку **webPart** в качестве дочернего элемента для элемента **webParts**.</span><span class="sxs-lookup"><span data-stu-id="44824-120">Add the following **webPart** markup as a child of the **webParts** element.</span></span> <span data-ttu-id="44824-121">Эта разметка добавляет элемент **XsltListViewWebPart** и сообщает веб-части, что необходимо отобразить список **New Employees in Seattle** (Новые сотрудники в Сиэтле).</span><span class="sxs-lookup"><span data-stu-id="44824-121">This markup adds an **XsltListViewWebPart** and tells the Web Part to show the **New Employees in Seattle** list.</span></span> <span data-ttu-id="44824-122">Обратите внимание, что для свойства **ViewContentTypeId** используется значение `0x`, а не фактический идентификатор типа контента **NewEmployee**.</span><span class="sxs-lookup"><span data-stu-id="44824-122">Note that the **ViewContentTypeId** property value is just `0x`, not the actual ID of the **NewEmployee** content type.</span></span>
    
    ```
      <webPart xmlns="http://schemas.microsoft.com/WebPart/v3">
        <metaData>
          <type name="Microsoft.SharePoint.WebPartPages.XsltListViewWebPart, 
                       Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, 
                       PublicKeyToken=71e9bce111e9429c" />
        </metaData>
        <data>
          <properties>
            <property name="ListUrl">Lists/NewEmployeesInSeattle</property>
            <property name="IsIncluded">True</property>
            <property name="NoDefaultStyle">True</property>
            <property name="Title">New Employees in Seattle</property>
            <property name="PageType">PAGE_NORMALVIEW</property>
            <property name="Default">False</property>
            <property name="ViewContentTypeId">0x</property>
          </properties>
        </data>
      </webPart>
    ```


## <a name="run-and-test-the-add-in"></a><span data-ttu-id="44824-123">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="44824-123">Run and test the add-in</span></span>

1. <span data-ttu-id="44824-p105">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="44824-p105">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 

2. <span data-ttu-id="44824-126">Когда откроется страница надстройки, используемая по умолчанию, на ней будет веб-часть представления списка и, соответственно, будет отображаться список.</span><span class="sxs-lookup"><span data-stu-id="44824-126">When the add-in's default page opens, the list view Web Part is on it and the list is displayed.</span></span> 
    
   <span data-ttu-id="44824-127">*Рис. 1. Страница, используемая по умолчанию, с веб-частью представления списка*</span><span class="sxs-lookup"><span data-stu-id="44824-127">*Figure 1. Default page with list view Web part*</span></span>

   ![Страница надстройки, используемая по умолчанию, на которой в веб-части отображается список New Employees in Seattle (Новые сотрудники в Сиэтле).](../images/31e8e4b1-e2e6-416b-b360-9979a1f16fc7.PNG)

3. <span data-ttu-id="44824-129">Попробуйте добавлять к списку новые элементы и редактировать существующие.</span><span class="sxs-lookup"><span data-stu-id="44824-129">Try adding new items to the list and editing existing items.</span></span>

4. <span data-ttu-id="44824-p106">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="44824-p106">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

5. <span data-ttu-id="44824-132">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуется отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="44824-132">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="44824-133">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="44824-133">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="44824-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44824-134">Next steps</span></span> 
<span data-ttu-id="44824-135"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="44824-135"></span></span>

<span data-ttu-id="44824-136">В следующей статье этой серии вы [добавите рабочий процесс в надстройку SharePoint, размещаемую в SharePoint](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="44824-136">In the next article in this series, you'll [add a workflow to a SharePoint-hosted SharePoint Add-in](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 

 

