---
title: "Сегментация пользователей в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 60809bfb16706709b448ba2d0fb3849cf5a33277
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="user-segmentation-in-sharepoint"></a><span data-ttu-id="c180f-102">Сегментация пользователей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-102">User segmentation in SharePoint</span></span>
<span data-ttu-id="c180f-103">Отображаемое содержимое варьировать для пользователя сегментов можно определять —, например зависимости от языкового стандарта, интересами, пол или ссылок ссылки — задает набор терминов, веб-части поиска контента, используя правила запроса в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c180f-103">Display content you tailor for user segments you define—for example, based on locale, interests, gender, or referral links—by using a combination of term sets, the Content Search Web Part, and query rules in SharePoint.</span></span>
<span data-ttu-id="c180f-104">SharePoint предоставляет стандартные блоки для настройки содержимого, которое Показать на сайте SharePoint, в зависимости от определенных атрибуты конечных пользователей, например их Пол место жительства, их интересами или ссылки ссылок.</span><span class="sxs-lookup"><span data-stu-id="c180f-104">SharePoint provides the building blocks to tailor content you show on a SharePoint site, depending on certain attributes of end-users, for example their gender, where they live, their interests, or referral links.</span></span> <span data-ttu-id="c180f-105">Эти группы атрибутов пользователя известны как сегменты пользователей.</span><span class="sxs-lookup"><span data-stu-id="c180f-105">These groupings of user attributes are known as user segments.</span></span> 
  
    
    

<span data-ttu-id="c180f-106">В SharePoint этой функциональности сегментирования пользователей может быть удобно использовать в различных сценариях, например:</span><span class="sxs-lookup"><span data-stu-id="c180f-106">In SharePoint, this user segmentation functionality can be beneficial in many scenarios, such as:</span></span>
- <span data-ttu-id="c180f-107">Отображение различных ленты на странице в зависимости от того, Пол конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="c180f-107">Displaying different banners on a page depending on the end-user's gender</span></span> 
    
  
- <span data-ttu-id="c180f-108">Отображение различных скидку предлагает в зависимости от языкового стандарта конечного пользователя</span><span class="sxs-lookup"><span data-stu-id="c180f-108">Displaying different discount offers depending on the end-user's locale</span></span> 
    
  
- <span data-ttu-id="c180f-109">Отображение различных статьи на страницы в зависимости от того, с которого производилось обращение ссылку конечного пользователя (приведенная конечного пользователя на страницу веб-сайта).</span><span class="sxs-lookup"><span data-stu-id="c180f-109">Displaying different articles on a page depending on the end-user's referrer link (the web site that brought the end-user to your page).</span></span> 
    
  
<span data-ttu-id="c180f-110">Для реализации сегментации пользователей в SharePoint, будет выполнить следующие действия: Создание набора терминов для каждого сегмента пользователей, расширения контента веб-части поиска следует принять во внимание на сегменты пользователей и затем использовать правила запросов для выполнения определенных действий для каждого сегмента пользователей.</span><span class="sxs-lookup"><span data-stu-id="c180f-110">To implement user segmentation in SharePoint, you'll do three things: create a term set for each user segment, extend the Content Search Web Part to make it aware of your user segments, and then use query rules to perform specific actions for each user segment.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="c180f-111">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="c180f-111">Prerequisites</span></span>
<span data-ttu-id="c180f-112"><a name="SP15_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-112"></span></span>

<span data-ttu-id="c180f-113">Перед началом работы, реализации сегментации пользователей в SharePoint, необходимо установить следующие компоненты в среде разработки:</span><span class="sxs-lookup"><span data-stu-id="c180f-113">Before you get started implementing user segmentation in SharePoint, be sure to have the following installed in your development environment:</span></span>
  
    
    

