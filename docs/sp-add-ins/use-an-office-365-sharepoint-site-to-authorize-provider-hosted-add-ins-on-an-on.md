
# <a name="use-an-office-365-sharepoint-site-to-authorize-provider-hosted-add-ins-on-an-on-premises-sharepoint-site"></a><span data-ttu-id="30b3d-101">Использование сайта SharePoint Office 365 для авторизации размещенных у поставщика надстроек на локальном сайте SharePoint</span><span class="sxs-lookup"><span data-stu-id="30b3d-101">Use an Office 365 SharePoint site to authorize provider-hosted add-ins on an on-premises SharePoint site</span></span>
<span data-ttu-id="30b3d-102">В этой статье описывается использование сайта Office 365 SharePoint для создания среды, в которой можно применять службу контроля доступа для установления отношения доверия между надстройкой с размещением у поставщика и в локальной ферме SharePoint, как при разработке надстроек для сайта Office 365 SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-102">Use an Office 365 SharePoint site to create an environment where you can use ACS to establish trust between a provider-hosted add-in and an on-premises SharePoint farm, just as you would if you were developing add-ins for an Office 365 SharePoint site.</span></span>
 

 <span data-ttu-id="30b3d-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="30b3d-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="prerequisites-for-using-acs-with-provider-hosted-add-ins-in-on-premises-environments"></a><span data-ttu-id="30b3d-106">Необходимые условия для использования службы контроля доступа и надстроек с размещением у поставщика в локальных средах</span><span class="sxs-lookup"><span data-stu-id="30b3d-106">Prerequisites for using ACS with provider-hosted add-ins in on-premises environments</span></span>
<span data-ttu-id="30b3d-107"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-107"></span></span>

<span data-ttu-id="30b3d-108">Убедитесь, что у вас есть все перечисленные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="30b3d-108">Be sure that you have the following.</span></span>
 

 

