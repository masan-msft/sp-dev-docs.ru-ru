# <a name="add-first-run-logic-to-the-provider-hosted-add-in"></a><span data-ttu-id="ad689-101">Добавление логики первого запуска в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-101">Add first-run logic to the provider-hosted add-in</span></span>
<span data-ttu-id="ad689-102">Узнайте, как добавить код, выполняемый при первом запуске, в надстройку SharePoint, размещенную у поставщика.</span><span class="sxs-lookup"><span data-stu-id="ad689-102">Learn how to include "first run" code in a provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="ad689-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="ad689-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="ad689-p102">Это восьмая часть серии статей, посвященной основам разработки надстроек, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="ad689-p102">Learn how to include "first run" code in a provider-hosted SharePoint Add-in. This is the eighth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="ad689-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="ad689-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [<span data-ttu-id="ad689-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="ad689-111">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad689-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [<span data-ttu-id="ad689-112">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-112">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="ad689-113">Добавление веб-части надстройки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-113">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="ad689-114">Обработка событий надстройки, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="ad689-114">Handle add-in events in the provider-hosted add-in</span></span>](handle-add-in-events-in-the-provider-hosted-add-in)
    
 

 <span data-ttu-id="ad689-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещенных в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeFirstRunLogic.sln.</span><span class="sxs-lookup"><span data-stu-id="ad689-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeFirstRunLogic.sln file.</span></span>
 

<span data-ttu-id="ad689-p104">В этой статье рассматривается добавление на начальную страницу надстройки SharePoint "Сеть магазинов" такого кода, который проверяет, первый ли это запуск текущего экземпляра надстройки. Если это так, код развернет список **Местные сотрудники** и пользовательскую кнопку ленты.</span><span class="sxs-lookup"><span data-stu-id="ad689-p104">In this article you add code to the start page of the Chain Store SharePoint Add-in that checks to see if the current instance of the add-in is being run for the first time. If it is the first time, your code will deploy the **Local Employees** list and the custom ribbon button.</span></span>
 

## <a name="create-the-basic-class-for-deploying-sharepoint-components"></a><span data-ttu-id="ad689-119">Создание базового класса для развертывания компонентов SharePoint</span><span class="sxs-lookup"><span data-stu-id="ad689-119">Create the basic class for deploying SharePoint components</span></span>


 

 

 <span data-ttu-id="ad689-p105">**Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений** и выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="ad689-p105">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
 


1. <span data-ttu-id="ad689-123">В проекте **ChainStoreWeb** в **обозревателе решений** щелкните правой кнопкой мыши папку **Утилиты** и выберите пункты **Добавить | Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="ad689-123">In the **ChainStoreWeb** project in **Solution Explorer**, right-click the **Utilities** folder and select **Add | Existing Item**.</span></span>
    
 
2. <span data-ttu-id="ad689-124">В открывшемся окне **проводника** перейдите к папке решения (**ChainStoreWeb**) и откройте папку **Utilities**.</span><span class="sxs-lookup"><span data-stu-id="ad689-124">In the **File Explorer** that opens navigate to the solution folder, the **ChainStoreWeb** folder, and then open the **Utilities** folder.</span></span>
    
 
3. <span data-ttu-id="ad689-125">Выберите файл SharePointComponentDeployer.cs и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ad689-125">Select SharePointComponentDeployer.cs and press **Add**.</span></span>
    
 
4. <span data-ttu-id="ad689-p106">Откройте файл SharePointComponentDeployer.cs. Он содержит статический класс и два статических метода, которые получают и задают версию надстройки в таблице **Клиенты** из корпоративной базы данных. Мы не будем рассматривать эти методы, так как эта серия статей не посвящена программированию на ASP.NET или SQL Server/Azure.</span><span class="sxs-lookup"><span data-stu-id="ad689-p106">Open the file SharePointComponentDeployer.cs. It has a static class and two static methods that get and set the add-in's version in the **Tenants** table of the corporate database. We won't discuss these methods because this series of articles is not intended to teach ASP.NET or SQL Server/Azure programming.</span></span>
    
 
5. <span data-ttu-id="ad689-129">Добавьте указанные ниже операторы **using** в начале файла.</span><span class="sxs-lookup"><span data-stu-id="ad689-129">Add the following **using** statements to the top of the file.</span></span>
    
```
  using System.Web;
using System.Linq;
using System.Collections.Generic;
using Microsoft.SharePoint.Client;
```

6. <span data-ttu-id="ad689-p107">В начале класса  `SharePointComponentDeployer` добавьте два указанных ниже статических поля. Инициализация обеих полей будет выполняться в методе **Page_Load** начальной страницы надстройки. Вы добавите этот код на одном из следующих этапов. В первом поле будет храниться объект **SharePointContext**, необходимый для выполнения операций CRUD в SharePoint. Во втором поле номер версии надстройки, установленной на хост-сайте. Изначально (когда обработчик установки регистрирует клиент) это значение будет отличаться от значения, используемого по умолчанию ( **0000.0000.0000.0000** ) и записанного в корпоративной таблице **Tenants** (Клиенты). Например, номер первой версии надстройки будет выглядеть следующим образом: **1.0.0.0**.</span><span class="sxs-lookup"><span data-stu-id="ad689-p107">At the top of the  `SharePointComponentDeployer` class, add the following two static fields. Both of these will be initialized in the **Page_Load** method of the add-in's start page. You add that code in a later step. The first field will hold the **SharePointContext** object that is needed to make CRUD operations on SharePoint. The second will hold the version number of the add-in that is installed on the host web. This value will initially be different from the default value ( **0000.0000.0000.0000** ) that is recorded in the corporate **Tenants** table when the installation handler registers the tenant. For example, the first version of the add-in will be **1.0.0.0**.</span></span>
    
```C#
  internal static SharePointContext sPContext;
internal static Version localVersion;
```

7. <span data-ttu-id="ad689-p108">Создайте приведенное ниже статическое свойство, в котором будет храниться версия надстройки, которая в текущий момент зарегистрирована в корпоративной таблице **Tenants** (Клиенты). Чтобы получать и задавать это значение, используются два метода, которые уже определены в файле.</span><span class="sxs-lookup"><span data-stu-id="ad689-p108">Create the following static property to hold the version of the add-in that is currently recorded in the corporate **Tenants** table. It uses the two methods that were already in the file to get and set this value.</span></span>
    
```C#
  internal static Version RemoteTenantVersion
{
    get
    {
        return GetTenantVersion();
    }
    set
    {
        SetTenantVersion(value);
    }
}
```

8. <span data-ttu-id="ad689-p109">Теперь создайте приведенное ниже свойство `IsDeployed`. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="ad689-p109">Now create the following  `IsDeployed` property. Note the following about this code:</span></span>
    
      - <span data-ttu-id="ad689-p110">Метод **Page_Load** начальной страницы надстройки будет использовать значение этого свойства, чтобы определить, первый ли это запуск надстройки. Значение **false** указывает, что надстройку раньше не запускали, поэтому необходимо развернуть ее компоненты.</span><span class="sxs-lookup"><span data-stu-id="ad689-p110">The **Page_Load** method of the add-in's start page will use the value of this property to determine whether or not the add-in is running for the first time. A **false** value signals that the add-in has not run before on the current host web, so its components need to be deployed.</span></span>
    
 
  - <span data-ttu-id="ad689-p111">Проверка выполняется путем сравнения номера версии, зарегистрированного в таблице **Tenants** (Клиенты) с номером установленной версии. При первом запуске надстройки первое значение будет меньше. Код, который вы напишете на одном из следующих этапов, задает в таблице **Tenants** номер фактически установленной версии, поэтому при повторном запуске надстройки метод `IsDeployed` вернет значение **true**, что позволит предотвратить повторное выполнение кода, отвечающего за развертывание.</span><span class="sxs-lookup"><span data-stu-id="ad689-p111">The criterion is whether or not the version number registered in the **Tenants** table is lower than the version actually installed. The first time the add-in runs, it will be lower. Code that you write in a later step sets the version in the **Tenants** table to the same version as is actually installed, so when the add-in runs again, `IsDeployed` will return **true** and the deployment logic will not execute again.</span></span>
    
 

```C#
  public static bool IsDeployed
{
    get
    {
        if (RemoteTenantVersion < localVersion)
            return false; 
        else
            return true; 
    }
}
```

9. <span data-ttu-id="ad689-p112">Добавьте указанный ниже метод в класс  `SharePointComponentDeployer`. Обратите внимание, что последнее, что делает метод, обновляет версию зарегистрированного клиента в базе данных предприятия ( **0000.0000.0000.0000** ), чтобы она соответствовала фактической версии надстройки на хост-сайте ( **1.0.0.0** ). Вы закончите этот метод на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="ad689-p112">Add the following method to the  `SharePointComponentDeployer` class. Note that the last thing the method does is update the registered tenant version in the corporate database ( **0000.0000.0000.0000** ) to match the actual version of the add-in on the host web ( **1.0.0.0** ). You will complete this method in a later step.</span></span>
    
```C#
  internal static void DeployChainStoreComponentsToHostWeb(HttpRequest request)
{
    // TODO4: Deployment code goes here.

    RemoteTenantVersion = localVersion;
}
```


 <span data-ttu-id="ad689-p113">**Примечание.** Вас может удивить, что надстройка сравнивает номера версий, чтобы определить ответ на простой логический вопрос: запущена ли надстройка впервые? Ведь мы с таким же успехом могли бы добавить в таблицу **Tenants** простое строковое поле со значением "еще не запускалась" в обработчике установки, а затем изменить его на "уже запускалось" в коде, выполняемом при первом запуске, после развертывания компонентов SharePoint. Для надстройки "Сеть магазинов" простой проверки было бы достаточно. Однако в общем случае рекомендуется использовать номера версий. Это связано с тем, что в будущем надстройки, используемые в рабочей среде, скорее всего будут обновляться "на месте", то есть уже после их установки. В этом случае коду надстройки будет недостаточно двух вариантов: "еще не запускалась" и "уже запускалась". Предположим, что при обновлении надстройки с версии 1.0.0.0 до версии 2.0.0.0 вы хотите добавить новый список на хост-сайт. Вы могли бы сделать это в обработчике событий обновления или в коде, выполняемом при первом запуске после обновления. В любом случае коду, выполняемому при развертывании, потребуется развернуть новые компоненты. Кроме того, ему потребуется не развертывать компоненты, которые были развернуты в предыдущей версии надстройки. Номер версии 1.0.0.0 станет сигналом, указывающим, что компоненты версии 1.0.0.0 уже развернуты, но код, выполняемый при первом запуске после обновления, еще не выполнялся.</span><span class="sxs-lookup"><span data-stu-id="ad689-p113">For the Chain Store add-in, a simple test would work. However, it is generally a good practice to use version numbers. This is because a production add-in is likely to be updated-in-place in the future; that is, updated after it is already installed. When that time comes, your add-in logic will need to be sensitive to more than the two possibilities not-yet-run andalready-run-once. Suppose, for example, that you want to add an additional list to the host web in the upgrade from version 1.0.0.0 to 2.0.0.0. You could do this in an update event handler, or in "first run after update" logic. Either way, your deployment logic will need to deploy new components, but it will also need to avoid trying to redeploy components that were deployed in a previous version of the add-in. A version number of 1.0.0.0 would signal that the components of version 1.0.0.0 have been deployed but that the first-run-after-update logic has not yet run.</span></span>
 


## <a name="add-the-basic-startup-logic"></a><span data-ttu-id="ad689-158">Добавьте базовой логики запуска</span><span class="sxs-lookup"><span data-stu-id="ad689-158">Add the basic startup logic</span></span>


 

 

1. <span data-ttu-id="ad689-p114">Хост-сайт SharePoint должен сообщить удаленному веб-приложению номер версии установленной на нем надстройки. Для этого мы используем параметр запроса. Откройте файл AppManifest.xml в проекте **ChainStore**. В конструкторе вы увидите, что в качестве значения поля **Строка запроса** используется заполнитель **{StandardTokens}**. Добавьте строку &amp;SPAddInVersion=1.0.0.0 в конец файла. Конструктор манифеста должен выглядеть примерно так, как показано ниже. *Обратите внимание, что номер версии, который вы передаете в строке запроса, должен совпадать со значением в поле **Версия** в конструкторе.* (Если вы когда-либо будете обновлять надстройку, вам потребуется увеличить эти два значения и обеспечить их совпадение.)</span><span class="sxs-lookup"><span data-stu-id="ad689-p114">The SharePoint host web needs to tell the remote web application what version of the add-in it has installed. We'll use a query parameter to do this. Open the AppManifest.xml file in the **ChainStore** project. In the designer you'll see the placeholder **{StandardTokens}** as the value of the **Query string** box. Add the string "&amp;SPAddInVersion=1.0.0.0" to the end. The manifest designer should look similar to the following.  *Notice that the version number you pass in the query string has to match the value in the **Version** box of the designer.*  (If you ever update the add-in, one of your tasks is to raise these two values and keep them the same.)</span></span>
    
  ![Вкладка "Общие" в конструкторе манифеста. Поле "Версия" содержит значение "один ноль ноль ноль". Поле "Строка запроса" содержит текст "{StandardTokens}&amp;SPAddInVersion=1.0.0.0"](../../images/db71c411-10c5-43d8-bb5e-3388d2f6f7bc.PNG)
 

 

 
2. <span data-ttu-id="ad689-p116">Откройте файл CorporateDataViewer.aspx.cs и добавьте приведенный ниже код в метод **Page_Load** сразу же после строки, в которой выполняется инициализация объекта `spContext`. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="ad689-p116">Open the CorporateDataViewer.aspx.cs file and add the following code to the **Page_Load** method, just below the line that initializes the `spContext` object. Note the following about this code:</span></span>
    
      - <span data-ttu-id="ad689-p117">Он начинается с задания двух статических полей в статическом классе  `SharePointComponentDeployer`. Он передает объект **SharePointContext**, так как код в  `SharePointComponentDeployer` будет вызываться в SharePoint, и использует параметр запроса, который вы добавили, чтобы задать свойство `localVersion`.</span><span class="sxs-lookup"><span data-stu-id="ad689-p117">It begins by setting the two static fields in the static  `SharePointComponentDeployer` class. It passes the **SharePointContext** object because the code in the `SharePointComponentDeployer` will be calling into SharePoint, and it uses the query parameter that you added to set the `localVersion` property.</span></span>
    
 
  - <span data-ttu-id="ad689-p118">Он ничего не делает, если  `IsDeployed` имеет значение true, то есть если код, выполняемый при первом запуске, уже был запущен. В противном случае он вызывает метод развертывания и передает объект запроса ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ad689-p118">It does nothing if  `IsDeployed` is true; that is, if the "first run" logic has already run. Otherwise it calls the deployment method and passes the ASP.NET Request object.</span></span>
    
 

```C#
  SharePointComponentDeployer.sPContext = spContext;
SharePointComponentDeployer.localVersion = new Version(Request.QueryString["SPAddInVersion"]);

if (!SharePointComponentDeployer.IsDeployed)
{
    SharePointComponentDeployer.DeployChainStoreComponentsToHostWeb(Request);
}
```


## <a name="programmatically-deploy-a-sharepoint-list"></a><span data-ttu-id="ad689-176">Развертывание списка SharePoint программным способом</span><span class="sxs-lookup"><span data-stu-id="ad689-176">Programmatically deploy a SharePoint list</span></span>


 

 

1. <span data-ttu-id="ad689-p119">В файле SharePointComponentDeployer.cs замените строку `TODO4` на приведенный ниже код. Этот метод создается на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="ad689-p119">In the SharePointComponentDeployer.cs file, replace the  `TODO4` with the following line. You create this method in the next step.</span></span>
    
```C#
  CreateLocalEmployeesList();
```

2. <span data-ttu-id="ad689-p120">Добавьте приведенный ниже метод в класс `SharePointComponentDeployer`. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="ad689-p120">Add the following method to the  `SharePointComponentDeployer` class. Note the following about this code:</span></span>
    
      - <span data-ttu-id="ad689-p121">Он содержит два вызова метода **ExecuteQuery**. Первый необходим, чтобы определить, существует ли список. Второй выполняет действия по созданию списка.</span><span class="sxs-lookup"><span data-stu-id="ad689-p121">It has two calls of **ExecuteQuery**. The first is needed to determine if the list already exists. The second does the work of creating the list.</span></span>
    
 
  - <span data-ttu-id="ad689-184">Метод **ClientContext.LoadQuery** похож на метод **ClientContext.Load**, но вместо объекта, например списка, он передает клиенту перечислимые результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="ad689-184">The **ClientContext.LoadQuery** method is similar to the **ClientContext.Load** except that instead of bringing an entity, such as a list, down to the client, it brings down the enumerable results of a query.</span></span>
    
 

```C#
  private static void CreateLocalEmployeesList()
{
    using (var clientContext = sPContext.CreateUserClientContextForSPHost())
    {
        var query = from list in clientContext.Web.Lists
                    where list.Title == "Local Employees"
                    select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        if (matchingLists.Count() == 0)
        {
           // TODO5: Create the list 

           // TODO6: Rename the Title field on the list 

           // TODO7: Add "Added to Corporate DB" field to the list 

           clientContext.ExecuteQuery();
        }
    }
}
```

3. <span data-ttu-id="ad689-p122">Замените строку `TODO5` на приведенный ниже код. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="ad689-p122">Replace  `TODO5` with the following code. Note the following about this code:</span></span>
    
      - <span data-ttu-id="ad689-p123">Класс **ListCreationInformation** похож на класс **ListItemCreationInformation**, который уже встречался в одной из предыдущих статей этой серии. Это упрощенный класс, более подходящий для отправки данных из веб-приложения в SharePoint, чем полноценный класс **List**.</span><span class="sxs-lookup"><span data-stu-id="ad689-p123">The **ListCreationInformation** class is similar to the **ListItemCreationInformation** class you saw in an earlier article in this series. It is a lightweight class more suitable for sending information from the web application to SharePoint than the full **List** class.</span></span>
    
 
  - <span data-ttu-id="ad689-p124">Существует много типов шаблонов списков, например тип Tasks для списка дел и тип Events для календаря. Список **Местные сотрудники** основан на самом простом типе Generic.</span><span class="sxs-lookup"><span data-stu-id="ad689-p124">There are many types of list templates, such as the Tasks type for a "to do" list and the Events type for a calendar. The **Local Employees** list is based on the simplest: the Generic type.</span></span>
    
 
  - <span data-ttu-id="ad689-p125">В свойстве **ListCreationInformation.Url** хранится URL-адрес списка *относительно* хост-сайта. Указывая адрес Lists/LocalEmployees, код задает полный URL-адрес списка: https://*{Домен_SharePoint}*/hongkong/_layouts/15/start.aspx#/Lists/Local%20Employees.</span><span class="sxs-lookup"><span data-stu-id="ad689-p125">The **ListCreationInformation.Url** property holds the URL of the list *relative*  to the host web. By specifying "Lists/LocalEmployees", the code is setting the full URL of the list to https:// *{SharePointDomain}*  /hongkong/_layouts/15/start.aspx#/Lists/Local%20Employees.</span></span>
    
 

```C#
  ListCreationInformation listInfo = new ListCreationInformation();
listInfo.Title = "Local Employees";
listInfo.TemplateType = (int)ListTemplateType.GenericList;
listInfo.Url = "Lists/Local Employees";
List localEmployeesList = clientContext.Web.Lists.Add(listInfo);
```

4. <span data-ttu-id="ad689-p126">Замените  `TODO6` указанным ниже кодом, который изменяет общедоступное имя поля (столбца) Title (Название) на Name (Имя). Это то, что вы делали на странице **List Settings** (Параметры списка), когда создавали список вручную.</span><span class="sxs-lookup"><span data-stu-id="ad689-p126">Replace  `TODO6` with the following code which changes the public name of the "Title" field (column) from "Title" to "Name". This is what you did on the **List Settings** page when you created the list manually.</span></span>
    
```C#
  Field field = localEmployeesList.Fields.GetByInternalNameOrTitle("Title");
field.Title = "Name";
field.Update();
```

5. <span data-ttu-id="ad689-p127">Кроме того, вы вручную создали поле с именем **Добавлен в корпоративную базу данных**. Чтобы сделать это программным способом, добавьте приведенный ниже код вместо строки `TODO7`. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="ad689-p127">You also manually created a field named **Added to Corporate DB**. To do that programmatically add the following code in place of  `TODO7`. Note the following about this code:</span></span>
    
      - <span data-ttu-id="ad689-p128">Ключевые свойства этого поля задаются с помощью большого двоичного объекта XML. Это связано с архитектурой SharePoint: веб-сайты, списки, поля, типы содержимого и большая часть других типов компонентов SharePoint определяются в виде XML. В данном случае мы указываем для поля отображаемое имя, тип данных и имя, используемое по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ad689-p128">The key properties of the field are specified with an XML blob. This is a legacy of SharePoint's architecture: websites, lists, fields, content types, and most other kinds of SharePoint components are defined as XML. In this case we are specifying the display name, data type, and default value of the field.</span></span>
    
 
  - <span data-ttu-id="ad689-p129">Второй параметр указывает, должно ли поле отображаться в представлении списка, используемом по умолчанию. Мы присвоим ему значение **true**.</span><span class="sxs-lookup"><span data-stu-id="ad689-p129">The second parameter determines whether the field is visible in the default view of the list. We're setting it to **true**.</span></span> 
    
 
  - <span data-ttu-id="ad689-p130">Третий параметр можно использовать для определения типов контента, к которым следует добавлять это поле. Если передать значение **DefaultValue**, поле будет добавляться в заданный по умолчанию тип контента для списка.</span><span class="sxs-lookup"><span data-stu-id="ad689-p130">The third parameter can be used to determine what content types the field is added to. Passing **DefaultValue** means that it is only added to the list's default content type.</span></span>
    
 

```C#
  localEmployeesList.Fields.AddFieldAsXml("<Field DisplayName='Added to Corporate DB'"
                                         +"Type='Boolean'>"
                                         + "<Default>FALSE</Default></Field>",
                                         true,
                                         AddFieldOptions.DefaultValue);
```

6. <span data-ttu-id="ad689-p131">Вспомним, что по умолчанию для поля **Добавлен в корпоративную базу данных** задано значение **Нет**, то есть false, но после добавления сотрудника в базу данных предприятия настраиваемая кнопка ленты в надстройке присваивает полю значение **Да**. Эта система работает безупречно, только если у пользователей нет возможности менять значение поля вручную. Чтобы у пользователей гарантированно не было такой возможности, сделайте поле невидимым в формах создания и редактирования элементов в списке **Местные сотрудники**. Для этого мы добавим два дополнительных атрибута в первый параметр, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ad689-p131">Recall that the **Added to Corporate DB** is **No** (that is, false) by default, but the custom ribbon button in the add-in sets it to **Yes** after it adds the employee to the corporate database. This system only works best if users cannot manually change the value of the field. To ensure that they don't, make the field invisible in the forms for creating and editing items on the **Local Employees** list. We do this by adding two more attributes to the first parameter, as shown in the following.</span></span>
    
```C#
  localEmployeesList.Fields.AddFieldAsXml("<Field DisplayName='Added to Corporate DB'" 
                                         + " Type='Boolean'"  
                                         + " ShowInEditForm='FALSE' "
                                         + " ShowInNewForm='FALSE'>"
                                         + "<Default>FALSE</Default></Field>",
                                         true,
                                         AddFieldOptions.DefaultValue);
```


    The entire  `CreateLocalEmployeesList` should now look like the following.
    


```C#
  private static void CreateLocalEmployeesList()
{
    using (var clientContext = sPContext.CreateUserClientContextForSPHost())
    {
        var query = from list in clientContext.Web.Lists
                    where list.Title == "Local Employees"
                    select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        if (matchingLists.Count() == 0)
        {
            ListCreationInformation listInfo = new ListCreationInformation();
            listInfo.Title = "Local Employees";
            listInfo.TemplateType = (int)ListTemplateType.GenericList;
            listInfo.Url = "LocalEmployees";
            List localEmployeesList = clientContext.Web.Lists.Add(listInfo);

            Field field = localEmployeesList.Fields.GetByInternalNameOrTitle("Title");
            field.Title = "Name";
            field.Update();

            localEmployeesList.Fields.AddFieldAsXml("<Field DisplayName='Added to Corporate DB'" 
                                                    + " Type='Boolean'"  
                                                   + " ShowInEditForm='FALSE' "
                                                   + " ShowInNewForm='FALSE'>"
                                                   + "<Default>FALSE</Default></Field>",
                                                    true,
                                                    AddFieldOptions.DefaultValue);
            clientContext.ExecuteQuery();
        }
    }
}
```


## <a name="temporarily-remove-the-custom-button-from-the-project"></a><span data-ttu-id="ad689-209">Временное удаление настраиваемой кнопки из проекта</span><span class="sxs-lookup"><span data-stu-id="ad689-209">Temporarily remove the custom button from the project</span></span>

<span data-ttu-id="ad689-p132">По техническим причинам, которые мы рассмотрим в следующей статье, созданную нами настраиваемую кнопку не удастся установить без изменений, если необходимо разместить ее на ленте списка, который развернут программным способом. Мы временно удалим ее из проекта, чтобы можно было протестировать код, выполняемый при первом запуске. Мы вернем ее в следующей статье.</span><span class="sxs-lookup"><span data-stu-id="ad689-p132">For technical reasons that we'll discuss in the next article, the custom button we created cannot be installed without modification when it is being put on the ribbon of a list that is programmatically deployed. We'll remove it temporarily from the project, so that we can test our first-run logic. We'll bring it back in the next article.</span></span>
 

 
<span data-ttu-id="ad689-213">В **обозревателе решений** в проекте **ChainStore** щелкните правой кнопкой мыши узел **AddEmployeeToCorpDB** и выберите пункт **Исключить из проекта**.</span><span class="sxs-lookup"><span data-stu-id="ad689-213">In **Solution Explorer**, in the **ChainStore** project, right-click the **AddEmployeeToCorpDB** node and select **Exclude from Project**.</span></span>
 

 

## <a name="request-permission-to-manage-lists-on-the-host-web"></a><span data-ttu-id="ad689-214">Запрос разрешения на управление списками на хост-сайте</span><span class="sxs-lookup"><span data-stu-id="ad689-214">Request permission to manage lists on the host web</span></span>

<span data-ttu-id="ad689-p133">Так как теперь надстройка добавляет список на хост-сайт, а не только элементы в существующий список, нам необходимо расширить разрешения для надстройки с "Запись" до "Управление". Выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="ad689-p133">Since the add-in is now adding a list to the host web, not just items to an existing list, we need to escalate the permissions that the add-in requests from Write to Manage. Follow these steps.</span></span>
 

 

1. <span data-ttu-id="ad689-217">В **обозревателе решений** откройте файл AppManifest.xml проекта **ChainStore**.</span><span class="sxs-lookup"><span data-stu-id="ad689-217">In **Solution Explorer**, open the AppManifest.xml file in the **ChainStore** project.</span></span>
    
 
2. <span data-ttu-id="ad689-218">Откройте вкладку **Разрешения**. Для поля **Область** оставьте значение "Интернет", а в поле **Разрешение** выберите в раскрывающемся списке пункт **Управление**.</span><span class="sxs-lookup"><span data-stu-id="ad689-218">Open the **Permissions** tab and leave the **Scope** value at Web, but in the **Permission** field, select **Manage** from the drop down.</span></span>
    
 
3. <span data-ttu-id="ad689-219">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="ad689-219">Save the file.</span></span>
    
 

## <a name="run-the-add-in-and-test-the-first-run-logic"></a><span data-ttu-id="ad689-220">Запуск надстройки и тестирование кода для первого запуска</span><span class="sxs-lookup"><span data-stu-id="ad689-220">Run the add-in and test the "first run" logic</span></span>


 

 

1. <span data-ttu-id="ad689-221">Откройте страницу **Содержимое сайта** для веб-сайта магазина в Гонконге *и удалите список **Местные сотрудники**.*</span><span class="sxs-lookup"><span data-stu-id="ad689-221">Open the **Site Contents** page of the Hong Kong store's website *and remove the **Local Employees** list!*</span></span> 
    
 
2. <span data-ttu-id="ad689-p134">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и сразу же запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить необходимые для надстройки разрешения.</span><span class="sxs-lookup"><span data-stu-id="ad689-p134">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before its start page opens.</span></span>
    
 
3. <span data-ttu-id="ad689-226">Когда откроется начальная страница надстройки, нажмите кнопку **Вернуться на сайт** на размещенном в верхней части элементе управления хрома.</span><span class="sxs-lookup"><span data-stu-id="ad689-226">When the add-in's start page opens, select the **Back to Site** link on the chrome control at the top.</span></span>
    
 
4. <span data-ttu-id="ad689-p135">Перейдите на страницу **Содержимое сайта**. Список **Местные сотрудники** отображается, потому что его добавил код, выполняемый при первом запуске.</span><span class="sxs-lookup"><span data-stu-id="ad689-p135">Navigate to the **Site Contents** page. The **Local Employees** list is present because your first-run logic added it.</span></span>
    
     <span data-ttu-id="ad689-p136">**Примечание.** Если список не отображается или имеются другие признаки того, что код для первого запуска не выполняется, это может быть вызвано тем, что таблица **Tenants** (Клиенты) не очищается при нажатии клавиши F5. Как правило, это связано с тем, что проект **ChainCorporateDB** больше не задан в качестве запускаемого проекта в Visual Studio. В начале этой статьи есть примечание о том, как это исправить. Кроме того, убедитесь, что база данных настроена на повторное создание, как описано в разделе [Настройка Visual Studio на повторное создание корпоративной базы данных в каждом сеансе отладки](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel#Rebuild).</span><span class="sxs-lookup"><span data-stu-id="ad689-p136">**Note** If the list is not there or you have other indications that the first-run code is not executing, it may be that the **Tenants** table is not being reverted to an empty state when you press F5. The most common cause of this is that the **ChainCorporateDB** project is no longer set as a startup project in Visual Studio. See the note near the top of this article for how to fix this. Also be sure that you've configured the database to be rebuilt as described in [Configure Visual Studio to rebuild the corporate database with each debugging session](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel#Rebuild).</span></span>
5. <span data-ttu-id="ad689-p137">Откройте список и добавьте в него элемент. Обратите внимание, что на новой форме элемента больше нет поля **Добавлен в корпоративную базу данных**, поэтому его значение невозможно задать вручную. Это справедливо и для формы редактирования элемента.</span><span class="sxs-lookup"><span data-stu-id="ad689-p137">Open the list and add an item. Note that on the new item form, the **Added to Corporate DB** field is no longer present, so it cannot be manually set. This is true of the edit item form as well.</span></span>
    
  ![Форма создания элемента списка "Локальные сотрудники". Поле "Добавлен в корпоративную базу данных" теперь отсутствует. Остались только поле имени и кнопки "ОК" и "Отмена".](../../images/3fdc6752-4184-4928-9423-0bc7c0206c62.PNG)
 

 

 
6. <span data-ttu-id="ad689-239">Вернитесь на начальную страницу надстройки с помощью кнопки "Назад" в браузере.</span><span class="sxs-lookup"><span data-stu-id="ad689-239">Use the browser's back button to navigate back to the add-in's start page.</span></span>
    
 
7. <span data-ttu-id="ad689-240">Нажмите значок шестеренки в элементе управления хрома сверху, а затем выберите пункт **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="ad689-240">Press the gear icon on the chrome control at the top, and select **Account settings**.</span></span>
    
 
8. <span data-ttu-id="ad689-p139">На странице **Учетные записи** нажмите кнопку **Показать версию надстройки**. Появится номер версии **1.0.0.0**, так как код, выполняемый при первом запуске, изменил ее.</span><span class="sxs-lookup"><span data-stu-id="ad689-p139">On the **Accounts** page, press the **Show Add-in Version** button. The version shows as **1.0.0.0** because the first-run logic changed it.</span></span>
    
  ![Страница параметров учетной записи с номером версии 1.0.0.0.](../../images/4c6d82a7-7c40-4190-b7e3-1337275e1e60.PNG)
 

 

 
9. <span data-ttu-id="ad689-p140">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="ad689-p140">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
10. <span data-ttu-id="ad689-p141">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="ad689-p141">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="ad689-248"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="ad689-248"></span></span>

 <span data-ttu-id="ad689-249">В следующей статье вы узнаете, как вернуть в надстройку настраиваемую кнопку для ленты **Local Employee** (Местный сотрудник), когда развертывание списка выполняется программным путем: [Программное развертывание настраиваемой кнопки в надстройке, размещаемой у поставщика](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in)</span><span class="sxs-lookup"><span data-stu-id="ad689-249">In the next article, you'll see how to get the custom button for the **Local Employee** ribbon back into the add-in now the list is being deployed programmatically: [Programmatically deploy a custom button in the provider-hosted add-in](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in)</span></span>
 

 