- <span data-ttu-id="c180f-114">SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-114">SharePoint</span></span>
    
  
- <span data-ttu-id="c180f-115">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c180f-115">Visual Studio 2012</span></span>
    
  
<span data-ttu-id="c180f-p102">В этой статье предполагается, что работы по разработке веб-частей в SharePoint. Дополнительные сведения о разработке веб-частей на ссылки  [стандартный блок: веб-части](http://msdn.microsoft.com/en-us/library/ee535520%28v=office.14%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="c180f-p102">This article assumes that you have experience with developing Web Parts in SharePoint. For more information on developing Web Parts, refer to  [Building Block: Web Parts](http://msdn.microsoft.com/en-us/library/ee535520%28v=office.14%29.aspx)</span></span>
  
    
    

## <a name="overview-on-adding-user-segmentation-functionality-to-your-sharepoint-site"></a><span data-ttu-id="c180f-118">Общие сведения о добавлении функциональности сегментирования пользователей на сайт SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-118">Overview on adding user segmentation functionality to your SharePoint site</span></span>
<span data-ttu-id="c180f-119"><a name="SP15_Overview_User_Segmentation"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-119"></span></span>

<span data-ttu-id="c180f-120">На рисунке 1 показаны основные действия для добавления функции сегментации пользователей на сайт SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c180f-120">Figure 1 shows the basic steps to add user segmentation functionality to your SharePoint site.</span></span>
  
    
    

<span data-ttu-id="c180f-121">**На рисунке 1. Действия по добавлению функциональности сегментирования пользователей на сайт SharePoint**</span><span class="sxs-lookup"><span data-stu-id="c180f-121">**Figure 1. Steps to add user segmentation functionality to your SharePoint site**</span></span>

  
    
    

  
    
    
![Действия по добавлению функциональности сегментирования пользователей](../images/SP15_User_Segmentation_with_ContentBySearchWebPart.jpg)
  
    
    

  
    
    

  
    
    

## <a name="create-a-term-set"></a><span data-ttu-id="c180f-123">Создайте набор терминов</span><span class="sxs-lookup"><span data-stu-id="c180f-123">Create a term set</span></span>
<span data-ttu-id="c180f-124"><a name="SP15_Create_a_term_set"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-124"></span></span>

<span data-ttu-id="c180f-125">Условие — это слово или фразу, которые могут быть связаны с элементом в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c180f-125">A term is a word or a phrase that can be associated with an item in SharePoint.</span></span> <span data-ttu-id="c180f-126">Набор Aterm — набор терминов, связанных с ними.</span><span class="sxs-lookup"><span data-stu-id="c180f-126">Aterm set is a collection of related terms.</span></span> <span data-ttu-id="c180f-127">Для получения дополнительных сведений см [управляемых метаданных в SharePoint](http://technet.microsoft.com/en-us/library/ee424402.aspx).</span><span class="sxs-lookup"><span data-stu-id="c180f-127">For more information, see [Overview of managed metadata in SharePoint](http://technet.microsoft.com/en-us/library/ee424402.aspx).</span></span> <span data-ttu-id="c180f-128">Создание наборов терминов через средство управления банками терминов SharePoint, или программными средствами.</span><span class="sxs-lookup"><span data-stu-id="c180f-128">You can create term sets either through the SharePoint Term Store Management Tool, or programmatically.</span></span> 
  
    
    

> <span data-ttu-id="c180f-129">**Примечание:** В следующих разделах представлены подробные инструкции о том, как использовать средство управления банками терминов для создания набора терминов: > [Настройка новый набор терминов](http://office.microsoft.com/en-us/sharepoint-help/set-up-a-new-term-set-HA102922634.aspx)>  [Создание терминов в наборе терминов и управление ими](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/create-and-manage-terms-in-a-term-set-HA102771989.aspx)</span><span class="sxs-lookup"><span data-stu-id="c180f-129">**Note:** See the following topics for detailed instructions on how to use the Term Store Management Tool to create your term set:>  [Set up a new term set](http://office.microsoft.com/en-us/sharepoint-help/set-up-a-new-term-set-HA102922634.aspx)>  [Create and manage terms in a term set](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/create-and-manage-terms-in-a-term-set-HA102771989.aspx)</span></span>
  
    
    

<span data-ttu-id="c180f-p104">Вы можете создать набор программным путем с помощью типов, представленные в  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) терминов. В следующем примере кода показано, как создать объект **TermSet** и получать **NavigationTermSet**. Создайте объекты **Term** в рамках вашей **TermSet**. И, наконец внести эти изменения **TermStore** и загружать **TermSet** для навигации.</span><span class="sxs-lookup"><span data-stu-id="c180f-p104">You can create a term set programmatically by using the types exposed via  [Microsoft.SharePoint.Taxonomy](https://msdn.microsoft.com/library/Microsoft.SharePoint.Taxonomy.aspx) . The following code example shows how to create a **TermSet** object and obtain the **NavigationTermSet**. Next, you create **Term** objects within your **TermSet**. Finally, commit these changes to the **TermStore** and load the **TermSet** to use for navigation.</span></span>
  
    
    
<span data-ttu-id="c180f-p105">Каждый термин, добавляемого к терминов set Получает уникальный идентификатор. Этот идентификатор является ключом к созданию  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) принять во внимание на сегменты пользователей.</span><span class="sxs-lookup"><span data-stu-id="c180f-p105">Each term you add to your term set receives a unique identifier. This identifier is the key to making the  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.aspx) aware of your user segments.</span></span>
  
    
    



