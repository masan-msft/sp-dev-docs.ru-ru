---
title: How to Set Various Credentials
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: eb819681-5a4f-49ae-b7f4-334366c51112
ms.openlocfilehash: a1faa07c07c24886d73874af54d125e713fd7c87
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-set-various-credentials"></a><span data-ttu-id="9e275-102">How to: Set Various Credentials</span><span class="sxs-lookup"><span data-stu-id="9e275-102">How to: Set Various Credentials</span></span>

<span data-ttu-id="9e275-103">Необходимо задать учетные данные для пользователей, прежде чем они могут вызывать веб-служб Excel с помощью настраиваемого приложения.</span><span class="sxs-lookup"><span data-stu-id="9e275-103">You must set credentials for your users before they can call Excel Web Services by using your custom application.</span></span> <span data-ttu-id="9e275-104">Необходимо явно задать учетные данные, даже в том случае, если вы намерены использовать учетные данные по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9e275-104">You must explicitly set credentials even if you intend to use the default credentials.</span></span> <span data-ttu-id="9e275-105">Веб-служб Excel с помощью схемы проверки подлинности, поддерживаемые Microsoft SharePoint Foundation.</span><span class="sxs-lookup"><span data-stu-id="9e275-105">Excel Web Services uses the authentication schemes that Microsoft SharePoint Foundation supports.</span></span> <span data-ttu-id="9e275-106">Дополнительные сведения о SharePoint Foundation схем проверки подлинности, обратитесь к документации SharePoint Foundation в этом пакете SDK и [входящей на основе утверждений: вход в SharePoint](incoming-claims-signing-into-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="9e275-106">For more information about SharePoint Foundation authentication schemes, see the SharePoint Foundation documentation in this SDK and  [Incoming claims: Signing into SharePoint](incoming-claims-signing-into-sharepoint.md).</span></span>
  
    
    

<span data-ttu-id="9e275-107">The following examples show how to set credentials.</span><span class="sxs-lookup"><span data-stu-id="9e275-107">The following examples show how to set credentials.</span></span>
## <a name="to-use-the-current-users-credentials"></a><span data-ttu-id="9e275-108">To use the current user's credentials</span><span class="sxs-lookup"><span data-stu-id="9e275-108">To use the current user's credentials</span></span>

<span data-ttu-id="9e275-109">The following code uses the current user's logon credentials to make a request to the Web service.</span><span class="sxs-lookup"><span data-stu-id="9e275-109">The following code uses the current user's logon credentials to make a request to the Web service.</span></span> 
  
    
    

```cs

//Instantiate the Web service.
    ExcelService xlService = new ExcelService();
//Set credentials for requests.
    xlService.Credentials = System.Net.CredentialCache.DefaultCredentials;

```


```VB.net

'Instantiate the Web service.
Dim xlService As New ExcelService()
'Set credentials for requests.
xlService.Credentials = System.Net.CredentialCache.DefaultCredentials
```


## <a name="to-use-various-sets-of-credentials"></a><span data-ttu-id="9e275-110">To use various sets of credentials</span><span class="sxs-lookup"><span data-stu-id="9e275-110">To use various sets of credentials</span></span>

<span data-ttu-id="9e275-111">The following code uses the current user's logon credentials to make a request to the Web service.</span><span class="sxs-lookup"><span data-stu-id="9e275-111">The following code uses the current user's logon credentials to make a request to the Web service.</span></span> 
  
    
    
 <span data-ttu-id="9e275-112">**Sample code provided by:** Saif Ullah Baig, Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="9e275-112">**Sample code provided by:** Saif Ullah Baig, Microsoft Corporation.</span></span>
  
    
    



