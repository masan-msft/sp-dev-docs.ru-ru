---
title: "Используйте возможности локализации в Office 365 пример надстройки"
ms.date: 11/03/2017
ms.openlocfilehash: e3f6644f841f53b8e62e95ed626477aef0b0ac6b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-localization-features-in-office-365-sample-add-in"></a><span data-ttu-id="bfe74-102">Используйте возможности локализации в Office 365 пример надстройки</span><span class="sxs-lookup"><span data-stu-id="bfe74-102">Use localization features in Office 365 sample add-in</span></span>

<span data-ttu-id="bfe74-103">Можно использовать возможности локализации в Office 365 для предоставления локализованных значений для сайтов, списков, типов контента и столбцы сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bfe74-103">You can use the localization features in Office 365 to provide localized values for SharePoint sites, lists, content types, and site columns.</span></span> 
    
<span data-ttu-id="bfe74-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="bfe74-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="bfe74-105">Пример [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) показано, как использовать возможности локализации Office 365 на сайты, списки, типы контента и столбцы сайта.</span><span class="sxs-lookup"><span data-stu-id="bfe74-105">The [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) sample shows you how to use the localization features of Office 365 on sites, lists, content types, and site columns.</span></span> <span data-ttu-id="bfe74-106">В этом образце кода используется консольного приложения для выполнения следующих:</span><span class="sxs-lookup"><span data-stu-id="bfe74-106">This code sample uses a console application to do the following:</span></span>

- <span data-ttu-id="bfe74-107">Создание типов контента, столбцы сайтов и списков и свяжите столбцы сайта с помощью типов содержимого.</span><span class="sxs-lookup"><span data-stu-id="bfe74-107">Create content types, site columns, and lists, and associate site columns with content types.</span></span>
    
- <span data-ttu-id="bfe74-108">Локализация типа контента, столбец сайта, списка и сайта, предоставленный пользователем.</span><span class="sxs-lookup"><span data-stu-id="bfe74-108">Localize the content type, site column, list, and a user-supplied site.</span></span>

