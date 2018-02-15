---
title: "Развертывание и установка надстроек SharePoint, размещаемых в SharePoint"
description: "Создайте каталог надстроек, упакуйте надстройку и отправьте ее в каталог, установите и удалите надстройку."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 58a1810d34d06b76a7e0e12b21792200bfe1bc93
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="deploy-and-install-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="8c03d-103">Развертывание и установка надстроек с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8c03d-103">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>

<span data-ttu-id="8c03d-104">Это вторая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и обзорной статьей из этой серии.</span><span class="sxs-lookup"><span data-stu-id="8c03d-104">This is the second in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with the topic [SharePoint Add-ins](sharepoint-add-ins.md) and the previous article in this series:</span></span>

-  [<span data-ttu-id="8c03d-105">Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8c03d-105">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
    
> [!NOTE]
> <span data-ttu-id="8c03d-106">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="8c03d-106">If you have been working through this series about SharePoint-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="8c03d-107">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeColumns.sln.</span><span class="sxs-lookup"><span data-stu-id="8c03d-107">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeColumns.sln file.</span></span>

<span data-ttu-id="8c03d-108">Размещаемые в SharePoint Надстройки SharePoint будет намного проще разрабатывать, зная, как пользователи развертывают и устанавливают надстройки. Поэтому в этой статье мы отвлечемся от кода, чтобы создать и использовать каталог надстроек, а затем установим надстройку, над которой вы работали.</span><span class="sxs-lookup"><span data-stu-id="8c03d-108">You'll find it a lot easier to develop SharePoint-hosted SharePoint Add-ins if you are familiar with how users deploy and install your add-ins. So, in this article, we'll take a brief break from coding to create and use an add-in catalog, and then install the add-in you've been working on.</span></span>

## <a name="create-an-add-in-catalog"></a><span data-ttu-id="8c03d-109">Создание каталога надстроек</span><span class="sxs-lookup"><span data-stu-id="8c03d-109">Create an add-in catalog</span></span>

1. <span data-ttu-id="8c03d-110">Войдите в учетную запись подписки на Office 365 от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="8c03d-110">Sign in to your Office 365 subscription as an administrator.</span></span> <span data-ttu-id="8c03d-111">Щелкните значок средства запуска надстроек, а затем выберите надстройку **Admin** (Администратор).</span><span class="sxs-lookup"><span data-stu-id="8c03d-111">Select the add-in launcher icon, and then select the **Admin** add-in.</span></span>
    
   <span data-ttu-id="8c03d-112">*Рис. 1. Средство запуска надстроек в Office 365*</span><span class="sxs-lookup"><span data-stu-id="8c03d-112">*Figure 1. Office 365 add-in launcher*</span></span>

   ![Средство запуска приложений в Office 365](../images/ec60797c-d329-4922-a811-70c64598f4d5.PNG)
 
2. <span data-ttu-id="8c03d-114">В **Центре администрирования** разверните узел **Администратор** в области задач и выберите пункт **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-114">In the **Admin Center**, expand the **Admin** node in the task pane, and then select **SharePoint**.</span></span>
     
3. <span data-ttu-id="8c03d-115">В **Центре администрирования SharePoint** выберите пункт **Надстройки** в области задач.</span><span class="sxs-lookup"><span data-stu-id="8c03d-115">In the **SharePoint Admin Center**, select **add-ins** in the task pane.</span></span>
     
4. <span data-ttu-id="8c03d-116">На странице **Надстройки** выберите пункт **Каталог надстроек**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-116">On the **add-ins** page, select **Add-in Catalog**.</span></span> <span data-ttu-id="8c03d-117">Если в подписке уже есть семейство веб-сайтов каталога надстроек, он откроется, и вам больше не нужно будет ничего делать.</span><span class="sxs-lookup"><span data-stu-id="8c03d-117">(If there is already an add-in catalog site collection in the subscription, it opens and you are finished.</span></span> <span data-ttu-id="8c03d-118">Вам не удастся создать более одного каталога в подписке.</span><span class="sxs-lookup"><span data-stu-id="8c03d-118">You cannot create more than one add-in catalog in a subscription.)</span></span>    
 
5. <span data-ttu-id="8c03d-119">На странице **Сайт каталога надстроек** нажмите кнопку **ОК**, чтобы принять параметр, используемый по умолчанию, и создать сайт каталога надстроек.</span><span class="sxs-lookup"><span data-stu-id="8c03d-119">On the **Add-in Catalog Site** page, select **OK** to accept the default option and create a new add-in catalog site.</span></span>    
 
6. <span data-ttu-id="8c03d-120">В диалоговом окне **Создание семейства веб-сайтов каталога надстроек** укажите название и веб-адрес сайта каталога надстроек.</span><span class="sxs-lookup"><span data-stu-id="8c03d-120">In the **Create Add-in Catalog Site Collection** dialog, specify the title and website address of your add-in catalog site.</span></span> <span data-ttu-id="8c03d-121">Рекомендуем включить слово "catalog" (каталог) в название и URL-адрес, чтобы было легче запомнить и найти их в **Центре администрирования SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-121">We recommend that you include "catalog" in the title and URL to make it memorable and distinguishable in the **SharePoint Admin Center**.</span></span>   
 
7. <span data-ttu-id="8c03d-122">Укажите **часовой пояс** и назначьте себя **администратором**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-122">Specify a **Time Zone** and set yourself as the **Administrator**.</span></span>
    
8. <span data-ttu-id="8c03d-123">Выберите минимально возможное значение для параметра **Квота хранилища** (в настоящее время оно равно 110, но его можно изменить), потому что пакеты надстроек, которые вы будете отправлять в это семейство веб-сайтов, совсем небольшие.</span><span class="sxs-lookup"><span data-stu-id="8c03d-123">Set the **Storage Quota** to the lowest possible value (currently 110, but that can change), because the add-in packages you upload to this site collection are very small.</span></span>
    
9. <span data-ttu-id="8c03d-124">Для параметра **Квота ресурсов сервера** задайте значение 0 (ноль) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-124">Set the **Server Resource Quota** to 0 (zero), and then select **OK**.</span></span> <span data-ttu-id="8c03d-125">(Квота ресурсов сервера связана с регулированием изолированных решений с низкой производительностью, но вы не будете устанавливать изолированные решения на сайте каталога надстроек.)</span><span class="sxs-lookup"><span data-stu-id="8c03d-125">(The server resource quota is related to throttling poorly performing sandboxed solutions, but you won't be installing any sandboxed solutions on your add-in catalog site.)</span></span> 
 
<span data-ttu-id="8c03d-126">В процессе создания семейства веб-сайтов SharePoint вернет вас в **Центр администрирования SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-126">As the site collection is being created, SharePoint takes you back to the **SharePoint Admin Center**.</span></span> <span data-ttu-id="8c03d-127">Через некоторое время вы увидите, что семейство веб-сайтов создано.</span><span class="sxs-lookup"><span data-stu-id="8c03d-127">After a few minutes, you'll see that the collection has been created.</span></span>

## <a name="package-the-add-in-and-upload-it-to-the-catalog"></a><span data-ttu-id="8c03d-128">Упаковка надстройки и ее отправка в каталог</span><span class="sxs-lookup"><span data-stu-id="8c03d-128">Package the add-in and upload it to the catalog</span></span>

1. <span data-ttu-id="8c03d-129">Откройте решение в Visual Studio, дважды щелкните узел проекта в **обозревателе решений**, а затем нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-129">Open the Visual Studio solution, right-click the project node in **Solution Explorer**, and then select **Publish**.</span></span>
     
2. <span data-ttu-id="8c03d-130">В области **Публикация** выберите пункт **Упаковать надстройку**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-130">In the **Publish** pane, select **Package the add-in**.</span></span> <span data-ttu-id="8c03d-131">Надстройка будет упакована и сохранена в виде файла `*.app` в папке решения \bin\debug\web.publish\1.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="8c03d-131">The add-in is packaged and saved as an `*.app` file in the solution's \bin\debug\web.publish\1.0.0.0 folder.</span></span>  
 
3. <span data-ttu-id="8c03d-132">Откройте сайт каталога надстроек в браузере и выберите пункт **Надстройки SharePoint** на панели навигации.</span><span class="sxs-lookup"><span data-stu-id="8c03d-132">Open your add-in catalog site in a browser, and then select **SharePoint Add-ins** in the navigation bar.</span></span>

4. <span data-ttu-id="8c03d-133">Каталог **Надстройки SharePoint** представляет собой стандартную библиотеку ресурсов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8c03d-133">The **SharePoint Add-ins** catalog is a standard SharePoint asset library.</span></span> <span data-ttu-id="8c03d-134">Отправьте в него пакет надстройки с помощью любого метода отправки файлов в библиотеки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8c03d-134">Upload the add-in package to it using any of the methods of uploading files to SharePoint libraries.</span></span>

## <a name="install-the-add-in-as-end-users-do"></a><span data-ttu-id="8c03d-135">Способ установки надстройки, применяемый пользователями</span><span class="sxs-lookup"><span data-stu-id="8c03d-135">Install the add-in as end users do</span></span>

1. <span data-ttu-id="8c03d-136">Перейдите на любой веб-сайт в подписке SharePoint Online и откройте страницу **Содержимое сайта**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-136">Navigate to any website in the SharePoint Online subscription and open the **Site Contents** page.</span></span>

2. <span data-ttu-id="8c03d-137">Выберите пункт **Добавить надстройку**. Откроется страница **Ваша надстройка**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-137">Select **add an add-in** to open the **Your Add-ins** page.</span></span>

3. <span data-ttu-id="8c03d-138">Найдите надстройку **Employee Orientation** (Обучение сотрудников) в разделе **Надстройки, которые можно добавить** и щелкните ее плитку.</span><span class="sxs-lookup"><span data-stu-id="8c03d-138">Find the **Employee Orientation** add-in in the **Add-ins you can add** section, and select its tile.</span></span>

4. <span data-ttu-id="8c03d-139">В диалоговом окне запроса согласия щелкните **Сделать доверенным**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-139">Select **Trust It** in the consent dialog.</span></span> <span data-ttu-id="8c03d-140">Автоматически откроется страница **Содержимое сайта**, и на ней отобразится надстройка с пометкой о том, что выполняется установка надстройки.</span><span class="sxs-lookup"><span data-stu-id="8c03d-140">The **Site Contents** page automatically opens and the add-in appears with a notation that it is installing.</span></span> <span data-ttu-id="8c03d-141">По завершении установки пользователи могут щелкнуть плитку, чтобы запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="8c03d-141">After it installs, users can select the tile to run the add-in.</span></span>

## <a name="remove-the-add-in"></a><span data-ttu-id="8c03d-142">Удаление надстройки</span><span class="sxs-lookup"><span data-stu-id="8c03d-142">Remove the add-in</span></span>

<span data-ttu-id="8c03d-143">Чтобы продолжить совершенствовать надстройку SharePoint в Visual Studio (см. раздел [Дальнейшие действия](#Nextsteps)), удалите ее, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="8c03d-143">To continue enhancing the same SharePoint Add-in in Visual Studio (see [Next steps](#Nextsteps)), remove the add-in with these steps:</span></span>

1. <span data-ttu-id="8c03d-144">На странице **Содержимое сайта** наведите курсор на надстройку, чтобы появилась кнопка выноски **…**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-144">In the **Site Contents** page, move the cursor over the add-in so that the callout button **...** appears.</span></span>

2. <span data-ttu-id="8c03d-145">Нажмите кнопку выноски и выберите пункт **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-145">Select the callout button, and then select **REMOVE** on the callout.</span></span>

3. <span data-ttu-id="8c03d-146">Вернитесь на сайт каталога надстроек и на панели навигации выберите пункт **Надстройки SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="8c03d-146">Navigate back to your add-in catalog site and select **SharePoint Add-ins** in the navigation bar.</span></span>

4. <span data-ttu-id="8c03d-147">Выделите надстройку и выберите команду **управление** на панели задач над списком, а затем нажмите кнопку **Удалить** в меню управления.</span><span class="sxs-lookup"><span data-stu-id="8c03d-147">Highlight the add-in and select **manage** on the task bar just above the list, and then select **Delete** on the manage menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c03d-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c03d-148">Next steps</span></span>
<a name="Nextsteps"></a>

<span data-ttu-id="8c03d-149">Настоятельно рекомендуем продолжить изучение этой серии статей о надстройках, размещаемых в SharePoint, прежде чем переходить к более сложным темам.</span><span class="sxs-lookup"><span data-stu-id="8c03d-149">We strongly recommend that you continue with this series about SharePoint-hosted add-ins before you go on to the more advanced topics.</span></span> <span data-ttu-id="8c03d-150">В статье [Добавление настраиваемых столбцов в надстройку SharePoint, размещаемую в SharePoint,](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md) мы вернемся к написанию кода.</span><span class="sxs-lookup"><span data-stu-id="8c03d-150">Next we get back to coding in [Add custom columns to a SharePoint-hosted SharePoint Add-in](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 

 