```cs

        protected string farmURL, docLibPath, workbookPath, uiCulture, dataCulture, localTempFolder, authenticationType;
        protected Cookie authCookie;

        protected API.ExcelService api;
        protected Constants.XLS_VER version;
        

        public VariousAuthScheme(Constants.XLS_VER ver, string farmurl, string docLib, string fileName, 
            string uic, string datac,
            string userName, string password, string domain,
            string localTemp, string authType)
        {
            api = new API.ExcelService();

            farmURL = farmurl;

            if (!farmURL.EndsWith("/"))
            {
                farmURL += "/";
            }

            api.Url = farmURL + "_vti_bin/ExcelService.asmx";

            
            version = ver;

            if (!docLib.EndsWith("/"))
            {
                docLib += "/";
            }

            workbookPath = farmURL + docLib + fileName;
            docLibPath = farmURL + docLib;
            uiCulture = uic;
            dataCulture = datac;
            localTempFolder = localTemp;
            authenticationType = authType;

            switch (authType)
            {
                case "Windows-Classic":
                    authenticationType = "Windows-Classic";
                    AuthenticateWindowsClassic(domain, userName, password);
                    break;

                case "Windows-Claims":
                    authenticationType = "Windows-Claims";
                    AuthenticateWindowsClaims();
                    break;

                case "FBA-Claims":
                    authenticationType = "FBA-Claims";
                    if (!AuthenticateFBAClaims(userName, password))
                        throw new Exception("FBA-Claims authentication failed");
                    break;

                case "Anonymous":
                    authenticationType = "Anonymous";
                    break;

                default:
                    throw new Exception ("Undefined authentication type specified: " + authType);
                    break;
            }
        }

        protected void AuthenticateWindowsClassic(string domain, string userName, string password)
        {
            if (userName != null &amp;&amp; userName.Length > 0)
            {
                api.Credentials = new System.Net.NetworkCredential(userName, password, domain);
            }
            else
            {
                api.Credentials = System.Net.CredentialCache.DefaultCredentials;
            }

            // Verify set credentials.
            System.Net.NetworkCredential cred = (System.Net.NetworkCredential) api.Credentials;
            Console.WriteLine(@"Credentials set to: {0}\\{1}", cred.Domain, cred.UserName);
        }

        protected void AuthenticateWindowsClaims()
        {
            throw new Exception ("Windows-Claims Authentication method not implemented");
        }

        protected bool AuthenticateFBAClaims(string userName, string password)
        {
            FBA.Authentication spAuthentication = new FBA.Authentication();
            spAuthentication.Url = farmURL + "_vti_bin/Authentication.asmx";
                          
            spAuthentication.CookieContainer = new CookieContainer();

            FBA.LoginResult loginResult = spAuthentication.Login(userName, password);
            authCookie = new Cookie();
                
            // Determines if login is successful.
            if (loginResult.ErrorCode == FBA.LoginErrorCode.NoError)
            {
                // Get the cookie collection from the authenticating Web service.
                CookieCollection cookies = spAuthentication.CookieContainer.GetCookies(new Uri(spAuthentication.Url));

                // Get the specific cookie that contains the security token.
                authCookie = cookies[loginResult.CookieName];

                // Initialize the cookie container of Excel Web Services.
                api.CookieContainer = new CookieContainer();
                api.CookieContainer.Add(authCookie);

                return true;
            }
            else
            {
                return false;
            }
        

```


## <a name="to-use-a-different-set-of-credentials"></a><span data-ttu-id="9e275-113">To use a different set of credentials</span><span class="sxs-lookup"><span data-stu-id="9e275-113">To use a different set of credentials</span></span>

<span data-ttu-id="9e275-114">The following code uses the current user's logon credentials to make a request to the Web service.</span><span class="sxs-lookup"><span data-stu-id="9e275-114">The following code uses the current user's logon credentials to make a request to the Web service.</span></span> 
  
    
    

