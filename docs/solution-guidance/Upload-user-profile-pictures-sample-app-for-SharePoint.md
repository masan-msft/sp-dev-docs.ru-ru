---
title: "Отправка пользовательского профиля изображения пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 0897ded60ef98f019450e73860685d014afc7834
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="upload-user-profile-pictures-sample-add-in-for-sharepoint"></a>Отправка пользовательского профиля изображения пример надстройки для SharePoint

Размещение у поставщика надстройки с можно использовать для выполнения массовая отправка данных профилей пользователей из общей папки или URL-адрес SharePoint Online.
    
_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_
    
Пример надстройки [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) показано, как выполнить массовая отправка данных профилей пользователей из общей папки или URL-адрес SharePoint Online и как связать свойств профилей пользователей для отправки изображений.
    
Используйте этот пример, чтобы узнать, как:

- Перенос фотографий профиля пользователя из SharePoint Server 2013 в локальной в SharePoint Online.
    
- Устранение неполадок, возникающих при сбое средства синхронизации Azure Active Directory (dirsync) для синхронизации фотографий профиля пользователя в SharePoint Online.
    
- Замените плохого качества изображения профилей пользователей в SharePoint Online.
    
В этом примере используются консольного приложения для выполнения следующих:

- Чтение имена пользователей и пути к файлам изображений или URL-адреса из файла сопоставления пользователей.
    
- Получение и отправка одного или трех изображений в библиотеку рисунков на узле личных сайтов. 
    
- Установка свойств профилей пользователей для связывания загруженному изображений профиля пользователя.
    
- Обновление свойств профиля пользователя дополнительных (не обязательно).
    
## <a name="before-you-begin"></a>Перед началом работы
<a name="sectionSection0"> </a>

