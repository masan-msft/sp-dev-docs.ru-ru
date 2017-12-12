---
title: "Отправка пользовательского профиля изображения пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: ac6787f528d3f611d9eaecb415e8f48d7b392f53
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upload-user-profile-pictures-sample-add-in-for-sharepoint"></a><span data-ttu-id="e01f0-102">Отправка пользовательского профиля изображения пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="e01f0-102">Upload user profile pictures sample add-in for SharePoint</span></span>

<span data-ttu-id="e01f0-103">Размещение у поставщика надстройки с можно использовать для выполнения массовая отправка данных профилей пользователей из общей папки или URL-адрес SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-103">You can use a provider-hosted add-in to do a bulk upload of user profile data from either a file share or SharePoint Online URL.</span></span>
    
<span data-ttu-id="e01f0-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="e01f0-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="e01f0-105">Пример надстройки [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) показано, как выполнить массовая отправка данных профилей пользователей из общей папки или URL-адрес SharePoint Online и как связать свойств профилей пользователей для отправки изображений.</span><span class="sxs-lookup"><span data-stu-id="e01f0-105">The [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) sample add-in shows how to do a bulk upload of user profile data from either a file share or SharePoint Online URL, and how to link user profile properties to uploaded images.</span></span>
    
<span data-ttu-id="e01f0-106">Используйте этот пример, чтобы узнать, как:</span><span class="sxs-lookup"><span data-stu-id="e01f0-106">Use this sample to learn how to:</span></span>

- <span data-ttu-id="e01f0-107">Перенос фотографий профиля пользователя из SharePoint Server 2013 в локальной в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-107">Migrate a user's profile pictures from SharePoint Server 2013 on-premises to SharePoint Online.</span></span>
    
- <span data-ttu-id="e01f0-108">Устранение неполадок, возникающих при сбое средства синхронизации Azure Active Directory (dirsync) для синхронизации фотографий профиля пользователя в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-108">Fix issues that occur when the Azure Active Directory Sync tool (dirsync) fails to synchronize user's profile pictures to SharePoint Online.</span></span>
    
- <span data-ttu-id="e01f0-109">Замените плохого качества изображения профилей пользователей в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-109">Replace poor quality user profile pictures in SharePoint Online.</span></span>
    
<span data-ttu-id="e01f0-110">В этом примере используются консольного приложения для выполнения следующих:</span><span class="sxs-lookup"><span data-stu-id="e01f0-110">This sample uses a console application to do the following:</span></span>

- <span data-ttu-id="e01f0-111">Чтение имена пользователей и пути к файлам изображений или URL-адреса из файла сопоставления пользователей.</span><span class="sxs-lookup"><span data-stu-id="e01f0-111">Read the user names and image file paths or URLs from a user mapping file.</span></span>
    
- <span data-ttu-id="e01f0-112">Получение и отправка одного или трех изображений в библиотеку рисунков на узле личных сайтов.</span><span class="sxs-lookup"><span data-stu-id="e01f0-112">Fetch and upload one or three images to a picture library on the My Site host.</span></span> 
    
- <span data-ttu-id="e01f0-113">Установка свойств профилей пользователей для связывания загруженному изображений профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="e01f0-113">Set user profile properties to link the uploaded images to a user's profile.</span></span>
    
- <span data-ttu-id="e01f0-114">Обновление свойств профиля пользователя дополнительных (не обязательно).</span><span class="sxs-lookup"><span data-stu-id="e01f0-114">Update additional (optional) user profile properties.</span></span>
    
## <a name="before-you-begin"></a><span data-ttu-id="e01f0-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e01f0-115">Before you begin</span></span>
<span data-ttu-id="e01f0-116"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="e01f0-116"></span></span>

