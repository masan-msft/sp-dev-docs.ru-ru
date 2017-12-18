---
title: "Доступ на чтение или обновление свойств профиля пользователя образец надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a8bbb4cba2414d7c95beb8e09f480b8e5307c02f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="read-or-update-user-profile-properties-sample-add-in-for-sharepoint"></a><span data-ttu-id="aecaf-102">Доступ на чтение или обновление свойств профиля пользователя образец надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="aecaf-102">Read or update user profile properties sample add-in for SharePoint</span></span>

<span data-ttu-id="aecaf-103">Размещение у поставщика в надстройке можно использовать для чтения или обновления SharePoint одним или несколькими значениями свойств профиля.</span><span class="sxs-lookup"><span data-stu-id="aecaf-103">You can use a provider-hosted add-in to read or update SharePoint single and multivalued user profile properties.</span></span>

<span data-ttu-id="aecaf-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="aecaf-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="aecaf-105">В примере [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) показано, как для чтения и обновления свойств профилей пользователей для определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-105">The [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) sample shows you how to read and update user profile properties for a particular user.</span></span> <span data-ttu-id="aecaf-106">В этом примере использует размещение у поставщика в надстройке для:</span><span class="sxs-lookup"><span data-stu-id="aecaf-106">This sample uses a provider-hosted add-in to:</span></span>

- <span data-ttu-id="aecaf-107">Чтение и отображение всех свойств профиля пользователя для пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-107">Read and display all user profile properties for a user.</span></span>
    
- <span data-ttu-id="aecaf-108">Обновление свойства профиля пользователя с одним значением.</span><span class="sxs-lookup"><span data-stu-id="aecaf-108">Update a single-valued user profile property.</span></span>
    
- <span data-ttu-id="aecaf-109">Обновление свойства профиля пользователя с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="aecaf-109">Update a multivalued user profile property.</span></span>
    
<span data-ttu-id="aecaf-110">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="aecaf-110">Use this solution if you want to:</span></span>

- <span data-ttu-id="aecaf-111">Чтение и запись данных в свойство профиля пользователя для пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-111">Read or write data to a user profile property for a user.</span></span> 
    
- <span data-ttu-id="aecaf-112">Использование значений свойств профиля пользователя для индивидуальной настройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="aecaf-112">Use user profile property values to personalize SharePoint.</span></span>

> [!NOTE] 
> <span data-ttu-id="aecaf-113">В этом примере кода выполняется только на Office 365.</span><span class="sxs-lookup"><span data-stu-id="aecaf-113">This code sample only runs on Office 365.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="aecaf-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="aecaf-114">Before you begin</span></span>
<span data-ttu-id="aecaf-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="aecaf-115"></span></span>

<span data-ttu-id="aecaf-116">Чтобы начать работу, загрузите пример надстройки [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="aecaf-116">To get started, download the  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="aecaf-117">Перед запуском сценария 1:</span><span class="sxs-lookup"><span data-stu-id="aecaf-117">Before you run Scenario 1:</span></span>

1. <span data-ttu-id="aecaf-118">В верхней части сайта Office 365 выберите изображение профиля и выберите команду **сведения обо мне**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="aecaf-118">At the top of your Office 365 site, choose your profile picture, and then choose  **About me**, as shown in Figure 1.</span></span> 
    
2. <span data-ttu-id="aecaf-119">На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-119">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="aecaf-120">**Сведения обо мне**, введите работы в компании Contoso.</span><span class="sxs-lookup"><span data-stu-id="aecaf-120">In  **About me**, enter I work at Contoso.</span></span>
    
4. <span data-ttu-id="aecaf-121">Выберите команду **Сохранить все и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-121">Choose  **Save all and close**.</span></span> 
    
<span data-ttu-id="aecaf-122">Перед запуском сценария 3:</span><span class="sxs-lookup"><span data-stu-id="aecaf-122">Before you run Scenario 3:</span></span>

1. <span data-ttu-id="aecaf-123">В верхней части веб-узла выберите изображение профиля и выберите команду **сведения обо мне**, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="aecaf-123">At the top of your site, choose your profile picture, and then choose  **About me**, as shown in Figure 1.</span></span> 
    
2. <span data-ttu-id="aecaf-124">На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-124">On the  **About me** page, choose **edit your profile**.</span></span>
    
3. <span data-ttu-id="aecaf-125">**Изменение сведений**выберите **сведения**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-125">On  **Edit Details**, choose  **Details**.</span></span>
    
4. <span data-ttu-id="aecaf-126">**Навыки**введите в C#, JavaScript.</span><span class="sxs-lookup"><span data-stu-id="aecaf-126">In  **Skills**, enter C#, JavaScript.</span></span>
    
5. <span data-ttu-id="aecaf-127">Выберите команду **Сохранить все и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-127">Choose  **Save all and close**.</span></span> 

<span data-ttu-id="aecaf-128">**На рисунке 1. Переход к странице профиля пользователя, выбрав сведения обо мне**</span><span class="sxs-lookup"><span data-stu-id="aecaf-128">**Figure 1. Navigating to a user's profile page by choosing About me**</span></span>

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением](media/692b9a82-45df-4c82-960b-42281be39f1c.png)

