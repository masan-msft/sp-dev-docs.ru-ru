# <a name="add-in-authorization-policy-types-in-sharepoint"></a><span data-ttu-id="938ae-101">Типы политик авторизации надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="938ae-101">Add-in authorization policy types in SharePoint</span></span>
<span data-ttu-id="938ae-p101">Узнайте о различных политиках авторизации надстроек в SharePoint: только для надстроек, для пользователей и надстроек и только для пользователей. В ней также представлены рекомендации по использованию политики только для надстроек.</span><span class="sxs-lookup"><span data-stu-id="938ae-p101">Learn about the different authorization policies for add-ins in SharePoint: add-in-only policy, user+add-in policy, and user-only policy. It also provides guidelines for using add-in-only policy. Before reading this article, you should first be familiar with the articles  Add-in permissions in SharePoint and Context Token OAuth flow for SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="938ae-p102">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="938ae-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="938ae-107">Прежде чем изучать эту статью, следует ознакомиться со статьями [Разрешения надстроек в SharePoint](add-in-permissions-in-sharepoint-2013) и [Поток OAuth маркера контекста для надстроек SharePoint](context-token-oauth-flow-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="938ae-107">Learn about the different authorization policies for add-ins in SharePoint: add-in-only policy, user+add-in policy, and user-only policy. It also provides guidelines for using add-in-only policy. Before reading this article, you should first be familiar with the articles  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint-2013) and [Context Token OAuth flow for SharePoint Add-ins](context-token-oauth-flow-for-sharepoint-add-ins).</span></span>
 

## <a name="get-an-overview-of-add-in-authorization-policies-types"></a><span data-ttu-id="938ae-108">Обзор типов политик авторизации для надстроек</span><span class="sxs-lookup"><span data-stu-id="938ae-108">Get an overview of add-in authorization policies types</span></span>
<span data-ttu-id="938ae-109"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="938ae-109"></span></span>

<span data-ttu-id="938ae-110">В SharePoint есть три типа политик авторизации:</span><span class="sxs-lookup"><span data-stu-id="938ae-110">SharePoint provides three types of authorization policies:</span></span>
 

 

-  <span data-ttu-id="938ae-p103">**Политика только для пользователей**. При ее использовании SharePoint проверяет только разрешения пользователя. SharePoint применяет эту политику, когда пользователь получает доступ непосредственно к ресурсам, не используя надстройку, например если пользователь впервые открывает домашнюю страницу веб-сайта SharePoint или получает доступ к API SharePoint из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="938ae-p103">**User-only policy** — When the user-only policy is used, SharePoint checks only the permissions for the user. SharePoint uses this policy when the user is accessing resources directly without using an add-in, such as when a user first opens a SharePoint website's home page or accesses SharePoint APIs from PowerShell.</span></span>
    
    
    
 
-  <span data-ttu-id="938ae-p104">**Политика для пользователей и надстроек**. При использовании этой политики SharePoint проверяет разрешения как пользователя, так и надстройки. Авторизация успешна, только если текущий пользователь и надстройка имеют разрешения на выполнение необходимых действий.</span><span class="sxs-lookup"><span data-stu-id="938ae-p104">**User+add-in policy** —When the user+add-in policy is used, SharePoint checks the permissions of both the user and the add-in principal. Authorization checks succeed only if both the current user and the add-in have permissions to perform the action in question.</span></span>
    
    <span data-ttu-id="938ae-p105">Например, эта политика используется, когда надстройке SharePoint необходимо получить доступ к ресурсам пользователя в SharePoint. Код в удаленных компонентах надстройки SharePoint должен быть реализован так, чтобы можно было выполнять вызовы для пользователей и надстроек к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="938ae-p105">For example this policy is used when a SharePoint Add-in wants to get access to the user's resources on SharePoint. (The code in the remote components of the SharePoint Add-in have to be designed to make user+add-in calls to SharePoint.)</span></span>
    
    
    
 
