---
title: "Подготовка пример консольного приложения"
ms.date: 11/03/2017
ms.openlocfilehash: f55962b55972312a421b8e153221f8b73bcf76b8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="provisioning-console-application-sample"></a>Подготовка пример консольного приложения

Изучение основ с помощью PnP модуля подготовки для создания и сохранения, а затем применять подготовки шаблонов для новых семейств сайтов SharePoint.

Для поддержки новой модели надстройки (PnP) программы Office 365 для разработчиков шаблоны и рекомендации представила подготовки структуру, которая позволяет пользователям создавать настраиваемые шаблоны сайтов, просто навести указатель мыши на узел модели, сохранение модели как шаблон подготовки а затем применять настраиваемый шаблон для новой или существующей семейств сайтов, при необходимости.

В этом примере мы создание простого консольного приложения, который реализует классы из подготовки PnP основной библиотеки для включения PnP модуля подготовки для выполнения этих основных задач подготовки: 

- Проектирование и модель настройки сайта. Это может быть новый сайт проекта, или можно последовательно к существующему сайту и сохранить его как шаблон подготовки.
    
- Сохраните и сохранения модели сайта как шаблона подготовки, чтобы его можно повторно использовать.
    
- Применение шаблона подготовки к семейства нового или существующего веб-сайтов.
    
> [!NOTE] 
> В этом пошаговом руководстве пример является companion для примера, в настоящее время недоступен на репозиториев: [Приступая к работе с PnP модуля подготовки](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Framework.Console). Код (Program.cs) и файлы решений для примера доступны для загрузки. Также имеется 20-минутный видео презентации этого процесса (с кодом немного отличаться) на сайте Microsoft канала 9: [Приступая к работе с PnP модуля подготовки](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).

## <a name="remote-provisioning-walkthrough"></a>Удаленный подготовки Пошаговое руководство

Чтобы начать, создайте проект Visual Studio. В этом примере для простоты мы создание простого консольного приложения, который реализует PnP модуля подготовки с помощью библиотеки PnP основных подготовки структуры. Чтобы обеспечить поддержку примера решения, тем не менее, мы необходимо загрузить и установить подготовки PnP основной библиотеки framework. Следуйте инструкциям для этого.

### <a name="create-and-prepare-a-visual-studio-project"></a>Создание и Подготовка проекта Visual Studio

1. Запустите Visual Studio, а затем выберите **файл** > **New** > **проекта**.
    
2. В мастере **Создания проекта** выберите **Visual C#**, а затем выберите пункт **Консольное приложение**.
    
3. Назовите проект «Программы» и нажмите кнопку **ОК**. (Вы можете назовите проект что-либо как, но помните, что в этом пошаговом руководстве ссылаются на имя проекта как «программа».)
    
