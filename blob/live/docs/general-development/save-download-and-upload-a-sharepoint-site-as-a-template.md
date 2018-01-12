---
title: "Сохранение, скачивание и передача сайта SharePoint в качестве шаблона"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 2e637172-ddac-4a70-bd77-55a1645a3db1
ms.openlocfilehash: b1d44cb47068d39af8411dec6524c9d93e626b76
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="save-download-and-upload-a-sharepoint-site-as-a-template"></a><span data-ttu-id="31d78-102">Сохранение, скачивание и передача сайта SharePoint в качестве шаблона</span><span class="sxs-lookup"><span data-stu-id="31d78-102">Save, download, and upload a SharePoint site as a template</span></span>
<span data-ttu-id="31d78-p101">Прочитав эту статью, вы узнаете, как проектировать и создавать надежные приложения с помощью шаблонов сайтов SharePoint. Вы можете создавать надежные приложения SharePoint, которые содержат набор источников данных, доступных пользователям представлений и форм, настраиваемые рабочие процессы и т. д. После создания сайт бизнес-решения можно начать использовать его непосредственно в среде SharePoint. Кроме того, можно превратить решение в шаблон, развернуть в другой среде и сделать его доступными для пользователей, чтобы они могли создавать новые сайты на его основе. Также решение можно передать разработчиком для расширения его возможностей в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31d78-p101">Learn how to design and build robust applications by using SharePoint site templates. You can design and build robust SharePoint applications that include a rich set of data sources, customer-facing views and forms, highly customized workflows, and more. Once you've built your business solution site, you can start to use it immediately in your SharePoint environment. Or, you can turn your solution into a template and deploy it in another environment, make it available to users so they can create new sites from it, or hand it off for additional development in Visual Studio.</span></span>
  
    
    


## <a name="what-is-a-sharepoint-site-template"></a><span data-ttu-id="31d78-107">Шаблон сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="31d78-107">What is a SharePoint site template?</span></span>
<span data-ttu-id="31d78-108"><a name="bkmk_WhatIsTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="31d78-108"><a name="bkmk_WhatIsTemplate"> </a></span></span>

<span data-ttu-id="31d78-p102">Шаблоны сайтов SharePoint  это готовые определения, разработанные с учетом определенных бизнес-потребностей. Создайте собственный сайт SharePoint с помощью шаблона и затем адаптируйте его под себя. Возможно, вы знакомы с шаблонами сайтов по умолчанию, например сайтом группы, сайтом проекта и сайтом сообщества.</span><span class="sxs-lookup"><span data-stu-id="31d78-p102">SharePoint site templates are prebuilt definitions designed around a particular business need. You can use these templates as they are to create your own SharePoint site, and then customize the site as much as you want. You're probably familiar with the default site templates, such as Team Site, Project Site, and Communities Site.</span></span>
  
    
    
<span data-ttu-id="31d78-p103">Кроме шаблонов по умолчанию, можно создать собственный шаблон, основанный на созданном и настроенном вами сайте. Это позволяет создать настраиваемое решение, а затем совместно использовать его с коллегами, другими отделами или вне организации. Можно также упаковать сайт и открыть его в другой среде или приложении, например Visual Studio, а затем настроить его в новой среде.</span><span class="sxs-lookup"><span data-stu-id="31d78-p103">In addition to the default templates, you can create your own site template based on a site you've created and customized. This is a powerful feature that allows you to create a custom solution and then share that solution with your peers, the broader organization, or outside organizations. You can also package the site and open it in another environment or application such as Visual Studio and also customize it there.</span></span>
  
    
    
<span data-ttu-id="31d78-p104">Преобразование настраиваемого сайта или бизнес-решения в шаблон  очень полезная и мощная функция. Создав из решения шаблон, вы поймете все возможности SharePoint в качестве платформы бизнес-приложений. Всех этих преимуществ можно добавиться с помощью шаблона сайта.</span><span class="sxs-lookup"><span data-stu-id="31d78-p104">Turning your customized site or business solution into a template is an extremely useful and very powerful capability. Once you start to package your solution as a template, you begin to realize the potential of SharePoint as a platform for business applications. The site template option makes all of this possible.</span></span>
  
    
    
