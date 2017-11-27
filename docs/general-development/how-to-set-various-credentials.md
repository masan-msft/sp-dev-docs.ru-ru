---
title: "Задание различных учетных данных"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: eb819681-5a4f-49ae-b7f4-334366c51112
ms.openlocfilehash: 03efdb576c70191c911d7668a3343b5ad832ea0e
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="set-various-credentials"></a>Задание различных учетных данных

Необходимо задать учетные данные для пользователей, прежде чем они могут вызывать веб-служб Excel с помощью настраиваемого приложения. Необходимо явно задать учетные данные, даже в том случае, если вы намерены использовать учетные данные по умолчанию. Веб-служб Excel с помощью схемы проверки подлинности, поддерживаемые Microsoft SharePoint Foundation. Дополнительные сведения о SharePoint Foundation схем проверки подлинности, обратитесь к документации SharePoint Foundation в этом пакете SDK и [входящей на основе утверждений: вход в SharePoint](incoming-claims-signing-into-sharepoint.md).
  
    
    

The following examples show how to set credentials.
## <a name="to-use-the-current-users-credentials"></a>To use the current user's credentials

The following code uses the current user's logon credentials to make a request to the Web service. 
  
    
    

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


## <a name="to-use-various-sets-of-credentials"></a>To use various sets of credentials

The following code uses the current user's logon credentials to make a request to the Web service. 
  
    
    
 **Sample code provided by:** Saif Ullah Baig, Microsoft Corporation.
  
    
    



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


## <a name="to-use-a-different-set-of-credentials"></a>To use a different set of credentials

The following code uses the current user's logon credentials to make a request to the Web service. 
  
    
    

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

In this example, **LoginNameTextBox**, **LoginPWDTextBox**, and **LoginDomainTextBox** are the **Name** property values of the logon text boxes.
  
    
    
For more information about how to use the **CredentialCache** class and the **NetworkCredential** class, and how to use them securely, see the Microsoft Visual Studio documentation, or [NetworkCredential Class](http://msdn.microsoft.com/library/60b63419-9606-4fdc-a30f-257ded236f16.aspx).
  
    
    

## <a name="see-also"></a>См. также


#### <a name="concepts"></a>Основные понятия


  
    
    
 [Доступ к API SOAP](accessing-the-soap-api.md)
#### <a name="other-resources"></a>Другие ресурсы


  
    
    
 [Шаг 1. Создание проекта клиента веб-службы](step-1-creating-the-web-service-client-project.md)
  
    
    
 [Этап 2. Добавление веб-ссылки](step-2-adding-a-web-reference.md)
  
    
    
 [Этап 3. Получение доступа к веб-службе](step-3-accessing-the-web-service.md)
  
    
    
 [Этап 4. Построение и тестирование приложения](step-4-building-and-testing-the-application.md)
  
    
    
 [Пошаговое руководство. Разработка настраиваемого приложения с помощью веб-служб Excel](walkthrough-developing-a-custom-application-using-excel-web-services.md)
