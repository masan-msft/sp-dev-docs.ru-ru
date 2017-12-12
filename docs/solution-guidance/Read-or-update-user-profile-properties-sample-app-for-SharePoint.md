---
title: "Доступ на чтение или обновление свойств профиля пользователя образец надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: a8bbb4cba2414d7c95beb8e09f480b8e5307c02f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="read-or-update-user-profile-properties-sample-add-in-for-sharepoint"></a>Доступ на чтение или обновление свойств профиля пользователя образец надстройки для SharePoint

Размещение у поставщика в надстройке можно использовать для чтения или обновления SharePoint одним или несколькими значениями свойств профиля.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
В примере [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) показано, как для чтения и обновления свойств профилей пользователей для определенного пользователя. В этом примере использует размещение у поставщика в надстройке для:

- Чтение и отображение всех свойств профиля пользователя для пользователя.
    
- Обновление свойства профиля пользователя с одним значением.
    
- Обновление свойства профиля пользователя с несколькими значениями.
    
Если вы хотите используйте этого решения:

- Чтение и запись данных в свойство профиля пользователя для пользователя. 
    
- Использование значений свойств профиля пользователя для индивидуальной настройки SharePoint.

> [!NOTE] 
> В этом примере кода выполняется только на Office 365. 

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Перед запуском сценария 1:

1. В верхней части сайта Office 365 выберите изображение профиля и выберите команду **сведения обо мне**, как показано на рисунке 1. 
    
2. На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.
    
3. **Сведения обо мне**, введите работы в компании Contoso.
    
4. Выберите команду **Сохранить все и закрыть**. 
    
Перед запуском сценария 3:

1. В верхней части веб-узла выберите изображение профиля и выберите команду **сведения обо мне**, как показано на рисунке 1. 
    
2. На странице " **сведения обо мне** " нажмите кнопку **Изменить профиль**.
    
3. **Изменение сведений**выберите **сведения**.
    
4. **Навыки**введите в C#, JavaScript.
    
5. Выберите команду **Сохранить все и закрыть**. 

**На рисунке 1. Переход к странице профиля пользователя, выбрав сведения обо мне**

![Снимок экрана страницы профиля пользователя с помощью сведения обо мне с выделением](media/692b9a82-45df-4c82-960b-42281be39f1c.png)

## <a name="using-the-userprofilemanipulationcsom-app"></a>С помощью приложения UserProfile.Manipulation.CSOM
<a name="sectionSection1"> </a>

При запуске в этом примере у поставщика надстройки с запускается, как показано на рисунке 2.

**На рисунке 2. Начальная страница приложения UserProfile.Manipulation.CSOM**

![Снимок экрана с начальной страницы приложения UserProfile.Manipulation.CSOM](media/ec62daf7-1323-4a12-b2c4-a95e0312c58f.png)

В этом примере кода включает в себя три сценария.

|Сценарий|Показано, как...|
|:---|:---|
|1|Чтение всех свойств профиля пользователя для пользователя, выполняющего приложение.|
|2|<p>Обновление свойства профиля пользователя с одним значением.</p><p>**Примечание**: этот сценарий поддерживается только в Office 365.</p>|
|3|<p>Обновление свойства профиля пользователя с несколькими значениями.</p><p>**Примечание**: этот сценарий поддерживается только в Office 365.</p>|

### <a name="scenario-1-read-all-user-profile-properties"></a>Сценарий 1: Чтение всех свойств профиля пользователя

При выборе команды **выполнить сценарий 1**надстройки считывает все свойства профиля пользователя для текущего пользователя и отображает данные профиля пользователя в **текущем свойств профилей пользователей**, как показано на рисунке 3.

**На рисунке 3. Данные свойства профиля текущего пользователя**

![Снимок экрана с данных свойств профиля текущего пользователя](media/012475be-21d7-48b1-bce2-1e863e025c0d.png)

Выбор **выполнения сценария 1** вызывает метод **btnScenario1_Click** в CodeSample1.aspx.cs для выполнения следующих задач:

- Используйте **PeopleManager** для извлечения всех свойств профиля пользователя для текущего пользователя.
    
- Выполните итерацию по **PersonProperties.UserProfileProperties** получение списка значений свойств профиля пользователя в текстовом поле.
    
> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