- <span data-ttu-id="30b3d-p102">Локальная среда разработки SharePoint. См. статью [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="30b3d-p102">An on-premises SharePoint development environment. See  [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span></span>
    
 
- <span data-ttu-id="30b3d-p103">Сайт Office 365 SharePoint. Если у вас его еще нет и вы хотите быстро настроить среду разработки, вы можете  [Настройка среды для разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365).</span><span class="sxs-lookup"><span data-stu-id="30b3d-p103">An Office 365 SharePoint site. If don't have one yet and you want to set up a development environment quickly, you can  [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365).</span></span>
    
 
-  <span data-ttu-id="30b3d-113">Среда [Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682), установленная либо на удаленном компьютере, либо на одном компьютере с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-113">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) installed either remotely or on the computer where you installed SharePoint.</span></span>
    
 
-  <span data-ttu-id="30b3d-114">[Инструменты разработчика Microsoft Office для Visual Studio 2012](https://msdn.microsoft.com/en-us/office/aa905340.aspx).</span><span class="sxs-lookup"><span data-stu-id="30b3d-114">[Microsoft Office Developer Tools for Visual Studio 2012](https://msdn.microsoft.com/en-us/office/aa905340.aspx) .</span></span>
    
 
- <span data-ttu-id="30b3d-p104">64-разрядный выпуск [помощника по входу в Microsoft Online Services](http://www.microsoft.com/en-us/download/details.aspx?id=41950), установленный на одном компьютере с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p104">The 64-bit edition of  [Microsoft Online Services Sign-In Assistant.](http://www.microsoft.com/en-us/download/details.aspx?id=41950) installed on the computer where you installed SharePoint.</span></span>
    
 
-  <span data-ttu-id="30b3d-117">[Модуль Microsoft Online Services для Windows Powershell (64-разрядная версия)](http://go.microsoft.com/fwlink/p/?linkid=236297), установленный на одном компьютере с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-117">[Microsoft Online Services Module for Windows Powershell (64-bit)](http://go.microsoft.com/fwlink/p/?linkid=236297) installed on the computer where you installed SharePoint.</span></span>
    
 

## <a name="create-a-certificate-and-make-it-the-security-token-service-sts-certificate-of-your-on-premises-installation-of-sharepoint"></a><span data-ttu-id="30b3d-118">Создание сертификата и назначение его сертификатом службы токенов безопасности (STS) для локальной установки SharePoint</span><span class="sxs-lookup"><span data-stu-id="30b3d-118">Create a certificate and make it the security token service (STS) certificate of your on-premises installation of SharePoint</span></span>
<span data-ttu-id="30b3d-119"><a name="Certificate"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-119"></span></span>

<span data-ttu-id="30b3d-p105">Вам потребуется заменить используемый по умолчанию сертификат службы токенов безопасности (STS) своей локальной установки SharePoint на собственный сертификат. В этой статье приводится пример создания тестового сертификата и его экспорта с помощью команды **Создать самозаверяющий сертификат** в службах IIS. Вы также можете использовать коммерческий сертификат, выданный центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p105">You'll need to replace the default security token service (STS) certificate of your on-premises installation of SharePoint with your own certificate. This article gives you an example of how to create and export a test certificate by using the **Create Self Signed Certificate** option in IIS. You can also use a commercial certificate issued by a certificate authority.</span></span>
 

 
 <span data-ttu-id="30b3d-123">[Сначала создайте тестовый PFX-файл сертификата, а затем соответствующий CER-файл](http://msdn.microsoft.com/en-us/library/windows/hardware/ff552299%28v=vs.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="30b3d-123">[Create a test .pfx certificate file first, and then a corresponding test .cer file](http://msdn.microsoft.com/en-us/library/windows/hardware/ff552299%28v=vs.85%29.aspx).</span></span> 
 

 
 <span data-ttu-id="30b3d-124">[Вы также можете использовать тестовую программу MakeCert, чтобы создать тестовый сертификат X.509](http://msdn.microsoft.com/en-us/library/ms537364%28VS.85%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="30b3d-124">[You can also use the MakeCert test program to generate a test X.509 certificate](http://msdn.microsoft.com/en-us/library/ms537364%28VS.85%29.aspx).</span></span> 
 

 

### <a name="to-create-a-test-pfx-certificate-file"></a><span data-ttu-id="30b3d-125">Создание тестового PFX-файла сертификата</span><span class="sxs-lookup"><span data-stu-id="30b3d-125">To create a test .pfx certificate file</span></span>


1. <span data-ttu-id="30b3d-126">В диспетчере IIS выберите узел _Имя сервера_ в представлении в виде дерева слева.</span><span class="sxs-lookup"><span data-stu-id="30b3d-126">In IIS Manager, select the  _ServerName_ node in the tree view on the left.</span></span>
    
 
2. <span data-ttu-id="30b3d-127">Выберите **Сертификаты сервера**, как показано на рис. 1.</span><span class="sxs-lookup"><span data-stu-id="30b3d-127">Choose **Server Certificates**, as shown in Figure 1.</span></span>
    
    <span data-ttu-id="30b3d-128">**Рис. 1. Элемент "Сертификаты сервера" в службах IIS**</span><span class="sxs-lookup"><span data-stu-id="30b3d-128">**Figure 1. Server Certificates option in IIS**</span></span>

 

  ![Элемент "Сертификаты сервера" в службах IIS](../../images/e38f9b7f-59a3-468c-bcde-a48272f1f217.gif)
 

 

 
3. <span data-ttu-id="30b3d-130">В наборе ссылок справа нажмите **Создать самозаверяющий сертификат**, как показано на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="30b3d-130">Click the **Create Self-Signed Certificate** link in the set of links on the right side, as shown in Figure 2.</span></span>
    
    <span data-ttu-id="30b3d-131">**Рис. 2. Ссылка "Создать самозаверяющий сертификат"**</span><span class="sxs-lookup"><span data-stu-id="30b3d-131">**Figure 2. Create Self-Signed Certificate link**</span></span>

 

  ![Ссылка "Создать самозаверяющий сертификат"](../../images/3f0aae5a-e58b-4ec8-b67f-0024abfa2dab.gif)
 

 

 
4. <span data-ttu-id="30b3d-133">Задайте для сертификата имя SampleCert и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="30b3d-133">Name the certificate SampleCert, and then choose **OK**.</span></span>
    
 
5. <span data-ttu-id="30b3d-134">Щелкните сертификат правой кнопкой мыши и выберите пункт **Экспорт**, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="30b3d-134">Right-click the certificate, and then choose **Export**, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="30b3d-135">**Рис. 3. Экспорт тестового сертификата**</span><span class="sxs-lookup"><span data-stu-id="30b3d-135">**Figure 3. Exporting a test certificate**</span></span>

 

  ![Экспорт тестового сертификата](../../images/997021de-c60c-46b0-961f-7e1e63c0f619.gif)
 

 

 
6. <span data-ttu-id="30b3d-p106">Экспортируйте файл в выбранное расположение и создайте для него пароль. В этом примере используется пароль **password**. В рабочей среде следует использовать надежный пароль. См. статьи [Рекомендации по созданию надежных паролей](http://msdn.microsoft.com/en-us/library/bb416446.aspx) и [Надежные пароли](http://msdn.microsoft.com/en-us/library/ms161962.aspx).</span><span class="sxs-lookup"><span data-stu-id="30b3d-p106">Export the file to a location you choose and give it a password. In this example, the password is **password**. In a production environment, use a strong password. See [Guidelines for creating strong passwords](http://msdn.microsoft.com/en-us/library/bb416446.aspx) and [Strong passwords](http://msdn.microsoft.com/en-us/library/ms161962.aspx).</span></span>
    
 

## <a name="make-your-certificate-the-sts-certificate-for-your-on-premises-installation-of-sharepoint"></a><span data-ttu-id="30b3d-141">Назначение сертификата STS для локальной установки SharePoint</span><span class="sxs-lookup"><span data-stu-id="30b3d-141">Make your certificate the STS certificate for your on-premises installation of SharePoint</span></span>
<span data-ttu-id="30b3d-142"><a name="STSCertificate"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-142"></span></span>

<span data-ttu-id="30b3d-143">Теперь, когда у вас есть сертификат, сделайте его сертификатом STS для своей локальной фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-143">Now that you have a certificate, you make it the STS certificate for your on-premises SharePoint farm.</span></span> 
 

 
<span data-ttu-id="30b3d-144">Откройте командную консоль SharePoint от имени администратора и запустите приведенный ниже скрипт Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30b3d-144">Open the SharePoint Management Shell as an administrator and run this Windows PowerShell script.</span></span>
 

 



```
$certPrKPath = "c:\location of your .pfx file"
$certPassword = "password"
$stsCertificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 $certPrKPath, $certPassword, 20
Set-SPSecurityTokenServiceConfig -ImportSigningCertificate $stsCertificate -confirm:$false

```


 <span data-ttu-id="30b3d-145">**Примечание.** В документе [Настройка односторонней гибридной среды с SharePoint Server 2013 и Office 365](http://download.microsoft.com/download/6/4/4/644BA525-96CB-4739-B08F-18949A9BDADC/sps-2013-config-one-way-hybrid-environment.docx), который можно скачать на [странице гибридных ресурсов SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=35593), подробнее объясняется, как заменить сертификат STS по умолчанию для локальной фермы на сертификат из известного центра сертификации или самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="30b3d-145">**Note** The  [Configure a one-way hybrid environment with SharePoint Server 2013 and Office 365](http://download.microsoft.com/download/6/4/4/644BA525-96CB-4739-B08F-18949A9BDADC/sps-2013-config-one-way-hybrid-environment.docx) document that is available for download on the [SharePoint hybrid resources page](http://www.microsoft.com/en-us/download/details.aspx?id=35593) explains in greater detail how to replace the default STS certificate of your on-premises farm with a certificate from a well-known certification authority or a self-signed certificate.</span></span>
 


## <a name="configure-your-on-premises-installation-of-sharepoint-to-use-acs"></a><span data-ttu-id="30b3d-146">Настройка локальной установки SharePoint на использование службы контроля доступа</span><span class="sxs-lookup"><span data-stu-id="30b3d-146">Configure your on-premises installation of SharePoint to use ACS</span></span>
<span data-ttu-id="30b3d-147"><a name="ConnectAAD"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-147"></span></span>

<span data-ttu-id="30b3d-p107">На рисунке 4 показаны четыре шага, позволяющие разрешить необходимые соединения в рамках всей архитектуры надстройки с размещением у поставщика, которое запускается на локальном сайте. На нем также показаны потоки маркеров OAuth при выполнении надстройки.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p107">Figure 4 shows the four steps to enable the connections you need within the overall architecture of a provider-hosted add-in that runs on an on-premises site. It also shows the flow of OAuth tokens when the add-in is running.</span></span>
 

 

<span data-ttu-id="30b3d-150">**Рис. 4. Настройка службы контроля доступа на работу с локальной установкой SharePoint с помощью сайта SharePoint в Office 365**</span><span class="sxs-lookup"><span data-stu-id="30b3d-150">**Figure 4. Make ACS work with an on-premises installation of SharePoint by using an Office 365 SharePoint site**</span></span>

 

 
![Настройка службы контроля доступа на работу с локальной установкой SharePoint с помощью сайта Office 365](../../images/SP15_OnPremACSArchitecture.png)
 

 

1. <span data-ttu-id="30b3d-152">Создайте прокси-сервер службы контроля доступа в локальной ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-152">Create an ACS proxy in your on-premises SharePoint farm.</span></span>
    
 
2. <span data-ttu-id="30b3d-153">Установите сертификат подписи своего локального сервера на правах аренды Office 365.</span><span class="sxs-lookup"><span data-stu-id="30b3d-153">Install the signing certificate of your on-premises server to your Office 365 tenancy.</span></span>
    
 
3. <span data-ttu-id="30b3d-154">Добавьте полные доменные имена сайтов на своей ферме SharePoint, на которой нужно запускать надстройки, в коллекцию имен субъектов-служб в аренде Office 365.</span><span class="sxs-lookup"><span data-stu-id="30b3d-154">Add the fully qualified domain names of the sites on your SharePoint farm where you want to run add-ins to the service principal name collection in your Office 365 tenancy.</span></span>
    
 
4. <span data-ttu-id="30b3d-155">Создайте прокси-сервер управления надстройками на своей ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-155">Create an add-in management proxy on your SharePoint farm.</span></span>
    
 
<span data-ttu-id="30b3d-p108">Представленная ниже функция выполняет всю настройку локального сайта SharePoint, необходимую для использования службы контроля доступа. С помощью этой функции можно также выполнять действия для удаления предыдущих конфигураций. Запускать функцию PowerShell можно многими способами. Ниже описан один из них.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p108">The function below does all the work to configure your on-premises SharePoint site to use ACS. You can also use this function to do some cleanup tasks if you need to remove previous configurations. There are a variety of ways to run the function in PowerShell. The following is one method:</span></span>
 

 

 

1. <span data-ttu-id="30b3d-p109">На локальном сервере SharePoint скопируйте код из функции в текстовый файл и сохраните его под именем MySharePointFunctions.psm1 в одну из следующих папок (но не в обе). Возможно, понадобится создать части пути, если он содержит папки, которых еще не существует. Обратите внимание, что в обоих случаях папка, находящаяся на самом низком уровне пути, должна иметь то же имя, что и файл.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p109">On the on-premises SharePoint server, copy the code in the function into a text file and save it with the name MySharePointFunctions.psm1 to one or the other of the following folders (not both). You may have to create parts of the path, if it includes folders that do not already exist. Notice that in both cases, the lowest folder in the path has to have the same name as the file.</span></span>
    
     <span data-ttu-id="30b3d-p110">**Совет.** Файл необходимо сохранить в формате ANSI, а не UTF-8. При загрузке файла в формате, отличном от ANSI, в PowerShell могут возникать ошибки синтаксиса. По умолчанию "Блокнот" Windows сохраняет файлы в формате ANSI. Если для сохранения файла используется другой редактор, обязательно выберите формат ANSI.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p110">**TIP** The file has to be saved as ANSI format, not UTF-8. PowerShell may give syntax errors when it loads a file with a non-ANSI format. Windows NotePad will default to saving it as ANSI. If you use any other editor to save the file, be sure you are saving it as ANSI.</span></span>

      -  <span data-ttu-id="30b3d-167">`C:\users\username\documents\windowspowershell\modules\MySharePointFunctions`, где _username_ — это имя администратора фермы, который будет запускать файл.</span><span class="sxs-lookup"><span data-stu-id="30b3d-167">`C:\users\username\documents\windowspowershell\modules\MySharePointFunctions`, where  _username_ is the farm administrator who will be executing the file.</span></span>
    
 
  -  `C:\windows\system32\windowspowershell\V1.0\modules\MySharePointFunctions`
    
 
2. <span data-ttu-id="30b3d-168">Откройте командную консоль SharePoint от имени администратора и выполните приведенный ниже командлет, чтобы убедиться, что модуль MySharePointFunctions добавлен в список.</span><span class="sxs-lookup"><span data-stu-id="30b3d-168">Open the SharePoint Management Shell as an administrator and run the following cmdlet to verify that the MySharePointFunctions module is listed.</span></span>
    
```
  Get-Module -listavailable
```

3. <span data-ttu-id="30b3d-169">Запустите следующий командлет, чтобы импортировать модуль.</span><span class="sxs-lookup"><span data-stu-id="30b3d-169">Run the following cmdlet to import the module.</span></span>
    
```
  Import-Module MySharePointFunctions
```

4. <span data-ttu-id="30b3d-170">Запустите следующий командлет, чтобы убедиться, что функция Connect-SPFarmToAAD входит в модуль.</span><span class="sxs-lookup"><span data-stu-id="30b3d-170">Run the following cmdlet to verify that the Connect-SPFarmToAAD function is listed as part of the module:</span></span>
    
```
  Get-Command -module MySharePointFunctions
```

5. <span data-ttu-id="30b3d-171">Выполните приведенный ниже командлет, чтобы убедиться, что функция Connect-SPFarmToAAD загружена.</span><span class="sxs-lookup"><span data-stu-id="30b3d-171">Run the following cmdlet to verify that the Connect-SPFarmToAAD function is loaded.</span></span>
    
```
  ls function:\ | where {$_.Name -eq "Connect-SPFarmToAAD"}
```

6. <span data-ttu-id="30b3d-p111">Запустите функцию  `Connect-SPFarmToAAD`. Обязательно укажите необходимые параметры и все дополнительные параметры, которые применяются к вашей среде разработки. Подробности и примеры см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p111">Run the  `Connect-SPFarmToAAD` function. Be sure to provide the required parameters and any optional parameters that apply to your developer environment. See the next section for details and examples.</span></span>
    
 

 

 

### <a name="connect-spfarmtoaad-function-parameters"></a><span data-ttu-id="30b3d-175">Параметры функции Connect-SPFarmToAAD</span><span class="sxs-lookup"><span data-stu-id="30b3d-175">Connect-SPFarmToAAD function parameters</span></span>
<span data-ttu-id="30b3d-176"><a name="parameters"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-176"></span></span>



|<span data-ttu-id="30b3d-177">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="30b3d-177">**Parameter**</span></span>|<span data-ttu-id="30b3d-178">**Значение**</span><span class="sxs-lookup"><span data-stu-id="30b3d-178">**Value**</span></span>|
|:-----|:-----|
| <span data-ttu-id="30b3d-179">`-AADDomain` (обязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-179">Required</span></span>|<span data-ttu-id="30b3d-p112">Домен *.onmicrosoft.com, который вы создали при регистрации на своем сайте Office 365 (_ваш_пользовательский_домен_.onmicrosoft.com). Когда появится запрос на проверку подлинности, укажите имя пользователя и пароль, созданные для этого домена: _имя пользователя_@ _ваш_пользовательский_домен_.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p112">The *.onmicrosoft.com domain that you created when you signed up for your off365short site (yourcustomdomain.onmicrosoft.com). When the script prompts you to authenticate, use the user name and password that you created for this domain:  username@yourcustomdomain.onmicrosoft.com.</span></span>|
| <span data-ttu-id="30b3d-182">`-SharePointOnlineUrl` (обязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-182">Required</span></span>|<span data-ttu-id="30b3d-p113">URL-адрес вашего сайта SharePoint в Office 365 (_https://ваш_пользовательский_домен_.sharepoint.com). Обратите внимание, что onmicrosoft.com *не* является родительским доменом.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p113">The URL of your Office 365 SharePoint site ( _https://yourcustomdomain_.sharepoint.com). Note that parent domain is  *not*  onmicrosoft.com.</span></span>|
| <span data-ttu-id="30b3d-185">`-SharePointWeb` (обязательный в некоторых случаях)</span><span class="sxs-lookup"><span data-stu-id="30b3d-185">`-SharePointWeb` (sometimes required)</span></span>|<span data-ttu-id="30b3d-p114">Полный URL-адрес (включая протокол) локального веб-приложения SharePoint, где вы будете запускать надстройки, размещаемые у поставщика. Эта функция добавляет только одно веб-приложение SharePoint из вашей локальной фермы в службу контроля доступа. Если значение этого параметра не указано, сценарий выберет первое веб-приложение из фермы. Если вы используете семейство веб-сайтов с именем узла, которое можно определить с помощью подстановочного знака (например, _http://*.contoso.com_), то эту строку можно использовать в качестве значения данного параметра. Если в веб-приложении используется альтернативное сопоставление доступа для зоны Интернета, то для данного параметра необходимо использовать его URL-адрес. Если веб-приложение SharePoint не настроено для протокола HTTPS, необходимо использовать протокол HTTP и *параметр командной строки -AllowOverHttp (см. ниже в этой таблице).* Если вы хотите запускать надстройки с размещением у поставщика, использующие ACS в нескольких веб-приложениях фермы, их потребуется добавить в коллекцию имен субъектов-служб. Приведенный ниже скрипт Windows PowerShell, использующий функцию `Connect-SPFarmToAAD`, иллюстрирует добавление всех веб-приложений фермы в коллекцию имен субъектов-служб.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p114">The full URL (including protocol) of the on-premises SharePoint web application where you'll run provider-hosted add-ins. This function adds only one SharePoint web application from your on-premises farm to ACS. If you don't specify a value for this, the script selects the first web application in your farm. If you're using a Host Name Site Collection (HNSC) that can be defined with a wildcard (such as  _http://*.contoso.com_), you can use that string as the value for this parameter. If the web application has an alternative access mapping (AAM) for the Internet zone, you must use that AAM URL for this parameter. If the SharePoint web application is not configured for HTTPS, you have to use HTTP as the protocol and  *you have to use the -AllowOverHttp switch (see below in this table).*</span></span>|
| <span data-ttu-id="30b3d-194">`-AllowOverHttp` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-194">`-AllowOverHttp` (optional)</span></span>|<span data-ttu-id="30b3d-p115">Используйте этот параметр командной строки, если вы работаете со средой разработки и не хотите использовать SSL для своих надстроек. Его необходимо использовать, если веб-приложение SharePoint не настроено для протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p115">Use this switch if you're working with a developer environment and don't want to use SSL with your add-ins. You have to use this switch if the SharePoint web application is not configured for HTTPS.</span></span>|
| <span data-ttu-id="30b3d-197">`-O365Credentials` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-197">`-O365Credentials` (optional)</span></span>|<span data-ttu-id="30b3d-p116">Первый символ — это прописная буква "O", а не ноль. Если вам придется много раз запускать скрипт для выполнения отладки, используйте этот параметр командной строки, чтобы каждый раз не вводить имя и пароль для Office 365 вручную. Прежде чем использовать этот параметр, необходимо создать объект учетных данных, который вы назначите ему с помощью следующих командлетов: ```$User = "username@yourcustomdomain.onmicrosoft.com"$PWord = ConvertTo-SecureString -String "the_password" -AsPlainText -Force$Credential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $PWord``` Используйте значение `$Credential` для параметра `-O365Credentials`.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p116">The first character is a capital "O", not a zero. If you find yourself repeatedly running the script for debugging purposes, this switch enables to you avoid having to manually enter your O365 name and password each time. Before you can use this parameter, you must create the credentials object that you will assign to it with these cmdlets:</span></span>|
| <span data-ttu-id="30b3d-201">`-Verbose` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-201">`-Verbose` (optional)</span></span>|<span data-ttu-id="30b3d-202">Этот параметр командной строки создает более подробный отчет, который может быть полезен, если функция не работает и нужно повторно запустить ее для отладки.</span><span class="sxs-lookup"><span data-stu-id="30b3d-202">This switch generates more detailed feedback which might help if the function is not working and you need to rerun it for debugging.</span></span>|
| <span data-ttu-id="30b3d-203">`-RemoveExistingACS` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-203">`-RemoveExistingACS` (optional)</span></span>|<span data-ttu-id="30b3d-p117">Используйте этот параметр командной строки, если вы заменяете существующее подключение к Microsoft Azure Active Directory. Это приведет к замене существующего прокси-сервера службы контроля доступа, если он уже создан на вашей ферме.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p117">Use this switch if you're replacing an existing connection to Microsoft Azure Active Directory. It removes an existing ACS proxy if you've already created one on your farm.</span></span>|
| <span data-ttu-id="30b3d-206">`-RemoveExistingSTS` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-206">`-RemoveExistingSTS` (optional)</span></span>|<span data-ttu-id="30b3d-p118">Используйте этот параметр командной строки, если вы заменяете существующее подключение к Microsoft Azure Active Directory. Он удалит существующего издателя маркеров безопасности, который остался от предыдущего подключения к службе контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p118">Use this switch if you're replacing an existing connection to Microsoft Azure Active Directory. It removes an existing trusted security token issuer that is left over from an earlier connection to ACS.</span></span>|
| <span data-ttu-id="30b3d-209">`-RemoveExistingSPOProxy` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-209">`-RemoveExistingSPOProxy` (optional)</span></span>|<span data-ttu-id="30b3d-p119">Используйте этот параметр командной строки, если вы заменяете существующее подключение к Microsoft Azure Active Directory. Это приведет к замене существующего прокси-сервера управления надстройками, если он уже создан на вашей ферме.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p119">Use this switch if you're replacing an existing connection to Microsoft Azure Active Directory. It removes an existing add-in management proxy if you've already created one on your farm.</span></span>|
| <span data-ttu-id="30b3d-212">`-RemoveExistingAADCredentials` (необязательный)</span><span class="sxs-lookup"><span data-stu-id="30b3d-212">`-RemoveExistingAADCredentials` (optional)</span></span>|<span data-ttu-id="30b3d-213">Используйте этот параметр командной строки, если вы заменяете сайт SharePoint в Office 365.</span><span class="sxs-lookup"><span data-stu-id="30b3d-213">Use this switch if you're replacing the Office 365 SharePoint site.</span></span>|
<span data-ttu-id="30b3d-214">Примеры.</span><span class="sxs-lookup"><span data-stu-id="30b3d-214">The following are examples:</span></span>
 

 

```
Connect-SPFarmToAAD -AADDomain 'MyO365Domain.onmicrosoft.com' -SharePointOnlineUrl https://MyO365Domain.sharepoint.com

Connect-SPFarmToAAD -AADDomain 'MyO365Domain.onmicrosoft.com' -SharePointOnlineUrl https://MyO365Domain.sharepoint.com -SharePointWeb https://fabrikam.com

Connect-SPFarmToAAD -AADDomain 'MyO365Domain.onmicrosoft.com' -SharePointOnlineUrl https://MyO365Domain.sharepoint.com -SharePointWeb http://northwind.com -AllowOverHttp

Connect-SPFarmToAAD -AADDomain 'MyO365Domain.onmicrosoft.com' -SharePointOnlineUrl https://MyO365Domain.sharepoint.com -SharePointWeb http://northwind.com -AllowOverHttp -RemoveExistingACS -RemoveExistingSTS -RemoveExistingSPOProxy -RemoveExistingAADCredentials

```


### <a name="connect-spfarmtoaad-function-script"></a><span data-ttu-id="30b3d-215">Скрипт с функцией Connect-SPFarmToAAD</span><span class="sxs-lookup"><span data-stu-id="30b3d-215">Connect-SPFarmToAAD function script</span></span>
<span data-ttu-id="30b3d-216"><a name="function"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-216"></span></span>


```

function Connect-SPFarmToAAD {
param(
    [Parameter(Mandatory)][String]   $AADDomain,
    [Parameter(Mandatory)][String]   $SharePointOnlineUrl,
    #Specify this parameter if you don't want to use the default SPWeb returned
    [Parameter()][String]            $SharePointWeb,
    [Parameter()][System.Management.Automation.PSCredential] $O365Credentials,
    #Use these switches if you're replacing an existing connection to AAD.
    [Parameter()][Switch]            $RemoveExistingACS,
    [Parameter()][Switch]            $RemoveExistingSTS,
    [Parameter()][Switch]            $RemoveExistingSPOProxy,
    #Use this switch if you're replacing the Office 365 SharePoint site.
    [Parameter()][Switch]            $RemoveExistingAADCredentials,
    #Use this switch if you don't want to use SSL when you launch your app.
    [Parameter()][Switch]            $AllowOverHttp
)
    #Prompt for credentials right away.
    if (-not $O365Credentials) {
        $O365Credentials = Get-Credential -Message "Admin credentials for $AADDomain"
    }
    Add-PSSnapin Microsoft.SharePoint.PowerShell
    #Import the Microsoft Online Services Sign-In Assistant.
    Import-Module -Name MSOnline
    #Import the Microsoft Online Services Module for Windows Powershell.
    Import-Module MSOnlineExtended -force -verbose 
    #Set values for Constants.
    New-Variable -Option Constant -Name SP_APPPRINCIPALID -Value '00000003-0000-0ff1-ce00-000000000000' | Out-Null
    New-Variable -Option Constant -Name ACS_APPPRINCIPALID -Value '00000001-0000-0000-c000-000000000000' | Out-Null
    New-Variable -Option Constant -Name ACS_APPPROXY_NAME -Value ACS
    New-Variable -Option Constant -Name SPO_MANAGEMENT_APPPROXY_NAME -Value 'SPO Add-in Management Proxy'
    New-Variable -Option Constant -Name ACS_STS_NAME -Value ACS-STS
    New-Variable -Option Constant -Name AAD_METADATAEP_FSTRING -Value 'https://accounts.accesscontrol.windows.net/{0}/metadata/json/1'
    New-Variable -Option Constant -Name SP_METADATAEP_FSTRING -Value '{0}/_layouts/15/metadata/json/1'
    #Get the default SPWeb from the on-premises farm if no $SharePointWeb parameter is specified.
    if ([String]::IsNullOrEmpty($SharePointWeb)) {
        $SharePointWeb = Get-SPSite | Select-Object -First 1 | Get-SPWeb | Select-Object -First 1 | % Url
    }

    #Configure the realm ID for local farm so that it matches the AAD realm.
    $ACSMetadataEndpoint = $AAD_METADATAEP_FSTRING -f $AADDomain
    $ACSMetadata = Invoke-RestMethod -Uri $ACSMetadataEndpoint
    $AADRealmId = $ACSMetadata.realm

    Set-SPAuthenticationRealm -ServiceContext $SharePointWeb -Realm $AADRealmId
    
    $LocalSTS = Get-SPSecurityTokenServiceConfig
    $LocalSTS.NameIdentifier = '{0}@{1}' -f $SP_APPPRINCIPALID,$AADRealmId
    $LocalSTS.Update()

    #Allow connections over HTTP if the switch is specified.
    if ($AllowOverHttp.IsPresent -and $AllowOverHttp -eq $True) {
        $serviceConfig = Get-SPSecurityTokenServiceConfig
        $serviceConfig.AllowOAuthOverHttp = $true
        $serviceConfig.AllowMetadataOverHttp = $true
        $serviceConfig.Update()
    }

    #Step 1: Set up the ACS proxy in the on-premises SharePoint farm. Remove the existing ACS proxy
    #if the switch is specified.
    if ($RemoveExistingACS.IsPresent -and $RemoveExistingACS -eq $True) {
        Get-SPServiceApplicationProxy | ? DisplayName -EQ $ACS_APPPROXY_NAME | Remove-SPServiceApplicationProxy -RemoveData -Confirm:$false
    }
    if (-not (Get-SPServiceApplicationProxy | ? DisplayName -EQ $ACS_APPPROXY_NAME)) {
        $AzureACSProxy = New-SPAzureAccessControlServiceApplicationProxy -Name $ACS_APPPROXY_NAME -MetadataServiceEndpointUri $ACSMetadataEndpoint -DefaultProxyGroup
    }

    #Remove the existing security token service if the switch is specified.
    if ($RemoveExistingSTS.IsPresent) {
        Get-SPTrustedSecurityTokenIssuer | ? Name -EQ $ACS_STS_NAME | Remove-SPTrustedSecurityTokenIssuer -Confirm:$false
    }
    if (-not (Get-SPTrustedSecurityTokenIssuer | ? DisplayName -EQ $ACS_STS_NAME)) {
        $AzureACSSTS = New-SPTrustedSecurityTokenIssuer -Name $ACS_STS_NAME -IsTrustBroker -MetadataEndPoint $ACSMetadataEndpoint
    }

    #Update the ACS Proxy for OAuth authentication.
    $ACSProxy = Get-SPServiceApplicationProxy | ? Name -EQ $ACS_APPPROXY_NAME
    $ACSProxy.DiscoveryConfiguration.SecurityTokenServiceName = $ACS_APPPRINCIPALID
    $ACSProxy.Update()

    #Retrieve the local STS signing key from JSON metadata.
    $SPMetadata = Invoke-RestMethod -Uri ($SP_METADATAEP_FSTRING -f $SharePointWeb)
    $SPSigningKey = $SPMetadata.keys | ? usage -EQ "Signing" | % keyValue
    $CertValue = $SPSigningKey.value
    
    #Connect to Office 365.
    Connect-MsolService -Credential $O365Credentials
    #Remove existing connection to an Office 365 SharePoint site if the switch is specified.
    if ($RemoveExistingAADCredentials.IsPresent -and $RemoveExistingAADCredentials -eq $true) {
        $msolserviceprincipal = Get-MsolServicePrincipal -AppPrincipalId $SP_APPPRINCIPALID
        [Guid[]] $ExistingKeyIds = Get-MsolServicePrincipalCredential -ObjectId $msolserviceprincipal.ObjectId -ReturnKeyValues $false | % {if ($_.Type -ne "Other") {$_.KeyId}}
        Remove-MsolServicePrincipalCredential -AppPrincipalId $SP_APPPRINCIPALID -KeyIds $ExistingKeyIds
    }
    #Step 2: Upload the local STS signing certificate
    New-MsolServicePrincipalCredential -AppPrincipalId $SP_APPPRINCIPALID -Type Asymmetric -Value $CertValue -Usage Verify

    #Step 3: Add the service principal name of the local web application, if necessary.
    $indexHostName = $SharePointWeb.IndexOf('://') + 3
    $HostName = $SharePointWeb.Substring($indexHostName)
    $NewSPN = '{0}/{1}' -f $SP_APPPRINCIPALID, $HostName
    $SPAppPrincipal = Get-MsolServicePrincipal -AppPrincipalId $SP_APPPRINCIPALID
    if ($SPAppPrincipal.ServicePrincipalNames -notcontains $NewSPN) {
        $SPAppPrincipal.ServicePrincipalNames.Add($NewSPN)
        Set-MsolServicePrincipal -AppPrincipalId $SPAppPrincipal.AppPrincipalId -ServicePrincipalNames $SPAppPrincipal.ServicePrincipalNames
    }

    #Remove the existing SharePoint Online proxy if the switch is specified.
    if ($RemoveExistingSPOProxy.IsPresent -and $RemoveExistingSPOProxy -eq $True) {
        Get-SPServiceApplicationProxy | ? DisplayName -EQ $SPO_MANAGEMENT_APPPROXY_NAME | Remove-SPServiceApplicationProxy -RemoveData -Confirm:$false
    }
    #Step 4: Add the SharePoint Online proxy
    if (-not (Get-SPServiceApplicationProxy | ? DisplayName -EQ $SPO_MANAGEMENT_APPPROXY_NAME)) {
        $spoproxy = New-SPOnlineApplicationPrincipalManagementServiceApplicationProxy -Name $SPO_MANAGEMENT_APPPROXY_NAME -OnlineTenantUri $SharePointOnlineUrl -DefaultProxyGroup
    }  
}
```


### <a name="configure-the-add-in-and-the-sharepoint-web-application-for-the-office-store"></a><span data-ttu-id="30b3d-217">Конфигурация надстройки и веб-приложения SharePoint для Магазина Office</span><span class="sxs-lookup"><span data-stu-id="30b3d-217">Configure the add-in and the SharePoint web application for the Office Store</span></span>
<span data-ttu-id="30b3d-218"><a name="function"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-218"></span></span>

<span data-ttu-id="30b3d-p120">Если администраторы ферм хотят, чтобы пользователи могли устанавливать размещенные у поставщика надстройки, использующие службу контроля доступа в Магазин Office, существует дополнительный шаг настройки, который необходимо выполнить в производственных средах (в среде разработки SharePoint это нецелесообразно, если вы не планируете устанавливать надстройки, использующие службу контроля доступа, из хранилища в такой среде). Приведенный ниже командлет выполняет такое действие. Этот код можно добавить в функцию выше.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p120">There is an optional configuration step that farm administrators should take on production environments, if they want users to be able to install provider-hosted add-ins that use ACS from the Office Store. (It serves no purpose on your SharePoint development environment unless you plan to install add-ins that use ACS from the store on that environment.) The following cmdlet makes this possible. This code can be added to the function above.</span></span>
 

 

```
New-SPMarketplaceWebServiceApplicationProxy -Name "ApplicationIdentityDataWebServiceProxy" -ServiceEndpointUri "https://oauth.sellerdashboard.microsoft.com/ApplicationIdentityDataWebService.svc" -DefaultProxyGroup

```

<span data-ttu-id="30b3d-p121">Для готовых веб-приложений SharePoint рекомендуем активировать компонент **Надстройки, которым требуются подключенные к Интернету конечные точки** после выполнения вышеописанный действий (см. приведенные ниже инструкции). Этот компонент на самом деле не выполняет никаких действий. Он просто выполняет роль флажка, сообщающего Магазину Office, что размещенные у поставщика надстройки, использующие службу контроля доступа, можно устанавливать на веб-сайты в веб-приложении SharePoint.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p121">It is also a good practice on production SharePoint web applications to activate the **Add-ins that require accessible internet facing endpoints** Feature after the configuration steps above have been completed. (See the instructions below.) This Feature does not actually do anything. It simply serves as a flag that tells the Office Store that provider-hosted add-ins that use ACS can be installed on websites in the SharePoint web application.</span></span>
 

 
<span data-ttu-id="30b3d-p122">Такая система может повлиять на манифест надстройки SharePoint. Если вы планируете продавать вашу надстройку в магазине, рекомендуем добавить следующий параметр **AppPrerequiste** в раздел **AppPrerequisites** манифеста надстройки:</span><span class="sxs-lookup"><span data-stu-id="30b3d-p122">This system may have implications for the add-in manifest of your SharePoint Add-in. If you plan to sell your add-in through the store, it is a good practice to add the following **AppPrerequiste** to the **AppPrerequisites** section of the add-in manifest:</span></span>
 

 



```
<AppPrerequisite Type="Feature" ID="{7877bbf6-30f5-4f58-99d9-a0cc787c1300}" />
```

<span data-ttu-id="30b3d-p123">Благодаря этому, когда пользователи просматривают магазин из локальной фермы SharePoint, ваша надстройка не будет доступна для установки, если для родительского веб-приложения SharePoint не включен компонент **Надстройки, которым требуются подключенные к Интернету конечные точки**. Это гарантирует, что вы не будете получать жалобы от пользователей, которые устанавливают вашу надстройку на локальный веб-сайт SharePoint и не могут ее использовать.</span><span class="sxs-lookup"><span data-stu-id="30b3d-p123">The effect of the prerequisite is that when users are browsing the store from an on-premises SharePoint farm, your add-in will be grayed-out and uninstallable when the parent SharePoint web application does not have the **Add-ins that require accessible internet facing endpoints** Feature enabled. This ensures that you won't get complaints from customers who install your add-in to an on-premises SharePoint website and find that it does not work.</span></span>
 

 
<span data-ttu-id="30b3d-p124">Функцию можно активировать двумя способами. Вы можете запустить приведенный ниже командлет PowerShell (который можно добавить в конец функции выше) на любом сервере SharePoint:</span><span class="sxs-lookup"><span data-stu-id="30b3d-p124">There are two ways to enable the Feature. The first is to run the following PowerShell cmdlet (which can be added to the end of the function above) on any SharePoint server:</span></span>
 

 



```
Enable-SPFeature -identity "7877bbf6-30f5-4f58-99d9-a0cc787c1300" -Url http://domain_of_the_SharePoint_web_application
```

<span data-ttu-id="30b3d-231">Чтобы запустить функцию, вы также можете выполнить указанные ниже действия в центре администрирования.</span><span class="sxs-lookup"><span data-stu-id="30b3d-231">The other way to enable the Feature is carry out the following steps in Central Administration:</span></span>
 

 

1. <span data-ttu-id="30b3d-232">В **Центре администрирования SharePoint** перейдите в раздел **Управление приложениями | Управление веб-приложениями**.</span><span class="sxs-lookup"><span data-stu-id="30b3d-232">In **SharePoint Central Administration**, navigate to **Application Management | Manage web applications**.</span></span>
    
 
2. <span data-ttu-id="30b3d-233">На странице **Управление веб-приложениями** выберите веб-приложение, которое требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="30b3d-233">On the **Manage Web Applications** page, select the web application that you want to change.</span></span>
    
 
3. <span data-ttu-id="30b3d-234">На ленте нажмите **Управление компонентами**.</span><span class="sxs-lookup"><span data-stu-id="30b3d-234">On the ribbon, click **Manage Features**.</span></span>
    
 
4. <span data-ttu-id="30b3d-235">В списке компонентов рядом со строкой **Надстройки, которым требуются подключенные к Интернету конечные точки** нажмите кнопку **Активировать**.</span><span class="sxs-lookup"><span data-stu-id="30b3d-235">In the feature list, next to **Add-ins that require accessible internet facing endpoints**, click **Activate**.</span></span>
    
 
5. <span data-ttu-id="30b3d-236">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="30b3d-236">Click **OK**.</span></span>
    
 

 

 

### <a name="configure-additional-sharepoint-web-applications-within-the-farm"></a><span data-ttu-id="30b3d-237">Настройка дополнительных веб-приложений SharePoint в ферме</span><span class="sxs-lookup"><span data-stu-id="30b3d-237">Configure additional SharePoint web applications within the farm</span></span>
<span data-ttu-id="30b3d-238"><a name="function"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-238"></span></span>

<span data-ttu-id="30b3d-239">Если на вашей ферме SharePoint есть дополнительные веб-приложения и вы хотите запускать на них надстройки с размещением у поставщика, использующие доверие службы контроля доступа, с помощью этого сценария Windows PowerShell (в Командная консоль SharePoint) вы можете добавить их в коллекцию имен субъектов службы.</span><span class="sxs-lookup"><span data-stu-id="30b3d-239">If you have additional web applications on your SharePoint farm and you want to run provider-hosted add-ins that use ACS trust on them, you can use this Windows PowerShell script (in the SharePoint Management Shell) to add them to the service principal name collection.</span></span>
 

 

```
$SPAppPrincipal = Get-MsolServicePrincipal -AppPrincipalId 00000003-0000-0ff1-ce00-000000000000
$id = "00000003-0000-0ff1-ce00-000000000000/"

Get-SPWebApplication | ForEach-Object {
    $hostName = $_.Url.substring($_.Url.indexof("//") + 2)
    $hostName = $hostName.Remove($hostName.Length - 1, 1)

    $NewSPN = $id + $hostName

    Write-Host "Adding SPN for" $NewSPN

    if ($SPAppPrincipal.ServicePrincipalNames -notcontains $NewSPN) {
       $SPAppPrincipal.ServicePrincipalNames.Add($NewSPN)
       Set-MsolServicePrincipal -AppPrincipalId $SPAppPrincipal.AppPrincipalId -ServicePrincipalNames $SPAppPrincipal.ServicePrincipalNames
    }
}

```


## <a name="next-steps"></a><span data-ttu-id="30b3d-240">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30b3d-240">Next Steps</span></span>
<span data-ttu-id="30b3d-241"><a name="CreateApp"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-241"></span></span>

<span data-ttu-id="30b3d-242">Выполните действия, описанные в статье  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins), чтобы создать простую надстройку Hello World с размещением у поставщика, которая использует службу контроля доступа в качестве издателя маркеров.</span><span class="sxs-lookup"><span data-stu-id="30b3d-242">Follow the steps in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins) to create a simple "hello world" provider-hosted add-in that uses ACS as the token issuer.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="30b3d-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="30b3d-243">Additional resources</span></span>
<span data-ttu-id="30b3d-244"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="30b3d-244"></span></span>


-  [<span data-ttu-id="30b3d-245">Авторизация и проверка подлинности надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="30b3d-245">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