4. Загрузка и установка PnP основной библиотеки, доступные в виде пакета NuGet: [OfficeDevPnP.Core пакетов](https://www.nuget.org/profiles/officedevpnp).
    
    > [!NOTE] 
    > Существует две версии основной библиотеки. Одна версия — это библиотека **OfficeDevPnP.Core** , которая относится SharePoint Online и Office 365. Второй версии — **OfficeDevPnP.Core (локально)**, который предназначен для SharePoint 2013 в локальной. Вот снимок из доступных вариантов.

    ![Два варианта загрузки библиотеки ядра](media/provisioning-console-application-sample/5b1adb8d-52e5-4c67-8792-6ef0ae41d655.png)

В этом пошаговом руководстве пример используется первый вариант, чтобы целевой SharePoint Online.

1. Во-первых установите клиент NuGet, перейдя на [установщик клиента NuGet](http://docs.nuget.org/consume/installing-nuget).

2. После NuGet установлен клиент, запустите **Диспетчер пакетов NuGet**. Щелкните правой кнопкой мыши узел **ссылки** в **Обозревателе решений**Visual Studio и выберите **Управление пакетами NuGet**.

3. Диспетчер пакетов, выберите **сети**, затем **EntityFramework**, а затем введите условие поиска разработчик офисных «решений» для предоставления библиотеки OfficeDevPnP.Core.

4. Следуйте инструкциям, чтобы загрузить и установить библиотеки **OfficeDevPnP.Core** , выполнив указания данного.

   После ссылки на библиотеку PnP основных в проекте Visual Studio, все члены библиотеки доступны как [методы расширения](https://msdn.microsoft.com/en-us/library/bb383977.aspx) на существующие экземпляры объекта, для примера, **веб-** серверы и **список** экземпляров.

5. Убедитесь, что файл Program.cs содержит все следующие `using` операторов.

    ```c#
    using Microsoft.SharePoint.Client;
    using OfficeDevPnP.Core.Framework.Provisioning.Connectors;
    using OfficeDevPnP.Core.Framework.Provisioning.Model;
    using OfficeDevPnP.Core.Framework.Provisioning.ObjectHandlers;
    using OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml;
    using System;
    using System.Net;
    using System.Security;
    using System.Threading;
    ```

**Один раз мы были заданы в проект**

После настройки проекта можно создать настройки сайта. Это можно сделать вручную или, указав на сайт, макет которого вы хотите использовать. Просто сохраните проект выбранного сайта в качестве шаблона подготовки. Или можно использовать сочетание оба подхода. В данном примере мы просто укажет на существующий сайт и сохранить его вариант оформления и артефактов сайта (но не его содержимое) как шаблон подготовки.

Чтобы приступить к работе, необходимо подключение к сайту, мы желаем для моделирования как наш подготовки шаблон. Начнем с собирает сведения о подключении, включая имя пользователя, пароль и исходный URL-адрес.

### <a name="create-and-extract-and-persist-the-provisioning-template"></a>Создание и извлечение и сохранение подготовки шаблона

1. Собирает сведения о подключении у пользователя. Обратите внимание, что в программе `Main` процедуры, мы выполнить три простых действия: собирать сведения о подключении и подготовки шаблона, а также ПРИМЕНЯЮТСЯ подготовки шаблона. Сложных задач выполняется с помощью методов **GetProvisioningTemplate** и **ApplyProvisioningTemplate** , которые мы определяют ниже.
    
    ```C#
    static void Main(string[] args)
        {
            ConsoleColor defaultForeground = Console.ForegroundColor;
    
            // Collect information 
            string templateWebUrl = GetInput("Enter the URL of the template site: ", false, defaultForeground);
            string targetWebUrl = GetInput("Enter the URL of the target site: ", false, defaultForeground);
            string userName = GetInput("Enter your user name:", false, defaultForeground);
            string pwdS = GetInput("Enter your password:", true, defaultForeground);
            SecureString pwd = new SecureString();
            foreach (char c in pwdS.ToCharArray()) pwd.AppendChar(c);
    
            // GET the template from existing site and serialize
            // Serializing the template for later reuse is optional
            ProvisioningTemplate template = GetProvisioningTemplate(defaultForeground, templateWebUrl, userName, pwd);
    
            // APPLY the template to new site from 
            ApplyProvisioningTemplate(defaultForeground, targetWebUrl, userName, pwd, template);
    
            // Pause and modify the UI to indicate that the operation is complete
            Console.ForegroundColor = ConsoleColor.White;
            Console.WriteLine("We're done. Press Enter to continue.");
            Console.ReadLine();
        }
    ```

2. Создайте и используйте закрытый метод **GetInput** для получения учетных данных пользователей.
    
    ```c#
    private static string GetInput(string label, bool isPassword, ConsoleColor defaultForeground)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("{0} : ", label);
            Console.ForegroundColor = defaultForeground;
    
            string value = "";
    
            for (ConsoleKeyInfo keyInfo = Console.ReadKey(true); keyInfo.Key != ConsoleKey.Enter; keyInfo = Console.ReadKey(true))
            {
                if (keyInfo.Key == ConsoleKey.Backspace)
                {
                    if (value.Length > 0)
                    {
                        value = value.Remove(value.Length - 1);
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                        Console.Write(" ");
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                    }
                }
                else if (keyInfo.Key != ConsoleKey.Enter)
                {
                    if (isPassword)
                    {
                        Console.Write("*");
                    }
                    else
                    {
                        Console.Write(keyInfo.KeyChar);
                    }
                    value += keyInfo.KeyChar;
    
                }
    
            }
            Console.WriteLine("");
    
            return value;
        }
    ```

3. Выберите сайт, который является модель для нашего шаблона, подготовки. Во время выполнения GET на исходного веб-сайта с помощью одной строки кода, рассмотрим `GetProvisioningTemplate()`, мы определили метод GET. 
    
    ```c#
    private static ProvisioningTemplate GetProvisioningTemplate(ConsoleColor defaultForeground, string webUrl, string userName, SecureString pwd)
        {
            using (var ctx = new ClientContext(webUrl))
            {
                // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    
                // Just to output the site details
                Web web = ctx.Web;
                ctx.Load(web, w => w.Title);
                ctx.ExecuteQueryRetry();
    
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine("Your site title is:" + ctx.Web.Title);
                Console.ForegroundColor = defaultForeground;
    
                ProvisioningTemplateCreationInformation ptci
                        = new ProvisioningTemplateCreationInformation(ctx.Web);
    
                // Create FileSystemConnector to store a temporary copy of the template 
                ptci.FileConnector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                ptci.PersistComposedLookFiles = true;
                ptci.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    // Only to output progress for console UI
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    
                // Execute actual extraction of the template
                ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);
    
                // We can serialize this template to save and reuse it
                // Optional step 
                XMLTemplateProvider provider =
                        new XMLFileSystemTemplateProvider(@"c:\temp\pnpprovisioningdemo", "");
                provider.SaveAs(template, "PnPProvisioningDemo.xml");
    
                return template;
            }
        }
    ```

    В приведенном выше фрагменте кода мы также определены переменной, **ProvisioningTemplateCreationInformation** **pcti**. Переменная дает возможность хранения сведений о артефакты, которые можно сохранить вместе с шаблоном.
    
4. Создание объекта файловой системы соединителя, чтобы сохранить копию временной подготовки шаблона, который мы собираемся для применения к другой сайт.
    
    > [!NOTE] 
    > Этот шаг является необязательным. Это не является обязательным, сериализации подготовки шаблон XML. На этом этапе шаблон — это просто кода C#. Не только сериализация является необязательным, но также можно использовать любой формат сериализации, вам следует.

5. Выполнение извлечения подготовки шаблона с помощью этой одной строки кода.      `ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);`
    
6. (Необязательно) Сохранить и сохраните сериализованных версия подготовки шаблона, чтобы его можно повторно использовать. Можно выполнить сериализацию подготовки шаблона в формате, независимо от выбранного вы предпочитаете. В этом примере мы сериализованным в XML-файл с именем **PnPProvisioningDemo.xml**. Сам файл является объектом **XMLFileSystemTemplateProvider** , для которого мы подготовили папку файловой системы.
    
**Один раз мы извлечения, сохранить и сохранение подготовки шаблона**

Мы извлечения, сохранить и сохранение подготовки шаблона следующий и последний шаг после для применения подготовки шаблон для нового семейства сайтов SharePoint с помощью метода **ApplyProvisioningTemplate** .

### <a name="apply-the-provisioning-template-to-a-new-or-existing-site"></a>Применение шаблона подготовки нового или существующего сайта

1. Получите учетную запись для целевого сайта.
    
    ```c#
    // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    ```

2. Capture артефактов сайта, которые были сохранены с помощью метода **ProvisioningTemplateCreationInformation** с помощью метода companion **ProvisioningTemplateApplyingInformation**.
    
    ```c#
    ProvisioningTemplateApplyingInformation ptai
                        = new ProvisioningTemplateApplyingInformation();
                ptai.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    ```

3. Получите связь с соединителя файла для активов.
    
    ```c#
    // Associate file connector for assets
                FileSystemConnector connector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                template.Connector = connector;
    
    ```

4. (Необязательно) Из-за подготовки шаблона экземпляра объекта, можно написать код для настройки артефактов сайта во время выполнения. В этом случае мы добавили новый список «контакт».
    
    ```c#
    // Since template is actual object, we can modify this using code as needed
                template.Lists.Add(new ListInstance()
                {
                    Title = "PnP Sample Contacts",
                    Url = "lists/PnPContacts",
                    TemplateType = (Int32)ListTemplateType.Contacts,
                    EnableAttachments = true
                });
    ```

5.  Применение подготовки шаблона в новый сайт еще раз с помощью одной строки кода.
    
    ```c#
        web.ApplyProvisioningTemplate(template, ptai);
    ```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [PnP подготовки framework](pnp-provisioning-framework.md)
    
- [Библиотека базовых и PnP модуля подготовки](pnp-provisioning-engine-and-the-core-library.md)