Чтобы начать работу, загрузите пример надстройки [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Прежде чем запускать этот пример кода:

- Хранить рисунки пользователей, которые требуется отправить в SharePoint Online на общий доступ или веб-сервере. 
    
- Редактирование файла userlist.csv, относятся следующие:
    
    - Заголовок строки, содержащей значение **UserPrincipalName** **SourceURL**.
    
    - Для каждого пользователя добавить новую строку, содержащую организационной учетной записи пользователя (или имя участника-пользователя) и путь к файлу или URL-адрес изображения для загрузки. 
    
- Для выполнения этого примера из Visual Studio, настройте **Core.ProfilePictureUploader** проекта с помощью следующей командной строки:`-SPOAdmin Username -SPOAdminPassword Password -Configuration filepath`
    
  Где:
    
    - *Имя пользователя* — это имя пользователя администратором Office 365.
    
    - *Пароль* — пароль администратора Office 365.
    
    - *FilePath* — это путь к файлу из файла configuration.xml.
    
- Чтобы задать аргументы командной строки для проекта Core.ProfilePictureUploader:
    
    - В обозревателе решений откройте контекстное меню (правой кнопкой мыши) для **Core.ProfilePictureUploader** project > **Свойства**.
    
    - Выберите команду **Отладка**.
    
    - В поле **аргументы командной строки**введите аргументы командной строки, перечисленных выше.
    
- Чтобы настроить процесс отправки в соответствии с требованиями, измените файл configuration.xml, введя следующие значения:
    
    - Имя клиента Office 365 в элементе **tenantName** . Например:`<tenantName>contoso.onmicrosoft.com</tenantName>`
    
    - Путь к файлу сопоставления пользователей в элементе **pictureSourceCsv** . Например:`<pictureSourceCsv>C:\temp\userlist.csv</pictureSourceCsv>`
    
    - С помощью элемента **палец** инструкции по Отправка изображения. Измените следующие атрибуты в элементе палец:
    
        -  **aupload3Thumbs** - присвоено **значение true,** Если вы хотите отправить три изображения для каждого пользователя, или значение **false** , если вы хотите отправить одно изображение.
    
        -  **createSMLThumbs** - параметр имеет значение **true,** Если вы хотите создать три различных размера изображения (малых, средних и крупных) из исходного изображения или параметр имеет значение **false,** Если вы хотите отправить три изображения по размеру.
    
    - Дополнительные свойства установка в профиле пользователя, с помощью элемента **additionalProfilePropties** . К примеру следующий XML-код указывает дополнительные свойство профиля называется **SPS-PictureExchangeSyncState** , который необходимо задать нулевое значение в профиле пользователя при запуске образца кода.

    ```
    <additionalProfileProperties>
         <property name="SPS-PictureExchangeSyncState" value="0"/>
    </additionalProfileProperties>
    ```

  - Путь к файлу журнала в элементе **файла журнала** , как показано в следующем примере. `<logFile path="C:\temp\log.txt" enableLogging="true" loggingLevel="verbose" />`
    
  - Задержка передачи в миллисекундах между отправляемых файлов другое изображение с помощью элемента **uploadDelay** . Рекомендуемое значение **uploadDelay** — 500 мс.
    
- В файле App.config измените **значение** элемента параметр **ProfilePictureUploader_UPSvc_UserProfileService** , чтобы получить справку службы профилей пользователей в центре администрирования SharePoint Online. как показано в следующем примере.

```XML  
<Contoso.Core.ProfilePictureUploader.Properties.Settings>
      <setting name="ProfilePictureUploader_UPSvc_UserProfileService"
            serializeAs="String">
            <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
      </setting>
 </Contoso.Core.ProfilePictureUploader.Properties.Settings>
```

**Важные**  Подключение к веб-службы userprofileservice.asmx в центре администрирования SharePoint Online позволяет обновлять свойства профиля пользователя по другим пользователям. При выполнении этого примера кода, используйте учетную запись администратора Office 365, имеющая разрешения на управление профилями пользователей. 

## <a name="using-the-coreprofilepictureuploader-app"></a>С помощью приложения Core.ProfilePictureUploader
<a name="sectionSection1"> </a>

В этом примере кода используется в качестве консольного приложения. При запуске образца кода, метод **Main** в файле Program.cs выполняет следующее.

- Инициализирует консольное приложение, с помощью **SetupArguments** и **InitializeConfiguration**. 
    
- Вызывает **InitializeWebService** для подключения к службе профилей пользователей в SharePoint Online.
    
- Итерация по userlist.csv файл, чтобы прочитать имя участника-пользователя (UPN) для пользователя и расположение файла изображения пользователя. 
    
- Извлекает изображение пользователя, с помощью объектов **WebRequest** и **WebResponse** в **GetImagefromHTTPUrl**.
    
- Вызывает **UploadImageToSpo** Отправка изображения пользователя в SharePoint Online.
    
- Вызывает **SetMultipleProfileProperties** в качестве пользователя **PictureURL** и **SPS-PicturePlaceholderState** свойств профиля пользователя.
    
- Вызывает **SetAdditionalProfileProperties** для установки дополнительных свойств в профиле пользователя после отправки файла изображения.

**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
static void Main(string[] args)
        {
            int count = 0;

            if (SetupArguments(args)) // Checks if args passed are valid 
            {

                if (InitializeConfiguration()) // Check that the configuration file is valid
                {
                    if (InitializeWebService()) // Initialize the web service end point for the SharePoint Online user profile service.
                    {
                        
                        using (StreamReader readFile = new StreamReader(_appConfig.PictureSourceCsv))
                        {
                            string line;
                            string[] row;
                            string sPoUserProfileName;
                            string sourcePictureUrl;

                            while ((line = readFile.ReadLine()) != null)
                            {
                                if (count > 0)
                                {
                                    row = line.Split(',');
                                    sPoUserProfileName = row[0]; 
                                    sourcePictureUrl = row[1]; 

                                    LogMessage("Begin processing for user " + sPoUserProfileName, LogLevel.Warning);

                                    // Get source picture from source image path.
                                    using (MemoryStream picturefromExchange = GetImagefromHTTPUrl(sourcePictureUrl))
                                    {
                                        if (picturefromExchange != null) // if we got image, upload to SharePoint Online
                                        {
                                            // Create SharePoint naming convention for image file.
                                            string newImageNamePrefix = sPoUserProfileName.Replace("@", "_").Replace(".", "_");
                                            // Upload source image to SharePoint Online.
                                            string spoImageUrl = UploadImageToSpo(newImageNamePrefix, picturefromExchange);
                                            if (spoImageUrl.Length > 0)// If upload worked.
                                            {
                                                string[] profilePropertyNamesToSet = new string[] { "PictureURL", "SPS-PicturePlaceholderState" };
                                                string[] profilePropertyValuesToSet = new string[] { spoImageUrl, "0" };
                                                // Set these two required user profile properties - path to uploaded image, and pictureplaceholder state.
                                                SetMultipleProfileProperties(_sPOProfilePrefix + sPoUserProfileName, profilePropertyNamesToSet, profilePropertyValuesToSet);
                                                // Set additional user profile properties based on your requirements.
                                                SetAdditionalProfileProperties(_sPOProfilePrefix + sPoUserProfileName);
                                            }
                                        }
                                    }

                                    LogMessage("End processing for user " + sPoUserProfileName, LogLevel.Warning);

                                    int sleepTime = _appConfig.UploadDelay;
                                    System.Threading.Thread.Sleep(sleepTime); // A pause between uploads is recommended. 
                                }
                                count++;
                            }
                        }
                    }
                }
            }


            LogMessage("Processing finished for " + count + " user profiles", LogLevel.Information);
         } 

```

**InitializeWebService** подключается к SharePoint Online и задает ссылку службы профилей пользователей для переменной экземпляра. Другие методы в этом примере кода используйте этот экземпляр переменной установки обновлений для свойств профиля пользователя. Для администрирования профилей пользователей, в этом образце кода используется userprofileservice.asmx веб-службы в центре администрирования SharePoint Online.

```
static bool InitializeWebService()
        {
            try
            {
                string webServiceExt = "_vti_bin/userprofileservice.asmx";
                string adminWebServiceUrl = string.Empty;

                // Append the web service (ASMX) URL onto the admin website URL.
                if (_profileSiteUrl.EndsWith("/"))
                    adminWebServiceUrl = _profileSiteUrl + webServiceExt;
                else
                    adminWebServiceUrl = _profileSiteUrl + "/" + webServiceExt;

                LogMessage("Initializing SPO web service " + adminWebServiceUrl, LogLevel.Information);

                // Get secure password from clear text password.
                SecureString securePassword = GetSecurePassword(_sPoAuthPasword);

                // Set credentials from SharePoint Client API, used later to extract authentication cookie, so can replay to web services.
                SharePointOnlineCredentials onlineCred = new SharePointOnlineCredentials(_sPoAuthUserName, securePassword);

                // Get the authentication cookie by passing the URL of the admin website. 
                string authCookie = onlineCred.GetAuthenticationCookie(new Uri(_profileSiteUrl));

                // Create a CookieContainer to authenticate against the web service. 
                CookieContainer authContainer = new CookieContainer();

                // Put the authenticationCookie string in the container. 
                authContainer.SetCookies(new Uri(_profileSiteUrl), authCookie);

                // Setting up the user profile web service. 
                _userProfileService = new UPSvc.UserProfileService();

                // Assign the correct URL to the admin profile web service. 
                _userProfileService.Url = adminWebServiceUrl;

                // Assign previously created authentication container to admin profile web service. 
                _userProfileService.CookieContainer = authContainer;
               // LogMessage("Finished creating service object for SharePoint Online Web Service " + adminWebServiceUrl, LogLevel.Information);
                return true;
            }
            catch (Exception ex)
            {
                LogMessage("Error initiating connection to profile web service in SPO " + ex.Message, LogLevel.Error);
                return false;

            }

            
        }

```

Метод **Main** в файле Program.cs вызывает **UploadImageToSpo** Отправка изображение профиля пользователя в SharePoint Online. Изображения профилей всех пользователей, хранятся в библиотеке рисунков на узле личных сайтов. **UploadImageToSpo** выполняет следующие задачи:

- Подключается к SharePoint Online.
    
- Определяет число изображения для загрузки для каждого пользователя. 
    
    - Если вы настроили приложение для загрузки одно изображение на одного пользователя, изображение передается в библиотеку рисунков. 
    
    - Если вы настроили приложение для загрузки три изображения на одного пользователя, приложение проверяет значение **createSMLThumbs** в файле конфигурации, чтобы определить, требуются ли три разных размера изображения. Если требуются три разных размера изображения, приложение использует **ResizeImageSmall** и **ResizeImageLarge** для создания три разных размера изображения из исходного изображения. Затем приложение загружает размер изображения в библиотеке рисунков. Если не требуются три разных размера изображения, приложение отправляет три изображения по размеру в библиотеку рисунков.

```C#
static string UploadImageToSpo(string PictureName, Stream ProfilePicture)
        {
            try
            {

                string spPhotoPathTempate = "/User Photos/Profile Pictures/{0}_{1}Thumb.jpg"; // Path template to picture library on the My Site Host.
                string spImageUrl = string.Empty;

                // Create SharePoint Online Client context to My Site Host.
                ClientContext mySiteclientContext = new ClientContext(_mySiteUrl);
                SecureString securePassword = GetSecurePassword(_sPoAuthPasword);
                // Provide authentication credentials using Office 365 authentication.
                mySiteclientContext.Credentials = new SharePointOnlineCredentials(_sPoAuthUserName, securePassword);
                                
                if (!_appConfig.Thumbs.Upload3Thumbs) // Upload a single input image only to picture library, no resizing necessary.
                {
                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "M");
                    LogMessage("Uploading single image, no resize, to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);
                }
                else if (_appConfig.Thumbs.Upload3Thumbs &amp;&amp; !_appConfig.Thumbs.CreateSMLThumbs)// Upload three images of the same size. 
                {
                    // The following code is not optimal. Upload the same source image three times with different names.
                    // No resizing of images necessary.
                    LogMessage("Uploading threes image to SPO, no resize", LogLevel.Information);

                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "M");
                    LogMessage("Uploading medium image to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);

                    ProfilePicture.Seek(0, SeekOrigin.Begin);
                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "L");
                    LogMessage("Uploading large image to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);
                    
                    ProfilePicture.Seek(0, SeekOrigin.Begin);
                    spImageUrl = string.Format(spPhotoPathTempate, PictureName, "S");
                    LogMessage("Uploading small image to " + spImageUrl, LogLevel.Information);
                    Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, ProfilePicture, true);

                    
                }
                else if (_appConfig.Thumbs.Upload3Thumbs &amp;&amp; _appConfig.Thumbs.CreateSMLThumbs) //generate 3 different sized images
                {
                    LogMessage("Uploading threes image to SPO, with resizing", LogLevel.Information);
                    // Create three images based on recommended sizes for SharePoint Online.
                    // Create small-sized image.
                    using (Stream smallThumb = ResizeImageSmall(ProfilePicture, _smallThumbWidth))
                    {
                        if (smallThumb != null)
                        {
                            spImageUrl = string.Format(spPhotoPathTempate, PictureName, "S");
                            LogMessage("Uploading small image to " + spImageUrl, LogLevel.Information);
                            Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, smallThumb, true);                            
                        }
                    }

                    // Create medium-sized image.
                    using (Stream mediumThumb = ResizeImageSmall(ProfilePicture, _mediumThumbWidth))
                    {
                        if (mediumThumb != null)
                        {
                            spImageUrl = string.Format(spPhotoPathTempate, PictureName, "M");
                            LogMessage("Uploading medium image to " + spImageUrl, LogLevel.Information);
                            Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, mediumThumb, true);
                           
                        }
                    }

                    // Create large-sized image. This image is shown when you open the user's OneDrive for Business. 
                    using (Stream largeThumb = ResizeImageLarge(ProfilePicture, _largeThumbWidth))
                    {
                        if (largeThumb != null)
                        {

                            spImageUrl = string.Format(spPhotoPathTempate, PictureName, "L");
                            LogMessage("Uploading large image to " + spImageUrl, LogLevel.Information);
                            Microsoft.SharePoint.Client.File.SaveBinaryDirect(mySiteclientContext, spImageUrl, largeThumb, true);
                            
                        }
                    }
                  
                   
                }
                // Return URL of the medium-sized image to set properties on the user profile.
                return _mySiteUrl + string.Format(spPhotoPathTempate, PictureName, "M");                
                
            }
            catch (Exception ex)
            {
                LogMessage("User Error: Failed to upload thumbnail picture to SPO for " + PictureName + " " + ex.Message, LogLevel.Error);
                return string.Empty;
            }

        }

