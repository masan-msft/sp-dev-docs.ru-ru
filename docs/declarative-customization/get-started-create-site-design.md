---
title: "Приступая к созданию макетов и скриптов сайтов SharePoint"
description: "Узнайте, как приступить к созданию макетов и скриптов сайтов SharePoint, с помощью которых пользователи смогут создавать собственные сайты."
ms.date: 01/08/2018
ms.openlocfilehash: 5781898dc7c2b7a8905003f8584a62470ef1fb9c
ms.sourcegitcommit: 9f492519d4eeb3f62a1fddc71cdca79263651a56
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="get-started-creating-site-designs-and-site-scripts"></a><span data-ttu-id="aba4d-103">Приступая к созданию макетов и скриптов сайтов</span><span class="sxs-lookup"><span data-stu-id="aba4d-103">Get started creating site designs and site scripts</span></span>

> [!NOTE]
> <span data-ttu-id="aba4d-104">Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="aba4d-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="aba4d-105">В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.</span><span class="sxs-lookup"><span data-stu-id="aba4d-105">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="aba4d-106">Создавая макеты сайтов, вы можете предоставлять пользователям пригодные для повторного использования списки, темы, макеты, страницы или дополнительные действия, чтобы они могли быстро создавать сайты SharePoint с нужными им функциями.</span><span class="sxs-lookup"><span data-stu-id="aba4d-106">You can create site designs to provide reusable lists, themes, layouts, pages, or custom actions so that your users can quickly build new SharePoint sites with the features they need.</span></span> <span data-ttu-id="aba4d-107">В этой статье описывается создание примера макета сайта, добавляющего список SharePoint для отслеживания заказов от клиентов.</span><span class="sxs-lookup"><span data-stu-id="aba4d-107">This article describes how to build a simple site design that adds a SharePoint list for tracking customer orders.</span></span> <span data-ttu-id="aba4d-108">Мы создадим при помощи этого макета новый сайт SharePoint с настраиваемым списком.</span><span class="sxs-lookup"><span data-stu-id="aba4d-108">You'll use the site design to create a new SharePoint site with the custom list.</span></span>

<span data-ttu-id="aba4d-109">В этой статье показано, как создавать скрипты и макеты сайтов с помощью командлетов PowerShell для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="aba4d-109">This article shows how to use SharePoint PowerShell cmdlets to create site scripts and site designs.</span></span> <span data-ttu-id="aba4d-110">Эти действия также можно выполнять с помощью интерфейсов REST API.</span><span class="sxs-lookup"><span data-stu-id="aba4d-110">You can also use REST APIs to perform the same actions.</span></span> <span data-ttu-id="aba4d-111">На каждом этапе для справки представлены соответствующие вызовы REST.</span><span class="sxs-lookup"><span data-stu-id="aba4d-111">The corresponding REST calls are shown for reference in each step.</span></span>

## <a name="create-the-site-script-in-json"></a><span data-ttu-id="aba4d-112">Создание скрипта сайта в JSON</span><span class="sxs-lookup"><span data-stu-id="aba4d-112">Create the site script in JSON</span></span>

<span data-ttu-id="aba4d-113">Макет сайта — это набор действий, которые SharePoint выполняет при создании сайта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-113">A site design is a collection of actions that SharePoint will run when creating a new site.</span></span> <span data-ttu-id="aba4d-114">Эти действия описывают изменения, применяемые к новому сайту, такие как создание списка или применение темы.</span><span class="sxs-lookup"><span data-stu-id="aba4d-114">Actions describe changes to apply to the new site, such as creating a new list, or applying a theme.</span></span> <span data-ttu-id="aba4d-115">Действия указываются в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="aba4d-115">The actions are specified in a JSON script.</span></span> <span data-ttu-id="aba4d-116">Скрипт JSON — это список всех выполняемых действий.</span><span class="sxs-lookup"><span data-stu-id="aba4d-116">The JSON script is a list of all actions to apply.</span></span> <span data-ttu-id="aba4d-117">При запуске скрипта SharePoint выполняет все действия в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="aba4d-117">When a script runs, SharePoint completes each action in the order listed.</span></span>

<span data-ttu-id="aba4d-118">Каждое действие указывается значением verb в скрипте JSON.</span><span class="sxs-lookup"><span data-stu-id="aba4d-118">Each action is specified by the "verb" value in the JSON script.</span></span> <span data-ttu-id="aba4d-119">Кроме того, в действия могут быть вложены другие действия, также представляющие собой значения verb.</span><span class="sxs-lookup"><span data-stu-id="aba4d-119">Also, actions can have subactions which are also "verb" values.</span></span> <span data-ttu-id="aba4d-120">В приведенном ниже коде JSON скрипт создает список с именем Customer Tracking, а затем вложенные действия задают описание и добавляют несколько полей, чтобы определить список.</span><span class="sxs-lookup"><span data-stu-id="aba4d-120">In the JSON below, the script specifies to create a new list named Customer Tracking, and then subactions set the description and add several fields to define the list.</span></span>

