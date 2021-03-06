# <a name="authorization-and-authentication-of-sharepoint-add-ins"></a>Авторизация и проверка подлинности надстроек SharePoint
Общие сведения о проверке подлинности и авторизации в SharePoint, используемых для авторизации запросов надстройки SharePoint на доступ к ресурсам SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

## <a name="add-in-authentication-in-sharepoint"></a>Проверка подлинности надстроек в SharePoint
<a name="AuthN"> </a>

Когда  *пользователь*  входит в SharePoint, проверяется его маркер безопасности. Маркер выдается поставщиком удостоверений. SharePoint поддерживает несколько видов аутентификации пользователя. Дополнительные сведения см. в статье [Проверка подлинности, авторизация и безопасность в SharePoint](http://msdn.microsoft.com/library/8734790c-eb75-4d78-9604-7cc23b33b693%28Office.15%29.aspx).
 

 
Надстройки SharePoint это также субъекты безопасности, требующие проверки подлинности и авторизации. Проверку подлинности и авторизацию надстроек можно выполнить несколькими различными способами. Дополнительные сведения см. в статье  [Три системы авторизации для надстроек для SharePoint](three-authorization-systems-for-sharepoint-add-ins). 
 

 

## <a name="authorization-policies-user-only-policy-useradd-in-policy-or-add-in-only-policy"></a>Политики авторизации: только для пользователей, для пользователей и надстроек или только для надстроек
<a name="AuthZ"> </a>

Процесс авторизации проверят, имеет ли прошедший проверку подлинности субъект (надстройка, пользователь или и то, и другое) разрешение на выполнение определенных операций или на доступ к конкретным ресурсам (например, к списку или к папке документов SharePoint).
 

 
В SharePoint используется три типа политик авторизации. Политика только для пользователя требует только того, чтобы вызов SharePoint включал удостоверение пользователя, прошедшее проверку подлинности. Политика только для надстройки требует только того, чтобы вызов включал удостоверение надстройки, прошедшее проверку подлинности. Политика для пользователя и надстройки требует, чтобы вызов включал удостоверения обоих видов, прошедшие проверку подлинности. Когда пользователь получает доступ к ресурсам SharePoint через пользовательский интерфейс SharePoint, а не через надстройку, SharePoint применяет политику только для пользователя. Тем не менее для вызовов, которые отправляет надстройка SharePoint, SharePoint всегда использует политику только для надстройки или политику для надстройки и пользователя. Надстройка SharePoint определяет используемую политику по типу маркера доступа, включенного в запрос к SharePoint. При отправке запроса для надстройки и пользователя SharePoint будет требовать, чтобы и у надстройки, и у пользователя были разрешения для ресурса, к которому надстройка получает доступ. В случае с запросом только для надстройки SharePoint требует, чтобы у надстройки были разрешения для ресурса. При этом не имеет значения, есть ли такие разрешения у пользователя (надстройка SharePoint может отправлять запросы только для надстройки, если ей заранее, обычно при установке, были предоставлены соответствующие разрешения).
 

 
Дополнительные сведения о политиках авторизации и принципе их работы см. в статье [Типы политик авторизации надстроек в SharePoint](add-in-authorization-policy-types-in-sharepoint-2013).
 

 

## <a name="add-in-permissions-and-add-in-permission-request-scopes"></a>Разрешения и области запросов разрешений для надстроек
<a name="Permissions"> </a>

Разработчик, создавший надстройку SharePoint, должен указать в файле манифеста надстройки разрешения, необходимые для ресурсов SharePoint за пределами сайта надстройки. (Надстройка автоматически получает полный доступ ко всему сайту надстройки.) Если надстройка предназначена для запуска из SharePoint, инфраструктура установки надстройки запрашивает у пользователя, устанавливающего ее, следует ли предоставить необходимые разрешения. После получения разрешений пользователи веб-сайта смогут работать с надстройкой без повторного предоставления разрешений. Тем не менее если надстройка должна запускаться за пределами SharePoint (то есть она не установлена в SharePoint), SharePoint спрашивает у пользователя, запускающего надстройку, следует ли предоставить необходимые разрешения при каждом ее запуске. Надстройки на мобильных устройствах и Надстройки Office это надстройки, которые могут получать доступ к среде SharePoint, но не устанавливаются в ней.
 

 
Только владелец веб-сайта может установить надстройку SharePoint на веб-сайте SharePoint (если не была создана настраиваемая роль с правами для установки надстроек). Пользователь может предоставить надстройке только те разрешения, которые есть у него самого. Поэтому пользователь не может установить надстройку, требующую разрешений, которых у него нет. Аналогично, пользователь не может запускать настройку, предназначенную для запуска из внешней среды, которой требуются разрешения, отсутствующие у пользователя. Но если Надстройка SharePoint установлена в SharePoint, она может запрашивать разрешение только на вызовы надстроек. Надстройка с таким разрешением может получать доступ к SharePoint способами, на которые нет разрешения у пользователя, запускающего ее.
 

 
Администраторы клиентов SharePoint Online и ферм SharePoint также могут отзывать и предоставлять разрешения для надстроек.
 

 
В файле манифеста Надстройка SharePoint указывает разрешения, которые необходимы ей для правильной работы. В запросах на разрешения указываются как права, необходимые надстройке, так и область, в которой требуются эти права. Области указывают, где применяется запрос на разрешение в иерархии SharePoint. SharePoint поддерживает четыре различных области контента: клиент, семейство веб-сайтов, веб-сайт и список. Существуют также специальные области для выполнения поисковых запросов, доступа к данным таксономии, социальным функциям, возможностям Службы Microsoft Business Connectivity Services (BCS) и Project Server 2013. Дополнительные сведения см. в разделе  [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint-2013).
 

 

## <a name="when-is-oauth-used"></a>В каких случаях используется OAuth?
<a name="FileName_uniquekeyword4"> </a>

Возможно, вы уже слышали, что OAuth 2.0 играет важную роль при проверки подлинности и авторизации надстроек SharePoint. Это действительно так, но Надстройка SharePoint может и не использовать этот протокол для авторизации. Если планируется создать надстройку SharePoint, работающую в удаленном веб-приложении и взаимодействующую с SharePoint с использованием кода на стороне сервера, то придется использовать OAuth. Если удаленное веб-приложение находится вне локальной среды, используется  [система авторизации с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization), в которой служба Azure ACS выступает поставщиком маркеров доступа. Если веб-приложение находится в локальной среде, обычно используется  [система с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization), в которой сама надстройка и цифровой сертификат служат поставщиками маркеров доступа.
 

 
Не следует использовать OAuth для вызова JavaScript на странице в самом веб-сайте надстройки или с удаленной веб-страницы с помощью  [междоменной библиотеки](creating-sharepoint-add-ins-that-use-the-cross-domain-library). Дополнительные сведения о междоменных библиотеках см. в статье  [Создание надстроек для SharePoint, которые используют междоменную библиотеку](creating-sharepoint-add-ins-that-use-the-cross-domain-library).
 

 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="Filename_AdditionalResources"> </a>


-  [Три системы авторизации для надстроек SharePoint](three-authorization-systems-for-sharepoint-add-ins)
    
 
-  [Разрешения надстроек в SharePoint](add-in-permissions-in-sharepoint-2013)
    
 
-  [Надстройки SharePoint](sharepoint-add-ins)
    
 