-  <span data-ttu-id="938ae-p106">**Политика только для надстроек**. При использовании этой политики SharePoint проверяет только разрешения надстройки. Авторизация успешна, только если текущая надстройка имеет достаточно разрешений для выполнения необходимый действий, независимо от разрешений, имеющихся у текущего пользователя (если они имеются).</span><span class="sxs-lookup"><span data-stu-id="938ae-p106">**Add-in-only policy** —When the add-in-only policy is used, SharePoint checks only the permissions of the add-in principal. Authorization checks succeed only if the current add-in has sufficient permissions to perform the action in question, regardless of the permissions of the current user (if any).</span></span>
    
    <span data-ttu-id="938ae-p107">Примером использования этой политики может служить надстройка для утверждения расходов. С ее помощью пользователи, которые не имеют возможности утверждать расходы меньше определенной суммы, могут выполнять такие действия. Дополнительные сведения см. в сценарии ниже.</span><span class="sxs-lookup"><span data-stu-id="938ae-p107">An expense approval add-in is an example of an add-in that could be designed to use this policy. The add-in allows users who wouldn't otherwise be able to approve expenses to approve expenses below a certain amount. See the scenario below for details.</span></span> 
    
    
    
     <span data-ttu-id="938ae-p108">**Примечание.** Некоторым API требуется контекст пользователя, и они не могут выполняться при использовании политики только для надстроек. К ним относятся многие API для взаимодействия с Project Server 2013 и выполнения поисковых запросов.</span><span class="sxs-lookup"><span data-stu-id="938ae-p108">**Note** Certain APIs require a user context and can't be executed with an add-in-only policy. These include many APIs for interacting with Project Server 2013 and for performing search queries.</span></span>

### <a name="see-an-example-scenario-of-an-add-in-that-uses-the-add-in-only-policy"></a><span data-ttu-id="938ae-124">Пример сценария с надстройкой, использующей политику только для надстроек</span><span class="sxs-lookup"><span data-stu-id="938ae-124">See an example scenario of an add-in that uses the add-in-only policy</span></span>
<span data-ttu-id="938ae-125"><a name="Scenario"> </a></span><span class="sxs-lookup"><span data-stu-id="938ae-125"></span></span>

<span data-ttu-id="938ae-p109">Предположим, менеджер по продажам в Contoso Сергей покупает надстройку по предоставлению документов о расходах, в которой используется политика только для надстроек. При покупке надстройки Сергею предлагается разрешить ей работать с разрешениями более высокого уровня (надстройка может выполнять вызовы только для надстроек в SharePoint). Допустим, что Сергей предоставил надстройке такие разрешения. Затем он покупает достаточное количество лицензий надстройки для всех продавцов Contoso и устанавливает ее на веб-сайте SharePoint отдела продаж.</span><span class="sxs-lookup"><span data-stu-id="938ae-p109">Let's says a sales manager at Contoso, Adam, buys an expense submission add-in that uses the add-in-only policy. When Adam chooses to buy the add-in, Adam is prompted to allow the add-in to elevate user permissions; that is, to allow the add-in to make add-in-only calls to SharePoint. Adam grants the add-in the requested permissions. He then purchases enough licenses of the add-in for all of the Contoso sales people, and he installs the add-in in the sales team's SharePoint website.</span></span>
 

 
<span data-ttu-id="938ae-p110">Вскоре продавцы начинают отправлять отчеты о расходах с помощью новой надстройки. Обычно продавцам не предоставляется возможность утверждать их собственные отчеты о расходах, но они могут это сделать с помощью надстройки для отчетов, сумма в которых не превышает 50 рублей. Сергей настроил автоматическое утверждение подобных отчетов. Надстройка автоматически назначает ему задачу по утверждению отчетов, сумма в которых меньше 50 рублей. Это можно реализовать, предоставив надстройке SharePoint разрешение на запись в список утвержденных расходов SharePoint. Но среди пользователей разрешение на запись в список имеется только у руководителей отдела кадров. Код в надстройке реализован так, что расходы в список добавляются с помощью вызова к SharePoint только для надстроек в том случае, если сумма расходов составляет меньше 50 рублей. Так как разрешения пользователя не проверяются, любые отчеты пользователя, не превышающие 50 рублей, автоматически добавляются в список утвержденных расходов, даже если у пользователя нет разрешения на запись в список.</span><span class="sxs-lookup"><span data-stu-id="938ae-p110">Soon, the salespeople are submitting expense reports using the new expense submission add-in. Salespeople usually cannot approve their own expense reports, but they can do this when using the add-in because Adam granted it the ability to do this for expense submissions below $50 because he set the add-in to automatically approve reports below $50. The add-in automatically assigns him a task to approve reports of $50 or more. This could be implemented by giving the SharePoint Add-in Write permission to a SharePoint list of approved expenses. But, among users, only human resources managers have Write permission to the list. The code in the add-in is designed to add the expense to the list by making an add-in-only call to SharePoint whenever the expense is less than $50. Since the user's permissions aren't checked, any user's submissions below $50 are automatically added to the approved expenses list, even if the user doesn't have Write permission to the list.</span></span>
 

 

 

 

