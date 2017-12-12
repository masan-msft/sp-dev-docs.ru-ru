---
title: "Таксономия операции примера приложения для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 32e7b535103dd20a988c1253afe7f505d6c0e6f0
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="taxonomy-operations-sample-app-for-sharepoint"></a><span data-ttu-id="9349f-102">Таксономия операции примера приложения для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9349f-102">Taxonomy operations sample app for SharePoint</span></span>

<span data-ttu-id="9349f-103">В рамках стратегии Enterprise Content Management (ECM) можно создавать и чтение данных таксономии для списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9349f-103">As part of your Enterprise Content Management (ECM) strategy, you can create and read taxonomy data on a SharePoint list.</span></span>
    
<span data-ttu-id="9349f-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9349f-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="9349f-105">Образец консольного приложения Core.MMS показано, как для взаимодействия со службой управляемых метаданных для создания и извлечения терминов, наборов терминов и группы.</span><span class="sxs-lookup"><span data-stu-id="9349f-105">The Core.MMS sample console application shows you how to interact with the SharePoint managed metadata service to create and retrieve terms, term sets, and groups.</span></span> <span data-ttu-id="9349f-106">В этом примере также будет выполняться в размещенном у поставщика приложения, например веб-приложение ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9349f-106">This sample will also run in a provider-hosted app, such as an ASP.NET MVC web application.</span></span> <span data-ttu-id="9349f-107">Используйте это решение, чтобы перенести условия между фермами SharePoint или отображение термины в пользовательское приложение.</span><span class="sxs-lookup"><span data-stu-id="9349f-107">Use this solution if you want to migrate terms between SharePoint farms or display terms in your custom app.</span></span>   

## <a name="before-you-begin"></a><span data-ttu-id="9349f-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9349f-108">Before you begin</span></span>
<span data-ttu-id="9349f-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9349f-109"></span></span>

