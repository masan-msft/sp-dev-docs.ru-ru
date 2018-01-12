---
title: "Создание рабочего процесса с повышенным уровнем разрешений при помощи платформы SharePoint Workflow"
description: "Создание рабочих процессов SharePoint, доступ к объектам в SharePoint, которые требуют повышенного уровня разрешений. Эти решения предоставлять разрешения для приложения рабочего процесса и перенос действия с шага приложения."
ms.date: 12/29/2017
ms.prod: sharepoint
ms.assetid: 4656f6a0-36fd-4b7d-898e-8cd4bdbbda57
ms.openlocfilehash: 2efa1810d3d6a0c579daa356599ef9dfffda230f
ms.sourcegitcommit: 469ce248552201a47ebea1b6c85bc5c90a97c7ac
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflow-platform"></a><span data-ttu-id="96c1f-104">Создание рабочего процесса с повышенным уровнем разрешений при помощи платформы SharePoint Workflow</span><span class="sxs-lookup"><span data-stu-id="96c1f-104">Create a workflow with elevated permissions by using the SharePoint Workflow platform</span></span>

<span data-ttu-id="96c1f-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="96c1f-105"></span></span>

<span data-ttu-id="96c1f-106">В этой статье описывается, как для создания рабочих процессов SharePoint, доступ к объектам в SharePoint, которые требуют повышенного уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="96c1f-106">This article describes how to create SharePoint workflows that access objects in SharePoint that require elevated permissions.</span></span> <span data-ttu-id="96c1f-107">Эти решения использовать две функции: предоставление разрешений для приложения рабочего процесса и переноса действий с помощью шаге приложения.</span><span class="sxs-lookup"><span data-stu-id="96c1f-107">These solutions use two features: granting permissions to the workflow app and wrapping actions with the App Step.</span></span>
  
