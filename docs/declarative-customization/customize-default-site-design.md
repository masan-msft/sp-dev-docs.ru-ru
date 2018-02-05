 ---
<span data-ttu-id="2d5e4-101">название: Настройка стандартных макетов сайтов в SharePoint описание: Настраивайте стандартные макеты сайтов в шаблоне сайта группы или сайта для общения SharePoint ms.date: 18.12.2017</span><span class="sxs-lookup"><span data-stu-id="2d5e4-101">title: Customize default site designs on SharePoint description: Customize the default site designs in either the SharePoint team site or communications site template ms.date: 12/18/2017</span></span>
---

# <a name="customize-a-default-site-design"></a><span data-ttu-id="2d5e4-102">Настройка стандартного макета сайта</span><span class="sxs-lookup"><span data-stu-id="2d5e4-102">Customize a default site design</span></span>

> [!NOTE]
> <span data-ttu-id="2d5e4-103">Макеты и скрипты сайтов находятся на стадии тестирования и могут меняться.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-103">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="2d5e4-104">В настоящее время в рабочих средах их можно использовать только в выпуске Targeted.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-104">They are currently only supported for use in production environments in Targeted Release.</span></span>

<span data-ttu-id="2d5e4-105">SharePoint содержит несколько макетов, уже доступных в шаблонах сайтов SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-105">SharePoint contains several site designs already available in the SharePoint Online site templates.</span></span> <span data-ttu-id="2d5e4-106">Это стандартные дизайны сайтов.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-106">These are the default site designs.</span></span> <span data-ttu-id="2d5e4-107">Вы можете изменить их с помощью PowerShell или REST API для контролирования всего процесса подготовки сайта.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-107">You can modify them using PowerShell or the REST APIs to control the entire site provisioning experience.</span></span> <span data-ttu-id="2d5e4-108">Например, вы можете сделать так, чтобы тема организации применялась к каждому создаваемому сайту.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-108">For example, you can ensure that your company theme is applied to every site that gets created.</span></span> <span data-ttu-id="2d5e4-109">Вы также можете обеспечить обязательное ведение журнала независимо от того, какой дизайн сайта выбран.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-109">Or you can make sure a logging mechanism always runs regardless of which site design is chosen.</span></span>

## <a name="apply-a-site-design-to-the-default-site-designs"></a><span data-ttu-id="2d5e4-110">Применение к стандартным дизайнам сайтов другого дизайна сайта</span><span class="sxs-lookup"><span data-stu-id="2d5e4-110">Apply a site design to the default site designs</span></span>

<span data-ttu-id="2d5e4-111">Чтобы настроить стандартные дизайны сайтов, примените новый дизайн с помощью командлета Powershell **Add-SPOSiteDesign** или REST API **CreateSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-111">To customize the default site designs, apply a new one with the Powershell **Add-SPOSiteDesign** cmdlet, or the **CreateSiteDesign** REST API.</span></span> <span data-ttu-id="2d5e4-112">Укажите параметр **IsDefault**, чтобы применить макет сайта в качестве стандартного.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-112">Specify the **IsDefault** switch to apply the site design as default.</span></span> 

<span data-ttu-id="2d5e4-113">Идентификатор WebTemplate для сайта группы — 64, для сайта для общения — 68.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-113">The WebTemplate ID for a Group-connected team site is 64; for a communication site it is 68.</span></span>

<span data-ttu-id="2d5e4-114">В приведенном ниже примере показано, как с помощью параметра **IsDefault** применить тему организации Contoso к стандартным макетам сайта.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-114">The following example shows how to use the **IsDefault** switch to apply the Contoso company theme to the default site designs.</span></span> <span data-ttu-id="2d5e4-115">Скрипт сайта, на который можно ссылаться по ИД, содержит скрипт JSON для применения правильной темы.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-115">The site script referenced by ID contains the JSON script to apply the correct theme.</span></span>

