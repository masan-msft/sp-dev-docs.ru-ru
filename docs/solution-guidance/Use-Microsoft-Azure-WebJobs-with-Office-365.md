---
title: "Использование Microsoft Azure WebJobs с Office 365"
ms.date: 11/03/2017
ms.openlocfilehash: 0b3eb304efb291dfa4c0bb7c0809f2c5b044d28f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-microsoft-azure-webjobs-with-office-365"></a>Использование Microsoft Azure WebJobs с Office 365

Используйте Azure WebJobs для реализации заданий таймера, можно получить доступ к SharePoint Online.

_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_

**Автор:** Zimmergren Тобиаса

Реализуйте функциональные возможности задания таймера с помощью [Microsoft Azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) или планировщиком заданий Windows для выполнения задач в SharePoint Online. Задание таймера: повторяющихся, запланированного, фонового процесса, который выполняется в SharePoint для выполнения некоторых задач. Например вы можете задания таймера для копирования данных, введенных в список SharePoint с базой данных. В SharePoint Online нельзя развернуть решений фермы, являющийся развертыванию заданий таймера в прошлом. Чтобы реализовать аналогичные функциональные возможности задания таймера в SharePoint Online, необходимо для запуска консольного приложения в качестве WebJob Azure. Консольное приложение получает доступ к SharePoint Online с помощью клиентской объектной модели (CSOM). В этой статье рассматриваются основные понятия, участвующих в развертывании консольные приложения как WebJobs Azure для запуска и получить доступ к SharePoint Online сайтов и контента.

## <a name="create-and-run-a-console-application-as-an-azure-webjob"></a>Создание и запуск консольного приложения в качестве WebJob Azure
<a name="sectionSection0"> </a>

Чтобы настроить консольного приложения для запуска в качестве WebJob Azure, необходимо:

1. Создание учетной записи организации для WebJob Azure для получения доступа к сайтов SharePoint и содержимого.
    
2. Создание и настройка консольного приложения.
    
3. Добавьте код в консольное приложение.
    
4. Публикация консольное приложение, как WebJob Azure.
    
5. Запуск и проверьте вашей WebJob Azure.

## <a name="create-an-organization-account"></a>Создание учетной записи организации
<a name="sectionSection1"> </a>

