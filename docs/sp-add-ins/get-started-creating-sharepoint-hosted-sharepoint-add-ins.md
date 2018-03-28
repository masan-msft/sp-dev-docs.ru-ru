---
title: Знакомство с созданием надстроек SharePoint с размещением в SharePoint
description: Узнайте, как настроить среду разработки и создать свою первую надстройку SharePoint с размещением в SharePoint.
ms.date: 03/14/2018
ms.prod: sharepoint
ms.openlocfilehash: 24cdfe50698d97021c406bdf0a27110ec4dce904
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="09d66-103">Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-103">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>

<span data-ttu-id="09d66-104">Надстройки с размещением в SharePoint — это один из двух основных типов надстроек SharePoint. Обзор надстроек SharePoint и этих основных типов см. в статье [Надстройки SharePoint](sharepoint-add-ins.md). Ниже представлен обзор надстроек с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09d66-104">SharePoint-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see [SharePoint Add-ins](sharepoint-add-ins.md). Here's a summary of SharePoint-hosted add-ins:</span></span>

- <span data-ttu-id="09d66-105">Они содержат списки SharePoint, веб-части, рабочие процессы, пользовательские страницы и другие компоненты, каждый из которых установлен на дочернем сайте (сайте надстройки) того веб-сайта SharePoint, на котором установлена надстройка.</span><span class="sxs-lookup"><span data-stu-id="09d66-105">They contain SharePoint lists, Web Parts, workflows, custom pages, and other components, all of which are installed on a subweb, called the add-in web, of the SharePoint website where the add-in is installed.</span></span>
- <span data-ttu-id="09d66-106">Единственный код, который они содержат, — JavaScript пользовательских страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09d66-106">The only code they have is JavaScript on custom SharePoint pages.</span></span>

<span data-ttu-id="09d66-107">В этой статье описываются перечисленные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="09d66-107">In this article, you'll complete the following steps:</span></span>

- <span data-ttu-id="09d66-108">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="09d66-108">Set up your dev environment</span></span>
- <span data-ttu-id="09d66-109">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="09d66-109">Create the add-in project</span></span>
- <span data-ttu-id="09d66-110">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="09d66-110">Code your add-in</span></span>
- <span data-ttu-id="09d66-111">Запуск надстройки и тестирование списка</span><span class="sxs-lookup"><span data-stu-id="09d66-111">Run the add-in and test the list</span></span>

<span data-ttu-id="09d66-112"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="09d66-112"><a name="Setup"> </a></span></span>

## <a name="set-up-your-dev-environment"></a><span data-ttu-id="09d66-113">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="09d66-113">Set up your dev environment</span></span>

<span data-ttu-id="09d66-114">Существует множество способов настройки среды разработки для надстроек SharePoint. Здесь приведен самый простой из них.</span><span class="sxs-lookup"><span data-stu-id="09d66-114">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="09d66-115">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="09d66-115">Get the tools</span></span>