```cs

static void CreateNavigationTermSet(string siteUrl)
{
    using (SPSite site = new SPSite(siteUrl))
    {
        using (SPWeb web = site.OpenWeb())
        {
            TaxonomySession taxonomySession = new TaxonomySession(site);
            taxonomySession.UpdateCache();
            TermStore termStore = taxonomySession.DefaultSiteCollectionTermStore;

            // Create a TermSet object in a default site collection term group.
            Group siteCollectionGroup = termStore.GetSiteCollectionGroup(site, createIfMissing: true);
            TermSet termSet = siteCollectionGroup.CreateTermSet("Navigation Demo", Guid.NewGuid(), lcid: 1033);

            // Obtain navigation term set.
            NavigationTermSet navigationTermSet = NavigationTermSet.GetAsResolvedByWeb(termSet, web, "GlobalNavigationTaxonomyProvider");

            // Create a term that points to a SharePoint page set at the term set level of hierarchy.
            NavigationTerm term1 = navigationTermSet.CreateTerm("Term 1", NavigationLinkType.FriendlyUrl, Guid.NewGuid());

            // Create a term that points to an already existing URL outside of SharePoint.
            NavigationTerm term2 = navigationTermSet.CreateTerm("Term 2", NavigationLinkType.SimpleLink, Guid.NewGuid());
            term2.SimpleLinkUrl = "http://www.bing.com/";

            // Create a term that points to an existing SharePoint page.
            NavigationTerm term3 = navigationTermSet.CreateTerm("Term 3", NavigationLinkType.FriendlyUrl, Guid.NewGuid());

            // Save all changes to the term store.
            termStore.CommitAll();
        }
    }
}
```


## <a name="create-a-custom-web-part-for-user-segmentation"></a><span data-ttu-id="c180f-136">Создание настраиваемых веб-части для сегментации пользователей</span><span class="sxs-lookup"><span data-stu-id="c180f-136">Create a custom Web Part for user segmentation</span></span>
<span data-ttu-id="c180f-137"><a name="SP15_Create_a_custom_web_part_user_segmentation"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-137"></span></span>

<span data-ttu-id="c180f-138">В Visual Studio 2012 Создание настраиваемых веб-части с помощью шаблона визуальных веб-частей из категории SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c180f-138">In Visual Studio 2012, create a custom Web Part by using the Visual Web Parts template from the SharePoint category.</span></span> <span data-ttu-id="c180f-139">Настраиваемые веб-части должен наследовать из объекта [ContentBySearchWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.office.server.search.webcontrols.contentbysearchwebpart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c180f-139">Your custom Web Part must inherit from the  [ContentBySearchWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.office.server.search.webcontrols.contentbysearchwebpart.aspx) object.</span></span>
  
    
    

> <span data-ttu-id="c180f-140">**Примечание:** В этой статье предполагается, что работы по разработке веб-частей в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c180f-140">**Note:** This article assumes that you have experience with developing Web Parts in SharePoint.</span></span> <span data-ttu-id="c180f-141">Дополнительные сведения о разработке веб-частей, можно найти [стандартный блок: веб-части](http://msdn.microsoft.com/en-us/library/ee535520%28v=office.14%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="c180f-141">For more information on developing Web Parts, refer to  [Building Block: Web Parts](http://msdn.microsoft.com/en-us/library/ee535520%28v=office.14%29.aspx)</span></span>
  
    
    


## <a name="configure-a-custom-web-part-with-user-segmentation-logic"></a><span data-ttu-id="c180f-142">Настройка настраиваемого веб-части с логикой сегментации пользователей</span><span class="sxs-lookup"><span data-stu-id="c180f-142">Configure a custom Web Part with user segmentation logic</span></span>
<span data-ttu-id="c180f-143"><a name="SP15_Configure_custom_web_part_user_segmentation_logic"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-143"></span></span>

