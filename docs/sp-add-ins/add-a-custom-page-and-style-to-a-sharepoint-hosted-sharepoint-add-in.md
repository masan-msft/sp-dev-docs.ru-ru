---
title: "Добавление пользовательских страницы и стиля в надстройку SharePoint, размещаемую в SharePoint"
description: "Добавьте пользовательскую страницу, добавьте класс стиля в таблицу стилей, а затем запустите и протестируйте надстройку."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: ff0376366f4dd003bdc84935841470e00c270696
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="79497-103">Добавление собственной страницы и стиля в надстройку с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="79497-103">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="79497-104">Это седьмая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="79497-104">This is the seventh in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 
    
> [!NOTE]
> <span data-ttu-id="79497-105">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="79497-105">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="79497-106">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforePage.sln.</span><span class="sxs-lookup"><span data-stu-id="79497-106">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforePage.sln file.</span></span>

<span data-ttu-id="79497-107">Работая с этой статьей, вы добавите страницу справки в надстройку SharePoint "Employee Orientation" (Обучение сотрудников) и настроите ее так, чтобы в ней использовалась специальная таблица стилей CSS.</span><span class="sxs-lookup"><span data-stu-id="79497-107">In this article, you add a help page to the Employee Orientation SharePoint Add-in and configure it to use a custom CSS stylesheet.</span></span> 

## <a name="add-a-page"></a><span data-ttu-id="79497-108">Добавление страницы</span><span class="sxs-lookup"><span data-stu-id="79497-108">Add a page</span></span>

1. <span data-ttu-id="79497-109">В **обозревателе решений** щелкните правой кнопкой мыши папку **Pages** (Страницы) и выберите пункты **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="79497-109">In **Solution Explorer**, right-click the **Pages** folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="79497-110">Откроется диалоговое окно **Добавление нового элемента** для узла **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="79497-110">The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>

2. <span data-ttu-id="79497-111">Выберите **Page** (Страница) и задайте имя **Help.aspx**.</span><span class="sxs-lookup"><span data-stu-id="79497-111">Select **Page** and give it the name **Help.aspx**.</span></span> 

3. <span data-ttu-id="79497-112">Найдите в файле два элемента **asp:Content** и добавьте между ними указанную ниже часть кода **asp:Content**.</span><span class="sxs-lookup"><span data-stu-id="79497-112">Find the two **asp:Content** elements in the file, and add the following third **asp:Content** markup in between them.</span></span>
    
    ```HTML
      <asp:Content ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server">
        Help
      </asp:Content> 
    ```

4. <span data-ttu-id="79497-113">Найдите элемент **asp:Content** с идентификатором **PlaceholderAdditionalPageHead** и добавьте к нему указанную ниже часть кода.</span><span class="sxs-lookup"><span data-stu-id="79497-113">Find the **asp:Content** element with the ID of **PlaceholderAdditionalPageHead**, and add the following markup to it.</span></span>
    
    ```HTML
      <link rel="Stylesheet" type="text/css" href="../Content/App.css" />
    ```

5. <span data-ttu-id="79497-114">Найдите элемент **asp:Content** с идентификатором **PlaceHolderMain** и удалите из него все дочерние элементы.</span><span class="sxs-lookup"><span data-stu-id="79497-114">Find the **asp:Content** element with the ID of **PlaceHolderMain**, and remove any child elements in it.</span></span>

6. <span data-ttu-id="79497-115">Добавьте указанное ниже содержимое в тот же элемент **asp:Content**.</span><span class="sxs-lookup"><span data-stu-id="79497-115">Add the following as content to the same **asp:Content** element.</span></span>
    
    ```HTML
      <H3>Having a problem with the add-in?</H3>
      <p>Call the help line for Fabrikam Add-ins:</p>
      <p>1-555-555-5555</p>
    ```

7. <span data-ttu-id="79497-116">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="79497-116">Save and close the file.</span></span>

8. <span data-ttu-id="79497-117">Откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="79497-117">Open the Default.aspx file.</span></span>

9. <span data-ttu-id="79497-118">Найдите элемент **asp:Content** с идентификатором **PlaceHolderMain**, а затем добавьте указанную ниже часть кода в конец элемента.</span><span class="sxs-lookup"><span data-stu-id="79497-118">Find the **asp:Content** element with the ID of **PlaceHolderMain**, and then add the following markup to the end of it.</span></span> 
    
    ```HTML
      <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Pages/Help.aspx';" 
        Text="Get help for the Employee Orientation add-in" /></p>
    ```

10. <span data-ttu-id="79497-119">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="79497-119">Save and close the file.</span></span>

## <a name="add-a-style-class-to-the-stylesheet"></a><span data-ttu-id="79497-120">Добавление класса стиля в таблицу стилей</span><span class="sxs-lookup"><span data-stu-id="79497-120">Add a style class to the stylesheet</span></span>

1. <span data-ttu-id="79497-121">В **обозревателе решений** откройте файл app.css в папке **Contents** (Содержимое) и добавьте в этот файл указанную ниже строку.</span><span class="sxs-lookup"><span data-stu-id="79497-121">In **Solution Explorer**, open the app.css file in the **Contents** folder, and then add the following line to the file.</span></span>
    
    ```
      p {color: green;}
    ```

2. <span data-ttu-id="79497-122">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="79497-122">Save and close the file.</span></span>

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="79497-123">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="79497-123">Run and test the add-in</span></span>

1. <span data-ttu-id="79497-p103">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="79497-p103">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 

2. <span data-ttu-id="79497-126">Когда откроется страница надстройки, используемая по умолчанию, перейдите по ссылке **Get help for the Employee Orientation add-in** (Получить справку для надстройки Employee Orientation). Откроется страница **Help** (Справка).</span><span class="sxs-lookup"><span data-stu-id="79497-126">When the add-in's default page opens, select the **Get help for the Employee Orientation add-in** link to open the **Help** page.</span></span>
    
   <span data-ttu-id="79497-127">Откроется ваша пользовательская страница, и две строки, которые вы поместили между тегами `<p>`, будут иметь зеленый цвет.</span><span class="sxs-lookup"><span data-stu-id="79497-127">Your custom page opens and the two lines that you put in `<p>` tags are green.</span></span>

   <span data-ttu-id="79497-128">*Рис. 1. Страница "Help" (Справка)*</span><span class="sxs-lookup"><span data-stu-id="79497-128">*Figure 1. Help page*</span></span>

   ![Страница SharePoint с заголовком "Help" (Справка). Она содержит черную строку заголовка, за которой следуют две зеленые текстовые строки.](../images/2df51ab0-5b24-4a37-8b6a-6e95dbb1aeaa.PNG)

3. <span data-ttu-id="79497-131">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79497-131">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="79497-132">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать последнюю.</span><span class="sxs-lookup"><span data-stu-id="79497-132">Each time that you select F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

4. <span data-ttu-id="79497-133">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуется отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="79497-133">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="79497-134">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="79497-134">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79497-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79497-135">Next steps</span></span>
<span data-ttu-id="79497-136"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="79497-136"></span></span>

<span data-ttu-id="79497-137">В следующей статье этой серии показано [добавление пользовательской клиентской обработки в надстройку SharePoint, размещаемую в SharePoint](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="79497-137">In the next article in this series, you'll [add custom client-side rendering to a SharePoint-hosted SharePoint Add-in](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 

 

