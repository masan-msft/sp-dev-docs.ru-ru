---
title: "Платформа задания таймера #"
ms.date: 11/03/2017
ms.openlocfilehash: d6db7e8e9eb50006d8abb6d02ccfd9a0d12b736c
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="the-timer-job-framework"></a>Платформа задания таймера #

PnP Framework задания таймера представляют собой набор классов, предназначенных для упрощения создания фоновых процессах, которые используются для сайтов SharePoint. Платформа задания таймера похож на код полного доверия локальной задания таймера (`SPJobDefinition`). С основным различием между Framework задания таймера и кода полного доверия задание таймера только в том, что Framework задания таймера с помощью API-интерфейсы на стороне клиента и таким образом можно и следует выполнять вне SharePoint. Framework задания таймера позволяет создавать задания таймера, работают в SharePoint Online.

После задания таймера был создан, его необходимо планирования и выполнения. Две основные параметры являются:

- Когда **Microsoft Azure** платформы размещения, задания таймера можно развернуть и запуска в качестве **Azure WebJobs**.
- **Windows Server** — размещения задания таймера платформы (например, для локального развертывания SharePoint) можно развернуть и запустить в **Планировщик Windows**.

Для видео Общие сведения о задания таймера [в этом видео PnP](http://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-the-PnP-timer-job-framework) представляется Framework задания таймера и показано в примере простого задания таймера.

## <a name="simple-timer-job-example"></a>Простой пример задания таймера ##
В этой главе вы увидите, как создать простой задание таймера: задача в этом примере — предоставить средство чтения быстрого представления, более поздней версии для мы предлагаем более подробное описание Framework задания таймера. 

**Примечание:** Расширенный PnP решение с десяти отдельных примеры задания таймера из примеры задания фактический истечения срока действия содержимого, «Hello world» в разделе https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples

Ниже описывается, как создать простой задания таймера:

### <a name="step-1-create-a-console-project-and-reference-pnp-core"></a>Этап 1: Создайте проект консольного и ссылаться PnP ядра ###
На первом этапе создайте новый проект типа «консоли» и ссылки на библиотеку PnP core, выполнив одно из следующих:

- Добавьте в проект пакетов Nuget основные рекомендации и шаблоны для разработчиков Office 365. Существует [пакетов nuget для v15 (локально), а также для v16 (Office 365)](https://www.nuget.org/packages?q=pnp). Это является предпочтительным.
- Добавление существующего проекта PnP основных источника в проект. Это позволит выполнить пошагово код PnP основных при отладке. **Примечание:** Ответственность за поддержание этот код, обновлены с последними изменениями, добавляемого PnP будет.

### <a name="step-2-create-a-timer-job-class-and-add-your-timer-job-logic"></a>Шаг 2: Создание задания таймера класса и добавьте логику задания таймера ###
1. Добавьте в класс для задания таймера с именем `SimpleJob`.
2. Класс, наследуемый `TimerJob` абстрактный базовый класс.
3. В конструкторе имя задания таймера (`base("SimpleJob")`) и подключение `TimerJobRun` обработчик событий.
4. Добавьте логику задания таймера для `TimerJobRun` обработчик событий.

Результатом будет следующим образом:
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using OfficeDevPnP.Core.Framework.TimerJobs;

namespace Core.TimerJobs.Samples.SimpleJob
{
    public class SimpleJob: TimerJob
    {
        public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }

        void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
    }
}
```

### <a name="step-3-update-programcs-to-use-the-timer-job"></a>Шаг 3: Обновление Program.cs использования задания таймера ###
По-прежнему требуется выполнение задания таймера, созданных на предыдущем шаге. Для этого обновления `Program.cs` , выполните следующие действия:

1. Создайте экземпляр класса задания таймера.
2. Введите сведения проверки подлинности для задания таймера. В этом примере используется имя пользователя и пароль для проверки подлинности SharePoint Online.
3. Добавление одного или нескольких сайтов для программы задания таймера для доступа. В этом примере используется подстановочный знак в URL-адрес. Задание таймера, которое будет выполняться на всех сайтах, которые соответствуют этот URL-адрес подстановочным знаком.
4. Запуск задания таймера, вызвав `Run` метод.

```C#
static void Main(string[] args)
{
    // Instantiate the Timer Job class
    SimpleJob simpleJob = new SimpleJob();
    
    // The provided credentials need access to the site collections you want to use
    simpleJob.UseOffice365Authentication("user@tenant.onmicrosoft.com", "pwd");

    // Add one or more sites to operate on
    simpleJob.AddSite("https://<tenant>.sharepoint.com/sites/d*");
    
    // Run the job
    simpleJob.Run();
}
```

## <a name="timer-job-deployment-options"></a>Параметры развертывания задания таймера ##
Предыдущее действие демонстрируется простой задания таймера. Следующим шагом является развертывание задания таймера.

Задание таймера: .exe файла, который необходимо запланировать на платформы размещения. В зависимости от выбранной платформы размещения отличается развертывания. Варианты платформы размещения два наиболее распространенных в следующих разделах:
- Использование Microsoft Azure в качестве платформы размещения
- Использование Windows Server в качестве платформы размещения

### <a name="deploying-timer-jobs-to-microsoft-azure-using-azure-webjobs"></a>Развертывание заданий таймера в Microsoft Azure с использованием Azure WebJobs ###
Перед развертыванием задания таймера, убедитесь, что задание можно запустить без взаимодействия с пользователем. Примеры в этой статье предлагать пользователю указать пароль или clientsecret (Дополнительные возможности **проверки подлинности**) котором работает во время тестирования но не будут работать при развертывании. Все существующие образцы разрешает пользователю указать пароль или clientsecret с помощью `app.config` файла:

```XML
  <appSettings>
    <add key="user" value="user@tenant.onmicrosoft.com"/>
    <add key="password" value="your password goes here!"/>
    <add key="domain" value="Contoso"/>
    <add key="clientid" value="a4cdf20c-3385-4664-8302-5eab57ee6f14"/>
    <add key="clientsecret" value="your clientsecret goes here!"/>
  </appSettings>
```

После добавления этих изменений `app.config` файл, запустите задание таймера из Visual Studio, чтобы убедиться, что он работает без взаимодействия с пользователем. 

Фактические развертывания в Azure основан на задания Web Azure. Чтобы развернуть в этом примере задание таймера, выполните следующие действия.

1. Щелкните правой кнопкой мыши проект в Visual Studio и выберите пункт **Опубликовать как Azure WebJob...**
2. Укажите расписание для задания таймера и нажмите **кнопку ОК**
3. Выберите **Веб-сайты Microsoft Azure** в качестве назначения публикации. Вам потребуется войти в систему в Azure и выберите веб-сайта Azure, используемом для задания таймера (можно также создать новый Если, который необходимо было)
4. Нажмите кнопку **Опубликовать** , чтобы push-WebJob в Azure
5. После публикации задания таймера можно запустить задание и проверьте выполнение задания из Visual Studio или [портала управления Azure](https://manage.windowsazure.com).

![Портала управления Azure](media/timerjob-framework/4xDUvXv.png)

Кроме того задания таймера можно выполнять с новой [Azure портала](https://portal.azure.com) , выберите задание и выберите **выполнить**. Дополнительные сведения о том, как работать с WebJobs в новый портал можно найти в статье, [запустите фоновых задач с WebJobs](https://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).

![Портал Azure](media/timerjob-framework/n4wGS5x.png)

**Примечание:** Подробная информация о развертывании WebJob Azure в разделе [Приступая к работе с azure WebJobs («задания таймера») для сайтов Office 365](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md). 

### <a name="deploying-timer-jobs-to-windows-server-using-the-windows-scheduler"></a>Развертывание задания таймера для Windows Server с помощью планировщика заданий Windows ###
При развертывании Windows Server, задание таймера, которое должно выполняться без взаимодействия с пользователем. Изменение `app.config` файлов, как описано в **Развертывание заданий таймера в Microsoft Azure с использованием Azure WebJobs**. 

Скопируйте версии выпуска задания вы должны быть выполнены сервере. **Важные:** Копирование всех соответствующих сборок, файлов .exe и config-файла убедитесь, что задание можно запустить на сервере без установки дополнительных файлов или программ на сервере. 

Планирование выполнения задания таймера. Рекомендуется использовать встроенный [Планировщик задач Windows](https://technet.microsoft.com/en-us/library/cc721871.aspx). Чтобы использовать планировщик задач Windows, выполните следующие действия:

1. Откройте планировщик заданий (панель управления -> планировщик заданий).
2. Щелкните **Создать задачу** и укажите имя и учетную запись, которая будет выполнять задачи.
3. Щелкните **триггеры** и добавить новый триггер. Укажите расписание, которое необходимо использовать для задания таймера.
4. Нажмите кнопку **действия** и выберите действие «Запустите программу», выберите файл .exe задание таймера и укажите время начала в папке.
5. Нажмите **кнопку ОК** , чтобы сохранить задачу.

![Планировщик заданий Windows](media/timerjob-framework/hkRc0Bo.png)

## <a name="timer-job-framework-in-depth"></a>Подробные Framework задания таймера ##
В этом разделе сведения о том, как функции Framework задания таймера и как это работает.

### <a name="structure"></a>Структура ###
`TimerJob` Класс — абстрактный базовый класс, который содержит следующие общие свойства, методы и события:

![Структура класса задания таймера](media/timerjob-framework/4XsZ1pN.png)

Большинство свойств и методов будет описано в следующих разделах более подробно. Остальные свойства и методы, описанные здесь:

- Свойство **IsRunning** : возвращает значение, указывающее, выполняется ли задание таймера. Значение **true,** Если выполнение; **значение false,** Если не выполняется.
- Свойство **Name** : Возвращает имя задания таймера. Имя изначально набора в конструкторе задания таймера.
- Свойство **SharePointVersion** : Получает или задает версию SharePoint. Это свойство автоматически устанавливается на основе версии загруженных Microsoft.SharePoint.Client.dll и вообще не изменятся. Тем не менее, можно изменить это свойство, в случае, если требуется для примера использования библиотек CSOM v16 в v15 развертывания (локально).
- Свойство **Version** : Получает версию этого задания таймера. Версия не задано в конструкторе задание таймера или параметры по умолчанию для версии 1.0, если не задано с помощью конструктора.

Чтобы подготовить для задания таймера, вы запустите необходимо **настроить** первый его:

1. Укажите параметры **проверки подлинности** .
2. Укажите **область**, в которой приведен список сайтов.
3. При необходимости задайте значения **Задания таймера**.

С точки зрения выполнения следующие общие действия, предпринимаемые при работы выполнения задания таймера:

1. **Разрешения сайтов**: URL-адреса сайтов подстановочным знаком (например, https://tenant.sharepoint.com/sites/d *) заменяются на фактический список существующих сайтов. Если развертывание сайта sub был запрошен со всеми сайтами sub развернут в список разрешенных узлов.
2. **Создание пакетов работы** на основе текущего treading параметров и создайте один поток в пакете.
3. **Потоки выполнения работы пакетов** и вызова `TimerJobRun` событий для каждого сайта в списке.

Дополнительные сведения о каждом шаге можно найти ниже.

### <a name="authentication"></a>Проверка подлинности ###
Прежде чем можно будет использовать задания таймера задание таймера, которое необходимо знать, как выполнить проверку подлинности на SharePoint. Платформа в настоящее время поддерживает подходов в перечисления **AuthenticationType** . **Office 365**, **NetworkCredentials** и **AppOnly**. С помощью методов ниже иллюстрируется автоматически устанавливает свойство **AuthenticationType** соответствующее значение **Office 365**, **NetworkCredentials** и **AppOnly**. Блок-схема ниже показаны шаги. Подробное объяснение на каждый подход находятся ниже.

![Блок-схема шаги проверки подлинности](media/timerjob-framework/rt4dZa3.png)

#### <a name="user-credentials"></a>Учетные данные пользователя ####
Чтобы указать учетные данные пользователя для работы с **Office 365** можно использовать эти методы 2:
```C#
public void UseOffice365Authentication(string userUPN, string password)
public void UseOffice365Authentication(string credentialName)
```

Первый метод просто принимает имя пользователя и пароль. Второй позволяет указать универсальный учетные данные, хранящиеся в диспетчере учетных данных Windows. Снимок экрана ниже показано `bertonline` универсальный учетных данных. Чтобы использовать ее для проверки подлинности задание таймера, предоставляют «bertonline» в качестве параметра метода второй.

![Диспетчер учетных данных Windows](media/timerjob-framework/HdqvsHy.png)

Существует аналогичные методы для работы с **SharePoint локально**.
```C#
public void UseNetworkCredentialsAuthentication(string samAccountName, string password, string domain)
public void UseNetworkCredentialsAuthentication(string credentialName)
```

#### <a name="app-only"></a>Только приложения ####
Приложение только — **предпочтительный способ** как может предоставить разрешения уровня клиента. Учетные данные пользователя для учетной записи пользователя должны быть необходимые разрешения. 

**Примечание:** Определенные веб-сайтов разрешения логику не работы с проверкой подлинности только для приложений. Подробные сведения можно найти в следующем разделе. 

Чтобы настроить задание для проверки подлинности только для приложений, используйте один из следующих методов:
```C#
public void UseAppOnlyAuthentication(string clientId, string clientSecret)
public void UseAzureADAppOnlyAuthentication(string clientId, string clientSecret)
```

Тот же метод можно использовать для Office 365 или SharePoint локальных что делает задания таймера с помощью только проверки подлинности легко портативных между средами.

**Примечание:** При использовании только логику задание таймера не удается при использовании API-интерфейсы, которые не работают с **AuthenticationType.AppOnly**. Типичные примеры — это API поиска, записи в хранилище данных таксономии и с помощью API профилей пользователей.

### <a name="sites-to-operate-on"></a>Сайты для работы с ###
После запуска задания таймера должно одного или нескольких сайтов должно выполняться. Чтобы добавить сайты задания таймера, используйте ниже набор методов.

```C#
public void AddSite(string site)
public void ClearAddedSites()
```

Чтобы добавить сайт, укажите полный URL-адрес (например, https://tenant.sharepoint.com/sites/dev) или URL-адрес подстановочным знаком. URL-адрес подстановочным знаком — это URL-адрес, который заканчивается на * (только один одним * может должно являться последнего символа, URL-адрес). — Это URL-адрес примера подстановочных https://tenant.sharepoint.com/sites/ *, которая возвращает **все** семейства веб-сайтов под управляемый путь из этого сайта. Другой пример https://tenant.sharepoint.com/sites/dev * возвращает все семейства сайтов которых содержит URL-адрес «dev».

Обычно сайты добавляются по программам, создает экземпляр объекта задания таймера, но при необходимости задание таймера, которое может принимать контроль над переданный список сайтов. Это можно сделать, добавив переопределение метода для `UpdateAddedSites`виртуальный метод, как показано в примере ниже:

```C#
public override List<string> UpdateAddedSites(List<string> addedSites)
{
    // Let's assume we're not happy with the provided list of sites, so first clear it
    addedSites.Clear();

    // Manually adding a new wildcard Url, without an added URL the Timer Job will do...nothing
    addedSites.Add("https://bertonline.sharepoint.com/sites/d*");

    // Return the updated list of sites
    return addedSites;
}
```

После добавления подстановочных URL-адрес и параметры проверки подлинности только для приложений, укажите учетные данные перечисление. Чтобы получить список семейств веб-сайтов, используемые в алгоритм сопоставления сайта для возврата реальных список сайтов используются учетные данные перечисление. Для получения списка семейств веб-сайтов framework таймера будет отличаться от Office 365 (v16) и локальной (v15):
- Office 365: `Tenant.GetSiteProperties` метод используется для чтения «периодически» семейств, API поиска используется для чтения OneDrive для бизнеса семейств веб-сайтов.
- Локальные: API поиска используется для чтения всех семейств веб-сайтов.

API поиска не работает с помощью контекста пользователя, что задание таймера, которое будет использоваться учетные данные указанного перечисления. 

Чтобы указать учетные данные пользователя для работы с **Office 365** можно использовать эти методы 2:
```C#
public void SetEnumerationCredentials(string userUPN, string password)
public void SetEnumerationCredentials(string credentialName)
```

Существует аналогичные методы для работы с **SharePoint локально**.
```C#
public void SetEnumerationCredentials(string samAccountName, string password, string domain)
public void SetEnumerationCredentials(string credentialName)
```

Первый метод просто принимает имя пользователя, пароль и при необходимости домена (в локальном). Второй — задает универсальный учетные данные, хранящиеся в диспетчере учетных данных Windows. Обратитесь к главе **проверки подлинности** для получения дополнительных сведений о диспетчере учетных данных.

#### <a name="sub-site-expanding"></a>Развертывание веб-узла ####
Часто требуется код задания таймера для выполнения корневого сайта семейства веб-сайтов и всех вложенных сайтов этого семейства веб-сайтов. Чтобы сделать это, присвойте свойству **ExpandSubSites** значение **true**. Это приведет к задания таймера для разверните узел сайты sub как часть узла, разрешение шаг.

#### <a name="override-resolved-andor-expanded-sites"></a>Переопределение разрешения и/или расширенное сайтов ####
Framework таймера обрабатывает шаблонами сайтов и при необходимости разворачивает сайты sub, следующий шаг после обработки в список сайтов. До начала обработки в список сайтов, может возникнуть необходимость изменить список сайтов. Например может потребоваться удаление определенных сайтов или добавить несколько узлов в список. Это можно сделать путем переопределения `ResolveAddedSites` виртуальный метод. В этом примере показано, как переопределить `ResolveAddedSites` метод для удаления одного сайта из списка. 

```C#
public override List<string> ResolveAddedSites(List<string> addedSites)
{
    // Use default TimerJob base class site resolving
    addedSites = base.ResolveAddedSites(addedSites);

    //Delete the first one from the list...simple change. A real life case could be reading the site scope 
    //from a SQL (Azure) DB to prevent the whole site resolving. 
    addedSites.RemoveAt(0);

    // return the updated list of resolved sites...this list will be processed by the Timer Job
    return addedSites;
}
```

### <a name="timerjobrun-event"></a>Событие TimerJobRun ###
Список сайтов разделяет Framework задания таймера на рабочих пакетов. Каждый пакет сайтов будет выполняться в отдельном потоке. По умолчанию платформа будет создавать пять пакетов и пять потоков для запуска этих пять пакетов. Чтобы узнать больше о threading параметры задания таймера в разделе **работы с потоками** . Когда поток обрабатывает пакет `TimerJobRun` событие инициируется framework таймера и будет предоставлять все необходимые сведения для выполнения задания таймера. Задания таймера выполняются как события, поэтому код необходимо подключить обработчик событий для `TimerJobRun` событий:

```C#
public SimpleJob() : base("SimpleJob")
{
    TimerJobRun += SimpleJob_TimerJobRun;
}

void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
{
    // your Timer Job logic goes here
}
```

Альтернативный подход с помощью делегата встроенного как показано ниже:

```C#
public SimpleJob() : base("SimpleJob")
{
    // Inline delegate
    TimerJobRun += delegate(object sender, TimerJobRunEventArgs e)
    {
        // your Timer Job logic goes here
    };
}
```

При `TimerJobRun` вызывает событие, вы получаете `TimerJobRunEventArgs` объект, который предоставляет сведения, необходимые для запись логику задания таймера. В этом классе доступны следующие атрибуты и методы:

![Структура класса TimerJobRunEventArgs](media/timerjob-framework/CRFBdwS.png)

Некоторые свойства и все методы, используемых в функции управления необязательно состояний, которая будет описан в следующем разделе. Тем не менее следующие свойства всегда будут доступны в все события, вне зависимости от конфигурации:
- Свойство **URL-адрес** : Получает или задает URL-адрес сайта для задания таймера для работы. Это может быть корневого сайта семейства веб-сайтов, но это может быть веб-узла в случае, если развертывание сайта было сделано.
- Свойство **ConfigurationData** : Получает или задает данные конфигурации задания таймера дополнительных (не обязательно). Эти данные конфигурации передается как часть `TimerJobRunEventArgs` объекта.
- Свойство **WebClientContext** : Получает или задает `ClientContext` объекта для текущего URL-адреса. Это свойство соответствует `ClientContext` объекта для сайта, определенного в свойстве *URL-адрес* . Обычно это `ClientContext` объект, который можно использовать в коде задания таймера.
- Свойство **SiteClientContext** : Получает или задает `ClientContext` объект для корневого сайта семейства веб-сайтов. Это свойство предоставляет доступ к корневому сайту задание таймера, которое требуется доступ к нему. Например задание таймера, которое можно добавить в макет страниц в коллекции главных страниц, с помощью свойства *SiteClientContext* .
- Свойство **TenantClientContext** : Получает или задает `ClientContext` объекта для работы с API клиента. Это свойство предоставляет `ClientContext`объект, созданный с помощью URL-адрес сайта администрирования клиентов. Для использования `Tenant` API в задание таймера `TimerJobRun` обработчик события создания нового `Tenant` объектов с помощью этого свойства TenantClientContext.

Все `ClientContext`объекты используют данные проверки подлинности, описанных в разделе **тип проверки подлинности** . Если вы удалили учетных данных пользователя Убедитесь, что используется учетная запись имеет необходимые разрешения для работы указанные веб-сайты. При использовании только для приложений, рекомендуется задать разрешения на уровне клиента участнику только для приложений.

### <a name="state-management"></a>Управление состоянием ###
При создании задания таймера логики часто требуется сохранить состояние. Например, для записи при последней обработки сайта или для хранения данных для поддержки бизнес-логикой. Задание таймера. По этой причине Framework задания таймера имеет возможности управления состояние. Управление состоянием хранит и получает набор стандартных и пользовательских свойств виде строки JSON сериализованным в контейнере свойств web обработанные узла (имя = имя задания таймера + «_Properties»). Ниже перечислены свойства по умолчанию `TimerJobRunEventArgs`объектов:
- Свойство **PreviousRun** : Получает или задает дату и время предыдущей процедуры.
- Свойство **PreviousRunSuccessful** : Получает или задает значение, указывающее, успешно ли предыдущего запуска. Обратите внимание на то, что задание таймера автора несет ответственность за Пометка задания, как успешно завершиться, задав свойство **CurrentRunSuccessful** как часть задания таймера внедрения
- Свойство **PreviousRunVersion** : Получает или задает версию предыдущего запуска задания таймера.

Рядом с пунктом эти стандартными свойствами имеется также параметр, чтобы указать свои собственные свойства путем добавления ключевого слова - пары значение `Properties` коллекцию `TimerJobRunEventArgs`объекта. Чтобы облегчить существует три способа, которые помогут вам:
- **SetProperty** добавляет или обновляет свойство.
- **GetProperty** возвращает значение свойства.
- **DeleteProperty** Удаляет свойство из коллекции свойств.

В следующем коде показано, как можно использовать управление состоянием:

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // grab reference to list
        library = "SiteAssets";
        List list = e.WebClientContext.Web.GetListByUrl(library);

        if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
        {
            if (list == null)
            {
                // grab reference to list
                library = "Style%20Library";
                list = e.WebClientContext.Web.GetListByUrl(library);
            }

            if (list != null)
            {
                // upload js file to list
                list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                e.SetProperty("ScriptFileVersion", "1.0");
            }
        }

        if (admins.Count < 2)
        {
            // Oops, we need at least 2 site collection administrators
            e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
            Console.WriteLine("Site {0} marked as incompliant!", e.Url);
            e.SetProperty("SiteCompliant", "false");
        }
        else
        {
            // We're all good...let's remove the notification
            e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
            Console.WriteLine("Site {0} is compliant", e.Url);
            e.SetProperty("SiteCompliant", "true");
        }

        e.CurrentRunSuccessful = true;
        e.DeleteProperty("LastError");
    }
    catch(Exception ex)
    {
        e.CurrentRunSuccessful = false;
        e.SetProperty("LastError", ex.Message);
    }
}
```

Состояние хранятся как одного JSON сериализованным свойство означает его можно использовать, а также другие настройки. Например, если создавал записи состояния задания таймера «SiteCompliant = false», JavaScript подпрограммы может предложить пользователю действовать, так как задание таймера, которое определено, что сайт был incompliant.

### <a name="threading"></a>Работа с потоками ###
Framework задания таймера по умолчанию используется для параллельного выполнения рабочих потоков. Threading служит для обоих sub сайта расширения (по запросу), а также для выполнения фактических логики задания таймера (`TimerJobRun` события) для каждого сайта. Следующие свойства могут быть использованы для управления реализация потоков:
- Свойство **UseThreading** : Получает или задает значение, указывающее, является ли threading будет использоваться. По умолчанию используется значение **true**.  Установите значение **false** , чтобы выполнить все действия с помощью основной поток приложения.
- Свойство **MaximumThreads** : Получает или задает число потоков, используемых для этого задания таймера. Допустимые значения: 2 до 100. Значение по умолчанию равно 5. Наличие большое количество потоков не обязательно быстрее, а затем всего несколько потоков. Оптимальное число должна быть получена посредством тестирования с использованием различных число потоков. По умолчанию 5 потоков обнаружило значительно повысить производительность в большинстве случаев. 

#### <a name="throttling"></a>Регулирование ####
Так как задание таймера с помощью threading и операции задания таймера, обычно выполняются операции связано со значительными затратами ресурсов, может регулирование выполнения задания таймера. Чтобы правильно иметь дело с регулирование Framework задания таймера и целые использует PnP основных `ExecuteQueryRetry` метод вместо по умолчанию `ExecuteQuery`метод.

**Примечание:** Необходимо использовать `ExecuteQueryRetry` в коде реализации задания таймера.

#### <a name="concurrency-issues---process-all-sub-sites-of-a-site-collection-in-the-same-thread"></a>Проблемы параллелизма — обрабатывать все сайты sub семейства веб-сайтов в том же потоке ####

Задания таймера могут возникнуть проблемы параллелизма при использовании нескольких потоков для обработки вложенных сайтов. Выполните в этом примере: поток A обрабатывает первого набора sub сайты из семейства веб-сайтов 1 и поток B обрабатывает rest sub сайты из семейства веб-сайтов 1. Если задание таймера, которое обрабатывает веб-узла и корневого сайта (с помощью `SiteClientContext` объект), начиная с оба потока A может быть проблема параллелизма и поток B обрабатывать корневого сайта. Чтобы предотвратить использование параллельного проблему (без запуска задания таймера в один поток) `GetAllSubSites` метод задания таймера.

Следующий код демонстрирует использование `GetAllSubSites` метод в рамках задания таймера:

```C#
public class SiteCollectionScopedJob: TimerJob
{
    public SiteCollectionScopedJob() : base("SiteCollectionScopedJob")
    {
        // ExpandSites *must* be false as we'll deal with that at TimerJobEvent level
        ExpandSubSites = false;
        TimerJobRun += SiteCollectionScopedJob_TimerJobRun;
    }

    void SiteCollectionScopedJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
    {
        // Get all the sub sites in the site we're processing
        IEnumerable<string> expandedSites = GetAllSubSites(e.SiteClientContext.Site);

        // Manually iterate over the content
        foreach (string site in expandedSites)
        {
            // Clone the existing ClientContext for the sub web
            using (ClientContext ccWeb = e.SiteClientContext.Clone(site))
            {
                // Here's the Timer Job logic, but now a single site collection is handled in a single thread which 
                // allows for further optimization or prevents race conditions
                ccWeb.Load(ccWeb.Web, s => s.Title);
                ccWeb.ExecuteQueryRetry();
                Console.WriteLine("Here: {0} - {1}", site, ccWeb.Web.Title);
            }
        }
    }
}
```

### <a name="logging"></a>Ведение журнала ###
Framework задание таймера используется ведения журнала PnP основных компонентов в его составе PnP основной библиотеки. Для активации встроенных PnP основных ведения журнала, настройте его с помощью файла соответствующие конфигурации (app.config или web.config). В следующем примере показано требуется следующий синтаксис:

```XML
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="DebugListenter" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log" />
        <!--<add name="consoleListener" type="System.Diagnostics.ConsoleTraceListener" />-->
      </listeners>
    </trace>
  </system.diagnostics>
```

С помощью выше файла конфигурации Framework задание таймера будет использовать `System.Diagnostics.TextWriterTraceListener` для записи журналов в файл с именем trace.log в ту же папку .exe задания таймера. Например, доступны другие слушателям трассировки:
- **ConsoleTraceListener** записывает журналы на консоль.
- Способов, описанных в [Облаке Диагностика - вступили в элемент управления из ведения журналов и трассировки в Windows Azure](https://msdn.microsoft.com/en-us/magazine/ff714589.aspx). Этот метод используется Microsoft.WindowsAzure.Diagnostics. **DiagnosticMonitorTraceListener**. Здесь можно найти дополнительные ресурсы Azure:
    - [Включение сбора данных диагностики для веб-сайтов Azure](http://azure.microsoft.com/en-us/documentation/articles/web-sites-enable-diagnostic-log/)
    - [Устранение неполадок в Azure веб-сайтов в Visual Studio](http://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

Настоятельно рекомендуется использовать такой же подход ведения журнала для свой код задания таймера, как для Framework задания таймера. В код задания таймера можно использовать PnP основных `Log` классов:

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // Additional Timer Job logic...

        e.CurrentRunSuccessful = true;
        e.DeleteProperty("LastError");
    }
    catch(Exception ex)
    {
        Log.Error("SiteGovernanceJob", "Error while processing site {0}. Error = {1}", e.Url, ex.Message);
        e.CurrentRunSuccessful = false;
        e.SetProperty("LastError", ex.Message);
    }
}
```
