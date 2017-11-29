---
title: "Перенос пользователей профиля свойств пример надстройки для SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 70b8fec69c22a0394184f6af969714d922b4c25a
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="migrate-user-profile-properties-sample-add-in-for-sharepoint"></a><span data-ttu-id="31bc8-102">Перенос пользователей профиля свойств пример надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="31bc8-102">Migrate user profile properties sample add-in for SharePoint</span></span>

<span data-ttu-id="31bc8-103">Можно использовать размещение у поставщика в надстройке перенос и импортировать данные профилей пользователей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31bc8-103">You can use a provider-hosted add-in to migrate and import SharePoint user profile data.</span></span>

<span data-ttu-id="31bc8-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="31bc8-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>
    
<span data-ttu-id="31bc8-105">Пример надстройки [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) показано, как для переноса данных профилей пользователей с SharePoint Server 2010 и SharePoint Server 2013 в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="31bc8-105">The [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) sample add-in shows you how to migrate user profile data from SharePoint Server 2010 or SharePoint Server 2013 into SharePoint Online.</span></span>
    
<span data-ttu-id="31bc8-106">Этот пример включает два консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="31bc8-106">This sample includes two console applications.</span></span> <span data-ttu-id="31bc8-107">Оба используют userprofileservice.asmx веб-службы для извлечения данных профиля пользователя одним или несколькими значениями в XML-файл, а также для импорта данных в службе профилей пользователей в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="31bc8-107">Both use the userprofileservice.asmx web service to extract single and multivalued user profile data to an XML file, and to import the extracted data into the user profile service in SharePoint Online.</span></span>
<span data-ttu-id="31bc8-108">Если вы хотите используйте в этом примере кода:</span><span class="sxs-lookup"><span data-stu-id="31bc8-108">Use this code sample if you want to:</span></span>

- <span data-ttu-id="31bc8-109">Извлечение данных профиля пользователя в SharePoint Server 2010 и SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="31bc8-109">Extract user profile data in SharePoint Server 2010 or SharePoint Server 2013.</span></span>
    
- <span data-ttu-id="31bc8-110">Импортировать данные профилей пользователей в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="31bc8-110">Import user profile data into SharePoint Online.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="31bc8-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="31bc8-111">Before you begin</span></span>
<span data-ttu-id="31bc8-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="31bc8-112"></span></span>

