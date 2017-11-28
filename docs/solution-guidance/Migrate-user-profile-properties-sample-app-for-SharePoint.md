---
title: "Перенос пользователей профиля свойств пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 70b8fec69c22a0394184f6af969714d922b4c25a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="migrate-user-profile-properties-sample-add-in-for-sharepoint"></a>Перенос пользователей профиля свойств пример надстройки для SharePoint

Можно использовать размещение у поставщика в надстройке перенос и импортировать данные профилей пользователей SharePoint.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Пример надстройки [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) показано, как для переноса данных профилей пользователей с SharePoint Server 2010 и SharePoint Server 2013 в SharePoint Online.
    
Этот пример включает два консольных приложений. Оба используют userprofileservice.asmx веб-службы для извлечения данных профиля пользователя одним или несколькими значениями в XML-файл, а также для импорта данных в службе профилей пользователей в SharePoint Online.
Если вы хотите используйте в этом примере кода:

- Извлечение данных профиля пользователя в SharePoint Server 2010 и SharePoint Server 2013.
    
- Импортировать данные профилей пользователей в SharePoint Online.

## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев. Пример кода содержит два проекта.

Для проекта **Contoso.ProfileProperty.Migration.Extract** :

- Поскольку в этом примере кода используется на сервере объектной модели, убедитесь, что выполнения проекта на сервере с SharePoint Server 2010 или установки SharePoint Server 2013.
    
- Используйте учетную запись с разрешениями администратора фермы SharePoint.
    
- Измените файл App.config, с помощью сведений о конфигурации, указанные в таблице 1.
    
- Для всех пользователей убедитесь, что свойство профиля пользователя **рабочий адрес электронной почты** не является пустым. Если пустое значение свойства профиля пользователя **электронной почты рабочий** процесс извлечения будет преждевременно.
    
- В этом примере кода извлекает профилей пользователей с SharePoint Server 2010. При извлечении профилей пользователей с SharePoint Server 2013, выполните следующие действия.
    
  . Откройте контекстное меню (щелкните правой кнопкой мыши) для **Contoso.ProfileProperty.Migration.Extract** > **Свойства**.
    
  б. В разделе **приложения**в **требуемой версии .NET framework** выберите **.NET Framework 4**.
    
  c. Нажмите кнопку **Да**, затем **Сохранить**.
    
**В таблице 1. Параметры конфигурации для файла App.Config**

|**Имя параметра конфигурации**|**Описание**|Пример|
|:-----|:-----|:-----|
|**MYSITEHOSTURL** |Мои URL-адрес сайта в исходной ферме SharePoint Server 2010 и SharePoint Server 2013.|http://My.contoso.com |
|**PROPERTYSEPERATOR** |Знак, используемый для разделения нескольких значений в свойства профиля пользователя с несколькими значениями.| |
|**USERPROFILESSTORE** |Путь к файлу XML использовать для записи данных профиля извлеченные пользователя.|C:\temp\ProfileData.XML|
|**ФАЙЛ ЖУРНАЛА** |Путь к файлу XML использовать для записи данных профиля извлеченные пользователя.|C:\temp\Extract.log|
|**ENABLELOGGING** |Включить ведение журнала диска.|Значение true|
|**ТЕСТОВЫЙ ПРОГОН** |Выполняет извлечение тестирования для убедитесь, что указаны правильные параметры конфигурации в файле App.Config.|Установка `TESTRUN=true` при выполнении извлечения тестирования. Запустите тест извлекает только одного пользователя из службы профилей пользователей.<br /> Установка `TESTRUN=false` при извлечении всех пользователей из службы профилей пользователей. |

Для проекта **Contoso.ProfileProperty.Migration.Import**

- Убедитесь, что существуют профили пользователей в Office 365. 
    
- Убедитесь, что адрес **рабочий адрес электронной почты** пользователя — это то же самое, в SharePoint Server 2013 в локальной и службы профилей пользователей Office 365.
    
- В файле App.config измените **значение** элемента параметр **Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService** , чтобы получить справку службы профилей пользователей в центре администрирования SharePoint Online, как показано в Следующий пример.

    ```XML
    <applicationSettings>
    <Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    <setting name="Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService" serializeAs="String">
    <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
    </setting>
    </Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    </applicationSettings>
    ```

- Измените файл App.config, используя параметры конфигурации, указанные в таблице 2.
    
**В таблице 2. Параметры конфигурации файла app.config**