```

**SetMultipleProfileProperties** задает свойства профиля несколько пользователей в одном методе. В этом примере кода **SetMultipleProfileProperties** задает следующие свойства профиля пользователя для пользователя:

-  **PictureURL** - значение URL-адрес среднего размера загружаемого изображения в библиотеке рисунков на узле личных сайтов.
    
-  **SPS PicturePlaceholderState** - нулевое значение для указания, что SharePoint Online следует показывать изображение загруженному для пользователя.

```C#
static void SetMultipleProfileProperties(string UserName, string[] PropertyName, string[] PropertyValue)
        {

            LogMessage("Setting multiple SPO user profile properties for " + UserName, LogLevel.Information);

            try
            {
                int arrayCount = PropertyName.Count();

                UPSvc.PropertyData[] data = new UPSvc.PropertyData[arrayCount];
                for (int x = 0; x < arrayCount; x++)
                {
                    data[x] = new UPSvc.PropertyData();
                    data[x].Name = PropertyName[x];
                    data[x].IsValueChanged = true;
                    data[x].Values = new UPSvc.ValueData[1];
                    data[x].Values[0] = new UPSvc.ValueData();
                    data[x].Values[0].Value = PropertyValue[x];
                }

                _userProfileService.ModifyUserPropertyByAccountName(UserName, data);
                // LogMessage("Finished setting multiple SharePoint Online user profile properties for " + UserName, LogLevel.Information);

            }
            catch (Exception ex)
            {
                LogMessage("User Error: Exception trying to update profile properties for user " + UserName + "\n" + ex.Message, LogLevel.Error);
            }
        }