### <a name="learn-how-add-ins-get-permission-to-use-the-add-in-only-policy"></a><span data-ttu-id="938ae-137">Сведения о том, как надстройки получают разрешение на использование политики только для надстроек</span><span class="sxs-lookup"><span data-stu-id="938ae-137">Learn how add-ins get permission to use the add-in-only policy</span></span>
<span data-ttu-id="938ae-138"><a name="Approve"> </a></span><span class="sxs-lookup"><span data-stu-id="938ae-138"></span></span>

<span data-ttu-id="938ae-p111">Чтобы получить возможность выполнять вызовы к SharePoint только для надстроек, в манифесте надстройки следует запросить разрешение на использование политики только для надстроек. Для этого добавьте атрибут **AllowAppOnlyPolicy** к элементу **AppPermissionRequests** и задайте для него значение **true**, как показано в приведенной ниже части кода.</span><span class="sxs-lookup"><span data-stu-id="938ae-p111">To be able to make add-in-only calls to SharePoint, your add-in must request permission to use the add-in-only policy. This request is made in the add-in manifest. You do this by adding the **AllowAppOnlyPolicy** attribute to the **AppPermissionRequests** element and setting it to **true** as shown in the following markup:</span></span>
 

 

```XML
<AppPermissionRequests AllowAppOnlyPolicy="true">
    ...
</AppPermissionRequests>
```


 <span data-ttu-id="938ae-p112">**Примечание.** Предыдущее название надстроек SharePoint — "приложения для SharePoint". Для поддержания обратной совместимости схема манифеста приложения осталась без изменений, поэтому строка "app" присутствует в именах многих элементов и атрибутов.</span><span class="sxs-lookup"><span data-stu-id="938ae-p112">**Note** SharePoint Add-ins used to be called "apps for SharePoint". To maintain backward compatibility, the app manifest schema was not changed, so the string "app" appears in may element and attribute names.</span></span>
 

