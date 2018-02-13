# <a name="introduction"></a>Введение
Большая часть SharePoint Online клиентов значками open работу в файл с помощью **строго** модели. В результате все файлы, которые потенциально могут вызывать вред (например HTML-файл, внедренный сценарий) не выполняются в браузере, но загружается или отображаться в виде необработанное содержимое (Предварительный просмотр HTML-код в современном пользовательского интерфейса). Если клиент настроен с помощью **Нестрогое** модель взаимодействия открыть файл будет выполняться файла, например получение выполняется HTML-файла в библиотеке документов и страница отображается в браузере. В strict этого файла будут загружены.

Сегодня по умолчанию строгие и вы уже не могут переключиться вашего клиента для разрешительной модели. Для клиентов, которым переключения, чтобы Нестрогое из прошлых элементов изменит: Нестрогое модель клиента является устаревшим, в этот момент всех клиентов переключается в strict.


# <a name="is-my-tenant-impacted"></a>Мои клиента на которые оказывает?
Для этого рекомендуется, установив параметр PermissiveBrowserFileHandlingOverride, с помощью [Office 365 PowerShell для SharePoint Online](https://technet.microsoft.com/en-us/library/fp161362.aspx):

```PowerShell
Connect-SPOService -url https://contoso-admin.sharepoint.com
$tenant = get-spotenant
$tenant.PermissiveBrowserFileHandlingOverride
```

Если это приводит к **значение False,** затем вашего клиента это не повлияет на, если задано значение **True,** а затем необходимо подготовить предстоящие прекратить. 

# <a name="how-can-i-prepare-for-changing-permissive-into-strict"></a>Как подготовить для изменения разрешений в strict

![Показывает Нестрогое strict модели](media/permissivetostrictmodel.png)

## <a name="step-1-assess-the-impact"></a>Шаг 1: Оценить влияние
Общие сведения о относится какие файлы — это первый шаг и вы можете сделать это с помощью сканера Нестрогое файлов. В разделе [Нестрогое сканера SharePoint](https://github.com/SharePoint/PnP-Tools/tree/master/Solutions/SharePoint.PermissiveFile.Scanner) для получения дополнительных сведений о сканер и способы его использования. В конфигурации по умолчанию в этом сканера ищет файлы html/html, но с помощью параметров командной строки можно запросить сканера для поиска дополнительных типов файлов.

В результате сканер является CSV-файла, где перечислены все задействованной (html/htm + необязательно других типов файлов) файлов, в том числе сведения о html/htm-файлы (число ссылок и сценарии, которые используются, последнего изменения данных, количество просмотров).

## <a name="step-2-analyze-the-scan-results"></a>Этап 2: Анализ результатов проверки
После списка задействованной файлов необходимо оценить которого, если эти файлы и сайты, использующие эти файлы, соответствующие по-прежнему business. Файл и/или сайт может быть устарели, а если so исправлению эти файлы/сайты могут быть пропущены. Чтобы помочь вам с Общие сведения об отчете потребностей бизнеса содержит Администраторы семейства сайтов и владельцев сайтов, предоставляя необходимые сведения для контактов.

## <a name="step-3-remediate-the-files"></a>Шаг 3: Устранение файлы
Если файлы по-прежнему важны и необходимо иметь возможность выполнять файлы после клиента была перемещена в strict параметр по-прежнему, необходимо исправить файлы, как описано в следующей главы. 

# <a name="remediation-process-for-htmlhtm-files"></a>Процесс обновления для html/htm-файлы
Основная причина клиентам использовать именно Нестрогое режима является, поскольку они хотят иметь возможность использовать HTML-файлы из внутри библиотеки документов. Как уже было сказано, прежде чем после перемещения в strict эти файлы будут просто загрузить и автоматически открывать больше.
Для этих файлов html/html исправлению простой: Если пользователь/приложение с разрешениями администратора семейства сайтов или владельца веб-сайта имени html/htm-файлы на ASPX-файлы, затем снова открыть эти файлы. Ниже отображает [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) как это можно сделать. Предположим, что HTML-файл с следующий URL-адрес: https://contoso.sharepoint.com/sites/permissive/html/newfile.html. 

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Rename-PnPFile -ServerRelativeUrl /sites/permissive/html/newfile.html -TargetFileName newfile.aspx -OverwriteIfAlreadyExists
```

Более поздней версии для будут отображаться в этой статье скрипта, который можно выполнить полную «исправления» для всего семейства сайтов.

## <a name="who-can-perform-this-rename"></a>Кто может выполнять переименуйте?
Переименование должен выполнить пользователи, имеющие разрешение AddAndCustomizePages (ACP), который по умолчанию предоставляется владельцы сайтов или администраторы семейств сайтов. Если rename выполняется с пользователя с помощью измените уровень разрешений (так участники сайта) затем осуществляется rename, однако результирующую ASPX-файл не помеченных для выполнения и таким образом будет загружена и не выполнена. 

Если вы собираетесь выполнить массовое переименование скорее всего, будет использоваться субъект приложения вместо учетной записи пользователя и то же применяется: участника приложения должны быть разрешения ACP (например уровнем разрешений полный доступ) этой функции необходимо выполнение.

## <a name="what-about-embedded-links-to-other-htmlhtm-files"></a>Как насчет внедренные ссылки на другие файлы html/htm?
Мои ссылки файлы html/htm для других html/htm-файлы в той же папке или во вложенной папке... будет эти ссылки не работают, если файлы переименовываются aspx? Если базовый переименовать выполняется с помощью вызов MoveTo API, а затем большая часть относительные ссылки в файле html автоматически исправленные быть ссылки на файлы aspx по сути переименование структура вложенных html/htm-файлы, которые связь друг с другом можно сделать, только Переименование файлов, все ссылки внутри документы будут обрабатываться rename.

> [!NOTE]
> Автоматическое переименование не работает, если HTML-документ ссылок, указывающих файлы в другом семействе сайтов или когда ссылки динамически создаются с помощью JavaScript. В таких случаях вручную действия необходимы для исправления ссылок.

## <a name="what-about-htmlhtml-files-referenced-in-a-content-editor-web-part"></a>Как насчет html/HTML-файлы по ссылке в веб-части редактора контента?
Общий шаблон при работе с веб-части редактора контента ссылается на файл html/htm. При переименовании файлов html/htm, на который указывает ссылка ASPX-файл, а затем SharePoint будет автоматически также обновите ссылку в веб-части редактора контента, что по состоянию на этот момент означает, что веб-часть редактора контента будут загружать ASPX-файл вместо html/htm-файл. Чтобы переименовать файлы, используемые на веб-части редактора контента можно совместно с другими файлы html/htm.

## <a name="what-about-sites-having-the-noscript-feature-enabled"></a>Какие сведения о сайтах с включенным средством «noscript»
Все сайты «Современный» (современных группового сайта, сайт связи) имеют функцию «noscript» включен по умолчанию. Таким образом, что никто не имеет разрешение AddAndCustomizePages (ACP), чтобы никто можно выполнить успешное переименовать из html/htm для aspx. Как правило html/htm-файлы live в веб-сайтов (перенесенных) классический групп этой проблемы не существует. В случае, используемого на сайте «noscript» вам потребуются для первого отключить функцию «noscript», выполнить операции и затем снова включить «noscript». В результате html/htm-файлы могут быть выполнены еще раз, но Обратите внимание на то, что каждого изменения на эти файлы будут помечены не исполняемый файл еще раз. Отключение «noscript» еще раз и обновление файла будет обрабатывать это.

## <a name="in-the-modern-document-library-experience-the-aspx-file-initially-do-not-seem-to-open"></a>В работу библиотеки документов современных файла aspx изначально не вступают в откройте?
Работу библиотеки документов современных «предполагается» определенного типа файлов после добавления файла и при доступе к файлу в первый раз вы увидите, что aspx-файлы открываются неправильно. Тем не менее второй попытки выполнения файла. Избегайте введите этой проблемы рекомендуется выполнить программными средствами раскрывающемся каждого переименованный файл один раз, что дает возможность правильно установить файл SharePoint. Ниже отображает [SharePoint PnP PowerShell](https://aka.ms/sppnp-powershell) как это можно сделать:

```PowerShell
Connect-PnPOnline -Url https://contoso.sharepoint.com/sites/permissive -Verbose
Get-PnPFile -Url /sites/permissive/html/newfile.aspx -Path c:\temp -Filename newfile.aspx -AsFile
```

> [!NOTE]
> Это действие «загрузить» включен в скрипт, который может выполнять полный «исправления» для всего семейства сайтов.

# <a name="remediation-of-other-file-types"></a>Исправление других типов файлов
HTML/htm-файлы должны использовать режим разрешений, но что о других типов файлов основные причины для клиентов? Для многих распространенных форматов файлов SharePoint Online предоставляют возможность просмотра как описано в этом [блоге](https://techcommunity.microsoft.com/t5/OneDrive-for-Business/Announcing-New-File-Viewers-Available-for-OneDrive-For-Business/td-p/60040). SharePoint Online можно выполнить предварительный просмотр следующих форматов:

## <a name="documents"></a>Документы
CSV, doc, docm, docx, dotx, eml, сообщение, odp, программ ods odt, pdf, pot, potm, potx, pps, ppsx, ppt, pptm, pptx, rtf, vsd, vsdx, xls, xlsb, xlsm, xlsx

## <a name="images"></a>изображения;
AI, arw, bmp, cr2, eps, erf, gif, ico, значок, jpeg, jpg, mrw, nef, orf, pict, png, psd, временных файлов Интернета, tiff

## <a name="video"></a>Видео
3GP, m4v, mov, MP4 (en), wmv

## <a name="3d"></a>3D
3mf, fbx, obj, лист, stl

## <a name="medical"></a>Медицинского обслуживания
DCM dcm30, dic, dicm, dicom

## <a name="text-and-code"></a>Текст и кода
abap, ada, adp, ahk как, as3, asc, ascx, asm, asp, awk, bash, bash_login, bash_logout, bash_profile, bashrc, bat, списка литературы, bsh, построения, построитель, c, c ++ capfile, cc, cfc, куб, cfml, cl, clj, cls, cmake, cmd, кофе, cpp, cpt, cpy, cs, cshtml, cson, csproj, css, CTP-версия , cxx, d, ddl, di, dif, копирования, disco, dml, dtd, dtml, el, emakefile, erb, erl, f, f90, f95, федерации Active Directory, ФСС, fsscript, fsx, gemfile, gemspec, gitconfig, последовательно выберите, хорошую, gvy, h, h ++ (en), haml, рули, hbs, hcp, hh, hpp, hrl, hs, htc, hxx, idl, iim, inc, inf, ini, inl, ipp , irbrc, jade, jav, java, js, jsp, jsx, l меньше lhs, lisp, журнала, lst, ltx, lua, m, сделать, markdn, наценки, md, mdown, mkdn, ml, mli, mll, mly, мм, лиственный, nfo, opml, osascript выходной параметр p, pas, исправление, php, php2, php3, php4, php5, phtml, pl, plist, pm, модуль, pp , профиля, свойства, ps1, pt, копировать, pyw, r, rake, rb, rbx, rc, re readme, reg, rest, resw, resx, rhtml, rjs, rprofile, rpy, RSS-канал, rst, rxml, s, sass, scala, диспетчер управления службами, sconscript, sconstruct, скрипт, scss, sgml, показывать, shtml, sml, sql, Стилисти, tcl, tex, текст, textile, доменов верхнего уровня, tli, шаблон, библиотека параллельных задач, txt, vb, vi, vim, WSDL-файлу, xhtml, xml, xoml, xsd, xsl, xslt, yaml, yaws, yml, zip, zsh

# <a name="sample-script-that-can-remediate-a-complete-site-collection"></a>Пример сценария, который можно Устранение всего семейства сайтов
Этот сценарий можно использовать в качестве отправной основы коррекции уровня семейства сайтов. Скрипт будет выполните следующие действия.
- Установка PnP PowerShell, если еще не установлены
- Поиск всех html/htm-файлы в коллекции веб-сайтов
- Переименуйте эти файлы в .aspx
- Загрузить переименованный файл, чтобы включить его для работы на первый доступа в пользовательском интерфейсе современных документов библиотеки


```PowerShell
# This script does rename .htm and .html files to .aspx files. Doing so enables these files to be "executed" in SharePoint Online 
# which has it's file handling configured to be strict. See https://docs.microsoft.com/en-us/sharepoint/dev/solution-guidance/security-permissivesetting 
# for more details

function PermissiveRemediateASiteCollection
{
    param([string] $siteCollectionUrl, [string] $winCredentialsManagerLabel)
    
    $siteCollectionUrl = $siteCollectionUrl.TrimEnd("/");

    # Gets or Sets the tenant admin credentials.
    $credentials = $null

    if(![String]::IsNullOrEmpty($winCredentialsManagerLabel) -and (Get-PnPStoredCredential -Name $winCredentialsManagerLabel) -ne $null)
    {
        $credentials = $winCredentialsManagerLabel
    }
    else
    {
        # Prompts for credentials, if not found in the Windows Credential Manager.
        $email = Read-Host -Prompt "Please enter admin email"
        $pass = Read-host -AsSecureString "Please enter admin password"
        $credentials = New-Object –TypeName "System.Management.Automation.PSCredential" –ArgumentList $email, $pass
    }

    if($credentials -eq $null) 
    {
        Write-Host "Error: No credentials supplied." -ForegroundColor Red
        exit 1
    }

    Connect-PnPOnline -Url $siteCollectionUrl -Credentials $credentials -Verbose

    Write-Host "Using search to obtain a list of files to remediate..."
    Try
    {
        $searchQuery = "((fileextension=htm OR fileextension=html) AND contentclass=STS_ListItem_DocumentLibrary AND Path:$siteCollectionUrl/*)"
        $htmlFiles = Submit-PnPSearchQuery -Query $searchQuery -TrimDuplicates:$false -All
    }
    Catch [Exception]
    {
       $ErrorMessage = $_.Exception.Message
       Write-Host "Error: Search query to find the files to remediate failed...exiting the script" -ForegroundColor Red 
       Write-Host "Error: $ErrorMessage" -ForegroundColor Red 
       exit 1
    }

    # if no files were found then bail out
    if ($htmlFiles.RowCount -eq 0)
    {
        Write-Host "No files found to remediate...exiting the script" -ForegroundColor Green
        exit 0
    }
    else
    {
        Write-Host "Found" $htmlFiles.RowCount "files to remediate" -ForegroundColor Green
    }

    # Create temp folder if not yet existing
    $path = "$env:TEMP\permissivefix"
    If(!(test-path $path))
    {
          New-Item -ItemType Directory -Force -Path $path
    }

    # iterate over the found files and rename them
    foreach($htmlFile in $htmlFiles.ResultRows)
    {
        Try
        {
            $web = $htmlFile.SPWebUrl
            Write-Host "Connected to $web..."
            Connect-PnPOnline -Url $web -Credentials $credentials

            $fileToRename = $htmlFile.OriginalPath
            Write-Host "Renaming $fileToRename..."

            # Get the server relative path
            $serverRelativePath = $fileToRename.Replace("https://", "")
            $serverRelativePath = $serverRelativePath.Substring($serverRelativePath.IndexOf("/"))
            #Write-Host $serverRelativePath

            # Get new file name and server relative path
            $newFileName = $serverRelativePath.Substring($serverRelativePath.LastIndexOf("/") + 1).ToLower()
            $serverRelativePathNew = $serverRelativePath
            if ($newFileName.EndsWith(".html"))
            {
                $newFileName = $newFileName.Replace(".html", ".aspx")
                $serverRelativePathNew = $serverRelativePathNew.Replace(".html", ".aspx")
            } 
            elseif($newFileName.EndsWith(".htm"))
            {
                $newFileName = $newFileName.Replace(".htm", ".aspx")
                $serverRelativePathNew = $serverRelativePathNew.Replace(".html", ".aspx")
            }
        
            # Perform the file rename
            Rename-PnPFile -ServerRelativeUrl $serverRelativePath -TargetFileName $newFileName -OverwriteIfAlreadyExists -Force
        
            # Download the file once to ensure it works correctly in modern UI
            Get-PnPFile -Url $serverRelativePathNew -Path $path -Filename $newFileName -AsFile -Force
        }
        Catch [Exception]
        {
           $ErrorMessage = $_.Exception.Message
           Write-Host "Error: Rename of file $serverRelativePath failed" -ForegroundColor Red 
           Write-Host "Error: $ErrorMessage" -ForegroundColor Red 
        }
    }

    # Cleanup the temp folder
    Write-Host "Cleaning up the temp folder $path"
    Remove-Item $path -Recurse -ErrorAction Ignore

    Write-Host "Remediation done for site collection $siteCollectionUrl" -BackgroundColor DarkGreen -ForegroundColor White
}

#######################################################
# MAIN section                                        #
#######################################################

# Url of the site collection to remediate
$siteCollectionUrlToRemediate = "https://contoso.sharepoint.com/sites/testsite"
# If you use credential manager then specify the used credential manager entry, if left blank you'll be asked for a user/pwd
$credentialManagerCredentialToUse = "credmandreference"

# Ensure PnP PowerShell is loaded
if (-not (Get-Module -ListAvailable -Name SharePointPnPPowerShellOnline)) 
{
    Install-Module SharePointPnPPowerShellOnline
}

Import-Module SharePointPnPPowerShellOnline

# Remediate the given site collection
PermissiveRemediateASiteCollection $siteCollectionUrlToRemediate $credentialManagerCredentialToUse

```

Пример выходных данных выполнения скрипта удачном выглядит следующим образом:

```Txt
WARNING: The names of some imported commands from the module 'SharePointPnPPowerShellOnline' include unapproved verbs that might make them less discoverable. To find the commands with unapproved ver
bs, run the Import-Module command again with the Verbose parameter. For a list of approved verbs, type Get-Verb.
VERBOSE: PnP PowerShell Cmdlets (2.22.1801.0): Connected to https://contoso.sharepoint.com/sites/testsite
Using search to obtain a list of files to remediate...
Found 15 files to remediate


    Directory: C:\Users\demouser\AppData\Local\Temp


Mode                LastWriteTime         Length Name                                                                                                                                                
----                -------------         ------ ----                                                                                                                                                
d-----        7/02/2018     19:48                permissivefix                                                                                                                                       
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/About.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/brol.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/imagetarget.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/sample_html_afternoscript9.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/bla.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/sample_html.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/home2.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/howtouse.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/home.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/team_home.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/imagesource.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/bla2.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/wikipage.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/newfile_html.html...
Connected to https://contoso.sharepoint.com/sites/testsite...
Renaming https://contoso.sharepoint.com/sites/testsite/Shared Documents/Home3.html...
Cleaning up the temp folder C:\Users\demouser\AppData\Local\Temp\permissivefix
Remediation done for site collection https://contoso.sharepoint.com/sites/testsite

```