<span data-ttu-id="31bc8-113">Чтобы начать работу, загрузите пример надстройки [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="31bc8-113">To get started, download the  [Core.ProfileProperty.Migration](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfileProperty.Migration) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span> <span data-ttu-id="31bc8-114">Пример кода содержит два проекта.</span><span class="sxs-lookup"><span data-stu-id="31bc8-114">The code sample contains two projects.</span></span>

<span data-ttu-id="31bc8-115">Для проекта **Contoso.ProfileProperty.Migration.Extract** :</span><span class="sxs-lookup"><span data-stu-id="31bc8-115">For the  **Contoso.ProfileProperty.Migration.Extract** project:</span></span>

- <span data-ttu-id="31bc8-116">Поскольку в этом примере кода используется на сервере объектной модели, убедитесь, что выполнения проекта на сервере с SharePoint Server 2010 или установки SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="31bc8-116">Because this code sample uses the server-side object model, be sure that you are running the project on a server with SharePoint Server 2010 or SharePoint Server 2013 installed.</span></span>
    
- <span data-ttu-id="31bc8-117">Используйте учетную запись с разрешениями администратора фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31bc8-117">Use an account that has SharePoint farm administrator permissions.</span></span>
    
- <span data-ttu-id="31bc8-118">Измените файл App.config, с помощью сведений о конфигурации, указанные в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="31bc8-118">Edit the App.config file using the configuration information listed in Table 1.</span></span>
    
- <span data-ttu-id="31bc8-119">Для всех пользователей убедитесь, что свойство профиля пользователя **рабочий адрес электронной почты** не является пустым.</span><span class="sxs-lookup"><span data-stu-id="31bc8-119">For all users, ensure that the  **Work email** user profile property is not empty.</span></span> <span data-ttu-id="31bc8-120">Если пустое значение свойства профиля пользователя **электронной почты рабочий** процесс извлечения будет преждевременно.</span><span class="sxs-lookup"><span data-stu-id="31bc8-120">If the value of the **Work email** user profile property is empty, the extraction process will end prematurely.</span></span>
    
- <span data-ttu-id="31bc8-121">В этом примере кода извлекает профилей пользователей с SharePoint Server 2010.</span><span class="sxs-lookup"><span data-stu-id="31bc8-121">This code sample extracts user profiles from SharePoint Server 2010.</span></span> <span data-ttu-id="31bc8-122">При извлечении профилей пользователей с SharePoint Server 2013, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="31bc8-122">If you are extracting user profiles from SharePoint Server 2013, do the following:</span></span>
    
  <span data-ttu-id="31bc8-123">.</span><span class="sxs-lookup"><span data-stu-id="31bc8-123">a.</span></span> <span data-ttu-id="31bc8-124">Откройте контекстное меню (щелкните правой кнопкой мыши) для **Contoso.ProfileProperty.Migration.Extract** > **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-124">Open the shortcut menu (right-click) for  **Contoso.ProfileProperty.Migration.Extract** > **Properties**.</span></span>
    
  <span data-ttu-id="31bc8-125">б.</span><span class="sxs-lookup"><span data-stu-id="31bc8-125">b.</span></span> <span data-ttu-id="31bc8-126">В разделе **приложения**в **требуемой версии .NET framework** выберите **.NET Framework 4**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-126">Under  **Application**, in  **Target framework** choose **.NET Framework 4**.</span></span>
    
  <span data-ttu-id="31bc8-127">c.</span><span class="sxs-lookup"><span data-stu-id="31bc8-127">c.</span></span> <span data-ttu-id="31bc8-128">Нажмите кнопку **Да**, затем **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-128">Choose  **Yes**, then  **Save**.</span></span>
    
<span data-ttu-id="31bc8-129">**В таблице 1. Параметры конфигурации для файла App.Config**</span><span class="sxs-lookup"><span data-stu-id="31bc8-129">**Table 1. Configuration settings for App.Config file**</span></span>

|<span data-ttu-id="31bc8-130">**Имя параметра конфигурации**</span><span class="sxs-lookup"><span data-stu-id="31bc8-130">**Configuration setting name**</span></span>|<span data-ttu-id="31bc8-131">**Описание**</span><span class="sxs-lookup"><span data-stu-id="31bc8-131">**Description**</span></span>|<span data-ttu-id="31bc8-132">Пример</span><span class="sxs-lookup"><span data-stu-id="31bc8-132">Example</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="31bc8-133">**MYSITEHOSTURL**</span><span class="sxs-lookup"><span data-stu-id="31bc8-133">**MYSITEHOSTURL**</span></span> |<span data-ttu-id="31bc8-134">Мои URL-адрес сайта в исходной ферме SharePoint Server 2010 и SharePoint Server 2013.</span><span class="sxs-lookup"><span data-stu-id="31bc8-134">My Site URL on the source SharePoint Server 2010 or SharePoint Server 2013 farm.</span></span>|<span data-ttu-id="31bc8-135">http://My.contoso.com</span><span class="sxs-lookup"><span data-stu-id="31bc8-135">http://my.contoso.com</span></span> |
|<span data-ttu-id="31bc8-136">**PROPERTYSEPERATOR**</span><span class="sxs-lookup"><span data-stu-id="31bc8-136">**PROPERTYSEPERATOR**</span></span> |<span data-ttu-id="31bc8-137">Знак, используемый для разделения нескольких значений в свойства профиля пользователя с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="31bc8-137">The character used to separate multiple values in a multivalued user profile property.</span></span>| |
|<span data-ttu-id="31bc8-138">**USERPROFILESSTORE**</span><span class="sxs-lookup"><span data-stu-id="31bc8-138">**USERPROFILESSTORE**</span></span> |<span data-ttu-id="31bc8-139">Путь к файлу XML использовать для записи данных профиля извлеченные пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-139">The XML file path to use to write extracted user profile data.</span></span>|<span data-ttu-id="31bc8-140">C:\temp\ProfileData.XML</span><span class="sxs-lookup"><span data-stu-id="31bc8-140">C:\temp\ProfileData.xml</span></span>|
|<span data-ttu-id="31bc8-141">**ФАЙЛ ЖУРНАЛА**</span><span class="sxs-lookup"><span data-stu-id="31bc8-141">**LOGFILE**</span></span> |<span data-ttu-id="31bc8-142">Путь к файлу XML использовать для записи данных профиля извлеченные пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-142">The XML file path to use to write extracted user profile data.</span></span>|<span data-ttu-id="31bc8-143">C:\temp\Extract.log</span><span class="sxs-lookup"><span data-stu-id="31bc8-143">C:\temp\Extract.log</span></span>|
|<span data-ttu-id="31bc8-144">**ENABLELOGGING**</span><span class="sxs-lookup"><span data-stu-id="31bc8-144">**ENABLELOGGING**</span></span> |<span data-ttu-id="31bc8-145">Включить ведение журнала диска.</span><span class="sxs-lookup"><span data-stu-id="31bc8-145">Enable disk logging.</span></span>|<span data-ttu-id="31bc8-146">Значение true</span><span class="sxs-lookup"><span data-stu-id="31bc8-146">True</span></span>|
|<span data-ttu-id="31bc8-147">**ТЕСТОВЫЙ ПРОГОН**</span><span class="sxs-lookup"><span data-stu-id="31bc8-147">**TESTRUN**</span></span> |<span data-ttu-id="31bc8-148">Выполняет извлечение тестирования для убедитесь, что указаны правильные параметры конфигурации в файле App.Config.</span><span class="sxs-lookup"><span data-stu-id="31bc8-148">Performs a test extraction to confirm that your configuration settings in App.Config are correct.</span></span>|<span data-ttu-id="31bc8-149">Установка `TESTRUN=true` при выполнении извлечения тестирования.</span><span class="sxs-lookup"><span data-stu-id="31bc8-149">Set `TESTRUN=true` if you are performing a test extraction.</span></span> <span data-ttu-id="31bc8-150">Запустите тест извлекает только одного пользователя из службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="31bc8-150">The test run extracts only one user from the user profile service.</span></span><br /> <span data-ttu-id="31bc8-151">Установка `TESTRUN=false` при извлечении всех пользователей из службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="31bc8-151">Set `TESTRUN=false` if you are extracting all users from the user profile service.</span></span> |

<span data-ttu-id="31bc8-152">Для проекта **Contoso.ProfileProperty.Migration.Import**</span><span class="sxs-lookup"><span data-stu-id="31bc8-152">For the  **Contoso.ProfileProperty.Migration.Import** project</span></span>

- <span data-ttu-id="31bc8-153">Убедитесь, что существуют профили пользователей в Office 365.</span><span class="sxs-lookup"><span data-stu-id="31bc8-153">Ensure that user profiles exist in Office 365.</span></span> 
    
- <span data-ttu-id="31bc8-154">Убедитесь, что адрес **рабочий адрес электронной почты** пользователя — это то же самое, в SharePoint Server 2013 в локальной и службы профилей пользователей Office 365.</span><span class="sxs-lookup"><span data-stu-id="31bc8-154">Ensure that the user's  **Work email** address is the same in the SharePoint Server 2013 on-premises and Office 365 user profile service.</span></span>
    
- <span data-ttu-id="31bc8-155">В файле App.config измените **значение** элемента параметр **Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService** , чтобы получить справку службы профилей пользователей в центре администрирования SharePoint Online, как показано в Следующий пример.</span><span class="sxs-lookup"><span data-stu-id="31bc8-155">In the App.config file, change the  **value** element of the **Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService** setting to include a reference to the user profile service in your SharePoint Online admin center, as shown in the following example.</span></span>

    ```XML
    <applicationSettings>
    <Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    <setting name="Contoso_ProfileProperty_Migration_Import_UPSvc_UserProfileService" serializeAs="String">
    <value>https://contoso-admin.sharepoint.com/_vti_bin/userprofileservice.asmx</value>
    </setting>
    </Contoso.ProfileProperty.Migration.Import.Properties.Settings>
    </applicationSettings>
    ```

- <span data-ttu-id="31bc8-156">Измените файл App.config, используя параметры конфигурации, указанные в таблице 2.</span><span class="sxs-lookup"><span data-stu-id="31bc8-156">Edit the App.config file using the configuration settings listed in Table 2.</span></span>
    
<span data-ttu-id="31bc8-157">**В таблице 2. Параметры конфигурации файла app.config**</span><span class="sxs-lookup"><span data-stu-id="31bc8-157">**Table 2. App.config file configuration settings**</span></span>

|<span data-ttu-id="31bc8-158">**Имя параметра конфигурации**</span><span class="sxs-lookup"><span data-stu-id="31bc8-158">**Configuration setting name**</span></span>|<span data-ttu-id="31bc8-159">**Описание**</span><span class="sxs-lookup"><span data-stu-id="31bc8-159">**Description**</span></span>|<span data-ttu-id="31bc8-160">Пример</span><span class="sxs-lookup"><span data-stu-id="31bc8-160">Example</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="31bc8-161">**tenantName**</span><span class="sxs-lookup"><span data-stu-id="31bc8-161">**tenantName**</span></span> |<span data-ttu-id="31bc8-162">Это имя вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="31bc8-162">This is your tenant’s name.</span></span>|<span data-ttu-id="31bc8-163">Если URL-адрес клиента http://contoso.onmicrosoft.com, введите contoso как имя клиента.</span><span class="sxs-lookup"><span data-stu-id="31bc8-163">If your tenant URL is http://contoso.onmicrosoft.com, enter contoso as your tenant name.</span></span>|
|<span data-ttu-id="31bc8-164">**PROPERTYSEPERATOR**</span><span class="sxs-lookup"><span data-stu-id="31bc8-164">**PROPERTYSEPERATOR**</span></span> |<span data-ttu-id="31bc8-165">Знак, используемый для разделения значений в свойства профиля пользователя с несколькими значениями.</span><span class="sxs-lookup"><span data-stu-id="31bc8-165">The character used to separate values in a multivalued user profile property.</span></span>| |
|<span data-ttu-id="31bc8-166">**USERPROFILESSTORE**</span><span class="sxs-lookup"><span data-stu-id="31bc8-166">**USERPROFILESSTORE**</span></span> |<span data-ttu-id="31bc8-167">XML-файл для использования на чтение данных профиля пользователя извлеченные.</span><span class="sxs-lookup"><span data-stu-id="31bc8-167">The XML file to use to read extracted user profile data.</span></span>|<span data-ttu-id="31bc8-168">C:\temp\ProfileData.XML</span><span class="sxs-lookup"><span data-stu-id="31bc8-168">C:\temp\ProfileData.xml</span></span>|
|<span data-ttu-id="31bc8-169">**ФАЙЛ ЖУРНАЛА**</span><span class="sxs-lookup"><span data-stu-id="31bc8-169">**LOGFILE**</span></span> |<span data-ttu-id="31bc8-170">Файл журнала используется для регистрации событий.</span><span class="sxs-lookup"><span data-stu-id="31bc8-170">Log file used for event logging.</span></span>|<span data-ttu-id="31bc8-171">C:\temp\Extract.log</span><span class="sxs-lookup"><span data-stu-id="31bc8-171">C:\temp\Extract.log</span></span>|
|<span data-ttu-id="31bc8-172">**ENABLELOGGING**</span><span class="sxs-lookup"><span data-stu-id="31bc8-172">**ENABLELOGGING**</span></span> |<span data-ttu-id="31bc8-173">Включить ведение журнала диска.</span><span class="sxs-lookup"><span data-stu-id="31bc8-173">Enable disk logging.</span></span>|<span data-ttu-id="31bc8-174">Значение true</span><span class="sxs-lookup"><span data-stu-id="31bc8-174">True</span></span>|
|<span data-ttu-id="31bc8-175">**SPOAdminUserName**</span><span class="sxs-lookup"><span data-stu-id="31bc8-175">**SPOAdminUserName**</span></span> |<span data-ttu-id="31bc8-176">Имя пользователя администратора Office 365.</span><span class="sxs-lookup"><span data-stu-id="31bc8-176">An Office 365 administrator’s username.</span></span>|<span data-ttu-id="31bc8-177">Примеры</span><span class="sxs-lookup"><span data-stu-id="31bc8-177">Not applicable.</span></span>|
|<span data-ttu-id="31bc8-178">**SPOAdminPassword**</span><span class="sxs-lookup"><span data-stu-id="31bc8-178">**SPOAdminPassword**</span></span> |<span data-ttu-id="31bc8-179">Пароль администратора Office 365.</span><span class="sxs-lookup"><span data-stu-id="31bc8-179">An Office 365 administrator’s password.</span></span>|<span data-ttu-id="31bc8-180">Примеры</span><span class="sxs-lookup"><span data-stu-id="31bc8-180">Not applicable.</span></span>|

## <a name="using-the-coreprofilepropertymigration-app"></a><span data-ttu-id="31bc8-181">С помощью приложения Core.ProfileProperty.Migration</span><span class="sxs-lookup"><span data-stu-id="31bc8-181">Using the Core.ProfileProperty.Migration app</span></span>
<span data-ttu-id="31bc8-182"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="31bc8-182"></span></span>

<span data-ttu-id="31bc8-183">В этом примере кода используется в качестве консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="31bc8-183">This code sample runs as a console application.</span></span> <span data-ttu-id="31bc8-184">Пример кода, функция **Main** в файле Program.cs выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="31bc8-184">When the code sample runs, the  **Main** function in Program.cs performs the following tasks:</span></span>

- <span data-ttu-id="31bc8-185">Подключается к узла личных сайтов и использует **Диспетчер профилей пользователей** для подключения к службе профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="31bc8-185">Connects to the My Site Host and uses  **UserProfileManager** to connect to the user profile service.</span></span> <span data-ttu-id="31bc8-186">**Диспетчер профилей пользователей** , принадлежит к сборке **Microsoft.Office.Server.UserProfiles.dll** .</span><span class="sxs-lookup"><span data-stu-id="31bc8-186">**UserProfileManager** belongs to the **Microsoft.Office.Server.UserProfiles.dll** assembly.</span></span>
    
- <span data-ttu-id="31bc8-187">Создает список с именем **pData** для хранения данных профиля извлеченные пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-187">Creates a list called  **pData** to store extracted user profile data.</span></span>
    
- <span data-ttu-id="31bc8-188">Для всех пользователей в службе профилей пользователей выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="31bc8-188">For all users in the user profile service it does the following:</span></span>
    
    - <span data-ttu-id="31bc8-189">Использует **GetSingleValuedProperty** для копирования объект **UserProfileData** с именем **userData** **WorkEmail** и **AboutMe** свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-189">Uses  **GetSingleValuedProperty** to copy the **WorkEmail** and **AboutMe** user profile properties to a **UserProfileData** object called **userData**.</span></span>
    
    - <span data-ttu-id="31bc8-190">Использует **GetMultiValuedProperty** для копирования свойство профиля пользователя **Ответственность за SPS** **userData**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-190">Uses  **GetMultiValuedProperty** to copy the **SPS-Responsibility** user profile property to **userData**.</span></span>
    
- <span data-ttu-id="31bc8-191">Использует **UserProfileCollection.Save** для сериализации **userData** в XML-файл.</span><span class="sxs-lookup"><span data-stu-id="31bc8-191">Uses  **UserProfileCollection.Save** to serialize **userData** to an XML file.</span></span> <span data-ttu-id="31bc8-192">XML-файл сохраняется в путь к файлу, указанному в файле App.config.</span><span class="sxs-lookup"><span data-stu-id="31bc8-192">The XML file is saved at the file path you specified in App.config.</span></span>

<span data-ttu-id="31bc8-193">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="31bc8-193">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="31bc8-194">Обратите внимание на то, что метод **GetSingleValuedProperty** используется для получения свойства профиля пользователя с одним значением userprofileservice.asmx.</span><span class="sxs-lookup"><span data-stu-id="31bc8-194">Note that the  **GetSingleValuedProperty** method uses userprofileservice.asmx to retrieve a single-valued user profile property.</span></span> <span data-ttu-id="31bc8-195">**GetSingleValuedProperty** производит следующие действия, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="31bc8-195">**GetSingleValuedProperty** does the following, as shown in the next code example:</span></span>

- <span data-ttu-id="31bc8-196">Возвращает объект свойства для извлечения данных из с помощью **spuser [userProperty]**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-196">Gets the property object to extract data from using  **spuser[userProperty]**.</span></span>
    
- <span data-ttu-id="31bc8-197">Возвращает первое значение в **UserProfileValueCollection** , если значение не равно **null**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-197">Returns the first value in the  **UserProfileValueCollection** if the value is not **null**.</span></span> 

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

<span data-ttu-id="31bc8-198">Обратите внимание на то, что метод **GetMultiValuedProperty** используется для получения свойства профиля пользователя многозначных userprofileservice.asmx.</span><span class="sxs-lookup"><span data-stu-id="31bc8-198">Note that the  **GetMultiValuedProperty** method uses userprofileservice.asmx to retrieve a multivalued user profile property.</span></span> <span data-ttu-id="31bc8-199">**GetMultiValuedProperty** производит следующие действия, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="31bc8-199">**GetMultiValuedProperty** does the following, as shown in the next code example:</span></span>

- <span data-ttu-id="31bc8-200">Получает объект свойство профиля пользователя с помощью **spuser [userProperty]**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-200">Gets the user profile property object to update using  **spuser[userProperty]**.</span></span>
    
- <span data-ttu-id="31bc8-201">Создает строку, разделенных точкой с **PROPERTYSEPARATOR** , указанное в файле App.config значений свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-201">Builds a string of user profile property values separated by the  **PROPERTYSEPARATOR** specified in the App.config file.</span></span>

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

## <a name="using-contosoprofilepropertymigrationimport"></a><span data-ttu-id="31bc8-202">С помощью Contoso.ProfileProperty.Migration.Import</span><span class="sxs-lookup"><span data-stu-id="31bc8-202">Using Contoso.ProfileProperty.Migration.Import</span></span>
<span data-ttu-id="31bc8-203"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="31bc8-203"></span></span>

<span data-ttu-id="31bc8-204">В этом примере кода используется в качестве консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="31bc8-204">This code sample runs as a console application.</span></span> <span data-ttu-id="31bc8-205">При запуске образца кода, метод **Main** в файле Program.cs выполняет следующее.</span><span class="sxs-lookup"><span data-stu-id="31bc8-205">When the code sample runs, the  **Main** method in Program.cs does the following:</span></span>

- <span data-ttu-id="31bc8-206">Инициализирует консольное приложение, с помощью **InitializeConfiguration** и **InitializeWebService**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-206">Initializes the console application using  **InitializeConfiguration** and **InitializeWebService**.</span></span> 
    
- <span data-ttu-id="31bc8-207">Десериализации XML-файл, содержащий данные профиля извлеченные пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-207">Deserializes the XML file containing the extracted user profile data.</span></span>
    
- <span data-ttu-id="31bc8-208">Для всех пользователей в XML-файле выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="31bc8-208">For all users in the XML file it does the following:</span></span>
    
    - <span data-ttu-id="31bc8-209">Извлекает свойства **UserName** из XML-файла.</span><span class="sxs-lookup"><span data-stu-id="31bc8-209">Extracts the  **UserName** property from the XML file.</span></span>
    
    - <span data-ttu-id="31bc8-210">**SetSingleMVProfileProperty** используется для определения **SPS ответственности** в профиле пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-210">Uses  **SetSingleMVProfileProperty** to set **SPS-Responsibility** on the user's profile.</span></span>
    
    - <span data-ttu-id="31bc8-211">**SetSingleMVProfileProperty** используется для определения **AboutMe** на профиль пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-211">Uses  **SetSingleMVProfileProperty** to set **AboutMe** on the user's profile.</span></span>
    
<span data-ttu-id="31bc8-212">**InitializeWebService** подключается к SharePoint Online и задает ссылку службы профилей пользователей для переменной экземпляра.</span><span class="sxs-lookup"><span data-stu-id="31bc8-212">**InitializeWebService** connects to SharePoint Online, and sets a reference of the user profile service to an instance variable.</span></span> <span data-ttu-id="31bc8-213">Другие методы в этом примере кода эта переменная экземпляра используется для записи значений свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-213">Other methods in this code sample use this instance variable to write values to user profile properties.</span></span> <span data-ttu-id="31bc8-214">Для администрирования профилей пользователей, в этом образце кода используется userprofileservice.asmx веб-службы в центре администрирования SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="31bc8-214">To administer the user profile, this code sample uses the userprofileservice.asmx web service on the SharePoint Online admin center.</span></span>

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

<span data-ttu-id="31bc8-215">Метод **SetSingleMVProfileProperty** устанавливает многозначных свойство профиля, например **SPS-ответственности**, выполнив следующие:</span><span class="sxs-lookup"><span data-stu-id="31bc8-215">The  **SetSingleMVProfileProperty** method sets a multivalued user profile property, such as **SPS-Responsibility**, by doing the following:</span></span>

- <span data-ttu-id="31bc8-216">Разделение **PropertyValue** в массив строк вызывает **arrs** для хранения значения свойств профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="31bc8-216">Splitting  **PropertyValue** into a string array called **arrs** to store user profile property values.</span></span> <span data-ttu-id="31bc8-217">Строка разделяется с помощью параметра конфигурации **PROPERTYSEPERATOR** , указанное в файле App.Config.</span><span class="sxs-lookup"><span data-stu-id="31bc8-217">The string is split using the **PROPERTYSEPERATOR** configuration setting specified in App.Config.</span></span>
    
- <span data-ttu-id="31bc8-218">Присвоение значения **arrs** массиву **ValueData** на службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="31bc8-218">Assigning the values of  **arrs** to a **ValueData** array on the user profile service.</span></span>
    
- <span data-ttu-id="31bc8-219">Создание массива **PropertyData** для службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="31bc8-219">Creating a  **PropertyData** array on the user profile service.</span></span> <span data-ttu-id="31bc8-220">Имя свойства профиля пользователя и массива **ValueData** передаются в свойства объекта **PropertyData** .</span><span class="sxs-lookup"><span data-stu-id="31bc8-220">The name of the user profile property and the **ValueData** array are passed to properties on the **PropertyData** object.</span></span> <span data-ttu-id="31bc8-221">Этот массив имеет один элемент только так, как только одно свойство профиля пользователя многозначных будет импортирован.</span><span class="sxs-lookup"><span data-stu-id="31bc8-221">This array has one element only because only one multivalued user profile property will be imported.</span></span>
    
<span data-ttu-id="31bc8-222">Данные записываются для службы профилей пользователей, с помощью **ModifyUserPropertyByAccountName** на веб-службы **userprofileservice.asmx** в центре администрирования SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="31bc8-222">The data is written to the user profile service using  **ModifyUserPropertyByAccountName** on the **userprofileservice.asmx** web service on the SharePoint Online admin center.</span></span> <span data-ttu-id="31bc8-223">Пользователя, выполняющего этот пример кода необходимо иметь полномочия администратора Office 365.</span><span class="sxs-lookup"><span data-stu-id="31bc8-223">The user running this code sample must be an Office 365 administrator.</span></span>

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

<span data-ttu-id="31bc8-224">Метод **SetSingleValuedProperty** устанавливает свойства профиля пользователя одним значением, такие как **AboutMe**.</span><span class="sxs-lookup"><span data-stu-id="31bc8-224">The  **SetSingleValuedProperty** method sets single-valued user profile properties, such as **AboutMe**.</span></span>  <span data-ttu-id="31bc8-225">**SetSingleValuedProperty** реализует та же технология, как **SetSingleMVProfileProperty**, но использует **ValueData** массива с только один элемент.</span><span class="sxs-lookup"><span data-stu-id="31bc8-225">**SetSingleValuedProperty** implements the same technique as **SetSingleMVProfileProperty**, but uses a  **ValueData** array with one element only.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="31bc8-226">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="31bc8-226">Additional resources</span></span>
<span data-ttu-id="31bc8-227"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="31bc8-227"></span></span>

-  [<span data-ttu-id="31bc8-228">Решения пользовательского профиля для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="31bc8-228">User profile solutions for SharePoint 2013 and SharePoint Online</span></span>](user-profile-solutions-for-sharepoint.md)
    
-  [<span data-ttu-id="31bc8-229">Core.ProfilePictureUploader</span><span class="sxs-lookup"><span data-stu-id="31bc8-229">Core.ProfilePictureUploader</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.ProfilePictureUploader)
    
-  [<span data-ttu-id="31bc8-230">UserProfile.Manipulation.CSOM</span><span class="sxs-lookup"><span data-stu-id="31bc8-230">UserProfile.Manipulation.CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM)
    
-  [<span data-ttu-id="31bc8-231">UserProfile.Manipulation.CSOM.Console</span><span class="sxs-lookup"><span data-stu-id="31bc8-231">UserProfile.Manipulation.CSOM.Console</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.Manipulation.CSOM.Console)