## <a name="using-the-userprofilemanipulationcsom-app"></a><span data-ttu-id="aecaf-130">С помощью приложения UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="aecaf-130">Using the UserProfile.Manipulation.CSOM app</span></span>
<span data-ttu-id="aecaf-131"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="aecaf-131"></span></span>

<span data-ttu-id="aecaf-132">При запуске в этом примере у поставщика надстройки с запускается, как показано на рисунке 2.</span><span class="sxs-lookup"><span data-stu-id="aecaf-132">When you run this sample, a provider-hosted add-in starts, as shown in Figure 2.</span></span>

<span data-ttu-id="aecaf-133">**На рисунке 2. Начальная страница приложения UserProfile.Manipulation.CSOM**</span><span class="sxs-lookup"><span data-stu-id="aecaf-133">**Figure 2. Start page of the UserProfile.Manipulation.CSOM app**</span></span>

![Снимок экрана с начальной страницы приложения UserProfile.Manipulation.CSOM](media/ec62daf7-1323-4a12-b2c4-a95e0312c58f.png)

<span data-ttu-id="aecaf-135">В этом примере кода включает в себя три сценария.</span><span class="sxs-lookup"><span data-stu-id="aecaf-135">This code sample includes three scenarios.</span></span>

|<span data-ttu-id="aecaf-136">Сценарий</span><span class="sxs-lookup"><span data-stu-id="aecaf-136">Scenario</span></span>|<span data-ttu-id="aecaf-137">Показано, как...</span><span class="sxs-lookup"><span data-stu-id="aecaf-137">Shows how to...</span></span>|
|:---|:---|
|<span data-ttu-id="aecaf-138">1</span><span class="sxs-lookup"><span data-stu-id="aecaf-138">1</span></span>|<span data-ttu-id="aecaf-139">Чтение всех свойств профиля пользователя для пользователя, выполняющего приложение.</span><span class="sxs-lookup"><span data-stu-id="aecaf-139">Read all user profile properties for the user running the app.</span></span>|
|<span data-ttu-id="aecaf-140">2</span><span class="sxs-lookup"><span data-stu-id="aecaf-140">2</span></span>|<p><span data-ttu-id="aecaf-141">Обновление свойства профиля пользователя с одним значением.</span><span class="sxs-lookup"><span data-stu-id="aecaf-141">Update a single-valued user profile property.</span></span></p><p><span data-ttu-id="aecaf-142">**Примечание**: этот сценарий поддерживается только в Office 365.</span><span class="sxs-lookup"><span data-stu-id="aecaf-142">**Note**: This scenario is only supported in Office 365.</span></span></p>|
|<span data-ttu-id="aecaf-143">3</span><span class="sxs-lookup"><span data-stu-id="aecaf-143">3</span></span>|<p><span data-ttu-id="aecaf-144">Обновление свойства профиля пользователя с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="aecaf-144">Update a multivalued user profile property.</span></span></p><p><span data-ttu-id="aecaf-145">**Примечание**: этот сценарий поддерживается только в Office 365.</span><span class="sxs-lookup"><span data-stu-id="aecaf-145">**Note**: This scenario is only supported in Office 365.</span></span></p>|

### <a name="scenario-1-read-all-user-profile-properties"></a><span data-ttu-id="aecaf-146">Сценарий 1: Чтение всех свойств профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="aecaf-146">Scenario 1: Read all user profile properties</span></span>

<span data-ttu-id="aecaf-147">При выборе команды **выполнить сценарий 1**надстройки считывает все свойства профиля пользователя для текущего пользователя и отображает данные профиля пользователя в **текущем свойств профилей пользователей**, как показано на рисунке 3.</span><span class="sxs-lookup"><span data-stu-id="aecaf-147">When you choose  **Run scenario 1**, the add-in reads all user profile properties for the current user, and then displays the user profile data in  **Current user profile properties**, as shown in Figure 3.</span></span>

<span data-ttu-id="aecaf-148">**На рисунке 3. Данные свойства профиля текущего пользователя**</span><span class="sxs-lookup"><span data-stu-id="aecaf-148">**Figure 3. Current user's profile properties data**</span></span>