- <span data-ttu-id="09d66-116">Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это, следуя инструкциям из статьи [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="09d66-116">If you don't already have **Visual Studio** 2013 or later installed, install it by using the instructions at [Install Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="09d66-117">Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="09d66-117">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
 
- <span data-ttu-id="09d66-118">Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="09d66-118">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="09d66-119">Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09d66-119">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="09d66-120">Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="09d66-120">To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 

<span data-ttu-id="09d66-121">Сверяйтесь с [более ранними версиями Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) или другой [документацией по Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/).</span><span class="sxs-lookup"><span data-stu-id="09d66-121">Reference [earlier versions of Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) or other [Visual Studio documentation](https://docs.microsoft.com/ru-RU/visualstudio/).</span></span>

<span data-ttu-id="09d66-122"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="09d66-122"><a name="o365_signup"> </a></span></span>

### <a name="sign-up-for-an-office-365-developer-subscription"></a><span data-ttu-id="09d66-123">Получение подписки разработчика Office 365</span><span class="sxs-lookup"><span data-stu-id="09d66-123">Sign up for an Office 365 Developer Subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09d66-124">Возможно, у вас уже есть доступ к подписке разработчика Office 365:</span><span class="sxs-lookup"><span data-stu-id="09d66-124">You might already have access to an Office 365 Developer Site:</span></span> 
> - <span data-ttu-id="09d66-p103">**Вы подписчик Visual Studio (MSDN)?** Подписчики Visual Studio Ultimate и Visual Studio Premium с MSDN получают подписку разработчика Office 365 бесплатно. [Воспользуйтесь этим преимуществом сегодня](https://msdn.microsoft.com/subscriptions/manage/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="09d66-p103">**Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span></span> 
> - <span data-ttu-id="09d66-128">**У вас есть один из указанных ниже планов подписки на Office 365?**</span><span class="sxs-lookup"><span data-stu-id="09d66-128">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="09d66-129">[Создайте сайт разработчика, используя имеющуюся подписку на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="09d66-129">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="09d66-130">Чтобы получить план Office 365:</span><span class="sxs-lookup"><span data-stu-id="09d66-130">Two ways to get an Office 365 plan.</span></span> 

- <span data-ttu-id="09d66-131">[Зарегистрируйтесь в программе для разработчиков Office 365](https://developer.microsoft.com/ru-RU/office/dev-program).</span><span class="sxs-lookup"><span data-stu-id="09d66-131">Sign up for a one-year Office 365 developer account through the Office 365 Developer Program.</span></span>

- <span data-ttu-id="09d66-132">Пошаговые инструкции для принятия участия в этой программе, регистрации и настройки подписки см. в [документации по программе для разработчиков приложений для Office 365](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="09d66-132">See the [Office 365 Developer Program documentation](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program) for step-by-step instructions about how to join the Office 365 Developer Program and sign up and configure your subscription.</span></span>

### <a name="open-your-developer-site"></a><span data-ttu-id="09d66-133">Открытие сайта разработчика</span><span class="sxs-lookup"><span data-stu-id="09d66-133">Open your developer site</span></span> 
 
<span data-ttu-id="09d66-134">Перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="09d66-134">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="09d66-135">Открывшийся сайт должен выглядеть так, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="09d66-135">You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="09d66-136">Наличие на странице списка **Тестируемые надстройки** подтверждает, что веб-сайт был создан с помощью шаблона "Сайт разработчика" SharePoint.</span><span class="sxs-lookup"><span data-stu-id="09d66-136">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="09d66-137">Если вместо этого отображается обычный сайт группы, подождите несколько минут и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="09d66-137">If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>
    
> [!NOTE]
> <span data-ttu-id="09d66-138">Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09d66-138">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>

<span data-ttu-id="09d66-139">**Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**</span><span class="sxs-lookup"><span data-stu-id="09d66-139">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

![Снимок экрана: домашняя страница сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)


<span data-ttu-id="09d66-141"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="09d66-141"></span></span>

## <a name="create-the-add-in-project"></a><span data-ttu-id="09d66-142">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="09d66-142">Create the add-in project</span></span>

1. <span data-ttu-id="09d66-143">Запустите Visual Studio, выбрав команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="09d66-143">Start Visual Studio by using the **Run as administrator** option.</span></span>

2. <span data-ttu-id="09d66-144">В Visual Studio выберите пункты **Файл** > **Создать** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="09d66-144">In Visual Studio, select **File** > **New** > **New Project**.</span></span>
 
3. <span data-ttu-id="09d66-145">В диалоговом окне **Новый проект** последовательно разверните узлы **Visual C#** и **Office/SharePoint**, а затем выберите элементы **Надстройки** > **Надстройка для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="09d66-145">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then select **Add-ins** > **Add-in for SharePoint**.</span></span>

4. <span data-ttu-id="09d66-146">Присвойте проекту имя **EmployeeOrientation**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="09d66-146">Name the project **EmployeeOrientation**, and then select **OK**.</span></span>

5. <span data-ttu-id="09d66-147">В диалоговом окне **Настройка параметров надстроек SharePoint** укажите полный URL-адрес сайта SharePoint, который требуется использовать для отладки надстройки.</span><span class="sxs-lookup"><span data-stu-id="09d66-147">In the **Specify the Add-in for SharePoint Settings** dialog box, provide the full URL of the SharePoint site that you want to use to debug your add-in.</span></span> <span data-ttu-id="09d66-148">Это URL-адрес сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="09d66-148">This is the URL of the Developer Site.</span></span> <span data-ttu-id="09d66-149">В URL-адресе используйте протокол HTTPS, а не HTTP. В разделе **Как требуется разместить надстройку SharePoint?**, выберите **Размещено в SharePoint**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="09d66-149">(Use HTTPS, not HTTP in the URL.) Under **How do you want to host your SharePoint Add-in**, select  **SharePoint-hosted**, and then select **Finish**.</span></span>

6. <span data-ttu-id="09d66-150">Вам может быть предложено войти на сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="09d66-150">You may be prompted to sign in to your Developer Site.</span></span> <span data-ttu-id="09d66-151">В таком случае используйте учетные данные администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="09d66-151">If so, use your subscription administrator's credentials.</span></span>

7. <span data-ttu-id="09d66-152">После создания проекта откройте файл **/Pages/Default.aspx** из корневой папки проекта.</span><span class="sxs-lookup"><span data-stu-id="09d66-152">After the project is created, open the file **/Pages/Default.aspx** from the root of the project.</span></span> <span data-ttu-id="09d66-153">Помимо прочего, этот созданный файл загружает один или оба сценария, размещенные в SharePoint: sp.runtime.js и sp.js.</span><span class="sxs-lookup"><span data-stu-id="09d66-153">Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js.</span></span> <span data-ttu-id="09d66-154">Разметку для загрузки этих файлов можно найти в элементе управления **Content** в верхней части файла с идентификатором **PlaceHolderAdditionalPageHead**.</span><span class="sxs-lookup"><span data-stu-id="09d66-154">The markup for loading these files is in the **Content** control near the top of the file that has the ID **PlaceHolderAdditionalPageHead**.</span></span> <span data-ttu-id="09d66-155">Разметка зависит от используемой версии **Инструментов разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="09d66-155">The markup varies depending on the version of **Microsoft Office Developer Tools for Visual Studio** that you are using.</span></span> <span data-ttu-id="09d66-156">В руководствах из этой серии необходимо загружать оба файла с обычными HTML-тегами **\<script\>**, а не с тегами **\<SharePoint:ScriptLink\>**.</span><span class="sxs-lookup"><span data-stu-id="09d66-156">This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML **\<script\>** tags, not **\<SharePoint:ScriptLink\>** tags.</span></span> 

    <span data-ttu-id="09d66-157">Убедитесь, что указанные ниже строки присутствуют в элементе управления **PlaceHolderAdditionalPageHead** *над* строкой `<meta name="WebPartPageExpansion" content="full" />`.</span><span class="sxs-lookup"><span data-stu-id="09d66-157">Ensure that the following lines are in the **PlaceHolderAdditionalPageHead** control, *just above*  the line `<meta name="WebPartPageExpansion" content="full" />`:</span></span>
    
    ```
      <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
      <script type="text/javascript" src="/_layouts/15/sp.js"></script> 
    ```

8. <span data-ttu-id="09d66-158">Проверьте файл на наличие другой разметки, загружающей один или оба файла сценариев, и удалите ее.</span><span class="sxs-lookup"><span data-stu-id="09d66-158">Search the file for any other markup that also loads one or the other of these files and remove the redundant markup.</span></span> <span data-ttu-id="09d66-159">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="09d66-159">Save and close the file.</span></span>

<span data-ttu-id="09d66-160"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="09d66-160"></span></span>
## <a name="code-your-add-in"></a><span data-ttu-id="09d66-161">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="09d66-161">Code your add-in</span></span>

<span data-ttu-id="09d66-162">Для вашей первой надстройки SharePoint с размещением в SharePoint мы включим классическое расширение SharePoint: настраиваемый список и его экземпляр.</span><span class="sxs-lookup"><span data-stu-id="09d66-162">For your first SharePoint-hosted SharePoint Add-in, we'll include the classic SharePoint extension: a custom list and list instance.</span></span>

1. <span data-ttu-id="09d66-163">В **обозревателе решений** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="09d66-163">In **Solution Explorer**, open the AppManifest.xml file.</span></span>

2. <span data-ttu-id="09d66-164">Когда откроется конструктор манифеста, измените значение в поле **Title**, на **Адаптация сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="09d66-164">When the manifest designer opens, add a space between the words in the **Title** field so that it reads **Employee Orientation**.</span></span> <span data-ttu-id="09d66-165">*Не* меняйте значение в поле **Name**.</span><span class="sxs-lookup"><span data-stu-id="09d66-165">(Do  *not* change the **Name** field.)</span></span>

3. <span data-ttu-id="09d66-166">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="09d66-166">Save and close the file.</span></span>

4. <span data-ttu-id="09d66-167">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="09d66-167">Right-click the project in **Solution Explorer** and select **Add** > **New Folder**.</span></span> <span data-ttu-id="09d66-168">Назовите папку Lists.</span><span class="sxs-lookup"><span data-stu-id="09d66-168">Name the folder Lists.</span></span>

5. <span data-ttu-id="09d66-169">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="09d66-169">Right-click the new folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="09d66-170">В узле **Office/SharePoint** откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="09d66-170">The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>

6. <span data-ttu-id="09d66-171">Выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="09d66-171">Select **List**.</span></span> <span data-ttu-id="09d66-172">Задайте для него имя **NewEmployeeOrientation** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="09d66-172">Give it the name **NewEmployeeOrientation**, and then select **Add**.</span></span> 
 
7. <span data-ttu-id="09d66-173">На странице **Выберите параметры списка** в мастере настройки SharePoint оставьте заданное по умолчанию отображаемое имя списка **NewEmployeeOrientation**, нажмите кнопку **Создать настраиваемый шаблон списка и экземпляр списка на его основе** и в раскрывающемся списке выберите **По умолчанию (настраиваемый список)**. Затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="09d66-173">On the **Choose List Settings** page of the SharePoint Customization Wizard, leave the list display name at the default **NewEmployeeOrientation**, select the **Create a customizable list template and a list instance of it** option button, select **Default (Custom List)** on the drop-down list, and then select **Finish**.</span></span>

8. <span data-ttu-id="09d66-p114">Мастер создаст шаблон списка **NewEmployeeOrientation** с экземпляром дочернего списка под названием **NewEmployeeOrientationInstance**. При этом может открыться конструктор списков, который понадобится на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="09d66-p114">The wizard creates a **NewEmployeeOrientation** list template with a child list instance named **NewEmployeeOrientationInstance**. A list designer may open. It is used in a later step.</span></span>

9. <span data-ttu-id="09d66-177">Разверните узел **NewEmployeeOrientationInstance** в **обозревателе решений**, если вы еще не сделали этого, чтобы четко отличать файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка, от файла elements.xml, который представляет собой дочерний элемент *шаблона* списка.</span><span class="sxs-lookup"><span data-stu-id="09d66-177">Expand the **NewEmployeeOrientationInstance** node in **Solution Explorer**, if it isn't already, so that you can clearly distinguish the elements.xml file that is a child of the list *instance* from the elements.xml file that is a child of the list *template*.</span></span>

    ![Содержимое папки с дочерним шаблоном NewEmployeeOrientation, у которого есть три дочерних элемента (NewEmployeeOrientationInstance, файл elements.xml и файл schema.xml). У экземпляра есть дочерний элемент elements.xml.](../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)

10. <span data-ttu-id="09d66-180">Откройте дочерний элемент elements.xml в шаблоне списка **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="09d66-180">Open the elements.xml child of the **NewEmployeeOrientation** list template.</span></span>

11. <span data-ttu-id="09d66-181">Измените значение атрибута **DisplayName** (не атрибута **Name**), чтобы имя стало более понятным: "Обучение новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="09d66-181">Add spaces to the **DisplayName** attribute (not the **Name** attribute) to make it friendlier: "New Employee Orientation."</span></span>

12. <span data-ttu-id="09d66-182">Задайте для атрибута **Description** значение "Сведения об адаптации новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="09d66-182">Set the **Description** attribute to "Orientation information about new employees."</span></span>

13. <span data-ttu-id="09d66-183">Оставьте для других атрибутов значения по умолчанию, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="09d66-183">Leave all other attributes at their default, save the file, and close it.</span></span>

14. <span data-ttu-id="09d66-184">Если конструктор списков не открыт, выберите узел **NewEmployeeOrientation** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="09d66-184">If the list designer is not open, select the **NewEmployeeOrientation** node in **Solution Explorer**.</span></span>

15. <span data-ttu-id="09d66-185">Откройте вкладку **Список** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="09d66-185">Open the **List** tab of the designer.</span></span> <span data-ttu-id="09d66-186">Эта вкладка используется для установки определенных значений *экземпляра* (не *шаблона*) списка, но она содержит некоторые значения по умолчанию, унаследованные от шаблона.</span><span class="sxs-lookup"><span data-stu-id="09d66-186">This tab is used to set certain values for the list *instance*, not the list *template*, but it has some default values that it inherited from the template.</span></span>

16. <span data-ttu-id="09d66-187">Замените значения на вкладке **Список** на следующие:</span><span class="sxs-lookup"><span data-stu-id="09d66-187">Change the values on the **List** tab to the following:</span></span>
    
    -  <span data-ttu-id="09d66-188">**Заголовок**: "Новые сотрудники в Сиэтле".</span><span class="sxs-lookup"><span data-stu-id="09d66-188">**Title**: New Employees in Seattle</span></span>
    -  <span data-ttu-id="09d66-189">**URL-адрес списка**: Lists/NewEmployeesInSeattle.</span><span class="sxs-lookup"><span data-stu-id="09d66-189">**List URL**: Lists/NewEmployeesInSeattle</span></span>
    -  <span data-ttu-id="09d66-190">**Описание**: "Новые сотрудники в Сиэтле".</span><span class="sxs-lookup"><span data-stu-id="09d66-190">**Description**: The new employees in Seattle</span></span>

17. <span data-ttu-id="09d66-191">Оставьте установленные по умолчанию флажки и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="09d66-191">Leave the check boxes at their default status, save the file, and then close the designer.</span></span>

18. <span data-ttu-id="09d66-192">В **обозревателе решений** может отображаться старое имя экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="09d66-192">The list instance may have its old name in **Solution Explorer**.</span></span> <span data-ttu-id="09d66-193">В таком случае откройте контекстное меню узла **NewEmployeeOrientationInstance**, выберите пункт **Переименовать** и измените имя на **NewEmployeesInSeattle**.</span><span class="sxs-lookup"><span data-stu-id="09d66-193">If so, open the shortcut menu for **NewEmployeeOrientationInstance**, select **Rename**, and change the name to **NewEmployeesInSeattle**.</span></span>

19. <span data-ttu-id="09d66-194">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="09d66-194">Open the schema.xml file.</span></span>

20. <span data-ttu-id="09d66-195">В элементе **View**, значение **BaseViewID** которого равно 0, замените имеющийся элемент **ViewFields** на приведенную ниже часть кода. Используйте именно этот GUID для параметра **FieldRef** с именем `Title`.</span><span class="sxs-lookup"><span data-stu-id="09d66-195">In the **View** element whose **BaseViewID** value is "0", replace the existing **ViewFields** element with the following markup (use exactly this GUID for the **FieldRef** named `Title`).</span></span> <span data-ttu-id="09d66-196">В этом автоматически созданном файле schema.xml могут встречаться разрывы строк в странных местах.</span><span class="sxs-lookup"><span data-stu-id="09d66-196">Line breaks may come at odd places in this autogenerated schema.xml file.</span></span> <span data-ttu-id="09d66-197">Убедитесь, что вы нашли соответствующие начальный и конечный теги элемента **ViewFields**.</span><span class="sxs-lookup"><span data-stu-id="09d66-197">Be sure you have found the matching begin and end tags for the **ViewFields** element.</span></span> <span data-ttu-id="09d66-198">Добавьте разрывы строк для удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="09d66-198">Add line breaks to improve readability.</span></span> 

    ```
      <ViewFields>
         <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
      </ViewFields>
    ```

21. <span data-ttu-id="09d66-199">Не закрывая файл schema.xml, в элементе **View**, значение **BaseViewID** которого равно 1, замените элемент **ViewFields** на приведенную ниже разметку. Используйте именно этот GUID для параметра **FieldRef** с именем `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="09d66-199">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", replace the existing **ViewFields** element with the following markup (use exactly this GUID for the **FieldRef** named `LinkTitle`).</span></span>
    
    ```
      <ViewFields>
         <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      </ViewFields>
    ```

22. <span data-ttu-id="09d66-200">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="09d66-200">Save and close the schema.xml file.</span></span>

23. <span data-ttu-id="09d66-201">Откройте файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка **NewEmployeesInSeattle** (а не *шаблона* списка **NewEmployeeOrientation**).</span><span class="sxs-lookup"><span data-stu-id="09d66-201">Open the elements.xml file that is a child of the list *instance* **NewEmployeesInSeattle** (not the elements.xml that is a child of the list *template* **NewEmployeeOrientation**).</span></span>

24. <span data-ttu-id="09d66-p119">В этом файле заполните список начальными данными. Для этого добавьте следующую разметку элемента **Data** в качестве дочернего элемента **ListInstance**.</span><span class="sxs-lookup"><span data-stu-id="09d66-p119">In this file, populate the list with some initial data. You do this by adding the following **Data** element markup as a child element of the **ListInstance** element.</span></span>
    
    ```
      <Data>
      <Rows>
        <Row>
          <Field Name="Title">Tom Higginbotham</Field>
        </Row>
        <Row>
          <Field Name="Title">Satomi Hayakawa</Field>
        </Row>
        <Row>
          <Field Name="Title">Cassi Hicks</Field>
        </Row>
        <Row>
          <Field Name="Title">Lertchai Treetawatchaiwong</Field>
        </Row>
      </Rows>
    </Data>
    ```

25. <span data-ttu-id="09d66-204">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="09d66-204">Save and close the file.</span></span>

26. <span data-ttu-id="09d66-205">В **обозревателе решений** дважды щелкните элемент **Компонент1**, чтобы открыть конструктор компонентов.</span><span class="sxs-lookup"><span data-stu-id="09d66-205">In **Solution Explorer**, double-click **Feature1** to open the Feature designer.</span></span> <span data-ttu-id="09d66-206">В конструкторе задайте для параметра **Название** значение **Компоненты для адаптации новый сотрудников**, а для параметра **Описание** — значение **Списки и другие компоненты для адаптации сотрудников в компании**.</span><span class="sxs-lookup"><span data-stu-id="09d66-206">In the designer, set the **Title** to **New Employee Orientation Components** and set the **Description** to **Lists and other components for getting employees oriented to the company**.</span></span> <span data-ttu-id="09d66-207">Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="09d66-207">Save the file, and then close the designer.</span></span>

27. <span data-ttu-id="09d66-208">Если элемент **Компонент1** в **обозревателе решений** не был переименован автоматически, откройте его контекстное меню, выберите пункт **Переименовать** и укажите имя **NewEmployeeOrientationComponents**.</span><span class="sxs-lookup"><span data-stu-id="09d66-208">If the **Feature1** in **Solution Explorer** has not been automatically renamed, open its shortcut menu, select **Rename**, and rename it to **NewEmployeeOrientationComponents**.</span></span>

28. <span data-ttu-id="09d66-209">Откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="09d66-209">Open the Default.aspx file.</span></span>

29. <span data-ttu-id="09d66-210">Найдите элемент **Content** для ASP.NET с идентификатором **PlaceHolderPageTitleInTitleArea**.</span><span class="sxs-lookup"><span data-stu-id="09d66-210">Find the ASP.NET **Content** element with the ID **PlaceHolderPageTitleInTitleArea**.</span></span> <span data-ttu-id="09d66-211">Замените стандартную строку **Заголовок страницы** на **Новые сотрудники по местонахождению**.</span><span class="sxs-lookup"><span data-stu-id="09d66-211">Replace the default string **Page Title** with **New Employees by Location**.</span></span>

30. <span data-ttu-id="09d66-212">Найдите элемент **Content** для ASP.NET с идентификатором **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="09d66-212">Find the ASP.NET **Content** element with the ID **PlaceHolderMain**.</span></span> <span data-ttu-id="09d66-213">*Замените* его содержимое на приведенную ниже разметку.</span><span class="sxs-lookup"><span data-stu-id="09d66-213">*Replace* its contents with the following markup.</span></span> <span data-ttu-id="09d66-214">`_spPageContextInfo` — это объект JavaScript, который SharePoint автоматически включает на страницу.</span><span class="sxs-lookup"><span data-stu-id="09d66-214">The `_spPageContextInfo` is a JavaScript object that SharePoint automatically includes on the page.</span></span> <span data-ttu-id="09d66-215">Его свойство `webAbsoluteUrl` возвращает URL-адрес сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="09d66-215">It's `webAbsoluteUrl` property returns the URL of the add-in web.</span></span>
    
    ```XML
        <p><asp:HyperLink runat="server" 
        NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="New Employees in Seattle" /></p>
    ```

<span data-ttu-id="09d66-216"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="09d66-216"></span></span>
## <a name="run-the-add-in-and-test-the-list"></a><span data-ttu-id="09d66-217">Запуск надстройки и тестирование списка</span><span class="sxs-lookup"><span data-stu-id="09d66-217">Run the add-in and test the list</span></span>

1. <span data-ttu-id="09d66-218">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="09d66-218">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="09d66-219">Visual Studio временно устанавливает надстройку на тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="09d66-219">Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="09d66-220">Сведения о том, как пользователи запускают установленную надстройку SharePoint, см. в разделе [Дальнейшие действия](#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="09d66-220">(To find out how end users run an installed SharePoint Add-in, see [Next Steps](#Nextsteps).)</span></span>

2. <span data-ttu-id="09d66-221">Когда откроется страница надстройки по умолчанию, перейдите по ссылке **Новые сотрудники в Сиэтле**, чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="09d66-221">When the add-in's default page opens, select the **New Employees in Seattle** link to open the custom list instance.</span></span>

    ![Отображается страница по умолчанию надстройки, озаглавленная "Новые сотрудники по расположению". Ссылка "Новые сотрудники в Сиэтле". Стрелка от этой ссылки указывает на страницу списка. Она называется "Новые сотрудники в Сиэтле", список приведен ниже.](../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)

3. <span data-ttu-id="09d66-226">Добавьте и удалите элементы в списке.</span><span class="sxs-lookup"><span data-stu-id="09d66-226">Add and delete items from the list.</span></span>

4. <span data-ttu-id="09d66-p125">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="09d66-p125">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

5. <span data-ttu-id="09d66-229">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="09d66-229">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are finished working with it for a while.</span></span> <span data-ttu-id="09d66-230">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="09d66-230">Right-click the project in **Solution Explorer**, and select **Retract**.</span></span>

<span data-ttu-id="09d66-231"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="09d66-231"></span></span>
## <a name="next-steps"></a><span data-ttu-id="09d66-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09d66-232">Next steps</span></span>

<span data-ttu-id="09d66-233">Чтобы создавать надстройки, выполняйте перечисленные ниже действия в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="09d66-233">To create your add-ins, walk through the following steps in this order:</span></span>

1.  [<span data-ttu-id="09d66-234">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-234">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
2.  [<span data-ttu-id="09d66-235">Добавление настраиваемых столбцов в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-235">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
3.  [<span data-ttu-id="09d66-236">Добавление настраиваемого типа контента в надстройку с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-236">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)
4.  [<span data-ttu-id="09d66-237">Добавление веб-части на страницу в надстройке SharePoint, размещаемой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-237">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
5.  [<span data-ttu-id="09d66-238">Добавление рабочего процесса в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-238">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
6.  [<span data-ttu-id="09d66-239">Добавление настраиваемой страницы и стиля для надстройки с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-239">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
7.  [<span data-ttu-id="09d66-240">Добавление настраиваемой функции отрисовки в клиенте в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-240">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
8.  [<span data-ttu-id="09d66-241">Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-241">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md)
9.  [<span data-ttu-id="09d66-242">Использование API JavaScript для SharePoint для работы с данными SharePoint</span><span class="sxs-lookup"><span data-stu-id="09d66-242">Use the SharePoint JavaScript APIs to work with SharePoint data</span></span>](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md)
10. [<span data-ttu-id="09d66-243">Работа с данными хост-сайта из JavaScript на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="09d66-243">Work with host web data from JavaScript in the add-in web</span></span>](work-with-host-web-data-from-javascript-in-the-add-in-web.md)