1. <span data-ttu-id="aba4d-121">Скачайте и установите [командную консоль SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="aba4d-121">Download and install the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span> <span data-ttu-id="aba4d-122">Если у вас уже установлена консоль предыдущей версии, сначала удалите ее, а затем установите последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="aba4d-122">If you already have a previous version of the shell installed, uninstall it first and then install the latest version.</span></span>
1. <span data-ttu-id="aba4d-123">Подключитесь к клиенту SharePoint, следуя инструкциям в статье [Подключение к PowerShell в SharePoint Online](https://technet.microsoft.com/ru-RU/library/fp161372.aspx).</span><span class="sxs-lookup"><span data-stu-id="aba4d-123">Follow the instructions at [Connect to SharePoint Online PowerShell](https://technet.microsoft.com/ru-RU/library/fp161372.aspx) to connect to your SharePoint tenant.</span></span>
1. <span data-ttu-id="aba4d-124">Создайте код JSON с описанием нового скрипта и назначьте его переменной, как показано в приведенном ниже фрагменте кода PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aba4d-124">Create and assign the JSON that describes the new script to a variable as shown in the following PowerShell code.</span></span>

 ```powershell
$site_script = @'
{
    "$schema": "schema.json",
        "actions": [
            {
                "verb": "createSPList",
                "listName": "Customer Tracking",
                "templateType": 100,
                "subactions": [
                    {
                        "verb": "SetDescription",
                        "description": "List of Customers and Orders"
                    },
                    {
                        "verb": "addSPField",
                        "fieldType": "Text",
                        "displayName": "Customer Name",
                        "isRequired": false,
                        "addToDefaultView": true
                    },
                    {
                        "verb": "addSPField",
                        "fieldType": "Number",
                        "displayName": "Requisition Total",
                        "addToDefaultView": true,
                        "isRequired": true
                    },
                    {
                        "verb": "addSPField",
                        "fieldType": "User",
                        "displayName": "Contact",
                        "addToDefaultView": true,
                        "isRequired": true
                    },
                    {
                        "verb": "addSPField",
                        "fieldType": "Note",
                        "displayName": "Meeting Notes",
                        "isRequired": false
                    }
                ]
            }
        ],
            "bindata": { },
    "version": 1
}
'@
```

<span data-ttu-id="aba4d-125">Приведенный выше скрипт создаст список SharePoint с именем Customer Tracking.</span><span class="sxs-lookup"><span data-stu-id="aba4d-125">The previous script will create a new SharePoint list named Customer Tracking.</span></span> <span data-ttu-id="aba4d-126">Он задаст описание, а также добавит в список четыре поля.</span><span class="sxs-lookup"><span data-stu-id="aba4d-126">It will set the description, and also add four fields to the list.</span></span> <span data-ttu-id="aba4d-127">Обратите внимание на то, что все они считаются действиями.</span><span class="sxs-lookup"><span data-stu-id="aba4d-127">Note that each of these are considered an action.</span></span> <span data-ttu-id="aba4d-128">Скрипты сайта ограничены 30 кумулятивными действиями (для одного или нескольких скриптов, которые могут быть вызваны в макете сайта).</span><span class="sxs-lookup"><span data-stu-id="aba4d-128">Site scripts are limited to 30 cumulative actions (across one or more scripts that may be called in a site design).</span></span>

## <a name="add-the-site-script"></a><span data-ttu-id="aba4d-129">Добавление скрипта сайта</span><span class="sxs-lookup"><span data-stu-id="aba4d-129">Add the site script</span></span>

<span data-ttu-id="aba4d-130">Каждый скрипт сайта должен быть зарегистрирован в SharePoint, чтобы он был доступен.</span><span class="sxs-lookup"><span data-stu-id="aba4d-130">Each site script must be registered in SharePoint so that it is available to.</span></span> <span data-ttu-id="aba4d-131">Добавьте новый макет сайта с помощью командлета **Add-SPOSiteScript**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-131">Add a new site design by using the **Add-SPOSiteScript** cmdlet.</span></span> <span data-ttu-id="aba4d-132">В приведенном ниже примере показано, как добавить вышеописанный скрипт JSON.</span><span class="sxs-lookup"><span data-stu-id="aba4d-132">The following example shows how to add the JSON script described previously.</span></span>

```powershell
C:\> Add-SPOSiteScript -Title "Create customer tracking list" -Content $site_script -Description "Creates list for tracking customer contact information"
```

<span data-ttu-id="aba4d-133">Результат выполнения командлета будет включать свойство **ID** добавленного скрипта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-133">After running the cmdlet you will get a result that lists the site script **ID** of the added script.</span></span> <span data-ttu-id="aba4d-134">Запишите этот ИД, так как он потребуется позже, при создании макета сайта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-134">Keep track of this ID somewhere because you will need it later when you create the site design.</span></span>

<span data-ttu-id="aba4d-135">Для добавления скрипта сайта используется REST API **CreateSiteScript**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-135">The REST API to add a new site script is **CreateSiteScript**.</span></span>

## <a name="create-the-site-design"></a><span data-ttu-id="aba4d-136">Создание макета сайта</span><span class="sxs-lookup"><span data-stu-id="aba4d-136">Create the site design</span></span>

<span data-ttu-id="aba4d-137">Теперь необходимо создать макет сайта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-137">Next you need to create the site design.</span></span> <span data-ttu-id="aba4d-138">Он будет отображаться в раскрывающемся списке, когда пользователь создает сайт на основе одного из шаблонов.</span><span class="sxs-lookup"><span data-stu-id="aba4d-138">The site design will appear in a drop down list when someone creates a new site from one of the templates.</span></span> <span data-ttu-id="aba4d-139">На нем может выполняться один или несколько уже добавленных скриптов.</span><span class="sxs-lookup"><span data-stu-id="aba4d-139">It can run one or more site scripts that have already been added.</span></span>

- <span data-ttu-id="aba4d-140">Выполните приведенный ниже командлет, чтобы добавить макет сайта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-140">Run the following cmdlet to add a new site design.</span></span> <span data-ttu-id="aba4d-141">Замените \<ID\> на ИД добавленного вами скрипта сайта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-141">Replace \<ID\> with the site script ID from when you added the site script.</span></span>

```powershell
C:\> Add-SPOSiteDesign -Title "Contoso customer tracking" -WebTemplate "64" -SiteScripts "<ID>" -Description "Tracks key customer data in a list"
```

<span data-ttu-id="aba4d-142">Приведенный выше командлет создает макет сайта с именем Contoso customer tracking.</span><span class="sxs-lookup"><span data-stu-id="aba4d-142">The previous cmdlet creates a new site design named Contoso customer tracking.</span></span> <span data-ttu-id="aba4d-143">Значение -WebTemplate указывает, с каким базовым шаблоном он будет связан.</span><span class="sxs-lookup"><span data-stu-id="aba4d-143">The -WebTemplate value selects which base template to associate with.</span></span> <span data-ttu-id="aba4d-144">Значение 64 обозначает шаблон сайта группы, а значение 68 — шаблон сайта для общения.</span><span class="sxs-lookup"><span data-stu-id="aba4d-144">The value "64" indicates Team site template, and the value "68" indicates the communication site template.</span></span>

<span data-ttu-id="aba4d-145">В отклике JSON будет отображаться свойство **ID** нового макета сайта.</span><span class="sxs-lookup"><span data-stu-id="aba4d-145">The JSON response will display the **ID** of the new site design.</span></span> <span data-ttu-id="aba4d-146">Вы можете обновить или изменить макет сайта в последующих командлетах.</span><span class="sxs-lookup"><span data-stu-id="aba4d-146">You can use in subsequent cmdlets to update or modify the site design.</span></span>

<span data-ttu-id="aba4d-147">Для добавления макета сайта используется REST API **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-147">The REST API to add a new site design is **CreateSiteDesign**.</span></span>

## <a name="use-the-new-site-design"></a><span data-ttu-id="aba4d-148">Использование нового макета сайта</span><span class="sxs-lookup"><span data-stu-id="aba4d-148">Use the new site design</span></span>

<span data-ttu-id="aba4d-149">Теперь, когда мы добавили скрипт и макет сайта, с их помощью можно создавать сайты.</span><span class="sxs-lookup"><span data-stu-id="aba4d-149">Now that you've added a site script and site design, you can use it to create new sites.</span></span>

1. <span data-ttu-id="aba4d-150">Перейдите на домашнюю страницу сайта SharePoint, который используется для разработки.</span><span class="sxs-lookup"><span data-stu-id="aba4d-150">Go to the home page of the SharePoint site you are using for development.</span></span>
1. <span data-ttu-id="aba4d-151">Нажмите **Создать сайт**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-151">Choose **Create site**.</span></span>
1. <span data-ttu-id="aba4d-152">Выберите **Сайт группы**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-152">Choose **Team site**.</span></span>
1. <span data-ttu-id="aba4d-153">В раскрывающемся списке **Выберите оформление** щелкните свой макет сайта **Customer orders**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-153">In the **Choose a design** drop down, select your site design **customer orders**.</span></span>
1. <span data-ttu-id="aba4d-154">В поле "Имя сайта" введите имя нового сайта — **Учет заказов от клиентов**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-154">In Site name enter a name for the new site **Customer order tracking**.</span></span>
1. <span data-ttu-id="aba4d-155">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-155">Choose **Next**.</span></span>
1. <span data-ttu-id="aba4d-156">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-156">Choose **Finish**.</span></span>
1. <span data-ttu-id="aba4d-157">В области будет показано, что применяется скрипт.</span><span class="sxs-lookup"><span data-stu-id="aba4d-157">A pane will indicate that your script is being applied.</span></span> <span data-ttu-id="aba4d-158">По завершении нажмите **Просмотреть обновленный сайт**.</span><span class="sxs-lookup"><span data-stu-id="aba4d-158">When it is done, choose **View updated site**.</span></span>
1. <span data-ttu-id="aba4d-159">На странице появится настраиваемый список.</span><span class="sxs-lookup"><span data-stu-id="aba4d-159">You will see the custom list on the page.</span></span>