<span data-ttu-id="c180f-p108">В настраиваемых веб-части можно повторно реализовать  [OnLoad()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnLoad.aspx) метод или метод [OnInit()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnInit.aspx) для выполнения настраиваемой логики. Обе эти методы полезны настроить свойства объекта [ContentBySearchWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.office.server.search.webcontrols.contentbysearchwebpart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c180f-p108">In your custom Web Part, you can re-implement either the  [OnLoad()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnLoad.aspx) method or the [OnInit()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnInit.aspx) method to carry out your custom logic. Both these methods are useful to set or customize properties of the [ContentBySearchWebPart](https://msdn.microsoft.com/en-us/library/office/microsoft.office.server.search.webcontrols.contentbysearchwebpart.aspx) object.</span></span>
  
    
    

### <a name="example-1-add-male-and-female-user-segments-to-your-sharepoint-site"></a><span data-ttu-id="c180f-146">В примере 1: Добавление м и женщина сегменты пользователей на сайт SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-146">Example 1: Add Male and Female user segments to your SharePoint site</span></span>

<span data-ttu-id="c180f-147">Чтобы добавить **Male** и **Female** сегменты пользователей, можно повторно реализуйте метод [OnLoad()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnLoad.aspx) , как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c180f-147">To add **Male** and **Female** user segments, you can re-implement the [OnLoad()](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebControls.ContentBySearchWebPart.OnLoad.aspx) method as shown in the following code.</span></span>
  
    
    

```cs

protected override void OnLoad(EventArgs e)
{
    if (this.AppManager != null)
    {
        if (this.AppManager.QueryGroups.ContainsKey(this.QueryGroupName) &amp;&amp; this.AppManager.QueryGroups[this.QueryGroupName].DataProvider != null)
        {
            this.AppManager.QueryGroups[this.QueryGroupName].DataProvider.BeforeSerializeToClient += new
                BeforeSerializeToClientEventHandler(AddMycustomProperties);
        }
    }
    base.OnLoad(e);
}
```

<span data-ttu-id="c180f-148">Соответствующий метод **AddMycustomProperties** будут выглядеть следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="c180f-148">The corresponding **AddMycustomProperties** method would look like the following code.</span></span>
  
    
    



```cs

private void AddMycustomProperties(object sender, BeforeSerializeToClientEventArgs e)
{
    DataProviderScriptWebPart dp = sender as DataProviderScriptWebPart;
    string gender = (string)Page.Session["DataProvider.Gender"];
    // Depends on what your DataProvider is: Facebook, LinkedIn, etc.

    if (dp != null &amp;&amp; gender != null)
    {   try
        {
            // Set property to male or female GUID.
            if (gender.CompareTo("female") == 0)
            {
                dp.Properties["TermSetName"] = new String[] { "TermUniqueIdentifier" };
                // E.g. 47ba9139-a4c5-4ff0-8f9a-2864be32da92
            }
            else if(gender.CompareTo("male") == 0)
            {
                dp.Properties["UserSegmentTerms"] = new String[] { "TermUniqueIdentifier" };
                // E.g. f5bf2195-2170-4b11-a018-a688a285e579
            }
        }
        catch (ArgumentException exp)
        {
             // Do something with the exception.
        }
   }
}
```


### <a name="example-2-create-user-segments-based-on-the-type-of-web-browser-your-end-user-is-using-when"></a><span data-ttu-id="c180f-149">Пример 2: Создание сегменты пользователей на основе типа конечного пользователя используется веб-браузера</span><span class="sxs-lookup"><span data-stu-id="c180f-149">Example 2: Create user segments based on the type of Web browser your end-user is using when</span></span>

<span data-ttu-id="c180f-150">Для создания сегменты пользователей, в зависимости от типа используемой конечный пользователь, чтобы просмотреть свой сайт SharePoint, веб-браузер повторно реализуйте метод **OnLoad** , как показано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="c180f-150">To create user segments based on the type of web browser the end-user is using, to view your SharePoint site, re-implement the **OnLoad** method as shown in the following code.</span></span>
  
    
    

```cs

protected override void OnLoad(EventArgs e)
{
    if (this.AppManager != null)
    {
        if (this.AppManager.QueryGroups.ContainsKey(this.QueryGroupName) &amp;&amp; this.AppManager.QueryGroups[this.QueryGroupName].DataProvider != null)
        {
             this.AppManager.QueryGroups[this.QueryGroupName].DataProvider.BeforeSerializeToClient += new 
                 BeforeSerializeToClientEventHandler(AddMycustomProperties);
        }
    }
    base.OnLoad(e);
}
```

<span data-ttu-id="c180f-151">Код для метода **AddMycustomProperties** будет выглядеть как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="c180f-151">The code for the **AddMycustomProperties** method would look like the following example.</span></span>
  
    
    



```cs

private void AddMycustomProperties(object sender, BeforeSerializeToClientEventArgs e)
{
    DataProviderScriptWebPart dataProvider = sender as DataProviderScriptWebPart;
    SPSite site = SPContext.Current.Site;
  
    TaxonomySession session = new TaxonomySession(site);
    TermStore defaultSiteCollectionStore = session.DefaultSiteCollectionTermStore;
    List<string> userSegmentTerms = new List<string>();

    var userAgentparts = Page.Request.UserAgent.Split(new char[] { ';', '(', ')' });

    foreach (var part in userAgentparts)
    {
        var entry = part.Trim();
        var terms = termStore.GetTermsWithCustomProperty("UserAgent", entry, false);

            if (terms.Count > 0)
            {
                userSegmentTerms.Add(terms[0].Id.ToString());
            }
    }
    dataProvider.Properties["UserSegmentTerms"] = userSegmentTerms.ToArray();
}
```


## <a name="upload-the-custom-web-part-to-the-sharepoint-web-part-gallery"></a><span data-ttu-id="c180f-152">Загрузите пользовательской веб-части в галерею веб-частей SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-152">Upload the custom Web Part to the SharePoint Web Part Gallery</span></span>
<span data-ttu-id="c180f-153"><a name="SP15_Upload_custom_web_part"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-153"></span></span>

<span data-ttu-id="c180f-154">Чтобы использовать настраиваемые веб-части на странице, необходимо отправка в веб-части в **SharePoint Web Part Gallery**.</span><span class="sxs-lookup"><span data-stu-id="c180f-154">In order to use your custom Web Part in your page, you need to upload the Web Part to the **SharePoint Web Part Gallery**.</span></span>
  
    
    
<span data-ttu-id="c180f-p109">В **SharePoint Web Part Gallery**выберите **Параметры сайта** и выберите **веб-частей** в разделе **Коллекции веб-дизайнера**. На вкладке **файлы** нажмите кнопку **Отправить документ**.</span><span class="sxs-lookup"><span data-stu-id="c180f-p109">In the **SharePoint Web Part Gallery**, choose **Site Settings**, and then choose **Web parts** under **Web Designer Galleries**. On the **Files** tab, choose **Upload Document**.</span></span>
  
    
    

## <a name="add-query-rules-to-carry-out-specific-actions-that-depend-on-the-user-segment"></a><span data-ttu-id="c180f-157">Добавление правила запросов для выполнения определенных действий, которые зависят от пользовательский сегмент</span><span class="sxs-lookup"><span data-stu-id="c180f-157">Add query rules to carry out specific actions that depend on the user segment</span></span>
<span data-ttu-id="c180f-158"><a name="SP15_Add_query_rules_to_carry_out_actions"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-158"></span></span>

<span data-ttu-id="c180f-p110">Правило запроса преобразований запросов для повышения релевантности результатов поиска путем рационально реагирует на то, что пользователь пытается найти. В правило запроса укажите условия и соответствующих действий. При запросе будут выполнены условия правила запроса, поисковая система выполняет действия, указанные в правиле для повышения релевантности результатов поиска, такие как их результаты или изменение порядка, в котором отображаются результаты.</span><span class="sxs-lookup"><span data-stu-id="c180f-p110">A query rule transforms queries to improve the relevance of search results by reacting intelligently to what the user might be trying to find. In a query rule, you specify conditions and correlated actions. When a query meets the conditions in a query rule, the search system performs the actions specified in the rule to improve the relevance of the search results, such as narrowing down the results or changing the order in which results are displayed.</span></span>
  
    
    
<span data-ttu-id="c180f-p111">При реализации сегментации пользователей, используемого правила запросов для определения условия и действия для сегменты определенных пользователей. Когда конечный пользователь является частью определенного пользовательский сегмент, будет активировать правило запроса и  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebConrols.ContentBySearchWebPart.aspx) будет отображать контент, который предназначен для определенного пользователя сегмента.</span><span class="sxs-lookup"><span data-stu-id="c180f-p111">When implementing user segmentation, you use query rules to define conditions and actions for the defined user segments. When an end-user is part of a particular user segment, the query rule will activate and the  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebConrols.ContentBySearchWebPart.aspx) will display content that is tailored for that particular user segment.</span></span>
  
    
    