```

**SetAdditionalProfileProperties** задает любые дополнительные пользовательские свойства профилей, которые необходимо обновить после отправки файлы изображений. Можно указать дополнительные свойства для обновления в файле configuration.xml.

```C#
static void SetAdditionalProfileProperties(string UserName)
        {
            if (_appConfig.AdditionalProfileProperties.Properties == null) // If there are no additional properties to update. 
                return;

            int propsCount = _appConfig.AdditionalProfileProperties.Properties.Count();
            if (propsCount > 0)
            {
                string[] profilePropertyNamesToSet = new string[propsCount];
                string[] profilePropertyValuesToSet = new string[propsCount];
                // Loop through each property in configuration file.
                for (int i = 0; i < propsCount; i++)
                {
                    profilePropertyNamesToSet[i] = _appConfig.AdditionalProfileProperties.Properties[i].Name;
                    profilePropertyValuesToSet[i] = _appConfig.AdditionalProfileProperties.Properties[i].Value;
                }

                // Set all properties in a single call.
                SetMultipleProfileProperties(UserName, profilePropertyNamesToSet, profilePropertyValuesToSet);

            }
        }

```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Решения пользовательского профиля для SharePoint 2013 и SharePoint Online](user-profile-solutions-for-sharepoint.md)
    
-  [Core.ProfilePictureUploader приложения](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [UserProfile.Manipulation.CSOM](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
    
-  [UserProfile.Manipulation.CSOM.Console](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
