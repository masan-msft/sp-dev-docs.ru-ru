---
title: Знакомство с созданием надстроек SharePoint с размещением у поставщика
description: Узнайте, как настроить среду разработки и создать свою первую надстройку SharePoint, размещаемую у поставщика.
ms.date: 03/14/2018
ms.prod: sharepoint
ms.openlocfilehash: 253dd72140a19e86d8a7d9d483dc289d0b022467
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="get-started-creating-provider-hosted-sharepoint-add-ins"></a><span data-ttu-id="03c80-103">Создание надстроек SharePoint, размещаемых у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-103">Get started creating provider-hosted SharePoint Add-ins</span></span>

<span data-ttu-id="03c80-104">Надстройки, размещаемые у поставщика, — это один из двух основных типов надстроек SharePoint. Обзор надстроек SharePoint и этих основных типов см. в статье [Надстройки SharePoint](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="03c80-104">Provider-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see [SharePoint Add-ins](sharepoint-add-ins.md).</span></span> 

<span data-ttu-id="03c80-105">Ниже представлен обзор надстроек, размещаемых у поставщика.</span><span class="sxs-lookup"><span data-stu-id="03c80-105">Here's a summary of provider-hosted add-ins:</span></span>

- <span data-ttu-id="03c80-106">К ним относятся веб-приложения, службы или базы данных, которые размещены на компьютерах, не относящихся к ферме SharePoint или подписке на SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="03c80-106">They include a web application, service, or database that is hosted externally from the SharePoint farm or SharePoint Online subscription.</span></span> <span data-ttu-id="03c80-107">Они также могут содержать компоненты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03c80-107">They may also include SharePoint components.</span></span> <span data-ttu-id="03c80-108">Вы можете размещать внешние компоненты в любом стеке веб-хостинга, включая стек LAMP (Linux, Apache, MySQL и PHP).</span><span class="sxs-lookup"><span data-stu-id="03c80-108">You can host the external components on any web-hosting stack, including the LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>
- <span data-ttu-id="03c80-109">Пользовательская бизнес-логика надстройки должна запускаться на внешних компонентах или в JavaScript пользовательских страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03c80-109">The custom business logic in the add-in has to run on either the external components or in JavaScript on custom SharePoint pages.</span></span>

<span data-ttu-id="03c80-110">В этой статье описаны следующие действия:</span><span class="sxs-lookup"><span data-stu-id="03c80-110">In this article, you'll complete the following steps:</span></span>

- <span data-ttu-id="03c80-111">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="03c80-111">Set up your dev environment</span></span>
- <span data-ttu-id="03c80-112">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="03c80-112">Create the add-in project</span></span>
- <span data-ttu-id="03c80-113">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="03c80-113">Code your add-in</span></span>

<span data-ttu-id="03c80-114"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="03c80-114"><a name="Setup"> </a></span></span>

## <a name="set-up-your-dev-environment"></a><span data-ttu-id="03c80-115">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="03c80-115">Set up your dev environment</span></span>

<span data-ttu-id="03c80-116">Настроить среду для разработки надстроек SharePoint можно разными способами. Здесь описан самый простой из них.</span><span class="sxs-lookup"><span data-stu-id="03c80-116">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way.</span></span> <span data-ttu-id="03c80-117">Информацию о настройке локальной среды и других альтернативных способах см. в [этой статье](tools-and-environments-for-developing-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="03c80-117">For alternatives, such as setting up an "all on-premises" environment, see [Tools](tools-and-environments-for-developing-sharepoint-add-ins.md).</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="03c80-118">Установите инструменты</span><span class="sxs-lookup"><span data-stu-id="03c80-118">Get the tools</span></span>

- <span data-ttu-id="03c80-119">Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это, следуя инструкциям из статьи [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="03c80-119">If you don't already have **Visual Studio** 2013 or later installed, install it by using the instructions at [Install Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="03c80-120">Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="03c80-120">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
 
- <span data-ttu-id="03c80-121">Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="03c80-121">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="03c80-122">Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03c80-122">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="03c80-123">Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="03c80-123">To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 

<span data-ttu-id="03c80-124">Сверяйтесь с [более ранними версиями Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) или другой [документацией по Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/).</span><span class="sxs-lookup"><span data-stu-id="03c80-124">Reference [earlier versions of Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) or other [Visual Studio documentation](https://docs.microsoft.com/ru-RU/visualstudio/).</span></span>

<span data-ttu-id="03c80-125"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="03c80-125"><a name="o365_signup"> </a></span></span>

### <a name="sign-up-for-an-office-365-developer-subscription"></a><span data-ttu-id="03c80-126">Получение подписки разработчика Office 365</span><span class="sxs-lookup"><span data-stu-id="03c80-126">Sign up for an Office 365 Developer Subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03c80-127">Возможно, у вас уже есть доступ к подписке разработчика Office 365:</span><span class="sxs-lookup"><span data-stu-id="03c80-127">You might already have access to an Office 365 Developer Site:</span></span> 
> - <span data-ttu-id="03c80-p105">**Вы подписчик Visual Studio (MSDN)?** Подписчики Visual Studio Ultimate и Visual Studio Premium с MSDN получают подписку разработчика Office 365 бесплатно. [Воспользуйтесь этим преимуществом сегодня](https://msdn.microsoft.com/subscriptions/manage/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="03c80-p105">**Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span></span> 
> - <span data-ttu-id="03c80-131">**У вас есть один из указанных ниже планов подписки на Office 365?**</span><span class="sxs-lookup"><span data-stu-id="03c80-131">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="03c80-132">[Создайте сайт разработчика, используя имеющуюся подписку на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="03c80-132">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="03c80-133">Чтобы получить план Office 365:</span><span class="sxs-lookup"><span data-stu-id="03c80-133">Two ways to get an Office 365 plan.</span></span> 

- <span data-ttu-id="03c80-134">[Зарегистрируйтесь в программе для разработчиков Office 365](https://developer.microsoft.com/ru-RU/office/dev-program).</span><span class="sxs-lookup"><span data-stu-id="03c80-134">Sign up for a one-year Office 365 developer account through the Office 365 Developer Program.</span></span>

- <span data-ttu-id="03c80-135">Пошаговые инструкции для принятия участия в этой программе, регистрации и настройки подписки см. в [документации по программе для разработчиков приложений для Office 365](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="03c80-135">See the [Office 365 Developer Program documentation](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program) for step-by-step instructions about how to join the Office 365 Developer Program and sign up and configure your subscription.</span></span>

### <a name="open-your-developer-site"></a><span data-ttu-id="03c80-136">Открытие сайта разработчика</span><span class="sxs-lookup"><span data-stu-id="03c80-136">Open your developer site</span></span> 
 
<span data-ttu-id="03c80-137">Перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="03c80-137">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="03c80-138">Открывшийся сайт должен выглядеть так, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="03c80-138">You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="03c80-139">Наличие на странице списка **Тестируемые надстройки** подтверждает, что веб-сайт был создан с помощью шаблона "Сайт разработчика" SharePoint.</span><span class="sxs-lookup"><span data-stu-id="03c80-139">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="03c80-140">Если вместо этого отображается обычный сайт группы, подождите несколько минут и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="03c80-140">If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>
    
> [!NOTE]
> <span data-ttu-id="03c80-141">Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03c80-141">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
<span data-ttu-id="03c80-142">**Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**</span><span class="sxs-lookup"><span data-stu-id="03c80-142">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

![Снимок экрана: домашняя страница сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)
 
<span data-ttu-id="03c80-144"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="03c80-144"></span></span>

## <a name="create-the-add-in-project"></a><span data-ttu-id="03c80-145">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="03c80-145">Create the add-in project</span></span>

1. <span data-ttu-id="03c80-146">Запустите Visual Studio, выбрав команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="03c80-146">Start Visual Studio by using the **Run as administrator** option.</span></span>
    
2. <span data-ttu-id="03c80-147">В Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="03c80-147">In Visual Studio, select **File** > **New** > **New Project**.</span></span>
    
3. <span data-ttu-id="03c80-148">В диалоговом окне **Создание проекта** последовательно разверните узлы **Visual C#** и **Office/SharePoint**, а затем выберите **Надстройки** > **Надстройка SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="03c80-148">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then select **Add-ins** > **SharePoint Add-in**.</span></span>
    
4. <span data-ttu-id="03c80-149">Назовите проект **SampleAddIn** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03c80-149">Name the project **SampleAddIn**, and then select **OK**.</span></span>
   
5. <span data-ttu-id="03c80-150">В диалоговом окне **Укажите параметры надстройки SharePoint** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="03c80-150">In the **Specify the SharePoint Add-in Settings** dialog box, do the following:</span></span>
    
   - <span data-ttu-id="03c80-151">Укажите полный URL-адрес сайта SharePoint, который вы хотите использовать для отладки надстройки.</span><span class="sxs-lookup"><span data-stu-id="03c80-151">Provide the full URL of the SharePoint site that you want to use to debug your add-in.</span></span> <span data-ttu-id="03c80-152">Это URL-адрес сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="03c80-152">This is the URL of the Developer Site.</span></span> <span data-ttu-id="03c80-153">В URL-адресе используйте протокол HTTPS, а не HTTP.</span><span class="sxs-lookup"><span data-stu-id="03c80-153">Use HTTPS, not HTTP in the URL.</span></span> <span data-ttu-id="03c80-154">В какой-то момент выполнения этой процедуры или вскоре после его завершения вам будет предложено войти на сайт.</span><span class="sxs-lookup"><span data-stu-id="03c80-154">At some point during this procedure, or shortly after it completes, you will be prompted to sign in to this site.</span></span> <span data-ttu-id="03c80-155">Это не всегда происходит в одно и то же время.</span><span class="sxs-lookup"><span data-stu-id="03c80-155">The timing of the prompt varies.</span></span> <span data-ttu-id="03c80-156">Используйте учетные данные администратора (в домене \*.onmicrosoft.com), созданные при регистрации сайта разработчика (например, Moye_Imya@contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="03c80-156">Use the administrator credentials (in the \*.onmicrosoft.com domain) that you created when you signed up for your Developer Site; for example MyName@contoso.onmicrosoft.com.</span></span>    

   - <span data-ttu-id="03c80-157">В разделе **Как требуется разместить надстройку SharePoint?** выберите элемент **Размещено у поставщика**.</span><span class="sxs-lookup"><span data-stu-id="03c80-157">Under **How do you want to host your SharePoint Add-in**, select **Provider-hosted**.</span></span>

   - <span data-ttu-id="03c80-158">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="03c80-158">Select **Next**.</span></span>  
 
6. <span data-ttu-id="03c80-159">На странице **Указание целевой версии SharePoint** выберите **SharePoint Online**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="03c80-159">On the **Specify the target SharePoint version** page, select **SharePoint Online**, and then select **Next**.</span></span>

7. <span data-ttu-id="03c80-160">В разделе **Какой тип проекта веб-приложения требуется создать?** выберите пункт **Приложение веб-форм ASP.NET**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="03c80-160">Under **Which type of web application project do you want to create?**, select **ASP.NET Web Forms Application**, and then select **Next**.</span></span>

8. <span data-ttu-id="03c80-161">В разделе **Как требуется выполнять проверку подлинности надстройки?** выберите пункт **Использовать службу контроля доступа Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="03c80-161">Under **How do you want your add-in to authenticate?**, select **Use Windows Azure Access Control Service**.</span></span>

9. <span data-ttu-id="03c80-162">В мастере нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="03c80-162">In the wizard, select **Finish**.</span></span>
    
   <span data-ttu-id="03c80-163">Основная часть операций по настройке совершается при открытии решения.</span><span class="sxs-lookup"><span data-stu-id="03c80-163">Much of the configuration is done when the solution opens.</span></span> <span data-ttu-id="03c80-164">В решении Visual Studio создаются два проекта: один для надстройки SharePoint, а другой — для веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="03c80-164">Two projects are created in the Visual Studio solution: one for the SharePoint Add-in and the other for the ASP.NET web application.</span></span>

<span data-ttu-id="03c80-165"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="03c80-165"></span></span>
## <a name="code-your-add-in"></a><span data-ttu-id="03c80-166">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="03c80-166">Code your add-in</span></span>

1. <span data-ttu-id="03c80-p110">Откройте файл AppManifest.xml. На вкладке **Разрешения** укажите область **Коллекция сайтов** и уровень разрешений **Read**.</span><span class="sxs-lookup"><span data-stu-id="03c80-p110">Open the AppManifest.xml file. On the **Permissions** tab, specify the **Site Collection** scope and the **Read** permission level.</span></span>

2. <span data-ttu-id="03c80-169">Удалите разметку в теге `<body>` файла Pages/Default.aspx веб-приложения, а затем добавьте приведенные ниже элементы управления HTML и ASP.NET в `<body>`.</span><span class="sxs-lookup"><span data-stu-id="03c80-169">Delete any markup inside the `<body>` tag of the Pages/Default.aspx file of your web application, and then add the following HTML and ASP.NET controls inside the `<body>`.</span></span> <span data-ttu-id="03c80-170">В этом примере используется элемент управления [UpdatePanel](http://msdn2.microsoft.com/ru-RU/library/bb359258) для обеспечения частичной отрисовки страницы.</span><span class="sxs-lookup"><span data-stu-id="03c80-170">This sample uses the [UpdatePanel](http://msdn2.microsoft.com/ru-RU/library/bb359258) control to enable partial page rendering.</span></span>
    
    ```HTML
     <form id="form1" runat="server">
       <div>
         <asp:ScriptManager ID="ScriptManager1" runat="server"
                 EnablePartialRendering="true" />
         <asp:UpdatePanel ID="PopulateData" runat="server" UpdateMode="Conditional">
           <ContentTemplate>      
             <table border="1" cellpadding="10">
              <tr><th><asp:LinkButton ID="CSOM" runat="server" Text="Populate Data" 
                                    OnClick="CSOM_Click" /></th></tr>
              <tr><td>

             <h2>SharePoint Site</h2>
             <asp:Label runat="server" ID="WebTitleLabel"/>

             <h2>Current User:</h2>
             <asp:Label runat="server" ID="CurrentUserLabel" />

             <h2>Site Users</h2>
             <asp:ListView ID="UserList" runat="server">     
                 <ItemTemplate >
                   <asp:Label ID="UserItem" runat="server" 
                                     Text="<%# Container.DataItem.ToString()  %>">
                   </asp:Label><br />
                </ItemTemplate>
             </asp:ListView>

             <h2>Site Lists</h2>
                    <asp:ListView ID="ListList" runat="server">
                        <ItemTemplate >
                          <asp:Label ID="ListItem" runat="server" 
                                     Text="<%# Container.DataItem.ToString()  %>">
                         </asp:Label><br />
                       </ItemTemplate>
                   </asp:ListView>
                 </td>              
               </tr>
              </table>
            </ContentTemplate>
          </asp:UpdatePanel>
       </div>
     </form>
    ```

3. <span data-ttu-id="03c80-171">Добавьте приведенные ниже объявления в файл Default.aspx.cs веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="03c80-171">Add the following declarations to the Default.aspx.cs file of your web application.</span></span>
    
    ```C#
       using Microsoft.SharePoint.Client;
       using Microsoft.IdentityModel.S2S.Tokens;
       using System.Net;
       using System.IO;
       using System.Xml;
    ```

4. <span data-ttu-id="03c80-172">В файле Default.aspx.cs веб-приложения добавьте указанные ниже переменные в класс [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1).</span><span class="sxs-lookup"><span data-stu-id="03c80-172">In the Default.aspx.cs file of your web application, add these variables inside the [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1) class.</span></span>
    
   ```C#
     SharePointContextToken contextToken;
     string accessToken;
     Uri sharepointUrl;
     string siteName;
     string currentUser;
     List<string> listOfUsers = new List<string>();
     List<string> listOfLists = new List<string>();
   ```

5. <span data-ttu-id="03c80-173">Добавьте метод `RetrieveWithCSOM` в класс [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1).</span><span class="sxs-lookup"><span data-stu-id="03c80-173">Add the `RetrieveWithCSOM` method inside the [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1) class.</span></span> <span data-ttu-id="03c80-174">Этот метод использует CSOM SharePoint, чтобы получать сведения о вашем сайте и отображать их на странице.</span><span class="sxs-lookup"><span data-stu-id="03c80-174">This method uses the SharePoint CSOM to retrieve information about your site and display it on the page.</span></span>
    
    ```C#
        // This method retrieves information about the host web by using the CSOM.
      private void RetrieveWithCSOM(string accessToken)
      {

          if (IsPostBack)
          {
              sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
          }            

          ClientContext clientContext =
                          TokenHelper.GetClientContextWithAccessToken(
                              sharepointUrl.ToString(), accessToken);

          // Load the properties for the web object.
          Web web = clientContext.Web;
          clientContext.Load(web);
          clientContext.ExecuteQuery();

          // Get the site name.
          siteName = web.Title;

          // Get the current user.
          clientContext.Load(web.CurrentUser);
          clientContext.ExecuteQuery();
          currentUser = clientContext.Web.CurrentUser.LoginName;

          // Load the lists from the Web object.
          ListCollection lists = web.Lists;
          clientContext.Load<ListCollection>(lists);
          clientContext.ExecuteQuery();

          // Load the current users from the Web object.
          UserCollection users = web.SiteUsers;
          clientContext.Load<UserCollection>(users);
          clientContext.ExecuteQuery();

          foreach (User siteUser in users)
          {
              listOfUsers.Add(siteUser.LoginName);
          }

          foreach (List list in lists)
          {
              listOfLists.Add(list.Title);
          }
      }
    ```

6. <span data-ttu-id="03c80-175">Добавьте метод `CSOM_Click` в класс [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1).</span><span class="sxs-lookup"><span data-stu-id="03c80-175">Add the `CSOM_Click` method inside the [Page](http://msdn2.microsoft.com/ru-RU/library/dfbt9et1) class.</span></span> <span data-ttu-id="03c80-176">Этот метод вызывает событие, которое происходит, когда пользователь переходит по ссылке **Заполнение данными**.</span><span class="sxs-lookup"><span data-stu-id="03c80-176">This method triggers the event that occurs when the user clicks the **Populate Data** link.</span></span>
    
    ```C#
      protected void CSOM_Click(object sender, EventArgs e)
    {
        string commandAccessToken = ((LinkButton)sender).CommandArgument;
        RetrieveWithCSOM(commandAccessToken);
        WebTitleLabel.Text = siteName;
        CurrentUserLabel.Text = currentUser;
        UserList.DataSource = listOfUsers;
        UserList.DataBind();
        ListList.DataSource = listOfLists;
        ListList.DataBind();    
     }
    ```

7. <span data-ttu-id="03c80-177">Замените существующий метод `Page_Load` указанным ниже.</span><span class="sxs-lookup"><span data-stu-id="03c80-177">Replace the existing `Page_Load` method with this one.</span></span> <span data-ttu-id="03c80-178">Метод `Page_Load` использует методы файла TokenHelper.cs, чтобы извлечь контекст из объекта `Request` и получить маркер доступа от службы контроля доступа Microsoft Azure (ACS).</span><span class="sxs-lookup"><span data-stu-id="03c80-178">The `Page_Load` method uses methods in the TokenHelper.cs file to retrieve the context from the `Request` object and get an access token from Microsoft Azure Access Control Service (ACS).</span></span>
    
    ```C#
      // The Page_load method fetches the context token and the access token. 
    // The access token is used by all of the data retrieval methods.
    protected void Page_Load(object sender, EventArgs e)
    {
         string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);

        if (contextTokenString != null)
        {
            contextToken =
                TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

            sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
            accessToken =
                        TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                        .AccessToken;

             // For simplicity, this sample assigns the access token to the button's CommandArgument property. 
             // In a production add-in, this would not be secure. The access token should be cached on the server-side.
            CSOM.CommandArgument = accessToken;
        }
        else if (!IsPostBack)
        {
            Response.Write("Could not find a context token.");
            return;
        }
    }
    ```

8. <span data-ttu-id="03c80-179">После этого файл Default.aspx.cs должен выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="03c80-179">The Default.aspx.cs file should look like this when you're finished.</span></span>
    
    ```C#
      using System;
      using System.Collections.Generic;
      using System.Linq;
      using System.Web;
      using System.Web.UI;
      using System.Web.UI.WebControls;

      using Microsoft.SharePoint.Client;
      using Microsoft.IdentityModel.S2S.Tokens;
      using System.Net;
      using System.IO;
      using System.Xml;

      namespace SampleAddInWeb
      {
          public partial class Default : System.Web.UI.Page
          {
              SharePointContextToken contextToken;
              string accessToken;
              Uri sharepointUrl;
              string siteName;
              string currentUser;
              List<string> listOfUsers = new List<string>();
              List<string> listOfLists = new List<string>();

              protected void Page_PreInit(object sender, EventArgs e)
              {
                  Uri redirectUrl;
                  switch (SharePointContextProvider.CheckRedirectionStatus(Context, out redirectUrl))
                  {
                      case RedirectionStatus.Ok:
                          return;
                      case RedirectionStatus.ShouldRedirect:
                          Response.Redirect(redirectUrl.AbsoluteUri, endResponse: true);
                          break;
                      case RedirectionStatus.CanNotRedirect:
                          Response.Write("An error occurred while processing your request.");
                          Response.End();
                          break;
                  }
              }

              protected void CSOM_Click(object sender, EventArgs e)
              {
                  string commandAccessToken = ((LinkButton)sender).CommandArgument;
                  RetrieveWithCSOM(commandAccessToken);
                  WebTitleLabel.Text = siteName;
                  CurrentUserLabel.Text = currentUser;
                  UserList.DataSource = listOfUsers;
                  UserList.DataBind();
                  ListList.DataSource = listOfLists;
                  ListList.DataBind();
              }

              // This method retrieves information about the host web by using the CSOM.
              private void RetrieveWithCSOM(string accessToken)
              {

                  if (IsPostBack)
                  {
                      sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
                  }

                  ClientContext clientContext =
                          TokenHelper.GetClientContextWithAccessToken(
                              sharepointUrl.ToString(), accessToken);

                  // Load the properties for the web object.
                  Web web = clientContext.Web;
                  clientContext.Load(web);
                  clientContext.ExecuteQuery();

                  // Get the site name.
                  siteName = web.Title;

                  // Get the current user.
                  clientContext.Load(web.CurrentUser);
                  clientContext.ExecuteQuery();
                  currentUser = clientContext.Web.CurrentUser.LoginName;

                  // Load the lists from the Web object.
                  ListCollection lists = web.Lists;
                  clientContext.Load<ListCollection>(lists);
                  clientContext.ExecuteQuery();

                  // Load the current users from the Web object.
                  UserCollection users = web.SiteUsers;
                  clientContext.Load<UserCollection>(users);
                  clientContext.ExecuteQuery();

                  foreach (User siteUser in users)
                  {
                      listOfUsers.Add(siteUser.LoginName);
                  }

                  foreach (List list in lists)
                  {
                      listOfLists.Add(list.Title);
                  }
              }

              protected void Page_Load(object sender, EventArgs e)
              {
                  string contextTokenString = 
                       TokenHelper.GetContextTokenFromRequest(Request);

                  if (contextTokenString != null)
                  {
                      contextToken =
                          TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);

                      sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);
                      accessToken =
                          TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority)
                                     .AccessToken;
                      CSOM.CommandArgument = accessToken;
                  }
                  else if (!IsPostBack)
                  {
                      Response.Write("Could not find a context token.");
                      return;
                  }
              }
          }
      }
     
    ```

9. <span data-ttu-id="03c80-180">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="03c80-180">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="03c80-181">Если отобразится окно **Оповещение системы безопасности** с предложением доверять самозаверяющему сертификату Localhost, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="03c80-181">If you see a **Security Alert** window that asks you to trust the self-signed Localhost certificate, select **Yes**.</span></span>
    
10. <span data-ttu-id="03c80-182">Выберите **Сделать доверенным** на странице подтверждения, чтобы предоставить надстройке разрешения.</span><span class="sxs-lookup"><span data-stu-id="03c80-182">Select **Trust It** on the consent page to grant permissions to the add-in.</span></span> <span data-ttu-id="03c80-183">Visual Studio установит веб-приложение в IIS Express, а затем установит надстройку на тестовом сайте SharePoint и запустит ее.</span><span class="sxs-lookup"><span data-stu-id="03c80-183">Visual Studio will install the web application to IIS Express and then install the add-in to your test SharePoint site and launch it.</span></span> <span data-ttu-id="03c80-184">Откроется страница с таблицей, как на приведенном ниже снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="03c80-184">You'll see a page that has the table shown in the following screen shot.</span></span> <span data-ttu-id="03c80-185">Чтобы просмотреть сводную информацию о сайте SharePoint, выберите **Заполнение данных**.</span><span class="sxs-lookup"><span data-stu-id="03c80-185">To see summary information about your SharePoint site, select **Populate Data**.</span></span>

   ![Страница запуска базовой надстройки с размещением у поставщика](../images/SP15_basicself-hostedapp.gif)
 

<span data-ttu-id="03c80-187"><a name="SP15createprovider_nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="03c80-187"></span></span>    
## <a name="next-steps"></a><span data-ttu-id="03c80-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03c80-188">Next steps</span></span>

<span data-ttu-id="03c80-189">Порядок дальнейших действий с надстройкой:</span><span class="sxs-lookup"><span data-stu-id="03c80-189">To create your add-ins, walk through the following steps in this order:</span></span>
 
1.  [<span data-ttu-id="03c80-190">Настройка внешнего вида надстройки SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-190">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
2.  [<span data-ttu-id="03c80-191">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-191">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in.md)
3.  [<span data-ttu-id="03c80-192">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="03c80-192">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model.md)
4.  [<span data-ttu-id="03c80-193">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-193">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
5.  [<span data-ttu-id="03c80-194">Добавление веб-части надстройки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-194">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in.md)
6.  [<span data-ttu-id="03c80-195">Обработка событий надстройки, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-195">Handle add-in events in the provider-hosted add-in</span></span>](handle-add-in-events-in-the-provider-hosted-add-in.md)
7.  [<span data-ttu-id="03c80-196">Добавление логики, выполняемой при первом запуске, в надстройку, размещаемую у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-196">Add first-run logic to the provider-hosted add-in</span></span>](add-first-run-logic-to-the-provider-hosted-add-in.md)
8.  [<span data-ttu-id="03c80-197">Программное развертывание собственной кнопки в надстройке с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-197">Programmatically deploy a custom button in the provider-hosted add-in</span></span>](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in.md)
9.  [<span data-ttu-id="03c80-198">Обработка событий элементов списков в надстройке с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="03c80-198">Handle list item events in the provider-hosted add-in</span></span>](handle-list-item-events-in-the-provider-hosted-add-in.md)