```cs

//Instantiate the Web service.
ExcelService xlService = new ExcelService();

public void VerifyCredentials()
   {
    //Check whether the default credentials
    //should be used instead.  
       if (DefaultCredentialsCheckBox.Checked)
 {
     xlService.Credentials =     
        System.Net.CredentialCache.DefaultCredentials;
  }
  else
  {
      //Check whether user-defined credentials
         //should be used instead.
      System.Net.NetworkCredential userDefined = new 
         System.Net.NetworkCredential(
            LoginNameTextBox.Text,
LoginPWDTextBox.Text,
LoginDomainTextBox.Text);

         xlService.Credentials = userDefined;          
      }
}
```


```VB.net

'Instantiate the Web service.
Private xlService As New ExcelService()

Public Sub VerifyCredentials()
    'Check whether the default credentials
    'should be used instead.  
       If DefaultCredentialsCheckBox.Checked Then
     xlService.Credentials = System.Net.CredentialCache.DefaultCredentials
  Else
      'Check whether user-defined credentials
         'should be used instead.
      Dim userDefined As New System.Net.NetworkCredential(LoginNameTextBox.Text, LoginPWDTextBox.Text, LoginDomainTextBox.Text)

         xlService.Credentials = userDefined
  End If
End Sub
```

<span data-ttu-id="9e275-115">In this example, **LoginNameTextBox**, **LoginPWDTextBox**, and **LoginDomainTextBox** are the **Name** property values of the logon text boxes.</span><span class="sxs-lookup"><span data-stu-id="9e275-115">In this example, **LoginNameTextBox**, **LoginPWDTextBox**, and **LoginDomainTextBox** are the **Name** property values of the logon text boxes.</span></span>
  
    
    
<span data-ttu-id="9e275-116">For more information about how to use the **CredentialCache** class and the **NetworkCredential** class, and how to use them securely, see the Microsoft Visual Studio documentation, or [NetworkCredential Class](http://msdn.microsoft.com/library/60b63419-9606-4fdc-a30f-257ded236f16.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e275-116">For more information about how to use the **CredentialCache** class and the **NetworkCredential** class, and how to use them securely, see the Microsoft Visual Studio documentation, or [NetworkCredential Class](http://msdn.microsoft.com/library/60b63419-9606-4fdc-a30f-257ded236f16.aspx).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="9e275-117">См. также</span><span class="sxs-lookup"><span data-stu-id="9e275-117">See also</span></span>


#### <a name="concepts"></a><span data-ttu-id="9e275-118">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="9e275-118">Concepts</span></span>


  
    
    
 [<span data-ttu-id="9e275-119">Доступ к API SOAP</span><span class="sxs-lookup"><span data-stu-id="9e275-119">Accessing the SOAP API</span></span>](accessing-the-soap-api.md)
#### <a name="other-resources"></a><span data-ttu-id="9e275-120">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="9e275-120">Other resources</span></span>


  
    
    
 [<span data-ttu-id="9e275-121">Шаг 1. Создание проекта клиента веб-службы</span><span class="sxs-lookup"><span data-stu-id="9e275-121">Step 1: Creating the Web Service Client Project</span></span>](step-1-creating-the-web-service-client-project.md)
  
    
    
 [<span data-ttu-id="9e275-122">Этап 2. Добавление веб-ссылки</span><span class="sxs-lookup"><span data-stu-id="9e275-122">Step 2: Adding a Web Reference</span></span>](step-2-adding-a-web-reference.md)
  
    
    
 [<span data-ttu-id="9e275-123">Этап 3. Получение доступа к веб-службе</span><span class="sxs-lookup"><span data-stu-id="9e275-123">Step 3: Accessing the Web Service</span></span>](step-3-accessing-the-web-service.md)
  
    
    
 [<span data-ttu-id="9e275-124">Этап 4. Построение и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="9e275-124">Step 4: Building and Testing the Application</span></span>](step-4-building-and-testing-the-application.md)
  
    
    
 [<span data-ttu-id="9e275-125">Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel</span><span class="sxs-lookup"><span data-stu-id="9e275-125">Walkthrough: Developing a Custom Application Using Excel Web Services</span></span>](walkthrough-developing-a-custom-application-using-excel-web-services.md)
