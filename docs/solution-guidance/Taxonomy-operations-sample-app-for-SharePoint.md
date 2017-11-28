---
title: "Таксономия операции примера приложения для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: c50bfe1afada0cfe907c4e11c4d2d6c6eb772b41
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="taxonomy-operations-sample-app-for-sharepoint"></a>Таксономия операции примера приложения для SharePoint

В рамках стратегии Enterprise Content Management (ECM) можно создавать и чтение данных таксономии для списка SharePoint.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Образец консольного приложения Core.MMS показано, как для взаимодействия со службой управляемых метаданных для создания и извлечения терминов, наборов терминов и группы. В этом примере также будет выполняться в размещенном у поставщика приложения, например веб-приложение ASP.NET MVC. Используйте это решение, чтобы перенести условия между фермами SharePoint или отображение термины в пользовательское приложение.   

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите [Core.MMS](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS) пример приложения из project [для разработчиков Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Перед запуском этого приложения, то необходимо:

- URL-адрес сайта SharePoint.
    
- Разрешения на доступ к термин хранилища в службе управляемых метаданных. На рисунке 1 показано центра администрирования Office 365, в которых назначаются разрешения. 
    
    **На рисунке 1. Предоставление разрешений на термин хранения в центре администрирования SharePoint**

    ![Снимок экрана центра администрирования SharePoint с банка терминов, полях администраторов хранилища терминов и поля поиска хранилища терминов таксономии с выделением.](media/5a9d8c07-afce-4d9e-b0d1-10b28e089278.png)
    
Назначение разрешений для хранилища терминов:

  1. В центре администрирования Office 365 выберите команду **хранилища терминов**.
    
  2. В **Банк ТЕРМИНОВ ТАКСОНОМИИ**выберите набор терминов, что необходимо назначить администратору.
    
  3. В группе **Администраторов хранилища терминов**введите учетная запись организации, который требует разрешений администратора для хранилища терминов.

## <a name="using-the-coremms-sample-app"></a>Использование примера приложения Core.MMS
<a name="sectionSection1"> </a>

При запуске приложения появится консольное приложение, как на рис. Вам будет предложено ввести URL-адрес сайта SharePoint 2013 или SharePoint Online и учетные данные. 

**На рисунке 2. Core.MMS консольного приложения**

![Снимок экрана консоли приложения Core.MMS пример вывода запроса на SharePoint имя пользователя и пароль.](media/5ddaf3f1-2d7c-4818-9a9a-b0e905226db5.png)

После указать URL-адрес SharePoint и учетные данные, происходит проверка подлинности пользователя. Следующий код выполняет проверку подлинности пользователя в SharePoint Online.
    
**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online.
cc.Credentials = new SharePointOnlineCredentials(userName, pwd);
```

Следующий код выполняет проверку подлинности пользователя в SharePoint Online выделенных или в локальной ферме SharePoint 2013.

```C#
ClientContext cc = new ClientContext(siteUrl);
cc.AuthenticationMode = ClientAuthenticationMode.Default;
// For SharePoint Online Dedicated or on-premises .
cc.Credentials = new NetworkCredential(userName, pwd);
```

Метод **CreateNecessaryMMSTermsToCloud** создает группу, набор терминов и несколько терминов службы управляемых метаданных. Код сначала получает ссылку на объект **TaxonomySession** , затем объекта **банка терминов** , перед созданием настраиваемых **TermGroup**, **TermSet**и новых терминов. 

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

После создания новых терминов, метод **GetMMSTermsFromCloud()** получает все группы терминов, наборов терминов и термины из службы управляемых метаданных. Как и метод **CreateNecessaryMMSTermsToCloud()** , код сначала получает ссылку на объект **TaxonomySession** , затем объект **банка терминов** , прежде чем получение и отображение сведений терминов.

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

Вы увидите терминов данные из службы управляемых метаданных отображается в консольное приложение, как показано на рисунке 3 и в срок хранения в службе управляемых метаданных, как показано на рисунке 4.

**На рисунке 3. Консольное приложение, отображение группы, наборы терминов и термины в службе управляемых метаданных**

![Снимок экрана с консольного приложения с данными терминов вывода.](media/a8907a10-8b4d-463f-89bc-811f9af4b34e.png)

**На рисунке 4. Центр администрирования SharePoint, отображение группы, наборы терминов и термины в службе управляемых метаданных**

![Снимок экрана центра администрирования SharePoint с банк терминов таксономии были развернуты.](media/9e623deb-569b-457a-ad1c-fa6d0d4d0a38.png)

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Управление корпоративным информационным содержимым решений для SharePoint 2013 и SharePoint Online](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
    
-  [Пример Core.MMSSync](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
    
-  [Пример Core.ContentTypesAndFields](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ContentTypesAndFields)