### <a name="to-create-a-query-rule-that-will-activate-for-a-particular-user-segment"></a><span data-ttu-id="c180f-164">Создание правила запроса, который будет активирован для конкретного пользователя сегмента</span><span class="sxs-lookup"><span data-stu-id="c180f-164">To create a query rule that will activate for a particular user segment</span></span>


1. <span data-ttu-id="c180f-165">Публикации семейства веб-сайтов в **Настройках сайта** выберите **Администрирование семейства веб-сайтов** и нажмите кнопку **Правила запросов поиска**.</span><span class="sxs-lookup"><span data-stu-id="c180f-165">In your publishing site collection in **Site Settings**, choose **Site Collection Administration**, and then choose **Search Query Rules**.</span></span> 
    
  
2. <span data-ttu-id="c180f-166">Выберите источник результатов, а затем выберите **Создать правило запроса**.</span><span class="sxs-lookup"><span data-stu-id="c180f-166">Choose a result source, and then choose **New Query Rule**.</span></span>
    
  
3. <span data-ttu-id="c180f-p112">В поле **Имя правила** введите имя правила. Щелкните и разверните **контекста**.</span><span class="sxs-lookup"><span data-stu-id="c180f-p112">Type a rule name in the **Rule Name** field. Then, click to expand **Context**.</span></span>
    
  
4. <span data-ttu-id="c180f-169">В разделе **запрос выполняется с эти сегменты пользователей** выберите **один из этих сегменты пользователей** и нажмите кнопку **Добавить сегмент пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c180f-169">Under the **Query is performed by these user segments** section, choose **One of these user segments**, and then click **Add User Segment**.</span></span>
    
  
5. <span data-ttu-id="c180f-p113">В поле **Название** введите имя для этого правила запроса сегмент пользователей. Нажмите кнопку **Добавить пользователя сегмент терминов**.</span><span class="sxs-lookup"><span data-stu-id="c180f-p113">In the **Title** field, type a name for this user segment query rule. Choose **Add user segment term**.</span></span>
    
  
6. <span data-ttu-id="c180f-p114">В диалоговом окне **Импорт из терминов хранилище** разверните узел **Службы управляемых метаданных**. В разделе **Семейства веб-сайтов** найдите набор терминов, в котором размещается условия сегментации пользователей, которые вы задали ранее в [Создайте набор терминов](#SP15_Create_a_term_set). Выберите пользовательский сегмент, для которого вы хотите применить это правило запроса. Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c180f-p114">In the **Import from term store** dialog box, expand the **Managed Metadata Service**. Under **Site Collection**, locate the term set that holds the user segmentation terms that you previously defined in  [Create a term set](#SP15_Create_a_term_set). Select the user segment for which you want to apply this query rule. Then, click **Save**.</span></span>
    
  
7. <span data-ttu-id="c180f-176">Имя вашего n сегмент пользователей диалоговое окно **Добавление пользовательского сегмента**.</span><span class="sxs-lookup"><span data-stu-id="c180f-176">Name your user segment n the **Add User Segment** dialog box.</span></span>
    
    <span data-ttu-id="c180f-177">Теперь, которым сопоставлены правило запроса пользовательским сегментом, который в свою очередь сопоставлен термину сегмент пользователей.</span><span class="sxs-lookup"><span data-stu-id="c180f-177">You have now mapped a query rule to a user segment, which in turn is mapped to a user segment term.</span></span>
    
  
8. <span data-ttu-id="c180f-178">В разделе **Условия запроса** выберите команду **Удалить условие**.</span><span class="sxs-lookup"><span data-stu-id="c180f-178">Under **Query Conditions**, choose **Remove Condition**.</span></span> 
    
    <span data-ttu-id="c180f-179">Указывает, что запрос, настроенные в  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebConrols.ContentBySearchWebPart.aspx) будет действовать как условие запроса.</span><span class="sxs-lookup"><span data-stu-id="c180f-179">This specifies that the query configured in the  [ContentBySearchWebPart](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.WebConrols.ContentBySearchWebPart.aspx) will act as the query condition.</span></span>
    
  