> [!NOTE] 
> <span data-ttu-id="bfe74-109">Локализация компонентов, описанных в этой статье доступны только в Office 365.</span><span class="sxs-lookup"><span data-stu-id="bfe74-109">The localization features described in this article are only available in Office 365.</span></span> <span data-ttu-id="bfe74-110">Сведения о возможности локализации, доступные в Office 365 выделенных или SharePoint Server 2013 в локальной можно [как: локализация надстроек для SharePoint](http://msdn.microsoft.com/library/907a9189-7ce3-469a-8c87-4cef26f03c73.aspx) и [решений SharePoint локализации](https://msdn.microsoft.com/en-us/library/ee696750.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfe74-110">For information about the localization features that are available in Office 365 Dedicated or SharePoint Server 2013 on-premises, see  [How to: Localize add-ins for SharePoint](http://msdn.microsoft.com/library/907a9189-7ce3-469a-8c87-4cef26f03c73.aspx) and [Localizing SharePoint solutions](https://msdn.microsoft.com/en-us/library/ee696750.aspx).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bfe74-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bfe74-111">Before you begin</span></span>
<span data-ttu-id="bfe74-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe74-112"></span></span>

<span data-ttu-id="bfe74-113">Чтобы начать работу, загрузите пример надстройки [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="bfe74-113">To get started, download the  [Core.CreateContentTypes](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="bfe74-114">Прежде чем запускать этот пример кода:</span><span class="sxs-lookup"><span data-stu-id="bfe74-114">Before you run this code sample:</span></span>

1. <span data-ttu-id="bfe74-115">Настройка языковых параметров на вашем сайте.</span><span class="sxs-lookup"><span data-stu-id="bfe74-115">Configure the language settings on your site.</span></span> <span data-ttu-id="bfe74-116">Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="bfe74-116">To do this:</span></span>
    
      <span data-ttu-id="bfe74-117">.</span><span class="sxs-lookup"><span data-stu-id="bfe74-117">a.</span></span> <span data-ttu-id="bfe74-118">На сайте группы выберите **Параметры** > **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-118">On your team site, choose  **Settings** > **Site settings**.</span></span>
    
      <span data-ttu-id="bfe74-119">б.</span><span class="sxs-lookup"><span data-stu-id="bfe74-119">b.</span></span> <span data-ttu-id="bfe74-120">**Администрирование веб-сайтов**выберите **языковые параметры**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-120">In  **Site Administration**, choose  **Language settings**.</span></span>
    
      <span data-ttu-id="bfe74-121">c.</span><span class="sxs-lookup"><span data-stu-id="bfe74-121">c.</span></span> <span data-ttu-id="bfe74-122">На странице **Языковых параметров** в **Альтернативные языки**выберите альтернативные языки, которые должны поддерживать веб-узла.</span><span class="sxs-lookup"><span data-stu-id="bfe74-122">On the  **Language Settings** page, in **Alternate language(s)**, choose the alternate languages your site should support.</span></span> <span data-ttu-id="bfe74-123">Например вы можете французский и финский, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="bfe74-123">For example, you can choose French and Finnish, as shown in Figure 1.</span></span>
    
      <span data-ttu-id="bfe74-124">d.</span><span class="sxs-lookup"><span data-stu-id="bfe74-124">d.</span></span> <span data-ttu-id="bfe74-125">Нажмите кнопку  **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-125">Choose  **OK**.</span></span>
     
2. <span data-ttu-id="bfe74-126">Задайте язык отображения на странице профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="bfe74-126">Set the display language on your user's profile page.</span></span> <span data-ttu-id="bfe74-127">Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="bfe74-127">To do this:</span></span>
    
      <span data-ttu-id="bfe74-128">.</span><span class="sxs-lookup"><span data-stu-id="bfe74-128">a.</span></span> <span data-ttu-id="bfe74-129">В верхней части сайта Office 365 выберите изображение профиля и выберите команду **сведения обо мне**, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="bfe74-129">At the top of your Office 365 site, choose your profile picture, and then choose  **About me**, as shown in Figure 2.</span></span>
    
      <span data-ttu-id="bfe74-130">б.</span><span class="sxs-lookup"><span data-stu-id="bfe74-130">b.</span></span> <span data-ttu-id="bfe74-131">На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-131">On the  **About me** page, choose **Edit your profile**.</span></span>
    
      <span data-ttu-id="bfe74-132">c.</span><span class="sxs-lookup"><span data-stu-id="bfe74-132">c.</span></span> <span data-ttu-id="bfe74-133">Выберите **...** (Дополнительные параметры) и затем выберите **языка и региона**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-133">Choose  **...** (additional options), and then choose **Language and Region**.</span></span>
    
      <span data-ttu-id="bfe74-134">d.</span><span class="sxs-lookup"><span data-stu-id="bfe74-134">d.</span></span> <span data-ttu-id="bfe74-135">На **Мой языки**, нажмите кнопку Новый язык, аналогичный тому, задайте на сайте, используя раскрывающийся список **выбрать новый язык** , нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-135">In  **My Display Languages**, choose a new language similar to the one you set on the site using the  **Pick a new language** dropdown, then choose **Add**.</span></span> <span data-ttu-id="bfe74-136">Например выберите французский и финский, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="bfe74-136">For example, choose French and Finnish, as shown in Figure 3.</span></span> <span data-ttu-id="bfe74-137">Вы можете переместить предпочитаемый язык вверх или вниз, выбрав вверх и вниз стрелки.</span><span class="sxs-lookup"><span data-stu-id="bfe74-137">You can move your preferred language up or down by choosing the up and down arrows.</span></span>
    
      <span data-ttu-id="bfe74-138">e.</span><span class="sxs-lookup"><span data-stu-id="bfe74-138">e.</span></span> <span data-ttu-id="bfe74-139">Выберите команду **Сохранить все и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-139">Choose  **Save all and close**.</span></span>

> [!NOTE] 
> <span data-ttu-id="bfe74-140">Выполнение может занять несколько минут для сайта отобразить в выбранные языки.</span><span class="sxs-lookup"><span data-stu-id="bfe74-140">It might take a few minutes for your site to render in the selected language(s).</span></span> 

<span data-ttu-id="bfe74-141">**На рисунке 1. Языковые параметры для сайта**</span><span class="sxs-lookup"><span data-stu-id="bfe74-141">**Figure 1. Language settings for a site**</span></span>

![Снимок экрана, который отображает параметры языка для сайта.](media/ffe149ae-17ab-4c55-a611-d47f4eb88c4e.png)

<span data-ttu-id="bfe74-143">**На рисунке 2. Переход к странице профиля пользователя, выбрав сведения обо мне**</span><span class="sxs-lookup"><span data-stu-id="bfe74-143">**Figure 2. Navigating to a user's profile page by choosing About me**</span></span>

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением](media/764b2ac2-155b-4ce9-b8eb-3ae04ad26593.png)

<span data-ttu-id="bfe74-145">**На рисунке 3. Изменение языка интерфейса пользователя на странице профиля пользователя**</span><span class="sxs-lookup"><span data-stu-id="bfe74-145">**Figure 3. Changing a user's display language settings on the user's profile page**</span></span>

![Снимок экрана в разделе языка и региона страницы профиля](media/ae5f565d-c932-43dd-9dc3-87630cee3692.png)

## <a name="using-the-corecreatecontenttypes-sample-app"></a><span data-ttu-id="bfe74-147">Использование примера приложения Core.CreateContentTypes</span><span class="sxs-lookup"><span data-stu-id="bfe74-147">Using the Core.CreateContentTypes sample app</span></span>
<span data-ttu-id="bfe74-148"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe74-148"></span></span>

<span data-ttu-id="bfe74-149">При запуске в этом примере кода отображаются консольного приложения как показано на рисунке 4.</span><span class="sxs-lookup"><span data-stu-id="bfe74-149">When you run this code sample, a console application displays, as shown in Figure 4.</span></span> <span data-ttu-id="bfe74-150">Необходимо предоставить учетные данные администратора Office 365 и сайта для локализации.</span><span class="sxs-lookup"><span data-stu-id="bfe74-150">You need to supply the site to localize, and your Office 365 administrator's credentials.</span></span> <span data-ttu-id="bfe74-151">После запуска консольного приложения в метод **Main** в файле Program.cs выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="bfe74-151">When the console application runs, the  **Main** method in Program.cs performs the following tasks:</span></span>

- <span data-ttu-id="bfe74-152">Вызывает метод **CreateContentTypeIfDoesNotExist** , чтобы создать тип контента с именем **Contoso документа**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-152">Calls the  **CreateContentTypeIfDoesNotExist** method to create a content type called **Contoso Document**.</span></span>
    
- <span data-ttu-id="bfe74-153">Вызывает метод **CreateSiteColumn** , чтобы создать столбец сайта с именем **Contoso строки**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-153">Calls the  **CreateSiteColumn** method to create a site column called **Contoso String**.</span></span>
    
- <span data-ttu-id="bfe74-154">Вызывает метод **AddSiteColumnToContentType** , чтобы связать столбец сайта **Contoso строки** с типом контента **Документа Contoso** .</span><span class="sxs-lookup"><span data-stu-id="bfe74-154">Calls the  **AddSiteColumnToContentType** method to link the **Contoso String** site column to the **Contoso Document** content type.</span></span>
    
- <span data-ttu-id="bfe74-155">Вызывает метод **CreateCustomList** , чтобы создать новый список с именем **MyList**.</span><span class="sxs-lookup"><span data-stu-id="bfe74-155">Calls the  **CreateCustomList** method to create a new list called **MyList**.</span></span>

<span data-ttu-id="bfe74-156">**На рисунке 4. Core.CreateContentTypes консольного приложения**</span><span class="sxs-lookup"><span data-stu-id="bfe74-156">**Figure 4. Core.CreateContentTypes console application**</span></span>

![Снимок экрана с Core.CreateContentTypes консольного приложения](media/ee806481-0089-4c65-8f8b-027bfff6ddb9.png)

<span data-ttu-id="bfe74-158">Метод **Main** вызывает методы **LocalizeSiteAndList** и **LocalizeContentTypeAndField** .</span><span class="sxs-lookup"><span data-stu-id="bfe74-158">The  **Main** method then calls the **LocalizeSiteAndList** and **LocalizeContentTypeAndField** methods.</span></span> <span data-ttu-id="bfe74-159">Метод **LocalizeSiteAndList** демонстрирует выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="bfe74-159">The **LocalizeSiteAndList** method shows you how to do the following:</span></span>

- <span data-ttu-id="bfe74-160">Установить разные локализованные значения для заголовок и описание сайта, с помощью метода **SetValueForUICulture** на свойства **TitleResource** и **DescriptionResource** на **веб-** объект.</span><span class="sxs-lookup"><span data-stu-id="bfe74-160">Set different localized values for the title and description of a site, by using the  **SetValueForUICulture** method on the **TitleResource** and **DescriptionResource** properties on the **Web** object.</span></span>
    
- <span data-ttu-id="bfe74-161">Установить разные локализованные значения для заголовок и описание сайта, с помощью метода **SetValueForUICulture** на свойства **TitleResource** и **DescriptionResource** на **веб-** объект.</span><span class="sxs-lookup"><span data-stu-id="bfe74-161">Set different localized values for the title and description of a site, by using the  **SetValueForUICulture** method on the **TitleResource** and **DescriptionResource** properties on the **Web** object.</span></span>
    
<span data-ttu-id="bfe74-162">Метод **LocalizeContentTypeAndField** демонстрирует выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="bfe74-162">The  **LocalizeContentTypeAndField** method shows you how to do the following:</span></span>

- <span data-ttu-id="bfe74-163">Установить разные локализованные значения для имени и описания типа контента с помощью метода **SetValueForUICulture** на **NameResource** и **DescriptionResource** свойств объекта **ContentType** .</span><span class="sxs-lookup"><span data-stu-id="bfe74-163">Set different localized values for the name and description of a content type, by using the  **SetValueForUICulture** method on the **NameResource** and **DescriptionResource** properties on the **ContentType** object.</span></span>
    
- <span data-ttu-id="bfe74-164">Установить разные локализованные значения для заголовок и описание сайта, с помощью метода **SetValueForUICulture** на **TitleResource** и **DescriptionResource** свойств объекта **поля** .</span><span class="sxs-lookup"><span data-stu-id="bfe74-164">Set different localized values for the title and description of a site, by using the  **SetValueForUICulture** method on the **TitleResource** and **DescriptionResource** properties on the **Field** object.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="bfe74-165">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="bfe74-165">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
private static void LocalizeSiteAndList(ClientContext cc, Web web)
        {
            // Localize the site title.
            web.TitleResource.SetValueForUICulture("en-US", "Hello World");
            web.TitleResource.SetValueForUICulture("fi-FI", "Hello World - Finnish");
            web.TitleResource.SetValueForUICulture("fr-FR", "Hello World - French");
            // Localize the site description.
            web.DescriptionResource.SetValueForUICulture("en-US", "Hello World site sample");
            web.DescriptionResource.SetValueForUICulture("fi-FI", " Hello World site sample - Finnish");
            web.DescriptionResource.SetValueForUICulture("fr-FR", " Hello World site sample - French");
            web.Update();
            cc.ExecuteQuery();

            // Localize the custom list that was created previously.
            List list = cc.Web.Lists.GetByTitle("MyList");
            cc.Load(list);
            cc.ExecuteQuery();
            // Localize the list title.
            list.TitleResource.SetValueForUICulture("en-US", "Hello World");
            list.TitleResource.SetValueForUICulture("fi-FI", "Hello World - Finnish");
            list.TitleResource.SetValueForUICulture("fr-FR", " Hello World - French");
            // Localize the list description.
            list.DescriptionResource.SetValueForUICulture("en-US", "This example localizes a list using CSOM.");
            list.DescriptionResource.SetValueForUICulture("fi-FI", "This example localizes a list using CSOM - Finnish.");
            list.DescriptionResource.SetValueForUICulture("fr-FR", "This example localizes a list using CSOM - French.");
            list.Update();
            cc.ExecuteQuery();
        }

private static void LocalizeContentTypeAndField(ClientContext cc, Web web)
        {
            ContentTypeCollection contentTypes = web.ContentTypes;
            ContentType myContentType = contentTypes.GetById("0x0101009189AB5D3D2647B580F011DA2F356FB2");
            cc.Load(contentTypes);
            cc.Load(myContentType);
            cc.ExecuteQuery();
            // Localize content type name.
            myContentType.NameResource.SetValueForUICulture("en-US", "Contoso Document");
            myContentType.NameResource.SetValueForUICulture("fi-FI", "Contoso Document - Finnish");
            myContentType.NameResource.SetValueForUICulture("fr-FR", "Contoso Document - French");
            // Localize content type description.
            myContentType.DescriptionResource.SetValueForUICulture("en-US", "This is the Contoso Document.");
            myContentType.DescriptionResource.SetValueForUICulture("fi-FI", " This is the Contoso Document - Finnish.");
            myContentType.DescriptionResource.SetValueForUICulture("fr-FR", " This is the Contoso Document - French.");
            myContentType.Update(true);
            cc.ExecuteQuery();

            // Localize the site column.
            FieldCollection fields = web.Fields;
            Field fld = fields.GetByInternalNameOrTitle("ContosoString");
            // Localize site column title.
            fld.TitleResource.SetValueForUICulture("en-US", "Contoso String");
            fld.TitleResource.SetValueForUICulture("fi-FI", "Contoso String - Finnish");
            fld.TitleResource.SetValueForUICulture("fr-FR", "Contoso String - French");
            // Localize site column description.
            fld.DescriptionResource.SetValueForUICulture("en-US", "Used to store Contoso specific metadata.");
            fld.DescriptionResource.SetValueForUICulture("fi-FI", "Used to store Contoso specific metadata - Finnish.");
            fld.DescriptionResource.SetValueForUICulture("fr-FR", "Used to store Contoso specific metadata - French.");
            fld.UpdateAndPushChanges(true);
            cc.ExecuteQuery();
        }
```

<span data-ttu-id="bfe74-166">Как показано на рисунке 5, веб-узла отображает пользовательский заголовок французского **Hello World — французский**, которое было задано с помощью метода **LocalizeSiteAndList** .</span><span class="sxs-lookup"><span data-stu-id="bfe74-166">As shown in Figure 5, your site displays your custom French title  **Hello World - French**, which was set using the  **LocalizeSiteAndList** method.</span></span>

<span data-ttu-id="bfe74-167">**На рисунке 5. Настраиваемая страница заголовка, обновлены с помощью метода LocalizeSiteAndList**</span><span class="sxs-lookup"><span data-stu-id="bfe74-167">**Figure 5. Customized page title updated by the LocalizeSiteAndList method**</span></span>

![Снимок экрана заголовка обновленные настраиваемая страница](media/14471283-f7b6-49ca-a507-a3e28e43ee22.png)

## <a name="see-also"></a><span data-ttu-id="bfe74-169">См. также</span><span class="sxs-lookup"><span data-stu-id="bfe74-169">See also</span></span>
<span data-ttu-id="bfe74-170"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bfe74-170"></span></span>

-  [<span data-ttu-id="bfe74-171">Локализация решения для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="bfe74-171">Localization solutions for SharePoint 2013 and SharePoint Online</span></span>](localization-solutions-for-sharepoint-2013-and-sharepoint-online.md)
    
-  [<span data-ttu-id="bfe74-172">Core.CreateContentTypes</span><span class="sxs-lookup"><span data-stu-id="bfe74-172">Core.CreateContentTypes</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.CreateContentTypes)
    
-  [<span data-ttu-id="bfe74-173">Управление контентом корпоративных решений для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="bfe74-173">Enterprise content management solutions for SharePoint 2013 and SharePoint Online</span></span>](Enterprise-Content-Management-solutions-for-SharePoint-2013-and-SharePoint-Online.md)