> [!IMPORTANT] 
> <span data-ttu-id="96c1f-108">В этой статье предполагается, что платформа рабочих процессов SharePoint установлено и настроено, и, что SharePoint будет настроен для надстроек. Для получения дополнительных сведений о рабочих процессах SharePoint и SharePoint надстроек, включая установку и настройку, посетите [рабочих процессов в SharePoint](workflows-in-sharepoint.md) и [Установка и управление ими надстройки SharePoint](../sp-add-ins/sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="96c1f-108">This article assumes that the SharePoint Workflow platform has been installed and configured and that SharePoint has been configured for add-ins. For more information about SharePoint Workflows and SharePoint Add-ins, including installation and configuration, see [Workflows in SharePoint](workflows-in-sharepoint.md) and [Install and manage SharePoint Add-ins](../sp-add-ins/sharepoint-add-ins.md).</span></span> 

<span data-ttu-id="96c1f-109">Предположим, что администратор SharePoint необходимо определить некоторые действия по управлению запросов пользователей на покупку надстроек приложений из магазина Office.</span><span class="sxs-lookup"><span data-stu-id="96c1f-109">Imagine that as a SharePoint administrator, you would like to define some processes for managing user requests for purchases of add-ins from the Office Store.</span></span> <span data-ttu-id="96c1f-110">В простом случае необходимо отправить сообщение электронной почты подтверждения, когда пользователь запрашивает надстройки.</span><span class="sxs-lookup"><span data-stu-id="96c1f-110">In the simplest case, you want to send an acknowledgment email when a user requests an add-in.</span></span> <span data-ttu-id="96c1f-111">Кроме того можно также добавление структуры в процесс утверждения запроса.</span><span class="sxs-lookup"><span data-stu-id="96c1f-111">In addition, you might also want to add structure to the request approval process.</span></span>
  
<span data-ttu-id="96c1f-112">По умолчанию рабочий процесс не имеет разрешений на доступ в каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="96c1f-112">By default, workflow does not have permissions to access the app catalog.</span></span> <span data-ttu-id="96c1f-113">Каталог списков в SharePoint требуются разрешения владельца (полный доступ).</span><span class="sxs-lookup"><span data-stu-id="96c1f-113">Catalog lists in SharePoint require owner (full control) permissions.</span></span> <span data-ttu-id="96c1f-114">Рабочие процессы обычно выполняются на уровне разрешений, соответствует записи.</span><span class="sxs-lookup"><span data-stu-id="96c1f-114">Workflows generally run at a permission level equivalent to write.</span></span> 
  
<span data-ttu-id="96c1f-115">Чтобы устранить эту проблему, необходимо создать рабочий процесс с повышенными правами, выполните указанные ниже действия на сайте семейства веб-сайтов:</span><span class="sxs-lookup"><span data-stu-id="96c1f-115">To solve this, you have to create a workflow with elevated permissions by doing the following in the Site Collection site:</span></span>

1. <span data-ttu-id="96c1f-116">Разрешить рабочего процесса, чтобы использовать надстройки разрешения.</span><span class="sxs-lookup"><span data-stu-id="96c1f-116">Allow the workflow to use add-in permissions.</span></span>

2. <span data-ttu-id="96c1f-117">Предоставить разрешение полного доступа к рабочему процессу.</span><span class="sxs-lookup"><span data-stu-id="96c1f-117">Grant full control permission to the workflow.</span></span>
 
3. <span data-ttu-id="96c1f-118">Разработка рабочего процесса, чтобы переносить действий внутри шага приложения.</span><span class="sxs-lookup"><span data-stu-id="96c1f-118">Develop the workflow to wrap actions inside an App Step.</span></span>

## <a name="allow-a-workflow-to-use-add-in-permissions-on-a-sharepoint-site"></a><span data-ttu-id="96c1f-119">Рабочий процесс использования надстройки разрешения на сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="96c1f-119">Allow a workflow to use add-in permissions on a SharePoint site</span></span>

<span data-ttu-id="96c1f-120">Первый шаг — это рабочий процесс с помощью надстройки разрешений.</span><span class="sxs-lookup"><span data-stu-id="96c1f-120">The first step is to allow the workflow to use add-in permissions.</span></span> <span data-ttu-id="96c1f-121">Настройка рабочего процесса для использования надстройки разрешения на странице " **Параметры сайта** " на сайте SharePoint, где выполняется рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="96c1f-121">You configure a workflow to use add-in permissions on the **Site settings** page of the SharePoint site where the workflow runs.</span></span> <span data-ttu-id="96c1f-122">Следующая процедура настраивает рабочий процесс с помощью надстройки разрешений на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="96c1f-122">The following procedure configures the SharePoint site to allow the workflow to use add-in permissions.</span></span>
  
> [!IMPORTANT] 
> <span data-ttu-id="96c1f-123">[!Важно!] Необходимо выполнить процедуру, пользователь, имеющий разрешения **Владельца сайта**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-123">The procedure must be completed by a user that has **Site Owner** permissions.</span></span>

### <a name="to-allow-workflow-to-use-add-in-permissions"></a><span data-ttu-id="96c1f-124">Чтобы разрешить рабочего процесса для использования надстройки разрешения</span><span class="sxs-lookup"><span data-stu-id="96c1f-124">To allow workflow to use add-in permissions</span></span>

1. <span data-ttu-id="96c1f-125">Выберите значок « **Параметры** », как показано на рисунке, чтобы открыть страницу **параметров сайта** .</span><span class="sxs-lookup"><span data-stu-id="96c1f-125">Select the **Settings** icon as shown in the figure to open the **Site settings** page.</span></span>

  ![Меню параметров](../images/SPD15-WFAppPermissions1.png)

2. <span data-ttu-id="96c1f-127">Переход к **параметрам сайта**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-127">Go to **Site settings**.</span></span>
 
3. <span data-ttu-id="96c1f-128">В разделе **Действия сайта** выберите **Управление возможностями сайта**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-128">In the **Site Actions** section, select **Manage site features**.</span></span>

4. <span data-ttu-id="96c1f-129">Найдите компонент **рабочих процессов можно использовать разрешения для приложений**, как показано на рисунке и затем нажмите кнопку **активировать**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-129">Locate the feature called **Workflows can use app permissions**, as shown in the figure, and then select **Activate**.</span></span>
    
  > [!WARNING] 
  > <span data-ttu-id="96c1f-130">Этот компонент не будет активирован, если не правильно настроены платформа рабочих процессов SharePoint и надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="96c1f-130">This feature will not activate unless you have properly configured the SharePoint Workflow platform and SharePoint Add-ins.</span></span> 

  ![Рабочий процесс может использовать компонент разрешений приложения](../images/SPD15-WFAppPermissions2.png)
  

## <a name="grant-full-control-permission-to-a-workflow"></a><span data-ttu-id="96c1f-132">Предоставить разрешение "Полный доступ" для рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="96c1f-132">Grant full control permission to a workflow</span></span>

<span data-ttu-id="96c1f-133">Для этого рабочего процесса для правильной его необходимо предоставить полный доступ на сайте.</span><span class="sxs-lookup"><span data-stu-id="96c1f-133">For the workflow to function properly, it must be granted full control on the site.</span></span> <span data-ttu-id="96c1f-134">Следующая процедура предоставляет разрешение полного доступа к рабочему процессу.</span><span class="sxs-lookup"><span data-stu-id="96c1f-134">The following procedure grants full control permission to the workflow.</span></span>
  
> [!IMPORTANT] 
> <span data-ttu-id="96c1f-135">[!Важно!] Необходимо выполнить процедуру, пользователь, имеющий разрешения **Владельца сайта**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-135">The procedure must be completed by a user that has **Site Owner** permissions.</span></span> <span data-ttu-id="96c1f-136">Рабочий процесс уже должны быть опубликованы на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="96c1f-136">The workflow must already be published to the SharePoint site.</span></span>

### <a name="to-grant-full-control-permission-to-a-workflow"></a><span data-ttu-id="96c1f-137">Чтобы предоставить разрешение на полный доступ к рабочему процессу</span><span class="sxs-lookup"><span data-stu-id="96c1f-137">To grant full control permission to a workflow</span></span>

1. <span data-ttu-id="96c1f-138">Выберите значок « **Параметры** ».</span><span class="sxs-lookup"><span data-stu-id="96c1f-138">Select the **Settings** icon.</span></span>
 
  ![Меню параметров](../images/SPD15-WFAppPermissions1.png)

2. <span data-ttu-id="96c1f-140">Переход к **параметрам сайта**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-140">Go to **Site settings**.</span></span>    
  
3. <span data-ttu-id="96c1f-141">В разделе **пользователи и разрешения** выберите **разрешения для сайта приложения**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-141">In the **Users and Permissions** section, select **Site app permissions**.</span></span>    
  
4. <span data-ttu-id="96c1f-p108">Копирование разделе **клиента** **Идентификатора приложения**. Это идентификатор между последним "|" и "@" войти, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-p108">Copy the **client** section of the **App Identifier**. This is the identifier between the last "|" and the "@" sign, as shown in the figure.</span></span>
    
  ![Выбор идентификатора приложения](../images/SPD15-WFAppPermissions3.png)

5. <span data-ttu-id="96c1f-145">Перейдите на страницу **Предоставление разрешений для приложения** .</span><span class="sxs-lookup"><span data-stu-id="96c1f-145">Go to the **Grant permission to an app** page.</span></span> <span data-ttu-id="96c1f-146">Это необходимо сделать, просмотрев имеющиеся appinv.aspx страницы сайта.</span><span class="sxs-lookup"><span data-stu-id="96c1f-146">This must be done by browsing to the appinv.aspx page of the site.</span></span>
    
  <span data-ttu-id="96c1f-147">Пример: `http://{hostname}/{the Site Collection}/_layouts/15/appinv.aspx`.</span><span class="sxs-lookup"><span data-stu-id="96c1f-147">Example: `http://{hostname}/{the Site Collection}/_layouts/15/appinv.aspx`.</span></span> 
    
  > [!NOTE]
  > <span data-ttu-id="96c1f-148">На этом этапе «приложение» относится к надстройки рабочего процесса в общих параметров и не только определенного рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="96c1f-148">The 'app' in this step refers to the workflow add-in in general and not just a specific workflow.</span></span> <span data-ttu-id="96c1f-149">Отдельные рабочие процессы не могут быть контролем доступа.</span><span class="sxs-lookup"><span data-stu-id="96c1f-149">Individual workflows cannot be access controlled.</span></span> <span data-ttu-id="96c1f-150">При включении разрешения надстройки включается для всех рабочих процессов в пределах семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="96c1f-150">When you enable add-in permissions, you are enabling for all workflows within the Site Collection.</span></span> 

  <span data-ttu-id="96c1f-151">Дополнительные сведения о настройке рабочего процесса можно [статья блога из Sympraxis Consulting: циклический через контента в рабочий процесс сайта SharePoint](http://sympmarc.com/series/looping-through-content-in-a-sharepoint-2013-site-workflow/)</span><span class="sxs-lookup"><span data-stu-id="96c1f-151">For more information about setting up a workflow, see the [Blog article from Sympraxis Consulting: Looping Through Content in a SharePoint Site Workflow](http://sympmarc.com/series/looping-through-content-in-a-sharepoint-2013-site-workflow/)</span></span>
    
  <span data-ttu-id="96c1f-152">На следующем рисунке показан пример.</span><span class="sxs-lookup"><span data-stu-id="96c1f-152">The following figure shows an example.</span></span>
 
  ![Пример URL-адреса appinv.aspx и страница.](../images/SPD15-WFAppPermissions4.png)

6. <span data-ttu-id="96c1f-154">Вставьте идентификатор клиента в поле **Код приложения** , а затем выберите **подстановки**, как показано на предыдущем рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-154">Paste the client ID in the **App Id** field, and then select **Lookup**, as shown in the previous figure.</span></span>

7. <span data-ttu-id="96c1f-155">Вставьте следующий код в поле **XML запрашивать разрешения** , чтобы предоставить разрешение "Полный доступ" *(Примечание: этот блок кода обновлен на 12/29/17 для включения `AllowAppOnlyPolicy`)*.</span><span class="sxs-lookup"><span data-stu-id="96c1f-155">Paste the following code in the **Permission Request XML** field to grant full control permission *(note: this code block was updated on 12/29/17 to include the `AllowAppOnlyPolicy`)*.</span></span>
    
  ```XML 
    <AppPermissionRequests AllowAppOnlyPolicy="true">
        <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="FullControl" />
    </AppPermissionRequests>

  ```

  > [!WARNING] 
  > <span data-ttu-id="96c1f-156">Нет нет заполнители в значение **области действия** .</span><span class="sxs-lookup"><span data-stu-id="96c1f-156">There are no placeholders in the **Scope** value.</span></span> <span data-ttu-id="96c1f-157">Это значения литерала.</span><span class="sxs-lookup"><span data-stu-id="96c1f-157">It is a literal value.</span></span> <span data-ttu-id="96c1f-158">Введите его так, как оно указано здесь.</span><span class="sxs-lookup"><span data-stu-id="96c1f-158">Enter it exactly as it appears here.</span></span>

  <span data-ttu-id="96c1f-159">На следующем рисунке показан пример завершенных страницы _(Обратите внимание, что код, приведенный в области **XML запроса разрешений** не отражает последнее обновление для кода на шаге 7)_.</span><span class="sxs-lookup"><span data-stu-id="96c1f-159">The following figure shows an example of the completed page _(note that the code in the **Permission Request XML** area does not reflect the recent update to the code in Step 7)_.</span></span> 
  
  ![Поиск идентификатора приложения.](../images/SPD15-WFAppPermissions5.png)

8. <span data-ttu-id="96c1f-161">Выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-161">Select **Create**.</span></span>
    
9. <span data-ttu-id="96c1f-162">Затем следует доверять надстройкой рабочего процесса, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-162">You are then asked to trust the workflow add-in, as shown in the following figure.</span></span> <span data-ttu-id="96c1f-163">Выберите **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-163">Select **Trust It**.</span></span>
    
  ![Приложение установки доверия для рабочего процесса.](../images/SPD15-WFAppPermissions6.png)
  

## <a name="wrap-actions-inside-an-app-step"></a><span data-ttu-id="96c1f-165">Перенос действия внутри шага приложения</span><span class="sxs-lookup"><span data-stu-id="96c1f-165">Wrap actions inside an App Step</span></span>

<span data-ttu-id="96c1f-p113">Наконец необходимо перенести действия рабочего процесса внутри шага приложения. **Отправка сообщения электронной почты** действие внутри шага приложения переносится по указанные ниже действия. Рабочий процесс в этом примере отправляет сообщение электронной почты подтверждение из настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="96c1f-p113">Finally, you need to wrap the workflow actions inside an App Step. The following procedure wraps a **Send an Email** action inside an App Step. The workflow in this example sends an acknowledgement email message from a custom list.</span></span>

### <a name="to-wrap-actions-inside-an-app-step"></a><span data-ttu-id="96c1f-169">Перенос действия внутри шага приложения</span><span class="sxs-lookup"><span data-stu-id="96c1f-169">To wrap actions inside an App Step</span></span>

1. <span data-ttu-id="96c1f-170">Откройте сайт каталога приложений в SharePoint Designer.</span><span class="sxs-lookup"><span data-stu-id="96c1f-170">Open the App Catalog site in SharePoint Designer.</span></span>    
  
2. <span data-ttu-id="96c1f-171">Создайте новый настраиваемый список, для которого нужно запустить рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="96c1f-171">Create a new Custom List on which to run the workflow.</span></span> <span data-ttu-id="96c1f-172">В этом примере имя списка — **Демонстрационная версия приложения**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-172">In this example, the list name is **App Demo**.</span></span>    
  
3. <span data-ttu-id="96c1f-173">Выберите **рабочие процессы** в окне навигации.</span><span class="sxs-lookup"><span data-stu-id="96c1f-173">Select **Workflows** in the navigation window.</span></span>    
  
4. <span data-ttu-id="96c1f-174">Создание нового **Рабочего процесса списка** для списка **Демонстрационная версия приложения** , как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-174">Create a new **List Workflow** for the **App Demo** list, as shown in the figure.</span></span>

  ![Создание нового рабочего процесса списка.](../images/SPD15-WFAppPermissions7.png)

5. <span data-ttu-id="96c1f-176">Вставка **Шага приложения**, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-176">Insert an **App Step**, as shown in the figure.</span></span>
    
  ![Добавление шага приложения.](../images/SPD15-WFAppPermissions8.png)

6. <span data-ttu-id="96c1f-178">Вставка действие **отправки сообщения электронной почты** на **Шаге приложение**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-178">Insert a **Send an Email** action in the **App Step**.</span></span>
 
7. <span data-ttu-id="96c1f-179">Нажмите кнопку **адресной книги** .</span><span class="sxs-lookup"><span data-stu-id="96c1f-179">Select the **Address book** button.</span></span> <span data-ttu-id="96c1f-180">В **поле** Выбор **Поиска рабочего процесса для пользователя**и выберите команду **Добавить** , как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-180">In the **To** field, select **Workflow Lookup for a User**, and then select **Add** as shown in the figure.</span></span>

  ![Выбор поиска рабочего процесса для пользователя.](../images/SPD15-WFAppPermissions9.png)
  
8. <span data-ttu-id="96c1f-182">Введите **в поле** в качестве искомого значения, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-182">Enter the **Created By** field as the lookup value, as shown in the figure.</span></span>

  ![Диалоговое окно "Поиск человека".](../images/SPD15-WFAppPermissions10.png)
  
9. <span data-ttu-id="96c1f-184">Введите **электронной почты** в списке **Демонстрационная версия приложения** в теле сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="96c1f-184">Enter **Email** from the **App Demo** list in the email message body.</span></span>
     
10. <span data-ttu-id="96c1f-185">Выберите **кнопку ОК** , чтобы вернуться в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="96c1f-185">Select **OK** to return to the workflow.</span></span> <span data-ttu-id="96c1f-186">Завершенный рабочий процесс показан на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-186">The completed workflow is shown in the figure.</span></span>

  ![Действие электронной почты в шаге уровня приложения.](../images/SPD15-WFAppPermissions11.png)
    
11. <span data-ttu-id="96c1f-188">Выберите значок **Параметры рабочих процессов** на ленте, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-188">Select the **Workflow Settings** icon in the ribbon, as shown in the figure.</span></span>
    
  ![Значок "Параметры рабочего процесса" на ленте.](../images/SPD15-WFAppPermissions12.png)

12. <span data-ttu-id="96c1f-190">Снимите флажок **автоматически обновлять состояние рабочего процесса на текущее имя рабочей области**и затем выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="96c1f-190">Clear the check box next to **Automatically update the workflow status to the current stage name**, and then select **Publish**.</span></span>
    
  ![Снятие флажка автоматических обновлений и публикация.](../images/SPD15-WFAppPermissions13.png)
  

<span data-ttu-id="96c1f-192"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="96c1f-192"></span></span>

## <a name="understand-how-it-works"></a><span data-ttu-id="96c1f-193">Понять, как это работает</span><span class="sxs-lookup"><span data-stu-id="96c1f-193">Understand how it works</span></span>

<span data-ttu-id="96c1f-194">Чтобы понять, почему повышению уровня разрешений для рабочего процесса является обязательным, необходимо учитывайте, что рабочие процессы — это базовая надстройки для SharePoint, и следуют в соответствии с правилами авторизации модели надстройки.</span><span class="sxs-lookup"><span data-stu-id="96c1f-194">To understand why elevating permissions for a workflow is required, consider that workflows are fundamentally add-ins for SharePoint, and they follow the same authorization rules of the add-in model.</span></span> <span data-ttu-id="96c1f-195">Конфигурация по умолчанию для рабочего процесса является действующие разрешения рабочего процесса пересечения разрешения пользователей и разрешения надстройки, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="96c1f-195">The default configuration for workflow is that the effective permissions of the workflow are an intersection of user permissions and the add-in permissions, as shown in the figure.</span></span>
    
![Схема разрешений.](../images/SPD15-WFAppPermissions14.png)
  
<span data-ttu-id="96c1f-197">Две причины, почему это необходимо повысить уровень разрешений для создания рабочего процесса в список запросов приложений являются:</span><span class="sxs-lookup"><span data-stu-id="96c1f-197">Two reasons why it is necessary to elevate permissions to create a workflow in the App Request list are:</span></span>

- <span data-ttu-id="96c1f-198">По умолчанию рабочего процесса только есть разрешения на запись.</span><span class="sxs-lookup"><span data-stu-id="96c1f-198">By default, workflow only has write permission.</span></span>

- <span data-ttu-id="96c1f-199">Пользователь не имеет разрешений.</span><span class="sxs-lookup"><span data-stu-id="96c1f-199">The user has no permissions.</span></span>
  
<span data-ttu-id="96c1f-p118">Первый шаг для решения этой проблемы  разрешить приложению авторизуйте, используя только его удостоверение и игнорирование от пользователя. Это делается, включив функцию шаг приложения. Второй шаг предоставляется разрешение на полный доступ с рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="96c1f-p118">The first step to solve this problem is to allow the application to authorize by using only its identity and ignoring that of the user. This is done by enabling the App Step feature. The second step grants full control permission to the workflow.</span></span> 
  
<span data-ttu-id="96c1f-203">На следующем рисунке показано изменение разрешений.</span><span class="sxs-lookup"><span data-stu-id="96c1f-203">The following diagram illustrates the change in permissions.</span></span>
  
![Матрица разрешений.](../images/SPD15-WFAppPermissions15.png)
  
<span data-ttu-id="96c1f-205"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="96c1f-205"></span></span>

## <a name="see-also"></a><span data-ttu-id="96c1f-206">См. также</span><span class="sxs-lookup"><span data-stu-id="96c1f-206">See also</span></span>

- [<span data-ttu-id="96c1f-207">Статье блога группы разработчиков SharePoint Designer: рабочий процесс упаковки и развертывания сценарий</span><span class="sxs-lookup"><span data-stu-id="96c1f-207">Blog article from the SharePoint Designer team: Workflow package and deploy scenario</span></span>](https://blogs.msdn.microsoft.com/sharepointdesigner/2012/08/29/packaging-sharepoint-2013-list-site-and-reusable-workflow-and-how-to-deploy-the-package/)
- [<span data-ttu-id="96c1f-208">Новые возможности рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="96c1f-208">What's new in workflow in SharePoint</span></span>](what-s-new-in-workflows-for-sharepoint.md)
- [<span data-ttu-id="96c1f-209">Начало работы с рабочими процессами SharePoint</span><span class="sxs-lookup"><span data-stu-id="96c1f-209">Getting started with SharePoint workflow</span></span>](get-started-with-workflows-in-sharepoint.md) 
- [<span data-ttu-id="96c1f-210">Справочник по действий рабочих процессов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="96c1f-210">Workflow actions and activities reference for SharePoint</span></span>](workflow-actions-and-activities-reference-for-sharepoint.md)
- [<span data-ttu-id="96c1f-211">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="96c1f-211">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)

    