9. <span data-ttu-id="c180f-p115">Задайте соответствующие действия, которые будут выполнять правила запроса. В разделе **действия** выберите соответствующее действие, которое требуется получить права из-за - правила запроса. Можно выбрать для **Добавления результатов повышенного уровня** или **Добавить блок результатов**.</span><span class="sxs-lookup"><span data-stu-id="c180f-p115">Set the corresponding actions that your query rule will perform. Under the **Actions** section, select a corresponding action that you want to take as a result of -your query rule. You can select to either **Add Promoted Result** or **Add a Result Block**.</span></span>
    
  
10. <span data-ttu-id="c180f-183">Сохраните правило запроса.</span><span class="sxs-lookup"><span data-stu-id="c180f-183">Save your query rule.</span></span>
    
  
11. <span data-ttu-id="c180f-184">Повторите шаги с 1 по 10 для других сегментов пользователя, в зависимости от действий, которые требуется выполнить.</span><span class="sxs-lookup"><span data-stu-id="c180f-184">Repeat steps 1 through 10 for your other user segments, depending on the actions you want to perform.</span></span>
    
  

## <a name="add-a-custom-web-part-to-the-sharepoint-page-and-configure-it-to-show-the-query-rule"></a><span data-ttu-id="c180f-185">Добавление пользовательской веб-части на страницу SharePoint и настроить его для отображения правила запроса</span><span class="sxs-lookup"><span data-stu-id="c180f-185">Add a custom Web Part to the SharePoint page and configure it to show the query rule</span></span>
<span data-ttu-id="c180f-186"><a name="SP15_Add_custom_web_part_to_SharePoint"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-186"></span></span>