<span data-ttu-id="31d78-p105">Если сохранить сайт как шаблон, создается пакет веб-решения (WSP). По сути, WSP-файл  это CAB-файл, использующий манифест решения. Созданное вами решение хранится в каталоге решений для семейства веб-сайтов SharePoint. После сохранения шаблона создается WSP-файл, который хранится в каталоге решений, где вы можете скачать или активировать решение.</span><span class="sxs-lookup"><span data-stu-id="31d78-p105">When you save your site as a template, you create a Web Solution Package, or WSP. A WSP is a CAB file that uses the solution manifest. The solution that you create is stored in the solutions gallery for the SharePoint site collection. Once you save the template, a solution file (.wsp) is created and stored in the solutions gallery where you can download or activate the solution.</span></span>
  
> [!NOTE]
> <span data-ttu-id="31d78-p106">Созданный пакет WSP — пользовательское решение с частичным доверием, которое использует тот же декларативный формат, что и решение SharePoint с полным доверием. Тем не менее, WSP поддерживает не весь спектр компонентов, которые поддерживаются решениями с полным доверием.</span><span class="sxs-lookup"><span data-stu-id="31d78-p106">The WSP you create is a partial trust user solution that has the same declarative format as a full trust SharePoint solution. However, it does not support the full extent of feature element types that are supported by full trust solutions.</span></span> 
  
    
    


### <a name="what-gets-saved-in-a-template"></a><span data-ttu-id="31d78-124">Какие данные сохраняются в шаблоне?</span><span class="sxs-lookup"><span data-stu-id="31d78-124">What gets saved in a template?</span></span>

<span data-ttu-id="31d78-p107">При сохранении сайта SharePoint в шаблоне записывается общая структура сайта  его списки и библиотеки, представления и формы, а также рабочие процессы. Помимо этих компонентов вы можно включить в шаблон контент сайта, например документы, хранящиеся в библиотеках документов. Так пользователи получат образцы контента для начала работы с сайтом. Помните, что при этом размер шаблона сайта может превысить ограничение по умолчанию  50 МБ.</span><span class="sxs-lookup"><span data-stu-id="31d78-p107">When you save a SharePoint site as a template, you're saving the overall framework of the site — its lists and libraries, views and forms, and workflows. In addition to these components, you can include the contents of the site in the template; for example, the documents stored in the document libraries. This could be useful to provide sample content for users to get started with. Consider that this could also increase the size of your template beyond the default 50-MB site template limit.</span></span>
  
    
    
<span data-ttu-id="31d78-p108">Большинство объектов на сайте добавляются в шаблон. Тем не менее, существуют несколько объектов и функций, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="31d78-p108">Most of the objects in a site are included and supported by the template. However, there are several objects and features that are not supported.</span></span> 
  
    
    