|**Имя параметра конфигурации**|**Описание**|Пример|
|:-----|:-----|:-----|
|**tenantName** |Это имя вашего клиента.|Если URL-адрес клиента http://contoso.onmicrosoft.com, введите contoso как имя клиента.|
|**PROPERTYSEPERATOR** |Знак, используемый для разделения значений в свойства профиля пользователя с несколькими значениями.| |
|**USERPROFILESSTORE** |XML-файл для использования на чтение данных профиля пользователя извлеченные.|C:\temp\ProfileData.XML|
|**ФАЙЛ ЖУРНАЛА** |Файл журнала используется для регистрации событий.|C:\temp\Extract.log|
|**ENABLELOGGING** |Включить ведение журнала диска.|Значение true|
|**SPOAdminUserName** |Имя пользователя администратора Office 365.|Примеры|
|**SPOAdminPassword** |Пароль администратора Office 365.|Примеры|

## <a name="using-the-coreprofilepropertymigration-app"></a>С помощью приложения Core.ProfileProperty.Migration
<a name="sectionSection1"> </a>

В этом примере кода используется в качестве консольного приложения. Пример кода, функция **Main** в файле Program.cs выполняет следующие задачи:

- Подключается к узла личных сайтов и использует **Диспетчер профилей пользователей** для подключения к службе профилей пользователей. **Диспетчер профилей пользователей** , принадлежит к сборке **Microsoft.Office.Server.UserProfiles.dll** .
    
- Создает список с именем **pData** для хранения данных профиля извлеченные пользователя.
    
- Для всех пользователей в службе профилей пользователей выполняет следующие действия:
    
    - Использует **GetSingleValuedProperty** для копирования объект **UserProfileData** с именем **userData** **WorkEmail** и **AboutMe** свойств профиля пользователя.
    
    - Использует **GetMultiValuedProperty** для копирования свойство профиля пользователя **Ответственность за SPS** **userData**.
    
- Использует **UserProfileCollection.Save** для сериализации **userData** в XML-файл. XML-файл сохраняется в путь к файлу, указанному в файле App.config.