### <a name="scenario-2-update-a-single-valued-user-profile-property"></a>Сценарий 2: Обновление свойства профиля пользователя с одним значением

Сценарий 2 показано, как обновить свойство профиля пользователя с одним значением. Как показано на рисунке 4, текущее значение **сведения обо мне** свойство профиля пользователя для пользователя, выполняющего эта надстройка — это **место работы Contoso**. Обновление значения **сведения обо мне** свойство профиля пользователя, в поле **новое значение сведения обо мне** enterI am разработчик программного обеспечения в компании Contoso и нажмите кнопку **запустить сценарий 2**. Код обновляется значение свойства **сведения обо мне** и **я разработчик программного обеспечения в компании Contoso**. Как показано на рисунке 5, надстройка обновляет **сведения обо мне текущее значение** новое значение **сведения обо мне** свойство профиля пользователя.

**На рисунке 4. Сценарий 2 начальной страницы**

![Снимок экрана с начальной страницы для сценария 2](media/ca229e30-e418-4701-a991-cf669cbc7483.png)

**На рисунке 5. Обновлены сведения обо мне свойства профиля пользователя**

![Снимок экрана с обновленные сведения обо мне свойство профиля пользователя](media/9ffc34d9-b9b5-481c-8b63-fa28bc883d04.png)

Выбор **выполнения сценария 2** вызывает метод **btnScenario2_Click** в CodeSample2.aspx.cs для выполнения следующих:

- Используйте **PeopleManager** для получения свойств профиля текущего пользователя.
    
- Формате текст, введенный пользователем в формате HTML.
    
- Обновите значение свойства профиля пользователя **AboutMe** с помощью **SetSingleValueProfileProperty**.  **SetSingleValueProfileProperty** принимает три параметра:
    
    - Имя учетной записи пользователя, профиль пользователя для обновления.
    
    - Имя свойства профиля пользователя ( **AboutMe** в этом сценарии).
    
    - Значение свойства, в формате HTML (** я разработчик программного обеспечения в компании Contoso ** в этом сценарии).
    
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
> Если вы используете свойства профиля пользователя, настройте свойство для редактироваться пользователями. Метод, используемый в данном сценарии будет работать для свойств профиля пользователя. 

### <a name="scenario-3-update-a-multivalued-user-profile-property"></a>Сценарий 3: Обновление свойства профиля пользователя с несколькими значениями

Сценарий 3 показано, как обновить свойство профиля пользователя с несколькими значениями. На рисунке 6 показан начальной страницы для сценария 3.  **Текущее значение навыки** показывает навыки пользователя, выполняющего приложение. Навыков считываются из свойства профиля пользователя SPS-навыки для пользователя.

**На рисунке 6. Сценарий 3 начальной страницы**

![Снимок экрана с начальной страницы для сценария 3](media/30926c45-3ecc-4c7d-bc27-d896fc6136b2.png)

Добавление нового свойства профиля пользователя SPS-навыки из эта надстройка:

1. Введите HTML5 и нажмите кнопку **Добавить навыков**. 
    
2. Введите ASP.Net и нажмите кнопку **Добавить навыков**. 
    
3. Выберите пункт **выполнить сценарий 3**.
    
4. Убедитесь, что **текущее значение навыки** отображаются новый список навыки, необходимые для пользователя.
    
5. Убедитесь, что свойство профиля пользователя **SPS-навыки** для пользователя теперь отображается новый список навыков.
    
Выбор **выполнения сценария 3** вызывает **btnScenario3_Click** в CodeSample3.aspx.cs для выполнения следующих:

- Используйте **PeopleManager** для получения свойств профиля текущего пользователя.
    
- Чтение списка навыки, отображаемое в поле списка. 
    
- Сохраните новые навыки свойство профиля пользователя **SPS-навыки работы** с помощью **SetMultiValuedProfileProperty**.  **SetMultiValuedProfileProperty** принимает три параметра:
    
    - Имя учетной записи пользователя, профиль которого пользователь обновляется.
    
    - Имя свойства пользователя профиля, являющийся **SPS-навыки**.
    
    - Значения свойств, как **список** объектов string.

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
## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Решения пользовательского профиля для SharePoint 2013 и SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Пример Search.PersonalizedResults](https://github.com/SharePoint/PnP/tree/master/Samples/Search.PersonalizedResults)