![Снимок экрана с данных свойств профиля текущего пользователя](media/012475be-21d7-48b1-bce2-1e863e025c0d.png)

<span data-ttu-id="aecaf-150">Выбор **выполнения сценария 1** вызывает метод **btnScenario1_Click** в CodeSample1.aspx.cs для выполнения следующих задач:</span><span class="sxs-lookup"><span data-stu-id="aecaf-150">Choosing  **Run scenario 1** calls the **btnScenario1_Click** method in CodeSample1.aspx.cs to perform the following tasks:</span></span>

- <span data-ttu-id="aecaf-151">Используйте **PeopleManager** для извлечения всех свойств профиля пользователя для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-151">Use  **PeopleManager** to retrieve all the user profile properties for the current user.</span></span>
    
- <span data-ttu-id="aecaf-152">Выполните итерацию по **PersonProperties.UserProfileProperties** получение списка значений свойств профиля пользователя в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="aecaf-152">Iterate over  **PersonProperties.UserProfileProperties** to list the values of the user profile properties in a text box.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="aecaf-153">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="aecaf-153">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
protected void btnScenario1_Click(object sender, EventArgs e)
        {

            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the people manager instance and load current properties.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties);
                clientContext.ExecuteQuery();

                // Output user profile properties to a text box.
                txtProperties.Text = "";
                foreach (var item in personProperties.UserProfileProperties)
                {
                    txtProperties.Text += string.Format("{0} - {1}{2}", item.Key, item.Value, Environment.NewLine);
                }
            }
        }
```

### <a name="scenario-2-update-a-single-valued-user-profile-property"></a><span data-ttu-id="aecaf-154">Сценарий 2: Обновление свойства профиля пользователя с одним значением</span><span class="sxs-lookup"><span data-stu-id="aecaf-154">Scenario 2: Update a single-valued user profile property</span></span>

<span data-ttu-id="aecaf-155">Сценарий 2 показано, как обновить свойство профиля пользователя с одним значением.</span><span class="sxs-lookup"><span data-stu-id="aecaf-155">Scenario 2 shows how to update a single-valued user profile property.</span></span> <span data-ttu-id="aecaf-156">Как показано на рисунке 4, текущее значение **сведения обо мне** свойство профиля пользователя для пользователя, выполняющего эта надстройка — это **место работы Contoso**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-156">As shown in Figure 4, the current value of the  **About me** user profile property for the user running this add-in is **I work at Contoso**.</span></span> <span data-ttu-id="aecaf-157">Обновление значения **сведения обо мне** свойство профиля пользователя, в поле **новое значение сведения обо мне** enterI am разработчик программного обеспечения в компании Contoso и нажмите кнопку **запустить сценарий 2**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-157">To update the value of the  **About me** user profile property, in the **About me new value** box, enterI am a software engineer at Contoso and then choose **Run scenario 2**.</span></span> <span data-ttu-id="aecaf-158">Код обновляется значение свойства **сведения обо мне** и **я разработчик программного обеспечения в компании Contoso**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-158">The code updates the value of the  **About me** property to **I am a software engineer at Contoso**.</span></span> <span data-ttu-id="aecaf-159">Как показано на рисунке 5, надстройка обновляет **сведения обо мне текущее значение** новое значение **сведения обо мне** свойство профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-159">As shown in Figure 5, the add-in updates  **About me current value** with the new value of the **About me** user profile property.</span></span>

<span data-ttu-id="aecaf-160">**На рисунке 4. Сценарий 2 начальной страницы**</span><span class="sxs-lookup"><span data-stu-id="aecaf-160">**Figure 4. Scenario 2 start page**</span></span>

![Снимок экрана с начальной страницы для сценария 2](media/ca229e30-e418-4701-a991-cf669cbc7483.png)

<span data-ttu-id="aecaf-162">**На рисунке 5. Обновлены сведения обо мне свойства профиля пользователя**</span><span class="sxs-lookup"><span data-stu-id="aecaf-162">**Figure 5. Updated About me user profile property**</span></span>

![Снимок экрана с обновленные сведения обо мне свойство профиля пользователя](media/9ffc34d9-b9b5-481c-8b63-fa28bc883d04.png)

<span data-ttu-id="aecaf-164">Выбор **выполнения сценария 2** вызывает метод **btnScenario2_Click** в CodeSample2.aspx.cs для выполнения следующих:</span><span class="sxs-lookup"><span data-stu-id="aecaf-164">Choosing  **Run scenario 2** calls the **btnScenario2_Click** method in CodeSample2.aspx.cs to do the following:</span></span>

- <span data-ttu-id="aecaf-165">Используйте **PeopleManager** для получения свойств профиля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-165">Use  **PeopleManager** to get the user profile properties of the current user.</span></span>
    
- <span data-ttu-id="aecaf-166">Формате текст, введенный пользователем в формате HTML.</span><span class="sxs-lookup"><span data-stu-id="aecaf-166">Format the text entered by the user in HTML.</span></span>
    
- <span data-ttu-id="aecaf-167">Обновите значение свойства профиля пользователя **AboutMe** с помощью **SetSingleValueProfileProperty**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-167">Update the value of the  **AboutMe** user profile property by using **SetSingleValueProfileProperty**.</span></span>  <span data-ttu-id="aecaf-168">**SetSingleValueProfileProperty** принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="aecaf-168">**SetSingleValueProfileProperty** accepts three parameters:</span></span>
    
    - <span data-ttu-id="aecaf-169">Имя учетной записи пользователя, профиль пользователя для обновления.</span><span class="sxs-lookup"><span data-stu-id="aecaf-169">The account name of the user whose user profile you're updating.</span></span>
    
    - <span data-ttu-id="aecaf-170">Имя свойства профиля пользователя ( **AboutMe** в этом сценарии).</span><span class="sxs-lookup"><span data-stu-id="aecaf-170">The user profile property name ( **AboutMe** in this scenario).</span></span>
    
    - <span data-ttu-id="aecaf-171">Значение свойства, в формате HTML (** я разработчик программного обеспечения в компании Contoso ** в этом сценарии).</span><span class="sxs-lookup"><span data-stu-id="aecaf-171">The property value, in HTML format ( ** I am a software engineer at Contoso** in this scenario).</span></span>
    
```C#
protected void btnScenario2_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the people manager instance and initialize the account name.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties, p => p.AccountName);
                clientContext.ExecuteQuery();

                // Convert entry to HTML.
                string updatedValue = (txtAboutMe.Text).Replace(Environment.NewLine, "");

                // Update the AboutMe property for the user using account name from the user profile.
                peopleManager.SetSingleValueProfileProperty(personProperties.AccountName, "AboutMe", updatedValue);
                clientContext.ExecuteQuery();

            }
        }
