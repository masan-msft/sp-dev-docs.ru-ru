---
title: "Создание облачной бизнес-надстройки"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: dd7c03e54da77a99f96e206844ca934de758ea8b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-cloud-business-add-in"></a><span data-ttu-id="522e8-102">Создание облачной бизнес-надстройки</span><span class="sxs-lookup"><span data-stu-id="522e8-102">Create a cloud business add-in</span></span>
<span data-ttu-id="522e8-103">С помощью шаблона "Облачная бизнес-надстройка" в Visual Studio можно создавать надстройки для SharePoint или SharePoint в Office 365, оптимизированные для добавления данных и управления ими.</span><span class="sxs-lookup"><span data-stu-id="522e8-103">By using the Cloud Business Add-in template in Visual Studio, you can create SharePoint Add-ins 2013 or SharePoint on Office 365 that are optimized for adding and managing data.</span></span>
 

 <span data-ttu-id="522e8-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="522e8-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="522e8-107">**Примечание.** Вы также можете создать надстройку SharePoint с помощью шаблона "Надстройка для SharePoint".</span><span class="sxs-lookup"><span data-stu-id="522e8-107">**Note**  You can also build a SharePoint Add-in by using the Add-in for SharePoint template.</span></span>
 


### <a name="to-create-a-cloud-business-add-in"></a><span data-ttu-id="522e8-108">Создание облачной бизнес-надстройки</span><span class="sxs-lookup"><span data-stu-id="522e8-108">To create a cloud business add-in</span></span>


1. <span data-ttu-id="522e8-109">В строке меню выберите пункты **Файл**, **Создать** и **Проект**.</span><span class="sxs-lookup"><span data-stu-id="522e8-109">On the menu bar, choose  **File**,  **New**,  **Project**.</span></span>
    
    <span data-ttu-id="522e8-110">Откроется диалоговое окно **Создание проекта**.</span><span class="sxs-lookup"><span data-stu-id="522e8-110">The  **New Project** dialog box opens.</span></span>
    
 
2. <span data-ttu-id="522e8-111">В списке шаблонов разверните узел **Visual Basic** или **Visual C#**, затем выберите **Office/SharePoint** > **Надстройки** > **Облачная бизнес-надстройка**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="522e8-111">In the list of templates, expand the  **Visual Basic** or **Visual C#** node, expand the **Office/SharePoint** node, choose the **Add-ins** node, and then choose **Cloud Business Add-in**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="522e8-112">**Рис. 1. Шаблон "Облачная бизнес-надстройка"**</span><span class="sxs-lookup"><span data-stu-id="522e8-112">**Figure 1. Cloud Business Add-in template**</span></span>

 

  ![Шаблон для создания облачного бизнес-приложения](../images/CloudBusinessApptemplate.PNG)
 

 

 
3. <span data-ttu-id="522e8-114">В текстовом поле **Имя** введите имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="522e8-114">In the  **Name** text box, enter a name for your project, and then choose the **OK** button.</span></span>
    
    <span data-ttu-id="522e8-115">Откроется мастер **создания облачной бизнес-надстройки**.</span><span class="sxs-lookup"><span data-stu-id="522e8-115">The  **New Cloud Business Add-in** wizard opens.</span></span>
    
 
4. <span data-ttu-id="522e8-116">В мастере **создания облачной бизнес-надстройки** введите URL-адрес вашего сервера SharePoint или сайта разработчика приложений для Office 365, как показано на рис. 2, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="522e8-116">In the  **New Cloud Business Add-in** wizard, enter the Site URL for your SharePoint server or your Office 365 Developer site as shown in Figure 2, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="522e8-117">**Рис. 2. URL-адрес SharePoint**</span><span class="sxs-lookup"><span data-stu-id="522e8-117">**Figure 2. SharePoint URL**</span></span>

 

  ![URL-адрес SharePoint](../images/SiteURL.PNG)
 

    <span data-ttu-id="522e8-119">URL-адрес должен быть представлен в следующем виде: https://_MySite_.sharepoint.com/sites/Developer/.</span><span class="sxs-lookup"><span data-stu-id="522e8-119">The URL should take the form https://  _MySite_.sharepoint.com/sites/Developer/.</span></span>
    
    <span data-ttu-id="522e8-120">В обозреватель решений будет добавлено новое решение с четырьмя проектами: проектом верхнего уровня, проектом **HTMLClient**, проектом **Server** и проектом **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="522e8-120">A new solution is added to Solution Explorer with four projects: a top-level project, a  **HTMLClient** project, a **Server** project, and a **SharePoint** project.</span></span>
    
 

### <a name="to-change-the-site-for-a-cloud-business-add-in"></a><span data-ttu-id="522e8-121">Изменение сайта для облачной бизнес-надстройки</span><span class="sxs-lookup"><span data-stu-id="522e8-121">To change the site for a cloud business add-in</span></span>


1. <span data-ttu-id="522e8-122">В **обозревателе решений** откройте контекстное меню для узла проекта верхнего уровня и выберите пункт **Свойства**, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="522e8-122">In  **Solution Explorer**, open the shortcut menu for the top-level project node and choose  **Properties**, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="522e8-123">**Рис. 3. Узел проекта верхнего уровня**</span><span class="sxs-lookup"><span data-stu-id="522e8-123">**Figure 3. The top-level project node**</span></span>

 

  ![Узел проекта верхнего уровня](../images/Top-levelprojectnode.PNG)
 

    <span data-ttu-id="522e8-125">Откроется конструктор приложений.</span><span class="sxs-lookup"><span data-stu-id="522e8-125">The application designer opens.</span></span>
    
 
2. <span data-ttu-id="522e8-126">В конструкторе приложений выберите вкладку **SharePoint**, как показано на рис. 4.</span><span class="sxs-lookup"><span data-stu-id="522e8-126">In the application designer, choose the  **SharePoint** tab as shown in Figure 4.</span></span>
    
    <span data-ttu-id="522e8-127">**Рис. 4. Вкладка SharePoint**</span><span class="sxs-lookup"><span data-stu-id="522e8-127">**Figure 4. The SharePoint tab**</span></span>

 

  ![Вкладка свойств SharePoint](../images/SharePointtab.PNG)
 

 

 
3. <span data-ttu-id="522e8-129">В списке **URL-адрес сайта** выберите существующий URL-адрес или введите URL-адрес вашего сервера SharePoint или сайта разработчика приложений для Office 365.</span><span class="sxs-lookup"><span data-stu-id="522e8-129">In the  **Site URL** list, choose an existing URL or enter the Site URL for your SharePoint server or your Office 365 Developer site.</span></span>
    
 
4. <span data-ttu-id="522e8-130">Нажмите кнопку **Проверить**, чтобы проверить URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="522e8-130">Choose the  **Validate** button to verify the URL.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="522e8-131">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="522e8-131">Additional resources</span></span>
<span data-ttu-id="522e8-132"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="522e8-132"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="522e8-133">Разработка облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="522e8-133">Develop cloud business add-ins</span></span>](develop-cloud-business-add-ins.md)
    
 
-  [<span data-ttu-id="522e8-134">Создание облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="522e8-134">Create cloud business add-ins</span></span>](create-cloud-business-add-ins.md)
    
 