**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
static void Main(string[] args)
        {
            int userCount = 1;

            try
            {

                if (Convert.ToBoolean(ConfigurationManager.AppSettings["TESTRUN"]))
                {
                    LogMessage(string.Format("******** RUNNING IN TEST RUN MODE **********"), LogLevel.Debug);
                }
                
                LogMessage(string.Format("Connecting to My Site Host: '{0}'...", ConfigurationManager.AppSettings["MYSITEHOSTURL"]), LogLevel.Info);
                using (SPSite mySite = new SPSite(ConfigurationManager.AppSettings["MYSITEHOSTURL"]))
                {
                    LogMessage(string.Format("Connecting to My Site Host: '{0}'...Done!", ConfigurationManager.AppSettings["MYSITEHOSTURL"]), LogLevel.Info);

                    LogMessage(string.Format("getting Service Context..."), LogLevel.Info);
                    SPServiceContext svcContext = SPServiceContext.GetContext(mySite);
                    LogMessage(string.Format("getting Service Context...Done!"), LogLevel.Info);

                    LogMessage(string.Format("Connecting to Profile Manager..."), LogLevel.Info);
                    UserProfileManager profileManager = new UserProfileManager(svcContext);
                    LogMessage(string.Format("Connecting to Profile Manager...Done!"), LogLevel.Info);

                    // Size of the List is set to the number of profiles.
                    List<UserProfileData> pData = new List<UserProfileData>(Convert.ToInt32(profileManager.Count));
                    
                    // Initialize Serialization Class.
                    UserProfileCollection ups = new UserProfileCollection();

                    foreach (UserProfile spUser in profileManager)
                    {
                        // Get Profile Information.
                        LogMessage(string.Format("processing user '{0}' of {1}...", userCount,profileManager.Count),LogLevel.Info);                       
                        UserProfileData userData = new UserProfileData();
                        
                        userData.UserName = GetSingleValuedProperty(spUser, "WorkEmail");
                        
                        if (userData.UserName != string.Empty)
                        {
                            userData.AboutMe = GetSingleValuedProperty(spUser, "AboutMe");
                            userData.AskMeAbout = GetMultiValuedProperty(spUser, "SPS-Responsibility");
                            pData.Add(userData);
                            // Add to Serialization Class List of Profiles.
                            ups.ProfileData = pData;
                        }
                        
                        LogMessage(string.Format("processing user '{0}' of {1}...Done!", userCount++, profileManager.Count), LogLevel.Info);

                        // Only process the first item if we are in test mode.
                        if (Convert.ToBoolean(ConfigurationManager.AppSettings["TESTRUN"]))
                        {
                            break;
                        }

                    }
                    
                    // Serialize profiles to disk.
                    ups.Save();

                }
            }
            catch(Exception ex)
            {
                LogMessage("Exception trying to get profile properties:\n" + ex.Message, LogLevel.Error);
            }
```

Обратите внимание на то, что метод **GetSingleValuedProperty** используется для получения свойства профиля пользователя с одним значением userprofileservice.asmx. **GetSingleValuedProperty** производит следующие действия, как показано в следующем примере кода:

- Возвращает объект свойства для извлечения данных из с помощью **spuser [userProperty]**.
    
- Возвращает первое значение в **UserProfileValueCollection** , если значение не равно **null**. 

```C#
private static string GetSingleValuedProperty(UserProfile spUser,string userProperty)
        {
            string returnString = string.Empty;
            try
            {
                UserProfileValueCollection propCollection = spUser[userProperty];

                if (propCollection[0] != null)
                {
                    returnString = propCollection[0].ToString();
                }
                else
                {
                    LogMessage(string.Format("User '{0}' does not have a value in property '{1}'", spUser.DisplayName, userProperty), LogLevel.Warning);                       
                }
            }
            catch 
            {
                LogMessage(string.Format("User '{0}' does not have a value in property '{1}'", spUser.DisplayName, userProperty), LogLevel.Warning);                       
            }


            return returnString;
            
        }
```

Обратите внимание на то, что метод **GetMultiValuedProperty** используется для получения свойства профиля пользователя многозначных userprofileservice.asmx. **GetMultiValuedProperty** производит следующие действия, как показано в следующем примере кода:

- Получает объект свойство профиля пользователя с помощью **spuser [userProperty]**.
    
- Создает строку, разделенных точкой с **PROPERTYSEPARATOR** , указанное в файле App.config значений свойств профиля пользователя.

```C#
private static string GetMultiValuedProperty(UserProfile spUser, string userProperty)
        {
            StringBuilder sb = new StringBuilder("");
            string seperator = ConfigurationManager.AppSettings["PROPERTYSEPERATOR"];

            string returnString = string.Empty;
            try
            {

                UserProfileValueCollection propCollection = spUser[userProperty];

                if (propCollection.Count > 1)
                {
                    for (int i = 0; i < propCollection.Count; i++)
                    {
                        if (i == propCollection.Count - 1) { seperator = ""; }
                        sb.AppendFormat("{0}{1}", propCollection[i], seperator);
                    }
                }
                else if (propCollection.Count == 1)
                {
                    sb.AppendFormat("{0}", propCollection[0]);
                }

            }
            catch
            {
                LogMessage(string.Format("User '{0}' does not have a value in property '{1}'", spUser.DisplayName, userProperty), LogLevel.Warning);
            }

            return sb.ToString();

        }
```

## <a name="using-contosoprofilepropertymigrationimport"></a>С помощью Contoso.ProfileProperty.Migration.Import
<a name="sectionSection2"> </a>

В этом примере кода используется в качестве консольного приложения. При запуске образца кода, метод **Main** в файле Program.cs выполняет следующее.

- Инициализирует консольное приложение, с помощью **InitializeConfiguration** и **InitializeWebService**. 
    
- Десериализации XML-файл, содержащий данные профиля извлеченные пользователя.
    
- Для всех пользователей в XML-файле выполняет следующие действия:
    
    - Извлекает свойства **UserName** из XML-файла.
    
    - **SetSingleMVProfileProperty** используется для определения **SPS ответственности** в профиле пользователя.
    
    - **SetSingleMVProfileProperty** используется для определения **AboutMe** на профиль пользователя.
    
**InitializeWebService** подключается к SharePoint Online и задает ссылку службы профилей пользователей для переменной экземпляра. Другие методы в этом примере кода эта переменная экземпляра используется для записи значений свойств профиля пользователя. Для администрирования профилей пользователей, в этом образце кода используется userprofileservice.asmx веб-службы в центре администрирования SharePoint Online.

```C#
static bool InitializeWebService()
        {
            try
            {
                string webServiceExt = "_vti_bin/userprofileservice.asmx";
                string adminWebServiceUrl = string.Empty;
                
                if (_profileSiteUrl.EndsWith("/"))
                    adminWebServiceUrl = _profileSiteUrl + webServiceExt;
                else
                    adminWebServiceUrl = _profileSiteUrl + "/" + webServiceExt;

                LogMessage("Initializing SPO web service " + adminWebServiceUrl, LogLevel.Information);

                SecureString securePassword = GetSecurePassword(_sPoAuthPasword);
                SharePointOnlineCredentials onlineCred = new SharePointOnlineCredentials(_sPoAuthUserName, securePassword);

                string authCookie = onlineCred.GetAuthenticationCookie(new Uri(_profileSiteUrl));

                CookieContainer authContainer = new CookieContainer();
                authContainer.SetCookies(new Uri(_profileSiteUrl), authCookie);

                // Setting up the user profile web service.
                _userProfileService = new UPSvc.UserProfileService();
                _userProfileService.Url = adminWebServiceUrl;

                // Assign previously created auth container to admin profile web service. 
                _userProfileService.CookieContainer = authContainer;
                return true;
            }
            catch (Exception ex)
            {
                LogMessage("Error initiating connection to profile web service in SPO " + ex.Message, LogLevel.Error);
                return false;

            }
            
        }
```

Метод **SetSingleMVProfileProperty** устанавливает многозначных свойство профиля, например **SPS-ответственности**, выполнив следующие:

- Разделение **PropertyValue** в массив строк вызывает **arrs** для хранения значения свойств профиля пользователя. Строка разделяется с помощью параметра конфигурации **PROPERTYSEPERATOR** , указанное в файле App.Config.
    
- Присвоение значения **arrs** массиву **ValueData** на службы профилей пользователей.
    
- Создание массива **PropertyData** для службы профилей пользователей. Имя свойства профиля пользователя и массива **ValueData** передаются в свойства объекта **PropertyData** . Этот массив имеет один элемент только так, как только одно свойство профиля пользователя многозначных будет импортирован.
    
Данные записываются для службы профилей пользователей, с помощью **ModifyUserPropertyByAccountName** на веб-службы **userprofileservice.asmx** в центре администрирования SharePoint Online. Пользователя, выполняющего этот пример кода необходимо иметь полномочия администратора Office 365.

```C#
static void SetSingleMVProfileProperty(string UserName, string PropertyName, string PropertyValue)
        {

            try
            {
                string[] arrs = PropertyValue.Split(ConfigurationManager.AppSettings["PROPERTYSEPERATOR"][0]);
                
               UPSvc.ValueData[] vd = new UPSvc.ValueData[arrs.Count()];
               
               for (int i=0;i<=arrs.Count()-1;i++)
               {
                    vd[i] = new UPSvc.ValueData();
                    vd[i].Value = arrs[i];
                }
               
                UPSvc.PropertyData[] data = new UPSvc.PropertyData[1];
                data[0] = new UPSvc.PropertyData();
                data[0].Name = PropertyName;
                data[0].IsValueChanged = true;
                data[0].Values = vd;
                               
                _userProfileService.ModifyUserPropertyByAccountName(string.Format(@"i:0#.f|membership|{0}", UserName), data);

            }
            catch (Exception ex)
            {
                LogMessage("Exception trying to update profile property " + PropertyName + " for user " + UserName + "\n" + ex.Message, LogLevel.Error);
            }

        }

```

Метод **SetSingleValuedProperty** устанавливает свойства профиля пользователя одним значением, такие как **AboutMe**.  **SetSingleValuedProperty** реализует та же технология, как **SetSingleMVProfileProperty**, но использует **ValueData** массива с только один элемент.

```C#
static void SetSingleProfileProperty(string UserName, string PropertyName, string PropertyValue)
        {

            try
            {
                UPSvc.PropertyData[] data = new UPSvc.PropertyData[1];
                data[0] = new UPSvc.PropertyData();
                data[0].Name = PropertyName;
                data[0].IsValueChanged = true;
                data[0].Values = new UPSvc.ValueData[1];
                data[0].Values[0] = new UPSvc.ValueData();
                data[0].Values[0].Value = PropertyValue;
                _userProfileService.ModifyUserPropertyByAccountName(UserName, data);
            }
            catch (Exception ex)
            {
                LogMessage("Exception trying to update profile property " + PropertyName + " for user " + UserName + "\n" + ex.Message, LogLevel.Error);
            }

        }

```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Решения пользовательского профиля для SharePoint 2013 и SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [UserProfile.Manipulation.CSOM.Console](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