```powershell
C:\> Add-SPOSiteDesign `
  -Title "Contoso company theme" `
  -WebTemplate "68" `
  -SiteScripts "89516c6d-9f4d-4a57-ae79-36b0c95a817b" `
  -Description "Applies standard company theme to site" `
  -IsDefault
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.CreateSiteDesign", {info:{Title:"Contoso company theme", Description:"Applies standard company theme to site", SiteScriptIds:["89516c6d-9f4d-4a57-ae79-36b0c95a817b"],  WebTemplate:"68", IsDefault: true}});
```

## <a name="which-default-site-designs-are-updated"></a><span data-ttu-id="2d5e4-116">Какие стандартные дизайны сайта обновляются?</span><span class="sxs-lookup"><span data-stu-id="2d5e4-116">Which default site designs are updated?</span></span>

<span data-ttu-id="2d5e4-117">В предыдущем примере значение 68 для параметра **WebTemplate** относится к шаблону сайта SharePoint Online для общения.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-117">In the previous example, the **WebTemplate** value of "68" refers to the SharePoint Online communication site template.</span></span> <span data-ttu-id="2d5e4-118">Этот шаблон содержит следующие дизайны сайта по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="2d5e4-118">That template contains the following default site designs:</span></span>

- <span data-ttu-id="2d5e4-119">"Тема";</span><span class="sxs-lookup"><span data-stu-id="2d5e4-119">Topic</span></span>
- <span data-ttu-id="2d5e4-120">"Демонстрация";</span><span class="sxs-lookup"><span data-stu-id="2d5e4-120">Showcase</span></span>
- <span data-ttu-id="2d5e4-121">"Пустой".</span><span class="sxs-lookup"><span data-stu-id="2d5e4-121">Blank</span></span>

<span data-ttu-id="2d5e4-122">Применяя новый дизайн сайта, вы одновременно обновляете все три дизайна сайта, используемые по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-122">When you apply a new site design, it will update all three of the default site designs at the same time.</span></span>

<span data-ttu-id="2d5e4-123">Шаблон сайта группы SharePoint Online содержит только один стандартный дизайн с именем **Группа**.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-123">The SharePoint Online team site template contains only one default site design named **Team**.</span></span> <span data-ttu-id="2d5e4-124">В этом случае при применении стандартного дизайна сайта обновляется только дизайн сайта **Группа**.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-124">In this case when you apply a default site design, only the **Team** site design is updated.</span></span>

## <a name="restoring-the-default-site-designs"></a><span data-ttu-id="2d5e4-125">Восстановление стандартных дизайнов сайтов</span><span class="sxs-lookup"><span data-stu-id="2d5e4-125">Restoring the default site designs</span></span>

<span data-ttu-id="2d5e4-126">Чтобы восстановить стандартный дизайн сайта, удалите примененный дизайн сайта.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-126">To restore a site design to the defaults, remove the site design you applied.</span></span> <span data-ttu-id="2d5e4-127">Если бы в предыдущем примере у созданного дизайна сайта был ИД db752673-18fd-44db-865a-aa3e0b28698e, его можно было бы удалить так, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-127">In the previous example, if the site design created had the ID db752673-18fd-44db-865a-aa3e0b28698e, you would remove it as shown in the following example.</span></span>

```powershell
C:\> Remove-SPOSiteDesign db752673-18fd-44db-865a-aa3e0b28698e
```
```javascript
RestRequest("/_api/Microsoft.Sharepoint.Utilities.WebTemplateExtensions.SiteScriptUtility.DeleteSiteDesign", {id:"db752673-18fd-44db-865a-aa3e0b28698e"});
```

> [!NOTE]
> <span data-ttu-id="2d5e4-128">Если вы не знаете, какой дизайн сайта используется по умолчанию, запустите командлет **Get-SPOSiteDesign**.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-128">If you're not sure which site design is the default, run the **Get-SPOSiteDesign** cmdlet.</span></span> <span data-ttu-id="2d5e4-129">Он перечислит все дизайны сайтов и укажет, какие из них стандартные.</span><span class="sxs-lookup"><span data-stu-id="2d5e4-129">It will list all site designs, and indicates which ones are defaults.</span></span>