Необходимо создать учетную запись для WebJob Azure для использования при доступе к сайтов SharePoint и содержимого. Для получения дополнительных сведений обратитесь к [справочной системе добавить пользователей по отдельности в администрирования Office 365](https://support.office.microsoft.com/article/Add-users-individually-to-Office-365---Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec). При выполнении Azure WebJob поле **Автор изменений** хранит и отображает значение, введенное в поле **отображаемое имя** учетной записи организации. Убедитесь, что выбрано отображаемое имя, которое пользователи могут легко определять как учетная запись, используемая Azure WebJob для доступа к SharePoint.

## <a name="create-and-set-up-the-console-application"></a>Создание и настройка консольного приложения
<a name="sectionSection2"> </a>

Создание консольного приложения для запуска в качестве WebJob Azure, выполните следующие действия:

1. Создайте новый проект консольного приложения с:
    
    1. Выберите **Новый проект**в Visual Studio > **Visual C#** > **Консольного приложения** > **кнопку ОК**.
    
    2. После создания консольного приложения, выберите в меню **Сервис** > **Диспетчер пакетов NuGet** > **Управление пакетами NuGet для решения...**  >  **Online** > **все**.
    
    3. Поиск **приложения для набора средств веб-сайта SharePoint**.
    
    4. Нажмите кнопку **установить**, а затем нажмите **кнопку ОК**.
    
    5. Нажмите кнопку **Закрыть**.
    
    6. Убедитесь, что SharePointContext.cs и TokenHelper.cs были добавлены в проект консольного приложения.
    
2. Сохранение сведений об учетной записи в файле app.config, добавив элемент **appSettings** показано. Измените **SPOAccount** и **SPOPassword** на имя пользователя и пароль для учетной записи организации, созданного ранее.
    
    ```XML
    <?xml version="1.0" encoding="utf-8" ?>
     <configuration>
      <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
      </startup>
      <appSettings>
        <add key="SPOAccount" value="admin@contoso.onmicrosoft.com"/>
        <add key="SPOPassword" value="Contoso"/>
      </appSettings>
     </configuration>
    ```

    **Внимание!**  App.config хранит имя пользователя и пароль учетной записи организации в виде простого текста. Этот метод используется только в целях демонстрации и не должен использоваться в развертывании рабочей вашей WebJobs Azure. Мы рекомендуем шифровать пароль или проверка подлинности с помощью OAuth с помощью маркера доступа. Дополнительные сведения см в блоге Петров Кирк по [построению надстройки SharePoint как задания таймера](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx).

## <a name="add-code-to-the-console-application"></a>Добавление кода для консольного приложения
<a name="sectionSection3"> </a>

В файле Program.cs добавьте следующий код в консольное приложение.

**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.


1. Добавьте операторы **using** .
    
    ```C#
    using Microsoft.SharePoint.Client;
    using System.Security;
    using System.Configuration; 
    ```

2. Добавление класса следующих методов:
    
    -  **Основные** перейдете на сайт SharePoint, а затем использует CSOM для выполнения задач на сайте или контент. В этом образце кода используется CSOM поиск списка и общее число элементов, входящих в список в окне консоли выходные данные. При использовании Azure WebJobs, могут видеть выходные данные окна консоли в WebJob сведения о выполнении, обсуждаемой в [выполните и проверьте вашей WebJob Azure](Use-Microsoft-Azure-WebJobs-with-Office-365.md#runandverify).
    
  -  **GetSPOSecureStringPassword** считывает пароль из app.config.
    
  -  **GetSPOAccountName** считывает текущее имя пользователя из app.config.

    ```C#
    static void Main(string[] args)
        {
            using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
            {
                // Use default authentication mode.
                context.AuthenticationMode = ClientAuthenticationMode.Default;                 
                context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());
    
                // Add your CSOM code to perform tasks on your sites and content.
    
                try
                {
                    List objList = context.Web.Lists.GetByTitle("Docs");
                    context.Load(objList);
                    context.ExecuteQuery();
    
                    if (objList != null &amp;&amp; objList.ItemCount > 0)
                    {
                        Console.WriteLine(objList.Title.ToString() + " has " + objList.ItemCount + " items.");
                    }
    
                }
                catch (Exception ex)
                {
                    Console.WriteLine("ERROR: " + ex.Message);
                    Console.WriteLine("ERROR: " + ex.Source);
                    Console.WriteLine("ERROR: " + ex.StackTrace);
                    Console.WriteLine("ERROR: " + ex.InnerException);
    
                }
            }
                
        }
    
    private static SecureString GetSPOSecureStringPassword()
    {
      try
      {
          Console.WriteLine("Entered GetSPOSecureStringPassword.");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine("Constructed the secure password.");
    
          return secureString;
      }
      catch
      {
          throw;
      }
    }
    
    private static string GetSPOAccountName()
    {
      try
      {
          Console.WriteLine("Entered GetSPOAccountName.");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
    }
    
    ```

## <a name="publish-your-console-application-as-an-azure-webjob"></a>Публикация консольное приложение, как WebJob Azure
<a name="sectionSection4"> </a>

Завершив разработку консольное приложение, необходимо выполнить развертывание консольного приложения как WebJob Azure. Чтобы развернуть консольное приложение, как WebJob Azure, вы можете:

- Передача двоичных файлов Azure веб-приложения и создание WebJob Azure с использованием [Портала Microsoft Azure](https://portal.azure.com/). Двоичные файлы для проекта Visual Studio можно найти в bin/Debug или bin/Release папки проекта Visual Studio. Для создания веб-приложения Azure и загрузки двоичных файлов, следуйте указаниям в разделе [Create веб-приложение ASP.NET в Azure приложения-службы](http://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/). Для создания по запросу, непрерывной или запланированного WebJob Azure видеть [Запуск фоновых задач с WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).
    
- Публикация вашего WebJob Azure из Visual Studio. Дополнительные сведения можно [Включить WebJobs развертывания без веб-проект](http://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#convertnolink).
    
## <a name="run-and-verify-your-azure-webjob"></a>Запуск и проверка вашей WebJob Azure
<a name="runandverify"> </a>

После завершения всех предыдущих шагов, вашей WebJob Azure должен быть под управлением и выполнения задач в подписки Office 365. В некоторых случаях может потребоваться выполнение обслуживания и устранения неполадок вашей WebJobs Azure. Чтобы проверить, что ваше WebJob Azure работает:

- Если ваше WebJob Azure обновление элемент SharePoint как элемент списка в поле **Автор изменений** отображается учетной записи организации, Azure WebJob для доступа к SharePoint.
    
- Просмотр журналов на WebJob подробные сведения для вашей WebJob Azure. Запустите позволяет журналы WebJob сведений, просмотрите при выполнении задания, успешное или неудачное задания, вывод из WebJob (например, когда Console.WriteLine вызван) и другие сведения о запустите задание. Для получения дополнительных сведений обратитесь к разделу Просмотр журнала заданий на [Запуск фоновых задач с WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).
    
-  [Создание WebJob .NET в Azure приложения-службы](http://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).
    
-  [Ресурсы azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).