<span data-ttu-id="938ae-p113">Пользователю, устанавливающему надстройку, будет предложено утвердить этот запрос. Если надстройка запрашивает клиентские разрешения, то разрешить использование политики только для надстроек может только администратор клиента, поэтому только он может установить надстройку. Если надстройка не запрашивает никакие разрешения, область которых выше семейства веб-сайтов, то установить ее может администратор семейства веб-сайтов. Дополнительные сведения об областях разрешений см. в разделе  [Разрешения для надстроек в SharePoint](add-in-permissions-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="938ae-p113">A user installing the add-in will be prompted to approve this request. If the add-in asks for tenant-scoped permissions, then only a tenant administrator can grant use of the add-in-only policy, so only a tenant administrator can install the add-in. If the add-in does not ask for any permissions scoped higher than site collection, then a site collection administrator can install the add-in. For more information about permission scopes, see  [Add-in permissions in SharePoint](add-in-permissions-in-sharepoint-2013).</span></span>
 

 

### <a name="learn-how-add-ins-make-add-in-only-calls"></a><span data-ttu-id="938ae-148">Узнайте, как надстройки выполняют вызовы только для надстроек</span><span class="sxs-lookup"><span data-stu-id="938ae-148">Learn how add-ins make add-in-only calls</span></span>
<span data-ttu-id="938ae-149"><a name="AppOnlyCalls"> </a></span><span class="sxs-lookup"><span data-stu-id="938ae-149"></span></span>

<span data-ttu-id="938ae-p114">Различие между вызовом к SharePoint только для надстроек и вызовом для пользователей и надстроек заключается в типе маркера доступа, который включен в вызов. В примере кода ниже показано, как создать и получить маркеры доступа для пользователей и надстроек и маркеры доступа только для надстроек в управляемом коде. Готовый код представлен в файле TokenHelper.cs (или с расширением VB), который Инструменты разработчика Office для Visual Studio автоматически добавляет в проект надстройки SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="938ae-p114">The difference between an add-in-only call to SharePoint and a user+add-in call is the type of access token that is included in the call. The following code shows how to obtain user+add-in and add-in-only access tokens in managed code. The detailed coding is done for you in the TokenHelper.cs (or .vb) file that the Office Developer Tools for Visual Studio automatically add to the project in Visual Studio.</span></span>
 

 

```C#
string contextTokenString = TokenHelper.GetContextTokenFromRequest(Request);
if (contextTokenString != null)
{
     //Get context token.
     SharePointContextToken contextToken =
          TokenHelper.ReadAndValidateContextToken(contextTokenString, Request.Url.Authority);
     Uri sharepointUrl = new Uri(Request.QueryString["SPHostUrl"]);

     //Get user+add-in access token.
     string accessToken =
          TokenHelper.GetAccessToken(contextToken, sharepointUrl.Authority).AccessToken;

      ClientContext clientContext =
           TokenHelper.GetClientContextWithAccessToken(sharepointUrl.ToString(), accessToken);

      //Do something. 
       ...
    
      //Get add-in-only access token.
       string addinOnlyAccessToken = 
            TokenHelper.GetAppOnlyAccessToken(contextToken.TargetPrincipalName, 
                              sharepointUrl.Authority, contextToken.Realm).AccessToken;
         //Do something.
         ...
}
```


 <span data-ttu-id="938ae-p115">**Примечание.** В надстройках, которые не поддерживают вызовы с проверкой подлинности OAuth (например, надстройки, представляющие собой только код JavaScript, выполняющийся на сайте надстройки), невозможно использовать политику только для надстроек. Такие надстройки запрашивают разрешение, но не могут им воспользоваться, так как при этом им необходимо обрабатывать токен OAuth только для надстроек. Только надстройки с веб-приложениями, выполняющиеся за пределами SharePoint, могут создавать и обрабатывать маркеры только для надстроек.</span><span class="sxs-lookup"><span data-stu-id="938ae-p115">**Note** Add-ins that do not make OAuth authenticated calls (for example, add-ins that are only JavaScript running in the add-in web) cannot use the add-in-only policy. They can request the permission, but they will not be able to take advantage of it because doing so requires passing an add-in-only OAuth token. Only add-ins with web applications running outside of SharePoint can create and pass add-in-only tokens.</span></span>
 

<span data-ttu-id="938ae-p116">Как правило, для выполнения вызова требуется наличие текущего пользователя. В случае политики только для надстроек SharePoint создает пользователя SHAREPOINT\APP (аналогично существующему пользователю SHAREPOINT\SYSTEM). Все запросы только для надстроек отправляются от имени пользователя SHAREPOINT\APP. Выполнить проверку подлинности на основе пользователя от имени SHAREPOINT\APP невозможно.</span><span class="sxs-lookup"><span data-stu-id="938ae-p116">In general, a current user is required to be present for a call to be made. In the case of add-in-only policy, SharePoint creates a SHAREPOINTAPP, similar to the existing SHAREPOINTSYSTEM user. All add-in-only requests are made by SHAREPOINTAPP. There is no way to authenticate as SHAREPOINTAPP through user-based authentication.</span></span>
 

 

### <a name="get-guidelines-for-using-the-add-in-only-policy"></a><span data-ttu-id="938ae-160">Рекомендации по использованию политики только для надстроек</span><span class="sxs-lookup"><span data-stu-id="938ae-160">Get guidelines for using the add-in-only policy</span></span>
<span data-ttu-id="938ae-161"><a name="GuidelinesFor"> </a></span><span class="sxs-lookup"><span data-stu-id="938ae-161"></span></span>

<span data-ttu-id="938ae-p117">Поскольку вызовы только для надстроек позволяют эффективно повысить уровень прав пользователя, следует с осторожностью создавать надстройки, которые запрашивают такие разрешения. Вызовы должны использовать политики только для надстроек исключительно в указанных ниже случаях.</span><span class="sxs-lookup"><span data-stu-id="938ae-p117">Since add-in-only calls effectively elevate user privileges, you should be conservative in creating add-ins that ask for permission to make them. Calls should use the add-in-only policy only if:</span></span>
 

 

- <span data-ttu-id="938ae-164">Надстройке необходимо повысить уровень своих разрешений по сравнению с пользователем для выполнения определенного вызова (например, чтобы надстройка могла самостоятельно утвердить отчет о расходах).</span><span class="sxs-lookup"><span data-stu-id="938ae-164">The add-in needs to elevate its permissions above the user for a specific call; for example, to approve an expense report under conditions evaluated by the add-in.</span></span>
    
 
- <span data-ttu-id="938ae-165">Надстройка не выполняется от имени любого пользователя (например, надстройка, выполняющая задачи по ночному обслуживанию библиотеки документов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="938ae-165">The add-in is not acting on behalf of any user; for example, an add-in that performs nightly maintenance tasks on a SharePoint document library.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="938ae-166">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="938ae-166">Additional resources</span></span>
<span data-ttu-id="938ae-167"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="938ae-167"></span></span>


-  [<span data-ttu-id="938ae-168">Авторизация и проверка подлинности надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="938ae-168">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="938ae-169">Разрешения надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="938ae-169">Add-in permissions in SharePoint</span></span>](add-in-permissions-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="938ae-170">Поток OAuth маркера контекста для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="938ae-170">Context Token OAuth flow for SharePoint Add-ins</span></span>](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="938ae-171">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="938ae-171">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="938ae-172">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="938ae-172">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 