```
    
> [!NOTE] 
> <span data-ttu-id="aecaf-172">Если вы используете свойства профиля пользователя, настройте свойство для редактироваться пользователями.</span><span class="sxs-lookup"><span data-stu-id="aecaf-172">If you use custom user profile properties, configure the property to be editable by users.</span></span> <span data-ttu-id="aecaf-173">Метод, используемый в данном сценарии будет работать для свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-173">The technique used in this scenario will work for custom user profile properties.</span></span> 

### <a name="scenario-3-update-a-multivalued-user-profile-property"></a><span data-ttu-id="aecaf-174">Сценарий 3: Обновление свойства профиля пользователя с несколькими значениями</span><span class="sxs-lookup"><span data-stu-id="aecaf-174">Scenario 3: Update a multivalued user profile property</span></span>

<span data-ttu-id="aecaf-175">Сценарий 3 показано, как обновить свойство профиля пользователя с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="aecaf-175">Scenario 3 shows how to update a multivalued user profile property.</span></span> <span data-ttu-id="aecaf-176">На рисунке 6 показан начальной страницы для сценария 3.</span><span class="sxs-lookup"><span data-stu-id="aecaf-176">Figure 6 shows the start page for Scenario 3.</span></span>  <span data-ttu-id="aecaf-177">**Текущее значение навыки** показывает навыки пользователя, выполняющего приложение.</span><span class="sxs-lookup"><span data-stu-id="aecaf-177">**Skills current value** shows the skills of the user running the app.</span></span> <span data-ttu-id="aecaf-178">Навыков считываются из свойства профиля пользователя SPS-навыки для пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-178">The skills are read from the SPS-Skills user profile property for the user.</span></span>

<span data-ttu-id="aecaf-179">**На рисунке 6. Сценарий 3 начальной страницы**</span><span class="sxs-lookup"><span data-stu-id="aecaf-179">**Figure 6. Scenario 3 start page**</span></span>

![Снимок экрана с начальной страницы для сценария 3](media/30926c45-3ecc-4c7d-bc27-d896fc6136b2.png)

<span data-ttu-id="aecaf-181">Добавление нового свойства профиля пользователя SPS-навыки из эта надстройка:</span><span class="sxs-lookup"><span data-stu-id="aecaf-181">To add new skills to the SPS-Skills user profile property from this add-in:</span></span>

1. <span data-ttu-id="aecaf-182">Введите HTML5 и нажмите кнопку **Добавить навыков**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-182">Enter HTML5, and then choose  **Add Skill**.</span></span> 
    
2. <span data-ttu-id="aecaf-183">Введите ASP.Net и нажмите кнопку **Добавить навыков**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-183">Enter ASP.Net, and then choose  **Add Skill**.</span></span> 
    
3. <span data-ttu-id="aecaf-184">Выберите пункт **выполнить сценарий 3**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-184">Choose  **Run scenario 3**.</span></span>
    
4. <span data-ttu-id="aecaf-185">Убедитесь, что **текущее значение навыки** отображаются новый список навыки, необходимые для пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-185">Verify that  **Skills current value** shows the new list of skills for the user.</span></span>
    
5. <span data-ttu-id="aecaf-186">Убедитесь, что свойство профиля пользователя **SPS-навыки** для пользователя теперь отображается новый список навыков.</span><span class="sxs-lookup"><span data-stu-id="aecaf-186">Verify that the  **SPS-Skills** user profile property for the user now shows the new list of skills.</span></span>
    
<span data-ttu-id="aecaf-187">Выбор **выполнения сценария 3** вызывает **btnScenario3_Click** в CodeSample3.aspx.cs для выполнения следующих:</span><span class="sxs-lookup"><span data-stu-id="aecaf-187">Choosing  **Run scenario 3** calls **btnScenario3_Click** in CodeSample3.aspx.cs to do the following:</span></span>

- <span data-ttu-id="aecaf-188">Используйте **PeopleManager** для получения свойств профиля текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="aecaf-188">Use  **PeopleManager** to get the user profile properties of the current user.</span></span>
    
- <span data-ttu-id="aecaf-189">Чтение списка навыки, отображаемое в поле списка.</span><span class="sxs-lookup"><span data-stu-id="aecaf-189">Read the list of skills shown in the list box.</span></span> 
    
- <span data-ttu-id="aecaf-190">Сохраните новые навыки свойство профиля пользователя **SPS-навыки работы** с помощью **SetMultiValuedProfileProperty**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-190">Save the new skills to the  **SPS-Skills** user profile property by using **SetMultiValuedProfileProperty**.</span></span>  <span data-ttu-id="aecaf-191">**SetMultiValuedProfileProperty** принимает три параметра:</span><span class="sxs-lookup"><span data-stu-id="aecaf-191">**SetMultiValuedProfileProperty** accepts three parameters:</span></span>
    
    - <span data-ttu-id="aecaf-192">Имя учетной записи пользователя, профиль которого пользователь обновляется.</span><span class="sxs-lookup"><span data-stu-id="aecaf-192">The account name of the user whose user profile is being updated.</span></span>
    
    - <span data-ttu-id="aecaf-193">Имя свойства пользователя профиля, являющийся **SPS-навыки**.</span><span class="sxs-lookup"><span data-stu-id="aecaf-193">The user profile property name, which is  **SPS-Skills**.</span></span>
    
    - <span data-ttu-id="aecaf-194">Значения свойств, как **список** объектов string.</span><span class="sxs-lookup"><span data-stu-id="aecaf-194">The property values as a  **List** of string objects.</span></span>

```C#
  protected void btnScenario3_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the people manager instance and initialize the account name.
                PeopleManager peopleManager = new PeopleManager(clientContext);
                PersonProperties personProperties = peopleManager.GetMyProperties();
                clientContext.Load(personProperties, p => p.AccountName);
                clientContext.ExecuteQuery();

                // Collect the user's skills from the list box in order to update the user's profile.
                List<string> skills = new List<string>();
                for (int i = 0; i < lstSkills.Items.Count; i++)
                {
                    skills.Add(lstSkills.Items[i].Value);
                }

                // Update the SPS-Skills property for the user using account name from the user's profile.
                peopleManager.SetMultiValuedProfileProperty(personProperties.AccountName, "SPS-Skills", skills);
                clientContext.ExecuteQuery();

                // Refresh the values.
                RefreshUIValues();
            }

        }
```
## <a name="see-also"></a><span data-ttu-id="aecaf-195">См. также</span><span class="sxs-lookup"><span data-stu-id="aecaf-195">See also</span></span>
<span data-ttu-id="aecaf-196"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="aecaf-196"></span></span>

-  [<span data-ttu-id="aecaf-197">Решения пользовательского профиля для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="aecaf-197">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="aecaf-198">Пример Search.PersonalizedResults</span><span class="sxs-lookup"><span data-stu-id="aecaf-198"> Search.PersonalizedResults sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