<span data-ttu-id="9349f-110">Чтобы начать работу, загрузите [Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) пример приложения из project [для разработчиков Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="9349f-110">To get started, download the  [Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) sample app from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="9349f-111">Перед запуском этого приложения, то необходимо:</span><span class="sxs-lookup"><span data-stu-id="9349f-111">Before you run this app, you'll need:</span></span>

- <span data-ttu-id="9349f-112">URL-адрес сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9349f-112">The URL of your SharePoint site.</span></span>
    
- <span data-ttu-id="9349f-113">Разрешения на доступ к термин хранилища в службе управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="9349f-113">Permission to access the term store in the managed metadata service.</span></span> <span data-ttu-id="9349f-114">На рисунке 1 показано центра администрирования Office 365, в которых назначаются разрешения.</span><span class="sxs-lookup"><span data-stu-id="9349f-114">Figure 1 shows the Office 365 admin center where these permissions are assigned.</span></span> 
    
    <span data-ttu-id="9349f-115">**На рисунке 1. Предоставление разрешений на термин хранения в центре администрирования SharePoint**</span><span class="sxs-lookup"><span data-stu-id="9349f-115">**Figure 1. Assigning permissions to the term store in the SharePoint admin center**</span></span>

    ![Снимок экрана центра администрирования SharePoint с банка терминов, полях администраторов хранилища терминов и поля поиска хранилища терминов таксономии с выделением.](media/5a9d8c07-afce-4d9e-b0d1-10b28e089278.png)
    
<span data-ttu-id="9349f-117">Назначение разрешений для хранилища терминов:</span><span class="sxs-lookup"><span data-stu-id="9349f-117">To assign permissions to the term store:</span></span>

  1. <span data-ttu-id="9349f-118">В центре администрирования Office 365 выберите команду **хранилища терминов**.</span><span class="sxs-lookup"><span data-stu-id="9349f-118">From the Office 365 admin center, choose  **term store**.</span></span>
    
  2. <span data-ttu-id="9349f-119">В **Банк ТЕРМИНОВ ТАКСОНОМИИ**выберите набор терминов, что необходимо назначить администратору.</span><span class="sxs-lookup"><span data-stu-id="9349f-119">In  **TAXONOMY TERM STORE**, choose the term set that you want to assign an administrator to.</span></span>
    
  3. <span data-ttu-id="9349f-120">В группе **Администраторов хранилища терминов**введите учетная запись организации, который требует разрешений администратора для хранилища терминов.</span><span class="sxs-lookup"><span data-stu-id="9349f-120">In  **Term Store Administrators**, enter the organizational account that requires term store administrator permissions.</span></span>

## <a name="using-the-coremms-sample-app"></a><span data-ttu-id="9349f-121">Использование примера приложения Core.MMS</span><span class="sxs-lookup"><span data-stu-id="9349f-121">Using the Core.MMS sample app</span></span>
<span data-ttu-id="9349f-122"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9349f-122"></span></span>

<span data-ttu-id="9349f-123">При запуске приложения появится консольное приложение, как на рис.</span><span class="sxs-lookup"><span data-stu-id="9349f-123">When you start the app, you see a console application similar to Figure 2.</span></span> <span data-ttu-id="9349f-124">Вам будет предложено ввести URL-адрес сайта SharePoint 2013 или SharePoint Online и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="9349f-124">You are prompted to enter the URL of your SharePoint 2013 or SharePoint Online site and your credentials.</span></span> 

<span data-ttu-id="9349f-125">**На рисунке 2. Core.MMS консольного приложения**</span><span class="sxs-lookup"><span data-stu-id="9349f-125">**Figure 2. Core.MMS console application**</span></span>

![Снимок экрана консоли приложения Core.MMS пример вывода запроса на SharePoint имя пользователя и пароль.](media/5ddaf3f1-2d7c-4818-9a9a-b0e905226db5.png)

<span data-ttu-id="9349f-127">После указать URL-адрес SharePoint и учетные данные, происходит проверка подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="9349f-127">After you supply the SharePoint URL and your credentials, user authentication occurs.</span></span> <span data-ttu-id="9349f-128">Следующий код выполняет проверку подлинности пользователя в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="9349f-128">The following code performs user authentication in SharePoint Online.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="9349f-129">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="9349f-129">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online.
cc.Credentials = new SharePointOnlineCredentials(userName, pwd);
```

<span data-ttu-id="9349f-130">Следующий код выполняет проверку подлинности пользователя в SharePoint Online выделенных или в локальной ферме SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="9349f-130">The following code performs user authentication in SharePoint Online Dedicated or in an on-premises SharePoint 2013 farm.</span></span>

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online Dedicated or on-premises .
cc.Credentials = new NetworkCredential(userName, pwd);
```

<span data-ttu-id="9349f-131">Метод **CreateNecessaryMMSTermsToCloud** создает группу, набор терминов и несколько терминов службы управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="9349f-131">The  **CreateNecessaryMMSTermsToCloud** method creates a group, term set, and several terms in the managed metadata service.</span></span> <span data-ttu-id="9349f-132">Код сначала получает ссылку на объект **TaxonomySession** , затем объекта **банка терминов** , перед созданием настраиваемых **TermGroup**, **TermSet**и новых терминов.</span><span class="sxs-lookup"><span data-stu-id="9349f-132">The code first gets a reference to the **TaxonomySession** object, then the **TermStore** object, before creating the custom **TermGroup**,  **TermSet**, and new terms.</span></span> 

```C#
private static void CreateNecessaryMMSTermsToCloud(ClientContext cc)
        {
            // Get access to taxonomy CSOM.
            TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(cc);
            cc.Load(taxonomySession);
            cc.ExecuteQuery();

            if (taxonomySession != null)
            {
                TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
                if (termStore != null)
                {
                    //
                    // Create group, termset, and terms.
                    //
                    TermGroup myGroup = termStore.CreateGroup("Custom", Guid.NewGuid());
                    TermSet myTermSet = myGroup.CreateTermSet("Colors", Guid.NewGuid(), 1033);
                    myTermSet.CreateTerm("Red", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Orange", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Yellow", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Green", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Blue", 1033, Guid.NewGuid());
                    myTermSet.CreateTerm("Purple", 1033, Guid.NewGuid());

                    cc.ExecuteQuery();
                }
            }
        }
```

<span data-ttu-id="9349f-133">После создания новых терминов, метод **GetMMSTermsFromCloud()** получает все группы терминов, наборов терминов и термины из службы управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="9349f-133">After creating the new terms, the  **GetMMSTermsFromCloud()** method retrieves all term groups, term sets, and terms from the managed metadata service.</span></span> <span data-ttu-id="9349f-134">Как и метод **CreateNecessaryMMSTermsToCloud()** , код сначала получает ссылку на объект **TaxonomySession** , затем объект **банка терминов** , прежде чем получение и отображение сведений терминов.</span><span class="sxs-lookup"><span data-stu-id="9349f-134">Similar to the **CreateNecessaryMMSTermsToCloud()** method, the code first gets a reference to the **TaxonomySession** object, then the **TermStore** object, before retrieving and displaying the term information.</span></span>

```C#
private static void GetMMSTermsFromCloud(ClientContext cc)
        {
            //
            // Load up the taxonomy item names.
            //
            TaxonomySession taxonomySession = TaxonomySession.GetTaxonomySession(cc);
            TermStore termStore = taxonomySession.GetDefaultSiteCollectionTermStore();
            cc.Load(termStore,
                    store => store.Name,
                    store => store.Groups.Include(
                        group => group.Name,
                        group => group.TermSets.Include(
                            termSet => termSet.Name,
                            termSet => termSet.Terms.Include(
                                term => term.Name)
                        )
                    )
            );
            cc.ExecuteQuery();

            //
            // Writes the taxonomy item names.
            //
            if (taxonomySession != null)
            {
                if (termStore != null)
                {
                    foreach (TermGroup group in termStore.Groups)
                    {
                        Console.WriteLine("Group " + group.Name);

                        foreach (TermSet termSet in group.TermSets)
                        {
                            Console.WriteLine("TermSet " + termSet.Name);

                            foreach (Term term in termSet.Terms)
                            {
                                // Writes root-level terms only.
                                Console.WriteLine("Term " + term.Name);
                            }
                        }
                    }
                }
            }
        }
```

<span data-ttu-id="9349f-135">Вы увидите терминов данные из службы управляемых метаданных отображается в консольное приложение, как показано на рисунке 3 и в срок хранения в службе управляемых метаданных, как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="9349f-135">You will see your term data from your managed metadata service displayed in the console application, as shown in Figure 3, and in the term store in your managed metadata service, as shown in Figure 4.</span></span>

<span data-ttu-id="9349f-136">**На рисунке 3. Консольное приложение, отображение группы, наборы терминов и термины в службе управляемых метаданных**</span><span class="sxs-lookup"><span data-stu-id="9349f-136">**Figure 3. Console application showing Groups, TermSets, and Terms in the managed metadata service**</span></span>

![Снимок экрана с консольного приложения с данными терминов вывода.](media/a8907a10-8b4d-463f-89bc-811f9af4b34e.png)

<span data-ttu-id="9349f-138">**На рисунке 4. Центр администрирования SharePoint, отображение группы, наборы терминов и термины в службе управляемых метаданных**</span><span class="sxs-lookup"><span data-stu-id="9349f-138">**Figure 4. SharePoint admin center showing Groups, TermSets, and Terms in the managed metadata service**</span></span>

![Снимок экрана центра администрирования SharePoint с банк терминов таксономии были развернуты.](media/9e623deb-569b-457a-ad1c-fa6d0d4d0a38.png)

## <a name="see-also"></a><span data-ttu-id="9349f-140">См. также</span><span class="sxs-lookup"><span data-stu-id="9349f-140">See also</span></span>
<span data-ttu-id="9349f-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9349f-141"></span></span>

-  [<span data-ttu-id="9349f-142">Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="9349f-142">Enterprise Content Management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [<span data-ttu-id="9349f-143">Пример Core.MMSSync</span><span class="sxs-lookup"><span data-stu-id="9349f-143">Core.MMSSync sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
    
-  [<span data-ttu-id="9349f-144">Пример Core.ContentTypesAndFields</span><span class="sxs-lookup"><span data-stu-id="9349f-144">Core.ContentTypesAndFields sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ContentTypesAndFields)