<span data-ttu-id="e01f0-117">Чтобы начать работу, загрузите пример надстройки [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="e01f0-117">To get started, download the  [Core.ProfilePictureUploader](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="e01f0-118">Прежде чем запускать этот пример кода:</span><span class="sxs-lookup"><span data-stu-id="e01f0-118">Before you run this code sample:</span></span>

- <span data-ttu-id="e01f0-119">Хранить рисунки пользователей, которые требуется отправить в SharePoint Online на общий доступ или веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="e01f0-119">Store your user images that you intend to upload to SharePoint Online on a file share or web server.</span></span> 
    
- <span data-ttu-id="e01f0-120">Редактирование файла userlist.csv, относятся следующие:</span><span class="sxs-lookup"><span data-stu-id="e01f0-120">Edit the userlist.csv file to include the following:</span></span>
    
    - <span data-ttu-id="e01f0-121">Заголовок строки, содержащей значение **UserPrincipalName** **SourceURL**.</span><span class="sxs-lookup"><span data-stu-id="e01f0-121">A header row containing the value  **UserPrincipalName**,  **SourceURL**.</span></span>
    
    - <span data-ttu-id="e01f0-122">Для каждого пользователя добавить новую строку, содержащую организационной учетной записи пользователя (или имя участника-пользователя) и путь к файлу или URL-адрес изображения для загрузки.</span><span class="sxs-lookup"><span data-stu-id="e01f0-122">For each user, add a new row containing the user's organizational account (or user principal name) and the file path or URL of the image to upload.</span></span> 
    
- <span data-ttu-id="e01f0-123">Для выполнения этого примера из Visual Studio, настройте **Core.ProfilePictureUploader** проекта с помощью следующей командной строки:`-SPOAdmin Username -SPOAdminPassword Password -Configuration filepath`</span><span class="sxs-lookup"><span data-stu-id="e01f0-123">To run this sample from Visual Studio, configure the  **Core.ProfilePictureUploader** project with the following command-line arguments: `-SPOAdmin Username -SPOAdminPassword Password -Configuration filepath`</span></span>
    
  <span data-ttu-id="e01f0-124">Где:</span><span class="sxs-lookup"><span data-stu-id="e01f0-124">Where:</span></span>
    
    - <span data-ttu-id="e01f0-125">*Имя пользователя* — это имя пользователя администратором Office 365.</span><span class="sxs-lookup"><span data-stu-id="e01f0-125">*Username* is your Office 365 administrator's username.</span></span>
    
    - <span data-ttu-id="e01f0-126">*Пароль* — пароль администратора Office 365.</span><span class="sxs-lookup"><span data-stu-id="e01f0-126">*Password* is your Office 365 administrator's password.</span></span>
    
    - <span data-ttu-id="e01f0-127">*FilePath* — это путь к файлу из файла configuration.xml.</span><span class="sxs-lookup"><span data-stu-id="e01f0-127">*Filepath* is the file path of the configuration.xml file.</span></span>
    
- <span data-ttu-id="e01f0-128">Чтобы задать аргументы командной строки для проекта Core.ProfilePictureUploader:</span><span class="sxs-lookup"><span data-stu-id="e01f0-128">To set the command-line arguments on the Core.ProfilePictureUploader project:</span></span>
    
    - <span data-ttu-id="e01f0-129">В обозревателе решений откройте контекстное меню (правой кнопкой мыши) для **Core.ProfilePictureUploader** project > **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e01f0-129">In Solution Explorer, open the shortcut menu (right click) for the  **Core.ProfilePictureUploader** project > **Properties**.</span></span>
    
    - <span data-ttu-id="e01f0-130">Выберите команду **Отладка**.</span><span class="sxs-lookup"><span data-stu-id="e01f0-130">Choose  **Debug**.</span></span>
    
    - <span data-ttu-id="e01f0-131">В поле **аргументы командной строки**введите аргументы командной строки, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="e01f0-131">In  **Command line arguments**, enter the command-line arguments listed earlier.</span></span>
    
- <span data-ttu-id="e01f0-132">Чтобы настроить процесс отправки в соответствии с требованиями, измените файл configuration.xml, введя следующие значения:</span><span class="sxs-lookup"><span data-stu-id="e01f0-132">To configure the upload process to meet your requirements, edit the configuration.xml file by entering the following values:</span></span>
    
    - <span data-ttu-id="e01f0-133">Имя клиента Office 365 в элементе **tenantName** .</span><span class="sxs-lookup"><span data-stu-id="e01f0-133">The name of your Office 365 tenant in the  **tenantName** element.</span></span> <span data-ttu-id="e01f0-134">Например:`<tenantName>contoso.onmicrosoft.com</tenantName>`</span><span class="sxs-lookup"><span data-stu-id="e01f0-134">For example: `<tenantName>contoso.onmicrosoft.com</tenantName>`</span></span>
    
    - <span data-ttu-id="e01f0-135">Путь к файлу сопоставления пользователей в элементе **pictureSourceCsv** .</span><span class="sxs-lookup"><span data-stu-id="e01f0-135">The user mapping file path in the  **pictureSourceCsv** element.</span></span> <span data-ttu-id="e01f0-136">Например:`<pictureSourceCsv>C:\temp\userlist.csv</pictureSourceCsv>`</span><span class="sxs-lookup"><span data-stu-id="e01f0-136">For example: `<pictureSourceCsv>C:\temp\userlist.csv</pictureSourceCsv>`</span></span>
    
    - <span data-ttu-id="e01f0-137">С помощью элемента **палец** инструкции по Отправка изображения.</span><span class="sxs-lookup"><span data-stu-id="e01f0-137">Image upload instructions using the  **thumbs** element.</span></span> <span data-ttu-id="e01f0-138">Измените следующие атрибуты в элементе палец:</span><span class="sxs-lookup"><span data-stu-id="e01f0-138">Edit the following attributes in the thumbs element:</span></span>
    
        -  <span data-ttu-id="e01f0-139">**aupload3Thumbs** - присвоено **значение true,** Если вы хотите отправить три изображения для каждого пользователя, или значение **false** , если вы хотите отправить одно изображение.</span><span class="sxs-lookup"><span data-stu-id="e01f0-139">**aupload3Thumbs** - Set to **true** if you want to upload three images for each user, or set to **false** if you only want to upload one image.</span></span>
    
        -  <span data-ttu-id="e01f0-140">**createSMLThumbs** - параметр имеет значение **true,** Если вы хотите создать три различных размера изображения (малых, средних и крупных) из исходного изображения или параметр имеет значение **false,** Если вы хотите отправить три изображения по размеру.</span><span class="sxs-lookup"><span data-stu-id="e01f0-140">**createSMLThumbs** - Set to **true** if you want to create three different sized images (small, medium, and large) of the source image, or set to **false** if you want to upload three images of the same size.</span></span>
    
    - <span data-ttu-id="e01f0-141">Дополнительные свойства установка в профиле пользователя, с помощью элемента **additionalProfilePropties** .</span><span class="sxs-lookup"><span data-stu-id="e01f0-141">Additional properties to set on the user's profile using the  **additionalProfilePropties** element.</span></span> <span data-ttu-id="e01f0-142">К примеру следующий XML-код указывает дополнительные свойство профиля называется **SPS-PictureExchangeSyncState** , который необходимо задать нулевое значение в профиле пользователя при запуске образца кода.</span><span class="sxs-lookup"><span data-stu-id="e01f0-142">For example, the following XML specifies an additional user profile property called **SPS-PictureExchangeSyncState** that should be set to zero on the user's profile when the code sample runs.</span></span>

    ```
    <additionalProfileProperties>
         <property name="SPS-PictureExchangeSyncState" value="0"/>
    </additionalProfileProperties>
    ```

  - <span data-ttu-id="e01f0-143">Путь к файлу журнала в элементе **файла журнала** , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="e01f0-143">The log file path in the  **logfile** element, as shown in the following example.</span></span> `<logFile path="C:\temp\log.txt" enableLogging="true" loggingLevel="verbose" />`
    
  - <span data-ttu-id="e01f0-144">Задержка передачи в миллисекундах между отправляемых файлов другое изображение с помощью элемента **uploadDelay** .</span><span class="sxs-lookup"><span data-stu-id="e01f0-144">The upload delay in milliseconds between the upload of different image files using the  **uploadDelay** element.</span></span> <span data-ttu-id="e01f0-145">Рекомендуемое значение **uploadDelay** — 500 мс.</span><span class="sxs-lookup"><span data-stu-id="e01f0-145">The recommended setting for **uploadDelay** is 500 milliseconds.</span></span>
    
- <span data-ttu-id="e01f0-146">В файле App.config измените **значение** элемента параметр **ProfilePictureUploader_UPSvc_UserProfileService** , чтобы получить справку службы профилей пользователей в центре администрирования SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-146">In the App.config file, change the  **value** element of the **ProfilePictureUploader_UPSvc_UserProfileService** setting to include a reference to the user profile service in your SharePoint Online admin center.</span></span> <span data-ttu-id="e01f0-147">как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="e01f0-147">as shown in the following example.</span></span>

```XML  
<Contoso.Core.ProfilePictureUploader.Properties.Settings>
      <setting name="ProfilePictureUploader_UPSvc_UserProfileService"
            serializeAs="String">
            <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
      </setting>
 </Contoso.Core.ProfilePictureUploader.Properties.Settings>
```

<span data-ttu-id="e01f0-148">**Важные**  Подключение к веб-службы userprofileservice.asmx в центре администрирования SharePoint Online позволяет обновлять свойства профиля пользователя по другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="e01f0-148">**Important**  Connecting to the userprofileservice.asmx web service on the SharePoint Online admin center allows you to update the user profile properties of other users.</span></span> <span data-ttu-id="e01f0-149">При выполнении этого примера кода, используйте учетную запись администратора Office 365, имеющая разрешения на управление профилями пользователей.</span><span class="sxs-lookup"><span data-stu-id="e01f0-149">When you run this code sample, use an Office 365 administrator account that has permissions to manage user profiles.</span></span> 

## <a name="using-the-coreprofilepictureuploader-app"></a><span data-ttu-id="e01f0-150">С помощью приложения Core.ProfilePictureUploader</span><span class="sxs-lookup"><span data-stu-id="e01f0-150">Using the Core.ProfilePictureUploader app</span></span>
<span data-ttu-id="e01f0-151"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="e01f0-151"></span></span>

<span data-ttu-id="e01f0-152">В этом примере кода используется в качестве консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="e01f0-152">This code sample runs as a console application.</span></span> <span data-ttu-id="e01f0-153">При запуске образца кода, метод **Main** в файле Program.cs выполняет следующее.</span><span class="sxs-lookup"><span data-stu-id="e01f0-153">When the code sample runs, the  **Main** method in Program.cs does the following:</span></span>

- <span data-ttu-id="e01f0-154">Инициализирует консольное приложение, с помощью **SetupArguments** и **InitializeConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="e01f0-154">Initializes the console application using  **SetupArguments** and **InitializeConfiguration**.</span></span> 
    
- <span data-ttu-id="e01f0-155">Вызывает **InitializeWebService** для подключения к службе профилей пользователей в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-155">Calls  **InitializeWebService** to connect to the user profile service in SharePoint Online.</span></span>
    
- <span data-ttu-id="e01f0-156">Итерация по userlist.csv файл, чтобы прочитать имя участника-пользователя (UPN) для пользователя и расположение файла изображения пользователя.</span><span class="sxs-lookup"><span data-stu-id="e01f0-156">Iterates through the userlist.csv file to read the user principal name (UPN) for the user and the location of the user's image file.</span></span> 
    
- <span data-ttu-id="e01f0-157">Извлекает изображение пользователя, с помощью объектов **WebRequest** и **WebResponse** в **GetImagefromHTTPUrl**.</span><span class="sxs-lookup"><span data-stu-id="e01f0-157">Fetches a user's image using  **WebRequest** and **WebResponse** objects in **GetImagefromHTTPUrl**.</span></span>
    
- <span data-ttu-id="e01f0-158">Вызывает **UploadImageToSpo** Отправка изображения пользователя в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-158">Calls  **UploadImageToSpo** to upload the user's image to SharePoint Online.</span></span>
    
- <span data-ttu-id="e01f0-159">Вызывает **SetMultipleProfileProperties** в качестве пользователя **PictureURL** и **SPS-PicturePlaceholderState** свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="e01f0-159">Calls  **SetMultipleProfileProperties** to set the **PictureURL** and **SPS-PicturePlaceholderState** user profile properties for the user.</span></span>
    
- <span data-ttu-id="e01f0-160">Вызывает **SetAdditionalProfileProperties** для установки дополнительных свойств в профиле пользователя после отправки файла изображения.</span><span class="sxs-lookup"><span data-stu-id="e01f0-160">Calls  **SetAdditionalProfileProperties** to set additional properties on the user profile after the image file is uploaded.</span></span>

> [!NOTE] 
> <span data-ttu-id="e01f0-161">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="e01f0-161">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="e01f0-162">**InitializeWebService** подключается к SharePoint Online и задает ссылку службы профилей пользователей для переменной экземпляра.</span><span class="sxs-lookup"><span data-stu-id="e01f0-162">**InitializeWebService** connects to SharePoint Online, and sets a reference of the user profile service to an instance variable.</span></span> <span data-ttu-id="e01f0-163">Другие методы в этом примере кода используйте этот экземпляр переменной установки обновлений для свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="e01f0-163">Other methods in this code sample use this instance variable to apply updates to user profile properties.</span></span> <span data-ttu-id="e01f0-164">Для администрирования профилей пользователей, в этом образце кода используется userprofileservice.asmx веб-службы в центре администрирования SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-164">To administer the user profile, this code sample uses the userprofileservice.asmx web service in the SharePoint Online admin center.</span></span>

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

<span data-ttu-id="e01f0-165">Метод **Main** в файле Program.cs вызывает **UploadImageToSpo** Отправка изображение профиля пользователя в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-165">The  **Main** method in Program.cs calls **UploadImageToSpo** to upload the user's profile picture to SharePoint Online.</span></span> <span data-ttu-id="e01f0-166">Изображения профилей всех пользователей, хранятся в библиотеке рисунков на узле личных сайтов.</span><span class="sxs-lookup"><span data-stu-id="e01f0-166">All users' profile pictures are stored in a picture library on the My Site Host.</span></span> <span data-ttu-id="e01f0-167">**UploadImageToSpo** выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e01f0-167">**UploadImageToSpo** performs the following tasks:</span></span>

- <span data-ttu-id="e01f0-168">Подключается к SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="e01f0-168">Connects to SharePoint Online.</span></span>
    
- <span data-ttu-id="e01f0-169">Определяет число изображения для загрузки для каждого пользователя.</span><span class="sxs-lookup"><span data-stu-id="e01f0-169">Determines the number of images to upload for each user.</span></span> 
    
    - <span data-ttu-id="e01f0-170">Если вы настроили приложение для загрузки одно изображение на одного пользователя, изображение передается в библиотеку рисунков.</span><span class="sxs-lookup"><span data-stu-id="e01f0-170">If you configured the application to upload one image per user, the image is uploaded to the picture library.</span></span> 
    
    - <span data-ttu-id="e01f0-171">Если вы настроили приложение для загрузки три изображения на одного пользователя, приложение проверяет значение **createSMLThumbs** в файле конфигурации, чтобы определить, требуются ли три разных размера изображения.</span><span class="sxs-lookup"><span data-stu-id="e01f0-171">If you configured the application to upload three images per user, the application checks the value of  **createSMLThumbs** in the configuration file to determine whether three different sized images are required.</span></span> <span data-ttu-id="e01f0-172">Если требуются три разных размера изображения, приложение использует **ResizeImageSmall** и **ResizeImageLarge** для создания три разных размера изображения из исходного изображения.</span><span class="sxs-lookup"><span data-stu-id="e01f0-172">If three different sized images are required, the application uses **ResizeImageSmall** and **ResizeImageLarge** to create three different sized images from the source image.</span></span> <span data-ttu-id="e01f0-173">Затем приложение загружает размер изображения в библиотеке рисунков.</span><span class="sxs-lookup"><span data-stu-id="e01f0-173">The application then uploads the resized images to the picture library.</span></span> <span data-ttu-id="e01f0-174">Если не требуются три разных размера изображения, приложение отправляет три изображения по размеру в библиотеку рисунков.</span><span class="sxs-lookup"><span data-stu-id="e01f0-174">If three different sized images are not required, the application uploads three images of the same size to the picture library.</span></span>

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

<span data-ttu-id="e01f0-175">**SetMultipleProfileProperties** задает свойства профиля несколько пользователей в одном методе.</span><span class="sxs-lookup"><span data-stu-id="e01f0-175">**SetMultipleProfileProperties** sets multiple user profile properties in a single method call.</span></span> <span data-ttu-id="e01f0-176">В этом примере кода **SetMultipleProfileProperties** задает следующие свойства профиля пользователя для пользователя:</span><span class="sxs-lookup"><span data-stu-id="e01f0-176">In this code sample, **SetMultipleProfileProperties** sets the following user profile properties for a user:</span></span>

-  <span data-ttu-id="e01f0-177">**PictureURL** - значение URL-адрес среднего размера загружаемого изображения в библиотеке рисунков на узле личных сайтов.</span><span class="sxs-lookup"><span data-stu-id="e01f0-177">**PictureURL** - Set to the URL of the medium-sized uploaded image in the picture library on the My Site Host.</span></span>
    
-  <span data-ttu-id="e01f0-178">**SPS PicturePlaceholderState** - нулевое значение для указания, что SharePoint Online следует показывать изображение загруженному для пользователя.</span><span class="sxs-lookup"><span data-stu-id="e01f0-178">**SPS-PicturePlaceholderState** - Set to zero to indicate that SharePoint Online should show the uploaded picture for the user.</span></span>

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

<span data-ttu-id="e01f0-179">**SetAdditionalProfileProperties** задает любые дополнительные пользовательские свойства профилей, которые необходимо обновить после отправки файлы изображений.</span><span class="sxs-lookup"><span data-stu-id="e01f0-179">**SetAdditionalProfileProperties** sets any additional user profile properties you want to update after uploading the image files.</span></span> <span data-ttu-id="e01f0-180">Можно указать дополнительные свойства для обновления в файле configuration.xml.</span><span class="sxs-lookup"><span data-stu-id="e01f0-180">You can specify additional properties to update in the configuration.xml file.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="e01f0-181">См. также</span><span class="sxs-lookup"><span data-stu-id="e01f0-181">See also</span></span>
<span data-ttu-id="e01f0-182"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e01f0-182"></span></span>

-  [<span data-ttu-id="e01f0-183">Решения пользовательского профиля для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="e01f0-183">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="e01f0-184">Core.ProfilePictureUploader приложения</span><span class="sxs-lookup"><span data-stu-id="e01f0-184">Core.ProfilePictureUploader app</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [<span data-ttu-id="e01f0-185">UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="e01f0-185">UserProfile.Manipulation.CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [<span data-ttu-id="e01f0-186">Core.ProfileProperty.Migration</span><span class="sxs-lookup"><span data-stu-id="e01f0-186">Core.ProfileProperty.Migration</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration)
    
-  [<span data-ttu-id="e01f0-187">UserProfile.Manipulation.CSOM.Console</span><span class="sxs-lookup"><span data-stu-id="e01f0-187">UserProfile.Manipulation.CSOM.Console</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