- <span data-ttu-id="31d78-131">**Поддерживаются:** списки, библиотеки, внешние списки, подключения к источникам данных, представления списков и данных, настраиваемые формы, рабочие процессы, типы контента, настраиваемые действия, навигация, страницы сайта, главные страницы, модули и веб-шаблоны.</span><span class="sxs-lookup"><span data-stu-id="31d78-131">**Supported** Lists, libraries, external lists, data source connections, list views and data views, custom forms, workflows, content types, custom actions, navigation, site pages, master pages, modules, and web templates.</span></span>
    
  
- <span data-ttu-id="31d78-132">**Не поддерживаются:** настроенные разрешения, запущенные экземпляры рабочих процессов, журнал версий элементов списка, задачи рабочих процессов, связанные с запущенными рабочими процессами, значения полей пользователей или групп, значения полей таксономии, страницы и сайты публикации, личные сайты, ассоциированные функции, Надстройки SharePoint и удаленные приемники событий.</span><span class="sxs-lookup"><span data-stu-id="31d78-132">**Unsupported** Customized permissions, running workflow instances, list item version history, workflow tasks associated with running workflows, people or group field values, taxonomy field values, publishing pages and publishing sites, My Sites, stapled features, SharePoint Add-ins, and remote event receivers.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="31d78-133">Для сайтов публикации можно пользоваться шаблонами определения сайта.</span><span class="sxs-lookup"><span data-stu-id="31d78-133">Note: For publishing sites, you can use site definition templates.</span></span> <span data-ttu-id="31d78-134">Дополнительные сведения см. в разделе [Дополнительные ресурсы](save-download-and-upload-a-sharepoint-site-as-a-template.md#bkmk_additionalresources) в конце данной статьи.</span><span class="sxs-lookup"><span data-stu-id="31d78-134">For more information, see  [Additional resources](save-download-and-upload-a-sharepoint-site-as-a-template.md#bkmk_additionalresources) at the end of this topic.</span></span>

### <a name="what-can-you-do-with-sharepoint-templates"></a><span data-ttu-id="31d78-135">Что можно делать с шаблонами SharePoint?</span><span class="sxs-lookup"><span data-stu-id="31d78-135">What can you do with SharePoint templates?</span></span>

<span data-ttu-id="31d78-p110">Сохранение сайта в виде шаблона  это мощный инструмент, поскольку вы получаете возможность использовать настраиваемые сайты разными способами. Ниже приведены некоторые очевидные преимущества сохранения сайта в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="31d78-p110">Saving a site as a template is a powerful feature because it offers so many uses of custom sites. Here are the immediate benefits you get from saving a site as a template:</span></span>
  
    
    

- <span data-ttu-id="31d78-p111">**Мгновенное развертывание решений**: сохраните и активируйте шаблон в каталоге решений, после чего другие сотрудники смогут создавать сайты на его основе. Вы можете выбрать шаблон и создать новый сайт, который наследует все компоненты шаблона, его структуру, рабочие процессы и многое другое. Вам не нужно использовать Visual Studio для создания решения, и вы получаете прямой доступ к серверу и можете выполнять команды администратора сервера. Просто сохраните сайт как шаблон, активируйте его  и вы готовы к работе.</span><span class="sxs-lookup"><span data-stu-id="31d78-p111">**Deploy solutions immediately** Save and activate the template in the solutions gallery and let other employees create new sites from this template. You can select it, and then create a new site from it, which will inherit the components of the site, its structure, workflows, and more. You don't need Visual Studio to create your solution, and you have to access the server directly and run server administrator commands. Just save the site as a template, activate it, and off you go.</span></span>
    
  
- <span data-ttu-id="31d78-p112">**Переносимость**: помимо развертывания настраиваемого решения в собственной среде, вы можете скачать WSP-файл, взять его с собой и развернуть в другой среде SharePoint. Все настройки сайта хранятся в одном файле.</span><span class="sxs-lookup"><span data-stu-id="31d78-p112">**Portability** In addition to deploying a custom solution in your environment, you can download the .wsp file, take it on the road, and deploy it in another SharePoint environment. All of your site customization is conveniently stored in one file.</span></span>
    
  
- <span data-ttu-id="31d78-p113">**Расширяемость**: вы можете открыть настроенный сайт как пакет веб-решения в Visual Studio, выполнить дополнительную настройку шаблона и развернуть его в SharePoint. В результате, разработка сайта SharePoint может пройти жизненный цикл решения (разработка, размещение и перевод в эксплуатацию), в который входят SharePoint Designer 2013, Visual Studio и браузер.</span><span class="sxs-lookup"><span data-stu-id="31d78-p113">**Extensibility** As a Web Solution Package, you can open your customized site in Visual Studio, perform additional development customization to the template, and then deploy it to SharePoint. SharePoint site development, as a result, can go through a solution life cycle (develop, stage, and put into production) that includes SharePoint Designer 2013, Visual Studio, and the browser.</span></span>
    
  
<span data-ttu-id="31d78-p114">Приступая к созданию настраиваемых сайтов в SharePoint, вы обнаружите еще больше преимуществ преобразования сайта в решение, которые можно перемещать в пределах организации. Ниже приведены основные шаги по работе с шаблонами сайтов.</span><span class="sxs-lookup"><span data-stu-id="31d78-p114">As you begin to create custom sites in SharePoint, you'll discover even more benefits to turning your site into a solution that can be made portable across the organization. The basic steps to working with site templates are as follows:</span></span>
  
    
    

- <span data-ttu-id="31d78-148">Сохраните сайт как шаблон в каталоге решений.</span><span class="sxs-lookup"><span data-stu-id="31d78-148">Save a site as a template to the solutions gallery.</span></span>
    
  
- <span data-ttu-id="31d78-149">Скачайте шаблон сайта из каталога решений в WSP-файл.</span><span class="sxs-lookup"><span data-stu-id="31d78-149">Download the site template from the solutions gallery to a .wsp file.</span></span>
    
  
- <span data-ttu-id="31d78-150">Отправьте WSP-файл в каталог решений.</span><span class="sxs-lookup"><span data-stu-id="31d78-150">Upload the .wsp file to the solutions gallery.</span></span>
    
  
<span data-ttu-id="31d78-151">После добавления шаблона сайта в каталог решений и его активации он будет доступен при следующем создании сайта или дочернего сайта на вкладке **Настраиваемое** в разделе **Выбор шаблона** на странице **Новый сайт SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="31d78-151">After you add a site template to the solutions gallery and the template is activated, the next time that you create a site or subsite, the template is available for selection in the **Custom** tab of the **Template Selection** section on the **New SharePoint Site** page.</span></span>
  
    
    

## <a name="save-a-site-as-a-template-to-the-solutions-gallery"></a><span data-ttu-id="31d78-152">Сохранение сайта как шаблона в каталоге решений</span><span class="sxs-lookup"><span data-stu-id="31d78-152">Save a site as a template to the solutions gallery</span></span>
<span data-ttu-id="31d78-153"><a name="bkmk_SaveTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="31d78-153"><a name="bkmk_SaveTemplate"> </a></span></span>


1. <span data-ttu-id="31d78-154">Перейдите на сайт верхнего уровня семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="31d78-154">Navigate to the top-level site of your site collection.</span></span>
    
  
2. <span data-ttu-id="31d78-155">Нажмите кнопку **Параметры**, а затем щелкните **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="31d78-155">Click **Settings**, and then click **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="31d78-156">В разделе **Действия сайта** щелкните **Сохранить сайт как шаблон**.</span><span class="sxs-lookup"><span data-stu-id="31d78-156">In the **Site Actions** section, click **Save site as a template**.</span></span>
    
  
4. <span data-ttu-id="31d78-157">Укажите имя файла шаблона в поле **Имя файла**.</span><span class="sxs-lookup"><span data-stu-id="31d78-157">Specify a name to use for the template file in the **File name** box.</span></span>
    
  
5. <span data-ttu-id="31d78-158">Введите имя и описание шаблона в полях **Имя шаблона** и **Описание шаблона**.</span><span class="sxs-lookup"><span data-stu-id="31d78-158">Specify a name and description for the template in the **Template name** and **Template description** boxes.</span></span>
    
  
6. <span data-ttu-id="31d78-159">Чтобы добавить контент сайта в шаблон сайта, установите флажок **Включить контент**.</span><span class="sxs-lookup"><span data-stu-id="31d78-159">To include the content of the site in the site template, select the **Include Content** box.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="31d78-160">Размер шаблона может существенно увеличиться при включении контента сайта.</span><span class="sxs-lookup"><span data-stu-id="31d78-160">Note: Including the content of the site can increase the size of the template significantly.</span></span> <span data-ttu-id="31d78-161">По умолчанию размер шаблона сайта ограничен 50 МБ, но в вашей организации этот показатель может быть меньше.</span><span class="sxs-lookup"><span data-stu-id="31d78-161">The default size limit for a site template is 50 MB but might be less in your organization.</span></span> <span data-ttu-id="31d78-162">Контент можно в любой момент исключить, а позже скопировать необходимые данные на новый сайт.</span><span class="sxs-lookup"><span data-stu-id="31d78-162">You can always exclude the content, and then copy what you need later into the new site.</span></span> <span data-ttu-id="31d78-163">Кроме того, вы можете изменить ограничение.</span><span class="sxs-lookup"><span data-stu-id="31d78-163">Or, you can increase the size limit.</span></span> <span data-ttu-id="31d78-164">Например, чтобы изменить ограничение, указав максимально допустимый размер, используйте указанный ниже синтаксис команды Stsadm.</span><span class="sxs-lookup"><span data-stu-id="31d78-164">For example, to increase the limit to the maximum allowed, use the following Stsadm command syntax.</span></span> >  `stsadm -o setproperty -pn max-template-document-size -pv 524288000`

7. <span data-ttu-id="31d78-165">Нажмите кнопку **ОК**, чтобы сохранить шаблон.</span><span class="sxs-lookup"><span data-stu-id="31d78-165">Click **OK** to save the template.</span></span>
    
    <span data-ttu-id="31d78-166">Если все компоненты сайта допустимы, будет создан шаблон, и появится сообщение с текстом "Операция успешно завершена".</span><span class="sxs-lookup"><span data-stu-id="31d78-166">If all of the components on the site are valid, the template is created, and you see a message that states "Operation Completed Successfully."</span></span>
    
  
8. <span data-ttu-id="31d78-167">Выполните одно из указанных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="31d78-167">Do one of the following:</span></span>
    
  - <span data-ttu-id="31d78-168">Чтобы вернуться на сайт, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="31d78-168">To return to your site, click **OK**.</span></span>
    
  
  - <span data-ttu-id="31d78-169">Чтобы перейти непосредственно к шаблону сайта, щелкните **Каталог решений**.</span><span class="sxs-lookup"><span data-stu-id="31d78-169">To go directly to the site template, click **Solutions Gallery**.</span></span>
    
  

## <a name="download-the-site-template-from-the-solutions-gallery-to-a-file"></a><span data-ttu-id="31d78-170">Скачивание шаблона сайта из каталога решений в файл</span><span class="sxs-lookup"><span data-stu-id="31d78-170">Download the site template from the solutions gallery to a file</span></span>
<span data-ttu-id="31d78-171"><a name="bkmk_DownloadTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="31d78-171"><a name="bkmk_DownloadTemplate"> </a></span></span>


1. <span data-ttu-id="31d78-172">Перейдите на сайт верхнего уровня семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="31d78-172">Navigate to the top-level site of your site collection.</span></span>
    
  
2. <span data-ttu-id="31d78-173">Нажмите кнопку **Параметры**, а затем щелкните **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="31d78-173">Click **Settings**, and then click **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="31d78-174">В разделе **Коллекции веб-дизайнера** щелкните **Решения**.</span><span class="sxs-lookup"><span data-stu-id="31d78-174">In the **Web Designer Galleries** section, click **Solutions**.</span></span>
    
  
4. <span data-ttu-id="31d78-p116">Если необходимо активировать решение, выберите его и в группе **Команды** щелкните **Активировать**. Затем в окне **Подтверждение активации решения** в группе **Команды** щелкните **Активировать**.</span><span class="sxs-lookup"><span data-stu-id="31d78-p116">If it's necessary to activate the solution, select it, and in the **Commands** group, click **Activate**. Then, on the **Activate Solution Confirmation** screen, in the **Commands** group, click **Activate**.</span></span>
    
  
5. <span data-ttu-id="31d78-p117">Чтобы скачать решение, щелкните его имя в каталоге решений и нажмите кнопку **Сохранить**. Затем в диалоговом окне **Сохранить как** перейдите к папке, в которой требуется сохранить решение, нажмите кнопку **Сохранить** и нажмите **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="31d78-p117">To download the solution, click its name in the solutions gallery, and click **Save**. Then, in the **Save As** dialog box, browse to the location where you want to save the solution, click **Save**, and then click **Close**.</span></span>
    
  

## <a name="upload-the-site-template-file-to-a-solutions-gallery"></a><span data-ttu-id="31d78-179">Отправка файла шаблона сайта в каталог решений</span><span class="sxs-lookup"><span data-stu-id="31d78-179">Upload the site template file to a solutions gallery</span></span>
<span data-ttu-id="31d78-180"><a name="bkmk_UploadTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="31d78-180"><a name="bkmk_UploadTemplate"> </a></span></span>


1. <span data-ttu-id="31d78-181">Перейдите на сайт верхнего уровня семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="31d78-181">Navigate to the top-level site of your site collection.</span></span>
    
  
2. <span data-ttu-id="31d78-182">Нажмите кнопку **Параметры**, а затем щелкните **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="31d78-182">Click **Settings**, and then click **Site Settings**.</span></span>
    
  
3. <span data-ttu-id="31d78-183">В разделе **Коллекции веб-дизайнера** щелкните **Решения**.</span><span class="sxs-lookup"><span data-stu-id="31d78-183">In the **Web Designer Galleries** section, click **Solutions**.</span></span>
    
  
4. <span data-ttu-id="31d78-p118">Чтобы отправить в решение, в группе **Команды** щелкните **Отправить**, а затем в диалоговом окне **Добавление документа** нажмите кнопку **Обзор**. В диалоговом окне **Выбор файла для отправки** перейдите к файлу, выберите его, нажмите кнопку **Открыть** и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="31d78-p118">To upload the solution, in the **Commands** group, click **Upload**, and then in the **Add a Document** dialog box, click **Browse**. Then, in the **Choose File to Upload** dialog box, locate the file, select it, click **Open**, and then click **OK**.</span></span>
    
  
5. <span data-ttu-id="31d78-186">Чтобы активировать решение, на экране подтверждения активации в группе **Команды** щелкните **Активировать**.</span><span class="sxs-lookup"><span data-stu-id="31d78-186">To activate the solution, on the activate solution confirmation screen, in the **Commands** group, click **Activate**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="31d78-187">См. также</span><span class="sxs-lookup"><span data-stu-id="31d78-187">See also</span></span>
<span data-ttu-id="31d78-188"><a name="bkmk_additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="31d78-188"><a name="bkmk_additionalresources"> </a></span></span>


-  [<span data-ttu-id="31d78-189">Типы сайтов: веб-шаблоны и определения сайтов</span><span class="sxs-lookup"><span data-stu-id="31d78-189">Site Types: WebTemplates and Site Definitions</span></span>](http://msdn.microsoft.com/ru-RU/library/ms434313.aspx)
    
  
-  [<span data-ttu-id="31d78-190">Общие сведения об упаковке и развертывании рабочего процесса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="31d78-190">Understanding how to package and deploy workflow in SharePoint</span></span>](http://msdn.microsoft.com/ru-RU/library/jj819316%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="31d78-191">Построение решений для ферм в SharePoint</span><span class="sxs-lookup"><span data-stu-id="31d78-191">Build farm solutions in SharePoint</span></span>](http://msdn.microsoft.com/ru-RU/library/jj163902%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="31d78-192">Копирование и перемещение списка с помощью шаблонов списка</span><span class="sxs-lookup"><span data-stu-id="31d78-192">Copy or move lists by using list templates</span></span>](http://office.com/redir/HA101782479.aspx)
    
  
-  [<span data-ttu-id="31d78-193">Копирование и перемещение библиотеки с помощью шаблонов библиотеки</span><span class="sxs-lookup"><span data-stu-id="31d78-193">Copy or move a library by using a library template</span></span>](http://office.com/redir/HA101814157.aspx)
    
  
-  [<span data-ttu-id="31d78-194">Копирование и перемещение файлов библиотеки с помощью проводника Windows</span><span class="sxs-lookup"><span data-stu-id="31d78-194">Copy or move library files by using Windows Explorer</span></span>](http://office.com/redir/HA101811182.aspx)
    
  