<span data-ttu-id="c180f-187">Необходимо добавить настраиваемые веб-части на страницу SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c180f-187">You need to add your custom Web Part to your SharePoint page.</span></span>
  
    
    

### <a name="to-add-your-custom-web-part"></a><span data-ttu-id="c180f-188">Добавление пользовательской веб-части</span><span class="sxs-lookup"><span data-stu-id="c180f-188">To add your custom Web Part</span></span>


1. <span data-ttu-id="c180f-189">Перейдите на страницу категорий, выберите команду **Изменить страницу** и выберите команду **Изменить шаблон страницы**.</span><span class="sxs-lookup"><span data-stu-id="c180f-189">Navigate to a category page, choose **Edit page**, and then choose **Edit page template**.</span></span>
    
  
2. <span data-ttu-id="c180f-p116">Выберите **Добавить веб-части** в верхней части страницы. Выберите настраиваемые веб-части в раскрывающемся меню в правом верхнем углу веб-части.</span><span class="sxs-lookup"><span data-stu-id="c180f-p116">Select **Add a Web Part** in the top section of the page. Then, select your custom Web Part from the drop-down menu in the upper right corner of the Web Part.</span></span>
    
  
3. <span data-ttu-id="c180f-192">Нажмите кнопку **Изменить веб-части**.</span><span class="sxs-lookup"><span data-stu-id="c180f-192">Click **Edit Web Part**.</span></span>
    
  
4. <span data-ttu-id="c180f-193">Разверните раздел **Параметры** и выберите **SpecialTermResults** в поле **В таблице результатов**.</span><span class="sxs-lookup"><span data-stu-id="c180f-193">Expand the **Settings** section, and in the **Result Table** field, choose **SpecialTermResults**.</span></span> 
    
  
5. <span data-ttu-id="c180f-194">Сохраните настройки.</span><span class="sxs-lookup"><span data-stu-id="c180f-194">Save your configuration.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="c180f-195">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c180f-195">Additional resources</span></span>
<span data-ttu-id="c180f-196"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c180f-196"></span></span>


-  [<span data-ttu-id="c180f-197">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-197">Build sites for SharePoint</span></span>](https://officedevcentersite-release.azurewebsites.net/sharepoint/docs/general-development/build-sites-for-sharepoint)
    
  
-  [<span data-ttu-id="c180f-198">Настройка сегментации пользователей на диске адаптивный каждый раз в каталог продуктов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c180f-198">Set up User Segmentation to drive adaptive experiences in a Product Catalog in SharePoint</span></span>](http://blogs.msdn.com/b/adaptive_experiences_in_sharepoint_2013/archive/2012/11/14/set-up-user-segmentation-to-drive-adaptive-experiences-in-a-product-catalog-in-sharepoint.aspx)
    
  

  
    
    

